---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: 入门与 OWIN 和 Katana |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472442"
---
# <a name="getting-started-with-owin-and-katana"></a>OWIN 和 Katana 入门

作者： [Mike Wasson](https://github.com/MikeWasson)

[开放式 Web Interface for .net （OWIN）](http://owin.org/)定义 .net web 服务器和 Web 应用程序之间的抽象。 通过将 web 服务器与应用程序分离，OWIN 可以更轻松地创建用于 .NET web 开发的中间件。 此外，OWIN 使你可以更轻松地将 web 应用程序&#8212;移植到其他主机（例如，在 Windows 服务或其他进程中自承载）。

OWIN 是社区拥有的规范，而不是实现。 Katana 项目是由 Microsoft 开发的一组开源 OWIN 组件。 有关 OWIN 和 Katana 的一般概述，请参阅[Project Katana 的概述](an-overview-of-project-katana.md)。 在本文中，我将直接转到代码开始。

本教程使用[Visual Studio 2013 候选发布版](https://go.microsoft.com/fwlink/?LinkId=306566)，但你也可以使用 Visual Studio 2012。 下面是一些在 Visual Studio 2012 中所述步骤不同的步骤。

## <a name="host-owin-in-iis"></a>在 IIS 中承载 OWIN

在本部分中，我们将在 IIS 中托管 OWIN。 使用此选项，你可以灵活地将 OWIN 管道与可组合性的成熟功能集结合使用。 使用此选项时，OWIN 应用程序会在 ASP.NET 请求管道中运行。

首先，创建一个新的 ASP.NET Web 应用程序项目。 （在 Visual Studio 2012 中，使用 ASP.NET 空白 Web 应用程序项目类型。）

![](getting-started-with-owin-and-katana/_static/image1.png)

在 "**新建 ASP.NET 项目**" 对话框中，选择 "**空**" 模板。

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a>添加 NuGet 包

接下来，添加所需的 NuGet 包。 从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在 "程序包管理器控制台" 窗口中，键入以下命令：

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a>添加 Startup 类

接下来，添加 OWIN startup 类。 在解决方案资源管理器中，右键单击项目并选择 "**添加**"，然后选择 "**新建项**"。 在 "**添加新项**" 对话框中，选择 " **Owin Startup class**"。 有关配置 startup 类的详细信息，请参阅[OWIN Startup Class 检测](owin-startup-class-detection.md)。

![](getting-started-with-owin-and-katana/_static/image4.png)

将以下代码添加到 `Startup1.Configuration` 方法中：

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

此代码将简单的中间件添加到 OWIN 管道，并将其作为接收**IOwinContext**实例的函数来实现。 当服务器收到 HTTP 请求时，OWIN 管道将调用中间件。 中间件设置响应的内容类型并写入响应正文。

> [!NOTE]
> Visual Studio 2013 中提供了 OWIN Startup 类模板。 如果使用的是 Visual Studio 2012，只需添加一个名为 `Startup1`的新空类，并粘贴以下代码：

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a>运行应用程序

按下 F5 以便开始调试。 Visual Studio 将打开一个浏览器窗口以 `http://localhost:*port*/`。 该页应如下所示：

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a>控制台应用程序中的自承载 OWIN

在自定义过程中，可以轻松地将此应用程序从承载 IIS 托管到自承载。 借助 IIS 托管，IIS 既充当 HTTP 服务器，又充当承载服务的进程。 使用自承载，你的应用程序将创建进程，并使用**HttpListener**类作为 HTTP 服务器。

在 Visual Studio 中创建新的控制台应用程序。 在 "程序包管理器控制台" 窗口中，键入以下命令：

`Install-Package Microsoft.Owin.SelfHost -Pre`

将本教程第1部分中的 `Startup1` 类添加到项目。 不需要修改此类。

按如下所示实现应用程序的 `Main` 方法。

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

运行控制台应用程序时，服务器开始侦听 `http://localhost:9000`。 如果在 web 浏览器中导航到此地址，将显示 "Hello world" 页面。

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a>添加 OWIN 诊断

Owin 包包含捕获未经处理的异常的中间件，并显示包含错误详细信息的 HTML 页面。 此页的工作方式非常类似于 ASP.NET 错误页，有时称为 "[黄屏死亡](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" （YSOD）。 与 YSOD 一样，Katana 错误页在开发期间很有用，但最好在生产模式下禁用它。

若要在项目中安装诊断包，请在 "包管理器控制台" 窗口中键入以下命令：

`install-package Microsoft.Owin.Diagnostics –Pre`

更改 `Startup1.Configuration` 方法中的代码，如下所示：

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

现在，使用 CTRL + F5 运行应用程序而不进行调试，以便 Visual Studio 不会在异常上中断。 应用程序的行为与以前相同，直到你导航到 `http://localhost/fail`，此时应用程序会引发异常。 错误页中间件将捕获异常，并显示包含有关错误的信息的 HTML 页面。 您可以单击选项卡以查看堆栈、查询字符串、cookie、请求标头和 OWIN 环境变量。

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a>后续步骤

- [OWIN 启动类检测](owin-startup-class-detection.md)
- [使用 OWIN 自承载 ASP.NET Web API](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [使用 OWIN 自承载 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
