---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: 为 ASP.NET MVC 应用程序创建单元测试C#（） |Microsoft Docs
author: StephenWalther
description: 了解如何为控制器操作创建单元测试。 在本教程中，Stephen Walther 演示了如何测试控制器操作是否返回 parti 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506090"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a>为 ASP.NET MVC 应用程序创建单元测试 (C#)

作者： [Stephen Walther](https://github.com/StephenWalther)

[下载 PDF](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> 了解如何为控制器操作创建单元测试。 在本教程中，Stephen Walther 演示了如何测试控制器操作返回特定的视图、返回特定的数据集，还是返回不同类型的操作结果。

本教程的目的是演示如何为 ASP.NET MVC 应用程序中的控制器编写单元测试。 我们介绍如何生成三种不同类型的单元测试。 您将了解如何测试控制器操作返回的视图、如何测试控制器操作返回的视图数据，以及如何测试一个控制器操作是否将您重定向到另一个控制器操作。

## <a name="creating-the-controller-under-test"></a>创建受测控制器

首先，让我们创建要测试的控制器。 名为 `ProductController`的控制器包含在列表1中。

**列表1– `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

`ProductController` 包含两个名为 `Index()` 和 `Details()`的操作方法。 这两个操作方法都返回视图。 请注意，`Details()` 操作接受名为 Id 的参数。

## <a name="testing-the-view-returned-by-a-controller"></a>测试控制器返回的视图

假设我们想要测试 `ProductController` 是否返回正确的视图。 我们想要确保在调用 `ProductController.Details()` 操作时，将返回详细信息视图。 清单2中的测试类包含用于测试 `ProductController.Details()` 操作返回的视图的单元测试。

**列表2– `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

清单2中的类包含一个名为 `TestDetailsView()`的测试方法。 此方法包含三行代码。 第一行代码创建 `ProductController` 类的新实例。 第二行代码调用控制器的 `Details()` 操作方法。 最后，代码的最后一行检查 `Details()` 操作返回的视图是否为详细信息视图。

`ViewResult.ViewName` 属性表示控制器返回的视图的名称。 有关测试此属性的一个严重警告。 控制器可以通过两种方式返回视图。 控制器可以显式返回如下所示的视图：

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

或者，可以从控制器操作的名称（如下所示）推断视图的名称：

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

此控制器操作还会返回一个名为 `Details`的视图。 但是，视图的名称是从操作名称推断出来的。 如果要测试视图名称，则必须从控制器操作显式返回视图名称。

你可以通过以下方式运行 "列表 2" 中的单元测试：输入键盘组合**Ctrl +、** 或单击 "**运行解决方案中的所有测试**" 按钮（参见图1）。 如果测试通过，则会看到图2中的 "测试结果" 窗口。

[![在解决方案中运行所有测试](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

**图 01**：运行解决方案中的所有测试（[单击以查看完全大小的映像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png)）

[![成功！](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

**图 02**： Success！ （[单击以查看完全大小的映像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png)）

## <a name="testing-the-view-data-returned-by-a-controller"></a>测试控制器返回的视图数据

MVC 控制器使用称为 *`View Data`* 的内容将数据传递给视图。 例如，假设你想要在调用 `ProductController Details()` 操作时显示特定产品的详细信息。 在这种情况下，您可以创建 `Product` 类的实例（在模型中定义），并通过利用 `View Data`将该实例传递到 `Details` 视图。

列表3中修改后的 `ProductController` 包含一个返回产品的已更新 `Details()` 操作。

**列表 3-`ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

首先，`Details()` 操作创建 `Product` 类的新实例，该实例表示便携式计算机。 接下来，`Product` 类的实例将作为第二个参数传递到 `View()` 方法。

您可以编写单元测试来测试所需的数据是否包含在查看数据中。 当你调用 `ProductController Details()` 操作方法时，列表4中的单元测试将测试是否返回表示便携式计算机的产品。

**列表 4-`ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

在列表4中，`TestDetailsView()` 方法通过调用 `Details()` 方法来测试返回的视图数据。 `ViewData` 通过调用 `Details()` 方法，作为 `ViewResult` 上的属性公开。 `ViewData.Model` 属性包含传递给该视图的产品。 该测试只是验证视图数据中包含的产品是否具有名称 "便携式计算机"。

## <a name="testing-the-action-result-returned-by-a-controller"></a>测试控制器返回的操作结果

更复杂的控制器操作可能返回不同类型的操作结果，具体取决于传递给控制器操作的参数的值。 控制器操作可以返回各种类型的操作结果，包括 `ViewResult`、`RedirectToRouteResult`或 `JsonResult`。

例如，将有效的产品 Id 传递到操作时，列表5中修改后的 `Details()` 操作返回 `Details` 视图。 如果传递的产品 Id 无效（Id 值小于1，则将重定向到 `Index()` 操作。

**列表5– `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

可以通过清单6中的单元测试测试 `Details()` 操作的行为。 清单6中的单元测试验证在将值为-1 的 Id 传递到 `Details()` 方法时，是否已重定向到 `Index` 视图。

**清单6– `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

当在控制器操作中调用 `RedirectToAction()` 方法时，控制器操作返回一个 `RedirectToRouteResult`。 测试检查 `RedirectToRouteResult` 是否会将用户重定向到名为 `Index`的控制器操作。

## <a name="summary"></a>摘要

在本教程中，您学习了如何生成 MVC 控制器操作的单元测试。 首先，您学习了如何验证控制器操作是否返回了正确的视图。 已了解如何使用 `ViewResult.ViewName` 属性验证视图的名称。

接下来，我们探讨了如何测试 `View Data`的内容。 已了解如何在调用控制器操作后检查是否在 `View Data` 中返回了正确的产品。

最后，我们讨论了如何测试控制器操作是否返回不同类型的操作结果。 了解了如何测试控制器是返回 `ViewResult` 还是 `RedirectToRouteResult`。

> [!div class="step-by-step"]
> [下一部分](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
