---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: 创建 JavaScript 客户端 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504722"
---
# <a name="create-the-javascript-client"></a><span data-ttu-id="5038e-102">创建 JavaScript 客户端</span><span class="sxs-lookup"><span data-stu-id="5038e-102">Create the JavaScript Client</span></span>

<span data-ttu-id="5038e-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5038e-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5038e-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="5038e-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="5038e-105">在本部分中，你将使用 HTML、JavaScript 和[挖空的 node.js](http://knockoutjs.com/)库创建应用程序的客户端。</span><span class="sxs-lookup"><span data-stu-id="5038e-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="5038e-106">我们将分阶段生成客户端应用：</span><span class="sxs-lookup"><span data-stu-id="5038e-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="5038e-107">显示书籍列表。</span><span class="sxs-lookup"><span data-stu-id="5038e-107">Showing a list of books.</span></span>
- <span data-ttu-id="5038e-108">显示书籍详细信息。</span><span class="sxs-lookup"><span data-stu-id="5038e-108">Showing a book detail.</span></span>
- <span data-ttu-id="5038e-109">添加新书籍。</span><span class="sxs-lookup"><span data-stu-id="5038e-109">Adding a new book.</span></span>

<span data-ttu-id="5038e-110">挖空库使用模型-视图-ViewModel （MVVM）模式：</span><span class="sxs-lookup"><span data-stu-id="5038e-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="5038e-111">**模型**是业务域中的数据的服务器端表示形式（在我们的示例中为书籍和作者）。</span><span class="sxs-lookup"><span data-stu-id="5038e-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="5038e-112">**视图**为表示层（HTML）。</span><span class="sxs-lookup"><span data-stu-id="5038e-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="5038e-113">**视图模型**是保存模型的 JavaScript 对象。</span><span class="sxs-lookup"><span data-stu-id="5038e-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="5038e-114">视图模型是 UI 的代码抽象。</span><span class="sxs-lookup"><span data-stu-id="5038e-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="5038e-115">它不知道 HTML 表示形式。</span><span class="sxs-lookup"><span data-stu-id="5038e-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="5038e-116">相反，它表示视图的抽象功能，如&quot;&quot;书籍的列表。</span><span class="sxs-lookup"><span data-stu-id="5038e-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="5038e-117">视图被数据绑定到视图模型。</span><span class="sxs-lookup"><span data-stu-id="5038e-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="5038e-118">视图模型的更新会自动反映在视图中。</span><span class="sxs-lookup"><span data-stu-id="5038e-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="5038e-119">视图模型还可从视图中获取事件，如按钮单击。</span><span class="sxs-lookup"><span data-stu-id="5038e-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="5038e-120">此方法可以轻松地更改应用的布局和 UI，因为可以更改绑定，而无需重写任何代码。</span><span class="sxs-lookup"><span data-stu-id="5038e-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="5038e-121">例如，可以将项目列表显示为 `<ul>`，然后将其更改为表。</span><span class="sxs-lookup"><span data-stu-id="5038e-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="5038e-122">添加挖空库</span><span class="sxs-lookup"><span data-stu-id="5038e-122">Add the Knockout Library</span></span>

<span data-ttu-id="5038e-123">在 Visual Studio 中，从“工具”菜单中选择“NuGet 包管理器”。</span><span class="sxs-lookup"><span data-stu-id="5038e-123">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="5038e-124">然后选择 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="5038e-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="5038e-125">在“Package Manager Console”窗口中，输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="5038e-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="5038e-126">此命令将挖空文件添加到 Scripts 文件夹。</span><span class="sxs-lookup"><span data-stu-id="5038e-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="5038e-127">创建视图模型</span><span class="sxs-lookup"><span data-stu-id="5038e-127">Create the View Model</span></span>

<span data-ttu-id="5038e-128">将名为 node.js 的 JavaScript 文件添加到 Scripts 文件夹。</span><span class="sxs-lookup"><span data-stu-id="5038e-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="5038e-129">（在解决方案资源管理器中，右键单击 "脚本" 文件夹，选择 "**添加**"，然后选择 " **JavaScript 文件**"。）粘贴以下代码：</span><span class="sxs-lookup"><span data-stu-id="5038e-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="5038e-130">在挖空中，`observable` 类启用数据绑定。</span><span class="sxs-lookup"><span data-stu-id="5038e-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="5038e-131">当可观察的内容发生更改时，可观察的会通知所有数据绑定控件，因此它们可以自行更新。</span><span class="sxs-lookup"><span data-stu-id="5038e-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="5038e-132">（`observableArray` 类是可*观察*的数组版本。）首先，我们的视图模型有两个可观察量：</span><span class="sxs-lookup"><span data-stu-id="5038e-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="5038e-133">`books` 包含书籍的列表。</span><span class="sxs-lookup"><span data-stu-id="5038e-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="5038e-134">如果 AJAX 调用失败，`error` 将包含一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="5038e-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="5038e-135">`getAllBooks` 方法进行 AJAX 调用以获取书籍列表。</span><span class="sxs-lookup"><span data-stu-id="5038e-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="5038e-136">然后将结果推送到 `books` 数组。</span><span class="sxs-lookup"><span data-stu-id="5038e-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="5038e-137">`ko.applyBindings` 方法是挖空库的一部分。</span><span class="sxs-lookup"><span data-stu-id="5038e-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="5038e-138">它将视图模型作为参数，并设置数据绑定。</span><span class="sxs-lookup"><span data-stu-id="5038e-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="5038e-139">添加脚本捆绑包</span><span class="sxs-lookup"><span data-stu-id="5038e-139">Add a Script Bundle</span></span>

<span data-ttu-id="5038e-140">绑定是 ASP.NET 4.5 中的一项功能，它使你可以轻松地将多个文件组合或捆绑到一个文件中。</span><span class="sxs-lookup"><span data-stu-id="5038e-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="5038e-141">绑定可减少向服务器发出的请求数，从而提高页面加载时间。</span><span class="sxs-lookup"><span data-stu-id="5038e-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="5038e-142">打开文件应用\_Start/BundleConfig。</span><span class="sxs-lookup"><span data-stu-id="5038e-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="5038e-143">将以下代码添加到 RegisterBundles 方法。</span><span class="sxs-lookup"><span data-stu-id="5038e-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="5038e-144">[上一页](part-5.md)
> [下一页](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="5038e-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
