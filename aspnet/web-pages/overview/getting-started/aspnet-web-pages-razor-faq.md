---
uid: web-pages/overview/getting-started/aspnet-web-pages-razor-faq
title: ASP.NET 网页（Razor） FAQ |Microsoft Docs
author: Rick-Anderson
description: 本文列出了一些关于 ASP.NET 网页（Razor）和 WebMatrix 的常见问题。 本教程中使用的软件版本 ASP.NET 网页（R 。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: b137bd04-25e1-47cb-9d96-ef2e179ecf1f
msc.legacyurl: /web-pages/overview/getting-started/aspnet-web-pages-razor-faq
msc.type: authoredcontent
ms.openlocfilehash: 6fa1b668e915af856a693e79eafb7180ed504dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520652"
---
# <a name="aspnet-web-pages-razor-faq"></a>ASP.NET 网页 (Razor) 常见问题解答

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> > [!NOTE] 
> > WebMatrix 不再建议作为 ASP.NET 网页的集成开发环境。 使用[Visual Studio](xref:aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio)或[Visual Studio Code](https://code.visualstudio.com/)。
>
> 本文列出了一些关于 ASP.NET 网页（Razor）和 WebMatrix 的常见问题。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
> - Visual Studio 2013
> - WebMatrix 3
>   
> 
> 本教程还适用于 ASP.NET 网页2、WebMatrix 2 和 Visual Studio 2012。

- [ASP.NET 网页、ASP.NET Web 窗体和 ASP.NET MVC 之间有何区别？](#Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC)
- [是否需要 WebMatrix 才能使用网页？](#Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages)
- [能否在网页页面上使用 ASP.NET Web 窗体控件？](#Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page)
- [是否可以在不使用 WebMatrix 的情况下部署 ASP.NET 网页网站？](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)
- [我是否必须使用 WebSecurity 帮助程序来支持登录名？](#Do_I_have_to_use_the_WebSecurity_helper_to_support_logins)
- [ASP.NET 网页是否支持 HTML5？](#Does_ASP.NET_Web_Pages_support_HTML5)
- [能否在网页中使用 JavaScript 和 jQuery？](#Can_I_use_JavaScript_and_jQuery_with_Web_Pages)
- [其他资源](#AdditionalResources)

有关错误和其他问题的问题，请参阅[ASP.NET 网页（Razor）故障排除指南](https://go.microsoft.com/fwlink/?LinkId=253001)。

<a id="Whats_the_difference_between_ASP.NET_Web_Pages,_ASP.NET_Web_Forms,_and_ASP.NET_MVC"></a>
## <a name="whats-the-difference-between-aspnet-web-pages-aspnet-web-forms-and-aspnet-mvc"></a>ASP.NET 网页、ASP.NET Web 窗体和 ASP.NET MVC 之间有何区别？

这三种技术都是用于创建动态 web 应用程序的 ASP.NET 技术：

- ASP.NET 网页重点介绍如何向 HTML 页面添加动态（服务器端）代码和数据库访问权限，并提供简单的轻型语法。
- ASP.NET Web 窗体基于页面对象模型和传统的窗口类型控件（按钮、列表等）。 Web 窗体使用基于事件的模型，该模型对使用基于客户端（Windows 窗体）开发的用户非常熟悉。
- ASP.NET MVC 实现 ASP.NET 的模型-视图-控制器模式。 重点是 "分离关注点" （处理、数据和 UI 层）。

完全支持所有三个框架，并继续由 ASP.NET 团队开发。 通常，选择要使用的框架将取决于您对 ASP.NET 的背景和体验。

具体而言，ASP.NET 网页旨在使已了解 HTML 的用户能够轻松地将服务器处理添加到页面中。 这是一种很好的选择，适用于学生，爱好者，这是常见的编程人员。 对于具有 non-ASP.NET web 技术经验的开发人员而言，它也是一个不错的选择。

<a id="Do_I_need_WebMatrix_in_order_to_work_with_Web_Pages"></a>
## <a name="do-i-need-webmatrix-in-order-to-work-with-web-pages"></a>是否需要 WebMatrix 才能使用网页？

否。 WebMatrix 不再建议作为 ASP.NET 网页的集成开发环境。 使用[Visual Studio](program-asp-net-web-pages-in-visual-studio.md)或[Visual Studio Code](https://code.visualstudio.com/)。

如果不想使用 Visual Studio 或 Visual Studio Code，则可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)单独安装组件产品。 需要以下产品：

- Microsoft .NET Framework 4.5
- ASP.NET MVC 5 （也安装 ASP.NET 网页 framework）
- IIS Express （web 服务器）
- Microsoft SQL Server Compact 4.0 （数据库）

您可以使用文本编辑器来编辑 *.* # （或*vbhtml*）页。

在不使用工具的情况下管理 SQL Server Compact 数据库（ *.sdf*文件）有点困难。 用于管理 *.sdf*数据库的 Visual Studio containds 工具。 你还可以在代码中运行 SQL 命令，以执行许多 SQL Server 管理任务。

若要在不使用集成开发环境（IDE）的情况下测试*cshtml*页，可以将它们部署到实时服务器。 （请参阅[能否在不使用 WebMatrix 的情况下部署 ASP.NET 网页网站？](#Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix)）

### <a name="running-iis-express-without-using-an-ide"></a>运行 IIS Express 而不使用 IDE

如果将 IIS Express 安装在计算机上作为 web 服务器，则可以使用它来测试页面。 你可以从命令行运行 IIS Express 并将其与特定端口号关联。 然后，在浏览器中请求*cshtml*文件时指定该端口。

在 Windows 中，使用管理员权限打开命令提示符，并更改为*C:\Program Files\IIS Express。* （对于64位系统，请使用文件夹*C:\Program Files （x86） \IIS Express。）* 然后，使用站点的实际路径输入以下命令：

`iisexpress.exe /port:35896 /path:C:\BasicWebSite`

你可以使用任何其他进程都没有保留的任何端口号。 （高于1024的端口号通常是免费的。）对于 "`path`" 值，请使用在其中. *.* # 文件的网站文件夹的路径。

运行此命令以设置要为页面提供服务的 IIS Express 后，可以打开浏览器并浏览到*cshtml*文件。 使用如下所示的 URL：

`http://localhost:35896/default.cshtml`

有关 IIS Express 命令行选项的帮助，请在命令行中输入 `iisexpress.exe /?`。

<a id="Can_I_use_ASP.NET_Web_Forms_controls_on_a_Web_Pages_page"></a>
## <a name="can-i-use-aspnet-web-forms-controls-on-a-web-pages-page"></a>能否在网页页面上使用 ASP.NET Web 窗体控件？

否。 Web 窗体控件（如[CheckBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.checkbox)控件、[验证控件](https://msdn.microsoft.com/library/bwd43d0x)和[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview)控件）仅适用于 web 窗体页（ *.aspx*文件）。 这些控件需要 Web 窗体页框架。

<a id="Can_I_deploy_an_ASP.NET_Web_Pages_site_without_using_WebMatrix"></a>
## <a name="can-i-deploy-an-aspnet-web-pages-site-without-using-webmatrix"></a>是否可以在不使用 WebMatrix 的情况下部署 ASP.NET 网页网站？

可以。 您可以手动将网站文件复制到服务器（通常使用 FTP）。 如果执行手动复制，则还必须复制支持 SQL Server Compact （数据库）的文件。 有关详细信息，请参阅博客文章[部署 Web Pages 应用程序时不使用工具](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2317)。

<a id="Do_I_have_to_use_the_WebSecurity_helper_to_support_logins"></a>
## <a name="do-i-have-to-use-the-websecurity-helper-to-support-logins"></a>我是否必须使用 WebSecurity 帮助程序来支持登录名？

否。 作为 ASP.NET 网页的一部分的 `SimpleMembership` 提供程序是一个选项。 也可以使用 ASP.NET 中的安全提供程序（在 Web 窗体中使用）。 例如，可以在 ASP.NET 网页中使用 forms 身份验证，就像在 Web 窗体中一样。 有关如何使用窗体身份验证的一个示例，请参阅 Microsoft 支持部门文章[如何C#使用 .Net 在 ASP.NET 应用程序中实现基于窗体的身份验证](https://support.microsoft.com/kb/301240)。 若要下载一个简单的示例，请参阅[ASP.NET 版本的 "Login &amp; Password](http://www.codeguru.com/csharp/.net/net_asp/scripting/article.php/c19295/ASPNET-version-of-Login--Password.htm)。

有关如何使用 Windows 身份验证的信息，请参阅博客文章[在 ASP.NET 网页中使用 windows 身份验证](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2298)。

<a id="Does_ASP.NET_Web_Pages_support_HTML5"></a>
## <a name="does-aspnet-web-pages-support-html5"></a>ASP.NET 网页是否支持 HTML5？

可以。 在呈现页面之前，你用 ASP.NET 网页（*cshtml*或*vbhtml*页）创建的页面实质上是包含在服务器上运行的代码的 HTML 页面。 只要用户的浏览器支持 HTML5，你就可以在 *.* # 或*vbhtml*页中使用 html5 元素。

<a id="Can_I_use_JavaScript_and_jQuery_with_Web_Pages"></a>
## <a name="can-i-use-javascript-and-jquery-with-web-pages"></a>能否在网页中使用 JavaScript 和 jQuery？

当然可以。 用 ASP.NET 网页（*cshtml*或*vbhtml*页）创建的页只是带有服务器代码的 HTML 页。 因此，您可以使用*JavaScript 或 jQuery*在普通 HTML 页面中执行的任何操作，也可以在 *.*

WebMatrix 中的**入门站点**模板包含许多 jQuery 库。 如果使用该模板创建一个网站，则 "*脚本*" 文件夹将包含 jquery core 库（ */selfservice/scripts/jquery-1.10.2.min.js 1.6.2）* 和 jquery 验证库（*jquery. validate*，等等）。

下面是一些博客文章，其中阐释了使用 jQuery 与 ASP.NET 网页的方法：

- [使用 WebMatrix 通过 Rachel Appel 将 jQuery 的使用情况添加到 ASP.NET 网页](http://rachelappel.com/jquery/adding-jquery-goodness-to-asp-net-web-pages-using-webmatrix/)
- [5 分钟： WebMatrix + JQUERY UI + json + jquery templates](http://joeriks.com/2011/01/30/5-min-webmatrix-jquery-ui-json-jquery-templates/)作者： Jonas Eriksson
- Mike Brind 的[WebMatrix 和 JQuery 窗体](http://mikesdotnetting.com/Article/155/WebMatrix-And-jQuery-Forms)

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他资源

[ASP.NET 网页 (Razor) 疑难解答指南](https://go.microsoft.com/fwlink/?LinkId=253001)

ASP.NET 网站上的[WebMatrix 和 ASP.NET 网页论坛](https://forums.asp.net/1224.aspx/1?WebMatrix)
