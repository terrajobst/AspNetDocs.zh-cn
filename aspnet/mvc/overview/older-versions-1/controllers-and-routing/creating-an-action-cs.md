---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: 创建操作（C#） |Microsoft Docs
author: microsoft
description: 了解如何向 ASP.NET MVC 控制器添加新操作。 了解方法为操作的要求。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470198"
---
# <a name="creating-an-action-c"></a><span data-ttu-id="7bc78-104">创建操作 (C#)</span><span class="sxs-lookup"><span data-stu-id="7bc78-104">Creating an Action (C#)</span></span>

<span data-ttu-id="7bc78-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7bc78-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7bc78-106">了解如何向 ASP.NET MVC 控制器添加新操作。</span><span class="sxs-lookup"><span data-stu-id="7bc78-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="7bc78-107">了解方法为操作的要求。</span><span class="sxs-lookup"><span data-stu-id="7bc78-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="7bc78-108">本教程的目的是介绍如何创建新的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="7bc78-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="7bc78-109">了解操作方法的要求。</span><span class="sxs-lookup"><span data-stu-id="7bc78-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="7bc78-110">你还将了解如何防止方法作为操作公开。</span><span class="sxs-lookup"><span data-stu-id="7bc78-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="7bc78-111">将操作添加到控制器</span><span class="sxs-lookup"><span data-stu-id="7bc78-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="7bc78-112">通过向控制器添加新方法，将新操作添加到控制器。</span><span class="sxs-lookup"><span data-stu-id="7bc78-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="7bc78-113">例如，列表1中的控制器包含一个名为 Index （）的操作和一个名为 SayHello （）的操作。</span><span class="sxs-lookup"><span data-stu-id="7bc78-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="7bc78-114">这两种方法都公开为操作。</span><span class="sxs-lookup"><span data-stu-id="7bc78-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="7bc78-115">**列表 1-Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="7bc78-115">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

<span data-ttu-id="7bc78-116">若要以操作的形式公开给 universe，方法必须满足某些要求：</span><span class="sxs-lookup"><span data-stu-id="7bc78-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="7bc78-117">方法必须是公共的。</span><span class="sxs-lookup"><span data-stu-id="7bc78-117">The method must be public.</span></span>
- <span data-ttu-id="7bc78-118">方法不能是静态方法。</span><span class="sxs-lookup"><span data-stu-id="7bc78-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="7bc78-119">方法不能是扩展方法。</span><span class="sxs-lookup"><span data-stu-id="7bc78-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="7bc78-120">方法不能为构造函数、getter 或 setter。</span><span class="sxs-lookup"><span data-stu-id="7bc78-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="7bc78-121">方法不能有开放式泛型类型。</span><span class="sxs-lookup"><span data-stu-id="7bc78-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="7bc78-122">方法不是控制器基类的方法。</span><span class="sxs-lookup"><span data-stu-id="7bc78-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="7bc78-123">方法不能包含**ref**或**out**参数。</span><span class="sxs-lookup"><span data-stu-id="7bc78-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="7bc78-124">请注意，控制器操作的返回类型没有限制。</span><span class="sxs-lookup"><span data-stu-id="7bc78-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="7bc78-125">控制器操作可以返回字符串、DateTime、随机类的实例或 void。</span><span class="sxs-lookup"><span data-stu-id="7bc78-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="7bc78-126">ASP.NET MVC 框架将任何不是操作结果的返回类型转换为字符串，并将该字符串转换为浏览器。</span><span class="sxs-lookup"><span data-stu-id="7bc78-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="7bc78-127">当你向控制器添加不违反这些要求的任何方法时，该方法将作为控制器操作公开。</span><span class="sxs-lookup"><span data-stu-id="7bc78-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="7bc78-128">请注意此处。</span><span class="sxs-lookup"><span data-stu-id="7bc78-128">Be careful here.</span></span> <span data-ttu-id="7bc78-129">连接到 Internet 的任何人都可以调用控制器操作。</span><span class="sxs-lookup"><span data-stu-id="7bc78-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="7bc78-130">请不要这样做，例如，创建 DeleteMyWebsite （）控制器操作。</span><span class="sxs-lookup"><span data-stu-id="7bc78-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="7bc78-131">阻止调用公共方法</span><span class="sxs-lookup"><span data-stu-id="7bc78-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="7bc78-132">如果需要在控制器类中创建一个公共方法，但不希望将该方法作为控制器操作公开，则可以通过使用 [NonAction] 特性来阻止调用此方法。</span><span class="sxs-lookup"><span data-stu-id="7bc78-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the [NonAction] attribute.</span></span> <span data-ttu-id="7bc78-133">例如，清单2中的控制器包含一个名为 CompanySecrets （）的公共方法，该方法用 [NonAction] 特性修饰。</span><span class="sxs-lookup"><span data-stu-id="7bc78-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the [NonAction] attribute.</span></span>

<span data-ttu-id="7bc78-134">**列表 2-Controllers\WorkController.cs**</span><span class="sxs-lookup"><span data-stu-id="7bc78-134">**Listing 2 - Controllers\WorkController.cs**</span></span>

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

<span data-ttu-id="7bc78-135">如果尝试通过在浏览器的地址栏中键入/Work/CompanySecrets 来调用 CompanySecrets （）控制器操作，则将收到图1所示的错误消息。</span><span class="sxs-lookup"><span data-stu-id="7bc78-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="7bc78-136">[调用 NonAction 方法 ![](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="7bc78-136">[![Invoking a NonAction method](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)</span></span>

<span data-ttu-id="7bc78-137">**图 01**：调用 NonAction 方法（[单击以查看完全大小的图像](creating-an-action-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="7bc78-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-cs/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7bc78-138">[上一页](creating-a-controller-cs.md)
> [下一页](asp-net-mvc-routing-overview-vb.md)</span><span class="sxs-lookup"><span data-stu-id="7bc78-138">[Previous](creating-a-controller-cs.md)
[Next](asp-net-mvc-routing-overview-vb.md)</span></span>
