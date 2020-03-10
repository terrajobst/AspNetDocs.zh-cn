---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 第5部分：业务逻辑 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第5部分添加了一些业务逻辑。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511544"
---
# <a name="part-5-business-logic"></a>第5部分：业务逻辑

作者： [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。 其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。
> 
> 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第5部分添加了一些业务逻辑。

## <a id="_Toc260221671"></a>添加一些业务逻辑

每次访问我们的网站时，我们都希望获得购物体验。 即使用户没有注册或登录，访问者也可以浏览和添加购物车中的商品。 当他们准备好签出时，会向他们提供身份验证选项，以及他们是否还可以创建帐户的成员。

这意味着，我们需要实施逻辑，将购物车从匿名状态转换为 "已注册用户" 状态。

让我们创建一个名为 "类" 的目录，然后右键单击该文件夹，然后创建一个名为 MyShoppingCart.cs 的新 "类" 文件。

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

如前文所述，我们将扩展实现 MyShoppingCart 页的类，并且我们将使用来实现此目的。网络强大的 "分部类" 构造。

MyShoppingCart.aspx.cf 文件的生成调用如下所示。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

请注意 "partial" 关键字的使用。

我们刚刚生成的类文件如下所示。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

我们还会通过向此文件添加 partial 关键字来合并实现。

新类文件现在如下所示。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

我们将向类添加的第一种方法是 "AddItem" 方法。 当用户单击产品列表和产品详细信息页上的 "添加到图片" 链接时，将最终调用此方法。

将以下附加到页面顶部的 using 语句。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

并将此方法添加到 MyShoppingCart 类。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

我们使用 LINQ to Entities 来查看物品是否已在购物车中。 如果是这样，我们将更新该项的订单数量，否则，将为所选项创建一个新项

为了调用此方法，我们将实现一个 AddToCart 页，该页面不仅类此方法，还在添加项后显示当前购物 = 购物车。

在解决方案资源管理器中右键单击解决方案名称，然后添加名为 AddToCart 的新页，如前文所述。

尽管我们可以使用此页来显示中期问题（如低股票问题），但在我们的实现中，该页面不会实际呈现，而是调用 "添加" 逻辑并重定向。

若要实现此目的，我们需要将以下代码添加到页面\_Load 事件。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

请注意，我们正在检索从 QueryString 参数添加到购物车中的产品，并调用我们的类的 AddItem 方法。

假设没有遇到任何错误，则会将控制传递到 SHoppingCart 页，我们将在下一步完成此页。 如果应出现错误，则会引发异常。

当前我们尚未实现全局错误处理程序，因此，我们的应用程序无法处理此异常，我们稍后将对此进行更正。

另请注意，使用语句 Debug。 Fail （）（可通过 `using System.Diagnostics;)`

当应用程序在调试器中运行时，此方法将显示一个详细的对话框，其中包含有关应用程序状态的信息以及我们指定的错误消息。

在生产环境中运行时，将忽略 Debug （）语句。

在上面的代码中，你会注意到，在调用购物车类名称 "GetShoppingCartId" 中的方法。

按如下所示添加代码以实现方法。

请注意，我们还添加了 "更新" 和 "签出" 按钮和一个标签，可在其中显示购物车 "总计"。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

现在，我们可以将物品添加到购物车，但我们尚未实施逻辑来在添加产品后显示购物车。

因此，在 MyShoppingCart 页中，我们将添加一个 EntityDataSource 控件和一个 GridVire 控件，如下所示。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

在设计器中调用窗体，以便您可以双击 "更新购物车" 按钮，然后生成在标记的声明中指定的 click 事件处理程序。

稍后我们将实现详细信息，但这样做将使我们生成并运行应用程序，而不会发生错误。

当你运行应用程序并向购物车中添加物品时，你将看到此内容。

![](tailspin-spyworks-part-5/_static/image2.jpg)

请注意，我们通过实现三个自定义列，遵循了 "默认" 网格显示。

第一个是用于数量的可编辑的 "绑定" 字段：

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

下一列是显示行项总计的 "计算" 列（该项的成本乘以要订购的数量）：

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

最后，我们有一个包含 CheckBox 控件的自定义列，用户将使用该复选框控件指示应从购物图表中删除该项。

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

如您所见，"订单总计" 行为空，因此让我们添加一些逻辑来计算订单总计。

首先，将 "GetTotal" 方法部署到我们的 MyShoppingCart 类。

在 MyShoppingCart.cs 文件中，添加以下代码。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

然后，在页面\_Load 事件处理程序中，我们可以调用 GetTotal 方法。 同时，我们将添加一个测试来查看购物车是否为空，并在其显示时进行相应调整。

现在，如果购物车为空，我们将得到以下内容：

![](tailspin-spyworks-part-5/_static/image4.jpg)

如果不是，我们会看到总数。

![](tailspin-spyworks-part-5/_static/image5.jpg)

但是，此页面尚未完成。

我们将需要额外的逻辑来重新计算购物车，方法是删除标记为要删除的项目，并确定新的数量值，因为用户可能在网格中更改了某些值。

允许在 MyShoppingCart.cs 中将 "RemoveItem" 方法添加到购物车类，以便在用户标记要删除的项时处理案例。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

现在，让我们使用一种方法来处理用户在 GridView 中更改质量时的情况。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

利用基本的 "删除" 和 "更新" 功能，我们可以实现在数据库中实际更新购物车的逻辑。 （在 MyShoppingCart.cs 中）

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

你会注意到，此方法需要两个参数。 一个是购物车 Id，另一个是用户定义类型的对象数组。

因此，为了最大限度地减少对用户界面细节的逻辑的依赖关系，我们定义了一种数据结构，可用于在不需要直接访问 GridView 控件的情况下将购物车项传递到代码。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

在我们的 MyShoppingCart.aspx.cs 文件中，可以在 "更新" 按钮单击事件处理程序中使用此结构，如下所示。 请注意，除更新购物车外，还会更新购物车总计。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

请注意，下面这行代码：

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

GetValues （）是一个特殊的 helper 函数，我们将在 MyShoppingCart.aspx.cs 中实现此功能，如下所示。

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

这提供了一种方法来访问 GridView 控件中的绑定元素的值。 由于我们的 "删除项" 复选框控件未绑定，我们将通过 FindControl （）方法对其进行访问。

在项目开发的此阶段，我们准备好实现结帐过程。

在执行此操作之前，让我们使用 Visual Studio 生成成员资格数据库，并将用户添加到成员资格存储库中。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-4.md)
> [下一页](tailspin-spyworks-part-6.md)
