---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 在 ASP.NET Web API 中发送 HTML 窗体数据： url 编码 ASP.NET
author: MikeWasson
description: 本文介绍如何使用 ASP.NET 4.x 将 url 编码数据发布到 Web API 控制器
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449240"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="bb3b1-103">在 ASP.NET Web API 中发送 HTML 窗体数据：窗体 url 编码数据</span><span class="sxs-lookup"><span data-stu-id="bb3b1-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="bb3b1-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bb3b1-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="bb3b1-105">第1部分：窗体 url 编码数据</span><span class="sxs-lookup"><span data-stu-id="bb3b1-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="bb3b1-106">本文介绍了如何将 url 编码数据发布到 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="bb3b1-107">HTML 窗体概述</span><span class="sxs-lookup"><span data-stu-id="bb3b1-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="bb3b1-108">发送复杂类型</span><span class="sxs-lookup"><span data-stu-id="bb3b1-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="bb3b1-109">通过 AJAX 发送窗体数据</span><span class="sxs-lookup"><span data-stu-id="bb3b1-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="bb3b1-110">发送简单类型</span><span class="sxs-lookup"><span data-stu-id="bb3b1-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="bb3b1-111">[下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="bb3b1-112">HTML 窗体概述</span><span class="sxs-lookup"><span data-stu-id="bb3b1-112">Overview of HTML Forms</span></span>

<span data-ttu-id="bb3b1-113">HTML 窗体使用 GET 或 POST 将数据发送到服务器。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="bb3b1-114">**Form**元素的**METHOD**属性提供 HTTP 方法：</span><span class="sxs-lookup"><span data-stu-id="bb3b1-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="bb3b1-115">默认方法为 GET。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-115">The default method is GET.</span></span> <span data-ttu-id="bb3b1-116">如果窗体使用 GET，则窗体数据在 URI 中将编码为查询字符串。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="bb3b1-117">如果窗体使用 POST，则窗体数据将置于请求正文中。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="bb3b1-118">对于已发布的数据， **enctype**特性指定请求正文的格式：</span><span class="sxs-lookup"><span data-stu-id="bb3b1-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="bb3b1-119">enctype</span><span class="sxs-lookup"><span data-stu-id="bb3b1-119">enctype</span></span> | <span data-ttu-id="bb3b1-120">说明</span><span class="sxs-lookup"><span data-stu-id="bb3b1-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bb3b1-121">application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="bb3b1-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="bb3b1-122">窗体数据被编码为名称/值对，类似于 URI 查询字符串。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="bb3b1-123">这是 POST 的默认格式。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="bb3b1-124">多部分/窗体数据</span><span class="sxs-lookup"><span data-stu-id="bb3b1-124">multipart/form-data</span></span> | <span data-ttu-id="bb3b1-125">表单数据编码为多部分 MIME 消息。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="bb3b1-126">如果要将文件上传到服务器，则使用此格式。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="bb3b1-127">本文的第1部分介绍了 x-www 格式的 url 编码格式。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="bb3b1-128">[第2部分](sending-html-form-data-part-2.md)介绍多部分 MIME。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="bb3b1-129">发送复杂类型</span><span class="sxs-lookup"><span data-stu-id="bb3b1-129">Sending Complex Types</span></span>

<span data-ttu-id="bb3b1-130">通常，您将发送由多个窗体控件中的值组成的复杂类型。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="bb3b1-131">请考虑以下代表状态更新的模型：</span><span class="sxs-lookup"><span data-stu-id="bb3b1-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="bb3b1-132">下面是通过 POST 接受 `Update` 对象的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="bb3b1-133">此控制器使用[基于操作的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)，因此路由模板 &quot;api/{controller}/{action}/{id}&quot;。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="bb3b1-134">客户端会将数据发布到 &quot;/api/updates/complex&quot;。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>

<span data-ttu-id="bb3b1-135">现在，让我们编写一个 HTML 窗体供用户提交状态更新。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="bb3b1-136">请注意，窗体上的**操作**属性是控制器操作的 URI。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="bb3b1-137">下面是在中输入一些值的窗体：</span><span class="sxs-lookup"><span data-stu-id="bb3b1-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="bb3b1-138">当用户单击 "提交" 时，浏览器发送 HTTP 请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bb3b1-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="bb3b1-139">请注意，请求正文包含格式为名称/值对的窗体数据。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="bb3b1-140">Web API 会自动将名称/值对转换为 `Update` 类的实例。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="bb3b1-141">通过 AJAX 发送窗体数据</span><span class="sxs-lookup"><span data-stu-id="bb3b1-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="bb3b1-142">当用户提交窗体时，浏览器从当前页面导航到，并呈现响应消息的正文。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="bb3b1-143">当响应为 HTML 页面时，这是正常的。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="bb3b1-144">但对于 web API，响应正文通常为空或包含结构化数据（如 JSON）。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="bb3b1-145">在这种情况下，使用 AJAX 请求发送窗体数据会更有意义，使页面可以处理响应。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="bb3b1-146">下面的代码演示如何使用 jQuery 发布表单数据。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="bb3b1-147">JQuery **submit**函数将 form 操作替换为新函数。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="bb3b1-148">这将覆盖 "提交" 按钮的默认行为。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="bb3b1-149">**序列化**函数会将窗体数据序列化为名称/值对。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="bb3b1-150">若要将表单数据发送到服务器，请调用 `$.post()`。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="bb3b1-151">请求完成后，`.success()` 或 `.error()` 处理程序将向用户显示相应的消息。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="bb3b1-152">发送简单类型</span><span class="sxs-lookup"><span data-stu-id="bb3b1-152">Sending Simple Types</span></span>

<span data-ttu-id="bb3b1-153">在前面的部分中，我们发送了复杂类型，该类型的 Web API 反序列化为模型类的实例。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="bb3b1-154">您还可以发送简单类型，如字符串。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="bb3b1-155">在发送简单类型之前，请考虑改为将值包装在复杂类型中。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="bb3b1-156">这为你提供了服务器端模型验证的优点，并使你可以在需要时更轻松地扩展模型。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>

<span data-ttu-id="bb3b1-157">发送简单类型的基本步骤是相同的，但有两个细微差别。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="bb3b1-158">首先，在控制器中，必须用**FromBody**属性修饰参数名称。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="bb3b1-159">默认情况下，Web API 尝试从请求 URI 获取简单类型。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="bb3b1-160">**FromBody**特性告诉 Web API 从请求正文中读取值。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="bb3b1-161">Web API 最多读取一次响应正文，因此一个操作的一个参数只能来自请求正文。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="bb3b1-162">如果需要从请求正文中获取多个值，请定义一个复杂类型。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-162">If you need to get multiple values from the request body, define a complex type.</span></span>

<span data-ttu-id="bb3b1-163">其次，客户端需要发送以下格式的值：</span><span class="sxs-lookup"><span data-stu-id="bb3b1-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="bb3b1-164">具体而言，简单类型的名称/值对的名称部分必须为空。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="bb3b1-165">并非所有浏览器都支持 HTML 窗体，但您在脚本中创建了以下格式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="bb3b1-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="bb3b1-166">下面是一个示例窗体：</span><span class="sxs-lookup"><span data-stu-id="bb3b1-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="bb3b1-167">下面是用于提交窗体值的脚本。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="bb3b1-168">与前一个脚本的唯一区别是传递到**post**函数的参数。</span><span class="sxs-lookup"><span data-stu-id="bb3b1-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="bb3b1-169">可以使用相同的方法来发送简单类型的数组：</span><span class="sxs-lookup"><span data-stu-id="bb3b1-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="bb3b1-170">其他资源</span><span class="sxs-lookup"><span data-stu-id="bb3b1-170">Additional Resources</span></span>

[<span data-ttu-id="bb3b1-171">第2部分：文件上传和多部分 MIME</span><span class="sxs-lookup"><span data-stu-id="bb3b1-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)
