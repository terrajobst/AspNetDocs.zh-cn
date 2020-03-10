---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: 第3部分：视图和 Viewmodel |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第3部分介绍了视图和 Viewmodel。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451130"
---
# <a name="part-3-views-and-viewmodels"></a>第3部分：视图和 Viewmodel

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。  
>   
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第3部分介绍了视图和 Viewmodel。

到目前为止，我们刚刚从控制器操作返回了字符串。 这是了解控制器工作方式的好方法，但并不是您想要如何构建真实的 web 应用程序。 我们想要一种更好的方法来向访问站点的浏览器生成 HTML，其中一种方法是，我们可以使用模板文件更轻松地自定义要发回的 HTML 内容。 这正是视图的作用。

## <a name="adding-a-view-template"></a>添加视图模板

若要使用视图模板，我们将更改 HomeController Index 方法以返回 ActionResult，并使其返回 View （），如下所示：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

上述更改指出，而不是返回字符串，而是想要使用 "视图" 来生成结果。

现在，我们将向项目中添加相应的视图模板。 为此，我们将文本光标置于索引操作方法中，然后右键单击并选择 "添加视图"。 此时将显示 "添加视图" 对话框：

![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)

"添加视图" 对话框使我们能够快速轻松地生成视图模板文件。 默认情况下，"添加视图" 对话框预先填充要创建的视图模板的名称，使其与将使用它的操作方法相匹配。 因为我们在 HomeController 的 Index （）操作方法中使用了 "添加视图" 上下文菜单，所以上面的 "添加视图" 对话框具有 "索引"，因为默认情况下填充了视图名称。 我们不需要更改此对话框中的任何选项，因此请单击 "添加" 按钮。

单击 "添加" 按钮后，Visual Web Developer 会在 \Views\Home 目录中创建新的 "索引" 视图模板（如果尚不存在，则创建该文件夹）。

![](mvc-music-store-part-3/_static/image2.png)

"ASP.NET" 文件的名称和文件夹位置很重要，并遵循默认的 "MVC 命名约定"。 目录名称 \Views\Home 与名为 HomeController 的控制器匹配。 视图模板名称、索引与将显示视图的控制器操作方法相匹配。

当我们使用此命名约定返回视图时，ASP.NET MVC 使我们无需显式指定视图模板的名称或位置。 当我们在我们的 HomeController 中编写如下代码时，它将默认呈现 \Views\Home\Index.cshtml 视图模板：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

在单击 "添加视图" 对话框中的 "添加" 按钮后，Visual Web Developer 创建并打开了 "Index. cshtml" 视图模板。 下面显示了 Index 的内容。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

此视图使用的是 Razor 语法，这比在 ASP.NET Web 窗体和 ASP.NET MVC 的以前版本中使用的 Web 窗体视图引擎更为简洁。 Web 窗体视图引擎在 ASP.NET MVC 3 中仍可用，但许多开发人员发现，Razor 视图引擎适用于 ASP.NET MVC 开发确实很好。

前三行使用 ViewBag 设置页面标题。 稍后我们将更详细地介绍此功能的工作原理，但首先我们来更新文本标题文本并查看该页。 将 &lt;h2&gt; 标记更新为 "这是主页"，如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

运行该应用程序时，会显示新文本显示在主页上。

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a>使用通用网站元素的布局

大多数网站包含许多页面之间共享的内容：导航、页脚、徽标图像、样式表引用等。使用 Razor 视图引擎可以轻松地使用名为 \_Layout 的页面进行管理，该页面已在/Views/Shared 文件夹中自动创建。

![](mvc-music-store-part-3/_static/image4.png)

双击此文件夹以查看内容，如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

来自各个视图的内容将由 @RenderBody（）命令显示，并且我们希望在其外部显示的任何通用内容都可添加到 \_的布局。 cshtml 标记。 我们会希望我们的 MVC 音乐商店具有一个通用标头，其中包含指向主页的链接，并在站点中的所有页面上存储区域，因此，我们会将该标头添加到 @RenderBody（）语句前面的模板。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a>更新样式表

空项目模板包含一个非常简单的 CSS 文件，其中只包含用于显示验证消息的样式。 设计器还提供了一些其他 CSS 和图像来定义站点的外观，因此我们将在其中立即添加。

已更新的 CSS 文件和映像包含在 MvcMusicStore-Assets 的内容目录中，该目录可在[MVC-音乐存储](https://github.com/evilDave/MVC-Music-Store)中找到。 我们会在 Windows 资源管理器中选择这两个文件，并将其放在 Visual Web Developer 的解决方案内容文件夹中，如下所示：

![](mvc-music-store-part-3/_static/image5.png)

系统会要求你确认是否要覆盖现有的 web.config 文件。 单击“是”。

![](mvc-music-store-part-3/_static/image6.png)

应用程序的内容文件夹现在如下所示：

![](mvc-music-store-part-3/_static/image7.png)

现在，让我们运行应用程序，并查看主页上的更改的外观。

![](mvc-music-store-part-3/_static/image8.png)

- 让我们回顾一下所做的更改： HomeController 的索引操作方法会找到并显示 \Views\Home\Index.cshtmlView 模板，尽管我们的视图模板遵循了标准命名约定，但我们的视图模板却是 "返回视图（）"。
- 主页正在显示在 \Views\Home\Index.cshtml 视图模板内定义的简单欢迎消息。
- 主页正在使用我们的 \_布局 cshtml 模板，因此欢迎消息包含在标准网站 HTML 布局中。

## <a name="using-a-model-to-pass-information-to-our-view"></a>使用模型将信息传递给我们的视图

只显示硬编码 HTML 的视图模板不会产生非常有趣的网站。 要创建动态网站，我们将改为将控制器操作的信息传递给视图模板。

在 "模型-视图-控制器" 模式中，术语 "模型" 是指表示应用程序中的数据的对象。 通常，模型对象与数据库中的表相对应，但不一定要这样做。

返回 ActionResult 的控制器操作方法可以将模型对象传递到视图。 这样一来，控制器就可以将生成响应所需的所有信息完全打包，然后将此信息传递到一个视图模板以生成相应的 HTML 响应。 通过查看其工作方式，可以更轻松地了解这一点，因此让我们开始吧。

首先，我们将创建一些模型类来表示商店中的流派和唱片集。 首先，让我们创建一个流派类。 右键单击项目中的 "模型" 文件夹，选择 "添加类" 选项，并将文件命名为 "Genre.cs"。

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

然后，将公共字符串名称属性添加到已创建的类：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

*注意：如果您想知道，{get; set;} 表示法正在使用C#自动实现的属性功能。这为我们提供了属性的优点，而无需声明支持字段。*

接下来，请按照相同的步骤创建具有标题和流派属性的唱片集类（名为 Album.cs）：

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

现在，我们可以修改 StoreController，以使用显示模型中的动态信息的视图。 如果现在为-出于演示目的，我们根据请求 ID 命名了唱集，我们可以像下面的视图所示显示该信息。

![](mvc-music-store-part-3/_static/image10.png)

首先，我们将更改存储详细信息操作，以便显示单个唱片集的信息。 在**StoreControllers**类的顶部添加一个 "using" 语句以包括 MvcMusicStore 命名空间，因此，每次使用唱片集类时，不需要键入 MvcMusicStore。 该类的 "using" 部分现在应如下所示。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

接下来，我们将更新详细信息控制器操作，使其返回 ActionResult 而不是字符串，就像使用 HomeController 的 Index 方法时所做的一样。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

现在，我们可以修改逻辑以将唱片集对象返回到视图中。 稍后在本教程中，我们将从数据库中检索数据，但现在，我们将使用 "虚拟数据" 开始使用。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

*注意：如果不熟悉C#，则可以假设使用 var 表示我们的唱集变量为后期绑定。这不是正确的– C#编译器将根据我们分配给变量的内容来使用类型推理来确定唱片集属于唱片集类型，并将本地唱片集变量编译为唱片集类型，因此我们将获得编译时检查和 Visual Studio 代码编辑器支持。*

现在，让我们创建一个使用唱片集生成 HTML 响应的视图模板。 在执行此操作之前，我们需要生成项目，以便 "添加视图" 对话框知道我们新创建的唱集类。 可以通过选择 "调试⇨生成 MvcMusicStore" 菜单项来生成项目（为实现额外信用，可以使用 Ctrl + Shift-B 快捷方式生成项目）。

![](mvc-music-store-part-3/_static/image11.png)

现在我们已经设置了支持类，接下来可以构建视图模板。 右键单击详细信息方法，然后选择 "添加视图 ..."从上下文菜单中。

![](mvc-music-store-part-3/_static/image12.png)

我们将创建一个新的视图模板，就像我们在使用 HomeController 之前做的一样。 由于我们是从 StoreController 创建它，因此默认情况下将在 \Views\Store\Index.cshtml 文件中生成它。

与之前不同，我们将选中 "创建强类型的视图" 复选框。 接下来，我们将在 "查看数据类" 下拉 downlist 中选择 "唱片集" 类。 这将导致 "添加视图" 对话框创建一个需要将唱片集对象传递到其使用的视图模板。

![](mvc-music-store-part-3/_static/image13.png)

单击 "添加" 按钮时，将创建 \Views\Store\Details.cshtml 视图模板，其中包含以下代码。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

请注意第一行，它指示此视图已强类型化到我们的唱片集类中。 Razor 视图引擎了解它已传递一个唱片集对象，因此我们可以轻松地访问模型属性，甚至可以在 Visual Web Developer 编辑器中获得 IntelliSense 的好处。

更新 &lt;h2&gt; 标记，使其显示唱片集的 Title 属性，方法是将该行修改为如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

请注意，在输入 @Model 关键字之后的时间段时，将触发 IntelliSense，其中显示了唱片集类支持的属性和方法。

现在，让我们重新运行项目并访问/Store/Details/5 URL。 我们将看到如下唱片集的详细信息。

![](mvc-music-store-part-3/_static/image14.png)

现在，我们将对 "存储浏览" 操作方法进行类似更新。 更新方法，使其返回 ActionResult，并修改方法逻辑，使其创建新的流派对象并将其返回给视图。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

右键单击浏览方法，然后选择 "添加视图 ..."在上下文菜单中，添加一个强类型的视图，将强类型化添加到流派类中。

![](mvc-music-store-part-3/_static/image15.png)

更新视图代码中的 &lt;h2&gt; 元素（在/Views/Store/Browse.cshtml 中）以显示流派信息。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

现在，让我们重新运行项目并浏览到/Store/Browse？流派 = Disco URL。 我们会看到如下所示的浏览页。

![](mvc-music-store-part-3/_static/image16.png)

最后，让我们对**商店索引**操作方法和视图进行稍微复杂的更新，以显示我们的商店中所有流派的列表。 我们将使用流派列表作为模型对象，而不只是使用单个流派来实现此目的。

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

右键单击 "存储索引" 操作方法，然后选择 "添加视图"，选择 "流派" 作为模型类，并按 "添加" 按钮。

![](mvc-music-store-part-3/_static/image17.png)

首先，我们将更改 @model 声明，以指示该视图将需要多个流派对象，而不只是一个。 更改/Store/Index.cshtml 的第一行，如下所示：

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

这会告诉 Razor 视图引擎它将使用可以容纳多个流派对象的模型对象。 我们使用的是 IEnumerable&lt;流派&gt; 而不是&lt;流派&gt; 列表，因为它更通用，使我们能够将模型类型以后更改为支持 IEnumerable 接口的任何对象类型。

接下来，我们将遍历模型中的流派对象，如下所示。

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

请注意，我们在输入此代码时具有完全的 IntelliSense 支持，因此，在我们输入 "@Model" 时。 我们看到类型为 "流派" 的 IEnumerable 支持的所有方法和属性。

![](mvc-music-store-part-3/_static/image18.png)

在我们的 "foreach" 循环中，Visual Web Developer 知道每个项的类型为 "流派"，因此我们会看到每个流派类型的 IntelliSense。

![](mvc-music-store-part-3/_static/image19.png)

接下来，基架功能检查了流派对象，并确定每个对象都有一个 Name 属性，以便循环访问并将其写入。它还会生成每个单独项的编辑、详细信息和删除链接。 我们稍后会在我们的商店经理中利用这一点，但现在，我们想要创建一个简单的列表。

当我们运行该应用程序并浏览到/Store 时，我们看到显示了 "计数" 和 "流派列表"。

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a>在页面之间添加链接

当前列出流派的/Store URL 仅以纯文本形式列出流派名称。 让我们对此进行更改，而不是将纯文本改为将流派名称链接到相应的/Store/Browse URL，这样，单击类似于 "Disco" 的音乐流派就会导航到/Store/Browse？流派 = Disco URL。 我们可以使用类似下面的代码更新 \Views\Store\Index.cshtml 视图模板来输出这些链接 **（不要在此中进行改进）** ：

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

这种方法很有效，但可能会在以后出现问题，因为它依赖于硬编码的字符串。 例如，如果我们要重命名控制器，则需要在代码中搜索，查找需要更新的链接。

可使用的替代方法是利用 HTML 帮助器方法。 ASP.NET MVC 包含 HTML Helper 方法，这些方法可从我们的查看模板代码中使用，以执行与此类似的各种常见任务。 .Html （） helper 方法非常有用，可轻松生成 HTML &lt;&gt; 链接，并处理令人讨厌的详细信息，例如确保 URL 路径正确地进行 URL 编码。

Html.actionlink （）具有多个不同的重载，以允许为你的链接指定尽可能多的信息。 最简单的情况是，在客户端上单击超链接时，将只提供链接文本和操作方法。 例如，我们可以使用以下调用链接到存储详细信息页上的 "/Store/" 索引（）方法和链接文本 "中转到存储索引"：

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

*注意：在这种情况下，我们不需要指定控制器名称，因为我们只链接到呈现当前视图的同一控制器中的其他操作。*

但指向浏览页的链接将需要传递参数，因此，我们将使用采用三个参数的 Html.actionlink 方法的另一个重载：

- 1. 链接文本，将显示流派名称
- 2. 控制器操作名称（浏览）
- 3. 路由参数值，同时指定名称（流派）和值（流派名称）

将这些内容放在一起，下面介绍了如何将这些链接写入商店索引视图：

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

现在，当我们再次运行项目并访问/Store/URL 时，我们将看到一个流派列表。 每个流派均为超链接–单击此项时，将转到我们的/Store/Browse？流派 = *[流派]* URL。

![](mvc-music-store-part-3/_static/image3.jpg)

流派列表的 HTML 如下所示：

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-2.md)
> [下一页](mvc-music-store-part-4.md)
