---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: ASP.NET 网页编程基础知识简介 |Microsoft Docs
author: Rick-Anderson
description: 本教程概述了如何使用 Razor 语法在 ASP.NET 网页中进行编程。 你将学习的内容：用于 pr 的基本 "Razor" 语法
ms.author: riande
ms.date: 06/17/2015
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 474de7671ac2931e5ba9ff635d77385403644521
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509978"
---
# <a name="introducing-aspnet-web-pages---programming-basics"></a><span data-ttu-id="db37d-104">ASP.NET 网页编程基础知识简介</span><span class="sxs-lookup"><span data-stu-id="db37d-104">Introducing ASP.NET Web Pages - Programming Basics</span></span>

<span data-ttu-id="db37d-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="db37d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="db37d-106">本教程概述了如何使用 Razor 语法在 ASP.NET 网页中进行编程。</span><span class="sxs-lookup"><span data-stu-id="db37d-106">This tutorial gives you an overview of how to program in ASP.NET Web Pages with Razor syntax.</span></span>
> 
> <span data-ttu-id="db37d-107">学习内容：</span><span class="sxs-lookup"><span data-stu-id="db37d-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="db37d-108">用于在 ASP.NET 网页中进行编程的基本 "Razor" 语法。</span><span class="sxs-lookup"><span data-stu-id="db37d-108">The basic "Razor" syntax that you use for programming in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="db37d-109">一些基本C#，这是你将使用的编程语言。</span><span class="sxs-lookup"><span data-stu-id="db37d-109">Some basic C#, which is the programming language you'll use.</span></span>
> - <span data-ttu-id="db37d-110">网页的一些基本编程概念。</span><span class="sxs-lookup"><span data-stu-id="db37d-110">Some fundamental programming concepts for Web Pages.</span></span>
> - <span data-ttu-id="db37d-111">如何安装包（包含预先生成的代码的组件）以用于您的站点。</span><span class="sxs-lookup"><span data-stu-id="db37d-111">How to install packages (components that contain prebuilt code) to use with your site.</span></span>
> - <span data-ttu-id="db37d-112">如何使用*帮助*程序执行常见的编程任务。</span><span class="sxs-lookup"><span data-stu-id="db37d-112">How to use *helpers* to perform common programming tasks.</span></span>
>   
> 
> <span data-ttu-id="db37d-113">介绍的功能/技术：</span><span class="sxs-lookup"><span data-stu-id="db37d-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="db37d-114">NuGet 和包管理器。</span><span class="sxs-lookup"><span data-stu-id="db37d-114">NuGet and the package manager.</span></span>
> - <span data-ttu-id="db37d-115">`Gravatar` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="db37d-115">The `Gravatar` helper.</span></span>

<span data-ttu-id="db37d-116">本教程主要为你介绍将用于 ASP.NET 网页的编程语法。</span><span class="sxs-lookup"><span data-stu-id="db37d-116">This tutorial is primarily an exercise in introducing you to the programming syntax that you'll use for ASP.NET Web Pages.</span></span> <span data-ttu-id="db37d-117">你将了解用 C#编程语言编写的 Razor 语法和代码。</span><span class="sxs-lookup"><span data-stu-id="db37d-117">You'll learn about *Razor syntax* and code that's written in the C# programming language.</span></span> <span data-ttu-id="db37d-118">你将在上一教程中大致了解此语法;在本教程中，我们将更详细地介绍语法。</span><span class="sxs-lookup"><span data-stu-id="db37d-118">You got a glimpse of this syntax in the previous tutorial; in this tutorial we'll explain the syntax more.</span></span>

<span data-ttu-id="db37d-119">我们保证本教程涉及到你在单个教程中看到的大多数编程，这是*仅有关编程的唯一教程*。</span><span class="sxs-lookup"><span data-stu-id="db37d-119">We promise that this tutorial involves the most programming that you'll see in a single tutorial, and that it's the only tutorial that is *only* about programming.</span></span> <span data-ttu-id="db37d-120">在此集的其余教程中，你将实际创建可执行有趣操作的页面。</span><span class="sxs-lookup"><span data-stu-id="db37d-120">In the remaining tutorials in this set, you'll actually create pages that do interesting things.</span></span>

<span data-ttu-id="db37d-121">你还将了解*帮助*程序。</span><span class="sxs-lookup"><span data-stu-id="db37d-121">You'll also learn about *helpers*.</span></span> <span data-ttu-id="db37d-122">帮助器是可添加到页面的组件（一段打包的代码）。</span><span class="sxs-lookup"><span data-stu-id="db37d-122">A helper is a component — a packaged-up piece of code — that you can add to a page.</span></span> <span data-ttu-id="db37d-123">帮助器会为您执行工作，否则，手动操作可能单调乏味或复杂。</span><span class="sxs-lookup"><span data-stu-id="db37d-123">The helper performs work for you that otherwise might be tedious or complex to do by hand.</span></span>

## <a name="creating-a-page-to-play-with-razor"></a><span data-ttu-id="db37d-124">创建使用 Razor 播放的页面</span><span class="sxs-lookup"><span data-stu-id="db37d-124">Creating a Page to Play with Razor</span></span>

<span data-ttu-id="db37d-125">在本部分中，你将玩 Razor，因此你可以了解基本语法。</span><span class="sxs-lookup"><span data-stu-id="db37d-125">In this section you'll play a bit with Razor so you can get a sense of the basic syntax.</span></span>

<span data-ttu-id="db37d-126">如果它尚未运行，请启动 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="db37d-126">Start WebMatrix if it's not already running.</span></span> <span data-ttu-id="db37d-127">你将使用在上一教程中创建的网站（[入门](https://go.microsoft.com/fwlink/?LinkId=251578)网页）。</span><span class="sxs-lookup"><span data-stu-id="db37d-127">You'll use the website you created in the previous tutorial ([Getting Started With Web Pages](https://go.microsoft.com/fwlink/?LinkId=251578)).</span></span> <span data-ttu-id="db37d-128">若要重新打开它，请单击 **"我的网站**" 并选择**WebPageMovies**：</span><span class="sxs-lookup"><span data-stu-id="db37d-128">To reopen it, click **My Sites** and choose **WebPageMovies**:</span></span>

![WebMatrix 开始屏幕显示 "打开网站选项" 和 "我的网站" 突出显示](intro-to-web-pages-programming/_static/image1.png)

<span data-ttu-id="db37d-130">选择 "**文件**" 工作区。</span><span class="sxs-lookup"><span data-stu-id="db37d-130">Select the **Files** workspace.</span></span>

<span data-ttu-id="db37d-131">在功能区中，单击 "**新建**" 以创建页面。</span><span class="sxs-lookup"><span data-stu-id="db37d-131">In the ribbon, click **New** to create a page.</span></span> <span data-ttu-id="db37d-132">选择 " **CSHTML** " 并将新页命名为*TestRazor*。</span><span class="sxs-lookup"><span data-stu-id="db37d-132">Select **CSHTML** and name the new page *TestRazor.cshtml*.</span></span>

<span data-ttu-id="db37d-133">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="db37d-133">Click **OK**.</span></span>

<span data-ttu-id="db37d-134">将以下内容复制到文件中，完全替换已存在的内容。</span><span class="sxs-lookup"><span data-stu-id="db37d-134">Copy the following into the file, completely replacing what's there already.</span></span>

> [!NOTE]
> <span data-ttu-id="db37d-135">将代码或标记从示例复制到页面时，缩进和对齐方式可能与教程中的不同。</span><span class="sxs-lookup"><span data-stu-id="db37d-135">When you copy code or markup from the examples into a page, the indentation and alignment might not be the same as in the tutorial.</span></span> <span data-ttu-id="db37d-136">不过，缩进和对齐不会影响代码的运行方式。</span><span class="sxs-lookup"><span data-stu-id="db37d-136">Indentation and alignment don't affect how the code runs, though.</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a><span data-ttu-id="db37d-137">检查 "示例" 页</span><span class="sxs-lookup"><span data-stu-id="db37d-137">Examining the Example Page</span></span>

<span data-ttu-id="db37d-138">你看到的大多数是普通的 HTML。</span><span class="sxs-lookup"><span data-stu-id="db37d-138">Most of what you see is ordinary HTML.</span></span> <span data-ttu-id="db37d-139">但在顶部有此代码块：</span><span class="sxs-lookup"><span data-stu-id="db37d-139">However, at the top there's this code block:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

<span data-ttu-id="db37d-140">请注意以下有关此代码块的事项：</span><span class="sxs-lookup"><span data-stu-id="db37d-140">Notice the following things about this code block:</span></span>

- <span data-ttu-id="db37d-141">@ 字符告诉 ASP.NET，下面是 Razor 代码，而不是 HTML。</span><span class="sxs-lookup"><span data-stu-id="db37d-141">The @ character tells ASP.NET that what follows is Razor code, not HTML.</span></span> <span data-ttu-id="db37d-142">ASP.NET 会将 @ 字符后面的所有内容视为代码，直到它再次进入一些 HTML。</span><span class="sxs-lookup"><span data-stu-id="db37d-142">ASP.NET will treat everything after the @ character as code until it runs into some HTML again.</span></span> <span data-ttu-id="db37d-143">（在这种情况下，这是 &lt;！DOCTYPE&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="db37d-143">(In this case, that's the &lt;!DOCTYPE&gt; element.</span></span>
- <span data-ttu-id="db37d-144">如果代码具有多个行，则大括号（{和}）包含一个 Razor 代码块。</span><span class="sxs-lookup"><span data-stu-id="db37d-144">The braces ( { and } ) enclose a block of Razor code if the code has more than one line.</span></span> <span data-ttu-id="db37d-145">大括号指示 ASP.NET 的代码在何处开始和结束。</span><span class="sxs-lookup"><span data-stu-id="db37d-145">The braces tell ASP.NET where the code for that block starts and ends.</span></span>
- <span data-ttu-id="db37d-146">字符标记注释，即不会执行的代码的一部分。</span><span class="sxs-lookup"><span data-stu-id="db37d-146">The // characters mark a comment — that is, a part of the code that won't execute.</span></span>
- <span data-ttu-id="db37d-147">每个语句必须以分号（;) 结束。</span><span class="sxs-lookup"><span data-stu-id="db37d-147">Each statement has to end with a semicolon (;).</span></span> <span data-ttu-id="db37d-148">（不过，不是注释。）</span><span class="sxs-lookup"><span data-stu-id="db37d-148">(Not comments, though.)</span></span>
- <span data-ttu-id="db37d-149">你可以将值存储在用关键字 var 创建（*声明*）的*变量*中。</span><span class="sxs-lookup"><span data-stu-id="db37d-149">You can store values in *variables*, which you create (*declare*) with the keyword var.</span></span> <span data-ttu-id="db37d-150">创建变量时，可以为其指定一个名称，该名称可以包含字母、数字和下划线（\_）。</span><span class="sxs-lookup"><span data-stu-id="db37d-150">When you create a variable, you give it a name, which can include letters, numbers, and underscore (\_).</span></span> <span data-ttu-id="db37d-151">变量名不能以数字开头，也不能使用编程关键字的名称（如 var）。</span><span class="sxs-lookup"><span data-stu-id="db37d-151">Variable names can't start with a number and can't use the name of a programming keyword (like var).</span></span>
- <span data-ttu-id="db37d-152">用引号将字符串（如 "ASP.NET" 和 "Web Pages"）括起来。</span><span class="sxs-lookup"><span data-stu-id="db37d-152">You enclose character strings (like "ASP.NET" and "Web Pages") in quotation marks.</span></span> <span data-ttu-id="db37d-153">（它们必须是双引号。）数字不是用引号引起来。</span><span class="sxs-lookup"><span data-stu-id="db37d-153">(They must be double quotation marks.) Numbers are not in quotation marks.</span></span>
- <span data-ttu-id="db37d-154">引号外的空白并不重要。</span><span class="sxs-lookup"><span data-stu-id="db37d-154">Whitespace outside of quotation marks doesn't matter.</span></span> <span data-ttu-id="db37d-155">换行符通常无关紧要;例外情况是不能跨行拆分用引号引起来的字符串。</span><span class="sxs-lookup"><span data-stu-id="db37d-155">Line breaks mostly don't matter; the exception is that you can't split a string in quotation marks across lines.</span></span> <span data-ttu-id="db37d-156">缩进和对齐并不重要。</span><span class="sxs-lookup"><span data-stu-id="db37d-156">Indentation and alignment don't matter.</span></span>

<span data-ttu-id="db37d-157">在此示例中不明显的内容是所有代码都区分大小写。</span><span class="sxs-lookup"><span data-stu-id="db37d-157">Something that's not obvious from this example is that all code is case sensitive.</span></span> <span data-ttu-id="db37d-158">这意味着变量参数是一个与可能名为参数或参数的变量不同的变量。</span><span class="sxs-lookup"><span data-stu-id="db37d-158">This means that the variable TheSum is a different variable than variables that might be named theSum or thesum.</span></span> <span data-ttu-id="db37d-159">同样，var 是关键字，但 Var 却不是。</span><span class="sxs-lookup"><span data-stu-id="db37d-159">Similarly, var is a keyword, but Var is not.</span></span>

### <a name="objects-and-properties-and-methods"></a><span data-ttu-id="db37d-160">对象和属性和方法</span><span class="sxs-lookup"><span data-stu-id="db37d-160">Objects and properties and methods</span></span>

<span data-ttu-id="db37d-161">接下来就是表达式日期时间。</span><span class="sxs-lookup"><span data-stu-id="db37d-161">Then there's the expression DateTime.Now.</span></span> <span data-ttu-id="db37d-162">简而言之，DateTime 是一个*对象*。</span><span class="sxs-lookup"><span data-stu-id="db37d-162">In simple terms, DateTime is an *object*.</span></span> <span data-ttu-id="db37d-163">对象是您可以使用进行编程的内容：页面、文本框、文件、图像、web 请求、电子邮件、客户记录等。对象具有一个或多个描述其特征的*属性*。</span><span class="sxs-lookup"><span data-stu-id="db37d-163">An object is a thing that you can program with—a page, a text box, a file, an image, a web request, an email message, a customer record, etc. Objects have one or more *properties* that describe their characteristics.</span></span> <span data-ttu-id="db37d-164">文本框对象具有文本属性（其他），请求对象具有 Url 属性（及其他），电子邮件中包含 From 属性和 To 属性等。</span><span class="sxs-lookup"><span data-stu-id="db37d-164">A text box object has a Text property (among others), a request object has a Url property (and others), an email message has a From property and a To property, and so on.</span></span> <span data-ttu-id="db37d-165">对象还包含它们可以执行的 "谓词" 的*方法*。</span><span class="sxs-lookup"><span data-stu-id="db37d-165">Objects also have *methods* that are the "verbs" they can perform.</span></span> <span data-ttu-id="db37d-166">您将很多地处理对象。</span><span class="sxs-lookup"><span data-stu-id="db37d-166">You'll be working with objects a lot.</span></span>

<span data-ttu-id="db37d-167">如示例中所示，DateTime 是一个对象，可用于对日期和时间进行编程。</span><span class="sxs-lookup"><span data-stu-id="db37d-167">As you can see from the example, DateTime is an object that lets you program dates and times.</span></span> <span data-ttu-id="db37d-168">它有一个名为 "现在" 的属性，该属性返回当前日期和时间。</span><span class="sxs-lookup"><span data-stu-id="db37d-168">It has a property named Now that returns the current date and time.</span></span>

### <a name="using-code-to-render-markup-in-the-page"></a><span data-ttu-id="db37d-169">使用代码在页中呈现标记</span><span class="sxs-lookup"><span data-stu-id="db37d-169">Using code to render markup in the page</span></span>

<span data-ttu-id="db37d-170">在页面的正文中，请注意以下事项：</span><span class="sxs-lookup"><span data-stu-id="db37d-170">In the body of the page, notice the following:</span></span>

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

<span data-ttu-id="db37d-171">同样，@ 字符告诉 ASP.NET，下面是代码而不是 HTML。</span><span class="sxs-lookup"><span data-stu-id="db37d-171">Again, the @ character tells ASP.NET that what follows is code, not HTML.</span></span> <span data-ttu-id="db37d-172">在标记中，可以添加 @，后跟代码表达式，ASP.NET 将在该点向右呈现该表达式的值。</span><span class="sxs-lookup"><span data-stu-id="db37d-172">In the markup you can add @ followed by a code expression, and ASP.NET will render the value of that expression right at that point.</span></span> <span data-ttu-id="db37d-173">在此示例中，@a 将呈现值为名为的变量，@product 呈现名为 product 的变量中的任何内容，等等。</span><span class="sxs-lookup"><span data-stu-id="db37d-173">In the example, @a will render whatever the value is of the variable named a, @product renders whatever is in the variable named product, and so on.</span></span>

<span data-ttu-id="db37d-174">不过，你并不局限于变量。</span><span class="sxs-lookup"><span data-stu-id="db37d-174">You're not limited to variables, though.</span></span> <span data-ttu-id="db37d-175">在此处的几个示例中，@ 字符位于表达式之前：</span><span class="sxs-lookup"><span data-stu-id="db37d-175">In a few instances here, the @ character precedes an expression:</span></span>

- <span data-ttu-id="db37d-176">@ （\*b）呈现变量 a 和 b 中的所有内容。</span><span class="sxs-lookup"><span data-stu-id="db37d-176">@(a\*b) renders the product of whatever is in the variables a and b.</span></span> <span data-ttu-id="db37d-177">（\* 运算符表示乘法。）</span><span class="sxs-lookup"><span data-stu-id="db37d-177">(The \* operator means multiplication.)</span></span>
- <span data-ttu-id="db37d-178">@ （技术 + "" + product）在连接变量并在两者之间添加空格后，呈现变量技术和产品中的值。</span><span class="sxs-lookup"><span data-stu-id="db37d-178">@(technology + " " + product) renders the values in the variables technology and product after concatenating them and adding a space in between.</span></span> <span data-ttu-id="db37d-179">用于串联字符串的运算符（+）与用于添加数字的运算符相同。</span><span class="sxs-lookup"><span data-stu-id="db37d-179">The operator (+) for concatenating strings is the same as the operator for adding numbers.</span></span> <span data-ttu-id="db37d-180">ASP.NET 通常可以判断你使用的是数字还是字符串，并使用 + 运算符执行正确的操作。</span><span class="sxs-lookup"><span data-stu-id="db37d-180">ASP.NET can usually tell whether you're working with numbers or with strings and does the right thing with the + operator.</span></span>
- <span data-ttu-id="db37d-181">@Request.Url 呈现 Request 对象的 Url 属性。</span><span class="sxs-lookup"><span data-stu-id="db37d-181">@Request.Url renders the Url property of the Request object.</span></span> <span data-ttu-id="db37d-182">Request 对象包含来自浏览器的当前请求的相关信息，当然，Url 属性包含该当前请求的 URL。</span><span class="sxs-lookup"><span data-stu-id="db37d-182">The Request object contains information about the current request from the browser, and of course the Url property contains the URL of that current request.</span></span>

<span data-ttu-id="db37d-183">该示例还旨在向您演示如何以不同的方式执行工作。</span><span class="sxs-lookup"><span data-stu-id="db37d-183">The example is also designed to show you that you can do work in different ways.</span></span> <span data-ttu-id="db37d-184">可以在顶部的代码块中执行计算，将结果放入变量中，然后在标记中呈现变量。</span><span class="sxs-lookup"><span data-stu-id="db37d-184">You can do calculations in the code block at the top, put the results into a variable, and then render the variable in markup.</span></span> <span data-ttu-id="db37d-185">或者，您可以在标记中的表达式中执行计算。</span><span class="sxs-lookup"><span data-stu-id="db37d-185">Or you can do calculations in an expression right in the markup.</span></span> <span data-ttu-id="db37d-186">使用哪种方法取决于您所执行的操作，并且在某种程度上取决于您自己的喜好。</span><span class="sxs-lookup"><span data-stu-id="db37d-186">The approach you use depends on what you're doing and, to some extent, on your own preference.</span></span>

### <a name="seeing-the-code-in-action"></a><span data-ttu-id="db37d-187">查看正在运行的代码</span><span class="sxs-lookup"><span data-stu-id="db37d-187">Seeing the code in action</span></span>

<span data-ttu-id="db37d-188">右键单击该文件的名称，然后选择 "**在浏览器中启动"** 。</span><span class="sxs-lookup"><span data-stu-id="db37d-188">Right-click the name of the file and then choose **Launch in browser**.</span></span> <span data-ttu-id="db37d-189">你将在浏览器中看到页面中已解决的所有值和表达式。</span><span class="sxs-lookup"><span data-stu-id="db37d-189">You see the page in the browser with all the values and expressions resolved in the page.</span></span>

![在浏览器中运行的 "TestRazor" 页](intro-to-web-pages-programming/_static/image2.png)

<span data-ttu-id="db37d-191">查看浏览器中的源。</span><span class="sxs-lookup"><span data-stu-id="db37d-191">Look at the source in the browser.</span></span>

![浏览器中的 "Test Razor" 页面源](intro-to-web-pages-programming/_static/image3.png)

<span data-ttu-id="db37d-193">正如你在上一教程中的经验所期望的那样，此页中不会有任何 Razor 代码。</span><span class="sxs-lookup"><span data-stu-id="db37d-193">As you expect from your experience in the previous tutorial, none of the Razor code is in the page.</span></span> <span data-ttu-id="db37d-194">您看到的只是实际显示值。</span><span class="sxs-lookup"><span data-stu-id="db37d-194">All you see are the actual display values.</span></span> <span data-ttu-id="db37d-195">当你运行某个页面时，实际上就是发出到 WebMatrix 中内置的 web 服务器的请求。</span><span class="sxs-lookup"><span data-stu-id="db37d-195">When you run a page, you're actually making a request to the web server that's built into WebMatrix.</span></span> <span data-ttu-id="db37d-196">收到请求后，ASP.NET 解析所有值和表达式，并将其值呈现到页面中。</span><span class="sxs-lookup"><span data-stu-id="db37d-196">When the request is received, ASP.NET resolves all the values and expressions and renders their values into the page.</span></span> <span data-ttu-id="db37d-197">然后，将该页发送到浏览器。</span><span class="sxs-lookup"><span data-stu-id="db37d-197">It then sends the page to the browser.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="db37d-198">**Razor 和C#**</span><span class="sxs-lookup"><span data-stu-id="db37d-198">**Razor and C#**</span></span>
> 
> <span data-ttu-id="db37d-199">至此，我们已经说过使用 Razor 语法。</span><span class="sxs-lookup"><span data-stu-id="db37d-199">Up to now we've said that you're working with Razor syntax.</span></span> <span data-ttu-id="db37d-200">这是正确的，但它不是完整的故事。</span><span class="sxs-lookup"><span data-stu-id="db37d-200">That's true, but it's not the complete story.</span></span> <span data-ttu-id="db37d-201">你使用的实际编程语言称为*C#* 。</span><span class="sxs-lookup"><span data-stu-id="db37d-201">The actual programming language you're using is called *C#*.</span></span> <span data-ttu-id="db37d-202">C#是 Microsoft 在十年前创建的，已成为创建 Windows 应用程序的主要编程语言之一。</span><span class="sxs-lookup"><span data-stu-id="db37d-202">C# was created by Microsoft over a decade ago and has become one of the primary programming languages for creating Windows apps.</span></span> <span data-ttu-id="db37d-203">已了解的有关如何命名变量以及如何创建语句等的所有规则实际上是该C#语言的所有规则。</span><span class="sxs-lookup"><span data-stu-id="db37d-203">All the rules you've seen about how to name a variable and how to create statements and so on are actually all rules of the C# language.</span></span>
> 
> <span data-ttu-id="db37d-204">Razor 特别适用于将此代码嵌入页面的一小部分约定。</span><span class="sxs-lookup"><span data-stu-id="db37d-204">Razor refers more specifically to the small set of conventions for how you embed this code into a page.</span></span> <span data-ttu-id="db37d-205">例如，使用 @ 在页中标记代码，并使用 @ {} 嵌入代码块的约定是页面的 Razor 方面。</span><span class="sxs-lookup"><span data-stu-id="db37d-205">For example, the convention of using @ to mark code in the page and using @{ } to embed a code block is the Razor aspect of a page.</span></span> <span data-ttu-id="db37d-206">帮助器也被视为 Razor 的一部分。</span><span class="sxs-lookup"><span data-stu-id="db37d-206">Helpers are also considered to be part of Razor.</span></span> <span data-ttu-id="db37d-207">Razor 语法在多个位置使用，而不只是在 ASP.NET 网页中使用。</span><span class="sxs-lookup"><span data-stu-id="db37d-207">Razor syntax is used in more places than just in ASP.NET Web Pages.</span></span> <span data-ttu-id="db37d-208">（例如，它也用于 ASP.NET MVC 视图中。）</span><span class="sxs-lookup"><span data-stu-id="db37d-208">(For example, it's used in ASP.NET MVC views as well.)</span></span>
> 
> <span data-ttu-id="db37d-209">我们提及这是因为，如果您查找有关编程 ASP.NET 网页的信息，您会发现很多对 Razor 的引用。</span><span class="sxs-lookup"><span data-stu-id="db37d-209">We mention this because if you look for information about programming ASP.NET Web Pages, you'll find lots of references to Razor.</span></span> <span data-ttu-id="db37d-210">但是，其中许多引用不适用于您正在执行的操作，因此可能会造成混淆。</span><span class="sxs-lookup"><span data-stu-id="db37d-210">However, a lot of those references don't apply to what you're doing and might therefore be confusing.</span></span> <span data-ttu-id="db37d-211">事实上，许多编程问题都确实涉及到使用C#或使用 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="db37d-211">And in fact, many of your programming questions are really going to be about either working with C# or working with ASP.NET.</span></span> <span data-ttu-id="db37d-212">因此，如果您特别了解 Razor 的相关信息，可能无法找到所需的答案。</span><span class="sxs-lookup"><span data-stu-id="db37d-212">So if you look specifically for information about Razor, you might not find the answers you need.</span></span>

## <a name="adding-some-conditional-logic"></a><span data-ttu-id="db37d-213">添加一些条件逻辑</span><span class="sxs-lookup"><span data-stu-id="db37d-213">Adding Some Conditional Logic</span></span>

<span data-ttu-id="db37d-214">在页面中使用代码的一项强大功能是，可以根据各种条件更改发生的情况。</span><span class="sxs-lookup"><span data-stu-id="db37d-214">One of the great features about using code in a page is that you can change what happens based on various conditions.</span></span> <span data-ttu-id="db37d-215">在本教程的此部分中，你将了解一些如何更改页面中显示的内容的方法。</span><span class="sxs-lookup"><span data-stu-id="db37d-215">In this part of the tutorial, you'll play around with some ways to change what's displayed in the page.</span></span>

<span data-ttu-id="db37d-216">该示例简单、有些精心设计，以便我们可以将精力集中在条件逻辑上。</span><span class="sxs-lookup"><span data-stu-id="db37d-216">The example will be simple and somewhat contrived so that we can concentrate on the conditional logic.</span></span> <span data-ttu-id="db37d-217">你将创建的页面将执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="db37d-217">The page you'll create will do this:</span></span>

- <span data-ttu-id="db37d-218">在页面上显示不同的文本，具体取决于页面是第一次显示还是已单击按钮来提交页面。</span><span class="sxs-lookup"><span data-stu-id="db37d-218">Show different text on the page depending on whether it's the first time the page is displayed or whether you've clicked a button to submit the page.</span></span> <span data-ttu-id="db37d-219">这将是第一个条件测试。</span><span class="sxs-lookup"><span data-stu-id="db37d-219">That will be the first conditional test.</span></span>
- <span data-ttu-id="db37d-220">仅当在 URL 的查询字符串中传递了某个值（http：//...？ show = true）时，才显示该消息。</span><span class="sxs-lookup"><span data-stu-id="db37d-220">Display the message only if a certain value is passed in the query string of the URL (http://...?show=true).</span></span> <span data-ttu-id="db37d-221">这将是第二个条件测试。</span><span class="sxs-lookup"><span data-stu-id="db37d-221">That will be the second conditional test.</span></span>

<span data-ttu-id="db37d-222">在 WebMatrix 中创建页面，并将其命名为*TestRazorPart2*。</span><span class="sxs-lookup"><span data-stu-id="db37d-222">In WebMatrix, create a page and name it *TestRazorPart2.cshtml*.</span></span> <span data-ttu-id="db37d-223">（在功能区中，单击 "**新建**"，选择 " **CSHTML**"，为文件命名，然后单击 **"确定"** 。）</span><span class="sxs-lookup"><span data-stu-id="db37d-223">(In the ribbon, click **New**, choose **CSHTML**, name the file, and then click **OK**.)</span></span>

<span data-ttu-id="db37d-224">将此页的内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="db37d-224">Replace the contents of that page with the following:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

<span data-ttu-id="db37d-225">顶部的代码块用一些文本初始化名为 message 的变量。</span><span class="sxs-lookup"><span data-stu-id="db37d-225">The code block at the top initializes a variable named message with some text.</span></span> <span data-ttu-id="db37d-226">在页面的正文中，消息变量的内容显示在 &lt;p&gt; 元素中。</span><span class="sxs-lookup"><span data-stu-id="db37d-226">In the body of the page, the contents of the message variable are displayed inside a &lt;p&gt; element.</span></span> <span data-ttu-id="db37d-227">标记还包含一个 &lt;输入&gt; 元素来创建 "**提交**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="db37d-227">The markup also contains an &lt;input&gt; element to create a **Submit** button.</span></span>

<span data-ttu-id="db37d-228">运行页面，查看其工作原理。</span><span class="sxs-lookup"><span data-stu-id="db37d-228">Run the page to see how it works now.</span></span> <span data-ttu-id="db37d-229">现在，它基本上是一个静态页面，即使单击 "**提交**" 按钮也是如此。</span><span class="sxs-lookup"><span data-stu-id="db37d-229">For now, it's basically a static page, even if you click the **Submit** button.</span></span>

<span data-ttu-id="db37d-230">返回到 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="db37d-230">Go back to WebMatrix.</span></span> <span data-ttu-id="db37d-231">在代码块中，在初始化消息的行*后*添加以下突出显示的代码：</span><span class="sxs-lookup"><span data-stu-id="db37d-231">Inside the code block, add the following highlighted code *after* the line that initializes message:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a><span data-ttu-id="db37d-232">If {} 块</span><span class="sxs-lookup"><span data-stu-id="db37d-232">The if { } block</span></span>

<span data-ttu-id="db37d-233">刚添加的是 if 条件。</span><span class="sxs-lookup"><span data-stu-id="db37d-233">What you just added was an if condition.</span></span> <span data-ttu-id="db37d-234">在代码中，if 条件的结构如下所示：</span><span class="sxs-lookup"><span data-stu-id="db37d-234">In code, the if condition has a structure like this:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

<span data-ttu-id="db37d-235">要测试的条件用圆括号括起来。</span><span class="sxs-lookup"><span data-stu-id="db37d-235">The condition to test is in parentheses.</span></span> <span data-ttu-id="db37d-236">它必须为值或返回 true 或 false 的表达式。</span><span class="sxs-lookup"><span data-stu-id="db37d-236">It has to be a value or an expression that returns true or false.</span></span> <span data-ttu-id="db37d-237">如果条件为 true，则 ASP.NET 将运行位于大括号内的语句或语句。</span><span class="sxs-lookup"><span data-stu-id="db37d-237">If the condition is true, ASP.NET runs the statement or statements that are inside the braces.</span></span> <span data-ttu-id="db37d-238">（这是*if*逻辑的*then*部分。）如果条件为 false，则跳过代码块。</span><span class="sxs-lookup"><span data-stu-id="db37d-238">(Those are the *then* part of the *if-then* logic.) If the condition is false, the block of code is skipped.</span></span>

<span data-ttu-id="db37d-239">下面是可以在 if 语句中测试的条件的几个示例：</span><span class="sxs-lookup"><span data-stu-id="db37d-239">Here are a few examples of conditions you can test in an if statement:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

<span data-ttu-id="db37d-240">您可以通过使用*逻辑运算符*或*比较运算符*来对照值或表达式来测试变量：等于（= =）、大于（&gt;）、小于（&lt;）、大于或等于（&gt;=）以及小于或等于（&lt;=）。</span><span class="sxs-lookup"><span data-stu-id="db37d-240">You can test variables against values or against expressions by using a *logical operator* or *comparison operator*: equal to (==), greater than (&gt;), less than (&lt;), greater than or equal to (&gt;=), and less than or equal to (&lt;=).</span></span> <span data-ttu-id="db37d-241">！ = 运算符表示不等于，例如，如果（a！ = 0）表示*不等于 0*。</span><span class="sxs-lookup"><span data-stu-id="db37d-241">The != operator means not equal to — for example, if(a != 0) means *if a is not equal to 0*.</span></span>

> [!NOTE]
> <span data-ttu-id="db37d-242">请务必注意，equals 的比较运算符（= =）与 = 不相同。</span><span class="sxs-lookup"><span data-stu-id="db37d-242">Make sure you notice that the comparison operator for equals to (==) is not the same as =.</span></span> <span data-ttu-id="db37d-243">= 运算符仅用于赋值（var a = 2）。</span><span class="sxs-lookup"><span data-stu-id="db37d-243">The = operator is used only to assign values (var a=2).</span></span> <span data-ttu-id="db37d-244">如果将这些运算符组合在一起，则会出现错误，否则会出现一些奇怪的结果。</span><span class="sxs-lookup"><span data-stu-id="db37d-244">If you mix these operators up, you'll either get an error or you'll get some strange results.</span></span>

<span data-ttu-id="db37d-245">若要测试是否为 true，则完整的语法为 if （操作 = = true）。</span><span class="sxs-lookup"><span data-stu-id="db37d-245">To test whether something is true, the complete syntax is if(IsDone == true).</span></span> <span data-ttu-id="db37d-246">但如果为（操作），则还可以使用快捷方式。</span><span class="sxs-lookup"><span data-stu-id="db37d-246">But you can also use the shortcut if(IsDone).</span></span> <span data-ttu-id="db37d-247">如果没有比较运算符，则 ASP.NET 假设您要测试是否为 true。</span><span class="sxs-lookup"><span data-stu-id="db37d-247">If there's no comparison operator, ASP.NET assumes that you're testing for true.</span></span>

<span data-ttu-id="db37d-248">此 !</span><span class="sxs-lookup"><span data-stu-id="db37d-248">The !</span></span> <span data-ttu-id="db37d-249">运算符本身表示逻辑非。</span><span class="sxs-lookup"><span data-stu-id="db37d-249">operator by itself means a logical NOT.</span></span> <span data-ttu-id="db37d-250">例如，条件 if （！IsPost）表示*IsPost 是否不为 true*。</span><span class="sxs-lookup"><span data-stu-id="db37d-250">For example, the condition if(!IsPost) means *if IsPost is not true*.</span></span>

<span data-ttu-id="db37d-251">您可以通过使用逻辑 AND （&amp;&amp; 运算符）或逻辑 OR （| | 运算符）来组合条件。</span><span class="sxs-lookup"><span data-stu-id="db37d-251">You can combine conditions by using a logical AND (&amp;&amp; operator) or logical OR (|| operator).</span></span> <span data-ttu-id="db37d-252">例如，在前面的示例中，if 条件的最后一个表示*如果 FileProcessingIsDone 未设置为 TRUE 且 displayMessage 设置为 false*。</span><span class="sxs-lookup"><span data-stu-id="db37d-252">For example, the last of the if conditions in the preceding examples means *if FileProcessingIsDone is not set to true AND displayMessage is set to false*.</span></span>

### <a name="the-else-block"></a><span data-ttu-id="db37d-253">Else 块</span><span class="sxs-lookup"><span data-stu-id="db37d-253">The else block</span></span>

<span data-ttu-id="db37d-254">如果是块，最后一件事： if 块后跟 else 块。</span><span class="sxs-lookup"><span data-stu-id="db37d-254">One final thing about if blocks: an if block can be followed by an else block.</span></span> <span data-ttu-id="db37d-255">Else 块很有用，因为当条件为 false 时，必须执行不同的代码。</span><span class="sxs-lookup"><span data-stu-id="db37d-255">An else block is useful is you have to execute different code when the condition is false.</span></span> <span data-ttu-id="db37d-256">以下是一个简单的示例：</span><span class="sxs-lookup"><span data-stu-id="db37d-256">Here's a simple example:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

<span data-ttu-id="db37d-257">你将在本系列的后续教程中看到一些示例，其中使用 else 块很有用。</span><span class="sxs-lookup"><span data-stu-id="db37d-257">You'll see some examples in later tutorials in this series where using an else block is useful.</span></span>

### <a name="testing-whether-the-request-is-a-submit-post"></a><span data-ttu-id="db37d-258">测试请求是否为提交（post）</span><span class="sxs-lookup"><span data-stu-id="db37d-258">Testing whether the request is a submit (post)</span></span>

<span data-ttu-id="db37d-259">还有很多，但让我们回到示例，该示例具有条件 if （IsPost） {...}。</span><span class="sxs-lookup"><span data-stu-id="db37d-259">There's more, but let's get back to the example, which has the condition if(IsPost){ ... }.</span></span> <span data-ttu-id="db37d-260">IsPost 实际上是当前页的属性。</span><span class="sxs-lookup"><span data-stu-id="db37d-260">IsPost is actually a property of the current page.</span></span> <span data-ttu-id="db37d-261">第一次请求页面时，IsPost 返回 false。</span><span class="sxs-lookup"><span data-stu-id="db37d-261">The first time the page is requested, IsPost returns false.</span></span> <span data-ttu-id="db37d-262">但是，如果您单击某一按钮或以其他方式提交该页（也就是说，您发布了它），则 IsPost 将返回 true。</span><span class="sxs-lookup"><span data-stu-id="db37d-262">However, if you click a button or otherwise submit the page — that is, you post it — IsPost returns true.</span></span> <span data-ttu-id="db37d-263">因此，IsPost 可让你确定是否正在处理窗体提交。</span><span class="sxs-lookup"><span data-stu-id="db37d-263">So IsPost lets you determine whether you're dealing with a form submission.</span></span> <span data-ttu-id="db37d-264">（根据 HTTP 谓词，如果请求是 GET 操作，则 IsPost 将返回 false。</span><span class="sxs-lookup"><span data-stu-id="db37d-264">(In terms of HTTP verbs, if the request is a GET operation, IsPost returns false.</span></span> <span data-ttu-id="db37d-265">如果请求是 POST 操作，则 IsPost 将返回 true。）在后面的教程中，你将使用输入窗体，此测试将特别有用。</span><span class="sxs-lookup"><span data-stu-id="db37d-265">If the request is a POST operation, IsPost returns true.) In a later tutorial you'll work with input forms, where this test becomes particularly useful.</span></span>

<span data-ttu-id="db37d-266">运行页面。</span><span class="sxs-lookup"><span data-stu-id="db37d-266">Run the page.</span></span> <span data-ttu-id="db37d-267">由于这是你第一次请求页面，你会看到 "这是你第一次请求页面"。</span><span class="sxs-lookup"><span data-stu-id="db37d-267">Because this is the first time you're requested the page, you see "This is the first time you've requested the page".</span></span> <span data-ttu-id="db37d-268">该字符串是将消息变量初始化为的值。</span><span class="sxs-lookup"><span data-stu-id="db37d-268">That string is the value that you initialized the message variable to.</span></span> <span data-ttu-id="db37d-269">存在 if （IsPost）测试，但此时返回 false，因此 if 块内的代码不会运行。</span><span class="sxs-lookup"><span data-stu-id="db37d-269">There's an if(IsPost) test, but that returns false at the moment, so the code inside the if block doesn't run.</span></span>

<span data-ttu-id="db37d-270">单击 "**提交**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="db37d-270">Click the **Submit** button.</span></span> <span data-ttu-id="db37d-271">再次请求该页。</span><span class="sxs-lookup"><span data-stu-id="db37d-271">The page is requested again.</span></span> <span data-ttu-id="db37d-272">与之前一样，消息变量设置为 "这是第一次 ..."。</span><span class="sxs-lookup"><span data-stu-id="db37d-272">As before, the message variable is set to "This is the first time ...".</span></span> <span data-ttu-id="db37d-273">但这一次，测试 if （IsPost）将返回 true，因此 if 块内的代码会运行。</span><span class="sxs-lookup"><span data-stu-id="db37d-273">But this time, the test if(IsPost) returns true, so the code inside the if block runs.</span></span> <span data-ttu-id="db37d-274">该代码将消息变量的值更改为一个不同的值，这是标记中呈现的内容。</span><span class="sxs-lookup"><span data-stu-id="db37d-274">The code changes the value of the message variable to a different value, which is what's rendered in the markup.</span></span>

<span data-ttu-id="db37d-275">现在，在标记中添加 if 条件。</span><span class="sxs-lookup"><span data-stu-id="db37d-275">Now add an if condition in the markup.</span></span> <span data-ttu-id="db37d-276">在包含 "**提交**" 按钮的 &lt;p&gt; 元素下，添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="db37d-276">Below the &lt;p&gt; element that contains the **Submit** button, add the following markup:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

<span data-ttu-id="db37d-277">你将在标记内添加代码，因此必须从 @开始。</span><span class="sxs-lookup"><span data-stu-id="db37d-277">You're adding code inside the markup, so you have to start with @.</span></span> <span data-ttu-id="db37d-278">然后有一个 if 测试，它类似于你之前在代码块中添加的测试。</span><span class="sxs-lookup"><span data-stu-id="db37d-278">Then there's an if test similar to the one you added earlier up in the code block.</span></span> <span data-ttu-id="db37d-279">但在大括号内，你添加的是普通的 HTML，但至少在 @DateTime.Now之前，它是普通的。</span><span class="sxs-lookup"><span data-stu-id="db37d-279">Inside the braces, though, you're adding ordinary HTML — at least, it's ordinary until it gets to @DateTime.Now.</span></span> <span data-ttu-id="db37d-280">这是另一小段 Razor 代码，因此，您必须在其前面加上 @。</span><span class="sxs-lookup"><span data-stu-id="db37d-280">This is another little bit of Razor code, so again you have to add @ in front of it.</span></span>

<span data-ttu-id="db37d-281">此处的要点是，可以在顶部和标记中的代码块中添加条件。</span><span class="sxs-lookup"><span data-stu-id="db37d-281">The point here is that you can add if conditions in both the code block at the top and in the markup.</span></span> <span data-ttu-id="db37d-282">如果在页面的正文中使用 if 条件，则块内的行可以是标记或代码。</span><span class="sxs-lookup"><span data-stu-id="db37d-282">If you use an if condition in the body of the page, the lines inside the block can be markup or code.</span></span> <span data-ttu-id="db37d-283">在这种情况下，无论何时混合标记和代码，都必须使用 @ 以使其清楚地 ASP.NET 代码的位置。</span><span class="sxs-lookup"><span data-stu-id="db37d-283">In that case, and as is true anytime you mix markup and code, you have to use @ to make it clear to ASP.NET where the code is.</span></span>

<span data-ttu-id="db37d-284">运行页面，然后单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="db37d-284">Run the page and click **Submit**.</span></span> <span data-ttu-id="db37d-285">这种情况下，你不仅可以在提交时看到不同的消息（"现在已提交 ..."），而且你会看到一条新消息，其中列出了日期和时间。</span><span class="sxs-lookup"><span data-stu-id="db37d-285">This time you not only see a different message when you submit ("Now you've submitted ..."), but you see a new message that lists the date and time.</span></span>

![在浏览器中运行的 "Test Razor 2" 页面，在提交后显示时间戳](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a><span data-ttu-id="db37d-287">测试查询字符串的值</span><span class="sxs-lookup"><span data-stu-id="db37d-287">Testing the value of a query string</span></span>

<span data-ttu-id="db37d-288">再一次测试。</span><span class="sxs-lookup"><span data-stu-id="db37d-288">One more test.</span></span> <span data-ttu-id="db37d-289">这一次，你将添加一个用于测试在查询字符串中可能传递的名为 show 的值的 if 块。</span><span class="sxs-lookup"><span data-stu-id="db37d-289">This time, you'll add an if block that tests a value named show that might be passed in the query string.</span></span> <span data-ttu-id="db37d-290">（如下所示： `http://localhost:43097/TestRazorPart2.cshtml?show=true`）你将更改页面，以便仅当 show 的值为 true 时才显示已显示的消息（"这是第一个时间 ..." 等）。</span><span class="sxs-lookup"><span data-stu-id="db37d-290">(Like this: `http://localhost:43097/TestRazorPart2.cshtml?show=true`) You'll change the page so that the message you've been displaying ("This is the first time ...", etc.) is only displayed if the value of show is true.</span></span>

<span data-ttu-id="db37d-291">在页面顶部（但内部）代码块的底部，添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="db37d-291">At the bottom (but inside) the code block at the top of the page, add the following:</span></span>

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

<span data-ttu-id="db37d-292">完整的代码块现在如下例所示。</span><span class="sxs-lookup"><span data-stu-id="db37d-292">The complete code block now look like the following example.</span></span> <span data-ttu-id="db37d-293">（请记住，将代码复制到页面时，缩进的外观可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="db37d-293">(Remember that when you copy the code into your page, the indentation might look different.</span></span> <span data-ttu-id="db37d-294">但这不会影响代码的运行方式。）</span><span class="sxs-lookup"><span data-stu-id="db37d-294">But that doesn't affect how the code runs.)</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

<span data-ttu-id="db37d-295">该块中的新代码将名为 showMessage 的变量初始化为 false。</span><span class="sxs-lookup"><span data-stu-id="db37d-295">The new code in the block initializes a variable named showMessage to false.</span></span> <span data-ttu-id="db37d-296">然后，它会执行 if 测试，以在查询字符串中查找值。</span><span class="sxs-lookup"><span data-stu-id="db37d-296">It then does an if test to look for a value in the query string.</span></span> <span data-ttu-id="db37d-297">第一次请求页面时，它具有如下所示的 URL：</span><span class="sxs-lookup"><span data-stu-id="db37d-297">When you first request the page, it has a URL like this one:</span></span>

`http://localhost:43097/TestRazorPart2.cshtml`

<span data-ttu-id="db37d-298">此代码确定 URL 是否在查询字符串中包含一个名为 show 的变量，如 URL 的此版本所示：</span><span class="sxs-lookup"><span data-stu-id="db37d-298">The code determines whether the URL contains a variable named show in the query string, like this version of the URL:</span></span>

<span data-ttu-id="db37d-299">`http://localhost:43097/TestRazorPart2.cshtml`？ show = true</span><span class="sxs-lookup"><span data-stu-id="db37d-299">`http://localhost:43097/TestRazorPart2.cshtml`?show=true</span></span>

<span data-ttu-id="db37d-300">测试本身将查看 Request 对象的 QueryString 属性。</span><span class="sxs-lookup"><span data-stu-id="db37d-300">The test itself looks at the QueryString property of the Request object.</span></span> <span data-ttu-id="db37d-301">如果查询字符串包含名为 show 的项，并且该项设置为 true，则 if 块将运行，并将 showMessage 变量设置为 true。</span><span class="sxs-lookup"><span data-stu-id="db37d-301">If the query string contains an item named show, and if that item is set to true, the if block runs and sets the showMessage variable to true.</span></span>

<span data-ttu-id="db37d-302">这里有一种技巧，如您所见。</span><span class="sxs-lookup"><span data-stu-id="db37d-302">There's a trick here, as you can see.</span></span> <span data-ttu-id="db37d-303">如名称所示，查询字符串是一个字符串。</span><span class="sxs-lookup"><span data-stu-id="db37d-303">Like the name says, the query string is a string.</span></span> <span data-ttu-id="db37d-304">但是，如果要测试的值为布尔值（true/false），则只能测试 true 和 false。</span><span class="sxs-lookup"><span data-stu-id="db37d-304">However, you can only test for true and false if the value you're testing is a Boolean (true/false) value.</span></span> <span data-ttu-id="db37d-305">在查询字符串中显示变量的值之前，必须将其转换为布尔值。</span><span class="sxs-lookup"><span data-stu-id="db37d-305">Before you can test the value of the show variable in the query string, you have to convert it to a Boolean value.</span></span> <span data-ttu-id="db37d-306">这就是 AsBool 方法的作用，它采用字符串作为输入并将其转换为布尔值。</span><span class="sxs-lookup"><span data-stu-id="db37d-306">That's what the AsBool method does — it takes a string as input and converts it to a Boolean value.</span></span> <span data-ttu-id="db37d-307">显然，如果字符串为 "true"，则 AsBool 方法会将该值转换为 true。</span><span class="sxs-lookup"><span data-stu-id="db37d-307">Clearly, if the string is "true", the AsBool method converts that value to true.</span></span> <span data-ttu-id="db37d-308">如果字符串的值为其他值，则 AsBool 返回 false。</span><span class="sxs-lookup"><span data-stu-id="db37d-308">If the value of the string is anything else, AsBool returns false.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="db37d-309">**数据类型和 As （）方法**</span><span class="sxs-lookup"><span data-stu-id="db37d-309">**Data Types and As() Methods**</span></span>
> 
> <span data-ttu-id="db37d-310">到目前为止，我们只是在创建变量时使用关键字 var。</span><span class="sxs-lookup"><span data-stu-id="db37d-310">We've only said so far that when you create a variable, you use the keyword var.</span></span> <span data-ttu-id="db37d-311">但这并不完整。</span><span class="sxs-lookup"><span data-stu-id="db37d-311">That's not the entire story, though.</span></span> <span data-ttu-id="db37d-312">若要操作值（若要添加数字或连接字符串，或者比较日期或测试 true/false） C# ，必须使用适当的内部表示形式的值。</span><span class="sxs-lookup"><span data-stu-id="db37d-312">In order to manipulate values — to add numbers, or concatenate strings, or compare dates, or test for true/false — C# has to work with an appropriate internal representation of the value.</span></span> <span data-ttu-id="db37d-313">C#根据要对值执行的操作，*通常*可以确定表示形式应该是什么（即，数据的*类型*）。</span><span class="sxs-lookup"><span data-stu-id="db37d-313">C# can *usually* figure out what that representation should be (that is, what *type* the data is) based on what you're doing with the values.</span></span> <span data-ttu-id="db37d-314">不过，现在它无法做到这一点。</span><span class="sxs-lookup"><span data-stu-id="db37d-314">Now and then, though, it can't do that.</span></span> <span data-ttu-id="db37d-315">如果不是，则必须明确指出应该如何C#表示数据。</span><span class="sxs-lookup"><span data-stu-id="db37d-315">If not, you have to help out by explicitly indicating how C# should represent the data.</span></span> <span data-ttu-id="db37d-316">AsBool 方法执行此功能，它会C#告知字符串值 "true" 或 "false" 应被视为布尔值。</span><span class="sxs-lookup"><span data-stu-id="db37d-316">The AsBool method does that — it tells C# that a string value of "true" or "false" should be treated as a Boolean value.</span></span> <span data-ttu-id="db37d-317">也存在将字符串表示为其他类型的类似方法，例如 AsInt （视为一个整数）、AsDateTime （视为日期/时间）、AsFloat （视为浮点数）等。</span><span class="sxs-lookup"><span data-stu-id="db37d-317">Similar methods exist to represent strings as other types as well, like AsInt (treat as an integer), AsDateTime (treat as a date/time), AsFloat (treat as a floating-point number), and so on.</span></span> <span data-ttu-id="db37d-318">当你使用这些 As （）方法时， C#如果不能根据请求来表示字符串值，你会看到错误。</span><span class="sxs-lookup"><span data-stu-id="db37d-318">When you use these As( ) methods, if C# can't represent the string value as requested, you'll see an error.</span></span>

<span data-ttu-id="db37d-319">在页面的标记中，删除或注释掉此元素（此处显示注释掉）：</span><span class="sxs-lookup"><span data-stu-id="db37d-319">In the markup of the page, remove or comment out this element (here it's shown commented out):</span></span>

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

<span data-ttu-id="db37d-320">如果已删除或注释掉该文本，请添加以下内容：</span><span class="sxs-lookup"><span data-stu-id="db37d-320">Right where you removed or commented out that text, add the following:</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

<span data-ttu-id="db37d-321">If 测试表明，如果 showMessage 变量为 true，则将使用消息变量的值渲染 &lt;p&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="db37d-321">The if test says that if the showMessage variable is true, render a &lt;p&gt; element with the value of the message variable.</span></span>

### <a name="summary-of-your-conditional-logic"></a><span data-ttu-id="db37d-322">条件逻辑摘要</span><span class="sxs-lookup"><span data-stu-id="db37d-322">Summary of your conditional logic</span></span>

<span data-ttu-id="db37d-323">如果你并不完全确定刚刚完成的操作，则可以使用摘要。</span><span class="sxs-lookup"><span data-stu-id="db37d-323">In case you're not entirely sure of what you've just done, here's a summary.</span></span>

- <span data-ttu-id="db37d-324">消息变量将初始化为默认字符串（"这是第一次 ..."）。</span><span class="sxs-lookup"><span data-stu-id="db37d-324">The message variable is initialized to a default string ("This is the first time ...").</span></span>
- <span data-ttu-id="db37d-325">如果页面请求是提交（post）的结果，则 "消息" 的值将更改为 "现在已提交 ..."</span><span class="sxs-lookup"><span data-stu-id="db37d-325">If the page request is the result of a submit (post), the value of message is changed to "Now you've submitted ..."</span></span>
- <span data-ttu-id="db37d-326">ShowMessage 变量初始化为 false。</span><span class="sxs-lookup"><span data-stu-id="db37d-326">The showMessage variable is initialized to false.</span></span>
- <span data-ttu-id="db37d-327">如果查询字符串包含？ show = true，则将 showMessage 变量设置为 true。</span><span class="sxs-lookup"><span data-stu-id="db37d-327">If the query string contains ?show=true, the showMessage variable is set to true.</span></span>
- <span data-ttu-id="db37d-328">在标记中，如果 showMessage 为 true，则将呈现一个 &lt;p&gt; 元素，该元素显示 message 的值。</span><span class="sxs-lookup"><span data-stu-id="db37d-328">In the markup, if showMessage is true, a &lt;p&gt; element is rendered that shows the value of message.</span></span> <span data-ttu-id="db37d-329">（如果 showMessage 为 false，则不会在标记中的该点呈现任何内容。）</span><span class="sxs-lookup"><span data-stu-id="db37d-329">(If showMessage is false, nothing is rendered at that point in the markup.)</span></span>
- <span data-ttu-id="db37d-330">在标记中，如果请求是 post，则会呈现 &lt;p&gt; 元素，该元素显示日期和时间。</span><span class="sxs-lookup"><span data-stu-id="db37d-330">In the markup, if the request is a post, a &lt;p&gt; element is rendered that displays the date and time.</span></span>

<span data-ttu-id="db37d-331">运行页面。</span><span class="sxs-lookup"><span data-stu-id="db37d-331">Run the page.</span></span> <span data-ttu-id="db37d-332">没有消息，因为 showMessage 为 false，因此在标记中，if （showMessage）测试返回 false。</span><span class="sxs-lookup"><span data-stu-id="db37d-332">There's no message, because showMessage is false, so in the markup the if(showMessage) test returns false.</span></span>

<span data-ttu-id="db37d-333">单击“提交”。</span><span class="sxs-lookup"><span data-stu-id="db37d-333">Click **Submit**.</span></span> <span data-ttu-id="db37d-334">此时会显示日期和时间，但不会显示任何消息。</span><span class="sxs-lookup"><span data-stu-id="db37d-334">You see the date and time, but still no message.</span></span>

<span data-ttu-id="db37d-335">在浏览器中，选择 "URL" 框，并将以下内容添加到 URL 的末尾：？ show = true，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="db37d-335">In your browser, go to the URL box and add the following to the end of the URL: ?show=true and then press Enter.</span></span>

![显示查询字符串的浏览器中的 "Test Razor 2" 页](intro-to-web-pages-programming/_static/image5.png)

<span data-ttu-id="db37d-337">再次显示该页。</span><span class="sxs-lookup"><span data-stu-id="db37d-337">The page is displayed again.</span></span> <span data-ttu-id="db37d-338">（因为你更改了 URL，所以这是一个新请求，而不是提交。）再次单击 "**提交**"。</span><span class="sxs-lookup"><span data-stu-id="db37d-338">(Because you changed the URL, this is a new request, not a submit.) Click **Submit** again.</span></span> <span data-ttu-id="db37d-339">此时将再次显示该消息，如日期和时间。</span><span class="sxs-lookup"><span data-stu-id="db37d-339">The message is displayed again, as is the date and time.</span></span>

![如果有查询字符串，则在提交后出现 "Test Razor 2" 页](intro-to-web-pages-programming/_static/image6.png)

<span data-ttu-id="db37d-341">在 URL 中，更改？ show = true to？ show = false，然后按 Enter。</span><span class="sxs-lookup"><span data-stu-id="db37d-341">In the URL, change ?show=true to ?show=false and press Enter.</span></span> <span data-ttu-id="db37d-342">再次提交该页。</span><span class="sxs-lookup"><span data-stu-id="db37d-342">Submit the page again.</span></span> <span data-ttu-id="db37d-343">该页返回到你的开始方式-无消息。</span><span class="sxs-lookup"><span data-stu-id="db37d-343">The page is back to how you started — no message.</span></span>

<span data-ttu-id="db37d-344">如前所述，此示例的逻辑有点精心设计。</span><span class="sxs-lookup"><span data-stu-id="db37d-344">As noted earlier, the logic of this example is a little contrived.</span></span> <span data-ttu-id="db37d-345">但是，如果要在许多页面中显示，将需要你在此处看到的一个或多个窗体。</span><span class="sxs-lookup"><span data-stu-id="db37d-345">However, if is going to come up in many of your pages, and it will take one or more of the forms you've seen here.</span></span>

## <a name="installing-a-helper-displaying-a-gravatar-image"></a><span data-ttu-id="db37d-346">安装帮助程序（显示 Gravatar 的映像）</span><span class="sxs-lookup"><span data-stu-id="db37d-346">Installing a Helper (Displaying a Gravatar Image)</span></span>

<span data-ttu-id="db37d-347">用户经常想要在网页上执行的某些任务需要大量代码或需要额外的知识。</span><span class="sxs-lookup"><span data-stu-id="db37d-347">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="db37d-348">示例：显示数据图表;在页面上放置 Facebook "赞" 按钮;从网站发送电子邮件;裁剪或调整图像大小;为站点使用 PayPal。</span><span class="sxs-lookup"><span data-stu-id="db37d-348">Examples: displaying a chart for data; putting a Facebook "Like" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="db37d-349">为了便于执行这些类型的操作，ASP.NET 网页允许使用*帮助*程序。</span><span class="sxs-lookup"><span data-stu-id="db37d-349">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="db37d-350">帮助器是为站点安装的组件，可让你使用只需几行 Razor 代码执行典型任务。</span><span class="sxs-lookup"><span data-stu-id="db37d-350">Helpers are components that you install for a site and that let you perform typical tasks by using just a few lines of Razor code.</span></span>

<span data-ttu-id="db37d-351">ASP.NET 网页内置了几个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="db37d-351">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="db37d-352">但是，许多帮助程序都在使用 NuGet 包管理器提供的包（外接程序）中提供。</span><span class="sxs-lookup"><span data-stu-id="db37d-352">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="db37d-353">NuGet 允许您选择要安装的包，然后处理安装的所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="db37d-353">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

<span data-ttu-id="db37d-354">在本教程的此部分，将安装帮助器，以显示 Gravatar （"全局识别的头像"）图像。</span><span class="sxs-lookup"><span data-stu-id="db37d-354">In this part of the tutorial, you'll install a helper that lets you display a Gravatar ("globally recognized avatar") image.</span></span> <span data-ttu-id="db37d-355">你将了解两个问题。</span><span class="sxs-lookup"><span data-stu-id="db37d-355">You'll learn two things.</span></span> <span data-ttu-id="db37d-356">其中一种方法是查找并安装帮助程序。</span><span class="sxs-lookup"><span data-stu-id="db37d-356">One is how to find and install a helper.</span></span> <span data-ttu-id="db37d-357">你还将了解如何使用帮助程序轻松完成一些操作，你需要使用大量代码来完成此操作。</span><span class="sxs-lookup"><span data-stu-id="db37d-357">You'll also learn how a helper makes it easy to do something you'd otherwise need to do by using a lot of code you'd have to write yourself.</span></span>

<span data-ttu-id="db37d-358">你可以在[http://www.gravatar.com/](http://www.gravatar.com/)上的 Gravatar 网站注册自己的 Gravatar，但创建 Gravatar 帐户并不是必需的。</span><span class="sxs-lookup"><span data-stu-id="db37d-358">You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/), but it is not essential to create a Gravatar account to perform this part of the tutorial.</span></span>

<span data-ttu-id="db37d-359">在 WebMatrix 中，单击 " **NuGet** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="db37d-359">In WebMatrix, click the **NuGet** button.</span></span>

![WebMatrix 中的 "NuGet 库" 对话框](intro-to-web-pages-programming/_static/image7.png)

<span data-ttu-id="db37d-361">这会启动 NuGet 包管理器，并显示可用的包。</span><span class="sxs-lookup"><span data-stu-id="db37d-361">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="db37d-362">（并不是所有的包都是帮助者; 某些包将添加到 WebMatrix 本身，一些是其他模板，等等。）可能会收到有关版本不兼容的错误消息。</span><span class="sxs-lookup"><span data-stu-id="db37d-362">(Not all of the packages are helpers; some add functionality to WebMatrix itself, some are additional templates, and so on.) You may get an error message about version incompatibility.</span></span> <span data-ttu-id="db37d-363">您可以通过单击 **"确定"** 并继续学习本教程来忽略此错误消息。</span><span class="sxs-lookup"><span data-stu-id="db37d-363">You can ignore this error message by clicking **OK** and proceeding with this tutorial.</span></span>

![WebMatrix 中的 "NuGet 库" 对话框](intro-to-web-pages-programming/_static/image8.png)

<span data-ttu-id="db37d-365">在搜索框中，输入 "asp.net 帮助程序"。</span><span class="sxs-lookup"><span data-stu-id="db37d-365">In the search box, enter "asp.net helpers".</span></span> <span data-ttu-id="db37d-366">NuGet 显示与搜索词匹配的包。</span><span class="sxs-lookup"><span data-stu-id="db37d-366">NuGet shows the packages that match the search terms.</span></span>

![WebMatrix 中显示包的 NuGet 库](intro-to-web-pages-programming/_static/image9.png)

<span data-ttu-id="db37d-368">ASP.NET Web 帮助程序库包含用于简化许多常见任务（包括使用 Gravatar 映像）的代码。</span><span class="sxs-lookup"><span data-stu-id="db37d-368">The ASP.NET Web Helpers Library contains code to simplify many common tasks, including the use of Gravatar images.</span></span> <span data-ttu-id="db37d-369">选择**ASP.NET Web 助手库**包，然后单击 "**安装**" 以启动安装程序。</span><span class="sxs-lookup"><span data-stu-id="db37d-369">Select the **ASP.NET Web Helpers Library** package and then click **Install** to launch the installer.</span></span> <span data-ttu-id="db37d-370">当系统询问你是否要安装包，请选择 **"是"** ，并接受条款以完成安装。</span><span class="sxs-lookup"><span data-stu-id="db37d-370">Select **Yes** when asked if you want to install the package, and accept the terms to complete the installation.</span></span>

<span data-ttu-id="db37d-371">介绍完毕。</span><span class="sxs-lookup"><span data-stu-id="db37d-371">That's it.</span></span> <span data-ttu-id="db37d-372">NuGet 会下载并安装所有内容，包括可能需要的任何其他组件（*依赖项*）。</span><span class="sxs-lookup"><span data-stu-id="db37d-372">NuGet downloads and installs everything, including any additional components that might be required (*dependencies*).</span></span>

<span data-ttu-id="db37d-373">如果出于某种原因，您必须卸载帮助程序，该过程非常相似。</span><span class="sxs-lookup"><span data-stu-id="db37d-373">If for some reason you have to uninstall a helper, the process is very similar.</span></span> <span data-ttu-id="db37d-374">单击 " **NuGet** " 按钮，单击 "**已安装**" 选项卡，然后选择要卸载的包。</span><span class="sxs-lookup"><span data-stu-id="db37d-374">Click the **NuGet** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="using-a-helper-in-a-page"></a><span data-ttu-id="db37d-375">在页面中使用帮助器</span><span class="sxs-lookup"><span data-stu-id="db37d-375">Using a Helper in a Page</span></span>

<span data-ttu-id="db37d-376">现在，你将使用刚刚安装的帮助器。</span><span class="sxs-lookup"><span data-stu-id="db37d-376">Now you'll use the helper that you just installed.</span></span> <span data-ttu-id="db37d-377">对于大多数帮助器，向页面添加帮助程序的过程类似。</span><span class="sxs-lookup"><span data-stu-id="db37d-377">The process for adding a helper to a page is similar for most helpers.</span></span>

<span data-ttu-id="db37d-378">在 WebMatrix 中创建页面，并将其命名为*GravatarTest. cshml*。</span><span class="sxs-lookup"><span data-stu-id="db37d-378">In WebMatrix, create a page and name it *GravatarTest.cshml*.</span></span> <span data-ttu-id="db37d-379">（您要创建一个特殊页面来测试帮助程序，但您可以在站点的任何页中使用帮助程序。）</span><span class="sxs-lookup"><span data-stu-id="db37d-379">(You're creating a special page to test the helper, but you can use helpers in any page in your site.)</span></span>

<span data-ttu-id="db37d-380">在 &lt;主体&gt; 元素内，添加一个 &lt;div&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="db37d-380">Inside the &lt;body&gt; element, add a &lt;div&gt; element.</span></span> <span data-ttu-id="db37d-381">在 &lt;div&gt; 元素内，键入以下内容：</span><span class="sxs-lookup"><span data-stu-id="db37d-381">Inside the &lt;div&gt; element, type this:</span></span>

<span data-ttu-id="db37d-382">@Gravatar。</span><span class="sxs-lookup"><span data-stu-id="db37d-382">@Gravatar.</span></span>

<span data-ttu-id="db37d-383">@ 字符与用来标记 Razor 代码的字符相同。</span><span class="sxs-lookup"><span data-stu-id="db37d-383">The @ character is the same character you've been using to mark Razor code.</span></span> <span data-ttu-id="db37d-384">**Gravatar**是您正在使用的帮助程序对象。</span><span class="sxs-lookup"><span data-stu-id="db37d-384">**Gravatar** is the helper object that you're working with.</span></span>

<span data-ttu-id="db37d-385">一旦键入句点（.），WebMatrix 就会显示 Gravatar helper 提供的*方法*（函数）的列表：</span><span class="sxs-lookup"><span data-stu-id="db37d-385">As soon as you type the period (.), WebMatrix displays a list of *methods* (functions) that the Gravatar helper makes available:</span></span>

![Gravatar 帮助程序 IntelliSense 下拉列表](intro-to-web-pages-programming/_static/image10.png)

<span data-ttu-id="db37d-387">此功能称为*IntelliSense*。</span><span class="sxs-lookup"><span data-stu-id="db37d-387">This feature is known as *IntelliSense*.</span></span> <span data-ttu-id="db37d-388">它通过提供上下文相关的选项来帮助你进行编码。</span><span class="sxs-lookup"><span data-stu-id="db37d-388">It helps you code by providing context-appropriate choices.</span></span> <span data-ttu-id="db37d-389">IntelliSense 适用于在 WebMatrix 中受支持的 HTML、CSS、ASP.NET 代码、JavaScript 和其他语言。</span><span class="sxs-lookup"><span data-stu-id="db37d-389">IntelliSense works with HTML, CSS, ASP.NET code, JavaScript, and other languages that are supported in WebMatrix.</span></span> <span data-ttu-id="db37d-390">这是另一项功能，可更轻松地在 WebMatrix 中开发网页。</span><span class="sxs-lookup"><span data-stu-id="db37d-390">It's another feature that makes it easier to develop web pages in WebMatrix.</span></span>

<span data-ttu-id="db37d-391">在键盘上按 G，你会看到 IntelliSense 查找 GetHtml 方法。</span><span class="sxs-lookup"><span data-stu-id="db37d-391">Press G on the keyboard, and you see that IntelliSense finds the GetHtml method.</span></span> <span data-ttu-id="db37d-392">按 Tab。 IntelliSense 会插入所选的方法（GetHtml）。</span><span class="sxs-lookup"><span data-stu-id="db37d-392">Press Tab. IntelliSense inserts the selected method (GetHtml) for you.</span></span> <span data-ttu-id="db37d-393">键入一个左括号，并注意右括号会自动添加。</span><span class="sxs-lookup"><span data-stu-id="db37d-393">Type an open parenthesis, and notice that the closing parenthesis is automatically added.</span></span> <span data-ttu-id="db37d-394">在两个括号之间键入电子邮件地址，用引号引起来。</span><span class="sxs-lookup"><span data-stu-id="db37d-394">Type your email address in quotation marks between the two parenthesis.</span></span> <span data-ttu-id="db37d-395">如果你有一个 Gravatar 帐户，将返回你的个人资料图片。</span><span class="sxs-lookup"><span data-stu-id="db37d-395">If you have a Gravatar account, your profile picture will be returned.</span></span> <span data-ttu-id="db37d-396">如果没有 Gravatar 帐户，将返回默认映像。</span><span class="sxs-lookup"><span data-stu-id="db37d-396">If you do not have a Gravatar account, a default image is returned.</span></span> <span data-ttu-id="db37d-397">完成后，该行如下所示：</span><span class="sxs-lookup"><span data-stu-id="db37d-397">When you're done, the line looks like this:</span></span>

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

<span data-ttu-id="db37d-398">现在，在浏览器中查看页面。</span><span class="sxs-lookup"><span data-stu-id="db37d-398">Now view the page in a browser.</span></span> <span data-ttu-id="db37d-399">你的照片或默认图像将显示，具体取决于你是否有 Gravatar 帐户。</span><span class="sxs-lookup"><span data-stu-id="db37d-399">Either your picture or the default image is displayed, depending on whether you have a Gravatar account.</span></span>

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![默认图像](intro-to-web-pages-programming/_static/image12.png)

<span data-ttu-id="db37d-402">若要了解帮助程序的作用，请在浏览器中查看该页的源。</span><span class="sxs-lookup"><span data-stu-id="db37d-402">To get an idea of what the helper is doing for you, view the source of the page in the browser.</span></span> <span data-ttu-id="db37d-403">除了页面中包含的 HTML 外，还会看到一个包含标识符的图像元素。</span><span class="sxs-lookup"><span data-stu-id="db37d-403">Along with the HTML that you had in your page, you see an image element that includes an identifier.</span></span> <span data-ttu-id="db37d-404">这是帮助程序在您已 @Gravatar.GetHtml的位置呈现的页中的代码。</span><span class="sxs-lookup"><span data-stu-id="db37d-404">This is code that the helper rendered into the page at the place where you had @Gravatar.GetHtml.</span></span> <span data-ttu-id="db37d-405">帮助器采取了提供的信息并生成了直接与 Gravatar 进行通信的代码，以便为所提供的帐户恢复正确的映像。</span><span class="sxs-lookup"><span data-stu-id="db37d-405">The helper took the information you provided and generated the code that talks directly to Gravatar in order to get back the correct image for supplied account.</span></span>

<span data-ttu-id="db37d-406">使用 GetHtml 方法，还可以通过提供其他参数来自定义映像。</span><span class="sxs-lookup"><span data-stu-id="db37d-406">The GetHtml method also enables you to customize the image by providing other parameters.</span></span> <span data-ttu-id="db37d-407">下面的代码演示如何请求图像的宽度和高度均为40像素，如果指定的帐户不存在，则使用名为**wavatar**的指定默认图像。</span><span class="sxs-lookup"><span data-stu-id="db37d-407">The following code shows how to request an image has a width and height of 40 pixels, and uses a specified default image named **wavatar** if the specified account does not exist.</span></span>

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

<span data-ttu-id="db37d-408">此代码将产生类似于以下结果的内容（默认图像将随机改变）。</span><span class="sxs-lookup"><span data-stu-id="db37d-408">This code produces something like the following result (the default image will randomly vary).</span></span>

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a><span data-ttu-id="db37d-409">下一步</span><span class="sxs-lookup"><span data-stu-id="db37d-409">Coming Up Next</span></span>

<span data-ttu-id="db37d-410">为了使本教程简短，我们只关注几个基础知识。</span><span class="sxs-lookup"><span data-stu-id="db37d-410">To keep this tutorial short, we had to focus on only a few basics.</span></span> <span data-ttu-id="db37d-411">从本质上来说，更多*的是*Razor C#和。</span><span class="sxs-lookup"><span data-stu-id="db37d-411">Naturally, there's a *lot* more to Razor and C#.</span></span> <span data-ttu-id="db37d-412">在学习这些教程时，你将了解更多。</span><span class="sxs-lookup"><span data-stu-id="db37d-412">You'll learn more as you go through these tutorials.</span></span> <span data-ttu-id="db37d-413">如果希望了解有关 Razor 和C#更高的编程方面的详细信息，可以阅读此处的更详尽的介绍：[使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)。</span><span class="sxs-lookup"><span data-stu-id="db37d-413">If you're interested in learning more about the programming aspects of Razor and C# right now, you can read a more thorough introduction here: [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkID=202890).</span></span>

<span data-ttu-id="db37d-414">下一教程将介绍如何使用数据库。</span><span class="sxs-lookup"><span data-stu-id="db37d-414">The next tutorial introduces you to working with a database.</span></span> <span data-ttu-id="db37d-415">在本教程中，您将开始创建一个示例应用程序，该应用程序使您能够列出您最喜爱的电影。</span><span class="sxs-lookup"><span data-stu-id="db37d-415">In that tutorial, you'll begin creating the sample application that lets you list your favorite movies.</span></span>

## <a name="complete-listing-for-testrazor-page"></a><span data-ttu-id="db37d-416">TestRazor 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="db37d-416">Complete Listing for TestRazor Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a><span data-ttu-id="db37d-417">TestRazorPart2 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="db37d-417">Complete Listing for TestRazorPart2 Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a><span data-ttu-id="db37d-418">GravatarTest 页的完整列表</span><span class="sxs-lookup"><span data-stu-id="db37d-418">Complete Listing for GravatarTest Page</span></span>

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="db37d-419">其他资源</span><span class="sxs-lookup"><span data-stu-id="db37d-419">Additional Resources</span></span>

- [<span data-ttu-id="db37d-420">使用 Razor 语法的 ASP.NET Web 编程简介</span><span class="sxs-lookup"><span data-stu-id="db37d-420">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- [<span data-ttu-id="db37d-421">Twitter 帮助程序</span><span class="sxs-lookup"><span data-stu-id="db37d-421">Twitter helper</span></span>](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> <span data-ttu-id="db37d-422">[上一页](getting-started.md)
> [下一页](displaying-data.md)</span><span class="sxs-lookup"><span data-stu-id="db37d-422">[Previous](getting-started.md)
[Next](displaying-data.md)</span></span>
