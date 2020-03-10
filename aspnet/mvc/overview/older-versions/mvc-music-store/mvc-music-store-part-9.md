---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 第9部分：注册和签出 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第9部分涵盖注册和签出。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450896"
---
# <a name="part-9-registration-and-checkout"></a>第9部分：注册和签出

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。  
>   
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第9部分涵盖注册和签出。

在本部分中，我们将创建一个 CheckoutController，它将收集购物者的地址和付款信息。 我们会要求用户在签出之前向我们的站点注册，因此此控制器需要授权。

用户通过单击 "结帐" 按钮，导航到其购物车中的结帐过程。

![](mvc-music-store-part-9/_static/image1.jpg)

如果用户未登录，系统会提示用户登录。

![](mvc-music-store-part-9/_static/image1.png)

成功登录后，用户将显示在 "地址" 和 "付款" 视图中。

![](mvc-music-store-part-9/_static/image2.png)

一旦用户填写了窗体并提交了订单后，它们就会显示在 "订单确认" 屏幕中。

![](mvc-music-store-part-9/_static/image3.png)

如果尝试查看不存在的订单或不属于您的订单，则将显示 "错误" 视图。

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a>迁移购物车

尽管购物过程是匿名的，但当用户单击 "签出" 按钮时，他们将需要注册并登录。 用户将希望在访问之间维护购物车信息，因此，在他们完成注册或登录时，我们需要将购物车信息与用户关联。

这实际上非常简单，因为我们的 ShoppingCart 类已经有了一个方法，该方法将当前购物车中的所有项与用户名相关联。 当用户完成注册或登录时，只需调用此方法。

打开我们设置成员身份和授权时添加的**AccountController**类。 添加一个引用 MvcMusicStore 的 using 语句，然后添加以下 MigrateShoppingCart 方法：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

接下来，请修改登录后操作，以便在验证用户后调用 MigrateShoppingCart，如下所示：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

成功创建用户帐户后，立即对注册 post 操作进行相同的更改：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

这就是，在成功注册或登录时，匿名购物车会自动转移到用户帐户。

## <a name="creating-the-checkoutcontroller"></a>创建 CheckoutController

右键单击 "控制器" 文件夹，并使用空的控制器模板将新的控制器添加到名为 CheckoutController 的项目。

![](mvc-music-store-part-9/_static/image5.png)

首先，将授权属性添加到控制器类声明之上，要求用户在签出之前注册：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

*注意：这与之前对 StoreManagerController 进行的更改类似，但在这种情况下，授权属性要求用户是管理员角色。在签出控制器中，我们要求用户登录，但不要求用户是管理员。*

为了简单起见，我们不会在本教程中处理支付信息。 相反，我们允许用户使用促销代码签出。 我们将使用名为 PromoCode 的常量存储此促销代码。

与在 StoreController 中一样，我们将声明一个字段来保存名为 storeDB 的 MusicStoreEntities 类的实例。 若要使用 MusicStoreEntities 类，我们需要为 MvcMusicStore 命名空间添加 using 语句。 我们的结帐控制器顶部显示在下方。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

CheckoutController 将具有以下控制器操作：

**AddressAndPayment （GET 方法）** 将显示允许用户输入其信息的窗体。

**AddressAndPayment （POST 方法）** 将验证输入并处理顺序。

**完成**后将在用户成功完成签出过程后显示。 此视图将包含用户的订单号，如 "确认"。

首先，让我们将索引控制器操作（在我们创建控制器时生成的）重命名为 AddressAndPayment。 此控制器操作只显示结帐窗体，因此不需要任何模型信息。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

我们的 AddressAndPayment POST 方法将遵循我们在 StoreManagerController 中使用的同一模式：它将尝试接受窗体提交并完成订单，并将在窗体失败时重新显示该窗体。

验证窗体输入满足对订单的验证要求后，将直接检查 PromoCode 窗体值。 假设一切正常，我们将按订单保存更新后的信息，告诉 ShoppingCart 对象完成订单过程，然后重定向到完整的操作。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

在成功完成签出过程后，用户将被重定向到 "完成" 控制器操作。 此操作将执行一个简单的检查，用于验证在将订单号显示为确认之前，该订单确实属于已登录用户。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

*注意：当我们开始项目时，会在/Views/Shared 文件夹中自动创建错误视图。*

完整的 CheckoutController 代码如下所示：

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a>添加 AddressAndPayment 视图

现在，让我们创建 AddressAndPayment 视图。 右键单击其中一个 AddressAndPayment 控制器操作，并添加一个名为 AddressAndPayment 的视图，该视图的类型为 "按顺序强类型" 并使用 "编辑模板"，如下所示。

![](mvc-music-store-part-9/_static/image6.png)

此视图将使用我们在生成 StoreManagerEdit 视图时查看的两种技术：

- 我们将使用 EditorForModel （）显示订单模型的窗体字段
- 我们将使用具有验证特性的 Order 类的验证规则

首先，我们将更新窗体代码以使用 EditorForModel （），后跟促销代码的一个文本框。 AddressAndPayment 视图的完整代码如下所示。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a>为订单定义验证规则

现在，我们已设置了视图，我们将为订单模型设置验证规则，就像我们先前针对唱片集模型进行的一样。 右键单击 "模型" 文件夹，然后添加一个名为 Order 的类。 除了之前用于唱片集的验证属性，我们还将使用正则表达式来验证用户的电子邮件地址。

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

如果尝试提交缺少或无效信息的窗体，现在将使用客户端验证显示错误消息。

![](mvc-music-store-part-9/_static/image7.png)

好了，我们已完成了结帐过程的大部分硬性工作;我们只会有几个机会，最后结束。 我们需要添加两个简单的视图，在登录过程中，我们需要负责交付购物车信息。

## <a name="adding-the-checkout-complete-view"></a>添加结帐完成视图

"结帐完成" 视图非常简单，因为它只需显示订单 ID。 右键单击 "完成控制器" 操作并添加一个名为 Complete 的视图，该视图的类型为 int。

![](mvc-music-store-part-9/_static/image8.png)

现在，我们将更新视图代码以显示订单 ID，如下所示。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a>正在更新错误视图

默认模板在 "共享视图" 文件夹中包含错误视图，以便可以将其重新用于站点中的其他位置。 此错误视图包含一个非常简单的错误，不会使用我们的站点布局，因此我们将对其进行更新。

由于这是一个一般错误页面，因此内容非常简单。 如果用户想要重新尝试操作，我们将包含一条消息和一个导航到历史记录中的上一页的链接。

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-8.md)
> [下一页](mvc-music-store-part-10.md)
