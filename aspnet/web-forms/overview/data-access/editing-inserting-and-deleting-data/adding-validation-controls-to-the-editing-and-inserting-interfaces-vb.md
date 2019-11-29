---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
title: 向编辑和插入界面添加验证控件（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将了解如何轻松地将验证控件添加到数据 Web 控件的 EditItemTemplate 和则中，以提供更多 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: e3d7028a-7a22-4a4f-babe-d53afc41c0e2
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c5ad110ee0836f0a464b02a2b29254e2e06381e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74571345"
---
# <a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-vb"></a>向编辑和插入界面添加验证控件 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_VB.exe)或[下载 PDF](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/datatutorial19vb1.pdf)

> 在本教程中，我们将了解如何轻松地将验证控件添加到数据 Web 控件的 EditItemTemplate 和则，以提供更可靠的用户界面。

## <a name="introduction"></a>简介

我们在过去三个教程中探讨过的示例中的 GridView 和 DetailsView 控件都包含 BoundFields 和 CheckBoxFields （在将 GridView 或 DetailsView 绑定到数据源时，Visual Studio 自动添加的字段类型）控制智能标记）。 在 GridView 或 DetailsView 中编辑行时，那些不是只读的 BoundFields 将转换为文本框，最终用户可以从这些文本框中修改现有数据。 同样，在将新记录插入到 DetailsView 控件中时，`InsertVisible` 属性设置为 `True` （默认值）的那些 BoundFields 将呈现为空文本框，用户可以在其中提供新记录的字段值。 同样，在标准只读接口中禁用的 CheckBoxFields 在编辑和插入界面中转换为启用的复选框。

尽管 BoundField 和 CheckBoxField 的默认编辑和插入界面都很有用，但接口缺乏任何类型的验证。 如果用户进行数据输入错误（例如省略 `ProductName` 字段或为 `UnitsInStock` 输入无效值（如-50），则将从应用程序体系结构的深度中引发异常。 尽管可以正常处理此异常，如[前一教程](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)中所示，理想情况下，编辑或插入用户界面应包括验证控件，以防止用户首先输入这样的无效数据。

为了提供自定义的编辑或插入界面，需要将 BoundField 或 CheckBoxField 替换为 TemplateField。 Templatefield 是在 GridView 控件中[使用 templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)和在[DetailsView 控件教程中使用 templatefield](../custom-formatting/using-templatefields-in-the-detailsview-control-vb.md)中讨论的主题，可以包含多个模板，用于为不同的行状态定义单独的接口。 TemplateField 的 `ItemTemplate` 用于在 DetailsView 或 GridView 控件中呈现只读字段或行，而 `EditItemTemplate` 和 `InsertItemTemplate` 分别指示用于编辑和插入模式的接口。

在本教程中，我们将了解如何轻松地将验证控件添加到 TemplateField 的 `EditItemTemplate` 和 `InsertItemTemplate` 以提供更加可靠的用户界面。 具体而言，本教程采用在[检查与插入、更新和删除教程关联的事件](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)中创建的示例，并补充编辑和插入界面以包括适当的验证。

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deletingexamining-the-events-associated-with-inserting-updating-and-deleting-vbmd"></a>步骤1：复制示例[以检查与插入、更新和删除相关的事件](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)

在[检查与插入、更新和删除教程关联的事件](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)中，我们创建了一个页面，其中列出了可编辑 GridView 中产品的名称和价格。 此外，此页还包括一个 DetailsView，其中 `DefaultMode` 属性设置为 `Insert`，因此始终以插入模式呈现。 从这一 DetailsView，用户可以输入新产品的名称和价格，单击 "插入"，然后将其添加到系统中（请参阅图1）。

[![前面的示例，用户可以添加新产品并编辑现有产品](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image1.png)

**图 1**：前面的示例允许用户添加新产品并编辑现有产品（[单击以查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image3.png)）

本教程的目标是增加 DetailsView 和 GridView 来提供验证控件。 具体而言，我们的验证逻辑将：

- 要求在插入或编辑产品时提供名称
- 需要在插入记录时提供价格;编辑一条记录时，我们仍需要价格，但将使用在之前的教程中已经存在的 GridView `RowUpdating` 事件处理程序中的编程逻辑
- 确保为 "价格" 输入的值是有效的货币格式

首先，我们需要将示例从 `DataModificationEvents.aspx` 页复制到本教程的页面，`UIValidation.aspx`，然后才能了解如何增强前面的示例以包括验证。 若要实现此目的，我们需要同时复制 `DataModificationEvents.aspx` 页面的声明性标记及其源代码。 首先，通过执行以下步骤，通过声明性标记进行复制：

1. 在 Visual Studio 中打开 `DataModificationEvents.aspx` 页面
2. 中转到页面的声明性标记（单击页面底部的 "源" 按钮）
3. 复制 `<asp:Content>` 和 `</asp:Content>` 标记（第3行到第44行）中的文本，如图2所示。

[![复制 &lt;asp： Content&gt; 控件中的文本](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image4.png)

**图 2**：复制 `<asp:Content>` 控件中的文本（[单击查看完全尺寸的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image6.png)）

1. 打开 `UIValidation.aspx` 页面
2. 中转到页面的声明性标记
3. 将文本粘贴到 `<asp:Content>` 控件中。

若要复制源代码，请打开 `DataModificationEvents.aspx.vb` 页面并只复制 `EditInsertDelete_DataModificationEvents` 类*中*的文本。 复制三个事件处理程序（`Page_Load`、`GridView1_RowUpdating`和 `ObjectDataSource1_Inserting`），但不要**复制类**声明。 将复制*的文本粘贴到 `UIValidation.aspx.vb`* 中的 `EditInsertDelete_UIValidation` 类中。

将内容和代码移到 `DataModificationEvents.aspx` 到 `UIValidation.aspx`后，请花点时间在浏览器中测试进度。 在这两个页面中，你应看到相同的输出和体验相同的功能（请参阅图1，了解 `DataModificationEvents.aspx` 操作中的屏幕截图）。

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>步骤2：将 BoundFields 转换为 Templatefield

若要向编辑和插入界面添加验证控件，需要将 DetailsView 和 GridView 控件使用的 BoundFields 转换为 Templatefield。 若要实现此目的，请分别单击 "编辑列" 和 "编辑字段" 链接。 在该字段中，选择每个 BoundFields，并单击 "将此字段转换为 TemplateField" 链接。

[![将每个 DetailsView 和 GridView 的 BoundFields 转换为 Templatefield](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image7.png)

**图 3**：将每个 DetailsView 和 GridView 的 BoundFields 转换为 Templatefield （[单击以查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image9.png)）

通过 "字段" 对话框将 BoundField 转换为 TemplateField 时，将生成一个 TemplateField，该显示与 BoundField 本身相同的只读、编辑和插入接口。 下面的标记显示了在 DetailsView 转换为 TemplateField 后，DetailsView 中的 `ProductName` 字段的声明性语法：

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample1.aspx)]

请注意，此 TemplateField 会自动创建三个模板 `ItemTemplate`、`EditItemTemplate`和 `InsertItemTemplate`。 `ItemTemplate` 使用标签 Web 控件显示单个数据字段值（`ProductName`），而 `EditItemTemplate` 和 `InsertItemTemplate` 在 TextBox Web 控件中显示数据字段值，该控件会使用双向数据绑定将数据字段与文本框的 `Text` 属性相关联。 由于我们仅在此页中使用 DetailsView 来插入，因此你可以从两个 Templatefield 中删除 `ItemTemplate` 和 `EditItemTemplate`，不过，这并不会对保留它们有任何损害。

由于 GridView 不支持 DetailsView 的内置插入功能，因此将 GridView 的 `ProductName` 字段转换为 TemplateField 将仅生成 `ItemTemplate` 并 `EditItemTemplate`：

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample2.aspx)]

单击 "将此字段转换为 TemplateField" 后，Visual Studio 将创建一个 TemplateField，其模板模拟已转换 BoundField 的用户界面。 可以通过浏览器访问此页来验证这一点。 你会发现，Templatefield 的外观和行为与改用 BoundFields 时的体验相同。

> [!NOTE]
> 根据需要随意自定义模板中的编辑界面。 例如，我们可能希望 `UnitPrice` Templatefield 中的文本框呈现为小于 `ProductName` 文本框的文本框。 若要实现此目的，可以将文本框的 `Columns` 属性设置为适当的值，或通过 `Width` 属性提供绝对宽度。 在下一教程中，我们将了解如何通过将文本框替换为备用数据输入 Web 控件来完全自定义编辑界面。

## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>步骤3：将验证控件添加到 GridView 的`EditItemTemplate`

构造数据输入窗体时，用户必须输入必填字段，并且提供的所有输入都是合法的格式正确的值，这一点非常重要。 为了帮助确保用户的输入有效，ASP.NET 提供了五个内置的验证控件，这些控件旨在用于验证单个输入控件的值：

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx)确保已提供值
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx)根据另一个 Web 控件值或常数值验证值，或确保该值的格式对于指定的数据类型是合法的
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx)可确保值在值范围内
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx)根据[正则表达式](http://en.wikipedia.org/wiki/Regular_expression)验证值
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx)根据自定义的用户定义方法验证值

有关这五个控件的详细信息，请参阅[ASP.NET 快速入门教程](https://asp.net/QuickStart/aspnet/)中的 "[验证控件" 部分](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx)。

对于本教程，我们将需要在 detailsview 和 GridView `ProductName` Templatefield 中使用 RequiredFieldValidator，并在 DetailsView 的 `UnitPrice` TemplateField 中使用 RequiredFieldValidator。 此外，我们还需要将 CompareValidator 添加到这两个控件的 `UnitPrice` Templatefield，以确保输入的价格的值大于或等于0，并且以有效的货币格式呈现。

> [!NOTE]
> 尽管 ASP.NET 1.x 具有这些相同的五个验证控件，但 ASP.NET 2.0 已增加了许多改进，主要两个是 Internet Explorer 之外的浏览器的客户端脚本支持，并能够将页面上的验证控件分区到验证组。 有关2.0 中的新验证控制功能的详细信息，请参阅[二级 the ASP.NET 2.0 中的验证控件](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)。

首先，将必要的验证控件添加到 GridView Templatefield 中的 `EditItemTemplate`。 若要实现此目的，请在 GridView 的智能标记中单击 "编辑模板" 链接，以打开模板编辑界面。 从这里，你可以从下拉列表中选择要编辑的模板。 由于我们要增加编辑界面，因此我们需要将验证控件添加到 `ProductName`，并 `UnitPrice`的 `EditItemTemplate`。

[![我们需要扩展 ProductName 和 EditItemTemplates 的](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image10.png)

**图 4**：需要扩展 `ProductName` 和 `UnitPrice`的 `EditItemTemplate` （[单击以查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image12.png)）

在 "`ProductName`" `EditItemTemplate`中，通过将 RequiredFieldValidator 拖放到模板编辑界面中来添加一个，并将其放置在文本框后面。

[![将 RequiredFieldValidator 添加到 ProductName EditItemTemplate](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image13.png)

**图 5**：将 RequiredFieldValidator 添加到 `ProductName` `EditItemTemplate` （[单击查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image15.png)）

所有验证控件都是通过验证单个 ASP.NET Web 控件的输入来完成的。 因此，我们需要指出，我们刚刚添加的 RequiredFieldValidator 应根据 `EditItemTemplate`中的文本框进行验证;这是通过将验证控件的[ControlToValidate 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx)设置为相应 Web 控件的 `ID` 来完成的。 文本框当前具有 `TextBox1`的 nondescript `ID`，但我们将其更改为更合适的内容。 单击模板中的文本框，然后从属性窗口将 `ID` 从 `TextBox1` 更改为 `EditProductName`。

[![将文本框的 ID 改为 EditProductName](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image16.png)

**图 6**：将文本框的 `ID` 更改为 `EditProductName` （[单击以查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image18.png)）

接下来，将 RequiredFieldValidator 的 `ControlToValidate` 属性设置为 `EditProductName`。 最后，将[ErrorMessage 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx)设置为 "必须提供产品名称"，将[Text 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx)设置为 "\*"。 如果验证失败，则 `Text` 属性值（如果提供）是验证控件显示的文本。 ValidationSummary 控件使用所需的 `ErrorMessage` 属性值;如果省略 `Text` 属性值，则 `ErrorMessage` 属性值也是验证控件在无效输入上显示的文本。

设置 RequiredFieldValidator 的这三个属性后，屏幕应类似于图7所示。

[![设置 RequiredFieldValidator 的 ControlToValidate、ErrorMessage 和 Text 属性](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image19.png)

**图 7**：设置 RequiredFieldValidator 的 `ControlToValidate`、`ErrorMessage`和 `Text` 属性（[单击以查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image21.png)）

将 RequiredFieldValidator 添加到 `ProductName` `EditItemTemplate`后，剩下的就是将必要的验证添加到 `UnitPrice` `EditItemTemplate`。 由于我们决定，在编辑记录时，`UnitPrice` 是可选的，因此，不需要添加 RequiredFieldValidator。 但是，我们需要添加一个 CompareValidator，以确保 `UnitPrice`（如提供）的格式正确设置为货币，并且大于或等于0。

将 CompareValidator 添加到 `UnitPrice` `EditItemTemplate`之前，让我们先将 TextBox Web 控件的 ID 从 `TextBox2` 更改为 `EditUnitPrice`。 做出此更改后，添加 CompareValidator，将其 `ControlToValidate` 属性设置为 `EditUnitPrice`，其 `ErrorMessage` 属性设置为 "该价格必须大于或等于零，并且不能包含货币符号"，并将其 `Text` 属性设置为 "\*"。

若要指示 `UnitPrice` 值必须大于或等于0，请将 CompareValidator 的[Operator 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx)设置为 "`GreaterThanEqual`，将其[ValueToCompare 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx)设置为" 0 "，并将其[Type 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx)设置为" `Currency`"。 以下声明性语法显示了进行这些更改之后 `UnitPrice` TemplateField 的 `EditItemTemplate`：

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample3.aspx)]

进行这些更改后，在浏览器中打开该页。 如果在编辑产品时尝试省略名称或输入无效价格值，则文本框的旁边会出现一个星号。 如图8所示，包含货币符号（如 $19.95）的价格值被视为无效。 CompareValidator 的 `Currency` `Type` 允许使用数字分隔符（如逗号或句点）和前导加号或减号，但*不允许货币*符号。 此行为可能会 perplex 用户，因为编辑界面当前使用货币格式呈现 `UnitPrice`。

> [!NOTE]
> 请记住，在*与插入、更新和删除教程关联的事件*中，我们将 BoundField 的 `DataFormatString` 属性设置为 `{0:c}`，以便将其设置为货币格式。 而且，我们将 `ApplyFormatInEditMode` 属性设置为 "true"，这会导致 GridView 的编辑界面将 `UnitPrice` 的格式设置为货币。 将 BoundField 转换为 TemplateField 时，Visual Studio 会记下这些设置，并使用数据绑定语法 `<%# Bind("UnitPrice", "{0:c}") %>`将文本框的 `Text` 属性的格式设置为货币。

[![带有无效输入的文本框旁边显示星号](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image22.png)

**图 8**：包含无效输入的文本框旁边显示一个星号（[单击以查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image24.png)）

当验证按原样工作时，用户必须在编辑记录时手动删除货币符号，这是不可接受的。 为此，我们有三个选项：

1. 将 `EditItemTemplate` 配置为将 `UnitPrice` 值设置为货币格式。
2. 允许用户通过删除 CompareValidator 来输入货币符号，并将其替换为正确检查正确格式货币值的 RegularExpressionValidator。 此处的问题在于，用于验证货币值的正则表达式并不是很好，如果我们想要合并区域性设置，则需要编写代码。
3. 完全移除验证控件，并依赖于 GridView `RowUpdating` 事件处理程序中的服务器端验证逻辑。

对于本练习，我们将提供选项 #1。 由于 `EditItemTemplate`： `<%# Bind("UnitPrice", "{0:c}") %>`中文本框的数据绑定表达式，当前 `UnitPrice` 被设置为货币格式。 将 Bind 语句更改为 `Bind("UnitPrice", "{0:n2}")`，该语句将结果的格式设置为具有两位数精度的数字。 这可以直接通过声明性语法或从 `UnitPrice` TemplateField 的 `EditItemTemplate` 中的 `EditUnitPrice` 文本框中单击 "编辑数据绑定" 链接来完成（请参阅图9和10）。

[![单击文本框的 "编辑 databinding" 链接](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image25.png)

**图 9**：单击文本框的 "编辑 databinding" 链接（[单击以查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image27.png)）

[![在 Bind 语句中指定格式说明符](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image28.png)

**图 10**：在 `Bind` 语句中指定格式说明符（[单击以查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image30.png)）

进行此更改后，编辑界面中的格式化价格以逗号作为组分隔符，将句点作为小数点分隔符，但保留货币符号。

> [!NOTE]
> `UnitPrice` `EditItemTemplate` 不包含 RequiredFieldValidator，允许回发到不幸和更新逻辑来开始。 但是，从*检查与插入、更新和删除教程关联的事件*中复制的 `RowUpdating` 事件处理程序包括以编程方式进行检查，以确保提供 `UnitPrice`。 随意删除此逻辑，按原样保留，或将 RequiredFieldValidator 添加到 `UnitPrice` `EditItemTemplate`。

## <a name="step-4-summarizing-data-entry-problems"></a>步骤4：汇总数据输入问题

除了五个验证控件外，ASP.NET 还包含[ValidationSummary 控件](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)，该控件显示检测到无效数据的那些验证控件的 `ErrorMessage`。 此摘要数据可以在网页上或通过模式的客户端 messagebox 显示为文本。 让我们来增强本教程，使其包括客户端 messagebox，其中汇总了所有验证问题。

若要实现此目的，请将 ValidationSummary 控件从工具箱拖到设计器上。 验证控件的位置并不重要，因为我们要将它配置为仅将摘要显示为 messagebox。 添加控件后，将其[ShowSummary 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx)设置为 "`False`"，并将其[ShowMessageBox 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx)设置为 "`True`"。 添加此项后，会在客户端 messagebox 中汇总任何验证错误。

[![在客户端 Messagebox 中汇总验证错误](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image31.png)

**图 11**：在客户端 Messagebox 中汇总验证错误（[单击以查看完全大小的映像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image33.png)）

## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>步骤5：将验证控件添加到 DetailsView 的`InsertItemTemplate`

本教程剩下的所有工作就是将验证控件添加到 DetailsView 的插入界面。 将验证控件添加到 DetailsView 的模板的过程与步骤3中所述的过程相同。因此，在此步骤中，我们将逐步完成该任务。 正如我们在 GridView 的 `EditItemTemplate` 中所做的那样，我建议您将 nondescript `TextBox1` 和 `TextBox2` 中的文本框 `ID` 重命名为 `InsertProductName` 和 `InsertUnitPrice`。

将 RequiredFieldValidator 添加到 `ProductName` `InsertItemTemplate`。 将 `ControlToValidate` 设置为模板中文本框的 `ID`，其 `Text` 属性设置为 "\*"，将其 `ErrorMessage` 属性设置为 "必须提供产品名称"。

由于在添加新记录时此页需要 `UnitPrice`，因此请将 RequiredFieldValidator 添加到 `UnitPrice` `InsertItemTemplate`，并相应地设置其 `ControlToValidate`、`Text`和 `ErrorMessage` 属性。 最后，将 CompareValidator 添加到 `UnitPrice` `InsertItemTemplate`，同时配置其 `ControlToValidate`、`Text`、`ErrorMessage`、`Type`、`Operator`和 `ValueToCompare` 属性，就像我们在 GridView 的 `UnitPrice`中使用 `EditItemTemplate`的 CompareValidator 一样。

添加这些验证控件后，如果未提供其名称或者其价格为负数或非法格式，则不能将新产品添加到系统中。

[已将 ![验证逻辑添加到 DetailsView 的插入界面](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image34.png)

**图 12**：已将验证逻辑添加到 DetailsView 的插入界面（[单击以查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image36.png)）

## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>步骤6：将验证控件分区为验证组

我们的页面包含两个逻辑上不同的验证控件集：它们对应于 GridView 的编辑界面，后者对应于 DetailsView 的插入界面。 默认情况下，当发生回发时，将检查页上的*所有*验证控件。 但是，在编辑记录时，我们不想要验证 DetailsView 的插入界面的验证控件。 图13说明了当用户使用完全合法的值编辑产品时的当前难题，单击 "更新" 将导致验证错误，因为插入界面中的名称和价格值为空。

[更新产品 ![会导致插入接口的验证控件激发](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image37.png)

**图 13**：更新产品会导致插入接口的验证控件激发（[单击查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image39.png)）

可以通过 `ValidationGroup` 属性将 ASP.NET 2.0 中的验证控件分区为验证组。 若要将组中的一组验证控件关联起来，只需将其 `ValidationGroup` 属性设置为相同的值。 对于本教程，请将 GridView Templatefield 中验证控件的 `ValidationGroup` 属性设置为 "`EditValidationControls`，并将 DetailsView 的 Templatefield 的 `ValidationGroup` 属性设置为" `InsertValidationControls`"。 使用设计器的编辑模板界面时，可以直接在声明性标记中或通过属性窗口来完成这些更改。

除了验证控件外，ASP.NET 2.0 中与按钮和按钮相关的控件也包含 `ValidationGroup` 属性。 仅当回发由具有相同 `ValidationGroup` 属性设置的按钮引发时，才检查验证组的验证程序的有效性。 例如，为了使 DetailsView 的 "插入" 按钮触发 `InsertValidationControls` 验证组，我们需要将 CommandField 的 `ValidationGroup` 属性设置为 "`InsertValidationControls`" （参见图14）。 此外，将 GridView 的 CommandField's `ValidationGroup` 属性设置为 `EditValidationControls`。

[![将 DetailsView 的 CommandField's ValidationGroup 属性设置为 InsertValidationControls](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image40.png)

**图 14**：将 DetailsView 的 CommandField's `ValidationGroup` 属性设置为 "`InsertValidationControls`[" （单击查看完全大小的图像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image42.png)）

进行这些更改后，DetailsView 和 GridView 的 Templatefield 和 CommandFields 应类似于以下内容：

DetailsView 的 Templatefield 和 CommandField

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample4.aspx)]

GridView 的 CommandField 和 Templatefield

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample5.aspx)]

此时，仅当单击了 GridView 的 "更新" 按钮并且特定于插入的验证控件仅在单击 DetailsView 的 "插入" 按钮时才会触发特定于编辑的验证控件，解决图13突出显示的问题。 但是，在这种情况下，当输入无效数据时，ValidationSummary 控件将不再显示。 ValidationSummary 控件还包含 `ValidationGroup` 属性，并且仅在其验证组中显示这些验证控件的摘要信息。 因此，在此页中需要有两个验证控件，一个用于 `InsertValidationControls` 验证组，另一个用于 `EditValidationControls`。

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample6.aspx)]

完成本教程后，我们的教程已完成！

## <a name="summary"></a>总结

尽管 BoundFields 可以提供插入和编辑接口，但接口不可自定义。 通常，我们想要向编辑和插入界面添加验证控件，以确保用户以合法格式输入所需的输入。 若要实现此目的，必须将 BoundFields 转换为 Templatefield，并将验证控件添加到相应的模板。 在本教程中，我们扩展了*检查与插入、更新和删除教程相关的事件*的示例，同时向 DetailsView 的插入界面和 GridView 的编辑界面添加验证控件。 此外，我们还了解了如何使用 ValidationSummary 控件显示摘要验证信息，以及如何将页面上的验证控件分为不同的验证组。

正如我们在本教程中看到的那样，Templatefield 允许对编辑和插入界面进行扩展，以包括验证控件。 还可以对 Templatefield 进行扩展以包含其他输入 Web 控件，使文本框替换为更适合的 Web 控件。 在下一教程中，我们将了解如何使用数据绑定 DropDownList 控件替换 TextBox 控件，这是编辑外键（如 `Products` 表中的 `CategoryID` 或 `SupplierID`）的理想选择。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Liz Shulok 和 Zack。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
> [下一页](customizing-the-data-modification-interface-vb.md)
