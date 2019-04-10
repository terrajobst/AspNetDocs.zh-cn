---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: 创建自定义路由 (VB) |Microsoft Docs
author: microsoft
description: 了解如何将自定义路由添加到 ASP.NET MVC 应用程序。 在本教程中，您将学习如何修改 Global.asax 文件中的默认路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: a7b8b85ba1cf5c18e605eb8114a305272baf41a6
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59404866"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="ac155-104">创建自定义路由 (VB)</span><span class="sxs-lookup"><span data-stu-id="ac155-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="ac155-105">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ac155-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ac155-106">了解如何将自定义路由添加到 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac155-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="ac155-107">在本教程中，您将学习如何修改 Global.asax 文件中的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="ac155-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>


<span data-ttu-id="ac155-108">在本教程中，您将学习如何将自定义的路由添加到 ASP.NET MVC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac155-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="ac155-109">了解如何修改自定义的路由在 Global.asax 文件中的默认路由表。</span><span class="sxs-lookup"><span data-stu-id="ac155-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="ac155-110">在 ASP.NET MVC 应用程序中的默认路由表将就可以正常工作。</span><span class="sxs-lookup"><span data-stu-id="ac155-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="ac155-111">但是，可能会发现有专门的路由的需要。</span><span class="sxs-lookup"><span data-stu-id="ac155-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="ac155-112">在这种情况下，可以创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="ac155-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="ac155-113">例如，假设您要生成的博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="ac155-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="ac155-114">你可能想要处理传入的请求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ac155-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="ac155-115">/ 存档/12-25-2009 年</span><span class="sxs-lookup"><span data-stu-id="ac155-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="ac155-116">当用户输入此请求时，你想要返回到日期相对应的博客条目 2009 年 12 月 25 日。</span><span class="sxs-lookup"><span data-stu-id="ac155-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="ac155-117">若要处理这种类型的请求，需要创建一个自定义路由。</span><span class="sxs-lookup"><span data-stu-id="ac155-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="ac155-118">在列表 1 中的 Global.asax 文件包含一个新的自定义路由，名为博客，看起来像 /Archive/ 哪些句柄请求*条目日期*。</span><span class="sxs-lookup"><span data-stu-id="ac155-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

**<span data-ttu-id="ac155-119">代码清单 1-Global.asax （具有自定义路由）</span><span class="sxs-lookup"><span data-stu-id="ac155-119">Listing 1 - Global.asax (with custom route)</span></span>**

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="ac155-120">您将添加到路由表路由的顺序非常重要。</span><span class="sxs-lookup"><span data-stu-id="ac155-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="ac155-121">我们新的自定义博客路由添加到之前的现有默认路由。</span><span class="sxs-lookup"><span data-stu-id="ac155-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="ac155-122">如果您颠倒顺序，则默认路由始终将获取调用而不是自定义路由。</span><span class="sxs-lookup"><span data-stu-id="ac155-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="ac155-123">自定义博客路由匹配的开头/存档/任何请求。</span><span class="sxs-lookup"><span data-stu-id="ac155-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="ac155-124">因此，它与匹配所有以下 Url:</span><span class="sxs-lookup"><span data-stu-id="ac155-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="ac155-125">/ 存档/12-25-2009 年</span><span class="sxs-lookup"><span data-stu-id="ac155-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="ac155-126">/ 存档/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="ac155-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="ac155-127">/ 存档/apple</span><span class="sxs-lookup"><span data-stu-id="ac155-127">/Archive/apple</span></span>

<span data-ttu-id="ac155-128">自定义的路由将传入请求映射到名为存档的控制器，并调用 Entry() 操作。</span><span class="sxs-lookup"><span data-stu-id="ac155-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="ac155-129">当调用 Entry() 方法时，条目日期在作为一个名为 entryDate 参数传递。</span><span class="sxs-lookup"><span data-stu-id="ac155-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="ac155-130">可以使用在代码清单 2 中的控制器使用博客自定义路由。</span><span class="sxs-lookup"><span data-stu-id="ac155-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

**<span data-ttu-id="ac155-131">代码清单 2-ArchiveController.vb</span><span class="sxs-lookup"><span data-stu-id="ac155-131">Listing 2 - ArchiveController.vb</span></span>**

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="ac155-132">请注意，代码清单 2 中的 Entry() 方法接受类型为 DateTime 的参数。</span><span class="sxs-lookup"><span data-stu-id="ac155-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="ac155-133">MVC 框架非常智能，可自动将条目日期从 URL 转换 DateTime 值。</span><span class="sxs-lookup"><span data-stu-id="ac155-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="ac155-134">如果 URL 中的条目日期参数不能转换为日期时间，将引发错误 （请参阅图 1）。</span><span class="sxs-lookup"><span data-stu-id="ac155-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

**<span data-ttu-id="ac155-135">图 1-通过转换参数错误</span><span class="sxs-lookup"><span data-stu-id="ac155-135">Figure 1 - Error from converting parameter</span></span>**


[![T<span data-ttu-id="ac155-136">他新建项目对话框中]</span><span class="sxs-lookup"><span data-stu-id="ac155-136">he New Project dialog box]</span></span>(creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)

<span data-ttu-id="ac155-137">**图 01**:通过转换参数的错误 ([单击此项可查看原尺寸图像](creating-custom-routes-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="ac155-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>


## <a name="summary"></a><span data-ttu-id="ac155-138">总结</span><span class="sxs-lookup"><span data-stu-id="ac155-138">Summary</span></span>

<span data-ttu-id="ac155-139">本教程的目的是演示如何创建自定义路由。</span><span class="sxs-lookup"><span data-stu-id="ac155-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="ac155-140">您学习了如何将自定义的路由添加到表示博客条目在 Global.asax 文件中的路由表。</span><span class="sxs-lookup"><span data-stu-id="ac155-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="ac155-141">我们讨论了如何将请求的博客条目映射到名为 ArchiveController 的控制器和名为 Entry() 的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="ac155-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ac155-142">[上一页](asp-net-mvc-controller-overview-vb.md)
> [下一页](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="ac155-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
