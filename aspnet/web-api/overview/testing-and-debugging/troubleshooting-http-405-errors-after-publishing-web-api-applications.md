---
uid: web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
title: 对在 Visual Studio 中工作并在生产 IIS 服务器上失败的 Web API2 应用进行故障排除
author: rmcmurray
description: 对在 Visual Studio 中工作并在生产 IIS 服务器上失败的 Web API2 应用进行故障排除
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 07ec7d37-023f-43ea-b471-60b08ce338f7
msc.legacyurl: /web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
msc.type: authoredcontent
ms.openlocfilehash: 1b47f1ade3619cfd010260352f6a96985ab3598b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447026"
---
# <a name="troubleshoot-web-api2-apps-that-work-in-visual-studio-and-fail-on-a-production-iis-server"></a>对在 Visual Studio 中工作并在生产 IIS 服务器上失败的 Web API2 应用进行故障排除

> 本文档介绍如何对部署到生产 IIS 服务器的 Web API2 应用程序进行故障排除。 它解决了常见的 HTTP 405 和501错误。
> 
> ## <a name="software-used-in-this-tutorial"></a>本教程中使用的软件
> 
> 
> - [Internet Information Services （IIS）](https://www.iis.net/) （版本7或更高版本）
> - [Web API](../../index.md) 

Web API 应用通常使用几个 HTTP 谓词： GET、POST、PUT、DELETE 和有时修补程序。 这种情况下，开发人员可能会遇到以下情况：这些谓词由其生产 IIS 服务器上的另一个 IIS 模块实现，这将导致在 Visual Studio 或开发服务器上正常运行的 Web API 控制器将 HTTP 405 错误部署到生产 IIS 服务器时，将返回该错误。

## <a name="what-causes-http-405-errors"></a>导致 HTTP 405 错误的原因

了解如何排查 HTTP 405 错误的第一步是了解 HTTP 405 错误的实际含义。 HTTP 的主要管理文档是[RFC 2616](http://www.ietf.org/rfc/rfc2616.txt)，它将 http 405 状态代码定义为***不允许的方法***，并在请求-URI 标识的资源中 &quot;，进一步描述了请求行中指定的方法。&quot; 换言之，http 客户端请求的特定 URL 不允许使用 HTTP 谓词。

下面是 RFC 2616 中定义的几个最常用的 HTTP 方法，RFC 4918 和 RFC 5789：

| HTTP 方法 | 说明 |
| --- | --- |
| **GET** | 此方法用于从 URI 检索数据，它可能是最常用的 HTTP 方法。 |
| **HEAD** | 此方法与 GET 方法非常相似，不同之处在于它不会从请求 URI 中实际检索数据，而只是检索 HTTP 状态。 |
| **POST** | 此方法通常用于将新数据发送到 URI;POST 通常用于提交表单数据。 |
| **PUT** | 此方法通常用于将原始数据发送到 URI;PUT 通常用于向 Web API 应用程序提交 JSON 或 XML 数据。 |
| **DELETE** | 此方法用于从 URI 中删除数据。 |
| **OPTIONS** | 此方法通常用于检索 URI 支持的 HTTP 方法的列表。 |
| **复制移动** | 这两种方法与 WebDAV 一起使用，其目的一目了然。 |
| **MKCOL** | 此方法与 WebDAV 一起使用，它用于在指定的 URI 处创建集合（例如目录）。 |
| **PROPFIND PROPPATCH** | 这两个方法与 WebDAV 一起使用，它们用于查询或设置 URI 的属性。 |
| **锁定解锁** | 这两个方法与 WebDAV 一起使用，并且在创作时用于锁定/解锁由请求 URI 标识的资源。 |
| **PATCH** | 此方法用于修改现有 HTTP 资源。 |

如果将其中一种 HTTP 方法配置为在服务器上使用，服务器将使用 HTTP 状态和适用于该请求的其他数据进行响应。 （例如，GET 方法可能会收到 HTTP 200 ***OK***响应，PUT 方法可能会收到 Http 201***创建***的响应。）

如果 HTTP 方法未配置为在服务器上使用，则服务器将响应 "***未实现***http 501" 错误。

但是，当将 HTTP 方法配置为在服务器上使用，但对于给定的 URI 禁用了该方法后，服务器将使用 HTTP 405***方法（不允许***错误）进行响应。

## <a name="example-http-405-error"></a>示例 HTTP 405 错误

以下 HTTP 请求和响应示例说明了 HTTP 客户端尝试将值放入 web 服务器上的 Web API 应用的情况，并且服务器返回 HTTP 错误，该错误指出不允许 PUT 方法：

HTTP 请求：

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample1.cmd)]

HTTP 响应：

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample2.cmd)]

在此示例中，HTTP 客户端向 web 服务器上的 Web API 应用程序的 URL 发送了有效的 JSON 请求，但服务器返回了 HTTP 405 错误消息，指示该 URL 不允许 PUT 方法。 相反，如果请求 URI 与 Web API 应用程序的路由不匹配，则服务器将返回 "***找不到***HTTP 404" 错误。

## <a name="resolve-http-405-errors"></a>解决 HTTP 405 错误

有几个原因可能导致无法允许特定的 HTTP 谓词，但在 IIS 中有一个主要原因是此错误的主要原因：多个处理程序是为同一谓词/方法定义的，其中一个处理程序阻止预期处理程序处理请求。 通过说明，IIS 会根据*applicationhost.config*和 web.config 文件中的顺序处理程序项处理从第一个到最后一个的处理*程序，其中*使用路径、谓词、资源等的第一个匹配组合来处理请求。

下面的示例摘自在使用 PUT 方法将数据提交到 Web API 应用程序时返回 HTTP 405 错误的 IIS 服务器的*applicationhost.config*文件。 在此摘录中，定义了几个 HTTP 处理程序，并且每个处理程序都有一组不同的 HTTP 方法，其中为其配置了一个。列表中的最后一项是静态内容处理程序，这是在其他处理程序具有 chanc 后使用的默认处理程序。e：检查请求：

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample3.xml)]

在前面的示例中，为不同的 HTTP 方法列表明确定义了用于 ASP.NET 的 WebDAV 处理程序和无扩展名的 URL 处理程序（用于 Web API）。 请注意，虽然此配置不一定会导致错误，但会为所有 HTTP 方法配置 ISAPI DLL 处理程序。 但是，当排除 HTTP 405 错误时，需要考虑此类配置设置。

在前面的示例中，ISAPI DLL 处理程序不是问题;事实上，未在 IIS 服务器的*applicationhost.config*文件中定义该问题-问题是由在 Visual Studio 中创建 web API 应用程序时在*web.config 文件中*所做的条目引起的。 应用程序的*web.config*文件中的以下摘录显示了问题的位置：

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample4.xml)]

在此节选内容中，将重新定义用于 ASP.NET 的无扩展名 URL 处理程序，以包括将用于 Web API 应用程序的其他 HTTP 方法。 但是，因为为 WebDAV 处理程序定义了一组类似的 HTTP 方法，所以会发生冲突。 在此特定情况下，IIS 将定义和加载 WebDAV 处理程序，即使为包含 Web API 应用程序的网站禁用了 WebDAV 也是如此。 在处理 HTTP PUT 请求期间，IIS 会调用 WebDAV 模块，因为它是为 PUT 谓词定义的。 调用 WebDAV 模块时，它会检查其配置并发现它已被禁用，因此它将返回与 WebDAV 请求类似的任何请求的 HTTP 405***方法***错误。 若要解决此问题，应从定义了 Web API 应用程序的网站的 HTTP 模块列表中删除 WebDAV。 下面的示例显示了可能出现的情况：

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample5.xml)]

在将应用程序从开发环境发布到 IIS 生产环境后，通常会遇到这种情况，这是因为在开发环境和生产环境之间的处理程序/模块列表不同。 例如，如果使用 Visual Studio 2012 或更高版本来开发 Web API 应用程序，则 IIS Express 是用于测试的默认 Web 服务器。 此开发 web 服务器是一种在服务器产品中提供的完整 IIS 功能的缩小版本，而此开发 web 服务器包含为开发方案添加的一些更改。 例如，WebDAV 模块通常安装在运行完整版 IIS 的生产 web 服务器上，尽管它可能未被使用。 IIS 开发版（IIS Express）安装了 WebDAV 模块，但 WebDAV 模块的条目被故意注释掉，因此，不会在 IIS Express 上加载 WebDAV 模块，除非您专门改变 IIS Express 配置用于向 IIS Express 安装添加 WebDAV 功能的设置。 因此，你的 web 应用程序可能会在你的开发计算机上正常运行，但当你将 Web API 应用程序发布到生产 IIS web 服务器时，可能会遇到 HTTP 405 错误。

## <a name="http-501-errors"></a>HTTP 501 错误

* 指示服务器上尚未实现特定功能。
* 通常意味着在 IIS 设置中未定义与 HTTP 请求匹配的处理程序：
  * 可能表示未在 IIS 上正确安装某些内容或
  * 某些内容已经修改了 IIS 设置，因此没有定义支持特定 HTTP 方法的处理程序。

若要解决此问题，需要重新安装尝试使用 HTTP 方法的任何应用程序，而该应用程序没有相应的模块或处理程序定义。

## <a name="summary"></a>摘要

当 web 服务器不允许 HTTP 方法用于请求的 URL 时，将导致 HTTP 405 错误。 如果已为特定谓词定义了特定的处理程序，并且该处理程序重写了预期处理请求的处理程序，则通常会出现这种情况。
