---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
title: 用 ObjectDataSource 缓存数据（VB） |Microsoft Docs
author: rick-anderson
description: 缓存可以表示慢速 Web 应用程序和快速 Web 应用程序之间的差异。 本教程是第四个教程，详细了解 ASP.NET 中的缓存 。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 2e56a733-5512-48a6-9276-70a65bbe4d5d
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-vb
msc.type: authoredcontent
ms.openlocfilehash: 16f20d9a0f4f677073174d680418b278dba40b07
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78443144"
---
# <a name="caching-data-with-the-objectdatasource-vb"></a>使用 ObjectDataSource 缓存数据 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_VB.exe)或[下载 PDF](caching-data-with-the-objectdatasource-vb/_static/datatutorial58vb1.pdf)

> 缓存可以表示慢速 Web 应用程序和快速 Web 应用程序之间的差异。 本教程是在 ASP.NET 中详细了解缓存的第四个教程。 了解缓存的关键概念，以及如何通过 ObjectDataSource 控件将缓存应用到表示层。

## <a name="introduction"></a>简介

在计算机科学中，*缓存*是指获取数据或信息的过程，这些数据或信息在访问速度更快的位置获取并存储其副本的费用很高。 对于数据驱动的应用程序，大型和复杂的查询通常会消耗应用程序的大部分执行时间。 这样，应用程序的性能通常可以通过将昂贵的数据库查询结果存储在内存中来提高性能。

ASP.NET 2.0 提供各种缓存选项。 可以通过*输出缓存*来缓存整个网页或用户控件的呈现的标记。 ObjectDataSource 和 SqlDataSource 控件也提供了缓存功能，从而允许在控件级别缓存数据。 和 ASP.NET 的*数据缓存*提供丰富的缓存 API，使页面开发人员能够以编程方式缓存对象。 在本教程和接下来的三个教程中，我们将使用 ObjectDataSource 的缓存功能以及数据缓存来进行检查。 我们还将探讨如何在启动时缓存应用程序范围内的数据，以及如何通过使用 SQL 缓存依赖项使缓存数据保持最新。 这些教程不会浏览输出缓存。 有关输出缓存的详细信息，请参阅[ASP.NET 2.0 中的输出缓存](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)。

可以在体系结构中的任何位置应用缓存，从数据访问层到表示层。 在本教程中，我们将介绍如何通过 ObjectDataSource 控件将缓存应用到表示层。 在下一教程中，我们将检查业务逻辑层的缓存数据。

## <a name="key-caching-concepts"></a>关键缓存概念

缓存可以通过在可更有效地访问的位置获取大量数据，从而极大地提高应用程序的整体性能和可伸缩性。 由于缓存只包含实际的基础数据的副本，因此，如果基础数据发生更改，它可能会过时或*过时*。 若要对付这一点，页面开发人员可以使用以下任一方法来指示缓存项将从缓存中*逐出*的条件：

- **基于时间的条件**可以将项添加到缓存中，以获得绝对或可调的持续时间。 例如，页开发人员可能会指示持续时间为60秒。 对于绝对持续时间，在将缓存项添加到缓存后，将其逐出60秒，而不考虑访问它的频率。 使用滑动持续时间时，将在上次访问后的60秒内逐出缓存的项。
- **基于依赖项的条件：** 依赖项在添加到缓存时可与项关联。 当项的依赖项发生更改时，它将从缓存中逐出。 依赖项可以是文件、其他缓存项或二者的组合。 ASP.NET 2.0 还允许使用 SQL 缓存依赖项，这些依赖项使开发人员可以向缓存中添加项，并在基础数据库数据发生更改时将其逐出。 我们将[使用 Sql 缓存依赖项](using-sql-cache-dependencies-vb.md)教程来检查 sql 缓存依赖关系。

无论指定了哪些逐出条件，都可以在满足基于时间或依赖项的标准之前*清理*缓存中的项。 如果缓存已达到其容量，则必须先删除现有项，然后才能添加新项。 因此，在以编程方式处理缓存数据时，必须始终假定缓存的数据可能不存在。 我们将在下一教程介绍如何在*体系结构中缓存数据*时，查看以编程方式访问缓存中的数据时使用的模式。

缓存提供了一种经济实惠的方法，用于从应用程序中挤压更多性能。 作为[Steven Smith](http://aspadvice.com/blogs/ssmith/)指定了的文章[ASP.NET 缓存：技术和最佳做法](https://msdn.microsoft.com/library/aa478965.aspx)：

缓存可以是获得足够性能的好办法，无需大量时间和分析。 内存开销较低，因此，如果你可以通过缓存30秒的输出来获得所需的性能，而不是花费一天或一周的时间来优化你的代码或数据库，请执行缓存解决方案（假定旧数据为30秒），然后继续。 最终，糟糕的设计可能会与你保持同步，因此，你当然应尝试正确设计应用程序。 但是，如果你现在只需获得足够的性能，则缓存可以是一个极佳的 [方法]，如果你有时间，则可以随时购买重构应用程序的时间。

虽然缓存可以提供明显的性能增强功能，但它不适用于所有情况（例如，使用实时、频繁更新数据的应用程序），也不适用于不接受的过时数据。 但对于大多数应用程序，应该使用缓存。 有关 ASP.NET 2.0 中缓存的更多背景信息，请参阅[ASP.NET 2.0 快速入门教程](https://quickstarts.asp.net/QuickStartv20/aspnet/)中的[性能缓存](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx)部分。

## <a name="step-1-creating-the-caching-web-pages"></a>步骤1：创建缓存网页

在开始探索 ObjectDataSource 的缓存功能之前，先花点时间在我们的网站项目中创建 ASP.NET 页面，我们将在本教程和接下来的三个网页中创建。 首先添加一个名为 `Caching`的新文件夹。 接下来，将以下 ASP.NET 页面添加到该文件夹，并确保将每个页面与 `Site.master` 母版页关联：

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`

![为与缓存相关的教程添加 ASP.NET 页](caching-data-with-the-objectdatasource-vb/_static/image1.png)

**图 1**：添加用于缓存相关教程的 ASP.NET 页面

与在其他文件夹中一样，`Caching` 文件夹中的 `Default.aspx` 会在其部分列出教程。 请记住，`SectionLevelTutorialListing.ascx` 用户控件提供此功能。 因此，通过将此用户控件从解决方案资源管理器拖到页面 s 设计视图，将该用户控件添加到 `Default.aspx`。

[![图2：将 SectionLevelTutorialListing 用户控件添加到 default.aspx](caching-data-with-the-objectdatasource-vb/_static/image3.png)](caching-data-with-the-objectdatasource-vb/_static/image2.png)

**图 2**：图2：将 `SectionLevelTutorialListing.ascx` 用户控件添加到 `Default.aspx` （[单击查看完全大小的图像](caching-data-with-the-objectdatasource-vb/_static/image4.png)）

最后，将这些页面作为条目添加到 `Web.sitemap` 文件中。 具体而言，请在使用二进制数据后添加以下标记 `<siteMapNode>`：

[!code-xml[Main](caching-data-with-the-objectdatasource-vb/samples/sample1.xml)]

更新 `Web.sitemap`后，请花点时间通过浏览器查看教程网站。 左侧的菜单包含用于缓存教程的项。

![站点映射现在包含用于缓存教程的条目](caching-data-with-the-objectdatasource-vb/_static/image5.png)

**图 3**：站点地图现在包含用于缓存教程的条目

## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>步骤2：在网页中显示产品列表

本教程介绍如何使用 ObjectDataSource control s 内置缓存功能。 但在查看这些功能之前，首先需要一个页面。 让我们创建一个网页，该网页使用 GridView 列出来自 `ProductsBLL` 类的 ObjectDataSource 检索到的产品信息。

首先打开 `Caching` 文件夹中的 "`ObjectDataSource.aspx`" 页。 将 GridView 从工具箱拖到设计器上，将其 `ID` 属性设置为 "`Products`，并从其智能标记中，选择将其绑定到名为 `ProductsDataSource`的新 ObjectDataSource 控件。 将 ObjectDataSource 配置为使用 `ProductsBLL` 类。

[![将 ObjectDataSource 配置为使用 ProductsBLL 类](caching-data-with-the-objectdatasource-vb/_static/image7.png)](caching-data-with-the-objectdatasource-vb/_static/image6.png)

**图 4**：将 ObjectDataSource 配置为使用 `ProductsBLL` 类（[单击以查看完全大小的映像](caching-data-with-the-objectdatasource-vb/_static/image8.png)）

在此页中，让我们创建一个可编辑的 GridView，以便我们可以检查当 ObjectDataSource 中缓存的数据通过 GridView s 接口修改时会发生的情况。 将 "选择" 选项卡中的下拉列表设置为默认值 "`GetProducts()`"，但将 "更新" 选项卡中的选定项更改为接受 `productName`、`unitPrice`和 `productID` 作为其输入参数的 `UpdateProduct` 重载。

[![将 "更新" 选项卡 s 下拉列表设置为相应的 UpdateProduct 重载](caching-data-with-the-objectdatasource-vb/_static/image10.png)](caching-data-with-the-objectdatasource-vb/_static/image9.png)

**图 5**：将 "更新" 选项卡 s 下拉列表设置为相应的 `UpdateProduct` 重载（[单击以查看完全大小的图像](caching-data-with-the-objectdatasource-vb/_static/image11.png)）

最后，在 "插入" 和 "删除" 选项卡中将下拉列表设置为 "（无）"，然后单击 "完成"。 完成配置数据源向导后，Visual Studio 会将 ObjectDataSource `OldValuesParameterFormatString` 属性设置为 `original_{0}`。 如有关[插入、更新和删除数据的概述](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教程中所述，需要从声明性语法中删除此属性或将其设置回默认值，`{0}`，以便更新工作流继续进行而不发生错误。

此外，在完成向导后，Visual Studio 会为每个产品数据字段向 GridView 添加一个字段。 删除除 `ProductName`、`CategoryName`和 `UnitPrice` 的所有 BoundFields。 接下来，将每个 BoundFields 的 `HeaderText` 属性分别更新为 "产品"、"类别" 和 "价格"。 由于 `ProductName` 字段是必需的，因此将 BoundField 转换为 TemplateField，并将 RequiredFieldValidator 添加到 `EditItemTemplate`中。 同样，将 `UnitPrice` BoundField 转换为 TemplateField 并添加 CompareValidator，以确保用户输入的值是大于或等于零的有效货币值。 除了这些修改以外，还可以随意执行任何美观更改，例如右对齐 `UnitPrice` 值，或者在其只读和编辑界面中指定 `UnitPrice` 文本的格式设置。

选中 GridView s 智能标记中的 "启用编辑" 复选框，使 GridView 可编辑。 另请选中 "启用分页" 和 "启用排序" 复选框。

> [!NOTE]
> 需要回顾如何自定义 GridView s 编辑界面？ 如果是这样，请返回到[自定义数据修改界面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教程。

[![启用对编辑、排序和分页的 GridView 支持](caching-data-with-the-objectdatasource-vb/_static/image13.png)](caching-data-with-the-objectdatasource-vb/_static/image12.png)

**图 6**：启用对编辑、排序和分页的 GridView 支持（[单击以查看完全大小的图像](caching-data-with-the-objectdatasource-vb/_static/image14.png)）

进行这些 GridView 修改后，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](caching-data-with-the-objectdatasource-vb/samples/sample2.aspx)]

如图7所示，可编辑 GridView 列出了数据库中每个产品的名称、类别和价格。 请花点时间测试页的功能、对结果进行分页并编辑记录。

[![每种产品的名称、类别和价格都列在可排序、可分页、可编辑的 GridView 中](caching-data-with-the-objectdatasource-vb/_static/image16.png)](caching-data-with-the-objectdatasource-vb/_static/image15.png)

**图 7**：每种产品的名称、类别和价格均以可排序、可分页的可编辑 GridView 列出（[单击以查看完全大小的图像](caching-data-with-the-objectdatasource-vb/_static/image17.png)）

## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>步骤3：检查 ObjectDataSource 请求数据的时间

`Products` GridView 通过调用 `ProductsDataSource` ObjectDataSource 的 `Select` 方法来检索要显示的数据。 此 ObjectDataSource 创建业务逻辑层 s `ProductsBLL` 类的实例，并调用其 `GetProducts()` 方法，后者又将调用数据访问 `ProductsTableAdapter` 层 `GetProducts()` 方法。 DAL 方法连接到 Northwind 数据库，并发出配置的 `SELECT` 查询。 然后，将此数据返回到 DAL，后者将其打包在 `NorthwindDataTable`中。 DataTable 对象将返回到 BLL，并将其返回到 ObjectDataSource，后者将其返回给 GridView。 然后，GridView 为 DataTable 中的每个 `DataRow` 创建一个 `GridViewRow` 对象，每个 `GridViewRow` 最终呈现给返回到客户端并显示在访问者浏览器上的 HTML。

此事件序列每次发生，而 GridView 每次需要绑定到其基础数据。 当首次访问页面、在对 GridView 进行排序时或通过其内置编辑或删除接口修改 GridView 的数据时，会发生这种情况。 如果 GridView 的视图状态为禁用，则将在每次回发时重新绑定 GridView。 GridView 还可以通过调用其 `DataBind()` 方法，显式重新绑定到其数据。

若要完全感谢从数据库检索数据的频率，请让 s 显示一条消息，指示何时重新检索数据。 将标签 Web 控件添加到名为 `ODSEvents`的 GridView 之上。 清除其 `Text` 属性，并将其 `EnableViewState` 属性设置为 "`False`"。 在标签下面，添加一个按钮 Web 控件，并将其 `Text` 属性设置为回发。

[![向 GridView 上方的页面添加标签和按钮](caching-data-with-the-objectdatasource-vb/_static/image19.png)](caching-data-with-the-objectdatasource-vb/_static/image18.png)

**图 8**：向 GridView 上方的页面添加标签和按钮（[单击以查看完全尺寸的图像](caching-data-with-the-objectdatasource-vb/_static/image20.png)）

在数据访问工作流过程中，将在创建基础对象之前激发 ObjectDataSource `Selecting` 事件并调用其配置方法。 为此事件创建事件处理程序并添加以下代码：

[!code-vb[Main](caching-data-with-the-objectdatasource-vb/samples/sample3.vb)]

每次 ObjectDataSource 向数据体系结构发出请求时，该标签都将显示选择 "触发事件" 的文本。

在浏览器中访问此页。 首次访问页面时，将显示 "选择触发的事件" 文本。 单击 "回发" 按钮，请注意文本将消失（假设 GridView `EnableViewState` 属性设置为 `True`（默认值）。 这是因为，在回发时，GridView 是从其视图状态重新构造的，因此不会转换为其数据的 ObjectDataSource。 但对数据进行排序、分页或编辑会导致 GridView 重新绑定到其数据源，因此会重新出现选择事件激发的文本。

[每当 GridView 重新绑定到其数据源时 ![，将显示选择 "触发事件"。](caching-data-with-the-objectdatasource-vb/_static/image22.png)](caching-data-with-the-objectdatasource-vb/_static/image21.png)

**图 9**：每当 GridView 重新绑定到其数据源时，将显示选择 "触发事件" （[单击查看完全大小的图像](caching-data-with-the-objectdatasource-vb/_static/image23.png)）

[单击回发按钮 ![会导致 GridView 从其视图状态重新构造](caching-data-with-the-objectdatasource-vb/_static/image25.png)](caching-data-with-the-objectdatasource-vb/_static/image24.png)

**图 10**：单击 "回发" 按钮会导致 GridView 从其视图状态重新构造（[单击以查看完全大小的图像](caching-data-with-the-objectdatasource-vb/_static/image26.png)）

每次对数据分页或排序时，检索数据库数据可能会浪费。 毕竟，由于我们使用默认分页，因此在显示第一页时，ObjectDataSource 已经检索了所有记录。 即使 GridView 不提供排序和分页支持，每次用户首次访问页面时，都必须从数据库中检索数据（如果禁用了视图状态，则必须在每次回发时）从数据库中检索数据。 但如果 GridView 向所有用户显示相同的数据，则这些额外的数据库请求是多余的。 为什么不缓存 `GetProducts()` 方法返回的结果，并将 GridView 绑定到这些缓存的结果？

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>步骤4：使用 ObjectDataSource 缓存数据

只需设置几个属性，ObjectDataSource 就可以配置为在 ASP.NET 数据缓存中自动缓存其检索的数据。 以下列表汇总了 ObjectDataSource 的与缓存相关的属性：

- 若要启用缓存， [EnableCaching](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx)必须设置为 `True`。 默认值为 `False`。
- [CacheDuration](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx)缓存数据的时间量（以秒为单位）。 默认值为 0。 如果 `EnableCaching` `True` 并且 `CacheDuration` 设置为大于零的值，则 ObjectDataSource 仅会缓存数据。
- [CacheExpirationPolicy](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx)可以设置为 `Absolute` 或 `Sliding`。 如果 `Absolute`，则 ObjectDataSource 会将检索到的数据缓存 `CacheDuration` 秒;如果 `Sliding`，则只有在 `CacheDuration` 秒内访问数据后，数据才会过期。 默认值为 `Absolute`。
- [CacheKeyDependency](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx)使用此属性将 ObjectDataSource 的缓存条目与现有的缓存依赖项相关联。 可以通过将 ObjectDataSource 数据条目的关联 `CacheKeyDependency`过期，从缓存中将其提前逐出。 此属性最常用于将 SQL 缓存依赖关系与 ObjectDataSource s 缓存相关联，我们将在以后[使用 SQL 缓存依赖项](using-sql-cache-dependencies-vb.md)教程探讨相关主题。

让 s 配置 `ProductsDataSource` ObjectDataSource，以将其数据缓存30秒，使其达到绝对比例。 将 ObjectDataSource s `EnableCaching` 属性设置为 `True`，其 `CacheDuration` 属性设置为30。 将 `CacheExpirationPolicy` 属性设置为其默认值，`Absolute`。

[![将 ObjectDataSource 配置为将其数据缓存30秒](caching-data-with-the-objectdatasource-vb/_static/image28.png)](caching-data-with-the-objectdatasource-vb/_static/image27.png)

**图 11**：将 ObjectDataSource 配置为将其数据缓存30秒（[单击查看完全大小的映像](caching-data-with-the-objectdatasource-vb/_static/image29.png)）

保存更改，并在浏览器中重新访问此页。 首次访问页面时，将显示 "选择事件激发的文本"，因为最初数据不在缓存中。 但是，通过单击回发按钮、排序、分页或单击 "编辑" 或 "取消" 按钮触发的后续回发*不*会重新显示选择 "事件触发文本"。 这是因为仅当 ObjectDataSource 从其基础对象获取其数据时才会触发 `Selecting` 事件;如果从数据缓存中提取数据，则不会激发 `Selecting` 事件。

30秒后，数据将从缓存中逐出。 如果调用 ObjectDataSource `Insert`、`Update`或 `Delete` 方法，则数据也将从缓存中逐出。 因此，超过30秒后，单击 "更新" 按钮、排序、分页或单击 "编辑" 或 "取消" 按钮将导致 ObjectDataSource 从其基础对象获取其数据，并在 `Selecting` 事件激发时显示选择事件引发的文本。 这些返回的结果会被放回到数据缓存中。

> [!NOTE]
> 如果您经常发现选择事件引发的文本，即使您希望 ObjectDataSource 使用缓存的数据，这可能是由于内存限制。 如果没有足够的可用内存，则由 ObjectDataSource 添加到缓存中的数据可能已被清除。 如果 ObjectDataSource 没有正确缓存数据或只是偶尔缓存数据，请关闭一些应用程序以释放内存，然后重试。

图12说明了 ObjectDataSource s 缓存工作流。 当选择 "激发的事件" 文本出现在屏幕上时，是因为数据不在缓存中，必须从基础对象中检索。 但当缺少此文本时，这是因为数据从缓存中可用。 如果从缓存返回数据，则不会调用基础对象，因此不会执行任何数据库查询。

![ObjectDataSource 存储和检索数据缓存中的数据](caching-data-with-the-objectdatasource-vb/_static/image30.png)

**图 12**： ObjectDataSource 存储和检索数据缓存中的数据

每个 ASP.NET 应用程序都有自己的数据缓存实例，该实例在所有页面和访问者之间共享。 这意味着由 ObjectDataSource 存储在数据缓存中的数据同样在访问该页面的所有用户之间共享。 若要验证这一点，请在浏览器中打开 `ObjectDataSource.aspx` 页面。 首次访问页面时，将显示 "选择事件激发的文本" （假设先前测试添加到缓存的数据现在已被逐出）。 打开第二个浏览器实例，将第一个浏览器实例中的 URL 复制并粘贴到第二个实例。 在第二个浏览器实例中，不会显示选择事件激发的文本，因为它使用的是与第一个相同的缓存数据。

将检索到的数据插入缓存中时，ObjectDataSource 使用缓存键值，其中包括： `CacheDuration` 和 `CacheExpirationPolicy` 属性值;由 ObjectDataSource 使用的基础业务对象的类型（通过[`TypeName` 属性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.typename.aspx)（在本示例中为`ProductsBLL`指定）;`SelectMethod` 属性的值和 `SelectParameters` 集合中的参数的名称和值;以及在实现[自定义分页](../paging-and-sorting/paging-and-sorting-report-data-vb.md)时使用的 `StartRowIndex` 和 `MaximumRows` 属性的值。

将缓存键值作为这些属性的组合进行定制可确保在这些值发生变化时唯一的缓存条目。 例如，在过去的教程中，我们已了解如何使用 `ProductsBLL` 类 `GetProductsByCategoryID(categoryID)`，这将返回指定类别的所有产品。 一个用户可能会转到页面并查看饮料，其中 `CategoryID` 为1。 如果 ObjectDataSource 缓存其结果，而不考虑 `SelectParameters` 值，当另一个用户进入页面查看调味品，而饮料产品在缓存中时，他们将看到缓存的饮料产品，而不是调味品。 通过使用这些属性（包括 `SelectParameters`的值）来改变缓存键，ObjectDataSource 为饮料和调味品维护单独的缓存条目。

## <a name="stale-data-concerns"></a>陈旧数据问题

当调用 `Insert`、`Update`或 `Delete` 方法中的任何一个时，ObjectDataSource 会自动从缓存中逐出其项。 这可通过在通过页面修改数据时清除缓存条目来帮助防止陈旧数据。 但是，ObjectDataSource 使用缓存仍可显示过时数据。 在最简单的情况下，这可能是因为数据直接在数据库中发生了变化。 数据库管理员可能仅运行了修改数据库中的某些记录的脚本。

此方案还可以更微妙地展开。 当 ObjectDataSource 在调用其数据修改方法之一时从缓存中逐出其项时，所移除的缓存项将适用于 ObjectDataSource 的属性值（`CacheDuration`、`TypeName`、`SelectMethod`等）的特定组合。 如果有两个使用不同 `SelectMethods` 或 `SelectParameters`的 Objectdatasource，但仍可更新相同的数据，则一个 ObjectDataSource 可以更新行并使其自己的缓存条目失效，但仍将从缓存中为第二个 ObjectDataSource 提供相应的行。 我鼓励您创建页面来展示这一功能。 创建一个页面，该页面显示可编辑的 GridView，该 GridView 从使用缓存的 ObjectDataSource 提取数据，并将其配置为从 `ProductsBLL` 类 `GetProducts()` 方法中获取数据。 将另一个可编辑的 GridView 和 ObjectDataSource 添加到此页（或另一个），但对于此第二个 ObjectDataSource，使用 `GetProductsByCategoryID(categoryID)` 方法。 由于两个 Objectdatasource `SelectMethod` 属性不同，因此每个属性都有其自己的缓存值。 如果在一个网格中编辑某一产品，则下次将数据绑定回另一个网格（通过分页、排序等）时，它仍将为旧的缓存数据提供服务，而不反映从另一个网格进行的更改。

简而言之，只使用基于时间的 expiries，如果你愿意拥有过时数据的可能性，并且在数据的新鲜度非常重要的情况下使用较短的 expiries。 如果陈旧数据是不可接受的，则放弃缓存或使用 SQL 缓存依赖项（假定它是重新缓存的数据库数据）。 在将来的教程中，我们将探索 SQL 缓存依赖关系。

## <a name="summary"></a>摘要

在本教程中，我们将探讨 ObjectDataSource 的内置缓存功能。 只需设置几个属性，就可以指示 ObjectDataSource 将指定 `SelectMethod` 返回的结果缓存到 ASP.NET 数据缓存中。 `CacheDuration` 和 `CacheExpirationPolicy` 属性指示项缓存的持续时间，以及它是绝对过期还是可调过期。 `CacheKeyDependency` 属性将所有 ObjectDataSource s 缓存条目与现有缓存依赖关系关联。 这可用于在达到基于时间的过期之前从缓存中逐出 ObjectDataSource 条目，并且通常用于 SQL 缓存依赖项。

由于 ObjectDataSource 只是将其值缓存到数据缓存中，因此我们可以以编程方式复制 ObjectDataSource 的内置功能。 在表示层执行此操作并无意义，因为 ObjectDataSource 提供现成的功能，但可以在体系结构的一个单独的层中实现缓存功能。 为此，我们需要重复该 ObjectDataSource 使用的相同逻辑。 我们将在下一教程中了解如何以编程方式在体系结构中使用数据缓存。

很高兴编程！

## <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 缓存：技术和最佳做法](https://msdn.microsoft.com/library/aa478965.aspx)
- [.NET Framework 应用程序的缓存体系结构指南](https://msdn.microsoft.com/library/ee817645.aspx)
- [ASP.NET 2.0 中的输出缓存](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](using-sql-cache-dependencies-cs.md)
> [下一页](caching-data-in-the-architecture-vb.md)
