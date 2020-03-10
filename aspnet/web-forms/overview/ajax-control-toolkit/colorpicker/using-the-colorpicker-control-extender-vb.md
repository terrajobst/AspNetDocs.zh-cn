---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: 使用 ColorPicker 控件扩展程序（VB） |Microsoft Docs
author: microsoft
description: ColorPicker 是一个 ASP.NET AJAX 扩展器，它在 popup 控件中提供 UI 的客户端颜色选取功能。 它可以附加到任何 ASP.NET 。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 77e2e3bc61a5e1498570959ca40acff83dc3fc82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446582"
---
# <a name="using-the-colorpicker-control-extender-vb"></a>使用 ColorPicker 控件扩展程序（VB）

由[Microsoft](https://github.com/microsoft)

> ColorPicker 是一个 ASP.NET AJAX 扩展器，它在 popup 控件中提供 UI 的客户端颜色选取功能。 它可以附加到任何 ASP.NET TextBox 控件。 以便.

本教程的目的是说明如何使用 AJAX 控件工具包 ColorPicker 控件扩展器。 ColorPicker 控件扩展器会显示一个弹出对话框，通过该对话框可以选择颜色。 当你希望为用户提供直观的用户界面来选取颜色时，ColorPicker 非常有用。

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>使用 ColorPicker 控件扩展器扩展 TextBox 控件

例如，假设您要创建一个网站，使访问者能够创建自定义的名片。 访问者可以输入名片的文本并选择颜色。 列表1中的 ASP.NET 页包含两个名为 txtCardText 和 txtCardColor 的 TextBox 控件。 提交窗体时，将显示所选的值（请参阅图1）。

[用于创建名片 ![简单窗体](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**图 01**：创建名片的简单窗体（[单击以查看完全尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image2.png)）

**列表 1-CreateCard .aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

列表1中的窗体是可行的，但它并不能提供出色的用户体验。 用户必须在文本框中键入一种颜色。 如果用户需要专用颜色（例如，pea 绿色的右阴影），则用户必须在不提供任何帮助的情况下确定 HTML 颜色代码。

可以使用 ColorPicker 控件扩展器来创建更好的用户体验。 将焦点移到 TextBox 控件时，ColorPicker 会显示颜色对话框（请参阅图2）。

[![ColorPicker 控件扩展器](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**图 02**： ColorPicker 控件扩展器（[单击以查看完全大小的图像](using-the-colorpicker-control-extender-vb/_static/image4.png)）

需要完成两个步骤才能将 ColorPicker 控件扩展器与列表1中的窗体一起使用：

1. 将 ScriptManager 控件添加到页面
2. 将 ColorPicker 控件扩展程序添加到页面

必须先将 ScriptManager 添加到页面，然后才能使用 ColorPicker。 要添加 ScriptManager 的好地方是在打开的服务器端 &lt;窗体&gt; 标记的右边。 可以将 ScriptManager 从工具箱拖到页面上（ScriptManager 位于 "AJAX 扩展" 选项卡下）。 或者，可以在 "打开服务器端窗体" 标记下的 "源" 视图中键入以下标记：

&lt;asp： ScriptManager ID = "ScriptManager1" runat = "server"/&gt;

将 ColorPicker 控件扩展程序添加到页面的最简单方法是在 "设计" 视图中。 如果将鼠标悬停在 "txtCardColor" 文本框上，则会出现一个智能任务选项，使你能够添加扩展器（请参阅图3）。 如果选择此选项，则会出现扩展器向导（见图4）。

[添加扩展器 ![](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**图 03**：添加扩展器（[单击以查看完全大小的映像](using-the-colorpicker-control-extender-vb/_static/image6.png)）

[![使用扩展器向导选择控件扩展器](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**图 04**：使用扩展器向导选择控件扩展器（[单击查看完全大小的映像](using-the-colorpicker-control-extender-vb/_static/image8.png)）

可以选取 ColorPicker 扩展器，通过 ColorPicker 扩展器来扩展 txtCardColor TextBox。 单击“确定”，关闭对话框。

进行这些更改后，页面的源如下所示。

**列表 2-CreateCard （带有 ColorPicker）**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

请注意，该页现在包含 ColorPickerExtender 控件，该控件直接出现在 txtCardColor TextBox 控件的下方。 ColorPickerExtender 控件扩展了 txtCardColor 控件，使其显示颜色选取器对话框。

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>使用按钮启动 "颜色选取器" 对话框

ColorPicker 扩展器支持以下属性：

- PopupButtonId-页面上导致颜色选取器对话框出现的按钮的 ID。
- PopupPosition-颜色选取器对话框的相对于目标控件的位置。 可能的值为绝对、居中、BottomLeft、BottomRight、TopLeft、右上、Right 和 Left （默认值为 BottomLeft）。
- SampleControlId-显示选定颜色的控件的 ID。
- SelectedColor-ColorPicker 所选择的初始颜色。

您可以使用这些属性自定义颜色选取器对话框的显示方式以及所选颜色的显示方式。 列表3中的页说明了如何使用这些属性中的几个。

**列表 3-CreateCardButton**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

列表3中的页包含 "选取颜色" 按钮（见图5）。 单击此按钮时，"颜色选取器" 对话框将显示在文本框上方。 如果从对话框中选择一种颜色，则所选颜色将显示为 lblSample 标签控件的背景色。

ColorPicker PopupButtonID 属性用于将拾色按钮与 ColorPicker 扩展器相关联。 为 PopupButtonID 属性提供值时，当目标控件具有焦点时，将不再显示 "颜色选取器" 对话框。 您必须单击该按钮以显示对话框。

SampleControlID 属性用于将显示选定颜色的控件与 ColorPicker 相关联。 ColorPicker 将该控件的背景色更改为当前选定的颜色。

[使用按钮显示 "颜色选取器" 对话框 ![](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**图 05**：使用按钮显示 "颜色选取器" 对话框（[单击查看完全尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image10.png)）

## <a name="summary"></a>摘要

在本教程中，已学习如何使用 ColorPicker 控件扩展器来显示弹出项颜色选取器对话框。 首先，我们介绍了如何在焦点移至 TextBox 控件时显示该对话框。 接下来，您学习了如何创建一个按钮，以便在单击按钮时显示颜色选取器对话框。

> [!div class="step-by-step"]
> [上一页](using-the-colorpicker-control-extender-cs.md)
