---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 创建数据传输对象（Dto） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445757"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="c0086-102">创建数据传输对象 (DTO)</span><span class="sxs-lookup"><span data-stu-id="c0086-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="c0086-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c0086-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c0086-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="c0086-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="c0086-105">现在，web API 将数据库实体公开给客户端。</span><span class="sxs-lookup"><span data-stu-id="c0086-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="c0086-106">客户端接收直接映射到数据库表的数据。</span><span class="sxs-lookup"><span data-stu-id="c0086-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="c0086-107">但是，这并不总是一个好主意。</span><span class="sxs-lookup"><span data-stu-id="c0086-107">However, that's not always a good idea.</span></span> <span data-ttu-id="c0086-108">有时，您需要更改发送到客户端的数据的形状。</span><span class="sxs-lookup"><span data-stu-id="c0086-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="c0086-109">例如，你可能希望：</span><span class="sxs-lookup"><span data-stu-id="c0086-109">For example, you might want to:</span></span>

- <span data-ttu-id="c0086-110">删除循环引用（请参阅上一节）。</span><span class="sxs-lookup"><span data-stu-id="c0086-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="c0086-111">隐藏客户端不应查看的特定属性。</span><span class="sxs-lookup"><span data-stu-id="c0086-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="c0086-112">省略某些属性以减小负载大小。</span><span class="sxs-lookup"><span data-stu-id="c0086-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="c0086-113">平展包含嵌套对象的对象图，以使它们更适合客户端。</span><span class="sxs-lookup"><span data-stu-id="c0086-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="c0086-114">避免出现 "过度发布" 漏洞。</span><span class="sxs-lookup"><span data-stu-id="c0086-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="c0086-115">（有关过多发布的讨论，请参阅[模型验证](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。）</span><span class="sxs-lookup"><span data-stu-id="c0086-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="c0086-116">将服务层与数据库层分离。</span><span class="sxs-lookup"><span data-stu-id="c0086-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="c0086-117">若要实现此目的，可以定义*数据传输对象*（DTO）。</span><span class="sxs-lookup"><span data-stu-id="c0086-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="c0086-118">DTO 是定义如何通过网络发送数据的对象。</span><span class="sxs-lookup"><span data-stu-id="c0086-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="c0086-119">让我们看看如何使用 Book 实体。</span><span class="sxs-lookup"><span data-stu-id="c0086-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="c0086-120">在 "模型" 文件夹中，添加两个 DTO 类：</span><span class="sxs-lookup"><span data-stu-id="c0086-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="c0086-121">`BookDetailDto` 类包括书籍模型中的所有属性，但 `AuthorName` 是将包含作者姓名的字符串。</span><span class="sxs-lookup"><span data-stu-id="c0086-121">The `BookDetailDto` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="c0086-122">`BookDto` 类包含 `BookDetailDto`中的属性子集。</span><span class="sxs-lookup"><span data-stu-id="c0086-122">The `BookDto` class contains a subset of properties from `BookDetailDto`.</span></span>

<span data-ttu-id="c0086-123">接下来，将 `BooksController` 类中的两个 GET 方法替换为返回 Dto 的版本。</span><span class="sxs-lookup"><span data-stu-id="c0086-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="c0086-124">我们将使用 LINQ **Select**语句将书籍实体转换为 dto。</span><span class="sxs-lookup"><span data-stu-id="c0086-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="c0086-125">下面是新 `GetBooks` 方法生成的 SQL。</span><span class="sxs-lookup"><span data-stu-id="c0086-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="c0086-126">您可以看到，EF 将 LINQ **select**转换为 SQL select 语句。</span><span class="sxs-lookup"><span data-stu-id="c0086-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="c0086-127">最后，修改 `PostBook` 方法以返回一个 DTO。</span><span class="sxs-lookup"><span data-stu-id="c0086-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="c0086-128">在本教程中，我们将在代码中手动转换为 Dto。</span><span class="sxs-lookup"><span data-stu-id="c0086-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="c0086-129">另一种方法是使用[AutoMapper](http://automapper.org/)等库来自动处理转换。</span><span class="sxs-lookup"><span data-stu-id="c0086-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="c0086-130">[上一页](part-4.md)
> [下一页](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="c0086-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>
