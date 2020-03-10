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
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>使用 Web API 2.2 在 OData v4 中创建单一实例

作者： Zoe Luo

> 通常，仅当实体封装在实体集内时，才能访问该实体。 但 OData v4 提供了两个额外的选项，即 Singleton 和包容，两者都支持 WebAPI 2.2。

本文介绍如何在 Web API 2.2 中定义 OData 终结点中的单一实例。 若要了解什么是单一实例以及如何使用它，请参阅[使用单一实例定义特殊实体](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx)。 若要在 Web API 中创建 OData V4 终结点，请参阅[使用 ASP.NET Web API 2.2 创建 odata V4 终结点](create-an-odata-v4-endpoint.md)。 

我们将使用以下数据模型在 Web API 项目中创建单一实例：

![数据模型](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

将根据类型 `Company`定义名为 `Umbrella` 的单一实例，并基于类型 `Employee`定义名为 `Employees` 的实体集。

本教程中使用的解决方案可以从[CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)下载。

## <a name="define-the-data-model"></a>定义数据模型

1. 定义 CLR 类型。

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. 基于 CLR 类型生成 EDM 模型。

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    在这里，`builder.Singleton<Company>("Umbrella")` 告知模型生成器在 EDM 模型中创建一个名为 `Umbrella` 的单一实例。

    生成的元数据将如下所示：

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    从元数据中，可以看到 `Employees` 实体集中 `Company` 的导航属性绑定到单一实例 `Umbrella`。 绑定由 `ODataConventionModelBuilder`自动完成，因为只有 `Umbrella` 具有 `Company` 类型。 如果模型中存在任何不明确性，可以使用 `HasSingletonBinding` 将导航属性显式绑定到单一实例;`HasSingletonBinding` 与使用 CLR 类型定义中的 `Singleton` 特性具有相同的效果：

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>定义单独控制器

与 EntitySet 控制器一样，singleton 控制器继承自 `ODataController`，单独控制器名称应为 `[singletonName]Controller`。

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

为了处理不同种类的请求，需要在控制器中预定义操作。 默认情况下，WebApi 2.2 中启用了**属性路由**。 例如，若要使用属性路由定义处理 `Company` 的查询 `Revenue` 操作，请使用以下内容：

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

如果你不愿意为每个操作定义属性，只需在[OData 路由约定](../odata-routing-conventions.md)后定义你的操作。 由于查询单一实例不需要密钥，因此在单一控制器中定义的操作与 entityset 控制器中定义的操作稍有不同。

下面列出了单一实例控制器中的每个操作定义的方法签名，以供参考。

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

基本上，这就是您需要在服务端完成的所有工作。 [示例项目](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)包含解决方案的所有代码，以及演示如何使用 Singleton 的 OData 客户端。 客户端是按照[创建 OData V4 客户端应用](create-an-odata-v4-client-app.md)中的步骤生成的。

. 

*感谢在本文的原始内容中 Leo 的。*
