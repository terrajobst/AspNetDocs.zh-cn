---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 创建数据传输对象（Dto） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445757"
---
# <a name="create-data-transfer-objects-dtos"></a>创建数据传输对象 (DTO)

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://github.com/MikeWasson/BookService)

现在，web API 将数据库实体公开给客户端。 客户端接收直接映射到数据库表的数据。 但是，这并不总是一个好主意。 有时，您需要更改发送到客户端的数据的形状。 例如，你可能希望：

- 删除循环引用（请参阅上一节）。
- 隐藏客户端不应查看的特定属性。
- 省略某些属性以减小负载大小。
- 平展包含嵌套对象的对象图，以使它们更适合客户端。
- 避免出现 "过度发布" 漏洞。 （有关过多发布的讨论，请参阅[模型验证](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。）
- 将服务层与数据库层分离。

若要实现此目的，可以定义*数据传输对象*（DTO）。 DTO 是定义如何通过网络发送数据的对象。 让我们看看如何使用 Book 实体。 在 "模型" 文件夹中，添加两个 DTO 类：

[!code-csharp[Main](part-5/samples/sample1.cs)]

`BookDetailDto` 类包括书籍模型中的所有属性，但 `AuthorName` 是将包含作者姓名的字符串。 `BookDto` 类包含 `BookDetailDto`中的属性子集。

接下来，将 `BooksController` 类中的两个 GET 方法替换为返回 Dto 的版本。 我们将使用 LINQ **Select**语句将书籍实体转换为 dto。

[!code-csharp[Main](part-5/samples/sample2.cs)]

下面是新 `GetBooks` 方法生成的 SQL。 您可以看到，EF 将 LINQ **select**转换为 SQL select 语句。

[!code-sql[Main](part-5/samples/sample3.sql)]

最后，修改 `PostBook` 方法以返回一个 DTO。

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> 在本教程中，我们将在代码中手动转换为 Dto。 另一种方法是使用[AutoMapper](http://automapper.org/)等库来自动处理转换。
> 
> [!div class="step-by-step"]
> [上一页](part-4.md)
> [下一页](part-6.md)
