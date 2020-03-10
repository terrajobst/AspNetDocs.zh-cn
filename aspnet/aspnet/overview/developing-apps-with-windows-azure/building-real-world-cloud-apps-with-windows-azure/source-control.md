---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: 源代码管理（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: 5a1e0d7cd3c396d4be79c8958422602055eb3db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500528"
---
# <a name="source-control-building-real-world-cloud-apps-with-azure"></a>源代码管理（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅[第一章](introduction.md)。

源代码管理对于所有云开发项目（而不仅仅是团队环境）都是必不可少的。 您不想编辑源代码，甚至无需使用 undo 函数和自动备份的 Word 文档，而且源代码管理可在项目级提供这些函数，在这种情况下，在出现错误时，它们可以节省更多的时间。 使用云源代码管理服务，你无需担心复杂的设置，你可以免费使用最多5个用户的 Azure Repos 源代码管理。

本章的第一部分介绍了需要注意的三个关键最佳方案：

- 将[自动化脚本视为源代码](#scripts)，并将其与应用程序代码结合在一起。
- [切勿将机密](#secrets)（敏感数据，如凭据）签入到源代码存储库中。
- [设置源分支](#devops)以启用 DevOps 工作流。

本章的其余部分提供 Visual Studio、Azure 和 Azure Repos 中这些模式的一些示例实现：

- [向 Visual Studio 中的源代码管理添加脚本](#vsscripts)
- [在 Azure 中存储敏感数据](#appsettings)
- [在 Visual Studio 中使用 Git 并 Azure Repos](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a>将自动化脚本视为源代码

当你在云项目上工作时，你会经常更改操作，并且你希望能够快速应对你的客户报告的问题。 响应速度很快涉及使用自动化脚本，如 "[自动化一切](automate-everything.md)" 一章中所述。 需要与应用程序源代码同步，用于创建你的环境、部署到该环境、进行缩放、扩展等的所有脚本。

若要使脚本与代码保持同步，请将脚本存储在源代码管理系统中。 然后，如果您需要回滚更改或快速修复与开发代码不同的生产代码，则无需浪费时间来尝试跟踪已更改的设置或哪些团队成员拥有所需版本的副本。 您可以确信，所需的脚本与需要它们的基本代码同步，并确保所有团队成员都能使用相同的脚本。 然后，无论是否需要将热修补程序自动部署和部署到生产环境或新功能开发中，都可以使用正确的脚本来编写需要更新的代码。

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a>不签入机密

通常很多人都可以访问源代码存储库，因为它是敏感数据（如密码）的适当安全位置。 如果脚本依赖于机密（如密码），请将这些设置参数化，使其不会保存在源代码中，并将机密存储在其他位置。

例如，Azure 允许你下载包含发布设置的文件，以便自动创建发布配置文件。 这些文件包括有权管理 Azure 服务的用户名和密码。 如果你使用此方法创建发布配置文件，并且将这些文件签入到源代码管理，则可以访问存储库的任何人都可以看到这些用户名和密码。 您可以安全地将密码存储在发布配置文件中，因为它已加密，并且位于默认情况下不包含在源控件中的 *.pubxml*文件中。

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a>用于促进 DevOps 工作流的结构源分支

你在存储库中实现分支的方式会影响你开发新功能和解决生产中的问题的能力。 下面是大量中型团队使用的一种模式：

![源分支结构](source-control/_static/image1.png)

主分支始终与生产中的代码匹配。 Master 下的分支对应开发生命周期中的不同阶段。 开发分支是实现新功能的地方。 对于小团队而言，你可能只是具有母版和开发，但我们通常建议用户在开发和主服务器之间具有过渡分支。 在将更新转移到生产环境之前，可以使用过渡进行最终集成测试。

对于大型团队，每个新功能可能有单独的分支;对于较小的团队，你可能会让每个人都签入开发分支。

如果每个功能都有一个分支，则当功能 A 准备就绪时，将其源代码更改向上合并到开发分支，并向下合并到其他功能分支。 此源代码合并过程可能非常耗时，若要避免这种工作，同时保持单独的功能，某些团队还实现了一种称为 " *[功能切换](http://en.wikipedia.org/wiki/Feature_toggle)* " 的替代方法（也称为*功能标志*）。 这意味着所有功能的所有代码都在相同的分支中，但你可以通过使用代码中的开关来启用或禁用每个功能。 例如，假设功能 A 是用于修复 It 应用任务的新字段，功能 B 添加了缓存功能。 这两种功能的代码可以在开发分支中进行，但在将变量设置为 true 时，应用程序将只显示新字段，并且在其他变量设置为 true 时，它将仅使用缓存。 如果功能 A 未准备好进行升级，但功能 B 已准备就绪，则可以将所有代码升级到生产，并将功能切换为 "关闭"，并打开功能 B 开关。 然后，你可以完成功能 A 并稍后升级，所有这些操作都不会合并源代码。

无论你是使用分支还是切换功能，这种类似的分支结构都使你能够以敏捷且可重复的方式将你的代码从开发环境传输到生产中。

利用此结构，你还可以快速响应客户反馈。 如果需要快速修复生产，还可以采用敏捷的方式高效地执行此操作。 你可以从主节点或过渡版创建分支，并在准备好将其合并到主分支和功能分支中。

![修补程序分支](source-control/_static/image2.png)

如果没有类似于此的分支结构与生产和开发分支分离，则生产问题可能会让你进入升级新功能代码和生产修补程序的位置。 新功能代码可能未经过充分测试并可投入生产，你可能需要执行大量工作来备份尚未准备好的更改。 或者你可能需要延迟你的修复，才能测试更改并使其做好部署准备。

接下来，你将看到有关如何在 Visual Studio、Azure 和 Azure Repos 中实现这三种模式的示例。 这些是示例，而不是详细的分步操作说明;有关提供所有必要上下文的详细说明，请参阅本章末尾的[资源](#resources)部分。

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a>向 Visual Studio 中的源代码管理添加脚本

可以通过将脚本包含在 Visual Studio 解决方案文件夹（假定项目在源代码管理中），将其添加到 Visual Studio 中的源代码管理。 下面是执行此操作的一种方法。

在解决方案文件夹中为脚本创建一个文件夹（与 *.sln*文件相同的文件夹）。

![自动化文件夹](source-control/_static/image3.png)

将脚本文件复制到该文件夹中。

![自动化文件夹内容](source-control/_static/image4.png)

在 Visual Studio 中，将解决方案文件夹添加到项目。

![新解决方案文件夹菜单选择](source-control/_static/image5.png)

并将脚本文件添加到解决方案文件夹中。

!["添加现有项" 菜单选择](source-control/_static/image6.png)

![“添加现有项”对话框](source-control/_static/image7.png)

脚本文件现在已包含在项目中，源代码管理正在跟踪其版本更改以及相应的源代码更改。

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a>在 Azure 中存储敏感数据

如果在 Azure 网站中运行应用程序，避免在源代码管理中存储凭据的一种方法是将其存储在 Azure 中。

例如，Fix It 应用程序在其 Web.config 文件中存储两个将在生产中使用密码的连接字符串和一个提供对 Azure 存储帐户的访问权限的密钥。

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

如果将这些设置的实际生产值放在 web.config*文件中*，或将它们放在 web.config 文件中来*配置 web.config 转换*以便在部署过程中插入它们，它们将存储在源存储库中。 如果将数据库连接字符串输入到生产发布配置文件中，则密码将位于 *.pubxml*文件中。 （您可以从源代码管理中排除 *.pubxml*文件，但这样就失去了共享所有其他部署设置所带来的好处。）

Azure 为你提供了*web.config*文件的 " **appSettings** " 和 "连接字符串" 部分的替代方法。 下面是 Azure 管理门户中网站的 "**配置**" 选项卡的相关部分：

![门户中的 appSettings 和 connectionStrings](source-control/_static/image8.png)

将项目部署到此网站并运行应用程序时，在 Azure 中存储的任何值都会覆盖 Web.config 文件中的任何值。

可以使用管理门户或脚本在 Azure 中设置这些值。 "[自动完成所有](automate-everything.md)操作" 一章中所述的环境创建自动化脚本将创建一个 Azure SQL 数据库，获取存储和 SQL 数据库连接字符串，并将这些机密存储在网站的设置中。

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

请注意，将对脚本进行参数化，以便不会将实际值保留到源存储库。

当你在开发环境中本地运行时，应用程序将读取本地 Web.config 文件，并且你的连接字符串指向 Web 项目的*应用\_数据*文件夹中的 LocalDB SQL Server 数据库。 当你在 Azure 中运行应用程序时，如果应用程序尝试从 web.config 文件中读取这些值，则它返回并使用的值是为网站存储的值，而不是在 Web.config 文件中的实际值。

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-azure-devops"></a>在 Visual Studio 和 Azure DevOps 中使用 Git

您可以使用任何源代码管理环境来实现前面介绍的 DevOps 分支结构。 对于分布式团队而言，[分布式版本控制系统](http://en.wikipedia.org/wiki/Distributed_revision_control)（DVCS）可能效果最好;对于其他团队而言，[集中式系统](http://en.wikipedia.org/wiki/Revision_control)的工作效果可能更好。

[Git](http://git-scm.com/)是一种流行的分布式版本控制系统。 如果使用 Git 进行源代码管理，则会在本地计算机上创建该存储库的完整副本及其所有历史记录。 许多人更喜欢这样做，因为当你未连接到网络时，可以更轻松地继续工作-你可以继续执行提交和回滚、创建和切换分支等操作。 即使你连接到网络，在所有内容都是本地的时，创建分支和切换分支会更简单快捷。 你还可以执行本地提交和回滚，而不会影响其他开发人员。 并且，你可以在将提交发送到服务器之前批处理提交。

[Azure Repos](/azure/devops/repos/index?view=vsts)提供[Git](/azure/devops/repos/git/?view=vsts)和[Team Foundation 版本控制](/azure/devops/repos/tfvc/index?view=vsts)（TFVC; 集中源代码管理）。 [此处](https://app.vsaex.visualstudio.com/signup)提供 Azure DevOps 入门。

Visual Studio 2017 包含内置的一流[Git 支持](https://msdn.microsoft.com/library/hh850437.aspx)。 下面是其工作原理的简要演示。

在 Visual Studio 中打开项目后，在**解决方案资源管理器**中右键单击该解决方案，然后选择 "**将解决方案添加到源代码管理**"。

![将解决方案添加到源代码管理](source-control/_static/image9.png)

Visual Studio 会询问你是否要使用 TFVC （集中式版本控制）或 Git。

![选择源代码管理](source-control/_static/image10.png)

选择 Git 并单击 **"确定"** 时，Visual Studio 将在解决方案文件夹中创建一个新的本地 Git 存储库。 新存储库尚无文件;必须通过执行 Git commit 将它们添加到存储库。 在**解决方案资源管理器**中右键单击该解决方案，然后单击 "**提交**"。

![提交](source-control/_static/image11.png)

Visual Studio 会自动暂存提交的所有项目文件，并在 "**包含的更改**" 窗格中**团队资源管理器**列出它们。 （如果不想在提交中包含某些资源，请选择它们，右键单击，然后单击 "**排除**"。）

![Team Explorer](source-control/_static/image12.png)

输入提交注释，然后单击 "**提交**"，Visual Studio 将执行提交，并显示提交 ID。

![团队资源管理器更改](source-control/_static/image13.png)

现在，如果您更改了某些代码，使其不同于存储库中的内容，则可以轻松查看不同之处。 右键单击已更改的文件，选择 "与未**修改的比较**"，将显示一个显示未提交更改的比较显示。

![与未修改的比较](source-control/_static/image14.png)

![显示更改的差异](source-control/_static/image15.png)

你可以轻松地查看正在进行的更改并将其签入。

假设您需要创建一个分支，也可以在 Visual Studio 中执行此操作。 在**团队资源管理器**中，单击 "**新建分支**"。

![团队资源管理器新建分支](source-control/_static/image16.png)

输入分支名称，单击 "**创建分支**"，如果已选择 "**签出分支**"，则 Visual Studio 会自动签出新分支。

![团队资源管理器新建分支](source-control/_static/image17.png)

你现在可以对文件进行更改并将其签入此分支。 你可以轻松地在分支之间切换，Visual Studio 会自动将文件同步到已签出的任何分支。在此示例中， *\_布局*中的网页标题已更改为 HotFix1 分支中的 "热修复 1"。

![Hotfix1 分支](source-control/_static/image18.png)

如果切换回 master 分支， *\_的布局. cshtml*文件的内容将自动还原为它们在 master 分支中的内容。

![主分支](source-control/_static/image19.png)

这是一个简单的示例，演示如何快速创建分支，以及如何在分支之间来回切换。 此功能使用 "[自动执行所有](automate-everything.md)操作" 一章中介绍的分支结构和自动化脚本，实现了高度敏捷的工作流。 例如，你可以在开发分支中工作，从主节点创建热修复分支，切换到新分支，在那里进行更改并提交，然后切换回开发分支，并继续执行所做的操作。

您在这里看到的是如何使用 Visual Studio 中的本地 Git 存储库。 在团队环境中，通常还会将更改推送到公共存储库中。 使用 Visual Studio 工具还可以指向远程 Git 存储库。 你可以使用 GitHub.com 来实现此目的，也可以将[Git 和 Azure Repos](/azure/devops/repos/git/overview?view=vsts)与所有其他 Azure DevOps 功能（如工作项和 bug 跟踪）相集成。

当然，这并不是实现敏捷分支策略的唯一方法。 您可以使用集中式的源代码管理存储库启用相同的敏捷工作流。

## <a name="summary"></a>摘要

基于你进行更改的速度，并以安全、可预测的方式，衡量你的源代码管理系统是否成功。 如果你发现自己的恐惧进行了更改，因为你必须对其进行一次或两次手动测试，你可能会问自己必须执行的操作或测试，以便可以在几分钟内或在最糟的时间不超过1小时进行该更改。 实现此目的的一种策略是实现持续集成和持续交付，这将在[下一章](continuous-integration-and-continuous-delivery.md)中介绍。

<a id="resources"></a>
## <a name="resources"></a>资源

有关分支策略的详细信息，请参阅以下资源：

- [使用 Team Foundation Server 2012 构建发布管道](https://msdn.microsoft.com/library/dn449957.aspx)。 Microsoft 模式和实践文档。 有关分支策略的讨论，请参阅第6章。 拥护者功能会切换功能分支，并且如果使用功能的分支，则会使它们保持短暂生存期（最多小时或天）。
- [版本控制指南](https://aka.ms/vsarsolutions)。 ALM Rangers 的分支策略指南。 请参阅 "下载" 选项卡上的分支策略。
- [通过功能切换进行软件开发](https://msdn.microsoft.com/magazine/dn683796.aspx)。 MSDN 杂志文章。
- [功能切换](http://martinfowler.com/bliki/FeatureToggle.html)。 圣马丁 Fowler 的博客上的功能切换/功能标志简介。
- [功能切换 Vs 功能分支](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx)。 有关功能的另一篇博客文章 Dylan Smith。

有关如何处理不应保留在源代码管理存储库中的敏感信息的详细信息，请参阅以下资源：

- [将密码和其他敏感数据部署到 ASP.NET 和 Azure App Service 的最佳实践](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md)。
- [Azure 网站：应用程序字符串和连接字符串的工作原理](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)。 说明替代*web.config*文件中 `appSettings` 和 `connectionStrings` 数据的 Azure 功能。
- [Azure 网站中的自定义配置和应用程序设置-具有 Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/)。

有关将敏感信息保留在源代码管理之外的其他方法的信息，请参阅[ASP.NET MVC：将专用设置保留在源代码管理之外](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx)。

> [!div class="step-by-step"]
> [上一页](automate-everything.md)
> [下一页](continuous-integration-and-continuous-delivery.md)
