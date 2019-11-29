---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-vb
title: 添加单选按钮的 GridView 列（VB） |Microsoft Docs
author: rick-anderson
description: 本教程介绍如何向 GridView 控件添加一列单选按钮，以向用户提供一种更直观的方式来选择单个行 。
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 2e31b60b-8723-4f14-b7ee-37859454dc3b
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-vb
msc.type: authoredcontent
ms.openlocfilehash: ee67a4556c65d2c9570bf15b42fc3c8e5f555bda
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593190"
---
# <a name="adding-a-gridview-column-of-radio-buttons-vb"></a>添加 GridView 单选按钮列 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_51_VB.exe)或[下载 PDF](adding-a-gridview-column-of-radio-buttons-vb/_static/datatutorial51vb1.pdf)

> 本教程介绍如何向 GridView 控件添加一列单选按钮，以便为用户提供更直观的方式来选择多个 GridView 行。

## <a name="introduction"></a>简介

GridView 控件提供大量的内置功能。 它包括多个用于显示文本、图像、超链接和按钮的不同字段。 它支持用于进一步自定义的模板。 只需单击几下鼠标，就能创建一个 GridView，其中每行都可以通过按钮进行选择，或启用编辑或删除功能。 尽管很多提供的功能，但在某些情况下，需要添加其他不支持的功能。 在本教程和接下来的两个教程中，我们将探讨如何增强 GridView 的功能以包含其他功能。

本教程和下一个教程重点介绍如何增强行选择过程。 如[使用可选的主控 GridView 和详细信息 DetailView 在主/详细信息](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)中进行检查，我们可以将 CommandField 添加到包含 "选择" 按钮的 GridView。 单击 "回发" 时，"`SelectedIndex` 可以" 属性将更新为单击 "选择" 按钮的行的索引。 在[主/详细信息中，使用可选择的主 GridView 和详细信息 DetailView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)教程，我们看到了如何使用此功能显示所选 GridView 行的详细信息。

尽管 "选择" 按钮在许多情况下都起作用，但它可能也不适用于其他人。 通常将其他两个用户界面元素用于选择：单选按钮和复选框，而不是使用按钮。 我们可以增加 GridView，使其而不是选择按钮，每行包含单选按钮或复选框。 在用户只能选择其中一个 GridView 记录的情况下，单选按钮可能优于 "选择" 按钮。 如果用户可能会在基于 web 的电子邮件应用程序中选择多个记录，例如在基于 web 的电子邮件应用程序中，用户可能想要选择多个邮件以删除复选框，则会提供 "选择按钮" 或 "单选按钮" 中不可用的功能。用户界面。

本教程介绍如何将一列单选按钮添加到 GridView。 继续教程探讨了如何使用 checkbox。

## <a name="step-1-creating-the-enhancing-the-gridview-web-pages"></a>步骤1：创建增强 GridView 网页

在开始增强 GridView 以包含一列单选按钮之前，让我们先花点时间在我们的网站项目中创建 ASP.NET 页面，我们将在本教程和接下来的两个网页中创建。 首先添加一个名为 `EnhancedGridView`的新文件夹。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `RadioButtonField.aspx`
- `CheckBoxField.aspx`
- `InsertThroughFooter.aspx`

![为 SqlDataSource 相关教程添加 ASP.NET 页](adding-a-gridview-column-of-radio-buttons-vb/_static/image1.gif)

**图 1**：添加 SqlDataSource 相关教程的 ASP.NET 页

与在其他文件夹中一样，`EnhancedGridView` 文件夹中的 `Default.aspx` 会在其部分列出教程。 请记住，`SectionLevelTutorialListing.ascx` 用户控件提供此功能。 因此，通过将此用户控件从解决方案资源管理器拖到页面 s 设计视图，将该用户控件添加到 `Default.aspx`。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](adding-a-gridview-column-of-radio-buttons-vb/_static/image2.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image1.png)

**图 2**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image2.png)）

最后，将这四个页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，请在使用 SqlDataSource 控件后添加以下标记 `<siteMapNode>`：

[!code-xml[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample1.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧菜单现在包含用于编辑、插入和删除教程的项。

![站点映射现在包含用于增强 GridView 教程的条目](adding-a-gridview-column-of-radio-buttons-vb/_static/image3.gif)

**图 3**：站点地图现在包含用于增强 GridView 教程的条目

## <a name="step-2-displaying-the-suppliers-in-a-gridview"></a>步骤2：在 GridView 中显示供应商

在本教程中，我们将构建一个 GridView，其中列出了美国的供应商，每个 GridView 行都提供一个单选按钮。 通过单选按钮选择供应商后，用户可以通过单击按钮查看供应商的产品。 尽管此任务听起来很简单，但有许多微妙之处，这会使其显得特别棘手。 在深入探讨这些微妙之处之前，首先让我们获得一个 GridView 列出供应商。

首先，通过将 GridView 从工具箱拖到设计器上，打开 `EnhancedGridView` 文件夹中的 `RadioButtonField.aspx` 页。 将 GridView `ID` 设置为 `Suppliers`，并从其智能标记中选择创建新的数据源。 具体而言，就是从 `SuppliersBLL` 对象中创建一个名为 `SuppliersDataSource` 的 ObjectDataSource。

[![创建一个名为 SuppliersDataSource 的新 ObjectDataSource](adding-a-gridview-column-of-radio-buttons-vb/_static/image4.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image3.png)

**图 4**：创建名为 `SuppliersDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](adding-a-gridview-column-of-radio-buttons-vb/_static/image4.png)）

[![将 ObjectDataSource 配置为使用 SuppliersBLL 类](adding-a-gridview-column-of-radio-buttons-vb/_static/image5.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image5.png)

**图 5**：将 ObjectDataSource 配置为使用 `SuppliersBLL` 类（[单击以查看完全大小的映像](adding-a-gridview-column-of-radio-buttons-vb/_static/image6.png)）

由于我们只想列出美国的这些供应商，因此请从 "选择" 选项卡的下拉列表中选择 `GetSuppliersByCountry(country)` 方法。

[![将 ObjectDataSource 配置为使用 SuppliersBLL 类](adding-a-gridview-column-of-radio-buttons-vb/_static/image6.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image7.png)

**图 6**：将 ObjectDataSource 配置为使用 `SuppliersBLL` 类（[单击以查看完全大小的映像](adding-a-gridview-column-of-radio-buttons-vb/_static/image8.png)）

在 "更新" 选项卡中，选择 "（无）" 选项并单击 "下一步"。

[![将 ObjectDataSource 配置为使用 SuppliersBLL 类](adding-a-gridview-column-of-radio-buttons-vb/_static/image7.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image9.png)

**图 7**：将 ObjectDataSource 配置为使用 `SuppliersBLL` 类（[单击以查看完全大小的映像](adding-a-gridview-column-of-radio-buttons-vb/_static/image10.png)）

由于 `GetSuppliersByCountry(country)` 方法接受参数，因此 "配置数据源" 向导会提示我们输入该参数的源。 若要指定硬编码值（在此示例中为 USA），请将 "参数源" 下拉列表设置为 "无"，并在文本框中输入默认值。 单击“完成”按钮以完成向导。

[![使用 USA 作为 country 参数的默认值](adding-a-gridview-column-of-radio-buttons-vb/_static/image8.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image11.png)

**图 8**：使用 USA 作为 `country` 参数的默认值（[单击以查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image12.png)）

完成向导后，GridView 将为每个供应商数据字段包括 BoundField。 删除除 `CompanyName`、`City`和 `Country` BoundFields 以外的所有，并将 `CompanyName` BoundFields `HeaderText` 属性重命名为 "供应商"。 完成此操作后，GridView 和 ObjectDataSource 声明性语法应类似于以下内容。

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample2.aspx)]

对于本教程，让用户可以在与供应商列表相同的页面上或在其他页面上查看所选供应商的产品。 为此，请将两个按钮 Web 控件添加到页面。 我已将这两个按钮的 `ID` 设置为 `ListProducts` 和 `SendToProducts`，这一想法表明，当单击 `ListProducts` 时，所选供应商的产品将在同一页上列出，但当单击 `SendToProducts` 时，用户将 whisked 另一页列出产品。

图9显示了在浏览器中查看 `Suppliers` GridView 和两个按钮 Web 控件。

[![美国的这些供应商列出了其姓名、城市和国家/地区信息](adding-a-gridview-column-of-radio-buttons-vb/_static/image9.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image13.png)

**图 9**：美国的这些供应商列出了其姓名、城市和国家/地区信息（[单击查看全尺寸图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image14.png)）

## <a name="step-3-adding-a-column-of-radio-buttons"></a>步骤3：添加单选按钮列

此时，`Suppliers` GridView 有三个 BoundFields，其中显示了美国每个供应商的公司名称、城市和国家/地区。 不过，它仍缺少单选按钮的列。 遗憾的是，GridView 不包含内置 RadioButtonField，但我们只需将其添加到网格即可完成。 相反，我们可以添加 TemplateField 并配置其 `ItemTemplate` 以呈现单选按钮，从而生成每个 GridView 行的单选按钮。

最初，我们可能会假设所需的用户界面可以通过将单选按钮 Web 控件添加到 TemplateField 的 `ItemTemplate` 来实现。 虽然这确实会向 GridView 的每个行添加一个单选按钮，但无法对单选按钮进行分组，因此它们不是互相排斥的。 也就是说，最终用户可以从 GridView 同时选择多个单选按钮。

即使使用的是单选按钮 Web 控件的 TemplateField，也不能提供所需的功能，因为这种方法有必要检查未分组所产生的单选按钮的原因。 首先将 TemplateField 添加到供应商 GridView，使其成为最左侧的字段。 接下来，在 GridView s 智能标记中，单击 "编辑模板" 链接，并将单选按钮 Web 控件从工具箱拖到 TemplateField s `ItemTemplate` （请参阅图10）。 将单选按钮 `ID` 属性设置为 `RowSelector`，将 `GroupName` 属性设置为 `SuppliersGroup`。

[![向 ItemTemplate 添加单选按钮 Web 控件](adding-a-gridview-column-of-radio-buttons-vb/_static/image10.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image15.png)

**图 10**：向 `ItemTemplate` 添加单选按钮 Web 控件（[单击以查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image16.png)）

通过设计器进行这些添加后，GridView 的标记应如下所示：

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample3.aspx)]

单选按钮[`GroupName` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.radiobutton.groupname(VS.80).aspx)用于对一系列单选按钮进行分组。 所有具有相同 `GroupName` 值的单选按钮控件均视为已分组;一次只能从一个组中选择一个单选按钮。 `GroupName` 属性指定呈现的单选按钮的 `name` 属性的值。 浏览器将检查单选按钮 `name` 属性以确定单选按钮分组。

将单选按钮 Web 控件添加到 `ItemTemplate`后，通过浏览器访问此页，然后单击网格行中的单选按钮。 请注意单选按钮如何分组，如图11所示，可以选择所有行。

[![未分组 GridView 单选按钮](adding-a-gridview-column-of-radio-buttons-vb/_static/image11.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image17.png)

**图 11**：不组合 GridView 的单选按钮（[单击以查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image18.png)）

单选按钮未分组的原因是因为它们 `name` 属性的呈现方式不同，但它们 `GroupName` 属性设置相同。 若要查看这些差异，请从浏览器执行视图/源并检查单选按钮标记：

[!code-html[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample4.html)]

请注意，`name` 和 `id` 属性与属性窗口中指定的值并不完全相同，但会附带多个其他 `ID` 值。 添加到呈现的 `id` 和 `name` 特性前面的附加 `ID` 值是单选按钮的 `ID`，父控件控制 `GridViewRow` s `ID`、GridView `ID`、内容控件 `ID`和 Web 窗体 `ID`。 添加这些 `ID`，这样，在 GridView 中呈现的每个 Web 控件都具有唯一的 `id` 和 `name` 值。

每个呈现的控件都需要不同 `name` 和 `id`，因为这是浏览器在客户端唯一标识每个控件的方式，以及它如何识别到 web 服务器回发时所发生的操作或更改。 例如，假设您希望在单选按钮的选中状态发生更改时运行一些服务器端代码。 为此，我们可以将 `AutoPostBack` 的单选按钮设置为 `True` 并为 `CheckChanged` 事件创建事件处理程序。 但是，如果为所有单选按钮呈现的 `name` 和 `id` 值相同，则回发时无法确定单击了哪个特定的单选按钮。

简而言之，我们不能使用单选按钮 Web 控件在 GridView 中创建一列单选按钮。 相反，我们必须使用陈旧的技术来确保将相应的标记注入到每个 GridView 行中。

> [!NOTE]
> 与单选按钮 Web 控件一样，单选按钮 HTML 控件添加到模板时，将包含唯一的 `name` 属性，使网格中的单选按钮取消分组。 如果你不熟悉 HTML 控件，可以随意忽略此注释，因为很少使用 HTML 控件，尤其是在 ASP.NET 2.0 中。 但如果想要了解详细信息，请参阅[Allen](http://odetocode.com/blogs/scott/default.aspx) s 博客文章[WEB 控件和 HTML 控件](http://www.odetocode.com/Articles/348.aspx)。

## <a name="using-a-literal-control-to-inject-radio-button-markup"></a>使用文本控件注入单选按钮标记

为了正确地分组 GridView 内的所有单选按钮，我们需要将单选按钮标记手动注入到 `ItemTemplate`中。 每个单选按钮都需要相同的 `name` 属性，但应具有唯一的 `id` 属性（如果我们想通过客户端脚本访问单选按钮）。 用户选择单选按钮并回发页面后，浏览器会将所选单选按钮 s `value` 属性的值发送回。 因此，每个单选按钮都需要唯一的 `value` 属性。 最后，在回发时，我们需要确保将 `checked` 特性添加到选定的单选按钮，否则在用户做出选择并回发后，单选按钮将恢复为其默认状态（所有未选择）。

可以采用两种方法将低级标记注入到模板。 一种方法是混合使用标记和调用代码隐藏类中定义的格式设置方法。 这项技术首先在 GridView 控件教程中的 "[使用 templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) " 中讨论。 在本例中，它可能类似于：

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample5.aspx)]

此处，`GetUniqueRadioButton` 和 `GetRadioButtonValue` 会是代码隐藏类中定义的方法，这些方法返回相应的 `id` 并 `value` 每个单选按钮的属性值。 这种方法非常适合用于分配 `id` 和 `value` 属性，但需要指定 `checked` 属性值时，这种方法非常简短，因为仅当数据第一次绑定到 GridView 时才会执行数据绑定语法。 因此，如果 GridView 启用了视图状态，则仅在第一次加载页面时（或在 GridView 显式重新绑定到数据源时）才会触发格式设置方法，因此不会在回发时调用设置 `checked` 属性的函数。 这只是一个非常微妙的问题，而不是本文的讨论范围，因此，我将把它留给我们。 不过，我确实会鼓励您尝试使用上述方法，并通过它来处理您会遇到的问题。 虽然这种做法不会使您更接近于工作版本，但它将帮助您更深入地了解 GridView 和数据绑定生命周期。

在模板中注入自定义低级别标记的另一种方法是将 "[文本" 控件](https://msdn.microsoft.com/library/sz4949ks(VS.80).aspx)添加到模板。 然后，在 GridView `RowCreated` 或 `RowDataBound` 事件处理程序中，可以通过编程方式访问文本控件，并将其 `Text` 属性设置为要发出的标记。

首先从 TemplateField s `ItemTemplate`中删除单选按钮，并将其替换为文本控件。 将文本控件 s `ID` 设置为 `RadioButtonMarkup`。

[![向 ItemTemplate 添加文本控件](adding-a-gridview-column-of-radio-buttons-vb/_static/image12.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image19.png)

**图 12**：向 `ItemTemplate` 添加文本控件（[单击以查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image20.png)）

接下来，为 GridView `RowCreated` 事件创建事件处理程序。 无论数据是否正在重新绑定到 GridView，都将对每个添加的行触发一次 `RowCreated` 事件。 这意味着，即使在从视图状态重新加载数据时，也会在回发时进行，但仍会激发 `RowCreated` 事件，这是我们使用它而不是 `RowDataBound` 的原因（仅当数据显式绑定到数据 Web 控件时才触发）。

在此事件处理程序中，我们只想要在我们处理数据行的情况下继续操作。 对于每个数据行，我们想要以编程方式引用 `RadioButtonMarkup` 文字控件，并将其 `Text` 属性设置为要发出的标记。 如下面的代码所示，发出的标记将创建一个单选按钮，其 `name` 特性设置为 `SuppliersGroup`，其 `id` 特性设置为 `RowSelectorX`，其中*X*是 gridview 行的索引，其 `value` 特性设置为 gridview 行的索引。

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample6.vb)]

选择 GridView 行并发生回发时，我们将对所选供应商的 `SupplierID` 感兴趣。 因此，可能会认为每个单选按钮的值应为实际 `SupplierID` （而不是 GridView 行的索引）。 尽管这在某些情况下可能会起作用，但盲目接受并处理 `SupplierID`会带来安全风险。 例如，我们的 GridView 仅列出了 USA 中的供应商。 但是，如果直接从单选按钮传递 `SupplierID`，将停止非常用户处理回发回发回的 `SupplierID` 值？ 通过使用行索引作为 `value`，然后从 `DataKeys` 集合获取对回发的 `SupplierID`，我们可以确保用户仅使用与某个 GridView 行关联的 `SupplierID` 值之一。

添加此事件处理程序代码后，请花几分钟时间在浏览器中测试页面。 首先，请注意，一次只能选择网格中的一个单选按钮。 但是，当选择某个单选按钮并单击其中一个按钮时，会发生回发，并且单选按钮会恢复到其初始状态（即，在回发时，不再选中所选单选按钮）。 若要解决此问题，我们需要增加 `RowCreated` 事件处理程序，使其检查从回发发送的所选单选按钮索引，并将 `checked="checked"` 属性添加到已发出的行索引匹配项。

发生回发时，浏览器将回发 `name` 和所选单选按钮的 `value`。 可以使用 `Request.Form("name")`以编程方式检索该值。 [`Request.Form` 属性](https://msdn.microsoft.com/library/system.web.httprequest.form.aspx)提供表示窗体变量的[`NameValueCollection`](https://msdn.microsoft.com/library/system.collections.specialized.namevaluecollection.aspx) 。 窗体变量是网页中窗体字段的名称和值，并在每次回发可以时由 web 浏览器发回。 由于 GridView 中的单选按钮的呈现 `name` 属性是 `SuppliersGroup`的，因此当网页回发后，浏览器会将 `SuppliersGroup=valueOfSelectedRadioButton` 发送回 web 服务器（与其他窗体字段一起）。 然后，可以使用： `Request.Form("SuppliersGroup")`从 `Request.Form` 属性访问此信息。

由于我们需要确定仅在 `RowCreated` 事件处理程序中选定的单选按钮索引，但在按钮 Web 控件的 `Click` 事件处理程序中，如果未选择任何单选按钮，则允许向返回 `-1` 的代码隐藏类添加 `SuppliersSelectedIndex` 属性，如果选择了其中一个单选按钮，则添加所选索引。

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample7.vb)]

添加此属性后，如果 `SuppliersSelectedIndex` 等于 `e.Row.RowIndex`，我们知道在 `RowCreated` 事件处理程序中添加 `checked="checked"` 标记。 更新事件处理程序以包括此逻辑：

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample8.vb)]

进行此更改后，在回发后，所选单选按钮将保持选中状态。 现在，我们能够指定选定的单选按钮，我们可以更改该行为，以便在第一次访问该页面时，选中第一个 "GridView 行" 单选按钮（而不是默认选择默认的单选按钮，这是当前行为）。 若要在默认情况下选择第一个单选按钮，只需将 `If SuppliersSelectedIndex = e.Row.RowIndex Then` 语句更改为以下内容： `If SuppliersSelectedIndex = e.Row.RowIndex OrElse (Not Page.IsPostBack AndAlso e.Row.RowIndex = 0) Then`。

此时，我们已将分组单选按钮列添加到 GridView 中，这样就可以在回发中选择并记住单个 GridView 行。 接下来的步骤是显示所选供应商提供的产品。 在步骤4中，我们将了解如何将用户重定向到另一页，并沿选定 `SupplierID`发送。 在步骤5中，我们将了解如何在同一页面上的 GridView 中显示所选供应商的产品。

> [!NOTE]
> 我们可以创建一个自定义 `DataControlField` 类来呈现适当的用户界面和功能，而不是使用 TemplateField （此冗长步骤3的重点）。 [`DataControlField` 类](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.aspx)是 BoundField、CheckBoxField、TemplateField 和其他内置 GridView 和 DetailsView 字段派生的基类。 创建自定义 `DataControlField` 类将意味着可以使用声明性语法添加单选按钮列，并且还可以更轻松地复制其他网页和其他 web 应用程序中的功能。

不过，如果你曾在 ASP.NET 中创建了自定义的已编译控件，则你知道这样做需要相当多的琐碎工作，并为其提供必须小心处理的微妙之处和 edge 事例的宿主。 因此，我们将放弃将一列作为自定义 `DataControlField` 类实现为现在并使用 TemplateField 选项。 也许我们可以在以后的教程中了解如何创建、使用和部署自定义 `DataControlField` 类！

## <a name="step-4-displaying-the-selected-supplier-s-products-in-a-separate-page"></a>步骤4：在单独的页面中显示所选供应商的产品

用户选择了 GridView 行后，需要显示所选供应商的产品。 在某些情况下，我们可能希望在单独的页面上显示这些产品，在其他页面中，我们可能更喜欢在同一页面中执行此操作。 首先，让我们检查如何在单独的页面上显示产品;在步骤5中，我们将介绍如何将 GridView 添加到 `RadioButtonField.aspx` 以显示选定的供应商产品。

当前页面上有两个按钮 Web 控件 `ListProducts` 和 `SendToProducts`。 单击 "`SendToProducts`" 按钮时，我们希望将用户发送到 `~/Filtering/ProductsForSupplierDetails.aspx`。 此页是在 "[跨两页的主/详细信息筛选](../masterdetail/master-detail-filtering-across-two-pages-vb.md)" 教程中创建的，它显示了其 `SupplierID` 通过名为 `SupplierID`的 querystring 字段传递的供应商的产品。

若要提供此功能，请为 `SendToProducts` "按钮 `Click` 事件创建事件处理程序。 在步骤3中，我们添加了 `SuppliersSelectedIndex` 属性，该属性返回选定的单选按钮所在的行的索引。 可以从 GridView 的 `DataKeys` 集合中检索相应的 `SupplierID`，然后可以使用 `Response.Redirect("url")`将用户发送到 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID`。

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample9.vb)]

只要从 GridView 中选择一个单选按钮，此代码就会 wonderfully。 如果最初没有选择任何单选按钮，并且用户单击 "`SendToProducts`" 按钮，则 `SuppliersSelectedIndex` 将 `-1`，这将导致引发异常，因为 `-1` 超出了 `DataKeys` 集合的索引范围。 但这并不是个问题，不过，如果您决定按照第3步中所述更新 `RowCreated` 事件处理程序，以使其最初选择的是 GridView 中的第一个单选按钮。

为了容纳 `-1``SuppliersSelectedIndex` 值，请将一个 "标签" Web 控件添加到 GridView 之上的页面。 将其 `ID` 属性设置为 `ChooseSupplierMsg`，其 `CssClass` 属性设置为 `Warning`，其 `EnableViewState` 和 `Visible` 属性设置为 `False`，并将其 `Text` 属性设置为从网格中选择一个供应商。 CSS 类 `Warning` 用红色、斜体、粗体、大字体显示文本，并在 `Styles.css`中定义。 通过将 `EnableViewState` 和 `Visible` 属性设置为 `False`，除了仅以编程方式将控件 `Visible` 属性设置为 `True`的回发之外，不呈现标签。

[![在 GridView 上方添加标签 Web 控件](adding-a-gridview-column-of-radio-buttons-vb/_static/image13.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image21.png)

**图 13**：在 GridView 上方添加标签 Web 控件（[单击以查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image22.png)）

接下来，增加 `Click` 事件处理程序，如果 `SuppliersSelectedIndex` 小于零，则显示 `ChooseSupplierMsg` 标签，并将用户重定向到 `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID`。

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample10.vb)]

在浏览器中访问该页面，然后单击 "`SendToProducts`" 按钮，然后从 GridView 中选择一个供应商。 如图14所示，这将显示 "`ChooseSupplierMsg`" 标签。 接下来，选择一个供应商，然后单击 "`SendToProducts`" 按钮。 这会 whisk 您的页面列出所选供应商提供的产品。 图15显示了选择 Bigfoot Breweries 供应商时的 "`ProductsForSupplierDetails.aspx`" 页。

[![如果未选择任何供应商，则显示 "ChooseSupplierMsg" 标签](adding-a-gridview-column-of-radio-buttons-vb/_static/image14.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image23.png)

**图 14**：如果未选择任何供应商，则显示 `ChooseSupplierMsg` 标签（[单击以查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image24.png)）

[![所选供应商的产品将显示在 ProductsForSupplierDetails 中](adding-a-gridview-column-of-radio-buttons-vb/_static/image15.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image25.png)

**图 15**：所选供应商的产品在 `ProductsForSupplierDetails.aspx` 中显示（[单击查看完全尺寸的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image26.png)）

## <a name="step-5-displaying-the-selected-supplier-s-products-on-the-same-page"></a>步骤5：在同一页面上显示所选供应商的产品

在步骤4中，我们看到了如何将用户发送到另一个网页以显示选定的供应商产品。 或者，所选供应商的产品可以显示在同一页上。 为了说明这一点，我们将向 `RadioButtonField.aspx` 添加一个 GridView 来显示所选供应商的产品。

由于我们只希望在选择供应商后显示这一 GridView 产品，因此请在 `Suppliers` GridView 下添加 Panel Web 控件，并将其 `ID` 设置为 `ProductsBySupplierPanel`，并将其 `Visible` 属性设置为 `False`。 在面板中，为所选供应商添加文本产品，然后添加名为 `ProductsBySupplier`的 GridView。 从 GridView s 智能标记中，选择将其绑定到名为 `ProductsBySupplierDataSource`的新 ObjectDataSource。

[![将 ProductsBySupplier GridView 绑定到新的 ObjectDataSource](adding-a-gridview-column-of-radio-buttons-vb/_static/image16.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image27.png)

**图 16**：将 `ProductsBySupplier` GridView 绑定到新的 ObjectDataSource （[单击以查看完全大小的映像](adding-a-gridview-column-of-radio-buttons-vb/_static/image28.png)）

接下来，将 ObjectDataSource 配置为使用 `ProductsBLL` 类。 由于我们只想检索所选供应商提供的产品，因此请指定 ObjectDataSource 应调用 `GetProductsBySupplierID(supplierID)` 方法来检索其数据。 从 "更新"、"插入" 和 "删除" 选项卡的下拉列表中选择 "（无）"。

[![将 ObjectDataSource 配置为使用 GetProductsBySupplierID （供应商）方法](adding-a-gridview-column-of-radio-buttons-vb/_static/image17.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image29.png)

**图 17**：将 ObjectDataSource 配置为使用 `GetProductsBySupplierID(supplierID)` 方法（[单击查看完全大小的映像](adding-a-gridview-column-of-radio-buttons-vb/_static/image30.png)）

[![在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"](adding-a-gridview-column-of-radio-buttons-vb/_static/image18.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image31.png)

**图 18**：将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image32.png)）

在配置了 SELECT、UPDATE、INSERT 和 DELETE 选项卡后，单击 "下一步"。 由于 `GetProductsBySupplierID(supplierID)` 方法需要输入参数，因此 "创建数据源" 向导会提示我们指定参数 s 值的源。

此处有几个选项可用于指定参数 s 值的源。 可以使用默认参数对象，并以编程方式将 `SuppliersSelectedIndex` 属性的值分配给 ObjectDataSource `Selecting` 事件处理程序中的参数 s `DefaultValue` 属性。 请参阅以[编程方式设置 objectdatasource 的参数值](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb.md)教程，了解如何以编程方式为 objectdatasource 参数分配值。

此外，我们还可以使用 ControlParameter 并引用 `Suppliers` GridView s [`SelectedValue` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue.aspx)（参见图19）。 GridView `SelectedValue` 属性返回对应于[`SelectedIndex` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex.aspx)的 `DataKey` 值。 若要使此选项正常运行，需要在单击 "`ListProducts`" 按钮时以编程方式将 "GridView" `SelectedIndex` 属性设置为所选行。 作为一项附加优势，通过设置 `SelectedIndex`，所选记录将采用 `DataWebControls` 主题中定义的 `SelectedRowStyle` （黄色背景）。

[![使用 ControlParameter 将 GridView s SelectedValue 指定为参数源](adding-a-gridview-column-of-radio-buttons-vb/_static/image19.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image33.png)

**图 19**：使用 ControlParameter 将 GridView s SelectedValue 指定为参数源（[单击查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image34.png)）

完成向导后，Visual Studio 将自动为产品的数据字段添加字段。 删除 `ProductName`、`CategoryName`和 `UnitPrice` 的所有 BoundFields，并将 `HeaderText` 属性更改为 "产品"、"类别" 和 "价格"。 配置 `UnitPrice` BoundField，以便将其值设置为货币格式。 进行这些更改后，面板、GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample11.aspx)]

若要完成此练习，我们需要将 "GridView s `SelectedIndex`" 属性设置为 "`SelectedSuppliersIndex`，将 `ProductsBySupplierPanel` 面板 `Visible`" 属性设置为在单击 "`True`" 按钮时 `ListProducts`。 若要完成此操作，请为 `ListProducts` 按钮 Web 控件 `Click` 事件创建事件处理程序，并添加以下代码：

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample12.vb)]

如果尚未从 GridView 中选择供应商，将显示 `ChooseSupplierMsg` 标签，并隐藏 "`ProductsBySupplierPanel`" 面板。 否则，如果选择了某个供应商，则会显示 `ProductsBySupplierPanel`，并更新 GridView 的 `SelectedIndex` 属性。

图20显示了在选择了 Bigfoot Breweries 供应商并且单击了 "在页面上显示产品" 按钮后的结果。

[![在同一页面上列出了 Bigfoot Breweries 提供的产品](adding-a-gridview-column-of-radio-buttons-vb/_static/image20.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image35.png)

**图 20**： Bigfoot Breweries 提供的产品在同一页面上列出（[单击以查看完全大小的图像](adding-a-gridview-column-of-radio-buttons-vb/_static/image36.png)）

## <a name="summary"></a>总结

如[使用可选的主控 GridView 和详细信息 DetailView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md)教程中所述，可以使用 CommandField （其 `ShowSelectButton` 属性设置为 `True`）从 GridView 中选择记录。 但 CommandField 将其按钮显示为普通的按钮、链接或图像。 备用行选择用户界面是在每个 GridView 行中提供单选按钮或复选框。 在本教程中，我们介绍了如何添加单选按钮的列。

遗憾的是，添加单选按钮列不会像预期那样简单简单或简单。 不存在可在单击按钮时添加的内置 RadioButtonField，在 TemplateField 中使用单选按钮 Web 控件引入了自己的一组问题。 最终，若要提供此类接口，我们需要创建一个自定义 `DataControlField` 类，或在 `RowCreated` 事件期间将相应的 HTML 注入 TemplateField。

了解如何添加单选按钮列后，让我们把注意力变成添加复选框。 通过一列 checkbox，用户可以选择一个或多个 GridView 行，然后对所有选定的行执行某些操作（例如，从基于 web 的电子邮件客户端选择一组电子邮件，然后选择删除所有选定的电子邮件）。 在下一教程中，我们将了解如何添加此类列。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导审查人员是 David Suru。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
> [下一页](adding-a-gridview-column-of-checkboxes-vb.md)
