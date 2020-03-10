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
# <a name="webmatrix-readme"></a><span data-ttu-id="ed509-103">WebMatrix 自述文件</span><span class="sxs-lookup"><span data-stu-id="ed509-103">WebMatrix Readme</span></span>

<span data-ttu-id="ed509-104">13 2011 年1月</span><span class="sxs-lookup"><span data-stu-id="ed509-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="ed509-105">内容</span><span class="sxs-lookup"><span data-stu-id="ed509-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="ed509-106">此自述文件适用于 WebMatrix 的1.0 版本。</span><span class="sxs-lookup"><span data-stu-id="ed509-106">This readme applies to the 1.0 release of WebMatrix.</span></span>

- [<span data-ttu-id="ed509-107">概述</span><span class="sxs-lookup"><span data-stu-id="ed509-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="ed509-108">安装</span><span class="sxs-lookup"><span data-stu-id="ed509-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="ed509-109">如何发布应用程序</span><span class="sxs-lookup"><span data-stu-id="ed509-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="ed509-110">更改和问题</span><span class="sxs-lookup"><span data-stu-id="ed509-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="ed509-111">WebMatrix 1.0 安装</span><span class="sxs-lookup"><span data-stu-id="ed509-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="ed509-112">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="ed509-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="ed509-113">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="ed509-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="ed509-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="ed509-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="ed509-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="ed509-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="ed509-116">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="ed509-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="ed509-117">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="ed509-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="ed509-118">更多信息</span><span class="sxs-lookup"><span data-stu-id="ed509-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="ed509-119">概述</span><span class="sxs-lookup"><span data-stu-id="ed509-119">Overview</span></span>

> <span data-ttu-id="ed509-120">Microsoft WebMatrix 1.0 是一种免费的 web 开发堆栈，只需几分钟即可完成安装。</span><span class="sxs-lookup"><span data-stu-id="ed509-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="ed509-121">它将 web 服务器与数据库和编程框架相集成，以创建单一、集成的体验。</span><span class="sxs-lookup"><span data-stu-id="ed509-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="ed509-122">你可以使用 WebMatrix 来简化你的代码、测试和发布你自己的 ASP.NET 或 PHP 网站的方式，也可以使用 WebMatrix 来使用常用开源应用（如 DotNetNuke、Umbraco、WordPress 或 Joomla）启动新网站。</span><span class="sxs-lookup"><span data-stu-id="ed509-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="ed509-123">WebMatrix 使用在 internet 上运行你的网站的功能强大的 web 服务器、数据库引擎和框架环境，这使得从开发到生产的过渡顺畅顺畅。</span><span class="sxs-lookup"><span data-stu-id="ed509-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="ed509-124">安装</span><span class="sxs-lookup"><span data-stu-id="ed509-124">Installation</span></span>

> <span data-ttu-id="ed509-125">若要安装 WebMatrix 1.0，必须首先安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="ed509-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="ed509-126">安装 Web 平台安装程序后，可以使用它来安装 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="ed509-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="ed509-127">如果在安装过程中遇到问题，请参阅[Microsoft Web 平台安装程序的疑难解答问题](https://go.microsoft.com/fwlink/?LinkId=196212)。</span><span class="sxs-lookup"><span data-stu-id="ed509-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="ed509-128">如何发布应用程序</span><span class="sxs-lookup"><span data-stu-id="ed509-128">How to Publish Applications</span></span>

> <span data-ttu-id="ed509-129">请参阅[发布应用程序的分步说明](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="ed509-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="ed509-130">更改和问题</span><span class="sxs-lookup"><span data-stu-id="ed509-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="ed509-131">WebMatrix 1.0 安装问题</span><span class="sxs-lookup"><span data-stu-id="ed509-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="ed509-132">问题： WebMatrix 1.0 仅在支持 Microsoft .NET Framework 4 的平台上可用</span><span class="sxs-lookup"><span data-stu-id="ed509-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="ed509-133">WebMatrix 需要 .NET Framework 版本4。</span><span class="sxs-lookup"><span data-stu-id="ed509-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="ed509-134">在某些情况下，WebMatrix 1.0 安装程序将允许你尝试在不属于受支持的配置集的平台上安装。</span><span class="sxs-lookup"><span data-stu-id="ed509-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="ed509-135">具体而言，没有 SP1 更新的 Windows Vista 会使你开始安装 WebMatrix，但 .NET Framework 4 组件将失败并阻止你的安装。</span><span class="sxs-lookup"><span data-stu-id="ed509-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="ed509-136">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-136">**Workaround**</span></span>  
> <span data-ttu-id="ed509-137">在支持的平台上安装，其中包括：</span><span class="sxs-lookup"><span data-stu-id="ed509-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="ed509-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="ed509-138">Windows 7</span></span>
> - <span data-ttu-id="ed509-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="ed509-139">Windows Server 2008</span></span>
> - <span data-ttu-id="ed509-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="ed509-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="ed509-141">Windows Vista SP1 或更高版本</span><span class="sxs-lookup"><span data-stu-id="ed509-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="ed509-142">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="ed509-142">Windows XP SP3</span></span>
> - <span data-ttu-id="ed509-143">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="ed509-143">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="ed509-144">问题：如果在未 Microsoft Visual Studio 2008 SP1 的情况下安装 Microsoft Visual Studio 2008，则无法安装 WebMatrix 1。0</span><span class="sxs-lookup"><span data-stu-id="ed509-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="ed509-145">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-145">**Workaround**</span></span>  
> <span data-ttu-id="ed509-146">从 Microsoft 下载中心安装[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 。</span><span class="sxs-lookup"><span data-stu-id="ed509-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="ed509-147">问题： GAC 中未安装 SQL Server Compact 4.0 的某些程序集</span><span class="sxs-lookup"><span data-stu-id="ed509-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="ed509-148">在64位计算机上安装 SQL Server Compact 4.0，并且计算机仅安装了 .NET Framework 3.5 SP1 客户端配置文件时，SQL Server Compact 4.0 的托管程序集不会放置在全局程序集缓存（GAC）中。</span><span class="sxs-lookup"><span data-stu-id="ed509-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="ed509-149">GAC 中未安装的托管程序集包括：</span><span class="sxs-lookup"><span data-stu-id="ed509-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="ed509-150">*System.data.sqlserverce* （ADO.NET 提供程序）</span><span class="sxs-lookup"><span data-stu-id="ed509-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="ed509-151">*System.web. system.data.sqlserverce* （ADO.NET 实体框架）</span><span class="sxs-lookup"><span data-stu-id="ed509-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="ed509-152">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-152">**Workaround**</span></span>  
> <span data-ttu-id="ed509-153">卸载 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="ed509-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="ed509-154">从以下位置下载并安装 .NET Framework 3.5 SP1 的完整版本：</span><span class="sxs-lookup"><span data-stu-id="ed509-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="ed509-155">Microsoft .NET Framework 3.5 Service pack 1 （完整程序包）</span><span class="sxs-lookup"><span data-stu-id="ed509-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="ed509-156">然后重新安装 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="ed509-156">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="ed509-157">问题：无法使用命令行卸载 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="ed509-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="ed509-158">使用命令行选项卸载 SQL Server Compact 在此版本中不起作用。</span><span class="sxs-lookup"><span data-stu-id="ed509-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="ed509-159">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-159">**Workaround**</span></span>  
> <span data-ttu-id="ed509-160">使用 Windows 控制面板中的 "*程序和功能*" 卸载 Microsoft SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="ed509-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="ed509-161">ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="ed509-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="ed509-162">本部分介绍与 Razor 语法 ASP.NET 网页的1.0 版的新功能、更改和已知问题。</span><span class="sxs-lookup"><span data-stu-id="ed509-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="ed509-163">新增功能</span><span class="sxs-lookup"><span data-stu-id="ed509-163">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="ed509-164">更改</span><span class="sxs-lookup"><span data-stu-id="ed509-164">Changes</span></span>](#Changes)
- [<span data-ttu-id="ed509-165">问题</span><span class="sxs-lookup"><span data-stu-id="ed509-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a><span data-ttu-id="ed509-166">新功能</span><span class="sxs-lookup"><span data-stu-id="ed509-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="ed509-167">新增：添加了配置设置以禁用程序包管理器</span><span class="sxs-lookup"><span data-stu-id="ed509-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="ed509-168">为*web.config*文件中的 `<appSettings>` 元素提供了一个新的 `asp:AdminManagerEnabled` 项，可让你完全禁用包管理器。</span><span class="sxs-lookup"><span data-stu-id="ed509-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="ed509-169">此元素的默认值为 true，这意味着，如果它未包含在*web.config 文件中*，则启用包管理器。</span><span class="sxs-lookup"><span data-stu-id="ed509-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="ed509-170">若要禁用程序包管理器，请将以下元素添加*到网站根目录*中的 web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="ed509-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a><span data-ttu-id="ed509-171">变化</span><span class="sxs-lookup"><span data-stu-id="ed509-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="ed509-172">更改： "网页： AdminFolderVirtualPath" 密钥已重命名为 "asp： AdminFolderVirtualPath"</span><span class="sxs-lookup"><span data-stu-id="ed509-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="ed509-173">可以添加到*web.config 文件以*指定包管理器位置的 `webPages:AdminFolderVirtualPath` 项已重命名为使用 `asp:` 命名空间，而不是 `webPages` 命名空间。</span><span class="sxs-lookup"><span data-stu-id="ed509-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="ed509-174">如果使用了此元素，则必须在配置文件中对其进行重命名。</span><span class="sxs-lookup"><span data-stu-id="ed509-174">If you have used this element, you must rename it in the configuration file.</span></span>

#### <a id="Issues"></a>  <span data-ttu-id="ed509-175">已知问题</span><span class="sxs-lookup"><span data-stu-id="ed509-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="ed509-176">问题：成员身份用户的密码不再被识别</span><span class="sxs-lookup"><span data-stu-id="ed509-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="ed509-177">用于创建和存储成员身份（登录名）密码的算法已更改为更安全。</span><span class="sxs-lookup"><span data-stu-id="ed509-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="ed509-178">因此，将无法识别为在 Beta 版本的 ASP.NET 中创建的成员（用户）存储的密码。</span><span class="sxs-lookup"><span data-stu-id="ed509-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="ed509-179">**解决方法**如果该站点尚未投入生产，请从成员资格数据库中删除用户记录。</span><span class="sxs-lookup"><span data-stu-id="ed509-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="ed509-180">如果数据库是实时的，则以编程方式在成员资格数据库中重新生成现有密码。</span><span class="sxs-lookup"><span data-stu-id="ed509-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="ed509-181">问题：将自定义用户表用于成员身份时出现意外行为</span><span class="sxs-lookup"><span data-stu-id="ed509-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="ed509-182">若要初始化 ASP.NET Razor 网站的成员资格提供程序，请调用 `WebSecurity.InitializeDatabaseConnection` 方法。</span><span class="sxs-lookup"><span data-stu-id="ed509-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="ed509-183">（在 WebMatrix 中，初学者站点模板在 *\_AppStart*文件中包含对此方法的调用。）如果此方法的 `autoCreateTables` 参数设置为 true （默认情况下，它在 Starter Site 模板中设置为 true），并且如果将无法识别的表名传递给方法（第二个参数），则此方法不会引发错误。</span><span class="sxs-lookup"><span data-stu-id="ed509-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="ed509-184">相反，它会自动创建表。</span><span class="sxs-lookup"><span data-stu-id="ed509-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="ed509-185">如果要将自定义用户表用于成员身份，但将错误的表名传递到 `WebSecurity.InitializeDatabaseConnection` 方法，这可能是一个问题。</span><span class="sxs-lookup"><span data-stu-id="ed509-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="ed509-186">由于方法默认情况下不会引发错误，因此，如果您指定的表不存在，而是创建新表，则该应用程序可能看起来正在运行。</span><span class="sxs-lookup"><span data-stu-id="ed509-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="ed509-187">但是，依赖于自定义用户表的应用程序代码（以及其中的字段）最终可能会失败，并出现意外错误。</span><span class="sxs-lookup"><span data-stu-id="ed509-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="ed509-188">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-188">**Workaround**</span></span>  
> <span data-ttu-id="ed509-189">请确保 `InitializeDatabaseConnection` 方法中传递的名称与成员资格数据库中的用户配置文件表匹配，或者确保 `autoCreateTables` 参数设置为 false。</span><span class="sxs-lookup"><span data-stu-id="ed509-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a><span data-ttu-id="ed509-190">问题：错误消息 "管理模块需要访问 ~/App\_数据"</span><span class="sxs-lookup"><span data-stu-id="ed509-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="ed509-191">在某些情况下，尝试创建用户或在其他情况下使用 ASP.NET 成员资格系统会导致该页显示错误：*管理模块需要访问 ~/App\_数据*。</span><span class="sxs-lookup"><span data-stu-id="ed509-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="ed509-192">如果运行 IIS 或 IIS Express 的帐户无权在网站根目录下创建并写入*应用\_Data*文件夹，则会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="ed509-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="ed509-193">**解决方法**手动为网站创建*应用\_Data*文件夹。</span><span class="sxs-lookup"><span data-stu-id="ed509-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="ed509-194">然后，确保应用程序在其下运行的 Windows 帐户（通常为网络服务）对应用程序的根文件夹和子文件夹（例如应用程序\_数据）具有读/写权限。</span><span class="sxs-lookup"><span data-stu-id="ed509-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="ed509-195">[SQL Server Express 用户实例化和 ASP.net Web 应用程序项目](https://support.microsoft.com/kb/2002980)的知识库文章问题中提供了更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="ed509-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="ed509-196">问题： "未能生成 SQL Server 的用户实例" 错误</span><span class="sxs-lookup"><span data-stu-id="ed509-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="ed509-197">如果 WebMatrix Web 应用程序使用 SQL Server Express 并且在 Windows 7 或 Windows Server 2008 R2 上运行 IIS 7.5，你可能会看到一个错误，指示 SQL Server 无法在运行时检索用户的本地应用程序路径。</span><span class="sxs-lookup"><span data-stu-id="ed509-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="ed509-198">**解决方法**请确保应用程序在其下运行的 Windows 帐户（通常为网络服务）对应用程序的根文件夹和子文件夹（例如*应用程序\_数据*）具有读/写权限。</span><span class="sxs-lookup"><span data-stu-id="ed509-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="ed509-199">[SQL Server Express 用户实例化和 ASP.net Web 应用程序项目](https://support.microsoft.com/kb/2002980)的知识库文章问题中提供了更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="ed509-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="ed509-200">问题：包含包管理器资源或包管理器密码的文件在 IIS 6.0 和更早版本下可用</span><span class="sxs-lookup"><span data-stu-id="ed509-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="ed509-201">如果部署使用 RC2 版本生成的 ASP.NET 网页（Razor）应用程序，并且应用程序在 */App\_Data/admin*下包含*password .txt*或*packagesources*文件，则 IIS 6.0 将为该文件提供服务（如果已请求），这可能会公开包管理器实例的密码。</span><span class="sxs-lookup"><span data-stu-id="ed509-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="ed509-202">**解决方法**将*password .txt*或*packagesources*文件重命名为*password*或*packagesources*。默认情况下，IIS 6.0 不会为扩展名为 *.config*的文件提供服务。</span><span class="sxs-lookup"><span data-stu-id="ed509-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="ed509-203">（在 IIS 7 中，不提供*应用\_Data*文件夹中的任何文件，因此你不需要重命名这些文件。）</span><span class="sxs-lookup"><span data-stu-id="ed509-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="ed509-204">问题：卸载使用 Beta 3 版本安装的包并不完全删除包组件</span><span class="sxs-lookup"><span data-stu-id="ed509-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="ed509-205">如果在 Beta 3 版本中使用程序包管理器安装了包，然后尝试使用当前版本卸载包，则不会完全卸载包。</span><span class="sxs-lookup"><span data-stu-id="ed509-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="ed509-206">使用包管理器的 "**卸载**" 按钮将删除某些组件，但会保留包的库代码，而不会更新*包 .config*文件。</span><span class="sxs-lookup"><span data-stu-id="ed509-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="ed509-207">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="ed509-207">**Workaround** </span></span>  
> <span data-ttu-id="ed509-208">执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="ed509-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="ed509-209">删除 *\_Data\packages* "文件夹中的应用。</span><span class="sxs-lookup"><span data-stu-id="ed509-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="ed509-210">这将删除所有包。</span><span class="sxs-lookup"><span data-stu-id="ed509-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="ed509-211">删除网站根目录中的*包 .config*文件。</span><span class="sxs-lookup"><span data-stu-id="ed509-211">Delete the *packages.config* file in the root of the website.</span></span>

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="ed509-212">问题：在 Visual Studio 中，调用基于 web 的包管理器使应用程序脱机</span><span class="sxs-lookup"><span data-stu-id="ed509-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="ed509-213">如果使用的是 Visual Studio （而不是 WebMatrix），并使用 *\_管理*功能启动包管理器，Visual studio 会使应用程序脱机，并将*应用程序\_脱机。*</span><span class="sxs-lookup"><span data-stu-id="ed509-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="ed509-214">虽然在使用基于 web 的包管理器界面时，通常会看到此行为，但是，如果你添加、删除或修改*应用\_Data*文件夹中的任何文件，则会发生相同的行为。</span><span class="sxs-lookup"><span data-stu-id="ed509-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="ed509-215">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="ed509-215">**Workaround** </span></span>  
> <span data-ttu-id="ed509-216">若要在 Visual Studio 中处理包，请使用 NuGet 扩展，而不是基于 web 的包管理器。</span><span class="sxs-lookup"><span data-stu-id="ed509-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="ed509-217">有关信息，请参阅[NuGet 文档](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="ed509-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="ed509-218">如果使用的是*应用\_Data*文件夹中的其他文件，请考虑将文件保留在其他位置以避免此问题。</span><span class="sxs-lookup"><span data-stu-id="ed509-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="ed509-219">如果这不可行，请手动删除*应用\_脱机 .htm*文件，或等待站点自动重新联机（默认情况下，30秒后）。</span><span class="sxs-lookup"><span data-stu-id="ed509-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="ed509-220">问题： Visual Studio IntelliSense 和项目模板仅在 ASP.NET MVC 版本3中提供</span><span class="sxs-lookup"><span data-stu-id="ed509-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="ed509-221">安装 ASP.NET 网页也不会安装适用于 Visual Studio 的工具，例如用于 ASP.NET 网页应用程序的 IntelliSense 和项目模板。</span><span class="sxs-lookup"><span data-stu-id="ed509-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="ed509-222">**解决方法**若要在 Visual Studio 中使用 ASP.NET 网页应用程序的 IntelliSense 和项目模板，请通过 Web 平台安装程序或[独立安装程序](https://go.microsoft.com/fwlink/?LinkID=191797)安装 ASP.NET MVC 3 RC。</span><span class="sxs-lookup"><span data-stu-id="ed509-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="ed509-223">问题：通过代理服务器读取源或其他外部数据</span><span class="sxs-lookup"><span data-stu-id="ed509-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="ed509-224">如果运行该站点的服务器位于代理服务器后面，则你可能需要在 web.config 文件中配置代理信息，以便能够读取来自你的站点*之外的信息*。</span><span class="sxs-lookup"><span data-stu-id="ed509-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="ed509-225">例如，如果使用 `ReCaptcha` 帮助程序，则帮助者与 reCAPTCHA 服务通信，但可能会被代理服务器阻止。</span><span class="sxs-lookup"><span data-stu-id="ed509-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="ed509-226">同样，在 ASP.NET 网页中使用的源（如包管理器使用的源）可能需要代理配置。</span><span class="sxs-lookup"><span data-stu-id="ed509-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="ed509-227">如果在使用外部服务或使用包源时遇到问题，请将以下元素添加到应用程序*的根 web.config*文件中：</span><span class="sxs-lookup"><span data-stu-id="ed509-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="ed509-228">有关配置代理服务器的详细信息，请参阅 MSDN 网站上的[&lt;proxy&gt; 元素（网络设置）](https://msdn.microsoft.com/library/sa91de1e.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="ed509-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="ed509-229">问题：卸载 .NET Framework 版本4禁用包含 Razor 语法 ASP.NET 网页</span><span class="sxs-lookup"><span data-stu-id="ed509-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="ed509-230">如果卸载 .NET Framework 版本4，然后重新安装它，则将禁用 Razor 语法的 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="ed509-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="ed509-231">扩展名为 *...*</span><span class="sxs-lookup"><span data-stu-id="ed509-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="ed509-232">ASP.NET 网页在计算机根*web.config*文件中注册程序集，删除 .NET Framework 删除该文件。</span><span class="sxs-lookup"><span data-stu-id="ed509-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="ed509-233">重新安装 .NET Framework 会安装新版本的配置文件，但不会为 ASP.NET 网页程序集添加引用。</span><span class="sxs-lookup"><span data-stu-id="ed509-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="ed509-234">**解决方法**重新安装 .NET Framework 后，请用 Razor 语法重新安装 ASP.NET 网页。</span><span class="sxs-lookup"><span data-stu-id="ed509-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="ed509-235">这会将以下元素添加到计算机根目录中的*web.config 文件中，该文件*通常位于以下位置：</span><span class="sxs-lookup"><span data-stu-id="ed509-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="ed509-236">问题：无扩展名 Url 在 IIS 7 或 IIS 7.5 上找不到. cshtml/vbhtml 文件</span><span class="sxs-lookup"><span data-stu-id="ed509-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="ed509-237">在 IIS 7 或 IIS 7.5 上，使用如下所示的 URL 的请求将无法*找到扩展名为* *.*</span><span class="sxs-lookup"><span data-stu-id="ed509-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="ed509-238">出现此问题的原因是，IIS 7 或 IIS 7.5 默认情况下未启用 URL 重写。</span><span class="sxs-lookup"><span data-stu-id="ed509-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="ed509-239">Likeliest 方案是，使用 IIS Express 在本地进行测试时不会出现问题，但在将网站部署到托管网站时，你会遇到此问题。</span><span class="sxs-lookup"><span data-stu-id="ed509-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="ed509-240">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="ed509-241">如果你可以控制服务器计算机，则在服务器计算机上安装更新中所述的更新[可使某些 IIS 7.0 或 IIS 7.5 处理程序处理其 url 不以句点结尾的请求](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="ed509-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="ed509-242">如果无法控制服务器计算机（例如，部署到托管网站），请将以下内容添加*到网站的 web.config 文件中*：</span><span class="sxs-lookup"><span data-stu-id="ed509-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="ed509-243">问题：将应用程序部署到未安装 SQL Server Compact 的计算机</span><span class="sxs-lookup"><span data-stu-id="ed509-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="ed509-244">包含 SQL Server Compact 数据库的应用程序可以在未安装 SQL Server Compact 的计算机上运行。</span><span class="sxs-lookup"><span data-stu-id="ed509-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="ed509-245">Microsoft WebMatrix 1.0 自动为你复制这些二进制文件，并执行适当的*web.config*文件转换。</span><span class="sxs-lookup"><span data-stu-id="ed509-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="ed509-246">**解决方法**如果需要复制这些文件并手动更改*web.config 文件，* 请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ed509-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="ed509-247">将数据库引擎程序集复制到目标计算机上的应用程序的*Bin*文件夹中（和子文件夹）：</span><span class="sxs-lookup"><span data-stu-id="ed509-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="ed509-248">复制*C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span><span class="sxs-lookup"><span data-stu-id="ed509-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>      <span data-ttu-id="ed509-249">**到** *\bin*</span><span class="sxs-lookup"><span data-stu-id="ed509-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="ed509-250">将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* 复制**到** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="ed509-250">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **to** *\Bin\x86*</span></span>
>    - <span data-ttu-id="ed509-251">将*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \* 复制**到** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="ed509-251">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 
> 2. <span data-ttu-id="ed509-252">在网站的根文件夹中，创建或打开*web.config*文件。</span><span class="sxs-lookup"><span data-stu-id="ed509-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="ed509-253">（在 WebMatrix 1.0 中，如果您在 "**选择文件类型**" 对话框中单击 "**全部**"，则此文件类型可用。）</span><span class="sxs-lookup"><span data-stu-id="ed509-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="ed509-254">添加以下元素作为 `<configuration>` 元素的子元素（不在 `<system.web>` 元素内）：</span><span class="sxs-lookup"><span data-stu-id="ed509-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="ed509-255">问题： "Database" 和 "WebGrid" 帮助程序在 Visual Basic 的中等信任中不起作用</span><span class="sxs-lookup"><span data-stu-id="ed509-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="ed509-256">如果使用 Visual Basic （创建*vbhtml*文件），并且将应用程序设置为使用中等信任，则 `Database` 和 `WebGrid` 帮助程序将不起作用。</span><span class="sxs-lookup"><span data-stu-id="ed509-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="ed509-257">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-257">**Workaround**</span></span>  
> <span data-ttu-id="ed509-258">如果你使用 Visual Studio 2010，则可以通过安装 Service Pack 1 版本来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="ed509-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="ed509-259">在 SP1 版本的最终版本可用之前，可以从 Microsoft 下载中心的[Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en)页面下载 Sp1 的 Beta 版本。</span><span class="sxs-lookup"><span data-stu-id="ed509-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="ed509-260">如果这不可行，或者如果不使用 Visual Studio 2010，可以暂时将应用程序设置为使用完全信任。</span><span class="sxs-lookup"><span data-stu-id="ed509-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="ed509-261">问题： "ApplicationPart" 资源可从外部访问</span><span class="sxs-lookup"><span data-stu-id="ed509-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="ed509-262">如果程序集包含从 `ApplicationPart` 类派生的对象，则该程序集的资源由 `ResourceRouteHandler` 类公开。</span><span class="sxs-lookup"><span data-stu-id="ed509-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="ed509-263">以下列 URL 为例：</span><span class="sxs-lookup"><span data-stu-id="ed509-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="ed509-264">此请求下载*system.web. .dll*程序集中的所有资源字符串。</span><span class="sxs-lookup"><span data-stu-id="ed509-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="ed509-265">下载所有嵌入资源（甚至不应作为静态内容提供的资源）。</span><span class="sxs-lookup"><span data-stu-id="ed509-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="ed509-266">如果嵌入资源包含敏感信息，这可能会带来安全风险。</span><span class="sxs-lookup"><span data-stu-id="ed509-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="ed509-267">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="ed509-267">**Workaround** </span></span>  
> <span data-ttu-id="ed509-268">如果创建**ApplicationPart**对象，请确保与该**ApplicationPart**对象的程序集关联的嵌入资源不包含敏感信息。</span><span class="sxs-lookup"><span data-stu-id="ed509-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="ed509-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="ed509-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="ed509-270">有关 WebMatrix 安装问题的信息，请参阅本文档前面的[WebMatrix 安装问题](#Known_Issues_Installation)。</span><span class="sxs-lookup"><span data-stu-id="ed509-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

<span data-ttu-id="ed509-271">文档的此部分介绍 WebMatrix 开发环境的已知问题。</span><span class="sxs-lookup"><span data-stu-id="ed509-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="ed509-272">问题： web.config 文件中的数据库连接字符串的用户名或密码更改不会反映在 "数据库" 工作区中</span><span class="sxs-lookup"><span data-stu-id="ed509-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="ed509-273">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="ed509-274">*在 web.config 文件中*，更改连接字符串中的数据库名称（例如，将 "1" 添加到该字符串中）。</span><span class="sxs-lookup"><span data-stu-id="ed509-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="ed509-275">保存 web.config*文件。*</span><span class="sxs-lookup"><span data-stu-id="ed509-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="ed509-276">单击 "**数据库**和刷新"。</span><span class="sxs-lookup"><span data-stu-id="ed509-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="ed509-277">将*web.config*文件中的连接字符串中的数据库名称更改回原始数据库名称。</span><span class="sxs-lookup"><span data-stu-id="ed509-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="ed509-278">保存 web.config*文件。*</span><span class="sxs-lookup"><span data-stu-id="ed509-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="ed509-279">单击 "**数据库**和刷新"。</span><span class="sxs-lookup"><span data-stu-id="ed509-279">Click **Databases** and refresh.</span></span>

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="ed509-280">问题：无法删除 WebMatrix 创建的文件夹</span><span class="sxs-lookup"><span data-stu-id="ed509-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="ed509-281">如果 WebMatrix 正在使用提升的权限运行（也就是说，使用 Windows 中的 "以**管理员身份运行**" 选项启动 webmatrix），则无法使用 Windows 资源管理器删除 webmatrix 创建的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ed509-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="ed509-282">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-282">**Workaround**</span></span>  
> <span data-ttu-id="ed509-283">使用提升的权限运行 Windows 资源管理器。</span><span class="sxs-lookup"><span data-stu-id="ed509-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="ed509-284">请执行这些步骤：</span><span class="sxs-lookup"><span data-stu-id="ed509-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="ed509-285">在 Windows 中，单击 "**启动**"。</span><span class="sxs-lookup"><span data-stu-id="ed509-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="ed509-286">输入 "Windows 资源管理器"，然后右键单击**Windows 资源管理器**的条目。</span><span class="sxs-lookup"><span data-stu-id="ed509-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="ed509-287">单击 "以**管理员身份运行**"。</span><span class="sxs-lookup"><span data-stu-id="ed509-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="ed509-288">然后，你可以删除这些文件夹。</span><span class="sxs-lookup"><span data-stu-id="ed509-288">You can then delete the folders.</span></span>

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="ed509-289">问题： WebMatrix 1.0 无法执行需要提升的某些任务</span><span class="sxs-lookup"><span data-stu-id="ed509-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="ed509-290">WebMatrix 1.0 无法执行某些需要提升的任务，例如在下列情况下安装其他组件：</span><span class="sxs-lookup"><span data-stu-id="ed509-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="ed509-291">在 Windows Vista 或 Windows 7 上，你使用没有管理权限的帐户登录，并且用户帐户控制（UAC）处于禁用状态。</span><span class="sxs-lookup"><span data-stu-id="ed509-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="ed509-292">你使用的是 Microsoft Windows XP 或 Microsoft Windows Server 2003。</span><span class="sxs-lookup"><span data-stu-id="ed509-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="ed509-293">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-293">**Workaround**</span></span>  
> <span data-ttu-id="ed509-294">WebMatrix 1.0 中的大多数任务不需要管理权限。</span><span class="sxs-lookup"><span data-stu-id="ed509-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="ed509-295">对于这种情况，您可以以管理员身份执行操作，也可以执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="ed509-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="ed509-296">在 Windows Vista 或 Windows 7 上，启用 UAC。</span><span class="sxs-lookup"><span data-stu-id="ed509-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="ed509-297">在 Windows XP 上，将用户添加到 "管理员" 安全组。</span><span class="sxs-lookup"><span data-stu-id="ed509-297">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="ed509-298">问题： "来自 Web 库的网站" 已禁用</span><span class="sxs-lookup"><span data-stu-id="ed509-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="ed509-299">如果未安装 Web 平台安装程序3.0，则将禁用 "**从 Web 库中站点**" 选项。</span><span class="sxs-lookup"><span data-stu-id="ed509-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="ed509-300">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-300">**Workaround**</span></span>  
> <span data-ttu-id="ed509-301">安装[Microsoft Web 平台安装程序 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="ed509-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="ed509-302">问题： Google Chrome 不可用作运行选项</span><span class="sxs-lookup"><span data-stu-id="ed509-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="ed509-303">"**主页**" 选项卡上的 "**运行**" 下的浏览器列表中不显示 Google Chrome。</span><span class="sxs-lookup"><span data-stu-id="ed509-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="ed509-304">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-304">**Workaround**</span></span>  
> <span data-ttu-id="ed509-305">某些版本的 Google Chrome 不会正确地通过 Windows 中的 "默认程序" 功能进行注册。</span><span class="sxs-lookup"><span data-stu-id="ed509-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="ed509-306">作为一种解决方法，请启动 Google Chrome，单击 "*自定义" 并控制 Google chrome*菜单，单击 "*选项*"，然后单击 "*使 google chrome 成为默认浏览器*"。</span><span class="sxs-lookup"><span data-stu-id="ed509-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="ed509-307">问题： "外键" 对话框不允许输入主键</span><span class="sxs-lookup"><span data-stu-id="ed509-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="ed509-308">"**外键**" 对话框不允许您输入主键表中的主键名称。</span><span class="sxs-lookup"><span data-stu-id="ed509-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="ed509-309">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-309">**Workaround**</span></span>  
> <span data-ttu-id="ed509-310">这是有意的。</span><span class="sxs-lookup"><span data-stu-id="ed509-310">This is intentional.</span></span> <span data-ttu-id="ed509-311">不需要输入主键表中的主键的名称。</span><span class="sxs-lookup"><span data-stu-id="ed509-311">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="ed509-312">问题：智能感知不适用于 Razor 语法、 C#或 Visual Basic 的 WebMatrix</span><span class="sxs-lookup"><span data-stu-id="ed509-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="ed509-313">在 WebMatrix 中，HTML 和 CSS 支持 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="ed509-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="ed509-314">但是，它不适用于其他语言。</span><span class="sxs-lookup"><span data-stu-id="ed509-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="ed509-315">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="ed509-315">**Workaround** </span></span>  
> <span data-ttu-id="ed509-316">无。</span><span class="sxs-lookup"><span data-stu-id="ed509-316">None.</span></span>

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="ed509-317">问题： HTML 和 CSS 的 IntelliSense 建议了根据上下文不适当的元素</span><span class="sxs-lookup"><span data-stu-id="ed509-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="ed509-318">WebMatrix 中用于标记的 IntelliSense 支持使用[XHTML 1.0 过渡架构](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional)和 css （使用[css 2.1 架构](http://www.w3.org/TR/CSS2/)）的 HTML。</span><span class="sxs-lookup"><span data-stu-id="ed509-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="ed509-319">由于 IntelliSense 基于这些特定的架构，因此可能建议某些标记、属性或属性不适合当前页面或样式定义。</span><span class="sxs-lookup"><span data-stu-id="ed509-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="ed509-320">对于 HTML，它还会在可能解释为格式错误的 XHTML 的内容（例如，当标记未关闭时）导致意外的建议。</span><span class="sxs-lookup"><span data-stu-id="ed509-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="ed509-321">如果插入点在不完整的标记内，此问题可能更为明显;在这种情况下，IntelliSense 可能会建议新的开始标记或提供其他不正确的建议。</span><span class="sxs-lookup"><span data-stu-id="ed509-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="ed509-322">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="ed509-322">**Workaround** </span></span>  
> <span data-ttu-id="ed509-323">对于 HTML，请确保在格式正确的完整 XHTML 页面中工作。</span><span class="sxs-lookup"><span data-stu-id="ed509-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="ed509-324">对于 CSS，没有解决方法。</span><span class="sxs-lookup"><span data-stu-id="ed509-324">For CSS, there is no workaround.</span></span>

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="ed509-325">问题：键入时未调用 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="ed509-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="ed509-326">有时，IntelliSense 可能不会在编辑器中输入 HTML 或 CSS。</span><span class="sxs-lookup"><span data-stu-id="ed509-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="ed509-327">具体而言，当插入点直接位于另一个元素或文件的末尾时，可能会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="ed509-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="ed509-328">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="ed509-328">**Workaround** </span></span>  
> <span data-ttu-id="ed509-329">请确保插入点附近有空白，并且插入点不在文件末尾。</span><span class="sxs-lookup"><span data-stu-id="ed509-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="ed509-330">还可以通过按 Ctrl + Space 手动调用 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="ed509-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="ed509-331">问题：没有可用于禁用 IntelliSense 的 UI</span><span class="sxs-lookup"><span data-stu-id="ed509-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="ed509-332">WebMatrix 1.0 不提供用于禁用 IntelliSense 的 UI 或手势。</span><span class="sxs-lookup"><span data-stu-id="ed509-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="ed509-333">**解决方法** </span><span class="sxs-lookup"><span data-stu-id="ed509-333">**Workaround** </span></span>  
> <span data-ttu-id="ed509-334">使用以下命令启动 WebMatrix，其中包含禁用 IntelliSense 的开关：</span><span class="sxs-lookup"><span data-stu-id="ed509-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="ed509-335">IIS Express</span><span class="sxs-lookup"><span data-stu-id="ed509-335">IIS Express</span></span>

<span data-ttu-id="ed509-336">IIS Express 有自己的自述文件，该文件可在以下 URL 中找到：</span><span class="sxs-lookup"><span data-stu-id="ed509-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="ed509-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x804</span><span class="sxs-lookup"><span data-stu-id="ed509-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="ed509-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="ed509-338">SQL Server Compact</span></span>

<span data-ttu-id="ed509-339">SQL Server Compact 有自己的自述文件，该文件可在以下 URL 中找到：</span><span class="sxs-lookup"><span data-stu-id="ed509-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="ed509-340">有关涉及将 SQL Server Compact 作为 WebMatrix 的一部分进行安装的问题的信息，请参阅本文档前面的[WebMatrix 安装问题](#Known_Issues_Installation)。</span><span class="sxs-lookup"><span data-stu-id="ed509-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a><span data-ttu-id="ed509-341">安装应用程序</span><span class="sxs-lookup"><span data-stu-id="ed509-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="ed509-342">问题：如果将用户的 "我的文档" 文件夹重定向到网络共享，则安装应用程序可能需要较长时间</span><span class="sxs-lookup"><span data-stu-id="ed509-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="ed509-343">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-343">**Workaround**</span></span>  
> <span data-ttu-id="ed509-344">无。</span><span class="sxs-lookup"><span data-stu-id="ed509-344">None.</span></span> <span data-ttu-id="ed509-345">安装应用程序可能需要一些时间，但会正确安装。</span><span class="sxs-lookup"><span data-stu-id="ed509-345">The application might take a while to install, but will install correctly.</span></span>

### <a id="Known_Issues_Publishing_Applications"></a><span data-ttu-id="ed509-346">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="ed509-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="ed509-347">问题：发布 SQL Compact 数据库时出现 "无法获取所需的权限" 错误</span><span class="sxs-lookup"><span data-stu-id="ed509-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="ed509-348">WebMatrix 不完全支持将 SQL Server Compact 支持的二进制文件部署到运行 .NET Framework 版本3.5 和中等信任配置的服务器。</span><span class="sxs-lookup"><span data-stu-id="ed509-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="ed509-349">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-349">**Workaround**</span></span>  
> <span data-ttu-id="ed509-350">首选的解决方法是在服务器上安装 .NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="ed509-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="ed509-351">或者，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="ed509-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="ed509-352">将以下元素添加到*Web\_MediumTrust*文件中的 `SecurityClasses` 部分：</span><span class="sxs-lookup"><span data-stu-id="ed509-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="ed509-353">在*Web\_MediumTrust*文件中创建一个具有以下必需权限的新权限集：</span><span class="sxs-lookup"><span data-stu-id="ed509-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="ed509-354">通过在*Web\_MediumTrust*文件中放置以下元素，将权限集应用到 SQL Server Compact：</span><span class="sxs-lookup"><span data-stu-id="ed509-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="ed509-355">问题：库和 PhpBB web 应用程序在发布后显示 "服务不可用" 错误</span><span class="sxs-lookup"><span data-stu-id="ed509-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="ed509-356">在某些情况下，发布应用程序会导致 "服务不可用" 错误。</span><span class="sxs-lookup"><span data-stu-id="ed509-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="ed509-357">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-357">**Workaround**</span></span>  
> <span data-ttu-id="ed509-358">在 WebMatrix 中，在 "**发布设置**" 窗口中的服务器名称末尾添加一个反斜杠（\)，然后重新发布该应用程序。</span><span class="sxs-lookup"><span data-stu-id="ed509-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="ed509-359">问题：发布后，Moodle 网站布局和链接已损坏</span><span class="sxs-lookup"><span data-stu-id="ed509-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="ed509-360">发布 Moodle 应用程序后，应用程序无法正常工作。</span><span class="sxs-lookup"><span data-stu-id="ed509-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="ed509-361">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-361">**Workaround**</span></span>  
> <span data-ttu-id="ed509-362">在 WebMatrix 中，在 "**发布设置**" 窗口中的 "**站点名称**" 字段的末尾添加一个斜杠（/），然后再次发布该应用程序。</span><span class="sxs-lookup"><span data-stu-id="ed509-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="ed509-363">问题：发布 nopCommerce 失败，出现数据库错误</span><span class="sxs-lookup"><span data-stu-id="ed509-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="ed509-364">发布 nopCommerce 失败，并报告数据库错误，如 "插入到 nop\_日志表失败"。</span><span class="sxs-lookup"><span data-stu-id="ed509-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="ed509-365">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="ed509-366">在 WebMatrix 中，单击 "**运行**" 以在本地启动 nopCommerce。</span><span class="sxs-lookup"><span data-stu-id="ed509-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="ed509-367">登录到管理页。</span><span class="sxs-lookup"><span data-stu-id="ed509-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="ed509-368">单击 "**系统**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="ed509-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="ed509-369">单击**日志**选项。</span><span class="sxs-lookup"><span data-stu-id="ed509-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="ed509-370">单击 **“清除日志”** 按钮。</span><span class="sxs-lookup"><span data-stu-id="ed509-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="ed509-371">再次发布 nopCommerce。</span><span class="sxs-lookup"><span data-stu-id="ed509-371">Publish nopCommerce again.</span></span>

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="ed509-372">问题：当你下载已发布的站点时，Silverstripe CMS 显示 "HTTP 500 PHP HANDLER.FCGI 错误"</span><span class="sxs-lookup"><span data-stu-id="ed509-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="ed509-373">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-373">**Workaround**</span></span>  
> <span data-ttu-id="ed509-374">单击 "**下载已发布网站**" 后，在**发布预览**中跳过 `silverstripe-cache/manifest_main`。</span><span class="sxs-lookup"><span data-stu-id="ed509-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="ed509-375">此文件用于缓存目的，并特定于每台计算机。</span><span class="sxs-lookup"><span data-stu-id="ed509-375">This file is used for caching purposes and is specific to each computer.</span></span>

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="ed509-376">问题：当你下载已发布的站点时，从属显示 "/" 应用程序中的服务器错误 "</span><span class="sxs-lookup"><span data-stu-id="ed509-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="ed509-377">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-377">**Workaround**</span></span>  
> <span data-ttu-id="ed509-378">打开站点的 web.config*文件，* 并将数据库连接字符串中的用户 ID 和密码替换 SQL Server 管理员凭据（"sa" 凭据）。</span><span class="sxs-lookup"><span data-stu-id="ed509-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="ed509-379">或者，按照以下步骤，为你登录的用户帐户提供 `db_owner` 权限：</span><span class="sxs-lookup"><span data-stu-id="ed509-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="ed509-380">使用 Web 平台安装程序安装 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="ed509-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="ed509-381">连接到本地 SQL Server Express 实例（默认情况下，`.\SQLEXPRESS`）。</span><span class="sxs-lookup"><span data-stu-id="ed509-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="ed509-382">单击 "**数据库**" &gt; *[LocalSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] （默认值为 `subtextuser`]，右键单击，然后单击 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="ed509-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="ed509-383">在角色成员资格部分中选择 " **db\_所有者**"。</span><span class="sxs-lookup"><span data-stu-id="ed509-383">Select **db\_owner** in the role membership section.</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="ed509-384">问题：如果 "目标 URL" 字段未使用 http://或 https://作为前缀，则站点可能无法正常工作</span><span class="sxs-lookup"><span data-stu-id="ed509-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="ed509-385">在 "**发布设置**" 对话框中，如果目标 URL 不以 `http://` 或 `https://`开头，则该站点在部署后可能不起作用。</span><span class="sxs-lookup"><span data-stu-id="ed509-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="ed509-386">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-386">**Workaround**</span></span>  
> <span data-ttu-id="ed509-387">请确保在发布站点之前，"**发布设置**" 对话框中的 "目标 URL" 以 `http://` 或 `https://`开头。</span><span class="sxs-lookup"><span data-stu-id="ed509-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="ed509-388">问题：发布 MySQL 数据库失败，出现错误 "无法发布数据库。</span><span class="sxs-lookup"><span data-stu-id="ed509-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="ed509-389">如果远程数据库无法运行该脚本，就会发生这种情况。</span><span class="sxs-lookup"><span data-stu-id="ed509-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="ed509-390">发生此错误的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="ed509-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="ed509-391">出现此错误的原因之一是，数据库脚本包含单引号字符（'），目标 MySQL 数据库的默认字符集不是 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="ed509-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="ed509-392">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-392">**Workaround**</span></span>  
> <span data-ttu-id="ed509-393">将远程 MySQL 数据库的默认字符集设置为 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="ed509-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="ed509-394">问题：发布或下载站点后，某些链接在 DotNetNuke 中不可见</span><span class="sxs-lookup"><span data-stu-id="ed509-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="ed509-395">如果发布或下载 DotNetNuke 站点，则可能需要清除缓存以使新链接显示在站点上。</span><span class="sxs-lookup"><span data-stu-id="ed509-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="ed509-396">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="ed509-397">以 "主机" 身份登录。</span><span class="sxs-lookup"><span data-stu-id="ed509-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="ed509-398">中转到 "主机" 菜单并选择 "**主机设置**"。</span><span class="sxs-lookup"><span data-stu-id="ed509-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="ed509-399">向下滚动，在 "**高级设置**" 下，展开 "**性能设置**"。</span><span class="sxs-lookup"><span data-stu-id="ed509-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="ed509-400">单击 "**清除缓存**" 链接以获取页面。</span><span class="sxs-lookup"><span data-stu-id="ed509-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="ed509-401">请切换到页面底部，然后重新启动应用程序。</span><span class="sxs-lookup"><span data-stu-id="ed509-401">Go to the bottom of the page and restart the application.</span></span>

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="ed509-402">问题：下载已发布站点后，AtomSite 中的某些链接已中断</span><span class="sxs-lookup"><span data-stu-id="ed509-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="ed509-403">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-403">**Workaround**</span></span>  
> <span data-ttu-id="ed509-404">在*service .config*文件、*用户 .config*文件和所有 *.XML*文件中，将 URL 字符串（例如 `http://myhost.com/atomsite`）替换为本地（例如，`http://localhost:1239`）。</span><span class="sxs-lookup"><span data-stu-id="ed509-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="ed509-405">问题：基于 MySQL 的应用程序（如 WordPress）无法发布和报告数据库错误</span><span class="sxs-lookup"><span data-stu-id="ed509-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="ed509-406">默认情况下，WebMatrix 使用 UTF-8 字符集安装 MySQL。</span><span class="sxs-lookup"><span data-stu-id="ed509-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="ed509-407">如果自己安装 MySQL，而字符集不是 UTF-8 （例如，它是 Latin1-general），则数据库的发布过程可能会失败。</span><span class="sxs-lookup"><span data-stu-id="ed509-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="ed509-408">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="ed509-409">将 MySQL 字符集设置为 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="ed509-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="ed509-410">（有关详细信息，请参阅 MySQL 网站上的[服务器字符集和排序规则](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html)。）</span><span class="sxs-lookup"><span data-stu-id="ed509-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="ed509-411">重新安装应用程序。</span><span class="sxs-lookup"><span data-stu-id="ed509-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="ed509-412">重新发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="ed509-412">Republish the application.</span></span>

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="ed509-413">问题：对于具有基于浏览器的安装程序的应用程序，"下载已发布的站点" 失败</span><span class="sxs-lookup"><span data-stu-id="ed509-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="ed509-414">某些应用程序（例如，Kentico CMS）要求您在浏览器中启动这些应用程序，以便执行安装后的安装程序（如创建数据库）。</span><span class="sxs-lookup"><span data-stu-id="ed509-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="ed509-415">如果在不完成基于浏览器的安装的情况下发布了此类应用程序，则尝试从远程服务器下载相同的站点将会失败。</span><span class="sxs-lookup"><span data-stu-id="ed509-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="ed509-416">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-416">**Workaround**</span></span>  
> <span data-ttu-id="ed509-417">在发布站点之前，请完成基于浏览器的设置。</span><span class="sxs-lookup"><span data-stu-id="ed509-417">Finish browser-based setup before publishing the site.</span></span>

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="ed509-418">问题： "下载已发布站点" 失败，并出现针对 DotNetNuke 和 Kooboo CMS 的数据库错误</span><span class="sxs-lookup"><span data-stu-id="ed509-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="ed509-419">如果尝试从服务器下载应用程序，并且在 "**发布设置**" 对话框中的数据库连接字符串中具有管理员凭据，则在发布日志中可能会看到以下错误：</span><span class="sxs-lookup"><span data-stu-id="ed509-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="ed509-420">**解决方法**</span><span class="sxs-lookup"><span data-stu-id="ed509-420">**Workaround**</span></span>  
> <span data-ttu-id="ed509-421">如果可行，请使用数据库的非管理员凭据重新发布站点（或已发布）。</span><span class="sxs-lookup"><span data-stu-id="ed509-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="ed509-422">更多信息</span><span class="sxs-lookup"><span data-stu-id="ed509-422">For More Information</span></span>

<span data-ttu-id="ed509-423">有关 WebMatrix 1.0 的详细信息，请参阅以下网站：</span><span class="sxs-lookup"><span data-stu-id="ed509-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="ed509-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="ed509-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="ed509-425">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ed509-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="ed509-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="ed509-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="ed509-427">© 2011 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="ed509-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="ed509-428">保留所有权利。</span><span class="sxs-lookup"><span data-stu-id="ed509-428">All Rights Reserved.</span></span> <span data-ttu-id="ed509-429">[使用条款](https://msdn.microsoft.cos/cc300389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ed509-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
