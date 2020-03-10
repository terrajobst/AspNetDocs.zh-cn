---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: 在 ASP.NET 网页（Razor）网站中创建和使用帮助器 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET 网页（Razor）网站中创建帮助程序。 帮助器是一个可重用的组件，其中包含代码和到性能的标记 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454304"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="9b5cd-104">在 ASP.NET 网页（Razor）网站中创建和使用 Helper</span><span class="sxs-lookup"><span data-stu-id="9b5cd-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="9b5cd-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9b5cd-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9b5cd-106">本文介绍如何在 ASP.NET 网页（Razor）网站中创建帮助程序。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="9b5cd-107">*帮助器*是一种可重用的组件，其中包括用于执行可能比较繁琐或复杂的任务的代码和标记。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="9b5cd-108">**你将学习的内容：**</span><span class="sxs-lookup"><span data-stu-id="9b5cd-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="9b5cd-109">如何创建和使用简单的帮助器。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="9b5cd-110">下面是本文中介绍的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="9b5cd-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="9b5cd-111">`@helper` 语法。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="9b5cd-112">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="9b5cd-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="9b5cd-113">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="9b5cd-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="9b5cd-114">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="9b5cd-115">帮助器概述</span><span class="sxs-lookup"><span data-stu-id="9b5cd-115">Overview of Helpers</span></span>

<span data-ttu-id="9b5cd-116">如果需要在站点中的不同页面上执行相同的任务，则可以使用帮助程序。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="9b5cd-117">ASP.NET 网页包括多个帮助程序，你可以下载和安装更多的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="9b5cd-118">（ [ASP.NET API 快速参考](https://go.microsoft.com/fwlink/?LinkId=202907)中列出了 ASP.NET 网页中的内置帮助程序列表。）如果现有的帮助程序都不能满足您的需要，您可以创建自己的帮助程序。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="9b5cd-119">利用帮助程序，可以在多个页中使用通用代码块。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="9b5cd-120">假设你经常需要在页面中创建与普通段落分开设置的注释项。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="9b5cd-121">也许会将便笺创建为样式为带有边框的框的 `<div>` 元素。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="9b5cd-122">您不必在每次要显示便笺时将此同一标记添加到页面，而是可以将标记打包为帮助程序。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="9b5cd-123">然后，你可以在所需的任何位置使用一行代码插入注释。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="9b5cd-124">使用与此类似的帮助程序使每个页面中的代码更简单且更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="9b5cd-125">它还使您可以更轻松地维护站点，因为如果您需要更改便笺的外观，则可以在一个位置更改标记。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="9b5cd-126">创建帮助程序</span><span class="sxs-lookup"><span data-stu-id="9b5cd-126">Creating a Helper</span></span>

<span data-ttu-id="9b5cd-127">此过程说明如何创建创建注释的帮助器，如刚才所述。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="9b5cd-128">这是一个简单的示例，但自定义帮助器可以包含所需的任何标记和 ASP.NET 代码。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="9b5cd-129">在网站的根文件夹中，创建名为 "*应用\_* 的文件夹"。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="9b5cd-130">这是 ASP.NET 中的保留文件夹名称，你可以在其中将代码用于组件（如帮助程序）。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="9b5cd-131">在*应用\_代码*文件夹中，创建一个新的*cshtml*文件并将其命名为*MyHelpers*。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="9b5cd-132">将现有内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="9b5cd-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="9b5cd-133">代码使用 `@helper` 语法来声明名为 `MakeNote`的新帮助器。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="9b5cd-134">此特定帮助器使你可以传递一个名为 `content` 的参数，该参数可以包含文本和标记的组合。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="9b5cd-135">帮助器使用 `@content` 变量将字符串插入到便笺正文中。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="9b5cd-136">请注意，该文件命名为*MyHelpers*，但该帮助程序名为 `MakeNote`。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="9b5cd-137">可以将多个自定义帮助程序放入单个文件中。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="9b5cd-138">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="9b5cd-139">在页面中使用帮助器</span><span class="sxs-lookup"><span data-stu-id="9b5cd-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="9b5cd-140">在根文件夹中，创建名为*TestHelper*的新空白文件。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="9b5cd-141">向文件中添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="9b5cd-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="9b5cd-142">若要调用创建的帮助程序，请使用 `@` 后跟帮助器是的文件名、点，然后是帮助程序名称。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="9b5cd-143">（如果应用中有多个文件夹 *\_代码*文件夹，则可以使用语法 `@FolderName.FileName.HelperName` 在任何嵌套文件夹级别中调用帮助程序）。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="9b5cd-144">在括号内的引号内添加的文本是帮助程序将在网页中作为注释的一部分显示的文本。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="9b5cd-145">保存页面并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="9b5cd-146">帮助器生成注释项权限，在这两个段落之间调用帮助程序：。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![显示浏览器中页的屏幕截图，以及帮助器生成的标记如何在指定文本周围放置一个框。](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="9b5cd-148">其他资源</span><span class="sxs-lookup"><span data-stu-id="9b5cd-148">Additional Resources</span></span>

<span data-ttu-id="9b5cd-149">[作为 Razor helper 的水平菜单](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="9b5cd-150">Mike Pope 的此博客文章演示了如何使用标记、CSS 和代码将水平菜单创建为帮助器。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="9b5cd-151">[在 WebMatrix 和 ASP.NET MVC3 的 ASP.NET 网页帮助程序中利用 HTML5](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="9b5cd-152">Sam Abraham 的此博客条目显示了一个帮助器，用于呈现 HTML5 `Canvas` 元素。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="9b5cd-153">[WebMatrix 中 @Helpers 和 @Functions 之间的差异](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix)。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="9b5cd-154">Mike Brind 的此博客文章介绍 `@helper` 语法和 `@function` 语法，以及何时使用它们。</span><span class="sxs-lookup"><span data-stu-id="9b5cd-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>
