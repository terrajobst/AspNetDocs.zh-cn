---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: 介绍 ASP.NET 网页-创建一致的布局 |Microsoft Docs
author: Rick-Anderson
description: 本教程介绍如何使用布局为使用 ASP.NET 网页的站点上的页面创建一致的外观。 它假定您已完成 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422744"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="fedef-104">简介 ASP.NET 网页-创建一致的布局</span><span class="sxs-lookup"><span data-stu-id="fedef-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>

<span data-ttu-id="fedef-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="fedef-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="fedef-106">本教程介绍如何使用*布局*为使用 ASP.NET 网页的站点上的页面创建一致的外观。</span><span class="sxs-lookup"><span data-stu-id="fedef-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="fedef-107">假设已[在 ASP.NET 网页中通过删除数据库数据](https://go.microsoft.com/fwlink/?LinkId=251584)完成了序列。</span><span class="sxs-lookup"><span data-stu-id="fedef-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="fedef-108">学习内容：</span><span class="sxs-lookup"><span data-stu-id="fedef-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="fedef-109">布局页的含义。</span><span class="sxs-lookup"><span data-stu-id="fedef-109">What a layout page is.</span></span>
> - <span data-ttu-id="fedef-110">如何将布局页与动态内容组合在一起。</span><span class="sxs-lookup"><span data-stu-id="fedef-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="fedef-111">如何将值传递到布局页。</span><span class="sxs-lookup"><span data-stu-id="fedef-111">How to pass values to a layout page.</span></span>

## <a name="about-layouts"></a><span data-ttu-id="fedef-112">关于布局</span><span class="sxs-lookup"><span data-stu-id="fedef-112">About Layouts</span></span>

<span data-ttu-id="fedef-113">到目前为止，已经完成了所有独立页面。</span><span class="sxs-lookup"><span data-stu-id="fedef-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="fedef-114">它们全都属于同一站点，但它们没有任何常见的元素或标准的外观。</span><span class="sxs-lookup"><span data-stu-id="fedef-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="fedef-115">大多数站点都具有一致的外观和布局。</span><span class="sxs-lookup"><span data-stu-id="fedef-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="fedef-116">例如，如果你访问[Microsoft.com/web](https://www.microsoft.com/web/)站点并进行查找，你会看到这些页面都遵循整体布局和视觉主题：</span><span class="sxs-lookup"><span data-stu-id="fedef-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![显示标头、导航区域、内容区域和页脚布局的 Microsoft.com/web 网站页面](layouts/_static/image1.png)

<span data-ttu-id="fedef-118">创建此布局的*低效*方法是在每个页面上分别定义标题、导航栏和页脚。</span><span class="sxs-lookup"><span data-stu-id="fedef-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="fedef-119">每次都要复制相同的标记。</span><span class="sxs-lookup"><span data-stu-id="fedef-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="fedef-120">如果要更改某些内容（例如，更新页脚），则必须单独更改每个页面。</span><span class="sxs-lookup"><span data-stu-id="fedef-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="fedef-121">这就是*布局页面*的位置。</span><span class="sxs-lookup"><span data-stu-id="fedef-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="fedef-122">在 ASP.NET 网页中，可以定义为网站上的页面提供总体容器的布局页面。</span><span class="sxs-lookup"><span data-stu-id="fedef-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="fedef-123">例如，"布局" 页可以包含页眉、导航区和页脚。</span><span class="sxs-lookup"><span data-stu-id="fedef-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="fedef-124">"布局" 页包含一个占位符，其中包含主要内容。</span><span class="sxs-lookup"><span data-stu-id="fedef-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="fedef-125">然后，可以定义单独的内容页，其中只包含该页的标记和代码。</span><span class="sxs-lookup"><span data-stu-id="fedef-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="fedef-126">内容页面不必是完整的 HTML 页面;它们甚至不必有 `<body>` 元素。</span><span class="sxs-lookup"><span data-stu-id="fedef-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="fedef-127">它们还具有一行代码，告诉 ASP.NET 要在其中显示内容的布局页。</span><span class="sxs-lookup"><span data-stu-id="fedef-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="fedef-128">下面的图片显示了此关系的具体工作原理：</span><span class="sxs-lookup"><span data-stu-id="fedef-128">Here's a picture that shows roughly how this relationship works:</span></span>

![显示两个内容页以及它们适用的布局页的概念图](layouts/_static/image2.png)

<span data-ttu-id="fedef-130">当你在操作中看到此交互时，可以轻松理解这种交互。</span><span class="sxs-lookup"><span data-stu-id="fedef-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="fedef-131">在本教程中，你将更改电影页面以使用布局。</span><span class="sxs-lookup"><span data-stu-id="fedef-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="fedef-132">添加布局页</span><span class="sxs-lookup"><span data-stu-id="fedef-132">Adding a Layout Page</span></span>

<span data-ttu-id="fedef-133">首先创建一个布局页面，用于定义具有页眉、页脚和主要内容区域的典型页面布局。</span><span class="sxs-lookup"><span data-stu-id="fedef-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="fedef-134">在 WebPagesMovies 网站中，添加一个名为 *\_* 的 CSHTML 页面。</span><span class="sxs-lookup"><span data-stu-id="fedef-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="fedef-135">前导下划线（`_`）字符很重要。</span><span class="sxs-lookup"><span data-stu-id="fedef-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="fedef-136">如果页的名称以下划线开头，则 ASP.NET 不会直接将该页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="fedef-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="fedef-137">此约定允许您定义站点所需的页面，但用户不能直接请求。</span><span class="sxs-lookup"><span data-stu-id="fedef-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="fedef-138">将页面中的内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="fedef-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="fedef-139">如您所见，此标记只是 HTML，它使用 `<div>` 元素来定义页面中的三个节，另外还有一个 `<div>` 元素用来保存这三个部分。</span><span class="sxs-lookup"><span data-stu-id="fedef-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="fedef-140">页脚包含一小段代码： `@DateTime.Now.Year`，它将在页面的该位置呈现当前年份。</span><span class="sxs-lookup"><span data-stu-id="fedef-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="fedef-141">请注意，有一个指向样式表的链接，*其名称为 ""。*</span><span class="sxs-lookup"><span data-stu-id="fedef-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="fedef-142">样式表将定义元素的物理布局的详细信息。</span><span class="sxs-lookup"><span data-stu-id="fedef-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="fedef-143">稍后你将创建它。</span><span class="sxs-lookup"><span data-stu-id="fedef-143">You'll create that in a moment.</span></span>

<span data-ttu-id="fedef-144">此 *\_布局*`@Render.Body()` 中唯一的一项功能是行。</span><span class="sxs-lookup"><span data-stu-id="fedef-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="fedef-145">这是在此布局与另一个页面合并时内容将移到的占位符。</span><span class="sxs-lookup"><span data-stu-id="fedef-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="fedef-146">添加 .css 文件</span><span class="sxs-lookup"><span data-stu-id="fedef-146">Adding a .css File</span></span>

<span data-ttu-id="fedef-147">定义页上元素的实际排列（即外观）的首选方法是使用级联样式表（CSS）规则。</span><span class="sxs-lookup"><span data-stu-id="fedef-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="fedef-148">因此，你将创建一个包含新布局规则的 *.css*文件。</span><span class="sxs-lookup"><span data-stu-id="fedef-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="fedef-149">在 WebMatrix 中，选择你的站点的根目录。</span><span class="sxs-lookup"><span data-stu-id="fedef-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="fedef-150">然后，在功能区的 "**文件**" 选项卡中，单击 "**新建**" 按钮下的箭头，然后单击 "**新建文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="fedef-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![功能区中的 "新建" 下面的 "新建文件夹" 选项。](layouts/_static/image3.png)

<span data-ttu-id="fedef-152">将新文件夹命名为*样式*。</span><span class="sxs-lookup"><span data-stu-id="fedef-152">Name the new folder *Styles*.</span></span>

![命名新文件夹 "样式"](layouts/_static/image4.png)

<span data-ttu-id="fedef-154">在 "新建*样式*" 文件夹中，*创建名为 "" 的文件*。</span><span class="sxs-lookup"><span data-stu-id="fedef-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![创建新的电影 .css 文件](layouts/_static/image5.png)

<span data-ttu-id="fedef-156">将新 *.css*文件的内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="fedef-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="fedef-157">除了说明两个情况外，我们不会涉及到这些 CSS 规则。</span><span class="sxs-lookup"><span data-stu-id="fedef-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="fedef-158">其中一种做法是：除了设置字体和大小以外，规则还使用绝对定位来确定页眉、页脚和主要内容区域的位置。</span><span class="sxs-lookup"><span data-stu-id="fedef-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="fedef-159">如果你不熟悉 CSS 中的定位，可以在 W3Schools 网站上阅读[Css 定位](http://www.w3schools.com/css/css_positioning.asp)教程。</span><span class="sxs-lookup"><span data-stu-id="fedef-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="fedef-160">需要注意的另一点是，在底部，我们复制了最初在 "*电影. cshtml* " 文件中单独定义的样式规则。</span><span class="sxs-lookup"><span data-stu-id="fedef-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="fedef-161">[通过使用 ASP.NET 网页](https://go.microsoft.com/fwlink/?LinkId=251580)教程使向表添加条纹的 `WebGrid` 帮助程序呈现标记，在介绍中使用了这些规则。</span><span class="sxs-lookup"><span data-stu-id="fedef-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="fedef-162">（如果要为样式定义使用 *.css*文件，则也可以将整个网站的样式规则放在一起。）</span><span class="sxs-lookup"><span data-stu-id="fedef-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="fedef-163">更新影片文件以使用布局</span><span class="sxs-lookup"><span data-stu-id="fedef-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="fedef-164">现在，你可以更新站点中的现有文件，以使用新的布局。</span><span class="sxs-lookup"><span data-stu-id="fedef-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="fedef-165">打开*电影. cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="fedef-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="fedef-166">在顶部，作为第一行代码，添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="fedef-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="fedef-167">该页现在以这种方式开始：</span><span class="sxs-lookup"><span data-stu-id="fedef-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="fedef-168">这一行代码告诉 ASP.NET 当*电影*页面运行时，应将其与 *\_布局 cshtml*文件合并。</span><span class="sxs-lookup"><span data-stu-id="fedef-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="fedef-169">由于*影院*文件现在使用布局页面，因此你可以从 *\_布局 cshtml*文件中删除由的 "*电影. cshtml* " 页中的标记。</span><span class="sxs-lookup"><span data-stu-id="fedef-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="fedef-170">`<!DOCTYPE>`、`<html>`和 `<body>` 打开和关闭标记。</span><span class="sxs-lookup"><span data-stu-id="fedef-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="fedef-171">提取整个 `<head>` 元素及其内容，其中包括网格的样式规则，因为现在已经在 *.css*文件中获得了这些规则。</span><span class="sxs-lookup"><span data-stu-id="fedef-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="fedef-172">在此过程中，将现有 `<h1>` 元素更改为 `<h2>` 元素;布局页中已有 `<h1>` 元素。</span><span class="sxs-lookup"><span data-stu-id="fedef-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="fedef-173">将 `<h2>` 文本更改为 "列出电影"。</span><span class="sxs-lookup"><span data-stu-id="fedef-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="fedef-174">通常无需在内容页中进行这些更改。</span><span class="sxs-lookup"><span data-stu-id="fedef-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="fedef-175">当你使用布局页启动站点时，将创建不包含所有这些元素的内容页面。</span><span class="sxs-lookup"><span data-stu-id="fedef-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="fedef-176">不过，在这种情况下，你要将独立页面转换为使用布局的页面，因此会有一点清理。</span><span class="sxs-lookup"><span data-stu-id="fedef-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="fedef-177">完成后，"*电影*" 页将如下所示：</span><span class="sxs-lookup"><span data-stu-id="fedef-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="fedef-178">测试布局</span><span class="sxs-lookup"><span data-stu-id="fedef-178">Testing the Layout</span></span>

<span data-ttu-id="fedef-179">现在，可以看到布局的外观。</span><span class="sxs-lookup"><span data-stu-id="fedef-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="fedef-180">在 WebMatrix 中，右键*单击 ""* ，然后选择 "**在浏览器中启动**"。</span><span class="sxs-lookup"><span data-stu-id="fedef-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="fedef-181">当浏览器显示该页时，它将如下所示：</span><span class="sxs-lookup"><span data-stu-id="fedef-181">When the browser displays the page, it looks like this page:</span></span>

![使用布局呈现的电影页面](layouts/_static/image6.png)

<span data-ttu-id="fedef-183">ASP.NET 已将 "" 页的内容合并到 `RenderBody` 方法所在的 *\_Layout。*</span><span class="sxs-lookup"><span data-stu-id="fedef-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="fedef-184">当然，\_的*布局. cshtml*页引用定义页面外观的 *.css*文件。</span><span class="sxs-lookup"><span data-stu-id="fedef-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="fedef-185">更新 AddMovie 页以使用布局</span><span class="sxs-lookup"><span data-stu-id="fedef-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="fedef-186">布局的真正优点在于，您可以将它们用于站点中的所有页面。</span><span class="sxs-lookup"><span data-stu-id="fedef-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="fedef-187">打开*AddMovie*页。</span><span class="sxs-lookup"><span data-stu-id="fedef-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="fedef-188">你可能会注意到， *AddMovie*页最初在其中有一些 CSS 规则用于定义验证错误消息的外观。</span><span class="sxs-lookup"><span data-stu-id="fedef-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="fedef-189">由于你的网站现在具有一个 *.css*文件，因此你可以将这些规则移动到 *.css*文件中。</span><span class="sxs-lookup"><span data-stu-id="fedef-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="fedef-190">从*AddMovie*文件中删除它们，并将它们添加到 "*电影*" 文件的底部。</span><span class="sxs-lookup"><span data-stu-id="fedef-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="fedef-191">正在移动以下规则：</span><span class="sxs-lookup"><span data-stu-id="fedef-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="fedef-192">现在，在*AddMovie*中对所做的更改进行相同的更改 *：添加*`Layout="~/_Layout.cshtml;`，并删除目前无关的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="fedef-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="fedef-193">将 `<h1>` 元素更改为 `<h2>`。</span><span class="sxs-lookup"><span data-stu-id="fedef-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="fedef-194">完成后，页面将如下所示：</span><span class="sxs-lookup"><span data-stu-id="fedef-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="fedef-195">运行页面。</span><span class="sxs-lookup"><span data-stu-id="fedef-195">Run the page.</span></span> <span data-ttu-id="fedef-196">现在，它如下图所示：</span><span class="sxs-lookup"><span data-stu-id="fedef-196">Now it looks like this illustration:</span></span>

![使用布局呈现的 "添加电影" 页面](layouts/_static/image7.png)

<span data-ttu-id="fedef-198">需要对站点中的页面（ *EditMovie*和*DeleteMovie*）进行类似的更改。</span><span class="sxs-lookup"><span data-stu-id="fedef-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="fedef-199">但是，在执行此操作之前，您可以对布局进行另一个更改，使其变得更加灵活。</span><span class="sxs-lookup"><span data-stu-id="fedef-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="fedef-200">将标题信息传递到布局页</span><span class="sxs-lookup"><span data-stu-id="fedef-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="fedef-201">你创建的 *\_Layout* `<title>` 元素的元素设置为 "我的电影网站"。</span><span class="sxs-lookup"><span data-stu-id="fedef-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="fedef-202">大多数浏览器将此元素的内容显示为选项卡上的文本：</span><span class="sxs-lookup"><span data-stu-id="fedef-202">Most browsers display the content of this element as the text on a tab:</span></span>

![在浏览器选项卡中显示的页面 &lt;标题&gt; 元素](layouts/_static/image8.png)

<span data-ttu-id="fedef-204">此标题信息是通用的。</span><span class="sxs-lookup"><span data-stu-id="fedef-204">This title information is generic.</span></span> <span data-ttu-id="fedef-205">假设您希望标题文本更特定于当前页。</span><span class="sxs-lookup"><span data-stu-id="fedef-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="fedef-206">（标题文本还由搜索引擎用来确定页面的内容。）可以将信息从诸如*AddMovie 或*的内容页传递到布局页，然后使用该信息自定义布局页的呈现内容。</span><span class="sxs-lookup"><span data-stu-id="fedef-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="fedef-207">再次打开 "*电影. cshtml* " 页。</span><span class="sxs-lookup"><span data-stu-id="fedef-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="fedef-208">在顶部的代码中，添加以下行：</span><span class="sxs-lookup"><span data-stu-id="fedef-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="fedef-209">`Page` 对象可用于所有的*cshtml*页，用于实现此目的，即在页与其布局之间共享信息。</span><span class="sxs-lookup"><span data-stu-id="fedef-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="fedef-210">打开 *\_布局. cshtml* "页。</span><span class="sxs-lookup"><span data-stu-id="fedef-210">Open the *\_Layout.cshtml* page.</span></span> <span data-ttu-id="fedef-211">更改 `<title>` 元素，使其类似于以下标记：</span><span class="sxs-lookup"><span data-stu-id="fedef-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="fedef-212">此代码会在页中该位置的 `Page.Title` 属性右侧呈现任何内容。</span><span class="sxs-lookup"><span data-stu-id="fedef-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="fedef-213">运行 "*电影*" 页。</span><span class="sxs-lookup"><span data-stu-id="fedef-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="fedef-214">这次，"浏览器" 选项卡会显示你作为 `Page.Title`值传递的内容：</span><span class="sxs-lookup"><span data-stu-id="fedef-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![显示动态创建的标题的浏览器选项卡](layouts/_static/image9.png)

<span data-ttu-id="fedef-216">如果需要，请在浏览器中查看页面源。</span><span class="sxs-lookup"><span data-stu-id="fedef-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="fedef-217">您可以看到 `<title>` 元素呈现为 `<title>List Movies</title>`。</span><span class="sxs-lookup"><span data-stu-id="fedef-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="fedef-218">**Page 对象**</span><span class="sxs-lookup"><span data-stu-id="fedef-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="fedef-219">`Page` 的一项有用功能是动态对象-`Title` 属性不是固定或保留的名称。</span><span class="sxs-lookup"><span data-stu-id="fedef-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="fedef-220">可以将*任何*名称用于 `Page` 对象的值。</span><span class="sxs-lookup"><span data-stu-id="fedef-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="fedef-221">例如，你可以通过使用名为 `Page.CurrentName` 或 `Page.MyPage`的属性轻松地传递标题。</span><span class="sxs-lookup"><span data-stu-id="fedef-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="fedef-222">唯一的限制是，名称必须遵循可命名属性的常规规则。</span><span class="sxs-lookup"><span data-stu-id="fedef-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="fedef-223">（例如，名称不能包含空格。）</span><span class="sxs-lookup"><span data-stu-id="fedef-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="fedef-224">可以通过使用 `Page` 对象传递任意数量的值。</span><span class="sxs-lookup"><span data-stu-id="fedef-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="fedef-225">如果要将电影信息传递到布局页面，可以使用 `Page.MovieTitle` 和 `Page.Genre` 和 `Page.MovieYear`之类的内容传递值。</span><span class="sxs-lookup"><span data-stu-id="fedef-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="fedef-226">（或你为存储信息而所用的任何其他名称。）唯一的要求（可能是显而易见的要求）是您必须在 "内容" 页和 "布局" 页中使用相同的名称。</span><span class="sxs-lookup"><span data-stu-id="fedef-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="fedef-227">使用 `Page` 对象传递的信息并不局限于布局页上显示的文本。</span><span class="sxs-lookup"><span data-stu-id="fedef-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="fedef-228">您可以将某个值传递到布局页，然后 "布局" 页中的代码可以使用该值来决定是显示该页的某个部分、要使用什么 *.css*文件等。</span><span class="sxs-lookup"><span data-stu-id="fedef-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="fedef-229">在 `Page` 对象中传递的值与您在代码中使用的任何其他值类似。</span><span class="sxs-lookup"><span data-stu-id="fedef-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="fedef-230">这只是值源自内容页，并传递到布局页。</span><span class="sxs-lookup"><span data-stu-id="fedef-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>

<span data-ttu-id="fedef-231">打开*AddMovie*页面，并在代码顶部添加一行，以提供*AddMovie*页面的标题：</span><span class="sxs-lookup"><span data-stu-id="fedef-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="fedef-232">运行*AddMovie*页。</span><span class="sxs-lookup"><span data-stu-id="fedef-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="fedef-233">你将在此处看到新标题：</span><span class="sxs-lookup"><span data-stu-id="fedef-233">You see the new title there:</span></span>

![显示动态创建的 "添加电影" 标题的浏览器选项卡](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="fedef-235">更新剩余页面以使用布局</span><span class="sxs-lookup"><span data-stu-id="fedef-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="fedef-236">现在，你可以完成站点中的其余页面，使其使用新的布局。</span><span class="sxs-lookup"><span data-stu-id="fedef-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="fedef-237">依次打开*EditMovie*和*DeleteMovie* ，并在每个中进行相同的更改。</span><span class="sxs-lookup"><span data-stu-id="fedef-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="fedef-238">添加链接到布局页的代码行：</span><span class="sxs-lookup"><span data-stu-id="fedef-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="fedef-239">添加线条以设置页面标题：</span><span class="sxs-lookup"><span data-stu-id="fedef-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="fedef-240">或：</span><span class="sxs-lookup"><span data-stu-id="fedef-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="fedef-241">删除所有无关的 HTML 标记，基本上只保留位于 `<body>` 元素内的位（和顶部的代码块）。</span><span class="sxs-lookup"><span data-stu-id="fedef-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="fedef-242">将 `<h1>` 元素更改为 `<h2>` 元素。</span><span class="sxs-lookup"><span data-stu-id="fedef-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="fedef-243">进行这些更改后，请对每个更改进行测试，并确保其正确显示并且标题正确。</span><span class="sxs-lookup"><span data-stu-id="fedef-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="fedef-244">有关布局页的分型想法</span><span class="sxs-lookup"><span data-stu-id="fedef-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="fedef-245">在本教程中，您将创建一个 *\_的布局. cshtml*页，并使用 `RenderBody` 方法来合并另一个页面中的内容。</span><span class="sxs-lookup"><span data-stu-id="fedef-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="fedef-246">这是在网页中使用布局的基本模式。</span><span class="sxs-lookup"><span data-stu-id="fedef-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="fedef-247">布局页中有一些其他功能，我们没有在此介绍。</span><span class="sxs-lookup"><span data-stu-id="fedef-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="fedef-248">例如，您可以嵌套布局页，一个布局页可以反过来引用另一个。</span><span class="sxs-lookup"><span data-stu-id="fedef-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="fedef-249">如果要使用需要不同布局的站点的子节，则嵌套布局会很有用。</span><span class="sxs-lookup"><span data-stu-id="fedef-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="fedef-250">你还可以使用其他方法（例如 `RenderSection`）在布局页面中设置命名节。</span><span class="sxs-lookup"><span data-stu-id="fedef-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="fedef-251">布局页和 *.css*文件的组合非常强大。</span><span class="sxs-lookup"><span data-stu-id="fedef-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="fedef-252">正如你将在下一系列教程中看到的那样，在 WebMatrix 中，你可以基于*模板*创建一个网站，该网站提供了一个具有预生成功能的网站。</span><span class="sxs-lookup"><span data-stu-id="fedef-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="fedef-253">这些模板充分利用了布局页和 CSS，创建外观非常好并且具有菜单等功能的网站。</span><span class="sxs-lookup"><span data-stu-id="fedef-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="fedef-254">下面是基于模板的网站主页的屏幕截图，其中显示了使用布局页和 CSS 的功能：</span><span class="sxs-lookup"><span data-stu-id="fedef-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![WebMatrix 站点模板创建的布局，显示标题、导航区域、内容区域、可选部分和登录链接](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="fedef-256">完整的电影页面列表（已更新为使用布局页面）</span><span class="sxs-lookup"><span data-stu-id="fedef-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="fedef-257">"添加电影" 页的完整页面列表（已更新布局）</span><span class="sxs-lookup"><span data-stu-id="fedef-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="fedef-258">删除电影页面的完整页面列表（已更新布局）</span><span class="sxs-lookup"><span data-stu-id="fedef-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="fedef-259">编辑电影页面的完整页面列表（已更新布局）</span><span class="sxs-lookup"><span data-stu-id="fedef-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="fedef-260">下一步</span><span class="sxs-lookup"><span data-stu-id="fedef-260">Coming Up Next</span></span>

<span data-ttu-id="fedef-261">在下一教程中，你将了解如何将网站发布到 Internet，以便每个人都可以看到它。</span><span class="sxs-lookup"><span data-stu-id="fedef-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="fedef-262">其他资源</span><span class="sxs-lookup"><span data-stu-id="fedef-262">Additional Resources</span></span>

- <span data-ttu-id="fedef-263">[创建一致的外观](https://go.microsoft.com/fwlink/?LinkID=202891)，这篇文章提供了有关如何使用布局的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="fedef-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="fedef-264">还介绍了如何将值传递到显示或隐藏某些内容的布局页。</span><span class="sxs-lookup"><span data-stu-id="fedef-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="fedef-265">[使用 Razor 的嵌套布局页](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor)-Mike Brind 博客提供了有关如何嵌套布局页的示例。</span><span class="sxs-lookup"><span data-stu-id="fedef-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="fedef-266">（包括页面的下载。）</span><span class="sxs-lookup"><span data-stu-id="fedef-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fedef-267">[上一页](deleting-data.md)
> [下一页](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="fedef-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>
