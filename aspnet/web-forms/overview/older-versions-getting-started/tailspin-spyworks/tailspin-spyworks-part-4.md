---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 第4部分：列出产品 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第4部分介绍了如何通过 GridView contr 来列出产品 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457280"
---
# <a name="part-4-listing-products"></a>第4部分：列出产品

作者： [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。 其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。
> 
> 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第4部分介绍了如何通过 GridView 控件列出产品。

## <a id="_Toc260221670"></a>用 GridView 控件列出产品

让我们开始实现 ProductsList 页，方法是在解决方案中单击 "右键单击"，并选择 "添加" 和 "新建项"。

![](tailspin-spyworks-part-4/_static/image1.jpg)

选择 "使用母版页的 Web 窗体" 并输入页面名称 "ProductsList"。

单击 "添加"。

![](tailspin-spyworks-part-4/_static/image2.jpg)

接下来，选择放置网站的 "样式" 文件夹，并从 "文件夹的内容" 窗口中选择它。

![](tailspin-spyworks-part-4/_static/image3.jpg)

单击 "确定" 以创建页面。

我们的数据库中填充了产品数据，如下所示。

![](tailspin-spyworks-part-4/_static/image4.jpg)

创建页面后，我们将再次使用实体数据源来访问该产品数据，但在此示例中，我们需要选择产品实体，并且我们需要将返回的项限制为仅返回所选类别的项。

为实现此目的，我们会告知 EntityDataSource 自动生成 WHERE 子句，并指定 WhereParameter。

你会想起，在我们的 "产品类别菜单" 中创建菜单项时，我们会动态生成链接，方法是将 "类别 Id" 添加到每个链接的 QueryString。 我们会告知实体数据源从该查询字符串参数派生 WHERE 参数。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

接下来，我们将配置 ListView 控件以显示产品列表。 若要创建最佳的购物体验，我们将压缩 ListVew 中显示的每个单独产品的几个简明功能。

- 产品名称将是产品详细信息视图的链接。
- 将显示产品的价格。
- 将显示产品的图像，我们将在应用程序的目录图像目录中动态选择映像。
- 我们将包含一个链接，以立即将特定产品添加到购物车。

下面是 ListView 控件实例的标记。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

我们为每个显示的产品动态构建多个链接。

此外，在测试自己的新页面之前，我们需要为产品目录映像创建目录结构，如下所示。

![](tailspin-spyworks-part-4/_static/image1.png)

可访问产品映像后，可以测试产品列表页面。

![](tailspin-spyworks-part-4/_static/image5.jpg)

在站点的 "主页" 页上，单击其中一个 "类别列表" 链接。

![](tailspin-spyworks-part-4/_static/image6.jpg)

现在，我们需要实现 ProductDetails 页和 AddToCart 功能。

如前文所述，使用 "文件-&gt;New" 创建一个使用站点母版页的页名称 ProductDetails。

我们将再次使用 EntityDataSource 控件来访问数据库中的特定产品记录，我们将使用 ASP.NET FormView 控件按如下所示显示产品数据。

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

如果格式看起来有点有趣，请不要担心。 上面的标记为我们稍后将实现的几项功能留出了显示布局的空间。

购物车会在应用程序中表示更复杂的逻辑。 若要开始使用，请使用文件&gt;新建来创建名为 MyShoppingCart 的页。

请注意，我们不会选择名称 ShoppingCart。

数据库中包含名为 "ShoppingCart" 的表。 生成实体数据模型为数据库中的每个表创建了一个类。 因此，实体数据模型生成了一个名为 "ShoppingCart" 的实体类。 我们可以编辑模型，以便我们可以将该名称用于购物车实现，或在需要时扩展它，但我们将选择只选择一个名称来避免冲突。

还值得注意的是，我们将创建一个简单的购物车，并使用购物车显示来嵌入购物车逻辑。 我们还可以选择在完全不同的业务层中实施购物车。

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-3.md)
> [下一页](tailspin-spyworks-part-5.md)
