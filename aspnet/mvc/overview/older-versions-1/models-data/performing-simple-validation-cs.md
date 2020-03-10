---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
title: 执行简单验证（C#） |Microsoft Docs
author: StephenWalther
description: 了解如何在 ASP.NET MVC 应用程序中执行验证。 在本教程中，Stephen Walther 介绍了模型状态和验证 HTML 帮助器 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 21383c9d-6aea-4bad-a99b-b5f2c9d6503f
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: e33f522af74efe97b5a245e956bc0b918ea769af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436718"
---
# <a name="performing-simple-validation-c"></a><span data-ttu-id="771de-104">执行简单验证 (C#)</span><span class="sxs-lookup"><span data-stu-id="771de-104">Performing Simple Validation (C#)</span></span>

<span data-ttu-id="771de-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="771de-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="771de-106">了解如何在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="771de-106">Learn how to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="771de-107">在本教程中，Stephen Walther 介绍了模型状态和验证 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="771de-107">In this tutorial, Stephen Walther introduces you to model state and the validation HTML helpers.</span></span>

<span data-ttu-id="771de-108">本教程的目的是介绍如何在 ASP.NET MVC 应用程序中执行验证。</span><span class="sxs-lookup"><span data-stu-id="771de-108">The goal of this tutorial is to explain how you can perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="771de-109">例如，您将了解如何防止某人提交不包含必填字段值的表单。</span><span class="sxs-lookup"><span data-stu-id="771de-109">For example, you learn how to prevent someone from submitting a form that does not contain a value for a required field.</span></span> <span data-ttu-id="771de-110">了解如何使用模型状态和验证 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="771de-110">You learn how to use model state and the validation HTML helpers.</span></span>

## <a name="understanding-model-state"></a><span data-ttu-id="771de-111">了解模型状态</span><span class="sxs-lookup"><span data-stu-id="771de-111">Understanding Model State</span></span>

<span data-ttu-id="771de-112">您可以使用模型状态（或者更准确地说，模型状态字典）来表示验证错误。</span><span class="sxs-lookup"><span data-stu-id="771de-112">You use model state - or more accurately, the model state dictionary - to represent validation errors.</span></span> <span data-ttu-id="771de-113">例如，在将 Product 类添加到数据库之前，列表1中的 Create （）操作将验证 Product 类的属性。</span><span class="sxs-lookup"><span data-stu-id="771de-113">For example, the Create() action in Listing 1 validates the properties of a Product class before adding the Product class to a database.</span></span>

<span data-ttu-id="771de-114">我不建议将验证或数据库逻辑添加到控制器。</span><span class="sxs-lookup"><span data-stu-id="771de-114">I'm not recommending that you add your validation or database logic to a controller.</span></span> <span data-ttu-id="771de-115">控制器仅应包含与应用程序流控制相关的逻辑。</span><span class="sxs-lookup"><span data-stu-id="771de-115">A controller should contain only logic related to application flow control.</span></span> <span data-ttu-id="771de-116">我们将使用一种快捷方式，使其保持简单。</span><span class="sxs-lookup"><span data-stu-id="771de-116">We are taking a shortcut to keep things simple.</span></span>

<span data-ttu-id="771de-117">**列表 1-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="771de-117">**Listing 1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](performing-simple-validation-cs/samples/sample1.cs)]

<span data-ttu-id="771de-118">在 "列表 1" 中，将验证 Product 类的 "名称"、"说明" 和 "库存量" 属性。</span><span class="sxs-lookup"><span data-stu-id="771de-118">In Listing 1, the Name, Description, and UnitsInStock properties of the Product class are validated.</span></span> <span data-ttu-id="771de-119">如果这些属性中的任何一个未能通过验证测试，则会将错误添加到模型状态字典（由控制器类的 ModelState 属性表示）。</span><span class="sxs-lookup"><span data-stu-id="771de-119">If any of these properties fail a validation test then an error is added to the model state dictionary (represented by the ModelState property of the Controller class).</span></span>

<span data-ttu-id="771de-120">如果模型状态中有任何错误，则 ModelState 属性返回 false。</span><span class="sxs-lookup"><span data-stu-id="771de-120">If there are any errors in model state then the ModelState.IsValid property returns false.</span></span> <span data-ttu-id="771de-121">在这种情况下，将重新显示用于创建新产品的 HTML 表单。</span><span class="sxs-lookup"><span data-stu-id="771de-121">In that case, the HTML form for creating a new product is redisplayed.</span></span> <span data-ttu-id="771de-122">否则，如果没有验证错误，则会将新产品添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="771de-122">Otherwise, if there are no validation errors, the new Product is added to the database.</span></span>

## <a name="using-the-validation-helpers"></a><span data-ttu-id="771de-123">使用验证帮助器</span><span class="sxs-lookup"><span data-stu-id="771de-123">Using the Validation Helpers</span></span>

<span data-ttu-id="771de-124">ASP.NET MVC 框架包含两个验证帮助器： ValidationMessage （） helper 和 ValidationSummary （）帮助程序。</span><span class="sxs-lookup"><span data-stu-id="771de-124">The ASP.NET MVC framework includes two validation helpers: the Html.ValidationMessage() helper and the Html.ValidationSummary() helper.</span></span> <span data-ttu-id="771de-125">可在视图中使用这两个帮助器来显示验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="771de-125">You use these two helpers in a view to display validation error messages.</span></span>

<span data-ttu-id="771de-126">ValidationMessage （）和 ValidationSummary （）帮助器用于 ASP.NET MVC 基架自动生成的 "创建" 和 "编辑" 视图。</span><span class="sxs-lookup"><span data-stu-id="771de-126">The Html.ValidationMessage() and Html.ValidationSummary() helpers are used in the Create and Edit views that are generated automatically by the ASP.NET MVC scaffolding.</span></span> <span data-ttu-id="771de-127">按照以下步骤生成创建视图：</span><span class="sxs-lookup"><span data-stu-id="771de-127">Follow these steps to generate the Create view:</span></span>

1. <span data-ttu-id="771de-128">右键单击产品控制器中的 "创建" （）操作，然后选择 "**添加视图**" 菜单选项（参见图1）。</span><span class="sxs-lookup"><span data-stu-id="771de-128">Right-click the Create() action in the Product controller and select the menu option **Add View** (see Figure 1).</span></span>
2. <span data-ttu-id="771de-129">在 "**添加视图**" 对话框中，选中标记为 "**创建强类型视图**" 的复选框（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="771de-129">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view** (see Figure 2).</span></span>
3. <span data-ttu-id="771de-130">从 "**查看数据类**" 下拉列表中，选择 "产品类"。</span><span class="sxs-lookup"><span data-stu-id="771de-130">From the **View data class** dropdown list, select the Product class.</span></span>
4. <span data-ttu-id="771de-131">从 "**查看内容**" 下拉列表中，选择 "创建"。</span><span class="sxs-lookup"><span data-stu-id="771de-131">From the **View content** dropdown list, select Create.</span></span>
5. <span data-ttu-id="771de-132">单击“添加”按钮。</span><span class="sxs-lookup"><span data-stu-id="771de-132">Click the **Add** button.</span></span>

<span data-ttu-id="771de-133">请确保在添加视图之前生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="771de-133">Make sure that you build your application before adding a view.</span></span> <span data-ttu-id="771de-134">否则，类的列表将不会显示在 "**查看数据类**" 下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="771de-134">Otherwise, the list of classes won't appear in the **View data class** dropdown list.</span></span>

<span data-ttu-id="771de-135">[!["新建项目" 对话框](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="771de-135">[![The New Project dialog box](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)</span></span>

<span data-ttu-id="771de-136">**图 01**：添加视图（[单击查看完全尺寸的图像](performing-simple-validation-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="771de-136">**Figure 01**: Adding a view([Click to view full-size image](performing-simple-validation-cs/_static/image2.png))</span></span>

<span data-ttu-id="771de-137">[!["新建项目" 对话框](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="771de-137">[![The New Project dialog box](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)</span></span>

<span data-ttu-id="771de-138">**图 02**：创建强类型视图（[单击查看完全大小的图像](performing-simple-validation-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="771de-138">**Figure 02**: Creating a strongly-typed view ([Click to view full-size image](performing-simple-validation-cs/_static/image4.png))</span></span>

<span data-ttu-id="771de-139">完成这些步骤后，将获得列表2中的 "创建" 视图。</span><span class="sxs-lookup"><span data-stu-id="771de-139">After you complete these steps, you get the Create view in Listing 2.</span></span>

<span data-ttu-id="771de-140">**列表 2-Views\Product\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="771de-140">**Listing 2 - Views\Product\Create.aspx**</span></span>

[!code-aspx[Main](performing-simple-validation-cs/samples/sample2.aspx)]

<span data-ttu-id="771de-141">在列表2中，html 窗体上立即调用 ValidationSummary （）帮助程序。</span><span class="sxs-lookup"><span data-stu-id="771de-141">In Listing 2, the Html.ValidationSummary() helper is called immediately above the HTML form.</span></span> <span data-ttu-id="771de-142">此帮助程序用于显示验证错误消息的列表。</span><span class="sxs-lookup"><span data-stu-id="771de-142">This helper is used to display a list of validation error messages.</span></span> <span data-ttu-id="771de-143">ValidationSummary （） helper 在项目符号列表中呈现错误。</span><span class="sxs-lookup"><span data-stu-id="771de-143">The Html.ValidationSummary() helper renders the errors in a bulleted list.</span></span>

<span data-ttu-id="771de-144">在每个 HTML 窗体字段的旁边调用 ValidationMessage （）帮助程序。</span><span class="sxs-lookup"><span data-stu-id="771de-144">The Html.ValidationMessage() helper is called next to each of the HTML form fields.</span></span> <span data-ttu-id="771de-145">此帮助器用于在窗体字段的旁边显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="771de-145">This helper is used to display an error message right next to a form field.</span></span> <span data-ttu-id="771de-146">对于列表2，当出错时，ValidationMessage （） helper 会显示星号。</span><span class="sxs-lookup"><span data-stu-id="771de-146">In the case of Listing 2, the Html.ValidationMessage() helper displays an asterisk when there is an error.</span></span>

<span data-ttu-id="771de-147">图3中的页说明了在使用缺失字段和无效值提交窗体时，验证帮助程序呈现的错误消息。</span><span class="sxs-lookup"><span data-stu-id="771de-147">The page in Figure 3 illustrates the error messages rendered by the validation helpers when the form is submitted with missing fields and invalid values.</span></span>

<span data-ttu-id="771de-148">[!["新建项目" 对话框](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="771de-148">[![The New Project dialog box](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)</span></span>

<span data-ttu-id="771de-149">**图 03**：已提交的创建视图出现问题（[单击以查看完全大小的图像](performing-simple-validation-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="771de-149">**Figure 03**: The Create view submitted with problems ([Click to view full-size image](performing-simple-validation-cs/_static/image6.png))</span></span>

<span data-ttu-id="771de-150">请注意，当存在验证错误时，还会修改 HTML 输入字段的外观。</span><span class="sxs-lookup"><span data-stu-id="771de-150">Notice that the appearance of the HTML input fields are also modified when there is a validation error.</span></span> <span data-ttu-id="771de-151">当存在与 Html. TextBox （） helper 呈现的属性关联的验证错误时，Html. TextBox （）帮助器将呈现*类 = "输入验证-错误"* 特性。</span><span class="sxs-lookup"><span data-stu-id="771de-151">The Html.TextBox() helper renders a *class="input-validation-error"* attribute when there is a validation error associated with the property rendered by the Html.TextBox() helper.</span></span>

<span data-ttu-id="771de-152">有三个用于控制验证错误外观的级联样式表类：</span><span class="sxs-lookup"><span data-stu-id="771de-152">There are three cascading style sheet classes used to control the appearance of validation errors:</span></span>

- <span data-ttu-id="771de-153">输入验证-错误-应用于 Html. TextBox （） helper 呈现&gt; 标记的 &lt;输入。</span><span class="sxs-lookup"><span data-stu-id="771de-153">input-validation-error - Applied to the &lt;input&gt; tag rendered by Html.TextBox() helper.</span></span>
- <span data-ttu-id="771de-154">字段验证-错误-应用于 ValidationMessage （）帮助程序呈现&gt; 标记的 &lt;范围。</span><span class="sxs-lookup"><span data-stu-id="771de-154">field-validation-error - Applied to the &lt;span&gt; tag rendered by the Html.ValidationMessage() helper.</span></span>
- <span data-ttu-id="771de-155">验证-摘要-错误-应用于 ValidationSummary （）帮助程序呈现的 &lt;ul&gt; 标记。</span><span class="sxs-lookup"><span data-stu-id="771de-155">validation-summary-errors - Applied to the &lt;ul&gt; tag rendered by the Html.ValidationSummary() helper.</span></span>

<span data-ttu-id="771de-156">您可以修改这些级联样式表类，并因此通过修改位于 Content 文件夹中的 web.config 文件来修改验证错误的外观。</span><span class="sxs-lookup"><span data-stu-id="771de-156">You can modify these cascading style sheet classes, and therefore modify the appearance of the validation errors, by modifying the Site.css file located in the Content folder.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="771de-157">HtmlHelper 类包括只读静态属性，用于检索与验证相关的 CSS 类的名称。</span><span class="sxs-lookup"><span data-stu-id="771de-157">The HtmlHelper class includes read-only static properties for retrieving the names of the validation related CSS classes.</span></span> <span data-ttu-id="771de-158">这些静态属性名为 ValidationInputCssClassName、ValidationFieldCssClassName 和 ValidationSummaryCssClassName。</span><span class="sxs-lookup"><span data-stu-id="771de-158">These static properties are named ValidationInputCssClassName, ValidationFieldCssClassName, and ValidationSummaryCssClassName.</span></span>

## <a name="prebinding-validation-and-postbinding-validation"></a><span data-ttu-id="771de-159">Prebinding 验证和 Postbinding 验证</span><span class="sxs-lookup"><span data-stu-id="771de-159">Prebinding Validation and Postbinding Validation</span></span>

<span data-ttu-id="771de-160">如果您提交用于创建产品的 HTML 表单，并且您为 "价格" 字段输入的值无效，而 "库存" 字段没有值，则您将收到图4中显示的验证消息。</span><span class="sxs-lookup"><span data-stu-id="771de-160">If you submit the HTML form for creating a Product, and you enter an invalid value for the price field and no value for the UnitsInStock field, then you'll get the validation messages displayed in Figure 4.</span></span> <span data-ttu-id="771de-161">这些验证错误消息来自何处？</span><span class="sxs-lookup"><span data-stu-id="771de-161">Where do these validation error messages come from?</span></span>

<span data-ttu-id="771de-162">[!["新建项目" 对话框](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="771de-162">[![The New Project dialog box](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)</span></span>

<span data-ttu-id="771de-163">**图 04**： Prebinding 验证错误（[单击以查看完全大小的图像](performing-simple-validation-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="771de-163">**Figure 04**: Prebinding Validation Errors([Click to view full-size image](performing-simple-validation-cs/_static/image8.png))</span></span>

<span data-ttu-id="771de-164">实际上存在两种类型的验证错误消息：在将 HTML 窗体字段绑定到类之前生成的错误消息，以及在窗体字段绑定到类后生成的错误消息。</span><span class="sxs-lookup"><span data-stu-id="771de-164">There are actually two types of validation error messages - those generated before the HTML form fields are bound to a class and those generated after the form fields are bound to the class.</span></span> <span data-ttu-id="771de-165">换句话说，存在 prebinding 验证错误和 postbinding 验证错误。</span><span class="sxs-lookup"><span data-stu-id="771de-165">In other words, there are prebinding validation errors and postbinding validation errors.</span></span>

<span data-ttu-id="771de-166">列表1中的产品控制器公开的 Create （）操作接受 Product 类的实例。</span><span class="sxs-lookup"><span data-stu-id="771de-166">The Create() action exposed by the Product controller in Listing 1 accepts an instance of the Product class.</span></span> <span data-ttu-id="771de-167">Create 方法的签名如下所示：</span><span class="sxs-lookup"><span data-stu-id="771de-167">The signature of the Create method looks like this:</span></span>

[!code-csharp[Main](performing-simple-validation-cs/samples/sample3.cs)]

<span data-ttu-id="771de-168">Create 窗体中的 HTML 窗体字段的值通过称为模型绑定器的内容绑定到 productToCreate 类。</span><span class="sxs-lookup"><span data-stu-id="771de-168">The values of the HTML form fields from the Create form are bound to the productToCreate class by something called a model binder.</span></span> <span data-ttu-id="771de-169">当不能将窗体字段绑定到窗体属性时，默认模型联编程序会自动将错误消息添加到模型状态。</span><span class="sxs-lookup"><span data-stu-id="771de-169">The default model binder adds an error message to model state automatically when it cannot bind a form field to a form property.</span></span>

<span data-ttu-id="771de-170">默认模型联编程序不能将字符串 "apple" 绑定到 Product 类的 Price 属性。</span><span class="sxs-lookup"><span data-stu-id="771de-170">The default model binder cannot bind the string "apple" to the Price property of the Product class.</span></span> <span data-ttu-id="771de-171">不能将字符串分配给 decimal 属性。</span><span class="sxs-lookup"><span data-stu-id="771de-171">You can't assign a string to a decimal property.</span></span> <span data-ttu-id="771de-172">因此，模型联编程序将错误添加到模型状态。</span><span class="sxs-lookup"><span data-stu-id="771de-172">Therefore, the model binder adds an error to model state.</span></span>

<span data-ttu-id="771de-173">默认模型联编程序也不能将 null 值分配给不接受 null 值的属性。</span><span class="sxs-lookup"><span data-stu-id="771de-173">The default model binder also cannot assign a null value to a property that does not accept nulls.</span></span> <span data-ttu-id="771de-174">具体而言，模型联编程序不能将 null 值分配给 "库存" 属性。</span><span class="sxs-lookup"><span data-stu-id="771de-174">In particular, the model binder cannot assign a null value to the UnitsInStock property.</span></span> <span data-ttu-id="771de-175">同样，模型联编程序会提供并将错误消息添加到模型状态。</span><span class="sxs-lookup"><span data-stu-id="771de-175">Once again, the model binder gives up and adds an error message to model state.</span></span>

<span data-ttu-id="771de-176">如果要自定义这些 prebinding 错误消息的外观，则需要为这些消息创建资源字符串。</span><span class="sxs-lookup"><span data-stu-id="771de-176">If you want to customize the appearance of these prebinding error messages then you need to create resource strings for these messages.</span></span>

## <a name="summary"></a><span data-ttu-id="771de-177">摘要</span><span class="sxs-lookup"><span data-stu-id="771de-177">Summary</span></span>

<span data-ttu-id="771de-178">本教程的目的是介绍 ASP.NET MVC 框架中验证的基本机制。</span><span class="sxs-lookup"><span data-stu-id="771de-178">The goal of this tutorial was to describe the basic mechanics of validation in the ASP.NET MVC framework.</span></span> <span data-ttu-id="771de-179">已学习如何使用模型状态和验证 HTML 帮助器。</span><span class="sxs-lookup"><span data-stu-id="771de-179">You learned how to use model state and the validation HTML helpers.</span></span> <span data-ttu-id="771de-180">还介绍了 prebinding 和 postbinding 验证之间的区别。</span><span class="sxs-lookup"><span data-stu-id="771de-180">We also discussed the distinction between prebinding and postbinding validation.</span></span> <span data-ttu-id="771de-181">在其他教程中，我们将讨论将验证代码移出控制器和模型类的各种策略。</span><span class="sxs-lookup"><span data-stu-id="771de-181">In other tutorials, we'll discuss various strategies for moving your validation code out of your controllers and into your model classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="771de-182">[上一页](displaying-a-table-of-database-data-cs.md)
> [下一页](validating-with-the-idataerrorinfo-interface-cs.md)</span><span class="sxs-lookup"><span data-stu-id="771de-182">[Previous](displaying-a-table-of-database-data-cs.md)
[Next](validating-with-the-idataerrorinfo-interface-cs.md)</span></span>
