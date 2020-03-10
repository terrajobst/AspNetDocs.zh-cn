---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: 使用 Web API 2.2 在 OData v4 中创建单一实例 |Microsoft Docs
author: rick-anderson
description: 本主题演示如何在 Web API 2.2 的 OData 终结点中定义单一实例。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504500"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a><span data-ttu-id="050dd-103">使用 Web API 2.2 在 OData v4 中创建单一实例</span><span class="sxs-lookup"><span data-stu-id="050dd-103">Create a Singleton in OData v4 Using Web API 2.2</span></span>

<span data-ttu-id="050dd-104">作者： Zoe Luo</span><span class="sxs-lookup"><span data-stu-id="050dd-104">by Zoe Luo</span></span>

> <span data-ttu-id="050dd-105">通常，仅当实体封装在实体集内时，才能访问该实体。</span><span class="sxs-lookup"><span data-stu-id="050dd-105">Traditionally, an entity could only be accessed if it were encapsulated inside an entity set.</span></span> <span data-ttu-id="050dd-106">但 OData v4 提供了两个额外的选项，即 Singleton 和包容，两者都支持 WebAPI 2.2。</span><span class="sxs-lookup"><span data-stu-id="050dd-106">But OData v4 provides two additional options, Singleton and Containment, both of which WebAPI 2.2 supports.</span></span>

<span data-ttu-id="050dd-107">本文介绍如何在 Web API 2.2 中定义 OData 终结点中的单一实例。</span><span class="sxs-lookup"><span data-stu-id="050dd-107">This article shows how to define a singleton in an OData endpoint in Web API 2.2.</span></span> <span data-ttu-id="050dd-108">若要了解什么是单一实例以及如何使用它，请参阅[使用单一实例定义特殊实体](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)。</span><span class="sxs-lookup"><span data-stu-id="050dd-108">For information on what a singleton is and how you can benefit from using it, see [Using a singleton to define your special entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx).</span></span> <span data-ttu-id="050dd-109">若要在 Web API 中创建 OData V4 终结点，请参阅[使用 ASP.NET Web API 2.2 创建 odata V4 终结点](create-an-odata-v4-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="050dd-109">To create an OData V4 endpoint in Web API, see [Create an OData v4 Endpoint Using ASP.NET Web API 2.2](create-an-odata-v4-endpoint.md).</span></span> 

<span data-ttu-id="050dd-110">我们将使用以下数据模型在 Web API 项目中创建单一实例：</span><span class="sxs-lookup"><span data-stu-id="050dd-110">We'll create a singleton in your Web API project using the following data model:</span></span>

![数据模型](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

<span data-ttu-id="050dd-112">将根据类型 `Company`定义名为 `Umbrella` 的单一实例，并基于类型 `Employee`定义名为 `Employees` 的实体集。</span><span class="sxs-lookup"><span data-stu-id="050dd-112">A singleton named `Umbrella` will be defined based on type `Company`, and an entity set named `Employees` will be defined based on type `Employee`.</span></span>

<span data-ttu-id="050dd-113">本教程中使用的解决方案可以从[CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)下载。</span><span class="sxs-lookup"><span data-stu-id="050dd-113">The solution used in this tutorial can be downloaded from [CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).</span></span>

## <a name="define-the-data-model"></a><span data-ttu-id="050dd-114">定义数据模型</span><span class="sxs-lookup"><span data-stu-id="050dd-114">Define the data model</span></span>

1. <span data-ttu-id="050dd-115">定义 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="050dd-115">Define the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. <span data-ttu-id="050dd-116">基于 CLR 类型生成 EDM 模型。</span><span class="sxs-lookup"><span data-stu-id="050dd-116">Generate the EDM model based on the CLR types.</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    <span data-ttu-id="050dd-117">在这里，`builder.Singleton<Company>("Umbrella")` 告知模型生成器在 EDM 模型中创建一个名为 `Umbrella` 的单一实例。</span><span class="sxs-lookup"><span data-stu-id="050dd-117">Here, `builder.Singleton<Company>("Umbrella")` tells the model builder to create a singleton named `Umbrella` in the EDM model.</span></span>

    <span data-ttu-id="050dd-118">生成的元数据将如下所示：</span><span class="sxs-lookup"><span data-stu-id="050dd-118">The generated metadata will look like the following:</span></span>

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    <span data-ttu-id="050dd-119">从元数据中，可以看到 `Employees` 实体集中 `Company` 的导航属性绑定到单一实例 `Umbrella`。</span><span class="sxs-lookup"><span data-stu-id="050dd-119">From the metadata we can see that the navigation property `Company` in the `Employees` entity set is bound to the singleton `Umbrella`.</span></span> <span data-ttu-id="050dd-120">绑定由 `ODataConventionModelBuilder`自动完成，因为只有 `Umbrella` 具有 `Company` 类型。</span><span class="sxs-lookup"><span data-stu-id="050dd-120">The binding is done automatically by `ODataConventionModelBuilder`, since only `Umbrella` has the `Company` type.</span></span> <span data-ttu-id="050dd-121">如果模型中存在任何不明确性，可以使用 `HasSingletonBinding` 将导航属性显式绑定到单一实例;`HasSingletonBinding` 与使用 CLR 类型定义中的 `Singleton` 特性具有相同的效果：</span><span class="sxs-lookup"><span data-stu-id="050dd-121">If there is any ambiguity in the model, you can use `HasSingletonBinding` to explicitly bind a navigation property to a singleton; `HasSingletonBinding` has the same effect as using the `Singleton` attribute in the CLR type definition:</span></span>

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a><span data-ttu-id="050dd-122">定义单独控制器</span><span class="sxs-lookup"><span data-stu-id="050dd-122">Define the singleton controller</span></span>

<span data-ttu-id="050dd-123">与 EntitySet 控制器一样，singleton 控制器继承自 `ODataController`，单独控制器名称应为 `[singletonName]Controller`。</span><span class="sxs-lookup"><span data-stu-id="050dd-123">Like the EntitySet controller, the singleton controller inherits from `ODataController`, and the singleton controller name should be `[singletonName]Controller`.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

<span data-ttu-id="050dd-124">为了处理不同种类的请求，需要在控制器中预定义操作。</span><span class="sxs-lookup"><span data-stu-id="050dd-124">In order to handle different kinds of requests, actions are required to be pre-defined in the controller.</span></span> <span data-ttu-id="050dd-125">默认情况下，WebApi 2.2 中启用了**属性路由**。</span><span class="sxs-lookup"><span data-stu-id="050dd-125">**Attribute routing** is enabled by default in WebApi 2.2.</span></span> <span data-ttu-id="050dd-126">例如，若要使用属性路由定义处理 `Company` 的查询 `Revenue` 操作，请使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="050dd-126">For example, to define an action to handle querying `Revenue` from `Company` using attribute routing, use the following:</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

<span data-ttu-id="050dd-127">如果你不愿意为每个操作定义属性，只需在[OData 路由约定](../odata-routing-conventions.md)后定义你的操作。</span><span class="sxs-lookup"><span data-stu-id="050dd-127">If you are not willing to define attributes for each action, just define your actions following [OData Routing Conventions](../odata-routing-conventions.md).</span></span> <span data-ttu-id="050dd-128">由于查询单一实例不需要密钥，因此在单一控制器中定义的操作与 entityset 控制器中定义的操作稍有不同。</span><span class="sxs-lookup"><span data-stu-id="050dd-128">Since a key is not required for querying a singleton, the actions defined in the singleton controller are slightly different from actions defined in the entityset controller.</span></span>

<span data-ttu-id="050dd-129">下面列出了单一实例控制器中的每个操作定义的方法签名，以供参考。</span><span class="sxs-lookup"><span data-stu-id="050dd-129">For reference, method signatures for every action definition in the singleton controller are listed below.</span></span>

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

<span data-ttu-id="050dd-130">基本上，这就是您需要在服务端完成的所有工作。</span><span class="sxs-lookup"><span data-stu-id="050dd-130">Basically, this is all you need to do on the service side.</span></span> <span data-ttu-id="050dd-131">[示例项目](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)包含解决方案的所有代码，以及演示如何使用 Singleton 的 OData 客户端。</span><span class="sxs-lookup"><span data-stu-id="050dd-131">The [sample project](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) contains all of the code for the solution and the OData client that shows how to use the singleton.</span></span> <span data-ttu-id="050dd-132">客户端是按照[创建 OData V4 客户端应用](create-an-odata-v4-client-app.md)中的步骤生成的。</span><span class="sxs-lookup"><span data-stu-id="050dd-132">The client is built by following the steps in [Create an OData v4 Client App](create-an-odata-v4-client-app.md).</span></span>

<span data-ttu-id="050dd-133">.</span><span class="sxs-lookup"><span data-stu-id="050dd-133">.</span></span> 

<span data-ttu-id="050dd-134">*感谢在本文的原始内容中 Leo 的。*</span><span class="sxs-lookup"><span data-stu-id="050dd-134">*Thanks to Leo Hu for the original content of this article.*</span></span>
