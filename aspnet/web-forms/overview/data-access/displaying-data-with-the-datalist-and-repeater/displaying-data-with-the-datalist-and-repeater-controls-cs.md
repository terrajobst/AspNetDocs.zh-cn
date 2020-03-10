---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs
title: 用 DataList 和 Repeater 控件显示数据（C#） |Microsoft Docs
author: rick-anderson
description: 在前面的教程中，我们使用了 GridView 控件来显示数据。 从本教程开始，我们将介绍如何生成常见的报表模式 。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 0591cacc-b34b-4cf6-885e-2c9953bb0946
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 09d3faf811f21a66bb5c234f71d77b2552ae6516
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78495746"
---
# <a name="displaying-data-with-the-datalist-and-repeater-controls-c"></a>使用 DataList 和 Repeater 控件显示数据 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_CS.exe)或[下载 PDF](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/datatutorial29cs1.pdf)

> 在前面的教程中，我们使用了 GridView 控件来显示数据。 从本教程开始，我们将介绍如何生成包含 DataList 和 Repeater 控件的常见报表模式，从用这些控件显示数据的基础知识开始。

## <a name="introduction"></a>简介

在过去28个教程中的所有示例中，如果我们需要显示数据源中的多个记录，请转到 GridView 控件。 GridView 为数据源中的每条记录呈现一行，并在列中显示记录的数据字段。 尽管 GridView 使它能够显示、分页、排序、编辑和删除数据，但其外观有点 boxy。 此外，为 GridView 结构提供的标记是固定的，它包括一个 HTML `<table>`，其中包含每个记录的一个表行（`<tr>`）以及每个字段的表单元（`<td>`）。

若要在显示多个记录时，在外观和呈现的标记中提供更多的自定义，ASP.NET 2.0 提供 DataList 和 Repeater 控件（在 ASP.NET 版本1.x 中也提供了这两个控件）。 DataList 和 Repeater 控件使用模板而不是 BoundFields、CheckBoxFields、ButtonFields 等来呈现其内容。 与 GridView 一样，DataList 呈现为 HTML `<table>`，但允许每个表行显示多个数据源记录。 另一方面，中继器不呈现任何与显式指定的标记不同的标记，当你需要精确控制发出的标记时，它是理想的候选项。

在接下来的教程中，我们将介绍如何通过 DataList 和 Repeater 控件生成常见报表模式，从用这些控件模板显示数据的基础知识开始。 我们将了解如何设置这些控件的格式，如何更改 DataList 中数据源记录的布局、常见的主要/细节方案、编辑和删除数据的方法、如何逐页浏览记录等。

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>步骤1：添加 DataList 和 Repeater 教程网页

开始本教程之前，首先请花点时间添加本教程所需的 ASP.NET 页面，接下来的几篇教程介绍如何使用 DataList 和中继器来显示数据。 首先，在项目中创建一个名为 `DataListRepeaterBasics`的新文件夹。 接下来，将以下五个 ASP.NET 页面添加到此文件夹，所有这些页面都配置为使用母版页 `Site.master`：

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`

![创建 DataListRepeaterBasics 文件夹并添加教程 ASP.NET 页面](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image1.png)

**图 1**：创建 `DataListRepeaterBasics` 文件夹并添加教程 ASP.NET 页面

打开 `Default.aspx` 页面，并将 `SectionLevelTutorialListing.ascx` 用户控件从 `UserControls` 文件夹拖到设计图面上。 此用户控件（我们在[母版页和站点导航](../introduction/master-pages-and-site-navigation-cs.md)教程中创建）枚举站点地图并显示项目符号列表中当前部分的教程。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image2.png)

**图 2**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image4.png)）

为了使项目符号列表显示要创建的 DataList 和 Repeater 教程，我们需要将它们添加到站点映射。 打开 `Web.sitemap` 文件，并在 "添加自定义按钮" 站点地图节点标记之后添加以下标记：

[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample1.xml)]

![更新站点映射以包括新的 ASP.NET 页面](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image5.png)

**图 3**：更新站点映射以包括新的 ASP.NET 页面

## <a name="step-2-displaying-product-information-with-the-datalist"></a>步骤2：显示包含 DataList 的产品信息

与 FormView 类似，DataList 控件呈现的输出取决于模板，而不是 BoundFields、CheckBoxFields 等等。 与 FormView 不同，DataList 用于显示一组记录，而不是孤立。 在本教程中，我们将介绍如何将产品信息绑定到 DataList。 首先打开 `DataListRepeaterBasics` 文件夹中的 "`Basics.aspx`" 页。 接下来，将 DataList 从工具箱拖到设计器上。 如图4所示，在指定 DataList 的模板之前，设计器会将其显示为灰色框。

[![将 DataList 从工具箱拖到设计器上](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image6.png)

**图 4**：将 DataList 从工具箱拖到设计器上（[单击以查看完全大小的图像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image8.png)）

从 DataList s 智能标记添加新的 ObjectDataSource，并将其配置为使用 `ProductsBLL` 类 `GetProducts` 方法。 由于我们在本教程中创建了只读的 DataList，因此请在向导的插入、更新和删除选项卡中将下拉列表设置为 "（无）"。

[![Opt 创建新的 ObjectDataSource](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image9.png)

**图 5**：选择创建新的 ObjectDataSource （[单击以查看完全大小的映像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image11.png)）

[![将 ObjectDataSource 配置为使用 ProductsBLL 类](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image12.png)

**图 6**：将 ObjectDataSource 配置为使用 `ProductsBLL` 类（[单击以查看完全大小的映像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image14.png)）

[![使用 GetProducts 方法检索有关所有产品的信息](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image15.png)

**图 7**：使用 `GetProducts` 方法检索有关所有产品的信息（[单击以查看完全大小的图像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image17.png)）

配置 ObjectDataSource 并通过其智能标记将其与 DataList 关联后，Visual Studio 将在 DataList 中自动创建一个 `ItemTemplate`，该 DataList 显示数据源返回的每个数据字段的名称和值（请参阅下面的标记）。 此默认 `ItemTemplate` s 外观与通过设计器将数据源绑定到 FormView 时自动创建的模板完全相同。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample2.aspx)]

> [!NOTE]
> 回忆一下，当通过 FormView 的智能标记将数据源绑定到 FormView 控件时，Visual Studio 创建了一个 `ItemTemplate`、`InsertItemTemplate`和 `EditItemTemplate`。 但对于 DataList，只会创建一个 `ItemTemplate`。 这是因为 DataList 不具有由 FormView 提供的相同内置编辑和插入支持。 DataList 确实包含编辑和与删除相关的事件，并且可以使用一段代码添加编辑和删除支持，但对于 FormView，没有任何简单的现成支持。 在将来的教程中，我们将介绍如何在后面包含对 DataList 的编辑和删除支持。

让我们花点时间来改进此模板的外观。 只显示产品名称、供应商、类别、每个单位的数量和单价，而不是显示所有数据字段。 此外，让 s 在 `<h4>` 标题中显示该名称，并使用标题下面的 `<table>` 布局其余字段。

若要进行这些更改，您可以从 DataList 的 "DataList" 智能标记使用设计器中的模板编辑功能，单击 "编辑模板" 链接，或者可以通过页的声明性语法手动修改模板。 如果在设计器中使用 "编辑模板" 选项，则生成的标记可能不会完全匹配以下标记，但当通过浏览器查看时，其外观应与图8中所示的屏幕截图非常类似。

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample3.aspx)]

> [!NOTE]
> 上面的示例使用 `Text` 属性分配有数据绑定语法值的标签 Web 控件。 或者，我们可以完全省略标签，只需键入数据绑定语法即可。 也就是说，我们不会使用 `<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />`，而是使用声明性语法 `<%# Eval("CategoryName") %>`。

然而，在标签 Web 控件中保留两个优点。 首先，它提供了一种更简单的方法来基于数据设置数据的格式，如下一教程中所示。 其次，设计器中的 "编辑模板" 选项不会显示在某些 Web 控件之外显示的声明性数据绑定语法。 相反，编辑模板接口旨在简化静态标记和 Web 控件的使用，并假设任何数据绑定都通过 "编辑数据绑定" 对话框完成，该对话框可从 Web 控件智能标记进行访问。

因此，在使用 DataList （提供通过设计器编辑模板的选项）时，我更喜欢使用标签 Web 控件，以便通过编辑模板界面访问内容。 我们很快就会看到，Repeater 要求从 "源" 视图编辑模板的内容。 因此，在手工编写 Repeater 模板时，我通常会忽略标签 Web 控件，除非我知道我需要基于编程逻辑来设置数据绑定文本的外观。

[![使用 DataList s ItemTemplate 呈现每个产品输出](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image18.png)

**图 8**：使用 DataList `ItemTemplate` 呈现每个产品输出（[单击以查看完全大小的映像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image20.png)）

## <a name="step-3-improving-the-appearance-of-the-datalist"></a>步骤3：提高 DataList 的外观

与 GridView 类似，DataList 提供了许多与样式相关的属性，例如 `Font`、`ForeColor`、`BackColor`、`CssClass`、`ItemStyle`、`AlternatingItemStyle`、`SelectedItemStyle`等。 使用 GridView 和 DetailsView 控制时，我们在 `DataWebControls` 主题中创建了外观文件，该主题预定义了这两个控件的 `CssClass` 属性，并为其多个子属性（`RowStyle`、`HeaderStyle`等）预定义了 `CssClass` 属性。 让，为 DataList 执行相同操作。

如[使用 ObjectDataSource 显示数据](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教程中所述，外观文件为 Web 控件指定了默认的与外观相关的属性。主题是外观、CSS、图像和 JavaScript 文件的集合，用于定义网站的特定外观和外观。 在*使用 ObjectDataSource 显示数据*教程中，我们创建了一个 `DataWebControls` 主题（作为 `App_Themes` 文件夹内的文件夹实现），当前有两个外观文件-`GridView.skin` 和 `DetailsView.skin`。 让我们添加第三个外观文件来指定 DataList 的预定义样式设置。

若要添加外观文件，请右键单击 "`App_Themes/DataWebControls`" 文件夹，选择 "添加新项"，然后从列表中选择 "外观文件" 选项。 为 `DataList.skin` 文件命名。

[![创建一个名为 DataList 的新外观文件](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image21.png)

**图 9**：创建名为 `DataList.skin` 的新外观文件（[单击以查看完全大小的映像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image23.png)）

将以下标记用于 `DataList.skin` 文件：

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample4.aspx)]

这些设置将相同的 CSS 类分配给相应的 DataList 属性，就像在 GridView 和 DetailsView 控件中使用一样。 此处使用的 CSS 类 `DataWebControlStyle`、`AlternatingRowStyle`、`RowStyle`等，在 `Styles.css` 文件中定义，并已添加到前面的教程中。

添加此外观文件后，会在设计器中更新 DataList 的外观（您可能需要刷新 "设计器" 视图以查看新外观文件的效果; 从 "查看" 菜单中，选择 "刷新"）。 如图10所示，每个交替产品都有浅粉色背景色。

[![创建一个名为 DataList 的新外观文件](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image24.png)

**图 10**：创建名为 `DataList.skin` 的新外观文件（[单击以查看完全大小的映像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image26.png)）

## <a name="step-4-exploring-the-datalist-s-other-templates"></a>步骤4：浏览 DataList 其他模板

除了 `ItemTemplate`之外，DataList 还支持六个其他可选模板：

- `HeaderTemplate` 如果提供，则将标题行添加到输出，并用于呈现此行
- 用于呈现交替项的 `AlternatingItemTemplate`
- 用于呈现选定项的 `SelectedItemTemplate`;选定项是其索引对应于 DataList s [`SelectedIndex` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx)的项
- 用于呈现所编辑的项的 `EditItemTemplate`
- `SeparatorTemplate` 如果提供，则在每个项之间添加分隔符，并用于呈现此分隔符
- `FooterTemplate`-如果提供，则将页脚行添加到输出，并用于呈现此行

指定 `HeaderTemplate` 或 `FooterTemplate`时，DataList 会向呈现的输出添加一个附加的页眉或页脚行。 与 GridView 的表头和表尾行一样，DataList 中的标头和表尾不会绑定到数据。 因此，`HeaderTemplate` 或 `FooterTemplate` 中尝试访问绑定数据的任何数据绑定语法都将返回一个空字符串。

> [!NOTE]
> 正如我们在 "GridView 页脚" 教程中的[显示摘要信息](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs.md)中所述，虽然页眉和页脚行不支持数据绑定语法，但数据特定的信息可直接注入到 GridView `RowDataBound` 事件处理程序中的这些行。 此方法可用于计算绑定到控件的数据的运行总计或其他信息，以及将该信息分配给脚注。 此相同的概念可以应用于 DataList 和 Repeater 控件;唯一的区别是，对于 DataList 和 Repeater，为 `ItemDataBound` 事件创建事件处理程序（而不是 `RowDataBound` 事件的事件处理程序）。

对于我们的示例，让我们将标题产品信息显示在 DataList 的顶部，结果为 `<h3>` 标题。 若要实现此目的，请使用相应的标记添加 `HeaderTemplate`。 从设计器中，可以通过以下方式完成此操作：单击 DataList 的 "编辑模板" 链接，从下拉列表中选择 "标题模板"，然后在 "样式" 下拉列表中选择 "标题 3" 选项后输入文本（参见图11）。

[![添加 System.windows.controls.headereditemscontrol.headertemplate 和文本产品信息](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image27.png)

**图 11**：添加带有文本产品信息的 `HeaderTemplate` （[单击查看完全大小的图像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image29.png)）

或者，可以通过在 `<asp:DataList>` 标记中输入以下标记以声明方式添加此项：

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample5.html)]

若要在每个产品列表之间添加一些空间，请在每个部分之间添加一个包含一条线的 `SeparatorTemplate`。 水平规则标记（`<hr>`）将添加这样的分隔线。 创建 `SeparatorTemplate`，使其具有以下标记：

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample6.html)]

> [!NOTE]
> 与 `HeaderTemplate` 和 `FooterTemplates`一样，`SeparatorTemplate` 不会绑定到数据源中的任何记录，因此不能直接访问绑定到 DataList 的数据源记录。

完成此添加后，在浏览器中查看页面时，它应类似于图12。 请注意标题行和每个产品列表之间的行。

[![DataList 包括标题行和每个产品列表之间的水平标尺](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image30.png)

**图 12**： DataList 包含标题行和每个产品列表之间的水平标尺（[单击以查看完全大小的图像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image32.png)）

## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>步骤5：利用 Repeater 控件呈现特定标记

当访问图12中的 DataList 示例时，如果从浏览器中执行视图/源，则会看到，DataList 发出一个 HTML `<table>`，其中包含一个表行（`<tr>`），其中每个绑定到 DataList 的项都有一个表单元（`<td>`）。 事实上，这种输出与使用单个 TemplateField 从 GridView 发出的内容完全相同。 我们将在将来的教程中看到，DataList 允许对输出进行进一步自定义，使我们能够显示每个表行的多个数据源记录。

如果你不想发出 HTML `<table>`怎么办？ 若要全面控制数据 Web 控件生成的标记，必须使用 Repeater 控件。 就像 DataList 一样，Repeater 是根据模板构建的。 但中继器仅提供以下五个模板：

- `HeaderTemplate` 如果提供，则将指定的标记添加到项之前
- 用于呈现项的 `ItemTemplate`
- `AlternatingItemTemplate` （如果提供）用于呈现交替项
- `SeparatorTemplate` 如果提供，则在每个项之间添加指定的标记
- `FooterTemplate`-如果提供，则在项后添加指定的标记

在 ASP.NET 1.x 中，Repeater 控件通常用于显示项目符号列表，其数据来自某些数据源。 在这种情况下，`HeaderTemplate` 和 `FooterTemplates` 将分别包含开始和结束 `<ul>` 标记，而 `ItemTemplate` 包含数据绑定语法的 `<li>` 元素。 此方法仍可用于 ASP.NET 2.0，如我们在[母版页和站点导航](../introduction/master-pages-and-site-navigation-cs.md)教程的两个示例中所看到的那样：

- 在 `Site.master` 的母版页中，使用中继器显示顶级网站图内容的项目符号列表（基本报告、筛选报告、自定义格式等）;另一种是使用嵌套式中继器显示顶级部分的子部分
- 在 `SectionLevelTutorialListing.ascx`中，使用中继器显示当前站点地图部分的子节的项目符号列表。

> [!NOTE]
> ASP.NET 2.0 引入了新的[BulletedList 控件](https://msdn.microsoft.com/library/ms228101.aspx)，该控件可绑定到数据源控件以便显示简单的项目符号列表。 对于 BulletedList 控件，我们不需要指定任何与列表相关的 HTML;相反，我们只是指明要显示为每个列表项的文本的数据字段。

中继器用作捕获所有数据 Web 控件。 如果没有生成所需标记的现有控件，则可以使用 Repeater 控件。 为了说明如何使用中继器，让我们在步骤2中创建的产品信息 DataList 上方显示类别的列表。 具体而言，让 s 中的类别显示在单行 HTML `<table>` 中，每个类别都显示为表中的一列。

若要实现此目的，请首先将 "Repeater" 控件从工具箱拖动到设计器上的 "产品信息" DataList 上方。 对于 DataList，Repeater 最初显示为灰色框，直到定义了其模板。

[![将中继器添加到设计器](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image33.png)

**图 13**：向设计器添加中继器（[单击以查看完全大小的映像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image35.png)）

"中继器" 智能标记中只有一个选项：选择 "数据源"。 选择创建新的 ObjectDataSource，并将其配置为使用 `CategoriesBLL` 类 `GetCategories` 方法。

[![创建新的 ObjectDataSource](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image36.png)

**图 14**：创建新的 ObjectDataSource （[单击以查看完全大小的映像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image38.png)）

[![将 ObjectDataSource 配置为使用 CategoriesBLL 类](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image39.png)

**图 15**：将 ObjectDataSource 配置为使用 `CategoriesBLL` 类（[单击以查看完全大小的映像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image41.png)）

[![使用 GetCategories 方法检索有关所有类别的信息](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image42.png)

**图 16**：使用 `GetCategories` 方法检索有关所有类别的信息（[单击以查看完全大小的图像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image44.png)）

与 DataList 不同，Visual Studio 不会在将其绑定到数据源后自动为中继器创建 ItemTemplate。 此外，无法通过设计器配置 Repeater 的模板，必须以声明方式指定。

若要将类别显示为具有每个类别的列的单行 `<table>`，需要中继器发出类似于下面的标记：

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample7.html)]

由于 `<td>Category X</td>` 文本是重复的部分，因此它将显示在 Repeater 的 ItemTemplate 中。 在 `<table><tr>` 之前出现的标记将放置在 `HeaderTemplate` 中，而结束标记 `</tr></table>` 将放置在 `FooterTemplate`中。 若要输入这些模板设置，请通过单击左下角的 "源" 按钮，在 "ASP.NET" 页的声明部分中单击，然后键入以下语法：

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample8.aspx)]

中继器按模板所指定的方式发出精确的标记，无其他任何内容。 图17显示了在浏览器中查看时的中继器输出。

[![单行 HTML &lt;表&gt; 在单独的列中列出每个类别](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image45.png)

**图 17**：单行 HTML `<table>` 列出了单独列中的每个类别（[单击以查看完全大小的图像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image47.png)）

## <a name="step-6-improving-the-appearance-of-the-repeater"></a>步骤6：改善中继器的外观

由于中继器会确切地发出其模板所指定的标记，因此不会出现用于 Repeater 的无样式相关属性。 若要更改中继器生成的内容的外观，必须手动将所需的 HTML 或 CSS 内容直接添加到 Repeater 的模板。

对于我们的示例，让 s 具有类别列可选背景色，如 DataList 中的交替行。 为实现此目的，我们需要通过 `ItemTemplate` 和 `AlternatingItemTemplate` 模板将 `RowStyle` CSS 类分配给每个 Repeater 项，并将 `AlternatingRowStyle` CSS 类分配给每个交替的中继器项，如下所示：

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample9.aspx)]

同时，还可以向包含文本产品类别的输出添加标题行。 由于我们不知道生成的 `<table>` 将包含多少列，因此生成保证跨越所有列的标题行的最简单方法是使用*两个*`<table>`。 第一个 `<table>` 将包含两行标题行和一个包含第二个单行 `<table>` 的行，该行包含系统中每个类别的列。 也就是说，我们想要发出以下标记：

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample10.html)]

以下 `HeaderTemplate` 和 `FooterTemplate` 会产生所需的标记：

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-cs/samples/sample11.aspx)]

图18显示了这些更改后的中继器。

[![以背景色替代的类别列，并且包括标题行](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image48.png)

**图 18**：类别列以背景色替换并包括标题行（[单击以查看完全大小的图像](displaying-data-with-the-datalist-and-repeater-controls-cs/_static/image50.png)）

## <a name="summary"></a>摘要

尽管 GridView 控件可以轻松地对数据进行显示、编辑、删除、排序和分页，但其外观非常 boxy，类似于网格。 为了更好地控制外观，需要转到 DataList 或 Repeater 控件。 这两个控件都使用模板显示一组记录，而不是使用 BoundFields、CheckBoxFields 等。

DataList 呈现为 HTML `<table>`，默认情况下，在单个表行中显示每个数据源记录，就像使用单个 TemplateField 的 GridView 一样。 但我们将在以后的教程中看到，DataList 允许每个表行显示多条记录。 另一方面，中继器会严格发出其模板中指定的标记;它不会添加任何其他标记，因此通常用于在 `<table>` （如项目符号列表）中的 HTML 元素中显示数据。

尽管 DataList 和中继器在呈现的输出中提供了更大的灵活性，但它们缺乏了在 GridView 中发现的许多内置功能。 我们将在即将推出的教程中进行探讨，其中的一些功能可以无需太多的工作就重新插入，但请记住，使用 DataList 或中继器代替 GridView 会限制你可以使用的功能，而无需实现这些功能。提醒.

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Yaakov Ellis、Liz Shulok、Randy Schmidt 和 Stacy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一部分](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
