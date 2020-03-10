---
uid: mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
title: 用查看母版页创建页面布局（C#） |Microsoft Docs
author: microsoft
description: 在本教程中，将了解如何通过利用视图母版页，为应用程序中的多个页面创建公共页面布局。 您可以使用 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: dff54fcb-68b1-4488-89a2-ca97532d6a4c
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-page-layouts-with-view-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 026e3efb4ebf84016aa0f6a5fda4af549fdadfcb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435194"
---
# <a name="creating-page-layouts-with-view-master-pages-c"></a><span data-ttu-id="81719-104">使用视图母版页创建页面布局 (C#)</span><span class="sxs-lookup"><span data-stu-id="81719-104">Creating Page Layouts with View Master Pages (C#)</span></span>

<span data-ttu-id="81719-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="81719-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="81719-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="81719-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_12_CS.pdf)

> <span data-ttu-id="81719-107">在本教程中，将了解如何通过利用视图母版页，为应用程序中的多个页面创建公共页面布局。</span><span class="sxs-lookup"><span data-stu-id="81719-107">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="81719-108">例如，您可以使用视图母版页来定义两列的页面布局，并为 web 应用程序中的所有页面使用两列布局。</span><span class="sxs-lookup"><span data-stu-id="81719-108">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

## <a name="creating-page-layouts-with-view-master-pages"></a><span data-ttu-id="81719-109">用查看母版页创建页面布局</span><span class="sxs-lookup"><span data-stu-id="81719-109">Creating Page Layouts with View Master Pages</span></span>

<span data-ttu-id="81719-110">在本教程中，将了解如何通过利用视图母版页，为应用程序中的多个页面创建公共页面布局。</span><span class="sxs-lookup"><span data-stu-id="81719-110">In this tutorial, you learn how to create a common page layout for multiple pages in your application by taking advantage of view master pages.</span></span> <span data-ttu-id="81719-111">例如，您可以使用视图母版页来定义两列的页面布局，并为 web 应用程序中的所有页面使用两列布局。</span><span class="sxs-lookup"><span data-stu-id="81719-111">You can use a view master page, for example, to define a two-column page layout and use the two-column layout for all of the pages in your web application.</span></span>

<span data-ttu-id="81719-112">还可以利用 "查看母版页" 在应用程序的多个页面上共享公共内容。</span><span class="sxs-lookup"><span data-stu-id="81719-112">You also can take advantage of view master pages to share common content across multiple pages in your application.</span></span> <span data-ttu-id="81719-113">例如，您可以将您的网站徽标、导航链接和横幅广告置于视图母版页中。</span><span class="sxs-lookup"><span data-stu-id="81719-113">For example, you can place your website logo, navigation links, and banner advertisements in a view master page.</span></span> <span data-ttu-id="81719-114">这样，应用程序中的每个页面都将自动显示此内容。</span><span class="sxs-lookup"><span data-stu-id="81719-114">That way, every page in your application would display this content automatically.</span></span>

<span data-ttu-id="81719-115">在本教程中，您将了解如何创建新的视图母版页，并基于母版页创建新的视图内容页。</span><span class="sxs-lookup"><span data-stu-id="81719-115">In this tutorial, you learn how to create a new view master page and create a new view content page based on the master page.</span></span>

### <a name="creating-a-view-master-page"></a><span data-ttu-id="81719-116">创建视图母版页</span><span class="sxs-lookup"><span data-stu-id="81719-116">Creating a View Master Page</span></span>

<span data-ttu-id="81719-117">首先，让我们创建一个定义两列布局的视图母版页。</span><span class="sxs-lookup"><span data-stu-id="81719-117">Let's start by creating a view master page that defines a two-column layout.</span></span> <span data-ttu-id="81719-118">通过右键单击 Views\Shared 文件夹，选择菜单选项 "**添加"、"新建项**"，然后选择 " **mvc 视图母版页**" 模板（请参阅图1），可将新的视图母版页添加到 mvc 项目。</span><span class="sxs-lookup"><span data-stu-id="81719-118">You add a new view master page to an MVC project by right-clicking the Views\Shared folder, selecting the menu option **Add, New Item**, and selecting the **MVC View Master Page** template (see Figure 1).</span></span>

<span data-ttu-id="81719-119">[添加视图母版页 ![](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="81719-119">[![Adding a view master page](creating-page-layouts-with-view-master-pages-cs/_static/image2.png)](creating-page-layouts-with-view-master-pages-cs/_static/image1.png)</span></span>

<span data-ttu-id="81719-120">**图 01**：添加视图母版页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="81719-120">**Figure 01**: Adding a view master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image3.png))</span></span>

<span data-ttu-id="81719-121">您可以在一个应用程序中创建多个视图母版页。</span><span class="sxs-lookup"><span data-stu-id="81719-121">You can create more than one view master page in an application.</span></span> <span data-ttu-id="81719-122">每个视图母版页都可以定义不同的页面布局。</span><span class="sxs-lookup"><span data-stu-id="81719-122">Each view master page can define a different page layout.</span></span> <span data-ttu-id="81719-123">例如，您可能希望某些页面具有两列布局，而其他页面具有三列布局。</span><span class="sxs-lookup"><span data-stu-id="81719-123">For example, you might want certain pages to have a two-column layout and other pages to have a three-column layout.</span></span>

<span data-ttu-id="81719-124">视图母版页的外观非常类似于标准的 ASP.NET MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="81719-124">A view master page looks very much like a standard ASP.NET MVC view.</span></span> <span data-ttu-id="81719-125">但与普通视图不同，视图母版页包含一个或多个 `<asp:ContentPlaceHolder>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-125">However, unlike a normal view, a view master page contains one or more `<asp:ContentPlaceHolder>` tags.</span></span> <span data-ttu-id="81719-126">`<contentplaceholder>` 标记用于标记可以在单个内容页中重写的母版页区域。</span><span class="sxs-lookup"><span data-stu-id="81719-126">The `<contentplaceholder>` tags are used to mark the areas of the master page that can be overridden in an individual content page.</span></span>

<span data-ttu-id="81719-127">例如，列表1中的 "视图" 母版页定义一个两列的布局。</span><span class="sxs-lookup"><span data-stu-id="81719-127">For example, the view master page in Listing 1 defines a two-column layout.</span></span> <span data-ttu-id="81719-128">它包含两个 `<contentplaceholder>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-128">It contains two `<contentplaceholder>` tags.</span></span> <span data-ttu-id="81719-129">每个列一个 `<ContentPlaceHolder>`。</span><span class="sxs-lookup"><span data-stu-id="81719-129">One `<ContentPlaceHolder>` for each column.</span></span>

<span data-ttu-id="81719-130">**列表1– `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="81719-130">**Listing 1 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample1.aspx)]

<span data-ttu-id="81719-131">列表1中的 "视图" 母版页的主体包含两个对应于两个列的 `<div>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-131">The body of the view master page in Listing 1 contains two `<div>` tags that correspond to the two columns.</span></span> <span data-ttu-id="81719-132">级联样式表列类可应用于这两个 `<div>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-132">The Cascading Style Sheet column class is applied to both `<div>` tags.</span></span> <span data-ttu-id="81719-133">此类是在母版页顶部声明的样式表中定义的。</span><span class="sxs-lookup"><span data-stu-id="81719-133">This class is defined in the style sheet declared at the top of the master page.</span></span> <span data-ttu-id="81719-134">可以通过切换到设计视图预览视图母版页的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="81719-134">You can preview how the view master page will be rendered by switching to Design view.</span></span> <span data-ttu-id="81719-135">单击源代码编辑器左下角的 "设计" 选项卡（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="81719-135">Click the Design tab at the bottom-left of the source code editor (see Figure 2).</span></span>

<span data-ttu-id="81719-136">[在设计器中预览母版页 ![](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="81719-136">[![Previewing a master page in the designer](creating-page-layouts-with-view-master-pages-cs/_static/image5.png)](creating-page-layouts-with-view-master-pages-cs/_static/image4.png)</span></span>

<span data-ttu-id="81719-137">**图 02**：在设计器中预览母版页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="81719-137">**Figure 02**: Previewing a master page in the designer ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image6.png))</span></span>

### <a name="creating-a-view-content-page"></a><span data-ttu-id="81719-138">创建视图内容页</span><span class="sxs-lookup"><span data-stu-id="81719-138">Creating a View Content Page</span></span>

<span data-ttu-id="81719-139">创建视图母版页后，可以创建一个或多个基于视图母版页的视图内容页。</span><span class="sxs-lookup"><span data-stu-id="81719-139">After you create a view master page, you can create one or more view content pages based on the view master page.</span></span> <span data-ttu-id="81719-140">例如，您可以通过右键单击 Views\Home 文件夹，选择 "**添加"、"新建项**"，选择 " **MVC 视图内容页**" 模板，输入名称 ""，然后单击 "**添加**" 按钮（见图3），为 Home 控制器创建索引视图内容页。</span><span class="sxs-lookup"><span data-stu-id="81719-140">For example, you can create an Index view content page for the Home controller by right-clicking the Views\Home folder, selecting **Add, New Item**, selecting the **MVC View Content Page** template, entering the name Index.aspx, and clicking the **Add** button (see Figure 3).</span></span>

<span data-ttu-id="81719-141">[![添加视图内容页](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="81719-141">[![Adding a view content page](creating-page-layouts-with-view-master-pages-cs/_static/image8.png)](creating-page-layouts-with-view-master-pages-cs/_static/image7.png)</span></span>

<span data-ttu-id="81719-142">**图 03**：添加视图内容页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-cs/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="81719-142">**Figure 03**: Adding a view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image9.png))</span></span>

<span data-ttu-id="81719-143">单击 "添加" 按钮后，将出现一个新对话框，您可以在其中选择要与 "查看内容" 页关联的视图母版页（参见图4）。</span><span class="sxs-lookup"><span data-stu-id="81719-143">After you click the Add button, a new dialog appears that enables you to select a view master page to associate with the view content page (see Figure 4).</span></span> <span data-ttu-id="81719-144">你可以导航到在上一部分中创建的 "母版视图" 母版页。</span><span class="sxs-lookup"><span data-stu-id="81719-144">You can navigate to the Site.master view master page that we created in the previous section.</span></span>

<span data-ttu-id="81719-145">[![选择母版页](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="81719-145">[![Selecting a master page](creating-page-layouts-with-view-master-pages-cs/_static/image11.png)](creating-page-layouts-with-view-master-pages-cs/_static/image10.png)</span></span>

<span data-ttu-id="81719-146">**图 04**：选择一个母版页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="81719-146">**Figure 04**: Selecting a master page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image12.png))</span></span>

<span data-ttu-id="81719-147">基于网站母版页创建新的视图内容页后，将获取列表2中的文件。</span><span class="sxs-lookup"><span data-stu-id="81719-147">After you create a new view content page based on the Site.master master page, you get the file in Listing 2.</span></span>

<span data-ttu-id="81719-148">**列表2– `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="81719-148">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample2.aspx)]

<span data-ttu-id="81719-149">请注意，此视图包含与 "查看母版页" 中每个 `<asp:ContentPlaceHolder>` 标记对应的 `<asp:Content>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-149">Notice that this view contains a `<asp:Content>` tag that corresponds to each of the `<asp:ContentPlaceHolder>` tags in the view master page.</span></span> <span data-ttu-id="81719-150">每个 `<asp:Content>` 标记都包含一个 ContentPlaceHolderID 属性，该属性指向其重写的特定 `<asp:ContentPlaceHolder>`。</span><span class="sxs-lookup"><span data-stu-id="81719-150">Each `<asp:Content>` tag includes a ContentPlaceHolderID attribute that points to the particular `<asp:ContentPlaceHolder>` that it overrides.</span></span>

<span data-ttu-id="81719-151">此外，请注意，列表2中的内容视图页面不包含任何正常的打开和关闭 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-151">Notice, furthermore, that the content view page in Listing 2 does not contain any of the normal opening and closing HTML tags.</span></span> <span data-ttu-id="81719-152">例如，它不包含开始和关闭 `<html>` 或 `<head>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-152">For example, it does not contain the opening and closing `<html>` or `<head>` tags.</span></span> <span data-ttu-id="81719-153">所有正常的开始标记和结束标记都包含在 "视图" 母版页中。</span><span class="sxs-lookup"><span data-stu-id="81719-153">All of the normal opening and closing tags are contained in the view master page.</span></span>

<span data-ttu-id="81719-154">您要在 "视图内容" 页中显示的任何内容都必须放置在 `<asp:Content>` 标记中。</span><span class="sxs-lookup"><span data-stu-id="81719-154">Any content that you want to display in a view content page must be placed within a `<asp:Content>` tag.</span></span> <span data-ttu-id="81719-155">如果将任何 HTML 或其他内容放置在这些标记之外，则在您尝试查看该页面时，您将收到错误消息。</span><span class="sxs-lookup"><span data-stu-id="81719-155">If you place any HTML or other content outside of these tags, then you will get an error when you attempt to view the page.</span></span>

<span data-ttu-id="81719-156">您无需覆盖内容视图页面中母版页的每个 `<asp:ContentPlaceHolder>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-156">You don't need to override every `<asp:ContentPlaceHolder>` tag from a master page in a content view page.</span></span> <span data-ttu-id="81719-157">仅当要将标记替换为特定内容时，才需要覆盖 `<asp:ContentPlaceHolder>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-157">You only need to override a `<asp:ContentPlaceHolder>` tag when you want to replace the tag with particular content.</span></span>

<span data-ttu-id="81719-158">例如，列表3中修改的索引视图仅包含两个 `<asp:Content>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-158">For example, the modified Index view in Listing 3 contains only two `<asp:Content>` tags.</span></span> <span data-ttu-id="81719-159">每个 `<asp:Content>` 标记都包含一些文本。</span><span class="sxs-lookup"><span data-stu-id="81719-159">Each of the `<asp:Content>` tags includes some text.</span></span>

<span data-ttu-id="81719-160">**列表 3-`Views\Home\Index.aspx (modified)`**</span><span class="sxs-lookup"><span data-stu-id="81719-160">**Listing 3 – `Views\Home\Index.aspx (modified)`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample3.aspx)]

<span data-ttu-id="81719-161">当请求列表3中的视图时，它将呈现图5中的页面。</span><span class="sxs-lookup"><span data-stu-id="81719-161">When the view in Listing 3 is requested, it renders the page in Figure 5.</span></span> <span data-ttu-id="81719-162">请注意，视图呈现了包含两个列的页。</span><span class="sxs-lookup"><span data-stu-id="81719-162">Notice that the view renders a page with two columns.</span></span> <span data-ttu-id="81719-163">此外，请注意，"查看内容" 页中的内容与 "视图" 母版页中的内容合并</span><span class="sxs-lookup"><span data-stu-id="81719-163">Notice, furthermore, that the content from the view content page is merged with the content from the view master page</span></span>

<span data-ttu-id="81719-164">[!["索引视图内容" 页](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="81719-164">[![The Index view content page](creating-page-layouts-with-view-master-pages-cs/_static/image14.png)](creating-page-layouts-with-view-master-pages-cs/_static/image13.png)</span></span>

<span data-ttu-id="81719-165">**图 05**：索引视图内容页（[单击以查看完全大小的图像](creating-page-layouts-with-view-master-pages-cs/_static/image15.png)）</span><span class="sxs-lookup"><span data-stu-id="81719-165">**Figure 05**: The Index view content page ([Click to view full-size image](creating-page-layouts-with-view-master-pages-cs/_static/image15.png))</span></span>

### <a name="modifying-view-master-page-content"></a><span data-ttu-id="81719-166">修改视图母版页内容</span><span class="sxs-lookup"><span data-stu-id="81719-166">Modifying View Master Page Content</span></span>

<span data-ttu-id="81719-167">与查看母版页一起使用时，几乎立即遇到的一个问题是在请求不同的视图内容页时修改视图母版页内容的问题。</span><span class="sxs-lookup"><span data-stu-id="81719-167">One issue that you encounter almost immediately when working with view master pages is the problem of modifying view master page content when different view content pages are requested.</span></span> <span data-ttu-id="81719-168">例如，你希望你的 web 应用程序中的每个页面都具有唯一的标题。</span><span class="sxs-lookup"><span data-stu-id="81719-168">For example, you want each page in your web application to have a unique title.</span></span> <span data-ttu-id="81719-169">但是，该标题在 "视图" 母版页中声明，而不是在 "查看内容" 页中声明。</span><span class="sxs-lookup"><span data-stu-id="81719-169">However, the title is declared in the view master page and not in the view content page.</span></span> <span data-ttu-id="81719-170">那么，如何为每个视图内容页自定义页面标题呢？</span><span class="sxs-lookup"><span data-stu-id="81719-170">So, how do you customize the page title for each view content page?</span></span>

<span data-ttu-id="81719-171">可以通过两种方式来修改视图内容页显示的标题。</span><span class="sxs-lookup"><span data-stu-id="81719-171">There are two ways that you can modify the title displayed by a view content page.</span></span> <span data-ttu-id="81719-172">首先，可以将页面标题分配给在视图内容页顶部声明的 `<%@ page %>` 指令的 title 属性。</span><span class="sxs-lookup"><span data-stu-id="81719-172">First, you can assign a page title to the title attribute of the `<%@ page %>` directive declared at the top of a view content page.</span></span> <span data-ttu-id="81719-173">例如，如果要将页标题 "超级优秀网站" 分配给索引视图，则可以在索引视图的顶部包含以下指令：</span><span class="sxs-lookup"><span data-stu-id="81719-173">For example, if you want to assign the page title "Super Great Website" to the Index view, then you can include the following directive at the top of the Index view:</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample4.aspx)]

<span data-ttu-id="81719-174">当向浏览器呈现索引视图时，所需标题会显示在浏览器标题栏中：</span><span class="sxs-lookup"><span data-stu-id="81719-174">When the Index view is rendered to the browser, the desired title appears in the browser title bar:</span></span>

<span data-ttu-id="81719-175">[![浏览器标题栏](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="81719-175">[![Browser title bar](creating-page-layouts-with-view-master-pages-cs/_static/image17.png)](creating-page-layouts-with-view-master-pages-cs/_static/image16.png)</span></span>

<span data-ttu-id="81719-176">若要使 title 属性正常工作，必须满足主视图页面的一项重要要求。</span><span class="sxs-lookup"><span data-stu-id="81719-176">There is one important requirement that a master view page must satisfy in order for the title attribute to work.</span></span> <span data-ttu-id="81719-177">"视图" 母版页必须包含 `<head runat="server">` 标记，而不是其标题的常规 `<head>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-177">The view master page must contain a `<head runat="server">` tag instead of a normal `<head>` tag for its header.</span></span> <span data-ttu-id="81719-178">如果 `<head>` 标记不包括 runat = "server" 属性，则不会显示标题。</span><span class="sxs-lookup"><span data-stu-id="81719-178">If the `<head>` tag does not include the runat="server" attribute then the title won't appear.</span></span> <span data-ttu-id="81719-179">默认视图母版页包含所需的 `<head runat="server">` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-179">The default view master page includes the required `<head runat="server">` tag.</span></span>

<span data-ttu-id="81719-180">修改单独视图内容页中的母版页内容的另一种方法是在 `<asp:ContentPlaceHolder>` 标记中包装要修改的区域。</span><span class="sxs-lookup"><span data-stu-id="81719-180">An alternative approach to modifying master page content from an individual view content page is to wrap the region that you want to modify in a `<asp:ContentPlaceHolder>` tag.</span></span> <span data-ttu-id="81719-181">例如，假设您不仅要更改标题，还需要更改由主视图页面呈现的元标记。</span><span class="sxs-lookup"><span data-stu-id="81719-181">For example, imagine that you want to change not only the title, but also the meta tags, rendered by a master view page.</span></span> <span data-ttu-id="81719-182">列表4中的母版视图页面在其 `<head>` 标记内包含一个 `<asp:ContentPlaceHolder>` 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-182">The master view page in Listing 4 contains a `<asp:ContentPlaceHolder>` tag within its `<head>` tag.</span></span>

<span data-ttu-id="81719-183">**列表 4-`Views\Shared\Site2.master`**</span><span class="sxs-lookup"><span data-stu-id="81719-183">**Listing 4 – `Views\Shared\Site2.master`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample5.aspx)]

<span data-ttu-id="81719-184">请注意，列表4中的 `<asp:ContentPlaceHolder>` 标记包含默认内容：默认标题和默认 meta 标记。</span><span class="sxs-lookup"><span data-stu-id="81719-184">Notice that the `<asp:ContentPlaceHolder>` tag in Listing 4 includes default content: a default title and default meta tags.</span></span> <span data-ttu-id="81719-185">如果在单个视图内容页中不覆盖此 `<asp:ContentPlaceHolder>` 标记，则将显示默认内容。</span><span class="sxs-lookup"><span data-stu-id="81719-185">If you don't override this `<asp:ContentPlaceHolder>` tag in an individual view content page, then the default content will be displayed.</span></span>

<span data-ttu-id="81719-186">列表5中的内容视图页面会重写 `<asp:ContentPlaceHolder>` 标记，以便显示自定义标题和自定义元标记。</span><span class="sxs-lookup"><span data-stu-id="81719-186">The content view page in Listing 5 overrides the `<asp:ContentPlaceHolder>` tag in order to display a custom title and custom meta tags.</span></span>

<span data-ttu-id="81719-187">**列表5– `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="81719-187">**Listing 5 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-page-layouts-with-view-master-pages-cs/samples/sample6.aspx)]

### <a name="summary"></a><span data-ttu-id="81719-188">摘要</span><span class="sxs-lookup"><span data-stu-id="81719-188">Summary</span></span>

<span data-ttu-id="81719-189">本教程提供了查看母版页和查看内容页的基本简介。</span><span class="sxs-lookup"><span data-stu-id="81719-189">This tutorial provided you with a basic introduction to view master pages and view content pages.</span></span> <span data-ttu-id="81719-190">已了解如何创建新的视图母版页，并基于这些页面创建视图内容页。</span><span class="sxs-lookup"><span data-stu-id="81719-190">You learned how to create new view master pages and create view content pages based on them.</span></span> <span data-ttu-id="81719-191">还介绍了如何从特定的视图内容页修改视图母版页的内容。</span><span class="sxs-lookup"><span data-stu-id="81719-191">We also examined how you can modify the content of a view master page from a particular view content page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="81719-192">[上一页](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
> [下一页](passing-data-to-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="81719-192">[Previous](using-the-tagbuilder-class-to-build-html-helpers-cs.md)
[Next](passing-data-to-view-master-pages-cs.md)</span></span>
