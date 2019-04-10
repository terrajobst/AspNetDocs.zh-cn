---
uid: web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
title: 为移动设备呈现 ASP.NET Web Pages (Razor) 站点 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在将相应地呈现在移动设备的 ASP.NET Web Pages (Razor) 站点中创建页面。 你将学习：您如何...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: f15ab392-c05e-4269-83bf-7c6d2b8c8ec8
msc.legacyurl: /web-pages/overview/mobile/rendering-aspnet-web-pages-sites-for-mobile-devices
msc.type: authoredcontent
ms.openlocfilehash: dbcd25331387f8606343e551302bc3ed1f9b2c25
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59379503"
---
# <a name="rendering-aspnet-web-pages-razor-sites-for-mobile-devices"></a><span data-ttu-id="8f9b5-104">为移动设备呈现 ASP.NET Web Pages (Razor) 站点</span><span class="sxs-lookup"><span data-stu-id="8f9b5-104">Rendering ASP.NET Web Pages (Razor) Sites for Mobile Devices</span></span>

<span data-ttu-id="8f9b5-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8f9b5-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8f9b5-106">本文介绍如何在将相应地呈现在移动设备的 ASP.NET Web Pages (Razor) 站点中创建页面。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-106">This article describes how to create pages in an ASP.NET Web Pages (Razor) site that will render appropriately on mobile devices.</span></span>
> 
> <span data-ttu-id="8f9b5-107">你将学习：</span><span class="sxs-lookup"><span data-stu-id="8f9b5-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="8f9b5-108">如何使用命名约定指定页专为移动设备。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-108">How to use a naming convention to specify that a page is designed specifically for mobile devices.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8f9b5-109">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="8f9b5-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="8f9b5-110">ASP.NET 网页 (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="8f9b5-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="8f9b5-111">本教程还适用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>


<span data-ttu-id="8f9b5-112">ASP.NET Web Pages 中，可以移动或其他设备上创建自定义呈现内容的显示。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-112">ASP.NET Web Pages lets you create custom displays for rendering content on mobile or other devices.</span></span>

<span data-ttu-id="8f9b5-113">在 ASP.NET Web Pages 站点中创建特定于设备的页面的最简单方法是使用此类文件命名模式：*FileName.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="8f9b5-113">The simplest way to create device-specific page in an ASP.NET Web Pages site is by using a file-naming pattern like this: *FileName.Mobile.cshtml*.</span></span> <span data-ttu-id="8f9b5-114">可以创建两个版本的页面 (例如，一个名为*MyFile.cshtml*另一个名为*MyFile.Mobile.cshtml*)。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-114">You can create two versions of a page (for example, one named *MyFile.cshtml* and one named *MyFile.Mobile.cshtml*).</span></span> <span data-ttu-id="8f9b5-115">在运行的时，移动设备的请求时*MyFile.cshtml*，ASP.NET 将从内容呈现*MyFile.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-115">At run time, when a mobile device requests *MyFile.cshtml*, ASP.NET renders the content from *MyFile.Mobile.cshtml*.</span></span> <span data-ttu-id="8f9b5-116">否则为*MyFile.cshtml*呈现。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-116">Otherwise, *MyFile.cshtml* is rendered.</span></span>

<span data-ttu-id="8f9b5-117">下面的示例演示如何通过添加内容页的移动设备启用移动呈现。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-117">The following example shows how to enable mobile rendering by adding a content page for mobile devices.</span></span> <span data-ttu-id="8f9b5-118">*Page1.cshtml*包含内容，以及导航侧边栏。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-118">*Page1.cshtml* contains content plus a navigation sidebar.</span></span> <span data-ttu-id="8f9b5-119">*Page1.Mobile.cshtml*包含相同的内容，但省略侧栏。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-119">*Page1.Mobile.cshtml* contains the same content, but omits the sidebar.</span></span>

1. <span data-ttu-id="8f9b5-120">在 ASP.NET Web Pages 站点中，创建名为的文件*Page1.cshtml*和当前的内容替换为以下标记。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-120">In an ASP.NET Web Pages site, create a file named *Page1.cshtml* and replace the current content with following markup.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample1.html)]
2. <span data-ttu-id="8f9b5-121">创建名为的文件*Page1.Mobile.cshtml*和现有内容替换为以下标记。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-121">Create a file named *Page1.Mobile.cshtml* and replace the existing content with the following markup.</span></span> <span data-ttu-id="8f9b5-122">请注意，页上的移动版本省略以便更好地呈现在较小屏幕上的导航部分。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-122">Notice that the mobile version of the page omits the navigation section for better rendering on a smaller screen.</span></span>

    [!code-html[Main](rendering-aspnet-web-pages-sites-for-mobile-devices/samples/sample2.html)]
3. <span data-ttu-id="8f9b5-123">运行桌面浏览器并浏览到*Page1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-123">Run a desktop browser and browse to *Page1.cshtml*.</span></span> ![mobilesites-1](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image1.png)
4. <span data-ttu-id="8f9b5-125">运行移动浏览器 （或移动设备仿真程序） 并浏览到*Page1.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-125">Run a mobile browser (or a mobile device emulator) and browse to *Page1.cshtml*.</span></span> <span data-ttu-id="8f9b5-126">(请注意，不包括 *.mobile。*</span><span class="sxs-lookup"><span data-stu-id="8f9b5-126">(Notice that you do not include *.mobile.*</span></span> <span data-ttu-id="8f9b5-127">作为 URL 的一部分。）即使该请求是对*Page1.cshtml*，ASP.NET 会将*Page1.Mobile.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-127">as part of the URL.) Even though the request is to *Page1.cshtml*, ASP.NET renders *Page1.Mobile.cshtml*.</span></span>

    ![mobilesites-2](rendering-aspnet-web-pages-sites-for-mobile-devices/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="8f9b5-129">若要测试移动页面，可以使用在桌面计算机运行的移动设备模拟器。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-129">To test mobile pages, you can use a mobile device simulator that runs on a desktop computer.</span></span> <span data-ttu-id="8f9b5-130">此工具允许您测试网页，如他们的移动设备上的外观 （即，通常使用小得多显示区域）。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-130">This tool lets you test web pages as they would look on mobile devices (that is, typically with a much smaller display area).</span></span> <span data-ttu-id="8f9b5-131">模拟器的一个示例是[用户代理切换器外接程序](http://addons.mozilla.org/firefox/addon/user-agent-switcher/)Mozilla firefox，它可以模拟各种移动浏览器，从桌面版本的 Firefox。</span><span class="sxs-lookup"><span data-stu-id="8f9b5-131">One example of a simulator is the [User Agent Switcher add-on](http://addons.mozilla.org/firefox/addon/user-agent-switcher/) for Mozilla Firefox, which lets you emulate various mobile browsers from a desktop version of Firefox.</span></span>


<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="8f9b5-132">其他资源</span><span class="sxs-lookup"><span data-stu-id="8f9b5-132">Additional Resources</span></span>


[<span data-ttu-id="8f9b5-133">Windows Phone 仿真程序</span><span class="sxs-lookup"><span data-stu-id="8f9b5-133">Windows Phone Emulator</span></span>](https://msdn.microsoft.com/library/ff402563(v=VS.92).aspx)
