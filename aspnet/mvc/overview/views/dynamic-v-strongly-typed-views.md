---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 动态类型化视图与 强类型视图 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3e81c6381b1e280e3b74cb7eb6ea6e6c3224e655
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455636"
---
# <a name="dynamic-v-strongly-typed-views"></a><span data-ttu-id="f1362-103">动态类型化视图与</span><span class="sxs-lookup"><span data-stu-id="f1362-103">Dynamic v.</span></span> <span data-ttu-id="f1362-104">强类型化视图</span><span class="sxs-lookup"><span data-stu-id="f1362-104">Strongly Typed Views</span></span>

<span data-ttu-id="f1362-105">作者： [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f1362-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="f1362-106">有三种方法可以将信息从控制器传递到 ASP.NET MVC 3 中的视图：</span><span class="sxs-lookup"><span data-stu-id="f1362-106">There are three ways to pass information from a controller to a view in ASP.NET MVC 3:</span></span>

1. <span data-ttu-id="f1362-107">作为强类型化模型对象。</span><span class="sxs-lookup"><span data-stu-id="f1362-107">As a strongly typed model object.</span></span>
2. <span data-ttu-id="f1362-108">为动态类型（使用 @model dynamic）</span><span class="sxs-lookup"><span data-stu-id="f1362-108">As a dynamic type (using @model dynamic)</span></span>
3. <span data-ttu-id="f1362-109">使用 ViewBag</span><span class="sxs-lookup"><span data-stu-id="f1362-109">Using the ViewBag</span></span>

<span data-ttu-id="f1362-110">我编写了一个简单的 MVC 3 顶级博客应用程序，用于比较和对比动态和强类型化的视图。</span><span class="sxs-lookup"><span data-stu-id="f1362-110">I've written a simple MVC 3 Top Blog application to compare and contrast dynamic and strongly typed views.</span></span> <span data-ttu-id="f1362-111">该控制器首先提供博客的简单列表：</span><span class="sxs-lookup"><span data-stu-id="f1362-111">The controller starts out with a simple list of blogs:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

<span data-ttu-id="f1362-112">右键单击 "IndexNotStonglyTyped" （）方法并添加 "Razor" 视图。</span><span class="sxs-lookup"><span data-stu-id="f1362-112">Right click in the IndexNotStonglyTyped() method and add a Razor view.</span></span>

<span data-ttu-id="f1362-113">[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="f1362-113">[![8475.NotStronglyTypedView[1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)</span></span>

<span data-ttu-id="f1362-114">请确保未选中 "**创建强类型视图**" 框。</span><span class="sxs-lookup"><span data-stu-id="f1362-114">Make sure the **Create a strongly-typed view** box is not checked.</span></span> <span data-ttu-id="f1362-115">生成的视图不包含太多内容：</span><span class="sxs-lookup"><span data-stu-id="f1362-115">The resulting view doesn't contain much:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

<span data-ttu-id="f1362-116">由于我们使用的是动态而不是强类型视图，intellisense 不能帮助我们。</span><span class="sxs-lookup"><span data-stu-id="f1362-116">Because we're using a dynamic and not a strongly typed view, intellisense doesn't help us.</span></span> <span data-ttu-id="f1362-117">完成的代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="f1362-117">The completed code is shown below:</span></span>

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

<span data-ttu-id="f1362-118">[![6646 NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="f1362-118">[![6646.NotStronglyTypedView_5F00_IE[1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)</span></span>

<span data-ttu-id="f1362-119">现在，我们将添加一个强类型视图。</span><span class="sxs-lookup"><span data-stu-id="f1362-119">Now we'll add a strongly typed view.</span></span> <span data-ttu-id="f1362-120">将以下代码添加到控制器：</span><span class="sxs-lookup"><span data-stu-id="f1362-120">Add the following code to the controller:</span></span>

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

<span data-ttu-id="f1362-121">请注意，它的返回视图（topBlogs）完全相同;作为非强类型视图调用。</span><span class="sxs-lookup"><span data-stu-id="f1362-121">Notice it's exactly the same return View(topBlogs); call as the non-strongly typed view.</span></span> <span data-ttu-id="f1362-122">在*StonglyTypedIndex （）* 中右键单击，然后选择 "**添加视图**"。</span><span class="sxs-lookup"><span data-stu-id="f1362-122">Right click inside of *StonglyTypedIndex()* and select **Add View**.</span></span> <span data-ttu-id="f1362-123">这次选择 "**博客**模型类"，然后选择 "**列表**" 作为基架模板。</span><span class="sxs-lookup"><span data-stu-id="f1362-123">This time select the **Blog** Model class and select **List** as the Scaffold template.</span></span>

<span data-ttu-id="f1362-124">[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="f1362-124">[![5658.StrongView[1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)</span></span>

<span data-ttu-id="f1362-125">在新的视图模板中，我们获得 intellisense 支持。</span><span class="sxs-lookup"><span data-stu-id="f1362-125">Inside the new view template we get intellisense support.</span></span>

<span data-ttu-id="f1362-126">[![7002 [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="f1362-126">[![7002.IntelliSense[1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)</span></span>

<span data-ttu-id="f1362-127">可在[此处](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)下载 c # 项目。</span><span class="sxs-lookup"><span data-stu-id="f1362-127">The c# project can be downloaded [here](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip).</span></span>
