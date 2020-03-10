---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 向视图母版页传递数据 |Microsoft Docs
author: microsoft
description: 本教程的目的是说明如何将数据从控制器传递到视图母版页。 我们检查两个将数据传递到视图的策略 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9f768f47557adedc43cebfa2c092014bba5842de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485672"
---
# <a name="passing-data-to-view-master-pages-vb"></a>向视图母版页传递数据 (VB)

由[Microsoft](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> 本教程的目的是说明如何将数据从控制器传递到视图母版页。 我们检查两个将数据传递给视图母版页的策略。 首先，我们讨论一种简单的解决方案，该解决方案会导致应用程序难以维护。 接下来，我们将研究一个更好的解决方案，该解决方案需要更多初始工作，但会导致应用程序更易于维护。

## <a name="passing-data-to-view-master-pages"></a>将数据传递给视图母版页

本教程的目的是说明如何将数据从控制器传递到视图母版页。 我们检查两个将数据传递给视图母版页的策略。 首先，我们讨论一种简单的解决方案，该解决方案会导致应用程序难以维护。 接下来，我们将研究一个更好的解决方案，该解决方案需要更多初始工作，但会导致应用程序更易于维护。

### <a name="the-problem"></a>问题

假设要生成一个电影数据库应用程序，并且想要在应用程序的每一页上显示电影类别列表（请参阅图1）。 而且，假设电影类别列表存储在数据库表中。 在这种情况下，可以从数据库中检索类别，并在视图母版页中呈现影片类别列表。

[![在视图母版页中显示电影类别](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**图 01**：在视图母版页中显示电影类别（[单击以查看完全大小的图像](passing-data-to-view-master-pages-vb/_static/image3.png)）

这就是问题所在。 如何在母版页中检索电影类别列表？ 直接在母版页中调用模型类的方法很有吸引力。 换句话说，在母版页中包含用于从数据库检索数据的代码非常有吸引力。 但是，绕过 MVC 控制器访问数据库将会违反与构建 MVC 应用程序的主要优势之一相关的问题。

在 MVC 应用程序中，你希望 mvc 控制器和 MVC 模型之间的所有交互都由 MVC 控制器进行处理。 这种关注点的分离将导致更易于维护、更适应性且可测试的应用程序。

在 MVC 应用程序中，传递给视图的所有数据（包括视图母版页）应由控制器操作传递到视图。 而且，数据应通过利用视图数据来传递。 在本教程的剩余部分中，我将介绍两种将视图数据传递到视图母版页的方法。

### <a name="the-simple-solution"></a>简单的解决方案

让我们从将视图数据从控制器传递到视图母版页的最简单解决方案开始。 最简单的解决方案是在每个控制器操作中传递母版页的视图数据。

请考虑列表1中的控制器。 它公开了两个名为 `Index()` 和 `Details()`的操作。 `Index()` 操作方法返回电影数据库表中的每个电影。 `Details()` 操作方法返回特定电影类别中的每个电影。

**列表1– `Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

请注意，`Index()` 和 `Details()` 操作都添加了两项来查看数据。 `Index()` 操作将添加两个键：类别和影片。 类别键表示 "视图" 母版页显示的电影类别的列表。 电影键表示 "索引视图" 页显示的电影列表。

`Details()` 操作还添加了两个名为 "类别" 和 "电影" 的键。 类别键再次表示视图母版页显示的电影类别的列表。 电影键表示 "详细信息视图" 页显示的特定类别中的电影列表（参见图2）。

[![详细信息视图](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**图 02**：详细信息视图（[单击查看完全尺寸的图像](passing-data-to-view-master-pages-vb/_static/image6.png)）

索引视图包含在列表2中。 它只是在查看数据中循环显示电影项所表示的电影列表。

**列表2– `Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

视图母版页包含在列表3中。 视图母版页从视图数据循环访问并呈现类别项表示的所有电影类别。

**列表 3-`Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

所有数据都通过视图数据传递到视图和 "视图" 母版页。 这是将数据传递到母版页的正确方法。

那么，此解决方案有什么不妥呢？ 问题在于，此解决方案违反了晾干（不要自我重复）原则。 每个控制器操作都必须添加完全相同的电影类别列表以查看数据。 在应用程序中具有重复的代码，使应用程序更加难以维护、改编和修改。

### <a name="the-good-solution"></a>好的解决方案

在本部分中，我们将讨论将数据从控制器操作传递到视图母版页的替代方法和更好的解决方案。 我们不会在每个控制器操作中为母版页添加电影类别，只会将电影类别添加到视图数据一次。 视图母版页使用的所有视图数据都添加到了应用程序控制器中。

ApplicationController 类包含在列表4中。

ApplicationController 类包含在列表4中。

**列表 4-`Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

对于列表4中的应用程序控制器，应注意以下三个方面。 首先，请注意，该类继承自基本 System.web 类。 应用程序控制器是一个控制器类。

其次，请注意，应用程序控制器类是 MustInherit 类。 MustInherit 类是必须由具体类实现的类。 由于应用程序控制器是一个 MustInherit 类，因此不能直接调用在类中定义的任何方法。 如果尝试直接调用应用程序类，则会出现 "找不到资源" 错误消息。

第三，请注意，应用程序控制器包含一个用于添加电影类别列表以查看数据的构造函数。 继承自应用程序控制器的每个控制器类都会自动调用应用程序控制器的构造函数。 无论何时对继承自应用程序控制器的任何控制器调用任何操作，都将自动在视图数据中包含电影类别。

列表5中的电影控制器继承自应用程序控制器。

**列表5– `Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

与上一节中所述的主控制器一样，电影控制器公开了两个名为 `Index()` 和 `Details()`的操作方法。 请注意，视图母版页显示的电影类别列表未添加到 `Index()` 或 `Details()` 方法中的查看数据。 由于影片控制器继承自应用程序控制器，因此会将电影类别列表添加到自动查看数据中。

请注意，用于为视图母版页添加视图数据的此解决方案不违反晾干（不要自我重复）原则。 用于将电影类别列表添加到视图数据的代码仅包含在一个位置：应用程序控制器的构造函数。

### <a name="summary"></a>摘要

在本教程中，我们讨论了将视图数据从控制器传递到视图母版页的两种方法。 首先，我们只是一种简单的方法，但难以维护。 在第一部分中，我们讨论了如何在应用程序的每个控制器操作中为视图母版页添加视图数据。 我们结论，这是一种不好的方法，因为它违反了晾干（不要自我重复）原则。

接下来，我们将讨论一个更好的策略，以便添加视图母版页查看数据所需的数据。 我们只在应用程序控制器中添加了一次视图数据，而不是在每个控制器操作中添加视图数据。 这样，就可以避免在将数据传递到 ASP.NET MVC 应用程序中的视图母版页时出现重复代码。

> [!div class="step-by-step"]
> [上一页](creating-page-layouts-with-view-master-pages-vb.md)
