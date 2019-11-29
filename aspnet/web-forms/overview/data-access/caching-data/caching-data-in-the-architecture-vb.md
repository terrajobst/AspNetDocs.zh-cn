---
uid: web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-vb
title: 缓存体系结构中的数据（VB） |Microsoft Docs
author: rick-anderson
description: 在上一教程中，我们学习了如何在表示层应用缓存。 在本教程中，我们将了解如何利用我们的分层 architectu 。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 5e189dd7-f4f9-4f28-9b3a-6cb7d392e9c7
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-vb
msc.type: authoredcontent
ms.openlocfilehash: dc991a205fa7e61f604bc0f26e9b24b3faefd3d3
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607503"
---
# <a name="caching-data-in-the-architecture-vb"></a>缓存体系结构中的数据 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载示例应用](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_59_VB.exe)或[下载 PDF](caching-data-in-the-architecture-vb/_static/datatutorial59vb1.pdf)

> 在上一教程中，我们学习了如何在表示层应用缓存。 在本教程中，我们将了解如何利用我们的分层体系结构来缓存业务逻辑层中的数据。 为此，我们要扩展体系结构，使其包含缓存层。

## <a name="introduction"></a>简介

如前面的教程中所述，缓存 ObjectDataSource 数据就像设置几个属性一样简单。 遗憾的是，ObjectDataSource 在表示层应用缓存，这会在 ASP.NET 页中将缓存策略紧密耦合在一起。 创建分层体系结构的原因之一是允许此类放开中断。 例如，业务逻辑层用于将业务逻辑与 ASP.NET 页面分离，而数据访问层则使数据访问详细信息分离。 这会使业务逻辑和数据访问详细信息的这种分离成为一种更好的方法，因为它使系统更具可读性，更易于维护，并且更灵活地进行更改。 它还允许对使用表示层的开发人员进行域知识和部门划分，无需熟悉数据库的详细信息，就能完成工作。 将缓存策略与表示层分离会提供类似的好处。

在本教程中，我们将补充体系结构，使之包含使用缓存策略的*缓存层*（或 CL）。 该缓存层将包括一个 `ProductsCL` 类，该类通过 `GetProducts()`、`GetProductsByCategoryID(categoryID)`等方法提供对产品信息的访问。在调用时，将首先尝试从缓存中检索数据。 如果缓存为空，这些方法将在 BLL 中调用相应的 `ProductsBLL` 方法，进而从 DAL 获取数据。 `ProductsCL` 方法缓存从 BLL 检索的数据，然后再将其返回。

如图1所示，CL 驻留在表示层和业务逻辑层之间。

![缓存层（CL）是体系结构中的另一层](caching-data-in-the-architecture-vb/_static/image1.png)

**图 1**：缓存层（CL）是体系结构中的另一层

## <a name="step-1-creating-the-caching-layer-classes"></a>步骤1：创建缓存层类

在本教程中，我们将创建一个非常简单的 CL，其中包含只有少量方法的单个类 `ProductsCL`。 为整个应用程序构建完整的缓存层需要创建 `CategoriesCL`、`EmployeesCL`和 `SuppliersCL` 类，并为 BLL 中的每个数据访问或修改方法提供这些缓存层类中的方法。 与 BLL 和 DAL 一样，应理想地将缓存层实现为单独的类库项目;但是，我们会将其实现为 `App_Code` 文件夹中的类。

若要更清晰地将 DAL 类与 DAL 和 BLL 类分开，请在 `App_Code` 文件夹中创建一个新的子文件夹。 右键单击解决方案资源管理器中的 "`App_Code`" 文件夹，选择 "新建文件夹"，然后将新文件夹命名为 "`CL`"。 创建此文件夹后，将添加到名为 `ProductsCL.vb`的新类中。

![添加一个名为 CL 的新文件夹和一个名为 ProductsCL 的类](caching-data-in-the-architecture-vb/_static/image2.png)

**图 2**：添加名为 `CL` 的新文件夹和名为 `ProductsCL.vb` 的类

`ProductsCL` 类应包含一组相同的数据访问和修改方法，如在其相应的业务逻辑层类（`ProductsBLL`）中找到。 只需创建这两种方法，就可以在这里构建一些方法，让你了解 CL 所使用的模式。 具体而言，我们将在步骤3中添加 `GetProducts()` 和 `GetProductsByCategoryID(categoryID)` 方法，在步骤4中添加 `UpdateProduct` 重载。 您可以在休闲中添加剩余的 `ProductsCL` 方法和 `CategoriesCL`、`EmployeesCL`和 `SuppliersCL` 类。

## <a name="step-2-reading-and-writing-to-the-data-cache"></a>步骤2：读取和写入数据缓存

前面的教程中所述的 ObjectDataSource 缓存功能在内部使用 ASP.NET 数据缓存来存储从 BLL 检索的数据。 还可以从 ASP.NET 页的代码隐藏类或 web 应用程序体系结构中的类以编程方式访问数据缓存。 若要从 ASP.NET 页的代码隐藏类读取和写入数据缓存，请使用以下模式：

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample1.vb)]

[`Cache` 类](https://msdn.microsoft.com/library/system.web.caching.cache.aspx) [`Insert` 方法](https://msdn.microsoft.com/library/system.web.caching.cache.insert.aspx)具有多个重载。 `Cache("key") = value` 和 `Cache.Insert(key, value)` 是同义词，这两种方法都使用指定的密钥将项添加到缓存，而不定义到期。 通常，我们希望在将项添加到缓存时指定到期时间，无论是依赖项、基于时间的过期，还是同时指定两者。 使用另一个 `Insert` 方法的重载来提供依赖项或基于时间的过期信息。

缓存层的方法首先需要检查请求的数据是否在缓存中，如果是，则从那里返回数据。 如果请求的数据不在缓存中，则需要调用相应的 BLL 方法。 应缓存并返回其返回值，如下图所示。

![缓存层 s 方法返回缓存中的数据（如果可用）](caching-data-in-the-architecture-vb/_static/image3.png)

**图 3**：缓存层 s 方法返回缓存中的数据（如果可用）

图3中所示的序列是使用以下模式在 CL 类中完成的：

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample2.vb)]

此处， *type*是在缓存 `Northwind.ProductsDataTable`中存储的数据的类型，例如， *key*是唯一标识缓存项的键。 如果缓存中不存在具有指定*键*的项，则将 `Nothing`*实例*，并将从适当的 BLL 方法检索数据并将其添加到缓存中。 达到 `Return instance` 时，*实例*将包含对数据的引用，无论是从缓存中提取，还是从 BLL 拉取。

访问缓存中的数据时，请务必使用以上模式。 以下模式（乍一看）看上去等效，包含引入争用条件的细微差异。 争用条件很难调试，因为它们偶尔显示，难以重现。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample3.vb)]

这一秒的不同之处在于，代码片段不正确，而不是在本地变量中存储对缓存项的引用，而是在条件语句*和*`Return`中直接访问数据缓存。 假设在达到此代码时，不 `Nothing``Cache("key")`，但在到达 `Return` 语句之前，将从缓存中逐出系统的*键*。 在这种罕见情况下，代码将返回 `Nothing` 而不是预期类型的对象。

> [!NOTE]
> 数据缓存是线程安全的，因此您无需为简单读取或写入操作同步线程访问。 但是，如果需要对缓存中需要为原子的数据执行多个操作，则需要负责实现锁定或某些其他机制以确保线程安全。 有关详细信息，请参阅[同步访问 ASP.NET 缓存](http://www.ddj.com/184406369)。

可以使用如下所示的[`Remove` 方法](https://msdn.microsoft.com/library/system.web.caching.cache.remove.aspx)，以编程方式从数据缓存中收回项：

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample4.vb)]

## <a name="step-3-returning-product-information-from-theproductsclclass"></a>步骤3：返回`ProductsCL`类中的产品信息

在本教程中，我们将实现两种方法，用于从 `ProductsCL` 类返回产品信息： `GetProducts()` 和 `GetProductsByCategoryID(categoryID)`。 与业务逻辑层中的 `ProductsBL` 类一样，CL 中的 `GetProducts()` 方法会将所有产品的相关信息作为 `Northwind.ProductsDataTable` 对象返回，同时 `GetProductsByCategoryID(categoryID)` 返回指定类别中的所有产品。

下面的代码演示了 `ProductsCL` 类中的部分方法：

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample5.vb)]

首先，请注意应用于类和方法的 `DataObject` 和 `DataObjectMethodAttribute` 特性。 这些属性向 ObjectDataSource 向导提供信息，指示应在向导步骤中显示的类和方法。 由于将从表示层中的 ObjectDataSource 访问 CL 类和方法，因此我添加了这些属性来增强设计时体验。 有关这些属性及其影响的更全面说明，请参阅 "[创建业务逻辑层](../introduction/creating-a-business-logic-layer-vb.md)" 教程。

在 `GetProducts()` 和 `GetProductsByCategoryID(categoryID)` 方法中，从 `GetCacheItem(key)` 方法返回的数据将被分配给本地变量。 `GetCacheItem(key)` 方法，我们稍后将对此进行检查，根据指定的*键*返回缓存中的特定项。 如果在缓存中找不到此类数据，则从相应的 `ProductsBLL` 类方法检索该数据，然后使用 `AddCacheItem(key, value)` 方法将其添加到缓存中。

`GetCacheItem(key)` 和 `AddCacheItem(key, value)` 方法分别为数据缓存、读取和写入值。 `GetCacheItem(key)` 方法是这二者中较简单的方法。 它只使用传入的*密钥*从缓存类返回值：

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample6.vb)]

`GetCacheItem(key)` 不使用提供的*键值*，而是调用 `GetCacheKey(key)` 方法，该方法将返回前面带有 ProductsCache 的*键*。 `AddCacheItem(key, value)` 方法还使用保存 ProductsCache 字符串的 `MasterCacheKeyArray`，如下所示。

在 ASP.NET 页的代码隐藏类中，可以使用 `Page` 类[`Cache` 属性](https://msdn.microsoft.com/library/system.web.ui.page.cache.aspx)访问数据缓存，并允许使用类似于 `Cache("key") = value`的语法，如步骤2中所述。 从体系结构内的类，可以使用 `HttpRuntime.Cache` 或 `HttpContext.Current.Cache`访问数据缓存。 [Peter Johnson](https://weblogs.asp.net/pjohnson/default.aspx)的博客文章[HttpRuntime 和 httpcontext.current](https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache)说明了使用 `HttpRuntime` 而不是 `HttpContext.Current`时的轻微性能优势。因此，`ProductsCL` 使用 `HttpRuntime`。

> [!NOTE]
> 如果使用类库项目来实现您的体系结构，则需要添加对 `System.Web` 程序集的引用，以便使用[`HttpRuntime`](https://msdn.microsoft.com/library/system.web.httpruntime.aspx)和[`HttpContext`](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)类。

如果在缓存中找不到该项，`ProductsCL` 类的方法将从 BLL 获取数据，并使用 `AddCacheItem(key, value)` 方法将其添加到缓存中。 若要将*值*添加到缓存，可以使用以下代码，该代码使用60秒的过期时间：

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample7.vb)]

`DateTime.Now.AddSeconds(CacheDuration)` 在将来指定基于时间的过期60秒， [`System.Web.Caching.Cache.NoSlidingExpiration`](https://msdn.microsoft.com/library/system.web.caching.cache.noslidingexpiration(vs.80).aspx)指示没有可调过期时间。 尽管这 `Insert` 方法重载都具有输入参数用于绝对和可调过期，但你只能提供两个参数中的一个。 如果尝试同时指定绝对时间和时间跨度，`Insert` 方法将引发 `ArgumentException` 异常。

> [!NOTE]
> `AddCacheItem(key, value)` 方法的这一实现当前有一些缺点。 我们将在步骤4中解决并解决这些问题。

## <a name="step-4-invalidating-the-cache-when-the-data-is-modified-through-the-architecture"></a>步骤4：通过体系结构修改数据时使缓存无效

除了数据检索方法，缓存层还需要提供与 BLL 相同的方法用于插入、更新和删除数据。 CL s 数据修改方法不会修改缓存的数据，而是调用与 BLL s 对应的数据修改方法，然后使缓存无效。 如前面的教程中所示，此行为与在启用缓存功能并调用其 `Insert`、`Update`或 `Delete` 方法时，ObjectDataSource 应用的行为相同。

下面的 `UpdateProduct` 重载说明了如何在 CL 中实现数据修改方法：

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample8.vb)]

将调用相应的数据修改业务逻辑层方法，但在返回其响应之前，需要使缓存无效。 遗憾的是，将缓存无效，这并不是很简单，因为 `ProductsCL` 类 `GetProducts()` 和 `GetProductsByCategoryID(categoryID)` 方法都将项添加到具有不同键的缓存，而 `GetProductsByCategoryID(categoryID)` 方法为每个唯一的*类别 id*添加了不同的缓存项。

在使缓存失效时，我们需要删除 `ProductsCL` 类可能已添加的*所有*项。 这可以通过将*缓存依赖*项与添加到 `AddCacheItem(key, value)` 方法中的缓存的每一项进行关联来实现。 通常，缓存依赖关系可以是缓存中的另一项、文件系统中的文件或 Microsoft SQL Server 数据库中的数据。 如果依赖项发生更改或已从缓存中删除，则与之关联的缓存项将自动从缓存中逐出。 对于本教程，我们想要在缓存中创建一个附加项，以用作通过 `ProductsCL` 类添加的所有项的缓存依赖项。 这样一来，只需删除缓存依赖项，就可以从缓存中删除所有这些项。

让我们更新 `AddCacheItem(key, value)` 方法，以便通过此方法添加到缓存中的每一项都与单个缓存依赖项相关联：

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample9.vb)]

`MasterCacheKeyArray` 是保存单个值 ProductsCache 的字符串数组。 首先，将缓存项添加到缓存，并为其分配当前日期和时间。 如果缓存项已存在，则更新该缓存项。 接下来，创建缓存依赖项。 [`CacheDependency` 类](https://msdn.microsoft.com/library/system.web.caching.cachedependency(VS.80).aspx)的构造函数有多个重载，但此处使用的不需要两个 `String` 数组输入。 第一个指定要用作依赖项的文件集。 由于我们不想使用任何基于文件的依赖项，因此会将 `Nothing` 的值用于第一个输入参数。 第二个输入参数指定用作依赖项的缓存键集。 这里，我们指定了单个依赖项，`MasterCacheKeyArray`。 然后，将 `CacheDependency` 传递到 `Insert` 方法中。

对 `AddCacheItem(key, value)`进行此修改后，invaliding 缓存就像删除依赖项一样简单。

[!code-vb[Main](caching-data-in-the-architecture-vb/samples/sample10.vb)]

## <a name="step-5-calling-the-caching-layer-from-the-presentation-layer"></a>步骤5：从表示层调用缓存层

缓存层的类和方法可用于使用我们在这些教程中所检查的技术来处理数据。 若要演示如何使用缓存数据，请将所做的更改保存到 `ProductsCL` 类，然后在 `Caching` 文件夹中打开 `FromTheArchitecture.aspx` 页，并添加 GridView。 从 GridView s 智能标记创建新的 ObjectDataSource。 在向导的第一步中，你应看到 `ProductsCL` 类作为下拉列表中的选项之一。

["业务对象" 下拉列表中包含 ProductsCL 类 ![](caching-data-in-the-architecture-vb/_static/image5.png)](caching-data-in-the-architecture-vb/_static/image4.png)

**图 4**： "业务对象" 下拉列表中包含了 `ProductsCL` 类（[单击以查看完全大小的图像](caching-data-in-the-architecture-vb/_static/image6.png)）

选择 `ProductsCL`后，单击 "下一步"。 "选择" 选项卡中的下拉列表具有两个项-`GetProducts()` "和" `GetProductsByCategoryID(categoryID)` "，" 更新 "选项卡具有唯一的 `UpdateProduct` 重载。 从 "更新" 选项卡中选择 "`GetProducts()` 方法"，`UpdateProducts` 然后单击 "完成"。

[下拉列表中列出了 ProductsCL 类的方法 ![](caching-data-in-the-architecture-vb/_static/image8.png)](caching-data-in-the-architecture-vb/_static/image7.png)

**图 5**：下拉列表中列出了 `ProductsCL` 类的方法（[单击查看完全大小的图像](caching-data-in-the-architecture-vb/_static/image9.png)）

完成向导后，Visual Studio 会将 "ObjectDataSource s" `OldValuesParameterFormatString` 属性设置为 "`original_{0}` 并将相应的字段添加到 GridView。 将 `OldValuesParameterFormatString` 属性改回其默认值 `{0}`，并配置 GridView 以支持分页、排序和编辑。 由于 CL 使用的 `UploadProducts` 重载只接受经过编辑的产品的名称和价格，因此限制 GridView，使只有这些字段可以编辑。

在前面的教程中，我们定义了一个 GridView，其中包含 `ProductName`、`CategoryName`和 `UnitPrice` 字段的字段。 可以随意复制此格式设置和结构，在这种情况下，GridView 和 ObjectDataSource 的声明性标记应如下所示：

[!code-aspx[Main](caching-data-in-the-architecture-vb/samples/sample11.aspx)]

此时，我们有一个使用缓存层的页面。 若要查看缓存的运行情况，请在 `ProductsCL` 类 `GetProducts()` 和 `UpdateProduct` 方法中设置断点。 访问浏览器中的页面，并在排序和分页时单步执行代码，以便查看从缓存中提取的数据。 然后更新记录，并注意缓存已失效，因此，在将数据重新绑定到 GridView 时，将从 BLL 中检索该记录。

> [!NOTE]
> 本文随附的下载内容中提供的缓存层不完整。 它只包含一个类，`ProductsCL`，仅体育几个方法。 而且，只有单个 ASP.NET 页面使用 CL （`~/Caching/FromTheArchitecture.aspx`），所有其他页面仍直接引用 BLL。 如果你计划在应用程序中使用 CL，则表示层中的所有调用都应转向 CL，这将要求 CL 的类和方法涵盖表示层当前使用的 BLL 中的这些类和方法。

## <a name="summary"></a>总结

尽管可以使用 ASP.NET 2.0 s SqlDataSource 和 ObjectDataSource 控件在表示层应用缓存，但理想情况下，会将缓存责任委托给体系结构中的一个单独的层。 在本教程中，我们创建了一个驻留在表示层和业务逻辑层之间的缓存层。 缓存层需要提供相同的类和方法集，它们存在于 BLL 中，并从表示层中调用。

本教程介绍了此示例中的缓存层示例，并介绍了如何进行*被动加载*。 使用被动加载时，仅当对数据进行请求并且缓存中缺少数据时，才会将数据加载到缓存中。 还可以将数据*主动加载*到缓存中，这种方法在实际需要数据之前将数据加载到缓存中。 在下一教程中，我们将在查看如何在应用程序启动时将静态值存储到缓存中时，将看到一个主动加载的示例。

很高兴编程！

## <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)，已在使用 Microsoft Web 技术，自1998开始。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以[mitchell@4GuysFromRolla.com访问。](mailto:mitchell@4GuysFromRolla.com) 或通过他的博客，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在mitchell@4GuysFromRolla.com放置一行[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](caching-data-with-the-objectdatasource-vb.md)
> [下一页](caching-data-at-application-startup-vb.md)
