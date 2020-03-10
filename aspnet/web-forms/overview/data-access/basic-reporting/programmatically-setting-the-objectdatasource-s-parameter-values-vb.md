---
uid: web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
title: 以编程方式设置 ObjectDataSource 的参数值（VB） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将介绍如何将方法添加到可接受单个输入参数并返回数据的 DAL 和 BLL。 此示例将设置此参数 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0ecb03b6-52a0-4731-8c7a-436391d36838
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb
msc.type: authoredcontent
ms.openlocfilehash: f1dd50f46528e8dd51f85e503604d3f0dbc21ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78465914"
---
# <a name="programmatically-setting-the-objectdatasources-parameter-values-vb"></a>以编程方式设置 ObjectDataSource 的参数值 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_6_VB.exe)或[下载 PDF](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/datatutorial06vb1.pdf)

> 在本教程中，我们将介绍如何将方法添加到可接受单个输入参数并返回数据的 DAL 和 BLL。 该示例将以编程方式设置此参数。

## <a name="introduction"></a>简介

正如在[上一教程](declarative-parameters-vb.md)中所看到的，有许多选项可用于以声明方式将参数值传递给 ObjectDataSource 的方法。 如果参数值是硬编码的，则来自页面上的 Web 控件，或来自数据源 `Parameter` 对象可读取的任何其他源，例如，该值可以绑定到输入参数而无需编写代码行。

但有时，当参数值来自某个内置数据源（`Parameter` 对象）未考虑的某些源时。 如果我们的站点支持的用户帐户，我们可能希望基于当前登录的访问者用户 ID 来设置参数。 或者，可能需要在将参数值发送到 ObjectDataSource 的基础对象的方法之前，对其进行自定义。

每当调用 ObjectDataSource 的 `Select` 方法时，ObjectDataSource 首先引发其[选择事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting%28VS.80%29.aspx)。 然后调用 ObjectDataSource 的基础对象的方法。 完成后，将引发 ObjectDataSource 的[选定事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selected%28VS.80%29.aspx)（图1说明此事件序列）。 可以在事件处理程序中为 `Selecting` 事件的事件处理程序设置或自定义传入 ObjectDataSource 的基础对象的方法的参数值。

[![所选的 ObjectDataSource，并选择在调用其基础对象的方法之前和之后激发的事件](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image2.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image1.png)

**图 1**： ObjectDataSource 的 `Selected` 和 `Selecting` 事件会在其基础对象的方法被调用之前和之后激发（[单击以查看完全大小的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image3.png)）

在本教程中，我们将介绍如何将方法添加到 DAL 和 BLL，这些方法接受 `Integer` 类型的单个输入参数 `Month`，并返回一个 `EmployeesDataTable` 对象，该对象以在指定 `Month`中具有录用周年的员工填充。 本示例将基于当前月份以编程方式设置此参数，并显示 "本月员工周年纪念日" 列表。

让我们进入正题！

## <a name="step-1-adding-a-method-toemployeestableadapter"></a>步骤1：将方法添加到`EmployeesTableAdapter`

对于我们的第一个示例，我们需要添加一个方法来检索 `HireDate` 在指定月份发生的雇员。 若要根据体系结构提供此功能，我们需要先在 `EmployeesTableAdapter` 中创建一个映射到正确 SQL 语句的方法。 若要实现此目的，请首先打开 Northwind 类型化数据集。 右键单击 "`EmployeesTableAdapter`" 标签，然后选择 "添加查询"。

[![向 EmployeesTableAdapter 中添加新查询](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image5.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image4.png)

**图 2**：向 `EmployeesTableAdapter` 中添加新查询（[单击查看完全大小的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image6.png)）

选择添加返回行的 SQL 语句。 到达 "指定 `SELECT` 语句" 屏幕时，`EmployeesTableAdapter` 的默认 `SELECT` 语句将被加载。 只需在 `WHERE` 子句中添加： `WHERE DATEPART(m, HireDate) = @Month`。 [DATEPART](https://msdn.microsoft.com/library/ms174420.aspx)是一个 t-sql 函数，该函数返回 `datetime` 类型的特定日期部分;在此示例中，我们使用 `DATEPART` 返回 `HireDate` 列的月份。

[![仅返回雇佣日期列小于或等于 @HiredBeforeDate 参数的行](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image8.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image7.png)

**图 3**：仅返回 `HireDate` 列小于或等于 `@HiredBeforeDate` 参数的行（[单击以查看完全大小的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image9.png)）

最后，将 `FillBy` 和 `GetDataBy` 方法名称分别更改为 `FillByHiredDateMonth` 和 `GetEmployeesByHiredDateMonth`。

[![选择更适合的方法名称，而不是 FillBy 和 GetDataBy](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image11.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image10.png)

**图 4**：选择更适合的方法名称，而不是 `FillBy` 和 `GetDataBy` （[单击查看完全大小的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image12.png)）

单击 "完成" 以完成向导并返回到数据集的设计图面。 `EmployeesTableAdapter` 现在应包含一组新方法用于访问在指定月份雇用的员工。

[![新方法将出现在数据集的 Design Surface 中](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image14.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image13.png)

**图 5**：新方法出现在数据集的 Design Surface 中（[单击查看完全大小的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image15.png)）

## <a name="step-2-adding-thegetemployeesbyhireddatemonthmonthmethod-to-the-business-logic-layer"></a>步骤2：将`GetEmployeesByHiredDateMonth(month)`方法添加到业务逻辑层

由于我们的应用程序体系结构为业务逻辑和数据访问逻辑使用了单独的层，因此需要向向下调用 DAL 的 BLL 添加一个方法，用于检索在指定日期之前雇用的员工。 打开 `EmployeesBLL.vb` 文件并添加以下方法：

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample1.vb)]

与此类中的其他方法一样，`GetEmployeesByHiredDateMonth(month)` 只需向下调用 DAL 并返回结果。

## <a name="step-3-displaying-employees-whose-hiring-anniversary-is-this-month"></a>步骤3：显示招聘周年纪念本月的雇员

此示例的最后一步是显示招聘周年为本月的雇员。 首先，将 GridView 添加到 `BasicReporting` 文件夹中的 "`ProgrammaticParams.aspx`" 页，然后添加一个新的 ObjectDataSource 作为其数据源。 将 ObjectDataSource 配置为使用 `EmployeesBLL` 类，将 `SelectMethod` 设置为 "`GetEmployeesByHiredDateMonth(month)`"。

[![使用 EmployeesBLL 类](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image17.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image16.png)

**图 6**：使用 `EmployeesBLL` 类（[单击以查看完全大小的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image18.png)）

[从 GetEmployeesByHiredDateMonth （月）方法中选择 ![](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image20.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image19.png)

**图 7**：从 `GetEmployeesByHiredDateMonth(month)` 方法中进行选择（[单击以查看完全大小的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image21.png)）

最终屏幕会要求我们提供 `month` 参数值的源。 由于我们将以编程方式设置此值，因此，将参数源设置为默认值 "无"，然后单击 "完成"。

[![将参数源设置为 "无"](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image23.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image22.png)

**图 8**：将参数 "源" 设置为 "无" （[单击查看完全大小的图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image24.png)）

这将在 ObjectDataSource 的 `SelectParameters` 集合中创建一个未指定值的 `Parameter` 对象。

[!code-aspx[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample2.aspx)]

若要以编程方式设置此值，需要为 ObjectDataSource 的 `Selecting` 事件创建事件处理程序。 若要实现此目的，请跳到设计视图，然后双击 ObjectDataSource。 或者，选择 "ObjectDataSource"，中转到 "属性窗口"，然后单击闪电形图标。 接下来，双击 "`Selecting`" 事件旁边的文本框，或键入要使用的事件处理程序的名称。 第三个选项是，可以通过从页面代码隐藏类顶部的两个下拉列表中选择 ObjectDataSource 及其 `Selecting` 事件来创建事件处理程序。

![单击 "属性" 窗口中的闪电形图标以列出 Web 控件的事件](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image25.png)

**图 9**：单击 "属性" 窗口中的闪电形图标以列出 Web 控件的事件

所有这三种方法都会向页面的代码隐藏类添加 ObjectDataSource 的 `Selecting` 事件的新事件处理程序。 在此事件处理程序中，我们可以使用 `e.InputParameters(parameterName)`读取和写入参数值，其中 *`parameterName`* 是 `<asp:Parameter>` 标记中 `Name` 特性的值（`InputParameters` 集合也可以按序号）。`e.InputParameters(index)` 若要将 `month` 参数设置为当月，请将以下内容添加到 `Selecting` 事件处理程序中：

[!code-vb[Main](programmatically-setting-the-objectdatasource-s-parameter-values-vb/samples/sample3.vb)]

通过浏览器访问此页时，可以看到，在本月（3月），她只聘用了一名员工，因为1994，她在该公司的 Callahan。

[![显示此月周年纪念的员工](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image27.png)](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image26.png)

**图 10**：显示本月周年纪念的员工（[单击查看全尺寸图像](programmatically-setting-the-objectdatasource-s-parameter-values-vb/_static/image28.png)）

## <a name="summary"></a>摘要

尽管 ObjectDataSource 的参数值通常可以通过声明方式进行设置，而无需编写代码行，但可以通过编程方式轻松地设置参数值。 我们需要做的就是为 ObjectDataSource 的 `Selecting` 事件创建事件处理程序，该事件处理程序在调用基础对象的方法之前激发，并通过 `InputParameters` 集合手动设置一个或多个参数的值。

本教程介绍了基本报表部分。 [下一教程](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md)将介绍如何使用 "筛选和主要-详细方案" 部分，其中介绍了允许访问者筛选数据以及从主报表向下钻取到详细信息报表的方法。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](declarative-parameters-vb.md)
