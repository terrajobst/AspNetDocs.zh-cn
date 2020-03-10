---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 第7部分：成员身份和授权 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第7部分涵盖成员身份和授权。
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433466"
---
# <a name="part-7-membership-and-authorization"></a><span data-ttu-id="fa829-104">第7部分：成员身份和授权</span><span class="sxs-lookup"><span data-stu-id="fa829-104">Part 7: Membership and Authorization</span></span>

<span data-ttu-id="fa829-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="fa829-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="fa829-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="fa829-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="fa829-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="fa829-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="fa829-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="fa829-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="fa829-109">第7部分涵盖成员身份和授权。</span><span class="sxs-lookup"><span data-stu-id="fa829-109">Part 7 covers Membership and Authorization.</span></span>

<span data-ttu-id="fa829-110">我们的商店经理控制器目前可供访问我们的站点的任何人访问。</span><span class="sxs-lookup"><span data-stu-id="fa829-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="fa829-111">让我们对此进行更改，将权限限制为站点管理员。</span><span class="sxs-lookup"><span data-stu-id="fa829-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="fa829-112">添加 AccountController 和视图</span><span class="sxs-lookup"><span data-stu-id="fa829-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="fa829-113">完整的 ASP.NET MVC 3 Web 应用程序模板和 ASP.NET MVC 3 空 Web 应用程序模板之间的一个差异是，空模板不包含帐户控制器。</span><span class="sxs-lookup"><span data-stu-id="fa829-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="fa829-114">我们将通过从完整 ASP.NET MVC 3 Web 应用程序模板创建的新 ASP.NET MVC 应用程序复制一些文件来添加帐户控制器。</span><span class="sxs-lookup"><span data-stu-id="fa829-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="fa829-115">使用 full ASP.NET MVC 3 Web 应用程序模板创建新的 ASP.NET MVC 应用程序，并将以下文件复制到项目中的相同目录中：</span><span class="sxs-lookup"><span data-stu-id="fa829-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="fa829-116">复制控制器目录中的 AccountController.cs</span><span class="sxs-lookup"><span data-stu-id="fa829-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="fa829-117">在模型目录中复制 AccountModels</span><span class="sxs-lookup"><span data-stu-id="fa829-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="fa829-118">在 Views 目录内创建帐户目录，并将所有四个视图复制到</span><span class="sxs-lookup"><span data-stu-id="fa829-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="fa829-119">更改控制器和模型类的命名空间，以使它们以 MvcMusicStore 开头。</span><span class="sxs-lookup"><span data-stu-id="fa829-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="fa829-120">AccountController 类应使用 MvcMusicStore 命名空间，而 AccountModels 类应使用 MvcMusicStore 命名空间。</span><span class="sxs-lookup"><span data-stu-id="fa829-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="fa829-121">*注意：这些文件也会在 MvcMusicStore-Assets 下载中提供，我们将在本教程的开头复制我们的站点设计文件。成员资格文件位于代码目录中。*</span><span class="sxs-lookup"><span data-stu-id="fa829-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="fa829-122">更新后的解决方案应如下所示：</span><span class="sxs-lookup"><span data-stu-id="fa829-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="fa829-123">添加具有 ASP.NET 配置站点的管理用户</span><span class="sxs-lookup"><span data-stu-id="fa829-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="fa829-124">在我们的网站中需要授权之前，我们需要创建一个具有访问权限的用户。</span><span class="sxs-lookup"><span data-stu-id="fa829-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="fa829-125">若要创建用户，最简单的方法是使用内置的 ASP.NET 配置网站。</span><span class="sxs-lookup"><span data-stu-id="fa829-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="fa829-126">单击解决方案资源管理器中的图标，启动 ASP.NET 配置网站。</span><span class="sxs-lookup"><span data-stu-id="fa829-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="fa829-127">这会启动配置网站。</span><span class="sxs-lookup"><span data-stu-id="fa829-127">This launches a configuration website.</span></span> <span data-ttu-id="fa829-128">单击主屏幕上的 "安全" 选项卡，然后单击屏幕中心的 "启用角色" 链接。</span><span class="sxs-lookup"><span data-stu-id="fa829-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="fa829-129">单击 "创建或管理角色" 链接。</span><span class="sxs-lookup"><span data-stu-id="fa829-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="fa829-130">输入 "管理员" 作为角色名称，然后按 "添加角色" 按钮。</span><span class="sxs-lookup"><span data-stu-id="fa829-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="fa829-131">单击 "返回" 按钮，然后单击左侧的 "创建用户" 链接。</span><span class="sxs-lookup"><span data-stu-id="fa829-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="fa829-132">使用以下信息填写左侧的 "用户信息" 字段：</span><span class="sxs-lookup"><span data-stu-id="fa829-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="fa829-133">**字段**</span><span class="sxs-lookup"><span data-stu-id="fa829-133">**Field**</span></span> | <span data-ttu-id="fa829-134">**值**</span><span class="sxs-lookup"><span data-stu-id="fa829-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="fa829-135">**用户名**</span><span class="sxs-lookup"><span data-stu-id="fa829-135">**User Name**</span></span> | <span data-ttu-id="fa829-136">管理员</span><span class="sxs-lookup"><span data-stu-id="fa829-136">Administrator</span></span> |
| <span data-ttu-id="fa829-137">**密码**</span><span class="sxs-lookup"><span data-stu-id="fa829-137">**Password**</span></span> | <span data-ttu-id="fa829-138">password123!</span><span class="sxs-lookup"><span data-stu-id="fa829-138">password123!</span></span> |
| <span data-ttu-id="fa829-139">**确认密码**</span><span class="sxs-lookup"><span data-stu-id="fa829-139">**Confirm Password**</span></span> | <span data-ttu-id="fa829-140">password123!</span><span class="sxs-lookup"><span data-stu-id="fa829-140">password123!</span></span> |
| <span data-ttu-id="fa829-141">**电子邮件**</span><span class="sxs-lookup"><span data-stu-id="fa829-141">**E-mail**</span></span> | <span data-ttu-id="fa829-142">（任何电子邮件地址都有效）</span><span class="sxs-lookup"><span data-stu-id="fa829-142">(any email address will work)</span></span> |
| <span data-ttu-id="fa829-143">**安全提示问题**</span><span class="sxs-lookup"><span data-stu-id="fa829-143">**Security Question**</span></span> | <span data-ttu-id="fa829-144">（任何所需内容）</span><span class="sxs-lookup"><span data-stu-id="fa829-144">(whatever you like)</span></span> |
| <span data-ttu-id="fa829-145">**安全提示问题的答案**</span><span class="sxs-lookup"><span data-stu-id="fa829-145">**Security Answer**</span></span> | <span data-ttu-id="fa829-146">（任何所需内容）</span><span class="sxs-lookup"><span data-stu-id="fa829-146">(whatever you like)</span></span> |

<span data-ttu-id="fa829-147">*注意：当然，你可以使用任何所需的密码。默认密码安全设置要求密码长度为7个字符，并且包含一个非字母数字字符。*</span><span class="sxs-lookup"><span data-stu-id="fa829-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="fa829-148">为此用户选择管理员角色，然后单击 "创建用户" 按钮。</span><span class="sxs-lookup"><span data-stu-id="fa829-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="fa829-149">此时，应会看到一条消息，指示已成功创建用户。</span><span class="sxs-lookup"><span data-stu-id="fa829-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="fa829-150">你现在可以关闭浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="fa829-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="fa829-151">基于角色的授权</span><span class="sxs-lookup"><span data-stu-id="fa829-151">Role-based Authorization</span></span>

<span data-ttu-id="fa829-152">现在，我们可以使用 [授权] 特性限制对 StoreManagerController 的访问，同时指定用户必须是管理员角色才能访问类中的任何控制器操作。</span><span class="sxs-lookup"><span data-stu-id="fa829-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="fa829-153">*注意：可以将 [授权] 特性置于特定操作方法和控制器类级别。*</span><span class="sxs-lookup"><span data-stu-id="fa829-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="fa829-154">现在，浏览到/StoreManager 会打开一个登录对话框：</span><span class="sxs-lookup"><span data-stu-id="fa829-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="fa829-155">在用新的管理员帐户登录后，我们就可以像以前一样来进入唱集编辑屏幕。</span><span class="sxs-lookup"><span data-stu-id="fa829-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="fa829-156">[上一页](mvc-music-store-part-6.md)
> [下一页](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="fa829-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>
