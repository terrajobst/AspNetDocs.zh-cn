---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API 中的模型验证-ASP.NET 4。x
author: MikeWasson
description: ASP.NET 4.x 的 ASP.NET Web API 中的模型验证概述。
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448928"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="fba30-103">ASP.NET Web API 中的模型验证</span><span class="sxs-lookup"><span data-stu-id="fba30-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="fba30-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fba30-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fba30-105">本文介绍如何批注模型、使用批注进行数据验证以及处理 web API 中的验证错误。</span><span class="sxs-lookup"><span data-stu-id="fba30-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="fba30-106">当客户端将数据发送到 web API 时，通常需要在进行任何处理之前验证数据。</span><span class="sxs-lookup"><span data-stu-id="fba30-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="fba30-107">数据注释</span><span class="sxs-lookup"><span data-stu-id="fba30-107">Data Annotations</span></span>

<span data-ttu-id="fba30-108">在 ASP.NET Web API 中，你可以使用[system.componentmodel. DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)命名空间中的属性为模型上的属性设置验证规则。</span><span class="sxs-lookup"><span data-stu-id="fba30-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="fba30-109">考虑下列模型：</span><span class="sxs-lookup"><span data-stu-id="fba30-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="fba30-110">如果已在 ASP.NET MVC 中使用了模型验证，则会看到这种情况。</span><span class="sxs-lookup"><span data-stu-id="fba30-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="fba30-111">**必需**的属性指示 `Name` 属性不得为 null。</span><span class="sxs-lookup"><span data-stu-id="fba30-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="fba30-112">**Range**特性指示 `Weight` 必须介于0到999之间。</span><span class="sxs-lookup"><span data-stu-id="fba30-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="fba30-113">假设客户端发送 POST 请求，其 JSON 表示形式如下：</span><span class="sxs-lookup"><span data-stu-id="fba30-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="fba30-114">您可以看到，客户端不包括标记为必需的 `Name` 属性。</span><span class="sxs-lookup"><span data-stu-id="fba30-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="fba30-115">当 Web API 将 JSON 转换为 `Product` 实例时，它会对照验证特性来验证 `Product`。</span><span class="sxs-lookup"><span data-stu-id="fba30-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="fba30-116">在控制器操作中，可以检查模型是否有效：</span><span class="sxs-lookup"><span data-stu-id="fba30-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="fba30-117">模型验证不保证客户端数据是安全的。</span><span class="sxs-lookup"><span data-stu-id="fba30-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="fba30-118">在应用程序的其他层中可能需要进行其他验证。</span><span class="sxs-lookup"><span data-stu-id="fba30-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="fba30-119">（例如，数据层可能强制外键约束。）[使用带有实体框架的 WEB API](../data/using-web-api-with-entity-framework/part-1.md)的教程探讨了其中一些问题。</span><span class="sxs-lookup"><span data-stu-id="fba30-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="fba30-120">**"** 正在进行中"：当客户端省略某些属性时，将发生正在进行的发布。</span><span class="sxs-lookup"><span data-stu-id="fba30-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="fba30-121">例如，假设客户端发送以下内容：</span><span class="sxs-lookup"><span data-stu-id="fba30-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="fba30-122">此时，客户端未指定 `Price` 或 `Weight`的值。</span><span class="sxs-lookup"><span data-stu-id="fba30-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="fba30-123">JSON 格式化程序将默认值0赋给缺少的属性。</span><span class="sxs-lookup"><span data-stu-id="fba30-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="fba30-124">模型状态有效，因为零是这些属性的有效值。</span><span class="sxs-lookup"><span data-stu-id="fba30-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="fba30-125">这是否是一个问题取决于你的方案。</span><span class="sxs-lookup"><span data-stu-id="fba30-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="fba30-126">例如，在更新操作中，你可能希望区分 "零" 和 "未设置"。</span><span class="sxs-lookup"><span data-stu-id="fba30-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="fba30-127">若要强制客户端设置值，请将属性设置为可以为 null，并设置**所需**的属性：</span><span class="sxs-lookup"><span data-stu-id="fba30-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="fba30-128">**"过度发布"** ：客户端还可以发送比预期*更多*的数据。</span><span class="sxs-lookup"><span data-stu-id="fba30-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="fba30-129">例如:</span><span class="sxs-lookup"><span data-stu-id="fba30-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="fba30-130">此处的 JSON 包含 `Product` 模型中不存在的属性（"颜色"）。</span><span class="sxs-lookup"><span data-stu-id="fba30-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="fba30-131">在这种情况下，JSON 格式化程序只会忽略此值。</span><span class="sxs-lookup"><span data-stu-id="fba30-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="fba30-132">（XML 格式化程序执行相同的功能。）如果您的模型具有您打算为只读的属性，则过度发布会导致问题。</span><span class="sxs-lookup"><span data-stu-id="fba30-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="fba30-133">例如:</span><span class="sxs-lookup"><span data-stu-id="fba30-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="fba30-134">您不希望用户更新 `IsAdmin` 属性，并将自己提升为管理员！</span><span class="sxs-lookup"><span data-stu-id="fba30-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="fba30-135">最安全的策略是使用与客户端可以发送的内容完全匹配的模型类：</span><span class="sxs-lookup"><span data-stu-id="fba30-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="fba30-136">Brad Wilson 的博客文章 "[输入验证与 ASP.NET MVC 中的模型验证" 相比](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)，有很好地讨论了下发和过账。</span><span class="sxs-lookup"><span data-stu-id="fba30-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="fba30-137">尽管 post 与 ASP.NET MVC 2 相关，但问题仍与 Web API 相关。</span><span class="sxs-lookup"><span data-stu-id="fba30-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>

## <a name="handling-validation-errors"></a><span data-ttu-id="fba30-138">处理验证错误</span><span class="sxs-lookup"><span data-stu-id="fba30-138">Handling Validation Errors</span></span>

<span data-ttu-id="fba30-139">验证失败时，Web API 不会自动向客户端返回错误。</span><span class="sxs-lookup"><span data-stu-id="fba30-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="fba30-140">它由控制器操作来检查模型状态，并做出相应的响应。</span><span class="sxs-lookup"><span data-stu-id="fba30-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="fba30-141">你还可以创建一个操作筛选器，以在调用控制器操作之前检查模型状态。</span><span class="sxs-lookup"><span data-stu-id="fba30-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="fba30-142">以下代码展示一个示例：</span><span class="sxs-lookup"><span data-stu-id="fba30-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="fba30-143">如果模型验证失败，此筛选器将返回包含验证错误的 HTTP 响应。</span><span class="sxs-lookup"><span data-stu-id="fba30-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="fba30-144">在这种情况下，不会调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="fba30-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="fba30-145">若要将此筛选器应用于所有 Web API 控制器，请在配置过程中将筛选器的实例添加到**HttpConfiguration**集合中：</span><span class="sxs-lookup"><span data-stu-id="fba30-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="fba30-146">另一种方法是将筛选器设置为单个控制器或控制器操作上的属性：</span><span class="sxs-lookup"><span data-stu-id="fba30-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
