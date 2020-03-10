---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: 第2部分：创建域模型 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504272"
---
# <a name="part-2-creating-the-domain-models"></a><span data-ttu-id="6fb50-102">第2部分：创建域模型</span><span class="sxs-lookup"><span data-stu-id="6fb50-102">Part 2: Creating the Domain Models</span></span>

<span data-ttu-id="6fb50-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6fb50-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="6fb50-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="6fb50-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="6fb50-105">添加模型</span><span class="sxs-lookup"><span data-stu-id="6fb50-105">Add Models</span></span>

<span data-ttu-id="6fb50-106">有三种方法可用于实体框架：</span><span class="sxs-lookup"><span data-stu-id="6fb50-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="6fb50-107">数据库优先：从数据库开始，实体框架生成代码。</span><span class="sxs-lookup"><span data-stu-id="6fb50-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="6fb50-108">模型优先：从视觉对象模型开始，实体框架生成数据库和代码。</span><span class="sxs-lookup"><span data-stu-id="6fb50-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="6fb50-109">代码优先：从代码开始，实体框架生成数据库。</span><span class="sxs-lookup"><span data-stu-id="6fb50-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="6fb50-110">我们使用代码优先方法，我们首先将域对象定义为 Poco （普通的 CLR 对象）。</span><span class="sxs-lookup"><span data-stu-id="6fb50-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="6fb50-111">在代码优先方法中，域对象不需要任何额外的代码就可以支持数据库层，如事务或持久性。</span><span class="sxs-lookup"><span data-stu-id="6fb50-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="6fb50-112">（具体而言，它们不需要从[EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx)类继承。）你仍可以使用数据批注来控制实体框架创建数据库架构的方式。</span><span class="sxs-lookup"><span data-stu-id="6fb50-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="6fb50-113">由于 Poco 不携带任何其他用于描述[数据库状态](https://msdn.microsoft.com/library/system.data.entitystate.aspx)的属性，因此可以轻松地将其序列化为 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="6fb50-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="6fb50-114">但是，这并不意味着您应该始终向客户端公开您的实体框架模型，因为我们将在本教程的后面部分介绍。</span><span class="sxs-lookup"><span data-stu-id="6fb50-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="6fb50-115">我们将创建以下 Poco：</span><span class="sxs-lookup"><span data-stu-id="6fb50-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="6fb50-116">产品</span><span class="sxs-lookup"><span data-stu-id="6fb50-116">Product</span></span>
- <span data-ttu-id="6fb50-117">顺序</span><span class="sxs-lookup"><span data-stu-id="6fb50-117">Order</span></span>
- <span data-ttu-id="6fb50-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="6fb50-118">OrderDetail</span></span>

<span data-ttu-id="6fb50-119">若要创建每个类，请在解决方案资源管理器中右键单击 "模型" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="6fb50-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="6fb50-120">从上下文菜单中，选择 "**添加**"，然后选择 "**类"。**</span><span class="sxs-lookup"><span data-stu-id="6fb50-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="6fb50-121">添加具有以下实现的 `Product` 类：</span><span class="sxs-lookup"><span data-stu-id="6fb50-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="6fb50-122">按照约定，实体框架使用 `Id` 属性作为主键，并将其映射到数据库表中的标识列。</span><span class="sxs-lookup"><span data-stu-id="6fb50-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="6fb50-123">创建新的 `Product` 实例时，不会为 `Id`设置值，因为数据库会生成值。</span><span class="sxs-lookup"><span data-stu-id="6fb50-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="6fb50-124">**ScaffoldColumn**特性指示 ASP.NET MVC 在生成编辑器窗体时跳过 `Id` 属性。</span><span class="sxs-lookup"><span data-stu-id="6fb50-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="6fb50-125">**必需**的属性用于验证模型。</span><span class="sxs-lookup"><span data-stu-id="6fb50-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="6fb50-126">它指定 `Name` 属性必须为非空字符串。</span><span class="sxs-lookup"><span data-stu-id="6fb50-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="6fb50-127">添加 `Order` 类：</span><span class="sxs-lookup"><span data-stu-id="6fb50-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="6fb50-128">添加 `OrderDetail` 类：</span><span class="sxs-lookup"><span data-stu-id="6fb50-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="6fb50-129">外键关系</span><span class="sxs-lookup"><span data-stu-id="6fb50-129">Foreign Key Relations</span></span>

<span data-ttu-id="6fb50-130">订单包含许多订单详细信息，每个订单详细信息都指单个产品。</span><span class="sxs-lookup"><span data-stu-id="6fb50-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="6fb50-131">为了表示这些关系，`OrderDetail` 类定义了名为 `OrderId` 和 `ProductId`属性。</span><span class="sxs-lookup"><span data-stu-id="6fb50-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="6fb50-132">实体框架将推断这些属性表示外键，并将对数据库添加外键约束。</span><span class="sxs-lookup"><span data-stu-id="6fb50-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="6fb50-133">`Order` 和 `OrderDetail` 类还包括 "导航" 属性，其中包含对相关对象的引用。</span><span class="sxs-lookup"><span data-stu-id="6fb50-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="6fb50-134">给定订单后，您可以按照导航属性导航到订单中的产品。</span><span class="sxs-lookup"><span data-stu-id="6fb50-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="6fb50-135">立即编译该项目。</span><span class="sxs-lookup"><span data-stu-id="6fb50-135">Compile the project now.</span></span> <span data-ttu-id="6fb50-136">实体框架使用反射来发现模型的属性，因此它需要已编译的程序集来创建数据库架构。</span><span class="sxs-lookup"><span data-stu-id="6fb50-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="6fb50-137">配置媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="6fb50-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="6fb50-138">[媒体类型格式化程序](../../formats-and-model-binding/media-formatters.md)是一个对象，该对象在 Web API 写入 HTTP 响应正文时序列化数据。</span><span class="sxs-lookup"><span data-stu-id="6fb50-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="6fb50-139">内置格式化程序支持 JSON 和 XML 输出。</span><span class="sxs-lookup"><span data-stu-id="6fb50-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="6fb50-140">默认情况下，这两个格式化程序都按值序列化所有对象。</span><span class="sxs-lookup"><span data-stu-id="6fb50-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="6fb50-141">如果对象图包含循环引用，则按值进行序列化会导致出现问题。</span><span class="sxs-lookup"><span data-stu-id="6fb50-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="6fb50-142">这与 `Order` 和 `OrderDetail` 类的情况完全相同，因为每个类都具有对另一个的引用。</span><span class="sxs-lookup"><span data-stu-id="6fb50-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="6fb50-143">格式化程序将跟随引用，按值写入每个对象，并使用圆圈。</span><span class="sxs-lookup"><span data-stu-id="6fb50-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="6fb50-144">因此，需要更改默认行为。</span><span class="sxs-lookup"><span data-stu-id="6fb50-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="6fb50-145">在解决方案资源管理器中，展开 "应用\_启动" 文件夹，然后打开名为 "WebApiConfig.cs" 的文件。</span><span class="sxs-lookup"><span data-stu-id="6fb50-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="6fb50-146">将下面的代码添加到 `WebApiConfig` 类中:</span><span class="sxs-lookup"><span data-stu-id="6fb50-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="6fb50-147">此代码设置 JSON 格式化程序以保留对象引用，并从管道中完全删除 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="6fb50-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="6fb50-148">（您可以配置 XML 格式化程序以保留对象引用，但要做的工作要多一些，并且我们只需要此应用程序的 JSON。</span><span class="sxs-lookup"><span data-stu-id="6fb50-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="6fb50-149">有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。）</span><span class="sxs-lookup"><span data-stu-id="6fb50-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6fb50-150">[上一页](using-web-api-with-entity-framework-part-1.md)
> [下一页](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="6fb50-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>
