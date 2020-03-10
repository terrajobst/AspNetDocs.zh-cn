---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: 在 ASP.NET 网页（Razor）站点中显示地图 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何基于必应、Google、Ma 提供的映射服务，在 ASP.NET 网页（Razor）网站的页面上显示交互式地图。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518720"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="f3179-103">在 ASP.NET 网页（Razor）站点中显示地图</span><span class="sxs-lookup"><span data-stu-id="f3179-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="f3179-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f3179-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f3179-105">本文介绍如何基于必应、Google、MapQuest 和 Yahoo 提供的映射服务，在 ASP.NET 网页（Razor）网站中的页面上显示交互式地图。</span><span class="sxs-lookup"><span data-stu-id="f3179-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="f3179-106">学习内容：</span><span class="sxs-lookup"><span data-stu-id="f3179-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f3179-107">如何生成基于地址的映射。</span><span class="sxs-lookup"><span data-stu-id="f3179-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="f3179-108">如何基于纬度和经度坐标生成地图。</span><span class="sxs-lookup"><span data-stu-id="f3179-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="f3179-109">如何注册必应地图开发人员帐户并获取用于 Bing 地图的密钥。</span><span class="sxs-lookup"><span data-stu-id="f3179-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="f3179-110">这是本文中介绍的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="f3179-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="f3179-111">`Maps` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="f3179-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f3179-112">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="f3179-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f3179-113">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="f3179-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="f3179-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="f3179-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="f3179-115">本教程还适用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="f3179-115">This tutorial also works with WebMatrix 3.</span></span>

<span data-ttu-id="f3179-116">在网页中，可以使用 `Maps` 帮助程序在页面上显示地图。</span><span class="sxs-lookup"><span data-stu-id="f3179-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="f3179-117">您可以基于一个地址或一组经度和纬度坐标生成地图。</span><span class="sxs-lookup"><span data-stu-id="f3179-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="f3179-118">利用 `Maps` 类，您可以调入常用的地图引擎，包括必应、Google、MapQuest 和 Yahoo。</span><span class="sxs-lookup"><span data-stu-id="f3179-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="f3179-119">无论调用哪个映射引擎，添加到页的映射的步骤都是相同的。</span><span class="sxs-lookup"><span data-stu-id="f3179-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="f3179-120">你只需添加一个 JavaScript 文件引用，该引用使可用方法显示映射，然后调用 `Maps` 帮助器的方法。</span><span class="sxs-lookup"><span data-stu-id="f3179-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="f3179-121">根据所使用的 `Maps` 帮助器方法选择映射服务。</span><span class="sxs-lookup"><span data-stu-id="f3179-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="f3179-122">可以使用以下任一操作：</span><span class="sxs-lookup"><span data-stu-id="f3179-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="f3179-123">安装所需的组件</span><span class="sxs-lookup"><span data-stu-id="f3179-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="f3179-124">若要显示地图，需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="f3179-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="f3179-125">`Maps` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="f3179-125">The `Maps` helper.</span></span> <span data-ttu-id="f3179-126">此帮助程序位于 ASP.NET Web 帮助程序库的第2版中。</span><span class="sxs-lookup"><span data-stu-id="f3179-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="f3179-127">如果尚未添加库，则可以将其作为 NuGet 包安装在站点中。</span><span class="sxs-lookup"><span data-stu-id="f3179-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="f3179-128">有关详细信息，请参阅[在 ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)。</span><span class="sxs-lookup"><span data-stu-id="f3179-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="f3179-129">（在库中，搜索 `microsoft-web-helpers` 包。）</span><span class="sxs-lookup"><span data-stu-id="f3179-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="f3179-130">JQuery 库。</span><span class="sxs-lookup"><span data-stu-id="f3179-130">The jQuery library.</span></span> <span data-ttu-id="f3179-131">一些 WebMatrix 站点模板已在其*脚本*文件夹中包含 jQuery 库。</span><span class="sxs-lookup"><span data-stu-id="f3179-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="f3179-132">如果你没有这些库，则可以直接从[jQuery.org](http://jQuery.org)网站下载最新 jQuery library。</span><span class="sxs-lookup"><span data-stu-id="f3179-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="f3179-133">或者，你可以使用模板创建新站点（例如，"**入门网站**" 模板），然后将该站点中的 jQuery 文件复制到当前站点。</span><span class="sxs-lookup"><span data-stu-id="f3179-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="f3179-134">最后，如果要使用 Bing 地图，必须首先创建一个（免费）帐户并获取一个密钥。</span><span class="sxs-lookup"><span data-stu-id="f3179-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="f3179-135">若要获取密钥，请执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="f3179-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="f3179-136">在[Bing Maps 开发人员帐户](https://www.microsoft.com/maps/developers/web.aspx)上创建帐户。</span><span class="sxs-lookup"><span data-stu-id="f3179-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="f3179-137">还必须有 Microsoft 帐户（Windows Live ID）。</span><span class="sxs-lookup"><span data-stu-id="f3179-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="f3179-138">可以指定要使用密钥进行**评估/测试**。</span><span class="sxs-lookup"><span data-stu-id="f3179-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="f3179-139">如果你使用 WebMatrix 和 IIS Express 在你自己的计算机上测试 mapping 函数，请在 "**站点**" 工作区中，记下站点的 URL （例如，`http://localhost:50408`，尽管你的端口号可能会不同）。</span><span class="sxs-lookup"><span data-stu-id="f3179-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="f3179-140">注册时，可以使用此*localhost*地址作为站点。</span><span class="sxs-lookup"><span data-stu-id="f3179-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="f3179-141">注册帐户后，请前往 Bing 地图帐户中心，并单击 "**创建" 或 "查看密钥**"：</span><span class="sxs-lookup"><span data-stu-id="f3179-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![映射-2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="f3179-143">记录必应创建的密钥。</span><span class="sxs-lookup"><span data-stu-id="f3179-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="f3179-144">基于地址创建地图（使用 Google）</span><span class="sxs-lookup"><span data-stu-id="f3179-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="f3179-145">下面的示例演示如何创建基于地址呈现地图的页面。</span><span class="sxs-lookup"><span data-stu-id="f3179-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="f3179-146">此示例演示如何使用 Google Maps。</span><span class="sxs-lookup"><span data-stu-id="f3179-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="f3179-147">在站点的根目录中创建一个名为 MapAddress 的文件 *。*</span><span class="sxs-lookup"><span data-stu-id="f3179-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="f3179-148">此页将根据您传递给它的地址生成一个映射。</span><span class="sxs-lookup"><span data-stu-id="f3179-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="f3179-149">将以下代码复制到文件中，并覆盖现有内容。</span><span class="sxs-lookup"><span data-stu-id="f3179-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="f3179-150">请注意页面的以下功能：</span><span class="sxs-lookup"><span data-stu-id="f3179-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="f3179-151">`<head>` 元素中的 `<script>` 元素。</span><span class="sxs-lookup"><span data-stu-id="f3179-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="f3179-152">在此示例中，`<script>` 元素引用 */selfservice/scripts/jquery-1.10.2.min.js 1.6.4*文件，这是 jquery library 版本1.6.4 的缩小（压缩）版本。</span><span class="sxs-lookup"><span data-stu-id="f3179-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="f3179-153">请注意，该引用假设 *.js*文件位于您的网站的*Scripts*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="f3179-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="f3179-154">如果使用的是不同版本的 jQuery library，只需确保正确指向该版本即可。</span><span class="sxs-lookup"><span data-stu-id="f3179-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="f3179-155">对页面正文中的 `@Maps.GetGoogleHtml` 的调用。</span><span class="sxs-lookup"><span data-stu-id="f3179-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="f3179-156">若要映射地址，必须传递地址字符串。</span><span class="sxs-lookup"><span data-stu-id="f3179-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="f3179-157">其他地图引擎的方法的工作方式类似（`@Maps.GetYahooHtml`、`@Maps.GetMapQuestHtml`）。</span><span class="sxs-lookup"><span data-stu-id="f3179-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="f3179-158">运行该页并输入地址。</span><span class="sxs-lookup"><span data-stu-id="f3179-158">Run the page and enter an address.</span></span> <span data-ttu-id="f3179-159">页面将显示一个基于 Google Maps 的地图，其中显示指定的位置。</span><span class="sxs-lookup"><span data-stu-id="f3179-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![映射-1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="f3179-161">基于纬度和经度坐标创建地图（使用必应）</span><span class="sxs-lookup"><span data-stu-id="f3179-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="f3179-162">此示例演示如何基于坐标创建地图。</span><span class="sxs-lookup"><span data-stu-id="f3179-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="f3179-163">此示例演示如何使用 Bing 地图以及如何包含必应关键字。</span><span class="sxs-lookup"><span data-stu-id="f3179-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="f3179-164">（也可以在不使用必应密钥的情况下，基于使用其他地图引擎的坐标创建地图。）</span><span class="sxs-lookup"><span data-stu-id="f3179-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="f3179-165">在站点的根目录中创建一个名为*MapCoordinates*的文件，并将现有内容替换为以下代码和标记：</span><span class="sxs-lookup"><span data-stu-id="f3179-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="f3179-166">将 `your-key-here` 替换为之前生成的 Bing 地图密钥。</span><span class="sxs-lookup"><span data-stu-id="f3179-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="f3179-167">运行*MapCoordinates*页，输入纬度和经度坐标，然后单击**地图！**</span><span class="sxs-lookup"><span data-stu-id="f3179-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="f3179-168">按钮。</span><span class="sxs-lookup"><span data-stu-id="f3179-168">button.</span></span> <span data-ttu-id="f3179-169">（如果您不知道任何坐标，请尝试以下。</span><span class="sxs-lookup"><span data-stu-id="f3179-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="f3179-170">这是 Microsoft Redmond 校园的位置。）</span><span class="sxs-lookup"><span data-stu-id="f3179-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="f3179-171">纬度：47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="f3179-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="f3179-172">经度：-122.158317565918</span><span class="sxs-lookup"><span data-stu-id="f3179-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="f3179-173">该页使用您指定的坐标来显示。</span><span class="sxs-lookup"><span data-stu-id="f3179-173">The page is displayed using the coordinates that you specified.</span></span>

     ![映射-3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="f3179-175">其他资源</span><span class="sxs-lookup"><span data-stu-id="f3179-175">Additional Resources</span></span>

[<span data-ttu-id="f3179-176">Microsoft Maps API 参考</span><span class="sxs-lookup"><span data-stu-id="f3179-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)
