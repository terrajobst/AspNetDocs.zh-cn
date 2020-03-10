---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: 在 ASP.NET 网页（Razor）站点中安装帮助程序 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET 网页（Razor）网站中安装帮助程序。 帮助器是一个可重用的组件，其中包括代码和每个的标记。
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518642"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="ede84-104">在 ASP.NET 网页（Razor）站点中安装帮助器</span><span class="sxs-lookup"><span data-stu-id="ede84-104">Installing a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="ede84-105">作者： [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="ede84-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ede84-106">本文介绍如何在 ASP.NET 网页（Razor）网站中安装帮助程序。</span><span class="sxs-lookup"><span data-stu-id="ede84-106">This article describes how to install a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="ede84-107">*帮助器*是一种可重用的组件，其中包括用于执行可能比较繁琐或复杂的任务的代码和标记。</span><span class="sxs-lookup"><span data-stu-id="ede84-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="ede84-108">学习内容：</span><span class="sxs-lookup"><span data-stu-id="ede84-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="ede84-109">如何在使用 WebMatrix 3 创建的网站中安装帮助程序。</span><span class="sxs-lookup"><span data-stu-id="ede84-109">How to install a helper in a website created using WebMatrix 3.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="ede84-110">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="ede84-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="ede84-111">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="ede84-111">WebMatrix 3</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="ede84-112">帮助器概述</span><span class="sxs-lookup"><span data-stu-id="ede84-112">Overview of Helpers</span></span>

<span data-ttu-id="ede84-113">用户经常想要在网页上执行的某些任务需要大量代码或需要额外的知识。</span><span class="sxs-lookup"><span data-stu-id="ede84-113">Some tasks that people often want to do on web pages require a lot of code or require extra knowledge.</span></span> <span data-ttu-id="ede84-114">示例包括显示数据图表;将 Twitter "关注" 按钮置于页面上;从网站发送电子邮件;裁剪或调整图像大小;为站点使用 PayPal。</span><span class="sxs-lookup"><span data-stu-id="ede84-114">Examples include displaying a chart for data; putting a Twitter "Follow" button on a page; sending email from your website; cropping or resizing images; using PayPal for your site.</span></span> <span data-ttu-id="ede84-115">为了便于执行这些类型的操作，ASP.NET 网页允许使用*帮助*程序。</span><span class="sxs-lookup"><span data-stu-id="ede84-115">To make it easy to do these kinds of things, ASP.NET Web Pages lets you use *helpers*.</span></span> <span data-ttu-id="ede84-116">帮助器是为站点安装的组件，可让你使用一条或两条 Razor 代码执行典型任务。</span><span class="sxs-lookup"><span data-stu-id="ede84-116">Helpers are components that you install for a site and that let you perform typical tasks by using just a line or two of Razor code.</span></span>

<span data-ttu-id="ede84-117">ASP.NET 网页内置了几个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="ede84-117">ASP.NET Web Pages has a few helpers built in.</span></span> <span data-ttu-id="ede84-118">但是，许多帮助程序都在使用 NuGet 包管理器提供的包（外接程序）中提供。</span><span class="sxs-lookup"><span data-stu-id="ede84-118">However, many helpers are available in packages (add-ins) that are provided using the NuGet package manager.</span></span> <span data-ttu-id="ede84-119">NuGet 允许您选择要安装的包，然后处理安装的所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="ede84-119">NuGet lets you select a package to install and then it takes care of all the details of the installation.</span></span>

## <a name="installing-a-helper-in-webmatrix-3"></a><span data-ttu-id="ede84-120">在 WebMatrix 3 中安装帮助器</span><span class="sxs-lookup"><span data-stu-id="ede84-120">Installing a Helper in WebMatrix 3</span></span>

1. <span data-ttu-id="ede84-121">在 WebMatrix 3 中，单击 " **NuGet** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="ede84-121">In WebMatrix 3, click the **NuGet** button.</span></span>

    ![WebMatrix 中的 "NuGet 库" 对话框](installing-helpers/_static/image1.png)
2. <span data-ttu-id="ede84-123">这会启动 NuGet 包管理器，并显示可用的包。</span><span class="sxs-lookup"><span data-stu-id="ede84-123">This launches the NuGet package manager and displays available packages.</span></span> <span data-ttu-id="ede84-124">在搜索框中，为要安装的帮助程序输入关键字。</span><span class="sxs-lookup"><span data-stu-id="ede84-124">In the search box, enter a keyword for the helper you want to install.</span></span>

    ![WebMatrix 中的 "NuGet 库" 对话框](installing-helpers/_static/image2.png)
3. <span data-ttu-id="ede84-126">选择该包，然后单击 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="ede84-126">Select the package and then click **Install**.</span></span> <span data-ttu-id="ede84-127">当系统询问你是否要安装包并指示你接受这些条款时，请单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="ede84-127">Click **Yes** when asked if you want to install the package and indicate that you accept the terms.</span></span>

     <span data-ttu-id="ede84-128">如果这是您第一次安装帮助器，NuGet 将在您的网站中创建用于组成帮助器的代码的文件夹。</span><span class="sxs-lookup"><span data-stu-id="ede84-128">If this is the first time you've installed a helper, NuGet creates folders in your website for the code that makes up the helper.</span></span>
4. <span data-ttu-id="ede84-129">若要卸载帮助程序，请单击 "**库**" 按钮，单击 "**已安装**" 选项卡，然后选择要卸载的包。</span><span class="sxs-lookup"><span data-stu-id="ede84-129">To uninstall a helper, click the **Gallery** button, click the **Installed** tab, and pick the package you want to uninstall.</span></span>

## <a name="installing-the-twitter-helper"></a><span data-ttu-id="ede84-130">安装 Twitter 帮助程序</span><span class="sxs-lookup"><span data-stu-id="ede84-130">Installing the Twitter helper</span></span>

<span data-ttu-id="ede84-131">Twitter API 的最新版本与通过 NuGet 安装的 Twitter 帮助程序不兼容。</span><span class="sxs-lookup"><span data-stu-id="ede84-131">The latest version of the Twitter API is not compatible with the Twitter helper you install through NuGet.</span></span> <span data-ttu-id="ede84-132">请参阅[Twitter helper With WebMatrix](twitter-helper.md)主题，了解有关如何在项目中设置 Twitter 帮助器的信息。</span><span class="sxs-lookup"><span data-stu-id="ede84-132">Instead, see the [Twitter Helper with WebMatrix](twitter-helper.md) topic for information about how to set up the Twitter helper in your project.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="ede84-133">其他资源</span><span class="sxs-lookup"><span data-stu-id="ede84-133">Additional Resources</span></span>

[<span data-ttu-id="ede84-134">介绍 ASP.NET 网页 2-编程基础知识</span><span class="sxs-lookup"><span data-stu-id="ede84-134">Introducing ASP.NET Web Pages 2 - Programming Basics</span></span>](../getting-started/introducing-razor-syntax-c.md)

[<span data-ttu-id="ede84-135">Twitter Helper with WebMatrix</span><span class="sxs-lookup"><span data-stu-id="ede84-135">Twitter Helper with WebMatrix</span></span>](twitter-helper.md)
