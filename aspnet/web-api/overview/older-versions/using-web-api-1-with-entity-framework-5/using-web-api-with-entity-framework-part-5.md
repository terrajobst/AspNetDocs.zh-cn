---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 第5部分：使用挖空创建动态 UI |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599999"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="ebb39-102">第5部分：使用挖空创建动态 UI</span><span class="sxs-lookup"><span data-stu-id="ebb39-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="ebb39-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ebb39-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ebb39-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="ebb39-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="ebb39-105">使用 Knockout.js 创建动态 UI</span><span class="sxs-lookup"><span data-stu-id="ebb39-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="ebb39-106">在本部分中，我们将使用 "挖空" 将功能添加到 "管理" 视图。</span><span class="sxs-lookup"><span data-stu-id="ebb39-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="ebb39-107">"[挖空](http://knockoutjs.com/)" 是一种 Javascript 库，可轻松地将 HTML 控件绑定到数据。</span><span class="sxs-lookup"><span data-stu-id="ebb39-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="ebb39-108">挖空 node.js 使用模型-视图-ViewModel （MVVM）模式。</span><span class="sxs-lookup"><span data-stu-id="ebb39-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="ebb39-109">*模型*是业务域中的数据的服务器端表示形式（在我们的示例中，是产品和订单）。</span><span class="sxs-lookup"><span data-stu-id="ebb39-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="ebb39-110">*视图*为表示层（HTML）。</span><span class="sxs-lookup"><span data-stu-id="ebb39-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="ebb39-111">*视图模型*是包含模型数据的 Javascript 对象。</span><span class="sxs-lookup"><span data-stu-id="ebb39-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="ebb39-112">视图模型是 UI 的代码抽象。</span><span class="sxs-lookup"><span data-stu-id="ebb39-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="ebb39-113">它不知道 HTML 表示形式。</span><span class="sxs-lookup"><span data-stu-id="ebb39-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="ebb39-114">相反，它表示视图的抽象功能，如 "项目列表"。</span><span class="sxs-lookup"><span data-stu-id="ebb39-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="ebb39-115">视图被数据绑定到视图模型。</span><span class="sxs-lookup"><span data-stu-id="ebb39-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="ebb39-116">视图模型的更新会自动反映在视图中。</span><span class="sxs-lookup"><span data-stu-id="ebb39-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="ebb39-117">视图模型还可获取视图中的事件（如按钮单击），并在模型上执行操作，例如创建订单。</span><span class="sxs-lookup"><span data-stu-id="ebb39-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="ebb39-118">首先，我们将定义视图模型。</span><span class="sxs-lookup"><span data-stu-id="ebb39-118">First we'll define the view-model.</span></span> <span data-ttu-id="ebb39-119">之后，我们将 HTML 标记绑定到视图模型。</span><span class="sxs-lookup"><span data-stu-id="ebb39-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="ebb39-120">将以下 Razor 节添加到管理员：</span><span class="sxs-lookup"><span data-stu-id="ebb39-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="ebb39-121">可以将此部分添加到文件中的任何位置。</span><span class="sxs-lookup"><span data-stu-id="ebb39-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="ebb39-122">呈现视图时，该部分将显示在 HTML 页的底部，位于关闭 &lt;/body&gt; 标记之前。</span><span class="sxs-lookup"><span data-stu-id="ebb39-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="ebb39-123">此页的所有脚本都将进入注释指示的脚本标记内：</span><span class="sxs-lookup"><span data-stu-id="ebb39-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="ebb39-124">首先，定义视图模型类：</span><span class="sxs-lookup"><span data-stu-id="ebb39-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="ebb39-125">**observableArray**是挖空的特殊对象，称为可*观察*对象。</span><span class="sxs-lookup"><span data-stu-id="ebb39-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="ebb39-126">从[挖空的 .js 文档](http://knockoutjs.com/documentation/observables.html)：可观测对象是一个 "JavaScript 对象，可通知订阅服务器的更改"。</span><span class="sxs-lookup"><span data-stu-id="ebb39-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="ebb39-127">当可观察的内容更改时，视图将自动更新以匹配。</span><span class="sxs-lookup"><span data-stu-id="ebb39-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="ebb39-128">若要填充 `products` 数组，请向 web API 发出 AJAX 请求。</span><span class="sxs-lookup"><span data-stu-id="ebb39-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="ebb39-129">回忆一下，我们已将 API 的基本 URI 存储在视图包中（请参阅本教程的第[4 部分](using-web-api-with-entity-framework-part-4.md)）。</span><span class="sxs-lookup"><span data-stu-id="ebb39-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="ebb39-130">接下来，将函数添加到视图模型，以创建、更新和删除产品。</span><span class="sxs-lookup"><span data-stu-id="ebb39-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="ebb39-131">这些函数将 AJAX 调用提交到 web API，并使用结果来更新视图模型。</span><span class="sxs-lookup"><span data-stu-id="ebb39-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="ebb39-132">现在最重要的部分是： fulled 加载 DOM 时，调用**applyBindings**函数并传入 `ProductsViewModel`的新实例：</span><span class="sxs-lookup"><span data-stu-id="ebb39-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="ebb39-133">**ApplyBindings**方法激活视图模型与视图的挖空和连线。</span><span class="sxs-lookup"><span data-stu-id="ebb39-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="ebb39-134">现在我们有了一个视图模型，接下来可以创建绑定。</span><span class="sxs-lookup"><span data-stu-id="ebb39-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="ebb39-135">在挖空中，可以通过将 `data-bind` 特性添加到 HTML 元素来实现此目的。</span><span class="sxs-lookup"><span data-stu-id="ebb39-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="ebb39-136">例如，若要将 HTML 列表绑定到数组，请使用 `foreach` 绑定：</span><span class="sxs-lookup"><span data-stu-id="ebb39-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="ebb39-137">`foreach` 绑定将循环访问数组，并为数组中的每个对象创建子元素。</span><span class="sxs-lookup"><span data-stu-id="ebb39-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="ebb39-138">子元素上的绑定可以引用数组对象中的属性。</span><span class="sxs-lookup"><span data-stu-id="ebb39-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="ebb39-139">将以下绑定添加到 "更新产品" 列表：</span><span class="sxs-lookup"><span data-stu-id="ebb39-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="ebb39-140">`<li>` 元素出现在**foreach**绑定的作用域内。</span><span class="sxs-lookup"><span data-stu-id="ebb39-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="ebb39-141">这意味着，挖空会针对 `products` 数组中的每个产品呈现一次元素。</span><span class="sxs-lookup"><span data-stu-id="ebb39-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="ebb39-142">`<li>` 元素中的所有绑定都引用该产品实例。</span><span class="sxs-lookup"><span data-stu-id="ebb39-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="ebb39-143">例如，`$data.Name` 引用产品的 `Name` 属性。</span><span class="sxs-lookup"><span data-stu-id="ebb39-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="ebb39-144">若要设置文本输入的值，请使用 `value` 绑定。</span><span class="sxs-lookup"><span data-stu-id="ebb39-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="ebb39-145">使用 `click` 绑定将这些按钮绑定到模型视图上的函数。</span><span class="sxs-lookup"><span data-stu-id="ebb39-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="ebb39-146">产品实例作为参数传递给每个函数。</span><span class="sxs-lookup"><span data-stu-id="ebb39-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="ebb39-147">有关详细信息，请[参阅 "挖空](http://knockoutjs.com/documentation/observables.html)的" 文档对各种绑定有很好的说明。</span><span class="sxs-lookup"><span data-stu-id="ebb39-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="ebb39-148">接下来，在 "添加产品" 窗体上为**提交**事件添加绑定：</span><span class="sxs-lookup"><span data-stu-id="ebb39-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="ebb39-149">此绑定对视图模型调用 `create` 函数来创建新产品。</span><span class="sxs-lookup"><span data-stu-id="ebb39-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="ebb39-150">下面是管理视图的完整代码：</span><span class="sxs-lookup"><span data-stu-id="ebb39-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="ebb39-151">运行应用程序，用管理员帐户登录，然后单击 "管理员" 链接。</span><span class="sxs-lookup"><span data-stu-id="ebb39-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="ebb39-152">应会看到产品列表，并能够创建、更新或删除产品。</span><span class="sxs-lookup"><span data-stu-id="ebb39-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ebb39-153">[上一页](using-web-api-with-entity-framework-part-4.md)
> [下一页](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="ebb39-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
