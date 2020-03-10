---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: 创建路由约束（C#） |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 演示了如何通过使用正则表达式创建路由约束来控制浏览器请求如何匹配路由。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470162"
---
# <a name="creating-a-route-constraint-c"></a>创建路由约束 (C#)

作者： [Stephen Walther](https://github.com/StephenWalther)

> 在本教程中，Stephen Walther 演示了如何通过使用正则表达式创建路由约束来控制浏览器请求如何匹配路由。

使用路由约束可以限制与特定路由匹配的浏览器请求。 可以使用正则表达式指定路由约束。

例如，假设你已在 global.asax 文件中的列表1中定义路由。

**列表 1-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

列表1包含名为 Product 的路由。 您可以使用产品路由将浏览器请求映射到列表2中包含的 ProductController。

**列表 2-Controllers\ProductController.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

请注意，产品控制器公开的详细信息（）操作接受名为 "productId" 的单个参数。 此参数是一个整数参数。

列表1中定义的路由将匹配以下任何 Url：

- /Product/23
- /Product/7

遗憾的是，该路由还会匹配以下 Url：

- /Product/blah
- /Product/apple

由于 Details （）操作需要整数参数，因此，如果请求包含整数值以外的值，则会导致错误。 例如，如果在浏览器中键入 URL/Product/apple，则会收到图1中的错误页。

[!["新建项目" 对话框](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)

**图 01**：查看页面分解（[单击以查看完全大小的图像](creating-a-route-constraint-cs/_static/image2.png)）

你真正想要做的只是匹配包含适当整数 productId 的 Url。 定义路由时，可以使用约束来限制与路由匹配的 Url。 清单3中修改后的产品路由包含仅匹配整数的正则表达式约束。

**列表 3-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

正则表达式 \d + 匹配一个或多个整数。 此约束会导致产品路由与以下 Url 匹配：

- /Product/3
- /Product/8999

但不是以下 Url：

- /Product/apple
- /Product

- 这些浏览器请求将由其他路由处理; 如果没有匹配的路由，则将返回 *"找不到资源"* 错误。

> [!div class="step-by-step"]
> [上一页](creating-custom-routes-cs.md)
> [下一页](creating-a-custom-route-constraint-cs.md)
