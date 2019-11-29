---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: 在 ASP.NET Web API 1-ASP.NET 4.x 中启用 CRUD 操作
author: MikeWasson
description: 本教程介绍如何使用 ASP.NET Web API for ASP.NET 4.x 支持 HTTP 服务中的 CRUD 操作。
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600335"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="5cb6b-103">在 ASP.NET Web API 1 中启用 CRUD 操作</span><span class="sxs-lookup"><span data-stu-id="5cb6b-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="5cb6b-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5cb6b-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="5cb6b-105">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="5cb6b-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="5cb6b-106">本教程演示如何使用 ASP.NET Web API for ASP.NET 4.x 支持 HTTP 服务中的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5cb6b-107">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="5cb6b-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5cb6b-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="5cb6b-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="5cb6b-109">Web API 1 （也适用于 Web API 2）</span><span class="sxs-lookup"><span data-stu-id="5cb6b-109">Web API 1 (also works with Web API 2)</span></span>

<span data-ttu-id="5cb6b-110">CRUD 代表 &quot;创建、读取、更新和删除，&quot; 这四个基本数据库操作。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="5cb6b-111">许多 HTTP 服务还通过 REST 或 REST 等 Api 对 CRUD 操作进行建模。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="5cb6b-112">在本教程中，你将构建一个非常简单的 web API 来管理产品列表。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="5cb6b-113">每个产品都将包含一个名称、价格和类别（如 &quot;玩具&quot; 或 &quot;硬件&quot;）和产品 ID。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="5cb6b-114">产品 API 将公开以下方法。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="5cb6b-115">操作</span><span class="sxs-lookup"><span data-stu-id="5cb6b-115">Action</span></span> | <span data-ttu-id="5cb6b-116">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="5cb6b-116">HTTP method</span></span> | <span data-ttu-id="5cb6b-117">相对 URI</span><span class="sxs-lookup"><span data-stu-id="5cb6b-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5cb6b-118">获取所有产品的列表</span><span class="sxs-lookup"><span data-stu-id="5cb6b-118">Get a list of all products</span></span> | <span data-ttu-id="5cb6b-119">GET</span><span class="sxs-lookup"><span data-stu-id="5cb6b-119">GET</span></span> | <span data-ttu-id="5cb6b-120">/api/products</span><span class="sxs-lookup"><span data-stu-id="5cb6b-120">/api/products</span></span> |
| <span data-ttu-id="5cb6b-121">按 ID 获取产品</span><span class="sxs-lookup"><span data-stu-id="5cb6b-121">Get a product by ID</span></span> | <span data-ttu-id="5cb6b-122">GET</span><span class="sxs-lookup"><span data-stu-id="5cb6b-122">GET</span></span> | <span data-ttu-id="5cb6b-123">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="5cb6b-123">/api/products/*id*</span></span> |
| <span data-ttu-id="5cb6b-124">按类别获取产品</span><span class="sxs-lookup"><span data-stu-id="5cb6b-124">Get a product by category</span></span> | <span data-ttu-id="5cb6b-125">GET</span><span class="sxs-lookup"><span data-stu-id="5cb6b-125">GET</span></span> | <span data-ttu-id="5cb6b-126">/api/products？ category =*类别*</span><span class="sxs-lookup"><span data-stu-id="5cb6b-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="5cb6b-127">创建新产品</span><span class="sxs-lookup"><span data-stu-id="5cb6b-127">Create a new product</span></span> | <span data-ttu-id="5cb6b-128">POST</span><span class="sxs-lookup"><span data-stu-id="5cb6b-128">POST</span></span> | <span data-ttu-id="5cb6b-129">/api/products</span><span class="sxs-lookup"><span data-stu-id="5cb6b-129">/api/products</span></span> |
| <span data-ttu-id="5cb6b-130">更新产品</span><span class="sxs-lookup"><span data-stu-id="5cb6b-130">Update a product</span></span> | <span data-ttu-id="5cb6b-131">PUT</span><span class="sxs-lookup"><span data-stu-id="5cb6b-131">PUT</span></span> | <span data-ttu-id="5cb6b-132">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="5cb6b-132">/api/products/*id*</span></span> |
| <span data-ttu-id="5cb6b-133">删除产品</span><span class="sxs-lookup"><span data-stu-id="5cb6b-133">Delete a product</span></span> | <span data-ttu-id="5cb6b-134">删除</span><span class="sxs-lookup"><span data-stu-id="5cb6b-134">DELETE</span></span> | <span data-ttu-id="5cb6b-135">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="5cb6b-135">/api/products/*id*</span></span> |

<span data-ttu-id="5cb6b-136">请注意，某些 Uri 包含 "路径" 中的产品 ID。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="5cb6b-137">例如，若要获取 ID 为28的产品，客户端将为 `http://hostname/api/products/28`发送 GET 请求。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="5cb6b-138">资源</span><span class="sxs-lookup"><span data-stu-id="5cb6b-138">Resources</span></span>

<span data-ttu-id="5cb6b-139">产品 API 定义两种资源类型的 Uri：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="5cb6b-140">资源</span><span class="sxs-lookup"><span data-stu-id="5cb6b-140">Resource</span></span> | <span data-ttu-id="5cb6b-141">URI</span><span class="sxs-lookup"><span data-stu-id="5cb6b-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="5cb6b-142">所有产品的列表。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-142">The list of all the products.</span></span> | <span data-ttu-id="5cb6b-143">/api/products</span><span class="sxs-lookup"><span data-stu-id="5cb6b-143">/api/products</span></span> |
| <span data-ttu-id="5cb6b-144">单个产品。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-144">An individual product.</span></span> | <span data-ttu-id="5cb6b-145">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="5cb6b-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="5cb6b-146">方法</span><span class="sxs-lookup"><span data-stu-id="5cb6b-146">Methods</span></span>

<span data-ttu-id="5cb6b-147">四个主要 HTTP 方法（GET、PUT、POST 和 DELETE）可以映射到 CRUD 操作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="5cb6b-148">GET 检索指定 URI 处的资源的表示形式。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="5cb6b-149">GET 应在服务器上没有副作用。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="5cb6b-150">PUT 在指定的 URI 上更新资源。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="5cb6b-151">如果服务器允许客户端指定新的 uri，则 PUT 还可用于在指定的 URI 处创建新的资源。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="5cb6b-152">对于本教程，API 不支持通过 PUT 进行创建。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="5cb6b-153">POST 会创建一个新的资源。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-153">POST creates a new resource.</span></span> <span data-ttu-id="5cb6b-154">服务器分配新对象的 URI，并在响应消息中返回此 URI。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="5cb6b-155">DELETE 删除指定 URI 处的资源。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="5cb6b-156">注意： PUT 方法将替换整个 product 实体。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="5cb6b-157">也就是说，客户端应发送已更新产品的完整表示形式。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="5cb6b-158">如果希望支持部分更新，则最好选择 PATCH 方法。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="5cb6b-159">本教程不实现修补程序。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="5cb6b-160">创建新的 Web API 项目</span><span class="sxs-lookup"><span data-stu-id="5cb6b-160">Create a New Web API Project</span></span>

<span data-ttu-id="5cb6b-161">首先运行 Visual Studio，然后从**起始**页中选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="5cb6b-162">或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="5cb6b-163">在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="5cb6b-164">在 **" C#视觉对象**" 下选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="5cb6b-165">在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="5cb6b-166">将项目命名为 &quot;ProductStore&quot; 并单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="5cb6b-167">在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Web API** "，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="5cb6b-168">添加模型</span><span class="sxs-lookup"><span data-stu-id="5cb6b-168">Adding a Model</span></span>

<span data-ttu-id="5cb6b-169">模型是表示应用程序中的数据的对象。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="5cb6b-170">在 ASP.NET Web API 中，可以使用强类型化的 CLR 对象作为模型，它们会自动序列化为客户端的 XML 或 JSON。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="5cb6b-171">对于 ProductStore API，我们的数据包含产品，因此，我们将创建一个名为 `Product`的新类。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="5cb6b-172">如果解决方案资源管理器尚不可见，请单击 "**查看**" 菜单，然后选择 "**解决方案资源管理器**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="5cb6b-173">在解决方案资源管理器中，右键单击 "**模型**" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="5cb6b-174">从上下文菜单中，选择 "**添加**"，然后选择 "**类**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="5cb6b-175">将类命名为 &quot;产品&quot;。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="5cb6b-176">将以下属性添加到 `Product` 类。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="5cb6b-177">添加存储库</span><span class="sxs-lookup"><span data-stu-id="5cb6b-177">Adding a Repository</span></span>

<span data-ttu-id="5cb6b-178">我们需要存储产品集合。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-178">We need to store a collection of products.</span></span> <span data-ttu-id="5cb6b-179">最好将集合与我们的服务实现分离。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="5cb6b-180">这样，我们就可以更改后备存储，而无需重写服务类。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="5cb6b-181">这种类型的设计称为*存储库*模式。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="5cb6b-182">首先定义存储库的泛型接口。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="5cb6b-183">在解决方案资源管理器中，右键单击 "**模型**" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="5cb6b-184">选择 "**添加**"，然后选择 "**新建项**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="5cb6b-185">在 "**模板**" 窗格中，选择 "**已安装模板**" 并展开C#节点。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="5cb6b-186">在C#下，选择 "**代码**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-186">Under C#, select **Code**.</span></span> <span data-ttu-id="5cb6b-187">在代码模板列表中，选择 "**接口**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="5cb6b-188">将接口命名 &quot;IProductRepository&quot;。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="5cb6b-189">添加以下实现：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="5cb6b-190">现在，将另一个类添加到名为 &quot;化 productrepository 的模型文件夹中。此类&quot; 将实现 `IProductRepository` 接口。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="5cb6b-191">添加以下实现：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="5cb6b-192">存储库将列表保存在本地内存中。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="5cb6b-193">这对于教程来说是可以的，但在实际的应用程序中，你应将数据存储在外部、数据库或云存储中。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="5cb6b-194">存储库模式使稍后可以更轻松地更改实现。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="5cb6b-195">添加 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="5cb6b-195">Adding a Web API Controller</span></span>

<span data-ttu-id="5cb6b-196">如果你使用了 ASP.NET MVC，则已熟悉控制器。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="5cb6b-197">在 ASP.NET Web API 中，*控制器*是处理来自客户端的 HTTP 请求的类。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="5cb6b-198">"新建项目" 向导在创建项目时为您创建了两个控制器。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="5cb6b-199">若要查看它们，请展开解决方案资源管理器中的 "控制器" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="5cb6b-200">HomeController 是传统的 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="5cb6b-201">它负责为网站提供 HTML 页面，而不是直接与 web API 相关。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="5cb6b-202">ValuesController 是 WebAPI 控制器的示例。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="5cb6b-203">在解决方案资源管理器中右键单击该文件，然后选择 "删除"，以删除 ValuesController **。**</span><span class="sxs-lookup"><span data-stu-id="5cb6b-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="5cb6b-204">现在，添加一个新的控制器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="5cb6b-205">在**解决方案资源管理器**中，右键单击 "控制器" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="5cb6b-206">选择 "**添加**"，然后选择 "**控制器**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="5cb6b-207">在 "**添加控制器**" 向导中，将控制器命名为 &quot;ProductsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="5cb6b-208">在 "**模板**" 下拉列表中，选择 "**空 API 控制器**"。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="5cb6b-209">然后单击 **“添加”** 。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="5cb6b-210">不需要将控制器放入名为控制器的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="5cb6b-211">文件夹名称不重要;它只是一种用于组织源文件的简便方法。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>

<span data-ttu-id="5cb6b-212">**添加控制器**向导将在 "控制器" 文件夹中创建一个名为 "ProductsController.cs" 的文件。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="5cb6b-213">如果此文件尚未打开，请双击该文件将其打开。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="5cb6b-214">添加以下**using**语句：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="5cb6b-215">添加用于保存**IProductRepository**实例的字段。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="5cb6b-216">在控制器中调用 `new ProductRepository()` 不是最佳设计，因为它将控制器与 `IProductRepository`的特定实现联系在一起。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="5cb6b-217">有关更好的方法，请参阅[使用 WEB API 依赖关系解析程序](../advanced/dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>

## <a name="getting-a-resource"></a><span data-ttu-id="5cb6b-218">获取资源</span><span class="sxs-lookup"><span data-stu-id="5cb6b-218">Getting a Resource</span></span>

<span data-ttu-id="5cb6b-219">ProductStore API 将公开几个 &quot;将&quot; 操作作为 HTTP GET 方法进行读取。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="5cb6b-220">每个操作都对应于 `ProductsController` 类中的一个方法。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="5cb6b-221">操作</span><span class="sxs-lookup"><span data-stu-id="5cb6b-221">Action</span></span> | <span data-ttu-id="5cb6b-222">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="5cb6b-222">HTTP method</span></span> | <span data-ttu-id="5cb6b-223">相对 URI</span><span class="sxs-lookup"><span data-stu-id="5cb6b-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5cb6b-224">获取所有产品的列表</span><span class="sxs-lookup"><span data-stu-id="5cb6b-224">Get a list of all products</span></span> | <span data-ttu-id="5cb6b-225">GET</span><span class="sxs-lookup"><span data-stu-id="5cb6b-225">GET</span></span> | <span data-ttu-id="5cb6b-226">/api/products</span><span class="sxs-lookup"><span data-stu-id="5cb6b-226">/api/products</span></span> |
| <span data-ttu-id="5cb6b-227">按 ID 获取产品</span><span class="sxs-lookup"><span data-stu-id="5cb6b-227">Get a product by ID</span></span> | <span data-ttu-id="5cb6b-228">GET</span><span class="sxs-lookup"><span data-stu-id="5cb6b-228">GET</span></span> | <span data-ttu-id="5cb6b-229">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="5cb6b-229">/api/products/*id*</span></span> |
| <span data-ttu-id="5cb6b-230">按类别获取产品</span><span class="sxs-lookup"><span data-stu-id="5cb6b-230">Get a product by category</span></span> | <span data-ttu-id="5cb6b-231">GET</span><span class="sxs-lookup"><span data-stu-id="5cb6b-231">GET</span></span> | <span data-ttu-id="5cb6b-232">/api/products？ category =*类别*</span><span class="sxs-lookup"><span data-stu-id="5cb6b-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="5cb6b-233">若要获取所有产品的列表，请将以下方法添加到 `ProductsController` 类：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="5cb6b-234">方法名称以 &quot;Get&quot;开始，因此按约定映射到获取请求。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="5cb6b-235">此外，因为该方法没有参数，它将映射到路径中不包含 *&quot;id&quot;* 段的 URI。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="5cb6b-236">若要按 ID 获取产品，请将以下方法添加到 `ProductsController` 类：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="5cb6b-237">此方法名称还从 &quot;Get&quot;开始，但该方法具有一个名为*id*的参数。此参数映射到 URI 路径 &quot;id&quot; 段。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="5cb6b-238">ASP.NET Web API 框架自动将该 ID 转换为参数的正确数据类型（**int**）。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="5cb6b-239">如果*id*无效，GetProduct 方法将引发**带有 httpresponseexception**类型的异常。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="5cb6b-240">此异常将由框架转换为404（未找到）错误。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="5cb6b-241">最后，添加一个方法，按类别查找产品：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="5cb6b-242">如果请求 URI 具有查询字符串，则 Web API 会尝试将查询参数与控制器方法的参数匹配。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="5cb6b-243">因此，"api/products？ category =*category*" 形式的 URI 将映射到此方法。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="5cb6b-244">创建资源</span><span class="sxs-lookup"><span data-stu-id="5cb6b-244">Creating a Resource</span></span>

<span data-ttu-id="5cb6b-245">接下来，我们将向 `ProductsController` 类添加一个方法来创建新产品。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="5cb6b-246">下面是方法的简单实现：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="5cb6b-247">请注意有关此方法的两个事项：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-247">Note two things about this method:</span></span>

- <span data-ttu-id="5cb6b-248">方法名称以 &quot;Post ...&quot;开头。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="5cb6b-249">若要创建新产品，客户端将发送 HTTP POST 请求。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="5cb6b-250">方法采用 Product 类型的参数。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="5cb6b-251">在 Web API 中，具有复杂类型的参数将从请求正文反序列化。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="5cb6b-252">因此，我们希望客户端以 XML 或 JSON 格式发送 product 对象的序列化表示形式。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="5cb6b-253">此实现将起作用，但并不完整。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="5cb6b-254">理想情况下，我们希望 HTTP 响应包括以下内容：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="5cb6b-255">**响应代码：** 默认情况下，Web API 框架将响应状态代码设置为200（OK）。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="5cb6b-256">但根据 HTTP/1.1 协议，当 POST 请求导致资源创建时，服务器应使用状态201（已创建）进行回复。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="5cb6b-257">**位置：** 当服务器创建资源时，它应在响应的 Location 标头中包含新资源的 URI。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="5cb6b-258">ASP.NET Web API 可以轻松地操作 HTTP 响应消息。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="5cb6b-259">下面是改进的实现：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="5cb6b-260">请注意，方法返回类型现在为**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="5cb6b-261">通过返回**HttpResponseMessage**而不是产品，我们可以控制 HTTP 响应消息的详细信息，包括状态代码和位置标头。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="5cb6b-262">**CreateResponse**方法创建**HttpResponseMessage** ，并将产品对象的序列化表示形式自动写入响应消息的正文中。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="5cb6b-263">此示例不验证 `Product`。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="5cb6b-264">有关模型验证的信息，请参阅[中的模型验证 ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

## <a name="updating-a-resource"></a><span data-ttu-id="5cb6b-265">更新资源</span><span class="sxs-lookup"><span data-stu-id="5cb6b-265">Updating a Resource</span></span>

<span data-ttu-id="5cb6b-266">使用 PUT 更新产品非常简单：</span><span class="sxs-lookup"><span data-stu-id="5cb6b-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="5cb6b-267">方法名称以 &quot;Put ...&quot;开头，因此 Web API 会将其与 PUT 请求相匹配。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="5cb6b-268">方法采用两个参数：产品 ID 和更新的产品。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="5cb6b-269">*Id*参数是从 URI 路径获取的， *product*参数是从请求正文反序列化的。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="5cb6b-270">默认情况下，ASP.NET Web API 框架从路由使用简单的参数类型，并从请求正文获取复杂类型。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="5cb6b-271">删除资源</span><span class="sxs-lookup"><span data-stu-id="5cb6b-271">Deleting a Resource</span></span>

<span data-ttu-id="5cb6b-272">若要删除资源，请定义 "Delete ..."付款方式.</span><span class="sxs-lookup"><span data-stu-id="5cb6b-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="5cb6b-273">如果 DELETE 请求成功，则它可以返回状态200（OK），其中包含描述状态的实体正文;如果删除仍处于挂起状态，则为状态202（已接受）;或状态204（无内容），无实体正文。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="5cb6b-274">在这种情况下，`DeleteProduct` 方法具有 `void` 返回类型，因此 ASP.NET Web API 会自动将其转换为状态代码204（无内容）。</span><span class="sxs-lookup"><span data-stu-id="5cb6b-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
