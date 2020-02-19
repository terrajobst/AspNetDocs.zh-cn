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
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a>使用 Glimpse 分析和调试 ASP.NET MVC 应用

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 概述是一系列蓬勃发展和不断增长的开源 NuGet 包系列，可为 ASP.NET 应用提供详细的性能、调试和诊断信息。 在每一页的底部，都可以轻松安装、轻量、极其快速地显示关键性能指标。 当需要找出服务器上的内容时，可以通过它向下钻取到你的应用程序。 概述提供了如此重要的信息，我们建议你在整个开发周期（包括你的 Azure 测试环境）中使用它。 尽管[Fiddler](http://www.telerik.com/fiddler)和[F-12 开发工具](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx)提供客户端视图，但概述提供了一个来自服务器的详细视图。 本教程将重点介绍如何使用 "大致了解" ASP.NET MVC 和 EF 包，但还有许多其他包可用。 在可能的情况下，我将链接到我要维护的适当的 "[粗略文档](http://getglimpse.com/Docs/)"。 "概述" 是开源项目，也可以参与源代码和文档。

- [安装初步了解](#ig)
- [启用对 localhost 的了解](#eg)
- ["时间线" 选项卡](#Time)
- [模型绑定](#mb)
- [路由](#route)
- [使用初步了解 Azure](#da)
- [其他资源](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a>安装初步了解

你可以从 NuGet 包管理器控制台或 "**管理 NuGet 包**" 控制台安装。 对于此演示，我将安装 Mvc5 和 EF6 包：

![从 NuGet Dlg 安装](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

搜索大致适用于*EF*

![从 NuGet 安装 dlg 了解 EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

通过选择 "**已安装的包**"，可以看到已安装的 "粗略依赖" 模块：

![从 DLg 安装的 "了解包"](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

以下命令从包管理器控制台安装 MVC5 和 EF6 模块：

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a>启用对 localhost 的了解

导航到 http://localhost:&lt;p o #&gt;/glimpse.axd 并单击 "<strong>打开</strong>" "了解" 按钮。

![大致为 axd 页](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

如果显示了 "收藏夹" 栏，可以拖放 "了解" 按钮，然后将其添加为 bookmarklets：

![IE with bookmarklets](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

你现在可以在应用中导航，并在页面底部显示 "**打印头显示**" （HUD）。

![具有 HUD 的 "联系人管理器" 页](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

"[大致 HUD" 页](http://getglimpse.com/Docs/Heads-up-Display)详细介绍了上面所示的计时信息。 HUD 显示的非引人注目性能数据会立即通知你问题，然后再进入测试周期。 单击右下角的 &quot;g&quot; 会打开 "了解" 面板：

![了解面板](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

在上面的图像中，选择 "[执行" 选项卡，该选项卡](http://getglimpse.com/Docs/Execution-Tab)显示管道中操作和筛选器的计时详细信息。 你可以看到我的[停止监视筛选器计时器](http://www.nuget.org/packages/StopWatch/)在管道的第6阶段开始。 虽然我的轻型计时器可以提供有用的配置文件/计时数据，但它会丢失授权和呈现视图所花费的时间。 你可以在配置文件中阅读我[的计时器，并将 ASP.NET MVC 应用程序一直到 Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)。 "[选项卡](http://getglimpse.com/Docs/Tabs)" 页提供了有关每个选项卡的详细信息的链接。

<a id="Time"></a>
## <a name="the-timeline-tab"></a>"时间线" 选项卡

我已经修改了 Tom Dykstra 的未完成[EF 6/MVC 5 教程](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)，并将以下代码更改为讲师控制器：

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

上述代码允许我传入查询字符串（`eager`）来控制数据的预先加载或显式加载。 在下图中，使用了显式加载，"计时" 页显示了在 `Index` 操作方法中加载的每个注册：

![显式加载 (Explicit Loading)](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

在下面的代码中，指定了渴望，并在调用 `Index` 视图后提取每个注册：

![指定了热情](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

您可以将鼠标悬停在某个时间段上，以获取详细的计时信息：

![悬停以查看详细计时](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a>模型绑定

"[模型绑定" 选项卡](http://getglimpse.com/Docs/Model-Binding-Tab)提供丰富的信息，可帮助您了解窗体变量的绑定方式以及某些内容为何不按预期方式绑定。 下图显示了 **？** 图标，单击该图标可显示该功能的 "了解帮助" 页。

![了解模型绑定视图](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a>路由

 "粗略路由" 选项卡可帮助你调试和了解路由。 在下图中，选择了产品路线（以绿色、粗略约定显示）。 同时还会显示 ![选定](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 路由约束、区域和数据标记的产品名称。 有关详细信息，请参阅[ASP.NET MVC 5 中的 "](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx)了解[路由](http://getglimpse.com/Docs/Routes-Tab)和属性路由"。 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a>使用初步了解 Azure

"粗略默认" 安全策略仅允许从本地主机显示数据。 你可以更改此安全策略，以便在远程服务器（如 Azure 上的 web 应用）上查看此数据。 对于 Azure 上的测试环境，请将突出显示的标记添加到 web.config*文件的*底部，以启用概述：

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

如果只使用此更改，任何用户都可以看到你在远程站点上的数据。 请考虑将上面的标记添加到发布配置文件，以便在使用该发布配置文件时（例如，Azure 测试配置文件）仅部署了。为了限制对数据的了解，我们将添加 `canViewGlimpseData` 角色并仅允许此角色中的用户查看数据。

从*GlimpseSecurityPolicy.cs*文件中删除注释，并将[IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx)调用从 `Administrator` 更改为 `canViewGlimpseData` 角色：

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> 安全性-通过 "概述" 提供的丰富数据可以公开应用程序的安全性。 Microsoft 尚未执行概述以在生产应用上使用的安全审核。

有关添加角色的信息，请参阅[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 5 web 应用部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)教程。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

- [使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET MVC 5 应用程序部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- "了解[配置](http://getglimpse.com/Docs/Configuration)-文档" 页上的配置选项卡、运行时策略、日志记录等。
