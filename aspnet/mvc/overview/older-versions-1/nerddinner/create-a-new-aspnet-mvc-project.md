---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 创建新的 ASP.NET MVC 项目 |Microsoft Docs
author: microsoft
description: 步骤1说明了如何就地放置基本 NerdDinner 应用程序结构。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469238"
---
# <a name="create-a-new-aspnet-mvc-project"></a><span data-ttu-id="3c7bc-103">新建 ASP.NET MVC 项目</span><span class="sxs-lookup"><span data-stu-id="3c7bc-103">Create a New ASP.NET MVC Project</span></span>

<span data-ttu-id="3c7bc-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3c7bc-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="3c7bc-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="3c7bc-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="3c7bc-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第1步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-106">This is step 1 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="3c7bc-107">步骤1说明了如何就地放置基本 NerdDinner 应用程序结构。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-107">Step 1 shows you how to put the basic NerdDinner application structure in place.</span></span>
> 
> <span data-ttu-id="3c7bc-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-1-file-gtnew-project"></a><span data-ttu-id="3c7bc-109">NerdDinner 步骤1：文件-&gt;新项目</span><span class="sxs-lookup"><span data-stu-id="3c7bc-109">NerdDinner Step 1: File-&gt;New Project</span></span>

<span data-ttu-id="3c7bc-110">在 Visual Studio 2008 或免费的 Visual Web Developer 2008 Express 中，通过选择 "**文件&gt;新的" 项目**"菜单项开始我们的 NerdDinner 应用程序。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-110">We'll begin our NerdDinner application by selecting the **File-&gt;New Project** menu item within either Visual Studio 2008 or the free Visual Web Developer 2008 Express.</span></span>

<span data-ttu-id="3c7bc-111">这将显示 "新建项目" 对话框。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-111">This will bring up the "New Project" dialog.</span></span> <span data-ttu-id="3c7bc-112">若要创建新的 ASP.NET MVC 应用程序，我们将选择对话框左侧的 "Web" 节点，然后选择右侧的 "ASP.NET MVC Web 应用程序" 项目模板：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-112">To create a new ASP.NET MVC application, we'll select the "Web" node on the left-hand side of the dialog and then choose the "ASP.NET MVC Web Application" project template on the right:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image1.png)

<span data-ttu-id="3c7bc-113">*重要提示：请确保已下载并安装 ASP.NET MVC-否则它不会显示在 "新建项目" 对话框中。如果尚未安装，则可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 （在 "Web 平台-&gt;框架和运行时" 一节中提供了 ASP.NET MVC）。*</span><span class="sxs-lookup"><span data-stu-id="3c7bc-113">*Important: Make sure you've downloaded and installed ASP.NET MVC - otherwise it won't show up in the New Project dialog. You can use V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) if you haven't installed it yet (ASP.NET MVC is available within the "Web Platform-&gt;Frameworks and Runtimes" section).*</span></span>

<span data-ttu-id="3c7bc-114">我们会将新项目命名为 "NerdDinner"，然后单击 "确定" 按钮进行创建。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-114">We'll name the new project we are going to create "NerdDinner" and then click the "ok" button to create it.</span></span>

<span data-ttu-id="3c7bc-115">单击 "确定" 时，Visual Studio 将显示一个额外的对话框，提示我们还可以选择为新应用程序创建单元测试项目。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-115">When we click "ok" Visual Studio will bring up an additional dialog that prompts us to optionally create a unit test project for the new application as well.</span></span> <span data-ttu-id="3c7bc-116">此单元测试项目使我们能够创建自动测试来验证应用程序的功能和行为（我们将在本教程的后面部分介绍如何执行此操作）。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-116">This unit test project enables us to create automated tests that verify the functionality and behavior of our application (something we'll cover how to-do later in this tutorial).</span></span>

![](create-a-new-aspnet-mvc-project/_static/image2.png)

<span data-ttu-id="3c7bc-117">以上对话框中的 "测试框架" 下拉列表中填充了计算机上安装的所有可用 ASP.NET MVC 单元测试项目模板。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-117">The "Test framework" dropdown in the above dialog is populated with all available ASP.NET MVC unit test project templates installed on the machine.</span></span> <span data-ttu-id="3c7bc-118">可下载的版本可用于 NUnit、MBUnit 和 XUnit。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-118">Versions can be downloaded for NUnit, MBUnit, and XUnit.</span></span> <span data-ttu-id="3c7bc-119">此外，还支持内置 Visual Studio 单元测试框架。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-119">The built-in Visual Studio Unit Test framework is also supported.</span></span>

<span data-ttu-id="3c7bc-120">*注意： Visual Studio 单元测试框架仅适用于 Visual Studio 2008 Professional 和更高版本。如果使用 VS 2008 Standard Edition 或 Visual Web Developer 2008 Express，则需要下载并安装 ASP.NET MVC 的 NUnit、MBUnit 或 XUnit 扩展，以便显示此对话框。如果未安装任何测试框架，则不会显示该对话框。*</span><span class="sxs-lookup"><span data-stu-id="3c7bc-120">*Note: The Visual Studio Unit Test Framework is only available with Visual Studio 2008 Professional and higher versions. If you are using VS 2008 Standard Edition or Visual Web Developer 2008 Express you will need to download and install the NUnit, MBUnit or XUnit extensions for ASP.NET MVC in order for this dialog to be shown. The dialog will not display if there aren't any test frameworks installed.*</span></span>

<span data-ttu-id="3c7bc-121">我们将使用我们创建的测试项目的默认 "NerdDinner" 名称，并使用 "Visual Studio 单元测试" 框架选项。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-121">We'll use the default "NerdDinner.Tests" name for the test project we create, and use the "Visual Studio Unit Test" framework option.</span></span> <span data-ttu-id="3c7bc-122">单击 "确定" 按钮时，Visual Studio 将为我们创建一个包含两个项目的解决方案-一个用于我们的 web 应用程序，另一个用于我们的单元测试：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-122">When we click the "ok" button Visual Studio will create a solution for us with two projects in it - one for our web application and one for our unit tests:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a><span data-ttu-id="3c7bc-123">检查 NerdDinner 目录结构</span><span class="sxs-lookup"><span data-stu-id="3c7bc-123">Examining the NerdDinner directory structure</span></span>

<span data-ttu-id="3c7bc-124">当使用 Visual Studio 创建新的 ASP.NET MVC 应用程序时，它会自动将许多文件和目录添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-124">When you create a new ASP.NET MVC application with Visual Studio, it automatically adds a number of files and directories to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image4.png)

<span data-ttu-id="3c7bc-125">默认情况下，ASP.NET MVC 项目具有六个顶级目录：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-125">ASP.NET MVC projects by default have six top-level directories:</span></span>

| <span data-ttu-id="3c7bc-126">**目录**</span><span class="sxs-lookup"><span data-stu-id="3c7bc-126">**Directory**</span></span> | <span data-ttu-id="3c7bc-127">**目的**</span><span class="sxs-lookup"><span data-stu-id="3c7bc-127">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="3c7bc-128">**/Controllers**</span><span class="sxs-lookup"><span data-stu-id="3c7bc-128">**/Controllers**</span></span> | <span data-ttu-id="3c7bc-129">放置处理 URL 请求的控制器类的位置</span><span class="sxs-lookup"><span data-stu-id="3c7bc-129">Where you put Controller classes that handle URL requests</span></span> |
| <span data-ttu-id="3c7bc-130">**/Models**</span><span class="sxs-lookup"><span data-stu-id="3c7bc-130">**/Models**</span></span> | <span data-ttu-id="3c7bc-131">放置表示和操作数据的类的位置</span><span class="sxs-lookup"><span data-stu-id="3c7bc-131">Where you put classes that represent and manipulate data</span></span> |
| <span data-ttu-id="3c7bc-132">**/Views**</span><span class="sxs-lookup"><span data-stu-id="3c7bc-132">**/Views**</span></span> | <span data-ttu-id="3c7bc-133">放置负责呈现输出的 UI 模板文件的位置</span><span class="sxs-lookup"><span data-stu-id="3c7bc-133">Where you put UI template files that are responsible for rendering output</span></span> |
| <span data-ttu-id="3c7bc-134">**/Scripts**</span><span class="sxs-lookup"><span data-stu-id="3c7bc-134">**/Scripts**</span></span> | <span data-ttu-id="3c7bc-135">在其中放置 JavaScript 库文件和脚本（.js）</span><span class="sxs-lookup"><span data-stu-id="3c7bc-135">Where you put JavaScript library files and scripts (.js)</span></span> |
| <span data-ttu-id="3c7bc-136">**/Content**</span><span class="sxs-lookup"><span data-stu-id="3c7bc-136">**/Content**</span></span> | <span data-ttu-id="3c7bc-137">放置 CSS 和映像文件的位置以及其他非动态/非 JavaScript 内容</span><span class="sxs-lookup"><span data-stu-id="3c7bc-137">Where you put CSS and image files, and other non-dynamic/non-JavaScript content</span></span> |
| <span data-ttu-id="3c7bc-138">**/App\_数据**</span><span class="sxs-lookup"><span data-stu-id="3c7bc-138">**/App\_Data**</span></span> | <span data-ttu-id="3c7bc-139">存储要读取/写入的数据文件的位置。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-139">Where you store data files you want to read/write.</span></span> |

<span data-ttu-id="3c7bc-140">ASP.NET MVC 不需要此结构。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-140">ASP.NET MVC does not require this structure.</span></span> <span data-ttu-id="3c7bc-141">事实上，处理大型应用程序的开发人员通常会在多个项目中对应用程序进行分区，以使其更易于管理（例如：数据模型类通常与 web 应用程序在单独的类库项目中）。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-141">In fact, developers working on large applications will typically partition the application up across multiple projects to make it more manageable (for example: data model classes often go in a separate class library project from the web application).</span></span> <span data-ttu-id="3c7bc-142">不过，默认的项目结构提供了一个非常好的默认目录约定，可以使用它来使应用程序保持干净整洁。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-142">The default project structure, however, does provide a nice default directory convention that we can use to keep our application concerns clean.</span></span>

<span data-ttu-id="3c7bc-143">展开/Controllers 目录后，我们会发现，Visual Studio 会将两个控制器类（HomeController 和 AccountController）添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-143">When we expand the /Controllers directory we'll find that Visual Studio added two controller classes – HomeController and AccountController – by default to the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image5.png)

<span data-ttu-id="3c7bc-144">当我们展开/Views 目录时，将在默认情况下，找到三个子目录–/Home、/Account 和/Shared –其中的多个模板文件也会添加到项目中：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-144">When we expand the /Views directory, we'll find three sub-directories – /Home, /Account and /Shared – as well as several template files within them were also added to the project by default:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image6.png)

<span data-ttu-id="3c7bc-145">展开 "/Content" 和 "/Scripts" 目录时，会找到一个用于为站点上的所有 HTML 提供样式的 web.config 文件，以及可以在应用程序中启用 ASP.NET AJAX 和 jQuery 支持的 JavaScript 库：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-145">When we expand the /Content and /Scripts directories, we'll find a Site.css file that is used to style all HTML on the site, as well as JavaScript libraries that can enable ASP.NET AJAX and jQuery support within the application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image7.png)

<span data-ttu-id="3c7bc-146">展开 NerdDinner 项目时，我们会看到两个包含控制器类的单元测试的类：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-146">When we expand the NerdDinner.Tests project we'll find two classes that contain unit tests for our controller classes:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image8.png)

<span data-ttu-id="3c7bc-147">Visual Studio 添加的这些默认文件为我们提供了一个用于工作的工作应用程序的基本结构，即主页、页面、帐户登录/注销/注册页和未经处理的错误页（所有有线和开箱即用）。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-147">These default files added by Visual Studio provide us with a basic structure for a working application - complete with home page, about page, account login/logout/registration pages, and an unhandled error page (all wired-up and working out of the box).</span></span>

### <a name="running-the-nerddinner-application"></a><span data-ttu-id="3c7bc-148">运行 NerdDinner 应用程序</span><span class="sxs-lookup"><span data-stu-id="3c7bc-148">Running the NerdDinner Application</span></span>

<span data-ttu-id="3c7bc-149">可以通过选择 "**调试"&gt;、"启动调试**" 或 "**调试-&gt;启动而不调试**" 菜单项来运行项目：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-149">We can run the project by choosing either the **Debug-&gt;Start Debugging** or **Debug-&gt;Start Without Debugging** menu items:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image9.png)

<span data-ttu-id="3c7bc-150">这将启动 Visual Studio 附带的内置 ASP.NET Web 服务器，并运行应用程序：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-150">This will launch the built-in ASP.NET Web-server that comes with Visual Studio, and run our application:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image10.png)

<span data-ttu-id="3c7bc-151">下面是新项目（URL： "/"）在运行时的主页：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-151">Below is the home page for our new project (URL: "/") when it runs:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image11.png)

<span data-ttu-id="3c7bc-152">单击 "关于" 选项卡将显示 "关于" 页（URL： "/Home/About"）：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-152">Clicking the "About" tab displays an about page (URL: "/Home/About"):</span></span>

![](create-a-new-aspnet-mvc-project/_static/image12.png)

<span data-ttu-id="3c7bc-153">单击右上方的 "登录" 链接将转到登录页（URL： "/Account/LogOn"）</span><span class="sxs-lookup"><span data-stu-id="3c7bc-153">Clicking the "Log On" link on the top-right takes us to a Login page (URL: "/Account/LogOn")</span></span>

![](create-a-new-aspnet-mvc-project/_static/image13.png)

<span data-ttu-id="3c7bc-154">如果没有登录帐户，我们可以单击 "注册" 链接（URL： "/Account/Register"）创建一个：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-154">If we don't have a login account we can click the register link (URL: "/Account/Register") to create one:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image14.png)

<span data-ttu-id="3c7bc-155">默认情况下，在创建新项目时，会添加用于实现上述 home、about 和注销/注册功能的代码。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-155">The code to implement the above home, about, and logout/ register functionality was added by default when we created our new project.</span></span> <span data-ttu-id="3c7bc-156">我们会将其用作应用程序的起点。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-156">We'll use it as the starting point of our application.</span></span>

### <a name="testing-the-nerddinner-application"></a><span data-ttu-id="3c7bc-157">测试 NerdDinner 应用程序</span><span class="sxs-lookup"><span data-stu-id="3c7bc-157">Testing the NerdDinner Application</span></span>

<span data-ttu-id="3c7bc-158">如果使用的是专业版或更高版本的 Visual Studio 2008，则可以使用 Visual Studio 中的内置单元测试 IDE 支持来测试项目：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-158">If we are using the Professional Edition or higher version of Visual Studio 2008, we can use the built-in unit testing IDE support within Visual Studio to test the project:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image15.png)

<span data-ttu-id="3c7bc-159">选择上述选项之一将打开 IDE 中的 "测试结果" 窗格，并在包含在新项目中的27个单元测试中为我们提供 "通过/失败" 状态，涵盖内置功能：</span><span class="sxs-lookup"><span data-stu-id="3c7bc-159">Choosing one of the above options will open the "Test Results" pane within the IDE and provide us with pass/fail status on the 27 unit tests included in our new project that cover the built-in functionality:</span></span>

![](create-a-new-aspnet-mvc-project/_static/image16.png)

<span data-ttu-id="3c7bc-160">稍后在本教程中，我们将详细介绍自动测试，并添加其他涵盖我们实现的应用程序功能的单元测试。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-160">Later in this tutorial we'll talk more about automated testing and add additional unit tests that cover the application functionality we implement.</span></span>

### <a name="next-step"></a><span data-ttu-id="3c7bc-161">下一步</span><span class="sxs-lookup"><span data-stu-id="3c7bc-161">Next Step</span></span>

<span data-ttu-id="3c7bc-162">现在，我们已经获得了一个基本的应用程序结构。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-162">We've now got a basic application structure in place.</span></span> <span data-ttu-id="3c7bc-163">现在，让我们[创建一个用于存储应用程序数据的数据库](create-a-database.md)。</span><span class="sxs-lookup"><span data-stu-id="3c7bc-163">Let's now [create a database to store our application data](create-a-database.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3c7bc-164">[上一页](introducing-the-nerddinner-tutorial.md)
> [下一页](create-a-database.md)</span><span class="sxs-lookup"><span data-stu-id="3c7bc-164">[Previous](introducing-the-nerddinner-tutorial.md)
[Next](create-a-database.md)</span></span>
