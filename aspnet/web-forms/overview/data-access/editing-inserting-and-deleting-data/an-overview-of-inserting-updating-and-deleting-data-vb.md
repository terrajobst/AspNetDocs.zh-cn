---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
title: 插入、更新和删除数据概述（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何将 ObjectDataSource 的 Insert （）、Update （）和 Delete （）方法映射到 BLL 类的方法，以及如何配置 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 35b40b8f-2ca8-4ab3-9c19-f361a91a3647
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 79491118ba1cbbc8c1b67ca9646a817d941f17ba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78493838"
---
# <a name="an-overview-of-inserting-updating-and-deleting-data-vb"></a>插入、更新和删除数据概述（VB）

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_VB.exe)或[下载 PDF](an-overview-of-inserting-updating-and-deleting-data-vb/_static/datatutorial16vb1.pdf)

> 在本教程中，我们将了解如何将 ObjectDataSource 的 Insert （）、Update （）和 Delete （）方法映射到 BLL 类的方法，以及如何配置 GridView、DetailsView 和 FormView 控件以提供数据修改功能。

## <a name="introduction"></a>简介

在过去的几个教程中，我们已探讨了如何使用 GridView、DetailsView 和 FormView 控件在 ASP.NET 页中显示数据。 这些控件只使用提供给它们的数据。 通常，这些控件通过使用数据源控件（如 ObjectDataSource）来访问数据。 我们已了解 ObjectDataSource 如何充当 ASP.NET 页与基础数据之间的代理。 当 GridView 需要显示数据时，它将调用其 ObjectDataSource `Select()` 方法，该方法反过来从我们的业务逻辑层（BLL）调用一个方法，该方法在相应的数据访问层（DAL） TableAdapter 中调用一个方法，后者反过来将 `SELECT` 查询发送到 Northwind 数据库。

请记住，当我们在[第一个教程](../introduction/creating-a-data-access-layer-cs.md)中创建 DAL 中的 tableadapter 时，Visual Studio 会自动添加用于从基础数据库表中插入、更新和删除数据的方法。 此外，在[创建业务逻辑层](../introduction/creating-a-business-logic-layer-vb.md)时，我们在 BLL 中设计了一些方法，这些方法向下调用这些数据修改 DAL 方法。

除了其 `Select()` 方法，ObjectDataSource 还具有 `Insert()`、`Update()`和 `Delete()` 方法。 与 `Select()` 方法一样，这三种方法都可以映射到基础对象中的方法。 配置为插入、更新或删除数据时，GridView、DetailsView 和 FormView 控件提供了一个用于修改基础数据的用户界面。 此用户界面调用 ObjectDataSource 的 `Insert()`、`Update()`和 `Delete()` 方法，然后调用基础对象的关联方法（请参阅图1）。

[![ObjectDataSource 的 Insert （）、Update （）和 Delete （）方法在 BLL 中充当代理](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image1.png)

**图 1**： ObjectDataSource 的 `Insert()`、`Update()`和 `Delete()` 方法充当 BLL 的代理（[单击以查看完全大小的映像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image3.png)）

在本教程中，我们将了解如何将 ObjectDataSource 的 `Insert()`、`Update()`和 `Delete()` 方法映射到 BLL 中的类的方法，以及如何配置 GridView、DetailsView 和 FormView 控件以提供数据修改功能。

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>步骤1：创建 Insert、Update 和 Delete 教程网页

在开始探索如何插入、更新和删除数据之前，首先请花点时间在我们的网站项目中创建 ASP.NET 页面，我们将在本教程和下几个页面中创建这些页面。 首先添加一个名为 `EditInsertDelete`的新文件夹。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![为与数据修改相关的教程添加 ASP.NET 页](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image4.png)

**图 2**：为与数据修改相关的教程添加 ASP.NET 页

与在其他文件夹中一样，`EditInsertDelete` 文件夹中的 `Default.aspx` 会在其部分列出教程。 请记住，`SectionLevelTutorialListing.ascx` 用户控件提供此功能。 因此，通过将此用户控件从解决方案资源管理器拖到页面的设计视图上，将其添加到 `Default.aspx`。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image5.png)

**图 3**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image7.png)）

最后，将页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，在自定义格式设置之后添加以下标记 `<siteMapNode>`：

[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample1.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧菜单现在包含用于编辑、插入和删除教程的项。

![站点映射现在包含用于编辑、插入和删除教程的条目](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image8.png)

**图 4**：站点地图现在包含用于编辑、插入和删除教程的条目

## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>步骤2：添加和配置 ObjectDataSource 控件

由于 GridView、DetailsView 和 FormView 各自的数据修改功能和布局不同，因此让我们单独检查每个项。 不过，只需创建所有三个控件示例都可以共享的单个 ObjectDataSource，而不是让每个控件使用其自己的 ObjectDataSource。

打开 "`Basics.aspx`" 页，将 "ObjectDataSource" 从工具箱拖到设计器上，并单击其智能标记中的 "配置数据源" 链接。 由于 `ProductsBLL` 是唯一提供编辑、插入和删除方法的 BLL 类，因此请将 ObjectDataSource 配置为使用此类。

[![将 ObjectDataSource 配置为使用 ProductsBLL 类](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image9.png)

**图 5**：将 ObjectDataSource 配置为使用 `ProductsBLL` 类（[单击以查看完全大小的映像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image11.png)）

在下一屏幕中，可以通过选择相应的选项卡，然后从下拉列表中选择方法，指定将 `ProductsBLL` 类的哪些方法映射到 ObjectDataSource 的 `Select()`、`Insert()`、`Update()`和 `Delete()`。 图6（现在应熟悉）将 ObjectDataSource 的 `Select()` 方法映射到 `ProductsBLL` 类的 `GetProducts()` 方法。 通过从顶部的列表中选择相应的选项卡，可以配置 `Insert()`、`Update()`和 `Delete()` 方法。

[![让 ObjectDataSource 返回所有产品](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image12.png)

**图 6**： ObjectDataSource 返回所有产品（[单击以查看完全大小的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image14.png)）

图7、8和9显示了 ObjectDataSource 的 "更新"、"插入" 和 "删除" 选项卡。 配置这些选项卡，以便 `Insert()`、`Update()`和 `Delete()` 方法分别调用 `ProductsBLL` 类的 `UpdateProduct`、`AddProduct`和 `DeleteProduct` 方法。

[![将 ObjectDataSource 的 Update （）方法映射到 ProductBLL 类的 UpdateProduct 方法](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image15.png)

**图 7**：将 ObjectDataSource 的 `Update()` 方法映射到 `ProductBLL` 类的 `UpdateProduct` 方法（[单击以查看完全大小的映像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image17.png)）

[![将 ObjectDataSource 的 Insert （）方法映射到 ProductBLL 类的 AddProduct 方法](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image18.png)

**图 8**：将 ObjectDataSource 的 `Insert()` 方法映射到 `ProductBLL` 类的添加 `Product` 方法（[单击以查看完全大小的映像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image20.png)）

[![将 ObjectDataSource 的 Delete （）方法映射到 ProductBLL 类的 DeleteProduct 方法](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image21.png)

**图 9**：将 ObjectDataSource 的 `Delete()` 方法映射到 `ProductBLL` 类的 `DeleteProduct` 方法（[单击以查看完全大小的映像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image23.png)）

您可能已注意到，"更新"、"插入" 和 "删除" 选项卡中的下拉列表已经选择了这些方法。 这是因为我们使用 `DataObjectMethodAttribute` 来修饰 `ProductsBLL`的方法。 例如，DeleteProduct 方法具有以下签名：

[!code-vb[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample2.vb)]

`DataObjectMethodAttribute` 特性指示每个方法的用途，无论该方法是用于选择、插入、更新或删除，还是为默认值。 如果在创建 BLL 类时省略了这些属性，则需要从 "更新"、"插入" 和 "删除" 选项卡中手动选择方法。

在确保将适当的 `ProductsBLL` 方法映射到 ObjectDataSource 的 `Insert()`、`Update()`和 `Delete()` 方法之后，单击 "完成" 以完成向导。

## <a name="examining-the-objectdatasources-markup"></a>检查 ObjectDataSource 的标记

通过其向导配置 ObjectDataSource 后，请切换到 "源" 视图以检查生成的声明性标记。 `<asp:ObjectDataSource>` 标记指定基础对象以及要调用的方法。 此外，还有 `DeleteParameters`、`UpdateParameters`和 `InsertParameters`，它们映射到 `ProductsBLL` 类的 `AddProduct`、`UpdateProduct`和 `DeleteProduct` 方法的输入参数：

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample3.aspx)]

ObjectDataSource 为其关联的方法包含每个输入参数的参数，如同在 ObjectDataSource 配置为调用需要输入参数的 select 方法（如 `GetProductsByCategoryID(categoryID)`）时提供 `SelectParameter` 的列表。 我们很快就会看到，这些 `DeleteParameters`、`UpdateParameters`和 `InsertParameters` 的值是在调用 ObjectDataSource 的 `Insert()`、`Update()`或 `Delete()` 方法之前由 GridView、DetailsView 和 FormView 自动设置的。 还可以根据需要以编程方式设置这些值，因为我们将在以后的教程中进行讨论。

使用向导配置为 ObjectDataSource 的一个副作用是，Visual Studio 会将[OldValuesParameterFormatString 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx)设置为 `original_{0}`。 此属性值用于包括正在编辑的数据的原始值，在两种情况下非常有用：

- 如果编辑记录时，用户可以更改主键值。 在这种情况下，必须提供新的主键值和原始主键值，才能找到具有原始主键值的记录，并相应地更新其值。
- 使用乐观并发时。 乐观并发是一项技术，可确保两个同时进行的用户不会覆盖另一项更改，并在以后的教程中提供主题。

`OldValuesParameterFormatString` 属性指示基础对象的更新和删除方法中的输入参数的名称，这些值用于原始值。 当我们探索开放式并发时，我们将更详细地讨论此属性及其目的。 但现在我会将其引入，因为 BLL 的方法不需要原始值，因此我们必须删除此属性。 如果将 `OldValuesParameterFormatString` 属性设置为默认值（`{0}`）以外的任何值，则当数据 Web 控件尝试调用 ObjectDataSource 的 `Update()` 或 `Delete()` 方法时，将会导致错误，因为 ObjectDataSource 尝试同时传入指定的 `UpdateParameters` 或 `DeleteParameters`，以及原始值参数。

如果这不是很明显，别担心，我们会在以后的教程中检查此属性及其实用工具。 现在，只需确保完全从声明性语法中删除此属性声明，或将该值设置为默认值（{0}）。

> [!NOTE]
> 如果只是从设计视图的属性窗口中清除 `OldValuesParameterFormatString` 属性值，则该属性仍将在声明性语法中存在，但会设置为空字符串。 遗憾的是，这仍会导致前面讨论相同的问题。 因此，从声明性语法中删除完全相同的属性，或者从属性窗口中，将该值设置为默认值，`{0}`。

## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>步骤3：添加数据 Web 控件并对其进行配置以进行数据修改

一旦将 ObjectDataSource 添加到页面并进行了配置，我们就可以将数据 Web 控件添加到页面以显示数据，并提供一种方法供最终用户修改。 我们将单独探讨 GridView、DetailsView 和 FormView，因为这些数据 Web 控件的数据修改功能和配置不同。

正如我们将在本文的剩余部分中看到的那样，通过 GridView、DetailsView 和 FormView 控件添加非常基本的编辑、插入和删除支持实际上与选中几个复选框一样简单。 现实世界中有许多微妙之处和 edge 事例，这使得提供此类功能比只需点击和单击更多。 不过，本教程只重点介绍如何证明简单的数据修改功能。 未来的教程将探讨无疑会在实际设置中出现的问题。

## <a name="deleting-data-from-the-gridview"></a>从 GridView 中删除数据

首先，将 GridView 从工具箱拖到设计器上。 接下来，在 GridView 的智能标记的下拉列表中选择它，将其绑定到 GridView。 此时，GridView 的声明性标记将为：

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample4.aspx)]

通过其智能标记将 GridView 绑定到 ObjectDataSource 有两个优点：

- 为 ObjectDataSource 返回的每个字段自动创建 BoundFields 和 CheckBoxFields。 此外，基于基础字段的元数据设置 BoundField 和 CheckBoxField 属性。 例如，`ProductID`、`CategoryName`和 `SupplierName` 字段在 `ProductsDataTable` 中被标记为只读，因此在编辑时不能更新。 为此，这些 BoundFields 的[ReadOnly 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx)设置为 `True`。
- [DataKeyNames 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx)将分配给基础对象的主键字段。 当使用 GridView 编辑或删除数据时，这一点非常重要，因为此属性指示唯一标识每条记录的一个或多个字段。 有关 `DataKeyNames` 属性的详细信息，请参阅有关详细信息，请参阅[使用可选的 Master GridView DetailView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)教程。

尽管 GridView 可以通过属性窗口或声明性语法绑定到 ObjectDataSource，但这样做需要你手动添加适当的 BoundField 和 `DataKeyNames` 标记。

GridView 控件为行级编辑和删除提供内置支持。 将 GridView 配置为支持删除将添加 "删除" 按钮的列。 当最终用户单击特定行的 "删除" 按钮时，将执行以下步骤：

1. 已分配 ObjectDataSource 的 `DeleteParameters` 值
2. 将调用 ObjectDataSource 的 `Delete()` 方法，并删除指定的记录
3. GridView 通过调用其 `Select()` 方法将自身重新绑定到 ObjectDataSource

分配给 `DeleteParameters` 的值是单击 "删除" 按钮的行的 `DataKeyNames` 字段的值。 因此，必须正确设置 GridView 的 `DataKeyNames` 属性。 如果缺少此值，则会在步骤1中为 `DeleteParameters` 分配 `Nothing` 值，而不会导致步骤2中的任何已删除的记录。

> [!NOTE]
> `DataKeys` 集合存储在 GridView 的控件状态中，这意味着，即使已禁用 GridView 的视图状态，也会在回发时记住 `DataKeys` 值。 但是，对于支持编辑或删除的 GridViews （默认行为），视图状态保持为启用状态是非常重要的。 如果将 GridView `EnableViewState` 属性设置为 "`false`，则编辑和删除行为将适用于单个用户，但是，如果存在并发用户删除数据，则这些并发用户可能会意外删除或编辑他们不打算的记录。 有关详细信息，请参阅我的博客文章[： ASP.NET 2.0 GridViews/DetailsView/FormViews 上支持编辑和/删除以及禁用了其视图状态的并发问题](http://scottonwriting.net/sowblog/posts/10054.aspx)。

同样的警告同样适用于 DetailsViews 和 FormViews。

若要将删除功能添加到 GridView，只需切换到其智能标记，并选中 "启用删除" 复选框。

![选中 "启用删除" 复选框](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image24.png)

**图 10**：选中 "启用删除" 复选框

选中智能标记中的 "启用删除" 复选框会将 CommandField 添加到 GridView。 CommandField 在 GridView 中呈现一列，其中包含用于执行以下一项或多项任务的按钮：选择记录、编辑记录和删除记录。 我们以前在[使用可选的 Master GridView 和详细信息 DetailView](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)教程中，通过使用可选的 master GridView 选择记录 CommandField 操作。

CommandField 包含许多 `ShowXButton` 属性，这些属性指示在 CommandField 中显示哪一系列按钮。 选中 "启用删除" 复选框，即已将 `ShowDeleteButton` 属性 `True` 的 CommandField 添加到 GridView 的列集合中。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample5.aspx)]

此时，相信这一点，我们已将删除支持添加到 GridView 中！ 如图11所示，当通过浏览器访问此页时，将显示一列 "删除" 按钮。

[![CommandField 添加了 "删除" 按钮的列](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image25.png)

**图 11**： CommandField 添加了 "删除" 按钮的列（[单击以查看完全大小的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image27.png)）

如果你是从头开始构建本教程，则在测试此页面时单击 "删除" 按钮将引发异常。 继续阅读以了解为何会引发这些异常以及如何修复它们。

> [!NOTE]
> 如果使用本教程附带的下载内容，则这些问题已考虑到。 不过，我建议您通读下面列出的详细信息，以帮助确定可能出现的问题以及合适的解决方法。

如果尝试删除某个产品时收到一个异常，其消息类似于 "*ObjectDataSource" ObjectDataSource1 "找不到具有参数的非泛型方法 ' DeleteProduct '： productID，原始\_productID*"，则可能是忘记从 ObjectDataSource 中删除 `OldValuesParameterFormatString` 属性。 指定 `OldValuesParameterFormatString` 属性后，ObjectDataSource 尝试同时将 `productID` 和 `original_ProductID` 输入参数传入 `DeleteProduct` 方法。 但 `DeleteProduct`仅接受单个输入参数，从而引发异常。 如果删除 `OldValuesParameterFormatString` 属性（或将其设置为 `{0}`），则将指示 ObjectDataSource 不尝试传入原始输入参数。

[![确保已清除 OldValuesParameterFormatString 属性](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image28.png)

**图 12**：确保已清除 `OldValuesParameterFormatString` 属性（[单击以查看完全大小的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image30.png)）

即使您已删除 `OldValuesParameterFormatString` 属性，但在尝试删除包含以下消息的产品时仍会出现异常： "*delete 语句与引用约束的 FK\_Order\_详细信息\_产品"* 。Northwind 数据库包含 `Order Details` 和 `Products` 表之间的外键约束，这意味着，如果 `Order Details` 表中有一个或多个记录，则无法从系统中删除该产品。 由于 Northwind 数据库中的每个产品在 `Order Details`中至少有一条记录，因此在我们首次删除该产品的关联订单详细信息记录之前，我们无法删除任何产品。

[![Foreign Key 约束禁止删除产品](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image31.png)

**图 13**：外键约束禁止删除产品（[单击查看完全尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image33.png)）

对于本教程，我们只需删除 `Order Details` 表中的所有记录。 在实际应用程序中，我们需要：

- 有另一个用于管理订单详细信息的屏幕
- 增加 `DeleteProduct` 方法，使其包含用于删除指定产品的订单详细信息的逻辑
- 修改由 TableAdapter 使用的 SQL 查询，以包括删除指定产品的订单详细信息

只需从 `Order Details` 表中删除所有记录即可规避外键约束。 在 Visual Studio 中转到服务器资源管理器，右键单击 "`NORTHWND.MDF`" 节点，然后选择 "新建查询"。 然后，在查询窗口中运行以下 SQL 语句： `DELETE FROM [Order Details]`

[![从订单详细信息表中删除所有记录](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image34.png)

**图 14**：从 `Order Details` 表中删除所有记录（[单击以查看完全大小的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image36.png)）

清除 `Order Details` 表后，单击 "删除" 按钮将删除该产品而不发生错误。 如果单击 "删除" 按钮不会删除该产品，请检查以确保 GridView 的 `DataKeyNames` 属性设置为主键字段（`ProductID`）。

> [!NOTE]
> 单击 "删除" 按钮时，回发可以并删除记录。 这可能很危险，因为很容易意外地单击错误行的 "删除" 按钮。 在将来的教程中，我们将了解如何在删除记录时添加客户端确认。

## <a name="editing-data-with-the-gridview"></a>用 GridView 编辑数据

除了删除外，GridView 控件还提供内置的行级编辑支持。 将 GridView 配置为支持编辑会添加一个编辑按钮的列。 从最终用户的角度来看，单击行的 "编辑" 按钮将使该行变为可编辑状态，将单元格转换为包含现有值的文本框，并将 "编辑" 按钮替换为 "更新" 和 "取消" 按钮。 进行所需的更改后，最终用户可以单击 "更新" 按钮以提交更改，或者单击 "取消" 按钮以放弃更改。 无论是哪种情况，在单击 "更新" 或 "取消" 后，GridView 都将恢复到其预编辑状态。

从我们的角度来看，当最终用户单击特定行的 "编辑" 按钮时，回发可以和 GridView 执行以下步骤：

1. GridView 的 `EditItemIndex` 属性分配给单击了 "编辑" 按钮的行的索引
2. GridView 通过调用其 `Select()` 方法将自身重新绑定到 ObjectDataSource
3. 与 `EditItemIndex` 匹配的行索引以 "编辑模式" 呈现。 在此模式下，"编辑" 按钮替换为 "更新" 和 "取消" 按钮，BoundFields，其 `ReadOnly` 属性为 False （默认值）呈现为 TextBox Web 控件，其 `Text` 属性分配给数据字段的值。

此时，标记将返回到浏览器，从而允许最终用户对该行的数据进行任何更改。 当用户单击 "更新" 按钮时，将发生回发，GridView 执行以下步骤：

1. 将由最终用户输入的值分配给该 ObjectDataSource 的 `UpdateParameters` 值到 GridView 的编辑界面中
2. 将调用 ObjectDataSource 的 `Update()` 方法，并更新指定的记录
3. GridView 通过调用其 `Select()` 方法将自身重新绑定到 ObjectDataSource

分配到步骤1中的 `UpdateParameters` 的主键值来自 `DataKeyNames` 属性中指定的值，而非主键值来自于所编辑的行的 TextBox Web 控件中的文本。 与删除一样，必须正确设置 GridView 的 `DataKeyNames` 属性。 如果缺少此参数，则会在步骤1中为 `UpdateParameters` 的主键值分配 `Nothing` 值，而不会导致步骤2中的任何更新记录。

只需选中 GridView 智能标记中的 "启用编辑" 复选框，即可激活编辑功能。

![选中 "启用编辑" 复选框](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image37.png)

**图 15**：选中 "启用编辑" 复选框

选中 "启用编辑" 复选框将添加 CommandField （如果需要），并将其 `ShowEditButton` 属性设置为 `True`。 如前文所述，CommandField 包含许多 `ShowXButton` 属性，这些属性指示 CommandField 中显示哪一系列按钮。 选中 "启用编辑" 复选框会将 `ShowEditButton` 属性添加到现有的 CommandField：

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample6.aspx)]

这就是添加基本编辑支持的全部。 如 Figure16 所示，编辑界面相当于每个 BoundField，其 `ReadOnly` 属性设置为 `False` （默认值）呈现为一个文本框。 这包括 `CategoryID` 和 `SupplierID`等字段，它们是其他表的键。

[![单击 "编辑" 按钮时，将在编辑模式下显示该行](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image38.png)

**图 16**：单击 "Chai s 编辑" 按钮以编辑模式显示行（[单击以查看完全大小的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image40.png)）

除了要求用户直接编辑外键值外，还需要通过以下方式来实现编辑接口的接口：

- 如果用户输入数据库中不存在的 `CategoryID` 或 `SupplierID`，则 `UPDATE` 将违反外键约束，导致引发异常。
- 编辑界面不包括任何验证。 如果未提供所需的值（如 `ProductName`），或输入需要数值的字符串值（例如，输入 "太多！" 在 "`UnitPrice`" 文本框中），将引发异常。 将来的教程将介绍如何向编辑用户界面添加验证控件。
- 目前，*所有*不是只读的产品字段都必须包含在 GridView 中。 如果要从 GridView 中删除字段（例如 `UnitPrice`），则在更新数据时，GridView 不会将 `UnitPrice` `UpdateParameters` 值，这会将数据库记录的 `UnitPrice` 更改为 `NULL` 值。 同样，如果将某个必填字段（如 `ProductName`）从 GridView 中删除，则更新将失败，并且会出现与上面提到的 "*列 ' ProductName ' 不允许空值*" 这一错误。
- 编辑界面的格式设置不太必要。 `UnitPrice` 显示有四个小数点。 理想情况下，`CategoryID` 和 `SupplierID` 值将包含列出系统中的类别和供应商的 DropDownLists。

这些都是我们现在将需要使用的所有缺点，但会在以后的教程中解决。

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>用 DetailsView 插入、编辑和删除数据

如前文所述，DetailsView 控件一次显示一条记录，与 GridView 一样，允许编辑和删除当前显示的记录。 最终用户在 DetailsView 中编辑和删除项以及 ASP.NET 端工作流的体验与 GridView 的工作方式相同。 如果 DetailsView 不同于 GridView，则它还提供内置的插入支持。

若要演示 GridView 的数据修改功能，请首先将 DetailsView 添加到现有 GridView 之上的 `Basics.aspx` 页面，并通过 DetailsView 的智能标记将其绑定到现有的 ObjectDataSource。 接下来，清除 DetailsView 的 `Height` 和 `Width` 属性，然后从智能标记中选中 "启用分页" 选项。 若要启用编辑、插入和删除支持，只需选中 "启用编辑"、"启用插入" 和 "启用删除" 复选框。

![配置 DetailsView 以支持编辑、插入和删除](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image41.png)

**图 17**：配置 DetailsView 以支持编辑、插入和删除

对于 GridView，添加编辑、插入或删除支持会将 CommandField 添加到 DetailsView，如以下声明性语法所示：

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample7.aspx)]

请注意，对于 DetailsView，默认情况下，CommandField 显示在列集合的末尾。 由于 DetailsView 的字段呈现为行，CommandField 显示为行，其中显示了 DetailsView 底部的 "插入"、"编辑" 和 "删除" 按钮。

[![配置 DetailsView 以支持编辑、插入和删除](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image42.png)

**图 18**：配置 DetailsView 以支持编辑、插入和删除（[单击查看完全尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image44.png)）

单击 "删除" 按钮会启动与 GridView 相同的事件序列：回发;接下来，根据 `DataKeyNames` 值填充其 ObjectDataSource 的 `DeleteParameters`;并通过调用其 ObjectDataSource 的 `Delete()` 方法来完成，这会从数据库中实际删除产品。 在 DetailsView 中进行编辑时，其工作方式与 GridView 的工作方式相同。

对于插入，最终用户会看到一个新按钮，单击该按钮时，将在 "插入模式" 下呈现 DetailsView。 使用 "插入模式" 时，"新建" 按钮将被 "插入" 和 "取消" 按钮替换，并且仅显示 `InsertVisible` 属性设置为 `True` （默认值）的 BoundFields。 在通过智能标记将 DetailsView 绑定到数据源时，这些数据字段（如 `ProductID`）会将其[InsertVisible 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx)设置为 `False`。

通过智能标记将数据源绑定到 DetailsView 时，Visual Studio 会将 `InsertVisible` 属性设置为仅 `False` 自动增量字段。 只读字段（如 `CategoryName` 和 `SupplierName`）将显示在 "插入模式" 用户界面中，除非其 `InsertVisible` 属性显式设置为 `False`。 请花点时间将这两个字段的 `InsertVisible` 属性设置为 `False`，方法是通过 DetailsView 的声明性语法，或通过智能标记中的编辑字段链接。 图19显示了如何通过单击 "编辑字段" 链接将 `InsertVisible` 属性设置为 `False`。

[![Northwind 商贸现在提供 Acme 茶](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image45.png)

**图 19**： Northwind 商贸现在提供 Acme 茶（[单击查看全尺寸图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image47.png)）

设置 `InsertVisible` 属性后，请在浏览器中查看 `Basics.aspx` 页面，然后单击 "新建" 按钮。 图20显示了将新饮料（Acme 茶）添加到产品系列时的 DetailsView。

[![Northwind 商贸现在提供 Acme 茶](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image48.png)

**图 20**： Northwind 商贸现在提供 Acme 茶（[单击查看全尺寸图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image50.png)）

输入 Acme 茶的详细信息并单击 "插入" 按钮后，将向 `Products` 数据库表添加回发可以和新记录。 由于此 DetailsView 列出了产品，这些产品的顺序与数据库表中的产品顺序相同，因此我们必须向上一产品进行页，以便查看新产品。

[Acme 茶 ![详细信息](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image51.png)

**图 21**： Acme 茶的详细信息（[单击以查看完全大小的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image53.png)）

> [!NOTE]
> DetailsView 的[CurrentMode 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx)指示要显示的接口，可以是以下值之一： `Edit`、`Insert`或 `ReadOnly`。 [DefaultMode 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx)指示在编辑或插入完成后，detailsview 返回到的模式，适用于显示永久性处于编辑或插入模式的 detailsview。

对 DetailsView 的 "插入和编辑" 功能的点击和编辑功能受到与 GridView 相同的限制：用户必须通过文本框输入现有 `CategoryID` 和 `SupplierID` 值;接口缺少任何验证逻辑;不允许 `NULL` 值或没有在数据库级别指定默认值的所有产品字段都必须包含在插入接口中，依此类推。

在将来的文章中，我们将探讨的用于扩展和增强 GridView 编辑界面的技术也适用于 DetailsView 控件的编辑和插入界面。

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>使用 FormView 实现更灵活的数据修改用户界面

FormView 提供对插入、编辑和删除数据的内置支持，但由于它使用的是模板而不是字段，因此不能添加 BoundFields 或由 GridView 和 DetailsView 控件使用的 CommandField 来提供数据。修改接口。 相反，此接口用于收集用户输入的 Web 控件，以及在添加新项或编辑现有项时，还必须手动将新的、编辑、删除、插入、更新和取消按钮添加到相应的模板。 幸运的是，在通过其智能标记将 FormView 绑定到数据源时，Visual Studio 将自动创建所需的接口。

若要演示这些技术，请先将 FormView 添加到 `Basics.aspx` 页，然后从 FormView 的智能标记将其绑定到已创建的 ObjectDataSource。 这将为带有 TextBox Web 控件的 FormView 生成 `EditItemTemplate`、`InsertItemTemplate`和 `ItemTemplate`，以便为新的、编辑、删除、插入、更新和取消按钮收集用户的输入和按钮 Web 控件。 此外，FormView 的 `DataKeyNames` 属性设置为 ObjectDataSource 返回的对象的主键字段（`ProductID`）。 最后，选中 FormView 的智能标记中的 "启用分页" 选项。

下面显示了在 FormView 绑定到 ObjectDataSource 后，FormView 的 `ItemTemplate` 的声明性标记。 默认情况下，每个非布尔值 product 字段都绑定到标签 Web 控件的 `Text` 属性，而每个布尔值字段（`Discontinued`）都绑定到已禁用 CheckBox Web 控件的 `Checked` 属性。 要使 "新建"、"编辑" 和 "删除" 按钮在被单击时触发某些 FormView 行为，必须分别将其 `CommandName` 值设置为 `New`、`Edit`和 `Delete`。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample8.aspx)]

图22显示了通过浏览器查看 FormView 的 `ItemTemplate`。 列出的每个 "产品" 字段都带有底部的 "新建"、"编辑" 和 "删除" 按钮。

[![下 FormView ItemTemplate 列出了每个 "产品" 字段以及 "新建"、"编辑" 和 "删除" 按钮](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image54.png)

**图 22**：下 FormView `ItemTemplate` 列出了每个 "产品" 字段以及 "新建"、"编辑" 和 "删除" 按钮（[单击以查看完全大小的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image56.png)）

例如，在 GridView 和 DetailsView 中，单击 "删除" 按钮或任何 `CommandName` 属性设置为 "删除" 的按钮、LinkButton 或 ImageButton 将导致回发，根据 FormView 的 `DataKeyNames` 值填充 ObjectDataSource 的 `DeleteParameters`，并调用 ObjectDataSource 的 `Delete()` 方法。

单击 "编辑" 按钮时，会将回发可以，并将数据重新绑定到负责呈现编辑界面的 `EditItemTemplate`。 此接口包括用于编辑数据的 Web 控件以及 "更新" 和 "取消" 按钮。 Visual Studio 生成的默认 `EditItemTemplate` 包含任何自动增量字段（`ProductID`）的标签、每个非布尔值字段的文本框，以及每个布尔值字段的复选框。 此行为与在 GridView 和 DetailsView 控件中自动生成的 BoundFields 非常相似。

> [!NOTE]
> FormView 自动生成 `EditItemTemplate` 的一个小问题是，它会为只读字段呈现 TextBox Web 控件，如 `CategoryName` 和 `SupplierName`。 稍后我们将了解如何对此进行说明。

`EditItemTemplate` 中的 TextBox 控件使用*双向数据*绑定将其 `Text` 属性绑定到其对应数据字段的值。 在将数据绑定到模板时，以及在填充 ObjectDataSource 用于插入或编辑记录的参数时，由 `<%# Bind("dataField") %>`表示的双向数据绑定将执行数据绑定。 也就是说，当用户在 `ItemTemplate`单击 "编辑" 按钮时，`Bind()` 方法返回指定的数据字段值。 用户进行更改并单击 "更新" 后，将向 ObjectDataSource 的 `UpdateParameters`应用与使用 `Bind()` 指定的数据字段对应的回发值。 或者，通过 `<%# Eval("dataField") %>`表示的单向数据绑定仅在将数据绑定到模板时检索数据字段值，并且*不*会在回发时将用户输入的值返回到数据源的参数。

以下声明性标记显示了 FormView 的 `EditItemTemplate`。 请注意，此处的数据绑定语法中使用的是 `Bind()` 方法，并且 "更新" 和 "取消" 按钮 Web 控件将相应地设置其 `CommandName` 属性。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample9.aspx)]

此时，我们的 `EditItemTemplate`会在我们尝试使用异常时引发异常。 问题在于，"`CategoryName`" 和 "`SupplierName`" 字段在 `EditItemTemplate`中呈现为 TextBox Web 控件。 需要将这些文本框更改为标签，或将其全部删除。 让我们从 `EditItemTemplate`完全删除它们。

图23在单击 Chai 的 "编辑" 按钮后，在浏览器中显示 FormView。 请注意，`ItemTemplate` 中所示的 "`SupplierName`" 和 "`CategoryName`" 字段不再存在，因为我们只是将它们从 `EditItemTemplate`中删除。 单击 "更新" 按钮时，FormView 会经历与 GridView 和 DetailsView 控件相同的步骤顺序。

[默认情况下，EditItemTemplate 会将每个可编辑的产品字段显示为文本框或复选框 ![](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image57.png)

**图 23**：默认情况下，`EditItemTemplate` 将每个可编辑的产品字段显示为文本框或复选框（[单击查看完全尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image59.png)）

单击 "插入" 按钮时，FormView `ItemTemplate` 回发可以。 但是，由于正在添加新记录，因此不会将任何数据绑定到 FormView。 `InsertItemTemplate` 接口包括用于添加新记录的 Web 控件以及 "插入" 和 "取消" 按钮。 Visual Studio 生成的默认 `InsertItemTemplate` 包含一个文本框，其中包含每个非布尔值字段和每个布尔值字段对应的复选框，这与自动生成 `EditItemTemplate`的接口类似。 TextBox 控件将其 `Text` 属性绑定到使用双向数据绑定的相应数据字段的值。

以下声明性标记显示了 FormView 的 `InsertItemTemplate`。 请注意，此处的数据绑定语法中使用的是 `Bind()` 方法，"插入" 和 "取消" 按钮 Web 控件的 `CommandName` 属性设置相应。

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-vb/samples/sample10.aspx)]

`InsertItemTemplate`的 FormView 自动生成有个很微妙。 具体来说，即使是只读字段（如 `CategoryName` 和 `SupplierName`），也会创建 TextBox Web 控件。 与 `EditItemTemplate`一样，我们需要从 `InsertItemTemplate`中删除这些文本框。

图24在添加新产品时，在浏览器中显示 FormView，Acme 咖啡。 请注意，`ItemTemplate` 中所示的 "`SupplierName`" 和 "`CategoryName`" 字段不再存在，因为我们刚刚将它们删除。 单击 "插入" 按钮时，FormView 会按照 DetailsView 控件的相同步骤顺序进行，并向 `Products` 表中添加一条新记录。 图25在插入后，在 FormView 中显示 Acme 咖啡产品的详细信息。

[![则指示 FormView 的插入界面](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image60.png)

**图 24**： `InsertItemTemplate` 指示 FormView 的插入界面（[单击以查看完全尺寸的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image62.png)）

[![新产品的详细信息，Acme 咖啡显示在 FormView](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image63.png)

**图 25**：新产品的详细信息，Acme 咖啡在 FormView 中显示（[单击查看完全大小的图像](an-overview-of-inserting-updating-and-deleting-data-vb/_static/image65.png)）

通过将只读、编辑和插入界面分为三个单独的模板，FormView 允许比 DetailsView 和 GridView 更精细地控制这些接口。

> [!NOTE]
> 与 DetailsView 一样，FormView 的 `CurrentMode` 属性指示正在显示的接口，其 `DefaultMode` 属性指示在完成编辑或插入后，FormView 返回到的模式。

## <a name="summary"></a>摘要

在本教程中，我们将介绍使用 GridView、DetailsView 和 FormView 插入、编辑和删除数据的基本知识。 这三种控件都提供了一定程度的内置数据修改功能，无需在 ASP.NET 页中编写单行代码即可使用这些功能，这是因为数据 Web 控件和 ObjectDataSource。 然而，简单的点和单击技巧会呈现一个相当 frail 的数据修改用户界面。 为了提供验证、注入编程值、合理地处理异常、自定义用户界面等，我们需要依赖于将在接下来的几个教程中讨论的一系列技术。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](limiting-data-modification-functionality-based-on-the-user-cs.md)
> [下一页](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
