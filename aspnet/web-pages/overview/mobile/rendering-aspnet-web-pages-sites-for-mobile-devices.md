---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 呈现移动设备 ASP.NET 网页（Razor）站点 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET 网页（Razor）站点中创建将在移动设备上正确呈现的页面。 你将学习的内容：操作方法 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: c012348d65e48a275cb0e4808fef2a7f31e5fb33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454352"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="6baea-104">呈现移动设备 ASP.NET 网页（Razor）站点</span><span class="sxs-lookup"><span data-stu-id="6baea-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>

<span data-ttu-id="6baea-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6baea-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6baea-106">本文介绍如何在 ASP.NET 网页（Razor）站点中创建将在移动设备上正确呈现的页面。</span><span class="sxs-lookup"><span data-stu-id="6baea-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="6baea-107">学习内容：</span><span class="sxs-lookup"><span data-stu-id="6baea-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="6baea-108">如何使用命名约定来指定某个页面专门用于移动设备。</span><span class="sxs-lookup"><span data-stu-id="6baea-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6baea-109">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="6baea-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6baea-110">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="6baea-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="6baea-111">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="6baea-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="6baea-112">ASP.NET 网页允许你创建自定义显示以在移动设备或其他设备上呈现内容。</span><span class="sxs-lookup"><span data-stu-id="6baea-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="6baea-113">若要在 ASP.NET 网页站点中创建特定于设备的页面，最简单的方法是使用如下所示的文件命名模式： *FileName。*</span><span class="sxs-lookup"><span data-stu-id="6baea-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.Mobile.cshtml*.</span></span> <span data-ttu-id="6baea-114">你可以创建两个版本的页（例如，一个名为*myfile.txt*的页，一个名为*myfile.txt*）。</span><span class="sxs-lookup"><span data-stu-id="6baea-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="6baea-115">在运行时，当移动设备请求*myfile.txt*时，ASP.NET 将呈现*myfile.txt*中的内容。</span><span class="sxs-lookup"><span data-stu-id="6baea-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="6baea-116">否则，将呈现*myfile.txt* 。</span><span class="sxs-lookup"><span data-stu-id="6baea-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="6baea-117">下面的示例演示如何通过添加移动设备的内容页来启用移动呈现。</span><span class="sxs-lookup"><span data-stu-id="6baea-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="6baea-118">*Page1*包含内容以及导航边栏。</span><span class="sxs-lookup"><span data-stu-id="6baea-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="6baea-119">*Page1*包含相同的内容，但省略了侧栏。</span><span class="sxs-lookup"><span data-stu-id="6baea-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="6baea-120">在 ASP.NET 网页的站点中，创建一个名为 " *Page1* " 的文件，并将当前内容替换为以下标记。</span><span class="sxs-lookup"><span data-stu-id="6baea-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="6baea-121">创建一个名为 " *Page1* " 的文件，并将现有内容替换为以下标记。</span><span class="sxs-lookup"><span data-stu-id="6baea-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="6baea-122">请注意，此页的移动版本省略了导航部分，以便更好地在较小的屏幕上进行呈现。</span><span class="sxs-lookup"><span data-stu-id="6baea-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="6baea-123">运行桌面浏览器并浏览到*Page1*。</span><span class="sxs-lookup"><span data-stu-id="6baea-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="6baea-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="6baea-124">![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)</span></span>
4. <span data-ttu-id="6baea-125">运行移动浏览器（或移动设备模拟器）并浏览到*Page1。*</span><span class="sxs-lookup"><span data-stu-id="6baea-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="6baea-126">（请注意，不包括*mobile。*</span><span class="sxs-lookup"><span data-stu-id="6baea-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="6baea-127">作为 URL 的一部分。）即使请求是*ASP.NET，也*会呈现*page1*。</span><span class="sxs-lookup"><span data-stu-id="6baea-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="6baea-129">若要测试移动页，可以使用在台式计算机上运行的移动设备模拟器。</span><span class="sxs-lookup"><span data-stu-id="6baea-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="6baea-130">使用此工具，您可以像在移动设备上查看网页一样对其进行测试（也就是，显示区域通常更小）。</span><span class="sxs-lookup"><span data-stu-id="6baea-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="6baea-131">模拟器的一个示例是用于 Mozilla Firefox 的[用户代理切换器外接程序](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)，它使你可以从 Firefox 的桌面版本模拟各种移动浏览器。</span><span class="sxs-lookup"><span data-stu-id="6baea-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="6baea-132">其他资源</span><span class="sxs-lookup"><span data-stu-id="6baea-132">Additional Resources</span></span>

<span data-ttu-id="6baea-133">[Windows Phone 模拟器](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span><span class="sxs-lookup"><span data-stu-id="6baea-133">[Windows Phone Emulator](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)</span></span>
