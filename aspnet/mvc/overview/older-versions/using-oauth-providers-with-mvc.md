---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: 将 OAuth 提供程序与 MVC 4 一起使用 |Microsoft Docs
author: Rick-Anderson
description: 本教程演示如何生成一个 ASP.NET MVC 4 web 应用程序，该应用程序允许用户使用来自外部提供程序的凭据（如 Facebo ...）登录。
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433364"
---
# <a name="using-oauth-providers-with-mvc-4"></a><span data-ttu-id="d41b5-103">通过 MVC 4 使用 OAuth 提供程序</span><span class="sxs-lookup"><span data-stu-id="d41b5-103">Using OAuth Providers with MVC 4</span></span>

<span data-ttu-id="d41b5-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d41b5-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d41b5-105">本教程演示如何生成一个 ASP.NET MVC 4 web 应用程序，该应用程序允许用户使用来自外部提供程序（如 Facebook、Twitter、Microsoft 或 Google）的凭据登录，然后将这些提供程序中的某些功能集成到你的web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="d41b5-105">This tutorial shows you how to build an ASP.NET MVC 4 web application that enables users to log in with credentials from an external provider, such as Facebook, Twitter, Microsoft, or Google, and then integrate some of the functionality from those providers into your web application.</span></span> <span data-ttu-id="d41b5-106">为简单起见，本教程重点介绍如何使用 Facebook 中的凭据。</span><span class="sxs-lookup"><span data-stu-id="d41b5-106">For simplicity, this tutorial focuses on working with credentials from Facebook.</span></span>
> 
> <span data-ttu-id="d41b5-107">若要在 ASP.NET MVC 5 web 应用程序中使用外部凭据，请参阅使用[Facebook 和 Google OAuth2 创建 ASP.NET MVC 5 应用和 OpenID 登录](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="d41b5-107">To use external credentials in an ASP.NET MVC 5 web application, see [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>
> 
> <span data-ttu-id="d41b5-108">如果在您的网站中启用这些凭据，则会带来明显的优势，因为数百万用户已经拥有了具有这些外部提供商的帐户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-108">Enabling these credentials in your web sites provides a significant advantage because millions of users already have accounts with these external providers.</span></span> <span data-ttu-id="d41b5-109">如果用户无需创建和记住一组新凭据，则可能更倾向于注册你的站点。</span><span class="sxs-lookup"><span data-stu-id="d41b5-109">These users may be more inclined to sign up for your site if they do not have to create and remember a new set of credentials.</span></span> <span data-ttu-id="d41b5-110">此外，在用户通过其中一个提供程序登录后，你可以将社交操作纳入提供商。</span><span class="sxs-lookup"><span data-stu-id="d41b5-110">Also, after a user has logged in through one of these providers, you can incorporate social operations from the provider.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="d41b5-111">要生成的内容</span><span class="sxs-lookup"><span data-stu-id="d41b5-111">What you'll build</span></span>

<span data-ttu-id="d41b5-112">在本教程中，主要有两个目标：</span><span class="sxs-lookup"><span data-stu-id="d41b5-112">There are two main goals in this tutorial:</span></span>

1. <span data-ttu-id="d41b5-113">允许用户使用 OAuth 提供程序提供的凭据登录。</span><span class="sxs-lookup"><span data-stu-id="d41b5-113">Enable a user to log in with credentials from an OAuth provider.</span></span>
2. <span data-ttu-id="d41b5-114">从提供程序中检索帐户信息，并将该信息与网站的帐户注册集成。</span><span class="sxs-lookup"><span data-stu-id="d41b5-114">Retrieve account information from the provider and integrate that information with the account registration for your site.</span></span>

<span data-ttu-id="d41b5-115">尽管本教程中的示例重点介绍如何使用 Facebook 作为身份验证提供程序，但你可以修改代码以使用任何提供程序。</span><span class="sxs-lookup"><span data-stu-id="d41b5-115">Although the examples in this tutorial focus on using Facebook as the authentication provider, you can modify the code to use any of the providers.</span></span> <span data-ttu-id="d41b5-116">实现任何提供程序的步骤与你将在本教程中看到的步骤非常类似。</span><span class="sxs-lookup"><span data-stu-id="d41b5-116">The steps to implement any provider are very similar to the steps you will see in this tutorial.</span></span> <span data-ttu-id="d41b5-117">直接调用提供程序的 API 集时，你只会注意到明显差异。</span><span class="sxs-lookup"><span data-stu-id="d41b5-117">You will only notice significant differences when making direct calls to the provider's API set.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d41b5-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="d41b5-118">Prerequisites</span></span>

- <span data-ttu-id="d41b5-119">Web [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs)或[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span><span class="sxs-lookup"><span data-stu-id="d41b5-119">[Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) or [Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)</span></span>

<span data-ttu-id="d41b5-120">Or</span><span class="sxs-lookup"><span data-stu-id="d41b5-120">Or</span></span>

- <span data-ttu-id="d41b5-121">Microsoft Visual Studio 2010 SP1 或[Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span><span class="sxs-lookup"><span data-stu-id="d41b5-121">Microsoft Visual Studio 2010 SP1 or [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)</span></span>
- [<span data-ttu-id="d41b5-122">ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="d41b5-122">ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)

<span data-ttu-id="d41b5-123">此外，本主题假定您具有有关 ASP.NET MVC 和 Visual Studio 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="d41b5-123">Furthermore, this topic assumes you have basic knowledge about ASP.NET MVC and Visual Studio.</span></span> <span data-ttu-id="d41b5-124">如果需要 ASP.NET MVC 4 简介，请参阅[ASP.NET mvc 4 简介](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="d41b5-124">If you need an introduction to ASP.NET MVC 4, see [Intro to ASP.NET MVC 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).</span></span>

## <a name="create-the-project"></a><span data-ttu-id="d41b5-125">创建项目</span><span class="sxs-lookup"><span data-stu-id="d41b5-125">Create the project</span></span>

<span data-ttu-id="d41b5-126">在 Visual Studio 中，创建一个新的 ASP.NET MVC 4 Web 应用程序，并将其命名为 &quot;OAuthMVC&quot;。</span><span class="sxs-lookup"><span data-stu-id="d41b5-126">In Visual Studio, create a new ASP.NET MVC 4 Web Application, and name it &quot;OAuthMVC&quot;.</span></span> <span data-ttu-id="d41b5-127">可以为 .NET Framework 4.5 或4。</span><span class="sxs-lookup"><span data-stu-id="d41b5-127">You can target either .NET Framework 4.5 or 4.</span></span>

![创建项目](using-oauth-providers-with-mvc/_static/image1.png)

<span data-ttu-id="d41b5-129">在 New ASP.NET MVC 4 项目窗口中，选择 " **Internet 应用程序**"，并将**Razor**保留为视图引擎。</span><span class="sxs-lookup"><span data-stu-id="d41b5-129">In the New ASP.NET MVC 4 Project window, select **Internet Application** and leave **Razor** as the view engine.</span></span>

![选择 Internet 应用程序](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a><span data-ttu-id="d41b5-131">启用提供程序</span><span class="sxs-lookup"><span data-stu-id="d41b5-131">Enable a provider</span></span>

<span data-ttu-id="d41b5-132">使用 Internet 应用程序模板创建 MVC 4 web 应用程序时，将使用应用\_Start 文件夹中名为 "AuthConfig.cs" 的文件创建该项目。</span><span class="sxs-lookup"><span data-stu-id="d41b5-132">When you create an MVC 4 web application with the Internet Application template, the project is created with a file named AuthConfig.cs in the App\_Start folder.</span></span>

![AuthConfig 文件](using-oauth-providers-with-mvc/_static/image3.png)

<span data-ttu-id="d41b5-134">AuthConfig 文件包含用于注册外部身份验证提供程序的客户端的代码。</span><span class="sxs-lookup"><span data-stu-id="d41b5-134">The AuthConfig file contains code to register clients for external authentication providers.</span></span> <span data-ttu-id="d41b5-135">默认情况下，此代码已被注释掉，因此没有启用任何外部提供程序。</span><span class="sxs-lookup"><span data-stu-id="d41b5-135">By default, this code is commented out, so none of the external providers are enabled.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

<span data-ttu-id="d41b5-136">必须取消注释此代码才能使用外部身份验证客户端。</span><span class="sxs-lookup"><span data-stu-id="d41b5-136">You must uncomment this code to use the external authentication client.</span></span> <span data-ttu-id="d41b5-137">仅取消注释要包含在站点中的提供程序。</span><span class="sxs-lookup"><span data-stu-id="d41b5-137">You uncomment only the providers you want to include in your site.</span></span> <span data-ttu-id="d41b5-138">对于本教程，将只启用 Facebook 凭据。</span><span class="sxs-lookup"><span data-stu-id="d41b5-138">For this tutorial, you will only enable the Facebook credentials.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

<span data-ttu-id="d41b5-139">请注意，在上面的示例中，该方法包含用于注册参数的空字符串。</span><span class="sxs-lookup"><span data-stu-id="d41b5-139">Notice in the above example that the method includes empty strings for the registration parameters.</span></span> <span data-ttu-id="d41b5-140">如果现在尝试运行应用程序，应用程序会引发参数异常，因为参数不允许使用空字符串。</span><span class="sxs-lookup"><span data-stu-id="d41b5-140">If you try to run the application now, the application throws an argument exception because empty strings are not allowed for the parameters.</span></span> <span data-ttu-id="d41b5-141">若要提供有效值，您必须向外部提供程序注册您的网站，如下一节所示。</span><span class="sxs-lookup"><span data-stu-id="d41b5-141">To provide valid values, you must register your web site with the external providers, as shown in the next section.</span></span>

## <a name="registering-with-an-external-provider"></a><span data-ttu-id="d41b5-142">使用外部提供程序进行注册</span><span class="sxs-lookup"><span data-stu-id="d41b5-142">Registering with an external provider</span></span>

<span data-ttu-id="d41b5-143">若要使用来自外部提供程序的凭据对用户进行身份验证，必须向提供程序注册您的网站。</span><span class="sxs-lookup"><span data-stu-id="d41b5-143">To authenticate users with credentials from an external provider, you must register your web site with the provider.</span></span> <span data-ttu-id="d41b5-144">注册站点时，会收到注册客户端时要包含的参数（如密钥或 id 和机密）。</span><span class="sxs-lookup"><span data-stu-id="d41b5-144">When you register your site, you will receive the parameters (such as key or id, and secret) to include when registering the client.</span></span> <span data-ttu-id="d41b5-145">您必须拥有一个要使用的提供程序的帐户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-145">You must have an account with the providers you wish to use.</span></span>

<span data-ttu-id="d41b5-146">本教程不提供使用这些提供程序进行注册所必须执行的全部步骤。</span><span class="sxs-lookup"><span data-stu-id="d41b5-146">This tutorial does not show all of the steps you must perform to register with these providers.</span></span> <span data-ttu-id="d41b5-147">这些步骤通常比较简单。</span><span class="sxs-lookup"><span data-stu-id="d41b5-147">The steps are typically not difficult.</span></span> <span data-ttu-id="d41b5-148">若要成功注册您的网站，请按照这些网站上提供的说明操作。</span><span class="sxs-lookup"><span data-stu-id="d41b5-148">To successfully register your site, follow the instructions provided on those sites.</span></span> <span data-ttu-id="d41b5-149">若要开始注册您的网站，请查看下列门户的开发人员网站：</span><span class="sxs-lookup"><span data-stu-id="d41b5-149">To get started with registering your site, see the developer site for:</span></span>

- [<span data-ttu-id="d41b5-150">Facebook</span><span class="sxs-lookup"><span data-stu-id="d41b5-150">Facebook</span></span>](https://developers.facebook.com/)
- [<span data-ttu-id="d41b5-151">Google</span><span class="sxs-lookup"><span data-stu-id="d41b5-151">Google</span></span>](https://developers.google.com/)
- [<span data-ttu-id="d41b5-152">Microsoft</span><span class="sxs-lookup"><span data-stu-id="d41b5-152">Microsoft</span></span>](http://manage.dev.live.com/)
- [<span data-ttu-id="d41b5-153">Twitter</span><span class="sxs-lookup"><span data-stu-id="d41b5-153">Twitter</span></span>](https://dev.twitter.com/)

<span data-ttu-id="d41b5-154">向 Facebook 注册站点时，可以为站点域提供 &quot;localhost&quot;，并为 URL `&quot; http://localhost/&quot;` 提供 URL，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="d41b5-154">When registering your site with Facebook, you can provide &quot;localhost&quot; for the site domain and `&quot;http://localhost/&quot;` for the URL, as shown in the image below.</span></span> <span data-ttu-id="d41b5-155">使用 localhost 适用于大多数提供程序，但目前不适用于 Microsoft 提供商。</span><span class="sxs-lookup"><span data-stu-id="d41b5-155">Using localhost works with most providers, but currently does not work with the Microsoft provider.</span></span> <span data-ttu-id="d41b5-156">对于 Microsoft 提供程序，您必须包含一个有效的网站 URL。</span><span class="sxs-lookup"><span data-stu-id="d41b5-156">For the Microsoft provider, you must include a valid web site URL.</span></span>

![注册站点](using-oauth-providers-with-mvc/_static/image4.png)

<span data-ttu-id="d41b5-158">在上图中，已删除应用程序 id、应用程序密钥和联系人电子邮件的值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-158">In the previous image, the values for the app id, app secret, and contact email have been removed.</span></span> <span data-ttu-id="d41b5-159">当你实际注册站点时，这些值将存在。</span><span class="sxs-lookup"><span data-stu-id="d41b5-159">When you actually register your site, those values will be present.</span></span> <span data-ttu-id="d41b5-160">你需要记下应用程序 id 和应用程序机密的值，因为你会将它们添加到你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d41b5-160">You will want to note the values for app id and app secret because you will add them to your application.</span></span>

## <a name="creating-test-users"></a><span data-ttu-id="d41b5-161">创建测试用户</span><span class="sxs-lookup"><span data-stu-id="d41b5-161">Creating test users</span></span>

<span data-ttu-id="d41b5-162">如果你不介意使用现有 Facebook 帐户来测试网站，则可以跳过此部分。</span><span class="sxs-lookup"><span data-stu-id="d41b5-162">If you do not mind using an existing Facebook account to test your site, you can skip this section.</span></span>

<span data-ttu-id="d41b5-163">可以在 Facebook 应用管理页中轻松地为应用程序创建测试用户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-163">You can easily create test users for your application within the Facebook app management page.</span></span> <span data-ttu-id="d41b5-164">你可以使用这些测试帐户登录到你的站点。</span><span class="sxs-lookup"><span data-stu-id="d41b5-164">You can use these test accounts to log in to your site.</span></span> <span data-ttu-id="d41b5-165">通过单击左侧导航窗格中的 "**角色**" 链接，然后单击 "**创建**" 链接，创建测试用户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-165">You create test users by clicking the **Roles** link in the left navigation pane and the clicking the **Create** link.</span></span>

![创建测试用户](using-oauth-providers-with-mvc/_static/image5.png)

<span data-ttu-id="d41b5-167">Facebook 站点会自动创建你请求的测试帐户数。</span><span class="sxs-lookup"><span data-stu-id="d41b5-167">The Facebook site automatically creates the number of test accounts that you request.</span></span>

## <a name="adding-application-id-and-secret-from-the-provider"></a><span data-ttu-id="d41b5-168">从提供程序中添加应用程序 ID 和密码</span><span class="sxs-lookup"><span data-stu-id="d41b5-168">Adding application id and secret from the provider</span></span>

<span data-ttu-id="d41b5-169">现在，你已从 Facebook 接收了 id 和机密，请返回到 AuthConfig 文件，并将它们作为参数值添加。</span><span class="sxs-lookup"><span data-stu-id="d41b5-169">Now that you have received the id and secret from Facebook, go back to the AuthConfig file and add them as the parameter values.</span></span> <span data-ttu-id="d41b5-170">下面显示的值不是实际值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-170">The values shown below are not real values.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a><span data-ttu-id="d41b5-171">用外部凭据登录</span><span class="sxs-lookup"><span data-stu-id="d41b5-171">Log in with external credentials</span></span>

<span data-ttu-id="d41b5-172">这就是在站点中启用外部凭据所必须执行的所有操作。</span><span class="sxs-lookup"><span data-stu-id="d41b5-172">That is all you have to do to enable external credentials in your site.</span></span> <span data-ttu-id="d41b5-173">运行应用程序，并单击右上角的 "登录" 链接。</span><span class="sxs-lookup"><span data-stu-id="d41b5-173">Run your application and click the login link in the upper right corner.</span></span> <span data-ttu-id="d41b5-174">该模板将自动识别已将 Facebook 注册为提供程序，并包括提供程序的按钮。</span><span class="sxs-lookup"><span data-stu-id="d41b5-174">The template automatically recognizes that you have registered Facebook as a provider and includes a button for the provider.</span></span> <span data-ttu-id="d41b5-175">如果注册多个提供程序，则会自动包含每个提供程序的按钮。</span><span class="sxs-lookup"><span data-stu-id="d41b5-175">If you register multiple providers, a button for each one is automatically included.</span></span>

![外部登录](using-oauth-providers-with-mvc/_static/image6.png)

<span data-ttu-id="d41b5-177">本教程不介绍如何自定义外部提供程序的 "登录" 按钮。</span><span class="sxs-lookup"><span data-stu-id="d41b5-177">This tutorial does not cover how to customize the log in buttons for the external providers.</span></span> <span data-ttu-id="d41b5-178">有关此信息，请参阅[使用 OAuth/OpenID 时自定义登录 UI](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d41b5-178">For that information, see [Customizing the login UI when using OAuth/OpenID](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).</span></span>

<span data-ttu-id="d41b5-179">单击 "Facebook" 按钮，以 Facebook 凭据登录。</span><span class="sxs-lookup"><span data-stu-id="d41b5-179">Click on the Facebook button to log in with Facebook credentials.</span></span> <span data-ttu-id="d41b5-180">当你选择一个外部提供程序时，你会被重定向到该站点并提示该服务登录。</span><span class="sxs-lookup"><span data-stu-id="d41b5-180">When you select one of the external providers, you are redirected to that site and prompted by that service to log in.</span></span>

<span data-ttu-id="d41b5-181">下图显示了 Facebook 的登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="d41b5-181">The following image shows the login screen for Facebook.</span></span> <span data-ttu-id="d41b5-182">请注意，你正在使用 Facebook 帐户登录到名为 oauthmvcexample 的站点。</span><span class="sxs-lookup"><span data-stu-id="d41b5-182">It notes that you are using your Facebook account to log in to a site named oauthmvcexample.</span></span>

![facebook 身份验证](using-oauth-providers-with-mvc/_static/image7.png)

<span data-ttu-id="d41b5-184">使用 Facebook 凭据登录后，页面将向用户通知网站将有权访问基本信息。</span><span class="sxs-lookup"><span data-stu-id="d41b5-184">After logging in with Facebook credentials, a page informs the user that the site will have access to basic information.</span></span>

![请求权限](using-oauth-providers-with-mvc/_static/image8.png)

<span data-ttu-id="d41b5-186">选择 "**转向应用**" 后，用户必须注册该站点。</span><span class="sxs-lookup"><span data-stu-id="d41b5-186">After selecting **Go to App**, the user must register for the site.</span></span> <span data-ttu-id="d41b5-187">下图显示了用户使用 Facebook 凭据登录后的注册页面。</span><span class="sxs-lookup"><span data-stu-id="d41b5-187">The following image shows the registration page after a user has logged in with Facebook credentials.</span></span> <span data-ttu-id="d41b5-188">通常，用户名以提供者的名称预先填充。</span><span class="sxs-lookup"><span data-stu-id="d41b5-188">The user name is typically pre-filled with a name from the provider.</span></span>

![register](using-oauth-providers-with-mvc/_static/image9.png)

<span data-ttu-id="d41b5-190">单击 "**注册**" 完成注册。</span><span class="sxs-lookup"><span data-stu-id="d41b5-190">Click **Register** to complete registration.</span></span> <span data-ttu-id="d41b5-191">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="d41b5-191">Close the browser.</span></span>

<span data-ttu-id="d41b5-192">你可以看到，新帐户已添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="d41b5-192">You can see that the new account has been added to your database.</span></span> <span data-ttu-id="d41b5-193">在服务器资源管理器中，打开**DefaultConnection**数据库并打开 "**表**" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="d41b5-193">In Server Explorer, open the **DefaultConnection** database and open the **Tables** folder.</span></span>

![数据库表](using-oauth-providers-with-mvc/_static/image10.png)

<span data-ttu-id="d41b5-195">右键单击 " **UserProfile** " 表，然后选择 "**显示表数据**"。</span><span class="sxs-lookup"><span data-stu-id="d41b5-195">Right-click the **UserProfile** table and select **Show Table Data**.</span></span>

![显示数据](using-oauth-providers-with-mvc/_static/image11.png)

<span data-ttu-id="d41b5-197">你将看到已添加的新帐户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-197">You will see the new account you added.</span></span> <span data-ttu-id="d41b5-198">查看**网页\_OAuthMembership**表中的数据。</span><span class="sxs-lookup"><span data-stu-id="d41b5-198">Look at the data in **webpage\_OAuthMembership** table.</span></span> <span data-ttu-id="d41b5-199">你将看到与你刚添加的帐户的外部提供程序相关的更多数据。</span><span class="sxs-lookup"><span data-stu-id="d41b5-199">You will see more data related to the external provider for the account you just added.</span></span>

<span data-ttu-id="d41b5-200">如果只想启用外部身份验证，则已完成。</span><span class="sxs-lookup"><span data-stu-id="d41b5-200">If you only want to enable external authentication, you are done.</span></span> <span data-ttu-id="d41b5-201">但是，你可以将提供程序中的信息进一步集成到新的用户注册过程中，如以下部分所示。</span><span class="sxs-lookup"><span data-stu-id="d41b5-201">However, you can further integrate information from the provider into the new user registration process, as shown in the following sections.</span></span>

## <a name="create-models-for-additional-user-information"></a><span data-ttu-id="d41b5-202">为其他用户信息创建模型</span><span class="sxs-lookup"><span data-stu-id="d41b5-202">Create models for additional user information</span></span>

<span data-ttu-id="d41b5-203">正如你在前面的部分中所看到的那样，无需检索用于内置帐户注册工作的任何其他信息。</span><span class="sxs-lookup"><span data-stu-id="d41b5-203">As you noticed in the previous sections, you do not need to retrieve any additional information for the built-in account registration to work.</span></span> <span data-ttu-id="d41b5-204">但是，大多数外部提供程序会传回有关用户的其他信息。</span><span class="sxs-lookup"><span data-stu-id="d41b5-204">However, most external providers pass back additional information about the user.</span></span> <span data-ttu-id="d41b5-205">以下各节说明如何保留该信息并将其保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="d41b5-205">The following sections show how to retain that information and save it to a database.</span></span> <span data-ttu-id="d41b5-206">具体来说，您将保留用户的全名、用户个人网页的 URI 以及一个指示 Facebook 是否验证了帐户的值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-206">Specifically, you will retain values for the user's full name, the URI of the user's personal web page, and a value that indicates whether Facebook has verified the account.</span></span>

<span data-ttu-id="d41b5-207">您将使用[Code First 迁移](https://msdn.microsoft.com/data/jj591621)添加用于存储其他用户信息的表。</span><span class="sxs-lookup"><span data-stu-id="d41b5-207">You will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) to add a table for storing additional user information.</span></span> <span data-ttu-id="d41b5-208">您要将表添加到现有数据库，因此您首先需要创建当前数据库的快照。</span><span class="sxs-lookup"><span data-stu-id="d41b5-208">You are adding the table to an existing database, so you will first need to create a snapshot of the current database.</span></span> <span data-ttu-id="d41b5-209">通过创建当前数据库的快照，稍后可以创建只包含新表的迁移。</span><span class="sxs-lookup"><span data-stu-id="d41b5-209">By creating a snapshot of the current database, you can later create a migration that contains only the new table.</span></span> <span data-ttu-id="d41b5-210">若要创建当前数据库的快照，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="d41b5-210">To create a snapshot of the current database:</span></span>

1. <span data-ttu-id="d41b5-211">打开**包管理器控制台**</span><span class="sxs-lookup"><span data-stu-id="d41b5-211">Open the **Package Manager Console**</span></span>
2. <span data-ttu-id="d41b5-212">运行命令**启用-迁移**</span><span class="sxs-lookup"><span data-stu-id="d41b5-212">Run the command **enable-migrations**</span></span>
3. <span data-ttu-id="d41b5-213">运行命令 "**添加迁移初始– IgnoreChanges** "</span><span class="sxs-lookup"><span data-stu-id="d41b5-213">Run the command **add-migration initial –IgnoreChanges**</span></span>
4. <span data-ttu-id="d41b5-214">运行命令**更新-数据库**</span><span class="sxs-lookup"><span data-stu-id="d41b5-214">Run the command **update-database**</span></span>

<span data-ttu-id="d41b5-215">现在，您将添加新属性。</span><span class="sxs-lookup"><span data-stu-id="d41b5-215">Now, you will add the new properties.</span></span> <span data-ttu-id="d41b5-216">在 "模型" 文件夹中，打开 AccountModels.cs 文件，并找到 RegisterExternalLoginModel 类。</span><span class="sxs-lookup"><span data-stu-id="d41b5-216">In the Models folder, open the AccountModels.cs file, and find the RegisterExternalLoginModel class.</span></span> <span data-ttu-id="d41b5-217">RegisterExternalLoginModel 类包含从身份验证提供程序返回的值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-217">The RegisterExternalLoginModel class holds values that come back from the authentication provider.</span></span> <span data-ttu-id="d41b5-218">添加名为 FullName 和 Link 的属性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d41b5-218">Add properties named FullName and Link, as highlighted below.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

<span data-ttu-id="d41b5-219">同样，在 AccountModels.cs 中，添加一个名为 ExtraUserInformation 的新类。</span><span class="sxs-lookup"><span data-stu-id="d41b5-219">Also in AccountModels.cs, add a new class called ExtraUserInformation.</span></span> <span data-ttu-id="d41b5-220">此类表示将在数据库中创建的新表。</span><span class="sxs-lookup"><span data-stu-id="d41b5-220">This class represents the new table which will be created in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

<span data-ttu-id="d41b5-221">在 UsersContext 类中，添加以下突出显示的代码，为新类创建 DbSet 属性。</span><span class="sxs-lookup"><span data-stu-id="d41b5-221">In the UsersContext class, add the highlighted code below to create a DbSet property for the new class.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

<span data-ttu-id="d41b5-222">你现在已准备好创建新表。</span><span class="sxs-lookup"><span data-stu-id="d41b5-222">You are now ready to create the new table.</span></span> <span data-ttu-id="d41b5-223">再次打开包管理器控制台，这一次：</span><span class="sxs-lookup"><span data-stu-id="d41b5-223">Open the Package Manager Console again and this time:</span></span>

1. <span data-ttu-id="d41b5-224">运行命令**添加迁移 AddExtraUserInformation**</span><span class="sxs-lookup"><span data-stu-id="d41b5-224">Run the command **add-migration AddExtraUserInformation**</span></span>
2. <span data-ttu-id="d41b5-225">运行命令**更新-数据库**</span><span class="sxs-lookup"><span data-stu-id="d41b5-225">Run the command **update-database**</span></span>

<span data-ttu-id="d41b5-226">新表现在存在于数据库中。</span><span class="sxs-lookup"><span data-stu-id="d41b5-226">The new table now exists in the database.</span></span>

## <a name="retrieve-the-additional-data"></a><span data-ttu-id="d41b5-227">检索其他数据</span><span class="sxs-lookup"><span data-stu-id="d41b5-227">Retrieve the additional data</span></span>

<span data-ttu-id="d41b5-228">可以通过两种方法来检索其他用户数据。</span><span class="sxs-lookup"><span data-stu-id="d41b5-228">There are two ways to retrieve additional user data.</span></span> <span data-ttu-id="d41b5-229">第一种方法是保留默认情况下在身份验证请求期间传递回的用户数据。</span><span class="sxs-lookup"><span data-stu-id="d41b5-229">The first way is to retain user data that is passed back, by default, during the authentication request.</span></span> <span data-ttu-id="d41b5-230">第二种方法是专门调用提供程序 API 并请求详细信息。</span><span class="sxs-lookup"><span data-stu-id="d41b5-230">The second way is to specifically call the provider API and request more information.</span></span> <span data-ttu-id="d41b5-231">FullName 和 Link 的值将由 Facebook 自动传回。</span><span class="sxs-lookup"><span data-stu-id="d41b5-231">Values for FullName and Link are automatically passed back by Facebook.</span></span> <span data-ttu-id="d41b5-232">一个值，该值指示 Facebook 是否已验证该帐户是通过调用 Facebook API 来检索的。</span><span class="sxs-lookup"><span data-stu-id="d41b5-232">A value that indicates whether Facebook has verified the account is retrieved through a call to the Facebook API.</span></span> <span data-ttu-id="d41b5-233">首先，填充 FullName 和 Link 的值，然后您将获得已验证的值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-233">First, you will populate values for FullName and Link, and then later, you will get the verified value.</span></span>

<span data-ttu-id="d41b5-234">若要检索其他用户数据，请打开 "**控制器**" 文件夹中的**AccountController.cs**文件。</span><span class="sxs-lookup"><span data-stu-id="d41b5-234">To retrieve the additional user data, open the **AccountController.cs** file in the **Controllers** folder.</span></span>

<span data-ttu-id="d41b5-235">此文件包含用于记录、注册和管理帐户的逻辑。</span><span class="sxs-lookup"><span data-stu-id="d41b5-235">This file contains the logic for logging, registering, and managing accounts.</span></span> <span data-ttu-id="d41b5-236">具体而言，请注意称为**ExternalLoginCallback**和**ExternalLoginConfirmation**的方法。</span><span class="sxs-lookup"><span data-stu-id="d41b5-236">In particular, notice the methods called **ExternalLoginCallback** and **ExternalLoginConfirmation**.</span></span> <span data-ttu-id="d41b5-237">在这些方法中，你可以添加代码，以便为你的应用程序自定义外部登录操作。</span><span class="sxs-lookup"><span data-stu-id="d41b5-237">Within these methods, you can add code to customize external login operations for your application.</span></span> <span data-ttu-id="d41b5-238">**ExternalLoginCallback**方法的第一行包含：</span><span class="sxs-lookup"><span data-stu-id="d41b5-238">The first line of the **ExternalLoginCallback** method contains:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

<span data-ttu-id="d41b5-239">其他用户数据会传递回**VerifyAuthentication**方法返回的**AuthenticationResult**对象的**ExtraData**属性。</span><span class="sxs-lookup"><span data-stu-id="d41b5-239">Additional user data is passed back in the **ExtraData** property of the **AuthenticationResult** object that is returned from the **VerifyAuthentication** method.</span></span> <span data-ttu-id="d41b5-240">Facebook 客户端在**ExtraData**属性中包含以下值：</span><span class="sxs-lookup"><span data-stu-id="d41b5-240">The Facebook client contains the following values in the **ExtraData** property:</span></span>

- <span data-ttu-id="d41b5-241">id</span><span class="sxs-lookup"><span data-stu-id="d41b5-241">id</span></span>
- <span data-ttu-id="d41b5-242">NAME</span><span class="sxs-lookup"><span data-stu-id="d41b5-242">name</span></span>
- <span data-ttu-id="d41b5-243">链接</span><span class="sxs-lookup"><span data-stu-id="d41b5-243">link</span></span>
- <span data-ttu-id="d41b5-244">gender</span><span class="sxs-lookup"><span data-stu-id="d41b5-244">gender</span></span>
- <span data-ttu-id="d41b5-245">accesstoken</span><span class="sxs-lookup"><span data-stu-id="d41b5-245">accesstoken</span></span>

<span data-ttu-id="d41b5-246">其他提供程序在 ExtraData 属性中将具有类似但略有不同的数据。</span><span class="sxs-lookup"><span data-stu-id="d41b5-246">Other providers will have similar but slightly different data in the ExtraData property.</span></span>

<span data-ttu-id="d41b5-247">如果用户是站点的新用户，则将检索某些其他数据并将该数据传递到确认视图。</span><span class="sxs-lookup"><span data-stu-id="d41b5-247">If the user is new to your site, you will retrieve some the additional data and pass that data to the confirmation view.</span></span> <span data-ttu-id="d41b5-248">仅当用户是站点的新用户时，才会运行方法中的最后一个代码块。</span><span class="sxs-lookup"><span data-stu-id="d41b5-248">The last block of code in the method is run only if the user is new to your site.</span></span> <span data-ttu-id="d41b5-249">替换以下行：</span><span class="sxs-lookup"><span data-stu-id="d41b5-249">Replace the following line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

<span data-ttu-id="d41b5-250">替换为以下行：</span><span class="sxs-lookup"><span data-stu-id="d41b5-250">With this line:</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

<span data-ttu-id="d41b5-251">此更改仅包含 FullName 和 Link 属性的值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-251">This change merely includes values for the FullName and Link properties.</span></span>

<span data-ttu-id="d41b5-252">在**ExternalLoginConfirmation**方法中，按下面突出显示的代码修改代码以保存其他用户信息。</span><span class="sxs-lookup"><span data-stu-id="d41b5-252">In the **ExternalLoginConfirmation** method, modify the code as highlighted below to save the additional user information.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a><span data-ttu-id="d41b5-253">调整视图</span><span class="sxs-lookup"><span data-stu-id="d41b5-253">Adjusting the view</span></span>

<span data-ttu-id="d41b5-254">您从提供程序中检索的其他用户数据将显示在 "注册" 页中。</span><span class="sxs-lookup"><span data-stu-id="d41b5-254">The additional user data that you retrieve from the provider will be displayed in the registration page.</span></span>

<span data-ttu-id="d41b5-255">**在/** **帐户**"文件夹中，打开**ExternalLoginConfirmation**。</span><span class="sxs-lookup"><span data-stu-id="d41b5-255">In the **Views**/**Account** folder, open **ExternalLoginConfirmation.cshtml**.</span></span> <span data-ttu-id="d41b5-256">在 "用户名" 的现有字段下面，为 FullName、Link 和 PictureLink 添加字段。</span><span class="sxs-lookup"><span data-stu-id="d41b5-256">Below the existing field for user name, add fields for FullName, Link, and PictureLink.</span></span>

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

<span data-ttu-id="d41b5-257">你现在已准备好运行应用程序，并注册了附加信息已保存的新用户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-257">You are now almost ready to run the application and register a new user with the additional information saved.</span></span> <span data-ttu-id="d41b5-258">你必须有一个尚未注册到站点的帐户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-258">You must have an account that is not already registered with the site.</span></span> <span data-ttu-id="d41b5-259">你可以使用不同的测试帐户，也可以删除**UserProfile**和网页中的行， **\_OAuthMembership**表中要重用的帐户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-259">You can either use a different test account, or delete the rows in the **UserProfile** and **webpages\_OAuthMembership** tables for the account you wish to reuse.</span></span> <span data-ttu-id="d41b5-260">通过删除这些行，你将确保再次注册该帐户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-260">By deleting those rows, you will ensure that the account is registered again.</span></span>

<span data-ttu-id="d41b5-261">运行应用程序并注册新用户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-261">Run the application and register the new user.</span></span> <span data-ttu-id="d41b5-262">请注意，这次确认页面包含更多值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-262">Notice that this time the confirmation page contains more values.</span></span>

![register](using-oauth-providers-with-mvc/_static/image12.png)

<span data-ttu-id="d41b5-264">完成注册后，关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="d41b5-264">After completing registration, close the browser.</span></span> <span data-ttu-id="d41b5-265">查看数据库中的**ExtraUserInformation**表中的新值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-265">Look in the database to notice the new values in the **ExtraUserInformation** table.</span></span>

## <a name="install-nuget-package-for-facebook-api"></a><span data-ttu-id="d41b5-266">安装 Facebook API 的 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="d41b5-266">Install NuGet package for Facebook API</span></span>

<span data-ttu-id="d41b5-267">Facebook 提供了一个[API](https://developers.facebook.com/docs/reference/apis/) ，你可以调用它来执行操作。</span><span class="sxs-lookup"><span data-stu-id="d41b5-267">Facebook provides an [API](https://developers.facebook.com/docs/reference/apis/) that you can call to perform operations.</span></span> <span data-ttu-id="d41b5-268">你可以通过指示发送 HTTP 请求或使用安装 NuGet 包（有助于发送这些请求）来调用 Facebook API。</span><span class="sxs-lookup"><span data-stu-id="d41b5-268">You can call the Facebook API either by directing sending HTTP requests, or by using installing a NuGet package that facilitates sending those requests.</span></span> <span data-ttu-id="d41b5-269">本教程演示了如何使用 NuGet 包，但安装 NuGet 包并不重要。</span><span class="sxs-lookup"><span data-stu-id="d41b5-269">Using a NuGet package is shown in this tutorial, but installing NuGet package is not essential.</span></span> <span data-ttu-id="d41b5-270">本教程演示如何使用 Facebook C# SDK 包。</span><span class="sxs-lookup"><span data-stu-id="d41b5-270">This tutorial shows how to use the Facebook C# SDK package.</span></span> <span data-ttu-id="d41b5-271">还有其他 NuGet 包可帮助调用 Facebook API。</span><span class="sxs-lookup"><span data-stu-id="d41b5-271">There are other NuGet packages that assist with calling the Facebook API.</span></span>

<span data-ttu-id="d41b5-272">从 "**管理 NuGet 包**" 窗口中，选择C# Facebook SDK 包。</span><span class="sxs-lookup"><span data-stu-id="d41b5-272">From the **Manage NuGet Packages** windows, select the Facebook C# SDK package.</span></span>

![安装包](using-oauth-providers-with-mvc/_static/image13.png)

<span data-ttu-id="d41b5-274">你将使用 Facebook C# SDK 调用需要用户访问令牌的操作。</span><span class="sxs-lookup"><span data-stu-id="d41b5-274">You will use the Facebook C# SDK to call an operation that requires the access token for the user.</span></span> <span data-ttu-id="d41b5-275">下一节将演示如何获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="d41b5-275">The next section shows how to get the access token.</span></span>

## <a name="retrieve-access-token"></a><span data-ttu-id="d41b5-276">检索访问令牌</span><span class="sxs-lookup"><span data-stu-id="d41b5-276">Retrieve access token</span></span>

<span data-ttu-id="d41b5-277">大多数外部提供程序在验证用户凭据后，将返回访问令牌。</span><span class="sxs-lookup"><span data-stu-id="d41b5-277">Most external providers pass back an access token after the user's credentials are verified.</span></span> <span data-ttu-id="d41b5-278">此访问令牌非常重要，因为它使你可以调用仅适用于经过身份验证的用户的操作。</span><span class="sxs-lookup"><span data-stu-id="d41b5-278">This access token is very important because it enables you to call operations that are only available to authenticated users.</span></span> <span data-ttu-id="d41b5-279">因此，当您想要提供更多功能时，检索和存储访问令牌是必不可少的。</span><span class="sxs-lookup"><span data-stu-id="d41b5-279">Therefore, retrieving and storing the access token is essential when you want to provide more functionality.</span></span>

<span data-ttu-id="d41b5-280">根据外部提供程序，访问令牌的有效期仅限一段时间。</span><span class="sxs-lookup"><span data-stu-id="d41b5-280">Depending on the external provider, the access token may be valid for only a limited amount of time.</span></span> <span data-ttu-id="d41b5-281">若要确保你拥有有效的访问令牌，你将在每次用户登录时检索它，并将其存储为会话值，而不是将其保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="d41b5-281">To ensure that you have a valid access token, you will retrieve it each time the user logs in, and store it as a session value rather than save it to a database.</span></span>

<span data-ttu-id="d41b5-282">在**ExternalLoginCallback**方法中，访问令牌也会在**AuthenticationResult**对象的**ExtraData**属性中传回。</span><span class="sxs-lookup"><span data-stu-id="d41b5-282">In the **ExternalLoginCallback** method, the access token is also passed back in the **ExtraData** property of the **AuthenticationResult** object.</span></span> <span data-ttu-id="d41b5-283">将突出显示的代码添加到**ExternalLoginCallback** ，以将访问令牌保存到**Session**对象中。</span><span class="sxs-lookup"><span data-stu-id="d41b5-283">Add the highlighted code to **ExternalLoginCallback** to save the access token in the **Session** object.</span></span> <span data-ttu-id="d41b5-284">每次用户使用 Facebook 帐户登录时，都会运行此代码。</span><span class="sxs-lookup"><span data-stu-id="d41b5-284">This code is run every time the user logs in with a Facebook account.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

<span data-ttu-id="d41b5-285">尽管此示例从 Facebook 检索一个访问令牌，但你可以通过名为 &quot;accesstoken&quot;的同一密钥从任何外部提供商那里检索访问令牌。</span><span class="sxs-lookup"><span data-stu-id="d41b5-285">Although this example retrieves an access token from Facebook, you can retrieve the access token from any external provider through the same key named &quot;accesstoken&quot;.</span></span>

## <a name="logging-off"></a><span data-ttu-id="d41b5-286">注销</span><span class="sxs-lookup"><span data-stu-id="d41b5-286">Logging off</span></span>

<span data-ttu-id="d41b5-287">默认的**注销**方法会将用户记录在应用程序之外，但不会将用户从外部提供程序中注销。</span><span class="sxs-lookup"><span data-stu-id="d41b5-287">The default **LogOff** method logs the user out of your application, but does not log the user out of the external provider.</span></span> <span data-ttu-id="d41b5-288">若要将用户从 Facebook 注销，并在用户注销后阻止令牌持续，你可以将以下突出显示的代码添加到 AccountController 中的**注销**方法。</span><span class="sxs-lookup"><span data-stu-id="d41b5-288">To log the user out of Facebook, and prevent the token from persisting after the user has logged off, you can add the following highlighted code to the **LogOff** method in the AccountController.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

<span data-ttu-id="d41b5-289">在 `next` 参数中提供的值是用户注销 Facebook 后要使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="d41b5-289">The value you provide in the `next` parameter is the URL to use after the user has logged out of Facebook.</span></span> <span data-ttu-id="d41b5-290">在本地计算机上进行测试时，应为本地站点提供正确的端口号。</span><span class="sxs-lookup"><span data-stu-id="d41b5-290">When testing on your local computer, you would provide the correct port number for your local site.</span></span> <span data-ttu-id="d41b5-291">在生产环境中，你将提供一个默认页面，如 contoso.com。</span><span class="sxs-lookup"><span data-stu-id="d41b5-291">In production, you would provide a default page, such as contoso.com.</span></span>

## <a name="retrieve-user-information-that-requires-the-access-token"></a><span data-ttu-id="d41b5-292">检索需要访问令牌的用户信息</span><span class="sxs-lookup"><span data-stu-id="d41b5-292">Retrieve user information that requires the access token</span></span>

<span data-ttu-id="d41b5-293">现在，你已存储访问令牌并安装了 Facebook C# SDK 包，可以将它们一起用于请求 facebook 中的其他用户信息。</span><span class="sxs-lookup"><span data-stu-id="d41b5-293">Now that you have stored the access token and installed the Facebook C# SDK package, you can use them together to request additional user information from Facebook.</span></span> <span data-ttu-id="d41b5-294">在**ExternalLoginConfirmation**方法中，通过传递访问令牌的值来创建**FacebookClient**类的实例。</span><span class="sxs-lookup"><span data-stu-id="d41b5-294">In the **ExternalLoginConfirmation** method, create an instance of the **FacebookClient** class by passing the value of the access token.</span></span> <span data-ttu-id="d41b5-295">请求经过身份验证的当前用户的**验证**属性的值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-295">Request the value of the **verified** property for the current, authenticated user.</span></span> <span data-ttu-id="d41b5-296">**验证**的属性指示 Facebook 是否已通过某种其他方式验证了帐户，如将消息发送到手机。</span><span class="sxs-lookup"><span data-stu-id="d41b5-296">The **verified** property indicates whether Facebook has validated the account through some other means, such as sending a message to a cell phone.</span></span> <span data-ttu-id="d41b5-297">将该值保存在数据库中。</span><span class="sxs-lookup"><span data-stu-id="d41b5-297">Save this value in the database.</span></span>

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

<span data-ttu-id="d41b5-298">您将再次需要为用户删除数据库中的记录，或者使用其他 Facebook 帐户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-298">You will again need to either delete the records in the database for the user, or use a different Facebook account.</span></span>

<span data-ttu-id="d41b5-299">运行应用程序，并注册新用户。</span><span class="sxs-lookup"><span data-stu-id="d41b5-299">Run the application, and register the new user.</span></span> <span data-ttu-id="d41b5-300">查看**ExtraUserInformation**表，查看已验证属性的值。</span><span class="sxs-lookup"><span data-stu-id="d41b5-300">Look at the **ExtraUserInformation** table to see the value for the Verified property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d41b5-301">结束语</span><span class="sxs-lookup"><span data-stu-id="d41b5-301">Conclusion</span></span>

<span data-ttu-id="d41b5-302">在本教程中，已创建了一个与 Facebook 集成的、用于用户身份验证和注册数据的站点。</span><span class="sxs-lookup"><span data-stu-id="d41b5-302">In this tutorial, you created a site that is integrated with Facebook for user authentication and registration data.</span></span> <span data-ttu-id="d41b5-303">已了解为 MVC 4 web 应用程序设置的默认行为，以及如何自定义该默认行为。</span><span class="sxs-lookup"><span data-stu-id="d41b5-303">You learned about the default behavior that is set up for MVC 4 web application, and how to customize that default behavior.</span></span>

## <a name="related-topics"></a><span data-ttu-id="d41b5-304">相关主题</span><span class="sxs-lookup"><span data-stu-id="d41b5-304">Related topics</span></span>

- [<span data-ttu-id="d41b5-305">创建具有身份验证和 SQL 数据库的 ASP.NET MVC 应用程序并将其部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="d41b5-305">Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service</span></span>](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)
