---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: 模型验证在 ASP.NET Web API-ASP.NET 4.x
author: MikeWasson
description: 概述 ASP.NET Web API 中的模型验证的 ASP.NET 4.x。
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: d4e792f8cc2f79c2ab82c5a74fd50f49475fac4f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404567"
---
# <a name="model-validation-in-aspnet-web-api"></a><span data-ttu-id="fc515-103">ASP.NET Web API 中的模型验证</span><span class="sxs-lookup"><span data-stu-id="fc515-103">Model Validation in ASP.NET Web API</span></span>

<span data-ttu-id="fc515-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="fc515-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="fc515-105">本文介绍如何对模型进行批注、 使用批注以进行数据验证和处理你的 web API 中的验证错误。</span><span class="sxs-lookup"><span data-stu-id="fc515-105">This article shows how to annotate your models, use the annotations for data validation, and handle validation errors in your web API.</span></span> <span data-ttu-id="fc515-106">当客户端将数据发送到 web API 时，通常要执行任何处理之前验证数据。</span><span class="sxs-lookup"><span data-stu-id="fc515-106">When a client sends data to your web API, often you want to validate the data before doing any processing.</span></span> 

## <a name="data-annotations"></a><span data-ttu-id="fc515-107">数据注释</span><span class="sxs-lookup"><span data-stu-id="fc515-107">Data Annotations</span></span>

<span data-ttu-id="fc515-108">在 ASP.NET Web API 中，可以使用中的属性[System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)命名空间来对模型设置属性的验证规则。</span><span class="sxs-lookup"><span data-stu-id="fc515-108">In ASP.NET Web API, you can use attributes from the [System.ComponentModel.DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) namespace to set validation rules for properties on your model.</span></span> <span data-ttu-id="fc515-109">考虑下列模型：</span><span class="sxs-lookup"><span data-stu-id="fc515-109">Consider the following model:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="fc515-110">如果已在 ASP.NET MVC 中使用模型验证，这应该很熟悉。</span><span class="sxs-lookup"><span data-stu-id="fc515-110">If you have used model validation in ASP.NET MVC, this should look familiar.</span></span> <span data-ttu-id="fc515-111">**所需**属性指出`Name`属性不能为 null。</span><span class="sxs-lookup"><span data-stu-id="fc515-111">The **Required** attribute says that the `Name` property must not be null.</span></span> <span data-ttu-id="fc515-112">**范围**属性指出`Weight`必须是介于 0 和 999 之间。</span><span class="sxs-lookup"><span data-stu-id="fc515-112">The **Range** attribute says that `Weight` must be between zero and 999.</span></span>

<span data-ttu-id="fc515-113">假设客户端发送 POST 请求，其中以下 JSON 表示形式：</span><span class="sxs-lookup"><span data-stu-id="fc515-113">Suppose that a client sends a POST request with the following JSON representation:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

<span data-ttu-id="fc515-114">您可以看到客户端未包括`Name`属性，它被标记为必需。</span><span class="sxs-lookup"><span data-stu-id="fc515-114">You can see that the client did not include the `Name` property, which is marked as required.</span></span> <span data-ttu-id="fc515-115">当 Web API 将转换为 JSON`Product`实例，它会验证`Product`针对验证特性。</span><span class="sxs-lookup"><span data-stu-id="fc515-115">When Web API converts the JSON into a `Product` instance, it validates the `Product` against the validation attributes.</span></span> <span data-ttu-id="fc515-116">在你的控制器操作，可以检查模型是否有效：</span><span class="sxs-lookup"><span data-stu-id="fc515-116">In your controller action, you can check whether the model is valid:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="fc515-117">模型验证不保证客户端数据的安全。</span><span class="sxs-lookup"><span data-stu-id="fc515-117">Model validation does not guarantee that client data is safe.</span></span> <span data-ttu-id="fc515-118">其他验证可能需要在应用程序的其他层中。</span><span class="sxs-lookup"><span data-stu-id="fc515-118">Additional validation might be needed in other layers of the application.</span></span> <span data-ttu-id="fc515-119">（例如，数据层可能会强制实施外键约束。）本教程[使用实体框架使用 Web API](../data/using-web-api-with-entity-framework/part-1.md)探讨了其中一些问题。</span><span class="sxs-lookup"><span data-stu-id="fc515-119">(For example, the data layer might enforce foreign key constraints.) The tutorial [Using Web API with Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) explores some of these issues.</span></span>

<span data-ttu-id="fc515-120">**"未得到充分发布"**:客户端将省略某些属性会发生未得到充分的发布。</span><span class="sxs-lookup"><span data-stu-id="fc515-120">**"Under-Posting"**: Under-posting happens when the client leaves out some properties.</span></span> <span data-ttu-id="fc515-121">例如，假设客户端发送以下：</span><span class="sxs-lookup"><span data-stu-id="fc515-121">For example, suppose the client sends the following:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

<span data-ttu-id="fc515-122">在这里，客户端未指定值`Price`或`Weight`。</span><span class="sxs-lookup"><span data-stu-id="fc515-122">Here, the client did not specify values for `Price` or `Weight`.</span></span> <span data-ttu-id="fc515-123">JSON 格式化程序将分配默认值为 0 到缺少的属性。</span><span class="sxs-lookup"><span data-stu-id="fc515-123">The JSON formatter assigns a default value of zero to the missing properties.</span></span>

![](model-validation-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="fc515-124">模型状态无效，因为零是这些属性的有效值。</span><span class="sxs-lookup"><span data-stu-id="fc515-124">The model state is valid, because zero is a valid value for these properties.</span></span> <span data-ttu-id="fc515-125">这是否是一个问题取决于你的方案。</span><span class="sxs-lookup"><span data-stu-id="fc515-125">Whether this is a problem depends on your scenario.</span></span> <span data-ttu-id="fc515-126">例如，在更新操作中，可能想要区分"零"和"未设置。"</span><span class="sxs-lookup"><span data-stu-id="fc515-126">For example, in an update operation, you might want to distinguish between "zero" and "not set."</span></span> <span data-ttu-id="fc515-127">若要强制客户端可以设置一个值，使该属性可以为 null，并且已设置**所需**属性：</span><span class="sxs-lookup"><span data-stu-id="fc515-127">To force clients to set a value, make the property nullable and set the **Required** attribute:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

<span data-ttu-id="fc515-128">**"过度发布"**:客户端还可以发送*详细*比预期的数据。</span><span class="sxs-lookup"><span data-stu-id="fc515-128">**"Over-Posting"**: A client can also send *more* data than you expected.</span></span> <span data-ttu-id="fc515-129">例如：</span><span class="sxs-lookup"><span data-stu-id="fc515-129">For example:</span></span>

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

<span data-ttu-id="fc515-130">在这里，JSON 包括中不存在的属性 ("Color")`Product`模型。</span><span class="sxs-lookup"><span data-stu-id="fc515-130">Here, the JSON includes a property ("Color") that does not exist in the `Product` model.</span></span> <span data-ttu-id="fc515-131">在这种情况下，JSON 格式化程序只需将忽略此值。</span><span class="sxs-lookup"><span data-stu-id="fc515-131">In this case, the JSON formatter simply ignores this value.</span></span> <span data-ttu-id="fc515-132">（XML 格式化程序执行相同操作。）如果您的模型具有你想要为只读属性，过度提交会导致问题。</span><span class="sxs-lookup"><span data-stu-id="fc515-132">(The XML formatter does the same.) Over-posting causes problems if your model has properties that you intended to be read-only.</span></span> <span data-ttu-id="fc515-133">例如：</span><span class="sxs-lookup"><span data-stu-id="fc515-133">For example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="fc515-134">你不希望用户更新`IsAdmin`属性并将自己提升为管理员 ！</span><span class="sxs-lookup"><span data-stu-id="fc515-134">You don't want users to update the `IsAdmin` property and elevate themselves to administrators!</span></span> <span data-ttu-id="fc515-135">最安全的策略是使用与客户端可以发送完全匹配的模型类：</span><span class="sxs-lookup"><span data-stu-id="fc515-135">The safest strategy is to use a model class that exactly matches what the client is allowed to send:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> <span data-ttu-id="fc515-136">Brad Wilson 的博客文章"[输入验证 vs。ASP.NET MVC 中的模型验证](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)"具有未得到充分的发布和过度提交了适当探讨。</span><span class="sxs-lookup"><span data-stu-id="fc515-136">Brad Wilson's blog post "[Input Validation vs. Model Validation in ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" has a good discussion of under-posting and over-posting.</span></span> <span data-ttu-id="fc515-137">虽然文章是有关 ASP.NET MVC 2，但是是仍然与 Web API 相关的问题。</span><span class="sxs-lookup"><span data-stu-id="fc515-137">Although the post is about ASP.NET MVC 2, the issues are still relevant to Web API.</span></span>


## <a name="handling-validation-errors"></a><span data-ttu-id="fc515-138">处理验证错误</span><span class="sxs-lookup"><span data-stu-id="fc515-138">Handling Validation Errors</span></span>

<span data-ttu-id="fc515-139">Web API 不会自动返回错误到客户端验证失败时。</span><span class="sxs-lookup"><span data-stu-id="fc515-139">Web API does not automatically return an error to the client when validation fails.</span></span> <span data-ttu-id="fc515-140">负责检查模型状态并做出相应的响应的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="fc515-140">It is up to the controller action to check the model state and respond appropriately.</span></span>

<span data-ttu-id="fc515-141">此外可以创建一个操作筛选器来调用控制器操作之前检查模型状态。</span><span class="sxs-lookup"><span data-stu-id="fc515-141">You can also create an action filter to check the model state before the controller action is invoked.</span></span> <span data-ttu-id="fc515-142">下面的代码演示一个示例：</span><span class="sxs-lookup"><span data-stu-id="fc515-142">The following code shows an example:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="fc515-143">如果模型验证失败，此筛选器将返回 HTTP 响应，其中包含验证错误。</span><span class="sxs-lookup"><span data-stu-id="fc515-143">If model validation fails, this filter returns an HTTP response that contains the validation errors.</span></span> <span data-ttu-id="fc515-144">在这种情况下，不会调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="fc515-144">In that case, the controller action is not invoked.</span></span>

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

<span data-ttu-id="fc515-145">若要将此筛选器应用于所有的 Web API 控制器，将添加到筛选器的实例**HttpConfiguration.Filters**在配置期间的集合：</span><span class="sxs-lookup"><span data-stu-id="fc515-145">To apply this filter to all Web API controllers, add an instance of the filter to the **HttpConfiguration.Filters** collection during configuration:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="fc515-146">另一个选项是设置筛选器作为特性上各个控制器或控制器操作：</span><span class="sxs-lookup"><span data-stu-id="fc515-146">Another option is to set the filter as an attribute on individual controllers or controller actions:</span></span>

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
