---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第8部分 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示了如何使用实体框架创建 ASP.NET Web 窗体应用程序。 示例应用程序为 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473504"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a><span data-ttu-id="4274f-104">入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体-第8部分</span><span class="sxs-lookup"><span data-stu-id="4274f-104">Getting Started with Entity Framework 4.0 Database First and ASP.NET 4 Web Forms - Part 8</span></span>

<span data-ttu-id="4274f-105">作者： [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4274f-105">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

> <span data-ttu-id="4274f-106">Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="4274f-106">The Contoso University sample web application demonstrates how to create ASP.NET Web Forms applications using the Entity Framework 4.0 and Visual Studio 2010.</span></span> <span data-ttu-id="4274f-107">有关本教程系列的信息，请参阅[系列教程中的第一个教程](the-entity-framework-and-aspnet-getting-started-part-1.md)</span><span class="sxs-lookup"><span data-stu-id="4274f-107">For information about the tutorial series, see [the first tutorial in the series](the-entity-framework-and-aspnet-getting-started-part-1.md)</span></span>

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a><span data-ttu-id="4274f-108">使用动态数据功能格式化和验证数据</span><span class="sxs-lookup"><span data-stu-id="4274f-108">Using Dynamic Data Functionality to Format and Validate Data</span></span>

<span data-ttu-id="4274f-109">在上一教程中，您将实现存储过程。</span><span class="sxs-lookup"><span data-stu-id="4274f-109">In the previous tutorial you implemented stored procedures.</span></span> <span data-ttu-id="4274f-110">本教程将演示动态数据功能如何提供以下好处：</span><span class="sxs-lookup"><span data-stu-id="4274f-110">This tutorial will show you how Dynamic Data functionality can provide the following benefits:</span></span>

- <span data-ttu-id="4274f-111">根据字段的数据类型，字段将自动进行格式设置。</span><span class="sxs-lookup"><span data-stu-id="4274f-111">Fields are automatically formatted for display based on their data type.</span></span>
- <span data-ttu-id="4274f-112">根据字段的数据类型自动验证字段。</span><span class="sxs-lookup"><span data-stu-id="4274f-112">Fields are automatically validated based on their data type.</span></span>
- <span data-ttu-id="4274f-113">您可以将元数据添加到数据模型，以自定义格式设置和验证行为。</span><span class="sxs-lookup"><span data-stu-id="4274f-113">You can add metadata to the data model to customize formatting and validation behavior.</span></span> <span data-ttu-id="4274f-114">执行此操作时，只需在一个位置添加格式设置和验证规则，这些规则就会自动应用到使用动态数据控件访问这些字段的任何位置。</span><span class="sxs-lookup"><span data-stu-id="4274f-114">When you do this, you can add the formatting and validation rules in just one place, and they're automatically applied everywhere you access the fields using Dynamic Data controls.</span></span>

<span data-ttu-id="4274f-115">若要查看其工作原理，你将更改用于显示和*编辑现有 "* student" 页中的字段的控件，并将格式设置和验证元数据添加到 `Student` 实体类型的 "名称" 和 "日期" 字段。</span><span class="sxs-lookup"><span data-stu-id="4274f-115">To see how this works, you'll change the controls you use to display and edit fields in the existing *Students.aspx* page, and you'll add formatting and validation metadata to the name and date fields of the `Student` entity type.</span></span>

<span data-ttu-id="4274f-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4274f-116">[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)</span></span>

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a><span data-ttu-id="4274f-117">使用 DynamicField 和 DynamicControl 控件</span><span class="sxs-lookup"><span data-stu-id="4274f-117">Using DynamicField and DynamicControl Controls</span></span>

<span data-ttu-id="4274f-118">打开 "student *" 页，* 然后在 `StudentsGridView` 控件中，用以下标记替换**名称**和**注册日期**`TemplateField` 元素：</span><span class="sxs-lookup"><span data-stu-id="4274f-118">Open the *Students.aspx* page and in the `StudentsGridView` control replace the **Name** and **Enrollment Date** `TemplateField` elements with the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

<span data-ttu-id="4274f-119">此标记使用 `DynamicControl` 控件来代替 `TextBox` 并在 "学生姓名模板" 字段中 `Label` 控件，并对注册日期使用 `DynamicField` 控件。</span><span class="sxs-lookup"><span data-stu-id="4274f-119">This markup uses `DynamicControl` controls in place of `TextBox` and `Label` controls in the student name template field, and it uses a `DynamicField` control for the enrollment date.</span></span> <span data-ttu-id="4274f-120">未指定格式字符串。</span><span class="sxs-lookup"><span data-stu-id="4274f-120">No format strings are specified.</span></span>

<span data-ttu-id="4274f-121">将 `ValidationSummary` 控件添加到 `StudentsGridView` 控件之后。</span><span class="sxs-lookup"><span data-stu-id="4274f-121">Add a `ValidationSummary` control after the `StudentsGridView` control.</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

<span data-ttu-id="4274f-122">在 `SearchGridView` 控件中，将 "**名称**" 和 "**注册日期**" 列的标记替换为在 `StudentsGridView` 控件中执行的操作，但省略 `EditItemTemplate` 元素除外。</span><span class="sxs-lookup"><span data-stu-id="4274f-122">In the `SearchGridView` control replace the markup for the **Name** and **Enrollment Date** columns as you did in the `StudentsGridView` control, except omit the `EditItemTemplate` element.</span></span> <span data-ttu-id="4274f-123">`SearchGridView` 控件的 `Columns` 元素现在包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="4274f-123">The `Columns` element of the `SearchGridView` control now contains the following markup:</span></span>

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

<span data-ttu-id="4274f-124">打开*Students.aspx.cs*并添加以下 `using` 语句：</span><span class="sxs-lookup"><span data-stu-id="4274f-124">Open *Students.aspx.cs* and add the following `using` statement:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

<span data-ttu-id="4274f-125">为页面的 `Init` 事件添加处理程序：</span><span class="sxs-lookup"><span data-stu-id="4274f-125">Add a handler for the page's `Init` event:</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

<span data-ttu-id="4274f-126">此代码指定动态数据将在 `Student` 实体的字段的这些数据绑定控件中提供格式设置和验证。</span><span class="sxs-lookup"><span data-stu-id="4274f-126">This code specifies that Dynamic Data will provide formatting and validation in these data-bound controls for fields of the `Student` entity.</span></span> <span data-ttu-id="4274f-127">如果在运行页面时收到类似于以下示例的错误消息，则通常意味着你在 `Page_Init`中忘记了调用 `EnableDynamicData` 方法：</span><span class="sxs-lookup"><span data-stu-id="4274f-127">If you get an error message like the following example when you run the page, it typically means you've forgotten to call the `EnableDynamicData` method in `Page_Init`:</span></span>

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

<span data-ttu-id="4274f-128">运行页面。</span><span class="sxs-lookup"><span data-stu-id="4274f-128">Run the page.</span></span>

<span data-ttu-id="4274f-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="4274f-129">[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)</span></span>

<span data-ttu-id="4274f-130">在 "**注册日期**" 列中，时间与日期一起显示，因为属性类型为 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="4274f-130">In the **Enrollment Date** column, the time is displayed along with the date because the property type is `DateTime`.</span></span> <span data-ttu-id="4274f-131">稍后你将解决此问题。</span><span class="sxs-lookup"><span data-stu-id="4274f-131">You'll fix that later.</span></span>

<span data-ttu-id="4274f-132">请注意，动态数据会自动提供基本的数据验证。</span><span class="sxs-lookup"><span data-stu-id="4274f-132">For now, notice that Dynamic Data automatically provides basic data validation.</span></span> <span data-ttu-id="4274f-133">例如，单击 "**编辑**"，清除 "日期" 字段，单击 "**更新**"，您将看到动态数据自动使此字段成为必填字段，因为在数据模型中值不可为 null。</span><span class="sxs-lookup"><span data-stu-id="4274f-133">For example, click **Edit**, clear the date field, click **Update**, and you see that Dynamic Data automatically makes this a required field because the value is not nullable in the data model.</span></span> <span data-ttu-id="4274f-134">该页在字段后面显示星号，在 `ValidationSummary` 控件中显示错误消息：</span><span class="sxs-lookup"><span data-stu-id="4274f-134">The page displays an asterisk after the field and an error message in the `ValidationSummary` control:</span></span>

<span data-ttu-id="4274f-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="4274f-135">[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)</span></span>

<span data-ttu-id="4274f-136">您可以省略 `ValidationSummary` 控件，因为还可以将鼠标指针停留在星号上以查看错误消息：</span><span class="sxs-lookup"><span data-stu-id="4274f-136">You could omit the `ValidationSummary` control, because you can also hold the mouse pointer over the asterisk to see the error message:</span></span>

<span data-ttu-id="4274f-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="4274f-137">[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)</span></span>

<span data-ttu-id="4274f-138">动态数据还将验证在 "**注册日期**" 字段中输入的数据是否为有效日期：</span><span class="sxs-lookup"><span data-stu-id="4274f-138">Dynamic Data will also validate that data entered in the **Enrollment Date** field is a valid date:</span></span>

<span data-ttu-id="4274f-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="4274f-139">[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)</span></span>

<span data-ttu-id="4274f-140">如您所见，这是一个一般性错误消息。</span><span class="sxs-lookup"><span data-stu-id="4274f-140">As you can see, this is a generic error message.</span></span> <span data-ttu-id="4274f-141">在下一部分中，你将了解如何自定义消息以及验证和格式设置规则。</span><span class="sxs-lookup"><span data-stu-id="4274f-141">In the next section you'll see how to customize messages as well as validation and formatting rules.</span></span>

## <a name="adding-metadata-to-the-data-model"></a><span data-ttu-id="4274f-142">将元数据添加到数据模型</span><span class="sxs-lookup"><span data-stu-id="4274f-142">Adding Metadata to the Data Model</span></span>

<span data-ttu-id="4274f-143">通常，您需要自定义动态数据提供的功能。</span><span class="sxs-lookup"><span data-stu-id="4274f-143">Typically, you want to customize the functionality provided by Dynamic Data.</span></span> <span data-ttu-id="4274f-144">例如，你可以更改数据的显示方式以及错误消息的内容。</span><span class="sxs-lookup"><span data-stu-id="4274f-144">For example, you might change how data is displayed and the content of error messages.</span></span> <span data-ttu-id="4274f-145">通常，你还可以自定义数据验证规则，以提供比动态数据基于数据类型自动提供的功能更多的功能。</span><span class="sxs-lookup"><span data-stu-id="4274f-145">You typically also customize data validation rules to provide more functionality than what Dynamic Data provides automatically based on data types.</span></span> <span data-ttu-id="4274f-146">为此，可以创建与实体类型相对应的分部类。</span><span class="sxs-lookup"><span data-stu-id="4274f-146">To do this, you create partial classes that correspond to entity types.</span></span>

<span data-ttu-id="4274f-147">在**解决方案资源管理器**中，右键单击**ContosoUniversity**项目，选择 "**添加引用**"，并添加对 `System.ComponentModel.DataAnnotations`的引用。</span><span class="sxs-lookup"><span data-stu-id="4274f-147">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Add Reference**, and add a reference to `System.ComponentModel.DataAnnotations`.</span></span>

<span data-ttu-id="4274f-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="4274f-148">[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)</span></span>

<span data-ttu-id="4274f-149">在*DAL*文件夹中，创建一个新的类文件，将其命名为*Student.cs*，并将其中的模板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="4274f-149">In the *DAL* folder, create a new class file, name it *Student.cs*, and replace the template code in it with the following code.</span></span>

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

<span data-ttu-id="4274f-150">此代码将创建 `Student` 实体的分部类。</span><span class="sxs-lookup"><span data-stu-id="4274f-150">This code creates a partial class for the `Student` entity.</span></span> <span data-ttu-id="4274f-151">应用于此分部类的 `MetadataType` 属性标识用于指定元数据的类。</span><span class="sxs-lookup"><span data-stu-id="4274f-151">The `MetadataType` attribute applied to this partial class identifies the class that you're using to specify metadata.</span></span> <span data-ttu-id="4274f-152">Metadata 类可以具有任何名称，但使用实体名称加 "Metadata" 是常见做法。</span><span class="sxs-lookup"><span data-stu-id="4274f-152">The metadata class can have any name, but using the entity name plus "Metadata" is a common practice.</span></span>

<span data-ttu-id="4274f-153">应用于元数据类中的属性的特性指定格式设置、验证、规则和错误消息。</span><span class="sxs-lookup"><span data-stu-id="4274f-153">The attributes applied to properties in the metadata class specify formatting, validation, rules, and error messages.</span></span> <span data-ttu-id="4274f-154">此处显示的属性将具有以下结果：</span><span class="sxs-lookup"><span data-stu-id="4274f-154">The attributes shown here will have the following results:</span></span>

- <span data-ttu-id="4274f-155">`EnrollmentDate` 将显示为日期（没有时间）。</span><span class="sxs-lookup"><span data-stu-id="4274f-155">`EnrollmentDate` will display as a date (without a time).</span></span>
- <span data-ttu-id="4274f-156">两个名称字段的长度必须小于或等于25个字符，并提供自定义错误消息。</span><span class="sxs-lookup"><span data-stu-id="4274f-156">Both name fields must be 25 characters or less in length, and a custom error message is provided.</span></span>
- <span data-ttu-id="4274f-157">这两个名称字段都是必需的，并且提供了一个自定义错误消息。</span><span class="sxs-lookup"><span data-stu-id="4274f-157">Both name fields are required, and a custom error message is provided.</span></span>

<span data-ttu-id="4274f-158">再次运行*student 页面，* 你会看到现在没有时间显示日期：</span><span class="sxs-lookup"><span data-stu-id="4274f-158">Run the *Students.aspx* page again, and you see that the dates are now displayed without times:</span></span>

<span data-ttu-id="4274f-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="4274f-159">[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)</span></span>

<span data-ttu-id="4274f-160">编辑行，并尝试清除 "名称" 字段中的值。</span><span class="sxs-lookup"><span data-stu-id="4274f-160">Edit a row and try to clear the values in the name fields.</span></span> <span data-ttu-id="4274f-161">在您单击 "**更新**" 之前，一旦您离开字段，就会出现指示域错误的星号。</span><span class="sxs-lookup"><span data-stu-id="4274f-161">The asterisks indicating field errors appear as soon as you leave a field, before you click **Update**.</span></span> <span data-ttu-id="4274f-162">单击 "**更新**" 时，页面将显示您指定的错误消息文本。</span><span class="sxs-lookup"><span data-stu-id="4274f-162">When you click **Update**, the page displays the error message text you specified.</span></span>

<span data-ttu-id="4274f-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="4274f-163">[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)</span></span>

<span data-ttu-id="4274f-164">尝试输入超过25个字符的名称，单击 "**更新**"，该页将显示您指定的错误消息文本。</span><span class="sxs-lookup"><span data-stu-id="4274f-164">Try to enter names that are longer than 25 characters, click **Update**, and the page displays the error message text you specified.</span></span>

<span data-ttu-id="4274f-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="4274f-165">[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)</span></span>

<span data-ttu-id="4274f-166">现在，你已在数据模型元数据中设置这些格式设置和验证规则，只要你使用 `DynamicControl` 或 `DynamicField` 控件，规则就会自动应用于显示或允许对这些字段进行更改的每个页面。</span><span class="sxs-lookup"><span data-stu-id="4274f-166">Now that you've set up these formatting and validation rules in the data model metadata, the rules will automatically be applied on every page that displays or allows changes to these fields, so long as you use `DynamicControl` or `DynamicField` controls.</span></span> <span data-ttu-id="4274f-167">这会减少您必须编写的冗余代码量，使编程和测试变得更加容易，并且确保数据格式和验证在整个应用程序中保持一致。</span><span class="sxs-lookup"><span data-stu-id="4274f-167">This reduces the amount of redundant code you have to write, which makes programming and testing easier, and it ensures that data formatting and validation are consistent throughout an application.</span></span>

## <a name="more-information"></a><span data-ttu-id="4274f-168">详细信息</span><span class="sxs-lookup"><span data-stu-id="4274f-168">More Information</span></span>

<span data-ttu-id="4274f-169">这将在与实体框架入门的这一系列教程结束。</span><span class="sxs-lookup"><span data-stu-id="4274f-169">This concludes this series of tutorials on Getting Started with the Entity Framework.</span></span> <span data-ttu-id="4274f-170">若要详细了解如何使用实体框架，请继续学习[下一实体框架教程系列中的第一个教程](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)，或访问以下站点：</span><span class="sxs-lookup"><span data-stu-id="4274f-170">For more resources to help you learn how to use the Entity Framework, continue with [the first tutorial in the next Entity Framework tutorial series](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) or visit the following sites:</span></span>

- [<span data-ttu-id="4274f-171">实体框架常见问题</span><span class="sxs-lookup"><span data-stu-id="4274f-171">Entity Framework FAQ</span></span>](http://www.ef-faq.org/introduction.html)
- [<span data-ttu-id="4274f-172">实体框架团队博客</span><span class="sxs-lookup"><span data-stu-id="4274f-172">The Entity Framework Team Blog</span></span>](https://blogs.msdn.com/b/adonet/)
- [<span data-ttu-id="4274f-173">MSDN Library 中的实体框架</span><span class="sxs-lookup"><span data-stu-id="4274f-173">Entity Framework in the MSDN Library</span></span>](https://msdn.microsoft.com/library/bb399572.aspx)
- [<span data-ttu-id="4274f-174">MSDN 数据开发人员中心中的实体框架</span><span class="sxs-lookup"><span data-stu-id="4274f-174">Entity Framework in the MSDN Data Developer Center</span></span>](https://msdn.microsoft.com/data/ef.aspx)
- [<span data-ttu-id="4274f-175">MSDN Library 中的 EntityDataSource Web 服务器控件概述</span><span class="sxs-lookup"><span data-stu-id="4274f-175">EntityDataSource Web Server Control Overview in the MSDN Library</span></span>](https://msdn.microsoft.com/library/cc488502.aspx)
- [<span data-ttu-id="4274f-176">MSDN Library 中的 EntityDataSource 控件 API 参考</span><span class="sxs-lookup"><span data-stu-id="4274f-176">EntityDataSource control API reference in the MSDN Library</span></span>](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [<span data-ttu-id="4274f-177">MSDN 上的实体框架论坛</span><span class="sxs-lookup"><span data-stu-id="4274f-177">Entity Framework Forums on MSDN</span></span>](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [<span data-ttu-id="4274f-178">Julie Lerman 的博客</span><span class="sxs-lookup"><span data-stu-id="4274f-178">Julie Lerman's blog</span></span>](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [<span data-ttu-id="4274f-179">上一页</span><span class="sxs-lookup"><span data-stu-id="4274f-179">Previous</span></span>](the-entity-framework-and-aspnet-getting-started-part-7.md)
