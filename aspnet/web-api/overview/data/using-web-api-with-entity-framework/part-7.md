---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-7
title: 创建视图（UI） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: b2445062-a1fe-4133-8994-f510280f6d9a
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-7
msc.type: authoredcontent
ms.openlocfilehash: 62c4523c2c6fb399cfbc3716309a1379996d601c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448982"
---
# <a name="create-the-view-ui"></a><span data-ttu-id="0c37a-102">创建视图 (UI)</span><span class="sxs-lookup"><span data-stu-id="0c37a-102">Create the View (UI)</span></span>

<span data-ttu-id="0c37a-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0c37a-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="0c37a-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="0c37a-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="0c37a-105">在本部分中，你将开始定义应用程序的 HTML，并在 HTML 与视图模型之间添加数据绑定。</span><span class="sxs-lookup"><span data-stu-id="0c37a-105">In this section, you will start to define the HTML for the app, and add data binding between the HTML and the view model.</span></span>

<span data-ttu-id="0c37a-106">打开文件视图/Home/Index。</span><span class="sxs-lookup"><span data-stu-id="0c37a-106">Open the file Views/Home/Index.cshtml.</span></span> <span data-ttu-id="0c37a-107">将该文件的整个内容替换为以下内容。</span><span class="sxs-lookup"><span data-stu-id="0c37a-107">Replace the entire contents of that file with the following.</span></span>

[!code-cshtml[Main](part-7/samples/sample1.cshtml)]

<span data-ttu-id="0c37a-108">大多数 `div` 元素都适用于[启动](http://getbootstrap.com/)样式设置。</span><span class="sxs-lookup"><span data-stu-id="0c37a-108">Most of the `div` elements are there for [Bootstrap](http://getbootstrap.com/) styling.</span></span> <span data-ttu-id="0c37a-109">重要元素是具有 `data-bind` 特性的元素。</span><span class="sxs-lookup"><span data-stu-id="0c37a-109">The important elements are the ones with `data-bind` attributes.</span></span> <span data-ttu-id="0c37a-110">此属性将 HTML 链接到视图模型。</span><span class="sxs-lookup"><span data-stu-id="0c37a-110">This attribute links the HTML to the view model.</span></span>

<span data-ttu-id="0c37a-111">例如:</span><span class="sxs-lookup"><span data-stu-id="0c37a-111">For example:</span></span>

[!code-html[Main](part-7/samples/sample2.html)]

<span data-ttu-id="0c37a-112">在此示例中，&quot;`text`&quot; 绑定导致 `<p>` 元素显示视图模型中 `error` 属性的值。</span><span class="sxs-lookup"><span data-stu-id="0c37a-112">In this example, the &quot;`text`&quot; binding causes the `<p>` element to show the value of the `error` property from the view model.</span></span> <span data-ttu-id="0c37a-113">请记住，`error` 被声明为 `ko.observable`：</span><span class="sxs-lookup"><span data-stu-id="0c37a-113">Recall that `error` was declared as a `ko.observable`:</span></span>

[!code-javascript[Main](part-7/samples/sample3.js)]

<span data-ttu-id="0c37a-114">每当将新值分配给 `error`时，挖空会更新 `<p>` 元素中的文本。</span><span class="sxs-lookup"><span data-stu-id="0c37a-114">Whenever a new value is assigned to `error`, Knockout updates the text in the `<p>` element.</span></span>

<span data-ttu-id="0c37a-115">`foreach` 绑定通知挖空以循环遍历 `books` 数组的内容。</span><span class="sxs-lookup"><span data-stu-id="0c37a-115">The `foreach` binding tells Knockout to loop through the contents of the `books` array.</span></span> <span data-ttu-id="0c37a-116">对于数组中的每个项，挖空会创建一个新的 &lt;li&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="0c37a-116">For each item in the array, Knockout creates a new &lt;li&gt; element.</span></span> <span data-ttu-id="0c37a-117">上下文中的绑定 `foreach` 引用数组项的属性。</span><span class="sxs-lookup"><span data-stu-id="0c37a-117">Bindings inside the context of the `foreach` refer to properties on the array item.</span></span> <span data-ttu-id="0c37a-118">例如:</span><span class="sxs-lookup"><span data-stu-id="0c37a-118">For example:</span></span>

[!code-html[Main](part-7/samples/sample4.html)]

<span data-ttu-id="0c37a-119">此处 `text` 绑定读取每本书的 Author 属性。</span><span class="sxs-lookup"><span data-stu-id="0c37a-119">Here the `text` binding reads the Author property of each book.</span></span>

<span data-ttu-id="0c37a-120">如果现在运行应用程序，其外观应如下所示：</span><span class="sxs-lookup"><span data-stu-id="0c37a-120">If you run the application now, it should look like this:</span></span>

![](part-7/_static/image1.png)

<span data-ttu-id="0c37a-121">加载页面后，将以异步方式加载书籍的列表。</span><span class="sxs-lookup"><span data-stu-id="0c37a-121">The list of books loads asynchronously, after the page loads.</span></span> <span data-ttu-id="0c37a-122">现在，&quot; 链接的 &quot;详细信息不起作用。</span><span class="sxs-lookup"><span data-stu-id="0c37a-122">Right now, the &quot;Details&quot; links are not functional.</span></span> <span data-ttu-id="0c37a-123">我们将在下一节中添加此功能。</span><span class="sxs-lookup"><span data-stu-id="0c37a-123">We'll add this functionality in the next section.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0c37a-124">[上一页](part-6.md)
> [下一页](part-8.md)</span><span class="sxs-lookup"><span data-stu-id="0c37a-124">[Previous](part-6.md)
[Next](part-8.md)</span></span>
