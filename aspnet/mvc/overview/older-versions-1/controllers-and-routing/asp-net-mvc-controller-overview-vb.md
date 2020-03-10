---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC 控制器概述（VB） |Microsoft Docs
author: StephenWalther
description: 在本教程中，Stephen Walther 介绍了 ASP.NET MVC 控制器。 了解如何创建新控制器并返回不同类型的操作 res 。
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f19e7dd7fc025de2e0c387db898d36623e790e6a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486920"
---
# <a name="aspnet-mvc-controller-overview-vb"></a>ASP.NET MVC 控制器概述 (VB)

作者： [Stephen Walther](https://github.com/StephenWalther)

> 在本教程中，Stephen Walther 介绍了 ASP.NET MVC 控制器。 了解如何创建新控制器并返回不同类型的操作结果。

本教程将探讨 ASP.NET MVC 控制器、控制器操作和操作结果的相关主题。 完成本教程后，你将了解如何使用控制器来控制访问者与 ASP.NET MVC 网站交互的方式。

## <a name="understanding-controllers"></a>了解控制器

MVC 控制器负责响应针对 ASP.NET MVC 网站发出的请求。 每个浏览器请求将映射到特定的控制器。 例如，假设你在浏览器的地址栏中输入以下 URL：

`http://localhost/Product/Index/3`

在这种情况下，将调用名为 ProductController 的控制器。 ProductController 负责生成对浏览器请求的响应。 例如，控制器可能会将特定视图返回到浏览器，或者控制器可能会将用户重定向到另一个控制器。

列表1包含一个名为 ProductController 的简单控制器。

**Listing1 - Controllers\ProductController.vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

从列表1可以看出，控制器只是类（一种 Visual Basic 的 .NET 或C#类）。 控制器是一个派生自基 System.web 类的类。 由于控制器继承自此基类，控制器继承了几个免费的有用方法（稍后我们将讨论这些方法）。

## <a name="understanding-controller-actions"></a>了解控制器操作

控制器公开控制器操作。 操作是在浏览器地址栏中输入特定 URL 时调用的控制器上的方法。 例如，假设您对以下 URL 发出请求：

`http://localhost/Product/Index/3`

在这种情况下，将在 ProductController 类上调用 Index （）方法。 Index （）方法是控制器操作的一个示例。

控制器操作必须是控制器类的公共方法。 默认情况下，Visual Basic.NET 方法为公共方法。 请注意，你添加到控制器类的任何公共方法都将自动作为控制器操作公开（必须小心，因为 universe 中的任何人只需在浏览器地址栏中键入正确的 URL 即可调用控制器操作）。

控制器操作必须满足一些额外的要求。 用作控制器操作的方法不能重载。 而且，控制器操作不能是静态方法。 除了这样，你可以将任何方法仅用作控制器操作。

## <a name="understanding-action-results"></a>了解操作结果

控制器操作返回称为*操作结果*的内容。 操作结果是控制器操作为响应浏览器请求而返回的内容。

ASP.NET MVC 框架支持多种类型的操作结果，其中包括：

1. ViewResult-表示 HTML 和标记。
2. EmptyResult-不表示任何结果。
3. RedirectResult-表示重定向到新的 URL。
4. JsonResult-表示可在 AJAX 应用程序中使用的 JavaScript 对象表示法结果。
5. JavaScriptResult-表示 JavaScript 脚本。
6. ContentResult-表示文本结果。
7. FileContentResult-表示可下载的文件（包含二进制内容）。
8. FilePathResult-表示可下载的文件（具有路径）。
9. FileStreamResult-表示可下载的文件（带有文件流）。

所有这些操作结果都从基本 ActionResult 类继承。

在大多数情况下，控制器操作返回 ViewResult。 例如，清单2中的索引控制器操作返回 ViewResult。

**列表 2-Controllers\BookController.vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

当操作返回 ViewResult 时，会将 HTML 返回到浏览器。 清单2中的 Index （）方法会将名为 Index 的视图返回到浏览器。

请注意，清单2中的 Index （）操作不返回 ViewResult （）。 相反，控制器基类的 View （）方法会被调用。 通常不会直接返回操作结果。 相反，你可以调用控制器基类的下列方法之一：

1. 视图-返回 ViewResult 操作结果。
2. 重定向-返回 RedirectResult 操作结果。
3. RedirectToAction-返回 RedirectToRouteResult 操作结果。
4. RedirectToRoute-返回 RedirectToRouteResult 操作结果。
5. Json-返回 JsonResult 操作结果。
6. JavaScriptResult-返回 JavaScriptResult。
7. Content-返回 ContentResult 操作结果。
8. File-返回 FileContentResult、FilePathResult 或 FileStreamResult，具体取决于传递给方法的参数。

因此，如果想要将视图返回到浏览器，请调用 View （）方法。 若要将用户从一个控制器操作重定向到另一个控制器操作，请调用 RedirectToAction （）方法。 例如，"清单 3" 中的 "详细信息" （）操作显示视图或将用户重定向到 Index （）操作，具体取决于 Id 参数是否具有值。

**列表 3-Customercontroller.cs**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

ContentResult 操作结果是特殊的。 你可以使用 ContentResult 操作结果以纯文本形式返回操作结果。 例如，列表4中的 Index （）方法以纯文本而不是 HTML 格式返回一条消息。

**列表 4-Controllers\StatusController.vb**

> StatusController
> 
> 
> System.Web.Mvc.Controller

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

调用 StatusController （）操作时，不会返回视图。 相反，原始文本 "Hello World！" 返回到浏览器。

如果控制器操作返回的结果不是操作结果（例如，日期或整数），结果将自动包装在 ContentResult 中。 例如，当调用列表5中 WorkController 的 Index （）操作时，日期会自动返回为 ContentResult。

**列表 5-WorkController**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

列表5中的 Index （）操作返回 DateTime 对象。 ASP.NET MVC 框架将 DateTime 对象转换为字符串，并自动在 ContentResult 中包装 DateTime 值。 浏览器以纯文本形式接收日期和时间。

## <a name="summary"></a>摘要

本教程的目的是介绍 ASP.NET MVC 控制器、控制器操作和控制器操作结果的概念。 在第一部分中，您学习了如何将新的控制器添加到 ASP.NET MVC 项目。 接下来，已了解控制器的公共方法如何作为控制器操作公开给 universe。 最后，我们讨论了可从控制器操作返回的不同类型的操作结果。 具体而言，我们讨论了如何从控制器操作返回 ViewResult、RedirectToActionResult 和 ContentResult。

> [!div class="step-by-step"]
> [上一页](creating-a-custom-route-constraint-cs.md)
> [下一页](creating-custom-routes-vb.md)
