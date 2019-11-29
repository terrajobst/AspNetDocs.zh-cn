---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
title: 自定义 DataList 的编辑界面（C#） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将为 DataList 创建更丰富的编辑界面，其中包含 DropDownLists 和复选框。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: a5d13067-ddfb-4c36-8209-0f69fd40e45c
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 81f5a7f6737f544f577447f263dbd37dbc8279d9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74623857"
---
# <a name="customizing-the-datalists-editing-interface-c"></a>自定义 DataList 的编辑界面 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_CS.exe)或[下载 PDF](customizing-the-datalist-s-editing-interface-cs/_static/datatutorial40cs1.pdf)

> 在本教程中，我们将为 DataList 创建更丰富的编辑界面，其中包含 DropDownLists 和复选框。

## <a name="introduction"></a>简介

DataList s 中的标记和 Web 控件 `EditItemTemplate` 定义其可编辑界面。 到目前为止，我们已经检查过的所有可编辑的 DataList 示例，该可编辑界面由 TextBox Web 控件组成。 在[前面的教程](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)中，我们通过添加验证控件改善了编辑时间用户体验。

`EditItemTemplate` 可以进一步扩展为包含文本框以外的 Web 控件，如 DropDownLists、RadioButtonLists、日历等。 与文本框一样，在自定义编辑界面以包括其他 Web 控件时，请使用以下步骤：

1. 将 Web 控件添加到 `EditItemTemplate`。
2. 使用数据绑定语法将相应的数据字段值分配给相应的属性。
3. 在 `UpdateCommand` 事件处理程序中，以编程方式访问 Web 控件值并将其传递到适当的 BLL 方法。

在本教程中，我们将为 DataList 创建更丰富的编辑界面，其中包含 DropDownLists 和复选框。 具体而言，我们将创建一个 DataList，其中列出了产品信息，并允许更新产品的名称、供应商、类别和停止状态（请参阅图1）。

[编辑界面 ![包括 TextBox、两个 DropDownLists 和一个复选框](customizing-the-datalist-s-editing-interface-cs/_static/image2.png)](customizing-the-datalist-s-editing-interface-cs/_static/image1.png)

**图 1**：编辑界面包括 TextBox、两个 DropDownLists 和一个复选框（[单击查看完全大小的图像](customizing-the-datalist-s-editing-interface-cs/_static/image3.png)）

## <a name="step-1-displaying-product-information"></a>步骤1：显示产品信息

我们首先需要生成只读接口，然后才能创建 DataList s 可编辑界面。 首先，从 "`EditDeleteDataList`" 文件夹打开 "`CustomizedUI.aspx`" 页，然后从设计器中将 DataList 添加到页面，并将其 `ID` 属性设置为 "`Products`"。 从 DataList s 智能标记创建一个新的 ObjectDataSource。 将此新 ObjectDataSource 命名为 `ProductsDataSource` 并将其配置为从 `ProductsBLL` 类 `GetProducts` 方法检索数据。 与前面的可编辑 DataList 教程一样，我们将通过直接转到业务逻辑层来更新已编辑的产品信息。 相应地，将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。

[![将 "更新"、"插入" 和 "删除选项卡" 下拉列表设置为 "（无）"](customizing-the-datalist-s-editing-interface-cs/_static/image5.png)](customizing-the-datalist-s-editing-interface-cs/_static/image4.png)

**图 2**：将 "更新"、"插入" 和 "删除选项卡" 下拉列表设置为 "（无）" （[单击查看完全大小的映像](customizing-the-datalist-s-editing-interface-cs/_static/image6.png)）

配置 ObjectDataSource 后，Visual Studio 将为 DataList 创建默认 `ItemTemplate`，该 DataList 列出返回的每个数据字段的名称和值。 修改 `ItemTemplate`，使模板在 `<h4>` 元素中列出产品名称，以及类别名称、供应商名称、价格和停止状态。 此外，添加 "编辑" 按钮，确保其 `CommandName` 属性设置为 "编辑"。 `ItemTemplate` 的声明性标记如下所示：

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample1.aspx)]

上述标记使用 &lt;h4&gt; 标题作为产品名称，并使用四列 `<table>` 为其余字段布局产品信息。 之前的教程中讨论了在 `Styles.css`中定义的 `ProductPropertyLabel` 和 `ProductPropertyValue` CSS 类。 图3显示了通过浏览器查看的进度。

[显示每个产品的名称、供应商、类别、已停用状态和价格的 ![](customizing-the-datalist-s-editing-interface-cs/_static/image8.png)](customizing-the-datalist-s-editing-interface-cs/_static/image7.png)

**图 3**：显示了每个产品的名称、供应商、类别、已停用状态和价格（[单击查看全尺寸图像](customizing-the-datalist-s-editing-interface-cs/_static/image9.png)）

## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>步骤2：将 Web 控件添加到编辑界面

构建自定义的 DataList 编辑界面的第一步是将所需的 Web 控件添加到 `EditItemTemplate`。 特别是，我们需要为该类别指定一个 DropDownList，为供应商提供另一个复选框，并在停用状态下复选框。 由于本示例中不能编辑产品的价格，因此我们可以继续使用标签 Web 控件显示它。

若要自定义编辑界面，请单击 DataList s 智能标记的 "编辑模板" 链接，然后从下拉列表中选择 "`EditItemTemplate`" 选项。 将 DropDownList 添加到 `EditItemTemplate`，并将其 `ID` 设置为 "`Categories`"。

[![为类别添加 DropDownList](customizing-the-datalist-s-editing-interface-cs/_static/image11.png)](customizing-the-datalist-s-editing-interface-cs/_static/image10.png)

**图 4**：为类别添加 DropDownList （[单击查看完全大小的图像](customizing-the-datalist-s-editing-interface-cs/_static/image12.png)）

接下来，从 DropDownList s 智能标记中，选择 "选择数据源" 选项，并创建名为 `CategoriesDataSource`的新 ObjectDataSource。 将此 ObjectDataSource 配置为使用 `CategoriesBLL` 类 `GetCategories()` 方法（参见图5）。 接下来，DropDownList 的数据源配置向导会提示输入要用于每个 `ListItem` `Text` 和 `Value` 属性的数据字段。 让 DropDownList 显示 `CategoryName` 数据字段并使用 `CategoryID` 作为值，如图6所示。

[![创建一个名为 CategoriesDataSource 的新 ObjectDataSource](customizing-the-datalist-s-editing-interface-cs/_static/image14.png)](customizing-the-datalist-s-editing-interface-cs/_static/image13.png)

**图 5**：创建名为 `CategoriesDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](customizing-the-datalist-s-editing-interface-cs/_static/image15.png)）

[![配置 DropDownList s 显示和值字段](customizing-the-datalist-s-editing-interface-cs/_static/image17.png)](customizing-the-datalist-s-editing-interface-cs/_static/image16.png)

**图 6**：配置 DropDownList s 显示和值字段（[单击查看完全大小的图像](customizing-the-datalist-s-editing-interface-cs/_static/image18.png)）

重复此系列步骤，为供应商创建 DropDownList。 将此 DropDownList 的 `ID` 设置为 `Suppliers` 并将其 ObjectDataSource `SuppliersDataSource`命名为。

添加这两个 DropDownLists 后，为 "已停用" 状态添加复选框并为产品名称添加文本框。 将复选框和文本框的 `ID` 分别设置为 `Discontinued` 和 `ProductName`。 添加 RequiredFieldValidator 以确保用户为产品名称提供一个值。

最后，添加 "更新" 和 "取消" 按钮。 请记住，对于这两个按钮，必须将其 `CommandName` 属性分别设置为 "更新" 和 "取消"。

您可以随意布局编辑界面。 我选择在只读界面中使用相同的四列 `<table>` 布局，如以下声明性语法和屏幕截图所示：

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample2.aspx)]

[编辑界面的布局 ![如下所示](customizing-the-datalist-s-editing-interface-cs/_static/image20.png)](customizing-the-datalist-s-editing-interface-cs/_static/image19.png)

**图 7**：编辑界面的布局类似于只读界面（[单击以查看完全大小的图像](customizing-the-datalist-s-editing-interface-cs/_static/image21.png)）

## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>步骤3：创建 EditCommand 和 CancelCommand 事件处理程序

目前 `EditItemTemplate` 中没有数据绑定语法（`UnitPriceLabel`（已从 `ItemTemplate`中的原义复制）。 接下来，我们将添加数据绑定语法，但首先，让我们为 DataList s `EditCommand` 和 `CancelCommand` 事件创建事件处理程序。 请记住，`EditCommand` 事件处理程序的责任是为单击了 "编辑" 按钮的 DataList 项呈现编辑界面，而 `CancelCommand` 的作业是将 DataList 返回到其预编辑状态。

创建这两个事件处理程序，并让它们使用以下代码：

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample3.cs)]

准备好这两个事件处理程序后，单击 "编辑" 按钮将显示编辑界面，单击 "取消" 按钮会将编辑后的项返回到其只读模式。 图8显示了在单击 "编辑" 按钮后，Chef Anton s Gumbo 组合后的 DataList。 由于我们尚未将任何数据绑定语法添加到编辑界面，因此 `ProductName` TextBox 为空白，未选中 `Discontinued` 复选框，并且从 `Categories` 和 `Suppliers` DropDownLists 中选择的第一项。

[![单击 "编辑" 按钮将显示编辑界面](customizing-the-datalist-s-editing-interface-cs/_static/image23.png)](customizing-the-datalist-s-editing-interface-cs/_static/image22.png)

**图 8**：单击 "编辑" 按钮将显示编辑界面（[单击以查看完全尺寸的图像](customizing-the-datalist-s-editing-interface-cs/_static/image24.png)）

## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>步骤4：将数据绑定语法添加到编辑界面

为了使编辑界面显示当前产品的值，我们需要使用数据绑定语法将数据字段值分配给相应的 Web 控件值。 可以通过访问设计器来应用数据绑定语法，方法是转到 "编辑模板" 屏幕并从 Web 控件智能标记中选择 "编辑数据绑定" 链接。 或者，可以将数据绑定语法直接添加到声明性标记中。

将 `ProductName` 数据字段值分配给 `ProductName` TextBox s `Text` 属性，将 "`CategoryID`" 和 "`SupplierID` 数据" 字段值分配给 "`Categories`" 和 "`Suppliers`" `SelectedValue` 属性，将 "`Discontinued`" 数据字段值分配给 `Discontinued` CheckBox `Checked` 属性。 进行这些更改后，可以通过设计器或直接通过声明性标记，通过浏览器重新访问页面，然后单击 "Chef Anton s Gumbo Mix" 的 "编辑" 按钮。 如图9所示，数据绑定语法已将当前值添加到 TextBox、DropDownLists 和 CheckBox 中。

[![单击 "编辑" 按钮将显示编辑界面](customizing-the-datalist-s-editing-interface-cs/_static/image26.png)](customizing-the-datalist-s-editing-interface-cs/_static/image25.png)

**图 9**：单击 "编辑" 按钮将显示编辑界面（[单击以查看完全大小的图像](customizing-the-datalist-s-editing-interface-cs/_static/image27.png)）

## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>步骤5：在 UpdateCommand 事件处理程序中保存用户的更改

当用户编辑产品并单击 "更新" 按钮时，将发生回发并引发 DataList `UpdateCommand` 事件。 在事件处理程序中，我们需要从 `EditItemTemplate` 中的 Web 控件读取值，并与 BLL 交互以更新数据库中的产品。 如前面的教程中所示，已更新产品的 `ProductID` 可通过 `DataKeys` 集合进行访问。 用户输入的字段通过使用 `FindControl("controlID")`以编程方式引用 Web 控件进行访问，如以下代码所示：

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample4.cs)]

代码首先查看 `Page.IsValid` 属性，以确保页面上的所有验证控件都有效。 如果 `True``Page.IsValid`，则将从 `DataKeys` 集合读取已编辑的产品的 `ProductID` 值，并以编程方式引用 `EditItemTemplate` 中的数据输入 Web 控件。 接下来，将这些 Web 控件中的值读入变量，然后将其传递到相应的 `UpdateProduct` 重载。 更新数据后，DataList 返回到其预编辑状态。

> [!NOTE]
> 我省略了在[处理 BLL 和 DAL 级别的异常](handling-bll-and-dal-level-exceptions-cs.md)教程中添加的异常处理逻辑，目的是使代码和本示例重点保存。 作为练习，请在完成本教程后添加此功能。

## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>步骤6：处理 NULL 类别 Id 和供应商值

Northwind 数据库允许 `Products` 表 s `CategoryID` 和 `SupplierID` 列 `NULL` 值。 但是，我们的编辑界面目前不能容纳 `NULL` 值。 如果尝试编辑其 `CategoryID` 或 `SupplierID` 列都具有 `NULL` 值的产品，我们将得到一个 `ArgumentOutOfRangeException`，其中包含类似于以下内容的错误消息： *"类别" 的 SelectedValue 无效，因为它不存在于项目列表中。* 此外，目前还没有办法将 product s 类别或供应商值从非`NULL` 值更改为 `NULL` 一。

若要支持类别和供应商 DropDownLists `NULL` 值，需要添加其他 `ListItem`。 我选择使用 "（无）" 作为此 `ListItem`的 `Text` 值，但您可以根据需要将其更改为其他内容（例如空字符串）。 最后，请记住将 DropDownLists `AppendDataBoundItems` 设置为 `True`;如果忘记这样做，则绑定到 DropDownList 的类别和供应商将覆盖静态添加的 `ListItem`。

进行这些更改后，DataList `EditItemTemplate` 中的 DropDownLists 标记应如下所示：

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample5.aspx)]

> [!NOTE]
> 可以通过设计器或直接通过声明性语法将静态 `ListItem` 添加到 DropDownList。 添加 DropDownList 项以表示数据库 `NULL` 值时，请确保通过声明性语法添加 `ListItem`。 如果在设计器中使用 `ListItem` 集合编辑器，则生成的声明性语法将在分配空字符串时完全省略 `Value` 设置，创建类似于以下内容的声明性标记： `<asp:ListItem>(None)</asp:ListItem>`。 虽然这看起来可能无害，但缺少 `Value` 会导致 DropDownList 使用 `Text` 属性值。 这意味着，如果选择此 `NULL` `ListItem`，则会尝试将值（None）分配给 "产品数据" 字段（在本教程中为`CategoryID` 或 `SupplierID`），这会导致异常。 通过显式设置 `Value=""`，当选择 `NULL` `ListItem` 时，`NULL` 值将分配给产品数据字段。

花点时间通过浏览器查看进度。 编辑产品时，请注意，在 DropDownList 的开头，`Categories` 和 `Suppliers` DropDownLists 都有一个 "（无）" 选项。

[![类别和供应商 DropDownLists 包括 "（无）" 选项](customizing-the-datalist-s-editing-interface-cs/_static/image29.png)](customizing-the-datalist-s-editing-interface-cs/_static/image28.png)

**图 10**： `Categories` 和 `Suppliers` DropDownLists 包含一个 "（无）" 选项（[单击以查看完全大小的图像](customizing-the-datalist-s-editing-interface-cs/_static/image30.png)）

若要将 "（无）" 选项保存为数据库 `NULL` 值，需要返回 `UpdateCommand` 事件处理程序。 仅当 DropDownList s `SelectedValue` 不为空字符串时，将 `categoryIDValue` 和 `supplierIDValue` 变量更改为可为 null 的整数，并为其分配除 `Nothing` 之外的值。

[!code-csharp[Main](customizing-the-datalist-s-editing-interface-cs/samples/sample6.cs)]

进行此更改后，如果用户从任一下拉列表中选择了 "（无）" 选项，则 `Nothing` 的值将传递到 `UpdateProduct` BLL 方法，这与 `NULL` 数据库值相对应。

## <a name="summary"></a>总结

在本教程中，我们了解了如何创建更复杂的 DataList 编辑界面，该界面包含三个不同的输入 Web 控件 TextBox、两个 DropDownLists 和一个复选框以及验证控件。 在生成编辑接口时，无论使用何种 Web 控件，步骤都是相同的：首先将 Web 控件添加到 DataList s `EditItemTemplate`;使用 databinding 语法将相应的数据字段值分配给相应的 Web 控件属性;并且，在 `UpdateCommand` 事件处理程序中，以编程方式访问 Web 控件及其相应的属性，并将其值传递到 BLL。

创建编辑界面时，无论它是只由 textbox 还是由不同的 Web 控件组成的集合，都务必正确处理数据库 `NULL` 值。 在核算 `NULL` 时，必须在编辑界面中只正确地显示现有 `NULL` 值，还必须提供一种将值标记为 `NULL`的方式。 对于 DataLists 中的 DropDownLists，这通常意味着添加 `Value` 属性显式设置为空字符串（`Value=""`）的静态 `ListItem`，并将一些代码添加到 `UpdateCommand` 事件处理程序，以确定是否选择了 `NULL``ListItem`。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Dennis Patterson 将、David Suru 和 Randy Schmidt。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)
> [下一页](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
