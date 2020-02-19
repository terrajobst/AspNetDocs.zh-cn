---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 （C#）简介Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457517"
---
# <a name="intro-to-aspnet-mvc-3-c"></a><span data-ttu-id="dd367-103">ASP.NET MVC 3 简介 (C#)</span><span class="sxs-lookup"><span data-stu-id="dd367-103">Intro to ASP.NET MVC 3 (C#)</span></span>

<span data-ttu-id="dd367-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="dd367-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="dd367-105">[此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="dd367-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="dd367-106">更安全的方法是遵循更多功能，并演示更多的功能。</span><span class="sxs-lookup"><span data-stu-id="dd367-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="dd367-107">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="dd367-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="dd367-108">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="dd367-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="dd367-109">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="dd367-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="dd367-110">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="dd367-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="dd367-111">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="dd367-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="dd367-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="dd367-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="dd367-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="dd367-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="dd367-114">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="dd367-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="dd367-115">本主题提供了包含C#源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="dd367-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="dd367-116">[下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="dd367-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="dd367-117">如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="dd367-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="dd367-118">所需操作</span><span class="sxs-lookup"><span data-stu-id="dd367-118">What You'll Build</span></span>

<span data-ttu-id="dd367-119">您将实现一个简单的电影列表应用程序，该应用程序支持从数据库创建、编辑和列出影片。</span><span class="sxs-lookup"><span data-stu-id="dd367-119">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="dd367-120">下面是要生成的应用程序的两个屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="dd367-120">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="dd367-121">它包含一个页面，其中显示了数据库中的电影列表：</span><span class="sxs-lookup"><span data-stu-id="dd367-121">It includes a page that displays a list of movies from a database:</span></span>

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

<span data-ttu-id="dd367-123">应用程序还可用于添加、编辑和删除电影，以及查看有关单个影片的详细信息。</span><span class="sxs-lookup"><span data-stu-id="dd367-123">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="dd367-124">所有数据输入方案都包括验证，以确保数据库中存储的数据是正确的。</span><span class="sxs-lookup"><span data-stu-id="dd367-124">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a><span data-ttu-id="dd367-125">将要学到的技能</span><span class="sxs-lookup"><span data-stu-id="dd367-125">Skills You'll Learn</span></span>

<span data-ttu-id="dd367-126">学习内容：</span><span class="sxs-lookup"><span data-stu-id="dd367-126">Here's what you'll learn:</span></span>

- <span data-ttu-id="dd367-127">如何创建新的 ASP.NET MVC 项目。</span><span class="sxs-lookup"><span data-stu-id="dd367-127">How to create a new ASP.NET MVC project.</span></span>
- <span data-ttu-id="dd367-128">如何创建 ASP.NET MVC 控制器和视图。</span><span class="sxs-lookup"><span data-stu-id="dd367-128">How to create ASP.NET MVC controllers and views.</span></span>
- <span data-ttu-id="dd367-129">如何使用实体框架 Code First 范例创建新数据库。</span><span class="sxs-lookup"><span data-stu-id="dd367-129">How to create a new database using the Entity Framework Code First paradigm.</span></span>
- <span data-ttu-id="dd367-130">如何检索和显示数据。</span><span class="sxs-lookup"><span data-stu-id="dd367-130">How to retrieve and display data.</span></span>
- <span data-ttu-id="dd367-131">如何编辑数据和启用数据验证。</span><span class="sxs-lookup"><span data-stu-id="dd367-131">How to edit data and enable data validation.</span></span>

## <a name="getting-started"></a><span data-ttu-id="dd367-132">入门</span><span class="sxs-lookup"><span data-stu-id="dd367-132">Getting Started</span></span>

<span data-ttu-id="dd367-133">首先运行 Visual Web Developer 2010 Express （"Visual Web Developer"），并从 "**开始**" 页选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="dd367-133">Start by running Visual Web Developer 2010 Express ("Visual Web Developer" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="dd367-134">Visual Web Developer 是一个 IDE 或集成开发环境。</span><span class="sxs-lookup"><span data-stu-id="dd367-134">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="dd367-135">就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd367-135">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="dd367-136">在 Visual Web Developer 中，顶部有一个工具栏，其中显示了可供你使用的各种选项。</span><span class="sxs-lookup"><span data-stu-id="dd367-136">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="dd367-137">还有一个菜单，该菜单提供了在 IDE 中执行任务的另一种方法。</span><span class="sxs-lookup"><span data-stu-id="dd367-137">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="dd367-138">（例如，可以使用菜单并选择 "**文件**" &gt; "**新建项目**"，而不是从**起始**页中选择 "**新建项目**"。）</span><span class="sxs-lookup"><span data-stu-id="dd367-138">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="dd367-139">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="dd367-139">Creating Your First Application</span></span>

<span data-ttu-id="dd367-140">您可以使用 Visual Basic 或 Visual C#作为编程语言来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd367-140">You can create applications using either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="dd367-141">选择左侧C#的 "视觉对象"，然后选择 " **ASP.NET MVC 3 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="dd367-141">Select Visual C# on the left and then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="dd367-142">将项目命名为 "MvcMovie"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="dd367-142">Name your project "MvcMovie" and then click **OK**.</span></span> <span data-ttu-id="dd367-143">（如果你喜欢 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。）</span><span class="sxs-lookup"><span data-stu-id="dd367-143">(If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.)</span></span>

![](intro-to-aspnet-mvc-3/_static/image5.png)

<span data-ttu-id="dd367-144">在 "**新建 ASP.NET MVC 3 项目**" 对话框中，选择 " **Internet 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="dd367-144">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="dd367-145">选中 "**使用 HTML5 标记**并将**Razor**保留为默认视图引擎"。</span><span class="sxs-lookup"><span data-stu-id="dd367-145">Check **Use HTML5 markup** and leave **Razor** as the default view engine.</span></span>

![](intro-to-aspnet-mvc-3/_static/image6.png)

<span data-ttu-id="dd367-146">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="dd367-146">Click **OK**.</span></span> <span data-ttu-id="dd367-147">Visual Web Developer 使用您刚创建的 ASP.NET MVC 项目的默认模板，因此您现在无需执行任何操作即可使用有效的应用程序！</span><span class="sxs-lookup"><span data-stu-id="dd367-147">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="dd367-148">这是一个简单的 "Hello World！"</span><span class="sxs-lookup"><span data-stu-id="dd367-148">This is a simple "Hello World!"</span></span> <span data-ttu-id="dd367-149">项目，这是启动应用程序的好地方。</span><span class="sxs-lookup"><span data-stu-id="dd367-149">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="dd367-150">从“调试”菜单中选择“启动调试”。</span><span class="sxs-lookup"><span data-stu-id="dd367-150">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="dd367-151">请注意，启动调试的键盘快捷方式是 F5。</span><span class="sxs-lookup"><span data-stu-id="dd367-151">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="dd367-152">使用 F5，Visual Web Developer 可以启动开发 web 服务器并运行您的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd367-152">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="dd367-153">然后，Visual Web Developer 会启动浏览器并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="dd367-153">Visual Web Developer then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="dd367-154">请注意，浏览器的地址栏会显示 `localhost`，而不是类似 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="dd367-154">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="dd367-155">这是因为 `localhost` 始终指向您自己的本地计算机，在本例中，该计算机运行刚构建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="dd367-155">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="dd367-156">当 Visual Web Developer 运行 web 项目时，会将随机端口用于 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="dd367-156">When Visual Web Developer runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="dd367-157">在下图中，随机端口号为43246。</span><span class="sxs-lookup"><span data-stu-id="dd367-157">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="dd367-158">运行应用程序时，可能会看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="dd367-158">When you run the application, you'll probably see a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image10.png)

<span data-ttu-id="dd367-159">右侧此默认模板提供两个要访问的页面和一个基本登录页。</span><span class="sxs-lookup"><span data-stu-id="dd367-159">Right out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="dd367-160">下一步是更改此应用程序的工作方式，并在此过程中了解有关 ASP.NET MVC 的一些相关信息。</span><span class="sxs-lookup"><span data-stu-id="dd367-160">The next step is to change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="dd367-161">关闭浏览器并更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="dd367-161">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="dd367-162">Next</span><span class="sxs-lookup"><span data-stu-id="dd367-162">Next</span></span>](adding-a-controller.md)
