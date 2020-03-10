---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 第8部分：购物车和 Ajax 更新 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第8部分涵盖了包含 Ajax 更新的购物车。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433514"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a>第8部分：带有 Ajax 更新的购物车

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。  
>   
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第8部分涵盖了包含 Ajax 更新的购物车。

我们将允许用户在购物车中放入唱片集而无需注册，但他们需要注册为来宾才能完成签出。 购物和结帐过程将分为两个控制器：一个 ShoppingCart 控制器，允许匿名向购物车添加项，并使用签出控制器来处理结帐过程。 我们将从本部分中的购物车开始，然后在下一节中构建结帐过程。

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a>添加 Cart、Order 和 OrderDetail 模型类

购物车和结帐过程将利用一些新的类。 右键单击 "模型" 文件夹，然后使用以下代码添加 Cart 类（Cart.cs）。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

此类非常类似于我们目前使用过的其他类，但 RecordId 属性的 [Key] 属性除外。 购物车项将具有名为 CartID 的字符串标识符，以允许进行匿名购物，但该表包含名为 RecordId 的整数主键。 按照约定，实体框架代码优先要求名为 "Cart" 的表的主键为 CartId 或 ID，但我们可以根据需要通过注释或代码轻松覆盖。 下面的示例演示了如何在代码中使用简单的约定，在这种情况下，我们不会对其进行实体框架。

接下来，使用以下代码添加订单类（Order.cs）。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

此类跟踪订单的摘要和传递信息。 **它尚不会进行编译**，因为它有一个 OrderDetails 导航属性，该属性依赖于我们尚未创建的类。 现在，通过添加一个名为 OrderDetail.cs 的类，添加以下代码来解决此问题。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

我们将对我们的 MusicStoreEntities 类进行最后一次更新，以包括公开这些新模型类的 Dbset，其中包括 DbSet&lt;艺术家&gt;。 已更新的 MusicStoreEntities 类显示如下。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a>管理购物车业务逻辑

接下来，我们将在 "模型" 文件夹中创建 ShoppingCart 类。 ShoppingCart 模型处理对 Cart 表的数据访问。 此外，它还将处理用于在购物车中添加和删除项目的业务逻辑。

由于我们不想要求用户只注册某个帐户来向其购物车添加商品，因此，我们会在访问购物车时为用户分配一个临时唯一标识符（使用 GUID 或全局唯一标识符）。 我们将使用 ASP.NET Session 类存储此 ID。

*注意： ASP.NET 会话是存储用户特定信息（在离开站点后过期）的便利位置。虽然会话状态的滥用可能会对较大的站点产生性能影响，但我们的轻型用途非常适合用于演示目的。*

ShoppingCart 类公开以下方法：

**AddToCart**采用唱片集作为参数，并将其添加到用户的购物车。 由于 Cart 表跟踪每个唱片集的数量，因此，它包括在需要时创建新行的逻辑，或者只是在用户已订购唱片集的一个副本时增加数量。

**RemoveFromCart**采用唱片集 ID 并将其从用户购物车中删除。 如果用户的购物车中只包含唱片集的一个副本，则删除该行。

**EmptyCart**删除用户购物车中的所有项目。

**GetCartItems**检索用于显示或处理的 CartItems 的列表。

**GetCount**检索用户在其购物车中拥有的唱集总数。

**GetTotal**计算购物车中所有物品的总成本。

在结帐阶段， **CreateOrder**将购物车转换为订单。

**GetCart**是一种静态方法，它允许我们的控制器获取购物车对象。 它使用**GetCartId**方法来处理从用户的会话读取 CartId。 GetCartId 方法需要 HttpContextBase，以便它能够从用户的会话中读取用户的 CartId。

下面是完整的**ShoppingCart 类**：

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a>ViewModels

购物车控制器需要将一些复杂信息传达给其视图，而不会完全映射到模型对象。 我们不想修改模型以适合我们的视图;Model 类应代表我们的域，而不是用户界面。 一种解决方案是使用 ViewBag 类将信息传递到我们的视图，就像我们对商店经理下拉列表信息进行的一样，但通过 ViewBag 传递大量信息变得难以管理。

此方法的解决方案是使用*ViewModel*模式。 使用此模式时，我们将创建针对特定视图方案进行了优化的强类型类，并公开了视图模板所需的动态值/内容的属性。 然后，控制器类可以填充这些视图优化类并将其传递给视图模板以供使用。 这会在视图模板中启用类型安全、编译时检查和编辑器 IntelliSense。

我们将创建两个用于购物车控制器的视图模型： ShoppingCartViewModel 将保存用户购物车的内容，而 ShoppingCartRemoveViewModel 将用于显示用户删除内容时的确认信息购物车。

让我们在项目的根目录中创建一个新的 Viewmodel 文件夹，使其保持井然有序。 右键单击该项目，选择 "添加/新建文件夹"。

![](mvc-music-store-part-8/_static/image1.jpg)

将文件夹命名为 Viewmodel。

![](mvc-music-store-part-8/_static/image1.png)

接下来，将 ShoppingCartViewModel 类添加到 Viewmodel 文件夹。 它有两个属性：购物车项列表，以及用于保存购物车中所有物品总价的小数值。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

现在，请将 ShoppingCartRemoveViewModel 添加到 Viewmodel 文件夹，其中包含以下四个属性。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a>购物车控制器

购物车控制器有三个主要用途：将商品添加到购物车、从购物车中删除物品以及查看购物车中的物品。 它将使用我们刚刚创建的三个类： ShoppingCartViewModel、ShoppingCartRemoveViewModel 和 ShoppingCart。 如 StoreController 和 StoreManagerController 中所示，我们将添加一个字段来保存 MusicStoreEntities 的实例。

使用空的控制器模板将新的购物车控制器添加到项目。

![](mvc-music-store-part-8/_static/image2.png)

下面是完整的 ShoppingCart 控制器。 索引和添加控制器操作应该非常熟悉。 "删除" 和 "CartSummary 控制器" 操作处理两种特殊情况，我们将在下一节将对此进行讨论。

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a>通过 jQuery 进行 Ajax 更新

接下来，我们将创建一个强类型化为 ShoppingCartViewModel 的购物车索引页，并使用与以前相同的方法的列表视图模板。

![](mvc-music-store-part-8/_static/image3.png)

但是，我们将使用 jQuery 为此视图中具有 HTML 类 RemoveLink 的所有链接 "向上绑定" 单击事件，而不是使用 Html.actionlink 从购物车中删除项目。 此单击事件处理程序不会发布窗体，而只是对 RemoveFromCart 控制器操作进行 AJAX 回调。 RemoveFromCart 返回 JSON 序列化的结果，我们的 jQuery 回调随后使用 jQuery 分析并执行对页面的四次快速更新：

- 1. 从列表中删除已删除的唱片集
- 2. 更新页眉中的购物车计数
- 3. 向用户显示更新消息
- 4. 更新购物车总价

由于删除方案是在索引视图中由 Ajax 回调处理的，因此我们不需要 RemoveFromCart 操作的其他视图。 下面是/ShoppingCart/Index 视图的完整代码：

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

为了进行测试，我们需要将商品添加到购物车中。 我们将更新**应用商店详细信息**视图，以包含 "添加到购物车" 按钮。 在此过程中，我们可以包含自上次更新此视图以来添加的某些唱片集附加信息：流派、艺术家、价格和唱片集画面。 此时将显示更新的商店详细信息视图代码，如下所示。

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

现在，我们可以单击整个商店，并测试在购物车中添加和删除唱片集。 运行应用程序并浏览到存储索引。

![](mvc-music-store-part-8/_static/image4.png)

接下来，单击某一流派以查看唱片集列表。

![](mvc-music-store-part-8/_static/image5.png)

单击唱片集标题现在将显示更新的 "唱片集详细信息" 视图，包括 "添加到购物车" 按钮。

![](mvc-music-store-part-8/_static/image6.png)

单击 "添加到购物车" 按钮将显示购物车摘要列表中的购物车索引视图。

![](mvc-music-store-part-8/_static/image7.png)

在加载购物车后，可以单击 "从购物车中删除" 链接，查看购物车的 Ajax 更新。

![](mvc-music-store-part-8/_static/image8.png)

我们构建了一个工作购物车，允许未注册的用户将物品添加到购物车。 在下一部分中，我们将允许他们注册并完成签出过程。

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-7.md)
> [下一页](mvc-music-store-part-9.md)
