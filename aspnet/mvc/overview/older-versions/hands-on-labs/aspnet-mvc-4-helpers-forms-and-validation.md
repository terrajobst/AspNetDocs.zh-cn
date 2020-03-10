---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 帮助程序，窗体和验证 |Microsoft Docs
author: rick-anderson
description: 在 ASP.NET MVC 4 模型和数据访问动手实验中，你已从数据库加载并显示数据。 在此动手实验中，您将添加到 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433790"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="edaf4-104">ASP.NET MVC 4 帮助程序、窗体和验证</span><span class="sxs-lookup"><span data-stu-id="edaf4-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="edaf4-105">由[Web 训练营团队](https://twitter.com/webcamps)使用</span><span class="sxs-lookup"><span data-stu-id="edaf4-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="edaf4-106">下载 Web 训练营培训工具包</span><span class="sxs-lookup"><span data-stu-id="edaf4-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="edaf4-107">在**ASP.NET MVC 4 模型和数据访问**动手实验中，你已从数据库加载并显示数据。</span><span class="sxs-lookup"><span data-stu-id="edaf4-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="edaf4-108">在此动手实验中，你将向**音乐应用商店**应用程序添加编辑该数据的功能。</span><span class="sxs-lookup"><span data-stu-id="edaf4-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="edaf4-109">考虑到这一目标，您将首先创建一个支持创建、读取、更新和删除（CRUD）影集操作的控制器。</span><span class="sxs-lookup"><span data-stu-id="edaf4-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="edaf4-110">你将生成一个索引视图模板，该模板利用 ASP.NET MVC 的基架功能在 HTML 表中显示唱片集的属性。</span><span class="sxs-lookup"><span data-stu-id="edaf4-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="edaf4-111">若要增强该视图，您将添加一个将截断详细说明的自定义 HTML 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="edaf4-112">之后，您将添加 "编辑" 和 "创建" 视图，以使您能够在数据库中更改影集，并提供类似于下拉列表的窗体元素的帮助。</span><span class="sxs-lookup"><span data-stu-id="edaf4-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="edaf4-113">最后，您将允许用户删除唱片集，同时还会通过验证其输入来阻止他们输入错误的数据。</span><span class="sxs-lookup"><span data-stu-id="edaf4-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="edaf4-114">此动手实验假设你具有**ASP.NET MVC**的基本知识。</span><span class="sxs-lookup"><span data-stu-id="edaf4-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="edaf4-115">如果你之前未使用过**ASP.NET mvc** ，则建议使用**ASP.NET Mvc 基础**动手实验。</span><span class="sxs-lookup"><span data-stu-id="edaf4-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="edaf4-116">此实验室通过应用对源文件夹中提供的示例 Web 应用程序的少量更改，指导你完成前面介绍的增强功能和新功能。</span><span class="sxs-lookup"><span data-stu-id="edaf4-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="edaf4-117">所有示例代码和代码段都包含在 Web 训练营培训工具包中，在[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)中提供。</span><span class="sxs-lookup"><span data-stu-id="edaf4-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="edaf4-118">[ASP.NET MVC 4 帮助程序、窗体和验证中](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)提供了此实验室特定的项目。</span><span class="sxs-lookup"><span data-stu-id="edaf4-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="edaf4-119">目标</span><span class="sxs-lookup"><span data-stu-id="edaf4-119">Objectives</span></span>

<span data-ttu-id="edaf4-120">在此动手实验中，您将学习如何：</span><span class="sxs-lookup"><span data-stu-id="edaf4-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="edaf4-121">创建控制器以支持 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="edaf4-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="edaf4-122">生成索引视图以显示 HTML 表中的实体属性</span><span class="sxs-lookup"><span data-stu-id="edaf4-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="edaf4-123">添加自定义 HTML 帮助程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="edaf4-124">创建和自定义编辑视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="edaf4-125">区分对 HTTP GET 或 HTTP POST 调用做出反应的操作方法</span><span class="sxs-lookup"><span data-stu-id="edaf4-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="edaf4-126">添加和自定义创建视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-126">Add and customize a Create View</span></span>
- <span data-ttu-id="edaf4-127">处理实体的删除</span><span class="sxs-lookup"><span data-stu-id="edaf4-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="edaf4-128">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="edaf4-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="edaf4-129">系统必备</span><span class="sxs-lookup"><span data-stu-id="edaf4-129">Prerequisites</span></span>

<span data-ttu-id="edaf4-130">你必须具有以下项才能完成此实验室：</span><span class="sxs-lookup"><span data-stu-id="edaf4-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="edaf4-131">适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。</span><span class="sxs-lookup"><span data-stu-id="edaf4-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="edaf4-132">安装</span><span class="sxs-lookup"><span data-stu-id="edaf4-132">Setup</span></span>

<span data-ttu-id="edaf4-133">**安装代码片段**</span><span class="sxs-lookup"><span data-stu-id="edaf4-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="edaf4-134">为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。</span><span class="sxs-lookup"><span data-stu-id="edaf4-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="edaf4-135">若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi**文件。</span><span class="sxs-lookup"><span data-stu-id="edaf4-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="edaf4-136">如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本 &quot;文档中的附录[：附录 B：使用代码片段](#AppendixB)&quot;。</span><span class="sxs-lookup"><span data-stu-id="edaf4-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="edaf4-137">练习</span><span class="sxs-lookup"><span data-stu-id="edaf4-137">Exercises</span></span>

<span data-ttu-id="edaf4-138">以下练习构成了此动手实验：</span><span class="sxs-lookup"><span data-stu-id="edaf4-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="edaf4-139">创建存储管理器控制器及其索引视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="edaf4-140">添加 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="edaf4-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="edaf4-141">创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="edaf4-142">添加创建视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="edaf4-143">处理删除</span><span class="sxs-lookup"><span data-stu-id="edaf4-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="edaf4-144">添加验证</span><span class="sxs-lookup"><span data-stu-id="edaf4-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="edaf4-145">在客户端使用非引人注目 jQuery</span><span class="sxs-lookup"><span data-stu-id="edaf4-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="edaf4-146">每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="edaf4-147">如果需要更多帮助，请使用此解决方案作为指导。</span><span class="sxs-lookup"><span data-stu-id="edaf4-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="edaf4-148">完成本实验的估计时间： **60 分钟**</span><span class="sxs-lookup"><span data-stu-id="edaf4-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="edaf4-149">练习1：创建存储管理器控制器及其索引视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="edaf4-150">在此练习中，您将学习如何创建新的控制器以支持 CRUD 操作，自定义其索引操作方法，以从数据库中返回影集列表，并最终生成一个利用 ASP.NET MVC 基架的索引视图模板。用于在 HTML 表中显示影集属性的功能。</span><span class="sxs-lookup"><span data-stu-id="edaf4-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="edaf4-151">任务 1-创建 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="edaf4-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="edaf4-152">在此任务中，你将创建一个名为**StoreManagerController**的新控制器以支持 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="edaf4-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="edaf4-153">打开位于**Source/Ex1-CreatingTheStoreManagerController/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="edaf4-154">在继续之前，需要下载一些缺少的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="edaf4-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="edaf4-155">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="edaf4-156">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="edaf4-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="edaf4-157">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="edaf4-158">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="edaf4-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="edaf4-159">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="edaf4-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="edaf4-160">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="edaf4-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="edaf4-161">添加新控制器。</span><span class="sxs-lookup"><span data-stu-id="edaf4-161">Add a new controller.</span></span> <span data-ttu-id="edaf4-162">为此，请在解决方案资源管理器中右键单击 "**控制器**" 文件夹，选择 "**添加**"，然后选择 "**控制器**" 命令。</span><span class="sxs-lookup"><span data-stu-id="edaf4-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="edaf4-163">将**控制器** **名称**更改为**StoreManagerController** ，并确保选中选项 "**带有空读/写操作的 MVC 控制器**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="edaf4-164">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="edaf4-164">Click **Add**.</span></span>

    <span data-ttu-id="edaf4-165">!["添加控制器" 对话框](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "“添加控制器”对话框")</span><span class="sxs-lookup"><span data-stu-id="edaf4-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="edaf4-166">*"添加控制器" 对话框*</span><span class="sxs-lookup"><span data-stu-id="edaf4-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="edaf4-167">生成新的控制器类。</span><span class="sxs-lookup"><span data-stu-id="edaf4-167">A new Controller class is generated.</span></span> <span data-ttu-id="edaf4-168">由于你指示添加对读/写操作的操作，因此，将在其中填充了 TODO 注释来创建常见的 CRUD 操作，并提示包含应用程序特定的逻辑。</span><span class="sxs-lookup"><span data-stu-id="edaf4-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="edaf4-169">任务 2-自定义 StoreManager 索引</span><span class="sxs-lookup"><span data-stu-id="edaf4-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="edaf4-170">在此任务中，您将自定义 StoreManager Index 操作方法，以从数据库中返回包含唱片集列表的视图。</span><span class="sxs-lookup"><span data-stu-id="edaf4-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="edaf4-171">在 StoreManagerController 类中，添加以下*using*指令。</span><span class="sxs-lookup"><span data-stu-id="edaf4-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="edaf4-172">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-使用 MvcMusicStore 的 Ex1*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="edaf4-173">向**StoreManagerController**添加一个字段，用于保存 MusicStoreEntities 的实例 **。**</span><span class="sxs-lookup"><span data-stu-id="edaf4-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="edaf4-174">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex1 MusicStoreEntities*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="edaf4-175">实现 StoreManagerController 索引操作，以返回包含唱片集列表的视图。</span><span class="sxs-lookup"><span data-stu-id="edaf4-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="edaf4-176">控制器操作逻辑与之前编写的 StoreController 索引操作非常相似。</span><span class="sxs-lookup"><span data-stu-id="edaf4-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="edaf4-177">使用 LINQ 检索所有相册，包括要显示的流派和艺术家信息。</span><span class="sxs-lookup"><span data-stu-id="edaf4-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="edaf4-178">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex1 StoreManagerController Index*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="edaf4-179">任务 3-创建索引视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="edaf4-180">在此任务中，您将创建索引视图模板以显示由**StoreManager**控制器返回的唱片集列表。</span><span class="sxs-lookup"><span data-stu-id="edaf4-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="edaf4-181">在创建新的视图模板之前，您应该生成项目，以便 "**添加视图" 对话框**知道要使用的**唱片集**类。</span><span class="sxs-lookup"><span data-stu-id="edaf4-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="edaf4-182">选择**生成 |生成 MvcMusicStore**以生成项目。</span><span class="sxs-lookup"><span data-stu-id="edaf4-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="edaf4-183">在**索引**操作方法中右键单击，然后选择 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="edaf4-184">此时将显示 "**添加视图**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="edaf4-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="edaf4-185">![添加视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "添加视图")</span><span class="sxs-lookup"><span data-stu-id="edaf4-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="edaf4-186">*从 Index 方法中添加视图*</span><span class="sxs-lookup"><span data-stu-id="edaf4-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="edaf4-187">在 "添加视图" 对话框中，验证视图名称是否为 "**索引**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="edaf4-188">选择 "**创建强类型视图**" 选项，然后从 "**模型类**" 下拉选项中选择 "**唱片集（MvcMusicStore）** "。</span><span class="sxs-lookup"><span data-stu-id="edaf4-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="edaf4-189">从 "**基架模板**" 下拉列表中选择 "**列表**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="edaf4-190">将**视图引擎**保留为**Razor** ，将其他字段保留其默认值，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="edaf4-191">![添加索引视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "添加索引视图")</span><span class="sxs-lookup"><span data-stu-id="edaf4-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="edaf4-192">*添加索引视图*</span><span class="sxs-lookup"><span data-stu-id="edaf4-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="edaf4-193">任务 4-自定义索引视图的基架</span><span class="sxs-lookup"><span data-stu-id="edaf4-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="edaf4-194">在此任务中，您将调整使用 ASP.NET MVC 基架功能创建的简单视图模板，使其显示所需的字段。</span><span class="sxs-lookup"><span data-stu-id="edaf4-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="edaf4-195">ASP.NET MVC 内的**基架**支持会生成一个简单的视图模板，其中列出了唱片集模型中的所有字段。</span><span class="sxs-lookup"><span data-stu-id="edaf4-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="edaf4-196">**基架**提供了开始强类型化视图的快速方法：不必手动编写视图模板，基架会快速生成默认模板，然后可以修改生成的代码。</span><span class="sxs-lookup"><span data-stu-id="edaf4-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>

1. <span data-ttu-id="edaf4-197">查看创建的代码。</span><span class="sxs-lookup"><span data-stu-id="edaf4-197">Review the code created.</span></span> <span data-ttu-id="edaf4-198">生成的字段列表将是**基架**用于显示表格格式数据的以下 HTML 表的一部分。</span><span class="sxs-lookup"><span data-stu-id="edaf4-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="edaf4-199">将 **&lt;表**替换为以下代码&gt;代码，以便仅显示**流派**、**艺术家**、**唱片集标题**和**价格**字段。</span><span class="sxs-lookup"><span data-stu-id="edaf4-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="edaf4-200">这将删除**AlbumId**和**唱片集画面 URL**列。</span><span class="sxs-lookup"><span data-stu-id="edaf4-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="edaf4-201">此外，它会更改 GenreId 和 ArtistId 列，使其显示**Artist.Name**和**Genre.Name**的链接类属性，并删除**详细信息**链接。</span><span class="sxs-lookup"><span data-stu-id="edaf4-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="edaf4-202">更改以下说明。</span><span class="sxs-lookup"><span data-stu-id="edaf4-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="edaf4-203">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="edaf4-204">在此任务中，您将测试 " **StoreManager** **索引**" 视图模板是否根据前面步骤的设计显示唱片集列表。</span><span class="sxs-lookup"><span data-stu-id="edaf4-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="edaf4-205">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-206">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-206">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-207">将 URL 更改为 " **/StoreManager** " 以验证是否显示影集列表，并显示其**标题**、**艺术家**和**流派**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="edaf4-208">![浏览唱片集列表](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "浏览唱片集列表")</span><span class="sxs-lookup"><span data-stu-id="edaf4-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="edaf4-209">*浏览唱片集列表*</span><span class="sxs-lookup"><span data-stu-id="edaf4-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="edaf4-210">练习2：添加 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="edaf4-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="edaf4-211">"StoreManager 索引" 页有一个潜在的问题： "标题" 和 "艺术家名称" 属性的长度可以足以引发表格式设置。</span><span class="sxs-lookup"><span data-stu-id="edaf4-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="edaf4-212">在本练习中，您将学习如何添加自定义 HTML 帮助程序来截断该文本。</span><span class="sxs-lookup"><span data-stu-id="edaf4-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="edaf4-213">在下图中，可以看到，在使用较小浏览器大小时，如何修改格式，因为文本长度太长。</span><span class="sxs-lookup"><span data-stu-id="edaf4-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="edaf4-214">![浏览没有截断文本的唱片集列表](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "浏览没有截断文本的唱片集列表")</span><span class="sxs-lookup"><span data-stu-id="edaf4-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="edaf4-215">*浏览没有截断文本的唱片集列表*</span><span class="sxs-lookup"><span data-stu-id="edaf4-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="edaf4-216">任务 1-扩展 HTML 帮助器</span><span class="sxs-lookup"><span data-stu-id="edaf4-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="edaf4-217">在此任务中，您将添加一个新方法，该方法将**截断**到在 ASP.NET MVC 视图中公开的**HTML**对象。</span><span class="sxs-lookup"><span data-stu-id="edaf4-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="edaf4-218">要执行此操作，需要为 ASP.NET MVC 提供的内置**HtmlHelper**类实现**扩展方法**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="edaf4-219">若要了解有关**扩展方法**的详细信息，请访问此 msdn 文章。</span><span class="sxs-lookup"><span data-stu-id="edaf4-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="edaf4-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="edaf4-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>

1. <span data-ttu-id="edaf4-221">打开位于**Source/buildingappswithcachingservice-ex2-getproducts latency-cs-AddingAnHTMLHelper/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="edaf4-222">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="edaf4-223">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="edaf4-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="edaf4-224">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="edaf4-225">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="edaf4-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="edaf4-226">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="edaf4-227">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="edaf4-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="edaf4-228">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="edaf4-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="edaf4-229">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="edaf4-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="edaf4-230">打开 StoreManager 的 "索引" 视图。</span><span class="sxs-lookup"><span data-stu-id="edaf4-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="edaf4-231">为此，请在 "解决方案资源管理器展开" **Views** "文件夹，然后打开" **StoreManager** "**文件。**</span><span class="sxs-lookup"><span data-stu-id="edaf4-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="edaf4-232">在<strong>@model</strong>指令下面添加以下代码，以定义<strong>截断</strong>helper 方法。</span><span class="sxs-lookup"><span data-stu-id="edaf4-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="edaf4-233">任务 2-截断页面中的文本</span><span class="sxs-lookup"><span data-stu-id="edaf4-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="edaf4-234">在此任务中，您将使用**截断**方法来截断视图模板中的文本。</span><span class="sxs-lookup"><span data-stu-id="edaf4-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="edaf4-235">打开 StoreManager 的 "索引" 视图。</span><span class="sxs-lookup"><span data-stu-id="edaf4-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="edaf4-236">为此，请在 "解决方案资源管理器展开" **Views** "文件夹，然后打开" **StoreManager** "**文件。**</span><span class="sxs-lookup"><span data-stu-id="edaf4-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="edaf4-237">替换显示**艺术家名称**和唱片集**标题**的行。</span><span class="sxs-lookup"><span data-stu-id="edaf4-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="edaf4-238">为此，请替换以下行。</span><span class="sxs-lookup"><span data-stu-id="edaf4-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="edaf4-239">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="edaf4-240">在此任务中，你将测试**StoreManager** **索引**视图模板是否截断了唱片集的标题和名称。</span><span class="sxs-lookup"><span data-stu-id="edaf4-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="edaf4-241">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-242">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-242">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-243">将 URL 更改为 " **/StoreManager** " 以验证 "**标题**" 和 "**艺术家**" 列中的长文本是否已截断。</span><span class="sxs-lookup"><span data-stu-id="edaf4-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="edaf4-244">![截断的标题和艺术家名称](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "截断的标题和艺术家名称")</span><span class="sxs-lookup"><span data-stu-id="edaf4-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="edaf4-245">*截断的标题和艺术家姓名*</span><span class="sxs-lookup"><span data-stu-id="edaf4-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="edaf4-246">练习3：创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="edaf4-247">在此练习中，您将学习如何创建窗体，以允许商店经理编辑唱片集。</span><span class="sxs-lookup"><span data-stu-id="edaf4-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="edaf4-248">他们将浏览 **/StoreManager/Edit/id** URL （**id**是要编辑的唱片集的唯一 id），从而对服务器发出 HTTP GET 调用。</span><span class="sxs-lookup"><span data-stu-id="edaf4-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="edaf4-249">控制器编辑操作方法将从数据库中检索相应的唱片集，创建**StoreManagerViewModel**对象以封装它（连同艺术家和流派的列表），然后将其传递给视图模板，以将 HTML 页面呈现给用户。</span><span class="sxs-lookup"><span data-stu-id="edaf4-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="edaf4-250">此页将包含一个 **&lt;窗体&gt;** 元素，其中包含用于编辑唱片集属性的文本框和下拉列表。</span><span class="sxs-lookup"><span data-stu-id="edaf4-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="edaf4-251">用户更新唱片集格式值并单击 "**保存**" 按钮后，将通过 HTTP POST 调用将更改提交回 **/StoreManager/Edit/id**。尽管 URL 与上一次调用中的内容相同，但 ASP.NET MVC 标识这是一个 HTTP POST，因此执行其他编辑操作方法（一个修饰使用 **[HttpPost]** ）。</span><span class="sxs-lookup"><span data-stu-id="edaf4-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="edaf4-252">任务 1-实现 HTTP-获取编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="edaf4-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="edaf4-253">在此任务中，您将实现 "编辑操作" 方法的 HTTP 获取版本以从数据库中检索相应的唱片集，以及所有流派和艺术家的列表。</span><span class="sxs-lookup"><span data-stu-id="edaf4-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="edaf4-254">它会将此数据打包到上一步骤中定义的**StoreManagerViewModel**对象中，然后将该对象传递给视图模板以呈现响应。</span><span class="sxs-lookup"><span data-stu-id="edaf4-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="edaf4-255">打开位于**Source/section-cs-CreatingTheEditView/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="edaf4-256">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="edaf4-257">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="edaf4-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="edaf4-258">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="edaf4-259">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="edaf4-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="edaf4-260">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="edaf4-261">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="edaf4-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="edaf4-262">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="edaf4-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="edaf4-263">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="edaf4-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="edaf4-264">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="edaf4-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="edaf4-265">为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="edaf4-266">将**HTTP-GET 编辑**操作方法替换为以下代码，以检索相应的**唱片集**以及**流派**和**艺术家**列表。</span><span class="sxs-lookup"><span data-stu-id="edaf4-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="edaf4-267">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Section-cs STOREMANAGERCONTROLLER HTTP-获取编辑操作*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="edaf4-268">正在为艺术家和**流派使用** **SelectList** ，而不是对**system.object**列表使用。</span><span class="sxs-lookup"><span data-stu-id="edaf4-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="edaf4-269">**SelectList**是一种用于填充 HTML 下拉列表并管理当前所选内容的更干净的方式。</span><span class="sxs-lookup"><span data-stu-id="edaf4-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="edaf4-270">实例化并稍后在控制器操作中设置这些 ViewModel 对象将使编辑窗体方案更整洁。</span><span class="sxs-lookup"><span data-stu-id="edaf4-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="edaf4-271">任务 2-创建编辑视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="edaf4-272">在此任务中，您将创建一个稍后将显示唱片集属性的编辑视图模板。</span><span class="sxs-lookup"><span data-stu-id="edaf4-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="edaf4-273">创建 "编辑" 视图。</span><span class="sxs-lookup"><span data-stu-id="edaf4-273">Create the Edit View.</span></span> <span data-ttu-id="edaf4-274">为此，请在**编辑**操作方法内右键单击，然后选择 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="edaf4-275">在 "添加视图" 对话框中，验证视图名称是否为 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="edaf4-276">选中 "**创建强类型视图**" 复选框，然后从 "**查看数据类**" 下拉框中选择 "**唱片集（MvcMusicStore）** "。</span><span class="sxs-lookup"><span data-stu-id="edaf4-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="edaf4-277">从 "**基架模板**" 下拉选择 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="edaf4-278">让其他字段保留其默认值，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="edaf4-279">![添加编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "添加编辑视图")</span><span class="sxs-lookup"><span data-stu-id="edaf4-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="edaf4-280">*添加编辑视图*</span><span class="sxs-lookup"><span data-stu-id="edaf4-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="edaf4-281">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="edaf4-282">在此任务中，您将测试**StoreManager**的 "**编辑**视图" 页是否显示作为参数传递的唱片集的属性值。</span><span class="sxs-lookup"><span data-stu-id="edaf4-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="edaf4-283">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-284">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-284">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-285">将 URL 更改为 " **/StoreManager/Edit/1** " 以验证是否显示了所传递的唱片集的属性值。</span><span class="sxs-lookup"><span data-stu-id="edaf4-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="edaf4-286">![浏览唱片集的编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "浏览唱片集的编辑视图")</span><span class="sxs-lookup"><span data-stu-id="edaf4-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="edaf4-287">*浏览唱片集的编辑视图*</span><span class="sxs-lookup"><span data-stu-id="edaf4-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="edaf4-288">任务 4-在唱片集编辑器模板上实现下拉</span><span class="sxs-lookup"><span data-stu-id="edaf4-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="edaf4-289">在此任务中，您将向在上一个任务中创建的视图模板添加下拉列表，以便用户可以从艺术家和流派列表中进行选择。</span><span class="sxs-lookup"><span data-stu-id="edaf4-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="edaf4-290">将所有**唱**集字段代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="edaf4-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="edaf4-291">已将**DropDownList** helper 添加到用于选择艺术家和流派的渲染下拉。</span><span class="sxs-lookup"><span data-stu-id="edaf4-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="edaf4-292">传递给**DropDownList**的参数是：</span><span class="sxs-lookup"><span data-stu-id="edaf4-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="edaf4-293">窗体字段的名称（ **&quot;ArtistId&quot;** ）。</span><span class="sxs-lookup"><span data-stu-id="edaf4-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="edaf4-294">下拉的值的**SelectList** 。</span><span class="sxs-lookup"><span data-stu-id="edaf4-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="edaf4-295">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="edaf4-296">在此任务中，您将测试**StoreManager**的 "**编辑**视图" 页是否显示下拉下拉标识符而不是艺术家和流派 ID 文本字段。</span><span class="sxs-lookup"><span data-stu-id="edaf4-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="edaf4-297">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-298">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-298">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-299">将 URL 更改为 " **/StoreManager/Edit/1** " 以验证它是否显示下拉项，而不是 "艺术家" 和 "流派 ID" 文本字段。</span><span class="sxs-lookup"><span data-stu-id="edaf4-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="edaf4-300">![浏览唱片集的编辑视图和下拉](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "浏览唱片集的编辑视图和下拉")</span><span class="sxs-lookup"><span data-stu-id="edaf4-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="edaf4-301">*浏览唱片集的编辑视图，这一次带 dropdown*</span><span class="sxs-lookup"><span data-stu-id="edaf4-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="edaf4-302">任务 6-实现 HTTP POST 编辑操作方法</span><span class="sxs-lookup"><span data-stu-id="edaf4-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="edaf4-303">编辑视图按预期显示后，需要实现 HTTP POST 编辑操作方法以保存对唱片集所做的更改。</span><span class="sxs-lookup"><span data-stu-id="edaf4-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="edaf4-304">如果需要，请关闭浏览器以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="edaf4-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="edaf4-305">从 "**控制器**" 文件夹中打开**StoreManagerController** 。</span><span class="sxs-lookup"><span data-stu-id="edaf4-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="edaf4-306">将**HTTP-POST 编辑**操作方法代码替换为以下代码（请注意，必须替换的方法是接收两个参数的重载版本）：</span><span class="sxs-lookup"><span data-stu-id="edaf4-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="edaf4-307">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Section-cs STOREMANAGERCONTROLLER HTTP-POST 编辑操作*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="edaf4-308">此方法将在用户单击视图的 "**保存**" 按钮时执行，并将窗体值的 HTTP POST 返回给服务器，以将其保留在数据库中。</span><span class="sxs-lookup"><span data-stu-id="edaf4-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="edaf4-309">修饰器 **[HttpPost]** 指示该方法应该用于这些 HTTP POST 方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="edaf4-310">方法使用**唱片集**对象。</span><span class="sxs-lookup"><span data-stu-id="edaf4-310">The method takes an **Album** object.</span></span> <span data-ttu-id="edaf4-311">ASP.NET MVC 将自动从发布 &lt;窗体&gt; 值创建唱片集对象。</span><span class="sxs-lookup"><span data-stu-id="edaf4-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="edaf4-312">方法将执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="edaf4-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="edaf4-313">如果模型有效：</span><span class="sxs-lookup"><span data-stu-id="edaf4-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="edaf4-314">更新上下文中的 "唱片集" 条目，以将其标记为已修改对象。</span><span class="sxs-lookup"><span data-stu-id="edaf4-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="edaf4-315">保存更改并重定向到索引视图。</span><span class="sxs-lookup"><span data-stu-id="edaf4-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="edaf4-316">如果该模型无效，它将用**GenreId**和**ArtistId**填充 ViewBag，然后它将返回包含已接收唱片集对象的视图，以允许用户执行任何所需的更新。</span><span class="sxs-lookup"><span data-stu-id="edaf4-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="edaf4-317">任务 7-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="edaf4-318">在此任务中，您将测试 StoreManager 的 "**编辑**视图" 页是否确实将更新后的唱片集数据保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="edaf4-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="edaf4-319">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-320">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-320">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-321">将 URL 更改为 **/StoreManager/Edit/1**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="edaf4-322">更改要**加载**的唱片集标题，并单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="edaf4-323">验证影集列表中的唱片集标题是否实际已更改。</span><span class="sxs-lookup"><span data-stu-id="edaf4-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="edaf4-324">![更新唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "更新唱片集")</span><span class="sxs-lookup"><span data-stu-id="edaf4-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="edaf4-325">*更新唱片集*</span><span class="sxs-lookup"><span data-stu-id="edaf4-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="edaf4-326">练习4：添加 "创建" 视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="edaf4-327">既然**StoreManagerController**支持**编辑**功能，在此练习中，您将学习如何添加 "创建视图" 模板，以允许商店管理器向应用程序中添加新的唱片集。</span><span class="sxs-lookup"><span data-stu-id="edaf4-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="edaf4-328">与编辑功能一样，你将在**StoreManagerController**类中使用两个不同的方法来实现 Create 方案：</span><span class="sxs-lookup"><span data-stu-id="edaf4-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="edaf4-329">当存储经理首次访问 **/StoreManager/Create** URL 时，一个操作方法将显示一个空窗体。</span><span class="sxs-lookup"><span data-stu-id="edaf4-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="edaf4-330">第二个操作方法将处理方案，其中存储管理器在窗体中单击 "**保存**" 按钮，然后将值作为 HTTP POST 提交回 **/StoreManager/Create** URL。</span><span class="sxs-lookup"><span data-stu-id="edaf4-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="edaf4-331">任务 1-实现 HTTP 获取创建操作方法</span><span class="sxs-lookup"><span data-stu-id="edaf4-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="edaf4-332">在此任务中，您将实现 "创建操作" 方法的 HTTP GET 版本来检索所有流派和音乐家的列表，将此数据打包到**StoreManagerViewModel**对象，然后将该对象传递给视图模板。</span><span class="sxs-lookup"><span data-stu-id="edaf4-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="edaf4-333">打开位于**Source/Ex4-AddingACreateView/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="edaf4-334">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="edaf4-335">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="edaf4-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="edaf4-336">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="edaf4-337">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="edaf4-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="edaf4-338">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="edaf4-339">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="edaf4-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="edaf4-340">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="edaf4-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="edaf4-341">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="edaf4-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="edaf4-342">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="edaf4-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="edaf4-343">为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="edaf4-344">将**创建**操作方法代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="edaf4-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="edaf4-345">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex4 STOREMANAGERCONTROLLER HTTP-GET Create action*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="edaf4-346">任务 2-添加 "创建" 视图</span><span class="sxs-lookup"><span data-stu-id="edaf4-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="edaf4-347">在此任务中，您将添加 "创建视图" 模板，该模板将显示新的（空）唱集窗体。</span><span class="sxs-lookup"><span data-stu-id="edaf4-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="edaf4-348">在**创建**操作方法中右键单击，然后选择 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="edaf4-349">此时将显示 "添加视图" 对话框。</span><span class="sxs-lookup"><span data-stu-id="edaf4-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="edaf4-350">在 "添加视图" 对话框中，验证视图名称是否为 "**创建**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="edaf4-351">选择 "**创建强类型视图**" 选项，然后从 "**模型类**" 下拉项中选择 "**唱片集（MvcMusicStore）** "，**并从 "** **基架模板**" 下拉。</span><span class="sxs-lookup"><span data-stu-id="edaf4-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="edaf4-352">让其他字段保留其默认值，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="edaf4-353">![添加创建视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view .png")</span><span class="sxs-lookup"><span data-stu-id="edaf4-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="edaf4-354">*添加 "创建" 视图*</span><span class="sxs-lookup"><span data-stu-id="edaf4-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="edaf4-355">更新 " **GenreId** " 和 " **ArtistId** " 字段，以使用如下所示的下拉列表：</span><span class="sxs-lookup"><span data-stu-id="edaf4-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="edaf4-356">任务 3-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="edaf4-357">在此任务中，您将测试**StoreManager** **创建**视图页是否显示空的唱片集窗体。</span><span class="sxs-lookup"><span data-stu-id="edaf4-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="edaf4-358">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-359">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-359">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-360">将 URL 更改为 **/StoreManager/Create**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="edaf4-361">验证是否显示了一个空窗体，用于填充新的唱片集属性。</span><span class="sxs-lookup"><span data-stu-id="edaf4-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="edaf4-362">![使用空窗体创建视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "使用空窗体创建视图")</span><span class="sxs-lookup"><span data-stu-id="edaf4-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="edaf4-363">*使用空窗体创建视图*</span><span class="sxs-lookup"><span data-stu-id="edaf4-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="edaf4-364">任务 4-实现 HTTP POST 创建操作方法</span><span class="sxs-lookup"><span data-stu-id="edaf4-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="edaf4-365">在此任务中，你将实现创建操作方法的 HTTP POST 版本，该方法将在用户单击 "**保存**" 按钮时调用。</span><span class="sxs-lookup"><span data-stu-id="edaf4-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="edaf4-366">方法应将新的唱片集保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="edaf4-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="edaf4-367">如果需要，请关闭浏览器以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="edaf4-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="edaf4-368">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="edaf4-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="edaf4-369">为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="edaf4-370">将**HTTP POST 创建**操作方法代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="edaf4-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="edaf4-371">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex4 STOREMANAGERCONTROLLER HTTP-POST 创建操作*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="edaf4-372">"创建" 操作非常类似于上一编辑操作方法，而是将对象添加到上下文中，而不是将其设置为 "已修改"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="edaf4-373">任务 5-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="edaf4-374">在此任务中，您将测试**StoreManager 创建**视图页是否允许您创建一个新的唱片集，然后重定向到 StoreManager 索引视图。</span><span class="sxs-lookup"><span data-stu-id="edaf4-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="edaf4-375">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-376">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-376">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-377">将 URL 更改为 **/StoreManager/Create**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="edaf4-378">使用新唱片集的数据填充所有窗体字段，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="edaf4-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="edaf4-379">![创建唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "创建唱片集")</span><span class="sxs-lookup"><span data-stu-id="edaf4-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="edaf4-380">*创建唱片集*</span><span class="sxs-lookup"><span data-stu-id="edaf4-380">*Creating an Album*</span></span>
3. <span data-ttu-id="edaf4-381">验证是否已重定向到包含刚刚创建的新唱片集的 StoreManager 索引视图。</span><span class="sxs-lookup"><span data-stu-id="edaf4-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="edaf4-382">![已创建新唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "已创建新唱片集")</span><span class="sxs-lookup"><span data-stu-id="edaf4-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="edaf4-383">*已创建新唱片集*</span><span class="sxs-lookup"><span data-stu-id="edaf4-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="edaf4-384">练习5：处理删除</span><span class="sxs-lookup"><span data-stu-id="edaf4-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="edaf4-385">尚未实现删除唱片集的功能。</span><span class="sxs-lookup"><span data-stu-id="edaf4-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="edaf4-386">本练习将介绍这一点。</span><span class="sxs-lookup"><span data-stu-id="edaf4-386">This is what this exercise will be about.</span></span> <span data-ttu-id="edaf4-387">与之前一样，你将使用**StoreManagerController**类中的两个单独方法实现删除方案：</span><span class="sxs-lookup"><span data-stu-id="edaf4-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="edaf4-388">一个操作方法将显示确认窗体</span><span class="sxs-lookup"><span data-stu-id="edaf4-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="edaf4-389">第二个操作方法将处理窗体提交</span><span class="sxs-lookup"><span data-stu-id="edaf4-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="edaf4-390">任务 1-实现 HTTP-GET Delete 操作方法</span><span class="sxs-lookup"><span data-stu-id="edaf4-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="edaf4-391">在此任务中，您将实现 "删除操作" 方法的 HTTP 获取版本以检索唱片集的信息。</span><span class="sxs-lookup"><span data-stu-id="edaf4-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="edaf4-392">打开位于**Source/Ex5-HandlingDeletion/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="edaf4-393">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="edaf4-394">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="edaf4-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="edaf4-395">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="edaf4-396">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="edaf4-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="edaf4-397">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="edaf4-398">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="edaf4-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="edaf4-399">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="edaf4-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="edaf4-400">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="edaf4-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="edaf4-401">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="edaf4-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="edaf4-402">为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="edaf4-403">删除控制器操作与上一存储详细信息控制器操作完全相同：它使用 URL 中提供的**id**从数据库中查询**唱片集**对象，并返回相应的**视图**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="edaf4-404">为此，请将 HTTP-GET**删除**操作方法代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="edaf4-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="edaf4-405">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex5 处理删除 HTTP-GET 删除操作*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="edaf4-406">右键单击 "**删除**" 操作方法，然后选择 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="edaf4-407">此时将显示 "添加视图" 对话框。</span><span class="sxs-lookup"><span data-stu-id="edaf4-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="edaf4-408">在 "添加视图" 对话框中，验证视图名称是否为 "**删除**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="edaf4-409">选择 "**创建强类型视图**" 选项，然后从 "**模型类**" 下拉选项中选择 "**唱片集（MvcMusicStore）** "。</span><span class="sxs-lookup"><span data-stu-id="edaf4-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="edaf4-410">从 "基架"**模板**下拉选择 "**删除**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="edaf4-411">让其他字段保留其默认值，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="edaf4-412">![添加删除视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "添加删除视图")</span><span class="sxs-lookup"><span data-stu-id="edaf4-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="edaf4-413">*添加删除视图*</span><span class="sxs-lookup"><span data-stu-id="edaf4-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="edaf4-414">"删除" 模板显示模型中的所有字段。</span><span class="sxs-lookup"><span data-stu-id="edaf4-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="edaf4-415">您将只显示唱片集的标题。</span><span class="sxs-lookup"><span data-stu-id="edaf4-415">You will show only the album's title.</span></span> <span data-ttu-id="edaf4-416">为此，请将视图的内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="edaf4-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="edaf4-417">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="edaf4-418">在此任务中，您将测试**StoreManager** **删除**视图页是否显示确认删除窗体。</span><span class="sxs-lookup"><span data-stu-id="edaf4-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="edaf4-419">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-420">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-420">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-421">将 URL 更改为 **/StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="edaf4-422">单击 "**删除**" 以选择要删除的一个唱片集，并验证新视图是否已上传。</span><span class="sxs-lookup"><span data-stu-id="edaf4-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="edaf4-423">![删除唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "删除唱片集")</span><span class="sxs-lookup"><span data-stu-id="edaf4-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="edaf4-424">*删除唱片集*</span><span class="sxs-lookup"><span data-stu-id="edaf4-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="edaf4-425">任务 3-实现 HTTP POST 删除操作方法</span><span class="sxs-lookup"><span data-stu-id="edaf4-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="edaf4-426">在此任务中，您将实现删除操作方法的 HTTP POST 版本，当用户单击 "**删除**" 按钮时，将调用该方法。</span><span class="sxs-lookup"><span data-stu-id="edaf4-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="edaf4-427">方法应删除数据库中的唱片集。</span><span class="sxs-lookup"><span data-stu-id="edaf4-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="edaf4-428">如果需要，请关闭浏览器以返回到 Visual Studio 窗口。</span><span class="sxs-lookup"><span data-stu-id="edaf4-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="edaf4-429">打开**StoreManagerController**类。</span><span class="sxs-lookup"><span data-stu-id="edaf4-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="edaf4-430">为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="edaf4-431">将**HTTP POST 删除**操作方法代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="edaf4-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="edaf4-432">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex5 处理删除 HTTP-POST 删除操作*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="edaf4-433">任务 4-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="edaf4-434">在此任务中，您将测试 StoreManager 的 "**删除**视图" 页是否允许您删除唱片集，然后重定向到 StoreManager 索引视图。</span><span class="sxs-lookup"><span data-stu-id="edaf4-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="edaf4-435">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-436">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-436">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-437">将 URL 更改为 **/StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="edaf4-438">单击 "删除"，选择要删除的一个唱片集 **。**</span><span class="sxs-lookup"><span data-stu-id="edaf4-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="edaf4-439">单击 "**删除**" 按钮确认删除：</span><span class="sxs-lookup"><span data-stu-id="edaf4-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="edaf4-440">![删除唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "删除唱片集")</span><span class="sxs-lookup"><span data-stu-id="edaf4-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="edaf4-441">*删除唱片集*</span><span class="sxs-lookup"><span data-stu-id="edaf4-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="edaf4-442">验证是否已删除该唱片集，因为它未出现在 "**索引**" 页中。</span><span class="sxs-lookup"><span data-stu-id="edaf4-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="edaf4-443">练习6：添加验证</span><span class="sxs-lookup"><span data-stu-id="edaf4-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="edaf4-444">目前，所用的创建和编辑表单不执行任何类型的验证。</span><span class="sxs-lookup"><span data-stu-id="edaf4-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="edaf4-445">如果用户将必填字段留空，或在 "价格" 字段中键入字母，则将从数据库中获取第一个错误。</span><span class="sxs-lookup"><span data-stu-id="edaf4-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="edaf4-446">可以通过将数据批注添加到模型类来向应用程序添加验证。</span><span class="sxs-lookup"><span data-stu-id="edaf4-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="edaf4-447">数据批注允许描述要应用于模型属性的规则，ASP.NET MVC 将负责强制执行并向用户显示相应的消息。</span><span class="sxs-lookup"><span data-stu-id="edaf4-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="edaf4-448">任务 1-添加数据批注</span><span class="sxs-lookup"><span data-stu-id="edaf4-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="edaf4-449">在此任务中，您将向唱片集添加数据批注，使 "创建" 和 "编辑" 页在适当的时候显示验证消息。</span><span class="sxs-lookup"><span data-stu-id="edaf4-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="edaf4-450">对于简单模型类，只需添加**system.componentmodel. DataAnnotation**的**using**语句，然后将 **[必需]** 特性置于适当的属性上即可处理添加数据批注。</span><span class="sxs-lookup"><span data-stu-id="edaf4-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="edaf4-451">下面的示例将**Name**属性设置为视图中的必填字段。</span><span class="sxs-lookup"><span data-stu-id="edaf4-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="edaf4-452">在此应用程序中生成实体数据模型的情况下，这种情况稍微复杂一些。</span><span class="sxs-lookup"><span data-stu-id="edaf4-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="edaf4-453">如果您将数据批注直接添加到模型类，则当您从数据库更新模型时，将覆盖这些注释。</span><span class="sxs-lookup"><span data-stu-id="edaf4-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="edaf4-454">相反，您可以使用元数据分部类，这些类将存在来保存批注，并使用 **[MetadataType]** 特性与模型类关联。</span><span class="sxs-lookup"><span data-stu-id="edaf4-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="edaf4-455">打开位于**Source/Ex6-AddingValidation/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="edaf4-456">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="edaf4-457">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="edaf4-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="edaf4-458">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="edaf4-459">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="edaf4-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="edaf4-460">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="edaf4-461">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="edaf4-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="edaf4-462">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="edaf4-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="edaf4-463">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="edaf4-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="edaf4-464">从 "**模型**" 文件夹打开 " **Album.cs** "。</span><span class="sxs-lookup"><span data-stu-id="edaf4-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="edaf4-465">将**Album.cs**的内容替换为突出显示的代码，使其类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="edaf4-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="edaf4-466">行 **[DisplayFormat （ConvertEmptyStringToNull = false）]** 指示在数据源中更新数据字段时，模型中的空字符串不会转换为 null。</span><span class="sxs-lookup"><span data-stu-id="edaf4-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="edaf4-467">当实体框架在数据批注验证字段之前将 null 值分配给模型时，此设置将避免异常。</span><span class="sxs-lookup"><span data-stu-id="edaf4-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="edaf4-468">（代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex6 唱片集元数据分部类*）</span><span class="sxs-lookup"><span data-stu-id="edaf4-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="edaf4-469">此**唱片集**分部类具有一个**MetadataType**属性，该属性指向数据批注的**AlbumMetaData**类。</span><span class="sxs-lookup"><span data-stu-id="edaf4-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="edaf4-470">下面是一些用于注释唱片集模型的数据批注属性：</span><span class="sxs-lookup"><span data-stu-id="edaf4-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="edaf4-471">必需-指示该属性是必填字段</span><span class="sxs-lookup"><span data-stu-id="edaf4-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="edaf4-472">DisplayName-定义要用于窗体字段和验证消息的文本</span><span class="sxs-lookup"><span data-stu-id="edaf4-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="edaf4-473">DisplayFormat-指定显示和格式化数据字段的方式。</span><span class="sxs-lookup"><span data-stu-id="edaf4-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="edaf4-474">StringLength-定义字符串字段的最大长度</span><span class="sxs-lookup"><span data-stu-id="edaf4-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="edaf4-475">Range-为数值字段提供最大值和最小值</span><span class="sxs-lookup"><span data-stu-id="edaf4-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="edaf4-476">ScaffoldColumn-允许从编辑器窗体中隐藏字段</span><span class="sxs-lookup"><span data-stu-id="edaf4-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="edaf4-477">任务 2-运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="edaf4-478">在此任务中，您将使用在上一任务中选择的显示名称来测试 "创建" 和 "编辑" 页是否验证字段。</span><span class="sxs-lookup"><span data-stu-id="edaf4-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="edaf4-479">按**F5**运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="edaf4-480">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-480">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-481">将 URL 更改为 **/StoreManager/Create**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="edaf4-482">验证显示名称是否与分部类中的名称匹配（例如**唱片集画面 URL**而不是**AlbumArtUrl**）</span><span class="sxs-lookup"><span data-stu-id="edaf4-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="edaf4-483">单击 "**创建**"，不填充窗体。</span><span class="sxs-lookup"><span data-stu-id="edaf4-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="edaf4-484">验证是否获取了相应的验证消息。</span><span class="sxs-lookup"><span data-stu-id="edaf4-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="edaf4-485">!["创建" 页中已验证的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png ""创建" 页中已验证的字段")</span><span class="sxs-lookup"><span data-stu-id="edaf4-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="edaf4-486">*"创建" 页中已验证的字段*</span><span class="sxs-lookup"><span data-stu-id="edaf4-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="edaf4-487">您可以通过 "**编辑**" 页验证是否出现了这种情况。</span><span class="sxs-lookup"><span data-stu-id="edaf4-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="edaf4-488">将 URL 更改为 **/StoreManager/Edit/1** ，并验证显示名称是否与分部类中的名称匹配（例如**唱片集画面 URL**而不是**AlbumArtUrl**）。</span><span class="sxs-lookup"><span data-stu-id="edaf4-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="edaf4-489">清空 "**标题**" 和 "**价格**" 字段，然后单击 "**保存**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="edaf4-490">验证是否获取了相应的验证消息。</span><span class="sxs-lookup"><span data-stu-id="edaf4-490">Verify that you get the corresponding validation messages.</span></span>

    ![编辑页中已验证的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="edaf4-492">*编辑页中已验证的字段*</span><span class="sxs-lookup"><span data-stu-id="edaf4-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="edaf4-493">练习7：在客户端使用非引人注目 jQuery</span><span class="sxs-lookup"><span data-stu-id="edaf4-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="edaf4-494">在此练习中，你将了解如何在客户端启用 MVC 4 非引人注目 jQuery 验证。</span><span class="sxs-lookup"><span data-stu-id="edaf4-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="edaf4-495">非引人注目的 jQuery 使用数据 ajax 前缀 JavaScript 在服务器上调用操作方法，而不是 intrusively 发出内联客户端脚本。</span><span class="sxs-lookup"><span data-stu-id="edaf4-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="edaf4-496">任务 1-在启用非引人注目 jQuery 之前运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="edaf4-497">在此任务中，您将在包含 jQuery 之前运行该应用程序，以便比较这两个验证模型。</span><span class="sxs-lookup"><span data-stu-id="edaf4-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="edaf4-498">打开位于**Source/Ex7-UnobtrusivejQueryValidation/begin/** Folder 的**begin**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="edaf4-499">否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="edaf4-500">如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。</span><span class="sxs-lookup"><span data-stu-id="edaf4-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="edaf4-501">为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="edaf4-502">在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。</span><span class="sxs-lookup"><span data-stu-id="edaf4-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="edaf4-503">最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="edaf4-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="edaf4-504">使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。</span><span class="sxs-lookup"><span data-stu-id="edaf4-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="edaf4-505">使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。</span><span class="sxs-lookup"><span data-stu-id="edaf4-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="edaf4-506">这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。</span><span class="sxs-lookup"><span data-stu-id="edaf4-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="edaf4-507">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="edaf4-508">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-508">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-509">浏览 **/StoreManager/Create**并单击 "**创建**" 而不填满窗体，验证是否获取了验证消息：</span><span class="sxs-lookup"><span data-stu-id="edaf4-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="edaf4-510">![已禁用客户端验证](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "已禁用客户端验证")</span><span class="sxs-lookup"><span data-stu-id="edaf4-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="edaf4-511">*已禁用客户端验证*</span><span class="sxs-lookup"><span data-stu-id="edaf4-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="edaf4-512">在浏览器中，打开 HTML 源代码：</span><span class="sxs-lookup"><span data-stu-id="edaf4-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="edaf4-513">任务 2-启用非介入式客户端验证</span><span class="sxs-lookup"><span data-stu-id="edaf4-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="edaf4-514">在此任务中，**将从 web.config 文件中启用**jQuery 非**引人注目的客户端验证**，默认情况下，在所有新的 ASP.NET MVC 4 项目中将其设置为 false。</span><span class="sxs-lookup"><span data-stu-id="edaf4-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="edaf4-515">此外，还将添加必要的脚本引用，以使 jQuery 不引人注目的客户端验证工作。</span><span class="sxs-lookup"><span data-stu-id="edaf4-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="edaf4-516">在项目根目录**中打开 web.config**文件，并确保 " **ClientValidationEnabled** " 和 " **UnobtrusiveJavaScriptEnabled** " 键的值设置为 " **true**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="edaf4-517">还可以通过 Global.asax.cs 中的代码启用客户端验证，以获得相同的结果：</span><span class="sxs-lookup"><span data-stu-id="edaf4-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="edaf4-518">**HtmlHelper. ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="edaf4-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="edaf4-519">此外，还可以将 ClientValidationEnabled 属性分配到任何控制器，以获得自定义行为。</span><span class="sxs-lookup"><span data-stu-id="edaf4-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="edaf4-520">在**Views\StoreManager**中打开 "**创建"。**</span><span class="sxs-lookup"><span data-stu-id="edaf4-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="edaf4-521">请确保通过 &quot; **~/bundles/jqueryval**&quot; 捆绑在视图中引用以下脚本文件， **jquery. validate**和**jquery. validate**。</span><span class="sxs-lookup"><span data-stu-id="edaf4-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view through the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="edaf4-522">所有这些 jQuery 库都包含在 MVC 4 新项目中。</span><span class="sxs-lookup"><span data-stu-id="edaf4-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="edaf4-523">你可以在项目的 **/Scripts**文件夹中找到更多库。</span><span class="sxs-lookup"><span data-stu-id="edaf4-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="edaf4-524">若要使此验证库正常工作，需要添加对 jQuery framework 库的引用。</span><span class="sxs-lookup"><span data-stu-id="edaf4-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="edaf4-525">由于已将此引用添加到 **\_的布局 cshtml**文件中，因此您不需要在此特定视图中添加该引用。</span><span class="sxs-lookup"><span data-stu-id="edaf4-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="edaf4-526">任务 3-使用非引人注目 jQuery 验证运行应用程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="edaf4-527">在此任务中，将测试**StoreManager** create view 模板在用户创建新相册时使用 jQuery 库执行客户端验证。</span><span class="sxs-lookup"><span data-stu-id="edaf4-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="edaf4-528">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="edaf4-529">项目在主页中启动。</span><span class="sxs-lookup"><span data-stu-id="edaf4-529">The project starts in the Home page.</span></span> <span data-ttu-id="edaf4-530">浏览 **/StoreManager/Create**并单击 "**创建**" 而不填满窗体，验证是否获取了验证消息：</span><span class="sxs-lookup"><span data-stu-id="edaf4-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="edaf4-531">![已启用 jQuery 的客户端验证](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "已启用 jQuery 的客户端验证")</span><span class="sxs-lookup"><span data-stu-id="edaf4-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="edaf4-532">*已启用 jQuery 的客户端验证*</span><span class="sxs-lookup"><span data-stu-id="edaf4-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="edaf4-533">在浏览器中，打开 "创建视图" 的源代码：</span><span class="sxs-lookup"><span data-stu-id="edaf4-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="edaf4-534">对于每个客户端验证规则，非引人注目的 jQuery 会将具有数据-*rulename*=的属性添加 &quot;*消息*&quot;。</span><span class="sxs-lookup"><span data-stu-id="edaf4-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="edaf4-535">下面是一个标记列表，其中的标记将不引人注目地插入 html 输入字段以执行客户端验证：</span><span class="sxs-lookup"><span data-stu-id="edaf4-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="edaf4-536">数据-val</span><span class="sxs-lookup"><span data-stu-id="edaf4-536">Data-val</span></span>
   > - <span data-ttu-id="edaf4-537">数据值-数字</span><span class="sxs-lookup"><span data-stu-id="edaf4-537">Data-val-number</span></span>
   > - <span data-ttu-id="edaf4-538">数据-范围</span><span class="sxs-lookup"><span data-stu-id="edaf4-538">Data-val-range</span></span>
   > - <span data-ttu-id="edaf4-539">数据-值-范围-最小/数据-范围-最大值</span><span class="sxs-lookup"><span data-stu-id="edaf4-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="edaf4-540">数据-val-必需</span><span class="sxs-lookup"><span data-stu-id="edaf4-540">Data-val-required</span></span>
   > - <span data-ttu-id="edaf4-541">数据长度-长度</span><span class="sxs-lookup"><span data-stu-id="edaf4-541">Data-val-length</span></span>
   > - <span data-ttu-id="edaf4-542">数据-值-长度-最大/数据值-长度-分钟</span><span class="sxs-lookup"><span data-stu-id="edaf4-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="edaf4-543">所有数据值都用模型**数据批注**填充。</span><span class="sxs-lookup"><span data-stu-id="edaf4-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="edaf4-544">然后，可以在客户端运行在服务器端工作的所有逻辑。</span><span class="sxs-lookup"><span data-stu-id="edaf4-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="edaf4-545">例如，Price 属性在模型中具有以下数据批注：</span><span class="sxs-lookup"><span data-stu-id="edaf4-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="edaf4-546">使用非引人注目的 jQuery 后，生成的代码为：</span><span class="sxs-lookup"><span data-stu-id="edaf4-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="edaf4-547">摘要</span><span class="sxs-lookup"><span data-stu-id="edaf4-547">Summary</span></span>

<span data-ttu-id="edaf4-548">完成此动手实验后，你已了解如何让用户使用以下内容更改存储在数据库中的数据：</span><span class="sxs-lookup"><span data-stu-id="edaf4-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="edaf4-549">索引、创建、编辑、删除等控制器操作</span><span class="sxs-lookup"><span data-stu-id="edaf4-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="edaf4-550">用于在 HTML 表中显示属性的 ASP.NET MVC 基架功能</span><span class="sxs-lookup"><span data-stu-id="edaf4-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="edaf4-551">用于改进用户体验的自定义 HTML 帮助程序</span><span class="sxs-lookup"><span data-stu-id="edaf4-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="edaf4-552">对 HTTP GET 或 HTTP POST 调用做出反应的操作方法</span><span class="sxs-lookup"><span data-stu-id="edaf4-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="edaf4-553">类似视图模板（如创建和编辑）的共享编辑器模板</span><span class="sxs-lookup"><span data-stu-id="edaf4-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="edaf4-554">窗体元素，例如下拉</span><span class="sxs-lookup"><span data-stu-id="edaf4-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="edaf4-555">模型验证的数据批注</span><span class="sxs-lookup"><span data-stu-id="edaf4-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="edaf4-556">使用 jQuery 非引人注目库进行客户端验证</span><span class="sxs-lookup"><span data-stu-id="edaf4-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="edaf4-557">附录 A：安装 Visual Studio Express 2012 for Web</span><span class="sxs-lookup"><span data-stu-id="edaf4-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="edaf4-558">您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="edaf4-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="edaf4-559">以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。</span><span class="sxs-lookup"><span data-stu-id="edaf4-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="edaf4-560">请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="edaf4-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="edaf4-561">或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。</span><span class="sxs-lookup"><span data-stu-id="edaf4-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="edaf4-562">单击 "**立即安装**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-562">Click on **Install Now**.</span></span> <span data-ttu-id="edaf4-563">如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="edaf4-564">**Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="edaf4-565">![安装 Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "安装 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="edaf4-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="edaf4-566">*安装 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="edaf4-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="edaf4-567">阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。</span><span class="sxs-lookup"><span data-stu-id="edaf4-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受许可条款](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="edaf4-569">*接受许可条款*</span><span class="sxs-lookup"><span data-stu-id="edaf4-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="edaf4-570">等待下载和安装过程完成。</span><span class="sxs-lookup"><span data-stu-id="edaf4-570">Wait until the downloading and installation process completes.</span></span>

    ![安装进度](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="edaf4-572">*安装进度*</span><span class="sxs-lookup"><span data-stu-id="edaf4-572">*Installation progress*</span></span>
6. <span data-ttu-id="edaf4-573">安装完成后，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="edaf4-573">When the installation completes, click **Finish**.</span></span>

    ![安装完成](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="edaf4-575">*安装完成*</span><span class="sxs-lookup"><span data-stu-id="edaf4-575">*Installation completed*</span></span>
7. <span data-ttu-id="edaf4-576">单击 "**退出**" 以关闭 Web 平台安装程序。</span><span class="sxs-lookup"><span data-stu-id="edaf4-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="edaf4-577">若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。</span><span class="sxs-lookup"><span data-stu-id="edaf4-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磁贴](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="edaf4-579">*VS Express for Web 磁贴*</span><span class="sxs-lookup"><span data-stu-id="edaf4-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="edaf4-580">附录 B：使用代码片段</span><span class="sxs-lookup"><span data-stu-id="edaf4-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="edaf4-581">使用代码片段，您可以随时获得所需的全部代码。</span><span class="sxs-lookup"><span data-stu-id="edaf4-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="edaf4-582">实验室文档将告诉你何时可以使用它们，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="edaf4-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="edaf4-583">![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "使用 Visual Studio code 代码段将代码插入到项目中")</span><span class="sxs-lookup"><span data-stu-id="edaf4-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="edaf4-584">*使用 Visual Studio code 代码段将代码插入到项目中*</span><span class="sxs-lookup"><span data-stu-id="edaf4-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="edaf4-585">***使用键盘添加代码片段（C#仅限）***</span><span class="sxs-lookup"><span data-stu-id="edaf4-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="edaf4-586">将光标放在要插入代码的位置。</span><span class="sxs-lookup"><span data-stu-id="edaf4-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="edaf4-587">开始键入代码片段名称（不含空格或连字符）。</span><span class="sxs-lookup"><span data-stu-id="edaf4-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="edaf4-588">请注意，IntelliSense 显示匹配的代码段名称。</span><span class="sxs-lookup"><span data-stu-id="edaf4-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="edaf4-589">选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。</span><span class="sxs-lookup"><span data-stu-id="edaf4-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="edaf4-590">按 Tab 键两次，将代码段插入到光标位置。</span><span class="sxs-lookup"><span data-stu-id="edaf4-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="edaf4-591">![开始键入代码片段名称](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "开始键入代码片段名称")</span><span class="sxs-lookup"><span data-stu-id="edaf4-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="edaf4-592">*开始键入代码片段名称*</span><span class="sxs-lookup"><span data-stu-id="edaf4-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="edaf4-593">![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "按 Tab 键以选择突出显示的代码段")</span><span class="sxs-lookup"><span data-stu-id="edaf4-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="edaf4-594">*按 Tab 键以选择突出显示的代码段*</span><span class="sxs-lookup"><span data-stu-id="edaf4-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="edaf4-595">![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "再次按 Tab 键，代码片段将展开")</span><span class="sxs-lookup"><span data-stu-id="edaf4-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="edaf4-596">*再次按 Tab 键，代码片段将展开*</span><span class="sxs-lookup"><span data-stu-id="edaf4-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="edaf4-597">***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2.</span><span class="sxs-lookup"><span data-stu-id="edaf4-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="edaf4-598">右键单击要插入代码片段的位置。</span><span class="sxs-lookup"><span data-stu-id="edaf4-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="edaf4-599">选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。</span><span class="sxs-lookup"><span data-stu-id="edaf4-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="edaf4-600">通过单击从列表中选择相关的代码片段。</span><span class="sxs-lookup"><span data-stu-id="edaf4-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="edaf4-601">![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")</span><span class="sxs-lookup"><span data-stu-id="edaf4-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="edaf4-602">*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*</span><span class="sxs-lookup"><span data-stu-id="edaf4-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="edaf4-603">![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "通过单击从列表中选择相关的代码片段")</span><span class="sxs-lookup"><span data-stu-id="edaf4-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="edaf4-604">*通过单击从列表中选择相关的代码片段*</span><span class="sxs-lookup"><span data-stu-id="edaf4-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
