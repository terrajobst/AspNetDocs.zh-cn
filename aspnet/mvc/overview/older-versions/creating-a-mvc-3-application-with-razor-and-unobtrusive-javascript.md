---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: 使用 Razor 和非引人注目的 JavaScript 创建 MVC 3 应用程序 |Microsoft Docs
author: microsoft
description: 用户列表示例 web 应用程序演示了使用 Razor 视图引擎创建 ASP.NET MVC 3 应用程序的简单方法。 示例应用程序 。
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434996"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="41010-104">使用 Razor 和非介入性 JavaScript 创建 MVC 3 应用程序</span><span class="sxs-lookup"><span data-stu-id="41010-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="41010-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="41010-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="41010-106">用户列表示例 web 应用程序演示了使用 Razor 视图引擎创建 ASP.NET MVC 3 应用程序的简单方法。</span><span class="sxs-lookup"><span data-stu-id="41010-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="41010-107">该示例应用程序演示了如何将新的 Razor 视图引擎与 ASP.NET MVC 版本3和 Visual Studio 2010 一起使用，以创建包含创建、显示、编辑和删除用户等功能的虚拟用户列表网站。</span><span class="sxs-lookup"><span data-stu-id="41010-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="41010-108">本教程介绍了生成用户列表示例 ASP.NET MVC 3 应用程序所采取的步骤。</span><span class="sxs-lookup"><span data-stu-id="41010-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="41010-109">本主题附带有与C#和 VB 源代码的 Visual Studio 项目：[下载](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114)。</span><span class="sxs-lookup"><span data-stu-id="41010-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="41010-110">如果你有关于本教程的问题，请将其发布到[MVC 论坛](https://forums.asp.net/1146.aspx)。</span><span class="sxs-lookup"><span data-stu-id="41010-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="41010-111">概述</span><span class="sxs-lookup"><span data-stu-id="41010-111">Overview</span></span>

<span data-ttu-id="41010-112">要构建的应用程序是一个简单的用户列表网站。</span><span class="sxs-lookup"><span data-stu-id="41010-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="41010-113">用户可以输入、查看和更新用户信息。</span><span class="sxs-lookup"><span data-stu-id="41010-113">Users can enter, view, and update user information.</span></span>

![示例站点](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="41010-115">可在此处下载 VB 和C#已完成[here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)的项目。</span><span class="sxs-lookup"><span data-stu-id="41010-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="41010-116">创建 Web 应用程序</span><span class="sxs-lookup"><span data-stu-id="41010-116">Creating the Web Application</span></span>

<span data-ttu-id="41010-117">若要开始学习本教程，请打开 Visual Studio 2010 并使用 " *ASP.NET MVC 3 Web 应用程序*" 模板创建一个新项目。</span><span class="sxs-lookup"><span data-stu-id="41010-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="41010-118">将应用程序命名 &quot;Mvc3Razor&quot;。</span><span class="sxs-lookup"><span data-stu-id="41010-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="41010-119">[![新的 MVC 3 项目](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="41010-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="41010-120">在 "**新建 ASP.NET MVC 3 项目**" 对话框中，选择 " **Internet 应用程序**"，选择 "Razor" 视图引擎，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="41010-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![New ASP.NET MVC 3 项目对话框](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="41010-122">在本教程中，你将不使用 ASP.NET 成员资格提供程序，因此你可以删除与登录名和成员身份关联的所有文件。</span><span class="sxs-lookup"><span data-stu-id="41010-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="41010-123">在**解决方案资源管理器**中，删除以下文件和目录：</span><span class="sxs-lookup"><span data-stu-id="41010-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="41010-124">*Controllers\AccountController*</span><span class="sxs-lookup"><span data-stu-id="41010-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="41010-125">*Models\AccountModels*</span><span class="sxs-lookup"><span data-stu-id="41010-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="41010-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="41010-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="41010-127">*Views\Account* （以及此目录中的所有文件）</span><span class="sxs-lookup"><span data-stu-id="41010-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln Exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="41010-129">编辑<em>\_的布局 cshtml</em>文件，并<em>&quot;</em>将名为 `logindisplay` 的 `<div>` 元素内的标记替换为禁用了 "已禁用登录名"&quot;。</span><span class="sxs-lookup"><span data-stu-id="41010-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="41010-130">下面的示例显示了新标记：</span><span class="sxs-lookup"><span data-stu-id="41010-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="41010-131">添加模型</span><span class="sxs-lookup"><span data-stu-id="41010-131">Adding the Model</span></span>

<span data-ttu-id="41010-132">在**解决方案资源管理器**中，右键单击 "*模型*" 文件夹，选择 "**添加**"，然后单击 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="41010-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![新用户 Mdl 类](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="41010-134">将此类命名为 `UserModel`。</span><span class="sxs-lookup"><span data-stu-id="41010-134">Name the class `UserModel`.</span></span> <span data-ttu-id="41010-135">将*UserModel*文件的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="41010-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="41010-136">`UserModel` 类表示用户。</span><span class="sxs-lookup"><span data-stu-id="41010-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="41010-137">类的每个成员都用[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间中的[必需](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性进行批注。</span><span class="sxs-lookup"><span data-stu-id="41010-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="41010-138">[DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)命名空间中的属性为 web 应用程序提供自动的客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="41010-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="41010-139">打开 `HomeController` 类并添加 `using` 指令，以便可以访问 `UserModel` 和 `Users` 类：</span><span class="sxs-lookup"><span data-stu-id="41010-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="41010-140">在 `HomeController` 声明的后面，添加以下注释和对 `Users` 类的引用：</span><span class="sxs-lookup"><span data-stu-id="41010-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="41010-141">`Users` 类是一种简化的内存中数据存储区，你将在本教程中使用它。</span><span class="sxs-lookup"><span data-stu-id="41010-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="41010-142">在实际应用程序中，您将使用数据库来存储用户信息。</span><span class="sxs-lookup"><span data-stu-id="41010-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="41010-143">下面的示例演示了 `HomeController` 文件的前几行：</span><span class="sxs-lookup"><span data-stu-id="41010-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="41010-144">构建应用程序，以便在下一步中将用户模型提供给基架向导使用。</span><span class="sxs-lookup"><span data-stu-id="41010-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="41010-145">创建默认视图</span><span class="sxs-lookup"><span data-stu-id="41010-145">Creating the Default View</span></span>

<span data-ttu-id="41010-146">下一步是添加操作方法和视图以显示用户。</span><span class="sxs-lookup"><span data-stu-id="41010-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="41010-147">删除现有的*Views\Home\Index*文件。</span><span class="sxs-lookup"><span data-stu-id="41010-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="41010-148">您将创建一个新的*索引*文件以显示用户。</span><span class="sxs-lookup"><span data-stu-id="41010-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="41010-149">在 `HomeController` 类中，将 `Index` 方法的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="41010-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="41010-150">在 `Index` 方法中右键单击，然后单击 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="41010-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![添加视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="41010-152">选择 "**创建强类型视图**" 选项。</span><span class="sxs-lookup"><span data-stu-id="41010-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="41010-153">对于 "**视图数据类**"，请选择**Mvc3Razor。 UserModel**。</span><span class="sxs-lookup"><span data-stu-id="41010-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="41010-154">（如果在 "**查看数据类**" 框中看不到**Mvc3Razor** ，则需要生成项目。）请确保 "视图引擎" 设置为 " **Razor**"。</span><span class="sxs-lookup"><span data-stu-id="41010-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="41010-155">将 "**查看内容**" 设置为 "**列表**"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="41010-155">Set **View content** to **List** and then click **Add**.</span></span>

![添加索引视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="41010-157">新视图将自动基架传递到 `Index` 视图的用户数据。</span><span class="sxs-lookup"><span data-stu-id="41010-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="41010-158">检查新生成的*Views\Home\Index*文件。</span><span class="sxs-lookup"><span data-stu-id="41010-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="41010-159">"**新建**"、"**编辑**"、"**详细信息**" 和 "**删除**" 链接不起作用，但页面的其余部分都正常工作。</span><span class="sxs-lookup"><span data-stu-id="41010-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="41010-160">运行页面。</span><span class="sxs-lookup"><span data-stu-id="41010-160">Run the page.</span></span> <span data-ttu-id="41010-161">你将看到用户列表。</span><span class="sxs-lookup"><span data-stu-id="41010-161">You see a list of users.</span></span>

![索引页](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="41010-163">打开*索引.* # 文件，并将 "**编辑**"、"**详细信息**" 和 "**删除**" `ActionLink` 标记替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="41010-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="41010-164">用户名用作 ID，以在 "**编辑**"、"**详细信息**" 和 "**删除**" 链接中查找所选记录。</span><span class="sxs-lookup"><span data-stu-id="41010-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="41010-165">创建详细信息视图</span><span class="sxs-lookup"><span data-stu-id="41010-165">Creating the Details View</span></span>

<span data-ttu-id="41010-166">下一步是添加 `Details` 操作方法和视图，以便显示用户详细信息。</span><span class="sxs-lookup"><span data-stu-id="41010-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="41010-168">将以下 `Details` 方法添加到 home 控制器：</span><span class="sxs-lookup"><span data-stu-id="41010-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="41010-169">在 `Details` 方法中右键单击，然后选择 "<strong>添加视图</strong>"。</span><span class="sxs-lookup"><span data-stu-id="41010-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="41010-170">验证 "<strong>查看数据类</strong>" 框是否包含<strong>Mvc3Razor。 UserModel</strong><em>。</em></span><span class="sxs-lookup"><span data-stu-id="41010-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="41010-171">将 "<strong>查看内容</strong>" 设置为<strong>详细信息</strong>，然后单击 "<strong>添加</strong>"。</span><span class="sxs-lookup"><span data-stu-id="41010-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![添加详细信息视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="41010-173">运行应用程序并选择 "详细信息" 链接。</span><span class="sxs-lookup"><span data-stu-id="41010-173">Run the application and select a details link.</span></span> <span data-ttu-id="41010-174">自动基架显示模型中的每个属性。</span><span class="sxs-lookup"><span data-stu-id="41010-174">The automatic scaffolding shows each property in the model.</span></span>

![详细信息](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="41010-176">创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="41010-176">Creating the Edit View</span></span>

<span data-ttu-id="41010-177">将以下 `Edit` 方法添加到 home 控制器。</span><span class="sxs-lookup"><span data-stu-id="41010-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="41010-178">按照前面的步骤添加视图，但将 "**查看内容**" 设置为 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="41010-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![添加编辑视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="41010-180">运行应用程序，并编辑一个用户的名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="41010-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="41010-181">如果违反了已应用于 `UserModel` 类的任何 `DataAnnotation` 约束，则在提交窗体时，将会看到由服务器代码生成的验证错误。</span><span class="sxs-lookup"><span data-stu-id="41010-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="41010-182">例如，如果将王&quot; &quot;的名字改为 &quot;&quot;，则在提交窗体时，窗体上将显示以下错误：</span><span class="sxs-lookup"><span data-stu-id="41010-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="41010-183">在本教程中，你要将用户名视为主键。</span><span class="sxs-lookup"><span data-stu-id="41010-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="41010-184">因此，不能更改 "用户名" 属性。</span><span class="sxs-lookup"><span data-stu-id="41010-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="41010-185">在*编辑*`Html.BeginForm` 语句后，将用户名设置为隐藏的字段。</span><span class="sxs-lookup"><span data-stu-id="41010-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="41010-186">这将导致在模型中传递属性。</span><span class="sxs-lookup"><span data-stu-id="41010-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="41010-187">以下代码段显示了 `Hidden` 语句的位置：</span><span class="sxs-lookup"><span data-stu-id="41010-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="41010-188">使用 `DisplayFor` 调用替换用户名的 `TextBoxFor` 和 `ValidationMessageFor` 标记。</span><span class="sxs-lookup"><span data-stu-id="41010-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="41010-189">`DisplayFor` 方法将属性显示为只读元素。</span><span class="sxs-lookup"><span data-stu-id="41010-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="41010-190">下面的示例演示了完整标记。</span><span class="sxs-lookup"><span data-stu-id="41010-190">The following example shows the completed markup.</span></span> <span data-ttu-id="41010-191">原始 `TextBoxFor` 和 `ValidationMessageFor` 调用被注释掉 Razor 开始注释和结束注释字符（`@* *@`）</span><span class="sxs-lookup"><span data-stu-id="41010-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="41010-192">启用客户端验证</span><span class="sxs-lookup"><span data-stu-id="41010-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="41010-193">若要在 ASP.NET MVC 3 中启用客户端验证，必须设置两个标志，并且必须包含三个 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="41010-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="41010-194">打开应用程序的*web.config 文件。*</span><span class="sxs-lookup"><span data-stu-id="41010-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="41010-195">在应用程序设置中验证 `that ClientValidationEnabled` 和 `UnobtrusiveJavaScriptEnabled` 是否设置为 true。</span><span class="sxs-lookup"><span data-stu-id="41010-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="41010-196">*根 web.config*文件中的以下片段显示了正确的设置：</span><span class="sxs-lookup"><span data-stu-id="41010-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="41010-197">将 `UnobtrusiveJavaScriptEnabled` 设置为 true 可启用非引人注目的 Ajax 和不引人注目的客户端验证。</span><span class="sxs-lookup"><span data-stu-id="41010-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="41010-198">使用非介入式验证时，验证规则将被转换为 HTML5 属性。</span><span class="sxs-lookup"><span data-stu-id="41010-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="41010-199">HTML5 属性名称只能包含小写字母、数字和短划线。</span><span class="sxs-lookup"><span data-stu-id="41010-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="41010-200">将 `ClientValidationEnabled` 设置为 true 可启用客户端验证。</span><span class="sxs-lookup"><span data-stu-id="41010-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="41010-201">通过在应用程序的 web.config 文件中设置这些密钥，可为整个*应用程序启用*客户端验证和非引人注目的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="41010-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="41010-202">你还可以使用以下代码在各个视图或控制器方法中启用或禁用这些设置：</span><span class="sxs-lookup"><span data-stu-id="41010-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="41010-203">还需要在呈现的视图中包含多个 JavaScript 文件。</span><span class="sxs-lookup"><span data-stu-id="41010-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="41010-204">在所有视图中包含 JavaScript 的简单方法是将其添加到*Views\Shared\\_Layout cshtml*文件中。</span><span class="sxs-lookup"><span data-stu-id="41010-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="41010-205">用以下代码替换 *\_布局*的 `<head>` 元素：</span><span class="sxs-lookup"><span data-stu-id="41010-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="41010-206">前两个 jQuery 脚本由 Microsoft Ajax 内容交付网络（CDN）承载。</span><span class="sxs-lookup"><span data-stu-id="41010-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="41010-207">利用 Microsoft Ajax CDN，可以显著提高应用程序的第一次命中率。</span><span class="sxs-lookup"><span data-stu-id="41010-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="41010-208">运行应用程序，并单击 "编辑" 链接。</span><span class="sxs-lookup"><span data-stu-id="41010-208">Run the application and click an edit link.</span></span> <span data-ttu-id="41010-209">在浏览器中查看该页的源。</span><span class="sxs-lookup"><span data-stu-id="41010-209">View the page's source in the browser.</span></span> <span data-ttu-id="41010-210">Browser source 显示了 `data-val` 格式（用于数据验证）的许多属性。</span><span class="sxs-lookup"><span data-stu-id="41010-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="41010-211">如果启用了客户端验证和非介入式 JavaScript，则具有客户端验证规则的输入字段将包含 `data-val="true"` 特性来触发非引人注目的客户端验证。</span><span class="sxs-lookup"><span data-stu-id="41010-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="41010-212">例如，模型中的 "`City`" 字段是用[Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)属性修饰的，这将生成以下示例中所示的 HTML：</span><span class="sxs-lookup"><span data-stu-id="41010-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="41010-213">对于每个客户端验证规则，会添加格式 `data-val-rulename="message"`的属性。</span><span class="sxs-lookup"><span data-stu-id="41010-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="41010-214">使用前面所示的 `City` 字段示例，必需的客户端验证规则生成 `data-val-required` 属性，&quot;City 字段&quot;消息。</span><span class="sxs-lookup"><span data-stu-id="41010-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="41010-215">运行应用程序，编辑用户之一，然后清除 "`City`" 字段。</span><span class="sxs-lookup"><span data-stu-id="41010-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="41010-216">当您通过 tab 键跳出字段时，您会看到客户端验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="41010-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![需要城市](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="41010-218">同样，对于客户端验证规则中的每个参数，都会添加格式 `data-val-rulename-paramname=paramvalue`的属性。</span><span class="sxs-lookup"><span data-stu-id="41010-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="41010-219">例如，`FirstName` 属性使用[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性进行批注，并指定最小长度为3且最大长度为8。</span><span class="sxs-lookup"><span data-stu-id="41010-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="41010-220">名为 `length` 的数据验证规则的参数名称 `max` 和参数值8。</span><span class="sxs-lookup"><span data-stu-id="41010-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="41010-221">下面显示了在编辑用户之一时为 "`FirstName`" 字段生成的 HTML：</span><span class="sxs-lookup"><span data-stu-id="41010-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="41010-222">有关非介入式客户端验证的详细信息，请参阅 Brad Wilson 博客中的[ASP.NET MVC 3 中的条目不引人注目的客户端验证](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)。</span><span class="sxs-lookup"><span data-stu-id="41010-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="41010-223">在 ASP.NET MVC 3 Beta 中，有时需要提交窗体以便启动客户端验证。</span><span class="sxs-lookup"><span data-stu-id="41010-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="41010-224">对于最终发布，这可能会发生更改。</span><span class="sxs-lookup"><span data-stu-id="41010-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="41010-225">创建 "创建" 视图</span><span class="sxs-lookup"><span data-stu-id="41010-225">Creating the Create View</span></span>

<span data-ttu-id="41010-226">下一步是添加 `Create` 操作方法和视图，以便使用户能够创建新用户。</span><span class="sxs-lookup"><span data-stu-id="41010-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="41010-227">将以下 `Create` 方法添加到 home 控制器：</span><span class="sxs-lookup"><span data-stu-id="41010-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="41010-228">按照前面的步骤添加视图，但将 "**查看内容**" 设置为 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="41010-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![创建视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="41010-230">运行应用程序，选择 "**创建**" 链接，然后添加一个新用户。</span><span class="sxs-lookup"><span data-stu-id="41010-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="41010-231">`Create` 方法自动利用客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="41010-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="41010-232">尝试输入包含空白的用户名，例如 &quot;Ben X&quot;。</span><span class="sxs-lookup"><span data-stu-id="41010-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="41010-233">当您从 "用户名" 字段中按 tab 键时，将显示客户端验证错误（`White space is not allowed`）。</span><span class="sxs-lookup"><span data-stu-id="41010-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="41010-234">添加 Delete 方法</span><span class="sxs-lookup"><span data-stu-id="41010-234">Add the Delete method</span></span>

<span data-ttu-id="41010-235">若要完成本教程，请将以下 `Delete` 方法添加到 home 控制器：</span><span class="sxs-lookup"><span data-stu-id="41010-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="41010-236">如前面的步骤中所示，添加 "`Delete`" 视图，将 "**查看内容**" 设置为 "**删除**"。</span><span class="sxs-lookup"><span data-stu-id="41010-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![删除视图](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="41010-238">现在，你有了一个简单但功能完备的 ASP.NET MVC 3 应用程序，并具有验证。</span><span class="sxs-lookup"><span data-stu-id="41010-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>
