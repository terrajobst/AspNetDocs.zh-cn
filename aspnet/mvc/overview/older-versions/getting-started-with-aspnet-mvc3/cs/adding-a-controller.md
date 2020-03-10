---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: 添加控制器（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 959116ff773f4ef466cda6b172e8321590b50e5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434960"
---
# <a name="adding-a-controller-c"></a>添加控制器 (C#)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。
> 
> 
> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题提供了包含C#源代码的 Visual Web Developer 项目。 [下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。

MVC 代表*模型-视图-控制器*。 MVC 是一种用于开发设计良好且易于维护的应用程序的模式。 基于 MVC 的应用程序包含：

- 控制器：用于处理对应用程序的传入请求、检索模型数据，然后指定将响应返回客户端的视图模板的类。
- 模型：类，这些类表示应用程序的数据，并使用验证逻辑来强制执行该数据的业务规则。
- 视图：应用程序用于动态生成 HTML 响应的模板文件。

我们将在本系列教程中介绍所有这些概念，并向您演示如何使用它们来生成应用程序。

首先，让我们创建一个控制器类。 在**解决方案资源管理器**中，右键单击 "*控制器*" 文件夹，然后选择 "**添加控制器**"。

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

将新控制器命名为 "HelloWorldController"。 保留默认模板为**空控制器**，并单击 "**添加**"。

[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)

请注意，**解决方案资源管理器**已创建名为*HelloWorldController.cs*的新文件。 文件在 IDE 中处于打开状态。

![](adding-a-controller/_static/image5.png)

在 `public class HelloWorldController` 块中，创建两个类似于以下代码的方法。 控制器将返回 HTML 字符串作为示例。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

控制器名为 `HelloWorldController`，上面的第一个方法名为 `Index`。 让我们从浏览器中调用它。 运行应用程序（按 F5 或 Ctrl + F5）。 在浏览器中，将 "HelloWorld" 追加到地址栏中的路径。 （例如，在下图中，它 `http://localhost:43246/HelloWorld.`）浏览器中的页面将类似于以下屏幕截图。 在上面的方法中，代码直接返回了一个字符串。 你已告诉系统只返回了一些 HTML，但确实返回了！

![](adding-a-controller/_static/image6.png)

ASP.NET MVC 根据传入 URL 调用不同的控制器类（以及其中的不同操作方法）。 ASP.NET MVC 使用的默认映射逻辑使用如下格式来确定要调用的代码：

`/[Controller]/[ActionName]/[Parameters]`

URL 的第一部分确定要执行的控制器类。 因此， */HelloWorld*映射到 `HelloWorldController` 类。 URL 的第二部分确定要执行的类的操作方法。 因此， */HelloWorld/Index*将导致执行 `HelloWorldController` 类的 `Index` 方法。 请注意，我们只需要浏览到 */HelloWorld* ，并且默认使用 `Index` 方法。 这是因为，名为 `Index` 的方法是将在控制器上调用的默认方法，如果未显式指定一个方法。

浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome` 方法运行并返回字符串“这是 Welcome 操作方法...”。 默认 MVC 映射 `/[Controller]/[ActionName]/[Parameters]`。 对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。 目前尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image7.png)

让我们略微修改示例，以便可以将一些参数信息从 URL 传递到控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes = 4*）。 将 `Welcome` 方法更改为包含两个参数，如下所示。 请注意，该代码使用C#可选的参数功能，指示如果没有为该参数传递值，则 `numTimes` 参数应默认为1。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

运行应用程序并浏览到示例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。 可在 URL 中对 `name` 和 `numtimes` 使用其他值。 系统自动将命名参数从地址栏中的查询字符串映射到方法中的参数。

![](adding-a-controller/_static/image8.png)

在这两个示例中，控制器都在执行 MVC 的 "VC" 部分，即视图和控制器工作。 控制器将直接返回 HTML。 通常情况下，你不希望控制器直接返回 HTML，因为这会对代码非常麻烦。 我们通常会使用单独的视图模板文件来帮助生成 HTML 响应。 接下来，我们来看看如何实现此目的。

> [!div class="step-by-step"]
> [上一页](intro-to-aspnet-mvc-3.md)
> [下一页](adding-a-view.md)
