---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: 创建自定义路由约束（VB） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 演示了如何创建自定义路由约束。 我们实现了一个简单的自定义约束，可防止路由与 w 。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 2330708cf4a28180ce8a05f4696bf7a7a32092d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486788"
---
# <a name="creating-a-custom-route-constraint-vb"></a>创建自定义路由约束 (VB)

作者： [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther 演示了如何创建自定义路由约束。 我们实现了一个简单的自定义约束，当浏览器请求从远程计算机发出请求时，它会阻止路由匹配。

本教程的目的是演示如何创建自定义路由约束。 使用自定义路由约束，可以防止路由匹配，除非有某些自定义条件匹配。

在本教程中，我们将创建一个 Localhost 路由约束。 Localhost 路由约束仅匹配从本地计算机发出的请求。 不匹配 Internet 上的远程请求。

通过实现 IRouteConstraint 接口实现自定义路由约束。 这是一个非常简单的接口，用于描述单一方法：

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

方法返回一个布尔值。 如果返回 False，则与该约束关联的路由将不与浏览器请求匹配。

Localhost 约束包含在列表1中。

**列表 1-LocalhostConstraint**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

列表1中的约束利用 HttpRequest 类公开的 IsLocal 属性。 当请求的 IP 地址是127.0.0.1 或请求的 IP 地址与服务器的 IP 地址相同时，此属性返回 true。

在 global.asax 文件中定义的路由内使用自定义约束。 清单2中的 global.asax 文件使用 Localhost 约束来阻止任何人请求管理页，除非他们发出来自本地服务器的请求。 例如，当从远程服务器发出请求时，/Admin/DeleteAll 的请求将会失败。

**列表 2-global.asax**

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

本地主机约束在管理路由的定义中使用。 远程浏览器请求不会匹配此路由。 但请注意，在 global.asax 中定义的其他路由可能与同一请求匹配。 必须了解的是，约束阻止特定路由匹配请求，而不是在 global.asax 文件中定义的所有路由。

请注意，默认路由已从清单2的 global.asax 文件中注释掉。 如果包括默认路由，则默认路由将与管理控制器的请求相匹配。 在这种情况下，即使其请求与管理路由不匹配，远程用户仍可以调用管理控制器的操作。

> [!div class="step-by-step"]
> [上一页](creating-a-route-constraint-vb.md)
