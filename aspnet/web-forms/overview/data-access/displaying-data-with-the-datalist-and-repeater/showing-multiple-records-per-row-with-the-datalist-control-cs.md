---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
title: 显示每行包含 DataList 控件（C#）的多个记录 |Microsoft Docs
author: rick-anderson
description: 在本快速教程中，我们将探讨如何通过其 RepeatColumns 和 RepeatDirection 属性自定义 DataList 的布局。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: cf5acaf5-d4f6-4957-badc-b89956b285f3
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/showing-multiple-records-per-row-with-the-datalist-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 3280a7b5f28207d3e640a6480f47869ce19692bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78481106"
---
# <a name="showing-multiple-records-per-row-with-the-datalist-control-c"></a>使用 DataList 控件每行显示多条记录 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_31_CS.exe)或[下载 PDF](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/datatutorial31cs1.pdf)

> 在本快速教程中，我们将探讨如何通过其 RepeatColumns 和 RepeatDirection 属性自定义 DataList 的布局。

## <a name="introduction"></a>简介

过去两个教程中所示的 DataList 示例已将其数据源中的每条记录呈现为单列 HTML `<table>`中的一行。 虽然这是默认的 DataList 行为，但很容易自定义 DataList 显示，使数据源项分布在多行多行表中。 而且，可以将所有数据源项显示在一行多列 DataList 中。

我们可以通过其 `RepeatColumns` 自定义 DataList 布局，并 `RepeatDirection` 属性，这两个属性分别指示呈现的列数以及这些项是垂直布局还是水平布局。 例如，图1显示了一个 DataList，其中显示了包含三列的表中的产品信息。

[![DataList 显示每行三个产品](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image2.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image1.png)

**图 1**： DataList 显示每行三个产品（[单击查看完全尺寸的图像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image3.png)）

通过显示每行的多个数据源项，DataList 可以更有效地利用水平屏幕空间。 在本快速教程中，我们将探讨这两个 DataList 属性。

## <a name="step-1-displaying-product-information-in-a-datalist"></a>步骤1：在 DataList 中显示产品信息

在检查 `RepeatColumns` 和 `RepeatDirection` 属性之前，让我们先在页面上创建一个 DataList，其中列出了使用标准单列多行表格布局的产品信息。 在此示例中，让我们使用以下标记显示产品的名称、类别和价格：

[!code-html[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample1.html)]

我们已了解如何将数据绑定到前面示例中的 DataList，因此，我将快速执行这些步骤。 首先打开 `DataListRepeaterBasics` 文件夹中的 "`RepeatColumnAndDirection.aspx`" 页，然后从 "工具箱" 将 DataList 拖到设计器上。 从 DataList s 智能标记中，选择创建新的 ObjectDataSource，并将其配置为从 `ProductsBLL` 类 `GetProducts` 方法拉取其数据，从向导的插入、更新和删除选项卡中选择 "（无）" 选项。

创建新的 ObjectDataSource 并将其绑定到 DataList 后，Visual Studio 将自动创建一个 `ItemTemplate`，该显示每个产品数据字段的名称和值。 直接通过声明性标记或 DataList s 智能标记中的 "编辑模板" 选项调整 `ItemTemplate`，以使用上面所示的标记，将*产品名称*、*类别名称*和*价格*文本替换为使用适当的数据绑定语法将值分配给其 `Text` 属性的标签控件。 更新 `ItemTemplate`后，页面的声明性标记应如下所示：

[!code-aspx[Main](showing-multiple-records-per-row-with-the-datalist-control-cs/samples/sample2.aspx)]

请注意，我在 `UnitPrice`中包含了 `Eval` 数据绑定语法中的格式说明符，并将返回值的格式设置为货币-`Eval("UnitPrice", "{0:C}").`

请花点时间在浏览器中访问你的页面。 如图2所示，DataList 呈现为产品的单列多行表。

[默认情况下，DataList 将作为单列多行表呈现 ![](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image5.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image4.png)

**图 2**：默认情况下，DataList 呈现为单列多行表（[单击以查看完全大小的图像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image6.png)）

## <a name="step-2-changing-the-datalist-s-layout-direction"></a>步骤2：更改 DataList 布局方向

尽管 DataList 的默认行为是在单列多行表中垂直布局其项，但这种行为可以通过 DataList s [`RepeatDirection` 属性](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatdirection.aspx)轻松更改。 `RepeatDirection` 属性可以接受两个可能的值之一： `Horizontal` 或 `Vertical` （默认值）。

通过将 `RepeatDirection` 属性从 `Vertical` 改为 `Horizontal`，DataList 在单个行中呈现其记录，并为每个数据源项创建一个列。 为了说明这种效果，请在设计器中单击 DataList，然后从属性窗口将 `RepeatDirection` 属性从 `Vertical` 更改为 `Horizontal`。 在此之后，设计器会对 DataList 布局进行调整，从而创建单行的多列接口（请参阅图3）。

[![RepeatDirection 属性决定 DataList 项的布局方向](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image8.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image7.png)

**图 3**： `RepeatDirection` 属性决定 DataList 项的布局方向（[单击以查看完全大小的图像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image9.png)）

显示少量数据时，可以使用单行的多列表表来最大程度地提高屏幕空间。 不过，对于更大的数据量，单个行需要大量列，这会将可在屏幕上显示的那些项从右侧推送到右侧。 图4显示了单行 DataList 中呈现的产品。 由于有许多产品（超过80个），用户将需要向右滚动以查看有关每个产品的信息。

[![足够大的数据源，则单个列 DataList 需要水平滚动](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image11.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image10.png)

**图 4**：对于足够大的数据源，单列 DataList 需要水平滚动（[单击即可查看完全大小的图像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image12.png)）

## <a name="step-3-displaying-data-in-a-multi-column-multi-row-table"></a>步骤3：在多行多行表中显示数据

若要创建多列多行 DataList，需要将[`RepeatColumns` 属性](https://msdn.microsoft.com/system.web.ui.webcontrols.datalist.repeatcolumns.aspx)设置为要显示的列数。 默认情况下，`RepeatColumns` 属性设置为0，这将导致 DataList 显示单个行或列中的所有项（具体取决于 `RepeatDirection` 属性的值）。

对于我们的示例，让 s 显示每个表行的三个产品。 因此，将 `RepeatColumns` 属性设置为3。 做出此更改后，请花点时间在浏览器中查看结果。 如图5所示，产品现在已在一个三列多行表中列出。

[每行显示 ![三个产品](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image14.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image13.png)

**图 5**：三个产品按行显示（[单击以查看完全大小的图像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image15.png)）

`RepeatDirection` 属性影响 DataList 中项的布局方式。图5显示了 `RepeatDirection` 属性设置为 `Horizontal`的结果。 请注意，前三个产品 Chai、改动和 Aniseed Syrup 按从左到右、从上到下的顺序排列。 接下来的三个产品（从 Chef Anton s Cajun Seasoning 开始）显示在前三个下的行中。 但将 `RepeatDirection` 属性改回 `Vertical`，但是，从上到下、从左到右布局这些产品，如图6所示。

[在此 ![，产品是垂直布局的](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image17.png)](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image16.png)

**图 6**：此处的产品垂直布局（[单击以查看完全尺寸的图像](showing-multiple-records-per-row-with-the-datalist-control-cs/_static/image18.png)）

生成的表中显示的行数取决于绑定到 DataList 的记录总数。 准确地说，它是数据源项总数的上限除以 `RepeatColumns` 属性值。 由于 `Products` 表当前包含84个可被3整除的产品，因此有28行。 如果数据源中的项目数与 `RepeatColumns` 的属性值不能被整除，则最后一行或列将包含空白单元。 如果 `RepeatDirection` 设置为 `Vertical`，则最后一列将包含空单元格;如果 `Horizontal``RepeatDirection`，则最后一行将包含空单元。

## <a name="summary"></a>摘要

默认情况下，DataList 在单列多行表中列出其项，这将模拟具有单个 TemplateField 的 GridView 的布局。 尽管此默认布局是可接受的，但我们可通过每行显示多个数据源项来最大化屏幕空间。 完成这只是将 DataList s `RepeatColumns` 属性设置为每行显示的列数。 此外，DataList s `RepeatDirection` 属性可用于指示多列、多行表的内容是否应按从左到右、从上到下、从上到下、从左到右垂直布局。

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 John Suru。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](formatting-the-datalist-and-repeater-based-upon-data-cs.md)
> [下一页](nested-data-web-controls-cs.md)
