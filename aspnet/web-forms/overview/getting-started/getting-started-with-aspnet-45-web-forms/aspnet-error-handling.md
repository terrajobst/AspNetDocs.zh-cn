---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 错误处理 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识, 并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: f420be369801208fa875d9a60e6e154afbe84aa7
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995309"
---
# <a name="aspnet-error-handling"></a><span data-ttu-id="1f535-103">ASP.NET 错误处理</span><span class="sxs-lookup"><span data-stu-id="1f535-103">ASP.NET Error Handling</span></span>

<span data-ttu-id="1f535-104">作者: [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="1f535-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="1f535-105">[下载 Wingtip 玩具示例项目 (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书 (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="1f535-105">[Download Wingtip Toys Sample Project (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="1f535-106">本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识, 并为 Web Microsoft Visual Studio Express 2013。</span><span class="sxs-lookup"><span data-stu-id="1f535-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="1f535-107">此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。</span><span class="sxs-lookup"><span data-stu-id="1f535-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="1f535-108">在本教程中, 您将修改 Wingtip 玩具示例应用程序以包括错误处理和错误日志记录。</span><span class="sxs-lookup"><span data-stu-id="1f535-108">In this tutorial, you will modify the Wingtip Toys sample application to include error handling and error logging.</span></span> <span data-ttu-id="1f535-109">错误处理将使应用程序能够正常处理错误并相应地显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="1f535-109">Error handling will allow the application to gracefully handle errors and display error messages accordingly.</span></span> <span data-ttu-id="1f535-110">错误日志记录将允许你查找并修复已发生的错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-110">Error logging will allow you to find and fix errors that have occurred.</span></span> <span data-ttu-id="1f535-111">本教程以上一教程 "URL 路由" 为基础, 是 Wingtip 玩具教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="1f535-111">This tutorial builds on the previous tutorial "URL Routing" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="1f535-112">你将学习的内容:</span><span class="sxs-lookup"><span data-stu-id="1f535-112">What you'll learn:</span></span>

- <span data-ttu-id="1f535-113">如何将全局错误处理添加到应用程序的配置。</span><span class="sxs-lookup"><span data-stu-id="1f535-113">How to add global error handling to the application's configuration.</span></span>
- <span data-ttu-id="1f535-114">如何在应用程序、页和代码级别添加错误处理。</span><span class="sxs-lookup"><span data-stu-id="1f535-114">How to add error handling at the application, page, and code levels.</span></span>
- <span data-ttu-id="1f535-115">如何记录错误供以后查看。</span><span class="sxs-lookup"><span data-stu-id="1f535-115">How to log errors for later review.</span></span>
- <span data-ttu-id="1f535-116">如何显示不损害安全的错误消息。</span><span class="sxs-lookup"><span data-stu-id="1f535-116">How to display error messages that do not compromise security.</span></span>
- <span data-ttu-id="1f535-117">如何实现错误日志记录模块和处理程序 (ELMAH) 错误日志记录。</span><span class="sxs-lookup"><span data-stu-id="1f535-117">How to implement Error Logging Modules and Handlers (ELMAH) error logging.</span></span>

## <a name="overview"></a><span data-ttu-id="1f535-118">概述</span><span class="sxs-lookup"><span data-stu-id="1f535-118">Overview</span></span>

<span data-ttu-id="1f535-119">ASP.NET 应用程序必须能够以一致的方式处理执行期间发生的错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-119">ASP.NET applications must be able to handle errors that occur during execution in a consistent manner.</span></span> <span data-ttu-id="1f535-120">ASP.NET 使用公共语言运行时 (CLR), 这提供了一种以统一方式向应用程序通知错误的方式。</span><span class="sxs-lookup"><span data-stu-id="1f535-120">ASP.NET uses the common language runtime (CLR), which provides a way of notifying applications of errors in a uniform way.</span></span> <span data-ttu-id="1f535-121">出现错误时, 将引发异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-121">When an error occurs, an exception is thrown.</span></span> <span data-ttu-id="1f535-122">异常是指应用程序遇到的任何错误、条件或意外行为。</span><span class="sxs-lookup"><span data-stu-id="1f535-122">An exception is any error, condition, or unexpected behavior that an application encounters.</span></span>

<span data-ttu-id="1f535-123">在 .NET Framework 中，异常是从 `System.Exception` 类继承的对象。</span><span class="sxs-lookup"><span data-stu-id="1f535-123">In the .NET Framework, an exception is an object that inherits from the `System.Exception` class.</span></span> <span data-ttu-id="1f535-124">异常引发自发生问题的代码区域。</span><span class="sxs-lookup"><span data-stu-id="1f535-124">An exception is thrown from an area of code where a problem has occurred.</span></span> <span data-ttu-id="1f535-125">异常将在调用堆栈中向上传递到一个位置, 应用程序提供代码来处理异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-125">The exception is passed up the call stack to a place where the application provides code to handle the exception.</span></span> <span data-ttu-id="1f535-126">如果应用程序不处理此异常, 则会强制浏览器显示错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-126">If the application does not handle the exception, the browser is forced to display the error details.</span></span>

<span data-ttu-id="1f535-127">最佳做法是, 在代码中`Try`的`Finally`块内的代码级别/ `Catch` /处理错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-127">As a best practice, handle errors in at the code level in `Try`/`Catch`/`Finally` blocks within your code.</span></span> <span data-ttu-id="1f535-128">尝试放置这些块, 以使用户能够在发生错误的上下文中更正问题。</span><span class="sxs-lookup"><span data-stu-id="1f535-128">Try to place these blocks so that the user can correct problems in the context in which they occur.</span></span> <span data-ttu-id="1f535-129">如果错误处理块离错误发生的时间太远, 则为用户提供解决问题所需的信息变得更加困难。</span><span class="sxs-lookup"><span data-stu-id="1f535-129">If the error handling blocks are too far away from where the error occurred, it becomes more difficult to provide users with the information they need to fix the problem.</span></span>

### <a name="exception-class"></a><span data-ttu-id="1f535-130">Exception 类</span><span class="sxs-lookup"><span data-stu-id="1f535-130">Exception Class</span></span>

<span data-ttu-id="1f535-131">Exception 类是异常从中继承的基类。</span><span class="sxs-lookup"><span data-stu-id="1f535-131">The Exception class is the base class from which exceptions inherit.</span></span> <span data-ttu-id="1f535-132">大多数异常对象是异常类的某个派生类的实例, 例如`SystemException`类`IndexOutOfRangeException` 、类或`ArgumentNullException`类。</span><span class="sxs-lookup"><span data-stu-id="1f535-132">Most exception objects are instances of some derived class of the Exception class, such as the `SystemException` class, the `IndexOutOfRangeException` class, or the `ArgumentNullException` class.</span></span> <span data-ttu-id="1f535-133">Exception 类具有属性, 如`StackTrace`属性`InnerException` 、属性和`Message`属性, 这些属性提供有关已发生的错误的特定信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-133">The Exception class has properties, such as the `StackTrace` property, the `InnerException` property, and the `Message` property, that provide specific information about the error that has occurred.</span></span>

### <a name="exception-inheritance-hierarchy"></a><span data-ttu-id="1f535-134">异常继承层次结构</span><span class="sxs-lookup"><span data-stu-id="1f535-134">Exception Inheritance Hierarchy</span></span>

<span data-ttu-id="1f535-135">运行时有一组从`SystemException`类派生的基本异常, 运行时在遇到异常时引发。</span><span class="sxs-lookup"><span data-stu-id="1f535-135">The runtime has a base set of exceptions deriving from the `SystemException` class that the runtime throws when an exception is encountered.</span></span> <span data-ttu-id="1f535-136">大多数继承自异常类的类 (如`IndexOutOfRangeException`类`ArgumentNullException`和类) 不实现其他成员。</span><span class="sxs-lookup"><span data-stu-id="1f535-136">Most of the classes that inherit from the Exception class, such as the `IndexOutOfRangeException` class and the `ArgumentNullException` class, do not implement additional members.</span></span> <span data-ttu-id="1f535-137">因此, 可在异常层次结构、异常名称和异常中包含的信息中找到异常的最重要信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-137">Therefore, the most important information for an exception can be found in the hierarchy of exceptions, the exception name, and the information contained in the exception.</span></span>

### <a name="exception-handling-hierarchy"></a><span data-ttu-id="1f535-138">异常处理层次结构</span><span class="sxs-lookup"><span data-stu-id="1f535-138">Exception Handling Hierarchy</span></span>

<span data-ttu-id="1f535-139">在 ASP.NET Web 窗体应用程序中, 可以根据特定的处理层次结构来处理异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-139">In an ASP.NET Web Forms application, exceptions can be handled based on a specific handling hierarchy.</span></span> <span data-ttu-id="1f535-140">可以在以下级别处理异常:</span><span class="sxs-lookup"><span data-stu-id="1f535-140">An exception can be handled at the following levels:</span></span>

- <span data-ttu-id="1f535-141">应用程序级别</span><span class="sxs-lookup"><span data-stu-id="1f535-141">Application level</span></span>
- <span data-ttu-id="1f535-142">页面级别</span><span class="sxs-lookup"><span data-stu-id="1f535-142">Page level</span></span>
- <span data-ttu-id="1f535-143">代码级别</span><span class="sxs-lookup"><span data-stu-id="1f535-143">Code level</span></span>

<span data-ttu-id="1f535-144">当应用程序处理异常时, 通常可以检索有关继承自异常类的异常的其他信息, 并向用户显示这些信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-144">When an application handles exceptions, additional information about the exception that is inherited from the Exception class can often be retrieved and displayed to the user.</span></span> <span data-ttu-id="1f535-145">除应用程序、页和代码级别外, 还可以使用 IIS 自定义处理程序来处理 HTTP 模块级别的异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-145">In addition to application, page, and code level, you can also handle exceptions at the HTTP module level and by using an IIS custom handler.</span></span>

### <a name="application-level-error-handling"></a><span data-ttu-id="1f535-146">应用程序级别的错误处理</span><span class="sxs-lookup"><span data-stu-id="1f535-146">Application Level Error Handling</span></span>

<span data-ttu-id="1f535-147">可以通过修改应用程序的配置或在应用程序的`Application_Error` *global.asax*文件中添加处理程序来处理应用程序级别的默认错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-147">You can handle default errors at the application level either by modifying your application's configuration or by adding an `Application_Error` handler in the *Global.asax* file of your application.</span></span>

<span data-ttu-id="1f535-148">您可以通过向`customErrors` *web.config*文件添加节来处理默认错误和 HTTP 错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-148">You can handle default errors and HTTP errors by adding a `customErrors` section to the *Web.config* file.</span></span> <span data-ttu-id="1f535-149">使用`customErrors`节, 您可以指定在发生错误时用户将重定向到的默认页面。</span><span class="sxs-lookup"><span data-stu-id="1f535-149">The `customErrors` section allows you to specify a default page that users will be redirected to when an error occurs.</span></span> <span data-ttu-id="1f535-150">它还允许您为特定状态代码错误指定单独的页面。</span><span class="sxs-lookup"><span data-stu-id="1f535-150">It also allows you to specify individual pages for specific status code errors.</span></span>

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

<span data-ttu-id="1f535-151">遗憾的是, 当你使用配置将用户重定向到其他页面时, 你没有发生的错误的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-151">Unfortunately, when you use the configuration to redirect the user to a different page, you do not have the details of the error that occurred.</span></span>

<span data-ttu-id="1f535-152">但是, 你可以通过将代码添加到`Application_Error` *global.asax*文件中的处理程序来捕获应用程序中任何位置发生的错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-152">However, you can trap errors that occur anywhere in your application by adding code to the `Application_Error` handler in the *Global.asax* file.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a><span data-ttu-id="1f535-153">页级别错误事件处理</span><span class="sxs-lookup"><span data-stu-id="1f535-153">Page Level Error Event Handling</span></span>

<span data-ttu-id="1f535-154">页面级处理程序将用户返回到发生错误的页面, 但由于不保留控件的实例, 因此页面上将不再有任何内容。</span><span class="sxs-lookup"><span data-stu-id="1f535-154">A page-level handler returns the user to the page where the error occurred, but because instances of controls are not maintained, there will no longer be anything on the page.</span></span> <span data-ttu-id="1f535-155">若要向应用程序的用户提供错误详细信息, 必须专门将错误详细信息写入页面。</span><span class="sxs-lookup"><span data-stu-id="1f535-155">To provide the error details to the user of the application, you must specifically write the error details to the page.</span></span>

<span data-ttu-id="1f535-156">通常使用页面级错误处理程序来记录未处理的错误, 或使用户进入可显示有用信息的页面。</span><span class="sxs-lookup"><span data-stu-id="1f535-156">You would typically use a page-level error handler to log unhandled errors or to take the user to a page that can display helpful information.</span></span>

<span data-ttu-id="1f535-157">此代码示例演示了 ASP.NET 网页中错误事件的处理程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-157">This code example shows a handler for the Error event in an ASP.NET Web page.</span></span> <span data-ttu-id="1f535-158">此处理程序捕获页中的块内`try` / `catch`尚未处理的所有异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-158">This handler catches all exceptions that are not already handled within `try`/`catch` blocks in the page.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

<span data-ttu-id="1f535-159">处理错误后, 必须通过调用`ClearError`服务器对象 (`HttpServerUtility`类) 的方法来清除该错误, 否则将看到之前发生的错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-159">After you handle an error, you must clear it by calling the `ClearError` method of the Server object (`HttpServerUtility` class), otherwise you will see an error that has previously occurred.</span></span>

### <a name="code-level-error-handling"></a><span data-ttu-id="1f535-160">代码级别错误处理</span><span class="sxs-lookup"><span data-stu-id="1f535-160">Code Level Error Handling</span></span>

<span data-ttu-id="1f535-161">Try-catch 语句包含一个 try 块, 后跟一个或多个 catch 子句, 这些子句指定不同异常的处理程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-161">The try-catch statement consists of a try block followed by one or more catch clauses, which specify handlers for different exceptions.</span></span> <span data-ttu-id="1f535-162">当引发异常时, 公共语言运行时 (CLR) 将查找处理此异常的 catch 语句。</span><span class="sxs-lookup"><span data-stu-id="1f535-162">When an exception is thrown, the common language runtime (CLR) looks for the catch statement that handles this exception.</span></span> <span data-ttu-id="1f535-163">如果当前正在执行的方法不包含 catch 块, 则 CLR 将查看调用当前方法的方法, 依此类推, 直到调用堆栈。</span><span class="sxs-lookup"><span data-stu-id="1f535-163">If the currently executing method does not contain a catch block, the CLR looks at the method that called the current method, and so on, up the call stack.</span></span> <span data-ttu-id="1f535-164">如果未找到 catch 块, 则 CLR 向用户显示一条未处理的异常消息, 并停止执行程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-164">If no catch block is found, then the CLR displays an unhandled exception message to the user and stops execution of the program.</span></span>

<span data-ttu-id="1f535-165">下面的代码示例演示了`try`如何使用/ `catch` / `finally`来处理错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-165">The following code example shows a common way of using `try`/`catch`/`finally` to handle errors.</span></span>

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

<span data-ttu-id="1f535-166">在上面的代码中, try 块包含需要针对可能的异常进行保护的代码。</span><span class="sxs-lookup"><span data-stu-id="1f535-166">In the above code, the try block contains the code that needs to be guarded against a possible exception.</span></span> <span data-ttu-id="1f535-167">在引发异常或成功完成块之前, 将执行块。</span><span class="sxs-lookup"><span data-stu-id="1f535-167">The block is executed until either an exception is thrown or the block is completed successfully.</span></span> <span data-ttu-id="1f535-168">如果发生`IOException`异常或异常, 则会将执行转移到其他页。 `FileNotFoundException`</span><span class="sxs-lookup"><span data-stu-id="1f535-168">If either a `FileNotFoundException` exception or an `IOException` exception occurs, the execution is transferred to a different page.</span></span> <span data-ttu-id="1f535-169">然后, 将执行 finally 块中包含的代码, 无论是否发生了错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-169">Then, the code contained in the finally block is executed, whether an error occurred or not.</span></span>

## <a name="adding-error-logging-support"></a><span data-ttu-id="1f535-170">添加错误日志记录支持</span><span class="sxs-lookup"><span data-stu-id="1f535-170">Adding Error Logging Support</span></span>

<span data-ttu-id="1f535-171">在将错误处理添加到 Wingtip 玩具示例应用程序之前, 你将通过`ExceptionUtility`向*逻辑*文件夹添加类来添加错误日志记录支持。</span><span class="sxs-lookup"><span data-stu-id="1f535-171">Before adding error handling to the Wingtip Toys sample application, you will add error logging support by adding an `ExceptionUtility` class to the *Logic* folder.</span></span> <span data-ttu-id="1f535-172">这样一来, 每次应用程序处理错误时, 错误详细信息都将添加到错误日志文件中。</span><span class="sxs-lookup"><span data-stu-id="1f535-172">By doing this, each time the application handles an error, the error details will be added to the error log file.</span></span>

1. <span data-ttu-id="1f535-173">右键单击*逻辑*文件夹, 然后选择 "**添加** - &gt; **新项**"。</span><span class="sxs-lookup"><span data-stu-id="1f535-173">Right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="1f535-174">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="1f535-174">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="1f535-175">选择左侧的 "  - **视觉对象C#**  &gt; **代码**模板" 组。</span><span class="sxs-lookup"><span data-stu-id="1f535-175">Select the **Visual C#** -&gt; **Code** templates group on the left.</span></span> <span data-ttu-id="1f535-176">然后, 从中间列表中选择 "**类**", 并将其命名为**ExceptionUtility.cs**。</span><span class="sxs-lookup"><span data-stu-id="1f535-176">Then, select **Class**from the middle list and name it **ExceptionUtility.cs**.</span></span>
3. <span data-ttu-id="1f535-177">选择“添加”。</span><span class="sxs-lookup"><span data-stu-id="1f535-177">Choose **Add**.</span></span> <span data-ttu-id="1f535-178">将显示新的类文件。</span><span class="sxs-lookup"><span data-stu-id="1f535-178">The new class file is displayed.</span></span>
4. <span data-ttu-id="1f535-179">将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="1f535-179">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

<span data-ttu-id="1f535-180">发生异常时, 可以通过调用`LogException`方法将异常写入异常日志文件。</span><span class="sxs-lookup"><span data-stu-id="1f535-180">When an exception occurs, the exception can be written to an exception log file by calling the `LogException` method.</span></span> <span data-ttu-id="1f535-181">此方法采用两个参数, 即 exception 对象和包含有关异常源的详细信息的字符串。</span><span class="sxs-lookup"><span data-stu-id="1f535-181">This method takes two parameters, the exception object and a string containing details about the source of the exception.</span></span> <span data-ttu-id="1f535-182">异常日志将写入到*应用程序\_数据*文件夹中的错误日志文件 *。*</span><span class="sxs-lookup"><span data-stu-id="1f535-182">The exception log is written to the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>

### <a name="adding-an-error-page"></a><span data-ttu-id="1f535-183">添加错误页</span><span class="sxs-lookup"><span data-stu-id="1f535-183">Adding an Error Page</span></span>

<span data-ttu-id="1f535-184">在 Wingtip 玩具示例应用程序中, 将使用一个页面来显示错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-184">In the Wingtip Toys sample application, one page will be used to display errors.</span></span> <span data-ttu-id="1f535-185">错误页旨在向网站用户显示一条安全的错误消息。</span><span class="sxs-lookup"><span data-stu-id="1f535-185">The error page is designed to show a secure error message to users of the site.</span></span> <span data-ttu-id="1f535-186">但是, 如果用户是发出 HTTP 请求的开发人员, 而该请求正在本地提供, 则错误页面上将显示其他错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-186">However, if the user is a developer making an HTTP request that is being served locally on the machine where the code lives, additional error details will be displayed on the error page.</span></span>

1. <span data-ttu-id="1f535-187">在**解决方案资源管理器**中右键单击项目名称 **(Wingtip 玩具**), 然后选择 **"添加** -&gt;新项"。</span><span class="sxs-lookup"><span data-stu-id="1f535-187">Right-click the project name (**Wingtip Toys**) in **Solution Explorer** and select **Add** -&gt; **New Item**.</span></span>   
   <span data-ttu-id="1f535-188">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="1f535-188">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="1f535-189">选择左侧的 "  - **可视C#**  &gt; **Web**模板" 组。</span><span class="sxs-lookup"><span data-stu-id="1f535-189">Select the **Visual C#** -&gt; **Web** templates group on the left.</span></span> <span data-ttu-id="1f535-190">从中间列表中, 选择 "**带有母版页的 Web 窗体**", 并将其命名为**ErrorPage**。</span><span class="sxs-lookup"><span data-stu-id="1f535-190">From the middle list, select **Web Form with Master Page**,and name it **ErrorPage.aspx**.</span></span>
3. <span data-ttu-id="1f535-191">单击 **添加**。</span><span class="sxs-lookup"><span data-stu-id="1f535-191">Click **Add**.</span></span>
4. <span data-ttu-id="1f535-192">选择 "*网站*" 作为母版页的主文件, 然后选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="1f535-192">Select the *Site.Master* file as the master page, and then choose **OK**.</span></span>
5. <span data-ttu-id="1f535-193">将现有标记替换为以下内容:</span><span class="sxs-lookup"><span data-stu-id="1f535-193">Replace the existing markup with the following:</span></span>   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. <span data-ttu-id="1f535-194">替换代码隐藏 (*ErrorPage.aspx.cs*) 的现有代码, 使其显示如下:</span><span class="sxs-lookup"><span data-stu-id="1f535-194">Replace the existing code of the code-behind (*ErrorPage.aspx.cs*) so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

<span data-ttu-id="1f535-195">显示错误页面后, `Page_Load`将执行事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-195">When the error page is displayed, the `Page_Load` event handler is executed.</span></span> <span data-ttu-id="1f535-196">`Page_Load`在处理程序中, 确定第一次处理错误的位置。</span><span class="sxs-lookup"><span data-stu-id="1f535-196">In the `Page_Load` handler, the location of where the error was first handled is determined.</span></span> <span data-ttu-id="1f535-197">然后, 通过调用`GetLastError` Server 对象的方法来确定发生的最后一个错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-197">Then, the last error that occurred is determined by call the `GetLastError` method of the Server object.</span></span> <span data-ttu-id="1f535-198">如果异常不再存在, 则将创建一般异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-198">If the exception no longer exists, a generic exception is created.</span></span> <span data-ttu-id="1f535-199">然后, 如果在本地发出 HTTP 请求, 则显示所有错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-199">Then, if the HTTP request was made locally, all error details are shown.</span></span> <span data-ttu-id="1f535-200">在这种情况下, 只有运行 web 应用程序的本地计算机才能看到这些错误的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-200">In this case, only the local machine running the web application will see these error details.</span></span> <span data-ttu-id="1f535-201">显示错误信息后, 会将错误添加到日志文件中, 并从服务器中清除错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-201">After the error information has been displayed, the error is added to the log file and the error is cleared from the server.</span></span>

### <a name="displaying-unhandled-error-messages-for-the-application"></a><span data-ttu-id="1f535-202">显示应用程序的未处理错误消息</span><span class="sxs-lookup"><span data-stu-id="1f535-202">Displaying Unhandled Error Messages for the Application</span></span>

<span data-ttu-id="1f535-203">通过将`customErrors`节添加到 web.config文件, 可以快速处理整个应用程序中发生的简单错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-203">By adding a `customErrors` section to the *Web.config* file, you can quickly handle simple errors that occur throughout the application.</span></span> <span data-ttu-id="1f535-204">你还可以根据错误的状态代码值指定如何处理错误, 如 "404-找不到文件"。</span><span class="sxs-lookup"><span data-stu-id="1f535-204">You can also specify how to handle errors based on their status code value, such as 404 - File not found.</span></span>

#### <a name="update-the-configuration"></a><span data-ttu-id="1f535-205">更新配置</span><span class="sxs-lookup"><span data-stu-id="1f535-205">Update the Configuration</span></span>

<span data-ttu-id="1f535-206">通过向`customErrors` *web.config*文件添加节来更新配置。</span><span class="sxs-lookup"><span data-stu-id="1f535-206">Update the configuration by adding a `customErrors` section to the *Web.config* file.</span></span>

1. <span data-ttu-id="1f535-207">在**解决方案资源管理器**中, 找到并打开 Wingtip 玩具示例应用程序根目录处的 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="1f535-207">In **Solution Explorer**, find and open the *Web.config* file at the root of the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="1f535-208">将节添加到`<system.web>`节点内的 web.config 文件中, 如下所示: `customErrors`</span><span class="sxs-lookup"><span data-stu-id="1f535-208">Add the `customErrors` section to the *Web.config* file within the `<system.web>` node as follows:</span></span>   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. <span data-ttu-id="1f535-209">保存 web.config文件。</span><span class="sxs-lookup"><span data-stu-id="1f535-209">Save the *Web.config* file.</span></span>

<span data-ttu-id="1f535-210">`customErrors`部分指定模式, 该模式设置为 "打开"。</span><span class="sxs-lookup"><span data-stu-id="1f535-210">The `customErrors` section specifies the mode, which is set to "On".</span></span> <span data-ttu-id="1f535-211">它还指定`defaultRedirect`, 它会告知应用程序在发生错误时要导航到的页面。</span><span class="sxs-lookup"><span data-stu-id="1f535-211">It also specifies the `defaultRedirect`, which tells the application which page to navigate to when an error occurs.</span></span> <span data-ttu-id="1f535-212">此外, 还添加了特定的 error 元素, 该元素指定在找不到页面时如何处理404错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-212">In addition, you have added a specific error element that specifies how to handle a 404 error when a page is not found.</span></span> <span data-ttu-id="1f535-213">稍后在本教程中, 你将添加其他错误处理, 以在应用程序级别捕获错误的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-213">Later in this tutorial, you will add additional error handling that will capture the details of an error at the application level.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="1f535-214">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="1f535-214">Running the Application</span></span>

<span data-ttu-id="1f535-215">现在可以运行应用程序来查看更新的路由。</span><span class="sxs-lookup"><span data-stu-id="1f535-215">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="1f535-216">按**F5**运行 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-216">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="1f535-217">浏览器将打开并显示*default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="1f535-217">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="1f535-218">在浏览器中输入以下 URL (请务必使用端口号):</span><span class="sxs-lookup"><span data-stu-id="1f535-218">Enter the following URL into the browser (be sure to use **your** port number):</span></span>  
    `https://localhost:44300/NoPage.aspx`
3. <span data-ttu-id="1f535-219">查看浏览器中显示的*ErrorPage* 。</span><span class="sxs-lookup"><span data-stu-id="1f535-219">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 错误处理-找不到页面错误](aspnet-error-handling/_static/image1.png)

<span data-ttu-id="1f535-221">当你请求不存在的*NoPage*页时, 如果有更多详细信息, "错误" 页将显示简单错误消息和详细的错误信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-221">When you request the *NoPage.aspx* page, which does not exist, the error page will show the simple error message and the detailed error information if additional details are available.</span></span> <span data-ttu-id="1f535-222">但是, 如果用户从远程位置请求了不存在的页, 则 "错误" 页将只以红色显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="1f535-222">However, if the user requested a non-existent page from a remote location, the error page would only show the error message in red.</span></span>

### <a name="including-an-exception-for-testing-purposes"></a><span data-ttu-id="1f535-223">包括用于测试目的的异常</span><span class="sxs-lookup"><span data-stu-id="1f535-223">Including an Exception for Testing Purposes</span></span>

<span data-ttu-id="1f535-224">若要在发生错误时验证应用程序的工作方式, 可以在 ASP.NET 中特意创建错误条件。</span><span class="sxs-lookup"><span data-stu-id="1f535-224">To verify how your application will function when an error occurs, you can deliberately create error conditions in ASP.NET.</span></span> <span data-ttu-id="1f535-225">在 Wingtip 玩具示例应用程序中, 当加载默认页面时, 将引发测试异常以查看发生的情况。</span><span class="sxs-lookup"><span data-stu-id="1f535-225">In the Wingtip Toys sample application, you will throw a test exception when the default page loads to see what happens.</span></span>

1. <span data-ttu-id="1f535-226">在 Visual Studio 中打开*default.aspx*页的代码隐藏。</span><span class="sxs-lookup"><span data-stu-id="1f535-226">Open the code-behind of the *Default.aspx* page in Visual Studio.</span></span>   
   <span data-ttu-id="1f535-227">将显示*Default.aspx.cs*代码隐藏页面。</span><span class="sxs-lookup"><span data-stu-id="1f535-227">The *Default.aspx.cs* code-behind page will be displayed.</span></span>
2. <span data-ttu-id="1f535-228">`Page_Load`在处理程序中, 添加代码, 使处理程序如下所示:</span><span class="sxs-lookup"><span data-stu-id="1f535-228">In the `Page_Load` handler, add code so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

<span data-ttu-id="1f535-229">可以创建各种不同类型的异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-229">It is possible to create various different types of exceptions.</span></span> <span data-ttu-id="1f535-230">在上面的代码中, 将在加载`InvalidOperationException` *default.aspx*页面时创建。</span><span class="sxs-lookup"><span data-stu-id="1f535-230">In the above code, you are creating an `InvalidOperationException` when the *Default.aspx* page is loaded.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="1f535-231">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="1f535-231">Running the Application</span></span>

<span data-ttu-id="1f535-232">您可以运行应用程序, 以了解应用程序如何处理异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-232">You can run the application to see how the application handles the exception.</span></span>

1. <span data-ttu-id="1f535-233">按**CTRL + F5**运行 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-233">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="1f535-234">应用程序会引发 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="1f535-234">The application throws the InvalidOperationException.</span></span> 

    > [!NOTE] 
    > 
    > <span data-ttu-id="1f535-235">您必须按**CTRL + F5**来显示页面, 而不会中断代码以查看 Visual Studio 中的错误来源。</span><span class="sxs-lookup"><span data-stu-id="1f535-235">You must press **CTRL+F5** to display the page without breaking into the code to view the source of the error in Visual Studio.</span></span>
2. <span data-ttu-id="1f535-236">查看浏览器中显示的*ErrorPage* 。</span><span class="sxs-lookup"><span data-stu-id="1f535-236">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 错误处理-错误页](aspnet-error-handling/_static/image2.png)

<span data-ttu-id="1f535-238">如错误详细信息中所示, 在 web.config 文件中的`customError`节捕获了异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-238">As you can see in the error details, the exception was trapped by the `customError` section in the *Web.config* file.</span></span>

### <a name="adding-application-level-error-handling"></a><span data-ttu-id="1f535-239">添加应用程序级别的错误处理</span><span class="sxs-lookup"><span data-stu-id="1f535-239">Adding Application-Level Error Handling</span></span>

<span data-ttu-id="1f535-240">不要使用`customErrors` *web.config*文件中的节来捕获异常, 其中您几乎不会获得有关异常的信息, 您可以在应用程序级别捕获错误并检索错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-240">Rather than trap the exception using the `customErrors` section in the *Web.config* file, where you gain little information about the exception, you can trap the error at the application level and retrieve error details.</span></span>

1. <span data-ttu-id="1f535-241">在**解决方案资源管理器**中, 找到并打开*Global.asax.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="1f535-241">In **Solution Explorer**, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="1f535-242">添加**应用程序\_错误**处理程序, 使其显示如下:</span><span class="sxs-lookup"><span data-stu-id="1f535-242">Add an **Application\_Error** handler so that it appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

<span data-ttu-id="1f535-243">当应用程序中出现错误时, 将`Application_Error`调用处理程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-243">When an error occurs in the application, the `Application_Error` handler is called.</span></span> <span data-ttu-id="1f535-244">在此处理程序中, 将检索并查看最后一个异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-244">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="1f535-245">如果异常未得到处理, 并且异常包含内部异常详细信息 (即, `InnerException`不为 null), 则应用程序会将执行转移到显示异常详细信息的错误页。</span><span class="sxs-lookup"><span data-stu-id="1f535-245">If the exception was unhandled and the exception contains inner-exception details (that is, `InnerException` is not null), the application transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="1f535-246">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="1f535-246">Running the Application</span></span>

<span data-ttu-id="1f535-247">可以通过在应用程序级别处理异常来运行应用程序, 以查看其他错误详细信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-247">You can run the application to see the additional error details provided by handling the exception at the application level.</span></span>

1. <span data-ttu-id="1f535-248">按**CTRL + F5**运行 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-248">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="1f535-249">应用程序引发`InvalidOperationException` 。</span><span class="sxs-lookup"><span data-stu-id="1f535-249">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="1f535-250">查看浏览器中显示的*ErrorPage* 。</span><span class="sxs-lookup"><span data-stu-id="1f535-250">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 错误处理-应用程序级别错误](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a><span data-ttu-id="1f535-252">添加页面级错误处理</span><span class="sxs-lookup"><span data-stu-id="1f535-252">Adding Page-Level Error Handling</span></span>

<span data-ttu-id="1f535-253">可以通过`ErrorPage`将属性添加`@Page`到页面的指令`Page_Error`中, 或通过将事件处理程序添加到页面的代码隐藏来向页面添加页面级错误处理。</span><span class="sxs-lookup"><span data-stu-id="1f535-253">You can add page-level error handling to a page either by using adding an `ErrorPage` attribute to the `@Page` directive of the page, or by adding a `Page_Error` event handler to the code-behind of a page.</span></span> <span data-ttu-id="1f535-254">在本部分中, 将添加一个`Page_Error`事件处理程序, 用于将执行传输到*ErrorPage*页。</span><span class="sxs-lookup"><span data-stu-id="1f535-254">In this section, you will add a `Page_Error` event handler that will transfer execution to the *ErrorPage.aspx* page.</span></span>

1. <span data-ttu-id="1f535-255">在**解决方案资源管理器**中, 找到并打开*Default.aspx.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="1f535-255">In **Solution Explorer**, find and open the *Default.aspx.cs* file.</span></span>
2. <span data-ttu-id="1f535-256">添加一个`Page_Error`处理程序, 使代码隐藏如下所示:</span><span class="sxs-lookup"><span data-stu-id="1f535-256">Add a `Page_Error` handler so that the code-behind appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

<span data-ttu-id="1f535-257">当页面上发生错误时, `Page_Error`将调用事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-257">When an error occurs on the page, the `Page_Error` event handler is called.</span></span> <span data-ttu-id="1f535-258">在此处理程序中, 将检索并查看最后一个异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-258">In this handler, the last exception is retrieved and reviewed.</span></span> <span data-ttu-id="1f535-259">如果发生这种情况`Page_Error` , 事件处理程序会将执行转移到错误页, 其中显示异常详细信息。 `InvalidOperationException`</span><span class="sxs-lookup"><span data-stu-id="1f535-259">If an `InvalidOperationException` occurs, the `Page_Error` event handler transfers execution to the error page where the exception details are displayed.</span></span>

#### <a name="running-the-application"></a><span data-ttu-id="1f535-260">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="1f535-260">Running the Application</span></span>

<span data-ttu-id="1f535-261">现在可以运行应用程序来查看更新的路由。</span><span class="sxs-lookup"><span data-stu-id="1f535-261">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="1f535-262">按**CTRL + F5**运行 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-262">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="1f535-263">应用程序引发`InvalidOperationException` 。</span><span class="sxs-lookup"><span data-stu-id="1f535-263">The application throws the `InvalidOperationException` .</span></span>
2. <span data-ttu-id="1f535-264">查看浏览器中显示的*ErrorPage* 。</span><span class="sxs-lookup"><span data-stu-id="1f535-264">Review the *ErrorPage.aspx* displayed in the browser.</span></span> 

    ![ASP.NET 错误处理-页面级别错误](aspnet-error-handling/_static/image4.png)
3. <span data-ttu-id="1f535-266">关闭浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="1f535-266">Close your browser window.</span></span>

### <a name="removing-the-exception-used-for-testing"></a><span data-ttu-id="1f535-267">删除用于测试的异常</span><span class="sxs-lookup"><span data-stu-id="1f535-267">Removing the Exception Used for Testing</span></span>

<span data-ttu-id="1f535-268">若要允许 Wingtip 玩具示例应用程序正常运行而不引发您在本教程前面部分添加的异常, 请删除该异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-268">To allow the Wingtip Toys sample application to function without throwing the exception you added earlier in this tutorial, remove the exception.</span></span>

1. <span data-ttu-id="1f535-269">打开*default.aspx*页的代码隐藏。</span><span class="sxs-lookup"><span data-stu-id="1f535-269">Open the code-behind of the *Default.aspx* page.</span></span>
2. <span data-ttu-id="1f535-270">`Page_Load`在处理程序中, 删除引发异常的代码, 使处理程序如下所示:</span><span class="sxs-lookup"><span data-stu-id="1f535-270">In the `Page_Load` handler, remove the code that throws the exception so that the handler appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a><span data-ttu-id="1f535-271">添加代码级别错误日志记录</span><span class="sxs-lookup"><span data-stu-id="1f535-271">Adding Code-Level Error Logging</span></span>

<span data-ttu-id="1f535-272">如本教程前面所述, 你可以添加 try/catch 语句来尝试运行部分代码, 并处理发生的第一个错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-272">As mentioned earlier in this tutorial, you can add try/catch statements to attempt to run a section of code and handle the first error that occurs.</span></span> <span data-ttu-id="1f535-273">在此示例中, 只会将错误详细信息写入错误日志文件, 以便以后可以查看该错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-273">In this example, you will only write the error details to the error log file so that the error can be reviewed later.</span></span>

1. <span data-ttu-id="1f535-274">在**解决方案资源管理器**的*逻辑*文件夹中, 找到并打开*PayPalFunctions.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="1f535-274">In **Solution Explorer**, in the *Logic* folder, find and open the *PayPalFunctions.cs* file.</span></span>
2. <span data-ttu-id="1f535-275">`HttpCall`更新方法, 使代码如下所示:</span><span class="sxs-lookup"><span data-stu-id="1f535-275">Update the `HttpCall` method so that the code appears as follows:</span></span>   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

<span data-ttu-id="1f535-276">上面的代码调用`LogException` `ExceptionUtility`类中包含的方法。</span><span class="sxs-lookup"><span data-stu-id="1f535-276">The above code calls the `LogException` method that is contained in the `ExceptionUtility` class.</span></span> <span data-ttu-id="1f535-277">在本教程的前面部分中, 已将*ExceptionUtility.cs*类文件添加到*逻辑*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="1f535-277">You added the *ExceptionUtility.cs* class file to the *Logic* folder earlier in this tutorial.</span></span> <span data-ttu-id="1f535-278">`LogException` 方法采用两个参数。</span><span class="sxs-lookup"><span data-stu-id="1f535-278">The `LogException` method takes two parameters.</span></span> <span data-ttu-id="1f535-279">第一个参数是 exception 对象。</span><span class="sxs-lookup"><span data-stu-id="1f535-279">The first parameter is the exception object.</span></span> <span data-ttu-id="1f535-280">第二个参数是用于识别错误源的字符串。</span><span class="sxs-lookup"><span data-stu-id="1f535-280">The second parameter is a string used to recognize the source of the error.</span></span>

### <a name="inspecting-the-error-logging-information"></a><span data-ttu-id="1f535-281">检查错误日志记录信息</span><span class="sxs-lookup"><span data-stu-id="1f535-281">Inspecting the Error Logging Information</span></span>

<span data-ttu-id="1f535-282">如前文所述, 你可以使用错误日志来确定应用程序中应该首先修复哪些错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-282">As mentioned previously, you can use the error log to determine which errors in your application should be fixed first.</span></span> <span data-ttu-id="1f535-283">当然, 只会记录已捕获并写入错误日志的错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-283">Of course, only errors that have been trapped and written to the error log will be recorded.</span></span>

1. <span data-ttu-id="1f535-284">在**解决方案资源管理器**中, 查找并打开 "*应用程序\_数据*" 文件夹中的*错误日志文件。*</span><span class="sxs-lookup"><span data-stu-id="1f535-284">In **Solution Explorer**, find and open the *ErrorLog.txt* file in the *App\_Data* folder.</span></span>   
 <span data-ttu-id="1f535-285">可能需要选择 "**显示所有文件**" 选项, 或从**解决方案资源管理器**顶部选择 "**刷新**" 选项以查看*错误日志*文件。</span><span class="sxs-lookup"><span data-stu-id="1f535-285">You may need to select the "**Show All Files**" option or the "**Refresh**" option from the top of **Solution Explorer** to see the *ErrorLog.txt* file.</span></span>
2. <span data-ttu-id="1f535-286">查看在 Visual Studio 中显示的错误日志:</span><span class="sxs-lookup"><span data-stu-id="1f535-286">Review the error log displayed in Visual Studio:</span></span> 

    ![ASP.NET 错误处理-错误日志](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a><span data-ttu-id="1f535-288">安全错误消息</span><span class="sxs-lookup"><span data-stu-id="1f535-288">Safe Error Messages</span></span>

<span data-ttu-id="1f535-289">**请务必注意**, 当应用程序显示错误消息时, 它不应提供恶意用户在攻击应用程序时可能会有帮助的信息。</span><span class="sxs-lookup"><span data-stu-id="1f535-289">It is **important to note** that when your application displays error messages, it should not give away information that a malicious user might find helpful in attacking your application.</span></span> <span data-ttu-id="1f535-290">例如, 如果应用程序尝试将写入数据库失败, 则不会显示一条错误消息, 其中包含该数据库所使用的用户名。</span><span class="sxs-lookup"><span data-stu-id="1f535-290">For example, if your application unsuccessfully tries to write in to a database, it should not display an error message that includes the user name it is using.</span></span> <span data-ttu-id="1f535-291">出于此原因, 将向用户显示红色的一般错误消息。</span><span class="sxs-lookup"><span data-stu-id="1f535-291">For this reason, a generic error message in red is displayed to the user.</span></span> <span data-ttu-id="1f535-292">所有其他错误详细信息仅向开发人员显示在本地计算机上。</span><span class="sxs-lookup"><span data-stu-id="1f535-292">All additional error details are only displayed to the developer on the local machine.</span></span>

## <a name="using-elmah"></a><span data-ttu-id="1f535-293">使用 ELMAH</span><span class="sxs-lookup"><span data-stu-id="1f535-293">Using ELMAH</span></span>

<span data-ttu-id="1f535-294">ELMAH (错误日志记录模块和处理程序) 是一个错误日志记录工具, 它将你作为 NuGet 包插入 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-294">ELMAH (Error Logging Modules and Handlers) is an error logging facility that you plug into your ASP.NET application as a NuGet package.</span></span> <span data-ttu-id="1f535-295">ELMAH 提供以下功能:</span><span class="sxs-lookup"><span data-stu-id="1f535-295">ELMAH provides the following capabilities:</span></span>

- <span data-ttu-id="1f535-296">未处理的异常的日志记录。</span><span class="sxs-lookup"><span data-stu-id="1f535-296">Logging of unhandled exceptions.</span></span>
- <span data-ttu-id="1f535-297">用于查看重新编码未经处理的异常的整个日志的网页。</span><span class="sxs-lookup"><span data-stu-id="1f535-297">A web page to view the entire log of recoded unhandled exceptions.</span></span>
- <span data-ttu-id="1f535-298">用于查看每个记录的异常的完整详细信息的网页。</span><span class="sxs-lookup"><span data-stu-id="1f535-298">A web page to view the full details of each logged exception.</span></span>
- <span data-ttu-id="1f535-299">发生时每个错误的电子邮件通知。</span><span class="sxs-lookup"><span data-stu-id="1f535-299">An email notification of each error at the time it occurs.</span></span>
- <span data-ttu-id="1f535-300">日志中最后15个错误的 RSS 源。</span><span class="sxs-lookup"><span data-stu-id="1f535-300">An RSS feed of the last 15 errors from the log.</span></span>

<span data-ttu-id="1f535-301">使用 ELMAH 之前, 必须先安装它。</span><span class="sxs-lookup"><span data-stu-id="1f535-301">Before you can work with the ELMAH, you must install it.</span></span> <span data-ttu-id="1f535-302">使用*NuGet*包安装程序可以轻松地完成此过程。</span><span class="sxs-lookup"><span data-stu-id="1f535-302">This is easy using the *NuGet* package installer.</span></span> <span data-ttu-id="1f535-303">如本系列教程前面所述, NuGet 是一个 Visual Studio 扩展, 可让你轻松地在 Visual Studio 中安装和更新开源库和工具。</span><span class="sxs-lookup"><span data-stu-id="1f535-303">As mentioned earlier in this tutorial series, NuGet is a Visual Studio extension that makes it easy to install and update open source libraries and tools in Visual Studio.</span></span>

1. <span data-ttu-id="1f535-304">在 Visual Studio 的 "**工具**" 菜单中, 选择 " **nuget 包管理器** > " "**管理解决方案的 nuget 包**"。</span><span class="sxs-lookup"><span data-stu-id="1f535-304">Within Visual Studio, from the **Tools** menu, select **NuGet Package Manager** > **Manage NuGet Packages for Solution**.</span></span> 

    ![ASP.NET 错误处理-管理解决方案的 NuGet 包](aspnet-error-handling/_static/image6.png)
2. <span data-ttu-id="1f535-306">在 Visual Studio 中显示 "**管理 NuGet 包**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="1f535-306">The **Manage NuGet Packages** dialog box is displayed within Visual Studio.</span></span>
3. <span data-ttu-id="1f535-307">在 "**管理 NuGet 包**" 对话框中, 在左侧展开 "**联机**", 然后选择 " **nuget.org**"。然后, 从可用包列表中查找并安装**ELMAH**包。</span><span class="sxs-lookup"><span data-stu-id="1f535-307">In the **Manage NuGet Packages** dialog box, expand **Online** on the left, and then select **nuget.org**. Then, find and install the **ELMAH** package from the list of available packages online.</span></span> 

    ![ASP.NET 错误处理-ELMA NuGet 包](aspnet-error-handling/_static/image7.png)
4. <span data-ttu-id="1f535-309">需要建立 internet 连接才能下载包。</span><span class="sxs-lookup"><span data-stu-id="1f535-309">You will need to have an internet connection to download the package.</span></span>
5. <span data-ttu-id="1f535-310">在 "**选择项目**" 对话框中, 确保选择了 " **WingtipToys** " 选项, 然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="1f535-310">In the **Select Projects** dialog box, make sure the **WingtipToys** selection is selected, and then click **OK**.</span></span> 

    ![ASP.NET 错误处理-"选择项目" 对话框](aspnet-error-handling/_static/image8.png)
6. <span data-ttu-id="1f535-312">如果需要, 请在 "**管理 NuGet 包**" 对话框中单击 "**关闭**"。</span><span class="sxs-lookup"><span data-stu-id="1f535-312">Click **Close** in the **Manage NuGet Packages** dialog box if needed.</span></span>
7. <span data-ttu-id="1f535-313">如果 Visual Studio 请求你重新加载任何打开的文件, 请选择 "**全部为**"。</span><span class="sxs-lookup"><span data-stu-id="1f535-313">If Visual Studio requests that you reload any open files, select "**Yes to All**".</span></span>
8. <span data-ttu-id="1f535-314">ELMAH 包在项目根目录的 web.config 文件中添加其自身的条目。</span><span class="sxs-lookup"><span data-stu-id="1f535-314">The ELMAH package adds entries for itself in the *Web.config* file at the root of your project.</span></span> <span data-ttu-id="1f535-315">如果 Visual Studio 询问你是否要重新加载修改后的*web.config*文件, 请单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="1f535-315">If Visual Studio asks you if you want to reload the modified *Web.config* file, click **Yes**.</span></span>

<span data-ttu-id="1f535-316">ELMAH 现在可以存储发生的任何未经处理的错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-316">ELMAH is now ready to store any unhandled errors that occur.</span></span>

### <a name="viewing-the-elmah-log"></a><span data-ttu-id="1f535-317">查看 ELMAH 日志</span><span class="sxs-lookup"><span data-stu-id="1f535-317">Viewing the ELMAH Log</span></span>

<span data-ttu-id="1f535-318">查看 ELMAH 日志很简单, 但首先您将创建一个将在 ELMAH 日志中记录的未经处理的异常。</span><span class="sxs-lookup"><span data-stu-id="1f535-318">Viewing the ELMAH log is easy, but first you will create an unhandled exception that will be recorded in the ELMAH log.</span></span>

1. <span data-ttu-id="1f535-319">按**CTRL + F5**运行 Wingtip 玩具示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="1f535-319">Press **CTRL+F5** to run the Wingtip Toys sample application.</span></span>
2. <span data-ttu-id="1f535-320">若要将未经处理的异常写入 ELMAH 日志, 请在浏览器中导航到以下 URL (使用端口号):</span><span class="sxs-lookup"><span data-stu-id="1f535-320">To write an unhandled exception to the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    <span data-ttu-id="1f535-321">`https://localhost:44300/NoPage.aspx`将显示错误页。</span><span class="sxs-lookup"><span data-stu-id="1f535-321">`https://localhost:44300/NoPage.aspx` The error page will be displayed.</span></span>
3. <span data-ttu-id="1f535-322">若要显示 ELMAH 日志, 请在浏览器中导航到以下 URL (使用端口号):</span><span class="sxs-lookup"><span data-stu-id="1f535-322">To display the ELMAH log, navigate in your browser to the following URL (using your port number):</span></span>  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 错误处理-ELMAH 错误日志](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="1f535-324">总结</span><span class="sxs-lookup"><span data-stu-id="1f535-324">Summary</span></span>

<span data-ttu-id="1f535-325">在本教程中, 已了解如何在应用程序级别、页级别和代码级别处理错误。</span><span class="sxs-lookup"><span data-stu-id="1f535-325">In this tutorial, you have learned about handling errors at the application level, the page level, and the code level.</span></span> <span data-ttu-id="1f535-326">还了解了如何记录已处理和未处理的错误, 以便以后查看。</span><span class="sxs-lookup"><span data-stu-id="1f535-326">You have also learned how to log handled and unhandled errors for later review.</span></span> <span data-ttu-id="1f535-327">你已添加了 ELMAH 实用工具, 使用 NuGet 向应用程序提供异常日志记录和通知。</span><span class="sxs-lookup"><span data-stu-id="1f535-327">You added the ELMAH utility to provide exception logging and notification to your application using NuGet.</span></span> <span data-ttu-id="1f535-328">此外, 您还了解了安全错误消息的重要性。</span><span class="sxs-lookup"><span data-stu-id="1f535-328">Additionally, you have learned about the importance of safe error messages.</span></span>

## <a name="tutorial-series-conclusion"></a><span data-ttu-id="1f535-329">教程系列结论</span><span class="sxs-lookup"><span data-stu-id="1f535-329">Tutorial Series Conclusion</span></span>

<span data-ttu-id="1f535-330">感谢大家关注。</span><span class="sxs-lookup"><span data-stu-id="1f535-330">Thanks for following along.</span></span> <span data-ttu-id="1f535-331">我希望这一系列教程有助于您更熟悉 ASP.NET Web 窗体。</span><span class="sxs-lookup"><span data-stu-id="1f535-331">I hope this set of tutorials helped you become more familiar with ASP.NET Web Forms.</span></span> <span data-ttu-id="1f535-332">如果需要有关 ASP.NET 4.5 和 Visual Studio 2013 中提供的 Web 窗体功能的详细信息, 请参阅[Visual Studio 2013 发行说明 ASP.NET 和 Web 工具](../../../../visual-studio/overview/2013/release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="1f535-332">If you need more information about Web Forms features available in ASP.NET 4.5 and Visual Studio 2013, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span> <span data-ttu-id="1f535-333">另外, 请务必查看**后续步骤**部分中提到的教程, 并 defintely 试用[免费的 Azure 试用版](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1f535-333">Also, be sure to take a look at the tutorial mentioned in the **Next Steps** section and defintely try out the [free Azure trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

![感谢-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a><span data-ttu-id="1f535-335">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1f535-335">Next Steps</span></span>

<span data-ttu-id="1f535-336">有关将 web 应用程序部署到 Microsoft Azure 的详细信息, 请参阅[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)网站。</span><span class="sxs-lookup"><span data-stu-id="1f535-336">Learn more about deploying your web application to Microsoft Azure, see [Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to an Azure Web Site](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/).</span></span>

## <a name="free-trial"></a><span data-ttu-id="1f535-337">免费试用版</span><span class="sxs-lookup"><span data-stu-id="1f535-337">Free Trial</span></span>

[<span data-ttu-id="1f535-338">Microsoft Azure 免费试用版</span><span class="sxs-lookup"><span data-stu-id="1f535-338">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)  
 <span data-ttu-id="1f535-339">将网站发布到 Microsoft Azure 可节省时间、维护和支出。</span><span class="sxs-lookup"><span data-stu-id="1f535-339">Publishing your website to Microsoft Azure will save you time, maintenance and expense.</span></span> <span data-ttu-id="1f535-340">将 web 应用部署到 Azure 的过程非常简单。</span><span class="sxs-lookup"><span data-stu-id="1f535-340">It's a quick process to deploying your web app to Azure.</span></span> <span data-ttu-id="1f535-341">如果需要维护和监视 web 应用, Azure 提供各种工具和服务。</span><span class="sxs-lookup"><span data-stu-id="1f535-341">When you need to maintain and monitor your web app, Azure offers a variety of tools and services.</span></span> <span data-ttu-id="1f535-342">管理 Azure 中的数据、流量、标识、备份、消息传递、媒体和性能。</span><span class="sxs-lookup"><span data-stu-id="1f535-342">Manage data, traffic, identity, backups, messaging, media and performance in Azure.</span></span> <span data-ttu-id="1f535-343">而且, 所有这些都是以一种非常经济高效的方法提供的。</span><span class="sxs-lookup"><span data-stu-id="1f535-343">And, all of this is provided in a very cost effective approach.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1f535-344">其他资源</span><span class="sxs-lookup"><span data-stu-id="1f535-344">Additional Resources</span></span>

<span data-ttu-id="1f535-345">[通过 ASP.NET 运行状况监视记录错误详细信息](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span><span class="sxs-lookup"><span data-stu-id="1f535-345">[Logging Error Details with ASP.NET Health Monitoring](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md) </span></span>  
[<span data-ttu-id="1f535-346">ELMAH</span><span class="sxs-lookup"><span data-stu-id="1f535-346">ELMAH</span></span>](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a><span data-ttu-id="1f535-347">致谢</span><span class="sxs-lookup"><span data-stu-id="1f535-347">Acknowledgements</span></span>

<span data-ttu-id="1f535-348">我想感谢以下人员对本系列教程的内容进行了重大贡献:</span><span class="sxs-lookup"><span data-stu-id="1f535-348">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="1f535-349">Alberto Poblacion, MVP &amp; MCT, 西班牙</span><span class="sxs-lookup"><span data-stu-id="1f535-349">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- <span data-ttu-id="1f535-350">[Alex Thissen, 荷兰](http://blog.alexthissen.nl/)(twitter: [@alexthissen](http://twitter.com/alexthissen))</span><span class="sxs-lookup"><span data-stu-id="1f535-350">[Alex Thissen, Netherlands](http://blog.alexthissen.nl/) (twitter: [@alexthissen](http://twitter.com/alexthissen))</span></span>
- [<span data-ttu-id="1f535-351">美国 Andre Tournier</span><span class="sxs-lookup"><span data-stu-id="1f535-351">Andre Tournier, USA</span></span>](http://andret503.wordpress.com/)
- <span data-ttu-id="1f535-352">Apurva Joshi, Microsoft</span><span class="sxs-lookup"><span data-stu-id="1f535-352">Apurva Joshi, Microsoft</span></span>
- [<span data-ttu-id="1f535-353">Bojan Vrhovnik, 斯洛文尼亚</span><span class="sxs-lookup"><span data-stu-id="1f535-353">Bojan Vrhovnik, Slovenia</span></span>](http://twitter.com/bvrhovnik)
- <span data-ttu-id="1f535-354">[Bruno Sonnino, 巴西](http://msmvps.com/blogs/bsonnino)(twitter: [@bsonnino](http://twitter.com/bsonnino))</span><span class="sxs-lookup"><span data-stu-id="1f535-354">[Bruno Sonnino, Brazil](http://msmvps.com/blogs/bsonnino) (twitter: [@bsonnino](http://twitter.com/bsonnino))</span></span>
- [<span data-ttu-id="1f535-355">Carlos dos Santos, 巴西</span><span class="sxs-lookup"><span data-stu-id="1f535-355">Carlos dos Santos, Brazil</span></span>](http://www.carloscds.net/)
- <span data-ttu-id="1f535-356">[美国 Dave Campbell](http://www.wynapse.com/)(twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))</span><span class="sxs-lookup"><span data-stu-id="1f535-356">[Dave Campbell, USA](http://www.wynapse.com/) (twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))</span></span>
- <span data-ttu-id="1f535-357">[吴建 Galloway, Microsoft](https://weblogs.asp.net/jgalloway)(twitter: [@jongalloway](http://twitter.com/jongalloway))</span><span class="sxs-lookup"><span data-stu-id="1f535-357">[Jon Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (twitter: [@jongalloway](http://twitter.com/jongalloway))</span></span>
- <span data-ttu-id="1f535-358">[Michael Sharps](http://www.930solutions.com/)(twitter: [@mrsharps](http://twitter.com/mrsharps))</span><span class="sxs-lookup"><span data-stu-id="1f535-358">[Michael Sharps, USA](http://www.930solutions.com/) (twitter: [@mrsharps](http://twitter.com/mrsharps))</span></span>
- <span data-ttu-id="1f535-359">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="1f535-359">Mike Pope</span></span>
- <span data-ttu-id="1f535-360">[美国 Mitchel 卖方](http://www.mitchelsellers.com/)(twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))</span><span class="sxs-lookup"><span data-stu-id="1f535-360">[Mitchel Sellers, USA](http://www.mitchelsellers.com/) (twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))</span></span>
- [<span data-ttu-id="1f535-361">Paul Cociuba, Microsoft</span><span class="sxs-lookup"><span data-stu-id="1f535-361">Paul Cociuba, Microsoft</span></span>](http://linqto.me/Links/pcociuba)
- [<span data-ttu-id="1f535-362">圣保罗 Morgado, 葡萄牙</span><span class="sxs-lookup"><span data-stu-id="1f535-362">Paulo Morgado, Portugal</span></span>](http://paulomorgado.net/)
- [<span data-ttu-id="1f535-363">Pranav Rastogi 撰写, Microsoft</span><span class="sxs-lookup"><span data-stu-id="1f535-363">Pranav Rastogi, Microsoft</span></span>](https://blogs.msdn.com/b/pranav_rastogi)
- [<span data-ttu-id="1f535-364">Tim Ammann, Microsoft</span><span class="sxs-lookup"><span data-stu-id="1f535-364">Tim Ammann, Microsoft</span></span>](https://blogs.iis.net/timamm/default.aspx)
- [<span data-ttu-id="1f535-365">Tom Dykstra, Microsoft</span><span class="sxs-lookup"><span data-stu-id="1f535-365">Tom Dykstra, Microsoft</span></span>](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a><span data-ttu-id="1f535-366">社区贡献</span><span class="sxs-lookup"><span data-stu-id="1f535-366">Community Contributions</span></span>

- <span data-ttu-id="1f535-367">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span><span class="sxs-lookup"><span data-stu-id="1f535-367">Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))</span></span>  
  <span data-ttu-id="1f535-368">MSDN 上的 Visual Studio 2012 相关代码示例:[导航 Wingtip 玩具](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span><span class="sxs-lookup"><span data-stu-id="1f535-368">Visual Studio 2012 related code sample on MSDN: [Navigation Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)</span></span>
- <span data-ttu-id="1f535-369">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span><span class="sxs-lookup"><span data-stu-id="1f535-369">James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))</span></span>  
  <span data-ttu-id="1f535-370">MSDN 上的 Visual Studio 2012 相关代码示例:[Visual Basic 中的 ASP.NET 4.5 Web 窗体教程系列](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span><span class="sxs-lookup"><span data-stu-id="1f535-370">Visual Studio 2012 related code sample on MSDN: [ASP.NET 4.5 Web Forms Tutorial Series in Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)</span></span>
- <span data-ttu-id="1f535-371">Andrielle Azevedo-Microsoft 技术受众撰稿人 (twitter: @driazevedo)</span><span class="sxs-lookup"><span data-stu-id="1f535-371">Andrielle Azevedo - Microsoft Technical Audience Contributor (twitter: @driazevedo)</span></span>  
  <span data-ttu-id="1f535-372">Visual Studio 2012 翻译:[Iniciando com ASP.NET Web 窗体 4.5-Parte 1-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span><span class="sxs-lookup"><span data-stu-id="1f535-372">Visual Studio 2012 translation: [Iniciando com ASP.NET Web Forms 4.5 - Parte 1 - Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="1f535-373">上一篇</span><span class="sxs-lookup"><span data-stu-id="1f535-373">Previous</span></span>](url-routing.md)
