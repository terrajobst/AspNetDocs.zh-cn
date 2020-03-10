---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: 创建操作（C#） |Microsoft Docs
author: microsoft
description: 了解如何向 ASP.NET MVC 控制器添加新操作。 了解方法为操作的要求。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470198"
---
# <a name="creating-an-action-c"></a>创建操作 (C#)

由[Microsoft](https://github.com/microsoft)

> 了解如何向 ASP.NET MVC 控制器添加新操作。 了解方法为操作的要求。

本教程的目的是介绍如何创建新的控制器操作。 了解操作方法的要求。 你还将了解如何防止方法作为操作公开。

## <a name="adding-an-action-to-a-controller"></a>将操作添加到控制器

通过向控制器添加新方法，将新操作添加到控制器。 例如，列表1中的控制器包含一个名为 Index （）的操作和一个名为 SayHello （）的操作。 这两种方法都公开为操作。

**列表 1-Controllers\HomeController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

若要以操作的形式公开给 universe，方法必须满足某些要求：

- 方法必须是公共的。
- 方法不能是静态方法。
- 方法不能是扩展方法。
- 方法不能为构造函数、getter 或 setter。
- 方法不能有开放式泛型类型。
- 方法不是控制器基类的方法。
- 方法不能包含**ref**或**out**参数。

请注意，控制器操作的返回类型没有限制。 控制器操作可以返回字符串、DateTime、随机类的实例或 void。 ASP.NET MVC 框架将任何不是操作结果的返回类型转换为字符串，并将该字符串转换为浏览器。

当你向控制器添加不违反这些要求的任何方法时，该方法将作为控制器操作公开。 请注意此处。 连接到 Internet 的任何人都可以调用控制器操作。 请不要这样做，例如，创建 DeleteMyWebsite （）控制器操作。

## <a name="preventing-a-public-method-from-being-invoked"></a>阻止调用公共方法

如果需要在控制器类中创建一个公共方法，但不希望将该方法作为控制器操作公开，则可以通过使用 [NonAction] 特性来阻止调用此方法。 例如，清单2中的控制器包含一个名为 CompanySecrets （）的公共方法，该方法用 [NonAction] 特性修饰。

**列表 2-Controllers\WorkController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

如果尝试通过在浏览器的地址栏中键入/Work/CompanySecrets 来调用 CompanySecrets （）控制器操作，则将收到图1所示的错误消息。

[调用 NonAction 方法 ![](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**图 01**：调用 NonAction 方法（[单击以查看完全大小的图像](creating-an-action-cs/_static/image2.png)）

> [!div class="step-by-step"]
> [上一页](creating-a-controller-cs.md)
> [下一页](asp-net-mvc-routing-overview-vb.md)
