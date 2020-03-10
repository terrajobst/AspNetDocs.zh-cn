---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-cs
title: 从 GridView 的页脚插入新记录（C#） |Microsoft Docs
author: rick-anderson
description: 尽管 GridView 控件不提供用于插入新数据记录的内置支持，但本教程介绍了如何增加 GridView，使其包含 。
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 49545652-98af-46ba-9dbc-9ab529805d9b
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: 6b337fe395a0ed54b03767111e73ea6d6c0ba23a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78477524"
---
# <a name="inserting-a-new-record-from-the-gridviews-footer-c"></a>从 GridView 页脚插入新记录 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_CS.exe)或[下载 PDF](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/datatutorial53cs1.pdf)

> 尽管 GridView 控件不提供用于插入新数据记录的内置支持，但本教程介绍了如何增加 GridView 以包含插入接口。

## <a name="introduction"></a>简介

如在[插入、更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程中所述，GridView、DetailsView 和 FormView Web 控件都包含内置的数据修改功能。 与声明性数据源控件一起使用时，可以快速轻松地将这三个 Web 控件配置为修改数据和方案，而无需编写单行代码。 遗憾的是，只有 DetailsView 和 FormView 控件提供内置的插入、编辑和删除功能。 GridView 仅提供编辑和删除支持。 不过，有一点弯头硅脂，我们可以增加 GridView，使其包括插入界面。

在将插入功能添加到 GridView 中时，我们负责确定新记录的添加方式、创建插入界面以及编写代码以插入新记录。 在本教程中，我们将了解如何将插入界面添加到 GridView 的页脚行（请参阅图1）。 每个列的页脚单元包括相应的数据收集用户界面元素（产品的 "名称" 文本框、供应商的 DropDownList 等）。 我们还需要一个 "添加" 按钮列，单击该按钮将导致回发，并使用脚注行中提供的值将新记录插入到 `Products` 表中。

[![页脚行为添加新产品提供了一个接口](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image1.png)

**图 1**：页脚行为添加新产品提供了一个接口（[单击以查看完全大小的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image2.png)）

## <a name="step-1-displaying-product-information-in-a-gridview"></a>步骤1：在 GridView 中显示产品信息

在我们考虑在 GridView 的页脚中创建插入界面之前，首先要重点介绍如何向列出数据库中产品的页面添加 GridView。 首先打开 `EnhancedGridView` 文件夹中的 "`InsertThroughFooter.aspx`" 页，然后从 "工具箱" 中将一个 GridView 拖到设计器上，将 GridView s `ID` 属性设置为 "`Products`"。 接下来，使用 GridView s 智能标记将其绑定到名为 `ProductsDataSource`的新 ObjectDataSource。

[![创建一个名为 ProductsDataSource 的新 ObjectDataSource](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image3.png)

**图 2**：创建名为 `ProductsDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image4.png)）

将 ObjectDataSource 配置为使用 `ProductsBLL` 类 `GetProducts()` 方法来检索产品信息。 对于本教程，让我们严格关注如何添加插入功能，而无需担心编辑和删除。 因此，请确保 "插入" 选项卡中的下拉列表设置为 "`AddProduct()`"，并且 "更新" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。

[![将 AddProduct 方法映射到 ObjectDataSource s Insert （）方法](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image5.png)

**图 3**：将 `AddProduct` 方法映射到 ObjectDataSource s `Insert()` 方法（[单击以查看完全大小的映像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image6.png)）

[![将 "更新和删除选项卡" 下拉列表设置为 "（无）"](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image7.png)

**图 4**：将 "更新" 和 "删除选项卡" 下拉列表设置为 "（无）" （[单击查看完全大小的映像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image8.png)）

完成 ObjectDataSource 的 "配置数据源" 向导后，Visual Studio 将为每个相应的数据字段自动向 GridView 添加字段。 现在，保留 Visual Studio 添加的所有字段。 稍后在本教程中，我们将返回并删除一些字段，这些字段的值在添加新记录时需要指定。

由于数据库中有近80的产品，用户必须一直向下滚动到网页底部，以便添加新的记录。 因此，让我们启用分页，使插入接口更可见且更易访问。 若要启用分页，只需从 GridView s 智能标记中选中 "启用分页" 复选框。

此时，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample1.aspx)]

[![所有产品数据字段都显示在分页 GridView 中](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image9.png)

**图 5**：所有产品数据字段都显示在分页 GridView 中（[单击以查看完全大小的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image10.png)）

## <a name="step-2-adding-a-footer-row"></a>步骤2：添加脚注行

除了其标头和数据行以外，GridView 还包括一个页脚行。 显示表头和表尾行，具体取决于 GridView [`ShowHeader`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showheader.aspx)和[`ShowFooter`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showfooter.aspx)属性的值。 若要显示页脚行，只需将 `ShowFooter` 属性设置为 `true`。 如图6所示，将 `ShowFooter` 属性设置为 `true` 将页脚行添加到网格。

[![，若要显示页脚行，请将 ShowFooter 设置为 True](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image11.png)

**图 6**：若要显示页脚行，请将 `ShowFooter` 设置为 `True` （[单击查看完全大小的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image12.png)）

请注意，页脚行的背景色为深红色。 这是因为我们已创建 DataWebControls 主题，并将其应用到了[通过 ObjectDataSource 教程显示数据](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)的所有页面。 具体而言，`GridView.skin` 文件配置 `FooterStyle` 属性，以便使用 `FooterStyle` CSS 类。 `FooterStyle` 类在 `Styles.css` 中定义，如下所示：

[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample2.css)]

> [!NOTE]
> 我们已在前面的教程中使用了 GridView s 的页脚行。 如果需要，请参阅[GridView 页脚教程中的显示](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md)刷新程序的摘要信息。

将 `ShowFooter` 属性设置为 "`true`" 后，请花点时间在浏览器中查看输出。 当前页脚行不包含任何文本或 Web 控件。 在步骤3中，我们将修改每个 GridView 字段的页脚，使其包括适当的插入界面。

[![在分页界面控件上方显示空页脚行](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image13.png)

**图 7**：在分页界面控件上方显示空的页脚行（[单击以查看完全大小的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image14.png)）

## <a name="step-3-customizing-the-footer-row"></a>步骤3：自定义页脚行

返回到 GridView 控件教程中的[使用 templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) ，我们看到了如何使用 templatefield （而不是 BoundFields 或 CheckBoxFields）极大地自定义特定 GridView 列的显示;[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)时，我们介绍了如何使用 templatefield 自定义 GridView 中的编辑界面。 请记住，TemplateField 由许多模板构成，这些模板定义了用于某些类型的行的标记、Web 控件和数据绑定语法的混合。 例如，`ItemTemplate`指定用于只读行的模板，而 `EditItemTemplate` 定义可编辑行的模板。

除了 `ItemTemplate` 和 `EditItemTemplate`，TemplateField 还包括一个指定脚注行的内容的 `FooterTemplate`。 因此，我们可以将插入接口的每个字段所需的 Web 控件添加到 `FooterTemplate`中。 若要开始，请将 GridView 中的所有字段转换为 Templatefield。 若要完成此操作，可以单击 GridView s 智能标记中的 "编辑列" 链接，选择左下角的每个字段，然后单击 "将此字段转换为 TemplateField" 链接。

![将每个字段转换为 TemplateField](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image8.gif)

**图 8**：将每个字段转换为 TemplateField

单击 "将此字段转换为 TemplateField" 可将当前字段类型变为等效的 TemplateField。 例如，每个 BoundField 都将替换为带有 `ItemTemplate` 的 TemplateField，其中包含一个显示相应数据字段的标签和一个显示文本框中的数据字段的 `EditItemTemplate`。 `ProductName` BoundField 已转换为以下 TemplateField 标记：

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample3.aspx)]

同样，`Discontinued` CheckBoxField 已转换为 `ItemTemplate`，`EditItemTemplate` 包含复选框 Web 控件（禁用了 `ItemTemplate` 的复选框）。 只读 `ProductID` BoundField 已转换为 TemplateField，并在 "`ItemTemplate`" 和 "`EditItemTemplate`" 中具有 "标签" 控件。 简而言之，将现有 GridView 字段转换为 TemplateField 是一种快速简便的方法，可用于切换到更具自定义的 TemplateField，而不会丢失任何现有的字段功能。

由于我们重新使用的 GridView 不支持编辑，因此可随意从每个 TemplateField 删除 `EditItemTemplate`，只需 `ItemTemplate`。 完成此操作后，GridView 的声明性标记应如下所示：

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample4.aspx)]

由于已将每个 GridView 字段转换为 TemplateField，因此可以在 `FooterTemplate`的每个字段中输入相应的插入界面。 某些字段将不包含插入接口（例如`ProductID`）;其他人会在用于收集新产品信息的 Web 控件中有所不同。

若要创建编辑界面，请从 GridView s 智能标记中选择 "编辑模板" 链接。 然后，从下拉列表中选择相应的字段 "`FooterTemplate` 并将相应的控件从工具箱拖动到设计器上。

[![将相应的插入界面添加到每个字段 FooterTemplate](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image15.png)

**图 9**：将适当的插入界面添加到 `FooterTemplate` 的每个字段（[单击以查看完全大小的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image16.png)）

下面的项目符号列表枚举 GridView 字段，并指定要添加的插入接口：

- 无 `ProductID`。
- `ProductName` 添加文本框，并将其 `ID` 设置为 "`NewProductName`"。 同时添加 RequiredFieldValidator 控件，以确保用户输入新产品名称的值。
- 无 `SupplierID`。
- 无 `CategoryID`。
- `QuantityPerUnit` 添加文本框，并将其 `ID` 设置为 "`NewQuantityPerUnit`"。
- `UnitPrice` 添加一个名为 `NewUnitPrice` 的文本框和一个确保输入的值为大于或等于零的 CompareValidator。
- `UnitsInStock` 使用 `ID` 设置为 "`NewUnitsInStock`" 的文本框。 包括一个 CompareValidator，它确保输入的值为大于或等于零的整数值。
- `UnitsOnOrder` 使用 `ID` 设置为 "`NewUnitsOnOrder`" 的文本框。 包括一个 CompareValidator，它确保输入的值为大于或等于零的整数值。
- `ReorderLevel` 使用 `ID` 设置为 "`NewReorderLevel`" 的文本框。 包括一个 CompareValidator，它确保输入的值为大于或等于零的整数值。
- `Discontinued` 添加一个复选框，将其 `ID` 设置为 "`NewDiscontinued`"。
- `CategoryName` 添加 DropDownList 并将其 `ID` 设置为 "`NewCategoryID`"。 将其绑定到名为 `CategoriesDataSource` 的新 ObjectDataSource，并将其配置为使用 `CategoriesBLL` class s `GetCategories()` 方法。 使 DropDownList `ListItem` s 显示 `CategoryName` 数据字段，并使用 `CategoryID` 数据字段作为其值。
- `SupplierName` 添加 DropDownList 并将其 `ID` 设置为 "`NewSupplierID`"。 将其绑定到名为 `SuppliersDataSource` 的新 ObjectDataSource，并将其配置为使用 `SuppliersBLL` class s `GetSuppliers()` 方法。 使 DropDownList `ListItem` s 显示 `CompanyName` 数据字段，并使用 `SupplierID` 数据字段作为其值。

对于每个验证控件，请清除 "`ForeColor`" 属性，以便将使用 `FooterStyle` CSS 类的 "白色" 前景色替换为默认的红色。 另外，请使用 `ErrorMessage` 属性获取详细说明，但将 `Text` 属性设置为星号。 若要防止验证控制文本导致插入接口环绕两行，请将使用验证控件的每个 `FooterTemplate` 的 `FooterStyle` s `Wrap` 属性设置为 false。 最后，在 GridView 下面添加 ValidationSummary 控件，并将其 `ShowMessageBox` 属性设置为 "`true`"，并将其 `ShowSummary` 属性设置为 "`false`"。

添加新产品时，需要提供 `CategoryID` 和 `SupplierID`。 此信息通过 "`CategoryName`" 和 "`SupplierName`" 字段的页脚单元格中的 DropDownLists 捕获。 我选择使用这些字段，而不是 `CategoryID` 和 `SupplierID` Templatefield，因为在网格的数据行中，用户可能更希望查看类别和供应商名称而不是其 ID 值。 由于 `CategoryID` 和 `SupplierID` 值现在正在 `CategoryName` 中捕获，并 `SupplierName` 字段 s s 插入接口，因此可以从 GridView 中删除 `CategoryID` 和 `SupplierID` Templatefield。

同样，添加新产品时不使用 `ProductID`，因此也可以删除 `ProductID` TemplateField。 不过，让我们将 "`ProductID`" 字段保留在网格中。 除了组成插入界面的 textbox、DropDownLists、Checkbox 和验证控件外，我们还需要一个 "添加" 按钮，单击该按钮可执行逻辑以将新产品添加到数据库中。 在步骤4中，我们将在 `ProductID` TemplateField s `FooterTemplate`的插入界面中包含一个 "添加" 按钮。

可随意提高各种 GridView 字段的外观。 例如，您可能希望将 `UnitPrice` 值设置为货币格式，将 `UnitsInStock`、`UnitsOnOrder`和 `ReorderLevel` 字段右对齐，并更新 Templatefield 的 `HeaderText` 值。

创建在 `FooterTemplate` 中插入接口的许多、删除 `SupplierID`和 `CategoryID` Templatefield，并通过格式设置和对齐 Templatefield 来改善网格美观后，GridView 的声明性标记应如下所示：

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample5.aspx)]

通过浏览器查看时，GridView 的页脚行现在包含已完成的插入界面（请参阅图10）。 此时，插入接口并不包含一种方法，指示她为新产品输入了数据，并想要在数据库中插入新记录。 此外，我们还需要解决在页脚中输入的数据如何转换为 `Products` 数据库中的新记录。 在步骤4中，我们将介绍如何在插入界面中包含 "添加" 按钮，以及如何在单击时在回发时执行代码。 步骤5演示了如何使用页脚中的数据插入新记录。

["GridView" 页脚 ![提供用于添加新记录的接口](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image17.png)

**图 10**： GridView 页脚提供了一个用于添加新记录的接口（[单击以查看完全大小的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image18.png)）

## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>步骤4：在插入界面中包含 "添加" 按钮

我们需要在插入界面中的某个位置包含一个 "添加" 按钮，因为 "页脚行" 插入接口目前缺少用户指示用户已完成输入新的产品信息的方法。 这可以放置在现有 `FooterTemplate` 之一中，也可以将新列添加到网格以实现此目的。 对于本教程，请将 "添加" 按钮置于 `ProductID` TemplateField s `FooterTemplate`中。

在设计器中，单击 "GridView s 智能" 标记中的 "编辑模板" 链接，然后从下拉列表中选择 "`ProductID` 字段" `FooterTemplate`。 向模板中添加一个按钮 Web 控件（或 LinkButton 或 ImageButton，如果需要），将其 ID 设置为 "`AddProduct`"，将其 `CommandName` 设置为 "插入"，并将其 `Text` 属性设置为 "添加"，如图11所示。

[![将 "添加" 按钮放入 ProductID TemplateField s FooterTemplate](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image19.png)

**图 11**：将 "添加" 按钮置于 `ProductID` TemplateField s `FooterTemplate` （[单击以查看完全大小的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image20.png)）

一旦您包含 "添加" 按钮，即可在浏览器中测试页面。 请注意，当在插入界面中单击带有无效数据的 "添加" 按钮时，回发是短路的，而 ValidationSummary 控件会指示无效数据（见图12）。 输入适当的数据后，单击 "添加" 按钮会导致回发。 但不会将任何记录添加到数据库中。 我们需要编写一些代码来实际执行插入。

[![如果插入接口中有无效的数据，则 "添加" 按钮的回发短路较短](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image21.png)

**图 12**：如果插入接口中有无效的数据，则 "添加" 按钮的回发是短暂的短路（[单击查看完全大小的图像](inserting-a-new-record-from-the-gridview-s-footer-cs/_static/image22.png)）

> [!NOTE]
> 插入接口中的验证控件未分配给验证组。 只要插入接口是页面上唯一的验证控件集，这就可以正常工作。 但是，如果页面上有其他验证控件（如网格编辑界面中的验证控件），则应为插入接口中的验证控件和添加按钮 `ValidationGroup` 属性指定相同的值，以便将这些控件与特定的验证组相关联。 有关将页上的验证控件和按钮分区到验证组的详细信息，请参阅[二级 the ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)。

## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>步骤5：将新记录插入到`Products`表中

利用 GridView 的内置编辑功能时，GridView 会自动处理执行更新所需的所有工作。 具体而言，当单击 "更新" 按钮时，它会将从编辑界面输入的值复制到 ObjectDataSource `UpdateParameters` 集合中的参数，并通过调用 ObjectDataSource s `Update()` 方法来启动更新。 由于 GridView 并不提供用于插入的内置功能，因此必须实现调用 ObjectDataSource `Insert()` 方法的代码，并将插入接口中的值复制到 ObjectDataSource 的 `InsertParameters` 集合。

此插入逻辑应在单击 "添加" 按钮后执行。 如 LinkButton 中的 "[添加和响应" 按钮](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs.md)教程中所述，在 gridview 中单击按钮、或 ImageButton 时，在回发时将激发 gridview `RowCommand` 事件。 此事件将在以下情况下引发：是否显式添加了 Button、LinkButton 或 ImageButton （如脚注行中的 "添加" 按钮），或者是否自动添加了 GridView （例如，选中 "启用排序" 时每个列顶部的 LinkButtons，或选中 "启用分页" 时，寻呼界面中的 LinkButtons。

因此，若要响应用户单击 "添加" 按钮，需要为 GridView `RowCommand` 事件创建事件处理程序。 由于在 GridView 中单击*任何*按钮、LinkButton 或 ImageButton 时，将触发此事件，因此，如果传递到事件处理程序的 `CommandName` 属性映射到 "添加" 按钮（Insert）的 `CommandName` 值，则只会继续插入逻辑。 此外，如果验证控件报告了有效数据，则还应继续。 为此，请使用以下代码为 `RowCommand` 事件创建事件处理程序：

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample6.cs)]

> [!NOTE]
> 您可能想知道为什么事件处理程序麻烦检查 `Page.IsValid` 属性。 毕竟，如果插入接口中提供的数据无效，则不会禁止回发？ 只要用户未禁用 JavaScript 或已采取步骤来绕过客户端验证逻辑，此假设就是正确的。 简而言之，绝不会严格依赖于客户端验证;在处理数据之前，应始终执行服务器端检查的有效性。

在步骤1中，我们创建了 `ProductsDataSource` ObjectDataSource，使其 `Insert()` 方法映射到 `ProductsBLL` 类的 `AddProduct` 方法。 若要将新记录插入到 `Products` 表中，只需调用 ObjectDataSource s `Insert()` 方法即可：

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample7.cs)]

现在已调用 `Insert()` 方法，接下来要做的就是将插入接口中的值复制到传递给 `ProductsBLL` class s `AddProduct` 方法的参数。 正如我们所看到的，在[检查与插入、更新和删除教程相关的事件](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)时，可以通过 ObjectDataSource `Inserting` 事件完成此操作。 在 `Inserting` 事件中，我们需要以编程方式引用 `Products` GridView s 脚注行中的控件，并将它们的值分配给 `e.InputParameters` 集合。 如果用户省略了一个值，例如将 "`ReorderLevel`" 文本框留空，则需要指定是否应 `NULL`插入到数据库中的值。 由于 `AddProducts` 方法接受可为 null 的数据库字段的可以为 null 的类型，因此只需使用可以为 null 的类型，并将其值设置为在省略 user 输入的情况下 `null`。

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample8.cs)]

完成 `Inserting` 事件处理程序后，可以通过 GridView s 脚注行将新记录添加到 `Products` 数据库表中。 继续尝试添加几个新产品。

## <a name="enhancing-and-customizing-the-add-operation"></a>增强和自定义添加操作

目前，单击 "添加" 按钮可向数据库表中添加一条新记录，但不会提供记录已成功添加的任何视觉反馈。 理想情况下，"标签 Web 控件" 或 "客户端警报" 框将通知用户其插入已成功完成。 我将此留给读者的练习。

本教程中使用的 GridView 并不会对列出的产品应用任何排序顺序，也不允许最终用户对数据进行排序。 因此，记录按其主键字段在数据库中排序。 由于每个新记录的 `ProductID` 值都大于最后一个，因此，每次添加新的产品时，它都将堆积到网格的结尾。 因此，您可能希望在添加新记录后将用户自动发送到 GridView 的最后一页。 这可以通过在 `RowCommand` 事件处理程序中的 `ProductsDataSource.Insert()` 调用后添加以下代码行来实现，以指示在将数据绑定到 GridView 后，需要将用户发送到最后一页：

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample9.cs)]

`SendUserToLastPage` 是最初为其赋值 `false`的页级布尔变量。 在 GridView `DataBound` 事件处理程序中，如果 `SendUserToLastPage` 为 false，则更新 `PageIndex` 属性以将用户发送到最后一页。

[!code-csharp[Main](inserting-a-new-record-from-the-gridview-s-footer-cs/samples/sample10.cs)]

在 `DataBound` 事件处理程序（而不是 `RowCommand` 事件处理程序）中设置 `PageIndex` 属性的原因是，当 `RowCommand` 事件处理程序触发时，我们还需要将新记录添加到 `Products` 数据库表中。 因此，在 `RowCommand` 事件处理程序中，最后一页索引（`PageCount - 1`）表示添加新产品*之前*的最后一页索引。 对于添加的大部分产品，最后一页索引在添加新产品后是相同的。 但当添加的产品产生新的最后一页索引时，如果在 `RowCommand` 事件处理程序中错误地更新 `PageIndex`，则将转到第二页到最后一页（添加新产品之前的最后一页索引），而不是新的最后一页索引。 由于在添加新产品和将数据重新绑定到网格后会触发 `DataBound` 事件处理程序，因此，通过设置 `PageIndex` 属性，我们知道我们会获得正确的最后一页索引。

最后，本教程中使用的 GridView 非常广泛，因为为了添加新产品必须收集字段数。 由于此宽度的原因，可能首选 DetailsView s 垂直布局。 可以通过收集更少的输入来减少 GridView 的整体宽度。 我们可能不需要在添加新产品时收集 `UnitsOnOrder`、`UnitsInStock`和 `ReorderLevel` 字段，在这种情况下，可以从 GridView 中删除这些字段。

若要调整收集的数据，可以使用以下两种方法之一：

- 继续使用需要 `UnitsOnOrder`、`UnitsInStock`和 `ReorderLevel` 字段值的 `AddProduct` 方法。 在 `Inserting` 事件处理程序中，提供硬编码的默认值，这些默认值用于已从插入接口中删除的输入。
- 在 `ProductsBLL` 类中创建不接受 `UnitsOnOrder`、`UnitsInStock`和 `ReorderLevel` 字段输入的 `AddProduct` 方法的新重载。 然后，在 "ASP.NET" 页中，将 ObjectDataSource 配置为使用此新的重载。

这两个选项也同样适用。 在过去的教程中，我们使用后一种方法，为 `ProductsBLL` 类 `UpdateProduct` 方法创建多个重载。

## <a name="summary"></a>摘要

GridView 缺少在 DetailsView 和 FormView 中找到的内置插入功能，但有很大努力可以将插入界面添加到脚注行。 若要在 GridView 中显示页脚行，只需将其 `ShowFooter` 属性设置为 `true`。 可以通过将字段转换为 TemplateField 并将插入接口添加到 `FooterTemplate`为每个字段自定义页脚行内容。 如本教程中所述，`FooterTemplate` 可以包含按钮、文本框、DropDownLists、Checkbox、用于填充数据驱动的 Web 控件的数据源控件（如 DropDownLists）和验证控件。 除了收集用户输入的控件以外，还需要添加按钮、LinkButton 或 ImageButton。

单击 "添加" 按钮后，将调用 ObjectDataSource s `Insert()` 方法来启动插入工作流。 然后，ObjectDataSource 将调用配置的 insert 方法（本教程中的 `ProductsBLL` 类 `AddProduct` 方法）。 在调用 insert 方法之前，我们必须将来自 GridView s 的插入接口的值复制到 ObjectDataSource s `InsertParameters` 集合。 这可以通过以编程方式引用 `Inserting` 事件处理程序中的插入接口 Web 控件来实现。

本教程介绍了用于增强 GridView 外观的方法。 下一组教程将介绍如何处理二进制数据（如图像、Pdf、Word 文档等）以及数据 Web 控件。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Bernadette Leigh。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](adding-a-gridview-column-of-checkboxes-cs.md)
> [下一页](adding-a-gridview-column-of-radio-buttons-vb.md)
