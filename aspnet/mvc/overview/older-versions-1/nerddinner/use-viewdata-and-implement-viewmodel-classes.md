---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: 使用 ViewData 和实现 ViewModel 类 |Microsoft Docs
author: microsoft
description: 步骤6显示了如何启用对更丰富的窗体编辑方案的支持，并讨论了可用于将数据从控制器传递到视图的两种方法： 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435530"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a><span data-ttu-id="0e5b7-103">使用 ViewData 和实现 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="0e5b7-103">Use ViewData and Implement ViewModel Classes</span></span>

<span data-ttu-id="0e5b7-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0e5b7-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="0e5b7-105">下载 PDF</span><span class="sxs-lookup"><span data-stu-id="0e5b7-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="0e5b7-106">这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第6步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-106">This is step 6 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="0e5b7-107">步骤6显示了如何启用对更丰富的窗体编辑方案的支持，并讨论了可用于将数据从控制器传递到视图的两种方法： ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-107">Step 6 shows how enable support for richer form editing scenarios, and also discusses two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>
> 
> <span data-ttu-id="0e5b7-108">如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a><span data-ttu-id="0e5b7-109">NerdDinner 步骤6： ViewData 和 ViewModel</span><span class="sxs-lookup"><span data-stu-id="0e5b7-109">NerdDinner Step 6: ViewData and ViewModel</span></span>

<span data-ttu-id="0e5b7-110">我们介绍了大量的窗体发布方案，并讨论了如何实现创建、更新和删除（CRUD）支持。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-110">We've covered a number of form post scenarios, and discussed how to implement create, update and delete (CRUD) support.</span></span> <span data-ttu-id="0e5b7-111">现在我们将进一步 DinnersController 实现，并支持更丰富的窗体编辑方案。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-111">We'll now take our DinnersController implementation further and enable support for richer form editing scenarios.</span></span> <span data-ttu-id="0e5b7-112">在此过程中，我们将讨论可用于将数据从控制器传递到视图的两种方法： ViewData 和 ViewModel。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-112">While doing this we'll discuss two approaches that can be used to pass data from controllers to views: ViewData and ViewModel.</span></span>

### <a name="passing-data-from-controllers-to-view-templates"></a><span data-ttu-id="0e5b7-113">将数据从控制器传递到视图-模板</span><span class="sxs-lookup"><span data-stu-id="0e5b7-113">Passing Data from Controllers to View-Templates</span></span>

<span data-ttu-id="0e5b7-114">MVC 模式的一项定义特征是严格的 "问题分离"，它有助于在应用程序的不同组件之间强制实施。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-114">One of the defining characteristics of the MVC pattern is the strict "separation of concerns" it helps enforce between the different components of an application.</span></span> <span data-ttu-id="0e5b7-115">每个模型、控制器和视图都具有完善定义的角色和职责，它们彼此之间以定义的方式相互通信。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-115">Models, Controllers and Views each have well defined roles and responsibilities, and they communicate amongst each other in well defined ways.</span></span> <span data-ttu-id="0e5b7-116">这有助于提高可测试性和代码重用。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-116">This helps promote testability and code reuse.</span></span>

<span data-ttu-id="0e5b7-117">当控制器类决定向客户端呈现 HTML 响应时，它负责将呈现响应所需的所有数据显式传递给视图模板。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-117">When a Controller class decides to render an HTML response back to a client, it is responsible for explicitly passing to the view template all of the data needed to render the response.</span></span> <span data-ttu-id="0e5b7-118">视图模板不应执行任何数据检索或应用程序逻辑，而应将其限制为仅包含由控制器传递给它的模型/数据驱动的呈现代码。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-118">View templates should never perform any data retrieval or application logic – and should instead limit themselves to only have rendering code that is driven off of the model/data passed to it by the controller.</span></span>

<span data-ttu-id="0e5b7-119">现在，我们的 DinnersController 类传递到我们的视图模板的模型数据简单直接明了，其中显示了索引（）的晚餐对象的列表，并在出现详细信息（）、编辑（）、Create （）和 Delete （）的情况下使用了一个晚餐对象。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-119">Right now the model data being passed by our DinnersController class to our view templates is simple and straight-forward – a list of Dinner objects in the case of Index(), and a single Dinner object in the case of Details(), Edit(), Create() and Delete().</span></span> <span data-ttu-id="0e5b7-120">随着我们向应用程序中添加更多的 UI 功能，我们通常需要只传递此数据以在视图模板中呈现 HTML 响应。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-120">As we add more UI capabilities to our application, we are often going to need to pass more than just this data to render HTML responses within our view templates.</span></span> <span data-ttu-id="0e5b7-121">例如，我们可能需要更改编辑中的 "国家/地区" 字段，并创建 dropdownlist 为 HTML 文本框的视图。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-121">For example, we might want to change the "Country" field within our Edit and Create views from being an HTML textbox to a dropdownlist.</span></span> <span data-ttu-id="0e5b7-122">我们可能想要从我们动态填充的支持国家/地区列表中生成，而不是硬编码查看模板中的国家/地区名称列表。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-122">Rather than hard-code the dropdown list of country names in the view template, we might want to generate it from a list of supported countries that we populate dynamically.</span></span> <span data-ttu-id="0e5b7-123">我们需要一种方法，将晚餐对象*和*支持的国家/地区列表从我们的控制器传递到我们的视图模板。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-123">We will need a way to pass both the Dinner object *and* the list of supported countries from our controller to our view templates.</span></span>

<span data-ttu-id="0e5b7-124">让我们看看可以实现此目的的两种方法。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-124">Let's look at two ways we can accomplish this.</span></span>

### <a name="using-the-viewdata-dictionary"></a><span data-ttu-id="0e5b7-125">使用 ViewData 字典</span><span class="sxs-lookup"><span data-stu-id="0e5b7-125">Using the ViewData Dictionary</span></span>

<span data-ttu-id="0e5b7-126">控制器基类公开了 "ViewData" 字典属性，该属性可用于将其他数据项从控制器传递到视图。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-126">The Controller base class exposes a "ViewData" dictionary property that can be used to pass additional data items from Controllers to Views.</span></span>

<span data-ttu-id="0e5b7-127">例如，若要支持我们想要将编辑视图中的 "国家/地区" 文本框从 HTML 文本框更改为 dropdownlist 的方案，我们可以更新 Edit （）操作方法以传递（除了晚餐对象） SelectList 对象，该对象可用作 mdropdownlist 的模型。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-127">For example, to support the scenario where we want to change the "Country" textbox within our Edit view from being an HTML textbox to a dropdownlist, we can update our Edit() action method to pass (in addition to a Dinner object) a SelectList object that can be used as the model of a countries dropdownlist.</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

<span data-ttu-id="0e5b7-128">上述 SelectList 的构造函数将接受用来填充 downlist 的县列表，以及当前选定的值。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-128">The constructor of the SelectList above is accepting a list of counties to populate the drop-downlist with, as well as the currently selected value.</span></span>

<span data-ttu-id="0e5b7-129">然后，我们可以更新我们的 "Edit .aspx" 视图模板，以使用我们之前使用的 Html. TextBox （） helper 方法，而不是使用的 Html. TextBox （） helper 方法。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-129">We can then update our Edit.aspx view template to use the Html.DropDownList() helper method instead of the Html.TextBox() helper method we used previously:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

<span data-ttu-id="0e5b7-130">上面的 DropDownList （） helper 方法使用两个参数。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-130">The Html.DropDownList() helper method above takes two parameters.</span></span> <span data-ttu-id="0e5b7-131">第一个是要输出的 HTML form 元素的名称。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-131">The first is the name of the HTML form element to output.</span></span> <span data-ttu-id="0e5b7-132">第二个是通过 ViewData 字典传递的 "SelectList" 模型。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-132">The second is the "SelectList" model we passed via the ViewData dictionary.</span></span> <span data-ttu-id="0e5b7-133">我们使用C# "as" 关键字将字典中的类型转换为 SelectList。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-133">We are using the C# "as" keyword to cast the type within the dictionary as a SelectList.</span></span>

<span data-ttu-id="0e5b7-134">现在，当我们运行应用程序并在浏览器中访问 */Dinners/Edit/1* URL 时，我们将看到编辑 UI 已更新，以显示 dropdownlist 的国家/地区，而不是文本框：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-134">And now when we run our application and access the */Dinners/Edit/1* URL within our browser we'll see that our edit UI has been updated to display a dropdownlist of countries instead of a textbox:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

<span data-ttu-id="0e5b7-135">由于我们还会从 HTTP-POST 编辑方法呈现编辑视图模板（在发生错误的情况下），因此我们将需要确保在错误情况下呈现视图模板时，我们还将更新此方法以将 SelectList 添加到 ViewData 中：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-135">Because we also render the Edit view template from the HTTP-POST Edit method (in scenarios when errors occur), we'll want to make sure that we also update this method to add the SelectList to ViewData when the view template is rendered in error scenarios:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

<span data-ttu-id="0e5b7-136">现在我们的 DinnersController 编辑方案支持 DropDownList。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-136">And now our DinnersController edit scenario supports a DropDownList.</span></span>

### <a name="using-a-viewmodel-pattern"></a><span data-ttu-id="0e5b7-137">使用 ViewModel 模式</span><span class="sxs-lookup"><span data-stu-id="0e5b7-137">Using a ViewModel Pattern</span></span>

<span data-ttu-id="0e5b7-138">ViewData 字典方法的好处是，实现起来非常快捷快捷。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-138">The ViewData dictionary approach has the benefit of being fairly fast and easy to implement.</span></span> <span data-ttu-id="0e5b7-139">不过，某些开发人员不喜欢使用基于字符串的字典，因为键入错误会导致编译时不会捕获到错误。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-139">Some developers don't like using string-based dictionaries, though, since typos can lead to errors that will not be caught at compile-time.</span></span> <span data-ttu-id="0e5b7-140">使用强类型化语言（如C#在视图模板中）时，非类型化的 ViewData 字典还需要使用 "as" 运算符或强制转换。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-140">The un-typed ViewData dictionary also requires using the "as" operator or casting when using a strongly-typed language like C# in a view template.</span></span>

<span data-ttu-id="0e5b7-141">我们可以使用的另一种方法是 "ViewModel" 模式。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-141">An alternative approach that we could use is one often referred to as the "ViewModel" pattern.</span></span> <span data-ttu-id="0e5b7-142">使用此模式时，我们将创建针对特定视图方案进行了优化的强类型类，并公开了视图模板所需的动态值/内容的属性。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-142">When using this pattern we create strongly-typed classes that are optimized for our specific view scenarios, and which expose properties for the dynamic values/content needed by our view templates.</span></span> <span data-ttu-id="0e5b7-143">然后，控制器类可以填充这些视图优化类并将其传递给视图模板以供使用。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-143">Our controller classes can then populate and pass these view-optimized classes to our view template to use.</span></span> <span data-ttu-id="0e5b7-144">这会在视图模板中启用类型安全、编译时检查和编辑器 intellisense。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-144">This enables type-safety, compile-time checking, and editor intellisense within view templates.</span></span>

<span data-ttu-id="0e5b7-145">例如，若要启用晚餐窗体编辑方案，我们可以创建一个如下所示的 "DinnerFormViewModel" 类，该类公开两个强类型的属性：晚餐对象和填充国家 dropdownlist 所需的 SelectList 模型：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-145">For example, to enable dinner form editing scenarios we can create a "DinnerFormViewModel" class like below that exposes two strongly-typed properties: a Dinner object, and the SelectList model needed to populate the countries dropdownlist:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

<span data-ttu-id="0e5b7-146">然后，可以使用我们从存储库中检索到的晚餐对象，更新 Edit （）操作方法来创建 DinnerFormViewModel，然后将其传递到我们的视图模板：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-146">We can then update our Edit() action method to create the DinnerFormViewModel using the Dinner object we retrieve from our repository, and then pass it to our view template:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

<span data-ttu-id="0e5b7-147">接下来，我们将更新视图模板，使其需要一个 "DinnerFormViewModel" 而不是 "晚餐" 对象，方法是更改 "编辑 .aspx" 页顶部的 "继承" 属性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-147">We'll then update our view template so that it expects a "DinnerFormViewModel" instead of a "Dinner" object by changing the "inherits" attribute at the top of the edit.aspx page like so:</span></span>

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

<span data-ttu-id="0e5b7-148">完成此操作后，我们的视图模板中的 "模型" 属性的 intellisense 将会更新，以反映我们传递它的 DinnerFormViewModel 类型的对象模型：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-148">Once we do this, the intellisense of the "Model" property within our view template will be updated to reflect the object model of the DinnerFormViewModel type we are passing it:</span></span>

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

<span data-ttu-id="0e5b7-149">然后，我们可以更新我们的视图代码来处理它。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-149">We can then update our view code to work off of it.</span></span> <span data-ttu-id="0e5b7-150">请注意，我们不会更改我们正在创建的输入元素的名称（窗体元素仍将命名为 "Title"、"国家/地区"），但我们正在更新 HTML 帮助器方法以使用 DinnerFormViewModel 类检索值：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-150">Notice below how we are not changing the names of the input elements we are creating (the form elements will still be named "Title", "Country") – but we are updating the HTML Helper methods to retrieve the values using the DinnerFormViewModel class:</span></span>

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

<span data-ttu-id="0e5b7-151">在呈现错误时，我们还将更新编辑 post 方法以使用 DinnerFormViewModel 类：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-151">We'll also update our Edit post method to use the DinnerFormViewModel class when rendering errors:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

<span data-ttu-id="0e5b7-152">我们还可以更新 Create （）操作方法，以便重复使用完全相同的*DinnerFormViewModel*类，以便在这些国家/地区中 DropDownList。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-152">We can also update our Create() action methods to re-use the exact same *DinnerFormViewModel* class to enable the countries DropDownList within those as well.</span></span> <span data-ttu-id="0e5b7-153">下面是 HTTP GET 实现：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-153">Below is the HTTP-GET implementation:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

<span data-ttu-id="0e5b7-154">下面是 HTTP POST Create 方法的实现：</span><span class="sxs-lookup"><span data-stu-id="0e5b7-154">Below is the implementation of the HTTP-POST Create method:</span></span>

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

<span data-ttu-id="0e5b7-155">同时，我们的 "编辑" 和 "创建" 屏幕支持用于挑选国家/地区的下拉 downlists。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-155">And now both our Edit and Create screens support drop-downlists for picking the country.</span></span>

### <a name="custom-shaped-viewmodel-classes"></a><span data-ttu-id="0e5b7-156">自定义形状的 ViewModel 类</span><span class="sxs-lookup"><span data-stu-id="0e5b7-156">Custom-shaped ViewModel classes</span></span>

<span data-ttu-id="0e5b7-157">在上述方案中，我们的 DinnerFormViewModel 类直接将晚餐模型对象公开为属性，同时将支持 SelectList 模型属性公开。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-157">In the scenario above, our DinnerFormViewModel class directly exposes the Dinner model object as a property, along with a supporting SelectList model property.</span></span> <span data-ttu-id="0e5b7-158">如果我们要在视图模板中创建的 HTML UI 相对接近我们的域模型对象，则此方法适用于这种情况。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-158">This approach works fine for scenarios where the HTML UI we want to create within our view template corresponds relatively closely to our domain model objects.</span></span>

<span data-ttu-id="0e5b7-159">对于这种情况不是这样的情况，可以使用的一种方法是创建一个自定义形状的 ViewModel 类，该类的对象模型对视图的使用进行了更多的优化，并可能与基础域模型对象完全不同。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-159">For scenarios where this isn't the case, one option that you can use is to create a custom-shaped ViewModel class whose object model is more optimized for consumption by the view – and which might look completely different from the underlying domain model object.</span></span> <span data-ttu-id="0e5b7-160">例如，它可能会公开从多个模型对象中收集的不同属性名称和/或聚合属性。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-160">For example, it could potentially expose different property names and/or aggregate properties collected from multiple model objects.</span></span>

<span data-ttu-id="0e5b7-161">自定义形状的 ViewModel 类可用于将数据从控制器传递到要呈现的视图，以及帮助处理回发到控制器操作方法的窗体数据。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-161">Custom-shaped ViewModel classes can be used both to pass data from controllers to views to render, as well as to help handle form data posted back to a controller's action method.</span></span> <span data-ttu-id="0e5b7-162">对于此后一种情况，您可能让操作方法使用窗体发布数据更新 ViewModel 对象，然后使用 ViewModel 实例映射或检索实际的域模型对象。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-162">For this later scenario, you might have the action method update a ViewModel object with the form-posted data, and then use the ViewModel instance to map or retrieve an actual domain model object.</span></span>

<span data-ttu-id="0e5b7-163">自定义形状的 ViewModel 类可以提供很大的灵活性，并且可以在任何时候在视图模板内查找呈现代码，或在操作方法内的窗体发布代码太复杂时进行调查。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-163">Custom-shaped ViewModel classes can provide a great deal of flexibility, and are something to investigate any time you find the rendering code within your view templates or the form-posting code inside your action methods starting to get too complicated.</span></span> <span data-ttu-id="0e5b7-164">这通常是因为您的域模型并不完全对应于您所生成的 UI，并且中间的自定义形状的 ViewModel 类可以帮助。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-164">This is often a sign that your domain models don't cleanly correspond to the UI you are generating, and that an intermediate custom-shaped ViewModel class can help.</span></span>

### <a name="next-step"></a><span data-ttu-id="0e5b7-165">下一步</span><span class="sxs-lookup"><span data-stu-id="0e5b7-165">Next Step</span></span>

<span data-ttu-id="0e5b7-166">现在我们来看看如何使用分区和母版页跨应用程序重复使用和共享 UI。</span><span class="sxs-lookup"><span data-stu-id="0e5b7-166">Let's now look at how we can use partials and master-pages to re-use and share UI across our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0e5b7-167">[上一页](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [下一页](re-use-ui-using-master-pages-and-partials.md)</span><span class="sxs-lookup"><span data-stu-id="0e5b7-167">[Previous](provide-crud-create-read-update-delete-data-form-entry-support.md)
[Next](re-use-ui-using-master-pages-and-partials.md)</span></span>
