---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: 分析和调试 ASP.NET MVC 应用程序入门 |Microsoft Docs
author: Rick-Anderson
description: 概述是蓬勃发展的开源 NuGet 包系列，其中提供了有关 ASP.NET 的详细性能、调试和诊断信息 。
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457656"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="f1e7f-103">使用 Glimpse 分析和调试 ASP.NET MVC 应用</span><span class="sxs-lookup"><span data-stu-id="f1e7f-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>

<span data-ttu-id="f1e7f-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f1e7f-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="f1e7f-105">概述是一系列蓬勃发展和不断增长的开源 NuGet 包系列，可为 ASP.NET 应用提供详细的性能、调试和诊断信息。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="f1e7f-106">在每一页的底部，都可以轻松安装、轻量、极其快速地显示关键性能指标。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="f1e7f-107">当需要找出服务器上的内容时，可以通过它向下钻取到你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="f1e7f-108">概述提供了如此重要的信息，我们建议你在整个开发周期（包括你的 Azure 测试环境）中使用它。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="f1e7f-109">尽管[Fiddler](http://www.telerik.com/fiddler)和[F-12 开发工具](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx)提供客户端视图，但概述提供了一个来自服务器的详细视图。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="f1e7f-110">本教程将重点介绍如何使用 "大致了解" ASP.NET MVC 和 EF 包，但还有许多其他包可用。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="f1e7f-111">在可能的情况下，我将链接到我要维护的适当的 "[粗略文档](http://getglimpse.com/Docs/)"。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="f1e7f-112">"概述" 是开源项目，也可以参与源代码和文档。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>

- [<span data-ttu-id="f1e7f-113">安装初步了解</span><span class="sxs-lookup"><span data-stu-id="f1e7f-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="f1e7f-114">启用对 localhost 的了解</span><span class="sxs-lookup"><span data-stu-id="f1e7f-114">Enable Glimpse for localhost</span></span>](#eg)
- [<span data-ttu-id="f1e7f-115">"时间线" 选项卡</span><span class="sxs-lookup"><span data-stu-id="f1e7f-115">The Timeline tab</span></span>](#Time)
- [<span data-ttu-id="f1e7f-116">模型绑定</span><span class="sxs-lookup"><span data-stu-id="f1e7f-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="f1e7f-117">路由</span><span class="sxs-lookup"><span data-stu-id="f1e7f-117">Routes</span></span>](#route)
- [<span data-ttu-id="f1e7f-118">使用初步了解 Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="f1e7f-119">其他资源</span><span class="sxs-lookup"><span data-stu-id="f1e7f-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="f1e7f-120">安装初步了解</span><span class="sxs-lookup"><span data-stu-id="f1e7f-120">Installing Glimpse</span></span>

<span data-ttu-id="f1e7f-121">你可以从 NuGet 包管理器控制台或 "**管理 NuGet 包**" 控制台安装。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="f1e7f-122">对于此演示，我将安装 Mvc5 和 EF6 包：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![从 NuGet Dlg 安装](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="f1e7f-124">搜索大致适用于*EF*</span><span class="sxs-lookup"><span data-stu-id="f1e7f-124">Search for *Glimpse.EF*</span></span>

![从 NuGet 安装 dlg 了解 EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="f1e7f-126">通过选择 "**已安装的包**"，可以看到已安装的 "粗略依赖" 模块：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![从 DLg 安装的 "了解包"](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="f1e7f-128">以下命令从包管理器控制台安装 MVC5 和 EF6 模块：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="f1e7f-129">启用对 localhost 的了解</span><span class="sxs-lookup"><span data-stu-id="f1e7f-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="f1e7f-130">导航到 http://localhost:&lt;p o #&gt;/glimpse.axd 并单击 "<strong>打开</strong>" "了解" 按钮。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![大致为 axd 页](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="f1e7f-132">如果显示了 "收藏夹" 栏，可以拖放 "了解" 按钮，然后将其添加为 bookmarklets：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![IE with bookmarklets](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="f1e7f-134">你现在可以在应用中导航，并在页面底部显示 "**打印头显示**" （HUD）。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![具有 HUD 的 "联系人管理器" 页](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="f1e7f-136">"[大致 HUD" 页](http://getglimpse.com/Docs/Heads-up-Display)详细介绍了上面所示的计时信息。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="f1e7f-137">HUD 显示的非引人注目性能数据会立即通知你问题，然后再进入测试周期。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="f1e7f-138">单击右下角的 &quot;g&quot; 会打开 "了解" 面板：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![了解面板](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="f1e7f-140">在上面的图像中，选择 "[执行" 选项卡，该选项卡](http://getglimpse.com/Docs/Execution-Tab)显示管道中操作和筛选器的计时详细信息。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="f1e7f-141">你可以看到我的[停止监视筛选器计时器](http://www.nuget.org/packages/StopWatch/)在管道的第6阶段开始。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="f1e7f-142">虽然我的轻型计时器可以提供有用的配置文件/计时数据，但它会丢失授权和呈现视图所花费的时间。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="f1e7f-143">你可以在配置文件中阅读我[的计时器，并将 ASP.NET MVC 应用程序一直到 Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="f1e7f-144">"[选项卡](http://getglimpse.com/Docs/Tabs)" 页提供了有关每个选项卡的详细信息的链接。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="f1e7f-145">"时间线" 选项卡</span><span class="sxs-lookup"><span data-stu-id="f1e7f-145">The Timeline tab</span></span>

<span data-ttu-id="f1e7f-146">我已经修改了 Tom Dykstra 的未完成[EF 6/MVC 5 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)，并将以下代码更改为讲师控制器：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="f1e7f-147">上述代码允许我传入查询字符串（`eager`）来控制数据的预先加载或显式加载。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="f1e7f-148">在下图中，使用了显式加载，"计时" 页显示了在 `Index` 操作方法中加载的每个注册：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![显式加载 (Explicit Loading)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="f1e7f-150">在下面的代码中，指定了渴望，并在调用 `Index` 视图后提取每个注册：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![指定了热情](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="f1e7f-152">您可以将鼠标悬停在某个时间段上，以获取详细的计时信息：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-152">You can hover over a time segment to get detailed timing information:</span></span>

![悬停以查看详细计时](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="f1e7f-154">模型绑定</span><span class="sxs-lookup"><span data-stu-id="f1e7f-154">Model Binding</span></span>

<span data-ttu-id="f1e7f-155">"[模型绑定" 选项卡](http://getglimpse.com/Docs/Model-Binding-Tab)提供丰富的信息，可帮助您了解窗体变量的绑定方式以及某些内容为何不按预期方式绑定。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="f1e7f-156">下图显示了 **？**</span><span class="sxs-lookup"><span data-stu-id="f1e7f-156">The image below shows the **?**</span></span> <span data-ttu-id="f1e7f-157">图标，单击该图标可显示该功能的 "了解帮助" 页。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![了解模型绑定视图](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="f1e7f-159">路由</span><span class="sxs-lookup"><span data-stu-id="f1e7f-159">Routes</span></span>

 <span data-ttu-id="f1e7f-160">"粗略路由" 选项卡可帮助你调试和了解路由。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="f1e7f-161">在下图中，选择了产品路线（以绿色、粗略约定显示）。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="f1e7f-162">同时还会显示 ![选定](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 路由约束、区域和数据标记的产品名称。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="f1e7f-163">有关详细信息，请参阅[ASP.NET MVC 5 中的 "](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx)了解[路由](http://getglimpse.com/Docs/Routes-Tab)和属性路由"。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="f1e7f-164">使用初步了解 Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="f1e7f-165">"粗略默认" 安全策略仅允许从本地主机显示数据。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="f1e7f-166">你可以更改此安全策略，以便在远程服务器（如 Azure 上的 web 应用）上查看此数据。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="f1e7f-167">对于 Azure 上的测试环境，请将突出显示的标记添加到 web.config*文件的*底部，以启用概述：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.config* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="f1e7f-168">如果只使用此更改，任何用户都可以看到你在远程站点上的数据。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="f1e7f-169">请考虑将上面的标记添加到发布配置文件，以便在使用该发布配置文件时（例如，Azure 测试配置文件）仅部署了。为了限制对数据的了解，我们将添加 `canViewGlimpseData` 角色并仅允许此角色中的用户查看数据。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-169">Consider adding the markup above to a publish profile so it's only deployed an applied when you use that publish profile (for example, your Azure test profile.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="f1e7f-170">从*GlimpseSecurityPolicy.cs*文件中删除注释，并将[IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx)调用从 `Administrator` 更改为 `canViewGlimpseData` 角色：</span><span class="sxs-lookup"><span data-stu-id="f1e7f-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="f1e7f-171">安全性-通过 "概述" 提供的丰富数据可以公开应用程序的安全性。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="f1e7f-172">Microsoft 尚未执行概述以在生产应用上使用的安全审核。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>

<span data-ttu-id="f1e7f-173">有关添加角色的信息，请参阅[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 5 web 应用部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)教程。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="f1e7f-174">其他资源</span><span class="sxs-lookup"><span data-stu-id="f1e7f-174">Additional Resources</span></span>

- [<span data-ttu-id="f1e7f-175">使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 5 应用程序部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="f1e7f-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="f1e7f-176">"了解[配置](http://getglimpse.com/Docs/Configuration)-文档" 页上的配置选项卡、运行时策略、日志记录等。</span><span class="sxs-lookup"><span data-stu-id="f1e7f-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
