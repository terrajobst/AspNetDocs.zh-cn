---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Web API 中使用 ASP.NET Web 窗体的 ASP.NET 4.x
author: MikeWasson
description: 教程代码地将 Web API 添加到 ASP.NET 窗体应用程序，asp.net 4.x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59422572"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="aeeaa-103">向 ASP.NET Web 窗体使用 Web API</span><span class="sxs-lookup"><span data-stu-id="aeeaa-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="aeeaa-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="aeeaa-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="aeeaa-105">本教程将指导你完成将 Web API 添加到 ASP.NET 中传统的 ASP.NET Web 窗体应用程序的步骤 4.x。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="aeeaa-106">概述</span><span class="sxs-lookup"><span data-stu-id="aeeaa-106">Overview</span></span>

<span data-ttu-id="aeeaa-107">尽管 ASP.NET Web API 与 ASP.NET MVC 一起打包，很容易地将 Web API 添加到传统的 ASP.NET Web 窗体应用程序。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="aeeaa-108">若要在 Web 窗体应用程序中使用 Web API，有两个主要步骤：</span><span class="sxs-lookup"><span data-stu-id="aeeaa-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="aeeaa-109">添加 Web API 控制器派生自**ApiController**类。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="aeeaa-110">添加到路由表**应用程序\_启动**方法。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="aeeaa-111">创建 Web 窗体项目</span><span class="sxs-lookup"><span data-stu-id="aeeaa-111">Create a Web Forms Project</span></span>

<span data-ttu-id="aeeaa-112">启动 Visual Studio 并选择**新的项目**从**启动**页。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="aeeaa-113">或者，从**文件**菜单中，选择**新建**，然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="aeeaa-114">在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="aeeaa-115">下**Visual C#**，选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="aeeaa-116">在项目模板列表中选择**ASP.NET Web 窗体应用程序**。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="aeeaa-117">输入项目的名称，然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="aeeaa-118">创建模型和控制器</span><span class="sxs-lookup"><span data-stu-id="aeeaa-118">Create the Model and Controller</span></span>

<span data-ttu-id="aeeaa-119">本教程使用相同的模型和控制器类[Getting Started](tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="aeeaa-120">首先，添加一个模型类。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-120">First, add a model class.</span></span> <span data-ttu-id="aeeaa-121">在中**解决方案资源管理器**，右键单击该项目并选择**添加类**。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="aeeaa-122">命名类产品，并添加以下实现：</span><span class="sxs-lookup"><span data-stu-id="aeeaa-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="aeeaa-123">接下来，将 Web API 控制器添加到项目中。，一个*控制器*是针对 Web API 处理 HTTP 请求的对象。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="aeeaa-124">在“解决方案资源管理器”中，右键单击项目。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="aeeaa-125">选择**添加新项**。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="aeeaa-126">下**已安装的模板**，展开**Visual C#** ，然后选择**Web**。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="aeeaa-127">然后，从模板列表中，选择**Web API 控制器类**。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="aeeaa-128">将控制器命名为"ProductsController"，然后单击**添加**。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="aeeaa-129">**添加新项**向导将创建一个名为 ProductsController.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="aeeaa-130">删除向导包括的方法并添加以下方法：</span><span class="sxs-lookup"><span data-stu-id="aeeaa-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="aeeaa-131">有关此控制器中的代码的详细信息，请参阅[Getting Started](tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="aeeaa-132">添加路由信息</span><span class="sxs-lookup"><span data-stu-id="aeeaa-132">Add Routing Information</span></span>

<span data-ttu-id="aeeaa-133">接下来，我们将因此添加 URI 路由该形式的 Uri &quot;/api/产品/&quot;路由到控制器。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="aeeaa-134">在中**解决方案资源管理器**，双击 Global.asax 以打开代码隐藏文件 Global.asax.cs。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="aeeaa-135">添加以下**使用**语句。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="aeeaa-136">然后将以下代码添加到**应用程序\_启动**方法：</span><span class="sxs-lookup"><span data-stu-id="aeeaa-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="aeeaa-137">有关路由表的详细信息，请参阅[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="aeeaa-138">添加客户端 AJAX</span><span class="sxs-lookup"><span data-stu-id="aeeaa-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="aeeaa-139">这是您需要创建的 web 客户端可以访问的 API。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="aeeaa-140">现在让我们添加使用 jQuery 来调用 API 的 HTML 页。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="aeeaa-141">请确保主页面 (例如， *Site.Master*) 包括`ContentPlaceHolder`与`ID="HeadContent"`:</span><span class="sxs-lookup"><span data-stu-id="aeeaa-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="aeeaa-142">打开 Default.aspx 文件。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-142">Open the file Default.aspx.</span></span> <span data-ttu-id="aeeaa-143">替换为在主内容部分中，样板文本所示：</span><span class="sxs-lookup"><span data-stu-id="aeeaa-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="aeeaa-144">接下来，添加对 jQuery 源代码文件中的引用`HeaderContent`部分：</span><span class="sxs-lookup"><span data-stu-id="aeeaa-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="aeeaa-145">注意:您可以方便地添加脚本引用，通过拖放文件从**解决方案资源管理器**的代码编辑器窗口中。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="aeeaa-146">下面的 jQuery 脚本标记，添加以下脚本块：</span><span class="sxs-lookup"><span data-stu-id="aeeaa-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="aeeaa-147">当文档加载后时，此脚本进行到 AJAX 请求&quot;api/产品&quot;。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="aeeaa-148">该请求以 JSON 格式返回的产品的列表。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="aeeaa-149">该脚本将产品信息添加到 HTML 表。</span><span class="sxs-lookup"><span data-stu-id="aeeaa-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="aeeaa-150">当您运行该应用程序时，它应如下所示：</span><span class="sxs-lookup"><span data-stu-id="aeeaa-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
