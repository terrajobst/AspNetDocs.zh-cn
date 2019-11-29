---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: 阻止 JavaScript 注入攻击（VB） |Microsoft Docs
author: StephenWalther
description: 阻止 JavaScript 注入攻击和跨站点脚本攻击。 在本教程中，Stephen Walther 介绍了如何轻松地消除 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: dfe09085f26c62c566649bc6f570aa25367a0f07
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594755"
---
# <a name="preventing-javascript-injection-attacks-vb"></a><span data-ttu-id="316cc-104">阻止 JavaScript 注入攻击 (VB)</span><span class="sxs-lookup"><span data-stu-id="316cc-104">Preventing JavaScript Injection Attacks (VB)</span></span>

<span data-ttu-id="316cc-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="316cc-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="316cc-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="316cc-106">Download PDF</span></span>](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> <span data-ttu-id="316cc-107">阻止 JavaScript 注入攻击和跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="316cc-107">Prevent JavaScript Injection Attacks and Cross-Site Scripting Attacks from happening to you.</span></span> <span data-ttu-id="316cc-108">在本教程中，Stephen Walther 介绍了如何通过 HTML 编码内容轻松抵御这些类型的攻击。</span><span class="sxs-lookup"><span data-stu-id="316cc-108">In this tutorial, Stephen Walther explains how you can easily defeat these types of attacks by HTML encoding your content.</span></span>

<span data-ttu-id="316cc-109">本教程的目的是介绍如何防止 ASP.NET MVC 应用程序中出现 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="316cc-109">The goal of this tutorial is to explain how you can prevent JavaScript injection attacks in your ASP.NET MVC applications.</span></span> <span data-ttu-id="316cc-110">本教程讨论了用于防范 JavaScript 注入攻击网站的两种方法。</span><span class="sxs-lookup"><span data-stu-id="316cc-110">This tutorial discusses two approaches to defending your website against a JavaScript injection attack.</span></span> <span data-ttu-id="316cc-111">了解如何通过对显示的数据进行编码来防止 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="316cc-111">You learn how to prevent JavaScript injection attacks by encoding the data that you display.</span></span> <span data-ttu-id="316cc-112">你还将了解如何通过对你接受的数据进行编码来防止 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="316cc-112">You also learn how to prevent JavaScript injection attacks by encoding the data that you accept.</span></span>

## <a name="what-is-a-javascript-injection-attack"></a><span data-ttu-id="316cc-113">什么是 JavaScript 注入攻击？</span><span class="sxs-lookup"><span data-stu-id="316cc-113">What is a JavaScript Injection Attack?</span></span>

<span data-ttu-id="316cc-114">只要你接受用户输入并重新显示用户输入，就会打开你的网站，并显示 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="316cc-114">Whenever you accept user input and redisplay the user input, you open your website to JavaScript injection attacks.</span></span> <span data-ttu-id="316cc-115">我们来看一看公开了 JavaScript 注入攻击的具体应用程序。</span><span class="sxs-lookup"><span data-stu-id="316cc-115">Let's examine a concrete application that is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="316cc-116">假设您已经创建了一个客户反馈网站（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="316cc-116">Imagine that you have created a customer feedback website (see Figure 1).</span></span> <span data-ttu-id="316cc-117">客户可以访问该网站，并使用你的产品输入其体验的反馈。</span><span class="sxs-lookup"><span data-stu-id="316cc-117">Customers can visit the website and enter feedback on their experience using your products.</span></span> <span data-ttu-id="316cc-118">当客户提交其反馈时，反馈页面上会重新显示反馈。</span><span class="sxs-lookup"><span data-stu-id="316cc-118">When a customer submits their feedback, the feedback is redisplayed on the feedback page.</span></span>

<span data-ttu-id="316cc-119">[![客户反馈网站](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="316cc-119">[![Customer Feedback Website](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)</span></span>

<span data-ttu-id="316cc-120">**图 01**：客户反馈网站（[单击查看全尺寸图像](preventing-javascript-injection-attacks-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="316cc-120">**Figure 01**: Customer Feedback Website ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image3.png))</span></span>

<span data-ttu-id="316cc-121">客户反馈网站使用列表1中的 `controller`。</span><span class="sxs-lookup"><span data-stu-id="316cc-121">The customer feedback website uses the `controller` in Listing 1.</span></span> <span data-ttu-id="316cc-122">此 `controller` 包含两个名为 `Index()` 和 `Create()`的操作。</span><span class="sxs-lookup"><span data-stu-id="316cc-122">This `controller` contains two actions named `Index()` and `Create()`.</span></span>

<span data-ttu-id="316cc-123">**列表1– `HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="316cc-123">**Listing 1 – `HomeController.vb`**</span></span>

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

<span data-ttu-id="316cc-124">`Index()` 方法显示 `Index` 视图。</span><span class="sxs-lookup"><span data-stu-id="316cc-124">The `Index()` method displays the `Index` view.</span></span> <span data-ttu-id="316cc-125">此方法通过从数据库检索反馈（使用 LINQ to SQL 查询）将以前的所有客户反馈传递到 `Index` 视图。</span><span class="sxs-lookup"><span data-stu-id="316cc-125">This method passes all of the previous customer feedback to the `Index` view by retrieving the feedback from the database (using a LINQ to SQL query).</span></span>

<span data-ttu-id="316cc-126">`Create()` 方法创建新的反馈项并将其添加到数据库中。</span><span class="sxs-lookup"><span data-stu-id="316cc-126">The `Create()` method creates a new Feedback item and adds it to the database.</span></span> <span data-ttu-id="316cc-127">客户在窗体中输入的消息将传递给 message 参数中的 `Create()` 方法。</span><span class="sxs-lookup"><span data-stu-id="316cc-127">The message that the customer enters in the form is passed to the `Create()` method in the message parameter.</span></span> <span data-ttu-id="316cc-128">将创建一个反馈项，并将该消息分配给反馈项的 `Message` 属性。</span><span class="sxs-lookup"><span data-stu-id="316cc-128">A Feedback item is created and the message is assigned to the Feedback item's `Message` property.</span></span> <span data-ttu-id="316cc-129">通过 `DataContext.SubmitChanges()` 方法调用将反馈项提交到数据库。</span><span class="sxs-lookup"><span data-stu-id="316cc-129">The Feedback item is submitted to the database with the `DataContext.SubmitChanges()` method call.</span></span> <span data-ttu-id="316cc-130">最后，访问者将重定向回 `Index` 视图，其中显示了所有反馈。</span><span class="sxs-lookup"><span data-stu-id="316cc-130">Finally, the visitor is redirected back to the `Index` view where all of the feedback is displayed.</span></span>

<span data-ttu-id="316cc-131">`Index` 视图包含在清单2中。</span><span class="sxs-lookup"><span data-stu-id="316cc-131">The `Index` view is contained in Listing 2.</span></span>

<span data-ttu-id="316cc-132">**列表2– `Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="316cc-132">**Listing 2 – `Index.aspx`**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

<span data-ttu-id="316cc-133">`Index` 视图包含两部分。</span><span class="sxs-lookup"><span data-stu-id="316cc-133">The `Index` view has two sections.</span></span> <span data-ttu-id="316cc-134">顶部部分包含实际的客户反馈窗体。</span><span class="sxs-lookup"><span data-stu-id="316cc-134">The top section contains the actual customer feedback form.</span></span> <span data-ttu-id="316cc-135">下半部分包含用于的。每个循环遍历前面的所有客户反馈项，并显示每个反馈项的 EntryDate 和消息属性。</span><span class="sxs-lookup"><span data-stu-id="316cc-135">The bottom section contains a For..Each loop that loops through all of the previous customer feedback items and displays the EntryDate and Message properties for each feedback item.</span></span>

<span data-ttu-id="316cc-136">客户反馈网站是一个简单的网站。</span><span class="sxs-lookup"><span data-stu-id="316cc-136">The customer feedback website is a simple website.</span></span> <span data-ttu-id="316cc-137">遗憾的是，该网站公开了 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="316cc-137">Unfortunately, the website is open to JavaScript injection attacks.</span></span>

<span data-ttu-id="316cc-138">假设您在客户反馈窗体中输入以下文本：</span><span class="sxs-lookup"><span data-stu-id="316cc-138">Imagine that you enter the following text into the customer feedback form:</span></span>

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

<span data-ttu-id="316cc-139">此文本表示显示警报消息框的 JavaScript 脚本。</span><span class="sxs-lookup"><span data-stu-id="316cc-139">This text represents a JavaScript script that displays an alert message box.</span></span> <span data-ttu-id="316cc-140">有人将此脚本提交到反馈窗体后，消息<em>Boo！</em>只要有人在以后访问客户反馈网站，就会出现此情况（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="316cc-140">After someone submits this script into the feedback form, the message <em>Boo!</em>will appear whenever anyone visits the customer feedback website in the future (see Figure 2).</span></span>

<span data-ttu-id="316cc-141">[![JavaScript 注入](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="316cc-141">[![JavaScript Injection](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)</span></span>

<span data-ttu-id="316cc-142">**图 02**： JavaScript 注入（[单击以查看完全大小的映像](preventing-javascript-injection-attacks-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="316cc-142">**Figure 02**: JavaScript Injection ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image6.png))</span></span>

<span data-ttu-id="316cc-143">现在，最初对 JavaScript 注入攻击的响应可能是自傲的。</span><span class="sxs-lookup"><span data-stu-id="316cc-143">Now, your initial response to JavaScript injection attacks might be apathy.</span></span> <span data-ttu-id="316cc-144">您可能认为 JavaScript 注入攻击只是一种*篡改*攻击。</span><span class="sxs-lookup"><span data-stu-id="316cc-144">You might think that JavaScript injection attacks are simply a type of *defacement* attack.</span></span> <span data-ttu-id="316cc-145">你可能会相信，任何人都不能通过提交 JavaScript 注入攻击来执行任何操作。</span><span class="sxs-lookup"><span data-stu-id="316cc-145">You might believe that no one can do anything truly evil by committing a JavaScript injection attack.</span></span>

<span data-ttu-id="316cc-146">遗憾的是，黑客可以通过将 JavaScript 注入到网站来完成一些实际工作。</span><span class="sxs-lookup"><span data-stu-id="316cc-146">Unfortunately, a hacker can do some really, really evil things by injecting JavaScript into a website.</span></span> <span data-ttu-id="316cc-147">你可以使用 JavaScript 注入攻击来执行跨站点脚本（XSS）攻击。</span><span class="sxs-lookup"><span data-stu-id="316cc-147">You can use a JavaScript injection attack to perform a Cross-Site Scripting (XSS) attack.</span></span> <span data-ttu-id="316cc-148">在跨站点脚本攻击中，会盗取机密用户信息，并将信息发送到其他网站。</span><span class="sxs-lookup"><span data-stu-id="316cc-148">In a Cross-Site Scripting attack, you steal confidential user information and send the information to another website.</span></span>

<span data-ttu-id="316cc-149">例如，黑客可以使用 JavaScript 注入攻击来窃取其他用户的浏览器 cookie 值。</span><span class="sxs-lookup"><span data-stu-id="316cc-149">For example, a hacker can use a JavaScript injection attack to steal the values of browser cookies from other users.</span></span> <span data-ttu-id="316cc-150">如果敏感信息（如密码、信用卡号或社会安全号码）存储在浏览器 cookie 中，则黑客可以使用 JavaScript 注入攻击来窃取此信息。</span><span class="sxs-lookup"><span data-stu-id="316cc-150">If sensitive information -- such as passwords, credit card numbers, or social security numbers – is stored in the browser cookies, then a hacker can use a JavaScript injection attack to steal this information.</span></span> <span data-ttu-id="316cc-151">或者，如果用户在页面中包含的窗体字段中输入的敏感信息已受到 JavaScript 攻击，则黑客可以使用注入的 JavaScript 来捕获窗体数据并将其发送到另一个网站。</span><span class="sxs-lookup"><span data-stu-id="316cc-151">Or, if a user enters sensitive information in a form field contained in a page that has been compromised with a JavaScript attack, then the hacker can use the injected JavaScript to grab the form data and send it to another website.</span></span>

<span data-ttu-id="316cc-152">*请恐惧*。</span><span class="sxs-lookup"><span data-stu-id="316cc-152">*Please be scared*.</span></span> <span data-ttu-id="316cc-153">认真考虑 JavaScript 注入攻击，并保护用户的机密信息。</span><span class="sxs-lookup"><span data-stu-id="316cc-153">Take JavaScript injection attacks seriously and protect your user's confidential information.</span></span> <span data-ttu-id="316cc-154">在接下来的两个部分中，我们将介绍两种可用于阻止 ASP.NET MVC 应用程序防御 JavaScript 注入式攻击的技术。</span><span class="sxs-lookup"><span data-stu-id="316cc-154">In the next two sections, we discuss two techniques that you can use to defend your ASP.NET MVC applications from JavaScript injection attacks.</span></span>

## <a name="approach-1-html-encode-in-the-view"></a><span data-ttu-id="316cc-155">方法 #1：视图中的 HTML 编码</span><span class="sxs-lookup"><span data-stu-id="316cc-155">Approach #1: HTML Encode in the View</span></span>

<span data-ttu-id="316cc-156">阻止 JavaScript 注入攻击的一种简单方法是在视图中重新显示数据时对网站用户输入的任何数据进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="316cc-156">One easy method of preventing JavaScript injection attacks is to HTML encode any data entered by website users when you redisplay the data in a view.</span></span> <span data-ttu-id="316cc-157">在列表3中更新的 `Index` 视图遵循此方法。</span><span class="sxs-lookup"><span data-stu-id="316cc-157">The updated `Index` view in Listing 3 follows this approach.</span></span>

<span data-ttu-id="316cc-158">**列表 3-`Index.aspx` （HTML 编码）**</span><span class="sxs-lookup"><span data-stu-id="316cc-158">**Listing 3 – `Index.aspx` (HTML Encoded)**</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

<span data-ttu-id="316cc-159">请注意，在显示值之前，`feedback.Message` 的值为 HTML 编码，并显示以下代码：</span><span class="sxs-lookup"><span data-stu-id="316cc-159">Notice that the value of `feedback.Message` is HTML encoded before the value is displayed with the following code:</span></span>

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

<span data-ttu-id="316cc-160">对字符串进行 HTML 编码是什么意思？</span><span class="sxs-lookup"><span data-stu-id="316cc-160">What does it mean to HTML encode a string?</span></span> <span data-ttu-id="316cc-161">在对字符串进行 HTML 编码时，诸如 `<` 和 `>` 之类的危险字符将替换为 HTML 实体引用，如 `&lt;` 和 `&gt;`。</span><span class="sxs-lookup"><span data-stu-id="316cc-161">When you HTML encode a string, dangerous characters such as `<` and `>` are replaced by HTML entity references such as `&lt;` and `&gt;`.</span></span> <span data-ttu-id="316cc-162">因此，如果字符串 `<script>alert("Boo!")</script>` 是 HTML 编码的，则会将其转换为 `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`。</span><span class="sxs-lookup"><span data-stu-id="316cc-162">So when the string `<script>alert("Boo!")</script>` is HTML encoded, it gets converted to `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`.</span></span> <span data-ttu-id="316cc-163">当浏览器解释时，已编码的字符串不再作为 JavaScript 脚本执行。</span><span class="sxs-lookup"><span data-stu-id="316cc-163">The encoded string no longer executes as a JavaScript script when interpreted by a browser.</span></span> <span data-ttu-id="316cc-164">相反，你会看到图3中的无害页面。</span><span class="sxs-lookup"><span data-stu-id="316cc-164">Instead, you get the harmless page in Figure 3.</span></span>

<span data-ttu-id="316cc-165">[![失效的 JavaScript 攻击](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="316cc-165">[![Defeated JavaScript Attack](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)</span></span>

<span data-ttu-id="316cc-166">**图 03**：无法通过 JavaScript 攻击（[单击查看完全大小的映像](preventing-javascript-injection-attacks-vb/_static/image9.png)）</span><span class="sxs-lookup"><span data-stu-id="316cc-166">**Figure 03**: Defeated JavaScript Attack ([Click to view full-size image](preventing-javascript-injection-attacks-vb/_static/image9.png))</span></span>

<span data-ttu-id="316cc-167">请注意，在列表3的 `Index` 视图中，只对 `feedback.Message` 的值进行编码。</span><span class="sxs-lookup"><span data-stu-id="316cc-167">Notice that in the `Index` view in Listing 3 only the value of `feedback.Message` is encoded.</span></span> <span data-ttu-id="316cc-168">不编码 `feedback.EntryDate` 的值。</span><span class="sxs-lookup"><span data-stu-id="316cc-168">The value of `feedback.EntryDate` is not encoded.</span></span> <span data-ttu-id="316cc-169">只需对用户输入的数据进行编码。</span><span class="sxs-lookup"><span data-stu-id="316cc-169">You only need to encode data entered by a user.</span></span> <span data-ttu-id="316cc-170">因为 EntryDate 的值是在控制器中生成的，所以无需对此值进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="316cc-170">Because the value of EntryDate was generated in the controller, you don't need to HTML encode this value.</span></span>

## <a name="approach-2-html-encode-in-the-controller"></a><span data-ttu-id="316cc-171">方法 #2：控制器中的 HTML 编码</span><span class="sxs-lookup"><span data-stu-id="316cc-171">Approach #2: HTML Encode in the Controller</span></span>

<span data-ttu-id="316cc-172">当你在视图中显示数据时，你可以在将数据提交到数据库之前对数据进行 HTML 编码，而不是使用 HTML 编码数据。</span><span class="sxs-lookup"><span data-stu-id="316cc-172">Instead of HTML encoding data when you display the data in a view, you can HTML encode the data just before you submit the data to the database.</span></span> <span data-ttu-id="316cc-173">此第二种方法是在列出 4 `controller` 的情况下执行的。</span><span class="sxs-lookup"><span data-stu-id="316cc-173">This second approach is taken in the case of the `controller` in Listing 4.</span></span>

<span data-ttu-id="316cc-174">**列表 4-`HomeController.cs` （HTML 编码）**</span><span class="sxs-lookup"><span data-stu-id="316cc-174">**Listing 4 – `HomeController.cs` (HTML Encoded)**</span></span>

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

<span data-ttu-id="316cc-175">请注意，在 `Create()` 操作内将值提交到数据库之前，消息的值是 HTML 编码的。</span><span class="sxs-lookup"><span data-stu-id="316cc-175">Notice that the value of Message is HTML encoded before the value is submitted to the database within the `Create()` action.</span></span> <span data-ttu-id="316cc-176">当消息重新显示在视图中时，消息是 HTML 编码的，并且不会执行消息中注入的任何 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="316cc-176">When the Message is redisplayed in the view, the Message is HTML encoded and any JavaScript injected in the Message is not executed.</span></span>

<span data-ttu-id="316cc-177">通常，您应该优先考虑本教程中介绍的第一种方法。</span><span class="sxs-lookup"><span data-stu-id="316cc-177">Typically, you should favor the first approach discussed in this tutorial over this second approach.</span></span> <span data-ttu-id="316cc-178">此第二种方法的问题是，你最终会在数据库中得到 HTML 编码数据。</span><span class="sxs-lookup"><span data-stu-id="316cc-178">The problem with this second approach is that you end up with HTML encoded data in your database.</span></span> <span data-ttu-id="316cc-179">换句话说，您的数据库数据更新具有有趣的字符。</span><span class="sxs-lookup"><span data-stu-id="316cc-179">In other words, your database data is dirtied with funny looking characters.</span></span>

<span data-ttu-id="316cc-180">为什么这很糟糕？</span><span class="sxs-lookup"><span data-stu-id="316cc-180">Why is this bad?</span></span> <span data-ttu-id="316cc-181">如果需要在网页以外的其他内容中显示数据库数据，则会出现问题。</span><span class="sxs-lookup"><span data-stu-id="316cc-181">If you ever need to display the database data in something other than a web page, then you will have problems.</span></span> <span data-ttu-id="316cc-182">例如，你无法在 Windows 窗体的应用程序中轻松地显示数据。</span><span class="sxs-lookup"><span data-stu-id="316cc-182">For example, you can no longer easily display the data in a Windows Forms application.</span></span>

## <a name="summary"></a><span data-ttu-id="316cc-183">总结</span><span class="sxs-lookup"><span data-stu-id="316cc-183">Summary</span></span>

<span data-ttu-id="316cc-184">本教程的目的是心有余悸您对 JavaScript 注入攻击的目标。</span><span class="sxs-lookup"><span data-stu-id="316cc-184">The purpose of this tutorial was to scare you about the prospect of a JavaScript injection attack.</span></span> <span data-ttu-id="316cc-185">本教程讨论了两种防御 JavaScript 注入式攻击的 ASP.NET MVC 应用程序的方法：可以通过 HTML 编码方式在视图中编码用户提交的数据，也可以在控制器中对用户提交的数据进行 HTML 编码。</span><span class="sxs-lookup"><span data-stu-id="316cc-185">This tutorial discussed two approaches for defending your ASP.NET MVC applications against JavaScript injection attacks: you can either HTML encode user submitted data in the view or you can HTML encode user submitted data in the controller.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="316cc-186">上一部分</span><span class="sxs-lookup"><span data-stu-id="316cc-186">Previous</span></span>](authenticating-users-with-windows-authentication-vb.md)
