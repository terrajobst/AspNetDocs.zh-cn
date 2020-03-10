---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
title: 通过数据批注验证程序进行验证（VB） |Microsoft Docs
author: microsoft
description: 利用数据批注模型绑定器在 ASP.NET MVC 应用程序中执行验证。 了解如何使用不同类型的验证程序 。
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 0d23ff2b-f2ec-434a-be3b-1180beeccba3
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-vb
msc.type: authoredcontent
ms.openlocfilehash: 00150575baabc659f7dd0c07349cde52105f6c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435938"
---
# <a name="validation-with-the-data-annotation-validators-vb"></a><span data-ttu-id="94a06-104">使用数据注释验证程序进行验证 (VB)</span><span class="sxs-lookup"><span data-stu-id="94a06-104">Validation with the Data Annotation Validators (VB)</span></span>

<span data-ttu-id="94a06-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="94a06-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="94a06-106">利用数据批注模型绑定器在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="94a06-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="94a06-107">了解如何使用不同类型的验证程序属性并在 Microsoft 实体框架中处理它们。</span><span class="sxs-lookup"><span data-stu-id="94a06-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="94a06-108">在本教程中，将了解如何使用数据批注验证程序在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="94a06-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="94a06-109">使用数据批注验证程序的优点在于，只需将一个或多个属性（如 Required 或 StringLength 属性）添加到类属性即可执行验证。</span><span class="sxs-lookup"><span data-stu-id="94a06-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="94a06-110">在可以使用数据批注验证程序之前，必须下载数据批注模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="94a06-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="94a06-111">通过单击[此处](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471)，可以从 CodePlex 网站下载数据批注模型绑定器示例。</span><span class="sxs-lookup"><span data-stu-id="94a06-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="94a06-112">必须了解的是，数据批注模型联编程序不是 Microsoft ASP.NET MVC 框架的官方部分。</span><span class="sxs-lookup"><span data-stu-id="94a06-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="94a06-113">尽管数据批注模型联编程序由 Microsoft ASP.NET MVC 团队创建，但对于本教程中介绍和使用的数据批注模型联编程序，Microsoft 不提供正式的产品支持。</span><span class="sxs-lookup"><span data-stu-id="94a06-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="94a06-114">使用数据批注模型联编程序</span><span class="sxs-lookup"><span data-stu-id="94a06-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="94a06-115">若要在 ASP.NET MVC 应用程序中使用数据批注模型联编程序，首先需要添加对 DataAnnotations 程序集和 System.componentmodel. DataAnnotations 程序集的引用的引用。</span><span class="sxs-lookup"><span data-stu-id="94a06-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="94a06-116">选择菜单选项 "**项目"、"添加引用"** 。</span><span class="sxs-lookup"><span data-stu-id="94a06-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="94a06-117">接下来，单击 "**浏览**" 选项卡，然后浏览到数据批注模型绑定器示例的下载位置（和解压 **）。**</span><span class="sxs-lookup"><span data-stu-id="94a06-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image2.png)](validation-with-the-data-annotation-validators-vb/_static/image1.png)

<span data-ttu-id="94a06-118">**图 1**：添加对数据批注模型联编程序的引用（[单击查看完全大小的图像](validation-with-the-data-annotation-validators-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="94a06-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image3.png))</span></span>

<span data-ttu-id="94a06-119">同时选择 DataAnnotations 程序集和 DataAnnotations 程序集，然后单击 **"确定" （"确定"** 按钮）。</span><span class="sxs-lookup"><span data-stu-id="94a06-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="94a06-120">不能将 .NET Framework Service Pack 1 随附的 DataAnnotations 程序集用于数据批注模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="94a06-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="94a06-121">必须使用数据批注模型绑定器示例下载中包含的 System.componentmodel. DataAnnotations 程序集版本。</span><span class="sxs-lookup"><span data-stu-id="94a06-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="94a06-122">最后，需要在 global.asax 文件中注册 DataAnnotations 模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="94a06-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="94a06-123">将以下代码行添加到应用程序\_Start （）事件处理程序，使应用程序\_Start （）方法如下所示：</span><span class="sxs-lookup"><span data-stu-id="94a06-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample1.vb)]

<span data-ttu-id="94a06-124">下面这行代码会将 DataAnnotationsModelBinder 注册为整个 ASP.NET MVC 应用程序的默认模型联编程序。</span><span class="sxs-lookup"><span data-stu-id="94a06-124">This line of code registers the DataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="94a06-125">使用数据批注验证程序特性</span><span class="sxs-lookup"><span data-stu-id="94a06-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="94a06-126">使用数据批注模型绑定器时，将使用验证程序特性来执行验证。</span><span class="sxs-lookup"><span data-stu-id="94a06-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="94a06-127">System.componentmodel. DataAnnotations 命名空间包括以下验证程序特性：</span><span class="sxs-lookup"><span data-stu-id="94a06-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="94a06-128">范围–用于验证属性的值是否在指定的值范围之间。</span><span class="sxs-lookup"><span data-stu-id="94a06-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="94a06-129">RegularExpression –用于验证属性的值是否与指定的正则表达式模式匹配。</span><span class="sxs-lookup"><span data-stu-id="94a06-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="94a06-130">必需–使你能够根据需要标记属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="94a06-131">StringLength-用于指定字符串属性的最大长度。</span><span class="sxs-lookup"><span data-stu-id="94a06-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="94a06-132">验证–所有验证程序特性的基类。</span><span class="sxs-lookup"><span data-stu-id="94a06-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="94a06-133">如果任何标准验证程序都不满足您的验证需求，则您始终可以通过从基本验证属性继承新的验证程序属性，来创建自定义验证程序特性。</span><span class="sxs-lookup"><span data-stu-id="94a06-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="94a06-134">**列表 1**中的 Product 类演示了如何使用这些验证程序特性。</span><span class="sxs-lookup"><span data-stu-id="94a06-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="94a06-135">"名称"、"说明" 和 "单价" 属性标记为 "必需"。</span><span class="sxs-lookup"><span data-stu-id="94a06-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="94a06-136">Name 属性的字符串长度必须小于10个字符。</span><span class="sxs-lookup"><span data-stu-id="94a06-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="94a06-137">最后，"单价" 属性必须与表示货币金额的正则表达式模式匹配。</span><span class="sxs-lookup"><span data-stu-id="94a06-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample2.vb)]

<span data-ttu-id="94a06-138">**列表 1**： Models\Product.vb</span><span class="sxs-lookup"><span data-stu-id="94a06-138">**Listing 1**: Models\Product.vb</span></span>

<span data-ttu-id="94a06-139">Product 类阐释了如何使用另一个特性： DisplayName 特性。</span><span class="sxs-lookup"><span data-stu-id="94a06-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="94a06-140">当属性显示在错误消息中时，DisplayName 特性使你可以修改属性的名称。</span><span class="sxs-lookup"><span data-stu-id="94a06-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="94a06-141">您可以显示错误消息 "需要此价格字段"，而不是显示错误消息 "需要单价字段"。</span><span class="sxs-lookup"><span data-stu-id="94a06-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="94a06-142">如果要完全自定义验证程序所显示的错误消息，可以将自定义错误消息分配给验证程序的 ErrorMessage 属性，如下所示： `<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="94a06-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="94a06-143">您可以在列表**1**中使用 Product 类，并在**列表 2**中使用 Create （）控制器操作。</span><span class="sxs-lookup"><span data-stu-id="94a06-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="94a06-144">当模型状态包含任何错误时，此控制器操作会重新显示 "创建" 视图。</span><span class="sxs-lookup"><span data-stu-id="94a06-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample3.vb)]

<span data-ttu-id="94a06-145">**列表 2**： Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="94a06-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="94a06-146">最后，您可以通过右键单击 Create （）操作并选择菜单选项 "**添加视图**"，在**列表 3**中创建视图。</span><span class="sxs-lookup"><span data-stu-id="94a06-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="94a06-147">使用 Product 类作为模型类创建强类型视图。</span><span class="sxs-lookup"><span data-stu-id="94a06-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="94a06-148">从 "查看内容" 下拉列表中选择 "**创建**" （参见**图 2**）。</span><span class="sxs-lookup"><span data-stu-id="94a06-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image5.png)](validation-with-the-data-annotation-validators-vb/_static/image4.png)

<span data-ttu-id="94a06-149">**图 2**：添加 "创建" 视图</span><span class="sxs-lookup"><span data-stu-id="94a06-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-vb/samples/sample4.aspx)]

<span data-ttu-id="94a06-150">**列表 3**： Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="94a06-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="94a06-151">从 "**添加视图**" 菜单选项生成的创建窗体中删除 Id 字段。</span><span class="sxs-lookup"><span data-stu-id="94a06-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="94a06-152">由于 Id 字段对应于标识列，因此不希望允许用户为此字段输入值。</span><span class="sxs-lookup"><span data-stu-id="94a06-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="94a06-153">如果您提交用于创建产品的表单，并且没有为必填字段输入值，则将显示**图 3**中的验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="94a06-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image7.png)](validation-with-the-data-annotation-validators-vb/_static/image6.png)

<span data-ttu-id="94a06-154">**图 3**：缺少必填字段</span><span class="sxs-lookup"><span data-stu-id="94a06-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="94a06-155">如果输入的货币金额无效，则会显示**图 4**中的错误消息。</span><span class="sxs-lookup"><span data-stu-id="94a06-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image9.png)](validation-with-the-data-annotation-validators-vb/_static/image8.png)

<span data-ttu-id="94a06-156">**图 4**：货币金额无效</span><span class="sxs-lookup"><span data-stu-id="94a06-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="94a06-157">将数据批注验证程序用于实体框架</span><span class="sxs-lookup"><span data-stu-id="94a06-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="94a06-158">如果使用 Microsoft 实体框架生成数据模型类，则不能将验证程序特性直接应用于类。</span><span class="sxs-lookup"><span data-stu-id="94a06-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="94a06-159">由于 Entity Framework Designer 会生成模型类，因此，在设计器中进行任何更改时，对模型类所做的任何更改都将被覆盖。</span><span class="sxs-lookup"><span data-stu-id="94a06-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="94a06-160">如果要将验证程序与实体框架生成的类一起使用，则需要创建元数据类。</span><span class="sxs-lookup"><span data-stu-id="94a06-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="94a06-161">将验证程序应用于元数据类，而不是将验证程序应用于实际的类。</span><span class="sxs-lookup"><span data-stu-id="94a06-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="94a06-162">例如，假设您已使用实体框架创建了一个 Movie 类（见**图 5**）。</span><span class="sxs-lookup"><span data-stu-id="94a06-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="94a06-163">而且，假设要使影片标题和控制器属性为必填属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="94a06-164">在这种情况下，可以在**列表 4**中创建分部类和元数据类。</span><span class="sxs-lookup"><span data-stu-id="94a06-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image11.png)](validation-with-the-data-annotation-validators-vb/_static/image10.png)

<span data-ttu-id="94a06-165">**图 5**：由实体框架生成的 Movie 类</span><span class="sxs-lookup"><span data-stu-id="94a06-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-vb[Main](validation-with-the-data-annotation-validators-vb/samples/sample5.vb)]

<span data-ttu-id="94a06-166">**列表 4**： Models\Movie.vb</span><span class="sxs-lookup"><span data-stu-id="94a06-166">**Listing 4**: Models\Movie.vb</span></span>

<span data-ttu-id="94a06-167">**列表 4**中的文件包含两个名为 "Movie" 和 "MovieMetaData" 的类。</span><span class="sxs-lookup"><span data-stu-id="94a06-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="94a06-168">Movie 类是一个分部类。</span><span class="sxs-lookup"><span data-stu-id="94a06-168">The Movie class is a partial class.</span></span> <span data-ttu-id="94a06-169">它对应于 DataModel 文件中包含的实体框架生成的分部类。</span><span class="sxs-lookup"><span data-stu-id="94a06-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="94a06-170">目前，.NET framework 不支持部分属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="94a06-171">因此，无法将验证程序特性应用于 DataModel 文件中定义的 Movie 类的属性，方法是将验证程序特性应用到在**列表 4**中定义的电影类的属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="94a06-172">请注意，Movie 分部类使用指向 MovieMetaData 类的 MetadataType 特性进行修饰。</span><span class="sxs-lookup"><span data-stu-id="94a06-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="94a06-173">MovieMetaData 类包含 Movie 类的属性的代理属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="94a06-174">验证程序属性应用于 MovieMetaData 类的属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="94a06-175">Title、Director 和 DateReleased 属性都标记为必需属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="94a06-176">必须为 Director 属性分配一个包含少于5个字符的字符串。</span><span class="sxs-lookup"><span data-stu-id="94a06-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="94a06-177">最后，将 DisplayName 特性应用到 DateReleased 属性，以显示一条错误消息，如 "所需的日期字段为必填字段"。</span><span class="sxs-lookup"><span data-stu-id="94a06-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="94a06-178">而不是 "DateReleased" 字段是必需的。</span><span class="sxs-lookup"><span data-stu-id="94a06-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="94a06-179">请注意，MovieMetaData 类中的代理属性不需要与 Movie 类中的相应属性表示相同的类型。</span><span class="sxs-lookup"><span data-stu-id="94a06-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="94a06-180">例如，Director 属性是 Movie 类中的字符串属性和 MovieMetaData 类中的对象属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="94a06-181">**图 6**中的页说明了为电影属性输入无效值时返回的错误消息。</span><span class="sxs-lookup"><span data-stu-id="94a06-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-vb/_static/image13.png)](validation-with-the-data-annotation-validators-vb/_static/image12.png)

<span data-ttu-id="94a06-182">**图 6**：在实体框架中使用验证器（[单击查看完全大小的图像](validation-with-the-data-annotation-validators-vb/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="94a06-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-vb/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="94a06-183">摘要</span><span class="sxs-lookup"><span data-stu-id="94a06-183">Summary</span></span>

<span data-ttu-id="94a06-184">在本教程中，已学习如何利用数据批注模型联编程序在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="94a06-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="94a06-185">已了解如何使用不同类型的验证程序属性，如 Required 和 StringLength 属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="94a06-186">还了解了如何在使用 Microsoft 实体框架时使用这些属性。</span><span class="sxs-lookup"><span data-stu-id="94a06-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="94a06-187">上一页</span><span class="sxs-lookup"><span data-stu-id="94a06-187">Previous</span></span>](validating-with-a-service-layer-vb.md)
