---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: 在 Katana 中启用 Windows 身份验证 |Microsoft Docs
author: MikeWasson
description: 本文介绍如何在 Katana 中启用 Windows 身份验证。 它介绍了两种方案：使用 IIS 托管 Katana，并使用 HttpListener 来自主 Katt 。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500294"
---
# <a name="enabling-windows-authentication-in-katana"></a>在 Katana 中启用 Windows 身份验证

作者： [Mike Wasson](https://github.com/MikeWasson)

> 本文介绍如何在 Katana 中启用 Windows 身份验证。 它介绍了两种方案：使用 IIS 托管 Katana，并使用 HttpListener 在自定义进程中自承载 Katana。 感谢 Barry Dorrans、David Matson 和丽丽 Ross，查看本文。

Katana 是 Microsoft 的[OWIN](http://owin.org/)的实现，它是用于 .Net 的开放 Web 界面。 可在[此处](an-overview-of-project-katana.md)阅读 OWIN 和 Katana 简介。 OWIN 体系结构具有多个层：

- Host：管理运行 OWIN 管道的进程。
- 服务器：打开网络套接字并侦听请求。
- 中间件：处理 HTTP 请求和响应。

Katana 目前提供两台服务器，两者都支持 Windows 集成身份验证：

- **Owin. SystemWeb**。 在 ASP.NET 管道中使用 IIS。
- **Owin. HttpListener**。 使用[系统 HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)。 此服务器当前是自承载 Katana 时的默认选项。

> [!NOTE]
> Katana 当前不提供用于 Windows 身份验证的 OWIN 中间件，因为此功能已在服务器中可用。

## <a name="windows-authentication-in-iis"></a>IIS 中的 Windows 身份验证

使用 Owin，只需在 IIS 中启用 Windows 身份验证即可。

首先，让我们使用 "ASP.NET 空 Web 应用程序" 项目模板创建一个新的 ASP.NET 应用程序。

![](enabling-windows-authentication-in-katana/_static/image1.png)

接下来，添加 NuGet 包。 从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在“Package Manager Console”窗口中，输入以下命令：

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

现在，使用以下代码添加名为 `Startup` 的类：

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

这就是创建一个在 IIS 上运行的 OWIN "Hello world" 应用程序所需的全部工作。 按 F5 调试该应用程序。 应会看到“Hello World!” 在浏览器窗口中。

![](enabling-windows-authentication-in-katana/_static/image2.png)

接下来，我们将在 IIS Express 中启用 Windows 身份验证。 从 "**视图**" 菜单中选择 "**属性**"。 单击解决方案资源管理器中的项目名称，查看项目属性。

在 "**属性**" 窗口中，将 "**匿名身份验证**"**设置为 "** **已禁用**" 并将**Windows 身份验证**设置为

![](enabling-windows-authentication-in-katana/_static/image3.png)

当你从 Visual Studio 中运行应用程序时，IIS Express 将需要用户的 Windows 凭据。 可以通过使用[Fiddler](http://fiddler2.com/home)或其他 HTTP 调试工具来查看此。 下面是一个 HTTP 响应示例：

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

此响应中的 WWW 身份验证标头指示服务器支持[协商](http://www.ietf.org/rfc/rfc4559.txt)协议，该协议使用 KERBEROS 或 NTLM。

稍后，当你将应用程序部署到服务器时，请按照[以下步骤](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)在该服务器上的 IIS 中启用 Windows 身份验证。

## <a name="windows-authentication-in-httplistener"></a>HttpListener 中的 Windows 身份验证

如果你使用的是 Owin 的 HttpListener，则可以直接在**HttpListener**实例上启用 Windows 身份验证。

首先，创建一个新的控制台应用程序。 接下来，添加 NuGet 包。 从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在“Package Manager Console”窗口中，输入以下命令：

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

现在，使用以下代码添加名为 `Startup` 的类：

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

此类在以前实现相同的 "Hello world" 示例，但它还将 Windows 身份验证设置为身份验证方案。

在 `Main` 函数内，启动 OWIN 管道：

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

可以在 Fiddler 中发送请求，以确认应用程序正在使用 Windows 身份验证：

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a>相关主题

[项目 Katana 概述](an-overview-of-project-katana.md)

[System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[了解 MVC 5 中的 OWIN Forms 身份验证](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
