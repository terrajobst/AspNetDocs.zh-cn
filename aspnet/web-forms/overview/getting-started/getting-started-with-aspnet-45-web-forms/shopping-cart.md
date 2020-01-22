---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: 购物车 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: d3b619ebd9448d30857ffbaf17fd245b1d54a662
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519292"
---
# <a name="shopping-cart"></a><span data-ttu-id="5eede-103">购物车</span><span class="sxs-lookup"><span data-stu-id="5eede-103">Shopping Cart</span></span>

<span data-ttu-id="5eede-104">作者： [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="5eede-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="5eede-105">[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="5eede-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="5eede-106">本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。</span><span class="sxs-lookup"><span data-stu-id="5eede-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="5eede-107">此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。</span><span class="sxs-lookup"><span data-stu-id="5eede-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="5eede-108">本教程介绍将购物车添加到 Wingtip 玩具示例 ASP.NET Web 窗体应用程序所需的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="5eede-108">This tutorial describes the business logic required to add a shopping cart to the Wingtip Toys sample ASP.NET Web Forms application.</span></span> <span data-ttu-id="5eede-109">本教程基于前面的 "显示数据项和详细信息" 教程，是 Wingtip 玩具商店教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="5eede-109">This tutorial builds on the previous tutorial "Display Data Items and Details" and is part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="5eede-110">完成本教程后，你的示例应用程序的用户将能够在其购物车中添加、删除和修改产品。</span><span class="sxs-lookup"><span data-stu-id="5eede-110">When you've completed this tutorial, the users of your sample app will be able to add, remove, and modify the products in their shopping cart.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="5eede-111">学习内容：</span><span class="sxs-lookup"><span data-stu-id="5eede-111">What you'll learn:</span></span>

1. <span data-ttu-id="5eede-112">如何为 web 应用程序创建购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-112">How to create a shopping cart for the web application.</span></span>
2. <span data-ttu-id="5eede-113">如何使用户能够将物品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-113">How to enable users to add items to the shopping cart.</span></span>
3. <span data-ttu-id="5eede-114">如何添加[GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction)控件以显示购物车详情。</span><span class="sxs-lookup"><span data-stu-id="5eede-114">How to add a [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction) control to display shopping cart details.</span></span>
4. <span data-ttu-id="5eede-115">如何计算并显示订单总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-115">How to calculate and display the order total.</span></span>
5. <span data-ttu-id="5eede-116">如何删除和更新购物车中的项目。</span><span class="sxs-lookup"><span data-stu-id="5eede-116">How to remove and update items in the shopping cart.</span></span>
6. <span data-ttu-id="5eede-117">如何包含购物车计数器。</span><span class="sxs-lookup"><span data-stu-id="5eede-117">How to include a shopping cart counter.</span></span>

## <a name="code-features-in-this-tutorial"></a><span data-ttu-id="5eede-118">本教程中的代码功能：</span><span class="sxs-lookup"><span data-stu-id="5eede-118">Code features in this tutorial:</span></span>

1. <span data-ttu-id="5eede-119">实体框架 Code First</span><span class="sxs-lookup"><span data-stu-id="5eede-119">Entity Framework Code First</span></span>
2. <span data-ttu-id="5eede-120">数据注释</span><span class="sxs-lookup"><span data-stu-id="5eede-120">Data Annotations</span></span>
3. <span data-ttu-id="5eede-121">强类型化数据控件</span><span class="sxs-lookup"><span data-stu-id="5eede-121">Strongly typed data controls</span></span>
4. <span data-ttu-id="5eede-122">模型绑定</span><span class="sxs-lookup"><span data-stu-id="5eede-122">Model binding</span></span>

## <a name="creating-a-shopping-cart"></a><span data-ttu-id="5eede-123">创建购物车</span><span class="sxs-lookup"><span data-stu-id="5eede-123">Creating a Shopping Cart</span></span>

<span data-ttu-id="5eede-124">在本系列教程的前面部分中，已添加了用于从数据库查看产品数据的页面和代码。</span><span class="sxs-lookup"><span data-stu-id="5eede-124">Earlier in this tutorial series, you added pages and code to view product data from a database.</span></span> <span data-ttu-id="5eede-125">在本教程中，你将创建一个购物车来管理用户感兴趣的产品。</span><span class="sxs-lookup"><span data-stu-id="5eede-125">In this tutorial, you'll create a shopping cart to manage the products that users are interested in buying.</span></span> <span data-ttu-id="5eede-126">即使用户没有注册或登录，用户也能够浏览并向购物车添加商品。</span><span class="sxs-lookup"><span data-stu-id="5eede-126">Users will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="5eede-127">若要管理购物车访问权限，请在用户首次访问购物车时，为用户分配唯一的 `ID`，使用全局唯一标识符（GUID）。</span><span class="sxs-lookup"><span data-stu-id="5eede-127">To manage shopping cart access, you will assign users a unique `ID` using a globally unique identifier (GUID) when the user accesses the shopping cart for the first time.</span></span> <span data-ttu-id="5eede-128">你将使用 ASP.NET 会话状态存储此 `ID`。</span><span class="sxs-lookup"><span data-stu-id="5eede-128">You'll store this `ID` using the ASP.NET Session state.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5eede-129">ASP.NET 会话状态是一个方便的位置，用于存储用户特定的信息，这些信息会在用户离开站点后过期。</span><span class="sxs-lookup"><span data-stu-id="5eede-129">The ASP.NET Session state is a convenient place to store user-specific information which will expire after the user leaves the site.</span></span> <span data-ttu-id="5eede-130">尽管会话状态滥用可能会对较大的站点产生性能影响，但会话状态的使用非常适合用于演示目的。</span><span class="sxs-lookup"><span data-stu-id="5eede-130">While misuse of session state can have performance implications on larger sites, light use of session state works well for demonstration purposes.</span></span> <span data-ttu-id="5eede-131">Wingtip 玩具示例项目演示了如何在没有外部提供程序的情况下使用会话状态，在该提供程序中，会话状态存储在托管站点的 web 服务器上的进程中。</span><span class="sxs-lookup"><span data-stu-id="5eede-131">The Wingtip Toys sample project shows how to use session state without an external provider, where session state is stored in-process on the web server hosting the site.</span></span> <span data-ttu-id="5eede-132">对于提供应用程序的多个实例的大型站点或在不同服务器上运行多个应用程序实例的站点，请考虑使用**Windows Azure Cache Service**。</span><span class="sxs-lookup"><span data-stu-id="5eede-132">For larger sites that provide multiple instances of an application or for sites that run multiple instances of an application on different servers, consider using **Windows Azure Cache Service**.</span></span> <span data-ttu-id="5eede-133">此缓存服务提供网站外部的分布式缓存服务，并解决使用进程内会话状态的问题。</span><span class="sxs-lookup"><span data-stu-id="5eede-133">This Cache Service provides a distributed caching service that is external to the web site and solves the problem of using in-process session state.</span></span> <span data-ttu-id="5eede-134">有关详细信息，请参阅[如何将 ASP.NET 会话状态用于 Microsoft Azure 网站](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider)。</span><span class="sxs-lookup"><span data-stu-id="5eede-134">For more information see, [How to Use ASP.NET Session State with Windows Azure Web Sites](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider).</span></span>

### <a name="add-cartitem-as-a-model-class"></a><span data-ttu-id="5eede-135">将 CartItem 添加为模型类</span><span class="sxs-lookup"><span data-stu-id="5eede-135">Add CartItem as a Model Class</span></span>

<span data-ttu-id="5eede-136">在本系列教程的前面部分，你通过在 "*模型*" 文件夹中创建 `Category` 和 `Product` 类来定义类别和产品数据的架构。</span><span class="sxs-lookup"><span data-stu-id="5eede-136">Earlier in this tutorial series, you defined the schema for the category and product data by creating the `Category` and `Product` classes in the *Models* folder.</span></span> <span data-ttu-id="5eede-137">现在，添加一个新类来定义购物车的架构。</span><span class="sxs-lookup"><span data-stu-id="5eede-137">Now, add a new class to define the schema for the shopping cart.</span></span> <span data-ttu-id="5eede-138">稍后在本教程中，您将添加一个类来处理对 `CartItem` 表的数据访问。</span><span class="sxs-lookup"><span data-stu-id="5eede-138">Later in this tutorial, you will add a class to handle data access to the `CartItem` table.</span></span> <span data-ttu-id="5eede-139">此类将提供业务逻辑，以便添加、删除和更新购物车中的项目。</span><span class="sxs-lookup"><span data-stu-id="5eede-139">This class will provide the business logic to add, remove, and update items in the shopping cart.</span></span>

1. <span data-ttu-id="5eede-140">右键单击 "*模型*" 文件夹，然后选择 "**添加** -&gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-140">Right-click the *Models* folder and select **Add** -&gt; **New Item**.</span></span> 

    ![购物车-新项目](shopping-cart/_static/image1.png)
2. <span data-ttu-id="5eede-142">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="5eede-142">The **Add New Item** dialog box is displayed.</span></span> <span data-ttu-id="5eede-143">选择 "**代码**"，然后选择 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-143">Select **Code**, and then select **Class**.</span></span> 

    ![购物车-"添加新项" 对话框](shopping-cart/_static/image2.png)
3. <span data-ttu-id="5eede-145">将此新类命名为*CartItem.cs*。</span><span class="sxs-lookup"><span data-stu-id="5eede-145">Name this new class *CartItem.cs*.</span></span>
4. <span data-ttu-id="5eede-146">单击“添加”。</span><span class="sxs-lookup"><span data-stu-id="5eede-146">Click **Add**.</span></span>  
   <span data-ttu-id="5eede-147">新的类文件将显示在编辑器中。</span><span class="sxs-lookup"><span data-stu-id="5eede-147">The new class file is displayed in the editor.</span></span>
5. <span data-ttu-id="5eede-148">将默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5eede-148">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

<span data-ttu-id="5eede-149">`CartItem` 类包含将定义用户添加到购物车的每个产品的架构。</span><span class="sxs-lookup"><span data-stu-id="5eede-149">The `CartItem` class contains the schema that will define each product a user adds to the shopping cart.</span></span> <span data-ttu-id="5eede-150">此类类似于在本教程系列中前面创建的其他架构类。</span><span class="sxs-lookup"><span data-stu-id="5eede-150">This class is similar to the other schema classes you created earlier in this tutorial series.</span></span> <span data-ttu-id="5eede-151">按照约定，实体框架 Code First 需要 `CartItem` 表的主键将 `CartItemId` 或 `ID`。</span><span class="sxs-lookup"><span data-stu-id="5eede-151">By convention, Entity Framework Code First expects that the primary key for the `CartItem` table will be either `CartItemId` or `ID`.</span></span> <span data-ttu-id="5eede-152">但是，代码使用数据批注 `[Key]` 特性来重写默认行为。</span><span class="sxs-lookup"><span data-stu-id="5eede-152">However, the code overrides the default behavior by using the data annotation `[Key]` attribute.</span></span> <span data-ttu-id="5eede-153">ItemId 属性的 `Key` 特性指定 `ItemID` 属性为主键。</span><span class="sxs-lookup"><span data-stu-id="5eede-153">The `Key` attribute of the ItemId property specifies that the `ItemID` property is the primary key.</span></span>

<span data-ttu-id="5eede-154">`CartId` 属性指定与要购买的项关联的用户的 `ID`。</span><span class="sxs-lookup"><span data-stu-id="5eede-154">The `CartId` property specifies the `ID` of the user that is associated with the item to purchase.</span></span> <span data-ttu-id="5eede-155">当用户访问购物车时，你将添加代码以创建此用户 `ID`。</span><span class="sxs-lookup"><span data-stu-id="5eede-155">You'll add code to create this user `ID` when the user accesses the shopping cart.</span></span> <span data-ttu-id="5eede-156">此 `ID` 还将存储为 ASP.NET 会话变量。</span><span class="sxs-lookup"><span data-stu-id="5eede-156">This `ID` will also be stored as an ASP.NET Session variable.</span></span>

### <a name="update-the-product-context"></a><span data-ttu-id="5eede-157">更新产品上下文</span><span class="sxs-lookup"><span data-stu-id="5eede-157">Update the Product Context</span></span>

<span data-ttu-id="5eede-158">除了添加 `CartItem` 类之外，您还需要更新管理实体类的数据库上下文类，并提供对数据库的数据访问。</span><span class="sxs-lookup"><span data-stu-id="5eede-158">In addition to adding the `CartItem` class, you will need to update the database context class that manages the entity classes and that provides data access to the database.</span></span> <span data-ttu-id="5eede-159">为此，您需要将新创建的 `CartItem` 模型类添加到 `ProductContext` 类。</span><span class="sxs-lookup"><span data-stu-id="5eede-159">To do this, you will add the newly created `CartItem` model class to the `ProductContext` class.</span></span>

1. <span data-ttu-id="5eede-160">在**解决方案资源管理器**中，查找并打开 "*模型*" 文件夹中的*ProductContext.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="5eede-160">In **Solution Explorer**, find and open the *ProductContext.cs* file in the *Models* folder.</span></span>
2. <span data-ttu-id="5eede-161">将突出显示的代码添加到*ProductContext.cs*文件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5eede-161">Add the highlighted code to the *ProductContext.cs* file as follows:</span></span>  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

<span data-ttu-id="5eede-162">如本系列教程前面所述， *ProductContext.cs*文件中的代码将添加 `System.Data.Entity` 命名空间，以便您可以访问实体框架的所有核心功能。</span><span class="sxs-lookup"><span data-stu-id="5eede-162">As mentioned previously in this tutorial series, the code in the *ProductContext.cs* file adds the `System.Data.Entity` namespace so that you have access to all the core functionality of the Entity Framework.</span></span> <span data-ttu-id="5eede-163">此功能包括使用强类型对象查询、插入、更新和删除数据的功能。</span><span class="sxs-lookup"><span data-stu-id="5eede-163">This functionality includes the capability to query, insert, update, and delete data by working with strongly typed objects.</span></span> <span data-ttu-id="5eede-164">`ProductContext` 类添加对新添加的 `CartItem` 模型类的访问。</span><span class="sxs-lookup"><span data-stu-id="5eede-164">The `ProductContext` class adds access to the newly added `CartItem` model class.</span></span>

### <a name="managing-the-shopping-cart-business-logic"></a><span data-ttu-id="5eede-165">管理购物车业务逻辑</span><span class="sxs-lookup"><span data-stu-id="5eede-165">Managing the Shopping Cart Business Logic</span></span>

<span data-ttu-id="5eede-166">接下来，你将在新的*逻辑*文件夹中创建 `ShoppingCart` 类。</span><span class="sxs-lookup"><span data-stu-id="5eede-166">Next, you'll create the `ShoppingCart` class in a new *Logic* folder.</span></span> <span data-ttu-id="5eede-167">`ShoppingCart` 类处理对 `CartItem` 表的数据访问。</span><span class="sxs-lookup"><span data-stu-id="5eede-167">The `ShoppingCart` class handles data access to the `CartItem` table.</span></span> <span data-ttu-id="5eede-168">类还将包括用于添加、删除和更新购物车中的项的业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="5eede-168">The class will also include the business logic to add, remove, and update items in the shopping cart.</span></span>

<span data-ttu-id="5eede-169">你将添加的购物车逻辑将包含管理以下操作的功能：</span><span class="sxs-lookup"><span data-stu-id="5eede-169">The shopping cart logic that you will add will contain the functionality to manage the following actions:</span></span>

1. <span data-ttu-id="5eede-170">将商品添加到购物车</span><span class="sxs-lookup"><span data-stu-id="5eede-170">Adding items to the shopping cart</span></span>
2. <span data-ttu-id="5eede-171">从购物车中删除商品</span><span class="sxs-lookup"><span data-stu-id="5eede-171">Removing items from the shopping cart</span></span>
3. <span data-ttu-id="5eede-172">获取购物车 ID</span><span class="sxs-lookup"><span data-stu-id="5eede-172">Getting the shopping cart ID</span></span>
4. <span data-ttu-id="5eede-173">检索购物车中的物品</span><span class="sxs-lookup"><span data-stu-id="5eede-173">Retrieving items from the shopping cart</span></span>
5. <span data-ttu-id="5eede-174">总计购物车商品的总量</span><span class="sxs-lookup"><span data-stu-id="5eede-174">Totaling the amount of all the shopping cart items</span></span>
6. <span data-ttu-id="5eede-175">更新购物车数据</span><span class="sxs-lookup"><span data-stu-id="5eede-175">Updating the shopping cart data</span></span>

<span data-ttu-id="5eede-176">购物车页面（*ShoppingCart*）和购物车类将一起用于访问购物车数据。</span><span class="sxs-lookup"><span data-stu-id="5eede-176">A shopping cart page (*ShoppingCart.aspx*) and the shopping cart class will be used together to access shopping cart data.</span></span> <span data-ttu-id="5eede-177">"购物车" 页将显示用户添加到购物车中的所有项目。</span><span class="sxs-lookup"><span data-stu-id="5eede-177">The shopping cart page will display all the items the user adds to the shopping cart.</span></span> <span data-ttu-id="5eede-178">除了购物车页和类之外，你还将创建一个页面（*AddToCart*），用于将产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-178">Besides the shopping cart page and class, you'll create a page (*AddToCart.aspx*) to add products to the shopping cart.</span></span> <span data-ttu-id="5eede-179">你还会将代码添加到*ProductList*页和*ProductDetails*页，该页面将提供指向*AddToCart*页的链接，以便用户可以将产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-179">You will also add code to the *ProductList.aspx* page and the *ProductDetails.aspx* page that will provide a link to the *AddToCart.aspx* page, so that the user can add products to the shopping cart.</span></span>

<span data-ttu-id="5eede-180">下图显示了用户向购物车添加产品时所发生的基本过程。</span><span class="sxs-lookup"><span data-stu-id="5eede-180">The following diagram shows the basic process that occurs when the user adds a product to the shopping cart.</span></span>

![购物车-添加到购物车](shopping-cart/_static/image3.png)

<span data-ttu-id="5eede-182">当用户单击*ProductList*页或*ProductDetails*页上的 "**添加到购物车**" 链接时，应用程序将导航到*AddToCart*页，然后自动定位到*ShoppingCart*页。</span><span class="sxs-lookup"><span data-stu-id="5eede-182">When the user clicks the **Add To Cart** link on either the *ProductList.aspx* page or the *ProductDetails.aspx* page, the application will navigate to the *AddToCart.aspx* page and then automatically to the *ShoppingCart.aspx* page.</span></span> <span data-ttu-id="5eede-183">*AddToCart*页面通过调用 ShoppingCart 类中的方法将选择的产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-183">The *AddToCart.aspx* page will add the select product to the shopping cart by calling a method in the ShoppingCart class.</span></span> <span data-ttu-id="5eede-184">*ShoppingCart*页将显示已添加到购物车中的产品。</span><span class="sxs-lookup"><span data-stu-id="5eede-184">The *ShoppingCart.aspx* page will display the products that have been added to the shopping cart.</span></span>

#### <a name="creating-the-shopping-cart-class"></a><span data-ttu-id="5eede-185">创建购物车类</span><span class="sxs-lookup"><span data-stu-id="5eede-185">Creating the Shopping Cart Class</span></span>

<span data-ttu-id="5eede-186">`ShoppingCart` 类将添加到应用程序中的单独文件夹中，以便模型（模型文件夹）、页面（根文件夹）和逻辑（逻辑文件夹）之间存在明显的区别。</span><span class="sxs-lookup"><span data-stu-id="5eede-186">The `ShoppingCart` class will be added to a separate folder in the application so that there will be a clear distinction between the model (Models folder), the pages (root folder) and the logic (Logic folder).</span></span>

1. <span data-ttu-id="5eede-187">在**解决方案资源管理器**中，右键单击**WingtipToys**项目，然后选择 "**添加**-&gt;**新文件夹**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-187">In **Solution Explorer**, right-click the **WingtipToys**project and select **Add**-&gt;**New Folder**.</span></span> <span data-ttu-id="5eede-188">将新文件夹命名为*逻辑*。</span><span class="sxs-lookup"><span data-stu-id="5eede-188">Name the new folder *Logic*.</span></span>
2. <span data-ttu-id="5eede-189">右键单击*逻辑*文件夹，然后选择 "**添加** -&gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-189">Right-click the *Logic* folder and then select **Add** -&gt; **New Item**.</span></span>
3. <span data-ttu-id="5eede-190">添加一个名为*ShoppingCartActions.cs*的新类文件。</span><span class="sxs-lookup"><span data-stu-id="5eede-190">Add a new class file named *ShoppingCartActions.cs*.</span></span>
4. <span data-ttu-id="5eede-191">将默认代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5eede-191">Replace the default code with the following code:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

<span data-ttu-id="5eede-192">利用 `AddToCart` 方法，可以根据产品 `ID`将各个产品包括在购物车中。</span><span class="sxs-lookup"><span data-stu-id="5eede-192">The `AddToCart` method enables individual products to be included in the shopping cart based on the product `ID`.</span></span> <span data-ttu-id="5eede-193">该产品将添加到购物车中，或者，如果该购物车中已包含该产品的物品，则该数量将递增。</span><span class="sxs-lookup"><span data-stu-id="5eede-193">The product is added to the cart, or if the cart already contains an item for that product, the quantity is incremented.</span></span>

<span data-ttu-id="5eede-194">`GetCartId` 方法返回用户的购物车 `ID`。</span><span class="sxs-lookup"><span data-stu-id="5eede-194">The `GetCartId` method returns the cart `ID` for the user.</span></span> <span data-ttu-id="5eede-195">购物车 `ID` 用于跟踪用户在其购物车中的物品。</span><span class="sxs-lookup"><span data-stu-id="5eede-195">The cart `ID` is used to track the items that a user has in their shopping cart.</span></span> <span data-ttu-id="5eede-196">如果用户没有 `ID`的现有购物车，将为其创建新的 cart `ID`。</span><span class="sxs-lookup"><span data-stu-id="5eede-196">If the user does not have an existing cart `ID`, a new cart `ID` is created for them.</span></span> <span data-ttu-id="5eede-197">如果用户以注册用户身份登录，则会将购物车 `ID` 设置为他们的用户名。</span><span class="sxs-lookup"><span data-stu-id="5eede-197">If the user is signed in as a registered user, the cart `ID` is set to their user name.</span></span> <span data-ttu-id="5eede-198">但是，如果用户未登录，则购物车 `ID` 设置为唯一值（GUID）。</span><span class="sxs-lookup"><span data-stu-id="5eede-198">However, if the user is not signed in, the cart `ID` is set to a unique value (a GUID).</span></span> <span data-ttu-id="5eede-199">GUID 可确保为每个用户仅基于会话创建一个购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-199">A GUID ensures that only one cart is created for each user, based on session.</span></span>

<span data-ttu-id="5eede-200">`GetCartItems` 方法返回用户的购物车项列表。</span><span class="sxs-lookup"><span data-stu-id="5eede-200">The `GetCartItems` method returns a list of shopping cart items for the user.</span></span> <span data-ttu-id="5eede-201">在本教程的后面部分中，你将看到，使用 `GetCartItems` 方法在购物车中显示购物车项的模型绑定。</span><span class="sxs-lookup"><span data-stu-id="5eede-201">Later in this tutorial, you will see that model binding is used to display the cart items in the shopping cart using the `GetCartItems` method.</span></span>

### <a name="creating-the-add-to-cart-functionality"></a><span data-ttu-id="5eede-202">创建添加到购物车功能</span><span class="sxs-lookup"><span data-stu-id="5eede-202">Creating the Add-To-Cart Functionality</span></span>

<span data-ttu-id="5eede-203">如前文所述，你将创建一个名为*AddToCart*的处理页，该页面将用于向用户的购物车中添加新产品。</span><span class="sxs-lookup"><span data-stu-id="5eede-203">As mentioned earlier, you will create a processing page named *AddToCart.aspx* that will be used to add new products to the shopping cart of the user.</span></span> <span data-ttu-id="5eede-204">此页将调用刚才创建的 `ShoppingCart` 类中的 `AddToCart` 方法。</span><span class="sxs-lookup"><span data-stu-id="5eede-204">This page will call the `AddToCart` method in the `ShoppingCart` class that you just created.</span></span> <span data-ttu-id="5eede-205">*AddToCart*页将预计向其传递产品 `ID`。</span><span class="sxs-lookup"><span data-stu-id="5eede-205">The *AddToCart.aspx* page will expect that a product `ID` is passed to it.</span></span> <span data-ttu-id="5eede-206">此产品 `ID` 将在 `ShoppingCart` 类中调用 `AddToCart` 方法时使用。</span><span class="sxs-lookup"><span data-stu-id="5eede-206">This product `ID` will be used when calling the `AddToCart` method in the `ShoppingCart` class.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5eede-207">你将修改此页面的代码隐藏（*AddToCart.aspx.cs*），而不是页面 UI （*AddToCart*）。</span><span class="sxs-lookup"><span data-stu-id="5eede-207">You will be modifying the code-behind (*AddToCart.aspx.cs*) for this page, not the page UI (*AddToCart.aspx*).</span></span>

#### <a name="to-create-the-add-to-cart-functionality"></a><span data-ttu-id="5eede-208">若要创建 "添加到购物车" 功能：</span><span class="sxs-lookup"><span data-stu-id="5eede-208">To create the Add-To-Cart functionality:</span></span>

1. <span data-ttu-id="5eede-209">在**解决方案资源管理器**中，右键单击**WingtipToys**项目，然后单击 "**添加** -" &gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-209">In **Solution Explorer**, right-click the **WingtipToys**project, click **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="5eede-210">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="5eede-210">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="5eede-211">将标准新页面（Web 窗体）添加到名为*AddToCart*的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5eede-211">Add a standard new page (Web Form) to the application named *AddToCart.aspx*.</span></span> 

    ![购物车-添加 Web 窗体](shopping-cart/_static/image4.png)
3. <span data-ttu-id="5eede-213">在**解决方案资源管理器**中，右键单击 " *AddToCart* " 页，然后单击 "**查看代码**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-213">In **Solution Explorer**, right-click the *AddToCart.aspx* page and then click **View Code**.</span></span> <span data-ttu-id="5eede-214">*AddToCart.aspx.cs*代码隐藏文件在编辑器中打开。</span><span class="sxs-lookup"><span data-stu-id="5eede-214">The *AddToCart.aspx.cs* code-behind file is opened in the editor.</span></span>
4. <span data-ttu-id="5eede-215">将*AddToCart.aspx.cs*代码隐藏中的现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5eede-215">Replace the existing code in the *AddToCart.aspx.cs* code-behind with the following:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

<span data-ttu-id="5eede-216">加载*AddToCart*页面后，将从查询字符串中检索 product `ID`。</span><span class="sxs-lookup"><span data-stu-id="5eede-216">When the *AddToCart.aspx* page is loaded, the product `ID` is retrieved from the query string.</span></span> <span data-ttu-id="5eede-217">接下来，将创建一个购物车类的实例，并使用该实例来调用你之前在本教程中添加的 `AddToCart` 方法。</span><span class="sxs-lookup"><span data-stu-id="5eede-217">Next, an instance of the shopping cart class is created and used to call the `AddToCart` method that you added earlier in this tutorial.</span></span> <span data-ttu-id="5eede-218">*ShoppingCartActions.cs*文件中包含的 `AddToCart` 方法包含将所选产品添加到购物车或增加所选产品的产品数量的逻辑。</span><span class="sxs-lookup"><span data-stu-id="5eede-218">The `AddToCart` method, contained in the *ShoppingCartActions.cs* file, includes the logic to add the selected product to the shopping cart or increment the product quantity of the selected product.</span></span> <span data-ttu-id="5eede-219">如果产品尚未添加到购物车中，则会将该产品添加到数据库的 `CartItem` 表。</span><span class="sxs-lookup"><span data-stu-id="5eede-219">If the product hasn't been added to the shopping cart, the product is added to the `CartItem` table of the database.</span></span> <span data-ttu-id="5eede-220">如果产品已添加到购物车，并且用户添加了同一产品的其他项，则产品数量在 `CartItem` 表中递增。</span><span class="sxs-lookup"><span data-stu-id="5eede-220">If the product has already been added to the shopping cart and the user adds an additional item of the same product, the product quantity is incremented in the `CartItem` table.</span></span> <span data-ttu-id="5eede-221">最后，页面重定向回*ShoppingCart*页面，你将在下一步中添加该页面，用户可在其中查看购物车中的项目的更新列表。</span><span class="sxs-lookup"><span data-stu-id="5eede-221">Finally, the page redirects back to the *ShoppingCart.aspx* page that you'll add in the next step, where the user sees an updated list of items in the cart.</span></span>

<span data-ttu-id="5eede-222">如前所述，用户 `ID` 用于标识与特定用户关联的产品。</span><span class="sxs-lookup"><span data-stu-id="5eede-222">As previously mentioned, a user `ID` is used to identify the products that are associated with a specific user.</span></span> <span data-ttu-id="5eede-223">每次用户将产品添加到购物车时，此 `ID` 都会添加到 `CartItem` 表中的一行。</span><span class="sxs-lookup"><span data-stu-id="5eede-223">This `ID` is added to a row in the `CartItem` table each time the user adds a product to the shopping cart.</span></span>

### <a name="creating-the-shopping-cart-ui"></a><span data-ttu-id="5eede-224">创建购物车 UI</span><span class="sxs-lookup"><span data-stu-id="5eede-224">Creating the Shopping Cart UI</span></span>

<span data-ttu-id="5eede-225">" *ShoppingCart* " 页将显示用户已添加到其购物车中的产品。</span><span class="sxs-lookup"><span data-stu-id="5eede-225">The *ShoppingCart.aspx* page will display the products that the user has added to their shopping cart.</span></span> <span data-ttu-id="5eede-226">它还将提供在购物车中添加、删除和更新项的功能。</span><span class="sxs-lookup"><span data-stu-id="5eede-226">It will also provide the ability to add, remove and update items in the shopping cart.</span></span>

1. <span data-ttu-id="5eede-227">在**解决方案资源管理器**中，右键单击**WingtipToys**，再单击 "**添加** -" &gt;**新项**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-227">In **Solution Explorer**, right-click **WingtipToys**, click **Add** -&gt; **New Item**.</span></span>  
   <span data-ttu-id="5eede-228">随即出现“添加新项”对话框。</span><span class="sxs-lookup"><span data-stu-id="5eede-228">The **Add New Item** dialog box is displayed.</span></span>
2. <span data-ttu-id="5eede-229">通过选择 "**使用母版页的 Web 窗体**"，添加包含母版页的新页面（Web 窗体）。</span><span class="sxs-lookup"><span data-stu-id="5eede-229">Add a new page (Web Form) that includes a master page by selecting **Web Form using Master Page**.</span></span> <span data-ttu-id="5eede-230">将新页面命名为*ShoppingCart*。</span><span class="sxs-lookup"><span data-stu-id="5eede-230">Name the new page *ShoppingCart.aspx*.</span></span>
3. <span data-ttu-id="5eede-231">选择 "**站点**" 以将母版页附加到新创建的 *.aspx*页面。</span><span class="sxs-lookup"><span data-stu-id="5eede-231">Select **Site.Master** to attach the master page to the newly created *.aspx* page.</span></span>
4. <span data-ttu-id="5eede-232">在*ShoppingCart*页中，将现有标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="5eede-232">In the *ShoppingCart.aspx* page, replace the existing markup with the following markup:</span></span>   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

<span data-ttu-id="5eede-233">*ShoppingCart*页包含一个名为 `CartList`的**GridView**控件。</span><span class="sxs-lookup"><span data-stu-id="5eede-233">The *ShoppingCart.aspx* page includes a **GridView** control named `CartList`.</span></span> <span data-ttu-id="5eede-234">此控件使用模型绑定将购物车数据从数据库绑定到**GridView**控件。</span><span class="sxs-lookup"><span data-stu-id="5eede-234">This control uses model binding to bind the shopping cart data from the database to the **GridView** control.</span></span> <span data-ttu-id="5eede-235">设置**GridView**控件的 `ItemType` 属性时，数据绑定表达式 `Item` 在控件的标记中可用，并且控件将成为强类型。</span><span class="sxs-lookup"><span data-stu-id="5eede-235">When you set the `ItemType` property of the **GridView** control, the data-binding expression `Item` is available in the markup of the control and the control becomes strongly typed.</span></span> <span data-ttu-id="5eede-236">如本系列教程前面所述，可以使用 IntelliSense 选择 `Item` 对象的详细信息。</span><span class="sxs-lookup"><span data-stu-id="5eede-236">As mentioned earlier in this tutorial series, you can select details of the `Item` object using IntelliSense.</span></span> <span data-ttu-id="5eede-237">若要将数据控件配置为使用模型绑定来选择数据，请设置控件的 `SelectMethod` 属性。</span><span class="sxs-lookup"><span data-stu-id="5eede-237">To configure a data control to use model binding to select data, you set the `SelectMethod` property of the control.</span></span> <span data-ttu-id="5eede-238">在上面的标记中，将 `SelectMethod` 设置为使用 GetShoppingCartItems 方法，该方法返回 `CartItem` 对象的列表。</span><span class="sxs-lookup"><span data-stu-id="5eede-238">In the markup above, you set the `SelectMethod` to use the GetShoppingCartItems method which returns a list of `CartItem` objects.</span></span> <span data-ttu-id="5eede-239">**GridView**数据控件在页面生命周期中的适当时间调用方法，并自动绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="5eede-239">The **GridView** data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="5eede-240">仍需添加 `GetShoppingCartItems` 方法。</span><span class="sxs-lookup"><span data-stu-id="5eede-240">The `GetShoppingCartItems` method must still be added.</span></span>

#### <a name="retrieving-the-shopping-cart-items"></a><span data-ttu-id="5eede-241">检索购物车商品</span><span class="sxs-lookup"><span data-stu-id="5eede-241">Retrieving the Shopping Cart Items</span></span>

<span data-ttu-id="5eede-242">接下来，将代码添加到*ShoppingCart.aspx.cs*代码隐藏中以检索和填充购物车 UI。</span><span class="sxs-lookup"><span data-stu-id="5eede-242">Next, you add code to the *ShoppingCart.aspx.cs* code-behind to retrieve and populate the Shopping Cart UI.</span></span>

1. <span data-ttu-id="5eede-243">在**解决方案资源管理器**中，右键单击 " *ShoppingCart* " 页，然后单击 "**查看代码**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-243">In **Solution Explorer**, right-click the *ShoppingCart.aspx* page and then click **View Code**.</span></span> <span data-ttu-id="5eede-244">*ShoppingCart.aspx.cs*代码隐藏文件在编辑器中打开。</span><span class="sxs-lookup"><span data-stu-id="5eede-244">The *ShoppingCart.aspx.cs* code-behind file is opened in the editor.</span></span>
2. <span data-ttu-id="5eede-245">将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="5eede-245">Replace the existing code with the following:</span></span>  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

<span data-ttu-id="5eede-246">如上所述，`GridView` 数据控件在页面生命周期中的适当时间调用 `GetShoppingCartItems` 方法，并自动绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="5eede-246">As mentioned above, the `GridView` data control calls the `GetShoppingCartItems` method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="5eede-247">`GetShoppingCartItems` 方法创建 `ShoppingCartActions` 对象的实例。</span><span class="sxs-lookup"><span data-stu-id="5eede-247">The `GetShoppingCartItems` method creates an instance of the `ShoppingCartActions` object.</span></span> <span data-ttu-id="5eede-248">然后，该代码使用该实例通过调用 `GetCartItems` 方法返回购物车中的项。</span><span class="sxs-lookup"><span data-stu-id="5eede-248">Then, the code uses that instance to return the items in the cart by calling the `GetCartItems` method.</span></span>

### <a name="adding-products-to-the-shopping-cart"></a><span data-ttu-id="5eede-249">将产品添加到购物车</span><span class="sxs-lookup"><span data-stu-id="5eede-249">Adding Products to the Shopping Cart</span></span>

<span data-ttu-id="5eede-250">当显示 " *ProductList* " 或 " *ProductDetails* " 页时，用户将能够使用链接将产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-250">When either the *ProductList.aspx* or the *ProductDetails.aspx* page is displayed, the user will be able to add the product to the shopping cart using a link.</span></span> <span data-ttu-id="5eede-251">当他们单击此链接时，应用程序将导航到名为*AddToCart*的处理页。</span><span class="sxs-lookup"><span data-stu-id="5eede-251">When they click the link, the application navigates to the processing page named *AddToCart.aspx*.</span></span> <span data-ttu-id="5eede-252">*AddToCart*页将调用你之前在本教程中添加的 `ShoppingCart` 类中的 `AddToCart` 方法。</span><span class="sxs-lookup"><span data-stu-id="5eede-252">The *AddToCart.aspx* page will call the `AddToCart` method in the `ShoppingCart` class that you added earlier in this tutorial.</span></span>

<span data-ttu-id="5eede-253">现在，将添加到 " *ProductList* " 页和 " *ProductDetails* " 页的 "**添加到购物车**" 链接。</span><span class="sxs-lookup"><span data-stu-id="5eede-253">Now, you'll add an **Add to Cart** link to both the *ProductList.aspx* page and the *ProductDetails.aspx* page.</span></span> <span data-ttu-id="5eede-254">此链接将包含从数据库中检索到的产品 `ID`。</span><span class="sxs-lookup"><span data-stu-id="5eede-254">This link will include the product `ID` that is retrieved from the database.</span></span>

1. <span data-ttu-id="5eede-255">在**解决方案资源管理器**中，找到并打开名为*ProductList*的页。</span><span class="sxs-lookup"><span data-stu-id="5eede-255">In **Solution Explorer**, find and open the page named *ProductList.aspx*.</span></span>
2. <span data-ttu-id="5eede-256">将黄色突出显示的标记添加到*ProductList*页面，使整个页面显示如下：</span><span class="sxs-lookup"><span data-stu-id="5eede-256">Add the markup highlighted in yellow to the *ProductList.aspx* page so that the entire page appears as follows:</span></span>  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a><span data-ttu-id="5eede-257">测试购物车</span><span class="sxs-lookup"><span data-stu-id="5eede-257">Testing the Shopping Cart</span></span>

<span data-ttu-id="5eede-258">运行应用程序，了解如何将产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-258">Run the application to see how you add products to the shopping cart.</span></span>

1. <span data-ttu-id="5eede-259">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="5eede-259">Press **F5** to run the application.</span></span>  
 <span data-ttu-id="5eede-260">在项目重新创建数据库后，浏览器将打开并显示*default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5eede-260">After the project recreates the database, the browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="5eede-261">从类别导航菜单中选择 "**汽车**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-261">Select **Cars** from the category navigation menu.</span></span>  
 <span data-ttu-id="5eede-262">随即显示 " *ProductList* " 页，其中仅显示 "汽车" 类别中包含的产品。</span><span class="sxs-lookup"><span data-stu-id="5eede-262">The *ProductList.aspx* page is displayed showing only products included in the "Cars" category.</span></span> 

    ![购物车-汽车](shopping-cart/_static/image5.png)
3. <span data-ttu-id="5eede-264">单击列出的第一个产品旁边的 "**添加到购物车**" 链接（可转换的汽车）。</span><span class="sxs-lookup"><span data-stu-id="5eede-264">Click the **Add to Cart** link next to the first product listed (the convertible car).</span></span>   
 <span data-ttu-id="5eede-265">随即显示 " *ShoppingCart* " 页，其中显示购物车中的选择。</span><span class="sxs-lookup"><span data-stu-id="5eede-265">The *ShoppingCart.aspx* page is displayed, showing the selection in your shopping cart.</span></span> 

    ![购物车-购物车](shopping-cart/_static/image6.png)
4. <span data-ttu-id="5eede-267">通过从类别导航菜单中选择 "**平面**" 来查看其他产品。</span><span class="sxs-lookup"><span data-stu-id="5eede-267">View additional products by selecting **Planes** from the category navigation menu.</span></span>
5. <span data-ttu-id="5eede-268">单击列出的第一个产品旁边的 "**添加到购物车**" 链接。</span><span class="sxs-lookup"><span data-stu-id="5eede-268">Click the **Add to Cart** link next to the first product listed.</span></span>  
 <span data-ttu-id="5eede-269">随即显示*ShoppingCart*页，其中包含附加项。</span><span class="sxs-lookup"><span data-stu-id="5eede-269">The *ShoppingCart.aspx* page is displayed with the additional item.</span></span>
6. <span data-ttu-id="5eede-270">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="5eede-270">Close the browser.</span></span>

### <a name="calculating-and-displaying-the-order-total"></a><span data-ttu-id="5eede-271">计算并显示订单总计</span><span class="sxs-lookup"><span data-stu-id="5eede-271">Calculating and Displaying the Order Total</span></span>

<span data-ttu-id="5eede-272">除了将产品添加到购物车外，还会将 `GetTotal` 方法添加到 `ShoppingCart` 类，并在购物车页中显示总订单量。</span><span class="sxs-lookup"><span data-stu-id="5eede-272">In addition to adding products to the shopping cart, you will add a `GetTotal` method to the `ShoppingCart` class and display the total order amount in the shopping cart page.</span></span>

1. <span data-ttu-id="5eede-273">在**解决方案资源管理器**中，打开*逻辑*文件夹中的*ShoppingCartActions.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="5eede-273">In **Solution Explorer**, open the *ShoppingCartActions.cs* file in the *Logic* folder.</span></span>
2. <span data-ttu-id="5eede-274">向 `ShoppingCart` 类添加以黄色突出显示的以下 `GetTotal` 方法，使类显示如下：</span><span class="sxs-lookup"><span data-stu-id="5eede-274">Add the following `GetTotal` method highlighted in yellow to the `ShoppingCart` class, so that the class appears as follows:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

<span data-ttu-id="5eede-275">首先，`GetTotal` 方法获取用户的购物车的 ID。</span><span class="sxs-lookup"><span data-stu-id="5eede-275">First, the `GetTotal` method gets the ID of the shopping cart for the user.</span></span> <span data-ttu-id="5eede-276">然后，该方法通过将产品价格乘以购物车中列出的每个产品的产品数量，来获取购物车总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-276">Then the method gets the cart total by multiplying the product price by the product quantity for each product listed in the cart.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="5eede-277">上面的代码使用可以为 null 的类型 "`int?`"。</span><span class="sxs-lookup"><span data-stu-id="5eede-277">The above code uses the nullable type "`int?`".</span></span> <span data-ttu-id="5eede-278">可以为 null 的类型可以表示基础类型的所有值，也可以表示为 null 值。</span><span class="sxs-lookup"><span data-stu-id="5eede-278">Nullable types can represent all the values of an underlying type, and also as a null value.</span></span> <span data-ttu-id="5eede-279">有关详细信息，请参阅[使用可以为 null 的类型](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="5eede-279">For more information see, [Using Nullable Types](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx).</span></span>

### <a name="modify-the-shopping-cart-display"></a><span data-ttu-id="5eede-280">修改购物车显示</span><span class="sxs-lookup"><span data-stu-id="5eede-280">Modify the Shopping Cart Display</span></span>

<span data-ttu-id="5eede-281">接下来，您将修改*ShoppingCart*页的代码，以调用 `GetTotal` 方法，并在加载页面时在*ShoppingCart*页上显示该总数。</span><span class="sxs-lookup"><span data-stu-id="5eede-281">Next you'll modify the code for the *ShoppingCart.aspx* page to call the `GetTotal` method and display that total on the *ShoppingCart.aspx* page when the page loads.</span></span>

1. <span data-ttu-id="5eede-282">在**解决方案资源管理器**中，右键单击 " *ShoppingCart* " 页，然后选择 "**查看代码**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-282">In **Solution Explorer**, right-click the *ShoppingCart.aspx* page and select **View Code**.</span></span>
2. <span data-ttu-id="5eede-283">在*ShoppingCart.aspx.cs*文件中，通过添加以下突出显示的代码来更新 `Page_Load` 处理程序：</span><span class="sxs-lookup"><span data-stu-id="5eede-283">In the *ShoppingCart.aspx.cs* file, update the `Page_Load` handler by adding the following code highlighted in yellow:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

<span data-ttu-id="5eede-284">加载*ShoppingCart*页面时，它会加载购物车对象，然后通过调用 `ShoppingCart` 类的 `GetTotal` 方法来检索购物车总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-284">When the *ShoppingCart.aspx* page loads, it loads the shopping cart object and then retrieves the shopping cart total by calling the `GetTotal` method of the `ShoppingCart` class.</span></span> <span data-ttu-id="5eede-285">如果购物车为空，则显示一条指向该效果的消息。</span><span class="sxs-lookup"><span data-stu-id="5eede-285">If the shopping cart is empty, a message to that effect is displayed.</span></span>

### <a name="testing-the-shopping-cart-total"></a><span data-ttu-id="5eede-286">测试购物车总计</span><span class="sxs-lookup"><span data-stu-id="5eede-286">Testing the Shopping Cart Total</span></span>

<span data-ttu-id="5eede-287">立即运行该应用程序，了解如何将产品添加到购物车，但你可以看到购物车总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-287">Run the application now to see how you can not only add a product to the shopping cart, but you can see the shopping cart total.</span></span>

1. <span data-ttu-id="5eede-288">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="5eede-288">Press **F5** to run the application.</span></span>  
 <span data-ttu-id="5eede-289">浏览器将打开并显示*default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5eede-289">The browser will open and show the *Default.aspx* page.</span></span>
2. <span data-ttu-id="5eede-290">从类别导航菜单中选择 "**汽车**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-290">Select **Cars** from the category navigation menu.</span></span>
3. <span data-ttu-id="5eede-291">单击第一个产品旁边的 "**添加到购物车**" 链接。</span><span class="sxs-lookup"><span data-stu-id="5eede-291">Click the **Add To Cart** link next to the first product.</span></span>   
 <span data-ttu-id="5eede-292">将显示*ShoppingCart*页，其中包含订单总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-292">The *ShoppingCart.aspx* page is displayed with the order total.</span></span> 

    ![购物车-购物车总计](shopping-cart/_static/image7.png)
4. <span data-ttu-id="5eede-294">将一些其他产品（例如，飞机）添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-294">Add some other products (for example, a plane) to the cart.</span></span>
5. <span data-ttu-id="5eede-295">随即显示 " *ShoppingCart* " 页，其中包含已添加的所有产品的更新总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-295">The *ShoppingCart.aspx* page is displayed with an updated total for all the products you've added.</span></span> 

    ![购物车-多个产品](shopping-cart/_static/image8.png)
6. <span data-ttu-id="5eede-297">关闭浏览器窗口，停止正在运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5eede-297">Stop the running app by closing the browser window.</span></span>

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a><span data-ttu-id="5eede-298">向购物车添加 "更新" 和 "签出" 按钮</span><span class="sxs-lookup"><span data-stu-id="5eede-298">Adding Update and Checkout Buttons to the Shopping Cart</span></span>

<span data-ttu-id="5eede-299">若要允许用户修改购物车，你需要将 "**更新**" 按钮和 "**结帐**" 按钮添加到 "购物车" 页。</span><span class="sxs-lookup"><span data-stu-id="5eede-299">To allow the users to modify the shopping cart, you'll add an **Update** button and a **Checkout** button to the shopping cart page.</span></span> <span data-ttu-id="5eede-300">在本系列教程的后面部分中，将不使用 "**签出**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="5eede-300">The **Checkout** button is not used until later in this tutorial series.</span></span>

1. <span data-ttu-id="5eede-301">在**解决方案资源管理器**中，打开 web 应用程序项目的根目录中的*ShoppingCart*页。</span><span class="sxs-lookup"><span data-stu-id="5eede-301">In **Solution Explorer**, open the *ShoppingCart.aspx* page in the root of the web application project.</span></span>
2. <span data-ttu-id="5eede-302">若要将 "**更新**" 按钮和 "**签出**" 按钮添加到 " *ShoppingCart* " 页，请将黄色突出显示的标记添加到现有标记，如以下代码所示：</span><span class="sxs-lookup"><span data-stu-id="5eede-302">To add the **Update** button and the **Checkout** button to the *ShoppingCart.aspx* page, add the markup highlighted in yellow to the existing markup, as shown in the following code:</span></span>   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

<span data-ttu-id="5eede-303">当用户单击 "**更新**" 按钮时，将调用 `UpdateBtn_Click` 事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="5eede-303">When the user clicks the **Update** button, the `UpdateBtn_Click` event handler will be called.</span></span> <span data-ttu-id="5eede-304">此事件处理程序将调用你将在下一步中添加的代码。</span><span class="sxs-lookup"><span data-stu-id="5eede-304">This event handler will call the code that you'll add in the next step.</span></span>

<span data-ttu-id="5eede-305">接下来，你可以更新*ShoppingCart.aspx.cs*文件中包含的代码，以循环遍历购物车项并调用 `RemoveItem` 和 `UpdateItem` 方法。</span><span class="sxs-lookup"><span data-stu-id="5eede-305">Next, you can update the code contained in the *ShoppingCart.aspx.cs* file to loop through the cart items and call the `RemoveItem` and `UpdateItem` methods.</span></span>

1. <span data-ttu-id="5eede-306">在**解决方案资源管理器**中，在 web 应用程序项目的根目录中打开*ShoppingCart.aspx.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="5eede-306">In **Solution Explorer**, open the *ShoppingCart.aspx.cs* file in the root of the web application project.</span></span>
2. <span data-ttu-id="5eede-307">将以下代码段以黄色突出显示给*ShoppingCart.aspx.cs*文件：</span><span class="sxs-lookup"><span data-stu-id="5eede-307">Add the following code sections highlighted in yellow to the *ShoppingCart.aspx.cs* file:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

<span data-ttu-id="5eede-308">当用户单击*ShoppingCart*页上的 "**更新**" 按钮时，将调用 UpdateCartItems 方法。</span><span class="sxs-lookup"><span data-stu-id="5eede-308">When the user clicks the **Update** button on the *ShoppingCart.aspx* page, the UpdateCartItems method is called.</span></span> <span data-ttu-id="5eede-309">UpdateCartItems 方法获取购物车中每一项的更新值。</span><span class="sxs-lookup"><span data-stu-id="5eede-309">The UpdateCartItems method gets the updated values for each item in the shopping cart.</span></span> <span data-ttu-id="5eede-310">然后，UpdateCartItems 方法调用 `UpdateShoppingCartDatabase` 方法（在下一步中添加和说明），以添加或删除购物车中的商品。</span><span class="sxs-lookup"><span data-stu-id="5eede-310">Then, the UpdateCartItems method calls the `UpdateShoppingCartDatabase` method (added and explained in the next step) to either add or remove items from the shopping cart.</span></span> <span data-ttu-id="5eede-311">更新数据库以反映购物车的更新后，会通过调用**gridview**的 `DataBind` 方法，在购物车页上更新**gridview**控件。</span><span class="sxs-lookup"><span data-stu-id="5eede-311">Once the database has been updated to reflect the updates to the shopping cart, the **GridView** control is updated on the shopping cart page by calling the `DataBind` method for the **GridView**.</span></span> <span data-ttu-id="5eede-312">此外，还会更新 "购物车" 页上的总订单量，以反映项的更新列表。</span><span class="sxs-lookup"><span data-stu-id="5eede-312">Also, the total order amount on the shopping cart page is updated to reflect the updated list of items.</span></span>

### <a name="updating-and-removing-shopping-cart-items"></a><span data-ttu-id="5eede-313">更新和删除购物车商品</span><span class="sxs-lookup"><span data-stu-id="5eede-313">Updating and Removing Shopping Cart Items</span></span>

<span data-ttu-id="5eede-314">在*ShoppingCart*页上，你可以看到已添加的控件，用于更新项的数量和删除项。</span><span class="sxs-lookup"><span data-stu-id="5eede-314">On the *ShoppingCart.aspx* page, you can see controls have been added for updating the quantity of an item and removing an item.</span></span> <span data-ttu-id="5eede-315">现在，添加将使这些控件工作的代码。</span><span class="sxs-lookup"><span data-stu-id="5eede-315">Now, add the code that will make these controls work.</span></span>

1. <span data-ttu-id="5eede-316">在**解决方案资源管理器**中，打开*逻辑*文件夹中的*ShoppingCartActions.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="5eede-316">In **Solution Explorer**, open the *ShoppingCartActions.cs* file in the *Logic* folder.</span></span>
2. <span data-ttu-id="5eede-317">将以下突出显示的代码添加到*ShoppingCartActions.cs*类文件中：</span><span class="sxs-lookup"><span data-stu-id="5eede-317">Add the following code highlighted in yellow to the *ShoppingCartActions.cs* class file:</span></span>   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

<span data-ttu-id="5eede-318">从*ShoppingCart.aspx.cs*页上的 `UpdateCartItems` 方法调用的 `UpdateShoppingCartDatabase` 方法包含用于从购物车中更新或删除项的逻辑。</span><span class="sxs-lookup"><span data-stu-id="5eede-318">The `UpdateShoppingCartDatabase` method, called from the `UpdateCartItems` method on the *ShoppingCart.aspx.cs* page, contains the logic to either update or remove items from the shopping cart.</span></span> <span data-ttu-id="5eede-319">`UpdateShoppingCartDatabase` 方法将循环访问购物车列表中的所有行。</span><span class="sxs-lookup"><span data-stu-id="5eede-319">The `UpdateShoppingCartDatabase` method iterates through all the rows within the shopping cart list.</span></span> <span data-ttu-id="5eede-320">如果购物车项已标记为要删除，或数量小于1，则调用 `RemoveItem` 方法。</span><span class="sxs-lookup"><span data-stu-id="5eede-320">If a shopping cart item has been marked to be removed, or the quantity is less than one, the `RemoveItem` method is called.</span></span> <span data-ttu-id="5eede-321">否则，在调用 `UpdateItem` 方法时，将检查购物车项的更新。</span><span class="sxs-lookup"><span data-stu-id="5eede-321">Otherwise, the shopping cart item is checked for updates when the `UpdateItem` method is called.</span></span> <span data-ttu-id="5eede-322">在删除或更新购物车项后，将保存数据库更改。</span><span class="sxs-lookup"><span data-stu-id="5eede-322">After the shopping cart item has been removed or updated, the database changes are saved.</span></span>

<span data-ttu-id="5eede-323">`ShoppingCartUpdates` 结构用于保存所有购物车商品。</span><span class="sxs-lookup"><span data-stu-id="5eede-323">The `ShoppingCartUpdates` structure is used to hold all the shopping cart items.</span></span> <span data-ttu-id="5eede-324">`UpdateShoppingCartDatabase` 方法使用 `ShoppingCartUpdates` 结构来确定是否需要更新或移除任何项。</span><span class="sxs-lookup"><span data-stu-id="5eede-324">The `UpdateShoppingCartDatabase` method uses the `ShoppingCartUpdates` structure to determine if any of the items need to be updated or removed.</span></span>

<span data-ttu-id="5eede-325">在下一教程中，你将使用 `EmptyCart` 方法在购买产品后清除购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-325">In the next tutorial, you will use the `EmptyCart` method to clear the shopping cart after purchasing products.</span></span> <span data-ttu-id="5eede-326">但现在，你将使用刚刚添加到*ShoppingCartActions.cs*文件的 `GetCount` 方法来确定购物车中有多少项。</span><span class="sxs-lookup"><span data-stu-id="5eede-326">But for now, you will use the `GetCount` method that you just added to the *ShoppingCartActions.cs* file to determine how many items are in the shopping cart.</span></span>

### <a name="adding-a-shopping-cart-counter"></a><span data-ttu-id="5eede-327">添加购物车计数器</span><span class="sxs-lookup"><span data-stu-id="5eede-327">Adding a Shopping Cart Counter</span></span>

<span data-ttu-id="5eede-328">若要允许用户查看购物车中的总项数，请将计数器添加到*网站母版页*。</span><span class="sxs-lookup"><span data-stu-id="5eede-328">To allow the user to view the total number of items in the shopping cart, you will add a counter to the *Site.Master* page.</span></span> <span data-ttu-id="5eede-329">此计数器还将充当购物车的链接。</span><span class="sxs-lookup"><span data-stu-id="5eede-329">This counter will also act as a link to the shopping cart.</span></span>

1. <span data-ttu-id="5eede-330">在**解决方案资源管理器**中，打开 "*网站母版页*"。</span><span class="sxs-lookup"><span data-stu-id="5eede-330">In **Solution Explorer**, open the *Site.Master* page.</span></span>
2. <span data-ttu-id="5eede-331">通过将 "购物车计数器" 链接（如黄色中所示）添加到导航部分来修改标记，使其显示如下：</span><span class="sxs-lookup"><span data-stu-id="5eede-331">Modify the markup by adding the shopping cart counter link as shown in yellow to the navigation section so it appears as follows:</span></span>  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. <span data-ttu-id="5eede-332">接下来，通过添加黄色突出显示的代码来更新*Site.Master.cs*文件的代码隐藏，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5eede-332">Next, update the code-behind of the *Site.Master.cs* file by adding the code highlighted in yellow as follows:</span></span>  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

<span data-ttu-id="5eede-333">在以 HTML 格式呈现页面之前，会引发 `Page_PreRender` 事件。</span><span class="sxs-lookup"><span data-stu-id="5eede-333">Before the page is rendered as HTML, the `Page_PreRender` event is raised.</span></span> <span data-ttu-id="5eede-334">在 `Page_PreRender` 处理程序中，通过调用 `GetCount` 方法来确定购物车的总计数。</span><span class="sxs-lookup"><span data-stu-id="5eede-334">In the `Page_PreRender` handler, the total count of the shopping cart is determined by calling the `GetCount` method.</span></span> <span data-ttu-id="5eede-335">返回的值将添加到*网站*的标记中包含的 `cartCount` 范围。</span><span class="sxs-lookup"><span data-stu-id="5eede-335">The returned value is added to the `cartCount` span included in the markup of the *Site.Master* page.</span></span> <span data-ttu-id="5eede-336">`<span>` 标记允许正确呈现内部元素。</span><span class="sxs-lookup"><span data-stu-id="5eede-336">The `<span>` tags enables the inner elements to be properly rendered.</span></span> <span data-ttu-id="5eede-337">显示站点的任何页面时，将显示购物车总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-337">When any page of the site is displayed, the shopping cart total will be displayed.</span></span> <span data-ttu-id="5eede-338">用户还可以单击购物车总计来显示购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-338">The user can also click the shopping cart total to display the shopping cart.</span></span>

## <a name="testing-the-completed-shopping-cart"></a><span data-ttu-id="5eede-339">测试已完成的购物车</span><span class="sxs-lookup"><span data-stu-id="5eede-339">Testing the Completed Shopping Cart</span></span>

<span data-ttu-id="5eede-340">现在可以运行应用程序，了解如何添加、删除和更新购物车中的项目。</span><span class="sxs-lookup"><span data-stu-id="5eede-340">You can run the application now to see how you can add, delete, and update items in the shopping cart.</span></span> <span data-ttu-id="5eede-341">购物车总计将反映购物车中所有物品的总成本。</span><span class="sxs-lookup"><span data-stu-id="5eede-341">The shopping cart total will reflect the total cost of all items in the shopping cart.</span></span>

1. <span data-ttu-id="5eede-342">按 **F5** 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="5eede-342">Press **F5** to run the application.</span></span>  
 <span data-ttu-id="5eede-343">浏览器将打开并显示*default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="5eede-343">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="5eede-344">从类别导航菜单中选择 "**汽车**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-344">Select **Cars** from the category navigation menu.</span></span>
3. <span data-ttu-id="5eede-345">单击第一个产品旁边的 "**添加到购物车**" 链接。</span><span class="sxs-lookup"><span data-stu-id="5eede-345">Click the **Add To Cart** link next to the first product.</span></span>   
 <span data-ttu-id="5eede-346">将显示*ShoppingCart*页，其中包含订单总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-346">The *ShoppingCart.aspx* page is displayed with the order total.</span></span>
4. <span data-ttu-id="5eede-347">从类别导航菜单中选择 "**平面**"。</span><span class="sxs-lookup"><span data-stu-id="5eede-347">Select **Planes** from the category navigation menu.</span></span>
5. <span data-ttu-id="5eede-348">单击第一个产品旁边的 "**添加到购物车**" 链接。</span><span class="sxs-lookup"><span data-stu-id="5eede-348">Click the **Add To Cart** link next to the first product.</span></span>
6. <span data-ttu-id="5eede-349">将购物车中第一项的数量设置为3，并选中第二项的 "**删除项**" 复选框。<a id="a"></a></span><span class="sxs-lookup"><span data-stu-id="5eede-349">Set the quantity of the first item in the shopping cart to 3 and select the **Remove Item** check box of the second item.<a id="a"></a></span></span>
7. <span data-ttu-id="5eede-350">单击 "**更新**" 按钮更新 "购物车" 页，并显示新订单总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-350">Click the **Update** button to update the shopping cart page and display the new order total.</span></span> 

    ![购物车-购物车更新](shopping-cart/_static/image9.png)

## <a name="summary"></a><span data-ttu-id="5eede-352">摘要</span><span class="sxs-lookup"><span data-stu-id="5eede-352">Summary</span></span>

<span data-ttu-id="5eede-353">在本教程中，已创建 Wingtip 玩具 Web 窗体示例应用程序的购物车。</span><span class="sxs-lookup"><span data-stu-id="5eede-353">In this tutorial, you have created a shopping cart for the Wingtip Toys Web Forms sample application.</span></span> <span data-ttu-id="5eede-354">在本教程中，你使用了实体框架 Code First、数据批注、强类型化数据控件和模型绑定。</span><span class="sxs-lookup"><span data-stu-id="5eede-354">During this tutorial you have used Entity Framework Code First, data annotations, strongly typed data controls, and model binding.</span></span>

<span data-ttu-id="5eede-355">购物车支持添加、删除和更新用户选择购买的商品。</span><span class="sxs-lookup"><span data-stu-id="5eede-355">The shopping cart supports adding, deleting, and updating items that the user has selected for purchase.</span></span> <span data-ttu-id="5eede-356">除了实现购物车功能外，还了解了如何在**GridView**控件中显示购物车项，并计算订单总计。</span><span class="sxs-lookup"><span data-stu-id="5eede-356">In addition to implementing the shopping cart functionality, you have learned how to display shopping cart items in a **GridView** control and calculate the order total.</span></span>

<span data-ttu-id="5eede-357">为了了解所述功能在实际的业务应用程序中的工作原理，你可以查看基于[nopCommerce](https://github.com/nopSolutions/nopCommerce) -ASP.NET 的开源电子商务购物车的示例。</span><span class="sxs-lookup"><span data-stu-id="5eede-357">In order to understand how the described functionality works in a real business application, you can view the example of [nopCommerce](https://github.com/nopSolutions/nopCommerce) - ASP.NET based open source eCommerce shopping cart.</span></span> <span data-ttu-id="5eede-358">最初，它是基于 Web 窗体构建的，并且已移动到 MVC 并现在 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="5eede-358">Originally, it was built on Web Forms and over the years it moved to MVC and now to ASP.NET Core.</span></span>

## <a name="addition-information"></a><span data-ttu-id="5eede-359">附加信息</span><span class="sxs-lookup"><span data-stu-id="5eede-359">Addition Information</span></span>

[<span data-ttu-id="5eede-360">ASP.NET 会话状态概述</span><span class="sxs-lookup"><span data-stu-id="5eede-360">ASP.NET Session State Overview</span></span>](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> <span data-ttu-id="5eede-361">[上一页](display_data_items_and_details.md)
> [下一页](checkout-and-payment-with-paypal.md)</span><span class="sxs-lookup"><span data-stu-id="5eede-361">[Previous](display_data_items_and_details.md)
[Next](checkout-and-payment-with-paypal.md)</span></span>
