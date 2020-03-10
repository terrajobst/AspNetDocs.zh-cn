---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: 在 Katana 中启用 Windows 身份验证 |Microsoft Docs
author: MikeWasson
description: 本文介绍如何在 Katana 中启用 Windows 身份验证。 它介绍了两种方案：使用 IIS 托管 Katana，并使用 HttpListener 来自主 Katt 。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500294"
---
# <a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="139b1-104">在 Katana 中启用 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="139b1-104">Enabling Windows Authentication in Katana</span></span>

<span data-ttu-id="139b1-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="139b1-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="139b1-106">本文介绍如何在 Katana 中启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="139b1-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="139b1-107">它介绍了两种方案：使用 IIS 托管 Katana，并使用 HttpListener 在自定义进程中自承载 Katana。</span><span class="sxs-lookup"><span data-stu-id="139b1-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="139b1-108">感谢 Barry Dorrans、David Matson 和丽丽 Ross，查看本文。</span><span class="sxs-lookup"><span data-stu-id="139b1-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>

<span data-ttu-id="139b1-109">Katana 是 Microsoft 的[OWIN](http://owin.org/)的实现，它是用于 .Net 的开放 Web 界面。</span><span class="sxs-lookup"><span data-stu-id="139b1-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="139b1-110">可在[此处](an-overview-of-project-katana.md)阅读 OWIN 和 Katana 简介。</span><span class="sxs-lookup"><span data-stu-id="139b1-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="139b1-111">OWIN 体系结构具有多个层：</span><span class="sxs-lookup"><span data-stu-id="139b1-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="139b1-112">Host：管理运行 OWIN 管道的进程。</span><span class="sxs-lookup"><span data-stu-id="139b1-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="139b1-113">服务器：打开网络套接字并侦听请求。</span><span class="sxs-lookup"><span data-stu-id="139b1-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="139b1-114">中间件：处理 HTTP 请求和响应。</span><span class="sxs-lookup"><span data-stu-id="139b1-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="139b1-115">Katana 目前提供两台服务器，两者都支持 Windows 集成身份验证：</span><span class="sxs-lookup"><span data-stu-id="139b1-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="139b1-116">**Owin. SystemWeb**。</span><span class="sxs-lookup"><span data-stu-id="139b1-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="139b1-117">在 ASP.NET 管道中使用 IIS。</span><span class="sxs-lookup"><span data-stu-id="139b1-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="139b1-118">**Owin. HttpListener**。</span><span class="sxs-lookup"><span data-stu-id="139b1-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="139b1-119">使用[系统 HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)。</span><span class="sxs-lookup"><span data-stu-id="139b1-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="139b1-120">此服务器当前是自承载 Katana 时的默认选项。</span><span class="sxs-lookup"><span data-stu-id="139b1-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="139b1-121">Katana 当前不提供用于 Windows 身份验证的 OWIN 中间件，因为此功能已在服务器中可用。</span><span class="sxs-lookup"><span data-stu-id="139b1-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>

## <a name="windows-authentication-in-iis"></a><span data-ttu-id="139b1-122">IIS 中的 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="139b1-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="139b1-123">使用 Owin，只需在 IIS 中启用 Windows 身份验证即可。</span><span class="sxs-lookup"><span data-stu-id="139b1-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="139b1-124">首先，让我们使用 "ASP.NET 空 Web 应用程序" 项目模板创建一个新的 ASP.NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="139b1-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="139b1-125">接下来，添加 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="139b1-125">Next, add NuGet packages.</span></span> <span data-ttu-id="139b1-126">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="139b1-126">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="139b1-127">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="139b1-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="139b1-128">现在，使用以下代码添加名为 `Startup` 的类：</span><span class="sxs-lookup"><span data-stu-id="139b1-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="139b1-129">这就是创建一个在 IIS 上运行的 OWIN "Hello world" 应用程序所需的全部工作。</span><span class="sxs-lookup"><span data-stu-id="139b1-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="139b1-130">按 F5 调试该应用程序。</span><span class="sxs-lookup"><span data-stu-id="139b1-130">Press F5 to debug the application.</span></span> <span data-ttu-id="139b1-131">应会看到“Hello World!”</span><span class="sxs-lookup"><span data-stu-id="139b1-131">You should see "Hello World!"</span></span> <span data-ttu-id="139b1-132">在浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="139b1-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="139b1-133">接下来，我们将在 IIS Express 中启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="139b1-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="139b1-134">从 "**视图**" 菜单中选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="139b1-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="139b1-135">单击解决方案资源管理器中的项目名称，查看项目属性。</span><span class="sxs-lookup"><span data-stu-id="139b1-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="139b1-136">在 "**属性**" 窗口中，将 "**匿名身份验证**"**设置为 "** **已禁用**" 并将**Windows 身份验证**设置为</span><span class="sxs-lookup"><span data-stu-id="139b1-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="139b1-137">当你从 Visual Studio 中运行应用程序时，IIS Express 将需要用户的 Windows 凭据。</span><span class="sxs-lookup"><span data-stu-id="139b1-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="139b1-138">可以通过使用[Fiddler](http://fiddler2.com/home)或其他 HTTP 调试工具来查看此。</span><span class="sxs-lookup"><span data-stu-id="139b1-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="139b1-139">下面是一个 HTTP 响应示例：</span><span class="sxs-lookup"><span data-stu-id="139b1-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="139b1-140">此响应中的 WWW 身份验证标头指示服务器支持[协商](http://www.ietf.org/rfc/rfc4559.txt)协议，该协议使用 KERBEROS 或 NTLM。</span><span class="sxs-lookup"><span data-stu-id="139b1-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="139b1-141">稍后，当你将应用程序部署到服务器时，请按照[以下步骤](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication)在该服务器上的 IIS 中启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="139b1-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="139b1-142">HttpListener 中的 Windows 身份验证</span><span class="sxs-lookup"><span data-stu-id="139b1-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="139b1-143">如果你使用的是 Owin 的 HttpListener，则可以直接在**HttpListener**实例上启用 Windows 身份验证。</span><span class="sxs-lookup"><span data-stu-id="139b1-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="139b1-144">首先，创建一个新的控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="139b1-144">First, create a new console application.</span></span> <span data-ttu-id="139b1-145">接下来，添加 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="139b1-145">Next, add NuGet packages.</span></span> <span data-ttu-id="139b1-146">从 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="139b1-146">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="139b1-147">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="139b1-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="139b1-148">现在，使用以下代码添加名为 `Startup` 的类：</span><span class="sxs-lookup"><span data-stu-id="139b1-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="139b1-149">此类在以前实现相同的 "Hello world" 示例，但它还将 Windows 身份验证设置为身份验证方案。</span><span class="sxs-lookup"><span data-stu-id="139b1-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="139b1-150">在 `Main` 函数内，启动 OWIN 管道：</span><span class="sxs-lookup"><span data-stu-id="139b1-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="139b1-151">可以在 Fiddler 中发送请求，以确认应用程序正在使用 Windows 身份验证：</span><span class="sxs-lookup"><span data-stu-id="139b1-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="139b1-152">相关主题</span><span class="sxs-lookup"><span data-stu-id="139b1-152">Related Topics</span></span>

[<span data-ttu-id="139b1-153">项目 Katana 概述</span><span class="sxs-lookup"><span data-stu-id="139b1-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="139b1-154">System.Net.HttpListener</span><span class="sxs-lookup"><span data-stu-id="139b1-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="139b1-155">了解 MVC 5 中的 OWIN Forms 身份验证</span><span class="sxs-lookup"><span data-stu-id="139b1-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)
