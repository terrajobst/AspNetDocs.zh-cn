---
uid: web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
title: '[如何实现：]使用 UpdatePanel 的条件 UpdateMode？ | Microsoft Docs'
author: JoeStagner
description: ASP.NET AJAX UpdatePanel 包含一个 UpdateMode 属性，该属性可以设置为 "Always" 或 "条件"。 默认值始终为，在这种情况下，UpdatePan
ms.author: riande
ms.date: 08/01/2007
ms.assetid: 10b5bad3-4c18-464f-9454-0b3e60b7b8be
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-use-the-conditional-updatemode-of-the-updatepanel
msc.type: video
ms.openlocfilehash: c05d4f262d56dfba858443b830d72ff0520b65d7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510122"
---
# <a name="how-do-i-use-the-conditional-updatemode-of-the-updatepanel"></a><span data-ttu-id="28d5a-105">[如何实现：]使用 UpdatePanel 的条件 UpdateMode？</span><span class="sxs-lookup"><span data-stu-id="28d5a-105">[How Do I:] Use the Conditional UpdateMode of the UpdatePanel?</span></span>

<span data-ttu-id="28d5a-106">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="28d5a-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="28d5a-107">ASP.NET AJAX UpdatePanel 包含一个 UpdateMode 属性，该属性可以设置为 "Always" 或 "条件"。</span><span class="sxs-lookup"><span data-stu-id="28d5a-107">The ASP.NET AJAX UpdatePanel includes an UpdateMode property that may be set to 'Always' or 'Conditional'.</span></span> <span data-ttu-id="28d5a-108">默认值始终为，在这种情况下，UpdatePanel 将始终在异步回发过程中更新其内容。</span><span class="sxs-lookup"><span data-stu-id="28d5a-108">The default is Always, in which case the UpdatePanel will always update its content during an asynchronous postback.</span></span> <span data-ttu-id="28d5a-109">在此视频中，我们将了解如何将 UpdateMode 设置为条件，在这种情况下，当服务器端代码调用其更新方法时，UpdatePanel 将仅更新其内容。</span><span class="sxs-lookup"><span data-stu-id="28d5a-109">In this video we learn how we can set the UpdateMode to Conditional, in which case the UpdatePanel will only update its content when our server-side code calls its Update method.</span></span> <span data-ttu-id="28d5a-110">这允许您在C#或 Visual Basic 代码中使用条件逻辑来确定 UpdatePanel 是否会在当前异步回发过程中更新其内容。</span><span class="sxs-lookup"><span data-stu-id="28d5a-110">This allows you to use conditional logic in your C# or Visual Basic code to determine whether the UpdatePanel will update its content during the current asynchronous postback.</span></span>

[<span data-ttu-id="28d5a-111">&#9654;观看视频（13分钟）</span><span class="sxs-lookup"><span data-stu-id="28d5a-111">&#9654; Watch video (13 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-use-the-conditional-updatemode-of-the-updatepanel)

> [!div class="step-by-step"]
> <span data-ttu-id="28d5a-112">[上一页](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
> [下一页](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span><span class="sxs-lookup"><span data-stu-id="28d5a-112">[Previous](how-do-i-determine-whether-an-asynchronous-postback-has-occurred.md)
[Next](how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel.md)</span></span>
