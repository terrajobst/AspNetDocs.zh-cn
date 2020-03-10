---
uid: web-api/overview/security/external-authentication-services
title: 带有 ASP.NET Web API （C#）的外部身份验证服务 |Microsoft Docs
author: rmcmurray
description: 介绍如何使用中的外部身份验证服务 ASP.NET Web API。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447416"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a><span data-ttu-id="3ad2a-103">带 ASP.NET Web API 的外部身份验证C#服务（）</span><span class="sxs-lookup"><span data-stu-id="3ad2a-103">External Authentication Services with ASP.NET Web API (C#)</span></span>

<span data-ttu-id="3ad2a-104">Visual Studio 2017 和 ASP.NET 4.7.2 展开了[单页面应用程序](../../../single-page-application/index.md)（SPA）和[Web API](../../index.md)服务的安全选项，以与外部身份验证服务（包括多个 OAuth/OpenID 和社交媒体身份验证服务）集成： Microsoft 帐户、Twitter、Facebook 和 Google。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-104">Visual Studio 2017 and ASP.NET 4.7.2 expand the security options for [Single Page Applications](../../../single-page-application/index.md) (SPA) and [Web API](../../index.md) services to integrate with external authentication services, which include several OAuth/OpenID and social media authentication services: Microsoft Accounts, Twitter, Facebook, and Google.</span></span>  

### <a name="in-this-walkthrough"></a><span data-ttu-id="3ad2a-105">本演练中</span><span class="sxs-lookup"><span data-stu-id="3ad2a-105">In this Walkthrough</span></span>

- [<span data-ttu-id="3ad2a-106">使用外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="3ad2a-106">Using External Authentication Services</span></span>](#USING)
- [<span data-ttu-id="3ad2a-107">创建示例 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="3ad2a-107">Creating the Sample Web Application</span></span>](#SAMPLE)
- [<span data-ttu-id="3ad2a-108">启用 Facebook 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ad2a-108">Enabling Facebook Authentication</span></span>](#FACEBOOK)
- [<span data-ttu-id="3ad2a-109">启用 Google 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ad2a-109">Enabling Google Authentication</span></span>](#GOOGLE)
- [<span data-ttu-id="3ad2a-110">启用 Microsoft 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ad2a-110">Enabling Microsoft Authentication</span></span>](#MICROSOFT)
- [<span data-ttu-id="3ad2a-111">启用 Twitter 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ad2a-111">Enabling Twitter Authentication</span></span>](#TWITTER)
- [<span data-ttu-id="3ad2a-112">其他信息</span><span class="sxs-lookup"><span data-stu-id="3ad2a-112">Additional Information</span></span>](#MOREINFO)

    - [<span data-ttu-id="3ad2a-113">合并外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="3ad2a-113">Combining External Authentication Services</span></span>](#COMBINE)
    - [<span data-ttu-id="3ad2a-114">将 IIS Express 配置为使用完全限定的域名</span><span class="sxs-lookup"><span data-stu-id="3ad2a-114">Configuring IIS Express to use a Fully Qualified Domain Name</span></span>](#FQDN)
    - [<span data-ttu-id="3ad2a-115">如何获取 Microsoft 身份验证的应用程序设置</span><span class="sxs-lookup"><span data-stu-id="3ad2a-115">How to Obtain your Application Settings for Microsoft Authentication</span></span>](#OBTAIN)
    - [<span data-ttu-id="3ad2a-116">可选：禁用本地注册</span><span class="sxs-lookup"><span data-stu-id="3ad2a-116">Optional: Disable Local Registration</span></span>](#DISABLE)

### <a name="prerequisites"></a><span data-ttu-id="3ad2a-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="3ad2a-117">Prerequisites</span></span>

<span data-ttu-id="3ad2a-118">若要执行本演练中的示例，需要具备以下各项：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-118">To follow the examples in this walkthrough, you need to have the following:</span></span>

- <span data-ttu-id="3ad2a-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="3ad2a-119">Visual Studio 2017</span></span>
- <span data-ttu-id="3ad2a-120">一个开发人员帐户，其中包含以下社交媒体身份验证服务之一的应用程序标识符和密钥：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-120">A developer account with the application identifier and secret key for one of the following social media authentication services:</span></span>

  - <span data-ttu-id="3ad2a-121">Microsoft 帐户（[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)）</span><span class="sxs-lookup"><span data-stu-id="3ad2a-121">Microsoft Accounts ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))</span></span>
  - <span data-ttu-id="3ad2a-122">Twitter （[https://dev.twitter.com/](https://dev.twitter.com/)）</span><span class="sxs-lookup"><span data-stu-id="3ad2a-122">Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))</span></span>
  - <span data-ttu-id="3ad2a-123">Facebook （[https://developers.facebook.com/](https://developers.facebook.com/)）</span><span class="sxs-lookup"><span data-stu-id="3ad2a-123">Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))</span></span>
  - <span data-ttu-id="3ad2a-124">Google （[https://developers.google.com/](https://developers.google.com)）</span><span class="sxs-lookup"><span data-stu-id="3ad2a-124">Google ([https://developers.google.com/](https://developers.google.com))</span></span>

<a id="USING"></a>
## <a name="using-external-authentication-services"></a><span data-ttu-id="3ad2a-125">使用外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="3ad2a-125">Using External Authentication Services</span></span>

<span data-ttu-id="3ad2a-126">目前可供 web 开发人员使用的外部身份验证服务丰富，有助于在创建新的 web 应用程序时缩短开发时间。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-126">The abundance of external authentication services that are currently available to web developers help to reduce development time when creating new web applications.</span></span> <span data-ttu-id="3ad2a-127">Web 用户通常有多个现有帐户用于常用 web 服务和社交媒体网站，因此，当 web 应用程序从外部 web 服务或社交媒体网站实施身份验证服务时，它将保存创建身份验证实现需要花费一些时间。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-127">Web users typically have several existing accounts for popular web services and social media websites, therefore when a web application implements the authentication services from an external web service or social media website, it saves the development time that would have been spent creating an authentication implementation.</span></span> <span data-ttu-id="3ad2a-128">使用外部身份验证服务可以使最终用户不必为你的 web 应用程序创建另一个帐户，也不必记住其他用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-128">Using an external authentication service saves end users from having to create another account for your web application, and also from having to remember another username and password.</span></span>

<span data-ttu-id="3ad2a-129">过去，开发人员有两种选择：创建自己的身份验证实现，或了解如何将外部身份验证服务集成到其应用程序中。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-129">In the past, developers have had two choices: create their own authentication implementation, or learn how to integrate an external authentication service into their applications.</span></span> <span data-ttu-id="3ad2a-130">在最基本的层面上，下图演示了一个简单的用户代理（web 浏览器）请求流，该请求流请求配置为使用外部身份验证服务的 web 应用程序中的信息：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-130">At the most basic level, the following diagram illustrates a simple request flow for a user agent (web browser) that is requesting information from a web application that is configured to use an external authentication service:</span></span>

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

<span data-ttu-id="3ad2a-131">在前面的关系图中，用户代理（或此示例中的 web 浏览器）向 web 应用程序发出请求，该请求将 web 浏览器重定向到外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-131">In the preceding diagram, the user agent (or web browser in this example) makes a request to a web application, which redirects the web browser to an external authentication service.</span></span> <span data-ttu-id="3ad2a-132">用户代理将其凭据发送到外部身份验证服务，并且如果用户代理已成功通过身份验证，则外部身份验证服务会将用户代理重定向到原始 web 应用程序，该应用程序的用户代理将发送到 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-132">The user agent sends its credentials to the external authentication service, and if the user agent has successfully authenticated, the external authentication service will redirect the user agent to the original web application with some form of token which the user agent will send to the web application.</span></span> <span data-ttu-id="3ad2a-133">Web 应用程序将使用令牌来验证是否已成功通过外部身份验证服务对用户代理进行了身份验证，并且 web 应用程序可以使用令牌来收集有关用户代理的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-133">The web application will use the token to verify that the user agent has been successfully authenticated by the external authentication service, and the web application may use the token to gather more information about the user agent.</span></span> <span data-ttu-id="3ad2a-134">一旦应用程序处理完用户代理的信息，web 应用程序就会根据其授权设置向用户代理返回适当的响应。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-134">Once the application is done processing the user agent's information, the web application will return the appropriate response to the user agent based on its authorization settings.</span></span>

<span data-ttu-id="3ad2a-135">在第二个示例中，用户代理与 web 应用程序和外部授权服务器协商，web 应用程序与外部授权服务器进行其他通信以检索有关用户的其他信息代理商</span><span class="sxs-lookup"><span data-stu-id="3ad2a-135">In this second example, the user agent negotiates with the web application and external authorization server, and the web application performs additional communication with the external authorization server to retrieve additional information about the user agent:</span></span>

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

<span data-ttu-id="3ad2a-136">Visual Studio 2017 和 ASP.NET 4.7.2 通过为以下身份验证服务提供内置集成，使开发人员可以更轻松地与外部身份验证服务集成：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-136">Visual Studio 2017 and ASP.NET 4.7.2 make integration with external authentication services easier for developers by providing built-in integration for the following authentication services:</span></span>

- <span data-ttu-id="3ad2a-137">Facebook</span><span class="sxs-lookup"><span data-stu-id="3ad2a-137">Facebook</span></span>
- <span data-ttu-id="3ad2a-138">Google</span><span class="sxs-lookup"><span data-stu-id="3ad2a-138">Google</span></span>
- <span data-ttu-id="3ad2a-139">Microsoft 帐户（Windows Live ID 帐户）</span><span class="sxs-lookup"><span data-stu-id="3ad2a-139">Microsoft Accounts (Windows Live ID accounts)</span></span>
- <span data-ttu-id="3ad2a-140">Twitter</span><span class="sxs-lookup"><span data-stu-id="3ad2a-140">Twitter</span></span>

<span data-ttu-id="3ad2a-141">本演练中的示例将演示如何使用随 Visual Studio 2017 随附的新的 ASP.NET Web 应用程序模板配置每个受支持的外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-141">The examples in this walkthrough will demonstrate how to configure each of the supported external authentication services by using the new ASP.NET Web Application template that ships with Visual Studio 2017.</span></span>

> [!NOTE]
> <span data-ttu-id="3ad2a-142">如果需要，你可能需要将 FQDN 添加到外部身份验证服务的设置。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-142">If necessary, you may need to add your FQDN to the settings for your external authentication service.</span></span> <span data-ttu-id="3ad2a-143">此要求基于某些外部身份验证服务的安全约束，要求应用程序设置中的 FQDN 与客户端使用的 FQDN 相匹配。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-143">This requirement is based on security constraints for some external authentication services which require the FQDN in your application settings to match the FQDN that is used by your clients.</span></span> <span data-ttu-id="3ad2a-144">（对于每个外部身份验证服务，此操作的步骤会很大; 您将需要查阅每个外部身份验证服务的文档，以确定是否需要这样做，以及如何配置这些设置。）如果需要将 IIS Express 配置为使用 FQDN 来测试此环境，请参阅本演练后面的[配置 IIS Express 以使用完全限定的域名](#FQDN)部分。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-144">(The steps for this will vary greatly for each external authentication service; you will need to consult the documentation for each external authentication service to see if this is required and how to configure these settings.) If you need to configure IIS Express to use an FQDN for testing this environment, see the [Configuring IIS Express to use a Fully Qualified Domain Name](#FQDN) section later in this walkthrough.</span></span>

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a><span data-ttu-id="3ad2a-145">创建示例 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="3ad2a-145">Create a Sample Web Application</span></span>

<span data-ttu-id="3ad2a-146">以下步骤将引导你完成使用 ASP.NET Web 应用程序模板创建示例应用程序的步骤，在本演练后面的部分中，你将为每个外部身份验证服务使用此示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-146">The following steps will lead you through creating a sample application by using the ASP.NET Web Application template, and you will use this sample application for each of the external authentication services later in this walkthrough.</span></span>

<span data-ttu-id="3ad2a-147">启动 Visual Studio 2017，然后从起始页中选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-147">Start Visual Studio 2017 and select **New Project** from the Start page.</span></span> <span data-ttu-id="3ad2a-148">或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-148">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

<span data-ttu-id="3ad2a-149">显示 "**新建项目**" 对话框时，选择 "**已安装**" 并展开 "**视觉对象C#** "。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-149">When the **New Project** dialog box is displayed, select **Installed** and expand **Visual C#**.</span></span> <span data-ttu-id="3ad2a-150">在 **" C#视觉对象**" 下选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-150">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="3ad2a-151">在项目模板列表中，选择 " **ASP.NET Web 应用程序（.Net Framework）** "。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-151">In the list of project templates, select **ASP.NET Web Application (.Net Framework)**.</span></span> <span data-ttu-id="3ad2a-152">输入项目的名称，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-152">Enter a name for your project and click **OK**.</span></span>

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

<span data-ttu-id="3ad2a-153">显示**新的 ASP.NET 项目**时，选择 "**单页面应用程序**" 模板，然后单击 "**创建项目**"。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-153">When the **New ASP.NET Project** is displayed, select the **Single Page Application** template and click **Create Project**.</span></span>

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

<span data-ttu-id="3ad2a-154">等待 Visual Studio 2017 创建项目。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-154">Wait as Visual Studio 2017 creates your project.</span></span>

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

<span data-ttu-id="3ad2a-155">当 Visual Studio 2017 创建完你的项目后，打开位于**应用\_Start**文件夹中的*Startup.Auth.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-155">When Visual Studio 2017 has finished creating your project, open the *Startup.Auth.cs* file that is located in the **App\_Start** folder.</span></span>

<span data-ttu-id="3ad2a-156">首次创建项目时，不会在*Startup.Auth.cs*文件中启用任何外部身份验证服务;下面演示了你的代码可能会出现的情况，其中突出显示了在其中启用外部身份验证服务的部分以及任何相关设置，以便将 Microsoft 帐户、Twitter、Facebook 或 Google 身份验证用于 ASP.NET 应用程序：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-156">When you first create the project, none of the external authentication services are enabled in *Startup.Auth.cs* file; the following illustrates what your code might resemble, with the sections highlighted for where you would enable an external authentication service and any relevant settings in order to use Microsoft Accounts, Twitter, Facebook, or Google authentication with your ASP.NET application:</span></span>

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

<span data-ttu-id="3ad2a-157">当你按 F5 生成和调试 web 应用程序时，它将显示一个登录屏幕，你会在其中看到未定义任何外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-157">When you press F5 to build and debug your web application, it will display a login screen where you will see that no external authentication services have been defined.</span></span>

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

<span data-ttu-id="3ad2a-158">在以下部分中，你将了解如何在 Visual Studio 2017 中启用与 ASP.NET 一起提供的每个外部身份验证服务。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-158">In the following sections, you will learn how to enable each of the external authentication services that are provided with ASP.NET in Visual Studio 2017.</span></span>

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a><span data-ttu-id="3ad2a-159">启用 Facebook 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ad2a-159">Enabling Facebook authentication</span></span>

<span data-ttu-id="3ad2a-160">使用 Facebook 身份验证要求你创建 Facebook 开发人员帐户，你的项目将需要 Facebook 中的应用程序 ID 和密钥，才能正常运行。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-160">Using Facebook authentication requires you to create a Facebook developer account, and your project will require an application ID and secret key from Facebook in order to function.</span></span> <span data-ttu-id="3ad2a-161">有关创建 Facebook 开发人员帐户和获取应用程序 ID 和机密密钥的信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-161">For information about creating a Facebook developer account and obtaining your application ID and secret key, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="3ad2a-162">获取应用程序 ID 和密钥后，请使用以下步骤为 web 应用程序启用 Facebook 身份验证：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-162">Once you have obtained your application ID and secret key, use the following steps to enable Facebook authentication for your web application:</span></span>

1. <span data-ttu-id="3ad2a-163">在 Visual Studio 2017 中打开项目后，打开*Startup.Auth.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-163">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="3ad2a-164">找到代码的 "Facebook 身份验证" 部分：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-164">Locate the Facebook authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. <span data-ttu-id="3ad2a-165">删除 &quot;//&quot; 字符取消注释突出显示的代码行，然后添加应用程序 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-165">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="3ad2a-166">添加这些参数后，可以重新编译项目：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-166">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. <span data-ttu-id="3ad2a-167">按 F5 在 web 浏览器中打开 web 应用程序时，将看到 Facebook 已定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-167">When you press F5 to open your web application in your web browser, you will see that Facebook has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. <span data-ttu-id="3ad2a-168">单击 " **facebook** " 按钮后，浏览器将重定向到 Facebook 登录页：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-168">When you click the **Facebook** button, your browser will be redirected to the Facebook login page:</span></span>

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. <span data-ttu-id="3ad2a-169">输入 Facebook 凭据并单击 "**登录**" 后，web 浏览器将重定向回 web 应用程序，该应用程序将提示你输入要与 Facebook 帐户关联的**用户名**：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-169">After you enter your Facebook credentials and click **Log in**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Facebook account:</span></span>

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. <span data-ttu-id="3ad2a-170">输入用户名并单击 "**注册**" 按钮后，你的 web 应用程序将显示 Facebook 帐户的默认**主页**：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-170">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Facebook account:</span></span>

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a><span data-ttu-id="3ad2a-171">启用 Google 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ad2a-171">Enabling Google Authentication</span></span>

<span data-ttu-id="3ad2a-172">使用 Google authentication 需要你创建 Google 开发人员帐户，你的项目将需要 Google 中的应用程序 ID 和密钥，才能正常运行。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-172">Using Google authentication requires you to create a Google developer account, and your project will require an application ID and secret key from Google in order to function.</span></span> <span data-ttu-id="3ad2a-173">有关创建 Google 开发人员帐户和获取应用程序 ID 和机密密钥的信息，请参阅[https://developers.google.com](https://developers.google.com)。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-173">For information about creating a Google developer account and obtaining your application ID and secret key, see [https://developers.google.com](https://developers.google.com).</span></span>

<span data-ttu-id="3ad2a-174">若要为 web 应用程序启用 Google 身份验证，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-174">To enable Google authentication for your web application, use the following steps:</span></span>

1. <span data-ttu-id="3ad2a-175">在 Visual Studio 2017 中打开项目后，打开*Startup.Auth.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-175">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="3ad2a-176">找到代码的 "Google 身份验证" 部分：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-176">Locate the Google authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. <span data-ttu-id="3ad2a-177">删除 &quot;//&quot; 字符取消注释突出显示的代码行，然后添加应用程序 ID 和密钥。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-177">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your application ID and secret key.</span></span> <span data-ttu-id="3ad2a-178">添加这些参数后，可以重新编译项目：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-178">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. <span data-ttu-id="3ad2a-179">按 F5 在 web 浏览器中打开 web 应用程序时，将看到 Google 已定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-179">When you press F5 to open your web application in your web browser, you will see that Google has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. <span data-ttu-id="3ad2a-180">单击 " **google** " 按钮后，浏览器将重定向到 Google 登录页：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-180">When you click the **Google** button, your browser will be redirected to the Google login page:</span></span>

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. <span data-ttu-id="3ad2a-181">输入 Google 凭据并单击 "**登录**" 后，Google 会提示你验证你的 web 应用程序是否有权访问 Google 帐户：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-181">After you enter your Google credentials and click **Sign in**, Google will prompt you to verify that your web application has permissions to access your Google account:</span></span>

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. <span data-ttu-id="3ad2a-182">单击 "**接受**" 时，web 浏览器将重定向回 web 应用程序，该应用程序将提示你输入要与 Google 帐户关联的**用户名**：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-182">When you click **Accept**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Google account:</span></span>

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. <span data-ttu-id="3ad2a-183">输入用户名并单击 "**注册**" 按钮后，你的 web 应用程序将显示 Google 帐户的默认**主页**：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-183">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Google account:</span></span>

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a><span data-ttu-id="3ad2a-184">启用 Microsoft 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ad2a-184">Enabling Microsoft Authentication</span></span>

<span data-ttu-id="3ad2a-185">Microsoft 身份验证要求您创建开发人员帐户，并需要客户端 ID 和客户端密码才能工作。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-185">Microsoft authentication requires you to create a developer account, and it requires a client ID and client secret in order to function.</span></span> <span data-ttu-id="3ad2a-186">有关创建 Microsoft 开发人员帐户和获取客户端 ID 和客户端密钥的信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-186">For information about creating a Microsoft developer account and obtaining your client ID and client secret, see [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).</span></span>

<span data-ttu-id="3ad2a-187">获取使用者密钥和使用者机密后，请使用以下步骤为你的 web 应用程序启用 Microsoft 身份验证：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-187">Once you have obtained your consumer key and consumer secret, use the following steps to enable Microsoft authentication for your web application:</span></span>

1. <span data-ttu-id="3ad2a-188">在 Visual Studio 2017 中打开项目后，打开*Startup.Auth.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-188">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="3ad2a-189">找到代码的 "Microsoft 身份验证" 部分：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-189">Locate the Microsoft authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. <span data-ttu-id="3ad2a-190">删除 &quot;//&quot; 字符取消注释突出显示的代码行，然后添加你的客户端 ID 和客户端密码。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-190">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your client ID and client secret.</span></span> <span data-ttu-id="3ad2a-191">添加这些参数后，可以重新编译项目：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-191">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. <span data-ttu-id="3ad2a-192">按 F5 在 web 浏览器中打开 web 应用程序时，将看到 Microsoft 已定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-192">When you press F5 to open your web application in your web browser, you will see that Microsoft has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. <span data-ttu-id="3ad2a-193">单击 " **microsoft** " 按钮后，浏览器将重定向到 microsoft 登录页：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-193">When you click the **Microsoft** button, your browser will be redirected to the Microsoft login page:</span></span>

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. <span data-ttu-id="3ad2a-194">输入 Microsoft 凭据并单击 "**登录**" 后，系统将提示你确认你的 web 应用程序有权访问 Microsoft 帐户：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-194">After you enter your Microsoft credentials and click **Sign in**, you will be prompted to verify that your web application has permissions to access your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. <span data-ttu-id="3ad2a-195">单击 **"是"** 后，web 浏览器将重定向回到 web 应用程序，该应用程序将提示你输入要与 Microsoft 帐户关联的**用户名**：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-195">When you click **Yes**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. <span data-ttu-id="3ad2a-196">输入用户名并单击 "**注册**" 按钮后，你的 web 应用程序将显示 Microsoft 帐户的默认**主页**：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-196">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Microsoft account:</span></span>

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a><span data-ttu-id="3ad2a-197">启用 Twitter 身份验证</span><span class="sxs-lookup"><span data-stu-id="3ad2a-197">Enabling Twitter Authentication</span></span>

<span data-ttu-id="3ad2a-198">Twitter 身份验证要求你创建开发人员帐户，并需要使用者密钥和使用者机密才能工作。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-198">Twitter authentication requires you to create a developer account, and it requires a consumer key and consumer secret in order to function.</span></span> <span data-ttu-id="3ad2a-199">有关创建 Twitter 开发人员帐户和获取使用者密钥和使用者机密的信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-199">For information about creating a Twitter developer account and obtaining your consumer key and consumer secret, see [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).</span></span>

<span data-ttu-id="3ad2a-200">获取使用者密钥和使用者机密后，请使用以下步骤为你的 web 应用程序启用 Twitter 身份验证：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-200">Once you have obtained your consumer key and consumer secret, use the following steps to enable Twitter authentication for your web application:</span></span>

1. <span data-ttu-id="3ad2a-201">在 Visual Studio 2017 中打开项目后，打开*Startup.Auth.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-201">When your project is open in Visual Studio 2017, open the *Startup.Auth.cs* file.</span></span>

2. <span data-ttu-id="3ad2a-202">找到代码的 "Twitter 身份验证" 部分：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-202">Locate the Twitter authentication section of code:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. <span data-ttu-id="3ad2a-203">删除 &quot;//&quot; 字符取消注释突出显示的代码行，然后添加使用者密钥和使用者机密。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-203">Remove the &quot;//&quot; characters to uncomment the highlighted lines of code, and then add your consumer key and consumer secret.</span></span> <span data-ttu-id="3ad2a-204">添加这些参数后，可以重新编译项目：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-204">Once you have added those parameters, you can recompile your project:</span></span>

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. <span data-ttu-id="3ad2a-205">按 F5 在 web 浏览器中打开 web 应用程序时，将看到 Twitter 已定义为外部身份验证服务：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-205">When you press F5 to open your web application in your web browser, you will see that Twitter has been defined as an external authentication service:</span></span>

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. <span data-ttu-id="3ad2a-206">单击 " **twitter** " 按钮后，浏览器将重定向到 Twitter 登录页面：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-206">When you click the **Twitter** button, your browser will be redirected to the Twitter login page:</span></span>

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. <span data-ttu-id="3ad2a-207">输入 Twitter 凭据并单击 "**授权应用**" 后，web 浏览器将重定向回 web 应用程序，该应用程序将提示你输入要与 Twitter 帐户关联的**用户名**：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-207">After you enter your Twitter credentials and click **Authorize app**, your web browser will be redirected back to your web application, which will prompt you for the **User name** that you want to associate with your Twitter account:</span></span>

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. <span data-ttu-id="3ad2a-208">输入用户名并单击 "**注册**" 按钮后，你的 web 应用程序将显示 Twitter 帐户的默认**主页**：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-208">After you have entered your user name and clicked the **Sign up** button, your web application will display the default **home page** for your Twitter account:</span></span>

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a><span data-ttu-id="3ad2a-209">其他信息</span><span class="sxs-lookup"><span data-stu-id="3ad2a-209">Additional Information</span></span>

<span data-ttu-id="3ad2a-210">有关创建使用 OAuth 和 OpenID 的应用程序的其他信息，请参阅以下 Url：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-210">For additional information about creating applications that use OAuth and OpenID, see the following URLs:</span></span>

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a><span data-ttu-id="3ad2a-211">合并外部身份验证服务</span><span class="sxs-lookup"><span data-stu-id="3ad2a-211">Combining External Authentication Services</span></span>

<span data-ttu-id="3ad2a-212">为了获得更大的灵活性，你可以同时定义多个外部身份验证服务-这允许你的 web 应用程序的用户使用任何已启用的外部身份验证服务中的帐户：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-212">For greater flexibility, you can define multiple external authentication services at the same time - this allows your web application's users to use an account from any of the enabled external authentication services:</span></span>

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a><span data-ttu-id="3ad2a-213">将 IIS Express 配置为使用完全限定的域名</span><span class="sxs-lookup"><span data-stu-id="3ad2a-213">Configure IIS Express to use a fully qualified domain name</span></span>

<span data-ttu-id="3ad2a-214">某些外部身份验证提供程序不支持使用 HTTP 地址（如 `http://localhost:port/`）来测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-214">Some external authentication providers do not support testing your application by using an HTTP address like `http://localhost:port/`.</span></span> <span data-ttu-id="3ad2a-215">若要解决此问题，可以向主机文件添加一个静态完全限定的域名（FQDN）映射，并在 Visual Studio 2017 中将项目选项配置为使用 FQDN 进行测试/调试。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-215">To work around this issue, you can add a static Fully Qualified Domain Name (FQDN) mapping to your HOSTS file and configure your project options in Visual Studio 2017 to use the FQDN for testing/debugging.</span></span> <span data-ttu-id="3ad2a-216">为此，请使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-216">To do so, use the following steps:</span></span>

- <span data-ttu-id="3ad2a-217">添加静态 FQDN 映射主机文件：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-217">Add a static FQDN mapping your HOSTS file:</span></span>

  1. <span data-ttu-id="3ad2a-218">在 Windows 中打开提升的命令提示符。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-218">Open an elevated command prompt in Windows.</span></span>
  2. <span data-ttu-id="3ad2a-219">键入以下命令：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-219">Type the following command:</span></span>

      <span data-ttu-id="3ad2a-220"><kbd>记事本%WinDir%\system32\drivers\etc\hosts</kbd></span><span class="sxs-lookup"><span data-stu-id="3ad2a-220"><kbd>notepad %WinDir%\system32\drivers\etc\hosts</kbd></span></span>
  3. <span data-ttu-id="3ad2a-221">在 HOSTS 文件中添加类似于以下内容的条目：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-221">Add an entry like the following to the HOSTS file:</span></span>

      <span data-ttu-id="3ad2a-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span><span class="sxs-lookup"><span data-stu-id="3ad2a-222"><kbd>127.0.0.1 www.wingtiptoys.com</kbd></span></span>
  4. <span data-ttu-id="3ad2a-223">保存并关闭主机文件。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-223">Save and close your HOSTS file.</span></span>

- <span data-ttu-id="3ad2a-224">将 Visual Studio 项目配置为使用 FQDN：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-224">Configure your Visual Studio project to use the FQDN:</span></span>

  1. <span data-ttu-id="3ad2a-225">在 Visual Studio 2017 中打开项目时，单击 "**项目**" 菜单，然后选择项目的属性。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-225">When your project is open in Visual Studio 2017, click the **Project** menu, and then select your project's properties.</span></span> <span data-ttu-id="3ad2a-226">例如，可以选择 " **WebApplication1 属性**"。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-226">For example, you might select **WebApplication1 Properties**.</span></span>
  2. <span data-ttu-id="3ad2a-227">选择 " **Web** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-227">Select the **Web** tab.</span></span>
  3. <span data-ttu-id="3ad2a-228">输入你的 FQDN 作为<strong>项目 Url</strong>。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-228">Enter your FQDN for the <strong>Project Url</strong>.</span></span> <span data-ttu-id="3ad2a-229">例如，如果是添加到 HOSTS 文件的 FQDN 映射，则需要输入<kbd><http://www.wingtiptoys.com></kbd> 。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-229">For example, you would enter <kbd><http://www.wingtiptoys.com></kbd> if that was the FQDN mapping that you added to your HOSTS file.</span></span>

- <span data-ttu-id="3ad2a-230">将 IIS Express 配置为使用应用程序的 FQDN：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-230">Configure IIS Express to use the FQDN for your application:</span></span>

    1. <span data-ttu-id="3ad2a-231">在 Windows 中打开提升的命令提示符。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-231">Open an elevated command prompt in Windows.</span></span>
    2. <span data-ttu-id="3ad2a-232">键入以下命令以更改到 IIS Express 文件夹：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-232">Type the following command to change to your IIS Express folder:</span></span>

        <span data-ttu-id="3ad2a-233"><kbd>cd/d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span><span class="sxs-lookup"><span data-stu-id="3ad2a-233"><kbd>cd /d &quot;%ProgramFiles%\IIS Express&quot;</kbd></span></span>
    3. <span data-ttu-id="3ad2a-234">键入以下命令，将 FQDN 添加到应用程序：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-234">Type the following command to add the FQDN to your application:</span></span>

        <span data-ttu-id="3ad2a-235"><kbd>appcmd.exe 设置配置-节： system.web/sites/+&quot;[name = ' WebApplication1 ']。[protocol = ' http '，bindingInformation = ' \*：80： wingtiptoys ']&quot;/commit： apphost</kbd></span><span class="sxs-lookup"><span data-stu-id="3ad2a-235"><kbd>appcmd.exe set config -section:system.applicationHost/sites /+&quot;[name='WebApplication1'].bindings.[protocol='http',bindingInformation='\*:80:www.wingtiptoys.com']&quot; /commit:apphost</kbd></span></span>

  <span data-ttu-id="3ad2a-236">其中， **WebApplication1**是项目的名称， **bindingInformation**包含要用于测试的端口号和 FQDN。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-236">Where **WebApplication1** is the name of your project and **bindingInformation** contains the port number and FQDN that you want to use for your testing.</span></span>

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a><span data-ttu-id="3ad2a-237">如何获取 Microsoft 身份验证的应用程序设置</span><span class="sxs-lookup"><span data-stu-id="3ad2a-237">How to Obtain your Application Settings for Microsoft Authentication</span></span>

<span data-ttu-id="3ad2a-238">将应用程序链接到 Windows Live for Microsoft 身份验证是一个简单的过程。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-238">Linking an application to Windows Live for Microsoft Authentication is a simple process.</span></span> <span data-ttu-id="3ad2a-239">如果尚未将应用程序链接到 Windows Live，可以使用以下步骤：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-239">If you have not already linked an application to Windows Live, you can use the following steps:</span></span>

1. <span data-ttu-id="3ad2a-240">浏览到[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)并在出现提示时输入 Microsoft 帐户的名称和密码，并单击 "**登录**"：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-240">Browse to [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) and enter your Microsoft account name and password when prompted, then click **Sign in**:</span></span>

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. <span data-ttu-id="3ad2a-241">选择 "**添加应用**"，并在出现提示时输入应用程序的名称，然后单击 "**创建**"：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-241">Select **Add an app** and enter the name of your application when prompted, and then click **Create**:</span></span>

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. <span data-ttu-id="3ad2a-242">在 "**名称**" 下选择你的应用，并显示其应用程序属性页。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-242">Select your app under **Name** and its application properties page appears.</span></span>

4. <span data-ttu-id="3ad2a-243">输入应用程序的重定向域。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-243">Enter the redirect domain for your application.</span></span> <span data-ttu-id="3ad2a-244">复制**应用程序 ID** ，然后在 "**应用程序机密**" 下选择 "**生成密码**"。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-244">Copy the **Application ID** and, under **Application Secrets**, select **Generate Password**.</span></span> <span data-ttu-id="3ad2a-245">复制显示的密码。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-245">Copy the password that appears.</span></span> <span data-ttu-id="3ad2a-246">应用程序 ID 和密码是你的客户端 ID 和客户端密码。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-246">The application ID and password are your client ID and client secret.</span></span> <span data-ttu-id="3ad2a-247">选择 **"确定"** ，然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-247">Select **Ok** and then **Save**.</span></span>

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a><span data-ttu-id="3ad2a-248">可选：禁用本地注册</span><span class="sxs-lookup"><span data-stu-id="3ad2a-248">Optional: Disable Local Registration</span></span>

<span data-ttu-id="3ad2a-249">当前 ASP.NET 本地注册功能不会阻止自动程序（bot）创建成员帐户;例如，使用[CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)等机器人防护和验证技术。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-249">The current ASP.NET local registration functionality does not prevent automated programs (bots) from creating member accounts; for example, by using a bot-prevention and validation technology like [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md).</span></span> <span data-ttu-id="3ad2a-250">因此，你应该在登录页上删除本地登录窗体和注册链接。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-250">Because of this, you should remove the local login form and registration link on the login page.</span></span> <span data-ttu-id="3ad2a-251">为此，请在你的项目中打开 *\_Login* ，然后注释掉本地登录面板和注册链接的行。</span><span class="sxs-lookup"><span data-stu-id="3ad2a-251">To do so, open the *\_Login.cshtml* page in your project, and then comment out the lines for the local login panel and the registration link.</span></span> <span data-ttu-id="3ad2a-252">生成的页应类似于以下代码示例：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-252">The resulting page should look like the following code sample:</span></span>

[!code-html[Main](external-authentication-services/samples/sample10.html)]

<span data-ttu-id="3ad2a-253">禁用本地登录面板和注册链接后，登录页将仅显示已启用的外部身份验证提供程序：</span><span class="sxs-lookup"><span data-stu-id="3ad2a-253">Once the local login panel and the registration link have been disabled, your login page will only display the external authentication providers that you have enabled:</span></span>

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
