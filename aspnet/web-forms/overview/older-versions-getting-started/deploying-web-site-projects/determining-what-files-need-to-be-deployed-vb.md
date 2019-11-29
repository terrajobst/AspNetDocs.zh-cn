---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-vb
title: 确定需要部署哪些文件（VB） |Microsoft Docs
author: rick-anderson
description: 需要从开发环境中将哪些文件部署到生产环境，具体取决于是否生成了 ASP.NET 应用程序。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: ea918f62-c9d6-4a7f-9bc6-e054d3764b2c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/determining-what-files-need-to-be-deployed-vb
msc.type: authoredcontent
ms.openlocfilehash: a11dadfda8b6a189acedd7ac723d85f8b2084324
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74569931"
---
# <a name="determining-what-files-need-to-be-deployed-vb"></a>确定需要部署哪些文件 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_02_VB.zip)或[下载 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial02_FilesToDeploy_vb.pdf)

> 需要从开发环境中将哪些文件部署到生产环境，具体取决于是否使用网站模型或 Web 应用程序模型生成了 ASP.NET 应用程序。 了解有关这两个项目模型的详细信息，以及项目模型如何影响部署。

## <a name="introduction"></a>简介

部署 ASP.NET web 应用程序需要将 ASP.NET 相关文件从开发环境复制到生产环境。 与 ASP.NET 相关的文件包括 ASP.NET 网页标记和代码以及客户端和服务器端支持文件。 客户端支持文件是由网页引用并直接发送到浏览器图像、CSS 文件和 JavaScript 文件的那些文件。 服务器端支持文件包含用于处理服务器端请求的文件。 这包括配置文件、web 服务、类文件、类型化数据集和 LINQ to SQL 文件，等等。

通常情况下，所有客户端支持文件都应该从开发环境复制到生产环境中，但复制哪些服务器端支持文件取决于您是要将服务器端代码显式编译到程序集（`.dll` 文件），还是要自动生成这些程序集。 本教程重点介绍在将代码显式编译到程序集中，而不是自动执行此编译步骤时需要部署哪些文件。

## <a name="explicit-compilation-versus-automatic-compilation"></a>显式编译与自动编译

ASP.NET 网页分为声明性标记和源代码。 声明性标记部分包括 HTML、Web 控件和数据绑定语法;代码部分包含用 Visual Basic 或C#代码编写的事件处理程序。 标记和代码部分通常分成不同的文件：在 `WebPage.aspx.vb` 包含代码时，`WebPage.aspx` 包含声明性标记。

假设有一个名为 `Clock.aspx` 的 "ASP.NET" 页，其中包含一个 "标签" 控件，其 Text 属性设置为当前日期和页面加载时间。 声明性标记部分（在 `Clock.aspx`中）包含标签 Web 控件 `<asp:Label runat="server" id="TimeLabel" />` 的标记，而代码部分（在 `Clock.aspx.vb`中）将具有具有以下代码的 `Page_Load` 事件处理程序：

[!code-vb[Main](determining-what-files-need-to-be-deployed-vb/samples/sample1.vb)]

为了使 ASP.NET 引擎为此页面的请求提供服务，必须首先编译页面的代码部分（ *`WebPage`* `.aspx.vb` 文件）。 此编译可以显式或自动发生。

如果编译显式发生，则整个应用程序的源代码将编译为位于应用程序的 `Bin` 目录中的一个或多个程序集（`.dll` 文件）。 如果编译自动发生，则默认情况下，生成的自动生成的程序集将位于 `Temporary ASP.NET Files` 文件夹中，该文件夹可在 `%WINDOWS%\Microsoft.NET\Framework\<version>`中找到，尽管可通过 `Web.config`中的[&lt;编译&gt; 元素](https://msdn.microsoft.com/library/s10awwz0.aspx)配置此位置。 使用显式编译时，必须执行一些操作来将 ASP.NET 应用程序的代码编译为程序集，并在部署之前进行此步骤。 通过自动编译，在首次访问资源时，会在 web 服务器上执行编译过程。

无论使用何种编译模型，都需要将所有 ASP.NET 页（`WebPage.aspx` 文件）的标记部分复制到生产环境中。 对于显式编译，你需要复制 `Bin` 文件夹中的程序集，但不需要复制 ASP.NET 页面的代码部分（`WebPage.aspx.vb` 文件）。 通过自动编译，你需要复制代码部分文件，使代码存在，并可在访问页面时自动编译。 每个 ASP.NET 网页的标记部分都包含一个 `@Page` 指令，该指令的特性指示是否已显式编译该页的关联代码，或者是否需要自动编译该页。 因此，生产环境可以无缝地使用任一编译模型，并且无需应用任何特殊的配置设置来指示显式或自动编译。

表1汇总了使用显式编译与自动编译时要部署的不同文件。 请注意，无论使用何种编译模型，都应始终将程序集部署到 `Bin` 文件夹中（如果该文件夹存在）。 `Bin` 文件夹包含特定于 web 应用程序的程序集，该程序集包括使用显式编译模型时编译的源代码。 `Bin` 目录还包含其他项目中的程序集，以及你可能使用的任何开源或第三方程序集，这些程序集需要位于生产服务器上。 因此，一般的经验法则是在部署时将 `Bin` 文件夹复制到生产环境中。 （如果使用的是自动编译模型，但不使用任何外部程序集，则不会有 `Bin` 目录-这是正常的！）

| **编译模型** | **部署标记部分文件？** | **部署源代码文件？** | **是否在 `Bin` Directory 中部署程序集？** |
| --- | --- | --- | --- |
| 显式编译 | 是 | 否 | 是 |
| 自动编译 | 是 | 是 | 是（如果存在） |

**表1：部署哪些文件取决于所使用的编译模型。**

## <a name="taking-a-trip-down-memory-lane"></a>正在向下移动内存通道

使用哪种编译方法，具体取决于在 Visual Studio 中管理 ASP.NET 应用程序的方式。 因此.2000年年，.NET 的开始时间为四个不同版本的 Visual Studio-Visual Studio .NET 2002、Visual Studio .NET 2003、Visual Studio 2005 和 Visual Studio 2008。 使用*Web 应用程序项目*模型的 Visual Studio .net 2002 和2003托管的 ASP.NET 应用程序。 Web 应用程序项目模型的主要功能是：

- 构成项目的文件在单个项目文件中定义。 对于未在项目文件中定义的任何文件，Visual Studio 不会将其视为 web 应用程序的一部分。
- 使用显式编译。 生成项目时，会将项目中的代码文件编译为放置在 `Bin` 文件夹中的单个程序集。

当 Microsoft 发布 Visual Studio 2005 时，它们会丢弃对 Web 应用程序项目模型的支持，并将其替换为网站项目模型。 网站项目模型通过以下方式区分*Web 应用程序项目*模型：

- 改为使用文件系统，而不是使用一个项目文件来拼写出项目的文件。 简而言之，web 应用程序文件夹中的所有文件（或子文件夹）都被视为项目的一部分。
- 在 Visual Studio 中生成项目不会在 `Bin` 目录中创建程序集。 相反，生成网站项目会报告编译时错误。
- 支持自动编译。 通常通过将标记和源代码复制到生产环境来部署网站项目，尽管可以预编译代码（显式编译）。

Microsoft 在发布 Visual Studio 2005 Service Pack 1 时恢复 Web 应用程序项目模型。 但是，Visual Web Developer 仅支持网站项目模型。 好消息是，Visual Web Developer 2008 Service Pack 1 删除了此限制。 现在，你可以在 Visual Studio 中使用 Web 应用程序项目模型或网站项目模型创建 ASP.NET 应用程序。 这两种模型都有其优点和缺点。 请参阅[Web 应用程序项目简介：比较网站项目和 Web 应用程序项目](https://msdn.microsoft.com/library/aa730880.aspx#wapp_topic5)以比较两个模型，帮助确定哪种项目模型最适合你的情况。

## <a name="exploring-the-sample-web-application"></a>浏览示例 Web 应用程序

本教程的下载内容包括一个名为书籍检查的 ASP.NET 应用程序。 该网站模仿了某个爱好网站，该网站可能会创建一个爱好网站来与在线社区共享其书籍评论。 此 ASP.NET web 应用程序非常简单，其中包含以下资源：

- `Web.config`，则为应用程序的配置文件。
- 一个母版页（`Site.master`）。
- 七个不同的 ASP.NET 页：

    - ~/`Default.aspx`-站点的主页。
    - ~/`About.aspx`-"关于站点" 页面。
    - ~/`Fiction/Default.aspx`-列出已查看的小说书籍的页面。

        - ~/`Fiction/Blaze.aspx`-审阅 Richard Bachman novel *Blaze*。
    - ~/`Tech/Default.aspx`-列出已评审的技术书籍的页面。

        - ~/`Tech/CYOW.aspx`-*创建你自己的网站*的评审。
        - ~/`Tech/TYASP35.aspx`-*在24小时内讲授 ASP.NET 3.5*的评论。
- `Styles` 文件夹中有三个不同的 CSS 文件。
- 四个图像文件-由三个审阅的书籍的 ASP.NET 提供支持的徽标和图像-全部位于 `Images` 文件夹中。
- 一个 `Web.sitemap` 文件，用于定义站点地图，并用于在根目录的 `Default.aspx` 页中显示菜单，以及 `Fiction` 和 `Tech` 文件夹。
- 一个名为 `BasePage.vb` 的类文件，它定义基 `Page` 类。 此类通过基于页面在站点地图中的位置自动设置 `Title` 属性，扩展了 `Page` 类的功能。 简而言之，扩展 `BasePage` 的任何 ASP.NET 代码隐藏类（而不是 `System.Web.UI.Page`）都将其标题设置为一个值，具体取决于它在站点地图中的位置。 例如，在查看 ~/`Tech/CYOW.aspx` 页面时，标题设置为 "Home：技术协会：创建自己的网站"。

图1显示了通过浏览器查看时书籍评论网站的屏幕截图。 在这里，你将看到页面 ~/Tech/TYASP35.aspx，它会*在24小时内查看 ASP.NET 3.5*的书籍。 跨越页面顶部和左侧列中菜单的痕迹导航基于 `Web.sitemap`中定义的站点地图结构。 右顶角中的图像是位于 `Images` 文件夹中的一本书封面图像之一。 网站的外观通过 "`Styles`" 文件夹中的 CSS 文件所述的级联样式表规则进行定义，而 "中" 页面布局则在母版页中定义，`Site.master`。

[![书籍评论网站提供有关标题的评论](determining-what-files-need-to-be-deployed-vb/_static/image2.png)](determining-what-files-need-to-be-deployed-vb/_static/image1.png)

**图 1**：书籍评论网站提供了有关标题分类的评论（[单击查看全尺寸图像](determining-what-files-need-to-be-deployed-vb/_static/image3.png)）

此应用程序不使用数据库;每个评审都作为应用程序中的单独网页实现。 本教程（和下几个教程）演练如何部署没有数据库的 web 应用程序。 但是，在将来的教程中，我们将增强此应用程序以在数据库中存储评审、读者备注和其他信息，并将探索正确部署数据驱动的 web 应用程序所需执行的步骤。

> [!NOTE]
> 这些教程重点介绍如何使用 web 宿主提供程序托管 ASP.NET 的应用程序，并且不会浏览 ASP 等辅助主题。网络的站点映射系统或使用基本页面类。 有关这些技术的详细信息，以及本教程中介绍的其他主题的更多背景信息，请参阅每个教程结尾处的其他阅读部分。

本教程的下载内容包含两个 web 应用程序副本，每个副本都作为不同的 Visual Studio 项目类型实现： BookReviewsWAP、Web 应用程序项目和 BookReviewsWSP，一个网站项目。 这两个项目均使用 Visual Web Developer 2008 SP1 创建，并使用 ASP.NET 3.5 SP1。 若要使用这些项目，请先将内容解压缩到桌面。 若要打开 Web 应用程序项目（BookReviewsWAP），请导航到 `BookReviewsWAP` 文件夹，然后双击解决方案文件 `BookReviewsWAP.sln`。 若要打开网站项目（BookReviewsWSP），请启动 Visual Studio，然后从 "文件" 菜单中选择 "打开网站" 选项，浏览到桌面上的 "`BookReviewsWSP`" 文件夹，然后单击 "确定"。

本教程中的其余两个部分介绍在部署应用程序时需要将哪些文件复制到生产环境。 接下来的两个教程-[*使用 FTP 部署网站*](deploying-your-site-using-an-ftp-client-vb.md)并[*使用 Visual Studio 部署网站*](deploying-your-site-using-visual-studio-vb.md)-显示将这些文件复制到 web 主机提供程序的不同方法。

## <a name="determining-the-files-to-deploy-for-the-web-application-project"></a>确定要为 Web 应用程序项目部署的文件

Web 应用程序项目模型使用显式编译-每次生成应用程序时，项目的源代码都将编译为一个程序集。 此编译包括 ASP.NET 页的代码隐藏文件（~/`Default.aspx.vb`、~/`About.aspx.vb`等）以及 `BasePage.vb` 类。 生成的程序集的名称为 `BookReviewsWAP.dll`，位于应用程序的 `Bin` 目录中。

图2显示了本书审查 Web 应用程序项目的文件。

[![解决方案资源管理器列出了包含 Web 应用程序项目的文件。](determining-what-files-need-to-be-deployed-vb/_static/image5.png)](determining-what-files-need-to-be-deployed-vb/_static/image4.png)

**图 2**：解决方案资源管理器列出了包含 Web 应用程序项目的文件

> [!NOTE]
> 如图2所示，ASP.NET 页的代码隐藏文件不会显示在 Visual Basic Web 应用程序项目的解决方案资源管理器中。 若要查看某个页面的代码隐藏类，请在解决方案资源管理器中右键单击该页面，然后选择 "查看代码"。

若要部署使用 Web 应用程序项目模型开发的 ASP.NET 应用程序，首先需要生成应用程序，以便将最新源代码显式编译为程序集。 接下来，将以下文件复制到生产环境：

- 包含每个 ASP.NET 页的声明性标记的文件，例如 ~/`Default.aspx`、~/`About.aspx`等。 此外，请复制任何母版页和用户控件的声明性标记。
- `Bin` 文件夹中的程序集（`.dll` 文件）。 不需要复制程序数据库文件（`.pdb`）或可能在 `Bin` 目录中找到的任何 XML 文件。

不需要将 ASP.NET 页的源代码文件复制到生产环境中，也不需要复制 `BasePage.vb` 类文件。

> [!NOTE]
> 如图2所示，`BasePage` 类实现为项目中的类文件，放在名为 `HelperClasses`的文件夹中。 编译项目时，会将 `BasePage.vb` 文件中的代码连同 ASP.NET 页面的代码隐藏类一起编译到单个程序集中，`BookReviewsWAP.dll`。 ASP.NET 有一个名为 `App_Code` 的特殊文件夹，旨在容纳网站项目的类文件。 `App_Code` 文件夹中的代码是自动编译的，因此不应将其用于 Web 应用程序项目。 相反，应将应用程序的类文件放在名为 `HelperClasses`、`Classes`或类似内容的普通文件夹中。 或者，你可以将类文件放在单独的类库项目中。

除了将 ASP.NET 相关标记文件和程序集复制到 `Bin` 文件夹中外，还需要复制客户端支持文件-图像和 CSS 文件以及其他服务器端支持文件，`Web.config` 和 `Web.sitemap`。 无论你使用的是显式编译还是自动编译，都需要将这些客户端和服务器端支持文件复制到生产环境中。

## <a name="determining-the-files-to-deploy-for-the-web-site-project-files"></a>确定要为网站项目文件部署的文件

网站项目模型支持自动编译，这是在使用 Web 应用程序项目模型时不可用的功能。 使用显式编译时，必须将项目的源代码编译为程序集，并将该程序集复制到生产环境中。 另一方面，通过自动编译，只需将源代码复制到生产环境，并根据需要按需运行时编译。

Visual Studio 中的 "生成" 菜单选项同时存在于 Web 应用程序项目和网站项目中。 构建 Web 应用程序项目会将项目的源代码编译为位于 `Bin` 目录中的单个程序集;构建网站项目时将检查是否存在任何编译时错误，但不会创建任何程序集。 若要部署使用网站项目模型开发的 ASP.NET 应用程序，只需将相应的文件复制到生产环境中，但我会鼓励您首先构建项目，以确保没有编译时错误。

图3显示了使书籍审阅网站项目的文件。

[![解决方案资源管理器列出了包含网站项目的文件。](determining-what-files-need-to-be-deployed-vb/_static/image7.png)](determining-what-files-need-to-be-deployed-vb/_static/image6.png)

**图 3**：解决方案资源管理器列出了包含网站项目的文件

部署网站项目时，需要将所有与 ASP.NET 相关的文件复制到生产环境中，其中包括 ASP.NET 页、母版页和用户控件的标记页，以及它们的代码文件。 还需要复制任何类文件，如 `BasePage.vb`。 请注意，`BasePage.vb` 文件位于 `App_Code` 文件夹中，该文件夹是用于类文件的网站项目中使用的特殊 ASP.NET 文件夹。 还需要在生产环境中创建特殊文件夹，因为必须将开发环境中 `App_Code` 文件夹中的类文件复制到生产上的 `App_Code` 文件夹中。

除了复制 ASP.NET 标记和源代码文件以外，还需要复制客户端支持文件-图像和 CSS 文件以及其他服务器端支持文件，`Web.config` 和 `Web.sitemap`。

> [!NOTE]
> 网站项目还可以使用显式编译。 将来的教程将介绍如何显式编译网站项目。

## <a name="summary"></a>总结

部署 ASP.NET 应用程序需要将所需的文件从开发环境复制到生产环境。 需要同步的精确文件集取决于 ASP.NET 应用程序的代码是显式还是自动编译。 如果将 Visual Studio 配置为使用 Web 应用程序项目模型或网站项目模型管理 ASP.NET 应用程序，则所采用的编译策略将受到影响。

Web 应用程序项目模型使用显式编译，并将项目的代码编译到 `Bin` 文件夹中的单个程序集中。 部署应用程序时，ASP.NET 页的标记部分和 `Bin` 文件夹的内容必须推送到生产环境;应用程序中的源代码（例如，不需要将代码文件和代码隐藏类复制到生产环境）。

默认情况下，网站项目模型使用自动编译，尽管可以显式编译网站项目，如以后的教程中所示。 部署使用自动编译的 ASP.NET 应用程序要求必须将标记部分*和*源代码复制到生产环境中。 首次请求时，将在生产环境中自动编译代码。

现在，我们已经检查了需要在开发和生产环境之间同步的文件，我们已准备好将书籍评论应用程序部署到 web 主机提供商。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 编译概述](https://msdn.microsoft.com/library/ms178466.aspx)
- [ASP.NET 用户控件](https://msdn.microsoft.com/library/y6wb1a0e.aspx)
- [正在检查 ASP。网络站点导航](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [Web 应用程序项目简介](https://msdn.microsoft.com/library/aa730880.aspx)
- [母版页教程](../master-pages/creating-a-site-wide-layout-using-master-pages-cs.md)
- [在页面之间共享代码](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/pages/code.aspx)
- [为 ASP.NET 页的代码隐藏类使用自定义基类](http://aspnet.4guysfromrolla.com/articles/041305-1.aspx)
- [Visual Studio 2005 的网站项目系统：它是什么？为什么要这样做呢？](https://weblogs.asp.net/scottgu/archive/2005/08/21/423201.aspx)
- [演练：在 Visual Studio 中将网站项目转换为 Web 应用程序项目](https://msdn.microsoft.com/library/aa983476.aspx)

> [!div class="step-by-step"]
> [上一页](asp-net-hosting-options-vb.md)
> [下一页](deploying-your-site-using-an-ftp-client-vb.md)
