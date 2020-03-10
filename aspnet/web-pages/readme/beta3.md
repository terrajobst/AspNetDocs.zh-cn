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
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="6b7d8-103">Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件</span><span class="sxs-lookup"><span data-stu-id="6b7d8-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

> <span data-ttu-id="6b7d8-104">Web Matrix 和 ASP.NET 网页 (Razor) Beta 3 版本自述文件</span><span class="sxs-lookup"><span data-stu-id="6b7d8-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="6b7d8-105">11月9日2010</span><span class="sxs-lookup"><span data-stu-id="6b7d8-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="6b7d8-106">内容</span><span class="sxs-lookup"><span data-stu-id="6b7d8-106">Contents</span></span>

- [<span data-ttu-id="6b7d8-107">概述</span><span class="sxs-lookup"><span data-stu-id="6b7d8-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="6b7d8-108">安装</span><span class="sxs-lookup"><span data-stu-id="6b7d8-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="6b7d8-109">Beta 3 版本中的新功能、更改和已知问题</span><span class="sxs-lookup"><span data-stu-id="6b7d8-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="6b7d8-110">WebMatrix 安装问题</span><span class="sxs-lookup"><span data-stu-id="6b7d8-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="6b7d8-111">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="6b7d8-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="6b7d8-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="6b7d8-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="6b7d8-113">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="6b7d8-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="6b7d8-114">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="6b7d8-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="6b7d8-115">其他问题</span><span class="sxs-lookup"><span data-stu-id="6b7d8-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="6b7d8-116">更多信息</span><span class="sxs-lookup"><span data-stu-id="6b7d8-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="6b7d8-117">概述</span><span class="sxs-lookup"><span data-stu-id="6b7d8-117">Overview</span></span>

> <span data-ttu-id="6b7d8-118">Microsoft WebMatrix Beta 是一个免费的 web 开发堆栈，只需几分钟即可完成安装。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="6b7d8-119">它将 web 服务器与数据库和编程框架相集成，以创建单一、集成的体验。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="6b7d8-120">你可以使用 WebMatrix Beta 来简化你的代码、测试和发布你自己的 ASP.NET 或 PHP 网站的方式，也可以使用 WebMatrix Beta 来使用常见开源应用（如 DotNetNuke、Umbraco、WordPress 或 Joomla）启动新网站。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="6b7d8-121">WebMatrix Beta 使用的功能强大的 web 服务器、数据库引擎和框架环境将在 internet 上运行你的网站，这使得从开发到生产的过渡顺畅顺畅。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="6b7d8-122">安装</span><span class="sxs-lookup"><span data-stu-id="6b7d8-122">Installation</span></span>

> <span data-ttu-id="6b7d8-123">若要安装 WebMatrix Beta 3，请使用[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="6b7d8-124">安装 Web 平台安装程序后，可以使用它来安装 WebMatrix Beta 3。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="6b7d8-125">如果在安装过程中遇到问题，请参阅[Microsoft Web 平台安装程序的疑难解答问题](https://go.microsoft.com/fwlink/?LinkId=196212)。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="6b7d8-126">有关发布应用程序的说明</span><span class="sxs-lookup"><span data-stu-id="6b7d8-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="6b7d8-127">请参阅[发布应用程序的分步说明](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="6b7d8-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="6b7d8-128">新功能、更改、andKnown 问题</span><span class="sxs-lookup"><span data-stu-id="6b7d8-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="6b7d8-129">WebMatrix Beta 3 安装</span><span class="sxs-lookup"><span data-stu-id="6b7d8-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="6b7d8-130">问题： WebMatrix Beta 3 仅适用于支持 Microsoft .NET Framework 4 的平台</span><span class="sxs-lookup"><span data-stu-id="6b7d8-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="6b7d8-131">WebMatrix Beta 版需要 .NET Framework 版本4。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="6b7d8-132">在某些情况下，WebMatrix Beta 安装程序将允许你尝试在不属于受支持的配置集的平台上安装。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="6b7d8-133">具体而言，如果没有 SP1 更新，Windows Vista 将允许你开始安装 WebMatrix Beta，但 .NET Framework 4 组件将失败并阻止你的安装。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="6b7d8-134">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-134">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-135">在支持的平台上安装，其中包括：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="6b7d8-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="6b7d8-136">Windows 7</span></span>
> - <span data-ttu-id="6b7d8-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="6b7d8-137">Windows Server 2008</span></span>
> - <span data-ttu-id="6b7d8-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="6b7d8-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="6b7d8-139">Windows Vista SP1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="6b7d8-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="6b7d8-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="6b7d8-140">Windows XP SP3</span></span>
> - <span data-ttu-id="6b7d8-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="6b7d8-141">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="6b7d8-142">问题：如果在未 Microsoft Visual Studio 2008 SP1 的情况下安装 Microsoft Visual Studio 2008，将无法安装 WebMatrix Beta 3</span><span class="sxs-lookup"><span data-stu-id="6b7d8-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="6b7d8-143">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-143">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-144">从 Microsoft 下载中心安装[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="6b7d8-145">问题： GAC 中未安装 SQL Server Compact 4.0 的某些程序集</span><span class="sxs-lookup"><span data-stu-id="6b7d8-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="6b7d8-146">在64位计算机上安装 SQL Server Compact 4.0，并且计算机仅安装了 .NET Framework 3.5 SP1 客户端配置文件时，SQL Server Compact 4.0 的托管程序集不会放置在全局程序集缓存（GAC）中。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="6b7d8-147">GAC 中未安装的托管程序集包括：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="6b7d8-148">*System.data.sqlserverce* （ADO.NET 提供程序）</span><span class="sxs-lookup"><span data-stu-id="6b7d8-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="6b7d8-149">*System.web. system.data.sqlserverce* （ADO.NET 实体框架）</span><span class="sxs-lookup"><span data-stu-id="6b7d8-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="6b7d8-150">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-150">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-151">卸载 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="6b7d8-152">从以下位置下载并安装 .NET Framework 3.5 SP1 的完整版本：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="6b7d8-153">Microsoft .NET Framework 3.5 Service pack 1 （完整程序包）</span><span class="sxs-lookup"><span data-stu-id="6b7d8-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="6b7d8-154">然后重新安装 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-154">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="6b7d8-155">问题：无法使用命令行卸载 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="6b7d8-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="6b7d8-156">使用命令行选项卸载 SQL Server Compact 在此版本中不起作用。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="6b7d8-157">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-157">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-158">使用 Windows 控制面板中的 "*程序和功能*" 卸载 Microsoft SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="6b7d8-159">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="6b7d8-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="6b7d8-160">本部分介绍与 Razor 语法 ASP.NET 网页的 Beta 3 版本的新功能、更改和已知问题。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="6b7d8-161">新增功能</span><span class="sxs-lookup"><span data-stu-id="6b7d8-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="6b7d8-162">更改</span><span class="sxs-lookup"><span data-stu-id="6b7d8-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="6b7d8-163">问题</span><span class="sxs-lookup"><span data-stu-id="6b7d8-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="6b7d8-164">Beta 3 中的新增功能，适用于带有 Razor 语法的 ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="6b7d8-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="6b7d8-165">New： ".Html" 方法呈现未编码的标记</span><span class="sxs-lookup"><span data-stu-id="6b7d8-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="6b7d8-166">利用新的 `Html.Raw` 方法，你可以将 HTML 标记呈现为标记，而不是呈现编码的输出。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="6b7d8-167">（默认情况下，ASP.NET Razor 在呈现字符串之前对其进行编码。）语法为：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="6b7d8-168">下面的示例演示如何使用 `Html.Raw`：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="6b7d8-169">Beta 3 中针对具有 Razor 语法 ASP.NET 网页的更改</span><span class="sxs-lookup"><span data-stu-id="6b7d8-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="6b7d8-170">Change：已删除 "HrefAttribute" 方法</span><span class="sxs-lookup"><span data-stu-id="6b7d8-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="6b7d8-171">已移除 `WebPage` 类的 `HrefAttribute` 方法。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="6b7d8-172">此帮助程序用于对 Url 中的不安全字符进行编码。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="6b7d8-173">不再需要此方法，因为 ASP.NET Razor 会自动对字符串进行编码。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="6b7d8-174">（使用新的 `Html.Raw` 方法呈现未编码的字符串。）</span><span class="sxs-lookup"><span data-stu-id="6b7d8-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="6b7d8-175">更改：声明性 "@helper" 帮助器的语法已更改</span><span class="sxs-lookup"><span data-stu-id="6b7d8-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="6b7d8-176">在 Beta 3 版本中，ASP.NET 更改了如何分析使用 `@helper` 语法创建的帮助器。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="6b7d8-177">实质上，`@helper` 语法现在被分析为代码块，而不是一个可包含代码的标记块。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="6b7d8-178">因此，帮助器内的代码不需要包含在 `@{ }` 块中。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="6b7d8-179">相反，帮助器中的标记必须显式包含在 HTML 元素中或 ASP.NET Razor `<text></text>` 标记中。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="6b7d8-180">例如，以下 `@helper` 语法适用于 Beta 3 版本：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="6b7d8-181">在 Beta 3 版本中，必须更改此帮助程序，使其类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="6b7d8-182">请注意，不再使用助手中初始代码周围的 `@{ }` 字符。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="6b7d8-183">这是因为默认情况下，帮助器的内容被视为代码块。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="6b7d8-184">帮助器呈现标记，该标记以开始 `<a>` 标记开头。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="6b7d8-185">如果帮助程序必须呈现纯文本或不包括结束标记的标记（例如 `<meta>` 标记），则要呈现的内容必须位于 `<text></text>` 标记中。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>

#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="6b7d8-186">更改：已删除 "WebPageContext"</span><span class="sxs-lookup"><span data-stu-id="6b7d8-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="6b7d8-187">`WebPageContext.HttpContext` 属性已被删除。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="6b7d8-188">请改用 `HttpContext.Current`。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="6b7d8-189">（`WebPageContext.HttpContext` 属性仅包装此。）</span><span class="sxs-lookup"><span data-stu-id="6b7d8-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>

#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="6b7d8-190">更改：已将 "Facebook" 帮助器移动到新包</span><span class="sxs-lookup"><span data-stu-id="6b7d8-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="6b7d8-191">`Facebook` 帮助程序已移动到*Facebook. 帮助*程序库，其中包括 `Facebook` 帮助程序和附加功能。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="6b7d8-192">必须以单独的包的形式安装此库，如教程[入门使用 ASP.NET 页面](https://go.microsoft.com/fwlink/?LinkId=202889)中的 "使用程序包管理器安装帮助程序" 中所述。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="6b7d8-193">更改：成员身份、角色和安全类型会移到新程序集</span><span class="sxs-lookup"><span data-stu-id="6b7d8-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="6b7d8-194">以下类型已移动到 `WebMatrix.WebData` 程序集：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="6b7d8-195">Change： "TagBuilder" 类已移动到 System.web .dll 程序集</span><span class="sxs-lookup"><span data-stu-id="6b7d8-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="6b7d8-196">`TagBuilde` r 类已移动到 System.web .dll 程序集。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="6b7d8-197">以前，此程序集位于作为 ASP.NET MVC 一部分的程序集中。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="6b7d8-198">此更改意味着无需安装 ASP.NET MVC 即可使用 `TagBuilder` 类。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="6b7d8-199">但是，该类仍处于 `System.Web.Mvc` 命名空间中。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="6b7d8-200">为了使用 `TagBuilder` 类（例如，在自定义 ASP.NET Razor 帮助器中），必须引用命名空间（例如，通过将 `@using System.Web.Mvc` 添加到代码中）。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="6b7d8-201">更改：请求验证语法已更改;已删除 "验证" 类</span><span class="sxs-lookup"><span data-stu-id="6b7d8-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="6b7d8-202">在 Beta 3 版本中，若要禁用单个字段或一组字段的验证，可以调用 `Validation.Exclude` 方法，并传入要从验证中排除的字段名称或名称。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="6b7d8-203">Beta 3 版本中提供了一个新语法，用于绕过验证。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="6b7d8-204">已删除 Beta 3 中使用的 `Validation` 方法。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="6b7d8-205">如果未禁用请求验证，则用户尝试上传 HTML 标记（例如，通过在页面上使用 rtf 文本编辑器），该网站将报告错误，如*潜在的危险请求。从客户端检测到表单值*，并且不接受用户输入。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="6b7d8-206">如果禁用请求验证，则必须手动检查用户输入，以确保它不会使用类似[Microsoft 反跨站点脚本库 v4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)的内容来包含潜在的危险标记或脚本。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="6b7d8-207">若要禁用自动请求验证，请调用 `Request.Unvalidated` 方法，并向其传递要绕过请求验证的字段或其他 post 对象的名称。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="6b7d8-208">您可以使用此方法绕过对 `Form`、`QueryString`、`Cookies`和 `ServerVariables` 集合中任何项的验证。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="6b7d8-209">下面的示例演示如何使用 `Unvalidated` 方法：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="6b7d8-210">用 Razor 语法 ASP.NET 网页的已知问题</span><span class="sxs-lookup"><span data-stu-id="6b7d8-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="6b7d8-211">问题：将自定义用户表用于成员身份时出现意外行为</span><span class="sxs-lookup"><span data-stu-id="6b7d8-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="6b7d8-212">若要初始化 ASP.NET Razor 网站的成员资格提供程序，请调用 `WebSecurity.InitializeDatabaseConnection` 方法。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="6b7d8-213">（在 WebMatrix 中，初学者站点模板在 *\_AppStart*文件中包含对此方法的调用。）如果此方法的 `autoCreateTables` 参数设置为 true （默认情况下，它在 Starter Site 模板中设置为 true），并且如果将无法识别的表名传递给方法（第二个参数），则此方法不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="6b7d8-214">相反，它会自动创建表。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="6b7d8-215">如果要将自定义用户表用于成员身份，但将错误的表名传递到 `WebSecurity.InitializeDatabaseConnection` 方法，这可能是一个问题。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="6b7d8-216">由于方法默认情况下不会引发错误，因此，如果您指定的表不存在，而是创建新表，则该应用程序可能看起来正在运行。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="6b7d8-217">但是，依赖于自定义用户表的应用程序代码（以及其中的字段）最终可能会失败，并出现意外错误。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="6b7d8-218">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-218">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-219">请确保 `InitializeDatabaseConnection` 方法中传递的名称与成员资格数据库中的用户配置文件表匹配，或者确保 `autoCreateTables` 参数设置为 false。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="6b7d8-220">问题： "未能生成 SQL Server 的用户实例" 错误</span><span class="sxs-lookup"><span data-stu-id="6b7d8-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="6b7d8-221">如果 WebMatrix Web 应用程序使用 SQL Server Express 并且在 Windows 7 或 Windows Server 2008 R2 上运行 IIS 7.5，你可能会看到一个错误，指示 SQL Server 无法在运行时检索用户的本地应用程序路径。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="6b7d8-222">**解决方法**请确保应用程序在其下运行的 Windows 帐户（通常为网络服务）对应用程序的根文件夹和子文件夹（例如*应用程序\_数据*）具有读/写权限。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="6b7d8-223">[SQL Server Express 用户实例化和 ASP.net Web 应用程序项目](https://support.microsoft.com/kb/2002980)的知识库文章问题中提供了更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="6b7d8-224">问题：在 Visual Studio 中，自定义程序集（Dll）的命名空间不会自动导入</span><span class="sxs-lookup"><span data-stu-id="6b7d8-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="6b7d8-225">如果你在 Visual Studio 的项目中使用自定义程序集，则在设计时不会自动导入在这些程序集中声明的命名空间。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="6b7d8-226">因此，在设计时可能无法识别对自定义类型的引用，并在 Visual Studio 中将其标记为无法识别（使用 "波形曲线"）。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="6b7d8-227">此问题仅发生在 Visual Studio 中的设计时;应用程序本身会正常运行。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="6b7d8-228">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-228">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-229">包括引用在设计时无法识别的实体的 `using` 语句（`imports` 在 Visual Basic 中）。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="6b7d8-230">问题： Visual Studio IntelliSense 和项目模板仅在 ASP.NET MVC 版本3中提供</span><span class="sxs-lookup"><span data-stu-id="6b7d8-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="6b7d8-231">安装 ASP.NET 网页也不会安装适用于 Visual Studio 的工具，例如用于 ASP.NET 网页应用程序的 IntelliSense 和项目模板。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="6b7d8-232">**解决方法**若要在 Visual Studio 中使用 ASP.NET 网页应用程序的 IntelliSense 和项目模板，请通过 Web 平台安装程序或[独立安装程序](https://go.microsoft.com/fwlink/?LinkID=191797)安装 ASP.NET MVC 3 RC。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="6b7d8-233">问题： "找不到&lt;helper&gt; 类" 错误</span><span class="sxs-lookup"><span data-stu-id="6b7d8-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="6b7d8-234">升级到 Beta 3 后，可能会看到一个错误，指出找不到帮助程序类（例如，`Facebook` 类）。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="6b7d8-235">从 Beta 2 开始，在 Beta 3 中继续，帮助程序已移动到必须显式安装的包。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="6b7d8-236">不会升级现有站点以包含这些包;这包括 *\My Documents\IISExpress*或 *\My Documents\My 网站*文件夹中的网站。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="6b7d8-237">具体而言，如果使用 "*我的网站*" （WebSite1）中的默认网站（包括对 `Twitter` 帮助程序的引用），将看到此错误。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="6b7d8-238">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-238">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-239">注释掉对站点中任何帮助程序的调用，运行 *\_管理*页，然后安装包含要使用的帮助程序的一个或一些包。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="6b7d8-240">安装包后，可以取消注释引用帮助器的行。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="6b7d8-241">问题：将 Beta 3 ASP.NET Razor 程序集部署到 Bin 文件夹在托管网站上可能不起作用</span><span class="sxs-lookup"><span data-stu-id="6b7d8-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="6b7d8-242">如果将 ASP.NET 网页网站部署到宿主站点，并且将 ASP.NET Razor Beta 3 程序集部署到站点的*Bin*文件夹，则可能会遇到错误，包括以下内容：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="6b7d8-243">如果宿主提供程序已将 ASP.NET 网页 Beta 1 程序集安装到服务器的全局应用程序缓存（GAC）中，则可能会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="6b7d8-244">GAC 中的程序集优先于在*Bin*文件夹中本地安装的程序集。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="6b7d8-245">**解决方法**请与您的宿主提供商联系，以确认您所遇到的错误是由提供程序的程序集版本和您的程序集版本之间的冲突引起的。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="6b7d8-246">如果是这样，则请求宿主提供程序更新服务器的 GAC 中的程序集。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="6b7d8-247">问题：通过代理服务器读取源或其他外部数据</span><span class="sxs-lookup"><span data-stu-id="6b7d8-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="6b7d8-248">如果运行该站点的服务器位于代理服务器后面，则你可能需要在 web.config 文件中配置代理信息，以便能够读取来自你的站点*之外的信息*。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="6b7d8-249">例如，如果使用 `ReCaptcha` 帮助程序，则帮助者与 reCAPTCHA 服务通信，但可能会被代理服务器阻止。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="6b7d8-250">同样，在 ASP.NET 网页中使用的源（如包管理器使用的源）可能需要代理配置。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="6b7d8-251">如果在使用外部服务或使用包源时遇到问题，请将以下元素添加到应用程序*的根 web.config*文件中：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="6b7d8-252">有关配置代理服务器的详细信息，请参阅 MSDN 网站上的[&lt;proxy&gt; 元素（网络设置）](https://msdn.microsoft.com/library/sa91de1e.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="6b7d8-253">问题： "无法加载" "。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="6b7d8-254">如果以前安装了 Beta 1 版本的 ASP.NET 网页与 Razor 语法，然后安装 Beta 3 版本，则所有适当的程序集都将安装到 GAC 中 *，但不包括：*</span><span class="sxs-lookup"><span data-stu-id="6b7d8-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="6b7d8-255">因此，当你运行 ASP.NET Razor 页面时，你将看到一个错误，指示无法加载*Microsoft* 。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="6b7d8-256">如果在干净的计算机上加载 Beta 3 版本，则不会出现此问题。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="6b7d8-257">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-257">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-258">在 "控制面板" 中，卸载 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="6b7d8-259">然后重新安装 Beta 3 版本。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-259">Then reinstall the Beta 3 release.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="6b7d8-260">问题：卸载 .NET Framework 版本4禁用包含 Razor 语法 ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="6b7d8-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="6b7d8-261">如果卸载 .NET Framework 版本4，然后重新安装它，则将禁用 Razor 语法的 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="6b7d8-262">扩展名为 *...*</span><span class="sxs-lookup"><span data-stu-id="6b7d8-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="6b7d8-263">ASP.NET 网页在计算机根*web.config*文件中注册程序集，删除 .NET Framework 删除该文件。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="6b7d8-264">重新安装 .NET Framework 会安装新版本的配置文件，但不会为 ASP.NET 网页程序集添加引用。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="6b7d8-265">**解决方法**重新安装 .NET Framework 后，请用 Razor 语法重新安装 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="6b7d8-266">这会将以下元素添加到计算机根目录中的*web.config 文件中，该文件*通常位于以下位置：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="6b7d8-267">问题：以前在 Bin 文件夹中用 ASP.NET 程序集部署的应用程序遇到错误</span><span class="sxs-lookup"><span data-stu-id="6b7d8-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="6b7d8-268">在部署期间，ASP.NET 网页程序集（例如， *.dll*）的副本将复制到服务器上网站的*Bin*文件夹中。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="6b7d8-269">（这可能是在部署过程中自动发生的，也可能是因为开发人员显式复制了这些程序集。）但是，当安装 Beta 3 版本时，会发生错误，如找不到某些类型的错误。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="6b7d8-270">出现这种情况的原因是，许多 ASP.NET 网页类型已移入到 Beta 3 版本的不同命名空间中。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="6b7d8-271">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="6b7d8-271">**Workaround** </span></span>  
> <span data-ttu-id="6b7d8-272">清除部署的应用程序的*Bin*文件夹，将新的程序集复制到该文件夹（或重新部署应用程序），然后重新启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="6b7d8-273">问题：无扩展名 Url 在 IIS 7 或 IIS 7.5 上找不到. cshtml/vbhtml 文件</span><span class="sxs-lookup"><span data-stu-id="6b7d8-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="6b7d8-274">在 IIS 7 或 IIS 7.5 上，使用如下所示的 URL 的请求将无法*找到扩展名为* *.*</span><span class="sxs-lookup"><span data-stu-id="6b7d8-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="6b7d8-275">出现此问题的原因是，IIS 7 或 IIS 7.5 默认情况下未启用 URL 重写。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="6b7d8-276">Likeliest 方案是，使用 IIS Express 在本地进行测试时不会出现问题，但在将网站部署到托管网站时，你会遇到此问题。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="6b7d8-277">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="6b7d8-278">如果你可以控制服务器计算机，则在服务器计算机上安装更新中所述的更新[可使某些 IIS 7.0 或 IIS 7.5 处理程序处理其 url 不以句点结尾的请求](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="6b7d8-279">如果无法控制服务器计算机（例如，部署到托管网站），请将以下内容添加*到网站的 web.config 文件中*：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="6b7d8-280">问题：在同一应用程序中使用 Web 应用程序项目或 ASP.NET MVC 和 ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="6b7d8-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="6b7d8-281">如果在 Web 应用程序项目或 ASP.NET MVC 应用程序中使用 ASP.NET 网页，则可能会出现*WebPageHttpApplication*找不到的错误。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="6b7d8-282">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-282">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-283">如果收到此错误，请更改应用程序派生自的基类。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="6b7d8-284">在*global.asax*文件中，更改以下行：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="6b7d8-285">更改为：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="6b7d8-286">这实际上会反转使用 Razor 语法的 ASP.NET 网页 Beta 1 版本引入的更改。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="6b7d8-287">问题：将应用程序部署到未安装 SQL Server Compact 的计算机</span><span class="sxs-lookup"><span data-stu-id="6b7d8-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="6b7d8-288">包含 SQL Server Compact 数据库的应用程序可以在未安装 SQL Server Compact 的计算机上运行。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="6b7d8-289">Microsoft WebMatrix Beta 3 会自动复制这些二进制文件，并执行适当的*web.config*文件转换。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="6b7d8-290">**解决方法**如果需要复制这些文件并手动更改*web.config 文件，* 请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="6b7d8-291">将数据库引擎程序集复制到目标计算机上的应用程序的*Bin*文件夹中（和子文件夹）：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="6b7d8-292">将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*复制**到** *\bin*</span><span class="sxs-lookup"><span data-stu-id="6b7d8-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="6b7d8-293">将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* \* 复制**到** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="6b7d8-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="6b7d8-294">将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \* 复制**到** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="6b7d8-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="6b7d8-295">在网站的根文件夹中，创建或打开*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="6b7d8-296">（在 WebMatrix Beta 3 中，如果您在 "**选择文件类型**" 对话框中单击 "**全部**"，则此文件类型可用。）</span><span class="sxs-lookup"><span data-stu-id="6b7d8-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="6b7d8-297">添加以下元素作为 **&lt;配置&gt;** 元素的子元素（不在 **&lt;system.web&gt;** 元素内）：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="6b7d8-298">问题：数据库和 WebGrid 帮助程序在 Visual Basic 的中等信任环境中不起作用</span><span class="sxs-lookup"><span data-stu-id="6b7d8-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="6b7d8-299">如果使用 Visual Basic （创建*vbhtml*文件），并且将应用程序设置为使用中等信任，则 `Database` 和 `WebGrid` 帮助程序将不起作用。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="6b7d8-300">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-300">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-301">暂时将应用程序设置为使用完全信任。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="6b7d8-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="6b7d8-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="6b7d8-303">问题： "加密" 属性无法识别</span><span class="sxs-lookup"><span data-stu-id="6b7d8-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="6b7d8-304">SQL Server Compact 4.0 无法识别 `SqlCeConnection` 类的 `Encrypt` 属性。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="6b7d8-305">不应使用此属性来加密数据库文件。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="6b7d8-306">`Encrypt` 属性在 SQL Server Compact 3.5 版本中已弃用，并且仅为向后兼容性而保留。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="6b7d8-307">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-307">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-308">使用 `SqlCeConnection` 类的 `Encryption Mode` 属性来加密 SQL Server Compact 4.0 数据库文件。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="6b7d8-309">下面的示例演示如何使用 `Encryption Mode` 属性创建加密的 SQL Server Compact 4.0 数据库：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="6b7d8-310">若要更改现有 SQL Server Compact 4.0 数据库的加密模式，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="6b7d8-311">若要对未加密的 SQL Server Compact 4.0 数据库进行加密，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="6b7d8-312">问题：需要 Microsoft C++ Visual 2008 运行时库</span><span class="sxs-lookup"><span data-stu-id="6b7d8-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="6b7d8-313">SQL Server Compact 4.0 的本机 Dll 需要 Microsoft Visual C++ 2008 运行时库（X86、IA64 和 X64） Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="6b7d8-314">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-314">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-315">安装 .NET Framework 3.5 SP1。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="6b7d8-316">这也会安装 Visual C++ 2008 运行时库 SP1。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="6b7d8-317">可以从以下位置下载库：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="6b7d8-318">Microsoft Visual C++ 2008 Service Pack 1 可再发行组件包 ATL 安全更新</span><span class="sxs-lookup"><span data-stu-id="6b7d8-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="6b7d8-319">请注意，安装 .NET Framework 2.0、3.0 或*4 不会安装 Visual* C++ 2008 运行时库 SP1。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="6b7d8-320">问题：如果在计算机上安装 .NET Framework 之前安装 SQL Server Compact，则其提供程序固定名称未在 .NET Framework machine.config 文件中注册</span><span class="sxs-lookup"><span data-stu-id="6b7d8-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="6b7d8-321">SQL Server Compact 可以安装在未安装 .NET Framework 的计算机上，因为 SQL Server Compact 需要 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="6b7d8-322">如果在安装 SQL Server Compact 之前，不会安装 .NET Framework 版本3.5 和4，SQL Server Compact 安装程序不*会在 machine.config 文件中*注册其提供程序固定名称。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="6b7d8-323">任何依赖于*machine.config*文件中的 SQL Server Compact 条目的应用程序都将失败。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="6b7d8-324">*Machine.config*中的固定名称注册条目类似于以下示例：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="6b7d8-325">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-325">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-326">卸载 SQL Server Compact 4.0 CTP1。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="6b7d8-327">从以下位置下载并安装 .NET Framework 的完整版本：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="6b7d8-328">Microsoft .NET Framework 3.5 Service pack 1 （完整程序包）</span><span class="sxs-lookup"><span data-stu-id="6b7d8-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="6b7d8-329">Microsoft .NET Framework 4.0 版本（完整包）</span><span class="sxs-lookup"><span data-stu-id="6b7d8-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="6b7d8-330">然后重新安装[SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="6b7d8-331">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="6b7d8-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="6b7d8-332">问题：如果将用户的 "我的文档" 文件夹重定向到网络共享，则安装应用程序可能需要较长时间</span><span class="sxs-lookup"><span data-stu-id="6b7d8-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="6b7d8-333">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-333">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-334">无。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-334">None.</span></span> <span data-ttu-id="6b7d8-335">安装应用程序可能需要一些时间，但会正确安装。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-335">The application might take a while to install, but will install correctly.</span></span>

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="6b7d8-336">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="6b7d8-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="6b7d8-337">问题：如果 "目标 URL" 字段未使用 http://或 https://作为前缀，则站点可能无法正常工作</span><span class="sxs-lookup"><span data-stu-id="6b7d8-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="6b7d8-338">在 "**发布设置**" 对话框中，如果目标 URL 不以 `http://` 或 `https://`开头，则该站点在部署后可能不起作用。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="6b7d8-339">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-339">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-340">请确保在发布站点之前，"**发布设置**" 对话框中的 "目标 URL" 以 `http://` 或 `https://`开头。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="6b7d8-341">问题：发布 MySQL 数据库失败，出现错误 "无法发布数据库。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="6b7d8-342">如果远程数据库无法运行该脚本，就会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="6b7d8-343">发生此错误的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="6b7d8-344">出现此错误的原因之一是，数据库脚本包含单引号字符（'），目标 MySQL 数据库的默认字符集不是 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="6b7d8-345">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-345">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-346">将远程 MySQL 数据库的默认字符集设置为 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="6b7d8-347">其他问题</span><span class="sxs-lookup"><span data-stu-id="6b7d8-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="6b7d8-348">问题： "搜索/筛选" 在 "分组依据" 的报表中不起作用：问题类型</span><span class="sxs-lookup"><span data-stu-id="6b7d8-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="6b7d8-349">当你为站点运行报表时，如果你在 "*按 URL 筛选*" 框中输入文本，然后单击 "*搜索*"，则不会发生任何事情。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="6b7d8-350">这是因为，当报表的 "*分组依据*" 状态设置为 "*问题类型*" （默认值）时，此控件不起作用。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="6b7d8-351">**解决方法**在功能区的 "*分组依据*" 选项卡中，单击 " *URL* "，按源 url 对条目分组。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="6b7d8-352">在处于此状态时，文本框和用于筛选条目的按钮是正常的。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-352">The text box and button to filter the entries are functional while in this state.</span></span>

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="6b7d8-353">问题： WCF 应用程序无法与 IIS Express 一起运行</span><span class="sxs-lookup"><span data-stu-id="6b7d8-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="6b7d8-354">浏览到 WCF 应用程序会导致错误，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="6b7d8-355">*无法加载文件或程序集 "7.0.0.0，Version =，Culture = 中立，PublicKeyToken = 31bf3856ad364e35" 或其依赖项之一。系统找不到指定的文件。*</span><span class="sxs-lookup"><span data-stu-id="6b7d8-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="6b7d8-356">出现这种情况的原因是 IIS Express Beta 版本默认情况下不支持 WCF。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="6b7d8-357">**解决方法**使用以下解决方法之一（解决方法 #2 需要 Microsoft Windows Vista 或更高版本）：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="6b7d8-358">将*microsoft. .dll*和 *.dll*程序集从 WebMatrix 安装位置复制到 WCF 应用程序的*bin*目录。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="6b7d8-359">默认情况下，WebMatrix 安装在系统的*Program Files*文件夹下的*Microsoft WebMatrix*子文件夹中。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="6b7d8-360">在 Microsoft Windows Vista 或更高版本上，使用以下命令在*bin*目录中创建程序集的符号链接。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="6b7d8-361">（此方法的优点是不会创建程序集的副本。）</span><span class="sxs-lookup"><span data-stu-id="6b7d8-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="6b7d8-362">在 GAC 中安装两个程序集。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="6b7d8-363">在提升的提示符下运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="6b7d8-364">问题： WebMatrix Beta 3 无法执行需要提升的某些任务</span><span class="sxs-lookup"><span data-stu-id="6b7d8-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="6b7d8-365">WebMatrix Beta 3 无法执行某些需要提升的任务，例如在下列情况下安装其他组件：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="6b7d8-366">在 Windows Vista 或 Windows 7 上，你使用没有管理权限的帐户登录，并且用户帐户控制（UAC）处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="6b7d8-367">你使用的是 Microsoft Windows XP 或 Microsoft Windows Server 2003。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="6b7d8-368">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-368">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-369">WebMatrix Beta 3 中的大多数任务不需要管理权限。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="6b7d8-370">对于这种情况，您可以以管理员身份执行操作，也可以执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="6b7d8-371">在 Windows Vista 或 Windows 7 上，启用 UAC。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="6b7d8-372">在 Windows XP 上，将用户添加到 "管理员" 安全组。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-372">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="6b7d8-373">问题： "来自 Web 库的网站" 已禁用</span><span class="sxs-lookup"><span data-stu-id="6b7d8-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="6b7d8-374">如果未安装 Web 平台安装程序3.0，则将禁用 "**从 Web 库中站点**" 选项。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="6b7d8-375">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-375">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-376">安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="6b7d8-377">问题：在 Windows Server 2003 上，不为非管理用户启动 IIS Express</span><span class="sxs-lookup"><span data-stu-id="6b7d8-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="6b7d8-378">在 Windows Server 2003 上，启动页面或启动 IIS Express 时，IIS Express 不会启动。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="6b7d8-379">对于网页，将显示一条错误，指示该应用程序已由非管理用户启动。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="6b7d8-380">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-380">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-381">以管理用户身份启动 WebMatrix Beta 3。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="6b7d8-382">有关更多详细信息，请参阅以下知识库文章：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="6b7d8-383">非管理用户启动的应用程序无法侦听在 Windows Vista、Windows Server 2003 或 Windows XP 中运行该应用程序的计算机的 HTTP 通信。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="6b7d8-384">问题： Google Chrome 不可用作运行选项</span><span class="sxs-lookup"><span data-stu-id="6b7d8-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="6b7d8-385">"**主页**" 选项卡上的 "**运行**" 下的浏览器列表中不显示 Google Chrome。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="6b7d8-386">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-386">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-387">某些版本的 Google Chrome 不会正确地通过 Windows 中的 "默认程序" 功能进行注册。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="6b7d8-388">作为一种解决方法，请启动 Google Chrome，单击 "*自定义" 并控制 Google chrome*菜单，单击 "*选项*"，然后单击 "*使 google chrome 成为默认浏览器*"。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="6b7d8-389">问题： "外键" 对话框不允许输入主键</span><span class="sxs-lookup"><span data-stu-id="6b7d8-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="6b7d8-390">"**外键**" 对话框不允许您输入主键表中的主键名称。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="6b7d8-391">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-391">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-392">这是有意的。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-392">This is intentional.</span></span> <span data-ttu-id="6b7d8-393">不需要输入主键表中的主键的名称。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-393">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="6b7d8-394">问题：已禁用 "关系" 按钮</span><span class="sxs-lookup"><span data-stu-id="6b7d8-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="6b7d8-395">对于 SQL Server Compact 数据库，禁用了 "**数据库**" 工作区中 "**表**" 选项卡下的 "**关系**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="6b7d8-396">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-396">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-397">无。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-397">None.</span></span> <span data-ttu-id="6b7d8-398">SQL Server Compact 不支持表之间的关系。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-398">SQL Server Compact does not support relationships between tables.</span></span>

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="6b7d8-399">问题：参数化 SQL 查询引发异常</span><span class="sxs-lookup"><span data-stu-id="6b7d8-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="6b7d8-400">在 SQL Server Compact 4.0 中，如果未指定参数化查询中参数的数据类型（如 `SqlDbType` 或 `DbType`），则在查询运行时将引发异常。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="6b7d8-401">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="6b7d8-401">**Workaround**</span></span>  
> <span data-ttu-id="6b7d8-402">显式设置 `SqlDbType` 或 `DbType`等参数的数据类型。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="6b7d8-403">这对于 BLOB 数据类型（`image` 和 `ntext`）非常重要。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="6b7d8-404">使用如下所示的代码：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="6b7d8-405">更多信息</span><span class="sxs-lookup"><span data-stu-id="6b7d8-405">For More Information</span></span>

<span data-ttu-id="6b7d8-406">有关 WebMatrix Beta 3 的详细信息，请参阅以下网站：</span><span class="sxs-lookup"><span data-stu-id="6b7d8-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="6b7d8-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="6b7d8-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="6b7d8-408">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6b7d8-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="6b7d8-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="6b7d8-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

---

<span data-ttu-id="6b7d8-410">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="6b7d8-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="6b7d8-411">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-411">All Rights Reserved.</span></span> <span data-ttu-id="6b7d8-412">[使用条款](https://msdn.microsoft.cos/cc300389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6b7d8-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
