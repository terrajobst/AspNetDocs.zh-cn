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
# <a name="using-the-colorpicker-control-extender-vb"></a><span data-ttu-id="fedbd-104">使用 ColorPicker 控件扩展程序（VB）</span><span class="sxs-lookup"><span data-stu-id="fedbd-104">Using the ColorPicker Control Extender (VB)</span></span>

<span data-ttu-id="fedbd-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="fedbd-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="fedbd-106">ColorPicker 是一个 ASP.NET AJAX 扩展器，它在 popup 控件中提供 UI 的客户端颜色选取功能。</span><span class="sxs-lookup"><span data-stu-id="fedbd-106">ColorPicker is an ASP.NET AJAX extender that provides client-side color-picking functionality with UI in a popup control.</span></span> <span data-ttu-id="fedbd-107">它可以附加到任何 ASP.NET TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="fedbd-107">It can be attached to any ASP.NET TextBox control.</span></span> <span data-ttu-id="fedbd-108">以便.</span><span class="sxs-lookup"><span data-stu-id="fedbd-108">It.</span></span>

<span data-ttu-id="fedbd-109">本教程的目的是说明如何使用 AJAX 控件工具包 ColorPicker 控件扩展器。</span><span class="sxs-lookup"><span data-stu-id="fedbd-109">The goal of this tutorial is to explain how you can use the AJAX Control Toolkit ColorPicker control extender.</span></span> <span data-ttu-id="fedbd-110">ColorPicker 控件扩展器会显示一个弹出对话框，通过该对话框可以选择颜色。</span><span class="sxs-lookup"><span data-stu-id="fedbd-110">The ColorPicker control extender displays a popup dialog that enables you to select a color.</span></span> <span data-ttu-id="fedbd-111">当你希望为用户提供直观的用户界面来选取颜色时，ColorPicker 非常有用。</span><span class="sxs-lookup"><span data-stu-id="fedbd-111">The ColorPicker is useful whenever you want to provide an intuitive user interface for a user to pick a color.</span></span>

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a><span data-ttu-id="fedbd-112">使用 ColorPicker 控件扩展器扩展 TextBox 控件</span><span class="sxs-lookup"><span data-stu-id="fedbd-112">Extending a TextBox Control with the ColorPicker Control Extender</span></span>

<span data-ttu-id="fedbd-113">例如，假设您要创建一个网站，使访问者能够创建自定义的名片。</span><span class="sxs-lookup"><span data-stu-id="fedbd-113">Imagine, for example, that you want to create a website that enables visitors to create customized business cards.</span></span> <span data-ttu-id="fedbd-114">访问者可以输入名片的文本并选择颜色。</span><span class="sxs-lookup"><span data-stu-id="fedbd-114">Visitors can enter the text for a business card and pick the color.</span></span> <span data-ttu-id="fedbd-115">列表1中的 ASP.NET 页包含两个名为 txtCardText 和 txtCardColor 的 TextBox 控件。</span><span class="sxs-lookup"><span data-stu-id="fedbd-115">The ASP.NET page in Listing 1 contains two TextBox controls named txtCardText and txtCardColor.</span></span> <span data-ttu-id="fedbd-116">提交窗体时，将显示所选的值（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="fedbd-116">When you submit the form, the selected values are displayed (see Figure 1).</span></span>

<span data-ttu-id="fedbd-117">[用于创建名片 ![简单窗体](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="fedbd-117">[![Simple form for creating a business card](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)</span></span>

<span data-ttu-id="fedbd-118">**图 01**：创建名片的简单窗体（[单击以查看完全尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="fedbd-118">**Figure 01**: Simple form for creating a business card ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image2.png))</span></span>

<span data-ttu-id="fedbd-119">**列表 1-CreateCard .aspx**</span><span class="sxs-lookup"><span data-stu-id="fedbd-119">**Listing 1 - CreateCard.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

<span data-ttu-id="fedbd-120">列表1中的窗体是可行的，但它并不能提供出色的用户体验。</span><span class="sxs-lookup"><span data-stu-id="fedbd-120">The form in Listing 1 works, but it does not provide a great user experience.</span></span> <span data-ttu-id="fedbd-121">用户必须在文本框中键入一种颜色。</span><span class="sxs-lookup"><span data-stu-id="fedbd-121">The user has to type a color into the textbox.</span></span> <span data-ttu-id="fedbd-122">如果用户需要专用颜色（例如，pea 绿色的右阴影），则用户必须在不提供任何帮助的情况下确定 HTML 颜色代码。</span><span class="sxs-lookup"><span data-stu-id="fedbd-122">If the user wants a specialized color - for example, just the right shade of pea green - then the user must figure out the HTML color code without any help.</span></span>

<span data-ttu-id="fedbd-123">可以使用 ColorPicker 控件扩展器来创建更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="fedbd-123">You can use the ColorPicker control extender to create a better user experience.</span></span> <span data-ttu-id="fedbd-124">将焦点移到 TextBox 控件时，ColorPicker 会显示颜色对话框（请参阅图2）。</span><span class="sxs-lookup"><span data-stu-id="fedbd-124">The ColorPicker displays a color dialog when you move focus to a TextBox control (see Figure 2).</span></span>

<span data-ttu-id="fedbd-125">[![ColorPicker 控件扩展器](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="fedbd-125">[![The ColorPicker Control Extender](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)</span></span>

<span data-ttu-id="fedbd-126">**图 02**： ColorPicker 控件扩展器（[单击以查看完全大小的图像](using-the-colorpicker-control-extender-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="fedbd-126">**Figure 02**: The ColorPicker Control Extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image4.png))</span></span>

<span data-ttu-id="fedbd-127">需要完成两个步骤才能将 ColorPicker 控件扩展器与列表1中的窗体一起使用：</span><span class="sxs-lookup"><span data-stu-id="fedbd-127">You need to complete two steps to use the ColorPicker control extender with the form in Listing 1:</span></span>

1. <span data-ttu-id="fedbd-128">将 ScriptManager 控件添加到页面</span><span class="sxs-lookup"><span data-stu-id="fedbd-128">Add a ScriptManager control to the page</span></span>
2. <span data-ttu-id="fedbd-129">将 ColorPicker 控件扩展程序添加到页面</span><span class="sxs-lookup"><span data-stu-id="fedbd-129">Add the ColorPicker control extender to the page</span></span>

<span data-ttu-id="fedbd-130">必须先将 ScriptManager 添加到页面，然后才能使用 ColorPicker。</span><span class="sxs-lookup"><span data-stu-id="fedbd-130">Before you can use the ColorPicker, you must add a ScriptManager to your page.</span></span> <span data-ttu-id="fedbd-131">要添加 ScriptManager 的好地方是在打开的服务器端 &lt;窗体&gt; 标记的右边。</span><span class="sxs-lookup"><span data-stu-id="fedbd-131">A good place to add the ScriptManager is right below the opening server-side &lt;form&gt; tag.</span></span> <span data-ttu-id="fedbd-132">可以将 ScriptManager 从工具箱拖到页面上（ScriptManager 位于 "AJAX 扩展" 选项卡下）。</span><span class="sxs-lookup"><span data-stu-id="fedbd-132">You can drag the ScriptManager onto the page from the toolbox (the ScriptManager is located under the AJAX Extensions tab).</span></span> <span data-ttu-id="fedbd-133">或者，可以在 "打开服务器端窗体" 标记下的 "源" 视图中键入以下标记：</span><span class="sxs-lookup"><span data-stu-id="fedbd-133">Alternatively, you can type the following tag into Source View beneath the opening server-side form tag:</span></span>

<span data-ttu-id="fedbd-134">&lt;asp： ScriptManager ID = "ScriptManager1" runat = "server"/&gt;</span><span class="sxs-lookup"><span data-stu-id="fedbd-134">&lt;asp:ScriptManager ID="ScriptManager1" runat="server" /&gt;</span></span>

<span data-ttu-id="fedbd-135">将 ColorPicker 控件扩展程序添加到页面的最简单方法是在 "设计" 视图中。</span><span class="sxs-lookup"><span data-stu-id="fedbd-135">The easiest way to add the ColorPicker control extender to the page is in Design View.</span></span> <span data-ttu-id="fedbd-136">如果将鼠标悬停在 "txtCardColor" 文本框上，则会出现一个智能任务选项，使你能够添加扩展器（请参阅图3）。</span><span class="sxs-lookup"><span data-stu-id="fedbd-136">If you hover your mouse over the txtCardColor TextBox, a smart task option appears the enables you to add an extender (see Figure 3).</span></span> <span data-ttu-id="fedbd-137">如果选择此选项，则会出现扩展器向导（见图4）。</span><span class="sxs-lookup"><span data-stu-id="fedbd-137">If you pick this option, the Extender Wizard appears (see Figure 4).</span></span>

<span data-ttu-id="fedbd-138">[添加扩展器 ![](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="fedbd-138">[![Adding an extender](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)</span></span>

<span data-ttu-id="fedbd-139">**图 03**：添加扩展器（[单击以查看完全大小的映像](using-the-colorpicker-control-extender-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="fedbd-139">**Figure 03**: Adding an extender ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image6.png))</span></span>

<span data-ttu-id="fedbd-140">[![使用扩展器向导选择控件扩展器](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="fedbd-140">[![Selecting a control extender with the Extender Wizard](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)</span></span>

<span data-ttu-id="fedbd-141">**图 04**：使用扩展器向导选择控件扩展器（[单击查看完全大小的映像](using-the-colorpicker-control-extender-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="fedbd-141">**Figure 04**: Selecting a control extender with the Extender Wizard ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image8.png))</span></span>

<span data-ttu-id="fedbd-142">可以选取 ColorPicker 扩展器，通过 ColorPicker 扩展器来扩展 txtCardColor TextBox。</span><span class="sxs-lookup"><span data-stu-id="fedbd-142">You can pick the ColorPicker extender to extend the txtCardColor TextBox with the ColorPicker extender.</span></span> <span data-ttu-id="fedbd-143">单击“确定”，关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="fedbd-143">Click OK to close the dialog.</span></span>

<span data-ttu-id="fedbd-144">进行这些更改后，页面的源如下所示。</span><span class="sxs-lookup"><span data-stu-id="fedbd-144">After you make these changes, the source for the page looks like Listing 2.</span></span>

<span data-ttu-id="fedbd-145">**列表 2-CreateCard （带有 ColorPicker）**</span><span class="sxs-lookup"><span data-stu-id="fedbd-145">**Listing 2 - CreateCard.aspx (with ColorPicker)**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

<span data-ttu-id="fedbd-146">请注意，该页现在包含 ColorPickerExtender 控件，该控件直接出现在 txtCardColor TextBox 控件的下方。</span><span class="sxs-lookup"><span data-stu-id="fedbd-146">Notice that the page now contains a ColorPickerExtender control that appears directly below the txtCardColor TextBox control.</span></span> <span data-ttu-id="fedbd-147">ColorPickerExtender 控件扩展了 txtCardColor 控件，使其显示颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="fedbd-147">The ColorPickerExtender control extends the txtCardColor control so that it displays a color picker dialog.</span></span>

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a><span data-ttu-id="fedbd-148">使用按钮启动 "颜色选取器" 对话框</span><span class="sxs-lookup"><span data-stu-id="fedbd-148">Using a Button to Launch the Color Picker Dialog</span></span>

<span data-ttu-id="fedbd-149">ColorPicker 扩展器支持以下属性：</span><span class="sxs-lookup"><span data-stu-id="fedbd-149">The ColorPicker extender supports the following properties:</span></span>

- <span data-ttu-id="fedbd-150">PopupButtonId-页面上导致颜色选取器对话框出现的按钮的 ID。</span><span class="sxs-lookup"><span data-stu-id="fedbd-150">PopupButtonId - The ID of a button on the page that causes the color picker dialog to appear.</span></span>
- <span data-ttu-id="fedbd-151">PopupPosition-颜色选取器对话框的相对于目标控件的位置。</span><span class="sxs-lookup"><span data-stu-id="fedbd-151">PopupPosition - The position, relative to the target control, of the color picker dialog.</span></span> <span data-ttu-id="fedbd-152">可能的值为绝对、居中、BottomLeft、BottomRight、TopLeft、右上、Right 和 Left （默认值为 BottomLeft）。</span><span class="sxs-lookup"><span data-stu-id="fedbd-152">Possible values are Absolute, Center, BottomLeft, BottomRight, TopLeft, TopRight, Right, and Left (the default is BottomLeft).</span></span>
- <span data-ttu-id="fedbd-153">SampleControlId-显示选定颜色的控件的 ID。</span><span class="sxs-lookup"><span data-stu-id="fedbd-153">SampleControlId - The ID of a control that displays the selected color.</span></span>
- <span data-ttu-id="fedbd-154">SelectedColor-ColorPicker 所选择的初始颜色。</span><span class="sxs-lookup"><span data-stu-id="fedbd-154">SelectedColor - The initial color selected by the ColorPicker.</span></span>

<span data-ttu-id="fedbd-155">您可以使用这些属性自定义颜色选取器对话框的显示方式以及所选颜色的显示方式。</span><span class="sxs-lookup"><span data-stu-id="fedbd-155">You can use these properties to customize how the color picker dialog is displayed and how the selected color is displayed.</span></span> <span data-ttu-id="fedbd-156">列表3中的页说明了如何使用这些属性中的几个。</span><span class="sxs-lookup"><span data-stu-id="fedbd-156">The page in Listing 3 illustrates how you can use several of these properties.</span></span>

<span data-ttu-id="fedbd-157">**列表 3-CreateCardButton**</span><span class="sxs-lookup"><span data-stu-id="fedbd-157">**Listing 3 - CreateCardButton.aspx**</span></span>

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

<span data-ttu-id="fedbd-158">列表3中的页包含 "选取颜色" 按钮（见图5）。</span><span class="sxs-lookup"><span data-stu-id="fedbd-158">The page in Listing 3 includes a Pick Color button (see Figure 5).</span></span> <span data-ttu-id="fedbd-159">单击此按钮时，"颜色选取器" 对话框将显示在文本框上方。</span><span class="sxs-lookup"><span data-stu-id="fedbd-159">When you click this button, the color picker dialog appears above the TextBox.</span></span> <span data-ttu-id="fedbd-160">如果从对话框中选择一种颜色，则所选颜色将显示为 lblSample 标签控件的背景色。</span><span class="sxs-lookup"><span data-stu-id="fedbd-160">If you select a color from the dialog then the selected color appears as the background color of the lblSample Label control.</span></span>

<span data-ttu-id="fedbd-161">ColorPicker PopupButtonID 属性用于将拾色按钮与 ColorPicker 扩展器相关联。</span><span class="sxs-lookup"><span data-stu-id="fedbd-161">The ColorPicker PopupButtonID property is used to associate the Pick Color button with the ColorPicker extender.</span></span> <span data-ttu-id="fedbd-162">为 PopupButtonID 属性提供值时，当目标控件具有焦点时，将不再显示 "颜色选取器" 对话框。</span><span class="sxs-lookup"><span data-stu-id="fedbd-162">When you supply a value for the PopupButtonID property, the color picker dialog no longer appears when the target control has focus.</span></span> <span data-ttu-id="fedbd-163">您必须单击该按钮以显示对话框。</span><span class="sxs-lookup"><span data-stu-id="fedbd-163">You must click the button to display the dialog.</span></span>

<span data-ttu-id="fedbd-164">SampleControlID 属性用于将显示选定颜色的控件与 ColorPicker 相关联。</span><span class="sxs-lookup"><span data-stu-id="fedbd-164">The SampleControlID property is used to associate a control that displays the selected color with the ColorPicker.</span></span> <span data-ttu-id="fedbd-165">ColorPicker 将该控件的背景色更改为当前选定的颜色。</span><span class="sxs-lookup"><span data-stu-id="fedbd-165">The ColorPicker changes the background color of this control to the currently selected color.</span></span>

<span data-ttu-id="fedbd-166">[使用按钮显示 "颜色选取器" 对话框 ![](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="fedbd-166">[![Displaying the color picker dialog with a button](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)</span></span>

<span data-ttu-id="fedbd-167">**图 05**：使用按钮显示 "颜色选取器" 对话框（[单击查看完全尺寸的图像](using-the-colorpicker-control-extender-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="fedbd-167">**Figure 05**: Displaying the color picker dialog with a button ([Click to view full-size image](using-the-colorpicker-control-extender-vb/_static/image10.png))</span></span>

## <a name="summary"></a><span data-ttu-id="fedbd-168">摘要</span><span class="sxs-lookup"><span data-stu-id="fedbd-168">Summary</span></span>

<span data-ttu-id="fedbd-169">在本教程中，已学习如何使用 ColorPicker 控件扩展器来显示弹出项颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="fedbd-169">In this tutorial, you learned how to use the ColorPicker control extender to display a popup color picker dialog.</span></span> <span data-ttu-id="fedbd-170">首先，我们介绍了如何在焦点移至 TextBox 控件时显示该对话框。</span><span class="sxs-lookup"><span data-stu-id="fedbd-170">First, we examined how you can display the dialog when focus is moved to a TextBox control.</span></span> <span data-ttu-id="fedbd-171">接下来，您学习了如何创建一个按钮，以便在单击按钮时显示颜色选取器对话框。</span><span class="sxs-lookup"><span data-stu-id="fedbd-171">Next, you learned how to create a button that displays the color picker dialog when the button is clicked.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fedbd-172">上一页</span><span class="sxs-lookup"><span data-stu-id="fedbd-172">Previous</span></span>](using-the-colorpicker-control-extender-cs.md)
