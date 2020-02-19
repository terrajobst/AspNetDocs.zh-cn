---
uid: mvc/overview/getting-started/introduction/getting-started
title: 入门与 ASP.NET MVC 5 |Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: c74daa37f68dda641cae97d3b0c19718f62d474d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456382"
---
# <a name="getting-started-with-aspnet-mvc-5"></a><span data-ttu-id="77070-102">ASP.NET MVC 5 入门</span><span class="sxs-lookup"><span data-stu-id="77070-102">Getting started with ASP.NET MVC 5</span></span>

<span data-ttu-id="77070-103">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="77070-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE [consider RP](../../../../includes/razor.md)]

<span data-ttu-id="77070-104">本教程介绍使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)生成 ASP.NET MVC 5 web 应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="77070-104">This tutorial teaches you the basics of building an ASP.NET MVC 5 web app using [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="77070-105">本教程的最终源代码位于[GitHub](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)上。</span><span class="sxs-lookup"><span data-stu-id="77070-105">The final source code for the tutorial is located on [GitHub](https://github.com/aspnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie).</span></span>

<span data-ttu-id="77070-106">本教程作者： [Scott Guthrie](https://weblogs.asp.net/scottgu/) （twitter[@scottgu](https://twitter.com/scottgu) ）、 [scott Hanselman](http://www.hanselman.com/blog/) （Twitter： [@shanselman](https://twitter.com/shanselman) ）和[Rick Anderson](https://twitter.com/RickAndMSFT) （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）</span><span class="sxs-lookup"><span data-stu-id="77070-106">This tutorial was written by [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](https://twitter.com/shanselman) ), and [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )</span></span>

<span data-ttu-id="77070-107">需要一个 Azure 帐户才能将此应用部署到 Azure：</span><span class="sxs-lookup"><span data-stu-id="77070-107">You need an Azure account to deploy this app to Azure:</span></span>

- <span data-ttu-id="77070-108">可以[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。</span><span class="sxs-lookup"><span data-stu-id="77070-108">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="77070-109">可以[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - MSDN 订阅每月提供可用来试用付费版 Azure 服务的信用额度。</span><span class="sxs-lookup"><span data-stu-id="77070-109">You can [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="get-started"></a><span data-ttu-id="77070-110">入门</span><span class="sxs-lookup"><span data-stu-id="77070-110">Get started</span></span>

<span data-ttu-id="77070-111">首先[安装 Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="77070-111">Start by [installing Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="77070-112">然后打开 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="77070-112">Then, open Visual Studio.</span></span>

<span data-ttu-id="77070-113">Visual Studio 是一个 IDE，或集成的开发环境。</span><span class="sxs-lookup"><span data-stu-id="77070-113">Visual Studio is an IDE, or integrated development environment.</span></span> <span data-ttu-id="77070-114">就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。</span><span class="sxs-lookup"><span data-stu-id="77070-114">Just like you use Microsoft Word to write documents, you'll use an IDE to create applications.</span></span> <span data-ttu-id="77070-115">在 Visual Studio 中，底部有一个列表，其中显示了可供你使用的各种选项。</span><span class="sxs-lookup"><span data-stu-id="77070-115">In Visual Studio, there's a list along the bottom showing various options available to you.</span></span> <span data-ttu-id="77070-116">还有一个菜单，该菜单提供了在 IDE 中执行任务的另一种方法。</span><span class="sxs-lookup"><span data-stu-id="77070-116">There's also a menu that provides another way to perform tasks in the IDE.</span></span> <span data-ttu-id="77070-117">例如，你可以使用菜单栏并选择 "**文件**" > "**新建项目**"，而不是在**起始页**上选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="77070-117">For example, instead of selecting **New Project** on the **Start page**, you can use the menu bar and select **File** > **New Project**.</span></span>

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a><span data-ttu-id="77070-118">创建第一个应用</span><span class="sxs-lookup"><span data-stu-id="77070-118">Create your first app</span></span>

<span data-ttu-id="77070-119">在 "**开始" 页**上，选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="77070-119">On the **Start page**, select **New Project**.</span></span> <span data-ttu-id="77070-120">在 "**新建项目**" 对话框中，选择左侧的**视觉对象C#** 类别，然后选择 " **web**"，然后选择 " **ASP.NET Web 应用程序（.NET Framework）** " 项目模板。</span><span class="sxs-lookup"><span data-stu-id="77070-120">In the **New project** dialog box, select the **Visual C#** category on the left, then **Web**, and then select the **ASP.NET Web Application (.NET Framework)** project template.</span></span> <span data-ttu-id="77070-121">将项目命名为 "MvcMovie"，然后选择 **"确定**"。</span><span class="sxs-lookup"><span data-stu-id="77070-121">Name your project "MvcMovie" and then choose **OK**.</span></span>

![](getting-started/_static/image2.png)

<span data-ttu-id="77070-122">在 "**新建 ASP.NET Web 应用程序**" 对话框中，选择 " **MVC** "，然后选择 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="77070-122">In the **New ASP.NET Web Application** dialog, choose **MVC** and then choose **OK**.</span></span>

![](getting-started/_static/image3.png)

<span data-ttu-id="77070-123">Visual Studio 使用了你刚刚创建的 ASP.NET MVC 项目的默认模板，因此你现在无需执行任何操作即可使用有效的应用程序！</span><span class="sxs-lookup"><span data-stu-id="77070-123">Visual Studio used a default template for the ASP.NET MVC project you just created, so you have a working application right now without doing anything!</span></span> <span data-ttu-id="77070-124">这是一个简单的 "Hello World！"</span><span class="sxs-lookup"><span data-stu-id="77070-124">This is a simple "Hello World!"</span></span> <span data-ttu-id="77070-125">项目，这是启动应用程序的好地方。</span><span class="sxs-lookup"><span data-stu-id="77070-125">project, and it's a good place to start your application.</span></span>

![](getting-started/_static/image4.png)

<span data-ttu-id="77070-126">按 **F5** 开始调试。</span><span class="sxs-lookup"><span data-stu-id="77070-126">Press **F5** to start debugging.</span></span> <span data-ttu-id="77070-127">按**F5**时，Visual Studio 将启动[IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview)并运行你的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="77070-127">When you press **F5**, Visual Studio starts [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) and runs your web app.</span></span> <span data-ttu-id="77070-128">然后，Visual Studio 会启动浏览器并打开应用程序的主页。</span><span class="sxs-lookup"><span data-stu-id="77070-128">Visual Studio then launches a browser and opens the application's home page.</span></span> <span data-ttu-id="77070-129">请注意，浏览器的地址栏会显示 `localhost:port#`，而不是类似 `example.com`。</span><span class="sxs-lookup"><span data-stu-id="77070-129">Notice that the address bar of the browser says `localhost:port#` and not something like `example.com`.</span></span> <span data-ttu-id="77070-130">这是因为 `localhost` 始终指向您自己的本地计算机，在本例中，该计算机运行刚构建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="77070-130">That's because `localhost` always points to your own local computer, which in this case is running the application you just built.</span></span> <span data-ttu-id="77070-131">当 Visual Studio 运行 web 项目时，会将随机端口用于 web 服务器。</span><span class="sxs-lookup"><span data-stu-id="77070-131">When Visual Studio runs a web project, a random port is used for the web server.</span></span> <span data-ttu-id="77070-132">在下图中，端口号为1234。</span><span class="sxs-lookup"><span data-stu-id="77070-132">In the image below, the port number is 1234.</span></span> <span data-ttu-id="77070-133">运行应用程序时，将看到不同的端口号。</span><span class="sxs-lookup"><span data-stu-id="77070-133">When you run the application, you'll see a different port number.</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="77070-134">立即将此默认模板提供给您 `Home`、`Contact`和 `About` 页面。</span><span class="sxs-lookup"><span data-stu-id="77070-134">Right out of the box this default template gives you `Home`, `Contact`, and `About` pages.</span></span> <span data-ttu-id="77070-135">下图不显示 "**主页**"、"**关于**" 和 "**联系人**" 链接。</span><span class="sxs-lookup"><span data-stu-id="77070-135">The image below doesn't show the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="77070-136">根据浏览器窗口的大小，可能需要单击导航图标才能看到这些链接。</span><span class="sxs-lookup"><span data-stu-id="77070-136">Depending on the size of your browser window, you might need to click the navigation icon to see these links.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="77070-137">该应用程序还为注册和登录提供支持。</span><span class="sxs-lookup"><span data-stu-id="77070-137">The application also provides support to register and log in.</span></span> <span data-ttu-id="77070-138">下一步是更改此应用程序的工作原理，并了解 ASP.NET MVC 的一些相关信息。</span><span class="sxs-lookup"><span data-stu-id="77070-138">The next step is to change how this application works and learn a little bit about ASP.NET MVC.</span></span> <span data-ttu-id="77070-139">关闭 ASP.NET MVC 应用程序并更改某些代码。</span><span class="sxs-lookup"><span data-stu-id="77070-139">Close the ASP.NET MVC application and let's change some code.</span></span>

<span data-ttu-id="77070-140">有关当前教程的列表，请参阅[MVC 推荐的文章](../mvc-learning-sequence.md)。</span><span class="sxs-lookup"><span data-stu-id="77070-140">For a list of current tutorials, see [MVC recommended articles](../mvc-learning-sequence.md).</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="77070-141">查看此应用在 Azure 上运行</span><span class="sxs-lookup"><span data-stu-id="77070-141">See this app running on Azure</span></span>

<span data-ttu-id="77070-142">要查看作为实时 web 应用运行的已完成站点吗？</span><span class="sxs-lookup"><span data-stu-id="77070-142">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="77070-143">只需单击以下按钮，即可将应用程序的完整版本部署到 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="77070-143">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/aspnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

<span data-ttu-id="77070-144">需要一个 Azure 帐户才能将此解决方案部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="77070-144">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="77070-145">如果还没有帐户，请使用以下选项之一创建一个帐户：</span><span class="sxs-lookup"><span data-stu-id="77070-145">If you don't already have an account, use one of the following options to create one:</span></span>

- <span data-ttu-id="77070-146">[免费打开 Azure 帐户](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-获取可用来试用付费版 Azure 服务的信用额度，甚至在用完信用额度后，你仍可以保留帐户和使用免费的 azure 服务。</span><span class="sxs-lookup"><span data-stu-id="77070-146">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="77070-147">[激活 Visual studio 订阅者权益](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers)-你的 visual studio 订阅每月为你提供可用于付费 Azure 服务的信用额度。</span><span class="sxs-lookup"><span data-stu-id="77070-147">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="77070-148">Next</span><span class="sxs-lookup"><span data-stu-id="77070-148">Next</span></span>](adding-a-controller.md)
