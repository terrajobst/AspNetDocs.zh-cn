---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
title: 执行批量更新（VB） |Microsoft Docs
author: rick-anderson
description: 了解如何创建完全可编辑的 DataList，其中所有项都处于编辑模式，并且可以通过单击上的 "全部更新" 按钮来保存其值。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 8dac22a7-91de-4e3b-888f-a4c438b03851
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
msc.type: authoredcontent
ms.openlocfilehash: e54c9fc12da278492b54164cf657eea142a3dae6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78494750"
---
# <a name="performing-batch-updates-vb"></a>执行批量更新 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_VB.exe)或[下载 PDF](performing-batch-updates-vb/_static/datatutorial37vb1.pdf)

> 了解如何创建完全可编辑的 DataList，其中所有项都处于编辑模式，并且可以通过单击页面上的 "全部更新" 按钮来保存其值。

## <a name="introduction"></a>简介

在[前面的教程](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)中，我们探讨了如何创建项级 DataList。 与标准的可编辑 GridView 类似，DataList 中的每一项都包含一个编辑按钮，单击此按钮将使该项可编辑。 尽管此项级编辑适用于仅偶尔更新的数据，但某些用例方案需要用户编辑多个记录。 如果用户需要编辑数十个记录，并强制单击 "编辑"，进行更改，然后单击每个记录的 "更新"，则单击的量会妨碍她的工作效率。 在这种情况下，更好的选择是提供一个完全可编辑的 DataList，其中的*所有*项目都处于编辑模式，并且可以通过单击页面上的 "全部更新" 按钮来编辑其值（请参阅图1）。

[可以修改完全可编辑的 DataList 中的每个项 ![](performing-batch-updates-vb/_static/image2.png)](performing-batch-updates-vb/_static/image1.png)

**图 1**：可以修改完全可编辑的 DataList 中的每个项（[单击以查看完全大小的图像](performing-batch-updates-vb/_static/image3.png)）

在本教程中，我们将探讨如何使用户能够使用完全可编辑的 DataList 更新供应商地址信息。

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a>步骤1：在 DataList s ItemTemplate 中创建可编辑的用户界面

在前面的教程中，我们将创建一个标准的项级可编辑 DataList，其中使用了两个模板：

- `ItemTemplate` 包含了只读用户界面（用于显示每个产品名称和价格的标签 Web 控件）。
- `EditItemTemplate` 包含编辑模式用户界面（两个 TextBox Web 控件）。

DataList s `EditItemIndex` 属性决定使用 `EditItemTemplate`呈现哪些 `DataListItem` （如果有）。 具体而言，`DataListItem` 的 `ItemIndex` 值与 DataList s `EditItemIndex` 属性匹配，则使用 `EditItemTemplate`进行呈现。 当一次只能编辑一个项，但在创建完全可编辑的 DataList 时，此模型的效果很好。

对于完全可编辑的 DataList，我们希望*所有 `DataListItem` 都*使用可编辑界面进行呈现。 实现此目的的最简单方法是在 `ItemTemplate`中定义可编辑接口。 对于修改供应商地址信息，可编辑界面将供应商名称包含为文本，然后是地址、城市和国家/地区值的文本框。

首先打开 "`BatchUpdate.aspx`" 页，添加 "DataList" 控件，并将其 `ID` 属性设置为 "`Suppliers`"。 从 DataList s 智能标记中，选择添加名为 `SuppliersDataSource`的新 ObjectDataSource 控件。

[![创建一个名为 SuppliersDataSource 的新 ObjectDataSource](performing-batch-updates-vb/_static/image5.png)](performing-batch-updates-vb/_static/image4.png)

**图 2**：创建名为 `SuppliersDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](performing-batch-updates-vb/_static/image6.png)）

将 ObjectDataSource 配置为使用 `SuppliersBLL` 类 `GetSuppliers()` 方法检索数据（参见图3）。 与前面的教程不同，我们将直接使用业务逻辑层，而不是通过 ObjectDataSource 更新供应商信息。 因此，请在 "更新" 选项卡中将下拉列表设置为 "（无）" （参见图4）。

[![使用 GetSuppliers （）方法检索供应商信息](performing-batch-updates-vb/_static/image8.png)](performing-batch-updates-vb/_static/image7.png)

**图 3**：使用 `GetSuppliers()` 方法检索供应商信息（[单击以查看完全大小的图像](performing-batch-updates-vb/_static/image9.png)）

[![在 "更新" 选项卡中将下拉列表设置为 "（无）"](performing-batch-updates-vb/_static/image11.png)](performing-batch-updates-vb/_static/image10.png)

**图 4**：在 "更新" 选项卡中将下拉列表设置为 "（无）" （[单击查看完全大小的图像](performing-batch-updates-vb/_static/image12.png)）

完成向导后，Visual Studio 会自动生成 DataList s `ItemTemplate` 以显示标签 Web 控件中由数据源返回的每个数据字段。 我们需要修改此模板，使其改为提供编辑界面。 通过使用 DataList s 智能标记中的 "编辑模板" 选项或直接通过声明性语法，可以通过设计器自定义 `ItemTemplate`。

花点时间创建一个编辑界面，该界面将供应商姓名显示为文本，但包含供应商地址、城市和国家/地区值的文本框。 进行这些更改后，页的声明性语法应类似于以下形式：

[!code-aspx[Main](performing-batch-updates-vb/samples/sample1.aspx)]

> [!NOTE]
> 与前面的教程一样，本教程中的 DataList 必须启用其视图状态。

在 `ItemTemplate` I m 使用两个新的 CSS 类 `SupplierPropertyLabel` 和 `SupplierPropertyValue`，已添加到 `Styles.css` 类并配置为使用与 `ProductPropertyLabel` 和 `ProductPropertyValue` CSS 类相同的样式设置。

[!code-css[Main](performing-batch-updates-vb/samples/sample2.css)]

进行这些更改后，请通过浏览器访问此页。 如图5所示，每个 DataList 项都将供应商名称显示为文本，并使用文本框显示地址、城市和国家/地区。

[DataList 中的每个供应商都可编辑 ![](performing-batch-updates-vb/_static/image14.png)](performing-batch-updates-vb/_static/image13.png)

**图 5**： DataList 中的每个供应商都是可编辑的（[单击以查看完全大小的图像](performing-batch-updates-vb/_static/image15.png)）

## <a name="step-2-adding-an-update-all-button"></a>步骤2：添加 "全部更新" 按钮

虽然图5中的每个供应商都在文本框中显示 "地址"、"城市" 和 "国家/地区" 字段，但目前没有可用的 "更新" 按钮。 通常，页面上只会有一个 "全部更新" 按钮，在单击该按钮时，会更新 DataList 中的*所有*记录，而不是每项使用 "更新" 按钮。 在本教程中，我们将添加两个 "全部更新" 按钮-一个位于页面顶部，另一个按钮位于底部（尽管单击任一按钮都将具有相同的效果）。

首先将一个按钮 Web 控件添加到 DataList 上方，然后将其 `ID` 属性设置为 `UpdateAll1`。 接下来，将第二个按钮 Web 控件添加到 DataList 下，并将其 `ID` 设置为 `UpdateAll2`。 设置两个按钮的 `Text` 属性以更新所有按钮。 最后，为两个按钮 `Click` 事件创建事件处理程序。 我们不是在每个事件处理程序中复制更新逻辑，而是将该逻辑重构为第三个方法，`UpdateAllSupplierAddresses`，让事件处理程序只调用此第三种方法。

[!code-vb[Main](performing-batch-updates-vb/samples/sample3.vb)]

图6显示了 "更新所有" 按钮添加后的页面。

[已将两个更新全部按钮添加到页面中 ![](performing-batch-updates-vb/_static/image17.png)](performing-batch-updates-vb/_static/image16.png)

**图 6**：已将两个 "更新" 按钮添加到页面（[单击查看完全尺寸的图像](performing-batch-updates-vb/_static/image18.png)）

## <a name="step-3-updating-all-of-the-suppliers-address-information"></a>步骤3：更新所有供应商地址信息

所有 DataList 项都显示编辑界面，并添加了 "全部更新" 按钮，剩下的就是编写代码来执行批更新。 具体而言，我们需要遍历 DataList 项，并为每个项调用 `SuppliersBLL` 类的 `UpdateSupplierAddress` 方法。

构成 DataList 的 `DataListItem` 实例的集合可以通过 DataList s [`Items` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx)进行访问。 引用 `DataListItem`后，可以从 `DataKeys` 集合中获取相应的 `SupplierID`，并以编程方式引用 `ItemTemplate` 中的 TextBox Web 控件，如以下代码所示：

[!code-vb[Main](performing-batch-updates-vb/samples/sample4.vb)]

当用户单击其中一个 "全部更新" 按钮时，`UpdateAllSupplierAddresses` 方法将循环访问 `Suppliers` DataList 中的每个 `DataListItem`，并调用 `SuppliersBLL` 类 `UpdateSupplierAddress` 方法，并传入相应的值。 "地址"、"城市" 或 "国家/地区" 传递的非输入值是 `Nothing` `UpdateSupplierAddress` 的值（而不是空字符串），这会导致数据库 `NULL` 基础记录 s 字段。

> [!NOTE]
> 作为增强功能，您可能需要将状态标签 Web 控件添加到在执行批更新之后提供了一些确认消息的页面。

## <a name="updating-only-those-addresses-that-have-been-modified"></a>仅更新那些已修改的地址

用于本教程的批处理更新算法将为 DataList 中的*每个*供应商调用 `UpdateSupplierAddress` 方法，而不考虑其地址信息是否已更改。 尽管此类直接更新并不是性能问题，但如果您对数据库表进行了审核更改，它们可能会导致不需要的记录。 例如，如果使用触发器将所有 `UPDATE` `Suppliers` s 记录到审核表，则每次用户单击 "全部更新" 按钮时，系统将为系统中的每个供应商创建一个新的审核记录，而不管用户是否进行了任何更改。

ADO.NET DataTable 和 DataAdapter 类的设计目的是支持批更新，在这种情况下，仅修改、删除和新记录会导致任何数据库通信。 DataTable 中的每一行都有一个[`RowState` 属性](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx)，该属性指示行是添加到 DataTable、从其删除、修改还是保持不变。 最初填充 DataTable 时，所有行都将被标记为保持不变。 更改任意行的列的值会将该行标记为已修改。

在 `SuppliersBLL` 类中，我们将通过先将单个供应商记录读入 `SuppliersDataTable`，然后使用以下代码设置 `Address`、`City`和 `Country` 列值，来更新指定的供应商地址信息：

[!code-vb[Main](performing-batch-updates-vb/samples/sample5.vb)]

此代码 naively 将传入的地址、城市和国家/地区值分配到 `SuppliersDataTable` 中的 `SuppliersRow`，无论这些值是否已更改。 这些修改将导致 `SuppliersRow` 的 `RowState` 属性标记为已修改。 调用数据访问层的 `Update` 方法时，它会看到 `SupplierRow` 已被修改，因此会将 `UPDATE` 命令发送到数据库。

但是，假设我们向此方法添加了代码，以便仅分配传入的地址、城市和国家/地区值，因为它们不同于 `SuppliersRow` 的现有值。 如果地址、城市和国家/地区与现有数据相同，则不会进行更改，并且 `SupplierRow` 的 `RowState` 将被标记为 "未更改"。 最终的结果是，当调用 DAL s `Update` 方法时，不会进行任何数据库调用，因为 `SuppliersRow` 尚未修改。

若要执行此更改，请将以下代码替换为传入的地址、城市和国家/地区值，并将其替换为以下代码：

[!code-vb[Main](performing-batch-updates-vb/samples/sample6.vb)]

使用此添加的代码，DAL s `Update` 方法仅将 `UPDATE` 语句发送到数据库，以获取与地址相关的值已更改的那些记录。

此外，我们还可以跟踪传入地址字段与数据库数据之间是否存在任何差异，如果没有，只需绕过对 DAL s `Update` 方法的调用。 如果你重新使用 DB 直接方法，则此方法非常适用，因为 DB 直接方法不会传递一个 `SuppliersRow` 实例，该实例的 `RowState` 可以进行检查以确定是否确实需要数据库调用。

> [!NOTE]
> 每次调用 `UpdateSupplierAddress` 方法时，对数据库进行调用以检索有关已更新记录的信息。 如果数据有任何更改，则会对数据库进行另一次调用以更新表行。 此工作流可以通过创建 `UpdateSupplierAddress` 方法重载来进行优化，该重载接受 `BatchUpdate.aspx` 页中*所有*更改的 `EmployeesDataTable` 实例。 然后，它可以调用数据库以获取 `Suppliers` 表中的所有记录。 然后，可以枚举这两个结果集，并且只能更新发生更改的记录。

## <a name="summary"></a>摘要

在本教程中，我们了解了如何创建完全可编辑的 DataList，使用户能够快速修改多个供应商的地址信息。 首先，我们为 DataList s `ItemTemplate`中的供应商地址、城市和国家/地区值定义了编辑界面。 接下来，我们添加了 "更新" DataList 上方和下方的所有按钮。 用户进行了更改，并单击了 "全部更新" 按钮之一后，会枚举 `DataListItem`，并对 `SuppliersBLL` 类 `UpdateSupplierAddress` 方法进行调用。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Zack 和 Ken Pespisa。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
> [下一页](handling-bll-and-dal-level-exceptions-vb.md)
