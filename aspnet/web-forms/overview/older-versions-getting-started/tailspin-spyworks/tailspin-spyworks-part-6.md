---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 第6部分： ASP.NET 成员身份 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第6部分添加 ASP.NET 成员身份。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454880"
---
# <a name="part-6-aspnet-membership"></a><span data-ttu-id="63fae-104">第6部分： ASP.NET 成员身份</span><span class="sxs-lookup"><span data-stu-id="63fae-104">Part 6: ASP.NET Membership</span></span>

<span data-ttu-id="63fae-105">作者： [Joe Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="63fae-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="63fae-106">Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。</span><span class="sxs-lookup"><span data-stu-id="63fae-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="63fae-107">其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。</span><span class="sxs-lookup"><span data-stu-id="63fae-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="63fae-108">本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。</span><span class="sxs-lookup"><span data-stu-id="63fae-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="63fae-109">第6部分添加 ASP.NET 成员身份。</span><span class="sxs-lookup"><span data-stu-id="63fae-109">Part 6 adds ASP.NET Membership.</span></span>

## <a id="_Toc260221672"></a><span data-ttu-id="63fae-110">使用 ASP.NET 成员身份</span><span class="sxs-lookup"><span data-stu-id="63fae-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="63fae-111">单击 "安全"</span><span class="sxs-lookup"><span data-stu-id="63fae-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="63fae-112">请确保使用的是窗体身份验证。</span><span class="sxs-lookup"><span data-stu-id="63fae-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="63fae-113">使用 "创建用户" 链接创建几个用户。</span><span class="sxs-lookup"><span data-stu-id="63fae-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="63fae-114">完成后，请参阅 "解决方案资源管理器" 窗口并刷新视图。</span><span class="sxs-lookup"><span data-stu-id="63fae-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="63fae-115">请注意，ASPNETDB.MDF。已创建 MDF 精细。</span><span class="sxs-lookup"><span data-stu-id="63fae-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="63fae-116">此文件包含支持核心 ASP.NET 服务（如成员身份）的表。</span><span class="sxs-lookup"><span data-stu-id="63fae-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="63fae-117">现在，我们可以开始实现结帐过程。</span><span class="sxs-lookup"><span data-stu-id="63fae-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="63fae-118">首先创建一个 "CheckOut" 页。</span><span class="sxs-lookup"><span data-stu-id="63fae-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="63fae-119">只应将 "CheckOut" 页提供给已登录的用户，这样我们就可以将访问权限限制为已登录的用户，并将不登录的用户重定向到登录页。</span><span class="sxs-lookup"><span data-stu-id="63fae-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="63fae-120">为此，我们将以下内容添加到 web.config 文件的配置节。</span><span class="sxs-lookup"><span data-stu-id="63fae-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="63fae-121">ASP.NET Web 窗体应用程序的模板会自动将身份验证部分添加到 web.config 文件中，并建立默认登录页。</span><span class="sxs-lookup"><span data-stu-id="63fae-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="63fae-122">当用户登录时，必须修改登录 .aspx 代码隐藏文件，以迁移匿名购物车。</span><span class="sxs-lookup"><span data-stu-id="63fae-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="63fae-123">按如下所示\_Load 事件更改页面。</span><span class="sxs-lookup"><span data-stu-id="63fae-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="63fae-124">然后，添加类似于下面的 "LoggedIn" 事件处理程序，将会话名称设置为新登录的用户，并通过在 MyShoppingCart 类中调用 MigrateCart 方法，将购物车中的临时会话 id 更改为该用户的会话 id。</span><span class="sxs-lookup"><span data-stu-id="63fae-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="63fae-125">（在 .cs 文件中实现）</span><span class="sxs-lookup"><span data-stu-id="63fae-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="63fae-126">实现如下所示的 MigrateCart （）方法。</span><span class="sxs-lookup"><span data-stu-id="63fae-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="63fae-127">在签出 .aspx 中，我们将使用 EntityDataSource 和 GridView 在我们的 "购物车" 页中。</span><span class="sxs-lookup"><span data-stu-id="63fae-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="63fae-128">请注意，我们的 GridView 控件指定了一个名为 MyList 的 "ondatabound" 事件处理程序\_RowDataBound，因此让我们按如下所示实现此事件处理程序。</span><span class="sxs-lookup"><span data-stu-id="63fae-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="63fae-129">此方法会在每行被绑定时保留购物车的运行总计，并更新 GridView 的底部行。</span><span class="sxs-lookup"><span data-stu-id="63fae-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="63fae-130">在此阶段，我们已实现了要放置的订单的 "评审" 演示。</span><span class="sxs-lookup"><span data-stu-id="63fae-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="63fae-131">让我们通过在页面\_Load 事件中添加几行代码来处理空购物车方案：</span><span class="sxs-lookup"><span data-stu-id="63fae-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="63fae-132">当用户单击 "提交" 按钮时，将在提交按钮单击事件处理程序中执行以下代码。</span><span class="sxs-lookup"><span data-stu-id="63fae-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="63fae-133">订单提交过程的 "肉类" 将在我们的 MyShoppingCart 类的订单（）方法中实现。</span><span class="sxs-lookup"><span data-stu-id="63fae-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="63fae-134">订单将：</span><span class="sxs-lookup"><span data-stu-id="63fae-134">SubmitOrder will:</span></span>

- <span data-ttu-id="63fae-135">获取购物车中的所有行项，并使用它们创建新订单记录和关联的 OrderDetails 记录。</span><span class="sxs-lookup"><span data-stu-id="63fae-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="63fae-136">计算寄送日期。</span><span class="sxs-lookup"><span data-stu-id="63fae-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="63fae-137">清除购物车。</span><span class="sxs-lookup"><span data-stu-id="63fae-137">Clear the shopping cart.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="63fae-138">在此示例应用程序中，我们只需将两天加到当前日期即可计算发货日期。</span><span class="sxs-lookup"><span data-stu-id="63fae-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="63fae-139">现在，运行应用程序将允许我们测试从一开始到完成的购物过程。</span><span class="sxs-lookup"><span data-stu-id="63fae-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="63fae-140">[上一页](tailspin-spyworks-part-5.md)
> [下一页](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="63fae-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
