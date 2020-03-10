---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 第8部分：购物车和 Ajax 更新 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第8部分涵盖了包含 Ajax 更新的购物车。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433514"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a><span data-ttu-id="677f1-104">第8部分：带有 Ajax 更新的购物车</span><span class="sxs-lookup"><span data-stu-id="677f1-104">Part 8: Shopping Cart with Ajax Updates</span></span>

<span data-ttu-id="677f1-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="677f1-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="677f1-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="677f1-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="677f1-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="677f1-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="677f1-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="677f1-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="677f1-109">第8部分涵盖了包含 Ajax 更新的购物车。</span><span class="sxs-lookup"><span data-stu-id="677f1-109">Part 8 covers Shopping Cart with Ajax Updates.</span></span>

<span data-ttu-id="677f1-110">我们将允许用户在购物车中放入唱片集而无需注册，但他们需要注册为来宾才能完成签出。</span><span class="sxs-lookup"><span data-stu-id="677f1-110">We'll allow users to place albums in their cart without registering, but they'll need to register as guests to complete checkout.</span></span> <span data-ttu-id="677f1-111">购物和结帐过程将分为两个控制器：一个 ShoppingCart 控制器，允许匿名向购物车添加项，并使用签出控制器来处理结帐过程。</span><span class="sxs-lookup"><span data-stu-id="677f1-111">The shopping and checkout process will be separated into two controllers: a ShoppingCart Controller which allows anonymously adding items to a cart, and a Checkout Controller which handles the checkout process.</span></span> <span data-ttu-id="677f1-112">我们将从本部分中的购物车开始，然后在下一节中构建结帐过程。</span><span class="sxs-lookup"><span data-stu-id="677f1-112">We'll start with the Shopping Cart in this section, then build the Checkout process in the following section.</span></span>

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a><span data-ttu-id="677f1-113">添加 Cart、Order 和 OrderDetail 模型类</span><span class="sxs-lookup"><span data-stu-id="677f1-113">Adding the Cart, Order, and OrderDetail model classes</span></span>

<span data-ttu-id="677f1-114">购物车和结帐过程将利用一些新的类。</span><span class="sxs-lookup"><span data-stu-id="677f1-114">Our Shopping Cart and Checkout processes will make use of some new classes.</span></span> <span data-ttu-id="677f1-115">右键单击 "模型" 文件夹，然后使用以下代码添加 Cart 类（Cart.cs）。</span><span class="sxs-lookup"><span data-stu-id="677f1-115">Right-click the Models folder and add a Cart class (Cart.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

<span data-ttu-id="677f1-116">此类非常类似于我们目前使用过的其他类，但 RecordId 属性的 [Key] 属性除外。</span><span class="sxs-lookup"><span data-stu-id="677f1-116">This class is pretty similar to others we've used so far, with the exception of the [Key] attribute for the RecordId property.</span></span> <span data-ttu-id="677f1-117">购物车项将具有名为 CartID 的字符串标识符，以允许进行匿名购物，但该表包含名为 RecordId 的整数主键。</span><span class="sxs-lookup"><span data-stu-id="677f1-117">Our Cart items will have a string identifier named CartID to allow anonymous shopping, but the table includes an integer primary key named RecordId.</span></span> <span data-ttu-id="677f1-118">按照约定，实体框架代码优先要求名为 "Cart" 的表的主键为 CartId 或 ID，但我们可以根据需要通过注释或代码轻松覆盖。</span><span class="sxs-lookup"><span data-stu-id="677f1-118">By convention, Entity Framework Code-First expects that the primary key for a table named Cart will be either CartId or ID, but we can easily override that via annotations or code if we want.</span></span> <span data-ttu-id="677f1-119">下面的示例演示了如何在代码中使用简单的约定，在这种情况下，我们不会对其进行实体框架。</span><span class="sxs-lookup"><span data-stu-id="677f1-119">This is an example of how we can use the simple conventions in Entity Framework Code-First when they suit us, but we're not constrained by them when they don't.</span></span>

<span data-ttu-id="677f1-120">接下来，使用以下代码添加订单类（Order.cs）。</span><span class="sxs-lookup"><span data-stu-id="677f1-120">Next, add an Order class (Order.cs) with the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

<span data-ttu-id="677f1-121">此类跟踪订单的摘要和传递信息。</span><span class="sxs-lookup"><span data-stu-id="677f1-121">This class tracks summary and delivery information for an order.</span></span> <span data-ttu-id="677f1-122">**它尚不会进行编译**，因为它有一个 OrderDetails 导航属性，该属性依赖于我们尚未创建的类。</span><span class="sxs-lookup"><span data-stu-id="677f1-122">**It won't compile yet**, because it has an OrderDetails navigation property which depends on a class we haven't created yet.</span></span> <span data-ttu-id="677f1-123">现在，通过添加一个名为 OrderDetail.cs 的类，添加以下代码来解决此问题。</span><span class="sxs-lookup"><span data-stu-id="677f1-123">Let's fix that now by adding a class named OrderDetail.cs, adding the following code.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

<span data-ttu-id="677f1-124">我们将对我们的 MusicStoreEntities 类进行最后一次更新，以包括公开这些新模型类的 Dbset，其中包括 DbSet&lt;艺术家&gt;。</span><span class="sxs-lookup"><span data-stu-id="677f1-124">We'll make one last update to our MusicStoreEntities class to include DbSets which expose those new Model classes, also including a DbSet&lt;Artist&gt;.</span></span> <span data-ttu-id="677f1-125">已更新的 MusicStoreEntities 类显示如下。</span><span class="sxs-lookup"><span data-stu-id="677f1-125">The updated MusicStoreEntities class appears as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="677f1-126">管理购物车业务逻辑</span><span class="sxs-lookup"><span data-stu-id="677f1-126">Managing the Shopping Cart business logic</span></span>

<span data-ttu-id="677f1-127">接下来，我们将在 "模型" 文件夹中创建 ShoppingCart 类。</span><span class="sxs-lookup"><span data-stu-id="677f1-127">Next, we'll create the ShoppingCart class in the Models folder.</span></span> <span data-ttu-id="677f1-128">ShoppingCart 模型处理对 Cart 表的数据访问。</span><span class="sxs-lookup"><span data-stu-id="677f1-128">The ShoppingCart model handles data access to the Cart table.</span></span> <span data-ttu-id="677f1-129">此外，它还将处理用于在购物车中添加和删除项目的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="677f1-129">Additionally, it will handle the business logic to for adding and removing items from the shopping cart.</span></span>

<span data-ttu-id="677f1-130">由于我们不想要求用户只注册某个帐户来向其购物车添加商品，因此，我们会在访问购物车时为用户分配一个临时唯一标识符（使用 GUID 或全局唯一标识符）。</span><span class="sxs-lookup"><span data-stu-id="677f1-130">Since we don't want to require users to sign up for an account just to add items to their shopping cart, we will assign users a temporary unique identifier (using a GUID, or globally unique identifier) when they access the shopping cart.</span></span> <span data-ttu-id="677f1-131">我们将使用 ASP.NET Session 类存储此 ID。</span><span class="sxs-lookup"><span data-stu-id="677f1-131">We'll store this ID using the ASP.NET Session class.</span></span>

<span data-ttu-id="677f1-132">*注意： ASP.NET 会话是存储用户特定信息（在离开站点后过期）的便利位置。虽然会话状态的滥用可能会对较大的站点产生性能影响，但我们的轻型用途非常适合用于演示目的。*</span><span class="sxs-lookup"><span data-stu-id="677f1-132">*Note: The ASP.NET Session is a convenient place to store user-specific information which will expire after they leave the site. While misuse of session state can have performance implications on larger sites, our light use will work well for demonstration purposes.*</span></span>

<span data-ttu-id="677f1-133">ShoppingCart 类公开以下方法：</span><span class="sxs-lookup"><span data-stu-id="677f1-133">The ShoppingCart class exposes the following methods:</span></span>

<span data-ttu-id="677f1-134">**AddToCart**采用唱片集作为参数，并将其添加到用户的购物车。</span><span class="sxs-lookup"><span data-stu-id="677f1-134">**AddToCart** takes an Album as a parameter and adds it to the user's cart.</span></span> <span data-ttu-id="677f1-135">由于 Cart 表跟踪每个唱片集的数量，因此，它包括在需要时创建新行的逻辑，或者只是在用户已订购唱片集的一个副本时增加数量。</span><span class="sxs-lookup"><span data-stu-id="677f1-135">Since the Cart table tracks quantity for each album, it includes logic to create a new row if needed or just increment the quantity if the user has already ordered one copy of the album.</span></span>

<span data-ttu-id="677f1-136">**RemoveFromCart**采用唱片集 ID 并将其从用户购物车中删除。</span><span class="sxs-lookup"><span data-stu-id="677f1-136">**RemoveFromCart** takes an Album ID and removes it from the user's cart.</span></span> <span data-ttu-id="677f1-137">如果用户的购物车中只包含唱片集的一个副本，则删除该行。</span><span class="sxs-lookup"><span data-stu-id="677f1-137">If the user only had one copy of the album in their cart, the row is removed.</span></span>

<span data-ttu-id="677f1-138">**EmptyCart**删除用户购物车中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="677f1-138">**EmptyCart** removes all items from a user's shopping cart.</span></span>

<span data-ttu-id="677f1-139">**GetCartItems**检索用于显示或处理的 CartItems 的列表。</span><span class="sxs-lookup"><span data-stu-id="677f1-139">**GetCartItems** retrieves a list of CartItems for display or processing.</span></span>

<span data-ttu-id="677f1-140">**GetCount**检索用户在其购物车中拥有的唱集总数。</span><span class="sxs-lookup"><span data-stu-id="677f1-140">**GetCount** retrieves a the total number of albums a user has in their shopping cart.</span></span>

<span data-ttu-id="677f1-141">**GetTotal**计算购物车中所有物品的总成本。</span><span class="sxs-lookup"><span data-stu-id="677f1-141">**GetTotal** calculates the total cost of all items in the cart.</span></span>

<span data-ttu-id="677f1-142">在结帐阶段， **CreateOrder**将购物车转换为订单。</span><span class="sxs-lookup"><span data-stu-id="677f1-142">**CreateOrder** converts the shopping cart to an order during the checkout phase.</span></span>

<span data-ttu-id="677f1-143">**GetCart**是一种静态方法，它允许我们的控制器获取购物车对象。</span><span class="sxs-lookup"><span data-stu-id="677f1-143">**GetCart** is a static method which allows our controllers to obtain a cart object.</span></span> <span data-ttu-id="677f1-144">它使用**GetCartId**方法来处理从用户的会话读取 CartId。</span><span class="sxs-lookup"><span data-stu-id="677f1-144">It uses the **GetCartId** method to handle reading the CartId from the user's session.</span></span> <span data-ttu-id="677f1-145">GetCartId 方法需要 HttpContextBase，以便它能够从用户的会话中读取用户的 CartId。</span><span class="sxs-lookup"><span data-stu-id="677f1-145">The GetCartId method requires the HttpContextBase so that it can read the user's CartId from user's session.</span></span>

<span data-ttu-id="677f1-146">下面是完整的**ShoppingCart 类**：</span><span class="sxs-lookup"><span data-stu-id="677f1-146">Here's the complete **ShoppingCart class**:</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a><span data-ttu-id="677f1-147">ViewModels</span><span class="sxs-lookup"><span data-stu-id="677f1-147">ViewModels</span></span>

<span data-ttu-id="677f1-148">购物车控制器需要将一些复杂信息传达给其视图，而不会完全映射到模型对象。</span><span class="sxs-lookup"><span data-stu-id="677f1-148">Our Shopping Cart Controller will need to communicate some complex information to its views which doesn't map cleanly to our Model objects.</span></span> <span data-ttu-id="677f1-149">我们不想修改模型以适合我们的视图;Model 类应代表我们的域，而不是用户界面。</span><span class="sxs-lookup"><span data-stu-id="677f1-149">We don't want to modify our Models to suit our views; Model classes should represent our domain, not the user interface.</span></span> <span data-ttu-id="677f1-150">一种解决方案是使用 ViewBag 类将信息传递到我们的视图，就像我们对商店经理下拉列表信息进行的一样，但通过 ViewBag 传递大量信息变得难以管理。</span><span class="sxs-lookup"><span data-stu-id="677f1-150">One solution would be to pass the information to our Views using the ViewBag class, as we did with the Store Manager dropdown information, but passing a lot of information via ViewBag gets hard to manage.</span></span>

<span data-ttu-id="677f1-151">此方法的解决方案是使用*ViewModel*模式。</span><span class="sxs-lookup"><span data-stu-id="677f1-151">A solution to this is to use the *ViewModel* pattern.</span></span> <span data-ttu-id="677f1-152">使用此模式时，我们将创建针对特定视图方案进行了优化的强类型类，并公开了视图模板所需的动态值/内容的属性。</span><span class="sxs-lookup"><span data-stu-id="677f1-152">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="677f1-153">然后，控制器类可以填充这些视图优化类并将其传递给视图模板以供使用。</span><span class="sxs-lookup"><span data-stu-id="677f1-153">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="677f1-154">这会在视图模板中启用类型安全、编译时检查和编辑器 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="677f1-154">This enables type-safety, compile-time checking, and editor IntelliSense within view templates.</span></span>

<span data-ttu-id="677f1-155">我们将创建两个用于购物车控制器的视图模型： ShoppingCartViewModel 将保存用户购物车的内容，而 ShoppingCartRemoveViewModel 将用于显示用户删除内容时的确认信息购物车。</span><span class="sxs-lookup"><span data-stu-id="677f1-155">We'll create two View Models for use in our Shopping Cart controller: the ShoppingCartViewModel will hold the contents of the user's shopping cart, and the ShoppingCartRemoveViewModel will be used to display confirmation information when a user removes something from their cart.</span></span>

<span data-ttu-id="677f1-156">让我们在项目的根目录中创建一个新的 Viewmodel 文件夹，使其保持井然有序。</span><span class="sxs-lookup"><span data-stu-id="677f1-156">Let's create a new ViewModels folder in the root of our project to keep things organized.</span></span> <span data-ttu-id="677f1-157">右键单击该项目，选择 "添加/新建文件夹"。</span><span class="sxs-lookup"><span data-stu-id="677f1-157">Right-click the project, select Add / New Folder.</span></span>

![](mvc-music-store-part-8/_static/image1.jpg)

<span data-ttu-id="677f1-158">将文件夹命名为 Viewmodel。</span><span class="sxs-lookup"><span data-stu-id="677f1-158">Name the folder ViewModels.</span></span>

![](mvc-music-store-part-8/_static/image1.png)

<span data-ttu-id="677f1-159">接下来，将 ShoppingCartViewModel 类添加到 Viewmodel 文件夹。</span><span class="sxs-lookup"><span data-stu-id="677f1-159">Next, add the ShoppingCartViewModel class in the ViewModels folder.</span></span> <span data-ttu-id="677f1-160">它有两个属性：购物车项列表，以及用于保存购物车中所有物品总价的小数值。</span><span class="sxs-lookup"><span data-stu-id="677f1-160">It has two properties: a list of Cart items, and a decimal value to hold the total price for all items in the cart.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

<span data-ttu-id="677f1-161">现在，请将 ShoppingCartRemoveViewModel 添加到 Viewmodel 文件夹，其中包含以下四个属性。</span><span class="sxs-lookup"><span data-stu-id="677f1-161">Now add the ShoppingCartRemoveViewModel to the ViewModels folder, with the following four properties.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a><span data-ttu-id="677f1-162">购物车控制器</span><span class="sxs-lookup"><span data-stu-id="677f1-162">The Shopping Cart Controller</span></span>

<span data-ttu-id="677f1-163">购物车控制器有三个主要用途：将商品添加到购物车、从购物车中删除物品以及查看购物车中的物品。</span><span class="sxs-lookup"><span data-stu-id="677f1-163">The Shopping Cart controller has three main purposes: adding items to a cart, removing items from the cart, and viewing items in the cart.</span></span> <span data-ttu-id="677f1-164">它将使用我们刚刚创建的三个类： ShoppingCartViewModel、ShoppingCartRemoveViewModel 和 ShoppingCart。</span><span class="sxs-lookup"><span data-stu-id="677f1-164">It will make use of the three classes we just created: ShoppingCartViewModel, ShoppingCartRemoveViewModel, and ShoppingCart.</span></span> <span data-ttu-id="677f1-165">如 StoreController 和 StoreManagerController 中所示，我们将添加一个字段来保存 MusicStoreEntities 的实例。</span><span class="sxs-lookup"><span data-stu-id="677f1-165">As in the StoreController and StoreManagerController, we'll add a field to hold an instance of MusicStoreEntities.</span></span>

<span data-ttu-id="677f1-166">使用空的控制器模板将新的购物车控制器添加到项目。</span><span class="sxs-lookup"><span data-stu-id="677f1-166">Add a new Shopping Cart controller to the project using the Empty controller template.</span></span>

![](mvc-music-store-part-8/_static/image2.png)

<span data-ttu-id="677f1-167">下面是完整的 ShoppingCart 控制器。</span><span class="sxs-lookup"><span data-stu-id="677f1-167">Here's the complete ShoppingCart Controller.</span></span> <span data-ttu-id="677f1-168">索引和添加控制器操作应该非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="677f1-168">The Index and Add Controller actions should look very familiar.</span></span> <span data-ttu-id="677f1-169">"删除" 和 "CartSummary 控制器" 操作处理两种特殊情况，我们将在下一节将对此进行讨论。</span><span class="sxs-lookup"><span data-stu-id="677f1-169">The Remove and CartSummary controller actions handle two special cases, which we'll discuss in the following section.</span></span>

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a><span data-ttu-id="677f1-170">通过 jQuery 进行 Ajax 更新</span><span class="sxs-lookup"><span data-stu-id="677f1-170">Ajax Updates with jQuery</span></span>

<span data-ttu-id="677f1-171">接下来，我们将创建一个强类型化为 ShoppingCartViewModel 的购物车索引页，并使用与以前相同的方法的列表视图模板。</span><span class="sxs-lookup"><span data-stu-id="677f1-171">We'll next create a Shopping Cart Index page that is strongly typed to the ShoppingCartViewModel and uses the List View template using the same method as before.</span></span>

![](mvc-music-store-part-8/_static/image3.png)

<span data-ttu-id="677f1-172">但是，我们将使用 jQuery 为此视图中具有 HTML 类 RemoveLink 的所有链接 "向上绑定" 单击事件，而不是使用 Html.actionlink 从购物车中删除项目。</span><span class="sxs-lookup"><span data-stu-id="677f1-172">However, instead of using an Html.ActionLink to remove items from the cart, we'll use jQuery to "wire up" the click event for all links in this view which have the HTML class RemoveLink.</span></span> <span data-ttu-id="677f1-173">此单击事件处理程序不会发布窗体，而只是对 RemoveFromCart 控制器操作进行 AJAX 回调。</span><span class="sxs-lookup"><span data-stu-id="677f1-173">Rather than posting the form, this click event handler will just make an AJAX callback to our RemoveFromCart controller action.</span></span> <span data-ttu-id="677f1-174">RemoveFromCart 返回 JSON 序列化的结果，我们的 jQuery 回调随后使用 jQuery 分析并执行对页面的四次快速更新：</span><span class="sxs-lookup"><span data-stu-id="677f1-174">The RemoveFromCart returns a JSON serialized result, which our jQuery callback then parses and performs four quick updates to the page using jQuery:</span></span>

- 1. <span data-ttu-id="677f1-175">从列表中删除已删除的唱片集</span><span class="sxs-lookup"><span data-stu-id="677f1-175">Removes the deleted album from the list</span></span>
- 2. <span data-ttu-id="677f1-176">更新页眉中的购物车计数</span><span class="sxs-lookup"><span data-stu-id="677f1-176">Updates the cart count in the header</span></span>
- 3. <span data-ttu-id="677f1-177">向用户显示更新消息</span><span class="sxs-lookup"><span data-stu-id="677f1-177">Displays an update message to the user</span></span>
- 4. <span data-ttu-id="677f1-178">更新购物车总价</span><span class="sxs-lookup"><span data-stu-id="677f1-178">Updates the cart total price</span></span>

<span data-ttu-id="677f1-179">由于删除方案是在索引视图中由 Ajax 回调处理的，因此我们不需要 RemoveFromCart 操作的其他视图。</span><span class="sxs-lookup"><span data-stu-id="677f1-179">Since the remove scenario is being handled by an Ajax callback within the Index view, we don't need an additional view for RemoveFromCart action.</span></span> <span data-ttu-id="677f1-180">下面是/ShoppingCart/Index 视图的完整代码：</span><span class="sxs-lookup"><span data-stu-id="677f1-180">Here is the complete code for the /ShoppingCart/Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

<span data-ttu-id="677f1-181">为了进行测试，我们需要将商品添加到购物车中。</span><span class="sxs-lookup"><span data-stu-id="677f1-181">In order to test this out, we need to be able to add items to our shopping cart.</span></span> <span data-ttu-id="677f1-182">我们将更新**应用商店详细信息**视图，以包含 "添加到购物车" 按钮。</span><span class="sxs-lookup"><span data-stu-id="677f1-182">We'll update our **Store Details** view to include an "Add to cart" button.</span></span> <span data-ttu-id="677f1-183">在此过程中，我们可以包含自上次更新此视图以来添加的某些唱片集附加信息：流派、艺术家、价格和唱片集画面。</span><span class="sxs-lookup"><span data-stu-id="677f1-183">While we're at it, we can include some of the Album additional information which we've added since we last updated this view: Genre, Artist, Price, and Album Art.</span></span> <span data-ttu-id="677f1-184">此时将显示更新的商店详细信息视图代码，如下所示。</span><span class="sxs-lookup"><span data-stu-id="677f1-184">The updated Store Details view code appears as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

<span data-ttu-id="677f1-185">现在，我们可以单击整个商店，并测试在购物车中添加和删除唱片集。</span><span class="sxs-lookup"><span data-stu-id="677f1-185">Now we can click through the store and test adding and removing Albums to and from our shopping cart.</span></span> <span data-ttu-id="677f1-186">运行应用程序并浏览到存储索引。</span><span class="sxs-lookup"><span data-stu-id="677f1-186">Run the application and browse to the Store Index.</span></span>

![](mvc-music-store-part-8/_static/image4.png)

<span data-ttu-id="677f1-187">接下来，单击某一流派以查看唱片集列表。</span><span class="sxs-lookup"><span data-stu-id="677f1-187">Next, click on a Genre to view a list of albums.</span></span>

![](mvc-music-store-part-8/_static/image5.png)

<span data-ttu-id="677f1-188">单击唱片集标题现在将显示更新的 "唱片集详细信息" 视图，包括 "添加到购物车" 按钮。</span><span class="sxs-lookup"><span data-stu-id="677f1-188">Clicking on an Album title now shows our updated Album Details view, including the "Add to cart" button.</span></span>

![](mvc-music-store-part-8/_static/image6.png)

<span data-ttu-id="677f1-189">单击 "添加到购物车" 按钮将显示购物车摘要列表中的购物车索引视图。</span><span class="sxs-lookup"><span data-stu-id="677f1-189">Clicking the "Add to cart" button shows our Shopping Cart Index view with the shopping cart summary list.</span></span>

![](mvc-music-store-part-8/_static/image7.png)

<span data-ttu-id="677f1-190">在加载购物车后，可以单击 "从购物车中删除" 链接，查看购物车的 Ajax 更新。</span><span class="sxs-lookup"><span data-stu-id="677f1-190">After loading up your shopping cart, you can click on the Remove from cart link to see the Ajax update to your shopping cart.</span></span>

![](mvc-music-store-part-8/_static/image8.png)

<span data-ttu-id="677f1-191">我们构建了一个工作购物车，允许未注册的用户将物品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="677f1-191">We've built out a working shopping cart which allows unregistered users to add items to their cart.</span></span> <span data-ttu-id="677f1-192">在下一部分中，我们将允许他们注册并完成签出过程。</span><span class="sxs-lookup"><span data-stu-id="677f1-192">In the following section, we'll allow them to register and complete the checkout process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="677f1-193">[上一页](mvc-music-store-part-7.md)
> [下一页](mvc-music-store-part-9.md)</span><span class="sxs-lookup"><span data-stu-id="677f1-193">[Previous](mvc-music-store-part-7.md)
[Next](mvc-music-store-part-9.md)</span></span>
