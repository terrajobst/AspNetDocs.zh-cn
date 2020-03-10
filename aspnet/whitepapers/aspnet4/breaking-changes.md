---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 重大更改 |Microsoft Docs
author: rick-anderson
description: 本文档介绍了对 .NET Framework 版本4版本进行的更改，这些更改可能会影响使用 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 8ccad3b40a723c92a3164de082e1f94577141008
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439508"
---
# <a name="aspnet-4-breaking-changes"></a>ASP.NET 4 重大更改

> 本文档介绍了对 .NET Framework 版本4版本进行的更改，这些更改可能会影响使用早期版本（包括 ASP.NET 4 Beta 1 和 Beta 2 版）创建的应用程序。
> 
> [下载此白皮书](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)

<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a>内容

[Web.config 文件中的 ControlRenderingCompatibilityVersion 设置](#0.1__Toc256770141 "_Toc256770141")  
[ClientIDMode 更改](#0.1__Toc256770142 "_Toc256770142")  
[Server.htmlencode 和 UrlEncode 现在对单引号进行编码](#0.1__Toc256770143 "_Toc256770143")  
[ASP.NET 页（.aspx）分析器更严格](#0.1__Toc256770144 "_Toc256770144")  
[已更新浏览器定义文件](#0.1__Toc256770145 "_Toc256770145")  
[从根 Web 配置文件中删除了 system.web. .dll](#0.1__Toc256770146 "_Toc256770146")  
[ASP.NET 请求验证](#0.1__Toc256770147 "_Toc256770147")  
[默认哈希算法现在为 HMACSHA256](#0.1__Toc256770148 "_Toc256770148")  
[与新的 ASP.NET 4 根配置相关的配置错误](#0.1__Toc256770149 "_Toc256770149")  
[ASP.NET 4 子应用程序在 ASP.NET 2.0 或 ASP.NET 3.5 应用程序下无法启动](#0.1__Toc256770150 "_Toc256770150")  
[ASP.NET 4 网站无法在安装了 SharePoint 的计算机上启动](#0.1__Toc256770151 "_Toc256770151")  
[HttpRequest 属性不再包括 PathInfo 值](#0.1__Toc256770152 "_Toc256770152")  
[ASP.NET 2.0 应用程序可能生成引用 eurl 的 HttpException 错误](#0.1__Toc256770153 "_Toc256770153")  
[IIS 7 或 IIS 7.5 集成模式下的默认文档中可能不会引发事件处理程序](#0.1__Toc256770154 "_Toc256770154")  
[对 ASP.NET 代码访问安全性（CAS）实现的更改](#0.1__Toc256770155 "_Toc256770155")  
[MembershipUser 命名空间中的其他类型已移动](#0.1__Toc256770156 "_Toc256770156")  
[\* HTTP 标头变化的输出缓存更改](#0.1__Toc256770157 "_Toc256770157")  
[Passport 的安全类型已过时](#0.1__Toc256770158 "_Toc256770158")  
[PopOutImageUrl 属性未能呈现 ASP.NET 4 中的图像](#0.1__Toc256770159 "_Toc256770159")  
[当路径包含反斜杠时，StaticPopOutImageUrl 和 DynamicPopOutImageUrl 无法呈现图像](#0.1__Toc256770160 "_Toc256770160")  
[否认](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a>Web.config 文件中的 ControlRenderingCompatibilityVersion 设置

.NET Framework 版本4中修改了 ASP.NET 控件，以便更准确地指定它们呈现标记的方式。 在以前版本的 .NET Framework 中，某些控件发出了你无法禁用的标记。 默认情况下，ASP.NET 4 不再生成这种类型的标记。

如果使用 Visual Studio 2010 从 ASP.NET 2.0 或 ASP.NET 3.5 升级应用程序，则该工具会自动将设置添加到保留旧呈现的 `Web.config` 文件中。 但是，如果通过在 IIS 中将应用程序池更改为面向 .NET Framework 4 来升级应用程序，ASP.NET 默认使用新的呈现模式。 若要禁用新的呈现模式，请在 `Web.config` 文件中添加以下设置：

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

新行为带来的主要呈现变化如下：

- **Image**和**ImageButton**控件不再呈现 `border="0"` 特性。
- 默认情况下，从派生的**BaseValidator**类和验证控件不再呈现红色文本。
- **HtmlForm**控件不呈现**name**特性。
- **Table**控件不再呈现 `border="0"` 特性。
- 如果控件的**Enabled**属性设置为**false** （或从容器控件继承此设置），则不是为用户输入（例如**标签**控件）设计的控件将不再呈现 `disabled="disabled"` 特性。

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a>ClientIDMode 更改

通过 ASP.NET 4 中的**ClientIDMode**设置，你可以指定 ASP.NET 生成 HTML 元素的**id**属性的方式。 在以前版本的 ASP.NET 中，默认行为等效于**ClientIDMode**的**AutoID**设置。 但是，默认设置现在是**可预测**的。

如果你使用 Visual Studio 2010 从 ASP.NET 2.0 或 ASP.NET 3.5 升级应用程序，则该工具会自动将设置添加到 `Web.config` 文件中，该文件保留 .NET Framework 早期版本的行为。 但是，如果通过在 IIS 中将应用程序池更改为面向 .NET Framework 4 来升级应用程序，ASP.NET 默认使用新的模式。 若要禁用新的客户端 ID 模式，请在 `Web.config` 文件中添加以下设置：

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a>Server.htmlencode 和 UrlEncode 现在对单引号进行编码

在 ASP.NET 4 中， **httputility.javascriptstringencode**和**HttpServerUtility**类的**server.htmlencode**和**UrlEncode**方法已更新，以对单引号字符（'）进行编码，如下所示：

- **Server.htmlencode**方法将单引号的实例编码为 "。
- **UrlEncode**方法将单引号的实例编码为 %27。

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a>ASP.NET 页（.aspx）分析器更严格

ASP.NET 页（`.aspx` 文件）和用户控件（`.ascx` 文件）的页分析器在 ASP.NET 4 中更严格，并将拒绝无效标记的更多实例。 例如，以下两个代码段将在早期版本的 ASP.NET 中成功进行分析，但现在会在 ASP.NET 4 中引发分析器错误。

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

请注意**HiddenField**标记结尾的无效分号。

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

请注意，在**CssClass**属性中运行的未闭合**样式**特性。

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a>已更新浏览器定义文件

浏览器定义文件已更新，以包括有关新的和已更新的浏览器和设备的信息。 旧式浏览器和设备（如 Netscape Navigator）已被删除，并且已添加更新的浏览器和设备（如 Google Chrome 和 Apple iPhone）。

如果应用程序包含的自定义浏览器定义继承自一个已删除的浏览器定义，将会出现错误。 例如，如果 `App_Browsers` 文件夹中包含继承自 IE2 浏览器定义的浏览器定义，则你将收到以下配置错误消息：

- 找不到 ID 为 "IE2" 的浏览器或网关元素。

> [!NOTE]
> **HttpBrowserCapabilities**对象（由页面的**Request**属性公开）由浏览器定义文件驱动。 因此，通过在 ASP.NET 4 中访问此对象的属性返回的信息可能与早期版本的 ASP.NET 中返回的信息不同。

可以通过从以下文件夹复制浏览器定义文件来恢复到旧的浏览器定义文件：

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

将文件复制到 ASP.NET 4 的相应 `\CONFIG\Browsers` 文件夹中。 复制文件后，请运行 Aspnet\_regbrowsers 命令行工具。

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a>从根 Web 配置文件中删除了 system.web. .dll

在以前版本的 ASP.NET 中，对 System.web 程序集的引用包含在下的**程序集**部分的根 `Web.config` 文件中。 为了提高性能，已删除对此程序集的引用。

ASP.NET 4 中包括了 System.web .dll 程序集，但该程序集已弃用。 如果要使用 System.web 程序集的类型，请将对此程序集的引用添加到根 `Web.config` 文件或应用程序 `Web.config` 文件中。 例如，如果要使用任何（弃用的） ASP.NET 移动控件，则必须将对 System.web 程序集的引用添加到 `Web.config` 文件中。

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a>ASP.NET 请求验证

ASP.NET 中的请求验证功能针对跨站点脚本（XSS）攻击提供一定程度的默认保护。 在以前版本的 ASP.NET 中，默认情况下已启用请求验证。 但是，它仅应用于 ASP.NET 页（`.aspx` 文件和它们的类文件），并且仅适用于这些页的执行时间。

默认情况下，在 ASP.NET 4 中，为所有请求启用了请求验证，因为在 HTTP 请求的**BeginRequest**阶段之前启用了请求验证。 因此，请求验证适用于对所有 ASP.NET 资源的请求，而不只是 .aspx 页面请求。 这包括诸如 Web 服务调用和自定义 HTTP 处理程序之类的请求。 当自定义 HTTP 模块读取 HTTP 请求的内容时，请求验证也处于活动状态。

因此，对于之前未触发错误的请求，此时可能会发生请求验证错误。 若要恢复到 ASP.NET 2.0 请求验证功能的行为，请在 `Web.config` 文件中添加以下设置：

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

但是，我们建议你分析任何请求验证错误，以确定现有处理程序、模块或其他自定义代码是否访问可能是 XSS 攻击向量的可能不安全的 HTTP 输入。

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a>默认哈希算法现在为 HMACSHA256

ASP.NET 使用加密算法和哈希算法来帮助保护数据（如窗体身份验证 Cookie 和视图状态）。 默认情况下，ASP.NET 4 现在使用 HMACSHA256 算法对 cookie 和视图状态进行哈希操作。 早期版本的 ASP.NET 使用了较旧的 HMACSHA1 算法。

如果运行混合 ASP.NET 2.0/ASP，应用程序可能会受到影响。 NET 4 环境，其中的数据（如 forms 身份验证 cookie）必须在 across.NET Framework 版本中工作。 若要将 ASP.NET 4 Web 应用程序配置为使用较旧的 HMACSHA1 算法，请在 `Web.config` 文件中添加以下设置：

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a>与新的 ASP.NET 4 根配置相关的配置错误

已更新 .NET Framework 4 （因此 ASP.NET 4）的根配置文件（`machine.config` 文件和根 `Web.config` 文件），以包含3.5 在应用程序 `Web.config` 文件中找到的大多数样本配置信息。 由于托管 IIS 7 和 IIS 7.5 配置系统的复杂性，在 ASP.NET 4 和 iis 7 和 IIS 7.5 下运行 ASP.NET 3.5 应用程序可能会导致 ASP.NET 或 IIS 配置错误。

如果可行，建议使用 Visual Studio 2010 中的项目升级工具将 ASP.NET 3.5 应用程序升级到 ASP.NET 4。 Visual Studio 2010 自动修改 ASP.NET 3.5 应用程序的 `Web.config` 文件，使其包含 ASP.NET 4 的相应设置。

但是，在不重新编译的情况下，使用 .NET Framework 4 运行 ASP.NET 3.5 应用程序是受支持的方案。 在这种情况下，你可能必须先手动修改应用程序的 `Web.config` 文件，然后才能在 .NET Framework 4 和 IIS 7 或 IIS 7.5 下运行该应用程序。

接下来的两部分介绍了你可能需要对不同软件组合做出的更改。

**Windows Vista SP1 或 Windows Server 2008 SP1，其中不安装修补程序 KB958854 和 SP2。** 在此配置中，IIS 7 配置系统会将应用程序级 `Web.config` 文件与 ASP.NET 2.0 `machine.config` 文件进行比较，从而错误地合并应用程序的托管配置。 因此，.NET Framework 3.5 或更高版本中的应用程序级 `Web.config` 文件必须具有一个**system.web. extension**配置节定义（元素），以便不会导致 IIS 7 验证失败。

但是，手动修改的应用程序级 `Web.config` 文件项与 Visual Studio 2008 中引入的原始样本配置节定义不完全匹配，将导致 ASP.NET 配置错误。 （Visual Studio 2008 生成的默认配置项工作正常。）一个常见的问题是，手动修改 `Web.config` 文件会遗漏在各种配置节定义中找到的**allowDefinition**和**requirePermission**配置属性。 这会导致应用程序级别 `Web.config` 文件中的缩写配置节和 ASP.NET 4 `machine.config` 文件中的完整定义不匹配。 因此，在运行时，ASP.NET 4 配置系统将引发配置错误。

**Windows Vista SP2、Windows Server 2008 SP2、Windows 7、Windows Server 2008 R2，以及安装了修补程序 KB958854 的 Windows Vista SP1 和 Windows Server 2008 SP1。**

在这种情况下，IIS 7 和 IIS 7.5 本机配置系统返回配置错误，因为它对为托管配置节处理程序定义的**类型**属性执行文本比较。 由于 Visual Studio 2008 和 Visual Studio 2008 SP1 生成的所有 `Web.config` 文件在系统的类型字符串中都有 "3.5"。由于在同一配置节处理程序的类型属性中，ASP.NET 4 `machine.config` 文件中有 "4.0"，在 Visual Studio 2008 或 Visual Studio 2008 SP1 中生成的应用程序在 IIS 7 和 IIS 7.5 中始终无法进行配置验证，因此， **web extensions** （及相关）配置节处理程序以及这**种**配置节处理程序和。

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a>解决这些问题

第一种情况的解决方法是通过将样本配置文本包含在 Visual Studio 2008 自动生成的 `Web.config` 文件中，来更新应用程序级别的 `Web.config` 文件。

第一种方案的另一种解决方法是在您的计算机上安装适用于 Vista 或 Windows Server 2008 的 Service Pack 2，或者安装修补程序 KB958854 （[https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)）来修复 IIS 配置系统的错误配置-合并行为。 但是，在执行上述任一操作后，你的应用程序可能会遇到配置错误，因为第二个方案中描述的问题。

第二种方案的解决方法是从应用程序级 `Web.config` 文件中删除或注释掉所有**system.web. extensions**配置节定义和配置节组定义。 这些定义通常位于应用程序级别 `Web.config` 文件的顶部，可由**configSections**元素及其子元素标识。

对于这两种方案，建议你也手动删除**system.object**部分，尽管这不是必需的。

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a>ASP.NET 4 子应用程序在 ASP.NET 2.0 或 ASP.NET 3.5 应用程序下无法启动

由于配置或编译错误，配置为运行 ASP.NET 早期版本的应用程序子级的 ASP.NET 4 应用程序可能无法启动。 下面的示例显示受影响的应用程序的目录结构。

`/parentwebapp` （配置为使用 ASP.NET 2.0 或 ASP.NET 3.5）  
`/childwebapp` （配置为使用 ASP.NET 4）

`childwebapp` 文件夹中的应用程序将无法在 IIS 7 或 IIS 7.5 上启动，并将报告配置错误。 错误文本将包含类似于下面的消息：

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

在 IIS 6 上，`childwebapp` 文件夹中的应用程序也将无法启动，但会报告其他错误。 例如，错误文本可能会声明以下内容：

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

之所以出现这种情况，是因为 `parentwebapp` 文件夹中的父应用程序的配置信息是配置信息层次结构的一部分，这些配置信息确定子 web 应用程序在 `childwebapp` 文件夹中所使用的最终合并配置设置。 根据 ASP.NET 4 Web 应用程序是在 IIS 7.5 7 上运行还是在 iis 6 上运行，IIS 配置系统或 ASP.NET 4 编译系统都将返回错误。

解决此问题并使子 ASP.NET 4 应用程序工作所必须遵循的步骤取决于 ASP.NET 4 应用程序是在 IIS 6 上运行还是在 IIS 7 上运行（或 IIS 7.5）。

### <a name="step-1-iis-7-or-iis-75-only"></a>步骤1（仅限 IIS 7 或 IIS 7.5）

此步骤仅在运行 IIS 7 或 IIS 7.5 的操作系统（包括 Windows Vista、Windows Server 2008、Windows 7 和 Windows Server 2008 R2）上是必需的。

将父应用程序（运行 ASP.NET 2.0 或 ASP.NET 3.5）的 `Web.config` 文件中的**configSections**定义移动到 the.NET Framework 2.0 的根 `Web.config` 文件中。 当**configSections**元素合并配置文件的层次结构时，iis 7 和 iis 7.5 本机配置系统会对其进行扫描。 将**configSections**定义从父 Web 应用程序的 `Web.config` 文件移到根 `Web.config` 文件，可以有效地隐藏为子 ASP.NET 4 应用程序发生的配置合并过程中的元素。

在32位操作系统或32位应用程序池上，ASP.NET 2.0 和 ASP.NET 3.5 的根 `Web.config` 文件通常位于以下文件夹中：

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

在64位操作系统或64位应用程序池上，ASP.NET 2.0 和 ASP.NET 3.5 的根 `Web.config` 文件通常位于以下文件夹中：

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

如果在64位计算机上同时运行32位和64位 Web 应用程序，则必须将**configSections**元素向上移动到32和64位系统的根 `Web.config` 文件中。

将**configSections**元素放在根 `Web.config` 文件中后，立即将该节粘贴到**configuration**元素之后。 下面的示例显示了在完成移动元素后，根 `Web.config` 文件的顶层内容应如下所示。

> [!NOTE]
> 在下面的示例中，已换行以方便阅读。

[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a>步骤2（所有版本的 IIS）

无论 ASP.NET 4 子 Web 应用程序是在 IIS 6 上运行还是在 IIS 7 上运行（或 IIS 7.5），都需要执行此步骤。

在运行 ASP.NET 2 或 ASP.NET 3.5 的父 Web 应用程序的 `Web.config` 文件中，添加一个**位置**标记，该标记显式指定（适用于 IIS 和 ASP.NET 配置系统），而这些配置项仅适用于父 web 应用程序。 下面的示例显示要添加的**location**元素的语法：

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

下面的示例演示如何使用**location**标记来包装从**appSettings**部分开始、以**system.webserver**节结尾的所有配置节。

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

完成步骤1和步骤2后，子 ASP.NET 4 Web 应用程序将会启动且不会出错。

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a>ASP.NET 4 网站无法在安装了 SharePoint 的计算机上启动

运行 SharePoint 的 Web 服务器具有一个在 SharePoint 网站的根目录（例如，默认网站 `c:\inetpub\wwwroot\web.config`）下部署的 `Web.config` 文件。 在此 `Web.config` 文件中，SharePoint 会将名为 WSS\_的自定义部分信任级别设置为 "最小"。

如果尝试运行部署为此类 SharePoint 网站的子网站的 ASP.NET 4 网站，将看到以下错误：

`Could not find permission set named 'ASP.NET'.`

发生此错误的原因是 ASP.NET 4 代码访问安全性（CAS）基础结构查找名为 ASP.NET 的权限集。 但是，WSS\_所引用的部分信任配置文件不包含具有该名称的任何权限集。

当前没有可与 ASP.NET 兼容的 SharePoint 版本。 因此，不应尝试将 ASP.NET 4 网站作为子站点运行在 SharePoint 网站下。

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a>HttpRequest 属性不再包括 PathInfo 值

以前版本的 ASP.NET 在从与文件路径相关的各种属性返回的值（包括**HttpRequest**、 **HttpRequest** **和 AppRelativeCurrentExecutionFilePath）** 中包含**PathInfo**值。 ASP.NET 4 不再包含这些属性返回值中的**PathInfo**值。 相反， **PathInfo**信息可在**HttpRequest**中找到。 例如，假定以下 URL 片段：

`/testapp/Action.mvc/SomeAction`

在早期版本的 ASP.NET 中， **HttpRequest**属性具有以下值：

**HttpRequest**： `/testapp/Action.mvc/SomeAction`

**HttpRequest. PathInfo**：（空）

在 ASP.NET 4 中， **HttpRequest**属性改为具有以下值：

**HttpRequest**： `/testapp/Action.mvc`

**HttpRequest. PathInfo**： `SomeAction`

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a>ASP.NET 2.0 应用程序可能生成引用 eurl 的 HttpException 错误

在 IIS 6 上启用 ASP.NET 4 后，IIS 6 上运行的 ASP.NET 2.0 应用（在 Windows Server 2003 或 Windows Server 2003 R2 中）可能会生成错误，如下所示：

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

之所以发生此错误，是因为当 ASP.NET 检测到网站配置为使用 ASP.NET 4 时，ASP.NET 4 的本机组件会将无扩展名 URL 传递到 ASP.NET 的托管部分，以便进一步处理。 但是，如果将 ASP.NET 4 网站下的虚拟目录配置为使用 ASP.NET 2.0，则以这种方式处理无扩展名 URL 会导致修改的 URL 包含字符串 "eurl"。 然后，将此修改后的 URL 发送到 ASP.NET 2.0 应用程序。 ASP.NET 2.0 无法识别 "eurl" 格式。 因此，ASP.NET 2.0 将尝试查找名为 `eurl.axd` 的文件并执行它。 由于不存在此类文件，请求会失败，并出现**HttpException**异常。

可以使用以下选项之一解决此问题。

### <a name="option-1"></a>选项 1

如果运行该网站不需要 ASP.NET 4，请重新映射该网站以改用 ASP.NET 2.0。

### <a name="option-2"></a>方法 2

如果需要 ASP.NET 4 才能运行该网站，请将所有子 ASP.NET 2.0 虚拟目录移动到映射到 ASP.NET 2.0 的其他网站。

### <a name="option-3"></a>选项3

如果无法将网站重新映射到 ASP.NET 2.0 或更改虚拟目录的位置，请在 ASP.NET 4 中显式禁用无扩展名 URL 处理。 请按以下过程操作：

1. 在 Windows 注册表中，打开以下节点：

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. 创建名为**EnableExtensionlessUrls**的新**DWORD**值。
2. 将**EnableExtensionlessUrls**设置为0。 这将禁用无扩展名 URL 行为。
3. 保存注册表值并关闭注册表编辑器。
4. 运行**iisreset**命令行工具，该工具导致 IIS 读取新的注册表值。

> [!NOTE]
> 将**EnableExtensionlessUrls**设置为1可启用无扩展名 URL 行为。 如果未指定任何值，则这是默认设置。

<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a>IIS 7 或 IIS 7.5 集成模式下的默认文档中可能不会引发事件处理程序

ASP.NET 4 包含一些修改，这些修改将更改在无扩展名 URL 解析为默认文档时如何呈现 HTML **form**元素的**action**属性。 将[http://contoso.com/](http://contoso.com/)解析为默认文档的无扩展名 URL 示例，导致[http://contoso.com/Default.aspx](http://contoso.com/Default.aspx)的请求。

ASP.NET 4 现在会将 HTML**窗体**元素的**action**属性值呈现为空字符串，同时向其提供默认文档的无扩展名 URL 发出请求。 例如，在早期版本的 ASP.NET 中，对[http://contoso.com](http://contoso.com)的请求将导致请求 `Default.aspx`。 在该文档中，开始**窗体**标记将呈现为，如以下示例中所示：

`<form action="Default.aspx" />`

在 ASP.NET 4 中， [http://contoso.com](http://contoso.com)的请求也会导致对 `Default.aspx`的请求。 但是，ASP.NET 现在会呈现 HTML 打开的**窗体**标记，如以下示例中所示：

`<form action="" />`

如何呈现**操作**属性的这一差异可能会导致 IIS 和 ASP.NET 处理窗体发布的方式发生细微的更改。 当**action**属性为空字符串时，IIS **DefaultDocumentModule**对象将创建 `Default.aspx`的子请求。 在大多数情况下，此子请求对于应用程序代码是透明的，并且 "`Default.aspx`" 页将正常运行。

但托管代码和 IIS 7 或 IIS 7.5 集成模式之间可能的交互会导致托管 .aspx 页在子请求期间停止正常工作。 如果出现以下情况，对 `Default.aspx` 文档的子请求将导致错误或意外行为：

1. .Aspx 页面将发送到浏览器，并将**form**元素的**action**特性设置为 ""。
2. 窗体将回发到 ASP.NET。
3. 托管 HTTP 模块读取实体正文的一部分。 例如，模块读取**Request**或**request**。 这会使 POST 请求的实体正文读入托管内存中。 因此，实体正文不再对在 IIS 7 或 IIS 7.5 集成模式中运行的任何本机代码模块可用。
4. IIS **DefaultDocumentModule**对象最终将运行并创建对 `Default.aspx` 文档的子请求。 但由于一段托管代码已读取实体正文，因此没有可发送给子请求的实体正文。
5. 当 HTTP 管道为子请求运行时，`.aspx` 文件的处理程序在处理程序执行阶段中运行。
6. 由于没有实体正文，因此没有窗体变量和视图状态，因此 .aspx 页面处理程序不能使用任何信息来确定应引发哪个事件（如果有）。 因此，不会运行针对受影响 .aspx 页的任何回发事件处理程序。

可以通过以下方式解决此问题：

- 标识在默认文档请求期间访问请求的实体正文的 HTTP 模块，并确定是否可将其配置为仅针对托管请求运行。 在用于 IIS 7 和 IIS 7.5 的集成模式下，可通过将以下属性添加到模块的**system.webserver/** module 条目来将 HTTP 模块标记为仅针对托管请求运行：

- `precondition="managedHandler"`

- 此设置将禁用 IIS 7 和 IIS 7.5 确定为不是托管请求的请求的模块。 对于默认的文档请求，第一个请求是无扩展名 URL。 因此，在初始请求处理过程中，IIS 不会运行用托管处理程序的前置条件标记的任何托管模块。 因此，托管模块不会意外读取实体正文，因此实体正文仍可用，并传递给子请求和默认文档。

- 如果有问题的 HTTP 模块必须为所有请求运行（对于可解析为**DefaultDocumentModule**对象的无扩展名 url，对于托管请求，等等），请通过将页面的**HtmlForm**控件的**Action**属性显式设置为非空字符串来修改受影响的 .aspx 页。 例如，如果 `Default.aspx`默认文档，请修改该页的代码，将**HtmlForm**控件的**Action**属性显式设置为 "default.aspx"。

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a>对 ASP.NET 代码访问安全性（CAS）实现的更改

ASP.NET 2.0，通过扩展3.5 中添加的 ASP.NET 功能，请使用 .NET Framework 1.1 和2.0 代码访问安全性（CAS）模型。 但是，实质上已对 ASP.NET 4 中的 CAS 实现进行了检查。 因此，依赖于全局程序集缓存（GAC）中运行的受信任代码的部分信任 ASP.NET 应用程序可能会失败，并会出现各种安全异常。 依赖于计算机 CAS 策略的广泛修改的部分信任应用程序可能也会失败，并出现安全异常。

你可以使用**信任**配置元素中的新**legacyCasModel**特性，将部分信任 ASP.NET 4 应用程序还原为 ASP.NET 1.1 和2.0 的行为，如以下示例中所示：

`<trust level= "Medium" legacyCasModel="true" />`

恢复为旧的 CAS 模型时，会启用以下旧的 CA 行为：

- 计算机 CAS 策略已生效。
- 允许在单个应用程序域中使用多个不同的权限集。
- 如果在堆栈上只有 ASP.NET 或其他 .NET Framework 代码，则将调用 GAC 中的程序集不需要显式权限断言。

无法在 .NET Framework 4 中还原一个方案：非 Web 部分信任应用程序无法再调用 System.web 和 System.web 中的某些 Api。 在 .NET Framework 的以前版本中，可能会向非 Web 部分信任应用程序显式授予**AspNetHostingPermission**权限。 然后，这些应用程序可使用**httputility.javascriptstringencode**、 **microsoft.samples.synchronization.clientservices.custom.\*** 命名空间中的类型和与成员资格、角色和配置文件相关的类型。 .NET Framework 4 中不再支持从非 Web 部分信任应用程序调用这些类型。

> [!NOTE]
> **Httputility.javascriptstringencode**类的**server.htmlencode**和**system.net.webutility.htmldecode**功能已移至新的 .NET Framework 4**系统 .net**类。 如果这是唯一使用的 ASP.NET 功能，请修改应用程序的代码以改用新的**webutility.htmldecode**类。

下面是对 ASP.NET 4 中默认 CAS 实现所做更改的高级摘要：

- ASP.NET 应用程序域现在是同类应用程序域。 只有部分信任和完全信任授权集在应用程序域中可用。
- ASP.NET 部分信任授予集独立于任何企业级、计算机级别或用户级别的 CAS 策略。
- 3\.5 和 3.5 SP1 随附的 ASP.NET 程序集已转换为使用 .NET Framework 4 透明度模型。
- ASP.NET **AspNetHostingPermission**属性的使用大大减少。 此属性的大多数实例已从公共 ASP.NET Api 中删除。
- 已更新由 ASP.NET 生成提供程序创建的动态编译的程序集，以将程序集显式标记为透明。
- 现在，所有 ASP.NET 程序集都标记为只能在 Web 宿主环境中使用 APTCA 特性。 部分受信任的非 Web 宿主环境（如 ClickOnce）将无法调用到 ASP.NET 程序集。

有关新的 ASP.NET 4 代码访问安全模型的详细信息，请参阅 MSDN 网站上的[使用 ASP.NET 应用程序中的代码访问安全性](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx)。

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a>MembershipUser 命名空间中的其他类型已移动

ASP.NET 成员身份中使用的某些类型已从 `System.Web.dll` 移动到新的 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 程序集。 移动这些类型是为了解析客户端中的类型与扩展的 .NET Framework SKU 中的类型之间的体系结构层依赖关系。

由于已将 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 添加到由 ASP.NET 编译系统默认使用的被引用程序集的列表中，因此网站项目在移动这些类型时没有问题。 如果将使用早期版本的 ASP.NET 创建的网站项目升级到 ASP.NET 4，则在 Visual Studio 2010 中打开该项目时，该项目将在编译时不会出错。

同样，如果你将在早期版本的 ASP.NET 中创建的 Web 应用程序项目升级到 ASP.NET 4，则在 Visual Studio 2010 中打开该项目时，升级过程会将对该项目的引用添加到该项目中。 因此，升级后的 Web 应用程序项目也会编译而不出错。

使用早期版本的 ASP.NET 创建的已编译（二进制）文件也会在 ASP.NET 4 上运行而不会出现错误，即使成员身份类型已移到不同的程序集。 类型转发信息已添加到 `System.Web.dll` 的 ASP.NET 4 版本中，可自动将这些类型的运行时引用路由到类型的新位置。

但是，使用特定成员身份类型并且已从早期版本的 ASP.NET 升级的类库在 ASP.NET 4 项目中使用时将无法进行编译。 例如，类库项目可能无法编译并报告错误，如下所示：

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

可以通过将类库项目中的引用添加到 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 来解决此问题。

以下列表显示了已从 `System.Web.dll` 移动到 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 的*system.web. Security*类型：

- *System.web. MembershipCreateStatus*
- *"CreateUserException"。*
- *System.web. System.web.security.membershippasswordexception*
- *System.web. MembershipPasswordFormat*
- *System.web. node.js*
- *System.web. MembershipProviderCollection*
- *System.web. MembershipUser*
- *System.web. MembershipUserCollection*
- *System.web. MembershipValidatePasswordEventHandler*
- *System.web. ValidatePasswordEventArgs*
- *System.web. RoleProvider*
- <a id="0.1_a"></a>*System.web. MembershipPasswordCompatibilityMode*

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a>\* HTTP 标头变化的输出缓存更改

在 ASP.NET 1.0 中，bug 导致指定 `Location="ServerAndClient"` 作为输出的缓存页在响应中发出 `Vary:*` HTTP 标头。 这还能起到告知客户端浏览器绝不要本地对页进行缓存的作用。

在 ASP.NET 1.1 中，添加了**HttpCachePolicy. SetOmitVaryStar**方法，你可以调用它来取消 `Vary:*` 标头。 之所以选择此方法，是因为更改发出的 HTTP 标头时被视为可能重大更改。 但是，开发人员与 ASP.NET 中的行为感到困惑，bug 报告建议开发人员不知道现有的**SetOmitVaryStar**行为。

在 ASP.NET 4 中，决定解决根本问题。 不再从指定以下指令的响应发出 `Vary:*` HTTP 标头：

`<%@OutputCache Location="ServerAndClient" %>`

因此，不再需要**SetOmitVaryStar**来禁止 `Vary:*` 标头。

在指定页面上 **@ OutputCache**指令中的 `Location="ServerAndClient"` 的应用程序中，现在可以看到**Location**属性的值的名称所隐含的行为，即，可以在浏览器中缓存页面，而无需调用**SetOmitVaryStar**方法。

如果应用程序中的页必须发出 `Vary:*`，请调用**AppendHeader**方法，如以下示例中所示：

`HttpResponse.AppendHeader("Vary","*");`

或者，您可以将 "输出缓存**位置**" 属性的值更改为 "Server"。

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a>Passport 的安全类型已过时

由于 Passport 中的更改（现在是 LiveID），ASP.NET 2.0 中内置的 Passport 支持已过时且不受支持。 因此，与**system.web**中的 Passport 相关的五个类型现在使用**ObsoleteAttribute**属性进行标记。

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a>PopOutImageUrl 属性未能呈现 ASP.NET 4 中的图像

在 ASP.NET 3.5 中， *PopOutImageUrl*属性允许你指定显示在菜单项中的图像的 URL，以指示菜单项具有动态子菜单。 下面的示例演示如何在 ASP.NET 3.5 的标记中指定此属性。

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

由于 ASP.NET 4 中的设计更改，如果为*MenuItem*类设置了属性，则不会呈现*PopOutImageUrl*的输出。 相反，必须使用*StaticPopOutImageUrl*属性或*DynamicPopOutImageUrl*属性直接在*MENU*控件中指定图像 URL。 使用静态菜单时， *StaticPopOutImageUrl*属性指定显示的图像的 URL，以指示静态菜单项包含子菜单，如以下示例中所示：

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

如果使用的是动态菜单，请使用*DynamicPopOutImageUrl*属性来指定图像的 URL，该图像指示动态菜单项具有子菜单。 下面的示例与上一个示例类似，但演示了如何设置动态菜单的*DynamicPopOutImageUrl*属性。

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

如果未设置*DynamicPopOutImageUrl*属性，并且*DynamicEnableDefaultPopOutImage*属性设置为*false*，则不会显示图像。 同样，如果未设置*StaticPopOutImageUrl*属性，并且*StaticEnableDefaultPopOutImage*属性设置为*false*，则不会显示图像。

设置这些属性的路径时，请使用正斜杠（/）而不是反斜杠（\)。 有关详细信息，请参阅[StaticPopOutImageUrl 和 DynamicPopOutImageUrl 无法呈现图像，因为路径包含](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu. StaticPopOutImageUrl_and_Menu。")本文档其他位置的反斜杠。

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a>当路径包含反斜杠时，StaticPopOutImageUrl 和 DynamicPopOutImageUrl 无法呈现图像

在 ASP.NET 4 中，如果路径包含 backlashes （\)，则不会呈现使用*StaticPopOutImageUrl*和*DynamicPopOutImageUrl*属性指定的图像。 这是对早期版本的 ASP.NET 的更改。

以下*Menu*控件标记的示例显示了*StaticPopOutImageUrl*属性集，其中使用了包含反斜杠的路径。 在 ASP.NET 4 中，将不呈现在属性中指定的图像。

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

若要更正此问题，请将*StaticPopOutImageUrl*和*DynamicPopOutImageUrl*属性中指定的路径值更改为使用正斜杠（/）。 下面的示例演示了此更改：

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

请注意，从早期版本的 ASP.NET 迁移到 ASP.NET 4 的应用程序可能也会受到影响，因为*PopOutImageUrl*属性已更改。 有关详细信息，请参阅 PopOutImageUrl 属性无法在本文档中的其他位置[呈现 ASP.NET 4 中的图像](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem. PopOutImageUrl_Propert")。

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a>免责声明

这是一份初稿，并可能在本文所述软件最终商业发布之前进行大幅更改。

本文所含信息代表 Microsoft Corporation 对截至发布之日所讨论问题持有的当前观点。 由于 Microsoft 必须对不断变化的市场情况作出响应，所以不应将本文解释为是 Microsoft 做出的承诺，Microsoft 并不保证所提供的任何信息在公布之日后的准确性。

本白皮书仅用于提供信息。 MICROSOFT 对本文档中的信息不做任何明示、暗示或法定的担保。

遵守所有适用的著作权法是用户的责任。 未经 Microsoft Corporation 明确的书面许可，不得出于任何目的或以任何形式或任何手段（电子、机械、影印、记录或其他方法）复制本文档的任何部分，或者将其存储或引入检索系统，或者将其进行传播。受版权法保护的权利不受此限制。

对于本文档中的主题，Microsoft 可能具有专利、专利申请、商标、版权或其他知识产权。 除非 Microsoft 的任何书面许可协议明确提出，否则，本文档的提供并不表示 Microsoft 已将这些专利、商标、版权或其他知识产权的任何许可权限授予您。

除非另有说明，否则本示例中描述的公司、组织、产品、域名、电子邮件地址、徽标、人物、地点和事件均属虚构，与任何真实的公司、组织、产品、域名、电子邮件关联应推断地址、徽标、人物、地点或事件。

© 2010 Microsoft Corporation. 保留所有权利。

Microsoft 和 Windows 是 Microsoft Corporation 在美国和/或其他国家/地区的注册商标或商标。

本文档所涉及的真实公司和产品名称可能是其各自所有者的商标。
