---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
title: 检查与插入、更新和删除（C#）相关联的事件 |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将使用 ASP.NET 数据 Web 控件的插入、更新或删除操作前后的事件进行检查。 W 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: dab291a0-a8b5-46fa-9dd8-3d35b249201f
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: a8c1388b73524a8bb918b67aa265db894c07636f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74571926"
---
# <a name="examining-the-events-associated-with-inserting-updating-and-deleting-c"></a>检查与插入、更新和删除操作有关的事件 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_CS.exe)或[下载 PDF](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/datatutorial17cs1.pdf)

> 在本教程中，我们将使用 ASP.NET 数据 Web 控件的插入、更新或删除操作前后的事件进行检查。 我们还将了解如何自定义编辑界面，以便仅更新产品字段的子集。

## <a name="introduction"></a>简介

使用内置的插入、编辑或删除 GridView、DetailsView 或 FormView 控件的功能时，最终用户完成添加新记录或更新或删除现有记录的过程时，会发生各种步骤。 如[前面的教程](an-overview-of-inserting-updating-and-deleting-data-cs.md)中所述，在 GridView 中编辑某一行时，"编辑" 按钮将被 "更新" 和 "取消" 按钮替换，并且 BoundFields 转换为文本框。 最终用户更新数据并单击 "更新" 后，将对回发执行以下步骤：

1. GridView 使用已编辑记录的唯一标识字段（通过 `DataKeyNames` 属性）和用户输入的值填充其 ObjectDataSource 的 `UpdateParameters`
2. GridView 调用其 ObjectDataSource `Update()` 方法，该方法反过来调用基础对象中的相应方法（`ProductsDAL.UpdateProduct`，在前面的教程中）
3. 底层数据现在包含更新的更改，将重新绑定到 GridView

在此步骤序列过程中，会触发大量事件，使我们能够创建事件处理程序，以便在需要时添加自定义逻辑。 例如，在步骤1之前，激发了 GridView 的 `RowUpdating` 事件。 如果出现某些验证错误，我们可以在此时取消更新请求。 调用 `Update()` 方法时，将激发 ObjectDataSource 的 `Updating` 事件，从而提供添加或自定义任意 `UpdateParameters`的值的机会。 在 ObjectDataSource 的基础对象的方法完成执行后，将引发 ObjectDataSource 的 `Updated` 事件。 `Updated` 事件的事件处理程序可以检查有关更新操作的详细信息，例如，受影响的行数以及是否发生了异常。 最后，在步骤2之后，将激发 GridView 的 `RowUpdated` 事件;此事件的事件处理程序可以检查有关刚执行的更新操作的其他信息。

图1描述了更新 GridView 时的这一系列事件和步骤。 图1中的事件模式对于使用 GridView 进行更新并不是唯一的。 从 GridView、DetailsView 或 FormView precipitates 插入、更新或删除数据时，对于数据 Web 控件和 ObjectDataSource，都具有相同的前期和后期级别事件的序列。

[在 GridView 中更新数据时，![一系列事件和事件后激发](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image1.png)

**图 1**：更新 GridView 中的数据时，一系列事件和事件后激发（[单击查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image3.png)）

在本教程中，我们将检查如何使用这些事件来扩展 ASP.NET 数据 Web 控件的内置插入、更新和删除功能。 我们还将了解如何自定义编辑界面，以便仅更新产品字段的子集。

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>步骤1：更新产品的`ProductName`和`UnitPrice`字段

在上一教程中，编辑界面中的*所有*不是只读的产品字段都必须包括在内。 如果我们要从 GridView 中删除字段（例如 `QuantityPerUnit`-更新数据时，数据 Web 控件不会将 ObjectDataSource 的 `QuantityPerUnit` `UpdateParameters` 值。 然后，ObjectDataSource 将 `null` 值传入 `UpdateProduct` 业务逻辑层（BLL）方法，该方法会将编辑的数据库记录的 `QuantityPerUnit` 列更改为 `NULL` 值。 同样，如果从编辑界面删除了某个必填字段（如 `ProductName`），则更新将失败，并出现 "*列 ' ProductName ' 不允许空值*" 异常。 此行为的原因是，ObjectDataSource 配置为调用 `ProductsBLL` 类的 `UpdateProduct` 方法，该方法需要每个产品字段的输入参数。 因此，ObjectDataSource 的 `UpdateParameters` 集合包含该方法的每个输入参数的参数。

如果我们想要提供一个允许最终用户仅更新字段子集的数据 Web 控件，则需要以编程方式在 ObjectDataSource 的 `Updating` 事件处理程序中设置缺少的 `UpdateParameters` 值，或者创建和调用只需要一部分字段的 BLL 方法。 让我们探讨后一种方法。

具体而言，我们将创建一个页面，只显示可编辑 GridView 中的 `ProductName` 和 `UnitPrice` 字段。 此 GridView 的编辑界面只允许用户更新两个显示的字段 `ProductName` 和 `UnitPrice`。 由于此编辑接口仅提供产品字段的子集，因此，我们需要创建一个 ObjectDataSource，该 ObjectDataSource 使用现有的 BLL `UpdateProduct` 方法，并在其 `Updating` 事件处理程序中以编程方式设置缺失的产品字段值，或者我们需要创建一个新的 BLL 方法，该方法只需要在 GridView 中定义的字段的子集。 对于本教程，我们将使用后一个选项，并创建 `UpdateProduct` 方法的重载，该重载只使用三个输入参数： `productName`、`unitPrice`和 `productID`：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample1.cs)]

与原始 `UpdateProduct` 方法一样，此重载通过检查数据库中是否存在具有指定 `ProductID`的产品开始。 否则，它将返回 `false`，指示更新产品信息的请求失败。 否则，它会相应地更新现有产品记录的 `ProductName` 和 `UnitPrice` 字段，并通过调用 TableAdapter 的 `Update()` 方法，并传入 `ProductsRow` 实例来提交更新。

通过此类添加到 `ProductsBLL` 类，可以创建简化的 GridView 界面。 打开 `EditInsertDelete` 文件夹中的 `DataModificationEvents.aspx`，并向页面添加 GridView。 创建新的 ObjectDataSource，并将其配置为使用 `ProductsBLL` 类，并将其 `Select()` 方法映射到 `GetProducts`，并将其 `Update()` 方法映射到仅采用 `UpdateProduct`、`productName`和 `unitPrice`输入参数的 `productID` 重载。 图2显示了在将 ObjectDataSource 的 `Update()` 方法映射到 `ProductsBLL` 类的新 `UpdateProduct` 方法重载时创建数据源向导。

[![将 ObjectDataSource 的 Update （）方法映射到新的 UpdateProduct 重载](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image4.png)

**图 2**：将 ObjectDataSource 的 `Update()` 方法映射到新的 `UpdateProduct` 重载（[单击以查看完全大小的映像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image6.png)）

由于我们的示例最初只需要能够编辑数据，而不是插入或删除记录，因此请花一些时间来明确指出，不应通过转到 "插入" 和 "删除" 选项卡，然后从下拉列表中选择 "（无）" 来将 ObjectDataSource 的 `Insert()` 和 `Delete()` 方法映射到任何 `ProductsBLL` 类的方法。

[从 "插入" 和 "删除" 选项卡的下拉列表中选择 "（无）" ![](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image7.png)

**图 3**：从 "插入" 和 "删除" 选项卡的下拉列表中选择 "（无）" （[单击查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image9.png)）

完成此向导后，请从 GridView 的智能标记中选中 "启用编辑" 复选框。

完成创建数据源向导并将其绑定到 GridView 后，Visual Studio 将为这两个控件创建了声明性语法。 请中转到 "源" 视图以检查 ObjectDataSource 的声明性标记，如下所示：

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample2.aspx)]

由于不存在用于 ObjectDataSource 的 `Insert()` 和 `Delete()` 方法的映射，因此没有 `InsertParameters` 或 `DeleteParameters` 部分。 此外，由于 `Update()` 方法映射到仅接受三个输入参数的 `UpdateProduct` 方法重载，`UpdateParameters` 节只包含三个 `Parameter` 实例。

请注意，ObjectDataSource 的 `OldValuesParameterFormatString` 属性设置为 `original_{0}`。 使用 "配置数据源" 向导时，Visual Studio 会自动设置此属性。 但是，由于 BLL 方法不希望传入原始 `ProductID` 值，因此请从 ObjectDataSource 的声明性语法中删除此属性赋值。

> [!NOTE]
> 如果只是从设计视图的属性窗口中清除 `OldValuesParameterFormatString` 属性值，则该属性仍将在声明性语法中存在，但会设置为空字符串。 从声明性语法中删除完全相同的属性，或者从属性窗口中将此值设置为默认值，`{0}`。

尽管 ObjectDataSource 只为产品的名称、价格和 ID `UpdateParameters`，但 Visual Studio 已为产品的每个字段在 GridView 中添加了 BoundField 或 CheckBoxField。

[![GridView 包含每个产品字段的 BoundField 或 CheckBoxField](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image10.png)

**图 4**： GridView 包含产品每个字段的 BoundField 或 CheckBoxField （[单击以查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image12.png)）

当最终用户编辑产品并单击其 "更新" 按钮时，GridView 会枚举不是只读字段的字段。 然后，它将 ObjectDataSource 的 `UpdateParameters` 集合中相应参数的值设置为用户输入的值。 如果没有相应的参数，则 GridView 会将其添加到集合中。 因此，如果 GridView 包含所有产品的字段的 BoundFields 和 CheckBoxFields，则 ObjectDataSource 最终将调用获取所有这些参数的 `UpdateProduct` 重载，尽管 ObjectDataSource 的声明性标记只指定了三个输入参数（参见图5）。 同样，如果 GridView 中存在与 `UpdateProduct` 重载的输入参数不对应的非只读 product 字段的组合，则在尝试更新时将引发异常。

[![GridView 会将参数添加到 ObjectDataSource 的 UpdateParameters 集合中](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image13.png)

**图 5**： GridView 将参数添加到 ObjectDataSource 的 `UpdateParameters` 集合（[单击查看完全大小的映像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image15.png)）

若要确保 ObjectDataSource 调用只采用产品名称、价格和 ID 的 `UpdateProduct` 重载，则需要将 GridView 限制为仅具有 `ProductName` 和 `UnitPrice`的可编辑字段。 这可以通过以下方式实现：删除其他 BoundFields 和 CheckBoxFields，将其他字段的 `ReadOnly` 属性设置为 `true`或这两者的组合。 对于本教程，我们只需删除除 `ProductName` 和 `UnitPrice` BoundFields 以外的所有 GridView 字段，之后 GridView 的声明性标记将如下所示：

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample3.aspx)]

即使 `UpdateProduct` 重载需要三个输入参数，在 GridView 中我们还是只有两 BoundFields。 这是因为 `productID` 输入参数是一个主键值，并且通过所编辑的行的 `DataKeyNames` 属性的值进行传递。

我们的 GridView 与 `UpdateProduct` 重载一起使用，允许用户仅编辑产品的名称和价格，而不会丢失任何其他产品字段。

[![界面仅允许编辑产品的名称和价格](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image16.png)

**图 6**：接口只允许编辑产品的名称和价格（[单击查看全尺寸图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image18.png)）

> [!NOTE]
> 如前面的教程中所述，必须启用 GridView 的视图状态（默认行为），这一点至关重要。 如果将 GridView `EnableViewState` 属性设置为 "`false`"，则可能会遇到使并发用户无意中删除或编辑记录的风险。 有关详细信息，请参阅[ASP.NET 2.0 GridViews/DetailsView/FormViews 的并发问题，其中支持编辑和/或删除并禁用了其视图状态](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx)。

## <a name="improving-theunitpriceformatting"></a>改善`UnitPrice`格式

虽然图6中所示的 GridView 示例是可行的，但 "`UnitPrice`" 字段不是格式的，这会导致价格显示缺少任何货币符号，且具有四个小数位。 若要为不可编辑的行应用货币格式设置，只需将 `UnitPrice` BoundField 的 `DataFormatString` 属性设置为 `{0:c}`，并将其 `HtmlEncode` 属性设置为 `false`。

[![设置 DataFormatString 和 Server.htmlencode 属性](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image19.png)

**图 7**：相应地设置 `UnitPrice`的 `DataFormatString` 和 `HtmlEncode` 属性（[单击以查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image21.png)）

进行此更改后，不可编辑的行将价格设置为货币格式;但已编辑的行仍会显示值，但不包含货币符号和四个小数位。

[现在 ![不可编辑的行的格式设置为货币值](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image22.png)

**图 8**：不可编辑的行现在已格式化为货币值（[单击以查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image24.png)）

通过将 BoundField 的 `ApplyFormatInEditMode` 属性设置为 `true` （默认值为 `false`），可以将 `DataFormatString` 属性中指定的格式设置指令应用于编辑界面。 请花点时间将此属性设置为 `true`。

[![将 BoundField 的 ApplyFormatInEditMode 属性设置为 true](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image25.png)

**图 9**：将 `UnitPrice` BoundField 的 `ApplyFormatInEditMode` 属性设置为 `true` （[单击查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image27.png)）

进行此更改后，所编辑的行中显示的 `UnitPrice` 的值也将设置为货币格式。

[![编辑的行的 "单价" 值现在已设置为货币格式](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image28.png)

**图 10**：已编辑的行的 `UnitPrice` 值现在已设置为货币格式（[单击查看完全尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image30.png)）

但是，在文本框（如 $19.00）中使用货币符号更新产品会引发 `FormatException`。 当 GridView 尝试将用户提供的值分配给 ObjectDataSource 的 `UpdateParameters` 集合时，它无法将 `UnitPrice` 字符串 "$19.00" 转换为参数所需的 `decimal` （参见图11）。 若要解决此情况，可以为 GridView 的 `RowUpdating` 事件创建事件处理程序，并让它将用户提供的 `UnitPrice` 分析为货币格式的 `decimal`。

GridView 的 `RowUpdating` 事件接受[GridViewUpdateEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx)类型的对象作为其第二个参数，其中包含一个 `NewValues` 字典作为其属性之一，其中包含可分配给 ObjectDataSource 的 `UpdateParameters` 集合的用户提供的值。 我们可以使用以下代码行在 `RowUpdating` 事件处理程序中，用货币格式分析的十进制值覆盖 `NewValues` 集合中的现有 `UnitPrice` 值：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample4.cs)]

如果用户提供了一个 `UnitPrice` 值（如 "$19.00"），则使用 Decimal 计算所得的十进制值覆盖此值。 [Parse](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx)，将值分析为货币。 这将在任何货币符号、逗号、小数点等的情况下正确分析 decimal，并使用 NumberStyles[命名空间中的](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx)[枚举](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx)。

图11显示了用户提供的 `UnitPrice`中的货币符号导致的问题，以及如何利用 GridView 的 `RowUpdating` 事件处理程序来正确分析此类输入。

[![编辑的行的 "单价" 值现在已设置为货币格式](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image31.png)

**图 11**：已编辑的行的 `UnitPrice` 值现在已设置为货币格式（[单击查看完全尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image33.png)）

## <a name="step-2-prohibitingnull-unitprices"></a>步骤2：禁止`NULL UnitPrices`

当数据库被配置为允许 `Products` 表的 `UnitPrice` 列中 `NULL` 值时，我们可能希望阻止用户通过指定 `NULL` `UnitPrice` 值来访问此特定页面。 也就是说，如果用户在编辑产品行时无法输入 `UnitPrice` 值，而不是将结果保存到数据库中，我们想要显示一条消息，告知用户在此页上，任何已编辑的产品都必须指定价格。

传递到 GridView `RowUpdating` 事件处理程序中的 `GridViewUpdateEventArgs` 对象包含一个 `Cancel` 属性，如果设置为 `true`，则终止更新过程。 接下来，我们将扩展 `RowUpdating` 事件处理程序，将 `e.Cancel` 设置为 `true` 并显示一条消息，说明 `NewValues` 集合中的 `UnitPrice` 值是否 `null`。

首先，将 "标签" Web 控件添加到名为 "`MustProvideUnitPriceMessage`" 的页。 如果在更新产品时用户未能指定 `UnitPrice` 值，则将显示此 "标签" 控件。 将标签的 `Text` 属性设置为 "必须提供产品价格"。 我还使用以下定义，在名为 `Warning` 的 `Styles.css` 中创建了一个新的 CSS 类：

[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample5.css)]

最后，将标签的 `CssClass` 属性设置为 `Warning`。 此时，设计器应显示警告消息，其中红色、粗体、斜体、小字体大小在 GridView 之上，如图12所示。

[![在 GridView 上方添加标签](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image34.png)

**图 12**：已在 GridView 上方添加标签（[单击以查看完全尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image36.png)）

默认情况下，应隐藏此标签，以便将其 `Visible` 属性设置为在 `Page_Load` 事件处理程序中 `false`：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample6.cs)]

如果用户在未指定 `UnitPrice`的情况下尝试更新产品，我们想要取消更新并显示警告标签。 增加 GridView 的 `RowUpdating` 事件处理程序，如下所示：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample7.cs)]

如果用户在未指定价格的情况下尝试保存产品，则将取消更新并显示有用的消息。 尽管数据库（和业务逻辑）允许 `NULL` `UnitPrice`，但这一特定的 ASP.NET 页面并不允许。

[![用户不能将单价留空](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image37.png)

**图 13**：用户不能将 `UnitPrice` 留空（[单击查看完全尺寸的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image39.png)）

到目前为止，我们已了解如何使用 GridView 的 `RowUpdating` 事件以编程方式更改分配给 ObjectDataSource 的 `UpdateParameters` 集合的参数值，以及如何完全取消更新过程。 这些概念将传输到 DetailsView 和 FormView 控件，并适用于插入和删除。

还可以通过事件处理程序在 ObjectDataSource 级别为其 `Inserting`、`Updating`和 `Deleting` 事件完成这些任务。 这些事件在调用基础对象的关联方法之前激发，并为最后修改输入参数集合或完全取消操作提供了最后机会。 这三个事件的事件处理程序将传递[ObjectDataSourceMethodEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx)类型的对象，该对象具有两个相关属性：

- [取消](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx)，此操作如果设置为 `true`，则取消正在执行的操作
- [输入参数](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx)，它是 `InsertParameters`、`UpdateParameters`或 `DeleteParameters`的集合，具体取决于事件处理程序是用于 `Inserting`、`Updating`还是 `Deleting` 事件

为了说明如何在 ObjectDataSource 级别使用参数值，让我们在页面中包含一项 DetailsView，使用户能够添加新产品。 此 DetailsView 将用于提供一个界面，用于快速将新产品添加到数据库。 若要在添加新产品时保持一致的用户界面，则允许用户仅输入 "`ProductName`" 和 "`UnitPrice`" 字段的值。 默认情况下，DetailsView 的插入界面中未提供的那些值将设置为 `NULL` 数据库值。 但是，我们可以使用 ObjectDataSource 的 `Inserting` 事件注入不同的默认值，正如我们稍后将看到的那样。

## <a name="step-3-providing-an-interface-to-add-new-products"></a>步骤3：提供添加新产品的接口

将 DetailsView 从工具箱拖到 GridView 上方的设计器中，清除其 `Height` 和 `Width` 属性，并将其绑定到页面上已存在的 ObjectDataSource。 这会为产品的每个字段添加 BoundField 或 CheckBoxField。 由于我们希望使用此 DetailsView 来添加新产品，因此需要从智能标记中选中 "启用插入" 选项;但是，没有这样的选项，因为 ObjectDataSource 的 `Insert()` 方法未映射到 `ProductsBLL` 类中的方法（请记住，在配置数据源时将此映射设置为（None），请参见图3）。

若要配置 ObjectDataSource，请从其智能标记中选择 "配置数据源" 链接，启动向导。 第一个屏幕允许您更改 ObjectDataSource 绑定到的基础对象;将其设置为 `ProductsBLL`。 下一屏幕中列出了从 ObjectDataSource 的方法到基础对象的映射。 即使我们明确指出，不应将 `Insert()` 和 `Delete()` 方法映射到任何方法，如果您访问 "插入" 和 "删除" 选项卡，您将看到映射存在。 这是因为 `ProductsBLL`的 `AddProduct` 和 `DeleteProduct` 方法使用 `DataObjectMethodAttribute` 特性来指示它们分别是 `Insert()` 和 `Delete()`的默认方法。 因此，在每次运行向导时，ObjectDataSource 向导会选择这些值，除非显式指定了某些其他值。

保留指向 `AddProduct` 方法的 `Insert()` 方法，但再次将 "删除" 选项卡的下拉列表设置为 "（无）"。

[![将 "插入" 选项卡的下拉列表设置为 AddProduct 方法](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image40.png)

**图 14**：将 "插入" 选项卡的下拉列表设置为 `AddProduct` 方法（[单击以查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image42.png)）

[![将 "删除" 选项卡的下拉列表设置为 "（无）"](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image43.png)

**图 15**：将 "删除" 选项卡的下拉列表设置为 "（无）" （[单击查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image45.png)）

进行这些更改后，ObjectDataSource 的声明性语法将展开以包括 `InsertParameters` 集合，如下所示：

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample8.aspx)]

重新运行已添加回 `OldValuesParameterFormatString` 属性的向导。 通过将此属性设置为默认值（`{0}`）或从声明性语法中删除它，花一些时间。

借助提供插入功能的 ObjectDataSource，DetailsView 的智能标记现在将包括 "启用插入" 复选框;返回到设计器并选中此选项。 接下来，削减 DetailsView，使其只具有两个 BoundFields `ProductName` `UnitPrice` 和 CommandField。 此时，DetailsView 的声明性语法应该如下所示：

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample9.aspx)]

图16此时会显示此页。 如您所见，DetailsView 列出了第一个产品的名称和价格（Chai）。 但我们想要的是一个插入接口，该接口为用户提供了一种将新产品快速添加到数据库的方法。

[![DetailsView 当前以只读模式呈现](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image46.png)

**图 16**： DetailsView 当前呈现为只读模式（[单击以查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image48.png)）

若要在插入模式下显示 DetailsView，需要将 `DefaultMode` 属性设置为 `Inserting`。 这会在首次访问时在插入模式下呈现 DetailsView，并在插入新记录后将其保存。 如图17所示，此类 DetailsView 提供了一个用于添加新记录的快速界面。

[![DetailsView 提供了一个界面，用于快速添加新产品](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image49.png)

**图 17**： DetailsView 提供了一个界面，用于快速添加新产品（[单击以查看完全大小的映像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image51.png)）

当用户输入产品名称和价格（例如，如图17所示的 "Acme 水源" 和1.99）并单击 "插入" 时，将在添加到数据库中的新产品记录中 culminating 回发可以和插入工作流开始。 DetailsView 维护其插入界面，GridView 会自动重新绑定到其数据源，以便包括新产品，如图18所示。

![产品](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image52.png)

**图 18**：已将产品 "Acme 水源" 添加到数据库中

虽然图18中的 GridView 并未显示，但从 DetailsView 界面 `CategoryID`、`SupplierID`、`QuantityPerUnit`等的产品字段被分配 `NULL` 数据库值。 可以通过执行以下步骤来查看此内容：

1. 在 Visual Studio 中转到服务器资源管理器
2. 展开 `NORTHWND.MDF` 数据库节点
3. 右键单击 "`Products` 数据库" 表节点
4. 选择 "显示表数据"

这将列出 `Products` 表中的所有记录。 如图19所示，除 `ProductID`、`ProductName`和 `UnitPrice` 之外的所有新产品列都具有 `NULL` 值。

[![未在 DetailsView 中提供的产品字段分配 NULL 值](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image53.png)

**图 19**： DetailsView 中未提供的产品字段分配 `NULL` 值（[单击以查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image55.png)）

对于一个或多个此类值，我们可能需要提供除 `NULL` 以外的默认值，因为 `NULL` 不是最佳的默认选项，或者数据库列本身不允许 `NULL`。 为实现此目的，我们可以通过编程方式设置 DetailsView 的 `InputParameters` 集合的参数值。 可在 DetailsView 的 `ItemInserting` 事件的事件处理程序或 ObjectDataSource 的 `Inserting` 事件的事件处理程序中完成此分配。 由于我们已经了解了如何在数据 Web 控件级别使用前期事件和后级事件，因此让我们来探索这次使用 ObjectDataSource 的事件。

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>步骤4：为`CategoryID`和`SupplierID`参数赋值

在本教程中，我们假设你在通过此接口添加新产品时，为应用程序分配了一个 `CategoryID`，并 `SupplierID` 值为1。 如前文所述，ObjectDataSource 包含一对在数据修改过程中激发的前期和后级事件。 调用 `Insert()` 方法时，ObjectDataSource 首先引发其 `Inserting` 事件，然后调用其 `Insert()` 方法已映射到的方法，并最终引发 `Inserted` 事件。 `Inserting` 事件处理程序为我们的最后一次机会来调整输入参数或取消操作。

> [!NOTE]
> 在实际应用程序中，你可能希望让用户指定类别和供应商，或者根据某些条件或业务逻辑为其选择此值（而不是盲目选择 ID 1）。 无论如何，此示例演示如何以编程方式设置 ObjectDataSource 的前期事件的输入参数的值。

请花片刻时间为 ObjectDataSource 的 `Inserting` 事件创建事件处理程序。 请注意，事件处理程序的第二个输入参数是类型 `ObjectDataSourceMethodEventArgs`的对象，它具有用于访问参数集合（`InputParameters`）的属性和用于取消操作的属性（`Cancel`）。

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample10.cs)]

此时，`InputParameters` 属性包含具有从 DetailsView 分配的值的 ObjectDataSource 的 `InsertParameters` 集合。 若要更改其中一个参数的值，只需使用： `e.InputParameters["paramName"] = value`。 因此，若要将 `CategoryID` 和 `SupplierID` 设置为值1，请调整 `Inserting` 事件处理程序，使其类似于以下内容：

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample11.cs)]

这次添加新产品（如 Acme Soda）时，新产品的 `CategoryID` 和 `SupplierID` 列都设置为1（请参阅图20）。

[![新产品现在将其类别 Id 和供应商值设置为1](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image56.png)

**图 20**：新产品现在的 `CategoryID` 和 `SupplierID` 值设置为1（[单击查看完全大小的图像](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image58.png)）

## <a name="summary"></a>总结

在编辑、插入和删除进程的过程中，数据 Web 控件和 ObjectDataSource 都继续经历多个前期和后期级别事件。 在本教程中，我们检查了预级别事件，并了解了如何使用这些事件来自定义输入参数或从数据 Web 控件和 ObjectDataSource 的事件中取消数据修改操作。 在下一教程中，我们将介绍如何创建和使用事件处理程序来执行后级事件。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Jackie Goor 和 Liz Shulok。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](an-overview-of-inserting-updating-and-deleting-data-cs.md)
> [下一页](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
