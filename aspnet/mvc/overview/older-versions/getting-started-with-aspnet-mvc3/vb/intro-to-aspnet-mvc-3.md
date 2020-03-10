---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 简介（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 24f7de303ef7f5a457bd509ecc6bd0e3be7e3d9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485492"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a><span data-ttu-id="3e7cb-103">ASP.NET MVC 3 简介 (VB)</span><span class="sxs-lookup"><span data-stu-id="3e7cb-103">Intro to ASP.NET MVC 3 (VB)</span></span>

<span data-ttu-id="3e7cb-104">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="3e7cb-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="3e7cb-105">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="3e7cb-106">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="3e7cb-107">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="3e7cb-108">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="3e7cb-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="3e7cb-109">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="3e7cb-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="3e7cb-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="3e7cb-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="3e7cb-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="3e7cb-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="3e7cb-112">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="3e7cb-113">本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="3e7cb-114">[下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="3e7cb-115">如果愿意C#，请切换到本教程的[ C#版本](../cs/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-115">If you prefer C#, switch to the [C# version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="3e7cb-116">本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-116">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="3e7cb-117">在开始之前，请确保已安装下列必备组件。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-117">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="3e7cb-118">可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-118">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="3e7cb-119">或者，你可以使用以下链接单独安装必备组件：</span><span class="sxs-lookup"><span data-stu-id="3e7cb-119">Alternatively, you can individually install the prerequisites using the following links:</span></span>

- [<span data-ttu-id="3e7cb-120">Visual Studio Web Developer Express SP1 必备组件</span><span class="sxs-lookup"><span data-stu-id="3e7cb-120">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [<span data-ttu-id="3e7cb-121">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="3e7cb-121">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- <span data-ttu-id="3e7cb-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）</span><span class="sxs-lookup"><span data-stu-id="3e7cb-122">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>

<span data-ttu-id="3e7cb-123">如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-123">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>

<span data-ttu-id="3e7cb-124">本主题提供了包含 VB 源代码的 Visual Web Developer 项目。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-124">A Visual Web Developer project with VB source code is available to accompany this topic.</span></span> <span data-ttu-id="3e7cb-125">[在此处下载 VB 版本](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-125">[Download the VB version here](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824).</span></span> <span data-ttu-id="3e7cb-126">如果你更愿意使用 CSharp，请切换到此教程的[CSharp 版本](../cs/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-126">If you prefer CSharp, switch to the [CSharp version](../cs/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="3e7cb-127">你将生成</span><span class="sxs-lookup"><span data-stu-id="3e7cb-127">What You'll Build</span></span>

<span data-ttu-id="3e7cb-128">您将实现一个简单的电影列表应用程序，该应用程序支持从数据库创建、编辑和列出影片。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-128">You'll implement a simple movie-listing application that supports creating, editing, and listing movies from a database.</span></span> <span data-ttu-id="3e7cb-129">下面是要生成的应用程序的两个屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-129">Below are two screenshots of the application you'll build.</span></span> <span data-ttu-id="3e7cb-130">它包含一个页面，其中显示了数据库中的电影列表：</span><span class="sxs-lookup"><span data-stu-id="3e7cb-130">It includes a page that displays a list of movies from a database:</span></span>

<span data-ttu-id="3e7cb-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3e7cb-131">[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)</span></span>

<span data-ttu-id="3e7cb-132">应用程序还可用于添加、编辑和删除电影，以及查看有关单个影片的详细信息。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-132">The application also lets you add, edit, and delete movies, as well as see details about individual ones.</span></span> <span data-ttu-id="3e7cb-133">所有数据输入方案都包括验证，以确保数据库中存储的数据是正确的。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-133">All data-entry scenarios include validation to ensure that the data stored in the database is correct.</span></span>

<span data-ttu-id="3e7cb-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3e7cb-134">[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="3e7cb-135">将要学到的技能</span><span class="sxs-lookup"><span data-stu-id="3e7cb-135">Skills You'll Learn</span></span>

<span data-ttu-id="3e7cb-136">学习内容：</span><span class="sxs-lookup"><span data-stu-id="3e7cb-136">Here's what you'll learn:</span></span>

- <span data-ttu-id="3e7cb-137">如何创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="3e7cb-137">How to create a new ASP.NET MVC project</span></span>
- <span data-ttu-id="3e7cb-138">如何使用实体框架代码优先创建新数据库</span><span class="sxs-lookup"><span data-stu-id="3e7cb-138">How to create a new database using Entity Framework code-first</span></span>
- <span data-ttu-id="3e7cb-139">如何创建 ASP.NET MVC 控制器和视图</span><span class="sxs-lookup"><span data-stu-id="3e7cb-139">How to create ASP.NET MVC controllers and views</span></span>
- <span data-ttu-id="3e7cb-140">如何检索和显示数据</span><span class="sxs-lookup"><span data-stu-id="3e7cb-140">How to retrieve and display data</span></span>
- <span data-ttu-id="3e7cb-141">如何编辑数据和启用数据验证</span><span class="sxs-lookup"><span data-stu-id="3e7cb-141">How to edit data and enable data validation</span></span>

## <a name="getting-started"></a><span data-ttu-id="3e7cb-142">入门</span><span class="sxs-lookup"><span data-stu-id="3e7cb-142">Getting Started</span></span>

<span data-ttu-id="3e7cb-143">首先运行 Visual Web Developer 2010 Express （简称 "VWD"），然后从**起始**页中选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-143">Start by running Visual Web Developer 2010 Express ("VWD" for short) and select **New Project** from the **Start** page.</span></span>

<span data-ttu-id="3e7cb-144">Visual Web Developer 是一个 IDE 或集成开发环境。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-144">Visual Web Developer is an IDE, or integrated development environment.</span></span> <span data-ttu-id="3e7cb-145">就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-145">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="3e7cb-146">在 Visual Web Developer 中，顶部有一个工具栏，其中显示了可供你使用的各种选项。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-146">In Visual Web Developer there's a toolbar along the top showing various options available to you.</span></span> <span data-ttu-id="3e7cb-147">还有一个菜单，该菜单提供了在 IDE 中执行任务的另一种方法。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-147">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="3e7cb-148">（例如，可以使用菜单并选择 "**文件**" &gt; "**新建项目**"，而不是从**起始**页中选择 "**新建项目**"。）</span><span class="sxs-lookup"><span data-stu-id="3e7cb-148">(For example, instead of selecting **New Project** from the **Start** page, you can use the menu and select **File** &gt; **New Project**.)</span></span>

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a><span data-ttu-id="3e7cb-149">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="3e7cb-149">Creating Your First Application</span></span>

<span data-ttu-id="3e7cb-150">您可以使用您选择的 Visual Basic 或 Visual C#作为编程语言来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-150">You can create applications using your choice of either Visual Basic or Visual C# as the programming language.</span></span> <span data-ttu-id="3e7cb-151">对于本教程，请选择左侧 Visual Basic，然后选择 " **ASP.NET MVC 3 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-151">For this tutorial, select Visual Basic on the left, then select **ASP.NET MVC 3 Web Application**.</span></span> <span data-ttu-id="3e7cb-152">将项目命名为 "MvcMovie"，然后单击 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-152">Name your project "MvcMovie" and then click **OK**.</span></span>

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

<span data-ttu-id="3e7cb-154">在 "**新建 ASP.NET MVC 3 项目**" 对话框中，选择 " **Internet 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-154">In the **New ASP.NET MVC 3 Project** dialog box, select **Internet Application**.</span></span> <span data-ttu-id="3e7cb-155">保留**Razor**作为默认视图引擎。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-155">Leave **Razor** as the default view engine.</span></span>

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

<span data-ttu-id="3e7cb-157">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-157">Click **OK**.</span></span> <span data-ttu-id="3e7cb-158">Visual Web Developer 使用您刚创建的 ASP.NET MVC 项目的默认模板，因此您现在无需执行任何操作即可使用有效的应用程序！</span><span class="sxs-lookup"><span data-stu-id="3e7cb-158">Visual Web Developer used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="3e7cb-159">这是一个简单的 "Hello World！"</span><span class="sxs-lookup"><span data-stu-id="3e7cb-159">This is a simple "Hello World!"</span></span> <span data-ttu-id="3e7cb-160">项目，这是启动应用程序的好地方。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-160">project, and it's a good place to start your application.</span></span>

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

<span data-ttu-id="3e7cb-161">从“调试”菜单中选择“启动调试”。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-161">From the **Debug** menu, select **Start Debugging**.</span></span>

![](intro-to-aspnet-mvc-3/_static/image11.png)

<span data-ttu-id="3e7cb-162">请注意，启动调试的键盘快捷方式是 F5。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-162">Notice that the keyboard shortcut to start debugging is F5.</span></span>

<span data-ttu-id="3e7cb-163">使用 F5，Visual Web Developer 可以启动开发 web 服务器并运行您的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-163">F5 causes Visual Web Developer to start a development web server and run your web application.</span></span> <span data-ttu-id="3e7cb-164">然后，VWD 启动浏览器并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-164">VWD then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="3e7cb-165">请注意，浏览器的地址栏会显示 `localhost`，而不是类似 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-165">Notice that the address bar of the browser says `localhost` and not something like `example.com`.</span></span> <span data-ttu-id="3e7cb-166">这是因为 `localhost` 始终指向您自己的本地计算机，在本例中，该计算机运行刚构建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-166">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="3e7cb-167">当 VWD 运行 web 项目时，该项目将使用一个随机端口。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-167">When VWD runs a web project, a random port is used for the project.</span></span> <span data-ttu-id="3e7cb-168">在下图中，随机端口号为43246。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-168">In the image below, the random port number is 43246.</span></span> <span data-ttu-id="3e7cb-169">你的项目可能会使用其他端口号。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-169">Your project will probably use a different port number.</span></span>

![](intro-to-aspnet-mvc-3/_static/image12.png)

<span data-ttu-id="3e7cb-170">此默认模板为你提供了两个要访问的页面和一个基本登录页。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-170">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="3e7cb-171">让我们更改此应用程序的工作方式，并在此过程中了解有关 ASP.NET MVC 的一些相关信息。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-171">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="3e7cb-172">关闭浏览器并更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="3e7cb-172">Close your browser and let's change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3e7cb-173">下一部分</span><span class="sxs-lookup"><span data-stu-id="3e7cb-173">Next</span></span>](adding-a-controller.md)
