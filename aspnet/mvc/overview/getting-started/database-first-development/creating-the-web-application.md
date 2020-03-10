---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 教程：创建 Web 应用程序和数据模型用于 EF Database First 与 ASP.NET MVC
description: 本教程重点介绍如何创建 web 应用程序，以及如何基于数据库表生成数据模型。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499526"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="ced42-103">教程：创建 Web 应用程序和数据模型用于 EF Database First 与 ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="ced42-103">Tutorial: Create the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="ced42-104">使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。</span><span class="sxs-lookup"><span data-stu-id="ced42-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="ced42-105">本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。</span><span class="sxs-lookup"><span data-stu-id="ced42-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="ced42-106">生成的代码与数据库表中的列相对应。</span><span class="sxs-lookup"><span data-stu-id="ced42-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="ced42-107">本教程重点介绍如何创建 web 应用程序，以及如何基于数据库表生成数据模型。</span><span class="sxs-lookup"><span data-stu-id="ced42-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="ced42-108">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="ced42-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ced42-109">创建 ASP.NET Web 应用</span><span class="sxs-lookup"><span data-stu-id="ced42-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="ced42-110">生成模型</span><span class="sxs-lookup"><span data-stu-id="ced42-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ced42-111">系统必备</span><span class="sxs-lookup"><span data-stu-id="ced42-111">Prerequisites</span></span>

* [<span data-ttu-id="ced42-112">使用 MVC 5 Database First 实体框架6入门</span><span class="sxs-lookup"><span data-stu-id="ced42-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="ced42-113">创建 ASP.NET Web 应用</span><span class="sxs-lookup"><span data-stu-id="ced42-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="ced42-114">在新解决方案或与数据库项目相同的解决方案中，在 Visual Studio 中创建一个新项目，然后选择 " **ASP.NET Web 应用程序**" 模板。</span><span class="sxs-lookup"><span data-stu-id="ced42-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="ced42-115">将项目命名为**ContosoSite**。</span><span class="sxs-lookup"><span data-stu-id="ced42-115">Name the project **ContosoSite**.</span></span>

![创建项目](creating-the-web-application/_static/image1.png)

<span data-ttu-id="ced42-117">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="ced42-117">Click **OK**.</span></span>

<span data-ttu-id="ced42-118">在 "新建 ASP.NET 项目" 窗口中，选择 " **MVC** " 模板。</span><span class="sxs-lookup"><span data-stu-id="ced42-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="ced42-119">你现在可以**在云中选项中清除主机**，因为你稍后会将该应用程序部署到云。</span><span class="sxs-lookup"><span data-stu-id="ced42-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="ced42-120">单击 **"确定"** 以创建该应用程序。</span><span class="sxs-lookup"><span data-stu-id="ced42-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="ced42-121">项目是用默认文件和文件夹创建的。</span><span class="sxs-lookup"><span data-stu-id="ced42-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="ced42-122">在本教程中，您将使用实体框架6。</span><span class="sxs-lookup"><span data-stu-id="ced42-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="ced42-123">可以通过 "管理 NuGet 包" 窗口，仔细检查项目中实体框架的版本。</span><span class="sxs-lookup"><span data-stu-id="ced42-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="ced42-124">如有必要，请更新实体框架的版本。</span><span class="sxs-lookup"><span data-stu-id="ced42-124">If necessary, update your version of Entity Framework.</span></span>

![显示版本](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="ced42-126">生成模型</span><span class="sxs-lookup"><span data-stu-id="ced42-126">Generate the models</span></span>

<span data-ttu-id="ced42-127">现在，您将从数据库表创建实体框架模型。</span><span class="sxs-lookup"><span data-stu-id="ced42-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="ced42-128">这些模型是将用于处理数据的类。</span><span class="sxs-lookup"><span data-stu-id="ced42-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="ced42-129">每个模型镜像数据库中的一个表，并包含与表中的列相对应的属性。</span><span class="sxs-lookup"><span data-stu-id="ced42-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="ced42-130">右键单击 "**模型**" 文件夹，然后选择 "**添加**" 和 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="ced42-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="ced42-131">在 "添加新项" 窗口中，选择左窗格中的 "**数据**"，并从中间窗格的选项中**ADO.NET 实体数据模型**。</span><span class="sxs-lookup"><span data-stu-id="ced42-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="ced42-132">将新的模型文件命名为**ContosoModel**。</span><span class="sxs-lookup"><span data-stu-id="ced42-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="ced42-133">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="ced42-133">Click **Add**.</span></span>

<span data-ttu-id="ced42-134">在实体数据模型向导中，选择 "**从数据库中选择 EF 设计器**"。</span><span class="sxs-lookup"><span data-stu-id="ced42-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="ced42-135">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="ced42-135">Click **Next**.</span></span>

<span data-ttu-id="ced42-136">如果在开发环境中定义了数据库连接，则可能会看到预先选择了这些连接之一。</span><span class="sxs-lookup"><span data-stu-id="ced42-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="ced42-137">但是，您希望创建一个与您在本教程第一部分中创建的数据库的新连接。</span><span class="sxs-lookup"><span data-stu-id="ced42-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="ced42-138">单击 "**新建连接**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="ced42-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="ced42-139">在 "连接属性窗口中，提供创建数据库的本地服务器的名称（在本例中为" **（localdb） \ProjectsV13**） "。</span><span class="sxs-lookup"><span data-stu-id="ced42-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="ced42-140">提供服务器名称后，从可用数据库中选择 "ContosoUniversityData"。</span><span class="sxs-lookup"><span data-stu-id="ced42-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![设置连接属性](creating-the-web-application/_static/image8.png)

<span data-ttu-id="ced42-142">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="ced42-142">Click **OK**.</span></span>

<span data-ttu-id="ced42-143">现在会显示正确的连接属性。</span><span class="sxs-lookup"><span data-stu-id="ced42-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="ced42-144">可以在 web.config 文件中使用连接的默认名称。</span><span class="sxs-lookup"><span data-stu-id="ced42-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="ced42-145">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="ced42-145">Click **Next**.</span></span>

<span data-ttu-id="ced42-146">选择最新版本的实体框架。</span><span class="sxs-lookup"><span data-stu-id="ced42-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="ced42-147">单击 **“下一步”** 。</span><span class="sxs-lookup"><span data-stu-id="ced42-147">Click **Next**.</span></span>

<span data-ttu-id="ced42-148">选择要为所有三个表生成模型的**表**。</span><span class="sxs-lookup"><span data-stu-id="ced42-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="ced42-149">单击“完成”。</span><span class="sxs-lookup"><span data-stu-id="ced42-149">Click **Finish**.</span></span>

<span data-ttu-id="ced42-150">如果收到安全警告，请选择 **"确定"** 以继续运行模板。</span><span class="sxs-lookup"><span data-stu-id="ced42-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="ced42-151">将从数据库表中生成模型，并显示一个关系图，其中显示表之间的属性和关系。</span><span class="sxs-lookup"><span data-stu-id="ced42-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![模型示意图](creating-the-web-application/_static/image11.png)

<span data-ttu-id="ced42-153">"模型" 文件夹现在包含许多与从数据库生成的模型相关的新文件。</span><span class="sxs-lookup"><span data-stu-id="ced42-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="ced42-154">**ContosoModel.Context.cs**文件包含从**DbContext**类派生的类，并为对应于数据库表的每个模型类提供一个属性。</span><span class="sxs-lookup"><span data-stu-id="ced42-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="ced42-155">**Course.cs**、 **Enrollment.cs**和**Student.cs**文件包含表示数据库表的模型类。</span><span class="sxs-lookup"><span data-stu-id="ced42-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="ced42-156">使用基架时，将使用上下文类和模型类。</span><span class="sxs-lookup"><span data-stu-id="ced42-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="ced42-157">在继续学习本教程之前，请生成项目。</span><span class="sxs-lookup"><span data-stu-id="ced42-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="ced42-158">在下一节中，您将生成基于数据模型的代码，但如果尚未生成项目，该部分将无法工作。</span><span class="sxs-lookup"><span data-stu-id="ced42-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ced42-159">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ced42-159">Next steps</span></span>

<span data-ttu-id="ced42-160">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="ced42-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ced42-161">创建 ASP.NET web 应用</span><span class="sxs-lookup"><span data-stu-id="ced42-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="ced42-162">生成模型</span><span class="sxs-lookup"><span data-stu-id="ced42-162">Generated the models</span></span>

<span data-ttu-id="ced42-163">转到下一教程，了解如何创建基于数据模型的代码。</span><span class="sxs-lookup"><span data-stu-id="ced42-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="ced42-164">正在生成视图</span><span class="sxs-lookup"><span data-stu-id="ced42-164">Generating views</span></span>](generating-views.md)
