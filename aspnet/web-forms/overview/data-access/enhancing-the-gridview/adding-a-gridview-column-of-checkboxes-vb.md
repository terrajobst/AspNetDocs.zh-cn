---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
title: 添加 Checkbox 列（VB） |Microsoft Docs
author: rick-anderson
description: 本教程介绍如何向 GridView 控件添加复选框列，以便为用户提供一种直观的方法来选择 G 的多行 。
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 39253d05-75c0-41c7-b9d4-a6c58ecf69ce
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: c620b2eac5844d4030c1309b45e7d6a72d1f386a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78491882"
---
# <a name="adding-a-gridview-column-of-checkboxes-vb"></a>添加 GridView 复选框列 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_VB.exe)或[下载 PDF](adding-a-gridview-column-of-checkboxes-vb/_static/datatutorial52vb1.pdf)

> 本教程介绍如何向 GridView 控件添加复选框列，以便为用户提供一种直观的方式来选择多个 GridView 行。

## <a name="introduction"></a>简介

在前面的教程中，我们介绍了如何将一列单选按钮添加到 GridView，以便选择特定记录。 当用户限制为从网格中选择最多一个项时，单选按钮的列是合适的用户界面。 但有时，我们可能希望允许用户从网格中选取任意数量的项目。 例如，基于 Web 的电子邮件客户端通常使用 checkbox 列显示消息列表。 用户可以选择任意数量的消息，然后执行一些操作，例如将电子邮件移动到另一个文件夹或将其删除。

在本教程中，我们将了解如何添加复选框列以及如何确定回发时检查了哪些复选框。 具体而言，我们将构建一个示例，用于充分模拟基于 web 的电子邮件客户端用户界面。 本示例将包含一个分页的 GridView，其中列出了 `Products` 数据库表中的产品，每行包含一个复选框（请参阅图1）。 单击 "删除所选产品" 按钮后，将删除所选产品。

[每个产品行 ![都包含一个复选框](adding-a-gridview-column-of-checkboxes-vb/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image1.png)

**图 1**：每个产品行都包含一个复选框（[单击查看完全大小的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image2.png)）

## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>步骤1：添加列出产品信息的分页 GridView

在考虑如何添加 checkbox 列之前，首先要重点介绍支持分页的 GridView 中的产品。 首先打开 `EnhancedGridView` 文件夹中的 "`CheckBoxField.aspx`" 页，然后从 "工具箱" 中将一个 GridView 拖到设计器上，将其 `ID` 设置为 "`Products`"。 接下来，选择将 GridView 绑定到名为 `ProductsDataSource`的新 ObjectDataSource。 将 ObjectDataSource 配置为使用 `ProductsBLL` 类，调用 `GetProducts()` 方法返回数据。 由于此 GridView 将是只读的，因此请将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）"。

[![创建一个名为 ProductsDataSource 的新 ObjectDataSource](adding-a-gridview-column-of-checkboxes-vb/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image3.png)

**图 2**：创建名为 `ProductsDataSource` 的新 ObjectDataSource （[单击以查看完全大小的映像](adding-a-gridview-column-of-checkboxes-vb/_static/image4.png)）

[![使用 GetProducts （）方法配置 ObjectDataSource 以检索数据](adding-a-gridview-column-of-checkboxes-vb/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image5.png)

**图 3**：使用 `GetProducts()` 方法配置 ObjectDataSource 以检索数据（[单击以查看完全大小的映像](adding-a-gridview-column-of-checkboxes-vb/_static/image6.png)）

[![在 "更新"、"插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"](adding-a-gridview-column-of-checkboxes-vb/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image7.png)

**图 4**：将 "更新"、"插入" 和 "删除" 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的映像](adding-a-gridview-column-of-checkboxes-vb/_static/image8.png)）

完成 "配置数据源" 向导后，Visual Studio 将自动创建 BoundColumns，并为与产品相关的数据字段创建一个 CheckBoxColumn。 与上一教程中的操作相同，请删除除 `ProductName`、`CategoryName`和 `UnitPrice` BoundFields 的所有操作，并将 `HeaderText` 属性更改为 "产品"、"类别" 和 "价格"。 配置 `UnitPrice` BoundField，以便将其值设置为货币格式。 此外，通过选中智能标记中的 "启用分页" 复选框，将 GridView 配置为支持分页。

同时，还可以添加用于删除所选产品的用户界面。 将按钮 Web 控件添加到 GridView 下，并将其 `ID` 设置为 `DeleteSelectedProducts` 及其 `Text` 属性以删除所选产品。 在此示例中，我们只会显示一条消息，指出已删除的产品，而不是从数据库中实际删除产品。 为此，请在按钮的下面添加一个 "标签" Web 控件。 将其 ID 设置为 `DeleteResults`，清除其 `Text` 属性，并将其 `Visible` 和 `EnableViewState` 属性设置为 `False`。

进行这些更改后，GridView、ObjectDataSource、按钮和标签的声明性标记应类似于以下内容：

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample1.aspx)]

请花点时间查看浏览器中的页面（见图5）。 此时，应会看到前十种产品的名称、类别和价格。

[![列出了前十个产品的名称、类别和价格](adding-a-gridview-column-of-checkboxes-vb/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image9.png)

**图 5**：列出了前十个产品的名称、类别和价格（[单击查看全尺寸图像](adding-a-gridview-column-of-checkboxes-vb/_static/image10.png)）

## <a name="step-2-adding-a-column-of-checkboxes"></a>步骤2：添加复选框的列

由于 ASP.NET 2.0 包含一个 CheckBoxField，因此可能会认为它可以用于向 GridView 添加复选框的列。 遗憾的是，这种情况并非如此，因为 CheckBoxField 的设计目的是使用布尔数据字段。 也就是说，若要使用 CheckBoxField，必须指定基础数据字段，该字段的值将用于确定是否选中了呈现的复选框。 不能使用 CheckBoxField 来只包含一列未选中的复选框。

相反，我们必须添加 TemplateField，并将复选框 Web 控件添加到其 `ItemTemplate`。 继续并将 TemplateField 添加到 `Products` GridView，并使其成为第一个（最左侧）字段。 从 GridView s 智能标记中，单击 "编辑模板" 链接，然后将 "复选框" Web 控件从工具箱拖动到 `ItemTemplate`中。 将此复选框 `ID` 属性设置为 `ProductSelector`。

[![将名为 ProductSelector 的复选框 Web 控件添加到 TemplateField s ItemTemplate](adding-a-gridview-column-of-checkboxes-vb/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image11.png)

**图 6**：将名为 `ProductSelector` 的复选框 Web 控件添加到 TemplateField s `ItemTemplate` （[单击查看完全大小的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image12.png)）

添加 TemplateField 和 CheckBox Web 控件后，每行现在都包含一个复选框。 图7显示了在浏览器中查看 TemplateField 和 CheckBox 后的此页。

[每个产品行 ![现在包含一个复选框](adding-a-gridview-column-of-checkboxes-vb/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image13.png)

**图 7**：每个产品行现在都包含一个复选框（[单击查看完全尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image14.png)）

## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>步骤3：确定回发时检查了哪些复选框

此时，我们有一列复选框，但无法确定回发时检查了哪些复选框。 但是，当单击 "删除所选产品" 按钮时，我们需要知道选中了哪些复选框，才能删除这些产品。

GridView s [`Rows` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx)提供对 gridview 中的数据行的访问权限。 我们可以循环访问这些行，以编程方式访问 CheckBox 控件，然后查阅其 `Checked` 属性以确定复选框是否已选中。

为 `DeleteSelectedProducts` 按钮 Web 控件 `Click` 事件创建事件处理程序，并添加以下代码：

[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample2.vb)]

`Rows` 属性返回构成 GridView 数据行的 `GridViewRow` 实例的集合。 此处的 `For Each` 循环枚举此集合。 对于每个 `GridViewRow` 对象，均使用 `row.FindControl("controlID")`以编程方式访问第 s 行复选框。 如果选中该复选框，则将从 `DataKeys` 集合中检索对应的行 `ProductID` 值。 在此练习中，我们只是在 "`DeleteResults`" 标签中显示一条信息性消息，但在运行的应用程序中，我们将改为调用 `ProductsBLL` class s `DeleteProduct(productID)` 方法。

添加此事件处理程序后，单击 "删除所选产品" 按钮，此时将显示选定产品的 `ProductID`。

[![当单击 "删除所选产品" 按钮时，将列出所选产品 Productid](adding-a-gridview-column-of-checkboxes-vb/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image15.png)

**图 8**：单击 "删除所选产品" 按钮后，将列出 `ProductID` 的所选产品（[单击查看完全大小的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image16.png)）

## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>步骤4：添加全部检查并取消选中所有按钮

如果用户想要删除当前页面上的所有产品，则必须选中十个复选框。 通过添加 "全部选中" 按钮，可帮助加速此过程，在单击该按钮时，将选择网格中的所有复选框。 "全部取消选中" 按钮将同样有用。

将两个按钮 Web 控件添加到页面，并将其放置在 GridView 之上。 将第一个 `ID` 设置为 `CheckAll`，并将其 `Text` 属性设置为 "全部检查";将第二个 `ID` 设置为 `UncheckAll`，并将其 `Text` 属性设置为 "全部取消选中"。

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample3.aspx)]

接下来，在名为 `ToggleCheckState(checkState)` 的代码隐藏类中创建一个方法，该方法在调用时枚举 `Products` GridView s `Rows` 集合，并将每个 CheckBox 的 `Checked` 属性设置为传入*checkState*参数的值。

[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample4.vb)]

接下来，为 `CheckAll` 和 `UncheckAll` 按钮创建 `Click` 事件处理程序。 在 `CheckAll` s 事件处理程序中，只需调用 `ToggleCheckState(True)`;在 `UncheckAll`中，调用 `ToggleCheckState(False)`。

[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample5.vb)]

使用此代码时，单击 "全部选中" 按钮会导致回发并检查 GridView 中的所有复选框。 同样，单击 "取消选中所有" 会取消选中所有复选框。 图9显示选中 "全部选中" 按钮后的屏幕。

[![单击 "全部选中" 按钮将选中所有复选框](adding-a-gridview-column-of-checkboxes-vb/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image17.png)

**图 9**：单击 "全部选中" 按钮将选中所有复选框（[单击查看完全尺寸的图像](adding-a-gridview-column-of-checkboxes-vb/_static/image18.png)）

> [!NOTE]
> 显示复选框列时，选择或取消选择所有复选框的一种方法是通过标题行中的复选框。 而且，当前的 "全部检查"/"取消选中" 所有实现都需要回发。 不过，可以通过客户端脚本完全选中或取消选中这些复选框，从而提供快捷的用户体验。 若要浏览 "全部选中并取消选中所有内容" 复选框，以及有关使用客户端技术的讨论，请参阅[使用客户端脚本检查 GridView 中的所有复选框和 "全部选中](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx)" 复选框。

## <a name="summary"></a>摘要

如果需要让用户在继续操作之前从 GridView 中选择任意数量的行，则添加一个 checkbox 列就是一个选项。 正如我们在本教程中看到的那样，在 GridView 中包含一列复选框，这需要使用 CheckBox Web 控件添加 TemplateField。 通过使用 Web 控件（与在模板中直接注入模板中的操作一样），ASP.NET 会自动记住哪些复选框，且未在回发中检查。 我们还可以通过编程方式访问代码中的复选框，以确定是否选中了给定的复选框，或更改选中的状态。

本教程和最后一个教程介绍了如何向 GridView 添加行选择器列。 在下一教程中，我们将检查如何在多个工作中添加插入功能。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](adding-a-gridview-column-of-radio-buttons-vb.md)
> [下一页](inserting-a-new-record-from-the-gridview-s-footer-vb.md)
