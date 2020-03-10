---
uid: web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
title: ASP.NET 网页（Razor）故障排除指南 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍使用 ASP.NET 网页（Razor）和某些建议的解决方案时可能遇到的问题。 软件版本 ASP.NET Web 页的链接...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: 2a2c1833-0bfe-4e2e-9cc0-341b52c7b121
msc.legacyurl: /web-pages/overview/testing-and-debugging/aspnet-web-pages-razor-troubleshooting-guide
msc.type: authoredcontent
ms.openlocfilehash: fc03767c16f46c1e282d24ee3a7df2409a7c38bb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473378"
---
# <a name="aspnet-web-pages-razor-troubleshooting-guide"></a>ASP.NET Web Pages (Razor) 疑难解答指南

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍使用 ASP.NET 网页（Razor）和某些建议的解决方案时可能遇到的问题。
> 
> ## <a name="software-versions"></a>软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2和 ASP.NET 网页1.0。

本主题包含以下各节：

- [正在运行的页面的问题](#Issues_Running_.cshtml_Pages)
- [Razor 代码问题](#IssuesWithRazorCode)
- [安全和成员身份问题](#membership)
- [发送电子邮件的问题](#email)
- [其他资源](#AdditionalResources)

有关一般问题，请参阅[ASP.NET 网页（Razor）常见问题解答](https://go.microsoft.com/fwlink/?LinkId=253000)。

<a id="Issues_Running_.cshtml_Pages"></a>
## <a name="issues-with-running-pages"></a>正在运行的页面的问题

许多问题都可能导致无法正常运行 *.* 本部分列出了常见的错误消息和可能的原因。

### <a name="http-error-403---forbidden-access-is-denied"></a>HTTP 错误 403-禁止访问：访问被拒绝

*您没有权限使用您提供的凭据查看此目录或页面。*

如果服务器未运行正确版本的 .NET Framework，则会发生此错误。 请确保运行服务器的计算机（本地或远程）至少安装了 .NET Framework 4。 此外，请确保将应用程序本身配置为运行正确的版本。

如果在 WebMatrix 中工作时本地发现此问题，请单击 "**站点**" 工作区，然后在 treeview 中单击 "**设置**"。 在 "**选择 .NET Framework 版本**" 列表中，选择 " **.Net 4 （集成）** "。 如果已设置此版本，请尝试以管理员身份运行 WebMatrix。

请确保网站的根目录中至少包含一个*cshtml*文件。

如果 web 服务器位于远程服务器上时看到此错误，请与服务器管理员联系。 请确保已安装 .NET Framework 4 或更高版本的服务器。 此外，请确保应用程序在配置为使用该版本的 the.NET Framework 的应用程序池中运行。

如果你可以控制服务器，请确保它正在运行正确版本的 .NET Framework。 你还可以尝试通过运行 `aspnet_regiis -iru` 命令来修复安装。 （例如，如果在安装 .NET Framework 后安装 IIS，则 IIS 将不会正确配置为运行 ASP.NET 页面。）有关详细信息，请参阅[ASP.NET IIS 注册工具（Aspnet\_regiis）](https://msdn.microsoft.com/library/k6h9cz8h(v=vs.100).aspx)。

### <a name="http-error-40314---forbidden"></a>HTTP 错误 403.14-禁止访问

*Web 服务器被配置为不列出此目录的内容。*

如果请求受保护的资源（如*web.config 文件）* 或在受保护的文件夹中（例如*应用\_数据*或*应用\_代码*），则会发生此错误。

### <a name="http-error-40417---not-found"></a>HTTP 错误 404.17-未找到

*请求的内容将显示为脚本，而不会由静态文件处理程序提供。*

如果服务器未正确配置为使用 .NET Framework 4 或更高版本，则可能发生此错误，因此无法识别 `@{ }` 块中的代码。 请参阅前面的说明，了解*HTTP 错误 403-禁止访问：访问被拒绝*。

### <a name="http-error-4047---not-found"></a>HTTP 错误 404.7-未找到

*请求筛选模块被配置为拒绝文件扩展名*

如果已在服务器上显式阻止了*cshtml*或*vbhtml*扩展，则会出现此错误。 此问题的症状在于，当 Url 不包含扩展名时，它们会正常工作，但包含 *.* 一种可能的解决方案是重新启用站点的*web.config 文件中的扩展*。 下面的示例演示如何启用 *.* # 扩展名。

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample1.xml?highlight=5-6)]

### <a name="http-error-4048---not-found"></a>HTTP 错误 404.8-未找到

*请求筛选模块被配置为拒绝包含 hiddenSegment 部分的 URL 中的路径。*

如果请求受保护的资源（如*web.config 文件）* 或在受保护的文件夹中（例如*应用\_数据*或*应用\_代码*），则会发生此错误。

### <a name="this-type-of-page-is-not-served-server-error-in--application"></a>此类型的页未提供（"/" 应用程序中的服务器错误）

请参阅前面的说明，了解 HTTP 错误404.17。

<a id="IssuesWithRazorCode"></a>
## <a name="issues-with-razor-code"></a>Razor 代码问题

### <a name="the-name-class-does-not-exist-in-the-current-context"></a>当前上下文中不存在名称 "*class*"

通常情况下，出现此错误的原因是 `class` 引用了帮助程序，但未安装帮助器。 例如，如果你尝试使用帮助程序，但如果尚未从 NuGet 安装包，则会看到此错误。 使用 WebMatrix 中的库查找并安装帮助程序。

如果帮助程序已安装，但页面仍无法识别，请尝试向代码添加 `using` 语句。 在 `using` 语句中，引用包含帮助器的命名空间。 例如，ASP.NET Web 帮助程序包中的基本帮助程序位于 `System.Web.Helpers` 命名空间中。 在要使用帮助器的页面的顶部，添加以下行：

`@using Microsoft.Web.Helpers;`

<a id="membership"></a>
## <a name="issues-with-security-and-membership"></a>安全和成员身份问题

如果在 ASP.NET 网页（Razor）中使用内置安全（成员）系统，则可能会遇到以下问题。

### <a name="to-call-this-method-the-membershipprovider-property-must-be-an-instance-of-extendedmembershipprovider"></a>若要调用此方法，"成员身份提供程序" 属性必须是 "ExtendedMembershipProvider" 的实例

此错误可能表示没有配置 `AspNetSqlMembershipProvider` 类。 （症状是站点在本地正常运行，但在将其发布到托管提供商的服务器时，会引发此错误。）此问题的一种解决方法是通过向站点的*web.config 文件添加*以下内容来显式启用简单成员身份：

[!code-xml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample2.xml?highlight=6)]

<a id="email"></a>
## <a name="issues-with-sending-email"></a>发送电子邮件的问题

对于发送电子邮件的问题，调试起来可能很困难。 初始问题可能是无法连接到 SMTP 服务器。 如果连接成功，ASP.NET 将消息发送到 SMTP 服务器。 但是，导致 SMTP 服务器无法发送的消息本身可能存在问题。

如果你的应用程序未成功发送电子邮件，请尝试以下操作：

- SMTP 服务器名称通常类似于 `smtp.provider.com` 或 `smtp.provider.net`。 但是，如果将网站发布到宿主提供程序，此时可能会 `localhost`该点的 SMTP 服务器名称。 出现这种情况的原因是，在发布并在提供程序的服务器上运行了站点后，SMTP 服务器可能从应用程序的角度来看是本地的。 服务器名称中的这一更改可能意味着必须在发布过程中更改 SMTP 服务器名称。
- 端口号通常为25。 但是，某些提供程序要求使用端口587或其他端口。 向 SMTP 服务器的所有者咨询他们希望使用的端口号。
- 请确保使用正确的凭据。 如果你已将站点发布到托管提供商，请使用提供商专门指出的凭据来发送电子邮件。 这些凭据可能不同于用于发布的凭据。
- 有时你根本不需要凭据。 如果你使用个人 ISP 发送电子邮件，则电子邮件提供商可能已知道你的凭据。 发布后，可能需要使用不同于在本地计算机上进行测试时使用的凭据。
- 如果电子邮件提供程序使用加密，请将 `WebMail.EnableSsl` 设置为 `true`。

如果发送电子邮件时出错，可能会看到标准 ASP.NET 错误消息，如下所示：

![电子邮件出现问题时出现 ASP.NET 错误消息](aspnet-web-pages-razor-troubleshooting-guide/_static/image1.png)

你还可以使用 `try-catch` 块调试发送电子邮件的问题，如以下示例中所示。 使用 `try-catch` 块时，ASP.NET 不会显示其标准错误消息。 相反，你可以在块的 `catch` 部分捕获该错误。

[!code-cshtml[Main](aspnet-web-pages-razor-troubleshooting-guide/samples/sample3.cshtml)]

用适当的值替换 `your-SMTP-server-name`等。 此方法可能会出现以下错误消息：

- *发送邮件失败。*

    或

    *由于连接的参与方在一段时间后未正确响应，连接尝试失败，或者已建立连接失败，因为连接的主机无法响应*

    此错误通常表示应用程序无法连接到 SMTP 服务器。 请检查服务器名称和端口号。
- *邮箱不可用。服务器响应为： 5.1.0 &lt;someuser@invaliddomain&gt; 发送方已拒绝：无效的发送方域*

    此消息可能表示 `From` 地址不正确或缺失。
- *指定的字符串不是电子邮件地址所需的形式。*

    此错误可能表示 `To` 或 `From` 属性的值未被识别为电子邮件地址。 （ASP.NET 无法检查电子邮件地址是否有效，只是其格式正确，如 *name@domain.com* 。）

> [!NOTE]
> 在将页面发布到活动站点之前，请删除显示错误（`@errorMessage`）的标记。 最好不要让用户看到从服务器获得的错误消息。

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他资源

[ASP.NET 网页 (Razor) 常见问题解答](https://go.microsoft.com/fwlink/?LinkId=253000)

ASP.NET 网站上的[WebMatrix 和 ASP.NET 网页](https://forums.asp.net/1224.aspx/1?WebMatrix)论坛
