---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: 了解操作筛选器（VB） |Microsoft Docs
author: microsoft
description: 本教程的目的是说明操作筛选器。 操作筛选器是一个属性，可应用于控制器操作--或整个控制器 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 263658231ccaa7863508c691a3570bc00b9e8039
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486584"
---
# <a name="understanding-action-filters-vb"></a>了解操作筛选器 (VB)

由[Microsoft](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> 本教程的目的是说明操作筛选器。 操作筛选器是一种可应用于控制器操作（或整个控制器）的属性，用于修改操作的执行方式。

## <a name="understanding-action-filters"></a>了解操作筛选器

本教程的目的是说明操作筛选器。 操作筛选器是一种可应用于控制器操作（或整个控制器）的属性，用于修改操作的执行方式。 ASP.NET MVC 框架包含多个操作筛选器：

- OutputCache –此操作筛选器将控制器操作的输出缓存指定的一段时间。
- HandleError –此操作筛选器处理控制器操作执行时引发的错误。
- 授权–此操作筛选器使你可以限制对特定用户或角色的访问。

还可以创建自己的自定义操作筛选器。 例如，你可能想要创建自定义操作筛选器以实现自定义身份验证系统。 或者，您可能想要创建一个操作筛选器来修改控制器操作返回的视图数据。

在本教程中，你将了解如何从头开始构建操作筛选器。 我们创建了一个日志操作筛选器，该筛选器将操作处理的不同阶段记录到 Visual Studio "输出" 窗口中。

### <a name="using-an-action-filter"></a>使用操作筛选器

操作筛选器是一个属性。 您可以将大多数操作筛选器应用于单个控制器操作或整个控制器。

例如，列表1中的数据控制器公开一个名为 `Index()` 的操作，该操作返回当前时间。 此操作通过 `OutputCache` 操作筛选器修饰。 此筛选器使操作返回的值缓存10秒。

**列表1– `Controllers\DataController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

如果重复调用 `Index()` 操作，方法是在浏览器的地址栏中输入 URL/Data/Index，并多次点击 "刷新" 按钮，则会看到相同的时间为10秒。 `Index()` 操作的输出将缓存10秒（参见图1）。

[![缓存时间](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)

**图 01**：缓存时间（[单击以查看完全大小的图像](understanding-action-filters-vb/_static/image3.png)）

在列表1中，单个操作筛选器– `OutputCache` 操作筛选器–应用于 `Index()` 方法。 如果需要，可以将多个操作筛选器应用于同一操作。 例如，你可能想要将 `OutputCache` 和 `HandleError` 操作筛选器应用于同一操作。

在列表1中，`OutputCache` 操作筛选器将应用于 `Index()` 操作。 您还可以将此特性应用于 `DataController` 类本身。 在这种情况下，由控制器公开的任何操作返回的结果将缓存10秒。

### <a name="the-different-types-of-filters"></a>不同类型的筛选器

ASP.NET MVC 框架支持四种不同类型的筛选器：

1. 授权筛选器–实现 `IAuthorizationFilter` 特性。
2. 操作筛选器–实现 `IActionFilter` 特性。
3. 结果筛选器–实现 `IResultFilter` 特性。
4. 异常筛选器–实现 `IExceptionFilter` 特性。

筛选器按照上面列出的顺序执行。 例如，始终先执行授权筛选器，然后在每个其他类型的筛选器之后始终执行操作筛选器和异常筛选器。

授权筛选器用于实现控制器操作的身份验证和授权。 例如，授权筛选器就是授权筛选器的一个示例。

操作筛选器包含执行控制器操作之前和之后执行的逻辑。 例如，可以使用操作筛选器来修改控制器操作返回的视图数据。

结果筛选器包含执行视图结果之前和之后执行的逻辑。 例如，你可能想要在视图呈现给浏览器之前修改视图结果。

异常筛选器是要运行的最后一类筛选器。 您可以使用异常筛选器来处理控制器操作或控制器操作结果引发的错误。 还可以使用异常筛选器记录错误。

每种不同类型的筛选器都按特定顺序执行。 如果要控制执行相同类型的筛选器的顺序，则可以设置筛选器的 Order 属性。

所有操作筛选器的基类都是 `System.Web.Mvc.FilterAttribute` 类。 如果要实现特定类型的筛选器，则需要创建一个继承自基本筛选器类的类，并实现一个或多个 IAuthorizationFilter、IActionFilter、IResultFilter 或 ExceptionFilter 接口。

### <a name="the-base-actionfilterattribute-class"></a>基本 ActionFilterAttribute 类

为了使你能够更轻松地实现自定义操作筛选器，ASP.NET MVC 框架包含一个基本 `ActionFilterAttribute` 类。 此类同时实现 `IActionFilter` 和 `IResultFilter` 接口，并继承自 `Filter` 类。

此处的术语并不完全一致。 从技术上说，继承自 ActionFilterAttribute 类的类既是操作筛选器，也是结果筛选器。 但是，在松散意义上，word 操作筛选器用于引用 ASP.NET MVC 框架中的任何类型的筛选器。

基本 ActionFilterAttribute 类具有以下可重写的方法：

- OnActionExecuting –在执行控制器操作之前调用此方法。
- OnActionExecuted –在执行控制器操作后调用此方法。
- OnResultExecuting –在执行控制器操作结果之前调用此方法。
- OnResultExecuted –在执行控制器操作结果后调用此方法。

在下一部分中，我们将了解如何实现上述每种不同的方法。

### <a name="creating-a-log-action-filter"></a>创建日志操作筛选器

为了说明如何生成自定义操作筛选器，我们将创建一个自定义操作筛选器，用于将处理控制器操作的阶段记录到 Visual Studio "输出" 窗口中。 我们的 `LogActionFilter` 包含在清单2中。

**列表2– `ActionFilters\LogActionFilter.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

在列表2中，`OnActionExecuting()`、`OnActionExecuted()`、`OnResultExecuting()`和 `OnResultExecuted()` 方法均调用 `Log()` 方法。 方法的名称和当前路由数据将传递到 `Log()` 方法。 `Log()` 方法将消息写入 Visual Studio 输出窗口（参见图2）。

[![写入 Visual Studio 输出窗口](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)

**图 02**：写入到 Visual Studio "输出" 窗口（[单击以查看完全大小的图像](understanding-action-filters-vb/_static/image6.png)）

列表3中的 Home 控制器说明了如何对整个控制器类应用日志操作筛选器。 每当调用由 Home 控制器公开的任何操作时（`Index()` 方法或 `About()` 方法），处理该操作的阶段都将记录到 Visual Studio 的 "输出" 窗口中。

**列表 3-`Controllers\HomeController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a>摘要

本教程介绍了如何 ASP.NET MVC 操作筛选器。 已了解四种不同类型的筛选器：授权筛选器、操作筛选器、结果筛选器和异常筛选器。 还了解了基本 `ActionFilterAttribute` 类。

最后，您学习了如何实现简单的操作筛选器。 我们创建了一个日志操作筛选器，该筛选器将处理控制器操作的阶段记录到 Visual Studio "输出" 窗口中。

> [!div class="step-by-step"]
> [上一页](asp-net-mvc-routing-overview-vb.md)
> [下一页](improving-performance-with-output-caching-vb.md)
