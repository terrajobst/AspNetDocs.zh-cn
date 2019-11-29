---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-cs
title: 处理 BLL 和 DAL 级别的异常（C#） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何 tactfully 在可编辑的 DataList 更新工作流过程中处理异常。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: f8fd58e2-f932-4f08-ab3d-fbf8ff3295d2
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/handling-bll-and-dal-level-exceptions-cs
msc.type: authoredcontent
ms.openlocfilehash: 35ff60be6ed67ea8d1bf226ae70f590100597757
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634123"
---
# <a name="handling-bll--and-dal-level-exceptions-c"></a>处理 BLL 和 DAL 级别的异常 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_38_CS.exe)或[下载 PDF](handling-bll-and-dal-level-exceptions-cs/_static/datatutorial38cs1.pdf)

> 在本教程中，我们将了解如何 tactfully 在可编辑的 DataList 更新工作流过程中处理异常。

## <a name="introduction"></a>简介

在 DataList 教程中[编辑和删除数据的概述](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)中，我们创建了一个 datalist，其中提供了简单的编辑和删除功能。 虽然完全正常运行，但它不是用户友好的，因为编辑或删除过程中出现的任何错误都将导致未经处理的异常。 例如，如果省略产品名称，或者在编辑产品时输入价格值 "非常经济实惠"，则会引发异常。 由于未在代码中捕获此异常，因此它冒泡到 ASP.NET 运行时，然后在网页中显示异常详细信息。

正如我们在[ASP.NET 页中处理 BLL 和 DAL 级别的异常](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)中看到的那样，如果从业务逻辑或数据访问层的深度引发异常，则会将异常详细信息返回到 ObjectDataSource，然后返回到 GridView。 我们了解到如何通过为 ObjectDataSource 或 GridView 创建 `Updated` 或 `RowUpdated` 事件处理程序来适当地处理这些异常，从而检查是否有异常，然后指示是否已处理异常。

不过，DataList 教程不使用 ObjectDataSource 来更新和删除数据。 相反，我们正在直接处理 BLL。 为了检测源自 BLL 或 DAL 的异常，我们需要在 ASP.NET 页面的代码隐藏内实现异常处理代码。 在本教程中，我们将了解如何使用更多 tactfully 处理在可编辑的 DataList s 更新工作流期间引发的异常。

> [!NOTE]
> 在 DataList 教程中*编辑和删除数据的概述*中，我们讨论了用于编辑和删除 datalist 中的数据的不同方法，这是使用 ObjectDataSource 进行更新和删除所涉及的一些技巧。 如果使用这些方法，则可以通过 ObjectDataSource `Updated` 或 `Deleted` 事件处理程序来处理 BLL 或 DAL 中的异常。

## <a name="step-1-creating-an-editable-datalist"></a>步骤1：创建可编辑的 DataList

在担心如何处理更新工作流中发生的异常之前，让我们先创建一个可编辑的 DataList。 打开 `EditDeleteDataList` 文件夹中的 "`ErrorHandling.aspx`" 页，将 DataList 添加到设计器，将其 `ID` 属性设置为 "`Products`"，然后添加名为 "`ProductsDataSource`" 的新 ObjectDataSource。 将 ObjectDataSource 配置为使用 `ProductsBLL` 类 `GetProducts()` 方法来选择记录;将插入、更新和删除选项卡中的下拉列表设置为 "（无）"。

[![使用 GetProducts （）方法返回产品信息](handling-bll-and-dal-level-exceptions-cs/_static/image2.png)](handling-bll-and-dal-level-exceptions-cs/_static/image1.png)

**图 1**：使用 `GetProducts()` 方法返回产品信息（[单击以查看完全大小的图像](handling-bll-and-dal-level-exceptions-cs/_static/image3.png)）

完成 ObjectDataSource 向导后，Visual Studio 将自动为 DataList 创建 `ItemTemplate`。 将此项替换为显示每个产品的名称和价格的 `ItemTemplate`，并包括 "编辑" 按钮。 接下来，创建一个具有 "名称"、"价格" 和 "更新" 和 "取消" 按钮的 TextBox Web 控件的 `EditItemTemplate`。 最后，将 DataList s `RepeatColumns` 属性设置为2。

进行这些更改后，页的声明性标记应如下所示。 仔细检查以确保 "编辑"、"取消" 和 "更新" 按钮的 `CommandName` 属性分别设置为 "编辑"、"取消" 和 "更新"。

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample1.aspx)]

> [!NOTE]
> 对于本教程，必须启用 DataList 的视图状态。

花点时间通过浏览器查看进度（参见图2）。

[每个产品 ![都包含 "编辑" 按钮](handling-bll-and-dal-level-exceptions-cs/_static/image5.png)](handling-bll-and-dal-level-exceptions-cs/_static/image4.png)

**图 2**：每个产品都包含一个 "编辑" 按钮（[单击以查看完全大小的图像](handling-bll-and-dal-level-exceptions-cs/_static/image6.png)）

目前，"编辑" 按钮仅导致回发，它尚未使产品变为可编辑状态。 若要启用编辑，需要为 DataList s `EditCommand`、`CancelCommand`和 `UpdateCommand` 事件创建事件处理程序。 `EditCommand` 和 `CancelCommand` 事件只更新 DataList s `EditItemIndex` 属性，然后将数据重新绑定到 DataList：

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample2.cs)]

`UpdateCommand` 事件处理程序更复杂一些。 它需要从 `DataKeys` 集合中读取所编辑的产品 `ProductID`，并从 `EditItemTemplate`中的文本框中读取产品的名称和价格，然后在将 DataList 返回到其预编辑状态之前调用 `ProductsBLL` 类 s `UpdateProduct` 方法。

现在，让我们在 DataList 教程中*编辑和删除数据的概述*中，只使用 `UpdateCommand` 事件处理程序中的完全相同的代码。 在步骤2中，我们将添加代码来适当地处理异常。

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample3.cs)]

如果输入的输入无效，可能采用格式不正确的单位价格的形式，则无效的单位价格值（如-$5.00）或省略产品的名称，将引发异常。 由于 `UpdateCommand` 事件处理程序此时不包括任何异常处理代码，因此，该异常将向上冒泡到 ASP.NET 运行时，它将显示给最终用户（请参阅图3）。

![发生未经处理的异常时，最终用户会看到错误页](handling-bll-and-dal-level-exceptions-cs/_static/image7.png)

**图 3**：当发生未处理的异常时，最终用户会看到错误页

## <a name="step-2-gracefully-handling-exceptions-in-the-updatecommand-event-handler"></a>步骤2：在 UpdateCommand 事件处理程序中正常处理异常

在更新工作流期间，`UpdateCommand` 事件处理程序、BLL 或 DAL 中可能出现异常。 例如，如果用户输入的价格太大，则 `UpdateCommand` 事件处理程序中的 `Decimal.Parse` 语句将引发 `FormatException` 异常。 如果用户省略产品名称，或者价格有负值，则 DAL 会引发异常。

发生异常时，我们希望在页面本身中显示信息性消息。 将标签 Web 控件添加到页面，其 `ID` 设置为 `ExceptionDetails`。 通过将标签文本的 `CssClass` 属性分配给在 `Styles.css` 文件中定义的 `Warning` CSS 类，将其配置为显示为红色、特大、粗体和斜体。

出现错误时，只需显示标签一次。 也就是说，在后续回发中，标签的警告消息将会消失。 这可以通过以下方式完成：清除标签 s `Text` 属性，或将其 `Visible` 属性设置为在 `Page_Load` 事件处理程序中 `False` （如我们在[ASP.NET 页教程中处理 BLL 和 DAL 级别的异常](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)）或禁用标签的视图状态支持。 使用后一种方法。

[!code-aspx[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample4.aspx)]

引发异常时，会将异常的详细信息分配给 `ExceptionDetails` 标签控件 `Text` 属性。 由于其视图状态处于禁用状态，因此在后续回发中，`Text` 属性的编程更改将丢失，恢复为默认文本（空字符串），从而隐藏警告消息。

若要确定何时引发错误以便在页面上显示有用的消息，需要将 `Try ... Catch` 块添加到 `UpdateCommand` 事件处理程序中。 `Try` 部分包含可能导致异常的代码，而 `Catch` 块包含在出现异常时执行的代码。 有关 `Try ... Catch` 块的详细信息，请查看 .NET Framework 文档中的 "[异常处理基础知识](https://msdn.microsoft.com/library/2w8f0bss.aspx)" 部分。

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample5.cs)]

当 `Try` 块内的代码引发任何类型的异常时，将开始执行 `Catch` 的代码块。 `DbException`、`NoNullAllowedException`、`ArgumentException`等引发的异常的类型取决于首先被错误的具体内容。 如果数据库级别出现问题，则会引发 `DbException`。 如果为 `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`或 `ReorderLevel` 字段输入了非法值，将引发 `ArgumentException`，因为我们添加了代码来验证 `ProductsDataTable` 类中的这些字段值（请参阅[创建业务逻辑层](../introduction/creating-a-business-logic-layer-cs.md)教程）。

我们可以通过基于所捕获异常的类型来对最终用户提供更有帮助的说明。 以下代码在[ASP.NET 页教程的处理 BLL 和 DAL 级别异常](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)中完全相同的窗体中提供了这一级别的详细信息：

[!code-csharp[Main](handling-bll-and-dal-level-exceptions-cs/samples/sample6.cs)]

若要完成本教程，只需从传入的 `Exception` 实例（`ex`）中 `Catch` 块调用 `DisplayExceptionDetails` 方法。

使用 `Try ... Catch` 块后，将向用户显示更丰富的错误消息，如图4和5所示。 请注意，在遇到异常的情况下，DataList 仍处于编辑模式。 这是因为，一旦发生异常，控制流立即被重定向到 `Catch` 块，绕过将 DataList 返回到其预编辑状态的代码。

[![如果用户省略了必填字段，则显示一条错误消息](handling-bll-and-dal-level-exceptions-cs/_static/image9.png)](handling-bll-and-dal-level-exceptions-cs/_static/image8.png)

**图 4**：如果用户省略了必填字段，将显示一条错误消息（[单击查看完全大小的图像](handling-bll-and-dal-level-exceptions-cs/_static/image10.png)）

[在输入负价格时，会显示一条错误消息 ![](handling-bll-and-dal-level-exceptions-cs/_static/image12.png)](handling-bll-and-dal-level-exceptions-cs/_static/image11.png)

**图 5**：输入负价格时显示错误消息（[单击查看全尺寸图像](handling-bll-and-dal-level-exceptions-cs/_static/image13.png)）

## <a name="summary"></a>总结

GridView 和 ObjectDataSource 提供了后端事件处理程序，这些处理程序包括有关在更新和删除工作流期间引发的任何异常的信息，以及可设置为指示异常是否已被设置的属性。妥善. 但是，在使用 DataList 并直接使用 BLL 时，这些功能不可用。 相反，我们负责实现异常处理。

在本教程中，我们介绍了如何通过将 `Try ... Catch` 块添加到 `UpdateCommand` 事件处理程序，将异常处理添加到可编辑的 DataList s 更新工作流。 如果在更新工作流的过程中引发了异常，则将执行 `Catch` 块代码，并在 `ExceptionDetails` 标签中显示有用的信息。

此时，DataList 不会执行任何操作来防止异常发生在第一位。 尽管我们知道负价格将导致异常，但我们尚未添加任何功能来主动阻止用户输入此类无效输入。 在下一教程中，我们将了解如何通过在 `EditItemTemplate`中添加验证控件来帮助减少因无效用户输入而导致的异常。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [异常的设计准则](https://msdn.microsoft.com/library/ms298399.aspx)
- [错误日志记录模块和处理程序（ELMAH）](http://workspaces.gotdotnet.com/elmah) （用于记录错误的开源库）
- [.NET Framework 2.0 的企业库](https://www.microsoft.com/downloads/details.aspx?familyid=5A14E870-406B-4F2A-B723-97BA84AE80B5&amp;displaylang=en)（包括异常管理应用程序块）

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Ken Pespisa。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](performing-batch-updates-cs.md)
> [下一页](adding-validation-controls-to-the-datalist-s-editing-interface-cs.md)
