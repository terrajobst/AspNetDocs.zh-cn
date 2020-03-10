---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 添加控制器 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f528c56435976c7f31fce453c834ef9eaebe6244
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485444"
---
# <a name="adding-a-controller"></a>添加控制器

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。

MVC 代表*模型-视图-控制器*。 MVC 是用于开发应用程序的一种模式，该模式设计良好、可测试且易于维护。 基于 MVC 的应用程序包含：

- **M**模式：类，这些类表示应用程序的数据，并使用验证逻辑来强制执行该数据的业务规则。
- **V**视图：应用程序用于动态生成 HTML 响应的模板文件。
- **C**控制器：用于处理传入浏览器请求、检索模型数据，然后指定将响应返回到浏览器的视图模板的类。

我们将在本系列教程中介绍所有这些概念，并向您演示如何使用它们来生成应用程序。

首先，让我们创建一个控制器类。 在**解决方案资源管理器**中，右键单击 "*控制器*" 文件夹，然后选择 "**添加控制器**"。

![](adding-a-controller/_static/image1.png)

将新控制器命名 &quot;HelloWorldController&quot;。 保留默认模板为**空 MVC 控制器**，并单击 "**添加**"。

![添加控制器](adding-a-controller/_static/image2.png)

请注意，**解决方案资源管理器**已创建名为*HelloWorldController.cs*的新文件。 文件在 IDE 中处于打开状态。

![](adding-a-controller/_static/image3.png)

将文件的内容替换为以下代码。

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

控制器方法将以 HTML 形式返回一个字符串作为示例。 控制器名为 `HelloWorldController`，上面的第一个方法名为 `Index`。 让我们从浏览器中调用它。 运行应用程序（按 F5 或 Ctrl + F5）。 在浏览器中，将 &quot;HelloWorld&quot; 追加到地址栏中的路径。 （例如，在下图中，它 `http://localhost:1234/HelloWorld.`）浏览器中的页面将类似于以下屏幕截图。 在上面的方法中，代码直接返回了一个字符串。 你已告诉系统只返回了一些 HTML，但确实返回了！

![](adding-a-controller/_static/image4.png)

ASP.NET MVC 根据传入 URL 调用不同的控制器类（以及其中的不同操作方法）。 ASP.NET MVC 使用的默认 URL 路由逻辑使用如下格式来确定要调用的代码：

`/[Controller]/[ActionName]/[Parameters]`

URL 的第一部分确定要执行的控制器类。 因此， */HelloWorld*映射到 `HelloWorldController` 类。 URL 的第二部分确定要执行的类的操作方法。 因此， */HelloWorld/Index*将导致执行 `HelloWorldController` 类的 `Index` 方法。 请注意，我们只需要浏览到 */HelloWorld* ，并且默认使用 `Index` 方法。 这是因为，名为 `Index` 的方法是将在控制器上调用的默认方法，如果未显式指定一个方法。

浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome` 方法将运行并返回字符串 &quot;这是欢迎操作方法 ...&quot;。 默认 MVC 映射 `/[Controller]/[ActionName]/[Parameters]`。 对于此 URL，采用 `HelloWorld` 控制器和 `Welcome` 操作方法。 目前尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image5.png)

让我们略微修改示例，以便可以将一些参数信息从 URL 传递到控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes = 4*）。 将 `Welcome` 方法更改为包含两个参数，如下所示。 请注意，该代码使用C#可选的参数功能，指示如果没有为该参数传递值，则 `numTimes` 参数应默认为1。

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

运行应用程序并浏览到示例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。 可在 URL 中对 `name` 和 `numtimes` 使用其他值。 [ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将命名参数从地址栏中的查询字符串映射到方法中的参数。

![](adding-a-controller/_static/image6.png)

在这两个示例中，控制器都在 &quot;的 VC&quot; 部分，即视图和控制器工作。 控制器将直接返回 HTML。 通常情况下，你不希望控制器直接返回 HTML，因为这会对代码非常麻烦。 我们通常会使用单独的视图模板文件来帮助生成 HTML 响应。 接下来，我们来看看如何实现此目的。

> [!div class="step-by-step"]
> [上一页](intro-to-aspnet-mvc-4.md)
> [下一页](adding-a-view.md)
