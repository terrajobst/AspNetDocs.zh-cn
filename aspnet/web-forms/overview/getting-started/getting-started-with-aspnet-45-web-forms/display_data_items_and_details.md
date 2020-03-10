---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: 显示数据项和详细信息 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.7 和 Microsoft Visual Studio 2017 生成 ASP.NET Web 窗体应用程序的基础知识。
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520808"
---
# <a name="display-data-items-and-details"></a><span data-ttu-id="e4005-103">显示数据项和详细信息</span><span class="sxs-lookup"><span data-stu-id="e4005-103">Display data items and details</span></span>

<span data-ttu-id="e4005-104">作者： [Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="e4005-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

> <span data-ttu-id="e4005-105">本教程系列介绍使用 ASP.NET 4.7 和 Microsoft Visual Studio 2017 构建 ASP.NET Web 窗体应用程序的基础知识。</span><span class="sxs-lookup"><span data-stu-id="e4005-105">This tutorial series teaches you the basics of building an ASP.NET Web Forms application with ASP.NET 4.7 and Microsoft Visual Studio 2017.</span></span>

<span data-ttu-id="e4005-106">在本教程中，你将了解如何通过 ASP.NET Web 窗体和实体框架 Code First 来显示数据项和数据项的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e4005-106">In this tutorial, you'll learn how to display data items and data item details with ASP.NET Web Forms and Entity Framework Code First.</span></span> <span data-ttu-id="e4005-107">本教程以上一 "UI 和导航" 教程为基础，作为 Wingtip 玩具商店教程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="e4005-107">This tutorial builds on the previous "UI and Navigation" tutorial as part of the Wingtip Toy Store tutorial series.</span></span> <span data-ttu-id="e4005-108">完成本教程后，你将在*ProductsList*页上看到产品，并在*ProductDetails*页上看到产品的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e4005-108">After completing this tutorial, you'll see products on the *ProductsList.aspx* page and a product's details on the *ProductDetails.aspx* page.</span></span>

## <a name="youll-learn-how-to"></a><span data-ttu-id="e4005-109">你将了解如何：</span><span class="sxs-lookup"><span data-stu-id="e4005-109">You'll learn how to:</span></span>

- <span data-ttu-id="e4005-110">添加数据控件以显示数据库中的产品</span><span class="sxs-lookup"><span data-stu-id="e4005-110">Add a data control to display products from the database</span></span>
- <span data-ttu-id="e4005-111">将数据控件连接到所选数据</span><span class="sxs-lookup"><span data-stu-id="e4005-111">Connect a data control to the selected data</span></span>
- <span data-ttu-id="e4005-112">添加数据控件以显示数据库中的产品详细信息</span><span class="sxs-lookup"><span data-stu-id="e4005-112">Add a data control to display product details from the database</span></span>
- <span data-ttu-id="e4005-113">从查询字符串中检索值，并使用该值来限制从数据库检索的数据。</span><span class="sxs-lookup"><span data-stu-id="e4005-113">Retrieve a value from the query string and use that value to limit the data that's retrieved from the database</span></span>

### <a name="features-introduced-in-this-tutorial"></a><span data-ttu-id="e4005-114">本教程中引入的功能：</span><span class="sxs-lookup"><span data-stu-id="e4005-114">Features introduced in this tutorial:</span></span>

- <span data-ttu-id="e4005-115">模型绑定</span><span class="sxs-lookup"><span data-stu-id="e4005-115">Model binding</span></span>
- <span data-ttu-id="e4005-116">值提供程序</span><span class="sxs-lookup"><span data-stu-id="e4005-116">Value providers</span></span>

## <a name="add-a-data-control"></a><span data-ttu-id="e4005-117">添加数据控件</span><span class="sxs-lookup"><span data-stu-id="e4005-117">Add a data control</span></span>

<span data-ttu-id="e4005-118">您可以使用几个不同的选项将数据绑定到服务器控件。</span><span class="sxs-lookup"><span data-stu-id="e4005-118">You can use a few different options to bind data to a server control.</span></span> <span data-ttu-id="e4005-119">最常见的包括：</span><span class="sxs-lookup"><span data-stu-id="e4005-119">The most common include:</span></span>

* <span data-ttu-id="e4005-120">添加数据源控件</span><span class="sxs-lookup"><span data-stu-id="e4005-120">Adding a data source control</span></span>
* <span data-ttu-id="e4005-121">手动添加代码</span><span class="sxs-lookup"><span data-stu-id="e4005-121">Adding code by hand</span></span>
* <span data-ttu-id="e4005-122">使用模型绑定</span><span class="sxs-lookup"><span data-stu-id="e4005-122">Using model binding</span></span>

### <a name="use-a-data-source-control-to-bind-data"></a><span data-ttu-id="e4005-123">使用数据源控件绑定数据</span><span class="sxs-lookup"><span data-stu-id="e4005-123">Use a data source control to bind data</span></span>

<span data-ttu-id="e4005-124">通过添加数据源控件，可以将数据源控件链接到显示数据的控件。</span><span class="sxs-lookup"><span data-stu-id="e4005-124">Adding a data source control allows you to link the data source control to the control that displays the data.</span></span> <span data-ttu-id="e4005-125">利用此方法，你可以通过声明方式（而不是以编程方式）将服务器端控件连接到数据源。</span><span class="sxs-lookup"><span data-stu-id="e4005-125">With this approach, you can declaratively,  rather than programmatically, connect server-side controls to data sources.</span></span>

### <a name="code-by-hand-to-bind-data"></a><span data-ttu-id="e4005-126">手动绑定数据的代码</span><span class="sxs-lookup"><span data-stu-id="e4005-126">Code by hand to bind data</span></span>

<span data-ttu-id="e4005-127">手动编码涉及：</span><span class="sxs-lookup"><span data-stu-id="e4005-127">Coding by hand involves:</span></span>

1. <span data-ttu-id="e4005-128">读取值</span><span class="sxs-lookup"><span data-stu-id="e4005-128">Reading a value</span></span>
2. <span data-ttu-id="e4005-129">检查其是否为 null</span><span class="sxs-lookup"><span data-stu-id="e4005-129">Checking if it's null</span></span>
3. <span data-ttu-id="e4005-130">将其转换为适当的类型</span><span class="sxs-lookup"><span data-stu-id="e4005-130">Converting it to an appropriate type</span></span>
4. <span data-ttu-id="e4005-131">检查转换是否成功</span><span class="sxs-lookup"><span data-stu-id="e4005-131">Checking conversion success</span></span>
5. <span data-ttu-id="e4005-132">在查询中使用值</span><span class="sxs-lookup"><span data-stu-id="e4005-132">Using the value in the query</span></span> 

<span data-ttu-id="e4005-133">利用此方法，您可以完全控制数据访问逻辑。</span><span class="sxs-lookup"><span data-stu-id="e4005-133">This approach lets you have full control over your data-access logic.</span></span>

### <a name="use-model-binding-to-bind-data"></a><span data-ttu-id="e4005-134">使用模型绑定来绑定数据</span><span class="sxs-lookup"><span data-stu-id="e4005-134">Use model binding to bind data</span></span>

<span data-ttu-id="e4005-135">模型绑定使你可以使用更少的代码绑定结果，并使你能够在整个应用程序中重复使用该功能。</span><span class="sxs-lookup"><span data-stu-id="e4005-135">Model binding lets you bind results with far less code and gives you the ability to reuse the functionality throughout your application.</span></span> <span data-ttu-id="e4005-136">它简化了使用以代码为中心的数据访问逻辑，同时还提供丰富的数据绑定框架。</span><span class="sxs-lookup"><span data-stu-id="e4005-136">It simplifies working with code-focused data-access logic while still providing a rich, data-binding framework.</span></span>

## <a name="display-products"></a><span data-ttu-id="e4005-137">显示产品</span><span class="sxs-lookup"><span data-stu-id="e4005-137">Display products</span></span>

<span data-ttu-id="e4005-138">在本教程中，您将使用模型绑定来绑定数据。</span><span class="sxs-lookup"><span data-stu-id="e4005-138">In this tutorial, you'll use model binding to bind data.</span></span> <span data-ttu-id="e4005-139">若要将数据控件配置为使用模型绑定来选择数据，请将控件的 `SelectMethod` 属性设置为该页的代码中的方法名称。</span><span class="sxs-lookup"><span data-stu-id="e4005-139">To configure a data control to use model binding to select data, you set the control's `SelectMethod` property to a method name in the page's code.</span></span> <span data-ttu-id="e4005-140">数据控件在页面生命周期中的适当时间调用方法，并自动绑定返回的数据。</span><span class="sxs-lookup"><span data-stu-id="e4005-140">The data control calls the method at the appropriate time in the page life cycle and automatically binds the returned data.</span></span> <span data-ttu-id="e4005-141">无需显式调用 `DataBind` 方法。</span><span class="sxs-lookup"><span data-stu-id="e4005-141">There's no need to explicitly call the `DataBind` method.</span></span>

1. <span data-ttu-id="e4005-142">在**解决方案资源管理器**中，打开*ProductList*。</span><span class="sxs-lookup"><span data-stu-id="e4005-142">In **Solution Explorer**, open *ProductList.aspx*.</span></span>
2. <span data-ttu-id="e4005-143">将现有标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="e4005-143">Replace the existing markup with this markup:</span></span>   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

<span data-ttu-id="e4005-144">此代码使用名为 `productList` 的**ListView**控件显示产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-144">This code uses a **ListView** control named `productList` to display products.</span></span>

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

<span data-ttu-id="e4005-145">对于模板和样式，您可以定义**ListView**控件显示数据的方式。</span><span class="sxs-lookup"><span data-stu-id="e4005-145">With templates and styles, you define how the **ListView** control displays data.</span></span> <span data-ttu-id="e4005-146">这对于任何重复结构中的数据都很有用。</span><span class="sxs-lookup"><span data-stu-id="e4005-146">It's useful for data in any repeating structure.</span></span> <span data-ttu-id="e4005-147">尽管此**ListView**示例只显示数据库数据，但你也可以不使用代码，使用户能够编辑、插入和删除数据，以及对数据进行排序和分页。</span><span class="sxs-lookup"><span data-stu-id="e4005-147">Though this **ListView** example simply displays database data, you can also, without code, enable users to edit, insert, and delete data, and to sort and page data.</span></span>

<span data-ttu-id="e4005-148">通过设置**ListView**控件中的 `ItemType` 属性，可使用数据绑定表达式 `Item` 并且控件成为强类型。</span><span class="sxs-lookup"><span data-stu-id="e4005-148">By setting the `ItemType` property in the **ListView** control, the data-binding expression `Item` is available and the control becomes strongly typed.</span></span> <span data-ttu-id="e4005-149">如前面的教程中所述，可以通过 IntelliSense 选择项对象详细信息，如指定 `ProductName`：</span><span class="sxs-lookup"><span data-stu-id="e4005-149">As mentioned in the previous tutorial, you can select Item object details with IntelliSense, such as specifying the `ProductName`:</span></span>

![显示数据项和详细信息-IntelliSense](display_data_items_and_details/_static/image1.png)

<span data-ttu-id="e4005-151">你还可以使用模型绑定来指定 `SelectMethod` 值。</span><span class="sxs-lookup"><span data-stu-id="e4005-151">You're also using model binding to specify a `SelectMethod` value.</span></span> <span data-ttu-id="e4005-152">此值（`GetProducts`）对应于要在下一步中向隐藏的代码中添加的方法。</span><span class="sxs-lookup"><span data-stu-id="e4005-152">This value (`GetProducts`) corresponds to the method you'll add to the code behind to display products in the next step.</span></span>

### <a name="add-code-to-display-products"></a><span data-ttu-id="e4005-153">添加用于显示产品的代码</span><span class="sxs-lookup"><span data-stu-id="e4005-153">Add code to display products</span></span>

<span data-ttu-id="e4005-154">在此步骤中，你将添加代码，以便用数据库中的产品数据填充**ListView**控件。</span><span class="sxs-lookup"><span data-stu-id="e4005-154">In this step, you'll add code to populate the **ListView** control with product data from the database.</span></span> <span data-ttu-id="e4005-155">此代码支持显示所有产品和单个类别的产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-155">The code supports showing all products and  individual category products.</span></span>

1. <span data-ttu-id="e4005-156">在**解决方案资源管理器**中，右键单击*ProductList* ，然后选择 "**查看代码**"。</span><span class="sxs-lookup"><span data-stu-id="e4005-156">In **Solution Explorer**, right-click *ProductList.aspx* and then select **View Code**.</span></span>
2. <span data-ttu-id="e4005-157">将*ProductList.aspx.cs*文件中的现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e4005-157">Replace the existing code in the *ProductList.aspx.cs* file with this:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

<span data-ttu-id="e4005-158">此代码显示**ListView**控件的 `ItemType` 属性在*ProductList*页中引用的 `GetProducts` 方法。</span><span class="sxs-lookup"><span data-stu-id="e4005-158">This code shows the `GetProducts` method that the **ListView** control's `ItemType` property references in the *ProductList.aspx* page.</span></span> <span data-ttu-id="e4005-159">若要将结果限制为特定的数据库类别，代码在导航到*ProductList*页面时，将设置传递到*ProductList*页的查询字符串值中的 `categoryId` 值。</span><span class="sxs-lookup"><span data-stu-id="e4005-159">To limit the results to a specific database category, the code sets the `categoryId` value from the query string value passed to the *ProductList.aspx* page when the *ProductList.aspx* page is navigated to.</span></span> <span data-ttu-id="e4005-160">`System.Web.ModelBinding` 命名空间中的 `QueryStringAttribute` 类用于检索 `id`的查询字符串变量的值。</span><span class="sxs-lookup"><span data-stu-id="e4005-160">The `QueryStringAttribute` class in the `System.Web.ModelBinding` namespace is used to retrieve the value of the query string variable `id`.</span></span> <span data-ttu-id="e4005-161">这将指示模型绑定在运行时尝试将值从查询字符串绑定到 `categoryId` 参数。</span><span class="sxs-lookup"><span data-stu-id="e4005-161">This instructs model binding to try to bind a value from the query string to the `categoryId` parameter at run time.</span></span>

<span data-ttu-id="e4005-162">当有效类别作为查询字符串传递到页面时，查询的结果将限于数据库中与 `categoryId` 值匹配的那些产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-162">When a valid category is passed as a query string to the page, the results of the query are limited to those products in the database that match the `categoryId` value.</span></span> <span data-ttu-id="e4005-163">例如，如果*ProductsList*页 URL 如下所示：</span><span class="sxs-lookup"><span data-stu-id="e4005-163">For instance, if the *ProductsList.aspx* page URL is this:</span></span>

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

<span data-ttu-id="e4005-164">页面仅显示 `categoryId` 等于 `1`的产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-164">The page displays only the products where the `categoryId` equals `1`.</span></span>

<span data-ttu-id="e4005-165">如果调用*ProductList*页时未包含任何查询字符串，则会显示所有产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-165">All products are displayed if no query string is included when the *ProductList.aspx* page is called.</span></span>

<span data-ttu-id="e4005-166">这些方法的值的源称为*值提供程序*（如*QueryString*），参数属性指示要使用的值提供程序的*属性*（如 `id`）。</span><span class="sxs-lookup"><span data-stu-id="e4005-166">The sources of values for these methods are referred to as *value providers* (such as *QueryString*), and the parameter attributes that indicate which value provider to use are referred to as *value provider attributes* (such as `id`).</span></span> <span data-ttu-id="e4005-167">ASP.NET 包括 Web 窗体应用程序中的所有典型用户输入源的值提供程序和相应属性，例如查询字符串、cookie、窗体值、控件、视图状态、会话状态和配置文件属性。</span><span class="sxs-lookup"><span data-stu-id="e4005-167">ASP.NET includes value providers and corresponding attributes for all of the typical sources of user input in a Web Forms application such as the query string, cookies, form values, controls, view state, session state, and profile properties.</span></span> <span data-ttu-id="e4005-168">你还可以编写自定义值提供程序。</span><span class="sxs-lookup"><span data-stu-id="e4005-168">You can also write custom value providers.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="e4005-169">运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="e4005-169">Run the application</span></span>

<span data-ttu-id="e4005-170">立即运行应用程序以查看所有产品或类别的产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-170">Run the application now to view all products or a category's products.</span></span>

1. <span data-ttu-id="e4005-171">在 Visual Studio 中按**F5**运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4005-171">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="e4005-172">浏览器将打开并显示*default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="e4005-172">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="e4005-173">从 "产品类别导航" 菜单中选择 "**汽车**"。</span><span class="sxs-lookup"><span data-stu-id="e4005-173">Select **Cars** from the product category navigation menu.</span></span>  
   <span data-ttu-id="e4005-174">*ProductList*页仅显示**汽车**类别产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-174">The *ProductList.aspx* page displays showing only **Cars** category products.</span></span> <span data-ttu-id="e4005-175">在本教程的后面部分中，将显示产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="e4005-175">Later in this tutorial, you'll display product details.</span></span>  

    ![显示数据项和详细信息-汽车](display_data_items_and_details/_static/image2.png)

3. <span data-ttu-id="e4005-177">在顶部的导航菜单中选择 "**产品**"。</span><span class="sxs-lookup"><span data-stu-id="e4005-177">Select **Products** from the navigation menu at the top.</span></span>  
   <span data-ttu-id="e4005-178">同样，将显示 " *ProductList* " 页，但这次它显示产品的整个列表。</span><span class="sxs-lookup"><span data-stu-id="e4005-178">Again, the *ProductList.aspx* page is displayed, however this time it shows the entire list of products.</span></span>   

    ![显示数据项和详细信息-产品](display_data_items_and_details/_static/image3.png)

4. <span data-ttu-id="e4005-180">关闭浏览器并返回到 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e4005-180">Close the browser and return to Visual Studio.</span></span>

### <a name="add-a-data-control-to-display-product-details"></a><span data-ttu-id="e4005-181">添加数据控件以显示产品详细信息</span><span class="sxs-lookup"><span data-stu-id="e4005-181">Add a data control to display product details</span></span>

<span data-ttu-id="e4005-182">接下来，您将修改在上一教程中添加的*ProductDetails*页面中的标记，以显示特定的产品信息。</span><span class="sxs-lookup"><span data-stu-id="e4005-182">Next, you'll modify the markup in the *ProductDetails.aspx* page that you added in the previous tutorial to display specific product information.</span></span>

1. <span data-ttu-id="e4005-183">在**解决方案资源管理器**中，打开*ProductDetails*。</span><span class="sxs-lookup"><span data-stu-id="e4005-183">In **Solution Explorer**, open *ProductDetails.aspx*.</span></span>

2. <span data-ttu-id="e4005-184">将现有标记替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="e4005-184">Replace the existing markup with this markup:</span></span>

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    <span data-ttu-id="e4005-185">此代码使用**FormView**控件显示特定产品的详细信息。</span><span class="sxs-lookup"><span data-stu-id="e4005-185">This code uses a **FormView** control to display specific product details.</span></span> <span data-ttu-id="e4005-186">此标记使用方法，如用于在*ProductList*页中显示数据的方法。</span><span class="sxs-lookup"><span data-stu-id="e4005-186">This markup uses methods like the methods used to display data in the *ProductList.aspx* page.</span></span> <span data-ttu-id="e4005-187">**FormView**控件用于从数据源一次显示一条记录。</span><span class="sxs-lookup"><span data-stu-id="e4005-187">The **FormView** control is used to display a single record at a time from a data source.</span></span> <span data-ttu-id="e4005-188">使用**FormView**控件时，可以创建模板来显示和编辑数据绑定值。</span><span class="sxs-lookup"><span data-stu-id="e4005-188">When you use the **FormView** control, you create templates to display and edit data-bound values.</span></span> <span data-ttu-id="e4005-189">这些模板包含定义窗体外观和功能的控件、绑定表达式和格式设置。</span><span class="sxs-lookup"><span data-stu-id="e4005-189">These templates contain controls, binding expressions, and formatting that define the form's look and functionality.</span></span>

<span data-ttu-id="e4005-190">将以前的标记连接到数据库需要其他代码。</span><span class="sxs-lookup"><span data-stu-id="e4005-190">Connecting the previous markup to the database requires additional code.</span></span>

1. <span data-ttu-id="e4005-191">在**解决方案资源管理器**中，右键单击*ProductDetails* ，然后单击 "**查看代码**"。</span><span class="sxs-lookup"><span data-stu-id="e4005-191">In **Solution Explorer**, right-click *ProductDetails.aspx* and then click **View Code**.</span></span>  
   <span data-ttu-id="e4005-192">将显示*ProductDetails.aspx.cs*文件。</span><span class="sxs-lookup"><span data-stu-id="e4005-192">The *ProductDetails.aspx.cs* file is displayed.</span></span>

2. <span data-ttu-id="e4005-193">将现有代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e4005-193">Replace the existing code with this code:</span></span>   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

<span data-ttu-id="e4005-194">此代码检查 "`productID`" 查询字符串值。</span><span class="sxs-lookup"><span data-stu-id="e4005-194">This code checks for a "`productID`" query-string value.</span></span> <span data-ttu-id="e4005-195">如果找到有效的查询字符串值，将显示匹配的产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-195">If a valid query-string value is found, the matching product is displayed.</span></span> <span data-ttu-id="e4005-196">如果找不到该查询字符串，或者其值无效，则不会显示任何产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-196">If the query-string isn't found, or its value isn't valid, no product is displayed.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="e4005-197">运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="e4005-197">Run the application</span></span>

<span data-ttu-id="e4005-198">现在可以运行应用程序，以查看基于产品 ID 显示的单个产品。</span><span class="sxs-lookup"><span data-stu-id="e4005-198">Now you can run the application to see an individual product displayed based on product ID.</span></span>

1. <span data-ttu-id="e4005-199">在 Visual Studio 中按**F5**运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="e4005-199">Press **F5** while in Visual Studio to run the application.</span></span>  
   <span data-ttu-id="e4005-200">浏览器将打开并显示*default.aspx*页。</span><span class="sxs-lookup"><span data-stu-id="e4005-200">The browser opens and shows the *Default.aspx* page.</span></span>

2. <span data-ttu-id="e4005-201">从类别导航菜单中选择 " **Boats** "。</span><span class="sxs-lookup"><span data-stu-id="e4005-201">Select **Boats** from the category navigation menu.</span></span>  
   <span data-ttu-id="e4005-202">将显示*ProductList*页。</span><span class="sxs-lookup"><span data-stu-id="e4005-202">The *ProductList.aspx* page is displayed.</span></span>

3. <span data-ttu-id="e4005-203">从产品列表中选择 "**纸张船**"。</span><span class="sxs-lookup"><span data-stu-id="e4005-203">Select **Paper Boat** from the product list.</span></span>
   <span data-ttu-id="e4005-204">将显示*ProductDetails*页。</span><span class="sxs-lookup"><span data-stu-id="e4005-204">The *ProductDetails.aspx* page is displayed.</span></span>

    ![显示数据项和详细信息-产品](display_data_items_and_details/_static/image4.png)
    
4. <span data-ttu-id="e4005-206">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="e4005-206">Close the browser.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e4005-207">其他资源</span><span class="sxs-lookup"><span data-stu-id="e4005-207">Additional resources</span></span>

[<span data-ttu-id="e4005-208">通过模型绑定和 web 窗体检索和显示数据</span><span class="sxs-lookup"><span data-stu-id="e4005-208">Retrieving and displaying data with model binding and web forms</span></span>](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a><span data-ttu-id="e4005-209">后续步骤</span><span class="sxs-lookup"><span data-stu-id="e4005-209">Next steps</span></span>

<span data-ttu-id="e4005-210">在本教程中，你添加了标记和代码以显示产品和产品详细信息。</span><span class="sxs-lookup"><span data-stu-id="e4005-210">In this tutorial, you added markup and code to display products and product details.</span></span> <span data-ttu-id="e4005-211">已了解强类型化数据控件、模型绑定和值提供程序。</span><span class="sxs-lookup"><span data-stu-id="e4005-211">You learned about strongly typed data controls, model binding, and value providers.</span></span> <span data-ttu-id="e4005-212">在下一教程中，你将向 Wingtip 玩具示例应用程序添加购物车。</span><span class="sxs-lookup"><span data-stu-id="e4005-212">In the next tutorial, you'll add a shopping cart to the Wingtip Toys sample application.</span></span> 

> [!div class="step-by-step"]
> <span data-ttu-id="e4005-213">[上一页](ui_and_navigation.md)
> [下一页](shopping-cart.md)</span><span class="sxs-lookup"><span data-stu-id="e4005-213">[Previous](ui_and_navigation.md)
[Next](shopping-cart.md)</span></span>
