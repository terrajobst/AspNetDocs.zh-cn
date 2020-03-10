---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: 通过 Windows 身份验证对用户进行身份验证（VB） |Microsoft Docs
author: microsoft
description: 了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。 了解如何在应用程序的 web co 中启用 Windows 身份验证 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: aa64b1f9ef6461a81611ca066310dca2d545baa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506240"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a><span data-ttu-id="aa03f-104">使用 Windows 身份验证对用户进行身份验证 (VB)</span><span class="sxs-lookup"><span data-stu-id="aa03f-104">Authenticating Users with Windows Authentication (VB)</span></span>

<span data-ttu-id="aa03f-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="aa03f-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="aa03f-106">了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-106">Learn how to use Windows authentication in the context of an MVC application.</span></span> <span data-ttu-id="aa03f-107">了解如何在应用程序的 web 配置文件中启用 Windows 身份验证，以及如何使用 IIS 配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-107">You learn how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="aa03f-108">最后，你将了解如何使用 [授权] 属性将对控制器操作的访问限制为特定的 Windows 用户或组。</span><span class="sxs-lookup"><span data-stu-id="aa03f-108">Finally, you learn how to use the [Authorize] attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

<span data-ttu-id="aa03f-109">本教程的目的是介绍如何利用 Internet Information Services 中内置的安全功能来保护 MVC 应用程序中的视图。</span><span class="sxs-lookup"><span data-stu-id="aa03f-109">The goal of this tutorial is to explain how you can take advantage of the security features built into Internet Information Services to password protect the views in your MVC applications.</span></span> <span data-ttu-id="aa03f-110">了解如何允许仅由特定 Windows 用户或特定 Windows 组成员的用户调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="aa03f-110">You learn how to allow controller actions to be invoked only by particular Windows users or users who are members of particular Windows groups.</span></span>

<span data-ttu-id="aa03f-111">在构建内部公司网站（intranet 站点）时，如果希望用户能够在访问网站时使用其标准的 Windows 用户名和密码，则使用 Windows 身份验证是非常有意义的。</span><span class="sxs-lookup"><span data-stu-id="aa03f-111">Using Windows authentication makes sense when you are building an internal company website (an intranet site) and you want your users to be able to use their standard Windows user names and passwords when accessing the website.</span></span> <span data-ttu-id="aa03f-112">如果要构建面向外的网站（Internet 网站），请考虑改用 Forms 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-112">If you are building an outwards facing website (an Internet website) consider using Forms authentication instead.</span></span>

#### <a name="enabling-windows-authentication"></a><span data-ttu-id="aa03f-113">启用 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="aa03f-113">Enabling Windows Authentication</span></span>

<span data-ttu-id="aa03f-114">创建新的 ASP.NET MVC 应用程序时，默认情况下不启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-114">When you create a new ASP.NET MVC application, Windows authentication is not enabled by default.</span></span> <span data-ttu-id="aa03f-115">Forms 身份验证是为 MVC 应用程序启用的默认身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="aa03f-115">Forms authentication is the default authentication type enabled for MVC applications.</span></span> <span data-ttu-id="aa03f-116">必须通过修改 MVC 应用程序的 web 配置（web.config）文件来启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-116">You must enable Windows authentication by modifying your MVC application's web configuration (web.config) file.</span></span> <span data-ttu-id="aa03f-117">找到 &lt;authentication&gt; 部分，并将其修改为使用 Windows 而不是 Forms 身份验证，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aa03f-117">Find the &lt;authentication&gt; section and modify it to use Windows instead of Forms authentication like this:</span></span>

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

<span data-ttu-id="aa03f-118">启用 Windows 身份验证后，web 服务器将负责对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-118">When you enable Windows authentication, your web server becomes responsible for authenticating users.</span></span> <span data-ttu-id="aa03f-119">通常，在创建和部署 ASP.NET MVC 应用程序时，可以使用两种不同类型的 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="aa03f-119">Typically, there are two different types of web servers that you use when creating and deploying an ASP.NET MVC application.</span></span>

<span data-ttu-id="aa03f-120">首先，在开发 MVC 应用程序时，使用 Visual Studio 附带的 ASP.NET 开发 Web 服务器。</span><span class="sxs-lookup"><span data-stu-id="aa03f-120">First, while developing an MVC application, you use the ASP.NET Development Web Server included with Visual Studio.</span></span> <span data-ttu-id="aa03f-121">默认情况下，ASP.NET 开发 Web 服务器在当前 Windows 帐户的上下文中执行所有页面（你用于登录 Windows 的任何帐户）。</span><span class="sxs-lookup"><span data-stu-id="aa03f-121">By default, the ASP.NET Development Web Server executes all pages in the context of the current Windows account (whatever account you used to log into Windows).</span></span>

<span data-ttu-id="aa03f-122">ASP.NET 开发 Web 服务器还支持 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-122">The ASP.NET Development Web Server also supports NTLM authentication.</span></span> <span data-ttu-id="aa03f-123">可以通过在 "解决方案资源管理器" 窗口中右键单击项目名称，然后选择 "属性" 来启用 NTLM 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-123">You can enable NTLM authentication by right-clicking the name of your project in the Solution Explorer window and selecting Properties.</span></span> <span data-ttu-id="aa03f-124">接下来，选择 "Web" 选项卡并选中 "NTLM" 复选框（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="aa03f-124">Next, select the Web tab and check the NTLM checkbox (see Figure 1).</span></span>

<span data-ttu-id="aa03f-125">**图1–为 ASP.NET 开发 Web 服务器启用 NTLM 身份验证**</span><span class="sxs-lookup"><span data-stu-id="aa03f-125">**Figure 1 – Enabling NTLM authentication for the ASP.NET Development Web Server**</span></span>

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

<span data-ttu-id="aa03f-127">对于生产 web 应用程序，您可以使用 IIS 作为 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="aa03f-127">For a production web application, on the hand, you use IIS as your web server.</span></span> <span data-ttu-id="aa03f-128">IIS 支持多种身份验证类型，包括：</span><span class="sxs-lookup"><span data-stu-id="aa03f-128">IIS supports several types of authentication including:</span></span>

- <span data-ttu-id="aa03f-129">基本身份验证-定义为 HTTP 1.0 协议的一部分。</span><span class="sxs-lookup"><span data-stu-id="aa03f-129">Basic Authentication – Defined as part of the HTTP 1.0 protocol.</span></span> <span data-ttu-id="aa03f-130">在 Internet 上以明文（Base64 编码）发送用户名和密码。</span><span class="sxs-lookup"><span data-stu-id="aa03f-130">Sends user names and passwords in clear text (Base64 encoded) across the Internet.</span></span> <span data-ttu-id="aa03f-131">-摘要式身份验证–通过 internet 发送密码的哈希，而不是密码本身。</span><span class="sxs-lookup"><span data-stu-id="aa03f-131">- Digest Authentication – Sends a hash of a password, instead of the password itself, across the internet.</span></span> <span data-ttu-id="aa03f-132">-集成 Windows （NTLM）身份验证-使用 Windows 在 intranet 环境中使用的最佳身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="aa03f-132">- Integrated Windows (NTLM) Authentication – The best type of authentication to use in intranet environments using windows.</span></span> <span data-ttu-id="aa03f-133">-证书身份验证-使用客户端证书启用身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-133">- Certificate Authentication – Enables authentication using a client-side certificate.</span></span> <span data-ttu-id="aa03f-134">证书映射到 Windows 用户帐户。</span><span class="sxs-lookup"><span data-stu-id="aa03f-134">The certificate maps to a Windows user account.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="aa03f-135">有关这些不同类型的身份验证的更详细概述，请参阅[https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。</span><span class="sxs-lookup"><span data-stu-id="aa03f-135">For a more detailed overview of these different types of authentication, see [https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx).</span></span>

<span data-ttu-id="aa03f-136">您可以使用 Internet Information Services Manager 启用特定类型的身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-136">You can use Internet Information Services Manager to enable a particular type of authentication.</span></span> <span data-ttu-id="aa03f-137">请注意，所有类型的身份验证在每个操作系统中都不可用。</span><span class="sxs-lookup"><span data-stu-id="aa03f-137">Be aware that all types of authentication are not available in the case of every operating system.</span></span> <span data-ttu-id="aa03f-138">此外，如果您将 IIS 7.0 与 Windows Vista 一起使用，则在 Internet Information Services 管理器中显示之前，您将需要启用不同类型的 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-138">Furthermore, if you are using IIS 7.0 with Windows Vista, you will need to enable the different types of Windows authentication before they appear in the Internet Information Services Manager.</span></span> <span data-ttu-id="aa03f-139">打开 "**控制面板"、"程序"、"程序和功能"、"打开或关闭 Windows 功能**"，然后展开 "Internet Information Services" 节点（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="aa03f-139">Open **Control Panel, Programs, Programs and Features, Turn Windows features on or off**, and expand the Internet Information Services node (see Figure 2).</span></span>

<span data-ttu-id="aa03f-140">**图 2-启用 Windows IIS 功能**</span><span class="sxs-lookup"><span data-stu-id="aa03f-140">**Figure 2 – Enabling Windows IIS features**</span></span>

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

<span data-ttu-id="aa03f-142">使用 Internet Information Services，可以启用或禁用不同类型的身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-142">Using Internet Information Services, you can enable or disable different types of authentication.</span></span> <span data-ttu-id="aa03f-143">例如，图3说明了如何在使用 IIS 7.0 时禁用匿名身份验证和启用集成的 Windows （NTLM）身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-143">For example, Figure 3 illustrates disabling anonymous authentication and enabling Integrated Windows (NTLM) authentication when using IIS 7.0.</span></span>

<span data-ttu-id="aa03f-144">**图 3-启用集成 Windows 身份验证**</span><span class="sxs-lookup"><span data-stu-id="aa03f-144">**Figure 3 – Enabling Integrated Windows Authentication**</span></span>

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a><span data-ttu-id="aa03f-146">授权 Windows 用户和组</span><span class="sxs-lookup"><span data-stu-id="aa03f-146">Authorizing Windows Users and Groups</span></span>

<span data-ttu-id="aa03f-147">启用 Windows 身份验证后，可以使用 &lt;授权&gt; 属性控制对控制器或控制器操作的访问。</span><span class="sxs-lookup"><span data-stu-id="aa03f-147">After you enable Windows authentication, you can use the &lt;Authorize&gt; attribute to control access to controllers or controller actions.</span></span> <span data-ttu-id="aa03f-148">此属性可应用于整个 MVC 控制器或特定控制器操作。</span><span class="sxs-lookup"><span data-stu-id="aa03f-148">This attribute can be applied to an entire MVC controller or a particular controller action.</span></span>

<span data-ttu-id="aa03f-149">例如，列表1中的 Home 控制器公开了三个名为 Index （）、CompanySecrets （）和 StephenSecrets （）的操作。</span><span class="sxs-lookup"><span data-stu-id="aa03f-149">For example, the Home controller in Listing 1 exposes three actions named Index(), CompanySecrets(), and StephenSecrets().</span></span> <span data-ttu-id="aa03f-150">任何人都可以调用 Index （）操作。</span><span class="sxs-lookup"><span data-stu-id="aa03f-150">Anyone can invoke the Index() action.</span></span> <span data-ttu-id="aa03f-151">但是，只有 Windows 本地管理器组的成员可以调用 CompanySecrets （）操作。</span><span class="sxs-lookup"><span data-stu-id="aa03f-151">However, only members of the Windows local Managers group can invoke the CompanySecrets() action.</span></span> <span data-ttu-id="aa03f-152">最后，只有名为 Stephen 的 Windows 域用户（在 Redmond 域中）才能调用 StephenSecrets （）操作。</span><span class="sxs-lookup"><span data-stu-id="aa03f-152">Finally, only the Windows domain user named Stephen (in the Redmond domain) can invoke the StephenSecrets() action.</span></span>

<span data-ttu-id="aa03f-153">**列表1– Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="aa03f-153">**Listing 1 – Controllers\HomeController.vb**</span></span>

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> <span data-ttu-id="aa03f-154">由于 Windows 用户帐户控制（UAC），与 Windows Vista 或 Windows Server 2008 一起使用时，本地管理员组的行为与其他组不同。</span><span class="sxs-lookup"><span data-stu-id="aa03f-154">Because of Windows User Account Control (UAC), when working with Windows Vista or Windows Server 2008, the local Administrators group will behave differently than other groups.</span></span> <span data-ttu-id="aa03f-155">除非你修改计算机的 UAC 设置，否则 &lt;授权&gt; 属性将无法正确识别本地 Administrators 组的成员。</span><span class="sxs-lookup"><span data-stu-id="aa03f-155">The &lt;Authorize&gt; attribute won't correctly recognize a member of the local Administrators group unless you modify your computer's UAC settings.</span></span>

<span data-ttu-id="aa03f-156">如果在不是正确权限的情况下尝试调用控制器操作，就会发生什么情况，具体取决于启用的身份验证类型。</span><span class="sxs-lookup"><span data-stu-id="aa03f-156">Exactly what happens when you attempt to invoke a controller action without being the right permissions depends on the type of authentication enabled.</span></span> <span data-ttu-id="aa03f-157">默认情况下，使用 ASP.NET 开发服务器时，只需获取一个空白页。</span><span class="sxs-lookup"><span data-stu-id="aa03f-157">By default, when using the ASP.NET Development Server, you simply get a blank page.</span></span> <span data-ttu-id="aa03f-158">该页提供了**401 未授权**的 HTTP 响应状态。</span><span class="sxs-lookup"><span data-stu-id="aa03f-158">The page is served with a **401 Not Authorized** HTTP Response Status.</span></span>

<span data-ttu-id="aa03f-159">另一方面，如果你在使用 IIS 时禁用了匿名身份验证，并且启用了基本身份验证，则每次请求受保护的页时都将继续获取登录对话框提示（请参阅图4）。</span><span class="sxs-lookup"><span data-stu-id="aa03f-159">If, on the other hand, you are using IIS with Anonymous authentication disabled and Basic authentication enabled, then you keep getting a login dialog prompt each time you request the protected page (see Figure 4).</span></span>

<span data-ttu-id="aa03f-160">**图4– "基本身份验证登录" 对话框**</span><span class="sxs-lookup"><span data-stu-id="aa03f-160">**Figure 4 – Basic authentication login dialog**</span></span>

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a><span data-ttu-id="aa03f-162">摘要</span><span class="sxs-lookup"><span data-stu-id="aa03f-162">Summary</span></span>

<span data-ttu-id="aa03f-163">本教程介绍了如何在 ASP.NET MVC 应用程序的上下文中使用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-163">This tutorial explained how you can use Windows authentication in the context of an ASP.NET MVC application.</span></span> <span data-ttu-id="aa03f-164">已了解如何在应用程序的 web 配置文件中启用 Windows 身份验证，以及如何使用 IIS 配置身份验证。</span><span class="sxs-lookup"><span data-stu-id="aa03f-164">You learned how to enable Windows authentication within your application's web configuration file and how to configure authentication with IIS.</span></span> <span data-ttu-id="aa03f-165">最后，你已了解如何使用 &lt;授权&gt; 属性将对控制器操作的访问限制为特定的 Windows 用户或组。</span><span class="sxs-lookup"><span data-stu-id="aa03f-165">Finally, you learned how to use the &lt;Authorize&gt; attribute to restrict access to controller actions to particular Windows users or groups.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="aa03f-166">[上一页](authenticating-users-with-forms-authentication-vb.md)
> [下一页](preventing-javascript-injection-attacks-vb.md)</span><span class="sxs-lookup"><span data-stu-id="aa03f-166">[Previous](authenticating-users-with-forms-authentication-vb.md)
[Next](preventing-javascript-injection-attacks-vb.md)</span></span>
