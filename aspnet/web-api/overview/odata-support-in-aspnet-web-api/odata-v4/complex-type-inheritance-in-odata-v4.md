---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: 与 ASP.NET Web API 的 OData v4 中的复杂类型继承 |Microsoft Docs
author: microsoft
description: 根据 OData v4 规范，复杂类型可以继承自其他复杂类型。 （复杂类型是没有键的结构化类型。）Web API 。
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448130"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a><span data-ttu-id="4968b-104">OData v4 中的复杂类型继承与 ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="4968b-104">Complex Type Inheritance in OData v4 with ASP.NET Web API</span></span>

<span data-ttu-id="4968b-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4968b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4968b-106">根据 OData v4[规范](http://www.odata.org/documentation/odata-version-4-0/)，复杂类型可以继承自其他复杂类型。</span><span class="sxs-lookup"><span data-stu-id="4968b-106">According to the OData v4 [specification](http://www.odata.org/documentation/odata-version-4-0/), a complex type can inherit from another complex type.</span></span> <span data-ttu-id="4968b-107">（*复杂*类型是没有键的结构化类型。）Web API OData 5.3 支持复杂的类型继承。</span><span class="sxs-lookup"><span data-stu-id="4968b-107">(A *complex* type is a structured type without a key.) Web API OData 5.3 supports complex type inheritance.</span></span>
> 
> <span data-ttu-id="4968b-108">本主题演示如何使用复杂的继承类型生成实体数据模型（EDM）。</span><span class="sxs-lookup"><span data-stu-id="4968b-108">This topic shows how to build an entity data model (EDM) with complex inheritance types.</span></span> <span data-ttu-id="4968b-109">有关完整的源代码，请参阅[OData 复杂类型继承示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。</span><span class="sxs-lookup"><span data-stu-id="4968b-109">For the complete source code, see [OData Complex Type Inheritance Sample](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4968b-110">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="4968b-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="4968b-111">Web API OData 5。3</span><span class="sxs-lookup"><span data-stu-id="4968b-111">Web API OData 5.3</span></span>
> - <span data-ttu-id="4968b-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="4968b-112">OData v4</span></span>

## <a name="model-hierarchy"></a><span data-ttu-id="4968b-113">模型层次结构</span><span class="sxs-lookup"><span data-stu-id="4968b-113">Model Hierarchy</span></span>

<span data-ttu-id="4968b-114">为了说明复杂类型继承，我们将使用下面的类层次结构。</span><span class="sxs-lookup"><span data-stu-id="4968b-114">To illustrate complex type inheritance, we'll use the following class hierarchy.</span></span>

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

<span data-ttu-id="4968b-115">`Shape` 是抽象复杂类型。</span><span class="sxs-lookup"><span data-stu-id="4968b-115">`Shape` is an abstract complex type.</span></span> <span data-ttu-id="4968b-116">`Rectangle`、`Triangle`和 `Circle` 是派生自 `Shape`的复杂类型，并且 `RoundRectangle` 派生自 `Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="4968b-116">`Rectangle`, `Triangle`, and `Circle` are complex types derived from `Shape`, and `RoundRectangle` derives from `Rectangle`.</span></span> <span data-ttu-id="4968b-117">`Window` 是实体类型并且包含 `Shape` 实例。</span><span class="sxs-lookup"><span data-stu-id="4968b-117">`Window` is an entity type and contains a `Shape` instance.</span></span>

<span data-ttu-id="4968b-118">下面是用于定义这些类型的 CLR 类。</span><span class="sxs-lookup"><span data-stu-id="4968b-118">Here are the CLR classes that define these types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a><span data-ttu-id="4968b-119">生成 EDM 模型</span><span class="sxs-lookup"><span data-stu-id="4968b-119">Build the EDM Model</span></span>

<span data-ttu-id="4968b-120">若要创建 EDM，可以使用**ODataConventionModelBuilder**，它可从 CLR 类型推断继承关系。</span><span class="sxs-lookup"><span data-stu-id="4968b-120">To create the EDM, you can use **ODataConventionModelBuilder**, which infers the inheritance relationships from the CLR types.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

<span data-ttu-id="4968b-121">还可以使用**ODataModelBuilder**显式生成 EDM。</span><span class="sxs-lookup"><span data-stu-id="4968b-121">You can also build the EDM explicitly, using **ODataModelBuilder**.</span></span> <span data-ttu-id="4968b-122">这将需要更多代码，但可以更好地控制 EDM。</span><span class="sxs-lookup"><span data-stu-id="4968b-122">This takes more code, but gives you more control over the EDM.</span></span>

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

<span data-ttu-id="4968b-123">这两个示例创建相同的 EDM 架构。</span><span class="sxs-lookup"><span data-stu-id="4968b-123">These two examples create the same EDM schema.</span></span>

## <a name="metadata-document"></a><span data-ttu-id="4968b-124">元数据文档</span><span class="sxs-lookup"><span data-stu-id="4968b-124">Metadata Document</span></span>

<span data-ttu-id="4968b-125">下面是 OData 元数据文档，显示复杂的类型继承。</span><span class="sxs-lookup"><span data-stu-id="4968b-125">Here is the OData metadata document, showing complex type inheritance.</span></span>

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

<span data-ttu-id="4968b-126">在元数据文档中，可以看到：</span><span class="sxs-lookup"><span data-stu-id="4968b-126">From the metadata document, you can see that:</span></span>

- <span data-ttu-id="4968b-127">`Shape` 复杂类型为抽象类型。</span><span class="sxs-lookup"><span data-stu-id="4968b-127">The `Shape` complex type is abstract.</span></span>
- <span data-ttu-id="4968b-128">`Rectangle`、`Triangle`和 `Circle` 复杂类型具有基类型 `Shape`。</span><span class="sxs-lookup"><span data-stu-id="4968b-128">The `Rectangle`, `Triangle`, and `Circle` complex type have the base type `Shape`.</span></span>
- <span data-ttu-id="4968b-129">`RoundRectangle` 类型的基类型为 `Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="4968b-129">The `RoundRectangle` type has the base type `Rectangle`.</span></span>

## <a name="casting-complex-types"></a><span data-ttu-id="4968b-130">转换复杂类型</span><span class="sxs-lookup"><span data-stu-id="4968b-130">Casting Complex Types</span></span>

<span data-ttu-id="4968b-131">现在支持在复杂类型上强制转换。</span><span class="sxs-lookup"><span data-stu-id="4968b-131">Casting on complex types is now supported.</span></span> <span data-ttu-id="4968b-132">例如，下面的查询将 `Shape` 转换为 `Rectangle`。</span><span class="sxs-lookup"><span data-stu-id="4968b-132">For example, the following query casts a `Shape` to a `Rectangle`.</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

<span data-ttu-id="4968b-133">下面是响应有效负载：</span><span class="sxs-lookup"><span data-stu-id="4968b-133">Here's the response payload:</span></span>

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
