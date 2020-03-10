---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 第9部分：注册和签出 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第9部分涵盖注册和签出。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450896"
---
# <a name="part-9-registration-and-checkout"></a><span data-ttu-id="aad42-104">第9部分：注册和签出</span><span class="sxs-lookup"><span data-stu-id="aad42-104">Part 9: Registration and Checkout</span></span>

<span data-ttu-id="aad42-105">作者： [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="aad42-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="aad42-106">MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。</span><span class="sxs-lookup"><span data-stu-id="aad42-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="aad42-107">MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。</span><span class="sxs-lookup"><span data-stu-id="aad42-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="aad42-108">本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="aad42-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="aad42-109">第9部分涵盖注册和签出。</span><span class="sxs-lookup"><span data-stu-id="aad42-109">Part 9 covers Registration and Checkout.</span></span>

<span data-ttu-id="aad42-110">在本部分中，我们将创建一个 CheckoutController，它将收集购物者的地址和付款信息。</span><span class="sxs-lookup"><span data-stu-id="aad42-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="aad42-111">我们会要求用户在签出之前向我们的站点注册，因此此控制器需要授权。</span><span class="sxs-lookup"><span data-stu-id="aad42-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="aad42-112">用户通过单击 "结帐" 按钮，导航到其购物车中的结帐过程。</span><span class="sxs-lookup"><span data-stu-id="aad42-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="aad42-113">如果用户未登录，系统会提示用户登录。</span><span class="sxs-lookup"><span data-stu-id="aad42-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="aad42-114">成功登录后，用户将显示在 "地址" 和 "付款" 视图中。</span><span class="sxs-lookup"><span data-stu-id="aad42-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="aad42-115">一旦用户填写了窗体并提交了订单后，它们就会显示在 "订单确认" 屏幕中。</span><span class="sxs-lookup"><span data-stu-id="aad42-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="aad42-116">如果尝试查看不存在的订单或不属于您的订单，则将显示 "错误" 视图。</span><span class="sxs-lookup"><span data-stu-id="aad42-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="aad42-117">迁移购物车</span><span class="sxs-lookup"><span data-stu-id="aad42-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="aad42-118">尽管购物过程是匿名的，但当用户单击 "签出" 按钮时，他们将需要注册并登录。</span><span class="sxs-lookup"><span data-stu-id="aad42-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="aad42-119">用户将希望在访问之间维护购物车信息，因此，在他们完成注册或登录时，我们需要将购物车信息与用户关联。</span><span class="sxs-lookup"><span data-stu-id="aad42-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="aad42-120">这实际上非常简单，因为我们的 ShoppingCart 类已经有了一个方法，该方法将当前购物车中的所有项与用户名相关联。</span><span class="sxs-lookup"><span data-stu-id="aad42-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="aad42-121">当用户完成注册或登录时，只需调用此方法。</span><span class="sxs-lookup"><span data-stu-id="aad42-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="aad42-122">打开我们设置成员身份和授权时添加的**AccountController**类。</span><span class="sxs-lookup"><span data-stu-id="aad42-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="aad42-123">添加一个引用 MvcMusicStore 的 using 语句，然后添加以下 MigrateShoppingCart 方法：</span><span class="sxs-lookup"><span data-stu-id="aad42-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="aad42-124">接下来，请修改登录后操作，以便在验证用户后调用 MigrateShoppingCart，如下所示：</span><span class="sxs-lookup"><span data-stu-id="aad42-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="aad42-125">成功创建用户帐户后，立即对注册 post 操作进行相同的更改：</span><span class="sxs-lookup"><span data-stu-id="aad42-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="aad42-126">这就是，在成功注册或登录时，匿名购物车会自动转移到用户帐户。</span><span class="sxs-lookup"><span data-stu-id="aad42-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="aad42-127">创建 CheckoutController</span><span class="sxs-lookup"><span data-stu-id="aad42-127">Creating the CheckoutController</span></span>

<span data-ttu-id="aad42-128">右键单击 "控制器" 文件夹，并使用空的控制器模板将新的控制器添加到名为 CheckoutController 的项目。</span><span class="sxs-lookup"><span data-stu-id="aad42-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="aad42-129">首先，将授权属性添加到控制器类声明之上，要求用户在签出之前注册：</span><span class="sxs-lookup"><span data-stu-id="aad42-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="aad42-130">*注意：这与之前对 StoreManagerController 进行的更改类似，但在这种情况下，授权属性要求用户是管理员角色。在签出控制器中，我们要求用户登录，但不要求用户是管理员。*</span><span class="sxs-lookup"><span data-stu-id="aad42-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="aad42-131">为了简单起见，我们不会在本教程中处理支付信息。</span><span class="sxs-lookup"><span data-stu-id="aad42-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="aad42-132">相反，我们允许用户使用促销代码签出。</span><span class="sxs-lookup"><span data-stu-id="aad42-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="aad42-133">我们将使用名为 PromoCode 的常量存储此促销代码。</span><span class="sxs-lookup"><span data-stu-id="aad42-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="aad42-134">与在 StoreController 中一样，我们将声明一个字段来保存名为 storeDB 的 MusicStoreEntities 类的实例。</span><span class="sxs-lookup"><span data-stu-id="aad42-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="aad42-135">若要使用 MusicStoreEntities 类，我们需要为 MvcMusicStore 命名空间添加 using 语句。</span><span class="sxs-lookup"><span data-stu-id="aad42-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="aad42-136">我们的结帐控制器顶部显示在下方。</span><span class="sxs-lookup"><span data-stu-id="aad42-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="aad42-137">CheckoutController 将具有以下控制器操作：</span><span class="sxs-lookup"><span data-stu-id="aad42-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="aad42-138">**AddressAndPayment （GET 方法）** 将显示允许用户输入其信息的窗体。</span><span class="sxs-lookup"><span data-stu-id="aad42-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="aad42-139">**AddressAndPayment （POST 方法）** 将验证输入并处理顺序。</span><span class="sxs-lookup"><span data-stu-id="aad42-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="aad42-140">**完成**后将在用户成功完成签出过程后显示。</span><span class="sxs-lookup"><span data-stu-id="aad42-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="aad42-141">此视图将包含用户的订单号，如 "确认"。</span><span class="sxs-lookup"><span data-stu-id="aad42-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="aad42-142">首先，让我们将索引控制器操作（在我们创建控制器时生成的）重命名为 AddressAndPayment。</span><span class="sxs-lookup"><span data-stu-id="aad42-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="aad42-143">此控制器操作只显示结帐窗体，因此不需要任何模型信息。</span><span class="sxs-lookup"><span data-stu-id="aad42-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="aad42-144">我们的 AddressAndPayment POST 方法将遵循我们在 StoreManagerController 中使用的同一模式：它将尝试接受窗体提交并完成订单，并将在窗体失败时重新显示该窗体。</span><span class="sxs-lookup"><span data-stu-id="aad42-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="aad42-145">验证窗体输入满足对订单的验证要求后，将直接检查 PromoCode 窗体值。</span><span class="sxs-lookup"><span data-stu-id="aad42-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="aad42-146">假设一切正常，我们将按订单保存更新后的信息，告诉 ShoppingCart 对象完成订单过程，然后重定向到完整的操作。</span><span class="sxs-lookup"><span data-stu-id="aad42-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="aad42-147">在成功完成签出过程后，用户将被重定向到 "完成" 控制器操作。</span><span class="sxs-lookup"><span data-stu-id="aad42-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="aad42-148">此操作将执行一个简单的检查，用于验证在将订单号显示为确认之前，该订单确实属于已登录用户。</span><span class="sxs-lookup"><span data-stu-id="aad42-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="aad42-149">*注意：当我们开始项目时，会在/Views/Shared 文件夹中自动创建错误视图。*</span><span class="sxs-lookup"><span data-stu-id="aad42-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="aad42-150">完整的 CheckoutController 代码如下所示：</span><span class="sxs-lookup"><span data-stu-id="aad42-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="aad42-151">添加 AddressAndPayment 视图</span><span class="sxs-lookup"><span data-stu-id="aad42-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="aad42-152">现在，让我们创建 AddressAndPayment 视图。</span><span class="sxs-lookup"><span data-stu-id="aad42-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="aad42-153">右键单击其中一个 AddressAndPayment 控制器操作，并添加一个名为 AddressAndPayment 的视图，该视图的类型为 "按顺序强类型" 并使用 "编辑模板"，如下所示。</span><span class="sxs-lookup"><span data-stu-id="aad42-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="aad42-154">此视图将使用我们在生成 StoreManagerEdit 视图时查看的两种技术：</span><span class="sxs-lookup"><span data-stu-id="aad42-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="aad42-155">我们将使用 EditorForModel （）显示订单模型的窗体字段</span><span class="sxs-lookup"><span data-stu-id="aad42-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="aad42-156">我们将使用具有验证特性的 Order 类的验证规则</span><span class="sxs-lookup"><span data-stu-id="aad42-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="aad42-157">首先，我们将更新窗体代码以使用 EditorForModel （），后跟促销代码的一个文本框。</span><span class="sxs-lookup"><span data-stu-id="aad42-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="aad42-158">AddressAndPayment 视图的完整代码如下所示。</span><span class="sxs-lookup"><span data-stu-id="aad42-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="aad42-159">为订单定义验证规则</span><span class="sxs-lookup"><span data-stu-id="aad42-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="aad42-160">现在，我们已设置了视图，我们将为订单模型设置验证规则，就像我们先前针对唱片集模型进行的一样。</span><span class="sxs-lookup"><span data-stu-id="aad42-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="aad42-161">右键单击 "模型" 文件夹，然后添加一个名为 Order 的类。</span><span class="sxs-lookup"><span data-stu-id="aad42-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="aad42-162">除了之前用于唱片集的验证属性，我们还将使用正则表达式来验证用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="aad42-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="aad42-163">如果尝试提交缺少或无效信息的窗体，现在将使用客户端验证显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="aad42-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="aad42-164">好了，我们已完成了结帐过程的大部分硬性工作;我们只会有几个机会，最后结束。</span><span class="sxs-lookup"><span data-stu-id="aad42-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="aad42-165">我们需要添加两个简单的视图，在登录过程中，我们需要负责交付购物车信息。</span><span class="sxs-lookup"><span data-stu-id="aad42-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="aad42-166">添加结帐完成视图</span><span class="sxs-lookup"><span data-stu-id="aad42-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="aad42-167">"结帐完成" 视图非常简单，因为它只需显示订单 ID。</span><span class="sxs-lookup"><span data-stu-id="aad42-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="aad42-168">右键单击 "完成控制器" 操作并添加一个名为 Complete 的视图，该视图的类型为 int。</span><span class="sxs-lookup"><span data-stu-id="aad42-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="aad42-169">现在，我们将更新视图代码以显示订单 ID，如下所示。</span><span class="sxs-lookup"><span data-stu-id="aad42-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="aad42-170">正在更新错误视图</span><span class="sxs-lookup"><span data-stu-id="aad42-170">Updating The Error view</span></span>

<span data-ttu-id="aad42-171">默认模板在 "共享视图" 文件夹中包含错误视图，以便可以将其重新用于站点中的其他位置。</span><span class="sxs-lookup"><span data-stu-id="aad42-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="aad42-172">此错误视图包含一个非常简单的错误，不会使用我们的站点布局，因此我们将对其进行更新。</span><span class="sxs-lookup"><span data-stu-id="aad42-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="aad42-173">由于这是一个一般错误页面，因此内容非常简单。</span><span class="sxs-lookup"><span data-stu-id="aad42-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="aad42-174">如果用户想要重新尝试操作，我们将包含一条消息和一个导航到历史记录中的上一页的链接。</span><span class="sxs-lookup"><span data-stu-id="aad42-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> <span data-ttu-id="aad42-175">[上一页](mvc-music-store-part-8.md)
> [下一页](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="aad42-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>
