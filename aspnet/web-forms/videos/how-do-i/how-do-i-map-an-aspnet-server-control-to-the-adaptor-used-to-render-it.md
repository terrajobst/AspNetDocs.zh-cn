---
uid: web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
title: '[如何实现：]将 ASP.NET 服务器控件映射到用于呈现该控件的适配器 |Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素将演示如何使用控制适配器为 ASP.NET 服务器控件提供不同的呈现，而无需实际更改 c 。
ms.author: riande
ms.date: 06/19/2008
ms.assetid: d4b498ef-8e1c-4fa2-9c35-1f32f20bb9b7
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it
msc.type: video
ms.openlocfilehash: 757c90fac3345b448513fb4c7cd946a3d10f3f89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78473420"
---
# <a name="how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it"></a><span data-ttu-id="e8cf0-103">[如何实现：]将 ASP.NET 服务器控件映射到用于呈现该控件的适配器</span><span class="sxs-lookup"><span data-stu-id="e8cf0-103">[How Do I:] Map an ASP.NET Server Control to the Adaptor Used to Render It</span></span>

<span data-ttu-id="e8cf0-104">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="e8cf0-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="e8cf0-105">在此视频中，Chris 像素将演示如何使用控制适配器为 ASP.NET 服务器控件提供不同的呈现，而无需实际更改控件本身。</span><span class="sxs-lookup"><span data-stu-id="e8cf0-105">In this video Chris Pels will show how to use a control adaptor to provide different renderings for an ASP.NET server control without actually changing the control itself.</span></span> <span data-ttu-id="e8cf0-106">在此视频中，ASP.NET BulletList 控件将改编为使用 DIV 元素（而不是传统的 UL 元素）以水平方式显示每个列表项。</span><span class="sxs-lookup"><span data-stu-id="e8cf0-106">In this video, an ASP.NET BulletList control will be adapted to display each list item horizontally using DIV elements instead of the traditional UL elements.</span></span> <span data-ttu-id="e8cf0-107">首先，请参阅如何创建继承 WebControlAdaptor 的类，然后实现代码以呈现新的列表格式。</span><span class="sxs-lookup"><span data-stu-id="e8cf0-107">First, see how to create a class that inherits WebControlAdaptor and then implements the code to render the new list format.</span></span> <span data-ttu-id="e8cf0-108">接下来，了解如何将新的控件适配器映射到 .browser 定义文件中的 ASP.NET 服务器控件。</span><span class="sxs-lookup"><span data-stu-id="e8cf0-108">Next, learn how to map the new control adaptor to the ASP.NET server control in the .browser definition file.</span></span> <span data-ttu-id="e8cf0-109">然后，请参阅如何在网站中的页面上使用新控制适配器。</span><span class="sxs-lookup"><span data-stu-id="e8cf0-109">Then see how to use the new control adaptor on pages in a web site.</span></span> <span data-ttu-id="e8cf0-110">最后，了解如何将控件适配器与所有浏览器或特定类型的浏览器相关联。</span><span class="sxs-lookup"><span data-stu-id="e8cf0-110">Finally, learn how a control adaptor can be associated with either all browsers or specific types of browsers.</span></span>

[<span data-ttu-id="e8cf0-111">&#9654;观看视频（23分钟）</span><span class="sxs-lookup"><span data-stu-id="e8cf0-111">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-map-an-aspnet-server-control-to-the-adaptor-used-to-render-it)
