---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: 结合使用 Web API 和 ASP.NET Web Forms-ASP.NET 4。x
author: MikeWasson
description: 有关将 Web API 添加到 ASP.NET 4.x 的 ASP.NET Forms 应用程序的分步指南
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448532"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="37b10-103">向 ASP.NET Web 窗体使用 Web API</span><span class="sxs-lookup"><span data-stu-id="37b10-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="37b10-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="37b10-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="37b10-105">本教程将指导你完成将 Web API 添加到 ASP.NET 4.x 中的传统 ASP.NET Web 窗体应用程序的步骤。</span><span class="sxs-lookup"><span data-stu-id="37b10-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="37b10-106">概述</span><span class="sxs-lookup"><span data-stu-id="37b10-106">Overview</span></span>

<span data-ttu-id="37b10-107">尽管 ASP.NET Web API 与 ASP.NET MVC 一起打包，但可以轻松地将 Web API 添加到传统的 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="37b10-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="37b10-108">若要在 Web 窗体应用程序中使用 Web API，需要执行两个主要步骤：</span><span class="sxs-lookup"><span data-stu-id="37b10-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="37b10-109">添加一个派生自**ApiController**类的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="37b10-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="37b10-110">将路由表添加到**应用程序\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="37b10-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="37b10-111">创建 Web 窗体项目</span><span class="sxs-lookup"><span data-stu-id="37b10-111">Create a Web Forms Project</span></span>

<span data-ttu-id="37b10-112">启动 Visual Studio，然后从**起始**页中选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="37b10-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="37b10-113">或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。</span><span class="sxs-lookup"><span data-stu-id="37b10-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="37b10-114">在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="37b10-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="37b10-115">在 **" C#视觉对象**" 下选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="37b10-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="37b10-116">在项目模板列表中，选择 " **ASP.NET Web 窗体应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="37b10-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="37b10-117">输入项目的名称，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="37b10-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="37b10-118">创建模型和控制器</span><span class="sxs-lookup"><span data-stu-id="37b10-118">Create the Model and Controller</span></span>

<span data-ttu-id="37b10-119">本教程使用与[入门](tutorial-your-first-web-api.md)教程相同的模型和控制器类。</span><span class="sxs-lookup"><span data-stu-id="37b10-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="37b10-120">首先，添加一个模型类。</span><span class="sxs-lookup"><span data-stu-id="37b10-120">First, add a model class.</span></span> <span data-ttu-id="37b10-121">在**解决方案资源管理器**中，右键单击项目，然后选择 "**添加类**"。</span><span class="sxs-lookup"><span data-stu-id="37b10-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="37b10-122">将类命名为 "Product"，并添加以下实现：</span><span class="sxs-lookup"><span data-stu-id="37b10-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="37b10-123">接下来，将 Web API 控制器添加到项目。，*控制器*是处理 Web API 的 HTTP 请求的对象。</span><span class="sxs-lookup"><span data-stu-id="37b10-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="37b10-124">在“解决方案资源管理器”中，右键单击项目。</span><span class="sxs-lookup"><span data-stu-id="37b10-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="37b10-125">选择 "**添加新项**"。</span><span class="sxs-lookup"><span data-stu-id="37b10-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="37b10-126">在 "**已安装的模板**" 下，展开 **C#视觉对象**并选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="37b10-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="37b10-127">然后，在模板列表中，选择 " **WEB API 控制器类**"。</span><span class="sxs-lookup"><span data-stu-id="37b10-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="37b10-128">将控制器命名为 "ProductsController"，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="37b10-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="37b10-129">"**添加新项**" 向导将创建一个名为 "ProductsController.cs" 的文件。</span><span class="sxs-lookup"><span data-stu-id="37b10-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="37b10-130">删除向导包含的方法并添加以下方法：</span><span class="sxs-lookup"><span data-stu-id="37b10-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="37b10-131">有关此控制器中代码的详细信息，请参阅[入门](tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="37b10-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="37b10-132">添加路由信息</span><span class="sxs-lookup"><span data-stu-id="37b10-132">Add Routing Information</span></span>

<span data-ttu-id="37b10-133">接下来，我们将添加 URI 路由，以便将 &quot;/api/products/&quot; 格式的 Uri 路由到控制器。</span><span class="sxs-lookup"><span data-stu-id="37b10-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="37b10-134">在**解决方案资源管理器**中，双击 "global.asax" 打开代码隐藏文件 Global.asax.cs。</span><span class="sxs-lookup"><span data-stu-id="37b10-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="37b10-135">添加以下**using**语句。</span><span class="sxs-lookup"><span data-stu-id="37b10-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="37b10-136">然后，将以下代码添加到**应用程序\_Start**方法：</span><span class="sxs-lookup"><span data-stu-id="37b10-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="37b10-137">有关路由表的详细信息，请参阅[中的路由 ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="37b10-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="37b10-138">添加客户端 AJAX</span><span class="sxs-lookup"><span data-stu-id="37b10-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="37b10-139">这就是创建客户端可以访问的 web API 所需的全部工作。</span><span class="sxs-lookup"><span data-stu-id="37b10-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="37b10-140">现在，让我们添加一个使用 jQuery 调用 API 的 HTML 页面。</span><span class="sxs-lookup"><span data-stu-id="37b10-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="37b10-141">请确保母版页（例如*master*）包含 `ID="HeadContent"`的 `ContentPlaceHolder`：</span><span class="sxs-lookup"><span data-stu-id="37b10-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="37b10-142">打开文件 "default.aspx"。</span><span class="sxs-lookup"><span data-stu-id="37b10-142">Open the file Default.aspx.</span></span> <span data-ttu-id="37b10-143">替换主要内容部分中的样本文本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="37b10-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="37b10-144">接下来，在 `HeaderContent` 部分中添加对 jQuery 源文件的引用：</span><span class="sxs-lookup"><span data-stu-id="37b10-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="37b10-145">注意：通过将文件从**解决方案资源管理器**拖放到代码编辑器窗口中，可以轻松地添加脚本引用。</span><span class="sxs-lookup"><span data-stu-id="37b10-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="37b10-146">在 jQuery script 标记下面添加以下脚本块：</span><span class="sxs-lookup"><span data-stu-id="37b10-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="37b10-147">加载文档时，此脚本将发出 AJAX 请求，&quot;api/产品&quot;。</span><span class="sxs-lookup"><span data-stu-id="37b10-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="37b10-148">请求返回 JSON 格式的产品列表。</span><span class="sxs-lookup"><span data-stu-id="37b10-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="37b10-149">该脚本将产品信息添加到 HTML 表中。</span><span class="sxs-lookup"><span data-stu-id="37b10-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="37b10-150">运行应用程序时，该应用程序应如下所示：</span><span class="sxs-lookup"><span data-stu-id="37b10-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
