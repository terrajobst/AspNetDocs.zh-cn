---
uid: web-pages/readme/overview
title: WebMatrix 自述文件 |Microsoft Docs
author: rick-anderson
description: WebMatrix 和 ASP.NET 网页（Razor）1.0 版本自述文件
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454268"
---
# <a name="webmatrix-readme"></a>WebMatrix 自述文件

13 2011 年1月

## <a name="contents"></a>内容

> [!NOTE]
> 此自述文件适用于 WebMatrix 的1.0 版本。

- [概述](#Overview)
- [安装](#Installation_Notes)
- [如何发布应用程序](#InstructionsForPublishingApplications)
- [更改和问题](#ChangesAndIssues)

    - [WebMatrix 1.0 安装](#Known_Issues_Installation)
    - [ASP.NET 网页](#Known_Issues_ASPNET)
    - [WebMatrix](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [安装应用程序](#Known_Issues_Installing_Applications)
    - [发布应用程序](#Known_Issues_Publishing_Applications)
- [更多信息](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>概述

> Microsoft WebMatrix 1.0 是一种免费的 web 开发堆栈，只需几分钟即可完成安装。 它将 web 服务器与数据库和编程框架相集成，以创建单一、集成的体验。 你可以使用 WebMatrix 来简化你的代码、测试和发布你自己的 ASP.NET 或 PHP 网站的方式，也可以使用 WebMatrix 来使用常用开源应用（如 DotNetNuke、Umbraco、WordPress 或 Joomla）启动新网站。 WebMatrix 使用在 internet 上运行你的网站的功能强大的 web 服务器、数据库引擎和框架环境，这使得从开发到生产的过渡顺畅顺畅。

<a id="Installation_Notes"></a>

## <a name="installation"></a>安装

> 若要安装 WebMatrix 1.0，必须首先安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。 安装 Web 平台安装程序后，可以使用它来安装 WebMatrix。
> 
> 如果在安装过程中遇到问题，请参阅[Microsoft Web 平台安装程序的疑难解答问题](https://go.microsoft.com/fwlink/?LinkId=196212)。

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>如何发布应用程序

> 请参阅[发布应用程序的分步说明](https://go.microsoft.com/fwlink/?LinkID=196149)

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>更改和问题

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>WebMatrix 1.0 安装问题

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>问题： WebMatrix 1.0 仅在支持 Microsoft .NET Framework 4 的平台上可用

> WebMatrix 需要 .NET Framework 版本4。 在某些情况下，WebMatrix 1.0 安装程序将允许你尝试在不属于受支持的配置集的平台上安装。 具体而言，没有 SP1 更新的 Windows Vista 会使你开始安装 WebMatrix，但 .NET Framework 4 组件将失败并阻止你的安装。
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

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>问题：如果在未 Microsoft Visual Studio 2008 SP1 的情况下安装 Microsoft Visual Studio 2008，则无法安装 WebMatrix 1。0

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

本部分介绍与 Razor 语法 ASP.NET 网页的1.0 版的新功能、更改和已知问题。

- [新增功能](#NewFeatures)
- [更改](#Changes)
- [问题](#Issues)

#### <a id="NewFeatures"></a>新功能

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>新增：添加了配置设置以禁用程序包管理器

> 为*web.config*文件中的 `<appSettings>` 元素提供了一个新的 `asp:AdminManagerEnabled` 项，可让你完全禁用包管理器。 此元素的默认值为 true，这意味着，如果它未包含在*web.config 文件中*，则启用包管理器。 若要禁用程序包管理器，请将以下元素添加*到网站根目录*中的 web.config 文件：
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a>变化

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>更改： "网页： AdminFolderVirtualPath" 密钥已重命名为 "asp： AdminFolderVirtualPath"

> 可以添加到*web.config 文件以*指定包管理器位置的 `webPages:AdminFolderVirtualPath` 项已重命名为使用 `asp:` 命名空间，而不是 `webPages` 命名空间。 如果使用了此元素，则必须在配置文件中对其进行重命名。

#### <a id="Issues"></a>  已知问题

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>问题：成员身份用户的密码不再被识别

> 用于创建和存储成员身份（登录名）密码的算法已更改为更安全。 因此，将无法识别为在 Beta 版本的 ASP.NET 中创建的成员（用户）存储的密码。 
> 
> **解决方法**如果该站点尚未投入生产，请从成员资格数据库中删除用户记录。 如果数据库是实时的，则以编程方式在成员资格数据库中重新生成现有密码。

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>问题：将自定义用户表用于成员身份时出现意外行为

> 若要初始化 ASP.NET Razor 网站的成员资格提供程序，请调用 `WebSecurity.InitializeDatabaseConnection` 方法。 （在 WebMatrix 中，初学者站点模板在 *\_AppStart*文件中包含对此方法的调用。）如果此方法的 `autoCreateTables` 参数设置为 true （默认情况下，它在 Starter Site 模板中设置为 true），并且如果将无法识别的表名传递给方法（第二个参数），则此方法不会引发错误。 相反，它会自动创建表。
> 
> 如果要将自定义用户表用于成员身份，但将错误的表名传递到 `WebSecurity.InitializeDatabaseConnection` 方法，这可能是一个问题。 由于方法默认情况下不会引发错误，因此，如果您指定的表不存在，而是创建新表，则该应用程序可能看起来正在运行。 但是，依赖于自定义用户表的应用程序代码（以及其中的字段）最终可能会失败，并出现意外错误。
> 
> **解决方法**  
> 请确保 `InitializeDatabaseConnection` 方法中传递的名称与成员资格数据库中的用户配置文件表匹配，或者确保 `autoCreateTables` 参数设置为 false。

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a>问题：错误消息 "管理模块需要访问 ~/App\_数据"

> 在某些情况下，尝试创建用户或在其他情况下使用 ASP.NET 成员资格系统会导致该页显示错误：*管理模块需要访问 ~/App\_数据*。 如果运行 IIS 或 IIS Express 的帐户无权在网站根目录下创建并写入*应用\_Data*文件夹，则会发生这种情况。 
> 
> **解决方法**手动为网站创建*应用\_Data*文件夹。 然后，确保应用程序在其下运行的 Windows 帐户（通常为网络服务）对应用程序的根文件夹和子文件夹（例如应用程序\_数据）具有读/写权限。 [SQL Server Express 用户实例化和 ASP.net Web 应用程序项目](https://support.microsoft.com/kb/2002980)的知识库文章问题中提供了更多详细信息。

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>问题： "未能生成 SQL Server 的用户实例" 错误

> 如果 WebMatrix Web 应用程序使用 SQL Server Express 并且在 Windows 7 或 Windows Server 2008 R2 上运行 IIS 7.5，你可能会看到一个错误，指示 SQL Server 无法在运行时检索用户的本地应用程序路径。
> 
> **解决方法**请确保应用程序在其下运行的 Windows 帐户（通常为网络服务）对应用程序的根文件夹和子文件夹（例如*应用程序\_数据*）具有读/写权限。 [SQL Server Express 用户实例化和 ASP.net Web 应用程序项目](https://support.microsoft.com/kb/2002980)的知识库文章问题中提供了更多详细信息。

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>问题：包含包管理器资源或包管理器密码的文件在 IIS 6.0 和更早版本下可用

> 如果部署使用 RC2 版本生成的 ASP.NET 网页（Razor）应用程序，并且应用程序在 */App\_Data/admin*下包含*password .txt*或*packagesources*文件，则 IIS 6.0 将为该文件提供服务（如果已请求），这可能会公开包管理器实例的密码。 
> 
> **解决方法**将*password .txt*或*packagesources*文件重命名为*password*或*packagesources*。默认情况下，IIS 6.0 不会为扩展名为 *.config*的文件提供服务。 （在 IIS 7 中，不提供*应用\_Data*文件夹中的任何文件，因此你不需要重命名这些文件。）

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>问题：卸载使用 Beta 3 版本安装的包并不完全删除包组件

> 如果在 Beta 3 版本中使用程序包管理器安装了包，然后尝试使用当前版本卸载包，则不会完全卸载包。 使用包管理器的 "**卸载**" 按钮将删除某些组件，但会保留包的库代码，而不会更新*包 .config*文件。
> 
> **解决方法**   
> 执行以下步骤：  
> 1. 删除 *\_Data\packages* "文件夹中的应用。 这将删除所有包。   
> 2. 删除网站根目录中的*包 .config*文件。

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>问题：在 Visual Studio 中，调用基于 web 的包管理器使应用程序脱机

> 如果使用的是 Visual Studio （而不是 WebMatrix），并使用 *\_管理*功能启动包管理器，Visual studio 会使应用程序脱机，并将*应用程序\_脱机。*
> 
> [!NOTE]
> 虽然在使用基于 web 的包管理器界面时，通常会看到此行为，但是，如果你添加、删除或修改*应用\_Data*文件夹中的任何文件，则会发生相同的行为。
> 
> **解决方法**   
> 若要在 Visual Studio 中处理包，请使用 NuGet 扩展，而不是基于 web 的包管理器。 有关信息，请参阅[NuGet 文档](https://docs.microsoft.com/nuget/)。 如果使用的是*应用\_Data*文件夹中的其他文件，请考虑将文件保留在其他位置以避免此问题。 如果这不可行，请手动删除*应用\_脱机 .htm*文件，或等待站点自动重新联机（默认情况下，30秒后）。

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>问题： Visual Studio IntelliSense 和项目模板仅在 ASP.NET MVC 版本3中提供

> 安装 ASP.NET 网页也不会安装适用于 Visual Studio 的工具，例如用于 ASP.NET 网页应用程序的 IntelliSense 和项目模板。
> 
> **解决方法**若要在 Visual Studio 中使用 ASP.NET 网页应用程序的 IntelliSense 和项目模板，请通过 Web 平台安装程序或[独立安装程序](https://go.microsoft.com/fwlink/?LinkID=191797)安装 ASP.NET MVC 3 RC。

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>问题：通过代理服务器读取源或其他外部数据

> 如果运行该站点的服务器位于代理服务器后面，则你可能需要在 web.config 文件中配置代理信息，以便能够读取来自你的站点*之外的信息*。 例如，如果使用 `ReCaptcha` 帮助程序，则帮助者与 reCAPTCHA 服务通信，但可能会被代理服务器阻止。 同样，在 ASP.NET 网页中使用的源（如包管理器使用的源）可能需要代理配置。
> 
> 如果在使用外部服务或使用包源时遇到问题，请将以下元素添加到应用程序*的根 web.config*文件中：
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> 有关配置代理服务器的详细信息，请参阅 MSDN 网站上的[&lt;proxy&gt; 元素（网络设置）](https://msdn.microsoft.com/library/sa91de1e.aspx) 。

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>问题：卸载 .NET Framework 版本4禁用包含 Razor 语法 ASP.NET 网页

> 如果卸载 .NET Framework 版本4，然后重新安装它，则将禁用 Razor 语法的 ASP.NET 网页。 扩展名为 *...* ASP.NET 网页在计算机根*web.config*文件中注册程序集，删除 .NET Framework 删除该文件。 重新安装 .NET Framework 会安装新版本的配置文件，但不会为 ASP.NET 网页程序集添加引用。
> 
> **解决方法**重新安装 .NET Framework 后，请用 Razor 语法重新安装 ASP.NET 网页。 这会将以下元素添加到计算机根目录中的*web.config 文件中，该文件*通常位于以下位置：  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

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
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>问题：将应用程序部署到未安装 SQL Server Compact 的计算机

> 包含 SQL Server Compact 数据库的应用程序可以在未安装 SQL Server Compact 的计算机上运行。 Microsoft WebMatrix 1.0 自动为你复制这些二进制文件，并执行适当的*web.config*文件转换。
> 
> **解决方法**如果需要复制这些文件并手动更改*web.config 文件，* 请执行以下操作：
> 
> 1. 将数据库引擎程序集复制到目标计算机上的应用程序的*Bin*文件夹中（和子文件夹）：  
> 
>    - 复制*C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*   
>      **到** *\bin*
>    - 将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* 复制**到** *\Bin\x86*
>    - 将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* * 复制**到** *\Bin\amd64*
> 
> 2. 在网站的根文件夹中，创建或打开*web.config*文件。 （在 WebMatrix 1.0 中，如果您在 "**选择文件类型**" 对话框中单击 "**全部**"，则此文件类型可用。）
> 3. 添加以下元素作为 `<configuration>` 元素的子元素（不在 `<system.web>` 元素内）：
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>问题： "Database" 和 "WebGrid" 帮助程序在 Visual Basic 的中等信任中不起作用

> 如果使用 Visual Basic （创建*vbhtml*文件），并且将应用程序设置为使用中等信任，则 `Database` 和 `WebGrid` 帮助程序将不起作用。
> 
> **解决方法**  
> 如果你使用 Visual Studio 2010，则可以通过安装 Service Pack 1 版本来解决此问题。 在 SP1 版本的最终版本可用之前，可以从 Microsoft 下载中心的[Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en)页面下载 Sp1 的 Beta 版本。   
>   
> 如果这不可行，或者如果不使用 Visual Studio 2010，可以暂时将应用程序设置为使用完全信任。

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>问题： "ApplicationPart" 资源可从外部访问

> 如果程序集包含从 `ApplicationPart` 类派生的对象，则该程序集的资源由 `ResourceRouteHandler` 类公开。 以下列 URL 为例：  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> 此请求下载*system.web. .dll*程序集中的所有资源字符串。 下载所有嵌入资源（甚至不应作为静态内容提供的资源）。 如果嵌入资源包含敏感信息，这可能会带来安全风险。 
> 
> **解决方法**   
> 如果创建**ApplicationPart**对象，请确保与该**ApplicationPart**对象的程序集关联的嵌入资源不包含敏感信息。

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> 有关 WebMatrix 安装问题的信息，请参阅本文档前面的[WebMatrix 安装问题](#Known_Issues_Installation)。

文档的此部分介绍 WebMatrix 开发环境的已知问题。

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>问题： web.config 文件中的数据库连接字符串的用户名或密码更改不会反映在 "数据库" 工作区中

> **解决方法**  
> 
> 1. *在 web.config 文件中*，更改连接字符串中的数据库名称（例如，将 "1" 添加到该字符串中）。
> 2. 保存 web.config*文件。*
> 3. 单击 "**数据库**和刷新"。
> 4. 将*web.config*文件中的连接字符串中的数据库名称更改回原始数据库名称。
> 5. 保存 web.config*文件。*
> 6. 单击 "**数据库**和刷新"。

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>问题：无法删除 WebMatrix 创建的文件夹

> 如果 WebMatrix 正在使用提升的权限运行（也就是说，使用 Windows 中的 "以**管理员身份运行**" 选项启动 webmatrix），则无法使用 Windows 资源管理器删除 webmatrix 创建的文件夹。
> 
> **解决方法**  
> 使用提升的权限运行 Windows 资源管理器。 请执行这些步骤：  
> 
> 1. 在 Windows 中，单击 "**启动**"。
> 2. 输入 "Windows 资源管理器"，然后右键单击**Windows 资源管理器**的条目。
> 3. 单击 "以**管理员身份运行**"。 然后，你可以删除这些文件夹。

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>问题： WebMatrix 1.0 无法执行需要提升的某些任务

> WebMatrix 1.0 无法执行某些需要提升的任务，例如在下列情况下安装其他组件：
> 
> - 在 Windows Vista 或 Windows 7 上，你使用没有管理权限的帐户登录，并且用户帐户控制（UAC）处于禁用状态。
> - 你使用的是 Microsoft Windows XP 或 Microsoft Windows Server 2003。
> 
> **解决方法**  
> WebMatrix 1.0 中的大多数任务不需要管理权限。 对于这种情况，您可以以管理员身份执行操作，也可以执行以下步骤：
> 
> - 在 Windows Vista 或 Windows 7 上，启用 UAC。
> - 在 Windows XP 上，将用户添加到 "管理员" 安全组。

#### <a name="issue-site-from-web-gallery-is-disabled"></a>问题： "来自 Web 库的网站" 已禁用

> 如果未安装 Web 平台安装程序3.0，则将禁用 "**从 Web 库中站点**" 选项。
> 
> **解决方法**  
> 安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。

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

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>问题：智能感知不适用于 Razor 语法、 C#或 Visual Basic 的 WebMatrix

> 在 WebMatrix 中，HTML 和 CSS 支持 IntelliSense。 但是，它不适用于其他语言。 
> 
> **解决方法**   
> 无。

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>问题： HTML 和 CSS 的 IntelliSense 建议了根据上下文不适当的元素

> WebMatrix 中用于标记的 IntelliSense 支持使用[XHTML 1.0 过渡架构](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional)和 css （使用[css 2.1 架构](http://www.w3.org/TR/CSS2/)）的 HTML。 由于 IntelliSense 基于这些特定的架构，因此可能建议某些标记、属性或属性不适合当前页面或样式定义。 对于 HTML，它还会在可能解释为格式错误的 XHTML 的内容（例如，当标记未关闭时）导致意外的建议。 如果插入点在不完整的标记内，此问题可能更为明显;在这种情况下，IntelliSense 可能会建议新的开始标记或提供其他不正确的建议。 
> 
> **解决方法**   
> 对于 HTML，请确保在格式正确的完整 XHTML 页面中工作。 对于 CSS，没有解决方法。

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>问题：键入时未调用 IntelliSense

> 有时，IntelliSense 可能不会在编辑器中输入 HTML 或 CSS。 具体而言，当插入点直接位于另一个元素或文件的末尾时，可能会发生这种情况。 
> 
> **解决方法**   
> 请确保插入点附近有空白，并且插入点不在文件末尾。 还可以通过按 Ctrl + Space 手动调用 IntelliSense。

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>问题：没有可用于禁用 IntelliSense 的 UI

> WebMatrix 1.0 不提供用于禁用 IntelliSense 的 UI 或手势。 
> 
> **解决方法**   
> 使用以下命令启动 WebMatrix，其中包含禁用 IntelliSense 的开关：  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express 有自己的自述文件，该文件可在以下 URL 中找到：

[https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x804](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact 有自己的自述文件，该文件可在以下 URL 中找到：

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

有关涉及将 SQL Server Compact 作为 WebMatrix 的一部分进行安装的问题的信息，请参阅本文档前面的[WebMatrix 安装问题](#Known_Issues_Installation)。

### <a id="Known_Issues_Installing_Applications"></a>安装应用程序

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>问题：如果将用户的 "我的文档" 文件夹重定向到网络共享，则安装应用程序可能需要较长时间

> **解决方法**  
> 无。 安装应用程序可能需要一些时间，但会正确安装。

### <a id="Known_Issues_Publishing_Applications"></a>发布应用程序

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>问题：发布 SQL Compact 数据库时出现 "无法获取所需的权限" 错误

> WebMatrix 不完全支持将 SQL Server Compact 支持的二进制文件部署到运行 .NET Framework 版本3.5 和中等信任配置的服务器。
> 
> **解决方法**  
> 首选的解决方法是在服务器上安装 .NET Framework 4。 或者，执行以下操作：
> 
> 1. 将以下元素添加到*Web\_MediumTrust*文件中的 `SecurityClasses` 部分：
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. 在*Web\_MediumTrust*文件中创建一个具有以下必需权限的新权限集：
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. 通过在*Web\_MediumTrust*文件中放置以下元素，将权限集应用到 SQL Server Compact：
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>问题：库和 PhpBB web 应用程序在发布后显示 "服务不可用" 错误

> 在某些情况下，发布应用程序会导致 "服务不可用" 错误。
> 
> **解决方法**  
> 在 WebMatrix 中，在 "**发布设置**" 窗口中的服务器名称末尾添加一个反斜杠（\)，然后重新发布该应用程序。

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>问题：发布后，Moodle 网站布局和链接已损坏

> 发布 Moodle 应用程序后，应用程序无法正常工作。
> 
> **解决方法**  
> 在 WebMatrix 中，在 "**发布设置**" 窗口中的 "**站点名称**" 字段的末尾添加一个斜杠（/），然后再次发布该应用程序。

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>问题：发布 nopCommerce 失败，出现数据库错误

> 发布 nopCommerce 失败，并报告数据库错误，如 "插入到 nop\_日志表失败"。
> 
> **解决方法**  
> 
> 1. 在 WebMatrix 中，单击 "**运行**" 以在本地启动 nopCommerce。
> 2. 登录到管理页。
> 3. 单击 "**系统**" 菜单。
> 4. 单击**日志**选项。
> 5. 单击 **“清除日志”** 按钮。
> 6. 再次发布 nopCommerce。

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>问题：当你下载已发布的站点时，Silverstripe CMS 显示 "HTTP 500 PHP HANDLER.FCGI 错误"

> **解决方法**  
> 单击 "**下载已发布网站**" 后，在**发布预览**中跳过 `silverstripe-cache/manifest_main`。 此文件用于缓存目的，并特定于每台计算机。

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>问题：当你下载已发布的站点时，从属显示 "/" 应用程序中的服务器错误 "

> **解决方法**  
> 打开站点的 web.config*文件，* 并将数据库连接字符串中的用户 ID 和密码替换 SQL Server 管理员凭据（"sa" 凭据）。
> 
> 或者，按照以下步骤，为你登录的用户帐户提供 `db_owner` 权限：
> 
> 1. 使用 Web 平台安装程序安装 SQL Server Management Studio。
> 2. 连接到本地 SQL Server Express 实例（默认情况下，`.\SQLEXPRESS`）。
> 3. 单击 "**数据库**" &gt; *[LocalSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] （默认值为 `subtextuser`]，右键单击，然后单击 "**属性**"。
> 4. 在角色成员资格部分中选择 " **db\_所有者**"。

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

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>问题：发布或下载站点后，某些链接在 DotNetNuke 中不可见

> 如果发布或下载 DotNetNuke 站点，则可能需要清除缓存以使新链接显示在站点上。
> 
> **解决方法**
> 
> 1. 以 "主机" 身份登录。
> 2. 中转到 "主机" 菜单并选择 "**主机设置**"。
> 3. 向下滚动，在 "**高级设置**" 下，展开 "**性能设置**"。
> 4. 单击 "**清除缓存**" 链接以获取页面。
> 5. 请切换到页面底部，然后重新启动应用程序。

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>问题：下载已发布站点后，AtomSite 中的某些链接已中断

> **解决方法**  
> 在*service .config*文件、*用户 .config*文件和所有 *.XML*文件中，将 URL 字符串（例如 `http://myhost.com/atomsite`）替换为本地（例如，`http://localhost:1239`）。

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>问题：基于 MySQL 的应用程序（如 WordPress）无法发布和报告数据库错误

> 默认情况下，WebMatrix 使用 UTF-8 字符集安装 MySQL。 如果自己安装 MySQL，而字符集不是 UTF-8 （例如，它是 Latin1-general），则数据库的发布过程可能会失败。
> 
> **解决方法**
> 
> 1. 将 MySQL 字符集设置为 UTF-8。 （有关详细信息，请参阅 MySQL 网站上的[服务器字符集和排序规则](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html)。）
> 2. 重新安装应用程序。
> 3. 重新发布应用程序。

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>问题：对于具有基于浏览器的安装程序的应用程序，"下载已发布的站点" 失败

> 某些应用程序（例如，Kentico CMS）要求您在浏览器中启动这些应用程序，以便执行安装后的安装程序（如创建数据库）。 如果在不完成基于浏览器的安装的情况下发布了此类应用程序，则尝试从远程服务器下载相同的站点将会失败。
> 
> **解决方法**  
> 在发布站点之前，请完成基于浏览器的设置。

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>问题： "下载已发布站点" 失败，并出现针对 DotNetNuke 和 Kooboo CMS 的数据库错误

> 如果尝试从服务器下载应用程序，并且在 "**发布设置**" 对话框中的数据库连接字符串中具有管理员凭据，则在发布日志中可能会看到以下错误：
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **解决方法**  
> 如果可行，请使用数据库的非管理员凭据重新发布站点（或已发布）。

<a id="More_Info"></a>

## <a name="for-more-information"></a>更多信息

有关 WebMatrix 1.0 的详细信息，请参阅以下网站：

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© 2011 Microsoft Corporation。 保留所有权利。 [使用条款](https://msdn.microsoft.cos/cc300389.aspx)。
