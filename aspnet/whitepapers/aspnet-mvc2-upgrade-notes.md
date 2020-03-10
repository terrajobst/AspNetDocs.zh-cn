---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: 将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2 |Microsoft Docs
author: rick-anderson
description: 本文档介绍了如何使用向导将 ASP.NET MVC 1.0 应用程序手动升级为 ASP.NET MVC 2。 此文档还适用于 d 。
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517298"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a><span data-ttu-id="8eb61-104">将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2 应用程序</span><span class="sxs-lookup"><span data-stu-id="8eb61-104">Upgrading an ASP.NET MVC 1.0 Application to ASP.NET MVC 2</span></span>

> <span data-ttu-id="8eb61-105">本文档介绍了如何使用向导将 ASP.NET MVC 1.0 应用程序手动升级为 ASP.NET MVC 2。</span><span class="sxs-lookup"><span data-stu-id="8eb61-105">This document describes both how to upgrade manually and with a wizard an ASP.NET MVC 1.0 Application to ASP.NET MVC 2.</span></span> <span data-ttu-id="8eb61-106">此文档还可供[下载](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span><span class="sxs-lookup"><span data-stu-id="8eb61-106">This document is also available for [Download](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)</span></span>

## <a name="introduction"></a><span data-ttu-id="8eb61-107">简介</span><span class="sxs-lookup"><span data-stu-id="8eb61-107">Introduction</span></span>

<span data-ttu-id="8eb61-108">ASP.NET MVC 2 可与同一服务器上的 ASP.NET MVC 1.0 并行安装。</span><span class="sxs-lookup"><span data-stu-id="8eb61-108">ASP.NET MVC 2 can be installed side by side with ASP.NET MVC 1.0 on the same server.</span></span> <span data-ttu-id="8eb61-109">这使应用程序开发人员可以灵活选择何时将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2。</span><span class="sxs-lookup"><span data-stu-id="8eb61-109">This gives application developers flexibility in choosing when to upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2.</span></span>

<span data-ttu-id="8eb61-110">Visual Studio 2010 包含一个向导，该向导将使用 Visual Studio 2008 生成的现有 ASP.NET MVC 1.0 项目升级到 ASP.NET MVC 2。</span><span class="sxs-lookup"><span data-stu-id="8eb61-110">Visual Studio 2010 includes a wizard that upgrades existing ASP.NET MVC 1.0 projects built with Visual Studio 2008 to ASP.NET MVC 2.</span></span> <span data-ttu-id="8eb61-111">通过在 Visual Studio 2010 中打开 ASP.NET MVC 1.0 项目来启动升级向导。</span><span class="sxs-lookup"><span data-stu-id="8eb61-111">The upgrade wizard is initiated by opening an ASP.NET MVC 1.0 project in Visual Studio 2010.</span></span>

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a><span data-ttu-id="8eb61-112">Visual Studio 2008 SP1 上的 ASP.NET MVC 1.0 升级向导</span><span class="sxs-lookup"><span data-stu-id="8eb61-112">Upgrade Wizard for ASP.NET MVC 1.0 on Visual Studio 2008 SP1</span></span>

<span data-ttu-id="8eb61-113">若要将 ASP.NET MVC 1.0 应用程序升级到 Visual Studio 2008 SP1 中的 ASP.NET MVC 2，请使用（不支持的） MvcAppConverter 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8eb61-113">To upgrade an ASP.NET MVC 1.0 application to ASP.NET MVC 2 in Visual Studio 2008 SP1, use the (unsupported) MvcAppConverter application.</span></span> <span data-ttu-id="8eb61-114">可以从以下 URL 下载此应用程序：</span><span class="sxs-lookup"><span data-stu-id="8eb61-114">You can download this application from the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a><span data-ttu-id="8eb61-115">手动升级 ASP.NET MVC 1.0 项目</span><span class="sxs-lookup"><span data-stu-id="8eb61-115">Manually Upgrading an ASP.NET MVC 1.0 Project</span></span>

<span data-ttu-id="8eb61-116">若要手动将现有 ASP.NET MVC 1.0 应用程序升级到版本2，请遵循以下步骤：</span><span class="sxs-lookup"><span data-stu-id="8eb61-116">To manually upgrade an existing ASP.NET MVC 1.0 application to version 2, follow these steps:</span></span>

1. <span data-ttu-id="8eb61-117">备份现有项目。</span><span class="sxs-lookup"><span data-stu-id="8eb61-117">Make a backup of the existing project.</span></span>
2. <span data-ttu-id="8eb61-118">在文本编辑器中，打开项目文件（扩展名为 .csproj 或 .vbproj 的文件），并查找 ProjectTypeGuid 元素。</span><span class="sxs-lookup"><span data-stu-id="8eb61-118">In a text editor, open the project file (the file with the .csproj or .vbproj file extension) and find the ProjectTypeGuid element.</span></span> <span data-ttu-id="8eb61-119">作为该元素的值，将 GUID {603c0e0b-db56-11dc-be95-000d561079b0} 替换为 {F85E285D-A4E0-4152-9332-AB1D724D3325}。</span><span class="sxs-lookup"><span data-stu-id="8eb61-119">As the value of that element, replace the GUID {603c0e0b-db56-11dc-be95-000d561079b0} with {F85E285D-A4E0-4152-9332-AB1D724D3325}.</span></span> <span data-ttu-id="8eb61-120">完成后，该元素的值应如下所示：</span><span class="sxs-lookup"><span data-stu-id="8eb61-120">When you are done, the value of that element should be as follows:</span></span> 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. <span data-ttu-id="8eb61-121">在 Web 应用程序根文件夹中，编辑 web.config 文件。</span><span class="sxs-lookup"><span data-stu-id="8eb61-121">In the Web application root folder, edit the Web.config file.</span></span> <span data-ttu-id="8eb61-122">搜索 System.web，Version = 1.0.0.0，并将所有实例替换为 System.web，Version = 2.0.0.0。</span><span class="sxs-lookup"><span data-stu-id="8eb61-122">Search for System.Web.Mvc, Version=1.0.0.0 and replace all instances with System.Web.Mvc, Version=2.0.0.0.</span></span>
4. <span data-ttu-id="8eb61-123">对位于 Views 文件夹中的 Web.config 文件重复上一步。</span><span class="sxs-lookup"><span data-stu-id="8eb61-123">Repeat the previous step for the Web.config file located in the Views folder.</span></span>
5. <span data-ttu-id="8eb61-124">使用 Visual Studio 打开项目，并在**解决方案资源管理器**中展开 "**引用**" 节点。</span><span class="sxs-lookup"><span data-stu-id="8eb61-124">Open the project using Visual Studio, and in **Solution Explorer**, expand the **References** node.</span></span> <span data-ttu-id="8eb61-125">删除对 System.web （指向版本1.0 程序集）的引用。</span><span class="sxs-lookup"><span data-stu-id="8eb61-125">Delete the reference to System.Web.Mvc (which points to the version 1.0 assembly).</span></span> <span data-ttu-id="8eb61-126">添加对 System.web （v 2.0.0.0）的引用。</span><span class="sxs-lookup"><span data-stu-id="8eb61-126">Add a reference to System.Web.Mvc (v2.0.0.0).</span></span>
6. <span data-ttu-id="8eb61-127">将以下 bindingRedirect 元素添加到配置部分下的应用程序根目录中的 web.config 文件：</span><span class="sxs-lookup"><span data-stu-id="8eb61-127">Add the following bindingRedirect element to the Web.config file in the application root under the configuraton section:</span></span>   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. <span data-ttu-id="8eb61-128">创建新的空 ASP.NET MVC 2 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8eb61-128">Create a new empty ASP.NET MVC 2 application.</span></span> <span data-ttu-id="8eb61-129">将新应用程序的 "脚本" 文件夹中的文件复制到现有应用程序的 "脚本" 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="8eb61-129">Copy the files from the Scripts folder of the new application into the Scripts folder of the existing application.</span></span>
8. <span data-ttu-id="8eb61-130">在应用程序文件中用 CSS 样式定义更新现有的€™ s CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="8eb61-130">Update the existing applicationâ€™s CSS file with the CSS style definitions in the Site.css file.</span></span>
9. <span data-ttu-id="8eb61-131">编译并运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="8eb61-131">Compile the application and run it.</span></span> <span data-ttu-id="8eb61-132">如果出现任何错误，请参阅[ASP.NET MVC 2 的新增功能页中](https://go.microsoft.com/fwlink/?LinkID=185038)的 "重大更改" 部分。</span><span class="sxs-lookup"><span data-stu-id="8eb61-132">If any errors occur, refer to the Breaking Changes section of the [What's New in ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) page.</span></span>
