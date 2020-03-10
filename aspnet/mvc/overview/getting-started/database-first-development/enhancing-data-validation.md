---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 教程：通过 ASP.NET MVC 应用增强 EF Database First 的数据验证
description: 本教程重点介绍如何将数据批注添加到数据模型，以指定验证要求和显示格式。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499532"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a><span data-ttu-id="7fe63-103">教程：通过 ASP.NET MVC 应用增强 EF Database First 的数据验证</span><span class="sxs-lookup"><span data-stu-id="7fe63-103">Tutorial: Enhance data validation for EF Database First with ASP.NET MVC app</span></span>

<span data-ttu-id="7fe63-104">使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。</span><span class="sxs-lookup"><span data-stu-id="7fe63-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="7fe63-105">本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。</span><span class="sxs-lookup"><span data-stu-id="7fe63-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="7fe63-106">生成的代码与数据库表中的列相对应。</span><span class="sxs-lookup"><span data-stu-id="7fe63-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="7fe63-107">本教程重点介绍如何将数据批注添加到数据模型，以指定验证要求和显示格式。</span><span class="sxs-lookup"><span data-stu-id="7fe63-107">This tutorial focuses on adding data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="7fe63-108">它已根据 "评论" 部分中用户的反馈进行了改进。</span><span class="sxs-lookup"><span data-stu-id="7fe63-108">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="7fe63-109">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="7fe63-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7fe63-110">添加数据批注</span><span class="sxs-lookup"><span data-stu-id="7fe63-110">Add data annotations</span></span>
> * <span data-ttu-id="7fe63-111">添加元数据类</span><span class="sxs-lookup"><span data-stu-id="7fe63-111">Add metadata classes</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fe63-112">系统必备</span><span class="sxs-lookup"><span data-stu-id="7fe63-112">Prerequisites</span></span>

* [<span data-ttu-id="7fe63-113">自定义视图</span><span class="sxs-lookup"><span data-stu-id="7fe63-113">Customize a view</span></span>](customizing-a-view.md)

## <a name="add-data-annotations"></a><span data-ttu-id="7fe63-114">添加数据批注</span><span class="sxs-lookup"><span data-stu-id="7fe63-114">Add data annotations</span></span>

<span data-ttu-id="7fe63-115">正如您在前面的主题中看到的那样，某些数据验证规则将自动应用于用户输入。</span><span class="sxs-lookup"><span data-stu-id="7fe63-115">As you saw in an earlier topic, some data validation rules are automatically applied to the user input.</span></span> <span data-ttu-id="7fe63-116">例如，只能为评分属性提供一个数字。</span><span class="sxs-lookup"><span data-stu-id="7fe63-116">For example, you can only provide a number for the Grade property.</span></span> <span data-ttu-id="7fe63-117">若要指定更多的数据验证规则，可以将数据批注添加到模型类。</span><span class="sxs-lookup"><span data-stu-id="7fe63-117">To specify more data validation rules, you can add data annotations to your model class.</span></span> <span data-ttu-id="7fe63-118">在整个 web 应用程序中，为指定的属性应用这些注释。</span><span class="sxs-lookup"><span data-stu-id="7fe63-118">These annotations are applied throughout your web application for the specified property.</span></span> <span data-ttu-id="7fe63-119">还可以应用更改属性显示方式的格式设置属性;例如，更改用于文本标签的值。</span><span class="sxs-lookup"><span data-stu-id="7fe63-119">You can also apply formatting attributes that change how the properties are displayed; such as, changing the value used for text labels.</span></span>

<span data-ttu-id="7fe63-120">在本教程中，您将添加数据批注，以限制为 FirstName、LastName 和 MiddleName 属性提供的值的长度。</span><span class="sxs-lookup"><span data-stu-id="7fe63-120">In this tutorial, you will add data annotations to restrict the length of the values provided for the FirstName, LastName, and MiddleName properties.</span></span> <span data-ttu-id="7fe63-121">在数据库中，这些值限制为50个字符;但是，在 web 应用程序中，当前不强制使用字符限制。</span><span class="sxs-lookup"><span data-stu-id="7fe63-121">In the database, these values are limited to 50 characters; however, in your web application that character limit is currently not enforced.</span></span> <span data-ttu-id="7fe63-122">如果用户为其中一个值提供了超过50个字符，则在尝试将该值保存到数据库时，此页将会崩溃。</span><span class="sxs-lookup"><span data-stu-id="7fe63-122">If a user provides more than 50 characters for one of those values, the page will crash when attempting to save the value to the database.</span></span> <span data-ttu-id="7fe63-123">还会将评分限制为介于0到4之间的值。</span><span class="sxs-lookup"><span data-stu-id="7fe63-123">You will also restrict Grade to values between 0 and 4.</span></span>

<span data-ttu-id="7fe63-124">选择 > **ContosoModel** \*\* > 的\*\* **模型**，并打开*Student.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="7fe63-124">Select **Models** > **ContosoModel.edmx** > **ContosoModel.tt** and open the *Student.cs* file.</span></span> <span data-ttu-id="7fe63-125">将以下突出显示的代码添加到类。</span><span class="sxs-lookup"><span data-stu-id="7fe63-125">Add the following highlighted code to the class.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

<span data-ttu-id="7fe63-126">打开*Enrollment.cs* ，并添加以下突出显示的代码。</span><span class="sxs-lookup"><span data-stu-id="7fe63-126">Open *Enrollment.cs* and add the following highlighted code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

<span data-ttu-id="7fe63-127">生成解决方案。</span><span class="sxs-lookup"><span data-stu-id="7fe63-127">Build the solution.</span></span>

<span data-ttu-id="7fe63-128">单击 "**学生列表**"，然后选择 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="7fe63-128">Click **List of students** and select **Edit**.</span></span> <span data-ttu-id="7fe63-129">如果尝试输入超过50个字符，将显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="7fe63-129">If you attempt to enter more than 50 characters, an error message is displayed.</span></span>

![显示错误消息](enhancing-data-validation/_static/image1.png)

<span data-ttu-id="7fe63-131">返回到主页。</span><span class="sxs-lookup"><span data-stu-id="7fe63-131">Go back to the home page.</span></span> <span data-ttu-id="7fe63-132">单击 "**注册列表**"，然后选择 "**编辑**"。</span><span class="sxs-lookup"><span data-stu-id="7fe63-132">Click **List of enrollments** and select **Edit**.</span></span> <span data-ttu-id="7fe63-133">尝试提供高于4的等级。</span><span class="sxs-lookup"><span data-stu-id="7fe63-133">Attempt to provide a grade above 4.</span></span> <span data-ttu-id="7fe63-134">您将收到此错误：*字段级别必须介于0到4之间。*</span><span class="sxs-lookup"><span data-stu-id="7fe63-134">You will receive this error: *The field Grade must be between 0 and 4.*</span></span>

## <a name="add-metadata-classes"></a><span data-ttu-id="7fe63-135">添加元数据类</span><span class="sxs-lookup"><span data-stu-id="7fe63-135">Add metadata classes</span></span>

<span data-ttu-id="7fe63-136">如果你不希望数据库发生更改，则直接将验证特性添加到模型类会有效：但是，如果您的数据库发生了更改，并且您需要重新生成模型类，则您将丢失已应用于 model 类的所有属性。</span><span class="sxs-lookup"><span data-stu-id="7fe63-136">Adding the validation attributes directly to the model class works when you do not expect the database to change; however, if your database changes and you need to regenerate the model class, you will lose all of the attributes you had applied to the model class.</span></span> <span data-ttu-id="7fe63-137">此方法可能非常低效，并容易丢失重要验证规则。</span><span class="sxs-lookup"><span data-stu-id="7fe63-137">This approach can be very inefficient and prone to losing important validation rules.</span></span>

<span data-ttu-id="7fe63-138">若要避免此问题，可以添加一个包含特性的元数据类。</span><span class="sxs-lookup"><span data-stu-id="7fe63-138">To avoid this problem, you can add a metadata class that contains the attributes.</span></span> <span data-ttu-id="7fe63-139">将模型类关联到 metadata 类时，这些属性将应用于该模型。</span><span class="sxs-lookup"><span data-stu-id="7fe63-139">When you associate the model class to the metadata class, those attributes are applied to the model.</span></span> <span data-ttu-id="7fe63-140">在此方法中，可以重新生成模型类，而不会丢失已应用于元数据类的所有属性。</span><span class="sxs-lookup"><span data-stu-id="7fe63-140">In this approach, the model class can be regenerated without losing all of the attributes that have been applied to the metadata class.</span></span>

<span data-ttu-id="7fe63-141">在 "**模型**" 文件夹中，添加名为*Metadata.cs*的类。</span><span class="sxs-lookup"><span data-stu-id="7fe63-141">In the **Models** folder, add a class named *Metadata.cs*.</span></span>

<span data-ttu-id="7fe63-142">将*Metadata.cs*中的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="7fe63-142">Replace the code in *Metadata.cs* with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

<span data-ttu-id="7fe63-143">这些元数据类包含之前应用于模型类的所有验证特性。</span><span class="sxs-lookup"><span data-stu-id="7fe63-143">These metadata classes contain all of the validation attributes that you had previously applied to the model classes.</span></span> <span data-ttu-id="7fe63-144">**显示**属性用于更改用于文本标签的值。</span><span class="sxs-lookup"><span data-stu-id="7fe63-144">The **Display** attribute is used to change the value used for text labels.</span></span>

<span data-ttu-id="7fe63-145">现在，必须将模型类与元数据类相关联。</span><span class="sxs-lookup"><span data-stu-id="7fe63-145">Now, you must associate the model classes with the metadata classes.</span></span>

<span data-ttu-id="7fe63-146">在 "**模型**" 文件夹中，添加名为*PartialClasses.cs*的类。</span><span class="sxs-lookup"><span data-stu-id="7fe63-146">In the **Models** folder, add a class named *PartialClasses.cs*.</span></span>

<span data-ttu-id="7fe63-147">将文件的内容替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="7fe63-147">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

<span data-ttu-id="7fe63-148">请注意，每个类都标记为 `partial` 类，每个类都将名称和命名空间与自动生成的类相匹配。</span><span class="sxs-lookup"><span data-stu-id="7fe63-148">Notice that each class is marked as a `partial` class, and each matches the name and namespace as the class that is automatically generated.</span></span> <span data-ttu-id="7fe63-149">通过将 metadata 特性应用到分部类，可以确保将数据验证特性应用到自动生成的类。</span><span class="sxs-lookup"><span data-stu-id="7fe63-149">By applying the metadata attribute to the partial class, you ensure that the data validation attributes will be applied to the automatically-generated class.</span></span> <span data-ttu-id="7fe63-150">重新生成模型类时这些属性将不会丢失，因为 metadata 特性应用于不会重新生成的分部类中。</span><span class="sxs-lookup"><span data-stu-id="7fe63-150">These attributes will not be lost when you regenerate the model classes because the metadata attribute is applied in partial classes that are not regenerated.</span></span>

<span data-ttu-id="7fe63-151">若要重新生成自动生成的类，请打开*ContosoModel*文件。</span><span class="sxs-lookup"><span data-stu-id="7fe63-151">To regenerate the automatically-generated classes, open the *ContosoModel.edmx* file.</span></span> <span data-ttu-id="7fe63-152">再次右键单击设计图面，然后选择 "**从数据库更新模型**"。</span><span class="sxs-lookup"><span data-stu-id="7fe63-152">Once again, right-click on the design surface and select **Update Model from Database**.</span></span> <span data-ttu-id="7fe63-153">即使尚未更改数据库，此过程也会重新生成类。</span><span class="sxs-lookup"><span data-stu-id="7fe63-153">Even though you have not changed the database, this process will regenerate the classes.</span></span> <span data-ttu-id="7fe63-154">在 "**刷新**" 选项卡中，选择 "**表**" 和 "**完成**"。</span><span class="sxs-lookup"><span data-stu-id="7fe63-154">In the **Refresh** tab, select **Tables** and **Finish**.</span></span>

<span data-ttu-id="7fe63-155">保存*ContosoModel*文件以应用所做的更改。</span><span class="sxs-lookup"><span data-stu-id="7fe63-155">Save the *ContosoModel.edmx* file to apply the changes.</span></span>

<span data-ttu-id="7fe63-156">打开*Student.cs*文件或*Enrollment.cs*文件，并注意你之前应用的数据验证属性已不再位于文件中。</span><span class="sxs-lookup"><span data-stu-id="7fe63-156">Open the *Student.cs* file or the *Enrollment.cs* file, and notice that the data validation attributes you applied earlier are no longer in the file.</span></span> <span data-ttu-id="7fe63-157">但是，运行应用程序，请注意，当输入数据时，仍然会应用验证规则。</span><span class="sxs-lookup"><span data-stu-id="7fe63-157">However, run the application, and notice that the validation rules are still applied when you enter data.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7fe63-158">结束语</span><span class="sxs-lookup"><span data-stu-id="7fe63-158">Conclusion</span></span>

<span data-ttu-id="7fe63-159">此系列提供了一个简单的示例，说明如何从允许用户编辑、更新、创建和删除数据的现有数据库生成代码。</span><span class="sxs-lookup"><span data-stu-id="7fe63-159">This series provided a simple example of how to generate code from an existing database that enables users to edit, update, create and delete data.</span></span> <span data-ttu-id="7fe63-160">它使用 ASP.NET MVC 5，实体框架和 ASP.NET 基架来创建项目。</span><span class="sxs-lookup"><span data-stu-id="7fe63-160">It used ASP.NET MVC 5, Entity Framework and ASP.NET Scaffolding to create the project.</span></span> 

<span data-ttu-id="7fe63-161">有关 Code First 开发的介绍性示例，请参阅[与 ASP.NET MVC 5 入门](../introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe63-161">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> 

<span data-ttu-id="7fe63-162">有关更高级的示例，请参阅为[ASP.NET MVC 4 应用创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe63-162">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="7fe63-163">请注意，用于在 Database First 中处理数据的 DbContext API 与在 Code First 中处理数据时使用的 API 相同。</span><span class="sxs-lookup"><span data-stu-id="7fe63-163">Note that the DbContext API that you use for working with data in Database First is the same as the API you use for working with data in Code First.</span></span> <span data-ttu-id="7fe63-164">即使你打算使用 Database First，也可以了解如何处理更复杂的方案，例如读取和更新相关数据、处理并发冲突等，以及从 Code First 教程中进行操作。</span><span class="sxs-lookup"><span data-stu-id="7fe63-164">Even if you intend to use Database First, you can learn how to handle more complex scenarios such as reading and updating related data, handling concurrency conflicts, and so forth from a Code First tutorial.</span></span> <span data-ttu-id="7fe63-165">唯一的差别在于如何创建数据库、上下文类和实体类。</span><span class="sxs-lookup"><span data-stu-id="7fe63-165">The only difference is in how the database, context class, and entity classes are created.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7fe63-166">其他资源</span><span class="sxs-lookup"><span data-stu-id="7fe63-166">Additional resources</span></span>

<span data-ttu-id="7fe63-167">有关可应用于属性和类的数据验证批注的完整列表，请参阅[system.componentmodel. DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7fe63-167">For a full list of data validation annotations you can apply to properties and classes, see [System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fe63-168">后续步骤</span><span class="sxs-lookup"><span data-stu-id="7fe63-168">Next steps</span></span>

<span data-ttu-id="7fe63-169">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="7fe63-169">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7fe63-170">添加的数据批注</span><span class="sxs-lookup"><span data-stu-id="7fe63-170">Added data annotations</span></span>
> * <span data-ttu-id="7fe63-171">添加的元数据类</span><span class="sxs-lookup"><span data-stu-id="7fe63-171">Added metadata classes</span></span>

<span data-ttu-id="7fe63-172">若要了解如何将 web 应用和 SQL 数据库部署到 Azure App Service，请参阅本教程：</span><span class="sxs-lookup"><span data-stu-id="7fe63-172">To learn how to deploy a web app and SQL database to Azure App Service, see this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="7fe63-173">将 .NET 应用部署到 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7fe63-173">Deploy a .NET app to Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
