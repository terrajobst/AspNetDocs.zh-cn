---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
title: 从服务器端修改动画（C#） |Microsoft Docs
author: wenz
description: ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。 动画还可能 。
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b0abec39-a1c9-422d-ba9a-ef16f6185af8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-cs
msc.type: authoredcontent
ms.openlocfilehash: 0594efea9598a6c2461a72f789b5bd5f8ece23da
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575178"
---
# <a name="modifying-animations-from-the-server-side-c"></a><span data-ttu-id="5d20f-104">从服务器端修改动画（C#）</span><span class="sxs-lookup"><span data-stu-id="5d20f-104">Modifying Animations From The Server Side (C#)</span></span>

<span data-ttu-id="5d20f-105">作者： [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="5d20f-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="5d20f-106">[下载代码](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip)或[下载 PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="5d20f-106">[Download Code](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.cs.zip) or [Download PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9CS.pdf)</span></span>

> <span data-ttu-id="5d20f-107">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="5d20f-107">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5d20f-108">动画还可以在服务器端进行更改</span><span class="sxs-lookup"><span data-stu-id="5d20f-108">The animations may also be changed on the server-side</span></span>

## <a name="overview"></a><span data-ttu-id="5d20f-109">概述</span><span class="sxs-lookup"><span data-stu-id="5d20f-109">Overview</span></span>

<span data-ttu-id="5d20f-110">ASP.NET AJAX 控件工具包中的动画控件不仅仅是一个控件，而是用于向控件添加动画的整个框架。</span><span class="sxs-lookup"><span data-stu-id="5d20f-110">The Animation control in the ASP.NET AJAX Control Toolkit is not just a control but a whole framework to add animations to a control.</span></span> <span data-ttu-id="5d20f-111">动画还可以在服务器端进行更改</span><span class="sxs-lookup"><span data-stu-id="5d20f-111">The animations may also be changed on the server-side</span></span>

## <a name="steps"></a><span data-ttu-id="5d20f-112">步骤</span><span class="sxs-lookup"><span data-stu-id="5d20f-112">Steps</span></span>

<span data-ttu-id="5d20f-113">首先，将 `ScriptManager` 包括在页面中;然后，加载 ASP.NET AJAX 库，使其可以使用控件工具包：</span><span class="sxs-lookup"><span data-stu-id="5d20f-113">First of all, include the `ScriptManager` in the page; then, the ASP.NET AJAX library is loaded, making it possible to use the Control Toolkit:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample1.aspx)]

<span data-ttu-id="5d20f-114">动画将应用于文本面板，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5d20f-114">The animation will be applied to a panel of text which looks like this:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample2.aspx)]

<span data-ttu-id="5d20f-115">在面板的关联 CSS 类中，定义良好的背景色，并为面板设置固定宽度：</span><span class="sxs-lookup"><span data-stu-id="5d20f-115">In the associated CSS class for the panel, define a nice background color and also set a fixed width for the panel:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample3.css)]

<span data-ttu-id="5d20f-116">其余代码在服务器端运行，不使用标记;相反，它使用代码创建 `AnimationExtender` 控件：</span><span class="sxs-lookup"><span data-stu-id="5d20f-116">The rest of the code runs on the server-side and does not use markup; instead, it uses code to create the `AnimationExtender` control:</span></span>

[!code-aspx[Main](modifying-animations-from-the-server-side-cs/samples/sample4.aspx)]

<span data-ttu-id="5d20f-117">不过，控件工具包当前不提供用于创建各个动画的 API 访问权限。</span><span class="sxs-lookup"><span data-stu-id="5d20f-117">However, the Control Toolkit currently does not provide an API access to create the individual animations.</span></span> <span data-ttu-id="5d20f-118">不过，可以将 `AnimationExtender`的动画属性设置为包含以声明方式分配动画时使用的 XML 标记的字符串。</span><span class="sxs-lookup"><span data-stu-id="5d20f-118">It is however possible to set the `AnimationExtender`'s Animations property to a string containing the XML markup used when assigning the animations declaratively.</span></span> <span data-ttu-id="5d20f-119">若要创建不能包含 `<Animations>` 元素的 XML，可以使用 .NET Framework 的 XML 支持，如以下代码所示，只需提供字符串：</span><span class="sxs-lookup"><span data-stu-id="5d20f-119">In order to create the XML which must not contain the `<Animations>` element you could use the .NET Framework's XML support or, as in the following code, just provide the string:</span></span>

[!code-css[Main](modifying-animations-from-the-server-side-cs/samples/sample5.css)]

<span data-ttu-id="5d20f-120">最后，将 `AnimationExtender` 控件添加到 `<form runat="server">` 元素中的当前页，确保包含并运行动画：</span><span class="sxs-lookup"><span data-stu-id="5d20f-120">Finally, add the `AnimationExtender` control to the current page, within the `<form runat="server">` element, making sure that the animation is included and runs:</span></span>

[!code-html[Main](modifying-animations-from-the-server-side-cs/samples/sample6.html)]

<span data-ttu-id="5d20f-121">[![使用服务器端C#/VB 代码创建动画](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5d20f-121">[![The animation is created using server-side C#/VB code](modifying-animations-from-the-server-side-cs/_static/image2.png)](modifying-animations-from-the-server-side-cs/_static/image1.png)</span></span>

<span data-ttu-id="5d20f-122">动画是使用服务器端C#/VB 代码创建的（[单击查看完全大小的映像](modifying-animations-from-the-server-side-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="5d20f-122">The animation is created using server-side C#/VB code ([Click to view full-size image](modifying-animations-from-the-server-side-cs/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5d20f-123">[上一页](triggering-an-animation-in-another-control-cs.md)
> [下一页](executing-animations-using-client-side-code-cs.md)</span><span class="sxs-lookup"><span data-stu-id="5d20f-123">[Previous](triggering-an-animation-in-another-control-cs.md)
[Next](executing-animations-using-client-side-code-cs.md)</span></span>
