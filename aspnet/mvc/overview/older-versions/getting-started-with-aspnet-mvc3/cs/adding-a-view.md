---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 添加视图（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: b4a1316feb8d9b7f3ef5ca4755bf1cc5b23e6ef9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498842"
---
# <a name="adding-a-view-c"></a>添加视图 (C#)

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

在本节中，您将修改 `HelloWorldController` 类以使用视图模板文件来将生成 HTML 响应的过程清晰地封装到客户端。

你将使用 ASP.NET MVC 3 中引入的新的[Razor 视图引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)创建视图模板文件。 基于 Razor 的视图模板的文件扩展名为*cshtml* ，并提供使用C#创建 HTML 输出的简洁方法。 Razor 最大程度地减少了编写视图模板时所需的字符和击键数量，并启用了快速、流畅的编码工作流。

首先将视图模板与 `HelloWorldController` 类中的 `Index` 方法一起使用。 当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。 更改 `Index` 方法以返回 `View` 对象，如下所示：

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

此代码使用视图模板生成浏览器的 HTML 响应。 在项目中，添加可与 `Index` 方法一起使用的视图模板。 为此，请在 `Index` 方法中右键单击，然后单击 "**添加视图**"。

![](adding-a-view/_static/image1.png)

此时将显示 "**添加视图**" 对话框。 保留默认值，并单击 "**添加**" 按钮：

![](adding-a-view/_static/image2.png)

将创建*MvcMovie\Views\HelloWorld*文件夹和*MvcMovie\Views\HelloWorld\Index.cshtml*文件。 可以在**解决方案资源管理器**中查看它们：

![](adding-a-view/_static/image3.png)

下面显示了已创建的*索引 cshtml*文件：

[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)

在 `<h2>` 标记下添加一些 HTML。 修改后的*MvcMovie\Views\HelloWorld\Index.cshtml*文件如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

运行应用程序并浏览到 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。 控制器中的 `Index` 方法不会执行大量工作;它只是 `return View()`运行语句，该语句指定方法应使用视图模板文件来呈现对浏览器的响应。 由于未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用 *\Views\HelloWorld*文件夹中的*视图文件。* 下图显示了视图中硬编码的字符串。

![](adding-a-view/_static/image6.png)

看起来不错。 但请注意，浏览器的标题栏显示 "索引"，而页面上的大标题显示为 "我的 MVC 应用程序"。 让我们更改这些。

## <a name="changing-views-and-layout-pages"></a>更改视图和布局页

首先，您需要更改页面顶部的 "我的 MVC 应用程序" 标题。 该文本对于每个页面都是通用的。 它实际上只在项目中的一个位置实现，即使它显示在应用程序中的每一页上也是如此。 中转到**解决方案资源管理器**中的 */Views/Shared*文件夹，然后打开 *\_的布局 cshtml*文件。 此文件称为*布局页面*，它是所有其他页面都使用的共享 "shell"。

[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)

布局模板允许在一个位置指定网站的 HTML 容器布局，然后将其应用到站点中的多个页面。 请注意文件底部附近的 `@RenderBody()` 行。 `RenderBody` 是一个占位符，其中所创建的所有视图特定页面都显示在 "布局" 页中的 "已包装"。 将布局模板中的标题标题从 "我的 MVC 应用程序" 更改为 "MVC 电影应用"。

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

运行该应用程序，请注意，它现在显示 "MVC 电影应用"。 单击 "**关于**" 链接，你将看到该页面还显示 "MVC 电影应用"。 我们能够在布局模板中进行一次更改，并让网站上的所有页面都反映新标题。

![](adding-a-view/_static/image9.png)

完整的 *\_布局 cshtml*文件如下所示：

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

现在，让我们更改索引页（视图）的标题。

打开*MvcMovie\Views\HelloWorld\Index.cshtml*。 有两个位置可进行更改：第一种是在浏览器的标题中显示的文本，然后是辅助标头（`<h2>` 元素）中的文本。 稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

若要指示要显示的 HTML 标题，上面的代码将设置 `ViewBag` 对象（在*索引. cshtml*视图模板中）的 `Title` 属性。 如果你查看布局模板的源代码，你会注意到，模板在 HTML 的 `<head>` 部分中使用 `<title>` 元素中的此值。 使用此方法，您可以轻松地在视图模板和布局文件之间传递其他参数。

运行应用程序并浏览到 `http://localhost:xx/HelloWorld`。 请注意，浏览器标题、主标题和辅助标题已更改。 （如果没有在浏览器中看到更改，则可能正在查看缓存的内容。 在浏览器中按 Ctrl + F5 强制加载来自服务器的响应。）

另请注意， *Index.* view 模板中的内容是如何与 *\_Layout*视图模板合并的，并向浏览器发送单个 HTML 响应。 凭借布局模板可以很容易地对应用程序中所有页面进行更改。

![](adding-a-view/_static/image10.png)

但我们这一点点“数据”（在此示例中为“Hello from our View Template!” 消息）是硬编码的。 MVC 应用程序有一个“V”（视图），而你已有一个“C”（控制器），但还没有“M”（模型）。 稍后，我们将逐步介绍如何创建数据库并从该数据库中检索模型数据。

## <a name="passing-data-from-the-controller-to-the-view"></a>将数据从控制器传递给视图

不过，在开始使用数据库并讨论模型之前，首先请讨论将信息从控制器传递到视图。 为了响应传入 URL 请求，将调用控制器类。 控制器类用于编写处理传入参数的代码、从数据库检索数据，并最终决定要发送回浏览器的响应类型。 然后，可以从控制器使用视图模板来生成 HTML 响应并设置其格式。

控制器负责提供所需的任何数据或对象，以便视图模板呈现对浏览器的响应。 视图模板不应执行业务逻辑或直接与数据库交互。 相反，它应仅适用于控制器为其提供的数据。 维护这种 "问题分离" 有助于使代码更干净且更易维护。

当前，`HelloWorldController` 类中的 `Welcome` 操作方法采用 `name` 和 `numTimes` 参数，然后将值直接输出到浏览器。 不要让控制器将此响应呈现为字符串，而是将控制器改为使用视图模板。 视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。 为此，可以让控制器将视图模板所需的动态数据放置在视图模板可以访问 `ViewBag` 对象中。

返回到*HelloWorldController.cs*文件，更改 `Welcome` 方法，将 `Message` 和 `NumTimes` 值添加到 `ViewBag` 对象。 `ViewBag` 是动态对象，这意味着你可以将所需的任何内容放在其中：在将对象放入其中之前，`ViewBag` 对象没有定义的属性。 完整的 HelloWorldController.cs 文件如下所示：

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

现在 `ViewBag` 对象包含将自动传递到该视图的数据。

接下来，需要一个欢迎视图模板！ 在 "**调试**" 菜单中，选择 "**生成 MvcMovie** " 以确保项目已编译。

[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)

然后在 `Welcome` 方法中右键单击，然后单击 "**添加视图**"。 "**添加视图**" 对话框如下所示：

![](adding-a-view/_static/image13.png)

单击 "**添加**"，然后在新的 "*欢迎*#" 文件中的 `<h2>` 元素下添加以下代码。 你将创建一个循环，该循环显示 "Hello" 的次数与用户所示的次数相同。 下面显示了完整的*欢迎. cshtml*文件。

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

运行应用程序并浏览到以下 URL：

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

现在，数据是从 URL 获取的，并会自动传递到控制器。 控制器将数据打包到 `ViewBag` 对象中，并将该对象传递给视图。 然后，视图将以 HTML 格式向用户显示数据。

![](adding-a-view/_static/image14.png)

当然，这是模型的一种“M”类型，而不是数据库类。 让我们用学到的内容来创建一个电影数据库。

> [!div class="step-by-step"]
> [上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)
