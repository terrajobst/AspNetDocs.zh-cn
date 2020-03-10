---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用 ViewData 和实现 ViewModel 类 |Microsoft Docs
author: microsoft
description: 步骤6显示了如何启用对更丰富的窗体编辑方案的支持，并讨论了可用于将数据从控制器传递到视图的两种方法： 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435530"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>使用 ViewData 和实现 ViewModel 类

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第6步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤6显示了如何启用对更丰富的窗体编辑方案的支持，并讨论了可用于将数据从控制器传递到视图的两种方法： ViewData 和 ViewModel。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>NerdDinner 步骤6： ViewData 和 ViewModel

我们介绍了大量的窗体发布方案，并讨论了如何实现创建、更新和删除（CRUD）支持。 现在我们将进一步 DinnersController 实现，并支持更丰富的窗体编辑方案。 在此过程中，我们将讨论可用于将数据从控制器传递到视图的两种方法： ViewData 和 ViewModel。

### <a name="passing-data-from-controllers-to-view-templates"></a>将数据从控制器传递到视图-模板

MVC 模式的一项定义特征是严格的 "问题分离"，它有助于在应用程序的不同组件之间强制实施。 每个模型、控制器和视图都具有完善定义的角色和职责，它们彼此之间以定义的方式相互通信。 这有助于提高可测试性和代码重用。

当控制器类决定向客户端呈现 HTML 响应时，它负责将呈现响应所需的所有数据显式传递给视图模板。 视图模板不应执行任何数据检索或应用程序逻辑，而应将其限制为仅包含由控制器传递给它的模型/数据驱动的呈现代码。

现在，我们的 DinnersController 类传递到我们的视图模板的模型数据简单直接明了，其中显示了索引（）的晚餐对象的列表，并在出现详细信息（）、编辑（）、Create （）和 Delete （）的情况下使用了一个晚餐对象。 随着我们向应用程序中添加更多的 UI 功能，我们通常需要只传递此数据以在视图模板中呈现 HTML 响应。 例如，我们可能需要更改编辑中的 "国家/地区" 字段，并创建 dropdownlist 为 HTML 文本框的视图。 我们可能想要从我们动态填充的支持国家/地区列表中生成，而不是硬编码查看模板中的国家/地区名称列表。 我们需要一种方法，将晚餐对象*和*支持的国家/地区列表从我们的控制器传递到我们的视图模板。

让我们看看可以实现此目的的两种方法。

### <a name="using-the-viewdata-dictionary"></a>使用 ViewData 字典

控制器基类公开了 "ViewData" 字典属性，该属性可用于将其他数据项从控制器传递到视图。

例如，若要支持我们想要将编辑视图中的 "国家/地区" 文本框从 HTML 文本框更改为 dropdownlist 的方案，我们可以更新 Edit （）操作方法以传递（除了晚餐对象） SelectList 对象，该对象可用作 mdropdownlist 的模型。

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

上述 SelectList 的构造函数将接受用来填充 downlist 的县列表，以及当前选定的值。

然后，我们可以更新我们的 "Edit .aspx" 视图模板，以使用我们之前使用的 Html. TextBox （） helper 方法，而不是使用的 Html. TextBox （） helper 方法。

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

上面的 DropDownList （） helper 方法使用两个参数。 第一个是要输出的 HTML form 元素的名称。 第二个是通过 ViewData 字典传递的 "SelectList" 模型。 我们使用C# "as" 关键字将字典中的类型转换为 SelectList。

现在，当我们运行应用程序并在浏览器中访问 */Dinners/Edit/1* URL 时，我们将看到编辑 UI 已更新，以显示 dropdownlist 的国家/地区，而不是文本框：

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

由于我们还会从 HTTP-POST 编辑方法呈现编辑视图模板（在发生错误的情况下），因此我们将需要确保在错误情况下呈现视图模板时，我们还将更新此方法以将 SelectList 添加到 ViewData 中：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

现在我们的 DinnersController 编辑方案支持 DropDownList。

### <a name="using-a-viewmodel-pattern"></a>使用 ViewModel 模式

ViewData 字典方法的好处是，实现起来非常快捷快捷。 不过，某些开发人员不喜欢使用基于字符串的字典，因为键入错误会导致编译时不会捕获到错误。 使用强类型化语言（如C#在视图模板中）时，非类型化的 ViewData 字典还需要使用 "as" 运算符或强制转换。

我们可以使用的另一种方法是 "ViewModel" 模式。 使用此模式时，我们将创建针对特定视图方案进行了优化的强类型类，并公开了视图模板所需的动态值/内容的属性。 然后，控制器类可以填充这些视图优化类并将其传递给视图模板以供使用。 这会在视图模板中启用类型安全、编译时检查和编辑器 intellisense。

例如，若要启用晚餐窗体编辑方案，我们可以创建一个如下所示的 "DinnerFormViewModel" 类，该类公开两个强类型的属性：晚餐对象和填充国家 dropdownlist 所需的 SelectList 模型：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

然后，可以使用我们从存储库中检索到的晚餐对象，更新 Edit （）操作方法来创建 DinnerFormViewModel，然后将其传递到我们的视图模板：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

接下来，我们将更新视图模板，使其需要一个 "DinnerFormViewModel" 而不是 "晚餐" 对象，方法是更改 "编辑 .aspx" 页顶部的 "继承" 属性，如下所示：

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

完成此操作后，我们的视图模板中的 "模型" 属性的 intellisense 将会更新，以反映我们传递它的 DinnerFormViewModel 类型的对象模型：

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

然后，我们可以更新我们的视图代码来处理它。 请注意，我们不会更改我们正在创建的输入元素的名称（窗体元素仍将命名为 "Title"、"国家/地区"），但我们正在更新 HTML 帮助器方法以使用 DinnerFormViewModel 类检索值：

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

在呈现错误时，我们还将更新编辑 post 方法以使用 DinnerFormViewModel 类：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

我们还可以更新 Create （）操作方法，以便重复使用完全相同的*DinnerFormViewModel*类，以便在这些国家/地区中 DropDownList。 下面是 HTTP GET 实现：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

下面是 HTTP POST Create 方法的实现：

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

同时，我们的 "编辑" 和 "创建" 屏幕支持用于挑选国家/地区的下拉 downlists。

### <a name="custom-shaped-viewmodel-classes"></a>自定义形状的 ViewModel 类

在上述方案中，我们的 DinnerFormViewModel 类直接将晚餐模型对象公开为属性，同时将支持 SelectList 模型属性公开。 如果我们要在视图模板中创建的 HTML UI 相对接近我们的域模型对象，则此方法适用于这种情况。

对于这种情况不是这样的情况，可以使用的一种方法是创建一个自定义形状的 ViewModel 类，该类的对象模型对视图的使用进行了更多的优化，并可能与基础域模型对象完全不同。 例如，它可能会公开从多个模型对象中收集的不同属性名称和/或聚合属性。

自定义形状的 ViewModel 类可用于将数据从控制器传递到要呈现的视图，以及帮助处理回发到控制器操作方法的窗体数据。 对于此后一种情况，您可能让操作方法使用窗体发布数据更新 ViewModel 对象，然后使用 ViewModel 实例映射或检索实际的域模型对象。

自定义形状的 ViewModel 类可以提供很大的灵活性，并且可以在任何时候在视图模板内查找呈现代码，或在操作方法内的窗体发布代码太复杂时进行调查。 这通常是因为您的域模型并不完全对应于您所生成的 UI，并且中间的自定义形状的 ViewModel 类可以帮助。

### <a name="next-step"></a>下一步

现在我们来看看如何使用分区和母版页跨应用程序重复使用和共享 UI。

> [!div class="step-by-step"]
> [上一页](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一页](re-use-ui-using-master-pages-and-partials.md)
