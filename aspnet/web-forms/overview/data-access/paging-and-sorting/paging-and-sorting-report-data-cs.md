---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
title: 分页和排序报表数据（C#） |Microsoft Docs
author: rick-anderson
description: 在联机应用程序中显示数据时，分页和排序是两种非常常见的功能。 在本教程中，我们将首先了解如何添加排序和 。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 811a6ef2-ec66-4c8e-a089-6f795056e288
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 2f77040316dadc218b8183e52628dc0cfe3b35a1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78502298"
---
# <a name="paging-and-sorting-report-data-c"></a>分页和排序报表数据 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_CS.exe)或[下载 PDF](paging-and-sorting-report-data-cs/_static/datatutorial24cs1.pdf)

> 在联机应用程序中显示数据时，分页和排序是两种非常常见的功能。 在本教程中，我们将首先了解如何向我们的报表添加排序和分页，然后我们将在以后的教程中进行构建。

## <a name="introduction"></a>简介

在联机应用程序中显示数据时，分页和排序是两种非常常见的功能。 例如，在在线书店搜索 ASP.NET 书籍时，可能会有数百个这类书籍，但是列出搜索结果的报告只列出每页的十个匹配项。 而且，结果可以按标题、价格、页计数、作者姓名等进行排序。 虽然过去的23个教程已经检查了如何构建各种报表（包括允许添加、编辑和删除数据的接口），但我们并未介绍如何对数据进行排序，并且仅在 DetailsView 和 FormView 上查看到的唯一分页示例控件.

在本教程中，我们将了解如何向报表添加排序和分页，只需选中几个复选框即可完成此操作。 遗憾的是，这一简单的实现有其缺点，即排序接口离开了所需的位，而分页例程却不是为高效地通过大型结果集进行分页而设计的。 将来的教程将探讨如何克服现成的分页和排序解决方案的限制。

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>步骤1：添加分页和排序教程网页

在开始本教程之前，首先请花点时间来添加本教程和接下来的三个 ASP.NET 所需的页面。 首先，在项目中创建一个名为 `PagingAndSorting`的新文件夹。 接下来，将以下五个 ASP.NET 页面添加到此文件夹，所有这些页面都配置为使用母版页 `Site.master`：

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`

![创建 PagingAndSorting 文件夹并添加教程 ASP.NET 页面](paging-and-sorting-report-data-cs/_static/image1.png)

**图 1**：创建 PagingAndSorting 文件夹并添加教程 ASP.NET 页面

接下来，打开 `Default.aspx` 页面，并将 `SectionLevelTutorialListing.ascx` 用户控件从 `UserControls` 文件夹拖到设计图面上。 此用户控件（我们在[母版页和站点导航](../introduction/master-pages-and-site-navigation-cs.md)教程中创建）枚举站点地图，并在项目符号列表中的当前部分显示这些教程。

![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](paging-and-sorting-report-data-cs/_static/image2.png)

**图 2**：将 SectionLevelTutorialListing 用户控件添加到 default.aspx

为了使项目符号列表显示我们要创建的分页和排序教程，我们需要将它们添加到站点地图。 打开 `Web.sitemap` 文件并在编辑、插入和删除站点地图节点标记之后添加以下标记：

[!code-xml[Main](paging-and-sorting-report-data-cs/samples/sample1.xml)]

![更新站点映射以包括新的 ASP.NET 页面](paging-and-sorting-report-data-cs/_static/image3.png)

**图 3**：更新站点映射以包括新的 ASP.NET 页面

## <a name="step-2-displaying-product-information-in-a-gridview"></a>步骤2：在 GridView 中显示产品信息

在实际实现分页和排序功能之前，首先让我们创建一个列出产品信息的标准不可排序、不可分页的 GridView。 这是我们以前在本系列教程中执行多次的任务，因此应熟悉这些步骤。 首先打开 "`SimplePagingSorting.aspx`" 页，然后将 "GridView" 控件从 "工具箱" 拖到设计器上，将其 `ID` 属性设置为 "`Products`"。 接下来，创建一个使用 ProductsBLL 类 `GetProducts()` 方法的新 ObjectDataSource 来返回所有产品信息。

![使用 GetProducts （）方法检索有关所有产品的信息](paging-and-sorting-report-data-cs/_static/image4.png)

**图 4**：使用 GetProducts （）方法检索有关所有产品的信息

由于此报表是只读报表，因此不需要将 ObjectDataSource `Insert()`、`Update()`或 `Delete()` 方法映射到相应的 `ProductsBLL` 方法;因此，从 "更新"、"插入" 和 "删除" 选项卡的下拉列表中选择 "（无）"。

![在 "更新"、"插入" 和 "删除" 选项卡的下拉列表中选择 "（无）" 选项](paging-and-sorting-report-data-cs/_static/image5.png)

**图 5**：在 "更新"、"插入" 和 "删除" 选项卡的下拉列表中选择 "（无）" 选项

接下来，让我们自定义 GridView 字段，以便仅显示产品名称、供应商、类别、价格和中止状态。 而且，可以随意进行任何字段级格式设置更改，例如调整 `HeaderText` 属性或将价格设置为货币格式。 完成这些更改后，GridView 的声明性标记应如下所示：

[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample2.aspx)]

图6显示了在浏览器中查看时的进度。 请注意，此页在一个屏幕中列出了所有产品，其中显示了每个产品的名称、类别、供应商、价格和废止状态。

[列出了每个产品 ![](paging-and-sorting-report-data-cs/_static/image7.png)](paging-and-sorting-report-data-cs/_static/image6.png)

**图 6**：列出了每个产品（[单击以查看完全大小的图像](paging-and-sorting-report-data-cs/_static/image8.png)）

## <a name="step-3-adding-paging-support"></a>步骤3：添加分页支持

在一个屏幕上列出*所有*产品可能导致用户浏览数据的信息过载。 为了使结果更易于管理，我们可以将数据分解为较小的数据页，并允许用户一次一页地单步执行数据。 若要实现此目的，只需选中 GridView s 智能标记的 "启用分页" 复选框（这会将 GridView [`AllowPaging` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx)设置为 `true`）。

[![选中 "启用分页" 复选框以添加分页支持](paging-and-sorting-report-data-cs/_static/image10.png)](paging-and-sorting-report-data-cs/_static/image9.png)

**图 7**：选中 "启用分页" 复选框以添加分页支持（[单击以查看完全大小的图像](paging-and-sorting-report-data-cs/_static/image11.png)）

启用分页将限制每页显示的记录数，并向 GridView 添加*分页接口*。 图7中所示的默认寻呼接口是一系列页码，允许用户从一页数据快速导航到另一页。 此分页接口应熟悉，因为在过去的教程中向 DetailsView 和 FormView 控件添加分页支持时，将会看到它。

DetailsView 和 FormView 控件都只显示每页一条记录。 但 GridView 会咨询其[`PageSize` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx)，以确定每页显示多少条记录（此属性默认值为10）。

可以使用以下属性自定义此 GridView、DetailsView 和 FormView s 分页接口：

- `PagerStyle` 指示分页接口的样式信息;可以指定 `BackColor`、`ForeColor`、`CssClass`、`HorizontalAlign`等设置。
- `PagerSettings` 包含可自定义分页接口功能的属性的一系列;`PageButtonCount` 指示分页界面中显示的数字页码的最大数目（默认值为10）;[`Mode` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx)指示分页接口的运行方式，并可将其设置为： 

    - `NextPrevious` 显示 "下一步" 和 "上一个" 按钮，允许用户一次向前或向后一页
    - 除了 "下一步" 和 "上一步" 按钮外，还包括 "第一个" 和 "最后一个" 按钮，使用户能够快速移动到第一个或最后一个数据页 `NextPreviousFirstLast`
    - `Numeric` 显示一系列页码，使用户能够立即跳转到任何页面
    - 除了页码外，`NumericFirstLast` 还包括第一个和最后一个按钮，使用户能够快速移动到第一个或最后一个数据页;仅当所有数字页码无法调整时才显示第一个/最后一个按钮

此外，GridView、DetailsView 和 FormView 都提供 `PageIndex` 和 `PageCount` 属性，分别指示正在查看的当前页面和数据的总页数。 `PageIndex` 属性的索引从0开始，这意味着查看数据的第一页时 `PageIndex` 将等于0。 另一方面，`PageCount`开始计数为1，这意味着 `PageIndex` 限制为0到 `PageCount - 1`之间的值。

让我们花点时间来改进 GridView 的分页界面的默认外观。 具体来说，让我们以浅灰色背景向右对齐分页界面。 不是直接通过 GridView `PagerStyle` 属性来设置这些属性，而是在名为 `PagerRowStyle` 的 `Styles.css` 中创建一个 CSS 类，然后通过我们的主题分配 `PagerStyle` 的 `CssClass` 属性。 首先打开 `Styles.css` 并添加以下 CSS 类定义：

[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample3.css)]

接下来，打开 `App_Themes` 文件夹内 `DataWebControls` 文件夹中的 `GridView.skin` 文件。 如我们在*母版页和站点导航*教程中所述，可以使用皮肤文件指定 Web 控件的默认属性值。 因此，增加现有设置以包括将 `PagerStyle` 的 `CssClass` 属性设置为 `PagerRowStyle`。 同时，让我们使用 `NumericFirstLast` 寻呼接口将寻呼接口配置为最多显示五个数值页面按钮。

[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>寻呼用户体验

图8显示了在选择了 GridView "启用分页" 复选框后通过浏览器访问的网页，并通过 `GridView.skin` 文件进行了 `PagerStyle` 和 `PagerSettings` 配置。 请注意，只显示了十条记录，分页接口指示我们正在查看数据的第一页。

[启用分页 ![，一次只显示部分记录](paging-and-sorting-report-data-cs/_static/image13.png)](paging-and-sorting-report-data-cs/_static/image12.png)

**图 8**：启用分页后，一次仅显示一小部分记录（[单击查看完全大小的图像](paging-and-sorting-report-data-cs/_static/image14.png)）

当用户单击分页界面中的某个页码时，回发可以和页面重新加载，其中显示了请求的页面记录。 图9显示了选择查看最后一个数据页后的结果。 请注意，最后一页只有一条记录;这是因为存在81个记录，这将导致每页有8个页面，加上一个包含单独记录的页面。

[单击页码 ![会导致回发并显示相应的记录子集](paging-and-sorting-report-data-cs/_static/image16.png)](paging-and-sorting-report-data-cs/_static/image15.png)

**图 9**：单击页码将导致回发并显示相应的记录子集（[单击查看完全大小的图像](paging-and-sorting-report-data-cs/_static/image17.png)）

## <a name="paging-s-server-side-workflow"></a>分页 s 服务器端工作流

当最终用户单击寻呼界面中的按钮时，将开始回发可以和以下服务器端工作流：

1. 激发 `PageIndexChanging` 事件的 GridView （或 DetailsView 或 FormView）
2. ObjectDataSource 重新请求 BLL 中的*所有*数据;GridView `PageIndex` 和 `PageSize` 属性值用于确定需要在 GridView 中显示从 BLL 返回的记录
3. 激发了 GridView `PageIndexChanged` 事件

在步骤2中，ObjectDataSource 重新请求其数据源中的所有数据。 这种形式的分页通常称为 "*默认分页*"，因为它在将 `AllowPaging` 属性设置为 `true`时默认使用分页行为。 使用默认分页时，数据 Web 控件 naively 将检索每个数据页的所有记录，即使只将部分记录呈现到发送到浏览器的 HTML 中。 除非通过 BLL 或 ObjectDataSource 来缓存数据库数据，否则对于具有很多并发用户的足够大的结果集或 web 应用程序，默认分页是不能使用的。

在下一教程中，我们将检查如何实现*自定义分页*。 通过自定义分页，可以专门指示 ObjectDataSource 仅检索请求的数据页所需的精确记录集。 如您所料，自定义分页极大地提高了通过大型结果集进行分页的效率。

> [!NOTE]
> 尽管在通过足够大的结果集或具有多个同时用户的站点进行分页时不适合使用默认分页，但请注意，自定义分页需要进行更多的更改和工作量来实现，但并不像选中复选框那样简单（默认情况下）分页）。 因此，对于小型和低流量网站，或在对相对较小的结果集进行分页时，默认分页可能是理想的选择，因为它的实现速度要快得多。

例如，如果我们知道，在我们的数据库中将永远不会超过100的产品，自定义分页所能获得的最小性能提升可能会抵消实现它所需的工作量。 然而，如果一天可能有数千或数十个产品，则*不*实现自定义分页会极大地影响应用程序的可伸缩性。

## <a name="step-4-customizing-the-paging-experience"></a>步骤4：自定义分页体验

数据 Web 控件提供了许多可用于增强用户分页体验的属性。 例如，`PageCount` 属性表示有多少页总数，而 `PageIndex` 属性指示当前访问的页，并且可以将其设置为快速将用户移动到特定页。 为了说明如何使用这些属性来改善用户的分页体验，让我们向页面中添加一个 "标签 Web 控件"，向用户通知他们当前正在访问的页面，以及允许用户快速跳转到任何给定页面的 DropDownList 控件.

首先，将 "标签" Web 控件添加到页面，将其 `ID` 属性设置为 "`PagingInformation`"，并清除其 `Text` 属性。 接下来，为 GridView `DataBound` 事件创建事件处理程序并添加以下代码：

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample5.cs)]

此事件处理程序将 `PagingInformation` 标签的 `Text` 属性分配给一条消息，告知用户其当前正在访问的页面 `Products.PageIndex + 1` 的总页数 `Products.PageCount` （我们将1添加到 `Products.PageIndex` 属性，因为 `PageIndex` 从0开始索引。） 我在 `DataBound` 事件处理程序中选择了 "分配此标签" `Text` 属性，而不是 `PageIndexChanged` 事件处理程序，因为每次将数据绑定到 GridView 时都会触发 `DataBound` 事件，而 `PageIndexChanged` 事件处理程序仅在页索引更改时激发。 如果 GridView 最初在第一页上绑定数据，则不会激发 `PageIndexChanging` 事件（而 `DataBound` 事件）。

使用此添加方法时，用户现在会显示一条消息，指示用户访问的页面以及数据的总页数。

[![显示当前页码和总页数](paging-and-sorting-report-data-cs/_static/image19.png)](paging-and-sorting-report-data-cs/_static/image18.png)

**图 10**：显示当前页码和总页数（[单击查看完全大小的图像](paging-and-sorting-report-data-cs/_static/image20.png)）

除了 "标签" 控件外，还可以添加一个 DropDownList 控件，该控件在选定的当前已查看页中列出 GridView 中的页码。 这里的思路是，用户只需从 DropDownList 中选择新的页面索引，就可以从当前页面快速跳转到另一个页面。 首先向设计器添加 DropDownList，将其 `ID` 属性设置为 `PageList` 并从其智能标记中检查 Enable AutoPostBack 选项。

接下来，返回 `DataBound` 事件处理程序并添加以下代码：

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample6.cs)]

此代码首先清除 `PageList` DropDownList 中的项。 这可能看起来是多余的，因为其中一项不会有要更改的页数，而其他用户可能同时使用系统、添加或删除 `Products` 表中的记录。 此类插入或删除操作可能会改变数据页的数目。

接下来，我们需要再次创建页码，并将映射到当前 GridView `PageIndex` 默认情况下处于选中状态。 我们使用从0到 `PageCount - 1`的循环来完成此项工作，在每次迭代中添加新 `ListItem`，并将其 `Selected` 属性设置为 true （如果当前迭代索引等于 GridView 的 `PageIndex` 属性）。

最后，我们需要为 DropDownList s `SelectedIndexChanged` 事件创建事件处理程序，每次用户从列表中选取不同项时都会触发此事件。 若要创建此事件处理程序，只需在设计器中双击 DropDownList，然后添加以下代码：

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample7.cs)]

如图11所示，仅更改 GridView `PageIndex` 属性会导致将数据重新绑定到 GridView。 在 GridView `DataBound` 事件处理程序中，选择相应的 DropDownList `ListItem`。

[选择页面6下拉列表项时，![会自动将用户转到第六页](paging-and-sorting-report-data-cs/_static/image22.png)](paging-and-sorting-report-data-cs/_static/image21.png)

**图 11**：选择页面6下拉列表项时，自动将用户转到第六页（[单击以查看完全大小的图像](paging-and-sorting-report-data-cs/_static/image23.png)）

## <a name="step-5-adding-bi-directional-sorting-support"></a>步骤5：添加双向排序支持

添加双向排序支持非常简单，只需在 "GridView s" 智能标记中检查 "启用排序" 选项（这会将 GridView [`AllowSorting` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx)设置为 `true`）即可。 这会以 LinkButtons 的形式呈现 GridView 字段的每个标头，在单击时，将导致回发，并按升序返回按被单击的列排序的数据。 再次单击相同的标头 LinkButton 会按降序对数据重新排序。

> [!NOTE]
> 如果使用的是自定义的数据访问层而不是类型化的数据集，则在 GridView s 智能标记中可能没有启用排序选项。 只有绑定到本机支持排序的数据源的 GridViews 才能使用此复选框。 类型化数据集提供了现成的排序支持，因为 ADO.NET DataTable 提供了一个 `Sort` 方法，在调用该方法时，会使用指定的条件对 DataTable s Datarow 进行排序。

如果 DAL 未返回本机支持排序的对象，则需要将 ObjectDataSource 配置为将排序信息传递给业务逻辑层，以便对数据进行排序或将数据按 DAL 排序。 在将来的教程中，我们将探讨如何在业务逻辑和数据访问层对数据进行排序。

排序 LinkButtons 呈现为 HTML 超链接，其当前颜色（对于已访问链接为蓝色，已访问链接为深红色）与标题行的背景色冲突。 而是使所有标题行链接都以白色显示，而不考虑它们是否已被访问。 这可以通过将以下内容添加到 `Styles.css` 类来实现：

[!code-css[Main](paging-and-sorting-report-data-cs/samples/sample8.css)]

此语法指示在使用 HeaderStyle 类的元素内显示这些超链接时，使用白色文本。

完成此 CSS 添加后，当通过浏览器访问页面时，屏幕应类似于图12。 具体而言，图12显示了在单击 "价格字段" 标题链接后的结果。

[![结果已按单价升序排序](paging-and-sorting-report-data-cs/_static/image25.png)](paging-and-sorting-report-data-cs/_static/image24.png)

**图 12**：按单价升序对结果进行排序（[单击以查看完全大小的图像](paging-and-sorting-report-data-cs/_static/image26.png)）

## <a name="examining-the-sorting-workflow"></a>检查排序工作流

BoundField、CheckBoxField、TemplateField 等所有 GridView 字段都有一个 `SortExpression` 属性，该属性指示在单击该字段的排序标头链接时，应用于对数据进行排序的表达式。 GridView 还具有一个 `SortExpression` 属性。 单击排序标头 LinkButton 时，GridView 将 `SortExpression` 值分配给该字段的 `SortExpression` 属性。 接下来，将从 ObjectDataSource 重新检索数据并根据 GridView 的 `SortExpression` 属性对数据进行排序。 以下列表详细说明了当最终用户在 GridView 中对数据进行排序时发生的步骤顺序：

1. 激发 GridView s[排序事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx)
2. GridView s [`SortExpression` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)设置为单击排序头 LinkButton 的字段的 `SortExpression`
3. ObjectDataSource 从 BLL 重新检索所有数据，然后使用 GridView `SortExpression` 来对数据进行排序。
4. GridView `PageIndex` 属性重置为0，这意味着在排序时，用户将返回到第一页数据（假设已实现分页支持）
5. 激发了 GridView [`Sorted` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx)

与默认分页一样，默认排序选项会重新从 BLL 中检索*所有*记录。 如果在没有分页的情况下使用排序或对默认分页使用排序，则没有办法避免此性能下降（数据库数据的缓存较短）。 不过，正如我们将在将来的教程中看到的那样，可以在使用自定义分页时有效地对数据进行排序。

当通过 GridView s 智能标记的下拉列表将 ObjectDataSource 绑定到 GridView 时，每个 GridView 字段都会自动将其 `SortExpression` 属性分配给 `ProductsRow` 类中的数据字段的名称。 例如，`ProductName` BoundField s `SortExpression` 设置为 `ProductName`，如以下声明性标记中所示：

[!code-aspx[Main](paging-and-sorting-report-data-cs/samples/sample9.aspx)]

可以配置字段，以便无法通过清除其 `SortExpression` 属性（将其分配给空字符串）来对其进行排序。 为了说明这一点，假设我们不想让客户按价格对产品进行排序。 `UnitPrice` BoundField s `SortExpression` 属性可以从声明性标记中删除，也可以通过 "字段" 对话框（可通过单击 GridView s 智能标记中的 "编辑列" 链接来访问）。

![结果已按单价升序排序](paging-and-sorting-report-data-cs/_static/image27.png)

**图 13**：按单价升序对结果进行排序

为 `UnitPrice` BoundField 删除 `SortExpression` 属性后，标头将呈现为文本而不是链接，从而阻止用户按价格对数据进行排序。

[![通过删除 SortExpression 属性，用户将不再能够按价格对产品进行排序](paging-and-sorting-report-data-cs/_static/image29.png)](paging-and-sorting-report-data-cs/_static/image28.png)

**图 14**：删除 SortExpression 属性后，用户就不能再按价格对产品进行排序（[单击查看完全大小的图像](paging-and-sorting-report-data-cs/_static/image30.png)）

## <a name="programmatically-sorting-the-gridview"></a>以编程方式对 GridView 排序

还可以使用 GridView [`Sort` 方法](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)以编程方式对 gridview 的内容进行排序。 只需传入 `SortExpression` 值以便按[`SortDirection`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) （`Ascending` 或 `Descending`）进行排序，并且将对 GridView 的数据进行重新排序。

假设我们关闭了 `UnitPrice` 排序的原因，因为我们担心我们的客户只需购买价格最低的产品。 但是，我们想要鼓励他们购买最昂贵的产品，因此，我们希望他们能够按价格对产品进行排序，而只需从最昂贵的价格对产品进行排序。

若要实现此目的，请将按钮 Web 控件添加到页，将其 `ID` 属性设置为 `SortPriceDescending`，并将其 `Text` 属性设置为按价格排序。 接下来，通过双击设计器中的 "按钮" 控件，为按钮 s `Click` 事件创建事件处理程序。 将以下代码添加到此事件处理程序：

[!code-csharp[Main](paging-and-sorting-report-data-cs/samples/sample10.cs)]

单击此按钮会将用户返回到第一页，其中包含按价格排序的产品，从最昂贵到最昂贵的产品（见图15）。

[单击按钮 ![按最昂贵到最小](paging-and-sorting-report-data-cs/_static/image32.png)](paging-and-sorting-report-data-cs/_static/image31.png)

**图 15**：单击按钮按最高到最低的顺序排列产品（[单击以查看完全尺寸的图像](paging-and-sorting-report-data-cs/_static/image33.png)）

## <a name="summary"></a>摘要

在本教程中，我们介绍了如何实现默认分页和排序功能，这两者都与选中复选框一样简单！ 当用户通过数据对数据进行排序时，类似的工作流将：

1. 回发可以
2. 引发数据 Web 控件的预级别事件（`PageIndexChanging` 或 `Sorting`）
3. 所有数据都由 ObjectDataSource 重新检索
4. 引发级别的数据 Web 控件后期事件（`PageIndexChanged` 或 `Sorted`）

虽然实现基本分页和排序非常简单，但必须显然，才能利用更有效的自定义分页或进一步增强分页或排序接口。 将来的教程将探讨这些主题。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [下一部分](efficiently-paging-through-large-amounts-of-data-cs.md)
