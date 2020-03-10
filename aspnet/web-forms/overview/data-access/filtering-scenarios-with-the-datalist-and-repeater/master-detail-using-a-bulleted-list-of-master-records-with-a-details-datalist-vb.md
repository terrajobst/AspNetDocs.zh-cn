---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
title: 使用带有详细信息 DataList 的主记录的项目符号列表的母版/详细信息（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将上一教程的两页主/从报表压缩为一个页面，并在 t 。
ms.author: riande
ms.date: 10/17/2006
ms.assetid: ee20742f-6fb7-49a0-a009-058fe363aacb
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb
msc.type: authoredcontent
ms.openlocfilehash: 81d72c666925e89729464e7ea696bde8d323e277
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78490688"
---
# <a name="masterdetail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb"></a>通过详细信息 DataList 使用母版记录项目符号列表的母版/详细信息 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_35_VB.exe)或[下载 PDF](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/datatutorial35vb1.pdf)

> 在本教程中，我们将上一教程的两页主/从报表压缩为一个页面，并在屏幕的左侧显示类别名称的项目符号列表，并在屏幕的右侧显示所选类别的产品。

## <a name="introduction"></a>简介

在[前面的教程](master-detail-filtering-acess-two-pages-datalist-vb.md)中，我们介绍了如何在两个页面之间分隔主/详细信息报表。 在母版页中，我们使用了中继器控件来呈现类别的项目符号列表。 每个类别名称都是一个超链接，单击该超链接时，会将用户转到详细信息页，其中两列 DataList 显示属于所选类别的产品。

在本教程中，我们会将两页教程压缩为一个页面，并在屏幕的左侧显示类别名称的项目符号列表，每个类别名称呈现为 LinkButton。 单击其中一个类别名称 LinkButtons 会引发回发，并将所选类别的产品绑定到屏幕右侧的两列 DataList。 除了显示每个类别的名称外，左侧的中继器还显示给定类别的总产品数（参见图1）。

[![类别的名称和产品总数显示在左侧](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image2.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image1.png)

**图 1**：类别的名称和产品总数显示在左侧（[单击以查看完全大小的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image3.png)）

## <a name="step-1-displaying-a-repeater-in-the-left-portion-of-the-screen"></a>步骤1：在屏幕左边部分显示中继器

对于本教程，我们需要在所选类别的产品左侧显示类别的项目符号列表。 网页中的内容可以使用标准 HTML 元素的段落标记、非换行空格、`<table>` s 等或通过级联样式表（CSS）技术进行定位。 到目前为止，我们的所有教程都使用了 CSS 技术进行定位。 当我们在母版页中的母版页[和站点导航](../introduction/master-pages-and-site-navigation-vb.md)教程中生成导航用户界面时，我们使用了*绝对定位*，指示导航列表和主要内容的精确像素偏移量。 此外，CSS 还可以用于通过*浮动*将一个元素定位到另一个元素的右侧或左侧。 对于所选类别的产品，我们可以将项目符号列表显示在所选类别的产品左侧

从 `DataListRepeaterFiltering` 文件夹打开 "`CategoriesAndProducts.aspx`" 页，并向该页添加一个 Repeater 和一个 DataList。 将中继站 `ID` 设置为 "`Categories`"，并将 "DataList" 设置为 "`CategoryProducts`"。 中转到源视图，将 Repeater 和 DataList 控件放在其自己的 `<div>` 元素中。 也就是说，在中继器之后直接在 `<div>` 元素内包含 Repeater，然后在其自己的 `<div>` 元素中包含 DataList。 此时，你的标记应如下所示：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample1.aspx)]

若要将中继器浮动到 DataList 的左侧，需要使用 `float` CSS 样式属性，如下所示：

[!code-html[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample2.html)]

`float: left;` 将第一个 `<div>` 元素左移到第二个元素的左侧。 "`width`" 和 "`padding-right`" 设置指示第一个 `<div>` `width` 以及在 "`<div>`" 元素的 "内容" 和 "右" 边距之间添加多少填充。 有关 CSS 中的浮动元素的详细信息，请参阅[Floatutorial](http://css.maxdesign.com.au/floatutorial/)。

不是直接通过第一个 `<p>` 元素的 `style` 属性来指定样式设置，而是在名为 `FloatLeft`的 `Styles.css` 中创建一个新的 CSS 类：

[!code-css[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample3.css)]

然后，可以将 `<div>` 替换为 `<div class="FloatLeft">`。

添加 CSS 类并在 `CategoriesAndProducts.aspx` "页中配置标记后，请切换到设计器。 你应会看到浮动在 DataList 左侧的中继器（尽管现在这两个对话框只显示为灰色框，因为我们尚未配置其数据源或模板）。

[![，Repeater 将浮动到 DataList 的左侧](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image5.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image4.png)

**图 2**：中继器在 DataList 的左侧浮动（[单击以查看完全大小的映像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image6.png)）

## <a name="step-2-determining-the-number-of-products-for-each-category"></a>步骤2：确定每个类别的产品数量

标记和 DataList 的标记完成后，我们就可以将类别数据绑定到 Repeater 控件了。 但是，如图1中的类别的项目符号列表所示，除了每个类别的名称，还需要显示与该类别关联的产品的数量。 若要访问此信息，可以：

- **从 ASP.NET 页 s 代码隐藏类中确定此信息。** 对于特定 *`categoryID`* ，可以通过调用 `ProductsBLL` 类的 `GetProductsByCategoryID(categoryID)` 方法来确定关联的产品数。 此方法将返回一个 `ProductsDataTable` 对象，该对象的 `Count` 属性指示存在多少 `ProductsRow`，即指定 *`categoryID`* 的产品数。 我们可以为中继器创建 `ItemDataBound` 事件处理程序，对于绑定到中继器的每个类别，将调用 `ProductsBLL` 类 s `GetProductsByCategoryID(categoryID)` 方法，并在输出中包含其计数。
- **更新类型化数据集中的 `CategoriesDataTable` 以包含 `NumberOfProducts` 列。** 然后，可以更新 `CategoriesDataTable` 中的 `GetCategories()` 方法以包含此信息，或将 `GetCategories()` 保留原样，并创建名为 `GetCategoriesAndNumberOfProducts()`的新 `CategoriesDataTable` 方法。

让我们来浏览这两种方法。 第一种方法更容易实现，因为我们不需要更新数据访问层;但是，它需要更多与数据库的通信。 在 `ItemDataBound` 事件处理程序中对 `ProductsBLL` 类 s `GetProductsByCategoryID(categoryID)` 方法的调用为中继器中显示的每个类别添加了额外的数据库调用。 采用此方法时，有*n* + 1 个数据库调用，其中*N*是 Repeater 中显示的类别数。 对于第二种方法，将返回产品计数，其中包含来自 `CategoriesBLL` 类 `GetCategories()` （或 `GetCategoriesAndNumberOfProducts()`）方法的每个类别的信息，因此只需一次处理数据库。

## <a name="determining-the-number-of-products-in-the-itemdatabound-event-handler"></a>确定 ItemDataBound 事件处理程序中的产品数

在 Repeater `ItemDataBound` 事件处理程序中确定每个类别的产品数量并不需要对现有的数据访问层进行任何修改。 所有修改都可以直接在 "`CategoriesAndProducts.aspx`" 页中进行。 首先通过中继器 s 智能标记添加一个名为 `CategoriesDataSource` 的新 ObjectDataSource。 接下来，配置 `CategoriesDataSource` ObjectDataSource，使其从 `CategoriesBLL` 类 s `GetCategories()` 方法检索其数据。

[![将 ObjectDataSource 配置为使用 CategoriesBLL class s GetCategories （）方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image8.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image7.png)

**图 3**：将 ObjectDataSource 配置为使用 `CategoriesBLL` 类 `GetCategories()` 方法（[单击以查看完全大小的映像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image9.png)）

`Categories` Repeater 中的每一项都需要是可单击的，单击此项时，将导致 `CategoryProducts` DataList 显示选定类别的产品。 这可以通过以下方式实现：将每个类别设为超链接，链接回此相同页面（`CategoriesAndProducts.aspx`），但将 `CategoryID` 传递到查询字符串，就像我们在上一教程中看到的那样。 此方法的优点是，可以通过搜索引擎将显示特定类别产品的页面加入书签并进行索引。

另外，我们还可以将每个类别设为 LinkButton，这是我们在本教程中使用的方法。 LinkButton 在用户浏览器中呈现为超链接，但单击它时，将引发回发;在回发时，需要刷新 DataList 的 ObjectDataSource 以显示属于所选类别的产品。 对于本教程，使用超链接比使用 LinkButton 更有意义;但在其他情况下，使用 LinkButton 更有利。 尽管在本示例中，超链接方法非常适合，但让我们来看一下使用 LinkButton。 正如我们所看到的，使用 LinkButton 会带来一些挑战，不会在超链接的情况下出现。 因此，在本教程中使用 LinkButton 将突出显示这些挑战，并帮助为可能需要使用 LinkButton 而不是超链接的情况提供解决方案。

> [!NOTE]
> 建议使用超链接控件或 `<a>` 元素（而不是 LinkButton）重复本教程。

以下标记显示了中继器和 ObjectDataSource 的声明性语法。 请注意，Repeater 模板会呈现一个项目符号列表，其中每个项都是 LinkButton：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample4.aspx)]

> [!NOTE]
> 在本教程中，Repeater 必须已启用其视图状态（请注意，省略 Repeater 声明性语法中的 `EnableViewState="False"`）。 在步骤3中，我们将为中继器 `ItemCommand` 事件创建事件处理程序，我们将在此事件中更新 DataList s ObjectDataSource `SelectParameters` 集合。 但是，如果禁用了视图状态，则不会触发 Repeater `ItemCommand`。 有关[Stumper 的](http://scottonwriting.net/sowblog/posts/1263.aspx)详细信息，请参阅 ASP.NET 问题及其[解决方案](http://scottonwriting.net/sowBlog/posts/1268.aspx)的详细信息。必须为中继器 `ItemCommand` 事件启用视图状态。

`ID` 属性值为 `ViewCategory` 的 LinkButton 没有其 `Text` 属性集。 如果只是想要显示类别名称，则可以通过数据绑定语法以声明方式设置文本属性，如下所示：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample5.aspx)]

但是，我们想要显示类别的名称*以及*属于该类别的产品数。 可以通过调用 `ProductBLL` 类 s `GetCategoriesByProductID(categoryID)` 方法并确定在生成的 `ProductsDataTable`中返回多少记录，来从 Repeater `ItemDataBound` 事件处理程序检索此信息，如以下代码所示：

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample6.vb)]

首先，我们要确保我们正在处理一个数据项（其 `ItemType` 是 `Item` 或 `AlternatingItem`），然后引用刚刚绑定到当前 `RepeaterItem`的 `CategoriesRow` 实例。 接下来，我们通过创建 `ProductsBLL` 类的实例，调用其 `GetCategoriesByProductID(categoryID)` 方法并确定使用 `Count` 属性返回的记录数来确定此类别的产品数。 最后，ItemTemplate 中的 `ViewCategory` LinkButton 是引用，其 `Text` 属性设置为 "*类别名称*（*NumberOfProductsInCategory*）"，其中*NumberOfProductsInCategory*的格式为包含零位小数位的数字。

> [!NOTE]
> 另外，我们还可以将*格式设置函数*添加到 ASP.NET 页 s 代码隐藏类中，该类接受 `CategoryName` 和 `CategoryID` 值的类别，并返回与该类别中的产品数量相连接的 `CategoryName` （通过调用 `GetCategoriesByProductID(categoryID)` 方法确定）。 可以通过声明方式将此类格式设置函数的结果分配给 LinkButton s Text 属性，以替换 `ItemDataBound` 事件处理程序的需求。 有关使用格式设置函数的详细信息，请参阅[GridView 控件中的 Using templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md)或[基于数据教程设置 DataList 和 Repeater 的格式](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb.md)。

添加此事件处理程序后，请花点时间通过浏览器测试页面。 请注意每个类别在项目符号列表中的列出方式，并显示类别的名称以及与该类别关联的产品数（请参阅图4）。

[![显示每个类别的名称和产品数量](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image11.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image10.png)

**图 4**：显示每个类别的名称和产品数量（[单击以查看完全大小的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image12.png)）

## <a name="updating-thecategoriesdatatableandcategoriestableadapterto-include-the-number-of-products-for-each-category"></a>更新`CategoriesDataTable`和`CategoriesTableAdapter`以包含每个类别的产品数量

我们可以通过调整数据访问层中的 `CategoriesDataTable` 和 `CategoriesTableAdapter` 来将此信息集中在一起，来简化此过程，而不是确定每个类别绑定到中继器的产品数。 若要实现此目的，必须将一个新列添加到 `CategoriesDataTable` 以容纳关联的产品数。 若要将新列添加到 DataTable，请打开类型化数据集（`App_Code\DAL\Northwind.xsd`），右键单击要修改的 DataTable，然后选择 "添加/列"。 向 `CategoriesDataTable` 添加一个新列（参见图5）。

[![将新列添加到 CategoriesDataSource](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image14.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image13.png)

**图 5**：将新列添加到 `CategoriesDataSource` （[单击以查看完全大小的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image15.png)）

这会添加一个名为 "`Column1`" 的新列，只需键入不同的名称即可更改此列。 将此新列重命名为 `NumberOfProducts`。 接下来，需要配置此列的属性。 单击新列并中转到属性窗口。 将列 `DataType` 属性从 `System.String` 更改为 `System.Int32`，并将 `ReadOnly` 属性设置为 `True`，如图6所示。

![设置新列的 DataType 和 ReadOnly 属性](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image16.png)

**图 6**：设置新列的 "`DataType`" 和 "`ReadOnly`" 属性

虽然 `CategoriesDataTable` 现在具有 `NumberOfProducts` 列，但它的值不是由任何对应的 TableAdapter 查询设置的。 如果希望每次检索类别信息时返回此信息，我们可以更新 `GetCategories()` 方法以返回此信息。 但是，如果只需要获取极少实例（例如，仅用于本教程）中类别的关联产品数，则可以将 `GetCategories()` 原样保留并创建返回此信息的新方法。 让我们使用后一种方法，创建名为 `GetCategoriesAndNumberOfProducts()`的新方法。

若要添加此新的 `GetCategoriesAndNumberOfProducts()` 方法，请右键单击 `CategoriesTableAdapter` 并选择 "新建查询"。 这会显示 "TableAdapter 查询配置向导"，在前面的教程中，我们曾使用过多次。 对于此方法，通过指示查询使用返回行的即席 SQL 语句启动向导。

[![使用即席 SQL 语句创建方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image18.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image17.png)

**图 7**：使用即席 SQL 语句创建方法（[单击以查看完全大小的映像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image19.png)）

[![SQL 语句返回的行数](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image21.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image20.png)

**图 8**： SQL 语句返回行（[单击以查看完全大小的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image22.png)）

接下来的向导屏幕提示我们提供查询以供使用。 若要返回每个类别 `CategoryID`、`CategoryName`和 `Description` 字段以及与该类别关联的产品数量，请使用以下 `SELECT` 语句：

[!code-sql[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample7.sql)]

[![指定要使用的查询](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image24.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image23.png)

**图 9**：指定要使用的查询（[单击以查看完全大小的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image25.png)）

请注意，计算与该类别关联的产品数量的子查询的别名为 `NumberOfProducts`。 此命名匹配会导致此子查询返回的值与 `CategoriesDataTable` `NumberOfProducts` 列关联。

输入此查询后，最后一步是选择新方法的名称。 使用 `FillWithNumberOfProducts` 和 `GetCategoriesAndNumberOfProducts` 填充 DataTable 并分别返回 DataTable 模式。

[![命名新的 TableAdapter s 方法 FillWithNumberOfProducts 和 GetCategoriesAndNumberOfProducts](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image27.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image26.png)

**图 10**：将新的 TableAdapter s 方法命名 `FillWithNumberOfProducts` 和 `GetCategoriesAndNumberOfProducts` （[单击以查看完全大小的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image28.png)）

此时，数据访问层已扩展为包含每个类别的产品数。 由于所有表示层都通过单独的业务逻辑层将对 DAL 的所有调用路由，我们需要将相应的 `GetCategoriesAndNumberOfProducts` 方法添加到 `CategoriesBLL` 类：

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample8.vb)]

当 DAL 和 BLL 完成后，我们就可以将这些数据绑定到 `CategoriesAndProducts.aspx`中的 `Categories` 中继器！ 如果已从确定 `ItemDataBound` 事件处理程序部分中的产品数创建了用于 Repeater 的 ObjectDataSource，请删除此 ObjectDataSource 并删除中继器 s `DataSourceID` 属性设置;还通过删除 ASP.NET 代码隐藏类中的 `Handles Categories.OnItemDataBound` 语法，unwire 事件处理程序中的中继器 `ItemDataBound` 事件。

重新播放器恢复其原始状态后，通过中继器 s 智能标记添加一个名为 `CategoriesDataSource` 的新 ObjectDataSource。 将 ObjectDataSource 配置为使用 `CategoriesBLL` 类，但不使用 `GetCategories()` 方法，而是改为使用 `GetCategoriesAndNumberOfProducts()` （参见图11）。

[![将 ObjectDataSource 配置为使用 GetCategoriesAndNumberOfProducts 方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image30.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image29.png)

**图 11**：将 ObjectDataSource 配置为使用 `GetCategoriesAndNumberOfProducts` 方法（[单击查看完全大小的映像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image31.png)）

接下来，更新 `ItemTemplate`，以便使用数据绑定语法以声明方式分配 LinkButton s `Text` 属性，同时包含 `CategoryName` 和 `NumberOfProducts` 数据字段。 转发器和 `CategoriesDataSource` ObjectDataSource 的完整声明性标记如下所示：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample9.aspx)]

通过将 DAL 更新为包含 `NumberOfProducts` 列时所呈现的输出与使用 `ItemDataBound` 事件处理程序方法相同（请参阅图4，以查看显示类别名称和产品数量的中继器屏幕截图）。

## <a name="step-3-displaying-the-selected-category-s-products"></a>步骤3：显示所选类别的产品

此时，我们的 `Categories` Repeater 会显示类别列表以及每个类别中的产品数目。 中继器对每个类别使用 LinkButton，当单击此类别时，将导致回发，此时需要在 `CategoryProducts` DataList 中显示所选类别的产品。

一项挑战是，如何让 DataList 仅显示所选类别的产品。 在[大纲/详细信息中，使用可选择的主 GridView 和详细信息 DetailsView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)教程，我们看到了如何构建一个可以选择行的 GridView，其中所选的行详细信息显示在同一页上的 DetailsView 中。 GridView 的 ObjectDataSource 使用 `ProductsBLL` s `GetProducts()` 方法返回有关所有产品的信息，而 DetailsView s 则 ObjectDataSource 使用 `GetProductsByProductID(productID)` 方法检索有关选定产品的信息。 通过将 *`productID`* 参数值与 GridView s `SelectedValue` 属性的值相关联，以声明方式提供。 遗憾的是，中继器没有 `SelectedValue` 属性，无法用作参数源。

> [!NOTE]
> 这是在 Repeater 中使用 LinkButton 时出现的难题之一。 如果我们使用了超链接通过 querystring 传入 `CategoryID`，则可以使用该 QueryString 字段作为参数 s 值的源。

不过，在我们担心是否缺少用于中继器的 `SelectedValue` 属性之前，让我们先将 DataList 绑定到 ObjectDataSource 并指定其 `ItemTemplate`。

在 DataList s 智能标记中，选择添加名为 `CategoryProductsDataSource` 的新 ObjectDataSource，并将其配置为使用 `ProductsBLL` 类 `GetProductsByCategoryID(categoryID)` 方法。 由于本教程中的 DataList 提供了一个只读界面，因此可随意将插入、更新和删除选项卡中的下拉列表设置为 "（无）"。

[![将 ObjectDataSource 配置为使用 ProductsBLL 类 s GetProductsByCategoryID （类别 Id）方法](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image33.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image32.png)

**图 12**：将 ObjectDataSource 配置为使用 `ProductsBLL` 类 `GetProductsByCategoryID(categoryID)` 方法（[单击以查看完全大小的映像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image34.png)）

由于 `GetProductsByCategoryID(categoryID)` 方法需要输入参数（ *`categoryID`* ），因此 "配置数据源" 向导允许我们指定参数 "源"。 如果类别已在 GridView 或 DataList 中列出，请将 "参数源" 下拉列表设置为 "控件"，并将 ControlID 设置为数据 Web 控件的 `ID`。 但是，由于中继器缺少 `SelectedValue` 属性，因此不能将其用作参数源。 如果选中，则会发现 ControlID 下拉列表仅包含一个控件 `ID``CategoryProducts`（DataList 的 `ID`）。

现在，将 "参数源" 下拉列表设置为 "无"。 当在 Repeater 中单击类别 LinkButton 时，我们将以编程方式分配此参数值。

[![未指定类别 Id 参数的参数源](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image36.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image35.png)

**图 13**：不要为 *`categoryID`* 参数指定参数源（[单击查看完全大小的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image37.png)）

完成 "配置数据源" 向导后，Visual Studio 会自动生成 DataList s `ItemTemplate`。 将此默认 `ItemTemplate` 替换为在前面的教程中使用的模板;同时，将 DataList s `RepeatColumns` 属性设置为2。 进行这些更改后，DataList 及其关联的 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample10.aspx)]

当前不会设置 `CategoryProductsDataSource` ObjectDataSource s *`categoryID`* 参数，因此查看该页时不会显示任何产品。 我们需要做的就是基于中继器中单击的类别的 `CategoryID` 设置此参数值。 这就带来了两个难题：首先，如何确定何时单击了 LinkButton `ItemTemplate` 中的;其次，如何确定被单击 LinkButton 的相应类别的 `CategoryID`？

LinkButton 和 ImageButton 控件一样，都有一个 `Click` 事件和一个[`Command` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.command.aspx)。 `Click` 事件旨在只需注意 LinkButton 已被单击。 但有时，除了指出已单击 LinkButton 外，还需要将一些额外的信息传递给事件处理程序。 如果是这种情况，则可以为 LinkButton s [`CommandName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandname.aspx)和[`CommandArgument`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.linkbutton.commandargument.aspx)属性分配此额外信息。 然后，在单击 LinkButton 时，将激发其 `Command` 事件（而不是其 `Click` 事件），并向事件处理程序传递 `CommandName` 和 `CommandArgument` 属性的值。

当从 Repeater 中的模板中引发 `Command` 事件时，将激发 Repeater [`ItemCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeater.itemcommand.aspx)，并将该事件传递给所单击的 LinkButton （或按钮或 ImageButton）的 `CommandName` 和 `CommandArgument` 值。 因此，若要确定何时单击了 Repeater 中的类别 LinkButton，需要执行以下操作：

1. 将 Repeater `ItemTemplate` 中 LinkButton 的 `CommandName` 属性设置为某个值（我曾使用 ListProducts）。 通过设置此 `CommandName` 值，单击 LinkButton 时将触发 LinkButton s `Command` 事件。
2. 将 LinkButton `CommandArgument` 属性设置为当前项的 `CategoryID`值。
3. 为中继器 `ItemCommand` 事件创建事件处理程序。 在事件处理程序中，将 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 参数设置为传入 `CommandArgument`的值。

以下 `ItemTemplate` 类别 Repeater 标记的标记实现步骤1和2。 请注意如何使用数据绑定语法为 `CommandArgument` 值分配数据项 `CategoryID`：

[!code-aspx[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample11.aspx)]

无论何时创建 `ItemCommand` 事件处理程序，始终首先检查传入的 `CommandName` 值是明智的，因为在 Repeater 中*任何*LinkButton 或 ImageButton 引发的*任何*`Command` 事件都将导致触发 `ItemCommand` 事件。 虽然目前只有一个这样的 LinkButton，但在将来我们（或我们团队的另一个开发人员）可能会将其他按钮 Web 控件添加到中继器，单击该控件时，将引发相同的 `ItemCommand` 事件处理程序。 因此，最佳做法是始终确保检查 `CommandName` 属性，如果与所需的值匹配，只需继续编程逻辑。

在确保传入的 `CommandName` 值等于 ListProducts 后，事件处理程序会将 `CategoryProductsDataSource` ObjectDataSource s `CategoryID` 参数分配给传入的 `CommandArgument`的值。 对 ObjectDataSource `SelectParameters` 的这一修改会自动导致 DataList 重新绑定到数据源，从而显示新选定类别的产品。

[!code-vb[Main](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/samples/sample12.vb)]

添加这些内容后，我们的教程已完成！ 花点时间在浏览器中进行测试。 图14：首次访问页面时显示屏幕。 由于尚未选择类别，因此不会显示任何产品。 单击某一类别（如 "生产"）会在两列视图的 "产品" 类别中显示这些产品（参见图15）。

[首次访问页面时，不会显示 ![产品](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image39.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image38.png)

**图 14**：首次访问页面时未显示任何产品（[单击以查看完全大小的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image40.png)）

[![单击 "生成" 类别将列出匹配的产品](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image42.png)](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image41.png)

**图 15**：单击 "生成" 类别将列出匹配的产品（[单击以查看完全大小的图像](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb/_static/image43.png)）

## <a name="summary"></a>摘要

正如我们在本教程中看到的那样，主/详细信息报表可以分散在两个页面上，也可以合并在一起。 但是，在单页上显示主/详细信息报表会给出一些有关如何最好地在页面上布局大纲和详细信息的问题。 在*主/详细信息中，使用可选择的主 GridView 和详细信息 DetailsView*教程，我们的详细信息记录显示在主记录上;在本教程中，我们使用了 CSS 技术将主记录浮动到详细信息的左侧。

除了显示主/详细信息报表之外，我们还可以探索如何检索与每个类别关联的产品的数量，以及如何在从中继器内单击 LinkButton （或按钮或 ImageButton）时执行服务器端逻辑。

本教程通过 DataList 和中继器完成对主/详细信息报表的检查。 下一组教程将演示如何向 DataList 控件添加编辑和删除功能。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- 使用 CSS [Floatutorial](http://css.maxdesign.com.au/floatutorial/)有关浮动 css 元素的教程
- [Css 定位](http://www.brainjar.com/css/positioning/)有关将元素定位到 css 的详细信息
- 使用 `<table>` 和用于定位的其他 HTML 元素，使用[Html 布局内容](http://www.w3schools.com/html/html_layout.asp)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导审查人员是 Zack 的。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-detail-filtering-acess-two-pages-datalist-vb.md)
