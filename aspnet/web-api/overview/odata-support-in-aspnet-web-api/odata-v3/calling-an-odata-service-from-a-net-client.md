---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: 从 .NET 客户端调用 OData 服务（C#） |Microsoft Docs
author: MikeWasson
description: 本教程演示如何从C#客户端应用程序调用 OData 服务。 本教程中使用的软件版本 Visual Studio 2013 （使用视觉对象 。
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498164"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a><span data-ttu-id="2ed91-104">从 .NET 客户端调用 OData 服务 (C#)</span><span class="sxs-lookup"><span data-stu-id="2ed91-104">Calling an OData Service From a .NET Client (C#)</span></span>

<span data-ttu-id="2ed91-105">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2ed91-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="2ed91-106">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="2ed91-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="2ed91-107">本教程演示如何从C#客户端应用程序调用 OData 服务。</span><span class="sxs-lookup"><span data-stu-id="2ed91-107">This tutorial shows how to call an OData service from a C# client application.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="2ed91-108">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="2ed91-108">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="2ed91-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) （适用于 Visual Studio 2012）</span><span class="sxs-lookup"><span data-stu-id="2ed91-109">[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (works with Visual Studio 2012)</span></span>
> - [<span data-ttu-id="2ed91-110">WCF Data Services 客户端库</span><span class="sxs-lookup"><span data-stu-id="2ed91-110">WCF Data Services Client Library</span></span>](https://msdn.microsoft.com/library/cc668772.aspx)
> - <span data-ttu-id="2ed91-111">Web API 2。</span><span class="sxs-lookup"><span data-stu-id="2ed91-111">Web API 2.</span></span> <span data-ttu-id="2ed91-112">（示例 OData 服务是使用 Web API 2 生成的，但是客户端应用程序不依赖于 Web API。）</span><span class="sxs-lookup"><span data-stu-id="2ed91-112">(The example OData service is built using Web API 2, but the client application does not depend on Web API.)</span></span>

<span data-ttu-id="2ed91-113">在本教程中，我将逐步介绍如何创建一个调用 OData 服务的客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="2ed91-113">In this tutorial, I'll walk through creating a client application that calls an OData service.</span></span> <span data-ttu-id="2ed91-114">OData 服务公开以下实体：</span><span class="sxs-lookup"><span data-stu-id="2ed91-114">The OData service exposes the following entities:</span></span>

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

<span data-ttu-id="2ed91-115">以下文章介绍如何在 Web API 中实现 OData 服务。</span><span class="sxs-lookup"><span data-stu-id="2ed91-115">The following articles describe how to implement the OData service in Web API.</span></span> <span data-ttu-id="2ed91-116">（但是，您不需要阅读它们来了解本教程。）</span><span class="sxs-lookup"><span data-stu-id="2ed91-116">(You don't need to read them to understand this tutorial, however.)</span></span>

- [<span data-ttu-id="2ed91-117">在 Web API 2 中创建 OData 终结点</span><span class="sxs-lookup"><span data-stu-id="2ed91-117">Creating an OData Endpoint in Web API 2</span></span>](creating-an-odata-endpoint.md)
- [<span data-ttu-id="2ed91-118">Web API 2 中的 OData 实体关系</span><span class="sxs-lookup"><span data-stu-id="2ed91-118">OData Entity Relations in Web API 2</span></span>](working-with-entity-relations.md)
- [<span data-ttu-id="2ed91-119">Web API 2 中的 OData 操作</span><span class="sxs-lookup"><span data-stu-id="2ed91-119">OData Actions in Web API 2</span></span>](odata-actions.md)

## <a name="generate-the-service-proxy"></a><span data-ttu-id="2ed91-120">生成服务代理</span><span class="sxs-lookup"><span data-stu-id="2ed91-120">Generate the Service Proxy</span></span>

<span data-ttu-id="2ed91-121">第一步是生成服务代理。</span><span class="sxs-lookup"><span data-stu-id="2ed91-121">The first step is to generate a service proxy.</span></span> <span data-ttu-id="2ed91-122">服务代理是一个 .NET 类，用于定义用于访问 OData 服务的方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-122">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="2ed91-123">代理会将方法调用转换为 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="2ed91-123">The proxy translates method calls into HTTP requests.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

<span data-ttu-id="2ed91-124">首先，在 Visual Studio 中打开 "OData 服务" 项目。</span><span class="sxs-lookup"><span data-stu-id="2ed91-124">Start by opening the OData service project in Visual Studio.</span></span> <span data-ttu-id="2ed91-125">在 IIS Express 中按 CTRL + F5 以本地方式运行该服务。</span><span class="sxs-lookup"><span data-stu-id="2ed91-125">Press CTRL+F5 to run the service locally in IIS Express.</span></span> <span data-ttu-id="2ed91-126">记下本地地址，包括 Visual Studio 分配的端口号。</span><span class="sxs-lookup"><span data-stu-id="2ed91-126">Note the local address, including the port number that Visual Studio assigns.</span></span> <span data-ttu-id="2ed91-127">创建代理时，将需要此地址。</span><span class="sxs-lookup"><span data-stu-id="2ed91-127">You will need this address when you create the proxy.</span></span>

<span data-ttu-id="2ed91-128">接下来，打开 Visual Studio 的另一个实例，并创建一个控制台应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="2ed91-128">Next, open another instance of Visual Studio and create a console application project.</span></span> <span data-ttu-id="2ed91-129">控制台应用程序将是我们的 OData 客户端应用程序。</span><span class="sxs-lookup"><span data-stu-id="2ed91-129">The console application will be our OData client application.</span></span> <span data-ttu-id="2ed91-130">（您也可以将该项目添加到与该服务相同的解决方案中。）</span><span class="sxs-lookup"><span data-stu-id="2ed91-130">(You can also add the project to the same solution as the service.)</span></span>

> [!NOTE]
> <span data-ttu-id="2ed91-131">其余步骤引用控制台项目。</span><span class="sxs-lookup"><span data-stu-id="2ed91-131">The remaining steps refer the console project.</span></span>

<span data-ttu-id="2ed91-132">在解决方案资源管理器中，右键单击 "**引用**"，然后选择 "**添加服务引用**"。</span><span class="sxs-lookup"><span data-stu-id="2ed91-132">In Solution Explorer, right-click **References** and select **Add Service Reference**.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

<span data-ttu-id="2ed91-133">在 "**添加服务引用**" 对话框中，键入 OData 服务的地址：</span><span class="sxs-lookup"><span data-stu-id="2ed91-133">In the **Add Service Reference** dialog, type the address of the OData service:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

<span data-ttu-id="2ed91-134">其中*port*是端口号。</span><span class="sxs-lookup"><span data-stu-id="2ed91-134">where *port* is the port number.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

<span data-ttu-id="2ed91-135">对于 "**命名空间**"，键入 "ProductService"。</span><span class="sxs-lookup"><span data-stu-id="2ed91-135">For **Namespace**, type "ProductService".</span></span> <span data-ttu-id="2ed91-136">此选项定义代理类的命名空间。</span><span class="sxs-lookup"><span data-stu-id="2ed91-136">This option defines the namespace of the proxy class.</span></span>

<span data-ttu-id="2ed91-137">单击 **“转到”** 。</span><span class="sxs-lookup"><span data-stu-id="2ed91-137">Click **Go**.</span></span> <span data-ttu-id="2ed91-138">Visual Studio 将读取 OData 元数据文档，以发现服务中的实体。</span><span class="sxs-lookup"><span data-stu-id="2ed91-138">Visual Studio reads the OData metadata document to discover the entities in the service.</span></span>

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

<span data-ttu-id="2ed91-139">单击 **"确定"** 将代理类添加到项目。</span><span class="sxs-lookup"><span data-stu-id="2ed91-139">Click **OK** to add the proxy class to your project.</span></span>

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a><span data-ttu-id="2ed91-140">创建服务代理类的实例</span><span class="sxs-lookup"><span data-stu-id="2ed91-140">Create an Instance of the Service Proxy Class</span></span>

<span data-ttu-id="2ed91-141">在 `Main` 方法中，创建代理类的新实例，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ed91-141">Inside your `Main` method, create a new instance of the proxy class, as follows:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

<span data-ttu-id="2ed91-142">同样，使用服务运行时使用的实际端口号。</span><span class="sxs-lookup"><span data-stu-id="2ed91-142">Again, use the actual port number where your service is running.</span></span> <span data-ttu-id="2ed91-143">部署服务时，将使用实时服务的 URI。</span><span class="sxs-lookup"><span data-stu-id="2ed91-143">When you deploy your service, you will use the URI of the live service.</span></span> <span data-ttu-id="2ed91-144">不需要更新代理。</span><span class="sxs-lookup"><span data-stu-id="2ed91-144">You don't need to update the proxy.</span></span>

<span data-ttu-id="2ed91-145">下面的代码将添加一个事件处理程序，用于将请求 Uri 打印到控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="2ed91-145">The following code adds an event handler that prints the request URIs to the console window.</span></span> <span data-ttu-id="2ed91-146">此步骤不是必需的，但请务必查看每个查询的 Uri。</span><span class="sxs-lookup"><span data-stu-id="2ed91-146">This step isn't required, but it's interesting to see the URIs for each query.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a><span data-ttu-id="2ed91-147">查询服务</span><span class="sxs-lookup"><span data-stu-id="2ed91-147">Query the Service</span></span>

<span data-ttu-id="2ed91-148">下面的代码从 OData 服务获取产品列表。</span><span class="sxs-lookup"><span data-stu-id="2ed91-148">The following code gets the list of products from the OData service.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

<span data-ttu-id="2ed91-149">请注意，不需要编写任何代码来发送 HTTP 请求或分析响应。</span><span class="sxs-lookup"><span data-stu-id="2ed91-149">Notice that you don't need to write any code to send the HTTP request or parse the response.</span></span> <span data-ttu-id="2ed91-150">在**foreach**循环中枚举 `Container.Products` 集合时，代理类会自动执行此类。</span><span class="sxs-lookup"><span data-stu-id="2ed91-150">The proxy class does this automatically when you enumerate the `Container.Products` collection in the **foreach** loop.</span></span>

<span data-ttu-id="2ed91-151">运行应用程序时，输出应如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ed91-151">When you run the application, the output should look like the following:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

<span data-ttu-id="2ed91-152">若要按 ID 获取实体，请使用 `where` 子句。</span><span class="sxs-lookup"><span data-stu-id="2ed91-152">To get an entity by ID, use a `where` clause.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

<span data-ttu-id="2ed91-153">本主题的其余部分不会显示整个 `Main` 函数，只是调用服务所需的代码。</span><span class="sxs-lookup"><span data-stu-id="2ed91-153">For the rest of this topic, I won't show the entire `Main` function, just the code needed to call the service.</span></span>

## <a name="apply-query-options"></a><span data-ttu-id="2ed91-154">应用查询选项</span><span class="sxs-lookup"><span data-stu-id="2ed91-154">Apply Query Options</span></span>

<span data-ttu-id="2ed91-155">OData 定义可用于对数据进行筛选、排序、分页等的[查询选项](../supporting-odata-query-options.md)。</span><span class="sxs-lookup"><span data-stu-id="2ed91-155">OData defines [query options](../supporting-odata-query-options.md) that can be used to filter, sort, page data, and so forth.</span></span> <span data-ttu-id="2ed91-156">在服务代理中，可以通过使用各种 LINQ 表达式来应用这些选项。</span><span class="sxs-lookup"><span data-stu-id="2ed91-156">In the service proxy, you can apply these options by using various LINQ expressions.</span></span>

<span data-ttu-id="2ed91-157">在本部分中，我将演示一些简单的示例。</span><span class="sxs-lookup"><span data-stu-id="2ed91-157">In this section, I'll show brief examples.</span></span> <span data-ttu-id="2ed91-158">有关更多详细信息，请参阅 MSDN 上的主题[LINQ 注意事项（WCF 数据服务）](https://msdn.microsoft.com/library/ee622463.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="2ed91-158">For more details, see the topic [LINQ Considerations (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) on MSDN.</span></span>

### <a name="filtering-filter"></a><span data-ttu-id="2ed91-159">筛选（$filter）</span><span class="sxs-lookup"><span data-stu-id="2ed91-159">Filtering ($filter)</span></span>

<span data-ttu-id="2ed91-160">若要进行筛选，请使用 `where` 子句。</span><span class="sxs-lookup"><span data-stu-id="2ed91-160">To filter, use a `where` clause.</span></span> <span data-ttu-id="2ed91-161">下面的示例按产品类别进行筛选。</span><span class="sxs-lookup"><span data-stu-id="2ed91-161">The following example filters by product category.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

<span data-ttu-id="2ed91-162">此代码对应于以下 OData 查询。</span><span class="sxs-lookup"><span data-stu-id="2ed91-162">This code corresponds to the following OData query.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

<span data-ttu-id="2ed91-163">请注意，代理将 `where` 子句转换为 OData `$filter` 表达式。</span><span class="sxs-lookup"><span data-stu-id="2ed91-163">Notice that the proxy converts the `where` clause into an OData `$filter` expression.</span></span>

### <a name="sorting-orderby"></a><span data-ttu-id="2ed91-164">排序（$orderby）</span><span class="sxs-lookup"><span data-stu-id="2ed91-164">Sorting ($orderby)</span></span>

<span data-ttu-id="2ed91-165">若要进行排序，请使用 `orderby` 子句。</span><span class="sxs-lookup"><span data-stu-id="2ed91-165">To sort, use an `orderby` clause.</span></span> <span data-ttu-id="2ed91-166">下面的示例按价格从高到低的顺序进行排序。</span><span class="sxs-lookup"><span data-stu-id="2ed91-166">The following example sorts by price, from highest to lowest.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

<span data-ttu-id="2ed91-167">下面是相应的 OData 请求。</span><span class="sxs-lookup"><span data-stu-id="2ed91-167">Here is the corresponding OData request.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a><span data-ttu-id="2ed91-168">客户端分页（$skip 和 $top）</span><span class="sxs-lookup"><span data-stu-id="2ed91-168">Client-Side Paging ($skip and $top)</span></span>

<span data-ttu-id="2ed91-169">对于大型实体集，客户端可能需要限制结果的数目。</span><span class="sxs-lookup"><span data-stu-id="2ed91-169">For large entity sets, the client might want to limit the number of results.</span></span> <span data-ttu-id="2ed91-170">例如，客户端一次可能会显示10个条目。</span><span class="sxs-lookup"><span data-stu-id="2ed91-170">For example, a client might show 10 entries at a time.</span></span> <span data-ttu-id="2ed91-171">这称为*客户端分页*。</span><span class="sxs-lookup"><span data-stu-id="2ed91-171">This is called *client-side paging*.</span></span> <span data-ttu-id="2ed91-172">（还有[服务器端分页](../supporting-odata-query-options.md#server-paging)，服务器将限制结果数。）若要执行客户端分页，请使用 LINQ **Skip**和**Take**方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-172">(There is also [server-side paging](../supporting-odata-query-options.md#server-paging), where the server limits the number of results.) To perform client-side paging, use the LINQ **Skip** and **Take** methods.</span></span> <span data-ttu-id="2ed91-173">下面的示例跳过前40个结果，并取下10。</span><span class="sxs-lookup"><span data-stu-id="2ed91-173">The following example skips the first 40 results and takes the next 10.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

<span data-ttu-id="2ed91-174">下面是相应的 OData 请求：</span><span class="sxs-lookup"><span data-stu-id="2ed91-174">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a><span data-ttu-id="2ed91-175">选择（$select）并展开（$expand）</span><span class="sxs-lookup"><span data-stu-id="2ed91-175">Select ($select) and Expand ($expand)</span></span>

<span data-ttu-id="2ed91-176">若要包括相关实体，请使用 `DataServiceQuery<t>.Expand` 方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-176">To include related entities, use the `DataServiceQuery<t>.Expand` method.</span></span> <span data-ttu-id="2ed91-177">例如，若要包括每个 `Product`的 `Supplier`：</span><span class="sxs-lookup"><span data-stu-id="2ed91-177">For example, to include the `Supplier` for each `Product`:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

<span data-ttu-id="2ed91-178">下面是相应的 OData 请求：</span><span class="sxs-lookup"><span data-stu-id="2ed91-178">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

<span data-ttu-id="2ed91-179">若要更改响应的形状，请使用 LINQ **select**子句。</span><span class="sxs-lookup"><span data-stu-id="2ed91-179">To change the shape of the response, use the LINQ **select** clause.</span></span> <span data-ttu-id="2ed91-180">下面的示例只获取每个产品的名称，不包含其他属性。</span><span class="sxs-lookup"><span data-stu-id="2ed91-180">The following example gets just the name of each product, with no other properties.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

<span data-ttu-id="2ed91-181">下面是相应的 OData 请求：</span><span class="sxs-lookup"><span data-stu-id="2ed91-181">Here is the corresponding OData request:</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

<span data-ttu-id="2ed91-182">Select 子句可以包括相关实体。</span><span class="sxs-lookup"><span data-stu-id="2ed91-182">A select clause can include related entities.</span></span> <span data-ttu-id="2ed91-183">在这种情况下，请不要调用**Expand**;在这种情况下，代理将自动包括扩展。</span><span class="sxs-lookup"><span data-stu-id="2ed91-183">In that case, do not call **Expand**; the proxy automatically includes the expansion in this case.</span></span> <span data-ttu-id="2ed91-184">下面的示例获取了每个产品的名称和供应商。</span><span class="sxs-lookup"><span data-stu-id="2ed91-184">The following example gets the name and supplier of each product.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

<span data-ttu-id="2ed91-185">下面是相应的 OData 请求。</span><span class="sxs-lookup"><span data-stu-id="2ed91-185">Here is the corresponding OData request.</span></span> <span data-ttu-id="2ed91-186">请注意，它包含 **$expand**选项。</span><span class="sxs-lookup"><span data-stu-id="2ed91-186">Notice that it includes the **$expand** option.</span></span>

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

<span data-ttu-id="2ed91-187">有关 $select 和 $expand 的详细信息，请参阅[在 WEB API 2 中使用 $select、$expand 和 $value](../using-select-expand-and-value.md)。</span><span class="sxs-lookup"><span data-stu-id="2ed91-187">For more information about $select and $expand, see [Using $select, $expand, and $value in Web API 2](../using-select-expand-and-value.md).</span></span>

## <a name="add-a-new-entity"></a><span data-ttu-id="2ed91-188">添加新实体</span><span class="sxs-lookup"><span data-stu-id="2ed91-188">Add a New Entity</span></span>

<span data-ttu-id="2ed91-189">若要将新实体添加到实体集，请调用 `AddToEntitySet`，其中*EntitySet*是实体集的名称。</span><span class="sxs-lookup"><span data-stu-id="2ed91-189">To add a new entity to an entity set, call `AddToEntitySet`, where *EntitySet* is the name of the entity set.</span></span> <span data-ttu-id="2ed91-190">例如，`AddToProducts` 向 `Products` 实体集添加新 `Product`。</span><span class="sxs-lookup"><span data-stu-id="2ed91-190">For example, `AddToProducts` adds a new `Product` to the `Products` entity set.</span></span> <span data-ttu-id="2ed91-191">生成代理时，WCF 数据服务会自动创建这些强类型的**AddTo**方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-191">When you generate the proxy, WCF Data Services automatically creates these strongly-typed **AddTo** methods.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

<span data-ttu-id="2ed91-192">若要在两个实体之间添加链接，请使用**AddLink**和**SetLink**方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-192">To add a link between two entities, use the **AddLink** and **SetLink** methods.</span></span> <span data-ttu-id="2ed91-193">以下代码将添加新的供应商和新产品，然后在它们之间创建链接。</span><span class="sxs-lookup"><span data-stu-id="2ed91-193">The following code adds a new supplier and a new product, and then creates links between them.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

<span data-ttu-id="2ed91-194">当导航属性是集合时，请使用**AddLink** 。</span><span class="sxs-lookup"><span data-stu-id="2ed91-194">Use **AddLink** when the navigation property is a collection.</span></span> <span data-ttu-id="2ed91-195">在此示例中，我们要将产品添加到供应商的 `Products` 集合。</span><span class="sxs-lookup"><span data-stu-id="2ed91-195">In this example, we are adding a product to the `Products` collection on the supplier.</span></span>

<span data-ttu-id="2ed91-196">当导航属性为单个实体时，请使用**SetLink** 。</span><span class="sxs-lookup"><span data-stu-id="2ed91-196">Use **SetLink** when the navigation property is a single entity.</span></span> <span data-ttu-id="2ed91-197">在此示例中，我们将设置产品的 `Supplier` 属性。</span><span class="sxs-lookup"><span data-stu-id="2ed91-197">In this example, we are setting the `Supplier` property on the product.</span></span>

## <a name="update--patch"></a><span data-ttu-id="2ed91-198">更新/修补</span><span class="sxs-lookup"><span data-stu-id="2ed91-198">Update / Patch</span></span>

<span data-ttu-id="2ed91-199">若要更新实体，请调用**UpdateObject**方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-199">To update an entity, call the **UpdateObject** method.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

<span data-ttu-id="2ed91-200">在调用**SaveChanges**时执行更新。</span><span class="sxs-lookup"><span data-stu-id="2ed91-200">The update is performed when you call **SaveChanges**.</span></span> <span data-ttu-id="2ed91-201">默认情况下，WCF 发送 HTTP 合并请求。</span><span class="sxs-lookup"><span data-stu-id="2ed91-201">By default, WCF sends an HTTP MERGE request.</span></span> <span data-ttu-id="2ed91-202">**PatchOnUpdate**选项告知 WCF 改为发送 HTTP 修补程序。</span><span class="sxs-lookup"><span data-stu-id="2ed91-202">The **PatchOnUpdate** option tells WCF to send an HTTP PATCH instead.</span></span>

> [!NOTE]
> <span data-ttu-id="2ed91-203">为什么要修补与合并？</span><span class="sxs-lookup"><span data-stu-id="2ed91-203">Why PATCH versus MERGE?</span></span> <span data-ttu-id="2ed91-204">原始 HTTP 1.1 规范（[RCF 2616](http://tools.ietf.org/html/rfc2616)）未定义具有 "部分更新" 语义的任何 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-204">The original HTTP 1.1 specification ([RCF 2616](http://tools.ietf.org/html/rfc2616)) did not define any HTTP method with "partial update" semantics.</span></span> <span data-ttu-id="2ed91-205">为了支持部分更新，OData 规范定义了 MERGE 方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-205">To support partial updates, the OData specification defined the MERGE method.</span></span> <span data-ttu-id="2ed91-206">在2010中， [RFC 5789](http://tools.ietf.org/html/rfc5789)为部分更新定义了修补程序方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-206">In 2010, [RFC 5789](http://tools.ietf.org/html/rfc5789) defined the PATCH method for partial updates.</span></span> <span data-ttu-id="2ed91-207">你可以在 WCF 数据服务博客上阅读此[博客文章](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx)中的部分历史记录。</span><span class="sxs-lookup"><span data-stu-id="2ed91-207">You can read some of the history in this [blog post](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) on the WCF Data Services Blog.</span></span> <span data-ttu-id="2ed91-208">目前，修补程序优先于 MERGE。</span><span class="sxs-lookup"><span data-stu-id="2ed91-208">Today, PATCH is preferred over MERGE.</span></span> <span data-ttu-id="2ed91-209">Web API 基架创建的 OData 控制器支持这两种方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-209">The OData controller created by the Web API scaffolding supports both methods.</span></span>

<span data-ttu-id="2ed91-210">如果要替换整个实体（PUT 语义），请指定**带 savechangesoptions.replaceonupdate**选项。</span><span class="sxs-lookup"><span data-stu-id="2ed91-210">If you want to replace the entire entity (PUT semantics), specify the **ReplaceOnUpdate** option.</span></span> <span data-ttu-id="2ed91-211">这将导致 WCF 发送 HTTP PUT 请求。</span><span class="sxs-lookup"><span data-stu-id="2ed91-211">This causes WCF to send an HTTP PUT request.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a><span data-ttu-id="2ed91-212">删除实体</span><span class="sxs-lookup"><span data-stu-id="2ed91-212">Delete an Entity</span></span>

<span data-ttu-id="2ed91-213">若要删除实体，请调用**DeleteObject**。</span><span class="sxs-lookup"><span data-stu-id="2ed91-213">To delete an entity, call **DeleteObject**.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a><span data-ttu-id="2ed91-214">调用 OData 操作</span><span class="sxs-lookup"><span data-stu-id="2ed91-214">Invoke an OData Action</span></span>

<span data-ttu-id="2ed91-215">在 OData 中，[操作](odata-actions.md)是一种添加服务器端行为的方法，这些行为不容易定义为对实体的 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="2ed91-215">In OData, [actions](odata-actions.md) are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span>

<span data-ttu-id="2ed91-216">尽管 OData 元数据文档描述了这些操作，但 proxy 类不会为它们创建任何强类型化方法。</span><span class="sxs-lookup"><span data-stu-id="2ed91-216">Although the OData metadata document describes the actions, the proxy class does not create any strongly-typed methods for them.</span></span> <span data-ttu-id="2ed91-217">你仍可以使用泛型**Execute**方法调用 OData 操作。</span><span class="sxs-lookup"><span data-stu-id="2ed91-217">You can still invoke an OData action by using the generic **Execute** method.</span></span> <span data-ttu-id="2ed91-218">但是，您需要了解参数的数据类型和返回值。</span><span class="sxs-lookup"><span data-stu-id="2ed91-218">However, you will need to know the data types of the parameters and the return value.</span></span>

<span data-ttu-id="2ed91-219">例如，`RateProduct` 操作使用 `Int32` 类型的名为 "分级" 的参数，并返回 `double`。</span><span class="sxs-lookup"><span data-stu-id="2ed91-219">For example, the `RateProduct` action takes parameter named "Rating" of type `Int32` and returns a `double`.</span></span> <span data-ttu-id="2ed91-220">下面的代码演示如何调用此操作。</span><span class="sxs-lookup"><span data-stu-id="2ed91-220">The following code shows how to invoke this action.</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

<span data-ttu-id="2ed91-221">有关详细信息，请参阅[调用服务操作和操作](https://msdn.microsoft.com/library/hh230677.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2ed91-221">For more information, see[Calling Service Operations and Actions](https://msdn.microsoft.com/library/hh230677.aspx).</span></span>

<span data-ttu-id="2ed91-222">一种选择是扩展**容器类**，以提供调用该操作的强类型方法：</span><span class="sxs-lookup"><span data-stu-id="2ed91-222">One option is to extend the **Container** class to provide a strongly typed method that invokes the action:</span></span>

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
