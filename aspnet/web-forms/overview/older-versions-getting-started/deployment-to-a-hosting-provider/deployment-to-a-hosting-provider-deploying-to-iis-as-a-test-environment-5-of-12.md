---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：作为测试环境部署到 IIS-5/12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: 5d85232ff2cb229d771d517db7173721c9e277bf
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633467"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：作为测试环境部署到 IIS-第5个（共12个）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

本教程介绍如何将 ASP.NET web 应用程序部署到本地计算机上的 IIS。

开发应用程序时，通常在 Visual Studio 中运行该应用程序。 默认情况下，这意味着你使用的是 Visual Studio 开发服务器（也称为 Cassini）。 使用 Visual Studio 开发服务器，可以在 Visual Studio 中进行开发时轻松地进行测试，但它不像 IIS 那样正常工作。 因此，当你在 Visual Studio 中测试应用程序时，该应用程序可能会正常运行，但在宿主环境中将其部署到 IIS 时，它会失败。

可以通过以下方式更可靠地测试应用程序：

1. 在开发过程中，当你在 Visual Studio 中测试时，请使用 IIS Express 或完整 IIS 而不是 Visual Studio 开发服务器。 此方法通常可以更准确地模拟网站在 IIS 下的运行方式。 但是，此方法不会测试你的部署过程，也不会验证部署过程的结果是否能正常运行。
2. 使用你稍后将其部署到生产环境的相同过程，将应用程序部署到你的开发计算机上的 IIS。 此方法验证你的部署过程，以及验证你的应用程序是否能在 IIS 下正确运行。
3. 将应用程序部署到尽可能接近生产环境的测试环境。 由于这些教程的生产环境是第三方托管提供商，因此理想的测试环境是托管提供商的第二个帐户。 此第二个帐户仅用于测试，但其设置方式与生产帐户相同。

本教程介绍选项2的步骤。 在[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程的末尾提供了有关选项3的指南，并在本教程结束时，还提供了有关选项1的资源的链接。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="configuring-the-application-to-run-in-medium-trust"></a>将应用程序配置为在中等信任环境中运行

在安装 IIS 并部署到它之前，你将更改 Web.config 文件设置，以使该站点在典型的共享宿主环境中运行得更类似。

宿主提供程序通常在*中等信任环境*下运行你的网站，这意味着不允许这样做。 例如，应用程序代码不能访问 Windows 注册表，也无法读取或写入您的应用程序的文件夹层次结构之外的文件。 默认情况下，你的应用程序在本地计算机上以*高信任*方式运行，这意味着应用程序可以执行在将其部署到生产环境时失败的操作。 因此，为了使测试环境更准确地反映生产环境，需要将应用程序配置为在中等信任环境下运行。

在应用程序的 web.config 文件中，在**system.web**元素中添加一个**信任**元素，如本示例中所示。

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

现在，应用程序将在 IIS 中的中等信任环境中运行，即使在本地计算机上也是如此。 此设置使你可以尽早地捕获应用程序代码对生产中可能会失败的操作的任何尝试。

> [!NOTE]
> 如果使用 Entity Framework Code First 迁移，请确保已安装版本5.0 或更高版本。 在实体框架版本4.3 中，迁移需要完全信任才能更新数据库架构。

## <a name="installing-iis-and-web-deploy"></a>安装 IIS 和 Web 部署

若要在开发计算机上部署到 IIS，你必须安装 IIS 和 Web 部署。 默认的 Windows 7 配置中不包括这些配置。 如果你已经安装了 IIS 和 Web 部署，请跳到下一部分。

使用[Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)是安装 iis 和 Web 部署的首选方式，因为 Web 平台安装程序将为 iis 安装推荐的配置，并在必要时自动安装 iis 和 Web 部署的必备组件。

若要运行 Web 平台安装程序来安装 IIS 和 Web 部署，请使用以下链接。 如果你已经安装了 IIS、Web 部署或任何所需的组件，Web 平台安装程序将仅安装缺少的内容。

- [使用 WebPI 安装 IIS 和 Web 部署](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a>将默认应用程序池设置为 .NET 4

安装 IIS 后，请运行**Iis 管理器**以确保将 .NET Framework 版本4分配给默认应用程序池。

在 Windows 的 "**开始**" 菜单中，选择 "**运行**"，输入 "inetmgr"，然后单击 **"确定**"。 （如果 "**运行**" 命令不在 "**开始**" 菜单中，则可以按 Windows 键和 R 打开它。 或者右键单击任务栏，单击 "**属性**"，选择 "**开始" 菜单**选项卡，单击 "**自定义**"，然后选择 "**运行命令**"。）

在 "**连接**" 窗格中，展开服务器节点，然后选择 "**应用程序池**"。 在 "**应用程序池**" 窗格中，如果将**DefaultAppPool**分配给 .net framework 版本4（如下图所示），请跳到下一部分。

[![Inetmgr_showing_4。0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

如果只看到两个应用程序池，并且两个应用程序池都设置为 .NET Framework 2.0，则必须在 IIS 中安装 ASP.NET 4：

- 右键单击 Windows "**开始**" 菜单中的 "**命令提示符**"，然后选择 "以**管理员身份运行**"，打开 "命令提示符" 窗口。 然后使用以下命令运行[aspnet\_regiis](https://msdn.microsoft.com/library/k6h9cz8h.aspx)在 IIS 中安装 ASP.NET 4。 （在64位系统中，将 "Framework" 替换为 "Framework64"。）

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [![aspnet_regiis_installing_ASP。 NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    此命令为 .NET Framework 4 创建新的应用程序池，但默认应用程序池仍将设置为2.0。 需要将面向 .NET 4 的应用程序部署到该应用程序池，因此必须将应用程序池更改为 .NET 4。

如果关闭了**IIS 管理器**，请再次运行它，展开服务器节点，然后单击 "**应用程序池**" 再次显示 "**应用程序池**" 窗格。

在 "**应用程序池**" 窗格中单击 " **DefaultAppPool**"，然后在 "**操作**" 窗格中单击 "**基本设置**"。

[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

在 "**编辑应用程序池**" 对话框中，将 **.NET Framework 版本**更改为 " **.NET Framework v 4.0.30319** "，然后单击 **"确定"** 。

[![Selecting_。 NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

你现在已准备好发布到 IIS。

## <a name="publishing-to-iis"></a>发布到 IIS

可以通过多种方式使用 Visual Studio 2010 和 Web 部署进行部署：

- 使用 Visual Studio 一键式发布。
- 创建*部署包*，并使用 IIS 管理器 UI 安装它。 部署包包含 *.zip*文件，该文件包含在 IIS 中安装站点所需的所有文件和元数据。
- 使用命令行创建部署包并进行安装。

在前面的教程中，设置 Visual Studio 以自动执行部署任务的过程适用于所有这三种方法。 在这些教程中，你将使用这些方法中的第一种方法。 有关使用部署包的信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx)。

在发布之前，请确保在管理员模式下运行 Visual Studio。 （在 Windows 7 "**开始**" 菜单中，右键单击要使用的 Visual Studio 版本的图标，然后选择 "以**管理员身份运行**"。）仅当发布到本地计算机上的 IIS 时，才需要管理员模式才能进行发布。

在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目（而不是 ContosoUniversity 项目），然后选择 "**发布**"。

此时将显示 "**发布 Web** " 向导。

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

在下拉列表中，选择 " **&lt;新建 ..."&gt;** 。

在 "**新建配置文件**" 对话框中，输入 "Test"，然后单击 **"确定**"。

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

此名称与之前创建的 Web.config 转换文件的中间节点相同。 当你使用此配置文件发布时，此函件会导致应用 web.config 转换。

向导会自动前进到 "**连接**" 选项卡。

在 "**服务 URL** " 框中，输入*localhost*。

在 "**站点/应用程序**" 框中，输入*Default Web Site/ContosoUniversity*。

在 "**目标 URL** " 框中，输入 `http://localhost/ContosoUniversity`。

不需要 "**目标 URL** " 设置。 当 Visual Studio 完成应用程序的部署时，它会自动打开此 URL 的默认浏览器。 如果你不希望在部署后自动打开浏览器，请将此框留空。

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

单击 "**验证连接**" 以验证设置是否正确，并且你可以连接到本地计算机上的 IIS。

绿色复选标记将验证连接是否成功。

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

单击 "**下一步**" 转到 "**设置**" 选项卡。

"**配置**" 下拉框指定要部署的生成配置。 默认值为 Release，这是所需的值。

选中 "**删除目标位置的其他文件**" 复选框。 由于这是首次部署，目标文件夹中没有任何文件。

在 "**数据库**" 部分的 "连接字符串" 框中，为**SchoolContext**输入以下值：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

部署过程会将此连接字符串放在部署的 Web.config 文件中，原因是选择了 "**在运行时使用此连接字符串**"。

同时，在 " **SchoolContext**" 下，选择 "**应用 Code First 迁移**"。 此选项将导致部署过程配置部署的 Web.config 文件以指定 `MigrateDatabaseToLatestVersion` 初始值设定项。 当应用程序在部署后首次访问数据库时，此初始值设定项会将数据库自动更新到最新版本。

在**DefaultConnection**的 "连接字符串" 框中，输入以下值：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

清除 "**更新数据库**"。 将通过在应用程序\_数据中复制 .sdf 文件来部署成员资格数据库，而不希望部署过程对此数据库执行任何其他操作。

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

单击 "**下一步**" 转到 "**预览**" 选项卡。

在 "**预览**" 选项卡中，单击 "**开始预览**" 以查看要复制的文件的列表。

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

单击“发布”。

如果 Visual Studio 未处于管理员模式，你可能会收到一条指示权限错误的错误消息。 在这种情况下，请关闭 Visual Studio，在管理员模式下打开它，然后再次尝试发布。

如果 Visual Studio 处于管理员模式下，则 "**输出**" 窗口将报告成功的生成和发布。

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

浏览器会自动打开到本地计算机上的 IIS 中运行的 Contoso 大学主页。

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a>测试环境中的测试

请注意，环境指示器显示 "（测试）"，而不是 "（开发）"，这表明环境指示器的*web.config 转换已*成功。

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

运行 "**学生**" 页，验证部署的数据库是否没有学生。 选择此页可能需要几分钟的时间才能加载，因为 Code First 会创建数据库，然后运行 `Seed` 方法。 （如果你在主页上，则不会执行此操作，因为应用程序尚未尝试访问数据库。）

[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

运行**讲师**页，验证 Code First 用指导员数据对数据库进行种子设定：

[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

从 "**学生**" 菜单中选择 "**添加学生**"，添加一个学生，然后在 "**学生**" 页中查看新学生，验证是否可以成功写入数据库：

[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

从**课程**菜单中，选择 "**更新信用**"。 **更新信用**页面需要管理员权限，因此将显示 "**登录**" 页。 输入先前创建的管理员帐户凭据（"admin" 和 "Pas $ w0rd"）。 此时将显示 "**更新信用**" 页，该页面验证你在上一教程中创建的管理员帐户是否已正确部署到测试环境中。

[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

验证*Elmah*文件夹是否仅存在包含占位符文件的文件。

[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a>查看 Code First 迁移的自动 web.config 更改

在 C:\inetpub\wwwroot\ContosoUniversity*中的已*部署应用程序中打开 web.config文件，并可以看到部署过程的配置 Code First 迁移将数据库自动更新到最新版本。

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

部署过程还为 Code First 迁移创建了一个新的连接字符串，以独占方式用于更新数据库架构：

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

使用此附加连接字符串，您可以为数据库架构更新指定一个用户帐户，并为应用程序数据访问指定不同的用户帐户。 例如，可以将 db\_所有者角色分配到 Code First 迁移，并将 db\_datareader 和 db\_datawriter 角色分配给应用程序。 这是一种常见的深层防御模式，可防止应用程序中可能存在的恶意代码更改数据库架构。 （例如，这可能会在成功的 SQL 注入攻击中发生。）这些教程不使用此模式。 它不适用于 SQL Server Compact，当你迁移到本系列后面的教程中 SQL Server 时，此功能不适用。 Cytanium 站点只提供一个用户帐户用于访问在 Cytanium 创建的 SQL Server 数据库。 如果你能够在你的方案中实现此模式，则可以执行以下步骤：

1. 在 "**发布 Web** " 向导的 "**设置**" 选项卡中，输入指定具有 "完全数据库架构更新" 权限的用户的连接字符串，然后清除 "**在运行时使用此连接字符串**" 复选框。 在部署的 Web.config 文件中，这将成为 `DatabasePublish` 的连接字符串。
2. 为希望应用程序在运行时使用的连接字符串创建 web.config 文件转换。

现在，你已将应用程序部署到 IIS 开发计算机上，并在其中进行测试。 这会验证部署过程是否已将应用程序的内容复制到正确的位置（不包括你不想部署的文件），并验证在部署过程中是否正确地 Web 部署配置 IIS。 在下一教程中，你将运行一个查找尚未完成的部署任务的更多测试：设置对*Elmah*文件夹的文件夹权限。

## <a name="more-information"></a>详细信息

有关在 Visual Studio 中运行 IIS 或 IIS Express 的信息，请参阅以下资源：

- [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 站点上的概述。
- Scott Guthrie 的博客[介绍 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) 。
- [如何：在 Visual Studio 中为 Web 项目指定 Web 服务器](https://msdn.microsoft.com/library/ms178108.aspx)。
- [IIS 与 ASP.NET 站点上的 ASP.NET 开发服务器之间的核心差异](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)。
- 在 Rick Anderson 的博客上的[30 秒内，在 IIS 7 上测试 ASP.NET MVC 或 Web 窗体应用程序](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx)。 此项提供了有关 Visual Studio 开发服务器（Cassini）进行测试的原因，以及在 IIS Express 中测试的可靠性，以及在 IIS Express 中进行测试的原因不像在 IIS 中测试那样可靠。

有关应用程序以中等信任模式运行时可能会出现的问题的信息，请参阅[ASP.NET](http://www.4guysfromrolla.com/articles/100307-1.aspx) Rolla

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
> [下一页](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
