---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: 使用 ASP.NET Web API 2.2 创建 OData v4 终结点 |Microsoft Docs
author: MikeWasson
description: Open Data Protocol （OData）是 web 的数据访问协议。 OData 通过 CRUD 操作提供一种统一的方法来查询和操作数据集 。
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484496"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a><span data-ttu-id="e638c-104">使用 ASP.NET Web API 创建 OData v4 终结点</span><span class="sxs-lookup"><span data-stu-id="e638c-104">Create an OData v4 Endpoint Using ASP.NET Web API</span></span> 

> <span data-ttu-id="e638c-105">Open Data Protocol （OData）是 web 的数据访问协议。</span><span class="sxs-lookup"><span data-stu-id="e638c-105">The Open Data Protocol (OData) is a data access protocol for the web.</span></span> <span data-ttu-id="e638c-106">OData 通过 CRUD 操作（创建、读取、更新和删除）提供了一种统一的方法来查询和操作数据集。</span><span class="sxs-lookup"><span data-stu-id="e638c-106">OData provides a uniform way to query and manipulate data sets through CRUD operations (create, read, update, and delete).</span></span>
>
> <span data-ttu-id="e638c-107">ASP.NET Web API 支持协议的 v3 和 v4。</span><span class="sxs-lookup"><span data-stu-id="e638c-107">ASP.NET Web API supports both v3 and v4 of the protocol.</span></span> <span data-ttu-id="e638c-108">甚至可以使用与 v3 终结点并行运行的 v4 终结点。</span><span class="sxs-lookup"><span data-stu-id="e638c-108">You can even have a v4 endpoint that runs side-by-side with a v3 endpoint.</span></span>
>
> <span data-ttu-id="e638c-109">本教程演示如何创建支持 CRUD 操作的 OData v4 终结点。</span><span class="sxs-lookup"><span data-stu-id="e638c-109">This tutorial shows how to create an OData v4 endpoint that supports CRUD operations.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e638c-110">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="e638c-110">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="e638c-111">Web API 5。2</span><span class="sxs-lookup"><span data-stu-id="e638c-111">Web API 5.2</span></span>
> - <span data-ttu-id="e638c-112">OData v4</span><span class="sxs-lookup"><span data-stu-id="e638c-112">OData v4</span></span>
> - <span data-ttu-id="e638c-113">Visual Studio 2017 （下载 Visual Studio 2017[此处](https://visualstudio.microsoft.com/downloads/)）</span><span class="sxs-lookup"><span data-stu-id="e638c-113">Visual Studio 2017 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/))</span></span>
> - <span data-ttu-id="e638c-114">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="e638c-114">Entity Framework 6</span></span>
> - <span data-ttu-id="e638c-115">.NET 4.7.2</span><span class="sxs-lookup"><span data-stu-id="e638c-115">.NET 4.7.2</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="e638c-116">教程版本</span><span class="sxs-lookup"><span data-stu-id="e638c-116">Tutorial versions</span></span>
>
> <span data-ttu-id="e638c-117">对于 OData 版本3，请参阅[创建 odata V3 终结点](../odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="e638c-117">For the OData Version 3, see [Creating an OData v3 Endpoint](../odata-v3/creating-an-odata-endpoint.md).</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="e638c-118">创建 Visual Studio 项目</span><span class="sxs-lookup"><span data-stu-id="e638c-118">Create the Visual Studio Project</span></span>

<span data-ttu-id="e638c-119">在 Visual Studio 的 "**文件**" 菜单中，选择 "**新建**" &gt;**项目**"。</span><span class="sxs-lookup"><span data-stu-id="e638c-119">In Visual Studio, from the **File** menu, select **New** &gt; **Project**.</span></span>

<span data-ttu-id="e638c-120">展开 "**已安装**&gt; **Visual C#**  &gt; **web**"，然后选择 " **ASP.NET Web 应用程序（.NET Framework）** " 模板。</span><span class="sxs-lookup"><span data-stu-id="e638c-120">Expand **Installed** &gt; **Visual C#** &gt; **Web**, and select the **ASP.NET Web Application (.NET Framework)** template.</span></span> <span data-ttu-id="e638c-121">将项目命名为 &quot;ProductService&quot;。</span><span class="sxs-lookup"><span data-stu-id="e638c-121">Name the project &quot;ProductService&quot;.</span></span>

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

<span data-ttu-id="e638c-122">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="e638c-122">Select **OK**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

<span data-ttu-id="e638c-123">选择“空”模板。</span><span class="sxs-lookup"><span data-stu-id="e638c-123">Select the **Empty** template.</span></span> <span data-ttu-id="e638c-124">在 "**添加文件夹和核心引用：** " 下，选择 " **Web API**"。</span><span class="sxs-lookup"><span data-stu-id="e638c-124">Under **Add folders and core references for:**, select **Web API**.</span></span> <span data-ttu-id="e638c-125">选择“确定”。</span><span class="sxs-lookup"><span data-stu-id="e638c-125">Select **OK**.</span></span>

## <a name="install-the-odata-packages"></a><span data-ttu-id="e638c-126">安装 OData 包</span><span class="sxs-lookup"><span data-stu-id="e638c-126">Install the OData packages</span></span>

<span data-ttu-id="e638c-127">从“工具”菜单中，选择“NuGet 包管理器” **“包管理器控制台”** &gt;。</span><span class="sxs-lookup"><span data-stu-id="e638c-127">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="e638c-128">在 "程序包管理器控制台" 窗口中，键入：</span><span class="sxs-lookup"><span data-stu-id="e638c-128">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

<span data-ttu-id="e638c-129">此命令安装最新的 OData NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e638c-129">This command installs the latest OData NuGet packages.</span></span>

## <a name="add-a-model-class"></a><span data-ttu-id="e638c-130">添加模型类</span><span class="sxs-lookup"><span data-stu-id="e638c-130">Add a model class</span></span>

<span data-ttu-id="e638c-131">*模型*是表示应用程序中的数据实体的对象。</span><span class="sxs-lookup"><span data-stu-id="e638c-131">A *model* is an object that represents a data entity in your application.</span></span>

<span data-ttu-id="e638c-132">在解决方案资源管理器中，右键单击“模型”文件夹。</span><span class="sxs-lookup"><span data-stu-id="e638c-132">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="e638c-133">从上下文菜单中，选择 "**添加**&gt;**类**"。</span><span class="sxs-lookup"><span data-stu-id="e638c-133">From the context menu, select **Add** &gt; **Class**.</span></span>

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> <span data-ttu-id="e638c-134">按照约定，模型类放置在 "模型" 文件夹中，但你无需在自己的项目中遵循此约定。</span><span class="sxs-lookup"><span data-stu-id="e638c-134">By convention, model classes are placed in the Models folder, but you don't have to follow this convention in your own projects.</span></span>

<span data-ttu-id="e638c-135">将此类命名为 `Product`。</span><span class="sxs-lookup"><span data-stu-id="e638c-135">Name the class `Product`.</span></span> <span data-ttu-id="e638c-136">在 Product.cs 文件中，将样板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="e638c-136">In the Product.cs file, replace the boilerplate code with the following:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

<span data-ttu-id="e638c-137">`Id` 属性是实体键。</span><span class="sxs-lookup"><span data-stu-id="e638c-137">The `Id` property is the entity key.</span></span> <span data-ttu-id="e638c-138">客户端可以按键查询实体。</span><span class="sxs-lookup"><span data-stu-id="e638c-138">Clients can query entities by key.</span></span> <span data-ttu-id="e638c-139">例如，若要获取 ID 为5的产品，请 `/Products(5)`URI。</span><span class="sxs-lookup"><span data-stu-id="e638c-139">For example, to get the product with ID of 5, the URI is `/Products(5)`.</span></span> <span data-ttu-id="e638c-140">`Id` 属性还将是后端数据库中的主键。</span><span class="sxs-lookup"><span data-stu-id="e638c-140">The `Id` property will also be the primary key in the back-end database.</span></span>

## <a name="enable-entity-framework"></a><span data-ttu-id="e638c-141">启用实体框架</span><span class="sxs-lookup"><span data-stu-id="e638c-141">Enable Entity Framework</span></span>

<span data-ttu-id="e638c-142">对于本教程，我们将使用实体框架（EF） Code First 创建后端数据库。</span><span class="sxs-lookup"><span data-stu-id="e638c-142">For this tutorial, we'll use Entity Framework (EF) Code First to create the back-end database.</span></span>

> [!NOTE]
> <span data-ttu-id="e638c-143">Web API OData 不需要 EF。</span><span class="sxs-lookup"><span data-stu-id="e638c-143">Web API OData does not require EF.</span></span> <span data-ttu-id="e638c-144">使用任何可以将数据库实体转换为模型的数据访问层。</span><span class="sxs-lookup"><span data-stu-id="e638c-144">Use any data-access layer that can translate database entities into models.</span></span>

<span data-ttu-id="e638c-145">首先，安装适用于 EF 的 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="e638c-145">First, install the NuGet package for EF.</span></span> <span data-ttu-id="e638c-146">从“工具”菜单中，选择“NuGet 包管理器” **“包管理器控制台”** &gt;。</span><span class="sxs-lookup"><span data-stu-id="e638c-146">From the **Tools** menu, select **NuGet Package Manager** &gt; **Package Manager Console**.</span></span> <span data-ttu-id="e638c-147">在 "程序包管理器控制台" 窗口中，键入：</span><span class="sxs-lookup"><span data-stu-id="e638c-147">In the Package Manager Console window, type:</span></span>

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

<span data-ttu-id="e638c-148">打开 web.config 文件，并将以下部分添加到**configuration**元素中的**configSections**元素之后。</span><span class="sxs-lookup"><span data-stu-id="e638c-148">Open the Web.config file, and add the following section inside the **configuration** element, after the **configSections** element.</span></span>

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

<span data-ttu-id="e638c-149">此设置将添加 LocalDB 数据库的连接字符串。</span><span class="sxs-lookup"><span data-stu-id="e638c-149">This setting adds a connection string for a LocalDB database.</span></span> <span data-ttu-id="e638c-150">在本地运行应用程序时，将使用此数据库。</span><span class="sxs-lookup"><span data-stu-id="e638c-150">This database will be used when you run the app locally.</span></span>

<span data-ttu-id="e638c-151">接下来，将名为 `ProductsContext` 的类添加到模型文件夹中：</span><span class="sxs-lookup"><span data-stu-id="e638c-151">Next, add a class named `ProductsContext` to the Models folder:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

<span data-ttu-id="e638c-152">在构造函数中，`"name=ProductsContext"` 提供连接字符串的名称。</span><span class="sxs-lookup"><span data-stu-id="e638c-152">In the constructor, `"name=ProductsContext"` gives the name of the connection string.</span></span>

## <a name="configure-the-odata-endpoint"></a><span data-ttu-id="e638c-153">配置 OData 终结点</span><span class="sxs-lookup"><span data-stu-id="e638c-153">Configure the OData endpoint</span></span>

<span data-ttu-id="e638c-154">打开文件应用\_Start/Webapiconfig.cs。</span><span class="sxs-lookup"><span data-stu-id="e638c-154">Open the file App\_Start/WebApiConfig.cs.</span></span> <span data-ttu-id="e638c-155">添加以下**using**语句：</span><span class="sxs-lookup"><span data-stu-id="e638c-155">Add the following **using** statements:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

<span data-ttu-id="e638c-156">然后，将以下代码添加到**Register**方法：</span><span class="sxs-lookup"><span data-stu-id="e638c-156">Then add the following code to the **Register** method:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

<span data-ttu-id="e638c-157">此代码执行两项操作：</span><span class="sxs-lookup"><span data-stu-id="e638c-157">This code does two things:</span></span>

- <span data-ttu-id="e638c-158">创建实体数据模型（EDM）。</span><span class="sxs-lookup"><span data-stu-id="e638c-158">Creates an Entity Data Model (EDM).</span></span>
- <span data-ttu-id="e638c-159">添加路由。</span><span class="sxs-lookup"><span data-stu-id="e638c-159">Adds a route.</span></span>

<span data-ttu-id="e638c-160">EDM 是数据的抽象模型。</span><span class="sxs-lookup"><span data-stu-id="e638c-160">An EDM is an abstract model of the data.</span></span> <span data-ttu-id="e638c-161">EDM 用于创建服务元数据文档。</span><span class="sxs-lookup"><span data-stu-id="e638c-161">The EDM is used to create the service metadata document.</span></span> <span data-ttu-id="e638c-162">**ODataConventionModelBuilder**类使用默认命名约定创建 EDM。</span><span class="sxs-lookup"><span data-stu-id="e638c-162">The **ODataConventionModelBuilder** class creates an EDM by using default naming conventions.</span></span> <span data-ttu-id="e638c-163">此方法需要最少的代码。</span><span class="sxs-lookup"><span data-stu-id="e638c-163">This approach requires the least code.</span></span> <span data-ttu-id="e638c-164">如果要对 EDM 进行更多的控制，可以使用**ODataModelBuilder**类来创建 edm，方法是显式添加属性、键和导航属性。</span><span class="sxs-lookup"><span data-stu-id="e638c-164">If you want more control over the EDM, you can use the **ODataModelBuilder** class to create the EDM by adding properties, keys, and navigation properties explicitly.</span></span>

<span data-ttu-id="e638c-165">*路由*通知 Web API 如何将 HTTP 请求路由到终结点。</span><span class="sxs-lookup"><span data-stu-id="e638c-165">A *route* tells Web API how to route HTTP requests to the endpoint.</span></span> <span data-ttu-id="e638c-166">若要创建 OData v4 路由，请调用**MapODataServiceRoute**扩展方法。</span><span class="sxs-lookup"><span data-stu-id="e638c-166">To create an OData v4 route, call the **MapODataServiceRoute** extension method.</span></span>

<span data-ttu-id="e638c-167">如果应用程序有多个 OData 终结点，请为每个终结点创建一个单独的路由。</span><span class="sxs-lookup"><span data-stu-id="e638c-167">If your application has multiple OData endpoints, create a separate route for each.</span></span> <span data-ttu-id="e638c-168">为每个路由指定唯一的路由名称和前缀。</span><span class="sxs-lookup"><span data-stu-id="e638c-168">Give each route a unique route name and prefix.</span></span>

## <a name="add-the-odata-controller"></a><span data-ttu-id="e638c-169">添加 OData 控制器</span><span class="sxs-lookup"><span data-stu-id="e638c-169">Add the OData controller</span></span>

<span data-ttu-id="e638c-170">*控制器*是处理 HTTP 请求的类。</span><span class="sxs-lookup"><span data-stu-id="e638c-170">A *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="e638c-171">为 OData 服务中的每个实体集创建一个单独的控制器。</span><span class="sxs-lookup"><span data-stu-id="e638c-171">You create a separate controller for each entity set in your OData service.</span></span> <span data-ttu-id="e638c-172">在本教程中，你将为 `Product` 实体创建一个控制器。</span><span class="sxs-lookup"><span data-stu-id="e638c-172">In this tutorial, you will create one controller, for the `Product` entity.</span></span>

<span data-ttu-id="e638c-173">在解决方案资源管理器中，右键单击 "控制器" 文件夹，然后选择 "**添加**&gt;**类**"。</span><span class="sxs-lookup"><span data-stu-id="e638c-173">In Solution Explorer, right-click the Controllers folder and select **Add** &gt; **Class**.</span></span> <span data-ttu-id="e638c-174">将此类命名为 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="e638c-174">Name the class `ProductsController`.</span></span>

> [!NOTE]
> <span data-ttu-id="e638c-175">此适用于 OData v3 的版本使用**添加控制器**基架。</span><span class="sxs-lookup"><span data-stu-id="e638c-175">The version of this tutorial for OData v3 uses the **Add Controller** scaffolding.</span></span> <span data-ttu-id="e638c-176">当前没有适用于 OData v4 的基架。</span><span class="sxs-lookup"><span data-stu-id="e638c-176">Currently, there is no scaffolding for OData v4.</span></span>

<span data-ttu-id="e638c-177">将 ProductsController.cs 中的样板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="e638c-177">Replace the boilerplate code in ProductsController.cs with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

<span data-ttu-id="e638c-178">控制器使用 `ProductsContext` 类通过 EF 访问数据库。</span><span class="sxs-lookup"><span data-stu-id="e638c-178">The controller uses the `ProductsContext` class to access the database using EF.</span></span> <span data-ttu-id="e638c-179">请注意，控制器会重写**dispose**方法以释放**ProductsContext**。</span><span class="sxs-lookup"><span data-stu-id="e638c-179">Notice that the controller overrides the **Dispose** method to dispose of the **ProductsContext**.</span></span>

<span data-ttu-id="e638c-180">这是控制器的起点。</span><span class="sxs-lookup"><span data-stu-id="e638c-180">This is the starting point for the controller.</span></span> <span data-ttu-id="e638c-181">接下来，我们将添加所有 CRUD 操作的方法。</span><span class="sxs-lookup"><span data-stu-id="e638c-181">Next, we'll add methods for all of the CRUD operations.</span></span>

## <a name="query-the-entity-set"></a><span data-ttu-id="e638c-182">查询实体集</span><span class="sxs-lookup"><span data-stu-id="e638c-182">Query the entity set</span></span>

<span data-ttu-id="e638c-183">将以下方法添加到 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="e638c-183">Add the following methods to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

<span data-ttu-id="e638c-184">`Get` 方法的无参数版本将返回整个产品集合。</span><span class="sxs-lookup"><span data-stu-id="e638c-184">The parameterless version of the `Get` method returns the entire Products collection.</span></span> <span data-ttu-id="e638c-185">带有*键*参数的 `Get` 方法按其键（在本例中为 `Id` 属性）查找产品。</span><span class="sxs-lookup"><span data-stu-id="e638c-185">The `Get` method with a *key* parameter looks up a product by its key (in this case, the `Id` property).</span></span>

<span data-ttu-id="e638c-186">**[EnableQuery]** 属性允许客户端使用查询选项（如 $filter、$sort 和 $page）来修改查询。</span><span class="sxs-lookup"><span data-stu-id="e638c-186">The **[EnableQuery]** attribute enables clients to modify the query, by using query options such as $filter, $sort, and $page.</span></span> <span data-ttu-id="e638c-187">有关详细信息，请参阅[支持 OData 查询选项](../supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="e638c-187">For more information, see [Supporting OData Query Options](../supporting-odata-query-options.md).</span></span>

## <a name="add-an-entity-to-the-entity-set"></a><span data-ttu-id="e638c-188">将实体添加到实体集</span><span class="sxs-lookup"><span data-stu-id="e638c-188">Add an entity to the entity set</span></span>

<span data-ttu-id="e638c-189">若要使客户端能够将新产品添加到数据库，请将以下方法添加到 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="e638c-189">To enable clients to add a new product to the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a><span data-ttu-id="e638c-190">更新实体</span><span class="sxs-lookup"><span data-stu-id="e638c-190">Update an entity</span></span>

<span data-ttu-id="e638c-191">OData 支持使用两种不同的语义来更新实体、修补和 PUT。</span><span class="sxs-lookup"><span data-stu-id="e638c-191">OData supports two different semantics for updating an entity, PATCH and PUT.</span></span>

- <span data-ttu-id="e638c-192">修补程序执行部分更新。</span><span class="sxs-lookup"><span data-stu-id="e638c-192">PATCH performs a partial update.</span></span> <span data-ttu-id="e638c-193">客户端仅指定要更新的属性。</span><span class="sxs-lookup"><span data-stu-id="e638c-193">The client specifies just the properties to update.</span></span>
- <span data-ttu-id="e638c-194">PUT 替换整个实体。</span><span class="sxs-lookup"><span data-stu-id="e638c-194">PUT replaces the entire entity.</span></span>

<span data-ttu-id="e638c-195">PUT 的缺点在于，客户端必须为实体中的所有属性发送值，包括未更改的值。</span><span class="sxs-lookup"><span data-stu-id="e638c-195">The disadvantage of PUT is that the client must send values for all of the properties in the entity, including values that are not changing.</span></span> <span data-ttu-id="e638c-196">[OData 规范](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719)指出此修补程序是首选的。</span><span class="sxs-lookup"><span data-stu-id="e638c-196">The [OData spec](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) states that PATCH is preferred.</span></span>

<span data-ttu-id="e638c-197">在任何情况下，以下是修补和 PUT 方法的代码：</span><span class="sxs-lookup"><span data-stu-id="e638c-197">In any case, here is the code for both PATCH and PUT methods:</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

<span data-ttu-id="e638c-198">对于修补程序，控制器使用**增量&lt;t&gt;** 类型跟踪所做的更改。</span><span class="sxs-lookup"><span data-stu-id="e638c-198">In the case of PATCH, the controller uses the **Delta&lt;T&gt;** type to track the changes.</span></span>

## <a name="delete-an-entity"></a><span data-ttu-id="e638c-199">删除实体</span><span class="sxs-lookup"><span data-stu-id="e638c-199">Delete an entity</span></span>

<span data-ttu-id="e638c-200">若要使客户端能够从数据库中删除产品，请将以下方法添加到 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="e638c-200">To enable clients to delete a product from the database, add the following method to `ProductsController`.</span></span>

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
