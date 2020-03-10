---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 2 OData 的安全指南-ASP.NET 4。x
author: MikeWasson
description: 描述在 ASP.NET 4.x 上通过 OData 公开 ASP.NET Web API 2 的数据集时要考虑的安全问题。
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448292"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 OData 的安全指南

作者： [Mike Wasson](https://github.com/MikeWasson)

本主题介绍在 ASP.NET 4.x 上通过 OData 公开 ASP.NET Web API 2 的数据集时应考虑的一些安全问题。

## <a name="edm-security"></a>EDM 安全性

查询语义基于实体数据模型（EDM），而不是基础模型类型。 可以从 EDM 中排除属性，而不会对查询显示此属性。 例如，假设您的模型包含一个具有 Salary 属性的雇员类型。 你可能想要从 EDM 中排除此属性，以将其从客户端中隐藏。

可以通过两种方法从 EDM 中排除属性。 您可以在 model 类的属性中设置 **[IgnoreDataMember]** 属性：

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

还可以通过编程方式从 EDM 中删除属性：

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>查询安全性

恶意或简单的客户端可能会构建花费很长时间执行的查询。 在最坏的情况下，这可能会中断对服务的访问。

" **[可查询]** " 属性是一个操作筛选器，用于分析、验证和应用查询。 筛选器会将查询选项转换为 LINQ 表达式。 当 OData 控制器返回**IQueryable**类型时， **iqueryable** linq 提供程序会将 linq 表达式转换为查询。 因此，性能取决于所使用的 LINQ 提供程序，还取决于您的数据集或数据库架构的特定特性。

有关在 ASP.NET Web API 中使用 OData 查询选项的详细信息，请参阅[支持 Odata 查询选项](supporting-odata-query-options.md)。

如果你知道所有客户端均受信任（例如，在企业环境中），或者如果你的数据集很小，则查询性能可能不是问题。 否则，应考虑下列建议。

- 通过各种查询测试服务并分析数据库。
- 启用服务器驱动的分页，以避免在一个查询中返回大数据集。 有关详细信息，请参阅[服务器驱动的分页](supporting-odata-query-options.md#server-paging)。 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- 是否需要 $filter 和 $orderby？ 某些应用程序可能允许使用 $top 和 $skip 的客户端分页，但禁用其他查询选项。 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- 请考虑将 $orderby 限制为聚集索引中的属性。 对不包含聚集索引的大型数据进行排序非常慢。 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- 最大节点计数： **[可查询]** 上的**MaxNodeCount**属性设置 $filter 语法树中允许的最大节点数。 默认值为100，但你可能想要设置较低的值，因为大量的节点可能会很慢，无法编译。 如果使用 LINQ to Objects （即，在内存中的集合上使用 LINQ 查询，而不使用中间 LINQ 提供程序），则更是如此。 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- 请考虑禁用 any （）和 all （）函数，因为这可能会很慢。 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- 例如，如果任何字符串属性包含&#8212;大型字符串（例如，产品描述或博客条目&#8212;），请考虑禁用字符串函数。 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- 请考虑禁止对导航属性进行筛选。 筛选导航属性可能会导致联接，这可能会很慢，具体取决于数据库架构。 下面的代码演示了阻止筛选导航属性的查询验证程序。 有关查询验证程序的详细信息，请参阅[查询验证](supporting-odata-query-options.md#query-validation)。 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- 请考虑通过编写为数据库自定义的验证程序来限制 $filter 查询。 例如，考虑以下两个查询： 

  - 具有姓氏以 "A" 开头的参与者的所有电影。
  - 1994中发布的所有电影。

    如果使用者对电影进行索引，则第一次查询可能需要数据库引擎才能扫描整个电影列表。 但第二个查询可能是可接受的，假设电影按发行年份进行索引。

    下面的代码演示一个验证程序，该验证程序允许筛选 "ReleaseYear" 和 "Title" 属性，但不允许使用其他属性。

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- 一般情况下，请考虑所需的 $filter 函数。 如果客户端无需完全表现力的 $filter，则可以限制允许的函数。
