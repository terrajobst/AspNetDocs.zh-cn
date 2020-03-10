---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 单元测试 ASP.NET Web API 2 |Microsoft Docs
author: Rick-Anderson
description: 本指南和应用程序演示了如何为 Web API 2 应用程序创建简单的单元测试。 本教程介绍如何包括单元测试的一 。
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446984"
---
# <a name="unit-testing-aspnet-web-api-2"></a><span data-ttu-id="a03fc-104">单元测试 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="a03fc-104">Unit Testing ASP.NET Web API 2</span></span>

<span data-ttu-id="a03fc-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a03fc-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[<span data-ttu-id="a03fc-106">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="a03fc-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> <span data-ttu-id="a03fc-107">本指南和应用程序演示了如何为 Web API 2 应用程序创建简单的单元测试。</span><span class="sxs-lookup"><span data-stu-id="a03fc-107">This guidance and application demonstrate how to create simple unit tests for your Web API 2 application.</span></span> <span data-ttu-id="a03fc-108">本教程演示如何在解决方案中包括单元测试项目，并编写用于检查控制器方法返回的值的测试方法。</span><span class="sxs-lookup"><span data-stu-id="a03fc-108">This tutorial shows how to include a unit test project in your solution, and write test methods that check the returned values from a controller method.</span></span>
>
> <span data-ttu-id="a03fc-109">本教程假设你熟悉 ASP.NET Web API 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="a03fc-109">This tutorial assumes you are familiar with the basic concepts of ASP.NET Web API.</span></span> <span data-ttu-id="a03fc-110">有关介绍性教程，请参阅[使用 ASP.NET Web API 2 入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="a03fc-110">For an introductory tutorial, see [Getting Started with ASP.NET Web API 2](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).</span></span>
>
> <span data-ttu-id="a03fc-111">本主题中的单元测试有意限制为简单的数据应用场景。</span><span class="sxs-lookup"><span data-stu-id="a03fc-111">The unit tests in this topic are intentionally limited to simple data scenarios.</span></span> <span data-ttu-id="a03fc-112">有关更高级数据方案的单元测试，请参阅[单元测试 ASP.NET Web API 2 时的模拟实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="a03fc-112">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="a03fc-113">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="a03fc-113">Software versions used in the tutorial</span></span>
>
> - [<span data-ttu-id="a03fc-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="a03fc-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - <span data-ttu-id="a03fc-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="a03fc-115">Web API 2</span></span>

## <a name="in-this-topic"></a><span data-ttu-id="a03fc-116">主题内容</span><span class="sxs-lookup"><span data-stu-id="a03fc-116">In this topic</span></span>

<span data-ttu-id="a03fc-117">本主题包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="a03fc-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="a03fc-118">先决条件</span><span class="sxs-lookup"><span data-stu-id="a03fc-118">Prerequisites</span></span>](#prereqs)
- [<span data-ttu-id="a03fc-119">下载代码</span><span class="sxs-lookup"><span data-stu-id="a03fc-119">Download code</span></span>](#download)
- [<span data-ttu-id="a03fc-120">创建具有单元测试项目的应用程序</span><span class="sxs-lookup"><span data-stu-id="a03fc-120">Create application with unit test project</span></span>](#appwithunittest)
    - [<span data-ttu-id="a03fc-121">创建应用程序时添加单元测试项目</span><span class="sxs-lookup"><span data-stu-id="a03fc-121">Add unit test project when creating the application</span></span>](#whencreate)
    - [<span data-ttu-id="a03fc-122">向现有应用程序添加单元测试项目</span><span class="sxs-lookup"><span data-stu-id="a03fc-122">Add unit test project to an existing application</span></span>](#addtoexisting)
- [<span data-ttu-id="a03fc-123">设置 Web API 2 应用程序</span><span class="sxs-lookup"><span data-stu-id="a03fc-123">Set up the Web API 2 application</span></span>](#setupproject)
- [<span data-ttu-id="a03fc-124">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="a03fc-124">Install NuGet packages in test project</span></span>](#testpackages)
- [<span data-ttu-id="a03fc-125">创建测试</span><span class="sxs-lookup"><span data-stu-id="a03fc-125">Create tests</span></span>](#tests)
- [<span data-ttu-id="a03fc-126">运行测试</span><span class="sxs-lookup"><span data-stu-id="a03fc-126">Run tests</span></span>](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a><span data-ttu-id="a03fc-127">系统必备</span><span class="sxs-lookup"><span data-stu-id="a03fc-127">Prerequisites</span></span>

<span data-ttu-id="a03fc-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社区版、专业版或企业版</span><span class="sxs-lookup"><span data-stu-id="a03fc-128">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional or Enterprise edition</span></span>

<a id="download"></a>
## <a name="download-code"></a><span data-ttu-id="a03fc-129">下载代码</span><span class="sxs-lookup"><span data-stu-id="a03fc-129">Download code</span></span>

<span data-ttu-id="a03fc-130">下载[完成的项目](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)。</span><span class="sxs-lookup"><span data-stu-id="a03fc-130">Download the [completed project](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11).</span></span> <span data-ttu-id="a03fc-131">可下载的项目包含本主题的单元测试代码以及[单元测试 ASP.NET Web API 主题的模拟实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="a03fc-131">The downloadable project includes unit test code for this topic and for the [Mocking Entity Framework when Unit Testing ASP.NET Web API](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) topic.</span></span>

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a><span data-ttu-id="a03fc-132">创建具有单元测试项目的应用程序</span><span class="sxs-lookup"><span data-stu-id="a03fc-132">Create application with unit test project</span></span>

<span data-ttu-id="a03fc-133">可在创建应用程序时创建单元测试项目，或者将单元测试项目添加到现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="a03fc-133">You can either create a unit test project when creating your application or add a unit test project to an existing application.</span></span> <span data-ttu-id="a03fc-134">本教程演示创建单元测试项目的两种方法。</span><span class="sxs-lookup"><span data-stu-id="a03fc-134">This tutorial shows both methods for creating a unit test project.</span></span> <span data-ttu-id="a03fc-135">若要按照本教程操作，可以使用这两种方法。</span><span class="sxs-lookup"><span data-stu-id="a03fc-135">To follow this tutorial, you can use either approach.</span></span>

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a><span data-ttu-id="a03fc-136">创建应用程序时添加单元测试项目</span><span class="sxs-lookup"><span data-stu-id="a03fc-136">Add unit test project when creating the application</span></span>

<span data-ttu-id="a03fc-137">创建名为**StoreApp**的新 ASP.NET Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a03fc-137">Create a new ASP.NET Web Application named **StoreApp**.</span></span>

![创建项目](unit-testing-with-aspnet-web-api/_static/image1.png)

<span data-ttu-id="a03fc-139">在 "新建 ASP.NET 项目" 窗口中，选择 "**空**" 模板，并为 Web API 添加文件夹和核心引用。</span><span class="sxs-lookup"><span data-stu-id="a03fc-139">In the New ASP.NET Project windows, select the **Empty** template and add folders and core references for Web API.</span></span> <span data-ttu-id="a03fc-140">选择 "**添加单元测试**" 选项。</span><span class="sxs-lookup"><span data-stu-id="a03fc-140">Select the **Add unit tests** option.</span></span> <span data-ttu-id="a03fc-141">单元测试项目被自动命名为**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="a03fc-141">The unit test project is automatically named **StoreApp.Tests**.</span></span> <span data-ttu-id="a03fc-142">您可以保留此名称。</span><span class="sxs-lookup"><span data-stu-id="a03fc-142">You can keep this name.</span></span>

![创建单元测试项目](unit-testing-with-aspnet-web-api/_static/image2.png)

<span data-ttu-id="a03fc-144">创建应用程序后，您将看到它包含两个项目。</span><span class="sxs-lookup"><span data-stu-id="a03fc-144">After creating the application, you will see it contains two projects.</span></span>

![两个项目](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a><span data-ttu-id="a03fc-146">向现有应用程序添加单元测试项目</span><span class="sxs-lookup"><span data-stu-id="a03fc-146">Add unit test project to an existing application</span></span>

<span data-ttu-id="a03fc-147">如果在创建应用程序时未创建单元测试项目，则可以随时添加一个。</span><span class="sxs-lookup"><span data-stu-id="a03fc-147">If you did not create the unit test project when you created your application, you can add one at any time.</span></span> <span data-ttu-id="a03fc-148">例如，假设已有一个名为 StoreApp 的应用程序，并且想要添加单元测试。</span><span class="sxs-lookup"><span data-stu-id="a03fc-148">For example, suppose you already have an application named StoreApp, and you want to add unit tests.</span></span> <span data-ttu-id="a03fc-149">若要添加单元测试项目，请右键单击解决方案，然后选择 "**添加**" 和 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="a03fc-149">To add a unit test project, right-click your solution and select **Add** and **New Project**.</span></span>

![向解决方案添加新项目](unit-testing-with-aspnet-web-api/_static/image4.png)

<span data-ttu-id="a03fc-151">在左窗格中选择 "**测试**"，然后选择 "**单元测试项目**" 作为 "项目类型"。</span><span class="sxs-lookup"><span data-stu-id="a03fc-151">Select **Test** in the left pane, and select **Unit Test Project** for the project type.</span></span> <span data-ttu-id="a03fc-152">将项目命名为**StoreApp**。</span><span class="sxs-lookup"><span data-stu-id="a03fc-152">Name the project **StoreApp.Tests**.</span></span>

![添加单元测试项目](unit-testing-with-aspnet-web-api/_static/image5.png)

<span data-ttu-id="a03fc-154">你将在你的解决方案中看到该单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="a03fc-154">You will see the unit test project in your solution.</span></span>

<span data-ttu-id="a03fc-155">在单元测试项目中，添加对原始项目的项目引用。</span><span class="sxs-lookup"><span data-stu-id="a03fc-155">In the unit test project, add a project reference to the original project.</span></span>

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a><span data-ttu-id="a03fc-156">设置 Web API 2 应用程序</span><span class="sxs-lookup"><span data-stu-id="a03fc-156">Set up the Web API 2 application</span></span>

<span data-ttu-id="a03fc-157">在 StoreApp 项目中，将类文件添加到名为**Product.cs**的**模型**文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a03fc-157">In your StoreApp project, add a class file to the **Models** folder named **Product.cs**.</span></span> <span data-ttu-id="a03fc-158">将文件的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="a03fc-158">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="a03fc-159">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="a03fc-159">Build the solution.</span></span>

<span data-ttu-id="a03fc-160">右键单击 "控制器" 文件夹，然后选择 "**添加**并**新建基架项**"。</span><span class="sxs-lookup"><span data-stu-id="a03fc-160">Right-click the Controllers folder and select **Add** and **New Scaffolded Item**.</span></span> <span data-ttu-id="a03fc-161">选择 " **WEB API 2 控制器-空**"。</span><span class="sxs-lookup"><span data-stu-id="a03fc-161">Select **Web API 2 Controller - Empty**.</span></span>

![添加新控制器](unit-testing-with-aspnet-web-api/_static/image6.png)

<span data-ttu-id="a03fc-163">将控制器名称设置为**SimpleProductController**，并单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="a03fc-163">Set the controller name to **SimpleProductController**, and click **Add**.</span></span>

![指定控制器](unit-testing-with-aspnet-web-api/_static/image7.png)

<span data-ttu-id="a03fc-165">用下面的代码替换现有代码。</span><span class="sxs-lookup"><span data-stu-id="a03fc-165">Replace the existing code with the following code.</span></span> <span data-ttu-id="a03fc-166">为了简化此示例，数据存储在列表中，而不是数据库中。</span><span class="sxs-lookup"><span data-stu-id="a03fc-166">To simplify this example, the data is stored in a list rather than a database.</span></span> <span data-ttu-id="a03fc-167">此类中定义的列表表示生产数据。</span><span class="sxs-lookup"><span data-stu-id="a03fc-167">The list defined in this class represents the production data.</span></span> <span data-ttu-id="a03fc-168">请注意，控制器包含一个构造函数，该构造函数采用产品对象列表作为参数。</span><span class="sxs-lookup"><span data-stu-id="a03fc-168">Notice that the controller includes a constructor that takes as a parameter a list of Product objects.</span></span> <span data-ttu-id="a03fc-169">此构造函数使你能够在单元测试时传递测试数据。</span><span class="sxs-lookup"><span data-stu-id="a03fc-169">This constructor enables you to pass test data when unit testing.</span></span> <span data-ttu-id="a03fc-170">控制器还包括两个**异步**方法，用于说明单元测试的异步方法。</span><span class="sxs-lookup"><span data-stu-id="a03fc-170">The controller also includes two **async** methods to illustrate unit testing asynchronous methods.</span></span> <span data-ttu-id="a03fc-171">这些异步方法是通过调用**system.threading.tasks.task.fromresult**来实现的，以最大程度地减少无关的代码，但通常情况下，方法会包括消耗大量资源的操作。</span><span class="sxs-lookup"><span data-stu-id="a03fc-171">These async methods were implemented by calling **Task.FromResult** to minimize extraneous code, but normally the methods would include resource-intensive operations.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="a03fc-172">GetProduct 方法返回**IHttpActionResult**接口的实例。</span><span class="sxs-lookup"><span data-stu-id="a03fc-172">The GetProduct method returns an instance of the **IHttpActionResult** interface.</span></span> <span data-ttu-id="a03fc-173">IHttpActionResult 是 Web API 2 中的一项新功能，它简化了单元测试的开发。</span><span class="sxs-lookup"><span data-stu-id="a03fc-173">IHttpActionResult is one of the new features in Web API 2, and it simplifies unit test development.</span></span> <span data-ttu-id="a03fc-174">[在 IHttpActionResult 命名空间](https://msdn.microsoft.com/library/system.web.http.results.aspx)中找到实现了接口的类。</span><span class="sxs-lookup"><span data-stu-id="a03fc-174">Classes that implement the IHttpActionResult interface are found in the [System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) namespace.</span></span> <span data-ttu-id="a03fc-175">这些类表示来自操作请求的可能响应，它们对应于 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="a03fc-175">These classes represent possible responses from an action request, and they correspond to HTTP status codes.</span></span>

<span data-ttu-id="a03fc-176">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="a03fc-176">Build the solution.</span></span>

<span data-ttu-id="a03fc-177">你现在已准备好设置测试项目。</span><span class="sxs-lookup"><span data-stu-id="a03fc-177">You are now ready to set up the test project.</span></span>

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a><span data-ttu-id="a03fc-178">在测试项目中安装 NuGet 包</span><span class="sxs-lookup"><span data-stu-id="a03fc-178">Install NuGet packages in test project</span></span>

<span data-ttu-id="a03fc-179">使用空模板创建应用程序时，单元测试项目（StoreApp）不包含任何已安装的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="a03fc-179">When you use the Empty template to create an application, the unit test project (StoreApp.Tests) does not include any installed NuGet packages.</span></span> <span data-ttu-id="a03fc-180">其他模板（如 Web API 模板）在单元测试项目中包含一些 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="a03fc-180">Other templates, such as the Web API template, include some NuGet packages in the unit test project.</span></span> <span data-ttu-id="a03fc-181">对于本教程，必须将 Microsoft ASP.NET Web API 2 核心包添加到测试项目中。</span><span class="sxs-lookup"><span data-stu-id="a03fc-181">For this tutorial, you must include the Microsoft ASP.NET Web API 2 Core package to the test project.</span></span>

<span data-ttu-id="a03fc-182">右键单击 "StoreApp" 项目，然后选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="a03fc-182">Right-click the StoreApp.Tests project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="a03fc-183">您必须选择 StoreApp 项目，才能将包添加到该项目中。</span><span class="sxs-lookup"><span data-stu-id="a03fc-183">You must select the StoreApp.Tests project to add the packages to that project.</span></span>

![管理包](unit-testing-with-aspnet-web-api/_static/image8.png)

<span data-ttu-id="a03fc-185">查找并安装 Microsoft ASP.NET Web API 2 核心包。</span><span class="sxs-lookup"><span data-stu-id="a03fc-185">Find and install Microsoft ASP.NET Web API 2 Core package.</span></span>

![安装 web api 核心包](unit-testing-with-aspnet-web-api/_static/image9.png)

<span data-ttu-id="a03fc-187">关闭 "管理 NuGet 包" 窗口。</span><span class="sxs-lookup"><span data-stu-id="a03fc-187">Close the Manage NuGet Packages window.</span></span>

<a id="tests"></a>
## <a name="create-tests"></a><span data-ttu-id="a03fc-188">创建测试</span><span class="sxs-lookup"><span data-stu-id="a03fc-188">Create tests</span></span>

<span data-ttu-id="a03fc-189">默认情况下，你的测试项目包含一个名为 UnitTest1.cs 的空测试文件。</span><span class="sxs-lookup"><span data-stu-id="a03fc-189">By default, your test project includes an empty test file named UnitTest1.cs.</span></span> <span data-ttu-id="a03fc-190">此文件显示用于创建测试方法的属性。</span><span class="sxs-lookup"><span data-stu-id="a03fc-190">This file shows the attributes you use to create test methods.</span></span> <span data-ttu-id="a03fc-191">对于单元测试，可以使用此文件，也可以创建自己的文件。</span><span class="sxs-lookup"><span data-stu-id="a03fc-191">For your unit tests, you can either use this file or create your own file.</span></span>

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

<span data-ttu-id="a03fc-193">在本教程中，您将创建自己的测试类。</span><span class="sxs-lookup"><span data-stu-id="a03fc-193">For this tutorial, you will create your own test class.</span></span> <span data-ttu-id="a03fc-194">你可以删除 UnitTest1.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="a03fc-194">You can delete the UnitTest1.cs file.</span></span> <span data-ttu-id="a03fc-195">添加一个名为**TestSimpleProductController.cs**的类，并将代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="a03fc-195">Add a class named **TestSimpleProductController.cs**, and replace the code with the following code.</span></span>

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a><span data-ttu-id="a03fc-196">运行测试</span><span class="sxs-lookup"><span data-stu-id="a03fc-196">Run tests</span></span>

<span data-ttu-id="a03fc-197">你现在已准备好运行测试。</span><span class="sxs-lookup"><span data-stu-id="a03fc-197">You are now ready to run the tests.</span></span> <span data-ttu-id="a03fc-198">将测试标记为**TestMethod**属性的所有方法。</span><span class="sxs-lookup"><span data-stu-id="a03fc-198">All of the method that are marked with the **TestMethod** attribute will be tested.</span></span> <span data-ttu-id="a03fc-199">从 "**测试**" 菜单项中，运行测试。</span><span class="sxs-lookup"><span data-stu-id="a03fc-199">From the **Test** menu item, run the tests.</span></span>

![运行测试](unit-testing-with-aspnet-web-api/_static/image11.png)

<span data-ttu-id="a03fc-201">打开 "**测试资源管理器**" 窗口，并注意测试的结果。</span><span class="sxs-lookup"><span data-stu-id="a03fc-201">Open the **Test Explorer** window, and notice the results of the tests.</span></span>

![测试结果](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a><span data-ttu-id="a03fc-203">摘要</span><span class="sxs-lookup"><span data-stu-id="a03fc-203">Summary</span></span>

<span data-ttu-id="a03fc-204">您已完成本教程的学习。</span><span class="sxs-lookup"><span data-stu-id="a03fc-204">You have completed this tutorial.</span></span> <span data-ttu-id="a03fc-205">本教程中的数据特意进行了简化，以专注于单元测试情况。</span><span class="sxs-lookup"><span data-stu-id="a03fc-205">The data in this tutorial was intentionally simplified to focus on unit testing conditions.</span></span> <span data-ttu-id="a03fc-206">有关更高级数据方案的单元测试，请参阅[单元测试 ASP.NET Web API 2 时的模拟实体框架](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)。</span><span class="sxs-lookup"><span data-stu-id="a03fc-206">For unit testing more advanced data scenarios, see [Mocking Entity Framework when Unit Testing ASP.NET Web API 2](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).</span></span>
