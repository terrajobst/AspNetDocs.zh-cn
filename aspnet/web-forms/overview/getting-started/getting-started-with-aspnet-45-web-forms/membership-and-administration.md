---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: 成员资格和管理 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: ab00bc90bfc767d06e747be6dfb973245b5aae88
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439928"
---
# <a name="membership-and-administration"></a><span data-ttu-id="8f2c0-103">成员身份和管理</span><span class="sxs-lookup"><span data-stu-id="8f2c0-103">Membership and Administration</span></span>

<span data-ttu-id="8f2c0-104">作者： [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="8f2c0-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="8f2c0-105">[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="8f2c0-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="8f2c0-106">本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="8f2c0-107">此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="8f2c0-108">本教程演示如何更新 Wingtip 玩具示例应用程序，以添加自定义角色并使用 ASP.NET Identity。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-108">This tutorial shows you how to update the Wingtip Toys sample application to add a custom role and use ASP.NET Identity.</span></span> <span data-ttu-id="8f2c0-109">还介绍了如何实现一个管理页面，通过该页面，具有自定义角色的用户可以在网站中添加和删除产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-109">It also shows you how to implement an administration page from which the user with a custom role can add and remove products from the website.</span></span>

<span data-ttu-id="8f2c0-110">[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)是用于构建 ASP.NET web 应用程序的成员资格系统，在 ASP.NET 4.5 中提供。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-110">[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md) is the membership system used to build ASP.NET web application and is available in ASP.NET 4.5.</span></span> <span data-ttu-id="8f2c0-111">ASP.NET Identity 用于 Visual Studio 2013 Web 窗体项目模板，以及用于[ASP.NET MVC](../../../../mvc/index.md)、 [ASP.NET Web API](../../../../web-api/index.md)和[ASP.NET 单页面应用程序](../../../../single-page-application/index.md)的模板。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-111">ASP.NET Identity is used in the Visual Studio 2013 Web Forms project template, as well as the templates for [ASP.NET MVC](../../../../mvc/index.md), [ASP.NET Web API](../../../../web-api/index.md), and [ASP.NET Single Page Application](../../../../single-page-application/index.md).</span></span> <span data-ttu-id="8f2c0-112">你还可以在使用空白 Web 应用程序启动时，使用 NuGet 专门安装 ASP.NET Identity 系统。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-112">You can also specifically install the ASP.NET Identity system using NuGet when you start with an empty Web application.</span></span> <span data-ttu-id="8f2c0-113">但是，在本教程系列中，你将使用**Web 窗体**projecttemplate，其中包含 ASP.NET Identity 系统。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-113">However, in this tutorial series you use the **Web Forms**projecttemplate, which includes the ASP.NET Identity system.</span></span> <span data-ttu-id="8f2c0-114">ASP.NET Identity 可以轻松地将特定于用户的配置文件数据与应用程序数据相集成。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-114">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="8f2c0-115">此外，ASP.NET 标识允许你为应用程序中的用户配置文件选择持久模型。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-115">Also, ASP.NET Identity allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="8f2c0-116">你可以将数据存储在 SQL Server 数据库或其他数据存储中，包括*NoSQL*数据存储，如 Windows Azure 存储表。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-116">You can store the data in a SQL Server database or another data store, including *NoSQL* data stores such as Windows Azure Storage Tables.</span></span>

<span data-ttu-id="8f2c0-117">本教程建立在 Wingtip 玩具教程系列标题为 "通过 PayPal 结帐和付款" 的前一教程中。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-117">This tutorial builds on the previous tutorial titled "Checkout and Payment with PayPal" in the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="8f2c0-118">学习内容：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-118">What you'll learn:</span></span>

- <span data-ttu-id="8f2c0-119">如何使用代码将自定义角色和用户添加到应用程序。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-119">How to use code to add a custom role and a user to the application.</span></span>
- <span data-ttu-id="8f2c0-120">如何限制对管理文件夹和页面的访问。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-120">How to restrict access to the administration folder and page.</span></span>
- <span data-ttu-id="8f2c0-121">如何为属于自定义角色的用户提供导航。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-121">How to provide navigation for the user that belongs to the custom role.</span></span>
- <span data-ttu-id="8f2c0-122">如何使用模型绑定填充产品类别的[DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx)控件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-122">How to use model binding to populate a [DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx) control with product categories.</span></span>
- <span data-ttu-id="8f2c0-123">如何使用[FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx)控件将文件上传到 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-123">How to upload a file to the web application using the [FileUpload](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx) control.</span></span>
- <span data-ttu-id="8f2c0-124">如何使用验证控件来实现输入验证。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-124">How to use validation controls to implement input validation.</span></span>
- <span data-ttu-id="8f2c0-125">如何在应用程序中添加和删除产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-125">How to add and remove products from the application.</span></span>

## <a name="these-features-are-included-in-the-tutorial"></a><span data-ttu-id="8f2c0-126">本教程包括以下功能：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-126">These features are included in the tutorial:</span></span>

- <span data-ttu-id="8f2c0-127">ASP.NET 标识</span><span class="sxs-lookup"><span data-stu-id="8f2c0-127">ASP.NET Identity</span></span>
- <span data-ttu-id="8f2c0-128">配置和授权</span><span class="sxs-lookup"><span data-stu-id="8f2c0-128">Configuration and Authorization</span></span>
- <span data-ttu-id="8f2c0-129">模型绑定</span><span class="sxs-lookup"><span data-stu-id="8f2c0-129">Model Binding</span></span>
- <span data-ttu-id="8f2c0-130">非引人注目验证</span><span class="sxs-lookup"><span data-stu-id="8f2c0-130">Unobtrusive Validation</span></span>

<span data-ttu-id="8f2c0-131">ASP.NET Web 窗体提供成员资格功能。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-131">ASP.NET Web Forms provides membership capabilities.</span></span> <span data-ttu-id="8f2c0-132">通过使用默认模板，您可以使用内置成员资格功能，以便在应用程序运行时立即使用。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-132">By using the default template, you have built-in membership functionality that you can immediately use when the application runs.</span></span> <span data-ttu-id="8f2c0-133">本教程演示如何使用 ASP.NET Identity 添加自定义角色并将用户分配给该角色。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-133">This tutorial shows you how to use ASP.NET Identity to add a custom role and assign a user to that role.</span></span> <span data-ttu-id="8f2c0-134">你将了解如何限制对管理文件夹的访问。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-134">You will learn how to restrict access to the administration folder.</span></span> <span data-ttu-id="8f2c0-135">你将向 "管理" 文件夹中添加一个页面，该页面允许具有自定义角色的用户添加和删除产品，以及在添加产品后预览产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-135">You'll add a page to the administration folder that allows a user with a custom role to add and remove products, and to preview a product after it has been added.</span></span>

## <a name="adding-a-custom-role"></a><span data-ttu-id="8f2c0-136">添加自定义角色</span><span class="sxs-lookup"><span data-stu-id="8f2c0-136">Adding a Custom Role</span></span>

<span data-ttu-id="8f2c0-137">使用 ASP.NET Identity，可以使用代码添加自定义角色并将用户分配给该角色。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-137">Using ASP.NET Identity, you can add a custom role and assign a user to that role using code.</span></span>

1. <span data-ttu-id="8f2c0-138">在**解决方案资源管理器**中，右键单击*逻辑*文件夹，然后创建新类。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-138">In **Solution Explorer**, right-click on the *Logic* folder and create a new class.</span></span>
2. <span data-ttu-id="8f2c0-139">将新类命名为*RoleActions.cs*。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-139">Name the new class *RoleActions.cs*.</span></span>
3. <span data-ttu-id="8f2c0-140">修改代码，使其显示如下：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-140">Modify the code so that it appears as follows:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. <span data-ttu-id="8f2c0-141">在**解决方案资源管理器**中，打开*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-141">In **Solution Explorer**, open the *Global.asax.cs* file.</span></span>
5. <span data-ttu-id="8f2c0-142">通过添加黄色突出显示的代码来修改*Global.asax.cs*文件，使其显示如下：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-142">Modify the *Global.asax.cs* file by adding the code highlighted in yellow so that it appears as follows:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. <span data-ttu-id="8f2c0-143">请注意，`AddUserAndRole` 将为红色且带下划线。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-143">Notice that `AddUserAndRole` is underlined in red.</span></span> <span data-ttu-id="8f2c0-144">双击 "AddUserAndRole" 代码。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-144">Double-click the AddUserAndRole code.</span></span>  
   <span data-ttu-id="8f2c0-145">突出显示的方法开头的字母 "A" 将带有下划线。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-145">The letter "A" at the beginning of the highlighted method will be underlined.</span></span>
7. <span data-ttu-id="8f2c0-146">将鼠标悬停在该字母 "A" 上，并单击允许您为 `AddUserAndRole` 方法生成方法存根的 UI。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-146">Hover over the letter "A" and click the UI that allows you to generate a method stub for the `AddUserAndRole` method.</span></span> 

    ![成员资格和管理-生成方法存根](membership-and-administration/_static/image1.png)
8. <span data-ttu-id="8f2c0-148">单击标题为以下内容的选项：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-148">Click the option titled:</span></span>  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. <span data-ttu-id="8f2c0-149">从*逻辑*文件夹打开*RoleActions.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-149">Open the *RoleActions.cs* file from the *Logic* folder.</span></span>  
   <span data-ttu-id="8f2c0-150">已将 `AddUserAndRole` 方法添加到了类文件中。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-150">The `AddUserAndRole` method has been added to the class file.</span></span>
10. <span data-ttu-id="8f2c0-151">通过删除 `NotImplementedException` 并添加以黄色突出显示的代码来修改*RoleActions.cs*文件，使其显示如下：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-151">Modify the *RoleActions.cs* file by removing the `NotImplementedException` and adding the code highlighted in yellow, so that it appears as follows:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

<span data-ttu-id="8f2c0-152">上面的代码首先为成员资格数据库建立数据库上下文。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-152">The above code first establishes a database context for the membership database.</span></span> <span data-ttu-id="8f2c0-153">成员资格数据库还以 *.mdf*文件的形式存储在*应用\_Data*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-153">The membership database is also stored as an *.mdf* file in the *App\_Data* folder.</span></span> <span data-ttu-id="8f2c0-154">第一个用户登录到此 web 应用程序后，你将能够查看此数据库。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-154">You will be able to view this database once the first user has signed in to this web application.</span></span> 

> [!NOTE] 
> 
> <span data-ttu-id="8f2c0-155">如果希望将成员资格数据与产品数据一起存储，可以考虑使用在上面的代码中用于存储产品数据的相同**DbContext** 。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-155">If you wish to store the membership data along with the product data, you can consider using the same **DbContext** that you used to store the product data in the above code.</span></span>

 <span data-ttu-id="8f2c0-156">*Internal*关键字是类型（如类）和类型成员（如方法或属性）的访问修饰符。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-156">The *internal* keyword is an access modifier for types (such as classes) and type members (such as methods or properties).</span></span> <span data-ttu-id="8f2c0-157">只能在同一程序集 *（.dll*文件）中包含的文件内访问内部类型或成员。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-157">Internal types or members are accessible only within files contained in the same assembly *(.dll* file).</span></span> <span data-ttu-id="8f2c0-158">生成应用程序时，将创建一个程序集文件 *（.dll*），其中包含运行应用程序时执行的代码。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-158">When you build your application, an assembly file *(.dll*) is created that contains the code that is executed when you run your application.</span></span> 

<span data-ttu-id="8f2c0-159">提供角色管理的 `RoleStore` 对象基于数据库上下文创建。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-159">A `RoleStore` object, which provides role management, is created based on the database context.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8f2c0-160">请注意，创建 `RoleStore` 对象时，它将使用泛型 `IdentityRole` 类型。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-160">Notice that when the `RoleStore` object is created it uses a Generic `IdentityRole` type.</span></span> <span data-ttu-id="8f2c0-161">这意味着 `RoleStore` 只允许包含 `IdentityRole` 对象。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-161">This means that the `RoleStore` is only allowed to contain `IdentityRole` objects.</span></span> <span data-ttu-id="8f2c0-162">此外，通过使用泛型，可以更好地处理内存中的资源。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-162">Also by using Generics, resources in memory are handled better.</span></span>

<span data-ttu-id="8f2c0-163">接下来，`RoleManager` 对象基于刚刚创建的 `RoleStore` 对象创建。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-163">Next, the `RoleManager` object, is created based on the `RoleStore` object that you just created.</span></span> <span data-ttu-id="8f2c0-164">`RoleManager` 对象公开与角色相关的 API，可用于自动将更改保存到 `RoleStore`。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-164">the `RoleManager` object exposes role related API which can be used to automatically save changes to the `RoleStore`.</span></span> <span data-ttu-id="8f2c0-165">只允许 `RoleManager` 包含 `IdentityRole` 对象，因为代码使用 `<IdentityRole>` 的泛型类型。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-165">The `RoleManager` is only allowed to contain `IdentityRole` objects because the code uses the `<IdentityRole>` Generic type.</span></span>

<span data-ttu-id="8f2c0-166">调用 `RoleExists` 方法来确定成员资格数据库中是否存在 "canEdit" 角色。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-166">You call the `RoleExists` method to determine if the "canEdit" role is present in the membership database.</span></span> <span data-ttu-id="8f2c0-167">如果不是，则创建角色。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-167">If it is not, you create the role.</span></span>

<span data-ttu-id="8f2c0-168">创建 `UserManager` 对象显得比 `RoleManager` 控件更复杂，但几乎相同。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-168">Creating the `UserManager` object appears to be more complicated than the `RoleManager` control, however it is nearly the same.</span></span> <span data-ttu-id="8f2c0-169">它只是在一行上编码，而不是在多行上编码。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-169">It is just coded on one line rather than several.</span></span> <span data-ttu-id="8f2c0-170">此处，要传递的参数将实例化为括号中包含的新对象。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-170">Here, the parameter that you are passing is instantiating as a new object contained in the parenthesis.</span></span>

<span data-ttu-id="8f2c0-171">接下来，通过创建新的 `ApplicationUser` 对象创建 "canEditUser" 用户。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-171">Next you create the "canEditUser" user by creating a new `ApplicationUser` object.</span></span> <span data-ttu-id="8f2c0-172">如果成功创建用户，请将该用户添加到新角色。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-172">Then, if you successfully create the user, you add the user to the new role.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="8f2c0-173">本系列教程后面的 "ASP.NET 错误处理" 教程中将更新错误处理。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-173">The error handling will be updated during the "ASP.NET Error Handling" tutorial later in this tutorial series.</span></span>

<span data-ttu-id="8f2c0-174">下一次启动应用程序时，会将名为 "canEditUser" 的用户添加为应用程序的名为 "canEdit" 的角色。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-174">The next time the application starts, the user named "canEditUser" will be added as the role named "canEdit" of the application.</span></span> <span data-ttu-id="8f2c0-175">稍后在本教程中，你将以 "canEditUser" 用户身份登录，以显示你将在本教程中添加的其他功能。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-175">Later in this tutorial, you will login as the "canEditUser" user to display additional capabilities that you will added during this tutorial.</span></span> <span data-ttu-id="8f2c0-176">有关 ASP.NET Identity 的 API 详细信息，请参阅 " [Microsoft Node.js 命名空间](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx)"。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-176">For API details about ASP.NET Identity, see the [Microsoft.AspNet.Identity Namespace](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx).</span></span> <span data-ttu-id="8f2c0-177">有关初始化 ASP.NET Identity 系统的其他详细信息，请参阅[AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs)。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-177">For additional details about initializing the ASP.NET Identity system, see the [AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs).</span></span>

### <a name="restricting-access-to-the-administration-page"></a><span data-ttu-id="8f2c0-178">限制对管理页的访问</span><span class="sxs-lookup"><span data-stu-id="8f2c0-178">Restricting Access to the Administration Page</span></span>

<span data-ttu-id="8f2c0-179">Wingtip 玩具示例应用程序允许匿名用户和已登录用户查看和购买产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-179">The Wingtip Toys sample application allows both anonymous users and logged-in users to view and purchase products.</span></span> <span data-ttu-id="8f2c0-180">但是，具有自定义 "canEdit" 角色的已登录用户可以访问受限制的页面，以便添加和删除产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-180">However, the logged-in user that has the custom "canEdit" role can access a restricted page in order to add and remove products.</span></span>

#### <a name="add-an-administration-folder-and-page"></a><span data-ttu-id="8f2c0-181">添加管理文件夹和页面</span><span class="sxs-lookup"><span data-stu-id="8f2c0-181">Add an Administration Folder and Page</span></span>

<span data-ttu-id="8f2c0-182">接下来，你将为属于 Wingtip 玩具示例应用程序的自定义角色的 "canEditUser" 用户创建名为*Admin*的文件夹。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-182">Next, you will create a folder named *Admin* for the "canEditUser" user belonging to the custom role of the Wingtip Toys sample application.</span></span>

1. <span data-ttu-id="8f2c0-183">在**解决方案资源管理器**中右键单击项目名称（**Wingtip 玩具**），然后选择 "**添加** -&gt;**新文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-183">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add** -&gt; **New Folder**.</span></span>
2. <span data-ttu-id="8f2c0-184">将新文件夹命名为 "*管理员*"。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-184">Name the new folder *Admin*.</span></span>
3. <span data-ttu-id="8f2c0-185">右键单击 "*管理*" 文件夹，然后选择 "**添加** -&gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-185">Right-click the *Admin* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="8f2c0-186">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-186">The **Add New Item** dialog box is displayed.</span></span>
4. <span data-ttu-id="8f2c0-187">选择左侧的 " <strong>Visual C#</strong> -&gt; <strong>Web</strong>模板" 组。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-187">Select the <strong>Visual C#</strong>-&gt; <strong>Web</strong> templates group on the left.</span></span> <span data-ttu-id="8f2c0-188">从中间列表中，选择 "<strong>带有母版页的 Web 窗体</strong>"，将其命名为<em>AdminPage</em>，然后选择 "<strong>添加</strong><strong>"</strong> 。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-188">From the middle list, select <strong>Web Form with Master Page</strong>,name it <em>AdminPage.aspx</em><strong>,</strong> and then select <strong>Add</strong>.</span></span>
5. <span data-ttu-id="8f2c0-189">选择 "*网站*" 作为母版页的主文件，然后选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-189">Select the *Site.Master* file as the master page, and then choose **OK**.</span></span>

#### <a name="add-a-webconfig-file"></a><span data-ttu-id="8f2c0-190">添加 web.config 文件</span><span class="sxs-lookup"><span data-stu-id="8f2c0-190">Add a Web.config File</span></span>

<span data-ttu-id="8f2c0-191">通过将*web.config*文件添加到*管理*文件夹，可以限制对文件夹中包含的页的访问。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-191">By adding a *Web.config* file to the *Admin* folder, you can restrict access to the page contained in the folder.</span></span>

1. <span data-ttu-id="8f2c0-192">右键单击 "*管理*" 文件夹，然后选择 "**添加** -&gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-192">Right-click the *Admin* folder and select **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="8f2c0-193">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-193">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="8f2c0-194">C#从 Visual web 模板列表中，从中间列表中选择 " <strong>web 配置文件</strong>"，接受 web.config 的默认<strong>名称，然后</strong>选择 "<strong>添加</strong>"。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-194">From the list of Visual C# web templates, select <strong>Web Configuration File</strong>from the middle list, accept the default name of <em>Web.config</em><strong>,</strong> and then select <strong>Add</strong>.</span></span>
3. <span data-ttu-id="8f2c0-195">*将 web.config 文件中*的现有 XML 内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-195">Replace the existing XML content in the *Web.config* file with the following:</span></span>  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

<span data-ttu-id="8f2c0-196">保存 *Web.config* 文件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-196">Save the *Web.config* file.</span></span> <span data-ttu-id="8f2c0-197">Web.config*文件指定*只有属于应用程序的 "canEdit" 角色的用户才能访问*管理*文件夹中包含的页。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-197">The *Web.config* file specifies that only user belonging to the "canEdit" role of the application can access the page contained in the *Admin* folder.</span></span>

### <a name="including-custom-role-navigation"></a><span data-ttu-id="8f2c0-198">包括自定义角色导航</span><span class="sxs-lookup"><span data-stu-id="8f2c0-198">Including Custom Role Navigation</span></span>

<span data-ttu-id="8f2c0-199">若要使自定义 "canEdit" 角色的用户可以导航到应用程序的 "管理" 部分，必须将链接添加到*网站母版页*。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-199">To enable the user of the custom "canEdit" role to navigate to the administration section of the application, you must add a link to the *Site.Master* page.</span></span> <span data-ttu-id="8f2c0-200">只有属于 "canEdit" 角色的用户才能看到 "**管理员**" 链接并访问 "管理" 部分。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-200">Only users that belong to the "canEdit" role will be able to see the **Admin** link and access the administration section.</span></span>

1. <span data-ttu-id="8f2c0-201">在解决方案资源管理器中，查找并打开 "*网站母版页*"。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-201">In Solution Explorer, find and open the *Site.Master* page.</span></span>
2. <span data-ttu-id="8f2c0-202">若要为 "canEdit" 角色的用户创建链接，请将黄色突出显示的标记添加 `<ul>` 元素，以便列表如下所示：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-202">To create a link for the user of the "canEdit" role, add the markup highlighted in yellow to the following unordered list `<ul>` element so that the list appears as follows:</span></span>  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. <span data-ttu-id="8f2c0-203">打开*Site.Master.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-203">Open the *Site.Master.cs* file.</span></span> <span data-ttu-id="8f2c0-204">通过将黄色突出显示的代码添加到 `Page_Load` 处理程序，使**管理员**链接仅对 "canEditUser" 用户可见。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-204">Make the **Admin** link visible only to the "canEditUser" user by adding the code highlighted in yellow to the `Page_Load` handler.</span></span> <span data-ttu-id="8f2c0-205">`Page_Load` 处理程序将如下所示：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-205">The `Page_Load` handler will appear as follows:</span></span>   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

<span data-ttu-id="8f2c0-206">加载页面时，代码会检查登录用户是否具有 "canEdit" 角色。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-206">When the page loads, the code checks whether the logged-in user has the role of "canEdit".</span></span> <span data-ttu-id="8f2c0-207">如果用户属于 "canEdit" 角色，则会使包含指向*AdminPage*页面的链接的 span 元素（进而使范围内的链接）变得可见。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-207">If the user belongs to the "canEdit" role, the span element containing the link to the *AdminPage.aspx* page (and consequently the link inside the span) is made visible.</span></span>

### <a name="enabling-product-administration"></a><span data-ttu-id="8f2c0-208">启用产品管理</span><span class="sxs-lookup"><span data-stu-id="8f2c0-208">Enabling Product Administration</span></span>

<span data-ttu-id="8f2c0-209">到目前为止，您已经创建了 "canEdit" 角色并添加了 "canEditUser" 用户、管理文件夹和管理页面。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-209">So far, you have created the "canEdit" role and added an "canEditUser" user, an administration folder, and an administration page.</span></span> <span data-ttu-id="8f2c0-210">已为管理文件夹和页面设置访问权限，并已将 "canEdit" 角色的用户的导航链接添加到了应用程序。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-210">You have set access rights for the administration folder and page, and have added a navigation link for the user of the "canEdit" role to the application.</span></span> <span data-ttu-id="8f2c0-211">接下来，您将向*AdminPage*页和代码添加标记，将其添加到*AdminPage.aspx.cs*代码隐藏文件中，该文件允许具有 "canEdit" 角色的用户添加和删除产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-211">Next, you will add markup to the *AdminPage.aspx* page and code to the *AdminPage.aspx.cs* code-behind file that will enable the user with the "canEdit" role to add and remove products.</span></span>

1. <span data-ttu-id="8f2c0-212">在**解决方案资源管理器**中，打开*管理*文件夹中的*AdminPage*文件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-212">In **Solution Explorer**, open the *AdminPage.aspx* file from the *Admin* folder.</span></span>
2. <span data-ttu-id="8f2c0-213">将现有标记替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-213">Replace the existing markup with the following:</span></span>  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. <span data-ttu-id="8f2c0-214">接下来，通过右键单击 " *AdminPage* " 并单击 "**查看代码**" 来打开*AdminPage.aspx.cs*代码隐藏文件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-214">Next, open the *AdminPage.aspx.cs* code-behind file by right-clicking the *AdminPage.aspx* and clicking **View Code**.</span></span>
4. <span data-ttu-id="8f2c0-215">将*AdminPage.aspx.cs*代码隐藏文件中的现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-215">Replace the existing code in the *AdminPage.aspx.cs* code-behind file with the following code:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

<span data-ttu-id="8f2c0-216">在为*AdminPage.aspx.cs*代码隐藏文件输入的代码中，名为 `AddProducts` 的类将执行将产品添加到数据库的实际工作。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-216">In the code that you entered for the *AdminPage.aspx.cs* code-behind file, a class called `AddProducts` does the actual work of adding products to the database.</span></span> <span data-ttu-id="8f2c0-217">此类尚不存在，因此你现在会创建它。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-217">This class doesn't exist yet, so you will create it now.</span></span>

1. <span data-ttu-id="8f2c0-218">在**解决方案资源管理器**中，右键单击*逻辑*文件夹，然后选择 "**添加** -&gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-218">In **Solution Explorer**, right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="8f2c0-219">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-219">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="8f2c0-220">选择左侧的 " **Visual C#**  -&gt;**代码**模板" 组。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-220">Select the **Visual C#** -&gt; **Code** templates group on the left.</span></span> <span data-ttu-id="8f2c0-221">然后，从中间列表中选择 "**类**"，并将其命名为*AddProducts.cs*。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-221">Then, select **Class**from the middle list and name it *AddProducts.cs*.</span></span>   
   <span data-ttu-id="8f2c0-222">将显示新的类文件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-222">The new class file is displayed.</span></span>
3. <span data-ttu-id="8f2c0-223">将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-223">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

<span data-ttu-id="8f2c0-224">*AdminPage*页允许属于 "canEdit" 角色的用户添加和删除产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-224">The *AdminPage.aspx* page allows the user belonging to the "canEdit" role to add and remove products.</span></span> <span data-ttu-id="8f2c0-225">添加新产品后，将验证有关该产品的详细信息，并将其输入到数据库中。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-225">When a new product is added, the details about the product are validated and then entered into the database.</span></span> <span data-ttu-id="8f2c0-226">新产品立即可供 web 应用程序的所有用户使用。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-226">The new product is immediately available to all users of the web application.</span></span>

#### <a name="unobtrusive-validation"></a><span data-ttu-id="8f2c0-227">非引人注目验证</span><span class="sxs-lookup"><span data-stu-id="8f2c0-227">Unobtrusive Validation</span></span>

<span data-ttu-id="8f2c0-228">用户在*AdminPage*页上提供的产品详细信息使用验证控件（`RequiredFieldValidator` 和 `RegularExpressionValidator`）进行验证。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-228">The product details that the user provides on the *AdminPage.aspx* page are validated using validation controls (`RequiredFieldValidator` and `RegularExpressionValidator`).</span></span> <span data-ttu-id="8f2c0-229">这些控件会自动使用不引人注目的验证。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-229">These controls automatically use unobtrusive validation.</span></span> <span data-ttu-id="8f2c0-230">非介入式验证允许验证控件将 JavaScript 用于客户端验证逻辑，这意味着该页不需要与服务器进行验证。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-230">Unobtrusive validation allows the validation controls to use JavaScript for client-side validation logic, which means the page does not require a trip to the server to be validated.</span></span> <span data-ttu-id="8f2c0-231">默认情况下，基于以下配置设置，不引人注目的验证包含在*web.config 文件中*：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-231">By default, unobtrusive validation is included in the *Web.config* file based on the following configuration setting:</span></span>

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a><span data-ttu-id="8f2c0-232">正则表达式</span><span class="sxs-lookup"><span data-stu-id="8f2c0-232">Regular Expressions</span></span>

<span data-ttu-id="8f2c0-233">使用**RegularExpressionValidator**控件验证*AdminPage*页上的产品价格。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-233">The product price on the *AdminPage.aspx* page is validated using a **RegularExpressionValidator** control.</span></span> <span data-ttu-id="8f2c0-234">此控件验证关联的输入控件（"AddProductPrice" 文本框）的值是否与正则表达式指定的模式匹配。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-234">This control validates whether the value of the associated input control (the "AddProductPrice" TextBox) matches the pattern specified by the regular expression.</span></span> <span data-ttu-id="8f2c0-235">正则表达式是模式匹配表示法，可用于快速查找和匹配特定字符模式。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-235">A regular expression is a pattern-matching notation that enables you to quickly find and match specific character patterns.</span></span> <span data-ttu-id="8f2c0-236">**RegularExpressionValidator**控件包含一个名为 `ValidationExpression` 的属性，该属性包含用于验证价格输入的正则表达式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-236">The **RegularExpressionValidator** control includes a property named `ValidationExpression` that contains the regular expression used to validate price input, as shown below:</span></span>

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a><span data-ttu-id="8f2c0-237">FileUpload 控件</span><span class="sxs-lookup"><span data-stu-id="8f2c0-237">FileUpload Control</span></span>

<span data-ttu-id="8f2c0-238">除了输入和验证控件外，还可以将**FileUpload**控件添加到*AdminPage*页。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-238">In addition to the input and validation controls, you added the **FileUpload** control to the *AdminPage.aspx* page.</span></span> <span data-ttu-id="8f2c0-239">此控件提供上传文件的功能。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-239">This control provides the capability to upload files.</span></span> <span data-ttu-id="8f2c0-240">在这种情况下，只允许上传图像文件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-240">In this case, you are only allowing image files to be uploaded.</span></span> <span data-ttu-id="8f2c0-241">在代码隐藏文件（*AdminPage.aspx.cs*）中，单击 `AddProductButton` 时，代码会检查**FileUpload**控件的 `HasFile` 属性。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-241">In the code-behind file (*AdminPage.aspx.cs*), when the `AddProductButton` is clicked, the code checks the `HasFile` property of the **FileUpload** control.</span></span> <span data-ttu-id="8f2c0-242">如果控件包含文件，并且允许文件类型（基于文件扩展名），则图像将保存到*images*文件夹和应用程序的*images/拇指*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-242">If the control has a file and if the file type (based on file extension) is allowed, the image is saved to the *Images* folder and the *Images/Thumbs* folder of the application.</span></span>

#### <a name="model-binding"></a><span data-ttu-id="8f2c0-243">模型绑定</span><span class="sxs-lookup"><span data-stu-id="8f2c0-243">Model Binding</span></span>

<span data-ttu-id="8f2c0-244">在本教程的前面部分，你使用了模型绑定来填充**ListView**控件、 **FormsView**控件、 **GridView**控件和**DetailView**控件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-244">Earlier in this tutorial series you used model binding to populate a **ListView** control, a **FormsView** control, a **GridView** control, and a **DetailView** control.</span></span> <span data-ttu-id="8f2c0-245">在本教程中，您将使用模型绑定来用产品类别列表填充**DropDownList**控件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-245">In this tutorial, you use model binding to populate a **DropDownList** control with a list of product categories.</span></span>

<span data-ttu-id="8f2c0-246">添加到*AdminPage*文件的标记包含名为 `DropDownAddCategory`的**DropDownList**控件：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-246">The markup that you added to the *AdminPage.aspx* file contains a **DropDownList** control called `DropDownAddCategory`:</span></span>

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

<span data-ttu-id="8f2c0-247">通过设置 `ItemType` 特性和 `SelectMethod` 特性，可以使用模型绑定来填充此**DropDownList** 。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-247">You use model binding to populate this **DropDownList** by setting the `ItemType` attribute and the `SelectMethod` attribute.</span></span> <span data-ttu-id="8f2c0-248">`ItemType` 特性指定在填充控件时使用 `WingtipToys.Models.Category` 类型。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-248">The `ItemType` attribute specifies that you use the `WingtipToys.Models.Category` type when populating the control.</span></span> <span data-ttu-id="8f2c0-249">可以通过创建 `Category` 类（如下所示）在本教程系列的开头定义此类型。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-249">You defined this type at the beginning of this tutorial series by creating the `Category` class (shown below).</span></span> <span data-ttu-id="8f2c0-250">`Category` 类位于*Category.cs*文件中的 "*模型*" 文件夹内。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-250">The `Category` class is in the *Models* folder inside the *Category.cs* file.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

<span data-ttu-id="8f2c0-251">**DropDownList**控件的 `SelectMethod` 特性指定你使用代码隐藏文件（*AdminPage.aspx.cs*）中包含的 `GetCategories` 方法（如下所示）。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-251">The `SelectMethod` attribute of the **DropDownList** control specifies that you use the `GetCategories` method (shown below) that is included in the code-behind file (*AdminPage.aspx.cs*).</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

<span data-ttu-id="8f2c0-252">此方法指定使用 `IQueryable` 接口来计算针对 `Category` 类型的查询。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-252">This method specifies that an `IQueryable` interface is used to evaluate a query against a `Category` type.</span></span> <span data-ttu-id="8f2c0-253">返回的值用于填充页面标记中的**DropDownList** （*AdminPage*）。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-253">The returned value is used to populate the **DropDownList** in the markup of the page (*AdminPage.aspx*).</span></span>

<span data-ttu-id="8f2c0-254">为列表中的每个项显示的文本通过设置 `DataTextField` 特性来指定。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-254">The text displayed for each item in the list is specified by setting the `DataTextField` attribute.</span></span> <span data-ttu-id="8f2c0-255">`DataTextField` 属性使用 `Category` 类的 `CategoryName` （如上所示）显示**DropDownList**控件中的每个类别。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-255">The `DataTextField` attribute uses the `CategoryName` of the `Category` class (shown above) to display each category in the **DropDownList** control.</span></span> <span data-ttu-id="8f2c0-256">在**DropDownList**控件中选择项时所传递的实际值基于 `DataValueField` 特性。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-256">The actual value that is passed when an item is selected in the **DropDownList** control is based on the `DataValueField` attribute.</span></span> <span data-ttu-id="8f2c0-257">`DataValueField` 特性设置为 `CategoryID` 在 `Category` 类中为 define （如上所示）。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-257">The `DataValueField` attribute is set to the `CategoryID` as define in the `Category` class (shown above).</span></span>

### <a name="how-the-application-will-work"></a><span data-ttu-id="8f2c0-258">应用程序的工作原理</span><span class="sxs-lookup"><span data-stu-id="8f2c0-258">How the Application Will Work</span></span>

<span data-ttu-id="8f2c0-259">当属于 "canEdit" 角色的用户第一次导航到页面时，将按照上述说明填充 `DropDownAddCategory`**DropDownList**控件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-259">When the user belonging to the "canEdit" role navigates to the page for the first time, the `DropDownAddCategory`**DropDownList** control is populated as described above.</span></span> <span data-ttu-id="8f2c0-260">`DropDownRemoveProduct`**DropDownList**控件也使用相同的方法填充产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-260">The `DropDownRemoveProduct`**DropDownList** control is also populated with products using the same approach.</span></span> <span data-ttu-id="8f2c0-261">属于 "canEdit" 角色的用户选择类别类型并添加产品详细信息（**名称**、**说明**、**价格**和**图像文件**）。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-261">The user belonging to the "canEdit" role selects the category type and adds product details (**Name**, **Description**, **Price**, and **Image File**).</span></span> <span data-ttu-id="8f2c0-262">当属于 "canEdit" 角色的用户单击 "**添加产品**" 按钮时，将触发 `AddProductButton_Click` 事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-262">When the user belonging to the "canEdit" role clicks the **Add Product** button, the `AddProductButton_Click` event handler is triggered.</span></span> <span data-ttu-id="8f2c0-263">位于代码隐藏文件（*AdminPage.aspx.cs*）中的 `AddProductButton_Click` 事件处理程序将检查映像文件，以确保它与允许的文件类型 *（.gif*、 *.png*、 *jpeg*或 *.jpg*）相匹配。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-263">The `AddProductButton_Click` event handler located in the code-behind file (*AdminPage.aspx.cs*) checks the image file to make sure it matches the allowed file types *(.gif*, *.png*, *.jpeg*, or *.jpg*).</span></span> <span data-ttu-id="8f2c0-264">然后，将图像文件保存到 Wingtip 玩具示例应用程序的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-264">Then, the image file is saved into a folder of the Wingtip Toys sample application.</span></span> <span data-ttu-id="8f2c0-265">接下来，将新产品添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-265">Next, the new product is added to the database.</span></span> <span data-ttu-id="8f2c0-266">为了实现新的产品，将创建 `AddProducts` 类的新实例，并将其命名为 "产品"。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-266">To accomplish adding a new product, a new instance of the `AddProducts` class is created and named products.</span></span> <span data-ttu-id="8f2c0-267">`AddProducts` 类具有一个名为 `AddProduct`的方法，products 对象调用此方法将产品添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-267">The `AddProducts` class has a method named `AddProduct`, and the products object calls this method to add products to the database.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

<span data-ttu-id="8f2c0-268">如果代码成功将新产品添加到数据库，则会重新加载该页面，并 `ProductAction=add`查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-268">If the code successfully adds the new product to the database, the page is reloaded with the query string value `ProductAction=add`.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

<span data-ttu-id="8f2c0-269">重新加载页面时，查询字符串将包含在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-269">When the page reloads, the query string is included in the URL.</span></span> <span data-ttu-id="8f2c0-270">通过重新加载页面，属于 "canEdit" 角色的用户可以立即在*AdminPage*页面上的**DropDownList**控件中查看更新。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-270">By reloading the page, the user belonging to the "canEdit" role can immediately see the updates in the **DropDownList** controls on the *AdminPage.aspx* page.</span></span> <span data-ttu-id="8f2c0-271">此外，通过在 URL 中包含查询字符串，页面可以向属于 "canEdit" 角色的用户显示一条成功消息。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-271">Also, by including the query string with the URL, the page can display a success message to the user belonging to the "canEdit" role.</span></span>

<span data-ttu-id="8f2c0-272">当*AdminPage*页重新加载时，将调用 `Page_Load` 事件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-272">When the *AdminPage.aspx* page reloads, the `Page_Load` event is called.</span></span>

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

<span data-ttu-id="8f2c0-273">`Page_Load` 事件处理程序检查查询字符串值，并确定是否显示成功消息。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-273">The `Page_Load` event handler checks the query string value and determines whether to show a success message.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="8f2c0-274">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="8f2c0-274">Running the Application</span></span>

<span data-ttu-id="8f2c0-275">现在可以运行应用程序，了解如何添加、删除和更新购物车中的项目。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-275">You can run the application now to see how you can add, delete, and update items in the shopping cart.</span></span> <span data-ttu-id="8f2c0-276">购物车总计将反映购物车中所有物品的总成本。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-276">The shopping cart total will reflect the total cost of all items in the shopping cart.</span></span>

1. <span data-ttu-id="8f2c0-277">在解决方案资源管理器中，按**F5**运行 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-277">In Solution Explorer, press **F5** to run the Wingtip Toys sample application.</span></span>  
   <span data-ttu-id="8f2c0-278">浏览器将打开并显示*default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-278">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="8f2c0-279">单击页面顶部的 "**登录**" 链接。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-279">Click the **Log in** link at the top of the page.</span></span> 

    ![成员身份和管理-登录链接](membership-and-administration/_static/image2.png)

   <span data-ttu-id="8f2c0-281">将显示*登录 .aspx*页。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-281">The *Login.aspx* page is displayed.</span></span>
3. <span data-ttu-id="8f2c0-282">使用以下用户名和密码：</span><span class="sxs-lookup"><span data-stu-id="8f2c0-282">Use the following user name and password:</span></span>  
   <span data-ttu-id="8f2c0-283">用户名： canEditUser@wingtiptoys.com</span><span class="sxs-lookup"><span data-stu-id="8f2c0-283">User name: canEditUser@wingtiptoys.com</span></span>  
   <span data-ttu-id="8f2c0-284">密码： Pa $ $word 1</span><span class="sxs-lookup"><span data-stu-id="8f2c0-284">Password: Pa$$word1</span></span> 

    ![成员资格和管理-登录页](membership-and-administration/_static/image3.png)
4. <span data-ttu-id="8f2c0-286">单击页面底部附近的 "**登录**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-286">Click the **Log in** button near the bottom of the page.</span></span>
5. <span data-ttu-id="8f2c0-287">在下一页的顶部，选择 "**管理**" 链接以导航到 " *AdminPage* " 页。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-287">At the top of the next page, select the **Admin** link to navigate to the *AdminPage.aspx* page.</span></span> 

    ![成员身份和管理-管理链接](membership-and-administration/_static/image4.png)
6. <span data-ttu-id="8f2c0-289">若要测试输入验证，请单击 "**添加产品**" 按钮，而不添加任何产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-289">To test the input validation, click the **Add Product** button without adding any product details.</span></span> 

    ![成员资格和管理-管理页面](membership-and-administration/_static/image5.png)

   <span data-ttu-id="8f2c0-291">请注意，将显示必填字段消息。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-291">Notice that the required field messages are displayed.</span></span>
7. <span data-ttu-id="8f2c0-292">为新产品添加详细信息，然后单击 "**添加产品**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-292">Add the details for a new product, and then click the **Add Product** button.</span></span> 

    ![成员资格和管理-添加产品](membership-and-administration/_static/image6.png)
8. <span data-ttu-id="8f2c0-294">从顶部导航菜单中选择 "**产品**"，以查看添加的新产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-294">Select **Products** from the top navigation menu to view the new product you added.</span></span> 

    ![成员资格和管理-显示新产品](membership-and-administration/_static/image7.png)
9. <span data-ttu-id="8f2c0-296">单击 "**管理**" 链接以返回到 "管理" 页。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-296">Click the **Admin** link to return to the administration page.</span></span>
10. <span data-ttu-id="8f2c0-297">在页面的 "**删除产品**" 部分中，选择在**DropDownListBox**中添加的新产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-297">In the **Remove Product** section of the page, select the new product you added in the **DropDownListBox**.</span></span>
11. <span data-ttu-id="8f2c0-298">单击 "**删除产品**" 按钮，从应用程序中删除新产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-298">Click the **Remove Product** button to remove the new product from the application.</span></span> 

    ![成员资格和管理-删除产品](membership-and-administration/_static/image8.png)
12. <span data-ttu-id="8f2c0-300">从顶部导航菜单中选择 "**产品**"，确认已删除该产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-300">Select **Products** from the top navigation menu to confirm that the product has been removed.</span></span>
13. <span data-ttu-id="8f2c0-301">单击 "**注销**" 以存在管理模式。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-301">Click **Log off** to exist administration mode.</span></span>   
    <span data-ttu-id="8f2c0-302">请注意，顶部导航窗格不再显示 "**管理**" 菜单项。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-302">Notice that the top navigation pane no longer shows the **Admin** menu item.</span></span>

## <a name="summary"></a><span data-ttu-id="8f2c0-303">摘要</span><span class="sxs-lookup"><span data-stu-id="8f2c0-303">Summary</span></span>

<span data-ttu-id="8f2c0-304">在本教程中，你添加了一个自定义角色和一个属于该自定义角色的用户、对管理文件夹和页面的有限访问权限，并为属于该自定义角色的用户提供了导航。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-304">In this tutorial, you added a custom role and a user belonging to the custom role, restricted access to the administration folder and page, and provided navigation for the user belonging to the custom role.</span></span> <span data-ttu-id="8f2c0-305">你使用了模型绑定来用数据填充**DropDownList**控件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-305">You used model binding to populate a **DropDownList** control with data.</span></span> <span data-ttu-id="8f2c0-306">实现了**FileUpload**控件和验证控件。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-306">You implemented the **FileUpload** control and validation controls.</span></span> <span data-ttu-id="8f2c0-307">此外，您还了解了如何在数据库中添加和删除产品。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-307">Also, you have learned how to add and remove products from a database.</span></span> <span data-ttu-id="8f2c0-308">在下一教程中，你将学习如何实现 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="8f2c0-308">In the next tutorial, you'll learn how to implement ASP.NET routing.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f2c0-309">其他资源</span><span class="sxs-lookup"><span data-stu-id="8f2c0-309">Additional Resources</span></span>

<span data-ttu-id="8f2c0-310">[Web.config-authorization 元素](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="8f2c0-310">[Web.config - authorization Element](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)</span></span>  
[<span data-ttu-id="8f2c0-311">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="8f2c0-311">ASP.NET Identity</span></span>](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[<span data-ttu-id="8f2c0-312">使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure 网站</span><span class="sxs-lookup"><span data-stu-id="8f2c0-312">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Web Site</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="8f2c0-313">Microsoft Azure 免费试用版</span><span class="sxs-lookup"><span data-stu-id="8f2c0-313">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="8f2c0-314">[上一页](checkout-and-payment-with-paypal.md)
> [下一页](url-routing.md)</span><span class="sxs-lookup"><span data-stu-id="8f2c0-314">[Previous](checkout-and-payment-with-paypal.md)
[Next](url-routing.md)</span></span>
