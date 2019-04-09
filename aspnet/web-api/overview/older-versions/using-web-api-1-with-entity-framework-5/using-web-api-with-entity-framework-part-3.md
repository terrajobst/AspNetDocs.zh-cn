---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 第 3 部分：创建管理员控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: de4bb063d2a6c1bdb4aeffdadb161ef19efd2b78
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59390943"
---
# <a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="c018c-102">第 3 部分：创建管理员控制器</span><span class="sxs-lookup"><span data-stu-id="c018c-102">Part 3: Creating an Admin Controller</span></span>

<span data-ttu-id="c018c-103">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c018c-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="c018c-104">下载已完成的项目</span><span class="sxs-lookup"><span data-stu-id="c018c-104">Download Completed Project</span></span>](http://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="c018c-105">添加管理员控制器</span><span class="sxs-lookup"><span data-stu-id="c018c-105">Add an Admin Controller</span></span>

<span data-ttu-id="c018c-106">在本部分中，我们将添加一个 Web API 控制器支持 CRUD （创建、 读取、 更新和删除） 对产品的操作。</span><span class="sxs-lookup"><span data-stu-id="c018c-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="c018c-107">控制器将使用 Entity Framework 与数据库层进行通信。</span><span class="sxs-lookup"><span data-stu-id="c018c-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="c018c-108">只有管理员将能够使用此控制器。</span><span class="sxs-lookup"><span data-stu-id="c018c-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="c018c-109">客户将通过另一个控制器访问产品。</span><span class="sxs-lookup"><span data-stu-id="c018c-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="c018c-110">在解决方案资源管理器，右键单击 Controllers 文件夹。</span><span class="sxs-lookup"><span data-stu-id="c018c-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="c018c-111">选择**添加**，然后**控制器**。</span><span class="sxs-lookup"><span data-stu-id="c018c-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="c018c-112">在中**添加控制器**对话框中，将控制器命名`AdminController`。</span><span class="sxs-lookup"><span data-stu-id="c018c-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="c018c-113">下**模板**，选择&quot;包含读/写操作，使用实体框架 API 控制器&quot;。</span><span class="sxs-lookup"><span data-stu-id="c018c-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="c018c-114">下**模型类**，选择"Product (ProductStore.Models)"。</span><span class="sxs-lookup"><span data-stu-id="c018c-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="c018c-115">下**数据上下文**，选择"&lt;新建数据上下文&gt;"。</span><span class="sxs-lookup"><span data-stu-id="c018c-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="c018c-116">如果**模型类**下拉列表不显示任何模型的类，请确保编译项目。</span><span class="sxs-lookup"><span data-stu-id="c018c-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="c018c-117">实体框架使用反射，因此它需要编译的程序集。</span><span class="sxs-lookup"><span data-stu-id="c018c-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>


<span data-ttu-id="c018c-118">选择"&lt;新建数据上下文&gt;"将打开**新建数据上下文**对话框。</span><span class="sxs-lookup"><span data-stu-id="c018c-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="c018c-119">命名的数据上下文`ProductStore.Models.OrdersContext`。</span><span class="sxs-lookup"><span data-stu-id="c018c-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="c018c-120">单击**确定**以关闭**新建数据上下文**对话框。</span><span class="sxs-lookup"><span data-stu-id="c018c-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="c018c-121">在中**添加控制器**对话框中，单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="c018c-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="c018c-122">下面是什么已添加到项目：</span><span class="sxs-lookup"><span data-stu-id="c018c-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="c018c-123">名为的类`OrdersContext`派生**DbContext**。</span><span class="sxs-lookup"><span data-stu-id="c018c-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="c018c-124">此类提供了 POCO 模型和数据库之间关联。</span><span class="sxs-lookup"><span data-stu-id="c018c-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="c018c-125">名为的 Web API 控制器`AdminController`。</span><span class="sxs-lookup"><span data-stu-id="c018c-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="c018c-126">此控制器上支持的 CRUD 操作`Product`实例。</span><span class="sxs-lookup"><span data-stu-id="c018c-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="c018c-127">它使用`OrdersContext`类与实体框架进行通信。</span><span class="sxs-lookup"><span data-stu-id="c018c-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="c018c-128">新数据库的连接字符串的 Web.config 文件中。</span><span class="sxs-lookup"><span data-stu-id="c018c-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="c018c-129">打开 OrdersContext.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="c018c-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="c018c-130">请注意，构造函数指定的数据库连接字符串名称。</span><span class="sxs-lookup"><span data-stu-id="c018c-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="c018c-131">此名称是指已添加到 Web.config 的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="c018c-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="c018c-132">向 `OrdersContext` 类添加以下属性：</span><span class="sxs-lookup"><span data-stu-id="c018c-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="c018c-133">一个**DbSet**表示一组可查询的实体。</span><span class="sxs-lookup"><span data-stu-id="c018c-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="c018c-134">下面是完整列表以供`OrdersContext`类：</span><span class="sxs-lookup"><span data-stu-id="c018c-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="c018c-135">`AdminController`类定义了五种实现基本的 CRUD 功能的方法。</span><span class="sxs-lookup"><span data-stu-id="c018c-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="c018c-136">每个方法对应于客户端可以调用的 URI:</span><span class="sxs-lookup"><span data-stu-id="c018c-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="c018c-137">控制器方法</span><span class="sxs-lookup"><span data-stu-id="c018c-137">Controller Method</span></span> | <span data-ttu-id="c018c-138">描述</span><span class="sxs-lookup"><span data-stu-id="c018c-138">Description</span></span> | <span data-ttu-id="c018c-139">URI</span><span class="sxs-lookup"><span data-stu-id="c018c-139">URI</span></span> | <span data-ttu-id="c018c-140">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="c018c-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c018c-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="c018c-141">GetProducts</span></span> | <span data-ttu-id="c018c-142">获取所有产品。</span><span class="sxs-lookup"><span data-stu-id="c018c-142">Gets all products.</span></span> | <span data-ttu-id="c018c-143">api/products</span><span class="sxs-lookup"><span data-stu-id="c018c-143">api/products</span></span> | <span data-ttu-id="c018c-144">GET</span><span class="sxs-lookup"><span data-stu-id="c018c-144">GET</span></span> |
| <span data-ttu-id="c018c-145">GetProduct</span><span class="sxs-lookup"><span data-stu-id="c018c-145">GetProduct</span></span> | <span data-ttu-id="c018c-146">查找产品的 id。</span><span class="sxs-lookup"><span data-stu-id="c018c-146">Finds a product by ID.</span></span> | <span data-ttu-id="c018c-147">api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="c018c-147">api/products/*id*</span></span> | <span data-ttu-id="c018c-148">GET</span><span class="sxs-lookup"><span data-stu-id="c018c-148">GET</span></span> |
| <span data-ttu-id="c018c-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="c018c-149">PutProduct</span></span> | <span data-ttu-id="c018c-150">更新产品。</span><span class="sxs-lookup"><span data-stu-id="c018c-150">Updates a product.</span></span> | <span data-ttu-id="c018c-151">api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="c018c-151">api/products/*id*</span></span> | <span data-ttu-id="c018c-152">PUT</span><span class="sxs-lookup"><span data-stu-id="c018c-152">PUT</span></span> |
| <span data-ttu-id="c018c-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="c018c-153">PostProduct</span></span> | <span data-ttu-id="c018c-154">创建一个新的产品。</span><span class="sxs-lookup"><span data-stu-id="c018c-154">Creates a new product.</span></span> | <span data-ttu-id="c018c-155">api/products</span><span class="sxs-lookup"><span data-stu-id="c018c-155">api/products</span></span> | <span data-ttu-id="c018c-156">发布</span><span class="sxs-lookup"><span data-stu-id="c018c-156">POST</span></span> |
| <span data-ttu-id="c018c-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="c018c-157">DeleteProduct</span></span> | <span data-ttu-id="c018c-158">删除产品。</span><span class="sxs-lookup"><span data-stu-id="c018c-158">Deletes a product.</span></span> | <span data-ttu-id="c018c-159">api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="c018c-159">api/products/*id*</span></span> | <span data-ttu-id="c018c-160">DELETE</span><span class="sxs-lookup"><span data-stu-id="c018c-160">DELETE</span></span> |

<span data-ttu-id="c018c-161">每个方法调入`OrdersContext`查询数据库。</span><span class="sxs-lookup"><span data-stu-id="c018c-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="c018c-162">修改集合 （PUT、 POST 和 DELETE） 的方法调用`db.SaveChanges`可保存到数据库更改。</span><span class="sxs-lookup"><span data-stu-id="c018c-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="c018c-163">控制器中创建每个 HTTP 请求，然后释放，因此需要以一种方法返回之前保存的更改。</span><span class="sxs-lookup"><span data-stu-id="c018c-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="c018c-164">添加数据库初始值设定项</span><span class="sxs-lookup"><span data-stu-id="c018c-164">Add a Database Initializer</span></span>

<span data-ttu-id="c018c-165">Entity Framework 有一个不错的功能，你可以在启动时，在数据库中填充和每当模型发生更改时自动重新创建数据库。</span><span class="sxs-lookup"><span data-stu-id="c018c-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="c018c-166">此功能可在开发期间，因为始终具有一些测试数据，即使更改了模型。</span><span class="sxs-lookup"><span data-stu-id="c018c-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="c018c-167">在解决方案资源管理器，右键单击模型文件夹并创建一个名为的新类`OrdersContextInitializer`。</span><span class="sxs-lookup"><span data-stu-id="c018c-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="c018c-168">粘贴以下实现：</span><span class="sxs-lookup"><span data-stu-id="c018c-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="c018c-169">通过继承自**DropCreateDatabaseIfModelChanges**类中，我们在告诉实体框架，以删除数据库，只要我们修改模型类。</span><span class="sxs-lookup"><span data-stu-id="c018c-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="c018c-170">当实体框架创建 （或重新创建） 数据库时，它将调用**种子**方法以填充表。</span><span class="sxs-lookup"><span data-stu-id="c018c-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="c018c-171">我们使用**种子**方法将添加一些示例产品以及示例订单。</span><span class="sxs-lookup"><span data-stu-id="c018c-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="c018c-172">此功能非常适用于测试，但不使用**DropCreateDatabaseIfModelChanges**类在生产环境、 中，因为如果有人更改 model 类，则可能会丢失数据。</span><span class="sxs-lookup"><span data-stu-id="c018c-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="c018c-173">接下来，打开 Global.asax，然后将以下代码添加到**应用程序\_启动**方法：</span><span class="sxs-lookup"><span data-stu-id="c018c-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="c018c-174">将请求发送到控制器</span><span class="sxs-lookup"><span data-stu-id="c018c-174">Send a Request to the Controller</span></span>

<span data-ttu-id="c018c-175">此时，我们还没有编写任何客户端代码，但你可以调用的 web API 使用 web 浏览器或 HTTP 调试工具如[Fiddler](http://www.fiddler2.com/fiddler2/)。</span><span class="sxs-lookup"><span data-stu-id="c018c-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="c018c-176">在 Visual Studio 中，按 F5 启动调试。</span><span class="sxs-lookup"><span data-stu-id="c018c-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="c018c-177">在 web 浏览器将打开到`http://localhost:*portnum*/`，其中*portnum*是某些端口号。</span><span class="sxs-lookup"><span data-stu-id="c018c-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="c018c-178">发送到 HTTP 请求"`http://localhost:*portnum*/api/admin`。</span><span class="sxs-lookup"><span data-stu-id="c018c-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="c018c-179">因为实体框架需要创建和设置数据库的种子速度可能较慢，若要完成，第一个请求。</span><span class="sxs-lookup"><span data-stu-id="c018c-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="c018c-180">响应应类似于下面：</span><span class="sxs-lookup"><span data-stu-id="c018c-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="c018c-181">[上一页](using-web-api-with-entity-framework-part-2.md)
> [下一页](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="c018c-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
