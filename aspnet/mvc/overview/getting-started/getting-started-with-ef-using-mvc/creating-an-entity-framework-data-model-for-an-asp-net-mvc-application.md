---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 教程：使用 MVC 5 开始使用实体框架 6 Code First |Microsoft Docs
description: 在本系列教程中，您将了解如何生成使用实体框架6进行数据访问的 ASP.NET MVC 5 应用程序。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499406"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a><span data-ttu-id="035c3-103">教程：使用 MVC 5 开始使用实体框架 6 Code First</span><span class="sxs-lookup"><span data-stu-id="035c3-103">Tutorial: Get Started with Entity Framework 6 Code First using MVC 5</span></span>

> [!NOTE]
> <span data-ttu-id="035c3-104">对于新开发，我们建议[ASP.NET Core Razor Pages](/aspnet/core/razor-pages) ASP.NET MVC 控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="035c3-104">For new development, we recommend [ASP.NET Core Razor Pages](/aspnet/core/razor-pages) over ASP.NET MVC controllers and views.</span></span> <span data-ttu-id="035c3-105">有关使用 Razor Pages 的与此类似的系列教程，请参阅[教程： ASP.NET Core 中的 Razor Pages 入门](/aspnet/core/tutorials/razor-pages/razor-pages-start)。</span><span class="sxs-lookup"><span data-stu-id="035c3-105">For a tutorial series similar to this one using Razor Pages, see [Tutorial: Get started with Razor Pages in ASP.NET Core](/aspnet/core/tutorials/razor-pages/razor-pages-start).</span></span> <span data-ttu-id="035c3-106">新教程：</span><span class="sxs-lookup"><span data-stu-id="035c3-106">The new tutorial:</span></span>
> * <span data-ttu-id="035c3-107">易于关注。</span><span class="sxs-lookup"><span data-stu-id="035c3-107">Is easier to follow.</span></span>
> * <span data-ttu-id="035c3-108">提供更多 EF Core 最佳做法。</span><span class="sxs-lookup"><span data-stu-id="035c3-108">Provides more EF Core best practices.</span></span>
> * <span data-ttu-id="035c3-109">使用更高效的查询。</span><span class="sxs-lookup"><span data-stu-id="035c3-109">Uses more efficient queries.</span></span>
> * <span data-ttu-id="035c3-110">通过最新 API 更新到更高版本。</span><span class="sxs-lookup"><span data-stu-id="035c3-110">Is more current with the latest API.</span></span>
> * <span data-ttu-id="035c3-111">涵盖更多功能。</span><span class="sxs-lookup"><span data-stu-id="035c3-111">Covers more features.</span></span>
> * <span data-ttu-id="035c3-112">是开发新应用程序的首选方法。</span><span class="sxs-lookup"><span data-stu-id="035c3-112">Is the preferred approach for new application development.</span></span>

<span data-ttu-id="035c3-113">在本系列教程中，您将了解如何生成使用实体框架6进行数据访问的 ASP.NET MVC 5 应用程序。</span><span class="sxs-lookup"><span data-stu-id="035c3-113">In this series of tutorials, you learn how to build an ASP.NET MVC 5 application that uses Entity Framework 6 for data access.</span></span> <span data-ttu-id="035c3-114">本教程使用 Code First 工作流。</span><span class="sxs-lookup"><span data-stu-id="035c3-114">This tutorial uses the Code First workflow.</span></span> <span data-ttu-id="035c3-115">有关如何在 Code First、Database First 和 Model First 之间进行选择的详细信息，请参阅[创建模型](/ef/ef6/modeling/)。</span><span class="sxs-lookup"><span data-stu-id="035c3-115">For information about how to choose between Code First, Database First, and Model First, see [Create a model](/ef/ef6/modeling/).</span></span>

<span data-ttu-id="035c3-116">本系列教程介绍了如何构建 Contoso 大学的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="035c3-116">This tutorial series explains how to build the Contoso University sample application.</span></span> <span data-ttu-id="035c3-117">该示例应用程序是一个简单的大学网站。</span><span class="sxs-lookup"><span data-stu-id="035c3-117">The sample application is a simple university website.</span></span> <span data-ttu-id="035c3-118">利用它，你可以查看和更新学生、课程和教师信息。</span><span class="sxs-lookup"><span data-stu-id="035c3-118">With it, you can view and update student, course, and instructor information.</span></span> <span data-ttu-id="035c3-119">下面是创建的两个屏幕：</span><span class="sxs-lookup"><span data-stu-id="035c3-119">Here are two of the screens you create:</span></span>

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![编辑学生](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="035c3-122">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="035c3-122">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="035c3-123">创建 MVC web 应用</span><span class="sxs-lookup"><span data-stu-id="035c3-123">Create an MVC web app</span></span>
> * <span data-ttu-id="035c3-124">设置网站样式</span><span class="sxs-lookup"><span data-stu-id="035c3-124">Set up the site style</span></span>
> * <span data-ttu-id="035c3-125">安装实体框架6</span><span class="sxs-lookup"><span data-stu-id="035c3-125">Install Entity Framework 6</span></span>
> * <span data-ttu-id="035c3-126">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="035c3-126">Create the data model</span></span>
> * <span data-ttu-id="035c3-127">创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="035c3-127">Create the database context</span></span>
> * <span data-ttu-id="035c3-128">使用测试数据初始化数据库</span><span class="sxs-lookup"><span data-stu-id="035c3-128">Initialize DB with test data</span></span>
> * <span data-ttu-id="035c3-129">设置 EF 6 以使用 LocalDB</span><span class="sxs-lookup"><span data-stu-id="035c3-129">Set up EF 6 to use LocalDB</span></span>
> * <span data-ttu-id="035c3-130">创建控制器和视图</span><span class="sxs-lookup"><span data-stu-id="035c3-130">Create controller and views</span></span>
> * <span data-ttu-id="035c3-131">查看数据库</span><span class="sxs-lookup"><span data-stu-id="035c3-131">View the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="035c3-132">系统必备</span><span class="sxs-lookup"><span data-stu-id="035c3-132">Prerequisites</span></span>

* [<span data-ttu-id="035c3-133">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="035c3-133">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a><span data-ttu-id="035c3-134">创建 MVC web 应用</span><span class="sxs-lookup"><span data-stu-id="035c3-134">Create an MVC web app</span></span>

1. <span data-ttu-id="035c3-135">打开 Visual Studio，并使用C# " **ASP.NET web 应用程序（.NET Framework）** " 模板创建一个 web 项目。</span><span class="sxs-lookup"><span data-stu-id="035c3-135">Open Visual Studio and create a C# web project using the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="035c3-136">将项目命名为*ContosoUniversity* ，然后选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="035c3-136">Name the project *ContosoUniversity* and select **OK**.</span></span>

   ![Visual Studio 中的 "新建项目" 对话框](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. <span data-ttu-id="035c3-138">在**New ASP.NET Web 应用程序-ContosoUniversity**中，选择 " **MVC**"。</span><span class="sxs-lookup"><span data-stu-id="035c3-138">In **New ASP.NET Web Application - ContosoUniversity**, select **MVC**.</span></span>

   ![Visual Studio 中的 "新建 web 应用" 对话框](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > <span data-ttu-id="035c3-140">默认情况下， **authentication**选项设置为 "**无身份验证**"。</span><span class="sxs-lookup"><span data-stu-id="035c3-140">By default, the **Authentication** option is set to **No Authentication**.</span></span> <span data-ttu-id="035c3-141">对于本教程，web 应用不需要用户登录。</span><span class="sxs-lookup"><span data-stu-id="035c3-141">For this tutorial, the web app doesn't require users to sign in.</span></span> <span data-ttu-id="035c3-142">此外，它不会基于登录用户限制访问权限。</span><span class="sxs-lookup"><span data-stu-id="035c3-142">Also, it doesn't restrict access based on who's signed in.</span></span>

1. <span data-ttu-id="035c3-143">选择“确定”创建项目。</span><span class="sxs-lookup"><span data-stu-id="035c3-143">Select **OK** to create the project.</span></span>

## <a name="set-up-the-site-style"></a><span data-ttu-id="035c3-144">设置网站样式</span><span class="sxs-lookup"><span data-stu-id="035c3-144">Set up the site style</span></span>

<span data-ttu-id="035c3-145">通过几个简单的更改设置站点菜单、 布局和主页。</span><span class="sxs-lookup"><span data-stu-id="035c3-145">A few simple changes will set up the site menu, layout, and home page.</span></span>

1. <span data-ttu-id="035c3-146">*_Layout\\打开 Views\Shared*，并进行以下更改：</span><span class="sxs-lookup"><span data-stu-id="035c3-146">Open *Views\Shared\\_Layout.cshtml*, and make the following changes:</span></span>

   - <span data-ttu-id="035c3-147">将每次出现的 "我的 ASP.NET Application" 和 "Application name" 更改为 "Contoso 大学"。</span><span class="sxs-lookup"><span data-stu-id="035c3-147">Change each occurrence of "My ASP.NET Application" and "Application name" to "Contoso University".</span></span>
   - <span data-ttu-id="035c3-148">为学生、课程、教师和部门添加菜单项，并删除联系人条目。</span><span class="sxs-lookup"><span data-stu-id="035c3-148">Add menu entries for Students, Courses, Instructors, and Departments, and delete the Contact entry.</span></span>

   <span data-ttu-id="035c3-149">下面的代码片段突出显示了这些更改：</span><span class="sxs-lookup"><span data-stu-id="035c3-149">The changes are highlighted in the following code snippet:</span></span>

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. <span data-ttu-id="035c3-150">在*Views\Home\Index.cshtml*中，将该文件的内容替换为以下代码，以将有关 ASP.NET 和 MVC 的文本替换为有关此应用程序的文本：</span><span class="sxs-lookup"><span data-stu-id="035c3-150">In *Views\Home\Index.cshtml*, replace the contents of the file with the following code to replace the text about ASP.NET and MVC with text about this application:</span></span>

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. <span data-ttu-id="035c3-151">按 Ctrl + F5 运行该网站。</span><span class="sxs-lookup"><span data-stu-id="035c3-151">Press Ctrl+F5 to run the web site.</span></span> <span data-ttu-id="035c3-152">你将看到带有主菜单的主页。</span><span class="sxs-lookup"><span data-stu-id="035c3-152">You see the home page with the main menu.</span></span>

## <a name="install-entity-framework-6"></a><span data-ttu-id="035c3-153">安装实体框架6</span><span class="sxs-lookup"><span data-stu-id="035c3-153">Install Entity Framework 6</span></span>

1. <span data-ttu-id="035c3-154">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="035c3-154">From the **Tools** menu, choose **NuGet Package Manager**, and then choose **Package Manager Console**.</span></span>

2. <span data-ttu-id="035c3-155">在“程序包管理器控制台”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="035c3-155">In the **Package Manager Console** window, enter the following command:</span></span>

   ```text
   Install-Package EntityFramework
   ```

<span data-ttu-id="035c3-156">此步骤是本教程手动执行的几个步骤中的一步，但这可能已由 ASP.NET MVC 基架功能自动完成。</span><span class="sxs-lookup"><span data-stu-id="035c3-156">This step is one of a few steps that this tutorial has you do manually, but that could have been done automatically by the ASP.NET MVC scaffolding feature.</span></span> <span data-ttu-id="035c3-157">您要手动执行这些操作，以便您可以查看使用实体框架（EF）所需的步骤。</span><span class="sxs-lookup"><span data-stu-id="035c3-157">You're doing them manually so that you can see the steps required to use Entity Framework (EF).</span></span> <span data-ttu-id="035c3-158">稍后将使用基架创建 MVC 控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="035c3-158">You'll use scaffolding later to create the MVC controller and views.</span></span> <span data-ttu-id="035c3-159">替代方法是让基架自动安装 EF NuGet 包、创建数据库上下文类并创建连接字符串。</span><span class="sxs-lookup"><span data-stu-id="035c3-159">An alternative is to let scaffolding automatically install the EF NuGet package, create the database context class, and create the connection string.</span></span> <span data-ttu-id="035c3-160">当您准备好这样做时，您需要做的就是在创建实体类后，跳过这些步骤并基架 MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="035c3-160">When you're ready to do it that way, all you have to do is skip those steps and scaffold your MVC controller after you create your entity classes.</span></span>

## <a name="create-the-data-model"></a><span data-ttu-id="035c3-161">创建数据模型</span><span class="sxs-lookup"><span data-stu-id="035c3-161">Create the data model</span></span>

<span data-ttu-id="035c3-162">接下来你将创建 Contoso 大学应用程序的实体类。</span><span class="sxs-lookup"><span data-stu-id="035c3-162">Next you'll create entity classes for the Contoso University application.</span></span> <span data-ttu-id="035c3-163">你将从以下三个实体开始：</span><span class="sxs-lookup"><span data-stu-id="035c3-163">You'll start with the following three entities:</span></span>

<span data-ttu-id="035c3-164">**课程** <-> **注册** <-> **学生**</span><span class="sxs-lookup"><span data-stu-id="035c3-164">**Course** <-> **Enrollment** <-> **Student**</span></span>

| <span data-ttu-id="035c3-165">实体</span><span class="sxs-lookup"><span data-stu-id="035c3-165">Entities</span></span> | <span data-ttu-id="035c3-166">关系</span><span class="sxs-lookup"><span data-stu-id="035c3-166">Relationship</span></span> |
| -------- | ------------ |
| <span data-ttu-id="035c3-167">课程注册课程</span><span class="sxs-lookup"><span data-stu-id="035c3-167">Course to Enrollment</span></span> | <span data-ttu-id="035c3-168">一对多</span><span class="sxs-lookup"><span data-stu-id="035c3-168">One-to-many</span></span> |
| <span data-ttu-id="035c3-169">学生注册</span><span class="sxs-lookup"><span data-stu-id="035c3-169">Student to Enrollment</span></span> | <span data-ttu-id="035c3-170">一对多</span><span class="sxs-lookup"><span data-stu-id="035c3-170">One-to-many</span></span> |

<span data-ttu-id="035c3-171">`Student` 和 `Enrollment`实体之间是一对多的关系，`Course` 和`Enrollment` 实体之间也是一个对多的关系。</span><span class="sxs-lookup"><span data-stu-id="035c3-171">There's a one-to-many relationship between `Student` and `Enrollment` entities, and there's a one-to-many relationship between `Course` and `Enrollment` entities.</span></span> <span data-ttu-id="035c3-172">换而言之，一名学生可以修读任意数量的课程, 并且某一课程可以被任意数量的学生修读。</span><span class="sxs-lookup"><span data-stu-id="035c3-172">In other words, a student can be enrolled in any number of courses, and a course can have any number of students enrolled in it.</span></span>

<span data-ttu-id="035c3-173">在下面几节中，你将为其中的每个实体创建一个类。</span><span class="sxs-lookup"><span data-stu-id="035c3-173">In the following sections, you'll create a class for each one of these entities.</span></span>

> [!NOTE]
> <span data-ttu-id="035c3-174">如果尝试在完成所有这些实体类的创建之前编译项目，将会出现编译器错误。</span><span class="sxs-lookup"><span data-stu-id="035c3-174">If you try to compile the project before you finish creating all of these entity classes, you'll get compiler errors.</span></span>

### <a name="the-student-entity"></a><span data-ttu-id="035c3-175">Student 实体</span><span class="sxs-lookup"><span data-stu-id="035c3-175">The Student entity</span></span>

- <span data-ttu-id="035c3-176">在 "*模型*" 文件夹中，右键单击**解决方案资源管理器**的文件夹，然后选择 "**添加** > **类**"，创建名为*Student.cs*的类文件。</span><span class="sxs-lookup"><span data-stu-id="035c3-176">In the *Models* folder, create a class file named *Student.cs* by right-clicking on the folder in **Solution Explorer** and choosing **Add** > **Class**.</span></span> <span data-ttu-id="035c3-177">将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="035c3-177">Replace the template code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

<span data-ttu-id="035c3-178">`ID` 属性将成为对应于此类的数据库表中的主键。</span><span class="sxs-lookup"><span data-stu-id="035c3-178">The `ID` property will become the primary key column of the database table that corresponds to this class.</span></span> <span data-ttu-id="035c3-179">默认情况下，实体框架会将名为 `ID` 或*classname* `ID` 的属性解释为主键。</span><span class="sxs-lookup"><span data-stu-id="035c3-179">By default, Entity Framework interprets a property that's named `ID` or *classname* `ID` as the primary key.</span></span>

<span data-ttu-id="035c3-180">`Enrollments` 属性是*导航属性*。</span><span class="sxs-lookup"><span data-stu-id="035c3-180">The `Enrollments` property is a *navigation property*.</span></span> <span data-ttu-id="035c3-181">导航属性中包含与此实体相关的其他实体。</span><span class="sxs-lookup"><span data-stu-id="035c3-181">Navigation properties hold other entities that are related to this entity.</span></span> <span data-ttu-id="035c3-182">在这种情况下，`Student` 实体的 `Enrollments` 属性将包含与该 `Student` 实体相关的所有 `Enrollment` 实体。</span><span class="sxs-lookup"><span data-stu-id="035c3-182">In this case, the `Enrollments` property of a `Student` entity will hold all of the `Enrollment` entities that are related to that `Student` entity.</span></span> <span data-ttu-id="035c3-183">换言之，如果数据库中给定的 `Student` 行具有两个相关 `Enrollment` 行（其 `StudentID` 外键列中包含该学生的主键值的行），则该 `Student` 实体的 `Enrollments` 导航属性将包含这两个 `Enrollment` 的实体。</span><span class="sxs-lookup"><span data-stu-id="035c3-183">In other words, if a given `Student` row in the database has two related `Enrollment` rows (rows that contain that student's primary key value in their `StudentID` foreign key column), that `Student` entity's `Enrollments` navigation property will contain those two `Enrollment` entities.</span></span>

<span data-ttu-id="035c3-184">导航属性通常定义为 `virtual`，以便它们可以利用某些实体框架功能，如*延迟加载*。</span><span class="sxs-lookup"><span data-stu-id="035c3-184">Navigation properties are typically defined as `virtual` so that they can take advantage of certain Entity Framework functionality such as *lazy loading*.</span></span> <span data-ttu-id="035c3-185">（稍后将在本系列的 "[读取相关数据](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)" 教程中介绍延迟加载。）</span><span class="sxs-lookup"><span data-stu-id="035c3-185">(Lazy loading will be explained later, in the [Reading Related Data](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series.)</span></span>

<span data-ttu-id="035c3-186">如果导航属性可以具有多个实体 （如多对多或一对多关系），那么导航属性的类型必须是可以添加、 删除和更新条目的容器，如 `ICollection`。</span><span class="sxs-lookup"><span data-stu-id="035c3-186">If a navigation property can hold multiple entities (as in many-to-many or one-to-many relationships), its type must be a list in which entries can be added, deleted, and updated, such as `ICollection`.</span></span>

### <a name="the-enrollment-entity"></a><span data-ttu-id="035c3-187">Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="035c3-187">The Enrollment entity</span></span>

- <span data-ttu-id="035c3-188">在 *Models* 文件夹中，创建 *Enrollment.cs* 并且用以下代码替换现有代码：</span><span class="sxs-lookup"><span data-stu-id="035c3-188">In the *Models* folder, create *Enrollment.cs* and replace the existing code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

<span data-ttu-id="035c3-189">`EnrollmentID` 属性将为主键;此实体使用*classname* `ID` 模式，而不是在 `Student` 实体中看到的那样 `ID`。</span><span class="sxs-lookup"><span data-stu-id="035c3-189">The `EnrollmentID` property will be the primary key; this entity uses the *classname* `ID` pattern instead of `ID` by itself as you saw in the `Student` entity.</span></span> <span data-ttu-id="035c3-190">通常情况下，你选择一个主键模式，并在你的数据模型自始至终使用这种模式。</span><span class="sxs-lookup"><span data-stu-id="035c3-190">Ordinarily you would choose one pattern and use it throughout your data model.</span></span> <span data-ttu-id="035c3-191">在这里，使用了两种不同的模式只是为了说明你可以使用任一模式来指定主键。</span><span class="sxs-lookup"><span data-stu-id="035c3-191">Here, the variation illustrates that you can use either pattern.</span></span> <span data-ttu-id="035c3-192">在后面的教程中，你将了解如何使用不带 `classname` 的 `ID`，从而更轻松地在数据模型中实现继承。</span><span class="sxs-lookup"><span data-stu-id="035c3-192">In a later tutorial, you'll see how using `ID` without `classname` makes it easier to implement inheritance in the data model.</span></span>

<span data-ttu-id="035c3-193">`Grade` 属性是一个[枚举](/ef/ef6/modeling/code-first/data-types/enums)。</span><span class="sxs-lookup"><span data-stu-id="035c3-193">The `Grade` property is an [enum](/ef/ef6/modeling/code-first/data-types/enums).</span></span> <span data-ttu-id="035c3-194">`Grade` 声明类型后的`?`表示 `Grade` 属性可以为 [null](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)。</span><span class="sxs-lookup"><span data-stu-id="035c3-194">The question mark after the `Grade` type declaration indicates that the `Grade` property is [nullable](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types).</span></span> <span data-ttu-id="035c3-195">Null 的级别不同于零级别，null 表示分数未知或尚未赋值。</span><span class="sxs-lookup"><span data-stu-id="035c3-195">A grade that's null is different from a zero grade — null means a grade isn't known or hasn't been assigned yet.</span></span>

<span data-ttu-id="035c3-196">`StudentID` 属性是一个外键，`Student` 是与其且对应的导航属性。</span><span class="sxs-lookup"><span data-stu-id="035c3-196">The `StudentID` property is a foreign key, and the corresponding navigation property is `Student`.</span></span> <span data-ttu-id="035c3-197">`Enrollment` 实体与一个 `Student` 实体相关联，因此该属性只包含单个 `Student` 实体 (与前面所看到的 `Student.Enrollments` 导航属性不同后，`Student`中可以容纳多个 `Enrollment` 实体)。</span><span class="sxs-lookup"><span data-stu-id="035c3-197">An `Enrollment` entity is associated with one `Student` entity, so the property can only hold a single `Student` entity (unlike the `Student.Enrollments` navigation property you saw earlier, which can hold multiple `Enrollment` entities).</span></span>

<span data-ttu-id="035c3-198">`CourseID` 属性是一个外键，`Course` 是与其且对应的导航属性。</span><span class="sxs-lookup"><span data-stu-id="035c3-198">The `CourseID` property is a foreign key, and the corresponding navigation property is `Course`.</span></span> <span data-ttu-id="035c3-199">`Enrollment` 实体与一个 `Course` 实体相关联。</span><span class="sxs-lookup"><span data-stu-id="035c3-199">An `Enrollment` entity is associated with one `Course` entity.</span></span>

<span data-ttu-id="035c3-200">实体框架将属性指定为外键属性，如果该属性命名为 *&lt;导航属性名称&gt;&lt;主键属性名称&gt;* （例如，`StudentID` 导航属性 `Student`，因为 `Student` 实体的主键是 `ID`）。</span><span class="sxs-lookup"><span data-stu-id="035c3-200">Entity Framework interprets a property as a foreign key property if it's named *&lt;navigation property name&gt;&lt;primary key property name&gt;* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="035c3-201">也可以将外键属性命名为相同 *&lt;主键属性名称&gt;* （例如 `CourseID`，因为 `Course` 实体的主键是 `CourseID`）。</span><span class="sxs-lookup"><span data-stu-id="035c3-201">Foreign key properties can also be named the same simply *&lt;primary key property name&gt;* (for example, `CourseID` since the `Course` entity's primary key is `CourseID`).</span></span>

### <a name="the-course-entity"></a><span data-ttu-id="035c3-202">Course 实体</span><span class="sxs-lookup"><span data-stu-id="035c3-202">The Course entity</span></span>

- <span data-ttu-id="035c3-203">在 "*模型*" 文件夹中，创建*Course.cs*，并将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="035c3-203">In the *Models* folder, create *Course.cs*, replacing the template code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

<span data-ttu-id="035c3-204">`Enrollments` 属性是导航属性。</span><span class="sxs-lookup"><span data-stu-id="035c3-204">The `Enrollments` property is a navigation property.</span></span> <span data-ttu-id="035c3-205">一个 `Course` 体可以与任意数量的 `Enrollment` 实体相关。</span><span class="sxs-lookup"><span data-stu-id="035c3-205">A `Course` entity can be related to any number of `Enrollment` entities.</span></span>

<span data-ttu-id="035c3-206">在本系列的后续教程中，我们将详细介绍 <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> 特性。</span><span class="sxs-lookup"><span data-stu-id="035c3-206">We'll say more about the <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> attribute in a later tutorial in this series.</span></span> <span data-ttu-id="035c3-207">简单来说，此特性让你能自行指定主键，而不是让数据库自动指定主键。</span><span class="sxs-lookup"><span data-stu-id="035c3-207">Basically, this attribute lets you enter the primary key for the course rather than having the database generate it.</span></span>

## <a name="create-the-database-context"></a><span data-ttu-id="035c3-208">创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="035c3-208">Create the database context</span></span>

<span data-ttu-id="035c3-209">为给定数据模型协调实体框架功能的主类是*数据库上下文*类。</span><span class="sxs-lookup"><span data-stu-id="035c3-209">The main class that coordinates Entity Framework functionality for a given data model is the *database context* class.</span></span> <span data-ttu-id="035c3-210">可以通过从[DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx)类派生来创建此类。</span><span class="sxs-lookup"><span data-stu-id="035c3-210">You create this class by deriving from the [System.Data.Entity.DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx) class.</span></span> <span data-ttu-id="035c3-211">在代码中，可以指定要包含在数据模型中的实体。</span><span class="sxs-lookup"><span data-stu-id="035c3-211">In your code, you specify which entities are included in the data model.</span></span> <span data-ttu-id="035c3-212">你还可以定义某些 Entity Framework 行为。</span><span class="sxs-lookup"><span data-stu-id="035c3-212">You can also customize certain Entity Framework behavior.</span></span> <span data-ttu-id="035c3-213">在此项目中将数据库上下文类命名为 `SchoolContext`。</span><span class="sxs-lookup"><span data-stu-id="035c3-213">In this project, the class is named `SchoolContext`.</span></span>

- <span data-ttu-id="035c3-214">若要在 ContosoUniversity 项目中创建文件夹，请在**解决方案资源管理器**中右键单击该项目，然后单击 "**添加**"，然后单击 "**新建文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="035c3-214">To create a folder in the ContosoUniversity project, right-click the project in **Solution Explorer** and click **Add**, and then click **New Folder**.</span></span> <span data-ttu-id="035c3-215">将新文件夹命名为*DAL* （适用于数据访问层）。</span><span class="sxs-lookup"><span data-stu-id="035c3-215">Name the new folder *DAL* (for Data Access Layer).</span></span> <span data-ttu-id="035c3-216">在该文件夹中，创建一个名为*SchoolContext.cs*的新类文件，并将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="035c3-216">In that folder, create a new class file named *SchoolContext.cs*, and replace the template code with the following code:</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a><span data-ttu-id="035c3-217">指定实体集</span><span class="sxs-lookup"><span data-stu-id="035c3-217">Specify entity sets</span></span>

<span data-ttu-id="035c3-218">此代码为每个实体集创建一个[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="035c3-218">This code creates a [DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx) property for each entity set.</span></span> <span data-ttu-id="035c3-219">在实体框架术语中，*实体集*通常对应于数据库表，*实体*对应于表中的行。</span><span class="sxs-lookup"><span data-stu-id="035c3-219">In Entity Framework terminology, an *entity set* typically corresponds to a database table, and an *entity* corresponds to a row in the table.</span></span>

> [!NOTE]
>
> <span data-ttu-id="035c3-220">您可以省略 `DbSet<Enrollment>` 和 `DbSet<Course>` 语句，它的工作原理相同。</span><span class="sxs-lookup"><span data-stu-id="035c3-220">You can omit the `DbSet<Enrollment>` and `DbSet<Course>` statements and it would work the same.</span></span> <span data-ttu-id="035c3-221">实体框架将隐式包含它们，因为 `Student` 实体引用 `Enrollment` 实体，而 `Enrollment` 实体引用 `Course` 实体。</span><span class="sxs-lookup"><span data-stu-id="035c3-221">Entity Framework would include them implicitly because the `Student` entity references the `Enrollment` entity and the `Enrollment` entity references the `Course` entity.</span></span>

### <a name="specify-the-connection-string"></a><span data-ttu-id="035c3-222">指定连接字符串</span><span class="sxs-lookup"><span data-stu-id="035c3-222">Specify the connection string</span></span>

<span data-ttu-id="035c3-223">连接字符串的名称（稍后要添加到 web.config 文件中）将传递到构造函数。</span><span class="sxs-lookup"><span data-stu-id="035c3-223">The name of the connection string (which you'll add to the Web.config file later) is passed in to the constructor.</span></span>

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

<span data-ttu-id="035c3-224">你还可以传递连接字符串本身，而不是存储在 web.config 文件中的连接字符串的名称。</span><span class="sxs-lookup"><span data-stu-id="035c3-224">You could also pass in the connection string itself instead of the name of one that is stored in the Web.config file.</span></span> <span data-ttu-id="035c3-225">有关用于指定要使用的数据库的选项的详细信息，请参阅[连接字符串和模型](/ef/ef6/fundamentals/configuring/connection-strings)。</span><span class="sxs-lookup"><span data-stu-id="035c3-225">For more information about options for specifying the database to use, see [Connection strings and models](/ef/ef6/fundamentals/configuring/connection-strings).</span></span>

<span data-ttu-id="035c3-226">如果未显式指定连接字符串或名称，则实体框架假设连接字符串名称与类名称相同。</span><span class="sxs-lookup"><span data-stu-id="035c3-226">If you don't specify a connection string or the name of one explicitly, Entity Framework assumes that the connection string name is the same as the class name.</span></span> <span data-ttu-id="035c3-227">然后，本示例中的默认连接字符串名称将为 `SchoolContext`，就像您显式指定的一样。</span><span class="sxs-lookup"><span data-stu-id="035c3-227">The default connection string name in this example would then be `SchoolContext`, the same as what you're specifying explicitly.</span></span>

### <a name="specify-singular-table-names"></a><span data-ttu-id="035c3-228">指定单一表名称</span><span class="sxs-lookup"><span data-stu-id="035c3-228">Specify singular table names</span></span>

<span data-ttu-id="035c3-229">[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的 `modelBuilder.Conventions.Remove` 语句阻止复数表名称。</span><span class="sxs-lookup"><span data-stu-id="035c3-229">The `modelBuilder.Conventions.Remove` statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method prevents table names from being pluralized.</span></span> <span data-ttu-id="035c3-230">如果未执行此操作，则数据库中生成的表将被命名为 `Students`、`Courses`和 `Enrollments`。</span><span class="sxs-lookup"><span data-stu-id="035c3-230">If you didn't do this, the generated tables in the database would be named `Students`, `Courses`, and `Enrollments`.</span></span> <span data-ttu-id="035c3-231">相反，表名称将为 `Student`、`Course`和 `Enrollment`。</span><span class="sxs-lookup"><span data-stu-id="035c3-231">Instead, the table names will be `Student`, `Course`, and `Enrollment`.</span></span> <span data-ttu-id="035c3-232">开发者对表名称是否应为复数意见不一。</span><span class="sxs-lookup"><span data-stu-id="035c3-232">Developers disagree about whether table names should be pluralized or not.</span></span> <span data-ttu-id="035c3-233">本教程使用单数形式，但重要的是，您可以选择您喜欢的任何形式，包括或省略此行代码。</span><span class="sxs-lookup"><span data-stu-id="035c3-233">This tutorial uses the singular form, but the important point is that you can select whichever form you prefer by including or omitting this line of code.</span></span>

## <a name="initialize-db-with-test-data"></a><span data-ttu-id="035c3-234">使用测试数据初始化数据库</span><span class="sxs-lookup"><span data-stu-id="035c3-234">Initialize DB with test data</span></span>

<span data-ttu-id="035c3-235">当应用程序运行时，实体框架可以自动创建（或删除并重新创建）数据库。</span><span class="sxs-lookup"><span data-stu-id="035c3-235">Entity Framework can automatically create (or drop and re-create) a database for you when the application runs.</span></span> <span data-ttu-id="035c3-236">您可以指定在每次应用程序运行时执行此操作，或仅在模型与现有数据库不同步时执行此操作。</span><span class="sxs-lookup"><span data-stu-id="035c3-236">You can specify that this should be done every time your application runs or only when the model is out of sync with the existing database.</span></span> <span data-ttu-id="035c3-237">您还可以编写一个 `Seed` 方法，该方法实体框架在创建数据库后自动调用，以便使用测试数据填充它。</span><span class="sxs-lookup"><span data-stu-id="035c3-237">You can also write a `Seed` method that Entity Framework automatically calls after creating the database in order to populate it with test data.</span></span>

<span data-ttu-id="035c3-238">默认行为是只在数据库不存在时才创建数据库（如果模型发生了更改并且数据库已存在，则会引发异常）。</span><span class="sxs-lookup"><span data-stu-id="035c3-238">The default behavior is to create a database only if it doesn't exist (and throw an exception if the model has changed and the database already exists).</span></span> <span data-ttu-id="035c3-239">在本部分中，你将指定在模型发生更改时应删除并重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="035c3-239">In this section, you'll specify that the database should be dropped and re-created whenever the model changes.</span></span> <span data-ttu-id="035c3-240">删除数据库将导致丢失所有数据。</span><span class="sxs-lookup"><span data-stu-id="035c3-240">Dropping the database causes the loss of all your data.</span></span> <span data-ttu-id="035c3-241">这通常在开发过程中是正常的，因为在重新创建数据库时将运行 `Seed` 方法，并将重新创建测试数据。</span><span class="sxs-lookup"><span data-stu-id="035c3-241">This is generally okay during development, because the `Seed` method will run when the database is re-created and will re-create your test data.</span></span> <span data-ttu-id="035c3-242">但在生产环境中，您通常不希望每次需要更改数据库架构时都丢失所有数据。</span><span class="sxs-lookup"><span data-stu-id="035c3-242">But in production you generally don't want to lose all your data every time you need to change the database schema.</span></span> <span data-ttu-id="035c3-243">稍后，您将了解如何使用 Code First 迁移更改数据库架构（而不是删除和重新创建数据库）来处理模型更改。</span><span class="sxs-lookup"><span data-stu-id="035c3-243">Later you'll see how to handle model changes by using Code First Migrations to change the database schema instead of dropping and re-creating the database.</span></span>

1. <span data-ttu-id="035c3-244">在 DAL 文件夹中，创建一个名为*SchoolInitializer.cs*的新类文件，并将模板代码替换为以下代码，这会导致在需要时创建数据库，并将测试数据加载到新数据库中。</span><span class="sxs-lookup"><span data-stu-id="035c3-244">In the DAL folder, create a new class file named *SchoolInitializer.cs* and replace the template code with the following code, which causes a database to be created when needed and loads test data into the new database.</span></span>

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   <span data-ttu-id="035c3-245">`Seed` 方法采用数据库上下文对象作为输入参数，方法中的代码使用该对象将新实体添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="035c3-245">The `Seed` method takes the database context object as an input parameter, and the code in the method uses that object to add new entities to the database.</span></span> <span data-ttu-id="035c3-246">对于每个实体类型，代码将创建新实体的集合，将其添加到相应的 `DbSet` 属性，然后将更改保存到数据库。</span><span class="sxs-lookup"><span data-stu-id="035c3-246">For each entity type, the code creates a collection of new  entities, adds them to the appropriate `DbSet` property, and then saves the changes to the database.</span></span> <span data-ttu-id="035c3-247">不需要在每个实体组之后调用 `SaveChanges` 方法，如此处所示，但这样做可帮助您找到问题的根源（如果代码写入数据库时出现异常）。</span><span class="sxs-lookup"><span data-stu-id="035c3-247">It isn't necessary to call the `SaveChanges` method after each group of entities, as is done here, but doing that helps you locate the source of a problem if an exception occurs while the code is writing to the database.</span></span>

2. <span data-ttu-id="035c3-248">若要告诉实体框架使用初始值设定项类，请将一个元素添加到应用程序*web.config*文件（位于根项目文件夹中）的 `entityFramework` 元素中，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="035c3-248">To tell Entity Framework to use your initializer class, add an element to the `entityFramework` element in the application *Web.config* file (the one in the root project folder), as shown in the following example:</span></span>

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   <span data-ttu-id="035c3-249">`context type` 指定完全限定的上下文类名称和它所在的程序集，并且 `databaseinitializer type` 指定初始值设定项类及其所在程序集的完全限定名称。</span><span class="sxs-lookup"><span data-stu-id="035c3-249">The `context type` specifies the fully qualified context class name and the assembly it's in, and the `databaseinitializer type` specifies the fully qualified name of the initializer class and the assembly it's in.</span></span> <span data-ttu-id="035c3-250">（如果不希望 EF 使用初始值设定项，则可在 `context` 元素上设置属性： `disableDatabaseInitialization="true"`。）有关详细信息，请参阅[配置文件设置](/ef/ef6/fundamentals/configuring/config-file)。</span><span class="sxs-lookup"><span data-stu-id="035c3-250">(When you don't want EF to use the initializer, you can set an attribute on the `context` element: `disableDatabaseInitialization="true"`.) For more information, see [Configuration File Settings](/ef/ef6/fundamentals/configuring/config-file).</span></span>

   <span data-ttu-id="035c3-251">在*web.config 文件中*设置初始值设定项的替代方法是在*Global.asax.cs*文件中将 `Database.SetInitializer` 语句添加到 `Application_Start` 方法，以便在代码中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="035c3-251">An alternative to setting the initializer in the *Web.config* file is to do it in code by adding a `Database.SetInitializer` statement to the `Application_Start` method in the *Global.asax.cs* file.</span></span> <span data-ttu-id="035c3-252">有关详细信息，请参阅[了解实体框架 Code First 中的数据库初始值设定项](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)。</span><span class="sxs-lookup"><span data-stu-id="035c3-252">For more information, see [Understanding Database Initializers in Entity Framework Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm).</span></span>

<span data-ttu-id="035c3-253">现在已设置应用程序，以便在应用程序的给定运行中首次访问数据库时，实体框架将数据库与模型（`SchoolContext` 和实体类）进行比较。</span><span class="sxs-lookup"><span data-stu-id="035c3-253">The application is now set up so that when you access the database for the first time in a given run of the application, Entity Framework compares the database to the model (your `SchoolContext` and entity classes).</span></span> <span data-ttu-id="035c3-254">如果存在差异，应用程序会删除并重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="035c3-254">If there's a difference, the application drops and re-creates the database.</span></span>

> [!NOTE]
> <span data-ttu-id="035c3-255">将应用程序部署到生产 web 服务器时，必须删除或禁用删除并重新创建该数据库的代码。</span><span class="sxs-lookup"><span data-stu-id="035c3-255">When you deploy an application to a production web server, you must remove or disable code that drops and re-creates the database.</span></span> <span data-ttu-id="035c3-256">你将在本系列的后续教程中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="035c3-256">You'll do that in a later tutorial in this series.</span></span>

## <a name="set-up-ef-6-to-use-localdb"></a><span data-ttu-id="035c3-257">设置 EF 6 以使用 LocalDB</span><span class="sxs-lookup"><span data-stu-id="035c3-257">Set up EF 6 to use LocalDB</span></span>

<span data-ttu-id="035c3-258">[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017)是 SQL Server Express 数据库引擎的轻型版本。</span><span class="sxs-lookup"><span data-stu-id="035c3-258">[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017) is a lightweight version of the SQL Server Express database engine.</span></span> <span data-ttu-id="035c3-259">它易于安装和配置，可以按需启动并在用户模式下运行。</span><span class="sxs-lookup"><span data-stu-id="035c3-259">It's easy to install and configure, starts on demand, and runs in user mode.</span></span> <span data-ttu-id="035c3-260">LocalDB 在 SQL Server Express 的特殊执行模式下运行，该模式使您能够将数据库用作 *.mdf*文件。</span><span class="sxs-lookup"><span data-stu-id="035c3-260">LocalDB runs in a special execution mode of SQL Server Express that enables you to work with databases as *.mdf* files.</span></span> <span data-ttu-id="035c3-261">如果希望能够使用项目复制数据库，则可以将 LocalDB 数据库文件放在 web 项目的*应用\_Data*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="035c3-261">You can put LocalDB database files in the *App\_Data* folder of a web project if you want to be able to copy the database with the project.</span></span> <span data-ttu-id="035c3-262">使用 SQL Server Express 中的用户实例功能，还可以使用 *.mdf*文件，但不推荐使用用户实例功能;因此，建议使用 LocalDB 来处理 *.mdf*文件。</span><span class="sxs-lookup"><span data-stu-id="035c3-262">The user instance feature in SQL Server Express also enables you to work with *.mdf* files, but the user instance feature is deprecated; therefore, LocalDB is recommended for working with *.mdf* files.</span></span> <span data-ttu-id="035c3-263">默认情况下，使用 Visual Studio 安装 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="035c3-263">LocalDB is installed by default with Visual Studio.</span></span>

<span data-ttu-id="035c3-264">通常，SQL Server Express 不用于生产 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="035c3-264">Typically, SQL Server Express is not used for production web applications.</span></span> <span data-ttu-id="035c3-265">不建议将 LocalDB 特别用于 web 应用程序，因为它不能与 IIS 一起使用。</span><span class="sxs-lookup"><span data-stu-id="035c3-265">LocalDB in particular is not recommended for production use with a web application because it's not designed to work with IIS.</span></span>

- <span data-ttu-id="035c3-266">在本教程中，你将使用 LocalDB。</span><span class="sxs-lookup"><span data-stu-id="035c3-266">In this tutorial, you'll work with LocalDB.</span></span> <span data-ttu-id="035c3-267">打开应用程序*web.config*文件，并在 `appSettings` 元素前面添加一个 `connectionStrings` 元素，如下面的示例中所示。</span><span class="sxs-lookup"><span data-stu-id="035c3-267">Open the application *Web.config* file and add a `connectionStrings` element preceding the `appSettings` element, as shown in the following example.</span></span> <span data-ttu-id="035c3-268">（请确保更新根项目文件夹中的*web.config 文件。*</span><span class="sxs-lookup"><span data-stu-id="035c3-268">(Make sure you update the *Web.config* file in the root project folder.</span></span> <span data-ttu-id="035c3-269">"*视图*" 子文件夹中还有一个不需要更新*的 web.config 文件*。</span><span class="sxs-lookup"><span data-stu-id="035c3-269">There's also a *Web.config* file in the *Views* subfolder that you don't need to update.)</span></span>

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

<span data-ttu-id="035c3-270">添加的连接字符串指定实体框架将使用名为*ContosoUniversity1*的 LocalDB 数据库。</span><span class="sxs-lookup"><span data-stu-id="035c3-270">The connection string you've added specifies that Entity Framework will use a LocalDB database named *ContosoUniversity1.mdf*.</span></span> <span data-ttu-id="035c3-271">（数据库尚不存在，但 EF 会创建它。）如果要在应用中创建数据库 *\_Data*文件夹，可以将 `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` 添加到连接字符串。</span><span class="sxs-lookup"><span data-stu-id="035c3-271">(The database doesn't exist yet but EF will create it.) If you want to create the database in your *App\_Data* folder, you could add `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` to the connection string.</span></span> <span data-ttu-id="035c3-272">有关连接字符串的详细信息，请参阅[SQL Server ASP.NET Web 应用程序的连接字符串](/previous-versions/aspnet/jj653752(v=vs.110))。</span><span class="sxs-lookup"><span data-stu-id="035c3-272">For more information about connection strings, see [SQL Server Connection Strings for ASP.NET Web Applications](/previous-versions/aspnet/jj653752(v=vs.110)).</span></span>

<span data-ttu-id="035c3-273">在*web.config 文件中，实际上*不需要连接字符串。</span><span class="sxs-lookup"><span data-stu-id="035c3-273">You don't actually need a connection string in the *Web.config* file.</span></span> <span data-ttu-id="035c3-274">如果没有提供连接字符串，实体框架会根据上下文类使用默认连接字符串。</span><span class="sxs-lookup"><span data-stu-id="035c3-274">If you don't supply a connection string, Entity Framework uses a default connection string based on your context class.</span></span> <span data-ttu-id="035c3-275">有关详细信息，请参阅[Code First 到新的数据库](/ef/ef6/modeling/code-first/workflows/new-database)。</span><span class="sxs-lookup"><span data-stu-id="035c3-275">For more information, see [Code First to a New Database](/ef/ef6/modeling/code-first/workflows/new-database).</span></span>

## <a name="create-controller-and-views"></a><span data-ttu-id="035c3-276">创建控制器和视图</span><span class="sxs-lookup"><span data-stu-id="035c3-276">Create controller and views</span></span>

<span data-ttu-id="035c3-277">现在，您将创建一个网页来显示数据。</span><span class="sxs-lookup"><span data-stu-id="035c3-277">Now you'll create a web page to display data.</span></span> <span data-ttu-id="035c3-278">请求数据的过程会自动触发数据库的创建。</span><span class="sxs-lookup"><span data-stu-id="035c3-278">The process of requesting the data automatically triggers the creation of the database.</span></span> <span data-ttu-id="035c3-279">首先创建一个新的控制器。</span><span class="sxs-lookup"><span data-stu-id="035c3-279">You'll begin by creating a new controller.</span></span> <span data-ttu-id="035c3-280">但在执行此操作之前，请生成项目，使模型和上下文类可用于 MVC 控制器基架。</span><span class="sxs-lookup"><span data-stu-id="035c3-280">But before you do that, build the project to make the model and context classes available to MVC controller scaffolding.</span></span>

1. <span data-ttu-id="035c3-281">右键单击**解决方案资源管理器**中的 "**控制器**" 文件夹，选择 "**添加**"，然后单击 "**新建基架项**"。</span><span class="sxs-lookup"><span data-stu-id="035c3-281">Right-click the **Controllers** folder in **Solution Explorer**, select **Add**, and then click **New Scaffolded Item**.</span></span>
2. <span data-ttu-id="035c3-282">在 "**添加基架**" 对话框中，选择 "**包含视图的 MVC 5 控制器，使用实体框架**"，然后选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="035c3-282">In the **Add Scaffold** dialog box, select **MVC 5 Controller with views, using Entity Framework**, and then choose **Add**.</span></span>

     ![在 Visual Studio 中添加基架对话框](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. <span data-ttu-id="035c3-284">在 "**添加控制器**" 对话框中，进行以下选择，然后选择 "**添加**"：</span><span class="sxs-lookup"><span data-stu-id="035c3-284">In the **Add Controller** dialog box, make the following selections, and then choose **Add**:</span></span>

   - <span data-ttu-id="035c3-285">Model 类： **Student （ContosoUniversity）** 。</span><span class="sxs-lookup"><span data-stu-id="035c3-285">Model class: **Student (ContosoUniversity.Models)**.</span></span> <span data-ttu-id="035c3-286">（如果未在下拉列表中看到此选项，请生成项目，然后重试。）</span><span class="sxs-lookup"><span data-stu-id="035c3-286">(If you don't see this option in the drop-down list, build the project and try again.)</span></span>
   - <span data-ttu-id="035c3-287">数据上下文类： **SchoolContext （ContosoUniversity）** 。</span><span class="sxs-lookup"><span data-stu-id="035c3-287">Data context class: **SchoolContext (ContosoUniversity.DAL)**.</span></span>
   - <span data-ttu-id="035c3-288">控制器名称： **StudentController** （而不是 StudentsController）。</span><span class="sxs-lookup"><span data-stu-id="035c3-288">Controller name: **StudentController** (not StudentsController).</span></span>
   - <span data-ttu-id="035c3-289">为其他字段保留默认值。</span><span class="sxs-lookup"><span data-stu-id="035c3-289">Leave the default values for the other fields.</span></span>

     <span data-ttu-id="035c3-290">单击 "**添加**" 时，scaffolder 会创建一个*StudentController.cs*文件和一组与控制器一起使用的视图（*cshtml*文件）。</span><span class="sxs-lookup"><span data-stu-id="035c3-290">When you click **Add**, the scaffolder creates a *StudentController.cs* file and a set of views (*.cshtml* files) that work with the controller.</span></span> <span data-ttu-id="035c3-291">在将来创建使用实体框架的项目时，还可以利用 scaffolder 的一些附加功能：创建第一个模型类，不要创建连接字符串，然后在 "**添加控制器**" 框中，通过选择 "**数据上下文类**" 旁边的 **+** 按钮来指定**新的数据上下文**。</span><span class="sxs-lookup"><span data-stu-id="035c3-291">In the future when you create projects that use Entity Framework, you can also take advantage of some additional functionality of the scaffolder: create your first model class, don't create a connection string, and then in the **Add Controller** box specify **New data context** by selecting the **+** button next to **Data context class**.</span></span> <span data-ttu-id="035c3-292">Scaffolder 将创建 `DbContext` 类和连接字符串以及控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="035c3-292">The scaffolder will create your `DbContext` class and your connection string as well as the controller and views.</span></span>
4. <span data-ttu-id="035c3-293">Visual Studio 将打开*Controllers\StudentController.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="035c3-293">Visual Studio opens the *Controllers\StudentController.cs* file.</span></span> <span data-ttu-id="035c3-294">你会看到已创建实例化数据库上下文对象的类变量：</span><span class="sxs-lookup"><span data-stu-id="035c3-294">You see that a class variable has been created that instantiates a database context object:</span></span>

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     <span data-ttu-id="035c3-295">`Index` 操作方法通过读取数据库上下文实例的 `Students` 属性，从*学生*实体集中获取学生列表：</span><span class="sxs-lookup"><span data-stu-id="035c3-295">The `Index` action method gets a list of students from the *Students* entity set by reading the `Students` property of the database context instance:</span></span>

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     <span data-ttu-id="035c3-296">*Student\Index.cshtml*视图将此列表显示在表中：</span><span class="sxs-lookup"><span data-stu-id="035c3-296">The *Student\Index.cshtml* view displays this list in a table:</span></span>

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. <span data-ttu-id="035c3-297">按 Ctrl+F5 运行项目。</span><span class="sxs-lookup"><span data-stu-id="035c3-297">Press Ctrl+F5 to run the project.</span></span> <span data-ttu-id="035c3-298">（如果收到 "无法创建卷影副本" 错误，请关闭浏览器并重试。）</span><span class="sxs-lookup"><span data-stu-id="035c3-298">(If you get a "Cannot create Shadow Copy" error, close the browser and try again.)</span></span>

     <span data-ttu-id="035c3-299">单击 "**学生**" 选项卡以查看 `Seed` 方法插入的测试数据。</span><span class="sxs-lookup"><span data-stu-id="035c3-299">Click the **Students** tab to see the test data that the `Seed` method inserted.</span></span> <span data-ttu-id="035c3-300">根据浏览器窗口的大小，你会在顶部的地址栏中看到 "学生" 选项卡链接，或单击右上角以查看链接。</span><span class="sxs-lookup"><span data-stu-id="035c3-300">Depending on how narrow your browser window is, you'll see the Student tab link in the top address bar or you'll have to click the upper right corner to see the link.</span></span>

     ![菜单按钮](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a><span data-ttu-id="035c3-302">查看数据库</span><span class="sxs-lookup"><span data-stu-id="035c3-302">View the database</span></span>

<span data-ttu-id="035c3-303">当你运行 "学生" 页且应用程序尝试访问数据库时，EF 发现没有数据库并创建了数据库。</span><span class="sxs-lookup"><span data-stu-id="035c3-303">When you ran the Students page and the application tried to access the database, EF discovered that there was no database and created one.</span></span> <span data-ttu-id="035c3-304">然后，EF 运行 seed 方法来用数据填充数据库。</span><span class="sxs-lookup"><span data-stu-id="035c3-304">EF then ran the seed method to populate the database with data.</span></span>

<span data-ttu-id="035c3-305">您可以使用**服务器资源管理器**或**SQL Server 对象资源管理器**（SSOX）在 Visual Studio 中查看数据库。</span><span class="sxs-lookup"><span data-stu-id="035c3-305">You can use either **Server Explorer** or **SQL Server Object Explorer** (SSOX) to view the database in Visual Studio.</span></span> <span data-ttu-id="035c3-306">对于本教程，你将使用**服务器资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="035c3-306">For this tutorial, you'll use **Server Explorer**.</span></span>

1. <span data-ttu-id="035c3-307">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="035c3-307">Close the browser.</span></span>
2. <span data-ttu-id="035c3-308">在**服务器资源管理器**中，展开 "**数据连接**" （可能需要首先选择 "刷新" 按钮），展开 "**学校上下文（ContosoUniversity）** "，然后展开 "**表**" 以查看新数据库中的表。</span><span class="sxs-lookup"><span data-stu-id="035c3-308">In **Server Explorer**, expand **Data Connections** (you may need to select the refresh button first), expand **School Context (ContosoUniversity)**, and then expand **Tables** to see the tables in your new database.</span></span>

3. <span data-ttu-id="035c3-309">右键单击**Student**表，然后单击 "**显示表数据**"，查看已创建的列和插入到该表中的行。</span><span class="sxs-lookup"><span data-stu-id="035c3-309">Right-click the **Student** table and click **Show Table Data** to see the columns that were created and the rows that were inserted into the table.</span></span>

4. <span data-ttu-id="035c3-310">关闭**服务器资源管理器**连接。</span><span class="sxs-lookup"><span data-stu-id="035c3-310">Close the **Server Explorer** connection.</span></span>

<span data-ttu-id="035c3-311">*ContosoUniversity1*和 *.ldf*数据库文件位于 *% USERPROFILE%* 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="035c3-311">The *ContosoUniversity1.mdf* and *.ldf* database files are in the *%USERPROFILE%* folder.</span></span>

<span data-ttu-id="035c3-312">由于你使用的是 `DropCreateDatabaseIfModelChanges` 初始值设定项，因此你现在可以对 `Student` 类进行更改，然后再次运行应用程序，并将自动重新创建数据库以匹配你的更改。</span><span class="sxs-lookup"><span data-stu-id="035c3-312">Because you're using the `DropCreateDatabaseIfModelChanges` initializer, you could now make a change to the `Student` class, run the application again, and the database would automatically be re-created to match your change.</span></span> <span data-ttu-id="035c3-313">例如，如果向 `Student` 类添加 `EmailAddress` 属性，请再次运行 "学生" 页，然后再次查看表，您将看到一个新的 `EmailAddress` 列。</span><span class="sxs-lookup"><span data-stu-id="035c3-313">For example, if you add an `EmailAddress` property to the `Student` class, run the Students page again, and then look at the table again, you'll see a new `EmailAddress` column.</span></span>

## <a name="conventions"></a><span data-ttu-id="035c3-314">约定</span><span class="sxs-lookup"><span data-stu-id="035c3-314">Conventions</span></span>

<span data-ttu-id="035c3-315">您必须编写的代码量，以便实体框架能够为您创建完整数据库，这是因为*约定*或实体框架所做的假设。</span><span class="sxs-lookup"><span data-stu-id="035c3-315">The amount of code you had to write in order for Entity Framework to be able to create a complete database for you is minimal because of *conventions*, or assumptions that Entity Framework makes.</span></span> <span data-ttu-id="035c3-316">其中一些内容已经过说明，或已被使用，无需注意它们：</span><span class="sxs-lookup"><span data-stu-id="035c3-316">Some of them have already been noted or were used without your being aware of them:</span></span>

- <span data-ttu-id="035c3-317">实体类名称的复数形式用作表名称。</span><span class="sxs-lookup"><span data-stu-id="035c3-317">The pluralized forms of entity class names are used as table names.</span></span>
- <span data-ttu-id="035c3-318">使用实体属性名作为列名。</span><span class="sxs-lookup"><span data-stu-id="035c3-318">Entity property names are used for column names.</span></span>
- <span data-ttu-id="035c3-319">命名为 `ID` 或*classname* `ID` 的实体属性被识别为主键属性。</span><span class="sxs-lookup"><span data-stu-id="035c3-319">Entity properties that are named `ID` or *classname* `ID` are recognized as primary key properties.</span></span>
- <span data-ttu-id="035c3-320">如果属性命名为 *&lt;导航属性名称&gt;&lt;primary key 属性名称&gt;* （例如 `StudentID` 导航属性 `Student`，因为 `Student` 实体的主键是 `ID`），则该属性将被解释为外键属性。</span><span class="sxs-lookup"><span data-stu-id="035c3-320">A property is interpreted as a foreign key property if it's named *&lt;navigation property name&gt;&lt;primary key property name&gt;* (for example, `StudentID` for the `Student` navigation property since the `Student` entity's primary key is `ID`).</span></span> <span data-ttu-id="035c3-321">也可以将外键属性命名为相同 &lt;主键属性名称&gt; （例如 `EnrollmentID`，因为 `Enrollment` 实体的主键是 `EnrollmentID`）。</span><span class="sxs-lookup"><span data-stu-id="035c3-321">Foreign key properties can also be named the same simply &lt;primary key property name&gt; (for example, `EnrollmentID` since the `Enrollment` entity's primary key is `EnrollmentID`).</span></span>

<span data-ttu-id="035c3-322">你已了解到可以重写约定。</span><span class="sxs-lookup"><span data-stu-id="035c3-322">You've seen that conventions can be overridden.</span></span> <span data-ttu-id="035c3-323">例如，你指定了表名不应为复数，稍后你将看到如何将属性显式标记为外键属性。</span><span class="sxs-lookup"><span data-stu-id="035c3-323">For example, you specified that table names shouldn't be pluralized, and you'll see later how to explicitly mark a property as a foreign key property.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="035c3-324">获取代码</span><span class="sxs-lookup"><span data-stu-id="035c3-324">Get the code</span></span>

[<span data-ttu-id="035c3-325">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="035c3-325">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="035c3-326">其他资源</span><span class="sxs-lookup"><span data-stu-id="035c3-326">Additional resources</span></span>

<span data-ttu-id="035c3-327">有关 EF 6 的详细信息，请参阅以下文章：</span><span class="sxs-lookup"><span data-stu-id="035c3-327">For more about EF 6, see these articles:</span></span>

* [<span data-ttu-id="035c3-328">ASP.NET 数据访问 - 推荐的资源</span><span class="sxs-lookup"><span data-stu-id="035c3-328">ASP.NET Data Access - Recommended Resources</span></span>](../../../../whitepapers/aspnet-data-access-content-map.md)

* [<span data-ttu-id="035c3-329">Code First 约定</span><span class="sxs-lookup"><span data-stu-id="035c3-329">Code First Conventions</span></span>](/ef/ef6/modeling/code-first/conventions/built-in)

* [<span data-ttu-id="035c3-330">创建更复杂的数据模型</span><span class="sxs-lookup"><span data-stu-id="035c3-330">Creating a More Complex Data Model</span></span>](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a><span data-ttu-id="035c3-331">后续步骤</span><span class="sxs-lookup"><span data-stu-id="035c3-331">Next steps</span></span>

<span data-ttu-id="035c3-332">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="035c3-332">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="035c3-333">创建 MVC web 应用</span><span class="sxs-lookup"><span data-stu-id="035c3-333">Created an MVC web app</span></span>
> * <span data-ttu-id="035c3-334">设置网站样式</span><span class="sxs-lookup"><span data-stu-id="035c3-334">Set up the site style</span></span>
> * <span data-ttu-id="035c3-335">安装实体框架6</span><span class="sxs-lookup"><span data-stu-id="035c3-335">Installed Entity Framework 6</span></span>
> * <span data-ttu-id="035c3-336">已创建数据模型</span><span class="sxs-lookup"><span data-stu-id="035c3-336">Created the data model</span></span>
> * <span data-ttu-id="035c3-337">已创建数据库上下文</span><span class="sxs-lookup"><span data-stu-id="035c3-337">Created the database context</span></span>
> * <span data-ttu-id="035c3-338">已使用测试数据初始化数据库</span><span class="sxs-lookup"><span data-stu-id="035c3-338">Initialized DB with test data</span></span>
> * <span data-ttu-id="035c3-339">设置 EF 6 以使用 LocalDB</span><span class="sxs-lookup"><span data-stu-id="035c3-339">Set up EF 6 to use LocalDB</span></span>
> * <span data-ttu-id="035c3-340">已创建控制器和视图</span><span class="sxs-lookup"><span data-stu-id="035c3-340">Created controller and views</span></span>
> * <span data-ttu-id="035c3-341">已查看数据库</span><span class="sxs-lookup"><span data-stu-id="035c3-341">Viewed the database</span></span>

<span data-ttu-id="035c3-342">转到下一篇文章，了解如何在控制器和视图中查看和自定义创建、读取、更新、删除（CRUD）代码。</span><span class="sxs-lookup"><span data-stu-id="035c3-342">Advance to the next article to learn how to review and customize the create, read, update, delete (CRUD) code in your controllers and views.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="035c3-343">实现基本的 CRUD 功能</span><span class="sxs-lookup"><span data-stu-id="035c3-343">Implement basic CRUD functionality</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)