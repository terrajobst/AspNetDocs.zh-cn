---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013 中的 ASP.NET 基架 |Microsoft Docs
author: Rick-Anderson
description: ASP.NET 基架是 Visual Studio 2013 中包含的一项新功能。
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449564"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a><span data-ttu-id="9e35c-103">Visual Studio 2013 中的 ASP.NET 基架</span><span class="sxs-lookup"><span data-stu-id="9e35c-103">ASP.NET Scaffolding in Visual Studio 2013</span></span>

<span data-ttu-id="9e35c-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9e35c-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9e35c-105">ASP.NET 基架是 Visual Studio 2013 中包含的一项新功能。</span><span class="sxs-lookup"><span data-stu-id="9e35c-105">ASP.NET Scaffolding is a new feature that is included in Visual Studio 2013.</span></span>

## <a name="overview"></a><span data-ttu-id="9e35c-106">概述</span><span class="sxs-lookup"><span data-stu-id="9e35c-106">Overview</span></span>

<span data-ttu-id="9e35c-107">ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。</span><span class="sxs-lookup"><span data-stu-id="9e35c-107">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="9e35c-108">Visual Studio 2013 包含用于 MVC 和 Web API 项目的预安装代码生成器。</span><span class="sxs-lookup"><span data-stu-id="9e35c-108">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="9e35c-109">若要快速添加与数据模型交互的代码，请将基架添加到项目。</span><span class="sxs-lookup"><span data-stu-id="9e35c-109">You add scaffolding to your project when you want to quickly add code that interacts with data models.</span></span> <span data-ttu-id="9e35c-110">使用基架可以减少在项目中开发标准数据操作所需的时间。</span><span class="sxs-lookup"><span data-stu-id="9e35c-110">Using scaffolding can reduce the amount of time to develop standard data operations in your project.</span></span>

<span data-ttu-id="9e35c-111">默认情况下，Visual Studio 2013 不支持为 Web 窗体项目生成代码，但你可以通过将 MVC 依赖项添加到项目或安装扩展，将基架与 Web 窗体一起使用。</span><span class="sxs-lookup"><span data-stu-id="9e35c-111">By default, Visual Studio 2013 does not support generating code for a Web Forms project, but you can use scaffolding with Web Forms by either adding MVC dependencies to the project or installing an extension.</span></span> <span data-ttu-id="9e35c-112">下面显示了这两种方法。</span><span class="sxs-lookup"><span data-stu-id="9e35c-112">Both approaches are shown below.</span></span>

<span data-ttu-id="9e35c-113">Visual Studio 2013 Update 2 （当前 RC）提供了扩展 ASP.NET 基架以满足方案要求的功能。</span><span class="sxs-lookup"><span data-stu-id="9e35c-113">Visual Studio 2013 Update 2 (currently RC) provides the ability to extend ASP.NET Scaffolding to meet the requirements of your scenario.</span></span> <span data-ttu-id="9e35c-114">利用此功能，你可以创建一个自定义的基架模板并将其添加到 "添加新基架" 对话框。</span><span class="sxs-lookup"><span data-stu-id="9e35c-114">With this functionality, you can create a customized scaffolding template and add it to Add New Scaffold dialog.</span></span> <span data-ttu-id="9e35c-115">在自定义模板中，指定添加基架项时生成的代码。</span><span class="sxs-lookup"><span data-stu-id="9e35c-115">Within the customized template, you specify the code that is generated when adding a scaffolded item.</span></span> <span data-ttu-id="9e35c-116">有关详细信息，请参阅[创建自定义 Scaffolder For Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029)。</span><span class="sxs-lookup"><span data-stu-id="9e35c-116">For more information, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e35c-117">系统必备</span><span class="sxs-lookup"><span data-stu-id="9e35c-117">Prerequisites</span></span>

<span data-ttu-id="9e35c-118">若要使用 ASP.NET 基架，必须具备：</span><span class="sxs-lookup"><span data-stu-id="9e35c-118">To use ASP.NET Scaffolding, you must have:</span></span>

- <span data-ttu-id="9e35c-119">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="9e35c-119">Microsoft Visual Studio 2013</span></span>
- <span data-ttu-id="9e35c-120">Web 开发人员工具（默认 Visual Studio 2013 安装的一部分）</span><span class="sxs-lookup"><span data-stu-id="9e35c-120">Web Developer Tools (part of default Visual Studio 2013 installation)</span></span>
- <span data-ttu-id="9e35c-121">ASP.NET Web 框架和工具2013（默认 Visual Studio 2013 安装的一部分）</span><span class="sxs-lookup"><span data-stu-id="9e35c-121">ASP.NET Web Frameworks and Tools 2013 (part of default Visual Studio 2013 installation)</span></span>

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a><span data-ttu-id="9e35c-122">将基架项添加到 MVC 或 Web API</span><span class="sxs-lookup"><span data-stu-id="9e35c-122">Add a scaffolded item to MVC or Web API</span></span>

<span data-ttu-id="9e35c-123">若要添加基架，请右键单击项目或项目中的文件夹，然后选择 "**添加**-**新建基架项**"，如下图所示。</span><span class="sxs-lookup"><span data-stu-id="9e35c-123">To add a scaffold, right-click either the project or a folder within the project, and select **Add** – **New Scaffolded Item**, as shown in the following image.</span></span>

![添加基架项](aspnet-scaffolding-overview/_static/image1.png)

<span data-ttu-id="9e35c-125">从 "**添加基架**" 窗口中，选择要添加的基架类型。</span><span class="sxs-lookup"><span data-stu-id="9e35c-125">From the **Add Scaffold** window, select the type of scaffold to add.</span></span>

![选择基架的类型](aspnet-scaffolding-overview/_static/image2.png)

<span data-ttu-id="9e35c-127">"**添加控制器**" 窗口可让你选择用于生成控制器的选项，包括是否要使用实体框架6中的新异步功能。</span><span class="sxs-lookup"><span data-stu-id="9e35c-127">The **Add Controller** window gives you the opportunity to select options for generating the controller, including whether you want to use the new async features from Entity Framework 6.</span></span>

![添加控制器](aspnet-scaffolding-overview/_static/image3.png)

<span data-ttu-id="9e35c-129">将为你的方案创建相关的类和页。</span><span class="sxs-lookup"><span data-stu-id="9e35c-129">The relevant classes and pages are created for your scenario.</span></span> <span data-ttu-id="9e35c-130">例如，下图显示了通过基架为名为电影的模型类创建的 MVC 控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="9e35c-130">For example, the following image shows the MVC controller and views that were created through scaffolding for a model class named Movies.</span></span>

![创建的文件](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a><span data-ttu-id="9e35c-132">将基架项添加到 Web 窗体</span><span class="sxs-lookup"><span data-stu-id="9e35c-132">Add a scaffolded item to Web Forms</span></span>

<span data-ttu-id="9e35c-133">若要添加生成 Web 窗体代码的基架，你必须安装 Visual Studio 的扩展或添加 MVC 依赖项。</span><span class="sxs-lookup"><span data-stu-id="9e35c-133">To add scaffolding that generates Web Forms code, you must either install an extension to Visual Studio or add MVC dependencies.</span></span> <span data-ttu-id="9e35c-134">下面显示了这两种方法，但只需执行这些方法之一。</span><span class="sxs-lookup"><span data-stu-id="9e35c-134">Both approaches are shown below, but you only need to do one of these approaches.</span></span>

### <a name="web-forms-scaffolding-extension"></a><span data-ttu-id="9e35c-135">Web 窗体基架扩展</span><span class="sxs-lookup"><span data-stu-id="9e35c-135">Web Forms Scaffolding Extension</span></span>

<span data-ttu-id="9e35c-136">可以安装 Visual Studio 扩展，使你能够将基架用于 Web 窗体项目。</span><span class="sxs-lookup"><span data-stu-id="9e35c-136">You can install a Visual Studio extension that enable you to use scaffolding with a Web Forms project.</span></span> <span data-ttu-id="9e35c-137">在 Visual Studio 中，依次选择 "**工具**" 和 "**扩展和更新**"。</span><span class="sxs-lookup"><span data-stu-id="9e35c-137">In Visual Studio, select **Tools** and then **Extensions and Updates**.</span></span> <span data-ttu-id="9e35c-138">从此对话框中，在 Visual Studio 库中搜索**Web 窗体基架**。</span><span class="sxs-lookup"><span data-stu-id="9e35c-138">From this dialog search the Visual Studio Gallery for **Web Forms Scaffolding**.</span></span>

![安装 web 窗体基架](aspnet-scaffolding-overview/_static/image5.png)

<span data-ttu-id="9e35c-140">有关详细信息，请参阅[Web 窗体基架](https://go.microsoft.com/fwlink/p/?LinkId=396478)。</span><span class="sxs-lookup"><span data-stu-id="9e35c-140">For more information, see [Web Forms Scaffolding](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span></span>

### <a name="mvc-dependencies"></a><span data-ttu-id="9e35c-141">MVC 依赖项</span><span class="sxs-lookup"><span data-stu-id="9e35c-141">MVC Dependencies</span></span>

<span data-ttu-id="9e35c-142">若要添加 MVC 依赖项，请选择 "**添加** - **新基架项**"。</span><span class="sxs-lookup"><span data-stu-id="9e35c-142">To add MVC dependencies, select **Add** - **New Scaffolded Item**.</span></span> <span data-ttu-id="9e35c-143">在 "添加基架" 窗口中，选择 " **MVC 依赖项**"，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9e35c-143">In the Add Scaffold window, select **MVC Dependencies**, as shown below.</span></span>

![添加 MVC 依赖项](aspnet-scaffolding-overview/_static/image6.png)

<span data-ttu-id="9e35c-145">基架 MVC 有两个选项：最小和完整。</span><span class="sxs-lookup"><span data-stu-id="9e35c-145">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="9e35c-146">如果选择 "最小"，则只会将 NuGet 包和 ASP.NET MVC 的引用添加到你的项目中。</span><span class="sxs-lookup"><span data-stu-id="9e35c-146">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="9e35c-147">如果选择 "完全" 选项，则会添加最小依赖项，以及 MVC 项目所需的内容文件。</span><span class="sxs-lookup"><span data-stu-id="9e35c-147">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span> <span data-ttu-id="9e35c-148">若要轻松使用基架，请选择 "完全依赖项"。</span><span class="sxs-lookup"><span data-stu-id="9e35c-148">To easily use scaffolding, select Full dependencies.</span></span>

![选择完全依赖项](aspnet-scaffolding-overview/_static/image7.png)

<span data-ttu-id="9e35c-150">添加依赖项后，你将看到 readme.txt**文件。**</span><span class="sxs-lookup"><span data-stu-id="9e35c-150">After adding the dependencies, you will see a **readme.txt** file.</span></span> <span data-ttu-id="9e35c-151">仔细按照此文件中的说明进行操作，以确保您的项目正常工作。</span><span class="sxs-lookup"><span data-stu-id="9e35c-151">Carefully follow the instructions in this file to ensure that your project works correctly.</span></span>

<span data-ttu-id="9e35c-152">完成 readme.txt 文件中的步骤后，可以添加新的基架项，如上一部分有关 MVC 和 Web API 的内容所示。</span><span class="sxs-lookup"><span data-stu-id="9e35c-152">When you have completed the steps in the readme.txt file, you can add a new scaffolded item as shown in the previous section about MVC and Web API.</span></span> <span data-ttu-id="9e35c-153">自动生成的视图和控制器将在你的项目中正确运行。</span><span class="sxs-lookup"><span data-stu-id="9e35c-153">The automatically-generated views and controller will function correctly within your project.</span></span>

## <a name="tutorials"></a><span data-ttu-id="9e35c-154">教程</span><span class="sxs-lookup"><span data-stu-id="9e35c-154">Tutorials</span></span>

<span data-ttu-id="9e35c-155">若要创建自定义的 scaffolder，请参阅[为 Visual Studio 创建自定义 scaffolder](https://go.microsoft.com/fwlink/p/?LinkId=395029)。</span><span class="sxs-lookup"><span data-stu-id="9e35c-155">To create a customized scaffolder, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

<span data-ttu-id="9e35c-156">若要自定义生成的文件，请参阅[如何自定义 "新建基架项" 对话框中生成的文件](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)。</span><span class="sxs-lookup"><span data-stu-id="9e35c-156">To customize the generated files, see [How to customize the generated files from the New Scaffolded Item dialog](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span></span>

<span data-ttu-id="9e35c-157">有关将基架与**Database First 开发**结合使用的示例，请参阅[使用 ASP.NET MVC Database First EF](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)。</span><span class="sxs-lookup"><span data-stu-id="9e35c-157">For an example of using scaffolding with **Database First development**, see [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span></span>

<span data-ttu-id="9e35c-158">有关在**MVC**项目中使用基架的示例，请参阅[与 ASP.NET MVC 5 入门](../../../mvc/overview/getting-started/introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="9e35c-158">For an example of using scaffolding in an **MVC** project, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="9e35c-159">有关在**WEB api**项目中使用基架的示例，请参阅使用[web api 2 中的属性路由创建 REST API](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="9e35c-159">For an example of using scaffolding in a **Web API** project, see [Create a REST API with Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span></span>
