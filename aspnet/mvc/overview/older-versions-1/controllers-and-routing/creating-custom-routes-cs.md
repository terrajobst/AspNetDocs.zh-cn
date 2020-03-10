---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 创建自定义路由C#（） |Microsoft Docs
author: microsoft
description: 了解如何将自定义路由添加到 ASP.NET MVC 应用程序。 在本教程中，您将了解如何修改 global.asax 文件中的默认路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 58f72e390f0053d136ef00ddbda0b071ba225d98
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486722"
---
# <a name="creating-custom-routes-c"></a>创建自定义路由 (C#)

由[Microsoft](https://github.com/microsoft)

> 了解如何将自定义路由添加到 ASP.NET MVC 应用程序。 在本教程中，您将了解如何修改 global.asax 文件中的默认路由表。

本教程介绍如何将自定义路由添加到 ASP.NET MVC 应用程序。 了解如何使用自定义路由修改 global.asax 文件中的默认路由表。

对于很多简单的 ASP.NET MVC 应用程序，默认路由表将正常运行。 但是，你可能会发现你有特殊的路由需求。 在这种情况下，你可以创建自定义路由。

例如，假设您要构建一个博客应用程序。 你可能需要处理传入的请求，如下所示：

/Archive/12-25-2009

当用户输入此请求时，你想要返回与日期12/25/2009 对应的博客条目。 若要处理此类型的请求，需要创建自定义路由。

列表1中的 Global.asa 文件包含一个名为 "博客" 的新自定义路由，该路由处理类似于/Archive/*输入日期*的请求。

**列表 1-global.asax （带有自定义路由）**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

添加到路由表中的路由顺序非常重要。 新的自定义博客路由将添加到现有默认路由之前。 如果你反转了顺序，则始终会调用默认路由，而不是自定义路由。

自定义博客路由匹配所有以/Archive/. 开头的请求 因此，它匹配以下所有 Url：

- /Archive/12-25-2009

- /Archive/10-6-2004

- /Archive/apple

自定义路由会将传入请求映射到名为 Archive 的控制器，并调用 Entry （）操作。 调用 Entry （）方法时，输入日期将作为名为 entryDate 的参数进行传递。

可以在清单2中将博客自定义路由用于控制器。

**列表 2-ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

请注意，列表2中的 Entry （）方法接受 DateTime 类型的参数。 MVC 框架的智能足以将输入日期从 URL 转换为日期时间值。 如果 URL 中的输入日期参数无法转换为 DateTime，则会引发错误（请参阅图1）。

**图 1-转换参数时出错**

[!["新建项目" 对话框](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**图 01**：转换参数时出错（[单击以查看完全大小的图像](creating-custom-routes-cs/_static/image2.png)）

## <a name="summary"></a>摘要

本教程的目的是演示如何创建自定义路由。 已了解如何将自定义路由添加到表示博客条目的 Global.asa 文件中的路由表。 本文介绍了如何将博客条目请求映射到名为 ArchiveController 的控制器，以及一个名为 Entry （）的控制器操作。

> [!div class="step-by-step"]
> [上一页](aspnet-mvc-controllers-overview-cs.md)
> [下一页](creating-a-route-constraint-cs.md)
