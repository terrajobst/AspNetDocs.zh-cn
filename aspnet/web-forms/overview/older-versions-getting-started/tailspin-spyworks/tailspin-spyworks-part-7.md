---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: 第7部分：添加功能 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第7部分添加了其他功能，例如 account 查看 。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521564"
---
# <a name="part-7-adding-features"></a><span data-ttu-id="20876-104">第7部分：添加功能</span><span class="sxs-lookup"><span data-stu-id="20876-104">Part 7: Adding Features</span></span>

<span data-ttu-id="20876-105">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="20876-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="20876-106">Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。</span><span class="sxs-lookup"><span data-stu-id="20876-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="20876-107">其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="20876-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="20876-108">本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="20876-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="20876-109">第7部分添加了其他功能，如帐户查看、产品评论和 "常用项" 和 "还已购买" 用户控件。</span><span class="sxs-lookup"><span data-stu-id="20876-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>

## <a id="_Toc260221673"></a><span data-ttu-id="20876-110">添加功能</span><span class="sxs-lookup"><span data-stu-id="20876-110">Adding Features</span></span>

<span data-ttu-id="20876-111">尽管用户可以浏览我们的目录、将商品放入购物车并完成结帐过程，但我们会提供许多支持功能来改善我们的站点。</span><span class="sxs-lookup"><span data-stu-id="20876-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="20876-112">帐户检查（列出订单并查看详细信息。）</span><span class="sxs-lookup"><span data-stu-id="20876-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="20876-113">向首页添加一些特定于上下文的内容。</span><span class="sxs-lookup"><span data-stu-id="20876-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="20876-114">添加一项功能，让用户查看目录中的产品。</span><span class="sxs-lookup"><span data-stu-id="20876-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="20876-115">创建用户控件以显示常用项，并将该控件置于首页。</span><span class="sxs-lookup"><span data-stu-id="20876-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="20876-116">创建 "也购买" 用户控件，并将其添加到产品详细信息页。</span><span class="sxs-lookup"><span data-stu-id="20876-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="20876-117">添加联系人页。</span><span class="sxs-lookup"><span data-stu-id="20876-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="20876-118">添加 "关于" 页。</span><span class="sxs-lookup"><span data-stu-id="20876-118">Add an About Page.</span></span>
8. <span data-ttu-id="20876-119">全局错误</span><span class="sxs-lookup"><span data-stu-id="20876-119">Global Error</span></span>

## <a id="_Toc260221674"></a><span data-ttu-id="20876-120">帐户检查</span><span class="sxs-lookup"><span data-stu-id="20876-120">Account Review</span></span>

<span data-ttu-id="20876-121">在 "帐户" 文件夹中，创建两个名为 OrderList 的 .aspx 页，另一个名为 OrderDetails</span><span class="sxs-lookup"><span data-stu-id="20876-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="20876-122">OrderList 将像以前一样，充分利用 GridView 和 EntityDataSource 控件。</span><span class="sxs-lookup"><span data-stu-id="20876-122">OrderList.aspx will leverage the GridView and EntityDataSource controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="20876-123">EntityDataSource 从 "订单" 表中选择筛选的 "订单" 表中的记录（请参阅 WhereParameter）。</span><span class="sxs-lookup"><span data-stu-id="20876-123">The EntityDataSource selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="20876-124">另请注意 HyperlinkField 中的以下参数：</span><span class="sxs-lookup"><span data-stu-id="20876-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="20876-125">这些参数指定每个产品的订单详细信息视图的链接，并将 "订单 Id" 字段指定为 OrderDetails 页的 QueryString 参数。</span><span class="sxs-lookup"><span data-stu-id="20876-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a><span data-ttu-id="20876-126">OrderDetails .aspx</span><span class="sxs-lookup"><span data-stu-id="20876-126">OrderDetails.aspx</span></span>

<span data-ttu-id="20876-127">我们将使用 EntityDataSource 控件来访问订单，并使用 FormView 显示订单数据，并使用 GridView 的另一个 EntityDataSource 显示订单的行项。</span><span class="sxs-lookup"><span data-stu-id="20876-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="20876-128">在代码隐藏文件（OrderDetails.aspx.cs）中，我们有两个小部分的内务处理。</span><span class="sxs-lookup"><span data-stu-id="20876-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="20876-129">首先，我们需要确保 OrderDetails 始终获取订单 Id。</span><span class="sxs-lookup"><span data-stu-id="20876-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="20876-130">还需要计算并显示行项的订单总计。</span><span class="sxs-lookup"><span data-stu-id="20876-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a><span data-ttu-id="20876-131">主页</span><span class="sxs-lookup"><span data-stu-id="20876-131">The Home Page</span></span>

<span data-ttu-id="20876-132">让我们在 default.aspx 页中添加一些静态内容。</span><span class="sxs-lookup"><span data-stu-id="20876-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="20876-133">首先，我将创建一个 "Content" 文件夹，并在其中包含 Images 文件夹（并在主页上包含一个要使用的图像）。</span><span class="sxs-lookup"><span data-stu-id="20876-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="20876-134">在 "default.aspx" 页的底部占位符中，添加以下标记。</span><span class="sxs-lookup"><span data-stu-id="20876-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a><span data-ttu-id="20876-135">产品审查</span><span class="sxs-lookup"><span data-stu-id="20876-135">Product Reviews</span></span>

<span data-ttu-id="20876-136">首先，我们将添加一个按钮，其中包含指向表单的链接，可用于输入产品评论。</span><span class="sxs-lookup"><span data-stu-id="20876-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="20876-137">请注意，我们将在查询字符串中传递 ProductID</span><span class="sxs-lookup"><span data-stu-id="20876-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="20876-138">接下来，添加名为 ReviewAdd 的页面</span><span class="sxs-lookup"><span data-stu-id="20876-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="20876-139">此页将使用 ASP.NET AJAX 控件工具包。</span><span class="sxs-lookup"><span data-stu-id="20876-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="20876-140">如果尚未执行此操作，请从[DevExpress](http://devexpress.com/act)下载该工具包，并提供有关设置用于 Visual Studio 的工具包的指南[https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)。</span><span class="sxs-lookup"><span data-stu-id="20876-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="20876-141">在设计模式下，从 "工具箱" 中拖动控件和验证器，然后生成如下所示的窗体。</span><span class="sxs-lookup"><span data-stu-id="20876-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="20876-142">标记将如下所示。</span><span class="sxs-lookup"><span data-stu-id="20876-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="20876-143">现在，我们可以输入评论，我们将在 "产品" 页上显示这些评论。</span><span class="sxs-lookup"><span data-stu-id="20876-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="20876-144">将此标记添加到 ProductDetails 页。</span><span class="sxs-lookup"><span data-stu-id="20876-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="20876-145">现在运行应用程序并导航到产品，显示产品信息（包括客户评审）。</span><span class="sxs-lookup"><span data-stu-id="20876-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a><span data-ttu-id="20876-146">常用项控件（创建用户控件）</span><span class="sxs-lookup"><span data-stu-id="20876-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="20876-147">为了增加网站的销售额，我们将向 "暗示销售" 常见或相关产品添加几个功能。</span><span class="sxs-lookup"><span data-stu-id="20876-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="20876-148">这些功能中的第一项功能是产品目录中更常用的产品列表。</span><span class="sxs-lookup"><span data-stu-id="20876-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="20876-149">我们将创建一个 "用户控件"，用于显示应用程序主页上的排名靠前的销售项目。</span><span class="sxs-lookup"><span data-stu-id="20876-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="20876-150">由于这将是一个控件，因此，只需在 Visual Studio 的设计器中将控件拖放到所喜欢的任何页上即可在任何页面上使用它。</span><span class="sxs-lookup"><span data-stu-id="20876-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="20876-151">在 Visual Studio 的解决方案资源管理器中，右键单击解决方案名称，然后创建一个名为 "Controls" 的新目录。</span><span class="sxs-lookup"><span data-stu-id="20876-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="20876-152">虽然这不是必需的，但我们将通过在 "Controls" 目录中创建所有用户控件来帮助保持项目的结构。</span><span class="sxs-lookup"><span data-stu-id="20876-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="20876-153">右键单击 "controls" 文件夹，然后选择 "新建项"：</span><span class="sxs-lookup"><span data-stu-id="20876-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="20876-154">为 "PopularItems" 的控件指定名称。</span><span class="sxs-lookup"><span data-stu-id="20876-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="20876-155">请注意，用户控件的文件扩展名为 .ascx 而不是 .aspx。</span><span class="sxs-lookup"><span data-stu-id="20876-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="20876-156">我们的常用项目用户控件将按如下方式定义。</span><span class="sxs-lookup"><span data-stu-id="20876-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="20876-157">这里，我们使用的是尚未在此应用程序中使用的方法。</span><span class="sxs-lookup"><span data-stu-id="20876-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="20876-158">我们使用的是 repeater 控件，而不是使用数据源控件将 Repeater 控件绑定到 LINQ to Entities 查询的结果。</span><span class="sxs-lookup"><span data-stu-id="20876-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="20876-159">在我们的控件后面的代码中，我们按如下所示执行此操作。</span><span class="sxs-lookup"><span data-stu-id="20876-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="20876-160">请注意，此重要的行位于控件标记的顶部。</span><span class="sxs-lookup"><span data-stu-id="20876-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="20876-161">由于最常用的项每分钟都不会更改，因此我们可以添加 aching 指令来改善应用程序的性能。</span><span class="sxs-lookup"><span data-stu-id="20876-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="20876-162">此指令将使控件代码仅在控件的缓存输出过期时执行。</span><span class="sxs-lookup"><span data-stu-id="20876-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="20876-163">否则，将使用控件输出的缓存版本。</span><span class="sxs-lookup"><span data-stu-id="20876-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="20876-164">现在我们要做的就是将新控件包含在我们的默认 .aspx 页中。</span><span class="sxs-lookup"><span data-stu-id="20876-164">Now all we have to do is include our new control in our Default.aspx page.</span></span>

<span data-ttu-id="20876-165">使用拖放将控件的一个实例置于默认窗体的 "打开" 列中。</span><span class="sxs-lookup"><span data-stu-id="20876-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="20876-166">现在，运行应用程序时，主页会显示最常用的项。</span><span class="sxs-lookup"><span data-stu-id="20876-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a><span data-ttu-id="20876-167">"还购买" 控件（带参数的用户控件）</span><span class="sxs-lookup"><span data-stu-id="20876-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="20876-168">我们要创建的第二个用户控件将通过添加上下文的具体内容来将暗示性销售转到下一级别。</span><span class="sxs-lookup"><span data-stu-id="20876-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="20876-169">用于计算前面 "也已购买" 项的逻辑是不重要的。</span><span class="sxs-lookup"><span data-stu-id="20876-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="20876-170">我们的 "还购买" 控制将为当前所选的 ProductID 选择 OrderDetails 记录（以前购买的记录），并为找到的每个唯一顺序获取 OrderIDs。</span><span class="sxs-lookup"><span data-stu-id="20876-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="20876-171">然后，将从所有订单中选择 "al"，并对购买的数量进行求和。</span><span class="sxs-lookup"><span data-stu-id="20876-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="20876-172">我们会按此数量进行排序，并显示前5项。</span><span class="sxs-lookup"><span data-stu-id="20876-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="20876-173">由于此逻辑的复杂性，我们将此算法作为存储过程实现。</span><span class="sxs-lookup"><span data-stu-id="20876-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="20876-174">存储过程的 T-sql 如下所示。</span><span class="sxs-lookup"><span data-stu-id="20876-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="20876-175">请注意，在我们的应用程序中包含此存储过程（SelectPurchasedWithProducts）后，如果生成实体数据模型，则除了需要的表和视图外，还实体数据模型应包括此存储过程。</span><span class="sxs-lookup"><span data-stu-id="20876-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="20876-176">若要从实体数据模型访问存储过程，我们需要导入函数。</span><span class="sxs-lookup"><span data-stu-id="20876-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="20876-177">双击 "解决方案资源管理器" 中的实体数据模型，在设计器中将其打开，然后打开模型浏览器，右键单击设计器并选择 "添加函数导入"。</span><span class="sxs-lookup"><span data-stu-id="20876-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="20876-178">这样做会打开此对话框。</span><span class="sxs-lookup"><span data-stu-id="20876-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="20876-179">如以上所示填写字段，请选择 "SelectPurchasedWithProducts"，并使用导入函数名称的过程名称。</span><span class="sxs-lookup"><span data-stu-id="20876-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="20876-180">单击 "确定"。</span><span class="sxs-lookup"><span data-stu-id="20876-180">Click "Ok".</span></span>

<span data-ttu-id="20876-181">完成此操作后，就可以对存储过程进行编程，就像我们在模型中的任何其他项一样。</span><span class="sxs-lookup"><span data-stu-id="20876-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="20876-182">因此，在我们的 "Controls" 文件夹中创建一个名为 AlsoPurchased 的新用户控件。</span><span class="sxs-lookup"><span data-stu-id="20876-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="20876-183">对于 PopularItems 控件，此控件的标记将非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="20876-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="20876-184">显著的区别在于，由于要呈现的项将因产品而异，因此不会缓存输出。</span><span class="sxs-lookup"><span data-stu-id="20876-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="20876-185">ProductId 将是控件的 "属性"。</span><span class="sxs-lookup"><span data-stu-id="20876-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="20876-186">在控件的预呈现事件处理程序中，我们 eed 执行三个操作。</span><span class="sxs-lookup"><span data-stu-id="20876-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="20876-187">请确保已设置 "ProductID"。</span><span class="sxs-lookup"><span data-stu-id="20876-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="20876-188">查看是否存在与当前产品一起购买的任何产品。</span><span class="sxs-lookup"><span data-stu-id="20876-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="20876-189">输出 #2 中确定的一些项。</span><span class="sxs-lookup"><span data-stu-id="20876-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="20876-190">请注意，通过模型调用存储过程是多么简单。</span><span class="sxs-lookup"><span data-stu-id="20876-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="20876-191">确定是否 "也已购买" 后，只需将中继器绑定到查询返回的结果。</span><span class="sxs-lookup"><span data-stu-id="20876-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="20876-192">如果没有任何 "也购买" 的项，我们只会从目录中显示其他热门项。</span><span class="sxs-lookup"><span data-stu-id="20876-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="20876-193">若要查看 "还购买" 项，请打开 "ProductDetails" 页，然后从 "解决方案资源管理器" 中拖动 "AlsoPurchased" 控件，使其显示在标记中的此位置。</span><span class="sxs-lookup"><span data-stu-id="20876-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="20876-194">这样做将创建对 ProductDetails 页顶部的控件的引用。</span><span class="sxs-lookup"><span data-stu-id="20876-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="20876-195">由于 AlsoPurchased 用户控件需要 ProductId 编号，因此我们将通过对页面的当前数据模型项使用 Eval 语句，来设置控件的 ProductID 属性。</span><span class="sxs-lookup"><span data-stu-id="20876-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="20876-196">当我们立即生成并运行并浏览到某一产品时，我们将看到 "也已购买" 项。</span><span class="sxs-lookup"><span data-stu-id="20876-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="20876-197">[上一页](tailspin-spyworks-part-6.md)
> [下一页](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="20876-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>
