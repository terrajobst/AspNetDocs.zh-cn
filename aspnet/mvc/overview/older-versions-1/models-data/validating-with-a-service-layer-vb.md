---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: 使用服务层进行验证（VB） |Microsoft Docs
author: StephenWalther
description: 了解如何将验证逻辑移出控制器操作和单独的服务层。 在本教程中，Stephen Walther 介绍了如何 。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 704657ffe6f50eaf3eb0d91d0d334567003ab7f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436574"
---
# <a name="validating-with-a-service-layer-vb"></a>使用服务层进行验证 (VB)

作者： [Stephen Walther](https://github.com/StephenWalther)

> 了解如何将验证逻辑移出控制器操作和单独的服务层。 在本教程中，Stephen Walther 介绍了如何通过将服务层与控制器层隔离来保持重要的关注点。

本教程的目的是介绍在 ASP.NET MVC 应用程序中执行验证的一种方法。 在本教程中，将了解如何将验证逻辑移出控制器，并将其移到单独的服务层。

## <a name="separating-concerns"></a>分离关注点

生成 ASP.NET MVC 应用程序时，不应将数据库逻辑放在控制器操作中。 混合数据库和控制器逻辑使应用程序在一段时间内更难以维护。 建议将所有数据库逻辑放在单独的存储库层中。

例如，列表1包含一个名为 "化 productrepository" 的简单存储库。 产品存储库包含应用程序的所有数据访问代码。 此列表还包括产品存储库实现的 IProductRepository 接口。

**列表 1-Models\ProductRepository.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

清单2中的控制器在其 Index （）和 Create （）操作中使用存储库层。 请注意，此控制器不包含任何数据库逻辑。 通过创建存储库层，可以保持完全分离的问题。 控制器负责应用程序流控制逻辑，而存储库负责数据访问逻辑。

**列表 2-Controllers\ProductController.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a>创建服务层

因此，应用程序流控制逻辑属于控制器，数据访问逻辑位于存储库中。 在这种情况下，你要将验证逻辑放在哪个位置？ 一种选择是将验证逻辑放在*服务层*中。

服务层是 ASP.NET MVC 应用程序中的一个额外层，用于调节控制器和存储库层之间的通信。 服务层包含业务逻辑。 具体而言，它包含验证逻辑。

例如，清单3中的产品服务层具有一个 CreateProduct （）方法。 CreateProduct （）方法调用 ValidateProduct （）方法，在将产品传递到产品存储库之前验证新产品。

**列表 3-Models\ProductService.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

产品控制器已在清单4中更新，以使用服务层而不是存储库层。 控制器层将与服务层通信。 服务层与存储库层通信。 每个层都有单独的责任。

**列表 4-Controllers\ProductController.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

请注意，产品服务是在产品控制器构造函数中创建的。 创建产品服务时，模型状态字典将传递给服务。 产品服务使用模型状态将验证错误消息传递回控制器。

## <a name="decoupling-the-service-layer"></a>分离服务层

我们无法将控制器层和服务层相互隔离。 控制器和服务层通过模型状态进行通信。 换言之，服务层依赖于 ASP.NET MVC 框架的特定功能。

我们希望尽可能将服务层与控制器层隔离开来。 从理论上讲，我们应该能够将服务层用于任何类型的应用程序，而不仅是一个 ASP.NET MVC 应用程序。 例如，在将来，我们可能要为应用程序生成 WPF 前端。 我们会发现一种从我们的服务层中删除 ASP.NET MVC 模型状态的依赖项的方法。

在列表5中，已更新服务层，使其不再使用模型状态。 相反，它使用实现 IValidationDictionary 接口的任何类。

**列表 5-Models\ProductService.vb （分离）**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

IValidationDictionary 接口在列表6中定义。 此简单接口有一个方法和一个属性。

**列表 6-Models\IValidationDictionary.cs**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

名为 ModelStateWrapper 类的清单7中的类实现 IValidationDictionary 接口。 可以通过将模型状态字典传递到构造函数来实例化 ModelStateWrapper 类。

**列表 7-Models\ModelStateWrapper.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

最后，在其构造函数中创建服务层时，列表8中的更新的控制器使用 ModelStateWrapper。

**列表 8-Controllers\ProductController.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

通过使用 IValidationDictionary 接口和 ModelStateWrapper 类，我们可以将我们的服务层从控制器层中完全隔离开来。 服务层不再依赖于模型状态。 可以将实现 IValidationDictionary 接口的任何类传递到服务层。 例如，WPF 应用程序可使用简单的集合类实现 IValidationDictionary 接口。

## <a name="summary"></a>摘要

本教程的目的是讨论在 ASP.NET MVC 应用程序中执行验证的一种方法。 在本教程中，已学习如何将所有验证逻辑移出控制器并移到单独的服务层。 还了解了如何通过创建 ModelStateWrapper 类将服务层与控制器层隔离开来。

> [!div class="step-by-step"]
> [上一页](validating-with-the-idataerrorinfo-interface-vb.md)
> [下一页](validation-with-the-data-annotation-validators-vb.md)
