---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: 添加视图（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: fa200935d83bb26c07b302449a6eba6fd67b5322
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434516"
---
# <a name="adding-a-view-vb"></a>添加视图 (VB)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。 [下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果愿意C#，请切换到本教程的[ C#版本](../cs/adding-a-view.md)。

在本部分中，我们将修改 `HelloWorldController` 类以使用视图模板文件将生成 HTML 响应的过程清晰地封装到客户端。

首先，将视图模板用于 `HelloWorldController` 类中的 `Index` 方法。 目前 `Index` 方法返回一个字符串，其中包含在控制器类中硬编码的消息。 更改 `Index` 方法以返回 `View` 对象，如下所示：

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

现在，让我们将视图模板添加到我们的项目，我们可以使用 `Index` 方法调用这些模板。 为此，请在 `Index` 方法中右键单击，然后单击 "**添加视图**"。

[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)

此时将显示 "**添加视图**" 对话框。 保留默认条目，然后单击 "**添加**" 按钮。

[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)

将创建*MvcMovie\Views\HelloWorld*文件夹和*MvcMovie\Views\HelloWorld\Index.vbhtml*文件。 可以在**解决方案资源管理器**中查看它们：

[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)

在 `<h2>` 标记下添加一些 HTML。 修改后的*MvcMovie\Views\HelloWorld\Index.vbhtml*文件如下所示。

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

运行应用程序并浏览到 &quot;hello world&quot; 控制器（`http://localhost:xxxx/HelloWorld`）。 控制器中的 `Index` 方法不会执行大量工作;它只是 `return View()`运行语句，指出我们想要使用视图模板文件来呈现客户端的响应。 由于我们未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用 *\Views\HelloWorld*文件夹中的*视图文件。* 下图显示了视图中硬编码的字符串。

[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)

看起来不错。 但请注意，浏览器的标题栏显示 &quot;索引&quot;，而页面上的大标题显示 &quot;我的 MVC 应用程序。&quot; 让我们更改这些。

## <a name="changing-views-and-layout-pages"></a>更改视图和布局页面

首先，让我们更改 MVC 应用程序 &quot;的文本。&quot; 共享文本，并在每一页上显示。 它实际上只出现在项目中的一个位置，即使它在应用程序的每一页上也是如此。 中转到**解决方案资源管理器**中的 */Views/Shared*文件夹，并打开 *\_Layout*文件。 此文件称为布局页，它是所有其他页面都使用的共享 &quot;shell&quot;。

请注意文件底部附近的 `@RenderBody()` 代码行。 `RenderBody` 是一个占位符，其中所创建的所有页面都显示在 "布局" 页中 &quot;包装&quot;。 将 `<h1>` 标题从 **&quot;** 我的 Mvc 应用程序&quot; 更改为 &quot;Mvc 电影应用程序&quot;。

[!code-html[Main](adding-a-view/samples/sample3.html)]

运行应用程序，并注意它现在会显示 &quot;MVC 电影应用&quot;。 单击 "**关于**" 链接，该页还会显示 &quot;MVC 电影应用&quot;。

下面显示了完整的 *\_布局*：

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

现在，让我们更改索引页（视图）的标题。

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

打开*MvcMovie\Views\HelloWorld\Index.vbhtml*。 有两个位置可进行更改：第一种是在浏览器的标题中显示的文本，然后是辅助标头（`<h2>` 元素）中的文本。 我们将使它们略有不同，以便您可以看到哪些代码更改了应用程序的哪一部分。

运行应用程序并浏览到`http://localhost:xx/HelloWorld`。 请注意，浏览器标题、主标题和辅助标题已更改。 在应用程序中对视图进行较小的更改时，可以轻松地对应用程序进行重大更改。 （如果没有在浏览器中看到更改，则可能正在查看缓存的内容。 在浏览器中按 Ctrl + F5 强制加载来自服务器的响应。）

[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)

但这有点 &quot;数据&quot; （在这种情况下，&quot;Hello World！&quot; 消息）是硬编码的。 MVC 应用程序有 V （views），但我们有 C （控制器），但没有 M （模型）。 稍后，我们将逐步介绍如何创建数据库并从该数据库中检索模型数据。

## <a name="passing-data-from-the-controller-to-the-view"></a>将数据从控制器传递给视图

不过，在开始使用数据库并讨论模型之前，首先请讨论将信息从控制器传递到视图。 我们想要传递视图模板所需的内容，以便向客户端呈现 HTML 响应。 这些对象通常由控制器类创建并传递给视图模板，并且它们应该只包含视图模板所需的数据，而不是更多。

以前使用 `HelloWorldController` 类时，`Welcome` 操作方法采用 `name` 和 `numTimes` 参数，然后将参数值输出到浏览器。 不要让控制器继续直接呈现此响应，而是让我们将该数据放入包中进行查看。 控制器和视图可以使用 `ViewBag` 对象来保存这些数据。 这会自动传递到视图模板，并用于使用包的内容作为数据呈现 HTML 响应。 这样一来，控制器就会考虑到其中的一项和视图模板，使我们能够在应用程序中保持&quot; &quot;分离问题。

另外，我们还可以定义一个自定义类，然后创建该对象的一个实例，用数据填充该对象并将其传递给视图。 这通常称为 ViewModel，因为它是视图的自定义模型。 但对于少量的数据，ViewBag 非常有用。

返回到*HelloWorldController*文件更改控制器内的 `Welcome` 方法，将消息和 NumTimes 置于 ViewBag 中。 ViewBag 是动态对象。 这意味着你可以将所需的任何内容放入其中。 在将某些内容放入其中之前，ViewBag 没有定义的属性。

同一个文件中的新类的完整 `HelloWorldController.vb`。

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

现在，我们的 ViewBag 包含将自动传递到该视图的数据。 同样，我们也可以在自己的对象中传递，如我们所喜欢的：

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

现在，我们需要 `WelcomeView` 模板！ 运行应用程序，以便编译新代码。 关闭浏览器，在 `Welcome` 方法中右键单击，然后单击 "**添加视图**"。

"**添加视图**" 对话框如下所示。

[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)

将以下代码添加到新欢迎中的 `<h2>` 元素下<em>。</em>vbhtml 文件。 我们会作出循环，说 &quot;Hello&quot;，因为用户应该说！

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

运行应用程序并浏览到 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

现在，数据是从 URL 获取的，并会自动传递到控制器。 控制器将数据打包到 `Model` 对象中，并将该对象传递给视图。 视图比向用户显示 HTML 数据。

[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)

嗯，这是模型的 &quot;M&quot;，而不是数据库类型。 让我们用学到的内容来创建一个电影数据库。

> [!div class="step-by-step"]
> [上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)
