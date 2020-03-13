---
uid: web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
title: 通过模型绑定和 web 窗体检索和显示数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 9f24fb82-c7ac-48da-b8e2-51b3da17e365
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data
msc.type: authoredcontent
ms.openlocfilehash: 81cca22cb4752d071d2a68986ae9ac2bed737594
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520022"
---
# <a name="retrieving-and-displaying-data-with-model-binding-and-web-forms"></a><span data-ttu-id="3770c-104">通过模型绑定和 web 窗体检索和显示数据</span><span class="sxs-lookup"><span data-stu-id="3770c-104">Retrieving and displaying data with model binding and web forms</span></span>

> <span data-ttu-id="3770c-105">本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="3770c-105">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="3770c-106">与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。</span><span class="sxs-lookup"><span data-stu-id="3770c-106">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="3770c-107">此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="3770c-107">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="3770c-108">模型绑定模式适用于任何数据访问技术。</span><span class="sxs-lookup"><span data-stu-id="3770c-108">The model binding pattern works with any data access technology.</span></span> <span data-ttu-id="3770c-109">在本教程中，你将使用实体框架，但你可以使用你最熟悉的数据访问技术。</span><span class="sxs-lookup"><span data-stu-id="3770c-109">In this tutorial, you will use Entity Framework, but you could use the data access technology that is most familiar to you.</span></span> <span data-ttu-id="3770c-110">从数据绑定服务器控件（例如 GridView、ListView、DetailsView 或 FormView 控件），指定用于选择、更新、删除和创建数据的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="3770c-110">From a data-bound server control, such as a GridView, ListView, DetailsView, or FormView control, you specify the names of the methods to use for selecting, updating, deleting, and creating data.</span></span> <span data-ttu-id="3770c-111">在本教程中，您将为 SelectMethod 指定一个值。</span><span class="sxs-lookup"><span data-stu-id="3770c-111">In this tutorial, you will specify a value for the SelectMethod.</span></span> 
> 
> <span data-ttu-id="3770c-112">在该方法中，将提供用于检索数据的逻辑。</span><span class="sxs-lookup"><span data-stu-id="3770c-112">Within that method, you provide the logic for retrieving the data.</span></span> <span data-ttu-id="3770c-113">在下一教程中，你将为 UpdateMethod、DeleteMethod 和 InsertMethod 设置值。</span><span class="sxs-lookup"><span data-stu-id="3770c-113">In the next tutorial, you will set values for UpdateMethod, DeleteMethod and InsertMethod.</span></span>
>
> <span data-ttu-id="3770c-114">您可以在或 Visual Basic 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。</span><span class="sxs-lookup"><span data-stu-id="3770c-114">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or Visual Basic.</span></span> <span data-ttu-id="3770c-115">可下载的代码适用于 Visual Studio 2012 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="3770c-115">The downloadable code works with Visual Studio 2012 and later.</span></span> <span data-ttu-id="3770c-116">它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2017 模板略有不同。</span><span class="sxs-lookup"><span data-stu-id="3770c-116">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2017 template shown in this tutorial.</span></span>
> 
> <span data-ttu-id="3770c-117">在本教程中，你将在 Visual Studio 中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="3770c-117">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="3770c-118">你还可以将应用程序部署到托管提供程序，并使其在 internet 上可用。</span><span class="sxs-lookup"><span data-stu-id="3770c-118">You can also deploy the application to a hosting provider and make it available over the internet.</span></span> <span data-ttu-id="3770c-119">Microsoft 为提供最多10个网站的免费 web 托管</span><span class="sxs-lookup"><span data-stu-id="3770c-119">Microsoft offers free web hosting for up to 10 web sites in a</span></span>  
> <span data-ttu-id="3770c-120">[免费的 Azure 试用帐户](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。</span><span class="sxs-lookup"><span data-stu-id="3770c-120">[free Azure trial account](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="3770c-121">有关如何将 Visual Studio web 项目部署到 Azure App Service Web Apps 的信息，请参阅[使用 Visual studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)系列。</span><span class="sxs-lookup"><span data-stu-id="3770c-121">For information about how to deploy a Visual Studio web project to Azure App Service Web Apps, see the [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md) series.</span></span> <span data-ttu-id="3770c-122">该教程还演示了如何使用 Entity Framework Code First 迁移将 SQL Server 数据库部署到 Azure SQL 数据库。</span><span class="sxs-lookup"><span data-stu-id="3770c-122">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Azure SQL Database.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="3770c-123">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="3770c-123">Software versions used in the tutorial</span></span>
> 
> - <span data-ttu-id="3770c-124">Microsoft Visual Studio 2017 或 Microsoft Visual Studio Community 2017</span><span class="sxs-lookup"><span data-stu-id="3770c-124">Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017</span></span>
>   
> <span data-ttu-id="3770c-125">本教程还适用于 Visual Studio 2012 和 Visual Studio 2013，但用户界面和项目模板有一些不同之处。</span><span class="sxs-lookup"><span data-stu-id="3770c-125">This tutorial also works with Visual Studio 2012 and Visual Studio 2013, but there are some differences in the user interface and project template.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="3770c-126">要生成的内容</span><span class="sxs-lookup"><span data-stu-id="3770c-126">What you'll build</span></span>

<span data-ttu-id="3770c-127">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="3770c-127">In this tutorial, you'll:</span></span>

* <span data-ttu-id="3770c-128">生成数据对象，这些对象反映了学生注册课程的大学</span><span class="sxs-lookup"><span data-stu-id="3770c-128">Build data objects that reflect a university with students enrolled in courses</span></span>
* <span data-ttu-id="3770c-129">从对象生成数据库表</span><span class="sxs-lookup"><span data-stu-id="3770c-129">Build database tables from the objects</span></span>
* <span data-ttu-id="3770c-130">用测试数据填充数据库</span><span class="sxs-lookup"><span data-stu-id="3770c-130">Populate the database with test data</span></span>
* <span data-ttu-id="3770c-131">在 web 窗体中显示数据</span><span class="sxs-lookup"><span data-stu-id="3770c-131">Display data in a web form</span></span>

## <a name="create-the-project"></a><span data-ttu-id="3770c-132">创建项目</span><span class="sxs-lookup"><span data-stu-id="3770c-132">Create the project</span></span>

1. <span data-ttu-id="3770c-133">在 Visual Studio 2017 中，创建名为**ContosoUniversityModelBinding**的**ASP.NET Web 应用程序（.NET Framework）** 项目。</span><span class="sxs-lookup"><span data-stu-id="3770c-133">In Visual Studio 2017, create a **ASP.NET Web Application (.NET Framework)** project called **ContosoUniversityModelBinding**.</span></span>

   ![创建项目](retrieving-data/_static/image19.png)

2. <span data-ttu-id="3770c-135">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="3770c-135">Select **OK**.</span></span> <span data-ttu-id="3770c-136">此时将显示用于选择模板的对话框。</span><span class="sxs-lookup"><span data-stu-id="3770c-136">The dialog box to select a template appears.</span></span>

   ![选择 web 窗体](retrieving-data/_static/image3.png)

3. <span data-ttu-id="3770c-138">选择 " **Web 窗体**" 模板。</span><span class="sxs-lookup"><span data-stu-id="3770c-138">Select the **Web Forms** template.</span></span> 

4. <span data-ttu-id="3770c-139">如有必要，请将身份验证更改为**单独的用户帐户**。</span><span class="sxs-lookup"><span data-stu-id="3770c-139">If necessary, change the authentication to **Individual User Accounts**.</span></span> 

5. <span data-ttu-id="3770c-140">选择“确定”创建项目。</span><span class="sxs-lookup"><span data-stu-id="3770c-140">Select **OK** to create the project.</span></span>

## <a name="modify-site-appearance"></a><span data-ttu-id="3770c-141">修改站点外观</span><span class="sxs-lookup"><span data-stu-id="3770c-141">Modify site appearance</span></span>

   <span data-ttu-id="3770c-142">进行一些更改，以自定义站点外观。</span><span class="sxs-lookup"><span data-stu-id="3770c-142">Make a few changes to customize site appearance.</span></span> 
   
   1. <span data-ttu-id="3770c-143">打开站点 .Master 文件。</span><span class="sxs-lookup"><span data-stu-id="3770c-143">Open the Site.Master file.</span></span>
   
   2. <span data-ttu-id="3770c-144">更改标题以显示**Contoso 大学**，而不是**我的 ASP.NET 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="3770c-144">Change the title to display **Contoso University** and not **My ASP.NET Application**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample1.aspx?highlight=1)]

   3. <span data-ttu-id="3770c-145">将标题文本从**应用程序名称**更改为**Contoso 大学**。</span><span class="sxs-lookup"><span data-stu-id="3770c-145">Change the header text from **Application name** to **Contoso University**.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample2.aspx?highlight=7)]

   4. <span data-ttu-id="3770c-146">更改导航标题链接到站点相应的链接。</span><span class="sxs-lookup"><span data-stu-id="3770c-146">Change the navigation header links to site appropriate ones.</span></span> 
   
      <span data-ttu-id="3770c-147">删除**关于**和**联系人**的链接，而不是链接到您将创建的**学生**页面。</span><span class="sxs-lookup"><span data-stu-id="3770c-147">Remove the links for **About** and **Contact** and, instead, link to a **Students** page, which you will create.</span></span>

      [!code-aspx-csharp[Main](retrieving-data/samples/sample3.aspx)]

   5. <span data-ttu-id="3770c-148">保存站点。</span><span class="sxs-lookup"><span data-stu-id="3770c-148">Save Site.Master.</span></span>

## <a name="add-a-web-form-to-display-student-data"></a><span data-ttu-id="3770c-149">添加 web 窗体以显示学生数据</span><span class="sxs-lookup"><span data-stu-id="3770c-149">Add a web form to display student data</span></span>

   1. <span data-ttu-id="3770c-150">在**解决方案资源管理器**中，右键单击项目，选择 "**添加**"，然后选择 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="3770c-150">In **Solution Explorer**, right-click your project, select **Add** and then **New Item**.</span></span> 
   
   2. <span data-ttu-id="3770c-151">在 "**添加新项**" 对话框中，选择 "**带有母版页的 Web 窗体**" 模板，**并将其**命名为 "student"。</span><span class="sxs-lookup"><span data-stu-id="3770c-151">In the **Add New Item** dialog box, select the **Web Form with Master Page** template and name it **Students.aspx**.</span></span>

      ![创建页面](retrieving-data/_static/image5.png)

   3. <span data-ttu-id="3770c-153">选择 **添加** 。</span><span class="sxs-lookup"><span data-stu-id="3770c-153">Select **Add**.</span></span>
   
   4. <span data-ttu-id="3770c-154">对于 web 窗体的母版页，选择 "**网站"。**</span><span class="sxs-lookup"><span data-stu-id="3770c-154">For the web form's master page, select **Site.Master**.</span></span>
   
   5. <span data-ttu-id="3770c-155">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="3770c-155">Select **OK**.</span></span>

## <a name="add-the-data-model"></a><span data-ttu-id="3770c-156">添加数据模型</span><span class="sxs-lookup"><span data-stu-id="3770c-156">Add the data model</span></span>

<span data-ttu-id="3770c-157">在 "**模型**" 文件夹中，添加名为**UniversityModels.cs**的类。</span><span class="sxs-lookup"><span data-stu-id="3770c-157">In the **Models** folder, add a class named **UniversityModels.cs**.</span></span>

   1. <span data-ttu-id="3770c-158">右键单击 "**模型**"，依次选择 "**添加**"、"**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="3770c-158">Right-click **Models**, select **Add**, and then **New Item**.</span></span> <span data-ttu-id="3770c-159">“添加新项”对话框随即出现。</span><span class="sxs-lookup"><span data-stu-id="3770c-159">The **Add New Item** dialog box appears.</span></span>

   2. <span data-ttu-id="3770c-160">从左侧导航菜单中，选择 "**代码**"，然后选择 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="3770c-160">From the left navigation menu, select **Code**, then **Class**.</span></span>

      ![创建模型类](retrieving-data/_static/image20.png)

   3. <span data-ttu-id="3770c-162">将类命名为**UniversityModels.cs** ，然后选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="3770c-162">Name the class **UniversityModels.cs** and select **Add**.</span></span>

      <span data-ttu-id="3770c-163">在此文件中，按如下所示定义 `SchoolContext`、`Student`、`Enrollment`和 `Course` 类：</span><span class="sxs-lookup"><span data-stu-id="3770c-163">In this file, define the `SchoolContext`, `Student`, `Enrollment`, and `Course` classes as follows:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample4.cs)]

      <span data-ttu-id="3770c-164">`SchoolContext` 类派生自 `DbContext`，它管理数据库连接和数据中的更改。</span><span class="sxs-lookup"><span data-stu-id="3770c-164">The `SchoolContext` class derives from `DbContext`, which manages the database connection and changes in the data.</span></span>

      <span data-ttu-id="3770c-165">在 `Student` 类中，请注意应用于 `FirstName`、`LastName`和 `Year` 属性的特性。</span><span class="sxs-lookup"><span data-stu-id="3770c-165">In the `Student` class, notice the attributes applied to the `FirstName`, `LastName`, and `Year` properties.</span></span> <span data-ttu-id="3770c-166">本教程将使用这些属性进行数据验证。</span><span class="sxs-lookup"><span data-stu-id="3770c-166">This tutorial uses these attributes for data validation.</span></span> <span data-ttu-id="3770c-167">若要简化代码，只会将这些属性标记为数据验证特性。</span><span class="sxs-lookup"><span data-stu-id="3770c-167">To simplify the code, only these properties are marked with data-validation attributes.</span></span> <span data-ttu-id="3770c-168">在实际项目中，您将验证特性应用到需要验证的所有属性。</span><span class="sxs-lookup"><span data-stu-id="3770c-168">In a real project, you would apply validation attributes to all properties needing validation.</span></span>

   4. <span data-ttu-id="3770c-169">保存 UniversityModels.cs。</span><span class="sxs-lookup"><span data-stu-id="3770c-169">Save UniversityModels.cs.</span></span>

## <a name="set-up-the-database-based-on-classes"></a><span data-ttu-id="3770c-170">基于类设置数据库</span><span class="sxs-lookup"><span data-stu-id="3770c-170">Set up the database based on classes</span></span>

<span data-ttu-id="3770c-171">本教程使用[Code First 迁移](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/)来创建对象和数据库表。</span><span class="sxs-lookup"><span data-stu-id="3770c-171">This tutorial uses [Code First Migrations](https://docs.microsoft.com/ef/ef6/modeling/code-first/migrations/) to create objects and database tables.</span></span> <span data-ttu-id="3770c-172">这些表存储有关学生及其课程的信息。</span><span class="sxs-lookup"><span data-stu-id="3770c-172">These tables store information about the students and their courses.</span></span>

   1. <span data-ttu-id="3770c-173">选择“工具” > “NuGet 包管理器” > “包管理器控制台”。</span><span class="sxs-lookup"><span data-stu-id="3770c-173">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

   2. <span data-ttu-id="3770c-174">在 "**程序包管理器控制台**" 中运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="3770c-174">In **Package Manager Console**, run this command:</span></span>  
      `enable-migrations -ContextTypeName ContosoUniversityModelBinding.Models.SchoolContext`

      <span data-ttu-id="3770c-175">如果该命令成功完成，则会出现一条消息，指出已启用了迁移。</span><span class="sxs-lookup"><span data-stu-id="3770c-175">If the command completes successfully, a message stating migrations have been enabled appears.</span></span>

      ![启用迁移](retrieving-data/_static/image8.png)

      <span data-ttu-id="3770c-177">请注意，已创建一个名为*Configuration.cs*的文件。</span><span class="sxs-lookup"><span data-stu-id="3770c-177">Notice that a file named *Configuration.cs* has been created.</span></span> <span data-ttu-id="3770c-178">`Configuration` 类具有一个 `Seed` 方法，该方法可使用测试数据预先填充数据库表。</span><span class="sxs-lookup"><span data-stu-id="3770c-178">The `Configuration` class has a `Seed` method, which can pre-populate the database tables with test data.</span></span>

## <a name="pre-populate-the-database"></a><span data-ttu-id="3770c-179">预先填充数据库</span><span class="sxs-lookup"><span data-stu-id="3770c-179">Pre-populate the database</span></span>

   1. <span data-ttu-id="3770c-180">打开 Configuration.cs。</span><span class="sxs-lookup"><span data-stu-id="3770c-180">Open Configuration.cs.</span></span>
   
   2. <span data-ttu-id="3770c-181">将以下代码添加到 `Seed` 方法中。</span><span class="sxs-lookup"><span data-stu-id="3770c-181">Add the following code to the `Seed` method.</span></span> <span data-ttu-id="3770c-182">此外，为 `ContosoUniversityModelBinding. Models` 命名空间添加 `using` 语句。</span><span class="sxs-lookup"><span data-stu-id="3770c-182">Also, add a `using` statement for the `ContosoUniversityModelBinding. Models` namespace.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample5.cs)]

   3. <span data-ttu-id="3770c-183">保存 Configuration.cs。</span><span class="sxs-lookup"><span data-stu-id="3770c-183">Save Configuration.cs.</span></span>

   4. <span data-ttu-id="3770c-184">在 "包管理器控制台" 中，运行命令 "**添加迁移初始**"。</span><span class="sxs-lookup"><span data-stu-id="3770c-184">In the Package Manager Console, run the command **add-migration initial**.</span></span>

   5. <span data-ttu-id="3770c-185">运行命令**更新-数据库**。</span><span class="sxs-lookup"><span data-stu-id="3770c-185">Run the command **update-database**.</span></span>

      <span data-ttu-id="3770c-186">如果在运行此命令时收到异常，则 `StudentID` 和 `CourseID` 值可能与 `Seed` 方法值不同。</span><span class="sxs-lookup"><span data-stu-id="3770c-186">If you receive an exception when running this command, the `StudentID` and `CourseID` values might be different from the `Seed` method values.</span></span> <span data-ttu-id="3770c-187">打开这些数据库表，查找 `StudentID` 和 `CourseID`的现有值。</span><span class="sxs-lookup"><span data-stu-id="3770c-187">Open those database tables and find existing values for `StudentID` and `CourseID`.</span></span> <span data-ttu-id="3770c-188">将这些值添加到用于播种 `Enrollments` 表的代码中。</span><span class="sxs-lookup"><span data-stu-id="3770c-188">Add those values to the code for seeding the `Enrollments` table.</span></span>

## <a name="add-a-gridview-control"></a><span data-ttu-id="3770c-189">添加 GridView 控件</span><span class="sxs-lookup"><span data-stu-id="3770c-189">Add a GridView control</span></span>

<span data-ttu-id="3770c-190">如果填充了数据库数据，则可以检索并显示数据。</span><span class="sxs-lookup"><span data-stu-id="3770c-190">With populated database data, you're now ready to retrieve that data and display it.</span></span> 

1. <span data-ttu-id="3770c-191">打开 "student"。</span><span class="sxs-lookup"><span data-stu-id="3770c-191">Open Students.aspx.</span></span>

2. <span data-ttu-id="3770c-192">找到 `MainContent` 占位符。</span><span class="sxs-lookup"><span data-stu-id="3770c-192">Locate the `MainContent` placeholder.</span></span> <span data-ttu-id="3770c-193">在该占位符中，添加包含此代码的**GridView**控件。</span><span class="sxs-lookup"><span data-stu-id="3770c-193">Within that placeholder, add a **GridView** control that includes this code.</span></span>

   [!code-aspx-csharp[Main](retrieving-data/samples/sample6.aspx)]

   <span data-ttu-id="3770c-194">注意事项：</span><span class="sxs-lookup"><span data-stu-id="3770c-194">Things to note:</span></span>
   * <span data-ttu-id="3770c-195">请注意为 GridView 元素中的 `SelectMethod` 属性设置的值。</span><span class="sxs-lookup"><span data-stu-id="3770c-195">Notice the value set for the `SelectMethod` property in the GridView element.</span></span> <span data-ttu-id="3770c-196">此值指定用于检索在下一步中创建的 GridView 数据的方法。</span><span class="sxs-lookup"><span data-stu-id="3770c-196">This value specifies the method used to retrieve GridView data, which you create in the next step.</span></span> 
   
   * <span data-ttu-id="3770c-197">`ItemType` 属性设置为前面创建的 `Student` 类。</span><span class="sxs-lookup"><span data-stu-id="3770c-197">The `ItemType` property is set to the `Student` class created earlier.</span></span> <span data-ttu-id="3770c-198">此设置允许你引用标记中的类属性。</span><span class="sxs-lookup"><span data-stu-id="3770c-198">This setting allows you to reference class properties in the markup.</span></span> <span data-ttu-id="3770c-199">例如，`Student` 类具有一个名为 `Enrollments`的集合。</span><span class="sxs-lookup"><span data-stu-id="3770c-199">For example, the `Student` class has a collection named `Enrollments`.</span></span> <span data-ttu-id="3770c-200">您可以使用 `Item.Enrollments` 检索该集合，然后使用[LINQ 语法](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)检索每个学生的已注册信用总数。</span><span class="sxs-lookup"><span data-stu-id="3770c-200">You can use `Item.Enrollments` to retrieve that collection and then use [LINQ syntax](https://docs.microsoft.com/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq) to retrieve each student's enrolled credits sum.</span></span>
   
3. <span data-ttu-id="3770c-201">保存学生 .aspx。</span><span class="sxs-lookup"><span data-stu-id="3770c-201">Save Students.aspx.</span></span>

## <a name="add-code-to-retrieve-data"></a><span data-ttu-id="3770c-202">添加代码以检索数据</span><span class="sxs-lookup"><span data-stu-id="3770c-202">Add code to retrieve data</span></span>

   <span data-ttu-id="3770c-203">在 "student" 代码隐藏文件中，添加为 "`SelectMethod`" 值指定的方法。</span><span class="sxs-lookup"><span data-stu-id="3770c-203">In the Students.aspx code-behind file, add the method specified for the `SelectMethod` value.</span></span> 
   
   1. <span data-ttu-id="3770c-204">打开 Students.aspx.cs。</span><span class="sxs-lookup"><span data-stu-id="3770c-204">Open Students.aspx.cs.</span></span>
   
   2. <span data-ttu-id="3770c-205">为 `ContosoUniversityModelBinding. Models` 和 `System.Data.Entity` 命名空间添加 `using` 语句。</span><span class="sxs-lookup"><span data-stu-id="3770c-205">Add `using` statements for the `ContosoUniversityModelBinding. Models` and `System.Data.Entity` namespaces.</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample7.cs)]

   3. <span data-ttu-id="3770c-206">添加为 `SelectMethod`指定的方法：</span><span class="sxs-lookup"><span data-stu-id="3770c-206">Add the method you specified for `SelectMethod`:</span></span>

      [!code-csharp[Main](retrieving-data/samples/sample8.cs)]

      <span data-ttu-id="3770c-207">`Include` 子句可提高查询性能，但不是必需的。</span><span class="sxs-lookup"><span data-stu-id="3770c-207">The `Include` clause improves query performance but isn't required.</span></span> <span data-ttu-id="3770c-208">如果没有 `Include` 子句，则使用[*延迟加载*](https://en.wikipedia.org/wiki/Lazy_loading)来检索数据，这涉及到每次检索相关数据时向数据库发送一个单独的查询。</span><span class="sxs-lookup"><span data-stu-id="3770c-208">Without the `Include` clause, the data is retrieved using [*lazy loading*](https://en.wikipedia.org/wiki/Lazy_loading), which involves sending a separate query to the database each time related data is retrieved.</span></span> <span data-ttu-id="3770c-209">使用 `Include` 子句时，将使用*预先加载*来检索数据，这意味着单个数据库查询将检索所有相关数据。</span><span class="sxs-lookup"><span data-stu-id="3770c-209">With the `Include` clause, data is retrieved using *eager loading*, which means a single database query retrieves all related data.</span></span> <span data-ttu-id="3770c-210">如果未使用相关数据，预先加载的效率会降低，因为检索到更多的数据。</span><span class="sxs-lookup"><span data-stu-id="3770c-210">If related data isn't used, eager loading is less efficient because more data is retrieved.</span></span> <span data-ttu-id="3770c-211">但在这种情况下，预先加载可提供最佳性能，因为每个记录都显示了相关数据。</span><span class="sxs-lookup"><span data-stu-id="3770c-211">However, in this case, eager loading gives you the best performance because the related data is displayed for each record.</span></span>

      <span data-ttu-id="3770c-212">有关加载相关数据时的性能注意事项的详细信息，请参阅[使用 ASP.NET MVC 应用程序中的实体框架读取相关数据](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)部分中的 "**延迟、预先和显式加载相关**数据" 部分。</span><span class="sxs-lookup"><span data-stu-id="3770c-212">For more information about performance considerations when loading related data, see the **Lazy, Eager, and Explicit Loading of Related Data** section in the [Reading Related Data with the Entity Framework in an ASP.NET MVC Application](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) article.</span></span>

      <span data-ttu-id="3770c-213">默认情况下，数据按标记为键的属性的值进行排序。</span><span class="sxs-lookup"><span data-stu-id="3770c-213">By default, the data is sorted by the values of the property marked as the key.</span></span> <span data-ttu-id="3770c-214">可以添加一个 `OrderBy` 子句来指定其他排序值。</span><span class="sxs-lookup"><span data-stu-id="3770c-214">You can add an `OrderBy` clause to specify a different sort value.</span></span> <span data-ttu-id="3770c-215">在此示例中，将使用默认的 `StudentID` 属性进行排序。</span><span class="sxs-lookup"><span data-stu-id="3770c-215">In this example, the default `StudentID` property is used for sorting.</span></span> <span data-ttu-id="3770c-216">在[排序、分页和筛选数据](sorting-paging-and-filtering-data.md)一文中，用户可以选择要排序的列。</span><span class="sxs-lookup"><span data-stu-id="3770c-216">In the [Sorting, Paging, and Filtering Data](sorting-paging-and-filtering-data.md) article, the user is enabled to select a column for sorting.</span></span>
 
   4. <span data-ttu-id="3770c-217">保存 Students.aspx.cs。</span><span class="sxs-lookup"><span data-stu-id="3770c-217">Save Students.aspx.cs.</span></span>

## <a name="run-your-application"></a><span data-ttu-id="3770c-218">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="3770c-218">Run your application</span></span> 

<span data-ttu-id="3770c-219">运行 web 应用程序（**F5**），并导航到 "**学生**" 页，其中显示了以下内容：</span><span class="sxs-lookup"><span data-stu-id="3770c-219">Run your web application (**F5**) and navigate to the **Students** page, which displays the following:</span></span>

   ![显示数据](retrieving-data/_static/image16.png)

## <a name="automatic-generation-of-model-binding-methods"></a><span data-ttu-id="3770c-221">自动生成模型绑定方法</span><span class="sxs-lookup"><span data-stu-id="3770c-221">Automatic generation of model binding methods</span></span>

<span data-ttu-id="3770c-222">在学习本系列教程时，只需将代码从教程复制到项目即可。</span><span class="sxs-lookup"><span data-stu-id="3770c-222">When working through this tutorial series, you can simply copy the code from the tutorial to your project.</span></span> <span data-ttu-id="3770c-223">但是，这种方法的一个缺点是，你可能不会意识到 Visual Studio 提供的功能自动为模型绑定方法生成代码。</span><span class="sxs-lookup"><span data-stu-id="3770c-223">However, one disadvantage of this approach is that you may not become aware of the feature provided by Visual Studio to automatically generate code for model binding methods.</span></span> <span data-ttu-id="3770c-224">在处理自己的项目时，自动代码生成可以节省时间，并帮助你了解如何实现操作。</span><span class="sxs-lookup"><span data-stu-id="3770c-224">When working on your own projects, automatic code generation can save you time and help you gain a sense of how to implement an operation.</span></span> <span data-ttu-id="3770c-225">本部分介绍自动代码生成功能。</span><span class="sxs-lookup"><span data-stu-id="3770c-225">This section describes the automatic code generation feature.</span></span> <span data-ttu-id="3770c-226">本节仅提供信息，并且不包含你在项目中实现所需的任何代码。</span><span class="sxs-lookup"><span data-stu-id="3770c-226">This section is only informational and does not contain any code you need to implement in your project.</span></span> 

<span data-ttu-id="3770c-227">在标记代码中设置 `SelectMethod`的值、`UpdateMethod`、`InsertMethod`或 `DeleteMethod` 属性时，可以选择 "**创建新方法**" 选项。</span><span class="sxs-lookup"><span data-stu-id="3770c-227">When setting a value for the `SelectMethod`, `UpdateMethod`, `InsertMethod`, or `DeleteMethod` properties in the markup code, you can select the **Create New Method** option.</span></span>

![创建方法](retrieving-data/_static/image18.png)

<span data-ttu-id="3770c-229">Visual Studio 不仅使用正确的签名在代码隐藏中创建方法，而且还会生成执行代码来执行该操作。</span><span class="sxs-lookup"><span data-stu-id="3770c-229">Visual Studio not only creates a method in the code-behind with the proper signature, but also generates implementation code to perform the operation.</span></span> <span data-ttu-id="3770c-230">如果首先在使用自动代码生成功能之前设置 `ItemType` 属性，则生成的代码将使用该类型进行操作。</span><span class="sxs-lookup"><span data-stu-id="3770c-230">If you first set the `ItemType` property before using the automatic code generation feature, the generated code uses that type for the operations.</span></span> <span data-ttu-id="3770c-231">例如，设置 `UpdateMethod` 属性时，将自动生成以下代码：</span><span class="sxs-lookup"><span data-stu-id="3770c-231">For example, when setting the `UpdateMethod` property, the following code is automatically generated:</span></span>

[!code-csharp[Main](retrieving-data/samples/sample9.cs)]

<span data-ttu-id="3770c-232">同样，不需要将此代码添加到您的项目中。</span><span class="sxs-lookup"><span data-stu-id="3770c-232">Again, this code doesn't need to be added to your project.</span></span> <span data-ttu-id="3770c-233">在下一教程中，你将实现用于更新、删除和添加新数据的方法。</span><span class="sxs-lookup"><span data-stu-id="3770c-233">In the next tutorial, you'll implement methods for updating, deleting, and adding new data.</span></span>

## <a name="summary"></a><span data-ttu-id="3770c-234">Summary</span><span class="sxs-lookup"><span data-stu-id="3770c-234">Summary</span></span>

<span data-ttu-id="3770c-235">本教程介绍了如何创建数据模型类，并从这些类生成了数据库。</span><span class="sxs-lookup"><span data-stu-id="3770c-235">In this tutorial, you created data model classes and generated a database from those classes.</span></span> <span data-ttu-id="3770c-236">用测试数据填充数据库表。</span><span class="sxs-lookup"><span data-stu-id="3770c-236">You filled the database tables with test data.</span></span> <span data-ttu-id="3770c-237">你使用了模型绑定从数据库检索数据，然后在 GridView 中显示数据。</span><span class="sxs-lookup"><span data-stu-id="3770c-237">You used model binding to retrieve data from the database, and then displayed the data in a GridView.</span></span>

<span data-ttu-id="3770c-238">在本系列的下一个[教程](updating-deleting-and-creating-data.md)中，你将启用更新、删除和创建数据。</span><span class="sxs-lookup"><span data-stu-id="3770c-238">In the next [tutorial](updating-deleting-and-creating-data.md) in this series, you'll enable updating, deleting, and creating data.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3770c-239">下一页</span><span class="sxs-lookup"><span data-stu-id="3770c-239">Next</span></span>](updating-deleting-and-creating-data.md)
