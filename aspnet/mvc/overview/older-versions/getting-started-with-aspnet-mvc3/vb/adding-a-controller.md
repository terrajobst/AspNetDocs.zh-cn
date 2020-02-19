---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: 添加控制器（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e77f62a9796211b0e59a99c71bc532659b7cb92
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457387"
---
# <a name="adding-a-controller-vb"></a>添加控制器 (VB)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。 [下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果愿意C#，请切换到本教程的[ C#版本](../cs/adding-a-controller.md)。

MVC 代表*模型-视图-控制器*。 MVC 是用于开发应用程序的一种模式，因此，每个部分都有单独的责任：

- 模型：应用程序的数据。
- 视图：你的应用程序将用于动态生成 HTML 响应的模板文件。
- 控制器：用于处理对应用程序的传入 URL 请求、检索模型数据，然后指定用于呈现客户端响应的视图模板的类。

我们将在本教程中介绍所有这些概念，并说明如何使用它们来生成应用程序。

右键单击 "**解决方案资源管理器**中的"*控制器*"文件夹，然后选择"**添加控制器**"，创建新的控制器。

[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)

将新控制器命名 &quot;HelloWorldController&quot; 并单击 "**添加**"。

[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)

请注意，在右侧**解决方案资源管理器**，已为你创建了一个名为*HelloWorldController.cs*的新文件，并且该文件在 IDE 中处于打开状态。

在新的 `public class HelloWorldController` 块中，创建两个类似于以下代码的新方法。 作为示例，我们将直接从控制器返回 HTML 字符串。

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

控制器名为 `HelloWorldController`，新的方法名为 `Index`。 运行应用程序（按 F5 或 Ctrl + F5）。 浏览器启动后，将 &quot;HelloWorld&quot; 追加到地址栏中的路径。 （在我的计算机上，它是 `http://localhost:43246/HelloWorld`）你的浏览器将类似于下面的屏幕截图。 在上面的方法中，代码直接返回了一个字符串。 我们告诉系统只需返回一些 HTML，就是这样！

![](adding-a-controller/_static/image5.png)

ASP.NET MVC 根据传入 URL 调用不同的控制器类（以及其中的不同操作方法）。 ASP.NET MVC 使用的默认映射逻辑使用如下格式来控制要调用的代码：

`/[Controller]/[ActionName]/[Parameters]`

URL 的第一部分确定要执行的控制器类。 因此， */HelloWorld*映射到 `HelloWorldController` 类。 URL 的第二部分确定要执行的类的操作方法。 因此， */HelloWorld/Index*将导致执行 `HelloWorldController` 类的 `Index` 方法。 请注意，我们只需要访问上面的 */HelloWorld* ，默认情况下使用 `Index` 方法。 这是因为，名为 `Index` 的方法是将在控制器上调用的默认方法，如果未显式指定一个方法。

浏览到 `http://localhost:xxxx/HelloWorld/Welcome`。 `Welcome` 方法将运行并返回字符串 &quot;这是欢迎操作方法 ...&quot;。 默认 MVC 映射 `/[Controller]/[ActionName]/[Parameters]`。 对于此 URL，控制器是 `HelloWorld` 的，`Welcome` 为方法。 尚未使用 URL 的 `[Parameters]` 部分。

![](adding-a-controller/_static/image6.png)

让我们略微修改示例，以便我们可以将中的一些参数信息从 URL 传递到控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes = 4*）。 将 `Welcome` 方法更改为包含两个参数，如下所示。 请注意，我们已使用 VB 可选参数功能，指示如果没有为该参数传递值，则 `numTimes` 参数应默认为1。

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

运行应用程序并浏览到 `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` **。** 可以为 `name` 和 `numtimes`尝试不同的值。 系统会自动将地址栏中的查询字符串中的命名参数映射到方法中的参数。

![](adding-a-controller/_static/image7.png)

在这两个示例中，控制器都在执行 MVC 的 VC 部分，即视图和控制器工作。 控制器将直接返回 HTML。 通常，我们不希望控制器直接返回 HTML，因为这对代码而言非常麻烦。 我们通常会使用单独的视图模板文件来帮助生成 HTML 响应。 我们来看看如何实现此目的。

> [!div class="step-by-step"]
> [上一页](intro-to-aspnet-mvc-3.md)
> [下一页](adding-a-view.md)
