---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: 第4部分：列出产品 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第4部分介绍了如何通过 GridView contr 来列出产品 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457280"
---
# <a name="part-4-listing-products"></a><span data-ttu-id="83d76-104">第4部分：列出产品</span><span class="sxs-lookup"><span data-stu-id="83d76-104">Part 4: Listing Products</span></span>

<span data-ttu-id="83d76-105">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="83d76-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="83d76-106">Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。</span><span class="sxs-lookup"><span data-stu-id="83d76-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="83d76-107">其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="83d76-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="83d76-108">本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="83d76-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="83d76-109">第4部分介绍了如何通过 GridView 控件列出产品。</span><span class="sxs-lookup"><span data-stu-id="83d76-109">Part 4 covers listing products with the GridView control.</span></span>

## <a id="_Toc260221670"></a><span data-ttu-id="83d76-110">用 GridView 控件列出产品</span><span class="sxs-lookup"><span data-stu-id="83d76-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="83d76-111">让我们开始实现 ProductsList 页，方法是在解决方案中单击 "右键单击"，并选择 "添加" 和 "新建项"。</span><span class="sxs-lookup"><span data-stu-id="83d76-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="83d76-112">选择 "使用母版页的 Web 窗体" 并输入页面名称 "ProductsList"。</span><span class="sxs-lookup"><span data-stu-id="83d76-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="83d76-113">单击 "添加"。</span><span class="sxs-lookup"><span data-stu-id="83d76-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="83d76-114">接下来，选择放置网站的 "样式" 文件夹，并从 "文件夹的内容" 窗口中选择它。</span><span class="sxs-lookup"><span data-stu-id="83d76-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="83d76-115">单击 "确定" 以创建页面。</span><span class="sxs-lookup"><span data-stu-id="83d76-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="83d76-116">我们的数据库中填充了产品数据，如下所示。</span><span class="sxs-lookup"><span data-stu-id="83d76-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="83d76-117">创建页面后，我们将再次使用实体数据源来访问该产品数据，但在此示例中，我们需要选择产品实体，并且我们需要将返回的项限制为仅返回所选类别的项。</span><span class="sxs-lookup"><span data-stu-id="83d76-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="83d76-118">为实现此目的，我们会告知 EntityDataSource 自动生成 WHERE 子句，并指定 WhereParameter。</span><span class="sxs-lookup"><span data-stu-id="83d76-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="83d76-119">你会想起，在我们的 "产品类别菜单" 中创建菜单项时，我们会动态生成链接，方法是将 "类别 Id" 添加到每个链接的 QueryString。</span><span class="sxs-lookup"><span data-stu-id="83d76-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CategoryID to the QueryString for each link.</span></span> <span data-ttu-id="83d76-120">我们会告知实体数据源从该查询字符串参数派生 WHERE 参数。</span><span class="sxs-lookup"><span data-stu-id="83d76-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="83d76-121">接下来，我们将配置 ListView 控件以显示产品列表。</span><span class="sxs-lookup"><span data-stu-id="83d76-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="83d76-122">若要创建最佳的购物体验，我们将压缩 ListVew 中显示的每个单独产品的几个简明功能。</span><span class="sxs-lookup"><span data-stu-id="83d76-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="83d76-123">产品名称将是产品详细信息视图的链接。</span><span class="sxs-lookup"><span data-stu-id="83d76-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="83d76-124">将显示产品的价格。</span><span class="sxs-lookup"><span data-stu-id="83d76-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="83d76-125">将显示产品的图像，我们将在应用程序的目录图像目录中动态选择映像。</span><span class="sxs-lookup"><span data-stu-id="83d76-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="83d76-126">我们将包含一个链接，以立即将特定产品添加到购物车。</span><span class="sxs-lookup"><span data-stu-id="83d76-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="83d76-127">下面是 ListView 控件实例的标记。</span><span class="sxs-lookup"><span data-stu-id="83d76-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="83d76-128">我们为每个显示的产品动态构建多个链接。</span><span class="sxs-lookup"><span data-stu-id="83d76-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="83d76-129">此外，在测试自己的新页面之前，我们需要为产品目录映像创建目录结构，如下所示。</span><span class="sxs-lookup"><span data-stu-id="83d76-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="83d76-130">可访问产品映像后，可以测试产品列表页面。</span><span class="sxs-lookup"><span data-stu-id="83d76-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="83d76-131">在站点的 "主页" 页上，单击其中一个 "类别列表" 链接。</span><span class="sxs-lookup"><span data-stu-id="83d76-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="83d76-132">现在，我们需要实现 ProductDetails 页和 AddToCart 功能。</span><span class="sxs-lookup"><span data-stu-id="83d76-132">Now we need to implement the ProductDetails.aspx page and the AddToCart functionality.</span></span>

<span data-ttu-id="83d76-133">如前文所述，使用 "文件-&gt;New" 创建一个使用站点母版页的页名称 ProductDetails。</span><span class="sxs-lookup"><span data-stu-id="83d76-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="83d76-134">我们将再次使用 EntityDataSource 控件来访问数据库中的特定产品记录，我们将使用 ASP.NET FormView 控件按如下所示显示产品数据。</span><span class="sxs-lookup"><span data-stu-id="83d76-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="83d76-135">如果格式看起来有点有趣，请不要担心。</span><span class="sxs-lookup"><span data-stu-id="83d76-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="83d76-136">上面的标记为我们稍后将实现的几项功能留出了显示布局的空间。</span><span class="sxs-lookup"><span data-stu-id="83d76-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="83d76-137">购物车会在应用程序中表示更复杂的逻辑。</span><span class="sxs-lookup"><span data-stu-id="83d76-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="83d76-138">若要开始使用，请使用文件&gt;新建来创建名为 MyShoppingCart 的页。</span><span class="sxs-lookup"><span data-stu-id="83d76-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="83d76-139">请注意，我们不会选择名称 ShoppingCart。</span><span class="sxs-lookup"><span data-stu-id="83d76-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="83d76-140">数据库中包含名为 "ShoppingCart" 的表。</span><span class="sxs-lookup"><span data-stu-id="83d76-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="83d76-141">生成实体数据模型为数据库中的每个表创建了一个类。</span><span class="sxs-lookup"><span data-stu-id="83d76-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="83d76-142">因此，实体数据模型生成了一个名为 "ShoppingCart" 的实体类。</span><span class="sxs-lookup"><span data-stu-id="83d76-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="83d76-143">我们可以编辑模型，以便我们可以将该名称用于购物车实现，或在需要时扩展它，但我们将选择只选择一个名称来避免冲突。</span><span class="sxs-lookup"><span data-stu-id="83d76-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply select a name that will avoid the conflict.</span></span>

<span data-ttu-id="83d76-144">还值得注意的是，我们将创建一个简单的购物车，并使用购物车显示来嵌入购物车逻辑。</span><span class="sxs-lookup"><span data-stu-id="83d76-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="83d76-145">我们还可以选择在完全不同的业务层中实施购物车。</span><span class="sxs-lookup"><span data-stu-id="83d76-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="83d76-146">[上一页](tailspin-spyworks-part-3.md)
> [下一页](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="83d76-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>
