---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
title: 使用 FTP 客户端部署站点（VB） |Microsoft Docs
author: rick-anderson
description: 部署 ASP.NET 应用程序的最简单方法是将所需文件手动复制到生产环境。 Thi 。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 09279194-bcf9-4b59-a09d-c68e5926a758
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-your-site-using-an-ftp-client-vb
msc.type: authoredcontent
ms.openlocfilehash: 7875304c672625d8c0eaaf0fea8ef509bb801a3a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611844"
---
# <a name="deploying-your-site-using-an-ftp-client-vb"></a>使用 FTP 客户端部署站点 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_03_VB.zip)或[下载 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial03_DeployingViaFTP_vb.pdf)

> 部署 ASP.NET 应用程序的最简单方法是将所需文件手动复制到生产环境。 本教程演示如何使用 FTP 客户端将文件从桌面获取到 web 宿主提供程序。

## <a name="introduction"></a>简介

前面的教程介绍了一个简单的书籍回顾 ASP.NET web 应用程序，该应用程序由几个 ASP.NET 页、一个母版页、一个自定义基 `Page` 类、多个图像和三个 CSS 样式表组成。 现在，我们已准备好将此应用程序部署到 web 主机提供程序，此时连接到 Internet 的任何人都可以访问该应用程序！

从我们在[*确定需要部署哪些文件*](determining-what-files-need-to-be-deployed-vb.md)的讨论中，我们知道需要将哪些文件复制到 web 宿主提供程序。 （回想一下，要复制哪些文件取决于应用程序是显式编译还是自动编译。）但如何从开发环境（桌面）到生产环境（由 web 主机提供商管理的 web 服务器）获取文件？ [ **F** Ile **T** ransfer **P**协议（FTP）](http://en.wikipedia.org/wiki/File_Transfer_Protocol)是用于通过网络将文件从一台计算机复制到另一台计算机的常用协议。 另一个选项是 FrontPage 服务器扩展（FPSE）。 本教程重点介绍如何使用独立的 FTP 客户端软件将开发环境中所需的文件部署到生产环境。

> [!NOTE]
> Visual Studio 包含通过 FTP 发布网站的工具;下一教程将介绍这些工具以及使用 FPSE 的工具。

若要使用 FTP 复制文件，需要在开发环境中使用*ftp 客户端*。 FTP 客户端是一种应用程序，用于将文件从安装了计算机的计算机复制到运行*FTP 服务器*的计算机。 （如果你的 web 宿主提供程序支持通过 FTP 进行文件传输，则在这种情况下，web 服务器上会运行一个 FTP 服务器。）有许多可用的 FTP 客户端应用程序。 你的 web 浏览器甚至可以作为 FTP 客户端使用 double。 我喜欢的 FTP 客户端和我将用于本教程的客户端是[FileZilla](http://filezilla-project.org/)，它是一种可用于 Windows、Linux 和 mac 的免费开源 FTP 客户端。 不过，任何 FTP 客户端都可以使用，因此可以随意使用最适合的任何客户端。

如果你正在进行以下过程，你将需要使用 web 主机提供商创建一个帐户，然后才能完成本教程或后续教程。 如前面的教程中所述，有一个 gaggle 的 web 主机提供商公司，具有各种价格、功能和服务质量。 在本系列教程中，我将使用 ASP.NET 作为 web 主机提供商提供[折扣](http://discountasp.net)，但您可以遵循任何 web 主机提供程序，只要它们支持您在中开发的 ASP.NET 版本即可。 （这些教程是使用 ASP.NET 3.5 创建的。）此外，因为我们将在本教程中使用 FTP 将文件复制到 web 主机提供程序，而在以后使用时，必须确保 web 主机提供商支持对其 web 服务器的 FTP 访问。 几乎所有 web 宿主提供程序都提供了此功能，但在注册之前应仔细检查。

## <a name="deploying-the-book-review-web-application-project"></a>部署书籍评审 Web 应用程序项目

请记住，有两个版本的书籍评审 web 应用程序：一个是使用 Web 应用程序项目模型（BookReviewsWAP）实现的，另一个是使用网站项目模型（BookReviewsWSP）实现的。 项目类型影响网站是自动编译还是显式编译，并且编译模型确定需要部署哪些文件。 因此，我们将从 BookReviewsWAP 开始分别检查 BookReviewsWAP 和 BookReviewsWSP 项目的部署。 下载这两个 ASP.NET 应用程序（如果尚未这样做）。

通过导航到 `BookReviewsWAP` 文件夹并双击 `BookReviewsWAP.sln` 文件来启动 BookReviewsWAP 项目。 在部署项目之前，必须生成该项目以确保对源代码进行的任何更改都包含在编译的程序集中。 若要生成项目，请在 "生成" 菜单中选择 "生成" 菜单选项。 BookReviewsWAP 这会将项目中的源代码编译成一个程序集，`BookReviewsWAP.dll`放置在 `Bin` 文件夹中。

现在，我们已准备好部署所需的文件！ 启动 FTP 客户端，并连接到 web 主机提供程序上的 web 服务器。 （当你注册 web 托管公司时，他们将通过电子邮件向你发送有关如何连接到 FTP 服务器的信息; 这包括 FTP 服务器的地址以及用户名和密码。）

将以下文件从桌面复制到 web 主机提供程序的根网站文件夹中。 当你在 web 主机提供商处 FTP 到 web 服务器时，可能会出现根网站目录。 但是，某些 web 宿主提供程序有一个名为 `www` 或 `wwwroot` 的子文件夹，用作网站文件的根文件夹。 最后，在 FTPing 文件时，您可能需要在生产环境中创建相应的文件夹结构-`Bin` 文件夹、`Fiction` 文件夹、`Images` 文件夹等。

- `~/Default.aspx`
- `~/About.aspx`
- `~/Site.master`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` 文件夹的完整内容
- `Images` 文件夹（及其子文件夹，`BookCovers`）的完整内容
- `~/Fiction/Default.aspx`
- `~/Fiction/Blaze.aspx`
- `~/Tech/Default.aspx`
- `~/Tech/CYOW.aspx`
- `~/Tech/TYASP35.aspx`
- `~/Bin/BookReviewsWAP.dll`

图1显示了复制必需文件后的 FileZilla。 FileZilla 将本地计算机上的文件显示在左侧，并显示远程计算机上的文件。 如图1所示，ASP.NET 源代码文件（如 `About.aspx.vb`）位于本地计算机（开发环境）上，但尚未复制到 web 主机提供程序（生产环境），因为使用显式编译时不需要部署代码文件。

> [!NOTE]
> 在生产服务器上不会有任何损害，因为这些文件被忽略。 默认情况下，ASP.NET 禁止 HTTP 请求发送到源代码文件，因此即使在生产服务器上存在源代码文件，网站的访问者也无法访问这些文件。 （也就是说，如果用户尝试访问 `http://www.yoursite.com/Default.aspx.vb` 他们会收到一个错误页面，指出这些类型的文件 `.vb` 文件-是禁止的。）

[![使用 FTP 客户端将您的桌面中所需的文件复制到 Web 主机提供程序中的 Web 服务器。](deploying-your-site-using-an-ftp-client-vb/_static/image2.png)](deploying-your-site-using-an-ftp-client-vb/_static/image1.png)

**图 1**：使用 FTP 客户端将您的桌面中所需的文件复制到 Web 宿主提供程序中的 web 服务器（[单击以查看完全大小的图像](deploying-your-site-using-an-ftp-client-vb/_static/image3.png)）

部署站点后，请花点时间测试站点。 如果你已购买域名并正确配置了 DNS 设置，则可以通过输入你的域名来访问你的站点。 或者，你的 web 主机提供商应为你提供一个指向你的网站的 URL，该 URL 将类似于*accountname*。*webhostprovider*或*webhostprovider*/*accountname*。 例如，ASP.NET 上我的帐户的 URL 为： `http://httpruntime.web703.discountasp.net`。

图2显示了已部署的书籍审阅网站。 请注意，我在折扣 ASP 上查看它。网络服务器，`http://httpruntime.web703.discountasp.net`。 此时，与 Internet 建立连接的任何人都可以查看我的网站！ 正如我们所料，站点的外观和行为与在开发环境中测试时的行为一样。

> [!NOTE]
> 如果在查看应用程序时出现错误，请确保部署了正确的文件集。 接下来，请检查错误消息，以确定它是否显示了问题的任何线索。 之后，你可以转到你的 web 主机公司的技术支持人员，或将你的问题发布到[ASP.NET 论坛](https://forums.asp.net/)中的相应论坛。

[!["书籍评论" 站点现在可以通过 Internet 连接的任何人访问。](deploying-your-site-using-an-ftp-client-vb/_static/image5.png)](deploying-your-site-using-an-ftp-client-vb/_static/image4.png)

**图 2**：使用 Internet 连接的任何人都可以访问 "书籍评论" 站点（[单击查看完全大小的图像](deploying-your-site-using-an-ftp-client-vb/_static/image6.png)）

## <a name="deploying-the-book-review-web-site-project"></a>部署书籍评审网站项目

部署使用自动编译的 ASP.NET 应用程序（如 BookReviewsWSP 网站项目）时，`Bin` 文件夹中没有已编译的程序集。 因此，必须将 web 应用程序的源代码文件部署到生产环境中。 我们来演练此过程。

对于 Web 应用程序项目，在部署应用程序之前，最好先生成应用程序。 生成网站项目时，不会创建程序集，它会检查页面中是否存在任何编译时错误。 现在更好地发现这些错误，而不是让网站访问者为你发现这些错误！

成功生成项目后，请使用 FTP 客户端将以下文件复制到 web 主机提供商处的根网站文件夹中。 可能需要在生产环境中创建相应的文件夹结构。

> [!NOTE]
> 如果已部署 BookReviewsWAP 项目，但仍想要尝试部署 BookReviewsWSP 项目，请先删除 web 服务器上的所有文件，这些文件是在部署 BookReviewsWAP 时上载的，然后部署 BookReviewsWSP 的文件。

- `~/Default.aspx`
- `~/Default.aspx.vb`
- `~/About.aspx`
- `~/About.aspx.vb`
- `~/Site.master`
- `~/Site.master.vb`
- `~/Web.config`
- `~/Web.sitemap`
- `Styles` 文件夹的完整内容
- `Images` 文件夹（及其子文件夹，`BookCovers`）的完整内容
- `~/App_Code/BasePage.vb`
- `~/Fiction/Default.aspx`
- `~/Fiction/Default.aspx.vb`
- `~/Fiction/Blaze.aspx`
- `~/Fiction/Blaze.aspx.vb`
- `~/Tech/Default.aspx`
- `~/Tech/Default.aspx.vb`
- `~/Tech/CYOW.aspx`
- `~/Tech/CYOW.aspx.vb`
- `~/Tech/TYASP35.aspx`
- `~/Tech/TYASP35.aspx.vb`

图3显示了复制所需文件后的 FileZilla。 如您所见，ASP.NET 源代码文件（如 `About.aspx.vb`）同时存在于本地计算机（开发环境）和 web 主机提供程序（生产环境）上，因为代码文件需要在使用自动编译时进行部署。

[![使用 FTP 客户端将您的桌面中所需的文件复制到 Web 宿主提供程序中的 Web 服务器](deploying-your-site-using-an-ftp-client-vb/_static/image8.png)](deploying-your-site-using-an-ftp-client-vb/_static/image7.png)

**图 3**：使用 FTP 客户端将您的桌面中所需的文件复制到 Web 宿主提供程序中的 web 服务器（[单击以查看完全大小的图像](deploying-your-site-using-an-ftp-client-vb/_static/image9.png)）

应用程序的编译模型不会影响用户体验。 无论网站是使用 Web 应用程序项目模型还是网站项目模型创建的，相同的 ASP.NET 页面都可访问，其外观和行为都相同。

## <a name="updating-a-web-application-on-production"></a>在生产环境中更新 Web 应用程序

Web 应用程序开发和部署不是一次性过程。 例如，在创建书籍检查网站时，我生成了各种页面，并在个人计算机（开发环境）上编写了随附的代码。 在达到某个稳定状态后，我部署了应用程序，以便其他人可以访问该网站并阅读我的评论。 但部署不会在此站点上标记我的开发结束。 我可以添加更多书籍评论或实施新功能，例如允许我的访客对书籍进行评级或离开他们自己的意见。 此类增强功能将在开发环境中开发，完成后，需要进行部署。 因此，开发和部署是循环的。 开发应用程序，然后将其部署。 当站点处于活动阶段和生产环境中时，会添加新功能，并随着时间的推移固定 bug，这就需要重新部署应用程序。 依此类推。

正如您所料，在重新部署 web 应用程序时，只需要复制新文件和更改的文件。 无需重新部署未更改的页面或服务器端或客户端支持文件（虽然这样做不会有任何损害）。

> [!NOTE]
> 使用显式编译时需要注意的一点是，每当向项目添加新的 ASP.NET 页或进行任何与代码相关的更改时，都需要重新生成项目，该项目将更新 `Bin` 文件夹中的程序集。 因此，在生产环境中更新 web 应用程序时，您需要将此更新的程序集复制到生产环境中。

还要了解，对 `Web.config` 或 `Bin` 目录中的文件所做的任何更改都将停止并重新启动网站的应用程序池。 如果使用 `InProc` 模式（默认值）存储会话状态，则每当修改这些密钥文件时，网站的访问者都将失去其会话状态。 若要避免这种情况，请考虑使用 `StateServer` 或 `SQLServer` 模式存储会话。 有关本主题的详细信息，请阅读[会话状态模式](https://msdn.microsoft.com/library/ms178586.aspx)。

最后，请记住，重新部署应用程序可能需要几秒钟到几分钟的时间，具体取决于需要复制到生产环境中的文件的数量和大小。 在此期间，访问站点的用户可能会遇到错误或错误行为。 你可以通过将名为 `App_Offline.htm` 的页添加到应用程序的根目录中来 "关闭" 你的整个应用程序，该目录向用户说明网站关闭进行维护（或任何其他），稍后将进行备份。 存在 `App_Offline.htm` 文件时，ASP.NET 运行时会将所有传入请求重定向到该页面。

## <a name="summary"></a>总结

部署 web 应用程序需要将所需的文件从开发环境复制到生产环境。 通过网络传输文件的最常见方式是文件传输协议（FTP），大多数 web 主机提供程序支持对其 web 服务器的 FTP 访问。 在本教程中，我们介绍了如何使用 FTP 客户端将所需文件部署到 web 服务器。 部署后，任何连接到 Internet 的人都可以访问该网站！

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [应用\_脱机，并避开 "IE 友好错误" 功能](https://weblogs.asp.net/scottgu/App_5F00_Offline.htm-and-working-around-the-_2200_IE-Friendly-Errors_2200_-feature)
- [会话状态模式](https://msdn.microsoft.com/library/ms178586.aspx)

> [!div class="step-by-step"]
> [上一页](determining-what-files-need-to-be-deployed-vb.md)
> [下一页](deploying-your-site-using-visual-studio-vb.md)
