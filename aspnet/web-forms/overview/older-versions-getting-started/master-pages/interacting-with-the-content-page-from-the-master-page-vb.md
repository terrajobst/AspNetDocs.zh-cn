---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
title: 从母版页与内容页交互（VB） |Microsoft Docs
author: rick-anderson
description: 检查如何从母版页中的代码调用内容页的方法、设置属性等。
ms.author: riande
ms.date: 07/11/2008
ms.assetid: a6e2e1a0-c925-43e9-b711-1f178fdd72d7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 5367ad1b7f2fa11c635ad95754c9bcc1edcb6c1d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464534"
---
# <a name="interacting-with-the-content-page-from-the-master-page-vb"></a>从母版页与内容页交互 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_VB.zip)或[下载 PDF](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_VB.pdf)

> 检查如何从母版页中的代码调用内容页的方法、设置属性等。

## <a name="introduction"></a>简介

前面的教程介绍了如何使内容页以编程方式与母版页交互。 回忆一下，我们已将母版页更新为包含一个 GridView 控件，该控件列出了五个最近添加的产品。 然后，我们创建了一个内容页面，用户可在其中添加新产品。 添加新产品后，需指导母版页刷新其 GridView，使其包含刚添加的产品。 此功能的实现方法是：向母版页添加一个公共方法，该母版页刷新绑定到 GridView 的数据，然后从内容页中调用该方法。

最常见的内容和母版页交互形式源自内容页。 不过，母版页可能会将当前内容页 rouse 到操作中，如果母版页包含允许用户修改也显示在内容页上的数据的用户界面元素，则可能需要此类功能。 请考虑一个显示 GridView 控件中的产品信息的内容页，以及一个包含按钮控件的母版页，单击该按钮可将所有产品的价格加倍。 与上一教程中的示例非常类似，单击 "双重价格" 按钮后需要刷新 GridView，以便显示新的价格，但在此方案中，它是需要将内容页 rouse 到操作中的母版页。

本教程将探讨如何在 "内容" 页中定义母版页调用功能。

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a>通过事件和事件处理程序进行的 Instigating 编程交互

从母版页调用内容页功能比另一种方法更具挑战性。 由于内容页有一个母版页，因此当 instigating 从内容页进行编程交互时，我们知道哪些公共方法和属性是我们的处置方法。 但是，母版页可以有许多不同的内容页，每个内容页都具有自己的一组属性和方法。 接下来，我们如何在母版页中编写代码，以在其内容页中执行某些操作，而在运行时之前不知道将调用哪个内容页？

假设有一个 ASP.NET 的 Web 控件，如 Button 控件。 按钮控件可以出现在任意数量的 ASP.NET 页面上并需要一种机制，通过该机制可以向页面发出警报。 这是使用*事件*实现的。 特别是，按钮控件在被单击时引发其 `Click` 事件;包含按钮的 "ASP.NET" 页可以选择通过*事件处理程序*来响应该通知。

此相同模式可用于在其内容页中拥有母版页触发器功能：

1. 向母版页添加一个事件。
2. 每当母版页需要与其内容页通信时，引发事件。 例如，如果母版页需要提醒其内容页，用户已将价格增加了一倍，则在双倍价格后会立即引发事件。
3. 在需要采取某种操作的内容页中创建事件处理程序。

本教程的其余部分将实现简介中概述的示例;这是一个内容页，其中列出了数据库中的产品和一个母版页，其中包含一个按钮控件来使价格翻倍。

## <a name="step-1-displaying-products-in-a-content-page"></a>步骤1：在内容页中显示产品

我们的第一个业务顺序是创建一个内容页，该页面列出 Northwind 数据库中的产品。 （我们将 Northwind 数据库添加到了前面教程中的项目，[*与内容页中的母版页交互*](interacting-with-the-master-page-from-the-content-page-vb.md)。）首先将新的 ASP.NET 页面添加到名为 `Products.aspx`的 `~/Admin` 文件夹中，并确保将其绑定到 `Site.master` 母版页。 图1显示了将此页面添加到网站后解决方案资源管理器。

[![将新的 ASP.NET 页面添加到管理文件夹](interacting-with-the-content-page-from-the-master-page-vb/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image1.png)

**图 01**：将新的 "ASP.NET" 页添加到 `Admin` 文件夹（[单击查看完全大小的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image3.png)）

请记住，在[*母版页教程中指定标题、Meta 标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)时，我们创建了一个名为 `BasePage` 的自定义基类类，如果未显式设置该页面的标题，则生成该页面的标题。 转到 "`Products.aspx`" 页的代码隐藏类，并使其从 `BasePage` （而不是从 `System.Web.UI.Page`）派生。

最后，更新 `Web.sitemap` 文件以包含本课中的条目。 将以下标记添加到内容到母版页交互课程的 `<siteMapNode>` 下面：

[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample1.xml)]

此 `<siteMapNode>` 元素的添加将反映在课程列表中（见图5）。

返回 `Products.aspx`。 在 `MainContent`的内容控件中，添加 GridView 控件并将其命名为 `ProductsGrid`。 将 GridView 绑定到名为 `ProductsDataSource`的新 SqlDataSource 控件。

[![将 GridView 绑定到新的 SqlDataSource 控件](interacting-with-the-content-page-from-the-master-page-vb/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image4.png)

**图 02**：将 GridView 绑定到新的 SqlDataSource 控件（[单击以查看完全大小的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image6.png)）

将向导配置为使用 Northwind 数据库。 如果已完成上述教程，则在 `Web.config`中应该已经有一个名为 `NorthwindConnectionString` 的连接字符串。 从下拉列表中选择此连接字符串，如图3所示。

[![将 SqlDataSource 配置为使用 Northwind 数据库](interacting-with-the-content-page-from-the-master-page-vb/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image7.png)

**图 03**：将 SqlDataSource 配置为使用 Northwind 数据库（[单击查看完全大小的映像](interacting-with-the-content-page-from-the-master-page-vb/_static/image9.png)）

接下来，通过从下拉列表中选择 Products 表并返回 `ProductName` 和 `UnitPrice` 列来指定数据源控件的 `SELECT` 语句（参见图4）。 单击 "下一步"，然后单击 "完成" 完成配置数据源向导。

[![从 Products 表中返回 "ProductName" 和 "单价" 字段](interacting-with-the-content-page-from-the-master-page-vb/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image10.png)

**图 04**：返回 `Products` 表中的 "`ProductName`" 和 "`UnitPrice`" 字段（[单击以查看完全大小的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image12.png)）

就这么简单！ 完成向导后，Visual Studio 会将两个 BoundFields 添加到 GridView，以反映 SqlDataSource 控件返回的两个字段。 GridView 和 SqlDataSource 控件的标记如下所示。 图5显示了通过浏览器查看的结果。

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample2.aspx)]

[GridView 中列出了每个产品及其价格 ![](interacting-with-the-content-page-from-the-master-page-vb/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image13.png)

**图 05**：在 GridView 中列出了每个产品及其价格（[单击查看完全大小的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image15.png)）

> [!NOTE]
> 随意清理 GridView 的外观。 某些建议包括将显示的 "单价" 值的格式设置为货币，并使用背景色和字体来改善网格的外观。 有关在 ASP.NET 中显示和格式化数据的详细信息，请参阅[使用数据教程系列](../../data-access/index.md)。

## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a>步骤2：向母版页添加双重价格按钮

下一项任务是将按钮 Web 控件添加到母版页，单击该控件时，会将数据库中所有产品的价格翻倍。 打开 `Site.master` 母版页，然后将一个按钮从工具箱拖动到设计器上，将其放在上一教程中添加的 `RecentProductsDataSource` SqlDataSource 控件下。 将该按钮的 `ID` 属性设置为 `DoublePrice`，其 `Text` 属性设置为 "双积价格"。

接下来，将 SqlDataSource 控件添加到母版页，并 `DoublePricesDataSource`命名。 此 SqlDataSource 将用于执行 `UPDATE` 语句以将所有价格加倍。 具体而言，我们需要设置其 `ConnectionString`，并 `UpdateCommand` 属性设置为相应的连接字符串和 `UPDATE` 语句。 然后，需要在单击 "`DoublePrice`" 按钮时调用此 SqlDataSource 控件的 `Update` 方法。 若要设置 "`ConnectionString`" 和 "`UpdateCommand`" 属性，请选择 SqlDataSource 控件，然后选择 "属性窗口"。 `ConnectionString` 属性列出了已存储在下拉列表中 `Web.config` 的连接字符串;选择 "`NorthwindConnectionString`" 选项，如图6所示。

[![将 SqlDataSource 配置为使用 NorthwindConnectionString](interacting-with-the-content-page-from-the-master-page-vb/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image16.png)

**图 06**：将 SqlDataSource 配置为使用 `NorthwindConnectionString` （[单击查看完全大小的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image18.png)）

若要设置 `UpdateCommand` 属性，请在属性窗口中找到 UpdateQuery 选项。 此属性在选中时显示带有省略号的按钮;单击此按钮可显示图7中所示的 "命令和参数编辑器" 对话框。 在对话框的文本框中键入以下 `UPDATE` 语句：

[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample3.sql)]

执行此语句时，将为 `Products` 表中的每条记录将 `UnitPrice` 值加倍。

[![设置 SqlDataSource 的 UpdateCommand 属性](interacting-with-the-content-page-from-the-master-page-vb/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image19.png)

**图 07**：设置 SqlDataSource 的 `UpdateCommand` 属性（[单击以查看完全大小的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image21.png)）

设置这些属性之后，Button 和 SqlDataSource 控件的声明性标记应如下所示：

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample4.aspx)]

在单击 "`DoublePrice`" 按钮时，剩下的就是调用 `Update` 方法。 为 "`DoublePrice`" 按钮创建 `Click` 事件处理程序并添加以下代码：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample5.vb)]

若要测试此功能，请访问我们在步骤1中创建的 `~/Admin/Products.aspx` 页面，然后单击 "产品价格翻倍" 按钮。 单击该按钮将导致回发，并执行 "`DoublePrice`" 按钮的 `Click` 事件处理程序，使所有产品的价格翻倍。 然后，将重新呈现页面，并在浏览器中返回并重新显示标记。 但在 "内容" 页中，GridView 列出的价格与单击 "双积价格" 按钮之前的价格相同。 这是因为，在 GridView 中最初加载的数据将其状态存储在视图状态中，因此除非另外说明，否则不会在回发时重新加载它。 如果访问其他页面，然后返回 `~/Admin/Products.aspx` 页面，则会看到更新的价格。

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a>步骤3：当价格加倍时引发事件

由于 "`~/Admin/Products.aspx`" 页中的 GridView 不会立即反映价格翻倍，因此用户可能会理解认为他们未单击 "产品价格" 按钮，或者该按钮不起作用。 它们可能会多次尝试单击该按钮，并再次将该价格加倍。 若要解决此问题，我们需要在 "内容" 页中的网格立即显示新价格。

如本教程前面所述，每当用户单击 "`DoublePrice`" 按钮时，我们都需要在母版页中引发事件。 事件是一种类（事件发布者）通知另一组其他有意义的类（事件订阅者）的方法。 在此示例中，母版页是事件发布者;当单击 "`DoublePrice`" 按钮时，这些内容页是订阅服务器。

类通过创建事件处理程序订阅事件，该*事件处理程序*是为响应所引发的事件而执行的方法。 发布者通过定义*事件委托*来定义他引发的事件。 事件委托指定事件处理程序必须接受的输入参数。 在 .NET Framework 中，事件委托不返回任何值，并接受两个输入参数：

- 用于标识事件源的 `Object`，
- 派生自 `System.EventArgs` 的类

传递给事件处理程序的第二个参数可以包括有关事件的其他信息。 虽然基 `EventArgs` 类未通过任何信息，但 .NET Framework 包含许多扩展 `EventArgs` 和包含附加属性的类。 例如，`CommandEventArgs` 实例将传递给响应 `Command` 事件的事件处理程序，并包括两个信息性属性： `CommandArgument` 和 `CommandName`。

> [!NOTE]
> 有关创建、引发和处理事件的详细信息，请参阅[采用简单英语的](http://www.codeproject.com/KB/cs/eventdelegates.aspx)[事件和委托](https://msdn.microsoft.com/library/17sde2xt.aspx)和事件委托。

若要定义事件，请使用以下语法：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample6.vb)]

由于我们只需在用户单击 "`DoublePrice`" 按钮时对内容页发出警报，而无需通过其他任何其他信息传递，因此我们可以使用事件委托 `EventHandler`，它定义一个事件处理程序，该事件处理程序接受作为其第二个参数的类型 `System.EventArgs`的对象。 若要在母版页中创建事件，请将以下代码行添加到母版页的代码隐藏类：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample7.vb)]

上面的代码将一个公共事件添加到名为 `PricesDoubled`的母版页。 现在，我们需要在价格翻倍后引发此事件。 若要引发事件，请使用以下语法：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample8.vb)]

其中，*发送方*和*eventArgs*是要传递到订阅服务器的事件处理程序的值。

将 `DoublePrice` `Click` 事件处理程序更新为以下代码：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample9.vb)]

与之前一样，`Click` 事件处理程序首先调用 `DoublePricesDataSource` SqlDataSource 控件的 `Update` 方法，将所有产品的价格翻倍。 下面是对事件处理程序进行了两项添加。 首先，刷新 `RecentProducts` GridView 的数据。 此 GridView 添加到了前面教程中的母版页，并显示了五个最近添加的产品。 我们需要刷新此网格，使其显示这5个产品的刚好翻倍的价格。 之后，会引发 `PricesDoubled` 事件。 对母版页本身（`Me`）的引用将作为事件源发送到事件处理程序，并以事件参数的形式发送空的 `EventArgs` 对象。

## <a name="step-4-handling-the-event-in-the-content-page"></a>步骤4：处理内容页中的事件

此时，只要单击 `DoublePrice` 按钮控件，母版页就会引发其 `PricesDoubled` 事件。 但是，这只是工作的一半，我们仍需要处理订阅服务器上的事件。 这涉及两个步骤：创建事件处理程序和添加事件布线代码，以便在引发事件时执行事件处理程序。

首先，创建一个名为 `Master_PricesDoubled`的事件处理程序。 由于我们在母版页中定义了 `PricesDoubled` 事件，因此，事件处理程序的两个输入参数必须分别为 `Object` 和 `EventArgs`类型。 在事件处理程序中，调用 `ProductsGrid` GridView 的 `DataBind` 方法将数据重新绑定到网格。

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample10.vb)]

事件处理程序的代码已完成，但我们尚未将母版页的 `PricesDoubled` 事件连接到此事件处理程序。 订阅服务器通过以下语法将事件线路到事件处理程序：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample11.vb)]

"*发布服务器*" 是对提供事件*事件名称的*对象的引用，"*方法*名称" 是订阅服务器中定义的事件处理程序的名称。

必须在第一页访问和后续回发中执行此事件布线代码，并应在页面生命周期中的某个时间点执行此事件布线。 添加事件布线代码的好时机是在 PreInit 阶段，这种情况在页面生命周期中非常早发生。

打开 `~/Admin/Products.aspx` 并创建 `Page_PreInit` 事件处理程序：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample12.vb)]

若要完成此布线代码，我们需要从内容页以编程方式引用母版页。 如前面的教程中所述，有两种方法可实现此目的：

- 通过将松类型 `Page.Master` 属性转换为相应的母版页类型，或
- 通过在 `.aspx` 页中添加一个 `@MasterType` 指令，然后使用强类型 `Master` 属性。

使用后一种方法。 将以下 `@MasterType` 指令添加到页面的声明性标记的顶部：

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample13.aspx)]

然后在 `Page_PreInit` 事件处理程序中添加以下事件布线代码：

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample14.vb)]

将此代码放入后，只要单击 "`DoublePrice`" 按钮，内容页中的 GridView 就会被刷新。

图8和9说明了此行为。 图8显示第一次访问时的页面。 请注意，`RecentProducts` GridView 中的价格值（在母版页的左栏中）和 `ProductsGrid` GridView （在 "内容" 页中）。 图9显示了在单击 "`DoublePrice`" 按钮后立即显示的同一屏幕。 正如您所看到的，这两个 GridViews 中的新价格会立即反映出来。

[![初始价格值](interacting-with-the-content-page-from-the-master-page-vb/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image22.png)

**图 08**：初始价格值（[单击以查看完全大小的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image24.png)）

[![在 GridViews 中显示双线价格](interacting-with-the-content-page-from-the-master-page-vb/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image25.png)

**图 09**： GridViews 中显示最大的价格（[单击以查看完全大小的图像](interacting-with-the-content-page-from-the-master-page-vb/_static/image27.png)）

## <a name="summary"></a>摘要

理想情况下，母版页及其内容页完全独立，无需交互。 但是，如果您有一个母版页或内容页，其中显示了可从母版页或内容页修改的数据，则在修改数据以便可以更新显示内容页时，您可能需要将母版页通知内容页（或相反）。 在前面的教程中，我们看到了如何使内容页以编程方式与母版页交互;在本教程中，我们介绍了如何使母版页启动交互。

尽管内容和母版页之间的编程交互可以来自内容或母版页，但使用的交互模式取决于源。 不同之处在于内容页有一个母版页，但一个母版页可以有许多不同的内容页。 更好的方法是使母版页引发一个事件，以指示发生了某种操作，而不是让母版页直接与内容页交互。 关心此操作的那些内容页可以创建事件处理程序。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [访问和更新 ASP.NET 中的数据](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [事件和委托](https://msdn.microsoft.com/library/17sde2xt.aspx)
- [在内容和母版页之间传递信息](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [使用 ASP.NET 教程中的数据](../../data-access/index.md)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Suchi Banerjee。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](interacting-with-the-master-page-from-the-content-page-vb.md)
> [下一页](master-pages-and-asp-net-ajax-vb.md)
