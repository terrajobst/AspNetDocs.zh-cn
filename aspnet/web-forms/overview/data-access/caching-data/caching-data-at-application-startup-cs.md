---
uid: web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
title: 在应用程序启动时缓存C#数据（） |Microsoft Docs
author: rick-anderson
description: 在任何 Web 应用程序中，一些数据会频繁使用，一些数据将不常使用。 我们可以提高 ASP.NET 应用程序的性能。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 22ca8efa-7cd1-45a7-b9ce-ce6eb3b3ff95
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
msc.type: authoredcontent
ms.openlocfilehash: a0b55b0df1b7843120de284891e16178df23fabe
ms.sourcegitcommit: fe5c7512383a9b0a05d321ff10d3cca1611556f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2019
ms.locfileid: "70386611"
---
# <a name="caching-data-at-application-startup-c"></a>在应用程序启动时缓存数据 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](caching-data-at-application-startup-cs/_static/datatutorial60cs1.pdf)

> 在任何 Web 应用程序中，一些数据会频繁使用，一些数据将不常使用。 我们可以预先加载频繁使用的数据（一种称为 "缓存" 的方法），提高 ASP.NET 应用程序的性能。 本教程演示一种主动加载方法，该方法是在应用程序启动时将数据加载到缓存中。

## <a name="introduction"></a>介绍

前面的两个教程介绍了如何在表示层和缓存层中缓存数据。 使用[Objectdatasource 缓存数据](caching-data-with-the-objectdatasource-cs.md)时，我们了解到使用 objectdatasource 的缓存功能来缓存表示层中的数据。 在[体系结构中缓存数据](caching-data-in-the-architecture-cs.md)在新的、单独的缓存层中检查了缓存。 这两个教程使用数据缓存中的 "*被动" 加载*。 对于被动加载，每次请求数据时，系统会先检查它是否在缓存中。 如果不是，则它从原始源中获取数据（如数据库），然后将其存储在缓存中。 被动加载的主要优点在于它的实现。 它的缺点之一是跨请求的性能不均衡。 假设某个页面使用前面教程中的缓存层来显示产品信息。 如果是第一次访问此页面，或由于内存限制或已达到指定的过期时间而逐出缓存数据后首次访问此页面，则必须从数据库中检索数据。 因此，这些用户请求所用的时间超过了可由缓存提供服务的用户请求。

*主动加载*提供备用缓存管理策略，可在需要时通过加载缓存数据来平滑处理请求的性能。 通常情况下，主动加载将使用在已对基础数据进行更新时定期检查或通知的某个进程。 然后，此过程更新缓存以使其保持最新。 如果基础数据来自慢速数据库连接、Web 服务或其他一些特别缓慢的数据源，则主动加载特别有用。 但这种主动加载方法更难实现，因为这种方法需要创建、管理和部署一个过程来检查更改和更新缓存。

主动加载的另一种风格和我们在本教程中要探讨的类型是在应用程序启动时将数据加载到缓存中。 此方法特别适用于缓存静态数据，如数据库查找表中的记录。

> [!NOTE]
> 若要更深入地了解主动和被动加载之间的差异，以及优缺点的优点、缺点和实施建议，请参阅 .NET 缓存体系结构指南中的[管理缓存内容](https://msdn.microsoft.com/library/ms978503.aspx)部分[框架应用程序](https://msdn.microsoft.com/library/ms978498.aspx)。

## <a name="step-1-determining-what-data-to-cache-at-application-startup"></a>步骤 1：确定在应用程序启动时要缓存的数据

使用前两个教程中所述的 "被动" 加载的缓存示例适用于可能会定期更改且不需要 exorbitantly 长时间生成的数据。 但是，如果缓存的数据永远不会发生更改，则被动加载所使用的过期时间将是多余的。 同样，如果要缓存的数据需要很长时间才能生成，则在检索基础数据时，其请求查找缓存为空的用户必须经受较长的等待时间。 请考虑缓存静态数据，以及在应用程序启动时需要很长时间生成的数据。

尽管数据库具有很多动态、频繁变化的值，但大多数情况下也有大量静态数据。 例如，几乎所有数据模型都具有一个或多个列，其中包含一组固定的选项中的特定值。 数据库表可能包含一个`PrimaryLanguage`列，其值集可以是英语、西班牙语、法语、俄语、日语等。 `Patients` 通常，这些类型的列是使用*查找表*实现的。 除了在`Patients`表中存储字符串英语或法语外，还会创建第二个表，其中通常包含两个列：唯一标识符和字符串说明-具有针对每个可能值的记录。 表中的`PrimaryLanguage`列存储查找表中对应的唯一标识符。 `Patients` 在图1中，患者 John Doe 的主要语言是英语，而 Ed Johnson 是俄语。

!["语言" 表是 "患者" 表使用的查找表](caching-data-at-application-startup-cs/_static/image1.png)

**图 1**：该表是`Patients`表使用的查找表`Languages`

用于编辑或创建新患者的用户界面将包含`Languages`表中记录所填充的允许语言的下拉列表。 如果不缓存，则每次访问该接口时，系统都`Languages`必须查询表。 因为查找表值更改很少（如果有），所以这是不必要的。

我们可以使用前面`Languages`教程中所述的相同反应性加载方法来缓存数据。 但是，反应性加载将使用基于时间的过期，这对于静态查找表数据不是必需的。 虽然使用被动加载的缓存比根本不缓存更好，但最好的方法是在应用程序启动时，将查找表数据主动加载到缓存中。

在本教程中，我们将介绍如何缓存查找表数据和其他静态信息。

## <a name="step-2-examining-the-different-ways-to-cache-data"></a>步骤 2：检查缓存数据的不同方式

可以使用多种方法以编程方式在 ASP.NET 应用程序中缓存信息。 我们已在前面的教程中了解到如何使用数据缓存。 或者，可以使用*静态成员*或*应用程序状态*以编程方式缓存对象。

使用类时，通常必须先对类进行实例化，然后才能访问其成员。 例如，若要从我们的业务逻辑层中的某个类调用方法，必须首先创建类的实例：

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample1.cs)]

在可以调用*SomeMethod*或使用*SomeProperty*之前，必须先使用`new`关键字创建类的一个实例。 *SomeMethod*和*SomeProperty*与特定实例关联。 这些成员的生存期与其关联对象的生存期相关联。 另一方面，*静态成员*是在类的*所有*实例之间共享的变量、属性和方法，因此，其生存期与类相同。 静态成员由关键字`static`表示。

除了静态成员以外，还可以使用应用程序状态来缓存数据。 每个 ASP.NET 应用程序都维护一个在应用程序的所有用户和页面之间共享的名称/值集合。 可以使用[ `HttpContext`类](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)的[ `Application`属性](https://msdn.microsoft.com/library/system.web.httpcontext.application.aspx)访问此集合，并使用 ASP.NET 页的代码隐藏类（如下所示）：

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample2.cs)]

数据缓存提供了一种更丰富的 API 用于缓存数据，并提供基于时间和依赖依赖关系的 expiries、缓存项优先级等的机制。 对于静态成员和应用程序状态，页面开发人员必须手动添加此类功能。 但是，在应用程序的生存期内缓存数据时，数据缓存的优点是差异。 在本教程中，我们将介绍使用所有三种方法来缓存静态数据的代码。

## <a name="step-3-caching-thesupplierstable-data"></a>步骤 3：`Suppliers`缓存表数据

我们迄今为止实现的 Northwind 数据库表不包含任何传统的查找表。 在我们的 DAL 中实现的四个数据表都是值是非静态的模型表。 在本教程中，我们只是假设`Suppliers`该表的数据是静态的，而不是花时间将新 DataTable 添加到 DAL，然后将新的类和方法添加到 BLL。 因此，我们可以在应用程序启动时缓存此数据。

首先， `StaticCache.cs` `CL`在文件夹中创建一个名为的新类。

![在 CL 文件夹中创建 StaticCache.cs 类](caching-data-at-application-startup-cs/_static/image2.png)

**图 2**：在文件夹中创建类`StaticCache.cs` `CL`

我们需要添加一个方法，用于在启动时将数据加载到相应的缓存存储中，以及从该缓存返回数据的方法。

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample3.cs)]

上面的代码使用静态`suppliers`成员变量来保存从`LoadStaticCache()`方法调用的`SuppliersBLL`类的`GetSuppliers()`方法中的结果。 `LoadStaticCache()`方法旨在在应用程序启动过程中调用。 在应用程序启动时加载此数据后，需要使用供应商数据的任何页都可以调用`StaticCache`类的`GetSuppliers()`方法。 因此，在应用程序启动时，对数据库的调用只会出现一次。

我们可以使用或使用应用程序状态或数据缓存，而不是使用静态成员变量作为缓存存储区。 下面的代码演示重组的类以使用应用程序状态：

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample4.cs)]

在`LoadStaticCache()`中，将供应商信息存储到应用程序变量*键*。 它从中`GetSuppliers()`返回为适当的类型`Northwind.SuppliersDataTable`（）。 尽管可以使用`Application["key"]`在 ASP.NET 页面的代码隐藏类中访问应用程序状态，但在体系结构中，我们`HttpContext.Current.Application["key"]`必须使用才能获得最新`HttpContext`的。

同样，可以将数据缓存用作缓存存储，如以下代码所示：

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample5.cs)]

若要将项添加到数据缓存，但不使用基于时间的过期时间`System.Web.Caching.Cache.NoAbsoluteExpiration` ， `System.Web.Caching.Cache.NoSlidingExpiration`请使用和值作为输入参数。 选择了数据缓存`Insert`方法的此特定重载，以便可以指定缓存项的*优先级*。 当可用内存不足时，该优先级用于确定要从缓存中清除哪些项。 此处我们使用优先级`NotRemovable`，这可确保不会清理此缓存项。

> [!NOTE]
> 本教程的下载将使用`StaticCache`静态成员变量方法实现类。 类文件的注释中提供了应用程序状态和数据缓存技术的代码。

## <a name="step-4-executing-code-at-application-startup"></a>步骤 4：在应用程序启动时执行代码

若要在 web 应用程序首次启动时执行代码，我们需要创建一个名`Global.asax`为的特殊文件。 此文件可以包含应用程序、会话和请求级事件的事件处理程序，并且可以在此处添加应用程序每次启动时执行的代码。

在 Visual `Global.asax` Studio 的 "解决方案资源管理器中右键单击网站项目名称，然后选择" 添加新项 "，将该文件添加到 web 应用程序的根目录中。 从 "添加新项" 对话框中，选择 "全局应用程序类" 项类型，然后单击 "添加" 按钮。

> [!NOTE]
> 如果项目中已经有`Global.asax`一个文件，则 "添加新项" 对话框中将不会列出 "全局应用程序类" 项类型。

[![将 global.asax 文件添加到 Web 应用程序的根目录](caching-data-at-application-startup-cs/_static/image4.png)](caching-data-at-application-startup-cs/_static/image3.png)

**图 3**：将文件添加到 Web 应用程序的根目录（[单击以查看完全大小的映像）](caching-data-at-application-startup-cs/_static/image5.png) `Global.asax`

默认`Global.asax`文件模板在服务器端`<script>`标记中包含五个方法：

- **`Application_Start`** 当 web 应用程序首次启动时执行
- **`Application_End`** 在应用程序关闭时运行
- **`Application_Error`** 每当未处理的异常到达应用程序时执行
- **`Session_Start`** 创建新会话时执行
- **`Session_End`** 当会话过期或弃用时运行

在应用程序的生命周期内，只调用一次事件处理程序。`Application_Start` 第一次从应用程序请求 ASP.NET 资源时，应用程序将继续运行，直到重新启动该应用程序，这可以通过修改`/Bin`文件夹的内容、修改`Global.asax`、修改文件夹中的`App_Code`内容，或`Web.config`修改文件，等等。 有关应用程序生命周期的详细讨论，请参阅[ASP.NET 应用程序生命周期概述](https://msdn.microsoft.com/library/ms178473.aspx)。

对于这些教程，我们只需向`Application_Start`方法中添加代码，因此可随意删除其他代码。 在`Application_Start`中，只需`StaticCache`调用类`LoadStaticCache()`的方法，它将加载并缓存供应商信息：

[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample6.aspx)]

就这么简单！ 在应用程序启动时`LoadStaticCache()` ，方法将从 BLL 中获取供应商信息，并将其存储在静态成员变量中（或在类中使用结束的`StaticCache`任何缓存存储）。 若要验证此行为，请在`Application_Start`方法中设置断点并运行应用程序。 请注意，将在应用程序启动时命中该断点。 但后续请求不会导致执行此`Application_Start`方法。

[![使用断点验证是否正在执行 Application_Start 事件处理程序](caching-data-at-application-startup-cs/_static/image7.png)](caching-data-at-application-startup-cs/_static/image6.png)

**图 4**：使用断点验证`Application_Start`是否正在执行事件处理程序（[单击查看完全大小的映像](caching-data-at-application-startup-cs/_static/image8.png)）

> [!NOTE]
> 如果在首次启动调试`Application_Start`时未命中断点，则是因为应用程序已启动。 通过修改`Global.asax`或`Web.config`文件来强制应用程序重启，然后重试。 您可以在其中一个文件的末尾添加（或删除）空白行，以快速重新启动该应用程序。

## <a name="step-5-displaying-the-cached-data"></a>步骤 5：显示缓存的数据

此时， `StaticCache`类具有在应用程序启动时缓存的供应商数据版本，可通过其`GetSuppliers()`方法进行访问。 若要在表示层处理此`StaticCache`类数据，可以使用 ObjectDataSource 或以编程方式从 ASP.NET 页的代码隐藏类中调用类的`GetSuppliers()`方法。 让我们看一下如何使用 ObjectDataSource 和 GridView 控件显示缓存的供应商信息。

首先打开`Caching`文件夹中`AtApplicationStartup.aspx`的页面。 将 GridView 从工具箱拖到设计器上，并将`ID`其属性`Suppliers`设置为。 接下来，在 GridView 的智能标记中，选择创建名为`SuppliersCachedDataSource`的新 ObjectDataSource。 将 ObjectDataSource 配置为使用`StaticCache`类的`GetSuppliers()`方法。

[![将 ObjectDataSource 配置为使用 StaticCache 类](caching-data-at-application-startup-cs/_static/image10.png)](caching-data-at-application-startup-cs/_static/image9.png)

**图 5**：将 ObjectDataSource 配置为使用`StaticCache`类（[单击以查看完全大小的映像](caching-data-at-application-startup-cs/_static/image11.png)）

[![使用 GetSuppliers （）方法检索缓存的供应商数据](caching-data-at-application-startup-cs/_static/image13.png)](caching-data-at-application-startup-cs/_static/image12.png)

**图 6**：使用方法检索缓存的供应商数据（[单击以查看完全大小的图像）](caching-data-at-application-startup-cs/_static/image14.png) `GetSuppliers()`

完成向导后，Visual Studio 将为中`SuppliersDataTable`的每个数据字段自动添加 BoundFields。 GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample7.aspx)]

图7显示了通过浏览器查看的页面。 从 BLL 的`SuppliersBLL`类中提取数据时，输出是相同的，但`StaticCache`使用类会在应用程序启动时返回缓存的供应商数据。 可以在`StaticCache`类的`GetSuppliers()`方法中设置断点来验证此行为。

[![已缓存的供应商数据显示在 GridView 中](caching-data-at-application-startup-cs/_static/image16.png)](caching-data-at-application-startup-cs/_static/image15.png)

**图 7**：缓存的供应商数据显示在 GridView 中（[单击以查看完全大小的图像](caching-data-at-application-startup-cs/_static/image17.png)）

## <a name="summary"></a>总结

大多数数据模型都包含大量静态数据，通常以查找表的形式实现。 由于此信息是静态的，因此在每次需要显示此信息时，无需持续访问数据库。 而且，在缓存数据时，由于其静态性质，无需过期。 在本教程中，我们介绍了如何使用此类数据并将其缓存到数据缓存、应用程序状态和静态成员变量中。 此信息在应用程序启动时缓存，并在应用程序的整个生存期内保留在缓存中。

在本教程和过去的两个教程中，我们已在应用程序的生存期和使用基于时间的 expiries 的持续时间内查看缓存数据。 但是，在缓存数据库数据时，基于时间的到期时间可能会低于理想的时间。 不会定期刷新缓存，只是在修改基础数据库数据时才会逐出缓存的项。 使用 SQL 缓存依赖项可以实现此理想选择，我们将在下一教程中对此进行介绍。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以到达[ mitchell@4GuysFromRolla.com。](mailto:mitchell@4GuysFromRolla.com) 或者，通过他的博客，可以找到[http://ScottOnWriting.NET](http://ScottOnWriting.NET)。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的领导评审者是 Teresa Murphy 和 Zack。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[ mitchell@4GuysFromRolla.com中放置一行。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](caching-data-in-the-architecture-cs.md)
> [下一页](using-sql-cache-dependencies-cs.md)
