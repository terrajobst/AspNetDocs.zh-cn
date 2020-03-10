---
uid: web-api/overview/error-handling/exception-handling
title: ASP.NET Web API-ASP.NET 4.x 中的异常处理
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504698"
---
# <a name="exception-handling-in-aspnet-web-api"></a><span data-ttu-id="bf910-102">ASP.NET Web API 中的异常处理</span><span class="sxs-lookup"><span data-stu-id="bf910-102">Exception Handling in ASP.NET Web API</span></span>

<span data-ttu-id="bf910-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bf910-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bf910-104">本文介绍了 ASP.NET Web API 中的错误和异常处理。</span><span class="sxs-lookup"><span data-stu-id="bf910-104">This article describes error and exception handling in ASP.NET Web API.</span></span>

- [<span data-ttu-id="bf910-105">带有 httpresponseexception</span><span class="sxs-lookup"><span data-stu-id="bf910-105">HttpResponseException</span></span>](#httpresponserexception)
- [<span data-ttu-id="bf910-106">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="bf910-106">Exception Filters</span></span>](#exception_filters)
- [<span data-ttu-id="bf910-107">注册异常筛选器</span><span class="sxs-lookup"><span data-stu-id="bf910-107">Registering Exception Filters</span></span>](#registering_exception_filters)
- [<span data-ttu-id="bf910-108">HttpError</span><span class="sxs-lookup"><span data-stu-id="bf910-108">HttpError</span></span>](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a><span data-ttu-id="bf910-109">HttpResponseException</span><span class="sxs-lookup"><span data-stu-id="bf910-109">HttpResponseException</span></span>

<span data-ttu-id="bf910-110">如果 Web API 控制器引发未捕获的异常，会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="bf910-110">What happens if a Web API controller throws an uncaught exception?</span></span> <span data-ttu-id="bf910-111">默认情况下，大多数异常都转换为 HTTP 响应，状态代码为500，内部服务器错误。</span><span class="sxs-lookup"><span data-stu-id="bf910-111">By default, most exceptions are translated into an HTTP response with status code 500, Internal Server Error.</span></span>

<span data-ttu-id="bf910-112">**带有 httpresponseexception**类型是一种特殊情况。</span><span class="sxs-lookup"><span data-stu-id="bf910-112">The **HttpResponseException** type is a special case.</span></span> <span data-ttu-id="bf910-113">此异常返回在异常构造函数中指定的任何 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="bf910-113">This exception returns any HTTP status code that you specify in the exception constructor.</span></span> <span data-ttu-id="bf910-114">例如，如果*id*参数无效，则以下方法返回404，但找不到。</span><span class="sxs-lookup"><span data-stu-id="bf910-114">For example, the following method returns 404, Not Found, if the *id* parameter is not valid.</span></span>

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

<span data-ttu-id="bf910-115">为了更好地控制响应，你还可以构造整个响应消息，并将其包含在**带有 httpresponseexception 中：**</span><span class="sxs-lookup"><span data-stu-id="bf910-115">For more control over the response, you can also construct the entire response message and include it with the **HttpResponseException:**</span></span> 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a><span data-ttu-id="bf910-116">异常筛选器</span><span class="sxs-lookup"><span data-stu-id="bf910-116">Exception Filters</span></span>

<span data-ttu-id="bf910-117">可以通过编写*异常筛选器*来自定义 Web API 处理异常的方式。</span><span class="sxs-lookup"><span data-stu-id="bf910-117">You can customize how Web API handles exceptions by writing an *exception filter*.</span></span> <span data-ttu-id="bf910-118">当控制器方法引发*不*是**带有 httpresponseexception**异常的任何未经处理的异常时，将执行异常筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf910-118">An exception filter is executed when a controller method throws any unhandled exception that is *not* an **HttpResponseException** exception.</span></span> <span data-ttu-id="bf910-119">**带有 httpresponseexception**类型是一种特殊情况，因为它专用于返回 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="bf910-119">The **HttpResponseException** type is a special case, because it is designed specifically for returning an HTTP response.</span></span>

<span data-ttu-id="bf910-120">异常筛选器实现了**IExceptionFilter**接口。</span><span class="sxs-lookup"><span data-stu-id="bf910-120">Exception filters implement the **System.Web.Http.Filters.IExceptionFilter** interface.</span></span> <span data-ttu-id="bf910-121">编写异常筛选器的最简单方法是从**ExceptionFilterAttribute**类派生，并重写**OnException**方法。</span><span class="sxs-lookup"><span data-stu-id="bf910-121">The simplest way to write an exception filter is to derive from the **System.Web.Http.Filters.ExceptionFilterAttribute** class and override the **OnException** method.</span></span>

> [!NOTE]
> <span data-ttu-id="bf910-122">ASP.NET Web API 中的异常筛选器类似于 ASP.NET MVC 中的筛选器。</span><span class="sxs-lookup"><span data-stu-id="bf910-122">Exception filters in ASP.NET Web API are similar to those in ASP.NET MVC.</span></span> <span data-ttu-id="bf910-123">但是，它们分别在单独的命名空间和函数中声明。</span><span class="sxs-lookup"><span data-stu-id="bf910-123">However, they are declared in a separate namespace and function separately.</span></span> <span data-ttu-id="bf910-124">特别是，MVC 中使用的**HandleErrorAttribute**类不处理 Web API 控制器引发的异常。</span><span class="sxs-lookup"><span data-stu-id="bf910-124">In particular, the **HandleErrorAttribute** class used in MVC does not handle exceptions thrown by Web API controllers.</span></span>

<span data-ttu-id="bf910-125">下面的筛选器将**NotImplementedException**异常转换为 HTTP 状态代码501，而未实现：</span><span class="sxs-lookup"><span data-stu-id="bf910-125">Here is a filter that converts **NotImplementedException** exceptions into HTTP status code 501, Not Implemented:</span></span>

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

<span data-ttu-id="bf910-126">**HttpActionExecutedContext**对象的**Response**属性包含将发送到客户端的 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="bf910-126">The **Response** property of the **HttpActionExecutedContext** object contains the HTTP response message that will be sent to the client.</span></span>

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a><span data-ttu-id="bf910-127">注册异常筛选器</span><span class="sxs-lookup"><span data-stu-id="bf910-127">Registering Exception Filters</span></span>

<span data-ttu-id="bf910-128">可通过多种方法注册 Web API 异常筛选器：</span><span class="sxs-lookup"><span data-stu-id="bf910-128">There are several ways to register a Web API exception filter:</span></span>

- <span data-ttu-id="bf910-129">按操作</span><span class="sxs-lookup"><span data-stu-id="bf910-129">By action</span></span>
- <span data-ttu-id="bf910-130">按控制器</span><span class="sxs-lookup"><span data-stu-id="bf910-130">By controller</span></span>
- <span data-ttu-id="bf910-131">全局</span><span class="sxs-lookup"><span data-stu-id="bf910-131">Globally</span></span>

<span data-ttu-id="bf910-132">要将筛选器应用到特定的操作，请将筛选器作为特性添加到该操作：</span><span class="sxs-lookup"><span data-stu-id="bf910-132">To apply the filter to a specific action, add the filter as an attribute to the action:</span></span>

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

<span data-ttu-id="bf910-133">若要将筛选器应用于控制器上的所有操作，请将筛选器作为属性添加到控制器类：</span><span class="sxs-lookup"><span data-stu-id="bf910-133">To apply the filter to all of the actions on a controller, add the filter as an attribute to the controller class:</span></span>

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

<span data-ttu-id="bf910-134">若要将筛选器全局应用到所有 Web API 控制器，请将筛选器的实例添加到**GlobalConfiguration**集合。</span><span class="sxs-lookup"><span data-stu-id="bf910-134">To apply the filter globally to all Web API controllers, add an instance of the filter to the **GlobalConfiguration.Configuration.Filters** collection.</span></span> <span data-ttu-id="bf910-135">此集合中的异常筛选器将应用到任何 Web API 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="bf910-135">Exception filters in this collection apply to any Web API controller action.</span></span>

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

<span data-ttu-id="bf910-136">如果使用 "ASP.NET MVC 4 Web 应用程序" 项目模板来创建项目，请将 Web API 配置代码置于 `WebApiConfig` 类中，该代码位于应用\_启动文件夹中：</span><span class="sxs-lookup"><span data-stu-id="bf910-136">If you use the "ASP.NET MVC 4 Web Application" project template to create your project, put your Web API configuration code inside the `WebApiConfig` class, which is located in the App\_Start folder:</span></span>

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a><span data-ttu-id="bf910-137">HttpError</span><span class="sxs-lookup"><span data-stu-id="bf910-137">HttpError</span></span>

<span data-ttu-id="bf910-138">**HttpError**对象提供了一种一致的方式来在响应正文中返回错误信息。</span><span class="sxs-lookup"><span data-stu-id="bf910-138">The **HttpError** object provides a consistent way to return error information in the response body.</span></span> <span data-ttu-id="bf910-139">下面的示例演示如何在响应正文中返回包含**HttpError**的 HTTP 状态代码404（未找到）。</span><span class="sxs-lookup"><span data-stu-id="bf910-139">The following example shows how to return HTTP status code 404 (Not Found) with an **HttpError** in the response body.</span></span>

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

<span data-ttu-id="bf910-140">**CreateErrorResponse**是在**HttpRequestMessageExtensions**类中定义的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="bf910-140">**CreateErrorResponse** is an extension method defined in the **System.Net.Http.HttpRequestMessageExtensions** class.</span></span> <span data-ttu-id="bf910-141">在内部， **CreateErrorResponse**创建一个**HttpError**实例，然后创建一个包含**HttpError**的**HttpResponseMessage** 。</span><span class="sxs-lookup"><span data-stu-id="bf910-141">Internally, **CreateErrorResponse** creates an **HttpError** instance and then creates an **HttpResponseMessage** that contains the **HttpError**.</span></span>

<span data-ttu-id="bf910-142">在此示例中，如果方法成功，它将在 HTTP 响应中返回产品。</span><span class="sxs-lookup"><span data-stu-id="bf910-142">In this example, if the method is successful, it returns the product in the HTTP response.</span></span> <span data-ttu-id="bf910-143">但如果找不到请求的产品，HTTP 响应会在请求正文中包含**HttpError** 。</span><span class="sxs-lookup"><span data-stu-id="bf910-143">But if the requested product is not found, the HTTP response contains an **HttpError** in the request body.</span></span> <span data-ttu-id="bf910-144">响应可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="bf910-144">The response might look like the following:</span></span>

[!code-console[Main](exception-handling/samples/sample9.cmd)]

<span data-ttu-id="bf910-145">请注意，在此示例中， **HttpError**已序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="bf910-145">Notice that the **HttpError** was serialized to JSON in this example.</span></span> <span data-ttu-id="bf910-146">使用**HttpError**的一个优点是，它与任何其他强类型模型进行相同的[内容协商](../formats-and-model-binding/content-negotiation.md)和序列化过程。</span><span class="sxs-lookup"><span data-stu-id="bf910-146">One advantage of using **HttpError** is that it goes through the same [content-negotiation](../formats-and-model-binding/content-negotiation.md) and serialization process as any other strongly-typed model.</span></span>

### <a name="httperror-and-model-validation"></a><span data-ttu-id="bf910-147">HttpError 和模型验证</span><span class="sxs-lookup"><span data-stu-id="bf910-147">HttpError and Model Validation</span></span>

<span data-ttu-id="bf910-148">对于模型验证，可以将模型状态传递到**CreateErrorResponse**，以便在响应中包括验证错误：</span><span class="sxs-lookup"><span data-stu-id="bf910-148">For model validation, you can pass the model state to **CreateErrorResponse**, to include the validation errors in the response:</span></span>

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

<span data-ttu-id="bf910-149">此示例可能返回以下响应：</span><span class="sxs-lookup"><span data-stu-id="bf910-149">This example might return the following response:</span></span>

[!code-console[Main](exception-handling/samples/sample11.cmd)]

<span data-ttu-id="bf910-150">有关模型验证的详细信息，请参阅[中的模型验证 ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="bf910-150">For more information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

### <a name="using-httperror-with-httpresponseexception"></a><span data-ttu-id="bf910-151">将 HttpError 与带有 httpresponseexception 配合使用</span><span class="sxs-lookup"><span data-stu-id="bf910-151">Using HttpError with HttpResponseException</span></span>

<span data-ttu-id="bf910-152">前面的示例从控制器操作返回**HttpResponseMessage**消息，但也可以使用**带有 httpresponseexception**返回**HttpError**。</span><span class="sxs-lookup"><span data-stu-id="bf910-152">The previous examples return an **HttpResponseMessage** message from the controller action, but you can also use **HttpResponseException** to return an **HttpError**.</span></span> <span data-ttu-id="bf910-153">这使您可以在正常的成功情况下返回强类型化的模型，同时在出现错误时仍会返回**HttpError** ：</span><span class="sxs-lookup"><span data-stu-id="bf910-153">This lets you return a strongly-typed model in the normal success case, while still returning **HttpError** if there is an error:</span></span>

[!code-csharp[Main](exception-handling/samples/sample12.cs)]
