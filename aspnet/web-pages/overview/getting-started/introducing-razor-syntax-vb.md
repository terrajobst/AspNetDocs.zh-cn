---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: 使用 Razor 语法的 ASP.NET Web 编程简介（Visual Basic） |Microsoft Docs
author: Rick-Anderson
description: 本附录提供使用 Razor 语法 Visual Basic 中使用 ASP.NET 网页进行编程的概述。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422660"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="46be0-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)（使用 Razor 语法的 ASP.NET Web 编程简介 (Visual Basic)）</span><span class="sxs-lookup"><span data-stu-id="46be0-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="46be0-104">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="46be0-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="46be0-105">本文提供使用 Razor 语法和 Visual Basic 对 ASP.NET 网页进行编程的概述。</span><span class="sxs-lookup"><span data-stu-id="46be0-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="46be0-106">ASP.NET 是 Microsoft 在 web 服务器上运行动态网页的技术。</span><span class="sxs-lookup"><span data-stu-id="46be0-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="46be0-107">**你将学习的内容**：</span><span class="sxs-lookup"><span data-stu-id="46be0-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="46be0-108">使用 Razor 语法编程 ASP.NET 网页入门的前8个编程提示。</span><span class="sxs-lookup"><span data-stu-id="46be0-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="46be0-109">需要的基本编程概念。</span><span class="sxs-lookup"><span data-stu-id="46be0-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="46be0-110">什么是 ASP.NET 服务器代码和 Razor 语法都是如此。</span><span class="sxs-lookup"><span data-stu-id="46be0-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="46be0-111">软件版本</span><span class="sxs-lookup"><span data-stu-id="46be0-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="46be0-112">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="46be0-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="46be0-113">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="46be0-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="46be0-114">使用 ASP.NET 网页 Razor 语法使用C#的大多数示例。</span><span class="sxs-lookup"><span data-stu-id="46be0-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="46be0-115">但 Razor 语法还支持 Visual Basic。</span><span class="sxs-lookup"><span data-stu-id="46be0-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="46be0-116">若要在 Visual Basic 中对 ASP.NET 网页进行编程，请创建一个具有 #*扩展名的网页*，然后添加 Visual Basic 代码。</span><span class="sxs-lookup"><span data-stu-id="46be0-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="46be0-117">本文概述如何使用 Visual Basic 语言和语法来创建 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="46be0-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="46be0-118">Microsoft WebMatrix （**面包店**、**照片库**和**入门网站**等）的默认网站模板在和 Visual Basic 版本中C#可用。</span><span class="sxs-lookup"><span data-stu-id="46be0-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="46be0-119">你可以将 Visual Basic 模板按 NuGet 包的形式安装。</span><span class="sxs-lookup"><span data-stu-id="46be0-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="46be0-120">网站模板安装在网站的根文件夹中，该文件夹位于名为*Microsoft templates*的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="46be0-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="46be0-121">前8个编程提示</span><span class="sxs-lookup"><span data-stu-id="46be0-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="46be0-122">本部分列出了开始使用 Razor 语法编写 ASP.NET 服务器代码时需要了解的一些提示。</span><span class="sxs-lookup"><span data-stu-id="46be0-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="46be0-123">1. 使用 @ 字符将代码添加到页面</span><span class="sxs-lookup"><span data-stu-id="46be0-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="46be0-124">`@` 字符将启动内联表达式、单语句块和多语句块：</span><span class="sxs-lookup"><span data-stu-id="46be0-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="46be0-125">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="46be0-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="46be0-127">**HTML 编码**</span><span class="sxs-lookup"><span data-stu-id="46be0-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="46be0-128">如前面的示例中所示，使用 `@` 字符显示页面中的内容时，ASP.NET 对输出进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="46be0-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="46be0-129">这会将保留 HTML 字符（如 `<` 和 `>` 和 `&`）替换为代码，使字符在网页中显示为字符，而不是解释为 HTML 标记或实体。</span><span class="sxs-lookup"><span data-stu-id="46be0-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="46be0-130">如果没有 HTML 编码，服务器代码的输出可能无法正确显示，并且可能会使页面面临安全风险。</span><span class="sxs-lookup"><span data-stu-id="46be0-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="46be0-131">如果你的目标是输出 HTML 标记，该标记将标记呈现为标记（例如，为段落 `<p></p>` 或 `<em></em>` 强调文本），请参阅本文后面的在[代码块中组合文本、标记和代码](#BM_CombiningTextMarkupAndCode)部分。</span><span class="sxs-lookup"><span data-stu-id="46be0-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="46be0-132">有关 HTML 编码的详细信息，请参阅在[ASP.NET 网页网站中使用 Html 表单](https://go.microsoft.com/fwlink/?LinkId=202892)。</span><span class="sxs-lookup"><span data-stu-id="46be0-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="46be0-133">2. 将代码块括在代码 .。。结束代码</span><span class="sxs-lookup"><span data-stu-id="46be0-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="46be0-134">代码块包含一个或多个代码语句，并以关键字 `Code` 和 `End Code`括起来。</span><span class="sxs-lookup"><span data-stu-id="46be0-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="46be0-135">将左 `Code` 关键字紧靠在 `@` 字符&#8212;后，它们之间不能有空格。</span><span class="sxs-lookup"><span data-stu-id="46be0-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="46be0-136">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="46be0-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="46be0-138">3. 在块中，用换行符结束每个代码语句</span><span class="sxs-lookup"><span data-stu-id="46be0-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="46be0-139">在 Visual Basic 代码块中，每个语句以换行符结尾。</span><span class="sxs-lookup"><span data-stu-id="46be0-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="46be0-140">（稍后在本文中，你将看到一种方法，以便在需要时将长代码语句包装到多行中。）</span><span class="sxs-lookup"><span data-stu-id="46be0-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="46be0-141">4. 使用变量存储值</span><span class="sxs-lookup"><span data-stu-id="46be0-141">4. You use variables to store values</span></span>

<span data-ttu-id="46be0-142">可以将值存储在*变量*中，包括字符串、数字和日期等。使用 `Dim` 关键字创建新变量。</span><span class="sxs-lookup"><span data-stu-id="46be0-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="46be0-143">您可以使用 `@`直接在页面中插入变量值。</span><span class="sxs-lookup"><span data-stu-id="46be0-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="46be0-144">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="46be0-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="46be0-146">5. 将文字字符串值用双引号引起来</span><span class="sxs-lookup"><span data-stu-id="46be0-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="46be0-147">*字符串*是被视为文本的字符序列。</span><span class="sxs-lookup"><span data-stu-id="46be0-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="46be0-148">若要指定字符串，请用双引号将其引起来：</span><span class="sxs-lookup"><span data-stu-id="46be0-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="46be0-149">若要在字符串值中嵌入双引号，请插入两个双引号字符。</span><span class="sxs-lookup"><span data-stu-id="46be0-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="46be0-150">如果希望双引号字符在页面输出中出现一次，则在带引号的字符串中输入它作为 `""`; 如果要显示两次，请在引号内的字符串中输入 `""""`。</span><span class="sxs-lookup"><span data-stu-id="46be0-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="46be0-151">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="46be0-151">The result displayed in a browser:</span></span>

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="46be0-153">6. Visual Basic 代码不区分大小写</span><span class="sxs-lookup"><span data-stu-id="46be0-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="46be0-154">Visual Basic 语言不区分大小写。</span><span class="sxs-lookup"><span data-stu-id="46be0-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="46be0-155">可以在任何情况下编写编程关键字（如 `Dim`、`If`和 `True`）和变量名称（如 `myString`或 `subTotal`）。</span><span class="sxs-lookup"><span data-stu-id="46be0-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="46be0-156">以下代码行使用小写名称将值分配给变量 `lastname`，然后使用大写名称将变量值输出到页面。</span><span class="sxs-lookup"><span data-stu-id="46be0-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="46be0-157">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="46be0-157">The result displayed in a browser:</span></span>

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="46be0-159">7. 您的大部分编码都涉及处理对象</span><span class="sxs-lookup"><span data-stu-id="46be0-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="46be0-160">对象表示您可以使用&#8212;页面、文本框、文件、图像、web 请求、电子邮件、客户记录（数据库行）等进行编程的内容。对象具有描述其特性&#8212;的属性：文本框对象具有 `Text` 属性，请求对象具有 `Url` 属性，电子邮件具有 `From` 属性，而 customer 对象具有 `FirstName` 属性。</span><span class="sxs-lookup"><span data-stu-id="46be0-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="46be0-161">对象还具有可执行&quot; &quot;谓词的方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="46be0-162">示例包括文件对象的 `Save` 方法、图像对象的 `Rotate` 方法和电子邮件对象的 `Send` 方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="46be0-163">你通常会使用 `Request` 对象，该对象提供有关页面上的窗体字段的值（文本框等）、发出请求的浏览器的类型、页面的 URL、用户标识等。此示例演示如何访问 `Request` 对象的属性，以及如何调用 `Request` 对象的 `MapPath` 方法，这为你提供了服务器上页面的绝对路径：</span><span class="sxs-lookup"><span data-stu-id="46be0-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="46be0-164">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="46be0-164">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="46be0-166">8. 您可以编写代码来做出决策</span><span class="sxs-lookup"><span data-stu-id="46be0-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="46be0-167">动态网页的一项重要功能是，你可以根据条件确定要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="46be0-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="46be0-168">要执行此操作，最常见的方法是用 `If` 语句（和可选的 `Else` 语句）。</span><span class="sxs-lookup"><span data-stu-id="46be0-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="46be0-169">语句 `If IsPost` 是编写 `If IsPost = True`的一种简便方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="46be0-170">除了 `If` 语句，还可以使用多种方法来测试条件、重复的代码块等，本文稍后将对此进行介绍。</span><span class="sxs-lookup"><span data-stu-id="46be0-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="46be0-171">在浏览器中显示的结果（在单击 "**提交**" 后）：</span><span class="sxs-lookup"><span data-stu-id="46be0-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="46be0-173">**HTTP GET 和 POST 方法和 IsPost 属性**</span><span class="sxs-lookup"><span data-stu-id="46be0-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="46be0-174">用于 web pages （HTTP）的协议支持用于向服务器发出请求的有限数量的方法（&quot;谓词&quot;）。</span><span class="sxs-lookup"><span data-stu-id="46be0-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="46be0-175">最常见的两个是 GET，用于读取页面，使用 POST 来提交页面。</span><span class="sxs-lookup"><span data-stu-id="46be0-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="46be0-176">通常，当用户第一次请求页面时，将使用 GET 请求页面。</span><span class="sxs-lookup"><span data-stu-id="46be0-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="46be0-177">如果用户填写表单，然后单击 "**提交**"，则浏览器向服务器发出 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="46be0-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="46be0-178">在 web 编程中，很有必要了解页面是否作为 GET 或 POST 请求，以便您知道如何处理页面。</span><span class="sxs-lookup"><span data-stu-id="46be0-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="46be0-179">在 ASP.NET 网页中，可以使用 `IsPost` 属性来查看请求是 GET 还是 POST。</span><span class="sxs-lookup"><span data-stu-id="46be0-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="46be0-180">如果请求是 POST，则 `IsPost` 属性将返回 true，您可以执行一些操作，例如读取窗体上的文本框的值。</span><span class="sxs-lookup"><span data-stu-id="46be0-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="46be0-181">你将看到的许多示例演示了如何根据 `IsPost`的值不同地处理页。</span><span class="sxs-lookup"><span data-stu-id="46be0-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="46be0-182">简单的代码示例</span><span class="sxs-lookup"><span data-stu-id="46be0-182">A Simple Code Example</span></span>

<span data-ttu-id="46be0-183">此过程说明如何创建一个说明基本编程技术的页面。</span><span class="sxs-lookup"><span data-stu-id="46be0-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="46be0-184">在此示例中，您将创建一个允许用户输入两个数字的页面，然后将其添加并显示结果。</span><span class="sxs-lookup"><span data-stu-id="46be0-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="46be0-185">在编辑器中，创建一个新文件并将其命名为*AddNumbers*。</span><span class="sxs-lookup"><span data-stu-id="46be0-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="46be0-186">将以下代码和标记复制到页面中，替换页面中已有的任何内容。</span><span class="sxs-lookup"><span data-stu-id="46be0-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="46be0-187">下面是要注意的一些事项：</span><span class="sxs-lookup"><span data-stu-id="46be0-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="46be0-188">`@` 字符将启动页面中的第一个代码块，并将其置于底部嵌入的 `totalMessage` 变量之前。</span><span class="sxs-lookup"><span data-stu-id="46be0-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="46be0-189">页面顶部的块括在 `Code...End Code`中。</span><span class="sxs-lookup"><span data-stu-id="46be0-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="46be0-190">变量 `total`、`num1`、`num2`和 `totalMessage` 存储几个数字和一个字符串。</span><span class="sxs-lookup"><span data-stu-id="46be0-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="46be0-191">赋给 `totalMessage` 变量的文字字符串值用双引号引起来。</span><span class="sxs-lookup"><span data-stu-id="46be0-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="46be0-192">由于 Visual Basic 代码不区分大小写，因此当在页面底部附近使用 `totalMessage` 变量时，其名称只需要与页面顶部的变量声明的拼写匹配。</span><span class="sxs-lookup"><span data-stu-id="46be0-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="46be0-193">大小写并不重要。</span><span class="sxs-lookup"><span data-stu-id="46be0-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="46be0-194">表达式 `num1.AsInt()` + `num2.AsInt()` 演示了如何使用对象和方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="46be0-195">每个变量的 `AsInt` 方法将用户输入的字符串转换为可添加的整数（整数）。</span><span class="sxs-lookup"><span data-stu-id="46be0-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="46be0-196">`<form>` 标记包含 `method="post"` 特性。</span><span class="sxs-lookup"><span data-stu-id="46be0-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="46be0-197">这指定在用户单击 "**添加**" 时，将使用 HTTP POST 方法将页发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="46be0-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="46be0-198">提交页面后，代码 `If IsPost` 的计算结果为 true，并且运行条件代码，显示添加数字的结果。</span><span class="sxs-lookup"><span data-stu-id="46be0-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="46be0-199">保存页面并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="46be0-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="46be0-200">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）输入两个整数，然后单击 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="46be0-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="46be0-202">Visual Basic 语言和语法</span><span class="sxs-lookup"><span data-stu-id="46be0-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="46be0-203">前面部分介绍了如何创建 ASP.NET 网页，以及如何将服务器代码添加到 HTML 标记的基本示例。</span><span class="sxs-lookup"><span data-stu-id="46be0-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="46be0-204">在这里，你将了解有关使用 Visual Basic 编写 ASP.NET 服务器代码的基础知识， &#8212;该 Razor 语法是编程语言规则。</span><span class="sxs-lookup"><span data-stu-id="46be0-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="46be0-205">如果你使用的是编程（尤其是在使用 C、 C++、 C#、Visual Basic 或 JavaScript）的情况下，你将会熟悉此处所述的大部分内容。</span><span class="sxs-lookup"><span data-stu-id="46be0-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="46be0-206">您可能只需要熟悉如何将 WebMatrix 代码添加到*vbhtml*文件中的标记。</span><span class="sxs-lookup"><span data-stu-id="46be0-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a><span data-ttu-id="46be0-207">在代码块中组合文本、标记和代码</span><span class="sxs-lookup"><span data-stu-id="46be0-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="46be0-208">在服务器代码块中，通常需要将文本和标记输出到页面。</span><span class="sxs-lookup"><span data-stu-id="46be0-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="46be0-209">如果服务器代码块包含不是代码的文本，而应按原样呈现，则 ASP.NET 需要能够区分该文本与代码。</span><span class="sxs-lookup"><span data-stu-id="46be0-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="46be0-210">有多种方法可实现此目的。</span><span class="sxs-lookup"><span data-stu-id="46be0-210">There are several ways to do this.</span></span>

- <span data-ttu-id="46be0-211">将文本括在 HTML 块元素中，如 `<p></p>` 或 `<em></em>`：</span><span class="sxs-lookup"><span data-stu-id="46be0-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="46be0-212">HTML 元素可以包括文本、附加 HTML 元素和服务器代码表达式。</span><span class="sxs-lookup"><span data-stu-id="46be0-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="46be0-213">当 ASP.NET 查看开始 HTML 标记（例如 `<p>`）时，它会将元素及其内容的所有内容呈现为浏览器（并解析服务器代码表达式）。</span><span class="sxs-lookup"><span data-stu-id="46be0-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="46be0-214">使用 `@:` 运算符或 `<text>` 元素。</span><span class="sxs-lookup"><span data-stu-id="46be0-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="46be0-215">`@:` 输出包含纯文本或不匹配 HTML 标记的单个行内容;`<text>` 元素包含多个要输出的行。</span><span class="sxs-lookup"><span data-stu-id="46be0-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="46be0-216">如果您不希望在输出过程中呈现 HTML 元素，则这些选项非常有用。</span><span class="sxs-lookup"><span data-stu-id="46be0-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="46be0-217">下面的示例重复前面的示例，但使用一对 `<text>` 标记来包含要呈现的文本。</span><span class="sxs-lookup"><span data-stu-id="46be0-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="46be0-218">在下面的示例中，"`<text>`" 和 "`</text>`" 标记包含三行，其中所有行都包含一些非包含文本和匹配的 HTML 标记（`<br />`）以及服务器代码和匹配的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="46be0-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="46be0-219">同样，您还可以在每行的前面加上 `@:` 运算符;这两种方法都适用。</span><span class="sxs-lookup"><span data-stu-id="46be0-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="46be0-220">使用 HTML 元素输出此部分&#8212;中所示的文本时，`@:` 运算符或 `<text>` 元素&#8212; ASP.NET 不会对输出进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="46be0-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="46be0-221">（如前文所述，ASP.NET 会对前面是 `@`的服务器代码表达式和服务器代码块的输出进行编码，但本部分中所述的特殊情况除外。</span><span class="sxs-lookup"><span data-stu-id="46be0-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="46be0-222">Whitespace</span><span class="sxs-lookup"><span data-stu-id="46be0-222">Whitespace</span></span>

<span data-ttu-id="46be0-223">语句中的多余空格（字符串文字外）不会影响语句：</span><span class="sxs-lookup"><span data-stu-id="46be0-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="46be0-224">将长语句分解为多行</span><span class="sxs-lookup"><span data-stu-id="46be0-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="46be0-225">您可以在每个代码行后使用下划线字符 `_` （在 Visual Basic 中称为*继续*符），将长代码语句分解为多行。</span><span class="sxs-lookup"><span data-stu-id="46be0-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="46be0-226">若要将某个语句分解到下一行，请在该行的末尾添加一个空格，然后添加继续符。</span><span class="sxs-lookup"><span data-stu-id="46be0-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="46be0-227">继续执行下一行中的语句。</span><span class="sxs-lookup"><span data-stu-id="46be0-227">Continue the statement on the next line.</span></span> <span data-ttu-id="46be0-228">您可以根据需要将语句换行，以提高可读性。</span><span class="sxs-lookup"><span data-stu-id="46be0-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="46be0-229">下列语句相同：</span><span class="sxs-lookup"><span data-stu-id="46be0-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="46be0-230">但是，不能在字符串文字的中间换行。</span><span class="sxs-lookup"><span data-stu-id="46be0-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="46be0-231">下面的示例不起作用：</span><span class="sxs-lookup"><span data-stu-id="46be0-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="46be0-232">若要将换行的长字符串与以上代码一起使用，需要使用*串联运算符*（`&`），稍后将在本文中看到。</span><span class="sxs-lookup"><span data-stu-id="46be0-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="46be0-233">代码注释</span><span class="sxs-lookup"><span data-stu-id="46be0-233">Code comments</span></span>

<span data-ttu-id="46be0-234">您可以为自己或其他人留言。</span><span class="sxs-lookup"><span data-stu-id="46be0-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="46be0-235">Razor 语法注释以 `@*` 为前缀，以 `*@`结尾。</span><span class="sxs-lookup"><span data-stu-id="46be0-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="46be0-236">在代码块中，你可以使用 Razor 语法注释，也可以使用普通的 Visual Basic 注释字符，这是每一行都作为前缀的单引号（`'`）。</span><span class="sxs-lookup"><span data-stu-id="46be0-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="46be0-237">变量</span><span class="sxs-lookup"><span data-stu-id="46be0-237">Variables</span></span>

<span data-ttu-id="46be0-238">变量是用于存储数据的命名对象。</span><span class="sxs-lookup"><span data-stu-id="46be0-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="46be0-239">您可以将变量命名为任何名称，但该名称必须以字母字符开头且不能包含空格或保留字符。</span><span class="sxs-lookup"><span data-stu-id="46be0-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="46be0-240">在 Visual Basic 中，如前文所述，变量名称中字母的大小写并不重要。</span><span class="sxs-lookup"><span data-stu-id="46be0-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="46be0-241">变量和数据类型</span><span class="sxs-lookup"><span data-stu-id="46be0-241">Variables and data types</span></span>

<span data-ttu-id="46be0-242">变量可以具有特定的数据类型，用于指示变量中存储的数据类型。</span><span class="sxs-lookup"><span data-stu-id="46be0-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="46be0-243">可以有存储字符串值（如 &quot;Hello world&quot;）的字符串变量、存储整数值的整数变量（例如3或79）以及以多种格式存储日期值的日期变量（如4/12/2012 或3月2009）。</span><span class="sxs-lookup"><span data-stu-id="46be0-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="46be0-244">还可以使用许多其他数据类型。</span><span class="sxs-lookup"><span data-stu-id="46be0-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="46be0-245">但是，您不必为变量指定类型。</span><span class="sxs-lookup"><span data-stu-id="46be0-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="46be0-246">在大多数情况下，ASP.NET 可以根据变量中的数据的使用方式判断出类型。</span><span class="sxs-lookup"><span data-stu-id="46be0-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="46be0-247">（有时您必须指定一个类型，您将看到这样的示例。）</span><span class="sxs-lookup"><span data-stu-id="46be0-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="46be0-248">若要在不指定类型的情况下声明变量，请使用 `Dim` 加变量名（例如，`Dim myVar`）。</span><span class="sxs-lookup"><span data-stu-id="46be0-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="46be0-249">若要声明类型为的变量，请使用 `Dim` 和变量名称，然后使用 `As` 和类型名称（例如，`Dim myVar As String`）。</span><span class="sxs-lookup"><span data-stu-id="46be0-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="46be0-250">下面的示例演示一些使用网页中的变量的内联表达式。</span><span class="sxs-lookup"><span data-stu-id="46be0-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="46be0-251">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="46be0-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="46be0-253">转换和测试数据类型</span><span class="sxs-lookup"><span data-stu-id="46be0-253">Converting and testing data types</span></span>

<span data-ttu-id="46be0-254">尽管 ASP.NET 通常可以自动确定数据类型，但有时不能。</span><span class="sxs-lookup"><span data-stu-id="46be0-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="46be0-255">因此，您可能需要通过执行显式转换来帮助 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="46be0-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="46be0-256">即使您不需要转换类型，有时也可以通过测试来查看您可能使用的数据类型。</span><span class="sxs-lookup"><span data-stu-id="46be0-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="46be0-257">最常见的情况是必须将字符串转换为其他类型，例如整数或日期。</span><span class="sxs-lookup"><span data-stu-id="46be0-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="46be0-258">下面的示例演示一个典型情况，您必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="46be0-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="46be0-259">作为一种规则，用户输入作为字符串提供给你。</span><span class="sxs-lookup"><span data-stu-id="46be0-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="46be0-260">即使您已提示用户输入一个数字，甚至输入了一个数字，在提交用户输入并在代码中读取它时，数据仍采用字符串格式。</span><span class="sxs-lookup"><span data-stu-id="46be0-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="46be0-261">因此，必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="46be0-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="46be0-262">在此示例中，如果你尝试对值执行算术运算而不转换这些值，则会产生以下错误，因为 ASP.NET 无法添加两个字符串：</span><span class="sxs-lookup"><span data-stu-id="46be0-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="46be0-263">若要将值转换为整数，请调用 `AsInt` 方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="46be0-264">如果转换成功，则可以添加数字。</span><span class="sxs-lookup"><span data-stu-id="46be0-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="46be0-265">下表列出了一些常见的变量转换方法和测试方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-265">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="46be0-266"><strong>方法</strong></span><span class="sxs-lookup"><span data-stu-id="46be0-266"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-267"><strong>描述</strong></span><span class="sxs-lookup"><span data-stu-id="46be0-267"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-268"><strong>示例</strong></span><span class="sxs-lookup"><span data-stu-id="46be0-268"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-269">将表示整数（如 &quot;593&quot;）的字符串转换为整数。</span><span class="sxs-lookup"><span data-stu-id="46be0-269">Converts a string that represents a whole number (like &quot;593&quot;) to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-270">将字符串（如 &quot;true&quot; 或 &quot;false&quot; 转换为布尔类型。</span><span class="sxs-lookup"><span data-stu-id="46be0-270">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-271">将具有十进制值（如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字符串转换为浮点数。</span><span class="sxs-lookup"><span data-stu-id="46be0-271">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-272">将具有十进制值（如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字符串转换为十进制数字。</span><span class="sxs-lookup"><span data-stu-id="46be0-272">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="46be0-273">（在 ASP.NET 中，小数比浮点数更精确。）</span><span class="sxs-lookup"><span data-stu-id="46be0-273">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-274">将表示日期和时间值的字符串转换为 ASP.NET `DateTime` 类型。</span><span class="sxs-lookup"><span data-stu-id="46be0-274">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-275">将任何其他数据类型转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="46be0-275">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="46be0-276">运算符</span><span class="sxs-lookup"><span data-stu-id="46be0-276">Operators</span></span>

<span data-ttu-id="46be0-277">运算符是一个关键字或字符，用于告知 ASP.NET 要在表达式中执行哪种类型的命令。</span><span class="sxs-lookup"><span data-stu-id="46be0-277">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="46be0-278">Visual Basic 支持许多运算符，但你只需要识别一些操作即可开始开发 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="46be0-278">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="46be0-279">下表总结了最常见的运算符。</span><span class="sxs-lookup"><span data-stu-id="46be0-279">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="46be0-280"><strong>Operator</strong></span><span class="sxs-lookup"><span data-stu-id="46be0-280"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-281"><strong>描述</strong></span><span class="sxs-lookup"><span data-stu-id="46be0-281"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-282"><strong>示例</strong></span><span class="sxs-lookup"><span data-stu-id="46be0-282"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-283">数值表达式中使用的数学运算符。</span><span class="sxs-lookup"><span data-stu-id="46be0-283">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-284">赋值和相等。</span><span class="sxs-lookup"><span data-stu-id="46be0-284">Assignment and equality.</span></span> <span data-ttu-id="46be0-285">根据上下文，可以将语句右侧的值分配给左侧的对象，也可以检查值是否相等。</span><span class="sxs-lookup"><span data-stu-id="46be0-285">Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-286">不相等。</span><span class="sxs-lookup"><span data-stu-id="46be0-286">Inequality.</span></span> <span data-ttu-id="46be0-287">如果值不相等，则返回 `True`。</span><span class="sxs-lookup"><span data-stu-id="46be0-287">Returns `True` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-288">小于、大于、小于等于、大于或等于。</span><span class="sxs-lookup"><span data-stu-id="46be0-288">Less than, greater than, less than or equal, and greater than or equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-289">串联，用于联接字符串。</span><span class="sxs-lookup"><span data-stu-id="46be0-289">Concatenation, which is used to join strings.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-290">递增和递减运算符，它们分别增加和减少1。</span><span class="sxs-lookup"><span data-stu-id="46be0-290">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-291">着重号.</span><span class="sxs-lookup"><span data-stu-id="46be0-291">Dot.</span></span> <span data-ttu-id="46be0-292">用于区分对象及其属性和方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-292">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-293">括号.</span><span class="sxs-lookup"><span data-stu-id="46be0-293">Parentheses.</span></span> <span data-ttu-id="46be0-294">用于对表达式进行分组、将参数传递给方法，以及访问数组和集合的成员。</span><span class="sxs-lookup"><span data-stu-id="46be0-294">Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-295">不仅.</span><span class="sxs-lookup"><span data-stu-id="46be0-295">Not.</span></span> <span data-ttu-id="46be0-296">反转 true 值为 false，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="46be0-296">Reverses a true value to false and vice versa.</span></span> <span data-ttu-id="46be0-297">通常用作测试 `False` （即，不 `True`）的一种简便方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-297">Typically used as a shorthand way to test for `False` (that is, for not `True`).</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        <span data-ttu-id="46be0-298">逻辑 "与" 或 "或"，用于将条件链接在一起。</span><span class="sxs-lookup"><span data-stu-id="46be0-298">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="46be0-299">处理代码中的文件和文件夹路径</span><span class="sxs-lookup"><span data-stu-id="46be0-299">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="46be0-300">通常会在代码中使用文件和文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="46be0-300">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="46be0-301">下面是网站的物理文件夹结构示例，因为它可能出现在开发计算机上：</span><span class="sxs-lookup"><span data-stu-id="46be0-301">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="46be0-302">下面是有关 Url 和路径的一些基本详细信息：</span><span class="sxs-lookup"><span data-stu-id="46be0-302">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="46be0-303">URL 以域名（`http://www.example.com`）或服务器名称（`http://localhost`，`http://mycomputer`）开头。</span><span class="sxs-lookup"><span data-stu-id="46be0-303">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="46be0-304">URL 对应于主计算机上的物理路径。</span><span class="sxs-lookup"><span data-stu-id="46be0-304">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="46be0-305">例如，`http://myserver` 可能对应于服务器上的*C:\websites\mywebsite*文件夹。</span><span class="sxs-lookup"><span data-stu-id="46be0-305">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="46be0-306">虚拟路径是在代码中表示路径的速记，无需指定完整路径。</span><span class="sxs-lookup"><span data-stu-id="46be0-306">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="46be0-307">它包括位于域或服务器名称后面的 URL 部分。</span><span class="sxs-lookup"><span data-stu-id="46be0-307">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="46be0-308">使用虚拟路径时，可以将代码移到不同的域或服务器上，而无需更新路径。</span><span class="sxs-lookup"><span data-stu-id="46be0-308">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="46be0-309">下面是一个示例，可帮助你了解不同之处：</span><span class="sxs-lookup"><span data-stu-id="46be0-309">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="46be0-310">完成 URL</span><span class="sxs-lookup"><span data-stu-id="46be0-310">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="46be0-311">服务器名称</span><span class="sxs-lookup"><span data-stu-id="46be0-311">Server name</span></span> | <span data-ttu-id="46be0-312">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="46be0-312">*mycompanyserver*</span></span> |
| <span data-ttu-id="46be0-313">虚拟路径</span><span class="sxs-lookup"><span data-stu-id="46be0-313">Virtual path</span></span> | <span data-ttu-id="46be0-314">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="46be0-314">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="46be0-315">物理路径</span><span class="sxs-lookup"><span data-stu-id="46be0-315">Physical path</span></span> | <span data-ttu-id="46be0-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="46be0-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="46be0-317">虚拟根目录为/，正如 C：驱动器的根目录为 \。</span><span class="sxs-lookup"><span data-stu-id="46be0-317">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="46be0-318">（虚拟文件夹路径始终使用正斜杠。）文件夹的虚拟路径不必与物理文件夹同名;它可以是别名。</span><span class="sxs-lookup"><span data-stu-id="46be0-318">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="46be0-319">（在生产服务器上，虚拟路径很少匹配确切的物理路径。）</span><span class="sxs-lookup"><span data-stu-id="46be0-319">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="46be0-320">当你在代码中处理文件和文件夹时，有时需要引用物理路径，有时还需要引用虚拟路径，具体取决于你使用的对象。</span><span class="sxs-lookup"><span data-stu-id="46be0-320">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="46be0-321">ASP.NET 提供了以下工具来处理代码中的文件和文件夹路径： `Server.MapPath` 方法、`~` 运算符和 `Href` 方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-321">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="46be0-322">将虚拟路径转换为物理路径：服务器. MapPath 方法</span><span class="sxs-lookup"><span data-stu-id="46be0-322">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="46be0-323">`Server.MapPath` 方法将虚拟路径（如 */default.cshtml*）转换为绝对物理路径（如*C:\WebSites\MyWebSiteFolder\default.cshtml*）。</span><span class="sxs-lookup"><span data-stu-id="46be0-323">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="46be0-324">任何时候都需要完整的物理路径时，可以使用此方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-324">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="46be0-325">典型的示例是在 web 服务器上读取或写入文本文件或图像文件时。</span><span class="sxs-lookup"><span data-stu-id="46be0-325">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="46be0-326">您通常不知道站点在宿主站点的服务器上的绝对物理路径，因此此方法可以将您知道的路径（虚拟路径）转换为服务器上的相应路径。</span><span class="sxs-lookup"><span data-stu-id="46be0-326">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="46be0-327">将文件或文件夹的虚拟路径传递给方法，并返回物理路径：</span><span class="sxs-lookup"><span data-stu-id="46be0-327">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="46be0-328">引用虚拟根： ~ operator 和 Href 方法</span><span class="sxs-lookup"><span data-stu-id="46be0-328">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="46be0-329">在*cshtml*或*vbhtml*文件中，可以使用 `~` 运算符引用虚拟根路径。</span><span class="sxs-lookup"><span data-stu-id="46be0-329">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="46be0-330">这非常方便，因为您可以在站点中移动页面，并且任何包含到其他页面的链接都不会损坏。</span><span class="sxs-lookup"><span data-stu-id="46be0-330">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="46be0-331">如果你将网站移到其他位置，也可以方便地使用它。</span><span class="sxs-lookup"><span data-stu-id="46be0-331">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="46be0-332">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="46be0-332">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="46be0-333">如果网站 `http://myserver/myapp`，以下是在页面运行时 ASP.NET 将如何处理这些路径：</span><span class="sxs-lookup"><span data-stu-id="46be0-333">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="46be0-334">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="46be0-334">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="46be0-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="46be0-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="46be0-336">（实际上，您不会看到这些路径作为变量的值，而 ASP.NET 会将这些路径视为它们。）</span><span class="sxs-lookup"><span data-stu-id="46be0-336">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="46be0-337">可以在服务器代码（如上所示）和标记中使用 `~` 运算符，如下所示：</span><span class="sxs-lookup"><span data-stu-id="46be0-337">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="46be0-338">在标记中，使用 `~` 运算符来创建资源的路径，如图像文件、其他网页和 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="46be0-338">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="46be0-339">当该页运行时，ASP.NET 将浏览该页（代码和标记），并将所有 `~` 引用解析为相应的路径。</span><span class="sxs-lookup"><span data-stu-id="46be0-339">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="46be0-340">条件逻辑和循环</span><span class="sxs-lookup"><span data-stu-id="46be0-340">Conditional Logic and Loops</span></span>

<span data-ttu-id="46be0-341">通过 ASP.NET 服务器代码，你可以根据条件执行任务，并编写代码，将语句重复指定次数（即运行循环的代码）。</span><span class="sxs-lookup"><span data-stu-id="46be0-341">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="46be0-342">测试条件</span><span class="sxs-lookup"><span data-stu-id="46be0-342">Testing conditions</span></span>

<span data-ttu-id="46be0-343">若要测试简单的条件，请使用 `If...Then` 语句，该语句根据指定的测试返回 `True` 或 `False`：</span><span class="sxs-lookup"><span data-stu-id="46be0-343">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="46be0-344">`If` 关键字启动块。</span><span class="sxs-lookup"><span data-stu-id="46be0-344">The `If` keyword starts a block.</span></span> <span data-ttu-id="46be0-345">实际测试（条件）遵循 `If` 关键字，并返回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="46be0-345">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="46be0-346">`If` 语句以 `Then`结束。</span><span class="sxs-lookup"><span data-stu-id="46be0-346">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="46be0-347">如果测试为 true，则将运行的语句由 `If` 和 `End If`括起来。</span><span class="sxs-lookup"><span data-stu-id="46be0-347">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="46be0-348">`If` 语句可以包括指定语句的 `Else` 块，条件为 false 时运行：</span><span class="sxs-lookup"><span data-stu-id="46be0-348">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="46be0-349">如果 `If` 语句启动一个代码块，则无需使用 normal `Code...End Code` 语句来包含这些块。</span><span class="sxs-lookup"><span data-stu-id="46be0-349">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="46be0-350">你只需将 `@` 添加到块中，它将正常工作。</span><span class="sxs-lookup"><span data-stu-id="46be0-350">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="46be0-351">此方法适用于 `If` 和后面跟有代码块的其他 Visual Basic 编程关键字，包括 `For`、`For Each`、`Do While`等。</span><span class="sxs-lookup"><span data-stu-id="46be0-351">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="46be0-352">可以使用一个或多个 `ElseIf` 块添加多个条件：</span><span class="sxs-lookup"><span data-stu-id="46be0-352">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="46be0-353">在此示例中，如果 `If` 块中的第一个条件不为 true，则检查 `ElseIf` 条件。</span><span class="sxs-lookup"><span data-stu-id="46be0-353">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="46be0-354">如果满足该条件，则执行 `ElseIf` 块中的语句。</span><span class="sxs-lookup"><span data-stu-id="46be0-354">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="46be0-355">如果未满足任何条件，则执行 `Else` 块中的语句。</span><span class="sxs-lookup"><span data-stu-id="46be0-355">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="46be0-356">你可以添加任意数量的 `ElseIf` 块，然后使用 `Else` 块作为 &quot;所有其他&quot; 条件来结束。</span><span class="sxs-lookup"><span data-stu-id="46be0-356">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="46be0-357">若要测试大量条件，请使用 `Select Case` 块：</span><span class="sxs-lookup"><span data-stu-id="46be0-357">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="46be0-358">要测试的值位于括号内（在本示例中为 weekday 变量）。</span><span class="sxs-lookup"><span data-stu-id="46be0-358">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="46be0-359">每个单独的测试都使用 `Case` 语句来列出某个值。</span><span class="sxs-lookup"><span data-stu-id="46be0-359">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="46be0-360">如果 `Case` 语句的值与测试值匹配，则将执行该 `Case` 块中的代码。</span><span class="sxs-lookup"><span data-stu-id="46be0-360">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="46be0-361">在浏览器中显示的最后两个条件块的结果：</span><span class="sxs-lookup"><span data-stu-id="46be0-361">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="46be0-363">循环代码</span><span class="sxs-lookup"><span data-stu-id="46be0-363">Looping code</span></span>

<span data-ttu-id="46be0-364">经常需要重复运行相同的语句。</span><span class="sxs-lookup"><span data-stu-id="46be0-364">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="46be0-365">通过循环执行此操作。</span><span class="sxs-lookup"><span data-stu-id="46be0-365">You do this by looping.</span></span> <span data-ttu-id="46be0-366">例如，通常对数据集合中的每个项运行相同的语句。</span><span class="sxs-lookup"><span data-stu-id="46be0-366">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="46be0-367">如果确切知道要循环多少次，则可以使用 `For` 循环。</span><span class="sxs-lookup"><span data-stu-id="46be0-367">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="46be0-368">此类循环特别适用于计算或计数：</span><span class="sxs-lookup"><span data-stu-id="46be0-368">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="46be0-369">循环以 `For` 关键字开头，后跟三个元素：</span><span class="sxs-lookup"><span data-stu-id="46be0-369">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="46be0-370">紧跟在 `For` 语句之后，可以声明一个计数器变量（不必使用 `Dim`），然后指示范围，如 `i = 10 to 20`中所示。</span><span class="sxs-lookup"><span data-stu-id="46be0-370">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="46be0-371">这意味着变量 `i` 将开始计数为10，并继续，直到达到20（含）。</span><span class="sxs-lookup"><span data-stu-id="46be0-371">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="46be0-372">`For` 和 `Next` 语句之间是块的内容。</span><span class="sxs-lookup"><span data-stu-id="46be0-372">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="46be0-373">这可以包含一个或多个在每个循环中执行的代码语句。</span><span class="sxs-lookup"><span data-stu-id="46be0-373">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="46be0-374">`Next i` 语句结束循环。</span><span class="sxs-lookup"><span data-stu-id="46be0-374">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="46be0-375">它会递增计数器并启动循环的下一次迭代。</span><span class="sxs-lookup"><span data-stu-id="46be0-375">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="46be0-376">`For` 和 `Next` 行之间的代码行包含为每个循环迭代运行的代码。</span><span class="sxs-lookup"><span data-stu-id="46be0-376">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="46be0-377">标记每次创建一个新段落（`<p>` 元素）并向输出添加一行，并显示 i （计数器）的值。</span><span class="sxs-lookup"><span data-stu-id="46be0-377">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="46be0-378">运行此页时，此示例将创建11行显示输出，每行中的文本指示项号。</span><span class="sxs-lookup"><span data-stu-id="46be0-378">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="46be0-380">如果使用的是集合或数组，通常使用 `For Each` 循环。</span><span class="sxs-lookup"><span data-stu-id="46be0-380">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="46be0-381">集合是一组类似的对象，而 `For Each` 循环使你可以对集合中的每个项执行一个任务。</span><span class="sxs-lookup"><span data-stu-id="46be0-381">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="46be0-382">这种类型的循环非常适合于回收，因为与 `For` 循环不同，您不必递增计数器或设置限制。</span><span class="sxs-lookup"><span data-stu-id="46be0-382">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="46be0-383">相反，`For Each` 循环代码只需经过回收，直到完成。</span><span class="sxs-lookup"><span data-stu-id="46be0-383">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="46be0-384">此示例返回 `Request.ServerVariables` 集合中的项（包含有关 web 服务器的信息）。</span><span class="sxs-lookup"><span data-stu-id="46be0-384">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="46be0-385">它通过在 HTML 项目符号列表中创建新的 `<li>` 元素，使用 `For Each` 循环来显示每个项的名称。</span><span class="sxs-lookup"><span data-stu-id="46be0-385">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="46be0-386">`For Each` 关键字后跟一个变量，该变量表示集合中的单个项（在本例中为 `myItem`），后跟 `In` 关键字，后跟要循环访问的集合。</span><span class="sxs-lookup"><span data-stu-id="46be0-386">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="46be0-387">在 `For Each` 循环的主体中，可以使用之前声明的变量访问当前项。</span><span class="sxs-lookup"><span data-stu-id="46be0-387">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="46be0-389">若要创建更通用的循环，请使用 `Do While` 语句：</span><span class="sxs-lookup"><span data-stu-id="46be0-389">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="46be0-390">此循环以 `Do While` 关键字开头，后跟一个条件，然后是要重复的块。</span><span class="sxs-lookup"><span data-stu-id="46be0-390">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="46be0-391">循环通常会递增（添加到）或递减（减去）用于计数的变量或对象。</span><span class="sxs-lookup"><span data-stu-id="46be0-391">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="46be0-392">在此示例中，每次循环运行时，`+=` 运算符都向变量的值加1。</span><span class="sxs-lookup"><span data-stu-id="46be0-392">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="46be0-393">（若要减小循环中计算的变量，请使用减量运算符 `-=`。）</span><span class="sxs-lookup"><span data-stu-id="46be0-393">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="46be0-394">对象和集合</span><span class="sxs-lookup"><span data-stu-id="46be0-394">Objects and Collections</span></span>

<span data-ttu-id="46be0-395">ASP.NET 网站中的几乎所有内容都是一个对象，包括网页本身。</span><span class="sxs-lookup"><span data-stu-id="46be0-395">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="46be0-396">本部分讨论你将经常在代码中使用的一些重要对象。</span><span class="sxs-lookup"><span data-stu-id="46be0-396">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="46be0-397">页面对象</span><span class="sxs-lookup"><span data-stu-id="46be0-397">Page objects</span></span>

<span data-ttu-id="46be0-398">ASP.NET 中的最基本对象是页面。</span><span class="sxs-lookup"><span data-stu-id="46be0-398">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="46be0-399">您可以直接访问 page 对象的属性，而无需任何合格的对象。</span><span class="sxs-lookup"><span data-stu-id="46be0-399">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="46be0-400">下面的代码使用页面的 `Request` 对象获取页面的文件路径：</span><span class="sxs-lookup"><span data-stu-id="46be0-400">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="46be0-401">您可以使用 `Page` 对象的属性来获取很多信息，例如：</span><span class="sxs-lookup"><span data-stu-id="46be0-401">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="46be0-402">`Request`。</span><span class="sxs-lookup"><span data-stu-id="46be0-402">`Request`.</span></span> <span data-ttu-id="46be0-403">正如您所看到的，这是有关当前请求的信息的集合，包括发出请求的浏览器的类型、页面的 URL、用户标识等。</span><span class="sxs-lookup"><span data-stu-id="46be0-403">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="46be0-404">`Response`。</span><span class="sxs-lookup"><span data-stu-id="46be0-404">`Response`.</span></span> <span data-ttu-id="46be0-405">这是在服务器代码完成运行时将发送到浏览器的响应（页）信息的集合。</span><span class="sxs-lookup"><span data-stu-id="46be0-405">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="46be0-406">例如，您可以使用此属性将信息写入响应中。</span><span class="sxs-lookup"><span data-stu-id="46be0-406">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="46be0-407">集合对象（数组和字典）</span><span class="sxs-lookup"><span data-stu-id="46be0-407">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="46be0-408">集合是一组相同类型的对象，例如来自数据库的 `Customer` 对象的集合。</span><span class="sxs-lookup"><span data-stu-id="46be0-408">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="46be0-409">ASP.NET 包含许多内置集合，如 `Request.Files` 集合。</span><span class="sxs-lookup"><span data-stu-id="46be0-409">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="46be0-410">通常会使用集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="46be0-410">You'll often work with data in collections.</span></span> <span data-ttu-id="46be0-411">两个常见的集合类型是*数组*和*字典*。</span><span class="sxs-lookup"><span data-stu-id="46be0-411">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="46be0-412">如果希望存储类似项的集合，但又不想创建单独的变量来保存每个项，则数组将非常有用：</span><span class="sxs-lookup"><span data-stu-id="46be0-412">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="46be0-413">使用数组，可以声明特定的数据类型，例如 `String`、`Integer`或 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="46be0-413">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="46be0-414">若要指示变量可以包含数组，请在声明中向变量名称添加括号（如 `Dim myVar() As String`）。</span><span class="sxs-lookup"><span data-stu-id="46be0-414">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="46be0-415">您可以使用其位置（索引）或使用 `For Each` 语句来访问数组中的项。</span><span class="sxs-lookup"><span data-stu-id="46be0-415">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="46be0-416">数组索引从零开始， &#8212;这是，第一个项的位置为0，第二项位于位置1，依此类推。</span><span class="sxs-lookup"><span data-stu-id="46be0-416">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="46be0-417">可以通过获取数组中的项的 `Length` 属性来确定这些项的数目。</span><span class="sxs-lookup"><span data-stu-id="46be0-417">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="46be0-418">若要获取数组中特定项的位置（即，若要搜索数组），请使用 `Array.IndexOf` 方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-418">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="46be0-419">您还可以执行一些操作，例如反转数组的内容（`Array.Reverse` 方法）或对内容进行排序（`Array.Sort` 方法）。</span><span class="sxs-lookup"><span data-stu-id="46be0-419">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="46be0-420">在浏览器中显示的字符串数组代码的输出：</span><span class="sxs-lookup"><span data-stu-id="46be0-420">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="46be0-422">字典是键/值对的集合，其中提供了用于设置或检索相应值的键（或名称）：</span><span class="sxs-lookup"><span data-stu-id="46be0-422">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="46be0-423">若要创建字典，请使用 `New` 关键字指示正在创建新的 `Dictionary` 对象。</span><span class="sxs-lookup"><span data-stu-id="46be0-423">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="46be0-424">可以使用 `Dim` 关键字为变量分配字典。</span><span class="sxs-lookup"><span data-stu-id="46be0-424">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="46be0-425">使用括号（`( )`）指示字典中项的数据类型。</span><span class="sxs-lookup"><span data-stu-id="46be0-425">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="46be0-426">在声明的末尾，你必须添加另一对括号，因为这实际上是创建新字典的方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-426">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="46be0-427">若要将项添加到字典中，可以调用字典变量的 `Add` 方法（在本例中为`myScores`），然后指定键和值。</span><span class="sxs-lookup"><span data-stu-id="46be0-427">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="46be0-428">或者，您可以使用括号来指示密钥并执行简单的分配，如以下示例中所示：</span><span class="sxs-lookup"><span data-stu-id="46be0-428">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="46be0-429">若要从字典中获取值，请在括号中指定密钥：</span><span class="sxs-lookup"><span data-stu-id="46be0-429">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="46be0-430">调用带参数的方法</span><span class="sxs-lookup"><span data-stu-id="46be0-430">Calling Methods with Parameters</span></span>

<span data-ttu-id="46be0-431">正如您在本文前面所看到的那样，使用进行编程的对象具有方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-431">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="46be0-432">例如，`Database` 对象可能具有 `Database.Connect` 方法。</span><span class="sxs-lookup"><span data-stu-id="46be0-432">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="46be0-433">许多方法还具有一个或多个参数。</span><span class="sxs-lookup"><span data-stu-id="46be0-433">Many methods also have one or more parameters.</span></span> <span data-ttu-id="46be0-434">*参数*是传递给方法以使方法完成其任务的值。</span><span class="sxs-lookup"><span data-stu-id="46be0-434">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="46be0-435">例如，查看 `Request.MapPath` 方法的声明，该方法采用三个参数：</span><span class="sxs-lookup"><span data-stu-id="46be0-435">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="46be0-436">此方法返回与指定虚拟路径相对应的服务器上的物理路径。</span><span class="sxs-lookup"><span data-stu-id="46be0-436">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="46be0-437">方法的三个参数 `virtualPath`、`baseVirtualDir`和 `allowCrossAppMapping`。</span><span class="sxs-lookup"><span data-stu-id="46be0-437">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="46be0-438">（请注意，在声明中，参数与它们将接受的数据的数据类型一起列出。）调用此方法时，必须为所有三个参数提供值。</span><span class="sxs-lookup"><span data-stu-id="46be0-438">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="46be0-439">使用 Razor 语法的 Visual Basic 时，有两个选项可用于将参数传递给方法：*位置参数*或*命名参数*。</span><span class="sxs-lookup"><span data-stu-id="46be0-439">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="46be0-440">若要使用位置参数调用方法，请按方法声明中指定的严格顺序传递参数。</span><span class="sxs-lookup"><span data-stu-id="46be0-440">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="46be0-441">（您通常可以通过阅读该方法的文档来了解此顺序。）必须按照顺序进行操作，如果必要，则不能跳过&#8212;任何参数，对于没有值的位置参数，可以传递空字符串（`""`）或 null。</span><span class="sxs-lookup"><span data-stu-id="46be0-441">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="46be0-442">以下示例假定网站上有一个名为 "*脚本*" 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="46be0-442">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="46be0-443">此代码调用 `Request.MapPath` 方法，并按正确的顺序传递三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="46be0-443">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="46be0-444">然后，它会显示生成的映射路径。</span><span class="sxs-lookup"><span data-stu-id="46be0-444">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="46be0-445">如果有多个参数用于方法，则可以通过使用命名参数来使代码更简洁、更具可读性。</span><span class="sxs-lookup"><span data-stu-id="46be0-445">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="46be0-446">若要使用命名参数调用方法，请指定参数名称后接 `:=`，然后提供值。</span><span class="sxs-lookup"><span data-stu-id="46be0-446">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="46be0-447">命名参数的优点是可以按所需的任意顺序添加它们。</span><span class="sxs-lookup"><span data-stu-id="46be0-447">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="46be0-448">（缺点是方法调用并不是压缩方法。）</span><span class="sxs-lookup"><span data-stu-id="46be0-448">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="46be0-449">下面的示例调用与上面相同的方法，但使用命名参数来提供值：</span><span class="sxs-lookup"><span data-stu-id="46be0-449">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="46be0-450">正如您所看到的，参数以不同的顺序传递。</span><span class="sxs-lookup"><span data-stu-id="46be0-450">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="46be0-451">但是，如果运行前面的示例和此示例，它们将返回相同的值。</span><span class="sxs-lookup"><span data-stu-id="46be0-451">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="46be0-452">处理错误</span><span class="sxs-lookup"><span data-stu-id="46be0-452">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="46be0-453">Try-catch 语句</span><span class="sxs-lookup"><span data-stu-id="46be0-453">Try-Catch statements</span></span>

<span data-ttu-id="46be0-454">由于控件外的原因，你的代码中经常会出现语句。</span><span class="sxs-lookup"><span data-stu-id="46be0-454">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="46be0-455">例如:</span><span class="sxs-lookup"><span data-stu-id="46be0-455">For example:</span></span>

- <span data-ttu-id="46be0-456">如果你的代码尝试打开、创建、读取或写入文件，则可能会出现各种错误。</span><span class="sxs-lookup"><span data-stu-id="46be0-456">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="46be0-457">你需要的文件可能不存在，可能已被锁定，代码可能没有权限，等等。</span><span class="sxs-lookup"><span data-stu-id="46be0-457">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="46be0-458">同样，如果你的代码尝试更新数据库中的记录，则可能存在权限问题，可能会删除与数据库的连接，要保存的数据可能会无效，依此类推。</span><span class="sxs-lookup"><span data-stu-id="46be0-458">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="46be0-459">在编程术语中，这种情况称为 "*异常*"。</span><span class="sxs-lookup"><span data-stu-id="46be0-459">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="46be0-460">如果你的代码遇到异常，则会生成（引发）一条错误消息，该消息对用户而言是一种非常令人讨厌的错误消息。</span><span class="sxs-lookup"><span data-stu-id="46be0-460">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="46be0-462">在代码可能遇到异常的情况下，若要避免此类型的错误消息，可以使用 `Try/Catch` 语句。</span><span class="sxs-lookup"><span data-stu-id="46be0-462">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="46be0-463">在 `Try` 语句中，运行要检查的代码。</span><span class="sxs-lookup"><span data-stu-id="46be0-463">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="46be0-464">在一个或多个 `Catch` 语句中，可以查找可能发生的特定错误（特定类型的异常）。</span><span class="sxs-lookup"><span data-stu-id="46be0-464">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="46be0-465">您可以包含任意数量的 `Catch` 语句，以便查找您要预测的错误。</span><span class="sxs-lookup"><span data-stu-id="46be0-465">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="46be0-466">建议避免在 `Try/Catch` 语句中使用 `Response.Redirect` 方法，因为这可能会导致页中出现异常。</span><span class="sxs-lookup"><span data-stu-id="46be0-466">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="46be0-467">下面的示例演示了在第一个请求中创建文本文件的页面，然后显示一个按钮，使用户可以打开该文件。</span><span class="sxs-lookup"><span data-stu-id="46be0-467">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="46be0-468">该示例有意使用错误的文件名，以便它将导致异常。</span><span class="sxs-lookup"><span data-stu-id="46be0-468">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="46be0-469">此代码包含两个可能的异常的 `Catch` 语句： `FileNotFoundException`，如果文件名错误 `DirectoryNotFoundException`，则会发生这种情况，在 ASP.NET 甚至不能找到该文件夹时，也会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="46be0-469">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="46be0-470">（您可以在示例中取消注释语句，以查看它在一切正常工作时的运行情况。）</span><span class="sxs-lookup"><span data-stu-id="46be0-470">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="46be0-471">如果代码未处理异常，则会看到一个错误页，如上一个屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="46be0-471">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="46be0-472">但 `Try/Catch` 部分可帮助防止用户看到这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="46be0-472">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="46be0-473">其他资源</span><span class="sxs-lookup"><span data-stu-id="46be0-473">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="46be0-474">参考文档</span><span class="sxs-lookup"><span data-stu-id="46be0-474">Reference Documentation</span></span>

- [<span data-ttu-id="46be0-475">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="46be0-475">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="46be0-476">Visual Basic 语言</span><span class="sxs-lookup"><span data-stu-id="46be0-476">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
