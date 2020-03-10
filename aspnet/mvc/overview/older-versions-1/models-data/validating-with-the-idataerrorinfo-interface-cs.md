---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: 用 IDataErrorInfo 接口（C#）进行验证 |Microsoft Docs
author: StephenWalther
description: Stephen Walther 演示了如何通过在模型类中实现 IDataErrorInfo 接口来显示自定义验证错误消息。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 938b180da02b1963acffd021d18621d75d1d0447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436346"
---
# <a name="validating-with-the-idataerrorinfo-interface-c"></a><span data-ttu-id="e5431-103">使用 IDataErrorInfo 接口进行验证 (C#)</span><span class="sxs-lookup"><span data-stu-id="e5431-103">Validating with the IDataErrorInfo Interface (C#)</span></span>

<span data-ttu-id="e5431-104">作者： [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="e5431-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="e5431-105">Stephen Walther 演示了如何通过在模型类中实现 IDataErrorInfo 接口来显示自定义验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="e5431-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>

<span data-ttu-id="e5431-106">本教程的目的是介绍一种在 ASP.NET MVC 应用程序中执行验证的方法。</span><span class="sxs-lookup"><span data-stu-id="e5431-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="e5431-107">了解如何在不为所需的窗体域提供值的情况下，防止某人提交 HTML 表单。</span><span class="sxs-lookup"><span data-stu-id="e5431-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="e5431-108">在本教程中，将了解如何使用 IErrorDataInfo 接口执行验证。</span><span class="sxs-lookup"><span data-stu-id="e5431-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="e5431-109">假设</span><span class="sxs-lookup"><span data-stu-id="e5431-109">Assumptions</span></span>

<span data-ttu-id="e5431-110">在本教程中，我将使用 MoviesDB 数据库和电影数据库表。</span><span class="sxs-lookup"><span data-stu-id="e5431-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="e5431-111">此表包含以下列：</span><span class="sxs-lookup"><span data-stu-id="e5431-111">This table has the following columns:</span></span>

<a id="0.5_table01"></a>

| <span data-ttu-id="e5431-112">**列名称**</span><span class="sxs-lookup"><span data-stu-id="e5431-112">**Column Name**</span></span> | <span data-ttu-id="e5431-113">**数据类型**</span><span class="sxs-lookup"><span data-stu-id="e5431-113">**Data Type**</span></span> | <span data-ttu-id="e5431-114">**允许 Null 值**</span><span class="sxs-lookup"><span data-stu-id="e5431-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e5431-115">Id</span><span class="sxs-lookup"><span data-stu-id="e5431-115">Id</span></span> | <span data-ttu-id="e5431-116">Int</span><span class="sxs-lookup"><span data-stu-id="e5431-116">Int</span></span> | <span data-ttu-id="e5431-117">False</span><span class="sxs-lookup"><span data-stu-id="e5431-117">False</span></span> |
| <span data-ttu-id="e5431-118">标题</span><span class="sxs-lookup"><span data-stu-id="e5431-118">Title</span></span> | <span data-ttu-id="e5431-119">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="e5431-119">Nvarchar(100)</span></span> | <span data-ttu-id="e5431-120">False</span><span class="sxs-lookup"><span data-stu-id="e5431-120">False</span></span> |
| <span data-ttu-id="e5431-121">导演</span><span class="sxs-lookup"><span data-stu-id="e5431-121">Director</span></span> | <span data-ttu-id="e5431-122">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="e5431-122">Nvarchar(100)</span></span> | <span data-ttu-id="e5431-123">False</span><span class="sxs-lookup"><span data-stu-id="e5431-123">False</span></span> |
| <span data-ttu-id="e5431-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="e5431-124">DateReleased</span></span> | <span data-ttu-id="e5431-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="e5431-125">DateTime</span></span> | <span data-ttu-id="e5431-126">False</span><span class="sxs-lookup"><span data-stu-id="e5431-126">False</span></span> |

<span data-ttu-id="e5431-127">在本教程中，我将使用 Microsoft 实体框架生成数据库模型类。</span><span class="sxs-lookup"><span data-stu-id="e5431-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="e5431-128">实体框架生成的 Movie 类如图1所示。</span><span class="sxs-lookup"><span data-stu-id="e5431-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>

<span data-ttu-id="e5431-129">[!["电影" 实体](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e5431-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span></span>

<span data-ttu-id="e5431-130">**图 01**：电影实体（[单击以查看完全大小的图像](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="e5431-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e5431-131">若要了解有关使用实体框架生成数据库模型类的详细信息，请参阅我的教程使用实体框架创建模型类。</span><span class="sxs-lookup"><span data-stu-id="e5431-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>

## <a name="the-controller-class"></a><span data-ttu-id="e5431-132">控制器类</span><span class="sxs-lookup"><span data-stu-id="e5431-132">The Controller Class</span></span>

<span data-ttu-id="e5431-133">我们使用 Home 控制器来列出电影并创建新电影。</span><span class="sxs-lookup"><span data-stu-id="e5431-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="e5431-134">此类的代码包含在列表1中。</span><span class="sxs-lookup"><span data-stu-id="e5431-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="e5431-135">**列表 1-Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="e5431-135">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

<span data-ttu-id="e5431-136">列表1中的 Home 控制器类包含两个 Create （）操作。</span><span class="sxs-lookup"><span data-stu-id="e5431-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="e5431-137">第一个操作显示用于创建新电影的 HTML 窗体。</span><span class="sxs-lookup"><span data-stu-id="e5431-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="e5431-138">第二个 Create （）操作执行将新电影插入到数据库中的实际操作。</span><span class="sxs-lookup"><span data-stu-id="e5431-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="e5431-139">当第一个 Create （）操作显示的窗体提交给服务器时，将调用第二个 Create （）操作。</span><span class="sxs-lookup"><span data-stu-id="e5431-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="e5431-140">请注意，第二个 Create （）操作包含以下代码行：</span><span class="sxs-lookup"><span data-stu-id="e5431-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

<span data-ttu-id="e5431-141">当存在验证错误时，IsValid 属性返回 false。</span><span class="sxs-lookup"><span data-stu-id="e5431-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="e5431-142">在这种情况下，将重新显示包含用于创建电影的 HTML 窗体的 "创建" 视图。</span><span class="sxs-lookup"><span data-stu-id="e5431-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="e5431-143">创建分部类</span><span class="sxs-lookup"><span data-stu-id="e5431-143">Creating a Partial Class</span></span>

<span data-ttu-id="e5431-144">Movie 类由实体框架生成。</span><span class="sxs-lookup"><span data-stu-id="e5431-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="e5431-145">如果在 "解决方案资源管理器" 窗口中展开 "MoviesDBModel" 文件，然后在代码编辑器中打开 MoviesDBModel.Designer.cs 文件（请参阅图2），则可以查看 Movie 类的代码。</span><span class="sxs-lookup"><span data-stu-id="e5431-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.cs file in the Code Editor (see Figure 2).</span></span>

<span data-ttu-id="e5431-146">[!["电影" 实体的代码](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e5431-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span></span>

<span data-ttu-id="e5431-147">**图 02**：电影实体的代码（[单击以查看完全大小的图像](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="e5431-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span></span>

<span data-ttu-id="e5431-148">Movie 类是一个分部类。</span><span class="sxs-lookup"><span data-stu-id="e5431-148">The Movie class is a partial class.</span></span> <span data-ttu-id="e5431-149">这意味着，我们可以添加具有相同名称的另一个分部类，以扩展 Movie 类的功能。</span><span class="sxs-lookup"><span data-stu-id="e5431-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="e5431-150">我们会将验证逻辑添加到新的分部类。</span><span class="sxs-lookup"><span data-stu-id="e5431-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="e5431-151">将清单2中的类添加到 "模型" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="e5431-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="e5431-152">**列表 2-Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="e5431-152">**Listing 2 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

<span data-ttu-id="e5431-153">请注意，"清单 2" 中的类包括*partial*修饰符。</span><span class="sxs-lookup"><span data-stu-id="e5431-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="e5431-154">你添加到此类的任何方法或属性都将成为实体框架生成的 Movie 类的一部分。</span><span class="sxs-lookup"><span data-stu-id="e5431-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="e5431-155">添加 OnChanging 和 OnChanged 分部方法</span><span class="sxs-lookup"><span data-stu-id="e5431-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="e5431-156">当实体框架生成实体类时，实体框架会自动向类中添加分部方法。</span><span class="sxs-lookup"><span data-stu-id="e5431-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="e5431-157">实体框架生成与类的每个属性相对应的 OnChanging 和 OnChanged 分部方法。</span><span class="sxs-lookup"><span data-stu-id="e5431-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="e5431-158">对于 Movie 类，实体框架会创建以下方法：</span><span class="sxs-lookup"><span data-stu-id="e5431-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="e5431-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="e5431-159">OnIdChanging</span></span>
- <span data-ttu-id="e5431-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="e5431-160">OnIdChanged</span></span>
- <span data-ttu-id="e5431-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="e5431-161">OnTitleChanging</span></span>
- <span data-ttu-id="e5431-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="e5431-162">OnTitleChanged</span></span>
- <span data-ttu-id="e5431-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="e5431-163">OnDirectorChanging</span></span>
- <span data-ttu-id="e5431-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="e5431-164">OnDirectorChanged</span></span>
- <span data-ttu-id="e5431-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="e5431-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="e5431-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="e5431-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="e5431-167">在相应属性更改之前，先调用 OnChanging 方法。</span><span class="sxs-lookup"><span data-stu-id="e5431-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="e5431-168">更改属性后，将立即调用 OnChanged 方法。</span><span class="sxs-lookup"><span data-stu-id="e5431-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="e5431-169">您可以利用这些分部方法将验证逻辑添加到 Movie 类中。</span><span class="sxs-lookup"><span data-stu-id="e5431-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="e5431-170">清单3中的 update Movie 类验证是否为 Title 和 Director 属性分配了非空值。</span><span class="sxs-lookup"><span data-stu-id="e5431-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e5431-171">分部方法是在类中定义的不需要实现的方法。</span><span class="sxs-lookup"><span data-stu-id="e5431-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="e5431-172">如果未实现分部方法，则编译器会删除方法签名和对方法的所有调用，因此没有与分部方法关联的运行时开销。</span><span class="sxs-lookup"><span data-stu-id="e5431-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="e5431-173">在 Visual Studio Code 编辑器中，可以通过键入关键字*partial*后面跟一个空格来添加分部方法，以便查看要实现的分区列表。</span><span class="sxs-lookup"><span data-stu-id="e5431-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>

<span data-ttu-id="e5431-174">**列表 3-Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="e5431-174">**Listing 3 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

<span data-ttu-id="e5431-175">例如，如果尝试将空字符串分配给 Title 属性，则会将错误消息分配给名为 \_错误的字典。</span><span class="sxs-lookup"><span data-stu-id="e5431-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="e5431-176">此时，将空字符串分配给 Title 属性并将错误添加到 "私有 \_错误" 字段时，实际上不会发生任何操作。</span><span class="sxs-lookup"><span data-stu-id="e5431-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="e5431-177">我们需要实现 IDataErrorInfo 接口，将这些验证错误公开给 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="e5431-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="e5431-178">实现 IDataErrorInfo 接口</span><span class="sxs-lookup"><span data-stu-id="e5431-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="e5431-179">自第一版以来，IDataErrorInfo 接口已是 .NET framework 的一部分。</span><span class="sxs-lookup"><span data-stu-id="e5431-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="e5431-180">此接口是一个非常简单的接口：</span><span class="sxs-lookup"><span data-stu-id="e5431-180">This interface is a very simple interface:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

<span data-ttu-id="e5431-181">如果类实现 IDataErrorInfo 接口，则 ASP.NET MVC 框架将在创建类的实例时使用此接口。</span><span class="sxs-lookup"><span data-stu-id="e5431-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="e5431-182">例如，"主控制器创建（）" 操作接受 Movie 类的实例：</span><span class="sxs-lookup"><span data-stu-id="e5431-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

<span data-ttu-id="e5431-183">ASP.NET MVC 框架使用模型绑定器（DefaultModelBinder）创建传递到 Create （）操作的电影的实例。</span><span class="sxs-lookup"><span data-stu-id="e5431-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="e5431-184">模型联编程序负责通过将 HTML 窗体字段绑定到 Movie 对象的实例来创建 Movie 对象的实例。</span><span class="sxs-lookup"><span data-stu-id="e5431-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="e5431-185">DefaultModelBinder 检测类是否实现 IDataErrorInfo 接口。</span><span class="sxs-lookup"><span data-stu-id="e5431-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="e5431-186">如果类实现此接口，则模型绑定器将为类的每个属性调用 IDataErrorInfo。</span><span class="sxs-lookup"><span data-stu-id="e5431-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="e5431-187">如果索引器返回错误消息，则模型联编程序会自动将此错误消息添加到模型状态。</span><span class="sxs-lookup"><span data-stu-id="e5431-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="e5431-188">DefaultModelBinder 还会检查 IDataErrorInfo 属性。</span><span class="sxs-lookup"><span data-stu-id="e5431-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="e5431-189">此属性用于表示与类关联的非属性特定的验证错误。</span><span class="sxs-lookup"><span data-stu-id="e5431-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="e5431-190">例如，你可能希望强制实施依赖于 Movie 类的多个属性的值的验证规则。</span><span class="sxs-lookup"><span data-stu-id="e5431-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="e5431-191">在这种情况下，您将从 Error 属性返回一个验证错误。</span><span class="sxs-lookup"><span data-stu-id="e5431-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="e5431-192">列表4中更新后的 Movie 类实现 IDataErrorInfo 接口。</span><span class="sxs-lookup"><span data-stu-id="e5431-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="e5431-193">**列表 4-Models\Movie.cs （实现 IDataErrorInfo）**</span><span class="sxs-lookup"><span data-stu-id="e5431-193">**Listing 4 - Models\Movie.cs (implements IDataErrorInfo)**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

<span data-ttu-id="e5431-194">在列表4中，索引器属性检查 \_错误集合，以查看它是否包含与传递给索引器的属性名称对应的键。</span><span class="sxs-lookup"><span data-stu-id="e5431-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="e5431-195">如果没有与属性关联的验证错误，则返回空字符串。</span><span class="sxs-lookup"><span data-stu-id="e5431-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="e5431-196">无需以任何方式修改 Home 控制器即可使用修改后的 Movie 类。</span><span class="sxs-lookup"><span data-stu-id="e5431-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="e5431-197">图3中所示的页说明了在没有为标题或主管窗体字段输入值时将发生的情况。</span><span class="sxs-lookup"><span data-stu-id="e5431-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>

<span data-ttu-id="e5431-198">[![自动创建操作方法](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="e5431-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span></span>

<span data-ttu-id="e5431-199">**图 03**：缺少值的窗体（[单击以查看完全大小的图像](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="e5431-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span></span>

<span data-ttu-id="e5431-200">请注意，DateReleased 值会自动进行验证。</span><span class="sxs-lookup"><span data-stu-id="e5431-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="e5431-201">由于 DateReleased 属性不接受 NULL 值，因此当 DefaultModelBinder 没有值时，它会自动为此属性生成一个验证错误。</span><span class="sxs-lookup"><span data-stu-id="e5431-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="e5431-202">如果要修改 DateReleased 属性的错误消息，则需要创建自定义模型绑定器。</span><span class="sxs-lookup"><span data-stu-id="e5431-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="e5431-203">摘要</span><span class="sxs-lookup"><span data-stu-id="e5431-203">Summary</span></span>

<span data-ttu-id="e5431-204">在本教程中，您学习了如何使用 IDataErrorInfo 接口生成验证错误消息。</span><span class="sxs-lookup"><span data-stu-id="e5431-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="e5431-205">首先，我们创建了一个部分电影类，该类用于扩展由实体框架生成的部分电影类的功能。</span><span class="sxs-lookup"><span data-stu-id="e5431-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="e5431-206">接下来，我们向 Movie 类 OnTitleChanging （）和 OnDirectorChanging （）分部方法添加了验证逻辑。</span><span class="sxs-lookup"><span data-stu-id="e5431-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="e5431-207">最后，我们实现了 IDataErrorInfo 接口，以便将这些验证消息公开给 ASP.NET MVC 框架。</span><span class="sxs-lookup"><span data-stu-id="e5431-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e5431-208">[上一页](performing-simple-validation-cs.md)
> [下一页](validating-with-a-service-layer-cs.md)</span><span class="sxs-lookup"><span data-stu-id="e5431-208">[Previous](performing-simple-validation-cs.md)
[Next](validating-with-a-service-layer-cs.md)</span></span>
