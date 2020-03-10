---
uid: web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
title: '[如何实现：]在 AJAX 页面更新的方法之间进行选择吗？ | Microsoft Docs'
author: JoeStagner
description: 在此视频中，Stagner 比较了两种主要方法，即在 ASP.NET 应用程序中执行 AJAX 样式的页面更新。 第一种方法是使用 Upd 。
ms.author: riande
ms.date: 07/09/2007
ms.assetid: a5e33a7d-ccb2-483f-a955-3d39f72ba4ec
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
msc.type: video
ms.openlocfilehash: 56e3ebfbe0b5af4234791136725de79e38171cc1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78420152"
---
# <a name="how-do-i-choose-between-methods-of-ajax-page-updates"></a><span data-ttu-id="f4025-105">[如何实现：]在 AJAX 页面更新的方法之间进行选择吗？</span><span class="sxs-lookup"><span data-stu-id="f4025-105">[How Do I:] Choose Between Methods of AJAX Page Updates?</span></span>

<span data-ttu-id="f4025-106">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="f4025-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="f4025-107">在此视频中，Stagner 比较了两种主要方法，即在 ASP.NET 应用程序中执行 AJAX 样式的页面更新。</span><span class="sxs-lookup"><span data-stu-id="f4025-107">In this video Joe Stagner compares the two primary methods of performing AJAX-style page updates in an ASP.NET application.</span></span> <span data-ttu-id="f4025-108">第一种方法是使用 UpdatePanel，无需在客户端或服务器端编写其他代码。</span><span class="sxs-lookup"><span data-stu-id="f4025-108">The first method is to use an UpdatePanel, where no additional code needs to be written on either the client side or the server side.</span></span> <span data-ttu-id="f4025-109">使用 UpdatePanel 的好处是一切都能自动运行。</span><span class="sxs-lookup"><span data-stu-id="f4025-109">The benefit of using the UpdatePanel is that everything works automatically.</span></span> <span data-ttu-id="f4025-110">损失是，在客户端上，它要求在 AJAX 请求和响应中包含大量数据，并在服务器上需要执行完整的页生命周期。</span><span class="sxs-lookup"><span data-stu-id="f4025-110">The penalty is that at the client it requires a lot of data to be included in the AJAX request and response, and at the server it requires a full page lifecycle to be executed.</span></span> <span data-ttu-id="f4025-111">第二种方法是使用网络回调，需要在客户端和服务器端同时编写附加代码。</span><span class="sxs-lookup"><span data-stu-id="f4025-111">The second method is to use network callbacks, where additional code needs to be written on both the client side and the server side.</span></span> <span data-ttu-id="f4025-112">使用网络回调的好处是，在客户端上，它要求在 AJAX 请求和响应中包含非常少的数据，并且在服务器上只需要执行调用的服务方法。</span><span class="sxs-lookup"><span data-stu-id="f4025-112">The benefit of using network callbacks is that at the client it requires very little data to be included in the AJAX request and response, and at the server it requires only the called service method to be executed.</span></span> <span data-ttu-id="f4025-113">Penality 是编写所需代码所需的时间和精力。</span><span class="sxs-lookup"><span data-stu-id="f4025-113">The penality is the time and effort it takes to write the necessary code.</span></span> <span data-ttu-id="f4025-114">Joe 通过讨论在 AJAX 样式的页面更新的两个主要方法之间进行选择时应考虑的内容来结束视频。</span><span class="sxs-lookup"><span data-stu-id="f4025-114">Joe concludes the video by discussing what you should consider when choosing between the two primary methods of AJAX-style page updates.</span></span> <span data-ttu-id="f4025-115">（此视频使用[如何开始使用 ASP.NET ajax](how-do-i-get-started-with-aspnet-ajax.md)视频，以及[如何使用 ASP.NET Ajax 视频进行客户端网络回调](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md)。）</span><span class="sxs-lookup"><span data-stu-id="f4025-115">(This video uses the code from the [How Do I Get Started with ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) video and the [How Do I Make Client-Side Network Callbacks with ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) video.)</span></span>

[<span data-ttu-id="f4025-116">&#9654;观看视频（11分钟）</span><span class="sxs-lookup"><span data-stu-id="f4025-116">&#9654; Watch video (11 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-choose-between-methods-of-ajax-page-updates)

> [!div class="step-by-step"]
> <span data-ttu-id="f4025-117">[上一页](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
> [下一页](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span><span class="sxs-lookup"><span data-stu-id="f4025-117">[Previous](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
[Next](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span></span>
