---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: 教程：为 ASP.NET MVC 应用创建更复杂的数据模型
author: tdykstra
description: 在本教程中, 您将添加更多实体和关系, 并通过指定格式设置、验证和数据库映射规则来自定义数据模型。
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 46f7f3c9-274f-4649-811d-92222a9b27e2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 933354b09eb4674e6f523f8a65816410521f026f
ms.sourcegitcommit: aa3c2efd56466fc6bdc387ee01ad6f50a261665b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70020994"
---
# <a name="tutorial-create-a-more-complex-data-model-for-an-aspnet-mvc-app"></a><span data-ttu-id="6f9ea-103">教程：为 ASP.NET MVC 应用创建更复杂的数据模型</span><span class="sxs-lookup"><span data-stu-id="6f9ea-103">Tutorial: Create a more complex data model for an ASP.NET MVC app</span></span>

<span data-ttu-id="6f9ea-104">在前面的教程中, 你使用了由三个实体组成的简单数据模型。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-104">In the previous tutorials you worked with a simple data model that was composed of three entities.</span></span> <span data-ttu-id="6f9ea-105">在本教程中, 您将添加更多实体和关系, 并通过指定格式设置、验证和数据库映射规则来自定义数据模型。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-105">In this tutorial you add more entities and relationships and you customize the data model by specifying formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="6f9ea-106">本文介绍了两种自定义数据模型的方法: 通过向实体类添加属性和向数据库上下文类添加代码。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-106">This article shows two ways to customize the data model: by adding attributes to entity classes and by adding code to the database context class.</span></span>

<span data-ttu-id="6f9ea-107">完成本教程后，实体类将构成下图所示的完整数据模型：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-107">When you're finished, the entity classes will make up the completed data model that's shown in the following illustration:</span></span>

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="6f9ea-109">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-109">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6f9ea-110">自定义数据模型</span><span class="sxs-lookup"><span data-stu-id="6f9ea-110">Customize the data model</span></span>
> * <span data-ttu-id="6f9ea-111">更新学生实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-111">Update Student entity</span></span>
> * <span data-ttu-id="6f9ea-112">创建 Instructor 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-112">Create Instructor entity</span></span>
> * <span data-ttu-id="6f9ea-113">创建 OfficeAssignment 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-113">Create OfficeAssignment entity</span></span>
> * <span data-ttu-id="6f9ea-114">修改课程实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-114">Modify the Course entity</span></span>
> * <span data-ttu-id="6f9ea-115">创建 Department 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-115">Create the Department entity</span></span>
> * <span data-ttu-id="6f9ea-116">修改 Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-116">Modify the Enrollment entity</span></span>
> * <span data-ttu-id="6f9ea-117">将代码添加到数据库上下文</span><span class="sxs-lookup"><span data-stu-id="6f9ea-117">Add code to database context</span></span>
> * <span data-ttu-id="6f9ea-118">使用测试数据设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="6f9ea-118">Seed database with test data</span></span>
> * <span data-ttu-id="6f9ea-119">添加迁移</span><span class="sxs-lookup"><span data-stu-id="6f9ea-119">Add a migration</span></span>
> * <span data-ttu-id="6f9ea-120">更新数据库</span><span class="sxs-lookup"><span data-stu-id="6f9ea-120">Update the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f9ea-121">系统必备</span><span class="sxs-lookup"><span data-stu-id="6f9ea-121">Prerequisites</span></span>

* [<span data-ttu-id="6f9ea-122">Code First 迁移和部署</span><span class="sxs-lookup"><span data-stu-id="6f9ea-122">Code First migrations and deployment</span></span>](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-the-data-model"></a><span data-ttu-id="6f9ea-123">自定义数据模型</span><span class="sxs-lookup"><span data-stu-id="6f9ea-123">Customize the data model</span></span>

<span data-ttu-id="6f9ea-124">本节介绍如何使用指定格式化、验证和数据库映射规则的特性来自定义数据模型。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-124">In this section you'll see how to customize the data model by using attributes that specify formatting, validation, and database mapping rules.</span></span> <span data-ttu-id="6f9ea-125">然后, 在以下几节中, 您将通过向`School`已创建的类添加特性并为模型中的其余实体类型创建新类, 来创建完整的数据模型。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-125">Then in several of the following sections you'll create the complete `School` data model by adding attributes to the classes you already created and creating new classes for the remaining entity types in the model.</span></span>

### <a name="the-datatype-attribute"></a><span data-ttu-id="6f9ea-126">DataType 特性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-126">The DataType Attribute</span></span>

<span data-ttu-id="6f9ea-127">对于学生注册日期，目前所有网页都显示有时间和日期，尽管对此字段而言重要的只是日期。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-127">For student enrollment dates, all of the web pages currently display the time along with the date, although all you care about for this field is the date.</span></span> <span data-ttu-id="6f9ea-128">使用数据注释特性，可更改一次代码，修复每个视图中数据的显示格式。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-128">By using data annotation attributes, you can make one code change that will fix the display format in every view that shows the data.</span></span> <span data-ttu-id="6f9ea-129">若要查看如何执行此操作，请向 `Student` 类的 `EnrollmentDate` 属性添加一个特性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-129">To see an example of how to do that, you'll add an attribute to the `EnrollmentDate` property in the `Student` class.</span></span>

<span data-ttu-id="6f9ea-130">在*Models\Student.cs*中, 为`using` `System.ComponentModel.DataAnnotations` `DataType` 命名空间`DisplayFormat`添加一个语句, 并将和属性添加到属性,如以下示例中所示:`EnrollmentDate`</span><span class="sxs-lookup"><span data-stu-id="6f9ea-130">In *Models\Student.cs*, add a `using` statement for the `System.ComponentModel.DataAnnotations` namespace and add `DataType` and `DisplayFormat` attributes to the `EnrollmentDate` property, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,12-13)]

<span data-ttu-id="6f9ea-131">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性用于指定比数据库内部类型更具体的数据类型。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-131">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute is used to specify a data type that is more specific than the database intrinsic type.</span></span> <span data-ttu-id="6f9ea-132">在此示例中，我们只想跟踪日期，而不是日期和时间。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-132">In this case we only want to keep track of the date, not the date and time.</span></span> <span data-ttu-id="6f9ea-133">[DataType 枚举](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供多种数据类型, 例如*日期、时间、PhoneNumber、货币、EmailAddress*等。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-133">The [DataType Enumeration](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) provides for many data types, such as *Date, Time, PhoneNumber, Currency, EmailAddress* and more.</span></span> <span data-ttu-id="6f9ea-134">应用程序还可通过 `DataType` 特性自动提供类型特定的功能。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-134">The `DataType` attribute can also enable the application to automatically provide type-specific features.</span></span> <span data-ttu-id="6f9ea-135">例如`mailto:` , 可以为[EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)创建链接, 并且可以在支持[HTML5](http://html5.org/)的浏览器中为[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)提供日期选择器。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-135">For example, a `mailto:` link can be created for [DataType.EmailAddress](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx), and a date selector can be provided for [DataType.Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) in browsers that support [HTML5](http://html5.org/).</span></span> <span data-ttu-id="6f9ea-136">数据[类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性发出 html 5[数据](http://ejohn.org/blog/html-5-data-attributes/)(发音为*数据破折号*) 属性, html 5 浏览器可以理解这些属性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-136">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes emits HTML 5 [data-](http://ejohn.org/blog/html-5-data-attributes/) (pronounced *data dash*) attributes that HTML 5 browsers can understand.</span></span> <span data-ttu-id="6f9ea-137">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性不提供任何验证。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-137">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attributes do not provide any validation.</span></span>

<span data-ttu-id="6f9ea-138">`DataType.Date` 不指定显示日期的格式。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-138">`DataType.Date` does not specify the format of the date that is displayed.</span></span> <span data-ttu-id="6f9ea-139">默认情况下, 数据字段根据服务器的[CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)按默认格式显示。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-139">By default, the data field is displayed according to the default formats based on the server's [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx).</span></span>

<span data-ttu-id="6f9ea-140">`DisplayFormat` 特性用于显式指定日期格式：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-140">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="6f9ea-141">此`ApplyFormatInEditMode`设置指定当在文本框中显示值进行编辑时, 还应应用指定的格式设置。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-141">The `ApplyFormatInEditMode` setting specifies that the specified formatting should also be applied when the value is displayed in a text box for editing.</span></span> <span data-ttu-id="6f9ea-142">(您可能不希望为某些字段 (例如, 对于货币值), 您可能不希望文本框中的货币符号进行编辑。)</span><span class="sxs-lookup"><span data-stu-id="6f9ea-142">(You might not want that for some fields — for example, for currency values, you might not want the currency symbol in the text box for editing.)</span></span>

<span data-ttu-id="6f9ea-143">您可以单独使用[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)属性, 但通常最好使用[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)属性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-143">You can use the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) attribute by itself, but it's generally a good idea to use the [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute also.</span></span> <span data-ttu-id="6f9ea-144">属性传达数据的*语义*, 而不是在屏幕上呈现数据的语义, 并提供以下不`DisplayFormat`需要的优点: `DataType`</span><span class="sxs-lookup"><span data-stu-id="6f9ea-144">The `DataType` attribute conveys the *semantics* of the data as opposed to how to render it on a screen, and provides the following benefits that you don't get with `DisplayFormat`:</span></span>

- <span data-ttu-id="6f9ea-145">浏览器可启用 HTML5 功能（例如，显示日历控件、区域设置适用的货币符号、电子邮件链接、某种客户端输入验证等）。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-145">The browser can enable HTML5 features (for example to show a calendar control, the locale-appropriate currency symbol, email links, some client-side input validation, etc.).</span></span>
- <span data-ttu-id="6f9ea-146">默认情况下, 浏览器将根据[区域设置](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)使用正确的格式呈现数据。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-146">By default, the browser will render data using the correct format based on your [locale](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx).</span></span>
- <span data-ttu-id="6f9ea-147">[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性可以使 MVC 选择正确的字段模板来呈现数据 ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx)使用字符串模板)。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-147">The [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) attribute can enable MVC to choose the right field template to render the data (the [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) uses the string template).</span></span> <span data-ttu-id="6f9ea-148">有关详细信息, 请参阅 Brad Wilson 的[ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-148">For more information, see Brad Wilson's [ASP.NET MVC 2 Templates](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html).</span></span> <span data-ttu-id="6f9ea-149">(尽管是针对 MVC 2 编写的, 但本文仍适用于当前版本的 ASP.NET MVC。)</span><span class="sxs-lookup"><span data-stu-id="6f9ea-149">(Though written for MVC 2, this article still applies to the current version of ASP.NET MVC.)</span></span>

<span data-ttu-id="6f9ea-150">如果将`DataType`属性与日期字段一起使用, 则还必须`DisplayFormat`指定属性, 以确保字段在 Chrome 浏览器中正确呈现。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-150">If you use the `DataType` attribute with a date field, you have to specify the `DisplayFormat` attribute also in order to ensure that the field renders correctly in Chrome browsers.</span></span> <span data-ttu-id="6f9ea-151">有关详细信息, 请参阅[此 StackOverflow 线程](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-151">For more information, see [this StackOverflow thread](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie).</span></span>

<span data-ttu-id="6f9ea-152">有关如何在 mvc 中处理其他日期格式的详细信息, 请参阅[mvc 5 简介:检查 "编辑" 方法和 "](../introduction/examining-the-edit-methods-and-edit-view.md)编辑" 视图, 并在&quot;国际化&quot;页面中搜索。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-152">For more information about how to handle other date formats in MVC, go to [MVC 5 Introduction: Examining the Edit Methods and Edit View](../introduction/examining-the-edit-methods-and-edit-view.md) and search in the page for &quot;internationalization&quot;.</span></span>

<span data-ttu-id="6f9ea-153">再次运行 "学生索引" 页, 注意注册日期不再显示时间。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-153">Run the Student Index page again and notice that times are no longer displayed for the enrollment dates.</span></span> <span data-ttu-id="6f9ea-154">对于使用该`Student`模型的任何视图, 这一点都是相同的。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-154">The same will be true for any view that uses the `Student` model.</span></span>

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a><span data-ttu-id="6f9ea-156">StringLengthAttribute</span><span class="sxs-lookup"><span data-stu-id="6f9ea-156">The StringLengthAttribute</span></span>

<span data-ttu-id="6f9ea-157">还可使用特性指定数据验证规则和验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-157">You can also specify data validation rules and validation error messages using attributes.</span></span> <span data-ttu-id="6f9ea-158">[StringLength 特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)设置数据库中的最大长度, 并为 ASP.NET MVC 提供客户端和服务器端验证。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-158">The [StringLength attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) sets the maximum length in the database and provides client side and server side validation for ASP.NET MVC.</span></span> <span data-ttu-id="6f9ea-159">还可在此属性中指定最小字符串长度，但最小值对数据库架构没有影响。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-159">You can also specify the minimum string length in this attribute, but the minimum value has no impact on the database schema.</span></span>

<span data-ttu-id="6f9ea-160">假设要确保用户输入的名称不超过 50 个字符。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-160">Suppose you want to ensure that users don't enter more than 50 characters for a name.</span></span> <span data-ttu-id="6f9ea-161">若要添加此限制, 请将[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)特性`LastName`添加`FirstMidName`到和属性, 如以下示例中所示:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-161">To add this limitation, add [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attributes to the `LastName` and `FirstMidName` properties, as shown in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

<span data-ttu-id="6f9ea-162">[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)属性不会阻止用户为某个名称输入空格。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-162">The [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute won't prevent a user from entering white space for a name.</span></span> <span data-ttu-id="6f9ea-163">可以使用[RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx)属性将限制应用到输入。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-163">You can use the [RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) attribute to apply restrictions to the input.</span></span> <span data-ttu-id="6f9ea-164">例如, 下面的代码要求第一个字符为大写, 其余的字符为字母顺序:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-164">For example the following code requires the first character to be upper case and the remaining characters to be alphabetical:</span></span>

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

<span data-ttu-id="6f9ea-165">[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx)特性为[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)特性提供了类似的功能, 但不提供客户端验证。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-165">The [MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) attribute provides similar functionality to the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute but doesn't provide client side validation.</span></span>

<span data-ttu-id="6f9ea-166">运行应用程序, 然后单击 "**学生**" 选项卡。收到以下错误:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-166">Run the application and click the **Students** tab. You get the following error:</span></span>

<span data-ttu-id="6f9ea-167">*创建数据库后, 支持 "SchoolContext" 上下文的模型已发生更改。请考虑使用 Code First 迁移来更新数据库 ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269))。*</span><span class="sxs-lookup"><span data-stu-id="6f9ea-167">*The model backing the 'SchoolContext' context has changed since the database was created. Consider using Code First Migrations to update the database ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*</span></span>

<span data-ttu-id="6f9ea-168">数据库模型已更改, 这种情况下需要更改数据库架构, 并且实体框架检测到的情况。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-168">The database model has changed in a way that requires a change in the database schema, and Entity Framework detected that.</span></span> <span data-ttu-id="6f9ea-169">你将使用迁移来更新架构, 而不会丢失你使用 UI 添加到数据库的任何数据。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-169">You'll use migrations to update the schema without losing any data that you added to the database by using the UI.</span></span> <span data-ttu-id="6f9ea-170">如果更改了通过`Seed`方法创建的数据, 则会将其更改回其原始状态, 因为在`Seed`方法中使用的是[AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-170">If you changed data that was created by the `Seed` method, that will be changed back to its original state because of the [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) method that you're using in the `Seed` method.</span></span> <span data-ttu-id="6f9ea-171">([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx)相当于数据库术语中的 "upsert" 操作。)</span><span class="sxs-lookup"><span data-stu-id="6f9ea-171">([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) is equivalent to an "upsert" operation from database terminology.)</span></span>

<span data-ttu-id="6f9ea-172">在包管理器控制台 (PMC) 中输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-172">In the Package Manager Console (PMC), enter the following commands:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

<span data-ttu-id="6f9ea-173">`add-migration`命令创建名为的文件 *&lt;时间戳&gt;\_MaxLengthOnNames.cs* 。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-173">The `add-migration` command creates a file named *&lt;timeStamp&gt;\_MaxLengthOnNames.cs*.</span></span> <span data-ttu-id="6f9ea-174">此文件包含 `Up` 方法中的代码，该代码将更新数据库以匹配当前数据模型。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-174">This file contains code in the `Up` method that will update the database to match the current data model.</span></span> <span data-ttu-id="6f9ea-175">`update-database` 命令运行该代码。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-175">The `update-database` command ran that code.</span></span>

<span data-ttu-id="6f9ea-176">实体框架使用迁移文件名前面预置的时间戳来对迁移进行排序。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-176">The timestamp prepended to the migrations file name is used by Entity Framework to order the migrations.</span></span> <span data-ttu-id="6f9ea-177">你可以在运行`update-database`命令之前创建多个迁移, 然后按照创建的顺序应用所有迁移。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-177">You can create multiple migrations before running the `update-database` command, and then all of the migrations are applied in the order in which they were created.</span></span>

<span data-ttu-id="6f9ea-178">运行 "**创建**" 页, 并输入长度超过50个字符的名称。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-178">Run the **Create** page, and enter either name longer than 50 characters.</span></span> <span data-ttu-id="6f9ea-179">单击 "**创建**" 时, 客户端验证会显示一条错误消息:*字段 LastName 必须是最大长度为50的字符串。*</span><span class="sxs-lookup"><span data-stu-id="6f9ea-179">When you click **Create**, client side validation shows an error message: *The field LastName must be a string with a maximum length of 50.*</span></span>

### <a name="the-column-attribute"></a><span data-ttu-id="6f9ea-180">列属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-180">The Column Attribute</span></span>

<span data-ttu-id="6f9ea-181">还可使用特性来控制类和属性映射到数据库的方式。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-181">You can also use attributes to control how your classes and properties are mapped to the database.</span></span> <span data-ttu-id="6f9ea-182">假设在名字字段使用了 `FirstMidName`，这是因为该字段也可能包含中间名。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-182">Suppose you had used the name `FirstMidName` for the first-name field because the field might also contain a middle name.</span></span> <span data-ttu-id="6f9ea-183">但却希望将数据库列命名为 `FirstName`，因为要针对数据库编写即席查询的用户习惯使用该姓名。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-183">But you want the database column to be named `FirstName`, because users who will be writing ad-hoc queries against the database are accustomed to that name.</span></span> <span data-ttu-id="6f9ea-184">若要进行此映射，可使用 `Column` 特性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-184">To make this mapping, you can use the `Column` attribute.</span></span>

<span data-ttu-id="6f9ea-185">`Column` 特性指定，创建数据库时，映射到 `FirstMidName` 属性的 `Student` 表的列将被命名为 `FirstName`。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-185">The `Column` attribute specifies that when the database is created, the column of the `Student` table that maps to the `FirstMidName` property will be named `FirstName`.</span></span> <span data-ttu-id="6f9ea-186">换言之，在代码引用 `Student.FirstMidName` 时，数据来源将是 `Student` 表的 `FirstName` 列或在其中进行更新。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-186">In other words, when your code refers to `Student.FirstMidName`, the data will come from or be updated in the `FirstName` column of the `Student` table.</span></span> <span data-ttu-id="6f9ea-187">如果未指定列名, 则将其指定为与属性名称相同的名称。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-187">If you don't specify column names, they are given the same name as the property name.</span></span>

<span data-ttu-id="6f9ea-188">在*Student.cs*文件中, 添加`using` [system.componentmodel](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx)的语句, 并将列名特性添加到`FirstMidName`属性, 如以下突出显示的代码所示:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-188">In the *Student.cs* file, add a `using` statement for [System.ComponentModel.DataAnnotations.Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) and add the column name attribute to the `FirstMidName` property, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

<span data-ttu-id="6f9ea-189">添加[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)会更改 SchoolContext 的模型, 因此它不会与数据库匹配。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-189">The addition of the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) changes the model backing the SchoolContext, so it won't match the database.</span></span> <span data-ttu-id="6f9ea-190">在 PMC 中输入以下命令以创建另一个迁移:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-190">Enter the following commands in the PMC to create another migration:</span></span>

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

<span data-ttu-id="6f9ea-191">在**服务器资源管理器**中, 双击*student*表, 打开*student*表设计器。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-191">In **Server Explorer**, open the *Student* table designer by double-clicking the *Student* table.</span></span>

<span data-ttu-id="6f9ea-192">下图显示了在应用前两个迁移之前的原始列名称。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-192">The following image shows the original column name as it was before you applied the first two migrations.</span></span> <span data-ttu-id="6f9ea-193">除了从`FirstMidName`更改到`FirstName`的列名以外, 这两个名称列已从`MAX`长度更改为50个字符。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-193">In addition to the column name changing from `FirstMidName` to `FirstName`, the two name columns have changed from `MAX` length to 50 characters.</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

<span data-ttu-id="6f9ea-194">你还可以使用[熟知的 API](https://msdn.microsoft.com/data/jj591617)进行数据库映射更改, 如本教程的后面部分所示。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-194">You can also make database mapping changes using the [Fluent API](https://msdn.microsoft.com/data/jj591617), as you'll see later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="6f9ea-195">如果尚未按以下各节所述创建所有实体类就尝试进行编译，则可能会出现编译器错误。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-195">If you try to compile before you finish creating all of the entity classes in the following sections, you might get compiler errors.</span></span>

## <a name="update-student-entity"></a><span data-ttu-id="6f9ea-196">更新学生实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-196">Update Student entity</span></span>

<span data-ttu-id="6f9ea-197">在*Models\Student.cs*中, 将之前添加的代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-197">In *Models\Student.cs*, replace the code you added earlier with the following code.</span></span> <span data-ttu-id="6f9ea-198">突出显示所作更改。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-198">The changes are highlighted.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=11,13,15,18,22,25-32)]

### <a name="the-required-attribute"></a><span data-ttu-id="6f9ea-199">必需的属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-199">The Required Attribute</span></span>

<span data-ttu-id="6f9ea-200">[必需的属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx)使名称属性成为必填字段。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-200">The [Required attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) makes the name properties required fields.</span></span> <span data-ttu-id="6f9ea-201">`Required attribute`值类型 (例如 DateTime、int、double 和 float) 不需要。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-201">The `Required attribute` is not needed for value types such as DateTime, int, double, and float.</span></span> <span data-ttu-id="6f9ea-202">值类型不能赋予 null 值, 因此它们原本被视为必填字段。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-202">Value types cannot be assigned a null value, so they are inherently treated as required fields.</span></span> 

<span data-ttu-id="6f9ea-203">特性必须`MinimumLength` 与`MinimumLength`结合使用, 以便强制执行。 `Required`</span><span class="sxs-lookup"><span data-stu-id="6f9ea-203">The `Required` attribute must be used with `MinimumLength` for the `MinimumLength` to be enforced.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs?highlight=2)]

<span data-ttu-id="6f9ea-204">`MinimumLength`和`Required`允许空格满足验证。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-204">`MinimumLength` and `Required` allow whitespace to satisfy the validation.</span></span> <span data-ttu-id="6f9ea-205">对字符串使用完整控制的属性。`RegularExpression`</span><span class="sxs-lookup"><span data-stu-id="6f9ea-205">Use the `RegularExpression` attribute for full controll over the string.</span></span>

### <a name="the-display-attribute"></a><span data-ttu-id="6f9ea-206">显示属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-206">The Display Attribute</span></span>

<span data-ttu-id="6f9ea-207">`Display` 特性指定文本框的标题应是“名”、“姓”、“全名”和“注册日期”，而不是每个实例中的属性名称（其中没有分隔单词的空格）。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-207">The `Display` attribute specifies that the caption for the text boxes should be "First Name", "Last Name", "Full Name", and "Enrollment Date" instead of the property name in each instance (which has no space dividing the words).</span></span>

### <a name="the-fullname-calculated-property"></a><span data-ttu-id="6f9ea-208">FullName 计算属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-208">The FullName Calculated Property</span></span>

<span data-ttu-id="6f9ea-209">`FullName` 是计算属性，可返回通过串联两个其他属性创建的值。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-209">`FullName` is a calculated property that returns a value that's created by concatenating two other properties.</span></span> <span data-ttu-id="6f9ea-210">因此, 它只有一个`get`取值函数, 并且`FullName`在数据库中不会生成任何列。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-210">Therefore it has only a `get` accessor, and no `FullName` column will be generated in the database.</span></span>

## <a name="create-instructor-entity"></a><span data-ttu-id="6f9ea-211">创建 Instructor 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-211">Create Instructor entity</span></span>

<span data-ttu-id="6f9ea-212">创建*Models\Instructor.cs*, 将模板代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-212">Create *Models\Instructor.cs*, replacing the template code with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs)]

<span data-ttu-id="6f9ea-213">请注意，`Student` 和 `Instructor` 实体中具有几个相同属性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-213">Notice that several properties are the same in the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="6f9ea-214">本系列后面的[实现继承](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)教程将重构此代码以消除冗余。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-214">In the [Implementing Inheritance](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial later in this series, you'll refactor this code to eliminate the redundancy.</span></span>

<span data-ttu-id="6f9ea-215">可以将多个属性放在一行上, 因此还可以编写讲师类, 如下所示:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-215">You can put multiple attributes on one line, so you could also write the instructor class as follows:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a><span data-ttu-id="6f9ea-216">课程和 OfficeAssignment 导航属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-216">The Courses and OfficeAssignment Navigation Properties</span></span>

<span data-ttu-id="6f9ea-217">`Courses` 和 `OfficeAssignment` 是导航属性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-217">The `Courses` and `OfficeAssignment` properties are navigation properties.</span></span> <span data-ttu-id="6f9ea-218">如前所述, 它们通常定义为[虚拟](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx), 以便能够利用称为[延迟加载](https://msdn.microsoft.com/magazine/hh205756.aspx)的实体框架功能。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-218">As was explained earlier, they are typically defined as [virtual](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) so that they can take advantage of an Entity Framework feature called [lazy loading](https://msdn.microsoft.com/magazine/hh205756.aspx).</span></span> <span data-ttu-id="6f9ea-219">此外, 如果导航属性可以包含多个实体, 则其类型必须实现[ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx)接口。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-219">In addition, if a navigation property can hold multiple entities, its type must implement the [ICollection&lt;T&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) Interface.</span></span> <span data-ttu-id="6f9ea-220">例如, [IList&lt;t&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx)合格, 但不实现[&lt;IEnumerable t&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx) , 因为`IEnumerable<T>`不实现[Add](https://msdn.microsoft.com/library/63ywd54z.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-220">For example [IList&lt;T&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) qualifies but not [IEnumerable&lt;T&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) because `IEnumerable<T>` doesn't implement [Add](https://msdn.microsoft.com/library/63ywd54z.aspx).</span></span>

<span data-ttu-id="6f9ea-221">讲师可以讲授任意数量的课程, 因此`Courses`将其定义为一个`Course`实体集合。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-221">An instructor can teach any number of courses, so `Courses` is defined as a collection of `Course` entities.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

<span data-ttu-id="6f9ea-222">我们的业务规则陈述, 一个指导员最多只能有一个办公室, `OfficeAssignment`因此, 它定义为`OfficeAssignment`单个`null`实体 (如果没有分配任何 office)。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-222">Our business rules state an instructor can only have at most one office, so `OfficeAssignment` is defined as a single `OfficeAssignment` entity (which may be `null` if no office is assigned).</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-officeassignment-entity"></a><span data-ttu-id="6f9ea-223">创建 OfficeAssignment 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-223">Create OfficeAssignment entity</span></span>

<span data-ttu-id="6f9ea-224">用以下代码创建*Models\OfficeAssignment.cs* :</span><span class="sxs-lookup"><span data-stu-id="6f9ea-224">Create *Models\OfficeAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

<span data-ttu-id="6f9ea-225">生成项目, 该项目保存更改并验证编译器能否捕获任何复制和粘贴错误。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-225">Build the project, which saves your changes and verifies you haven't made any copy and paste errors the compiler can catch.</span></span>

### <a name="the-key-attribute"></a><span data-ttu-id="6f9ea-226">键属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-226">The Key Attribute</span></span>

<span data-ttu-id="6f9ea-227">`Instructor`和实体之间存在一对零或一的关系。`OfficeAssignment`</span><span class="sxs-lookup"><span data-stu-id="6f9ea-227">There's a one-to-zero-or-one relationship between the `Instructor` and the `OfficeAssignment` entities.</span></span> <span data-ttu-id="6f9ea-228">Office 分配只与分配给它的指导员相关, 因此, 其主键也是该`Instructor`实体的外键。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-228">An office assignment only exists in relation to the instructor it's assigned to, and therefore its primary key is also its foreign key to the `Instructor` entity.</span></span> <span data-ttu-id="6f9ea-229">但实体框架无法自动`InstructorID`识别为此实体的主键, 因为其名称不`ID`遵循或*classname* `ID`命名约定。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-229">But the Entity Framework can't automatically recognize `InstructorID` as the primary key of this entity because its name doesn't follow the `ID` or *classname* `ID` naming convention.</span></span> <span data-ttu-id="6f9ea-230">因此，`Key` 特性用于将其识别为主键：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-230">Therefore, the `Key` attribute is used to identify it as the key:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

<span data-ttu-id="6f9ea-231">如果实体具有其自己`Key`的主键, 但你想要将属性命名为不同于`classnameID`或`ID`的属性, 你也可以使用属性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-231">You can also use the `Key` attribute if the entity does have its own primary key but you want to name the property something different than `classnameID` or `ID`.</span></span> <span data-ttu-id="6f9ea-232">默认情况下, EF 将该键视为非数据库生成, 因为列是用于标识关系的。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-232">By default EF treats the key as non-database-generated because the column is for an identifying relationship.</span></span>

### <a name="the-foreignkey-attribute"></a><span data-ttu-id="6f9ea-233">ForeignKey 特性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-233">The ForeignKey Attribute</span></span>

<span data-ttu-id="6f9ea-234">如果两个实体之间存在一对零或一关系或一对一关系 (如与`OfficeAssignment` `Instructor`之间的关系), 则 EF 无法解决关系的哪一端是主体, 哪一端依赖于。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-234">When there is a one-to-zero-or-one relationship or a one-to-one relationship between two entities (such as between `OfficeAssignment` and `Instructor`), EF can't work out which end of the relationship is the principal and which end is dependent.</span></span> <span data-ttu-id="6f9ea-235">一对一关系在每个类中都有一个指向另一个类的引用导航属性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-235">One-to-one relationships have a reference navigation property in each class to the other class.</span></span> <span data-ttu-id="6f9ea-236">[ForeignKey 特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)可应用于依赖类以建立关系。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-236">The [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) can be applied to the dependent class to establish the relationship.</span></span> <span data-ttu-id="6f9ea-237">如果省略了[ForeignKey 属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), 则在尝试创建迁移时, 会收到以下错误:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-237">If you omit the [ForeignKey Attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx), you get the following error when you try to create the migration:</span></span>

<span data-ttu-id="6f9ea-238">*无法确定类型为 "ContosoUniversity" 和 "ContosoUniversity" 之间的关联的主体端。必须使用关系 Fluent API 或数据批注显式配置此关联的主体端。*</span><span class="sxs-lookup"><span data-stu-id="6f9ea-238">*Unable to determine the principal end of an association between the types 'ContosoUniversity.Models.OfficeAssignment' and 'ContosoUniversity.Models.Instructor'. The principal end of this association must be explicitly configured using either the relationship fluent API or data annotations.*</span></span>

<span data-ttu-id="6f9ea-239">稍后在本教程中, 你将了解如何配置此关系与 Fluent API。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-239">Later in the tutorial you'll see how to configure this relationship with the fluent API.</span></span>

### <a name="the-instructor-navigation-property"></a><span data-ttu-id="6f9ea-240">讲师导航属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-240">The Instructor Navigation Property</span></span>

<span data-ttu-id="6f9ea-241">实体有一个可以为`OfficeAssignment` null 的导航属性 (因为讲师可能没有办公室分配), 并且该`OfficeAssignment`实体具有不可为 null `Instructor`的导航属性 (因为办公室分配无法`Instructor`存在但不包含指导员- `InstructorID` -不可为 null)。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-241">The `Instructor` entity has a nullable `OfficeAssignment` navigation property (because an instructor might not have an office assignment), and the `OfficeAssignment` entity has a non-nullable `Instructor` navigation property (because an office assignment can't exist without an instructor -- `InstructorID` is non-nullable).</span></span> <span data-ttu-id="6f9ea-242">当实体具有相关`OfficeAssignment`实体时, 每个实体都将在其导航属性中引用另一个实体。 `Instructor`</span><span class="sxs-lookup"><span data-stu-id="6f9ea-242">When an `Instructor` entity has a related `OfficeAssignment` entity, each entity will have a reference to the other one in its navigation property.</span></span>

<span data-ttu-id="6f9ea-243">您可以在讲师`[Required]`导航属性中放置一个属性以指定必须有相关讲师, 但您不必这样做, 因为 InstructorID 外键 (也是此表的键) 不可为 null。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-243">You could put a `[Required]` attribute on the Instructor navigation property to specify that there must be a related instructor, but you don't have to do that because the InstructorID foreign key (which is also the key to this table) is non-nullable.</span></span>

## <a name="modify-the-course-entity"></a><span data-ttu-id="6f9ea-244">修改课程实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-244">Modify the Course entity</span></span>

<span data-ttu-id="6f9ea-245">在*Models\Course.cs*中, 将之前添加的代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-245">In *Models\Course.cs*, replace the code you added earlier with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

<span data-ttu-id="6f9ea-246">课程实体具有外键属性, 该`DepartmentID`属性指向相关`Department` `Department`实体并且具有导航属性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-246">The course entity has a foreign key property `DepartmentID` which points to the related `Department` entity and it has a `Department` navigation property.</span></span> <span data-ttu-id="6f9ea-247">如果拥有相关实体的导航属性，则 Entity Framework 不会要求为数据模型添加外键属性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-247">The Entity Framework doesn't require you to add a foreign key property to your data model when you have a navigation property for a related entity.</span></span> <span data-ttu-id="6f9ea-248">EF 在需要时在数据库中自动创建外键。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-248">EF automatically creates foreign keys in the database wherever they are needed.</span></span> <span data-ttu-id="6f9ea-249">但如果数据模型包含外键，则更新会变得更简单、更高效。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-249">But having the foreign key in the data model can make updates simpler and more efficient.</span></span> <span data-ttu-id="6f9ea-250">例如, 当您提取要编辑的课程实体时, `Department`如果不加载它, 则实体为 null, 因此, 在更新课程实体时, 必须首先提取该`Department`实体。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-250">For example, when you fetch a course entity to edit, the `Department` entity is null if you don't load it, so when you update the course entity, you would have to first fetch the `Department` entity.</span></span> <span data-ttu-id="6f9ea-251">如果数据模型中包含`DepartmentID`外键属性, 则不需要在更新前`Department`提取实体。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-251">When the foreign key property `DepartmentID` is included in the data model, you don't need to fetch the `Department` entity before you update.</span></span>

### <a name="the-databasegenerated-attribute"></a><span data-ttu-id="6f9ea-252">DatabaseGenerated 特性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-252">The DatabaseGenerated Attribute</span></span>

<span data-ttu-id="6f9ea-253">`CourseID`属性上带有[None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx)参数的[DatabaseGenerated 特性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx)指定, 主键值由用户提供, 而不是由数据库生成。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-253">The [DatabaseGenerated attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) with the [None](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) parameter on the `CourseID` property specifies that primary key values are provided by the user rather than generated by the database.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

<span data-ttu-id="6f9ea-254">默认情况下, 实体框架假定数据库生成主键值。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-254">By default, the Entity Framework assumes that primary key values are generated by the database.</span></span> <span data-ttu-id="6f9ea-255">大多数情况下，这是理想情况。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-255">That's what you want in most scenarios.</span></span> <span data-ttu-id="6f9ea-256">但是, 对于`Course`实体, 你将使用用户指定的课程编号, 如一个部门的1000系列、另一部门的2000系列等等。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-256">However, for `Course` entities, you'll use a user-specified course number such as a 1000 series for one department, a 2000 series for another department, and so on.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="6f9ea-257">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-257">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="6f9ea-258">`Course`实体中的外键属性和导航属性反映以下关系:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-258">The foreign key properties and navigation properties in the `Course` entity reflect the following relationships:</span></span>

- <span data-ttu-id="6f9ea-259">向一个系分配课程后，出于上述原因，会出现 `DepartmentID` 外键和 `Department` 导航属性。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-259">A course is assigned to one department, so there's a `DepartmentID` foreign key and a `Department` navigation property for the reasons mentioned above.</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- <span data-ttu-id="6f9ea-260">参与一门课程的学生数量不定，因此 `Enrollments` 导航属性是一个集合：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-260">A course can have any number of students enrolled in it, so the `Enrollments` navigation property is a collection:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- <span data-ttu-id="6f9ea-261">一门课程可能由多位讲师讲授，因此 `Instructors` 导航属性是一个集合：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-261">A course may be taught by multiple instructors, so the `Instructors` navigation property is a collection:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="create-the-department-entity"></a><span data-ttu-id="6f9ea-262">创建 Department 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-262">Create the Department entity</span></span>

<span data-ttu-id="6f9ea-263">用以下代码创建*Models\Department.cs* :</span><span class="sxs-lookup"><span data-stu-id="6f9ea-263">Create *Models\Department.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a><span data-ttu-id="6f9ea-264">列属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-264">The Column Attribute</span></span>

<span data-ttu-id="6f9ea-265">之前, 你已使用[列属性](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx)更改列名映射。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-265">Earlier you used the [Column attribute](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) to change column name mapping.</span></span> <span data-ttu-id="6f9ea-266">在`Department`实体的代码中`Column` , 特性用于更改 SQL 数据类型映射, 以便使用数据库中的 SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx)类型定义列:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-266">In the code for the `Department` entity, the `Column` attribute is being used to change SQL data type mapping so that the column will be defined using the SQL Server [money](https://msdn.microsoft.com/library/ms179882.aspx) type in the database:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

<span data-ttu-id="6f9ea-267">通常不需要列映射, 因为实体框架通常基于您为属性定义的 CLR 类型选择适当的 SQL Server 数据类型。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-267">Column mapping is generally not required, because the Entity Framework usually chooses the appropriate SQL Server data type based on the CLR type that you define for the property.</span></span> <span data-ttu-id="6f9ea-268">CLR `decimal` 类型会映射到 SQL Server `decimal` 类型。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-268">The CLR `decimal` type maps to a SQL Server `decimal` type.</span></span> <span data-ttu-id="6f9ea-269">但在这种情况下, 您知道列将包含货币金额, 而[money](https://msdn.microsoft.com/library/ms179882.aspx)数据类型则更适合这样做。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-269">But in this case you know that the column will be holding currency amounts, and the [money](https://msdn.microsoft.com/library/ms179882.aspx) data type is more appropriate for that.</span></span> <span data-ttu-id="6f9ea-270">有关 CLR 数据类型以及它们如何与 SQL Server 数据类型匹配的详细信息, 请参阅[SqlClient For Entity sqlclient 类型](https://msdn.microsoft.com/library/bb896344.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-270">For more information about CLR data types and how they match to SQL Server data types, see [SqlClient for Entity FrameworkTypes](https://msdn.microsoft.com/library/bb896344.aspx).</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="6f9ea-271">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-271">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="6f9ea-272">外键和导航属性可反映以下关系：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-272">The foreign key and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="6f9ea-273">一个系可能有也可能没有管理员，而管理员始终是讲师。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-273">A department may or may not have an administrator, and an administrator is always an instructor.</span></span> <span data-ttu-id="6f9ea-274">因此, `InstructorID`该属性包含为`Instructor`实体的外键, 而在`int`类型标识之后添加一个问号, 以将该属性标记为可为 null。导航属性名为`Administrator` , 但`Instructor`包含实体:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-274">Therefore the `InstructorID` property is included as the foreign key to the `Instructor` entity, and a question mark is added after the `int` type designation to mark the property as nullable.The navigation property is named `Administrator` but holds an `Instructor` entity:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- <span data-ttu-id="6f9ea-275">一个部门可能有许多课程, 因此存在一个`Courses`导航属性:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-275">A department may have many courses, so there's a `Courses` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > <span data-ttu-id="6f9ea-276">按照约定，Entity Framework 能针对不可为 null 的外键和多对多关系启用级联删除。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-276">By convention, the Entity Framework enables cascade delete for non-nullable foreign keys and for many-to-many relationships.</span></span> <span data-ttu-id="6f9ea-277">这可能导致循环级联删除规则，尝试添加迁移时该规则会造成异常。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-277">This can result in circular cascade delete rules, which will cause an exception when you try to add a migration.</span></span> <span data-ttu-id="6f9ea-278">例如, 如果未将`Department.InstructorID`属性定义为可为 null, 则会收到以下异常消息:"引用关系将导致循环引用, 这是不允许的。"</span><span class="sxs-lookup"><span data-stu-id="6f9ea-278">For example, if you didn't define the `Department.InstructorID` property as nullable, you'd get the following exception message: "The referential relationship will result in a cyclical reference that's not allowed."</span></span> <span data-ttu-id="6f9ea-279">如果业务规则要求`InstructorID`属性不可为 null, 则必须使用以下 Fluent API 语句禁用关系的级联删除:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-279">If your business rules required `InstructorID` property to be non-nullable, you would have to use the following fluent API statement to disable cascade delete on the relationship:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modify-the-enrollment-entity"></a><span data-ttu-id="6f9ea-280">修改 Enrollment 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-280">Modify the Enrollment entity</span></span>

 <span data-ttu-id="6f9ea-281">在*Models\Enrollment.cs*中, 将之前添加的代码替换为以下代码</span><span class="sxs-lookup"><span data-stu-id="6f9ea-281">In *Models\Enrollment.cs*, replace the code you added earlier with the following code</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=1,15)]

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="6f9ea-282">外键和导航属性</span><span class="sxs-lookup"><span data-stu-id="6f9ea-282">Foreign Key and Navigation Properties</span></span>

<span data-ttu-id="6f9ea-283">外键属性和导航属性可反映以下关系：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-283">The foreign key properties and navigation properties reflect the following relationships:</span></span>

- <span data-ttu-id="6f9ea-284">注册记录面向一门课程，因此存在 `CourseID` 外键属性和 `Course` 导航属性：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-284">An enrollment record is for a single course, so there's a `CourseID` foreign key property and a `Course` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs)]
- <span data-ttu-id="6f9ea-285">注册记录面向一名学生，因此存在 `StudentID` 外键属性和 `Student` 导航属性：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-285">An enrollment record is for a single student, so there's a `StudentID` foreign key property and a `Student` navigation property:</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]

### <a name="many-to-many-relationships"></a><span data-ttu-id="6f9ea-286">多对多关系</span><span class="sxs-lookup"><span data-stu-id="6f9ea-286">Many-to-Many Relationships</span></span>

<span data-ttu-id="6f9ea-287">`Student` `Enrollment`和实体`Course`之间存在多对多关系, 并且实体将作为具有数据库中的*有效负载*的多对多联接表。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-287">There's a many-to-many relationship between the `Student` and `Course` entities, and the `Enrollment` entity functions as a many-to-many join table *with payload* in the database.</span></span> <span data-ttu-id="6f9ea-288">这意味着`Enrollment` , 除了联接的表的外键 (在本例中为主键`Grade`和属性) 外键外, 表还包含其他数据。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-288">This means that the `Enrollment` table contains additional data besides foreign keys for the joined tables (in this case, a primary key and a `Grade` property).</span></span>

<span data-ttu-id="6f9ea-289">下图显示这些关系在实体关系图中的外观。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-289">The following illustration shows what these relationships look like in an entity diagram.</span></span> <span data-ttu-id="6f9ea-290">(此关系图是使用[实体框架 Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)生成的; 创建关系图不是本教程的一部分, 它只是在此处用作说明。)</span><span class="sxs-lookup"><span data-stu-id="6f9ea-290">(This diagram was generated using the [Entity Framework Power Tools](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d); creating the diagram isn't part of the tutorial, it's just being used here as an illustration.)</span></span>

![Student-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

<span data-ttu-id="6f9ea-292">每个关系线在一端有1个, 另一个用\*星号 () 表示一对多关系。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-292">Each relationship line has a 1 at one end and an asterisk (\*) at the other, indicating a one-to-many relationship.</span></span>

<span data-ttu-id="6f9ea-293">如果表未包括评分信息, 只需包含两个外键`CourseID`和`StudentID`。 `Enrollment`</span><span class="sxs-lookup"><span data-stu-id="6f9ea-293">If the `Enrollment` table didn't include grade information, it would only need to contain the two foreign keys `CourseID` and `StudentID`.</span></span> <span data-ttu-id="6f9ea-294">在这种情况下, 它与数据库中*没有负载*(或*纯联接表*) 的多对多联接表相对应, 无需为其创建模型类。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-294">In that case, it would correspond to a many-to-many join table *without payload* (or a *pure join table*) in the database, and you wouldn't have to create a model class for it at all.</span></span> <span data-ttu-id="6f9ea-295">`Instructor` 和`Course`实体具有这种类型的多对多关系, 如您所见, 它们之间没有实体类:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-295">The `Instructor` and `Course` entities have that kind of many-to-many relationship, and as you can see, there is no entity class between them:</span></span>

![Instructor-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

<span data-ttu-id="6f9ea-297">但是, 数据库中需要联接表, 如以下数据库关系图中所示:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-297">A join table is required in the database, however, as shown in the following database diagram:</span></span>

![Instructor-Course_many-to-many_relationship_tables](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

<span data-ttu-id="6f9ea-299">实体框架会自动创建`CourseInstructor`表, 并通过读取和`Instructor.Courses`更新和`Course.Instructors`导航属性来间接读取和更新表。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-299">The Entity Framework automatically creates the `CourseInstructor` table, and you read and update it indirectly by reading and updating the `Instructor.Courses` and `Course.Instructors` navigation properties.</span></span>

## <a name="entity-relationship-diagram"></a><span data-ttu-id="6f9ea-300">实体关系图</span><span class="sxs-lookup"><span data-stu-id="6f9ea-300">Entity relationship diagram</span></span>

<span data-ttu-id="6f9ea-301">下图显示 Entity Framework Power Tools 针对已完成的学校模型创建的关系图。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-301">The following illustration shows the diagram that the Entity Framework Power Tools create for the completed School model.</span></span>

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="6f9ea-303">除了多对多的\*关系线\*和一对多关系线 (1 到\*) 外, 您可以在此处看到`Instructor`与`OfficeAssignment`之间的一对零或一关系线 (1 到 0, 1)。在讲师和部门实体之间, 实体和零或一对多关系线 (0 到\*1)。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-303">Besides the many-to-many relationship lines (\* to \*) and the one-to-many relationship lines (1 to \*), you can see here the one-to-zero-or-one relationship line (1 to 0..1) between the `Instructor` and `OfficeAssignment` entities and the zero-or-one-to-many relationship line (0..1 to \*) between the Instructor and Department entities.</span></span>

## <a name="add-code-to-database-context"></a><span data-ttu-id="6f9ea-304">将代码添加到数据库上下文</span><span class="sxs-lookup"><span data-stu-id="6f9ea-304">Add code to database context</span></span>

<span data-ttu-id="6f9ea-305">接下来, 将新实体添加到`SchoolContext`类, 并使用[Fluent API](https://msdn.microsoft.com/data/jj591617)调用自定义某些映射。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-305">Next you'll add the new entities to the `SchoolContext` class and customize some of the mapping using [fluent API](https://msdn.microsoft.com/data/jj591617) calls.</span></span> <span data-ttu-id="6f9ea-306">API 是 "熟知的", 因为它通常由排列一系列方法调用组合成单个语句, 如以下示例中所示:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-306">The API is "fluent" because it's often used by stringing a series of method calls together into a single statement, as in the following example:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

<span data-ttu-id="6f9ea-307">在本教程中, 你将仅对不能使用属性执行的数据库映射使用 Fluent API。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-307">In this tutorial you'll use the fluent API only for database mapping that you can't do with attributes.</span></span> <span data-ttu-id="6f9ea-308">但 Fluent API 还可用于指定大多数格式化、验证和映射规则，这可通过特性完成。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-308">However, you can also use the fluent API to specify most of the formatting, validation, and mapping rules that you can do by using attributes.</span></span> <span data-ttu-id="6f9ea-309">`MinimumLength` 等特性不能通过 Fluent API 应用。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-309">Some attributes such as `MinimumLength` can't be applied with the fluent API.</span></span> <span data-ttu-id="6f9ea-310">如前所述, `MinimumLength`不会更改架构, 它只应用客户端和服务器端验证规则。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-310">As mentioned previously, `MinimumLength` doesn't change the schema, it only applies a client and server side validation rule</span></span>

<span data-ttu-id="6f9ea-311">某些开发者倾向于仅使用 Fluent API 以保持实体类的“纯净”。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-311">Some developers prefer to use the fluent API exclusively so that they can keep their entity classes "clean."</span></span> <span data-ttu-id="6f9ea-312">如有需要，可混合使用特性和 Fluent API，且有些自定义只能通过 Fluent API 实现，但通常建议选择一种方法并尽可能坚持使用这一种。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-312">You can mix attributes and fluent API if you want, and there are a few customizations that can only be done by using fluent API, but in general the recommended practice is to choose one of these two approaches and use that consistently as much as possible.</span></span>

<span data-ttu-id="6f9ea-313">若要将新实体添加到数据模型, 并使用属性执行你不执行的数据库映射, 请将*DAL\SchoolContext.cs*中的代码替换为以下代码:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-313">To add the new entities to the data model and perform database mapping that you didn't do by using attributes, replace the code in *DAL\SchoolContext.cs* with the following code:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

<span data-ttu-id="6f9ea-314">[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的新语句配置多对多联接表:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-314">The new statement in the [OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) method configures the many-to-many join table:</span></span>

- <span data-ttu-id="6f9ea-315">对于`Instructor` 和`Course`实体之间的多对多关系, 代码指定联接表的表名和列名。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-315">For the many-to-many relationship between the `Instructor` and `Course` entities, the code specifies the table and column names for the join table.</span></span> <span data-ttu-id="6f9ea-316">Code First 可以为你配置多对多关系, 而无需此代码, 但如果不调用此代码, 则将`InstructorInstructorID` `InstructorID`为列获取默认名称, 例如。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-316">Code First can configure the many-to-many relationship for you without this code, but if you don't call it, you will get default names such as `InstructorInstructorID` for the `InstructorID` column.</span></span>

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

<span data-ttu-id="6f9ea-317">下面的代码提供了一个示例, 说明如何使用 Fluent API 而不是特性来指定`Instructor`和`OfficeAssignment`实体之间的关系:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-317">The following code provides an example of how you could have used fluent API instead of attributes to specify the relationship between the `Instructor` and `OfficeAssignment` entities:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

<span data-ttu-id="6f9ea-318">有关 "Fluent API" 语句在幕后执行的操作的信息, 请参阅 "[流畅 API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) " 博客文章。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-318">For information about what "fluent API" statements are doing behind the scenes, see the [Fluent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) blog post.</span></span>

## <a name="seed-database-with-test-data"></a><span data-ttu-id="6f9ea-319">使用测试数据设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="6f9ea-319">Seed database with test data</span></span>

<span data-ttu-id="6f9ea-320">将*Migrations\Configuration.cs*文件中的代码替换为以下代码, 以便为你创建的新实体提供种子数据。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-320">Replace the code in the *Migrations\Configuration.cs* file with the following code in order to provide seed data for the new entities you've created.</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

<span data-ttu-id="6f9ea-321">正如你在第一个教程中看到的那样, 此代码中的大多数只是更新或创建新的实体对象, 并根据测试需要将示例数据加载到属性中。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-321">As you saw in the first tutorial, most of this code simply updates or creates new entity objects and loads sample data into properties as required for testing.</span></span> <span data-ttu-id="6f9ea-322">但请注意, 如何`Course`处理`Instructor`与实体具有多对多关系的实体:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-322">However, notice how the `Course` entity, which has a many-to-many relationship with the `Instructor` entity, is handled:</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

<span data-ttu-id="6f9ea-323">创建`Course`对象时, 可以使用代码`Instructors = new List<Instructor>()`将`Instructors`导航属性初始化为空集合。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-323">When you create a `Course` object, you initialize the `Instructors` navigation property as an empty collection using the code `Instructors = new List<Instructor>()`.</span></span> <span data-ttu-id="6f9ea-324">这样, 便可以使用`Instructor` `Instructors.Add`方法添加与此`Course`相关的实体。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-324">This makes it possible to add `Instructor` entities that are related to this `Course` by using the `Instructors.Add` method.</span></span> <span data-ttu-id="6f9ea-325">如果未创建空列表, 则无法添加这些关系, 因为`Instructors`属性将为 null, 并且不`Add`具有方法。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-325">If you didn't create an empty list, you wouldn't be able to add these relationships, because the `Instructors` property would be null and wouldn't have an `Add` method.</span></span> <span data-ttu-id="6f9ea-326">你还可以将列表初始化添加到构造函数。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-326">You could also add the list initialization to the constructor.</span></span>

## <a name="add-a-migration"></a><span data-ttu-id="6f9ea-327">添加迁移</span><span class="sxs-lookup"><span data-stu-id="6f9ea-327">Add a migration</span></span>

<span data-ttu-id="6f9ea-328">在 PMC 中, 输入`add-migration`命令 (请勿执行此`update-database`命令):</span><span class="sxs-lookup"><span data-stu-id="6f9ea-328">From the PMC, enter the `add-migration` command (don't do the `update-database` command yet):</span></span>

`add-Migration ComplexDataModel`

<span data-ttu-id="6f9ea-329">如果此时尝试运行 `update-database` 命令（先不要执行此操作），则会出现以下错误：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-329">If you tried to run the `update-database` command at this point (don't do it yet), you would get the following error:</span></span>

<span data-ttu-id="6f9ea-330">*ALTER TABLE 语句与外键约束 "FK\_dbo" 冲突。课程\_dbo。部门\_DepartmentID "。在表 "dbo" 的数据库 "ContosoUniversity" 中发生冲突。部门 ", 列" DepartmentID "。*</span><span class="sxs-lookup"><span data-stu-id="6f9ea-330">*The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK\_dbo.Course\_dbo.Department\_DepartmentID". The conflict occurred in database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.*</span></span>

<span data-ttu-id="6f9ea-331">有时, 当您使用现有数据执行迁移时, 您需要将存根 (stub) 数据插入到数据库中以满足外键约束, 这就是您现在必须执行的操作。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-331">Sometimes when you execute migrations with existing data, you need to insert stub data into the database to satisfy foreign key constraints, and that's what you have to do now.</span></span> <span data-ttu-id="6f9ea-332">ComplexDataModel `Up`方法中生成的代码将不可为 null `DepartmentID`的外键添加到`Course`表中。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-332">The generated code in the ComplexDataModel `Up` method adds a non-nullable `DepartmentID` foreign key to the `Course` table.</span></span> <span data-ttu-id="6f9ea-333">由于在代码运行时`Course`表中已有行`AddColumn` , 因此操作将失败, 因为 SQL Server 不知道要放入列中的值不能为 null。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-333">Because there are already rows in the `Course` table when the code runs, the `AddColumn` operation will fail because SQL Server doesn't know what value to put in the column that can't be null.</span></span> <span data-ttu-id="6f9ea-334">因此, 必须更改代码以为新列指定默认值, 并创建一个名为 "Temp" 的存根部作为默认部门。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-334">Therefore have to change the code to give the new column a default value, and create a stub department named "Temp" to act as the default department.</span></span> <span data-ttu-id="6f9ea-335">因此, 在该`Course` `Up`方法运行后, 现有行将与 "Temp" 部门相关。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-335">As a result, existing `Course` rows will all be related to the "Temp" department after the `Up` method runs.</span></span> <span data-ttu-id="6f9ea-336">可以将它们与`Seed`方法中的正确部门相关联。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-336">You can relate them to the correct departments in the `Seed` method.</span></span>

<span data-ttu-id="6f9ea-337">编辑时间*戳\_ComplexDataModel.cs 文件, 注释掉将 DepartmentID 列添加到课程表的代码行, 然后添加以下突出显示的代码 (注释行也是&gt;* &lt;突出显示):</span><span class="sxs-lookup"><span data-stu-id="6f9ea-337">Edit the &lt;*timestamp&gt;\_ComplexDataModel.cs* file, comment out the line of code that adds the DepartmentID column to the Course table, and add the following highlighted code (the commented line is also highlighted):</span></span>

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

<span data-ttu-id="6f9ea-338">当该`Seed`方法运行时, 它将`Department`在表中插入行, 并将现有`Course`行与这些新`Department`行相关。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-338">When the `Seed` method runs, it will insert rows in the `Department` table and it will relate existing `Course` rows to those new `Department` rows.</span></span> <span data-ttu-id="6f9ea-339">如果你尚未在 UI 中添加任何课程, 则不再需要 "Temp" 部门或`Course.DepartmentID`列的默认值。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-339">If you haven't added any courses in the UI, you would then no longer need the "Temp" department or the default value on the `Course.DepartmentID` column.</span></span> <span data-ttu-id="6f9ea-340">若要允许有人使用应用程序添加了课程, 你还需要更新`Seed`方法代码, 以确保所有`Course`行 (不只是先前运行`Seed`方法所插入的行) 具有在`DepartmentID`从列中删除默认值之前有效的值, 并删除 "Temp" 部门。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-340">To allow for the possibility that someone might have added courses by using the application, you'd also want to update the `Seed` method code to ensure that all `Course` rows (not just the ones inserted by earlier runs of the `Seed` method) have valid `DepartmentID` values before you remove the default value from the column and delete the "Temp" department.</span></span>

## <a name="update-the-database"></a><span data-ttu-id="6f9ea-341">更新数据库</span><span class="sxs-lookup"><span data-stu-id="6f9ea-341">Update the database</span></span>

<span data-ttu-id="6f9ea-342">完成&lt; `update-database` *&gt;ComplexDataModel.cs 文件的编辑后, 请在 PMC 中输入命令来执行迁移。\_*</span><span class="sxs-lookup"><span data-stu-id="6f9ea-342">After you have finished editing the &lt;*timestamp&gt;\_ComplexDataModel.cs* file, enter the `update-database` command in the PMC to execute the migration.</span></span>

[!code-powershell[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.ps1)]

> [!NOTE]
> <span data-ttu-id="6f9ea-343">迁移数据和进行架构更改时, 可能会收到其他错误。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-343">It's possible to get other errors when migrating data and making schema changes.</span></span> <span data-ttu-id="6f9ea-344">如果遇到无法解决的迁移错误，你可以更改连接字符串中的数据库名称，或删除数据库。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-344">If you get migration errors you can't resolve, you can either change the database name in the connection string or delete the database.</span></span> <span data-ttu-id="6f9ea-345">最简单的方法是在 web.config 文件中重命名数据库。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-345">The simplest approach is to rename the database in *Web.config* file.</span></span> <span data-ttu-id="6f9ea-346">下面的示例演示更改为 CU\_测试的名称:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-346">The following example shows the name changed to CU\_Test:</span></span>
>
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample36.xml?highlight=1)]
>
> <span data-ttu-id="6f9ea-347">对于新数据库, 没有要迁移的数据, 并且命令更有`update-database`可能在没有错误的情况下完成。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-347">With a new database, there is no data to migrate, and the `update-database` command is much more likely to complete without errors.</span></span> <span data-ttu-id="6f9ea-348">有关如何删除数据库的说明, 请参阅[如何从 Visual Studio 2012 中删除数据库](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/)。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-348">For instructions on how to delete the database, see [How to Drop a Database from Visual Studio 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).</span></span>
>
> <span data-ttu-id="6f9ea-349">如果此操作失败, 可以尝试的另一种方法是, 通过在 PMC 中输入以下命令, 重新初始化数据库:</span><span class="sxs-lookup"><span data-stu-id="6f9ea-349">If that fails, another thing you can try is re-initialize the database by entering the following command in the PMC:</span></span>
>
> `update-database -TargetMigration:0`

<span data-ttu-id="6f9ea-350">像之前一样, 在**服务器资源管理器**中打开数据库, 然后展开 "**表**" 节点以查看是否已创建所有表。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-350">Open the database in **Server Explorer** as you did earlier, and expand the **Tables** node to see that all of the tables have been created.</span></span> <span data-ttu-id="6f9ea-351">(如果您仍在之前打开**服务器资源管理器**, 请单击 "**刷新**" 按钮。)</span><span class="sxs-lookup"><span data-stu-id="6f9ea-351">(If you still have **Server Explorer** open from the earlier time, click the **Refresh** button.)</span></span>

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image16.png)

<span data-ttu-id="6f9ea-352">您没有为`CourseInstructor`该表创建模型类。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-352">You didn't create a model class for the `CourseInstructor` table.</span></span> <span data-ttu-id="6f9ea-353">如前所述, 这是`Instructor`与`Course`实体之间的多对多关系的联接表。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-353">As explained earlier, this is a join table for the many-to-many relationship between the `Instructor` and `Course` entities.</span></span>

<span data-ttu-id="6f9ea-354">右键单击`CourseInstructor`该表, 然后选择 "**显示表数据**", 以验证它是否具有添加到`Instructor` `Course.Instructors`导航属性的实体的结果中的数据。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-354">Right-click the `CourseInstructor` table and select **Show Table Data** to verify that it has data in it as a result of the `Instructor` entities you added to the `Course.Instructors` navigation property.</span></span>

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image17.png)

## <a name="get-the-code"></a><span data-ttu-id="6f9ea-356">获取代码</span><span class="sxs-lookup"><span data-stu-id="6f9ea-356">Get the code</span></span>

[<span data-ttu-id="6f9ea-357">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="6f9ea-357">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="6f9ea-358">其他资源</span><span class="sxs-lookup"><span data-stu-id="6f9ea-358">Additional resources</span></span>

<span data-ttu-id="6f9ea-359">可在[ASP.NET 数据访问-建议的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-359">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f9ea-360">后续步骤</span><span class="sxs-lookup"><span data-stu-id="6f9ea-360">Next steps</span></span>

<span data-ttu-id="6f9ea-361">在本教程中，你将了解：</span><span class="sxs-lookup"><span data-stu-id="6f9ea-361">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6f9ea-362">自定义数据模型</span><span class="sxs-lookup"><span data-stu-id="6f9ea-362">Customized the data model</span></span>
> * <span data-ttu-id="6f9ea-363">更新的学生实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-363">Updated Student entity</span></span>
> * <span data-ttu-id="6f9ea-364">已创建 Instructor 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-364">Created Instructor entity</span></span>
> * <span data-ttu-id="6f9ea-365">已创建 OfficeAssignment 实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-365">Created OfficeAssignment entity</span></span>
> * <span data-ttu-id="6f9ea-366">修改了课程实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-366">Modified the Course entity</span></span>
> * <span data-ttu-id="6f9ea-367">已创建部门实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-367">Created the Department entity</span></span>
> * <span data-ttu-id="6f9ea-368">已修改注册实体</span><span class="sxs-lookup"><span data-stu-id="6f9ea-368">Modified the Enrollment entity</span></span>
> * <span data-ttu-id="6f9ea-369">向数据库上下文添加了代码</span><span class="sxs-lookup"><span data-stu-id="6f9ea-369">Added code to database context</span></span>
> * <span data-ttu-id="6f9ea-370">已使用测试数据设定数据库种子</span><span class="sxs-lookup"><span data-stu-id="6f9ea-370">Seeded database with test data</span></span>
> * <span data-ttu-id="6f9ea-371">已添加迁移</span><span class="sxs-lookup"><span data-stu-id="6f9ea-371">Added a migration</span></span>
> * <span data-ttu-id="6f9ea-372">已更新数据库</span><span class="sxs-lookup"><span data-stu-id="6f9ea-372">Updated the database</span></span>

<span data-ttu-id="6f9ea-373">转到下一篇文章, 了解如何读取和显示实体框架加载到导航属性中的相关数据。</span><span class="sxs-lookup"><span data-stu-id="6f9ea-373">Advance to the next article to learn how to read and display related data that the Entity Framework loads into navigation properties.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6f9ea-374">读取相关数据</span><span class="sxs-lookup"><span data-stu-id="6f9ea-374">Read related data</span></span>](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
