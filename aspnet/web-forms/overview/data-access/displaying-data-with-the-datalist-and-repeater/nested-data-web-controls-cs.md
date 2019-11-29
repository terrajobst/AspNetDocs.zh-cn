---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
title: 嵌套的数据 Web 控件C#（） |Microsoft Docs
author: rick-anderson
description: 在本教程中，我们将探讨如何使用嵌套在其他中继器内的中继器。 这些示例将演示如何在 d 。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: ad3cb0ec-26cf-42d7-b81b-184a34ec9f86
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8ef15bebb2c29976274b0cca1d6ace434ccc55ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640306"
---
# <a name="nested-data-web-controls-c"></a>嵌套的数据 Web 控件 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_32_CS.exe)或[下载 PDF](nested-data-web-controls-cs/_static/datatutorial32cs1.pdf)

> 在本教程中，我们将探讨如何使用嵌套在其他中继器内的中继器。 这些示例将演示如何以声明方式和编程方式填充内部中继器。

## <a name="introduction"></a>简介

除了静态 HTML 和数据绑定语法外，模板还可以包括 Web 控件和用户控件。 可以通过声明性的数据绑定语法为这些 Web 控件分配其属性，也可以通过编程方式在相应的服务器端事件处理程序中对其进行访问。

通过在模板中嵌入控件，可以自定义和改进外观和用户体验。 例如，在 GridView 控件教程中的 "[使用 templatefield](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) " 教程中，我们看到了如何通过在 TemplateField 中添加 Calendar 控件来自定义 GridView 的显示，以显示雇员的雇佣日期;在向[编辑和插入界面添加验证控件](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)和[自定义数据修改接口](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教程中，我们了解了如何通过添加验证控件、文本框、DropDownLists 和其他 Web 控件自定义编辑和插入界面。

模板还可以包含其他数据 Web 控件。 也就是说，在模板中，可以有一个 DataList，其中包含另一个 DataList （或 Repeater、GridView 或 DetailsView，等等）。 此类接口的难题是将相应的数据绑定到内部数据 Web 控件。 有几种不同的方法可用，范围从使用 ObjectDataSource 的声明性选项到编程方法。

在本教程中，我们将探讨如何使用嵌套在其他中继器内的中继器。 外部中继器将为数据库中的每个类别包含一项，并显示类别 "名称" 和 "说明"。 每个类别项的内部中继器都将显示属于该类别的每个产品的信息（参见图1）。 下面的示例演示如何以声明方式和编程方式填充内部中继器。

[列出了每个类别及其产品的 ![](nested-data-web-controls-cs/_static/image2.png)](nested-data-web-controls-cs/_static/image1.png)

**图 1**：列出了每个类别及其产品（[单击以查看完全大小的图像](nested-data-web-controls-cs/_static/image3.png)）

## <a name="step-1-creating-the-category-listing"></a>步骤1：创建类别列表

在生成使用嵌套数据 Web 控件的页面时，我发现首先设计、创建和测试最外面的数据 Web 控件是非常有帮助的，无需担心内部嵌套控件。 因此，让我们先完成向页面中添加中继器的必要步骤，其中列出了每个类别的名称和描述。

首先打开 `DataListRepeaterBasics` 文件夹中的 "`NestedControls.aspx`" 页，然后将 "Repeater" 控件添加到页面，并将其 `ID` 属性设置为 "`CategoryList`"。 从 "Repeater" 智能标记中，选择创建名为 `CategoriesDataSource`的新 ObjectDataSource。

[![命名新的 ObjectDataSource CategoriesDataSource](nested-data-web-controls-cs/_static/image5.png)](nested-data-web-controls-cs/_static/image4.png)

**图 2**：将新的 ObjectDataSource 命名 `CategoriesDataSource` （[单击以查看完全大小的映像](nested-data-web-controls-cs/_static/image6.png)）

配置 ObjectDataSource，使其从 `CategoriesBLL` 类 `GetCategories` 方法拉取其数据。

[![将 ObjectDataSource 配置为使用 CategoriesBLL Class s GetCategories 方法](nested-data-web-controls-cs/_static/image8.png)](nested-data-web-controls-cs/_static/image7.png)

**图 3**：将 ObjectDataSource 配置为使用 `CategoriesBLL` 类 `GetCategories` 方法（[单击以查看完全大小的映像](nested-data-web-controls-cs/_static/image9.png)）

若要指定 Repeater 的模板内容，需要先进入源视图，然后手动输入声明性语法。 添加一个 `ItemTemplate`，该显示 `<h4>` 元素中的类别名称和段落元素（`<p>`）中的类别说明。 此外，让我们用水平标尺（`<hr>`）分隔每个类别。 进行这些更改后，页面应包含与以下内容类似的中继器和 ObjectDataSource 的声明性语法：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample1.aspx)]

图4显示了通过浏览器查看时的进度。

[![列出了每个类别的名称和说明，并以水平规则分隔](nested-data-web-controls-cs/_static/image11.png)](nested-data-web-controls-cs/_static/image10.png)

**图 4**：列出了每个类别的 "名称" 和 "说明"，并以水平规则分隔（[单击以查看完全大小的图像](nested-data-web-controls-cs/_static/image12.png)）

## <a name="step-2-adding-the-nested-product-repeater"></a>步骤2：添加嵌套产品中继器

类别列表完成后，接下来的任务是向 `CategoryList` 的 `ItemTemplate` 添加一个中继器，以显示有关属于相应类别的产品的信息。 有多种方法可以检索此内部中继器的数据，其中两种方法将很快进行探讨。 现在，让我们在 `CategoryList` Repeater `ItemTemplate`中创建产品中继器。 具体而言，让我们的产品中继器在项目符号列表中显示每个产品，每个列表项包括产品的名称和价格。

若要创建此中继站，需要手动将内部中继器声明性语法和模板输入到 `CategoryList` 的 `ItemTemplate`中。 在 `CategoryList` Repeater `ItemTemplate`中添加以下标记：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample2.aspx)]

## <a name="step-3-binding-the-category-specific-products-to-the-productsbycategorylist-repeater"></a>步骤3：将特定于类别的产品绑定到 ProductsByCategoryList 中继器

如果此时通过浏览器访问该页，屏幕将与图4中的外观相同，因为我们尚未将任何数据绑定到中继器。 可以通过几种方式来获取适当的产品记录，并将它们绑定到中继器，这比其他方式更有效。 这里的主要难题是返回指定类别的相应产品。

绑定到内部 Repeater 控件的数据可以通过声明性访问，通过 `CategoryList` Repeater s `ItemTemplate`中的 ObjectDataSource 进行访问，也可以通过编程方式从 ASP.NET 页的代码隐藏页访问。 同样，可以通过内部中继器 `DataSourceID` 属性或通过声明性的数据绑定语法或以编程方式将此数据绑定到内部中继器，方法是：在 `CategoryList` 中继器 s `ItemDataBound` 事件处理程序中引用内部中继器，以编程方式设置其 `DataSource` 属性，并调用其 `DataBind()` 方法。 让我们来了解一下这些方法。

## <a name="accessing-the-data-declaratively-with-an-objectdatasource-control-and-theitemdataboundevent-handler"></a>用 ObjectDataSource 控件和`ItemDataBound`事件处理程序以声明方式访问数据

由于我们已在本系列教程中广泛使用了 ObjectDataSource，因此在此示例中访问数据的最自然选择是坚持 ObjectDataSource。 `ProductsBLL` 类具有一个 `GetProductsByCategoryID(categoryID)` 方法，该方法返回有关属于指定 *`categoryID`* 的产品的信息。 因此，可以将 ObjectDataSource 添加到 `CategoryList` Repeater `ItemTemplate`，并将其配置为从此类方法访问其数据。

遗憾的是，Repeater 不允许通过设计视图编辑其模板，因此需要手动为此 ObjectDataSource 控件添加声明性语法。 下面的语法演示了在添加此新 ObjectDataSource （`ProductsByCategoryDataSource`）之后 `ItemTemplate` `CategoryList` 中继站：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample3.aspx)]

使用 ObjectDataSource 方法时，需要将 `ProductsByCategoryList` Repeater `DataSourceID` 属性设置为 ObjectDataSource （`ProductsByCategoryDataSource`）的 `ID`。 另请注意，我们的 ObjectDataSource 包含一个 `<asp:Parameter>` 元素，该元素指定将传递到 `GetProductsByCategoryID(categoryID)` 方法的 *`categoryID`* 值。 但如何指定此值呢？ 理想情况下，我们只需使用数据绑定语法来设置 `<asp:Parameter>` 元素的 `DefaultValue` 属性，如下所示：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample4.aspx)]

遗憾的是，数据绑定语法只在具有 `DataBinding` 事件的控件中有效。 `Parameter` 类缺少此类事件，因此上述语法是非法的，将导致运行时错误。

若要设置此值，需要为 `CategoryList` Repeater `ItemDataBound` 事件创建事件处理程序。 请记住，对于绑定到中继器的每个项，`ItemDataBound` 事件将激发一次。 因此，每次对外部中继器引发此事件时，都可以将当前 `CategoryID` 值分配给 `ProductsByCategoryDataSource` ObjectDataSource s `CategoryID` 参数。

使用以下代码为 `CategoryList` Repeater `ItemDataBound` 事件创建事件处理程序：

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample5.cs)]

此事件处理程序首先确保我们正在处理某个数据项，而不是标头、脚注或分隔符项。 接下来，引用刚刚绑定到当前 `RepeaterItem`的实际 `CategoriesRow` 实例。 最后，引用 `ItemTemplate` 中的 ObjectDataSource，并将其 `CategoryID` 参数值分配给当前 `RepeaterItem`的 `CategoryID`。

在此事件处理程序中，每个 `RepeaterItem` 中的 `ProductsByCategoryList` 中继器都绑定到 `RepeaterItem` 类别中的那些产品。 图5显示了生成的输出的屏幕截图。

[![外部中继器列出了每个类别;内部为该类别列出的产品](nested-data-web-controls-cs/_static/image14.png)](nested-data-web-controls-cs/_static/image13.png)

**图 5**：外部中继器列出了每个类别;内部列出该类别的产品（[单击以查看完全大小的图像](nested-data-web-controls-cs/_static/image15.png)）

## <a name="accessing-the-products-by-category-data-programmatically"></a>以编程方式访问按类别数据列出的产品

我们可以在 ASP.NET 页的代码隐藏类（或在 `App_Code` 文件夹中或单独的类库项目中）创建一个方法，该方法在 `CategoryID`时返回适当的一组产品，而不是使用 ObjectDataSource 检索当前类别的产品。 假设我们在 ASP.NET page s 代码隐藏类中具有此类方法，并将其命名为 `GetProductsInCategory(categoryID)`。 使用此方法时，我们可以使用以下声明性语法将当前类别的产品绑定到内部中继器：

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample6.aspx)]

Repeater `DataSource` 属性使用 databinding 语法来指示它的数据来自 `GetProductsInCategory(categoryID)` 方法。 由于 `Eval("CategoryID")` 返回 `Object`类型的值，因此我们将对象强制转换为 `Integer`，然后将其传递到 `GetProductsInCategory(categoryID)` 方法。 请注意，此处通过数据绑定语法访问的 `CategoryID` 是*外部*中继器（`CategoryList`）中的 `CategoryID`，它绑定到 `Categories` 表中的记录。 因此，我们知道 `CategoryID` 不能是数据库 `NULL` 值，这就是我们可以在不检查是否正在处理 `DBNull`的情况下，盲目地强制转换 `Eval` 方法的原因。

使用此方法，我们需要创建 `GetProductsInCategory(categoryID)` 方法，并让它在给定提供的 *`categoryID`* 的情况下检索相应的产品集。 只需返回 `ProductsBLL` 类 `GetProductsByCategoryID(categoryID)` 方法返回的 `ProductsDataTable`，即可实现此目的。 让我们在 `NestedControls.aspx` 页的代码隐藏类中创建 `GetProductsInCategory(categoryID)` 方法。 使用以下代码执行此操作：

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample7.cs)]

此方法只是创建 `ProductsBLL` 方法的实例，并返回 `GetProductsByCategoryID(categoryID)` 方法的结果。 请注意，该方法必须标记 `Public` 或 `Protected`;如果该方法被标记为 `Private`，将无法从 ASP.NET 页的声明性标记访问该方法。

进行这些更改以使用这一新方法之后，请花点时间查看浏览器中的页面。 使用 ObjectDataSource 和 `ItemDataBound` 事件处理程序方法时，输出应与输出相同（请参阅图5以查看屏幕截图）。

> [!NOTE]
> 在 ASP.NET page s 代码隐藏类中创建 `GetProductsInCategory(categoryID)` 方法可能看起来工作量。 毕竟，此方法只是创建 `ProductsBLL` 类的实例并返回其 `GetProductsByCategoryID(categoryID)` 方法的结果。 为什么不直接从内部中继器中的数据绑定语法调用此方法，例如： `DataSource='<%# ProductsBLL.GetProductsByCategoryID((int)(Eval("CategoryID"))) %>'`？ 尽管此语法不能与当前的 `ProductsBLL` 类实现一起使用（因为 `GetProductsByCategoryID(categoryID)` 方法是实例方法），但你可以将 `ProductsBLL` 修改为包含静态 `GetProductsByCategoryID(categoryID)` 方法，或让类包含静态 `Instance()` 方法以返回 `ProductsBLL` 类的新实例。

尽管此类修改不需要 ASP.NET 页 s 代码隐藏类中的 `GetProductsInCategory(categoryID)` 方法，但代码隐藏类方法使我们能够更灵活地处理检索到的数据。

## <a name="retrieving-all-of-the-product-information-at-once"></a>同时检索所有产品信息

通过调用 `ProductsBLL` 类 `GetProductsByCategoryID(categoryID)` 方法（第一种方法是通过 ObjectDataSource 进行的，第二种方法是通过代码隐藏类中的 `GetProductsInCategory(categoryID)` 方法实现），我们已检查了两个早期方法，通过调用该方法获取当前类别的产品。 每次调用此方法时，业务逻辑层都向下调用数据访问层，这将使用 SQL 语句查询数据库，该语句将返回 `Products` 表中的行，该语句的 `CategoryID` 字段与提供的输入参数相匹配。

对于系统中的*n*个类别，此方法网络*n* + 1 调用数据库一个数据库查询以获取所有类别，然后按*N*次调用来获取特定于每个类别的产品。 但是，我们可以仅在两个数据库中检索所有所需的数据，调用一次调用来获取所有类别，并将另一调用用于获取所有产品。 完成所有产品后，便可以对这些产品进行筛选，以便仅将与当前 `CategoryID` 匹配的产品绑定到该类别的内部中继器。

为了提供此功能，我们只需对 ASP.NET 页 s 代码隐藏类中的 `GetProductsInCategory(categoryID)` 方法进行少许修改。 我们不会盲目地返回 `ProductsBLL` 类 `GetProductsByCategoryID(categoryID)` 方法的结果，而是先访问*所有*产品（如果尚未对其进行访问），然后基于传入的 `CategoryID`只返回产品的筛选视图。

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample8.cs)]

请注意，页面级变量的添加 `allProducts`。 这包含所有产品的相关信息，并在第一次调用 `GetProductsInCategory(categoryID)` 方法时填充。 在确保已创建并填充 `allProducts` 对象之后，该方法将筛选 DataTable 结果，以便只能访问 `CategoryID` 与指定 `CategoryID` 匹配的行。 此方法减少了从*N* + 1 到2访问数据库的次数。

此增强功能不会对页面的呈现标记进行任何更改，也不会像其他方法那样返回更少的记录。 它只是减少对数据库的调用次数。

> [!NOTE]
> 一种可能的原因是减少数据库访问的数量会肯定提高性能。 但这可能不是这样。 例如，如果有大量的产品 `CategoryID` `NULL`，则对 `GetProducts` 方法的调用将返回一系列从未显示的产品。 而且，如果您只显示了几个类别的子集，则返回所有产品可能会浪费大量的情况。

与往常一样，在分析两种方法的性能时，唯一的 surefire 度量值是针对应用程序的常见案例运行受控测试。

## <a name="summary"></a>总结

在本教程中，我们介绍了如何将一个数据 Web 控件嵌套在另一个数据控件中，特别是检查如何让外部中继器为每个类别显示一个项，并在列表中列出每个类别的产品。 构建嵌套用户界面的主要难题在于访问和将正确的数据绑定到内部数据 Web 控件。 有多种方法可供使用，这两个方法在本教程中进行了介绍。 第一种方法是使用外部数据 Web 控件中的 ObjectDataSource `ItemTemplate` 通过其 `DataSourceID` 属性绑定到内部数据 Web 控件。 第二种方法是通过 ASP.NET 页 s 代码隐藏类中的方法访问数据。 然后，可以通过数据绑定语法将此方法绑定到内部数据 Web 控件的 `DataSource` 属性。

虽然本教程中所述的嵌套用户界面使用了嵌套在中继器内的中继器，但这些技术可以扩展到其他数据 Web 控件。 可以在 GridView 内或 DataList 内的 GridView 中嵌套中继器，等等。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Zack 的 Liz Shulok。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
> [下一页](displaying-data-with-the-datalist-and-repeater-controls-vb.md)
