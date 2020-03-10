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
# <a name="part-2-creating-the-domain-models"></a>第2部分：创建域模型

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a>添加模型

有三种方法可用于实体框架：

- 数据库优先：从数据库开始，实体框架生成代码。
- 模型优先：从视觉对象模型开始，实体框架生成数据库和代码。
- 代码优先：从代码开始，实体框架生成数据库。

我们使用代码优先方法，我们首先将域对象定义为 Poco （普通的 CLR 对象）。 在代码优先方法中，域对象不需要任何额外的代码就可以支持数据库层，如事务或持久性。 （具体而言，它们不需要从[EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx)类继承。）你仍可以使用数据批注来控制实体框架创建数据库架构的方式。

由于 Poco 不携带任何其他用于描述[数据库状态](https://msdn.microsoft.com/library/system.data.entitystate.aspx)的属性，因此可以轻松地将其序列化为 JSON 或 XML。 但是，这并不意味着您应该始终向客户端公开您的实体框架模型，因为我们将在本教程的后面部分介绍。

我们将创建以下 Poco：

- 产品
- 顺序
- OrderDetail

若要创建每个类，请在解决方案资源管理器中右键单击 "模型" 文件夹。 从上下文菜单中，选择 "**添加**"，然后选择 "**类"。**

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

添加具有以下实现的 `Product` 类：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

按照约定，实体框架使用 `Id` 属性作为主键，并将其映射到数据库表中的标识列。 创建新的 `Product` 实例时，不会为 `Id`设置值，因为数据库会生成值。

**ScaffoldColumn**特性指示 ASP.NET MVC 在生成编辑器窗体时跳过 `Id` 属性。 **必需**的属性用于验证模型。 它指定 `Name` 属性必须为非空字符串。

添加 `Order` 类：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

添加 `OrderDetail` 类：

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a>外键关系

订单包含许多订单详细信息，每个订单详细信息都指单个产品。 为了表示这些关系，`OrderDetail` 类定义了名为 `OrderId` 和 `ProductId`属性。 实体框架将推断这些属性表示外键，并将对数据库添加外键约束。

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

`Order` 和 `OrderDetail` 类还包括 "导航" 属性，其中包含对相关对象的引用。 给定订单后，您可以按照导航属性导航到订单中的产品。

立即编译该项目。 实体框架使用反射来发现模型的属性，因此它需要已编译的程序集来创建数据库架构。

## <a name="configure-the-media-type-formatters"></a>配置媒体类型格式化程序

[媒体类型格式化程序](../../formats-and-model-binding/media-formatters.md)是一个对象，该对象在 Web API 写入 HTTP 响应正文时序列化数据。 内置格式化程序支持 JSON 和 XML 输出。 默认情况下，这两个格式化程序都按值序列化所有对象。

如果对象图包含循环引用，则按值进行序列化会导致出现问题。 这与 `Order` 和 `OrderDetail` 类的情况完全相同，因为每个类都具有对另一个的引用。 格式化程序将跟随引用，按值写入每个对象，并使用圆圈。 因此，需要更改默认行为。

在解决方案资源管理器中，展开 "应用\_启动" 文件夹，然后打开名为 "WebApiConfig.cs" 的文件。 将下面的代码添加到 `WebApiConfig` 类中:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

此代码设置 JSON 格式化程序以保留对象引用，并从管道中完全删除 XML 格式化程序。 （您可以配置 XML 格式化程序以保留对象引用，但要做的工作要多一些，并且我们只需要此应用程序的 JSON。 有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。）

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-1.md)
> [下一页](using-web-api-with-entity-framework-part-3.md)
