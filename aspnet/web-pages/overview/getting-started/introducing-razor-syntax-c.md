---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: 使用 Razor 语法的 ASP.NET Web 编程简介（C#） |Microsoft Docs
author: Rick-Anderson
description: 本章提供使用 Razor 语法对 ASP.NET 网页进行编程的概述。 ASP.NET 是 Microsoft 用于运行动态 web pa 的技术 。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564876"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="0363d-104">使用 Razor 语法的 ASP.NET Web 编程简介（C#）</span><span class="sxs-lookup"><span data-stu-id="0363d-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="0363d-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0363d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0363d-106">本文提供使用 Razor 语法对 ASP.NET 网页进行编程的概述。</span><span class="sxs-lookup"><span data-stu-id="0363d-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="0363d-107">ASP.NET 是 Microsoft 在 web 服务器上运行动态网页的技术。</span><span class="sxs-lookup"><span data-stu-id="0363d-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="0363d-108">本文重点介绍如何使用C#编程语言。</span><span class="sxs-lookup"><span data-stu-id="0363d-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="0363d-109">**你将学习的内容**：</span><span class="sxs-lookup"><span data-stu-id="0363d-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="0363d-110">使用 Razor 语法编程 ASP.NET 网页入门的前8个编程提示。</span><span class="sxs-lookup"><span data-stu-id="0363d-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="0363d-111">需要的基本编程概念。</span><span class="sxs-lookup"><span data-stu-id="0363d-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="0363d-112">什么是 ASP.NET 服务器代码和 Razor 语法都是如此。</span><span class="sxs-lookup"><span data-stu-id="0363d-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="0363d-113">软件版本</span><span class="sxs-lookup"><span data-stu-id="0363d-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="0363d-114">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="0363d-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="0363d-115">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="0363d-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="0363d-116">前8个编程提示</span><span class="sxs-lookup"><span data-stu-id="0363d-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="0363d-117">本部分列出了开始使用 Razor 语法编写 ASP.NET 服务器代码时需要了解的一些提示。</span><span class="sxs-lookup"><span data-stu-id="0363d-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="0363d-118">Razor 语法基于C#编程语言，这是 ASP.NET 网页最常使用的语言。</span><span class="sxs-lookup"><span data-stu-id="0363d-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="0363d-119">但 Razor 语法还支持 Visual Basic 语言，你所看到的所有内容也可以在 Visual Basic 中执行。</span><span class="sxs-lookup"><span data-stu-id="0363d-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="0363d-120">有关详细信息，请参阅附录[Visual Basic 语言和语法](https://go.microsoft.com/fwlink/?LinkId=202908)。</span><span class="sxs-lookup"><span data-stu-id="0363d-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>

<span data-ttu-id="0363d-121">可在本文后面的部分中找到有关这些编程技术的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="0363d-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="0363d-122">1. 使用 @ 字符将代码添加到页面</span><span class="sxs-lookup"><span data-stu-id="0363d-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="0363d-123">`@` 字符将启动内联表达式、单语句块和多语句块：</span><span class="sxs-lookup"><span data-stu-id="0363d-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="0363d-124">当页面在浏览器中运行时，这些语句如下所示：</span><span class="sxs-lookup"><span data-stu-id="0363d-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="0363d-126">**HTML 编码**</span><span class="sxs-lookup"><span data-stu-id="0363d-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="0363d-127">如前面的示例中所示，使用 `@` 字符显示页面中的内容时，ASP.NET 对输出进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="0363d-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="0363d-128">这会将保留 HTML 字符（如 `<` 和 `>` 和 `&`）替换为代码，使字符在网页中显示为字符，而不是解释为 HTML 标记或实体。</span><span class="sxs-lookup"><span data-stu-id="0363d-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="0363d-129">如果没有 HTML 编码，服务器代码的输出可能无法正确显示，并且可能会使页面面临安全风险。</span><span class="sxs-lookup"><span data-stu-id="0363d-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="0363d-130">如果你的目标是输出 HTML 标记，该标记将标记呈现为标记（例如，为段落 `<p></p>` 或 `<em></em>` 强调文本），请参阅本文后面的在[代码块中组合文本、标记和代码](#BM_CombiningTextMarkupAndCode)部分。</span><span class="sxs-lookup"><span data-stu-id="0363d-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="0363d-131">有关 HTML 编码的详细信息，请参阅[使用窗体](https://go.microsoft.com/fwlink/?LinkId=202892)。</span><span class="sxs-lookup"><span data-stu-id="0363d-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="0363d-132">2. 将代码块括在大括号中</span><span class="sxs-lookup"><span data-stu-id="0363d-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="0363d-133">*代码块*包含一个或多个代码语句，并括在大括号中。</span><span class="sxs-lookup"><span data-stu-id="0363d-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="0363d-134">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="0363d-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="0363d-136">3. 在块中，用分号结束每个代码语句</span><span class="sxs-lookup"><span data-stu-id="0363d-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="0363d-137">在代码块中，每个完整的代码语句必须以分号结束。</span><span class="sxs-lookup"><span data-stu-id="0363d-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="0363d-138">内联表达式不以分号结束。</span><span class="sxs-lookup"><span data-stu-id="0363d-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="0363d-139">4. 使用变量存储值</span><span class="sxs-lookup"><span data-stu-id="0363d-139">4. You use variables to store values</span></span>

<span data-ttu-id="0363d-140">可以将值存储在*变量*中，包括字符串、数字和日期等。使用 `var` 关键字创建新变量。</span><span class="sxs-lookup"><span data-stu-id="0363d-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="0363d-141">您可以使用 `@`直接在页面中插入变量值。</span><span class="sxs-lookup"><span data-stu-id="0363d-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="0363d-142">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="0363d-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="0363d-144">5. 将文字字符串值用双引号引起来</span><span class="sxs-lookup"><span data-stu-id="0363d-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="0363d-145">*字符串*是被视为文本的字符序列。</span><span class="sxs-lookup"><span data-stu-id="0363d-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="0363d-146">若要指定字符串，请用双引号将其引起来：</span><span class="sxs-lookup"><span data-stu-id="0363d-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="0363d-147">如果要显示的字符串包含反斜杠字符（`\`）或双引号（`"`），请使用以 `@` 运算符为前缀的*原义字符串文本*。</span><span class="sxs-lookup"><span data-stu-id="0363d-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="0363d-148">（在C#中，除非使用原义字符串文本，否则，\ 字符具有特殊意义。）</span><span class="sxs-lookup"><span data-stu-id="0363d-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="0363d-149">若要嵌入双引号，请使用原义字符串并重复引号：</span><span class="sxs-lookup"><span data-stu-id="0363d-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="0363d-150">下面是在页面中使用这两个示例的结果：</span><span class="sxs-lookup"><span data-stu-id="0363d-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="0363d-152">请注意，`@` 字符用于标记和中C#的原义字符串文本，以在 ASP.NET 页中标记代码。</span><span class="sxs-lookup"><span data-stu-id="0363d-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>

### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="0363d-153">6. 代码区分大小写</span><span class="sxs-lookup"><span data-stu-id="0363d-153">6. Code is case sensitive</span></span>

<span data-ttu-id="0363d-154">在C#中，关键字（如 `var`、`true`和 `if`）和变量名称区分大小写。</span><span class="sxs-lookup"><span data-stu-id="0363d-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="0363d-155">以下代码行创建两个不同的变量，`lastName` 和 `LastName.`</span><span class="sxs-lookup"><span data-stu-id="0363d-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="0363d-156">如果将变量声明为 `var lastName = "Smith";`，并尝试在页中将该变量作为 `@LastName`进行引用，则会 `"Jones"` 而不是 `"Smith"`来获取值。</span><span class="sxs-lookup"><span data-stu-id="0363d-156">If you declare a variable as `var lastName = "Smith";` and try to reference that variable in your page as `@LastName`, you would get the value `"Jones"` instead of `"Smith"`.</span></span>

> [!NOTE]
> <span data-ttu-id="0363d-157">在 Visual Basic 中，关键字和变量*不*区分大小写。</span><span class="sxs-lookup"><span data-stu-id="0363d-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>

### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="0363d-158">7. 您的大部分编码都涉及对象</span><span class="sxs-lookup"><span data-stu-id="0363d-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="0363d-159">*对象*表示您可以使用&#8212;页面、文本框、文件、图像、web 请求、电子邮件、客户记录（数据库行）等进行编程的内容。对象具有描述其特性的属性，并且您可以读取或更改&#8212;文本框对象具有 `Text` 属性（其他），请求对象具有 `Url` 属性，电子邮件具有 `From` 属性，而 customer 对象具有 `FirstName` 属性。</span><span class="sxs-lookup"><span data-stu-id="0363d-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="0363d-160">对象还具有可执行&quot; &quot;谓词的方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="0363d-161">示例包括文件对象的 `Save` 方法、图像对象的 `Rotate` 方法和电子邮件对象的 `Send` 方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="0363d-162">你通常会使用 `Request` 对象，该对象提供的信息类似于页面上文本框（窗体字段）的值、发出请求的浏览器的类型、页面的 URL、用户标识等。下面的示例演示如何访问 `Request` 对象的属性，以及如何调用 `Request` 对象的 `MapPath` 方法，这为你提供了服务器上页面的绝对路径：</span><span class="sxs-lookup"><span data-stu-id="0363d-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="0363d-163">浏览器中显示的结果：</span><span class="sxs-lookup"><span data-stu-id="0363d-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="0363d-165">8. 您可以编写代码来做出决策</span><span class="sxs-lookup"><span data-stu-id="0363d-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="0363d-166">动态网页的一项重要功能是，你可以根据条件确定要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="0363d-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="0363d-167">要执行此操作，最常见的方法是用 `if` 语句（和可选的 `else` 语句）。</span><span class="sxs-lookup"><span data-stu-id="0363d-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="0363d-168">语句 `if(IsPost)` 是编写 `if(IsPost == true)`的一种简便方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="0363d-169">除了 `if` 语句，还可以使用多种方法来测试条件、重复的代码块等，本文稍后将对此进行介绍。</span><span class="sxs-lookup"><span data-stu-id="0363d-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="0363d-170">在浏览器中显示的结果（在单击 "**提交**" 后）：</span><span class="sxs-lookup"><span data-stu-id="0363d-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="0363d-172">HTTP GET 和 POST 方法和 IsPost 属性</span><span class="sxs-lookup"><span data-stu-id="0363d-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="0363d-173">用于 web pages （HTTP）的协议支持用于向服务器发出请求的有限数量的方法（谓词）。</span><span class="sxs-lookup"><span data-stu-id="0363d-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="0363d-174">最常见的两个是 GET，用于读取页面，使用 POST 来提交页面。</span><span class="sxs-lookup"><span data-stu-id="0363d-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="0363d-175">通常，当用户第一次请求页面时，将使用 GET 请求页面。</span><span class="sxs-lookup"><span data-stu-id="0363d-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="0363d-176">如果用户填写表单，然后单击 "提交" 按钮，则浏览器向服务器发出 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="0363d-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="0363d-177">在 web 编程中，很有必要了解页面是否作为 GET 或 POST 请求，以便您知道如何处理页面。</span><span class="sxs-lookup"><span data-stu-id="0363d-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="0363d-178">在 ASP.NET 网页中，可以使用 `IsPost` 属性来查看请求是 GET 还是 POST。</span><span class="sxs-lookup"><span data-stu-id="0363d-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="0363d-179">如果请求是 POST，则 `IsPost` 属性将返回 true，您可以执行一些操作，例如读取窗体上的文本框的值。</span><span class="sxs-lookup"><span data-stu-id="0363d-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="0363d-180">你将看到的许多示例演示了如何根据 `IsPost`的值不同地处理页。</span><span class="sxs-lookup"><span data-stu-id="0363d-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="0363d-181">简单的代码示例</span><span class="sxs-lookup"><span data-stu-id="0363d-181">A Simple Code Example</span></span>

<span data-ttu-id="0363d-182">此过程说明如何创建一个说明基本编程技术的页面。</span><span class="sxs-lookup"><span data-stu-id="0363d-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="0363d-183">在此示例中，您将创建一个允许用户输入两个数字的页面，然后将其添加并显示结果。</span><span class="sxs-lookup"><span data-stu-id="0363d-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="0363d-184">在编辑器中，创建一个新文件并将其命名为*AddNumbers*。</span><span class="sxs-lookup"><span data-stu-id="0363d-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="0363d-185">将以下代码和标记复制到页面中，替换页面中已有的任何内容。</span><span class="sxs-lookup"><span data-stu-id="0363d-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="0363d-186">下面是要注意的一些事项：</span><span class="sxs-lookup"><span data-stu-id="0363d-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="0363d-187">`@` 字符将启动页面中的第一个代码块，并在嵌入到页面底部的 `totalMessage` 变量之前。</span><span class="sxs-lookup"><span data-stu-id="0363d-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="0363d-188">页面顶部的块括在大括号中。</span><span class="sxs-lookup"><span data-stu-id="0363d-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="0363d-189">在顶部的块中，所有行都以分号结束。</span><span class="sxs-lookup"><span data-stu-id="0363d-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="0363d-190">变量 `total`、`num1`、`num2`和 `totalMessage` 存储几个数字和一个字符串。</span><span class="sxs-lookup"><span data-stu-id="0363d-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="0363d-191">赋给 `totalMessage` 变量的文字字符串值用双引号引起来。</span><span class="sxs-lookup"><span data-stu-id="0363d-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="0363d-192">由于代码区分大小写，因此，当在页面底部附近使用 `totalMessage` 变量时，其名称必须完全匹配顶部的变量。</span><span class="sxs-lookup"><span data-stu-id="0363d-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="0363d-193">表达式 `num1.AsInt() + num2.AsInt()` 演示如何使用对象和方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="0363d-194">每个变量的 `AsInt` 方法将用户输入的字符串转换为数字（整数），以便您可以对其执行算术运算。</span><span class="sxs-lookup"><span data-stu-id="0363d-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="0363d-195">`<form>` 标记包含 `method="post"` 特性。</span><span class="sxs-lookup"><span data-stu-id="0363d-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="0363d-196">这指定在用户单击 "**添加**" 时，将使用 HTTP POST 方法将页发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="0363d-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="0363d-197">提交页面后，`if(IsPost)` 测试的计算结果为 true，并且运行条件代码，并显示添加数字的结果。</span><span class="sxs-lookup"><span data-stu-id="0363d-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="0363d-198">保存页面并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="0363d-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="0363d-199">（请确保在运行之前在 "**文件**" 工作区中选择了该页面。）输入两个整数，然后单击 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="0363d-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="0363d-201">基本编程概念</span><span class="sxs-lookup"><span data-stu-id="0363d-201">Basic Programming Concepts</span></span>

<span data-ttu-id="0363d-202">本文提供 ASP.NET web 编程的概述。</span><span class="sxs-lookup"><span data-stu-id="0363d-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="0363d-203">这并不是一种全面的调查，只是通过最常使用的编程概念的简要教程。</span><span class="sxs-lookup"><span data-stu-id="0363d-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="0363d-204">尽管如此，它还涵盖了开始 ASP.NET 网页所需的几乎所有内容。</span><span class="sxs-lookup"><span data-stu-id="0363d-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="0363d-205">但首先，这是一个很小的技术背景。</span><span class="sxs-lookup"><span data-stu-id="0363d-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="0363d-206">Razor 语法、服务器代码和 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0363d-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="0363d-207">Razor 语法是一种简单的编程语法，用于在网页中嵌入基于服务器的代码。</span><span class="sxs-lookup"><span data-stu-id="0363d-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="0363d-208">在使用 Razor 语法的网页中，有两种内容：客户端内容和服务器代码。</span><span class="sxs-lookup"><span data-stu-id="0363d-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="0363d-209">客户端内容是您在网页中使用的内容： HTML 标记（元素）、样式信息（如 CSS）或某些客户端脚本（如 JavaScript）和纯文本。</span><span class="sxs-lookup"><span data-stu-id="0363d-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="0363d-210">Razor 语法允许你将服务器代码添加到此客户端内容。</span><span class="sxs-lookup"><span data-stu-id="0363d-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="0363d-211">如果页中有服务器代码，则服务器会在将页发送到浏览器之前先运行该代码。</span><span class="sxs-lookup"><span data-stu-id="0363d-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="0363d-212">通过在服务器上运行，代码可以执行可能更复杂的任务，而不是使用客户端内容，如访问基于服务器的数据库。</span><span class="sxs-lookup"><span data-stu-id="0363d-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="0363d-213">最重要的是，服务器代码可以动态创建&#8212;客户端内容，它可以动态生成 HTML 标记或其他内容，然后将其连同页面可能包含的任何静态 HTML 一起发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="0363d-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="0363d-214">从浏览器的角度来看，服务器代码生成的客户端内容与任何其他客户端内容没有什么不同。</span><span class="sxs-lookup"><span data-stu-id="0363d-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="0363d-215">正如您所看到的，所需的服务器代码非常简单。</span><span class="sxs-lookup"><span data-stu-id="0363d-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="0363d-216">包含 Razor 语法的 ASP.NET 网页具有特殊的文件扩展名（*cshtml*或*vbhtml*）。</span><span class="sxs-lookup"><span data-stu-id="0363d-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="0363d-217">服务器可识别这些扩展，运行 Razor 语法标记的代码，然后将该页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="0363d-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="0363d-218">ASP.NET 适用于何处？</span><span class="sxs-lookup"><span data-stu-id="0363d-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="0363d-219">Razor 语法基于 Microsoft 中称为 ASP.NET 的技术，后者又基于 Microsoft .NET 框架。</span><span class="sxs-lookup"><span data-stu-id="0363d-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="0363d-220">The.NET 框架是 Microsoft 提供的一个大型综合性编程框架，用于开发几乎任何类型的计算机应用程序。</span><span class="sxs-lookup"><span data-stu-id="0363d-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="0363d-221">ASP.NET 是专门为创建 web 应用程序而设计的 .NET Framework 部分。</span><span class="sxs-lookup"><span data-stu-id="0363d-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="0363d-222">开发人员使用 ASP.NET 在世界各地创建了许多最大和最高的流量网站。</span><span class="sxs-lookup"><span data-stu-id="0363d-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="0363d-223">（只要你在站点中的 URL 中看到文件扩展名 *.aspx* ，你就会知道该站点是使用 ASP.NET 编写的。）</span><span class="sxs-lookup"><span data-stu-id="0363d-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="0363d-224">Razor 语法提供了 ASP.NET 的全部功能，但使用简化的语法，可以更方便地了解你是否是初级用户，如果你是一位专家，这会使你的工作效率更高。</span><span class="sxs-lookup"><span data-stu-id="0363d-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="0363d-225">尽管该语法很简单，但它与 ASP.NET 的系列关系 .NET Framework 也是如此，这意味着当您的网站变得更加复杂时，您可以使用更大的框架。</span><span class="sxs-lookup"><span data-stu-id="0363d-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="0363d-227">**类和实例**</span><span class="sxs-lookup"><span data-stu-id="0363d-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="0363d-228">ASP.NET 服务器代码使用对象，这些对象又基于类的概念而构建。</span><span class="sxs-lookup"><span data-stu-id="0363d-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="0363d-229">类是对象的定义或模板。</span><span class="sxs-lookup"><span data-stu-id="0363d-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="0363d-230">例如，应用程序可能包含一个 `Customer` 类，该类定义任何客户对象所需的属性和方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="0363d-231">当应用程序需要使用实际的客户信息时，它将创建一个客户对象的实例（或实例*化*）。</span><span class="sxs-lookup"><span data-stu-id="0363d-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="0363d-232">每个客户都是 `Customer` 类的单独实例。</span><span class="sxs-lookup"><span data-stu-id="0363d-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="0363d-233">每个实例都支持相同的属性和方法，但每个实例的属性值通常是不同的，因为每个客户对象都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="0363d-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="0363d-234">在一个客户对象中，`LastName` 属性可能为 "Smith";在另一个客户对象中，`LastName` 属性可能为 ""。</span><span class="sxs-lookup"><span data-stu-id="0363d-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="0363d-235">同样，您站点中的任何单个网页都是 `Page` 对象，它是 `Page` 类的实例。</span><span class="sxs-lookup"><span data-stu-id="0363d-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="0363d-236">页面上的按钮是 `Button` 对象，它是 `Button` 类的实例等。</span><span class="sxs-lookup"><span data-stu-id="0363d-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="0363d-237">每个实例都有其自身的特征，但它们都基于对象的类定义中指定的内容。</span><span class="sxs-lookup"><span data-stu-id="0363d-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>

## <a name="basic-syntax"></a><span data-ttu-id="0363d-238">基本语法</span><span class="sxs-lookup"><span data-stu-id="0363d-238">Basic Syntax</span></span>

<span data-ttu-id="0363d-239">前面部分介绍了如何创建 ASP.NET 网页页，以及如何将服务器代码添加到 HTML 标记的基本示例。</span><span class="sxs-lookup"><span data-stu-id="0363d-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="0363d-240">在这里，你将学习使用 Razor 语法&#8212; （即编程语言规则）编写 ASP.NET 服务器代码的基础知识。</span><span class="sxs-lookup"><span data-stu-id="0363d-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="0363d-241">如果你使用的是编程（尤其是在使用 C、 C++、 C#、Visual Basic 或 JavaScript）的情况下，你将会熟悉此处所述的大部分内容。</span><span class="sxs-lookup"><span data-stu-id="0363d-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="0363d-242">您可能只需要熟悉如何将服务器代码添加到*cshtml*文件中的标记。</span><span class="sxs-lookup"><span data-stu-id="0363d-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="0363d-243">在代码块中组合文本、标记和代码</span><span class="sxs-lookup"><span data-stu-id="0363d-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="0363d-244">在服务器代码块中，通常需要将文本或标记（或两者）输出到页面。</span><span class="sxs-lookup"><span data-stu-id="0363d-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="0363d-245">如果服务器代码块包含不是代码的文本，而应按原样呈现，则 ASP.NET 需要能够区分该文本与代码。</span><span class="sxs-lookup"><span data-stu-id="0363d-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="0363d-246">有若干方法可实现此操作。</span><span class="sxs-lookup"><span data-stu-id="0363d-246">There are several ways to do this.</span></span>

- <span data-ttu-id="0363d-247">将文本括在 HTML 元素中，如 `<p></p>` 或 `<em></em>`：</span><span class="sxs-lookup"><span data-stu-id="0363d-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="0363d-248">HTML 元素可以包括文本、附加 HTML 元素和服务器代码表达式。</span><span class="sxs-lookup"><span data-stu-id="0363d-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="0363d-249">当 ASP.NET 查看开始 HTML 标记（例如 `<p>`）时，它会将所有内容（包括元素）和其内容呈现为浏览器，并在服务器代码表达式发生时进行解析。</span><span class="sxs-lookup"><span data-stu-id="0363d-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="0363d-250">使用 `@:` 运算符或 `<text>` 元素。</span><span class="sxs-lookup"><span data-stu-id="0363d-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="0363d-251">`@:` 输出包含纯文本或不匹配 HTML 标记的单个行内容;`<text>` 元素包含多个要输出的行。</span><span class="sxs-lookup"><span data-stu-id="0363d-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="0363d-252">如果您不希望在输出过程中呈现 HTML 元素，则这些选项非常有用。</span><span class="sxs-lookup"><span data-stu-id="0363d-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="0363d-253">如果要输出多行文本或不匹配的 HTML 标记，则可以在每行的前面加 `@:`，也可以在 `<text>` 元素中包含行。</span><span class="sxs-lookup"><span data-stu-id="0363d-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="0363d-254">与 `@:` 运算符一样，ASP.NET 使用`<text>` 标记来标识文本内容，而不会在页输出中呈现。</span><span class="sxs-lookup"><span data-stu-id="0363d-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="0363d-255">第一个示例重复前面的示例，但使用一对 `<text>` 标记来包含要呈现的文本。</span><span class="sxs-lookup"><span data-stu-id="0363d-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="0363d-256">在第二个示例中，"`<text>`" 和 "`</text>`" 标记包含三行，其中所有行都包含一些非包含文本和匹配的 HTML 标记（`<br />`）以及服务器代码和匹配的 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="0363d-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="0363d-257">同样，您还可以在每行的前面加上 `@:` 运算符;这两种方法都适用。</span><span class="sxs-lookup"><span data-stu-id="0363d-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0363d-258">使用 HTML 元素输出此部分&#8212;中所示的文本时，`@:` 运算符或 `<text>` 元素&#8212; ASP.NET 不会对输出进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="0363d-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="0363d-259">（如前文所述，ASP.NET 会对前面是 `@`的服务器代码表达式和服务器代码块的输出进行编码，但本部分中所述的特殊情况除外。</span><span class="sxs-lookup"><span data-stu-id="0363d-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="0363d-260">Whitespace</span><span class="sxs-lookup"><span data-stu-id="0363d-260">Whitespace</span></span>

<span data-ttu-id="0363d-261">语句中的多余空格（字符串文字外）不会影响语句：</span><span class="sxs-lookup"><span data-stu-id="0363d-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="0363d-262">语句中的换行符对语句没有影响，您可以包装语句以便于阅读。</span><span class="sxs-lookup"><span data-stu-id="0363d-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="0363d-263">下列语句相同：</span><span class="sxs-lookup"><span data-stu-id="0363d-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="0363d-264">但是，不能在字符串文字的中间换行。</span><span class="sxs-lookup"><span data-stu-id="0363d-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="0363d-265">下面的示例不起作用：</span><span class="sxs-lookup"><span data-stu-id="0363d-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="0363d-266">若要将换行的长字符串与以上代码中的多个行合并，有两个选项。</span><span class="sxs-lookup"><span data-stu-id="0363d-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="0363d-267">可以使用串联运算符（`+`），稍后将在本文中看到。</span><span class="sxs-lookup"><span data-stu-id="0363d-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="0363d-268">你还可以使用 `@` 字符创建原义字符串，如本文前面所述。</span><span class="sxs-lookup"><span data-stu-id="0363d-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="0363d-269">可以跨行中断原义字符串文本：</span><span class="sxs-lookup"><span data-stu-id="0363d-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="0363d-270">代码（和标记）注释</span><span class="sxs-lookup"><span data-stu-id="0363d-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="0363d-271">您可以为自己或其他人留言。</span><span class="sxs-lookup"><span data-stu-id="0363d-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="0363d-272">它们还允许您禁用（*注释掉*）您不想运行但要在页面中保留的代码或标记的部分。</span><span class="sxs-lookup"><span data-stu-id="0363d-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="0363d-273">Razor 代码和 HTML 标记有不同的注释语法。</span><span class="sxs-lookup"><span data-stu-id="0363d-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="0363d-274">与所有 Razor 代码一样，在将页发送到浏览器之前，将在服务器上处理并删除 Razor 注释。</span><span class="sxs-lookup"><span data-stu-id="0363d-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="0363d-275">因此，Razor 注释语法使你可以将注释添加到代码中（甚至是标记中），你可以在编辑文件时查看这些注释，但即使在页面源中也不会看到。</span><span class="sxs-lookup"><span data-stu-id="0363d-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="0363d-276">对于 ASP.NET Razor 注释，会开始 `@*` 注释，并通过 `*@`结束。</span><span class="sxs-lookup"><span data-stu-id="0363d-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="0363d-277">注释可以在一行或多行上：</span><span class="sxs-lookup"><span data-stu-id="0363d-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="0363d-278">下面是代码块中的注释：</span><span class="sxs-lookup"><span data-stu-id="0363d-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="0363d-279">下面是相同的代码块，代码行已注释掉，因此无法运行：</span><span class="sxs-lookup"><span data-stu-id="0363d-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="0363d-280">在代码块内，作为使用 Razor 注释语法的替代方法，你可以使用所使用的编程语言的注释语法，例如C#：</span><span class="sxs-lookup"><span data-stu-id="0363d-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="0363d-281">在C#中，单行注释前面带有 `//` 字符，多行注释以 `/*` 开头，并以 `*/`结尾。</span><span class="sxs-lookup"><span data-stu-id="0363d-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="0363d-282">（与 Razor 注释一样， C#注释不会呈现给浏览器。）</span><span class="sxs-lookup"><span data-stu-id="0363d-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="0363d-283">对于标记，你可能知道，可以创建 HTML 注释：</span><span class="sxs-lookup"><span data-stu-id="0363d-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="0363d-284">HTML 注释从 `<!--` 字符开始，以 `-->`结束。</span><span class="sxs-lookup"><span data-stu-id="0363d-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="0363d-285">您可以使用 HTML 注释来包围文本，还可以使用任何 HTML 标记（您可能希望在页面中保留，但不希望呈现）。</span><span class="sxs-lookup"><span data-stu-id="0363d-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="0363d-286">此 HTML 注释将隐藏标记的全部内容及其包含的文本：</span><span class="sxs-lookup"><span data-stu-id="0363d-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="0363d-287">与 Razor 注释不同，HTML*注释呈现*到页面，用户可以通过查看页面源来查看这些注释。</span><span class="sxs-lookup"><span data-stu-id="0363d-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="0363d-288">Razor 的嵌套块有限制C#。</span><span class="sxs-lookup"><span data-stu-id="0363d-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="0363d-289">有关详细信息[，请C#参阅命名变量和嵌套块生成损坏的代码](http://aspnetwebstack.codeplex.com/workitem/1914)</span><span class="sxs-lookup"><span data-stu-id="0363d-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="0363d-290">变量</span><span class="sxs-lookup"><span data-stu-id="0363d-290">Variables</span></span>

<span data-ttu-id="0363d-291">变量是用于存储数据的命名对象。</span><span class="sxs-lookup"><span data-stu-id="0363d-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="0363d-292">您可以将变量命名为任何名称，但该名称必须以字母字符开头且不能包含空格或保留字符。</span><span class="sxs-lookup"><span data-stu-id="0363d-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="0363d-293">变量和数据类型</span><span class="sxs-lookup"><span data-stu-id="0363d-293">Variables and Data Types</span></span>

<span data-ttu-id="0363d-294">变量可以具有特定的数据类型，用于指示变量中存储的数据类型。</span><span class="sxs-lookup"><span data-stu-id="0363d-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="0363d-295">可以有存储字符串值（如 &quot;Hello world&quot;）的字符串变量、存储整数值的整数变量（例如3或79）以及以多种格式存储日期值的日期变量（如4/12/2012 或3月2009）。</span><span class="sxs-lookup"><span data-stu-id="0363d-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="0363d-296">还可以使用许多其他数据类型。</span><span class="sxs-lookup"><span data-stu-id="0363d-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="0363d-297">但是，您通常不需要为变量指定类型。</span><span class="sxs-lookup"><span data-stu-id="0363d-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="0363d-298">大多数情况下，ASP.NET 可以根据变量中数据的使用方式来确定类型。</span><span class="sxs-lookup"><span data-stu-id="0363d-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="0363d-299">（有时您必须指定一个类型，您将看到这样的示例。）</span><span class="sxs-lookup"><span data-stu-id="0363d-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="0363d-300">使用 `var` 关键字声明一个变量（如果不希望指定类型）或使用该类型的名称：</span><span class="sxs-lookup"><span data-stu-id="0363d-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="0363d-301">下面的示例演示了网页中变量的一些典型用法：</span><span class="sxs-lookup"><span data-stu-id="0363d-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="0363d-302">如果将前面的示例组合到页面中，则会看到此显示在浏览器中：</span><span class="sxs-lookup"><span data-stu-id="0363d-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="0363d-304">转换和测试数据类型</span><span class="sxs-lookup"><span data-stu-id="0363d-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="0363d-305">尽管 ASP.NET 通常可以自动确定数据类型，但有时不能。</span><span class="sxs-lookup"><span data-stu-id="0363d-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="0363d-306">因此，您可能需要通过执行显式转换来帮助 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="0363d-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="0363d-307">即使您不需要转换类型，有时也可以通过测试来查看您可能使用的数据类型。</span><span class="sxs-lookup"><span data-stu-id="0363d-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="0363d-308">最常见的情况是必须将字符串转换为其他类型，例如整数或日期。</span><span class="sxs-lookup"><span data-stu-id="0363d-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="0363d-309">下面的示例演示一个典型情况，您必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="0363d-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="0363d-310">作为一种规则，用户输入作为字符串提供给你。</span><span class="sxs-lookup"><span data-stu-id="0363d-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="0363d-311">即使您已提示用户输入一个数字，甚至输入了一个数字，在提交用户输入并在代码中读取它时，数据仍采用字符串格式。</span><span class="sxs-lookup"><span data-stu-id="0363d-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="0363d-312">因此，必须将字符串转换为数字。</span><span class="sxs-lookup"><span data-stu-id="0363d-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="0363d-313">在此示例中，如果你尝试对值执行算术运算而不转换这些值，则会产生以下错误，因为 ASP.NET 无法添加两个字符串：</span><span class="sxs-lookup"><span data-stu-id="0363d-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="0363d-314">*无法将类型 "string" 隐式转换为 "int"。*</span><span class="sxs-lookup"><span data-stu-id="0363d-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="0363d-315">若要将值转换为整数，请调用 `AsInt` 方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="0363d-316">如果转换成功，则可以添加数字。</span><span class="sxs-lookup"><span data-stu-id="0363d-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="0363d-317">下表列出了一些常见的变量转换方法和测试方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="0363d-318"><strong>方法</strong></span><span class="sxs-lookup"><span data-stu-id="0363d-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-319"><strong>描述</strong></span><span class="sxs-lookup"><span data-stu-id="0363d-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-320"><strong>示例</strong></span><span class="sxs-lookup"><span data-stu-id="0363d-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-321">将表示整数的字符串（如 "593"）转换为整数。</span><span class="sxs-lookup"><span data-stu-id="0363d-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-322">将字符串（如 &quot;true&quot; 或 &quot;false&quot; 转换为布尔类型。</span><span class="sxs-lookup"><span data-stu-id="0363d-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-323">将具有十进制值（如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字符串转换为浮点数。</span><span class="sxs-lookup"><span data-stu-id="0363d-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-324">将具有十进制值（如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字符串转换为十进制数字。</span><span class="sxs-lookup"><span data-stu-id="0363d-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="0363d-325">（在 ASP.NET 中，小数比浮点数更精确。）</span><span class="sxs-lookup"><span data-stu-id="0363d-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-326">将表示日期和时间值的字符串转换为 ASP.NET `DateTime` 类型。</span><span class="sxs-lookup"><span data-stu-id="0363d-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-327">将任何其他数据类型转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="0363d-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="0363d-328">运算符</span><span class="sxs-lookup"><span data-stu-id="0363d-328">Operators</span></span>

<span data-ttu-id="0363d-329">运算符是一个关键字或字符，用于告知 ASP.NET 要在表达式中执行哪种类型的命令。</span><span class="sxs-lookup"><span data-stu-id="0363d-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="0363d-330">C#语言（以及基于它的 Razor 语法）支持许多运算符，但你只需要识别几个运算符即可开始使用。</span><span class="sxs-lookup"><span data-stu-id="0363d-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="0363d-331">下表总结了最常见的运算符。</span><span class="sxs-lookup"><span data-stu-id="0363d-331">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="0363d-332"><strong>Operator</strong></span><span class="sxs-lookup"><span data-stu-id="0363d-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-333"><strong>描述</strong></span><span class="sxs-lookup"><span data-stu-id="0363d-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-334"><strong>示例</strong></span><span class="sxs-lookup"><span data-stu-id="0363d-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="0363d-335">`+` `-` `*` `/`</span><span class="sxs-lookup"><span data-stu-id="0363d-335">`+` `-` `*` `/`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-336">数值表达式中使用的数学运算符。</span><span class="sxs-lookup"><span data-stu-id="0363d-336">Math operators used in numerical expressions.</span></span>
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-337">赋值。</span><span class="sxs-lookup"><span data-stu-id="0363d-337">Assignment.</span></span> <span data-ttu-id="0363d-338">将语句右侧的值分配给左侧的对象。</span><span class="sxs-lookup"><span data-stu-id="0363d-338">Assigns the value on the right side of a statement to the object on the left side.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-339">相等。</span><span class="sxs-lookup"><span data-stu-id="0363d-339">Equality.</span></span> <span data-ttu-id="0363d-340">如果值相等，则返回 `true`。</span><span class="sxs-lookup"><span data-stu-id="0363d-340">Returns `true` if the values are equal.</span></span> <span data-ttu-id="0363d-341">（请注意 `=` 运算符与 `==` 运算符之间的区别。）</span><span class="sxs-lookup"><span data-stu-id="0363d-341">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-342">不相等。</span><span class="sxs-lookup"><span data-stu-id="0363d-342">Inequality.</span></span> <span data-ttu-id="0363d-343">如果值不相等，则返回 `true`。</span><span class="sxs-lookup"><span data-stu-id="0363d-343">Returns `true` if the values are not equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-344">小于、大于、小于等于、等于、大于等于或大于或等于。</span><span class="sxs-lookup"><span data-stu-id="0363d-344">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-345">串联，用于联接字符串。</span><span class="sxs-lookup"><span data-stu-id="0363d-345">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="0363d-346">ASP.NET 根据表达式的数据类型知道此运算符与加法运算符之间的差异。</span><span class="sxs-lookup"><span data-stu-id="0363d-346">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="0363d-347">`+=` `-=`</span><span class="sxs-lookup"><span data-stu-id="0363d-347">`+=` `-=`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-348">递增和递减运算符，它们分别增加和减少1。</span><span class="sxs-lookup"><span data-stu-id="0363d-348">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-349">着重号.</span><span class="sxs-lookup"><span data-stu-id="0363d-349">Dot.</span></span> <span data-ttu-id="0363d-350">用于区分对象及其属性和方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-350">Used to distinguish objects and their properties and methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-351">括号.</span><span class="sxs-lookup"><span data-stu-id="0363d-351">Parentheses.</span></span> <span data-ttu-id="0363d-352">用于对表达式分组并将参数传递给方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-352">Used to group expressions and to pass parameters to methods.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-353">方括号.</span><span class="sxs-lookup"><span data-stu-id="0363d-353">Brackets.</span></span> <span data-ttu-id="0363d-354">用于访问数组或集合中的值。</span><span class="sxs-lookup"><span data-stu-id="0363d-354">Used for accessing values in arrays or collections.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-355">不仅.</span><span class="sxs-lookup"><span data-stu-id="0363d-355">Not.</span></span> <span data-ttu-id="0363d-356">反转 `true` 值为 `false`，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="0363d-356">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="0363d-357">通常用作测试 `false` （即，不 `true`）的一种简便方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-357">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="0363d-358">`&&` `||`</span><span class="sxs-lookup"><span data-stu-id="0363d-358">`&&` `||`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="0363d-359">逻辑 "与" 或 "或"，用于将条件链接在一起。</span><span class="sxs-lookup"><span data-stu-id="0363d-359">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="0363d-360">处理代码中的文件和文件夹路径</span><span class="sxs-lookup"><span data-stu-id="0363d-360">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="0363d-361">通常会在代码中使用文件和文件夹路径。</span><span class="sxs-lookup"><span data-stu-id="0363d-361">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="0363d-362">下面是网站的物理文件夹结构示例，因为它可能出现在开发计算机上：</span><span class="sxs-lookup"><span data-stu-id="0363d-362">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="0363d-363">下面是有关 Url 和路径的一些基本详细信息：</span><span class="sxs-lookup"><span data-stu-id="0363d-363">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="0363d-364">URL 以域名（`http://www.example.com`）或服务器名称（`http://localhost`，`http://mycomputer`）开头。</span><span class="sxs-lookup"><span data-stu-id="0363d-364">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="0363d-365">URL 对应于主计算机上的物理路径。</span><span class="sxs-lookup"><span data-stu-id="0363d-365">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="0363d-366">例如，`http://myserver` 可能对应于服务器上的*C:\websites\mywebsite*文件夹。</span><span class="sxs-lookup"><span data-stu-id="0363d-366">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="0363d-367">虚拟路径是在代码中表示路径的速记，无需指定完整路径。</span><span class="sxs-lookup"><span data-stu-id="0363d-367">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="0363d-368">它包括位于域或服务器名称后面的 URL 部分。</span><span class="sxs-lookup"><span data-stu-id="0363d-368">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="0363d-369">使用虚拟路径时，可以将代码移到不同的域或服务器上，而无需更新路径。</span><span class="sxs-lookup"><span data-stu-id="0363d-369">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="0363d-370">下面是一个示例，可帮助你了解不同之处：</span><span class="sxs-lookup"><span data-stu-id="0363d-370">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="0363d-371">完成 URL</span><span class="sxs-lookup"><span data-stu-id="0363d-371">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="0363d-372">服务器名称</span><span class="sxs-lookup"><span data-stu-id="0363d-372">Server name</span></span> | <span data-ttu-id="0363d-373">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="0363d-373">*mycompanyserver*</span></span> |
| <span data-ttu-id="0363d-374">虚拟路径</span><span class="sxs-lookup"><span data-stu-id="0363d-374">Virtual path</span></span> | <span data-ttu-id="0363d-375">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="0363d-375">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="0363d-376">物理路径</span><span class="sxs-lookup"><span data-stu-id="0363d-376">Physical path</span></span> | <span data-ttu-id="0363d-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="0363d-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="0363d-378">虚拟根目录为/，正如 C：驱动器的根目录为 \。</span><span class="sxs-lookup"><span data-stu-id="0363d-378">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="0363d-379">（虚拟文件夹路径始终使用正斜杠。）文件夹的虚拟路径不必与物理文件夹同名;它可以是别名。</span><span class="sxs-lookup"><span data-stu-id="0363d-379">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="0363d-380">（在生产服务器上，虚拟路径很少匹配确切的物理路径。）</span><span class="sxs-lookup"><span data-stu-id="0363d-380">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="0363d-381">当你在代码中处理文件和文件夹时，有时需要引用物理路径，有时还需要引用虚拟路径，具体取决于你使用的对象。</span><span class="sxs-lookup"><span data-stu-id="0363d-381">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="0363d-382">ASP.NET 提供了以下工具来处理代码中的文件和文件夹路径： `Server.MapPath` 方法、`~` 运算符和 `Href` 方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-382">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="0363d-383">将虚拟路径转换为物理路径：服务器. MapPath 方法</span><span class="sxs-lookup"><span data-stu-id="0363d-383">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="0363d-384">`Server.MapPath` 方法将虚拟路径（如 */default.cshtml*）转换为绝对物理路径（如*C:\WebSites\MyWebSiteFolder\default.cshtml*）。</span><span class="sxs-lookup"><span data-stu-id="0363d-384">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="0363d-385">任何时候都需要完整的物理路径时，可以使用此方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-385">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="0363d-386">典型的示例是在 web 服务器上读取或写入文本文件或图像文件时。</span><span class="sxs-lookup"><span data-stu-id="0363d-386">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="0363d-387">您通常不知道站点在宿主站点的服务器上的绝对物理路径，因此此方法可以将您知道的路径（虚拟路径）转换为服务器上的相应路径。</span><span class="sxs-lookup"><span data-stu-id="0363d-387">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="0363d-388">将文件或文件夹的虚拟路径传递给方法，并返回物理路径：</span><span class="sxs-lookup"><span data-stu-id="0363d-388">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="0363d-389">引用虚拟根： ~ operator 和 Href 方法</span><span class="sxs-lookup"><span data-stu-id="0363d-389">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="0363d-390">在*cshtml*或*vbhtml*文件中，可以使用 `~` 运算符引用虚拟根路径。</span><span class="sxs-lookup"><span data-stu-id="0363d-390">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="0363d-391">这非常方便，因为您可以在站点中移动页面，并且任何包含到其他页面的链接都不会损坏。</span><span class="sxs-lookup"><span data-stu-id="0363d-391">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="0363d-392">如果你将网站移到其他位置，也可以方便地使用它。</span><span class="sxs-lookup"><span data-stu-id="0363d-392">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="0363d-393">下面是一些可能的恶意活动：</span><span class="sxs-lookup"><span data-stu-id="0363d-393">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="0363d-394">如果网站 `http://myserver/myapp`，以下是在页面运行时 ASP.NET 将如何处理这些路径：</span><span class="sxs-lookup"><span data-stu-id="0363d-394">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="0363d-395">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="0363d-395">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="0363d-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="0363d-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="0363d-397">（实际上，您不会看到这些路径作为变量的值，而 ASP.NET 会将这些路径视为它们。）</span><span class="sxs-lookup"><span data-stu-id="0363d-397">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="0363d-398">可以在服务器代码（如上所示）和标记中使用 `~` 运算符，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0363d-398">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="0363d-399">在标记中，使用 `~` 运算符来创建资源的路径，如图像文件、其他网页和 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="0363d-399">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="0363d-400">当该页运行时，ASP.NET 将浏览该页（代码和标记），并将所有 `~` 引用解析为相应的路径。</span><span class="sxs-lookup"><span data-stu-id="0363d-400">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="0363d-401">条件逻辑和循环</span><span class="sxs-lookup"><span data-stu-id="0363d-401">Conditional Logic and Loops</span></span>

<span data-ttu-id="0363d-402">通过 ASP.NET 服务器代码，你可以根据条件执行任务，并编写代码，将语句重复指定次数（即运行循环的代码）。</span><span class="sxs-lookup"><span data-stu-id="0363d-402">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="0363d-403">测试条件</span><span class="sxs-lookup"><span data-stu-id="0363d-403">Testing Conditions</span></span>

<span data-ttu-id="0363d-404">若要测试简单的条件，请使用 `if` 语句，该语句根据指定的测试返回 true 或 false：</span><span class="sxs-lookup"><span data-stu-id="0363d-404">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="0363d-405">`if` 关键字启动块。</span><span class="sxs-lookup"><span data-stu-id="0363d-405">The `if` keyword starts a block.</span></span> <span data-ttu-id="0363d-406">实际测试（条件）位于括号中，并返回 true 或 false。</span><span class="sxs-lookup"><span data-stu-id="0363d-406">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="0363d-407">如果测试为 true，则运行的语句括在大括号中。</span><span class="sxs-lookup"><span data-stu-id="0363d-407">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="0363d-408">`if` 语句可以包括指定语句的 `else` 块，条件为 false 时运行：</span><span class="sxs-lookup"><span data-stu-id="0363d-408">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="0363d-409">您可以使用 `else if` 块添加多个条件：</span><span class="sxs-lookup"><span data-stu-id="0363d-409">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="0363d-410">在此示例中，如果 if 块中的第一个条件不为 true，则选中 `else if` 条件。</span><span class="sxs-lookup"><span data-stu-id="0363d-410">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="0363d-411">如果满足该条件，则执行 `else if` 块中的语句。</span><span class="sxs-lookup"><span data-stu-id="0363d-411">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="0363d-412">如果未满足任何条件，则执行 `else` 块中的语句。</span><span class="sxs-lookup"><span data-stu-id="0363d-412">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="0363d-413">你可以添加任意数量的 else if block，然后使用 `else` 块关闭，因为 &quot;所有其他&quot; 条件。</span><span class="sxs-lookup"><span data-stu-id="0363d-413">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="0363d-414">若要测试大量条件，请使用 `switch` 块：</span><span class="sxs-lookup"><span data-stu-id="0363d-414">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="0363d-415">要测试的值位于括号内（在本例中为 `weekday` 变量）。</span><span class="sxs-lookup"><span data-stu-id="0363d-415">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="0363d-416">每个单独的测试都使用以冒号（:) 结尾的 `case` 语句。</span><span class="sxs-lookup"><span data-stu-id="0363d-416">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="0363d-417">如果 `case` 语句的值与测试值匹配，则将执行该 case 块中的代码。</span><span class="sxs-lookup"><span data-stu-id="0363d-417">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="0363d-418">使用 `break` 语句关闭每个 case 语句。</span><span class="sxs-lookup"><span data-stu-id="0363d-418">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="0363d-419">（如果忘记在每个 `case` 块中包含 break，则下一 `case` 语句中的代码也会运行。）`switch` 块通常将 `default` 语句作为 &quot;所有其他情况下运行&quot; 选项的最后一种情况。</span><span class="sxs-lookup"><span data-stu-id="0363d-419">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="0363d-420">在浏览器中显示的最后两个条件块的结果：</span><span class="sxs-lookup"><span data-stu-id="0363d-420">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="0363d-422">循环代码</span><span class="sxs-lookup"><span data-stu-id="0363d-422">Looping Code</span></span>

<span data-ttu-id="0363d-423">经常需要重复运行相同的语句。</span><span class="sxs-lookup"><span data-stu-id="0363d-423">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="0363d-424">通过循环执行此操作。</span><span class="sxs-lookup"><span data-stu-id="0363d-424">You do this by looping.</span></span> <span data-ttu-id="0363d-425">例如，通常对数据集合中的每个项运行相同的语句。</span><span class="sxs-lookup"><span data-stu-id="0363d-425">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="0363d-426">如果确切知道要循环多少次，则可以使用 `for` 循环。</span><span class="sxs-lookup"><span data-stu-id="0363d-426">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="0363d-427">此类循环特别适用于计算或计数：</span><span class="sxs-lookup"><span data-stu-id="0363d-427">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="0363d-428">循环以 `for` 关键字开头，后跟括在括号中的三个语句，每个语句用分号结束。</span><span class="sxs-lookup"><span data-stu-id="0363d-428">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="0363d-429">在括号内，第一个语句（`var i=10;`）会创建一个计数器，并将其初始化为10。</span><span class="sxs-lookup"><span data-stu-id="0363d-429">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="0363d-430">无需命名计数器 `i` &#8212;可以使用任何变量。</span><span class="sxs-lookup"><span data-stu-id="0363d-430">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="0363d-431">`for` 循环运行时，计数器会自动递增。</span><span class="sxs-lookup"><span data-stu-id="0363d-431">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="0363d-432">第二个语句（`i < 21;`）设置要计数的条件。</span><span class="sxs-lookup"><span data-stu-id="0363d-432">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="0363d-433">在这种情况下，你希望其最大值为20（即，在计数器小于21的情况下继续）。</span><span class="sxs-lookup"><span data-stu-id="0363d-433">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="0363d-434">第三个语句（`i++`）使用增量运算符，该运算符仅指定在每次循环运行时应将计数器添加1。</span><span class="sxs-lookup"><span data-stu-id="0363d-434">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="0363d-435">大括号内是将为循环的每次迭代运行的代码。</span><span class="sxs-lookup"><span data-stu-id="0363d-435">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="0363d-436">标记每次创建一个新段落（`<p>` 元素），并在输出中添加一行，并显示 `i` （计数器）的值。</span><span class="sxs-lookup"><span data-stu-id="0363d-436">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="0363d-437">运行此页时，此示例将创建11行显示输出，每行中的文本指示项号。</span><span class="sxs-lookup"><span data-stu-id="0363d-437">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="0363d-439">如果使用的是集合或数组，通常使用 `foreach` 循环。</span><span class="sxs-lookup"><span data-stu-id="0363d-439">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="0363d-440">集合是一组类似的对象，而 `foreach` 循环使你可以对集合中的每个项执行一个任务。</span><span class="sxs-lookup"><span data-stu-id="0363d-440">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="0363d-441">这种类型的循环非常适合于回收，因为与 `for` 循环不同，您不必递增计数器或设置限制。</span><span class="sxs-lookup"><span data-stu-id="0363d-441">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="0363d-442">相反，`foreach` 循环代码只需经过回收，直到完成。</span><span class="sxs-lookup"><span data-stu-id="0363d-442">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="0363d-443">例如，下面的代码返回 `Request.ServerVariables` 集合中的项，这是一个包含有关 web 服务器的信息的对象。</span><span class="sxs-lookup"><span data-stu-id="0363d-443">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="0363d-444">它通过在 HTML 项目符号列表中创建一个新的 `<li>` 元素，使用 `foreac` h 循环来显示每个项的名称。</span><span class="sxs-lookup"><span data-stu-id="0363d-444">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="0363d-445">`foreach` 关键字后跟括号，在此括号中，你可以声明一个表示集合中单个项的变量（在本例中为 `var item`），后跟 `in` 关键字，后跟要循环访问的集合。</span><span class="sxs-lookup"><span data-stu-id="0363d-445">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="0363d-446">在 `foreach` 循环的主体中，可以使用之前声明的变量访问当前项。</span><span class="sxs-lookup"><span data-stu-id="0363d-446">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="0363d-448">若要创建更通用的循环，请使用 `while` 语句：</span><span class="sxs-lookup"><span data-stu-id="0363d-448">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="0363d-449">`while` 循环以 `while` 关键字开头，后跟括号，可在其中指定循环的持续时间（在此之后，只要 `countNum` 小于50），就会重复执行块。</span><span class="sxs-lookup"><span data-stu-id="0363d-449">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="0363d-450">循环通常会递增（添加到）或递减（减去）用于计数的变量或对象。</span><span class="sxs-lookup"><span data-stu-id="0363d-450">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="0363d-451">在此示例中，每次循环运行时，`+=` 运算符都 `countNum` 加1。</span><span class="sxs-lookup"><span data-stu-id="0363d-451">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="0363d-452">（若要减小循环中计算的变量，请使用减量运算符 `-=`）。</span><span class="sxs-lookup"><span data-stu-id="0363d-452">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="0363d-453">对象和集合</span><span class="sxs-lookup"><span data-stu-id="0363d-453">Objects and Collections</span></span>

<span data-ttu-id="0363d-454">ASP.NET 网站中的几乎所有内容都是一个对象，包括网页本身。</span><span class="sxs-lookup"><span data-stu-id="0363d-454">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="0363d-455">本部分讨论你将经常在代码中使用的一些重要对象。</span><span class="sxs-lookup"><span data-stu-id="0363d-455">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="0363d-456">页面对象</span><span class="sxs-lookup"><span data-stu-id="0363d-456">Page Objects</span></span>

<span data-ttu-id="0363d-457">ASP.NET 中的最基本对象是页面。</span><span class="sxs-lookup"><span data-stu-id="0363d-457">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="0363d-458">您可以直接访问 page 对象的属性，而无需任何合格的对象。</span><span class="sxs-lookup"><span data-stu-id="0363d-458">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="0363d-459">下面的代码使用页面的 `Request` 对象获取页面的文件路径：</span><span class="sxs-lookup"><span data-stu-id="0363d-459">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="0363d-460">若要清楚地说您在当前 page 对象上引用属性和方法，您可以选择使用关键字 `this` 在代码中表示 page 对象。</span><span class="sxs-lookup"><span data-stu-id="0363d-460">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="0363d-461">下面是上面的代码示例，其中添加了 `this` 以表示页面：</span><span class="sxs-lookup"><span data-stu-id="0363d-461">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="0363d-462">您可以使用 `Page` 对象的属性来获取很多信息，例如：</span><span class="sxs-lookup"><span data-stu-id="0363d-462">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="0363d-463">`Request`。</span><span class="sxs-lookup"><span data-stu-id="0363d-463">`Request`.</span></span> <span data-ttu-id="0363d-464">正如您所看到的，这是有关当前请求的信息的集合，包括发出请求的浏览器的类型、页面的 URL、用户标识等。</span><span class="sxs-lookup"><span data-stu-id="0363d-464">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="0363d-465">`Response`。</span><span class="sxs-lookup"><span data-stu-id="0363d-465">`Response`.</span></span> <span data-ttu-id="0363d-466">这是在服务器代码完成运行时将发送到浏览器的响应（页）信息的集合。</span><span class="sxs-lookup"><span data-stu-id="0363d-466">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="0363d-467">例如，您可以使用此属性将信息写入响应中。</span><span class="sxs-lookup"><span data-stu-id="0363d-467">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="0363d-468">集合对象（数组和字典）</span><span class="sxs-lookup"><span data-stu-id="0363d-468">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="0363d-469">*集合*是一组相同类型的对象，例如来自数据库的 `Customer` 对象的集合。</span><span class="sxs-lookup"><span data-stu-id="0363d-469">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="0363d-470">ASP.NET 包含许多内置集合，如 `Request.Files` 集合。</span><span class="sxs-lookup"><span data-stu-id="0363d-470">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="0363d-471">通常会使用集合中的数据。</span><span class="sxs-lookup"><span data-stu-id="0363d-471">You'll often work with data in collections.</span></span> <span data-ttu-id="0363d-472">两个常见的集合类型是*数组*和*字典*。</span><span class="sxs-lookup"><span data-stu-id="0363d-472">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="0363d-473">如果希望存储类似项的集合，但又不想创建单独的变量来保存每个项，则数组将非常有用：</span><span class="sxs-lookup"><span data-stu-id="0363d-473">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="0363d-474">使用数组，可以声明特定的数据类型，例如 `string`、`int`或 `DateTime`。</span><span class="sxs-lookup"><span data-stu-id="0363d-474">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="0363d-475">若要指示变量可以包含数组，请在声明中添加方括号（如 `string[]` 或 `int[]`）。</span><span class="sxs-lookup"><span data-stu-id="0363d-475">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="0363d-476">您可以使用其位置（索引）或使用 `foreach` 语句来访问数组中的项。</span><span class="sxs-lookup"><span data-stu-id="0363d-476">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="0363d-477">数组索引从零开始， &#8212;这是，第一个项的位置为0，第二项位于位置1，依此类推。</span><span class="sxs-lookup"><span data-stu-id="0363d-477">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="0363d-478">可以通过获取数组中的项的 `Length` 属性来确定这些项的数目。</span><span class="sxs-lookup"><span data-stu-id="0363d-478">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="0363d-479">若要获取数组中特定项的位置（以搜索数组），请使用 `Array.IndexOf` 方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-479">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="0363d-480">您还可以执行一些操作，例如反转数组的内容（`Array.Reverse` 方法）或对内容进行排序（`Array.Sort` 方法）。</span><span class="sxs-lookup"><span data-stu-id="0363d-480">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="0363d-481">在浏览器中显示的字符串数组代码的输出：</span><span class="sxs-lookup"><span data-stu-id="0363d-481">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="0363d-483">字典是键/值对的集合，其中提供了用于设置或检索相应值的键（或名称）：</span><span class="sxs-lookup"><span data-stu-id="0363d-483">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="0363d-484">若要创建字典，请使用 `new` 关键字指示正在创建新的字典对象。</span><span class="sxs-lookup"><span data-stu-id="0363d-484">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="0363d-485">可以使用 `var` 关键字为变量分配字典。</span><span class="sxs-lookup"><span data-stu-id="0363d-485">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="0363d-486">使用尖括号（`< >`）指示字典中项的数据类型。</span><span class="sxs-lookup"><span data-stu-id="0363d-486">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="0363d-487">在声明的末尾，必须添加一对括号，因为这实际上是创建新字典的方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-487">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="0363d-488">若要将项添加到字典中，可以调用字典变量的 `Add` 方法（在本例中为`myScores`），然后指定键和值。</span><span class="sxs-lookup"><span data-stu-id="0363d-488">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="0363d-489">或者，您可以使用方括号来指示密钥并执行简单的分配，如下面的示例中所示：</span><span class="sxs-lookup"><span data-stu-id="0363d-489">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="0363d-490">若要从字典中获取值，请在括号中指定密钥：</span><span class="sxs-lookup"><span data-stu-id="0363d-490">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="0363d-491">调用带参数的方法</span><span class="sxs-lookup"><span data-stu-id="0363d-491">Calling Methods with Parameters</span></span>

<span data-ttu-id="0363d-492">如本文前面所述，使用编写的对象可以有方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-492">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="0363d-493">例如，`Database` 对象可能具有 `Database.Connect` 方法。</span><span class="sxs-lookup"><span data-stu-id="0363d-493">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="0363d-494">许多方法还具有一个或多个参数。</span><span class="sxs-lookup"><span data-stu-id="0363d-494">Many methods also have one or more parameters.</span></span> <span data-ttu-id="0363d-495">*参数*是传递给方法以使方法完成其任务的值。</span><span class="sxs-lookup"><span data-stu-id="0363d-495">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="0363d-496">例如，查看 `Request.MapPath` 方法的声明，该方法采用三个参数：</span><span class="sxs-lookup"><span data-stu-id="0363d-496">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="0363d-497">（此行已换行以使其更具可读性。</span><span class="sxs-lookup"><span data-stu-id="0363d-497">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="0363d-498">请记住，除了用引号引起来的字符串内，您几乎可以在任何位置放置换行符。）</span><span class="sxs-lookup"><span data-stu-id="0363d-498">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="0363d-499">此方法返回与指定虚拟路径相对应的服务器上的物理路径。</span><span class="sxs-lookup"><span data-stu-id="0363d-499">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="0363d-500">方法的三个参数 `virtualPath`、`baseVirtualDir`和 `allowCrossAppMapping`。</span><span class="sxs-lookup"><span data-stu-id="0363d-500">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="0363d-501">（请注意，在声明中，参数与它们将接受的数据的数据类型一起列出。）调用此方法时，必须为所有三个参数提供值。</span><span class="sxs-lookup"><span data-stu-id="0363d-501">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="0363d-502">Razor 语法提供了两个用于将参数传递给方法的选项：*位置参数*和*命名参数*。</span><span class="sxs-lookup"><span data-stu-id="0363d-502">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="0363d-503">若要使用位置参数调用方法，请按方法声明中指定的严格顺序传递参数。</span><span class="sxs-lookup"><span data-stu-id="0363d-503">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="0363d-504">（您通常可以通过阅读该方法的文档来了解此顺序。）必须按照顺序进行操作，如果需要，则不能跳过&#8212;任何参数，而是为没有值的位置参数传递空字符串（`""`）或 `null`。</span><span class="sxs-lookup"><span data-stu-id="0363d-504">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="0363d-505">以下示例假定网站上有一个名为 "*脚本*" 的文件夹。</span><span class="sxs-lookup"><span data-stu-id="0363d-505">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="0363d-506">此代码调用 `Request.MapPath` 方法，并按正确的顺序传递三个参数的值。</span><span class="sxs-lookup"><span data-stu-id="0363d-506">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="0363d-507">然后，它会显示生成的映射路径。</span><span class="sxs-lookup"><span data-stu-id="0363d-507">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="0363d-508">如果方法具有多个参数，则可以通过使用命名参数使代码更具可读性。</span><span class="sxs-lookup"><span data-stu-id="0363d-508">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="0363d-509">若要使用命名参数调用方法，请指定参数名称后跟冒号（:)，然后输入值。</span><span class="sxs-lookup"><span data-stu-id="0363d-509">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="0363d-510">命名参数的优点是可以按所需的任意顺序传递它们。</span><span class="sxs-lookup"><span data-stu-id="0363d-510">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="0363d-511">（缺点是方法调用并不是压缩方法。）</span><span class="sxs-lookup"><span data-stu-id="0363d-511">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="0363d-512">下面的示例调用与上面相同的方法，但使用命名参数来提供值：</span><span class="sxs-lookup"><span data-stu-id="0363d-512">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="0363d-513">正如您所看到的，参数以不同的顺序传递。</span><span class="sxs-lookup"><span data-stu-id="0363d-513">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="0363d-514">但是，如果运行前面的示例和此示例，它们将返回相同的值。</span><span class="sxs-lookup"><span data-stu-id="0363d-514">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="0363d-515">处理错误</span><span class="sxs-lookup"><span data-stu-id="0363d-515">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="0363d-516">Try-catch 语句</span><span class="sxs-lookup"><span data-stu-id="0363d-516">Try-Catch Statements</span></span>

<span data-ttu-id="0363d-517">由于控件外的原因，你的代码中经常会出现语句。</span><span class="sxs-lookup"><span data-stu-id="0363d-517">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="0363d-518">例如：</span><span class="sxs-lookup"><span data-stu-id="0363d-518">For example:</span></span>

- <span data-ttu-id="0363d-519">如果代码尝试创建或访问文件，则可能会出现各种错误。</span><span class="sxs-lookup"><span data-stu-id="0363d-519">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="0363d-520">你需要的文件可能不存在，可能已被锁定，代码可能没有权限，等等。</span><span class="sxs-lookup"><span data-stu-id="0363d-520">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="0363d-521">同样，如果你的代码尝试更新数据库中的记录，则可能存在权限问题，可能会删除与数据库的连接，要保存的数据可能会无效，依此类推。</span><span class="sxs-lookup"><span data-stu-id="0363d-521">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="0363d-522">在编程术语中，这种情况称为 "*异常*"。</span><span class="sxs-lookup"><span data-stu-id="0363d-522">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="0363d-523">如果代码遇到异常，则会生成（引发）一条错误消息，该消息对于用户而言是一种非常令人讨厌的错误消息：</span><span class="sxs-lookup"><span data-stu-id="0363d-523">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="0363d-525">在代码可能遇到异常的情况下，若要避免此类型的错误消息，可以使用 `try/catch` 语句。</span><span class="sxs-lookup"><span data-stu-id="0363d-525">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="0363d-526">在 `try` 语句中，运行要检查的代码。</span><span class="sxs-lookup"><span data-stu-id="0363d-526">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="0363d-527">在一个或多个 `catch` 语句中，可以查找可能发生的特定错误（特定类型的异常）。</span><span class="sxs-lookup"><span data-stu-id="0363d-527">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="0363d-528">您可以包含任意数量的 `catch` 语句，以便查找您要预测的错误。</span><span class="sxs-lookup"><span data-stu-id="0363d-528">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="0363d-529">建议避免在 `try/catch` 语句中使用 `Response.Redirect` 方法，因为这可能会导致页中出现异常。</span><span class="sxs-lookup"><span data-stu-id="0363d-529">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="0363d-530">下面的示例演示了在第一个请求中创建文本文件的页面，然后显示一个按钮，使用户可以打开该文件。</span><span class="sxs-lookup"><span data-stu-id="0363d-530">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="0363d-531">该示例有意使用错误的文件名，以便它将导致异常。</span><span class="sxs-lookup"><span data-stu-id="0363d-531">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="0363d-532">此代码包含两个可能的异常的 `catch` 语句： `FileNotFoundException`，如果文件名错误 `DirectoryNotFoundException`，则会发生这种情况，在 ASP.NET 甚至不能找到该文件夹时，也会出现这种情况。</span><span class="sxs-lookup"><span data-stu-id="0363d-532">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="0363d-533">（您可以在示例中取消注释语句，以查看它在一切正常工作时的运行情况。）</span><span class="sxs-lookup"><span data-stu-id="0363d-533">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="0363d-534">如果代码未处理异常，则会看到一个错误页，如上一个屏幕截图所示。</span><span class="sxs-lookup"><span data-stu-id="0363d-534">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="0363d-535">但 `try/catch` 部分可帮助防止用户看到这些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="0363d-535">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="0363d-536">其他资源</span><span class="sxs-lookup"><span data-stu-id="0363d-536">Additional Resources</span></span>

<span data-ttu-id="0363d-537">**用 Visual Basic 进行编程**</span><span class="sxs-lookup"><span data-stu-id="0363d-537">**Programming with Visual Basic**</span></span>

[<span data-ttu-id="0363d-538">附录： Visual Basic 语言和语法</span><span class="sxs-lookup"><span data-stu-id="0363d-538">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)

<span data-ttu-id="0363d-539">**参考文档**</span><span class="sxs-lookup"><span data-stu-id="0363d-539">**Reference Documentation**</span></span>

[<span data-ttu-id="0363d-540">ASP.NET 2.0</span><span class="sxs-lookup"><span data-stu-id="0363d-540">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="0363d-541">C#语言</span><span class="sxs-lookup"><span data-stu-id="0363d-541">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)
