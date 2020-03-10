---
uid: visual-studio/overview/2013/using-browser-link
title: 在 Visual Studio 2013 中使用浏览器链接Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505202"
---
# <a name="using-browser-link-in-visual-studio-2013"></a><span data-ttu-id="7c0ef-102">在 Visual Studio 2013 中使用浏览器链接</span><span class="sxs-lookup"><span data-stu-id="7c0ef-102">Using Browser Link in Visual Studio 2013</span></span>

<span data-ttu-id="7c0ef-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7c0ef-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7c0ef-104">Browser 链接是 Visual Studio 2013 中的一项新功能，它在开发环境和一个或多个 web 浏览器之间创建信道。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-104">Browser Link is a new feature in Visual Studio 2013 that creates a communication channel between the development environment and one or more web browsers.</span></span> <span data-ttu-id="7c0ef-105">您可以使用浏览器链接一次刷新多个浏览器中的 web 应用程序，这对于跨浏览器测试非常有用。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-105">You can use Browser Link to refresh your web application in several browsers at once, which is useful for cross-browser testing.</span></span>

- [<span data-ttu-id="7c0ef-106">浏览器刷新</span><span class="sxs-lookup"><span data-stu-id="7c0ef-106">Browser Refresh</span></span>](#browser-refresh)
- [<span data-ttu-id="7c0ef-107">查看浏览器链接仪表板</span><span class="sxs-lookup"><span data-stu-id="7c0ef-107">Viewing the Browser Link Dashboard</span></span>](#dashboard)
- [<span data-ttu-id="7c0ef-108">为静态 HTML 文件启用浏览器链接</span><span class="sxs-lookup"><span data-stu-id="7c0ef-108">Enabling Browser Link for Static HTML Files</span></span>](#static-html)
- [<span data-ttu-id="7c0ef-109">禁用浏览器链接</span><span class="sxs-lookup"><span data-stu-id="7c0ef-109">Disabling Browser Link</span></span>](#disabling)
- [<span data-ttu-id="7c0ef-110">它的工作原理是什么？</span><span class="sxs-lookup"><span data-stu-id="7c0ef-110">How Does It Work?</span></span>](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a><span data-ttu-id="7c0ef-111">浏览器刷新</span><span class="sxs-lookup"><span data-stu-id="7c0ef-111">Browser Refresh</span></span>

<span data-ttu-id="7c0ef-112">使用浏览器刷新，可以刷新通过浏览器链接连接到 Visual Studio 的多个浏览器。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-112">With Browser Refresh, you can refresh multiple browsers that are connected to Visual Studio through Browser Link.</span></span>

<span data-ttu-id="7c0ef-113">若要使用浏览器刷新，请首先使用任意项目模板创建 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-113">To use Browser Refresh, first create an ASP.NET application, using any of the project templates.</span></span> <span data-ttu-id="7c0ef-114">按 F5 或单击工具栏中的箭头图标来调试应用程序：</span><span class="sxs-lookup"><span data-stu-id="7c0ef-114">Debug the application by pressing F5 or clicking the arrow icon in the toolbar:</span></span>

![](using-browser-link/_static/image1.png)

<span data-ttu-id="7c0ef-115">你还可以使用下拉列表选择特定的浏览器进行调试。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-115">You can also use the dropdown to select a specific browser for debugging.</span></span>

![](using-browser-link/_static/image2.png)

<span data-ttu-id="7c0ef-116">若要通过多个浏览器进行调试，请选择 "**浏览方式**"。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-116">To debug with multiple browsers, select **Browse With**.</span></span> <span data-ttu-id="7c0ef-117">在 "**浏览**" 对话框中，按住 CTRL 键以选择多个浏览器。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-117">In the **Browse With** dialog, hold down the CTRL key to select more than one browser.</span></span> <span data-ttu-id="7c0ef-118">单击 "**浏览**" 以通过所选浏览器进行调试。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-118">Click **Browse** to debug with the selected browsers.</span></span> <span data-ttu-id="7c0ef-119">如果从 Visual Studio 外部启动浏览器并导航到应用程序 URL，则浏览器链接也起作用。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-119">Browser Link also works if you launch a browser from outside Visual Studio and navigate to the application URL.</span></span>

![](using-browser-link/_static/image3.png)

<span data-ttu-id="7c0ef-120">浏览器链接控件位于包含环形箭头图标的下拉列表中。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-120">The Browser Link controls are located in the dropdown with the circular arrow icon.</span></span> <span data-ttu-id="7c0ef-121">箭头图标为 "**刷新**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-121">The arrow icon is the **Refresh** button.</span></span>

![](using-browser-link/_static/image4.png)

<span data-ttu-id="7c0ef-122">若要查看连接了哪些浏览器，请在调试时将鼠标悬停在 "**刷新**" 按钮上。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-122">To see which browsers are connected, hover the mouse over the **Refresh** button while debugging.</span></span> <span data-ttu-id="7c0ef-123">已连接的浏览器将显示在工具提示窗口中。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-123">The connected browsers are shown in a ToolTip window.</span></span>

![](using-browser-link/_static/image5.png)

<span data-ttu-id="7c0ef-124">若要刷新连接的浏览器，请单击 "**刷新**" 按钮或按 CTRL + ALT + enter。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-124">To refresh the connected browsers, click the **Refresh** button or press CTRL+ALT+ENTER.</span></span> <span data-ttu-id="7c0ef-125">例如，以下屏幕截图显示了我使用 MVC 5 项目模板创建的 ASP.NET 项目。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-125">For example, the following screenshot shows an ASP.NET project, which I created using the MVC 5 project template.</span></span> <span data-ttu-id="7c0ef-126">可以在顶部看到两个浏览器中运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-126">You can see the application running in two browsers at the top.</span></span> <span data-ttu-id="7c0ef-127">在底部，项目在 Visual Studio 中打开。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-127">At the bottom, the project is open in Visual Studio.</span></span>

![](using-browser-link/_static/image6.png)

<span data-ttu-id="7c0ef-128">在 Visual Studio 中，我更改了主页的 &lt;h1&gt; 标题：</span><span class="sxs-lookup"><span data-stu-id="7c0ef-128">In Visual Studio, I changed the &lt;h1&gt; heading for the home page:</span></span>

![](using-browser-link/_static/image7.png)

<span data-ttu-id="7c0ef-129">单击 "**刷新**" 按钮时，更改会出现在浏览器窗口中：</span><span class="sxs-lookup"><span data-stu-id="7c0ef-129">When I clicked the **Refresh** button, the change appeared in both browser windows:</span></span>

![](using-browser-link/_static/image8.png)

<span data-ttu-id="7c0ef-130">**注意**</span><span class="sxs-lookup"><span data-stu-id="7c0ef-130">**Notes**</span></span>

- <span data-ttu-id="7c0ef-131">若要启用浏览器链接，请在项目的 Web.config 文件中的[&lt;编译&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx)元素中设置 `debug=true`。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-131">To enable Browser Link, set `debug=true` in the [&lt;compilation&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx) element in the project's Web.config file.</span></span>
- <span data-ttu-id="7c0ef-132">应用程序必须在 localhost 上运行。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-132">The application must be running on localhost.</span></span>
- <span data-ttu-id="7c0ef-133">应用程序必须面向 .NET 4.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-133">The application must target .NET 4.0 or later.</span></span>

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a><span data-ttu-id="7c0ef-134">查看浏览器链接仪表板</span><span class="sxs-lookup"><span data-stu-id="7c0ef-134">Viewing the Browser Link Dashboard</span></span>

<span data-ttu-id="7c0ef-135">浏览器链接仪表板显示有关浏览器链接连接的信息。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-135">The Browser Link dashboard shows information about the Browser Link connections.</span></span> <span data-ttu-id="7c0ef-136">若要查看仪表板，请选择 "浏览器链接" 下拉菜单（"**刷新**" 按钮旁边的小箭头）。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-136">To view the dashboard, select the Browser Link dropdown menu (the small arrow next to the **Refresh** button).</span></span> <span data-ttu-id="7c0ef-137">然后单击 "**浏览器链接仪表板**"。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-137">Then click **Browser Link Dashboard**.</span></span>

![](using-browser-link/_static/image9.png)

<span data-ttu-id="7c0ef-138">面板列出了连接的浏览器以及每个浏览器导航到的 URL。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-138">The dashboard lists the connected Browsers and the URL to which each browser has navigated.</span></span>

![](using-browser-link/_static/image10.png)

<span data-ttu-id="7c0ef-139">"**先决条件**" 部分显示为该项目启用浏览器链接所需的任何步骤。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-139">The **Prerequisites** section shows any steps needed to enable Browser Link for that project.</span></span> <span data-ttu-id="7c0ef-140">例如，以下屏幕截图显示了 Web.config 文件中的 "debug" 设置为 false 的项目。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-140">For example, the following screenshot shows a project where "debug" is set to false in the Web.config file.</span></span>

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a><span data-ttu-id="7c0ef-141">为静态 HTML 文件启用浏览器链接</span><span class="sxs-lookup"><span data-stu-id="7c0ef-141">Enabling Browser Link for Static HTML Files</span></span>

<span data-ttu-id="7c0ef-142">若要为静态 HTML 文件启用浏览器链接，请将以下项添加到 web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-142">To enable Browser Link for static HTML files, add the following to your Web.config file.</span></span>

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

<span data-ttu-id="7c0ef-143">出于性能方面的考虑，请在发布项目时删除此设置。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-143">For performance reasons, remove this setting when you publish your project.</span></span>

<a id="disabling"></a>
## <a name="disabling-browser-link"></a><span data-ttu-id="7c0ef-144">禁用浏览器链接</span><span class="sxs-lookup"><span data-stu-id="7c0ef-144">Disabling Browser Link</span></span>

<span data-ttu-id="7c0ef-145">默认情况下启用浏览器链接。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-145">Browser Link is enabled by default.</span></span> <span data-ttu-id="7c0ef-146">可以通过多种方式来禁用它：</span><span class="sxs-lookup"><span data-stu-id="7c0ef-146">There are several ways to disable it:</span></span>

- <span data-ttu-id="7c0ef-147">在 "浏览器链接" 下拉菜单中，取消选中 "**启用浏览器链接**"。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-147">In the Browser Link dropdown menu, uncheck **Enable Browser Link**.</span></span> 

    ![](using-browser-link/_static/image12.png)
- <span data-ttu-id="7c0ef-148">在 web.config 文件中，在 appSettings 节中添加一个名为 "vs： EnableBrowserLink" 的项，其值为 "false"。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-148">In the Web.config file, add a key named "vs:EnableBrowserLink" with the value "false" in the appSettings section.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- <span data-ttu-id="7c0ef-149">在 web.config 文件中，将 "debug" 设置为 "false"。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-149">In the Web.config file, set debug to false.</span></span> 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a><span data-ttu-id="7c0ef-150">它的工作原理是什么？</span><span class="sxs-lookup"><span data-stu-id="7c0ef-150">How Does It Work?</span></span>

<span data-ttu-id="7c0ef-151">Browser Link 使用[SignalR](../../../signalr/index.md)在 Visual Studio 与浏览器之间创建信道。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-151">Browser Link uses [SignalR](../../../signalr/index.md) to create a communication channel between Visual Studio and the browser.</span></span> <span data-ttu-id="7c0ef-152">启用浏览器链接后，Visual Studio 将充当 SignalR 服务器，多个客户端（浏览器）可以连接到该服务器。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-152">When Browser Link is enabled, Visual Studio acts as a SignalR server that multiple clients (browsers) can connect to.</span></span> <span data-ttu-id="7c0ef-153">浏览器链接还向 ASP.NET 注册 HTTP 模块。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-153">Browser Link also registers an HTTP module with ASP.NET.</span></span> <span data-ttu-id="7c0ef-154">此模块从服务器中插入特殊 &lt;脚本&gt; 对每个页面请求的引用。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-154">This module injects special &lt;script&gt; references into every page request from the server.</span></span> <span data-ttu-id="7c0ef-155">可以通过在浏览器中选择 "查看源" 来查看脚本引用。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-155">You can see the script references by selecting "View source" in the browser.</span></span>

![](using-browser-link/_static/image13.png)

<span data-ttu-id="7c0ef-156">不会修改您的源文件。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-156">Your source files are not modified.</span></span> <span data-ttu-id="7c0ef-157">HTTP 模块动态地插入脚本引用。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-157">The HTTP module injects the script references dynamically.</span></span>

<span data-ttu-id="7c0ef-158">由于浏览器端代码都是 JavaScript，因此它适用于[SignalR 支持](../../../signalr/overview/getting-started/supported-platforms.md)的所有浏览器，无需任何浏览器插件。</span><span class="sxs-lookup"><span data-stu-id="7c0ef-158">Because the browser-side code is all JavaScript, it works on all browsers that [SignalR supports](../../../signalr/overview/getting-started/supported-platforms.md), without requiring any browser plug-in.</span></span>
