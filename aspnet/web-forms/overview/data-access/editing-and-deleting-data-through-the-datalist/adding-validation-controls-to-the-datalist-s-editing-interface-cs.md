---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-cs
title: 向 DataList 的编辑界面（C#）添加验证控件 |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何轻松地将验证控件添加到 DataList 的 EditItemTemplate 中，以便为用户提供更可靠的编辑用户 int 。
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 3ecc21c5-da0e-40ab-abb4-fac1e47398ad
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/adding-validation-controls-to-the-datalist-s-editing-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: e3c14b7098da832bd28f57026e81dcb7f7ba7130
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78480854"
---
# <a name="adding-validation-controls-to-the-datalists-editing-interface-c"></a>向 DataList 的编辑界面添加验证控件 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_39_CS.exe)或[下载 PDF](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/datatutorial39cs1.pdf)

> 在本教程中，我们将了解如何轻松地将验证控件添加到 DataList 的 EditItemTemplate 中，以便提供更可靠的编辑用户界面。

## <a name="introduction"></a>简介

在迄今为止的 DataList 编辑教程中，DataLists 编辑界面未包含任何主动用户输入验证，即使无效的用户输入（如缺少产品名称或负价格），也不会导致异常。 在[前面的教程](handling-bll-and-dal-level-exceptions-cs.md)中，我们介绍了如何将异常处理代码添加到 DataList s `UpdateCommand` 事件处理程序中，以便捕获并正确地显示有关引发的任何异常的信息。 但理想情况下，编辑界面会包括验证控件，以防止用户首先输入这样的无效数据。

在本教程中，我们将了解如何轻松地将验证控件添加到 DataList s `EditItemTemplate` 中，以便提供更可靠的编辑用户界面。 具体而言，本教程采用前面教程中创建的示例，并补充编辑界面以包括适当的验证。

## <a name="step-1-replicating-the-example-fromhandling-bll--and-dal-level-exceptions"></a>步骤1：复制示例以[处理 BLL 和 DAL 级别的异常](handling-bll-and-dal-level-exceptions-cs.md)

在[处理 BLL 和 DAL 级别的异常](handling-bll-and-dal-level-exceptions-cs.md)教程中，我们创建了一个页面，其中列出了两列的可编辑 DataList 中产品的名称和价格。 本教程的目标是增加 DataList 的编辑界面以包括验证控件。 具体而言，我们的验证逻辑将：

- 要求提供产品名称
- 确保为 "价格" 输入的值是有效的货币格式
- 确保为价格输入的值大于或等于零，因为负 `UnitPrice` 值是非法的

首先，我们需要将本教程的 "`ErrorHandling.aspx`" 页中的示例从 `EditDeleteDataList` 文件夹中的 "" 页复制到本教程的页面，`UIValidation.aspx`。 若要实现此目的，我们需要通过 `ErrorHandling.aspx` 页的声明性标记及其源代码进行复制。 首先，通过执行以下步骤，通过声明性标记进行复制：

1. 在 Visual Studio 中打开 `ErrorHandling.aspx` 页面
2. 中转到页面声明性标记（单击页面底部的 "源" 按钮）
3. 复制 `<asp:Content>` 和 `</asp:Content>` 标记（第3行到第32行）中的文本，如图1所示。

[![复制 &lt;asp： Content&gt; 控件中的文本](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image2.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image1.png)

**图 1**：复制 `<asp:Content>` 控件中的文本（[单击查看完全尺寸的图像](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image3.png)）

1. 打开 `UIValidation.aspx` 页面
2. 中转到页面声明性标记
3. 将文本粘贴到 `<asp:Content>` 控件中。

若要复制源代码，请打开 `ErrorHandling.aspx.vb` 页面并只复制 `EditDeleteDataList_ErrorHandling` 类*中*的文本。 将三个事件处理程序（`Products_EditCommand`、`Products_CancelCommand`和 `Products_UpdateCommand`）与 `DisplayExceptionDetails` 方法**一起复制，但不要复制类**声明或 `using` 语句。 将复制*的文本粘贴到 `UIValidation.aspx.vb`* 中的 `EditDeleteDataList_UIValidation` 类中。

将内容和代码移到 `ErrorHandling.aspx` 到 `UIValidation.aspx`后，请花点时间在浏览器中测试页面。 在这两个页面中，你应看到相同的输出和体验相同的功能（请参阅图2）。

[![UIValidation 页面模拟 ErrorHandling 中的功能](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image5.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image4.png)

**图 2**： `UIValidation.aspx` 页模拟 `ErrorHandling.aspx` 中的功能（[单击查看完全大小的图像](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image6.png)）

## <a name="step-2-adding-the-validation-controls-to-the-datalist-s-edititemtemplate"></a>步骤2：将验证控件添加到 DataList s EditItemTemplate

构造数据输入窗体时，用户必须输入所有必填字段，并且其提供的所有输入都是合法的格式正确的值，这一点非常重要。 为了帮助确保用户的输入有效，ASP.NET 提供了五个用于验证单个输入 Web 控件的值的内置验证控件：

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx)确保已提供值
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx)根据另一个 Web 控件值或常数值验证值，或确保值 s 格式对于指定的数据类型是合法的
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx)可确保值在值范围内
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx)根据[正则表达式](http://en.wikipedia.org/wiki/Regular_expression)验证值
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx)根据自定义的用户定义方法验证值

有关这五个控件的详细信息，请参阅将[验证控件添加到编辑和插入接口](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)教程或查看[ASP.NET 快速入门教程](https://quickstarts.asp.net)中的 "[验证控件" 部分](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/validation/default.aspx)。

在本教程中，我们将需要使用 RequiredFieldValidator 来确保已提供产品名称的值，并使用 CompareValidator 确保输入的价格的值大于或等于0，并且以有效的货币格式显示。

> [!NOTE]
> 尽管 ASP.NET 1.x 具有这些相同的五个验证控件，但 ASP.NET 2.0 已增加了许多改进，主要两个是浏览器的客户端脚本支持，除了 Internet Explorer 外，还可以将页上的验证控件分区为验证组。 有关2.0 中的新验证控制功能的详细信息，请参阅[二级 the ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)。

首先，让我们将必要的验证控件添加到 DataList s `EditItemTemplate`。 可以通过在设计器中单击 DataList s 智能标记或声明性语法中的 "编辑模板" 链接来执行此任务。 让我们使用设计视图中的 "编辑模板" 选项逐步执行该过程。 选择编辑 DataList `EditItemTemplate`后，通过将其从 "工具箱" 拖放到模板编辑界面中来添加 RequiredFieldValidator，并将其放置在 "`ProductName`" 文本框之后。

[![在 "ProductName" 文本框后面添加 RequiredFieldValidator 到 EditItemTemplate](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image8.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image7.png)

**图 3**：将 RequiredFieldValidator 添加到 "`ProductName`" 文本框 `EditItemTemplate After` （[单击以查看完全大小的图像](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image9.png)）

所有验证控件都是通过验证单个 ASP.NET Web 控件的输入来完成的。 因此，我们需要指出，我们刚刚添加的 RequiredFieldValidator 应该针对 `ProductName` 文本框进行验证;完成此操作的方法是：将[`ControlToValidate` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx)的验证控件设置为相应 Web 控件的 `ID` （在此实例中为`ProductName`）。 接下来，将[`ErrorMessage` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx)设置为，则必须将产品的名称和[`Text` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx)提供给 \*。 如果验证失败，则 `Text` 属性值（如果提供）是验证控件显示的文本。 ValidationSummary 控件使用所需的 `ErrorMessage` 属性值;如果省略 `Text` 属性值，则验证控件将对无效输入显示 `ErrorMessage` 属性值。

设置 RequiredFieldValidator 的这三个属性后，屏幕应类似于图4所示。

[![设置 RequiredFieldValidator s ControlToValidate、ErrorMessage 和 Text 属性](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image11.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image10.png)

**图 4**：设置 RequiredFieldValidator `ControlToValidate`、`ErrorMessage`和 `Text` 属性（[单击以查看完全大小的图像](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image12.png)）

将 RequiredFieldValidator 添加到 `EditItemTemplate`后，剩下的就是为 "产品价格" 文本框添加必要的验证。 由于 `UnitPrice` 在编辑记录时是可选的，因此我们不需要添加 RequiredFieldValidator。 但是，我们需要添加一个 CompareValidator，以确保 `UnitPrice`（如提供）的格式正确设置为货币，并且大于或等于0。

将 CompareValidator 添加到 `EditItemTemplate` 中，并将其 `ControlToValidate` 属性设置为 `UnitPrice`，其 "`ErrorMessage`" 属性值必须大于或等于零，并且不能包含货币符号，并将其 `Text` 属性添加到 "\*"。 若要指示 `UnitPrice` 值必须大于或等于0，请将 CompareValidator s [`Operator` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx)设置为 `GreaterThanEqual`，将其[`ValueToCompare` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx)设置为0，并将其[`Type` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx)设置为 `Currency`。

添加这两个验证控件后，DataList s `EditItemTemplate` 的声明性语法应类似于以下形式：

[!code-aspx[Main](adding-validation-controls-to-the-datalist-s-editing-interface-cs/samples/sample1.aspx)]

进行这些更改后，在浏览器中打开该页。 如果在编辑产品时尝试省略名称或输入无效价格值，则文本框的旁边会出现一个星号。 如图5所示，包含货币符号（如 $19.95）的价格值被视为无效。 CompareValidator s `Currency` `Type` 允许使用数字分隔符（如逗号或句点，具体取决于区域性设置）和前导加号或减号，但*不允许货币*符号。 此行为可能会 perplex 用户，因为编辑界面当前使用货币格式呈现 `UnitPrice`。

[![带有无效输入的文本框旁边显示星号](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image14.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image13.png)

**图 5**：在包含无效输入的文本框旁边显示一个星号（[单击以查看完全大小的图像](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image15.png)）

当验证按原样工作时，用户必须在编辑记录时手动删除货币符号，这是不可接受的。 此外，如果编辑界面中有无效输入，则在单击 "更新" 或 "取消" 按钮时，将调用回发。 理想情况下，"取消" 按钮会将 DataList 返回到其预编辑状态，而不考虑用户输入的有效性。 此外，在更新 DataList `UpdateCommand` 事件处理程序中的产品信息之前，我们需要确保页数据有效，因为浏览器不支持 JavaScript 或禁用其支持时，用户可以绕过验证控件客户端逻辑。

## <a name="removing-the-currency-symbol-from-the-edititemtemplate-s-unitprice-textbox"></a>从 "EditItemTemplate" 的 "单价" 文本框中删除货币符号

使用 CompareValidator `Currency``Type`时，正在验证的输入不能包含任何货币符号。 此类符号的存在导致 CompareValidator 将输入标记为 "无效"。 不过，编辑界面当前在 "`UnitPrice`" 文本框中包含一个货币符号，这意味着用户必须在保存其更改之前显式删除该货币符号。 为此，我们有三个选项：

1. 将 `EditItemTemplate` 配置为不将 `UnitPrice` TextBox 值设置为货币格式。
2. 允许用户通过删除 CompareValidator 来输入货币符号，并将其替换为 RegularExpressionValidator 检查格式是否正确的货币值。 此处的难题是，用于验证货币值的正则表达式与 CompareValidator 简单，并且如果要合并区域性设置，则需要编写代码。
3. 完全移除验证控件，并依赖于 GridView `RowUpdating` 事件处理程序中的自定义服务器端验证逻辑。

在本教程中，让我们通过选项1。 由于 `EditItemTemplate`： `<%# Eval("UnitPrice", "{0:c}") %>`中文本框的数据绑定表达式，当前 `UnitPrice` 被设置为货币值的格式。 将 `Eval` 语句更改为 `Eval("UnitPrice", "{0:n2}")`，这将结果的格式设置为具有两位精度的数字。 这可以直接通过声明性语法来完成，也可以通过单击 DataList s `EditItemTemplate`的 "`UnitPrice`" 文本框中的 "编辑 databinding" 链接来完成。

进行此更改后，编辑界面中的格式化价格以逗号作为组分隔符，将句点作为小数点分隔符，但保留货币符号。

> [!NOTE]
> 从可编辑界面中删除货币格式时，我发现将货币符号放置在文本框外的文本很有用。 这是用户不需要提供货币符号的提示。

## <a name="fixing-the-cancel-button"></a>修复 "取消" 按钮

默认情况下，验证 Web 控件发出 JavaScript 以在客户端执行验证。 单击 "Button"、"LinkButton" 或 "ImageButton" 时，将在客户端上检查页上的验证控件，然后进行回发。 如果有任何无效数据，则取消回发。 但对于某些按钮，数据的有效性可能是重要;在这种情况下，由于无效数据导致回发已取消，因此是一种干扰。

"取消" 按钮是一个示例。 假设用户输入的数据无效，如省略产品名称，然后决定不想在所有的产品之后保存产品并点击 "取消" 按钮。 当前，"取消" 按钮用于触发页面上的验证控件，该控件报告产品名称缺失并阻止回发。 用户必须在 "`ProductName`" 文本框中键入一些文本，才能取消编辑过程。

幸运的是，按钮、LinkButton 和 ImageButton 具有一个[`CausesValidation` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.causesvalidation.aspx)，该属性可以指示单击按钮是否应启动验证逻辑（默认为 `True`）。 将 "取消" 按钮 `CausesValidation` 属性设置为 `False`。

## <a name="ensuring-the-inputs-are-valid-in-the-updatecommand-event-handler"></a>确保输入在 UpdateCommand 事件处理程序中有效

由于验证控件发出的客户端脚本，如果用户输入了无效输入，则验证控件将取消按钮、LinkButton 或 ImageButton 控件启动的任何回发，其 `CausesValidation` 属性是 `True` （默认值）。 但是，如果用户使用陈旧浏览器访问，或其 JavaScript 支持已禁用的浏览器，则不会执行客户端验证检查。

所有 ASP.NET 验证控件会在回发时立即重复其验证逻辑，并通过[`Page.IsValid` 属性](https://msdn.microsoft.com/library/system.web.ui.page.isvalid.aspx)报告页面输入的整体有效性。 但是，不会根据 `Page.IsValid`的值，以任何方式中断或停止页面流。 作为开发人员，我们负责确保 `Page.IsValid` 属性的值为 `True`，然后再继续执行采用有效输入数据的代码。

如果用户禁用了 JavaScript，请访问我们的页面，编辑产品，输入价格值太大，然后单击 "更新" 按钮，客户端验证将被绕过，而回发会不幸。 在回发时，ASP.NET 页 s `UpdateCommand` 事件处理程序执行，在尝试分析 `Decimal`的资源太昂贵时，将引发异常。 由于我们有异常处理，因此将适当处理此类异常，但如果 `Page.IsValid` 的值为 `True`，则只能通过 `UpdateCommand` 事件处理程序来阻止无效数据在第一次遍历。

将以下代码添加到 `UpdateCommand` 事件处理程序的开头，紧跟在 `Try` 块之前：

[!code-csharp[Main](adding-validation-controls-to-the-datalist-s-editing-interface-cs/samples/sample2.cs)]

通过此添加，产品将尝试仅在提交的数据有效时进行更新。 由于验证控制客户端脚本，大多数用户将无法回发无效数据，但是浏览器不支持 JavaScript 或禁用了 JavaScript 支持的用户可以绕过客户端检查并提交无效数据。

> [!NOTE]
> 敏锐读取器会回忆到，在通过 GridView 更新数据时，我们不需要在页面代码隐藏类中显式检查 `Page.IsValid` 属性。 这是因为 GridView 会询问我们的 `Page.IsValid` 属性，只在返回值为 `True`时才继续更新。

## <a name="step-3-summarizing-data-entry-problems"></a>步骤3：汇总数据输入问题

除了五个验证控件外，ASP.NET 还包含[ValidationSummary 控件](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)，该控件显示检测到无效数据的那些验证控件的 `ErrorMessage`。 此摘要数据可以在网页上或通过模式的客户端 messagebox 显示为文本。 让我们增加本教程，使其包括客户端 messagebox，汇总所有验证问题。

若要实现此目的，请将 ValidationSummary 控件从工具箱拖到设计器上。 ValidationSummary 控件的位置并不重要，因为我们会将其配置为仅将摘要显示为 messagebox。 添加控件后，将其[`ShowSummary` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx)设置为 "`False`"，并将其[`ShowMessageBox` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx)设置为 "`True`"。 添加此项后，会在客户端 messagebox 中汇总验证错误（参见图6）。

[![在客户端 Messagebox 中汇总验证错误](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image17.png)](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image16.png)

**图 6**：在客户端 Messagebox 中汇总验证错误（[单击以查看完全大小的映像](adding-validation-controls-to-the-datalist-s-editing-interface-cs/_static/image18.png)）

## <a name="summary"></a>摘要

在本教程中，我们介绍了如何通过使用验证控件主动确保用户输入有效，然后再尝试在更新工作流中使用它们，从而降低异常的可能性。 ASP.NET 提供了五个验证 Web 控件，这些控件旨在检查特定的 Web 控件的输入，并返回输入的有效性。 在本教程中，我们使用这五个控件中的两个控件 RequiredFieldValidator 和 CompareValidator，以确保已提供产品的名称，并且价格的货币格式值大于或等于零。

向 DataList 的编辑界面添加验证控件就像将它们从工具箱拖动到 `EditItemTemplate`，再设置几个属性一样简单。 默认情况下，验证控件会自动发出客户端验证脚本;它们还提供对回发的服务器端验证，将累积结果存储在 `Page.IsValid` 属性中。 若要在单击按钮、LinkButton 或 ImageButton 时绕过客户端验证，请将按钮 `CausesValidation` 属性设置为 `False`。 此外，在对回发提交的数据执行任何任务之前，请确保 `Page.IsValid` 属性返回 `True`。

到目前为止，我们已经检查过的所有 DataList 编辑教程都有非常简单的编辑界面，其中包含产品名称的文本框和价格。 不过，编辑界面可以包含不同的 Web 控件，如 DropDownLists、日历、单选按钮、复选框等。 在下一教程中，我们将介绍如何构建使用各种 Web 控件的接口。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管评审者是 Dennis Patterson 将、Ken Pespisa 和 Liz Shulok。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](handling-bll-and-dal-level-exceptions-cs.md)
> [下一页](customizing-the-datalist-s-editing-interface-cs.md)
