---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: 配置和检测 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 中的配置和检测有重大变化。 新的 ASP.NET 配置 API 允许将配置更改为 pr 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: cd5bedce5459e8cf8e72df8de69ebd82f2d97789
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78507878"
---
# <a name="configuration-and-instrumentation"></a>配置和检测

由[Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 中的配置和检测有重大变化。 新的 ASP.NET 配置 API 允许以编程方式进行配置更改。 此外，还存在许多新的配置设置，允许进行新配置和检测。

ASP.NET 2.0 中的配置和检测有重大变化。 新的 ASP.NET 配置 API 允许以编程方式进行配置更改。 此外，还存在许多新的配置设置，允许进行新配置和检测。

在此模块中，我们将讨论与从 ASP.NET 配置文件中读取和写入相关的配置 API ASP.NET，我们还将介绍 ASP.NET 检测。 我们还将介绍 ASP.NET 跟踪中提供的新功能。

## <a name="aspnet-configuration-api"></a>ASP.NET 配置 API

ASP.NET 配置 API 允许使用单个编程接口开发、部署和管理应用程序配置数据。 您可以使用配置 API 以编程方式开发和修改完整的 ASP.NET 配置，而无需直接编辑配置文件中的 XML。 此外，还可以使用控制台应用程序中的配置 API、在基于 Web 的管理工具中以及在 Microsoft 管理控制台（MMC）管理单元中开发的脚本。

以下两个配置管理工具使用配置 API，并包含在 .NET Framework 版本2.0 中：

- ASP.NET MMC 管理单元，它使用配置 API 来简化管理任务，并提供来自所有级别的配置层次结构的本地配置数据的集成视图。
- 网站管理工具，可用于管理本地和远程应用程序（包括托管站点）的配置设置。

ASP.NET 配置 API 包含一组 ASP.NET 管理对象，可用于以编程方式配置网站和应用程序。 管理对象是作为 .NET Framework 类库实现的。 配置 API 编程模型通过在编译时强制数据类型来帮助确保代码的一致性和可靠性。 为了更轻松地管理应用程序配置，可以使用配置 API 查看从配置层次结构中的所有点合并为单个集合的数据，而不是将数据作为不同集合的单独集合查看配置文件。 此外，配置 API 使您能够操作整个应用程序配置，而无需在配置文件中直接编辑 XML。 最后，API 通过支持管理工具（例如网站管理工具）来简化配置任务。 配置 API 通过支持在计算机上创建配置文件并在多台计算机上运行配置脚本来简化部署。

> [!NOTE]
> 配置 API 不支持创建 IIS 应用程序。

## <a name="working-with-local-and-remote-configuration-settings"></a>使用本地和远程配置设置

配置对象表示应用于特定物理实体（例如计算机）的配置设置的合并视图，或应用于逻辑实体（如应用程序或网站）的配置设置的合并视图。 指定的逻辑实体可以存在于本地计算机上或远程服务器上。 如果指定实体不存在任何配置文件，则配置对象会按 machine.config 文件的定义来表示默认配置设置。

可以通过使用以下类中的一个打开的配置方法来获取配置对象：

1. 如果你的实体是客户端应用程序，则为 ConfigurationManager 类。
2. 如果你的实体是 Web 应用程序，则为 WebConfigurationManager 类。

这些方法将返回一个配置对象，该对象反过来提供处理基础配置文件所需的方法和属性。 您可以访问这些文件以进行读取或写入。

### <a name="reading"></a>阅读

使用 GetSection 或 GetSectionGroup 方法可以读取配置信息。 读取操作必须对层次结构中的所有配置文件都具有读取权限。

> [!NOTE]
> 如果使用采用路径参数的静态 GetSection 方法，路径参数必须引用运行代码的应用程序。 否则，将忽略该参数，并返回当前正在运行的应用程序的配置信息。

### <a name="writing"></a>写入

您可以使用其中一种保存方法来编写配置信息。 写入操作的用户或进程必须对当前配置层次结构级别的配置文件和目录具有写入权限，以及对层次结构中所有配置文件的读取权限。

若要生成一个配置文件，该文件表示指定实体的继承配置设置，请使用以下保存配置方法之一：

1. 用于创建新配置文件的 Save 方法。
2. 用于在另一个位置生成新配置文件的 SaveAs 方法。

## <a name="configuration-classes-and-namespaces"></a>配置类和命名空间

许多配置类和方法彼此类似。 下表介绍了最常用的配置类和命名空间。

| **配置类或命名空间** | **描述** |
| --- | --- |
| [System.web](https://msdn.microsoft.com/library/system.configuration.aspx)命名空间 | 包含所有 .NET Framework 应用程序的主要配置类。 节处理程序类用于从方法（例如 GetSection 和 GetSectionGroup）获取部分的配置数据。 这两种方法是非静态的。 |
| 配置类 | 表示计算机、应用程序、Web 目录或其他资源的一组配置数据。 此类包含有用的方法，如 GetSection 和 GetSectionGroup，用于更新配置设置和获取对节和节组的引用。 此类用作获取设计时配置数据的方法的返回类型，如 WebConfigurationManager 和 ConfigurationManager 类的方法。 |
| System.web 命名空间 | 包含在[ASP.NET 配置设置](https://msdn.microsoft.com/library/b5ysx397.aspx)中定义的 ASP.NET 配置节的节处理程序类。 节处理程序类用于从方法（例如 GetSection 和 GetSectionGroup）获取部分的配置数据。 |
| System.web. WebConfigurationManager 类 | 提供用于获取对运行时和设计时配置设置的引用的有用方法。 这些方法使用 System.web 类作为返回类型。 您可以使用此类的静态 GetSection 方法或 ConfigurationManager 类的非静态 GetSection 方法。 对于 Web 应用程序配置，建议使用 WebConfigurationManager 类，而不是 ConfigurationManager 类。 |
| [System.web](https://msdn.microsoft.com/library/system.configuration.provider.aspx)命名空间 | 提供了一种自定义和扩展配置提供程序的方法。 这是配置系统中所有提供程序类的基类。 |
| [System.web. Management](https://msdn.microsoft.com/library/system.web.management.aspx)命名空间 | 包含用来管理和监视 Web 应用程序运行状况的类和接口。 严格地说，此命名空间不被视为配置 API 的一部分。 例如，跟踪和事件激发由此命名空间中的类完成。 |
| [System.web](https://msdn.microsoft.com/library/system.management.instrumentation.aspx)命名空间 | 提供对应用程序进行检测所需的类，以便通过 Windows Management Instrumentation （WMI）将其管理信息和事件公开给潜在使用者。 ASP.NET 运行状况监视使用 WMI 传递事件。 严格地说，此命名空间不被视为配置 API 的一部分。 |

## <a name="reading-from-aspnet-configuration-files"></a>从 ASP.NET 配置文件中读取

WebConfigurationManager 类是用于从 ASP.NET 配置文件中读取的核心类。 读取 ASP.NET 配置文件实质上有三个步骤：

1. 使用 OpenWebConfiguration 方法获取配置对象。
2. 获取对配置文件中所需部分的引用。
3. 从配置文件中读取所需的信息。

配置对象表示不表示特定的配置文件。 相反，它表示计算机、应用程序或网站的配置的合并视图。 下面的代码示例实例化一个配置对象，该对象表示名为*data.productinfo*的 Web 应用程序的配置。

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> 请注意，如果/ProductInfo 路径不存在，则上述代码将返回 machine.config 文件中指定的默认配置。

获得配置对象后，可以使用 GetSection 或 GetSectionGroup 方法钻取到配置设置。 下面的示例获取对上述 Data.productinfo 应用程序的模拟设置的引用：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>写入到 ASP.NET 配置文件

与从配置文件中读取的一样，WebConfigurationManager 类是用于写入 Asp.NET 配置文件的核心。 还需要编写三个步骤来 ASP.NET 配置文件。

1. 使用 OpenWebConfiguration 方法获取配置对象。
2. 获取对配置文件中所需部分的引用。
3. 使用 Save 或 SaveAs 方法，从配置文件中写入所需的信息。

下面的代码将 &lt;编译&gt; 元素的**debug**特性更改为 false：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

执行此代码时， *webApp*应用程序的 web.config 文件的 &lt;编译&gt; 元素的**debug**属性将设置为 false。

## <a name="systemwebmanagement-namespace"></a>System.web. Management 命名空间

System.web 命名空间提供用于管理和监视 ASP.NET 应用程序运行状况的类和接口。

通过定义将事件与提供程序关联的规则来完成日志记录。 规则定义发送到提供程序的事件类型。 可以使用以下基本事件进行记录：

| **WebBaseEvent** | 所有事件的基本事件类。 包含所有事件（例如事件代码、事件详细信息代码、引发事件的日期和时间、序列号、事件消息和事件详细信息）所需的属性。 |
| --- | --- |
| **WebManagementEvent** | 管理事件的基本事件类，如应用程序生存期、请求、错误和审核事件。 |
| **WebHeartbeatEvent** | 应用程序定期生成的事件，以捕获有用的运行时状态信息。 |
| **WebAuditEvent** | 安全审核事件的基类，用于标记身份验证失败、解密失败*等情况。* |
| **WebRequestEvent** | 所有信息请求事件的基类。 |
| **WebBaseErrorEvent** | 指示错误条件的所有事件的基类。 |

可用的提供程序类型允许你将事件输出发送到事件查看器、SQL Server、Windows Management Instrumentation （WMI）和电子邮件。 预配置的提供程序和事件映射可减少获取记录事件输出所需的工作量。

ASP.NET 2.0 根据启动和停止的应用程序域，使用现成的事件日志提供程序来记录事件，并记录任何未经处理的异常。 这有助于涵盖一些基本方案。 例如，假设应用程序引发了异常，但用户不保存该错误，因而无法重现该错误。 使用默认事件日志规则，您可以收集异常和堆栈信息，以更好地了解发生了什么类型的错误。 另一个示例适用于你的应用程序是否丢失会话状态。 在这种情况下，你可以查看事件日志，以确定应用程序域是否正在回收，以及应用程序域首次停止的原因。

运行状况监视系统也可扩展。 例如，你可以定义自定义 Web 事件，在应用程序中触发这些事件，然后定义将事件信息发送到提供商（如电子邮件）的规则。 这使你可以轻松地将检测与运行状况监视提供程序关联。 作为另一个示例，你可以在每次处理订单时激发事件，并设置将每个事件发送到 SQL Server 数据库的规则。 当用户未能多次登录时，还可以触发事件，并将事件设置为使用基于电子邮件的访问接口。

默认提供程序和事件的配置存储在全局 web.config 文件中。 全局 web.config 文件存储存储在 ASP.NET 1x 中的 Machine.config 文件中的所有基于 Web 的设置。 全局 web.config 文件位于以下目录中：

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

全局 Web.config 文件的 &lt;healthMonitoring&gt; 部分提供了默认配置设置。 可以通过在应用程序的 web.config 文件中实现 &lt;healthMonitoring&gt; 部分来覆盖这些设置或配置自己的设置。

全局 Web.config 文件的 &lt;healthMonitoring&gt; 部分包含以下项：

| **providers** | 包含为事件查看器、WMI 和 SQL Server 设置的提供程序。 |
| --- | --- |
| **eventMappings** | 包含各种 WebBase 类的映射。 如果你生成自己的事件类，则可以扩展此列表。 生成自己的事件类，可以更精确地控制向其发送信息的提供程序。 例如，你可以将未经处理的异常配置为发送到 SQL Server，同时将你自己的自定义事件发送到电子邮件。 |
| **原则** | 将 eventMappings 链接到提供程序。 |
| **缓冲区** | 与 SQL Server 和电子邮件提供程序一起使用，以确定将事件刷新到提供程序的频率。 |

下面是来自全局 web.config 文件的代码示例。

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>如何将事件存储到事件查看器

如前所述，在全局 Web.config 文件中为事件查看器中的日志记录事件配置提供程序。 默认情况下，会记录基于**WebBaseErrorEvent**和**WebFailureAuditEvent**的所有事件。 可以添加其他规则，将其他信息记录到事件日志中。 例如，如果想要记录所有事件（*即*，基于**WebBaseEvent**的每个事件），可以将以下规则添加到 web.config 文件：

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

此规则会将 "**所有事件**" 事件映射链接到事件日志提供程序。 EventMapping 和提供程序都包含在全局 web.config 文件中。

## <a name="how-to-store-events-to-sql-server"></a>如何将事件存储到 SQL Server

此方法使用由 Aspnet\_regsql 工具生成的**aspnetdb.mdf**数据库。 默认提供程序使用 LocalSqlServer 连接字符串，该字符串使用应用中基于文件的数据库\_data 文件夹或 SQL Server 的本地 SQLExpress 实例。 LocalSqlServer 连接字符串和 SqlProvider 都在全局 web.config 文件中进行配置。

全局 Web.config 文件中的 LocalSqlServer 连接字符串如下所示：

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

如果要使用另一个 SQL Server 实例，则需要使用 Aspnet\_regsql 工具，该工具可以在%windir%\Microsoft.Net\Framework\v2.0. 中找到。\* 文件夹。 使用 Aspnet\_regsql 工具在 SQL Server 实例上生成自定义**aspnetdb.mdf**数据库，然后将连接字符串添加到应用程序配置文件，然后使用新的连接字符串添加提供程序。 创建**aspnetdb.mdf**数据库后，需要设置规则以将 eventMapping 链接到 sqlProvider。

无论您使用的是默认 SqlProvider 还是配置您自己的提供程序，都需要添加一个规则，将该提供程序链接到事件映射。 以下规则将前面创建的新提供程序链接到 "**所有事件**" 事件映射。 此规则将基于**WebBaseEvent**记录所有事件，并将其发送到将使用 MYASPNETDB 连接字符串的 MySqlWebEventProvider。 下面的代码添加了一个规则，用于将提供程序链接到事件映射：

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

如果只想将错误发送到 SQL Server，则可以添加以下规则：

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>如何将事件转发到 WMI

你还可以将事件转发到 WMI。 默认情况下，会在全局 web.config 文件中为您配置 WMI 提供程序。

下面的代码示例添加了一个规则，用于将事件转发到 WMI：

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

你将需要添加一个规则，以便将 eventMapping 与提供程序相关联，同时添加一个用于侦听事件的 WMI 侦听器应用程序。 下面的代码示例添加了一个规则，用于将 WMI 提供程序链接到 "**所有事件**" 事件映射：

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>如何将事件转发给电子邮件

你还可以将事件转发给电子邮件。 请注意你映射到你的电子邮件提供商的事件规则，因为你可能会无意间向自己发送大量可能更适合 SQL Server 或事件日志的信息。 有两个电子邮件提供商：SimpleMailWebEventProvider 和 TemplatedMailWebEventProvider。 每个属性都具有相同的配置属性（"模板" 和 "detailedTemplateErrors" 属性除外），这两个属性都仅在 TemplatedMailWebEventProvider 上可用。

> [!NOTE]
> 这两个电子邮件提供程序均未配置。 需要将它们添加到 Web.config 文件。

这两个电子邮件提供商之间的主要区别在于，SimpleMailWebEventProvider 在不能修改的通用模板中发送电子邮件。 Web.config 文件示例使用以下规则将此电子邮件提供程序添加到已配置的提供程序列表：

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

还添加了以下规则，将电子邮件提供程序与 "**所有事件**" 事件映射关联：

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2.0 跟踪

ASP.NET 2.0 中的跟踪有三个主要增强功能。

1. 集成跟踪功能
2. 对跟踪消息的编程访问
3. 改进的应用程序级别跟踪

## <a name="integrated-tracing-functionality"></a>集成跟踪功能

你现在可以将 ASP.NET 发出的消息路由到跟踪输出，并将 ASP.NET 跟踪发出的消息路由到。 还可以将 ASP.NET 检测事件转发到 "诊断"。 此功能由 &lt;trace&gt; 元素的新的**writeToDiagnosticsTrace**属性提供。 如果此布尔值为 true，则会将 ASP.NET 跟踪消息转发到系统。诊断跟踪基础结构，供所有已注册的侦听器用于显示跟踪消息。

## <a name="programmatic-access-to-trace-messages"></a>对跟踪消息的编程访问

ASP.NET 2.0 允许通过**TraceContextRecord**类和**TraceRecords**集合以编程方式访问所有跟踪消息。 访问跟踪消息最有效的方法是注册**TraceContextEventHandler**委托（也是 ASP.NET 2.0 中的新）以处理新的**TraceFinished**事件。 然后，你可以根据需要循环遍历跟踪消息。

下面的代码示例对此进行了说明：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

在上面的示例中，我循环遍历 TraceRecords 集合，然后将每条消息写入响应流。

## <a name="improved-application-level-tracing"></a>改进的应用程序级别跟踪

应用程序级跟踪通过引入 &lt;trace&gt; 元素的新**mostRecent**属性来改进。 此属性指定是否显示最新的应用程序级跟踪输出，以及超出 requestLimit 指示的限制的旧跟踪数据。 如果为 false，则在达到 requestLimit 属性之前为请求显示跟踪数据。

## <a name="aspnet-command-line-tools"></a>ASP.NET 命令行工具

有几个命令行工具可帮助配置 ASP.NET。 ASP.NET 开发人员应熟悉 aspnet\_regiis 工具。 ASP.NET 2.0 提供了三个其他命令行工具来帮助进行配置。

可以使用以下命令行工具：

| **工具** | **使用** |
| --- | --- |
| **aspnet\_regiis** | 允许将 ASP.NET 注册到 IIS。 此工具提供了两个版本的 ASP.NET 2.0，一个用于32位系统（在框架文件夹中），另一个用于64位系统（位于 Framework64 文件夹中）。64位版本将不会安装在32位操作系统上。 |
| **aspnet\_regsql** | ASP.NET SQL Server 注册工具用于创建 Microsoft SQL Server 数据库，供 ASP.NET 中的 SQL Server 提供程序使用，或者用于在现有数据库中添加或删除选项。 Aspnet\_regsql 文件位于 Web 服务器上的 [drive：] \WINDOWS\Microsoft.NET\Framework\versionNumber 文件夹中。 |
| **aspnet\_regbrowsers** | ASP.NET 浏览器注册工具会将所有系统范围的浏览器定义分析并编译到一个程序集中，并将该程序集安装到全局程序集缓存中。 该工具使用浏览器定义文件（。浏览器文件 .NET Framework）。 可在%SystemRoot%\Microsoft.NET\Framework\version\ 目录中找到该工具。 |
| **aspnet\_编译器** | 使用 ASP.NET 编译工具，可以就地编译 ASP.NET Web 应用程序，也可以将其部署到目标位置（如生产服务器）。 就地编译可帮助应用程序性能，因为在编译应用程序时，最终用户对应用程序的第一个请求不会有延迟。 |

由于 aspnet\_regiis 工具不是 ASP.NET 2.0 的新手，我们不会在此讨论。

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL Server 注册工具-aspnet\_regsql

可以使用 ASP.NET SQL Server 注册工具设置几种类型的选项。 您可以指定 SQL 连接，指定应用程序服务 SQL Server 使用哪些 ASP.NET 来管理信息，指示哪些数据库或表用于 SQL 缓存依赖关系，以及添加或删除对使用 SQL Server 来存储过程和会话状态的支持。

多个 ASP.NET 应用程序服务依赖于提供程序来管理存储和检索数据源中的数据。 每个提供程序都是特定于数据源的。 ASP.NET 包含以下 ASP.NET 功能的 SQL Server 提供程序：

- 成员身份（ [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx)类）。
- 角色管理（ [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx)类）。
- Profile （ [SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx)类）。
- Web 部件个性化（ [SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx)类）。
- Web 事件（ [SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx)类）。

当你安装 ASP.NET 时，你的服务器的 machine.config 文件将包含配置元素，这些元素指定依赖于提供程序的每个 ASP.NET 功能 SQL Server 提供程序。 默认情况下，这些提供程序配置为连接到 SQL Server Express 2005 的本地用户实例。 如果更改了提供程序使用的默认连接字符串，则在可以使用在计算机配置中配置的任何 ASP.NET 功能之前，必须使用 Aspnet\_regsql 安装所选功能的 SQL Server 数据库和数据库元素。 如果你使用 SQL 注册工具指定的数据库尚不存在（如果在命令行中未指定 aspnetdb.mdf，则它将为默认数据库），则当前用户必须有权在 SQL Server 中创建数据库，并创建架构 e数据库中的 lements。

### <a name="sql-cache-dependency"></a>SQL 缓存依赖项

ASP.NET 输出缓存的一项高级功能是使用 SQL 缓存依赖项。 SQL 缓存依赖项支持两种不同的操作模式：一个使用表轮询的 ASP.NET 实现，另一个使用 SQL Server 2005 的查询通知功能的模式。 SQL 注册工具可用于配置操作的表轮询模式。

### <a name="session-state"></a>会话状态

默认情况下，会话状态值和信息存储在 ASP.NET 进程中的内存中。 或者，你可以将会话数据存储在 SQL Server 数据库中，该数据库可供多个 Web 服务器共享。 如果您为使用 SQL 注册工具的会话状态指定的数据库尚不存在，则当前用户必须有权在 SQL Server 中创建数据库，并在数据库中创建架构元素。 如果数据库存在，则当前用户必须有权在现有数据库中创建架构元素。

若要在 SQL Server 上安装会话状态数据库，请运行 Aspnet\_regsql 工具，并在命令中提供以下信息：

- 使用 **-S**选项的 SQL Server 实例的名称。
- 有权在运行 SQL Server 的计算机上创建数据库的帐户的登录凭据。 使用 **-E**选项可以使用当前已登录的用户，或使用 **-U**选项指定用户 ID 以及使用 **-P**选项指定密码。
- 用于添加会话状态数据库的 **-ssadd**命令行选项。

默认情况下，你不能使用 Aspnet\_regsql 工具在运行 SQL Server 2005 Express Edition 的计算机上安装会话状态数据库。

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>ASP.NET 浏览器注册工具-aspnet\_regbrowsers

在 ASP.NET 版本1.1 中，Machine.config 文件包含名为 &lt;browserCaps&gt;的部分。 本部分包含一系列 XML 条目，这些条目定义了基于正则表达式的各种浏览器的配置。 对于 ASP.NET 版本2.0，则为新的。BROWSER 文件使用 XML 条目定义特定浏览器的参数。 通过添加新的浏览器，可以在新浏览器中添加信息。浏览器文件到位于系统%SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers 的文件夹。

由于应用程序不会在每次都需要浏览器信息时读取 .config 文件，因此你可以创建一个新的。浏览器文件并运行 Aspnet\_regbrowsers 将所需的更改添加到程序集。 这允许服务器立即访问新的浏览器信息，因此你无需关闭任何应用程序即可获取该信息。 应用程序可以通过当前 HttpRequest 的浏览器属性访问浏览器功能。

运行 aspnet\_regbrowser 时，可以使用以下选项：

| **选项** | **描述** |
| --- | --- |
| **-?** | 在命令窗口中显示 Aspnet\_regbbrowsers 帮助文本。 |
| **-i** | 创建运行时浏览器功能程序集，并将其安装在全局程序集缓存中。 |
| **-u** | 从全局程序集缓存中卸载运行时浏览器功能程序集。 |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>ASP.NET 编译工具-aspnet\_编译器

可以通过两种常规方式使用 ASP.NET 编译工具：适用于部署的就地编译和编译，其中指定了目标输出目录。

### <a name="compiling-an-application-in-place"></a>[就地编译应用程序](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET 编译工具可以就地编译应用程序，也就是说，它模拟了向应用程序发出多个请求的行为，从而导致了常规编译。 预编译站点的用户不会遇到因首次请求编译页面而导致的延迟。

就地预编译站点时，将应用以下各项：

- 站点保留其文件和目录结构。
- 你必须具有服务器上站点所用的所有编程语言的编译器。
- 如果任何文件编译失败，整个站点都将无法进行编译。

你还可以在向应用程序添加新的源文件后就地重新编译该应用程序。 该工具仅编译新的或已更改的文件，除非包含 **-c**选项。

> [!NOTE]
> 对包含嵌套应用程序的应用程序进行编译不会编译嵌套的应用程序。 必须单独编译嵌套的应用程序。

### <a name="compiling-an-application-for-deployment"></a>[编译要部署的应用程序](https://msdn.microsoft.com/library/ms229863.aspx)

可以通过指定 targetDir 参数来编译要部署的应用程序（编译到目标位置）。 TargetDir 可以是 Web 应用程序的最终位置，也可以进一步部署已编译的应用程序。 使用 **-u**选项编译应用程序时，可以在编译的应用程序中对某些文件进行更改而无需重新编译该应用程序。 Aspnet\_编译器在静态和动态文件类型之间进行区分，并在创建生成的应用程序时以不同方式处理它们。

- 静态文件类型是指没有关联的编译器或生成提供程序的类型，例如，名为的文件的扩展名为 .css、.gif、.htm、.html、.jpg、.js 等。 仅将这些文件复制到目标位置，并保留其在目录结构中的相对位置。
- 动态文件类型是具有关联编译器或生成提供程序的，其中包括具有 ASP.NET 特定文件扩展名的文件，例如： global.asax、.ascx、. foo.ashx、.aspx、.browser、.master 等。 ASP.NET 编译工具从这些文件生成程序集。 如果省略 **-u**选项，此工具还会创建文件扩展名为的文件。已编译，将原始源文件映射到其程序集。 为了确保保留应用程序源的目录结构，该工具会在目标应用程序中的相应位置生成占位符文件。

你必须使用 **-u**选项来指示可以修改已编译的应用程序的内容。 否则，将忽略后续修改或导致运行时错误。

下表说明了在包含 **-u**选项时，ASP.NET 编译工具如何处理不同的文件类型。

| **文件类型** | **编译器操作** |
| --- | --- |
| .ascx、.aspx、.master | 这些文件分为标记和源代码，其中包括代码隐藏文件和包含在 &lt;script runat = "server"&gt; 元素中的任何代码。 源代码编译为程序集，名称派生自哈希算法，并且程序集放在 Bin 目录中。 任何内联代码（即，括在 **&lt;%** 和 **%&gt;** 方括号之间的代码）都包含在标记中，并且不会进行编译。 将创建与源文件同名的新文件，以包含标记并将其放置在相应的输出目录中。 |
| . foo.ashx、.asmx | 这些文件不会进行编译，并按原样移到输出目录中，也不会进行编译。 如果希望编译处理程序代码，请将代码放入应用\_代码目录中的源代码文件中。 |
| .cs、.vb、. jsl、.cpp （不包括前面列出的文件类型的代码隐藏文件） | 这些文件将编译并作为资源包含在引用它们的程序集中。 不会将源文件复制到输出目录。 如果未引用代码文件，则不会对其进行编译。 |
| 自定义文件类型 | 这些文件不会进行编译。 这些文件将复制到相应的输出目录中。 |
| 应用\_代码子目录中的源代码文件 | 这些文件编译为程序集并放置在 Bin 目录中。 |
| 应用\_GlobalResources 子目录中的 .resx 和. 资源文件 | 这些文件编译为程序集并放置在 Bin 目录中。 不会在主输出目录下创建应用\_GlobalResources 子目录，并且源目录中的 .resx 或 .resources 文件都将被复制到输出目录中。 |
| 应用\_LocalResources 子目录中的 .resx 和. 资源文件 | 这些文件不会编译并复制到相应的输出目录中。 |
| 应用\_主题子目录中的 .skin 文件 | 不会编译 .skin 文件和静态主题文件，并且会将这些文件复制到相应的输出目录中。 |
| .browser Web.config 静态文件类型程序集已存在于 Bin 目录中 | 这些文件将按原样复制到输出目录。 |

下表说明了当省略 **-u**选项时，ASP.NET 编译工具如何处理不同的文件类型。

| **文件类型** | **编译器操作** |
| --- | --- |
| .aspx、.asmx、. foo.ashx、.master | 这些文件分为标记和源代码，其中包括代码隐藏文件和包含在 &lt;script runat = "server"&gt; 元素中的任何代码。 源代码编译为程序集，名称派生自哈希算法。 生成的程序集放在 Bin 目录中。 任何内联代码（即，括在 **&lt;%** 和 **%&gt;** 方括号之间的代码）都包含在标记中，并且不会进行编译。 编译器会创建新文件，以包含与源文件同名的标记。 这些生成的文件会置于 Bin 目录中。 编译器还会创建与源文件同名但扩展名为的文件。已编译，其中包含映射信息。 此.已编译的文件放置在对应于源文件的原始位置的输出目录中。 |
| .ascx | 这些文件被拆分为标记和源代码。 源代码编译为程序集并放置在 Bin 目录中，其名称派生自哈希算法。 不生成标记文件。 |
| .cs、.vb、. jsl、.cpp （不包括前面列出的文件类型的代码隐藏文件） | 由 .ascx、foo.ashx 或 .aspx 文件生成的程序集所引用的源代码将编译成程序集并放置在 Bin 目录中。 不复制任何源文件。 |
| 自定义文件类型 | 这些文件编译为动态文件。 编译器可以将映射文件放置在输出目录中，具体取决于它们所基于的文件的类型。 |
| 应用\_代码子目录中的文件 | 此子目录中的源代码文件编译为程序集并放置在 Bin 目录中。 |
| 应用\_GlobalResources 子目录中的文件 | 这些文件编译为程序集并放置在 Bin 目录中。 不会在主输出目录下创建应用\_GlobalResources 子目录。 如果配置文件指定 appliesTo = "All"，则将 .resx 和 .resources 文件复制到输出目录。 如果被[BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)引用，则不会复制它们。 |
| 应用\_LocalResources 子目录中的 .resx 和. 资源文件 | 这些文件编译为具有唯一名称并置于 Bin 目录中的程序集。 不会将 .resx 或. 资源文件复制到输出目录。 |
| 应用\_主题子目录中的 .skin 文件 | 主题编译到程序集中并置于 Bin 目录中。 为 .skin 文件创建存根文件，并将其放置在相应的输出目录中。 静态文件（如 .css）会被复制到输出目录。 |
| .browser Web.config 静态文件类型程序集已存在于 Bin 目录中 | 这些文件将按原样复制到输出目录。 |

### <a name="fixed-assembly-names"></a>[固定程序集名称](https://msdn.microsoft.com/library/ms229863.aspx##)

某些情况下（例如使用 MSI Windows Installer 部署 Web 应用程序）需要使用一致的文件名和内容，以及一致的目录结构来识别更新程序集或配置设置。 在这些情况下，可以使用 **-fixednames**选项指定 ASP.NET 编译工具应为每个源文件编译程序集，而不是使用将多个页编译到程序集中的。 这可能会导致生成大量程序集，因此，如果你担心可伸缩性，则应慎用此选项。

### <a name="strong-name-compilation"></a>[强名称编译](https://msdn.microsoft.com/library/ms229863.aspx##)

提供 **-aptca**、 **-delaysign**、 **-keycontainer**和 **-Keyfile**选项，以便您可以使用 Aspnet\_编译器创建强名称程序集，而无需单独使用[强名称工具（sn.exe）](https://msdn.microsoft.com/library/k5b5tt23.aspx) 。 这些选项分别对应于**AllowPartiallyTrustedCallersAttribute**、 **AssemblyDelaySignAttribute**、 **AssemblyKeyNameAttribute**和**AssemblyKeyFileAttribute**。

本课程的讨论范围之外介绍了这些属性。

## <a name="labs"></a>实验室

以下每个实验都在上一实验室上构建。 需要按顺序执行这些操作。

## <a name="lab-1-using-the-configuration-api"></a>实验室1：使用配置 API

1. 创建名为*mod9lab*的新网站。
2. 向站点添加新的 Web 配置文件。
3. 将以下内容添加到 web.config 文件：

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

这将确保您有权保存对 web.config 文件所做的更改。

1. 将新的 "标签" 控件添加到 default.aspx 并将 ID 更改为**lblDebugStatus**。
2. 将新的按钮控件添加到 default.aspx。
3. 将按钮控件的 ID 更改为**btnToggleDebug** ，并将文本更改为**切换调试状态**。
4. 打开 default.aspx 的代码隐藏文件的代码视图，并为**system.web**添加**using**语句，如下所示：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. 将两个私有变量添加到类和页\_Init 方法，如下所示：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. 将以下代码添加到页面\_负载：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. 保存并浏览默认 .aspx。 请注意，"标签" 控件显示当前的调试状态。
2. 双击设计器中的 "Button" 控件，并将以下代码添加到按钮控件的 Click 事件中：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. 保存并浏览 "default.aspx"，然后单击 "" 按钮。
2. 单击每个按钮后打开 web.config 文件，并观察 &lt;编译&gt; 部分中的**调试**属性。

## <a name="lab-2-logging-application-restarts"></a>实验室2：记录应用程序重启

在此实验室中，您将创建可用于在事件查看器中切换应用程序关闭、启动和重新编译的日志记录的代码。

1. 将 DropDownList 添加到 default.aspx 并将 ID 更改为 ddlLogAppEvents。
2. 将 DropDownList 的**AutoPostBack**属性设置为**true**。
3. 将三个项添加到 DropDownList 的项集合。 使第一项的**文本***选择值*和值-1。 使第二个项的**文本**和值**为 True** ，并使第三项**的文本和** **值为** **False**。
4. 将新标签添加到默认 .aspx。 将 ID 更改为**lblLogAppEvents**。
5. 打开 default.aspx 的代码隐藏视图，并为类型为 HealthMonitoringSection 的变量添加新的声明，如下所示：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. 将以下代码添加到页面中的现有代码\_Init：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. 双击 DropDownList 并将以下代码添加到 SelectedIndexChanged 事件：

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. 浏览 default.aspx。
2. 将下拉列表设置为**False**。
3. 清除事件查看器中的应用程序日志。
4. 单击该按钮可更改应用程序的调试属性。
5. 刷新事件查看器中的应用程序日志。 

    1. 是否记录了任何事件？
    2. 为什么或为什么不呢？
6. 将下拉列表设置为**True。**
7. 单击该按钮可以切换应用程序的调试属性。
8. 刷新事件查看器的应用程序登录名。 

    1. 是否记录了任何事件？
    2. 应用程序关闭的原因是什么？
9. 尝试启用和禁用日志记录，并查看对 web.config 文件所做的更改。

## <a name="more-information"></a>详细信息：

使用 ASP.NET 2.0 的提供程序模型，你可以创建自己的提供程序，不仅可用于应用程序检测，还可以创建许多其他用途，如成员身份、配置文件等。有关编写自定义提供程序以将应用程序事件记录到文本文件的详细信息，请访问[此链接](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)。
