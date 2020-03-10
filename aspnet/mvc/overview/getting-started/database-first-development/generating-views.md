---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 教程：通过 ASP.NET MVC 应用生成 EF Database First 视图
description: 本教程重点介绍如何使用 ASP.NET 基架生成控制器和视图。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499472"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="a447b-103">教程：通过 ASP.NET MVC 应用生成 EF Database First 视图</span><span class="sxs-lookup"><span data-stu-id="a447b-103">Tutorial: Generate views for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="a447b-104">使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。</span><span class="sxs-lookup"><span data-stu-id="a447b-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="a447b-105">本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。</span><span class="sxs-lookup"><span data-stu-id="a447b-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="a447b-106">生成的代码与数据库表中的列相对应。</span><span class="sxs-lookup"><span data-stu-id="a447b-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="a447b-107">本教程重点介绍如何使用 ASP.NET 基架生成控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="a447b-107">This tutorial focuses on using ASP.NET Scaffolding to generate the controllers and views.</span></span>

<span data-ttu-id="a447b-108">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="a447b-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a447b-109">添加基架</span><span class="sxs-lookup"><span data-stu-id="a447b-109">Add scaffold</span></span>
> * <span data-ttu-id="a447b-110">将链接添加到新视图</span><span class="sxs-lookup"><span data-stu-id="a447b-110">Add links to new views</span></span>
> * <span data-ttu-id="a447b-111">显示学生视图</span><span class="sxs-lookup"><span data-stu-id="a447b-111">Display student views</span></span>
> * <span data-ttu-id="a447b-112">显示注册视图</span><span class="sxs-lookup"><span data-stu-id="a447b-112">Display enrollment views</span></span>

## <a name="prerequisite"></a><span data-ttu-id="a447b-113">必备组件</span><span class="sxs-lookup"><span data-stu-id="a447b-113">Prerequisite</span></span>

* [<span data-ttu-id="a447b-114">创建 web 应用程序和数据模型</span><span class="sxs-lookup"><span data-stu-id="a447b-114">Create the web application and data models</span></span>](creating-the-web-application.md)

## <a name="add-scaffold"></a><span data-ttu-id="a447b-115">添加基架</span><span class="sxs-lookup"><span data-stu-id="a447b-115">Add scaffold</span></span>

<span data-ttu-id="a447b-116">你已准备好生成代码，该代码将为模型类提供标准数据操作。</span><span class="sxs-lookup"><span data-stu-id="a447b-116">You are ready to generate code that will provide standard data operations for the model classes.</span></span> <span data-ttu-id="a447b-117">添加基架项即可添加代码。</span><span class="sxs-lookup"><span data-stu-id="a447b-117">You add the code by adding a scaffold item.</span></span> <span data-ttu-id="a447b-118">可以添加的基架类型有很多选项;在本教程中，基架将包含与上一节中创建的学生和注册模型相对应的控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="a447b-118">There are many options for the type of scaffolding you can add; in this tutorial, the scaffold will include a controller and views that correspond to the Student and Enrollment models you created in the previous section.</span></span>

<span data-ttu-id="a447b-119">若要在项目中保持一致性，请将新的控制器添加到 "现有**控制器**" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="a447b-119">To maintain consistency in your project, you will add the new controller to the existing **Controllers** folder.</span></span> <span data-ttu-id="a447b-120">右键单击 "**控制器**" 文件夹，然后选择 "**添加** > **新的基架项**"。</span><span class="sxs-lookup"><span data-stu-id="a447b-120">Right-click the **Controllers** folder, and select **Add** > **New Scaffolded Item**.</span></span>

<span data-ttu-id="a447b-121">**使用 "实体框架" 选项，选择 "包含视图的 MVC 5 控制器"** 。</span><span class="sxs-lookup"><span data-stu-id="a447b-121">Select the **MVC 5 Controller with views, using Entity Framework** option.</span></span> <span data-ttu-id="a447b-122">此选项将生成控制器和视图，用于更新、删除、创建和显示模型中的数据。</span><span class="sxs-lookup"><span data-stu-id="a447b-122">This option will generate the controller and views for updating, deleting, creating and displaying the data in your model.</span></span>

![添加 mvc 控制器](generating-views/_static/image2.png)

<span data-ttu-id="a447b-124">选择 "ContosoSite" 作为模型类的 "**学生（）** "，然后选择 "上下文" 类的**ContosoUniversityDataEntities （ContosoSite）** 。</span><span class="sxs-lookup"><span data-stu-id="a447b-124">Select **Student (ContosoSite.Models)** for the model class and select the **ContosoUniversityDataEntities (ContosoSite.Models)** for the context class.</span></span> <span data-ttu-id="a447b-125">将控制器名称保留为**StudentsController**。</span><span class="sxs-lookup"><span data-stu-id="a447b-125">Keep the controller name as **StudentsController**.</span></span>

<span data-ttu-id="a447b-126">单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="a447b-126">Click **Add**.</span></span>

<span data-ttu-id="a447b-127">如果收到错误，则可能是因为你在上一节中未生成项目。</span><span class="sxs-lookup"><span data-stu-id="a447b-127">If you receive an error, it may be because you did not build the project in the previous section.</span></span> <span data-ttu-id="a447b-128">如果是这样，请尝试生成该项目，然后再次添加基架项。</span><span class="sxs-lookup"><span data-stu-id="a447b-128">If so, try building the project, and then add the scaffolded item again.</span></span>

<span data-ttu-id="a447b-129">代码生成过程完成后，你将在项目的**控制器**中看到一个新的控制器和\*\*视图，并 > \*\* **学生**文件夹中查看。</span><span class="sxs-lookup"><span data-stu-id="a447b-129">After the code generation process is complete, you will see a new controller and views in your project's **Controllers** and **Views** > **Students** folders.</span></span>

<span data-ttu-id="a447b-130">再次执行相同的步骤，但为**注册**类添加基架。</span><span class="sxs-lookup"><span data-stu-id="a447b-130">Perform the same steps again, but add a scaffold for the **Enrollment** class.</span></span> <span data-ttu-id="a447b-131">完成后，你将拥有一个**EnrollmentsController.cs**文件，并使用创建、删除、详细信息、编辑和索引视图在名为 "**注册**" 的**视图**下创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="a447b-131">When finished, you have an **EnrollmentsController.cs** file, and a folder under **Views** named **Enrollments** with the Create, Delete, Details, Edit and Index views.</span></span>

## <a name="add-links-to-new-views"></a><span data-ttu-id="a447b-132">将链接添加到新视图</span><span class="sxs-lookup"><span data-stu-id="a447b-132">Add links to new views</span></span>

<span data-ttu-id="a447b-133">为了更轻松地导航到新视图，您可以向学生和注册的索引视图添加几个超链接。</span><span class="sxs-lookup"><span data-stu-id="a447b-133">To make it easier for you to navigate to your new views, you can add a couple of hyperlinks to the Index views for students and enrollments.</span></span> <span data-ttu-id="a447b-134">在 > **home** > 的**视图**中打开文件，该文件是你的网站的*主页。*</span><span class="sxs-lookup"><span data-stu-id="a447b-134">Open the file at **Views** > **Home** > *Index.cshtml*, which is the home page for your site.</span></span> <span data-ttu-id="a447b-135">在 jumbotron 下面添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="a447b-135">Add the following code below the jumbotron.</span></span>

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

<span data-ttu-id="a447b-136">对于 Html.actionlink 方法，第一个参数是要在链接中显示的文本。</span><span class="sxs-lookup"><span data-stu-id="a447b-136">For the ActionLink method, the first parameter is the text to display in the link.</span></span> <span data-ttu-id="a447b-137">第二个参数是操作，第三个参数是控制器的名称。</span><span class="sxs-lookup"><span data-stu-id="a447b-137">The second parameter is the action and the third parameter is the name of the controller.</span></span> <span data-ttu-id="a447b-138">例如，第一个链接指向 StudentsController 中的 Index 操作。</span><span class="sxs-lookup"><span data-stu-id="a447b-138">For example, the first link points to the Index action in StudentsController.</span></span> <span data-ttu-id="a447b-139">实际的超链接是根据这些值构造的。</span><span class="sxs-lookup"><span data-stu-id="a447b-139">The actual hyperlink is constructed from these values.</span></span> <span data-ttu-id="a447b-140">第一个链接最终将用户转到 "**视图/学生**" 文件夹内的**索引 cshtml**文件。</span><span class="sxs-lookup"><span data-stu-id="a447b-140">The first link ultimately takes users to the **Index.cshtml** file within the **Views/Students** folder.</span></span>

## <a name="display-student-views"></a><span data-ttu-id="a447b-141">显示学生视图</span><span class="sxs-lookup"><span data-stu-id="a447b-141">Display student views</span></span>

<span data-ttu-id="a447b-142">你将验证添加到你的项目的代码是否正确显示了学生列表，并使用户能够在数据库中编辑、创建或删除学生记录。</span><span class="sxs-lookup"><span data-stu-id="a447b-142">You will verify that the code added to your project correctly displays a list of the students, and enables users to edit, create, or delete the student records in the database.</span></span>

<span data-ttu-id="a447b-143">右键单击 > **Home** > \*索引的\***视图**文件，然后选择 "**在浏览器中查看**"。</span><span class="sxs-lookup"><span data-stu-id="a447b-143">Right-click the **Views** > **Home** > *Index.cshtml* file, and select **View in Browser**.</span></span> <span data-ttu-id="a447b-144">在应用程序主页上，选择 "**学生列表**"。</span><span class="sxs-lookup"><span data-stu-id="a447b-144">On the application home page, select **List of students**.</span></span>

![](generating-views/_static/image6.png)

<span data-ttu-id="a447b-145">在 "**索引**" 页上，请注意学生列表和修改此数据的链接。</span><span class="sxs-lookup"><span data-stu-id="a447b-145">On the **Index** page, notice the list of the students and links to modify this data.</span></span> <span data-ttu-id="a447b-146">选择 "**新建**" 链接，并为新学生提供一些值。</span><span class="sxs-lookup"><span data-stu-id="a447b-146">Select the **Create New** link and provide some values for a new student.</span></span> <span data-ttu-id="a447b-147">单击 "**创建**"，并注意将新的学生添加到列表。</span><span class="sxs-lookup"><span data-stu-id="a447b-147">Click **Create**, and notice the new student is added to your list.</span></span>

<span data-ttu-id="a447b-148">返回到 "**索引**" 页，选择 "**编辑**" 链接，然后更改学生的某些值。</span><span class="sxs-lookup"><span data-stu-id="a447b-148">Back on the **Index** page, select the **Edit** link, and change some of the values for a student.</span></span> <span data-ttu-id="a447b-149">单击 "**保存**"，并注意学生记录已更改。</span><span class="sxs-lookup"><span data-stu-id="a447b-149">Click **Save**, and notice the student record has been changed.</span></span>

<span data-ttu-id="a447b-150">最后，选择 "**删除**" 链接，并通过单击 "**删除**" 按钮确认是否要删除该记录。</span><span class="sxs-lookup"><span data-stu-id="a447b-150">Finally, select the **Delete** link and confirm that you want to delete the record by clicking the **Delete** button.</span></span>

<span data-ttu-id="a447b-151">在不编写任何代码的情况下，你添加了对 "学生" 表中的数据执行常见操作的视图。</span><span class="sxs-lookup"><span data-stu-id="a447b-151">Without writing any code, you have added views that perform common operations on the data in the Student table.</span></span>

<span data-ttu-id="a447b-152">您可能已注意到，字段的文本标签基于数据库属性（如**LastName**），这并不一定是您想要在网页上显示的内容。</span><span class="sxs-lookup"><span data-stu-id="a447b-152">You may have noticed that the text label for a field is based on the database property (such as **LastName**) which is not necessarily what you want to display on the web page.</span></span> <span data-ttu-id="a447b-153">例如，您可能希望标签为 "**姓氏**"。</span><span class="sxs-lookup"><span data-stu-id="a447b-153">For example, you may prefer the label to be **Last Name**.</span></span> <span data-ttu-id="a447b-154">你将在本教程的后面部分修复此显示问题。</span><span class="sxs-lookup"><span data-stu-id="a447b-154">You will fix this display issue later in the tutorial.</span></span>

## <a name="display-enrollment-views"></a><span data-ttu-id="a447b-155">显示注册视图</span><span class="sxs-lookup"><span data-stu-id="a447b-155">Display enrollment views</span></span>

<span data-ttu-id="a447b-156">您的数据库包含学生和注册表之间的一对多关系，以及课程表和注册表之间的一对多关系。</span><span class="sxs-lookup"><span data-stu-id="a447b-156">Your database includes a one-to-many relationship between the Student and Enrollment tables, and a one-to-many relationship between the Course and Enrollment tables.</span></span> <span data-ttu-id="a447b-157">注册的视图会正确地处理这些关系。</span><span class="sxs-lookup"><span data-stu-id="a447b-157">The views for Enrollment correctly handle these relationships.</span></span> <span data-ttu-id="a447b-158">导航到网站的主页并选择 "注册" 链接**列表**，然后选择 "**创建新**链接"。</span><span class="sxs-lookup"><span data-stu-id="a447b-158">Navigate to the home page for your site and select the **List of enrollments** link and then the **Create New** link.</span></span>

<span data-ttu-id="a447b-159">此视图显示用于创建新注册记录的窗体。</span><span class="sxs-lookup"><span data-stu-id="a447b-159">The view displays a form for creating a new enrollment record.</span></span> <span data-ttu-id="a447b-160">特别要注意的是，该窗体包含**CourseID**下拉列表和**StudentID**下拉列表。</span><span class="sxs-lookup"><span data-stu-id="a447b-160">In particular, notice that the form contains a **CourseID** drop-down list and a **StudentID** drop-down list.</span></span> <span data-ttu-id="a447b-161">两者都用相关表中的值填充。</span><span class="sxs-lookup"><span data-stu-id="a447b-161">Both are populated with values from the related tables.</span></span>

<span data-ttu-id="a447b-162">此外，系统会根据字段的数据类型自动应用对提供值的验证。</span><span class="sxs-lookup"><span data-stu-id="a447b-162">Furthermore, validation of the provided values is automatically applied based on the data type of the field.</span></span> <span data-ttu-id="a447b-163">**评分**要求数字，因此如果您尝试提供不兼容的值，将显示一条错误消息：*字段级别必须为数字。*</span><span class="sxs-lookup"><span data-stu-id="a447b-163">**Grade** requires a number, so an error message is displayed if you try to provide an incompatible value: *The field Grade must be a number.*</span></span>

<span data-ttu-id="a447b-164">您已经验证了自动生成的视图使用户能够处理数据库中的数据。</span><span class="sxs-lookup"><span data-stu-id="a447b-164">You have verified that the automatically-generated views enable users to work with the data in the database.</span></span> <span data-ttu-id="a447b-165">在本系列的下一个教程中，您将更新数据库，并在 web 应用程序中进行相应的更改。</span><span class="sxs-lookup"><span data-stu-id="a447b-165">In the next tutorial in this series, you will update the database and make the corresponding changes in the web application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a447b-166">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a447b-166">Next steps</span></span>

<span data-ttu-id="a447b-167">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="a447b-167">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a447b-168">添加的基架</span><span class="sxs-lookup"><span data-stu-id="a447b-168">Added scaffold</span></span>
> * <span data-ttu-id="a447b-169">添加了到新视图的链接</span><span class="sxs-lookup"><span data-stu-id="a447b-169">Added links to new views</span></span>
> * <span data-ttu-id="a447b-170">显示的学生视图</span><span class="sxs-lookup"><span data-stu-id="a447b-170">Displayed student views</span></span>
> * <span data-ttu-id="a447b-171">显示的注册视图</span><span class="sxs-lookup"><span data-stu-id="a447b-171">Displayed enrollment views</span></span>

<span data-ttu-id="a447b-172">转到下一教程，了解如何更改数据库。</span><span class="sxs-lookup"><span data-stu-id="a447b-172">Advance to the next tutorial to learn how to change the database.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a447b-173">更改数据库</span><span class="sxs-lookup"><span data-stu-id="a447b-173">Change the database</span></span>](changing-the-database.md)