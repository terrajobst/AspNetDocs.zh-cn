---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
title: 使用 Visual Studio 部署站点（C#） |Microsoft Docs
author: rick-anderson
description: Visual Studio 包含用于部署网站的工具。 在本教程中了解有关这些工具的详细信息。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: cde4ee53-a5d0-4937-a54b-67877e8266c3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-visual-studio-cs
msc.type: authoredcontent
ms.openlocfilehash: 4259e51f5a3e6a97bae2aa27b76cbd56ca3449d6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636411"
---
# <a name="deploying-your-site-using-visual-studio-c"></a>使用 Visual Studio 部署站点 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_04_CS.zip)或[下载 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial04_DeployingViaVS_cs.pdf)

> Visual Studio 包含用于部署网站的工具。 在本教程中了解有关这些工具的详细信息。

## <a name="introduction"></a>简介

前面的教程介绍了如何将简单的 ASP.NET web 应用程序部署到 web 宿主提供程序。 具体而言，本教程演示了如何使用 FTP 客户端（如 FileZilla）将所需的文件从开发环境传输到生产环境中。 Visual Studio 还提供了一些内置工具，便于部署到 web 宿主提供程序。 本教程将探讨以下两个工具中的两个： "复制网站" 工具，你可以在其中使用 FTP 或 FrontPage 服务器扩展将文件移入和移出远程 Web 服务器。发布工具将整个网站复制到指定位置。

> [!NOTE]
> Visual Studio 提供的其他与部署相关的工具包括[Web 安装项目](https://msdn.microsoft.com/library/wx3b589t.aspx)和[web 部署项目](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en)外接程序。 Web 安装项目将网站的内容和配置信息打包到单个 MSI 文件中。 此选项最适用于在 intranet 中部署的网站或销售预打包 web 应用程序（客户在其自己的 web 服务器上安装）的公司。 Web 部署项目外接程序是一个 Visual Studio 外接程序，它有助于指定开发环境和生产环境的生成之间的配置差异。 本系列教程不讨论 Web 安装项目;[*开发和生产教程之间的常见配置差异*](common-configuration-differences-between-development-and-production-cs.md)总结了 Web 部署项目。

## <a name="deploying-your-site-using-the-copy-web-site-tool"></a>使用 "复制网站" 工具部署网站

Visual Studio 的 "复制网站" 工具在功能上类似于独立的 FTP 客户端。 简而言之，"复制网站" 工具允许通过 FTP 或 FrontPage 服务器扩展连接到远程网站。 类似于 FileZilla 的用户界面，"复制网站" 用户界面由两个窗格组成：左窗格列出本地文件，而右窗格列出目标服务器上的文件。

> [!NOTE]
> "复制网站" 工具仅适用于网站项目。 使用 Web 应用程序项目时，Visual Studio 会提供此工具。

让我们看一下如何使用 "复制网站" 工具将书籍评审应用程序发布到生产环境。 由于 "复制网站" 工具仅适用于使用网站项目模型的项目，因此我们只能通过 BookReviewsWSP 项目使用此工具进行检查。 打开该项目。

通过单击解决方案资源管理器中的 "复制网站" 图标来启动 "复制网站" 工具项目（图1中的此图标为圆圈）;或者，您可以从 "网站" 菜单中选择 "复制网站" 选项。 这两种方法都可启动 "复制网站" 用户界面，如图1所示。仅填充图1中的左窗格，因为我们尚未连接到远程服务器。

[!["复制网站" 工具的用户界面分为两个窗格](deploying-your-site-using-visual-studio-cs/_static/image2.png)](deploying-your-site-using-visual-studio-cs/_static/image1.png)

**图 1**： "复制网站" 工具的用户界面分为两个窗格（[单击以查看完全大小的图像](deploying-your-site-using-visual-studio-cs/_static/image3.png)）

若要部署站点，需要先连接到 web 主机提供商。 单击 "复制网站" 用户界面顶部的 "连接" 按钮。 此时将显示图2所示的 "打开网站" 对话框。

可以通过从左侧选择以下四个选项之一来连接到目标网站：

- **文件系统**-选择此项可将你的站点部署到可从你的计算机中访问的文件夹或网络共享。
- **本地 IIS** -使用此选项可将站点部署到计算机上安装的 IIS web 服务器。
- **Ftp 站点**-使用 ftp 连接到远程网站。
- **远程站点**-使用 FrontPage 服务器扩展连接到远程网站。

大多数 web 宿主提供程序都支持 FTP，但更少提供 FrontPage 服务器扩展支持。 出于此原因，我选择了 "FTP 站点" 选项，然后输入连接信息，如图2所示。

[![指定目标网站](deploying-your-site-using-visual-studio-cs/_static/image5.png)](deploying-your-site-using-visual-studio-cs/_static/image4.png)

**图 2**：指定目标网站（[单击查看完全大小的图像](deploying-your-site-using-visual-studio-cs/_static/image6.png)）

连接后，"复制网站" 工具将在右窗格中的远程站点上加载文件，并指示每个文件的状态： "新建"、"已删除"、"已更改" 或 "未更改"。 您可以将文件从本地站点复制到远程站点，反之亦然。

让我们向 BookReviewsWSP 项目添加一个新页面，然后将其部署，以便我们可以在操作中看到 "复制网站" 工具。 在名为 `Privacy.aspx`的根目录中的 Visual Studio 中创建新的 ASP.NET 页面。 让页面 `Site.master` 使用母版页，并将网站的隐私策略添加到此页。 图3显示了此页创建后的 Visual Studio。

[![在网站的根文件夹中添加名为 &lt;code&gt;&gt;/code&lt;的新页面](deploying-your-site-using-visual-studio-cs/_static/image8.png)](deploying-your-site-using-visual-studio-cs/_static/image7.png)

**图 3**：将名为 `Privacy.aspx` 的新页添加到网站的根文件夹（[单击查看完全大小的图像](deploying-your-site-using-visual-studio-cs/_static/image9.png)）

接下来，返回到 "复制网站" 用户界面。 如图4所示，左窗格现在包含新的文件-`Policy.aspx` 和 `Policy.aspx.cs`。 更多功能是，这些文件标记有一个箭头图标和一个状态为 "新建"，这表示它们存在于本地站点上，而不是在远程站点上。

[!["复制网站" 工具的左窗格中包含新的 &lt;代码&gt;default.aspx&lt;/code&gt; 页](deploying-your-site-using-visual-studio-cs/_static/image11.png)](deploying-your-site-using-visual-studio-cs/_static/image10.png)

**图 4**： "复制网站" 工具在其左窗格中包含新的 `Privacy.aspx` 页面（[单击查看完全大小的图像](deploying-your-site-using-visual-studio-cs/_static/image12.png)）

若要部署新文件，请选择它们，然后单击箭头图标将它们传输到远程站点。 传输完成后，会在本地和远程站点上同时存在状态为 "未更改" 的 `Policy.aspx` 和 `Policy.aspx.cs` 文件。

除了列出新文件，"复制网站" 工具还会突出显示本地和远程站点之间的任何不同文件。 若要查看此操作，请返回 `Privacy.aspx` 页面，并向隐私策略添加几个单词。 保存该页，然后返回到 "复制网站" 工具。 如图5所示，左窗格中的 "`Privacy.aspx`" 页的状态为 "已更改"，表示它与远程站点不同步。

[!["复制网站" 工具指示 &lt;代码&gt;的 ".aspx&lt;&gt;/code" 页已更改](deploying-your-site-using-visual-studio-cs/_static/image14.png)](deploying-your-site-using-visual-studio-cs/_static/image13.png)

**图 5**： "复制网站" 工具指示 `Privacy.aspx` 页已更改（[单击查看完全大小的图像](deploying-your-site-using-visual-studio-cs/_static/image15.png)）

"复制网站" 工具还表明自上次复制操作后是否已删除某个文件。 从本地项目中删除 `Privacy.aspx`，然后刷新 "复制网站" 工具。 `Privacy.aspx` 和 `Privacy.aspx.cs` 文件仍将在左窗格中列出，但其状态为 "已删除"，表示自上次复制操作后已将其删除。

## <a name="publishing-a-web-application"></a>发布 Web 应用程序

从 Visual Studio 中部署 web 应用程序的另一种方法是使用 "发布" 选项，该选项可通过 "生成" 菜单访问。 "发布" 选项显式编译应用程序，然后将所有必需的文件复制到指定的远程站点。 我们很快就会看到，"发布" 选项比 "复制网站" 工具更为钝。 借助 "复制网站" 工具，你可以检查本地和远程站点上的文件，并允许你根据需要上载或下载单个文件，"发布" 选项将部署整个 Web 应用程序。

除了将所有所需文件复制到指定的远程站点外，"发布" 选项还会显式编译该应用程序。 如果需要对 Web 应用程序项目进行显式编译，则发布选项对于 Web 应用程序项目是不可奇怪的。 可能有点令人吃惊的是，"发布" 选项也可用于网站项目。 如[*确定需要部署的文件*](determining-what-files-need-to-be-deployed-cs.md)教程中所述，可以通过称为*预编译*的过程显式编译网站项目。 本教程重点介绍如何将发布选项用于 Web 应用程序项目。将来的教程将探讨预编译，此时我们将返回来了解如何将发布选项用于网站项目。

> [!NOTE]
> 尽管发布选项在 Visual Studio 中可用于网站项目和 Web 应用程序项目，但 Visual Web Developer 仅为 Web 应用程序项目提供发布选项。

让我们看一下如何使用 "发布" 选项部署书籍评论应用程序。 首先，在 Visual Studio 中打开 BookReviewsWAP （Web 应用程序项目）。 从 "发布" 菜单中选择 "生成 BookReviewsWAP" 项目。 此时将显示一个对话框，提示输入目标位置，以及其他配置选项（请参见图6）。 与 "复制网站" 工具非常类似，你可以输入指向本地文件夹的位置、IIS 上的本地网站、支持 FrontPage 服务器扩展的远程网站或 FTP 服务器地址。 你可以选择是将远程 web 服务器上的文件替换为已部署的文件，还是在发布之前删除远程站点上的所有内容。 还可以指定是否复制：

- 仅运行应用程序所需的项目中的文件，该应用程序忽略不需要的源代码和与项目相关的文件。
- 所有项目文件，包括源代码文件和 Visual Studio 项目文件（如解决方案文件）。
- 源项目文件夹中的所有文件，这些文件将复制源项目文件夹中的所有文件，而不考虑它们是否包含在项目中。

还可以选择上传 `App_Data` 文件夹的内容。

[![指定目标网站](deploying-your-site-using-visual-studio-cs/_static/image17.png)](deploying-your-site-using-visual-studio-cs/_static/image16.png)

**图 6**：指定目标网站（[单击查看完全大小的图像](deploying-your-site-using-visual-studio-cs/_static/image18.png)）

对于书籍评审应用程序，远程站点包含通过 "复制网站" 工具复制 BookReviewsWSP 项目时所部署的文件。 因此，让我们通过删除所有现有内容开始发布选项。 另外，我们只是复制必要的文件，而不是将生产环境干扰到不需要的源代码和项目文件。 指定这些选项后，单击 "发布" 按钮。 在接下来的几秒钟内，Visual Studio 会将所需的文件部署到目标站点，并在 "输出" 窗口中显示其进度。

图7显示了发布操作完成后 FTP 站点上的文件。 请注意，仅上传了标记页和必要的服务器端和客户端支持文件。

[仅 ![将所需文件发布到生产环境](deploying-your-site-using-visual-studio-cs/_static/image20.png)](deploying-your-site-using-visual-studio-cs/_static/image19.png)

**图 7**：只将所需的文件发布到生产环境（[单击以查看完全大小的映像](deploying-your-site-using-visual-studio-cs/_static/image21.png)）

"发布" 选项是一个比 "复制网站" 工具更少的微妙工具。 通过 "复制网站" 工具，你可以检查本地和远程站点上的文件，并查看它们之间的差异，"发布" 选项不提供此类接口。 此外，通过 "复制网站" 工具，您可以进行一次性更改，上载或删除单个文件。 "发布" 选项不允许这样的精细控制;而是发布*整个*应用程序。 此行为的优点和缺点。 在这一方，您知道使用发布选项时，您不会忘记上传重要文件。 但如果你对非常大的网站进行了少量更改，则请考虑使用 "发布" 选项不能更新已修改的页面，而是在 Visual Studio 部署整个站点时要等待的情况。

某些文件的内容在生产环境和开发环境之间有所不同，这并不少见。 例如，应用程序的配置文件 `Web.config`。 由于发布选项会盲目地复制 web 应用程序文件，因此它将用开发环境中的版本覆盖生产环境的自定义配置文件。 后续教程进一步探讨了此主题，并提供了在存在此类差异时部署 web 应用程序的提示。

## <a name="summary"></a>总结

部署网站需要将所需的文件从开发环境复制到生产环境。 前面的教程介绍了如何使用 FileZilla 等 FTP 客户端传输文件。 本教程在 Visual Studio 中检查了两种部署工具： "复制网站" 工具和 "发布" 选项。 "复制网站" 工具类似于 FTP 客户端，因为它具有一个平移接口，该接口列出了本地计算机上的文件和指定的远程计算机，使您可以轻松地在这两台计算机之间上传或下载文件。 "发布" 选项是一个更为钝的工具，它显式编译项目，然后将整个应用程序部署到指定的目标。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [通过 "复制网站" 工具复制网站](https://msdn.microsoft.com/library/1cc82atw.aspx)
- [如何实现：使用 "复制网站" 工具部署](../../../videos/how-do-i/how-do-i-deploy-a-web-site-using-the-copy-web-site-tool.md)网站（视频）
- [如何：发布 Web 应用程序项目](https://msdn.microsoft.com/library/aa983453.aspx)
- [如何：发布网站](https://msdn.microsoft.com/library/20yh9f1b.aspx)
- [Visual Studio 中的安装和部署项目](https://msdn.microsoft.com/library/wx3b589t.aspx)

> [!div class="step-by-step"]
> [上一页](deploying-your-site-using-an-ftp-client-cs.md)
> [下一页](common-configuration-differences-between-development-and-production-cs.md)
