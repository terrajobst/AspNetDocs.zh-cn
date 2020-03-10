---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: 实体框架4.0 中的新增功能 |Microsoft Docs
author: tdykstra
description: 本教程系列在使用实体框架4.0 教程系列的入门创建的 Contoso 大学 web 应用程序上构建。 I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 29d2bd61e8361b130e7b9415dad4fe1d5b847945
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522146"
---
# <a name="whats-new-in-the-entity-framework-40"></a><span data-ttu-id="1a756-104">Entity Framework 4.0 的新增功能</span><span class="sxs-lookup"><span data-stu-id="1a756-104">What's New in the Entity Framework 4.0</span></span>

<span data-ttu-id="1a756-105">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="1a756-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="1a756-106">本教程系列在[使用实体框架](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)教程系列的入门创建的 Contoso 大学 web 应用程序上构建。</span><span class="sxs-lookup"><span data-stu-id="1a756-106">This tutorial series builds on the Contoso University web application that is created by the [Getting Started with the Entity Framework](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) tutorial series.</span></span> <span data-ttu-id="1a756-107">如果你没有完成前面的教程，作为本教程的起点，你可以下载你要创建[的应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)。</span><span class="sxs-lookup"><span data-stu-id="1a756-107">If you didn't complete the earlier tutorials, as a starting point for this tutorial you can [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) that you would have created.</span></span> <span data-ttu-id="1a756-108">你还可以下载完整的系列教程创建的[应用程序](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa)。</span><span class="sxs-lookup"><span data-stu-id="1a756-108">You can also [download the application](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) that is created by the complete tutorial series.</span></span> <span data-ttu-id="1a756-109">如果有关于这些教程的问题，可以将其发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1a756-109">If you have questions about the tutorials, you can post them to the [ASP.NET Entity Framework forum](https://forums.asp.net/1227.aspx).</span></span>

<span data-ttu-id="1a756-110">在上一教程中，你看到了一些方法，用于最大程度地提高使用实体框架的 web 应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="1a756-110">In the previous tutorial you saw some methods for maximizing the performance of a web application that uses the Entity Framework.</span></span> <span data-ttu-id="1a756-111">本教程回顾实体框架版本4中的一些最重要的新功能，并链接到可提供更完整的所有新功能的资源。</span><span class="sxs-lookup"><span data-stu-id="1a756-111">This tutorial reviews some of the most important new features in version 4 of the Entity Framework, and it links to resources that provide a more complete introduction to all of the new features.</span></span> <span data-ttu-id="1a756-112">本教程中突出显示的功能包括：</span><span class="sxs-lookup"><span data-stu-id="1a756-112">The features highlighted in this tutorial include the following:</span></span>

- <span data-ttu-id="1a756-113">外键关联。</span><span class="sxs-lookup"><span data-stu-id="1a756-113">Foreign-key associations.</span></span>
- <span data-ttu-id="1a756-114">正在执行用户定义的 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="1a756-114">Executing user-defined SQL commands.</span></span>
- <span data-ttu-id="1a756-115">模型优先开发。</span><span class="sxs-lookup"><span data-stu-id="1a756-115">Model-first development.</span></span>
- <span data-ttu-id="1a756-116">POCO 支持。</span><span class="sxs-lookup"><span data-stu-id="1a756-116">POCO support.</span></span>

<span data-ttu-id="1a756-117">此外，本教程将简要介绍*代码优先开发*，这是下一版本的实体框架的一项功能。</span><span class="sxs-lookup"><span data-stu-id="1a756-117">In addition, the tutorial will briefly introduce *code-first development*, a feature that's coming in the next release of the Entity Framework.</span></span>

<span data-ttu-id="1a756-118">若要开始学习本教程，请启动 Visual Studio，并打开在上一教程中使用的 Contoso 大学 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1a756-118">To start the tutorial, start Visual Studio and open the Contoso University web application that you were working with in the previous tutorial.</span></span>

## <a name="foreign-key-associations"></a><span data-ttu-id="1a756-119">外键关联</span><span class="sxs-lookup"><span data-stu-id="1a756-119">Foreign-Key Associations</span></span>

<span data-ttu-id="1a756-120">实体框架的3.5 版包含导航属性，但它不包括数据模型中的外键属性。</span><span class="sxs-lookup"><span data-stu-id="1a756-120">Version 3.5 of the Entity Framework included navigation properties, but it didn't include foreign-key properties in the data model.</span></span> <span data-ttu-id="1a756-121">例如，`StudentGrade` 实体中将省略 `StudentGrade` 表的 `CourseID` 和 `StudentID` 列。</span><span class="sxs-lookup"><span data-stu-id="1a756-121">For example, the `CourseID` and `StudentID` columns of the `StudentGrade` table would be omitted from the `StudentGrade` entity.</span></span>

<span data-ttu-id="1a756-122">[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-122">[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)</span></span>

<span data-ttu-id="1a756-123">此方法的原因在于，严格地说，外键是物理实现细节，不属于概念数据模型。</span><span class="sxs-lookup"><span data-stu-id="1a756-123">The reason for this approach was that, strictly speaking, foreign keys are a physical implementation detail and don't belong in a conceptual data model.</span></span> <span data-ttu-id="1a756-124">但实际上，当你具有对外键的直接访问权限时，通常可以更轻松地在代码中处理实体。</span><span class="sxs-lookup"><span data-stu-id="1a756-124">However, as a practical matter, it's often easier to work with entities in code when you have direct access to the foreign keys.</span></span>

<span data-ttu-id="1a756-125">有关如何使用数据模型中的外键来简化代码的示例，请考虑在没有这些外键的情况下，你必须如何编码*DepartmentsAdd*页。</span><span class="sxs-lookup"><span data-stu-id="1a756-125">For an example of how foreign keys in the data model can simplify your code, consider how you would have had to code the *DepartmentsAdd.aspx* page without them.</span></span> <span data-ttu-id="1a756-126">在 `Department` 实体中，`Administrator` 属性是与 `Person` 实体中 `PersonID` 对应的外键。</span><span class="sxs-lookup"><span data-stu-id="1a756-126">In the `Department` entity, the `Administrator` property is a foreign key that corresponds to `PersonID` in the `Person` entity.</span></span> <span data-ttu-id="1a756-127">若要在新的部门及其管理员之间建立关联，只需要在数据绑定控件的 `ItemInserting` 事件处理程序中设置 "`Administrator`" 属性的值：</span><span class="sxs-lookup"><span data-stu-id="1a756-127">In order to establish the association between a new department and its administrator, all you had to do was set the value for the `Administrator` property in the `ItemInserting` event handler of the databound control:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

<span data-ttu-id="1a756-128">如果数据模型中没有外键，则需要处理数据源控件的 `Inserting` 事件，而不是数据绑定控件的 `ItemInserting` 事件，以便在将实体添加到实体集之前获取对实体本身的引用。</span><span class="sxs-lookup"><span data-stu-id="1a756-128">Without foreign keys in the data model, you'd handle the `Inserting` event of the data source control instead of the `ItemInserting` event of the databound control, in order to get a reference to the entity itself before the entity is added to the entity set.</span></span> <span data-ttu-id="1a756-129">使用该引用时，可以使用类似于以下示例的代码建立关联：</span><span class="sxs-lookup"><span data-stu-id="1a756-129">When you have that reference, you establish the association using code like that in the following examples:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

<span data-ttu-id="1a756-130">正如你在实体框架团队的[有关外键关联的博客文章](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)中所看到的，在其他情况下，代码复杂性的差异要大得多。</span><span class="sxs-lookup"><span data-stu-id="1a756-130">As you can see in the Entity Framework team's [blog post on Foreign Key associations](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx), there are other cases where the difference in code complexity is much greater.</span></span> <span data-ttu-id="1a756-131">为了满足更简单代码的概念数据模型中更喜欢使用实现细节的用户的需求，实体框架现在提供了在数据模型中包括外键的选项。</span><span class="sxs-lookup"><span data-stu-id="1a756-131">To meet the needs of those who prefer to live with implementation details in the conceptual data model for the sake of simpler code, the Entity Framework now gives you the option of including foreign keys in the data model.</span></span>

<span data-ttu-id="1a756-132">在实体框架术语中，如果你在使用*外键关联*的数据模型中包含外键，并且你排除使用*独立关联*的外键，则为。</span><span class="sxs-lookup"><span data-stu-id="1a756-132">In Entity Framework terminology, if you include foreign keys in the data model you're using *foreign key associations*, and if you exclude foreign keys you're using *independent associations*.</span></span>

## <a name="executing-user-defined-sql-commands"></a><span data-ttu-id="1a756-133">执行用户定义的 SQL 命令</span><span class="sxs-lookup"><span data-stu-id="1a756-133">Executing User-Defined SQL Commands</span></span>

<span data-ttu-id="1a756-134">在实体框架的早期版本中，不能轻松地创建自己的 SQL 命令并运行这些命令。</span><span class="sxs-lookup"><span data-stu-id="1a756-134">In earlier versions of the Entity Framework, there was no easy way to create your own SQL commands on the fly and run them.</span></span> <span data-ttu-id="1a756-135">实体框架为您动态生成 SQL 命令，或者您必须创建一个存储过程并将其作为函数导入。</span><span class="sxs-lookup"><span data-stu-id="1a756-135">Either the Entity Framework dynamically generated SQL commands for you, or you had to create a stored procedure and import it as a function.</span></span> <span data-ttu-id="1a756-136">版本4添加了 `ObjectContext` 类 `ExecuteStoreQuery` 和 `ExecuteStoreCommand` 方法，使您可以更轻松地将任何查询直接传递到数据库。</span><span class="sxs-lookup"><span data-stu-id="1a756-136">Version 4 adds `ExecuteStoreQuery` and `ExecuteStoreCommand` methods the `ObjectContext` class that make it easier for you to pass any query directly to the database.</span></span>

<span data-ttu-id="1a756-137">假设 Contoso 大学管理员希望能够在数据库中执行大容量更改，而不必完成创建存储过程并将其导入到数据模型中的过程。</span><span class="sxs-lookup"><span data-stu-id="1a756-137">Suppose Contoso University administrators want to be able to perform bulk changes in the database without having to go through the process of creating a stored procedure and importing it into the data model.</span></span> <span data-ttu-id="1a756-138">它们的第一个请求是针对页面，使其可以更改数据库中所有课程的信用额度。</span><span class="sxs-lookup"><span data-stu-id="1a756-138">Their first request is for a page that lets them change the number of credits for all courses in the database.</span></span> <span data-ttu-id="1a756-139">在网页上，他们希望能够输入一个数字，用来将每个 `Course` 行 `Credits` 列的值相乘。</span><span class="sxs-lookup"><span data-stu-id="1a756-139">On the web page, they want to be able to enter a number to use to multiply the value of every `Course` row's `Credits` column.</span></span>

<span data-ttu-id="1a756-140">创建一个使用*网站母版页*的新页面，并将其命名为*UpdateCredits*。</span><span class="sxs-lookup"><span data-stu-id="1a756-140">Create a new page that uses the *Site.Master* master page and name it *UpdateCredits.aspx*.</span></span> <span data-ttu-id="1a756-141">然后，将以下标记添加到名为 `Content2`的 `Content` 控件：</span><span class="sxs-lookup"><span data-stu-id="1a756-141">Then add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

<span data-ttu-id="1a756-142">此标记创建一个 `TextBox` 控件，用户可在其中输入乘数值、要单击以执行命令的 `Button` 控件，以及指示受影响的行数的 `Label` 控件。</span><span class="sxs-lookup"><span data-stu-id="1a756-142">This markup creates a `TextBox` control in which the user can enter the multiplier value, a `Button` control to click in order to execute the command, and a `Label` control for indicating the number of rows affected.</span></span>

<span data-ttu-id="1a756-143">打开*UpdateCredits.aspx.cs*，并为按钮的 `Click` 事件添加以下 `using` 语句和处理程序：</span><span class="sxs-lookup"><span data-stu-id="1a756-143">Open *UpdateCredits.aspx.cs*, and add the following `using` statement and a handler for the button's `Click` event:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

<span data-ttu-id="1a756-144">此代码使用文本框中的值执行 SQL `Update` 命令，并使用标签显示受影响的行数。</span><span class="sxs-lookup"><span data-stu-id="1a756-144">This code executes the SQL `Update` command using the value in the text box and uses the label to display the number of rows affected.</span></span> <span data-ttu-id="1a756-145">在运行页面之前，请运行 "*课程 .aspx* " 页，获取一些数据的 "之前" 图片。</span><span class="sxs-lookup"><span data-stu-id="1a756-145">Before you run the page, run the *Courses.aspx* page to get a "before" picture of some data.</span></span>

<span data-ttu-id="1a756-146">[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-146">[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)</span></span>

<span data-ttu-id="1a756-147">运行*UpdateCredits*，输入 "10" 作为乘数，然后单击 "**执行**"。</span><span class="sxs-lookup"><span data-stu-id="1a756-147">Run *UpdateCredits.aspx*, enter "10" as the multiplier, and then click **Execute**.</span></span>

<span data-ttu-id="1a756-148">[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-148">[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)</span></span>

<span data-ttu-id="1a756-149">再次运行 "*课程 .aspx* " 页以查看更改后的数据。</span><span class="sxs-lookup"><span data-stu-id="1a756-149">Run the *Courses.aspx* page again to see the changed data.</span></span>

<span data-ttu-id="1a756-150">[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-150">[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)</span></span>

<span data-ttu-id="1a756-151">（如果要将富余点数设置回其原始值，请在 " *UpdateCredits.aspx.cs*更改 `Credits * {0}`" 中 `Credits / {0}` 并重新运行该页面，输入10作为除数。）</span><span class="sxs-lookup"><span data-stu-id="1a756-151">(If you want to set the number of credits back to their original values, in *UpdateCredits.aspx.cs* change `Credits * {0}` to `Credits / {0}` and re-run the page, entering 10 as the divisor.)</span></span>

<span data-ttu-id="1a756-152">有关执行在代码中定义的查询的详细信息，请参阅[如何：直接对数据源执行命令](https://msdn.microsoft.com/library/ee358769.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1a756-152">For more information about executing queries that you define in code, see [How to: Directly Execute Commands Against the Data Source](https://msdn.microsoft.com/library/ee358769.aspx).</span></span>

## <a name="model-first-development"></a><span data-ttu-id="1a756-153">模型优先开发</span><span class="sxs-lookup"><span data-stu-id="1a756-153">Model-First Development</span></span>

<span data-ttu-id="1a756-154">在这些演练中，首先创建了数据库，然后根据数据库结构生成了数据模型。</span><span class="sxs-lookup"><span data-stu-id="1a756-154">In these walkthroughs you created the database first and then generated the data model based on the database structure.</span></span> <span data-ttu-id="1a756-155">在实体框架4中，可以改为从数据模型开始，并基于数据模型结构生成数据库。</span><span class="sxs-lookup"><span data-stu-id="1a756-155">In the Entity Framework 4 you can start with the data model instead and generate the database based on the data model structure.</span></span> <span data-ttu-id="1a756-156">如果创建的应用程序数据库尚不存在，则使用模型优先方法可以创建在概念上适用于该应用程序的实体和关系，而无需担心物理实现细节.</span><span class="sxs-lookup"><span data-stu-id="1a756-156">If you're creating an application for which the database doesn't already exist, the model-first approach enables you to create entities and relationships that make sense conceptually for the application, while not worrying about physical implementation details.</span></span> <span data-ttu-id="1a756-157">（不过，这一点仅通过开发的初始阶段才适用。</span><span class="sxs-lookup"><span data-stu-id="1a756-157">(This remains true only through the initial stages of development, however.</span></span> <span data-ttu-id="1a756-158">最终会创建数据库，并在其中包含生产数据，并从模型重新创建该数据库将不再可行;此时，您将返回到数据库优先的方法。）</span><span class="sxs-lookup"><span data-stu-id="1a756-158">Eventually the database will be created and will have production data in it, and recreating it from the model will no longer be practical; at that point you'll be back to the database-first approach.)</span></span>

<span data-ttu-id="1a756-159">在本教程的此部分中，你将创建一个简单的数据模型，并从该模型生成数据库。</span><span class="sxs-lookup"><span data-stu-id="1a756-159">In this section of the tutorial, you'll create a simple data model and generate the database from it.</span></span>

<span data-ttu-id="1a756-160">在**解决方案资源管理器**中，右键单击*DAL*文件夹，然后选择 "**添加新项**"。</span><span class="sxs-lookup"><span data-stu-id="1a756-160">In **Solution Explorer**, right-click the *DAL* folder and select **Add New Item**.</span></span> <span data-ttu-id="1a756-161">在 "**添加新项**" 对话框中，在 "**已安装的模板**" 下选择 "**数据**"，然后选择 " **ADO.NET 实体数据模型**" 模板。</span><span class="sxs-lookup"><span data-stu-id="1a756-161">In the **Add New Item** dialog box, under **Installed Templates** select **Data** and then select the **ADO.NET Entity Data Model** template.</span></span> <span data-ttu-id="1a756-162">将新文件命名为*AlumniAssociationModel* ，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="1a756-162">Name the new file *AlumniAssociationModel.edmx* and click **Add**.</span></span>

<span data-ttu-id="1a756-163">[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-163">[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)</span></span>

<span data-ttu-id="1a756-164">这将启动实体数据模型向导。</span><span class="sxs-lookup"><span data-stu-id="1a756-164">This launches the Entity Data Model Wizard.</span></span> <span data-ttu-id="1a756-165">在 "**选择模型内容**" 步骤中，选择 "**空模型**"，然后单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="1a756-165">In the **Choose Model Contents** step, select **Empty Model** and then click **Finish**.</span></span>

<span data-ttu-id="1a756-166">[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-166">[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)</span></span>

<span data-ttu-id="1a756-167">此时将打开**实体数据模型设计器**，其中显示一个空白设计图面。</span><span class="sxs-lookup"><span data-stu-id="1a756-167">The **Entity Data Model Designer** opens with a blank design surface.</span></span> <span data-ttu-id="1a756-168">将一个**实体**项从**工具箱**拖到设计图面上。</span><span class="sxs-lookup"><span data-stu-id="1a756-168">Drag an **Entity** item from the **Toolbox** onto the design surface.</span></span>

<span data-ttu-id="1a756-169">[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-169">[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)</span></span>

<span data-ttu-id="1a756-170">将实体名称从 `Entity1` 更改为 `Alumnus`，将 `Id` 属性名称更改为 `AlumnusId`，并添加名为 `Name`的新标量属性。</span><span class="sxs-lookup"><span data-stu-id="1a756-170">Change the entity name from `Entity1` to `Alumnus`, change the `Id` property name to `AlumnusId`, and add a new scalar property named `Name`.</span></span> <span data-ttu-id="1a756-171">若要添加新属性，可在更改 `Id` 列的名称后按 Enter，或右键单击该实体并选择 "**添加标量属性**"。</span><span class="sxs-lookup"><span data-stu-id="1a756-171">To add new properties you can press Enter after changing the name of the `Id` column, or right-click the entity and select **Add Scalar Property**.</span></span> <span data-ttu-id="1a756-172">新属性的默认类型为 `String`，这对于这一简单的演示非常不错，但您也可以在 "**属性**" 窗口中更改数据类型等。</span><span class="sxs-lookup"><span data-stu-id="1a756-172">The default type for new properties is `String`, which is fine for this simple demonstration, but of course you can change things like data type in the **Properties** window.</span></span>

<span data-ttu-id="1a756-173">以相同的方式创建另一个实体，并将其命名 `Donation`。</span><span class="sxs-lookup"><span data-stu-id="1a756-173">Create another entity the same way and name it `Donation`.</span></span> <span data-ttu-id="1a756-174">将 `Id` 属性更改为 `DonationId` 并添加一个名为 `DateAndAmount`的标量属性。</span><span class="sxs-lookup"><span data-stu-id="1a756-174">Change the `Id` property to `DonationId` and add a scalar property named `DateAndAmount`.</span></span>

<span data-ttu-id="1a756-175">[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-175">[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)</span></span>

<span data-ttu-id="1a756-176">若要添加这两个实体之间的关联，请右键单击 `Alumnus` 实体，选择 "**添加**"，然后选择 "**关联**"。</span><span class="sxs-lookup"><span data-stu-id="1a756-176">To add an association between these two entities, right-click the `Alumnus` entity, select **Add**, and then select **Association**.</span></span>

<span data-ttu-id="1a756-177">[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-177">[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)</span></span>

<span data-ttu-id="1a756-178">"**添加关联**" 对话框中的默认值是你想要的内容（一对多，包括导航属性，包括外键），因此只需单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="1a756-178">The default values in the **Add Association** dialog box are what you want (one-to-many, include navigation properties, include foreign keys), so just click **OK**.</span></span>

<span data-ttu-id="1a756-179">[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-179">[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)</span></span>

<span data-ttu-id="1a756-180">设计器添加关联连线和外键属性。</span><span class="sxs-lookup"><span data-stu-id="1a756-180">The designer adds an association line and a foreign-key property.</span></span>

<span data-ttu-id="1a756-181">[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-181">[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)</span></span>

<span data-ttu-id="1a756-182">现在，可以创建数据库了。</span><span class="sxs-lookup"><span data-stu-id="1a756-182">Now you're ready to create the database.</span></span> <span data-ttu-id="1a756-183">右键单击设计图面，然后选择 "**从模型生成数据库**"。</span><span class="sxs-lookup"><span data-stu-id="1a756-183">Right-click the design surface and select **Generate Database from Model**.</span></span>

<span data-ttu-id="1a756-184">[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-184">[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)</span></span>

<span data-ttu-id="1a756-185">这将启动 "生成数据库向导"。</span><span class="sxs-lookup"><span data-stu-id="1a756-185">This launches the Generate Database Wizard.</span></span> <span data-ttu-id="1a756-186">（如果您看到指示实体未映射的警告，则可以忽略这些实体。）</span><span class="sxs-lookup"><span data-stu-id="1a756-186">(If you see warnings that indicate that the entities aren't mapped, you can ignore those for the time being.)</span></span>

<span data-ttu-id="1a756-187">在 "**选择你的数据连接**" 步骤中，单击 "**新建连接**"。</span><span class="sxs-lookup"><span data-stu-id="1a756-187">In the **Choose Your Data Connection** step, click **New Connection**.</span></span>

<span data-ttu-id="1a756-188">[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-188">[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)</span></span>

<span data-ttu-id="1a756-189">在 "**连接属性**" 对话框中，选择本地 SQL Server Express 实例，并将数据库命名为 `AlumniAssociation`。</span><span class="sxs-lookup"><span data-stu-id="1a756-189">In the **Connection Properties** dialog box, select the local SQL Server Express instance and name the database `AlumniAssociation`.</span></span>

<span data-ttu-id="1a756-190">[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-190">[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)</span></span>

<span data-ttu-id="1a756-191">当系统询问您是否要创建数据库时，请单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="1a756-191">Click **Yes** when you're asked if you want to create the database.</span></span> <span data-ttu-id="1a756-192">再次显示 "**选择数据连接**" 步骤时，单击 "**下一**步"。</span><span class="sxs-lookup"><span data-stu-id="1a756-192">When the **Choose Your Data Connection** step is displayed again, click **Next**.</span></span>

<span data-ttu-id="1a756-193">在 "**摘要和设置**" 步骤中，单击 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="1a756-193">In the **Summary and Settings** step, click **Finish**.</span></span>

<span data-ttu-id="1a756-194">[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-194">[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)</span></span>

<span data-ttu-id="1a756-195">已创建包含数据定义语言（DDL）命令的 *.sql*文件，但尚未运行这些命令。</span><span class="sxs-lookup"><span data-stu-id="1a756-195">A *.sql* file with the data definition language (DDL) commands is created, but the commands haven't been run yet.</span></span>

<span data-ttu-id="1a756-196">[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-196">[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)</span></span>

<span data-ttu-id="1a756-197">使用诸如**SQL Server Management Studio**之类的工具运行脚本和创建表，就像你在为[入门教程系列中的第一个教程](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)创建 `School` 数据库时所做的那样。</span><span class="sxs-lookup"><span data-stu-id="1a756-197">Use a tool such as **SQL Server Management Studio** to run the script and create the tables, as you might have done when you created the `School` database for [the first tutorial in the Getting Started tutorial series](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md).</span></span> <span data-ttu-id="1a756-198">（除非已下载数据库。）</span><span class="sxs-lookup"><span data-stu-id="1a756-198">(Unless you downloaded the database.)</span></span>

<span data-ttu-id="1a756-199">现在，你可以在网页中使用 `AlumniAssociation` 数据模型，就像使用 `School` 模型一样。</span><span class="sxs-lookup"><span data-stu-id="1a756-199">You can now use the `AlumniAssociation` data model in your web pages the same way you've been using the `School` model.</span></span> <span data-ttu-id="1a756-200">为此，请将一些数据添加到表中，并创建一个显示数据的网页。</span><span class="sxs-lookup"><span data-stu-id="1a756-200">To try this out, add some data to the tables and create a web page that displays the data.</span></span>

<span data-ttu-id="1a756-201">使用**服务器资源管理器**将以下行添加到 `Alumnus` 并 `Donation` 表中。</span><span class="sxs-lookup"><span data-stu-id="1a756-201">Using **Server Explorer**, add the following rows to the `Alumnus` and `Donation` tables.</span></span>

<span data-ttu-id="1a756-202">[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-202">[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)</span></span>

<span data-ttu-id="1a756-203">创建一个使用校友*母版页的*名为的新网页。</span><span class="sxs-lookup"><span data-stu-id="1a756-203">Create a new web page named *Alumni.aspx* that uses the *Site.Master* master page.</span></span> <span data-ttu-id="1a756-204">将以下标记添加到名为 `Content2`的 `Content` 控件：</span><span class="sxs-lookup"><span data-stu-id="1a756-204">Add the following markup to the `Content` control named `Content2`:</span></span>

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

<span data-ttu-id="1a756-205">此标记创建嵌套 `GridView` 控件，外部控件用于显示校友的名称和内部控件，以显示捐赠日期和金额。</span><span class="sxs-lookup"><span data-stu-id="1a756-205">This markup creates nested `GridView` controls, the outer one to display alumni names and the inner one to display donation dates and amounts.</span></span>

<span data-ttu-id="1a756-206">打开*Alumni.aspx.cs*。</span><span class="sxs-lookup"><span data-stu-id="1a756-206">Open *Alumni.aspx.cs*.</span></span> <span data-ttu-id="1a756-207">添加数据访问层的 `using` 语句，并为外部 `GridView` 控件的 `RowDataBound` 事件添加处理程序：</span><span class="sxs-lookup"><span data-stu-id="1a756-207">Add a `using` statement for the data access layer and a handler for the outer `GridView` control's `RowDataBound` event:</span></span>

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

<span data-ttu-id="1a756-208">此代码使用当前行的 `Alumnus` 实体的 `Donations` 导航属性 databinds 内部 `GridView` 控件。</span><span class="sxs-lookup"><span data-stu-id="1a756-208">This code databinds the inner `GridView` control using the `Donations` navigation property of the current row's `Alumnus` entity.</span></span>

<span data-ttu-id="1a756-209">运行页面。</span><span class="sxs-lookup"><span data-stu-id="1a756-209">Run the page.</span></span>

<span data-ttu-id="1a756-210">[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)</span><span class="sxs-lookup"><span data-stu-id="1a756-210">[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)</span></span>

<span data-ttu-id="1a756-211">（注意：可下载的项目中包含此页，但要使其正常工作，必须在本地 SQL Server Express 实例中创建数据库; 该数据库不作为*应用\_数据*文件夹中的 *.mdf*文件包含。）</span><span class="sxs-lookup"><span data-stu-id="1a756-211">(Note: This page is included in the downloadable project, but to make it work you must create the database in your local SQL Server Express instance; the database isn't included as an *.mdf* file in the *App\_Data* folder.)</span></span>

<span data-ttu-id="1a756-212">有关使用实体框架的模型优先功能的详细信息，请参阅[实体框架4中的 "模型优先](https://msdn.microsoft.com/data/ff830362.aspx)"。</span><span class="sxs-lookup"><span data-stu-id="1a756-212">For more information about using the model-first feature of the Entity Framework, see [Model-First in the Entity Framework 4](https://msdn.microsoft.com/data/ff830362.aspx).</span></span>

## <a name="poco-support"></a><span data-ttu-id="1a756-213">POCO 支持</span><span class="sxs-lookup"><span data-stu-id="1a756-213">POCO Support</span></span>

<span data-ttu-id="1a756-214">使用域驱动的设计方法时，可以设计数据类，这些类表示与业务域相关的数据和行为。</span><span class="sxs-lookup"><span data-stu-id="1a756-214">When you use domain-driven design methodology, you design data classes that represent data and behavior that's relevant to the business domain.</span></span> <span data-ttu-id="1a756-215">这些类应独立于用于存储（持久）数据的任何特定技术;换言之，它们应该是*持久性未知*的。</span><span class="sxs-lookup"><span data-stu-id="1a756-215">These classes should be independent of any specific technology used to store (persist) the data; in other words, they should be *persistence ignorant*.</span></span> <span data-ttu-id="1a756-216">持久性无感知还可以使类更易于进行单元测试，因为单元测试项目可以使用最方便测试的任何持久性技术。</span><span class="sxs-lookup"><span data-stu-id="1a756-216">Persistence ignorance can also make a class easier to unit test because the unit test project can use whatever persistence technology is most convenient for testing.</span></span> <span data-ttu-id="1a756-217">早期版本的实体框架提供对持久性无感知的有限支持，因为实体类必须继承自 `EntityObject` 类，因此包含大量实体框架特定的功能。</span><span class="sxs-lookup"><span data-stu-id="1a756-217">Earlier versions of the Entity Framework offered limited support for persistence ignorance because entity classes had to inherit from the `EntityObject` class and thus included a great deal of Entity Framework-specific functionality.</span></span>

<span data-ttu-id="1a756-218">实体框架4引入了使用不从 `EntityObject` 类继承的实体类，因而是持久性未知的功能。</span><span class="sxs-lookup"><span data-stu-id="1a756-218">The Entity Framework 4 introduces the ability to use entity classes that don't inherit from the `EntityObject` class and therefore are persistence ignorant.</span></span> <span data-ttu-id="1a756-219">在实体框架的上下文中，通常会将类似于这样的类称为 "*纯旧 CLR 对象*（POCO 或 poco）"。</span><span class="sxs-lookup"><span data-stu-id="1a756-219">In the context of the Entity Framework, classes like this are typically called *plain-old CLR objects* (POCO, or POCOs).</span></span> <span data-ttu-id="1a756-220">您可以手动编写 POCO 类，也可以使用实体框架提供的文本模板转换工具包（T4）模板基于现有数据模型自动生成它们。</span><span class="sxs-lookup"><span data-stu-id="1a756-220">You can write POCO classes manually, or you can automatically generate them based on an existing data model using Text Template Transformation Toolkit (T4) templates provided by the Entity Framework.</span></span>

<span data-ttu-id="1a756-221">有关在实体框架中使用 Poco 的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="1a756-221">For more information about using POCOs in the Entity Framework, see the following resources:</span></span>

- <span data-ttu-id="1a756-222">使用[POCO 实体](https://msdn.microsoft.com/library/dd456853.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1a756-222">[Working with POCO Entities](https://msdn.microsoft.com/library/dd456853.aspx).</span></span> <span data-ttu-id="1a756-223">这是一个 MSDN 文档，其中概述了 Poco，并提供了指向更详细信息的其他文档的链接。</span><span class="sxs-lookup"><span data-stu-id="1a756-223">This is an MSDN document that's an overview of POCOs, with links to other documents that have more detailed information.</span></span>
- <span data-ttu-id="1a756-224">[演练：用于实体框架的 POCO 模板](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx)这是来自实体框架开发团队的博客文章，其中提供了有关 Poco 的其他博客文章的链接。</span><span class="sxs-lookup"><span data-stu-id="1a756-224">[Walkthrough: POCO Template for the Entity Framework](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx) This is a blog post from the Entity Framework development team, with links to other blog posts about POCOs.</span></span>

## <a name="code-first-development"></a><span data-ttu-id="1a756-225">代码优先开发</span><span class="sxs-lookup"><span data-stu-id="1a756-225">Code-First Development</span></span>

<span data-ttu-id="1a756-226">实体框架4中的 POCO 支持仍要求您创建一个数据模型，并将实体类链接到数据模型。</span><span class="sxs-lookup"><span data-stu-id="1a756-226">POCO support in the Entity Framework 4 still requires that you create a data model and link your entity classes to the data model.</span></span> <span data-ttu-id="1a756-227">下一版本的实体框架将包括一项名为*代码优先开发*的功能。</span><span class="sxs-lookup"><span data-stu-id="1a756-227">The next release of the Entity Framework will include a feature called *code-first development*.</span></span> <span data-ttu-id="1a756-228">此功能使你能够将实体框架用于自己的 POCO 类，而无需使用数据模型设计器或数据模型 XML 文件。</span><span class="sxs-lookup"><span data-stu-id="1a756-228">This feature enables you to use the Entity Framework with your own POCO classes without needing to use either the data model designer or a data model XML file.</span></span> <span data-ttu-id="1a756-229">（因此，此选项也被称为*仅限代码*;*代码优先*和*仅代码*都引用相同的实体框架功能。）</span><span class="sxs-lookup"><span data-stu-id="1a756-229">(Therefore, this option has also been called *code-only*; *code-first* and *code-only* both refer to the same Entity Framework feature.)</span></span>

<span data-ttu-id="1a756-230">有关使用代码优先方法进行开发的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="1a756-230">For more information about using the code-first approach to development, see the following resources:</span></span>

- <span data-ttu-id="1a756-231">[代码优先开发与实体框架 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1a756-231">[Code-First Development with Entity Framework 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx).</span></span> <span data-ttu-id="1a756-232">这是 Scott Guthrie 的博客文章，其中介绍了代码优先开发。</span><span class="sxs-lookup"><span data-stu-id="1a756-232">This is a blog post by Scott Guthrie introducing code-first development.</span></span>
- [<span data-ttu-id="1a756-233">实体框架开发团队博客-标记为 CodeOnly 的文章</span><span class="sxs-lookup"><span data-stu-id="1a756-233">Entity Framework Development Team Blog - posts tagged CodeOnly</span></span>](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [<span data-ttu-id="1a756-234">实体框架开发团队博客-已标记的文章 Code First</span><span class="sxs-lookup"><span data-stu-id="1a756-234">Entity Framework Development Team Blog - posts tagged Code First</span></span>](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [<span data-ttu-id="1a756-235">MVC 音乐应用商店教程-第4部分：模型和数据访问</span><span class="sxs-lookup"><span data-stu-id="1a756-235">MVC Music Store tutorial - Part 4: Models and Data Access</span></span>](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [<span data-ttu-id="1a756-236">入门 MVC 3-第4部分：实体框架代码优先开发</span><span class="sxs-lookup"><span data-stu-id="1a756-236">Getting Started with MVC 3 - Part 4: Entity Framework Code-First Development</span></span>](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

<span data-ttu-id="1a756-237">此外，还会在[https://asp.net/entity-framework/tutorials](../../../../entity-framework.md) 2011 的弹簧中发布一个新的 MVC 代码优先教程，该教程与 Contoso 大学应用程序类似</span><span class="sxs-lookup"><span data-stu-id="1a756-237">In addition, a new MVC Code-First tutorial that builds an application similar to the Contoso University application is projected to be published in the spring of 2011 at [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)</span></span>

## <a name="more-information"></a><span data-ttu-id="1a756-238">详细信息</span><span class="sxs-lookup"><span data-stu-id="1a756-238">More Information</span></span>

<span data-ttu-id="1a756-239">这将完成实体框架中的新增功能的概述，这将继续学习实体框架教程系列。</span><span class="sxs-lookup"><span data-stu-id="1a756-239">This completes the overview to what's new in the Entity Framework and this Continuing with the Entity Framework tutorial series.</span></span> <span data-ttu-id="1a756-240">有关此处未涵盖的实体框架4中的新功能的详细信息，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="1a756-240">For more information about new features in the Entity Framework 4 that aren't covered here, see the following resources:</span></span>

- <span data-ttu-id="1a756-241">[ADO.NET 中的新增功能](https://msdn.microsoft.com/library/ex6y04yf.aspx)MSDN 主题，介绍实体框架版本4中的新增功能。</span><span class="sxs-lookup"><span data-stu-id="1a756-241">[What's New in ADO.NET](https://msdn.microsoft.com/library/ex6y04yf.aspx) MSDN topic on new features in version 4 of the Entity Framework.</span></span>
- <span data-ttu-id="1a756-242">[宣布发布实体框架 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx)实体框架开发团队的博客文章版本4中的新功能。</span><span class="sxs-lookup"><span data-stu-id="1a756-242">[Announcing the release of Entity Framework 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx) The Entity Framework development team's blog post about new features in version 4.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1a756-243">上一页</span><span class="sxs-lookup"><span data-stu-id="1a756-243">Previous</span></span>](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
