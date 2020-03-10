---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: 使用身份验证和授权保护应用程序 |Microsoft Docs
author: microsoft
description: 步骤9显示了如何添加身份验证和授权以保护我们的 NerdDinner 应用程序，以便用户需要注册并登录到网站才能创建 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486422"
---
# <a name="secure-applications-using-authentication-and-authorization"></a><span data-ttu-id="58f7b-103">使用身份验证和授权保护应用程序</span><span class="sxs-lookup"><span data-stu-id="58f7b-103">Secure Applications Using Authentication and Authorization</span></span>

<span data-ttu-id="58f7b-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="58f7b-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="58f7b-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="58f7b-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="58f7b-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第9步，其中演练了如何使用 ASP.NET MVC 1 构建一个小型的、完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="58f7b-106">This is step 9 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="58f7b-107">步骤9显示了如何添加身份验证和授权来保护我们的 NerdDinner 应用程序，以便用户需要注册并登录到站点来创建新的就，并且只有托管晚餐的用户才能在以后编辑。</span><span class="sxs-lookup"><span data-stu-id="58f7b-107">Step 9 shows how to add authentication and authorization to secure our NerdDinner application, so that users need to register and login to the site to create new dinners, and only the user who is hosting a dinner can edit it later.</span></span>
> 
> <span data-ttu-id="58f7b-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="58f7b-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-9-authentication-and-authorization"></a><span data-ttu-id="58f7b-109">NerdDinner 步骤9：身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="58f7b-109">NerdDinner Step 9: Authentication and Authorization</span></span>

<span data-ttu-id="58f7b-110">现在，我们的 NerdDinner 应用程序授予访问该站点的任何人创建和编辑任何晚餐的详细信息的能力。</span><span class="sxs-lookup"><span data-stu-id="58f7b-110">Right now our NerdDinner application grants anyone visiting the site the ability to create and edit the details of any dinner.</span></span> <span data-ttu-id="58f7b-111">让我们对此进行更改，以使用户需要注册并登录到站点来创建新的就，并添加限制，以便仅托管晚餐的用户可以在以后编辑该限制。</span><span class="sxs-lookup"><span data-stu-id="58f7b-111">Let's change this so that users need to register and login to the site to create new dinners, and add a restriction so that only the user who is hosting a dinner can edit it later.</span></span>

<span data-ttu-id="58f7b-112">为此，我们将使用身份验证和授权来确保应用程序的安全。</span><span class="sxs-lookup"><span data-stu-id="58f7b-112">To enable this we'll use authentication and authorization to secure our application.</span></span>

### <a name="understanding-authentication-and-authorization"></a><span data-ttu-id="58f7b-113">了解身份验证和授权</span><span class="sxs-lookup"><span data-stu-id="58f7b-113">Understanding Authentication and Authorization</span></span>

<span data-ttu-id="58f7b-114">*身份验证*是指标识并验证访问应用程序的客户端标识的过程。</span><span class="sxs-lookup"><span data-stu-id="58f7b-114">*Authentication* is the process of identifying and validating the identity of a client accessing an application.</span></span> <span data-ttu-id="58f7b-115">更简单地说，它与确定最终用户访问网站时的身份相关。</span><span class="sxs-lookup"><span data-stu-id="58f7b-115">Put more simply, it is about identifying "who" the end-user is when they visit a website.</span></span> <span data-ttu-id="58f7b-116">ASP.NET 支持通过多种方式对浏览器用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="58f7b-116">ASP.NET supports multiple ways to authenticate browser users.</span></span> <span data-ttu-id="58f7b-117">对于 Internet web 应用程序，使用最常用的身份验证方法称为 "Forms 身份验证"。</span><span class="sxs-lookup"><span data-stu-id="58f7b-117">For Internet web applications, the most common authentication approach used is called "Forms Authentication".</span></span> <span data-ttu-id="58f7b-118">使用窗体身份验证，开发人员可以在其应用程序中创作 HTML 登录窗体，然后根据数据库或其他密码凭据存储来验证最终用户提交的用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="58f7b-118">Forms Authentication enables a developer to author an HTML login form within their application, and then validate the username/password an end-user submits against a database or other password credential store.</span></span> <span data-ttu-id="58f7b-119">如果用户名/密码组合正确，则开发人员可以要求 ASP.NET 发出加密的 HTTP cookie，以便在将来的请求中标识用户。</span><span class="sxs-lookup"><span data-stu-id="58f7b-119">If the username/password combination is correct, the developer can then ask ASP.NET to issue an encrypted HTTP cookie to identify the user across future requests.</span></span> <span data-ttu-id="58f7b-120">我们将通过 NerdDinner 应用程序使用 forms 身份验证。</span><span class="sxs-lookup"><span data-stu-id="58f7b-120">We'll by using forms authentication with our NerdDinner application.</span></span>

<span data-ttu-id="58f7b-121">*授权*是指确定经过身份验证的用户是否有权访问特定 URL/资源或执行某些操作的过程。</span><span class="sxs-lookup"><span data-stu-id="58f7b-121">*Authorization* is the process of determining whether an authenticated user has permission to access a particular URL/resource or to perform some action.</span></span> <span data-ttu-id="58f7b-122">例如，在我们的 NerdDinner 应用程序中，我们想要授权只有登录的用户才能访问 */Dinners/Create* URL 并创建新的就。</span><span class="sxs-lookup"><span data-stu-id="58f7b-122">For example, within our NerdDinner application we'll want to authorize that only users who are logged in can access the */Dinners/Create* URL and create new Dinners.</span></span> <span data-ttu-id="58f7b-123">我们还需要添加授权逻辑，以便仅托管晚餐的用户可以对其进行编辑，并拒绝对所有其他用户的编辑权限。</span><span class="sxs-lookup"><span data-stu-id="58f7b-123">We'll also want to add authorization logic so that only the user who is hosting a dinner can edit it – and deny edit access to all other users.</span></span>

### <a name="forms-authentication-and-the-accountcontroller"></a><span data-ttu-id="58f7b-124">Forms 身份验证和 AccountController</span><span class="sxs-lookup"><span data-stu-id="58f7b-124">Forms Authentication and the AccountController</span></span>

<span data-ttu-id="58f7b-125">创建新的 ASP.NET MVC 应用程序时，ASP.NET MVC 的默认 Visual Studio 项目模板会自动启用表单身份验证。</span><span class="sxs-lookup"><span data-stu-id="58f7b-125">The default Visual Studio project template for ASP.NET MVC automatically enables forms authentication when new ASP.NET MVC applications are created.</span></span> <span data-ttu-id="58f7b-126">它还自动向项目添加预先生成的帐户登录页实现，这使得在站点内集成安全性变得非常简单。</span><span class="sxs-lookup"><span data-stu-id="58f7b-126">It also automatically adds a pre-built account login page implementation to the project – which makes it really easy to integrate security within a site.</span></span>

<span data-ttu-id="58f7b-127">"默认网站"。当访问用户的用户未通过身份验证时，它会在站点的右上角显示 "登录" 链接：</span><span class="sxs-lookup"><span data-stu-id="58f7b-127">The default Site.master master page displays a "Log On" link at the top-right of the site when the user accessing it is not authenticated:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

<span data-ttu-id="58f7b-128">单击 "登录" 链接会将用户带到 */Account/LogOn* URL：</span><span class="sxs-lookup"><span data-stu-id="58f7b-128">Clicking the "Log On" link takes a user to the */Account/LogOn* URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

<span data-ttu-id="58f7b-129">尚未注册的访问者可以通过单击 "注册" 链接来执行此操作，方法是单击 "注册" 链接（将其转到 */Account/Register* URL 并允许他们输入帐户详细信息）：</span><span class="sxs-lookup"><span data-stu-id="58f7b-129">Visitors who haven't registered can do so by clicking the "Register" link – which will take them to the */Account/Register* URL and allow them to enter account details:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

<span data-ttu-id="58f7b-130">单击 "注册" 按钮将在 ASP.NET 成员资格系统中创建新用户，并使用 forms 身份验证对用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="58f7b-130">Clicking the "Register" button will create a new user within the ASP.NET Membership system, and authenticate the user onto the site using forms authentication.</span></span>

<span data-ttu-id="58f7b-131">当用户登录时，站点。主节点将更改页面的右上方，以输出 "欢迎 [username]！"</span><span class="sxs-lookup"><span data-stu-id="58f7b-131">When a user is logged-in, the Site.master changes the top-right of the page to output a "Welcome [username]!"</span></span> <span data-ttu-id="58f7b-132">消息并呈现一个 "注销" 链接，而不是 "登录" 链接。</span><span class="sxs-lookup"><span data-stu-id="58f7b-132">message and renders a "Log Off" link instead of a "Log On" one.</span></span> <span data-ttu-id="58f7b-133">单击 "注销" 链接会注销用户：</span><span class="sxs-lookup"><span data-stu-id="58f7b-133">Clicking the "Log Off" link logs out the user:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

<span data-ttu-id="58f7b-134">上述登录、注销和注册功能是在 AccountController 类中实现的，该类在创建项目时由 Visual Studio 添加到了项目中。</span><span class="sxs-lookup"><span data-stu-id="58f7b-134">The above login, logout, and registration functionality is implemented within the AccountController class that was added to our project by Visual Studio when it created the project.</span></span> <span data-ttu-id="58f7b-135">使用 \Views\Account 目录中的视图模板来实现 AccountController 的 UI：</span><span class="sxs-lookup"><span data-stu-id="58f7b-135">The UI for the AccountController is implemented using view templates within the \Views\Account directory:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

<span data-ttu-id="58f7b-136">AccountController 类使用 ASP.NET Forms Authentication 系统颁发加密的身份验证 cookie，并使用 ASP.NET 成员资格 API 来存储和验证用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="58f7b-136">The AccountController class uses the ASP.NET Forms Authentication system to issue encrypted authentication cookies, and the ASP.NET Membership API to store and validate usernames/passwords.</span></span> <span data-ttu-id="58f7b-137">ASP.NET 成员资格 API 是可扩展的，可使用任何密码凭据存储。</span><span class="sxs-lookup"><span data-stu-id="58f7b-137">The ASP.NET Membership API is extensible and enables any password credential store to be used.</span></span> <span data-ttu-id="58f7b-138">ASP.NET 附带内置成员资格提供程序实现，用于在 SQL 数据库中或 Active Directory 中存储用户名/密码。</span><span class="sxs-lookup"><span data-stu-id="58f7b-138">ASP.NET ships with built-in membership provider implementations that store username/passwords within a SQL database, or within Active Directory.</span></span>

<span data-ttu-id="58f7b-139">我们可以通过在项目根目录中打开 "web.config" 文件并查找其中 &lt;成员身份&gt; 部分来配置 NerdDinner 应用程序应使用的成员资格提供程序。</span><span class="sxs-lookup"><span data-stu-id="58f7b-139">We can configure which membership provider our NerdDinner application should use by opening the "web.config" file at the root of the project and looking for the &lt;membership&gt; section within it.</span></span> <span data-ttu-id="58f7b-140">默认情况下，在创建项目时添加的 web.config 将注册 SQL 成员资格提供程序，并将其配置为使用一个名为 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 的连接字符串来指定数据库位置。</span><span class="sxs-lookup"><span data-stu-id="58f7b-140">The default web.config added when the project was created registers the SQL membership provider, and configures it to use a connection-string named "ApplicationServices" to specify the database location.</span></span>

<span data-ttu-id="58f7b-141">默认 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 连接字符串（在 web.config 文件的 &lt;connectionStrings&gt; 部分中指定）配置为使用 SQL Express。</span><span class="sxs-lookup"><span data-stu-id="58f7b-141">The default "ApplicationServices" connection string (which is specified within the &lt;connectionStrings&gt; section of the web.config file) is configured to use SQL Express.</span></span> <span data-ttu-id="58f7b-142">它指向名为 "ASPNETDB.MDF" 的 SQL Express 数据库。MDF "的应用程序\_数据" 目录下。</span><span class="sxs-lookup"><span data-stu-id="58f7b-142">It points to a SQL Express database named "ASPNETDB.MDF" under the application's "App\_Data" directory.</span></span> <span data-ttu-id="58f7b-143">如果此数据库在应用程序中首次使用成员资格 API 时不存在，ASP.NET 将自动创建数据库并在其中预配相应的成员资格数据库架构：</span><span class="sxs-lookup"><span data-stu-id="58f7b-143">If this database doesn't exist the first time the Membership API is used within the application, ASP.NET will automatically create the database and provision the appropriate membership database schema within it:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

<span data-ttu-id="58f7b-144">如果使用的不是 SQL Express，我们想要使用完全 SQL Server 实例（或连接到远程数据库），只需在 web.config 文件中更新 "Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception" 连接字符串，并确保相应的成员身份架构已添加到它指向的数据库。</span><span class="sxs-lookup"><span data-stu-id="58f7b-144">If instead of using SQL Express we wanted to use a full SQL Server instance (or connect to a remote database), all we'd need to-do is to update the "ApplicationServices" connection string within the web.config file and make sure that the appropriate membership schema has been added to the database it points at.</span></span> <span data-ttu-id="58f7b-145">可以在 \Windows\Microsoft.NET\Framework\v2.0.50727\ 目录中运行 "aspnet\_regsql" 实用程序，以将相应的成员身份和其他 ASP.NET 应用程序服务的架构添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="58f7b-145">You can run the "aspnet\_regsql.exe" utility within the \Windows\Microsoft.NET\Framework\v2.0.50727\ directory to add the appropriate schema for membership and the other ASP.NET application services to a database.</span></span>

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a><span data-ttu-id="58f7b-146">使用 [授权] 筛选器授权/Dinners/Create URL</span><span class="sxs-lookup"><span data-stu-id="58f7b-146">Authorizing the /Dinners/Create URL using the [Authorize] filter</span></span>

<span data-ttu-id="58f7b-147">我们无需编写任何代码即可为 NerdDinner 应用程序启用安全的身份验证和帐户管理实现。</span><span class="sxs-lookup"><span data-stu-id="58f7b-147">We didn't have to write any code to enable a secure authentication and account management implementation for the NerdDinner application.</span></span> <span data-ttu-id="58f7b-148">用户可以向我们的应用程序注册新帐户，还可以登录/注销网站。</span><span class="sxs-lookup"><span data-stu-id="58f7b-148">Users can register new accounts with our application, and login/logout of the site.</span></span>

<span data-ttu-id="58f7b-149">现在，我们可以将授权逻辑添加到应用程序，并使用访问者的身份验证状态和用户名控制其在站点中可以和不能执行的操作。</span><span class="sxs-lookup"><span data-stu-id="58f7b-149">Now we can add authorization logic to the application, and use the authentication status and username of visitors to control what they can and can't do within the site.</span></span> <span data-ttu-id="58f7b-150">首先，让我们将授权逻辑添加到我们的 DinnersController 类的 "创建" 操作方法。</span><span class="sxs-lookup"><span data-stu-id="58f7b-150">Let's begin by adding authorization logic to the "Create" action methods of our DinnersController class.</span></span> <span data-ttu-id="58f7b-151">具体来说，我们将要求必须登录访问 */Dinners/Create* URL 的用户。</span><span class="sxs-lookup"><span data-stu-id="58f7b-151">Specifically, we will require that users accessing the */Dinners/Create* URL must be logged in.</span></span> <span data-ttu-id="58f7b-152">如果未登录，我们会将它们重定向到登录页，以便他们可以登录。</span><span class="sxs-lookup"><span data-stu-id="58f7b-152">If they aren't logged in we'll redirect them to the login page so that they can sign-in.</span></span>

<span data-ttu-id="58f7b-153">实现此逻辑非常简单。</span><span class="sxs-lookup"><span data-stu-id="58f7b-153">Implementing this logic is pretty easy.</span></span> <span data-ttu-id="58f7b-154">我们只需将 [授权] 筛选器属性添加到创建操作方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="58f7b-154">All we need to-do is to add an [Authorize] filter attribute to our Create action methods like so:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

<span data-ttu-id="58f7b-155">ASP.NET MVC 支持创建 "操作筛选器" 的功能，该操作筛选器可用于实现可在操作方法中以声明方式应用的可重复使用的逻辑。</span><span class="sxs-lookup"><span data-stu-id="58f7b-155">ASP.NET MVC supports the ability to create "action filters" that can be used to implement re-usable logic that can be declaratively applied to action methods.</span></span> <span data-ttu-id="58f7b-156">[授权] 筛选器是 ASP.NET MVC 提供的内置操作筛选器之一，它使开发人员能够以声明方式将授权规则应用到操作方法和控制器类。</span><span class="sxs-lookup"><span data-stu-id="58f7b-156">The [Authorize] filter is one of the built-in action filters provided by ASP.NET MVC, and it enables a developer to declaratively apply authorization rules to action methods and controller classes.</span></span>

<span data-ttu-id="58f7b-157">如果应用时不带任何参数（如上所示），[授权] 筛选器将强制执行操作方法请求的用户必须登录–并且它会自动将浏览器重定向到登录 URL （如果它们不存在）。</span><span class="sxs-lookup"><span data-stu-id="58f7b-157">When applied without any parameters (like above) the [Authorize] filter enforces that the user making the action method request must be logged in – and it will automatically redirect the browser to the login URL if they aren't.</span></span> <span data-ttu-id="58f7b-158">执行此重定向时，最初请求的 URL 将作为 querystring 参数传递（例如：/Account/LogOn？ReturnUrl =% 2fDinners% 2fCreate）。</span><span class="sxs-lookup"><span data-stu-id="58f7b-158">When doing this redirect the originally requested URL is passed as a querystring argument (for example: /Account/LogOn?ReturnUrl=%2fDinners%2fCreate).</span></span> <span data-ttu-id="58f7b-159">然后，在用户登录后，AccountController 会将用户重定向回最初请求的 URL。</span><span class="sxs-lookup"><span data-stu-id="58f7b-159">The AccountController will then redirect the user back to the originally requested URL once they login.</span></span>

<span data-ttu-id="58f7b-160">[授权] 筛选器可以指定指定 "用户" 或 "角色" 属性的功能，该属性可用于要求用户同时登录到允许用户或允许的安全角色的列表。</span><span class="sxs-lookup"><span data-stu-id="58f7b-160">The [Authorize] filter optionally supports the ability to specify a "Users" or "Roles" property that can be used to require that the user is both logged in and within a list of allowed users or a member of an allowed security role.</span></span> <span data-ttu-id="58f7b-161">例如，以下代码仅允许两个特定用户 "scottgu" 和 "billg" 访问/Dinners/Create URL：</span><span class="sxs-lookup"><span data-stu-id="58f7b-161">For example, the code below only allows two specific users, "scottgu" and "billg", to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

<span data-ttu-id="58f7b-162">不过，在代码中嵌入特定的用户名往往会变得非常容易。</span><span class="sxs-lookup"><span data-stu-id="58f7b-162">Embedding specific user names within code tends to be pretty un-maintainable though.</span></span> <span data-ttu-id="58f7b-163">更好的方法是定义代码检查的高级 "角色"，然后使用数据库或 active directory 系统将用户映射到角色（使实际用户映射列表可以从代码外部存储）。</span><span class="sxs-lookup"><span data-stu-id="58f7b-163">A better approach is to define higher-level "roles" that the code checks against, and then to map users into the role using either a database or active directory system (enabling the actual user mapping list to be stored externally from the code).</span></span> <span data-ttu-id="58f7b-164">ASP.NET 包括内置角色管理 API 以及内置角色提供程序集（包括 SQL 和 Active Directory 的内置角色提供程序集），可帮助执行此用户/角色映射。</span><span class="sxs-lookup"><span data-stu-id="58f7b-164">ASP.NET includes a built-in role management API as well as a built-in set of role providers (including ones for SQL and Active Directory) that can help perform this user/role mapping.</span></span> <span data-ttu-id="58f7b-165">然后，我们可以更新代码，以便只允许特定 "管理员" 角色中的用户访问/Dinners/Create URL：</span><span class="sxs-lookup"><span data-stu-id="58f7b-165">We could then update the code to only allow users within a specific "admin" role to access the /Dinners/Create URL:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a><span data-ttu-id="58f7b-166">创建就时使用 User.Identity.Name 属性</span><span class="sxs-lookup"><span data-stu-id="58f7b-166">Using the User.Identity.Name property when Creating Dinners</span></span>

<span data-ttu-id="58f7b-167">我们可以使用控制器基类上公开的 User.Identity.Name 属性来检索请求的当前已登录用户的用户名。</span><span class="sxs-lookup"><span data-stu-id="58f7b-167">We can retrieve the username of the currently logged-in user of a request using the User.Identity.Name property exposed on the Controller base class.</span></span>

<span data-ttu-id="58f7b-168">之前当我们实现了 Create （）操作方法的 HTTP POST 版本时，我们已将晚餐的 "HostedBy" 属性硬编码为静态字符串。</span><span class="sxs-lookup"><span data-stu-id="58f7b-168">Earlier when we implemented the HTTP-POST version of our Create() action method we had hardcoded the "HostedBy" property of the Dinner to a static string.</span></span> <span data-ttu-id="58f7b-169">现在，我们可以更新此代码以改为使用 User.Identity.Name 属性，并为创建晚餐的主机自动添加 RSVP：</span><span class="sxs-lookup"><span data-stu-id="58f7b-169">We can now update this code to instead use the User.Identity.Name property, as well as automatically add an RSVP for the host creating the Dinner:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

<span data-ttu-id="58f7b-170">由于我们已将 [授权] 特性添加到 Create （）方法，因此 ASP.NET MVC 可确保仅在用户访问/Dinners/Create URL 的用户登录到站点时才执行操作方法。</span><span class="sxs-lookup"><span data-stu-id="58f7b-170">Because we have added an [Authorize] attribute to the Create() method, ASP.NET MVC ensures that the action method only executes if the user visiting the /Dinners/Create URL is logged in on the site.</span></span> <span data-ttu-id="58f7b-171">因此，User.Identity.Name 属性值将始终包含有效的用户名。</span><span class="sxs-lookup"><span data-stu-id="58f7b-171">As such, the User.Identity.Name property value will always contain a valid username.</span></span>

### <a name="using-the-useridentityname-property-when-editing-dinners"></a><span data-ttu-id="58f7b-172">编辑就时使用 User.Identity.Name 属性</span><span class="sxs-lookup"><span data-stu-id="58f7b-172">Using the User.Identity.Name property when Editing Dinners</span></span>

<span data-ttu-id="58f7b-173">现在，让我们添加一些限制用户的授权逻辑，使用户只能编辑他们自己所托管的就的属性。</span><span class="sxs-lookup"><span data-stu-id="58f7b-173">Let's now add some authorization logic that restricts users so that they can only edit the properties of dinners they themselves are hosting.</span></span>

<span data-ttu-id="58f7b-174">为帮助实现此目标，我们首先将 "IsHostedBy （用户名）" 帮助器方法添加到晚餐对象（在前面构建的 Dinner.cs 分部类中）。</span><span class="sxs-lookup"><span data-stu-id="58f7b-174">To help with this, we'll first add an "IsHostedBy(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="58f7b-175">此帮助器方法返回 true 或 false，具体取决于所提供的用户名是否与晚餐 HostedBy 属性匹配，并封装对它们执行不区分大小写的字符串比较所需的逻辑：</span><span class="sxs-lookup"><span data-stu-id="58f7b-175">This helper method returns true or false depending on whether a supplied username matches the Dinner HostedBy property, and encapsulates the logic necessary to perform a case-insensitive string comparison of them:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

<span data-ttu-id="58f7b-176">然后，将 [授权] 特性添加到 DinnersController 类中的 Edit （）操作方法。</span><span class="sxs-lookup"><span data-stu-id="58f7b-176">We'll then add an [Authorize] attribute to the Edit() action methods within our DinnersController class.</span></span> <span data-ttu-id="58f7b-177">这将确保用户必须登录才能请求 */Dinners/Edit/[id]* URL。</span><span class="sxs-lookup"><span data-stu-id="58f7b-177">This will ensure that users must be logged in to request a */Dinners/Edit/[id]* URL.</span></span>

<span data-ttu-id="58f7b-178">然后，可以将代码添加到使用 IsHostedBy （用户名）帮助程序方法的编辑方法，以验证登录的用户是否与晚餐主机匹配。</span><span class="sxs-lookup"><span data-stu-id="58f7b-178">We can then add code to our Edit methods that uses the Dinner.IsHostedBy(username) helper method to verify that the logged-in user matches the Dinner host.</span></span> <span data-ttu-id="58f7b-179">如果用户不是主机，将显示 "InvalidOwner" 视图并终止请求。</span><span class="sxs-lookup"><span data-stu-id="58f7b-179">If the user is not the host, we'll display an "InvalidOwner" view and terminate the request.</span></span> <span data-ttu-id="58f7b-180">执行此操作的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="58f7b-180">The code to do this looks like below:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

<span data-ttu-id="58f7b-181">然后，可以右键单击 \Views\Dinners 目录，然后选择 "添加&gt;视图" 菜单命令以创建新的 "InvalidOwner" 视图。</span><span class="sxs-lookup"><span data-stu-id="58f7b-181">We can then right-click on the \Views\Dinners directory and choose the Add-&gt;View menu command to create a new "InvalidOwner" view.</span></span> <span data-ttu-id="58f7b-182">我们会在其中填充以下错误消息：</span><span class="sxs-lookup"><span data-stu-id="58f7b-182">We'll populate it with the below error message:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

<span data-ttu-id="58f7b-183">现在，当用户尝试编辑他们不拥有的晚餐时，他们将收到一条错误消息：</span><span class="sxs-lookup"><span data-stu-id="58f7b-183">And now when a user attempts to edit a dinner they don't own, they'll get an error message:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

<span data-ttu-id="58f7b-184">对于控制器中的 Delete （）操作方法，我们可以重复相同的步骤，以锁定删除就的权限，并确保只有晚餐的主机才能将其删除。</span><span class="sxs-lookup"><span data-stu-id="58f7b-184">We can repeat the same steps for the Delete() action methods within our controller to lock down permission to delete Dinners as well, and ensure that only the host of a Dinner can delete it.</span></span>

### <a name="showinghiding-edit-and-delete-links"></a><span data-ttu-id="58f7b-185">显示/隐藏编辑和删除链接</span><span class="sxs-lookup"><span data-stu-id="58f7b-185">Showing/Hiding Edit and Delete Links</span></span>

<span data-ttu-id="58f7b-186">我们将从详细信息 URL 链接到我们的 DinnersController 类的编辑和删除操作方法：</span><span class="sxs-lookup"><span data-stu-id="58f7b-186">We are linking to the Edit and Delete action method of our DinnersController class from our Details URL:</span></span>

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

<span data-ttu-id="58f7b-187">当前显示的是编辑和删除操作链接，而不考虑到详细信息 URL 的访问者是否是晚餐的主机。</span><span class="sxs-lookup"><span data-stu-id="58f7b-187">Currently we are showing the Edit and Delete action links regardless of whether the visitor to the details URL is the host of the dinner.</span></span> <span data-ttu-id="58f7b-188">让我们对此进行更改，以便仅在访问用户是晚餐的所有者时显示链接。</span><span class="sxs-lookup"><span data-stu-id="58f7b-188">Let's change this so that the links are only displayed if the visiting user is the owner of the dinner.</span></span>

<span data-ttu-id="58f7b-189">DinnersController 中的详细信息（）操作方法检索晚餐对象，然后将其作为模型对象传递到我们的视图模板：</span><span class="sxs-lookup"><span data-stu-id="58f7b-189">The Details() action method within our DinnersController retrieves a Dinner object and then passes it as the model object to our view template:</span></span>

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

<span data-ttu-id="58f7b-190">我们可以使用如下所示的 IsHostedBy （）帮助程序方法将视图模板更新为有条件地显示/隐藏 "编辑" 和 "删除" 链接：</span><span class="sxs-lookup"><span data-stu-id="58f7b-190">We can update our view template to conditionally show/hide the Edit and Delete links by using the Dinner.IsHostedBy() helper method like below:</span></span>

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a><span data-ttu-id="58f7b-191">后续步骤</span><span class="sxs-lookup"><span data-stu-id="58f7b-191">Next Steps</span></span>

<span data-ttu-id="58f7b-192">现在，让我们看看如何使用 AJAX 为经过身份验证的用户提供 RSVP for 就。</span><span class="sxs-lookup"><span data-stu-id="58f7b-192">Let's now look at how we can enable authenticated users to RSVP for dinners using AJAX.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="58f7b-193">[上一页](implement-efficient-data-paging.md)
> [下一页](use-ajax-to-deliver-dynamic-updates.md)</span><span class="sxs-lookup"><span data-stu-id="58f7b-193">[Previous](implement-efficient-data-paging.md)
[Next](use-ajax-to-deliver-dynamic-updates.md)</span></span>
