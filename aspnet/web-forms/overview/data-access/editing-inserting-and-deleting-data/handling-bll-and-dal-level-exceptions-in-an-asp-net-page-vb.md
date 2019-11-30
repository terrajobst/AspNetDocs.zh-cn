---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
title: 在 ASP.NET 页中处理 BLL 和 DAL 级别的异常（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何在执行插入、更新或删除操作的过程中显示友好的信息性错误消息。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 129d4338-1315-4f40-89b5-2b84b807707d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb
msc.type: authoredcontent
ms.openlocfilehash: ee277596ade18d2603892d134b47c2c8697836bb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621049"
---
# <a name="handling-bll--and-dal-level-exceptions-in-an-aspnet-page-vb"></a>在 ASP.NET 页中处理 BLL 和 DAL 级别的异常 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_18_VB.exe)或[下载 PDF](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/datatutorial18vb1.pdf)

> 在本教程中，我们将了解如何在 ASP.NET 数据 Web 控件的插入、更新或删除操作过程中显示友好的信息性错误消息。

## <a name="introduction"></a>简介

使用分层应用程序体系结构处理 ASP.NET web 应用程序中的数据涉及以下三个常规步骤：

1. 确定需要调用的业务逻辑层的方法以及要传递的参数值。 参数值可以进行硬编码、以编程方式分配，也可以是用户输入的输入。
2. 调用方法。
3. 处理结果。 调用返回数据的 BLL 方法时，这可能涉及将数据绑定到数据 Web 控件。 对于用于修改数据的 BLL 方法，这可能包括基于返回值执行某些操作或适当地处理在步骤2中出现的任何异常。

正如在[上一教程](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)中看到的那样，ObjectDataSource 和数据 Web 控件都为步骤1和3提供了扩展点。 例如，在将其字段值分配给其 ObjectDataSource 的 `UpdateParameters` 集合之前，GridView 会激发其 `RowUpdating` 事件;在 ObjectDataSource 完成操作后引发其 `RowUpdated` 事件。

我们已经检查了在步骤1中激发的事件，并已了解如何使用它们来自定义输入参数或取消操作。 在本教程中，我们将关注完成操作后激发的事件。 使用这些后期级别事件处理程序，我们可以确定在操作过程中是否发生了异常并适当地对其进行处理，而不是在屏幕上显示一条友好的信息性错误消息，而不是默认为标准 ASP.NET异常页。

为了说明如何使用这些后期事件，我们将创建一个页面，其中列出了可编辑的 GridView 中的产品。 更新产品时，如果引发了异常，我们的 ASP.NET 页面将在 GridView 之上显示一条简短消息，说明发生了问题。 让我们进入正题！

## <a name="step-1-creating-an-editable-gridview-of-products"></a>步骤1：创建可编辑的产品 GridView

在上一教程中，我们创建了一个可编辑的 GridView，其中只包含两个字段，`ProductName` 和 `UnitPrice`。 这就需要为 `ProductsBLL` 类的 `UpdateProduct` 方法创建一个额外的重载，该重载只接受三个输入参数（产品的名称、单价和 ID）而不是每个产品字段的参数。 在本教程中，我们将再次练习此方法，创建可编辑的 GridView，其中显示产品的名称、每个单位的数量、单价和库存单位，但仅允许编辑股票的名称、单位价格和单位。

为了适应这种情况，我们需要 `UpdateProduct` 方法的另一个重载，该重载接受四个参数：产品名称、单位价格、库存单位和 ID。 将以下方法添加到 `ProductsBLL` 类：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample1.vb)]

此方法完成后，便可以创建 ASP.NET 页面，通过该页面可编辑这四个特定的产品字段。 打开 `EditInsertDelete` 文件夹中的 "`ErrorHandling.aspx`" 页，通过设计器将一个 GridView 添加到页面。 将 GridView 绑定到新的 ObjectDataSource，将 `Select()` 方法映射到 `ProductsBLL` 类的 `GetProducts()` 方法，并将 `Update()` 方法映射到刚刚创建的 `UpdateProduct` 重载。

[![使用接受四个输入参数的 UpdateProduct 方法重载](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image2.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image1.png)

**图 1**：使用接受四个输入参数的 `UpdateProduct` 方法重载（[单击以查看完全大小的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image3.png)）

这将创建一个具有四个参数的 `UpdateParameters` 集合和一个具有每个产品字段的字段的 ObjectDataSource。 ObjectDataSource 的声明性标记将值 `original_{0}`赋给 `OldValuesParameterFormatString` 属性，这将导致异常，因为我们的 BLL 类不期望传入一个名为 `original_productID` 的输入参数。 别忘了从声明性语法中完全删除此设置（或将其设置为默认值 `{0}`）。

接下来，削减将 GridView 分解为仅包含 `ProductName`、`QuantityPerUnit`、`UnitPrice`和 `UnitsInStock` BoundFields。 还可随意应用所需的任何字段级格式设置（例如，更改 `HeaderText` 属性）。

在上一教程中，我们介绍了如何在只读模式和编辑模式下将 `UnitPrice` BoundField 的格式设置为货币。 让我们在这里执行相同操作。 请记住，这需要将 BoundField 的 `DataFormatString` 属性设置为 `{0:c}`，其 `HtmlEncode` 属性 `false`，并将其 `ApplyFormatInEditMode` 为 `true`，如图2所示。

[![将 BoundField 配置为显示为货币](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image5.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image4.png)

**图 2**：将 `UnitPrice` BoundField 配置为显示为货币（[单击以查看完全大小的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image6.png)）

在编辑界面中将 `UnitPrice` 的格式设置为货币需要为 GridView 的 `RowUpdating` 事件创建事件处理程序，该事件处理程序将货币格式的字符串分析为 `decimal` 值。 请记住，最后一个教程中的 `RowUpdating` 事件处理程序也会检查以确保用户提供了 `UnitPrice` 值。 但是，在本教程中，我们将允许用户省略此价格。

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample2.vb)]

我们的 GridView 包含一个 `QuantityPerUnit` BoundField，但此 BoundField 应仅用于显示目的，不应由用户编辑。 为此，只需将 "BoundFields" `ReadOnly` 属性设置为 "`true`。

[![将 QuantityPerUnit BoundField 设置为只读](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image8.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image7.png)

**图 3**：使 `QuantityPerUnit` BoundField 为只读（[单击查看完全大小的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image9.png)）

最后，选中 "启用编辑" 复选框。 完成这些步骤后，`ErrorHandling.aspx` 页面的设计器应类似于图4所示。

[![删除所需的所有 BoundFields，并选中 "启用编辑" 复选框](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image11.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image10.png)

**图 4**：删除所需的所有 BoundFields，并选中 "启用编辑" 复选框（[单击查看完全大小的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image12.png)）

此时，我们有一个列表，其中包含所有产品的 "`ProductName`"、"`QuantityPerUnit`"、"`UnitPrice`" 和 "`UnitsInStock`" 字段;但是，只能编辑 `ProductName`、`UnitPrice`和 `UnitsInStock` 字段。

[![用户现在可以轻松地在库存域中编辑产品的名称、价格和单位](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image14.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image13.png)

**图 5**：用户现在可以轻松地在库存域中编辑产品的名称、价格和单位（[单击查看全尺寸图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image15.png)）

## <a name="step-2-gracefully-handling-dal-level-exceptions"></a>步骤2：妥善处理 DAL 级别的异常

虽然在用户为已编辑产品的名称、价格和库存单位输入合法值时，可编辑的 GridView wonderfully，但输入非法值会导致异常。 例如，省略 `ProductName` 值将导致引发[system.data.nonullallowedexception](https://msdn.microsoft.com/library/default.asp?url=/library/cpref/html/frlrfsystemdatanonullallowedexceptionclasstopic.asp) ，因为 `ProductsRow` 类中的 `ProductName` 属性将其 `AllowDBNull` 属性设置为 `false`;如果数据库关闭，则在尝试连接到数据库时，TableAdapter 会引发 `SqlException`。 在不执行任何操作的情况下，这些异常将从数据访问层向上冒泡到业务逻辑层，然后再冒泡到 ASP.NET 页，最后指向 ASP.NET 运行时。

根据你的 web 应用程序的配置方式以及是否要从 `localhost`访问应用程序，未经处理的异常可能会导致出现一般服务器错误页、详细的错误报告或用户友好的网页。 有关 ASP.NET 运行时如何响应未捕获的异常的详细信息，请参阅[ASP.NET 中的 Web 应用程序错误处理](http://www.15seconds.com/issue/030102.htm)和[customErrors 元素](https://msdn.microsoft.com/library/h0hfz6fc(VS.80).aspx)。

图6显示了在未指定 `ProductName` 值的情况下尝试更新产品时遇到的屏幕。 这是 `localhost`进入时显示的默认详细错误报告。

[省略产品名称的 ![将显示异常详细信息](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image17.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image16.png)

**图 6**：省略产品名称将显示异常详细信息（[单击以查看完全大小的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image18.png)）

虽然在测试应用程序时，此类异常详细信息很有用，但在发生异常的情况下，向最终用户呈现这样的屏幕并不是理想之选。 最终用户可能不知道 `NoNullAllowedException` 的原因或原因。 更好的方法是向用户提供一个更易于用户理解的消息，该消息说明在尝试更新产品时出现问题。

如果在执行该操作时出现异常，则 ObjectDataSource 和数据 Web 控件中的后期级别事件提供了一种方法来检测它并取消了从冒泡到 ASP.NET 运行时的异常。 在我们的示例中，让我们为 GridView 的 `RowUpdated` 事件创建事件处理程序，该事件确定是否已引发异常，如果是，则在标签 Web 控件中显示异常详细信息。

首先向 ASP.NET 页添加一个标签，将其 `ID` 属性设置为 `ExceptionDetails` 并清除其 `Text` 属性。 为了使用户注意此消息，请将其 `CssClass` 属性设置为 `Warning`，这是我们在上一教程中添加到 `Styles.css` 文件中的 CSS 类。 请记住，此 CSS 类会使标签的文本以红色、斜体、粗体、特大字体显示。

[![向页面添加标签 Web 控件](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image20.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image19.png)

**图 7**：将标签 Web 控件添加到页面（[单击以查看完全大小的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image21.png)）

由于我们希望此标签 Web 控件在异常发生之后立即显示，因此在 `Page_Load` 事件处理程序中将其 `Visible` 属性设置为 false：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample3.vb)]

在此代码中，在第一页上访问和后续回发 `ExceptionDetails` 控件将其 `Visible` 属性设置为 "`false`"。 在出现 DAL 或 BLL 级别的异常（可在 GridView 的 `RowUpdated` 事件处理程序中检测）的情况下，我们会将 `ExceptionDetails` 控件的 `Visible` 属性设置为 true。 由于 Web 控件事件处理程序在页面生命周期中的 `Page_Load` 事件处理程序之后发生，将显示标签。 但是，在下一次回发时，`Page_Load` 事件处理程序会将 `Visible` 属性还原到 `false`，再次将其从视图中隐藏。

> [!NOTE]
> 另外，还可以通过在声明性语法中将 `ExceptionDetails` 控件的 `Visible` 属性 `Visible` 指定为 `false`，并禁用其视图状态（将其 `EnableViewState` 属性设置为 `false`）来消除这 `Page_Load` 种需要。 我们将在以后的教程中使用这种替代方法。

添加 "标签" 控件后，下一步是为 GridView 的 `RowUpdated` 事件创建事件处理程序。 在设计器中选择 GridView，中转到 "属性窗口"，然后单击闪电形图标，并列出 GridView 的事件。 对于 GridView 的 `RowUpdating` 事件，应该已经有一个条目，因为我们在本教程前面部分为此事件创建了一个事件处理程序。 同时为 `RowUpdated` 事件创建事件处理程序。

![为 GridView 的 RowUpdated 事件创建事件处理程序](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image22.png)

**图 8**：创建 GridView `RowUpdated` 事件的事件处理程序

> [!NOTE]
> 还可以通过代码隐藏类文件顶部的下拉列表创建事件处理程序。 从左侧下拉列表中选择 "GridView"，然后从右侧的下拉列表中选择 "`RowUpdated`" 事件。

创建此事件处理程序会将以下代码添加到 ASP.NET 页的代码隐藏类：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample4.vb)]

此事件处理程序的第二个输入参数是[GridViewUpdatedEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdatedeventargs.aspx)类型的对象，它具有三个相关属性，用于处理异常：

- `Exception` 对引发的异常的引用;如果未引发任何异常，则此属性的值为 `null`
- `ExceptionHandled` 一个布尔值，该值指示是否已在 `RowUpdated` 事件处理程序中处理异常;如果 `false` （默认值），则会重新引发异常，percolating 到 ASP.NET 运行时
- 如果设置为，则 `KeepInEditMode` `true` 编辑的 GridView 行仍处于编辑模式;如果 `false` （默认值），GridView 行将恢复为其只读模式

然后，代码应检查是否 `Exception` 未 `null`，这意味着在执行该操作时引发了异常。 如果是这种情况，我们想要：

- 在 `ExceptionDetails` 标签中显示用户友好的消息
- 指示已处理异常
- 在编辑模式下保持 GridView 行

下面的代码将实现以下目标：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample5.vb)]

此事件处理程序首先检查是否 `null``e.Exception`。 如果不是，则将 `ExceptionDetails` 标签的 `Visible` 属性设置为 "`true`，并将其 `Text` 属性设置为" 更新产品时出现问题。 " 引发的实际异常的详细信息位于 `e.Exception` 对象的 `InnerException` 属性中。 检查此内部异常，如果它属于特定类型，则会向 `ExceptionDetails` 标签的 `Text` 属性追加额外的有用消息。 最后，"`ExceptionHandled`" 和 "`KeepInEditMode`" 属性均设置为 "`true`"。

图9显示了省略产品名称时此页的屏幕截图;图10显示了输入非法 `UnitPrice` 值时的结果（-50）。

[![ProductName BoundField 必须包含值](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image24.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image23.png)

**图 9**： `ProductName` BoundField 必须包含一个值（[单击以查看完全大小的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image25.png)）

[不允许使用 ![负的单价值](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image27.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image26.png)

**图 10**：不允许使用负值 `UnitPrice` 值（[单击查看完全大小的图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image28.png)）

通过将 `e.ExceptionHandled` 属性设置为 `true`，`RowUpdated` 事件处理程序表明它已处理了该异常。 因此，异常不会传播到 ASP.NET 运行时。

> [!NOTE]
> 图9和10显示了处理因无效用户输入而引发的异常的正常方式。 不过，理想情况下，此类无效输入永远不会到达业务逻辑层，因为在调用 `ProductsBLL` 类的 `UpdateProduct` 方法之前，ASP.NET 页应确保用户的输入有效。 在下一教程中，我们将了解如何向编辑和插入界面添加验证控件，以确保提交到业务逻辑层的数据符合业务规则。 在用户提供的数据有效之前，验证控件不仅会阻止调用 `UpdateProduct` 方法，还可以提供更丰富的用户体验来识别数据输入问题。

## <a name="step-3-gracefully-handling-bll-level-exceptions"></a>步骤3：妥善处理 BLL 级别的异常

在插入、更新或删除数据时，数据访问层可能会在遇到与数据相关的错误时引发异常。 数据库可能处于脱机状态、所需的数据库表列可能没有指定值，或者可能违反了表级约束。 除了与数据相关的严格异常外，业务逻辑层还可以使用异常来指示违反业务规则的时间。 例如，在[创建业务逻辑层](../introduction/creating-a-business-logic-layer-vb.md)教程中，我们向原始 `UpdateProduct` 重载添加了业务规则检查。 具体而言，如果用户将产品标记为 "已停用"，则需要该产品不是供应商提供的唯一产品。 如果违反此条件，则会引发 `ApplicationException`。

对于本教程中创建的 `UpdateProduct` 重载，让我们添加一条业务规则，禁止将 `UnitPrice` 字段设置为一个新值，该新值超过原始 `UnitPrice` 值的两倍。 若要实现此目的，请调整 `UpdateProduct` 重载，使其执行此检查，并在违反规则时引发 `ApplicationException`。 更新的方法如下：

[!code-vb[Main](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/samples/sample6.vb)]

进行这种更改后，现有价格的两倍以上的任何价格更新都将导致引发 `ApplicationException`。 就像从 DAL 引发的异常，可以在 GridView 的 `RowUpdated` 事件处理程序中检测并处理此 BLL 引发的 `ApplicationException`。 事实上，`RowUpdated` 事件处理程序的代码（如所编写的代码）将正确检测此异常，并显示 `ApplicationException`的 `Message` 属性值。 图11显示了当用户尝试将 Chai 的价格更新为 $50.00 时的屏幕截图，此价格超过了 $19.95 当前的2倍。

[![业务规则禁止价格增加，超过产品的价格](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image30.png)](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image29.png)

**图 11**：业务规则禁止价格增加，超过产品的价格（[单击查看全尺寸图像](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb/_static/image31.png)）

> [!NOTE]
> 理想情况下，我们的业务逻辑规则将从 `UpdateProduct` 方法重载中重构并转变为常见方法。 这就是读者的练习。

## <a name="summary"></a>总结

在插入、更新和删除操作期间，数据 Web 控件和 ObjectDataSource 都涉及到 bookend 实际操作的前期和后级事件。 正如我们在本教程中看到的那样，在使用可编辑的 GridView 时，将激发 GridView 的 `RowUpdating` 事件，后跟 ObjectDataSource 的 `Updating` 事件，此时会对 ObjectDataSource 的基础对象执行 update 命令。 操作完成后，将触发 ObjectDataSource 的 `Updated` 事件，后跟 GridView 的 `RowUpdated` 事件。

我们可以为前期事件创建事件处理程序，以便自定义输入参数或为后期级别事件自定义，以便检查并响应操作的结果。 后期级别事件处理程序最常用于检测在操作过程中是否发生了异常。 在出现异常时，这些后期级别事件处理程序可以选择自行处理异常。 在本教程中，我们介绍了如何通过显示友好错误消息来处理此类异常。

在下一教程中，我们将了解如何减小因数据格式问题（如输入消极 `UnitPrice`）引起的异常的可能性。 具体而言，我们将介绍如何向编辑和插入界面添加验证控件。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Liz Shulok。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)
> [下一页](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
