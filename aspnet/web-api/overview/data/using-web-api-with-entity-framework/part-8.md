---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 显示项详细信息 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449000"
---
# <a name="display-item-details"></a>显示项详细信息

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，你将添加查看每个书籍的详细信息的能力。 在 node.js 中，将以下代码添加到视图模型：

[!code-javascript[Main](part-8/samples/sample1.js)]

在 Views/Home/索引中，将数据绑定元素添加到详细信息链接：

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

这会将 &lt;&gt; 元素的 click 处理程序绑定到视图模型上的 `getBookDetail` 函数。

在同一文件中，替换以下标记：

[!code-html[Main](part-8/samples/sample3.html)]

替换为以下内容：

[!code-html[Main](part-8/samples/sample4.html)]

此标记创建一个表，该表绑定到视图模型中的 `detail` 的属性。

"&lt;!--ko&gt;&quot; 语法允许在 DOM 元素之外包含挖空绑定。 在这种情况下，仅当 `details` 为非 null 时，`if` 绑定才会显示此部分标记。

[!code-html[Main](part-8/samples/sample5.html)]

现在，如果运行应用并单击 &quot;详细信息&quot; 链接之一，该应用将显示书籍详细信息。

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [上一页](part-7.md)
> [下一页](part-9.md)
