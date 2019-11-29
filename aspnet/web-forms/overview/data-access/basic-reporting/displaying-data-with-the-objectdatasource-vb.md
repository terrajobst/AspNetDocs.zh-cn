---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
title: 用 ObjectDataSource 显示数据（VB） |Microsoft Docs
author: rick-anderson
description: 本教程将使用此控件查看 ObjectDataSource 控件，可以绑定从上一教程中创建的 BLL 检索的数据，无需 havi 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d62c3a63-0940-4019-874e-4a4047df0c1c
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 754188352cbfb08e610027f5b7890a32bd88ae26
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74608883"
---
# <a name="displaying-data-with-the-objectdatasource-vb"></a>使用 ObjectDataSource 显示数据 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_4_VB.exe)或[下载 PDF](displaying-data-with-the-objectdatasource-vb/_static/datatutorial04vb1.pdf)

> 本教程将使用此控件查看 ObjectDataSource 控件，可以绑定从上一教程中创建的 BLL 检索的数据，而无需编写代码行！

## <a name="introduction"></a>简介

随着应用程序体系结构和网站页面布局的完成，我们已准备好开始探索如何完成各种常见的数据和与报表相关的任务。 在前面的教程中，我们已了解如何以编程方式将来自 DAL 和 BLL 的数据绑定到 ASP.NET 页中的数据 Web 控件。 此语法将数据 Web 控件的 `DataSource` 属性分配给要显示的数据，然后调用该控件的 `DataBind()` 方法是 ASP.NET 1.x 应用程序中使用的模式，可以继续在2.0 应用程序中使用。 但是，ASP.NET 2.0 的新数据源控件提供了一种用于处理数据的声明性方式。 使用这些控件，可以绑定从上一教程中创建的 BLL 检索的数据，而无需编写代码行！

ASP.NET 2.0 随附了五个内置数据源控件[SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx)、 [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)、 [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx)、 [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)和[SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx) ，不过，如果需要，你可以构建自己的[自定义数据源控件](https://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/DataSourceCon1.asp)。 由于我们已开发了一个适用于我们的教程应用程序的体系结构，我们将针对 BLL 类使用 ObjectDataSource。

![ASP.NET 2.0 包括五个内置数据源控件](displaying-data-with-the-objectdatasource-vb/_static/image1.png)

**图 1**： ASP.NET 2.0 包括五个内置数据源控件

ObjectDataSource 充当用于处理其他某个对象的代理。 若要配置 ObjectDataSource，我们需要指定此基础对象，以及其方法是如何映射到 ObjectDataSource 的 `Select`、`Insert`、`Update`和 `Delete` 方法。 指定此基础对象并将其方法映射到 ObjectDataSource 后，接下来我们可以将该 ObjectDataSource 绑定到数据 Web 控件。 ASP.NET 附带了许多数据 Web 控件，其中包括 GridView、DetailsView、RadioButtonList 和 DropDownList 等。 在页生命周期内，数据 Web 控件可能需要访问它所绑定到的数据，这将通过调用其 ObjectDataSource 的 `Select` 方法来实现;如果数据 Web 控件支持插入、更新或删除，则可以对其 ObjectDataSource 的 `Insert`、`Update`或 `Delete` 方法进行调用。 然后，ObjectDataSource 将这些调用路由到相应的基础对象的方法，如下图所示。

[![ObjectDataSource 充当代理](displaying-data-with-the-objectdatasource-vb/_static/image3.png)](displaying-data-with-the-objectdatasource-vb/_static/image2.png)

**图 2**： ObjectDataSource 充当代理（[单击以查看完全大小的映像](displaying-data-with-the-objectdatasource-vb/_static/image4.png)）

尽管可以使用 ObjectDataSource 来调用用于插入、更新或删除数据的方法，但我们只需专注于返回数据;将来的教程将探讨如何使用用于修改数据的 ObjectDataSource 和数据 Web 控件。

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>步骤1：添加和配置 ObjectDataSource 控件

首先打开 `BasicReporting` 文件夹中的 "`SimpleDisplay.aspx`" 页，切换到设计视图，然后将 "ObjectDataSource" 控件从 "工具箱" 拖动到页面的设计图面上。 ObjectDataSource 在设计图面上显示为灰色框，因为它不生成任何标记;它只是通过从指定的对象调用方法来访问数据。 ObjectDataSource 返回的数据可以通过数据 Web 控件显示，例如 GridView、DetailsView、FormView 等。

> [!NOTE]
> 或者，您可以首先将数据 Web 控件添加到页面，然后从其智能标记中，从下拉列表中选择 "&lt;新建数据源&gt;" 选项。

若要指定 ObjectDataSource 的基础对象以及该对象的方法映射到 ObjectDataSource 的方式，请单击该 ObjectDataSource 的智能标记中的 "配置数据源" 链接。

[![单击智能标记中的 "配置数据源" 链接](displaying-data-with-the-objectdatasource-vb/_static/image6.png)](displaying-data-with-the-objectdatasource-vb/_static/image5.png)

**图 3**：从智能标记中单击 "配置数据源" 链接（[单击以查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image7.png)）

此时将打开 "配置数据源" 向导。 首先，必须指定 ObjectDataSource 要使用的对象。 如果选中了 "仅显示数据组件" 复选框，则此屏幕上的下拉列表将仅列出已使用 `DataObject` 特性修饰的对象。 目前，我们的列表包含在上一教程中创建的类型化数据集和 BLL 类中的 Tableadapter。 如果忘记将 `DataObject` 特性添加到业务逻辑层类，则不会在此列表中看到它们。 在这种情况下，取消选中 "仅显示数据组件" 复选框，以查看所有对象，这些对象应包括 BLL 类（以及数据表、Datarow 等的类型化数据集中的其他类）。

在第一个屏幕中，从下拉列表中选择 `ProductsBLL` 类，然后单击 "下一步"。

[![指定要用于 ObjectDataSource 控件的对象](displaying-data-with-the-objectdatasource-vb/_static/image9.png)](displaying-data-with-the-objectdatasource-vb/_static/image8.png)

**图 4**：指定要用于 ObjectDataSource 控件的对象（[单击以查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image10.png)）

向导中的下一个屏幕提示您选择 ObjectDataSource 应调用的方法。 下拉列表列出了返回从上一屏幕中选择的对象中的数据的方法。 在这里，我们将看到 `GetProductByProductID`、`GetProducts`、`GetProductsByCategoryID`和 `GetProductsBySupplierID`。 从下拉列表中选择 `GetProducts` 方法，然后单击 "完成" （如果已将 `DataObjectMethodAttribute` 添加到 `ProductBLL`的方法（如前面的教程中所示），则默认情况下将选中此选项。

[![从 "选择" 选项卡中选择返回数据的方法](displaying-data-with-the-objectdatasource-vb/_static/image12.png)](displaying-data-with-the-objectdatasource-vb/_static/image11.png)

**图 5**：从 "选择" 选项卡中选择返回数据的方法（[单击查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image13.png)）

## <a name="configure-the-objectdatasource-manually"></a>手动配置 ObjectDataSource

ObjectDataSource 的 "配置数据源" 向导提供了一种快速方法来指定它使用的对象，并将调用对象的哪些方法关联起来。 但是，可以通过属性窗口或直接在声明性标记中，通过其属性配置 ObjectDataSource。 只需将 `TypeName` 属性设置为要使用的基础对象的类型，并将 `SelectMethod` 设置为在检索数据时要调用的方法。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample1.aspx)]

即使您更喜欢 "配置数据源" 向导，有时也可能需要手动配置 ObjectDataSource，因为向导仅列出开发人员创建的类。 如果要将 ObjectDataSource 绑定到 .NET Framework （例如[成员身份类](https://msdn.microsoft.com/library/system.web.security.membership.aspx)）中的类，若要访问用户帐户信息或[目录类](https://msdn.microsoft.com/library/system.io.directory.aspx)以使用文件系统信息，则需要手动设置 ObjectDataSource 的属性。

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>步骤2：添加数据 Web 控件并将其绑定到 ObjectDataSource

一旦将 ObjectDataSource 添加到页面并进行了配置，就可以将数据 Web 控件添加到页面，以显示由 ObjectDataSource 的 `Select` 方法返回的数据。 任何数据 Web 控件都可以绑定到 ObjectDataSource;让我们看看如何在 GridView、DetailsView 和 FormView 中显示 ObjectDataSource 的数据。

## <a name="binding-a-gridview-to-the-objectdatasource"></a>将 GridView 绑定到 ObjectDataSource

将工具箱中的 GridView 控件添加到 `SimpleDisplay.aspx`的设计图面。 从 GridView 的智能标记中，选择在步骤1中添加的 ObjectDataSource 控件。 这会自动为 ObjectDataSource `Select` 方法（即 Products DataTable 定义的属性）中的数据返回的每个属性创建 BoundField。

[![已将 GridView 添加到页面并绑定到 ObjectDataSource](displaying-data-with-the-objectdatasource-vb/_static/image15.png)](displaying-data-with-the-objectdatasource-vb/_static/image14.png)

**图 6**：已将 GridView 添加到页面并绑定到 ObjectDataSource （[单击以查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image16.png)）

然后，可以通过从智能标记中单击 "编辑列" 选项来自定义、重新排列或删除 GridView 的 BoundFields。

[![通过 "编辑列" 对话框管理 GridView 的 BoundFields](displaying-data-with-the-objectdatasource-vb/_static/image18.png)](displaying-data-with-the-objectdatasource-vb/_static/image17.png)

**图 7**：通过 "编辑列" 对话框管理 GridView 的 BoundFields （[单击以查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image19.png)）

花点时间修改 GridView 的 BoundFields，删除 `ProductID`、`SupplierID`、`CategoryID`、`QuantityPerUnit`、`UnitsInStock`、`UnitsOnOrder`和 `ReorderLevel` BoundFields。 只需从左下方的列表中选择 "BoundField"，然后单击 "删除" 按钮（红色 X）即可将其删除。 接下来，重新排列 BoundFields，以便 `CategoryName` 和 `SupplierName` BoundFields 在 `UnitPrice` BoundField 之前，选择这些 BoundFields 并单击向上箭头。 将剩余 BoundFields 的 `HeaderText` 属性分别设置为 "`Products`"、"`Category`"、"`Supplier`" 和 "`Price`"。 接下来，通过将 BoundField 的 `HtmlEncode` 属性设置为 False，将 `Price` BoundField 的格式设置为 "False"，并将其 `DataFormatString` 属性设置为 "`{0:c}`"。 最后，在水平方向上将 `Price` 向右对齐，并通过 `ItemStyle`/`HorizontalAlign` 属性将中心 `Discontinued` 复选框水平对齐。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

[已自定义 GridView BoundFields ![](displaying-data-with-the-objectdatasource-vb/_static/image21.png)](displaying-data-with-the-objectdatasource-vb/_static/image20.png)

**图 8**：已经自定义了 GridView 的 BoundFields （[单击查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image22.png)）

## <a name="using-themes-for-a-consistent-look"></a>使用主题实现一致的外观

这些教程尽力删除任何控件级样式设置，而不是尽可能使用外部文件中定义的级联样式表。 `Styles.css` 文件包含 `DataWebControlStyle`、`HeaderStyle`、`RowStyle`和 `AlternatingRowStyle` CSS 类，它们应该用于决定这些教程中所使用的数据 Web 控件的外观。 为实现此目的，我们可以将 GridView 的 `CssClass` 属性设置为 `DataWebControlStyle`，并相应地设置其 `HeaderStyle`、`RowStyle`和 `AlternatingRowStyle` 属性。

如果在 Web 控件中设置这些 `CssClass` 属性，我们需要记得为每个已添加到教程中的数据 Web 控件显式设置这些属性值。 更易于管理的方法是使用主题为 GridView、DetailsView 和 FormView 控件定义默认的与 CSS 相关的属性。 主题是可应用于站点中的页面以强制使用常见外观的控件级属性设置、图像和 CSS 类的集合。

本主题不包括任何图像或 CSS 文件（我们会在 web 应用程序的根文件夹中按原样 `Styles.css` 原样保留样式表，但将包括两个外观。 外观是一个文件，用于定义 Web 控件的默认属性。 具体而言，我们将有一个用于 GridView 和 DetailsView 控件的外观文件，用于指示默认 `CssClass`相关的属性。

首先，在解决方案资源管理器中右键单击项目名称，然后选择 "添加新项"，以将新的外观文件添加到名为 `GridView.skin` 的项目。

[![添加名为 GridView 的外观文件](displaying-data-with-the-objectdatasource-vb/_static/image24.png)](displaying-data-with-the-objectdatasource-vb/_static/image23.png)

**图 9**：添加一个名为 `GridView.skin` 的外观文件（[单击以查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image25.png)）

外观文件需要放在位于 `App_Themes` 文件夹中的主题中。 由于我们还没有这样一个文件夹，因此，在添加第一个外观时，Visual Studio 将为我们创建一个。 单击 "是" 以创建 `App_Theme` 文件夹，然后将新的 `GridView.skin` 文件放在此处。

[![让 Visual Studio 创建 App_Theme 文件夹](displaying-data-with-the-objectdatasource-vb/_static/image27.png)](displaying-data-with-the-objectdatasource-vb/_static/image26.png)

**图 10**：让 Visual Studio 创建 `App_Theme` 文件夹（[单击查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image28.png)）

这会在名为 GridView 的 `App_Themes` 文件夹中创建一个新主题，并 `GridView.skin`外观文件。

![GridView 主题已添加到 App_Theme 文件夹](displaying-data-with-the-objectdatasource-vb/_static/image29.png)

**图 11**： GridView 主题已添加到 `App_Theme` 文件夹

将 GridView 主题重命名为 "DataWebControls" （右键单击 `App_Theme` 文件夹中的 GridView 文件夹，然后选择 "重命名"）。 接下来，将以下标记输入到 `GridView.skin` 文件中：

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample3.aspx)]

这将为任何使用 DataWebControls 主题的页面中的任何 GridView 定义与 `CssClass`相关的属性的默认属性。 接下来，我们将为 DetailsView 添加另一个外观，这是我们稍后将使用的数据 Web 控件。 将新外观添加到名为 `DetailsView.skin` 的 DataWebControls 主题，并添加以下标记：

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample4.aspx)]

定义主题后，最后一步是将主题应用于我们的 ASP.NET 页面。 主题可以逐页应用，也可以针对网站中的所有页面应用。 让我们为网站中的所有页面使用此主题。 若要实现此目的，请将以下标记添加到 `Web.config`的 `<system.web>` 部分：

[!code-xml[Main](displaying-data-with-the-objectdatasource-vb/samples/sample5.xml)]

就这么简单！ `styleSheetTheme` 设置指示主题中指定的属性*不*应重写在控件级别指定的属性。 若要指定主题设置应王牌控制设置，请使用 `theme` 特性代替 `styleSheetTheme`;遗憾的是，主题设置不会出现在 Visual Studio 设计视图中。 有关主题和外观的详细信息，请参阅[ASP.NET 主题和外观概述](https://msdn.microsoft.com/library/ykzx33wh.aspx)和[服务器端样式](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)。有关将页配置为使用主题的详细信息，请参阅[如何：应用 ASP.NET 主题](https://msdn.microsoft.com/library/0yy5hxdk%28VS.80%29.aspx)。

[![GridView 显示产品的名称、类别、供应商、价格和废止信息](displaying-data-with-the-objectdatasource-vb/_static/image31.png)](displaying-data-with-the-objectdatasource-vb/_static/image30.png)

**图 12**： GridView 显示产品的名称、类别、供应商、价格和废止信息（[单击查看全尺寸图像](displaying-data-with-the-objectdatasource-vb/_static/image32.png)）

## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>在 DetailsView 中一次显示一条记录

GridView 为其绑定的数据源控件返回的每个记录显示一行。 但有时，我们可能希望一次只显示一个记录或一条记录。 [DetailsView 控件](https://msdn.microsoft.com/library/s3w1w7t4.aspx)提供此功能，呈现为 HTML `<table>`，其中包含两列，每个绑定到控件的列或属性占一行。 您可以将 DetailsView 看作是一条记录旋转了90度的 GridView。

首先在 `SimpleDisplay.aspx`中的 GridView*上方*添加一个 DetailsView 控件。 接下来，将其绑定到作为 GridView 的相同 ObjectDataSource 控件。 与 GridView 一样，对于由 ObjectDataSource `Select` 方法返回的对象中的每个属性，都将向 DetailsView 添加一个 BoundField。 唯一的区别是，DetailsView 的 BoundFields 水平布局，而不是垂直布局。

[![向页面添加 DetailsView 并将其绑定到 ObjectDataSource](displaying-data-with-the-objectdatasource-vb/_static/image34.png)](displaying-data-with-the-objectdatasource-vb/_static/image33.png)

**图 13**：将 DetailsView 添加到页面并将其绑定到 ObjectDataSource （[单击以查看完全大小的映像](displaying-data-with-the-objectdatasource-vb/_static/image35.png)）

与 GridView 一样，DetailsView 的 BoundFields 可以调整，以提供对 ObjectDataSource 返回的数据的更自定义显示。 图14显示了在其 BoundFields 和 `CssClass` 属性已配置为使其外观类似于 GridView 示例后的 DetailsView。

[![DetailsView 显示单个记录](displaying-data-with-the-objectdatasource-vb/_static/image37.png)](displaying-data-with-the-objectdatasource-vb/_static/image36.png)

**图 14**： DetailsView 显示单个记录（[单击查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image38.png)）

请注意，DetailsView 只显示其数据源返回的第一条记录。 若要允许用户单步执行所有记录，必须为 DetailsView 启用分页。 为此，请返回到 Visual Studio 并选中 DetailsView 的智能标记中的 "启用分页" 复选框。

[![在 DetailsView 控件中启用分页](displaying-data-with-the-objectdatasource-vb/_static/image40.png)](displaying-data-with-the-objectdatasource-vb/_static/image39.png)

**图 15**：在 DetailsView 控件中启用分页（[单击以查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image41.png)）

[![启用了分页，DetailsView 允许用户查看任何产品](displaying-data-with-the-objectdatasource-vb/_static/image43.png)](displaying-data-with-the-objectdatasource-vb/_static/image42.png)

**图 16**：启用分页后，DetailsView 允许用户查看任何产品（[单击查看完全尺寸的图像](displaying-data-with-the-objectdatasource-vb/_static/image44.png)）

在将来的教程中，我们将详细介绍分页。

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>一次显示一条记录的更灵活的布局

DetailsView 在显示从 ObjectDataSource 返回的每条记录的方式上非常严格。 我们可能需要更灵活的数据视图。 例如，我们可能需要在一个 `<h4>` 标题中显示产品名称和价格，而不是在单独的行中显示产品名称、类别、供应商、价格和废止信息，而是以较小字体大小显示在名称和价格下面的类别和供应商信息。 我们可能不介意在值旁显示属性名称（产品、类别等）。

[FormView 控件](https://msdn.microsoft.com/library/fyf1dk77.aspx)可提供此级别的自定义。 FormView 使用模板，这些模板允许混合使用 Web 控件、静态 HTML 和[数据绑定语法](http://www.15seconds.com/issue/040630.htm)，而不是使用字段（如 GridView 和 DetailsView 这样做）。 如果你熟悉 ASP.NET 1.x 中的中继器控件，可以将 FormView 视为用于显示单个记录的中继器。

将 FormView 控件添加到 `SimpleDisplay.aspx` 页面的设计图面。 最初，FormView 以灰色块显示，告知我们需要至少提供控件的 `ItemTemplate`。

[![FormView 必须包含 ItemTemplate](displaying-data-with-the-objectdatasource-vb/_static/image46.png)](displaying-data-with-the-objectdatasource-vb/_static/image45.png)

**图 17**： FormView 必须包含 `ItemTemplate` （[单击查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image47.png)）

您可以通过 FormView 的智能标记将 FormView 直接绑定到数据源控件，这将自动创建默认 `ItemTemplate` （连同 `EditItemTemplate` 和 `InsertItemTemplate`，如果 ObjectDataSource 控件的 `InsertMethod` 和 `UpdateMethod` 属性已设置）。 但是，在此示例中，我们将数据绑定到 FormView，并手动指定其 `ItemTemplate`。 首先将 FormView 的 `DataSourceID` 属性设置为 ObjectDataSource 控件的 `ID`，`ObjectDataSource1`。 接下来，创建 `ItemTemplate`，使其在 `<h4>` 元素中显示产品的名称和价格，并将其下的类别和货主名称显示为较小的字号。

[!code-aspx[Main](displaying-data-with-the-objectdatasource-vb/samples/sample6.aspx)]

[![第一个产品（Chai）以自定义格式显示](displaying-data-with-the-objectdatasource-vb/_static/image49.png)](displaying-data-with-the-objectdatasource-vb/_static/image48.png)

**图 18**：第一个产品（Chai）以自定义格式显示（[单击以查看完全大小的图像](displaying-data-with-the-objectdatasource-vb/_static/image50.png)）

`<%# Eval(propertyName) %>` 是数据绑定语法。 `Eval` 方法返回当前正在绑定到 FormView 控件的对象的指定属性的值。 有关数据绑定的详细信息，请参阅 Alex Homer 的文章： [ASP.NET 2.0 中的简化和扩展的数据绑定语法](http://www.15seconds.com/issue/040630.htm)。

与 DetailsView 一样，FormView 只显示从 ObjectDataSource 返回的第一条记录。 可以在 FormView 中启用分页，以允许访问者一次单步执行一次产品。

## <a name="summary"></a>总结

无需编写代码，就可以在不编写代码的情况下，访问和显示业务逻辑层中的数据，而无需编写代码。 ObjectDataSource 调用类的指定方法并返回结果。 这些结果可以显示在绑定到 ObjectDataSource 的数据 Web 控件中。 在本教程中，我们将介绍如何将 GridView、DetailsView 和 FormView 控件绑定到 ObjectDataSource。

到目前为止，我们仅了解了如何使用 ObjectDataSource 调用无参数的方法，但如果我们想要调用需要输入参数的方法（如 `ProductBLL` 类的 `GetProductsByCategoryID(categoryID)`），该怎么办？ 为了调用需要一个或多个参数的方法，必须将 ObjectDataSource 配置为指定这些参数的值。 我们将在[下一教程](declarative-parameters-vb.md)中了解如何实现此目的。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [创建自己的数据源控件](https://msdn.microsoft.com/library/ms364049.aspx)
- [ASP.NET 2.0 的 GridView 示例](https://msdn.microsoft.com/library/aa479339.aspx)
- [ASP.NET 2.0 中的简化和扩展的数据绑定语法](http://www.15seconds.com/issue/040630.htm)
- [ASP.NET 2.0 中的主题](http://www.odetocode.com/Articles/423.aspx)
- [使用主题的服务器端样式](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [如何：以编程方式应用 ASP.NET 主题](https://msdn.microsoft.com/library/tx35bd89.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Hilton Giesenow。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)
> [下一页](declarative-parameters-vb.md)
