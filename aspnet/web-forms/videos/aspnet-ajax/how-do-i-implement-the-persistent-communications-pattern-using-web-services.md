---
uid: web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
title: '[如何实现：]使用 Web 服务实现持久通信模式？ | Microsoft Docs'
author: JoeStagner
description: 在传统的网站中，浏览器和服务器不保持正在进行的通信，而只是为了响应执行 act 。
ms.author: riande
ms.date: 08/22/2007
ms.assetid: 424c06cd-6d61-43cd-a1f2-d1a6b62e47b1
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-using-web-services
msc.type: video
ms.openlocfilehash: de2eb281cd4bab46635af480ac2e8f07f60f1591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510212"
---
# <a name="how-do-i-implement-the-persistent-communications-pattern-using-web-services"></a><span data-ttu-id="3a40a-104">[如何实现：]使用 Web 服务实现持久通信模式？</span><span class="sxs-lookup"><span data-stu-id="3a40a-104">[How Do I:] Implement the Persistent Communications Pattern using Web Services?</span></span>

<span data-ttu-id="3a40a-105">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="3a40a-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="3a40a-106">在传统网站中，浏览器和服务器不保持持续的通信，而只是为了响应执行操作的用户。</span><span class="sxs-lookup"><span data-stu-id="3a40a-106">In a traditional Web site the browser and the server do not maintain an ongoing communication, but communicate only in response to the user performing an action.</span></span> <span data-ttu-id="3a40a-107">在页面成为应用程序容器的新式网站中，浏览器和服务器保持正在进行的通信很有利，这样，无需用户执行操作，即可进行页面更新。</span><span class="sxs-lookup"><span data-stu-id="3a40a-107">In a modern Web site where the page becomes an application container, it can be advantageous for the browser and the server to maintain an ongoing communication so that page updates can occur without the user performing an action.</span></span> <span data-ttu-id="3a40a-108">这称为 AJAX 的持久通信模式。</span><span class="sxs-lookup"><span data-stu-id="3a40a-108">This is known as the Persistent Communications Pattern for AJAX.</span></span> <span data-ttu-id="3a40a-109">ASP.NET AJAX 为 Web 开发人员提供了两种主要方式来实现持久通信模式。</span><span class="sxs-lookup"><span data-stu-id="3a40a-109">ASP.NET AJAX provides two main ways for Web developers to implement the Persistent Communications Pattern.</span></span> <span data-ttu-id="3a40a-110">在前面的视频中，我们看到了如何使用 ASP.NET AJAX UpdatePanel 作为实现的基础。</span><span class="sxs-lookup"><span data-stu-id="3a40a-110">In an earlier video we saw how to use the ASP.NET AJAX UpdatePanel as the basis of the implementation.</span></span> <span data-ttu-id="3a40a-111">在此视频中，我们将了解如何使用对 Web 服务的 JavaScrpt 调用来实现同一模式，这不再需要 ASP.NET AJAX UpdatePanel。</span><span class="sxs-lookup"><span data-stu-id="3a40a-111">In this video we learn how to implement the same pattern using a JavaScrpt call to a Web service, which removes the need for an ASP.NET AJAX UpdatePanel.</span></span>

[<span data-ttu-id="3a40a-112">&#9654;观看视频（16分钟）</span><span class="sxs-lookup"><span data-stu-id="3a40a-112">&#9654; Watch video (16 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-the-persistent-communications-pattern-using-web-services)

> [!div class="step-by-step"]
> <span data-ttu-id="3a40a-113">[上一页](how-do-i-localize-an-aspnet-ajax-application.md)
> [下一页](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span><span class="sxs-lookup"><span data-stu-id="3a40a-113">[Previous](how-do-i-localize-an-aspnet-ajax-application.md)
[Next](how-do-i-trigger-an-updatepanel-refresh-from-a-dropdownlist-control.md)</span></span>
