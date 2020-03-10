---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: 创建视图（UI） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448982"
---
# <a name="create-the-view-ui"></a>创建视图 (UI)

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，你将开始定义应用程序的 HTML，并在 HTML 与视图模型之间添加数据绑定。

打开文件视图/Home/Index。 将该文件的整个内容替换为以下内容。

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

大多数 `div` 元素都适用于[启动](http://getbootstrap.com/)样式设置。 重要元素是具有 `data-bind` 特性的元素。 此属性将 HTML 链接到视图模型。

例如:

[!code-html[Main](part-7/samples/sample2.html)]

在此示例中，&quot;`text`&quot; 绑定导致 `<p>` 元素显示视图模型中 `error` 属性的值。 请记住，`error` 被声明为 `ko.observable`：

[!code-javascript[Main](part-7/samples/sample3.js)]

每当将新值分配给 `error`时，挖空会更新 `<p>` 元素中的文本。

`foreach` 绑定通知挖空以循环遍历 `books` 数组的内容。 对于数组中的每个项，挖空会创建一个新的 &lt;li&gt; 元素。 上下文中的绑定 `foreach` 引用数组项的属性。 例如:

[!code-html[Main](part-7/samples/sample4.html)]

此处 `text` 绑定读取每本书的 Author 属性。

如果现在运行应用程序，其外观应如下所示：

![](part-7/_static/image1.png)

加载页面后，将以异步方式加载书籍的列表。 现在，&quot; 链接的 &quot;详细信息不起作用。 我们将在下一节中添加此功能。

> [!div class="step-by-step"]
> [上一页](part-6.md)
> [下一页](part-8.md)
