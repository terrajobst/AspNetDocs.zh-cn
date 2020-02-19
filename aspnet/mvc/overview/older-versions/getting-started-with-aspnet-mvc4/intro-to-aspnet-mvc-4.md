---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 简介 |Microsoft Docs
author: Rick-Anderson
description: 如果本教程可在此处使用 Visual Studio 2013，则为已更新的版本。 新教程使用 ASP.NET MVC 5，它对 t 。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51709a9c6ddb39b8fcd1cd94cd08d530a595825a
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455537"
---
# <a name="intro-to-aspnet-mvc-4"></a><span data-ttu-id="b9efa-104">ASP.NET MVC 4 简介</span><span class="sxs-lookup"><span data-stu-id="b9efa-104">Intro to ASP.NET MVC 4</span></span>

<span data-ttu-id="b9efa-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="b9efa-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="b9efa-106">如果本教程可在[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，则为已更新的版本。</span><span class="sxs-lookup"><span data-stu-id="b9efa-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="b9efa-107">新教程使用 ASP.NET MVC 5，这在本教程中提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="b9efa-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
> <span data-ttu-id="b9efa-108">本教程将教你使用 Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC 4 Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="b9efa-108">This tutorial will teach you the basics of building an ASP.NET MVC 4 Web application using Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) or Visual Web Developer 2010 Express Service Pack 1.</span></span> <span data-ttu-id="b9efa-109">建议使用 Visual Studio 2012，无需安装任何内容即可完成本教程。</span><span class="sxs-lookup"><span data-stu-id="b9efa-109">Visual Studio 2012 is recommended, you won't need to install anything to complete the tutorial.</span></span> <span data-ttu-id="b9efa-110">如果你使用的是 Visual Studio 2010，则必须安装以下组件。</span><span class="sxs-lookup"><span data-stu-id="b9efa-110">If you are using Visual Studio 2010 you must install the components below.</span></span> <span data-ttu-id="b9efa-111">可以通过单击以下链接安装所有这些程序：</span><span class="sxs-lookup"><span data-stu-id="b9efa-111">You can install all of them by clicking the following links:</span></span>
>
> - [<span data-ttu-id="b9efa-112">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="b9efa-112">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="b9efa-113">ASP.NET MVC 4 的 WPI 安装程序</span><span class="sxs-lookup"><span data-stu-id="b9efa-113">WPI installer for ASP.NET MVC 4</span></span>](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [<span data-ttu-id="b9efa-114">LocalDB</span><span class="sxs-lookup"><span data-stu-id="b9efa-114">LocalDB</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [<span data-ttu-id="b9efa-115">SSDT</span><span class="sxs-lookup"><span data-stu-id="b9efa-115">SSDT</span></span>](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
>
> <span data-ttu-id="b9efa-116">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请安装[适用于 ASP.NET MVC 4 的 WPI 安装程序](https://go.microsoft.com/fwlink/?LinkId=243392)和： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)</span><span class="sxs-lookup"><span data-stu-id="b9efa-116">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the [WPI installer for ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392) and the: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)</span></span>
>
> <span data-ttu-id="b9efa-117">本主题提供了包含C#源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="b9efa-117">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="b9efa-118">[下载C#版本](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip)。</span><span class="sxs-lookup"><span data-stu-id="b9efa-118">[Download the C# version](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip).</span></span>
>
> <span data-ttu-id="b9efa-119">在本教程中，你将在 Visual Studio 中运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9efa-119">In the tutorial you run the application in Visual Studio.</span></span> <span data-ttu-id="b9efa-120">还可以通过将应用程序部署到托管提供程序来使应用程序在 Internet 上可用。</span><span class="sxs-lookup"><span data-stu-id="b9efa-120">You can also make the application available over the Internet by deploying it to a hosting provider.</span></span> <span data-ttu-id="b9efa-121">Microsoft 在免费的 microsoft [Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中为多达10个网站提供免费的 web 托管。</span><span class="sxs-lookup"><span data-stu-id="b9efa-121">Microsoft offers free web hosting for up to 10 web sites in a [free Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="b9efa-122">有关如何将 Visual Studio web 项目部署到 Microsoft Azure 网站的信息，请参阅[使用 Visual Studio 创建和部署 ASP.NET 网站和 SQL 数据库](https://docs.microsoft.com/dotnet/azure/)。</span><span class="sxs-lookup"><span data-stu-id="b9efa-122">For information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Create and deploy an ASP.NET web site and SQL Database with Visual Studio](https://docs.microsoft.com/dotnet/azure/).</span></span> <span data-ttu-id="b9efa-123">该教程还演示了如何使用 Entity Framework Code First 迁移将 SQL Server 数据库部署到 Microsoft Azure SQL 数据库（以前称为 SQL Azure）。</span><span class="sxs-lookup"><span data-stu-id="b9efa-123">That tutorial also shows how to use Entity Framework Code First Migrations to deploy your SQL Server database to Windows Azure SQL Database (formerly SQL Azure).</span></span>
>
> <span data-ttu-id="b9efa-124">本教程由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）编写。</span><span class="sxs-lookup"><span data-stu-id="b9efa-124">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="b9efa-125">所需操作</span><span class="sxs-lookup"><span data-stu-id="b9efa-125">What You'll Build</span></span>

> [!NOTE]
> <span data-ttu-id="b9efa-126">如果本教程可在[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，则为已更新的版本。</span><span class="sxs-lookup"><span data-stu-id="b9efa-126">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="b9efa-127">新教程使用 ASP.NET MVC 5，这在本教程中提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="b9efa-127">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>

<span data-ttu-id="b9efa-128">您将实现一个简单的电影列表应用程序，该应用程序支持从数据库创建、编辑、搜索和列出影片。</span><span class="sxs-lookup"><span data-stu-id="b9efa-128">You'll implement a simple movie-listing application that supports creating, editing, searching and listing movies from a database.</span></span> <span data-ttu-id="b9efa-129">下面是要生成的应用程序的两个屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="b9efa-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="b9efa-130">它包含一个页面，其中显示了数据库中的电影列表：</span><span class="sxs-lookup"><span data-stu-id="b9efa-130">It includes a page that displays a list of movies from a database:</span></span>

![](intro-to-aspnet-mvc-4/_static/image1.png)

<span data-ttu-id="b9efa-131">应用程序还可用于添加、编辑和删除电影，以及查看有关单个影片的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b9efa-131">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="b9efa-132">所有数据输入方案都包括验证，以确保数据库中存储的数据是正确的。</span><span class="sxs-lookup"><span data-stu-id="b9efa-132">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a><span data-ttu-id="b9efa-133">入门</span><span class="sxs-lookup"><span data-stu-id="b9efa-133">Getting Started</span></span>

<span data-ttu-id="b9efa-134">首先运行 Visual Studio Express 2012 或 Visual Web Developer 2010 Express。</span><span class="sxs-lookup"><span data-stu-id="b9efa-134">Start by running Visual Studio Express 2012 or Visual Web Developer 2010 Express.</span></span> <span data-ttu-id="b9efa-135">此系列中的大部分屏幕快照都使用 Visual Studio Express 2012，但你可以使用 Visual Studio 2010/SP1、Visual Studio 2012、Visual Studio Express 2012 或 Visual Web Developer 2010 Express 来完成本教程。</span><span class="sxs-lookup"><span data-stu-id="b9efa-135">Most of the screen shots in this series use Visual Studio Express 2012, but you can complete this tutorial with Visual Studio 2010/SP1, Visual Studio 2012, Visual Studio Express 2012 or Visual Web Developer 2010 Express.</span></span> <span data-ttu-id="b9efa-136">从**起始**页中选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="b9efa-136">Select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="b9efa-137">Visual Studio 是一个 IDE，或集成的开发环境。</span><span class="sxs-lookup"><span data-stu-id="b9efa-137">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="b9efa-138">就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9efa-138">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="b9efa-139">在 Visual Studio 中，顶部有一个工具栏，其中显示了可供你使用的各种选项。</span><span class="sxs-lookup"><span data-stu-id="b9efa-139">In Visual Studio there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="b9efa-140">还有一个菜单，该菜单提供了在 IDE 中执行任务的另一种方法。</span><span class="sxs-lookup"><span data-stu-id="b9efa-140">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="b9efa-141">（例如，可以使用菜单并选择 "**文件**" &gt; "**新建项目**"，而不是从**起始**页中选择 "**新建项目**"。）</span><span class="sxs-lookup"><span data-stu-id="b9efa-141">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="b9efa-142">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="b9efa-142">Creating Your First Application</span></span>

<span data-ttu-id="b9efa-143">您可以使用 Visual Basic 或 Visual C#作为编程语言来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9efa-143">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="b9efa-144">选择左侧C#的 "视觉对象"，然后选择 " **ASP.NET MVC 4 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="b9efa-144">Select Visual C# on the left and then select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="b9efa-145">将项目命名为 &quot;MvcMovie&quot; 然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="b9efa-145">Name your project &quot;MvcMovie&quot; and then click **OK**.</span></span>

![](intro-to-aspnet-mvc-4/_static/image4.png)

<span data-ttu-id="b9efa-146">在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="b9efa-146">In the **New ASP.NET MVC 4 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="b9efa-147">保留**Razor**作为默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="b9efa-147">Leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-4/_static/image5.png)

<span data-ttu-id="b9efa-148">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="b9efa-148">Click **OK**.</span></span> <span data-ttu-id="b9efa-149">Visual Studio 使用了你刚刚创建的 ASP.NET MVC 项目的默认模板，因此你现在无需执行任何操作即可使用有效的应用程序！</span><span class="sxs-lookup"><span data-stu-id="b9efa-149">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="b9efa-150">这是一个简单的 &quot;Hello World！&quot; 项目，它是启动应用程序的好地方。</span><span class="sxs-lookup"><span data-stu-id="b9efa-150">This is a simple &quot;Hello World!&quot; project, and it's a good place to start your application.</span></span>

![](intro-to-aspnet-mvc-4/_static/image6.png)

<span data-ttu-id="b9efa-151">从“调试”菜单中选择“启动调试”。</span><span class="sxs-lookup"><span data-stu-id="b9efa-151">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-4/_static/image7.png)

<span data-ttu-id="b9efa-152">请注意，启动调试的键盘快捷方式是 F5。</span><span class="sxs-lookup"><span data-stu-id="b9efa-152">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="b9efa-153">F5 会使 Visual Studio 启动 IIS Express 并运行你的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9efa-153">F5 causes Visual Studio to start IIS Express and run your web application.</span></span> <span data-ttu-id="b9efa-154">然后，Visual Studio 会启动浏览器并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="b9efa-154">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="b9efa-155">请注意，浏览器的地址栏会显示 `localhost`，而不是类似 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="b9efa-155">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="b9efa-156">这是因为 `localhost` 始终指向您自己的本地计算机，在本例中，该计算机运行刚构建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="b9efa-156">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="b9efa-157">当 Visual Studio 运行 web 项目时，会将随机端口用于 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="b9efa-157">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="b9efa-158">在下图中，端口号为41788。</span><span class="sxs-lookup"><span data-stu-id="b9efa-158">In the image below, the port number is 41788.</span></span> <span data-ttu-id="b9efa-159">运行应用程序时，可能会看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="b9efa-159">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-4/_static/image8.png)

<span data-ttu-id="b9efa-160">立即将此默认模板提供给你的 "主页"、"联系人" 和 "关于" 页。</span><span class="sxs-lookup"><span data-stu-id="b9efa-160">Right out of the box this default template gives you Home, Contact and About pages.</span></span> <span data-ttu-id="b9efa-161">它还支持注册和登录，并提供到 Facebook 和 Twitter 的链接。</span><span class="sxs-lookup"><span data-stu-id="b9efa-161">It also provides support to register and log in, and links to Facebook and Twitter.</span></span> <span data-ttu-id="b9efa-162">下一步是更改此应用程序的工作原理，并了解 ASP.NET MVC 的一些相关信息。</span><span class="sxs-lookup"><span data-stu-id="b9efa-162">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="b9efa-163">关闭浏览器并更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="b9efa-163">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b9efa-164">Next</span><span class="sxs-lookup"><span data-stu-id="b9efa-164">Next</span></span>](adding-a-controller.md)
