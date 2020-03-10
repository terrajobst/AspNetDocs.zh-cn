---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: 在 OData v4 中用 ASP.NET Web API 打开类型 |Microsoft Docs
author: microsoft
description: 在 OData v4 中，开放类型是一种结构化类型，其中包含动态属性以及在类型定义中声明的任何属性。 打开...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504578"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>在 OData v4 中用 ASP.NET Web API 打开类型

由[Microsoft](https://github.com/microsoft)

> 在 OData v4 中，*开放类型*是一种结构化类型，其中包含动态属性以及在类型定义中声明的任何属性。 开放式类型使你可以为数据模型添加灵活性。 本教程演示如何使用 ASP.NET Web API OData 中的开放类型。
> 
> 本教程假定你已了解如何在 ASP.NET Web API 中创建 OData 终结点。 如果未启用，请首先阅读[创建 OData V4 终结点](create-an-odata-v4-endpoint.md)。
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - Web API OData 5。3
> - OData v4

首先，一些 OData 术语：

- 实体类型：具有键的结构化类型。
- 复杂类型：没有键的结构化类型。
- 开放式类型：包含动态属性的类型。 实体类型和复杂类型都可以打开。

动态属性的值可以是基元类型、复杂类型或枚举类型;或任何这些类型的集合。 有关开放类型的详细信息，请参阅[OData v4 规范](http://www.odata.org/documentation/odata-version-4-0/)。

## <a name="install-the-web-odata-libraries"></a>安装 Web OData 库

使用 NuGet 包管理器安装最新的 Web API OData 库。 从 "包管理器控制台" 窗口：

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>定义 CLR 类型

首先，将 EDM 模型定义为 CLR 类型。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

创建实体数据模型（EDM）时，

- `Category` 为枚举类型。
- `Address` 是一种复杂类型。 （它没有密钥，因此它不是实体类型。）
- `Customer` 是实体类型。 （有一个键。）
- `Press` 为开放式复杂类型。
- `Book` 是一种开放的实体类型。

若要创建开放类型，CLR 类型必须有一个类型为 `IDictionary<string, object>`的属性，该属性包含动态属性。

## <a name="build-the-edm-model"></a>生成 EDM 模型

如果使用**ODataConventionModelBuilder**创建 EDM，则基于是否存在 `IDictionary<string, object>` 属性，`Press` 和 `Book` 会自动添加为开放类型。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

还可以使用**ODataModelBuilder**显式生成 EDM。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>添加 OData 控制器

接下来，添加 OData 控制器。 对于本教程，我们将使用简单的控制器，该控制器仅支持 GET 和 POST 请求，并使用内存中列表存储实体。

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

请注意，第一个 `Book` 实例没有动态属性。 第二个 `Book` 实例具有以下动态属性：

- "已发布"：基元类型
- "作者"：基元类型的集合
- "OtherCategories"：枚举类型的集合。

此外，`Book` 实例的 `Press` 属性具有以下动态属性：

- "博客"：基元类型
- "Address"：复杂类型

## <a name="query-the-metadata"></a>查询元数据

若要获取 OData 元数据文档，请将 GET 请求发送到 `~/$metadata`。 响应正文应类似于：

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

在元数据文档中，可以看到：

- 对于 `Book` 和 `Press` 类型，`OpenType` 属性的值为 true。 `Customer` 和 `Address` 类型不具有此属性。
- `Book` 实体类型具有三个已声明的属性： ISBN、Title 和按压。 OData 元数据不包括 CLR 类中的 `Book.Properties` 属性。
- 同样，`Press` 复杂类型仅包含两个已声明的属性：名称和类别。 元数据不包括 CLR 类中的 `Press.DynamicProperties` 属性。

## <a name="query-an-entity"></a>查询实体

若要获取 ISBN 等于 "978-0-7356-7942-9" 的书籍，请将 GET 请求发送到 `~/Books('978-0-7356-7942-9')`。 响应正文应类似于以下内容。 （缩进以使其更具可读性。）

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

请注意，动态属性与已声明的属性一起包含在一起。

## <a name="post-an-entity"></a>发布实体

若要添加 Book 实体，请将 POST 请求发送到 `~/Books`。 客户端可以设置请求负载中的动态属性。

下面是一个示例请求。 请注意 "价格" 和 "已发布" 属性。

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

如果在控制器方法中设置断点，可以看到 Web API 已将这些属性添加到 `Properties` 字典中。

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>其他资源

[OData 开放式类型示例](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
