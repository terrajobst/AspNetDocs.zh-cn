---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: 在 ASP.NET 网页（Razor）网站中创建一致的布局 |Microsoft Docs
author: Rick-Anderson
description: 为了更高效地为网站创建网页，你可以为网站创建可重用的内容块（如页眉和页脚），并且你可以创建
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 3f63ce68ae4c13970ac0df196167ace0b22b592c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509096"
---
# <a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="58e0f-103">在 ASP.NET 网页（Razor）网站中创建一致的布局</span><span class="sxs-lookup"><span data-stu-id="58e0f-103">Creating a Consistent Layout in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="58e0f-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="58e0f-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="58e0f-105">本文介绍如何在 ASP.NET 网页（Razor）网站中使用布局页来创建可重用的内容块（如页眉和页脚），并为站点中的所有页面创建一致的外观。</span><span class="sxs-lookup"><span data-stu-id="58e0f-105">This article explains how you can use layout pages in an ASP.NET Web Pages (Razor) website to create reusable blocks of content (like headers and footers) and to create a consistent look for all the pages in the site.</span></span>
> 
> <span data-ttu-id="58e0f-106">**你将学习的内容：**</span><span class="sxs-lookup"><span data-stu-id="58e0f-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="58e0f-107">如何创建可重用的内容块，如页眉和页脚。</span><span class="sxs-lookup"><span data-stu-id="58e0f-107">How to create reusable blocks of content like headers and footers.</span></span>
> - <span data-ttu-id="58e0f-108">如何使用布局为站点中的所有页面创建一致的外观。</span><span class="sxs-lookup"><span data-stu-id="58e0f-108">How to create a consistent look for all the pages in your site using a layout.</span></span>
> - <span data-ttu-id="58e0f-109">如何在运行时将数据传递到布局页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-109">How to pass data at run time to a layout page.</span></span>
> 
> <span data-ttu-id="58e0f-110">下面是本文中介绍的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="58e0f-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="58e0f-111">内容块：包含要插入到多页中的 HTML 格式内容的文件。</span><span class="sxs-lookup"><span data-stu-id="58e0f-111">Content blocks, which are files that contain HTML-formatted content to be inserted in multiple pages.</span></span>
> - <span data-ttu-id="58e0f-112">布局页，页面包含可由网站上的页面共享的 HTML 格式的内容。</span><span class="sxs-lookup"><span data-stu-id="58e0f-112">Layout pages, which are pages that contain HTML-formatted content that can be shared by pages on the website.</span></span>
> - <span data-ttu-id="58e0f-113">`RenderPage`、`RenderBody`和 `RenderSection` 方法，这些方法告诉 ASP.NET 在何处插入页面元素。</span><span class="sxs-lookup"><span data-stu-id="58e0f-113">The `RenderPage`, `RenderBody`, and `RenderSection` methods, which tell ASP.NET where to insert page elements.</span></span>
> - <span data-ttu-id="58e0f-114">`PageData` 字典，可用于在内容块和布局页之间共享数据。</span><span class="sxs-lookup"><span data-stu-id="58e0f-114">The `PageData` dictionary that lets you share data between content blocks and layout pages.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="58e0f-115">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="58e0f-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="58e0f-116">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="58e0f-116">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="58e0f-117">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="58e0f-117">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-layout-pages"></a><span data-ttu-id="58e0f-118">关于布局页</span><span class="sxs-lookup"><span data-stu-id="58e0f-118">About Layout Pages</span></span>

<span data-ttu-id="58e0f-119">许多网站具有显示在每个页面上的内容，如页眉和页脚，或指示用户登录用户的框。</span><span class="sxs-lookup"><span data-stu-id="58e0f-119">Many websites have content that's displayed on every page, like a header and footer, or a box that tells users that they're logged in.</span></span> <span data-ttu-id="58e0f-120">使用 ASP.NET 可以创建一个包含文本、标记和代码的单独文件，就像常规网页一样。</span><span class="sxs-lookup"><span data-stu-id="58e0f-120">ASP.NET lets you create a separate file with a content block that can contain text, markup, and code, just like a regular web page.</span></span> <span data-ttu-id="58e0f-121">然后，你可以在要显示信息的站点上的其他页面中插入内容块。</span><span class="sxs-lookup"><span data-stu-id="58e0f-121">You can then insert the content block in other pages on the site where you want the information to appear.</span></span> <span data-ttu-id="58e0f-122">这样就无需将相同的内容复制并粘贴到每个页面。</span><span class="sxs-lookup"><span data-stu-id="58e0f-122">That way you don't have to copy and paste the same content into every page.</span></span> <span data-ttu-id="58e0f-123">创建类似于这样的常用内容还可以更轻松地更新站点。</span><span class="sxs-lookup"><span data-stu-id="58e0f-123">Creating common content like this also makes it easier to update your site.</span></span> <span data-ttu-id="58e0f-124">如果需要更改内容，只需更新单个文件，所做的更改就会反映到内容插入位置。</span><span class="sxs-lookup"><span data-stu-id="58e0f-124">If you need to change the content, you can just update a single file, and the changes are then reflected everywhere the content has been inserted.</span></span>

<span data-ttu-id="58e0f-125">下图显示内容块的工作方式。</span><span class="sxs-lookup"><span data-stu-id="58e0f-125">The following diagram shows how content blocks work.</span></span> <span data-ttu-id="58e0f-126">当浏览器请求 web 服务器中的某个页面时，ASP.NET 会在主页中调用 `RenderPage` 方法的位置插入内容块。</span><span class="sxs-lookup"><span data-stu-id="58e0f-126">When a browser requests a page from the web server, ASP.NET inserts the content blocks at the point where the `RenderPage` method is called in the main page.</span></span> <span data-ttu-id="58e0f-127">然后，将 "完成（合并）" 页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="58e0f-127">The finished (merged) page is then sent to the browser.</span></span>

![显示 RenderPage 方法如何将引用的页插入当前页的概念图。](3-creating-a-consistent-look/_static/image1.jpg)

<span data-ttu-id="58e0f-129">在此过程中，您将创建一个引用位于不同文件中的两个内容块（标头和脚注）的页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-129">In this procedure, you'll create a page that references two content blocks (a header and a footer) that are located in separate files.</span></span> <span data-ttu-id="58e0f-130">你可以在站点中的任何页面上使用这些相同的内容块。</span><span class="sxs-lookup"><span data-stu-id="58e0f-130">You can use these same content blocks in any page in your site.</span></span> <span data-ttu-id="58e0f-131">完成后，会看到如下所示的页面：</span><span class="sxs-lookup"><span data-stu-id="58e0f-131">When you're done, you'll get a page like this:</span></span>

![显示浏览器中的页面的屏幕截图，其中包含对 RenderPage 方法的调用的页面。](3-creating-a-consistent-look/_static/image2.png)

1. <span data-ttu-id="58e0f-133">在网站的根文件夹中，创建一个名为 "*索引*" 的文件。</span><span class="sxs-lookup"><span data-stu-id="58e0f-133">In the root folder of your website, create a file named *Index.cshtml*.</span></span>
2. <span data-ttu-id="58e0f-134">将现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-134">Replace the existing markup with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. <span data-ttu-id="58e0f-135">在根文件夹中，创建一个名为 "*共享*" 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="58e0f-135">In the root folder, create a folder named *Shared*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="58e0f-136">常见的做法是在名为*shared*的文件夹中存储网页间共享的文件。</span><span class="sxs-lookup"><span data-stu-id="58e0f-136">It's common practice to store files that are shared among web pages in a folder named *Shared*.</span></span>
4. <span data-ttu-id="58e0f-137">在*共享*文件夹中，创建一个名为 *\_* 的文件。</span><span class="sxs-lookup"><span data-stu-id="58e0f-137">In the *Shared* folder, create a file named *\_Header.cshtml*.</span></span>
5. <span data-ttu-id="58e0f-138">将所有现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-138">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    <span data-ttu-id="58e0f-139">请注意，文件名是 *\_的标头*，以下划线（\_）作为前缀。</span><span class="sxs-lookup"><span data-stu-id="58e0f-139">Notice that the file name is *\_Header.cshtml*, with an underscore (\_) as a prefix.</span></span> <span data-ttu-id="58e0f-140">如果 ASP.NET 的名称以下划线开头，则不会向浏览器发送页面。</span><span class="sxs-lookup"><span data-stu-id="58e0f-140">ASP.NET won't send a page to the browser if its name starts with an underscore.</span></span> <span data-ttu-id="58e0f-141">这可防止用户直接请求（无意或其他）这些页面。</span><span class="sxs-lookup"><span data-stu-id="58e0f-141">This prevents people from requesting (inadvertently or otherwise) these pages directly.</span></span> <span data-ttu-id="58e0f-142">最好是使用下划线来命名包含内容块的页面，因为您并不想让用户完全请求将这些页面&#8212;完全插入到其他页面。</span><span class="sxs-lookup"><span data-stu-id="58e0f-142">It's a good idea to use an underscore to name pages that have content blocks in them, because you don't really want users to be able to request these pages &#8212; they exist strictly to be inserted into other pages.</span></span>
6. <span data-ttu-id="58e0f-143">在*共享*文件夹中，创建一个名为 *\_页脚*的文件，并将内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-143">In the *Shared* folder, create a file named *\_Footer.cshtml* and replace the content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. <span data-ttu-id="58e0f-144">在 "*索引*" 页上，添加两个对 `RenderPage` 方法的调用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="58e0f-144">In the *Index.cshtml* page, add two calls to the `RenderPage` method, as shown here:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    <span data-ttu-id="58e0f-145">这说明了如何将内容块插入到网页中。</span><span class="sxs-lookup"><span data-stu-id="58e0f-145">This shows how to insert a content block into a web page.</span></span> <span data-ttu-id="58e0f-146">调用 `RenderPage` 方法，并向其传递要在该点插入其内容的文件的名称。</span><span class="sxs-lookup"><span data-stu-id="58e0f-146">You call the `RenderPage` method and pass it the name of the file whose contents you want to insert at that point.</span></span> <span data-ttu-id="58e0f-147">此时，您要将\_的标\_*头*的内容插入到 *索引的 cshtml*文件中。</span><span class="sxs-lookup"><span data-stu-id="58e0f-147">Here, you're inserting the contents of the *\_Header.cshtml* and *\_Footer.cshtml* files into the *Index.cshtml* file.</span></span>
8. <span data-ttu-id="58e0f-148">在浏览器中运行 "*索引*" 页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-148">Run the *Index.cshtml* page in a browser.</span></span> <span data-ttu-id="58e0f-149">（在 WebMatrix 中，在 "**文件**" 工作区中，右键单击该文件，然后选择 "**在浏览器中启动**"。）</span><span class="sxs-lookup"><span data-stu-id="58e0f-149">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.)</span></span>
9. <span data-ttu-id="58e0f-150">在浏览器中查看页面源。</span><span class="sxs-lookup"><span data-stu-id="58e0f-150">In the browser, view the page source.</span></span> <span data-ttu-id="58e0f-151">（例如，在 Internet Explorer 中，右键单击该页面，然后单击 "**查看源**"。）</span><span class="sxs-lookup"><span data-stu-id="58e0f-151">(For example, in Internet Explorer, right-click the page and then click **View Source**.)</span></span>

    <span data-ttu-id="58e0f-152">这使你可以查看发送到浏览器的网页标记，该标记将索引页标记与内容块合并在一起。</span><span class="sxs-lookup"><span data-stu-id="58e0f-152">This lets you see the web page markup that's sent to the browser, which combines the index page markup with the content blocks.</span></span> <span data-ttu-id="58e0f-153">下面的示例显示了为*索引.*</span><span class="sxs-lookup"><span data-stu-id="58e0f-153">The following example shows the page source that's rendered for *Index.cshtml*.</span></span> <span data-ttu-id="58e0f-154">对插入到*Index*中的 `RenderPage` 的调用已替换为页眉和页脚文件的实际内容。</span><span class="sxs-lookup"><span data-stu-id="58e0f-154">The calls to `RenderPage` that you inserted into *Index.cshtml* have been replaced with the actual contents of the header and footer files.</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a><span data-ttu-id="58e0f-155">使用布局页创建一致的外观</span><span class="sxs-lookup"><span data-stu-id="58e0f-155">Creating a Consistent Look Using Layout Pages</span></span>

<span data-ttu-id="58e0f-156">到目前为止，您已经了解到，在多个页面上包含相同的内容是很容易的。</span><span class="sxs-lookup"><span data-stu-id="58e0f-156">So far you've seen that it's easy to include the same content on multiple pages.</span></span> <span data-ttu-id="58e0f-157">若要为站点创建一致的外观，一种更结构化的方法是使用布局页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-157">A more structured approach to creating a consistent look for a site is to use layout pages.</span></span> <span data-ttu-id="58e0f-158">布局页定义网页的结构，但不包含任何实际内容。</span><span class="sxs-lookup"><span data-stu-id="58e0f-158">A layout page defines the structure of a web page, but doesn't contain any actual content.</span></span> <span data-ttu-id="58e0f-159">创建布局页后，可以创建包含内容的网页，然后将其链接到 "布局" 页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-159">After you've created a layout page, you can create web pages that contain the content and then link them to the layout page.</span></span> <span data-ttu-id="58e0f-160">显示这些页面后，将根据布局页面设置这些页面的格式。</span><span class="sxs-lookup"><span data-stu-id="58e0f-160">When these pages are displayed, they'll be formatted according to the layout page.</span></span> <span data-ttu-id="58e0f-161">（在这种意义上，布局页充当其他页中定义的内容的一种模板。）</span><span class="sxs-lookup"><span data-stu-id="58e0f-161">(In this sense, a layout page acts as a kind of template for content that's defined in other pages.)</span></span>

<span data-ttu-id="58e0f-162">布局页与任何 HTML 页面一样，只是它包含对 `RenderBody` 方法的调用。</span><span class="sxs-lookup"><span data-stu-id="58e0f-162">The layout page is just like any HTML page, except that it contains a call to the `RenderBody` method.</span></span> <span data-ttu-id="58e0f-163">"布局" 页中 `RenderBody` 方法的位置确定将包含内容页中信息的位置。</span><span class="sxs-lookup"><span data-stu-id="58e0f-163">The position of the `RenderBody` method in the layout page determines where the information from the content page will be included.</span></span>

<span data-ttu-id="58e0f-164">下图显示如何在运行时组合内容页和布局页以生成已完成的网页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-164">The following diagram shows how content pages and layout pages are combined at run time to produce the finished web page.</span></span> <span data-ttu-id="58e0f-165">浏览器请求内容页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-165">The browser requests a content page.</span></span> <span data-ttu-id="58e0f-166">"内容" 页中有代码，它指定要用于页结构的布局页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-166">The content page has code in it that specifies the layout page to use for the page's structure.</span></span> <span data-ttu-id="58e0f-167">在布局页中，将在调用 `RenderBody` 方法的位置插入内容。</span><span class="sxs-lookup"><span data-stu-id="58e0f-167">In the layout page, the content is inserted at the point where the `RenderBody` method is called.</span></span> <span data-ttu-id="58e0f-168">还可以通过调用 `RenderPage` 方法（在上一节中的方式）将内容块插入到布局页中。</span><span class="sxs-lookup"><span data-stu-id="58e0f-168">Content blocks can also be inserted into the layout page by calling the `RenderPage` method, the way you did in the previous section.</span></span> <span data-ttu-id="58e0f-169">网页完成后，将发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="58e0f-169">When the web page is complete, it's sent to the browser.</span></span>

![显示浏览器中的页面的屏幕截图，其中包含对 RenderBody 方法的调用的页面。](3-creating-a-consistent-look/_static/image3.jpg)

<span data-ttu-id="58e0f-171">下面的过程演示如何创建布局页并将内容页链接到它。</span><span class="sxs-lookup"><span data-stu-id="58e0f-171">The following procedure shows how to create a layout page and link content pages to it.</span></span>

1. <span data-ttu-id="58e0f-172">在网站的*共享*文件夹中，创建一个名为 *\_Layout1*的文件。</span><span class="sxs-lookup"><span data-stu-id="58e0f-172">In the *Shared* folder of your website, create a file named *\_Layout1.cshtml*.</span></span>
2. <span data-ttu-id="58e0f-173">将所有现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-173">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    <span data-ttu-id="58e0f-174">您可以在布局页中使用 `RenderPage` 方法来插入内容块。</span><span class="sxs-lookup"><span data-stu-id="58e0f-174">You use the `RenderPage` method in a layout page to insert content blocks.</span></span> <span data-ttu-id="58e0f-175">布局页只能包含对 `RenderBody` 方法的一次调用。</span><span class="sxs-lookup"><span data-stu-id="58e0f-175">A layout page can contain only one call to the `RenderBody` method.</span></span>
3. <span data-ttu-id="58e0f-176">在*共享*文件夹中，创建一个名为 *\_.header2*的文件，并将所有现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-176">In the *Shared* folder, create a file named *\_Header2.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. <span data-ttu-id="58e0f-177">在根文件夹中，创建一个新文件夹并将其命名为*样式*。</span><span class="sxs-lookup"><span data-stu-id="58e0f-177">In the root folder, create a new folder and name it *Styles*.</span></span>
5. <span data-ttu-id="58e0f-178">在 "*样式*" 文件夹中，创建名为 " *web.config* " 的文件并添加以下样式定义：</span><span class="sxs-lookup"><span data-stu-id="58e0f-178">In the *Styles* folder, create a file named *Site.css* and add the following style definitions:</span></span>

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    <span data-ttu-id="58e0f-179">此处的样式定义仅用于显示样式表如何与布局页一起使用。</span><span class="sxs-lookup"><span data-stu-id="58e0f-179">These style definitions are here only to show how style sheets can be used with layout pages.</span></span> <span data-ttu-id="58e0f-180">如果需要，可以为这些元素定义自己的样式。</span><span class="sxs-lookup"><span data-stu-id="58e0f-180">If you want, you can define your own styles for these elements.</span></span>
6. <span data-ttu-id="58e0f-181">在根文件夹中，创建一个名为*Content1*的文件，并将所有现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-181">In the root folder, create a file named *Content1.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    <span data-ttu-id="58e0f-182">这是将使用布局页的页面。</span><span class="sxs-lookup"><span data-stu-id="58e0f-182">This is a page that will use a layout page.</span></span> <span data-ttu-id="58e0f-183">页面顶部的代码块指示用于设置此内容格式的布局页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-183">The code block at the top of the page indicates which layout page to use to format this content.</span></span>
7. <span data-ttu-id="58e0f-184">在浏览器中运行*Content1* 。</span><span class="sxs-lookup"><span data-stu-id="58e0f-184">Run *Content1.cshtml* in a browser.</span></span> <span data-ttu-id="58e0f-185">呈现的页使用 *\_Layout1*中定义的格式和样式表，以及在*Content1*中定义的文本（内容）。</span><span class="sxs-lookup"><span data-stu-id="58e0f-185">The rendered page uses the format and style sheet defined in *\_Layout1.cshtml* and the text (content) defined in *Content1.cshtml*.</span></span>

    ![[图像]](3-creating-a-consistent-look/_static/image4.png)

    <span data-ttu-id="58e0f-187">您可以重复步骤6来创建可以共享同一布局页的其他内容页面。</span><span class="sxs-lookup"><span data-stu-id="58e0f-187">You can repeat step 6 to create additional content pages that can then share the same layout page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="58e0f-188">你可以设置站点，以便可以为文件夹中的所有内容页自动使用相同的布局页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-188">You can set up your site so that you can automatically use the same layout page for all the content pages in a folder.</span></span> <span data-ttu-id="58e0f-189">有关详细信息，请参阅为[ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906)。</span><span class="sxs-lookup"><span data-stu-id="58e0f-189">For details, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906).</span></span>

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a><span data-ttu-id="58e0f-190">设计具有多个内容节的布局页</span><span class="sxs-lookup"><span data-stu-id="58e0f-190">Designing Layout Pages That Have Multiple Content Sections</span></span>

<span data-ttu-id="58e0f-191">内容页可以有多个部分，如果要使用具有可替换内容的多个区域的布局，这会很有用。</span><span class="sxs-lookup"><span data-stu-id="58e0f-191">A content page can have multiple sections, which is useful if you want to use layouts that have multiple areas with replaceable content.</span></span> <span data-ttu-id="58e0f-192">在 "内容" 页中，为每个部分指定唯一名称。</span><span class="sxs-lookup"><span data-stu-id="58e0f-192">In the content page, you give each section a unique name.</span></span> <span data-ttu-id="58e0f-193">（默认节未命名。）在 "布局" 页中，添加一个 `RenderBody` 方法，以指定应显示未命名（默认）节的位置。</span><span class="sxs-lookup"><span data-stu-id="58e0f-193">(The default section is left unnamed.) In the layout page, you add a `RenderBody` method to specify where the unnamed (default) section should appear.</span></span> <span data-ttu-id="58e0f-194">然后，添加单独的 `RenderSection` 方法以便单独呈现命名节。</span><span class="sxs-lookup"><span data-stu-id="58e0f-194">You then add separate `RenderSection` methods in order to render named sections individually.</span></span>

<span data-ttu-id="58e0f-195">下图显示了 ASP.NET 如何处理划分为多个部分的内容。</span><span class="sxs-lookup"><span data-stu-id="58e0f-195">The following diagram shows how ASP.NET handles content that's divided into multiple sections.</span></span> <span data-ttu-id="58e0f-196">每个命名节包含在内容页的节块中。</span><span class="sxs-lookup"><span data-stu-id="58e0f-196">Each named section is contained in a section block in the content page.</span></span> <span data-ttu-id="58e0f-197">（在示例中，它们被命名为 `Header` 和 `List`。）在调用 `RenderSection` 方法时，框架会将 "内容" 部分插入布局页中。</span><span class="sxs-lookup"><span data-stu-id="58e0f-197">(They're named `Header` and `List` in the example.) The framework inserts content section into the layout page at the point where the `RenderSection` method is called.</span></span> <span data-ttu-id="58e0f-198">如前文所述，将在调用 `RenderBody` 方法的位置插入未命名的（默认）部分。</span><span class="sxs-lookup"><span data-stu-id="58e0f-198">The unnamed (default) section is inserted at the point where the `RenderBody` method is called, as you saw earlier.</span></span>

![显示 RenderSection 方法将引用节插入当前页的方式的概念图。](3-creating-a-consistent-look/_static/image5.jpg)

<span data-ttu-id="58e0f-200">此过程演示如何创建包含多个内容节的内容页，以及如何使用支持多个内容节的布局页呈现该内容页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-200">This procedure shows how to create a content page that has multiple content sections and how to render it using a layout page that supports multiple content sections.</span></span>

1. <span data-ttu-id="58e0f-201">在*共享*文件夹中，创建一个名为 *\_Layout2*的文件。</span><span class="sxs-lookup"><span data-stu-id="58e0f-201">In the *Shared* folder, create a file named *\_Layout2.cshtml*.</span></span>
2. <span data-ttu-id="58e0f-202">将所有现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-202">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    <span data-ttu-id="58e0f-203">使用 `RenderSection` 方法可呈现标头和列表部分。</span><span class="sxs-lookup"><span data-stu-id="58e0f-203">You use the `RenderSection` method to render both the header and list sections.</span></span>
3. <span data-ttu-id="58e0f-204">在根文件夹中，创建一个名为*Content2*的文件，并将所有现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-204">In the root folder, create a file named *Content2.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    <span data-ttu-id="58e0f-205">此内容页在页面顶部包含一个代码块。</span><span class="sxs-lookup"><span data-stu-id="58e0f-205">This content page contains a code block at the top of the page.</span></span> <span data-ttu-id="58e0f-206">每个命名节包含在一个节块中。</span><span class="sxs-lookup"><span data-stu-id="58e0f-206">Each named section is contained in a section block.</span></span> <span data-ttu-id="58e0f-207">页面的其余部分包含默认（未命名）内容部分。</span><span class="sxs-lookup"><span data-stu-id="58e0f-207">The rest of the page contains the default (unnamed) content section.</span></span>
4. <span data-ttu-id="58e0f-208">在浏览器中运行*Content2* 。</span><span class="sxs-lookup"><span data-stu-id="58e0f-208">Run *Content2.cshtml* in a browser.</span></span>

    ![显示浏览器中的页面的屏幕截图，其中包含对 RenderSection 方法的调用的页面。](3-creating-a-consistent-look/_static/image6.png)

## <a name="making-content-sections-optional"></a><span data-ttu-id="58e0f-210">使内容部分可选</span><span class="sxs-lookup"><span data-stu-id="58e0f-210">Making Content Sections Optional</span></span>

<span data-ttu-id="58e0f-211">通常，在内容页中创建的部分必须与布局页中定义的节匹配。</span><span class="sxs-lookup"><span data-stu-id="58e0f-211">Normally, the sections that you create in a content page have to match sections that are defined in the layout page.</span></span> <span data-ttu-id="58e0f-212">如果发生以下任何情况，则会出现错误：</span><span class="sxs-lookup"><span data-stu-id="58e0f-212">You can get errors if any of the following occur:</span></span>

- <span data-ttu-id="58e0f-213">"内容" 页包含没有布局页中对应部分的部分。</span><span class="sxs-lookup"><span data-stu-id="58e0f-213">The content page contains a section that has no corresponding section in the layout page.</span></span>
- <span data-ttu-id="58e0f-214">"布局" 页包含没有内容的部分。</span><span class="sxs-lookup"><span data-stu-id="58e0f-214">The layout page contains a section for which there's no content.</span></span>
- <span data-ttu-id="58e0f-215">布局页包含尝试多次呈现同一节的方法调用。</span><span class="sxs-lookup"><span data-stu-id="58e0f-215">The layout page includes method calls that try to render the same section more than once.</span></span>

<span data-ttu-id="58e0f-216">但是，您可以通过在布局页中将节声明为可选，来覆盖命名部分的此行为。</span><span class="sxs-lookup"><span data-stu-id="58e0f-216">However, you can override this behavior for a named section by declaring the section to be optional in the layout page.</span></span> <span data-ttu-id="58e0f-217">这允许您定义多个内容页，这些内容页可以共享布局页，但对于特定部分可能有也可能没有内容。</span><span class="sxs-lookup"><span data-stu-id="58e0f-217">This lets you define multiple content pages that can share a layout page but that might or might not have content for a specific section.</span></span>

1. <span data-ttu-id="58e0f-218">打开*Content2*并删除以下部分：</span><span class="sxs-lookup"><span data-stu-id="58e0f-218">Open *Content2.cshtml* and remove the following section:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. <span data-ttu-id="58e0f-219">保存该页，然后在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="58e0f-219">Save the page and then run it in a browser.</span></span> <span data-ttu-id="58e0f-220">将显示一条错误消息，因为内容页不提供布局页中定义的节的内容，即页眉节。</span><span class="sxs-lookup"><span data-stu-id="58e0f-220">An error message is displayed, because the content page doesn't provide content for a section defined in the layout page, namely the header section.</span></span>

    ![屏幕截图，显示在运行调用 RenderSection 方法但未提供相应部分的页面时发生的错误。](3-creating-a-consistent-look/_static/image7.png)
3. <span data-ttu-id="58e0f-222">在*共享*文件夹中，打开 *\_Layout2* "页面并替换以下行：</span><span class="sxs-lookup"><span data-stu-id="58e0f-222">In the *Shared* folder, open the *\_Layout2.cshtml* page and replace this line:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    <span data-ttu-id="58e0f-223">替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="58e0f-223">with the following code:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    <span data-ttu-id="58e0f-224">作为替代方法，您可以将之前的代码行替换为以下代码块，这会产生相同的结果：</span><span class="sxs-lookup"><span data-stu-id="58e0f-224">As an alternative, you could replace the previous line of code with the following code block, which produces the same results:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. <span data-ttu-id="58e0f-225">再次在浏览器中运行*Content2*页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-225">Run the *Content2.cshtml* page in a browser again.</span></span> <span data-ttu-id="58e0f-226">（如果你仍在浏览器中打开此页，则可以只刷新它。）这一次，即使该页没有标头，也不会显示任何错误。</span><span class="sxs-lookup"><span data-stu-id="58e0f-226">(If you still have this page open in the browser, you can just refresh it.) This time the page is displayed with no error, even though it has no header.</span></span>

## <a name="passing-data-to-layout-pages"></a><span data-ttu-id="58e0f-227">将数据传递到布局页</span><span class="sxs-lookup"><span data-stu-id="58e0f-227">Passing Data to Layout Pages</span></span>

<span data-ttu-id="58e0f-228">你可能在 "内容" 页中定义了在布局页中需要引用的数据。</span><span class="sxs-lookup"><span data-stu-id="58e0f-228">You might have data defined in the content page that you need to refer to in a layout page.</span></span> <span data-ttu-id="58e0f-229">如果是这样，则需要将数据从 "内容" 页传递到 "布局" 页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-229">If so, you need to pass the data from the content page to the layout page.</span></span> <span data-ttu-id="58e0f-230">例如，你可能想要显示用户的登录状态，或者可能想要基于用户输入显示或隐藏内容区域。</span><span class="sxs-lookup"><span data-stu-id="58e0f-230">For example, you might want to display the login status of a user, or you might want to show or hide content areas based on user input.</span></span>

<span data-ttu-id="58e0f-231">若要将数据从内容页传递到布局页，可以将值放入内容页的 `PageData` 属性。</span><span class="sxs-lookup"><span data-stu-id="58e0f-231">To pass data from a content page to a layout page, you can put values into the `PageData` property of the content page.</span></span> <span data-ttu-id="58e0f-232">`PageData` 属性是名称/值对的集合，这些名称/值对保存你要在页面间传递的数据。</span><span class="sxs-lookup"><span data-stu-id="58e0f-232">The `PageData` property is a collection of name/value pairs that hold the data that you want to pass between pages.</span></span> <span data-ttu-id="58e0f-233">然后，您可以在 "布局" 页中读取 `PageData` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="58e0f-233">In the layout page, you can then read values out of the `PageData` property.</span></span>

<span data-ttu-id="58e0f-234">下面是另一个关系图。</span><span class="sxs-lookup"><span data-stu-id="58e0f-234">Here's another diagram.</span></span> <span data-ttu-id="58e0f-235">这会显示 ASP.NET 如何使用 `PageData` 属性将值从内容页传递到布局页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-235">This one shows how ASP.NET can use the `PageData` property to pass values from a content page to the layout page.</span></span> <span data-ttu-id="58e0f-236">当 ASP.NET 开始生成网页时，它将创建 `PageData` 集合。</span><span class="sxs-lookup"><span data-stu-id="58e0f-236">When ASP.NET begins building the web page, it creates the `PageData` collection.</span></span> <span data-ttu-id="58e0f-237">在 "内容" 页中，你将编写用于将数据放入 `PageData` 集合中的代码。</span><span class="sxs-lookup"><span data-stu-id="58e0f-237">In the content page, you write code to put data in the `PageData` collection.</span></span> <span data-ttu-id="58e0f-238">"内容" 页或其他内容块中的其他部分也可以访问 `PageData` 集合中的值。</span><span class="sxs-lookup"><span data-stu-id="58e0f-238">Values in the `PageData` collection can also be accessed by other sections in the content page or by additional content blocks.</span></span>

![显示内容页如何填充 PageData 字典并将该信息传递到布局页的概念图。](3-creating-a-consistent-look/_static/image8.jpg)

<span data-ttu-id="58e0f-240">下面的过程演示如何将数据从内容页传递到布局页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-240">The following procedure shows how to pass data from a content page to a layout page.</span></span> <span data-ttu-id="58e0f-241">当页面运行时，它会显示一个按钮，使用户可以隐藏或显示在布局页面中定义的列表。</span><span class="sxs-lookup"><span data-stu-id="58e0f-241">When the page runs, it displays a button that lets the user hide or show a list that's defined in the layout page.</span></span> <span data-ttu-id="58e0f-242">当用户单击该按钮时，它会在 "`PageData`" 属性中设置 true/false （布尔值）值。</span><span class="sxs-lookup"><span data-stu-id="58e0f-242">When users click the button, it sets a true/false (Boolean) value in the `PageData` property.</span></span> <span data-ttu-id="58e0f-243">布局页读取该值，如果该值为 false，则隐藏列表。</span><span class="sxs-lookup"><span data-stu-id="58e0f-243">The layout page reads that value, and if it's false, hides the list.</span></span> <span data-ttu-id="58e0f-244">还可以在 "内容" 页中使用该值来确定是否显示 "**隐藏列表**" 按钮或 "**显示列表**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="58e0f-244">The value is also used in the content page to determine whether to display the **Hide List** button or the **Show List** button.</span></span>

![[图像]](3-creating-a-consistent-look/_static/image9.jpg)

1. <span data-ttu-id="58e0f-246">在根文件夹中，创建一个名为*Content3*的文件，并将所有现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-246">In the root folder, create a file named *Content3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    <span data-ttu-id="58e0f-247">该代码将两个数据片段存储在 "`PageData` &#8212; " 属性 "网页标题" 和 "true" 或 "false" 以指定是否显示列表。</span><span class="sxs-lookup"><span data-stu-id="58e0f-247">The code stores two pieces of data in the `PageData` property &#8212; the title of the web page and true or false to specify whether to display a list.</span></span>

    <span data-ttu-id="58e0f-248">请注意，ASP.NET 允许你使用代码块有条件地将 HTML 标记放入页面。</span><span class="sxs-lookup"><span data-stu-id="58e0f-248">Notice that ASP.NET lets you put HTML markup into the page conditionally using a code block.</span></span> <span data-ttu-id="58e0f-249">例如，页体中的 `if/else` 块决定显示哪一窗体，具体取决于 `PageData["ShowList"]` 是否设置为 true。</span><span class="sxs-lookup"><span data-stu-id="58e0f-249">For example, the `if/else` block in the body of the page determines which form to display depending on whether `PageData["ShowList"]` is set to true.</span></span>
2. <span data-ttu-id="58e0f-250">在*共享*文件夹中，创建一个名为 *\_Layout3*的文件，并将所有现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-250">In the *Shared* folder, create a file named *\_Layout3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    <span data-ttu-id="58e0f-251">布局页在 `<title>` 元素中包含一个表达式，该表达式可获取 `PageData` 属性的标题值。</span><span class="sxs-lookup"><span data-stu-id="58e0f-251">The layout page includes an expression in the `<title>` element that gets the title value from the `PageData` property.</span></span> <span data-ttu-id="58e0f-252">它还使用 `PageData` 属性的 `ShowList` 值来确定是否显示列表内容块。</span><span class="sxs-lookup"><span data-stu-id="58e0f-252">It also uses the `ShowList` value of the `PageData` property to determine whether to display the list content block.</span></span>
3. <span data-ttu-id="58e0f-253">在*共享*文件夹中，创建一个名为 *\_* 的文件，并将所有现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="58e0f-253">In the *Shared* folder, create a file named *\_List.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. <span data-ttu-id="58e0f-254">在浏览器中运行*Content3*页。</span><span class="sxs-lookup"><span data-stu-id="58e0f-254">Run the *Content3.cshtml* page in a browser.</span></span> <span data-ttu-id="58e0f-255">此时将显示该页，其中的列表显示在该页的左侧，**隐藏列表**按钮位于底部。</span><span class="sxs-lookup"><span data-stu-id="58e0f-255">The page is displayed with the list visible on the left side of the page and a **Hide List** button at the bottom.</span></span>

    ![屏幕截图，显示包含列表的页面和一个显示 "隐藏列表" 的按钮。](3-creating-a-consistent-look/_static/image10.png)
5. <span data-ttu-id="58e0f-257">单击 "**隐藏列表**"。</span><span class="sxs-lookup"><span data-stu-id="58e0f-257">Click **Hide List**.</span></span> <span data-ttu-id="58e0f-258">列表消失，按钮会变为 "**显示列表**"。</span><span class="sxs-lookup"><span data-stu-id="58e0f-258">The list disappears and the button changes to **Show List**.</span></span>

    ![显示页的屏幕截图，其中不包含列表和显示 "显示列表" 的按钮。](3-creating-a-consistent-look/_static/image11.png)
6. <span data-ttu-id="58e0f-260">单击 "**显示列表**" 按钮，然后重新显示列表。</span><span class="sxs-lookup"><span data-stu-id="58e0f-260">Click the **Show List** button, and the list is displayed again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="58e0f-261">其他资源</span><span class="sxs-lookup"><span data-stu-id="58e0f-261">Additional Resources</span></span>

[<span data-ttu-id="58e0f-262">为 ASP.NET 网页自定义站点范围的行为</span><span class="sxs-lookup"><span data-stu-id="58e0f-262">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
