---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: 在 ASP.NET 网页（Razor）站点中使用 HTML 窗体 |Microsoft Docs
author: Rick-Anderson
description: 窗体是 HTML 文档的一个部分，您可以在其中放置用户输入控件（如文本框、复选框、单选按钮和下拉列表）。 使用 forms 符合 。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519602"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="dedd9-104">在 ASP.NET 网页（Razor）站点中使用 HTML 表单</span><span class="sxs-lookup"><span data-stu-id="dedd9-104">Working with HTML Forms in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="dedd9-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="dedd9-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="dedd9-106">本文介绍当你在 ASP.NET 网页（Razor）网站中工作时如何处理 HTML 窗体（带有文本框和按钮）。</span><span class="sxs-lookup"><span data-stu-id="dedd9-106">This article describes how to process an HTML form (with text boxes and buttons) when you are working in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="dedd9-107">**你将学习的内容：**</span><span class="sxs-lookup"><span data-stu-id="dedd9-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="dedd9-108">如何创建 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="dedd9-108">How to create an HTML form.</span></span>
> - <span data-ttu-id="dedd9-109">如何读取窗体中的用户输入。</span><span class="sxs-lookup"><span data-stu-id="dedd9-109">How to read user input from the form.</span></span>
> - <span data-ttu-id="dedd9-110">如何验证用户输入。</span><span class="sxs-lookup"><span data-stu-id="dedd9-110">How to validate user input.</span></span>
> - <span data-ttu-id="dedd9-111">如何在提交页面后还原表单值。</span><span class="sxs-lookup"><span data-stu-id="dedd9-111">How to restore form values after the page is submitted.</span></span>
> 
> <span data-ttu-id="dedd9-112">下面是本文中引入的 ASP.NET 编程概念：</span><span class="sxs-lookup"><span data-stu-id="dedd9-112">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="dedd9-113">`Request` 对象。</span><span class="sxs-lookup"><span data-stu-id="dedd9-113">The `Request` object.</span></span>
> - <span data-ttu-id="dedd9-114">输入验证。</span><span class="sxs-lookup"><span data-stu-id="dedd9-114">Input validation.</span></span>
> - <span data-ttu-id="dedd9-115">HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="dedd9-115">HTML encoding.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="dedd9-116">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="dedd9-116">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="dedd9-117">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="dedd9-117">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="dedd9-118">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="dedd9-118">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="creating-a-simple-html-form"></a><span data-ttu-id="dedd9-119">创建简单的 HTML 窗体</span><span class="sxs-lookup"><span data-stu-id="dedd9-119">Creating a Simple HTML Form</span></span>

1. <span data-ttu-id="dedd9-120">创建新网站。</span><span class="sxs-lookup"><span data-stu-id="dedd9-120">Create a new website.</span></span>
2. <span data-ttu-id="dedd9-121">在根文件夹中，创建一个名为 "*窗体*" 的网页，然后输入以下标记：</span><span class="sxs-lookup"><span data-stu-id="dedd9-121">In the root folder, create a web page named *Form.cshtml* and enter the following markup:</span></span>

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. <span data-ttu-id="dedd9-122">在浏览器中启动页面。</span><span class="sxs-lookup"><span data-stu-id="dedd9-122">Launch the page in your browser.</span></span> <span data-ttu-id="dedd9-123">（在 WebMatrix 中，在 "**文件**" 工作区中，右键单击该文件，然后选择 "**在浏览器中启动**"。）将显示一个简单的窗体，其中包含三个输入字段和一个**提交**按钮。</span><span class="sxs-lookup"><span data-stu-id="dedd9-123">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.) A simple form with three input fields and a **Submit** button is displayed.</span></span>

    ![带有三个文本框的窗体的屏幕截图。](4-working-with-forms/_static/image1.png)

    <span data-ttu-id="dedd9-125">此时，如果单击 "**提交**" 按钮，则不会执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="dedd9-125">At this point, if you click the **Submit** button, nothing happens.</span></span> <span data-ttu-id="dedd9-126">若要使窗体有用，必须添加一些将在服务器上运行的代码。</span><span class="sxs-lookup"><span data-stu-id="dedd9-126">To make the form useful, you have to add some code that will run on the server.</span></span>

## <a name="reading-user-input-from-the-form"></a><span data-ttu-id="dedd9-127">从窗体读取用户输入</span><span class="sxs-lookup"><span data-stu-id="dedd9-127">Reading User Input from the Form</span></span>

<span data-ttu-id="dedd9-128">若要处理窗体，请添加代码，用于读取已提交的字段值并对其执行操作。</span><span class="sxs-lookup"><span data-stu-id="dedd9-128">To process the form, you add code that reads the submitted field values and does something with them.</span></span> <span data-ttu-id="dedd9-129">此过程说明如何读取字段并在页面上显示用户输入。</span><span class="sxs-lookup"><span data-stu-id="dedd9-129">This procedure shows you how to read the fields and display the user input on the page.</span></span> <span data-ttu-id="dedd9-130">（在生产应用程序中，你通常会对用户输入执行更有趣的操作。</span><span class="sxs-lookup"><span data-stu-id="dedd9-130">(In a production application, you generally do more interesting things with user input.</span></span> <span data-ttu-id="dedd9-131">你将在有关使用数据库的文章中完成此操作。）</span><span class="sxs-lookup"><span data-stu-id="dedd9-131">You'll do that in the article about working with databases.)</span></span>

1. <span data-ttu-id="dedd9-132">在 "# *.* #" 文件的顶部，输入以下代码：</span><span class="sxs-lookup"><span data-stu-id="dedd9-132">At the top of the *Form.cshtml* file, enter the following code:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    <span data-ttu-id="dedd9-133">当用户首次请求页面时，只显示空窗体。</span><span class="sxs-lookup"><span data-stu-id="dedd9-133">When the user first requests the page, only the empty form is displayed.</span></span> <span data-ttu-id="dedd9-134">用户（将是你）将填写表单，然后单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="dedd9-134">The user (which will be you) fills in the form and then clicks **Submit**.</span></span> <span data-ttu-id="dedd9-135">这会将用户输入提交（发布）到服务器。</span><span class="sxs-lookup"><span data-stu-id="dedd9-135">This submits (posts) the user input to the server.</span></span> <span data-ttu-id="dedd9-136">默认情况下，该请求将进入同一页（即，*窗体.* #）。</span><span class="sxs-lookup"><span data-stu-id="dedd9-136">By default, the request goes to the same page (namely, *Form.cshtml*).</span></span>

    <span data-ttu-id="dedd9-137">此时，在您提交该页时，您输入的值将显示在窗体的上方：</span><span class="sxs-lookup"><span data-stu-id="dedd9-137">When you submit the page this time, the values you entered are displayed just above the form:</span></span>

    ![屏幕截图，显示你在页面上显示的输入值。](4-working-with-forms/_static/image2.png)

    <span data-ttu-id="dedd9-139">查看页面的代码。</span><span class="sxs-lookup"><span data-stu-id="dedd9-139">Look at the code for the page.</span></span> <span data-ttu-id="dedd9-140">首先使用 `IsPost` 方法来确定页面是否正在发布&#8212; ，即用户是否单击 "**提交**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="dedd9-140">You first use the `IsPost` method to determine whether the page is being posted &#8212; that is, whether a user clicked the **Submit** button.</span></span> <span data-ttu-id="dedd9-141">如果这是 post，`IsPost` 返回 true。</span><span class="sxs-lookup"><span data-stu-id="dedd9-141">If this is a post, `IsPost` returns true.</span></span> <span data-ttu-id="dedd9-142">这是 ASP.NET 网页确定使用的是初始请求（GET 请求）还是回发（POST 请求）的标准方法。</span><span class="sxs-lookup"><span data-stu-id="dedd9-142">This is the standard way in ASP.NET Web Pages to determine whether you're working with an initial request (a GET request) or a postback (a POST request).</span></span> <span data-ttu-id="dedd9-143">（有关 GET 和 POST 的详细信息，请参阅[使用 Razor 语法 ASP.NET 网页编程简介](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)中的边栏 "HTTP GET 和 Post 和 IsPost 属性"。）</span><span class="sxs-lookup"><span data-stu-id="dedd9-143">(For more information about GET and POST, see the sidebar "HTTP GET and POST and the IsPost Property" in [Introduction to ASP.NET Web Pages Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)</span></span>

    <span data-ttu-id="dedd9-144">接下来，从 `Request.Form` 对象获取用户填写的值，并将其放在变量中供以后查看。</span><span class="sxs-lookup"><span data-stu-id="dedd9-144">Next, you get the values that the user filled in from the `Request.Form` object, and you put them in variables for later.</span></span> <span data-ttu-id="dedd9-145">`Request.Form` 对象包含通过页提交的所有值，每个值都由一个键标识。</span><span class="sxs-lookup"><span data-stu-id="dedd9-145">The `Request.Form` object contains all the values that were submitted with the page, each identified by a key.</span></span> <span data-ttu-id="dedd9-146">该键等效于要读取的窗体字段的 `name` 属性。</span><span class="sxs-lookup"><span data-stu-id="dedd9-146">The key is the equivalent to the `name` attribute of the form field that you want to read.</span></span> <span data-ttu-id="dedd9-147">例如，若要读取 `companyname` 字段（文本框），请使用 `Request.Form["companyname"]`。</span><span class="sxs-lookup"><span data-stu-id="dedd9-147">For example, to read the `companyname` field (text box), you use `Request.Form["companyname"]`.</span></span>

    <span data-ttu-id="dedd9-148">表单值作为字符串存储在 `Request.Form` 对象中。</span><span class="sxs-lookup"><span data-stu-id="dedd9-148">Form values are stored in the `Request.Form` object as strings.</span></span> <span data-ttu-id="dedd9-149">因此，当您必须使用值作为数字、日期或其他类型的值时，必须将其从字符串转换为该类型。</span><span class="sxs-lookup"><span data-stu-id="dedd9-149">Therefore, when you have to work with a value as a number or a date or some other type, you have to convert it from a string to that type.</span></span> <span data-ttu-id="dedd9-150">在此示例中，`Request.Form` 的 `AsInt` 方法用于将 employees 字段（包含雇员计数）的值转换为整数。</span><span class="sxs-lookup"><span data-stu-id="dedd9-150">In the example, the `AsInt` method of the `Request.Form` is used to convert the value of the employees field (which contains an employee count) to an integer.</span></span>
2. <span data-ttu-id="dedd9-151">在浏览器中启动页面，填写表单域，并单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="dedd9-151">Launch the page in your browser, fill in the form fields, and click **Submit**.</span></span> <span data-ttu-id="dedd9-152">页面将显示您输入的值。</span><span class="sxs-lookup"><span data-stu-id="dedd9-152">The page displays the values you entered.</span></span>

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a><span data-ttu-id="dedd9-153">外观和安全性的 HTML 编码</span><span class="sxs-lookup"><span data-stu-id="dedd9-153">HTML Encoding for Appearance and Security</span></span>
> 
> <span data-ttu-id="dedd9-154">HTML 对 `<`、`>`和 `&`等字符具有特殊用途。</span><span class="sxs-lookup"><span data-stu-id="dedd9-154">HTML has special uses for characters like `<`, `>`, and `&`.</span></span> <span data-ttu-id="dedd9-155">如果这些特殊字符出现在不预期的位置，则它们可能会破坏网页的外观和功能。</span><span class="sxs-lookup"><span data-stu-id="dedd9-155">If these special characters appear where they're not expected, they can ruin the appearance and functionality of your web page.</span></span> <span data-ttu-id="dedd9-156">例如，浏览器将 `<` 字符（除非后跟空格）解释为 HTML 元素的开头，如 `<b>` 或 `<input ...>`。</span><span class="sxs-lookup"><span data-stu-id="dedd9-156">For example, the browser interprets the `<` character (unless it's followed by a space) as the beginning of an HTML element, like `<b>` or `<input ...>`.</span></span> <span data-ttu-id="dedd9-157">如果浏览器不能识别元素，则只会丢弃以 `<` 开头的字符串，直到到达它再次识别的内容。</span><span class="sxs-lookup"><span data-stu-id="dedd9-157">If the browser doesn't recognize the element, it simply discards the string that begins with `<` until it reaches something that it again recognizes.</span></span> <span data-ttu-id="dedd9-158">很明显，这可能会导致页面中出现某种奇怪的渲染。</span><span class="sxs-lookup"><span data-stu-id="dedd9-158">Obviously, this can result in some weird rendering in the page.</span></span>
> 
> <span data-ttu-id="dedd9-159">HTML 编码将这些保留字符替换为浏览器解释为正确符号的代码。</span><span class="sxs-lookup"><span data-stu-id="dedd9-159">HTML encoding replaces these reserved characters with a code that browsers interpret as the correct symbol.</span></span> <span data-ttu-id="dedd9-160">例如，`<` 字符将替换为 `&lt;`，`>` 字符将替换为 `&gt;`。</span><span class="sxs-lookup"><span data-stu-id="dedd9-160">For example, the `<` character is replaced with `&lt;` and the `>` character is replaced with `&gt;`.</span></span> <span data-ttu-id="dedd9-161">浏览器将这些替换字符串呈现为你要查看的字符。</span><span class="sxs-lookup"><span data-stu-id="dedd9-161">The browser renders these replacement strings as the characters that you want to see.</span></span>
> 
> <span data-ttu-id="dedd9-162">在显示从用户那里获得的字符串（输入）时，最好使用 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="dedd9-162">It's a good idea to use HTML encoding any time you display strings (input) that you got from a user.</span></span> <span data-ttu-id="dedd9-163">如果不这样做，用户可以尝试让您的网页运行恶意脚本，或执行其他影响您的站点安全的操作，或者不是您所期望的内容。</span><span class="sxs-lookup"><span data-stu-id="dedd9-163">If you don't, a user can try to get your web page to run a malicious script or do something else that compromises your site security or that's just not what you intend.</span></span> <span data-ttu-id="dedd9-164">（如果您采用用户输入，将其存储在其他位置，然后在以后&#8212;显示（例如，作为博客注释、用户评论或类似的内容），这一点特别重要。</span><span class="sxs-lookup"><span data-stu-id="dedd9-164">(This is particularly important if you take user input, store it someplace, and then display it later &#8212; for example, as a blog comment, user review, or something like that.)</span></span>
> 
> <span data-ttu-id="dedd9-165">为了帮助防止这些问题，ASP.NET 网页自动对您从代码中输出的任何文本内容进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="dedd9-165">To help prevent these problems, ASP.NET Web Pages automatically HTML-encodes any text content that you output from your code.</span></span> <span data-ttu-id="dedd9-166">例如，当使用代码（如 `@MyVar`）显示变量或表达式的内容时，ASP.NET 网页会自动对输出进行编码。</span><span class="sxs-lookup"><span data-stu-id="dedd9-166">For example, when you display the content of a variable or an expression using code such as `@MyVar`, ASP.NET Web Pages automatically encodes the output.</span></span>

## <a name="validating-user-input"></a><span data-ttu-id="dedd9-167">验证用户输入</span><span class="sxs-lookup"><span data-stu-id="dedd9-167">Validating User Input</span></span>

<span data-ttu-id="dedd9-168">用户出错。</span><span class="sxs-lookup"><span data-stu-id="dedd9-168">Users make mistakes.</span></span> <span data-ttu-id="dedd9-169">要求用户填写某个字段，并将其忽略，或者要求他们输入雇员数量并改为键入名称。</span><span class="sxs-lookup"><span data-stu-id="dedd9-169">You ask them to fill in a field, and they forget to, or you ask them to enter the number of employees and they type a name instead.</span></span> <span data-ttu-id="dedd9-170">若要确保窗体在处理之前已正确填充，需验证用户的输入。</span><span class="sxs-lookup"><span data-stu-id="dedd9-170">To make sure that a form has been filled in correctly before you process it, you validate the user's input.</span></span>

<span data-ttu-id="dedd9-171">此过程说明如何验证所有三个窗体字段，以确保用户不将其留空。</span><span class="sxs-lookup"><span data-stu-id="dedd9-171">This procedure shows how to validate all three form fields to make sure the user didn't leave them blank.</span></span> <span data-ttu-id="dedd9-172">还应检查员工计数值是否为数字。</span><span class="sxs-lookup"><span data-stu-id="dedd9-172">You also check that the employee count value is a number.</span></span> <span data-ttu-id="dedd9-173">如果有错误，将显示一条错误消息，告知用户哪些值未通过验证。</span><span class="sxs-lookup"><span data-stu-id="dedd9-173">If there are errors, you'll display an error message that tells the user what values didn't pass validation.</span></span>

1. <span data-ttu-id="dedd9-174">在 "# *" 文件中，将第*一个代码块替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="dedd9-174">In the *Form.cshtml* file, replace the first block of code with the following code:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    <span data-ttu-id="dedd9-175">若要验证用户输入，请使用 `Validation` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="dedd9-175">To validate user input, you use the `Validation` helper.</span></span> <span data-ttu-id="dedd9-176">可以通过调用 `Validation.RequireField`来注册必填字段。</span><span class="sxs-lookup"><span data-stu-id="dedd9-176">You register required fields by calling `Validation.RequireField`.</span></span> <span data-ttu-id="dedd9-177">您可以通过调用 `Validation.Add` 并指定要验证的字段和要执行的验证类型来注册其他类型的验证。</span><span class="sxs-lookup"><span data-stu-id="dedd9-177">You register other types of validation by calling `Validation.Add` and specifying the field to validate and the type of validation to perform.</span></span>

    <span data-ttu-id="dedd9-178">当页面运行时，ASP.NET 将为你执行所有验证。</span><span class="sxs-lookup"><span data-stu-id="dedd9-178">When the page runs, ASP.NET does all the validation for you.</span></span> <span data-ttu-id="dedd9-179">您可以通过调用 `Validation.IsValid`来检查结果，如果所有内容均通过验证，则返回 true; 如果任何字段未通过验证，则返回 false。</span><span class="sxs-lookup"><span data-stu-id="dedd9-179">You can check the results by calling `Validation.IsValid`, which returns true if everything passed and false if any field failed validation.</span></span> <span data-ttu-id="dedd9-180">通常，在对用户输入执行任何处理之前，先调用 `Validation.IsValid`。</span><span class="sxs-lookup"><span data-stu-id="dedd9-180">Typically, you call `Validation.IsValid` before you perform any processing on the user input.</span></span>
2. <span data-ttu-id="dedd9-181">通过向 `Html.ValidationMessage` 方法添加三次调用来更新 `<body>` 元素，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dedd9-181">Update the `<body>` element by adding three calls to the `Html.ValidationMessage` method, like this:</span></span>

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    <span data-ttu-id="dedd9-182">若要显示验证错误消息，可以调用 Html.`ValidationMessage`</span><span class="sxs-lookup"><span data-stu-id="dedd9-182">To display validation error messages, you can call Html.`ValidationMessage`</span></span> <span data-ttu-id="dedd9-183">并向其传递您需要消息的字段的名称。</span><span class="sxs-lookup"><span data-stu-id="dedd9-183">and pass it the name of the field that you want the message for.</span></span>
3. <span data-ttu-id="dedd9-184">运行页面。</span><span class="sxs-lookup"><span data-stu-id="dedd9-184">Run the page.</span></span> <span data-ttu-id="dedd9-185">将字段留空，然后单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="dedd9-185">Leave the fields blank and click **Submit**.</span></span> <span data-ttu-id="dedd9-186">你将看到错误消息。</span><span class="sxs-lookup"><span data-stu-id="dedd9-186">You see error messages.</span></span>

    ![显示在用户输入未通过验证时显示的错误消息的屏幕截图。](4-working-with-forms/_static/image3.jpg)
4. <span data-ttu-id="dedd9-188">将字符串（例如，"ABC"）添加到 "**员工计数**" 字段，然后再次单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="dedd9-188">Add a string (for example, "ABC") to the **Employee Count** field and click **Submit** again.</span></span> <span data-ttu-id="dedd9-189">此时会出现一个错误，指示该字符串的格式不正确，即整数。</span><span class="sxs-lookup"><span data-stu-id="dedd9-189">This time you see an error that indicates that the string isn't in the right format, namely, an integer.</span></span>

    ![显示在用户为 "员工" 字段输入字符串时显示的错误消息的屏幕截图。](4-working-with-forms/_static/image4.jpg)

<span data-ttu-id="dedd9-191">ASP.NET 网页提供了用于验证用户输入的更多选项，其中包括使用客户端脚本自动执行验证的功能，以便用户可以在浏览器中获得即时反馈。</span><span class="sxs-lookup"><span data-stu-id="dedd9-191">ASP.NET Web Pages provides more options for validating user input, including the ability to automatically perform validation using client script, so that users get immediate feedback in the browser.</span></span> <span data-ttu-id="dedd9-192">有关详细信息，请参阅[其他资源](#Additional_Resources)部分。</span><span class="sxs-lookup"><span data-stu-id="dedd9-192">See the [Additional Resources](#Additional_Resources) section later for more information.</span></span>

## <a name="restoring-form-values-after-postbacks"></a><span data-ttu-id="dedd9-193">在回发之后还原窗体值</span><span class="sxs-lookup"><span data-stu-id="dedd9-193">Restoring Form Values After Postbacks</span></span>

<span data-ttu-id="dedd9-194">当你在上一节中测试页面时，你可能已注意到，如果有验证错误，则你输入的所有内容（不只是无效数据）都已消失，你必须为所有字段重新输入值。</span><span class="sxs-lookup"><span data-stu-id="dedd9-194">When you tested the page in the previous section, you might have noticed that if you had a validation error, everything you entered (not just the invalid data) was gone, and you had to re-enter values for all the fields.</span></span> <span data-ttu-id="dedd9-195">这说明了一个重要的要点：提交页面并处理它，然后再次呈现页面时，将从头开始重新创建页面。</span><span class="sxs-lookup"><span data-stu-id="dedd9-195">This illustrates an important point: when you submit a page, process it, and then render the page again, the page is re-created from scratch.</span></span> <span data-ttu-id="dedd9-196">正如您所看到的，这意味着页面上提交的任何值都将丢失。</span><span class="sxs-lookup"><span data-stu-id="dedd9-196">As you saw, this means that any values that were in the page when it was submitted are lost.</span></span>

<span data-ttu-id="dedd9-197">不过，您可以轻松地解决此问题。</span><span class="sxs-lookup"><span data-stu-id="dedd9-197">You can fix this easily, however.</span></span> <span data-ttu-id="dedd9-198">你有权访问已提交的值（在 `Request.Form` 对象中），因此，在呈现页面时可以将这些值填充到窗体字段。</span><span class="sxs-lookup"><span data-stu-id="dedd9-198">You have access to the values that were submitted (in the `Request.Form` object, so you can fill those values back into the form fields when the page is rendered.</span></span>

1. <span data-ttu-id="dedd9-199">*在 "#" 文件中*，使用 `value` 属性替换 `<input>` 元素的 `value` 属性。：</span><span class="sxs-lookup"><span data-stu-id="dedd9-199">In the *Form.cshtml* file, replace the `value` attributes of the `<input>` elements using the `value` attribute.:</span></span> 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    <span data-ttu-id="dedd9-200">已将 `<input>` 元素的 `value` 属性设置为从 `Request.Form` 对象动态读取字段值。</span><span class="sxs-lookup"><span data-stu-id="dedd9-200">The `value` attribute of the `<input>` elements has been set to dynamically read the field value out of the `Request.Form` object.</span></span> <span data-ttu-id="dedd9-201">第一次请求页面时，`Request.Form` 对象中的值全部为空。</span><span class="sxs-lookup"><span data-stu-id="dedd9-201">The first time that the page is requested, the values in the `Request.Form` object are all empty.</span></span> <span data-ttu-id="dedd9-202">这很好，因为该窗体为空白。</span><span class="sxs-lookup"><span data-stu-id="dedd9-202">This is fine, because that way the form is blank.</span></span>
2. <span data-ttu-id="dedd9-203">在浏览器中启动页面，填写表单域或将其保留为空，然后单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="dedd9-203">Launch the page in your browser, fill in the form fields or leave them blank, and click **Submit**.</span></span> <span data-ttu-id="dedd9-204">将显示一页，其中显示了提交的值。</span><span class="sxs-lookup"><span data-stu-id="dedd9-204">A page that shows the submitted values is displayed.</span></span>

    ![forms 5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="dedd9-206">其他资源</span><span class="sxs-lookup"><span data-stu-id="dedd9-206">Additional Resources</span></span>

- [<span data-ttu-id="dedd9-207">从 Web 用户获取输入的1001方法</span><span class="sxs-lookup"><span data-stu-id="dedd9-207">1,001 Ways to Get Input from Web Users</span></span>](https://msdn.microsoft.com/library/ms971057.aspx)
- <span data-ttu-id="dedd9-208">[使用窗体和处理用户输入](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span><span class="sxs-lookup"><span data-stu-id="dedd9-208">[Using Forms and Processing User Input](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)</span></span>
- [<span data-ttu-id="dedd9-209">在 ASP.NET 网站中验证用户输入</span><span class="sxs-lookup"><span data-stu-id="dedd9-209">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
- <span data-ttu-id="dedd9-210">[使用 HTML 窗体中的自动完成功能](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="dedd9-210">[Using AutoComplete in HTML Forms](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)</span></span>
