---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和视图实现列表/详细信息 UI |Microsoft Docs
author: microsoft
description: 步骤4显示了如何将控制器添加到应用程序，该应用程序利用我们的模型为用户提供数据列表/详细信息导航体验 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486218"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>使用控制器和视图实现列表/详细信息 UI

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第4步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤4显示了如何将控制器添加到应用程序，该应用程序利用我们的模型为用户提供针对 NerdDinner 站点上的就的数据列表/详细信息导航体验。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-4-controllers-and-views"></a>NerdDinner 步骤4：控制器和视图

对于传统的 web 框架（经典 ASP、PHP、ASP.NET Web 窗体等），传入 Url 通常映射到磁盘上的文件。 例如： "/Products.aspx" 或 "/Products.php" 等 URL 请求可能由 "Products" 或 "Products" 文件处理。

基于 Web 的 MVC 框架以略有不同的方式将 Url 映射到服务器代码。 它们不会将传入 Url 映射到文件，而是将 Url 映射到类的方法。 这些类称为 "控制器"，它们负责处理传入的 HTTP 请求，处理用户输入，检索和保存数据，确定要发送回客户端的响应（显示 HTML、下载文件、重定向到其他URL，等等）。

现在，我们已经为 NerdDinner 应用程序构建了一个基本模型，接下来我们要将一个控制器添加到该应用程序，该应用程序利用它来向用户提供针对网站上的就的数据列表/详细信息导航体验。

### <a name="adding-a-dinnerscontroller-controller"></a>添加 DinnersController 控制器

首先，右键单击 web 项目中的 "控制器" 文件夹，然后选择 " **&gt;控制器**" 菜单命令（还可以通过键入 Ctrl-M、Ctrl-C 来执行此命令）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

这会显示 "添加控制器" 对话框：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

我们会将新控制器命名为 "DinnersController"，并单击 "添加" 按钮。 然后，Visual Studio 会在我们的 \Controllers 目录下添加 DinnersController.cs 文件：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

它还将在代码编辑器中打开新的 DinnersController 类。

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>向 DinnersController 类添加 Index （）和 Details （）操作方法

我们想要使用我们的应用程序启用访问者来浏览即将到来的就列表，并允许他们单击列表中的任何晚餐来查看有关它的特定详细信息。 我们将通过从应用程序发布以下 Url 来实现此目的：

| **URL** | **目的** |
| --- | --- |
| *就* | 显示即将发布的就的 HTML 列表 |
| */Dinners/Details/[id]* | 显示在 URL 中嵌入的 "id" 参数所指示的特定晚餐的详细信息-这将与数据库中晚餐的 DinnerID 匹配。 例如：/Dinners/Details/2 会显示一个 HTML 页面，其中包含有关其 DinnerID 值为2的晚餐的详细信息。 |

我们将通过将两个公共 "操作方法" 添加到 DinnersController 类（如下所示），发布这些 Url 的初始实现：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

接下来，我们将运行 NerdDinner 应用程序，并使用浏览器对其进行调用。 键入 *"/Dinners/"* URL 将导致*Index （）* 方法运行，并且该方法将返回以下响应：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

键入 *"/Dinners/Details/2"* URL 将导致*详细信息（）* 方法运行，并发送回以下响应：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

您可能想知道，ASP.NET MVC 如何知道如何创建 DinnersController 类并调用这些方法呢？ 若要了解如何使用路由，请快速了解路由的工作原理。

### <a name="understanding-aspnet-mvc-routing"></a>了解 ASP.NET MVC 路由

ASP.NET MVC 包含一个功能强大的 URL 路由引擎，该引擎在控制 Url 映射到控制器类的方式方面提供了很大的灵活性。 它允许我们完全自定义 ASP.NET MVC 选择要创建的控制器类的方式，对其调用哪个方法，并配置不同的方法来自动分析 URL/Querystring 中的变量，并将这些变量作为参数参数传递给方法。 它为 SEO （搜索引擎优化）提供完全优化站点的灵活性，并发布应用程序所需的任何 URL 结构。

默认情况下，新的 ASP.NET MVC 项目附带了已注册的一组预配置的 URL 路由规则。 这样，我们就可以轻松地开始使用应用程序，而无需显式配置任何内容。 可以在我们的项目的 "应用程序" 类中找到默认路由规则注册，可以通过在项目的根目录中双击 "global.asax" 文件来打开这些注册：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

默认的 ASP.NET MVC 路由规则在此类的 "RegisterRoutes" 方法中注册：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"路由。上面的 Maproute.html （） "方法调用使用 URL 格式注册将传入 Url 映射到控制器类的默认路由规则："/{controller}/{action}/{id} "–其中，" 控制器 "是要实例化的控制器类的名称，" action "是要对其调用的公共方法的名称，而" id "是嵌入在 URL 中的可选参数，可作为参数传递给方法。 传递给 "Maproute.html （）" 方法调用的第三个参数是在 URL （控制器 = "Home"、Action = "Index"、Id = ""）中不存在的情况下，用于控制器/操作/id 值的默认值集。

下面的表演示如何使用默认的 "<em>/{controllers}/{action}/{id}"</em>路由规则映射各种 url：

| **URL** | **控制器类** | **操作方法** | **传递的参数** |
| --- | --- | --- | --- |
| */Dinners/Details/2* | DinnersController | 详细信息（id） | id=2 |
| */Dinners/Edit/5* | DinnersController | 编辑（id） | id=5 |
| */Dinners/Create* | DinnersController | Create() | 不适用 |
| */Dinners* | DinnersController | Index （） | 不适用 |
| */Home* | HomeController | Index （） | 不适用 |
| */* | HomeController | Index （） | 不适用 |

最后三行显示使用的默认值（Controller = Home，Action = Index，Id = ""）。 由于已将 "Index" 方法注册为默认操作名称（如果未指定），因此 "/Dinners" 和 "/Home" Url 会使 Index （）操作方法在其控制器类上调用。 由于 "Home" 控制器注册为默认控制器（如果未指定），因此 "/" URL 将导致创建 HomeController，并对其调用 Index （）操作方法。

如果你不喜欢这些默认的 URL 路由规则，好消息就是可以轻松地更改-只需在上面的 RegisterRoutes 方法中编辑它们即可。 但对于我们的 NerdDinner 应用程序，我们不会更改任何默认的 URL 路由规则，而只是将其按原样使用。

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>使用我们的 DinnersController 中的 DinnerRepository

现在，我们将 DinnersController 的 Index （）和 Details （）操作方法的当前实现替换为使用我们的模型的实现。

我们将使用我们之前构建的 DinnerRepository 类来实现该行为。 首先，我们将添加一个引用 "NerdDinner" 命名空间的 "using" 语句，然后将 DinnerRepository 的实例声明为 DinnerController 类中的字段。

本章稍后将介绍 "依赖关系注入" 的概念，并为我们的控制器提供了另一种方法来获取对 DinnerRepository 的引用以实现更好的单元测试，但现在我们只需创建 DinnerRepository 的实例。与下面类似。

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

现在，我们已准备好使用检索到的数据模型对象生成 HTML 响应。

### <a name="using-views-with-our-controller"></a>通过控制器使用视图

尽管可以在操作方法中编写代码来汇编 HTML，然后使用*Response （）* helper 方法将其发送回客户端，但这种方法很快就会变得相当困难。 更好的方法是，仅在 DinnersController 操作方法中执行应用程序和数据逻辑，然后将呈现 HTML 响应所需的数据传递给单独的 "视图" 模板，该模板负责输出 HTML 表示形式的。 正如我们稍后将看到的，"视图" 模板是文本文件，通常包含 HTML 标记和嵌入的呈现代码的组合。

从视图呈现中分离我们的控制器逻辑带来了几大好处。 特别是，它有助于强制在应用程序代码和 UI 格式设置/呈现代码之间进行明确的 "问题分离"。 这样，就可以更轻松地将应用程序逻辑与 UI 呈现逻辑隔离。 这样就可以更轻松地修改 UI 呈现模板，而无需更改应用程序代码。 而且，开发人员和设计人员可以更轻松地协作项目。

我们可以更新 DinnersController 类，以便通过将两个操作方法的方法签名从 "void" 改为 "ActionResult" 的返回类型，来指示要使用视图模板来发送回 HTML UI 响应。 然后，可以对控制器基类调用*View （）* helper 方法，以返回如下所示的 "ViewResult" 对象：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

上面使用的*视图（）* 帮助器方法的签名如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

*View （）* helper 方法的第一个参数是要用于呈现 HTML 响应的视图模板文件的名称。 第二个参数是一个模型对象，其中包含视图模板呈现 HTML 响应所需的数据。

在索引（）操作方法中，我们将调用*View （）* helper 方法，并指示我们要使用 "索引" 视图模板呈现就的 HTML 列表。 我们正在向视图模板传递一系列晚餐对象，以生成以下列表：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

在我们的详细信息（）操作方法中，我们尝试使用 URL 内提供的 id 检索晚餐对象。 如果找到有效的晚餐，我们将调用*View （）* helper 方法，这表示我们想要使用 "详细信息" 视图模板来呈现检索到的晚餐对象。 如果请求的晚餐无效，我们将呈现一个有用的错误消息，指示不存在使用 "NotFound" 视图模板的晚餐（以及仅采用模板名称的*view （）* helper 方法的重载版本）：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

现在，让我们实现 "NotFound"、"Details" 和 "Index" 视图模板。

### <a name="implementing-the-notfound-view-template"></a>实现 "NotFound" 视图模板

首先，我们将实现 "NotFound" 视图模板，该模板会显示友好错误消息，指示找不到请求的晚餐。

我们将通过将文本光标置于控制器操作方法中来创建新的视图模板，然后右键单击并选择 "添加视图" 菜单命令（我们还可以通过键入 Ctrl-M、Ctrl + V）执行此命令：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

这会显示如下所示的 "添加视图" 对话框。 默认情况下，对话框将预先填充要创建的视图的名称，以匹配启动对话框时光标所在的操作方法的名称（在本例中为 "详细信息"）。 由于我们要首先实现 "NotFound" 模板，因此我们将覆盖此视图名称，并将其设置为 "NotFound"：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

当我们单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们创建一个新的 "NotFound" 视图模板（如果目录尚不存在，它也会创建）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

它还将在代码编辑器中打开新的 "NotFound" 视图模板：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

默认情况下，查看模板具有两个 "内容区域"，可以在其中添加内容和代码。 第一种是允许我们自定义发送回的 HTML 页面的 "标题"。 第二种是允许我们自定义发送回的 HTML 页面的 "主要内容"。

若要实现我们的 "NotFound" 视图模板，我们将添加一些基本内容：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

然后，可以在浏览器中进行尝试。 为此，请请求 *"/Dinners/Details/9999"* URL。 这将引用数据库中当前不存在的晚餐，并将导致我们的 DinnersController （）操作方法呈现我们的 "NotFound" 视图模板：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

在上面的屏幕截图中，你会注意到，我们的基本视图模板继承了一组围绕屏幕上的主要内容的 HTML。 这是因为，我们的视图模板使用 "母版页" 模板，使我们能够在网站上的所有视图中应用一致的布局。 我们将在本教程的后面部分讨论母版页的工作方式。

### <a name="implementing-the-details-view-template"></a>实现 "详细信息" 视图模板

现在，我们实现了 "详细信息" 查看模板，该模板将为单个晚宴型号生成 HTML。

为此，我们将文本游标定位到详细信息操作方法，然后右键单击并选择 "添加视图" 菜单命令（或按 Ctrl-M、Ctrl + V）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

此时将显示 "添加视图" 对话框。 我们将保留默认视图名称（"详细信息"）。 还将在对话框中选中 "创建强类型视图" 复选框，并选择（使用 combobox 下拉列表）要从控制器传递到视图的模型类型的名称。 在此视图中，我们将传递晚餐对象（该类型的完全限定名称为 "NerdDinner"）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

与上一个模板不同，我们选择创建一个 "空视图"，这次我们将选择使用 "详细信息" 模板自动 "基架" 视图。 为此，我们可以在上面的对话框中更改 "查看内容" 下拉标记。

"基架" 会根据传递给它的晚餐对象，生成详细信息视图模板的初始实现。 这为我们提供了一种简单的方法，让我们快速开始使用视图模板实现。

单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们创建新的 "Details .aspx" 视图模板文件：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

它还将在代码编辑器中打开新的 "Details .aspx" 视图模板。 它将包含基于晚宴型号的详细信息视图的初始基架实现。 基架引擎使用 .NET 反射来查看公开给该类的公共属性，并基于它找到的每个类型添加适当的内容：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

我们可以请求 *"/Dinners/Details/1"* URL 来查看此 "详细信息" 基架实现在浏览器中的外观。 使用此 URL 将显示我们在第一次创建数据库时手动添加到数据库中的就之一：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

这会使我们快速启动并运行，并提供我们的详细信息 .aspx 视图的初始实现。 接下来，我们可以对其进行调整，以自定义 UI 以实现满意。

当我们更密切地查看详细信息 .aspx 模板时，我们会发现它包含静态 HTML 和嵌入的呈现代码。 &lt;%%&gt; 代码片段在视图模板呈现时执行代码，&lt;% =%&gt; 代码片段执行其中包含的代码，然后将结果呈现给模板的输出流。

我们可以在视图中编写代码，以便访问使用强类型 "模型" 属性从控制器传入的 "晚餐" 模型对象。 当在编辑器中访问此 "模型" 属性时，Visual Studio 将为我们提供完整的代码-intellisense：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

让我们进行一些调整，以便最终详细信息视图模板的源如下所示：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

当我们再次访问 *"/Dinners/Details/1"* URL 时，它现在将如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>实现 "索引" 视图模板

现在，我们实现 "索引" 视图模板，该模板将生成即将发布的就的列表。 为此，我们将文本光标置于 Index 操作方法中，然后右键单击并选择 "添加视图" 菜单命令（或按 Ctrl-M、Ctrl + V）。

在 "添加视图" 对话框中，我们将保留名为 "Index" 的视图模板，并选中 "创建强类型视图" 复选框。 这一次，我们将选择自动生成 "列表" 视图模板，并选择 "NerdDinner" 作为传递到该视图的模型类型（这是因为我们指出我们要创建 "List" 基架，这将导致 "添加视图" 对话框假设我们将晚餐对象序列从控制器传递到视图）：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

单击 "添加" 按钮时，Visual Studio 将在 "\Views\Dinners" 目录中为我们创建一个新的 "Index .aspx" 视图模板文件。 它将 "基架" 其中的初始实现，该实现提供传递到视图的就的 HTML 表列表。

当我们运行应用程序并访问 *"/Dinners/"* URL 时，它会呈现就的列表，如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

上面的表解决方案为我们的晚餐数据提供了类似于网格的布局，而这并不是我们想要的面向消费者的晚餐列表。 我们可以更新 node.js 视图模板，并对其进行修改，以列出更少的数据列，并使用 &lt;ul&gt; 元素，使用下面的代码呈现这些数据，而不是使用表：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

我们将在上述 foreach 语句中使用 "var" 关键字，因为我们循环遍历模型中的每个晚餐。 不熟悉C# 3.0 的人员可能会认为，使用 "var" 意味着晚餐对象已后期绑定。 相反，它意味着编译器对强类型 "Model" 属性（其类型为 "IEnumerable&lt;晚宴&gt;"）使用类型推理，并将本地 "晚餐" 变量编译为晚餐类型，这意味着我们将在代码块中获取完整的 intellisense 和编译时检查：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

当我们在浏览器中的 */Dinners* URL 上进行刷新时，更新视图现在如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

这看起来很好，但目前还没有。 最后一步是让最终用户在列表中单击各个就，并查看其详细信息。 我们将通过呈现链接到 DinnersController 上的详细信息操作方法的 HTML hyperlink 元素来实现此操作。

可以通过以下两种方式之一在索引视图中生成这些超链接。 第一种方式是手动创建 HTML &lt;如下所示的&gt; 元素，在该元素中，我们将 &lt;%%&gt; 块嵌入到 &lt;的 HTML 元素中：&gt;

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

可使用的替代方法是利用 ASP.NET MVC 中的内置 "Html.actionlink （）" 帮助器方法，该方法支持以编程方式创建 HTML &lt;一个链接到控制器上其他操作方法的&gt; 元素：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html 的第一个参数。 Html.actionlink （）帮助程序方法是要显示的链接文本（在本例中为晚餐的标题），第二个参数是我们要生成链接的控制器操作名称（在本例中为详细信息方法），第三个参数是要发送到操作的一组参数（实现为具有属性名称/值的匿名类型）。 在这种情况下，我们将指定要链接到的晚餐的 "id" 参数，并因为 ASP.NET MVC 中的默认 URL 路由规则是 "{Controller}/{Action}/{id}"，则 Html.actionlink （） helper 方法将生成以下输出：

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

对于我们的索引 .aspx 视图，我们将使用 Html.actionlink （） helper 方法方法，并将列表中的每个晚宴链接到相应的详细信息 URL：

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

现在，当我们点击 */Dinners* URL 时，晚餐列表如下所示：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

当我们单击列表中的任何就时，我们将导航以查看其详细信息：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>基于约定的命名和 \Views 目录结构

ASP.NET MVC 应用程序默认情况下，在解析视图模板时使用基于约定的目录命名结构。 这允许开发人员在从控制器类内引用视图时避免必须完全限定位置路径。 默认情况下，ASP.NET MVC 将在应用程序下的 * \Views\[ControllerName]\* 目录中查找视图模板文件。

例如，我们一直在处理 DinnersController 类，该类显式引用三个视图模板： "Index"、"Details" 和 "NotFound"。 ASP.NET MVC 默认情况下会在应用程序根目录下的 *\Views\Dinners*目录中查找这些视图：

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

请注意，项目中当前有三个控制器类（DinnersController、HomeController 和 AccountController），默认情况下，在创建项目时添加了最后两个控制器类，其中有三个子目录（每个目录一个控制器）的 \Views。

从 Home 和 Accounts 控制器引用的视图将自动从各自的 *\Views\Home*和 *\Views\Account*目录解析其视图模板。 *\Views\Shared*子目录提供一种方式来存储在应用程序内跨多个控制器重复使用的视图模板。 当 ASP.NET MVC 尝试解析视图模板时，它将首先检查 *\Views\[控制器]* 特定的目录，如果找不到该视图模板，它将在 *\Views\Shared*目录中查找。

命名单独的视图模板时，建议的指导原则是将视图模板与导致其呈现的操作方法共享相同的名称。 例如，在我们的 "索引" 操作方法之上，使用 "索引" 视图呈现视图结果，并且 "详细信息" 操作方法使用 "详细信息" 视图呈现其结果。 这样就可以轻松地快速查看与每个操作关联的模板。

当视图模板与在控制器上调用的操作方法同名时，开发人员无需显式指定视图模板名称。 只需将 model 对象传递到 "View （）" 帮助器方法（无需指定视图名称），ASP.NET MVC 就会自动推断要使用 *\Views\[ControllerName]\[ActionName]* 查看要呈现的模板。

这样一来，我们就可以清理控制器代码，避免在代码中重复两次：

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

以上代码是为站点实现良好的晚餐列表/详细信息所需的所有内容。

#### <a name="next-step"></a>下一步

我们现在已生成了一个良好的晚餐浏览体验。

现在，让我们启用 CRUD （创建、读取、更新、删除）数据窗体编辑支持。

> [!div class="step-by-step"]
> [上一页](build-a-model-with-business-rule-validations.md)
> [下一页](provide-crud-create-read-update-delete-data-form-entry-support.md)
