---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs
title: IIS 与 ASP.NET 开发服务器（C#）之间的核心差异 |Microsoft Docs
author: rick-anderson
description: 在本地测试 ASP.NET 应用程序时，可能会使用 ASP.NET 开发 Web 服务器。 不过，生产网站很可能 pow
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 13a5a423-9235-4dde-b408-2fd10f791d63
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs
msc.type: authoredcontent
ms.openlocfilehash: 7fea3939bd910a052340215c207013e2269f32a2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522080"
---
# <a name="core-differences-between-iis-and-the-aspnet-development-server-c"></a>IIS 和 ASP.NET 开发服务器之间的核心差异 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/4/5/F/45F815EC-8B0E-46D3-9FB8-2DC015CCA306/ASPNET_Hosting_Tutorial_06_CS.zip)或[下载 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial06_WebServerDiff_cs.pdf)

> 在本地测试 ASP.NET 应用程序时，可能会使用 ASP.NET 开发 Web 服务器。 不过，生产网站很可能是支持的 IIS。 这些 web 服务器处理请求的方式有一些差异，这些差异可能会产生重要的影响。 本教程探讨了一些无关的不同之处。

## <a name="introduction"></a>简介

每当用户访问 ASP.NET 应用程序时，他的浏览器就会将请求发送到网站。 Web 服务器软件会选取该请求，该软件与 ASP.NET 运行时协调，以便为请求的资源生成和返回内容。 [**I** Internet **i**璝**S** ervices （IIS）](http://en.wikipedia.org/wiki/Internet_Information_Services)是一套服务，可为 Windows 服务器提供常见的基于 Internet 的功能。 在生产环境中，IIS 是最常用的用于 ASP.NET 应用程序的 web 服务器;web 主机提供商可能使用 web 服务器软件来为 ASP.NET 应用程序提供服务。 IIS 还可以用作开发环境中的 web 服务器软件，尽管这需要安装 IIS 和正确配置 IIS。

ASP.NET 开发服务器是用于开发环境的替代 web 服务器选项;它随附并集成到 Visual Studio 中。 如果 web 应用程序已配置为使用 IIS，则当你第一次从 Visual Studio 中访问网页时，将自动启动 ASP.NET 开发服务器并将其用作 web 服务器。 我们在[*确定需要部署哪些文件*](determining-what-files-need-to-be-deployed-cs.md)教程中创建的演示 web 应用程序是基于文件系统且未配置为使用 IIS 的 web 应用程序。 因此，在从 Visual Studio 中访问这两个网站时，将使用 ASP.NET 开发服务器。

在完美的世界中，开发环境和生产环境都是相同的。 然而，如以上教程中所述，环境具有不同的配置设置并不常见。 在环境中使用不同的 web 服务器软件会添加另一个在部署应用程序时必须考虑的变量。 本教程介绍 IIS 与 ASP.NET 开发服务器之间的主要区别。 由于存在这些差异，因此在开发环境中运行的代码在生产环境中执行时将引发异常或行为不同。

## <a name="security-context-differences"></a>安全上下文差异

当 web 服务器软件处理传入请求时，它会将该请求与特定安全上下文相关联。 操作系统使用此安全上下文信息来确定请求允许哪些操作。 例如，ASP.NET 页面可能包含将一些消息记录到磁盘上的文件的代码。 为了使此 ASP.NET 页执行时不出现错误，安全上下文必须具有相应的文件系统级权限，即对该文件的写入权限。

ASP.NET 开发服务器将传入请求与当前登录的用户的安全上下文相关联。 如果你以管理员身份登录到你的桌面，则 ASP.NET 开发服务器提供的 ASP.NET 页面将具有与管理员相同的访问权限。 但是，IIS 处理的 ASP.NET 请求与特定的计算机帐户相关联。 默认情况下，网络服务计算机帐户由 IIS 版本6和7使用，不过您的 web 宿主提供程序可能为每个客户配置了唯一的帐户。 而且，您的 web 主机提供商可能向此计算机帐户授予了有限的权限。 最终的结果是，在开发环境中，可能会有在开发环境中执行时没有错误的网页，但会生成在生产环境中托管的与授权相关的异常。

若要在操作中显示此类型的错误，我已在书籍评论网站中创建了一个在磁盘上创建文件的文件，该文件存储最近的日期和时间，用户在*24 小时内查看 ASP.NET 3.5*的时间。 若要继续操作，请打开 `~/Tech/TYASP35.aspx` 页面，并将以下代码添加到 `Page_Load` 事件处理程序：

[!code-csharp[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample1.cs)]

> [!NOTE]
> 如果文件不存在，则[`File.WriteAllText` 方法](https://msdn.microsoft.com/library/system.io.file.writealltext.aspx)会创建一个新文件，然后将指定的内容写入其中。 如果文件已存在，则会覆盖现有内容。

接下来，请访问使用 ASP.NET 开发服务器在开发环境中的*24 小时内的 ASP.NET 3.5* 。 假设你使用有权在 web 应用程序的根目录中创建和修改文本文件的帐户登录到你的计算机，则书籍评审看起来与以前相同，但是每次访问该页面时，日期和时间以及用户的 IP 地址都存储在 `LastTYASP35Access.txt` 文件中。 将浏览器指向此文件;应该会看到类似于图1所示的消息。

[![该文本文件包含访问书籍审阅的最后日期和时间](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image2.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image1.png)

**图 1**：文本文件包含访问书籍审阅的最后日期和时间（[单击查看完全大小的图像](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image3.png)）

将 web 应用程序部署到生产环境，然后访问托管的*ASP.NET 3.5，并在24小时内*完成图书审核页。 此时，你应该会看到 "书籍审阅" 页，如图2所示。 某些 web 宿主提供程序向匿名 ASP.NET 计算机帐户授予写入权限，在这种情况下，页将正常运行。 但是，如果您的 web 宿主提供程序禁止对匿名帐户具有写入权限，则当 `TYASP35.aspx` 页尝试将当前日期和时间写入 `LastTYASP35Access.txt` 文件时，将引发[`UnauthorizedAccessException` 异常](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx)。

[![IIS 使用的默认计算机帐户没有写入文件系统的权限](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image5.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image4.png)

**图 2**： IIS 使用的默认计算机帐户没有写入文件系统的权限（[单击查看完全大小的映像](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image6.png)）

好消息是，大多数 web 宿主提供程序都有某种类型的权限工具，可用于在网站中指定文件系统权限。 向匿名 ASP.NET 帐户授予对根目录的写入权限，然后再查看书籍审阅页面。 （如果需要，请与 web 主机提供商联系，以获取有关如何向默认 ASP.NET 帐户授予写入权限的帮助。）这次应加载页面而不会出错，并且应成功创建 `LastTYASP35Access.txt` 文件。

这就是因为 ASP.NET 开发服务器在与 IIS 不同的安全上下文中运行，因此，ASP.NET 页面可能会读取或写入到文件系统、读取或写入 Windows 事件日志，或者读取或写入 Windows 在开发时，注册表将按预期运行，但在生产时将生成异常。 构建将部署到共享 web 宿主环境的 web 应用程序时，不要读取或写入事件日志或 Windows 注册表。 另外，请记下从文件系统读取或写入文件系统的任何 ASP.NET 页面，因为你可能需要向生产环境中的相应文件夹授予读取和写入权限。

## <a name="differences-on-serving-static-content"></a>提供静态内容的差异

IIS 与 ASP.NET 开发服务器之间的另一个核心差别在于它们处理静态内容请求的方式。 进入 ASP.NET 开发服务器的每个请求（无论是针对 ASP.NET 页、图像还是 JavaScript 文件）都由 ASP.NET 运行时处理。 默认情况下，仅当请求进入 ASP.NET 资源（例如 ASP.NET 网页、Web 服务等）时，IIS 才会调用 ASP.NET 运行时。 对于静态内容（图像、CSS 文件、JavaScript 文件、PDF 文件、ZIP 文件和 like）的请求，IIS 将检索这些请求，而无需使用 ASP.NET 运行时。 （当提供静态内容时，可以指示 IIS 使用 ASP.NET 运行时; 有关详细信息，请参阅本教程中的 "使用 IIS 7 对静态文件执行基于窗体的身份验证和 URL 身份验证" 部分。）

ASP.NET 运行时执行多个步骤来生成请求的内容，包括身份验证（标识请求者）和授权（确定请求者是否有权查看所请求的内容）。 一种常用的身份验证形式是*基于窗体的身份验证*，用户通过输入其凭据（通常是用户名和密码）来标识网页上的文本框。 验证凭据后，该网站将在用户的浏览器上存储一个*身份验证票证*cookie，并向网站的每个后续请求发送此 cookie，这是用于对用户进行身份验证的用户。 此外，还可以指定*URL 授权*规则，以规定用户可以或不能访问特定文件夹的内容。 许多 ASP.NET 网站使用基于窗体的身份验证和 URL 授权来支持用户帐户，并定义仅供经过身份验证的用户或属于特定角色的用户访问的站点部分。

> [!NOTE]
> 有关 ASP 的全面检查。网络的基于表单的身份验证、URL 授权和其他用户帐户相关功能，请务必查看[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。

请考虑一个网站，该网站支持使用基于窗体的授权的用户帐户，并且拥有一个使用 URL 授权的文件夹，该文件夹配置为仅允许经过身份验证的用户。 假设此文件夹包含 ASP.NET 页面和 PDF 文件，这意味着，只有经过身份验证的用户才能查看这些 PDF 文件。

如果访问者试图通过在其浏览器的地址栏中直接输入 URL 来查看其中一个 PDF 文件，会发生什么情况？ 要了解这一点，让我们在书籍评论站点中创建一个新文件夹，添加一些 PDF 文件，然后将该站点配置为使用 URL 授权来禁止匿名用户访问此文件夹。 如果下载演示应用程序，会看到我创建了一个名为 `PrivateDocs` 的文件夹，并从我的[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)中添加了一个 PDF （如何适应！）。 `PrivateDocs` 文件夹还包含一个 `Web.config` 文件，该文件指定用于拒绝匿名用户的 URL 授权规则：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample2.xml)]

最后，通过在根目录中更新 `Web.config` 文件，将 web 应用程序配置为使用基于窗体的身份验证，替换：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample3.xml)]

替换为：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample4.xml)]

使用 ASP.NET 开发服务器，访问站点，然后在浏览器的地址栏中输入其中一个 PDF 文件的直接 URL。 如果下载了与本教程关联的网站，URL 应如下所示： `http://localhost:portNumber/PrivateDocs/aspnet_tutorial01_Basics_vb.pdf`

在地址栏中输入此 URL 将导致浏览器将请求发送到该文件的 ASP.NET 开发服务器。 ASP.NET 开发服务器将请求移交给 ASP.NET 运行时进行处理。 由于尚未登录，并且因为 `PrivateDocs` 文件夹中的 `Web.config` 已配置为拒绝匿名访问，ASP.NET 运行时将自动重定向到登录 `Login.aspx` 页（请参阅图3）。 将用户重定向到登录页时，ASP.NET 包括一个 `ReturnUrl` querystring 参数，该参数指示用户尝试查看的页。 成功登录后，可以将用户返回到此页。

[![未经授权的用户将自动重定向到登录页](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image8.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image7.png)

**图 3**：未经授权的用户将自动重定向到登录页（[单击以查看完全大小的图像](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image9.png)）

现在让我们看看它在生产上的行为方式。 部署应用程序，并在生产中的 `PrivateDocs` 文件夹中输入其中一个 Pdf 的直接 URL。 这会提示你的浏览器发送文件的请求 IIS。 由于请求了静态文件，因此 IIS 将在不调用 ASP.NET 运行时的情况下检索并返回该文件。 因此，未执行任何 URL 授权检查;知道文件的直接 URL 的任何人都可以访问被认为专用 PDF 的内容。

[![匿名用户可以通过输入文件的直接 URL 来下载专用 PDF 文件](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image11.png)](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image10.png)

**图 4**：匿名用户可以通过输入文件的直接 URL 来下载专用 PDF 文件（[单击以查看完全大小的图像](core-differences-between-iis-and-the-asp-net-development-server-cs/_static/image12.png)）

### <a name="performing-forms-based-authentication-and-url-authentication-on-static-files-with-iis-7"></a>在 IIS 7 上对静态文件执行基于窗体的身份验证和 URL 身份验证

可以使用几种方法来防止未经授权的用户使用静态内容。 IIS 7 引入了*集成管道*，它将 IIS 的工作流与 ASP.NET 运行时的工作流结婚时会。 简而言之，可以指示 IIS 调用 ASP.NET 运行时的身份验证和授权模块所有传入的请求（包括 PDF 文件之类的静态内容）。 请与 web 主机提供商联系，了解如何将网站配置为使用集成管道。

将 IIS 配置为使用集成管道后，请将以下标记添加到根目录中的 `Web.config` 文件：

[!code-xml[Main](core-differences-between-iis-and-the-asp-net-development-server-cs/samples/sample5.xml)]

此标记指示 IIS 7 使用基于 ASP.NET 的身份验证和授权模块。 重新部署应用程序，然后重新访问 PDF 文件。 这次 IIS 处理请求时，它会向 ASP.NET 运行时的身份验证和授权逻辑提供检查请求的机会。 由于只有经过身份验证的用户才有权查看 `PrivateDocs` 文件夹中的内容，因此，匿名访问者会自动重定向到登录页（请参阅图3）。

> [!NOTE]
> 如果 web 主机提供商仍在使用 IIS 6，则无法使用集成管道功能。 一种解决方法是将私有文档放在禁止 HTTP 访问的文件夹中（例如 `App_Data`），然后创建一个用于服务这些文档的页面。 此页可能会被 `GetPDF.aspx`调用，并通过 querystring 参数传递 PDF 的名称。 `GetPDF.aspx` 页将首先验证用户是否有权查看该文件，如果是，则将使用[`Response.WriteFile(filePath)`](https://msdn.microsoft.com/library/system.web.httpresponse.writefile.aspx)方法将请求的 PDF 文件的内容发送回发出请求的客户端。 如果你不想启用集成管道，此方法也适用于 IIS 7。

## <a name="summary"></a>摘要

生产环境中的 Web 应用程序是使用 Microsoft 的 IIS web 服务器软件托管的。 但是，在开发环境中，可以使用 IIS 或 ASP.NET 开发服务器来承载应用程序。 理想情况下，应在这两个环境中使用相同的 web 服务器软件，因为使用不同的软件会在混合中添加另一个变量。 但是，易用性 ASP.NET 开发服务器使其成为开发环境中的一个极具吸引力的选择。 好消息是，IIS 与 ASP.NET 开发服务器之间只有几个基本差异，并且如果你知道这些差异，你可以采取措施来帮助确保应用程序的工作方式和功能，无论环境.

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [与 IIS 7.0 的 ASP.NET 集成](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)
- 将[ASP.NET 论坛身份验证用于 IIS 7 上的所有类型的内容](https://blogs.iis.net/bills/archive/2007/05/19/using-asp-net-forms-authentication-with-all-types-of-content-with-iis7-video.aspx)（视频）
- [Visual Web Developer 中的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)

> [!div class="step-by-step"]
> [上一页](common-configuration-differences-between-development-and-production-cs.md)
> [下一页](deploying-a-database-cs.md)
