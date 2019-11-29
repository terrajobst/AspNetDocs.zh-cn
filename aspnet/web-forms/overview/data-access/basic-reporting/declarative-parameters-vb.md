---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
title: 声明性参数（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将演示如何使用设置为硬编码值的参数，以选择要在 DetailsView 控件中显示的数据。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: dc1234a3-114f-4c9a-8d25-50ca03cc8e8e
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-vb
msc.type: authoredcontent
ms.openlocfilehash: cdc42752fc78d18366af037a81fe4ebe5a1646ef
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74612900"
---
# <a name="declarative-parameters-vb"></a>声明性参数 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_5_VB.exe)或[下载 PDF](declarative-parameters-vb/_static/datatutorial05vb1.pdf)

> 在本教程中，我们将演示如何使用设置为硬编码值的参数，以选择要在 DetailsView 控件中显示的数据。

## <a name="introduction"></a>简介

在[最后一个教程](displaying-data-with-the-objectdatasource-vb.md)中，我们将介绍如何使用与在 `ProductsBLL` 类中调用 `GetProducts()` 方法的 ObjectDataSource 控件绑定的 "GridView"、"DetailsView" 和 "FormView" 控件来显示数据。 `GetProducts()` 方法返回强类型的 DataTable，其中填充了 Northwind 数据库的 `Products` 表中的所有记录。 `ProductsBLL` 类包含其他方法，用于仅返回部分产品-`GetProductByProductID(productID)`、`GetProductsByCategoryID(categoryID)`和 `GetProductsBySupplierID(supplierID)`。 这三种方法都需要一个输入参数，指示如何筛选返回的产品信息。

ObjectDataSource 可用于调用需要输入参数的方法，但为了实现此目的，必须指定这些参数的值来自何处。 参数值可以是硬编码的，也可以来自多种动态源，包括查询字符串值、会话变量、页面上 Web 控件的属性值或其他值。

对于本教程，我们首先演示如何使用设置为硬编码值的参数。 具体来说，我们将介绍如何将 DetailsView 添加到页面，此页面显示有关特定产品的信息（即 Chef Anton 的 Gumbo Mix，其中 `ProductID` 为5）。 接下来，我们将了解如何基于 Web 控件设置参数值。 具体而言，我们将使用 TextBox 使用户键入国家/地区，之后用户可以单击按钮以查看位于该国家/地区的供应商列表。

## <a name="using-a-hard-coded-parameter-value"></a>使用硬编码的参数值

在第一个示例中，首先将 "DetailsView" 控件添加到 `BasicReporting` 文件夹中的 "`DeclarativeParams.aspx`" 页。 从 DetailsView 的智能标记中，从下拉列表中选择 "&lt;新数据源"&gt;，并选择添加 ObjectDataSource。

[![向页面添加 ObjectDataSource](declarative-parameters-vb/_static/image2.png)](declarative-parameters-vb/_static/image1.png)

**图 1**：向页面添加 ObjectDataSource （[单击以查看完全大小的图像](declarative-parameters-vb/_static/image3.png)）

这会自动启动 ObjectDataSource 控件的 "选择数据源" 向导。 从向导的第一个屏幕中选择 `ProductsBLL` 类。

[![选择 ProductsBLL 类](declarative-parameters-vb/_static/image5.png)](declarative-parameters-vb/_static/image4.png)

**图 2**：选择 `ProductsBLL` 类（[单击以查看完全大小的图像](declarative-parameters-vb/_static/image6.png)）

由于我们希望显示有关特定产品的信息，因此我们想要使用 `GetProductByProductID(productID)` 方法。

[![选择 GetProductByProductID （productID）方法](declarative-parameters-vb/_static/image8.png)](declarative-parameters-vb/_static/image7.png)

**图 3**：选择 `GetProductByProductID(productID)` 方法（[单击以查看完全大小的图像](declarative-parameters-vb/_static/image9.png)）

由于我们选择的方法包含一个参数，因此向导有一个屏幕，系统会要求你定义用于参数的值。 左侧列表显示了所选方法的所有参数。 对于 `GetProductByProductID(productID)` 只有一个 `productID`。 在右侧，可以指定所选参数的值。 "参数源" 下拉列表枚举参数值的各种可能的源。 由于我们要将 `productID` 参数的硬编码值指定为5，请将参数源保留为 "无"，并在 "DefaultValue" 文本框中输入5。

[![，将对 productID 参数使用硬编码参数值5](declarative-parameters-vb/_static/image11.png)](declarative-parameters-vb/_static/image10.png)

**图 4**：硬编码参数值5将用于 `productID` 参数（[单击以查看完全大小的图像](declarative-parameters-vb/_static/image12.png)）

完成配置数据源向导后，ObjectDataSource 控件的声明性标记在 `SelectMethod` 属性中定义的方法所需的每个输入参数的 `SelectParameters` 集合中都包含一个 `Parameter` 对象。 由于本示例中使用的方法只需要一个输入参数 `parameterID`，因此这里只有一个条目。 `SelectParameters` 集合可以包含从 `System.Web.UI.WebControls` 命名空间中的 `Parameter` 类派生的任何类。 对于硬编码的参数值，将使用基 `Parameter` 类，但对于其他参数源选项，使用派生 `Parameter` 类;如果需要，还可以创建自己的[自定义参数类型](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11)。

[!code-aspx[Main](declarative-parameters-vb/samples/sample1.aspx)]

> [!NOTE]
> 如果你在自己的计算机上执行以下过程，此时你会看到的声明性标记可能包含 `InsertMethod`、`UpdateMethod`和 `DeleteMethod` 属性的值以及 `DeleteParameters`。 ObjectDataSource 的 "选择数据源" 向导会自动指定 `ProductBLL` 中用于插入、更新和删除操作的方法，因此除非您显式清除这些方法，否则这些方法将包含在上述标记中。

访问此页时，数据 Web 控件将调用 ObjectDataSource 的 `Select` 方法，该方法将调用 `ProductsBLL` 类的 `GetProductByProductID(productID)` 方法，该方法将为 `productID` 输入参数使用硬编码的值5。 方法将返回一个强类型 `ProductDataTable` 对象，该对象包含一个包含单个行的行，其中包含有关 Chef Anton 的 Gumbo 混合的信息（具有 `ProductID` 5 的产品）。

[显示 Chef Anton 的 Gumbo 混合的 ![信息](declarative-parameters-vb/_static/image14.png)](declarative-parameters-vb/_static/image13.png)

**图 5**：显示 Chef Anton 的 Gumbo 混合的相关信息（[单击以查看完全大小的图像](declarative-parameters-vb/_static/image15.png)）

## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>将参数值设置为 Web 控件的属性值

还可以基于页面上 Web 控件的值设置 ObjectDataSource 的参数值。 为了说明这一点，让我们有一个 GridView，其中列出了位于用户指定的国家/地区的所有供应商。 为此，请将文本框添加到用户可在其中输入国家/地区名称的页面。 将此 TextBox 控件的 `ID` 属性设置为 `CountryName`。 另外添加一个按钮 Web 控件。

[![将文本框添加到 ID 为 CountryName 的页面](declarative-parameters-vb/_static/image17.png)](declarative-parameters-vb/_static/image16.png)

**图 6**：使用 `ID` `CountryName` 向页面添加文本框（[单击以查看完全大小的图像](declarative-parameters-vb/_static/image18.png)）

接下来，将 GridView 添加到页面，然后从智能标记中选择添加新的 ObjectDataSource。 由于我们要显示供应商信息，请从向导的第一个屏幕中选择 `SuppliersBLL` 类。 在第二个屏幕上，选取 `GetSuppliersByCountry(country)` 方法。

[![选择 GetSuppliersByCountry （国家/地区）方法](declarative-parameters-vb/_static/image20.png)](declarative-parameters-vb/_static/image19.png)

**图 7**：选择 `GetSuppliersByCountry(country)` 方法（[单击以查看完全大小的图像](declarative-parameters-vb/_static/image21.png)）

由于 `GetSuppliersByCountry(country)` 方法具有输入参数，因此向导再次包含用于选择参数值的最终屏幕。 此时，将参数源设置为 "控件"。 这会将 ControlID 下拉列表填充到页面上的控件的名称;从列表中选择 `CountryName` 控件。 首次访问页面时，`CountryName` TextBox 将为空，因此不会返回任何结果，也不会显示任何内容。 如果希望在默认情况下显示某些结果，请相应地设置 "默认值" 文本框。

[![将参数值设置为 CountryName 控件值](declarative-parameters-vb/_static/image23.png)](declarative-parameters-vb/_static/image22.png)

**图 8**：将参数值设置为 `CountryName` 控制值（[单击以查看完全大小的图像](declarative-parameters-vb/_static/image24.png)）

使用[ControlParameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx)而不是标准 `Parameter` 对象，ObjectDataSource 的声明性标记与第一个示例略有不同。 `ControlParameter` 包含用于指定 Web 控件的 `ID` 的附加属性和用于参数的属性值（`PropertyName`）。 "配置数据源" 向导的智能足以确定对于文本框，我们可能希望使用参数值的 `Text` 属性。 但是，如果您想要使用 Web 控件中的不同属性值，则可以在此处更改 `PropertyName` 值，或者单击向导中的 "显示高级属性" 链接。

[!code-aspx[Main](declarative-parameters-vb/samples/sample2.aspx)]

首次访问页面时，`CountryName` TextBox 为空。 此 ObjectDataSource 的 `Select` 方法仍由 GridView 调用，但是 `Nothing` 的值会传递到 `GetSuppliersByCountry(country)` 方法。 TableAdapter 将 `Nothing` 转换为数据库 `NULL` 值（`DBNull.Value`），但 `GetSuppliersByCountry(country)` 方法使用的查询将被写入，以便在为 `NULL` 参数指定 `@CategoryID` 值时不返回任何值。 简而言之，不返回任何供应商。

但一旦访问者进入国家/地区，并单击 "显示供应商" 按钮来导致回发，则 ObjectDataSource 的 `Select` 方法将被重新查询，并传入 TextBox 控件的 `Text` 值作为 `country` 参数。

[![显示来自加拿大的供应商](declarative-parameters-vb/_static/image26.png)](declarative-parameters-vb/_static/image25.png)

**图 9**：显示了加拿大的供应商（[单击以查看完全大小的图像](declarative-parameters-vb/_static/image27.png)）

## <a name="showing-all-suppliers-by-default"></a>默认情况下显示所有供应商

在第一次查看页面时不显示任何供应商，我们可能希望首先显示*所有*供应商，从而允许用户通过在文本框中输入国家/地区名称削减列表。 当 TextBox 为空时，`SuppliersBLL` 类的 `GetSuppliersByCountry(country)` 方法将传入 *`country`* 输入参数的 `Nothing` 中。 然后，将此 `Nothing` 值向下传递到 DAL 的 `GetSupplierByCountry(country)` 方法，在此方法中，会将该值转换为数据库 `NULL` 以下查询中的 `@Country` 参数值：

[!code-sql[Main](declarative-parameters-vb/samples/sample3.sql)]

即使 `Country` 列具有 `NULL` 值的记录，表达式 `Country = NULL` 始终返回 False;因此，不会返回任何记录。

若要在 "国家/地区" 文本框为空时返回*所有*供应商，我们可以在 BLL 中增加 `GetSuppliersByCountry(country)` 方法，以便在其国家/地区参数 `Nothing` 时调用 `GetSuppliers()` 方法，否则调用 DAL 的 `GetSuppliersByCountry(country)` 方法。 当未指定国家/地区时，这将具有返回所有供应商的效果，以及在包括国家/地区参数时返回的供应商子集。

将 `SuppliersBLL` 类中的 `GetSuppliersByCountry(country)` 方法更改为以下内容：

[!code-vb[Main](declarative-parameters-vb/samples/sample4.vb)]

进行此更改后，"`DeclarativeParams.aspx`" 页将显示第一次访问时的所有供应商（或只要 `CountryName` 的文本框为空）。

[默认情况下，![所有供应商现在显示](declarative-parameters-vb/_static/image29.png)](declarative-parameters-vb/_static/image28.png)

**图 10**：默认情况下，所有供应商都显示（[单击以查看完全大小的图像](declarative-parameters-vb/_static/image30.png)）

## <a name="summary"></a>总结

为了将方法用于输入参数，我们需要在 ObjectDataSource 的 `SelectParameters` 集合中指定参数的值。 不同类型的参数允许从不同的源中获取参数值。 默认参数类型使用硬编码值，但与从查询字符串、会话变量、cookie，甚至是用户输入的值一样，可以从页上的 Web 控件获取参数值。

本教程中所述的示例演示了如何使用声明性参数值。 但是，有时可能需要使用不可用的参数源，例如当前日期和时间，或者，如果我们的站点正在使用成员身份，则可能是访问者的用户 ID。 对于这种情况，我们可以在 ObjectDataSource 调用其基础对象的方法之前以编程方式设置参数值。 [下一教程](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)将介绍如何实现此目的。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](displaying-data-with-the-objectdatasource-vb.md)
> [下一页](programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)
