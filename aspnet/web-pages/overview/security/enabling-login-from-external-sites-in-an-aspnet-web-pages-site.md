---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: 使用 ASP.NET 网页（Razor）站点中的外部站点登录 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何使用 Facebook、Google、Twitter、Yahoo 和其他站点登录到你的 ASP.NET 网页（Razor）站点—也就是说，如何支持 。
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518786"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="8df9a-103">使用 ASP.NET 网页（Razor）站点中的外部站点登录</span><span class="sxs-lookup"><span data-stu-id="8df9a-103">Logging In Using External Sites in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="8df9a-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8df9a-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8df9a-105">本文介绍如何使用 Facebook、Google、Twitter、Yahoo 和其他站点登录到你的 ASP.NET 网页（Razor）站点—也就是说，如何在站点中支持 OAuth 和 OpenID。</span><span class="sxs-lookup"><span data-stu-id="8df9a-105">This article explains how to log in to your ASP.NET Web Pages (Razor) site using Facebook, Google, Twitter, Yahoo, and other sites — that is, how to support OAuth and OpenID in your site.</span></span>
> 
> <span data-ttu-id="8df9a-106">学习内容：</span><span class="sxs-lookup"><span data-stu-id="8df9a-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="8df9a-107">当你使用 WebMatrix 入门网站模板时，如何允许来自其他站点的登录。</span><span class="sxs-lookup"><span data-stu-id="8df9a-107">How to enable login from other sites when you use the WebMatrix Starter Site template.</span></span>
> 
> <span data-ttu-id="8df9a-108">这是本文中介绍的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="8df9a-108">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="8df9a-109">`OAuthWebSecurity` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="8df9a-109">The `OAuthWebSecurity` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8df9a-110">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="8df9a-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="8df9a-111">ASP.NET 网页（Razor）2</span><span class="sxs-lookup"><span data-stu-id="8df9a-111">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="8df9a-112">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="8df9a-112">WebMatrix 3</span></span>

<span data-ttu-id="8df9a-113">ASP.NET 网页包括对[OAuth](http://oauth.net/)和[OpenID](http://openid.net/)提供程序的支持。</span><span class="sxs-lookup"><span data-stu-id="8df9a-113">ASP.NET Web Pages includes support for [OAuth](http://oauth.net/) and [OpenID](http://openid.net/) providers.</span></span> <span data-ttu-id="8df9a-114">使用这些提供程序，你可以让用户使用其现有的 Facebook、Twitter、Microsoft 和 Google 凭据登录到你的站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-114">Using these providers, you can let users log into your site using their existing credentials from Facebook, Twitter, Microsoft, and Google.</span></span> <span data-ttu-id="8df9a-115">例如，若要使用 Facebook 帐户登录，用户只需选择一个 Facebook 图标，该图标会将其重定向到 Facebook 登录页，用户在其中输入其用户信息。</span><span class="sxs-lookup"><span data-stu-id="8df9a-115">For example, to log in using a Facebook account, users can just choose a Facebook icon, which redirects them to the Facebook login page where they enter their user information.</span></span> <span data-ttu-id="8df9a-116">然后，他们可以将 Facebook 登录名与其在你的站点上的帐户相关联。</span><span class="sxs-lookup"><span data-stu-id="8df9a-116">They can then associate the Facebook login with their account on your site.</span></span> <span data-ttu-id="8df9a-117">网页成员资格功能的相关增强功能是，用户可以将多个登录名（包括来自社交网站的登录名）与网站上的单个帐户关联起来。</span><span class="sxs-lookup"><span data-stu-id="8df9a-117">A related enhancement to the Web Pages membership features is that users can associate multiple logins (including logins from social networking sites) with a single account on your website.</span></span>

<span data-ttu-id="8df9a-118">此图显示了 "**入门网站**" 模板中的登录页，用户可以在其中选择 Facebook、Twitter、Google 或 Microsoft 图标来启用使用外部帐户登录：</span><span class="sxs-lookup"><span data-stu-id="8df9a-118">This image shows the Login page from the **Starter Site** template, where a user can choose a Facebook, Twitter, Google or Microsoft icon to enable logging in with an external account:</span></span>

![外部提供程序](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

<span data-ttu-id="8df9a-120">你可以通过取消注释**入门网站**模板中的几行代码来启用 OAuth 和 OpenID 成员身份。</span><span class="sxs-lookup"><span data-stu-id="8df9a-120">You can enable OAuth and OpenID membership by uncommenting a few lines of code in the **Starter Site** template.</span></span> <span data-ttu-id="8df9a-121">用于 OAuth 和 OpenID 提供程序的方法和属性位于 `WebMatrix.Security.OAuthWebSecurity` 类中。</span><span class="sxs-lookup"><span data-stu-id="8df9a-121">The methods and properties you use to work with the OAuth and OpenID providers are in the `WebMatrix.Security.OAuthWebSecurity` class.</span></span> <span data-ttu-id="8df9a-122">"**入门网站**" 模板包括完整的成员身份基础结构、"登录" 页和 "成员资格数据库"，以及让用户使用本地凭据或其他站点中的凭据登录到你的站点所需的所有代码。</span><span class="sxs-lookup"><span data-stu-id="8df9a-122">The **Starter Site** template includes a full membership infrastructure, complete with a login page, a membership database, and all the code you need to let users log into your site using either local credentials or those from another site.</span></span>

<span data-ttu-id="8df9a-123">本部分举例说明如何允许用户从外部站点登录到基于 "**入门网站**" 模板的站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-123">This section provides an example of how to let users log in from external sites to a site that's based on the **Starter Site** template.</span></span> <span data-ttu-id="8df9a-124">创建入门站点后，可以执行以下操作（详细信息如下）：</span><span class="sxs-lookup"><span data-stu-id="8df9a-124">After creating a starter site, you do this (details follow):</span></span>

- <span data-ttu-id="8df9a-125">对于使用 OAuth 提供程序（Facebook、Twitter 和 Microsoft）的站点，请在外部站点上创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="8df9a-125">For the sites that use an OAuth provider (Facebook, Twitter, and Microsoft), you create an application on the external site.</span></span> <span data-ttu-id="8df9a-126">这会提供为这些站点调用登录功能所需的应用程序密钥。</span><span class="sxs-lookup"><span data-stu-id="8df9a-126">This gives you application keys that you'll need in order to invoke the login feature for those sites.</span></span>
- <span data-ttu-id="8df9a-127">对于使用 OpenID 提供程序（Google）的站点，无需创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="8df9a-127">For sites that use an OpenID provider (Google), you do not have to create an application.</span></span> <span data-ttu-id="8df9a-128">对于所有这些站点，您必须具有一个帐户才能登录和创建开发人员应用程序。</span><span class="sxs-lookup"><span data-stu-id="8df9a-128">For all of these sites, you must have an account in order to log in and to create developer applications.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8df9a-129">Microsoft 应用程序仅接受工作网站的实时 URL，因此不能使用本地网站 URL 来测试登录名。</span><span class="sxs-lookup"><span data-stu-id="8df9a-129">Microsoft applications only accept a live URL for a working website, so you cannot use a local website URL for testing logins.</span></span>
- <span data-ttu-id="8df9a-130">编辑网站中的一些文件，以便指定适当的身份验证提供程序并将登录名提交到要使用的站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-130">Edit a few files in your website in order to specify the appropriate authentication provider and to submit a login to the site you want to use.</span></span>

<span data-ttu-id="8df9a-131">本文提供了有关以下任务的单独说明：</span><span class="sxs-lookup"><span data-stu-id="8df9a-131">This article provides separate instructions for the following tasks:</span></span>

- [<span data-ttu-id="8df9a-132">启用 Google 登录</span><span class="sxs-lookup"><span data-stu-id="8df9a-132">Enabling Google logins</span></span>](#To_enable_Google_logins)
- [<span data-ttu-id="8df9a-133">启用 Facebook 登录</span><span class="sxs-lookup"><span data-stu-id="8df9a-133">Enabling Facebook logins</span></span>](#To_enable_Facebook_logins)
- [<span data-ttu-id="8df9a-134">启用 Twitter 登录</span><span class="sxs-lookup"><span data-stu-id="8df9a-134">Enabling Twitter logins</span></span>](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a><span data-ttu-id="8df9a-135">启用 Google 登录</span><span class="sxs-lookup"><span data-stu-id="8df9a-135">Enabling Google Logins</span></span>

1. <span data-ttu-id="8df9a-136">创建或打开基于 WebMatrix 入门网站模板的 ASP.NET 网页站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-136">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="8df9a-137">打开 *\_AppStart* "页，取消注释以下代码行。</span><span class="sxs-lookup"><span data-stu-id="8df9a-137">Open the *\_AppStart.cshtml* page and uncomment the following line of code.</span></span> 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a><span data-ttu-id="8df9a-138">测试 Google login</span><span class="sxs-lookup"><span data-stu-id="8df9a-138">Testing Google login</span></span>

1. <span data-ttu-id="8df9a-139">运行站点的*默认.* # 页，然后选择 "**登录**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-139">Run the *default.cshtml* page of your site and choose the **Log in** button.</span></span>
2. <span data-ttu-id="8df9a-140">在 "*登录*" 页上，在 "**使用其他服务登录**" 部分中，选择 " **Google** " 或 " **Yahoo**提交" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-140">On the *Login* page, in the **Use another service to log in** section, choose either the **Google** or **Yahoo** submit button.</span></span> <span data-ttu-id="8df9a-141">此示例使用 Google 登录名。</span><span class="sxs-lookup"><span data-stu-id="8df9a-141">This example uses the Google login.</span></span> 

    <span data-ttu-id="8df9a-142">网页将请求重定向到 Google 登录页。</span><span class="sxs-lookup"><span data-stu-id="8df9a-142">The web page redirects the request to the Google login page.</span></span>

    ![Google 登录](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. <span data-ttu-id="8df9a-144">输入现有 Google 帐户的凭据。</span><span class="sxs-lookup"><span data-stu-id="8df9a-144">Enter credentials for an existing Google account.</span></span>
4. <span data-ttu-id="8df9a-145">如果 Google 询问你是否允许*Localhost*使用帐户中的信息，请单击 "**允许**"。</span><span class="sxs-lookup"><span data-stu-id="8df9a-145">If Google asks you whether you want to allow *Localhost* to use information from the account, click **Allow**.</span></span>

    <span data-ttu-id="8df9a-146">此代码使用 Google 令牌对用户进行身份验证，然后在你的网站上返回到此页面。</span><span class="sxs-lookup"><span data-stu-id="8df9a-146">The code uses the Google token to authenticate the user, and then returns to this page on your website.</span></span> <span data-ttu-id="8df9a-147">此页面允许用户将其 Google 登录名与网站上的现有帐户关联，或者他们可以在你的站点上注册新帐户以将外部登录名关联。</span><span class="sxs-lookup"><span data-stu-id="8df9a-147">This page lets users associate their Google login with an existing account on your website, or they can register a new account on your site to associate the external login with.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. <span data-ttu-id="8df9a-149">选择 "**关联**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-149">Choose the **Associate** button.</span></span> <span data-ttu-id="8df9a-150">浏览器返回到应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="8df9a-150">The browser returns to your application's home page.</span></span>

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a><span data-ttu-id="8df9a-151">启用 Facebook 登录</span><span class="sxs-lookup"><span data-stu-id="8df9a-151">Enabling Facebook Logins</span></span>

1. <span data-ttu-id="8df9a-152">如果你尚未登录，请前往[Facebook 开发人员站点](https://developers.facebook.com/apps)（登录）。</span><span class="sxs-lookup"><span data-stu-id="8df9a-152">Go to the [Facebook developers site](https://developers.facebook.com/apps) (log in if you're not already logged in).</span></span>
2. <span data-ttu-id="8df9a-153">选择 "**新建应用**程序" 按钮，然后按照提示命名并创建新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8df9a-153">Choose the **Create New App** button, and then follow the prompts to name and create the new application.</span></span>
3. <span data-ttu-id="8df9a-154">在 "**选择应用将如何与 Facebook 集成**" 部分中，选择 "**网站**" 部分。</span><span class="sxs-lookup"><span data-stu-id="8df9a-154">In the section **Select how your app will integrate with Facebook**, choose the **Website** section.</span></span>
4. <span data-ttu-id="8df9a-155">在 "**网站 url** " 字段中填入网站的 url （例如 `http://www.example.com`）。</span><span class="sxs-lookup"><span data-stu-id="8df9a-155">Fill in the **Site URL** field with the URL of your site (for example, `http://www.example.com`).</span></span> <span data-ttu-id="8df9a-156">**域**字段是可选的;您可以使用此来为整个域（如*example.com*）提供身份验证。</span><span class="sxs-lookup"><span data-stu-id="8df9a-156">The **Domain** field is optional; you can use this to provide authentication for an entire domain (such as *example.com*).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="8df9a-157">如果你在本地计算机上运行的站点的 URL 如 `http://localhost:12345` （其中数字是本地端口号），则可以将此值添加到用于测试网站的 "**网站 URL** " 字段。</span><span class="sxs-lookup"><span data-stu-id="8df9a-157">If you are running a site on your local computer with a URL like `http://localhost:12345` (where the number is a local port number), you can add this value to the **Site URL** field for testing your site.</span></span> <span data-ttu-id="8df9a-158">但是，只要本地站点的端口号发生更改，就需要更新应用程序的 "**网站 URL** " 字段。</span><span class="sxs-lookup"><span data-stu-id="8df9a-158">However, any time the port number of your local site changes, you will need to update the **Site URL** field of your application.</span></span>
5. <span data-ttu-id="8df9a-159">选择 "**保存更改**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-159">Choose the **Save Changes** button.</span></span>
6. <span data-ttu-id="8df9a-160">再次选择 "**应用**" 选项卡，然后查看应用程序的起始页。</span><span class="sxs-lookup"><span data-stu-id="8df9a-160">Choose the **Apps** tab again, and then view the start page for your application.</span></span>
7. <span data-ttu-id="8df9a-161">复制应用程序的应用**ID**和应用**密钥**值，并将其粘贴到临时文本文件中。</span><span class="sxs-lookup"><span data-stu-id="8df9a-161">Copy the **App ID** and **App Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="8df9a-162">你将在网站代码中将这些值传递到 Facebook 提供程序。</span><span class="sxs-lookup"><span data-stu-id="8df9a-162">You will pass these values to the Facebook provider in your website code.</span></span>
8. <span data-ttu-id="8df9a-163">退出 Facebook 开发人员网站。</span><span class="sxs-lookup"><span data-stu-id="8df9a-163">Exit the Facebook developer site.</span></span>

<span data-ttu-id="8df9a-164">现在，你将更改网站中的两个页面，以便用户能够使用其 Facebook 帐户登录到站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-164">Now you make changes to two pages in your website so that users will able to log into the site using their Facebook accounts.</span></span>

1. <span data-ttu-id="8df9a-165">创建或打开基于 WebMatrix 入门网站模板的 ASP.NET 网页站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-165">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="8df9a-166">打开 *\_AppStart* "页，取消注释 Facebook OAuth 提供程序的代码。</span><span class="sxs-lookup"><span data-stu-id="8df9a-166">Open the *\_AppStart.cshtml* page and uncomment the code for the Facebook OAuth provider.</span></span> <span data-ttu-id="8df9a-167">取消注释代码块如下所示：</span><span class="sxs-lookup"><span data-stu-id="8df9a-167">The uncommented code block looks like the following:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. <span data-ttu-id="8df9a-168">将 Facebook 应用程序的**应用 ID**值复制为 `appId` 参数的值（在引号内）。</span><span class="sxs-lookup"><span data-stu-id="8df9a-168">Copy the **App ID** value from the Facebook application as the value of the `appId` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="8df9a-169">从 Facebook 应用程序中复制**应用程序密钥**值作为 `appSecret` 参数值。</span><span class="sxs-lookup"><span data-stu-id="8df9a-169">Copy **App Secret** value from the Facebook application as the `appSecret` parameter value.</span></span>
5. <span data-ttu-id="8df9a-170">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="8df9a-170">Save and close the file.</span></span>

### <a name="testing-facebook-login"></a><span data-ttu-id="8df9a-171">测试 Facebook 登录</span><span class="sxs-lookup"><span data-stu-id="8df9a-171">Testing Facebook login</span></span>

1. <span data-ttu-id="8df9a-172">运行该站点的 "*默认值*" 页，然后选择 "**登录**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-172">Run the site's *default.cshtml* page and choose the **Login** button.</span></span>
2. <span data-ttu-id="8df9a-173">在 "*登录*" 页上，在 "**使用其他服务登录**" 部分中，选择 " **Facebook** " 图标。</span><span class="sxs-lookup"><span data-stu-id="8df9a-173">On the *Login* page, in the **Use another service to log in** section, choose the **Facebook** icon.</span></span> 

    <span data-ttu-id="8df9a-174">网页将请求重定向到 Facebook 登录页。</span><span class="sxs-lookup"><span data-stu-id="8df9a-174">The web page redirects the request to the Facebook login page.</span></span>

    ![oauth-2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. <span data-ttu-id="8df9a-176">登录到 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="8df9a-176">Log into a Facebook account.</span></span> 

    <span data-ttu-id="8df9a-177">该代码使用 Facebook 令牌对你进行身份验证，然后返回到一个页面，可在其中将 Facebook 登录名与站点的登录名相关联。</span><span class="sxs-lookup"><span data-stu-id="8df9a-177">The code uses the Facebook token to authenticate you and then returns to a page where you can associate your Facebook login with your site's login.</span></span> <span data-ttu-id="8df9a-178">你的用户名或电子邮件地址将填充到表单上的 "**电子邮件**" 字段。</span><span class="sxs-lookup"><span data-stu-id="8df9a-178">Your user name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. <span data-ttu-id="8df9a-180">选择 "**关联**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-180">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="8df9a-181">浏览器返回到主页并且您已登录。</span><span class="sxs-lookup"><span data-stu-id="8df9a-181">The browser returns to the home page and you are logged in.</span></span>

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a><span data-ttu-id="8df9a-182">启用 Twitter 登录</span><span class="sxs-lookup"><span data-stu-id="8df9a-182">Enabling Twitter Logins</span></span>

1. <span data-ttu-id="8df9a-183">浏览到[Twitter 开发人员网站](https://dev.twitter.com/)。</span><span class="sxs-lookup"><span data-stu-id="8df9a-183">Browse to the [Twitter developers site](https://dev.twitter.com/).</span></span>
2. <span data-ttu-id="8df9a-184">选择 "**创建应用程序**" 链接，然后登录到站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-184">Choose the **Create an App** link and then log into the site.</span></span>
3. <span data-ttu-id="8df9a-185">在 "**创建应用程序**" 窗体中，填写 "**名称**" 和 "**说明**" 字段。</span><span class="sxs-lookup"><span data-stu-id="8df9a-185">On the **Create an Application** form, fill in the **Name** and **Description** fields.</span></span>
4. <span data-ttu-id="8df9a-186">在 "**网站**" 字段中，输入网站的 URL （例如 `http://www.example.com`）。</span><span class="sxs-lookup"><span data-stu-id="8df9a-186">In the **WebSite** field, enter the URL of your site (for example, `http://www.example.com`).</span></span> 

    > [!NOTE]
    > <span data-ttu-id="8df9a-187">如果要在本地测试网站（使用 `http://localhost:12345`的 URL），Twitter 可能不会接受 URL。</span><span class="sxs-lookup"><span data-stu-id="8df9a-187">If you're testing your site locally (using a URL like `http://localhost:12345`), Twitter might not accept the URL.</span></span> <span data-ttu-id="8df9a-188">但是，你可以使用本地环回 IP 地址（例如 `http://127.0.0.1:12345`）。</span><span class="sxs-lookup"><span data-stu-id="8df9a-188">However, you might be able to use the local loopback IP address (for example `http://127.0.0.1:12345`).</span></span> <span data-ttu-id="8df9a-189">这简化了本地测试应用程序的过程。</span><span class="sxs-lookup"><span data-stu-id="8df9a-189">This simplifies the process of testing your application locally.</span></span> <span data-ttu-id="8df9a-190">但是，每次你的本地站点的端口号发生变化时，你将需要更新应用程序的 "**网站**" 字段。</span><span class="sxs-lookup"><span data-stu-id="8df9a-190">However, every time the port number of your local site changes, you'll need to update the **WebSite** field of your application.</span></span>
5. <span data-ttu-id="8df9a-191">在 "**回调 URL** " 字段中，输入你希望用户在登录到 Twitter 后返回到的页面 URL。</span><span class="sxs-lookup"><span data-stu-id="8df9a-191">In the **Callback URL** field, enter a URL for the page in your website that you want users to return to after logging into Twitter.</span></span> <span data-ttu-id="8df9a-192">例如，要将用户发送到起始站点（将识别其登录状态）的主页，请输入你在 "**网站**" 字段中输入的相同 URL。</span><span class="sxs-lookup"><span data-stu-id="8df9a-192">For example, to send users to the home page of the Starter Site (which will recognize their logged-in status), enter the same URL that you entered in the **WebSite** field.</span></span>
6. <span data-ttu-id="8df9a-193">接受这些条款，然后选择 "**创建 Twitter 应用程序**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-193">Accept the terms and choose the **Create your Twitter application** button.</span></span>
7. <span data-ttu-id="8df9a-194">在 "**我的应用程序**" 登陆页上，选择您创建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8df9a-194">On the **My Applications** landing page, choose the application you created.</span></span>
8. <span data-ttu-id="8df9a-195">在 "**详细信息**" 选项卡上，滚动到底部，然后选择 "**创建我的访问令牌**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-195">On the **Details** tab, scroll to the bottom and choose the **Create My Access Token** button.</span></span>
9. <span data-ttu-id="8df9a-196">在 "**详细信息**" 选项卡上，复制应用程序的 "**使用者密钥**" 和 "**使用者机密**" 值，并将其粘贴到临时文本文件中。</span><span class="sxs-lookup"><span data-stu-id="8df9a-196">On the **Details** tab, copy the **Consumer Key** and **Consumer Secret** values for your application and paste them into a temporary text file.</span></span> <span data-ttu-id="8df9a-197">你将在网站代码中将这些值传递给 Twitter 提供商。</span><span class="sxs-lookup"><span data-stu-id="8df9a-197">You'll pass these values to the Twitter provider in your website code.</span></span>
10. <span data-ttu-id="8df9a-198">退出 Twitter 站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-198">Exit the Twitter site.</span></span>

<span data-ttu-id="8df9a-199">现在，你将更改网站中的两个页面，以便用户能够使用其 Twitter 帐户登录到站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-199">Now you make changes to two pages in your website so that users will be able to log into the site using their Twitter accounts.</span></span>

1. <span data-ttu-id="8df9a-200">创建或打开基于 WebMatrix 入门网站模板的 ASP.NET 网页站点。</span><span class="sxs-lookup"><span data-stu-id="8df9a-200">Create or open an ASP.NET Web Pages site that's based on the WebMatrix Starter Site template.</span></span>
2. <span data-ttu-id="8df9a-201">打开 *\_AppStart* "页，取消对 Twitter OAuth 提供程序的代码的注释。</span><span class="sxs-lookup"><span data-stu-id="8df9a-201">Open the *\_AppStart.cshtml* page and uncomment the code for the Twitter OAuth provider.</span></span> <span data-ttu-id="8df9a-202">取消注释代码块如下所示：</span><span class="sxs-lookup"><span data-stu-id="8df9a-202">The uncommented code block looks like this:</span></span> 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. <span data-ttu-id="8df9a-203">将 Twitter 应用程序的**使用者密钥**值复制为 `consumerKey` 参数的值（在引号内）。</span><span class="sxs-lookup"><span data-stu-id="8df9a-203">Copy the **Consumer Key** value from the Twitter application as the value of the `consumerKey` parameter (inside the quotation marks).</span></span>
4. <span data-ttu-id="8df9a-204">复制 Twitter 应用程序的**使用者机密**值作为 `consumerSecret` 参数的值。</span><span class="sxs-lookup"><span data-stu-id="8df9a-204">Copy the **Consumer Secret** value from the Twitter application as the value of the `consumerSecret` parameter.</span></span>
5. <span data-ttu-id="8df9a-205">保存并关闭文件。</span><span class="sxs-lookup"><span data-stu-id="8df9a-205">Save and close the file.</span></span>

### <a name="testing-twitter-login"></a><span data-ttu-id="8df9a-206">测试 Twitter 登录</span><span class="sxs-lookup"><span data-stu-id="8df9a-206">Testing Twitter login</span></span>

1. <span data-ttu-id="8df9a-207">运行网站的*默认.* # 页，然后选择 "**登录**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-207">Run the *default.cshtml* page of your site and choose the **Login** button.</span></span>
2. <span data-ttu-id="8df9a-208">在 "*登录*" 页上，在 "**使用其他服务登录**" 部分中，选择 " **Twitter** " 图标。</span><span class="sxs-lookup"><span data-stu-id="8df9a-208">On the *Login* page, in the **Use another service to log in** section, choose the **Twitter** icon.</span></span> 

    <span data-ttu-id="8df9a-209">网页将请求重定向到所创建的应用程序的 Twitter 登录页。</span><span class="sxs-lookup"><span data-stu-id="8df9a-209">The web page redirects the request to a Twitter login page for the application you created.</span></span>

    ![oauth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. <span data-ttu-id="8df9a-211">登录到 Twitter 帐户。</span><span class="sxs-lookup"><span data-stu-id="8df9a-211">Log into a Twitter account.</span></span>
4. <span data-ttu-id="8df9a-212">此代码使用 Twitter 令牌对用户进行身份验证，并返回到可将登录名与网站帐户关联的页面。</span><span class="sxs-lookup"><span data-stu-id="8df9a-212">The code uses the Twitter token to authenticate the user and then returns you to a page where you can associate your login with your website account.</span></span> <span data-ttu-id="8df9a-213">你的姓名或电子邮件地址将填充到表单上的 "**电子邮件**" 字段中。</span><span class="sxs-lookup"><span data-stu-id="8df9a-213">Your name or email address is filled into the **Email** field on the form.</span></span>

    ![oauth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. <span data-ttu-id="8df9a-215">选择 "**关联**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8df9a-215">Choose the **Associate** button.</span></span> 

    <span data-ttu-id="8df9a-216">浏览器返回到主页并且您已登录。</span><span class="sxs-lookup"><span data-stu-id="8df9a-216">The browser returns to the home page and you are logged in.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="8df9a-217">其他资源</span><span class="sxs-lookup"><span data-stu-id="8df9a-217">Additional Resources</span></span>

- [<span data-ttu-id="8df9a-218">自定义站点范围内的行为</span><span class="sxs-lookup"><span data-stu-id="8df9a-218">Customizing Site-Wide Behavior</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="8df9a-219">将安全性和成员身份添加到 ASP.NET 网页站点</span><span class="sxs-lookup"><span data-stu-id="8df9a-219">Adding Security and Membership to an ASP.NET Web Pages Site</span></span>](https://go.microsoft.com/fwlink/?LinkID=202904)
