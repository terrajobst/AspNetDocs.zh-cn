---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
title: DataList 和 Repeater 中的自定义按钮（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将构建一个接口，该接口使用中继器列出系统中的类别，每个类别都提供一个按钮以显示其 associ 。
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 1afdb14d-6e49-4e1f-aead-2934730d472e
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: bc7e94e59226b739c2948434c1bfecb46b3d7856
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465350"
---
# <a name="custom-buttons-in-the-datalist-and-repeater-vb"></a>DataList 和 Repeater 中的自定义按钮 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_VB.exe)或[下载 PDF](custom-buttons-in-the-datalist-and-repeater-vb/_static/datatutorial46vb1.pdf)

> 在本教程中，我们将构建一个接口，该接口使用中继器列出系统中的类别，每个类别都提供一个按钮来使用 BulletedList 控件显示其关联的产品。

## <a name="introduction"></a>简介

在过去的十七个 DataList 和中继器教程中，我们创建了只读示例并编辑和删除了示例。 为了便于编辑和删除 DataList 中的功能，我们向 DataList s 添加了一些按钮，在单击该按钮时，该按钮 `ItemTemplate` 会导致回发并引发对应于按钮 s `CommandName` 属性的 DataList 事件。 例如，将一个按钮添加到 `CommandName` 属性值为 "编辑" 的 `ItemTemplate` 会导致 DataList `EditCommand` 在回发时激发;一个具有 `CommandName` 删除的将引发 `DeleteCommand`。

除了 "编辑" 和 "删除" 按钮外，DataList 和 Repeater 控件还可以包含按钮、LinkButtons 或 ImageButtons，单击该按钮时，将执行一些自定义服务器端逻辑。 在本教程中，我们将构建一个接口，该接口使用中继器来列出系统中的类别。 对于每个类别，中继器都将包含一个按钮，用于使用 BulletedList 控件显示与类别关联的产品（请参阅图1）。

[![单击 "显示产品" 链接会在项目符号列表中显示类别的产品](custom-buttons-in-the-datalist-and-repeater-vb/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image1.png)

**图 1**：单击 "显示产品" 链接可在项目符号列表中显示类别的产品（[单击以查看完全大小的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image3.png)）

## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>步骤1：添加自定义按钮教程网页

在我们介绍如何添加自定义按钮之前，首先请花点时间在我们的网站项目中创建 ASP.NET 页面，我们将在本教程中需要用到这些页面。 首先添加一个名为 `CustomButtonsDataListRepeater`的新文件夹。 接下来，将以下两个 ASP.NET 页面添加到该文件夹，确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `CustomButtons.aspx`

![为自定义按钮相关教程添加 ASP.NET 页](custom-buttons-in-the-datalist-and-repeater-vb/_static/image4.png)

**图 2**：为自定义按钮相关教程添加 ASP.NET 页

与在其他文件夹中一样，`CustomButtonsDataListRepeater` 文件夹中的 `Default.aspx` 会在其部分列出教程。 请记住，`SectionLevelTutorialListing.ascx` 用户控件提供此功能。 将此用户控件从解决方案资源管理器拖到页面 s 设计视图，以将其添加到 `Default.aspx`。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](custom-buttons-in-the-datalist-and-repeater-vb/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image5.png)

**图 3**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image7.png)）

最后，将页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，请在 DataList 和 Repeater `<siteMapNode>`后面添加以下标记：

[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample1.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧菜单现在包含用于编辑、插入和删除教程的项。

![站点映射现在包含用于自定义按钮教程的条目](custom-buttons-in-the-datalist-and-repeater-vb/_static/image8.png)

**图 4**：站点地图现在包含用于自定义按钮教程的条目

## <a name="step-2-adding-the-list-of-categories"></a>步骤2：添加类别列表

对于本教程，我们需要创建一个中继器，其中列出了所有类别以及 "显示产品" LinkButton，单击此项将在项目符号列表中显示关联的类别的产品。 首先，让我们创建一个简单的中继器来列出系统中的类别。 首先打开 `CustomButtonsDataListRepeater` 文件夹中的 "`CustomButtons.aspx`" 页。 将 Repeater 从工具箱拖到设计器上，并将其 `ID` 属性设置为 `Categories`。 接下来，从 Repeater 的智能标记创建新的数据源控件。 具体而言，将创建一个名为 `CategoriesDataSource` 的新 ObjectDataSource 控件，该控件从 `CategoriesBLL` 类 `GetCategories()` 方法中选择其数据。

[![将 ObjectDataSource 配置为使用 CategoriesBLL Class s GetCategories （）方法](custom-buttons-in-the-datalist-and-repeater-vb/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image9.png)

**图 5**：将 ObjectDataSource 配置为使用 `CategoriesBLL` 类 `GetCategories()` 方法（[单击以查看完全大小的映像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image11.png)）

与 DataList 控件不同，Visual Studio 根据数据源创建默认 `ItemTemplate`，必须手动定义中继器。 此外，必须以声明方式（即，在中继器 s 智能标记中没有 "编辑模板" 选项）创建和编辑中继器模板。

单击左下角的 "源" 选项卡，并添加一个 `ItemTemplate`，它在 `<h3>` 元素中显示类别的名称及其在段落标记中的说明;包括在每个类别之间显示水平标尺（`<hr />`）的 `SeparatorTemplate`。 另外添加一个 LinkButton，其 `Text` 属性设置为 "显示产品"。 完成这些步骤后，页面的声明性标记应如下所示：

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample2.aspx)]

图6显示了通过浏览器查看的页面。 列出了每个类别的名称和描述。 单击 "显示产品" 按钮会导致回发，但不会执行任何操作。

[![显示每个类别的名称和描述，以及显示产品 LinkButton](custom-buttons-in-the-datalist-and-repeater-vb/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image12.png)

**图 6**：显示了每个类别的名称和描述，以及显示产品 LinkButton （[单击查看完全大小的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image14.png)）

## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>步骤3：单击显示产品 LinkButton 时执行服务器端逻辑

如果单击 DataList 或 Repeater 中模板内的按钮、LinkButton 或 ImageButton，则会发生回发，并引发 DataList 或 Repeater `ItemCommand` 事件。 除了 `ItemCommand` 事件之外，如果按钮的 `CommandName` 属性设置为保留的字符串之一（删除、编辑、取消、更新或选择），DataList 控件也可能引发另一个更具体的事件，但 `ItemCommand` 事件*始终*激发。

当在 DataList 或中继器内单击某个按钮时，有时我们需要沿单击哪个按钮（如果控件中可能有多个按钮，例如 "编辑" 和 "删除" 按钮），以及其他一些信息（如单击了按钮的项的主键值）。 按钮、LinkButton 和 ImageButton 提供了两个属性，这些属性的值将传递到 `ItemCommand` 事件处理程序：

- `CommandName` 通常用于标识模板中的每个按钮的字符串
- `CommandArgument` 通常用于保存某些数据字段的值，例如主键值

对于本示例，请将 LinkButton s `CommandName` 属性设置为 ShowProducts，并使用 databinding 语法 `CategoryArgument='<%# Eval("CategoryID") %>'`将当前记录的主键值 `CategoryID` 绑定到 `CommandArgument` 属性。 指定这两个属性后，LinkButton 的声明性语法应如下所示：

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample3.aspx)]

单击该按钮时，将发生回发，并激发 DataList 或 Repeater `ItemCommand` 事件。 向事件处理程序传递按钮 s `CommandName` 和 `CommandArgument` 值。

为中继器 `ItemCommand` 事件创建事件处理程序，并记下传递到事件处理程序中的第二个参数（名为 `e`）。 此第二个参数的类型为[`RepeaterCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx) ，具有以下四个属性：

- `CommandArgument` 单击的按钮 `CommandArgument` 属性的值
- `CommandName` 按钮 `CommandName` 属性的值
- `CommandSource` 对单击的按钮控件的引用
- `Item` 对包含所单击按钮的[`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem.aspx)的引用;绑定到 Repeater 的每个记录均表现为 `RepeaterItem`

由于所选的类别 `CategoryID` 通过 `CommandArgument` 属性传入，因此，我们可以在 `ItemCommand` 事件处理程序中获取与所选类别关联的一组产品。 然后，可以将这些产品绑定到 `ItemTemplate` 中的 BulletedList 控件（我们尚未添加）。 接下来，我们将添加 BulletedList，在 `ItemCommand` 事件处理程序中引用该，并将其绑定到所选类别的产品集，我们将在步骤4中进行此操作。

> [!NOTE]
> 为 DataList `ItemCommand` 事件处理程序传递[`DataListCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx)类型的对象，该对象提供与 `RepeaterCommandEventArgs` 类相同的四个属性。

## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>步骤4：在项目符号列表中显示所选类别的产品

使用任意数量的控件，可以在 Repeater `ItemTemplate` 中显示所选类别的产品。 可以添加其他嵌套的中继器、DataList、DropDownList、GridView 等。 不过，由于我们想要将产品显示为项目符号列表，因此我们将使用 BulletedList 控件。 返回到 `CustomButtons.aspx` 页的声明性标记，将 BulletedList 控件添加到 Show Products LinkButton 之后的 `ItemTemplate` 中。 将 BulletedLists `ID` 设置为 `ProductsInCategory`。 BulletedList 显示通过 `DataTextField` 属性指定的数据字段的值;由于此控件将绑定产品信息，因此请将 `DataTextField` 属性设置为 `ProductName`。

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample4.aspx)]

在 `ItemCommand` 事件处理程序中，使用 `e.Item.FindControl("ProductsInCategory")` 引用此控件，并将其绑定到与所选类别关联的一组产品。

[!code-vb[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample5.vb)]

在 `ItemCommand` 事件处理程序中执行任何操作之前，首先应检查传入 `CommandName`的值。 由于在单击*任何*按钮时将触发 `ItemCommand` 事件处理程序，因此，如果模板中有多个按钮，则使用 `CommandName` 值来了解要执行的操作。 在此处检查 `CommandName` 是差异的，因为我们只有一个按钮，但这是一种很好的形式。 接下来，从 `CommandArgument` 属性中检索所选类别的 `CategoryID`。 然后，引用模板中的 BulletedList 控件并将其绑定到 `ProductsBLL` 类 s `GetProductsByCategoryID(categoryID)` 方法的结果。

在以前的教程中，使用了 DataList 内的按钮（例如[编辑和删除 datalist](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)中的数据），我们通过 `DataKeys` 集合确定了给定项的主键值。 尽管此方法非常适合用于 DataList，但 Repeater 没有 `DataKeys` 属性。 相反，我们必须使用另一种方法来提供主键值，例如通过按钮 s `CommandArgument` 属性，或将主键值分配给模板内的隐藏标签 Web 控件，并使用 `e.Item.FindControl("LabelID")`在 `ItemCommand` 事件处理程序中读取其值。

完成 `ItemCommand` 事件处理程序后，请花点时间在浏览器中测试此页。 如图7所示，单击 "显示产品" 链接会导致回发并在 BulletedList 中显示所选类别的产品。 此外，请注意，即使单击其他类别显示 "产品" 链接，也会保留此产品信息。

> [!NOTE]
> 如果要修改此报表的行为，以便一次只列出一种类别的产品，只需将 BulletedList 控件 `EnableViewState` 属性设置为 `False`。

[![BulletedList 用于显示所选类别的产品](custom-buttons-in-the-datalist-and-repeater-vb/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image15.png)

**图 7**： BulletedList 用于显示所选类别的产品（[单击以查看完全尺寸的图像](custom-buttons-in-the-datalist-and-repeater-vb/_static/image17.png)）

## <a name="summary"></a>摘要

DataList 和 Repeater 控件可以在其模板中包含任意数量的按钮、LinkButtons 或 ImageButtons。 当单击此类按钮时，将导致回发并引发 `ItemCommand` 事件。 若要将自定义服务器端操作与单击的按钮相关联，请为 `ItemCommand` 事件创建事件处理程序。 在此事件处理程序中，首先检查传入 `CommandName` 值以确定单击了哪个按钮。 还可以选择通过 "button `CommandArgument`" 属性提供其他信息。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Dennis Patterson 将。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](custom-buttons-in-the-datalist-and-repeater-cs.md)
