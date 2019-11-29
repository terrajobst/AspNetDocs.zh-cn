---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: 入门 ASP.NET 4.7 Web 窗体和 Visual Studio 2017 |Microsoft Docs
author: Erikre
description: 此循序渐进教程系列将指导你使用 ASP.NET 4.7 和 Microsoft Visual Studio 构建 ASP.NET Web 窗体应用程序的基础知识
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615456"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a><span data-ttu-id="a8164-103">与 ASP.NET 4.5 Web 窗体和 Visual Studio 2017 入门</span><span class="sxs-lookup"><span data-stu-id="a8164-103">Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2017</span></span>

<span data-ttu-id="a8164-104">[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="a8164-104">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

<span data-ttu-id="a8164-105">本系列教程演示如何使用 ASP.NET 4.5 和 Microsoft Visual Studio 2017 生成 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="a8164-105">This tutorial series shows you how to build an ASP.NET Web Forms application with ASP.NET 4.5 and Microsoft Visual Studio 2017.</span></span> 

## <a name="introduction"></a><span data-ttu-id="a8164-106">简介</span><span class="sxs-lookup"><span data-stu-id="a8164-106">Introduction</span></span>

<span data-ttu-id="a8164-107">本教程系列将指导你使用 Visual Studio 2017 和 ASP.NET 4.5 创建 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="a8164-107">This tutorial series guides you through creating an ASP.NET Web Forms application using Visual Studio 2017 and ASP.NET 4.5.</span></span> <span data-ttu-id="a8164-108">你将创建一个名为 " **Wingtip 玩具**" 的应用程序，它是一个可联机销售项目的简化店面网站。</span><span class="sxs-lookup"><span data-stu-id="a8164-108">You'll create an application named **Wingtip Toys** - a simplified storefront web site selling items online.</span></span> <span data-ttu-id="a8164-109">在序列中，将突出显示新的 ASP.NET 4.5 功能。</span><span class="sxs-lookup"><span data-stu-id="a8164-109">During the series, new ASP.NET 4.5 features are highlighted.</span></span>

### <a name="target-audience"></a><span data-ttu-id="a8164-110">目标受众</span><span class="sxs-lookup"><span data-stu-id="a8164-110">Target audience</span></span>

<span data-ttu-id="a8164-111">对于 ASP.NET Web 窗体，开发人员是本系列教程的目标受众。</span><span class="sxs-lookup"><span data-stu-id="a8164-111">Developers new to ASP.NET Web Forms are the target audience for this tutorial series.</span></span>

<span data-ttu-id="a8164-112">你应了解以下几个方面的知识：</span><span class="sxs-lookup"><span data-stu-id="a8164-112">You should have some knowledge in the following areas:</span></span>

- <span data-ttu-id="a8164-113">面向对象的编程（OOP）和语言</span><span class="sxs-lookup"><span data-stu-id="a8164-113">Object-oriented programming (OOP) and languages</span></span>
- <span data-ttu-id="a8164-114">Web 开发（HTML、CSS、JavaScript）</span><span class="sxs-lookup"><span data-stu-id="a8164-114">Web development (HTML, CSS, JavaScript)</span></span>
- <span data-ttu-id="a8164-115">关系数据库</span><span class="sxs-lookup"><span data-stu-id="a8164-115">Relational databases</span></span>
- <span data-ttu-id="a8164-116">N 层体系结构</span><span class="sxs-lookup"><span data-stu-id="a8164-116">N-tier architecture</span></span>

<span data-ttu-id="a8164-117">若要查看这些区域，请考虑学习以下内容：</span><span class="sxs-lookup"><span data-stu-id="a8164-117">To review these areas, consider studying the following content:</span></span>

- [<span data-ttu-id="a8164-118">Visual C# 入门</span><span class="sxs-lookup"><span data-stu-id="a8164-118">Getting Started with Visual C#</span></span>](https://msdn.microsoft.com/library/a72418yk.aspx)
- <span data-ttu-id="a8164-119">[Web 开发](https://msdn.microsoft.com/beginner/bb308760.aspx)， [HTML，CSS，JavaScript，SQL，PHP，JQuery](http://w3schools.com/)</span><span class="sxs-lookup"><span data-stu-id="a8164-119">[Web Development](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)</span></span>
- [<span data-ttu-id="a8164-120">关系数据库</span><span class="sxs-lookup"><span data-stu-id="a8164-120">Relational database</span></span>](http://en.wikipedia.org/wiki/Relational_database)
- [<span data-ttu-id="a8164-121">多层体系结构</span><span class="sxs-lookup"><span data-stu-id="a8164-121">Multitier architecture</span></span>](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a><span data-ttu-id="a8164-122">应用程序功能</span><span class="sxs-lookup"><span data-stu-id="a8164-122">Application features</span></span>

<span data-ttu-id="a8164-123">本系列中介绍的 ASP.NET Web 窗体功能包括：</span><span class="sxs-lookup"><span data-stu-id="a8164-123">The ASP.NET Web Form features presented in this series include:</span></span>

- <span data-ttu-id="a8164-124">Web 应用程序项目（而非网站项目）</span><span class="sxs-lookup"><span data-stu-id="a8164-124">The Web Application Project (not Web Site Project)</span></span>
- <span data-ttu-id="a8164-125">Web Forms — Web 窗体</span><span class="sxs-lookup"><span data-stu-id="a8164-125">Web Forms</span></span>
- <span data-ttu-id="a8164-126">母版页，配置</span><span class="sxs-lookup"><span data-stu-id="a8164-126">Master Pages, Configuration</span></span>
- <span data-ttu-id="a8164-127">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="a8164-127">Bootstrap</span></span>
- <span data-ttu-id="a8164-128">实体框架 Code First，LocalDB</span><span class="sxs-lookup"><span data-stu-id="a8164-128">Entity Framework Code First, LocalDB</span></span>
- <span data-ttu-id="a8164-129">请求验证</span><span class="sxs-lookup"><span data-stu-id="a8164-129">Request Validation</span></span>
- <span data-ttu-id="a8164-130">强类型数据控件</span><span class="sxs-lookup"><span data-stu-id="a8164-130">Strongly-typed Data Controls</span></span>
- <span data-ttu-id="a8164-131">模型绑定</span><span class="sxs-lookup"><span data-stu-id="a8164-131">Model Binding</span></span>
- <span data-ttu-id="a8164-132">数据注释</span><span class="sxs-lookup"><span data-stu-id="a8164-132">Data Annotations</span></span>
- <span data-ttu-id="a8164-133">值提供程序</span><span class="sxs-lookup"><span data-stu-id="a8164-133">Value Providers</span></span>
- <span data-ttu-id="a8164-134">SSL 和 OAuth</span><span class="sxs-lookup"><span data-stu-id="a8164-134">SSL and OAuth</span></span>
- <span data-ttu-id="a8164-135">ASP.NET Identity、配置和授权</span><span class="sxs-lookup"><span data-stu-id="a8164-135">ASP.NET Identity, Configuration, and Authorization</span></span>
- <span data-ttu-id="a8164-136">非引人注目验证</span><span class="sxs-lookup"><span data-stu-id="a8164-136">Unobtrusive Validation</span></span>
- <span data-ttu-id="a8164-137">路由</span><span class="sxs-lookup"><span data-stu-id="a8164-137">Routing</span></span>
- <span data-ttu-id="a8164-138">ASP.NET 错误处理</span><span class="sxs-lookup"><span data-stu-id="a8164-138">ASP.NET Error Handling</span></span>

### <a name="application-scenarios-and-tasks"></a><span data-ttu-id="a8164-139">应用程序方案和任务</span><span class="sxs-lookup"><span data-stu-id="a8164-139">Application scenarios and tasks</span></span>

<span data-ttu-id="a8164-140">教程系列任务包括：</span><span class="sxs-lookup"><span data-stu-id="a8164-140">Tutorial series tasks include:</span></span>

- <span data-ttu-id="a8164-141">创建、查看和运行新项目</span><span class="sxs-lookup"><span data-stu-id="a8164-141">Creating, reviewing, and running a new project</span></span>
- <span data-ttu-id="a8164-142">创建数据库结构</span><span class="sxs-lookup"><span data-stu-id="a8164-142">Creating a database structure</span></span>
- <span data-ttu-id="a8164-143">初始化和播种数据库</span><span class="sxs-lookup"><span data-stu-id="a8164-143">Initializing and seeding a database</span></span>
- <span data-ttu-id="a8164-144">使用样式、图形和母版页自定义 UI</span><span class="sxs-lookup"><span data-stu-id="a8164-144">Customizing the UI with styles, graphics, and a master page</span></span>
- <span data-ttu-id="a8164-145">添加页面和导航</span><span class="sxs-lookup"><span data-stu-id="a8164-145">Adding pages and navigation</span></span>
- <span data-ttu-id="a8164-146">显示菜单详细信息和产品数据</span><span class="sxs-lookup"><span data-stu-id="a8164-146">Displaying menu details and product data</span></span>
- <span data-ttu-id="a8164-147">创建购物车</span><span class="sxs-lookup"><span data-stu-id="a8164-147">Creating a shopping cart</span></span>
- <span data-ttu-id="a8164-148">添加 SSL 和 OAuth 支持</span><span class="sxs-lookup"><span data-stu-id="a8164-148">Adding SSL and OAuth support</span></span>
- <span data-ttu-id="a8164-149">添加付款方式</span><span class="sxs-lookup"><span data-stu-id="a8164-149">Adding a payment method</span></span>
- <span data-ttu-id="a8164-150">包括管理员角色和应用程序的用户</span><span class="sxs-lookup"><span data-stu-id="a8164-150">Including an administrator role and a user to the application</span></span>
- <span data-ttu-id="a8164-151">限制对特定页面和文件夹的访问</span><span class="sxs-lookup"><span data-stu-id="a8164-151">Restricting access to specific pages and folder</span></span>
- <span data-ttu-id="a8164-152">将文件上传到 web 应用程序</span><span class="sxs-lookup"><span data-stu-id="a8164-152">Uploading a file to the web application</span></span>
- <span data-ttu-id="a8164-153">实现输入验证</span><span class="sxs-lookup"><span data-stu-id="a8164-153">Implementing input validation</span></span>
- <span data-ttu-id="a8164-154">注册 web 应用程序的路由</span><span class="sxs-lookup"><span data-stu-id="a8164-154">Registering routes for the web application</span></span>
- <span data-ttu-id="a8164-155">实现错误处理和错误日志记录</span><span class="sxs-lookup"><span data-stu-id="a8164-155">Implementing error handling and error logging</span></span>

## <a name="overview"></a><span data-ttu-id="a8164-156">概述</span><span class="sxs-lookup"><span data-stu-id="a8164-156">Overview</span></span>

<span data-ttu-id="a8164-157">本教程系列适用于熟悉编程概念的人员，但却是 ASP.NET Web 窗体的新手。</span><span class="sxs-lookup"><span data-stu-id="a8164-157">This tutorial series is intended for someone familiar with programming concepts, but new to ASP.NET Web Forms.</span></span> <span data-ttu-id="a8164-158">如果已熟悉 ASP.NET Web 窗体，此系列仍可帮助你了解新的 ASP.NET 4.5 功能。</span><span class="sxs-lookup"><span data-stu-id="a8164-158">If you're already familiar with ASP.NET Web Forms, this series can still help you learn about new ASP.NET 4.5 features.</span></span> <span data-ttu-id="a8164-159">对于不熟悉编程概念和 ASP.NET Web 窗体的读者，请参阅 ASP.NET 网站上的[入门](../../../index.md)部分中提供的其他 Web 窗体教程。</span><span class="sxs-lookup"><span data-stu-id="a8164-159">For readers unfamiliar with programming concepts and ASP.NET Web Forms, see the additional Web Forms tutorials provided in the [Getting Started](../../../index.md) section on the ASP.NET Web site.</span></span>

<span data-ttu-id="a8164-160">本系列教程提供了 ASP.NET 4.5，其中包含以下功能：</span><span class="sxs-lookup"><span data-stu-id="a8164-160">The ASP.NET 4.5 provided in this tutorial series includes the following features:</span></span>

- <span data-ttu-id="a8164-161">用于创建[支持多个 ASP.NET 框架](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add)（Web 窗体、MVC 和 Web API）的项目的简单 UI。</span><span class="sxs-lookup"><span data-stu-id="a8164-161">A simple UI for creating projects that offers [support for many ASP.NET frameworks](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) (Web Forms, MVC, and Web API).</span></span>
- <span data-ttu-id="a8164-162">[启动](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)、布局、主题和响应式设计框架。</span><span class="sxs-lookup"><span data-stu-id="a8164-162">[Bootstrap](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), a layout, theming, and responsive design framework.</span></span>
- <span data-ttu-id="a8164-163">[ASP.NET Identity](../../../../identity/index.md)，这是一个新的 ASP.NET 成员资格系统，该系统在所有 ASP.NET 框架中运行相同的功能，并且适用于除 IIS 之外的 web 托管软件。</span><span class="sxs-lookup"><span data-stu-id="a8164-163">[ASP.NET Identity](../../../../identity/index.md), a new ASP.NET membership system that works the same in all ASP.NET frameworks and works with web hosting software other than IIS.</span></span>
- [<span data-ttu-id="a8164-164">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="a8164-164">Entity Framework 6</span></span>](https://msdn.microsoft.com/data/ef.aspx)

  <span data-ttu-id="a8164-165">更新实体框架使你能够：</span><span class="sxs-lookup"><span data-stu-id="a8164-165">An update to the Entity Framework enabling you to:</span></span>
  - <span data-ttu-id="a8164-166">作为强类型对象检索和操作数据</span><span class="sxs-lookup"><span data-stu-id="a8164-166">Retrieve and manipulate data as strongly-typed objects</span></span>
  - <span data-ttu-id="a8164-167">异步访问数据</span><span class="sxs-lookup"><span data-stu-id="a8164-167">Access data asynchronously</span></span>
  - <span data-ttu-id="a8164-168">处理暂时性连接故障</span><span class="sxs-lookup"><span data-stu-id="a8164-168">Handle transient connection faults</span></span>
  - <span data-ttu-id="a8164-169">记录 SQL 语句</span><span class="sxs-lookup"><span data-stu-id="a8164-169">Log SQL statements</span></span>

<span data-ttu-id="a8164-170">有关完整的 ASP.NET 4.5 功能列表，请参阅[Visual Studio 2013 发行说明 ASP.NET 和 Web 工具](../../../../visual-studio/overview/2013/release-notes.md)。</span><span class="sxs-lookup"><span data-stu-id="a8164-170">For a complete ASP.NET 4.5 feature list, see [ASP.NET and Web Tools for Visual Studio 2013 Release Notes](../../../../visual-studio/overview/2013/release-notes.md).</span></span>

### <a name="the-wingtip-toys-sample-application"></a><span data-ttu-id="a8164-171">Wingtip 玩具示例应用程序</span><span class="sxs-lookup"><span data-stu-id="a8164-171">The Wingtip Toys sample application</span></span>

<span data-ttu-id="a8164-172">以下屏幕截图来自您在本教程系列中创建的 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="a8164-172">The following screenshots are from the ASP.NET Web Forms application that you create in this tutorial series.</span></span> <span data-ttu-id="a8164-173">在 Visual Studio 中运行应用程序时，将显示以下 web 主页。</span><span class="sxs-lookup"><span data-stu-id="a8164-173">When you run the application in Visual Studio, the following web Home page appears.</span></span>

![Wingtip 玩具-默认页面](introduction-and-overview/_static/image1.png)

<span data-ttu-id="a8164-175">你可以注册为新用户或以现有用户身份登录。</span><span class="sxs-lookup"><span data-stu-id="a8164-175">You can register as a new user, or sign in as an existing user.</span></span> <span data-ttu-id="a8164-176">顶部导航栏中提供了来自数据库的产品类别和产品的链接。</span><span class="sxs-lookup"><span data-stu-id="a8164-176">The top navigation has links to product categories and their products from the database.</span></span>

<span data-ttu-id="a8164-177">如果选择 "**产品**"，则会显示所有可用的产品。</span><span class="sxs-lookup"><span data-stu-id="a8164-177">If you select **Products**, all available products are displayed.</span></span> 

![Wingtip 玩具-产品](introduction-and-overview/_static/image2.png)

<span data-ttu-id="a8164-179">如果选择特定产品，则将显示产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="a8164-179">If you select a specific product, product details are displayed.</span></span>

![Wingtip 玩具-产品详细信息](introduction-and-overview/_static/image3.png)

<span data-ttu-id="a8164-181">用户可以使用 Web 窗体模板默认功能注册并登录。</span><span class="sxs-lookup"><span data-stu-id="a8164-181">As a user, you can register and sign in with Web Forms template default functionality.</span></span> <span data-ttu-id="a8164-182">本教程还介绍如何使用现有 Gmail 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="a8164-182">This tutorial also explains how to sign in using an existing Gmail account.</span></span> <span data-ttu-id="a8164-183">此外，您可以以管理员身份登录，以便在数据库中添加和删除产品。</span><span class="sxs-lookup"><span data-stu-id="a8164-183">Additionally, you can sign in as the administrator to add and remove products from the database.</span></span>

![Wingtip 玩具-登录](introduction-and-overview/_static/image4.png)

<span data-ttu-id="a8164-185">以用户身份登录后，可以将产品添加到购物车，并使用 PayPal 结帐。</span><span class="sxs-lookup"><span data-stu-id="a8164-185">Once you've signed in as a user, you can add products to the shopping cart and checkout with PayPal.</span></span> <span data-ttu-id="a8164-186">该示例应用程序设计用于在 PayPal 的开发人员沙盒中运行。</span><span class="sxs-lookup"><span data-stu-id="a8164-186">The sample application is designed to work in PayPal's developer sandbox.</span></span> <span data-ttu-id="a8164-187">不会进行实际的 money 交易。</span><span class="sxs-lookup"><span data-stu-id="a8164-187">No actual money transaction takes place.</span></span>

![Wingtip 玩具-购物车](introduction-and-overview/_static/image5.png)

<span data-ttu-id="a8164-189">PayPal 确认你的帐户、订单和付款信息。</span><span class="sxs-lookup"><span data-stu-id="a8164-189">PayPal confirms your account, order, and payment information.</span></span>

![Wingtip 玩具-PayPal](introduction-and-overview/_static/image6.png)

<span data-ttu-id="a8164-191">从 PayPal 返回后，你可以查看并完成你的订单。</span><span class="sxs-lookup"><span data-stu-id="a8164-191">After returning from PayPal, you can review and complete your order.</span></span>

![Wingtip 玩具-订购审核](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a><span data-ttu-id="a8164-193">先决条件</span><span class="sxs-lookup"><span data-stu-id="a8164-193">Prerequisites</span></span>

<span data-ttu-id="a8164-194">在开始之前，请确保已在计算机上安装以下软件：</span><span class="sxs-lookup"><span data-stu-id="a8164-194">Before you start, make sure the following software is installed on your computer:</span></span>

- <span data-ttu-id="a8164-195">[Microsoft Visual Studio 2017 或 Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="a8164-195">[Microsoft Visual Studio 2017 or Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).</span></span>

<span data-ttu-id="a8164-196">将自动安装 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="a8164-196">The .NET Framework is installed automatically.</span></span>

<span data-ttu-id="a8164-197">本教程系列使用 Microsoft Visual Studio Community 2017。</span><span class="sxs-lookup"><span data-stu-id="a8164-197">This tutorial series uses Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="a8164-198">您可以使用该方法或 Microsoft Visual Studio 2017 来完成本系列教程。</span><span class="sxs-lookup"><span data-stu-id="a8164-198">You can use either that or Microsoft Visual Studio 2017 to complete this tutorial series.</span></span>

<span data-ttu-id="a8164-199">请注意以下关于 Visual Studio 的内容：</span><span class="sxs-lookup"><span data-stu-id="a8164-199">Note the following about Visual Studio:</span></span>

* <span data-ttu-id="a8164-200">在本系列教程中，Microsoft Visual Studio 2017 和 Microsoft Visual Studio Community 2017 称为*Visual Studio* 。</span><span class="sxs-lookup"><span data-stu-id="a8164-200">Microsoft Visual Studio 2017 and Microsoft Visual Studio Community 2017 are referred to as *Visual Studio* throughout this tutorial series.</span></span>

* <span data-ttu-id="a8164-201">Visual Studio 2017 安装在已安装的任何较旧版本旁边。</span><span class="sxs-lookup"><span data-stu-id="a8164-201">Visual Studio 2017 is installed next to any older versions already installed.</span></span> <span data-ttu-id="a8164-202">可在 Visual Studio 2017 中打开在早期版本中创建的网站，并在以前的版本中继续打开。</span><span class="sxs-lookup"><span data-stu-id="a8164-202">Sites created in earlier versions can be opened in Visual Studio 2017 and continue to open in previous versions.</span></span>

* <span data-ttu-id="a8164-203">首次启动 Visual Studio 时，会假定你选择了*Web 开发*设置。</span><span class="sxs-lookup"><span data-stu-id="a8164-203">The first time you started Visual Studio, it is assumed you selected the *Web Development* settings.</span></span> <span data-ttu-id="a8164-204">有关详细信息，请参阅[如何：选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a8164-204">For more information, see [How to: Select Web Development Environment Settings](https://msdn.microsoft.com/library/ff521558.aspx).</span></span>

<span data-ttu-id="a8164-205">安装必备组件后，您就可以开始创建本教程系列中介绍的 Web 项目了。</span><span class="sxs-lookup"><span data-stu-id="a8164-205">After installing the prerequisites, you're ready to begin creating the Web project presented in this tutorial series.</span></span>

## <a name="download-the-sample-application"></a><span data-ttu-id="a8164-206">下载示例应用程序</span><span class="sxs-lookup"><span data-stu-id="a8164-206">Download the sample application</span></span>

 <span data-ttu-id="a8164-207">你可以随时从 MSDN 示例站点下载已完成的示例应用程序：</span><span class="sxs-lookup"><span data-stu-id="a8164-207">You can download the completed sample application at anytime from the MSDN Samples site:</span></span>

<span data-ttu-id="a8164-208">[与 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）入门</span><span class="sxs-lookup"><span data-stu-id="a8164-208">[Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)</span></span> 

 <span data-ttu-id="a8164-209">此下载包含以下各项：</span><span class="sxs-lookup"><span data-stu-id="a8164-209">This download has the following items:</span></span>

- <span data-ttu-id="a8164-210">*WingtipToys*文件夹中的示例应用程序。</span><span class="sxs-lookup"><span data-stu-id="a8164-210">The sample application in the *WingtipToys* folder.</span></span>
- <span data-ttu-id="a8164-211">用于在*WingtipToys*文件夹中的*WingtipToys*文件夹中创建示例应用程序的资源。</span><span class="sxs-lookup"><span data-stu-id="a8164-211">The resources used to create the sample application in the *WingtipToys-Assets* folder in the *WingtipToys* folder.</span></span>

<span data-ttu-id="a8164-212">下载文件为 *.zip*文件。</span><span class="sxs-lookup"><span data-stu-id="a8164-212">The download is a *.zip* file.</span></span> <span data-ttu-id="a8164-213">若要查看本教程系列创建的已完成项目，请在 .zip *C#* 文件中找到并选择该文件夹。</span><span class="sxs-lookup"><span data-stu-id="a8164-213">To see the completed project that this tutorial series creates, find and select the *C#* folder in the .zip file.</span></span> <span data-ttu-id="a8164-214">将C#文件夹保存到用于使用 Visual Studio 项目的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="a8164-214">Save the C# folder to the folder you use to work with Visual Studio projects.</span></span> <span data-ttu-id="a8164-215">默认情况下，Visual Studio 2017 项目文件夹为：</span><span class="sxs-lookup"><span data-stu-id="a8164-215">By default, the Visual Studio 2017 projects folder is:</span></span>

<span data-ttu-id="a8164-216"><strong>C:\Users&#92;</strong>  <strong><em>&lt;用户名&gt;</em></strong> <strong>\source\repos</strong></span><span class="sxs-lookup"><span data-stu-id="a8164-216"><strong>C:\Users&#92;</strong><strong><em>&lt;username&gt;</em></strong><strong>\source\repos</strong></span></span>

<span data-ttu-id="a8164-217">将***C#*** 文件夹重命名为***WingtipToys***。</span><span class="sxs-lookup"><span data-stu-id="a8164-217">Rename the ***C#*** folder to ***WingtipToys***.</span></span>

> [!NOTE]
> <span data-ttu-id="a8164-218">如果项目文件夹中已有一个名为*WingtipToys*的文件夹，请在将*C#* 文件夹重命名为*WingtipToys*之前暂时重命名该现有文件夹。</span><span class="sxs-lookup"><span data-stu-id="a8164-218">If you already have a folder named *WingtipToys* in your Projects folder, temporarily rename that existing folder before renaming the *C#* folder to *WingtipToys*.</span></span>

<span data-ttu-id="a8164-219">若要运行已完成的项目，请打开*WingtipToys*文件夹，然后双击*WingtipToys*文件。</span><span class="sxs-lookup"><span data-stu-id="a8164-219">To run the completed project, open the *WingtipToys* folder and double-click the *WingtipToys.sln* file.</span></span> <span data-ttu-id="a8164-220">Visual Studio 2017 打开项目。</span><span class="sxs-lookup"><span data-stu-id="a8164-220">Visual Studio 2017 opens the project.</span></span> <span data-ttu-id="a8164-221">接下来，在**解决方案资源管理器**中右键单击*default.aspx*文件，然后选择 **"在浏览器中查看"** 。</span><span class="sxs-lookup"><span data-stu-id="a8164-221">Next, right-click the *Default.aspx* file in **Solution Explorer** and select **View In Browser**.</span></span>

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a><span data-ttu-id="a8164-222">参加 ASP.NET Web Forms 测验以查看内容</span><span class="sxs-lookup"><span data-stu-id="a8164-222">Take a ASP.NET Web Forms quiz to review content</span></span>

<span data-ttu-id="a8164-223">完成本系列教程后，请进行测验来测试您的知识和强化关键概念。</span><span class="sxs-lookup"><span data-stu-id="a8164-223">After completing the tutorial series, take a quiz to test your knowledge and reinforce key concepts.</span></span> <span data-ttu-id="a8164-224">每个问题都提供了说明和指向其他指南的链接。</span><span class="sxs-lookup"><span data-stu-id="a8164-224">Each question provides an explanation and links to additional guidance.</span></span>

* [<span data-ttu-id="a8164-225">ASP.NET Web 窗体测验</span><span class="sxs-lookup"><span data-stu-id="a8164-225">ASP.NET Web Forms Quiz</span></span>](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a><span data-ttu-id="a8164-226">教程支持和注释</span><span class="sxs-lookup"><span data-stu-id="a8164-226">Tutorial support and comments</span></span>

<span data-ttu-id="a8164-227">对于问题和意见，请使用入门中包含的 Q 和部分，[其中包含 ASP.NET 4.5 Web Forms 和 Visual Studio 2013-Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）示例页面。</span><span class="sxs-lookup"><span data-stu-id="a8164-227">For questions and comments, use the Q and A section included on the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span>

<span data-ttu-id="a8164-228">欢迎使用本系列教程上的评论。</span><span class="sxs-lookup"><span data-stu-id="a8164-228">Comments on this tutorial series are welcome.</span></span> <span data-ttu-id="a8164-229">更新本系列教程后，每次都要考虑更正或改进建议。</span><span class="sxs-lookup"><span data-stu-id="a8164-229">When this tutorial series is updated, every effort is made to consider corrections or suggestions for improvements.</span></span>

<span data-ttu-id="a8164-230">如果发生错误，相应的错误消息可能会令人困惑，并没有关于如何修复此问题的好说明。</span><span class="sxs-lookup"><span data-stu-id="a8164-230">If an error occurs, the corresponding error messages could be confusing, with no good explanation on how to fix it.</span></span> <span data-ttu-id="a8164-231">若要获得帮助，你可以查看[ASP.NET 论坛](https://forums.asp.net/)。</span><span class="sxs-lookup"><span data-stu-id="a8164-231">For help, you can check the [ASP.NET forums](https://forums.asp.net/).</span></span> <span data-ttu-id="a8164-232">另一种好的来源是[入门使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013 Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）示例页的 "问答" 部分。</span><span class="sxs-lookup"><span data-stu-id="a8164-232">Another good source is the Q and A section in the [Getting Started with ASP.NET 4.5 Web Forms and Visual Studio 2013 - Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) sample page.</span></span> 

> [!div class="step-by-step"]
> [<span data-ttu-id="a8164-233">下一页</span><span class="sxs-lookup"><span data-stu-id="a8164-233">Next</span></span>](create-the-project.md)
