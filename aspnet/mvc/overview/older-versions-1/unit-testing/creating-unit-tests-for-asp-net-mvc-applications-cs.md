---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: 为 ASP.NET MVC 应用程序创建单元测试C#（） |Microsoft Docs
author: StephenWalther
description: 了解如何为控制器操作创建单元测试。 在本教程中，Stephen Walther 演示了如何测试控制器操作是否返回 parti 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595251"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a><span data-ttu-id="a377c-104">为 ASP.NET MVC 应用程序创建单元测试 (C#)</span><span class="sxs-lookup"><span data-stu-id="a377c-104">Creating Unit Tests for ASP.NET MVC Applications (C#)</span></span>

<span data-ttu-id="a377c-105">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="a377c-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="a377c-106">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="a377c-106">Download PDF</span></span>](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> <span data-ttu-id="a377c-107">了解如何为控制器操作创建单元测试。</span><span class="sxs-lookup"><span data-stu-id="a377c-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="a377c-108">在本教程中，Stephen Walther 演示了如何测试控制器操作返回特定的视图、返回特定的数据集，还是返回不同类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="a377c-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>

<span data-ttu-id="a377c-109">本教程的目的是演示如何为 ASP.NET MVC 应用程序中的控制器编写单元测试。</span><span class="sxs-lookup"><span data-stu-id="a377c-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="a377c-110">我们介绍如何生成三种不同类型的单元测试。</span><span class="sxs-lookup"><span data-stu-id="a377c-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="a377c-111">您将了解如何测试控制器操作返回的视图、如何测试控制器操作返回的视图数据，以及如何测试一个控制器操作是否将您重定向到另一个控制器操作。</span><span class="sxs-lookup"><span data-stu-id="a377c-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="a377c-112">创建受测控制器</span><span class="sxs-lookup"><span data-stu-id="a377c-112">Creating the Controller under Test</span></span>

<span data-ttu-id="a377c-113">首先，让我们创建要测试的控制器。</span><span class="sxs-lookup"><span data-stu-id="a377c-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="a377c-114">名为 `ProductController`的控制器包含在列表1中。</span><span class="sxs-lookup"><span data-stu-id="a377c-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="a377c-115">**列表1– `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="a377c-115">**Listing 1 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

<span data-ttu-id="a377c-116">`ProductController` 包含两个名为 `Index()` 和 `Details()`的操作方法。</span><span class="sxs-lookup"><span data-stu-id="a377c-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="a377c-117">这两个操作方法都返回视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-117">Both action methods return a view.</span></span> <span data-ttu-id="a377c-118">请注意，`Details()` 操作接受名为 Id 的参数。</span><span class="sxs-lookup"><span data-stu-id="a377c-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="a377c-119">测试控制器返回的视图</span><span class="sxs-lookup"><span data-stu-id="a377c-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="a377c-120">假设我们想要测试 `ProductController` 是否返回正确的视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="a377c-121">我们想要确保在调用 `ProductController.Details()` 操作时，将返回详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="a377c-122">清单2中的测试类包含用于测试 `ProductController.Details()` 操作返回的视图的单元测试。</span><span class="sxs-lookup"><span data-stu-id="a377c-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="a377c-123">**列表2– `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="a377c-123">**Listing 2 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

<span data-ttu-id="a377c-124">清单2中的类包含一个名为 `TestDetailsView()`的测试方法。</span><span class="sxs-lookup"><span data-stu-id="a377c-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="a377c-125">此方法包含三行代码。</span><span class="sxs-lookup"><span data-stu-id="a377c-125">This method contains three lines of code.</span></span> <span data-ttu-id="a377c-126">第一行代码创建 `ProductController` 类的新实例。</span><span class="sxs-lookup"><span data-stu-id="a377c-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="a377c-127">第二行代码调用控制器的 `Details()` 操作方法。</span><span class="sxs-lookup"><span data-stu-id="a377c-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="a377c-128">最后，代码的最后一行检查 `Details()` 操作返回的视图是否为详细信息视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="a377c-129">`ViewResult.ViewName` 属性表示控制器返回的视图的名称。</span><span class="sxs-lookup"><span data-stu-id="a377c-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="a377c-130">有关测试此属性的一个严重警告。</span><span class="sxs-lookup"><span data-stu-id="a377c-130">One big warning about testing this property.</span></span> <span data-ttu-id="a377c-131">控制器可以通过两种方式返回视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="a377c-132">控制器可以显式返回如下所示的视图：</span><span class="sxs-lookup"><span data-stu-id="a377c-132">A controller can explicitly return a view like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

<span data-ttu-id="a377c-133">或者，可以从控制器操作的名称（如下所示）推断视图的名称：</span><span class="sxs-lookup"><span data-stu-id="a377c-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

<span data-ttu-id="a377c-134">此控制器操作还会返回一个名为 `Details`的视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="a377c-135">但是，视图的名称是从操作名称推断出来的。</span><span class="sxs-lookup"><span data-stu-id="a377c-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="a377c-136">如果要测试视图名称，则必须从控制器操作显式返回视图名称。</span><span class="sxs-lookup"><span data-stu-id="a377c-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="a377c-137">你可以通过以下方式运行 "列表 2" 中的单元测试：输入键盘组合**Ctrl +、** 或单击 "**运行解决方案中的所有测试**" 按钮（参见图1）。</span><span class="sxs-lookup"><span data-stu-id="a377c-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="a377c-138">如果测试通过，则会看到图2中的 "测试结果" 窗口。</span><span class="sxs-lookup"><span data-stu-id="a377c-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>

<span data-ttu-id="a377c-139">[![在解决方案中运行所有测试](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a377c-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)</span></span>

<span data-ttu-id="a377c-140">**图 01**：运行解决方案中的所有测试（[单击以查看完全大小的映像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="a377c-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))</span></span>

<span data-ttu-id="a377c-141">[![成功！](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="a377c-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)</span></span>

<span data-ttu-id="a377c-142">**图 02**： Success！</span><span class="sxs-lookup"><span data-stu-id="a377c-142">**Figure 02**: Success!</span></span> <span data-ttu-id="a377c-143">（[单击以查看完全大小的映像](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="a377c-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))</span></span>

## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="a377c-144">测试控制器返回的视图数据</span><span class="sxs-lookup"><span data-stu-id="a377c-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="a377c-145">MVC 控制器使用称为 *`View Data`* 的内容将数据传递给视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="a377c-146">例如，假设你想要在调用 `ProductController Details()` 操作时显示特定产品的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a377c-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="a377c-147">在这种情况下，您可以创建 `Product` 类的实例（在模型中定义），并通过利用 `View Data`将该实例传递到 `Details` 视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="a377c-148">列表3中修改后的 `ProductController` 包含一个返回产品的已更新 `Details()` 操作。</span><span class="sxs-lookup"><span data-stu-id="a377c-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="a377c-149">**列表 3-`ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="a377c-149">**Listing 3 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

<span data-ttu-id="a377c-150">首先，`Details()` 操作创建 `Product` 类的新实例，该实例表示便携式计算机。</span><span class="sxs-lookup"><span data-stu-id="a377c-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="a377c-151">接下来，`Product` 类的实例将作为第二个参数传递到 `View()` 方法。</span><span class="sxs-lookup"><span data-stu-id="a377c-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="a377c-152">您可以编写单元测试来测试所需的数据是否包含在查看数据中。</span><span class="sxs-lookup"><span data-stu-id="a377c-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="a377c-153">当你调用 `ProductController Details()` 操作方法时，列表4中的单元测试将测试是否返回表示便携式计算机的产品。</span><span class="sxs-lookup"><span data-stu-id="a377c-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="a377c-154">**列表 4-`ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="a377c-154">**Listing 4 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

<span data-ttu-id="a377c-155">在列表4中，`TestDetailsView()` 方法通过调用 `Details()` 方法来测试返回的视图数据。</span><span class="sxs-lookup"><span data-stu-id="a377c-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="a377c-156">`ViewData` 通过调用 `Details()` 方法，作为 `ViewResult` 上的属性公开。</span><span class="sxs-lookup"><span data-stu-id="a377c-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="a377c-157">`ViewData.Model` 属性包含传递给该视图的产品。</span><span class="sxs-lookup"><span data-stu-id="a377c-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="a377c-158">该测试只是验证视图数据中包含的产品是否具有名称 "便携式计算机"。</span><span class="sxs-lookup"><span data-stu-id="a377c-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="a377c-159">测试控制器返回的操作结果</span><span class="sxs-lookup"><span data-stu-id="a377c-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="a377c-160">更复杂的控制器操作可能返回不同类型的操作结果，具体取决于传递给控制器操作的参数的值。</span><span class="sxs-lookup"><span data-stu-id="a377c-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="a377c-161">控制器操作可以返回各种类型的操作结果，包括 `ViewResult`、`RedirectToRouteResult`或 `JsonResult`。</span><span class="sxs-lookup"><span data-stu-id="a377c-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="a377c-162">例如，将有效的产品 Id 传递到操作时，列表5中修改后的 `Details()` 操作返回 `Details` 视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="a377c-163">如果传递的产品 Id 无效（Id 值小于1，则将重定向到 `Index()` 操作。</span><span class="sxs-lookup"><span data-stu-id="a377c-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="a377c-164">**列表5– `ProductController.cs`**</span><span class="sxs-lookup"><span data-stu-id="a377c-164">**Listing 5 – `ProductController.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

<span data-ttu-id="a377c-165">可以通过清单6中的单元测试测试 `Details()` 操作的行为。</span><span class="sxs-lookup"><span data-stu-id="a377c-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="a377c-166">清单6中的单元测试验证在将值为-1 的 Id 传递到 `Details()` 方法时，是否已重定向到 `Index` 视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="a377c-167">**清单6– `ProductControllerTest.cs`**</span><span class="sxs-lookup"><span data-stu-id="a377c-167">**Listing 6 – `ProductControllerTest.cs`**</span></span>

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

<span data-ttu-id="a377c-168">当在控制器操作中调用 `RedirectToAction()` 方法时，控制器操作返回一个 `RedirectToRouteResult`。</span><span class="sxs-lookup"><span data-stu-id="a377c-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="a377c-169">测试检查 `RedirectToRouteResult` 是否会将用户重定向到名为 `Index`的控制器操作。</span><span class="sxs-lookup"><span data-stu-id="a377c-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="a377c-170">总结</span><span class="sxs-lookup"><span data-stu-id="a377c-170">Summary</span></span>

<span data-ttu-id="a377c-171">在本教程中，您学习了如何生成 MVC 控制器操作的单元测试。</span><span class="sxs-lookup"><span data-stu-id="a377c-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="a377c-172">首先，您学习了如何验证控制器操作是否返回了正确的视图。</span><span class="sxs-lookup"><span data-stu-id="a377c-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="a377c-173">已了解如何使用 `ViewResult.ViewName` 属性验证视图的名称。</span><span class="sxs-lookup"><span data-stu-id="a377c-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="a377c-174">接下来，我们探讨了如何测试 `View Data`的内容。</span><span class="sxs-lookup"><span data-stu-id="a377c-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="a377c-175">已了解如何在调用控制器操作后检查是否在 `View Data` 中返回了正确的产品。</span><span class="sxs-lookup"><span data-stu-id="a377c-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="a377c-176">最后，我们讨论了如何测试控制器操作是否返回不同类型的操作结果。</span><span class="sxs-lookup"><span data-stu-id="a377c-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="a377c-177">了解了如何测试控制器是返回 `ViewResult` 还是 `RedirectToRouteResult`。</span><span class="sxs-lookup"><span data-stu-id="a377c-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="a377c-178">下一页</span><span class="sxs-lookup"><span data-stu-id="a377c-178">Next</span></span>](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
