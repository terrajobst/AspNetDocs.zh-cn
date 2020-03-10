---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
title: 删除时添加客户端确认（C#） |Microsoft Docs
author: rick-anderson
description: 到目前为止创建的接口中，用户在要单击 "编辑" 按钮时，可以通过单击 "删除" 按钮来意外删除数据。 在此 t 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: f6e2a12a-2b5e-48fd-8db3-1e94a500c19a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: e7d53bc65fdbbfa9ce9bfa5fbdbfa0dea598eebe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78479816"
---
# <a name="adding-client-side-confirmation-when-deleting-c"></a>删除时添加客户端确认 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_CS.exe)或[下载 PDF](adding-client-side-confirmation-when-deleting-cs/_static/datatutorial22cs1.pdf)

> 到目前为止创建的接口中，用户在要单击 "编辑" 按钮时，可以通过单击 "删除" 按钮来意外删除数据。 在本教程中，我们将添加一个在单击 "删除" 按钮时显示的客户端确认对话框。

## <a name="introduction"></a>简介

在过去的几个教程中，我们已了解如何结合使用我们的应用程序体系结构、ObjectDataSource 和数据 Web 控件来提供插入、编辑和删除功能。 到目前为止，我们已经检查过的删除接口由 "删除" 按钮组成，在单击该按钮时，将导致回发并调用 ObjectDataSource `Delete()` 方法。 然后，`Delete()` 方法从业务逻辑层调用配置的方法，该方法将调用向下传播到数据访问层，并向数据库发出实际的 `DELETE` 语句。

虽然此用户界面允许访问者通过 GridView、DetailsView 或 FormView 控件删除记录，但当用户单击 "删除" 按钮时，它不会有任何类型的确认。 如果用户想要单击 "编辑" 按钮时意外单击 "删除" 按钮，则会将其更新的记录改为删除。 为了帮助防止出现这种情况，在本教程中，我们将添加一个在单击 "删除" 按钮时显示的客户端确认对话框。

JavaScript `confirm(string)` 函数将其字符串输入参数显示为模式对话框内提供了两个按钮的文本（"确定" 和 "取消"）（请参阅图1）。 `confirm(string)` 函数根据单击的按钮（`true`，如果用户单击 "确定"，则返回布尔值; 如果用户单击 "取消"，则返回 `false`）。

![JavaScript confirm （string）方法显示模式的客户端 Messagebox](adding-client-side-confirmation-when-deleting-cs/_static/image1.png)

**图 1**： JavaScript `confirm(string)` 方法显示模式的客户端 Messagebox

提交表单时，如果从客户端事件处理程序返回 `false` 的值，则将取消窗体提交。 使用此功能，可以使 "删除" 按钮的客户端 `onclick` 事件处理程序返回对 `confirm("Are you sure you want to delete this product?")`的调用值。 如果用户单击 "取消"，`confirm(string)` 将返回 false，从而导致窗体提交取消。 如果没有回发，则单击 "删除" 按钮的产品不会被删除。 但是，如果用户在确认对话框中单击 "确定"，则回发将继续 unabated 并且将删除该产品。 有关此技术的详细信息，请参阅[使用 JavaScript s `confirm()` 方法控制窗体提交](http://www.webreference.com/programming/javascript/confirm/)。

如果使用模板，则添加所需的客户端脚本略有不同，因为使用 CommandField 时。 因此，在本教程中，我们将查看 FormView 和 GridView 示例。

> [!NOTE]
> 使用客户端确认技术（如本教程中所述的方法），假设用户正在访问支持 JavaScript 且已启用 JavaScript 的浏览器。 如果某个特定用户不满足上述任一假设，则单击 "删除" 按钮会立即导致回发（不显示 "确认" messagebox）。

## <a name="step-1-creating-a-formview-that-supports-deletion"></a>步骤1：创建支持删除的 FormView

首先将 FormView 添加到 `EditInsertDelete` 文件夹中的 `ConfirmationOnDelete.aspx` 页，将其绑定到新的 ObjectDataSource，该 ObjectDataSource 通过 `ProductsBLL` 类 `GetProducts()` 方法取回产品信息。 还要配置 ObjectDataSource，使 `ProductsBLL` 类 `DeleteProduct(productID)` 方法映射到 ObjectDataSource s `Delete()` 方法;确保 "插入和更新选项卡" 下拉列表设置为 "（无）"。 最后，选中 FormView s 智能标记中的 "启用分页" 复选框。

完成这些步骤后，新的 ObjectDataSource 声明性标记将如下所示：

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample1.aspx)]

正如我们过去在不使用开放式并发的示例中一样，请花一些时间来清除 ObjectDataSource 的 `OldValuesParameterFormatString` 属性。

由于它已绑定到仅支持删除的 ObjectDataSource 控件，因此 FormView s `ItemTemplate` 仅提供 "删除" 按钮，缺少 "新建" 和 "更新" 按钮。 不过，FormView 的声明性标记包含一个多余的 `EditItemTemplate` 和 `InsertItemTemplate`，可以将其删除。 请花片刻时间自定义 `ItemTemplate`，以便仅显示部分产品数据字段。 我配置了 "地雷"，以在其供应商和类别名称（连同 "删除" 按钮）上方的 `<h3>` 标题中显示产品名称。

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample2.aspx)]

进行这些更改后，我们提供了一个功能完备的网页，使用户能够一次切换产品，只需单击 "删除" 按钮即可删除产品。 图2显示了在浏览器中查看进度的屏幕截图。

[![FormView 显示单个产品的相关信息](adding-client-side-confirmation-when-deleting-cs/_static/image3.png)](adding-client-side-confirmation-when-deleting-cs/_static/image2.png)

**图 2**： FormView 显示了有关单个产品的信息（[单击查看完全尺寸的图像](adding-client-side-confirmation-when-deleting-cs/_static/image4.png)）

## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a>步骤2：从 "删除" 按钮的客户端 onclick 事件调用确认（string）函数

创建 FormView 后，最后一步是配置 "删除" 按钮，以便在访问者单击此按钮时，将调用 JavaScript `confirm(string)` 函数。 将客户端脚本添加到按钮、LinkButton 或 ImageButton s 客户端 `onclick` 事件可以通过使用 `OnClientClick property`（ASP.NET 2.0 的新增操作）来实现。 由于我们希望返回 `confirm(string)` 函数的值，因此只需将以下属性设置为： `return confirm('Are you certain that you want to delete this product?');`

完成此更改后，删除 LinkButton 的声明性语法应类似于：

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample3.aspx)]

就是这样！ 图3显示了此确认在操作中的屏幕截图。 单击 "删除" 按钮会打开 "确认" 对话框。 如果用户单击 "取消"，则将取消回发并不删除产品。 不过，如果用户单击 "确定"，则回发将继续，并且会调用 ObjectDataSource `Delete()` 方法，将删除数据库记录中的 culminating。

> [!NOTE]
> 传递到 `confirm(string)` JavaScript 函数的字符串用撇号分隔（而不是引号）。 在 JavaScript 中，可以使用任意一个字符来分隔字符串。 此处使用了撇号，以便 `confirm(string)` 传递给中的字符串的分隔符不会对 `OnClientClick` 属性值使用分隔符引入歧义。

[![在单击 "删除" 按钮时显示确认](adding-client-side-confirmation-when-deleting-cs/_static/image6.png)](adding-client-side-confirmation-when-deleting-cs/_static/image5.png)

**图 3**：当单击 "删除" 按钮时，现在会显示一个确认（[单击以查看完全大小的图像](adding-client-side-confirmation-when-deleting-cs/_static/image7.png)）

## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a>步骤3：为 CommandField 中的 "删除" 按钮配置 OnClientClick 属性

直接在模板中使用 Button、LinkButton 或 ImageButton 时，只需将确认对话框 `OnClientClick` 配置为返回 JavaScript `confirm(string)` 函数的结果，就可以将该对话框与关联。 但是，CommandField-将 "删除" 按钮的字段添加到 GridView 或 DetailsView，没有可通过声明方式进行设置的 `OnClientClick` 属性。 相反，我们必须以编程方式引用 GridView 或 DetailsView 中适用 `DataBound` 事件处理程序的 "删除" 按钮，然后在此处设置其 `OnClientClick` 属性。

> [!NOTE]
> 在适当的 `DataBound` 事件处理程序中设置 "删除" 按钮 `OnClientClick` 属性时，我们有权访问数据并将其绑定到当前记录。 这意味着我们可以扩展确认消息以包含有关特定记录的详细信息，例如 "是否确实要删除 Chai 产品？" 使用数据绑定语法，也可以在模板中进行此类自定义。

若要练习为 CommandField 中的 "删除" 按钮设置 `OnClientClick` 属性，请向页面中添加一个 GridView。 将此 GridView 配置为使用 FormView 使用的相同 ObjectDataSource 控件。 还将 BoundFields 限制为仅包括产品名称、类别和供应商。 最后，选中 "启用" 复选框。 这会将 CommandField 添加到 GridView `Columns` 集合，并将其 `ShowDeleteButton` 属性设置为 "`true`"。

进行这些更改后，GridView 的声明性标记应如下所示：

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample4.aspx)]

CommandField 包含单个 Delete LinkButton 实例，该实例可通过 GridView `RowDataBound` 事件处理程序以编程方式进行访问。 引用后，可以相应地设置其 `OnClientClick` 属性。 使用以下代码为 `RowDataBound` 事件创建事件处理程序：

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample5.cs)]

此事件处理程序可用于数据行（将具有 "删除" 按钮的行），并以编程方式引用 "删除" 按钮开始。 通常使用以下模式：

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample6.cs)]

*ButtonType*是 CommandField、LinkButton 或 ImageButton 使用的按钮类型。 默认情况下，CommandField 使用 LinkButtons，但这可以通过 CommandField s `ButtonType property`进行自定义。 *CommandFieldIndex*是 GridView `Columns` 集合中 CommandField 的序号索引，而*controlIndex*是 CommandField s `Controls` 集合内的 "删除" 按钮的索引。 *ControlIndex*值取决于按钮相对于 CommandField 中的其他按钮的位置。 例如，如果 CommandField 中显示的唯一按钮是 "删除" 按钮，请使用的索引为0。 但是，如果在 "删除" 按钮之前有一个 "编辑" 按钮，请使用索引2。 使用索引2的原因是，"删除" 按钮之前的 CommandField 添加了两个控件： "编辑" 按钮和用于在 "编辑" 和 "删除" 按钮之间添加一些空间的 LiteralControl。

对于我们的特定示例，CommandField 使用 LinkButtons，而是最左侧的字段，其*commandFieldIndex*为0。 由于 CommandField 中没有其他按钮，而删除按钮，我们使用的*controlIndex*为0。

引用 CommandField 中的 "删除" 按钮后，接下来将获取与当前 GridView 行绑定的产品有关的信息。 最后，我们将 "删除" 按钮 `OnClientClick` 属性设置为相应的 JavaScript，其中包括产品名称。 由于传递到 `confirm(string)` 函数的 JavaScript 字符串是使用撇号分隔的，因此，必须对出现在产品名内的任何撇号进行转义。 特别是，产品名称中的任何撇号都用 "`\'`" 进行转义。

完成这些更改后，在 GridView 中单击 "删除" 按钮将显示 "自定义确认" 对话框（请参阅图4）。 与 FormView 的确认消息一样，如果用户单击 "取消"，则会取消回发，从而阻止发生删除。

> [!NOTE]
> 此方法还可用于以编程方式访问 DetailsView 中 CommandField 的 "删除" 按钮。 但对于 DetailsView，为 `DataBound` 事件创建事件处理程序，因为 DetailsView 没有 `RowDataBound` 事件。

[![单击 GridView 的 "删除" 按钮将显示 "自定义确认" 对话框](adding-client-side-confirmation-when-deleting-cs/_static/image9.png)](adding-client-side-confirmation-when-deleting-cs/_static/image8.png)

**图 4**：单击 GridView 的 "删除" 按钮将显示 "自定义确认" 对话框（[单击以查看完全大小的图像](adding-client-side-confirmation-when-deleting-cs/_static/image10.png)）

## <a name="using-templatefields"></a>使用 Templatefield

CommandField 的缺点之一是必须通过索引访问其按钮，并且必须将生成的对象强制转换为相应的按钮类型（Button、LinkButton 或 ImageButton）。 使用 "幻数" 和硬编码类型会导致在运行时之前无法发现的问题。 例如，如果你或另一个开发人员在未来的某个时间（例如 "编辑" 按钮）向 CommandField 添加了新按钮，或更改了 `ButtonType` 属性，则现有代码仍将编译而不出错，但访问此页可能会导致异常或意外的行为，具体取决于代码的编写方式和所做的更改。

另一种方法是将 GridView 和 DetailsView s CommandFields 转换为 Templatefield。 这将生成一个 TemplateField，其中包含一个 `ItemTemplate`，该具有 CommandField 中每个按钮的 LinkButton （或按钮或 ImageButton）。 可以通过声明方式分配这些按钮 `OnClientClick` 属性（如我们在 FormView 中看到的那样），也可以使用以下模式以编程方式在相应的 `DataBound` 事件处理程序中进行访问：

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample7.cs)]

其中， *controlID*是按钮 `ID` 属性的值。 虽然此模式仍需要强制转换的硬编码类型，但它无需对索引进行索引，因此布局可以更改，而不会导致运行时错误。

## <a name="summary"></a>摘要

JavaScript `confirm(string)` 函数是用于控制窗体提交工作流的常用方法。 执行时，该函数将显示一个模式客户端对话框，其中包含两个按钮，即 "确定" 和 "取消"。 如果用户单击 "确定"，`confirm(string)` 函数将返回 `true`;单击 "取消" 将返回 `false`。 此功能与浏览器的行为相结合，如果提交过程中的事件处理程序返回 `false`，则可用于在删除记录时显示确认消息。

`confirm(string)` 函数可以通过 control s `OnClientClick` 属性与按钮 Web 控件 s 客户端 `onclick` 事件处理程序关联。 在模板中使用 "删除" 按钮时-无论是在某个 FormView 的模板中，还是在 DetailsView 或 GridView 的 TemplateField 中使用，都可以通过声明方式或编程方式设置此属性，如本教程中所述。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一页](implementing-optimistic-concurrency-cs.md)
> [下一页](limiting-data-modification-functionality-based-on-the-user-cs.md)
