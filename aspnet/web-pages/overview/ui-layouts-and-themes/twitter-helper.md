---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: ASP.NET 网页的 Twitter 帮助程序 |Microsoft Docs
author: Rick-Anderson
description: 本主题和应用程序演示如何向 WebMatrix 3 项目添加 Twitter 帮助程序。 它包含 Twitter 帮助程序代码，并演示如何调用帮助器 。
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518618"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a><span data-ttu-id="91b50-104">ASP.NET 网页的 Twitter 帮助程序</span><span class="sxs-lookup"><span data-stu-id="91b50-104">Twitter Helper with ASP.NET Web Pages</span></span>

<span data-ttu-id="91b50-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="91b50-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91b50-106">Twitter 帮助程序已过时。</span><span class="sxs-lookup"><span data-stu-id="91b50-106">Twitter Helpers are obsolete.</span></span> <span data-ttu-id="91b50-107">对于 Twitter 最新的网站参与工具，请参阅[twitter For 网站概述](https://developer.twitter.com/en/docs/twitter-for-websites/overview)。</span><span class="sxs-lookup"><span data-stu-id="91b50-107">For Twitter's latest engagement tools for websites, see [Twitter for Websites Overview](https://developer.twitter.com/en/docs/twitter-for-websites/overview).</span></span>

> <span data-ttu-id="91b50-108">本主题和应用程序演示如何向 WebMatrix 3 项目添加 Twitter 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="91b50-108">This topic and application show how to add a Twitter Helper to your WebMatrix 3 project.</span></span> <span data-ttu-id="91b50-109">它包含 Twitter 帮助程序代码，并演示如何调用帮助程序方法。</span><span class="sxs-lookup"><span data-stu-id="91b50-109">It contains the Twitter Helper code and shows how to call the helper methods.</span></span>
> 
> <span data-ttu-id="91b50-110">Twitter 文件的此代码由 Microsoft 的**Tian Pan**开发。</span><span class="sxs-lookup"><span data-stu-id="91b50-110">This code for the Twitter.cshtml file was developed by **Tian Pan** of Microsoft.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="91b50-111">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="91b50-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="91b50-112">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="91b50-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="91b50-113">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="91b50-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="introduction"></a><span data-ttu-id="91b50-114">简介</span><span class="sxs-lookup"><span data-stu-id="91b50-114">Introduction</span></span>

<span data-ttu-id="91b50-115">本主题演示如何将 Twitter 帮助程序添加到应用程序，并使用 Razor 语法调用帮助程序方法。</span><span class="sxs-lookup"><span data-stu-id="91b50-115">This topic demonstrates how to add a Twitter Helper to your application and use Razor syntax to call the helper methods.</span></span> <span data-ttu-id="91b50-116">Twitter 帮助器使你可以轻松地在应用程序中包含 Twitter 按钮和小组件。</span><span class="sxs-lookup"><span data-stu-id="91b50-116">The Twitter Helper makes it easy to incorporate Twitter buttons and widgets in your application.</span></span> <span data-ttu-id="91b50-117">若要使用 Twitter 小组件（例如用户的时间线或井号标签的搜索结果），必须先[在 Twitter 上创建该小组件](https://twitter.com/settings/widgets)。</span><span class="sxs-lookup"><span data-stu-id="91b50-117">To use a Twitter widget, such as a user's timeline or the search results for a hashtag, you must first create the [widget on Twitter](https://twitter.com/settings/widgets).</span></span> <span data-ttu-id="91b50-118">创建小组件后，将收到小组件 id。调用显示小组件的帮助器方法时，可以将此小组件 id 作为参数传递。</span><span class="sxs-lookup"><span data-stu-id="91b50-118">After creating your widget, you will receive a widget id. You pass this widget id as a parameter when calling the helper methods that show widget.</span></span>

<span data-ttu-id="91b50-119">本主题是针对 Twitter API 版本1.1 编写的。</span><span class="sxs-lookup"><span data-stu-id="91b50-119">This topic was written for version 1.1 of the Twitter API.</span></span> <span data-ttu-id="91b50-120">通过直接将 Twitter 帮助程序代码添加到你的项目，你可以在 Twitter API 发生更改时更新帮助器代码。</span><span class="sxs-lookup"><span data-stu-id="91b50-120">By directly adding the Twitter Helper code to your project, you can update the helper code if the Twitter API changes.</span></span>

<span data-ttu-id="91b50-121">有关安装 WebMatrix 的信息，请参阅[ASP.NET 网页 2-入门简介](../getting-started/introducing-aspnet-web-pages-2/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="91b50-121">For information about installing WebMatrix, see [Introducing ASP.NET Web Pages 2 - Getting Started](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).</span></span>

## <a name="add-twitter-helper-to-your-project"></a><span data-ttu-id="91b50-122">将 Twitter 帮助程序添加到项目</span><span class="sxs-lookup"><span data-stu-id="91b50-122">Add Twitter Helper to your project</span></span>

<span data-ttu-id="91b50-123">若要添加 Twitter 帮助程序，请首先向项目中添加一个名为 "**应用\_代码**" 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="91b50-123">To add the Twitter Helper, first, add a folder named **App\_Code** to your project.</span></span> <span data-ttu-id="91b50-124">然后，创建一个名为**Twitter**的文件。</span><span class="sxs-lookup"><span data-stu-id="91b50-124">Then, create a file named **Twitter.cshtml**.</span></span>

![App_Code 文件夹](twitter-helper/_static/image1.png)

<span data-ttu-id="91b50-126">将 Twitter 中的默认代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="91b50-126">Replace the default code in Twitter.cshtml with the following code.</span></span>

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a><span data-ttu-id="91b50-127">从网页调用 Twitter 方法</span><span class="sxs-lookup"><span data-stu-id="91b50-127">Call Twitter methods from your web pages</span></span>

<span data-ttu-id="91b50-128">下面的示例演示如何在项目的页中使用 Twitter 帮助器方法。</span><span class="sxs-lookup"><span data-stu-id="91b50-128">The following example shows how to use the Twitter Helper methods from a page in your project.</span></span> <span data-ttu-id="91b50-129">在您的项目中，您将需要将参数值替换为与您的需求相关的值。</span><span class="sxs-lookup"><span data-stu-id="91b50-129">In your project, you will want to replace the parameter values with values that are relevant to your needs.</span></span> <span data-ttu-id="91b50-130">您可以使用提供的小组件 id 来浏览这些方法的工作方式，但您需要为您的项目生成您自己的小组件。</span><span class="sxs-lookup"><span data-stu-id="91b50-130">You can use the provided widget ids to explore how the methods work, but you will want to generate your own widgets for your project.</span></span>

<span data-ttu-id="91b50-131">并非下面显示的所有参数都是必需的。</span><span class="sxs-lookup"><span data-stu-id="91b50-131">Not all of the parameters shown below are required.</span></span> <span data-ttu-id="91b50-132">可选参数用于自定义按钮或小组件的显示方式。</span><span class="sxs-lookup"><span data-stu-id="91b50-132">The optional parameters are used to customize how the button or widget is displayed.</span></span> <span data-ttu-id="91b50-133">例如，"关注" 按钮只要求按用户名，但该示例显示如何包含关注者的数量，以及如何指定按钮的大小和语言。</span><span class="sxs-lookup"><span data-stu-id="91b50-133">For example, the Follow Button only requires the user name to follow, but the example shows how to include the number of followers, and how specify the size of the button and the language.</span></span>

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a><span data-ttu-id="91b50-134">查看结果</span><span class="sxs-lookup"><span data-stu-id="91b50-134">See the results</span></span>

<span data-ttu-id="91b50-135">上面的代码生成以下按钮和小组件。</span><span class="sxs-lookup"><span data-stu-id="91b50-135">The above code produces the following buttons and widgets.</span></span> <span data-ttu-id="91b50-136">这些按钮和小组件是功能齐全的，而不是屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="91b50-136">These buttons and widgets are fully-functional, not screenshots.</span></span> <span data-ttu-id="91b50-137">"关注" 按钮以西班牙语显示，因为 language 参数设置为**es**。</span><span class="sxs-lookup"><span data-stu-id="91b50-137">The Follow Button is displayed in Spanish because the language parameter was set to **es**.</span></span>

### <a name="follow-button"></a><span data-ttu-id="91b50-138">跟随按钮</span><span class="sxs-lookup"><span data-stu-id="91b50-138">Follow Button</span></span>

<span data-ttu-id="91b50-139">[遵循 @aspnet）](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="91b50-139">[Follow @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="tweet-button"></a><span data-ttu-id="91b50-140">推文按钮</span><span class="sxs-lookup"><span data-stu-id="91b50-140">Tweet Button</span></span>

<span data-ttu-id="91b50-141">[推文](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span><span class="sxs-lookup"><span data-stu-id="91b50-141">[Tweet](https://twitter.com/share)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`</span></span>

### <a name="user-timeline-profile"></a><span data-ttu-id="91b50-142">用户时间线（配置文件）</span><span class="sxs-lookup"><span data-stu-id="91b50-142">User Timeline (Profile)</span></span>

<span data-ttu-id="91b50-143">[推文 @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="91b50-143">[Tweets by @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="favorites"></a><span data-ttu-id="91b50-144">收藏夹</span><span class="sxs-lookup"><span data-stu-id="91b50-144">Favorites</span></span>

<span data-ttu-id="91b50-145">[@Microsoft`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>` 收藏的推文](https://twitter.com/Microsoft/favorites)</span><span class="sxs-lookup"><span data-stu-id="91b50-145">[Favorite Tweets by @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="list"></a><span data-ttu-id="91b50-146">列表</span><span class="sxs-lookup"><span data-stu-id="91b50-146">List</span></span>

<span data-ttu-id="91b50-147">[来自 @Microsoft/MS\_使用者\_波段的推文](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="91b50-147">[Tweets from @Microsoft/MS\_Consumer\_Bands](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>

### <a name="search"></a><span data-ttu-id="91b50-148">搜索</span><span class="sxs-lookup"><span data-stu-id="91b50-148">Search</span></span>

<span data-ttu-id="91b50-149">[有关 .net&quot;&quot;#asp 的推文](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span><span class="sxs-lookup"><span data-stu-id="91b50-149">[Tweets about &quot;#asp.net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`</span></span>
