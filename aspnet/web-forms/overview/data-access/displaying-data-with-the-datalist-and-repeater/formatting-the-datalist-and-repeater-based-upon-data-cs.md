---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
title: 基于数据设置 DataList 和 Repeater 的格式（C#） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将逐步介绍如何设置 DataList 和 Repeater 控件的外观格式的示例，方法是使用格式设置函数和 。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 83e3d759-82b8-41e6-8d62-f0f4b3edec41
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 68de3450ed97fc7bd0efb27e089d9db8e3e85fb0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633286"
---
# <a name="formatting-the-datalist-and-repeater-based-upon-data-c"></a>基于数据设置 DataList 和 Repeater 的格式 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_30_CS.exe)或[下载 PDF](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/datatutorial30cs1.pdf)

> 在本教程中，我们将逐步介绍如何设置 DataList 和 Repeater 控件的外观格式，方法是使用模板中的格式设置函数或处理数据绑定事件。

## <a name="introduction"></a>简介

如前面的教程中所述，DataList 提供了许多与样式相关的属性，这些属性会影响其外观。 具体而言，我们已了解如何向 DataList s 分配默认的 CSS 类 `HeaderStyle`、`ItemStyle`、`AlternatingItemStyle`和 `SelectedItemStyle` 属性。 除了这四个属性，DataList 还包含许多其他样式相关的属性，例如 `Font`、`ForeColor`、`BackColor`和 `BorderWidth`等。 Repeater 控件不包含任何与样式相关的属性。 任何此类样式设置都必须直接在 Repeater 模板的标记中进行。

通常，如何设置数据的格式取决于数据本身。 例如，在列出产品时，如果产品信息已停用，我们可能希望以浅灰色的字体颜色显示产品信息，或者，如果此值为零，则可能想要突出显示 `UnitsInStock` 值。 如前面的教程中所述，GridView、DetailsView 和 FormView 提供了两种不同的方法来根据数据的数据设置其外观：

- **`DataBound` 事件**为相应的 `DataBound` 事件创建事件处理程序，该事件处理程序在数据绑定到每一项后触发（对于 GridView，它是 `RowDataBound` 事件; 对于 DataList 和中继器，它是 `ItemDataBound` 事件）。 在该事件处理程序中，可以检查刚刚绑定的数据，并做出格式决策。 我们[基于数据教程在自定义格式设置](../custom-formatting/custom-formatting-based-upon-data-cs.md)中检查了此方法。
- 在 DetailsView 或 GridView 控件中使用 Templatefield 或使用 FormView 控件中的模板时，**模板中的格式设置**函数可以将格式设置函数添加到 ASP.NET 页的代码隐藏类、业务逻辑层或可从 web 应用程序访问的任何其他类库。 此格式设置函数可以接受任意数量的输入参数，但必须返回要在模板中呈现的 HTML。 首次[使用 GridView 控件](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)教程中的 templatefield 检查格式设置函数。

这两种格式设置方法均可用于 DataList 和 Repeater 控件。 在本教程中，我们将逐步介绍如何对这两个控件使用这两种方法。

## <a name="using-theitemdataboundevent-handler"></a>使用`ItemDataBound`事件处理程序

当数据绑定到 DataList 时，无论是通过数据源控件还是以编程方式将数据分配给控件的 `DataSource` 属性并调用其 `DataBind()` 方法，会触发 DataList s `DataBinding` 事件，枚举的数据源，每个数据记录都绑定到 DataList。 对于数据源中的每个记录，DataList 创建一个[`DataListItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.aspx)对象，然后将其绑定到当前记录。 在此过程中，DataList 将引发两个事件：

- 在创建 `DataListItem` 之后 **`ItemCreated`** 激发
- 当前记录绑定到 `DataListItem` 之后 **`ItemDataBound`** 激发

以下步骤概述了 DataList 控件的数据绑定过程。

1. 引发 DataList s [`DataBinding` 事件](https://msdn.microsoft.com/library/system.web.ui.control.databinding.aspx)
2. 数据绑定到 DataList  
  
   对于数据源中的每个记录 

    1. 创建 `DataListItem` 对象
    2. 激发[`ItemCreated` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemcreated.aspx)
    3. 将记录绑定到 `DataListItem`
    4. 激发[`ItemDataBound` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemdatabound.aspx)
    5. 将 `DataListItem` 添加到 `Items` 集合

在将数据绑定到 Repeater 控件时，它会经历完全相同的步骤顺序。 唯一的区别是，中继器使用[`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem(VS.80).aspx)，而不是创建 `DataListItem` 实例。

> [!NOTE]
> 敏锐读取器可能已注意到，当 DataList 和 Repeater 绑定到数据时，以及 GridView 绑定到数据时所发生的一系列步骤之间发生了略微异常。 在数据绑定过程的结尾处，GridView 引发 `DataBound` 事件;但是，DataList 和 Repeater 控件都没有此类事件。 这是因为 DataList 和 Repeater 控件是在 ASP.NET 1.x 时间范围内创建的，并且在前期和后期级别事件处理程序模式变得很常见之前。

与 GridView 一样，根据数据进行格式设置的一个选项是为 `ItemDataBound` 事件创建事件处理程序。 此事件处理程序将检查刚刚绑定到 `DataListItem` 或 `RepeaterItem` 的数据，并根据需要影响该控件的格式设置。

对于 DataList 控件，可以使用与 `DataListItem` 的样式相关的属性来实现整个项的格式更改，其中包括标准 `Font`、`ForeColor`、`BackColor`、`CssClass`等。 若要影响 DataList s 模板中特定 Web 控件的格式设置，需要以编程方式访问和修改这些 Web 控件的样式。 我们已经了解了如何*基于数据*教程来完成此操作。 与 Repeater 控件一样，`RepeaterItem` 类没有与样式相关的属性;因此，必须通过编程方式访问和更新模板中的 Web 控件，对 `ItemDataBound` 事件处理程序中的 `RepeaterItem` 所做的所有与样式相关的更改。

由于 DataList 和 Repeater `ItemDataBound` 的格式设置方法几乎完全相同，因此我们的示例将重点介绍如何使用 DataList。

## <a name="step-1-displaying-product-information-in-the-datalist"></a>步骤1：在 DataList 中显示产品信息

在对格式进行担忧之前，先创建一个使用 DataList 显示产品信息的页面。 在[上一教程](displaying-data-with-the-datalist-and-repeater-controls-cs.md)中，我们创建了一个 DataList，其 `ItemTemplate` 显示每个产品的名称、类别、供应商、每个单位的数量和价格。 在本教程中，让我们重复此功能。 若要实现此目的，可以从头开始重新创建 DataList 及其 ObjectDataSource，也可以从上一教程中创建的页面（`Basics.aspx`）复制这些控件，并将其粘贴到本教程的页面（`Formatting.aspx`）。

将 DataList 和 ObjectDataSource 功能从 `Basics.aspx` 复制到 `Formatting.aspx`中后，请花点时间将 DataList s `ID` 属性从 `DataList1` 更改为更具描述性的 `ItemDataBoundFormattingExample`。 接下来，在浏览器中查看 DataList。 如图1所示，每个产品之间唯一的格式设置差别在于背景色是备用的。

[!["DataList" 控件中列出的产品](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image2.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image1.png)

**图 1**： "DataList" 控件中列出了产品（[单击以查看完全大小的图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image3.png)）

对于本教程，让我们设置 DataList 的格式，以便价格低于 $20.00 的任何产品都将其名称和单价突出显示为黄色。

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-itemdatabound-event-handler"></a>步骤2：以编程方式确定 ItemDataBound 事件处理程序中的数据值

由于只有价格低于 $20.00 的产品会应用自定义格式，因此我们必须能够确定每种产品的价格。 在将数据绑定到 DataList 时，DataList 将枚举其数据源中的记录，并为每个记录创建一个 `DataListItem` 实例，将数据源记录绑定到 `DataListItem`。 将特定记录的数据绑定到当前 `DataListItem` 对象之后，将触发 DataList s `ItemDataBound` 事件。 我们可以为此事件创建事件处理程序，以检查当前 `DataListItem` 的数据值，并根据这些值进行任何格式更改。

为 DataList 创建 `ItemDataBound` 事件，并添加以下代码：

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample1.cs)]

尽管 DataList `ItemDataBound` 事件处理程序背后的概念和语义与*基于数据教程的自定义格式设置*中的 GridView `RowDataBound` 事件处理程序所使用的概念和语义相同，但语法略有不同。 当 `ItemDataBound` 事件触发时，绑定到数据的 `DataListItem` 将通过 `e.Item` （而不是 `e.Row`，与 GridView `RowDataBound` 事件处理程序）传递到相应的事件处理程序中。 对于添加到 DataList 的*每个*行（包括标题行、行尾行和分隔符行），将激发 datalist `ItemDataBound` 事件处理程序。 但是，产品信息仅绑定到数据行。 因此，在使用 `ItemDataBound` 事件检查绑定到 DataList 的数据时，我们需要首先确保我们使用数据项。 这可以通过检查 `DataListItem` s [`ItemType` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.itemtype.aspx)来完成，该属性可以具有[以下8个值](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listitemtype.aspx)之一：

- `AlternatingItem`
- `EditItem`
- `Footer`
- `Header`
- `Item`
- `Pager`
- `SelectedItem`
- `Separator`

`Item` 和 `AlternatingItem``DataListItem` 均构成 DataList 的数据项。 假设我们要使用 `Item` 或 `AlternatingItem`，则可以访问已绑定到当前 `DataListItem`的实际 `ProductsRow` 的实例。 `DataListItem` s [`DataItem` 属性](https://msdn.microsoft.com/system.web.ui.webcontrols.datalistitem.dataitem.aspx)包含对 `DataRowView` 对象的引用，该对象的 `Row` 属性提供对实际 `ProductsRow` 对象的引用。

接下来，检查 `ProductsRow` 实例的 `UnitPrice` 属性。 由于 Products 表的 `UnitPrice` 字段允许 `NULL` 值，因此在尝试访问 `UnitPrice` 属性之前，首先应查看它是否具有使用 `IsUnitPriceNull()` 方法的 `NULL` 值。 如果未 `NULL``UnitPrice` 值，我们会检查它是否小于 $20.00。 如果它确实低于 $20.00，则需要应用自定义格式设置。

## <a name="step-3-highlighting-the-product-s-name-and-price"></a>步骤3：突出显示产品的名称和价格

知道产品价格低于 $20.00 后，剩下的就是强调其名称和价格。 若要实现此目的，必须先以编程方式引用 `ItemTemplate` 中显示产品的名称和价格的 "标签" 控件。 接下来，需要使它们显示黄色背景。 此格式设置信息可通过直接修改 `BackColor` 属性（`LabelID.BackColor = Color.Yellow`）的标签来应用;不过，理想情况下，所有与显示相关的问题都应该通过级联样式表来表示。 事实上，我们已经有了一个样式表，它提供了 `Styles.css` - `AffordablePriceEmphasis`中定义的所需格式，该格式已在*基于数据的自定义格式设置*教程中创建和讨论。

若要应用格式设置，只需将两个标签 Web 控件 `CssClass` 属性设置为 `AffordablePriceEmphasis`，如下面的代码所示：

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample2.cs)]

完成 `ItemDataBound` 事件处理程序后，请在浏览器中重新访问 `Formatting.aspx` 页面。 如图2所示，价格低于 $20.00 的产品会突出显示其名称和价格。

[![突出显示小于 $20.00 的产品](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image5.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image4.png)

**图 2**：突出显示小于 $20.00 的产品（[单击以查看完全大小的图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image6.png)）

> [!NOTE]
> 由于 DataList 呈现为 HTML `<table>`，因此其 `DataListItem` 实例具有与样式相关的属性，这些属性可设置为将特定样式应用于整个项。 例如，如果要在其价格低于 $20.00 时突出显示*整个*项黄色，则可以使用以下代码行替换引用标签的代码，并设置其 `CssClass` 属性： `e.Item.CssClass = "AffordablePriceEmphasis"` （请参阅图3）。

构成 Repeater 控件的 `RepeaterItem`，但不提供此类样式级属性。 因此，将自定义格式应用于中继器需要将样式属性应用到 Repeater 模板内的 Web 控件，就像我们在图2中所做的一样。

[![在 $20.00 下突出显示产品的整个产品项](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image8.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image7.png)

**图 3**：在 $20.00 下突出显示产品的整个产品项（[单击以查看完全大小的图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image9.png)）

## <a name="using-formatting-functions-from-within-the-template"></a>在模板中使用格式设置函数

在 GridView 控件教程中的 "*使用 templatefield* " 教程中，我们看到了如何使用 gridview TemplateField 内的格式设置函数根据绑定到 GridView 行的数据应用自定义格式设置。 格式设置函数是一种方法，可从模板调用，并返回要在其位置发出的 HTML。 格式设置函数可以位于 ASP.NET 页 s 代码隐藏类中，也可以集中到 `App_Code` 文件夹或单独类库项目中的类文件中。 如果你计划在多个 ASP.NET 页面或其他 ASP.NET web 应用程序中使用相同的格式设置功能，则将格式设置函数移出 ASP.NET 页的代码隐藏类是理想之选。

若要演示格式设置功能，请在产品名为 "已停用" 时让 s 中的文本 [已停用]。 此外，如果小于 $20.00，则将价格突出显示为黄色（如我们在 `ItemDataBound` 事件处理程序示例中所做的那样）;如果价格为 $20.00 或更高，则让我们不显示实际价格，而是改为使用价格报价。 图4显示了应用这些格式设置规则的产品列表的屏幕截图。

[![成本高昂的产品，则会将价格替换为文本，请拨打价格报价](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image11.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image10.png)

**图 4**：对于昂贵的产品，价格将替换为文本，请拨打价格报价（[单击查看全尺寸图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image12.png)）

## <a name="step-1-create-the-formatting-functions"></a>步骤1：创建格式设置函数

在此示例中，我们需要两个格式设置功能，一个用于显示产品名称以及文本 [已停用]，如有需要，另一个显示突出显示的价格（如果小于 $20.00）或文本，请拨打价格报价。 让我们在 ASP.NET 页 s 代码隐藏类中创建这些函数，并将它们命名为 `DisplayProductNameAndDiscontinuedStatus` 和 `DisplayPrice`。 这两种方法都需要以字符串的形式返回要呈现的 HTML，并且两者都需要标记 `Protected` （或 `Public`），以便从 ASP.NET 页的声明性语法部分进行调用。 以下两种方法的代码如下所示：

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample3.cs)]

请注意，`DisplayProductNameAndDiscontinuedStatus` 方法接受 `productName` 的值并将数据字段作为标量值 `discontinued`，而 `DisplayPrice` 方法接受 `ProductsRow` 的实例（而不是标量值）。 这两种方法都可行;但是，如果格式设置函数使用的标量值可以包含数据库 `NULL` 值（如 `UnitPrice`，则 `ProductName` 和 `Discontinued` 都不允许 `NULL` 值），则在处理这些标量输入时必须特别小心。

特别是，输入参数的类型必须为 `Object`，因为传入的值可能是 `DBNull` 实例，而不是预期的数据类型。 此外，必须进行检查以确定传入的值是否为数据库 `NULL` 值。 也就是说，如果我们希望 `DisplayPrice` 方法接受作为标量值的价格，则需要使用以下代码：

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample4.cs)]

请注意，`unitPrice` 输入参数的类型为 `Object`，并且已修改条件语句以确定是否 `DBNull` `unitPrice`。 此外，由于 `unitPrice` 输入参数作为 `Object`传入，因此必须将其强制转换为十进制值。

## <a name="step-2-calling-the-formatting-function-from-the-datalist-s-itemtemplate"></a>步骤2：从 DataList s ItemTemplate 调用格式设置函数

在 ASP.NET 页的代码隐藏类中添加格式设置函数后，剩下的就是从 DataList `ItemTemplate`调用这些格式设置函数。 若要从模板调用格式设置函数，请将函数调用置于 databinding 语法中：

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample5.aspx)]

在 DataList 中 `ItemTemplate` `ProductNameLabel` "标签 Web 控件" 当前显示产品名称，方法是将 `<%# Eval("ProductName") %>`的结果分配给其 `Text` 属性。 为了使它显示名称和文本 [已停用]，如果需要，请更新声明性语法，使其改为将 `Text` 属性分配 `DisplayProductNameAndDiscontinuedStatus` 方法的值。 执行此操作时，必须使用 `Eval("columnName")` 语法传入 product s name 和废止值。 `Eval` 返回 `Object`类型的值，但 `DisplayProductNameAndDiscontinuedStatus` 方法需要类型 `String` 和 `Boolean`的输入参数。因此，必须将 `Eval` 方法返回的值强制转换为所需的输入参数类型，如下所示：

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample6.aspx)]

为了显示价格，只需将 `UnitPriceLabel` 标签的 `Text` 属性设置为 `DisplayPrice` 方法返回的值，就像我们为显示产品名称和 [废止] 文本所做的那样。 但是，我们改为传入整个 `ProductsRow` 实例，而不是作为标量输入参数传入 `UnitPrice`：

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample7.aspx)]

在就地调用格式设置函数后，请花点时间在浏览器中查看进度。 您的屏幕应类似于图5，其中包含文本 [已停用的产品]，而那些产品的价格超过 $20.00，但其价格已替换为文本。

[![成本高昂的产品，则会将价格替换为文本，请拨打价格报价](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image14.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image13.png)

**图 5**：对于昂贵的产品，价格将替换为文本，请拨打价格报价（[单击查看全尺寸图像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image15.png)）

## <a name="summary"></a>总结

可以使用两种方法来基于数据设置 DataList 或 Repeater 控件的内容的格式。 第一种方法是为 `ItemDataBound` 事件创建事件处理程序，当数据源中的每条记录绑定到新的 `DataListItem` 或 `RepeaterItem`时，将触发该事件处理程序。 在 `ItemDataBound` 事件处理程序中，可以检查当前项的数据，然后将格式设置应用于模板的内容，或应用于将 `DataListItem` 的内容应用于整个项本身。

或者，可以通过格式设置函数来实现自定义格式设置。 格式设置函数是一种方法，可从 DataList 或 Repeater 模板调用，这些模板返回要在其位置发出的 HTML。 通常，格式设置函数返回的 HTML 由绑定到当前项的值确定。 这些值可作为标量值或通过传入要绑定到项的整个对象（如 `ProductsRow` 实例）传递到格式设置函数。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Yaakov Ellis、Randy Schmidt 和 Liz Shulok。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](displaying-data-with-the-datalist-and-repeater-controls-cs.md)
> [下一页](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
