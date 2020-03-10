---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 第10部分：导航和站点设计的最终更新，结论 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第10部分涵盖了对导航和的最终更新 。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433610"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>第10部分：导航和站点设计的最终更新，结论

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。  
>   
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第10部分涵盖了对导航和站点设计的最终更新，结论。

我们已经完成了我们网站的所有主要功能，但仍有一些功能要添加到站点导航、主页和商店浏览页面。

## <a name="creating-the-shopping-cart-summary-partial-view"></a>创建购物车摘要分部视图

我们想要在整个站点中公开用户购物车中的项目数。

![](mvc-music-store-part-10/_static/image1.png)

通过创建已添加到我们的站点的分部视图，我们可以轻松地实现此目标。

如上所示，ShoppingCart 控制器包括 CartSummary 操作方法，该方法返回分部视图：

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

若要创建 CartSummary 分部视图，请右键单击 Views/ShoppingCart 文件夹，然后选择 "添加视图"。 将视图命名为 CartSummary，并选中 "创建分部视图" 复选框，如下所示。

![](mvc-music-store-part-10/_static/image2.png)

CartSummary 分部视图非常简单-它只是一个指向 "ShoppingCart" 索引视图的链接，它显示购物车中的项目数。 CartSummary 的完整代码如下所示：

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

通过使用 RenderAction 方法，可以在站点中的任何页面（包括站点主机）中包括分部视图。 RenderAction 要求我们指定操作名称（"CartSummary"）和控制器名称（"ShoppingCart"），如下所示。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

在将此项添加到站点布局之前，我们还将创建流派菜单，以便我们可以将我们的所有网站更新一次。

## <a name="creating-the-genre-menu-partial-view"></a>创建流派菜单分部视图

我们可以通过添加流派菜单来更轻松地在应用商店中导航，其中列出了我们的商店中可用的所有流派。

![](mvc-music-store-part-10/_static/image3.png)

我们将按照相同的步骤创建 GenreMenu 分部视图，然后可以将它们都添加到站点主节点。 首先，将以下 GenreMenu 控制器操作添加到 StoreController：

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

此操作返回将由分部视图显示的流派列表，将在下一步创建。

*注意：我们已将 [ChildActionOnly] 属性添加到此控制器操作，这表示只需从分部视图中使用此操作。此属性将阻止通过浏览到/Store/GenreMenu. 来执行控制器操作这并不是部分视图所必需的，但这是一种很好的做法，因为我们希望确保我们的控制器操作按预期方式使用。我们还会返回 PartialView，而不是 View，这让视图引擎知道，它不应使用此视图的布局，因为它将包含在其他视图中。*

右键单击 "GenreMenu 控制器" 操作，并创建一个名为 GenreMenu 的分部视图，它是使用 "流派视图" 数据类强类型化的，如下所示。

![](mvc-music-store-part-10/_static/image4.png)

更新 GenreMenu 分部视图的视图代码，按如下所示使用未排序的列表显示项。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>正在更新站点布局以显示分部视图

可以通过调用 RenderAction （）将分部视图添加到站点布局（/Views/Shared/\_Layout）。 我们会将它们添加到中，并添加一些其他标记以显示这些内容，如下所示：

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

现在，运行应用程序时，会在左侧导航区域中看到 "流派"，并在顶部看到 "购物车摘要"。

## <a name="update-to-the-store-browse-page"></a>更新到存储浏览页

存储浏览页运行正常，但看起来不太好。 通过更新视图代码（在/Views/Store/Browse.cshtml 中找到），我们可以更新页面以更好地布局显示唱片集，如下所示：

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

这里我们将使用 Url，而不是 Html.actionlink，以便我们可以将特殊格式应用于链接以包含唱片集作品。

*注意：我们将为这些专辑显示一般的唱片集封面。此信息存储在数据库中，可通过商店管理器进行编辑。欢迎添加自己的图稿。*

现在，浏览到某一流派后，会看到包含唱片集图稿的网格中显示的唱片集。

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>更新主页以显示顶级销售专辑

我们想要在主页上提供我们最畅销的销售专辑，以增加销售。 我们将对我们的 HomeController 进行一些更新，以便进行处理，并添加一些其他图形。

首先，我们将向唱片集类添加一个导航属性，以便 EntityFramework 知道它们已关联。 我们的**唱片集**类的最后几行现在应如下所示：

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*注意：这将要求添加 using 语句以引入 System.object 命名空间。*

首先，我们将使用语句添加 storeDB 字段和 MvcMusicStore，如其他控制器中所述。 接下来，我们将以下方法添加到 HomeController，该方法查询数据库以根据 OrderDetails 查找顶级销售唱集。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

这是一种私有方法，因为我们不希望将其作为控制器操作来使用。 为了简单起见，我们将它包含在 HomeController 中，但建议你根据需要将业务逻辑移到不同的服务类中。

接下来，我们可以更新索引控制器操作以查询前5个销售专辑，并将其返回到视图中。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

已更新的 HomeController 的完整代码如下所示。

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

最后，我们需要更新 "主页索引" 视图，使其可以通过更新模型类型并将 "唱片集" 列表添加到底部来显示唱片集列表。 我们还将利用此机会向页面添加标题和促销部分。

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

现在，运行应用程序时，我们将看到更新的主页，其中包含顶级销售专辑和促销消息。

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>结束语

我们已了解到，ASP.NET MVC 使你可以轻松地创建具有数据库访问权限、成员资格、AJAX 等的复杂网站。 速度非常快。 希望本教程提供了开始构建自己的 ASP.NET MVC 应用程序所需的工具！

> [!div class="step-by-step"]
> [上一页](mvc-music-store-part-9.md)
