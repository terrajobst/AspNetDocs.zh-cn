---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: 使用 AJAX 交付动态更新 |Microsoft Docs
author: microsoft
description: 步骤10实现对已登录用户的支持：通过使用晚餐详细信息中集成的基于 Ajax 的方法对已登录的用户进行的兴趣
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486308"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a><span data-ttu-id="088bf-103">使用 AJAX 提供动态更新</span><span class="sxs-lookup"><span data-stu-id="088bf-103">Use AJAX to Deliver Dynamic Updates</span></span>

<span data-ttu-id="088bf-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="088bf-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="088bf-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="088bf-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="088bf-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的步骤10，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="088bf-106">This is step 10 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="088bf-107">步骤10使用 "晚餐详细信息" 页中集成的基于 Ajax 的方法，实现对已登录用户的支持，以使其对参加晚宴感兴趣。</span><span class="sxs-lookup"><span data-stu-id="088bf-107">Step 10 implements support for logged-in users to RSVP their interest in attending a dinner, using an Ajax-based approach integrated within the dinner details page.</span></span>
> 
> <span data-ttu-id="088bf-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="088bf-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a><span data-ttu-id="088bf-109">NerdDinner 步骤10： AJAX 启用 RSVPs 接受</span><span class="sxs-lookup"><span data-stu-id="088bf-109">NerdDinner Step 10: AJAX Enabling RSVPs Accepts</span></span>

<span data-ttu-id="088bf-110">现在，让我们将对已登录用户的支持用于向你提供对参加晚宴的兴趣。</span><span class="sxs-lookup"><span data-stu-id="088bf-110">Let's now implement support for logged-in users to RSVP their interest in attending a dinner.</span></span> <span data-ttu-id="088bf-111">我们将使用 "晚餐详细信息" 页中集成的基于 AJAX 的方法启用此项。</span><span class="sxs-lookup"><span data-stu-id="088bf-111">We'll enable this using an AJAX-based approach integrated within the dinner details page.</span></span>

### <a name="indicating-whether-the-user-is-rsvpd"></a><span data-ttu-id="088bf-112">指示用户是否为 RSVP</span><span class="sxs-lookup"><span data-stu-id="088bf-112">Indicating whether the user is RSVP'd</span></span>

<span data-ttu-id="088bf-113">用户可以访问 */Dinners/Details/[id*] URL 来查看有关特定晚餐的详细信息：</span><span class="sxs-lookup"><span data-stu-id="088bf-113">Users can visit the */Dinners/Details/[id*] URL to see details about a particular dinner:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

<span data-ttu-id="088bf-114">详细信息（）操作方法的实现如下所示：</span><span class="sxs-lookup"><span data-stu-id="088bf-114">The Details() action method is implemented like so:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

<span data-ttu-id="088bf-115">实现 RSVP 支持的第一步是将 "IsUserRegistered （用户名）" 帮助器方法添加到晚餐对象（在前面构建的 Dinner.cs 分部类中）。</span><span class="sxs-lookup"><span data-stu-id="088bf-115">Our first step to implement RSVP support will be to add an "IsUserRegistered(username)" helper method to our Dinner object (within the Dinner.cs partial class we built earlier).</span></span> <span data-ttu-id="088bf-116">此帮助器方法返回 true 或 false，具体取决于用户当前是否为晚宴，以获取晚餐：</span><span class="sxs-lookup"><span data-stu-id="088bf-116">This helper method returns true or false depending on whether the user is currently RSVP'd for the Dinner:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

<span data-ttu-id="088bf-117">然后，可以将以下代码添加到详细信息 .aspx 视图模板，以显示相应的消息，指示用户是否已注册事件：</span><span class="sxs-lookup"><span data-stu-id="088bf-117">We can then add the following code to our Details.aspx view template to display an appropriate message indicating whether the user is registered or not for the event:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

<span data-ttu-id="088bf-118">现在，当用户访问晚餐时，他们将会看到以下消息：</span><span class="sxs-lookup"><span data-stu-id="088bf-118">And now when a user visits a Dinner they are registered for they'll see this message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

<span data-ttu-id="088bf-119">当他们访问晚餐时，他们并未注册，会看到以下消息：</span><span class="sxs-lookup"><span data-stu-id="088bf-119">And when they visit a Dinner they are not registered for they'll see the below message:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a><span data-ttu-id="088bf-120">实现注册操作方法</span><span class="sxs-lookup"><span data-stu-id="088bf-120">Implementing the Register Action Method</span></span>

<span data-ttu-id="088bf-121">现在，让我们添加使用户能够通过 "详细信息" 页获取晚餐的必要功能。</span><span class="sxs-lookup"><span data-stu-id="088bf-121">Let's now add the functionality necessary to enable users to RSVP for a dinner from the details page.</span></span>

<span data-ttu-id="088bf-122">若要实现此方法，我们将创建一个新的 "RSVPController" 类，方法是右键单击 "\Controllers" 目录，然后选择 "&gt;控制器" 菜单命令。</span><span class="sxs-lookup"><span data-stu-id="088bf-122">To implement this, we'll create a new "RSVPController" class by right-clicking on the \Controllers directory and choosing the Add-&gt;Controller menu command.</span></span>

<span data-ttu-id="088bf-123">我们会在新的 RSVPController 类内实现一个 "注册" 操作方法，该方法采用获取晚餐的 id 作为参数，检索相应的晚餐对象，检查登录用户当前是否处于已注册的用户列表，以及不为其添加 RSVP 对象：</span><span class="sxs-lookup"><span data-stu-id="088bf-123">We'll implement a "Register" action method within the new RSVPController class that takes an id for a Dinner as an argument, retrieves the appropriate Dinner object, checks to see if the logged-in user is currently in the list of users who have registered for it, and if not adds an RSVP object for them:</span></span>

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

<span data-ttu-id="088bf-124">请注意，我们如何将简单字符串返回为操作方法的输出。</span><span class="sxs-lookup"><span data-stu-id="088bf-124">Notice above how we are returning a simple string as the output of the action method.</span></span> <span data-ttu-id="088bf-125">我们可以将此消息嵌入到视图模板中，但由于它太小了，因此我们只需在控制器基类上使用 Content （） helper 方法，并返回如上所示的字符串消息。</span><span class="sxs-lookup"><span data-stu-id="088bf-125">We could have embedded this message within a view template – but since it is so small we'll just use the Content() helper method on the controller base class and return a string message like above.</span></span>

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a><span data-ttu-id="088bf-126">使用 AJAX 调用 RSVPForEvent 操作方法</span><span class="sxs-lookup"><span data-stu-id="088bf-126">Calling the RSVPForEvent Action Method using AJAX</span></span>

<span data-ttu-id="088bf-127">我们将使用 AJAX 从详细信息视图中调用注册操作方法。</span><span class="sxs-lookup"><span data-stu-id="088bf-127">We'll use AJAX to invoke the Register action method from our Details view.</span></span> <span data-ttu-id="088bf-128">实现此过程相当简单。</span><span class="sxs-lookup"><span data-stu-id="088bf-128">Implementing this is pretty easy.</span></span> <span data-ttu-id="088bf-129">首先，我们将添加两个脚本库引用：</span><span class="sxs-lookup"><span data-stu-id="088bf-129">First we'll add two script library references:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

<span data-ttu-id="088bf-130">第一个库引用核心 ASP.NET AJAX 客户端脚本库。</span><span class="sxs-lookup"><span data-stu-id="088bf-130">The first library references the core ASP.NET AJAX client-side script library.</span></span> <span data-ttu-id="088bf-131">此文件的大小大约为24k，包含核心客户端 AJAX 功能。</span><span class="sxs-lookup"><span data-stu-id="088bf-131">This file is approximately 24k in size (compressed) and contains core client-side AJAX functionality.</span></span> <span data-ttu-id="088bf-132">第二个库包含与 ASP.NET MVC 的内置 AJAX 帮助器方法（稍后将用到）集成的实用工具函数。</span><span class="sxs-lookup"><span data-stu-id="088bf-132">The second library contains utility functions that integrate with ASP.NET MVC's built-in AJAX helper methods (which we'll use shortly).</span></span>

<span data-ttu-id="088bf-133">接下来，我们可以更新前面添加的视图模板代码，使其不会输出 "未注册此事件" 消息，而是呈现一个链接，当推送时，该链接将在我们的 RSVP 控制器上执行调用我们的 RSVPForEvent 操作方法的 AJAX 调用并 RSVPs 用户：</span><span class="sxs-lookup"><span data-stu-id="088bf-133">We can then update the view template code we added earlier so that instead of outputting a "You are not registered for this event" message, we instead render a link that when pushed performs an AJAX call that invokes our RSVPForEvent action method on our RSVP controller and RSVPs the user:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

<span data-ttu-id="088bf-134">上面使用的 Ajax （） helper 方法内置于 ASP.NET MVC 中，它类似于 Html.actionlink （） helper 方法，不同之处在于，在单击链接时，它会向操作方法发出 AJAX 调用。</span><span class="sxs-lookup"><span data-stu-id="088bf-134">The Ajax.ActionLink() helper method used above is built-into ASP.NET MVC and is similar to the Html.ActionLink() helper method except that instead of performing a standard navigation it makes an AJAX call to the action method when the link is clicked.</span></span> <span data-ttu-id="088bf-135">以上，我们将对 "RSVP" 控制器调用 "Register" 操作方法，并将 DinnerID 作为 "id" 参数传递给它。</span><span class="sxs-lookup"><span data-stu-id="088bf-135">Above we are calling the "Register" action method on the "RSVP" controller and passing the DinnerID as the "id" parameter to it.</span></span> <span data-ttu-id="088bf-136">要传递的最终 AjaxOptions 参数表示我们要获取从操作方法返回的内容，并更新 id 为 "rsvpmsg" 的页面上的 HTML &lt;div&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="088bf-136">The final AjaxOptions parameter we are passing indicates that we want to take the content returned from the action method and update the HTML &lt;div&gt; element on the page whose id is "rsvpmsg".</span></span>

<span data-ttu-id="088bf-137">现在，当用户浏览到未注册的晚餐时，他们将看到一个到 RSVP 的链接：</span><span class="sxs-lookup"><span data-stu-id="088bf-137">And now when a user browses to a dinner they aren't registered for yet they'll see a link to RSVP for it:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

<span data-ttu-id="088bf-138">如果他们单击 "此事件的 RSVP" 链接，则他们将对 RSVP 控制器进行 AJAX 调用注册操作方法，并在完成后，会看到如下所示的更新消息：</span><span class="sxs-lookup"><span data-stu-id="088bf-138">If they click the "RSVP for this event" link they'll make an AJAX call to the Register action method on the RSVP controller, and when it completes they'll see an updated message like below:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

<span data-ttu-id="088bf-139">进行此 AJAX 调用时所涉及的网络带宽和流量确实非常轻量。</span><span class="sxs-lookup"><span data-stu-id="088bf-139">The network bandwidth and traffic involved when making this AJAX call is really lightweight.</span></span> <span data-ttu-id="088bf-140">当用户单击 "此事件的 RSVP" 链接时，将对 */Dinners/Register/1* URL 发出小型 HTTP POST 网络请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="088bf-140">When the user clicks on the "RSVP for this event" link, a small HTTP POST network request is made to the */Dinners/Register/1* URL that looks like below on the wire:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

<span data-ttu-id="088bf-141">来自注册操作方法的响应只是：</span><span class="sxs-lookup"><span data-stu-id="088bf-141">And the response from our Register action method is simply:</span></span>

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

<span data-ttu-id="088bf-142">此轻型调用速度快，甚至在慢速网络上都可以工作。</span><span class="sxs-lookup"><span data-stu-id="088bf-142">This lightweight call is fast and will work even over a slow network.</span></span>

### <a name="adding-a-jquery-animation"></a><span data-ttu-id="088bf-143">添加 jQuery 动画</span><span class="sxs-lookup"><span data-stu-id="088bf-143">Adding a jQuery Animation</span></span>

<span data-ttu-id="088bf-144">我们实现的 AJAX 功能非常有效和快速。</span><span class="sxs-lookup"><span data-stu-id="088bf-144">The AJAX functionality we implemented works well and fast.</span></span> <span data-ttu-id="088bf-145">有时，这种情况很快，用户可能不会注意到 RSVP 链接已替换为新文本。</span><span class="sxs-lookup"><span data-stu-id="088bf-145">Sometimes it can happen so fast, though, that a user might not notice that the RSVP link has been replaced with new text.</span></span> <span data-ttu-id="088bf-146">为了使结果稍微明显明了，我们可以添加一个简单的动画来强调更新消息。</span><span class="sxs-lookup"><span data-stu-id="088bf-146">To make the outcome a little more obvious we can add a simple animation to draw attention to the update message.</span></span>

<span data-ttu-id="088bf-147">默认的 ASP.NET MVC 项目模板包含 jQuery – Microsoft 也支持的极佳（和非常流行的）开源 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="088bf-147">The default ASP.NET MVC project template includes jQuery – an excellent (and very popular) open source JavaScript library that is also supported by Microsoft.</span></span> <span data-ttu-id="088bf-148">jQuery 提供了许多功能，包括良好的 HTML DOM 选择和效果库。</span><span class="sxs-lookup"><span data-stu-id="088bf-148">jQuery provides a number of features, including a nice HTML DOM selection and effects library.</span></span>

<span data-ttu-id="088bf-149">若要使用 jQuery，我们首先要向其添加脚本引用。</span><span class="sxs-lookup"><span data-stu-id="088bf-149">To use jQuery we'll first add a script reference to it.</span></span> <span data-ttu-id="088bf-150">由于我们将在我们的站点中的各种地方使用 jQuery，因此我们将在我们的站点中添加脚本引用。主母版页文件，以便所有页面都可以使用它。</span><span class="sxs-lookup"><span data-stu-id="088bf-150">Because we are going to be using jQuery within a variety of places within our site, we'll add the script reference within our Site.master master page file so that all pages can use it.</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

<span data-ttu-id="088bf-151">*提示：请确保已安装用于 VS 2008 SP1 的 JavaScript intellisense 修补程序，以便为 JavaScript 文件（包括 jQuery）启用更丰富的 intellisense 支持。可以从以下内容下载： http://tinyurl.com/vs2008javascripthotfix*</span><span class="sxs-lookup"><span data-stu-id="088bf-151">*Tip: make sure you have installed the JavaScript intellisense hotfix for VS 2008 SP1 that enables richer intellisense support for JavaScript files (including jQuery). You can download it from: http://tinyurl.com/vs2008javascripthotfix*</span></span>

<span data-ttu-id="088bf-152">使用 JQuery 编写的代码通常使用全局 "$ （）" JavaScript 方法，该方法可使用 CSS 选择器检索一个或多个 HTML 元素。</span><span class="sxs-lookup"><span data-stu-id="088bf-152">Code written using JQuery often uses a global "$()" JavaScript method that retrieves one or more HTML elements using a CSS selector.</span></span> <span data-ttu-id="088bf-153">例如， *$ （"#rsvpmsg"）* 选择 id 为 rsvpmsg 的任何 HTML 元素，而 *$ （"."）* 将选择具有 "内容" CSS 类名称的所有元素。</span><span class="sxs-lookup"><span data-stu-id="088bf-153">For example, *$("#rsvpmsg")* selects any HTML element with the id of rsvpmsg, while *$(".something")* would select all elements with the "something" CSS class name.</span></span> <span data-ttu-id="088bf-154">你还可以使用选择器查询（如： *$ （"input [@type= 收音机] [@checked]"）* 编写更多高级查询，如 "返回所有选中的单选按钮"。</span><span class="sxs-lookup"><span data-stu-id="088bf-154">You can also write more advanced queries like "return all of the checked radio buttons" using a selector query like: *$("input[@type=radio][@checked]")*.</span></span>

<span data-ttu-id="088bf-155">选择元素后，可以对其调用方法来执行操作，如隐藏它们： *$ （"#rsvpmsg"）。 hide （）;*</span><span class="sxs-lookup"><span data-stu-id="088bf-155">Once you've selected elements, you can call methods on them to take action, like hiding them: *$("#rsvpmsg").hide();*</span></span>

<span data-ttu-id="088bf-156">对于 RSVP 方案，我们将定义一个名为 "AnimateRSVPMessage" 的简单 JavaScript 函数，该函数选择 "rsvpmsg" &lt;div&gt; 并对其文本内容的大小进行动画处理。</span><span class="sxs-lookup"><span data-stu-id="088bf-156">For our RSVP scenario, we'll define a simple JavaScript function named "AnimateRSVPMessage" that selects the "rsvpmsg" &lt;div&gt; and animates the size of its text content.</span></span> <span data-ttu-id="088bf-157">下面的代码将小小小，并使其在400毫秒的时间范围内增加：</span><span class="sxs-lookup"><span data-stu-id="088bf-157">The below code starts the text small and then causes it to increase over a 400 milliseconds timeframe:</span></span>

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

<span data-ttu-id="088bf-158">接下来，我们可以将此 JavaScript 函数连接到 AJAX 调用成功完成后调用，方法是将其名称传递给我们的 Html.actionlink （） helper 方法（通过 AjaxOptions "OnSuccess" 事件属性）：</span><span class="sxs-lookup"><span data-stu-id="088bf-158">We can then wire-up this JavaScript function to be called after our AJAX call successfully completes by passing its name to our Ajax.ActionLink() helper method (via the AjaxOptions "OnSuccess" event property):</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

<span data-ttu-id="088bf-159">现在，如果单击了 "RSVP for the 此事件" 链接，并且我们的 AJAX 调用成功完成，则发送回的内容消息将以动画和增长为大：</span><span class="sxs-lookup"><span data-stu-id="088bf-159">And now when the "RSVP for this event" link is clicked and our AJAX call completes successfully, the content message sent back will animate and grow large:</span></span>

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

<span data-ttu-id="088bf-160">除了提供 "OnSuccess" 事件之外，AjaxOptions 对象还公开可处理的 OnBegin、OnFailure 和 OnComplete 事件（以及各种其他属性和有用的选项）。</span><span class="sxs-lookup"><span data-stu-id="088bf-160">In addition to providing an "OnSuccess" event, the AjaxOptions object exposes OnBegin, OnFailure, and OnComplete events that you can handle (along with a variety of other properties and useful options).</span></span>

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a><span data-ttu-id="088bf-161">清除-重构 RSVP 分部视图</span><span class="sxs-lookup"><span data-stu-id="088bf-161">Cleanup - Refactor out a RSVP Partial View</span></span>

<span data-ttu-id="088bf-162">我们的详细信息视图模板即将开始，这会使您难以理解。</span><span class="sxs-lookup"><span data-stu-id="088bf-162">Our details view template is starting to get a little long, which overtime will make it a little harder to understand.</span></span> <span data-ttu-id="088bf-163">为了帮助提高代码的可读性，我们将创建一个分部视图– RSVPStatus，它封装了详细信息页的所有 RSVP 查看代码。</span><span class="sxs-lookup"><span data-stu-id="088bf-163">To help improve the code readability, let's finish up by creating a partial view – RSVPStatus.ascx – that encapsulate all of the RSVP view code for our Details page.</span></span>

<span data-ttu-id="088bf-164">为此，我们可以右键单击 \Views\Dinners 文件夹，然后选择 "添加&gt;视图" 菜单命令。</span><span class="sxs-lookup"><span data-stu-id="088bf-164">We can do this by right-clicking on the \Views\Dinners folder and then choosing the Add-&gt;View menu command.</span></span> <span data-ttu-id="088bf-165">我们将把晚餐对象作为其强类型 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="088bf-165">We'll have it take a Dinner object as its strongly-typed ViewModel.</span></span> <span data-ttu-id="088bf-166">接下来，我们可以将这些 RSVP 内容从 .aspx 视图复制/粘贴到其中。</span><span class="sxs-lookup"><span data-stu-id="088bf-166">We can then copy/paste the RSVP content from our Details.aspx view into it.</span></span>

<span data-ttu-id="088bf-167">完成此操作后，还可以创建另一个分部视图– EditAndDeleteLinks，它封装了编辑和删除链接视图代码。</span><span class="sxs-lookup"><span data-stu-id="088bf-167">Once we've done that, let's also create another partial view – EditAndDeleteLinks.ascx - that encapsulates our Edit and Delete link view code.</span></span> <span data-ttu-id="088bf-168">此外，我们还会将晚餐对象作为其强类型 ViewModel，并将其详细信息 .aspx 视图中的编辑和删除逻辑复制/粘贴到其中。</span><span class="sxs-lookup"><span data-stu-id="088bf-168">We'll also have it take a Dinner object as its strongly-typed ViewModel, and copy/paste the Edit and Delete logic from our Details.aspx view into it.</span></span>

<span data-ttu-id="088bf-169">然后，详细信息视图模板可以在底部包含两个 RenderPartial （）方法调用：</span><span class="sxs-lookup"><span data-stu-id="088bf-169">Our details view template can then just include two Html.RenderPartial() method calls at the bottom:</span></span>

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

<span data-ttu-id="088bf-170">这会使代码更简洁读取和维护。</span><span class="sxs-lookup"><span data-stu-id="088bf-170">This makes the code cleaner to read and maintain.</span></span>

### <a name="next-step"></a><span data-ttu-id="088bf-171">下一步</span><span class="sxs-lookup"><span data-stu-id="088bf-171">Next Step</span></span>

<span data-ttu-id="088bf-172">现在我们来看看如何更进一步地使用 AJAX，并向应用程序中添加交互式映射支持。</span><span class="sxs-lookup"><span data-stu-id="088bf-172">Let's now look at how we can use AJAX even further and add interactive mapping support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="088bf-173">[上一页](secure-applications-using-authentication-and-authorization.md)
> [下一页](use-ajax-to-implement-mapping-scenarios.md)</span><span class="sxs-lookup"><span data-stu-id="088bf-173">[Previous](secure-applications-using-authentication-and-authorization.md)
[Next](use-ajax-to-implement-mapping-scenarios.md)</span></span>
