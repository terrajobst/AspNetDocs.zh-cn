---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 向数据库添加新项 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448970"
---
# <a name="add-a-new-item-to-the-database"></a>向数据库添加一个新项

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，你将添加用户创建新书籍的能力。 在 node.js 中，将以下代码添加到视图模型：

[!code-javascript[Main](part-9/samples/sample1.js)]

在 "索引" 中，替换以下标记：

[!code-html[Main](part-9/samples/sample2.html)]

替换为：

[!code-html[Main](part-9/samples/sample3.html)]

此标记创建用于提交新作者的窗体。 "作者" 下拉列表的值被数据绑定到视图模型中的 `authors` 可见。 对于其他窗体输入，值被数据绑定到视图模型的 `newBook` 属性。

窗体上的提交处理程序绑定到 `addBook` 函数：

[!code-html[Main](part-9/samples/sample4.html)]

`addBook` 函数读取数据绑定窗体输入的当前值，以创建 JSON 对象。 然后，它将 JSON 对象发送到 `/api/books`。

> [!div class="step-by-step"]
> [上一页](part-8.md)
> [下一页](part-10.md)
