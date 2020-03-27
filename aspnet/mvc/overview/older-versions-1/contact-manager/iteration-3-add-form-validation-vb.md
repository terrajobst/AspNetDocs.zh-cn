---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: '迭代 #3 –添加窗体验证（VB） |Microsoft Docs'
author: microsoft
description: 在第三次迭代中，我们将添加基本的窗体验证。 我们阻止用户提交窗体，而无需填写所需的窗体字段。 我们还验证 emai 。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 73b307f53875abe84b592c75b1ff614ffd9d8b82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437966"
---
# <a name="iteration-3--add-form-validation-vb"></a><span data-ttu-id="79d80-105">迭代 #3 –添加窗体验证（VB）</span><span class="sxs-lookup"><span data-stu-id="79d80-105">Iteration #3 – Add form validation (VB)</span></span>

<span data-ttu-id="79d80-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="79d80-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="79d80-107">下载代码</span><span class="sxs-lookup"><span data-stu-id="79d80-107">Download Code</span></span>](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> <span data-ttu-id="79d80-108">在第三次迭代中，我们将添加基本的窗体验证。</span><span class="sxs-lookup"><span data-stu-id="79d80-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="79d80-109">我们阻止用户提交窗体，而无需填写所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="79d80-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="79d80-110">我们还验证了电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="79d80-110">We also validate email addresses and phone numbers.</span></span>

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="79d80-111">构建联系人管理 ASP.NET MVC 应用程序（VB）</span><span class="sxs-lookup"><span data-stu-id="79d80-111">Building a Contact Management ASP.NET MVC Application (VB)</span></span>

<span data-ttu-id="79d80-112">在本系列教程中，我们从一开始就生成一个完整的联系人管理应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d80-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="79d80-113">联系人管理器应用程序允许您存储联系人信息名称、电话号码和电子邮件地址，以获取人员列表。</span><span class="sxs-lookup"><span data-stu-id="79d80-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="79d80-114">我们通过多个迭代生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d80-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="79d80-115">随着每次迭代，我们将逐步改进应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d80-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="79d80-116">此多个迭代方法的目标是使您能够了解每个更改的原因。</span><span class="sxs-lookup"><span data-stu-id="79d80-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="79d80-117">迭代 #1-创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d80-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="79d80-118">在第一次迭代中，我们以尽可能简单的方式创建联系人管理器。</span><span class="sxs-lookup"><span data-stu-id="79d80-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="79d80-119">添加对基本数据库操作的支持：创建、读取、更新和删除（CRUD）。</span><span class="sxs-lookup"><span data-stu-id="79d80-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="79d80-120">迭代 #2-使应用程序看起来不错。</span><span class="sxs-lookup"><span data-stu-id="79d80-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="79d80-121">在此迭代中，我们通过修改默认的 ASP.NET MVC 视图母版页和级联样式表来改善应用程序的外观。</span><span class="sxs-lookup"><span data-stu-id="79d80-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="79d80-122">迭代 #3-添加窗体验证。</span><span class="sxs-lookup"><span data-stu-id="79d80-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="79d80-123">在第三次迭代中，我们将添加基本的窗体验证。</span><span class="sxs-lookup"><span data-stu-id="79d80-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="79d80-124">我们阻止用户提交窗体，而无需填写所需的窗体字段。</span><span class="sxs-lookup"><span data-stu-id="79d80-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="79d80-125">我们还验证了电子邮件地址和电话号码。</span><span class="sxs-lookup"><span data-stu-id="79d80-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="79d80-126">迭代 #4-使应用程序松散耦合。</span><span class="sxs-lookup"><span data-stu-id="79d80-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="79d80-127">在第四次迭代中，我们将利用多种软件设计模式来更轻松地维护和修改联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d80-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="79d80-128">例如，我们重构应用程序以使用存储库模式和依赖关系注入模式。</span><span class="sxs-lookup"><span data-stu-id="79d80-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="79d80-129">迭代 #5-创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="79d80-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="79d80-130">在第五次迭代中，通过添加单元测试使应用程序更易于维护和修改。</span><span class="sxs-lookup"><span data-stu-id="79d80-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="79d80-131">我们模拟数据模型类，并为控制器和验证逻辑生成单元测试。</span><span class="sxs-lookup"><span data-stu-id="79d80-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="79d80-132">迭代 #6-使用测试驱动开发。</span><span class="sxs-lookup"><span data-stu-id="79d80-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="79d80-133">在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。</span><span class="sxs-lookup"><span data-stu-id="79d80-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="79d80-134">在此迭代中，我们添加联系人组。</span><span class="sxs-lookup"><span data-stu-id="79d80-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="79d80-135">迭代 #7-添加 Ajax 功能。</span><span class="sxs-lookup"><span data-stu-id="79d80-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="79d80-136">在第七次迭代中，我们通过添加对 Ajax 的支持来提高应用程序的响应能力和性能。</span><span class="sxs-lookup"><span data-stu-id="79d80-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>

## <a name="this-iteration"></a><span data-ttu-id="79d80-137">此迭代</span><span class="sxs-lookup"><span data-stu-id="79d80-137">This Iteration</span></span>

<span data-ttu-id="79d80-138">在联系人管理器应用程序的第二次迭代中，我们添加了基本的窗体验证。</span><span class="sxs-lookup"><span data-stu-id="79d80-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="79d80-139">我们会在不输入所需表单域的值的情况下，阻止用户提交联系人。</span><span class="sxs-lookup"><span data-stu-id="79d80-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="79d80-140">我们还验证电话号码和电子邮件地址（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="79d80-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>

<span data-ttu-id="79d80-141">[!["新建项目" 对话框](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="79d80-141">[![The New Project dialog box](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="79d80-142">**图 01**：具有验证的窗体（[单击以查看完全大小的图像](iteration-3-add-form-validation-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="79d80-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-vb/_static/image2.png))</span></span>

<span data-ttu-id="79d80-143">在此迭代中，我们会将验证逻辑直接添加到控制器操作。</span><span class="sxs-lookup"><span data-stu-id="79d80-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="79d80-144">通常，不建议将验证添加到 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d80-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="79d80-145">更好的方法是将应用程序的验证逻辑放在单独的[服务层](http://martinfowler.com/eaaCatalog/serviceLayer.html)中。</span><span class="sxs-lookup"><span data-stu-id="79d80-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="79d80-146">在下一次迭代中，我们重构联系人管理器应用程序，使应用程序更易于维护。</span><span class="sxs-lookup"><span data-stu-id="79d80-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="79d80-147">在这种情况下，为了简单起见，我们将手动编写所有验证代码。</span><span class="sxs-lookup"><span data-stu-id="79d80-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="79d80-148">我们可以利用验证框架，而不是自己编写验证代码。</span><span class="sxs-lookup"><span data-stu-id="79d80-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="79d80-149">例如，你可以使用 Microsoft 企业库验证应用程序块（VAB）来实现 ASP.NET MVC 应用程序的验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="79d80-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="79d80-150">若要了解有关验证应用程序块的详细信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="79d80-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="79d80-151">将验证添加到创建视图</span><span class="sxs-lookup"><span data-stu-id="79d80-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="79d80-152">首先，让我们将验证逻辑添加到创建视图。</span><span class="sxs-lookup"><span data-stu-id="79d80-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="79d80-153">幸运的是，因为我们生成了带有 Visual Studio 的 "创建" 视图，所以 "创建" 视图已包含所有必要的用户界面逻辑来显示验证消息。</span><span class="sxs-lookup"><span data-stu-id="79d80-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="79d80-154">"创建" 视图包含在 "列表 1" 中。</span><span class="sxs-lookup"><span data-stu-id="79d80-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="79d80-155">**列表 1-\Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="79d80-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

<span data-ttu-id="79d80-156">字段验证-error 类用于为 ValidationMessage （） helper 呈现的输出绘制样式。</span><span class="sxs-lookup"><span data-stu-id="79d80-156">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="79d80-157">输入验证-错误类用于对由 Html. TextBox （） helper 呈现的文本框（输入）进行样式。</span><span class="sxs-lookup"><span data-stu-id="79d80-157">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="79d80-158">验证摘要-错误类用于对 ValidationSummary （）帮助程序呈现的无序列表进行样式。</span><span class="sxs-lookup"><span data-stu-id="79d80-158">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="79d80-159">您可以修改本部分中所述的样式表类，以自定义验证错误消息的外观。</span><span class="sxs-lookup"><span data-stu-id="79d80-159">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>

## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="79d80-160">将验证逻辑添加到创建操作</span><span class="sxs-lookup"><span data-stu-id="79d80-160">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="79d80-161">现在，Create view 从不显示验证错误消息，因为我们尚未编写用于生成任何消息的逻辑。</span><span class="sxs-lookup"><span data-stu-id="79d80-161">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="79d80-162">为了显示验证错误消息，需要将错误消息添加到 ModelState。</span><span class="sxs-lookup"><span data-stu-id="79d80-162">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="79d80-163">将窗体字段的值分配给属性错误时，UpdateModel （）方法会自动将错误消息添加到 ModelState 中。</span><span class="sxs-lookup"><span data-stu-id="79d80-163">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="79d80-164">例如，如果您尝试将字符串 "apple" 分配给接受日期时间值的出生日期属性，则 UpdateModel （）方法会将错误添加到 ModelState 中。</span><span class="sxs-lookup"><span data-stu-id="79d80-164">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>

<span data-ttu-id="79d80-165">清单2中修改的 Create （）方法包含一个新部分，该部分将在新联系人插入数据库之前验证 Contact 类的属性。</span><span class="sxs-lookup"><span data-stu-id="79d80-165">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="79d80-166">**列表 2-Controllers\ContactController.vb （通过验证创建）**</span><span class="sxs-lookup"><span data-stu-id="79d80-166">**Listing 2 - Controllers\ContactController.vb (Create with validation)**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

<span data-ttu-id="79d80-167">"验证" 部分强制实施四个不同的验证规则：</span><span class="sxs-lookup"><span data-stu-id="79d80-167">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="79d80-168">FirstName 属性的长度必须大于零（并且不能仅包含空格）</span><span class="sxs-lookup"><span data-stu-id="79d80-168">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="79d80-169">LastName 属性的长度必须大于零（并且不能仅包含空格）</span><span class="sxs-lookup"><span data-stu-id="79d80-169">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="79d80-170">如果电话属性具有值（长度大于0），则电话属性必须与正则表达式匹配。</span><span class="sxs-lookup"><span data-stu-id="79d80-170">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="79d80-171">如果电子邮件属性的值（长度大于0），则 Email 属性必须与正则表达式匹配。</span><span class="sxs-lookup"><span data-stu-id="79d80-171">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="79d80-172">如果违反了验证规则，则会将错误消息添加到 ModelState 中的 AddModelError （）方法的帮助下。</span><span class="sxs-lookup"><span data-stu-id="79d80-172">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="79d80-173">将消息添加到 ModelState 时，请提供属性的名称和验证错误消息的文本。</span><span class="sxs-lookup"><span data-stu-id="79d80-173">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="79d80-174">此错误消息将通过 ValidationSummary （）和 ValidationMessage （）帮助程序方法显示在视图中。</span><span class="sxs-lookup"><span data-stu-id="79d80-174">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="79d80-175">执行验证规则后，将检查 ModelState 的 IsValid 属性。</span><span class="sxs-lookup"><span data-stu-id="79d80-175">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="79d80-176">当任何验证错误消息已添加到 ModelState 时，IsValid 属性返回 false。</span><span class="sxs-lookup"><span data-stu-id="79d80-176">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="79d80-177">如果验证失败，则会重新显示带有错误消息的 Create 窗体。</span><span class="sxs-lookup"><span data-stu-id="79d80-177">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="79d80-178">我获取了用于在 [ *http://regexlib.com* ](http://regexlib.com) 中验证正则表达式存储库中的电话号码和电子邮件地址的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="79d80-178">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>

## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="79d80-179">向编辑操作添加验证逻辑</span><span class="sxs-lookup"><span data-stu-id="79d80-179">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="79d80-180">Edit （）操作更新联系人。</span><span class="sxs-lookup"><span data-stu-id="79d80-180">The Edit() action updates a Contact.</span></span> <span data-ttu-id="79d80-181">Edit （）操作需要执行与 Create （）操作完全相同的验证。</span><span class="sxs-lookup"><span data-stu-id="79d80-181">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="79d80-182">我们应重构 Contact controller，使 Create （）和 Edit （）操作都调用同一验证方法，而不是复制相同的验证代码。</span><span class="sxs-lookup"><span data-stu-id="79d80-182">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="79d80-183">修改后的 Contact controller 类包含在列表3中。</span><span class="sxs-lookup"><span data-stu-id="79d80-183">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="79d80-184">此类有一个新的 ValidateContact （）方法，该方法在 Create （）和 Edit （）操作中调用。</span><span class="sxs-lookup"><span data-stu-id="79d80-184">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="79d80-185">**Listing 3 - Controllers\ContactController.vb**</span><span class="sxs-lookup"><span data-stu-id="79d80-185">**Listing 3 - Controllers\ContactController.vb**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a><span data-ttu-id="79d80-186">Summary</span><span class="sxs-lookup"><span data-stu-id="79d80-186">Summary</span></span>

<span data-ttu-id="79d80-187">在此迭代中，我们向联系人管理器应用程序添加了基本的窗体验证。</span><span class="sxs-lookup"><span data-stu-id="79d80-187">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="79d80-188">我们的验证逻辑阻止用户提交新的联系人或编辑现有联系人，而不提供 FirstName 和 LastName 属性的值。</span><span class="sxs-lookup"><span data-stu-id="79d80-188">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="79d80-189">此外，用户必须提供有效的电话号码和电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="79d80-189">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="79d80-190">在此迭代中，我们以尽可能最简单的方式将验证逻辑添加到了联系人管理器应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d80-190">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="79d80-191">但是，将我们的验证逻辑混合到我们的控制器逻辑将会在长期中产生问题。</span><span class="sxs-lookup"><span data-stu-id="79d80-191">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="79d80-192">随着时间的推移，我们的应用程序将更难以维护和修改。</span><span class="sxs-lookup"><span data-stu-id="79d80-192">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="79d80-193">在下一次迭代中，我们将从控制器重构验证逻辑和数据库访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="79d80-193">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="79d80-194">我们将利用几项软件设计原则，使我们能够创建更松耦合、更易于维护的应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d80-194">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="79d80-195">[上一页](iteration-2-make-the-application-look-nice-vb.md)
> [下一页](iteration-4-make-the-application-loosely-coupled-vb.md)</span><span class="sxs-lookup"><span data-stu-id="79d80-195">[Previous](iteration-2-make-the-application-look-nice-vb.md)
[Next](iteration-4-make-the-application-loosely-coupled-vb.md)</span></span>
