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
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>OData v4 中的复杂类型继承与 ASP.NET Web API

由[Microsoft](https://github.com/microsoft)

> 根据 OData v4[规范](http://www.odata.org/documentation/odata-version-4-0/)，复杂类型可以继承自其他复杂类型。 （*复杂*类型是没有键的结构化类型。）Web API OData 5.3 支持复杂的类型继承。
> 
> 本主题演示如何使用复杂的继承类型生成实体数据模型（EDM）。 有关完整的源代码，请参阅[OData 复杂类型继承示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Web API OData 5。3
> - OData v4

## <a name="model-hierarchy"></a>模型层次结构

为了说明复杂类型继承，我们将使用下面的类层次结构。

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape` 是抽象复杂类型。 `Rectangle`、`Triangle`和 `Circle` 是派生自 `Shape`的复杂类型，并且 `RoundRectangle` 派生自 `Rectangle`。 `Window` 是实体类型并且包含 `Shape` 实例。

下面是用于定义这些类型的 CLR 类。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>生成 EDM 模型

若要创建 EDM，可以使用**ODataConventionModelBuilder**，它可从 CLR 类型推断继承关系。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

还可以使用**ODataModelBuilder**显式生成 EDM。 这将需要更多代码，但可以更好地控制 EDM。

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

这两个示例创建相同的 EDM 架构。

## <a name="metadata-document"></a>元数据文档

下面是 OData 元数据文档，显示复杂的类型继承。

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

在元数据文档中，可以看到：

- `Shape` 复杂类型为抽象类型。
- `Rectangle`、`Triangle`和 `Circle` 复杂类型具有基类型 `Shape`。
- `RoundRectangle` 类型的基类型为 `Rectangle`。

## <a name="casting-complex-types"></a>转换复杂类型

现在支持在复杂类型上强制转换。 例如，下面的查询将 `Shape` 转换为 `Rectangle`。

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

下面是响应有效负载：

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
