---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
title: 具有两个 DropDownLists （VB）的主/详细信息筛选 |Microsoft Docs
author: rick-anderson
description: 本教程将大纲/细节关系扩展为添加第三层，使用两个 DropDownList 控件选择所需的父级和祖父录制 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11ae4f64-01ba-4823-95f4-a2fe1f84f7d7
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-vb
msc.type: authoredcontent
ms.openlocfilehash: 166d6a7664a326361dc2a3f115eddb988cd39d20
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424292"
---
# <a name="masterdetail-filtering-with-two-dropdownlists-vb"></a>使用两个 DropDownList 实现母版/详细信息筛选 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_8_VB.exe)或[下载 PDF](master-detail-filtering-with-two-dropdownlists-vb/_static/datatutorial08vb1.pdf)

> 本教程将使用两个 DropDownList 控件来选择所需的父记录和祖父记录，从而将大纲/细节关系扩展为添加第三层。

## <a name="introduction"></a>简介

在[上一教程](master-detail-filtering-with-a-dropdownlist-vb.md)中，我们已介绍了如何使用 DropDownList 填充的单个单独的 "主/详细信息" 报表，该报表显示属于所选类别的产品。 此报表模式适用于显示具有一对多关系的记录，并且可以轻松扩展以适用于包含多个一对多关系的方案。 例如，订单输入系统具有与客户、订单和订单行项相对应的表。 给定的客户可能有多个订单，其中每个订单都包含多个项。 此类数据可以通过两个 DropDownLists 和一个 GridView 向用户提供。 第一个 DropDownList 对于数据库中的每个客户都有一个列表项，其中第二个内容是所选客户的订单。 GridView 会列出所选订单中的行项。

尽管 Northwind 数据库在其 `Customers`、`Orders`和 `Order Details` 表中包含规范的客户/订单/订单详细信息，但这些表不会在我们的体系结构中捕获。 尽管如此，我们仍然可以使用两个依赖 DropDownLists 进行说明。 第一个 DropDownList 将列出属于所选类别的产品类别和第二个产品。 然后，DetailsView 会列出所选产品的详细信息。

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>步骤1：创建和填充类别 DropDownList

第一个目标是添加列出类别的 DropDownList。 上述教程中详细介绍了这些步骤，但此处汇总了这些步骤。

打开 `Filtering` 文件夹中的 "`MasterDetailsDetails.aspx`" 页，将 DropDownList 添加到页面上，将其 `ID` 属性设置为 "`Categories`"，然后在其智能标记中单击 "配置数据源" 链接。 从 "数据源配置向导" 中选择 "添加新数据源"。

[![为 DropDownList 添加新的数据源](master-detail-filtering-with-two-dropdownlists-vb/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image1.png)

**图 1**：为 DropDownList 添加新的数据源（[单击查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image3.png)）

新数据源自然应为 ObjectDataSource。 将此新 ObjectDataSource `CategoriesDataSource` 命名，并让它调用 `CategoriesBLL` 对象的 `GetCategories()` 方法。

[![选择使用 CategoriesBLL 类](master-detail-filtering-with-two-dropdownlists-vb/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image4.png)

**图 2**：选择使用 `CategoriesBLL` 类（[单击以查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image6.png)）

[![将 ObjectDataSource 配置为使用 GetCategories （）方法](master-detail-filtering-with-two-dropdownlists-vb/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image7.png)

**图 3**：将 ObjectDataSource 配置为使用 `GetCategories()` 方法（[单击查看完全大小的映像](master-detail-filtering-with-two-dropdownlists-vb/_static/image9.png)）

配置 ObjectDataSource 后，我们仍然需要指定应在 `Categories` DropDownList 中显示的数据源字段，以及应将哪个数据源字段配置为列表项的值。 将 `CategoryName` 字段设置为显示，并将 `CategoryID` 为每个列表项的值。

[![DropDownList 显示 "类别名称" 字段，并使用 "类别 Id" 作为值](master-detail-filtering-with-two-dropdownlists-vb/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image10.png)

**图 4**：使 DropDownList 显示 "`CategoryName`" 字段并使用 "`CategoryID`" 作为值（[单击以查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image12.png)）

此时，我们已使用 `Categories` 表中的记录填充了 DropDownList 控件（`Categories`）。 当用户从 DropDownList 中选择一个新类别时，我们希望发生回发以便刷新要在步骤2中创建的产品 DropDownList。 因此，请从 `categories` DropDownList 的智能标记中选中 "启用 AutoPostBack" 选项。

[![为类别 DropDownList 启用 AutoPostBack](master-detail-filtering-with-two-dropdownlists-vb/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image13.png)

**图 5**：为 `Categories` DropDownList 启用 AutoPostBack （[单击查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image15.png)）

## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>步骤2：在第二个 DropDownList 中显示所选类别的产品

完成 `Categories` DropDownList 后，下一步是显示属于所选类别的产品的 DropDownList。 若要实现此目的，请将另一个 DropDownList 添加到名为 `ProductsByCategory`的页面。 与 `Categories` DropDownList 一样，为名为 `ProductsByCategoryDataSource``ProductsByCategory` DropDownList 创建新的 ObjectDataSource。

[![为 ProductsByCategory DropDownList 添加新的数据源](master-detail-filtering-with-two-dropdownlists-vb/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image16.png)

**图 6**：为 `ProductsByCategory` DropDownList 添加新数据源（[单击查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image18.png)）

[![创建一个名为 ProductsByCategoryDataSource 的新 ObjectDataSource](master-detail-filtering-with-two-dropdownlists-vb/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image19.png)

**图 7**：创建名为 `ProductsByCategoryDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](master-detail-filtering-with-two-dropdownlists-vb/_static/image21.png)）

由于 `ProductsByCategory` DropDownList 只需要显示属于所选类别的产品，因此，ObjectDataSource 从 `ProductsBLL` 对象调用 `GetProductsByCategoryID(categoryID)` 方法。

[![选择使用 ProductsBLL 类](master-detail-filtering-with-two-dropdownlists-vb/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image22.png)

**图 8**：选择使用 `ProductsBLL` 类（[单击以查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image24.png)）

[![将 ObjectDataSource 配置为使用 GetProductsByCategoryID （类别 Id）方法](master-detail-filtering-with-two-dropdownlists-vb/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image25.png)

**图 9**：将 ObjectDataSource 配置为使用 `GetProductsByCategoryID(categoryID)` 方法（[单击查看完全大小的映像](master-detail-filtering-with-two-dropdownlists-vb/_static/image27.png)）

在向导的最后一步中，需要指定 *`categoryID`* 参数的值。 将此参数从 `Categories` DropDownList 中的选定项分配。

[![从类别 DropDownList 中提取类别 Id 参数值](master-detail-filtering-with-two-dropdownlists-vb/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image28.png)

**图 10**：从 `Categories` DropDownList 拉取 *`categoryID`* 参数值（[单击以查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image30.png)）

配置 ObjectDataSource 后，剩下的就是指定哪些数据源字段用于显示和 DropDownList 的项的值。 显示 "`ProductName`" 字段，并使用 "`ProductID`" 字段作为值。

[![指定用于 DropDownList 的 ListItems 文本和值属性的数据源字段](master-detail-filtering-with-two-dropdownlists-vb/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image31.png)

**图 11**：指定用于 DropDownList 的 `ListItem` s "`Text` 和 `Value` 属性的数据源字段（[单击以查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image33.png)）

在 ObjectDataSource 和 `ProductsByCategory` DropDownList 配置的情况下，我们的页面将显示两个 DropDownLists：第一个将列出所有类别，而第二个则列出属于所选类别的产品。 当用户从第一个 DropDownList 选择一个新类别时，回发将不幸，第二个 DropDownList 将重新绑定，并显示属于新选定类别的产品。 图12和13显示了通过浏览器查看时 `MasterDetailsDetails.aspx` 的操作。

[![首次访问页面时，"饮料" 类别处于选中状态](master-detail-filtering-with-two-dropdownlists-vb/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image34.png)

**图 12**：首次访问页面时，"饮料" 类别处于选中状态（[单击以查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image36.png)）

[选择其他类别 ![显示新类别的产品](master-detail-filtering-with-two-dropdownlists-vb/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image37.png)

**图 13**：选择其他类别将显示新类别的产品（[单击以查看完全尺寸的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image39.png)）

当前，在更改时，`productsByCategory` DropDownList*不*会导致回发。 但是，我们希望在添加 DetailsView 以显示选定产品的详细信息时，才会发生回发（步骤3）。 因此，请从 `productsByCategory` DropDownList 的智能标记中选中 "启用 AutoPostBack" 复选框。

[![为 productsByCategory DropDownList 启用 AutoPostBack 功能](master-detail-filtering-with-two-dropdownlists-vb/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image40.png)

**图 14**：为 `productsByCategory` DropDownList 启用 AutoPostBack 功能（[单击查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image42.png)）

## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>步骤3：使用 DetailsView 显示选定产品的详细信息

最后一步是在 DetailsView 中显示所选产品的详细信息。 若要实现此目的，请将 DetailsView 添加到页面，将其 `ID` 属性设置为 `ProductDetails`，并为其创建新的 ObjectDataSource。 将此 ObjectDataSource 配置为使用 `ProductsBLL` 类的 `GetProductByProductID(productID)` 方法中的数据，并为 *`productID`* 参数的值使用 `ProductsByCategory` DropDownList 的所选值。

[![选择使用 ProductsBLL 类](master-detail-filtering-with-two-dropdownlists-vb/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image43.png)

**图 15**：选择使用 `ProductsBLL` 类（[单击以查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image45.png)）

[![将 ObjectDataSource 配置为使用 GetProductByProductID （productID）方法](master-detail-filtering-with-two-dropdownlists-vb/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image46.png)

**图 16**：将 ObjectDataSource 配置为使用 `GetProductByProductID(productID)` 方法（[单击查看完全大小的映像](master-detail-filtering-with-two-dropdownlists-vb/_static/image48.png)）

[![从 ProductsByCategory DropDownList 提取 productID 参数值](master-detail-filtering-with-two-dropdownlists-vb/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image49.png)

**图 17**：从 `ProductsByCategory` DropDownList 拉取 *`productID`* 参数值（[单击以查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image51.png)）

您可以选择在 `ProductDetails` DetailsView 中显示任何可用字段。 我已经选择删除 `ProductID`、`SupplierID`和 `CategoryID` 字段，并对剩余字段重新排序并设置其格式。 此外，我还清除了 DetailsView 的 `Height` 和 `Width` 属性，从而允许 DetailsView 扩展到最佳显示其数据所需的宽度，而不是将其限制为指定的大小。 完整标记如下所示：

[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample1.aspx)]

请花点时间在浏览器中试用 `MasterDetailsDetails.aspx` 页面。 乍一看，一切都可以正常工作，但有一个微妙的问题。 选择新类别时，`ProductsByCategory` DropDownList 将更新为包含所选类别的产品，但 `ProductDetails` DetailsView 继续显示以前的产品信息。 为所选类别选择不同的产品时，将更新 DetailsView。 此外，如果你完全测试，你会发现，如果你连续选择新的类别（例如从 `Categories` DropDownList 中选择饮料，然后调味品，然后 Confections），其他类别选择将导致刷新 `ProductDetails` DetailsView。

为了帮助解决此问题，让我们看一个具体的示例。具体化 首次访问该页面时，将选择 "饮料" 类别，并在 `ProductsByCategory` DropDownList 中加载相关产品。 Chai 是所选产品，其详细信息显示在 `ProductDetails` DetailsView，如图18所示。

[![在 DetailsView 中显示所选产品的详细信息](master-detail-filtering-with-two-dropdownlists-vb/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image52.png)

**图 18**：选择的产品的详细信息显示在 DetailsView （[单击查看全尺寸图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image54.png)）

如果将类别选择从 "饮料" 更改为调味品，则会发生回发并相应地更新 `ProductsByCategory` DropDownList，但 DetailsView 仍显示 Chai 的详细信息。

[![仍然显示以前选择的产品的详细信息](master-detail-filtering-with-two-dropdownlists-vb/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image55.png)

**图 19**：仍显示了以前选择的产品的详细信息（[单击以查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image57.png)）

从列表中选择新产品会按预期刷新 DetailsView。 如果在更改产品后选取新的类别，则不会再刷新 DetailsView。 不过，如果选择新的产品，而不是选择新的类别，则 DetailsView 会刷新。 这是什么？

问题在于页面生命周期中的计时问题。 每次请求页面时，它会通过一系列步骤进行渲染。 在其中一个步骤中，ObjectDataSource 控件将检查其任何 `SelectParameters` 值是否已更改。 如果是这样，则绑定到 ObjectDataSource 的数据 Web 控件知道它需要刷新其显示。 例如，选择新类别时，`ProductsByCategoryDataSource` ObjectDataSource 检测到其参数值已更改，`ProductsByCategory` DropDownList 重新绑定自身，从而获取所选类别的产品。

在这种情况下出现的问题是：页面生命周期中的 Objectdatasource 检查已更改的参数的点在绑定关联的数据 Web 控件*之前*发生。 因此，选择新类别时，`ProductsByCategoryDataSource` ObjectDataSource 会检测其参数值的更改。 但 `ProductDetails` DetailsView 使用的 ObjectDataSource 并未记下任何此类更改，因为 `ProductsByCategory` DropDownList 尚未重新绑定。 稍后在生命周期中，`ProductsByCategory` DropDownList 将重新绑定到其 ObjectDataSource，从而抓取新选定类别的产品。 如果 `ProductsByCategory` DropDownList 的值已更改，则 `ProductDetails` DetailsView 的 ObjectDataSource 已经完成了其参数值检查;因此，DetailsView 显示其以前的结果。 图20中描述了这种交互。

[![在 ProductDetails DetailsView 的 ObjectDataSource 检查更改后，ProductsByCategory DropDownList 值更改](master-detail-filtering-with-two-dropdownlists-vb/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image58.png)

**图 20**： `ProductDetails` DetailsView 的 ObjectDataSource 检查更改后 `ProductsByCategory` DropDownList 值发生更改（[单击查看完全大小的图像](master-detail-filtering-with-two-dropdownlists-vb/_static/image60.png)）

若要解决此情况，需要在 `ProductsByCategory` DropDownList 绑定后显式重新绑定 `ProductDetails` DetailsView。 可以通过调用 `ProductDetails` DetailsView 的 `DataBind()` 方法在 `ProductsByCategory` DropDownList 的 `DataBound` 事件时调用来实现此目的。 向 `MasterDetailsDetails.aspx` 页面的代码隐藏类添加以下事件处理程序代码（请参阅 "[以编程方式设置 ObjectDataSource 的参数值](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)"，以获取有关如何添加事件处理程序的讨论）：

[!code-vb[Main](master-detail-filtering-with-two-dropdownlists-vb/samples/sample2.vb)]

添加对 `ProductDetails` DetailsView 的 `DataBind()` 方法的显式调用之后，本教程将按预期方式工作。 图21重点介绍了这种更改如何修正之前的问题。

[![在 ProductsByCategory DropDownList 的数据绑定事件激发时显式刷新 ProductDetails DetailsView](master-detail-filtering-with-two-dropdownlists-vb/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-vb/_static/image61.png)

**图 21**：当 `ProductsByCategory` DropDownList 的 `DataBound` 事件激发时，`ProductDetails` DetailsView 会显式刷新（[单击查看完全大小的映像](master-detail-filtering-with-two-dropdownlists-vb/_static/image63.png)）

## <a name="summary"></a>摘要

DropDownList 用作主/详细信息报表的理想用户界面元素，在该元素中，主记录和详细记录之间存在一对多关系。 在前面的教程中，我们看到了如何使用单个 DropDownList 来筛选所选类别显示的产品。 在本教程中，我们将使用 DropDownList 替换产品的 GridView，并使用 DetailsView 显示所选产品的详细信息。 可以轻松地将本教程中讨论的概念扩展到涉及多个一对多关系（例如客户、订单和订单项）的数据模型。 通常，你始终可以为一对多关系中的每个 "one" 实体添加 DropDownList。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-filtering-with-a-dropdownlist-vb.md)
> [下一页](master-detail-filtering-across-two-pages-vb.md)
