---
uid: web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
title: 使用 FormView 的模板（C#） |Microsoft Docs
author: rick-anderson
description: 与 DetailsView 不同，FormView 不是由字段组成的。 而是使用模板呈现 FormView。 在本教程中，我们将使用 F 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d3f062af-88cf-426d-af44-e41f32c41672
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-the-formview-s-templates-cs
msc.type: authoredcontent
ms.openlocfilehash: 013c6878aad1a2277b0a334c096ff16ed84a95f1
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74625690"
---
# <a name="using-the-formviews-templates-c"></a>使用 FormView 的模板（C#）

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_14_CS.exe)或[下载 PDF](using-the-formview-s-templates-cs/_static/datatutorial14cs1.pdf)

> 与 DetailsView 不同，FormView 不是由字段组成的。 而是使用模板呈现 FormView。 在本教程中，我们将检查如何使用 FormView 控件来呈现更不严格的数据显示。

## <a name="introduction"></a>简介

在最后两个教程中，我们介绍了如何使用 Templatefield 自定义 GridView 和 DetailsView 控件的输出。 Templatefield 允许对特定字段的内容进行高度自定义，但在这种情况下，GridView 和 DetailsView 都具有相当 boxy 的外观。 在许多情况下，类似网格的布局是理想的，但有时需要更流畅、更不严格的显示。 显示单个记录时，可以使用 FormView 控件实现此类流体布局。

与 DetailsView 不同，FormView 不是由字段组成的。 不能向 FormView 添加 BoundField 或 TemplateField。 而是使用模板呈现 FormView。 将 FormView 视为包含单一 TemplateField 的 DetailsView 控件。 FormView 支持以下模板：

- `ItemTemplate`，用于呈现在 FormView 中显示的特定记录
- 用于指定可选标题行的 `HeaderTemplate`
- 用于指定可选页脚行的 `FooterTemplate`
- `EmptyDataTemplate` 在 FormView 的 `DataSource` 缺少任何记录时，`EmptyDataTemplate` 用于呈现控件标记的 `ItemTemplate`
- `PagerTemplate` 可用于为启用了分页的 FormViews 自定义分页接口
- `EditItemTemplate` / `InsertItemTemplate` 用于为支持此类功能的 FormViews 自定义编辑界面或插入接口

在本教程中，我们将检查如何使用 FormView 控件来提供不太严格的产品显示。 FormView 的 `ItemTemplate` 将使用标头元素和 `<table>` 的组合来显示这些值，而不是具有 "名称"、"类别"、"供应商" 等字段（参见图1）。

[![在 DetailsView 中查看的类似网格的布局中的 FormView 中断](using-the-formview-s-templates-cs/_static/image2.png)](using-the-formview-s-templates-cs/_static/image1.png)

**图 1**： FormView 中断了在 DetailsView 中看到的类似网格的布局（[单击以查看完全大小的图像](using-the-formview-s-templates-cs/_static/image3.png)）

## <a name="step-1-binding-the-data-to-the-formview"></a>步骤1：将数据绑定到 FormView

打开 `FormView.aspx` 页面，并将 FormView 从工具箱拖到设计器上。 第一次添加 FormView 时，它会显示为灰色框，指示我们需要 `ItemTemplate`。

[在提供 ItemTemplate 之前，![无法在设计器中呈现 FormView](using-the-formview-s-templates-cs/_static/image5.png)](using-the-formview-s-templates-cs/_static/image4.png)

**图 2**：在提供 `ItemTemplate` 之前，无法在设计器中呈现 FormView （[单击查看完全大小的图像](using-the-formview-s-templates-cs/_static/image6.png)）

可以手动创建 `ItemTemplate` （通过声明性语法），也可以通过设计器将 FormView 绑定到数据源控件来自动创建。 此自动创建的 `ItemTemplate` 包含 HTML，其中列出了每个字段的名称和 "标签" 控件，其 `Text` 属性绑定到该字段的值。 此方法还自动创建 `InsertItemTemplate` 和 `EditItemTemplate`，这两种方法都用输入控件填充数据源控件返回的每个数据字段。

如果要自动创建模板，请从 FormView 的智能标记添加一个调用 `ProductsBLL` 类的 `GetProducts()` 方法的新 ObjectDataSource 控件。 这将创建一个具有 `ItemTemplate`、`InsertItemTemplate`和 `EditItemTemplate`的 FormView。 从 "源" 视图中删除 `InsertItemTemplate` 和 `EditItemTemplate`，因为我们不想创建支持编辑或插入的 FormView。 接下来，请清除 `ItemTemplate` 中的标记，以便我们可以使用全新的盖板。

如果您想手动生成 `ItemTemplate`，则可以通过将该 ObjectDataSource 从工具箱拖到设计器上来添加和配置它。 不过，请不要在设计器中设置 FormView 的数据源。 相反，请转到 "源" 视图，手动将 FormView 的 `DataSourceID` 属性设置为 ObjectDataSource 的 `ID` 值。 接下来，手动添加 `ItemTemplate`。

无论你决定采用哪种方法，此时，你的 FormView 的声明性标记应如下所示：

[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample1.aspx)]

请花点时间选中 FormView 的智能标记中的 "启用分页" 复选框;这会将 `AllowPaging="True"` 特性添加到 FormView 的声明性语法。 同时，将 `EnableViewState` 属性设置为 False。

## <a name="step-2-defining-theitemtemplates-markup"></a>步骤2：定义`ItemTemplate`的标记

将 FormView 绑定到 ObjectDataSource 控件，并将其配置为支持分页后，就可以指定 `ItemTemplate`的内容了。 对于本教程，我们将在 `<h3>` 标题中显示产品的名称。 接下来，让我们使用 HTML `<table>` 将剩余的产品属性显示在一个四列的表中，其中第一个和第三个列列出了属性名称，第二个和第四个列表的值。

此标记可以通过设计器中的 FormView 模板编辑界面输入，也可以通过声明性语法手动输入。 使用模板时，我通常会发现直接使用声明性语法会更快速，但可以随意使用您最喜欢的任何方法。

以下标记显示了完成 `ItemTemplate`结构后的 FormView 声明性标记：

[!code-aspx[Main](using-the-formview-s-templates-cs/samples/sample2.aspx)]

请注意，可以将数据绑定语法 `<%# Eval("ProductName") %>`（例如）直接注入模板的输出中。 也就是说，无需将其分配给标签控件的 `Text` 属性。 例如，使用 `<h3><%# Eval("ProductName") %></h3>`显示在 `<h3>` 元素中的 `ProductName` 值，该产品 Chai 将呈现为 `<h3>Chai</h3>`。

`ProductPropertyLabel` 和 `ProductPropertyValue` CSS 类用于指定 `<table>`中的产品属性名称和值的样式。 这些 CSS 类在 `Styles.css` 中定义，并导致属性名称为粗体和右对齐，并向属性值添加右填充。

由于 FormView 中没有可用的 CheckBoxFields，因此，为了将 `Discontinued` 值显示为复选框，我们必须添加自己的 CheckBox 控件。 `Enabled` 属性设置为 False，使其成为只读的，复选框的 `Checked` 属性将绑定到 `Discontinued` 数据字段的值。

`ItemTemplate` 完成后，产品信息将以更流畅的方式显示。 将最后一个教程中的 DetailsView 输出（图3）与本教程中的 FormView 生成的输出进行比较（图4）。

[![严格 DetailsView 输出](using-the-formview-s-templates-cs/_static/image8.png)](using-the-formview-s-templates-cs/_static/image7.png)

**图 3**：硬 DetailsView 输出（[单击以查看完全大小的图像](using-the-formview-s-templates-cs/_static/image9.png)）

[![流体的 FormView 输出](using-the-formview-s-templates-cs/_static/image11.png)](using-the-formview-s-templates-cs/_static/image10.png)

**图 4**：流体的 FormView 输出（[单击以查看完全大小的图像](using-the-formview-s-templates-cs/_static/image12.png)）

## <a name="summary"></a>总结

尽管 GridView 和 DetailsView 控件可以使用 Templatefield 自定义其输出，但仍会以类似于网格的 boxy 格式显示其数据。 在需要使用不太严格的布局来显示单个记录的情况下，FormView 是理想选择。 与 DetailsView 一样，FormView 从其 `DataSource`呈现单条记录，但与 DetailsView 不同的是，它仅由模板组成，不支持字段。

如本教程中所述，在显示单个记录时，FormView 允许使用更灵活的布局。 在将来的教程中，我们将检查 DataList 和 Repeater 控件，它们提供与 FormsView 相同级别的灵活性，但能够显示多个记录（如 GridView）。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 E.R。 Gilmore. 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](using-templatefields-in-the-detailsview-control-cs.md)
> [下一页](displaying-summary-information-in-the-gridview-s-footer-cs.md)
