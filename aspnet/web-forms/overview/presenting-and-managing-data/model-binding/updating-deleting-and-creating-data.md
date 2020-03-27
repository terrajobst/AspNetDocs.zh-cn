---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: 通过模型绑定和 web 窗体更新、删除和创建数据 |Microsoft Docs
author: Rick-Anderson
description: 本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。 模型绑定使数据交互更加直接-。
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474134"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a><span data-ttu-id="d2243-104">通过模型绑定和 web 窗体更新、删除和创建数据</span><span class="sxs-lookup"><span data-stu-id="d2243-104">Updating, deleting, and creating data with model binding and web forms</span></span>

<span data-ttu-id="d2243-105">通过[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d2243-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d2243-106">本教程系列演示了将模型绑定用于 ASP.NET Web 窗体项目的基本方面。</span><span class="sxs-lookup"><span data-stu-id="d2243-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="d2243-107">与处理数据源对象（如 ObjectDataSource 或 SqlDataSource）相比，模型绑定使数据交互更直接。</span><span class="sxs-lookup"><span data-stu-id="d2243-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="d2243-108">此系列从介绍性材料开始，并在后面的教程中转到更高级的概念。</span><span class="sxs-lookup"><span data-stu-id="d2243-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="d2243-109">本教程介绍如何通过模型绑定创建、更新和删除数据。</span><span class="sxs-lookup"><span data-stu-id="d2243-109">This tutorial shows how to create, update, and delete data with model binding.</span></span> <span data-ttu-id="d2243-110">你将设置以下属性：</span><span class="sxs-lookup"><span data-stu-id="d2243-110">You will set the following properties:</span></span>
> 
> - <span data-ttu-id="d2243-111">DeleteMethod</span><span class="sxs-lookup"><span data-stu-id="d2243-111">DeleteMethod</span></span>
> - <span data-ttu-id="d2243-112">InsertMethod</span><span class="sxs-lookup"><span data-stu-id="d2243-112">InsertMethod</span></span>
> - <span data-ttu-id="d2243-113">UpdateMethod</span><span class="sxs-lookup"><span data-stu-id="d2243-113">UpdateMethod</span></span>
> 
> <span data-ttu-id="d2243-114">这些属性将接收处理相应操作的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="d2243-114">These properties receive the name of the method that handles the corresponding operation.</span></span> <span data-ttu-id="d2243-115">在该方法中，将提供用于与数据进行交互的逻辑。</span><span class="sxs-lookup"><span data-stu-id="d2243-115">Within that method, you provide the logic for interacting with the data.</span></span>
> 
> <span data-ttu-id="d2243-116">本教程基于在序列的第[一部分](retrieving-data.md)中创建的项目构建。</span><span class="sxs-lookup"><span data-stu-id="d2243-116">This tutorial builds on the project created in the first [part](retrieving-data.md) of the series.</span></span>
> 
> <span data-ttu-id="d2243-117">可以在或 VB 中C#[下载](https://go.microsoft.com/fwlink/?LinkId=286116)完整项目。</span><span class="sxs-lookup"><span data-stu-id="d2243-117">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="d2243-118">可下载的代码适用于 Visual Studio 2012 或 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="d2243-118">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="d2243-119">它使用 Visual Studio 2012 模板，该模板与本教程中所示的 Visual Studio 2013 模板略有不同。</span><span class="sxs-lookup"><span data-stu-id="d2243-119">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="d2243-120">要生成的内容</span><span class="sxs-lookup"><span data-stu-id="d2243-120">What you'll build</span></span>

<span data-ttu-id="d2243-121">在本教程中，你将：</span><span class="sxs-lookup"><span data-stu-id="d2243-121">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="d2243-122">添加动态数据模板</span><span class="sxs-lookup"><span data-stu-id="d2243-122">Add dynamic data templates</span></span>
2. <span data-ttu-id="d2243-123">启用通过模型绑定方法更新和删除数据</span><span class="sxs-lookup"><span data-stu-id="d2243-123">Enable updating and deleting data through model binding methods</span></span>
3. <span data-ttu-id="d2243-124">应用数据验证规则-启用在数据库中创建新记录</span><span class="sxs-lookup"><span data-stu-id="d2243-124">Apply data validation rules - Enable creating a new record in the database</span></span>

## <a name="add-dynamic-data-templates"></a><span data-ttu-id="d2243-125">添加动态数据模板</span><span class="sxs-lookup"><span data-stu-id="d2243-125">Add dynamic data templates</span></span>

<span data-ttu-id="d2243-126">为了提供最佳用户体验并最大程度减少代码重复，你将使用动态数据模板。</span><span class="sxs-lookup"><span data-stu-id="d2243-126">To provide the best user experience and minimize code repetition, you will use dynamic data templates.</span></span> <span data-ttu-id="d2243-127">你可以通过安装 NuGet 包轻松将预先生成的动态数据模板集成到现有站点。</span><span class="sxs-lookup"><span data-stu-id="d2243-127">You can easily integrate pre-built dynamic data templates into your existing site by installing a NuGet package.</span></span>

<span data-ttu-id="d2243-128">从 "**管理 NuGet 包**" 中安装**DynamicDataTemplatesCS**。</span><span class="sxs-lookup"><span data-stu-id="d2243-128">From the **Manage NuGet Packages**, install the **DynamicDataTemplatesCS**.</span></span>

![动态数据模板](updating-deleting-and-creating-data/_static/image1.png)

<span data-ttu-id="d2243-130">请注意，你的项目现在包括一个名为**DynamicData**的文件夹。</span><span class="sxs-lookup"><span data-stu-id="d2243-130">Notice that your project now includes a folder named **DynamicData**.</span></span> <span data-ttu-id="d2243-131">在该文件夹中，你将找到自动应用于 web 窗体中的动态控件的模板。</span><span class="sxs-lookup"><span data-stu-id="d2243-131">In that folder, you will find the templates that are automatically applied to dynamic controls in your web forms.</span></span>

![动态数据文件夹](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a><span data-ttu-id="d2243-133">启用更新和删除</span><span class="sxs-lookup"><span data-stu-id="d2243-133">Enable updating and deleting</span></span>

<span data-ttu-id="d2243-134">使用户能够更新和删除数据库中的记录与检索数据的过程非常相似。</span><span class="sxs-lookup"><span data-stu-id="d2243-134">Enabling users to update and delete records in the database is very similar to the process for retrieving data.</span></span> <span data-ttu-id="d2243-135">在 " **UpdateMethod** " 和 " **DeleteMethod** " 属性中，指定执行这些操作的方法的名称。</span><span class="sxs-lookup"><span data-stu-id="d2243-135">In the **UpdateMethod** and **DeleteMethod** properties, you specify the names of the methods that perform those operations.</span></span> <span data-ttu-id="d2243-136">使用 GridView 控件，还可以指定 "编辑" 和 "删除" 按钮的自动生成。</span><span class="sxs-lookup"><span data-stu-id="d2243-136">With a GridView control, you can also specify the automatic generation of edit and delete buttons.</span></span> <span data-ttu-id="d2243-137">以下突出显示的代码显示了向 GridView 代码添加的内容。</span><span class="sxs-lookup"><span data-stu-id="d2243-137">The following highlighted code shows the additions to the GridView code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

<span data-ttu-id="d2243-138">在代码隐藏文件中，添加用于**system.web. Entity**的 using 语句。</span><span class="sxs-lookup"><span data-stu-id="d2243-138">In the code-behind file, add a using statement for **System.Data.Entity.Infrastructure**.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

<span data-ttu-id="d2243-139">然后，添加以下更新和删除方法。</span><span class="sxs-lookup"><span data-stu-id="d2243-139">Then, add the following update and delete methods.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

<span data-ttu-id="d2243-140">**TryUpdateModel**方法将匹配的数据绑定值从 web 窗体应用到数据项。</span><span class="sxs-lookup"><span data-stu-id="d2243-140">The **TryUpdateModel** method applies the matching data-bound values from the web form to the data item.</span></span> <span data-ttu-id="d2243-141">根据 id 参数的值检索数据项。</span><span class="sxs-lookup"><span data-stu-id="d2243-141">The data item is retrieved based on the value of the id parameter.</span></span>

## <a name="enforce-validation-requirements"></a><span data-ttu-id="d2243-142">强制执行验证要求</span><span class="sxs-lookup"><span data-stu-id="d2243-142">Enforce validation requirements</span></span>

<span data-ttu-id="d2243-143">在更新数据时，将自动强制应用到 Student 类中的 "名字"、"姓氏" 和 "年" 属性的验证特性。</span><span class="sxs-lookup"><span data-stu-id="d2243-143">The validation attributes that you applied to the FirstName, LastName, and Year properties in the Student class are automatically enforced when updating the data.</span></span> <span data-ttu-id="d2243-144">DynamicField 控件基于验证特性添加客户端和服务器验证程序。</span><span class="sxs-lookup"><span data-stu-id="d2243-144">The DynamicField controls add client and server validators based on the validation attributes.</span></span> <span data-ttu-id="d2243-145">FirstName 和 LastName 属性都是必需的。</span><span class="sxs-lookup"><span data-stu-id="d2243-145">The FirstName and LastName properties are both required.</span></span> <span data-ttu-id="d2243-146">FirstName 长度不能超过20个字符，并且 LastName 长度不能超过40个字符。</span><span class="sxs-lookup"><span data-stu-id="d2243-146">FirstName cannot exceed 20 characters in length, and LastName cannot exceed 40 characters.</span></span> <span data-ttu-id="d2243-147">Year 必须是 AcademicYear 枚举的有效值。</span><span class="sxs-lookup"><span data-stu-id="d2243-147">Year must be a valid value for the AcademicYear enumeration.</span></span>

<span data-ttu-id="d2243-148">如果用户违反其中一项验证要求，则不会继续更新。</span><span class="sxs-lookup"><span data-stu-id="d2243-148">If the user violates one of the validation requirements, the update does not proceed.</span></span> <span data-ttu-id="d2243-149">若要查看错误消息，请将 ValidationSummary 控件添加到 GridView 之上。</span><span class="sxs-lookup"><span data-stu-id="d2243-149">To see the error message, add a ValidationSummary control above the GridView.</span></span> <span data-ttu-id="d2243-150">若要显示模型绑定中的验证错误，请将**ShowModelStateErrors**属性设置为**true**。</span><span class="sxs-lookup"><span data-stu-id="d2243-150">To display the validation errors from model binding, set the **ShowModelStateErrors** property set to **true**.</span></span> 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

<span data-ttu-id="d2243-151">运行 web 应用程序，并更新和删除任何记录。</span><span class="sxs-lookup"><span data-stu-id="d2243-151">Run the web application, and update and delete any of the records.</span></span>

![更新数据](updating-deleting-and-creating-data/_static/image3.png)

<span data-ttu-id="d2243-153">请注意，在编辑模式下，Year 属性的值将自动呈现为下拉列表。</span><span class="sxs-lookup"><span data-stu-id="d2243-153">Notice that when in the edit mode the value for the Year property is automatically rendered as a drop down list.</span></span> <span data-ttu-id="d2243-154">Year 属性是一个枚举值，枚举值的动态数据模板指定下拉列表以进行编辑。</span><span class="sxs-lookup"><span data-stu-id="d2243-154">The Year property is an enumeration value, and the dynamic data template for an enumeration value specifies a drop down list for editing.</span></span> <span data-ttu-id="d2243-155">可以通过在**DynamicData**/**FieldTemplates**文件夹中打开**枚举\_编辑 .ascx**文件来找到该模板。</span><span class="sxs-lookup"><span data-stu-id="d2243-155">You can find that template by opening the **Enumeration\_Edit.ascx** file in the **DynamicData**/**FieldTemplates** folder.</span></span>

<span data-ttu-id="d2243-156">如果提供了有效值，则更新成功完成。</span><span class="sxs-lookup"><span data-stu-id="d2243-156">If you provide valid values, the update completes successfully.</span></span> <span data-ttu-id="d2243-157">如果违反其中一项验证要求，则更新不会继续，并且会在网格上方显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="d2243-157">If you violate one of the validation requirements, the update does not proceed and an error message is displayed above the grid.</span></span>

![错误消息](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a><span data-ttu-id="d2243-159">添加新记录</span><span class="sxs-lookup"><span data-stu-id="d2243-159">Add new records</span></span>

<span data-ttu-id="d2243-160">GridView 控件不包含**InsertMethod**属性，因此不能用于添加具有模型绑定的新记录。</span><span class="sxs-lookup"><span data-stu-id="d2243-160">The GridView control does not include the **InsertMethod** property and therefore cannot be used for adding a new record with model binding.</span></span> <span data-ttu-id="d2243-161">可以在**FormView**、 **DetailsView**或**ListView**控件中找到 InsertMethod 属性。</span><span class="sxs-lookup"><span data-stu-id="d2243-161">You can find the InsertMethod property in the **FormView**, **DetailsView**, or **ListView** controls.</span></span> <span data-ttu-id="d2243-162">在本教程中，您将使用 FormView 控件来添加新记录。</span><span class="sxs-lookup"><span data-stu-id="d2243-162">In this tutorial, you will use a FormView control to add a new record.</span></span>

<span data-ttu-id="d2243-163">首先，将一个链接添加到要创建的新页面，以便添加新记录。</span><span class="sxs-lookup"><span data-stu-id="d2243-163">First, add a link to the new page you will create for adding a new record.</span></span> <span data-ttu-id="d2243-164">在 ValidationSummary 上，添加：</span><span class="sxs-lookup"><span data-stu-id="d2243-164">Above the ValidationSummary, add:</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

<span data-ttu-id="d2243-165">新链接将出现在 "学生" 页的内容顶部。</span><span class="sxs-lookup"><span data-stu-id="d2243-165">The new link will appear at the top of the content for the Students page.</span></span>

![新建链接](updating-deleting-and-creating-data/_static/image5.png)

<span data-ttu-id="d2243-167">然后，使用母版页添加新的 web 窗体，并将其命名为**AddStudent**。</span><span class="sxs-lookup"><span data-stu-id="d2243-167">Then, add a new web form using a master page, and name it **AddStudent**.</span></span> <span data-ttu-id="d2243-168">选择 "站点" 作为母版页。</span><span class="sxs-lookup"><span data-stu-id="d2243-168">Select Site.Master as the master page.</span></span>

<span data-ttu-id="d2243-169">您将使用**DynamicEntity**控件呈现添加新学生的字段。</span><span class="sxs-lookup"><span data-stu-id="d2243-169">You will render the fields for adding a new student by using a **DynamicEntity** control.</span></span> <span data-ttu-id="d2243-170">DynamicEntity 控件呈现在 ItemType 属性中指定的类中可编辑的属性。</span><span class="sxs-lookup"><span data-stu-id="d2243-170">The DynamicEntity control renders that editable properties in the class specified in the ItemType property.</span></span> <span data-ttu-id="d2243-171">StudentID 属性标记有 **[ScaffoldColumn （false）]** 属性，因此不会呈现。</span><span class="sxs-lookup"><span data-stu-id="d2243-171">The StudentID property was marked with the **[ScaffoldColumn(false)]** attribute so it is not rendered.</span></span> <span data-ttu-id="d2243-172">在 AddStudent 页的 MainContent 占位符中，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="d2243-172">In the MainContent placeholder of the AddStudent page, add the following code.</span></span>

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

<span data-ttu-id="d2243-173">在代码隐藏文件（AddStudent.aspx.cs）中，为**ContosoUniversityModelBinding**命名空间添加**using**语句。</span><span class="sxs-lookup"><span data-stu-id="d2243-173">In the code-behind file (AddStudent.aspx.cs), add a **using** statement for the **ContosoUniversityModelBinding.Models** namespace.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

<span data-ttu-id="d2243-174">然后，添加以下方法，以指定如何为 "取消" 按钮插入新记录和事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="d2243-174">Then, add the following methods to specify how to insert a new record and an event handler for the cancel button.</span></span>

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

<span data-ttu-id="d2243-175">保存所有更改。</span><span class="sxs-lookup"><span data-stu-id="d2243-175">Save all of the changes.</span></span>

<span data-ttu-id="d2243-176">运行 web 应用程序并创建新的学生。</span><span class="sxs-lookup"><span data-stu-id="d2243-176">Run the web application and create a new student.</span></span>

![添加新的学生](updating-deleting-and-creating-data/_static/image6.png)

<span data-ttu-id="d2243-178">单击 "**插入**"，可以看到已创建新的学生。</span><span class="sxs-lookup"><span data-stu-id="d2243-178">Click **Insert** and notice the new student has been created.</span></span>

![显示新的学生](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a><span data-ttu-id="d2243-180">结论</span><span class="sxs-lookup"><span data-stu-id="d2243-180">Conclusion</span></span>

<span data-ttu-id="d2243-181">在本教程中，你已启用更新、删除和创建数据。</span><span class="sxs-lookup"><span data-stu-id="d2243-181">In this tutorial, you enabled updating, deleting, and creating data.</span></span> <span data-ttu-id="d2243-182">在与数据进行交互时，已确保应用验证规则。</span><span class="sxs-lookup"><span data-stu-id="d2243-182">You ensured validation rules are applied when interacting with the data.</span></span>

<span data-ttu-id="d2243-183">在本系列的下一个[教程](sorting-paging-and-filtering-data.md)中，您将启用排序、分页和筛选数据。</span><span class="sxs-lookup"><span data-stu-id="d2243-183">In the next [tutorial](sorting-paging-and-filtering-data.md) in this series, you will enable sorting, paging, and filtering data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d2243-184">[上一页](retrieving-data.md)
> [下一页](sorting-paging-and-filtering-data.md)</span><span class="sxs-lookup"><span data-stu-id="d2243-184">[Previous](retrieving-data.md)
[Next](sorting-paging-and-filtering-data.md)</span></span>
