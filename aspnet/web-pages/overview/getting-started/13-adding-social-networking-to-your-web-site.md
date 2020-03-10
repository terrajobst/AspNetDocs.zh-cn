---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: 将社交网络添加到 ASP.NET 网页（Razor）站点 |Microsoft Docs
author: Rick-Anderson
description: 本章介绍如何将站点与社交网络服务集成。 在本章中，你将了解如何允许人员将你的网站做成书签/链接 。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 1637464b0473bba8133acbbf8918d92b4f552701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422954"
---
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a><span data-ttu-id="f6e22-104">将社交网络添加到 ASP.NET 网页（Razor）站点</span><span class="sxs-lookup"><span data-stu-id="f6e22-104">Adding Social Networking to ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="f6e22-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f6e22-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f6e22-106">本文介绍如何将适用于 Facebook、Twitter、Reddit 和 Digg 的社交网络链接添加到 ASP.NET 网页（Razor）网站中的页面，以及如何包含 Twitter 源、Xbox 游戏者卡和 Gravatar 映像。</span><span class="sxs-lookup"><span data-stu-id="f6e22-106">This article explains how to add social networking links for Facebook, Twitter, Reddit, and Digg to pages in an ASP.NET Web Pages (Razor) website, and how to include Twitter feeds, Xbox gamer cards, and Gravatar images.</span></span>
> 
> <span data-ttu-id="f6e22-107">学习内容：</span><span class="sxs-lookup"><span data-stu-id="f6e22-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f6e22-108">如何让用户加入书签/链接您的网站。</span><span class="sxs-lookup"><span data-stu-id="f6e22-108">How to let people bookmark/link your site.</span></span>
> - <span data-ttu-id="f6e22-109">如何添加 Twitter 源。</span><span class="sxs-lookup"><span data-stu-id="f6e22-109">How to add a Twitter feed.</span></span>
> - <span data-ttu-id="f6e22-110">如何将**类似于**Facebook 的按钮添加到页面中。</span><span class="sxs-lookup"><span data-stu-id="f6e22-110">How to add a Facebook **Like** button to pages.</span></span>
> - <span data-ttu-id="f6e22-111">如何呈现 Gravatar.com 图像。</span><span class="sxs-lookup"><span data-stu-id="f6e22-111">How to render Gravatar.com images.</span></span>
> - <span data-ttu-id="f6e22-112">如何在你的站点上显示 Xbox 游戏者卡。</span><span class="sxs-lookup"><span data-stu-id="f6e22-112">How to display an Xbox gamer card on your site.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f6e22-113">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="f6e22-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f6e22-114">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="f6e22-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="f6e22-115">ASP.NET Web 帮助程序库（NuGet 包）</span><span class="sxs-lookup"><span data-stu-id="f6e22-115">ASP.NET Web Helper Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="f6e22-116">本教程还适用于 ASP.NET 网页3，但使用 ASP.NET Web Helper Library 的部分除外。</span><span class="sxs-lookup"><span data-stu-id="f6e22-116">This tutorial also works with ASP.NET Web Pages 3, except for parts that use the ASP.NET Web Helper Library.</span></span>

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a><span data-ttu-id="f6e22-117">链接社交网站上的网站</span><span class="sxs-lookup"><span data-stu-id="f6e22-117">Linking Your Website on Social Networking Sites</span></span>

<span data-ttu-id="f6e22-118">如果用户赞了网站上的内容，通常需要与朋友分享。</span><span class="sxs-lookup"><span data-stu-id="f6e22-118">If people like something on your site, they often want to share it with friends.</span></span> <span data-ttu-id="f6e22-119">可以通过显示用户可单击以在 Digg、Reddit、Facebook、Twitter 或类似站点上共享页面的字形（图标）来简化此过程。</span><span class="sxs-lookup"><span data-stu-id="f6e22-119">You can make this easy by displaying glyphs (icons) that people can click to share a page on Digg, Reddit, Facebook, Twitter, or similar sites.</span></span>

<span data-ttu-id="f6e22-120">若要显示这些字形，请将 `LinkSharecode` 帮助器添加到页面。</span><span class="sxs-lookup"><span data-stu-id="f6e22-120">To display these glyphs, add the `LinkSharecode` helper to a page.</span></span> <span data-ttu-id="f6e22-121">访问页面的用户可以单击单个字形。</span><span class="sxs-lookup"><span data-stu-id="f6e22-121">People who visit your page can click an individual glyph.</span></span> <span data-ttu-id="f6e22-122">如果他们具有使用该社交网络站点的帐户，则他们可以在该站点上发布指向页面的链接。</span><span class="sxs-lookup"><span data-stu-id="f6e22-122">If they have an account with that social networking site, they can then post a link to your page on that site.</span></span>

![图片1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. <span data-ttu-id="f6e22-124">如在[ASP.NET 网页站点中安装帮助](https://go.microsoft.com/fwlink/?LinkId=252372)程序中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未添加）。-创建名为*ListLinkShare*的页并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="f6e22-124">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.- Create a page named *ListLinkShare.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    <span data-ttu-id="f6e22-125">在此示例中，当 `LinkShare` 帮助程序运行时，会将页标题作为参数传递，进而会将页面标题传递到社交网络站点。</span><span class="sxs-lookup"><span data-stu-id="f6e22-125">In this example, when the `LinkShare` helper runs, the page title is passed as a parameter, which in turn passes the page title to the social networking site.</span></span> <span data-ttu-id="f6e22-126">但是，可以传入任何所需的字符串。</span><span class="sxs-lookup"><span data-stu-id="f6e22-126">However, you could pass in any string you want.</span></span> <span data-ttu-id="f6e22-127">此示例还指定要包含在列表中的社交网络站点。</span><span class="sxs-lookup"><span data-stu-id="f6e22-127">This example also specifies which social networking sites to include in the list.</span></span> <span data-ttu-id="f6e22-128">你可以指定与你的网站相关的社交网络站点。</span><span class="sxs-lookup"><span data-stu-id="f6e22-128">You can specify the social networking sites that are relevant to your site.</span></span>
2. <span data-ttu-id="f6e22-129">在浏览器中运行*ListLinkShare*页。</span><span class="sxs-lookup"><span data-stu-id="f6e22-129">Run the *ListLinkShare.cshtml* page in a browser.</span></span> <span data-ttu-id="f6e22-130">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）</span><span class="sxs-lookup"><span data-stu-id="f6e22-130">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
3. <span data-ttu-id="f6e22-131">单击要注册的某个网站的标志符号。</span><span class="sxs-lookup"><span data-stu-id="f6e22-131">Click a glyph for one of the sites that you're signed up for.</span></span> <span data-ttu-id="f6e22-132">该链接会将你转到所选社交网络站点上可共享链接的页面。</span><span class="sxs-lookup"><span data-stu-id="f6e22-132">The link takes you to the page on the selected social network site where you can share a link.</span></span> <span data-ttu-id="f6e22-133">例如，如果单击 "Reddit" 链接，则转到 Reddit 网站上的 "`submit to reddit`" 页。</span><span class="sxs-lookup"><span data-stu-id="f6e22-133">For example, if you click the Reddit link, you're taken to the `submit to reddit` page on the Reddit website.</span></span>

     ![图片2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a><span data-ttu-id="f6e22-135">添加 Twitter 源</span><span class="sxs-lookup"><span data-stu-id="f6e22-135">Adding a Twitter Feed</span></span>

<span data-ttu-id="f6e22-136">有关使用与当前版本的 Twitter API 兼容的 Twitter 帮助器的信息，请参阅[twitter 帮助](../ui-layouts-and-themes/twitter-helper.md)程序。</span><span class="sxs-lookup"><span data-stu-id="f6e22-136">For information about using a Twitter helper that is compatible with the current version of the Twitter API, see [Twitter helper](../ui-layouts-and-themes/twitter-helper.md).</span></span> <span data-ttu-id="f6e22-137">此示例演示如何编写您自己的帮助程序，以便您可以轻松地重复使用多个页面中的代码。</span><span class="sxs-lookup"><span data-stu-id="f6e22-137">This example shows how to write your own helper so you can easily reuse the code from many pages.</span></span>

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a><span data-ttu-id="f6e22-138">显示 Facebook &quot;如&quot; 按钮</span><span class="sxs-lookup"><span data-stu-id="f6e22-138">Displaying a Facebook &quot;Like&quot; Button</span></span>

<span data-ttu-id="f6e22-139">在某些情况下，最好的选择是直接从社交网络提供商处获取代码，而不是依赖于帮助者。</span><span class="sxs-lookup"><span data-stu-id="f6e22-139">In some cases, your best option is to get the code directly from the social networking provider rather than relying on a helper.</span></span> <span data-ttu-id="f6e22-140">如果社交网络提供程序更新其选项的速度比助手更新的速度更快，则更是如此。</span><span class="sxs-lookup"><span data-stu-id="f6e22-140">This is especially true if the social network provider updates its options more quickly than the helper is updated.</span></span>

<span data-ttu-id="f6e22-141">若要将 Facebook 功能（如 "赞" 按钮）添加到站点，你可以从[developers.facebook.com](https://developers.facebook.com/)站点检索代码片段。</span><span class="sxs-lookup"><span data-stu-id="f6e22-141">To add Facebook features (such as the Like button) to your site, you can retrieve code snippets from the [developers.facebook.com](https://developers.facebook.com/) site.</span></span> <span data-ttu-id="f6e22-142">在 Facebook 网站上，使用其工具生成与你的网站相关的代码片段。</span><span class="sxs-lookup"><span data-stu-id="f6e22-142">On the Facebook site, you use their tools to generate a code snippet that is relevant to your site.</span></span>

<span data-ttu-id="f6e22-143">以下突出显示的代码是从 developers.facebook.com 站点上的 "Like" 按钮工具检索到的代码。</span><span class="sxs-lookup"><span data-stu-id="f6e22-143">The following highlighted code is the code that was retrieved from the Like Button tool on the developers.facebook.com site.</span></span> <span data-ttu-id="f6e22-144">你必须提供自己的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="f6e22-144">You must provide your own app ID.</span></span>

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a><span data-ttu-id="f6e22-145">呈现 Gravatar 图像</span><span class="sxs-lookup"><span data-stu-id="f6e22-145">Rendering a Gravatar Image</span></span>

<span data-ttu-id="f6e22-146">*Gravatar* （一种 &quot;全局识别的头像&quot;）是一个图像，可以在多个网站上用作你&#8212;的头像，即表示你的映像。</span><span class="sxs-lookup"><span data-stu-id="f6e22-146">A *Gravatar* (a &quot;globally recognized avatar&quot;) is an image that can be used on multiple websites as your avatar &#8212; that is, an image that represents you.</span></span> <span data-ttu-id="f6e22-147">例如，Gravatar 可以标识论坛帖子中的人员、博客评论等。</span><span class="sxs-lookup"><span data-stu-id="f6e22-147">For example, a Gravatar can identify a person in a forum post, in a blog comment, and so on.</span></span> <span data-ttu-id="f6e22-148">（你可以在[http://www.gravatar.com/](http://www.gravatar.com/)上的 Gravatar 网站注册自己的 Gravatar。）如果要在网站上的人员姓名或电子邮件地址旁显示图像，则可以使用 Gravatar 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="f6e22-148">(You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/).) If you want to display images next to people's names or email addresses on your website, you can use the Gravatar helper.</span></span>

<span data-ttu-id="f6e22-149">在此示例中，你将使用代表自己的单个 Gravatar。</span><span class="sxs-lookup"><span data-stu-id="f6e22-149">In this example, you're using a single Gravatar that represents yourself.</span></span> <span data-ttu-id="f6e22-150">使用 Gravatar 的另一种方法是让用户在网站上注册时指定其 Gravatar 地址。</span><span class="sxs-lookup"><span data-stu-id="f6e22-150">Another way to use a Gravatar is to let people specify their Gravatar address when they register on your site.</span></span> <span data-ttu-id="f6e22-151">（您可以了解如何让人们注册[ASP.NET 网页站点添加安全性和成员身份](https://go.microsoft.com/fwlink/?LinkId=202904)。）然后，只要显示该用户的信息，只需将 Gravatar 添加到显示该用户名称的位置即可。</span><span class="sxs-lookup"><span data-stu-id="f6e22-151">(You can learn how to let people register in [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).) Then whenever you display information for that user, you can just add the Gravatar to where you display the user's name.</span></span>

1. <span data-ttu-id="f6e22-152">根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。</span><span class="sxs-lookup"><span data-stu-id="f6e22-152">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="f6e22-153">创建名为*Gravatar*的新网页。</span><span class="sxs-lookup"><span data-stu-id="f6e22-153">Create a new web page named *Gravatar.cshtml*.</span></span>
3. <span data-ttu-id="f6e22-154">将以下标记添加到文件中：</span><span class="sxs-lookup"><span data-stu-id="f6e22-154">Add the following markup to the file:</span></span> 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    <span data-ttu-id="f6e22-155">`Gravatar.GetHtml` 方法显示页面上的 Gravatar 图像。</span><span class="sxs-lookup"><span data-stu-id="f6e22-155">The `Gravatar.GetHtml` method displays the Gravatar image on the page.</span></span> <span data-ttu-id="f6e22-156">若要更改图像的大小，可以将数字包含为第二个参数。</span><span class="sxs-lookup"><span data-stu-id="f6e22-156">To change the size of the image, you can include a number as a second parameter.</span></span> <span data-ttu-id="f6e22-157">默认大小为80。</span><span class="sxs-lookup"><span data-stu-id="f6e22-157">The default size is 80.</span></span> <span data-ttu-id="f6e22-158">小于80的数字使图像更小。</span><span class="sxs-lookup"><span data-stu-id="f6e22-158">Numbers less than 80 make the image smaller.</span></span> <span data-ttu-id="f6e22-159">大于80的数字会使图像变大。</span><span class="sxs-lookup"><span data-stu-id="f6e22-159">Numbers greater than 80 make the image larger.</span></span>
4. <span data-ttu-id="f6e22-160">在 `Gravatar.GetHtml` 方法中，将 `<Your Gravatar account here>` 替换为用于 Gravatar 帐户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="f6e22-160">In the `Gravatar.GetHtml` methods, replace `<Your Gravatar account here>` with the email address that you use for your Gravatar account.</span></span> <span data-ttu-id="f6e22-161">（如果没有 Gravatar 帐户，可以使用该用户的电子邮件地址。）</span><span class="sxs-lookup"><span data-stu-id="f6e22-161">(If you don't have a Gravatar account, you can use the email address of someone who does.)</span></span>
5. <span data-ttu-id="f6e22-162">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="f6e22-162">Run the page in your browser.</span></span> <span data-ttu-id="f6e22-163">该页为你指定的电子邮件地址显示两个 Gravatar 图像。</span><span class="sxs-lookup"><span data-stu-id="f6e22-163">The page displays two Gravatar images for the email address you specified.</span></span> <span data-ttu-id="f6e22-164">第二个图像小于第一个图像。</span><span class="sxs-lookup"><span data-stu-id="f6e22-164">The second image is smaller than the first.</span></span> 

    ![图片4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a><span data-ttu-id="f6e22-166">显示 Xbox 游戏玩家卡</span><span class="sxs-lookup"><span data-stu-id="f6e22-166">Displaying an Xbox Gamer Card</span></span>

<span data-ttu-id="f6e22-167">当人们联机玩 Microsoft Xbox 游戏时，每个用户都有唯一的 ID。</span><span class="sxs-lookup"><span data-stu-id="f6e22-167">When people play Microsoft Xbox games online, each user has a unique ID.</span></span> <span data-ttu-id="f6e22-168">将以游戏者卡的形式为每个玩家保留统计信息，其中显示了其信誉、游戏玩家评分和最近玩的游戏。</span><span class="sxs-lookup"><span data-stu-id="f6e22-168">Statistics are kept for each player in the form of a gamer card, which shows their reputation, gamer score, and recently played games.</span></span> <span data-ttu-id="f6e22-169">如果你是 Xbox 游戏者，则可以使用 `GamerCard` 帮助程序在站点的页面上显示你的游戏者卡。</span><span class="sxs-lookup"><span data-stu-id="f6e22-169">If you're an Xbox gamer, you can show your gamer card on pages in your site by using the `GamerCard` helper.</span></span>

1. <span data-ttu-id="f6e22-170">根据在[ASP.NET 网页站点中安装帮助程序](https://go.microsoft.com/fwlink/?LinkId=252372)中所述，将 ASP.NET Web 帮助程序库添加到你的网站中（如果尚未安装）。</span><span class="sxs-lookup"><span data-stu-id="f6e22-170">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="f6e22-171">创建名为*XboxGamer*的新页面，并添加以下标记。</span><span class="sxs-lookup"><span data-stu-id="f6e22-171">Create a new page named *XboxGamer.cshtml* and add the following markup.</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    <span data-ttu-id="f6e22-172">使用 `GamerCard.GetHtml` 属性指定要显示的游戏玩家卡的别名。</span><span class="sxs-lookup"><span data-stu-id="f6e22-172">You use the `GamerCard.GetHtml` property to specify the alias for the gamer card to be displayed.</span></span>
3. <span data-ttu-id="f6e22-173">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="f6e22-173">Run the page in your browser.</span></span> <span data-ttu-id="f6e22-174">页面将显示您指定的 Xbox 游戏玩家卡。</span><span class="sxs-lookup"><span data-stu-id="f6e22-174">The page displays the Xbox gamer card that you specified.</span></span>

    ![图片 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)
