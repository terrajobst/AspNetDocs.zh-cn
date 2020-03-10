---
uid: web-forms/overview/data-access/working-with-batched-data/batch-updating-cs
title: 批更新（C#） |Microsoft Docs
author: rick-anderson
description: 了解如何在一个操作中更新多个数据库记录。 在用户界面层，我们构建了一个 GridView，其中每行都是可编辑的。 在 "数据 ..."
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 4e849bcc-c557-4bc3-937e-f7453ee87265
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-updating-cs
msc.type: authoredcontent
ms.openlocfilehash: baaaf37c47cc57d90ea579a5c20949bf8cfc7a3c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78476402"
---
# <a name="batch-updating-c"></a>批量更新 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_64_CS.zip)或[下载 PDF](batch-updating-cs/_static/datatutorial64cs1.pdf)

> 了解如何在一个操作中更新多个数据库记录。 在用户界面层，我们构建了一个 GridView，其中每行都是可编辑的。 在数据访问层中，我们在事务中包装多个更新操作，以确保所有更新成功或回滚所有更新。

## <a name="introduction"></a>简介

在[前面的教程](wrapping-database-modifications-within-a-transaction-cs.md)中，我们介绍了如何扩展数据访问层以添加对数据库事务的支持。 数据库事务可确保将一系列数据修改语句视为一个原子操作，这可确保所有修改都将失败或全部成功。 通过这种低级别 DAL 功能，我们可以随时将注意力转换为创建批处理数据修改接口。

在本教程中，我们将构建一个 GridView，其中每行都是可编辑的（请参阅图1）。 由于每行都是在其编辑界面中呈现的，因此无需使用 "编辑"、"更新" 和 "取消" 按钮的列。 相反，页面上有两个 "更新产品" 按钮，在单击此按钮时，会枚举 GridView 行并更新数据库。

[GridView 中的每行都是可编辑的 ![](batch-updating-cs/_static/image1.gif)](batch-updating-cs/_static/image1.png)

**图 1**： GridView 中的每一行都是可编辑的（[单击以查看完全大小的图像](batch-updating-cs/_static/image2.png)）

让我们开始吧！

> [!NOTE]
> 在[执行批更新](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md)教程中，我们使用 DataList 控件创建了批处理编辑界面。 本教程不同于中的上一个教程，其中使用的是 GridView，批处理更新在事务范围内执行。 完成本教程后，我建议您返回到前面的教程，并将其更新为使用上一教程中添加的与数据库事务相关的功能。

## <a name="examining-the-steps-for-making-all-gridview-rows-editable"></a>检查使所有 GridView 行可编辑的步骤

如在[插入、更新和删除数据](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教程中所述，GridView 提供了针对每行编辑其基础数据的内置支持。 在内部，GridView 说明哪些行可通过其[`EditIndex` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.editindex(VS.80).aspx)进行编辑。 当 GridView 绑定到其数据源时，它会检查每一行以查看行的索引是否等于 `EditIndex`的值。 如果是这样，则使用其编辑界面呈现行字段。 对于 BoundFields，编辑界面是一个文本框，其 `Text` 属性分配有 BoundField s `DataField` 属性指定的数据字段的值。 对于 Templatefield，使用 `EditItemTemplate` 代替 `ItemTemplate`。

请记住，当用户单击 "编辑" 按钮时，编辑工作流将启动。 这会导致回发，将 GridView `EditIndex` 属性设置为单击的行的索引，并将数据重新绑定到网格。 单击 "取消" 按钮时，在回发时，`EditIndex` 设置为 `-1` 值，然后将数据重新绑定到网格。 由于 GridView 的行开始索引为零，因此，将 `EditIndex` 设置为 `-1` 会影响在只读模式下显示 GridView。

`EditIndex` 属性适用于每行编辑，但不适用于批量编辑。 若要使整个 GridView 可编辑，需要使用其编辑界面呈现每个行。 实现此目的的最简单方法是创建，其中每个可编辑字段的实现方式均为 TemplateField，并在 `ItemTemplate`中定义其编辑界面。

在接下来的几个步骤中，我们将创建一个完全可编辑的 GridView。 在步骤1中，我们首先创建 GridView 及其 ObjectDataSource，并将其 BoundFields 和 CheckBoxField 转换为 Templatefield。 在步骤2和步骤3中，我们会将编辑界面从 Templatefield `EditItemTemplate` s 移至其 `ItemTemplate`。

## <a name="step-1-displaying-product-information"></a>步骤1：显示产品信息

在考虑如何创建可编辑行的 GridView 之前，只需显示产品信息即可开始。 打开 `BatchData` 文件夹中的 "`BatchUpdate.aspx`" 页，并将 GridView 从工具箱拖到设计器上。 将 GridView `ID` 设置为 `ProductsGrid`，并从其智能标记中，选择将其绑定到名为 `ProductsDataSource`的新 ObjectDataSource。 配置 ObjectDataSource 以便从 `ProductsBLL` 类 `GetProducts` 方法检索其数据。

[![将 ObjectDataSource 配置为使用 ProductsBLL 类](batch-updating-cs/_static/image2.gif)](batch-updating-cs/_static/image3.png)

**图 2**：将 ObjectDataSource 配置为使用 `ProductsBLL` 类（[单击以查看完全大小的映像](batch-updating-cs/_static/image4.png)）

[![使用 GetProducts 方法检索产品数据](batch-updating-cs/_static/image3.gif)](batch-updating-cs/_static/image5.png)

**图 3**：使用 `GetProducts` 方法检索产品数据（[单击以查看完全大小的图像](batch-updating-cs/_static/image6.png)）

与 GridView 一样，ObjectDataSource 的修改功能旨在使每行工作。 若要更新一组记录，我们需要在 ASP.NET 页 s 代码隐藏类中编写一些代码，以便对数据进行批处理，并将其传递给 BLL。 因此，请在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"。 单击“完成”按钮以完成向导。

[![在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"](batch-updating-cs/_static/image4.gif)](batch-updating-cs/_static/image7.png)

**图 4**：将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的映像](batch-updating-cs/_static/image8.png)）

完成 "配置数据源" 向导后，ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](batch-updating-cs/samples/sample1.aspx)]

完成 "配置数据源" 向导还会导致 Visual Studio 为 GridView 中的 "产品" 数据字段创建 BoundFields 和一个 CheckBoxField。 对于本教程，让我们只允许用户查看和编辑产品的名称、类别、价格和废止状态。 删除除 `ProductName`、`CategoryName`、`UnitPrice`和 `Discontinued` 字段之外的所有字段，并分别将前三个字段的 `HeaderText` 属性重命名为 "产品"、"类别" 和 "价格"。 最后，选中 "GridView s 智能" 标记中的 "启用分页并启用排序" 复选框。

此时，GridView 有三个 BoundFields （`ProductName`、`CategoryName`和 `UnitPrice`）和 CheckBoxField （`Discontinued`）。 需要将这四个字段转换为 Templatefield，然后将编辑界面从 `ItemTemplate``EditItemTemplate` 移动到其。

> [!NOTE]
> 本文探讨了如何在[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教程中创建和自定义 templatefield。 我们将逐步介绍将 BoundFields 和 CheckBoxField 转换为 Templatefield 并在其 `ItemTemplate` 中定义其编辑界面的步骤，但如果你停滞或需要刷新器，请不要担心，请参阅前面的教程。

从 GridView s 智能标记中，单击 "编辑列" 链接，打开 "字段" 对话框。 接下来，选择每个字段，然后单击 "将此字段转换为 TemplateField" 链接。

![将现有的 BoundFields 和 CheckBoxField 转换为 TemplateField](batch-updating-cs/_static/image5.gif)

**图 5**：将现有的 BoundFields 和 CheckBoxField 转换为 TemplateField

由于每个字段都是 TemplateField，因此我们可以将编辑界面从 `EditItemTemplate` 移动到 `ItemTemplate`。

## <a name="step-2-creating-theproductnameunitprice-anddiscontinuedediting-interfaces"></a>步骤2：创建`ProductName`、`UnitPrice`和`Discontinued`编辑接口

创建 `ProductName`、`UnitPrice`和 `Discontinued` 编辑界面是此步骤的主题，并且非常简单，因为每个接口都已在 TemplateField s `EditItemTemplate`中定义。 创建 `CategoryName` 编辑界面有点多，因为我们需要创建适用类别的 DropDownList。 此 `CategoryName` 编辑接口在步骤3处理。

让我们从 `ProductName` TemplateField 开始。 单击 GridView s 智能标记的 "编辑模板" 链接，并向下钻取到 `ProductName` TemplateField s `EditItemTemplate`。 选择文本框，将其复制到剪贴板，然后将其粘贴到 `ProductName` TemplateField s `ItemTemplate`。 将 TextBox `ID` 属性更改为 "`ProductName`"。

接下来，将 RequiredFieldValidator 添加到 `ItemTemplate`，以确保用户为每个产品名称提供一个值。 将 `ControlToValidate` 属性设置为 ProductName `ErrorMessage`，则必须提供产品名称。 要 \*的 `Text` 属性。 对 `ItemTemplate`进行这些添加后，屏幕应类似于图6。

[![ProductName TemplateField 现在包括 TextBox 和 RequiredFieldValidator](batch-updating-cs/_static/image6.gif)](batch-updating-cs/_static/image9.png)

**图 6**： `ProductName` TemplateField 现在包含一个文本框和一个 RequiredFieldValidator （[单击以查看完全大小的图像](batch-updating-cs/_static/image10.png)）

对于 `UnitPrice` 编辑界面，请从 `EditItemTemplate` 将文本框复制到 `ItemTemplate`开始。 接下来，在文本框的前面放置一个 $，并将其 `ID` 属性设置为单价，并将其 `Columns` 属性设置为8。

同时，将 CompareValidator 添加到 `UnitPrice` 的 `ItemTemplate`，以确保用户输入的值是大于或等于 $0.00 的有效货币值。 将验证程序 `ControlToValidate` 属性设置为 "单价 `ErrorMessage`"，则必须输入有效的货币值。 请省略任何货币符号。、其 `Text` 属性可以 \*，其 `Type` 属性 `Currency`，其 `Operator` 属性为 `GreaterThanEqual`，其 `ValueToCompare` 属性为0。

[![添加 CompareValidator 以确保输入的价格是非负值货币值](batch-updating-cs/_static/image7.gif)](batch-updating-cs/_static/image11.png)

**图 7**：添加 CompareValidator 以确保输入的价格为非负货币值（[单击以查看完全大小的图像](batch-updating-cs/_static/image12.png)）

对于 `Discontinued` TemplateField，您可以使用已在 `ItemTemplate`中定义的复选框。 只需将其 `ID` 设置为废止，并将其 `Enabled` 属性设置为 "`true`"。

## <a name="step-3-creating-thecategorynameediting-interface"></a>步骤3：创建`CategoryName`编辑界面

`CategoryName` TemplateField s `EditItemTemplate` 中的编辑界面包含一个文本框，其中显示 `CategoryName` 数据字段的值。 需要将其替换为一个 DropDownList，其中列出了可能的类别。

> [!NOTE]
> [自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教程包含有关自定义模板以包含相对于文本框的 DropDownList 的更全面和完整讨论。 尽管步骤已完成，但会显示 tersely。 若要深入了解如何创建和配置类别 DropDownList，请参阅[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教程。

将 "DropDownList" 从 "工具箱" 拖动到 `CategoryName` TemplateField s `ItemTemplate`上，将其 `ID` 设置为 "`Categories`"。 此时，我们通常会通过其智能标记定义 DropDownLists 的数据源，从而创建新的 ObjectDataSource。 但是，这会将 ObjectDataSource 添加到 `ItemTemplate`中，这将导致为每个 GridView 行创建一个 ObjectDataSource 实例。 相反，在 GridView s Templatefield 之外创建 ObjectDataSource。 结束模板编辑，并将 ObjectDataSource 从工具箱拖动到 `ProductsDataSource` ObjectDataSource 下的设计器。 为新的 ObjectDataSource `CategoriesDataSource` 命名，并将其配置为使用 `CategoriesBLL` 类 `GetCategories` 方法。

[![将 ObjectDataSource 配置为使用 CategoriesBLL 类](batch-updating-cs/_static/image8.gif)](batch-updating-cs/_static/image13.png)

**图 8**：将 ObjectDataSource 配置为使用 `CategoriesBLL` 类（[单击以查看完全大小的映像](batch-updating-cs/_static/image14.png)）

[![使用 GetCategories 方法检索类别数据](batch-updating-cs/_static/image9.gif)](batch-updating-cs/_static/image15.png)

**图 9**：使用 `GetCategories` 方法检索类别数据（[单击以查看完全大小的图像](batch-updating-cs/_static/image16.png)）

由于此 ObjectDataSource 仅用于检索数据，因此请将 "更新" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。 单击“完成”按钮以完成向导。

[![将 "更新" 和 "删除" 选项卡中的下拉列表设置为 "（无）"](batch-updating-cs/_static/image10.gif)](batch-updating-cs/_static/image17.png)

**图 10**：将 "更新" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的图像](batch-updating-cs/_static/image18.png)）

完成向导后，`CategoriesDataSource` 的声明性标记应如下所示：

[!code-aspx[Main](batch-updating-cs/samples/sample2.aspx)]

创建并配置 `CategoriesDataSource` 后，返回到 `CategoryName` TemplateField s `ItemTemplate`，并从 DropDownList s 智能标记中，单击 "选择数据源" 链接。 在 "数据源配置向导" 中，从第一个下拉列表中选择 "`CategoriesDataSource`" 选项，然后 `CategoryName` 选择 "显示" 和 "`CategoryID`" 作为值。

[![将 DropDownList 绑定到 CategoriesDataSource](batch-updating-cs/_static/image11.gif)](batch-updating-cs/_static/image19.png)

**图 11**：将 DropDownList 绑定到 `CategoriesDataSource` （[单击查看完全大小的图像](batch-updating-cs/_static/image20.png)）

此时，`Categories` DropDownList 将列出所有类别，但它尚不会自动为绑定到 GridView 行的产品选择适当的类别。 为实现此目的，我们需要将 `Categories` DropDownList s `SelectedValue` 设置为产品的 `CategoryID` 值。 在 DropDownList s 智能标记中单击 "编辑数据绑定" 链接，并将 `SelectedValue` 属性与 `CategoryID` 数据字段相关联，如图12所示。

![将产品 s 类别 Id 值绑定到 DropDownList s SelectedValue 属性](batch-updating-cs/_static/image12.gif)

**图 12**：将产品 s `CategoryID` 值绑定到 DropDownList s `SelectedValue` 属性

最后一个问题仍存在：如果产品没有指定 `CategoryID` 值，则 `SelectedValue` 上的数据绑定语句将导致异常。 这是因为，DropDownList 仅包含类别的项目，并且不为具有 `CategoryID``NULL` 数据库值的产品提供选项。 若要解决此情况，请将 DropDownList `AppendDataBoundItems` 属性设置为 `true` 并将新项添加到 DropDownList，并从声明性语法中省略 `Value` 属性。 也就是说，请确保 `Categories` DropDownList s 声明性语法如下所示：

[!code-aspx[Main](batch-updating-cs/samples/sample3.aspx)]

请注意，`<asp:ListItem Value="">` 如何将其 `Value` 属性显式设置为空字符串。 请参阅[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教程，详细了解为什么需要此额外的 DropDownList 项来处理 `NULL` 案例，以及为什么将 `Value` 属性分配给空字符串是必不可少的。

> [!NOTE]
> 此处有一种潜在的性能和可伸缩性问题值得一提。 由于每一行都有一个使用 `CategoriesDataSource` 作为其数据源的 DropDownList，因此 `CategoriesBLL` 类 s `GetCategories` 方法将在每次访问页时调用*n*次，其中*n*是 GridView 中的行数。 这*n*对的调用 `GetCategories` 会导致对数据库进行*n*次查询。 可以通过使用 SQL 缓存依赖关系或基于时间的较短的过期缓存返回的类别，在每个请求缓存中或通过缓存层缓存返回的类别，从而减少对数据库的影响。 有关每请求缓存选项的详细信息，请参阅[`HttpContext.Items` 每个请求的缓存存储](http://aspnet.4guysfromrolla.com/articles/060904-1.aspx)。

## <a name="step-4-completing-the-editing-interface"></a>步骤4：完成编辑界面

在不暂停的情况下，我们已对 GridView 模板进行了大量更改，无法查看进度。 花点时间通过浏览器查看进度。 如图13所示，每行都使用其 `ItemTemplate`进行呈现，其中包含单元格编辑界面。

[每个 GridView 行 ![都是可编辑的](batch-updating-cs/_static/image13.gif)](batch-updating-cs/_static/image21.png)

**图 13**：每个 GridView 行都是可编辑的（[单击查看完全大小的图像](batch-updating-cs/_static/image22.png)）

此时，我们应该注意一些次要的格式问题。 首先，请注意，`UnitPrice` 值包含四个小数点。 若要解决此问题，请返回到 `UnitPrice` TemplateField s `ItemTemplate` 并在 "TextBox" 智能标记中单击 "编辑 databinding" 链接。 接下来，指定应将 `Text` 属性设置为数字格式。

![将 Text 属性设置为数字格式](batch-updating-cs/_static/image14.gif)

**图 14**：将 `Text` 属性设置为数字格式

其次，让我们将 `Discontinued` 列中的复选框居中（而不是左对齐）。 单击 "GridView s 智能" 标记中的 "编辑列"，然后从左下角的字段列表中选择 "`Discontinued` TemplateField"。 向下钻取到 `ItemStyle`，并将 `HorizontalAlign` 属性设置为 "居中"，如图15所示。

![停用复选框](batch-updating-cs/_static/image15.gif)

**图 15**：将 `Discontinued` 复选框居中

接下来，将 ValidationSummary 控件添加到页面，并将其 `ShowMessageBox` 属性设置为 "`true`"，并将其 `ShowSummary` 属性设置为 "`false`"。 另外，添加按钮 Web 控件，单击该按钮将更新用户的更改。 具体而言，添加两个按钮 Web 控件，一个位于 GridView 上方，另一个位于其下面，同时将两个控件 `Text` 属性设置为更新产品。

由于在 Templatefield `ItemTemplate` s 中定义了 GridView s 编辑界面，因此 `EditItemTemplate` 为多余，可能会被删除。

进行上述格式更改后，添加按钮控件并删除不必要的 `EditItemTemplate` 后，页的声明性语法应该如下所示：

[!code-aspx[Main](batch-updating-cs/samples/sample4.aspx)]

图16显示了在添加按钮 Web 控件和进行格式更改后通过浏览器查看的此页。

[![该页现在包括两个 "更新产品" 按钮](batch-updating-cs/_static/image16.gif)](batch-updating-cs/_static/image23.png)

**图 16**：该页现在包含两个更新产品按钮（[单击以查看完全大小的图像](batch-updating-cs/_static/image24.png)）

## <a name="step-5-updating-the-products"></a>步骤5：更新产品

当用户访问此页面时，他们将进行修改，然后单击两个 "更新产品" 按钮之一。 此时，我们需要以某种方式将每个行的用户输入的值保存到 `ProductsDataTable` 实例，然后将其传递给 BLL 方法，然后将该 `ProductsDataTable` 实例传递到 DAL s `UpdateWithTransaction` 方法。 在[上一教程](wrapping-database-modifications-within-a-transaction-cs.md)中创建的 `UpdateWithTransaction` 方法可确保将更改批更新为原子操作。

在 `BatchUpdate.aspx.cs` 中创建名为 `BatchUpdate` 的方法，并添加以下代码：

[!code-csharp[Main](batch-updating-cs/samples/sample5.cs)]

此方法的开始方式是通过调用 BLL 的 `GetProducts` 方法，将所有产品恢复到 `ProductsDataTable` 中。 然后枚举 `ProductGrid` GridView s [`Rows` 集合](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows(VS.80).aspx)。 `Rows` 集合包含 GridView 中显示的每一行的[`GridViewRow` 实例](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewrow.aspx)。 由于我们在每页上显示的行数最多为10，因此 GridView `Rows` 集合中的项不会超过10个。

对于每一行，`ProductID` 都从 `DataKeys` 集合中获取，并从 `ProductsDataTable`中选择相应的 `ProductsRow`。 以编程方式引用四个 TemplateField 输入控件，并将它们的值分配给 `ProductsRow` 实例的属性。 使用每个 GridView 行的值更新 `ProductsDataTable`后，它将传递给 BLL s `UpdateWithTransaction` 方法，如前面的教程中所示，只需向下调用 DAL s `UpdateWithTransaction` 方法。

本教程中使用的批更新算法将更新与 GridView 中的行相对应的 `ProductsDataTable` 中的每一行，而不管产品的信息是否已更改。 尽管此类直接更新并不是性能问题，但如果您对数据库表进行了审核更改，它们可能会导致不需要的记录。 回到[执行批更新](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md)教程，我们探索了包含 DataList 的批处理更新接口，并添加了只更新用户实际修改的记录的代码。 如果需要，可以根据需要使用此方法来[执行批量更新](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs.md)，以便更新本教程中的代码。

> [!NOTE]
> 当通过其智能标记将数据源绑定到 GridView 时，Visual Studio 会自动将数据源的主键值分配给 GridView 的 `DataKeyNames` 属性。 如果未通过步骤1中所述的 GridView s 智能标记将 ObjectDataSource 绑定到 GridView，则需要手动将 GridView `DataKeyNames` 属性设置为 ProductID，以便通过 `DataKeys` 集合访问每一行的 `ProductID` 值。

`BatchUpdate` 中使用的代码与 BLL `UpdateProduct` 方法中使用的代码相似，主要区别在于，`UpdateProduct` 方法仅从体系结构检索单个 `ProductRow` 实例。 指定 `ProductRow` 的属性的代码在 `BatchUpdate`中的 `foreach` 循环内的 `UpdateProducts` 方法和代码之间是相同的，就像总体模式一样。

若要完成本教程，需要在单击 "更新产品" 按钮时调用 `BatchUpdate` 方法。 为这两个按钮控件的 `Click` 事件创建事件处理程序，并在事件处理程序中添加以下代码：

[!code-csharp[Main](batch-updating-cs/samples/sample6.cs)]

首先调用 `BatchUpdate`。 接下来，将使用 `ClientScript property` 来注入 JavaScript，该 JavaScript 将显示读取产品已更新的 messagebox。

花点时间对此代码进行测试。 通过浏览器访问 `BatchUpdate.aspx`、编辑多个行，然后单击其中一个 "更新产品" 按钮。 假设没有输入验证错误，你应该会看到一个 messagebox，其中包含已更新的产品。 若要验证更新的原子性，请考虑添加一个随机 `CHECK` 约束，如不允许 `UnitPrice` 值1234.56 的值。 然后，在 `BatchUpdate.aspx`中，编辑多条记录，确保将产品的 `UnitPrice` 值之一设置为禁止值（1234.56）。 这会导致在此批处理操作出现时，单击 "更新产品" 时出现错误。

## <a name="an-alternativebatchupdatemethod"></a>备用`BatchUpdate`方法

我们刚才检查的 `BatchUpdate` 方法从 BLL s `GetProducts` 方法中检索*所有*产品，然后仅更新在 GridView 中显示的那些记录。 如果 GridView 不使用分页，则此方法非常理想，但如果有，则可能有成百上千的产品，但在 GridView 中只能有10行。 在这种情况下，只是从数据库中获取所有产品，只是修改其中的10个。

对于这些类型的情况，请考虑改用以下 `BatchUpdateAlternate` 方法：

[!code-csharp[Main](batch-updating-cs/samples/sample7.cs)]

`BatchMethodAlternate` 首先创建名为 `products`的新的空 `ProductsDataTable`。 然后，依次执行 GridView 的 `Rows` 集合，每一行都将使用 BLL s `GetProductByProductID(productID)` 方法获取特定的产品信息。 检索的 `ProductsRow` 实例的属性以与 `BatchUpdate`相同的方式进行更新，但在更新行后，将通过 DataTable [`ImportRow(DataRow)` 方法](https://msdn.microsoft.com/library/system.data.datatable.importrow(VS.80).aspx)将其导入到 `products``ProductsDataTable` 中。

`foreach` 循环完成后，`products` 为 GridView 中的每一行包含一个 `ProductsRow` 实例。 由于每个 `ProductsRow` 实例都已添加到 `products` （而不是更新），因此，如果我们盲目地将其传递到 `UpdateWithTransaction` 方法，`ProductsTableAdapter` 会尝试将每个记录插入到数据库中。 相反，我们需要指定每个行都已修改（不添加）。

这可以通过将新方法添加到名为 `UpdateProductsWithTransaction`的 BLL 来完成。 `UpdateProductsWithTransaction`，如下所示，将 `ProductsDataTable` 中每个 `ProductsRow` 实例的 `RowState` 设置为 `Modified`，然后将 `ProductsDataTable` 传递到 DAL s `UpdateWithTransaction` 方法。

[!code-csharp[Main](batch-updating-cs/samples/sample8.cs)]

## <a name="summary"></a>摘要

GridView 提供内置的按行编辑功能，但缺少创建完全可编辑的接口的支持。 正如我们在本教程中看到的那样，这些接口是可能的，但需要一些工作。 若要创建每个行都可编辑的 GridView，需要将 GridView 的字段转换为 Templatefield，并在 `ItemTemplate` 中定义编辑界面。 此外，必须将 "更新所有类型" 按钮 Web 控件添加到页面中，与 GridView 分离。 这些按钮 `Click` 事件处理程序需要枚举 GridView `Rows` 集合、将更改存储在 `ProductsDataTable`中，并将更新的信息传递到适当的 BLL 方法。

在下一教程中，我们将了解如何创建用于批量删除的接口。 具体而言，每个 GridView 行将包含一个复选框，而不是 "更新所有类型" 按钮，我们将删除选定的行按钮。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Teresa Murphy 和 David Suru。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](wrapping-database-modifications-within-a-transaction-cs.md)
> [下一页](batch-deleting-cs.md)
