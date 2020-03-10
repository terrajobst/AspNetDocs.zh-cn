---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: 第7部分：添加功能 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第7部分添加了其他功能，例如 account 查看 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521564"
---
# <a name="part-7-adding-features"></a>第7部分：添加功能

作者： [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。 其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。
> 
> 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第7部分添加了其他功能，如帐户查看、产品评论和 "常用项" 和 "还已购买" 用户控件。

## <a id="_Toc260221673"></a>添加功能

尽管用户可以浏览我们的目录、将商品放入购物车并完成结帐过程，但我们会提供许多支持功能来改善我们的站点。

1. 帐户检查（列出订单并查看详细信息。）
2. 向首页添加一些特定于上下文的内容。
3. 添加一项功能，让用户查看目录中的产品。
4. 创建用户控件以显示常用项，并将该控件置于首页。
5. 创建 "也购买" 用户控件，并将其添加到产品详细信息页。
6. 添加联系人页。
7. 添加 "关于" 页。
8. 全局错误

## <a id="_Toc260221674"></a>帐户检查

在 "帐户" 文件夹中，创建两个名为 OrderList 的 .aspx 页，另一个名为 OrderDetails

OrderList 将像以前一样，充分利用 GridView 和 EntityDataSource 控件。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

EntityDataSource 从 "订单" 表中选择筛选的 "订单" 表中的记录（请参阅 WhereParameter）。

另请注意 HyperlinkField 中的以下参数：

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

这些参数指定每个产品的订单详细信息视图的链接，并将 "订单 Id" 字段指定为 OrderDetails 页的 QueryString 参数。

## <a id="_Toc260221675"></a>OrderDetails .aspx

我们将使用 EntityDataSource 控件来访问订单，并使用 FormView 显示订单数据，并使用 GridView 的另一个 EntityDataSource 显示订单的行项。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

在代码隐藏文件（OrderDetails.aspx.cs）中，我们有两个小部分的内务处理。

首先，我们需要确保 OrderDetails 始终获取订单 Id。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

还需要计算并显示行项的订单总计。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>主页

让我们在 default.aspx 页中添加一些静态内容。

首先，我将创建一个 "Content" 文件夹，并在其中包含 Images 文件夹（并在主页上包含一个要使用的图像）。

在 "default.aspx" 页的底部占位符中，添加以下标记。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>产品审查

首先，我们将添加一个按钮，其中包含指向表单的链接，可用于输入产品评论。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

请注意，我们将在查询字符串中传递 ProductID

接下来，添加名为 ReviewAdd 的页面

此页将使用 ASP.NET AJAX 控件工具包。 如果尚未执行此操作，请从[DevExpress](http://devexpress.com/act)下载该工具包，并提供有关设置用于 Visual Studio 的工具包的指南[https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)。

在设计模式下，从 "工具箱" 中拖动控件和验证器，然后生成如下所示的窗体。

![](tailspin-spyworks-part-7/_static/image2.jpg)

标记将如下所示。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

现在，我们可以输入评论，我们将在 "产品" 页上显示这些评论。

将此标记添加到 ProductDetails 页。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

现在运行应用程序并导航到产品，显示产品信息（包括客户评审）。

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>常用项控件（创建用户控件）

为了增加网站的销售额，我们将向 "暗示销售" 常见或相关产品添加几个功能。

这些功能中的第一项功能是产品目录中更常用的产品列表。

我们将创建一个 "用户控件"，用于显示应用程序主页上的排名靠前的销售项目。 由于这将是一个控件，因此，只需在 Visual Studio 的设计器中将控件拖放到所喜欢的任何页上即可在任何页面上使用它。

在 Visual Studio 的解决方案资源管理器中，右键单击解决方案名称，然后创建一个名为 "Controls" 的新目录。 虽然这不是必需的，但我们将通过在 "Controls" 目录中创建所有用户控件来帮助保持项目的结构。

右键单击 "controls" 文件夹，然后选择 "新建项"：

![](tailspin-spyworks-part-7/_static/image4.jpg)

为 "PopularItems" 的控件指定名称。 请注意，用户控件的文件扩展名为 .ascx 而不是 .aspx。

我们的常用项目用户控件将按如下方式定义。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

这里，我们使用的是尚未在此应用程序中使用的方法。 我们使用的是 repeater 控件，而不是使用数据源控件将 Repeater 控件绑定到 LINQ to Entities 查询的结果。

在我们的控件后面的代码中，我们按如下所示执行此操作。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

请注意，此重要的行位于控件标记的顶部。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

由于最常用的项每分钟都不会更改，因此我们可以添加 aching 指令来改善应用程序的性能。 此指令将使控件代码仅在控件的缓存输出过期时执行。 否则，将使用控件输出的缓存版本。

现在我们要做的就是将新控件包含在我们的默认 .aspx 页中。

使用拖放将控件的一个实例置于默认窗体的 "打开" 列中。

![](tailspin-spyworks-part-7/_static/image5.jpg)

现在，运行应用程序时，主页会显示最常用的项。

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>"还购买" 控件（带参数的用户控件）

我们要创建的第二个用户控件将通过添加上下文的具体内容来将暗示性销售转到下一级别。

用于计算前面 "也已购买" 项的逻辑是不重要的。

我们的 "还购买" 控制将为当前所选的 ProductID 选择 OrderDetails 记录（以前购买的记录），并为找到的每个唯一顺序获取 OrderIDs。

然后，将从所有订单中选择 "al"，并对购买的数量进行求和。 我们会按此数量进行排序，并显示前5项。

由于此逻辑的复杂性，我们将此算法作为存储过程实现。

存储过程的 T-sql 如下所示。

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

请注意，在我们的应用程序中包含此存储过程（SelectPurchasedWithProducts）后，如果生成实体数据模型，则除了需要的表和视图外，还实体数据模型应包括此存储过程。

若要从实体数据模型访问存储过程，我们需要导入函数。

双击 "解决方案资源管理器" 中的实体数据模型，在设计器中将其打开，然后打开模型浏览器，右键单击设计器并选择 "添加函数导入"。

![](tailspin-spyworks-part-7/_static/image1.png)

这样做会打开此对话框。

![](tailspin-spyworks-part-7/_static/image2.png)

如以上所示填写字段，请选择 "SelectPurchasedWithProducts"，并使用导入函数名称的过程名称。

单击 "确定"。

完成此操作后，就可以对存储过程进行编程，就像我们在模型中的任何其他项一样。

因此，在我们的 "Controls" 文件夹中创建一个名为 AlsoPurchased 的新用户控件。

对于 PopularItems 控件，此控件的标记将非常熟悉。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

显著的区别在于，由于要呈现的项将因产品而异，因此不会缓存输出。

ProductId 将是控件的 "属性"。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

在控件的预呈现事件处理程序中，我们 eed 执行三个操作。

1. 请确保已设置 "ProductID"。
2. 查看是否存在与当前产品一起购买的任何产品。
3. 输出 #2 中确定的一些项。

请注意，通过模型调用存储过程是多么简单。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

确定是否 "也已购买" 后，只需将中继器绑定到查询返回的结果。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

如果没有任何 "也购买" 的项，我们只会从目录中显示其他热门项。

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

若要查看 "还购买" 项，请打开 "ProductDetails" 页，然后从 "解决方案资源管理器" 中拖动 "AlsoPurchased" 控件，使其显示在标记中的此位置。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

这样做将创建对 ProductDetails 页顶部的控件的引用。

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

由于 AlsoPurchased 用户控件需要 ProductId 编号，因此我们将通过对页面的当前数据模型项使用 Eval 语句，来设置控件的 ProductID 属性。

![](tailspin-spyworks-part-7/_static/image3.png)

当我们立即生成并运行并浏览到某一产品时，我们将看到 "也已购买" 项。

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> [上一页](tailspin-spyworks-part-6.md)
> [下一页](tailspin-spyworks-part-8.md)
