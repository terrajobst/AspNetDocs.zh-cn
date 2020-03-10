---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: 第10部分：导航和站点设计的最终更新，结论 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第10部分涵盖了对导航和的最终更新 。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433610"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a><span data-ttu-id="5247a-104">第10部分：导航和站点设计的最终更新，结论</span><span class="sxs-lookup"><span data-stu-id="5247a-104">Part 10: Final Updates to Navigation and Site Design, Conclusion</span></span>

<span data-ttu-id="5247a-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="5247a-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="5247a-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="5247a-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="5247a-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="5247a-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="5247a-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="5247a-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="5247a-109">第10部分涵盖了对导航和站点设计的最终更新，结论。</span><span class="sxs-lookup"><span data-stu-id="5247a-109">Part 10 covers Final Updates to Navigation and Site Design, Conclusion.</span></span>

<span data-ttu-id="5247a-110">我们已经完成了我们网站的所有主要功能，但仍有一些功能要添加到站点导航、主页和商店浏览页面。</span><span class="sxs-lookup"><span data-stu-id="5247a-110">We've completed all the major functionality for our site, but we still have some features to add to the site navigation, the home page, and the Store Browse page.</span></span>

## <a name="creating-the-shopping-cart-summary-partial-view"></a><span data-ttu-id="5247a-111">创建购物车摘要分部视图</span><span class="sxs-lookup"><span data-stu-id="5247a-111">Creating the Shopping Cart Summary Partial View</span></span>

<span data-ttu-id="5247a-112">我们想要在整个站点中公开用户购物车中的项目数。</span><span class="sxs-lookup"><span data-stu-id="5247a-112">We want to expose the number of items in the user's shopping cart across the entire site.</span></span>

![](mvc-music-store-part-10/_static/image1.png)

<span data-ttu-id="5247a-113">通过创建已添加到我们的站点的分部视图，我们可以轻松地实现此目标。</span><span class="sxs-lookup"><span data-stu-id="5247a-113">We can easily implement this by creating a partial view which is added to our Site.master.</span></span>

<span data-ttu-id="5247a-114">如上所示，ShoppingCart 控制器包括 CartSummary 操作方法，该方法返回分部视图：</span><span class="sxs-lookup"><span data-stu-id="5247a-114">As shown previously, the ShoppingCart controller includes a CartSummary action method which returns a partial view:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

<span data-ttu-id="5247a-115">若要创建 CartSummary 分部视图，请右键单击 Views/ShoppingCart 文件夹，然后选择 "添加视图"。</span><span class="sxs-lookup"><span data-stu-id="5247a-115">To create the CartSummary partial view, right-click on the Views/ShoppingCart folder and select Add View.</span></span> <span data-ttu-id="5247a-116">将视图命名为 CartSummary，并选中 "创建分部视图" 复选框，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5247a-116">Name the view CartSummary and check the "Create a partial view" checkbox as shown below.</span></span>

![](mvc-music-store-part-10/_static/image2.png)

<span data-ttu-id="5247a-117">CartSummary 分部视图非常简单-它只是一个指向 "ShoppingCart" 索引视图的链接，它显示购物车中的项目数。</span><span class="sxs-lookup"><span data-stu-id="5247a-117">The CartSummary partial view is really simple - it's just a link to the ShoppingCart Index view which shows the number of items in the cart.</span></span> <span data-ttu-id="5247a-118">CartSummary 的完整代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="5247a-118">The complete code for CartSummary.cshtml is as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

<span data-ttu-id="5247a-119">通过使用 RenderAction 方法，可以在站点中的任何页面（包括站点主机）中包括分部视图。</span><span class="sxs-lookup"><span data-stu-id="5247a-119">We can include a partial view in any page in the site, including the Site master, by using the Html.RenderAction method.</span></span> <span data-ttu-id="5247a-120">RenderAction 要求我们指定操作名称（"CartSummary"）和控制器名称（"ShoppingCart"），如下所示。</span><span class="sxs-lookup"><span data-stu-id="5247a-120">RenderAction requires us to specify the Action Name ("CartSummary") and the Controller Name ("ShoppingCart") as below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

<span data-ttu-id="5247a-121">在将此项添加到站点布局之前，我们还将创建流派菜单，以便我们可以将我们的所有网站更新一次。</span><span class="sxs-lookup"><span data-stu-id="5247a-121">Before adding this to the site Layout, we will also create the Genre Menu so we can make all of our Site.master updates at one time.</span></span>

## <a name="creating-the-genre-menu-partial-view"></a><span data-ttu-id="5247a-122">创建流派菜单分部视图</span><span class="sxs-lookup"><span data-stu-id="5247a-122">Creating the Genre Menu Partial View</span></span>

<span data-ttu-id="5247a-123">我们可以通过添加流派菜单来更轻松地在应用商店中导航，其中列出了我们的商店中可用的所有流派。</span><span class="sxs-lookup"><span data-stu-id="5247a-123">We can make it a lot easier for our users to navigate through the store by adding a Genre Menu which lists all the Genres available in our store.</span></span>

![](mvc-music-store-part-10/_static/image3.png)

<span data-ttu-id="5247a-124">我们将按照相同的步骤创建 GenreMenu 分部视图，然后可以将它们都添加到站点主节点。</span><span class="sxs-lookup"><span data-stu-id="5247a-124">We will follow the same steps also create a GenreMenu partial view, and then we can add them both to the Site master.</span></span> <span data-ttu-id="5247a-125">首先，将以下 GenreMenu 控制器操作添加到 StoreController：</span><span class="sxs-lookup"><span data-stu-id="5247a-125">First, add the following GenreMenu controller action to the StoreController:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

<span data-ttu-id="5247a-126">此操作返回将由分部视图显示的流派列表，将在下一步创建。</span><span class="sxs-lookup"><span data-stu-id="5247a-126">This action returns a list of Genres which will be displayed by the partial view, which we will create next.</span></span>

<span data-ttu-id="5247a-127">*注意：我们已将 [ChildActionOnly] 属性添加到此控制器操作，这表示只需从分部视图中使用此操作。此属性将阻止通过浏览到/Store/GenreMenu. 来执行控制器操作这并不是部分视图所必需的，但这是一种很好的做法，因为我们希望确保我们的控制器操作按预期方式使用。我们还会返回 PartialView，而不是 View，这让视图引擎知道，它不应使用此视图的布局，因为它将包含在其他视图中。*</span><span class="sxs-lookup"><span data-stu-id="5247a-127">*Note: We have added the [ChildActionOnly] attribute to this controller action, which indicates that we only want this action to be used from a Partial View. This attribute will prevent the controller action from being executed by browsing to /Store/GenreMenu. This isn't required for partial views, but it is a good practice, since we want to make sure our controller actions are used as we intend. We are also returning PartialView rather than View, which lets the view engine know that it shouldn't use the Layout for this view, as it is being included in other views.*</span></span>

<span data-ttu-id="5247a-128">右键单击 "GenreMenu 控制器" 操作，并创建一个名为 GenreMenu 的分部视图，它是使用 "流派视图" 数据类强类型化的，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5247a-128">Right-click on the GenreMenu controller action and create a partial view named GenreMenu which is strongly typed using the Genre view data class as shown below.</span></span>

![](mvc-music-store-part-10/_static/image4.png)

<span data-ttu-id="5247a-129">更新 GenreMenu 分部视图的视图代码，按如下所示使用未排序的列表显示项。</span><span class="sxs-lookup"><span data-stu-id="5247a-129">Update the view code for the GenreMenu partial view to display the items using an unordered list as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a><span data-ttu-id="5247a-130">正在更新站点布局以显示分部视图</span><span class="sxs-lookup"><span data-stu-id="5247a-130">Updating Site Layout to display our Partial Views</span></span>

<span data-ttu-id="5247a-131">可以通过调用 RenderAction （）将分部视图添加到站点布局（/Views/Shared/\_Layout）。</span><span class="sxs-lookup"><span data-stu-id="5247a-131">We can add our partial views to the Site Layout (/Views/Shared/\_Layout.cshtml) by calling Html.RenderAction().</span></span> <span data-ttu-id="5247a-132">我们会将它们添加到中，并添加一些其他标记以显示这些内容，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5247a-132">We'll add them both in, as well as some additional markup to display them, as shown below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

<span data-ttu-id="5247a-133">现在，运行应用程序时，会在左侧导航区域中看到 "流派"，并在顶部看到 "购物车摘要"。</span><span class="sxs-lookup"><span data-stu-id="5247a-133">Now when we run the application, we will see the Genre in the left navigation area and the Cart Summary at the top.</span></span>

## <a name="update-to-the-store-browse-page"></a><span data-ttu-id="5247a-134">更新到存储浏览页</span><span class="sxs-lookup"><span data-stu-id="5247a-134">Update to the Store Browse page</span></span>

<span data-ttu-id="5247a-135">存储浏览页运行正常，但看起来不太好。</span><span class="sxs-lookup"><span data-stu-id="5247a-135">The Store Browse page is functional, but doesn't look very good.</span></span> <span data-ttu-id="5247a-136">通过更新视图代码（在/Views/Store/Browse.cshtml 中找到），我们可以更新页面以更好地布局显示唱片集，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5247a-136">We can update the page to show the albums in a better layout by updating the view code (found in /Views/Store/Browse.cshtml) as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

<span data-ttu-id="5247a-137">这里我们将使用 Url，而不是 Html.actionlink，以便我们可以将特殊格式应用于链接以包含唱片集作品。</span><span class="sxs-lookup"><span data-stu-id="5247a-137">Here we are making use of Url.Action rather than Html.ActionLink so that we can apply special formatting to the link to include the album artwork.</span></span>

<span data-ttu-id="5247a-138">*注意：我们将为这些专辑显示一般的唱片集封面。此信息存储在数据库中，可通过商店管理器进行编辑。欢迎添加自己的图稿。*</span><span class="sxs-lookup"><span data-stu-id="5247a-138">*Note: We are displaying a generic album cover for these albums. This information is stored in the database and is editable via the Store Manager. You are welcome to add your own artwork.*</span></span>

<span data-ttu-id="5247a-139">现在，浏览到某一流派后，会看到包含唱片集图稿的网格中显示的唱片集。</span><span class="sxs-lookup"><span data-stu-id="5247a-139">Now when we browse to a Genre, we will see the albums shown in a grid with the album artwork.</span></span>

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a><span data-ttu-id="5247a-140">更新主页以显示顶级销售专辑</span><span class="sxs-lookup"><span data-stu-id="5247a-140">Updating the Home Page to show Top Selling Albums</span></span>

<span data-ttu-id="5247a-141">我们想要在主页上提供我们最畅销的销售专辑，以增加销售。</span><span class="sxs-lookup"><span data-stu-id="5247a-141">We want to feature our top selling albums on the home page to increase sales.</span></span> <span data-ttu-id="5247a-142">我们将对我们的 HomeController 进行一些更新，以便进行处理，并添加一些其他图形。</span><span class="sxs-lookup"><span data-stu-id="5247a-142">We'll make some updates to our HomeController to handle that, and add in some additional graphics as well.</span></span>

<span data-ttu-id="5247a-143">首先，我们将向唱片集类添加一个导航属性，以便 EntityFramework 知道它们已关联。</span><span class="sxs-lookup"><span data-stu-id="5247a-143">First, we'll add a navigation property to our Album class so that EntityFramework knows that they're associated.</span></span> <span data-ttu-id="5247a-144">我们的**唱片集**类的最后几行现在应如下所示：</span><span class="sxs-lookup"><span data-stu-id="5247a-144">The last few lines of our **Album** class should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

<span data-ttu-id="5247a-145">*注意：这将要求添加 using 语句以引入 System.object 命名空间。*</span><span class="sxs-lookup"><span data-stu-id="5247a-145">*Note: This will require adding a using statement to bring in the System.Collections.Generic namespace.*</span></span>

<span data-ttu-id="5247a-146">首先，我们将使用语句添加 storeDB 字段和 MvcMusicStore，如其他控制器中所述。</span><span class="sxs-lookup"><span data-stu-id="5247a-146">First, we'll add a storeDB field and the MvcMusicStore.Models using statements, as in our other controllers.</span></span> <span data-ttu-id="5247a-147">接下来，我们将以下方法添加到 HomeController，该方法查询数据库以根据 OrderDetails 查找顶级销售唱集。</span><span class="sxs-lookup"><span data-stu-id="5247a-147">Next, we'll add the following method to the HomeController which queries our database to find top selling albums according to OrderDetails.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

<span data-ttu-id="5247a-148">这是一种私有方法，因为我们不希望将其作为控制器操作来使用。</span><span class="sxs-lookup"><span data-stu-id="5247a-148">This is a private method, since we don't want to make it available as a controller action.</span></span> <span data-ttu-id="5247a-149">为了简单起见，我们将它包含在 HomeController 中，但建议你根据需要将业务逻辑移到不同的服务类中。</span><span class="sxs-lookup"><span data-stu-id="5247a-149">We are including it in the HomeController for simplicity, but you are encouraged to move your business logic into separate service classes as appropriate.</span></span>

<span data-ttu-id="5247a-150">接下来，我们可以更新索引控制器操作以查询前5个销售专辑，并将其返回到视图中。</span><span class="sxs-lookup"><span data-stu-id="5247a-150">With that in place, we can update the Index controller action to query the top 5 selling albums and return them to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

<span data-ttu-id="5247a-151">已更新的 HomeController 的完整代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="5247a-151">The complete code for the updated HomeController is as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

<span data-ttu-id="5247a-152">最后，我们需要更新 "主页索引" 视图，使其可以通过更新模型类型并将 "唱片集" 列表添加到底部来显示唱片集列表。</span><span class="sxs-lookup"><span data-stu-id="5247a-152">Finally, we'll need to update our Home Index view so that it can display a list of albums by updating the Model type and adding the album list to the bottom.</span></span> <span data-ttu-id="5247a-153">我们还将利用此机会向页面添加标题和促销部分。</span><span class="sxs-lookup"><span data-stu-id="5247a-153">We will take this opportunity to also add a heading and a promotion section to the page.</span></span>

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

<span data-ttu-id="5247a-154">现在，运行应用程序时，我们将看到更新的主页，其中包含顶级销售专辑和促销消息。</span><span class="sxs-lookup"><span data-stu-id="5247a-154">Now when we run the application, we'll see our updated home page with top selling albums and our promotional message.</span></span>

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a><span data-ttu-id="5247a-155">结束语</span><span class="sxs-lookup"><span data-stu-id="5247a-155">Conclusion</span></span>

<span data-ttu-id="5247a-156">我们已了解到，ASP.NET MVC 使你可以轻松地创建具有数据库访问权限、成员资格、AJAX 等的复杂网站。</span><span class="sxs-lookup"><span data-stu-id="5247a-156">We've seen that ASP.NET MVC makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="5247a-157">速度非常快。</span><span class="sxs-lookup"><span data-stu-id="5247a-157">pretty quickly.</span></span> <span data-ttu-id="5247a-158">希望本教程提供了开始构建自己的 ASP.NET MVC 应用程序所需的工具！</span><span class="sxs-lookup"><span data-stu-id="5247a-158">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET MVC applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="5247a-159">上一页</span><span class="sxs-lookup"><span data-stu-id="5247a-159">Previous</span></span>](mvc-music-store-part-9.md)
