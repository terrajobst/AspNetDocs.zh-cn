---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 单元测试 ASP.NET Web API 2 时的模拟实体框架 |Microsoft Docs
author: Rick-Anderson
description: 本指南和应用程序演示如何为使用实体框架的 Web API 2 应用程序创建单元测试。 它演示如何修改 。
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447086"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a><span data-ttu-id="e167c-104">单元测试 ASP.NET Web API 2 时的模拟实体框架</span><span class="sxs-lookup"><span data-stu-id="e167c-104">Mocking Entity Framework when Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="e167c-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e167c-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="e167c-106">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="e167c-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="e167c-107">本指南和应用程序演示如何为使用实体框架的 Web API 2 应用程序创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="e167c-107">This guidance and application demonstrate how to create unit tests for your Web API 2 application that uses the Entity Framework.</span></span> <span data-ttu-id="e167c-108">它演示如何修改基架控制器以便为测试传递上下文对象，以及如何创建用于实体框架的测试对象。</span><span class="sxs-lookup"><span data-stu-id="e167c-108">It shows how to modify the scaffolded controller to enable passing a context object for testing, and how to create test objects that work with Entity Framework.</span></span>
>
> <span data-ttu-id="e167c-109">有关 ASP.NET Web API 的单元测试的简介，请参阅[使用 ASP.NET Web API 2 的单元测试](unit-testing-with-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="e167c-109">For an introduction to unit testing with ASP.NET Web API, see [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md).</span></span>
>
> <span data-ttu-id="e167c-110">本教程假设你熟悉 ASP.NET Web API 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="e167c-110">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="e167c-111">有关介绍性教程，请参阅[使用 ASP.NET Web API 2 入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="e167c-111">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e167c-112">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="e167c-112">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="e167c-113">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e167c-113">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="e167c-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="e167c-114">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="e167c-115">主题内容</span><span class="sxs-lookup"><span data-stu-id="e167c-115">In this topic</span></span>

<span data-ttu-id="e167c-116">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="e167c-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="e167c-117">先决条件</span><span class="sxs-lookup"><span data-stu-id="e167c-117">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="e167c-118">下载代码</span><span class="sxs-lookup"><span data-stu-id="e167c-118">Download code</span></span>](#download)
- [<span data-ttu-id="e167c-119">创建具有单元测试项目的应用程序</span><span class="sxs-lookup"><span data-stu-id="e167c-119">Create application with unit test project</span></span>](#appwithunittest)
- [<span data-ttu-id="e167c-120">创建模型类</span><span class="sxs-lookup"><span data-stu-id="e167c-120">Create the model class</span></span>](#modelclass)
- [<span data-ttu-id="e167c-121">添加控制器</span><span class="sxs-lookup"><span data-stu-id="e167c-121">Add the controller</span></span>](#controller)
- [<span data-ttu-id="e167c-122">添加依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="e167c-122">Add dependency injection</span></span>](#dependency)
- [<span data-ttu-id="e167c-123">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="e167c-123">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="e167c-124">创建测试上下文</span><span class="sxs-lookup"><span data-stu-id="e167c-124">Create test context</span></span>](#testcontext)
- [<span data-ttu-id="e167c-125">创建测试</span><span class="sxs-lookup"><span data-stu-id="e167c-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="e167c-126">运行测试</span><span class="sxs-lookup"><span data-stu-id="e167c-126">Run tests</span></span>](#runtests)

<span data-ttu-id="e167c-127">如果已[使用 ASP.NET Web API 2 完成单元测试](unit-testing-with-aspnet-web-api.md)中的步骤，则可以跳到[添加控制器](#controller)部分。</span><span class="sxs-lookup"><span data-stu-id="e167c-127">If you have already completed the steps in [Unit Testing with ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md), you can skip to the section [Add the controller](#controller).</span></span>

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="e167c-128">系统必备</span><span class="sxs-lookup"><span data-stu-id="e167c-128">Prerequisites</span></span>

<span data-ttu-id="e167c-129">Visual Studio 2017 社区版、专业版或企业版</span><span class="sxs-lookup"><span data-stu-id="e167c-129">Visual Studio 2017 Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="e167c-130">下载代码</span><span class="sxs-lookup"><span data-stu-id="e167c-130">Download code</span></span>

<span data-ttu-id="e167c-131">下载[完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。</span><span class="sxs-lookup"><span data-stu-id="e167c-131">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="e167c-132">可下载的项目包含本主题和[单元测试 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md)主题的单元测试代码。</span><span class="sxs-lookup"><span data-stu-id="e167c-132">The downloadable project includes unit test code for this topic and for the [Unit Testing ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="e167c-133">创建具有单元测试项目的应用程序</span><span class="sxs-lookup"><span data-stu-id="e167c-133">Create application with unit test project</span></span>

<span data-ttu-id="e167c-134">可在创建应用程序时创建单元测试项目，或者将单元测试项目添加到现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="e167c-134">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="e167c-135">本教程演示如何在创建应用程序时创建单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="e167c-135">This tutorial shows creating a unit test project when creating the application.</span></span>

<span data-ttu-id="e167c-136">创建名为**StoreApp**的新 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="e167c-136">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

<span data-ttu-id="e167c-137">在 "新建 ASP.NET 项目" 窗口中，选择 "**空**" 模板，并为 Web API 添加文件夹和核心引用。</span><span class="sxs-lookup"><span data-stu-id="e167c-137">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="e167c-138">选择 "**添加单元测试**" 选项。</span><span class="sxs-lookup"><span data-stu-id="e167c-138">Select the **Add unit tests** option.</span></span> <span data-ttu-id="e167c-139">单元测试项目被自动命名为**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="e167c-139">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="e167c-140">您可以保留此名称。</span><span class="sxs-lookup"><span data-stu-id="e167c-140">You can keep this name.</span></span>

![创建单元测试项目](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

<span data-ttu-id="e167c-142">创建应用程序后，你将看到它包含两个项目- **StoreApp**和**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="e167c-142">After creating the application, you will see it contains two projects - **StoreApp** and **StoreApp.Tests**.</span></span>

<a id="modelclass"></a>
## <a name="create-the-model-class"></a><span data-ttu-id="e167c-143">创建模型类</span><span class="sxs-lookup"><span data-stu-id="e167c-143">Create the model class</span></span>

<span data-ttu-id="e167c-144">在 StoreApp 项目中，将类文件添加到名为**Product.cs**的**模型**文件夹中。</span><span class="sxs-lookup"><span data-stu-id="e167c-144">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="e167c-145">将文件的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e167c-145">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

<span data-ttu-id="e167c-146">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="e167c-146">Build the solution.</span></span>

<a id="controller"></a>
## <a name="add-the-controller"></a><span data-ttu-id="e167c-147">添加控制器</span><span class="sxs-lookup"><span data-stu-id="e167c-147">Add the controller</span></span>

<span data-ttu-id="e167c-148">右键单击 "控制器" 文件夹，然后选择 "**添加**并**新建基架项**"。</span><span class="sxs-lookup"><span data-stu-id="e167c-148">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="e167c-149">使用实体框架选择 "包含操作的 Web API 2 控制器"。</span><span class="sxs-lookup"><span data-stu-id="e167c-149">Select Web API 2 Controller with actions, using Entity Framework.</span></span>

![添加新控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

<span data-ttu-id="e167c-151">设置下列值：</span><span class="sxs-lookup"><span data-stu-id="e167c-151">Set the following values:</span></span>

- <span data-ttu-id="e167c-152">控制器名称： **ProductController**</span><span class="sxs-lookup"><span data-stu-id="e167c-152">Controller name: **ProductController**</span></span>
- <span data-ttu-id="e167c-153">Model 类：**产品**</span><span class="sxs-lookup"><span data-stu-id="e167c-153">Model class: **Product**</span></span>
- <span data-ttu-id="e167c-154">数据上下文类： [选择**新的数据上下文**按钮，该按钮可填充下面所示的值]</span><span class="sxs-lookup"><span data-stu-id="e167c-154">Data context class: [Select **New data context** button which fills in the values seen below]</span></span>

![指定控制器](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

<span data-ttu-id="e167c-156">单击 "**添加**" 以创建带有自动生成的代码的控制器。</span><span class="sxs-lookup"><span data-stu-id="e167c-156">Click **Add** to create the controller with automatically-generated code.</span></span> <span data-ttu-id="e167c-157">此代码包括用于创建、检索、更新和删除 Product 类的实例的方法。</span><span class="sxs-lookup"><span data-stu-id="e167c-157">The code includes methods for creating, retrieving, updating and deleting instances of the Product class.</span></span> <span data-ttu-id="e167c-158">下面的代码演示了用于添加产品的方法。</span><span class="sxs-lookup"><span data-stu-id="e167c-158">The following code shows the method for add a Product.</span></span> <span data-ttu-id="e167c-159">请注意，该方法将返回**IHttpActionResult**的实例。</span><span class="sxs-lookup"><span data-stu-id="e167c-159">Notice that the method returns an instance of **IHttpActionResult**.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

<span data-ttu-id="e167c-160">IHttpActionResult 是 Web API 2 中的一项新功能，它简化了单元测试的开发。</span><span class="sxs-lookup"><span data-stu-id="e167c-160">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span>

<span data-ttu-id="e167c-161">在下一部分中，你将自定义生成的代码，以便将测试对象传递到控制器。</span><span class="sxs-lookup"><span data-stu-id="e167c-161">In the next section, you will customize the generated code to facilitate passing test objects to the controller.</span></span>

<a id="dependency"></a>
## <a name="add-dependency-injection"></a><span data-ttu-id="e167c-162">添加依赖关系注入</span><span class="sxs-lookup"><span data-stu-id="e167c-162">Add dependency injection</span></span>

<span data-ttu-id="e167c-163">目前，ProductController 类硬编码为使用 StoreAppContext 类的实例。</span><span class="sxs-lookup"><span data-stu-id="e167c-163">Currently, the ProductController class is hard-coded to use an instance of the StoreAppContext class.</span></span> <span data-ttu-id="e167c-164">将使用名为 "依赖关系注入" 的模式来修改应用程序，并删除硬编码的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="e167c-164">You will use a pattern called dependency injection to modify your application and remove that hard-coded dependency.</span></span> <span data-ttu-id="e167c-165">通过中断此依赖项，你可以在测试时传入 mock 对象。</span><span class="sxs-lookup"><span data-stu-id="e167c-165">By breaking this dependency, you can pass in a mock object when testing.</span></span>

<span data-ttu-id="e167c-166">右键单击 "**模型**" 文件夹，然后添加一个名为**IStoreAppContext**的新接口。</span><span class="sxs-lookup"><span data-stu-id="e167c-166">Right-click the **Models** folder, and add a new interface named **IStoreAppContext**.</span></span>

<span data-ttu-id="e167c-167">将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e167c-167">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

<span data-ttu-id="e167c-168">打开 StoreAppContext.cs 文件并进行以下突出显示的更改。</span><span class="sxs-lookup"><span data-stu-id="e167c-168">Open the StoreAppContext.cs file and make the following highlighted changes.</span></span> <span data-ttu-id="e167c-169">需要注意的重要更改如下：</span><span class="sxs-lookup"><span data-stu-id="e167c-169">The important changes to note are:</span></span>

- <span data-ttu-id="e167c-170">StoreAppContext 类实现 IStoreAppContext 接口</span><span class="sxs-lookup"><span data-stu-id="e167c-170">StoreAppContext class implements IStoreAppContext interface</span></span>
- <span data-ttu-id="e167c-171">实现 MarkAsModified 方法</span><span class="sxs-lookup"><span data-stu-id="e167c-171">MarkAsModified method is implemented</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

<span data-ttu-id="e167c-172">打开 ProductController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="e167c-172">Open the ProductController.cs file.</span></span> <span data-ttu-id="e167c-173">更改现有代码以匹配突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="e167c-173">Change the existing code to match the highlighted code.</span></span> <span data-ttu-id="e167c-174">这些更改将中断对 StoreAppContext 的依赖关系，并使其他类能够为上下文类传入不同的对象。</span><span class="sxs-lookup"><span data-stu-id="e167c-174">These changes break the dependency on StoreAppContext and enable other classes to pass in a different object for the context class.</span></span> <span data-ttu-id="e167c-175">此更改将使你可以在单元测试期间传入测试上下文。</span><span class="sxs-lookup"><span data-stu-id="e167c-175">This change will enable you to pass in a test context during unit tests.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

<span data-ttu-id="e167c-176">还必须在 ProductController 中进行一项更改。</span><span class="sxs-lookup"><span data-stu-id="e167c-176">There is one more change you must make in ProductController.</span></span> <span data-ttu-id="e167c-177">在**PutProduct**方法中，使用对 MarkAsModified 方法的调用替换设置要修改的实体状态的行。</span><span class="sxs-lookup"><span data-stu-id="e167c-177">In the **PutProduct** method, replace the line that sets the entity state to modified with a call to the MarkAsModified method.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

<span data-ttu-id="e167c-178">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="e167c-178">Build the solution.</span></span>

<span data-ttu-id="e167c-179">你现在已准备好设置测试项目。</span><span class="sxs-lookup"><span data-stu-id="e167c-179">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="e167c-180">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="e167c-180">Install NuGet packages in test project</span></span>

<span data-ttu-id="e167c-181">使用空模板创建应用程序时，单元测试项目（StoreApp）不包含任何已安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e167c-181">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="e167c-182">其他模板（如 Web API 模板）在单元测试项目中包含一些 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e167c-182">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="e167c-183">对于本教程，必须将实体框架包和 Microsoft ASP.NET Web API 2 核心包添加到测试项目。</span><span class="sxs-lookup"><span data-stu-id="e167c-183">For this tutorial, you must include the Entity Framework package and the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="e167c-184">右键单击 "StoreApp" 项目，然后选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="e167c-184">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="e167c-185">您必须选择 StoreApp 项目，才能将包添加到该项目中。</span><span class="sxs-lookup"><span data-stu-id="e167c-185">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![管理包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

<span data-ttu-id="e167c-187">在联机包中，查找并安装 EntityFramework 包（版本6.0 或更高版本）。</span><span class="sxs-lookup"><span data-stu-id="e167c-187">From the Online packages, find and install the EntityFramework package (version 6.0 or later).</span></span> <span data-ttu-id="e167c-188">如果似乎已安装 EntityFramework 包，则可能已选择 StoreApp 项目而不是 StoreApp 项目。</span><span class="sxs-lookup"><span data-stu-id="e167c-188">If it appears that the EntityFramework package is already installed, you may have selected the StoreApp project instead of the StoreApp.Tests project.</span></span>

![添加实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

<span data-ttu-id="e167c-190">查找并安装 Microsoft ASP.NET Web API 2 核心包。</span><span class="sxs-lookup"><span data-stu-id="e167c-190">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![安装 web api 核心包](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

<span data-ttu-id="e167c-192">关闭 "管理 NuGet 包" 窗口。</span><span class="sxs-lookup"><span data-stu-id="e167c-192">Close the Manage NuGet Packages window.</span></span>

<a id="testcontext"></a>
## <a name="create-test-context"></a><span data-ttu-id="e167c-193">创建测试上下文</span><span class="sxs-lookup"><span data-stu-id="e167c-193">Create test context</span></span>

<span data-ttu-id="e167c-194">向测试项目添加一个名为**TestDbSet**的类。</span><span class="sxs-lookup"><span data-stu-id="e167c-194">Add a class named **TestDbSet** to the test project.</span></span> <span data-ttu-id="e167c-195">此类用作测试数据集的基类。</span><span class="sxs-lookup"><span data-stu-id="e167c-195">This class serves as the base class for your test data set.</span></span> <span data-ttu-id="e167c-196">将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e167c-196">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

<span data-ttu-id="e167c-197">将名为**TestProductDbSet**的类添加到包含以下代码的测试项目。</span><span class="sxs-lookup"><span data-stu-id="e167c-197">Add a class named **TestProductDbSet** to the test project which contains the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

<span data-ttu-id="e167c-198">添加一个名为**TestStoreAppContext**的类，并将现有代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e167c-198">Add a class named **TestStoreAppContext** and replace the existing code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="e167c-199">创建测试</span><span class="sxs-lookup"><span data-stu-id="e167c-199">Create tests</span></span>

<span data-ttu-id="e167c-200">默认情况下，你的测试项目包含一个名为**UnitTest1.cs**的空测试文件。</span><span class="sxs-lookup"><span data-stu-id="e167c-200">By default, your test project includes an empty test file named **UnitTest1.cs**.</span></span> <span data-ttu-id="e167c-201">此文件显示用于创建测试方法的属性。</span><span class="sxs-lookup"><span data-stu-id="e167c-201">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="e167c-202">对于本教程，你可以删除此文件，因为你将添加新的测试类。</span><span class="sxs-lookup"><span data-stu-id="e167c-202">For this tutorial, you can delete this file because you will add a new test class.</span></span>

<span data-ttu-id="e167c-203">向测试项目添加一个名为**TestProductController**的类。</span><span class="sxs-lookup"><span data-stu-id="e167c-203">Add a class named **TestProductController** to the test project.</span></span> <span data-ttu-id="e167c-204">将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e167c-204">Replace the code with the following code.</span></span>

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="e167c-205">运行测试</span><span class="sxs-lookup"><span data-stu-id="e167c-205">Run tests</span></span>

<span data-ttu-id="e167c-206">你现在已准备好运行测试。</span><span class="sxs-lookup"><span data-stu-id="e167c-206">You are now ready to run the tests.</span></span> <span data-ttu-id="e167c-207">将测试标记为**TestMethod**属性的所有方法。</span><span class="sxs-lookup"><span data-stu-id="e167c-207">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="e167c-208">从 "**测试**" 菜单项中，运行测试。</span><span class="sxs-lookup"><span data-stu-id="e167c-208">From the **Test** menu item, run the tests.</span></span>

![运行测试](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

<span data-ttu-id="e167c-210">打开 "**测试资源管理器**" 窗口，并注意测试的结果。</span><span class="sxs-lookup"><span data-stu-id="e167c-210">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![测试结果](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
