---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
title: 编辑和删除 DataList 中的数据的概述（C#） |Microsoft Docs
author: rick-anderson
description: 尽管 DataList 缺少内置的编辑和删除功能，但在本教程中，我们将了解如何创建支持编辑和删除 o 的 DataList 。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: c3b0c86e-fe98-41ee-b26f-ca38cddaa75e
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 481c9a14b1ebfe36ffcddd0237701bc04266e393
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78480914"
---
# <a name="an-overview-of-editing-and-deleting-data-in-the-datalist-c"></a>编辑和删除 DataList 中的数据的概述（C#）

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_36_CS.exe)或[下载 PDF](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/datatutorial36cs1.pdf)

> 尽管 DataList 缺少内置的编辑和删除功能，但在本教程中，我们将了解如何创建支持编辑和删除其基础数据的 DataList。

## <a name="introduction"></a>简介

在[插入、更新和删除数据的概述](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)中，我们介绍了如何使用应用程序体系结构、ObjectDataSource 和 GridView、DetailsView 和 FormView 控件插入、更新和删除数据。 使用 ObjectDataSource 和这三个数据 Web 控件，实现简单的数据修改接口就是一个 snap，只需从智能标记中计时一个复选框。 无需编写代码。

遗憾的是，DataList 缺少 GridView 控件中固有的内置编辑和删除功能。 此缺少的功能在某种程度上是因为，当声明性数据源控件和无代码的数据修改页不可用时，DataList 是以前版本的 ASP.NET 中的 relic。 尽管 ASP.NET 2.0 中的 DataList 不提供与 GridView 相同的现成数据修改功能，但我们仍可以使用 ASP.NET 1.x 技术来包括此类功能。 此方法需要一些代码，但正如我们在本教程中看到的那样，DataList 提供了一些事件和属性来帮助进行此过程。

在本教程中，我们将了解如何创建支持编辑和删除其基础数据的 DataList。 将来的教程将介绍更高级的编辑和删除方案，包括输入字段验证、适当处理从数据访问或业务逻辑层引发的异常等。

> [!NOTE]
> 与 DataList 一样，Repeater 控件缺少用于插入、更新或删除的现成功能。 虽然可以添加此类功能，但 DataList 包含在 Repeater 中找不到的属性和事件，可简化此类功能的添加。 因此，本教程和以后查看编辑和删除的教程将严格关注 DataList。

## <a name="step-1-creating-the-editing-and-deleting-tutorials-web-pages"></a>步骤1：创建编辑和删除教程网页

在开始探索如何更新和删除 DataList 中的数据之前，先花点时间在我们的网站项目中创建 ASP.NET 页面，我们将在本教程和下几个页面中创建这些页面。 首先添加一个名为 `EditDeleteDataList`的新文件夹。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `Basics.aspx`
- `BatchUpdate.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![添加教程的 ASP.NET 页](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image1.png)

**图 1**：添加教程的 ASP.NET 页

与在其他文件夹中一样，`EditDeleteDataList` 文件夹中的 `Default.aspx` 列出了本部分中的教程。 请记住，`SectionLevelTutorialListing.ascx` 用户控件提供此功能。 因此，通过将此用户控件从解决方案资源管理器拖到页面 s 设计视图，将该用户控件添加到 `Default.aspx`。

[![将 SectionLevelTutorialListing 用户控件添加到 default.aspx](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image3.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image2.png)

**图 2**：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击以查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image4.png)）

最后，将页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，请在主/详细信息报表后面添加包含 DataList 和 Repeater `<siteMapNode>`的以下标记：

[!code-xml[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample1.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧菜单现在包含 DataList 编辑和删除教程的项。

![站点映射现在包含 DataList 编辑和删除教程的条目](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image5.png)

**图 3**：站点地图现在包含 DataList 编辑和删除教程的条目

## <a name="step-2-examining-techniques-for-updating-and-deleting-data"></a>步骤2：检查更新和删除数据的方法

使用 GridView 编辑和删除数据变得非常简单，因为在幕后，GridView 和 ObjectDataSource 在协同工作。 如[检查与插入、更新和删除教程相关的事件](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)中所述，单击 "行更新" 按钮时，GridView 会自动将使用双向数据绑定的字段分配给其 ObjectDataSource 的 `UpdateParameters` 集合，然后调用该 objectdatasource 的 `Update()` 方法。

不幸的是，DataList 并未提供此内置功能。 我们负责确保将用户的值分配给 ObjectDataSource s 参数，并调用它的 `Update()` 方法。 为帮助我们做到这一点，DataList 提供了以下属性和事件：

- **[`DataKeyField` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeyfield.aspx)** 在更新或删除时，需要能够唯一地标识 DataList 中的每一项。 将此属性设置为显示的数据的主键字段。 这样做将用每个 DataList 项的指定 `DataKeyField` 值填充 DataList s [`DataKeys` 集合](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basedatalist.datakeys.aspx)。
- 当单击其 `CommandName` 属性设置为 "编辑" 的按钮、LinkButton 或 ImageButton 时，**将激发[`EditCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.editcommand.aspx)** 。
- 当单击 `CommandName` 属性设置为取消的按钮、LinkButton 或 ImageButton 时 **，将激发[`CancelCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.cancelcommand.aspx)** 。
- 当单击其 `CommandName` 属性设置为 Update 的按钮、LinkButton 或 ImageButton 时，**将激发[`UpdateCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.updatecommand.aspx)** 。
- 当单击其 `CommandName` 属性设置为删除的按钮、LinkButton 或 ImageButton 时，**将激发[`DeleteCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.deletecommand.aspx)** 。

使用这些属性和事件，可以使用四种方法更新和删除 DataList 中的数据：

1. **使用 ASP.NET 1.X 技术**，DataList 在 ASP.NET 2.0 和 objectdatasource 之前已经存在，并能够完全通过编程方式更新和删除数据。 此方法完全 ditches 了 ObjectDataSource，并要求将数据直接从业务逻辑层绑定到 DataList，同时检索要显示的数据以及更新或删除记录的时间。
2. 在**页面上使用单个 ObjectDataSource 控件来选择、更新和删除**DataList，而 DataList 缺少 GridView 固有的编辑和删除功能，则没有理由将它们自行添加。 使用此方法时，我们将使用一个 ObjectDataSource，就像在 GridView 示例中一样，但必须为 DataList s `UpdateCommand` 事件创建一个事件处理程序，并在其中设置 ObjectDataSource s 参数并调用其 `Update()` 方法。
3. **使用 ObjectDataSource 控件选择，但**在使用选项2时，直接针对 BLL 进行更新和删除，我们需要在 `UpdateCommand` 事件中编写一些代码，并分配参数值等。 相反，我们可以继续使用 ObjectDataSource 进行选择，但会直接对 BLL 进行更新和删除调用（如使用选项1）。 在我看来，通过直接与 BLL 进行联系，更新数据会导致可读性更高的代码，而不是分配 ObjectDataSource `UpdateParameters` 并调用其 `Update()` 方法。
4. **使用声明性方式，通过多个 objectdatasource** ，以上三种方法都需要使用几个代码。 如果你不想继续使用尽可能多的声明性语法，最后一种方法是在页面上包含多个 Objectdatasource。 第一个 ObjectDataSource 从 BLL 中检索数据并将其绑定到 DataList。 对于更新，会添加另一个 ObjectDataSource，但会直接在 `EditItemTemplate`的 DataList 中添加。 若要包括删除支持，请在 `ItemTemplate`中需要另一个 ObjectDataSource。 使用此方法时，这些嵌入的 ObjectDataSource 会使用 `ControlParameters` 以声明方式将 ObjectDataSource s 参数绑定到用户输入控件（不必在 DataList s `UpdateCommand` 事件处理程序中以编程方式指定这些参数）。 此方法仍需要一些代码来调用嵌入的 ObjectDataSource `Update()` 或 `Delete()` 命令，但所需的方法远远低于其他三个方法。 这里的缺点是，多个 Objectdatasource 确实会打乱页面，从整体的可读性中 detracting。

如果强制只使用其中一种方法，我将选择选项1，因为它提供了最大的灵活性，并且 DataList 最初设计为适应此模式。 尽管 DataList 已经过扩展，可以使用 ASP.NET 2.0 数据源控件，但它不具有官方 ASP.NET 2.0 数据 Web 控件（GridView、DetailsView 和 FormView）的所有扩展点或功能。 但不能使用选项2到4。

这种情况下，以后的编辑和删除教程将使用 ObjectDataSource 来检索要显示的数据，并直接调用 BLL 以更新和删除数据（选项3）。

## <a name="step-3-adding-the-datalist-and-configuring-its-objectdatasource"></a>步骤3：添加 DataList 并配置其 ObjectDataSource

在本教程中，我们将创建一个列出产品信息的 DataList，并为每个产品提供了编辑名称和价格以及完全删除该产品的功能。 具体而言，我们将使用 ObjectDataSource 检索要显示的记录，但通过直接与 BLL 进行直接交互来执行更新和删除操作。 在考虑如何实现对 DataList 的编辑和删除功能之前，让我们先获取页面以在只读界面中显示产品。 由于我们已在前面的教程中检查了这些步骤，因此我将继续执行这些步骤。

首先打开 `EditDeleteDataList` 文件夹中的 "`Basics.aspx`" 页，然后从设计视图向页面添加 DataList。 接下来，从 DataList s 智能标记创建一个新的 ObjectDataSource。 由于我们使用的是产品数据，因此请将其配置为使用 `ProductsBLL` 类。 若要检索*所有*产品，请在 "选择" 选项卡中选择 `GetProducts()` 方法。

[![将 ObjectDataSource 配置为使用 ProductsBLL 类](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image7.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image6.png)

**图 4**：将 ObjectDataSource 配置为使用 `ProductsBLL` 类（[单击以查看完全大小的映像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image8.png)）

[![使用 GetProducts （）方法返回产品信息](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image10.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image9.png)

**图 5**：使用 `GetProducts()` 方法返回产品信息（[单击以查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image11.png)）

DataList （如 GridView）不用于插入新数据;因此，请从 "插入" 选项卡的下拉列表中选择 "（无）" 选项。对于 "更新" 和 "删除" 选项卡，请选择 "（无）"，因为更新和删除操作将通过 BLL 以编程方式执行。

[![确认 ObjectDataSource s INSERT、UPDATE 和 DELETE 选项卡中的下拉列表设置为 "（无）"](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image13.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image12.png)

**图 6**：确认 OBJECTDATASOURCE s INSERT、UPDATE 和 DELETE 选项卡中的下拉列表设置为 "（无）" （[单击查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image14.png)）

配置 ObjectDataSource 后，单击 "完成"，返回到设计器。 正如我们过去的示例中所示，当完成 ObjectDataSource 配置时，Visual Studio 将自动为 DropDownList 创建 `ItemTemplate`，并显示每个数据字段。 将此 `ItemTemplate` 替换为仅显示产品的名称和价格的。 同时，将 `RepeatColumns` 属性设置为2。

> [!NOTE]
> 如*插入、更新和删除数据概述*教程中所述，当使用 ObjectDataSource 修改数据时，我们的体系结构需要从 objectdatasource 的声明性标记中删除 `OldValuesParameterFormatString` 属性（或将其重置为其默认值，`{0}`）。 但是，在本教程中，我们只使用 ObjectDataSource 来检索数据。 因此，不需要修改 ObjectDataSource s `OldValuesParameterFormatString` 属性值（尽管这不会造成影响）。

将默认 DataList `ItemTemplate` 替换为自定义的 DataList 后，页面上的声明性标记应如下所示：

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample2.aspx)]

花点时间通过浏览器查看进度。 如图7所示，DataList 显示两列中的每个产品的产品名称和单价。

[![产品名称和价格显示在两列 DataList 中](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image16.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image15.png)

**图 7**：产品名称和价格显示在两列 DataList 中（[单击以查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image17.png)）

> [!NOTE]
> DataList 具有多个更新和删除进程所需的属性，这些值存储在视图状态中。 因此，在生成支持编辑或删除数据的 DataList 时，必须启用 DataList 的视图状态。  
>   
> 敏锐读取器可能会回忆到，我们能够在创建可编辑的 GridViews、DetailsViews 和 FormViews 时禁用视图状态。 这是因为，ASP.NET 2.0 Web 控件可以包含*控件状态*，这是在视图状态等回发（如视图状态，但认为是必需的）期间保持的状态。

在 GridView 中禁用视图状态只会省略普通状态信息，但会保持控件状态（包括编辑和删除所需的状态）。 在 ASP.NET 1.x 时间范围内创建的 DataList 不使用控件状态，因此必须启用视图状态。 有关控件状态的用途及其与视图状态之间的不同之处的详细信息，请参阅[控件状态与视图状态](https://msdn.microsoft.com/library/1whwt1k7.aspx)。

## <a name="step-4-adding-an-editing-user-interface"></a>步骤4：添加编辑用户界面

GridView 控件由一组字段（BoundFields、CheckBoxFields、Templatefield 等）组成。 这些字段可根据其模式调整呈现的标记。 例如，在只读模式下，BoundField 将其数据字段值显示为文本;处于编辑模式时，它将呈现一个文本框 Web 控件，其 `Text` 属性分配有数据字段值。

另一方面，DataList 使用模板呈现其项。 只读项是使用 `ItemTemplate` 呈现的，而处于编辑模式的项则是通过 `EditItemTemplate`呈现的。 此时，DataList 只有一个 `ItemTemplate`。 若要支持项级编辑功能，我们需要添加一个 `EditItemTemplate`，其中包含要为可编辑项显示的标记。 对于本教程，我们将使用 TextBox Web 控件来编辑产品的名称和单价。

可以通过声明方式或通过设计器创建 `EditItemTemplate` （通过从 DataList s 智能标记选择 "编辑模板" 选项）。 若要使用 "编辑模板" 选项，请先在智能标记中单击 "编辑模板" 链接，然后从下拉列表中选择 `EditItemTemplate` 项。

[![选择使用 DataList s EditItemTemplate](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image19.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image18.png)

**图 8**：选择使用 DataList `EditItemTemplate` （[单击查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image20.png)）

接下来，键入产品名称：和价格：，然后将 "工具箱" 中的两个 TextBox 控件拖到设计器上的 `EditItemTemplate` 接口。 将 "文本框" `ID` 属性设置为 `ProductName` 和 `UnitPrice`。

[![为产品的名称和价格添加文本框](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image22.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image21.png)

**图 9**：为产品的 "名称" 和 "价格" 添加文本框（[单击以查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image23.png)）

需要将相应的产品数据字段值绑定到两个文本框的 `Text` 属性。 在 "文本框" 智能标记中，单击 "编辑数据绑定" 链接，然后将相应的数据字段与 `Text` 属性相关联，如图10所示。

> [!NOTE]
> 将 `UnitPrice` 数据字段绑定到 "价格" 文本框 `Text` 字段时，可以将其格式设置为货币值（`{0:C}`）、常规数字（`{0:N}`），或将其设置为未格式化。

![将 "产品名称" 和 "单价" 数据字段绑定到文本框的文本属性](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image24.png)

**图 10**：将 `ProductName` 和 `UnitPrice` 数据字段绑定到文本框的 `Text` 属性

请注意，图10中的 "编辑数据绑定" 对话框*不*包含双向数据绑定复选框，在 GridView 或 DetailsView 中编辑 TemplateField 时，或在 FormView 中模板。 双向数据绑定功能允许在插入或更新数据时将输入 Web 控件中输入的值自动分配给相应的 ObjectDataSource s `InsertParameters` 或 `UpdateParameters`。 DataList 不支持双向数据绑定，因为我们稍后将在本教程中看到，在用户进行更改并准备好更新数据后，我们需要以编程方式访问这些文本框 `Text` 属性，并将其值传入 `ProductsBLL` 类中相应的 `UpdateProduct` 方法。

最后，需要向 `EditItemTemplate`中添加 "更新" 和 "取消" 按钮。 正如我们[使用带有详细信息 DataList 教程的主记录的项目符号列表在主/详细信息](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)中看到的那样，在中继器或 datalist 内单击其 `CommandName` 属性的按钮、LinkButton 或 ImageButton 时，将引发 Repeater 或 datalist s `ItemCommand` 事件。 对于 DataList，如果 `CommandName` 属性设置为某个值，则还可能会引发附加事件。 特殊 `CommandName` 属性值包括：

- Cancel 引发 `CancelCommand` 事件
- 编辑引发 `EditCommand` 事件
- Update 引发 `UpdateCommand` 事件

请记住，除了 `ItemCommand` 事件外，*还*会引发这些事件。

添加到 `EditItemTemplate` 两个按钮 Web 控件，其中一个 `CommandName` 设置为 "更新"，另一个设置为 "取消"。 添加这两个按钮 Web 控件后，设计器应如下所示：

[![向 EditItemTemplate 添加 "更新" 和 "取消" 按钮](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image26.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image25.png)

**图 11**：向 `EditItemTemplate` 添加 "更新" 和 "取消" 按钮（[单击以查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image27.png)）

`EditItemTemplate` 完成后，DataList 的声明性标记应如下所示：

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample3.aspx)]

## <a name="step-5-adding-the-plumbing-to-enter-edit-mode"></a>步骤5：添加用于进入编辑模式的管道

此时，DataList 有一个通过其 `EditItemTemplate`定义的编辑界面;但是，目前没有办法让用户访问我们的页面，以指示他要编辑产品的信息。 我们需要向每个产品添加一个 "编辑" 按钮，在单击该按钮时，将在编辑模式下呈现该 DataList 项。 首先，通过设计器或以声明方式向 `ItemTemplate`添加 "编辑" 按钮。 请确保将 "编辑" 按钮 `CommandName` 属性设置为 "编辑"。

添加此编辑按钮后，请花点时间查看浏览器中的页面。 添加此项后，每个产品列表都应包含 "编辑" 按钮。

[![向 EditItemTemplate 添加 "更新" 和 "取消" 按钮](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image29.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image28.png)

**图 12**：向 `EditItemTemplate` 添加 "更新" 和 "取消" 按钮（[单击以查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image30.png)）

单击该按钮将导致回发，但*不会将产品列表置于编辑*模式。 要使产品可编辑，我们需要：

1. 将 DataList s [`EditItemIndex` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)设置为刚单击 "编辑" 按钮的 `DataListItem` 的索引。
2. 将数据重新绑定到 DataList。 重新呈现 DataList 后，其 `ItemIndex` 对应于 DataList s `EditItemIndex` 的 `DataListItem` 将使用其 `EditItemTemplate`进行呈现。

由于在单击 "编辑" 按钮时将激发 DataList `EditCommand` 事件，请使用以下代码创建 `EditCommand` 事件处理程序：

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample4.cs)]

`EditCommand` 事件处理程序在类型 `DataListCommandEventArgs` 的对象中传递为它的第二个输入参数，其中包括对其编辑按钮被单击（`e.Item`）的 `DataListItem` 的引用。 此事件处理程序首先将 DataList `EditItemIndex` 设置为可编辑 `DataListItem` 的 `ItemIndex`，然后通过调用 DataList s `DataBind()` 方法将数据重新绑定到 DataList。

添加此事件处理程序后，请在浏览器中重新访问此页。 单击 "编辑" 按钮会使单击的产品可编辑（参见图13）。

[单击 "编辑" 按钮 ![使产品可编辑](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image32.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image31.png)

**图 13**：单击 "编辑" 按钮使产品可编辑（[单击以查看完全尺寸的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image33.png)）

## <a name="step-6-saving-the-user-s-changes"></a>步骤6：保存用户的更改

此时单击 "已编辑的产品更新" 或 "取消" 按钮将不执行任何操作;若要添加此功能，需要为 DataList s `UpdateCommand` 和 `CancelCommand` 事件创建事件处理程序。 首先创建 `CancelCommand` 事件处理程序，该处理程序在单击 "已编辑的产品" "取消" 按钮时执行，并将 DataList 返回到其预编辑状态。

若要使 DataList 在只读模式下呈现其所有项，需执行以下操作：

1. 将 DataList s [`EditItemIndex` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)设置为不存在的 `DataListItem` 索引的索引。 `-1` 是一种安全选择，因为 `DataListItem` 索引从 `0`开始。
2. 将数据重新绑定到 DataList。 由于 `DataListItem` `ItemIndex` es 都不对应于 DataList `EditItemIndex`，因此整个 DataList 将以只读模式呈现。

可以通过以下事件处理程序代码来完成这些步骤：

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample5.cs)]

添加此项后，单击 "取消" 按钮会将 DataList 返回到其预编辑状态。

需要完成的最后一个事件处理程序是 `UpdateCommand` 事件处理程序。 此事件处理程序需要：

1. 以编程方式访问用户输入的产品名称、价格以及已编辑的产品 `ProductID`。
2. 通过在 `ProductsBLL` 类中调用相应的 `UpdateProduct` 重载来启动更新过程。
3. 将 DataList s [`EditItemIndex` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.edititemindex.aspx)设置为不存在的 `DataListItem` 索引的索引。 `-1` 是一种安全选择，因为 `DataListItem` 索引从 `0`开始。
4. 将数据重新绑定到 DataList。 由于 `DataListItem` `ItemIndex` es 都不对应于 DataList `EditItemIndex`，因此整个 DataList 将以只读模式呈现。

步骤1和步骤2负责保存用户的更改;在保存更改后，步骤3和4将 DataList 返回到其预编辑状态，并且与 `CancelCommand` 事件处理程序中执行的步骤相同。

若要获取更新后的产品名称和价格，需要使用 `FindControl` 方法以编程方式引用 `EditItemTemplate`中的 TextBox Web 控件。 我们还需要获取已编辑的产品 `ProductID` 值。 最初将 ObjectDataSource 绑定到 DataList 时，Visual Studio 将 DataList s `DataKeyField` 属性分配给数据源（`ProductID`）中的主键值。 然后，可以从 DataList s `DataKeys` 集合中检索此值。 请花点时间确保 `DataKeyField` 属性确实设置为 `ProductID`。

下面的代码实现了以下四个步骤：

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample6.cs)]

此事件处理程序首先从 `DataKeys` 集合的已编辑的产品 `ProductID` 中进行读取。 接下来，引用 `EditItemTemplate` 中的两个文本框，并将其 `Text` 属性存储在本地变量中，`productNameValue` 和 `unitPriceValue`。 我们使用 `Decimal.Parse()` 方法从 "`UnitPrice`" 文本框中读取值，以便如果输入的值具有货币符号，则仍可将其正确转换为 `Decimal` 值。

> [!NOTE]
> 如果文本框文本属性指定了值，则仅将 `ProductName` 和 `UnitPrice` 文本框中的值分配给 productNameValue 和 unitPriceValue 变量。 否则，将 `Nothing` 的值用于变量，这就是使用数据库 `NULL` 值更新数据的效果。 也就是说，我们的代码处理将空字符串转换为数据库 `NULL` 值，这是 GridView、DetailsView 和 FormView 控件中编辑界面的默认行为。

读取值后，将调用 `ProductsBLL` 类 s `UpdateProduct` 方法，并传入产品的名称、价格和 `ProductID`。 事件处理程序完成，方法是使用与 `CancelCommand` 事件处理程序中的完全相同的逻辑将 DataList 返回到其预编辑状态。

完成 `EditCommand`、`CancelCommand`和 `UpdateCommand` 事件处理程序后，访问者可以编辑产品的名称和价格。 图14-16 显示此编辑工作流的运行情况。

[![首次访问页面时，所有产品都处于只读模式](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image35.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image34.png)

**图 14**：首次访问页面时，所有产品都处于只读模式（[单击以查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image36.png)）

[![更新产品的名称或价格，请单击 "编辑" 按钮](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image38.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image37.png)

**图 15**：若要更新产品的名称或价格，请单击 "编辑" 按钮（[单击以查看完全大小的图像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image39.png)）

[更改值后 ![，单击 "更新" 以返回到只读模式](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image41.png)](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image40.png)

**图 16**：更改值后，单击 "更新" 以返回到只读模式（[单击以查看完全大小的映像](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/_static/image42.png)）

## <a name="step-7-adding-delete-capabilities"></a>步骤7：添加删除功能

将删除功能添加到 DataList 的步骤类似于用于添加编辑功能的步骤。 简而言之，在单击时，需要向 `ItemTemplate` 添加 "删除" 按钮：

1. 通过 `DataKeys` 集合读取相应的产品 `ProductID`。
2. 通过调用 `ProductsBLL` 类 s `DeleteProduct` 方法执行删除。
3. 将数据重新绑定到 DataList。

首先，让我们将 "删除" 按钮添加到 `ItemTemplate`。

单击此按钮时，其 `CommandName` 为 "编辑"、"更新" 或 "取消" 的按钮会引发 DataList s `ItemCommand` 事件，同时还会引发附加事件（例如，在使用 "编辑" 时，将引发 `EditCommand` 事件）。 同样，DataList 中其 `CommandName` 属性设置为 "删除" 的任何按钮、LinkButton 或 ImageButton 都将引发 `DeleteCommand` 事件（连同 `ItemCommand`）。

在 `ItemTemplate`中的 "编辑" 按钮旁边添加 "删除" 按钮，并将其 `CommandName` 属性设置为 "删除"。 添加此按钮后，DataList 的 `ItemTemplate` 声明性语法应该如下所示：

[!code-aspx[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample7.aspx)]

接下来，使用以下代码为 DataList s `DeleteCommand` 事件创建事件处理程序：

[!code-csharp[Main](an-overview-of-editing-and-deleting-data-in-the-datalist-cs/samples/sample8.cs)]

单击 "删除" 按钮会导致回发，并激发 DataList `DeleteCommand` 事件。 在事件处理程序中，从 `DataKeys` 集合访问已单击的产品 `ProductID` 值。 接下来，通过调用 `ProductsBLL` 类 `DeleteProduct` 方法删除该产品。

删除产品后，将数据重新绑定到 DataList （`DataList1.DataBind()`）非常重要，否则 DataList 将继续显示刚刚删除的产品。

## <a name="summary"></a>摘要

尽管 DataList 缺少点并单击编辑和删除 GridView 所能提供的支持，但有一小段代码可以对其进行增强，以包含这些功能。 在本教程中，我们介绍了如何创建一个两列的列表，其中列出了可删除的产品以及名称和价格。 添加编辑和删除支持是指在 `ItemTemplate` 和 `EditItemTemplate`中包含适当的 Web 控件，创建相应的事件处理程序，读取用户输入的值和主键值，并与业务逻辑层交互。

虽然我们向 DataList 添加了基本的编辑和删除功能，但它没有更多的高级功能。 例如，没有输入字段验证-如果用户输入的价格太大，则在尝试将太昂贵的资源转换为 `Decimal`时，`Decimal.Parse` 会引发异常。 同样，如果在业务逻辑或数据访问层上更新数据时出现问题，则会向用户显示标准错误屏幕。 如果在 "删除" 按钮上没有任何类型的确认，则意外删除产品会很有可能。

在将来的教程中，我们将了解如何改进编辑用户体验。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的潜在客户评审者是 Zack，Ken Pespisa 和 Randy Schmidt。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一部分](performing-batch-updates-cs.md)
