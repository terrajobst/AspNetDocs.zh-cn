---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: 调试 ASP.NET 网页（Razor）站点简介 |Microsoft Docs
author: Rick-Anderson
description: 调试是在代码页中查找和修复错误的过程。 本章介绍了一些可用于调试和分析的工具和技术 。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: ae7d871e56326610c043dc20fe6e0919e1b4ac89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506456"
---
# <a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a><span data-ttu-id="1a4fd-104">调试 ASP.NET 网页（Razor）站点简介</span><span class="sxs-lookup"><span data-stu-id="1a4fd-104">Introduction to Debugging ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="1a4fd-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="1a4fd-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="1a4fd-106">本文介绍了在 ASP.NET 网页（Razor）网站中调试页面的各种方式。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-106">This article explains various ways to debug pages in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="1a4fd-107">调试是在代码页中查找和修复错误的过程。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-107">Debugging is the process of finding and fixing errors in your code pages.</span></span>
>
> <span data-ttu-id="1a4fd-108">**你将学习的内容：**</span><span class="sxs-lookup"><span data-stu-id="1a4fd-108">**What you'll learn:**</span></span>
>
> - <span data-ttu-id="1a4fd-109">如何显示帮助分析和调试页面的信息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-109">How to display information that helps analyze and debug pages.</span></span>
> - <span data-ttu-id="1a4fd-110">如何在 Visual Studio 中使用调试工具。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-110">How to use debugging tools in Visual Studio.</span></span>
>
>
> <span data-ttu-id="1a4fd-111">下面是本文中介绍的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="1a4fd-111">These are the ASP.NET features introduced in the article:</span></span>
>
> - <span data-ttu-id="1a4fd-112">`ServerInfo` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-112">The `ServerInfo` helper.</span></span>
> - <span data-ttu-id="1a4fd-113">`ObjectInfo` 帮助程序。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-113">`ObjectInfo` helper.</span></span>
>
>
> ## <a name="software-versions"></a><span data-ttu-id="1a4fd-114">软件版本</span><span class="sxs-lookup"><span data-stu-id="1a4fd-114">Software versions</span></span>
>
>
> - <span data-ttu-id="1a4fd-115">ASP.NET 网页（Razor）3</span><span class="sxs-lookup"><span data-stu-id="1a4fd-115">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="1a4fd-116">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="1a4fd-116">Visual Studio 2013</span></span>
>
>
> <span data-ttu-id="1a4fd-117">本教程还适用于 ASP.NET 网页2。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-117">This tutorial also works with ASP.NET Web Pages 2.</span></span> <span data-ttu-id="1a4fd-118">可以使用 WebMatrix 3，但不支持集成调试器。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-118">You can use WebMatrix 3 but the integrated debugger is not supported.</span></span>

<span data-ttu-id="1a4fd-119">解决代码中的错误和问题的一个重要方面是，首先要避免这些错误。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-119">An important aspect of troubleshooting errors and problems in your code is to avoid them in the first place.</span></span> <span data-ttu-id="1a4fd-120">可以通过将可能导致错误的代码部分放入 `try/catch` 块来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-120">You can do that by putting sections of your code that are likely to cause errors into `try/catch` blocks.</span></span> <span data-ttu-id="1a4fd-121">有关详细信息，请参阅[使用 Razor 语法对 ASP.NET Web 编程的介绍](https://go.microsoft.com/fwlink/?LinkId=202890)中有关处理错误的部分。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-121">For more information, see the section on handling errors in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890).</span></span>

<span data-ttu-id="1a4fd-122">`ServerInfo` 帮助器是一个诊断工具，可提供有关承载页面的 web 服务器环境的信息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-122">The `ServerInfo` helper is a diagnostic tool that gives you an overview of information about the web server environment that hosts your page.</span></span> <span data-ttu-id="1a4fd-123">它还显示了当浏览器请求页面时发送的 HTTP 请求信息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-123">It also shows you HTTP request information that's sent when a browser requests the page.</span></span> <span data-ttu-id="1a4fd-124">`ServerInfo` 帮助程序显示当前用户标识、发出请求的浏览器的类型，等等。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-124">The `ServerInfo` helper displays the current user identity, the type of browser that made the request, and so on.</span></span> <span data-ttu-id="1a4fd-125">此类信息可帮助你解决常见问题。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-125">This kind of information can help you troubleshoot common issues.</span></span>

1. <span data-ttu-id="1a4fd-126">创建名为*ServerInfo*的新网页。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-126">Create a new web page named *ServerInfo.cshtml*.</span></span>
2. <span data-ttu-id="1a4fd-127">在页面末尾，紧靠在结束 `</body>` 标记之前，添加 `@ServerInfo.GetHtml()`：</span><span class="sxs-lookup"><span data-stu-id="1a4fd-127">At the end of the page, just before the closing `</body>` tag, add `@ServerInfo.GetHtml()`:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    <span data-ttu-id="1a4fd-128">可以将 `ServerInfo` 代码添加到页面中的任意位置。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-128">You can add the `ServerInfo` code anywhere in the page.</span></span> <span data-ttu-id="1a4fd-129">但在结尾处添加它会使其输出与其他页面内容分离，使其更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-129">But adding it at the end will keep its output separate from your other page content, which makes it easier to read.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="1a4fd-130">**重要提示**在将网页移动到生产服务器之前，应该从网页中删除任何诊断代码。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-130">**Important** You should remove any diagnostic code from your web pages before you move web pages to a production server.</span></span> <span data-ttu-id="1a4fd-131">这适用于 `ServerInfo` 帮助程序以及本文中涉及将代码添加到页面的其他诊断技术。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-131">This applies to the `ServerInfo` helper as well as the other diagnostic techniques in this article that involve adding code to a page.</span></span> <span data-ttu-id="1a4fd-132">您不希望您的网站访问者查看有关您的服务器名称、用户名、服务器上的路径和类似详细信息的信息，因为这种类型的信息可能对具有恶意行为的用户非常有用。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-132">You don't want your website visitors to see information about your server name, user names, paths on your server, and similar details, because this type of information might be useful to people with malicious intent.</span></span>
3. <span data-ttu-id="1a4fd-133">保存页面并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-133">Save the page and run it in a browser.</span></span>

    ![调试-1](introduction-to-debugging/_static/image1.jpg)

    <span data-ttu-id="1a4fd-135">`ServerInfo` 帮助程序在页面中显示四个信息表：</span><span class="sxs-lookup"><span data-stu-id="1a4fd-135">The `ServerInfo` helper displays four tables of information in the page:</span></span>

   - <span data-ttu-id="1a4fd-136">服务器配置。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-136">Server Configuration.</span></span> <span data-ttu-id="1a4fd-137">本部分提供有关托管 web 服务器的信息，包括计算机名称、正在运行的 ASP.NET 的版本、域名和服务器时间。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-137">This section provides information about the hosting web server, including computer name, the version of ASP.NET you're running, the domain name, and server time.</span></span>
   - <span data-ttu-id="1a4fd-138">ASP.NET 服务器变量。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-138">ASP.NET Server Variables.</span></span> <span data-ttu-id="1a4fd-139">本部分提供有关多个 HTTP 协议的详细信息（称为 HTTP 变量）和每个网页请求中包含的值的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-139">This section provides details about the many HTTP protocol details (called HTTP variables) and values that are part of each web page request.</span></span>
   - <span data-ttu-id="1a4fd-140">HTTP 运行时信息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-140">HTTP Runtime Information.</span></span> <span data-ttu-id="1a4fd-141">本部分提供有关在其下运行网页的 Microsoft .NET 框架的版本、路径、有关缓存的详细信息等的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-141">This section provides details about that the version of the Microsoft .NET Framework that your web page is running under, the path, details about the cache, and so on.</span></span> <span data-ttu-id="1a4fd-142">（正如您在[使用 Razor 语法的 ASP.NET Web 编程](https://go.microsoft.com/fwlink/?LinkId=202890)中所学到的那样，使用 Razor 语法的 ASP.NET 网页是在 Microsoft 的 ASP.NET web 服务器技术的基础上构建的，它本身构建于一个称为 .NET Framework 的广泛软件开发库之上。）</span><span class="sxs-lookup"><span data-stu-id="1a4fd-142">(As you learned in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890), ASP.NET Web Pages using the Razor syntax are built on Microsoft's ASP.NET web server technology, which is itself built on an extensive software development library called the .NET Framework.)</span></span>
   - <span data-ttu-id="1a4fd-143">环境变量。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-143">Environment Variables.</span></span> <span data-ttu-id="1a4fd-144">本部分提供了 web 服务器上所有本地环境变量及其值的列表。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-144">This section provides a list of all the local environment variables and their values on the web server.</span></span>

     <span data-ttu-id="1a4fd-145">所有服务器和请求信息的完整说明超出了本文的范围，但你可以看到 `ServerInfo` 帮助程序返回了大量诊断信息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-145">A full description of all the server and request information is beyond the scope of this article, but you can see that the `ServerInfo` helper returns a lot of diagnostic information.</span></span> <span data-ttu-id="1a4fd-146">有关 `ServerInfo` 返回的值的详细信息，请参阅 MSDN 网站上的 Microsoft TechNet 网站和[IIS 服务器变量](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)上[可识别的环境变量](https://technet.microsoft.com/library/dd560744(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-146">For more information about the values that `ServerInfo` returns, see [Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) on the Microsoft TechNet website and [IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) on the MSDN website.</span></span>

## <a name="embedding-output-expressions-to-display-page-values"></a><span data-ttu-id="1a4fd-147">嵌入用于显示页面值的输出表达式</span><span class="sxs-lookup"><span data-stu-id="1a4fd-147">Embedding Output Expressions to Display Page Values</span></span>

<span data-ttu-id="1a4fd-148">查看代码中发生的情况的另一种方法是在页中嵌入输出表达式。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-148">Another way to see what's happening in your code is to embed output expressions in the page.</span></span> <span data-ttu-id="1a4fd-149">如您所知，可以通过将 `@myVariable` 或 `@(subTotal * 12)` 等内容添加到页面，直接输出变量的值。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-149">As you know, you can directly output the value of a variable by adding something like `@myVariable` or `@(subTotal * 12)` to the page.</span></span> <span data-ttu-id="1a4fd-150">对于调试，可以在代码中的战略点放置这些输出表达式。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-150">For debugging, you can place these output expressions at strategic points in your code.</span></span> <span data-ttu-id="1a4fd-151">这使您可以在页面运行时查看关键变量的值或计算的结果。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-151">This enables you to see the value of key variables or the result of calculations when your page runs.</span></span> <span data-ttu-id="1a4fd-152">完成调试后，可以删除表达式或将其注释掉。此过程说明了使用嵌入表达式来帮助调试页的典型方法。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-152">When you're done debugging, you can remove the expressions or comment them out. This procedure illustrates a typical way to use embedded expressions to help debug a page.</span></span>

1. <span data-ttu-id="1a4fd-153">创建名为*OutputExpression*的新 WebMatrix 页面。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-153">Create a new WebMatrix page that's named *OutputExpression.cshtml*.</span></span>
2. <span data-ttu-id="1a4fd-154">将页面内容替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="1a4fd-154">Replace the page content with the following:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    <span data-ttu-id="1a4fd-155">该示例使用 `switch` 语句来检查 `weekday` 变量的值，然后根据它的星期几显示不同的输出消息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-155">The example uses a `switch` statement to check the value of the `weekday` variable and then display a different output message depending on which day of the week it is.</span></span> <span data-ttu-id="1a4fd-156">在此示例中，第一个代码块中的 `if` 块会通过将一天添加到当前工作日值来随意更改一周中的某一天。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-156">In the example, the `if` block within the first code block arbitrarily changes the day of the week by adding one day to the current weekday value.</span></span> <span data-ttu-id="1a4fd-157">这是出于说明目的导致的错误。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-157">This is an error introduced for illustration purposes.</span></span>
3. <span data-ttu-id="1a4fd-158">保存页面并在浏览器中运行它。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-158">Save the page and run it in a browser.</span></span>

    <span data-ttu-id="1a4fd-159">该页显示一周中错误日期的消息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-159">The page displays the message for the wrong day of the week.</span></span> <span data-ttu-id="1a4fd-160">无论当天的哪一天，你都可以在一天后看到消息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-160">Whatever day of the week it actually is, you'll see the message for one day later.</span></span> <span data-ttu-id="1a4fd-161">尽管在此情况下，你知道消息处于关闭状态的原因（因为代码特意设置了不正确的日期值），但在这种情况下，通常很难知道代码中发生错误的位置。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-161">Although in this case you know why the message is off (because the code deliberately sets the incorrect day value), in reality it's often hard to know where things are going wrong in the code.</span></span> <span data-ttu-id="1a4fd-162">若要进行调试，需要了解关键对象和变量（如 `weekday`）的值发生了什么情况。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-162">To debug, you need to find out what's happening to the value of key objects and variables such as `weekday`.</span></span>
4. <span data-ttu-id="1a4fd-163">通过插入 `@weekday` 来添加输出表达式，如代码中的注释所示。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-163">Add output expressions by inserting `@weekday` as shown in the two places indicated by comments in the code.</span></span> <span data-ttu-id="1a4fd-164">这些输出表达式会在代码执行中显示变量的值。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-164">These output expressions will display the values of the variable at that point in the code execution.</span></span>

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. <span data-ttu-id="1a4fd-165">保存并在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-165">Save and run the page in a browser.</span></span>

    <span data-ttu-id="1a4fd-166">该页首先显示一周中的某一天，然后是从第一天开始得到的更新日期，然后是从 `switch` 语句产生的消息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-166">The page displays the real day of the week first, then the updated day of the week that results from adding one day, and then the resulting message from the `switch` statement.</span></span> <span data-ttu-id="1a4fd-167">由于未向输出添加任何 HTML `<p>` 标记，因此两个变量表达式（`@weekday`）的输出在不同的日期之间没有空格。表达式仅用于测试。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-167">The output from the two variable expressions (`@weekday`) has no spaces between the days because you didn't add any HTML `<p>` tags to the output; the expressions are just for testing.</span></span>

    ![调试-2](introduction-to-debugging/_static/image2.jpg)

    <span data-ttu-id="1a4fd-169">现在，你可以看到错误的位置。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-169">Now you can see where the error is.</span></span> <span data-ttu-id="1a4fd-170">在代码中首次显示 `weekday` 变量时，它将显示正确的日期。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-170">When you first display the `weekday` variable in the code, it shows the correct day.</span></span> <span data-ttu-id="1a4fd-171">当第二次显示时，在代码中 `if` 块后，一天将关闭。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-171">When you display it the second time, after the `if` block in the code, the day is off by one.</span></span> <span data-ttu-id="1a4fd-172">因此，您知道 weekday 变量的第一个和第二个外观之间发生了某些情况。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-172">So you know that something has happened between the first and second appearance of the weekday variable.</span></span> <span data-ttu-id="1a4fd-173">如果这是一个真实 bug，这种方法可帮助您缩小引起问题的代码的位置。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-173">If this were a real bug, this kind of approach would help you narrow down the location of the code that's causing the problem.</span></span>
6. <span data-ttu-id="1a4fd-174">通过删除添加的两个输出表达式，并删除更改周中某天的代码，修复页面中的代码。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-174">Fix the code in the page by removing the two output expressions you added, and removing the code that changes the day of the week.</span></span> <span data-ttu-id="1a4fd-175">其余的完整代码块如下例所示：</span><span class="sxs-lookup"><span data-stu-id="1a4fd-175">The remaining, complete block of code looks like the following example:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. <span data-ttu-id="1a4fd-176">在浏览器中运行页。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-176">Run the page in a browser.</span></span> <span data-ttu-id="1a4fd-177">此时会看到显示的消息的正确消息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-177">This time you see the correct message displayed for the actual day of the week.</span></span>

## <a name="using-the-objectinfo-helper-to-display-object-values"></a><span data-ttu-id="1a4fd-178">使用 ObjectInfo 帮助器显示对象值</span><span class="sxs-lookup"><span data-stu-id="1a4fd-178">Using the ObjectInfo Helper to Display Object Values</span></span>

<span data-ttu-id="1a4fd-179">`ObjectInfo` 帮助程序显示您传递给它的每个对象的类型和值。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-179">The `ObjectInfo` helper displays the type and the value of each object you pass to it.</span></span> <span data-ttu-id="1a4fd-180">您可以使用它查看代码中变量和对象的值（与上一示例中的输出表达式一样），还可以看到有关对象的数据类型信息。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-180">You can use it to view the value of variables and objects in your code (like you did with output expressions in the previous example), plus you can see data type information about the object.</span></span>

1. <span data-ttu-id="1a4fd-181">打开前面创建的名为*OutputExpression*的文件。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-181">Open the file named *OutputExpression.cshtml* that you created earlier.</span></span>
2. <span data-ttu-id="1a4fd-182">将页面中的所有代码替换为以下代码块：</span><span class="sxs-lookup"><span data-stu-id="1a4fd-182">Replace all code in the page with the following block of code:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. <span data-ttu-id="1a4fd-183">保存并在浏览器中运行页面。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-183">Save and run the page in a browser.</span></span>

    ![调试-4](introduction-to-debugging/_static/image3.jpg)

    <span data-ttu-id="1a4fd-185">在此示例中，`ObjectInfo` 帮助程序显示两个项：</span><span class="sxs-lookup"><span data-stu-id="1a4fd-185">In this example, the `ObjectInfo` helper displays two items:</span></span>

   - <span data-ttu-id="1a4fd-186">类型。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-186">The type.</span></span> <span data-ttu-id="1a4fd-187">对于第一个变量，类型为 `DayOfWeek`。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-187">For the first variable, the type is `DayOfWeek`.</span></span> <span data-ttu-id="1a4fd-188">对于第二个变量，类型为 `String`。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-188">For the second variable, the type is `String`.</span></span>
   - <span data-ttu-id="1a4fd-189">值。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-189">The value.</span></span> <span data-ttu-id="1a4fd-190">在这种情况下，由于您已经在页面中显示了问候语变量的值，因此当您将该变量传递给 `ObjectInfo`时，将再次显示此值。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-190">In this case, because you already display the value of the greeting variable in the page, the value is displayed again when you pass the variable to `ObjectInfo`.</span></span>

     <span data-ttu-id="1a4fd-191">对于更复杂的对象，`ObjectInfo` 帮助器&#8212;基本上可以显示更多信息，它可以显示对象的所有属性的类型和值。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-191">For more complex objects, the `ObjectInfo` helper can display more information &#8212; basically, it can display the types and values of all of an object's properties.</span></span>

## <a name="using-debugging-tools-in-visual-studio"></a><span data-ttu-id="1a4fd-192">在 Visual Studio 中使用调试工具</span><span class="sxs-lookup"><span data-stu-id="1a4fd-192">Using Debugging Tools in Visual Studio</span></span>

<span data-ttu-id="1a4fd-193">若要获得更全面的调试体验，请使用[Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-193">For a more comprehensive debugging experience, use [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="1a4fd-194">使用 Visual Studio，可以在代码中要检查的行处设置断点。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-194">With Visual Studio, you can set a breakpoint in your code at the line that you want to inspect.</span></span>

![设置断点](introduction-to-debugging/_static/image1.png)

<span data-ttu-id="1a4fd-196">测试网站时，执行代码将在断点处暂停。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-196">When you test the web site, the executing code halts at the breakpoint.</span></span>

![到达断点](introduction-to-debugging/_static/image2.png)

<span data-ttu-id="1a4fd-198">你可以检查变量的当前值，并逐行执行代码。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-198">You can examine the current values of the variables, and step through the code line-by-line.</span></span>

![查看值](introduction-to-debugging/_static/image3.png)

<span data-ttu-id="1a4fd-200">有关使用 Visual Studio 中的集成调试器调试 ASP.NET Razor 页面的信息，请参阅[使用 Visual studio 进行编程 ASP.NET 网页（Razor）](https://go.microsoft.com/fwlink/?LinkId=205854)。</span><span class="sxs-lookup"><span data-stu-id="1a4fd-200">For information about using the integrated debugger in Visual Studio to debug ASP.NET Razor pages, see [Programming ASP.NET Web Pages (Razor) Using Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1a4fd-201">其他资源</span><span class="sxs-lookup"><span data-stu-id="1a4fd-201">Additional Resources</span></span>

- [<span data-ttu-id="1a4fd-202">使用 Visual Studio 的编程 ASP.NET 网页（Razor）</span><span class="sxs-lookup"><span data-stu-id="1a4fd-202">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?LinkId=205854)
- <span data-ttu-id="1a4fd-203">[IIS 服务器变量](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)（MSDN）</span><span class="sxs-lookup"><span data-stu-id="1a4fd-203">[IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)</span></span>
- <span data-ttu-id="1a4fd-204">[识别的环境变量](https://technet.microsoft.com/library/dd560744(WS.10).aspx)（TechNet）</span><span class="sxs-lookup"><span data-stu-id="1a4fd-204">[Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)</span></span>
