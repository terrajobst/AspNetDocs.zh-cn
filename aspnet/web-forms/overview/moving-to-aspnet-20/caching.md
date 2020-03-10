---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: 缓存 |Microsoft Docs
author: microsoft
description: 了解缓存对于执行良好的 ASP.NET 应用程序非常重要。 ASP.NET 1.x 为缓存提供了三种不同的选项;输出缓存,。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: 4f0b021ca6ca151544dd9fb0587ed9e0cf14ff65
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464954"
---
# <a name="caching"></a>缓存

由[Microsoft](https://github.com/microsoft)

> 了解缓存对于执行良好的 ASP.NET 应用程序非常重要。 ASP.NET 1.x 为缓存提供了三种不同的选项;输出缓存、片断缓存和缓存 API。

了解缓存对于执行良好的 ASP.NET 应用程序非常重要。 ASP.NET 1.x 为缓存提供了三种不同的选项;输出缓存、片断缓存和缓存 API。 ASP.NET 2.0 提供了所有这三种方法，但它添加了一些重要的附加功能。 有几个新的缓存依赖项，开发人员现在还可以选择创建自定义缓存依赖项。 ASP.NET 2.0 中还大幅改进了缓存配置。

## <a name="new-features"></a>新增功能

## <a name="cache-profiles"></a>缓存配置文件

缓存配置文件允许开发人员定义可应用于各个页面的特定缓存设置。 例如，如果您的某些页面在12小时后应从缓存中过期，则可以轻松地创建可以应用于这些页面的缓存配置文件。 若要添加新的缓存配置文件，请使用配置文件中的 &lt;outputCacheSettings&gt; 部分。 例如，以下是名为*twoday*的缓存配置文件的配置，它将缓存持续时间配置为12小时。

[!code-xml[Main](caching/samples/sample1.xml)]

若要将此缓存配置文件应用于特定页面，请使用 @ OutputCache 指令的 CacheProfile 属性，如下所示：

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>自定义缓存依赖项

ASP.NET 1.x 开发人员 cried 自定义缓存依赖项。 在 ASP.NET 1.x 中，CacheDependency 类是密封的，阻止开发人员从中派生自己的类。 在 ASP.NET 2.0 中，将删除该限制，开发人员可自由开发自己的自定义缓存依赖项。 CacheDependency 类允许基于文件、目录或缓存键创建自定义缓存依赖项。

例如，下面的代码基于位于 Web 应用程序根目录中的名为 .xml 的文件创建新的自定义缓存依赖项：

[!code-csharp[Main](caching/samples/sample3.cs)]

在这种情况下，当内容 .xml 文件更改时，缓存的项将失效。

还可以使用缓存键创建自定义缓存依赖项。 使用此方法时，删除缓存密钥会使缓存的数据无效。 下面的示例阐释了这一点：

[!code-csharp[Main](caching/samples/sample4.cs)]

若要使上面插入的项无效，只需删除已插入缓存的项作为缓存键即可。

[!code-csharp[Main](caching/samples/sample5.cs)]

请注意，用作缓存键的项的键必须与添加到缓存键数组中的值相同。

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>基于轮询的 SQL 缓存依赖项（也称为基于表的依赖项）

SQL Server 7 和2000为 SQL 缓存依赖项使用基于轮询的模型。 基于轮询的模型对表中的数据发生更改时触发的数据库表使用触发器。 该触发器更新 ASP.NET 定期检查的通知表中的**changeId**字段。 如果**changeId**字段已更新，则 ASP.NET 知道数据已更改，并使缓存的数据无效。

> [!NOTE]
> SQL Server 2005 还可以使用基于轮询的模型，但由于基于轮询的模型不是最有效的模型，因此最好使用 SQL Server 2005 的基于查询的模型（稍后讨论）。

为了使使用基于轮询的模型的 SQL 缓存依赖关系正常工作，这些表必须启用了通知。 这可以使用 SqlCacheDependencyAdmin 类以编程方式完成，也可以通过使用 aspnet\_regsql 实用程序来完成。

以下命令行将在名为*dbase*的 SQL Server 实例上，为 SQL 缓存依赖项注册 Northwind 数据库中的 Products 表。

[!code-console[Main](caching/samples/sample6.cmd)]

下面是上述命令中使用的命令行开关的说明：

| **命令行开关** | **目的** |
| --- | --- |
| -S *server* | 指定服务器名称。 |
| -ed | 指定应为 SQL 缓存依赖项启用数据库。 |
| -d*数据库\_名称* | 指定应为 SQL 缓存依赖项启用的数据库名称。 |
| -E | 指定在连接到数据库时，aspnet\_regsql 应使用 Windows 身份验证。 |
| -et | 指定为 SQL 缓存依赖项启用数据库表。 |
| -t*表\_名称* | 指定要为 SQL 缓存依赖项启用的数据库表的名称。 |

> [!NOTE]
> 还有其他交换机可用于 aspnet\_regsql。 有关完整列表，请运行 aspnet\_regsql-？ 从命令行。

当此命令运行时，将对 SQL Server 数据库进行以下更改：

- 添加了**AspNet\_SqlCacheTablesForChangeNotification**表。 对于数据库中启用了 SQL 缓存依赖关系的每个表，此表包含一行。
- 在数据库中创建以下存储过程：

| AspNet\_SqlCachePollingStoredProcedure | 查询 AspNet\_SqlCacheTablesForChangeNotification 表，并返回为 SQL 缓存依赖关系启用的所有表以及每个表的 changeId 值。 此存储过程用于轮询以确定数据是否已更改。 |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | 通过查询 AspNet\_SqlCacheTablesForChangeNotification 表并返回为 SQL 缓存依赖项启用的所有表，返回为 SQL 缓存依赖项启用的所有表。 |
| AspNet\_SqlCacheRegisterTableStoredProcedure | 通过在通知表中添加所需的项并添加触发器，为 SQL 缓存依赖项注册表。 |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | 通过删除通知表中的条目并删除触发器，为 SQL 缓存依赖关系注销表。 |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | 通过递增已更改表的 changeId 更新通知表。 ASP.NET 使用此值来确定数据是否已更改。 如下所示，此存储过程由启用表时所创建的触发器执行。 |

- 为表创建一个名为 **_table\_name_\_SQL Server 触发器\_SqlCacheNotification\_触发器**。 当对表执行 INSERT、UPDATE 或 DELETE 时，此触发器将执行 AspNet\_SqlCacheUpdateChangeIdStoredProcedure。
- 名为**aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess**的 SQL Server 角色将添加到数据库中。

**Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server Role 对 Aspnet\_SQLCACHEPOLLINGSTOREDPROCEDURE 具有 EXEC 权限。 为了使轮询模式正常工作，必须将进程帐户添加到 aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess 角色。 Aspnet\_regsql 工具不会为你执行此操作。

### <a name="configuring-polling-based-sql-cache-dependencies"></a>配置基于轮询的 SQL 缓存依赖关系

配置基于轮询的 SQL 缓存依赖项需要几个步骤。 第一步是启用数据库和表（如上文所述）。 完成该步骤后，配置的其余部分如下所示：

- 配置 ASP.NET 配置文件。
- 配置 SqlCacheDependency

### <a name="configuring-the-aspnet-configuration-file"></a>配置 ASP.NET 配置文件

除了添加之前模块中讨论的连接字符串外，还必须使用 &lt;sqlCacheDependency&gt; 元素配置 &lt;缓存&gt; 元素，如下所示：

[!code-xml[Main](caching/samples/sample7.xml)]

此配置启用对*pubs*数据库的 SQL 缓存依赖关系。 请注意，&lt;sqlCacheDependency&gt; 元素中的 pollTime 属性的默认值为60000毫秒或1分钟。 （此值不能小于500毫秒。）在此示例中，&lt;add&gt; 元素添加一个新的数据库并重写 pollTime，并将其设置为9000000毫秒。

#### <a name="configuring-the-sqlcachedependency"></a>配置 SqlCacheDependency

下一步是配置 SqlCacheDependency。 完成此操作的最简单方法是在 @ Outcache 指令中指定 SqlDependency 特性的值，如下所示：

[!code-aspx[Main](caching/samples/sample8.aspx)]

在上述 @ OutputCache 指令中，为*pubs*数据库中的*authors*表配置了 SQL 缓存依赖关系。 可以通过用分号分隔多个依赖项来配置这些依赖项，如下所示：

[!code-aspx[Main](caching/samples/sample9.aspx)]

配置 SqlCacheDependency 的另一种方法是以编程方式执行此操作。 下面的代码在*pubs*数据库的*authors*表中创建新的 SQL 缓存依赖项。

[!code-csharp[Main](caching/samples/sample10.cs)]

以编程方式定义 SQL 缓存依赖关系的优点之一是您可以处理任何可能发生的异常。 例如，如果你尝试为尚未启用通知的数据库定义 SQL 缓存依赖关系，则将引发**system.web.caching.databasenotenabledfornotificationexception**异常。 在这种情况下，你可以通过调用**SqlCacheDependencyAdmin. EnableNotifications**方法并向其传递数据库名称来尝试为通知启用数据库。

同样，如果你尝试为尚未启用通知的表定义 SQL 缓存依赖关系，则会引发**system.web.caching.tablenotenabledfornotificationexception** 。 然后，可以调用**SqlCacheDependencyAdmin. EnableTableForNotifications**方法向其传递数据库名称和表名称。

下面的代码示例演示如何在配置 SQL 缓存依赖项时正确配置异常处理。

[!code-csharp[Main](caching/samples/sample11.cs)]

详细信息： [https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>基于查询的 SQL 缓存依赖项（仅 SQL Server 2005）

为 SQL 缓存依赖关系使用 SQL Server 2005 时，不需要基于轮询的模型。 与 SQL Server 2005 一起使用时，SQL 缓存依赖项直接通过 SQL 连接传递到 SQL Server 实例（无需进一步配置）使用 SQL Server 2005 查询通知。

启用基于查询的通知的最简单方法是通过将数据源对象的**SqlCacheDependency**属性设置为**CommandNotification**并将**EnableCaching**属性设置为**true**，以声明方式执行此操作。 使用此方法时，无需任何代码。 如果对数据源执行的命令的结果发生更改，则会使缓存数据无效。

下面的示例为 SQL 缓存依赖项配置数据源控件：

[!code-aspx[Main](caching/samples/sample12.aspx)]

在这种情况下，如果**SelectCommand**中指定的查询返回的结果与最初的结果不同，则缓存的结果将失效。

还可以通过将 **@ OutputCache**指令的**SqlDependency**特性设置为**CommandNotification**，指定为 SQL 缓存依赖项启用所有数据源。 下面的示例阐释了这一点。

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> 有关 SQL Server 2005 中查询通知的详细信息，请参阅 SQL Server 联机丛书。

配置基于查询的 SQL 缓存依赖关系的另一种方法是使用 SqlCacheDependency 类以编程方式执行此操作。 下面的代码示例演示如何完成此操作。

[!code-csharp[Main](caching/samples/sample14.cs)]

详细信息： [https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>缓存后替换

缓存页可以显著提高 Web 应用程序的性能。 但是，在某些情况下，您需要缓存该页中的大部分，而页面内的某些片段是动态的。 例如，如果创建在设置的时间段内完全静态的新闻故事页面，则可以将整个页面设置为已缓存。 如果要包含在每次请求页面时更改的旋转广告横幅，则包含播发的页面部分必须是动态的。 若要允许缓存页面，但要动态替换部分内容，可以使用 ASP.NET 后缓存替换。 通过缓存后替换，整个页面都是用标记为不受缓存的特定部分进行缓存的输出。 在广告横幅的示例中，AdRotator 控件允许你利用缓存后的替换，以便为每个用户和每个页面刷新动态创建的广告。

有三种方法可以实现缓存后替换：

- 以声明方式使用替换控件。
- 使用替换控制 API 以编程方式。
- 使用 AdRotator 控件隐式。

### <a name="substitution-control"></a>替换控件

ASP.NET 替换控件指定动态创建而不是缓存的缓存页的一部分。 您可以将替换控件置于页面上希望显示动态内容的位置。 在运行时，替换控件调用使用方法名称属性指定的方法。 方法必须返回一个字符串，该字符串将替换替换控件的内容。 方法必须是包含页控件或 UserControl 控件上的静态方法。 使用替换控件将导致客户端可缓存性更改为服务器可缓存性，以便不会在客户端上缓存页面。 这可以确保以后向页面发出的请求再次调用该方法以生成动态内容。

### <a name="substitution-api"></a>替换 API

若要以编程方式为缓存页创建动态内容，可以在页代码中调用[WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx)方法，并将方法的名称作为参数传递。 处理动态内容创建的方法采用单个[HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)参数并返回一个字符串。 返回字符串是将在给定位置替换的内容。 调用 WriteSubstitution 方法（而不是以声明方式使用替换控件）的一个优点是，可以调用任意对象的方法，而不是调用页面或 UserControl 对象的静态方法。

调用 WriteSubstitution 方法将导致客户端可缓存性更改为服务器可缓存性，以便不会在客户端上缓存页面。 这可以确保以后向页面发出的请求再次调用该方法以生成动态内容。

### <a name="adrotator-control"></a>AdRotator 控件

AdRotator 服务器控件在内部实现对缓存后替换项的支持。 如果您将 AdRotator 控件置于页面上，则它将在每个请求上呈现唯一的广告，而不管是否缓存了父页。 因此，包含 AdRotator 控件的页面仅缓存服务器端。

## <a name="controlcachepolicy-class"></a>ControlCachePolicy 类

ControlCachePolicy 类允许使用用户控件以编程方式控制片段缓存。 ASP.NET 在[BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx)实例中嵌入用户控件。 BasePartialCachingControl 类表示启用了输出缓存的用户控件。

访问[PartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx)控件的[CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx)属性时，始终会收到有效的 ControlCachePolicy 对象。 但是，如果你访问 " [usercontrol](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) " 控件的[CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx)属性，则只有当用户控件已由 BasePartialCachingControl 控件包装时，才会收到有效的 ControlCachePolicy 对象。 如果未包装，属性返回的 ControlCachePolicy 对象将在您尝试对其进行操作时引发异常，因为它没有关联的 BasePartialCachingControl。 若要确定 UserControl 实例是否支持缓存而不生成异常，请检查[SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx)属性。

使用 ControlCachePolicy 类是启用输出缓存的多种方式之一。 以下列表描述了可用于启用输出缓存的方法：

- 使用[@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指令启用声明性方案中的输出缓存。
- 使用[PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx)属性可以在代码隐藏文件中为用户控件启用缓存。
- 使用 ControlCachePolicy 类可以在编程方案中指定缓存设置，在这些方案中，使用以前的方法之一并使用[TemplateControl LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)方法动态加载已启用缓存的 BasePartialCachingControl 实例。

只能在控件生命周期的初始和预呈现阶段之间成功处理 ControlCachePolicy 实例。 如果在预呈现阶段之后修改 ControlCachePolicy 对象，则 ASP.NET 会引发异常，因为呈现控件后所做的任何更改都不会影响缓存设置（控件在呈现阶段缓存）。 最后，在实际呈现时，用户控件实例（及其 ControlCachePolicy 对象）仅适用于编程操作。

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>缓存配置的更改-&lt;缓存&gt; 元素

ASP.NET 2.0 中对缓存配置进行了几处更改。 &lt;缓存&gt; 元素是 ASP.NET 2.0 中的新增功能，可用于在配置文件中进行缓存配置更改。 以下属性可用。

| **元素** | **描述** |
| --- | --- |
| **区** | 可选元素。 定义全局应用程序缓存设置。 |
| **outputCache** | 可选元素。 指定应用程序范围的输出缓存设置。 |
| **outputCacheSettings** | 可选元素。 指定可应用于应用程序中的页的输出缓存设置。 |
| **sqlCacheDependency** | 可选元素。 为 ASP.NET 应用程序配置 SQL 缓存依赖项。 |

### <a name="the-ltcachegt-element"></a>&lt;缓存&gt; 元素

&lt;cache&gt; 元素中提供以下属性：

| **特性** | **描述** |
| --- | --- |
| **disableMemoryCollection** | 可选的 **Boolean** 属性。 获取或设置一个值，该值指示在计算机处于内存压力下时发生的缓存内存收集是否处于禁用状态。 |
| **disableExpiration** | 可选的 **Boolean** 属性。 获取或设置一个值，该值指示是否禁用缓存过期。 如果禁用缓存项，则不会使缓存项过期，并且不会发生过期缓存项的后台清理。 |
| **privateBytesLimit** | 可选**Int64**特性。 获取或设置一个值，该值指示在缓存开始刷新过期项并尝试回收内存之前，应用程序的专用字节的最大大小。 此限制既包括缓存使用的内存，也包括正在运行的应用程序的正常内存开销。 如果设置为零，则表示 ASP.NET 将使用自己的试探法来确定何时开始回收内存。 |
| **percentagePhysicalMemoryUsedLimit** | 可选的**Int32**特性。 获取或设置一个值，该值指示在缓存开始刷新过期项并尝试回收内存之前，应用程序可以使用的计算机物理内存的最大百分比。此内存使用量同时包含缓存使用的内存作为正在运行的应用程序的正常内存使用情况。 如果设置为零，则表示 ASP.NET 将使用自己的试探法来确定何时开始回收内存。 |
| **privateBytesPollTime** | 可选的**TimeSpan**特性。 获取或设置一个值，该值指示应用程序的专用字节内存使用情况轮询之间的时间间隔。 |

### <a name="the-ltoutputcachegt-element"></a>&lt;outputCache&gt; 元素

以下属性可用于 &lt;outputCache&gt; 元素。

|       <strong>特性</strong>        |                                                                                                                                                                                                                                                       <strong>描述</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          可选的 <strong>Boolean</strong> 属性。 启用/禁用页面输出缓存。 如果禁用，则不会缓存任何页，无论采用何种编程方式或声明性设置。 默认值为 <strong>true</strong>。                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                可选的 <strong>Boolean</strong> 属性。 启用/禁用应用程序片段缓存。 如果禁用，则不会缓存任何页面，无论使用的是[@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx)指令还是使用缓存配置文件。 包括一个缓存控制标头，该标头指示上游代理服务器以及浏览器客户端不应尝试缓存页面输出。 默认值为“false”。                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      可选的 <strong>Boolean</strong> 属性。 获取或设置一个值，该值指示默认情况下是否由输出缓存模块发送<strong>缓存控件：专用</strong>标头。 默认值为“false”。                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | 可选的 <strong>Boolean</strong> 属性。 启用/禁用在响应中发送 Http "<strong>Vary： \</strong ><em>" 标头。默认设置为 false 时，</em>会为输出缓存页发送 "* Vary： \*<strong>" 标头。发送 Vary 标头时，它允许根据在 Vary 标头中指定的内容来缓存不同版本。例如， <em>Vary：用户代理</em>会根据发出请求的用户代理存储不同版本的页面。默认值为 * * false</strong>。 |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;outputCacheSettings&gt; 元素

如前文所述，&lt;outputCacheSettings&gt; 元素允许创建缓存配置文件。 &lt;outputCacheSettings&gt; 元素的唯一子元素是用于配置缓存配置文件的 &lt;outputCacheProfiles&gt; 元素。

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCacheDependency&gt; 元素

以下属性可用于 &lt;sqlCacheDependency&gt; 元素。

| **特性** | **描述** |
| --- | --- |
| **能够** | 必需的**布尔**属性。 指示是否正在轮询更改。 |
| **pollTime** | 可选的**Int32**特性。 设置 SqlCacheDependency 轮询数据库表以获取更改的频率。 此值对应于连续 pollings 之间的毫秒数。 不能将其设置为小于500毫秒。 默认值为1分钟。 |

### <a name="more-information"></a>详细信息

还应注意有关缓存配置的一些其他信息。

- 如果未设置工作进程专用字节数限制，则缓存将使用以下限制之一： 

    - x86 2GB：800MB 或60% 的物理 RAM，以较小者为准
    - x86 3GB：1800MB 或60% 的物理 RAM，以较小者为准
    - x64： 1 tb 或60% 的物理 RAM，以较小者为准
- 如果同时设置了工作进程专用字节数限制和 &lt;缓存 privateBytesLimit/&gt;，则缓存将使用二者中的最小值。
- 就像在1.x 中那样，我们会删除缓存条目并调用 GC。出于以下两个原因收集： 

    - 我们非常接近专用字节数限制
    - 可用内存接近或小于10%
- 可以通过将 &lt;cache percentagePhysicalMemoryUseLimit/&gt; 设置为100来有效地禁用剪裁和缓存。
- 与1.x 不同，2.0 将挂起剪裁，并在最后一个 GC 时收集调用。Collect 不会将专用字节或托管堆的大小减少1% （缓存）内存限制。

## <a name="lab1-custom-cache-dependencies"></a>Lab1：自定义缓存依赖项

1. 创建新网站。
2. 添加一个名为 "cache .xml" 的新 XML 文件，并将其保存到 Web 应用程序的根目录中。
3. 将以下代码添加到页面中\_Load 方法的 default.aspx： 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. 在源视图中，将以下内容添加到默认 .aspx 顶部： 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. 浏览 default.aspx。 时间是什么？
6. 刷新浏览器。 时间是什么？
7. 打开 cache .xml 并添加以下代码： 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. 保存缓存。
9. 刷新你的浏览器。 时间是什么？
10. 说明更新时间的原因，而不是显示以前缓存的值：

## <a name="lab-2-using-polling-based-cache-dependencies"></a>实验室2：使用基于轮询的缓存依赖项

此实验室使用您在上一个模块中创建的项目，该项目允许通过 GridView 和 DetailsView 控件在 Northwind 数据库中编辑数据。

1. 在 Visual Studio 2005 中打开项目。
2. 对 Northwind 数据库运行 aspnet\_regsql 实用工具，以启用数据库和 Products 表。 在 Visual Studio 命令提示符中使用以下命令： 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. 将以下内容添加到 web.config 文件： 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. 添加一个名为 showdata 的新 webform。
5. 将以下 @ outputcache 指令添加到 showdata 页： 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. 将以下代码添加到 showdata 的加载页面\_： 

    [!code-html[Main](caching/samples/sample21.html)]
7. 将新的 SqlDataSource 控件添加到 showdata，并将其配置为使用 Northwind 数据库连接。 单击“下一步”。
8. 选择 "ProductName 和 ProductID" 复选框，然后单击 "下一步"。
9. 单击“完成”。
10. 向 showdata 页添加新的 GridView。
11. 从下拉列表中选择 "SqlDataSource1"。
12. 保存并浏览 showdata。 记下显示的时间。
