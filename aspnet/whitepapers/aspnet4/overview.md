---
uid: whitepapers/aspnet4/overview
title: ASP.NET 4 和 Visual Studio 2010 Web 开发概述 |Microsoft Docs
author: rick-anderson
description: 本文档概述了 the.NET Framework 4 和 Visual Studio 2010 中包含的 ASP.NET 的许多新功能。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d7729af4-1eda-4ff2-8b61-dbbe4fc11d10
msc.legacyurl: /whitepapers/aspnet4
msc.type: content
ms.openlocfilehash: 8c93952adb33d1ce7008ebff9d032a71eb2a5f74
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995424"
---
# <a name="aspnet-4-and-visual-studio-2010-web-development-overview"></a>ASP.NET 4 和 Visual Studio 2010 Web 开发概述

> 本文档概述了 the.NET Framework 4 和 Visual Studio 2010 中包含的 ASP.NET 的许多新功能。
> 
> [下载此白皮书](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_and_Visual_Studio_2010_Web_Development_Overview.pdf)

**内容**

**[Core Services](#0.2__Toc253429238 "_Toc253429238")**  
Web.config[文件重构](#0.2__Toc253429239 "_Toc253429239")  
[可扩展的输出缓存](#0.2__Toc253429240 "_Toc253429240")  
[自动启动 Web 应用程序](#0.2__Toc253429241 "_Toc253429241")  
[永久重定向页面](#0.2__Toc253429242 "_Toc253429242")  
[收缩会话状态](#0.2__Toc253429243 "_Toc253429243")  
[展开允许的 Url 范围](#0.2__Toc253429244 "_Toc253429244")  
[可扩展请求验证](#0.2__Toc253429245 "_Toc253429245")  
[对象缓存和对象缓存扩展性](#0.2__Toc253429246 "_Toc253429246")  
[可扩展的 HTML、URL 和 HTTP 标头编码](#0.2__Toc253429247 "_Toc253429247")  
[单个工作进程中单个应用程序的性能监视](#0.2__Toc253429248 "_Toc253429248")  
[Multi-Targeting](#0.2__Toc253429249 "_Toc253429249")

**[Ajax](#0.2__Toc253429250 "_Toc253429250")**  
[Web 窗体和 MVC 中包含的 jQuery](#0.2__Toc253429251 "_Toc253429251")  
[内容交付网络支持](#0.2__Toc253429252 "_Toc253429252")  
[ScriptManager 显式脚本](#0.2__Toc253429253 "_Toc253429253")

**[Web Forms](#0.2__Toc253429256 "_Toc253429256")**  
[用 MetaKeywords 和 MetaDescription 属性设置 Meta 标记](#0.2__Toc253429257 "_Toc253429257")  
[启用各个控件的视图状态](#0.2__Toc253429258 "_Toc253429258")  
对[浏览器功能的更改](#0.2__Toc253429259 "_Toc253429259")  
[ASP.NET 4 中的路由](#0.2__Toc253429260 "_Toc253429260")  
[设置客户端 id](#0.2__Toc253429261 "_Toc253429261")  
[保持数据控件中的行选择](#0.2__Toc253429262 "_Toc253429262")  
[ASP.NET 图表控件](#0.2__Toc253429263 "_Toc253429263")  
[用 QueryExtender 控件筛选数据](#0.2__Toc253429264 "_Toc253429264")  
[Html 编码的代码表达式](#0.2__Toc253429265 "_Toc253429265")  
[项目模板更改](#0.2__Toc253429266 "_Toc253429266")  
[CSS 改进](#0.2__Toc253429267 "_Toc253429267")  
在[隐藏字段周围隐藏 Div 元素](#0.2__Toc253429268 "_Toc253429268")  
[为模板化控件呈现外部表](#0.2__Toc253429269 "_Toc253429269")  
[ListView 控件增强功能](#0.2__Toc253429270 "_Toc253429270")  
[CheckBoxList 和 RadioButtonList 控件增强功能](#0.2__Toc253429271 "_Toc253429271")  
[菜单控件改进](#0.2__Toc253429272 "_Toc253429272")  
[Wizard 和 CreateUserWizard 控件 56](#0.2__Toc253429273 "_Toc253429273")

**[ASP.NET MVC](#0.2__Toc253429274 "_Toc253429274")**  
[区域支持](#0.2__Toc253429275 "_Toc253429275")  
[数据-批注属性验证支持](#0.2__Toc253429276 "_Toc253429276")  
[模板化帮助]器(#0.2__Toc253429277 "_Toc253429277")

**[Dynamic Data](#0.2__Toc253429278 "_Toc253429278")**  
[为现有项目启用动态数据](#0.2__Toc253429279 "_Toc253429279")  
[声明性 DynamicDataManager 控件语法](#0.2__Toc253429280 "_Toc253429280")  
[实体模板](#0.2__Toc253429281 "_Toc253429281")  
[Url 和电子邮件地址的新字段模板](#0.2__Toc253429282 "_Toc253429282")  
[创建带有 DynamicHyperLink 控件的链接](#0.2__Toc253429283 "_Toc253429283")  
[数据模型中的继承支持](#0.2__Toc253429284 "_Toc253429284")  
[支持多对多关系 (仅实体框架)](#0.2__Toc253429285 "_Toc253429285")  
[用于控制显示和支持枚举的新属性](#0.2__Toc253429286 "_Toc253429286")  
[增强的筛选器支持](#0.2__Toc253429287 "_Toc253429287")

**[Visual Studio 2010 Web 开发改进](#0.2__Toc253429288 "_Toc253429288")**  
[提高了 CSS 兼容性](#0.2__Toc253429289 "_Toc253429289")  
[HTML 和 JavaScript 代码段](#0.2__Toc253429290 "_Toc253429290")  
[JavaScript IntelliSense 增强功能](#0.2__Toc253429291 "_Toc253429291")

**[用 Visual Studio 2010 部署 Web 应用程序](#0.2__Toc253429292 "_Toc253429292")**  
[Web 打包](#0.2__Toc253429293 "_Toc253429293")  
[Web.config Transformation](#0.2__Toc253429294 "_Toc253429294")  
[数据库部署](#0.2__Toc253429295 "_Toc253429295")  
[Web 应用程序一键式发布](#0.2__Toc253429296 "_Toc253429296")  
[Resources](#0.2__Toc253429297 "_Toc253429297")

**[Disclaimer](#0.2__Toc253429298 "_Toc253429298")**

<a id="0.2__Toc224729018"></a><a id="0.2__Toc253429238"></a><a id="0.2__Toc243304612"></a>

## <a name="core-services"></a>核心服务

ASP.NET 4 引入了许多功能, 可改善核心 ASP.NET 服务, 例如输出缓存和会话状态存储。

<a id="0.2__Toc243304613"></a><a id="0.2__Toc253429239"></a><a id="0.2__Toc224729019"></a>

### <a name="webconfig-file-refactoring"></a>Web.config 文件重构

由于添加了新功能 (如 Ajax、路由和与 IIS 7 的集成), 因此, 包含 Web 应用程序配置的文件在过去的几个版本上增长了很大的.NETFramework。`Web.config` 这样就无需使用 Visual Studio 之类的工具, 就可以更轻松地配置或启动新的 Web 应用程序。 在中, .net Framework 4 中的主要配置元素已移动到该`machine.config`文件中, 应用程序现在继承这些设置。 这允许 ASP.NET `Web.config` 4 应用程序中的文件为空或仅包含以下行, 这两行为 Visual Studio 指定应用程序面向的框架版本:

[!code-xml[Main](overview/samples/sample1.xml)]

<a id="0.2__Toc253429240"></a><a id="0.2__Toc243304614"></a>

### <a name="extensible-output-caching"></a>可扩展的输出缓存

自 ASP.NET 1.0 发布之日起, 输出缓存使开发人员能够将生成的页面、控件和 HTTP 响应的输出存储在内存中。 在后续 Web 请求中, ASP.NET 可以通过从内存中检索生成的输出, 而不是从头开始重新生成输出来更快地提供内容。 但是, 这种方法有一个限制: 始终必须将生成的内容存储在内存中, 并且在遇到大量流量的服务器上, 输出缓存使用的内存可能会与 Web 应用程序的其他部分中的内存需求争夺。

ASP.NET 4 将可扩展性点添加到输出缓存, 使你能够配置一个或多个自定义输出缓存提供程序。 输出缓存提供程序可以使用任何存储机制来保存 HTML 内容。 这样, 便可以为各种持久性机制 (包括本地或远程磁盘、云存储和分布式缓存引擎) 创建自定义输出缓存提供程序。

将自定义输出缓存提供程序创建为从新的*方便*类型派生的类。 然后, 可以使用*outputCache*元素的新`Web.config` provider 子节在文件中配置该提供程序, 如以下示例中所示:

[!code-xml[Main](overview/samples/sample2.xml)]

默认情况下, 在 ASP.NET 4 中, 所有 HTTP 响应、呈现的页面和控件都使用内存中输出缓存, 如前面的示例所示, 其中*defaultProvider*属性设置为 AspNetInternalProvider。 通过为*defaultProvider*指定不同的提供程序名称, 可以更改用于 Web 应用程序的默认输出缓存提供程序。

此外, 还可以为每个控件和每个请求选择不同的输出缓存提供程序。 为不同的 Web 用户控件选择不同的输出缓存提供程序的最简单方法是使用 control 指令中的 new *providerName*属性以声明方式执行此操作, 如以下示例中所示:

[!code-aspx[Main](overview/samples/sample3.aspx)]

为 HTTP 请求指定不同的输出缓存提供程序需要更多的工作。 不以声明方式指定提供程序, 而是覆盖 `Global.asax`文件中的新 GetOuputCacheProviderName 方法, 以编程方式指定要用于特定请求的提供程序。 下面的示例演示如何执行此操作。

[!code-csharp[Main](overview/samples/sample4.cs)]

通过向 ASP.NET 4 添加输出缓存提供程序扩展性, 你现在可以为你的网站提供更主动、更智能的输出缓存策略。 例如, 现在可以在内存中缓存站点的 "前10个" 页, 同时缓存可在磁盘上获取较低流量的页面。 或者, 你可以为呈现的页面缓存每个不同的不同组合, 但使用分布式缓存, 以便从前端 Web 服务器卸载内存消耗。

<a id="0.2__Toc224729020"></a><a id="0.2__Toc253429241"></a><a id="0.2__Toc243304615"></a>

### <a name="auto-start-web-applications"></a>自动启动 Web 应用程序

在处理第一个请求之前, 某些 Web 应用程序需要加载大量数据或执行昂贵的初始化处理。 在早期版本的 ASP.NET 中, 对于这种情况, 必须设计自定义方法来 "唤醒" ASP.NET 应用程序, 然后在该`Global.asax`文件中的*应用程序\_加载*方法期间运行初始化代码。

当 ASP.NET 4 在 Windows Server 2008 R2 上的 IIS 7.5 上运行时, 可以使用一个名为 "*自动启动*" 的新的可伸缩性功能, 该功能直接满足此方案。 自动启动功能提供了一种控制方法, 用于启动应用程序池、初始化 ASP.NET 应用程序, 然后接受 HTTP 请求。

> [!NOTE] 
> 
> Iis 7.5 的 IIS 应用程序预热模块
> 
> IIS 团队已发布 IIS 7.5 的应用程序预热模块的第一个 beta 版测试版本。 这会使应用程序的预热比之前介绍的更简单。 您可以指定在 Web 应用程序接受来自网络的请求之前要执行的资源 Url, 而不是编写自定义代码。 启动 IIS 服务 (如果将 IIS 应用程序池配置为*AlwaysRunning*) 和 iis 工作进程回收时, 会出现这种情况。 在回收期间, 旧的 IIS 工作进程将继续执行请求, 直到新生成的工作进程完全准备好, 这样应用程序就不会遇到中断或 unprimed 缓存引起的其他问题。 请注意, 此模块适用于 ASP.NET 的任何版本, 从版本2.0 开始。
> 
> 有关详细信息, 请参阅 IIS.net 网站上的[应用程序预热](https://www.iis.net/extensions/applicationwarmup%20on%20the%20IIS.net)。 有关演示如何使用预热功能的演练, 请参阅 IIS.net 网站上[的使用 IIS 7.5 应用程序预热模块入门](https://www.iis.net/learn/manage)。

若要使用自动启动功能, iis 管理员会在 iis 7.5 中将应用程序池设置为在`applicationHost.config`文件中使用以下配置自动启动:

[!code-xml[Main](overview/samples/sample5.xml)]

由于单个应用程序池可以包含多个应用程序, 因此可以使用以下配置在`applicationHost.config`文件中指定要自动启动的单个应用程序:

[!code-xml[Main](overview/samples/sample6.xml)]

当 iis 7.5 服务器冷启动或单个应用程序池被回收时, iis 7.5 会使用`applicationHost.config`文件中的信息来确定需要自动启动的 Web 应用程序。 对于标记为自动启动的每个应用程序, IIS 7.5 向 ASP.NET 4 发送请求, 以在应用程序暂时不接受 HTTP 请求的状态下启动应用程序。 当它处于此状态时, ASP.NET 将实例化由*serviceAutoStartProvider*属性定义的类型 (如前面的示例所示), 并调用其公共入口点。

通过实现*IProcessHostPreloadClient*接口, 可以创建具有所需入口点的托管自动启动类型, 如以下示例中所示:

[!code-csharp[Main](overview/samples/sample7.cs)]

在*预加载*方法中运行初始化代码并且方法返回后, ASP.NET 应用程序就可以处理请求了。

随着将自动启动添加到 IIS .5 和 ASP.NET 4, 你现在已有一个明确定义的方法, 用于在处理第一个 HTTP 请求之前执行开销较高的应用程序初始化。 例如, 你可以使用新的自动启动功能来初始化应用程序, 然后向负载平衡器发出信号, 指示该应用程序已初始化并准备接受 HTTP 流量。

<a id="0.2__Toc224729021"></a><a id="0.2__Toc253429242"></a><a id="0.2__Toc243304616"></a>

### <a name="permanently-redirecting-a-page"></a>永久重定向页面

Web 应用程序中常见的做法是在一段时间内四处移动页面和其他内容, 这可能导致搜索引擎中的过时链接堆积。 在 ASP.NET 中, 开发人员通过使用*响应重定向*方法将请求转发到旧 url。 但是,*重定向*方法会发出 Http 302 发现 (临时重定向) 响应, 这会在用户尝试访问旧 url 时产生额外的 HTTP 往返。

ASP.NET 4 添加了新的*RedirectPermanent*帮助器方法, 可轻松发出 HTTP 301 移动的永久响应, 如以下示例中所示:

[!code-csharp[Main](overview/samples/sample8.cs)]

用于识别永久重定向的搜索引擎和其他用户代理将存储与内容关联的新 URL, 从而消除了浏览器进行临时重定向时的不必要的往返过程。

<a id="0.2__Toc224729022"></a><a id="0.2__Toc253429243"></a><a id="0.2__Toc243304617"></a>

### <a name="shrinking-session-state"></a>收缩会话状态

ASP.NET 提供了两个默认选项, 用于在 Web 场中存储会话状态: 一个会话状态提供程序, 该提供程序调用进程外会话状态服务器, 以及一个将数据存储在 Microsoft SQL Server 数据库中的会话状态提供程序。 因为这两个选项都涉及将状态信息存储在 Web 应用程序的工作进程之外, 所以必须在将会话状态发送到远程存储之前对其进行序列化。 根据开发人员在会话状态中保存的信息量, 序列化数据的大小可能会很大。

对于这两种进程外会话状态提供程序, ASP.NET 4 引入了新的压缩选项。 如果下面的示例中所示的*compressionEnabled*配置选项设置为*true*, 则 ASP.NET 将使用 .NET Framework *GZipStream*类来压缩 (并解压缩) 序列化会话状态.

[!code-xml[Main](overview/samples/sample9.xml)]

通过简单地`Web.config`在文件中添加新属性, 在 Web 服务器上具有备用 CPU 周期的应用程序可以在序列化会话状态数据的大小上实现大幅降低。

<a id="0.2__Toc253429244"></a><a id="0.2__Toc243304618"></a>

### <a name="expanding-the-range-of-allowable-urls"></a>展开允许的 Url 范围

ASP.NET 4 引入了用于扩展应用程序 Url 大小的新选项。 以前版本的 ASP.NET 根据 NTFS 文件路径限制将 URL 路径长度限制为260个字符。 在 ASP.NET 4 中, 可以使用两个新的*httpRuntime*配置属性, 根据应用程序的需要增加 (或减少) 此限制。 下面的示例显示了这些新的属性。

[!code-xml[Main](overview/samples/sample10.xml)]

若要允许更长或更短的路径 (不包括协议、服务器名称和查询字符串的 URL 部分), 请修改 *[maxUrlLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxurllength.aspx)* 属性。 若要允许更长或更短的查询字符串, 请修改 *[maxQueryStringLength](https://msdn.microsoft.com/library/system.web.configuration.httpruntimesection.maxquerystringlength.aspx)* 属性的值。

ASP.NET 4 还允许您配置 URL 字符检查所使用的字符。 当 ASP.NET 在 URL 的路径部分找到无效字符时, 它将拒绝该请求并发出 HTTP 400 错误。 在以前版本的 ASP.NET 中, URL 字符检查限制为固定的字符集。 在 ASP.NET 4 中, 可以使用*httpRuntime*配置元素的新*requestPathInvalidCharacters*属性自定义一组有效字符, 如以下示例中所示:

[!code-xml[Main](overview/samples/sample11.xml)]

默认情况下, *requestPathInvalidCharacters*属性将8个字符定义为无效。 (在默认情况下, 分配给*requestPathInvalidCharacters*的字符串中&lt;, 小于 ()、大于 (&gt;) 和 & 号 (&amp;) 字符经过编码, 因为该`Web.config`文件是一个 XML 文件。)您可以根据需要自定义无效字符集。

> [!NOTE]
> 请注意, ASP.NET 4 始终拒绝在 ASCII 范围0x00 到0x1F 中包含字符的 URL 路径, 因为这些字符是在 IETF ([http://www.ietf.org/rfc/rfc2396.txt](http://www.ietf.org/rfc/rfc2396.txt)) 的 RFC 2396 中定义的无效 url 字符。 在运行 IIS 6 或更高版本的 Windows Server 版本上, http.sys 协议设备驱动程序会自动拒绝包含这些字符的 Url。

<a id="0.2__Toc253429245"></a><a id="0.2__Toc243304619"></a>

### <a name="extensible-request-validation"></a>可扩展请求验证

ASP.NET 请求验证会搜索传入的 HTTP 请求数据, 查找通常在跨站点脚本 (XSS) 攻击中使用的字符串。 如果发现潜在的 XSS 字符串, 请求验证会标记可疑字符串并返回错误。 内置请求验证仅在发现 XSS 攻击中使用的最常见字符串时才会返回错误。 以前尝试使 XSS 验证更积极会导致误报太多。 但是, 客户可能想要对更积极的请求进行验证, 或者相反, 可能想要为特定页面或特定类型的请求有意放松 XSS 检查。

在 ASP.NET 4 中, 已对请求验证功能进行了扩展, 使你可以使用自定义请求验证逻辑。 若要扩展请求验证, 请创建一个从新的*Util*类型派生的类, 并将应用程序 (在`Web.config`文件的*httpRuntime*节中) 配置为使用自定义类型。 下面的示例演示如何配置自定义请求验证类:

[!code-xml[Main](overview/samples/sample12.xml)]

新的*requestValidationType*属性需要指定提供自定义请求验证的类的标准 .NET Framework 类型标识符字符串。 对于每个请求, ASP.NET 会调用自定义类型来处理每个传入的 HTTP 请求数据。 传入 URL、所有 HTTP 标头 (cookie 和自定义标头) 和实体正文都可由自定义请求验证类进行检查, 如以下示例中所示:

[!code-csharp[Main](overview/samples/sample13.cs)]

对于不希望检查一段传入 HTTP 数据的情况, 请求验证类可以回退为通过只调用 base 来运行 ASP.NET 默认请求验证 *。IsValidRequestString。*

<a id="0.2__Toc253429246"></a><a id="0.2__Toc243304620"></a>

### <a name="object-caching-and-object-caching-extensibility"></a>对象缓存和对象缓存扩展性

自首次发布以来, ASP.NET 已包含一个功能强大的内存中对象缓存 ()。 缓存实现非常流行, 因为它已在非 Web 应用程序中使用。 不过, Windows 窗体或 WPF 应用程序在中包含对的引用`System.Web.dll`只是为了能够使用 ASP.NET 对象缓存。

为了使缓存可供所有应用程序使用, .NET Framework 4 引入了新的程序集、新的命名空间、某些基类型和具体的缓存实现。 新`System.Runtime.Caching.dll`程序集在*system.web*命名空间中包含新的缓存 API。 命名空间包含两个核心类集:

- 提供构建任何类型的自定义缓存实现的基础的抽象类型。
- 具体的内存中对象缓存实现 ( *MemoryCache*类)。

新的*MemoryCache*类在 ASP.NET 缓存上密切建模, 并与 ASP.NET 共享了许多内部缓存引擎逻辑。 尽管已更新了 system.exception 中的公共缓存 api 以支持开发自定义缓存, 但如果你使用了 ASP.NET*缓存*对象, 你将在新的 api 中找到熟悉的概念。

对于新的*MemoryCache*类和支持基本 api 的深入讨论, 需要一个完整的文档。 不过, 下面的示例为您提供了新的缓存 API 的工作原理。 该示例是为 Windows 窗体的应用程序编写的, 没有任何`System.Web.dll`依赖项。

[!code-csharp[Main](overview/samples/sample14.cs)]

<a id="0.2__Toc253429247"></a><a id="0.2__Toc243304621"></a>

### <a name="extensible-html-url-and-http-header-encoding"></a>可扩展的 HTML、URL 和 HTTP 标头编码

在 ASP.NET 4 中, 可以为以下常见文本编码任务创建自定义编码例程:

- HTML 编码。
- URL 编码。
- HTML 特性编码。
- 编码出站 HTTP 标头。

你可以通过从新的*Util*中派生来创建自定义编码器, 然后将 ASP.NET 配置为使用`Web.config`文件*httpRuntime*部分中的自定义类型, 如以下示例中所示:

[!code-xml[Main](overview/samples/sample15.xml)]

配置自定义编码器后, 只要调用*httputility.javascriptstringencode*或*HttpServerUtility*类的公共编码方法, ASP.NET 就会自动调用自定义编码实现。 这允许 Web 开发团队的一个部分创建可实现严格的字符编码的自定义编码器, 而其他 Web 开发团队则继续使用公共 ASP.NET 编码 Api。 通过在*httpRuntime*元素中集中配置自定义编码器, 可以确保来自公共 ASP.NET 编码 api 的所有文本编码调用都通过自定义编码器路由。

<a id="0.2__Toc253429248"></a><a id="0.2__Toc243304622"></a>

### <a name="performance-monitoring-for-individual-applications-in-a-single-worker-process"></a>单个工作进程中单个应用程序的性能监视

为了增加可在单个服务器上托管的网站的数量, 许多托管商在单个辅助进程中运行多个 ASP.NET 应用程序。 但是, 如果多个应用程序使用单个共享工作进程, 则服务器管理员很难识别遇到问题的单个应用程序。

ASP.NET 4 利用 CLR 引入的新的资源监视功能。 若要启用此功能, 可以将以下 XML 配置代码段添加到`aspnet.config`配置文件。

[!code-xml[Main](overview/samples/sample16.xml)]

> [!NOTE]
> 请注意`aspnet.config` , 该文件位于安装 .NET Framework 的目录中。 它不`Web.config`是文件。

启用*appDomainResourceMonitoring*功能后, "ASP.NET 应用程序" 性能类别中会提供两个新的性能计数器: *% 托管处理器时间*和*使用的托管内存*。 这两个性能计数器都使用新的 CLR 应用程序-域资源管理功能来跟踪单个 ASP.NET 应用程序的估计 CPU 时间和托管内存使用率。 因此, 使用 ASP.NET 4, 管理员现在可以更精细地查看单个辅助进程中运行的单个应用程序的资源消耗情况。

<a id="0.2__Toc253429249"></a><a id="0.2__Toc243304623"></a>

### <a name="multi-targeting"></a>多目标

你可以创建面向特定版本的 .NET Framework 的应用程序。 在 ASP.NET 4 中, 该`Web.config`文件的*编译*元素中的一个新属性使你可以针对 .NET Framework 4 和更高版本。 如果显式以 .NET Framework 4 为目标, 并且在`Web.config`文件中包含可选元素 (例如*system.object*的条目), 则这些元素必须是正确的 .NET Framework 4。 (如果未显式定位到 .NET Framework 4, 则将从该`Web.config`文件中缺少某个条目推断出目标框架。)

下面的示例演示如何在`Web.config`文件的*编译*元素中使用*targetFramework*特性。

[!code-xml[Main](overview/samples/sample17.xml)]

请注意以下有关特定版本的 .NET Framework 的信息:

- 在 .NET Framework 4 应用程序池中, 如果`Web.config`该文件不包含*targetFramework* `Web.config`特性或缺少该文件, 则 ASP.NET 生成系统会将 .NET Framework 4 作为目标。 (你可能需要对应用程序进行编码更改, 使其在 .NET Framework 4 下运行。)
- 如果包括*targetFramework*属性, 并且在`Web.config`文件中定义了*system.web*元素, 则此文件必须包含 .NET Framework 4 的正确条目。
- 如果使用*aspnet\_编译器*命令预编译应用程序 (如在生成环境中), 则必须为目标框架使用正确版本的*aspnet\_编译器*命令。 使用附带 .NET Framework 2.0 (%WINDIR%\Microsoft.NET\Framework\v2.0.50727) 的编译器编译 .NET Framework 3.5 及更早版本。 使用 .NET Framework 4 附带的编译器编译使用该框架或更高版本创建的应用程序。
- 在运行时, 编译器将使用计算机上安装的最新 framework 程序集 (因此在 GAC 中)。 如果稍后将更新到框架 (例如, 安装了假设版本 4.1), 则可以使用较新版本的 framework 中的功能, 即使*targetFramework*属性面向较低版本 (如 4.0)。 (但是, 在 Visual Studio 2010 的设计时或在使用*aspnet\_编译器*命令时, 使用该框架的新功能将导致编译器错误)。

<a id="0.2__Toc224729023"></a><a id="0.2__Toc253429250"></a><a id="0.2__Toc243304624"></a>

## <a name="ajax"></a>Ajax

<a id="0.2__Toc253429251"></a><a id="0.2__Toc243304625"></a>

### <a name="jquery-included-with-web-forms-and-mvc"></a>Web 窗体和 MVC 中包含的 jQuery

Web 窗体和 MVC 的 Visual Studio 模板都包含开放源代码 jQuery library。 创建新网站或项目时, 将创建一个包含以下3个文件的脚本文件夹:

- /Selfservice/scripts/jquery-1.10.2.min.js 1.4.1 – jQuery library 的用户可读的 unminified 版本。
- /Selfservice/scripts/jquery-1.10.2.min.js 14.1 版– jQuery library 的缩小版本。
- /Selfservice/scripts/jquery-1.10.2.min.js 1.4.1-vsdoc-jQuery library 的 Intellisense 文档文件。

开发应用程序时包括 jQuery 的 unminified 版本。 为生产应用程序包括 jQuery 的缩小版本。

例如, 下面的 Web 窗体页演示了如何使用 jQuery 将 ASP.NET TextBox 控件的背景色更改为黄色。

[!code-aspx[Main](overview/samples/sample18.aspx)]

<a id="0.2__Toc253429252"></a><a id="0.2__Toc243304626"></a>

### <a name="content-delivery-network-support"></a>内容交付网络支持

通过 Microsoft Ajax 内容交付网络 (CDN), 可以轻松地将 ASP.NET Ajax 和 jQuery 脚本添加到 Web 应用程序。 例如, 只需将一个`<script>`标记添加到页面, 就可以开始使用 jQuery library, 如下所示:

[!code-html[Main](overview/samples/sample19.html)]

利用 Microsoft Ajax CDN, 可以显著提高 Ajax 应用程序的性能。 Microsoft Ajax CDN 的内容缓存在位于世界各地的服务器上。 此外, Microsoft Ajax CDN 使浏览器可以为位于不同域中的网站重复使用缓存的 JavaScript 文件。

Microsoft Ajax 内容交付网络支持 SSL (HTTPS), 以防需要使用安全套接字层来提供网页。

当 CDN 不可用时, 实施回退。 测试回退。

若要了解有关 Microsoft Ajax CDN 的详细信息, 请访问以下网站:

[https://www.asp.net/ajaxlibrary/CDN.ashx](../../ajax/cdn/overview.md)

ASP.NET ScriptManager 支持 Microsoft Ajax CDN。 只需设置一个属性 EnableCdn 属性, 即可从 CDN 检索所有 ASP.NET framework JavaScript 文件:

[!code-aspx[Main](overview/samples/sample20.aspx)]

将 EnableCdn 属性设置为值 true 后, ASP.NET 框架将从 CDN 检索所有 ASP.NET framework JavaScript 文件, 其中包括用于验证和 UpdatePanel 的所有 JavaScript 文件。 设置此属性可能会对 web 应用程序的性能产生极大的影响。

可以使用 WebResource 属性为自己的 JavaScript 文件设置 CDN 路径。 新的 CdnPath 属性指定将 EnableCdn 属性设置为值 true 时使用的 CDN 的路径:

[!code-csharp[Main](overview/samples/sample21.cs)]

<a id="0.2__Toc253429253"></a><a id="0.2__Toc243304627"></a>

### <a name="scriptmanager-explicit-scripts"></a>ScriptManager 显式脚本

过去, 如果使用了 ASP.NET ScriptManger, 则需要加载整个单一 ASP.NET Ajax 库。 通过利用新的 AjaxFrameworkMode 属性, 您可以准确控制加载 ASP.NET Ajax 库的哪些组件并仅加载所需的 ASP.NET Ajax 库的组件。

可以将 AjaxFrameworkMode 属性设置为以下值:

- 已启用--指定 ScriptManager 控件自动包括 Microsoftajax.js 脚本文件, 该文件是每个核心框架脚本的合并脚本文件 (旧版行为)。
- Disabled-指定禁用所有 Microsoft Ajax script 功能, 并且 ScriptManager 控件不自动引用任何脚本。
- 显式--指定您将显式包括对页面所需的单独框架核心脚本文件的脚本引用, 并且您将包括对每个脚本文件所需的依赖项的引用。

例如, 如果将 AjaxFrameworkMode 属性设置为值 Explicit, 则可以指定所需的特定 ASP.NET Ajax 组件脚本:

[!code-aspx[Main](overview/samples/sample22.aspx)]

<a id="0.2__The_DataView_Control"></a><a id="0.2__The_DataContext_and"></a><a id="0.2__Refactoring_the_Microsoft"></a><a id="0.2__Toc224729032"></a><a id="0.2__Toc253429256"></a><a id="0.2__Toc243304630"></a>

## <a name="web-forms"></a>Web Forms — Web 窗体

自发布 ASP.NET 1.0 以来, Web 窗体已成为 ASP.NET 中的核心功能。 ASP.NET 4 的此区域已提供许多增强功能, 其中包括:

- 设置*meta*标记的功能。
- 更好地控制视图状态。
- 使用浏览器功能的更简单方法。
- 支持对 Web 窗体使用 ASP.NET 路由。
- 更好地控制生成的 Id。
- 可以在数据控件中保留选定的行。
- 更好地控制*FormView*和*ListView*控件中呈现的 HTML。
- 对数据源控件的筛选支持。

<a id="0.2__Toc224729033"></a><a id="0.2__Toc253429257"></a><a id="0.2__Toc243304631"></a>

### <a name="setting-meta-tags-with-the-pagemetakeywords-and-pagemetadescription-properties"></a>用 MetaKeywords 和 MetaDescription 属性设置 Meta 标记

ASP.NET 4 将两个属性添加到*页面*类*MetaKeywords*和*MetaDescription*。 这两个属性表示页面中对应的*元*标记, 如下面的示例中所示:

[!code-aspx[Main](overview/samples/sample23.aspx)]

这两个属性的工作方式与页面的 "*标题*" 属性相同。 它们遵循以下规则:

1. 如果*头*元素中没有与 MetaDescription 的属性名称匹配的*元*标记 (即*MetaKeywords*的 name = "关键字", 则为, 这意味着这些属性尚未设置), 则在呈现页面时, 会将*meta*标记添加到页面中。
2. 如果已存在具有这些名称的*元*标记, 则这些属性将充当现有标记的内容的 get 和 set 方法。

您可以在运行时设置这些属性, 这样您就可以从数据库或其他数据源中获取内容, 并使您可以动态设置标记来描述特定页面的用途。

你还可以在 Web 窗体页标记顶部的 *@ Page*指令中设置*关键字*和*说明*属性, 如以下示例中所示:

[!code-aspx[Main](overview/samples/sample24.aspx)]

这会重写页面中已声明的*元*标记内容 (如果有)。

Description*元*标记的内容用于改进 Google 中的搜索列表预览。 (有关详细信息, 请参阅 Google 网站管理员中心博客上的[使用元说明改善代码段功能改进](http://googlewebmastercentral.blogspot.com/2007/09/improve-snippets-with-meta-description.html)。)Google 和 Windows Live 搜索不会将关键字的内容用于任何内容, 但其他搜索引擎可能会。 有关详细信息, 请参阅搜索引擎指南网站上的[元关键字建议](http://www.searchengineguide.com/richard-ball/meta-keywords-a.php)。

这些新属性是一个简单的功能, 但它们会使你不需要手动添加这些属性或通过编写自己的代码来创建*元*标记。

<a id="0.2__Toc224729034"></a><a id="0.2__Toc253429258"></a><a id="0.2__Toc243304632"></a>

### <a name="enabling-view-state-for-individual-controls"></a>启用各个控件的视图状态

默认情况下, 将为页面启用视图状态, 结果是页面上的每个控件都可能存储视图状态, 即使应用程序不需要。 视图状态数据包含在页面生成的标记中, 并增加了向客户端发送页面并回发页面所需的时间。 如果存储的视图状态超出了所需的数量, 可能会导致性能显著下降。 在早期版本的 ASP.NET 中, 开发人员可以禁用各个控件的视图状态, 以便减小页面大小, 但必须为单个控件显式执行此操作。 在 ASP.NET 4 中, Web 服务器控件包含一个*ViewStateMode*属性, 该属性使你可以默认禁用视图状态, 然后只为需要在页面中使用它的控件启用该状态。

*ViewStateMode*属性采用包含三个值的枚举:*已启用*、*已禁用*和*继承*。 *启用*后, 将启用该控件的视图状态, 并为任何设置为*继承*或没有任何设置的子控件启用视图状态。 *Disabled*禁用视图状态, 而*Inherit*指定控件使用父控件中的*ViewStateMode*设置。

下面的示例演示*ViewStateMode*属性的工作方式。 以下页面中的控件的标记和代码包括*ViewStateMode*属性的值:

[!code-aspx[Main](overview/samples/sample25.aspx)]

正如您所看到的, 代码禁用了 PlaceHolder1 控件的视图状态。 子 label1 控件继承此属性值 (inherits是控件的*ViewStateMode*的默认值), 因此不保存任何视图状态。 在 PlaceHolder2 控件中, *ViewStateMode*设置为*Enabled*, 因此 label2 继承此属性并保存视图状态。 第一次加载页面时, 两个*标签*控件的*Text*属性都设置为字符串 "[DynamicValue]"。

这些设置的作用是: 当页面首次加载时, 浏览器中将显示以下输出:

Disabled`: [DynamicValue]`

能够`[DynamicValue]`

但回发后, 将显示以下输出:

Disabled`: [DeclaredValue]`

能够`[DynamicValue]`

Label1 控件 (其*ViewStateMode*值设置为 "*已禁用*") 未保留其在代码中设置为的值。 但是, label2 控件 (其*ViewStateMode*值设置为 "*已启用*") 已保持其状态。

你还可以在 *@ Page*指令中设置*ViewStateMode* , 如以下示例中所示:

[!code-aspx[Main](overview/samples/sample26.aspx)]

*Page*类只是另一个控件;它充当页面中所有其他控件的父控件。 为*页*的实例*启用*了*ViewStateMode*的默认值。 由于控件默认为*继承*, 因此控件将继承*Enabled*属性值, 除非你在页或控件级别设置*ViewStateMode* 。

*ViewStateMode*属性的值确定仅在*EnableViewState*属性设置为*true*时是否维护视图状态。 如果将*EnableViewState*属性设置为*false*, 则即使将*ViewStateMode*设置为 "*已启用*", 也不会维护视图状态。

此功能的一个不错用途是在母版页中使用*ContentPlaceHolder*控件, 你可以在其中将*ViewStateMode*设置为 "*已禁用*", 然后为*ContentPlaceHolder*控件逐个启用该母版页包含需要视图状态的控件。

<a id="0.2__Toc224729035"></a><a id="0.2__Toc253429259"></a><a id="0.2__Toc243304633"></a>

### <a name="changes-to-browser-capabilities"></a>对浏览器功能的更改

ASP.NET 确定用户使用的浏览器功能, 该浏览器使用一种名为*浏览器功能*的功能来浏览您的网站。 浏览器功能由*HttpBrowserCapabilities*对象表示 (由*请求. Browser*属性公开)。 例如, 可以使用*HttpBrowserCapabilities*对象来确定当前浏览器的类型和版本是否支持特定版本的 JavaScript。 或者, 你可以使用*HttpBrowserCapabilities*对象来确定请求是否来自移动设备。

*HttpBrowserCapabilities*对象由一组浏览器定义文件驱动。 这些文件包含有关特定浏览器的功能的信息。 在 ASP.NET 4 中, 这些浏览器定义文件已更新为包含有关最近引入的浏览器和设备 (如 Google Chrome、运动 BlackBerry 智能手机和 Apple iPhone) 的信息。

以下列表显示了新的浏览器定义文件:

- *blackberry.browser*
- *chrome.browser*
- *Default.browser*
- *firefox.browser*
- *gateway.browser*
- *generic.browser*
- *ie.browser*
- *iemobile.browser*
- *iphone.browser*
- *opera.browser*
- *safari.browser*

#### <a name="using-browser-capabilities-providers"></a>使用浏览器功能提供程序

在 ASP.NET 版本 3.5 Service Pack 1 中, 可以使用以下方式定义浏览器的功能:

- 在计算机级别, 可以创建或更新`.browser`以下文件夹中的 XML 文件:

- [!code-console[Main](overview/samples/sample27.cmd)]

- 定义浏览器功能后, 可以从 Visual Studio 命令提示符运行以下命令, 以便重新生成浏览器功能程序集并将其添加到 GAC:

- [!code-console[Main](overview/samples/sample28.cmd)]

- 对于单个应用程序, 在应用程序`.browser`的`App_Browsers`文件夹中创建一个文件。

这些方法要求你更改 XML 文件, 对于计算机级更改, 你必须在运行 aspnet\_regbrowsers 进程后重新启动应用程序。

ASP.NET 4 包含一项称为*浏览器功能提供程序*的功能。 顾名思义, 这允许您生成一个提供程序, 然后您可以使用自己的代码来确定浏览器的功能。

实际上, 开发人员通常不会定义自定义浏览器功能。 浏览器文件很难更新, 更新这些文件的过程相当复杂, 使用和定义`.browser`文件的 XML 语法可能会很复杂。 如果有常见的浏览器定义语法, 或是包含最新的浏览器定义的数据库, 甚至是此类数据库的 Web 服务, 则使此过程变得简单得多。 新的浏览器功能提供程序功能使得第三方开发人员可以实现这些方案。

使用 new ASP.NET 4 browser 功能提供程序功能时, 有两种主要方法: 扩展 ASP.NET 浏览器功能定义功能, 或完全替换。 以下各节介绍了如何替换功能, 以及如何对其进行扩展。

#### <a name="replacing-the-aspnet-browser-capabilities-functionality"></a>替换 ASP.NET 浏览器功能功能

若要完全替换 ASP.NET 浏览器功能定义功能, 请执行以下步骤:

1. 创建一个派生自*HttpCapabilitiesProvider*的提供程序类, 该提供程序类将重写*GetBrowserCapabilities*方法, 如以下示例中所示: 

    [!code-csharp[Main](overview/samples/sample29.cs)]

    此示例中的代码创建一个新的*HttpBrowserCapabilities*对象, 该对象仅指定名为 browser 的功能, 并将该功能设置为 MyCustomBrowser。
2. 将提供程序注册到应用程序。 

    若要将提供程序与应用程序一起使用, 必须将*提供程序*特性添加到 `Web.config`或`Machine.config`文件的 browserCaps 节中。 (你还可以在*location*元素中为应用程序中的特定目录定义提供程序属性, 例如在特定移动设备的文件夹中。)下面的示例演示如何在配置文件中设置*provider*特性:

    [!code-xml[Main](overview/samples/sample30.xml)]

    注册新的浏览器功能定义的另一种方法是使用代码, 如以下示例中所示:

    [!code-csharp[Main](overview/samples/sample31.cs)]

    此代码必须在`Global.asax`文件的*应用\_程序启动*事件中运行。 对*BrowserCapabilitiesProvider*类所做的任何更改必须在执行应用程序中的任何代码之前发生, 以确保缓存对于解析的*HttpCapabilitiesBase*对象保持有效状态。

#### <a name="caching-the-httpbrowsercapabilities-object"></a>缓存 HttpBrowserCapabilities 对象

前面的示例有一个问题, 即每次调用自定义提供程序来获取*HttpBrowserCapabilities*对象时, 代码都将运行。 这可能会在每个请求期间发生多次。 在此示例中, 提供程序的代码不会执行许多操作。 但是, 如果你的自定义提供程序中的代码执行了大量工作来获取*HttpBrowserCapabilities*对象, 则这可能会影响性能。 若要防止此情况发生, 可以缓存*HttpBrowserCapabilities*对象。 请执行以下步骤：

1. 创建一个派生自*HttpCapabilitiesProvider*的类, 如下例所示: 

    [!code-csharp[Main](overview/samples/sample32.cs)]

    在此示例中, 代码通过调用自定义 BuildCacheKey 方法生成一个缓存密钥, 并通过调用自定义 GetCacheTime 方法获取缓存的时间长度。 然后, 该代码将解析的*HttpBrowserCapabilities*对象添加到缓存中。 可以从缓存中检索对象, 并可在后续请求中重复使用自定义提供程序。
2. 按照前面的过程中所述, 将提供程序注册到应用程序。

#### <a name="extending-aspnet-browser-capabilities-functionality"></a>扩展 ASP.NET 浏览器功能功能

上一部分介绍了如何在 ASP.NET 4 中创建新的*HttpBrowserCapabilities*对象。 还可以通过将新的浏览器功能定义添加到已在 ASP.NET 中的功能, 来扩展 ASP.NET 浏览器功能。 可以在不使用 XML 浏览器定义的情况下执行此操作。 下面的过程演示了如何操作。

1. 创建一个从*HttpCapabilitiesEvaluator*派生的类, 它将重写*GetBrowserCapabilities*方法, 如以下示例中所示: 

    [!code-csharp[Main](overview/samples/sample33.cs)]

    此代码首先使用 ASP.NET 浏览器功能功能来尝试标识浏览器。 但是, 如果未根据请求中定义的信息来标识浏览器 (即, 如果*HttpBrowserCapabilities*对象的*browser*属性为字符串 "Unknown"), 则代码将调用自定义提供程序 (MyBrowserCapabilitiesEvaluator) 来标识浏览器。
2. 按照前面的示例中所述, 将提供程序注册到应用程序。

#### <a name="extending-browser-capabilities-functionality-by-adding-new-capabilities-to-existing-capabilities-definitions"></a>通过向现有功能定义添加新功能来扩展浏览器功能功能

除了创建自定义浏览器定义提供程序并动态创建新的浏览器定义以外, 还可以使用其他功能来扩展现有的浏览器定义。 这使你可以使用接近所需内容的定义, 但仅缺少几个功能。 为此，请执行下列步骤。

1. 创建一个从*HttpCapabilitiesEvaluator*派生的类, 它将重写*GetBrowserCapabilities*方法, 如以下示例中所示: 

    [!code-csharp[Main](overview/samples/sample34.cs)]

    示例代码扩展现有的 ASP.NET *HttpCapabilitiesEvaluator*类, 并通过使用以下代码获取与当前请求定义匹配的*HttpBrowserCapabilities*对象:

    [!code-csharp[Main](overview/samples/sample35.cs)]

    然后, 代码可以添加或修改此浏览器的功能。 可以通过两种方式来指定新的浏览器功能:

    - 将键/值对添加到由*HttpCapabilitiesBase*对象的*功能*属性公开的*IDictionary*对象。 在上面的示例中, 代码添加了一个名为 "多点触控" 的功能, 其值为*true*。
    - 设置*HttpCapabilitiesBase*对象的现有属性。 在上面的示例中, 代码将 "*帧*" 属性设置为 " *true*"。 此属性只是由*功能*属性公开的*IDictionary*对象的访问器。 

        > [!NOTE]
        > 请注意, 此模型适用于*HttpBrowserCapabilities*的任何属性, 包括控件适配器。
2. 按照前面的过程中所述, 将提供程序注册到应用程序。

<a id="0.2__Toc224729036"></a><a id="0.2__Toc253429260"></a><a id="0.2__Toc243304634"></a>

### <a name="routing-in-aspnet-4"></a>ASP.NET 4 中的路由

ASP.NET 4 添加了对使用 Web 窗体的路由的内置支持。 通过路由, 你可以将应用程序配置为接受未映射到物理文件的请求 Url。 相反, 你可以使用路由来定义对用户有意义的 Url, 并可以帮助你的应用程序使用搜索引擎优化 (SEO)。 例如, 显示现有应用程序中的产品类别的页面的 URL 可能类似于以下示例:

[!code-console[Main](overview/samples/sample36.cmd)]

通过使用路由, 你可以将应用程序配置为接受以下 URL 来呈现相同的信息:

[!code-console[Main](overview/samples/sample37.cmd)]

从 ASP.NET 3.5 SP1 开始, 路由已可用。 (有关如何在 ASP.NET 3.5 SP1 中使用路由的示例, 请参阅(http://haacked.com/archive/2008/03/11/using-routing-with-webforms.aspx "此项")的[使用 WebForms 的路由]的条目。 在 Phil Haack 的博客上。)但是, ASP.NET 4 包含一些使使用路由更容易的功能, 其中包括:

- *PageRouteHandler*类, 它是在定义路由时使用的简单 HTTP 处理程序。 类将数据传递到请求路由到的页面。
- 新属性*HttpRequest RequestContext*和*RouteData* (这是*HttpRequest* RequestContext 对象的代理)。 通过这些属性, 可更轻松地访问从路由传递的信息。
- 下面是在*RouteUrlExpressionBuilder*和*RouteValueExpressionBuilder*中定义的以下新的表达式生成器:):
- *RouteUrl*, 它提供了一种简单的方法来创建与 ASP.NET 服务器控件内的路由 url 相对应的 url。
- *RouteValue*, 它提供了一种从*RouteContext*对象中提取信息的简单方法。
- *RouteParameter*类, 可更轻松地将*RouteContext*对象中包含的数据传递到数据源控件的查询 (类似于[*FormParameter*](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx))。

#### <a name="routing-for-web-forms-pages"></a>Web 窗体页的路由

下面的示例演示如何使用*路由*类的新的*MapPageRoute*方法定义 Web 窗体路由:

[!code-csharp[Main](overview/samples/sample38.cs)]

ASP.NET 4 引入了*MapPageRoute*方法。 下面的示例与上一示例中所示的 SearchRoute 定义等效, 但使用*PageRouteHandler*类。

[!code-csharp[Main](overview/samples/sample39.cs)]

该示例中的代码将路由映射到物理页 (位于第一个路由`~/search.aspx`中)。 第一个路由定义还指定了应从 URL 中提取名为 searchterm 的参数并将其传递到页面。

*MapPageRoute*方法支持以下方法重载:

- *MapPageRoute (string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess)*
- *MapPageRoute (string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 默认值)*
- *MapPageRoute (string routeName, string routeUrl, string physicalFile, bool checkPhysicalUrlAccess, RouteValueDictionary 默认值, RouteValueDictionary 约束)*

*CheckPhysicalUrlAccess*参数指定路由是否应检查要路由到的物理页面的安全权限 (在本例中为 searchterm), 以及对传入 URL 的权限 (在本例中为 search/{})。 如果*checkPhysicalUrlAccess*的值为*false*, 则仅检查传入 URL 的权限。 使用如下设置在`Web.config`文件中定义这些权限:

[!code-xml[Main](overview/samples/sample40.xml)]

在此示例配置中, 除管理员角色中的用户`search.aspx`外, 对所有用户的物理页面的访问被拒绝。 如果将*checkPhysicalUrlAccess*参数设置为*true* (默认值), 则仅允许管理员用户访问 URL/search/{searchterm}, 因为物理页面搜索 .aspx 仅限于该角色中的用户。 如果将*checkPhysicalUrlAccess*设置为*false* , 并按前面的示例所示配置了站点, 则允许所有经过身份验证的用户访问 URL/search/{searchterm}。

#### <a name="reading-routing-information-in-a-web-forms-page"></a>在 Web 窗体页中读取路由信息

在 Web 窗体物理页面的代码中, 你可以使用两个新属性访问从 URL (或其他对象已添加到*RouteData*对象中的其他信息) 中提取的信息:*HttpRequest. RequestContext*和*RouteData*。 (*RouteData*包装 HttpRequest. *RequestContext. RouteData*.)下面的示例演示如何使用*RouteData*。

[!code-csharp[Main](overview/samples/sample41.cs)]

此代码提取为 searchterm 参数传递的值, 如前面的示例路由中所定义的那样。 请考虑以下请求 URL:

[!code-console[Main](overview/samples/sample42.cmd)]

发出此请求时, 将在`search.aspx`页面中呈现 "scott" 一词。

#### <a name="accessing-routing-information-in-markup"></a>访问标记中的路由信息

上一部分中所述的方法演示如何在 Web 窗体页中的代码中获取路由数据。 你还可以使用标记中的表达式, 这些表达式可让你访问相同的信息。 表达式生成器是一种功能强大且巧妙的方法来处理声明性代码。 (有关详细信息, 请参阅 Phil Haack 的博客上的入门[版自定义表达式生成器](http://haacked.com/archive/2006/11/29/Express_Yourself_With_Custom_Expression_Builders.aspx)。)

ASP.NET 4 包含用于 Web 窗体路由的两个新表达式生成器。 下面的示例演示如何使用它们。

[!code-aspx[Main](overview/samples/sample43.aspx)]

在此示例中, *RouteUrl*表达式用于定义基于路由参数的 URL。 这使你无需将完整的 URL 硬编码为标记, 并使你可以在以后更改 URL 结构, 而无需更改此链接。

根据前面定义的路由, 此标记生成以下 URL:

[!code-console[Main](overview/samples/sample44.cmd)]

ASP.NET 根据输入参数自动处理正确的路由 (也就是说, 它会生成正确的 URL)。 您还可以在表达式中包含一个路由名称, 这允许您指定要使用的路由。

下面的示例演示如何使用*RouteValue*表达式。

[!code-aspx[Main](overview/samples/sample45.aspx)]

当包含此控件的页运行时, 值 "scott" 将显示在标签中。

使用*RouteValue*表达式可以轻松地在标记中使用路由数据, 并避免在标记中使用更复杂的 RouteData ["x"] 语法。

#### <a name="using-route-data-for-data-source-control-parameters"></a>对数据源控件参数使用路由数据

使用*RouteParameter*类可以将路由数据指定为数据源控件中查询的参数值。 它[的工作方式非常类似](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formparameter.aspx)于类, 如下面的示例中所示:

[!code-aspx[Main](overview/samples/sample46.aspx)]

在这种情况下，路由参数 searchterm 的值将用于@companyname中的参数 *选择* 语句。

<a id="0.2__Toc224729037"></a><a id="0.2__Toc253429261"></a><a id="0.2__Toc243304635"></a>

### <a name="setting-client-ids"></a>设置客户端 Id

新的*ClientIDMode*属性解决了 ASP.NET 中的长期问题, 即控件如何为其呈现的元素创建*id*属性。 如果你的应用程序包括引用这些元素的客户端脚本, 则了解呈现元素的*id*属性是很重要的。

为 Web 服务器控件呈现的 HTML 中的*id*属性是根据控件的*ClientID*属性生成的。 在 ASP.NET 4 之前, 从*ClientID*属性生成*id*属性的算法已将命名容器 (如果有) 与 id 连接在一起, 对于重复的控件 (如在数据控件中), 若要添加前缀和顺序多种. 虽然这始终保证页面中控件的 Id 是唯一的, 但算法导致了不可预测的控件 Id, 因此很难在客户端脚本中引用它们。

新的*ClientIDMode*属性使你可以更精确地指定为控件生成客户端 ID 的方式。 可以为任何控件设置*ClientIDMode*属性, 包括页面的。 可能的设置如下所示:

- *AutoID* –这等效于用于生成*ClientID*属性值的算法, 该算法在早期版本的 ASP.NET 中使用。
- *Static* –指定*ClientID*值将与 id 相同, 而不会连接父命名容器的 id。 这对于 Web 用户控件很有用。 由于 Web 用户控件可以位于不同的页上和不同的容器控件中, 因此很难为使用*AutoID*算法的控件编写客户端脚本, 因为你无法预测 ID 值将是什么。
- *可预测*–此选项主要用于使用重复模板的数据控件。 它连接控件的命名容器的 ID 属性, 但生成的*ClientID*值不包含类似于 "ctlxxx" 的字符串。 此设置与控件的*ClientIDRowSuffix*属性结合使用。 将*ClientIDRowSuffix*属性设置为数据字段的名称, 该字段的值将用作生成的*ClientID*值的后缀。 通常使用数据记录的主键作为*ClientIDRowSuffix*值。
- *Inherit* –此设置是控件的默认行为;它指定控件的 ID 生成与其父级相同。

可以在页级别设置*ClientIDMode*属性。 这会为当前页中的所有控件定义默认的*ClientIDMode*值。

页面级别的默认*ClientIDMode*值为*AutoID*, 并且控件级别的默认*ClientIDMode*值将*继承*。 因此, 如果你未在代码中的任何位置设置此属性, 则所有控件将默认为*AutoID*算法。

在 *@ page*指令中设置页面级别的值, 如以下示例中所示:

[!code-aspx[Main](overview/samples/sample47.aspx)]

你还可以在配置文件中的 "计算机" 级别或应用程序级别上设置*ClientIDMode*值。 这将为应用程序中所有页面上的所有控件定义默认的*ClientIDMode*设置。 如果在计算机级别设置了值, 则它将为该计算机上的所有网站定义默认的*ClientIDMode*设置。 下面的示例演示配置文件中的*ClientIDMode*设置:

[!code-xml[Main](overview/samples/sample48.xml)]

如前文所述, *ClientID*属性的值派生自控件父对象的命名容器。 在某些情况下, 例如在使用母版页时, 控件可能最终会生成类似于以下呈现的 HTML 中的 Id:

[!code-html[Main](overview/samples/sample49.html)]

尽管标记中显示的*输入*元素 (来自*TextBox*控件) 在页面 (嵌套的*ContentPlaceholder*控件) 中仅有两个深层命名容器, 但最终结果是控件 ID, 如下所示:

[!code-console[Main](overview/samples/sample50.cmd)]

此 ID 在页面中是唯一的, 但在大多数情况下不必要太长。 假设您想要减少呈现的 ID 的长度, 并对生成该 ID 的方式具有更大的控制权。 (例如, 您想要消除 "ctlxxx" 前缀。)实现此目的的最简单方法是设置*ClientIDMode*属性, 如以下示例中所示:

[!code-aspx[Main](overview/samples/sample51.aspx)]

在此示例中, 最外面的*NamingPanel*元素的*ClientIDMode*属性设置为*Static* , 并将内层*NamingControl*元素设置为*可预测*。 这些设置会生成以下标记 (页面的其余部分和母版页假定为与上一示例中的相同):

[!code-html[Main](overview/samples/sample52.html)]

*静态*设置具有重置最外面的*NamingPanel*元素中的任何控件的命名层次结构, 以及从生成的 id 中删除*ContentPlaceHolder*和*MasterPage* id 的效果。 (所呈现元素的*name*属性不受影响, 因此会为事件、视图状态等保留正常的 ASP.NET 功能。)重置命名层次结构的副作用是, 即使将*NamingPanel*元素的标记移到不同的*ContentPlaceholder*控件, 呈现的客户端 id 仍保持不变。

> [!NOTE]
> 请注意, 您需要确保呈现的控件 Id 是唯一的。 如果不是, 则它可能会中断任何需要单独 HTML 元素的唯一 Id 的功能, 如客户端*document.getelementbyid*函数。

#### <a name="creating-predictable-client-ids-in-data-bound-controls"></a>在数据绑定控件中创建可预测的客户端 Id

旧算法为数据绑定列表控件中的控件生成的*ClientID*值可能很长, 而且不是真正可预测的。 *ClientIDMode*功能可帮助你更好地控制如何生成这些 id。

以下示例中的标记包含*ListView*控件:

[!code-aspx[Main](overview/samples/sample53.aspx)]

在上面的示例中, *ClientIDMode*和*RowClientIDRowSuffix*属性在标记中设置。 *ClientIDRowSuffix*属性只能在数据绑定控件中使用, 它的行为因所使用的控件而异。 不同之处如下:

- *GridView*控件-可以指定数据源中的一个或多个列的名称, 这些列在运行时组合在一起以创建客户端 id。 例如, 如果将*RowClientIDRowSuffix*设置为 "ProductName, ProductId", 则呈现元素的控件 id 将具有如下格式:

- [!code-console[Main](overview/samples/sample54.cmd)]

- *ListView*控件-可以指定数据源中追加到客户端 ID 的单个列。 例如, 如果将*ClientIDRowSuffix*设置为 "ProductName", 则呈现的控件 id 的格式将如下所示:

- [!code-console[Main](overview/samples/sample55.cmd)]

- 在这种情况下, 尾随1是从当前数据项的产品 ID 派生的。

- *Repeater*控件—此控件不支持*ClientIDRowSuffix*属性。 在*Repeater*控件中, 使用当前行的索引。 将 ClientIDMode = "可预测" 与*Repeater*控件一起使用时, 将生成具有以下格式的客户端 id:

- [!code-console[Main](overview/samples/sample56.cmd)]

- 尾随0是当前行的索引。

*FormView*和*DetailsView*控件不显示多行, 因此它们不支持*ClientIDRowSuffix*属性。

<a id="0.2__Toc224729038"></a><a id="0.2__Toc253429262"></a><a id="0.2__Toc243304636"></a>

### <a name="persisting-row-selection-in-data-controls"></a>保持数据控件中的行选择

*GridView*和*ListView*控件可以让用户选择行。 在以前版本的 ASP.NET 中, 选择已基于页面上的行索引。 例如, 如果在第1页上选择第三项, 然后移至第2页, 则将选中该页上的第三项。

仅在 .NET Framework 3.5 SP1 中的动态数据项目中最初支持暂留选择。 启用此功能时, 当前所选项将基于项的数据键。 这意味着, 如果您在第1页上选择第三行并移动到第2页, 则第2页上不会选择任何内容。 向后移动到第1页时, 第三行仍处于选中状态。 现在, 所有项目中的*GridView*和*ListView*控件都支持持久化选择, 如以下示例中所示:

[!code-aspx[Main](overview/samples/sample57.aspx)]

<a id="0.2__Toc253429263"></a><a id="0.2__Toc243304637"></a>

### <a name="aspnet-chart-control"></a>ASP.NET 图表控件

ASP.NET*图表*控件展开 .NET Framework 中的数据可视化产品。 使用*图表*控件, 可以创建 ASP.NET 页面, 它们具有直观且引人注目的图表, 可用于复杂的统计或财务分析。 ASP.NET*图表*控件作为 .NET Framework 版本 3.5 SP1 版本的外接程序引入, 并且属于 .NET Framework 4 版本。

控件包含以下功能:

- 35 种不同的图表类型。
- 不限数量的图表区、标题、图例和批注。
- 适用于所有图表元素的各种外观设置。
- 三维支持大多数图表类型。
- 可自动适应数据点的智能数据标签。
- 条带线、刻度分隔线和对数刻度。
- 包含 50 多个用于数据分析和转换的财务和统计公式。
- 简单的图表数据绑定和操作。
- 支持常用数据格式 (如日期、时间和货币)。
- 支持交互和事件驱动的自定义, 包括使用 Ajax 的客户端 click 事件。
- 状态管理。
- 二进制流。

下图显示了 ASP.NET 图表控件生成的财务图表的示例。

<a id="0.2_graphic17"></a>![](overview/_static/image1.png)

图 2：ASP.NET 图表控件示例

有关如何使用 ASP.NET 图表控件的更多示例, 请在 MSDN 网站上的[Microsoft 图表控件的示例环境](https://go.microsoft.com/fwlink/?LinkId=128300)中下载示例代码。 可以在[图表控件论坛](https://go.microsoft.com/fwlink/?LinkId=128713)上找到更多社区内容示例。

#### <a name="adding-the-chart-control-to-an-aspnet-page"></a>向 ASP.NET 页添加图表控件

下面的示例演示如何使用标记将*图表*控件添加到 ASP.NET 页。 在此示例中,*图表*控件为静态数据点生成柱形图。

[!code-aspx[Main](overview/samples/sample58.aspx)]

#### <a name="using-3-d-charts"></a>使用三维图表

*Chart*控件包含*ChartAreas*集合, 该集合可以包含定义图表区特征的*ChartArea*对象。 例如, 若要对图表区使用三维, 请使用*Area3DStyle*属性, 如以下示例中所示:

[!code-aspx[Main](overview/samples/sample59.aspx)]

下图显示了一个三维图表, 其中包含四系列*条形*图类型。

<a id="0.2_graphic18"></a>![](overview/_static/image2.png)

图 3：三维条形图

#### <a name="using-scale-breaks-and-logarithmic-scales"></a>使用刻度分隔线和对数刻度

刻度分隔线和对数刻度是向图表添加复杂的两种附加方法。 这些功能特定于图表区域中的每个轴。 例如, 若要在图表区域的主 Y 轴上使用这些功能, 请在*ChartArea*对象中使用*IsLogarithmic*和*ScaleBreakStyle*属性。 以下代码片段演示如何在主 Y 轴上使用刻度分隔线。

[!code-aspx[Main](overview/samples/sample60.aspx)]

下图显示了启用了刻度分隔线的 Y 轴。

<a id="0.2_graphic19"></a>![](overview/_static/image3.png)

图 4：刻度分隔线

<a id="0.2__QueryExtender"></a><a id="0.2__Toc224729041"></a><a id="0.2__Toc253429264"></a><a id="0.2__Toc243304638"></a>

### <a name="filtering-data-with-the-queryextender-control"></a>用 QueryExtender 控件筛选数据

对于创建数据驱动网页的开发人员而言, 一项非常常见的任务就是筛选数据。 这通常是通过在数据源控件中生成*Where*子句来执行的。 这种方法可能比较复杂, 在某些情况下, *Where*语法不允许你利用基础数据库的全部功能。

为了更轻松地进行筛选, 在 ASP.NET 4 中添加了一个新的*QueryExtender*控件。 此控件可以添加到*EntityDataSource*或*LinqDataSource*控件中, 以便筛选这些控件返回的数据。 由于*QueryExtender*控件依赖于 LINQ, 因此在将数据发送到页面之前, 将在数据库服务器上应用筛选器, 这会产生非常高效的操作。

*QueryExtender*控件支持多种筛选选项。 以下各节介绍了这些选项, 并提供有关如何使用这些选项的示例。

#### <a name="search"></a>搜索

对于 search 选项, *QueryExtender*控件在指定字段中执行搜索。 在下面的示例中, 控件使用在 TextBoxSearch 控件中输入的文本, 并在从*LinqDataSource*控件返回的数据`ProductName`的`Supplier.CompanyName`和列中搜索其内容。

[!code-aspx[Main](overview/samples/sample61.aspx)]

#### <a name="range"></a>范围

范围选项与搜索选项类似, 但指定了一对值来定义范围。 在下面的示例中, *QueryExtender*控件搜索从`UnitPrice` *LinqDataSource*控件返回的数据中的列。 从页面上的 TextBoxFrom 和 TextBoxTo 控件读取范围。

[!code-aspx[Main](overview/samples/sample62.aspx)]

#### <a name="propertyexpression"></a>PropertyExpression

使用 "属性表达式" 选项可以定义与属性值的比较。 如果表达式的计算结果为*true*, 则返回正在检查的数据。 在下面的示例中, *QueryExtender*控件通过将`Discontinued`列中的数据与页面上的 CheckBoxDiscontinued 控件中的值进行比较来筛选数据。

[!code-aspx[Main](overview/samples/sample63.aspx)]

#### <a name="customexpression"></a>CustomExpression

最后, 您可以指定要用于*QueryExtender*控件的自定义表达式。 使用此选项可以在定义自定义筛选器逻辑的页面中调用函数。 下面的示例演示如何以声明方式在*QueryExtender*控件中指定自定义表达式。

[!code-aspx[Main](overview/samples/sample64.aspx)]

下面的示例演示*QueryExtender*控件调用的自定义函数。 在这种情况下, 代码使用 LINQ 查询来筛选数据, 而不是使用包含*Where*子句的数据库查询。

[!code-csharp[Main](overview/samples/sample65.cs)]

这些示例一次只显示一个在*QueryExtender*控件中使用的表达式。 但是, 可以在*QueryExtender*控件内包含多个表达式。

<a id="0.2__Toc253429265"></a><a id="0.2__Toc243304639"></a>

### <a name="html-encoded-code-expressions"></a>Html 编码的代码表达式

某些 ASP.NET 站点 (特别是 ASP.NET MVC) 很大程度上`<%`依赖于使用=  `expression %>`语法 (通常称为 "代码片段") 来向响应中写入一些文本。 使用代码表达式时, 很容易忘记对文本进行 HTML 编码, 如果文本来自用户输入, 则会使页面进入 XSS (跨站点脚本) 攻击。

ASP.NET 4 引入了以下新的代码表达式语法:

[!code-aspx[Main](overview/samples/sample66.aspx)]

此语法在写入响应时默认使用 HTML 编码。 此新表达式有效地转换为以下内容:

[!code-aspx[Main](overview/samples/sample67.aspx)]

例如, &lt;%:Request ["u s"]%&gt;对*request ["u s"]* 的值执行 HTML 编码。

此功能的目的是为了能够将旧语法的所有实例替换为新语法, 以便不会强制决定要使用的每个步骤。 但是, 在某些情况下, 输出文本应为 HTML 或已经过编码, 在这种情况下, 这可能会导致双重编码。

对于这种情况, ASP.NET 4 引入了一个新接口*IHtmlString*, 同时提供了具体的实现*HtmlString*。 通过这些类型的实例, 你可以指示已正确编码 (或以其他方式检查) 返回值以使其显示为 HTML, 因此不应再次对值进行 HTML 编码。 例如, 以下内容不应为 (并且不是) HTML 编码:

[!code-aspx[Main](overview/samples/sample68.aspx)]

ASP.NET MVC 2 helper 方法已更新为使用此新语法, 因此它们不是双精度编码, 而只是在运行 ASP.NET 4 时。 当使用 ASP.NET 3.5 SP1 运行应用程序时, 此新语法不起作用。

请记住, 这不能保证防范 XSS 攻击。 例如, 使用不在引号中的属性值的 HTML 可以包含仍然容易受到攻击的用户输入。 请注意, ASP.NET 控件和 ASP.NET MVC 帮助器的输出始终将属性值包含在引号中, 这是建议的方法。

同样, 此语法不执行 JavaScript 编码, 例如在基于用户输入创建 JavaScript 字符串时。

<a id="0.2__Toc253429266"></a><a id="0.2__Toc243304640"></a>

### <a name="project-template-changes"></a>项目模板更改

在早期版本的 ASP.NET 中, 当你使用 Visual Studio 创建新的网站项目或 web 应用程序项目时, 生成的项目仅包含一个 default.aspx 页、一个默认`Web.config`文件`App_Data`和一个文件夹, 如下所示图

<a id="0.2_graphic1A"></a>![](overview/_static/image4.png)

Visual Studio 还支持空白网站项目类型, 不包含任何文件, 如下图所示:

<a id="0.2_graphic1B"></a>![](overview/_static/image5.png)

结果就是, 对于初学者来说, 如何构建生产型 Web 应用程序非常少。 因此, ASP.NET 4 引入了三个新模板, 一个用于空 Web 应用程序项目, 另一个用于 Web 应用程序和网站项目。

#### <a name="empty-web-application-template"></a>空 Web 应用程序模板

顾名思义, 空 Web 应用程序模板是一种被去除的 Web 应用程序项目。 从 Visual Studio 的 "新建项目" 对话框中选择此项目模板, 如下图所示:

[![](overview/_static/image7.png)](overview/_static/image6.png)

([单击以查看完全大小的映像](overview/_static/image8.png))

创建空的 ASP.NET Web 应用程序时, Visual Studio 会创建以下文件夹布局:

<a id="0.2_graphic1D"></a>![](overview/_static/image9.png)

这类似于早期版本的 ASP.NET 的空白网站布局, 但有一个例外。 在 Visual studio 2010 中, 空 web 应用程序和空网站项目包含以下最`Web.config`小文件, 其中包含 Visual Studio 用于标识项目所针对的框架的信息:

<a id="0.2_graphic1E"></a>![](overview/_static/image10.png)

如果没有此*targetFramework*属性, Visual Studio 默认为面向 .NET Framework 2.0, 以便在打开较旧的应用程序时保持兼容性。

#### <a name="web-application-and-web-site-project-templates"></a>Web 应用程序和网站项目模板

Visual Studio 2010 附带的其他两个新项目模板包含重大更改。 下图显示了在创建新的 Web 应用程序项目时创建的项目布局。 (网站项目的布局几乎完全相同。)

- <a id="0.2_graphic1F"></a>![](overview/_static/image11.png)

项目包含一些在早期版本中未创建的文件。 此外, 新的 Web 应用程序项目配置有基本成员资格功能, 这使你可以快速开始保护新应用程序的访问。 由于此包含, 新项目`Web.config`的文件包含用于配置成员资格、角色和配置文件的项。 下面的示例演示`Web.config`了用于新的 Web 应用程序项目的文件。 (在这种情况下, *roleManager*处于禁用状态。)

[![](overview/_static/image13.png)](overview/_static/image12.png)

([单击以查看完全大小的映像](overview/_static/image14.png))

该项目还包含该`Web.config` `Account`目录中的第二个文件。 第二个配置文件提供了一种方法, 用于保护对非登录用户的 ChangePassword 页的访问。 下面的示例显示了第二个`Web.config`文件的内容。

![](overview/_static/image15.png)

默认情况下, 在新项目模板中创建的页面还包含比早期版本更多的内容。 该项目包含一个默认母版页和 CSS 文件, 默认页 (default.aspx) 默认配置为使用母版页。 结果是, 当你首次运行 Web 应用程序或网站时, 默认的 (home) 页已正常运行。 事实上, 它类似于启动新 MVC 应用程序时看到的默认页面。

[![](overview/_static/image17.png)](overview/_static/image16.png)

([单击以查看完全大小的映像](overview/_static/image18.png))

对项目模板进行这些更改的目的是提供有关如何开始构建新的 Web 应用程序的指导。 使用语义正确、严格符合 XHTML 1.0 的标记和使用 CSS 指定的布局时, 模板中的页表示生成 ASP.NET 4 Web 应用程序的最佳实践。 默认页面还具有两列布局, 你可以轻松地对其进行自定义。

例如, 假设你要为新的 Web 应用程序更改某些颜色, 并插入你的公司徽标来代替我的 ASP.NET 应用程序徽标。 为此, 请在下`Content`创建一个新目录来存储徽标图像:

<a id="0.2_graphic23"></a>![](overview/_static/image19.png)

若要将图像添加到页面, 请打开该`Site.Master`文件, 查找 "我的 ASP.NET" 应用程序文本的定义位置, 并将其替换为一个*图像*元素, 其*src*属性设置为新的徽标图像, 如以下示例中所示:

[![](overview/_static/image21.png)](overview/_static/image20.png)

([单击以查看完全大小的映像](overview/_static/image22.png))

然后, 你可以转到 web.config 文件并修改 CSS 类定义, 以更改页面的背景色以及页眉的背景色。

这些更改的结果是, 可以使用非常少的精力显示自定义主页:

[![](overview/_static/image24.png)](overview/_static/image23.png)

([单击以查看完全大小的映像](overview/_static/image25.png))

<a id="0.2__Toc253429267"></a><a id="0.2__Toc243304641"></a>

### <a name="css-improvements"></a>CSS 改进

ASP.NET 4 中的主要工作区域之一是帮助呈现符合最新 HTML 标准的 HTML。 这包括对 ASP.NET Web 服务器控件使用 CSS 样式的方式的更改。

#### <a name="compatibility-setting-for-rendering"></a>用于呈现的兼容性设置

默认情况下, 如果 Web 应用程序或网站面向 .NET Framework 4, 则*pages*元素的*controlRenderingCompatibilityVersion*属性将设置为 "4.0"。 此元素在计算机级`Web.config`文件中定义, 并且默认适用于所有 ASP.NET 4 应用程序:

[!code-xml[Main](overview/samples/sample69.xml)]

*ControlRenderingCompatibility*的值是一个字符串, 它允许将来的版本中可能出现新版本定义。 在当前版本中, 此属性支持以下值:

- "3.5". 此设置表示旧的呈现和标记。 控件呈现的标记比向后兼容 100%, 并遵循*xhtmlConformance*属性的设置。
- "4.0". 如果属性具有此设置, ASP.NET Web 服务器控件将执行以下操作:
- *XhtmlConformance*属性始终被视为 "Strict"。 因此, 控件呈现 XHTML 1.0 严格标记。
- 禁用非输入控件将不再呈现无效样式。
- 现在, 隐藏字段周围的*div*元素的样式为, 因此它们不会干扰用户创建的 CSS 规则。
- Menu 控件呈现语义正确并符合辅助功能准则的标记。
- 验证控件不呈现内联样式。
- 之前呈现的 border = "0" 的控件 (从 ASP.NET*表*控件派生的控件和 ASP.NET*图像*控件) 不再呈现此特性。

#### <a name="disabling-controls"></a>禁用控件

在 ASP.NET 3.5 SP1 及更早版本中, 框架在 HTML 标记中为其*Enabled*属性设置为*false*的任何控件呈现*已禁用*的特性。 但是, 根据 HTML 4.01 规范, 仅*输入*元素应具有此属性。

在 ASP.NET 4 中, 可以将*controlRenderingCompatibilityVersion*属性设置为 "3.5", 如以下示例中所示:

[!code-xml[Main](overview/samples/sample70.xml)]

您可以为 "*标签*" 控件创建标记, 如下所示, 这将禁用控件:

[!code-aspx[Main](overview/samples/sample71.aspx)]

"*标签*" 控件将呈现以下 HTML:

[!code-html[Main](overview/samples/sample72.html)]

在 ASP.NET 4 中, 可以将*controlRenderingCompatibilityVersion*设置为 "4.0"。 在这种情况下, 当控件的*Enabled*属性设置为*false*时, 只有呈现*输入*元素的控件才会呈现*禁用*的特性。 不呈现 HTML*输入*元素的控件而是呈现一个引用 CSS 类的*类*特性, 你可以使用该 CSS 类定义控件的禁用外观。 例如, 在前面的示例中显示的*标签*控件将生成以下标记:

[!code-html[Main](overview/samples/sample73.html)]

为此控件指定的类的默认值为 "aspNetDisabled"。 但是, 可以通过设置*WebControl*类的静态*DisabledCssClass*静态属性来更改此默认值。 对于控件开发人员, 还可以使用*SupportsDisabledAttribute*属性定义要用于特定控件的行为。

<a id="0.2__Toc253429268"></a><a id="0.2__Toc243304642"></a>

### <a name="hiding-div-elements-around-hidden-fields"></a>在隐藏字段周围隐藏 div 元素

ASP.NET 2.0 和更高版本会在*div*元素中呈现系统特定的隐藏字段 (如用于存储视图状态信息的*隐藏*元素), 以便符合 XHTML 标准。 但是, 当 CSS 规则影响页面上的*div*元素时, 这可能会导致问题。 例如, 它可能会导致在隐藏的*div*元素周围出现一条像素的行。 在 ASP.NET 4 中, 包含由 ASP.NET 生成的隐藏字段的*div*元素添加 CSS 类引用, 如以下示例中所示:

[!code-html[Main](overview/samples/sample74.html)]

然后, 你可以定义仅适用于 ASP.NET 生成的*隐藏*元素的 CSS 类, 如以下示例中所示:

[!code-css[Main](overview/samples/sample75.css)]

<a id="0.2__Toc253429269"></a><a id="0.2__Toc243304643"></a>

### <a name="rendering-an-outer-table-for-templated-controls"></a>为模板化控件呈现外部表

默认情况下, 支持模板的以下 ASP.NET Web 服务器控件将自动包装在用于应用内联样式的外部表中:

- *FormView*
- *Id*
- *PasswordRecovery*
- *ChangePassword*
- *向导*
- *CreateUserWizard*

已将名为*RenderOuterTable*的新属性添加到这些控件, 这些控件允许从标记中删除外部表。 例如, 请看下面的*FormView*控件示例:

[!code-aspx[Main](overview/samples/sample76.aspx)]

此标记将向页面呈现以下输出, 其中包含一个 HTML 表:

[!code-html[Main](overview/samples/sample77.html)]

若要防止呈现表, 可以设置*FormView*控件的*RenderOuterTable*属性, 如以下示例中所示:

[!code-aspx[Main](overview/samples/sample78.aspx)]

前面的示例将呈现以下输出, 而不包含*table*、 *tr*和*td*元素:

> 内容

这种增强功能使你可以更轻松地使用 CSS 设置控件内容的样式, 因为控件不呈现意外标记。

> [!NOTE]
> 请注意, 此更改将禁用对 Visual Studio 2010 设计器中的自动格式化函数的支持, 因为不再有可以承载由自动格式选项生成的样式属性的*table*元素。

<a id="0.2__Toc253429270"></a><a id="0.2__Toc243304644"></a>

### <a name="listview-control-enhancements"></a>ListView 控件增强功能

*ListView*控件已经更易于在 ASP.NET 4 中使用。 早期版本的控件要求您指定一个包含具有已知 ID 的服务器控件的布局模板。 下面的标记显示了如何在 ASP.NET 3.5 中使用*ListView*控件的典型示例。

[!code-aspx[Main](overview/samples/sample79.aspx)]

在 ASP.NET 4 中, *ListView*控件不需要布局模板。 上一示例中所示的标记可以替换为以下标记:

[!code-aspx[Main](overview/samples/sample80.aspx)]

<a id="0.2__Toc253429271"></a><a id="0.2__Toc243304645"></a>

### <a name="checkboxlist-and-radiobuttonlist-control-enhancements"></a>CheckBoxList 和 RadioButtonList 控件增强功能

在 ASP.NET 3.5 中, 可以使用以下两个设置指定*CheckBoxList*和*RadioButtonList*的布局:

- *Flow*。 控件呈现*横跨*元素以包含其内容。
- *表*。 控件呈现一个*表*元素以包含其内容。

下面的示例演示其中每个控件的标记。

[!code-aspx[Main](overview/samples/sample81.aspx)]

默认情况下, 控件呈现的 HTML 类似于以下内容:

[!code-html[Main](overview/samples/sample82.html)]

由于这些控件包含项的列表, 因此为了呈现语义正确的 HTML, 它们应使用 HTML 列表 (*li*) 元素呈现其内容。 这使使用辅助技术阅读网页的用户更容易, 并使控件更易于使用 CSS 进行样式。

在 ASP.NET 4 中, *CheckBoxList*和*RadioButtonList*控件支持*RepeatLayout*属性的以下新值:

- *OrderedList* –内容在*ol*元素内呈现为*li*元素。
- *UnorderedList* –内容呈现为*ul*元素中的*li*元素。

下面的示例演示如何使用这些新值。

[!code-aspx[Main](overview/samples/sample83.aspx)]

上述标记生成以下 HTML:

[!code-html[Main](overview/samples/sample84.html)]

> [!NOTE]
> 注意如果将*RepeatLayout*设置为*OrderedList*或*UnorderedList*, 则不能再使用*RepeatDirection*属性, 如果在标记或代码中设置了该属性, 则会在运行时引发异常。 属性不具有值, 因为这些控件的可视布局是使用 CSS 定义的。

<a id="0.2__Toc253429272"></a><a id="0.2__Toc243304646"></a>

### <a name="menu-control-improvements"></a>菜单控件改进

在 ASP.NET 4 之前, *Menu*控件呈现一系列 HTML 表。 这使得在设置内联属性之外应用 CSS 样式变得更加困难, 也不符合辅助功能标准。

在 ASP.NET 4 中, 控件现在使用由无序列表和列表元素组成的语义标记呈现 HTML。 下面的示例演示了*菜单*控件的 ASP.NET 页中的标记。

[!code-aspx[Main](overview/samples/sample85.aspx)]

页面呈现时, 控件将生成以下 HTML (为清楚起见, 省略了*onclick*代码):

[!code-html[Main](overview/samples/sample86.html)]

除了呈现改进外, 还可以使用焦点管理改进菜单键盘导航。 当*Menu*控件获得焦点时, 可以使用箭头键来浏览元素。 *Menu*控件现在还附加了可访问的丰富 internet 应用程序 (ARIA) 角色和属性 w[翼上的](http://www.w3.org/TR/wai-aria-practices/#menu "菜单 ARIA 指导原则"), 以提高可访问性。

Menu 控件的样式呈现在页面顶部的样式块中, 而不是在包含呈现的 HTML 元素的行中。 如果要对控件的样式进行完全控制, 则可以将新的*IncludeStyleBlock*属性设置为*false*, 在这种情况下, 不会发出样式块。 使用此属性的一种方法是使用 Visual Studio 设计器中的自动格式功能设置菜单的外观。 然后, 可以运行页面, 打开页面源, 然后将呈现的样式块复制到外部 CSS 文件。 在 Visual Studio 中, 撤消样式设置, 并将*IncludeStyleBlock*设置为*false*。 结果就是使用外部样式表中的样式定义了菜单外观。

<a id="0.2__Toc253429273"></a><a id="0.2__Toc243304647"></a>

### <a name="wizard-and-createuserwizard-controls"></a>Wizard 和 CreateUserWizard 控件

ASP.NET*向导*和*CreateUserWizard*控件支持可用于定义其呈现的 HTML 的模板。 (*CreateUserWizard*派生自*向导*。)下面的示例演示完全模板化*CreateUserWizard*控件的标记:

[!code-aspx[Main](overview/samples/sample87.aspx)]

控件呈现的 HTML 类似于以下内容:

[!code-html[Main](overview/samples/sample88.html)]

在 ASP.NET 3.5 SP1 中, 尽管可以更改模板内容, 但仍对*向导*控件的输出具有有限的控制。 在 ASP.NET 4 中, 可以创建*LayoutTemplate*模板并插入*占位符*控件 (使用保留名称) 来指定*向导控件*的呈现方式。 下面的示例演示了这一点:

[!code-aspx[Main](overview/samples/sample89.aspx)]

该示例在*LayoutTemplate*元素中包含以下命名占位符:

- *headerPlaceholder* –在运行时, 这会替换为*system.windows.controls.headereditemscontrol.headertemplate*元素的内容。
- *sideBarPlaceholder* –在运行时, 这会替换为*SideBarTemplate*元素的内容。
- *wizardStepPlaceHolder* –在运行时, 这会替换为*WizardStepTemplate*元素的内容。
- *navigationPlaceholder* –在运行时, 这会替换为你定义的任何导航模板。

使用占位符的示例中的标记会呈现以下 HTML (不包含模板中实际定义的内容):

[!code-html[Main](overview/samples/sample90.html)]

现在, 唯一不是用户定义的 HTML 是*span*元素。 (我们预计在将来的版本中, 甚至不会呈现*span*元素。)现在, 可以完全控制*向导*控件生成的所有内容。

<a id="0.2_dyndata"></a><a id="0.2__Toc253429274"></a><a id="0.2__Toc243304648"></a><a id="0.2__Toc224729042"></a>

## <a name="aspnet-mvc"></a>ASP.NET MVC

ASP.NET MVC 已作为外接程序框架引入到3月2009的 ASP.NET 3.5 SP1。 Visual Studio 2010 包括 ASP.NET MVC 2, 其中包括新特性和功能。

<a id="0.2__Toc253429275"></a>

### <a name="areas-support"></a>区域支持

通过区域, 你可以将控制器和视图分组到大型应用程序中与其他部分的相对隔离的部分。 每个区域均可作为单独的 ASP.NET MVC 项目实现, 然后主应用程序可以引用该项目。 这有助于在构建大型应用程序时管理复杂性, 使多个团队能够在单个应用程序中协同工作。

<a id="0.2__Toc253429276"></a>

### <a name="data-annotation-attribute-validation-support"></a>数据-批注属性验证支持

*DataAnnotations*特性使你可以通过使用元数据特性将验证逻辑附加到模型。 ASP.NET 3.5 SP1 中的 ASP.NET 动态数据引入了*DataAnnotations*属性。 这些属性已集成到默认模型联编程序中, 并提供用于验证用户输入的元数据驱动的方法。

<a id="0.2__Toc253429277"></a>

### <a name="templated-helpers"></a>模板化帮助器

模板化帮助器允许您自动将编辑和显示模板与数据类型相关联。 例如, 您可以使用模板帮助器指定为*system.web*值自动呈现日期选取器 UI 元素。 这类似于 ASP.NET 动态数据中的字段模板。

*Html.editorfor*和*DisplayFor*帮助器方法为呈现标准数据类型以及具有多个属性的复杂对象提供内置支持。 它们还通过让你将数据批注特性 (如*DisplayName*和*ScaffoldColumn* ) 应用于*ViewModel*对象, 从而自定义呈现。

通常需要进一步自定义 UI 帮助器的输出, 并完全控制生成的内容。 *Html.editorfor*和*DisplayFor*帮助器方法使用模板化机制支持此功能, 该机制允许您定义可以重写和控制呈现的输出的外部模板。 可以为类单独呈现模板。

<a id="0.2__Toc253429278"></a><a id="0.2__Toc243304649"></a>

## <a name="dynamic-data"></a>Dynamic Data — 动态数据

动态数据是 .NET Framework 在3.5 年 SP1 版本2008中引入的。 此功能为创建数据驱动的应用程序提供了许多增强功能, 其中包括:

- 用于快速生成数据驱动的网站的 RAD 体验。
- 基于数据模型中定义的约束的自动验证。
- 通过使用动态数据项目中的字段模板, 可以轻松更改为*GridView*和*DetailsView*控件中的字段生成的标记。

> [!NOTE]
> 注意有关详细信息, 请参阅 MSDN Library 中的[动态数据文档](https://msdn.microsoft.com/library/cc488545.aspx)。

对于 ASP.NET 4, 动态数据已得到了增强, 使开发人员能够更轻松地快速生成数据驱动的网站。

<a id="0.2__Toc253429279"></a><a id="0.2__Toc243304650"></a>

### <a name="enabling-dynamic-data-for-existing-projects"></a>为现有项目启用动态数据

.NET Framework 3.5 SP1 随附的动态数据功能引入了以下新功能:

- 字段模板–它们为数据绑定控件提供基于数据类型的模板。 字段模板提供了一种更简单的方法来自定义数据控件的外观, 而不是使用每个字段的模板字段。
- 验证-动态数据允许你使用数据类上的属性为常见方案指定验证, 如必填字段、范围检查、类型检查、使用正则表达式的模式匹配和自定义验证。 验证由数据控件强制执行。

不过, 这些功能具有以下要求:

- 数据访问层必须基于实体框架或 LINQ to SQL。
- 这些功能唯一支持的数据源控件是*EntityDataSource*控件或*LinqDataSource*控件。
- 功能需要使用动态数据创建的 Web 项目或动态数据实体模板, 才能拥有支持该功能所需的所有文件。

ASP.NET 4 中动态数据支持的主要目标是为任何 ASP.NET 应用程序启用动态数据的新功能。 下面的示例演示可以利用现有页面中动态数据功能的控件的标记。

[!code-aspx[Main](overview/samples/sample91.aspx)]

在该页的代码中, 必须添加以下代码才能为这些控件启用动态数据支持:

[!code-csharp[Main](overview/samples/sample92.cs)]

当*GridView*控件处于编辑模式时, 动态数据自动验证输入的数据的格式是否正确。 如果不是, 则显示一条错误消息。

此功能还提供了其他优点, 例如, 能够指定插入模式的默认值。 如果没有动态数据, 若要为字段实现默认值, 则必须附加到事件, 找到控件 (使用*FindControl*), 并设置其值。 在 ASP.NET 4 中, *EnableDynamicData*调用支持第二个参数, 该参数可让你为对象上的任何字段传递默认值, 如以下示例中所示:

[!code-csharp[Main](overview/samples/sample93.cs)]

<a id="0.2__Toc224729043"></a><a id="0.2__Toc253429280"></a><a id="0.2__Toc243304651"></a>

### <a name="declarative-dynamicdatamanager-control-syntax"></a>声明性 DynamicDataManager 控件语法

*DynamicDataManager*控件已增强, 因此你可以通过声明方式配置它, 就像在 ASP.NET 中的大多数控件 (而不只是在代码中) 一样。 *DynamicDataManager*控件的标记类似于以下示例:

[!code-aspx[Main](overview/samples/sample94.aspx)]

此标记为*DynamicDataManager*控件的*先*节中引用的 GridView1 控件启用动态数据行为。

<a id="0.2__Toc224729044"></a><a id="0.2__Toc253429281"></a><a id="0.2__Toc243304652"></a>

### <a name="entity-templates"></a>实体模板

实体模板提供了一种新的方法, 用于自定义数据布局, 而无需创建自定义页面。 页面模板使用*FormView*控件 (而不是在早期版本的动态数据中的页模板中使用的*DetailsView*控件) 和*DynamicEntity*控件来呈现实体模板。 这使您可以更好地控制动态数据呈现的标记。

以下列表显示了包含实体模板的新项目目录布局:

[!code-console[Main](overview/samples/sample95.cmd)]

`EntityTemplate`目录包含用于显示数据模型对象的模板。 默认情况下, 使用`Default.ascx`模板呈现对象, 该模板提供的标记与 ASP.NET 3.5 SP1 中动态数据使用的*DetailsView*控件所创建的标记类似。 下面的示例演示`Default.ascx`控件的标记:

[!code-aspx[Main](overview/samples/sample96.aspx)]

可以编辑默认模板来更改整个站点的外观。 有用于显示、编辑和插入操作的模板。 可以基于数据对象的名称添加新模板, 以更改一种类型的对象的外观。 例如, 你可以添加以下模板:

[!code-console[Main](overview/samples/sample97.cmd)]

该模板可能包含以下标记:

[!code-aspx[Main](overview/samples/sample98.aspx)]

新的实体模板将在页面上通过使用新的*DynamicEntity*控件显示。 在运行时, 此控件将替换为实体模板的内容。 下面的标记显示了使用实体模板的`Detail.aspx`页面模板中的 FormView 控件。 请注意标记中的*DynamicEntity*元素。

[!code-aspx[Main](overview/samples/sample99.aspx)]

<a id="0.2__Toc224729045"></a><a id="0.2__Toc253429282"></a><a id="0.2__Toc243304653"></a>

### <a name="new-field-templates-for-urls-and-email-addresses"></a>Url 和电子邮件地址的新字段模板

ASP.NET 4 引入了两个新的内置字段模板`EmailAddress.ascx`和`Url.ascx`。 这些模板用于标记为*EmailAddress*的字段或包含*DataType*属性的*Url* 。 对于*EmailAddress*对象, 该字段显示为使用*mailto:* 协议创建的超链接。 当用户单击该链接时, 它将打开用户的电子邮件客户端并创建一个主干消息。 类型为*Url*的对象显示为普通超链接。

下面的示例演示如何标记字段。

[!code-csharp[Main](overview/samples/sample100.cs)]

<a id="0.2__Toc224729046"></a><a id="0.2__Toc253429283"></a><a id="0.2__Toc243304654"></a>

### <a name="creating-links-with-the-dynamichyperlink-control"></a>创建带有 DynamicHyperLink 控件的链接

动态数据使用 .NET Framework 3.5 SP1 中添加的新路由功能来控制最终用户访问网站时看到的 Url。 使用新的*DynamicHyperLink*控件可以轻松地生成指向动态数据网站中的页面的链接。 下面的示例演示如何使用*DynamicHyperLink*控件:

[!code-aspx[Main](overview/samples/sample101.aspx)]

此标记创建一个链接, 该链接指向基于`Products` `Global.asax`在文件中定义的路由的表的列表页。 控件将自动使用动态数据页所基于的默认表名称。

<a id="0.2__Toc224729047"></a><a id="0.2__Toc253429284"></a><a id="0.2__Toc243304655"></a>

### <a name="support-for-inheritance-in-the-data-model"></a>数据模型中的继承支持

实体框架和 LINQ to SQL 支持其数据模型中的继承。 这种情况的一个示例可能是包含`InsurancePolicy`表的数据库。 它还可能包含`CarPolicy`和`HousePolicy`表, 这些表`InsurancePolicy`具有与相同的字段, 然后添加更多字段。 已将动态数据修改为理解数据模型中的继承对象, 并支持继承的表的基架。

<a id="0.2__Toc224729048"></a><a id="0.2__Toc253429285"></a><a id="0.2__Toc243304656"></a>

### <a name="support-for-many-to-many-relationships-entity-framework-only"></a>支持多对多关系 (仅实体框架)

实体框架对表之间的多对多关系提供了丰富的支持, 这是通过在*实体*对象上以集合的形式公开关系来实现的。 添加`ManyToMany.ascx`了`ManyToMany_Edit.ascx`新的和字段模板以支持显示和编辑多对多关系中涉及的数据。

<a id="0.2__Toc224729049"></a><a id="0.2__Toc253429286"></a><a id="0.2__Toc243304657"></a>

### <a name="new-attributes-to-control-display-and-support-enumerations"></a>用于控制显示和支持枚举的新属性

添加了*DisplayAttribute* , 使你可以更进一步控制字段的显示方式。 动态数据的早期版本中的*DisplayName*属性允许您更改用作字段标题的名称。 新的*DisplayAttribute*类可用于指定用于显示字段的更多选项, 如字段的显示顺序以及是否将字段用作筛选器。 此属性还提供对*GridView*控件中标签使用的名称的独立控制、 *DetailsView*控件中使用的名称、字段的帮助文本以及用于字段的水印 (如果字段接受文本输入)。

添加了*EnumDataTypeAttribute*类, 以便将字段映射到枚举。 将此特性应用于字段时, 请指定枚举类型。 动态数据使用新`Enumeration.ascx`的字段模板来创建 UI, 以显示和编辑枚举值。 模板将数据库中的值映射到枚举中的名称。

<a id="0.2__Toc224729050"></a><a id="0.2__Toc253429287"></a><a id="0.2__Toc243304658"></a>

### <a name="enhanced-support-for-filters"></a>增强的筛选器支持

动态数据1.0 随内置筛选器提供, 用于布尔列和外键列。 筛选器不允许您指定是否显示这些筛选器或它们的显示顺序。 新的*DisplayAttribute*属性通过提供对列是否显示为筛选器并按其显示顺序进行控制来解决这两个问题。

另外一项增强功能是[为了使用]Web 窗体的新(#0.2__QueryExtender "_QueryExtender")功能, 已经编写了筛选支持。 这样, 便可以创建筛选器, 而无需了解将与筛选器一起使用的数据源控件。 除了这些扩展外, 筛选器也已转换为模板控件, 使您可以添加新筛选器。 最后, 前面提到的*DisplayAttribute*类允许重写默认筛选器, 其方式与*UIHint*允许重写列的默认字段模板的方式相同。

<a id="0.2__Toc224729051"></a><a id="0.2__Toc253429288"></a><a id="0.2__Toc243304659"></a>

## <a name="visual-studio-2010-web-development-improvements"></a>Visual Studio 2010 Web 开发改进

Visual Studio 2010 中的 Web 开发已得到增强, 以实现更好的 CSS 兼容性, 更高的效率, 通过 HTML 和 ASP.NET 的标记段和新的动态 IntelliSense JavaScript 提高。

<a id="0.2__Toc224729052"></a><a id="0.2__Toc253429289"></a><a id="0.2__Toc243304660"></a>

### <a name="improved-css-compatibility"></a>提高了 CSS 兼容性

Visual Studio 2010 中的 Visual Web Developer 设计器已更新, 以提高 CSS 2.1 标准的符合性。 设计器更好地保留了 HTML 源的完整性, 比早期版本的 Visual Studio 更可靠。 此外, 还制定了体系结构改进功能, 使其能够更好地实现呈现、布局和可维护性。

<a id="0.2__Toc224729053"></a><a id="0.2__Toc253429290"></a><a id="0.2__Toc243304661"></a>

### <a name="html-and-javascript-snippets"></a>HTML 和 JavaScript 代码段

在 HTML 编辑器中, IntelliSense 自动完成标记名。 IntelliSense 代码段功能自动完成整个标记等。 在 Visual Studio 2010 中, 在 Visual Studio 早期版本中受C#支持的 JavaScript、和 Visual Basic 支持 IntelliSense 代码片段。

Visual Studio 2010 包括超过200的代码段, 可帮助你自动完成常见的 ASP.NET 和 HTML 标记, 包括必需的属性 (如 runat = "server") 以及特定于标记的公共属性 (例如*ID*、 *DataSourceID* *)ControlToValidate*和*文本*)。

您可以下载其他代码段, 也可以编写自己的代码片段, 以封装您或您的团队用于常见任务的标记块。

<a id="0.2__Toc224729054"></a><a id="0.2__Toc253429291"></a><a id="0.2__Toc243304662"></a>

### <a name="javascript-intellisense-enhancements"></a>JavaScript IntelliSense 增强功能

在 Visual 2010 中, JavaScript IntelliSense 经过了重新设计, 以提供更丰富的编辑体验。 IntelliSense 现在可识别由方法 (如*registerNamespace* ) 和其他 JavaScript 框架使用的类似技术动态生成的对象。 提高了性能, 以便分析较大的脚本库, 并显示 IntelliSense, 只需很少或没有处理延迟。 为了支持几乎所有第三方库和支持各种编码样式, 兼容性已大幅增加。 文档注释现在会在你键入时进行分析, 并将立即由 IntelliSense 使用。

<a id="0.2__Toc224729055"></a><a id="0.2__Toc253429292"></a><a id="0.2__Toc243304663"></a>

## <a name="web-application-deployment-with-visual-studio-2010"></a>用 Visual Studio 2010 部署 Web 应用程序

当 ASP.NET 开发人员部署 Web 应用程序时, 他们通常会发现他们遇到如下问题:

- 部署到共享宿主站点需要诸如 FTP 等技术, 这可能会很慢。 此外, 您必须手动执行一些任务, 如运行 SQL 脚本来配置数据库, 您必须更改 IIS 设置, 如将虚拟目录文件夹配置为应用程序。
- 在企业环境中, 除了部署 Web 应用程序文件之外, 管理员经常必须修改 ASP.NET 配置文件和 IIS 设置。 数据库管理员必须运行一系列 SQL 脚本来使应用程序数据库运行。 此类安装非常耗费人力, 通常需要几小时才能完成, 并且必须仔细记录。

Visual Studio 2010 包括的技术可解决这些问题, 并使你能够无缝部署 Web 应用程序。 其中一种技术是 IIS Web 部署工具 (Msdeploy.exe)。

Visual Studio 2010 中的 Web 部署功能包括以下主要方面:

- Web 打包
- Web.config 转换
- 数据库部署
- Web 应用程序一键式发布

以下各节提供了有关这些功能的详细信息。

<a id="0.2__Toc224729056"></a><a id="0.2__Toc253429293"></a><a id="0.2__Toc243304664"></a>

### <a name="web-packaging"></a>Web 打包

Visual Studio 2010 使用 Msdeploy.exe 工具为应用程序创建压缩 (.zip) 文件, 该文件称为*Web 包*。 包文件包含有关应用程序的元数据以及以下内容:

- IIS 设置, 其中包括应用程序池设置、错误页设置等。
- 实际的 Web 内容, 其中包括网页、用户控件、静态内容 (图像和 HTML 文件) 等。
- SQL Server 数据库架构和数据。
- 安全证书、要在 GAC 中安装的组件、注册表设置等。

Web 包可以复制到任何服务器, 然后使用 IIS 管理器手动安装。 或者, 对于自动部署, 可以使用命令行命令或使用部署 Api 来安装包。

Visual Studio 2010 提供内置的 MSBuild 任务和目标, 以创建 Web 包。 有关详细信息, 请参阅 MSDN 网站上的[ASP.NET Web 应用程序项目部署概述](https://msdn.microsoft.com/library/dd394698%28VS.100%29.aspx)和 Vishal Joshi 的博客上[创建 web 包的10多个原因](http://vishaljoshi.blogspot.com/2009/07/10-20-reasons-why-you-should-create-web.html)。

<a id="0.2__Toc224729057"></a><a id="0.2__Toc253429294"></a><a id="0.2__Toc243304665"></a>

### <a name="webconfig-transformation"></a>Web.config 转换

对于 Web 应用程序部署, Visual Studio 2010 引入了[XML 文档转换 (XDT)](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html), 这是一项功能, 可`Web.config`用于将文件从开发设置转换为生产设置。 转换设置是在名为`web.debug.config`、 `web.release.config`等的转换文件中指定的。 (这些文件的名称与 MSBuild 配置匹配。)转换文件只包含需要对已部署`Web.config`文件进行的更改。 使用简单语法指定更改。

下面的示例显示了`web.release.config`文件的一部分, 在部署发布配置时可能会生成该文件的一部分。 示例中的 Replace 关键字指定在部署过程中, `Web.config`文件中的 connectionString 节点将替换为示例中列出的值。

[!code-xml[Main](overview/samples/sample102.xml)]

有关详细信息, 请参阅 MSDN <a id="0.2_a"></a>网站和[web 部署上的 web[应用程序项目部署的 web.config 转换语法](https://msdn.microsoft.com/library/dd465326%28VS.100%29.aspx):Vishal Joshi 的博客](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html)上的 web.config 转换。

<a id="0.2__Toc224729058"></a><a id="0.2__Toc253429295"></a><a id="0.2__Toc243304666"></a>

### <a name="database-deployment"></a>数据库部署

Visual Studio 2010 部署包可以包含对 SQL Server 数据库的依赖关系。 作为包定义的一部分, 你需要为源数据库提供连接字符串。 当你创建 Web 包时, Visual Studio 2010 将为数据库架构创建 SQL 脚本, 并根据需要为数据创建 SQL 脚本, 然后将这些脚本添加到包中。 你还可以提供自定义 SQL 脚本, 并指定它们应在服务器上运行的顺序。 在部署时, 提供适用于目标服务器的连接字符串;然后, 部署过程使用此连接字符串运行创建数据库架构并添加数据的脚本。

此外, 通过使用一键式发布, 可以配置部署, 以便在将应用程序发布到远程共享宿主站点时直接发布数据库。 有关详细信息，请参阅[如何：使用 MSDN 网站上的 web 应用程序](https://msdn.microsoft.com/library/dd465343%28VS.100%29.aspx)项目和 Vishal Joshi 的博客上的[VS 2010](http://vishaljoshi.blogspot.com/2009/03/web-deployment-webconfig-transformation_23.html) , 部署数据库。

<a id="0.2__Toc224729059"></a><a id="0.2__Toc253429296"></a><a id="0.2__Toc243304667"></a>

### <a name="one-click-publish-for-web-applications"></a>Web 应用程序一键式发布

通过 Visual Studio 2010, 你还可以使用 IIS 远程管理服务将 Web 应用程序发布到远程服务器。 你可以为托管帐户创建发布配置文件, 或者为测试服务器或临时服务器创建发布配置文件。 每个配置文件可以安全地保存适当的凭据。 然后, 你可以通过使用 Web 一键式发布工具栏, 只需要一次单击即可将其部署到任何目标服务器。 使用 Visual Studio 2010, 还可以使用 MSBuild 命令行进行发布。 这使您可以将您的团队生成环境配置为在持续集成模型中包含发布。

有关详细信息，请参阅[如何：在 MSDN 网站上使用一键式发布和 Web 部署](https://msdn.microsoft.com/library/dd465337%28VS.100%29.aspx)部署 web 应用程序项目, 并在 Vishal Joshi 的博客上使用[VS 2010 单击 "发布](http://vishaljoshi.blogspot.com/2009/05/web-1-click-publish-with-vs-2010.html)"。 若要查看有关 Visual Studio 2010 中 Web 应用程序部署的视频演示, 请参阅 Vishal Joshi 的博客上[的 VS 2010 For Web Developer](http://vishaljoshi.blogspot.com/2008/12/vs-2010-for-web-developer-previews.html) preview。

<a id="0.2__Toc224729060"></a><a id="0.2__Toc253429297"></a><a id="0.2__Toc243304668"></a>

### <a name="resources"></a>资源

以下网站提供了有关 ASP.NET 4 和 Visual Studio 2010 的其他信息。

- [ASP.NET 4](https://msdn.microsoft.com/library/ee532866%28VS.100%29.aspx) -MSDN 网站上的 ASP.NET 4 的官方文档。
- [https://www.asp.net/](https://www.asp.net/)— ASP.NET 团队自己的网站。
- [https://www.asp.net/dynamicdata/](https://msdn.microsoft.com/library/cc488545.aspx)[ASP.NET 动态数据内容地图](https://msdn.microsoft.com/library/cc488545%28VS.100%29.aspx)-ASP.NET 团队网站和 ASP.NET 动态数据的官方文档中的联机资源。
- [https://www.asp.net/ajax/](../../ajax/index.md)-ASP.NET Ajax 开发的主要 Web 资源。
- [https://blogs.msdn.com/webdevtools/](https://blogs.msdn.com/webdevtools/)-Visual Web Developer 团队博客, 其中包含有关 Visual Studio 2010 中的功能的信息。
- [ASP.NET WebStack](https://github.com/aspnet/AspNetWebStack) -ASP.NET 的预览版本的主要 Web 资源。

<a id="0.2__Toc224729061"></a><a id="0.2__Toc253429298"></a><a id="0.2__Toc243304669"></a>

## <a name="disclaimer"></a>免责声明

这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。

本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。 由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。

本白皮书仅用于提供信息。 MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。

遵守所有适用的著作权法是用户的责任。 未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。

对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。 除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。

除非另有说明, 否则本示例中描述的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点和事件均属虚构, 与任何真实的公司、组织、产品、域名、电子邮件关联应推断地址、徽标、人物、地点或事件。

© 2009 Microsoft Corporation. 保留所有权利。

Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。

此处提到的真实公司和产品的名称可能是其各自所有者的商标。
