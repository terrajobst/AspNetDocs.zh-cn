---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 简介 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469796"
---
# <a name="intro-to-aspnet-mvc"></a><span data-ttu-id="10164-104">ASP.NET MVC 简介</span><span class="sxs-lookup"><span data-stu-id="10164-104">Intro to ASP.NET MVC</span></span>

<span data-ttu-id="10164-105">作者： [Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="10164-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="10164-106">如果本教程可在[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，则为已更新的版本。</span><span class="sxs-lookup"><span data-stu-id="10164-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="10164-107">新教程使用 ASP.NET MVC 5，这在本教程中提供了许多改进。</span><span class="sxs-lookup"><span data-stu-id="10164-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="10164-108">本教程介绍了 ASP.NET MVC 的基本知识。</span><span class="sxs-lookup"><span data-stu-id="10164-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="10164-109">你将创建一个简单的 web 应用程序，用于读取和写入数据库。</span><span class="sxs-lookup"><span data-stu-id="10164-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="10164-110">请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。</span><span class="sxs-lookup"><span data-stu-id="10164-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="10164-111">让我们使用[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)创建第一个 ASP.NET MVC Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="10164-111">Let's make our first ASP.NET MVC Web Application using [Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/).</span></span> <span data-ttu-id="10164-112">我们会创建一个小电影列表应用程序，让我们创建和列出电影。</span><span class="sxs-lookup"><span data-stu-id="10164-112">We'll make a little Movie list application that will let us create and list movies.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="10164-113">你将生成</span><span class="sxs-lookup"><span data-stu-id="10164-113">What You'll Build</span></span>

<span data-ttu-id="10164-114">下面是要生成的应用程序的两个屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="10164-114">Here are two screenshots of the application you'll build.</span></span> <span data-ttu-id="10164-115">您将获得一个包含各种列的简单影片表。</span><span class="sxs-lookup"><span data-stu-id="10164-115">You will have a simple table of movies with various columns.</span></span>

<span data-ttu-id="10164-116">[![电影列表-Windows Internet Explorer （12）](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="10164-116">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)</span></span>

<span data-ttu-id="10164-117">您将创建一个窗体，以便可以将电影添加到列表。</span><span class="sxs-lookup"><span data-stu-id="10164-117">And you'll have a Create Form so we can add movies to the list.</span></span>

<span data-ttu-id="10164-118">[![创建电影-Windows Internet Explorer （2）](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="10164-118">[![Create a Movie - Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)</span></span>

## <a name="skills-youll-learn"></a><span data-ttu-id="10164-119">将要学到的技能</span><span class="sxs-lookup"><span data-stu-id="10164-119">Skills You'll Learn</span></span>

<span data-ttu-id="10164-120">本教程将介绍使用 Visual Studio 生成 ASP.NET MVC Web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="10164-120">This tutorial will teach you the basics of building an ASP.NET MVC Web Application using Visual Studio.</span></span> <span data-ttu-id="10164-121">学习内容：</span><span class="sxs-lookup"><span data-stu-id="10164-121">You'll learn:</span></span>

- <span data-ttu-id="10164-122">如何创建新的 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="10164-122">How to create a new ASP.NET MVC Project</span></span>
- <span data-ttu-id="10164-123">如何使用 SQL Server 创建新数据库</span><span class="sxs-lookup"><span data-stu-id="10164-123">How to create a new Database with SQL Server</span></span>
- <span data-ttu-id="10164-124">如何创建 ASP.NET MVC 控制器和视图</span><span class="sxs-lookup"><span data-stu-id="10164-124">How to create ASP.NET MVC Controllers and Views</span></span>
- <span data-ttu-id="10164-125">如何检索和显示数据</span><span class="sxs-lookup"><span data-stu-id="10164-125">How to retrieve and display data</span></span>
- <span data-ttu-id="10164-126">如何编辑数据和启用数据验证</span><span class="sxs-lookup"><span data-stu-id="10164-126">How to edit data and enable data validation</span></span>
- <span data-ttu-id="10164-127">如何更新数据库架构</span><span class="sxs-lookup"><span data-stu-id="10164-127">How to update the database schema</span></span>

## <a name="get-started"></a><span data-ttu-id="10164-128">开始操作</span><span class="sxs-lookup"><span data-stu-id="10164-128">Get Started</span></span>

<span data-ttu-id="10164-129">首先，运行 Visual Web Developer 2010 Express （我将从现在开始将其称为 "VWD"），然后从 "开始" 屏幕中选择 "新建项目"。</span><span class="sxs-lookup"><span data-stu-id="10164-129">Start by running Visual Web Developer 2010 Express (I'll call it "VWD" from now on) and select New Project from the Start Screen.</span></span>

<span data-ttu-id="10164-130">Visual Web Developer 是 IDE 或集成开发人员环境。</span><span class="sxs-lookup"><span data-stu-id="10164-130">Visual Web Developer is an IDE, or Integrated Developer Environment.</span></span> <span data-ttu-id="10164-131">就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="10164-131">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="10164-132">顶部有一个工具栏，其中显示了你可以使用的各种选项，以及你还可以用来选择文件的菜单 |新项目。</span><span class="sxs-lookup"><span data-stu-id="10164-132">There's a toolbar along the top showing various options available to you, as well as the menu you could also have used to Select File | New project.</span></span>

<span data-ttu-id="10164-133">[Microsoft Visual Web Developer 2010 Express ![](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="10164-133">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)</span></span>

## <a name="creating-your-first-application"></a><span data-ttu-id="10164-134">创建第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="10164-134">Creating Your First Application</span></span>

<span data-ttu-id="10164-135">可以使用 Visual Basic 或视觉对象C#创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="10164-135">You can create applications using Visual Basic or Visual C#.</span></span> <span data-ttu-id="10164-136">现在，在左侧选择C# "视觉对象"，然后选择 "ASP.NET MVC 2 Web 应用程序"。</span><span class="sxs-lookup"><span data-stu-id="10164-136">For now, Select Visual C# on the left, then pick "ASP.NET MVC 2 Web Application."</span></span> <span data-ttu-id="10164-137">将项目命名为 "电影"，然后单击 "确定"。</span><span class="sxs-lookup"><span data-stu-id="10164-137">Name your project "Movies" and click OK.</span></span>

<span data-ttu-id="10164-138">[![新项目](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="10164-138">[![New Project](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)</span></span>

<span data-ttu-id="10164-139">右侧是解决方案资源管理器显示应用程序中的所有文件和文件夹。</span><span class="sxs-lookup"><span data-stu-id="10164-139">On the right-hand side is the Solution Explorer showing all the files and folders in your application.</span></span> <span data-ttu-id="10164-140">您可以在中间的大窗口中编辑代码并花费大部分时间。</span><span class="sxs-lookup"><span data-stu-id="10164-140">The big window in the middle is where you edit your code and spend most of your time.</span></span> <span data-ttu-id="10164-141">Visual Studio 使用了你刚刚创建的 ASP.NET MVC 项目的默认模板，因此你现在无需执行任何操作即可使用有效的应用程序！</span><span class="sxs-lookup"><span data-stu-id="10164-141">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="10164-142">这是一个简单的 "Hello World！</span><span class="sxs-lookup"><span data-stu-id="10164-142">This is a simple "Hello World!</span></span> <span data-ttu-id="10164-143">对于我们的应用程序来说，这是一个不错的开端。</span><span class="sxs-lookup"><span data-stu-id="10164-143">project, and it is a good place to start for our application.</span></span>

<span data-ttu-id="10164-144">[Microsoft Visual Web Developer 2010 Express ![](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="10164-144">[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)</span></span>

<span data-ttu-id="10164-145">选择工具栏上的 "播放" 按钮。</span><span class="sxs-lookup"><span data-stu-id="10164-145">Select the "play" button to the toolbar.</span></span>

![开始调试](getting-started-with-mvc-part1/_static/image11.png)

<span data-ttu-id="10164-147">它是一个指向右侧的绿色箭头，将编译您的程序并在 web 浏览器中启动您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="10164-147">It's a green arrow pointing to the right that will compile your program and start your application in a web browser.</span></span>

<span data-ttu-id="10164-148">*注意：你可以在键盘上按 F5，或者从 "调试" 菜单中选择 "调试-&gt;启动调试"。*</span><span class="sxs-lookup"><span data-stu-id="10164-148">*NOTE: You can instead press F5 on your keyboard, or select Debug-&gt;Start Debugging from the "Debug" menu.*</span></span>

<span data-ttu-id="10164-149">这样，Visual Web Developer 就可以启动开发 web 服务器并运行 web 应用程序（启用此操作无需进行配置或手动步骤）。</span><span class="sxs-lookup"><span data-stu-id="10164-149">This will cause Visual Web Developer to start a development web-server and run our web application (there are no configuration or manual steps required to enable this).</span></span> <span data-ttu-id="10164-150">然后，它将启动一个浏览器并将其配置为浏览应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="10164-150">It will then launch a browser and configure it to browse the application's home-page.</span></span> <span data-ttu-id="10164-151">请注意，浏览器的地址栏显示 "localhost"，而不是类似于 "example.com" 的内容。</span><span class="sxs-lookup"><span data-stu-id="10164-151">Notice below that the address bar of the browser says "localhost", and not something like example.com.</span></span> <span data-ttu-id="10164-152">这是因为，localhost 始终指向你自己的本地计算机-在本例中，这种情况下运行的是刚刚构建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="10164-152">That's because localhost always points to your own local computer - which in this case is running the application we just built.</span></span>

<span data-ttu-id="10164-153">[![主页](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="10164-153">[![Home Page](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)</span></span>

<span data-ttu-id="10164-154">此默认模板为你提供了两个要访问的页面和一个基本登录页。</span><span class="sxs-lookup"><span data-stu-id="10164-154">Out of the box this default template gives you two pages to visit and a basic login page.</span></span> <span data-ttu-id="10164-155">让我们更改此应用程序的工作方式，并在此过程中了解有关 ASP.NET MVC 的一些相关信息。</span><span class="sxs-lookup"><span data-stu-id="10164-155">Let's change how this application works and learn a little bit about ASP.NET MVC in the process.</span></span> <span data-ttu-id="10164-156">关闭浏览器并更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="10164-156">Close your browser and lets change some code.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="10164-157">下一部分</span><span class="sxs-lookup"><span data-stu-id="10164-157">Next</span></span>](getting-started-with-mvc-part2.md)
