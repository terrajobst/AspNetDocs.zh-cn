---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
title: 自定义数据修改接口（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将介绍如何通过将 "标准" 文本框和复选框控件替换为 alternati，来自定义可编辑 GridView 的界面。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 4830d984-bd2c-4a08-bfe5-2385599f1f7d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 85ec7bdde6b2bffbbda066b0441bbd36b7072197
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585204"
---
# <a name="customizing-the-data-modification-interface-vb"></a>自定义数据修改界面 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_VB.exe)或[下载 PDF](customizing-the-data-modification-interface-vb/_static/datatutorial20vb1.pdf)

> 在本教程中，我们将介绍如何通过将 "标准" 文本框和复选框控件替换为备用输入 Web 控件来自定义可编辑 GridView 的界面。

## <a name="introduction"></a>简介

GridView 和 DetailsView 控件使用的 BoundFields 和 CheckBoxFields 可简化修改数据的过程，因为它们能够呈现只读、可编辑和可插入的接口。 可以呈现这些接口，而无需添加任何附加的声明性标记或代码。 但在实际情况下，BoundField 和 CheckBoxField 的接口缺乏可定制性。 若要在 GridView 或 DetailsView 中自定义可编辑或可插入的界面，需改为使用 TemplateField。

在[前面的教程](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)中，我们介绍了如何通过添加验证 Web 控件自定义数据修改接口。 在本教程中，我们将介绍如何自定义实际的数据收集 Web 控件，并将 BoundField 和 CheckBoxField 的标准 TextBox 和 CheckBox 控件替换为备用输入 Web 控件。 具体而言，我们将构建一个可编辑的 GridView，以允许更新产品的名称、类别、供应商和中止状态。 编辑特定行时，"类别" 和 "供应商" 字段将呈现为 DropDownLists，其中包含可供选择的可用类别和供应商组。 此外，我们会将 CheckBoxField 的默认复选框替换为提供两个选项的 RadioButtonList 控件： "活动" 和 "已停用"。

[![GridView 的编辑界面包括 DropDownLists 和单选按钮](customizing-the-data-modification-interface-vb/_static/image2.png)](customizing-the-data-modification-interface-vb/_static/image1.png)

**图 1**： GridView 的编辑界面包括 DropDownLists 和单选按钮（[单击以查看完全尺寸的图像](customizing-the-data-modification-interface-vb/_static/image3.png)）

## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>步骤1：创建适当的`UpdateProduct`重载

在本教程中，我们将构建一个可编辑的 GridView，以允许编辑产品的名称、类别、供应商和废止状态。 因此，我们需要一个 `UpdateProduct` 重载，它接受这四个产品值加 `ProductID`这四个输入参数。 与我们以前的重载一样，此操作将：

1. 从数据库检索指定 `ProductID`的产品信息。
2. 更新 `ProductName`、`CategoryID`、`SupplierID`和 `Discontinued` 字段，并
3. 通过 TableAdapter 的 `Update()` 方法将更新请求发送到 DAL。

为简洁起见，对于此特定重载，我省略了业务规则检查，确保标记为 "已停用" 的产品不是其供应商提供的唯一产品。 如果愿意，或最好将逻辑重构为单独的方法，则可以随意将其添加到中。

下面的代码演示了 `ProductsBLL` 类中的新 `UpdateProduct` 重载：

[!code-vb[Main](customizing-the-data-modification-interface-vb/samples/sample1.vb)]

## <a name="step-2-crafting-the-editable-gridview"></a>步骤2：编制可编辑的 GridView

添加 `UpdateProduct` 重载后，便可以创建可编辑的 GridView 了。 打开 `EditInsertDelete` 文件夹中的 "`CustomizedUI.aspx`" 页，并向设计器添加一个 GridView 控件。 接下来，从 GridView 的智能标记创建新的 ObjectDataSource。 将 ObjectDataSource 配置为通过 `ProductBLL` 类的 `GetProducts()` 方法检索产品信息，并使用刚刚创建的 `UpdateProduct` 重载更新产品数据。 从 "插入" 和 "删除" 选项卡中，从下拉列表中选择 "（无）"。

[![将 ObjectDataSource 配置为使用刚创建的 UpdateProduct 重载](customizing-the-data-modification-interface-vb/_static/image5.png)](customizing-the-data-modification-interface-vb/_static/image4.png)

**图 2**：将 ObjectDataSource 配置为使用刚创建的 `UpdateProduct` 重载（[单击查看完全大小的映像](customizing-the-data-modification-interface-vb/_static/image6.png)）

正如我们在数据修改教程中看到的那样，Visual Studio 创建的 ObjectDataSource 的声明性语法将 `OldValuesParameterFormatString` 属性分配给 `original_{0}`。 当然，这不能与我们的业务逻辑层一起使用，因为我们的方法不希望传入原始 `ProductID` 值。 因此，正如我们在上一教程中所做的那样，请花点时间从声明性语法中删除此属性分配，或将此属性的值设置为 `{0}`。

此更改之后，ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample2.aspx)]

请注意，`OldValuesParameterFormatString` 属性已被移除，并且对于 `UpdateProduct` 重载所需的每个输入参数，`UpdateParameters` 集合中都有 `Parameter`。

尽管 ObjectDataSource 配置为仅更新产品值的子集，但 GridView 当前显示的所有产品字段*均*为。 花点时间编辑 GridView，使：

- 它仅包含 `ProductName`、`SupplierName``CategoryName` BoundFields 和 `Discontinued` CheckBoxField
- "`CategoryName`" 和 "`SupplierName`" 字段显示在 `Discontinued` CheckBoxField 之前（左侧）
- `CategoryName` 和 `SupplierName` BoundFields ' `HeaderText` 属性分别设置为 "Category" 和 "供应商"。
- 启用编辑支持（选中 GridView 智能标记中的 "启用编辑" 复选框）

进行这些更改后，设计器将类似于图3，其中显示了 GridView 的声明性语法。

[![从 GridView 中删除不需要的字段](customizing-the-data-modification-interface-vb/_static/image8.png)](customizing-the-data-modification-interface-vb/_static/image7.png)

**图 3**：从 GridView 中删除不需要的字段（[单击以查看完全大小的图像](customizing-the-data-modification-interface-vb/_static/image9.png)）

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample3.aspx)]

此时，GridView 的只读行为已经完成。 查看数据时，每个产品都呈现为 GridView 中的一行，显示产品的名称、类别、供应商和停止状态。

[![GridView 的只读接口已完成](customizing-the-data-modification-interface-vb/_static/image11.png)](customizing-the-data-modification-interface-vb/_static/image10.png)

**图 4**： GridView 的只读接口已完成（[单击以查看完全大小的图像](customizing-the-data-modification-interface-vb/_static/image12.png)）

> [!NOTE]
> 如在[插入、更新和删除数据教程](an-overview-of-inserting-updating-and-deleting-data-cs.md)中所讨论的那样，启用 GridView 的视图状态（默认行为）至关重要。 如果将 GridView `EnableViewState` 属性设置为 "`false`"，则可能会遇到使并发用户无意中删除或编辑记录的风险。 有关详细信息，请参阅[ASP.NET 2.0 GridViews/DetailsView/FormViews 的并发问题，其中支持编辑和/或删除并禁用了其视图状态](http://scottonwriting.net/sowblog/posts/10054.aspx)。

## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>步骤3：使用 DropDownList 作为类别和供应商编辑界面

请记住，`ProductsRow` 对象包含 `CategoryID`、`CategoryName`、`SupplierID`和 `SupplierName` 属性，这些属性提供 `Products` 数据库表中的实际外键 ID 值和 `Name` 和 `Categories` 表中的相应 `Suppliers` 值。 `ProductRow`的 `CategoryID` 和 `SupplierID` 都可以从中读取和写入，而 `CategoryName` 和 `SupplierName` 属性被标记为只读。

由于 `CategoryName` 和 `SupplierName` 属性的只读状态，相应 BoundFields 的 `ReadOnly` 属性设置为 `True`，从而防止在编辑行时修改这些值。 虽然我们可以将 `ReadOnly` 属性设置为 `False`，在编辑过程中将 `CategoryName` 和 `SupplierName` BoundFields 呈现为文本框，但当用户尝试更新产品时，这种方法将导致异常，因为没有 `UpdateProduct` 和 `CategoryName` 输入中采用 `SupplierName` 重载。 事实上，我们不希望出于以下两个原因创建此类重载：

- `Products` 表没有 `SupplierName` 或 `CategoryName` 字段，但 `SupplierID` 和 `CategoryID`。 因此，我们希望将这些特定 ID 值（而不是查找表的值）传递给方法。
- 要求用户键入供应商或类别的名称小于理想的名称，因为它要求用户了解可用类别和供应商及其正确的拼写。

"供应商" 和 "类别" 字段应在处于只读模式时显示类别和供应商的名称（如同现在一样），并在编辑时提供适用选项的下拉列表。 使用下拉列表，最终用户可以快速查看哪些类别和供应商可供选择，并且可以更轻松地进行选择。

为了提供此行为，我们需要将 `SupplierName` 和 `CategoryName` BoundFields 转换为 Templatefield，其 `ItemTemplate` 发出 `SupplierName` 和 `CategoryName` 值，其 `EditItemTemplate` 使用 DropDownList 控件列出可用类别和供应商。

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>添加`Categories`和`Suppliers`DropDownLists

首先，将 "`SupplierName`" 和 "`CategoryName` BoundFields" 转换为 "Templatefield"，方法是单击 GridView 的智能标记上的 "编辑列" 链接;从左下方的列表中选择 BoundField;然后单击 "将此字段转换为 TemplateField" 链接。 转换过程将创建具有 `ItemTemplate` 和 `EditItemTemplate`的 TemplateField，如下面的声明性语法所示：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample4.aspx)]

由于 BoundField 被标记为只读，因此 `ItemTemplate` 和 `EditItemTemplate` 都包含一个标签 Web 控件，其 `Text` 属性绑定到相应的数据字段（在上述语法中为`CategoryName`）。 需要修改 `EditItemTemplate`，并将标签 Web 控件替换为 DropDownList 控件。

如前面的教程中所示，可以通过设计器或直接从声明性语法编辑模板。 若要通过设计器对其进行编辑，请从 GridView 的智能标记中单击 "编辑模板" 链接，然后选择使用 "类别" 字段的 `EditItemTemplate`。 删除标签 Web 控件，并将其替换为 DropDownList 控件，并将 DropDownList 的 ID 属性设置为 `Categories`。

[![删除文本框并将 DropDownList 添加到 EditItemTemplate](customizing-the-data-modification-interface-vb/_static/image14.png)](customizing-the-data-modification-interface-vb/_static/image13.png)

**图 5**：删除文本框并将 DropDownList 添加到 `EditItemTemplate` （[单击查看完全大小的图像](customizing-the-data-modification-interface-vb/_static/image15.png)）

接下来，需要使用可用类别来填充 DropDownList。 在 DropDownList 的智能标记中单击 "选择数据源" 链接，并选择创建名为 `CategoriesDataSource`的新 ObjectDataSource。

[![创建一个名为 CategoriesDataSource 的新 ObjectDataSource 控件](customizing-the-data-modification-interface-vb/_static/image17.png)](customizing-the-data-modification-interface-vb/_static/image16.png)

**图 6**：创建名为 `CategoriesDataSource` 的新 ObjectDataSource 控件（[单击以查看完全大小的图像](customizing-the-data-modification-interface-vb/_static/image18.png)）

若要让此 ObjectDataSource 返回所有类别，请将其绑定到 `CategoriesBLL` 类的 `GetCategories()` 方法。

[![将 ObjectDataSource 绑定到 CategoriesBLL 的 GetCategories （）方法](customizing-the-data-modification-interface-vb/_static/image20.png)](customizing-the-data-modification-interface-vb/_static/image19.png)

**图 7**：将 ObjectDataSource 绑定到 `CategoriesBLL`的 `GetCategories()` 方法（[单击以查看完全大小的映像](customizing-the-data-modification-interface-vb/_static/image21.png)）

最后，配置 DropDownList 的设置，使 "`CategoryName`" 字段显示在每个 DropDownList `ListItem` 中，并使用用作值 `CategoryID` 字段。

[![显示 "类别名称" 字段，并使用 "类别 Id" 作为值](customizing-the-data-modification-interface-vb/_static/image23.png)](customizing-the-data-modification-interface-vb/_static/image22.png)

**图 8**：显示 "`CategoryName`" 字段并将 `CategoryID` 用作值（[单击以查看完全大小的图像](customizing-the-data-modification-interface-vb/_static/image24.png)）

进行这些更改后，`CategoryName` TemplateField 中的 `EditItemTemplate` 的声明性标记将同时包含 DropDownList 和 ObjectDataSource：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> `EditItemTemplate` 中的 DropDownList 必须启用其视图状态。 我们很快会将 databinding 语法添加到 DropDownList 的声明性语法和数据绑定命令，例如 `Eval()` 和 `Bind()` 只能出现在启用了视图状态的控件中。

重复上述步骤，将名为 `Suppliers` 的 DropDownList 添加到 `SupplierName` TemplateField 的 `EditItemTemplate`。 这涉及到将 DropDownList 添加到 `EditItemTemplate` 并创建另一个 ObjectDataSource。 但 `Suppliers` DropDownList 的 ObjectDataSource 应配置为调用 `SuppliersBLL` 类的 `GetSuppliers()` 方法。 此外，配置 `Suppliers` DropDownList 以显示 `CompanyName` 字段，并使用 `SupplierID` 字段作为其 `ListItem` 的值。

将 DropDownLists 添加到两个 `EditItemTemplate` "后，在浏览器中加载页面，并单击 Chef Anton 的 Cajun Seasoning product 的" 编辑 "按钮。 如图9所示，该产品的类别和供应商列呈现为下拉列表，其中包含可供选择的可用类别和供应商。 但请注意，在默认情况下，这两个下拉列表中的*第一*项处于选中状态（类别的饮料和现 Liquids 作为供应商），尽管 Chef Anton 的 Cajun Seasoning 是由新奥尔良 Condiment Cajun 提供的乐趣。

[默认情况下，下拉列表中的第一项 ![处于选中状态](customizing-the-data-modification-interface-vb/_static/image26.png)](customizing-the-data-modification-interface-vb/_static/image25.png)

**图 9**：默认情况下，下拉列表中的第一项处于选中状态（[单击以查看完全大小的图像](customizing-the-data-modification-interface-vb/_static/image27.png)）

此外，如果单击 "更新"，会发现产品的 `CategoryID` 和 `SupplierID` 值设置为 "`NULL`"。 这两种不需要的行为都是因为 `EditItemTemplate` 中的 DropDownLists 未绑定到基础产品数据中的任何数据字段。

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>将 DropDownLists 绑定到`CategoryID`和`SupplierID`数据字段

为了使已编辑的产品的类别和供应商下拉列表设置为适当的值，并在单击 "更新" 后将这些值发回到 BLL 的 `UpdateProduct` 方法，我们需要使用双向数据绑定将 DropDownLists 的 `SelectedValue` 属性绑定到 `CategoryID` 和 `SupplierID` 数据字段。 若要通过 `Categories` DropDownList 来实现此目的，可以直接将 `SelectedValue='<%# Bind("CategoryID") %>'` 添加到声明性语法。

或者，你可以通过在设计器中编辑模板并单击 DropDownList 的智能标记的 "编辑 databinding" 链接来设置 DropDownList 的绑定。 接下来，指示应使用双向数据绑定将 `SelectedValue` 属性绑定到 `CategoryID` 字段（请参阅图10）。 重复声明性或设计器过程以将 `SupplierID` 数据字段绑定到 `Suppliers` DropDownList。

[![使用双向数据绑定将类别 Id 绑定到 DropDownList 的 SelectedValue 属性](customizing-the-data-modification-interface-vb/_static/image29.png)](customizing-the-data-modification-interface-vb/_static/image28.png)

**图 10**：使用双向数据绑定将 `CategoryID` 绑定到 DropDownList 的 `SelectedValue` 属性（[单击以查看完全大小的图像](customizing-the-data-modification-interface-vb/_static/image30.png)）

将绑定应用于这两个 DropDownLists 的 `SelectedValue` 属性后，编辑后的产品的 "类别" 和 "供应商" 列将默认为当前产品的值。 单击 "更新" 后，所选下拉列表项的 `CategoryID` 和 `SupplierID` 值将传递给 `UpdateProduct` 方法。 图11显示了数据绑定语句添加后的教程;请注意，Chef Anton 的 Cajun Seasoning 的选定下拉列表项如何正确 Condiment Cajun 和新奥尔良乐趣。

[默认情况下，将选择所编辑的产品的当前类别和供应商值 ![](customizing-the-data-modification-interface-vb/_static/image32.png)](customizing-the-data-modification-interface-vb/_static/image31.png)

**图 11**：默认情况下已编辑的产品的当前类别和供应商值处于选中状态（[单击以查看完全大小的图像](customizing-the-data-modification-interface-vb/_static/image33.png)）

## <a name="handlingnullvalues"></a>处理`NULL`值

`Products` 表中的 `CategoryID` 和 `SupplierID` 列可以 `NULL`，但 `EditItemTemplate` 中的 DropDownLists 不包含用于表示 `NULL` 值的列表项。 这有两个后果：

- 用户无法使用我们的界面将产品的类别或供应商从非`NULL` 值更改为 `NULL` 一个
- 如果产品有 `NULL` `CategoryID` 或 `SupplierID`，则单击 "编辑" 按钮将导致异常。 这是因为 `Bind()` 语句中 `CategoryID` （或 `SupplierID`）返回的 `NULL` 值未映射到 DropDownList 中的值（在其 `SelectedValue` 属性设置为*不*在其列表项集合中的值时，DropDownList 会引发异常）。

为了支持 `NULL` `CategoryID` 和 `SupplierID` 值，我们需要向每个 DropDownList 添加另一个 `ListItem` 来表示 `NULL` 值。 在[使用 DropDownList 教程进行主/详细筛选](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)的教程中，我们看到了如何将其他 `ListItem` 添加到数据绑定 DropDownList，这涉及到将 DropDownList 的 `AppendDataBoundItems` 属性设置为 `True`，并手动添加其他 `ListItem`。 但在之前的教程中，我们添加了一个 `Value` `-1`的 `ListItem`。 但是，ASP.NET 中的数据绑定逻辑会自动将空字符串转换为 `NULL` 的值，反之亦然。 因此，在本教程中，我们希望 `ListItem`的 `Value` 为空字符串。

首先，将 DropDownLists "`AppendDataBoundItems` 属性设置为" `True`"。 接下来，通过将以下 `<asp:ListItem>` 元素添加到每个 DropDownList 来添加 `NULL` `ListItem`，以便声明性标记如下所示：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample6.aspx)]

我已经选择使用 "（无）" 作为此 `ListItem`的文本值，但如果您愿意，也可以将其更改为空白字符串。

> [!NOTE]
> 正如我们*使用 DropDownList 教程在主/详细信息筛选*中看到的那样，可以通过在 "属性窗口" 中单击 DropDownList 的 `Items` 属性（将显示 `ListItem` 集合编辑器），将 `ListItem` 添加到 DropDownList 中。 但是，请务必通过声明性语法将 `NULL` `ListItem` 添加到本教程。 如果使用 `ListItem` 集合编辑器，则生成的声明性语法将在分配空字符串时完全省略 `Value` 设置，创建类似于以下内容的声明性标记： `<asp:ListItem>(None)</asp:ListItem>`。 虽然这看起来可能无害，但缺少值会导致 DropDownList 使用 `Text` 属性值。 这意味着，如果选择此 `NULL` `ListItem`，则会将值 "（无）" 分配给 `CategoryID`，这将导致异常。 通过显式设置 `Value=""`，选择 `NULL` `ListItem` 时，`NULL` 值将分配给 `CategoryID`。

为 "供应商 DropDownList" 重复这些步骤。

使用此附加 `ListItem`，编辑界面现在可以将 `NULL` 值分配给产品的 `CategoryID` 和 `SupplierID` 字段，如图12所示。

[![选择 "（无）" 为产品的类别或供应商分配 NULL 值](customizing-the-data-modification-interface-vb/_static/image35.png)](customizing-the-data-modification-interface-vb/_static/image34.png)

**图 12**：选择 "（无）" 可为产品的类别或供应商分配 `NULL` 值（[单击查看全尺寸图像](customizing-the-data-modification-interface-vb/_static/image36.png)）

## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>步骤4：将单选按钮用于中止状态

当前，使用 CheckBoxField 表示产品的 `Discontinued` 数据字段，该字段为只读行呈现禁用的复选框，并为正在编辑的行呈现 "已启用" 复选框。 虽然此用户界面通常适用，但如果需要，可以使用 TemplateField 对其进行自定义。 对于本教程，让我们将 CheckBoxField 更改为使用 RadioButtonList 控件的 TemplateField，该控件具有两个选项 "活动" 和 "已停用"，用户可以从中指定产品的 `Discontinued` 值。

首先将 `Discontinued` CheckBoxField 转换为 TemplateField，这将创建具有 `ItemTemplate` 和 `EditItemTemplate`的 TemplateField。 这两个模板都包含一个复选框，其 `Checked` 属性绑定到 `Discontinued` 数据字段，两者的唯一区别在于 `ItemTemplate`的复选框的 `Enabled` 属性设置为 `False`。

用 RadioButtonList 控件替换 `ItemTemplate` 和 `EditItemTemplate` 中的复选框，同时将两个 RadioButtonLists 的 `ID` 属性都设置为 `DiscontinuedChoice`。 接下来，指示 RadioButtonLists 应包含两个单选按钮，其中一个标记为 "活动"，其值为 "False"，另一个标记为 "已停用"，值为 "True"。 若要实现此目的，可以直接通过声明性语法输入 `<asp:ListItem>` 元素，也可以使用设计器中的 "`ListItem` 集合编辑器"。 图13在指定了两个单选按钮选项后，显示了 "`ListItem` 集合编辑器"。

[![向 RadioButtonList 添加主动和废止选项](customizing-the-data-modification-interface-vb/_static/image38.png)](customizing-the-data-modification-interface-vb/_static/image37.png)

**图 13**：向 RadioButtonList 添加主动和废止选项（[单击以查看完全大小的映像](customizing-the-data-modification-interface-vb/_static/image39.png)）

由于 `ItemTemplate` 中的 RadioButtonList 不能是可编辑的，因此请将其 `Enabled` 属性设置为 `False`，并将 `Enabled` 属性保留为 `True` （默认值），以 `EditItemTemplate`中的 RadioButtonList。 这会使未编辑的行中的单选按钮成为只读的，但允许用户更改已编辑行的单选按钮值。

我们仍需要分配 RadioButtonList 控件的 `SelectedValue` 属性，以便根据产品的 `Discontinued` 数据字段选择相应的单选按钮。 与本教程前面所述的 DropDownLists 一样，此数据绑定语法可以直接添加到声明性标记中，也可以通过 RadioButtonLists 的智能标记中的 "编辑数据绑定" 链接添加。

添加这两个 RadioButtonLists 并对其进行配置后，`Discontinued` TemplateField 的声明性标记应如下所示：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample7.aspx)]

进行这些更改后，`Discontinued` 列已从复选框列表转换为单选按钮对列表（参见图14）。 编辑产品时，将选择相应的单选按钮，然后可以通过选择 "其他" 单选按钮并单击 "更新" 来更新产品的已中止状态。

[![中止的复选框已被单选按钮对替换](customizing-the-data-modification-interface-vb/_static/image41.png)](customizing-the-data-modification-interface-vb/_static/image40.png)

**图 14**：停用的复选框已被单选按钮对替代（[单击以查看完全大小的图像](customizing-the-data-modification-interface-vb/_static/image42.png)）

> [!NOTE]
> 由于 `Products` 数据库中的 `Discontinued` 列不能具有 `NULL` 值，因此我们无需担心捕获接口中的 `NULL` 信息。 但是，如果 `Discontinued` 列可以包含 `NULL` 值，我们想要将第三个单选按钮添加到列表中，将其 `Value` 设置为空字符串（`Value=""`），就像类别和供应 DropDownLists 一样。

## <a name="summary"></a>总结

尽管 BoundField 和 CheckBoxField 会自动呈现只读、编辑和插入界面，但它们缺乏自定义功能。 但通常，我们需要自定义编辑或插入界面，可能会添加验证控件（如前面教程中所述）或自定义数据收集用户界面（如本教程中所述）。 在以下步骤中，可以使用 TemplateField 自定义接口：

1. 添加 TemplateField 或将现有的 BoundField 或 CheckBoxField 转换为 TemplateField
2. 根据需要增加接口
3. 使用双向数据绑定将相应的数据字段绑定到新添加的 Web 控件

除了使用内置的 ASP.NET Web 控件以外，还可以使用自定义的已编译服务器控件和用户控件自定义 TemplateField 的模板。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
> [下一页](implementing-optimistic-concurrency-vb.md)
