---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 第3部分：创建管理控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447908"
---
# <a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="49de5-102">第3部分：创建管理控制器</span><span class="sxs-lookup"><span data-stu-id="49de5-102">Part 3: Creating an Admin Controller</span></span>

<span data-ttu-id="49de5-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="49de5-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="49de5-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="49de5-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="49de5-105">添加管理控制器</span><span class="sxs-lookup"><span data-stu-id="49de5-105">Add an Admin Controller</span></span>

<span data-ttu-id="49de5-106">在本部分中，我们将添加一个 Web API 控制器，该控制器支持对产品的 CRUD （创建、读取、更新和删除）操作。</span><span class="sxs-lookup"><span data-stu-id="49de5-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="49de5-107">控制器将使用实体框架与数据库层进行通信。</span><span class="sxs-lookup"><span data-stu-id="49de5-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="49de5-108">只有管理员才能使用该控制器。</span><span class="sxs-lookup"><span data-stu-id="49de5-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="49de5-109">客户将通过另一控制器访问产品。</span><span class="sxs-lookup"><span data-stu-id="49de5-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="49de5-110">在解决方案资源管理器中，右键单击 "控制器" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="49de5-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="49de5-111">依次选择 "**添加**" 和 "**控制器**"。</span><span class="sxs-lookup"><span data-stu-id="49de5-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="49de5-112">在 "**添加控制器**" 对话框中，将控制器命名为 `AdminController`。</span><span class="sxs-lookup"><span data-stu-id="49de5-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="49de5-113">在 "**模板**" 下，选择 "使用实体框架&quot;&quot;API 控制器，其中包含读/写操作。</span><span class="sxs-lookup"><span data-stu-id="49de5-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="49de5-114">在 "**模型类**" 下，选择 "Product （ProductStore）"。</span><span class="sxs-lookup"><span data-stu-id="49de5-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="49de5-115">在 "**数据上下文**" 下，选择 "&lt;新建数据上下文&gt;"。</span><span class="sxs-lookup"><span data-stu-id="49de5-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="49de5-116">如果 "**模型类**" 下拉端未显示任何模型类，请确保已编译该项目。</span><span class="sxs-lookup"><span data-stu-id="49de5-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="49de5-117">实体框架使用反射，因此它需要已编译的程序集。</span><span class="sxs-lookup"><span data-stu-id="49de5-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>

<span data-ttu-id="49de5-118">选择 "&lt;新的数据上下文&gt;" 将打开 "**新建数据上下文**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="49de5-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="49de5-119">将数据上下文命名为 `ProductStore.Models.OrdersContext`。</span><span class="sxs-lookup"><span data-stu-id="49de5-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="49de5-120">单击 **"确定"** 以关闭 "**新建数据上下文**" 对话框。</span><span class="sxs-lookup"><span data-stu-id="49de5-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="49de5-121">在 "**添加控制器**" 对话框中，单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="49de5-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="49de5-122">下面是已添加到项目的内容：</span><span class="sxs-lookup"><span data-stu-id="49de5-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="49de5-123">从**DbContext**派生的名为 `OrdersContext` 的类。</span><span class="sxs-lookup"><span data-stu-id="49de5-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="49de5-124">此类提供 POCO 模型和数据库之间的粘附。</span><span class="sxs-lookup"><span data-stu-id="49de5-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="49de5-125">名为 `AdminController`的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="49de5-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="49de5-126">此控制器支持对 `Product` 实例的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="49de5-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="49de5-127">它使用 `OrdersContext` 类与实体框架通信。</span><span class="sxs-lookup"><span data-stu-id="49de5-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="49de5-128">Web.config 文件中的新数据库连接字符串。</span><span class="sxs-lookup"><span data-stu-id="49de5-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="49de5-129">打开 OrdersContext.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="49de5-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="49de5-130">请注意，构造函数指定了数据库连接字符串的名称。</span><span class="sxs-lookup"><span data-stu-id="49de5-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="49de5-131">此名称是指添加到 web.config 的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="49de5-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="49de5-132">向 `OrdersContext` 类添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="49de5-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="49de5-133">**DbSet**表示可查询的一组实体。</span><span class="sxs-lookup"><span data-stu-id="49de5-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="49de5-134">下面是 `OrdersContext` 类的完整列表：</span><span class="sxs-lookup"><span data-stu-id="49de5-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="49de5-135">`AdminController` 类定义了五种实现基本 CRUD 功能的方法。</span><span class="sxs-lookup"><span data-stu-id="49de5-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="49de5-136">每个方法都对应于客户端可以调用的 URI：</span><span class="sxs-lookup"><span data-stu-id="49de5-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="49de5-137">控制器方法</span><span class="sxs-lookup"><span data-stu-id="49de5-137">Controller Method</span></span> | <span data-ttu-id="49de5-138">说明</span><span class="sxs-lookup"><span data-stu-id="49de5-138">Description</span></span> | <span data-ttu-id="49de5-139">URI</span><span class="sxs-lookup"><span data-stu-id="49de5-139">URI</span></span> | <span data-ttu-id="49de5-140">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="49de5-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="49de5-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="49de5-141">GetProducts</span></span> | <span data-ttu-id="49de5-142">获取所有产品。</span><span class="sxs-lookup"><span data-stu-id="49de5-142">Gets all products.</span></span> | <span data-ttu-id="49de5-143">api/产品</span><span class="sxs-lookup"><span data-stu-id="49de5-143">api/products</span></span> | <span data-ttu-id="49de5-144">GET</span><span class="sxs-lookup"><span data-stu-id="49de5-144">GET</span></span> |
| <span data-ttu-id="49de5-145">GetProduct</span><span class="sxs-lookup"><span data-stu-id="49de5-145">GetProduct</span></span> | <span data-ttu-id="49de5-146">按 ID 查找产品。</span><span class="sxs-lookup"><span data-stu-id="49de5-146">Finds a product by ID.</span></span> | <span data-ttu-id="49de5-147">api/产品/*id*</span><span class="sxs-lookup"><span data-stu-id="49de5-147">api/products/*id*</span></span> | <span data-ttu-id="49de5-148">GET</span><span class="sxs-lookup"><span data-stu-id="49de5-148">GET</span></span> |
| <span data-ttu-id="49de5-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="49de5-149">PutProduct</span></span> | <span data-ttu-id="49de5-150">更新产品。</span><span class="sxs-lookup"><span data-stu-id="49de5-150">Updates a product.</span></span> | <span data-ttu-id="49de5-151">api/产品/*id*</span><span class="sxs-lookup"><span data-stu-id="49de5-151">api/products/*id*</span></span> | <span data-ttu-id="49de5-152">PUT</span><span class="sxs-lookup"><span data-stu-id="49de5-152">PUT</span></span> |
| <span data-ttu-id="49de5-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="49de5-153">PostProduct</span></span> | <span data-ttu-id="49de5-154">创建新产品。</span><span class="sxs-lookup"><span data-stu-id="49de5-154">Creates a new product.</span></span> | <span data-ttu-id="49de5-155">api/产品</span><span class="sxs-lookup"><span data-stu-id="49de5-155">api/products</span></span> | <span data-ttu-id="49de5-156">POST</span><span class="sxs-lookup"><span data-stu-id="49de5-156">POST</span></span> |
| <span data-ttu-id="49de5-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="49de5-157">DeleteProduct</span></span> | <span data-ttu-id="49de5-158">删除产品。</span><span class="sxs-lookup"><span data-stu-id="49de5-158">Deletes a product.</span></span> | <span data-ttu-id="49de5-159">api/产品/*id*</span><span class="sxs-lookup"><span data-stu-id="49de5-159">api/products/*id*</span></span> | <span data-ttu-id="49de5-160">DELETE</span><span class="sxs-lookup"><span data-stu-id="49de5-160">DELETE</span></span> |

<span data-ttu-id="49de5-161">每个方法都调用到 `OrdersContext` 来查询数据库。</span><span class="sxs-lookup"><span data-stu-id="49de5-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="49de5-162">修改集合（PUT、POST 和 DELETE）调用 `db.SaveChanges` 的方法将更改保存到数据库中。</span><span class="sxs-lookup"><span data-stu-id="49de5-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="49de5-163">控制器是根据每个 HTTP 请求创建的，然后被释放，因此，在方法返回之前需要保存更改。</span><span class="sxs-lookup"><span data-stu-id="49de5-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="49de5-164">添加数据库初始值设定项</span><span class="sxs-lookup"><span data-stu-id="49de5-164">Add a Database Initializer</span></span>

<span data-ttu-id="49de5-165">实体框架具有一项不错的功能，可让你在启动时填充数据库，并在模型发生更改时自动重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="49de5-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="49de5-166">此功能在开发期间很有用，因为您始终会有一些测试数据，即使您更改了模型也是如此。</span><span class="sxs-lookup"><span data-stu-id="49de5-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="49de5-167">在解决方案资源管理器中，右键单击 "模型" 文件夹，然后创建一个名为 "`OrdersContextInitializer`" 的新类。</span><span class="sxs-lookup"><span data-stu-id="49de5-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="49de5-168">粘贴以下实现：</span><span class="sxs-lookup"><span data-stu-id="49de5-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="49de5-169">通过从**DropCreateDatabaseIfModelChanges**类继承，我们会告诉实体框架在修改 model 类时删除数据库。</span><span class="sxs-lookup"><span data-stu-id="49de5-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="49de5-170">当实体框架创建（或重新创建）数据库时，它将调用**Seed**方法来填充表。</span><span class="sxs-lookup"><span data-stu-id="49de5-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="49de5-171">我们使用**Seed**方法添加一些示例产品和示例订单。</span><span class="sxs-lookup"><span data-stu-id="49de5-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="49de5-172">此功能非常适合测试，但请勿在生产中使用**DropCreateDatabaseIfModelChanges**类，因为如果有人更改了模型类，就会丢失数据。</span><span class="sxs-lookup"><span data-stu-id="49de5-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="49de5-173">接下来，打开 global.asax 并将以下代码添加到**应用程序\_Start**方法：</span><span class="sxs-lookup"><span data-stu-id="49de5-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="49de5-174">向控制器发送请求</span><span class="sxs-lookup"><span data-stu-id="49de5-174">Send a Request to the Controller</span></span>

<span data-ttu-id="49de5-175">此时，我们尚未编写任何客户端代码，但可以使用 web 浏览器或 HTTP 调试工具（如[Fiddler](http://www.fiddler2.com/fiddler2/)）来调用 web API。</span><span class="sxs-lookup"><span data-stu-id="49de5-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="49de5-176">在 Visual Studio 中，按 F5 开始调试。</span><span class="sxs-lookup"><span data-stu-id="49de5-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="49de5-177">Web 浏览器将打开以 `http://localhost:*portnum*/`，其中*portnum*是某个端口号。</span><span class="sxs-lookup"><span data-stu-id="49de5-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="49de5-178">向 "`http://localhost:*portnum*/api/admin`发送 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="49de5-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="49de5-179">第一次请求可能会很慢，因为实体框架需要创建并播种数据库。</span><span class="sxs-lookup"><span data-stu-id="49de5-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="49de5-180">响应应类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="49de5-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="49de5-181">[上一页](using-web-api-with-entity-framework-part-2.md)
> [下一页](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="49de5-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
