---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 第5部分：业务逻辑 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第5部分添加了一些业务逻辑。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511544"
---
# <a name="part-5-business-logic"></a><span data-ttu-id="930e2-104">第5部分：业务逻辑</span><span class="sxs-lookup"><span data-stu-id="930e2-104">Part 5: Business Logic</span></span>

<span data-ttu-id="930e2-105">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="930e2-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="930e2-106">Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。</span><span class="sxs-lookup"><span data-stu-id="930e2-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="930e2-107">其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="930e2-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="930e2-108">本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="930e2-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="930e2-109">第5部分添加了一些业务逻辑。</span><span class="sxs-lookup"><span data-stu-id="930e2-109">Part 5 adds some business logic.</span></span>

## <a id="_Toc260221671"></a><span data-ttu-id="930e2-110">添加一些业务逻辑</span><span class="sxs-lookup"><span data-stu-id="930e2-110">Adding Some Business Logic</span></span>

<span data-ttu-id="930e2-111">每次访问我们的网站时，我们都希望获得购物体验。</span><span class="sxs-lookup"><span data-stu-id="930e2-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="930e2-112">即使用户没有注册或登录，访问者也可以浏览和添加购物车中的商品。</span><span class="sxs-lookup"><span data-stu-id="930e2-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="930e2-113">当他们准备好签出时，会向他们提供身份验证选项，以及他们是否还可以创建帐户的成员。</span><span class="sxs-lookup"><span data-stu-id="930e2-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="930e2-114">这意味着，我们需要实施逻辑，将购物车从匿名状态转换为 "已注册用户" 状态。</span><span class="sxs-lookup"><span data-stu-id="930e2-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="930e2-115">让我们创建一个名为 "类" 的目录，然后右键单击该文件夹，然后创建一个名为 MyShoppingCart.cs 的新 "类" 文件。</span><span class="sxs-lookup"><span data-stu-id="930e2-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="930e2-116">如前文所述，我们将扩展实现 MyShoppingCart 页的类，并且我们将使用来实现此目的。网络强大的 "分部类" 构造。</span><span class="sxs-lookup"><span data-stu-id="930e2-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="930e2-117">MyShoppingCart.aspx.cf 文件的生成调用如下所示。</span><span class="sxs-lookup"><span data-stu-id="930e2-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="930e2-118">请注意 "partial" 关键字的使用。</span><span class="sxs-lookup"><span data-stu-id="930e2-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="930e2-119">我们刚刚生成的类文件如下所示。</span><span class="sxs-lookup"><span data-stu-id="930e2-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="930e2-120">我们还会通过向此文件添加 partial 关键字来合并实现。</span><span class="sxs-lookup"><span data-stu-id="930e2-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="930e2-121">新类文件现在如下所示。</span><span class="sxs-lookup"><span data-stu-id="930e2-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="930e2-122">我们将向类添加的第一种方法是 "AddItem" 方法。</span><span class="sxs-lookup"><span data-stu-id="930e2-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="930e2-123">当用户单击产品列表和产品详细信息页上的 "添加到图片" 链接时，将最终调用此方法。</span><span class="sxs-lookup"><span data-stu-id="930e2-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="930e2-124">将以下附加到页面顶部的 using 语句。</span><span class="sxs-lookup"><span data-stu-id="930e2-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="930e2-125">并将此方法添加到 MyShoppingCart 类。</span><span class="sxs-lookup"><span data-stu-id="930e2-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="930e2-126">我们使用 LINQ to Entities 来查看物品是否已在购物车中。</span><span class="sxs-lookup"><span data-stu-id="930e2-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="930e2-127">如果是这样，我们将更新该项的订单数量，否则，将为所选项创建一个新项</span><span class="sxs-lookup"><span data-stu-id="930e2-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="930e2-128">为了调用此方法，我们将实现一个 AddToCart 页，该页面不仅类此方法，还在添加项后显示当前购物 = 购物车。</span><span class="sxs-lookup"><span data-stu-id="930e2-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="930e2-129">在解决方案资源管理器中右键单击解决方案名称，然后添加名为 AddToCart 的新页，如前文所述。</span><span class="sxs-lookup"><span data-stu-id="930e2-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="930e2-130">尽管我们可以使用此页来显示中期问题（如低股票问题），但在我们的实现中，该页面不会实际呈现，而是调用 "添加" 逻辑并重定向。</span><span class="sxs-lookup"><span data-stu-id="930e2-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="930e2-131">若要实现此目的，我们需要将以下代码添加到页面\_Load 事件。</span><span class="sxs-lookup"><span data-stu-id="930e2-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="930e2-132">请注意，我们正在检索从 QueryString 参数添加到购物车中的产品，并调用我们的类的 AddItem 方法。</span><span class="sxs-lookup"><span data-stu-id="930e2-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="930e2-133">假设没有遇到任何错误，则会将控制传递到 SHoppingCart 页，我们将在下一步完成此页。</span><span class="sxs-lookup"><span data-stu-id="930e2-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="930e2-134">如果应出现错误，则会引发异常。</span><span class="sxs-lookup"><span data-stu-id="930e2-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="930e2-135">当前我们尚未实现全局错误处理程序，因此，我们的应用程序无法处理此异常，我们稍后将对此进行更正。</span><span class="sxs-lookup"><span data-stu-id="930e2-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="930e2-136">另请注意，使用语句 Debug。 Fail （）（可通过 `using System.Diagnostics;)`</span><span class="sxs-lookup"><span data-stu-id="930e2-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="930e2-137">当应用程序在调试器中运行时，此方法将显示一个详细的对话框，其中包含有关应用程序状态的信息以及我们指定的错误消息。</span><span class="sxs-lookup"><span data-stu-id="930e2-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="930e2-138">在生产环境中运行时，将忽略 Debug （）语句。</span><span class="sxs-lookup"><span data-stu-id="930e2-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="930e2-139">在上面的代码中，你会注意到，在调用购物车类名称 "GetShoppingCartId" 中的方法。</span><span class="sxs-lookup"><span data-stu-id="930e2-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="930e2-140">按如下所示添加代码以实现方法。</span><span class="sxs-lookup"><span data-stu-id="930e2-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="930e2-141">请注意，我们还添加了 "更新" 和 "签出" 按钮和一个标签，可在其中显示购物车 "总计"。</span><span class="sxs-lookup"><span data-stu-id="930e2-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="930e2-142">现在，我们可以将物品添加到购物车，但我们尚未实施逻辑来在添加产品后显示购物车。</span><span class="sxs-lookup"><span data-stu-id="930e2-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="930e2-143">因此，在 MyShoppingCart 页中，我们将添加一个 EntityDataSource 控件和一个 GridVire 控件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="930e2-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="930e2-144">在设计器中调用窗体，以便您可以双击 "更新购物车" 按钮，然后生成在标记的声明中指定的 click 事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="930e2-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="930e2-145">稍后我们将实现详细信息，但这样做将使我们生成并运行应用程序，而不会发生错误。</span><span class="sxs-lookup"><span data-stu-id="930e2-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="930e2-146">当你运行应用程序并向购物车中添加物品时，你将看到此内容。</span><span class="sxs-lookup"><span data-stu-id="930e2-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="930e2-147">请注意，我们通过实现三个自定义列，遵循了 "默认" 网格显示。</span><span class="sxs-lookup"><span data-stu-id="930e2-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="930e2-148">第一个是用于数量的可编辑的 "绑定" 字段：</span><span class="sxs-lookup"><span data-stu-id="930e2-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="930e2-149">下一列是显示行项总计的 "计算" 列（该项的成本乘以要订购的数量）：</span><span class="sxs-lookup"><span data-stu-id="930e2-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="930e2-150">最后，我们有一个包含 CheckBox 控件的自定义列，用户将使用该复选框控件指示应从购物图表中删除该项。</span><span class="sxs-lookup"><span data-stu-id="930e2-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="930e2-151">如您所见，"订单总计" 行为空，因此让我们添加一些逻辑来计算订单总计。</span><span class="sxs-lookup"><span data-stu-id="930e2-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="930e2-152">首先，将 "GetTotal" 方法部署到我们的 MyShoppingCart 类。</span><span class="sxs-lookup"><span data-stu-id="930e2-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="930e2-153">在 MyShoppingCart.cs 文件中，添加以下代码。</span><span class="sxs-lookup"><span data-stu-id="930e2-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="930e2-154">然后，在页面\_Load 事件处理程序中，我们可以调用 GetTotal 方法。</span><span class="sxs-lookup"><span data-stu-id="930e2-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="930e2-155">同时，我们将添加一个测试来查看购物车是否为空，并在其显示时进行相应调整。</span><span class="sxs-lookup"><span data-stu-id="930e2-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="930e2-156">现在，如果购物车为空，我们将得到以下内容：</span><span class="sxs-lookup"><span data-stu-id="930e2-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="930e2-157">如果不是，我们会看到总数。</span><span class="sxs-lookup"><span data-stu-id="930e2-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="930e2-158">但是，此页面尚未完成。</span><span class="sxs-lookup"><span data-stu-id="930e2-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="930e2-159">我们将需要额外的逻辑来重新计算购物车，方法是删除标记为要删除的项目，并确定新的数量值，因为用户可能在网格中更改了某些值。</span><span class="sxs-lookup"><span data-stu-id="930e2-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="930e2-160">允许在 MyShoppingCart.cs 中将 "RemoveItem" 方法添加到购物车类，以便在用户标记要删除的项时处理案例。</span><span class="sxs-lookup"><span data-stu-id="930e2-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="930e2-161">现在，让我们使用一种方法来处理用户在 GridView 中更改质量时的情况。</span><span class="sxs-lookup"><span data-stu-id="930e2-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="930e2-162">利用基本的 "删除" 和 "更新" 功能，我们可以实现在数据库中实际更新购物车的逻辑。</span><span class="sxs-lookup"><span data-stu-id="930e2-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="930e2-163">（在 MyShoppingCart.cs 中）</span><span class="sxs-lookup"><span data-stu-id="930e2-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="930e2-164">你会注意到，此方法需要两个参数。</span><span class="sxs-lookup"><span data-stu-id="930e2-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="930e2-165">一个是购物车 Id，另一个是用户定义类型的对象数组。</span><span class="sxs-lookup"><span data-stu-id="930e2-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="930e2-166">因此，为了最大限度地减少对用户界面细节的逻辑的依赖关系，我们定义了一种数据结构，可用于在不需要直接访问 GridView 控件的情况下将购物车项传递到代码。</span><span class="sxs-lookup"><span data-stu-id="930e2-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="930e2-167">在我们的 MyShoppingCart.aspx.cs 文件中，可以在 "更新" 按钮单击事件处理程序中使用此结构，如下所示。</span><span class="sxs-lookup"><span data-stu-id="930e2-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="930e2-168">请注意，除更新购物车外，还会更新购物车总计。</span><span class="sxs-lookup"><span data-stu-id="930e2-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="930e2-169">请注意，下面这行代码：</span><span class="sxs-lookup"><span data-stu-id="930e2-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="930e2-170">GetValues （）是一个特殊的 helper 函数，我们将在 MyShoppingCart.aspx.cs 中实现此功能，如下所示。</span><span class="sxs-lookup"><span data-stu-id="930e2-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="930e2-171">这提供了一种方法来访问 GridView 控件中的绑定元素的值。</span><span class="sxs-lookup"><span data-stu-id="930e2-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="930e2-172">由于我们的 "删除项" 复选框控件未绑定，我们将通过 FindControl （）方法对其进行访问。</span><span class="sxs-lookup"><span data-stu-id="930e2-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="930e2-173">在项目开发的此阶段，我们准备好实现结帐过程。</span><span class="sxs-lookup"><span data-stu-id="930e2-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="930e2-174">在执行此操作之前，让我们使用 Visual Studio 生成成员资格数据库，并将用户添加到成员资格存储库中。</span><span class="sxs-lookup"><span data-stu-id="930e2-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="930e2-175">[上一页](tailspin-spyworks-part-4.md)
> [下一页](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="930e2-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>
