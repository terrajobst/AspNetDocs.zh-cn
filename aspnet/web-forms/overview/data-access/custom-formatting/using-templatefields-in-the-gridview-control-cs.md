---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
title: 在 GridView 控件中使用 Templatefield （C#） |Microsoft Docs
author: rick-anderson
description: 为了提供灵活性，GridView 提供了使用模板呈现的 TemplateField。 模板可以包括静态 HTML、Web 控件和 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 11de31e8-a78a-4f96-bd75-66e994175902
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-gridview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: ec17a16d7bb487d1c5cacf2d5971bbeffc1ba031
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78481724"
---
# <a name="using-templatefields-in-the-gridview-control-c"></a>在 GridView 控件中使用 TemplateField (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_12_CS.exe)或[下载 PDF](using-templatefields-in-the-gridview-control-cs/_static/datatutorial12cs1.pdf)

> 为了提供灵活性，GridView 提供了使用模板呈现的 TemplateField。 模板可以包括静态 HTML、Web 控件和数据绑定语法的混合。 在本教程中，我们将探讨如何使用 TemplateField 通过 GridView 控件实现更好的自定义。

## <a name="introduction"></a>简介

GridView 由一组字段构成，这些字段指示 `DataSource` 中的哪些属性将包括在呈现的输出中以及如何显示数据。 最简单的字段类型为 BoundField，它将数据值显示为文本。 其他字段类型使用替换 HTML 元素显示数据。 例如，CheckBoxField 呈现为复选框处于选中状态的复选框，它取决于指定数据字段的值;ImageField 呈现图像源基于指定数据字段的图像。 其状态取决于基础数据字段值的超链接和按钮可以使用 HyperLinkField 和 ButtonField 字段类型呈现。

尽管 "CheckBoxField"、"ImageField"、"HyperLinkField" 和 "ButtonField" 字段类型允许数据的备用视图，但它们在格式设置方面仍然非常有限。 CheckBoxField 只能显示单个复选框，而 ImageField 只能显示单个图像。 如果特定字段需要显示某些文本、复选框*和*图像，所有这些都基于不同的数据字段值呢？ 或者，如果我们想要使用除复选框、图像、超链接或按钮之外的 Web 控件显示数据？ 而且，BoundField 将其显示限制为单个数据字段。 如果要在单个 GridView 列中显示两个或更多数据字段值，该怎么办？

为了适应这一级别的灵活性，GridView 提供了使用*模板*呈现的 TemplateField。 模板可以包括静态 HTML、Web 控件和数据绑定语法的混合。 此外，TemplateField 还提供了各种模板，可用于自定义不同情况下的呈现。 例如，默认情况下，`ItemTemplate` 使用来呈现每行的单元格，但 `EditItemTemplate` 模板可用于自定义编辑数据时的接口。

在本教程中，我们将探讨如何使用 TemplateField 通过 GridView 控件实现更好的自定义。 在[前面的教程](custom-formatting-based-upon-data-cs.md)中，我们看到了如何使用 `DataBound` 和 `RowDataBound` 事件处理程序基于基础数据自定义格式设置。 基于基础数据自定义格式设置的另一种方法是从模板内调用格式设置方法。 在本教程中，我们还将介绍此技术。

对于本教程，我们将使用 Templatefield 自定义员工列表的外观。 具体而言，我们将列出所有员工，但会在一列中显示雇员的名字和姓氏，在日历控件中显示其雇佣日期，并显示一个状态列，指示在公司使用了多少天。

[![三个 Templatefield 用于自定义显示](using-templatefields-in-the-gridview-control-cs/_static/image2.png)](using-templatefields-in-the-gridview-control-cs/_static/image1.png)

**图 1**：三个 Templatefield 用于自定义显示（[单击以查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image3.png)）

## <a name="step-1-binding-the-data-to-the-gridview"></a>步骤1：将数据绑定到 GridView

在需要使用 Templatefield 自定义外观的报告方案中，我发现首先创建一个只包含 BoundFields 的 GridView 控件，然后添加新 Templatefield 或将现有 BoundFields 转换为根据需要 Templatefield。 因此，让我们通过设计器将一个 GridView 添加到页面，并将其绑定到一个返回雇员列表的 ObjectDataSource 来开始学习本教程。 这些步骤将为每个员工字段创建一个包含 BoundFields 的 GridView。

打开 "`GridViewTemplateField.aspx`" 页，并将 GridView 从工具箱拖到设计器上。 从 GridView 的智能标记中，选择添加调用 `EmployeesBLL` 类的 `GetEmployees()` 方法的新 ObjectDataSource 控件。

[![添加调用 GetEmployees （）方法的新 ObjectDataSource 控件](using-templatefields-in-the-gridview-control-cs/_static/image5.png)](using-templatefields-in-the-gridview-control-cs/_static/image4.png)

**图 2**：添加调用 `GetEmployees()` 方法的新 ObjectDataSource 控件（[单击以查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image6.png)）

以这种方式绑定 GridView 会自动为每个雇员属性添加 BoundField： `EmployeeID`、`LastName`、`FirstName`、`Title`、`HireDate`、`ReportsTo`和 `Country`。 对于此报表，请不要干扰显示 `EmployeeID`、`ReportsTo`或 `Country` 属性。 若要删除这些 BoundFields，可以：

- 使用 "字段" 对话框单击 GridView 的智能标记上的 "编辑列" 链接可显示此对话框。 接下来，从左下方列表中选择 BoundFields，然后单击红色 X 按钮以删除 BoundField。
- 从 "源" 视图手动编辑 GridView 的声明性语法，删除要删除的 BoundField 的 `<asp:BoundField>` 元素。

删除 `EmployeeID`、`ReportsTo`和 `Country` BoundFields 后，GridView 的标记应如下所示：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample1.aspx)]

花点时间在浏览器中查看进度。 此时，你应该会看到一个表，其中包含每个员工的记录和四列：一个用于员工的姓氏，一个用于名字，一个用于标题，另一个用于其雇佣日期。

[为每个员工显示 "姓氏"、"名字"、"标题" 和 "雇佣日期" 字段 ![](using-templatefields-in-the-gridview-control-cs/_static/image8.png)](using-templatefields-in-the-gridview-control-cs/_static/image7.png)

**图 3**：为每个雇员显示 `LastName`、`FirstName`、`Title`和 `HireDate` 字段（[单击查看完全尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image9.png)）

## <a name="step-2-displaying-the-first-and-last-names-in-a-single-column"></a>步骤2：在单个列中显示姓氏和名字

目前，每个雇员的名字和姓氏都显示在单独的列中。 改为将它们合并到单个列中可能会很好。 若要实现此目的，我们需要使用 TemplateField。 我们可以添加新的 TemplateField，向其添加所需的标记和数据绑定语法，然后删除 `FirstName` 和 `LastName` BoundFields，也可以将 `FirstName` BoundField 转换为 TemplateField，编辑 TemplateField 以包含 `LastName` 值，然后删除 `LastName` BoundField。

这两种方法的结果都是相同的，但我想将 BoundFields 转换为 Templatefield （如果可能），因为转换会自动添加 `ItemTemplate`，`EditItemTemplate` 并使用 Web 控件和数据绑定语法来模拟 BoundField 的外观和功能。 优点在于，转换过程将为我们执行一些工作，因此我们需要执行更少的 TemplateField 工作。

若要将现有 BoundField 转换为 TemplateField，请在 GridView 的智能标记中单击 "编辑列" 链接，并打开 "字段" 对话框。 从左下角的列表中选择要转换的 BoundField，然后单击右下角的 "将此字段转换为 TemplateField" 链接。

[从 "字段" 对话框 ![将 BoundField 转换为 TemplateField](using-templatefields-in-the-gridview-control-cs/_static/image11.png)](using-templatefields-in-the-gridview-control-cs/_static/image10.png)

**图 4**：从 "字段" 对话框将 BoundField 转换为 TemplateField （[单击以查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image12.png)）

继续将 `FirstName` BoundField 转换为 TemplateField。 此更改后，设计器中没有敏锐差异。 这是因为，将 BoundField 转换为 TemplateField 会创建一个 TemplateField，用于维护 BoundField 的外观。 尽管在设计器的这一点，此转换过程已将 BoundField 的声明性语法 `<asp:BoundField DataField="FirstName" HeaderText="FirstName" SortExpression="FirstName" />` 替换为以下 TemplateField 语法：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample2.aspx)]

如您所见，TemplateField 包含两个模板 `ItemTemplate`，该标签的标签 `Text` 属性设置为 "`FirstName` 数据" 字段的值，以及一个带有 `Text` 属性的 TextBox 控件的 `EditItemTemplate` 也设置为 `FirstName` 数据字段。 数据绑定语法 `<%# Bind("fieldName") %>`-指示将数据字段 *`fieldName`* 绑定到指定的 Web 控件属性。

若要将 `LastName` 数据字段值添加到此 TemplateField，需要在 `ItemTemplate` 中添加另一个标签 Web 控件，并将其 `Text` 属性绑定到 `LastName`。 这可以手动完成，也可以通过设计器完成。 若要手动执行此操作，只需将相应的声明性语法添加到 `ItemTemplate`：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample3.aspx)]

若要通过设计器添加该设计器，请单击 GridView 的智能标记上的 "编辑模板" 链接。 这会显示 GridView 的模板编辑界面。 此接口的智能标记是 GridView 中模板的列表。 由于目前只有一个 TemplateField，因此下拉列表中列出的模板只是 `FirstName` TemplateField 的模板以及 `EmptyDataTemplate` 和 `PagerTemplate`。 如果已指定，则使用 `EmptyDataTemplate` 模板来呈现 GridView 的输出（如果绑定到 GridView 的数据没有结果）;如果指定，则使用 `PagerTemplate`为支持分页的 GridView 呈现分页接口。

[![可以通过设计器编辑 GridView 的模板](using-templatefields-in-the-gridview-control-cs/_static/image14.png)](using-templatefields-in-the-gridview-control-cs/_static/image13.png)

**图 5**：可以通过设计器编辑 GridView 的模板（[单击以查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image15.png)）

若要在 `FirstName` TemplateField 中显示 `LastName`，请将 "标签" 控件从 "工具箱" 拖动到 GridView 的模板编辑界面中的 `FirstName` TemplateField 的 `ItemTemplate` 中。

[![将标签 Web 控件添加到 FirstName TemplateField 的 ItemTemplate](using-templatefields-in-the-gridview-control-cs/_static/image17.png)](using-templatefields-in-the-gridview-control-cs/_static/image16.png)

**图 6**：将标签 Web 控件添加到 `FirstName` TemplateField 的 ItemTemplate （[单击以查看完全大小的映像](using-templatefields-in-the-gridview-control-cs/_static/image18.png)）

此时，添加到 TemplateField 的标签 Web 控件的 `Text` 属性设置为 "标签"。 需要对此进行更改，以便将此属性改为绑定到 `LastName` 数据字段的值。 为此，请单击 "标签" 控件的智能标记，然后选择 "编辑绑定" 选项。

[![从标签的智能标记选择 "编辑 databinding" 选项](using-templatefields-in-the-gridview-control-cs/_static/image20.png)](using-templatefields-in-the-gridview-control-cs/_static/image19.png)

**图 7**：从标签的智能标记选择 "编辑 Databinding" 选项（[单击以查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image21.png)）

这会显示 "绑定" 对话框。 从这里，你可以从左侧的列表中选择要参与数据绑定的属性，并从右侧的下拉列表中选择要将数据绑定到的字段。 选择左侧的 "`Text`" 属性，`LastName` 然后单击 "确定"。

[![将 Text 属性绑定到 LastName 数据字段](using-templatefields-in-the-gridview-control-cs/_static/image23.png)](using-templatefields-in-the-gridview-control-cs/_static/image22.png)

**图 8**：将 `Text` 属性绑定到 `LastName` 数据字段（[单击查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image24.png)）

> [!NOTE]
> "数据绑定" 对话框允许您指示是否执行双向数据绑定。 如果不选中此项，将使用 databinding 语法 `<%# Eval("LastName")%>` 而不是 `<%# Bind("LastName")%>`。 这两种方法都适用于本教程。 插入和编辑数据时，双向数据绑定变得非常重要。 但对于简单地显示数据，这两种方法都能正常工作。 我们将在以后的教程中详细讨论双向数据绑定。

请花点时间查看浏览器中的此页。 如您所见，GridView 仍包含四列;但 `FirstName` 列现在*同时*列出了 "`FirstName`" 和 "`LastName` 数据" 字段值。

[![FirstName 和 LastName 值都显示在单个列中](using-templatefields-in-the-gridview-control-cs/_static/image26.png)](using-templatefields-in-the-gridview-control-cs/_static/image25.png)

**图 9**： `FirstName` 和 `LastName` 值都显示在单个列中（[单击以查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image27.png)）

若要完成此第一步，请删除 `LastName` BoundField，并将 `FirstName` TemplateField 的 `HeaderText` 属性重命名为 "Name"。 这些更改之后，GridView 的声明性标记应如下所示：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample4.aspx)]

[![每个雇员的名字和姓氏都显示在一列中](using-templatefields-in-the-gridview-control-cs/_static/image29.png)](using-templatefields-in-the-gridview-control-cs/_static/image28.png)

**图 10**：每个雇员的名字和姓氏都显示在一列中（[单击查看完全尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image30.png)）

## <a name="step-3-using-the-calendar-control-to-display-thehireddatefield"></a>步骤3：使用 Calendar 控件显示 "`HiredDate`" 字段

以 GridView 文本形式显示数据字段值与使用 BoundField 一样简单。 但是，在某些情况下，最好使用特定的 Web 控件而不是文本来表示数据。 可以通过 Templatefield 进行此类自定义的数据显示。 例如，我们可以显示日历（使用[日历控件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar(VS.80).aspx)），其中突出显示了其雇佣日期，而不是将其作为文本显示。

为此，请首先将 `HiredDate` BoundField 转换为 TemplateField。 只需跳到 GridView 的智能标记，然后单击 "编辑列" 链接，打开 "字段" 对话框。 选择 `HiredDate` BoundField，然后单击 "将此字段转换为 TemplateField"。

[![将 HiredDate BoundField 转换为 TemplateField](using-templatefields-in-the-gridview-control-cs/_static/image32.png)](using-templatefields-in-the-gridview-control-cs/_static/image31.png)

**图 11**：将 `HiredDate` BoundField 转换为 TemplateField （[单击以查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image33.png)）

正如我们在步骤2中看到的那样，这会将 BoundField 替换为 TemplateField，其中 `EditItemTemplate` `ItemTemplate` 包含一个标签和文本框，其 `Text` 属性使用 databinding 语法 `<%# Bind("HiredDate")%>`绑定到 `HiredDate` 值。

若要将文本替换为日历控件，请通过删除标签并添加日历控件来编辑模板。 从设计器中，从 GridView 的智能标记中选择 "编辑模板"，然后从下拉列表中选择 `HireDate` TemplateField 的 `ItemTemplate`。 接下来，删除 "标签" 控件，并将 "日历" 控件从 "工具箱" 拖至模板编辑界面。

[![向雇用日期 TemplateField 的 ItemTemplate 添加日历控件](using-templatefields-in-the-gridview-control-cs/_static/image35.png)](using-templatefields-in-the-gridview-control-cs/_static/image34.png)

**图 12**：将日历控件添加到 `HireDate` TemplateField 的 `ItemTemplate` （[单击查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image36.png)）

此时，GridView 中的每一行都将包含其 `HiredDate` TemplateField 中的日历控件。 但是，不会在日历控件中的任何位置设置员工的实际 `HiredDate` 值，从而导致每个日历控件默认显示当前月份和日期。 若要解决此情况，需要将每个员工的 `HiredDate` 分配给 Calendar 控件的[SelectedDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selecteddate(VS.80).aspx)和[VisibleDate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.visibledate(VS.80).aspx)属性。

从日历控件的智能标记中，选择 "编辑绑定"。 接下来，将 `SelectedDate` 和 `VisibleDate` 属性绑定到 `HiredDate` 数据字段。

[![将 SelectedDate 和 VisibleDate 属性绑定到 HiredDate 数据字段](using-templatefields-in-the-gridview-control-cs/_static/image38.png)](using-templatefields-in-the-gridview-control-cs/_static/image37.png)

**图 13**：将 `SelectedDate` 和 `VisibleDate` 属性绑定到 "`HiredDate` 数据" 字段（[单击以查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image39.png)）

> [!NOTE]
> 日历控件所选的日期不一定是必需的。 例如，日历可以有8月1日<sup>圣</sup>1999，但显示当前月份和年份。 所选日期和可见日期由日历控件的 `SelectedDate` 和 `VisibleDate` 属性指定。 由于我们希望选择员工的 `HiredDate`，并确保显示它，我们需要将这两个属性绑定到 `HireDate` 数据字段。

查看浏览器中的页面时，日历现在显示员工雇用日期的月份，并选择该特定日期。

[![员工的 HiredDate 显示在日历控件中](using-templatefields-in-the-gridview-control-cs/_static/image41.png)](using-templatefields-in-the-gridview-control-cs/_static/image40.png)

**图 14**：员工的 `HiredDate` 显示在日历控件中（[单击查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image42.png)）

> [!NOTE]
> 与我们目前为止看到的所有示例相反，对于本教程，我们未*将此*GridView 的 `EnableViewState` 属性设置为 `false`。 此决策的原因是，单击日历控件的日期将导致回发，并将日历的选定日期设置为刚单击的日期。 但是，如果已禁用 GridView 的视图状态，则在每次回发时，将将 GridView 的数据重新绑定到其基础数据源，这会导致日历的选定日期被设置*回*雇员的 `HireDate`，从而覆盖用户选择的日期。

对于本教程，这是一个差异的讨论，因为用户无法更新员工的 `HireDate`。 最好将日历控件配置为不能选择其日期。 无论如何，此教程会说明，在某些情况下，必须启用视图状态才能提供某些功能。

## <a name="step-4-showing-the-number-of-days-the-employee-has-worked-for-the-company"></a>步骤4：显示员工为公司工作的天数

到目前为止，我们已经了解了 Templatefield 的两个应用程序：

- 将两个或更多数据字段值组合到一个列中，并
- 使用 Web 控件而不是文本表示数据字段值

Templatefield 的第三个用途是显示有关 GridView 的基础数据的元数据。 例如，除了显示员工的雇用日期以外，我们可能还需要列显示在该作业上的总天数。

此外，当基础数据需要在网页报表中以不同于存储在数据库中的格式显示时，还会出现 Templatefield 的另一种用法。 假设 `Employees` 表具有一个 `Gender` 字段，该字段存储了字符 `M` 或 `F`，以指示员工的性别。 在网页中显示此信息时，我们可能希望将性别显示为 "男" 或 "女性"，而不是只显示 "M" 或 "F"。

这两种情况都可以通过在 ASP.NET 页的代码隐藏类（或在作为 `static` 方法实现的单独类库中创建*格式设置方法*）进行处理，该方法是从模板调用的。 这种格式设置方法是使用前面所见的相同数据绑定语法从模板调用的。 格式设置方法可采用任意数量的参数，但必须返回一个字符串。 此返回字符串是插入到模板中的 HTML。

为了说明这一概念，让我们进一步增加教程，以显示一个列，该列列出了员工在该作业上的总天数。 此格式设置方法将采用 `Northwind.EmployeesRow` 对象，并返回该雇员被当作字符串使用的天数。 此方法可添加到 ASP.NET 页的代码隐藏类，但*必须*标记为 `protected` 或 `public` 才能从模板进行访问。

[!code-csharp[Main](using-templatefields-in-the-gridview-control-cs/samples/sample5.cs)]

由于 `HiredDate` 字段可以包含 `NULL` 数据库值，因此，在继续计算之前，必须先确保该值不 `NULL`。 如果 `NULL``HiredDate` 值，只需返回字符串 "Unknown";如果未 `NULL`，则计算当前时间与 `HiredDate` 值之间的差异并返回天数。

若要利用此方法，我们需要使用数据绑定语法从 GridView 中的 TemplateField 调用它。 首先，在 GridView 的智能标记中单击 "编辑列" 链接，然后添加新的 TemplateField，以将新的 TemplateField 添加到 GridView。

[![将新的 TemplateField 添加到 GridView](using-templatefields-in-the-gridview-control-cs/_static/image44.png)](using-templatefields-in-the-gridview-control-cs/_static/image43.png)

**图 15**：向 GridView 添加新的 TemplateField （[单击查看完全尺寸的图像](using-templatefields-in-the-gridview-control-cs/_static/image45.png)）

将此新 TemplateField 的 `HeaderText` 属性设置为 "作业日期"，并将其 `ItemStyle`的 `HorizontalAlign` 属性设置为 "`Center`"。 若要从模板调用 `DisplayDaysOnJob` 方法，请添加 `ItemTemplate` 并使用以下 databinding 语法：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample6.aspx)]

`Container.DataItem` 返回与绑定到 `GridViewRow`的 `DataSource` 记录对应的 `DataRowView` 对象。 它的 `Row` 属性返回强类型 `Northwind.EmployeesRow`，它将传递到 `DisplayDaysOnJob` 方法。 此数据绑定语法可以直接出现在 `ItemTemplate` （如下面的声明性语法所示），也可以分配给标签 Web 控件的 `Text` 属性。

> [!NOTE]
> 或者，只需使用 `<%# DisplayDaysOnJob(Eval("HireDate")) %>`传入 `HireDate` 值，而不是传入 `EmployeesRow` 实例。 但是，`Eval` 方法返回 `object`，因此，我们必须将 `DisplayDaysOnJob` 方法签名改为接受 `object`类型的输入参数。 不能盲目地将 `Eval("HireDate")` 调用强制转换为 `DateTime`，因为 `Employees` 表中的 `HireDate` 列可以包含 `NULL` 值。 因此，需要接受 `object` 作为 `DisplayDaysOnJob` 方法的输入参数，检查它是否有数据库 `NULL` 值（可以使用 `Convert.IsDBNull(objectToCheck)`完成此操作），然后进行相应的处理。

由于这些微妙之处，我选择了传入整个 `EmployeesRow` 的实例。 在下一教程中，我们将看到更适合使用 `Eval("columnName")` 语法将输入参数传递到格式设置方法的示例。

下面显示了在添加 TemplateField 后，GridView 的声明性语法以及从 `ItemTemplate`中调用的 `DisplayDaysOnJob` 方法：

[!code-aspx[Main](using-templatefields-in-the-gridview-control-cs/samples/sample7.aspx)]

图16显示了通过浏览器查看时的完整教程。

[![显示该员工已在该作业中的天数](using-templatefields-in-the-gridview-control-cs/_static/image47.png)](using-templatefields-in-the-gridview-control-cs/_static/image46.png)

**图 16**：显示了员工在该作业上的天数（[单击查看完全大小的图像](using-templatefields-in-the-gridview-control-cs/_static/image48.png)）

## <a name="summary"></a>摘要

使用 GridView 控件中的 TemplateField，可以在显示数据时提供比其他字段控件更高的灵活性。 Templatefield 适用于以下情况：

- 需要在一个 GridView 列中显示多个数据字段
- 使用 Web 控件而不是纯文本来最大程度地表示数据
- 输出取决于基础数据，如显示元数据或重新格式化数据

除了自定义数据显示之外，Templatefield 还可用于自定义用于编辑和插入数据的用户界面，如我们将在以后的教程中看到的那样。

接下来的两个教程将继续浏览模板，从一开始就在 DetailsView 中使用 Templatefield。 接下来，我们将转到 FormView，它使用模板来代替字段，为数据布局和结构提供更大的灵活性。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的潜在客户审阅者为 Dan Jagers。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](custom-formatting-based-upon-data-cs.md)
> [下一页](using-templatefields-in-the-detailsview-control-cs.md)
