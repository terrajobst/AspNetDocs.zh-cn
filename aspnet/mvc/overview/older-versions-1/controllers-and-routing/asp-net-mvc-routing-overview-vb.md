---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC 路由概述（VB） |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 显示 ASP.NET MVC 框架如何将浏览器请求映射到控制器操作。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486896"
---
# <a name="aspnet-mvc-routing-overview-vb"></a>ASP.NET MVC 路由概述 (VB)

作者： [Stephen Walther](https://github.com/StephenWalther)

> 在本教程中，Stephen Walther 显示 ASP.NET MVC 框架如何将浏览器请求映射到控制器操作。

本教程介绍了每个称为*ASP.NET 路由*的 ASP.NET MVC 应用程序的重要功能。 ASP.NET 路由模块负责将传入浏览器请求映射到特定 MVC 控制器操作。 在本教程结束时，您将了解标准路由表如何将请求映射到控制器操作。

## <a name="using-the-default-route-table"></a>使用默认路由表

在创建新的 ASP.NET MVC 应用程序时，应用程序已配置为使用 ASP.NET 路由。 ASP.NET 路由是在两个位置设置的。

首先，应用程序的 Web 配置文件（Web.config 文件）启用了 ASP.NET 路由。 配置文件中有四个部分与路由相关：system.web.httpModules 节、system.web.httpHandlers 节、system.webserver.modules 节和 system.webserver.handlers 节。 请注意不要删除这些节，因为如果没有这些节，路由将不再起作用。

其次，更重要的是，路由表是在应用程序的 Global.asax 文件中创建的。 Global.asax 文件是一个特殊文件，其中包含 ASP.NET 应用程序生命周期事件的事件处理程序。 路由表在 Application Start 事件中创建。

列表1中的文件包含 ASP.NET MVC 应用程序的默认 global.asax 文件。

**列表 1-global.asax**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

MVC 应用程序首次启动时，将调用应用程序\_Start （）方法。 此方法反过来会调用 RegisterRoutes() 方法。 RegisterRoutes() 方法负责创建路由表。

默认路由表包含一个路由（名为 Default）。 默认路由将 URL 的第一段映射到控制器名称，将 URL 的第二段映射到控制器操作，并将第三段映射到名为**id**的参数。

假设你在 web 浏览器的地址栏中输入以下 URL：

/Home/Index/3

默认路由将此 URL 映射到以下参数：

- 控制器 = Home

- 操作 = 索引

- id = 3

请求 URL/Home/Index/3 时，将执行以下代码：

HomeController.Index(3)

Default 路由包括所有三个参数的默认值。 如果不提供控制器，则控制器参数默认为值**Home**。 如果不提供操作，则操作参数将默认为值**索引**。 最后，如果不提供 id，id 参数将默认为空字符串。

让我们看几个有关默认路由如何将 Url 映射到控制器操作的示例。 假设你在浏览器地址栏中输入以下 URL：

/Home

由于 Default 路由参数存在默认值，输入此 URL 将导致 HomeController 类的 Index() 方法在列表 2 中被调用。

**列表 2-HomeController**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

在列表2中，HomeController 类包含一个名为 Index （）的方法，该方法接受名为 Id 的单一参数。URL/Home 导致调用 Index （）方法时，不会将值视为 Id 参数的值。

由于 MVC 框架调用控制器操作的方式，URL/Home 还与列表3中 HomeController 类的 Index （）方法匹配。

**列表 3-HomeController （不带参数的索引操作）**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

清单3中的 Index （）方法不接受任何参数。 URL/Home 将导致调用此索引（）方法。 URL/Home/Index/3 还会调用此方法（忽略 Id）。

URL/Home 还与列表4中 HomeController 类的 Index （）方法匹配。

**列表 4-HomeController （索引操作，参数可以为 null）**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

在列表4中，Index （）方法有一个整数参数。 因为参数是一个可以为 null 的参数（可以不包含任何值），所以可以在不引发错误的情况下调用索引（）。

最后，在使用 URL/Home 的列表5中调用 Index （）方法将导致异常，因为 Id 参数*不*是可以为 null 的参数。 如果尝试调用 Index （）方法，则会获得图1中显示的错误。

**列出 HomeController （Id 参数的索引操作）**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

[![调用需要参数值的控制器操作](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)

**图 01**：调用需要参数值的控制器操作（[单击以查看完全大小的图像](asp-net-mvc-routing-overview-vb/_static/image2.png)）

另一方面，URL/Home/Index/3 的工作方式与清单5中的索引控制器操作非常相似。 请求/Home/Index/3 导致使用值为3的 Id 参数调用 Index （）方法。

## <a name="summary"></a>摘要

本教程的目的是提供 ASP.NET 路由的简要介绍。 我们检查了你使用新的 ASP.NET MVC 应用程序获取的默认路由表。 已了解默认路由如何将 Url 映射到控制器操作。

> [!div class="step-by-step"]
> [上一页](creating-an-action-cs.md)
> [下一页](understanding-action-filters-vb.md)
