---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: 添加视图 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教程的更新版本可在此处使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更简单的操作和演示 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 81c2e1f46b08cbc9b5aa5d6c1b36d9d8dc2ba581
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485366"
---
# <a name="adding-a-view"></a>添加视图

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。

在本节中，您将修改 `HelloWorldController` 类以使用视图模板文件来将生成 HTML 响应的过程清晰地封装到客户端。

你将使用 ASP.NET MVC 3 引入的[Razor 视图引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)创建视图模板文件。 基于 Razor 的视图模板的文件扩展名为*cshtml* ，并提供使用C#创建 HTML 输出的简洁方法。 Razor 最大程度地减少了编写视图模板时所需的字符和击键数量，并启用了快速、流畅的编码工作流。

当前，`Index` 方法返回带有在控制器类中硬编码的消息的字符串。 更改 `Index` 方法以返回 `View` 对象，如以下代码所示：

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

上面的 `Index` 方法使用视图模板生成浏览器的 HTML 响应。 控制器方法（也称为[操作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)）（如上述 `Index` 方法）通常返回[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) （或派生自[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)的类），而不是基元类型（如 string）。

在项目中，添加可与 `Index` 方法一起使用的视图模板。 为此，请在 `Index` 方法中右键单击，然后单击 "**添加视图**"。

![](adding-a-view/_static/image1.png)

此时将显示 "**添加视图**" 对话框。 保留默认值，并单击 "**添加**" 按钮：

![](adding-a-view/_static/image2.png)

将创建*MvcMovie\Views\HelloWorld*文件夹和*MvcMovie\Views\HelloWorld\Index.cshtml*文件。 可以在**解决方案资源管理器**中查看它们：

![](adding-a-view/_static/image3.png)

下面显示了已创建的*索引 cshtml*文件：

![HelloWorldIndex](adding-a-view/_static/image4.png)

在 `<h2>` 标记下添加以下 HTML。

[!code-html[Main](adding-a-view/samples/sample2.html)]

完整的*MvcMovie\Views\HelloWorld\Index.cshtml*文件如下所示。

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

如果使用的是 Visual Studio 2012，请在 "解决方案资源管理器" 中，右键单击*索引.* # 文件，然后**在 Page Inspector 中选择 "查看**"。

![PI](adding-a-view/_static/image5.png)

[Page Inspector 教程](../../views/using-page-inspector-in-aspnet-mvc.md)包含有关此新工具的详细信息。

或者，运行应用程序并浏览到 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。 控制器中的 `Index` 方法不会执行大量工作;它只是 `return View()`运行语句，该语句指定方法应使用视图模板文件来呈现对浏览器的响应。 由于未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用 *\Views\HelloWorld*文件夹中的*视图文件。* 下图显示了我们的视图模板 &quot;的字符串！视图中&quot; 硬编码。

![](adding-a-view/_static/image6.png)

看起来不错。 但请注意，浏览器的标题栏显示 &quot;索引我的 ASP.NET A&quot;，页面顶部的大链接显示此处 &quot;徽标。下面&quot; &quot;你的徽标。&quot; "链接" 是 "注册" 和 "登录" 链接，并链接到 "主页"、"关于" 和 "联系人" 页。 我们来更改其中一些。

## <a name="changing-views-and-layout-pages"></a>更改视图和布局页

首先，需要在此处更改徽标 &quot;。页面顶部&quot; 标题。 该文本对于每个页面都是通用的。 它实际上只在项目中的一个位置实现，即使它显示在应用程序的每一页上也是如此。 中转到**解决方案资源管理器**中的 */Views/Shared*文件夹，然后打开 *\_的布局 cshtml*文件。 此文件称为*布局页*，它是所有其他页面都使用的共享 &quot;shell&quot;。

![_LayoutCshtml](adding-a-view/_static/image7.png)

布局模板允许在一个位置指定网站的 HTML 容器布局，然后将其应用到站点中的多个页面。 查找 `@RenderBody()` 行。 `RenderBody` 是显示创建的所有特定于视图的页面的占位符，已包装在布局页面中&quot;&quot;。 例如，如果选择 "关于" 链接，则会在 `RenderBody` 方法中呈现*Views\Home\About.cshtml*视图。

在此处&quot; &quot;徽标，将布局模板中的网站标题标题更改为 &quot;MVC 电影&quot;。

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

将 title 元素的内容替换为以下标记：

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

运行该应用程序，请注意，它现在显示 &quot;MVC 电影 &quot;。 单击 "**关于**" 链接，你将看到该页面还 &quot;MVC 电影&quot;中的显示方式。 我们能够在布局模板中进行一次更改，并让网站上的所有页面都反映新标题。

![](adding-a-view/_static/image8.png)

现在，让我们更改索引视图的标题。

打开*MvcMovie\Views\HelloWorld\Index.cshtml*。 有两个位置可进行更改：第一种是在浏览器的标题中显示的文本，然后是辅助标头（`<h2>` 元素）中的文本。 稍稍对它们进行一些更改，这样可以看出哪一段代码更改了应用的哪部分。

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

若要指示要显示的 HTML 标题，上面的代码将设置 `ViewBag` 对象（在*索引. cshtml*视图模板中）的 `Title` 属性。 如果你查看布局模板的源代码，你会注意到，模板在 `<title>` 元素中使用此值作为之前修改的 HTML 的 `<head>` 部分。 使用此 `ViewBag` 方法，可以轻松地在视图模板和布局文件之间传递其他参数。

运行应用程序并浏览到 `http://localhost:xx/HelloWorld`。 请注意，浏览器标题、主标题和辅助标题已更改。 （如果没有在浏览器中看到更改，则可能正在查看缓存的内容。 在浏览器中按 Ctrl + F5 来强制加载来自服务器的响应。）浏览器标题是通过在*Index. cshtml*视图模板中设置的 `ViewBag.Title` 创建的，而其他 &quot;电影应用&quot; 添加到布局文件中。

另请注意， *Index.* view 模板中的内容是如何与 *\_Layout*视图模板合并的，并向浏览器发送单个 HTML 响应。 凭借布局模板可以很容易地对应用程序中所有页面进行更改。

![](adding-a-view/_static/image9.png)

不过，我们的 &quot;数据&quot; （在这种情况下，我们的视图模板！&quot; 消息中的 &quot;Hello）是硬编码的。 MVC 应用程序有一个 &quot;V&quot; （视图），并且你有 &quot;C&quot; （控制器），但没有 &quot;M&quot; （模型）。 稍后，我们将逐步介绍如何创建数据库并从该数据库中检索模型数据。

## <a name="passing-data-from-the-controller-to-the-view"></a>将数据从控制器传递给视图

不过，在开始使用数据库并讨论模型之前，首先请讨论将信息从控制器传递到视图。 为了响应传入 URL 请求，将调用控制器类。 通过控制器类，您可以编写处理传入浏览器请求的代码，从数据库中检索数据，并最终决定要发送回浏览器的响应类型。 然后，可以从控制器使用视图模板来生成 HTML 响应并设置其格式。

控制器负责提供所需的任何数据或对象，以便视图模板呈现对浏览器的响应。 最佳做法：**视图模板不应执行业务逻辑或直接与数据库交互**。 相反，视图模板应仅适用于控制器为其提供的数据。 保持此 &quot;分离关注点&quot; 有助于使你的代码更干净、可测试、更易于维护。

当前，`HelloWorldController` 类中的 `Welcome` 操作方法采用 `name` 和 `numTimes` 参数，然后将值直接输出到浏览器。 不要让控制器将此响应呈现为字符串，而是将控制器改为使用视图模板。 视图模板将生成动态响应，这意味着你需要将适当的数据位从控制器传递给视图以生成响应。 为此，可以让控制器将视图模板所需的动态数据（参数）放置在视图模板可以访问 `ViewBag` 对象中。

返回到*HelloWorldController.cs*文件，更改 `Welcome` 方法，将 `Message` 和 `NumTimes` 值添加到 `ViewBag` 对象。 `ViewBag` 是动态对象，这意味着你可以将所需的任何内容放在其中：在将对象放入其中之前，`ViewBag` 对象没有定义的属性。 [ASP.NET MVC 模型绑定系统](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)自动将命名参数（`name` 和 `numTimes`）从地址栏中的查询字符串映射到方法中的参数。 完整的 HelloWorldController.cs 文件如下所示：

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

现在 `ViewBag` 对象包含将自动传递到该视图的数据。

接下来，需要一个欢迎视图模板！ 在 "**生成**" 菜单中，选择 "**生成 MvcMovie** " 以确保项目已编译。

然后在 `Welcome` 方法中右键单击，然后单击 "**添加视图**"。

![](adding-a-view/_static/image10.png)

"**添加视图**" 对话框如下所示：

![](adding-a-view/_static/image11.png)

单击 "**添加**"，然后在新的 "*欢迎*#" 文件中的 `<h2>` 元素下添加以下代码。 你将创建一个循环，该循环显示 &quot;Hello&quot; 用户应尽可能多地显示。 下面显示了完整的*欢迎. cshtml*文件。

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

运行应用程序并浏览到以下 URL：

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

现在，数据是从 URL 获取的，并使用[模型绑定](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)器传递到控制器。 控制器将数据打包到 `ViewBag` 对象中，并将该对象传递给视图。 然后，视图将以 HTML 格式向用户显示数据。

![](adding-a-view/_static/image12.png)

在上面的示例中，我们使用 `ViewBag` 对象将数据从控制器传递到视图。 在本教程中，我们将使用视图模型将数据从控制器传递到视图。 用于传递数据的视图模型方法通常比查看包方法更可取。 有关详细信息，请参阅博客文章[动态 V 强类型视图](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)。

嗯，这是模型的 &quot;M&quot;，而不是数据库类型。 让我们用学到的内容来创建一个电影数据库。

> [!div class="step-by-step"]
> [上一页](adding-a-controller.md)
> [下一页](adding-a-model.md)
