---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: 更改 ASP.NET Identity-ASP.NET 4.x 中用户的主密钥
author: Rick-Anderson
description: 在 Visual Studio 2013 中，默认的 web 应用程序使用用户帐户的键的字符串值。 ASP.NET Identity 使你能够更改 。
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472262"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a><span data-ttu-id="60932-104">在 ASP.NET Identity 中更改用户的主键</span><span class="sxs-lookup"><span data-stu-id="60932-104">Change Primary Key for Users in ASP.NET Identity</span></span>

<span data-ttu-id="60932-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="60932-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="60932-106">在 Visual Studio 2013 中，默认的 web 应用程序使用用户帐户的键的字符串值。</span><span class="sxs-lookup"><span data-stu-id="60932-106">In Visual Studio 2013, the default web application uses a string value for the key for user accounts.</span></span> <span data-ttu-id="60932-107">ASP.NET Identity 使你能够更改密钥的类型，以满足你的数据需求。</span><span class="sxs-lookup"><span data-stu-id="60932-107">ASP.NET Identity enables you to change the type of the key to meet your data requirements.</span></span> <span data-ttu-id="60932-108">例如，可以将键的类型从字符串更改为整数。</span><span class="sxs-lookup"><span data-stu-id="60932-108">For example, you can change the type of the key from a string to an integer.</span></span>
> 
> <span data-ttu-id="60932-109">本主题说明如何从默认的 web 应用程序开始，并将用户帐户密钥更改为整数。</span><span class="sxs-lookup"><span data-stu-id="60932-109">This topic shows how to start with the default web application and change the user account key to an integer.</span></span> <span data-ttu-id="60932-110">您可以使用相同的修改来实现项目中的任何类型的密钥。</span><span class="sxs-lookup"><span data-stu-id="60932-110">You can use the same modifications to implement any type of key in your project.</span></span> <span data-ttu-id="60932-111">它演示如何在默认 web 应用程序中进行这些更改，但您可以将类似的修改应用于自定义的应用程序。</span><span class="sxs-lookup"><span data-stu-id="60932-111">It shows how to make these changes in the default web application, but you could apply similar modifications to a customized application.</span></span> <span data-ttu-id="60932-112">其中显示了使用 MVC 或 Web 窗体时所需的更改。</span><span class="sxs-lookup"><span data-stu-id="60932-112">It shows the changes needed when working with MVC or Web Forms.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="60932-113">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="60932-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="60932-114">Visual Studio 2013 更新2（或更高版本）</span><span class="sxs-lookup"><span data-stu-id="60932-114">Visual Studio 2013 with Update 2 (or later)</span></span>
> - <span data-ttu-id="60932-115">ASP.NET Identity 2.1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="60932-115">ASP.NET Identity 2.1 or later</span></span>

<span data-ttu-id="60932-116">若要执行本教程中的步骤，必须具有 Visual Studio 2013 Update 2 （或更高版本）以及从 ASP.NET Web 应用程序模板创建的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="60932-116">To perform the steps in this tutorial, you must have Visual Studio 2013 Update 2 (or later), and a web application created from the ASP.NET Web Application template.</span></span> <span data-ttu-id="60932-117">在 Update 3 中更改的模板。</span><span class="sxs-lookup"><span data-stu-id="60932-117">The template changed in Update 3.</span></span> <span data-ttu-id="60932-118">本主题说明如何在 Update 2 和 Update 3 中更改模板。</span><span class="sxs-lookup"><span data-stu-id="60932-118">This topic shows how to change the template in Update 2 and Update 3.</span></span>

<span data-ttu-id="60932-119">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="60932-119">This topic contains the following sections:</span></span>

- [<span data-ttu-id="60932-120">更改标识用户类中的密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-120">Change the type of the key in the Identity user class</span></span>](#userclass)
- [<span data-ttu-id="60932-121">添加使用密钥类型的自定义标识类</span><span class="sxs-lookup"><span data-stu-id="60932-121">Add customized Identity classes that use the key type</span></span>](#customclass)
- [<span data-ttu-id="60932-122">更改上下文类和用户管理器以使用密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-122">Change the context class and user manager to use the key type</span></span>](#context)
- [<span data-ttu-id="60932-123">更改启动配置以使用密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-123">Change start-up configuration to use the key type</span></span>](#startup)
- [<span data-ttu-id="60932-124">对于包含 Update 2 的 MVC，请更改 AccountController 以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-124">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="60932-125">对于更新3的 MVC，请更改 AccountController 和 ManageController 以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-125">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="60932-126">对于更新2的 Web 窗体，更改帐户页以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-126">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="60932-127">对于更新3的 Web 窗体，更改帐户页以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-127">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)
- [<span data-ttu-id="60932-128">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="60932-128">Run application</span></span>](#run)
- [<span data-ttu-id="60932-129">其他资源</span><span class="sxs-lookup"><span data-stu-id="60932-129">Other resources</span></span>](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a><span data-ttu-id="60932-130">更改标识用户类中的密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-130">Change the type of the key in the Identity user class</span></span>

<span data-ttu-id="60932-131">在从 ASP.NET Web 应用程序模板创建的项目中，指定 ApplicationUser 类对用户帐户的密钥使用整数。</span><span class="sxs-lookup"><span data-stu-id="60932-131">In your project created from the ASP.NET Web Application template, specify that the ApplicationUser class uses an integer for the key for user accounts.</span></span> <span data-ttu-id="60932-132">在 IdentityModels.cs 中，更改 ApplicationUser 类，使其从类型为**int**的 IdentityUser 继承 TKey 泛型参数。</span><span class="sxs-lookup"><span data-stu-id="60932-132">In IdentityModels.cs, change the ApplicationUser class to inherit from IdentityUser that has a type of **int** for the TKey generic parameter.</span></span> <span data-ttu-id="60932-133">还将传递尚未实现的三个自定义类的名称。</span><span class="sxs-lookup"><span data-stu-id="60932-133">You also pass the names of three customized class which you have not implemented yet.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

<span data-ttu-id="60932-134">您已更改密钥的类型，但默认情况下，应用程序的其余部分仍假定该密钥是一个字符串。</span><span class="sxs-lookup"><span data-stu-id="60932-134">You have changed the type of the key, but, by default, the rest of the application still assumes the key is a string.</span></span> <span data-ttu-id="60932-135">必须在采用字符串的代码中显式指示密钥的类型。</span><span class="sxs-lookup"><span data-stu-id="60932-135">You must explicitly indicate the type of the key in code that assumes a string.</span></span>

<span data-ttu-id="60932-136">在**ApplicationUser**类中，将**GenerateUserIdentityAsync**方法更改为包含 int，如下面突出显示的代码所示。</span><span class="sxs-lookup"><span data-stu-id="60932-136">In the **ApplicationUser** class, change the **GenerateUserIdentityAsync** method to include int, as shown in the highlighted code below.</span></span> <span data-ttu-id="60932-137">对于具有 Update 3 模板的 Web 窗体项目，此更改不是必需的。</span><span class="sxs-lookup"><span data-stu-id="60932-137">This change is not necessary for Web Forms projects with the Update 3 template.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a><span data-ttu-id="60932-138">添加使用密钥类型的自定义标识类</span><span class="sxs-lookup"><span data-stu-id="60932-138">Add customized Identity classes that use the key type</span></span>

<span data-ttu-id="60932-139">其他标识类，如 IdentityUserRole、IdentityUserClaim、IdentityUserLogin、IdentityRole、UserStore、RoleStore 仍设置为使用字符串键。</span><span class="sxs-lookup"><span data-stu-id="60932-139">The other Identity classes, such as IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, are still set up to use a string key.</span></span> <span data-ttu-id="60932-140">创建这些类的新版本，这些类指定键的整数。</span><span class="sxs-lookup"><span data-stu-id="60932-140">Create new versions of these classes that specify an integer for the key.</span></span> <span data-ttu-id="60932-141">不需要在这些类中提供很多实现代码，你主要是将 int 设置为键。</span><span class="sxs-lookup"><span data-stu-id="60932-141">You do not need to provide much implementation code in these classes, you are primarily just setting int as the key.</span></span>

<span data-ttu-id="60932-142">将以下类添加到 IdentityModels.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="60932-142">Add the following classes to your IdentityModels.cs file.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a><span data-ttu-id="60932-143">更改上下文类和用户管理器以使用密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-143">Change the context class and user manager to use the key type</span></span>

<span data-ttu-id="60932-144">在 IdentityModels.cs 中，更改**ApplicationDbContext**类的定义，以使用新的自定义类和密钥的**int** ，如突出显示的代码中所示。</span><span class="sxs-lookup"><span data-stu-id="60932-144">In IdentityModels.cs, change the definition of the **ApplicationDbContext** class to use your new customized classes and an **int** for the key, as shown in the highlighted code.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

<span data-ttu-id="60932-145">ThrowIfV1Schema 参数在构造函数中不再有效。</span><span class="sxs-lookup"><span data-stu-id="60932-145">The ThrowIfV1Schema parameter is no longer valid in the constructor.</span></span> <span data-ttu-id="60932-146">更改构造函数，使其不传递 ThrowIfV1Schema 值。</span><span class="sxs-lookup"><span data-stu-id="60932-146">Change the constructor so it does not pass a ThrowIfV1Schema value.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

<span data-ttu-id="60932-147">打开 IdentityConfig.cs，并将**ApplicationUserManger**类更改为使用新用户存储类来保存数据，并使用**int**作为密钥。</span><span class="sxs-lookup"><span data-stu-id="60932-147">Open IdentityConfig.cs, and change the **ApplicationUserManger** class to use your new user store class for persisting data and an **int** for the key.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

<span data-ttu-id="60932-148">在 Update 3 模板中，必须更改 ApplicationSignInManager 类。</span><span class="sxs-lookup"><span data-stu-id="60932-148">In the Update 3 template, you must change the ApplicationSignInManager class.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a><span data-ttu-id="60932-149">更改启动配置以使用密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-149">Change start-up configuration to use the key type</span></span>

<span data-ttu-id="60932-150">在 Startup.Auth.cs 中，替换 OnValidateIdentity 代码，如下所示。</span><span class="sxs-lookup"><span data-stu-id="60932-150">In Startup.Auth.cs, replace the OnValidateIdentity code, as highlighted below.</span></span> <span data-ttu-id="60932-151">请注意，getUserIdCallback 定义会将字符串值分析为一个整数。</span><span class="sxs-lookup"><span data-stu-id="60932-151">Notice that the getUserIdCallback definition, parses the string value into an integer.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

<span data-ttu-id="60932-152">如果你的项目不能识别**GetUserId**方法的泛型实现，你可能需要将 ASP.NET Identity NuGet 包更新到版本2。1</span><span class="sxs-lookup"><span data-stu-id="60932-152">If your project does not recognize the generic implementation of the **GetUserId** method, you may need to update the ASP.NET Identity NuGet package to version 2.1</span></span>

<span data-ttu-id="60932-153">你已对 ASP.NET Identity 使用的基础结构类进行了大量更改。</span><span class="sxs-lookup"><span data-stu-id="60932-153">You have made a lot of changes to the infrastructure classes used by ASP.NET Identity.</span></span> <span data-ttu-id="60932-154">如果尝试编译项目，会注意到很多错误。</span><span class="sxs-lookup"><span data-stu-id="60932-154">If you try compiling the project, you will notice a lot of errors.</span></span> <span data-ttu-id="60932-155">幸运的是，剩下的错误都是类似的。</span><span class="sxs-lookup"><span data-stu-id="60932-155">Fortunately, the remaining errors are all similar.</span></span> <span data-ttu-id="60932-156">标识类需要键的整数，但控制器（或 Web 窗体）传递的是一个字符串值。</span><span class="sxs-lookup"><span data-stu-id="60932-156">The Identity class expects an integer for the key, but the controller (or Web Form) is passing a string value.</span></span> <span data-ttu-id="60932-157">在每种情况下，都需要通过调用**GetUserId&lt;int&gt;** ，将字符串转换为和整数。</span><span class="sxs-lookup"><span data-stu-id="60932-157">In each case, you need to convert from a string to and integer by calling **GetUserId&lt;int&gt;**.</span></span> <span data-ttu-id="60932-158">可以通过编译来处理 "错误列表"，也可以执行以下更改。</span><span class="sxs-lookup"><span data-stu-id="60932-158">You can either work through the error list from compilation or follow the changes below.</span></span>

<span data-ttu-id="60932-159">剩余的更改取决于要创建的项目的类型，以及在 Visual Studio 中安装的更新。</span><span class="sxs-lookup"><span data-stu-id="60932-159">The remaining changes depend on the type of project you are creating and which update you have installed in Visual Studio.</span></span> <span data-ttu-id="60932-160">可以通过以下链接直接进入相关部分</span><span class="sxs-lookup"><span data-stu-id="60932-160">You can go directly to the relevant section through the following links</span></span>

- [<span data-ttu-id="60932-161">对于包含 Update 2 的 MVC，请更改 AccountController 以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-161">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="60932-162">对于更新3的 MVC，请更改 AccountController 和 ManageController 以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-162">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="60932-163">对于更新2的 Web 窗体，更改帐户页以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-163">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="60932-164">对于更新3的 Web 窗体，更改帐户页以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-164">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a><span data-ttu-id="60932-165">对于包含 Update 2 的 MVC，请更改 AccountController 以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-165">For MVC with Update 2, change the AccountController to pass the key type</span></span>

<span data-ttu-id="60932-166">打开 AccountController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="60932-166">Open the AccountController.cs file.</span></span> <span data-ttu-id="60932-167">需要更改以下方法。</span><span class="sxs-lookup"><span data-stu-id="60932-167">You need to change the following methods.</span></span>

<span data-ttu-id="60932-168">**ConfirmEmail**方法</span><span class="sxs-lookup"><span data-stu-id="60932-168">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

<span data-ttu-id="60932-169">**解除关联**方法</span><span class="sxs-lookup"><span data-stu-id="60932-169">**Disassociate** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

<span data-ttu-id="60932-170">**管理（ManageUserViewModel）** 方法</span><span class="sxs-lookup"><span data-stu-id="60932-170">**Manage(ManageUserViewModel)** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

<span data-ttu-id="60932-171">**LinkLoginCallback**方法</span><span class="sxs-lookup"><span data-stu-id="60932-171">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

<span data-ttu-id="60932-172">**RemoveAccountList**方法</span><span class="sxs-lookup"><span data-stu-id="60932-172">**RemoveAccountList** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

<span data-ttu-id="60932-173">**HasPassword**方法</span><span class="sxs-lookup"><span data-stu-id="60932-173">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

<span data-ttu-id="60932-174">现在可以[运行应用程序](#run)并注册新用户。</span><span class="sxs-lookup"><span data-stu-id="60932-174">You can now [run the application](#run) and register a new user.</span></span>

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a><span data-ttu-id="60932-175">对于更新3的 MVC，请更改 AccountController 和 ManageController 以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-175">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>

<span data-ttu-id="60932-176">打开 AccountController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="60932-176">Open the AccountController.cs file.</span></span> <span data-ttu-id="60932-177">需要更改以下方法。</span><span class="sxs-lookup"><span data-stu-id="60932-177">You need to change the following method.</span></span>

<span data-ttu-id="60932-178">**ConfirmEmail**方法</span><span class="sxs-lookup"><span data-stu-id="60932-178">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

<span data-ttu-id="60932-179">**SendCode**方法</span><span class="sxs-lookup"><span data-stu-id="60932-179">**SendCode** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

<span data-ttu-id="60932-180">打开 ManageController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="60932-180">Open the ManageController.cs file.</span></span> <span data-ttu-id="60932-181">需要更改以下方法。</span><span class="sxs-lookup"><span data-stu-id="60932-181">You need to change the following methods.</span></span>

<span data-ttu-id="60932-182">**Index**方法</span><span class="sxs-lookup"><span data-stu-id="60932-182">**Index** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

<span data-ttu-id="60932-183">**RemoveLogin**方法</span><span class="sxs-lookup"><span data-stu-id="60932-183">**RemoveLogin** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

<span data-ttu-id="60932-184">**AddPhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="60932-184">**AddPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

<span data-ttu-id="60932-185">**EnableTwoFactorAuthentication**方法</span><span class="sxs-lookup"><span data-stu-id="60932-185">**EnableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

<span data-ttu-id="60932-186">**DisableTwoFactorAuthentication**方法</span><span class="sxs-lookup"><span data-stu-id="60932-186">**DisableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

<span data-ttu-id="60932-187">**VerifyPhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="60932-187">**VerifyPhoneNumber** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

<span data-ttu-id="60932-188">**RemovePhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="60932-188">**RemovePhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

<span data-ttu-id="60932-189">**ChangePassword**方法</span><span class="sxs-lookup"><span data-stu-id="60932-189">**ChangePassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

<span data-ttu-id="60932-190">**SetPassword**方法</span><span class="sxs-lookup"><span data-stu-id="60932-190">**SetPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

<span data-ttu-id="60932-191">**ManageLogins**方法</span><span class="sxs-lookup"><span data-stu-id="60932-191">**ManageLogins** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

<span data-ttu-id="60932-192">**LinkLoginCallback**方法</span><span class="sxs-lookup"><span data-stu-id="60932-192">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

<span data-ttu-id="60932-193">**HasPassword**方法</span><span class="sxs-lookup"><span data-stu-id="60932-193">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

<span data-ttu-id="60932-194">**HasPhoneNumber**方法</span><span class="sxs-lookup"><span data-stu-id="60932-194">**HasPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

<span data-ttu-id="60932-195">现在可以[运行应用程序](#run)并注册新用户。</span><span class="sxs-lookup"><span data-stu-id="60932-195">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="60932-196">对于更新2的 Web 窗体，更改帐户页以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-196">For Web Forms with Update 2, change Account pages to pass the key type</span></span>

<span data-ttu-id="60932-197">对于更新2的 Web 窗体，需要更改以下页面。</span><span class="sxs-lookup"><span data-stu-id="60932-197">For Web Forms with Update 2, you need to change the following pages.</span></span>

<span data-ttu-id="60932-198">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="60932-198">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

<span data-ttu-id="60932-199">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="60932-199">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

<span data-ttu-id="60932-200">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="60932-200">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

<span data-ttu-id="60932-201">现在可以[运行应用程序](#run)并注册新用户。</span><span class="sxs-lookup"><span data-stu-id="60932-201">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="60932-202">对于更新3的 Web 窗体，更改帐户页以传递密钥类型</span><span class="sxs-lookup"><span data-stu-id="60932-202">For Web Forms with Update 3, change Account pages to pass the key type</span></span>

<span data-ttu-id="60932-203">对于更新3的 Web 窗体，需要更改以下页面。</span><span class="sxs-lookup"><span data-stu-id="60932-203">For Web Forms with Update 3, you need to change the following pages.</span></span>

<span data-ttu-id="60932-204">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="60932-204">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

<span data-ttu-id="60932-205">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="60932-205">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

<span data-ttu-id="60932-206">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="60932-206">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

<span data-ttu-id="60932-207">**VerifyPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="60932-207">**VerifyPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

<span data-ttu-id="60932-208">**AddPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="60932-208">**AddPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

<span data-ttu-id="60932-209">**ManagePassword.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="60932-209">**ManagePassword.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

<span data-ttu-id="60932-210">**ManageLogins.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="60932-210">**ManageLogins.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

<span data-ttu-id="60932-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="60932-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a><span data-ttu-id="60932-212">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="60932-212">Run application</span></span>

<span data-ttu-id="60932-213">已完成对默认 Web 应用程序模板所需的所有更改。</span><span class="sxs-lookup"><span data-stu-id="60932-213">You have finished all of the required changes to the default Web Application template.</span></span> <span data-ttu-id="60932-214">运行应用程序并注册新用户。</span><span class="sxs-lookup"><span data-stu-id="60932-214">Run the application and register a new user.</span></span> <span data-ttu-id="60932-215">注册用户后，您会注意到，AspNetUsers 表的 Id 列是整数。</span><span class="sxs-lookup"><span data-stu-id="60932-215">After registering the user, you will notice that the AspNetUsers table has an Id column that is an integer.</span></span>

![新主键](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

<span data-ttu-id="60932-217">如果以前使用不同的主键创建了 ASP.NET Identity 表，则需要进行一些额外的更改。</span><span class="sxs-lookup"><span data-stu-id="60932-217">If you have previously created the ASP.NET Identity tables with a different primary key, you need to make some additional changes.</span></span> <span data-ttu-id="60932-218">如果可能，只需删除现有的数据库。</span><span class="sxs-lookup"><span data-stu-id="60932-218">If possible, just delete the existing database.</span></span> <span data-ttu-id="60932-219">在运行 web 应用程序并添加新用户时，将使用正确的设计重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="60932-219">The database will be re-created with the correct design when you run the web application and add a new user.</span></span> <span data-ttu-id="60932-220">如果无法删除，请运行 code first 迁移来更改表。</span><span class="sxs-lookup"><span data-stu-id="60932-220">If deletion is not possible, run code first migrations to change the tables.</span></span> <span data-ttu-id="60932-221">但是，新的整数主键将不会设置为数据库中的 "SQL 标识" 属性。</span><span class="sxs-lookup"><span data-stu-id="60932-221">However, the new integer primary key will not be set up as a SQL IDENTITY property in the database.</span></span> <span data-ttu-id="60932-222">您必须手动将 "Id" 列设置为标识。</span><span class="sxs-lookup"><span data-stu-id="60932-222">You must manually set the Id column as an IDENTITY.</span></span>

<a id="other"></a>
## <a name="other-resources"></a><span data-ttu-id="60932-223">其他资源</span><span class="sxs-lookup"><span data-stu-id="60932-223">Other resources</span></span>

- [<span data-ttu-id="60932-224">ASP.NET 标识的自定义存储提供程序概述</span><span class="sxs-lookup"><span data-stu-id="60932-224">Overview of Custom Storage Providers for ASP.NET Identity</span></span>](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [<span data-ttu-id="60932-225">将现有网站从 SQL 成员身份迁移到 ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="60932-225">Migrating an Existing Website from SQL Membership to ASP.NET Identity</span></span>](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [<span data-ttu-id="60932-226">将成员身份和用户配置文件的通用提供程序数据迁移到 ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="60932-226">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity</span></span>](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- <span data-ttu-id="60932-227">带有更改的主键的[示例应用程序](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)</span><span class="sxs-lookup"><span data-stu-id="60932-227">[Sample application](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) with changed primary key</span></span>
