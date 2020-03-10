---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: 支持带有 Web API 2 的 OData v3 中的实体关系 |Microsoft Docs
author: MikeWasson
description: 大多数数据集定义实体之间的关系：客户具有订单;书作者：产品具有供应商。 使用 OData，客户端可以导航到 。
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484502"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a>支持带有 Web API 2 的 OData v3 中的实体关系

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 大多数数据集定义实体之间的关系：客户具有订单;书作者：产品具有供应商。 使用 OData，客户端可在实体关系上导航。 在给定产品的情况下，您可以找到该供应商。 您还可以创建或删除关系。 例如，可以设置产品的供应商。
> 
> 本教程演示如何在 ASP.NET Web API 中支持这些操作。 本教程基于[使用 WEB API 2 创建 OData V3 终结点](creating-an-odata-endpoint.md)教程。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Web API 2
> - OData 版本3
> - Entity Framework 6

## <a name="add-a-supplier-entity"></a>添加供应商实体

首先，我们需要将新的实体类型添加到 OData 源。 我们将添加一个 `Supplier` 类。

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

此类使用实体键的字符串。 在实践中，这种做法可能不如使用整数键常见。 但值得注意的是，OData 如何处理除整数以外的其他密钥类型。

接下来，我们将通过向 `Product` 类添加 `Supplier` 属性来创建一个关系：

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

将新的**DbSet**添加到 `ProductServiceContext` 类中，以便实体框架将 `Supplier` 表包括在数据库中。

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

在 WebApiConfig.cs 中，将 "供应商" 实体添加到 EDM 模型：

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a>导航属性

若要获取产品的供应商，客户端将发送 GET 请求：

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

此处的 "供应商" 是 `Product` 类型的导航属性。 在这种情况下，`Supplier` 引用单个项，但导航属性还可以返回集合（一对多或多对多关系）。

若要支持此请求，请将以下方法添加到 `ProductsController` 类：

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

*Key*参数是产品的键。 此方法在此示例中&#8212;返回相关实体，即一个 `Supplier` 实例。 方法名称和参数名称都是重要的。 通常，如果导航属性名为 "X"，则需要添加一个名为 "GetX" 的方法。 此方法必须采用一个名为 "*key*" 的参数，该参数与父项的键的数据类型匹配。

还必须在*key*参数中包含 **[FromOdataUri]** 属性。 此属性告知 Web API 在分析来自请求 URI 的密钥时使用 OData 语法规则。

## <a name="creating-and-deleting-links"></a>创建和删除链接

OData 支持在两个实体之间创建或删除关系。 在 OData 术语中，关系是一个 "链接"。 每个链接都有一个 URI，其形式为*entity*/$links/*entity*。 例如，从产品到供应商的链接如下所示：

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

若要创建新链接，客户端会将 POST 请求发送到链接 URI。 请求正文是目标实体的 URI。 例如，假设有一个供应商的密钥为 "CTSO"。 若要创建从 "Product （1）" 到 "CTSO"）的链接，客户端将发送如下请求：

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

若要删除链接，客户端会将删除请求发送到链接 URI。

**创建链接**

若要允许客户端创建产品供应商链接，请将以下代码添加到 `ProductsController` 类：

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

该方法采用三个参数：

- *key*：父实体（产品）的键
- *navigationProperty*：导航属性的名称。 在此示例中，唯一有效的导航属性为 "供应商"。
- *link*：相关实体的 OData URI。 此值取自请求正文。 例如，链接 URI 可以是 "`http://localhost/odata/Suppliers('CTSO')`，这意味着 ID =" CTSO "的供应商。

方法使用链接查找供应商。 如果找到匹配的供应商，则方法将设置 `Product.Supplier` 属性，并将结果保存到数据库。

最难的部分是分析链接 URI。 基本上，需要模拟将 GET 请求发送到该 URI 的结果。 以下帮助器方法显示了如何执行此操作。 方法调用 Web API 路由进程，并返回表示已分析 OData 路径的**ODataPath**实例。 对于链接 URI，其中一个段应为实体键。 （如果不是，则客户端发送了错误的 URI。）

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

**删除链接**

若要删除链接，请将以下代码添加到 `ProductsController` 类：

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

在此示例中，导航属性是单个 `Supplier` 实体。 如果导航属性是集合，则用于删除链接的 URI 必须包含相关实体的键。 例如:

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

此请求从客户1中删除订单1。 在这种情况下，DeleteLink 方法将具有以下签名：

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

*RelatedKey*参数为相关实体提供密钥。 因此，在 `DeleteLink` 方法中，按*键*参数查找主实体，通过*relatedKey*参数查找相关实体，然后删除关联。 可能需要实现 `DeleteLink`的两个版本，具体取决于您的数据模型。 Web API 将根据请求 URI 调用正确的版本。
