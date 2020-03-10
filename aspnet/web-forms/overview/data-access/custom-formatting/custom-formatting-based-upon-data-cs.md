---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
title: 基于数据的自定义格式C#设置（） |Microsoft Docs
author: rick-anderson
description: 根据所绑定的数据，调整 GridView、DetailsView 或 FormView 的格式可以通过多种方式完成。 在本教程中，我们将 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 871a4574-f89c-4214-b786-79253ed3653b
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: d8f3fa337eda0ceed041475ecb52f8b378b9fbba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78442136"
---
# <a name="custom-formatting-based-upon-data-c"></a>基于数据的自定义格式设置 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_11_CS.exe)或[下载 PDF](custom-formatting-based-upon-data-cs/_static/datatutorial11cs1.pdf)

> 根据所绑定的数据，调整 GridView、DetailsView 或 FormView 的格式可以通过多种方式完成。 在本教程中，我们将介绍如何通过使用数据绑定和 RowDataBound 事件处理程序来完成数据绑定格式设置。

## <a name="introduction"></a>简介

可以通过多种与样式相关的属性来自定义 GridView、DetailsView 和 FormView 控件的外观。 例如 `CssClass`、`Font`、`BorderWidth`、`BorderStyle`、`BorderColor`、`Width`和 `Height`等属性将决定呈现的控件的一般外观。 包含 `HeaderStyle`、`RowStyle`、`AlternatingRowStyle`和其他属性的属性允许将这些相同的样式设置应用到特定的部分。 同样，可以在字段级别应用这些样式设置。

但在许多情况下，格式要求取决于所显示数据的值。 例如，若要对脱销产品引起注意，列出产品信息的报表可能会将其 "`UnitsInStock`" 和 "`UnitsOnOrder`" 字段都等于0的产品的背景色设置为黄色。 若要突出显示更昂贵的产品，我们可能希望将这些产品的价格按粗体字显示 $75.00。

根据所绑定的数据，调整 GridView、DetailsView 或 FormView 的格式可以通过多种方式完成。 在本教程中，我们将介绍如何通过使用 `DataBound` 和 `RowDataBound` 事件处理程序来实现数据绑定格式。 在下一教程中，我们将探讨一种替代方法。

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>使用 DetailsView 控件的`DataBound`事件处理程序

如果将数据从数据源控件绑定到 DetailsView，或通过编程方式将数据分配给控件的 `DataSource` 属性并调用其 `DataBind()` 方法，则将执行以下步骤：

1. 引发数据 Web 控件的 `DataBinding` 事件。
2. 数据绑定到数据 Web 控件。
3. 引发数据 Web 控件的 `DataBound` 事件。

在步骤1和3之后，可以通过事件处理程序立即注入自定义逻辑。 通过为 `DataBound` 事件创建事件处理程序，我们可以以编程方式确定已绑定到数据 Web 控件的数据，并根据需要调整格式。 为了说明这一点，我们将创建一个 DetailsView 来列出有关产品的一般信息，但会将 `UnitPrice` 值显示为***粗体、斜体（*** 如果它超过 $75.00）。

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>步骤1：在 DetailsView 中显示产品信息

打开 `CustomFormatting` 文件夹中的 "`CustomColors.aspx`" 页，将 "DetailsView" 控件从 "工具箱" 拖动到设计器上，将其 `ID` 属性值设置为 `ExpensiveProductsPriceInBoldItalic`，并将其绑定到调用 `ProductsBLL` 类的 `GetProducts()` 方法的新 ObjectDataSource 控件。 为了简洁起见，此处省略了用于完成此操作的详细步骤，因为我们在以前的教程中对它们进行了详细介绍。

将 ObjectDataSource 绑定到 DetailsView 后，请花点时间修改字段列表。 我已经选择删除 `ProductID`、`SupplierID`、`CategoryID`、`UnitsInStock`、`UnitsOnOrder`、`ReorderLevel`和 `Discontinued` BoundFields 并重命名并重新格式化剩余 BoundFields。 我还清除了 `Width` 和 `Height` 设置。 由于 DetailsView 只显示一条记录，因此我们需要启用分页以便使最终用户能够查看所有产品。 为此，请选中 DetailsView 的智能标记中的 "启用分页" 复选框。

[![选中 DetailsView 的智能标记中的 "启用分页" 复选框](custom-formatting-based-upon-data-cs/_static/image2.png)](custom-formatting-based-upon-data-cs/_static/image1.png)

**图 1**：选中 DetailsView 的智能标记中的 "启用分页" 复选框（[单击查看完全尺寸的图像](custom-formatting-based-upon-data-cs/_static/image3.png)）

进行这些更改后，DetailsView 标记将为：

[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample1.aspx)]

请花点时间在浏览器中测试此页。

[![DetailsView 控件一次显示一个产品](custom-formatting-based-upon-data-cs/_static/image5.png)](custom-formatting-based-upon-data-cs/_static/image4.png)

**图 2**： DetailsView 控件一次显示一个产品（[单击查看完全尺寸的图像](custom-formatting-based-upon-data-cs/_static/image6.png)）

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>步骤2：以编程方式确定数据绑定事件处理程序中数据的值

为了以粗体、斜体字体显示 `UnitPrice` 值超过 $75.00 的产品，我们首先需要能够以编程方式确定 `UnitPrice` 值。 对于 DetailsView，可以在 `DataBound` 事件处理程序中完成此操作。 若要创建事件处理程序，请在设计器中单击 DetailsView，然后导航到属性窗口。 按 F4 显示它（如果它不可见），或转到 "视图" 菜单并选择 "属性" 窗口菜单选项。 在属性窗口中，单击闪电形图标以列出 DetailsView 的事件。 接下来，双击 `DataBound` 事件，或键入要创建的事件处理程序的名称。

![为数据绑定事件创建事件处理程序](custom-formatting-based-upon-data-cs/_static/image7.png)

**图 3**：为 `DataBound` 事件创建事件处理程序

这样做会自动创建事件处理程序，并将你转到添加了该处理程序的代码部分。 此时，你将看到：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample2.cs)]

可以通过 `DataItem` 属性访问绑定到 DetailsView 的数据。 回忆一下，我们将控件绑定到强类型的 DataTable，后者由强类型化的 DataRow 实例的集合组成。 当 DataTable 绑定到 DetailsView 时，DataTable 中的第一个 DataRow 将分配给 DetailsView 的 `DataItem` 属性。 具体而言，为 `DataItem` 属性分配了 `DataRowView` 对象。 可以使用 `DataRowView`的 `Row` 属性访问基础 DataRow 对象，这实际上是一个 `ProductsRow` 的实例。 获得此 `ProductsRow` 实例后，只需检查对象的属性值就可以做出决定。

下面的代码演示如何确定绑定到 DetailsView 控件的 `UnitPrice` 值是否大于 $75.00：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample3.cs)]

> [!NOTE]
> 由于 `UnitPrice` 可以在数据库中具有 `NULL` 值，因此我们首先检查以确保在访问 `ProductsRow`的 `UnitPrice` 属性之前不处理 `NULL` 值。 这项检查非常重要，因为如果我们尝试在具有 `NULL` 值时访问 `UnitPrice` 属性，则 `ProductsRow` 对象将引发[StrongTypingException 异常](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)。

## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>步骤3：格式化 DetailsView 中的 "单价" 值

此时，我们可以确定绑定到 DetailsView 的 `UnitPrice` 值是否有超过 $75.00 的值，但我们还会了解如何以编程方式适当地调整 DetailsView 的格式。 若要修改 DetailsView 中整行的格式，请使用 `DetailsViewID.Rows[index]`以编程方式访问该行;为了修改特定单元，access 使用 `DetailsViewID.Rows[index].Cells[index]`。 引用行或单元后，可以通过设置其样式相关属性来调整其外观。

以编程方式访问行要求您知道行的索引（从0开始）。 `UnitPrice` 行是 DetailsView 的第五行，为它提供4的索引，并使其能够使用 `ExpensiveProductsPriceInBoldItalic.Rows[4]`以编程方式进行访问。 此时，我们可以使用以下代码以粗体、斜体字体显示整行的内容：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample4.cs)]

但是，这会使标签（价格）和值*均*为粗体和斜体。 如果我们想要使值为粗体和斜体，则需要将此格式应用于行中的第二个单元格，这可以通过以下方式来完成：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample5.cs)]

由于我们的教程目前使用了样式表来维护呈现的标记和样式相关信息之间的完全分离，因此，我们改为使用 CSS 类，而不是设置特定的样式属性（如上所示）。 打开 `Styles.css` 样式表，并使用以下定义添加名为 `ExpensivePriceEmphasis` 的新 CSS 类：

[!code-css[Main](custom-formatting-based-upon-data-cs/samples/sample6.css)]

然后，在 `DataBound` 事件处理程序中，将单元格的 `CssClass` 属性设置为 "`ExpensivePriceEmphasis`"。 下面的代码演示了完整的 `DataBound` 事件处理程序：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample7.cs)]

查看低于 $75.00 的 Chai 时，价格以普通字体显示（见图4）。 但是，当查看价格为 $97.00 的 Mishi Kobe Niku 时，价格将以粗体、斜体字体显示（见图5）。

[小于 $75.00 的 ![价格以普通字体显示](custom-formatting-based-upon-data-cs/_static/image9.png)](custom-formatting-based-upon-data-cs/_static/image8.png)

**图 4**：以普通字体显示小于 $75.00 的价格（[单击以查看完全大小的图像](custom-formatting-based-upon-data-cs/_static/image10.png)）

[![昂贵的产品价格以粗体、斜体字体显示](custom-formatting-based-upon-data-cs/_static/image12.png)](custom-formatting-based-upon-data-cs/_static/image11.png)

**图 5**：开销较高的产品价格以粗体、斜体字体显示（[单击以查看完全大小的图像](custom-formatting-based-upon-data-cs/_static/image13.png)）

## <a name="using-the-formview-controlsdataboundevent-handler"></a>使用 FormView 控件的`DataBound`事件处理程序

确定绑定到 FormView 的基础数据的步骤与针对 DetailsView 创建 `DataBound` 事件处理程序的步骤相同，将 `DataItem` 属性强制转换为绑定到控件的适当对象类型，并确定如何继续。 不过，FormView 和 DetailsView 在如何更新其用户界面的外观上有所不同。

FormView 不包含任何 BoundFields，因此缺少 `Rows` 的集合。 取而代之的是，FormView 由模板组成，模板可以包含静态 HTML、Web 控件和数据绑定语法的混合。 调整 FormView 样式通常涉及调整 FormView 的模板中的一个或多个 Web 控件的样式。

为了说明这一点，让我们使用 FormView 来列出如上例中所示的产品，但这一次，我们将只显示产品名称和库存单位，并以红色字体显示股票，如果其小于或等于10。

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>步骤4：在 FormView 中显示产品信息

将 FormView 添加到 DetailsView 下的 `CustomColors.aspx` 页面，并将其 `ID` 属性设置为 "`LowStockedProductsInRed`"。 将 FormView 绑定到从上一步创建的 ObjectDataSource 控件。 这将创建 FormView 的 `ItemTemplate`、`EditItemTemplate`和 `InsertItemTemplate`。 删除 `EditItemTemplate`，并 `InsertItemTemplate` 并简化 `ItemTemplate`，使其只包含 `ProductName` 值和 `UnitsInStock` 值，每个值都在其自己的适当命名的标签控件中。 与前面示例中的 DetailsView 一样，还请选中 FormView 的智能标记中的 "启用分页" 复选框。

编辑 FormView 标记后，应如下所示：

[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample8.aspx)]

请注意，`ItemTemplate` 包含：

- **静态 HTML**文本 "Product：" 和 "Stock In Units：" 以及 `<br />` 和 `<b>` 元素。
- **Web 控制**两个标签控件，`ProductNameLabel` 和 `UnitsInStockLabel`。
- **数据绑定语法**`<%# Bind("ProductName") %>` 和 `<%# Bind("UnitsInStock") %>` 语法，它将这些字段中的值赋值给标签控件的 `Text` 属性。

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>步骤5：以编程方式确定数据绑定事件处理程序中数据的值

完成 FormView 标记后，下一步是以编程方式确定 `UnitsInStock` 值是否小于或等于10。 完成此操作的方式与 FormView 完全相同。 首先为 FormView 的 `DataBound` 事件创建事件处理程序。

![创建数据绑定事件处理程序](custom-formatting-based-upon-data-cs/_static/image14.png)

**图 6**：创建 `DataBound` 事件处理程序

在事件处理程序中，将 FormView 的 `DataItem` 属性强制转换为 `ProductsRow` 实例，并确定 `UnitsInPrice` 值是否为需要以红色字体显示。

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample9.cs)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>步骤6：设置 FormView 的 ItemTemplate 中的 UnitsInStockLabel 标签控件的格式

最后一步是将显示的 `UnitsInStock` 值设置为红色字体（如果值为10或更小）。 若要实现此目的，我们需要以编程方式访问 `ItemTemplate` 中的 `UnitsInStockLabel` 控件并设置其样式属性，使其文本显示为红色。 若要访问模板中的 Web 控件，请使用如下所示的 `FindControl("controlID")` 方法：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample10.cs)]

对于我们的示例，我们想要访问 `ID` 值为 `UnitsInStockLabel`的 "标签" 控件，因此，我们将使用：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample11.cs)]

有了对 Web 控件的编程引用后，就可以根据需要修改与样式相关的属性。 与前面的示例一样，我已在名为 `LowUnitsInStockEmphasis`的 `Styles.css` 中创建了一个 CSS 类。 若要将此样式应用于标签 Web 控件，请相应地设置其 `CssClass` 属性。

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample12.cs)]

> [!NOTE]
> 使用 `FindControl("controlID")`，并在 DetailsView 或 GridView 控件中使用[templatefield](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx)时，还可以使用对模板进行格式设置的语法以编程方式访问 Web 控件。 我们将在下一教程中检查 Templatefield。

图7显示了在查看其 `UnitsInStock` 值大于10的产品时进行的 FormView，而图8中的产品的值小于10。

[![适用于库存量足够大的产品，不应用自定义格式设置](custom-formatting-based-upon-data-cs/_static/image16.png)](custom-formatting-based-upon-data-cs/_static/image15.png)

**图 7**：对于库存量足够大的产品，不应用自定义格式设置（[单击查看完全尺寸的图像](custom-formatting-based-upon-data-cs/_static/image17.png)）

[对于值为10或更小的产品，![库存数量中的单位显示为红色](custom-formatting-based-upon-data-cs/_static/image19.png)](custom-formatting-based-upon-data-cs/_static/image18.png)

**图 8**：对于值为10或更少的产品，库存编号的单位显示为红色（[单击查看全尺寸图像](custom-formatting-based-upon-data-cs/_static/image20.png)）

## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>设置 GridView`RowDataBound`事件的格式

以前，我们在数据绑定过程中检查了 DetailsView 和 FormView 控制进度的步骤顺序。 接下来，让我们再次看一遍这些步骤。

1. 引发数据 Web 控件的 `DataBinding` 事件。
2. 数据绑定到数据 Web 控件。
3. 引发数据 Web 控件的 `DataBound` 事件。

这三个简单步骤都足以应对 DetailsView 和 FormView，因为这三个步骤只显示单个记录。 对于 GridView，其中显示绑定到它的*所有*记录（而不仅仅是第一个），步骤2也更多。

在步骤2中，GridView 枚举数据源，并为每个记录创建一个 `GridViewRow` 实例，并将当前记录绑定到该实例。 对于添加到 GridView 的每个 `GridViewRow`，都将引发两个事件：

- 在创建 `GridViewRow` 之后 **`RowCreated`** 激发
- 当前记录绑定到 `GridViewRow`后， **`RowDataBound`** 触发。

对于 GridView，数据绑定可以通过以下一系列步骤进行更准确地描述：

1. 激发 GridView 的 `DataBinding` 事件。
2. 数据绑定到 GridView。   
  
   对于数据源中的每个记录 

    1. 创建 `GridViewRow` 对象
    2. 激发 `RowCreated` 事件
    3. 将记录绑定到 `GridViewRow`
    4. 激发 `RowDataBound` 事件
    5. 将 `GridViewRow` 添加到 `Rows` 集合
3. 激发 GridView 的 `DataBound` 事件。

若要自定义 GridView 的单个记录的格式，则需要为 `RowDataBound` 事件创建事件处理程序。 为了说明这一点，让我们将一个 GridView 添加到 "`CustomColors.aspx`" 页面，该页面列出了每个产品的名称、类别和价格，突出显示价格低于 $10.00 的产品，黄色背景颜色为黄色。

## <a name="step-7-displaying-product-information-in-a-gridview"></a>步骤7：在 GridView 中显示产品信息

在上一示例中的 FormView 下添加一个 GridView，并将其 `ID` 属性设置为 `HighlightCheapProducts`。 由于我们已有一个返回页面上所有产品的 ObjectDataSource，因此请将 GridView 绑定到该。 最后，编辑 GridView 的 BoundFields，以只包含产品的名称、类别和价格。 完成这些编辑后，GridView 的标记应如下所示：

[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample13.aspx)]

图9显示了通过浏览器查看此点的进度。

[![GridView 列出了每个产品的名称、类别和价格](custom-formatting-based-upon-data-cs/_static/image22.png)](custom-formatting-based-upon-data-cs/_static/image21.png)

**图 9**： GridView 列出了每个产品的名称、类别和价格（[单击查看完全尺寸的图像](custom-formatting-based-upon-data-cs/_static/image23.png)）

## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>步骤8：以编程方式确定 RowDataBound 事件处理程序中的数据值

将 `ProductsDataTable` 绑定到 GridView 时，会枚举其 `ProductsRow` 实例，并为每个 `ProductsRow` 创建 `GridViewRow`。 `GridViewRow`的 `DataItem` 属性分配给特定 `ProductRow`，之后将引发 GridView 的 `RowDataBound` 事件处理程序。 若要确定绑定到 GridView 的每个产品的 `UnitPrice` 值，则需要为 GridView 的 `RowDataBound` 事件创建事件处理程序。 在此事件处理程序中，我们可以检查当前 `GridViewRow` 的 `UnitPrice` 值并对该行进行格式决策。

此事件处理程序可以使用与 FormView 和 DetailsView 相同的步骤来创建。

![为 GridView 的 RowDataBound 事件创建事件处理程序](custom-formatting-based-upon-data-cs/_static/image24.png)

**图 10**：为 GridView 的 `RowDataBound` 事件创建事件处理程序

以这种方式创建事件处理程序将导致以下代码自动添加到 ASP.NET 页的代码部分：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample14.cs)]

当引发 `RowDataBound` 事件时，事件处理程序将作为其第二个参数 `GridViewRowEventArgs`类型的对象（该对象具有名为 `Row`的属性）。 此属性返回对只是数据绑定的 `GridViewRow` 的引用。 若要访问绑定到 `GridViewRow` 的 `ProductsRow` 实例，我们使用 `DataItem` 属性，如下所示：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample15.cs)]

使用 `RowDataBound` 事件处理程序时，请务必记住，GridView 由不同类型的行组成，并为*所有*行类型激发此事件。 `GridViewRow`的类型可由其 `RowType` 属性确定，并且可以有一个可能值：

- `DataRow` 绑定到 GridView `DataSource` 中的记录的行
- `EmptyDataRow` GridView `DataSource` 为空时所显示的行
- `Footer` 页脚行;如果 GridView 的 `ShowFooter` 属性设置为，则显示该属性 `true`
- `Header` 标题行;如果 GridView 的 ShowHeader 属性设置为 `true` （默认值），则显示此值
- 用于实现分页的 GridView 的 `Pager`，显示分页接口的行
- `Separator` 不用于 GridView，但用于 DataList 和 Repeater 控件的 `RowType` 属性，我们将在以后的教程中讨论两个数据 Web 控件

由于 `EmptyDataRow`、`Header`、`Footer`和 `Pager` 行并不与 `DataSource` 记录相关联，因此它们的 `null` 属性始终具有 `DataItem` 值。 出于此原因，在尝试使用当前 `GridViewRow`的 `DataItem` 属性之前，必须先确保我们正在处理 `DataRow`。 为此，可以检查 `GridViewRow`的 `RowType` 属性，如下所示：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample16.cs)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>步骤9：在 "单价" 值小于 $10.00 时突出显示行黄色

最后一个步骤是，如果该行的 `UnitPrice` 值小于 $10.00，则以编程方式突出显示整个 `GridViewRow`。 用于访问 GridView 的行或单元格的语法与用于访问整行 `GridViewID.Rows[index]` `GridViewID.Rows[index].Cells[index]` 访问特定单元格的语法相同。 但是，当 `RowDataBound` 事件处理程序触发了数据绑定 `GridViewRow`，而该数据绑定尚未添加到 GridView 的 `Rows` 集合中。 因此，不能使用 Rows 集合从 `RowDataBound` 事件处理程序访问当前 `GridViewRow` 实例。

我们可以使用 `e.Row`引用 `RowDataBound` 事件处理程序中的当前 `GridViewRow` 实例，而不是 `GridViewID.Rows[index]`。 也就是说，若要突出显示当前 `GridViewRow` 实例，请使用 `RowDataBound` 事件处理程序：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample17.cs)]

无需直接设置 `GridViewRow`的 `BackColor` 属性，只需使用 CSS 类即可。 我创建了一个名为 `AffordablePriceEmphasis` 的 CSS 类，它将背景色设置为黄色。 完成的 `RowDataBound` 事件处理程序如下所示：

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample18.cs)]

[![最经济实惠的产品将突出显示为黄色](custom-formatting-based-upon-data-cs/_static/image26.png)](custom-formatting-based-upon-data-cs/_static/image25.png)

**图 11**：最经济实惠的产品突出显示为黄色（[单击以查看完全大小的图像](custom-formatting-based-upon-data-cs/_static/image27.png)）

## <a name="summary"></a>摘要

在本教程中，我们了解了如何根据绑定到控件的数据设置 GridView、DetailsView 和 FormView 的格式。 为实现此目的，我们为 `DataBound` 或 `RowDataBound` 事件创建了一个事件处理程序，如果需要，将根据格式更改对基础数据进行检查。 若要访问已绑定到 DetailsView 或 FormView 的数据，请使用 `DataBound` 事件处理程序中的 `DataItem` 属性;对于 GridView，每个 `GridViewRow` 实例的 `DataItem` 属性都包含绑定到该行的数据，`RowDataBound` 事件处理程序中提供该数据。

用于以编程方式调整数据 Web 控件的格式的语法取决于 Web 控件和如何显示要设置格式的数据。 对于 DetailsView 和 GridView 控件，可以通过序号索引访问行和单元格。 对于使用模板的 FormView，`FindControl("controlID")` 方法通常用于从模板中查找 Web 控件。

在下一教程中，我们将介绍如何将模板与 GridView 和 DetailsView 一起使用。 此外，我们还会看到另一种基于基础数据自定义格式设置的方法。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 E.R。 Gilmore、Dennis Patterson 将和 Dan Jagers。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一部分](using-templatefields-in-the-gridview-control-cs.md)
