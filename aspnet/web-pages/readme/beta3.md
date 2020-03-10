---
uid: web-pages/readme/beta3
title: Web Matrix 和 ASP.NET 网页（Razor） Beta 3 版本自述文件 |Microsoft Docs
author: rick-anderson
description: Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510338"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a>Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件

> Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件

11月9日2010

## <a name="contents"></a>内容

- [概述](#Overview)
- [安装](#Installation_Notes)
- [Beta 3 版本中的新功能、更改和已知问题](#Known_Issues)

    - [WebMatrix 安装问题](#Known_Issues_Installation)
    - [ASP.NET 网页](#Known_Issues_ASPNET)
    - [SQL Server Compact](#Known_Issues_SQL_Server_Compact)
    - [安装应用程序](#Known_Issues_Installing_Applications)
    - [发布应用程序](#Known_Issues_Publishing_Applications)
    - [其他问题](#Known_Issues_Other_Issues)
- [更多信息](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>概述

> Microsoft WebMatrix Beta 是一个免费的 web 开发堆栈，只需几分钟即可完成安装。 它将 web 服务器与数据库和编程框架相集成，以创建单一、集成的体验。 你可以使用 WebMatrix Beta 来简化你的代码、测试和发布你自己的 ASP.NET 或 PHP 网站的方式，也可以使用 WebMatrix Beta 来使用常见开源应用（如 DotNetNuke、Umbraco、WordPress 或 Joomla）启动新网站。 WebMatrix Beta 使用的功能强大的 web 服务器、数据库引擎和框架环境将在 internet 上运行你的网站，这使得从开发到生产的过渡顺畅顺畅。

<a id="Installation_Notes"></a>

## <a name="installation"></a>安装

> 若要安装 WebMatrix Beta 3，请使用[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。 安装 Web 平台安装程序后，可以使用它来安装 WebMatrix Beta 3。
> 
> 如果在安装过程中遇到问题，请参阅[Microsoft Web 平台安装程序的疑难解答问题](https://go.microsoft.com/fwlink/?LinkId=196212)。

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a>有关发布应用程序的说明

> 请参阅[发布应用程序的分步说明](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a>新功能、更改、andKnown 问题

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a>WebMatrix Beta 3 安装

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a>问题： WebMatrix Beta 3 仅适用于支持 Microsoft .NET Framework 4 的平台

> WebMatrix Beta 版需要 .NET Framework 版本4。 在某些情况下，WebMatrix Beta 安装程序将允许你尝试在不属于受支持的配置集的平台上安装。 具体而言，如果没有 SP1 更新，Windows Vista 将允许你开始安装 WebMatrix Beta，但 .NET Framework 4 组件将失败并阻止你的安装。
> 
> **解决方法**  
> 在支持的平台上安装，其中包括：
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 或更高版本
> - Windows XP SP3
> - Windows Server 2003 SP2

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>问题：如果在未 Microsoft Visual Studio 2008 SP1 的情况下安装 Microsoft Visual Studio 2008，将无法安装 WebMatrix Beta 3

> **解决方法**  
> 从 Microsoft 下载中心安装[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 。

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>问题： GAC 中未安装 SQL Server Compact 4.0 的某些程序集

> 在64位计算机上安装 SQL Server Compact 4.0，并且计算机仅安装了 .NET Framework 3.5 SP1 客户端配置文件时，SQL Server Compact 4.0 的托管程序集不会放置在全局程序集缓存（GAC）中。 GAC 中未安装的托管程序集包括：
> 
> - *System.data.sqlserverce* （ADO.NET 提供程序）
> - *System.web. system.data.sqlserverce* （ADO.NET 实体框架）
> 
> **解决方法**  
> 卸载 SQL Server Compact 4.0。 从以下位置下载并安装 .NET Framework 3.5 SP1 的完整版本：  
>   
> [Microsoft .NET Framework 3.5 Service pack 1 （完整程序包）](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> 然后重新安装 SQL Server Compact 4.0。

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>问题：无法使用命令行卸载 SQL Server Compact

> 使用命令行选项卸载 SQL Server Compact 在此版本中不起作用。
> 
> **解决方法**  
> 使用 Windows 控制面板中的 "*程序和功能*" 卸载 Microsoft SQL Server Compact 4.0。

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET 网页

本部分介绍与 Razor 语法 ASP.NET 网页的 Beta 3 版本的新功能、更改和已知问题。

- [新增功能](#NewFeatures)
- [更改](#Changes)
- [问题](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Beta 3 中的新增功能，适用于带有 Razor 语法的 ASP.NET 网页

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a>New： ".Html" 方法呈现未编码的标记

> 利用新的 `Html.Raw` 方法，你可以将 HTML 标记呈现为标记，而不是呈现编码的输出。 （默认情况下，ASP.NET Razor 在呈现字符串之前对其进行编码。）语法为：
> 
> `Html.Raw(value)`
> 
> 下面的示例演示如何使用 `Html.Raw`：
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Beta 3 中针对具有 Razor 语法 ASP.NET 网页的更改

#### <a name="change-hrefattribute-method-removed"></a>Change：已删除 "HrefAttribute" 方法

> 已移除 `WebPage` 类的 `HrefAttribute` 方法。 此帮助程序用于对 Url 中的不安全字符进行编码。 不再需要此方法，因为 ASP.NET Razor 会自动对字符串进行编码。 （使用新的 `Html.Raw` 方法呈现未编码的字符串。）

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a>更改：声明性 "@helper" 帮助器的语法已更改

> 在 Beta 3 版本中，ASP.NET 更改了如何分析使用 `@helper` 语法创建的帮助器。 实质上，`@helper` 语法现在被分析为代码块，而不是一个可包含代码的标记块。 因此，帮助器内的代码不需要包含在 `@{ }` 块中。 相反，帮助器中的标记必须显式包含在 HTML 元素中或 ASP.NET Razor `<text></text>` 标记中。
> 
> 例如，以下 `@helper` 语法适用于 Beta 3 版本：
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> 在 Beta 3 版本中，必须更改此帮助程序，使其类似于以下示例：
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> 请注意，不再使用助手中初始代码周围的 `@{ }` 字符。 这是因为默认情况下，帮助器的内容被视为代码块。 帮助器呈现标记，该标记以开始 `<a>` 标记开头。 如果帮助程序必须呈现纯文本或不包括结束标记的标记（例如 `<meta>` 标记），则要呈现的内容必须位于 `<text></text>` 标记中。

#### <a name="change-webpagecontexthttpcontext-removed"></a>更改：已删除 "WebPageContext"

> `WebPageContext.HttpContext` 属性已被删除。 请改用 `HttpContext.Current`。 （`WebPageContext.HttpContext` 属性仅包装此。）

#### <a name="change-facebook-helper-moved-to-new-package"></a>更改：已将 "Facebook" 帮助器移动到新包

> `Facebook` 帮助程序已移动到*Facebook. 帮助*程序库，其中包括 `Facebook` 帮助程序和附加功能。 必须以单独的包的形式安装此库，如教程[入门使用 ASP.NET 页面](https://go.microsoft.com/fwlink/?LinkId=202889)中的 "使用程序包管理器安装帮助程序" 中所述。

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a>更改：成员身份、角色和安全类型会移到新程序集

> 以下类型已移动到 `WebMatrix.WebData` 程序集：
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a>Change： "TagBuilder" 类已移动到 System.web .dll 程序集

> `TagBuilde` r 类已移动到 System.web .dll 程序集。 以前，此程序集位于作为 ASP.NET MVC 一部分的程序集中。 此更改意味着无需安装 ASP.NET MVC 即可使用 `TagBuilder` 类。
> 
> 但是，该类仍处于 `System.Web.Mvc` 命名空间中。 为了使用 `TagBuilder` 类（例如，在自定义 ASP.NET Razor 帮助器中），必须引用命名空间（例如，通过将 `@using System.Web.Mvc` 添加到代码中）。

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a>更改：请求验证语法已更改;已删除 "验证" 类

> 在 Beta 3 版本中，若要禁用单个字段或一组字段的验证，可以调用 `Validation.Exclude` 方法，并传入要从验证中排除的字段名称或名称。 Beta 3 版本中提供了一个新语法，用于绕过验证。 已删除 Beta 3 中使用的 `Validation` 方法。
> 
> > [!NOTE]
> > 如果未禁用请求验证，则用户尝试上传 HTML 标记（例如，通过在页面上使用 rtf 文本编辑器），该网站将报告错误，如*潜在的危险请求。从客户端检测到表单值*，并且不接受用户输入。 如果禁用请求验证，则必须手动检查用户输入，以确保它不会使用类似[Microsoft 反跨站点脚本库 v4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)的内容来包含潜在的危险标记或脚本。
> 
> 
> 若要禁用自动请求验证，请调用 `Request.Unvalidated` 方法，并向其传递要绕过请求验证的字段或其他 post 对象的名称。 您可以使用此方法绕过对 `Form`、`QueryString`、`Cookies`和 `ServerVariables` 集合中任何项的验证。 下面的示例演示如何使用 `Unvalidated` 方法：
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a>用 Razor 语法 ASP.NET 网页的已知问题

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>问题：将自定义用户表用于成员身份时出现意外行为

> 若要初始化 ASP.NET Razor 网站的成员资格提供程序，请调用 `WebSecurity.InitializeDatabaseConnection` 方法。 （在 WebMatrix 中，初学者站点模板在 *\_AppStart*文件中包含对此方法的调用。）如果此方法的 `autoCreateTables` 参数设置为 true （默认情况下，它在 Starter Site 模板中设置为 true），并且如果将无法识别的表名传递给方法（第二个参数），则此方法不会引发错误。 相反，它会自动创建表。
> 
> 如果要将自定义用户表用于成员身份，但将错误的表名传递到 `WebSecurity.InitializeDatabaseConnection` 方法，这可能是一个问题。 由于方法默认情况下不会引发错误，因此，如果您指定的表不存在，而是创建新表，则该应用程序可能看起来正在运行。 但是，依赖于自定义用户表的应用程序代码（以及其中的字段）最终可能会失败，并出现意外错误。
> 
> **解决方法**  
> 请确保 `InitializeDatabaseConnection` 方法中传递的名称与成员资格数据库中的用户配置文件表匹配，或者确保 `autoCreateTables` 参数设置为 false。

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>问题： "未能生成 SQL Server 的用户实例" 错误

> 如果 WebMatrix Web 应用程序使用 SQL Server Express 并且在 Windows 7 或 Windows Server 2008 R2 上运行 IIS 7.5，你可能会看到一个错误，指示 SQL Server 无法在运行时检索用户的本地应用程序路径。
> 
> **解决方法**请确保应用程序在其下运行的 Windows 帐户（通常为网络服务）对应用程序的根文件夹和子文件夹（例如*应用程序\_数据*）具有读/写权限。 [SQL Server Express 用户实例化和 ASP.net Web 应用程序项目](https://support.microsoft.com/kb/2002980)的知识库文章问题中提供了更多详细信息。

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a>问题：在 Visual Studio 中，自定义程序集（Dll）的命名空间不会自动导入

> 如果你在 Visual Studio 的项目中使用自定义程序集，则在设计时不会自动导入在这些程序集中声明的命名空间。 因此，在设计时可能无法识别对自定义类型的引用，并在 Visual Studio 中将其标记为无法识别（使用 "波形曲线"）。 此问题仅发生在 Visual Studio 中的设计时;应用程序本身会正常运行。
> 
> **解决方法**  
> 包括引用在设计时无法识别的实体的 `using` 语句（`imports` 在 Visual Basic 中）。

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>问题： Visual Studio IntelliSense 和项目模板仅在 ASP.NET MVC 版本3中提供

> 安装 ASP.NET 网页也不会安装适用于 Visual Studio 的工具，例如用于 ASP.NET 网页应用程序的 IntelliSense 和项目模板。
> 
> **解决方法**若要在 Visual Studio 中使用 ASP.NET 网页应用程序的 IntelliSense 和项目模板，请通过 Web 平台安装程序或[独立安装程序](https://go.microsoft.com/fwlink/?LinkID=191797)安装 ASP.NET MVC 3 RC。

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a>问题： "找不到&lt;helper&gt; 类" 错误

> 升级到 Beta 3 后，可能会看到一个错误，指出找不到帮助程序类（例如，`Facebook` 类）。 从 Beta 2 开始，在 Beta 3 中继续，帮助程序已移动到必须显式安装的包。 不会升级现有站点以包含这些包;这包括 *\My Documents\IISExpress*或 *\My Documents\My 网站*文件夹中的网站。 具体而言，如果使用 "*我的网站*" （WebSite1）中的默认网站（包括对 `Twitter` 帮助程序的引用），将看到此错误。
> 
> **解决方法**  
> 注释掉对站点中任何帮助程序的调用，运行 *\_管理*页，然后安装包含要使用的帮助程序的一个或一些包。 安装包后，可以取消注释引用帮助器的行。

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a>问题：将 Beta 3 ASP.NET Razor 程序集部署到 Bin 文件夹在托管网站上可能不起作用

> 如果将 ASP.NET 网页网站部署到宿主站点，并且将 ASP.NET Razor Beta 3 程序集部署到站点的*Bin*文件夹，则可能会遇到错误，包括以下内容：
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> 如果宿主提供程序已将 ASP.NET 网页 Beta 1 程序集安装到服务器的全局应用程序缓存（GAC）中，则可能会发生这种情况。 GAC 中的程序集优先于在*Bin*文件夹中本地安装的程序集。
> 
> **解决方法**请与您的宿主提供商联系，以确认您所遇到的错误是由提供程序的程序集版本和您的程序集版本之间的冲突引起的。 如果是这样，则请求宿主提供程序更新服务器的 GAC 中的程序集。

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>问题：通过代理服务器读取源或其他外部数据

> 如果运行该站点的服务器位于代理服务器后面，则你可能需要在 web.config 文件中配置代理信息，以便能够读取来自你的站点*之外的信息*。 例如，如果使用 `ReCaptcha` 帮助程序，则帮助者与 reCAPTCHA 服务通信，但可能会被代理服务器阻止。 同样，在 ASP.NET 网页中使用的源（如包管理器使用的源）可能需要代理配置。
> 
> 如果在使用外部服务或使用包源时遇到问题，请将以下元素添加到应用程序*的根 web.config*文件中：
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> 有关配置代理服务器的详细信息，请参阅 MSDN 网站上的[&lt;proxy&gt; 元素（网络设置）](https://msdn.microsoft.com/library/sa91de1e.aspx) 。

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a>问题： "无法加载" "。

> 如果以前安装了 Beta 1 版本的 ASP.NET 网页与 Razor 语法，然后安装 Beta 3 版本，则所有适当的程序集都将安装到 GAC 中 *，但不包括：* 因此，当你运行 ASP.NET Razor 页面时，你将看到一个错误，指示无法加载*Microsoft* 。
> 
> 如果在干净的计算机上加载 Beta 3 版本，则不会出现此问题。
> 
> **解决方法**  
> 在 "控制面板" 中，卸载 ASP.NET 网页。 然后重新安装 Beta 3 版本。

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>问题：卸载 .NET Framework 版本4禁用包含 Razor 语法 ASP.NET 网页

> 如果卸载 .NET Framework 版本4，然后重新安装它，则将禁用 Razor 语法的 ASP.NET 网页。 扩展名为 *...* ASP.NET 网页在计算机根*web.config*文件中注册程序集，删除 .NET Framework 删除该文件。 重新安装 .NET Framework 会安装新版本的配置文件，但不会为 ASP.NET 网页程序集添加引用。
> 
> **解决方法**重新安装 .NET Framework 后，请用 Razor 语法重新安装 ASP.NET 网页。 这会将以下元素添加到计算机根目录中的*web.config 文件中，该文件*通常位于以下位置：  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a>问题：以前在 Bin 文件夹中用 ASP.NET 程序集部署的应用程序遇到错误

> 在部署期间，ASP.NET 网页程序集（例如， *.dll*）的副本将复制到服务器上网站的*Bin*文件夹中。 （这可能是在部署过程中自动发生的，也可能是因为开发人员显式复制了这些程序集。）但是，当安装 Beta 3 版本时，会发生错误，如找不到某些类型的错误。 出现这种情况的原因是，许多 ASP.NET 网页类型已移入到 Beta 3 版本的不同命名空间中。
> 
> **解决方法**   
> 清除部署的应用程序的*Bin*文件夹，将新的程序集复制到该文件夹（或重新部署应用程序），然后重新启动应用程序。

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>问题：无扩展名 Url 在 IIS 7 或 IIS 7.5 上找不到. cshtml/vbhtml 文件

> 在 IIS 7 或 IIS 7.5 上，使用如下所示的 URL 的请求将无法*找到扩展名为* *.*  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> 出现此问题的原因是，IIS 7 或 IIS 7.5 默认情况下未启用 URL 重写。 Likeliest 方案是，使用 IIS Express 在本地进行测试时不会出现问题，但在将网站部署到托管网站时，你会遇到此问题。
> 
> **解决方法**
> 
> - 如果你可以控制服务器计算机，则在服务器计算机上安装更新中所述的更新[可使某些 IIS 7.0 或 IIS 7.5 处理程序处理其 url 不以句点结尾的请求](https://support.microsoft.com/kb/980368)。
> - 如果无法控制服务器计算机（例如，部署到托管网站），请将以下内容添加*到网站的 web.config 文件中*：
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a>问题：在同一应用程序中使用 Web 应用程序项目或 ASP.NET MVC 和 ASP.NET 网页

> 如果在 Web 应用程序项目或 ASP.NET MVC 应用程序中使用 ASP.NET 网页，则可能会出现*WebPageHttpApplication*找不到的错误。
> 
> **解决方法**  
> 如果收到此错误，请更改应用程序派生自的基类。 在*global.asax*文件中，更改以下行：
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> 更改为：
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> 这实际上会反转使用 Razor 语法的 ASP.NET 网页 Beta 1 版本引入的更改。

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>问题：将应用程序部署到未安装 SQL Server Compact 的计算机

> 包含 SQL Server Compact 数据库的应用程序可以在未安装 SQL Server Compact 的计算机上运行。 Microsoft WebMatrix Beta 3 会自动复制这些二进制文件，并执行适当的*web.config*文件转换。
> 
> **解决方法**如果需要复制这些文件并手动更改*web.config 文件，* 请执行以下操作：
> 
> 1. 将数据库引擎程序集复制到目标计算机上的应用程序的*Bin*文件夹中（和子文件夹）： 
> 
>     - 将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*复制**到** *\bin*
>     - 将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* * 复制**到** *\Bin\x86*
>     - 将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* * 复制**到** *\Bin\amd64*
> 2. 在网站的根文件夹中，创建或打开*web.config*文件。 （在 WebMatrix Beta 3 中，如果您在 "**选择文件类型**" 对话框中单击 "**全部**"，则此文件类型可用。）
> 3. 添加以下元素作为 **&lt;配置&gt;** 元素的子元素（不在 **&lt;system.web&gt;** 元素内）：
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>问题：数据库和 WebGrid 帮助程序在 Visual Basic 的中等信任环境中不起作用

> 如果使用 Visual Basic （创建*vbhtml*文件），并且将应用程序设置为使用中等信任，则 `Database` 和 `WebGrid` 帮助程序将不起作用。
> 
> **解决方法**  
> 暂时将应用程序设置为使用完全信任。

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a>SQL Server Compact

#### <a name="issue-encrypt-property-is-not-recognized"></a>问题： "加密" 属性无法识别

> SQL Server Compact 4.0 无法识别 `SqlCeConnection` 类的 `Encrypt` 属性。 不应使用此属性来加密数据库文件。 `Encrypt` 属性在 SQL Server Compact 3.5 版本中已弃用，并且仅为向后兼容性而保留。 
> 
> **解决方法**  
> 使用 `SqlCeConnection` 类的 `Encryption Mode` 属性来加密 SQL Server Compact 4.0 数据库文件。 下面的示例演示如何使用 `Encryption Mode` 属性创建加密的 SQL Server Compact 4.0 数据库：
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> 若要更改现有 SQL Server Compact 4.0 数据库的加密模式，请执行以下操作：
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> 若要对未加密的 SQL Server Compact 4.0 数据库进行加密，请执行以下操作：
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a>问题：需要 Microsoft C++ Visual 2008 运行时库

> SQL Server Compact 4.0 的本机 Dll 需要 Microsoft Visual C++ 2008 运行时库（X86、IA64 和 X64） Service Pack 1。
> 
> **解决方法**  
> 安装 .NET Framework 3.5 SP1。 这也会安装 Visual C++ 2008 运行时库 SP1。 可以从以下位置下载库：   
>   
> [Microsoft Visual C++ 2008 Service Pack 1 可再发行组件包 ATL 安全更新](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> 请注意，安装 .NET Framework 2.0、3.0 或*4 不会安装 Visual* C++ 2008 运行时库 SP1。

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a>问题：如果在计算机上安装 .NET Framework 之前安装 SQL Server Compact，则其提供程序固定名称未在 .NET Framework machine.config 文件中注册

> SQL Server Compact 可以安装在未安装 .NET Framework 的计算机上，因为 SQL Server Compact 需要 .NET Framework。 如果在安装 SQL Server Compact 之前，不会安装 .NET Framework 版本3.5 和4，SQL Server Compact 安装程序不*会在 machine.config 文件中*注册其提供程序固定名称。 任何依赖于*machine.config*文件中的 SQL Server Compact 条目的应用程序都将失败。 *Machine.config*中的固定名称注册条目类似于以下示例：
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> **解决方法**  
> 卸载 SQL Server Compact 4.0 CTP1。 从以下位置下载并安装 .NET Framework 的完整版本：
> 
> [Microsoft .NET Framework 3.5 Service pack 1 （完整程序包）](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [Microsoft .NET Framework 4.0 版本（完整包）](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> 然后重新安装[SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)。

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a>安装应用程序

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>问题：如果将用户的 "我的文档" 文件夹重定向到网络共享，则安装应用程序可能需要较长时间

> **解决方法**  
> 无。 安装应用程序可能需要一些时间，但会正确安装。

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a>发布应用程序

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>问题：如果 "目标 URL" 字段未使用 http://或 https://作为前缀，则站点可能无法正常工作

> 在 "**发布设置**" 对话框中，如果目标 URL 不以 `http://` 或 `https://`开头，则该站点在部署后可能不起作用。
> 
> **解决方法**  
> 请确保在发布站点之前，"**发布设置**" 对话框中的 "目标 URL" 以 `http://` 或 `https://`开头。

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>问题：发布 MySQL 数据库失败，出现错误 "无法发布数据库。 如果远程数据库无法运行该脚本，就会发生这种情况。

> 发生此错误的原因有很多。 出现此错误的原因之一是，数据库脚本包含单引号字符（'），目标 MySQL 数据库的默认字符集不是 UTF-8。
> 
> **解决方法**  
> 将远程 MySQL 数据库的默认字符集设置为 UTF-8。

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a>其他问题

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a>问题： "搜索/筛选" 在 "分组依据" 的报表中不起作用：问题类型

> 当你为站点运行报表时，如果你在 "*按 URL 筛选*" 框中输入文本，然后单击 "*搜索*"，则不会发生任何事情。 这是因为，当报表的 "*分组依据*" 状态设置为 "*问题类型*" （默认值）时，此控件不起作用。
> 
> **解决方法**在功能区的 "*分组依据*" 选项卡中，单击 " *URL* "，按源 url 对条目分组。 在处于此状态时，文本框和用于筛选条目的按钮是正常的。

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a>问题： WCF 应用程序无法与 IIS Express 一起运行

> 浏览到 WCF 应用程序会导致错误，如下所示：
> 
> *无法加载文件或程序集 "7.0.0.0，Version =，Culture = 中立，PublicKeyToken = 31bf3856ad364e35" 或其依赖项之一。系统找不到指定的文件。*
> 
> 出现这种情况的原因是 IIS Express Beta 版本默认情况下不支持 WCF。
> 
> **解决方法**使用以下解决方法之一（解决方法 #2 需要 Microsoft Windows Vista 或更高版本）：
> 
> 
> 1. 将*microsoft. .dll*和 *.dll*程序集从 WebMatrix 安装位置复制到 WCF 应用程序的*bin*目录。 默认情况下，WebMatrix 安装在系统的*Program Files*文件夹下的*Microsoft WebMatrix*子文件夹中。
> 2. 在 Microsoft Windows Vista 或更高版本上，使用以下命令在*bin*目录中创建程序集的符号链接。 （此方法的优点是不会创建程序集的副本。）
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. 在 GAC 中安装两个程序集。 在提升的提示符下运行以下命令：
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a>问题： WebMatrix Beta 3 无法执行需要提升的某些任务

> WebMatrix Beta 3 无法执行某些需要提升的任务，例如在下列情况下安装其他组件：
> 
> - 在 Windows Vista 或 Windows 7 上，你使用没有管理权限的帐户登录，并且用户帐户控制（UAC）处于禁用状态。
> - 你使用的是 Microsoft Windows XP 或 Microsoft Windows Server 2003。
> 
> **解决方法**  
> WebMatrix Beta 3 中的大多数任务不需要管理权限。 对于这种情况，您可以以管理员身份执行操作，也可以执行以下步骤：
> 
> - 在 Windows Vista 或 Windows 7 上，启用 UAC。
> - 在 Windows XP 上，将用户添加到 "管理员" 安全组。

#### <a name="issue-site-from-web-gallery-is-disabled"></a>问题： "来自 Web 库的网站" 已禁用

> 如果未安装 Web 平台安装程序3.0，则将禁用 "**从 Web 库中站点**" 选项。
> 
> **解决方法**  
> 安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a>问题：在 Windows Server 2003 上，不为非管理用户启动 IIS Express

> 在 Windows Server 2003 上，启动页面或启动 IIS Express 时，IIS Express 不会启动。 对于网页，将显示一条错误，指示该应用程序已由非管理用户启动。
> 
> **解决方法**  
> 以管理用户身份启动 WebMatrix Beta 3。 有关更多详细信息，请参阅以下知识库文章：  
>   
> [非管理用户启动的应用程序无法侦听在 Windows Vista、Windows Server 2003 或 Windows XP 中运行该应用程序的计算机的 HTTP 通信。](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>问题： Google Chrome 不可用作运行选项

> "**主页**" 选项卡上的 "**运行**" 下的浏览器列表中不显示 Google Chrome。
> 
> **解决方法**  
> 某些版本的 Google Chrome 不会正确地通过 Windows 中的 "默认程序" 功能进行注册。 作为一种解决方法，请启动 Google Chrome，单击 "*自定义" 并控制 Google chrome*菜单，单击 "*选项*"，然后单击 "*使 google chrome 成为默认浏览器*"。

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>问题： "外键" 对话框不允许输入主键

> "**外键**" 对话框不允许您输入主键表中的主键名称。
> 
> **解决方法**  
> 这是有意的。 不需要输入主键表中的主键的名称。

#### <a name="issue-the-relationships-button-is-disabled"></a>问题：已禁用 "关系" 按钮

> 对于 SQL Server Compact 数据库，禁用了 "**数据库**" 工作区中 "**表**" 选项卡下的 "**关系**" 按钮。
> 
> **解决方法**  
> 无。 SQL Server Compact 不支持表之间的关系。

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a>问题：参数化 SQL 查询引发异常

> 在 SQL Server Compact 4.0 中，如果未指定参数化查询中参数的数据类型（如 `SqlDbType` 或 `DbType`），则在查询运行时将引发异常。
> 
> **解决方法**  
> 显式设置 `SqlDbType` 或 `DbType`等参数的数据类型。 这对于 BLOB 数据类型（`image` 和 `ntext`）非常重要。 使用如下所示的代码：
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a>更多信息

有关 WebMatrix Beta 3 的详细信息，请参阅以下网站：

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

---

© 2010 Microsoft Corporation. 保留所有权利。 [使用条款](https://msdn.microsoft.cos/cc300389.aspx)。
