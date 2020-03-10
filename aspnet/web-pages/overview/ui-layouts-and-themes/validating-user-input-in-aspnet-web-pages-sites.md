---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: 验证 ASP.NET 网页（Razor）站点中的用户输入 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何验证从用户那里获取的信息 &mdash; 即，确保用户在中的 HTML 窗体中输入有效的信息。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454298"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="df9b2-103">验证 ASP.NET 网页（Razor）站点中的用户输入</span><span class="sxs-lookup"><span data-stu-id="df9b2-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="df9b2-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="df9b2-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="df9b2-105">本文介绍如何验证从用户那里获取的信息 &mdash; 即，确保用户在 ASP.NET 网页（Razor）站点中以 HTML 格式输入有效的信息。</span><span class="sxs-lookup"><span data-stu-id="df9b2-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="df9b2-106">学习内容：</span><span class="sxs-lookup"><span data-stu-id="df9b2-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="df9b2-107">如何检查用户的输入是否与您定义的验证条件匹配。</span><span class="sxs-lookup"><span data-stu-id="df9b2-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="df9b2-108">如何确定是否已通过所有验证测试。</span><span class="sxs-lookup"><span data-stu-id="df9b2-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="df9b2-109">如何显示验证错误（以及如何设置它们的格式）。</span><span class="sxs-lookup"><span data-stu-id="df9b2-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="df9b2-110">如何验证不直接来自用户的数据。</span><span class="sxs-lookup"><span data-stu-id="df9b2-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="df9b2-111">下面是本文中引入的 ASP.NET 编程概念：</span><span class="sxs-lookup"><span data-stu-id="df9b2-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="df9b2-112">`Validation` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="df9b2-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="df9b2-113">`Html.ValidationSummary` 和 `Html.ValidationMessage` 方法。</span><span class="sxs-lookup"><span data-stu-id="df9b2-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="df9b2-114">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="df9b2-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="df9b2-115">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="df9b2-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="df9b2-116">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="df9b2-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="df9b2-117">本文包含以下各节：</span><span class="sxs-lookup"><span data-stu-id="df9b2-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="df9b2-118">用户输入验证概述</span><span class="sxs-lookup"><span data-stu-id="df9b2-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="df9b2-119">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="df9b2-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="df9b2-120">添加客户端验证</span><span class="sxs-lookup"><span data-stu-id="df9b2-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="df9b2-121">格式验证错误</span><span class="sxs-lookup"><span data-stu-id="df9b2-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="df9b2-122">验证不直接来自用户的数据</span><span class="sxs-lookup"><span data-stu-id="df9b2-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="df9b2-123">用户输入验证概述</span><span class="sxs-lookup"><span data-stu-id="df9b2-123">Overview of User Input Validation</span></span>

<span data-ttu-id="df9b2-124">如果要求用户在页面中输入信息（例如，转换为窗体），请务必确保输入的值有效。</span><span class="sxs-lookup"><span data-stu-id="df9b2-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="df9b2-125">例如，您不想处理丢失关键信息的窗体。</span><span class="sxs-lookup"><span data-stu-id="df9b2-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="df9b2-126">用户在 HTML 窗体中输入值时，它们输入的值是字符串。</span><span class="sxs-lookup"><span data-stu-id="df9b2-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="df9b2-127">在许多情况下，所需的值是一些其他数据类型，例如整数或日期。</span><span class="sxs-lookup"><span data-stu-id="df9b2-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="df9b2-128">因此，您还必须确保可以将用户输入的值正确地转换为相应的数据类型。</span><span class="sxs-lookup"><span data-stu-id="df9b2-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="df9b2-129">你可能还会对值有某些限制。</span><span class="sxs-lookup"><span data-stu-id="df9b2-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="df9b2-130">例如，即使用户正确输入整数，你可能也需要确保该值处于某个范围内。</span><span class="sxs-lookup"><span data-stu-id="df9b2-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="df9b2-132">**重要提示**验证用户输入对于安全性也很重要。</span><span class="sxs-lookup"><span data-stu-id="df9b2-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="df9b2-133">当您限制用户可在表单中输入的值时，您可以减少用户输入可能会危及您的网站安全的值的可能性。</span><span class="sxs-lookup"><span data-stu-id="df9b2-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="df9b2-134">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="df9b2-134">Validating User Input</span></span>

<span data-ttu-id="df9b2-135">在 ASP.NET 网页2中，你可以使用 `Validator` 帮助程序来测试用户输入。</span><span class="sxs-lookup"><span data-stu-id="df9b2-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="df9b2-136">基本方法是执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="df9b2-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="df9b2-137">确定要验证的输入元素（字段）。</span><span class="sxs-lookup"><span data-stu-id="df9b2-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="df9b2-138">通常在窗体中 `<input>` 元素中验证值。</span><span class="sxs-lookup"><span data-stu-id="df9b2-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="df9b2-139">不过，最好是验证所有输入，甚至是来自受约束元素（例如 `<select>` 列表）的输入。</span><span class="sxs-lookup"><span data-stu-id="df9b2-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="df9b2-140">这有助于确保用户不会绕过页面上的控件并提交窗体。</span><span class="sxs-lookup"><span data-stu-id="df9b2-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="df9b2-141">在页代码中，使用 `Validation` 帮助器的方法为每个输入元素添加单独的验证检查。</span><span class="sxs-lookup"><span data-stu-id="df9b2-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="df9b2-142">若要检查必填字段，请使用 `Validation.RequireField(field, [error message])` （适用于单个字段）或 `Validation.RequireFields(field1, field2, ...))` （用于字段列表）。</span><span class="sxs-lookup"><span data-stu-id="df9b2-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="df9b2-143">对于其他类型的验证，请使用 `Validation.Add(field, ValidationType)`。</span><span class="sxs-lookup"><span data-stu-id="df9b2-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="df9b2-144">对于 `ValidationType`，可以使用以下选项：</span><span class="sxs-lookup"><span data-stu-id="df9b2-144">For `ValidationType`, you can use these options:</span></span>

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. <span data-ttu-id="df9b2-145">提交页面后，检查验证是否通过检查 `Validation.IsValid`传递：</span><span class="sxs-lookup"><span data-stu-id="df9b2-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="df9b2-146">如果存在任何验证错误，则会跳过正常页面处理。</span><span class="sxs-lookup"><span data-stu-id="df9b2-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="df9b2-147">例如，如果页面的目的是更新数据库，则在解决所有验证错误之前，您不会这样做。</span><span class="sxs-lookup"><span data-stu-id="df9b2-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="df9b2-148">如果存在验证错误，请使用 `Html.ValidationSummary` 或 `Html.ValidationMessage`，或同时使用这两种方法在页的标记中显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="df9b2-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="df9b2-149">下面的示例演示了一个说明这些步骤的页面。</span><span class="sxs-lookup"><span data-stu-id="df9b2-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="df9b2-150">若要查看验证的工作原理，请运行此页，并故意犯错误。</span><span class="sxs-lookup"><span data-stu-id="df9b2-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="df9b2-151">例如，如果您忘记输入课程名称，并且输入的日期无效，则下面是页面的外观：</span><span class="sxs-lookup"><span data-stu-id="df9b2-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![呈现的页中的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="df9b2-153">添加客户端验证</span><span class="sxs-lookup"><span data-stu-id="df9b2-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="df9b2-154">默认情况下，用户输入在用户提交页面后进行验证，即在服务器代码中执行验证。</span><span class="sxs-lookup"><span data-stu-id="df9b2-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="df9b2-155">这种方法的缺点是，用户在提交页面之前并不知道它们已发生错误。</span><span class="sxs-lookup"><span data-stu-id="df9b2-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="df9b2-156">如果窗体较长或复杂，则仅在提交页面后报告错误可能对用户不方便。</span><span class="sxs-lookup"><span data-stu-id="df9b2-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="df9b2-157">你可以添加支持，以在客户端脚本中执行验证。</span><span class="sxs-lookup"><span data-stu-id="df9b2-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="df9b2-158">在这种情况下，将在用户在浏览器中工作时执行验证。</span><span class="sxs-lookup"><span data-stu-id="df9b2-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="df9b2-159">例如，假设您指定一个值应为整数。</span><span class="sxs-lookup"><span data-stu-id="df9b2-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="df9b2-160">如果用户输入的值为非整数值，则只要用户离开输入字段，就会报告该错误。</span><span class="sxs-lookup"><span data-stu-id="df9b2-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="df9b2-161">用户会立即获得反馈，这对他们非常方便。</span><span class="sxs-lookup"><span data-stu-id="df9b2-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="df9b2-162">基于客户端的验证还可以减少用户提交窗体以更正多个错误的次数。</span><span class="sxs-lookup"><span data-stu-id="df9b2-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="df9b2-163">即使使用客户端验证，也始终在服务器代码中执行验证。</span><span class="sxs-lookup"><span data-stu-id="df9b2-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="df9b2-164">在服务器代码中执行验证是一种安全措施，以防用户跳过基于客户端的验证。</span><span class="sxs-lookup"><span data-stu-id="df9b2-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>

1. <span data-ttu-id="df9b2-165">在页面中注册以下 JavaScript 库：</span><span class="sxs-lookup"><span data-stu-id="df9b2-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="df9b2-166">这两个库可从内容交付网络（CDN）中加载，因此你不必将它们安装在计算机或服务器上。</span><span class="sxs-lookup"><span data-stu-id="df9b2-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="df9b2-167">但是，必须具有 jquery 的本地副本。请*验证*</span><span class="sxs-lookup"><span data-stu-id="df9b2-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="df9b2-168">如果尚未使用包含库的 WebMatrix 模板（如**入门网站**），请创建基于**入门网站**的网页站点。</span><span class="sxs-lookup"><span data-stu-id="df9b2-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="df9b2-169">然后将 *.js*文件复制到当前站点。</span><span class="sxs-lookup"><span data-stu-id="df9b2-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="df9b2-170">在标记中，为要验证的每个元素添加对 `Validation.For(field)`的调用。</span><span class="sxs-lookup"><span data-stu-id="df9b2-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="df9b2-171">此方法发出客户端验证使用的属性。</span><span class="sxs-lookup"><span data-stu-id="df9b2-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="df9b2-172">（而不是发出实际的 JavaScript 代码，该方法发出 `data-val-...`之类的属性。</span><span class="sxs-lookup"><span data-stu-id="df9b2-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="df9b2-173">这些属性支持使用 jQuery 执行工作的不引人注目的客户端验证。</span><span class="sxs-lookup"><span data-stu-id="df9b2-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="df9b2-174">以下页面显示了如何将客户端验证功能添加到前面所示的示例中。</span><span class="sxs-lookup"><span data-stu-id="df9b2-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="df9b2-175">并非所有验证检查都在客户端上运行。</span><span class="sxs-lookup"><span data-stu-id="df9b2-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="df9b2-176">特别是，数据类型验证（整数、日期等）不会在客户端上运行。</span><span class="sxs-lookup"><span data-stu-id="df9b2-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="df9b2-177">以下检查适用于客户端和服务器：</span><span class="sxs-lookup"><span data-stu-id="df9b2-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="df9b2-178">在此示例中，有效日期的测试在客户端代码中不起作用。</span><span class="sxs-lookup"><span data-stu-id="df9b2-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="df9b2-179">但是，将在服务器代码中执行测试。</span><span class="sxs-lookup"><span data-stu-id="df9b2-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="df9b2-180">格式验证错误</span><span class="sxs-lookup"><span data-stu-id="df9b2-180">Formatting Validation Errors</span></span>

<span data-ttu-id="df9b2-181">您可以通过定义具有以下保留名称的 CSS 类来控制验证错误的显示方式：</span><span class="sxs-lookup"><span data-stu-id="df9b2-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="df9b2-182">`field-validation-error`。</span><span class="sxs-lookup"><span data-stu-id="df9b2-182">`field-validation-error`.</span></span> <span data-ttu-id="df9b2-183">定义在显示错误时 `Html.ValidationMessage` 方法的输出。</span><span class="sxs-lookup"><span data-stu-id="df9b2-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="df9b2-184">`field-validation-valid`。</span><span class="sxs-lookup"><span data-stu-id="df9b2-184">`field-validation-valid`.</span></span> <span data-ttu-id="df9b2-185">如果没有错误，则定义 `Html.ValidationMessage` 方法的输出。</span><span class="sxs-lookup"><span data-stu-id="df9b2-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="df9b2-186">`input-validation-error`。</span><span class="sxs-lookup"><span data-stu-id="df9b2-186">`input-validation-error`.</span></span> <span data-ttu-id="df9b2-187">定义在出现错误时如何呈现 `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="df9b2-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="df9b2-188">（例如，如果其值无效，则可以使用此类将 &lt;input&gt; 元素的背景色设置为不同的颜色。此 CSS 类仅在客户端验证期间使用（在 ASP.NET 网页2）。</span><span class="sxs-lookup"><span data-stu-id="df9b2-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="df9b2-189">`input-validation-valid`。</span><span class="sxs-lookup"><span data-stu-id="df9b2-189">`input-validation-valid`.</span></span> <span data-ttu-id="df9b2-190">定义在没有错误时 `<input>` 元素的外观。</span><span class="sxs-lookup"><span data-stu-id="df9b2-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="df9b2-191">`validation-summary-errors`。</span><span class="sxs-lookup"><span data-stu-id="df9b2-191">`validation-summary-errors`.</span></span> <span data-ttu-id="df9b2-192">定义 `Html.ValidationSummary` 方法的输出，它会显示错误列表。</span><span class="sxs-lookup"><span data-stu-id="df9b2-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="df9b2-193">`validation-summary-valid`。</span><span class="sxs-lookup"><span data-stu-id="df9b2-193">`validation-summary-valid`.</span></span> <span data-ttu-id="df9b2-194">如果没有错误，则定义 `Html.ValidationSummary` 方法的输出。</span><span class="sxs-lookup"><span data-stu-id="df9b2-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="df9b2-195">以下 `<style>` 块显示了错误情况的规则。</span><span class="sxs-lookup"><span data-stu-id="df9b2-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="df9b2-196">如果在本文前面的示例页中包括此样式块，则错误显示将如下图所示：</span><span class="sxs-lookup"><span data-stu-id="df9b2-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="df9b2-198">如果在 ASP.NET 网页2中未使用客户端验证，则 `<input>` 元素（`input-validation-error` 和 `input-validation-valid` 的 CSS 类将不会产生任何影响。</span><span class="sxs-lookup"><span data-stu-id="df9b2-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>

### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="df9b2-199">静态和动态错误显示</span><span class="sxs-lookup"><span data-stu-id="df9b2-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="df9b2-200">CSS 规则成对出现，如 `validation-summary-errors` 和 `validation-summary-valid`。</span><span class="sxs-lookup"><span data-stu-id="df9b2-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="df9b2-201">它们允许您为这两个条件定义规则：错误条件和 "正常" （非错误）条件。</span><span class="sxs-lookup"><span data-stu-id="df9b2-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="df9b2-202">必须了解的是，即使没有错误，也会始终呈现错误显示的标记。</span><span class="sxs-lookup"><span data-stu-id="df9b2-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="df9b2-203">例如，如果某页在标记中有 `Html.ValidationSummary` 方法，则即使第一次请求该页时，页源也将包含以下标记：</span><span class="sxs-lookup"><span data-stu-id="df9b2-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="df9b2-204">换句话说，`Html.ValidationSummary` 方法始终呈现 `<div>` 元素和列表，即使错误列表为空也是如此。</span><span class="sxs-lookup"><span data-stu-id="df9b2-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="df9b2-205">同样，`Html.ValidationMessage` 方法始终将 `<span>` 元素呈现为单个字段错误的占位符，即使没有错误也是如此。</span><span class="sxs-lookup"><span data-stu-id="df9b2-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="df9b2-206">在某些情况下，显示错误消息会导致页面重排，并会导致页面上的元素移动。</span><span class="sxs-lookup"><span data-stu-id="df9b2-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="df9b2-207">以 `-valid` 结尾的 CSS 规则使你能够定义可帮助防止此问题的布局。</span><span class="sxs-lookup"><span data-stu-id="df9b2-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="df9b2-208">例如，可以将 `field-validation-error` 和 `field-validation-valid` 定义为具有相同的固定大小。</span><span class="sxs-lookup"><span data-stu-id="df9b2-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="df9b2-209">这样一来，字段的显示区域是静态的，如果显示错误消息，则不会更改页面流。</span><span class="sxs-lookup"><span data-stu-id="df9b2-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="df9b2-210">验证不直接来自用户的数据</span><span class="sxs-lookup"><span data-stu-id="df9b2-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="df9b2-211">有时，您必须验证不直接来自 HTML 格式的信息。</span><span class="sxs-lookup"><span data-stu-id="df9b2-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="df9b2-212">典型的示例是在查询字符串中传递值的页，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="df9b2-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="df9b2-213">在这种情况下，您需要确保传递到页面的值（此处为1022，`classid`的值）有效。</span><span class="sxs-lookup"><span data-stu-id="df9b2-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="df9b2-214">不能直接使用 `Validation` 帮助器来执行此验证。</span><span class="sxs-lookup"><span data-stu-id="df9b2-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="df9b2-215">但是，您可以使用验证系统的其他功能，例如显示验证错误消息的功能。</span><span class="sxs-lookup"><span data-stu-id="df9b2-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="df9b2-216">**重要提示**始终验证从*任何*源获取的值，包括窗体字段值、查询字符串值和 cookie 值。</span><span class="sxs-lookup"><span data-stu-id="df9b2-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="df9b2-217">用户可以轻松地更改这些值（可能出于恶意目的）。</span><span class="sxs-lookup"><span data-stu-id="df9b2-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="df9b2-218">因此，你必须检查这些值才能保护你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="df9b2-218">So you must check these values in order to protect your application.</span></span>

<span data-ttu-id="df9b2-219">下面的示例演示如何验证在查询字符串中传递的值。</span><span class="sxs-lookup"><span data-stu-id="df9b2-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="df9b2-220">此代码测试该值是否不为空，以及该值是否为整数。</span><span class="sxs-lookup"><span data-stu-id="df9b2-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="df9b2-221">请注意，当请求不是窗体提交（`if(!IsPost)`）时，将执行该测试。</span><span class="sxs-lookup"><span data-stu-id="df9b2-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="df9b2-222">此测试将在第一次请求页面时通过，但不会在请求提交表单时通过。</span><span class="sxs-lookup"><span data-stu-id="df9b2-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="df9b2-223">若要显示此错误，可以通过调用 `Validation.AddFormError("message")`将错误添加到验证错误的列表中。</span><span class="sxs-lookup"><span data-stu-id="df9b2-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="df9b2-224">如果页面包含对 `Html.ValidationSummary` 方法的调用，则会在该处显示错误，就像用户输入验证错误一样。</span><span class="sxs-lookup"><span data-stu-id="df9b2-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="df9b2-225">其他资源</span><span class="sxs-lookup"><span data-stu-id="df9b2-225">Additional Resources</span></span>

[<span data-ttu-id="df9b2-226">在 ASP.NET 网页网站中使用 HTML 表单</span><span class="sxs-lookup"><span data-stu-id="df9b2-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)
