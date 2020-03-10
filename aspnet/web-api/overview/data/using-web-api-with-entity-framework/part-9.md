---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 向数据库添加新项 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448970"
---
# <a name="add-a-new-item-to-the-database"></a><span data-ttu-id="61454-102">向数据库添加一个新项</span><span class="sxs-lookup"><span data-stu-id="61454-102">Add a New Item to the Database</span></span>

<span data-ttu-id="61454-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="61454-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="61454-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="61454-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="61454-105">在本部分中，你将添加用户创建新书籍的能力。</span><span class="sxs-lookup"><span data-stu-id="61454-105">In this section, you will add the ability for users to create a new book.</span></span> <span data-ttu-id="61454-106">在 node.js 中，将以下代码添加到视图模型：</span><span class="sxs-lookup"><span data-stu-id="61454-106">In app.js, add the following code to the view model:</span></span>

[!code-javascript[Main](part-9/samples/sample1.js)]

<span data-ttu-id="61454-107">在 "索引" 中，替换以下标记：</span><span class="sxs-lookup"><span data-stu-id="61454-107">In Index.cshtml, replace the following markup:</span></span>

[!code-html[Main](part-9/samples/sample2.html)]

<span data-ttu-id="61454-108">替换为：</span><span class="sxs-lookup"><span data-stu-id="61454-108">With:</span></span>

[!code-html[Main](part-9/samples/sample3.html)]

<span data-ttu-id="61454-109">此标记创建用于提交新作者的窗体。</span><span class="sxs-lookup"><span data-stu-id="61454-109">This markup creates a form for submitting a new author.</span></span> <span data-ttu-id="61454-110">"作者" 下拉列表的值被数据绑定到视图模型中的 `authors` 可见。</span><span class="sxs-lookup"><span data-stu-id="61454-110">The values for the author drop-down list are data-bound to the `authors` observable in the view model.</span></span> <span data-ttu-id="61454-111">对于其他窗体输入，值被数据绑定到视图模型的 `newBook` 属性。</span><span class="sxs-lookup"><span data-stu-id="61454-111">For the other form inputs, the values are data-bound to the `newBook` property of the view model.</span></span>

<span data-ttu-id="61454-112">窗体上的提交处理程序绑定到 `addBook` 函数：</span><span class="sxs-lookup"><span data-stu-id="61454-112">The submit handler on the form is bound to the `addBook` function:</span></span>

[!code-html[Main](part-9/samples/sample4.html)]

<span data-ttu-id="61454-113">`addBook` 函数读取数据绑定窗体输入的当前值，以创建 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="61454-113">The `addBook` function reads the current values of the data-bound form inputs to create a JSON object.</span></span> <span data-ttu-id="61454-114">然后，它将 JSON 对象发送到 `/api/books`。</span><span class="sxs-lookup"><span data-stu-id="61454-114">Then it POSTs the JSON object to `/api/books`.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="61454-115">[上一页](part-8.md)
> [下一页](part-10.md)</span><span class="sxs-lookup"><span data-stu-id="61454-115">[Previous](part-8.md)
[Next](part-10.md)</span></span>
