---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
title: 在 DetailsView 控件（C#）中使用 templatefield |Microsoft Docs
author: rick-anderson
description: "\"DetailsView\" 控件也提供了与 GridView 一起提供的相同 Templatefield 功能。 在本教程中，我们将显示一个产品 。"
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 83efb21f-b231-446e-9356-f4c6cbcc6713
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 55c667800a9fb19d200bcf4b68e2c59ca4ef5d0e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78481862"
---
# <a name="using-templatefields-in-the-detailsview-control-c"></a>在 DetailsView 控件中使用 TemplateField (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_13_CS.exe)或[下载 PDF](using-templatefields-in-the-detailsview-control-cs/_static/datatutorial13cs1.pdf)

> "DetailsView" 控件也提供了与 GridView 一起提供的相同 Templatefield 功能。 在本教程中，我们将使用包含 Templatefield 的 DetailsView 一次显示一种产品。

## <a name="introduction"></a>简介

与 BoundField、CheckBoxField、HyperLinkField 和其他数据字段控件相比，TemplateField 提供的呈现数据的灵活性更高。 在[上一教程](using-templatefields-in-the-gridview-control-cs.md)中，我们介绍了如何在 GridView 中使用 TemplateField 来执行以下操作：

- 在一列中显示多个数据字段值。 具体而言，"`FirstName`" 和 "`LastName`" 字段均合并为一个 GridView 列。
- 使用备用 Web 控件表示数据字段值。 我们看到了如何使用日历控件显示 `HiredDate` 值。
- 基于基础数据显示状态信息。 尽管 "`Employees`" 表不包含返回员工在工作中的天数的列，但我们仍可以使用 TemplateField 和格式设置方法在上一教程中的 GridView 示例中显示此类信息。

"DetailsView" 控件也提供了与 GridView 一起提供的相同 Templatefield 功能。 在本教程中，我们将使用包含两个 Templatefield 的 DetailsView 一次显示一种产品。 第一个 TemplateField 将 `UnitPrice`、`UnitsInStock`和 `UnitsOnOrder` 数据字段合并为一个 DetailsView 行。 第二个 TemplateField 将显示 "`Discontinued`" 字段的值，但如果 `Discontinued` `true`，则将使用格式设置方法显示 "是"，否则将使用 "否"。

[![两个 Templatefield 用于自定义显示](using-templatefields-in-the-detailsview-control-cs/_static/image2.png)](using-templatefields-in-the-detailsview-control-cs/_static/image1.png)

**图 1**：两个 Templatefield 用于自定义显示（[单击以查看完全大小的图像](using-templatefields-in-the-detailsview-control-cs/_static/image3.png)）

让我们进入正题！

## <a name="step-1-binding-the-data-to-the-detailsview"></a>步骤1：将数据绑定到 DetailsView

如前面的教程中所述，使用 Templatefield 时，最容易的方法是创建仅包含 BoundFields 的 DetailsView 控件，然后添加新的 Templatefield，或根据需要将现有 BoundFields 转换为 Templatefield. 因此，通过设计器将 DetailsView 添加到页面，并将其绑定到返回产品列表的 ObjectDataSource，开始本教程。 这些步骤将为产品的每个非布尔值字段以及一个布尔值字段（已停止）的 CheckBoxField 创建 BoundFields。

打开 "`DetailsViewTemplateField.aspx`" 页，并将 "DetailsView" 从工具箱拖到设计器上。 从 DetailsView 的智能标记中，选择添加调用 `ProductsBLL` 类的 `GetProducts()` 方法的新 ObjectDataSource 控件。

[![添加调用 GetProducts （）方法的新 ObjectDataSource 控件](using-templatefields-in-the-detailsview-control-cs/_static/image5.png)](using-templatefields-in-the-detailsview-control-cs/_static/image4.png)

**图 2**：添加调用 `GetProducts()` 方法的新 ObjectDataSource 控件（[单击以查看完全大小的图像](using-templatefields-in-the-detailsview-control-cs/_static/image6.png)）

对于此报表，删除 `ProductID`、`SupplierID`、`CategoryID`和 `ReorderLevel` BoundFields。 接下来，对 BoundFields 进行重新排序，以便 `CategoryName` 和 `SupplierName` BoundFields 立即显示在 `ProductName` BoundField 之后。 根据需要调整 BoundFields 的 `HeaderText` 属性和格式设置属性。 与 GridView 一样，可以通过 "字段" 对话框（在 DetailsView 的智能标记中单击 "编辑字段" 链接）或声明性语法来执行这些 BoundField 级编辑。 最后，清除 DetailsView 的 `Height` 和 `Width` 属性值，以便根据显示的数据允许 DetailsView 控件展开，并选中智能标记中的 "启用分页" 复选框。

进行这些更改后，DetailsView 控件的声明性标记应如下所示：

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample1.aspx)]

花点时间查看浏览器中的页面。 此时，你应该会看到列出了单个产品（Chai）的行，其中的行显示产品的名称、类别、供应商、价格、库存单位数、订单数以及停用状态。

[![使用一系列 BoundFields 显示产品的详细信息](using-templatefields-in-the-detailsview-control-cs/_static/image8.png)](using-templatefields-in-the-detailsview-control-cs/_static/image7.png)

**图 3**：使用一系列 BoundFields 显示产品的详细信息（[单击查看全尺寸图像](using-templatefields-in-the-detailsview-control-cs/_static/image9.png)）

## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>步骤2：将价格、库存量和单位按顺序组合到一个行中

DetailsView 对 `UnitPrice`、`UnitsInStock`和 `UnitsOnOrder` 字段有一行。 可以通过添加新的 TemplateField，或通过将现有 `UnitPrice`、`UnitsInStock`和 `UnitsOnOrder` BoundFields 转换为 TemplateField，将这些数据字段合并为单个行（TemplateField）。 尽管我的个人习惯于转换现有的 BoundFields，但我们还是通过添加新的 TemplateField 来实现。

首先单击 DetailsView 的智能标记中的 "编辑字段" 链接，打开 "字段" 对话框。 接下来，添加一个新的 TemplateField，并将其 `HeaderText` 属性设置为 "价格和库存"，并移动新 TemplateField，使其位于 `UnitPrice` BoundField 的上方。

[![将新的 TemplateField 添加到 DetailsView 控件](using-templatefields-in-the-detailsview-control-cs/_static/image11.png)](using-templatefields-in-the-detailsview-control-cs/_static/image10.png)

**图 4**：向 DetailsView 控件添加新的 TemplateField （[单击查看完全大小的图像](using-templatefields-in-the-detailsview-control-cs/_static/image12.png)）

由于这个新的 TemplateField 将包含 `UnitPrice`中当前显示的值、`UnitsInStock`和 `UnitsOnOrder` BoundFields，因此我们将其删除。

此步骤的最后一项任务是定义价格和库存 TemplateField 的 `ItemTemplate` 标记，可以通过设计器中的 DetailsView 模板编辑界面或通过控件的声明性语法来完成此操作。 与 GridView 一样，可以通过在智能标记中单击 "编辑模板" 链接来访问 DetailsView 的模板编辑界面。 从这里，您可以从下拉列表中选择要编辑的模板，然后从 "工具箱" 添加任何 Web 控件。

在本教程中，首先将 "标签" 控件添加到价格和库存 TemplateField 的 `ItemTemplate`。 接下来，单击标签 Web 控件的智能标记上的 "编辑 databinding" 链接，并将 `Text` 属性绑定到 `UnitPrice` 字段。

[![将标签的 "Text" 属性绑定到 "单价" 数据字段](using-templatefields-in-the-detailsview-control-cs/_static/image14.png)](using-templatefields-in-the-detailsview-control-cs/_static/image13.png)

**图 5**：将标签的 `Text` 属性绑定到 `UnitPrice` 数据字段（[单击查看完全大小的图像](using-templatefields-in-the-detailsview-control-cs/_static/image15.png)）

## <a name="formatting-the-price-as-a-currency"></a>将价格的格式设置为货币

通过此添加，标签 Web 控件价格和库存 TemplateField 现在只显示所选产品的价格。 图6显示了在浏览器中查看进度的屏幕截图。

[![价格和库存 TemplateField 显示价格](using-templatefields-in-the-detailsview-control-cs/_static/image17.png)](using-templatefields-in-the-detailsview-control-cs/_static/image16.png)

**图 6**：价格和库存 TemplateField 显示价格（[单击查看全尺寸图像](using-templatefields-in-the-detailsview-control-cs/_static/image18.png)）

请注意，产品的价格未设置为货币格式。 使用 BoundField，可以通过将 `HtmlEncode` 属性设置为 `false` 并将 `DataFormatString` 属性设置为 `{0:formatSpecifier}`来实现格式设置。 不过，对于 TemplateField，必须在数据绑定语法中或在应用程序代码中的某处定义格式设置方法（如 ASP.NET 页的代码隐藏类）中指定格式设置说明。

若要为 "标签 Web 控件" 中使用的数据绑定语法指定格式设置，请通过单击标签的智能标记中的 "编辑数据绑定" 链接返回到 "数据绑定" 对话框。 您可以直接在 "格式" 下拉列表中键入格式说明，或选择一个定义的格式字符串。 与 BoundField 的 `DataFormatString` 属性一样，格式设置是使用 `{0:formatSpecifier}`指定的。

对于 "`UnitPrice`" 字段，通过选择相应的下拉列表值或手动键入 `{0:C}` 来使用指定的货币格式。

[![将价格设置为货币格式](using-templatefields-in-the-detailsview-control-cs/_static/image20.png)](using-templatefields-in-the-detailsview-control-cs/_static/image19.png)

**图 7**：将价格设置为货币格式（[单击以查看完全大小的图像](using-templatefields-in-the-detailsview-control-cs/_static/image21.png)）

以声明方式，格式设置规范表示为 `Bind` 或 `Eval` 方法中的第二个参数。 刚刚通过设计器进行的设置会导致声明性标记中出现以下数据绑定表达式：

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>将其余数据字段添加到 TemplateField

此时，我们已在价格和库存 TemplateField 中显示并格式化了 `UnitPrice` 数据字段，但仍需要显示 `UnitsInStock` 和 `UnitsOnOrder` 字段。 让我们将它们显示在价格下、括号中。 从设计器中的模板编辑界面，可以通过将光标置于模板内并只键入要显示的文本来添加此类标记。 或者，可以直接在声明性语法中输入此标记。

添加静态标记、标签 Web 控件和数据绑定语法，以便价格和库存 TemplateField 显示价格和清单信息，如下所示：

*单价*  
（**按库存/按顺序：** 按*库存 / * *UnitsOnOrder*）

执行此任务后，DetailsView 的声明性标记应如下所示：

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample3.aspx)]

进行这些更改后，我们已将价格和清单信息合并到单个 DetailsView 行中。

[![价格和库存信息显示在单个行中](using-templatefields-in-the-detailsview-control-cs/_static/image23.png)](using-templatefields-in-the-detailsview-control-cs/_static/image22.png)

**图 8**：价格和库存信息显示在单个行中（[单击以查看完全大小的图像](using-templatefields-in-the-detailsview-control-cs/_static/image24.png)）

## <a name="step-3-customizing-the-discontinued-field-information"></a>步骤3：自定义废止的字段信息

`Products` 表的 `Discontinued` 列是一个位值，指示产品是否已停止使用。 将 DetailsView （或 GridView）绑定到数据源控件时，布尔值字段（如 `Discontinued`）实现为 CheckBoxFields，而非布尔值字段（如 `ProductID`、`ProductName`等）作为 BoundFields 实现。 CheckBoxField 呈现为已禁用的复选框，如果数据字段的值为 True 且未选中，则选中该复选框。

我们可能不想显示 CheckBoxField，而是显示指示产品是否中止的文本。 若要完成此操作，我们可以从 DetailsView 中删除 CheckBoxField，然后添加其 `DataField` 属性设置为 `Discontinued`的 BoundField。 请花点时间来完成此操作。 在此更改后，DetailsView 将为停用的产品显示文本 "True"，为仍处于活动状态的产品显示 "False"。

[![字符串 True 和 False 用于显示中止状态](using-templatefields-in-the-detailsview-control-cs/_static/image26.png)](using-templatefields-in-the-detailsview-control-cs/_static/image25.png)

**图 9**：字符串 True 和 False 用于显示中止状态（[单击查看完全大小的图像](using-templatefields-in-the-detailsview-control-cs/_static/image27.png)）

假设我们不想使用字符串 "True" 或 "False"，而是 "YES" 和 "NO"。 可以使用 TemplateField 和格式设置方法来执行此类自定义。 格式设置方法可以采用任意数量的输入参数，但必须返回 HTML （作为字符串）才能插入模板。

向名为 `DisplayDiscontinuedAsYESorNO` 的 `DetailsViewTemplateField.aspx` 页的代码隐藏类添加格式设置方法，该方法接受一个布尔值作为输入参数并返回一个字符串。 如前面的教程中所述，此方法*必须*标记为 `protected` 或 `public` 才能从模板进行访问。

[!code-csharp[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample4.cs)]

此方法检查输入参数（`discontinued`），如果 `true`，则返回 "YES"，否则返回 "NO"。

> [!NOTE]
> 在上一教程中检查的格式设置方法中，请记住，我们传入的数据字段可能包含 `NULL`，因此，在访问 `EmployeesRow`的 `HiredDate` 属性之前，需要检查员工的 `HiredDate` 属性值是否具有数据库 `NULL` 值。 此处不需要此类检查，因为 `Discontinued` 列永远不会分配数据库 `NULL` 值。 而且，这就是为什么此方法可以接受布尔输入参数，而不必接受 `ProductsRow` 实例或 `object`类型的参数。

此格式设置方法完成后，剩下的就是从 TemplateField 的 `ItemTemplate`调用它。 若要创建 TemplateField，请删除 `Discontinued` BoundField 并添加新的 TemplateField，或将 `Discontinued` BoundField 转换为 TemplateField。 然后，从声明性标记视图编辑 TemplateField，使其只包含调用 `DisplayDiscontinuedAsYESorNO` 方法的 ItemTemplate，并传入当前 `ProductRow` 实例的 `Discontinued` 属性的值。 可以通过 `Eval` 方法访问此。 具体而言，TemplateField 的标记应如下所示：

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample5.aspx)]

这将导致在呈现 DetailsView 时调用 `DisplayDiscontinuedAsYESorNO` 方法，并传入 `ProductRow` 实例的 `Discontinued` 值。 由于 `Eval` 方法返回 `object`类型的值，但 `DisplayDiscontinuedAsYESorNO` 方法需要 `bool`类型的输入参数，因此，我们将 `Eval` 方法返回值强制转换为 `bool`。 然后 `DisplayDiscontinuedAsYESorNO` 方法返回 "是" 或 "否"，具体取决于它接收的值。 返回的值是在此 DetailsView 行中显示的值（请参阅图10）。

[!["是" 或 "否" 值现在显示在 "已停止" 行中](using-templatefields-in-the-detailsview-control-cs/_static/image29.png)](using-templatefields-in-the-detailsview-control-cs/_static/image28.png)

**图 10**： "是" 或 "否" 值现在显示在 "停止行" 中（[单击以查看完全大小的图像](using-templatefields-in-the-detailsview-control-cs/_static/image30.png)）

## <a name="summary"></a>摘要

使用 DetailsView 控件中的 TemplateField，可以在显示数据时提供比其他字段控件更高的灵活性，这对于以下情况非常理想：

- 需要在一个 GridView 列中显示多个数据字段
- 使用 Web 控件而不是纯文本来最大程度地表示数据
- 输出取决于基础数据，如显示元数据或重新格式化数据

虽然 Templatefield 允许在呈现 DetailsView 的基础数据时获得更大的灵活性，但 DetailsView 输出仍认为有点 boxy，因为每个字段在 HTML `<table>`中呈现为一行。

在配置呈现的输出时，FormView 控件可提供更大的灵活性。 FormView 不包含字段，而只包含一系列模板（`ItemTemplate`、`EditItemTemplate`、`HeaderTemplate`，等等）。 我们将在下一教程中了解如何使用 FormView 来更好地控制呈现的布局。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的潜在客户审阅者为 Dan Jagers。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](using-templatefields-in-the-gridview-control-cs.md)
> [下一页](using-the-formview-s-templates-cs.md)
