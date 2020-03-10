---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: 处理实体关系 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449120"
---
# <a name="handling-entity-relations"></a>处理实体关系

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://github.com/MikeWasson/BookService)

本部分详细介绍了 EF 如何加载相关实体，以及如何处理模型类中的循环导航属性。 （本部分提供了背景知识，并不是完成本教程所必需的。 如果愿意，请跳到第[5 部分。](part-5.md)

## <a name="eager-loading-versus-lazy-loading"></a>预先加载与延迟加载

将 EF 用于关系数据库时，请务必了解 EF 如何加载相关数据。

这也有助于查看 EF 生成的 SQL 查询。 若要跟踪 SQL，请将以下代码行添加到 `BookServiceContext` 构造函数：

[!code-csharp[Main](part-4/samples/sample1.cs)]

如果将 GET 请求发送到/api/books，它将返回如下所示的 JSON：

[!code-console[Main](part-4/samples/sample2.cmd)]

您可以看到 Author 属性为 null，即使该书包含有效的作者。 这是因为 EF 未加载相关的作者实体。 SQL 查询的跟踪日志会确认这一点：

[!code-console[Main](part-4/samples/sample3.sql)]

SELECT 语句采用书籍表，而不引用作者表。

下面是 `BooksController` 类中返回书籍列表的方法。

[!code-csharp[Main](part-4/samples/sample4.cs)]

我们来看看如何将作者返回为 JSON 数据的一部分。 有三种方法可以在实体框架中加载相关数据：预先加载、延迟加载和显式加载。 每种方法都有权衡，因此了解它们的工作原理很重要。

### <a name="eager-loading"></a>预先加载

如果*预先加载*，则 EF 会将相关实体加载到初始数据库查询中。 若要执行预先加载，请使用**system.web. Include**扩展方法。

[!code-csharp[Main](part-4/samples/sample5.cs)]

这会告知 EF 将作者数据包含在查询中。 如果进行此更改并运行应用，则 JSON 数据现在如下所示：

[!code-console[Main](part-4/samples/sample6.cmd)]

跟踪日志显示 EF 对书籍和作者表执行联接。

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a>延迟加载

使用延迟加载时，当取消引用实体的导航属性时，EF 会自动加载相关实体。 若要启用延迟加载，请将导航属性设置为虚拟。 例如，在 Book 类中：

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

现在，请考虑以下代码：

[!code-csharp[Main](part-4/samples/sample9.cs)]

启用延迟加载后，访问 `books[0]` 上的 `Author` 属性会导致 EF 为作者查询数据库。

延迟加载需要多个数据库行程，因为在每次检索相关实体时 EF 都会发送一个查询。 通常，您希望为您序列化的对象禁用延迟加载。 序列化程序必须读取模型上的所有属性，这将触发加载相关实体。 例如，当 EF 序列化启用了延迟加载的书籍列表时，以下是 SQL 查询。 你可以看到，EF 为三个作者进行了三次单独的查询。

[!code-console[Main](part-4/samples/sample10.sql)]

有时可能需要使用延迟加载。 预先加载可能会导致 EF 生成非常复杂的联接。 或者，可能需要一小部分数据的相关实体，延迟加载会更有效。

避免序列化问题的一种方法是序列化数据传输对象（Dto）而不是实体对象。 本文稍后会介绍此方法。

### <a name="explicit-loading"></a>显式加载

显式加载类似于延迟加载，只不过您在代码中显式获取了相关数据，在访问导航属性时，不会自动发生此情况。 显式加载使你可以更好地控制加载相关数据的时间，但需要额外的代码。 有关显式加载的详细信息，请参阅[加载相关实体](https://msdn.microsoft.com/data/jj574232#explicit)。

## <a name="navigation-properties-and-circular-references"></a>导航属性和循环引用

定义书籍和作者模型时，我在 "`Book`" 类上为 "书籍-作者" 关系定义了导航属性，但没有按其他方向定义导航属性。

如果将相应的导航属性添加到 `Author` 类，会发生什么情况？

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

遗憾的是，这会导致在序列化模型时出现问题。 如果加载相关数据，则会创建一个圆形对象图。

![](part-4/_static/image1.png)

当 JSON 或 XML 格式化程序尝试序列化关系图时，将引发异常。 这两个格式化程序引发不同的异常消息。 下面是 JSON 格式化程序的示例：

[!code-console[Main](part-4/samples/sample12.cmd)]

下面是 XML 格式化程序：

[!code-xml[Main](part-4/samples/sample13.xml)]

一种解决方法是使用 Dto，我将在下一节中介绍。 或者，你可以配置 JSON 和 XML 格式化程序来处理图形周期。 有关详细信息，请参阅[处理循环对象引用](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。

对于本教程，不需要 `Author.Book` 导航属性，因此可将其省略。

> [!div class="step-by-step"]
> [上一页](part-3.md)
> [下一页](part-5.md)
