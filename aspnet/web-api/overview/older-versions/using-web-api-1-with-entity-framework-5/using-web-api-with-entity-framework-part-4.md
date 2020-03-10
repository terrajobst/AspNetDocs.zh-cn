---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: 第4部分：添加管理视图 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447878"
---
# <a name="part-4-adding-an-admin-view"></a><span data-ttu-id="79603-102">第4部分：添加管理员视图</span><span class="sxs-lookup"><span data-stu-id="79603-102">Part 4: Adding an Admin View</span></span>

<span data-ttu-id="79603-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="79603-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="79603-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="79603-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a><span data-ttu-id="79603-105">添加管理员视图</span><span class="sxs-lookup"><span data-stu-id="79603-105">Add an Admin View</span></span>

<span data-ttu-id="79603-106">现在，我们将转到客户端，并添加可使用管理控制器中的数据的页面。</span><span class="sxs-lookup"><span data-stu-id="79603-106">Now we'll turn to the client side, and add a page that can consume data from the Admin controller.</span></span> <span data-ttu-id="79603-107">此页允许用户通过将 AJAX 请求发送到控制器来创建、编辑或删除产品。</span><span class="sxs-lookup"><span data-stu-id="79603-107">The page will allow users to create, edit, or delete products, by sending AJAX requests to the controller.</span></span>

<span data-ttu-id="79603-108">在解决方案资源管理器中，展开 "控制器" 文件夹，然后打开名为 "HomeController.cs" 的文件。</span><span class="sxs-lookup"><span data-stu-id="79603-108">In Solution Explorer, expand the Controllers folder and open the file named HomeController.cs.</span></span> <span data-ttu-id="79603-109">此文件包含 MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="79603-109">This file contains an MVC controller.</span></span> <span data-ttu-id="79603-110">添加一个名为 `Admin`的方法：</span><span class="sxs-lookup"><span data-stu-id="79603-110">Add a method named `Admin`:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

<span data-ttu-id="79603-111">**HttpRouteUrl**方法创建 web API 的 URI，并将其存储在查看包中供以后查看。</span><span class="sxs-lookup"><span data-stu-id="79603-111">The **HttpRouteUrl** method creates the URI to the web API, and we store this in the view bag for later.</span></span>

<span data-ttu-id="79603-112">接下来，将文本光标置于 `Admin` 操作方法中，然后右键单击并选择 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="79603-112">Next, position the text cursor within the `Admin` action method, then right-click and select **Add View**.</span></span> <span data-ttu-id="79603-113">此时将显示 "**添加视图**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="79603-113">This will bring up the **Add View** dialog.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

<span data-ttu-id="79603-114">在 "**添加视图**" 对话框中，将视图命名为 "Admin"。</span><span class="sxs-lookup"><span data-stu-id="79603-114">In the **Add View** dialog, name the view "Admin".</span></span> <span data-ttu-id="79603-115">选中标签为 "**创建强类型视图**" 的复选框。</span><span class="sxs-lookup"><span data-stu-id="79603-115">Select the check box labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="79603-116">在 "**模型类**" 下，选择 "Product （ProductStore）"。</span><span class="sxs-lookup"><span data-stu-id="79603-116">Under **Model Class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="79603-117">将所有其他选项保留为其默认值。</span><span class="sxs-lookup"><span data-stu-id="79603-117">Leave all the other options as their default values.</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

<span data-ttu-id="79603-118">单击 "**添加**" 将在 "视图"/"主页"</span><span class="sxs-lookup"><span data-stu-id="79603-118">Clicking **Add** adds a file named Admin.cshtml under Views/Home.</span></span> <span data-ttu-id="79603-119">打开此文件并添加以下 HTML。</span><span class="sxs-lookup"><span data-stu-id="79603-119">Open this file and add the following HTML.</span></span> <span data-ttu-id="79603-120">此 HTML 定义了页面的结构，但尚未连接任何功能。</span><span class="sxs-lookup"><span data-stu-id="79603-120">This HTML defines the structure of the page, but no functionality is wired up yet.</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a><span data-ttu-id="79603-121">创建指向管理页面的链接</span><span class="sxs-lookup"><span data-stu-id="79603-121">Create a Link to the Admin Page</span></span>

<span data-ttu-id="79603-122">在解决方案资源管理器中，展开 "Views" 文件夹，然后展开 "共享" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="79603-122">In Solution Explorer, expand the Views folder and then expand the Shared folder.</span></span> <span data-ttu-id="79603-123">打开名为 \_Layout 的文件。</span><span class="sxs-lookup"><span data-stu-id="79603-123">Open the file named \_Layout.cshtml.</span></span> <span data-ttu-id="79603-124">找到 id 为 "menu" 的**ul**元素，并找到 "管理" 视图的操作链接：</span><span class="sxs-lookup"><span data-stu-id="79603-124">Locate the **ul** element with id = "menu", and an action link for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> <span data-ttu-id="79603-125">在示例项目中，我进行了一些其他修饰更改，如替换字符串 "您的徽标"。</span><span class="sxs-lookup"><span data-stu-id="79603-125">In the sample project, I made a few other cosmetic changes, such as replacing the string "Your logo here".</span></span> <span data-ttu-id="79603-126">这不会影响应用程序的功能。</span><span class="sxs-lookup"><span data-stu-id="79603-126">These don't affect the functionality of the application.</span></span> <span data-ttu-id="79603-127">您可以下载项目并比较文件。</span><span class="sxs-lookup"><span data-stu-id="79603-127">You can download the project and compare the files.</span></span>

<span data-ttu-id="79603-128">运行应用程序，并单击 "管理" 链接，该链接显示在主页的顶部。</span><span class="sxs-lookup"><span data-stu-id="79603-128">Run the application and click the "Admin" link that appears at the top of the home page.</span></span> <span data-ttu-id="79603-129">"管理员" 页应该如下所示：</span><span class="sxs-lookup"><span data-stu-id="79603-129">The Admin page should look like the following:</span></span>

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

<span data-ttu-id="79603-130">现在，页面不会执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="79603-130">Right now, the page doesn't do anything.</span></span> <span data-ttu-id="79603-131">在下一部分中，我们将使用挖空创建动态 UI。</span><span class="sxs-lookup"><span data-stu-id="79603-131">In the next section, we'll use Knockout.js to create a dynamic UI.</span></span>

## <a name="add-authorization"></a><span data-ttu-id="79603-132">添加授权</span><span class="sxs-lookup"><span data-stu-id="79603-132">Add Authorization</span></span>

<span data-ttu-id="79603-133">访问站点的任何人当前都可以访问 "管理" 页。</span><span class="sxs-lookup"><span data-stu-id="79603-133">The Admin page is currently accessible to anyone visiting the site.</span></span> <span data-ttu-id="79603-134">让我们将其更改为限制管理员权限。</span><span class="sxs-lookup"><span data-stu-id="79603-134">Let's change this to restrict permission to administrators.</span></span>

<span data-ttu-id="79603-135">首先添加 "管理员" 角色和管理员用户。</span><span class="sxs-lookup"><span data-stu-id="79603-135">Start by adding an "Administrator" role and an administrator user.</span></span> <span data-ttu-id="79603-136">在解决方案资源管理器中，展开 "筛选器" 文件夹，然后打开名为 "InitializeSimpleMembershipAttribute.cs" 的文件。</span><span class="sxs-lookup"><span data-stu-id="79603-136">In Solution Explorer, expand the Filters folder and open the file named InitializeSimpleMembershipAttribute.cs.</span></span> <span data-ttu-id="79603-137">找到 `SimpleMembershipInitializer` 构造函数。</span><span class="sxs-lookup"><span data-stu-id="79603-137">Locate the `SimpleMembershipInitializer` constructor.</span></span> <span data-ttu-id="79603-138">调用**WebSecurity InitializeDatabaseConnection**后，添加以下代码：</span><span class="sxs-lookup"><span data-stu-id="79603-138">After the call to **WebSecurity.InitializeDatabaseConnection**, add the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

<span data-ttu-id="79603-139">这是添加 "管理员" 角色并为角色创建用户的一种快速而完善的方式。</span><span class="sxs-lookup"><span data-stu-id="79603-139">This is a quick-and-dirty way to add the "Administrator" role and create a user for the role.</span></span>

<span data-ttu-id="79603-140">在解决方案资源管理器中，展开 "控制器" 文件夹并打开 HomeController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="79603-140">In Solution Explorer, expand the Controllers folder and open the HomeController.cs file.</span></span> <span data-ttu-id="79603-141">将**授权**特性添加到 `Admin` 方法。</span><span class="sxs-lookup"><span data-stu-id="79603-141">Add the **Authorize** attribute to the `Admin` method.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

<span data-ttu-id="79603-142">打开 AdminController.cs 文件，并将**授权**属性添加到整个 `AdminController` 类中。</span><span class="sxs-lookup"><span data-stu-id="79603-142">Open the AdminController.cs file and add the **Authorize** attribute to the entire `AdminController` class.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="79603-143">MVC 和 Web API 在不同的命名空间中定义**授权**属性。</span><span class="sxs-lookup"><span data-stu-id="79603-143">MVC and Web API both define **Authorize** attributes, in different namespaces.</span></span> <span data-ttu-id="79603-144">MVC 使用**AuthorizeAttribute**，而 Web API 使用**AuthorizeAttribute**的情况下。</span><span class="sxs-lookup"><span data-stu-id="79603-144">MVC uses **System.Web.Mvc.AuthorizeAttribute**, while Web API uses **System.Web.Http.AuthorizeAttribute**.</span></span>

<span data-ttu-id="79603-145">现在，只有管理员才能查看 "管理" 页。</span><span class="sxs-lookup"><span data-stu-id="79603-145">Now only administrators can view the Admin page.</span></span> <span data-ttu-id="79603-146">此外，如果向管理控制器发送 HTTP 请求，则该请求必须包含身份验证 cookie。</span><span class="sxs-lookup"><span data-stu-id="79603-146">Also, if you send an HTTP request to the Admin controller, the request must contain an authentication cookie.</span></span> <span data-ttu-id="79603-147">如果没有，则服务器将发送 HTTP 401 （未授权）响应。</span><span class="sxs-lookup"><span data-stu-id="79603-147">If not, the server sends an HTTP 401 (Unauthorized) response.</span></span> <span data-ttu-id="79603-148">可以通过将 GET 请求发送到 `http://localhost:*port*/api/admin`在 Fiddler 中查看此项。</span><span class="sxs-lookup"><span data-stu-id="79603-148">You can see this in Fiddler by sending a GET request to `http://localhost:*port*/api/admin`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="79603-149">[上一页](using-web-api-with-entity-framework-part-3.md)
> [下一页](using-web-api-with-entity-framework-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="79603-149">[Previous](using-web-api-with-entity-framework-part-3.md)
[Next](using-web-api-with-entity-framework-part-5.md)</span></span>
