---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
title: 使用 DropDownList 进行主/详细信息筛选（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何使用 DropDownLists 在单个网页中显示大纲/详细信息报表，以显示 "master" 记录，并将 DataList displ 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: ad0f1014-1eff-465f-bdc6-93058de00e44
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-with-a-dropdownlist-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 537f8e76bc0cbfa759a014b63ae5f68b5d3ca64d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78491084"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>使用一个 DropDownList 实现母版/详细信息筛选 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_33_VB.exe)或[下载 PDF](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/datatutorial33vb1.pdf)

> 在本教程中，我们将了解如何使用 DropDownLists 在单个网页中显示大纲/详细信息报表，以显示 "master" 记录，并使用 DataList 显示 "详细信息"。

## <a name="introduction"></a>简介

首先，我们使用 DropDownList 教程在早期的[主/详细信息筛选](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)中使用 GridView 创建的主/详细信息报表将首先显示某些 "主" 记录集。 然后，用户可以向下钻取到其中一个主记录，从而查看该主记录的 "详细信息"。 主/详细信息报表是直观显示一对多关系的理想选择，并显示来自特别 "宽" 表（包含大量列）的详细信息。 我们已经探讨了如何使用前面教程中的 GridView 和 DetailsView 控件实现主/详细信息报表。 在本教程和接下来的两个教程中，我们将重新检查这些概念，但要改为使用 DataList 和 Repeater 控件。

在本教程中，我们将介绍如何使用 DropDownList 来包含 "master" 记录，并在 DataList 中显示 "详细信息" 记录。

## <a name="step-1-adding-the-masterdetail-tutorial-web-pages"></a>步骤1：添加大纲/细节教程网页

在开始本教程之前，首先请花点时间添加本教程所需的文件夹和 ASP.NET 页面，并使用 DataList 和 Repeater 控件处理主/详细信息报表。 首先，在项目中创建一个名为 `DataListRepeaterFiltering`的新文件夹。 接下来，将以下五个 ASP.NET 页面添加到此文件夹，所有这些页面都配置为使用母版页 `Site.master`：

- `Default.aspx`
- `FilterByDropDownList.aspx`
- `CategoryListMaster.aspx`
- `ProductsForCategoryDetails.aspx`
- `CategoriesAndProducts.aspx`

![创建 DataListRepeaterFiltering 文件夹并添加教程 ASP.NET 页面](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image1.png)

**图 1**：创建 `DataListRepeaterFiltering` 文件夹并添加教程 ASP.NET 页面

接下来，打开 `Default.aspx` 页面，并将 `SectionLevelTutorialListing.ascx` 用户控件从 `UserControls` 文件夹拖到设计图面上。 此用户控件（我们在[母版页和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中创建）枚举站点地图并显示项目符号列表中当前部分的教程。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image3.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image2.png)

**图 2**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image4.png)）

为了使项目符号列表显示我们要创建的主/详细教程，我们需要将它们添加到站点地图。 打开 `Web.sitemap` 文件，并在 "通过 DataList 和 Repeater 显示数据" 站点地图节点标记后面添加以下标记：

[!code-xml[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample1.xml)]

![更新站点映射以包括新的 ASP.NET 页面](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image5.png)

**图 3**：更新站点映射以包括新的 ASP.NET 页面

## <a name="step-2-displaying-the-categories-in-a-dropdownlist"></a>步骤2：在 DropDownList 中显示类别

我们的主/详细信息报表将列出 DropDownList 中的类别，其中选定列表项的产品在 DataList 的页面中向下显示。 接下来，第一个任务是在 DropDownList 中显示类别。 首先打开 `DataListRepeaterFiltering` 文件夹中的 "`FilterByDropDownList.aspx`" 页，然后将 "DropDownList" 从 "工具箱" 拖动到页面的设计器中。 接下来，将 DropDownList 的 `ID` 属性设置为 `Categories`。 在 DropDownList 的智能标记中单击 "选择数据源" 链接，并创建名为 `CategoriesDataSource`的新 ObjectDataSource。

[![添加名为 CategoriesDataSource 的新 ObjectDataSource](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image7.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image6.png)

**图 4**：添加名为 `CategoriesDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image8.png)）

配置新的 ObjectDataSource，使其调用 `CategoriesBLL` 类的 `GetCategories()` 方法。 配置 ObjectDataSource 后，我们仍需要指定应在 DropDownList 中显示的数据源字段，以及哪一字段应与每个列表项的值相关联。 将 `CategoryName` 字段作为显示，并将 `CategoryID` 为每个列表项的值。

[![DropDownList 显示 "类别名称" 字段，并使用 "类别 Id" 作为值](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image10.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image9.png)

**图 5**：使 DropDownList 显示 "`CategoryName`" 字段并使用 "`CategoryID`" 作为值（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image11.png)）

此时，我们有一个 DropDownList 控件，其中填充了 `Categories` 表中的记录（已在大约六秒钟内完成）。 图6显示了在浏览器中查看时的进度。

[![下拉列表中列出了当前类别](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image13.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image12.png)

**图 6**：下拉列表列出了当前类别（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image14.png)）

## <a name="step-2-adding-the-products-datalist"></a>步骤2：添加产品 DataList

主/详细信息报表中的最后一步是列出与所选类别关联的产品。 若要实现此目的，请将 DataList 添加到页面，并创建名为 `ProductsByCategoryDataSource`的新 ObjectDataSource。 让 `ProductsByCategoryDataSource` 控件从 `ProductsBLL` 类的 `GetProductsByCategoryID(categoryID)` 方法检索其数据。 由于此主/详细信息报表是只读的，因此请在插入、更新和删除选项卡中选择 "（无）" 选项。

[![选择 GetProductsByCategoryID （类别 Id）方法](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image16.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image15.png)

**图 7**：选择 `GetProductsByCategoryID(categoryID)` 方法（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image17.png)）

单击 "下一步" 后，ObjectDataSource 向导会提示我们输入 `GetProductsByCategoryID(categoryID)` 方法的 *`categoryID`* 参数的值的源。 若要使用所选 `categories` DropDownList 项的值，请将参数源设置为 Control，并将 ControlID 设置为 `Categories`。

[![将 "类别 Id" 参数设置为 "类别 DropDownList" 的值。](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image19.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image18.png)

**图 8**：将 *`categoryID`* 参数设置为 `Categories` DropDownList 的值（[单击以查看完全大小的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image20.png)）

完成 "配置数据源" 向导后，Visual Studio 将自动为 DataList 生成 `ItemTemplate`，其中显示每个数据字段的名称和值。 接下来，让我们将 DataList 改为使用只显示产品名称、类别、供应商、每单位数量和价格的 `ItemTemplate`，以及在每个项之间注入 `<hr>` 元素的 `SeparatorTemplate`。 我将在使用[DataList 和 Repeater 控件教程显示数据](../displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb.md)中的示例中使用 `ItemTemplate`，但您可以随意使用最具视觉吸引力的任何模板标记。

进行这些更改后，DataList 及其 ObjectDataSource 标记应如下所示：

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample2.aspx)]

请花点时间查看浏览器中的进度。 首次访问页面时，将显示属于所选类别（饮料）的产品（如图9所示），但更改 DropDownList 不会更新数据。 这是因为必须发生回发才能更新 DataList。 为实现此目的，我们可以将 DropDownList 的 `AutoPostBack` 属性设置为 `true` 或将按钮 Web 控件添加到页面。 对于本教程，我已选择将 DropDownList 的 `AutoPostBack` 属性设置为 `true`。

图9和10说明了操作中的主/详细信息报表。

[首次访问页面时 ![，将显示饮料产品](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image22.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image21.png)

**图 9**：首次访问页面时，会显示饮料产品（[单击查看全尺寸图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image23.png)）

[![选择新产品（生成）会自动导致回发，更新 DataList](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image25.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image24.png)

**图 10**：选择新产品（生成）会自动导致回发，更新 DataList （[单击查看完全大小的映像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image26.png)）

## <a name="adding-a----choose-a-category----list-item"></a>添加 "--选择类别--" 列表项

第一次访问 `FilterByDropDownList.aspx` 页面时，默认情况下会选择类别 DropDownList 的第一个列表项（饮料），其中显示了 DataList 中的饮料产品。 在*带有 DropDownList 的主/详细筛选*的教程中，我们向默认情况下选择的 DropDownList 添加了一个 "--选择一个类别--" 选项，并在选中后显示了数据库中的*所有*产品。 在 GridView 中列出产品时，这种方法是可管理的，因为每个产品行占用了少量的屏幕空间。 但对于 DataList，每个产品的信息会占用更大的屏幕块。 接下来，我们将添加一个 "--选择一个类别--" 选项，并在默认情况下选择该选项，而不是让它在选择时显示所有产品，而是将其配置为不显示产品。

若要向 DropDownList 添加新的列表项，请切换到属性窗口并单击 `Items` 属性中的省略号。 添加一个新列表项，其中包含 `Text` "--选择类别--" 和 `Value` `0`。

![添加](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image27.png)

**图 11**：添加 "--选择类别--" 列表项

或者，你可以通过将以下标记添加到 DropDownList 来添加列表项：

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-datalist-vb/samples/sample3.aspx)]

此外，我们需要将 DropDownList 控件的 `AppendDataBoundItems` 设置为 `true`，因为如果将它设置为 `false` （默认值），则当类别从 ObjectDataSource 绑定到 DropDownList 时，它们将覆盖所有手动添加的列表项。

![将 AppendDataBoundItems 属性设置为 True](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image28.png)

**图 12**：将 `AppendDataBoundItems` 属性设置为 True

之所以选择 "--选择类别--" 列表项 `0` 值，是因为系统中没有类别值为 "`0`"，因此在选择 "--选择类别--" 列表项时将不会返回任何产品记录。 若要确认这一点，请花点时间通过浏览器访问此页。 如图13所示，最初查看该页时，"--选择类别--" 列表项处于选中状态，并且不会显示任何产品。

[![](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image30.png)](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image29.png)

**图 13**：在 "--选择类别--" 列表项处于选中状态时，不会显示任何产品（[单击查看完全尺寸的图像](master-detail-filtering-with-a-dropdownlist-datalist-vb/_static/image31.png)）

如果选择 "--选择类别--" 选项，而不是显示*所有*产品，请改用 `-1` 的值。 敏锐读取器将使用 DropDownList 教程重新开始*使用主/详细筛选*，我们更新了 `ProductsBLL` 类的 `GetProductsByCategoryID(categoryID)` 方法，以便在传入 `-1` *`categoryID`* 值后，返回了所有产品记录。

## <a name="summary"></a>摘要

显示分层相关的数据时，通常可以使用主/详细信息报表来显示数据，用户可以从层次结构顶部开始浏览数据，并向下钻取详细信息。 在本教程中，我们将介绍如何生成一个简单的大纲/详细信息报告，其中显示了所选类别的产品。 为此，可以使用 DropDownList 作为类别列表，并将 DataList 用于属于所选类别的产品。

在下一教程中，我们将介绍如何在两个页面之间分隔主记录和详细记录。 在第一页中，将显示 "主" 记录的列表，其中包含用于查看详细信息的链接。 单击此链接会将用户 whisk 到第二页，这将显示所选主记录的详细信息。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢 。

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Randy Schmidt。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
> [下一页](master-detail-filtering-acess-two-pages-datalist-vb.md)
