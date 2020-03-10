---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-vb
title: 跨两个页面的母版/详细信息筛选（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将介绍如何在两个页面之间分隔主/详细信息报表。 在 "主" 页中，我们使用中继器控件呈现 categ 的列表 。
ms.author: riande
ms.date: 10/30/2010
ms.assetid: f1a1be2c-6fd9-4a09-916e-aa1b98d5cf17
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 037e5f47efff88bfcbec57b11efa4fec04f9542d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78491474"
---
# <a name="masterdetail-filtering-across-two-pages-vb"></a>跨两个页面的母版/详细信息筛选 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_34_VB.exe)或[下载 PDF](master-detail-filtering-acess-two-pages-datalist-vb/_static/datatutorial34vb1.pdf)

> 在本教程中，我们将介绍如何在两个页面之间分隔主/详细信息报表。 在 "主" 页中，我们使用中继器控件呈现类别列表，单击此类将使用户进入 "详细信息" 页，其中两列 DataList 显示属于所选类别的产品。

## <a name="introduction"></a>简介

在[跨两个页面的主/详细筛选](../masterdetail/master-detail-filtering-across-two-pages-vb.md)教程中，我们使用 GridView 显示了此模式，以显示系统中的所有供应商。 此 GridView 包含了一个 HyperLinkField，它呈现为指向第二个页面的链接，并沿查询字符串传递 `SupplierID`。 第二页使用 GridView 列出了所选供应商提供的产品。

此类主/详细报表也可使用 DataList 和 Repeater 控件来完成。 唯一的区别是，DataList 和 Repeater 都不支持 HyperLinkField 控件。 相反，我们必须在控件的 `ItemTemplate`中添加一个超链接 Web 控件或一个定位点 HTML 元素（`<a>`）。 然后，可以使用声明性或编程方法自定义超链接的 `NavigateUrl` 属性或定位点的 `href` 属性。

在本教程中，我们将探讨一个示例，该示例使用一个 Repeater 控件在一页上列出项目符号列表中的类别。 每个列表项都包含类别的名称和说明，类别名称显示为指向第二页的链接。 单击此链接将使用户 whisk 到第二页，其中 DataList 将显示属于所选类别的产品。

## <a name="step-1-displaying-the-categories-in-a-bulleted-list"></a>步骤1：在项目符号列表中显示类别

创建任何主/详细信息报表的第一步是通过显示 "主" 记录开始。 因此，第一个任务是在 "主" 页中显示类别。 打开 `DataListRepeaterFiltering` 文件夹中的 "`CategoryListMaster.aspx`" 页，添加一个 Repeater 控件，并从智能标记选择添加新的 ObjectDataSource。 配置新的 ObjectDataSource，使其从 `CategoriesBLL` 类的 `GetCategories` 方法访问其数据（参见图1）。

[![将 ObjectDataSource 配置为使用 CategoriesBLL 类的 GetCategories 方法](master-detail-filtering-acess-two-pages-datalist-vb/_static/image2.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image1.png)

**图 1**：将 ObjectDataSource 配置为使用 `CategoriesBLL` 类的 `GetCategories` 方法（[单击查看完全大小的映像](master-detail-filtering-acess-two-pages-datalist-vb/_static/image3.png)）

接下来，定义中继器模板，使其在项目符号列表中将每个类别的名称和描述显示为一项。 我们还不必担心每个类别都链接到详细信息页。 下面显示了中继器和 ObjectDataSource 的声明性标记：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample1.aspx)]

完成此标记后，请花点时间通过浏览器查看进度。 如图2所示，中继器呈现为项目符号列表，其中显示了每个类别的名称和说明。

[![每个类别显示为项目符号列表项](master-detail-filtering-acess-two-pages-datalist-vb/_static/image5.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image4.png)

**图 2**：每个类别显示为项目符号列表项（[单击以查看完全大小的图像](master-detail-filtering-acess-two-pages-datalist-vb/_static/image6.png)）

## <a name="step-2-turning-the-category-name-into-a-link-to-the-details-page"></a>步骤2：将类别名称转换为详细信息页的链接

若要允许用户显示给定类别的 "详细信息" 信息，我们需要添加指向每个项目符号列表项的链接，单击该链接时，将使用户进入第二页（`ProductsForCategoryDetails.aspx`）。 然后，第二页将使用 DataList 显示选定类别的产品。 若要确定其链接已被单击的类别，需要通过某种机制将单击的类别的 `CategoryID` 传递到第二页。 将标量数据从一个页面传输到另一个页面的最简单、最简单的方法是通过 querystring，这是我们将在本教程中使用的选项。 具体而言，`ProductsForCategoryDetails.aspx` 页将要求选定的 *`categoryID`* 值通过名为 `CategoryID`的 querystring 字段传递。 例如，若要查看具有 `CategoryID` 1 的 "饮料" 类别的产品，用户可以访问 `ProductsForCategoryDetails.aspx?CategoryID=1`。

若要为中继器中的每个项目符号列表项创建超链接，需要将超链接 Web 控件或 HTML 定位点元素（`<a>`）添加到 `ItemTemplate`。 对于每个行，超链接的显示方式相同，这两种方法都能满足需要。 对于中继器，我更喜欢使用定位点元素。 若要使用定位点元素，请将 Repeater 的 ItemTemplate 更新为：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample2.aspx)]

请注意，`CategoryID` 可以直接注入定位点元素的 `href` 属性中;但是，若要执行此操作，必须将 `href` 特性的值界定为撇号（和注释引号），因为 `href` 特性内的 `Eval` 方法将其字符串（`"CategoryID"`）与引号分隔。 或者，可以改为使用超链接 Web 控件：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample3.aspx)]

请注意，URL 的静态部分（`ProductsForCategoryDetails.aspx?CategoryID`）是通过字符串串联直接在数据绑定语法中追加到 `Eval("CategoryID")` 的结果中。

使用超链接控件的一个优点是，如果需要，可以从 Repeater 的 `ItemDataBound` 事件处理程序以编程方式访问该控件。 例如，你可能希望将类别名称显示为文本，而不是显示为没有关联产品的类别的链接。 此类检查可通过编程方式在 `ItemDataBound` 事件处理程序中执行;对于没有关联产品的类别，可以将超链接的 `NavigateUrl` 属性设置为空白字符串，从而导致特定类别名称呈现为纯文本（而不是链接）。 若要详细了解如何基于编程 `ItemDataBound` 逻辑设置 DataList 和 Repeater 的内容的格式，请参阅[基于数据的数据](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md)教程。

如果遵循此过程，可以随意使用页面中的定位点元素或超链接控件方法。 无论采用哪种方法，在浏览器中查看页面时，每个类别名称都应呈现为指向 `ProductsForCategoryDetails.aspx`的链接，并传入适当的 `CategoryID` 值（请参阅图3）。

[![类别名称现在链接到 ProductsForCategoryDetails](master-detail-filtering-acess-two-pages-datalist-vb/_static/image8.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image7.png)

**图 3**：类别名称现在链接到 `ProductsForCategoryDetails.aspx` （[单击查看完全大小的图像](master-detail-filtering-acess-two-pages-datalist-vb/_static/image9.png)）

## <a name="step-3-listing-the-products-that-belong-to-the-selected-category"></a>步骤3：列出属于所选类别的产品

在 `CategoryListMaster.aspx` 页面完成后，我们就可以打开 "详细信息" 页，`ProductsForCategoryDetails.aspx`。 打开此页，将 DataList 从工具箱拖到设计器上，并将其 `ID` 属性设置为 `ProductsInCategory`。 接下来，从 DataList 的智能标记中，选择将新的 ObjectDataSource 添加到页面，并将其命名为 `ProductsInCategoryDataSource`。 将其配置为调用 `ProductsBLL` 类的 `GetProductsByCategoryID(categoryID)` 方法;将插入、更新和删除选项卡中的下拉列表设置为 "（无）"。

[![将 ObjectDataSource 配置为使用 ProductsBLL 类的 GetProductsByCategoryID （类别 Id）方法](master-detail-filtering-acess-two-pages-datalist-vb/_static/image11.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image10.png)

**图 4**：将 ObjectDataSource 配置为使用 `ProductsBLL` 类的 `GetProductsByCategoryID(categoryID)` 方法（[单击查看完全大小的映像](master-detail-filtering-acess-two-pages-datalist-vb/_static/image12.png)）

由于 `GetProductsByCategoryID(categoryID)` 方法接受输入参数（ *`categoryID`* ），因此 "选择数据源" 向导会向我们提供指定参数源的机会。 使用 QueryStringField `CategoryID`将参数源设置为 QueryString。

[![使用 Querystring 字段 "类别 Id" 作为参数的源](master-detail-filtering-acess-two-pages-datalist-vb/_static/image14.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image13.png)

**图 5**：使用 Querystring 字段 `CategoryID` 作为参数的源（[单击查看完全大小的图像](master-detail-filtering-acess-two-pages-datalist-vb/_static/image15.png)）

如前面的教程中所示，在完成 "选择数据源" 向导后，Visual Studio 会自动为 DataList 创建 `ItemTemplate`，其中列出了每个数据字段的名称和值。 将此模板替换为仅列出产品名称、供应商和价格的模板。 同时，将 DataList 的 `RepeatColumns` 属性设置为2。 完成这些更改后，DataList 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample4.aspx)]

若要在操作中查看此页，请从 `CategoryListMaster.aspx` 页开始;接下来，单击 "类别" 项目符号列表中的链接。 这样做会将你转到 `ProductsForCategoryDetails.aspx`，通过查询字符串传递 `CategoryID`。 然后，`ProductsForCategoryDetails.aspx` 中的 `ProductsInCategoryDataSource` ObjectDataSource 将仅获取指定类别的这些产品并将其显示在 DataList 中，这将为每个行呈现两个产品。 图6显示了查看饮料时的 `ProductsForCategoryDetails.aspx` 屏幕截图。

[显示饮料，每行两个 ![](master-detail-filtering-acess-two-pages-datalist-vb/_static/image17.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image16.png)

**图 6**：显示饮料，每行两个（[单击查看全尺寸图像](master-detail-filtering-acess-two-pages-datalist-vb/_static/image18.png)）

## <a name="step-4-displaying-category-information-on-productsforcategorydetailsaspx"></a>步骤4：在 ProductsForCategoryDetails 上显示类别信息

当用户单击 `CategoryListMaster.aspx`中的某个类别时，它们将被视为 `ProductsForCategoryDetails.aspx` 并显示属于所选类别的产品。 但是，在 `ProductsForCategoryDetails.aspx` 没有与所选类别有关的视觉提示。 如果用户想要单击饮料，但意外单击了调味品，则在 `ProductsForCategoryDetails.aspx`后，就无法意识到它们的错误。 为了缓解这种潜在问题，我们可以在 "`ProductsForCategoryDetails.aspx`" 页的顶部显示所选类别的相关信息（其名称和说明）。

若要实现此目的，请在 `ProductsForCategoryDetails.aspx`中的中继器控件上添加 FormView。 接下来，将新的 ObjectDataSource 从名为 `CategoryDataSource` 的 FormView 智能标记添加到页面，并将其配置为使用 `CategoriesBLL` 类的 `GetCategoryByCategoryID(categoryID)` 方法。

[通过 CategoriesBLL 类的 GetCategoryByCategoryID （类别 Id）方法 ![访问有关该类别的信息](master-detail-filtering-acess-two-pages-datalist-vb/_static/image20.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image19.png)

**图 7**：通过 `CategoriesBLL` 类的 `GetCategoryByCategoryID(categoryID)` 方法访问有关类别的信息（[单击查看完全大小的图像](master-detail-filtering-acess-two-pages-datalist-vb/_static/image21.png)）

与步骤3中添加的 `ProductsInCategoryDataSource` ObjectDataSource 一样，`CategoryDataSource`的 "配置数据源" 向导会提示我们输入 `GetCategoryByCategoryID(categoryID)` 方法的输入参数的源。 使用与之前完全相同的设置，将参数源设置为 QueryString，将 QueryStringField 值设置为 `CategoryID` （请参阅图5）。

完成向导后，Visual Studio 会自动为 FormView 创建 `ItemTemplate`、`EditItemTemplate`和 `InsertItemTemplate`。 由于我们要提供只读接口，因此可随意删除 `EditItemTemplate` 和 `InsertItemTemplate`。 此外，还可以随意自定义 FormView 的 `ItemTemplate`。 删除多余的模板并自定义 ItemTemplate 后，FormView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample5.aspx)]

图8显示了通过浏览器查看此页时的屏幕截图。

> [!NOTE]
> 除 FormView 外，还在 FormView 上方添加了超链接控件，该控件会将用户返回到类别列表（`CategoryListMaster.aspx`）。 可以随意将此链接置于其他位置，也可以省略它。

[![类别信息现在显示在页面顶部](master-detail-filtering-acess-two-pages-datalist-vb/_static/image23.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image22.png)

**图 8**：类别信息现在显示在页面顶部（[单击以查看完全大小的图像](master-detail-filtering-acess-two-pages-datalist-vb/_static/image24.png)）

## <a name="step-5-displaying-a-message-if-no-products-belong-to-the-selected-category"></a>步骤5：如果没有产品属于所选类别，则显示一条消息

"`CategoryListMaster.aspx`" 页将列出系统中的所有类别，无论是否有任何关联的产品。 如果用户单击没有关联产品的类别，则不会呈现 `ProductsForCategoryDetails.aspx` 中的 DataList，因为其数据源不会包含任何项。 正如我们在过去教程中看到的那样，GridView 提供了一个 `EmptyDataText` 属性，该属性可用于指定在数据源中没有记录时要显示的文本消息。 遗憾的是，DataList 和 Repeater 都没有此类属性。

为了显示一条消息，告知用户对于所选类别没有匹配的产品，我们需要将 "标签" 控件添加到页面，其 `Text` 属性分配了在没有匹配的产品时要显示的消息。 接下来，我们需要根据 DataList 是否包含任何项，以编程方式设置其 `Visible` 属性。

若要实现此目的，请首先在 DataList 下添加标签。 将其 `ID` 属性设置为 "`NoProductsMessage`，并将其 `Text` 属性设置为" 没有适用于所选类别的产品 ... "接下来，需要根据是否有任何数据绑定到 `ProductsInCategory` DataList，以编程方式设置此标签的 `Visible` 属性。 在将数据绑定到 DataList 后，必须执行此分配。 对于 GridView、DetailsView 和 FormView，我们可以为控件的 `DataBound` 事件创建事件处理程序，该事件会在数据绑定完成后触发。 但是，DataList 和中继器都没有可用的 `DataBound` 事件。

在此特定示例中，我们可以在 `Page_Load` 事件处理程序中分配标签的 `Visible` 属性，因为在页面的 `Load` 事件之前，会将数据分配到 DataList。 但是，这种方法在一般情况下不起作用，因为 ObjectDataSource 中的数据可能会绑定到页面生命周期后期的 DataList。 例如，如果显示的数据基于另一个控件中的值（例如，当使用 DropDownList 存储 "主" 记录来显示主/详细信息报表时），则在页面生命周期中的 `PreRender` 阶段之前，数据可能不会重新绑定到数据 Web 控件。

适用于所有情况的一种解决方案是在绑定 `Item` 或 `AlternatingItem`的项类型时，将 `Visible` 属性分配给 DataList 的 `ItemDataBound` （或 `ItemCreated`）事件处理程序中的 `False`。 在这种情况下，我们知道数据源中至少有一个数据项，因此可以隐藏 `NoProductsMessage` 标签。 除了此事件处理程序外，还需要 DataList 的 `DataBinding` 事件的事件处理程序，在该事件中，将标签的 `Visible` 属性初始化为 `True`。 由于 `DataBinding` 事件在 `ItemDataBound` 事件之前激发，因此标签的 `Visible` 属性最初将设置为 `True`;但是，如果有任何数据项，则将其设置为 `False`。 下面的代码实现了此逻辑：

[!code-vb[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample6.vb)]

Northwind 数据库中的所有类别都与一个或多个产品关联。 若要测试此功能，我已经手动调整了用于本教程的 Northwind 数据库，并将与农产品类别（`CategoryID` = 7）关联的所有产品重新分配给海鲜类别（`CategoryID` = 8）。 为此，可以通过选择 "新建查询" 并使用以下 `UPDATE` 语句来实现服务器资源管理器：

[!code-sql[Main](master-detail-filtering-acess-two-pages-datalist-vb/samples/sample7.sql)]

相应地更新数据库后，返回到 "`CategoryListMaster.aspx`" 页，然后单击 "生成" 链接。 由于不存在属于 "生成" 类别的任何产品，您应该会看到 "没有适用于所选类别的产品 ..."消息，如图9所示。

[![如果所选类别中没有产品，则显示一条消息](master-detail-filtering-acess-two-pages-datalist-vb/_static/image26.png)](master-detail-filtering-acess-two-pages-datalist-vb/_static/image25.png)

**图 9**：如果所选类别中没有产品，则显示一条消息（[单击查看全尺寸图像](master-detail-filtering-acess-two-pages-datalist-vb/_static/image27.png)）

## <a name="summary"></a>摘要

虽然大纲/详细信息报表可以在单个页面上显示主记录和详细记录，但在许多网站中，它们在两个网页之间分隔开。 在本教程中，我们将介绍如何通过使用 "主" 网页中的中继器以及 "详细信息" 页中列出的关联产品，来实现此类主/从报表。 主网页中的每个列表项都包含指向详细信息页的链接，该链接通过行的 `CategoryID` 值传递。

在 "详细信息" 页中，通过 `ProductsBLL` 类的 `GetProductsByCategoryID(categoryID)` 方法来为指定的供应商检索那些产品。 *`categoryID`* 参数值是使用 `CategoryID` querystring 值作为参数源以声明方式指定的。 还介绍了如何使用 FormView 在详细信息页中显示类别详细信息，以及如何在不存在属于所选类别的产品时显示一条消息。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢 。

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Zack 的 Liz Shulok。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-filtering-with-a-dropdownlist-datalist-vb.md)
> [下一页](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md)
