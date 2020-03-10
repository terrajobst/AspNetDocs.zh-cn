---
uid: web-pages/overview/performance-and-traffic/14-analyzing-traffic
title: 跟踪 ASP.NET 网页（Razor）网站的访问者信息（分析） |Microsoft Docs
author: Rick-Anderson
description: 获得网站后，你可能想要分析你的网站流量。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 360bc6e1-84c5-4b8e-a84c-ea48ab807aa4
msc.legacyurl: /web-pages/overview/performance-and-traffic/14-analyzing-traffic
msc.type: authoredcontent
ms.openlocfilehash: 095a5572c755446e0661c052ca9de82d636429fd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421454"
---
# <a name="tracking-visitor-information-analytics-for-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="6d991-103">跟踪 ASP.NET 网页（Razor）网站的访问者信息（分析）</span><span class="sxs-lookup"><span data-stu-id="6d991-103">Tracking Visitor Information (Analytics) for an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="6d991-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6d991-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6d991-105">本文介绍如何使用 helper 将网站分析添加到 ASP.NET 网页（Razor）网站中的页面。</span><span class="sxs-lookup"><span data-stu-id="6d991-105">This article describes how to use a helper to add website analytics to pages in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="6d991-106">学习内容：</span><span class="sxs-lookup"><span data-stu-id="6d991-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="6d991-107">如何将有关网站流量的信息发送到分析提供程序。</span><span class="sxs-lookup"><span data-stu-id="6d991-107">How to send information about your website traffic to an analytics provider.</span></span>
> 
> <span data-ttu-id="6d991-108">下面是本文中引入的 ASP.NET 编程功能：</span><span class="sxs-lookup"><span data-stu-id="6d991-108">These are the ASP.NET programming features introduced in the article:</span></span>
> 
> - <span data-ttu-id="6d991-109">`Analytics` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="6d991-109">The `Analytics` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6d991-110">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="6d991-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="6d991-111">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="6d991-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="6d991-112">ASP.NET Web 帮助程序库（NuGet 包）</span><span class="sxs-lookup"><span data-stu-id="6d991-112">ASP.NET Web Helpers Library (NuGet package)</span></span>

<span data-ttu-id="6d991-113">分析是对你的网站上的流量进行度量的一项通用术语，你可以了解人们如何使用该网站。</span><span class="sxs-lookup"><span data-stu-id="6d991-113">Analytics is a general term for technology that measures traffic on your website so you can understand how people use the site.</span></span> <span data-ttu-id="6d991-114">许多 analytics 服务都可用，包括 Google、Yahoo、StatCounter 等服务。</span><span class="sxs-lookup"><span data-stu-id="6d991-114">Many analytics services are available, including services from Google, Yahoo, StatCounter, and others.</span></span>

<span data-ttu-id="6d991-115">分析的工作方式是使用分析提供程序注册一个帐户，你可以在其中注册要跟踪的站点。提供程序会向你发送 JavaScript 代码片段，其中包含你的帐户的 ID 或跟踪代码。</span><span class="sxs-lookup"><span data-stu-id="6d991-115">The way analytics works is that you sign up for an account with the analytics provider, where you register the site that you want to track. The provider sends you a snippet of JavaScript code that includes an ID or tracking code for your account.</span></span> <span data-ttu-id="6d991-116">将 JavaScript 代码片段添加到要跟踪的网站上的网页中。（通常将分析代码片段添加到页脚或布局页，或添加到站点中每个页面上的其他 HTML 标记。）当用户请求包含其中一个 JavaScript 代码段的页面时，该代码段会将有关当前页的信息发送到分析提供程序，该提供程序记录有关该页的各种详细信息。</span><span class="sxs-lookup"><span data-stu-id="6d991-116">You add the JavaScript snippet to the web pages on the site that you want to track. (You typically add the analytics snippet to a footer or layout page or other HTML markup that appears on every page in your site.) When users request a page that contains one of these JavaScript snippets, the snippet sends information about the current page to the analytics provider, who records various details about the page.</span></span>

<span data-ttu-id="6d991-117">若要查看站点统计信息，请登录到 analytics 提供商的网站。</span><span class="sxs-lookup"><span data-stu-id="6d991-117">When you want to have a look at your site statistics, you log into the analytics provider's website.</span></span> <span data-ttu-id="6d991-118">然后，您可以查看有关您的站点的所有种类的报告，例如：</span><span class="sxs-lookup"><span data-stu-id="6d991-118">You can then view all sorts of reports about your site, like:</span></span>

- <span data-ttu-id="6d991-119">单个页面的页面视图数。</span><span class="sxs-lookup"><span data-stu-id="6d991-119">The number of page views for individual pages.</span></span> <span data-ttu-id="6d991-120">这会告诉你（大致）有多少人在访问该站点，网站上的哪些页面最受欢迎。</span><span class="sxs-lookup"><span data-stu-id="6d991-120">This tells you (roughly) how many people are visiting the site, and which pages on your site are the most popular.</span></span>
- <span data-ttu-id="6d991-121">用户在特定页面上花费的时间。</span><span class="sxs-lookup"><span data-stu-id="6d991-121">How long people spend on specific pages.</span></span> <span data-ttu-id="6d991-122">这可以告诉你主页是否有兴趣。</span><span class="sxs-lookup"><span data-stu-id="6d991-122">This can tell you things like whether your home page is keeping people's interest.</span></span>
- <span data-ttu-id="6d991-123">用户访问你的站点之前，他们在访问的站点。</span><span class="sxs-lookup"><span data-stu-id="6d991-123">What sites people were on before they visited your site.</span></span> <span data-ttu-id="6d991-124">这可以帮助您了解您的流量是来自链接、搜索还是来自搜索。</span><span class="sxs-lookup"><span data-stu-id="6d991-124">This helps you understand whether your traffic is coming from links, from searches, and so on.</span></span>
- <span data-ttu-id="6d991-125">当用户访问你的网站时，他们会持续多长时间。</span><span class="sxs-lookup"><span data-stu-id="6d991-125">When people visit your site and how long they stay.</span></span>
- <span data-ttu-id="6d991-126">访问者的国家/地区。</span><span class="sxs-lookup"><span data-stu-id="6d991-126">What countries your visitors are from.</span></span>
- <span data-ttu-id="6d991-127">你的访问者所使用的浏览器和操作系统。</span><span class="sxs-lookup"><span data-stu-id="6d991-127">What browsers and operating systems your visitors are using.</span></span>

    ![Ch14traffic-1](14-analyzing-traffic/_static/image1.jpg)

## <a name="using-a-helper-to-add-analytics-to-a-page"></a><span data-ttu-id="6d991-129">使用 Helper 向页面添加分析</span><span class="sxs-lookup"><span data-stu-id="6d991-129">Using a Helper to Add Analytics to a Page</span></span>

<span data-ttu-id="6d991-130">ASP.NET 网页包括多个分析帮助程序（`Analytics.GetGoogleHtml`、`Analytics.GetYahooHtml`和 `Analytics.GetStatCounterHtml`），使你可以轻松地管理用于分析的 JavaScript 代码段。</span><span class="sxs-lookup"><span data-stu-id="6d991-130">ASP.NET Web Pages includes several analytics helpers (`Analytics.GetGoogleHtml`, `Analytics.GetYahooHtml`, and `Analytics.GetStatCounterHtml`) that make it easy to manage the JavaScript snippets used for analytics.</span></span> <span data-ttu-id="6d991-131">你只需将帮助程序添加到页面，而不是找出如何以及在何处放置 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="6d991-131">Instead of figuring out how and where to put the JavaScript code, all you have to do is add the helper to a page.</span></span> <span data-ttu-id="6d991-132">你需要提供的唯一信息是你的帐户名称、ID 或跟踪代码。</span><span class="sxs-lookup"><span data-stu-id="6d991-132">The only information you need to provide is your account name, ID, or tracking code.</span></span> <span data-ttu-id="6d991-133">（对于 StatCounter，还必须提供一些额外的值。）</span><span class="sxs-lookup"><span data-stu-id="6d991-133">(For StatCounter, you also have to provide a few additional values.)</span></span>

<span data-ttu-id="6d991-134">在此过程中，您将创建一个使用 `GetGoogleHtml` 帮助器的布局页。</span><span class="sxs-lookup"><span data-stu-id="6d991-134">In this procedure, you'll create a layout page that uses the `GetGoogleHtml` helper.</span></span> <span data-ttu-id="6d991-135">如果已经有一个具有其他分析提供程序的帐户，则可以改为使用该帐户，并根据需要进行细微调整。</span><span class="sxs-lookup"><span data-stu-id="6d991-135">If you already have an account with one of the other analytics providers, you can use that account instead and make slight adjustments as needed.</span></span>

> [!NOTE]
> <span data-ttu-id="6d991-136">创建 analytics 帐户时，将注册要跟踪的站点的 URL。</span><span class="sxs-lookup"><span data-stu-id="6d991-136">When you create an analytics account, you register the URL of the site that you want to be tracking.</span></span> <span data-ttu-id="6d991-137">如果要测试本地计算机上的所有内容，则不会跟踪实际流量（唯一的流量是你的），因此你将无法记录和查看站点统计信息。</span><span class="sxs-lookup"><span data-stu-id="6d991-137">If you're testing everything on your local computer, you won't be tracking actual traffic (the only traffic is you), so you won't be able to record and view site statistics.</span></span> <span data-ttu-id="6d991-138">但此过程显示了如何将分析帮助器添加到页面。</span><span class="sxs-lookup"><span data-stu-id="6d991-138">But this procedure shows how you add an analytics helper to a page.</span></span> <span data-ttu-id="6d991-139">当你发布站点时，实时网站会将信息发送到你的分析提供程序。</span><span class="sxs-lookup"><span data-stu-id="6d991-139">When you publish your site, the live site will send information to your analytics provider.</span></span>

1. <span data-ttu-id="6d991-140">如在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未添加）。</span><span class="sxs-lookup"><span data-stu-id="6d991-140">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="6d991-141">使用 Google Analytics 创建帐户并记录帐户名称。</span><span class="sxs-lookup"><span data-stu-id="6d991-141">Create an account with Google Analytics and record the account name.</span></span>
3. <span data-ttu-id="6d991-142">创建名为 " *Analytics* " 的布局页并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="6d991-142">Create a layout page named *Analytics.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](14-analyzing-traffic/samples/sample1.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="6d991-143">必须将对 `Analytics` 帮助程序的调用放入网页（`</body>` 标记之前）的正文中。</span><span class="sxs-lookup"><span data-stu-id="6d991-143">You must place the call to the `Analytics` helper in the body of your web page (before the `</body>` tag).</span></span> <span data-ttu-id="6d991-144">否则，浏览器不会运行该脚本。</span><span class="sxs-lookup"><span data-stu-id="6d991-144">Otherwise, the browser will not run the script.</span></span>

    <span data-ttu-id="6d991-145">如果使用的是其他分析提供程序，请改用以下帮助器之一：</span><span class="sxs-lookup"><span data-stu-id="6d991-145">If you're using a different analytics provider, use one of the following helpers instead:</span></span>

    - <span data-ttu-id="6d991-146">（Yahoo） `@Analytics.GetYahooHtml("myaccount")`</span><span class="sxs-lookup"><span data-stu-id="6d991-146">(Yahoo) `@Analytics.GetYahooHtml("myaccount")`</span></span>
    - <span data-ttu-id="6d991-147">（StatCounter） `@Analytics.GetStatCounterHtml("project", "security")`</span><span class="sxs-lookup"><span data-stu-id="6d991-147">(StatCounter) `@Analytics.GetStatCounterHtml("project", "security")`</span></span>
4. <span data-ttu-id="6d991-148">将 `myaccount` 替换为在步骤1中创建的帐户、ID 或跟踪代码的名称。</span><span class="sxs-lookup"><span data-stu-id="6d991-148">Replace `myaccount` with the name of the account, ID, or tracking code that you created in step 1.</span></span>
5. <span data-ttu-id="6d991-149">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="6d991-149">Run the page in the browser.</span></span> <span data-ttu-id="6d991-150">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）</span><span class="sxs-lookup"><span data-stu-id="6d991-150">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
6. <span data-ttu-id="6d991-151">在浏览器中查看页面源。</span><span class="sxs-lookup"><span data-stu-id="6d991-151">In the browser, view the page source.</span></span> <span data-ttu-id="6d991-152">你将能够看到呈现的分析代码：</span><span class="sxs-lookup"><span data-stu-id="6d991-152">You'll be able to see the rendered analytics code:</span></span>

    [!code-html[Main](14-analyzing-traffic/samples/sample2.html)]
7. <span data-ttu-id="6d991-153">登录到 Google Analytics 站点并检查站点的统计信息。</span><span class="sxs-lookup"><span data-stu-id="6d991-153">Log onto the Google Analytics site and examine the statistics for your site.</span></span> <span data-ttu-id="6d991-154">如果在实时站点上运行该页面，则会看到一个记录访问页面的条目。</span><span class="sxs-lookup"><span data-stu-id="6d991-154">If you're running the page on a live site, you see an entry that logs the visit to your page.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="6d991-155">其他资源</span><span class="sxs-lookup"><span data-stu-id="6d991-155">Additional Resources</span></span>

- [<span data-ttu-id="6d991-156">Google Analytics 网站</span><span class="sxs-lookup"><span data-stu-id="6d991-156">Google Analytics site</span></span>](https://www.google.com/analytics/)
- [<span data-ttu-id="6d991-157">Yahoo！ Web Analytics 网站</span><span class="sxs-lookup"><span data-stu-id="6d991-157">Yahoo! Web Analytics site</span></span>](http://help.yahoo.com/l/us/yahoo/ywa/)
- [<span data-ttu-id="6d991-158">StatCounter 站点</span><span class="sxs-lookup"><span data-stu-id="6d991-158">StatCounter site</span></span>](http://statcounter.com/)
