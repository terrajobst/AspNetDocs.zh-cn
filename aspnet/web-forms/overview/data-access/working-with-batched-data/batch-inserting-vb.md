---
uid: web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
title: 批处理插入（VB） |Microsoft Docs
author: rick-anderson
description: 了解如何在一个操作中插入多个数据库记录。 在用户界面层，我们扩展了 GridView，以允许用户输入多个 n 。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 48e2a4ae-77ca-4208-a204-c38c690ffb59
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
msc.type: authoredcontent
ms.openlocfilehash: 413a0e209b1899414eaab70aff07ee0d3223f28f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78501488"
---
# <a name="batch-inserting-vb"></a>批量插入 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_66_VB.zip)或[下载 PDF](batch-inserting-vb/_static/datatutorial66vb1.pdf)

> 了解如何在一个操作中插入多个数据库记录。 在用户界面层，我们扩展了 GridView，以允许用户输入多个新记录。 在数据访问层中，我们将多个 Insert 操作打包到一个事务中，以确保所有插入操作成功或回滚所有插入操作。

## <a name="introduction"></a>简介

在[批处理更新](batch-updating-vb.md)教程中，我们将介绍如何自定义 GridView 控件以显示可编辑多个记录的接口。 访问此页的用户可能会进行一系列更改，然后单击一个按钮即可执行批更新。 对于用户经常在一步中更新多条记录的情况，这种情况下，与在[插入、更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教程的概述中首次查看的默认每行编辑功能相比，此类接口可以节省无数次单击和键盘到鼠标的上下文切换。

此概念还可在添加记录时应用。 假设在 Northwind 商贸这里，我们通常会收到来自供应商的装运，其中包含一系列特定类别的产品。 例如，我们可能会从东京商贸接收六个不同的茶和咖啡产品。 如果用户一次通过 DetailsView 控件输入了六个产品，则他们将需要反复选择多个相同的值：他们需要选择相同的类别（饮料）、相同的供应商（东京商贸），这是一个相同的废止值（False）和按顺序值（0）相同的单位。 此重复数据输入不仅费时，而且容易出错。

使用少许工作，我们可以创建一个批插入界面，使用户能够选择供应商和类别一次，输入一系列产品名称和单价，然后单击按钮将新产品添加到数据库中（请参阅图1）。 添加每个产品后，其 `ProductName` 和 `UnitPrice` 数据字段将被分配在文本框中输入的值，而其 `CategoryID` 和 `SupplierID` 值将从窗体顶部的 DropDownLists 中分配值。 `Discontinued` 和 `UnitsOnOrder` 值分别设置为 `False` 和0的硬编码值。

[![批插入接口](batch-inserting-vb/_static/image2.png)](batch-inserting-vb/_static/image1.png)

**图 1**：批插入接口（[单击以查看完全大小的图像](batch-inserting-vb/_static/image3.png)）

在本教程中，我们将创建一个页面，用于实现图1所示的批插入接口。 与前两个教程一样，我们将在事务范围内包装插入内容，以确保原子性。 让我们开始吧！

## <a name="step-1-creating-the-display-interface"></a>步骤1：创建显示界面

本教程将包含一个分为两个区域的页面：一个显示区域和一个插入区域。 将在此步骤中创建的显示界面显示 GridView 中的产品并包含一个标题为 "处理产品发货" 的按钮。 单击此按钮时，显示界面将替换为插入界面，如图1所示。 单击 "从发货中添加产品" 或 "取消" 按钮后返回显示界面。 我们将在步骤2中创建插入接口。

当创建一个具有两个接口的页时，每次只显示其中一个接口，每个接口通常放置在一个[面板 Web 控件](http://www.w3schools.com/aspnet/control_panel.asp)中，后者用作其他控件的容器。 因此，我们的页面将有两个面板控件用于每个接口。

首先打开 `BatchData` 文件夹中的 "`BatchInsert.aspx`" 页，然后将面板从工具箱拖到设计器上（参见图2）。 将 Panel `ID` 属性设置为 `DisplayInterface`。 将面板添加到设计器中时，其 `Height` 和 `Width` 属性分别设置为50px 和125px。 从属性窗口中清除这些属性值。

[![将面板从工具箱拖到设计器上](batch-inserting-vb/_static/image5.png)](batch-inserting-vb/_static/image4.png)

**图 2**：将面板从工具箱拖到设计器上（[单击以查看完全大小的图像](batch-inserting-vb/_static/image6.png)）

接下来，将按钮和 GridView 控件拖动到面板中。 将 "`ID`" 按钮设置为 "`ProcessShipment`"，并将其 "`Text`" 属性设置为 "处理产品发货"。 将 GridView `ID` 属性设置为 `ProductsGrid`，并从其智能标记将其绑定到名为 `ProductsDataSource`的新 ObjectDataSource。 将 ObjectDataSource 配置为从 `ProductsBLL` 类 `GetProducts` 方法拉取其数据。 由于此 GridView 仅用于显示数据，因此请将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。 单击 "完成" 以完成 "配置数据源" 向导。

[![显示从 ProductsBLL 类 s GetProducts 方法返回的数据](batch-inserting-vb/_static/image8.png)](batch-inserting-vb/_static/image7.png)

**图 3**：显示从 `ProductsBLL` 类 `GetProducts` 方法返回的数据（[单击查看完全大小的图像](batch-inserting-vb/_static/image9.png)）

[![在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"](batch-inserting-vb/_static/image11.png)](batch-inserting-vb/_static/image10.png)

**图 4**：将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的映像](batch-inserting-vb/_static/image12.png)）

完成 ObjectDataSource 向导后，Visual Studio 将为产品数据字段添加 BoundFields 和 CheckBoxField。 删除除 `ProductName`、`CategoryName`、`SupplierName`、`UnitPrice`和 `Discontinued` 字段之外的所有字段。 随意进行任何美观自定义。 我决定将 `UnitPrice` 字段的格式设置为货币值，对字段重新排序，然后将多个字段重命名为 `HeaderText` 值。 此外，通过选中 GridView s 智能标记中的 "启用分页" 和 "启用排序" 复选框，将 GridView 配置为包含分页和排序支持。

添加面板、按钮、GridView 和 ObjectDataSource 控件并自定义 GridView 字段之后，页面的声明性标记应如下所示：

[!code-aspx[Main](batch-inserting-vb/samples/sample1.aspx)]

请注意，按钮和 GridView 的标记出现在开始标记和结束标记 `<asp:Panel>` 中。 由于这些控件位于 `DisplayInterface` 面板内，因此，只需将面板的 `Visible` 属性设置为 `False`即可隐藏它们。 步骤3查看以编程方式更改面板的 `Visible` 属性，以响应按钮单击以显示一个接口，同时隐藏另一个接口。

花点时间通过浏览器查看进度。 如图5所示，你应该会看到一个 GridView 之上的 "处理产品发货" 按钮，该按钮每次列出产品10个。

[![GridView 列出产品并提供排序和分页功能](batch-inserting-vb/_static/image14.png)](batch-inserting-vb/_static/image13.png)

**图 5**： GridView 列出了产品并提供排序和分页功能（[单击查看完全尺寸的图像](batch-inserting-vb/_static/image15.png)）

## <a name="step-2-creating-the-inserting-interface"></a>步骤2：创建插入接口

显示界面完成后，便可以开始创建插入界面了。 对于本教程，让我们创建一个提示输入单个供应商和类别值的插入界面，然后允许用户输入最多五个产品名称和单位价格值。 使用此界面，用户可以添加一个到五个新产品，它们都共享同一类别和供应商，但具有唯一的产品名称和价格。

首先，将面板从工具箱拖到设计器上，将其放在现有 `DisplayInterface` 面板下。 将此新添加的面板的 `ID` 属性设置为 "`InsertingInterface`，并将其 `Visible` 属性设置为" `False`"。 我们将添加代码，用于将 `InsertingInterface` Panel s `Visible` 属性设置为步骤3中的 `True`。 同时，请清除面板 `Height` 和 `Width` 属性值。

接下来，我们需要创建图1中显示的插入接口。 此接口可通过各种 HTML 技术来创建，但我们将使用相当简单的一种方法：四列七行的表。

> [!NOTE]
> 为 HTML `<table>` 元素输入标记时，我更喜欢使用源视图。 尽管 Visual Studio 确实包含用于通过设计器添加 `<table>` 元素的工具，但设计器似乎都不愿意向标记中注入 `style` 设置的 unasked。 创建 `<table>` 标记后，通常会返回到设计器来添加 Web 控件并设置其属性。 使用预先确定的列和行创建表时，我喜欢使用静态 HTML 而不是[表 web 控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.table.aspx)，因为位于表 web 控件中的任何 Web 控件都只能通过 `FindControl("controlID")` 模式进行访问。 不过，我确实要对动态大小的表（其行或列基于某些数据库或用户指定的条件）使用表 Web 控件，因为表 Web 控件可以通过编程方式构造。

在 "`InsertingInterface`" 面板的 `<asp:Panel>` 标记中输入以下标记：

[!code-html[Main](batch-inserting-vb/samples/sample2.html)]

此 `<table>` 标记尚未包含任何 Web 控件，我们将稍后添加这些控件。 请注意，每个 `<tr>` 元素都包含一个特定 CSS 类设置： `BatchInsertHeaderRow` 用于供应商和类别 DropDownLists 的标题行;`BatchInsertFooterRow`，用于将 "从发货中添加产品" 和 "取消" 按钮的页脚行。和将包含 "产品" 和 "单价" 文本框控件的行的替换 `BatchInsertRow` 和 `BatchInsertAlternatingRow` 值。 我在 `Styles.css` 文件中创建了相应的 CSS 类，使插入界面的外观类似于我们在本教程中使用的 GridView 和 DetailsView 控件。 下面显示了这些 CSS 类。

[!code-css[Main](batch-inserting-vb/samples/sample3.css)]

输入此标记后，返回到设计视图。 此 `<table>` 应在设计器中显示为四列七行的表，如图6所示。

[![插入接口由四列七行的表组成](batch-inserting-vb/_static/image17.png)](batch-inserting-vb/_static/image16.png)

**图 6**：插入界面由四列七行表格组成（[单击以查看完全尺寸的图像](batch-inserting-vb/_static/image18.png)）

现在，我们已准备好将 Web 控件添加到插入接口。 将两个 "DropDownLists" 从 "工具箱" 拖动到表中的相应单元格，一个用于供应商，另一个用于类别。

将 "供应 DropDownList" `ID` 属性设置为 "`Suppliers` 并将其绑定到名为 `SuppliersDataSource`的新 ObjectDataSource。 配置新 ObjectDataSource 以便从 `SuppliersBLL` 类 `GetSuppliers` 方法检索其数据，并将 "更新" 选项卡 s 下拉列表设置为 "（无）"。 单击“完成”按钮以完成向导。

[![将 ObjectDataSource 配置为使用 SuppliersBLL Class s GetSuppliers 方法](batch-inserting-vb/_static/image20.png)](batch-inserting-vb/_static/image19.png)

**图 7**：将 ObjectDataSource 配置为使用 `SuppliersBLL` 类 `GetSuppliers` 方法（[单击以查看完全大小的映像](batch-inserting-vb/_static/image21.png)）

让 `Suppliers` DropDownList 显示 `CompanyName` 数据字段，并使用 `SupplierID` 数据字段作为其 `ListItem` 值。

[![显示 "公司名称" 数据字段，并使用供应商作为值](batch-inserting-vb/_static/image23.png)](batch-inserting-vb/_static/image22.png)

**图 8**：显示 "`CompanyName` 数据" 字段并使用 "`SupplierID`" 作为值（[单击以查看完全大小的图像](batch-inserting-vb/_static/image24.png)）

将第二个 DropDownList `Categories` 命名为，并将其绑定到名为 `CategoriesDataSource`的新 ObjectDataSource。 将 `CategoriesDataSource` ObjectDataSource 配置为使用 `CategoriesBLL` 类 `GetCategories` 方法;将 "更新" 和 "删除" 选项卡中的下拉列表设置为 "（无）"，然后单击 "完成" 以完成向导。 最后，使 DropDownList 显示 `CategoryName` 数据字段并使用 `CategoryID` 作为值。

添加这两个 DropDownLists 并将其绑定到正确配置的 Objectdatasource 后，屏幕应类似于图9。

[![标题行现在包含供应商和类别 DropDownLists](batch-inserting-vb/_static/image26.png)](batch-inserting-vb/_static/image25.png)

**图 9**：标题行现在包含 `Suppliers` 和 `Categories` DropDownLists （[单击查看完全大小的图像](batch-inserting-vb/_static/image27.png)）

现在，我们需要创建文本框来收集每个新产品的名称和价格。 将 "TextBox" 控件从工具箱拖动到五个产品名称和价格行的设计器中。 将文本框的 "`ID` 属性设置为 `ProductName1`、`UnitPrice1`、`ProductName2`、`UnitPrice2`、`ProductName3`、`UnitPrice3`等。

在每个 "单价" 文本框后面添加一个 CompareValidator，将 `ControlToValidate` 属性设置为相应的 `ID`。 还将 `Operator` 属性设置为 `GreaterThanEqual`，将 `ValueToCompare` 设置为0，并将 `Type` 设置为 `Currency`。 这些设置指示 CompareValidator 确保价格（如果输入）是大于或等于零的有效货币值。 将 `Text` 属性设置为 \*，并将 `ErrorMessage` 为价格必须大于或等于零。 此外，请省略任何货币符号。

> [!NOTE]
> 即使 `Products` 数据库表中的 `ProductName` 字段不允许 `NULL` 值，插入接口也不包含任何 RequiredFieldValidator 控件。 这是因为我们希望让用户输入最多五个产品。 例如，如果用户要为前三行提供产品名称和单价，将最后两行保留为空白，则 d 只需将三个新产品添加到系统。 由于 `ProductName` 是必需的，因此，我们需要以编程方式进行检查，以确保在输入单价时是否提供了相应的产品名称值。 我们将在步骤4中解决此项检查。

当验证用户的输入时，如果值包含货币符号，CompareValidator 将报告无效数据。 在每个单位价格文本框的前面添加一个 $，作为视觉提示，指示用户在输入价格时省略货币符号。

最后，在 `InsertingInterface` 面板中添加 ValidationSummary 控件，将其 `ShowMessageBox` 属性设置为 `True`，并将其 `ShowSummary` 属性设置为 `False`。 使用这些设置时，如果用户输入的单位价格值无效，则会在有问题的 TextBox 控件旁显示一个星号，ValidationSummary 将显示一个客户端 messagebox，其中显示了我们前面指定的错误消息。

此时，屏幕应类似于图10所示。

[![插入接口现在包含产品名称和价格的文本框](batch-inserting-vb/_static/image29.png)](batch-inserting-vb/_static/image28.png)

**图 10**：插入接口现在包含产品名称和价格的文本框（[单击查看全尺寸图像](batch-inserting-vb/_static/image30.png)）

接下来，我们需要将 "从发货中添加产品" 和 "取消" 按钮添加到 "页脚" 行。 将两个按钮控件从工具箱拖放到插入界面的页脚中，将按钮 `ID` 属性设置为 `AddProducts` 并 `CancelButton` 和 `Text` 属性分别添加产品和取消。 此外，将 `CancelButton` 控件 `CausesValidation` 属性设置为 "`false`"。

最后，我们需要添加一个标签 Web 控件，该控件将显示这两个接口的状态消息。 例如，当用户成功添加产品的新发货时，我们希望返回到显示界面并显示一条确认消息。 但是，如果用户为新产品提供价格，但保留产品名称，则需要显示一条警告消息，因为 "`ProductName`" 字段是必填字段。 由于我们需要为这两个接口显示此消息，因此将其放置在面板外的页面顶部。

将 "标签" Web 控件从工具箱拖动到设计器中页面的顶部。 将 `ID` 属性设置为 `StatusLabel`，清除 `Text` 属性，并将 `Visible` 和 `EnableViewState` 属性设置为 `False`。 如前面的教程中所示，将 `EnableViewState` 属性设置为 "`False` 使我们能够以编程方式更改标签的属性值并使其在后续回发中自动还原为默认值。 这样可以简化显示状态消息的代码，以响应在后续回发中消失的某些用户操作。 最后，将 `StatusLabel` 控件 `CssClass` 属性设置为 "警告"，这是在 `Styles.css` 中定义的 CSS 类的名称，以大、斜体、粗体、红色字体显示文本。

图11显示了在添加和配置标签之后的 Visual Studio 设计器。

[![将 Statuslabel 设置控件放在两个面板控件上](batch-inserting-vb/_static/image32.png)](batch-inserting-vb/_static/image31.png)

**图 11**：将 `StatusLabel` 控件放在两个面板控件上（[单击以查看完全大小的图像](batch-inserting-vb/_static/image33.png)）

## <a name="step-3-switching-between-the-display-and-inserting-interfaces"></a>步骤3：在显示和插入接口之间切换

此时，我们已经完成了显示和插入界面的标记，但仍保留了两个任务：

- 在显示和插入接口之间切换
- 将装运中的产品添加到数据库

当前，显示界面可见，但插入界面处于隐藏状态。 这是因为 `DisplayInterface` 面板 s `Visible` 属性设置为 `True` （默认值），而 `InsertingInterface` Panel `Visible` 属性设置为 `False`。 若要在两个接口之间切换，只需将每个控件 `Visible` 属性值。

当单击 "处理产品发货" 按钮时，我们希望从显示界面移到插入接口。 因此，请为此按钮 `Click` 包含以下代码的事件创建一个事件处理程序：

[!code-vb[Main](batch-inserting-vb/samples/sample4.vb)]

此代码只需隐藏 `DisplayInterface` 面板并显示 `InsertingInterface` 面板。

接下来，为 "从发货中添加产品" 和 "取消" 按钮控件创建事件处理程序。 单击其中任一按钮时，需要恢复到显示界面。 为这两个按钮控件创建 `Click` 事件处理程序，以便它们调用 `ReturnToDisplayInterface`，这是一种暂时要添加的方法。 除了隐藏 `InsertingInterface` 面板并显示 `DisplayInterface` 面板外，`ReturnToDisplayInterface` 方法还需要将 Web 控件返回到其预编辑状态。 这涉及到将 DropDownLists `SelectedIndex` 属性设置为0并清除 TextBox 控件的 `Text` 属性。

> [!NOTE]
> 如果在返回到显示界面之前未将控件返回到其预编辑状态，请考虑可能会发生的情况。 用户可以单击 "处理产品发货" 按钮，输入装运中的产品，然后单击 "从发货中添加产品"。 这会添加产品并将用户返回到显示界面。 此时，用户可能想要添加另一个发货。 单击 "处理产品发货" 按钮后，它们将返回到插入界面，但 DropDownList 选择和文本框值仍将填充其以前的值。

[!code-vb[Main](batch-inserting-vb/samples/sample5.vb)]

`Click` 事件处理程序只需调用 `ReturnToDisplayInterface` 方法，但我们将返回到步骤4中的 "从发货中添加产品" `Click` 事件处理程序并添加代码以保存产品。 `ReturnToDisplayInterface` 首先将 `Suppliers` 并 `Categories` DropDownLists 返回到它们的第一个选项。 这两个常量 `firstControlID` 和 `lastControlID` 标记插入界面中的 "产品名称" 和 "单价" 文本框中使用的起始和结束控件索引值，并用于将 TextBox 控件的 `Text` 属性设置回空字符串的 `For` 循环的界限。 最后，将重置面板 `Visible` 属性，以便隐藏插入界面并显示显示界面。

请花点时间在浏览器中测试此页。 第一次访问该页面时，应会看到显示界面，如图5所示。 单击 "处理产品发货" 按钮。 页面将回发，此时应会看到插入界面，如图12所示。 单击 "从发货中添加产品" 或 "取消" 按钮会将您返回到显示界面。

> [!NOTE]
> 查看插入界面时，请花点时间来测试 "单价" 文本框中的 CompareValidators。 单击 "从发货中添加产品" 按钮时，如果货币值无效或价格值小于零，你应该会看到客户端 messagebox 警告。

[单击 "处理产品发货" 按钮后，将显示插入界面 ![](batch-inserting-vb/_static/image35.png)](batch-inserting-vb/_static/image34.png)

**图 12**：单击 "处理产品发货" 按钮后显示插入界面（[单击以查看完全尺寸的图像](batch-inserting-vb/_static/image36.png)）

## <a name="step-4-adding-the-products"></a>步骤4：添加产品

本教程剩下的全部工作就是在 "从发货中添加产品" 按钮 `Click` 事件处理程序将产品保存到数据库。 为此，可以创建 `ProductsDataTable`，并为提供的每个产品名称添加 `ProductsRow` 实例。 添加这些 `ProductsRow` 后，我们将在 `ProductsDataTable`中调用 `ProductsBLL` 类 `UpdateWithTransaction` 方法。 回忆一下，在[事务教程内的包装数据库修改](wrapping-database-modifications-within-a-transaction-vb.md)中创建的 `UpdateWithTransaction` 方法将 `ProductsDataTable` 传递到 `ProductsTableAdapter`的 `UpdateWithTransaction` 方法。 在该数据库中，将启动 ADO.NET 事务，并且对于 DataTable 中添加的每个 `ProductsRow`，TableAdapter 向数据库发出 `INSERT` 语句。 假设所有产品都已添加但未发生错误，则提交事务，否则回滚事务。

"从发货中添加产品" 按钮的代码 `Click` 事件处理程序还需要执行一些错误检查。 由于插入界面中没有使用 RequiredFieldValidators，用户可以输入产品的价格，同时省略其名称。 由于产品名称是必需的，因此，如果这种情况将，我们需要提醒用户，而不是继续插入操作。 完整的 `Click` 事件处理程序代码如下：

[!code-vb[Main](batch-inserting-vb/samples/sample6.vb)]

此事件处理程序首先确保 `Page.IsValid` 属性返回值为 `True`。 如果它返回 `False`，则表示一个或多个 CompareValidators 报告的数据无效;在这种情况下，我们不想尝试插入输入的产品，或者我们在尝试将用户输入的单位价格值分配到 `ProductsRow` s `UnitPrice` 属性时，将会出现异常。

接下来，将创建一个新的 `ProductsDataTable` 实例（`products`）。 `For` 循环用于循环访问 "产品名称" 和 "单价" 文本框，`Text` 属性读入本地变量 `productName` 和 `unitPrice`。 如果用户输入了单位价格的值而不是对应的产品名称，则 `StatusLabel` 将显示该消息。如果你提供单位价格，还必须包含产品的名称，并且事件处理程序将退出。

如果提供了产品名称，则会使用 `ProductsDataTable` s `NewProductsRow` 方法创建新的 `ProductsRow` 实例。 此新 `ProductsRow` 实例 s `ProductName` 属性设置为 "当前产品名称" 文本框，同时 `SupplierID` 和 `CategoryID` 属性分配给插入接口 "标头中 DropDownLists 的" `SelectedValue` 属性 "。 如果用户为产品价格输入了值，则会将其分配给 `ProductsRow` 实例的 `UnitPrice` 属性;否则，该属性将为空，这将导致数据库中的 `UnitPrice` `NULL` 值。 最后，`Discontinued` 和 `UnitsOnOrder` 属性分别分配给硬编码值 `False` 和0。

将属性分配到 `ProductsRow` 实例后，将其添加到 `ProductsDataTable`中。

完成 `For` 循环后，我们将检查是否添加了任何产品。 毕竟，用户可能在输入任何产品名称或价格之前单击了 "从发货中添加产品"。 如果 `ProductsDataTable`中至少有一个产品，将调用 `ProductsBLL` 类 `UpdateWithTransaction` 方法。 接下来，将数据重新绑定到 `ProductsGrid` GridView，以便新添加的产品将显示在显示界面中。 更新 `StatusLabel` 以显示确认消息，并调用 `ReturnToDisplayInterface`，隐藏插入界面并显示显示界面。

如果未输入任何产品，插入界面会保持显示，但不会添加消息。 请在显示的文本框中输入产品名称和单价。

图 s 13、14和15显示了操作中的插入和显示接口。 在图13中，用户输入的单位价格值没有相应的产品名称。 图14显示了三个新产品成功添加后的显示界面，而图15显示了 GridView 中新添加的两个产品（第三个产品在上一页上）。

[输入单位价格时，需要 ![产品名称](batch-inserting-vb/_static/image38.png)](batch-inserting-vb/_static/image37.png)

**图 13**：输入单位价格时需要产品名称（[单击查看全尺寸图像](batch-inserting-vb/_static/image39.png)）

[已为供应商 Mayumi 添加了 ![三个新的 Veggies](batch-inserting-vb/_static/image41.png)](batch-inserting-vb/_static/image40.png)

**图 14**：为供应商 Mayumi 添加了三个新的 Veggies （[单击查看完全尺寸的图像](batch-inserting-vb/_static/image42.png)）

[![可以在 GridView 的最后一页中找到新的产品](batch-inserting-vb/_static/image44.png)](batch-inserting-vb/_static/image43.png)

**图 15**：新产品可在 GridView 的最后一页中找到（[单击以查看完全大小的图像](batch-inserting-vb/_static/image45.png)）

> [!NOTE]
> 本教程中使用的批插入逻辑将在事务范围内进行插入。 若要验证这一点，有意会引入数据库级别的错误。 例如，不是将新的 `ProductsRow` 实例的 `CategoryID` 属性分配到 `Categories` DropDownList 中的选定值，而是将其分配给 `i * 5`之类的值。 此处 `i` 为循环索引器，其值范围从1到5。 因此，在批插入中添加两个或更多产品时，第一个产品将具有有效的 `CategoryID` 值（5），但后面的产品将具有与 `Categories` 表中的 `CategoryID` 值不匹配的 `CategoryID` 值。 实际效果是，在第一次 `INSERT` 成功后，后续的将失败，并出现外键约束冲突。 由于批处理插入是原子的，因此第一个 `INSERT` 会回滚，并将数据库返回到批处理插入进程开始之前的状态。

## <a name="summary"></a>摘要

在此过程中，我们创建了允许更新、删除和插入批处理数据的接口，所有这些数据都使用我们在事务教程中的[包装数据库修改](wrapping-database-modifications-within-a-transaction-vb.md)中添加到数据访问层的事务支持。 在某些情况下，此类批处理用户界面可通过减少点击次数、回发和键盘到鼠标的上下文切换，同时保持基础数据的完整性，从而极大地提高最终用户的工作效率。

本教程将介绍如何使用批处理数据。 下一组教程将探讨各种高级的数据访问层方案，包括使用 TableAdapter 方法中的存储过程、配置 DAL 中的连接和命令级设置、加密连接字符串，等等！

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Hilton Giesenow 和 Jacob Lauritsen。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](batch-deleting-vb.md)
