---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: 创建自定义 HTML 帮助C#程序（） |Microsoft Docs
author: microsoft
description: 本教程的目的是演示如何创建可在 MVC 视图中使用的自定义 HTML 帮助程序。 利用 HTML 帮助器 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 264ff9850bad397826b45649d52fbfefafc53a01
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594532"
---
# <a name="creating-custom-html-helpers-c"></a><span data-ttu-id="26e15-104">创建自定义 HTML 帮助程序 (C#)</span><span class="sxs-lookup"><span data-stu-id="26e15-104">Creating Custom HTML Helpers (C#)</span></span>

<span data-ttu-id="26e15-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="26e15-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="26e15-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="26e15-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> <span data-ttu-id="26e15-107">本教程的目的是演示如何创建可在 MVC 视图中使用的自定义 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="26e15-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="26e15-108">利用 HTML 帮助器，你可以减少创建标准 HTML 页面所必须执行的 HTML 标记的单调乏味类型。</span><span class="sxs-lookup"><span data-stu-id="26e15-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="26e15-109">本教程的目的是演示如何创建可在 MVC 视图中使用的自定义 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="26e15-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="26e15-110">利用 HTML 帮助器，你可以减少创建标准 HTML 页面所必须执行的 HTML 标记的单调乏味类型。</span><span class="sxs-lookup"><span data-stu-id="26e15-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="26e15-111">在本教程的第一部分中，我介绍了 ASP.NET MVC 框架附带的一些现有 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="26e15-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="26e15-112">接下来，我将介绍两种创建自定义 HTML 帮助器的方法：我介绍了如何通过创建静态方法并创建扩展方法来创建自定义 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="26e15-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a static method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="26e15-113">了解 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="26e15-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="26e15-114">HTML 帮助程序只是返回字符串的方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="26e15-115">字符串可以表示所需的任何类型的内容。</span><span class="sxs-lookup"><span data-stu-id="26e15-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="26e15-116">例如，可以使用 HTML 帮助器来呈现标准 HTML 标记，如 HTML `<input>` 和 `<img>` 标记。</span><span class="sxs-lookup"><span data-stu-id="26e15-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="26e15-117">你还可以使用 HTML 帮助器来呈现更复杂的内容，例如选项卡条或 HTML 表数据库数据。</span><span class="sxs-lookup"><span data-stu-id="26e15-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="26e15-118">ASP.NET MVC 框架包含以下一组标准 HTML 帮助程序（这不是完整的列表）：</span><span class="sxs-lookup"><span data-stu-id="26e15-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="26e15-119">Html.actionlink （）</span><span class="sxs-lookup"><span data-stu-id="26e15-119">Html.ActionLink()</span></span>
- <span data-ttu-id="26e15-120">Html.beginform （）</span><span class="sxs-lookup"><span data-stu-id="26e15-120">Html.BeginForm()</span></span>
- <span data-ttu-id="26e15-121">Html. CheckBox （）</span><span class="sxs-lookup"><span data-stu-id="26e15-121">Html.CheckBox()</span></span>
- <span data-ttu-id="26e15-122">DropDownList （）</span><span class="sxs-lookup"><span data-stu-id="26e15-122">Html.DropDownList()</span></span>
- <span data-ttu-id="26e15-123">EndForm （）</span><span class="sxs-lookup"><span data-stu-id="26e15-123">Html.EndForm()</span></span>
- <span data-ttu-id="26e15-124">.Html （隐藏）（）</span><span class="sxs-lookup"><span data-stu-id="26e15-124">Html.Hidden()</span></span>
- <span data-ttu-id="26e15-125">Html. ListBox （）</span><span class="sxs-lookup"><span data-stu-id="26e15-125">Html.ListBox()</span></span>
- <span data-ttu-id="26e15-126">.Html. Password （）</span><span class="sxs-lookup"><span data-stu-id="26e15-126">Html.Password()</span></span>
- <span data-ttu-id="26e15-127">.Html （）</span><span class="sxs-lookup"><span data-stu-id="26e15-127">Html.RadioButton()</span></span>
- <span data-ttu-id="26e15-128">.Html （）</span><span class="sxs-lookup"><span data-stu-id="26e15-128">Html.TextArea()</span></span>
- <span data-ttu-id="26e15-129">.Html （）</span><span class="sxs-lookup"><span data-stu-id="26e15-129">Html.TextBox()</span></span>

<span data-ttu-id="26e15-130">例如，请考虑列表1中的窗体。</span><span class="sxs-lookup"><span data-stu-id="26e15-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="26e15-131">此窗体通过两个标准 HTML 帮助器的帮助进行呈现（参见图1）。</span><span class="sxs-lookup"><span data-stu-id="26e15-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="26e15-132">此窗体使用 `Html.BeginForm()` 和 `Html.TextBox()` 帮助程序方法来呈现简单的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="26e15-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods to render a simple HTML form.</span></span>

<span data-ttu-id="26e15-133">[用 HTML 帮助器呈现的 ![页面](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="26e15-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="26e15-134">**图 01**：用 HTML 帮助器呈现的页面（[单击查看完全尺寸的图像](creating-custom-html-helpers-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="26e15-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image3.png))</span></span>

<span data-ttu-id="26e15-135">**列表1– `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="26e15-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

<span data-ttu-id="26e15-136">Html.beginform （） Helper 方法用于创建开始和关闭 HTML `<form>` 标记。</span><span class="sxs-lookup"><span data-stu-id="26e15-136">The Html.BeginForm() Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="26e15-137">请注意，`Html.BeginForm()` 方法是在 using 语句中调用的。</span><span class="sxs-lookup"><span data-stu-id="26e15-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="26e15-138">Using 语句可确保在使用块的末尾关闭 `<form>` 标记。</span><span class="sxs-lookup"><span data-stu-id="26e15-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="26e15-139">如果你愿意，可以调用 EndForm （） Helper 方法来关闭 `<form>` 标记，而不是创建 using 块。</span><span class="sxs-lookup"><span data-stu-id="26e15-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="26e15-140">使用任何一种方法来创建与您最直观的开始和结束 `<form>` 标记。</span><span class="sxs-lookup"><span data-stu-id="26e15-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="26e15-141">`Html.TextBox()` 帮助器方法在列表1中用于呈现 HTML `<input>` 标记。</span><span class="sxs-lookup"><span data-stu-id="26e15-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="26e15-142">如果在浏览器中选择 "查看源"，则会看到列表2中的 HTML 源。</span><span class="sxs-lookup"><span data-stu-id="26e15-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="26e15-143">请注意，源包含标准 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="26e15-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26e15-144">请注意，`Html.TextBox()`HTML 帮助器是用 `<%= %>` 标记而不是 `<% %>` 标记呈现的。</span><span class="sxs-lookup"><span data-stu-id="26e15-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="26e15-145">如果不包含等号，则不会在浏览器中呈现任何内容。</span><span class="sxs-lookup"><span data-stu-id="26e15-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="26e15-146">ASP.NET MVC 框架包含一小部分帮助程序。</span><span class="sxs-lookup"><span data-stu-id="26e15-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="26e15-147">大多数情况下，你将需要通过自定义 HTML 帮助器来扩展 MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="26e15-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="26e15-148">在本教程的其余部分中，您将学习创建自定义 HTML 帮助程序的两种方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="26e15-149">**列表2– `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="26e15-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a><span data-ttu-id="26e15-150">创建具有静态方法的 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="26e15-150">Creating HTML Helpers with Static Methods</span></span>

<span data-ttu-id="26e15-151">创建新的 HTML 帮助器的最简单方法是创建返回字符串的静态方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-151">The easiest way to create a new HTML Helper is to create a static method that returns a string.</span></span> <span data-ttu-id="26e15-152">例如，假设您决定创建一个呈现 HTML `<label>` 标记的新 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="26e15-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="26e15-153">您可以使用清单2中的类呈现 `<label>`。</span><span class="sxs-lookup"><span data-stu-id="26e15-153">You can use the class in Listing 2 to render a `<label>` .</span></span>

<span data-ttu-id="26e15-154">**列表2– `Helpers\LabelHelper.cs`**</span><span class="sxs-lookup"><span data-stu-id="26e15-154">**Listing 2 – `Helpers\LabelHelper.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

<span data-ttu-id="26e15-155">对于清单2中的类没有什么特别之处。</span><span class="sxs-lookup"><span data-stu-id="26e15-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="26e15-156">`Label()` 方法只返回一个字符串。</span><span class="sxs-lookup"><span data-stu-id="26e15-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="26e15-157">列表3中修改的索引视图使用 `LabelHelper` 来呈现 HTML `<label>` 标记。</span><span class="sxs-lookup"><span data-stu-id="26e15-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="26e15-158">请注意，此视图包含导入 `Application1.Helpers` 命名空间的 `<%@ imports %>` 指令。</span><span class="sxs-lookup"><span data-stu-id="26e15-158">Notice that the view includes an `<%@ imports %>` directive that imports the `Application1.Helpers` namespace.</span></span>

<span data-ttu-id="26e15-159">**列表2– `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="26e15-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="26e15-160">创建具有扩展方法的 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="26e15-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="26e15-161">如果要创建与 ASP.NET MVC 框架中包含的标准 HTML 帮助器相同的 HTML 帮助器，则需要创建扩展方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="26e15-162">扩展方法使你能够向现有类添加新方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="26e15-163">创建 HTML 帮助器方法时，可以向视图的 Html 属性所表示的 HtmlHelper 类添加新方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-163">When creating an HTML Helper method, you add new methods to the HtmlHelper class represented by a view's Html property.</span></span>

<span data-ttu-id="26e15-164">清单3中的类将扩展方法添加到名为 `Label()`的 `HtmlHelper` 类中。</span><span class="sxs-lookup"><span data-stu-id="26e15-164">The class in Listing 3 adds an extension method to the `HtmlHelper` class named `Label()`.</span></span> <span data-ttu-id="26e15-165">对于此类，需要注意几个问题。</span><span class="sxs-lookup"><span data-stu-id="26e15-165">There are a couple of things that you should notice about this class.</span></span> <span data-ttu-id="26e15-166">首先，请注意，类是静态类。</span><span class="sxs-lookup"><span data-stu-id="26e15-166">First, notice that the class is a static class.</span></span> <span data-ttu-id="26e15-167">必须使用静态类定义扩展方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-167">You must define an extension method with a static class.</span></span>

<span data-ttu-id="26e15-168">其次，请注意，`Label()` 方法的第一个参数前面有关键字 `this`。</span><span class="sxs-lookup"><span data-stu-id="26e15-168">Second, notice that the first parameter of the `Label()` method is preceded by the keyword `this`.</span></span> <span data-ttu-id="26e15-169">扩展方法的第一个参数指示扩展方法扩展的类。</span><span class="sxs-lookup"><span data-stu-id="26e15-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="26e15-170">**列表 3-`Helpers\LabelExtensions.cs`**</span><span class="sxs-lookup"><span data-stu-id="26e15-170">**Listing 3 – `Helpers\LabelExtensions.cs`**</span></span>

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

<span data-ttu-id="26e15-171">创建扩展方法并成功生成应用程序后，扩展方法将出现在 Visual Studio Intellisense 中，如类的所有其他方法（请参阅图2）。</span><span class="sxs-lookup"><span data-stu-id="26e15-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="26e15-172">唯一的区别在于，扩展方法旁边会出现一个特殊符号（向下箭头图标）。</span><span class="sxs-lookup"><span data-stu-id="26e15-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="26e15-173">[使用 Html. Label （）扩展方法 ![](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="26e15-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)</span></span>

<span data-ttu-id="26e15-174">**图 02**：使用 Html. Label （）扩展方法（[单击以查看完全大小的图像](creating-custom-html-helpers-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="26e15-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-cs/_static/image6.png))</span></span>

<span data-ttu-id="26e15-175">列表4中修改的索引视图使用 Html. Label （）扩展方法呈现其所有 `<label>` 标记。</span><span class="sxs-lookup"><span data-stu-id="26e15-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its `<label>` tags.</span></span>

<span data-ttu-id="26e15-176">**列表 4-`Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="26e15-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="26e15-177">总结</span><span class="sxs-lookup"><span data-stu-id="26e15-177">Summary</span></span>

<span data-ttu-id="26e15-178">本教程介绍了创建自定义 HTML 帮助程序的两种方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="26e15-179">首先，您学习了如何通过创建返回字符串的静态方法来创建自定义 `Label()` HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="26e15-179">First, you learned how to create a custom `Label()` HTML Helper by creating a static method that returns a string.</span></span> <span data-ttu-id="26e15-180">接下来，你已了解如何通过在 `HtmlHelper` 类上创建扩展方法来创建自定义 `Label()` HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="26e15-181">在本教程中，我将重点介绍如何构建一个极其简单的 HTML 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="26e15-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="26e15-182">请注意，HTML 帮助程序可能会非常复杂。</span><span class="sxs-lookup"><span data-stu-id="26e15-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="26e15-183">您可以生成 HTML 帮助器来呈现丰富的内容，如树视图、菜单或数据库数据的表。</span><span class="sxs-lookup"><span data-stu-id="26e15-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="26e15-184">[上一页](asp-net-mvc-views-overview-cs.md)
> [下一页](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span><span class="sxs-lookup"><span data-stu-id="26e15-184">[Previous](asp-net-mvc-views-overview-cs.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-cs.md)</span></span>
