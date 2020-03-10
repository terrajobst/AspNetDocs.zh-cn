---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: 创建 OData v4 客户端应用（C#） |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448118"
---
# <a name="create-an-odata-v4-client-app-c"></a><span data-ttu-id="da405-102">创建 OData v4 客户端应用 (C#)</span><span class="sxs-lookup"><span data-stu-id="da405-102">Create an OData v4 Client App (C#)</span></span>

<span data-ttu-id="da405-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="da405-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="da405-104">在上一教程中，你创建了支持 CRUD 操作的基本 OData 服务。</span><span class="sxs-lookup"><span data-stu-id="da405-104">In the previous tutorial, you created a basic OData service that supports CRUD operations.</span></span> <span data-ttu-id="da405-105">现在，让我们为该服务创建一个客户端。</span><span class="sxs-lookup"><span data-stu-id="da405-105">Now let's create a client for the service.</span></span>

<span data-ttu-id="da405-106">启动 Visual Studio 的新实例，并创建新的控制台应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="da405-106">Start a new instance of Visual Studio and create a new console application project.</span></span> <span data-ttu-id="da405-107">在 "**新建项目**" 对话框中，选择 "**安装**&gt;**模板**&gt;  **C# Visual** &gt; **Windows 桌面**"，然后选择 "**控制台应用程序**" 模板。</span><span class="sxs-lookup"><span data-stu-id="da405-107">In the **New Project** dialog, select **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Windows Desktop**, and select the **Console Application** template.</span></span> <span data-ttu-id="da405-108">将项目命名为 &quot;ProductsApp&quot;。</span><span class="sxs-lookup"><span data-stu-id="da405-108">Name the project &quot;ProductsApp&quot;.</span></span>

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="da405-109">你还可以将控制台应用添加到包含 OData 服务的同一 Visual Studio 解决方案中。</span><span class="sxs-lookup"><span data-stu-id="da405-109">You can also add the console app to the same Visual Studio solution that contains the OData service.</span></span>

## <a name="install-the-odata-client-code-generator"></a><span data-ttu-id="da405-110">安装 OData 客户端代码生成器</span><span class="sxs-lookup"><span data-stu-id="da405-110">Install the OData Client Code Generator</span></span>

<span data-ttu-id="da405-111">在“工具”菜单上，选择“扩展和更新”。</span><span class="sxs-lookup"><span data-stu-id="da405-111">From the **Tools** menu, select **Extensions and Updates**.</span></span> <span data-ttu-id="da405-112">选择 "**联机**&gt; **Visual Studio 库**"。</span><span class="sxs-lookup"><span data-stu-id="da405-112">Select **Online** &gt; **Visual Studio Gallery**.</span></span> <span data-ttu-id="da405-113">在搜索框中，搜索 "&quot;OData 客户端代码生成器"&quot;。</span><span class="sxs-lookup"><span data-stu-id="da405-113">In the search box, search for &quot;OData Client Code Generator&quot;.</span></span> <span data-ttu-id="da405-114">单击 "**下载**" 以安装 VSIX。</span><span class="sxs-lookup"><span data-stu-id="da405-114">Click **Download** to install the VSIX.</span></span> <span data-ttu-id="da405-115">系统可能会提示你重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="da405-115">You might be prompted to restart Visual Studio.</span></span>

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a><span data-ttu-id="da405-116">在本地运行 OData 服务</span><span class="sxs-lookup"><span data-stu-id="da405-116">Run the OData Service Locally</span></span>

<span data-ttu-id="da405-117">从 Visual Studio 运行 ProductService 项目。</span><span class="sxs-lookup"><span data-stu-id="da405-117">Run the ProductService project from Visual Studio.</span></span> <span data-ttu-id="da405-118">默认情况下，Visual Studio 会将浏览器启动到应用程序根目录。</span><span class="sxs-lookup"><span data-stu-id="da405-118">By default, Visual Studio launches a browser to the application root.</span></span> <span data-ttu-id="da405-119">记下 URI;你将在下一步中需要此项。</span><span class="sxs-lookup"><span data-stu-id="da405-119">Note the URI; you will need this in the next step.</span></span> <span data-ttu-id="da405-120">使应用程序保持运行。</span><span class="sxs-lookup"><span data-stu-id="da405-120">Leave the application running.</span></span>

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="da405-121">如果将这两个项目放在同一解决方案中，请确保在不调试的情况下运行 ProductService 项目。</span><span class="sxs-lookup"><span data-stu-id="da405-121">If you put both projects in the same solution, make sure to run the ProductService project without debugging.</span></span> <span data-ttu-id="da405-122">在下一步中，你将需要在修改控制台应用程序项目时保持该服务处于运行状态。</span><span class="sxs-lookup"><span data-stu-id="da405-122">In the next step, you will need to keep the service running while you modify the console application project.</span></span>

## <a name="generate-the-service-proxy"></a><span data-ttu-id="da405-123">生成服务代理</span><span class="sxs-lookup"><span data-stu-id="da405-123">Generate the Service Proxy</span></span>

<span data-ttu-id="da405-124">服务代理是一个 .NET 类，用于定义用于访问 OData 服务的方法。</span><span class="sxs-lookup"><span data-stu-id="da405-124">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="da405-125">代理会将方法调用转换为 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="da405-125">The proxy translates method calls into HTTP requests.</span></span> <span data-ttu-id="da405-126">您将通过运行[T4 模板](https://msdn.microsoft.com/library/bb126445.aspx)来创建代理类。</span><span class="sxs-lookup"><span data-stu-id="da405-126">You will create the proxy class by running a [T4 template](https://msdn.microsoft.com/library/bb126445.aspx).</span></span>

<span data-ttu-id="da405-127">右键单击项目。</span><span class="sxs-lookup"><span data-stu-id="da405-127">Right-click the project.</span></span> <span data-ttu-id="da405-128">选择“添加” **“新项”** &gt;。</span><span class="sxs-lookup"><span data-stu-id="da405-128">Select **Add** &gt; **New Item**.</span></span>

![](create-an-odata-v4-client-app/_static/image5.png)

<span data-ttu-id="da405-129">在 "**添加新项**" 对话框中，选择 "  **C#视觉对象项**&gt;**代码**&gt; **OData 客户端**"。</span><span class="sxs-lookup"><span data-stu-id="da405-129">In the **Add New Item** dialog, select **Visual C# Items** &gt; **Code** &gt; **OData Client**.</span></span> <span data-ttu-id="da405-130">将模板命名 &quot;ProductClient.tt&quot;。</span><span class="sxs-lookup"><span data-stu-id="da405-130">Name the template &quot;ProductClient.tt&quot;.</span></span> <span data-ttu-id="da405-131">单击 "**添加**"，然后单击安全警告。</span><span class="sxs-lookup"><span data-stu-id="da405-131">Click **Add** and click through the security warning.</span></span>

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

<span data-ttu-id="da405-132">此时，您将收到一个错误，您可以忽略该错误。</span><span class="sxs-lookup"><span data-stu-id="da405-132">At this point, you'll get an error, which you can ignore.</span></span> <span data-ttu-id="da405-133">Visual Studio 会自动运行该模板，但模板首先需要一些配置设置。</span><span class="sxs-lookup"><span data-stu-id="da405-133">Visual Studio automatically runs the template, but the template needs some configuration settings first.</span></span>

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

<span data-ttu-id="da405-134">打开文件 ProductClient。在 `Parameter` 元素中，从 ProductService 项目中粘贴 URI （上一步）。</span><span class="sxs-lookup"><span data-stu-id="da405-134">Open the file ProductClient.odata.config. In the `Parameter` element, paste in the URI from the ProductService project (previous step).</span></span> <span data-ttu-id="da405-135">例如:</span><span class="sxs-lookup"><span data-stu-id="da405-135">For example:</span></span>

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

<span data-ttu-id="da405-136">再次运行模板。</span><span class="sxs-lookup"><span data-stu-id="da405-136">Run the template again.</span></span> <span data-ttu-id="da405-137">在解决方案资源管理器中，右键单击 ProductClient.tt 文件并选择 "**运行自定义工具**"。</span><span class="sxs-lookup"><span data-stu-id="da405-137">In Solution Explorer, right click the ProductClient.tt file and select **Run Custom Tool**.</span></span>

<span data-ttu-id="da405-138">此模板创建一个名为 ProductClient.cs 的代码文件，用于定义代理。</span><span class="sxs-lookup"><span data-stu-id="da405-138">The template creates a code file named ProductClient.cs that defines the proxy.</span></span> <span data-ttu-id="da405-139">开发应用时，如果更改 OData 终结点，请再次运行模板以更新代理。</span><span class="sxs-lookup"><span data-stu-id="da405-139">As you develop your app, if you change the OData endpoint, run the template again to update the proxy.</span></span>

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a><span data-ttu-id="da405-140">使用服务代理调用 OData 服务</span><span class="sxs-lookup"><span data-stu-id="da405-140">Use the Service Proxy to Call the OData Service</span></span>

<span data-ttu-id="da405-141">打开文件 Program.cs，并将样板代码替换为以下代码。</span><span class="sxs-lookup"><span data-stu-id="da405-141">Open the file Program.cs and replace the boilerplate code with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

<span data-ttu-id="da405-142">将*serviceUri*的值替换为前面的服务 URI。</span><span class="sxs-lookup"><span data-stu-id="da405-142">Replace the value of *serviceUri* with the service URI from earlier.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

<span data-ttu-id="da405-143">运行应用时，它应输出以下内容：</span><span class="sxs-lookup"><span data-stu-id="da405-143">When you run the app, it should output the following:</span></span>

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
