---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
title: 添加和响应 GridView 的按钮（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将介绍如何将自定义按钮添加到模板以及 GridView 或 DetailsView 控件的字段。 特别是，我们将 l
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 06c6bbd2-4bdc-435b-87a3-df2c868f4baa
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb
msc.type: authoredcontent
ms.openlocfilehash: 8727d8faead02340d223c75845bf29f63d1a0834
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74601354"
---
# <a name="adding-and-responding-to-buttons-to-a-gridview-vb"></a>添加和响应 GridView 的按钮 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_VB.exe)或[下载 PDF](adding-and-responding-to-buttons-to-a-gridview-vb/_static/datatutorial28vb1.pdf)

> 在本教程中，我们将介绍如何将自定义按钮添加到模板以及 GridView 或 DetailsView 控件的字段。 具体而言，我们将生成一个接口，该接口具有允许用户逐页浏览供应商的 FormView。

## <a name="introduction"></a>简介

虽然很多报表方案都涉及到对报表数据的只读访问，但对于报表而言，包括基于所显示的数据执行操作的功能并不少见。 通常这涉及到使用报表中显示的每个记录添加按钮、LinkButton 或 ImageButton Web 控件，在单击此控件时，将导致回发并调用某些服务器端代码。 逐记录编辑和删除数据是最常见的示例。 事实上，正如我们所看到的，从[插入、更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教程的概述开始，编辑和删除很常见，因为 GridView、DetailsView 和 FormView 控件可以支持此类功能，而无需编写一行代码。

除了 "编辑" 和 "删除" 按钮外，GridView、DetailsView 和 FormView 控件还可以包含按钮、LinkButtons 或 ImageButtons，在单击该按钮时，将执行一些自定义服务器端逻辑。 在本教程中，我们将介绍如何将自定义按钮添加到模板以及 GridView 或 DetailsView 控件的字段。 具体而言，我们将生成一个接口，该接口具有允许用户逐页浏览供应商的 FormView。 对于指定的供应商，FormView 将显示有关该供应商的信息以及一个按钮 Web 控件，如果单击此控件，则会将其所有关联产品标记为已停用。 此外，GridView 列出了所选供应商提供的产品，其中每行都包含 "增加价格" 和 "折扣价格" 按钮，如果单击该按钮，则将产品 `UnitPrice` 增加10% （参见图1）。

[![FormView 和 GridView 都包含执行自定义操作的按钮](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image1.png)

**图 1**： FormView 和 GridView 都包含执行自定义操作的按钮（[单击查看完全尺寸的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image3.png)）

## <a name="step-1-adding-the-button-tutorial-web-pages"></a>步骤1：添加按钮教程网页

在我们介绍如何添加自定义按钮之前，先花点时间在我们的网站项目中创建 ASP.NET 页面，我们将在本教程中使用这些页面。 首先添加一个名为 `CustomButtons`的新文件夹。 接下来，将以下两个 ASP.NET 页面添加到该文件夹，确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `CustomButtons.aspx`

![为自定义按钮相关教程添加 ASP.NET 页](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image4.png)

**图 2**：为自定义按钮相关教程添加 ASP.NET 页

与在其他文件夹中一样，`CustomButtons` 文件夹中的 `Default.aspx` 会在其部分列出教程。 请记住，`SectionLevelTutorialListing.ascx` 用户控件提供此功能。 因此，通过将此用户控件从解决方案资源管理器拖到页面 s 设计视图，将该用户控件添加到 `Default.aspx`。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image5.png)

**图 3**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image7.png)）

最后，将页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，在分页和排序 `<siteMapNode>`之后添加以下标记：

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample1.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧菜单现在包含用于编辑、插入和删除教程的项。

![站点映射现在包含用于自定义按钮教程的条目](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image8.png)

**图 4**：站点地图现在包含用于自定义按钮教程的条目

## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>步骤2：添加列出供应商的 FormView

让我们通过添加列出供应商的 FormView 开始使用本教程。 如简介中所述，此 FormView 允许用户逐页浏览供应商，并显示 GridView 中供应商提供的产品。 此外，此 FormView 还包括一个按钮，单击该按钮时，会将所有供应商的产品标记为不再使用。 在我们考虑将自定义按钮添加到 FormView 之前，首先让我们先创建 FormView，使其显示供应商信息。

首先打开 `CustomButtons` 文件夹中的 "`CustomButtons.aspx`" 页。 将 FormView 从工具箱拖到设计器上，将其添加到页面，并将其 `ID` 属性设置为 `Suppliers`。 在 FormView s 智能标记中，选择创建名为 `SuppliersDataSource`的新 ObjectDataSource。

[![创建一个名为 SuppliersDataSource 的新 ObjectDataSource](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image9.png)

**图 5**：创建名为 `SuppliersDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image11.png)）

配置此新 ObjectDataSource，使其从 `SuppliersBLL` 类 `GetSuppliers()` 方法中进行查询（参见图6）。 由于此 FormView 不提供更新供应商信息的接口，因此请从 "更新" 选项卡的下拉列表中选择 "（无）" 选项。

[![将数据源配置为使用 SuppliersBLL Class s GetSuppliers （）方法](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image12.png)

**图 6**：将数据源配置为使用 `SuppliersBLL` 类 `GetSuppliers()` 方法（[单击以查看完全大小的映像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image14.png)）

配置 ObjectDataSource 后，Visual Studio 将为 FormView 生成 `InsertItemTemplate`、`EditItemTemplate`和 `ItemTemplate`。 删除 `InsertItemTemplate`，并 `EditItemTemplate` 并修改 `ItemTemplate`，使其只显示供应商的公司名称和电话号码。 最后，通过选中 "启用分页" 复选框（或通过将其 `AllowPaging` 属性设置为 `True`），启用 FormView 的分页支持。 完成这些更改后，页面的声明性标记应如下所示：

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample2.aspx)]

图7显示了通过浏览器查看 CustomButtons 页。

[![FormView 列出当前所选供应商的 "公司名称" 和 "电话" 字段](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image15.png)

**图 7**： FormView 列出了当前所选供应商的 "`CompanyName`" 和 "`Phone`" 字段（[单击以查看完全大小的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image17.png)）

## <a name="step-3-adding-a-gridview-that-lists-the-selected-supplier-s-products"></a>步骤3：添加一个 GridView，其中列出了所选的供应商产品

在将 "停止所有产品" 按钮添加到 FormView 的模板之前，让我们先在 FormView 下添加一个 GridView，其中列出了所选供应商提供的产品。 若要实现此目的，请将 GridView 添加到页面，将其 `ID` 属性设置为 `SuppliersProducts`，然后添加名为 `SuppliersProductsDataSource`的新 ObjectDataSource。

[![创建一个名为 SuppliersProductsDataSource 的新 ObjectDataSource](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image18.png)

**图 8**：创建名为 `SuppliersProductsDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image20.png)）

将此 ObjectDataSource 配置为使用 ProductsBLL 类 `GetProductsBySupplierID(supplierID)` 方法（请参阅图9）。 尽管此 GridView 允许调整产品的价格，但它不会使用来自 GridView 的内置编辑或删除功能。 因此，可以为 ObjectDataSource 的 "更新"、"插入" 和 "删除" 选项卡将下拉列表设置为 "（无）"。

[![将数据源配置为使用 ProductsBLL 类 s GetProductsBySupplierID （供应商）方法](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image21.png)

**图 9**：将数据源配置为使用 `ProductsBLL` 类 `GetProductsBySupplierID(supplierID)` 方法（[单击以查看完全大小的映像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image23.png)）

由于 `GetProductsBySupplierID(supplierID)` 方法接受输入参数，因此 ObjectDataSource 向导会提示我们输入此参数值的源。 若要从 FormView 传入 `SupplierID` 值，请将 "参数源" 下拉列表设置为 "控制"，并将 "ControlID" 下拉列表设置为 "`Suppliers`" （在步骤2中创建的 FormView 的 ID）。

[![指示供应商参数应来自供应商 FormView 控件](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image24.png)

**图 10**：指示 *`supplierID`* 参数应来自于 `Suppliers` FormView 控件（[单击查看完全大小的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image26.png)）

完成 ObjectDataSource 向导后，GridView 将包含每个产品的数据字段的 BoundField 或 CheckBoxField。 让我们对此进行微调，以便仅显示 `ProductName` 和 `UnitPrice` BoundFields 以及 `Discontinued` CheckBoxField;此外，让我们将 `UnitPrice` BoundField 的格式设置为货币格式。 GridView 和 `SuppliersProductsDataSource` ObjectDataSource 的声明性标记应类似于以下标记：

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample3.aspx)]

此时，我们的教程将显示一个主/详细信息报表，使用户可以从顶部的 FormView 中选择一个供应商，并通过底部的 GridView 查看该供应商提供的产品。 图11显示了在 FormView 中选择东京商贸供应商时此页的屏幕截图。

[![所选供应商的产品显示在 GridView 中](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image27.png)

**图 11**：选择的供应商产品显示在 GridView 中（[单击以查看完全大小的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image29.png)）

## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>步骤4：创建 DAL 和 BLL 方法，停止供应商的所有产品

在我们可以向 FormView 添加一个按钮，在单击该按钮时，将停止所有供应商的产品，我们首先需要向执行此操作的 DAL 和 BLL 添加一个方法。 具体而言，此方法将命名为 `DiscontinueAllProductsForSupplier(supplierID)`。 单击 "FormView" 按钮后，将在业务逻辑层中调用此方法，并传入所选供应商 `SupplierID`;然后，BLL 将向下调用相应的数据访问层方法，该方法将向数据库发出 `UPDATE` 语句，该语句会使指定的供应商产品中断。

正如我们在前面的教程中所做的那样，我们将使用自下而上的方法，从创建 DAL 方法，然后是 BLL 方法开始，最后在 ASP.NET 页中实现该功能。 打开 `App_Code/DAL` 文件夹中 `Northwind.xsd` 的类型化数据集，并将新方法添加到 `ProductsTableAdapter` （右键单击 `ProductsTableAdapter`，然后选择 "添加查询"）。 这样做将显示 "TableAdapter 查询配置向导"，指导我们完成添加新方法的过程。 首先，指示 DAL 方法将使用即席 SQL 语句。

[![使用即席 SQL 语句创建 DAL 方法](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image30.png)

**图 12**：使用即席 SQL 语句创建 DAL 方法（[单击以查看完全大小的映像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image32.png)）

接下来，向导将提示我们输入要创建的查询类型。 由于 `DiscontinueAllProductsForSupplier(supplierID)` 方法需要更新 `Products` 数据库表，因此，需要创建一个更新数据的查询，将 `Discontinued` 字段设置为 *`supplierID`* 1。

[![选择更新查询类型](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image33.png)

**图 13**：选择 "更新" 查询类型（[单击以查看完全大小的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image35.png)）

下一个向导屏幕提供了 TableAdapter 的现有 `UPDATE` 语句，该语句更新 `Products` DataTable 中定义的每个字段。 将此查询文本替换为以下语句：

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample4.sql)]

输入此查询并单击 "下一步" 后，最后一个向导屏幕会要求输入新方法 `DiscontinueAllProductsForSupplier`。 通过单击 "完成" 按钮完成向导。 返回到数据集设计器后，应会在名为 `DiscontinueAllProductsForSupplier(@SupplierID)`的 `ProductsTableAdapter` 中看到一个新方法。

[![命名新的 DAL 方法 DiscontinueAllProductsForSupplier](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image36.png)

**图 14**：将新的 DAL 方法命名 `DiscontinueAllProductsForSupplier` （[单击以查看完全大小的映像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image38.png)）

使用在数据访问层中创建的 `DiscontinueAllProductsForSupplier(supplierID)` 方法时，我们的下一个任务是在业务逻辑层中创建 `DiscontinueAllProductsForSupplier(supplierID)` 方法。 若要完成此操作，请打开 `ProductsBLL` 类文件，并添加以下内容：

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample5.vb)]

此方法只需向下调用 DAL 中的 `DiscontinueAllProductsForSupplier(supplierID)` 方法，同时传递提供的 *`supplierID`* 参数值。 如果在某些情况下，只有允许供应商产品停用的任何业务规则，则这些规则应在 BLL 中实施。

> [!NOTE]
> 与 `ProductsBLL` 类中的 `UpdateProduct` 重载不同，`DiscontinueAllProductsForSupplier(supplierID)` 方法签名不包含 `DataObjectMethodAttribute` 特性（`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`）。 这将从 "更新" 选项卡的 "ObjectDataSource s 配置数据源向导" 下拉列表中排除 `DiscontinueAllProductsForSupplier(supplierID)` 方法。我以前省略了此属性，因为我们将在 ASP.NET 页中直接从事件处理程序调用 `DiscontinueAllProductsForSupplier(supplierID)` 方法。

## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>步骤5：向 FormView 添加 "停止所有产品" 按钮

使用 BLL 和 DAL 中的 `DiscontinueAllProductsForSupplier(supplierID)` 方法完成后，为所选供应商添加停止所有产品的功能的最后一步是将按钮 Web 控件添加到 FormView 的 `ItemTemplate`中。 让我们将此类按钮添加到供应商的电话号码下，使用按钮文本，停止所有产品，将 `ID` 属性值 `DiscontinueAllProductsForSupplier`。 可以通过在设计器中单击 "编辑模板" 链接来添加此按钮 Web 控件（参见图15），或直接通过声明性语法。

[![将 "停止所有产品" 按钮 Web 控件添加到 FormView s ItemTemplate](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image39.png)

**图 15**：将 "停止所有产品" 按钮 Web 控件添加到 FormView s `ItemTemplate` （[单击查看完全大小的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image41.png)）

当访问该页的用户单击该按钮时，将触发回发可以和 FormView s [`ItemCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx)。 若要执行自定义代码来响应单击此按钮，可以为此事件创建事件处理程序。 但请注意，只要在 FormView 内单击*任何*按钮、LinkButton 或 ImageButton Web 控件，就会触发 `ItemCommand` 事件。 这意味着，当用户在 FormView 中从一个页面移动到另一个页面时，将激发 `ItemCommand` 事件;当用户在支持插入、更新或删除的 FormView 中单击 "新建"、"编辑" 或 "删除" 时，也是如此。

因为无论单击哪个按钮，都将激发 `ItemCommand`，因此，在事件处理程序中，我们需要一种方法来确定是否已单击 "停止所有产品" 按钮，或者是否为其他按钮。 若要实现此目的，可以将 "Web 控件 `CommandName`" 按钮设置为某个标识值。 单击该按钮时，此 `CommandName` 会传递到 `ItemCommand` 事件处理程序，从而使我们能够确定是否已单击 "停止所有产品" 按钮。 将 "停止所有产品" 按钮 `CommandName` 属性设置为 "DiscontinueProducts"。

最后，让我们使用客户端确认对话框，以确保用户确实要停止所选的供应商产品。 正如我们在[删除教程时添加客户端确认](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-vb.md)中看到的那样，这可以通过一些 JavaScript 来完成。 具体而言，将按钮 Web 控件的 OnClientClick 属性设置为 `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');`

进行这些更改后，FormView 的声明性语法应如下所示：

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample6.aspx)]

接下来，创建 FormView s `ItemCommand` 事件的事件处理程序。 在此事件处理程序中，我们需要首先确定是否已单击 "停止所有产品" 按钮。 如果是这样，我们想要创建 `ProductsBLL` 类的实例并调用其 `DiscontinueAllProductsForSupplier(supplierID)` 方法，并传入所选 FormView 的 `SupplierID`：

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample7.vb)]

请注意，可以使用 FormView 的[`SelectedValue` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)访问 formview 中当前所选供应商的 `SupplierID`。 `SelectedValue` 属性返回在 FormView 中显示的记录的第一个数据键值。 FormView s [`DataKeyNames` 属性](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx)，该属性指示从其中提取数据键值的数据字段，在将 ObjectDataSource 绑定到第2步中的 FormView 时，Visual Studio 会自动将其设置为 `SupplierID`。

创建 `ItemCommand` 事件处理程序后，请花点时间测试页面。 浏览到 Cooperativa de Quesos ' 内华达 Cabras ' 供应商（这是我在 FormView 中的第五个供应商）。 此供应商提供了两个产品： Queso Cabrales 和 Queso Manchego La Pastora，两者都*不*停用。

假设 Cooperativa de Quesos "内华达 Cabras" 已开生意，因此其产品将被淘汰。 单击 "停止所有产品" 按钮。 此时将显示 "客户端确认" 对话框（请参阅图16）。

[![Cooperativa de Quesos 拉斯维加斯 Cabras 提供了两个活动产品](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image42.png)

**图 16**： Cooperativa De Quesos 拉斯维加斯 Cabras 提供了两个活动产品（[单击查看全尺寸图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image44.png)）

如果在 "客户端确认" 对话框中单击 "确定"，则窗体提交将继续进行，从而导致激发 FormView s `ItemCommand` 事件的回发。 然后，创建的事件处理程序将执行，同时调用 `DiscontinueAllProductsForSupplier(supplierID)` 方法，同时停止 Queso Cabrales 和 Queso Manchego La Pastora 产品。

如果已禁用 GridView 视图状态，则将在每次回发时将 GridView 重新绑定到基础数据存储区，因此会立即更新以反映这两种产品现在已停止使用（请参阅图17）。 但是，如果您在 GridView 中未禁用视图状态，则在进行此更改后，您将需要手动将数据重新绑定到 GridView。 若要实现此目的，只需在调用 `DiscontinueAllProductsForSupplier(supplierID)` 方法之后立即调用 GridView `DataBind()` 方法。

[![单击 "停止所有产品" 按钮后，将相应地更新供应商产品](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image45.png)

**图 17**：单击 "停止所有产品" 按钮后，将相应地更新供应商产品（[单击以查看完全大小的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image47.png)）

## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-product-s-price"></a>步骤6：在业务逻辑层创建 UpdateProduct 重载以调整产品的价格

与 FormView 中的 "停止所有产品" 按钮一样，为了增加在 GridView 中增加和减少产品价格的按钮，我们需要首先添加适当的数据访问层和业务逻辑层方法。 由于我们已经有了一个方法来更新 DAL 中的单个产品行，因此可以通过为 BLL 中的 `UpdateProduct` 方法创建新的重载来提供此类功能。

过去的 `UpdateProduct` 重载采用某种形式的产品字段作为标量输入值，然后仅更新了指定产品的字段。 对于此重载，我们将与此标准略有不同，并改为传入产品 `ProductID` 和调整 `UnitPrice` 的百分比（而不是传入新的、调整后的 `UnitPrice` 本身）。 这种方法可以简化我们需要在 ASP.NET 页代码隐藏类中编写的代码，因为我们不必担心如何确定当前的产品 `UnitPrice`。

本教程的 `UpdateProduct` 重载如下所示：

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample8.vb)]

此重载通过 DAL s `GetProductByProductID(productID)` 方法检索有关指定产品的信息。 然后，它会检查是否向 product s `UnitPrice` 分配数据库 `NULL` 值。 如果是这样，价格将保持不变。 然而，如果存在非`NULL` `UnitPrice` 值，则该方法将 `UnitPrice` 指定百分比（`unitPriceAdjustmentPercent`）更新产品。

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>步骤7：将增加和减少按钮添加到 GridView

GridView （和 DetailsView）都由字段集合构成。 除了 BoundFields、CheckBoxFields 和 Templatefield 外，ASP.NET 还包括 ButtonField，该 LinkButton 将呈现为每一行都带有按钮、ImageButton 或的列。 类似于 FormView，单击 GridView 分页按钮中的*任意*按钮、编辑或删除按钮、排序按钮等将导致回发并引发 GridView [`RowCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)。

ButtonField 有一个 `CommandName` 属性，该属性将指定值分配给其每个按钮 `CommandName` 属性。 与 FormView 一样，`RowCommand` 事件处理程序使用 `CommandName` 值来确定单击了哪个按钮。

让我们将两个新的 ButtonFields 添加到 GridView，一个按钮的文本价格为 + 10%，另一个具有文本价格-10%。 若要添加这些 ButtonFields，请单击 GridView s 智能标记的 "编辑列" 链接，从左上角的列表中选择 "ButtonField" 字段类型，然后单击 "添加" 按钮。

![将两个 ButtonFields 添加到 GridView](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image48.png)

**图 18**：将两个 ButtonFields 添加到 GridView

移动两个 ButtonFields，使其显示为前两个 GridView 字段。 接下来，将这两个 ButtonFields 的 `Text` 属性分别设置为 "价格 + 10%" 和 "Price-10%"，并将 `CommandName` 属性分别设置为 "IncreasePrice" 和 "DecreasePrice"。 默认情况下，ButtonField 将其按钮列呈现为 LinkButtons。 不过，可以通过 ButtonField s [`ButtonType` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)更改此属性。 让我们将这两个 ButtonFields 呈现为常规推送按钮;因此，请将 `ButtonType` 属性设置为 `Button`。 图19在进行这些更改之后，将显示 "字段" 对话框。下面是 GridView 的声明性标记。

![配置 ButtonFields Text、CommandName 和 ButtonType 属性](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image49.png)

**图 19**：配置 ButtonFields `Text`、`CommandName`和 `ButtonType` 属性

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample9.aspx)]

创建这些 ButtonFields 后，最后一步是为 GridView `RowCommand` 事件创建事件处理程序。 此事件处理程序（如果在单击 "价格 + 10%" 或 "价格-10%" 按钮的情况下被激发）需要确定单击按钮的行的 `ProductID`，然后调用 `ProductsBLL` 类 `UpdateProduct` 方法，并传入相应的 `UnitPrice` 百分比调整和 `ProductID`。 以下代码执行这些任务：

[!code-vb[Main](adding-and-responding-to-buttons-to-a-gridview-vb/samples/sample10.vb)]

若要确定单击了 "价格 + 10%" 或 "Price-10%" 按钮的行的 `ProductID`，需要查阅 GridView `DataKeys` 集合。 此集合保存每个 GridView 行的 `DataKeyNames` 属性中指定的字段的值。 由于在将 ObjectDataSource 绑定到 GridView 时，GridView `DataKeyNames` 属性已设置为 ProductID，因此 `DataKeys(rowIndex).Value` 为指定的*rowIndex*提供 `ProductID`。

ButtonField 自动传入其按钮通过 `e.CommandArgument` 参数单击的行的*rowIndex* 。 因此，若要确定已单击 "价格 + 10%" 或 "Price-10%" 按钮的行的 `ProductID`，请使用： `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`。

对于 "停止所有产品" 按钮，如果禁用了 GridView 视图状态，则将在每次回发时将 GridView 重新绑定到基础数据存储区，因此会立即更新以反映单击任意一个按钮。 但是，如果您在 GridView 中未禁用视图状态，则在进行此更改后，您将需要手动将数据重新绑定到 GridView。 若要实现此目的，只需在调用 `UpdateProduct` 方法之后立即调用 GridView `DataBind()` 方法。

图20显示了查看奶奶王 Homestead 提供的产品时的页面。 图21显示了为奶奶的 Boysenberry 传播两次单击 "价格 + 10%" 按钮后的结果，为 Northwoods Cranberry 酱单击了 "价格-10%" 按钮一次。

[![GridView 包含价格 + 10% 和价格-10% 按钮](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image50.png)

**图 20**： GridView 包含价格 + 10% 和价格-10% 按钮（[单击以查看完全大小的图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image52.png)）

[![第一个和第三个产品的价格已通过价格 + 10% 和价格-10% 按钮进行更新](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image53.png)

**图 21**：第一个和第三个产品的价格已通过价格 + 10% 和价格-10% 按钮更新（[单击查看全尺寸图像](adding-and-responding-to-buttons-to-a-gridview-vb/_static/image55.png)）

> [!NOTE]
> GridView （和 DetailsView）还可以将按钮、LinkButtons 或 ImageButtons 添加到其 Templatefield。 与 BoundField 一样，单击这些按钮时，将引发回发，引发 GridView `RowCommand` 事件。 但是，当在 TemplateField 中添加按钮时，不会自动将 `CommandArgument` 的按钮设置为行的索引，因为使用 ButtonFields 时。 如果需要确定在 `RowCommand` 事件处理程序中单击的按钮的行索引，则需要使用类似以下代码在 TemplateField 中手动设置其声明性语法中的按钮 `CommandArgument` 属性：  
> `<asp:Button runat="server" ... CommandArgument='<%# CType(Container, GridViewRow).RowIndex %>' />`。

## <a name="summary"></a>总结

GridView、DetailsView 和 FormView 控件都可以包括按钮、LinkButtons 或 ImageButtons。 当单击此类按钮时，会导致回发，并引发在 "FormView" 和 "DetailsView" 控件中的 `ItemCommand` 事件和 GridView 中的 `RowCommand` 事件。 这些数据 Web 控件具有内置功能，可处理常见的命令相关操作，例如删除或编辑记录。 但是，我们还可以使用按钮，在单击该按钮时，会通过执行我们自己的自定义代码来做出响应。

若要实现此目的，需要为 `ItemCommand` 或 `RowCommand` 事件创建事件处理程序。 在此事件处理程序中，我们首先检查传入 `CommandName` 值以确定单击了哪个按钮，然后采取适当的自定义操作。 在本教程中，我们介绍了如何使用按钮和 ButtonFields 停止指定供应商的所有产品，或将特定产品的价格增加或降低10%。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一部分](adding-and-responding-to-buttons-to-a-gridview-cs.md)
