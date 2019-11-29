---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: 创建自定义 HTML 帮助程序（VB） |Microsoft Docs
author: microsoft
description: 本教程的目的是演示如何创建可在 MVC 视图中使用的自定义 HTML 帮助程序。 利用 HTML 帮助器 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: aaeadde258a2855343a5bfb1e5ee76000e04f6bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593832"
---
# <a name="creating-custom-html-helpers-vb"></a>创建自定义 HTML 帮助程序 (VB)

由[Microsoft](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> 本教程的目的是演示如何创建可在 MVC 视图中使用的自定义 HTML 帮助程序。 利用 HTML 帮助器，你可以减少创建标准 HTML 页面所必须执行的 HTML 标记的单调乏味类型。

本教程的目的是演示如何创建可在 MVC 视图中使用的自定义 HTML 帮助程序。 利用 HTML 帮助器，你可以减少创建标准 HTML 页面所必须执行的 HTML 标记的单调乏味类型。

在本教程的第一部分中，我介绍了 ASP.NET MVC 框架附带的一些现有 HTML 帮助器。 接下来，我将介绍两种创建自定义 HTML 帮助器的方法：我介绍了如何通过创建共享方法并创建扩展方法来创建自定义 HTML 帮助程序。

## <a name="understanding-html-helpers"></a>了解 HTML 帮助器

HTML 帮助程序只是返回字符串的方法。 字符串可以表示所需的任何类型的内容。 例如，可以使用 HTML 帮助器来呈现标准 HTML 标记，如 HTML `<input>` 和 `<img>` 标记。 你还可以使用 HTML 帮助器来呈现更复杂的内容，例如选项卡条或 HTML 表数据库数据。

ASP.NET MVC 框架包含以下一组标准 HTML 帮助程序（这不是完整的列表）：

- Html.actionlink （）
- Html.beginform （）
- Html. CheckBox （）
- DropDownList （）
- EndForm （）
- .Html （隐藏）（）
- Html. ListBox （）
- .Html. Password （）
- .Html （）
- .Html （）
- .Html （）

例如，请考虑列表1中的窗体。 此窗体通过两个标准 HTML 帮助器的帮助进行呈现（参见图1）。 此窗体使用 `Html.BeginForm()` 和 `Html.TextBox()` 帮助器方法。

[用 HTML 帮助器呈现的 ![页面](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)

**图 01**：用 HTML 帮助器呈现的页面（[单击查看完全尺寸的图像](creating-custom-html-helpers-vb/_static/image3.png)）

**列表1– `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

`Html.BeginForm()` Helper 方法用于创建打开和关闭 HTML `<form>` 标记。 请注意，`Html.BeginForm()` 方法是在 using 语句中调用的。 Using 语句可确保在使用块的末尾关闭 `<form>` 标记。

如果你愿意，可以调用 EndForm （） Helper 方法来关闭 `<form>` 标记，而不是创建 using 块。 使用任何一种方法来创建与您最直观的开始和结束 `<form>` 标记。

`Html.TextBox()` 帮助器方法在列表1中用于呈现 HTML `<input>` 标记。 如果在浏览器中选择 "查看源"，则会看到列表2中的 HTML 源。 请注意，源包含标准 HTML 标记。

> [!IMPORTANT]
> 请注意，`Html.TextBox()`HTML 帮助器是用 `<%= %>` 标记而不是 `<% %>` 标记呈现的。 如果不包含等号，则不会在浏览器中呈现任何内容。

ASP.NET MVC 框架包含一小部分帮助程序。 大多数情况下，你将需要通过自定义 HTML 帮助器来扩展 MVC 框架。 在本教程的其余部分中，您将学习创建自定义 HTML 帮助程序的两种方法。

**列表2– `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a>用共享方法创建 HTML 帮助器

创建新的 HTML 帮助器的最简单方法是创建一个返回字符串的共享方法。 例如，假设您决定创建一个呈现 HTML `<label>` 标记的新 HTML 帮助器。 您可以使用清单2中的类呈现 `<label>`。

**列表2– `Helpers\LabelHelper.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

对于清单2中的类没有什么特别之处。 `Label()` 方法只返回一个字符串。

列表3中修改的索引视图使用 `LabelHelper` 来呈现 HTML `<label>` 标记。 请注意，此视图包含导入 Application1 命名空间的 `<%@ imports %>` 指令。

**列表2– `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>创建具有扩展方法的 HTML 帮助器

如果要创建与 ASP.NET MVC 框架中包含的标准 HTML 帮助器相同的 HTML 帮助器，则需要创建扩展方法。 扩展方法使你能够向现有类添加新方法。 创建 HTML 帮助器方法时，可以向视图的 Html 属性所表示的 `HtmlHelper` 类添加新方法。

清单3中的 Visual Basic 模块向 `HtmlHelper` 类添加了一个名为 `Label()` 的扩展方法。 有关此模块，需要注意几个事项。 首先，请注意，模块是用 `<Extension()>` 特性修饰的。 若要使用此特性，必须导入 `System.Runtime.CompilerServices` 命名空间

其次，请注意，`Label()` 方法的第一个参数表示 `HtmlHelper` 类。 扩展方法的第一个参数指示扩展方法扩展的类。

**列表 3-`Helpers\LabelExtensions.vb`**

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

创建扩展方法并成功生成应用程序后，扩展方法将出现在 Visual Studio Intellisense 中，如类的所有其他方法（请参阅图2）。 唯一的区别在于，扩展方法旁边会出现一个特殊符号（向下箭头图标）。

[使用 Html. Label （）扩展方法 ![](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)

**图 02**：使用 Html. Label （）扩展方法（[单击以查看完全大小的图像](creating-custom-html-helpers-vb/_static/image6.png)）

列表4中修改的索引视图使用 Html. Label （）扩展方法来呈现其所有 &lt;标签&gt; 标记。

**列表 4-`Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a>总结

本教程介绍了创建自定义 HTML 帮助程序的两种方法。 首先，你已了解如何创建一个可返回字符串的共享方法来创建自定义 `Label()` HTML 帮助器。 接下来，你已了解如何通过在 `HtmlHelper` 类上创建扩展方法来创建自定义 `Label()` HTML 帮助器方法。

在本教程中，我将重点介绍如何构建一个极其简单的 HTML 帮助器方法。 请注意，HTML 帮助程序可能会非常复杂。 您可以生成 HTML 帮助器来呈现丰富的内容，如树视图、菜单或数据库数据的表。

> [!div class="step-by-step"]
> [上一页](asp-net-mvc-views-overview-vb.md)
> [下一页](using-the-tagbuilder-class-to-build-html-helpers-vb.md)
