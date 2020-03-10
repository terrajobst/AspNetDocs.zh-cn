---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 自承载 ASP.NET Web API 1 （C#）-ASP.NET 4。x
author: MikeWasson
description: 代码教程介绍了如何在控制台应用程序中承载 web API。
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421370"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="c44ee-103">自承载 ASP.NET Web API 1 （C#）</span><span class="sxs-lookup"><span data-stu-id="c44ee-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="c44ee-104">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c44ee-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="c44ee-105">本教程介绍如何在控制台应用程序中承载 web API。</span><span class="sxs-lookup"><span data-stu-id="c44ee-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="c44ee-106">ASP.NET Web API 不需要 IIS。</span><span class="sxs-lookup"><span data-stu-id="c44ee-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="c44ee-107">你可以在自己的主机进程中自承载 web API。</span><span class="sxs-lookup"><span data-stu-id="c44ee-107">You can self-host a web API in your own host process.</span></span> 
> 
> <span data-ttu-id="c44ee-108">**新应用程序应使用 OWIN 到自承载 Web API。**</span><span class="sxs-lookup"><span data-stu-id="c44ee-108">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="c44ee-109">请参阅[使用 OWIN ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="c44ee-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c44ee-110">本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="c44ee-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="c44ee-111">Web API 1</span><span class="sxs-lookup"><span data-stu-id="c44ee-111">Web API 1</span></span>
> - <span data-ttu-id="c44ee-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="c44ee-112">Visual Studio 2012</span></span>

## <a name="create-the-console-application-project"></a><span data-ttu-id="c44ee-113">创建控制台应用程序项目</span><span class="sxs-lookup"><span data-stu-id="c44ee-113">Create the Console Application Project</span></span>

<span data-ttu-id="c44ee-114">启动 Visual Studio，然后从**起始**页中选择 "**新建项目**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="c44ee-115">或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="c44ee-116">在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="c44ee-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="c44ee-117">在 **" C#视觉对象**" 下选择 " **Windows**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="c44ee-118">在项目模板列表中，选择 "**控制台应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="c44ee-119">将项目命名为 &quot;SelfHost&quot; 并单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="c44ee-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="c44ee-120">设置目标框架（Visual Studio 2010）</span><span class="sxs-lookup"><span data-stu-id="c44ee-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="c44ee-121">如果使用的是 Visual Studio 2010，请将目标框架更改为 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="c44ee-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="c44ee-122">（默认情况下，项目模板以[.Net Framework 客户端配置文件](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)为目标。）</span><span class="sxs-lookup"><span data-stu-id="c44ee-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="c44ee-123">在解决方案资源管理器中，右键单击项目，然后选择 "**属性**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="c44ee-124">在 "**目标框架**" 下拉列表中，将 "目标框架" 更改为 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="c44ee-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="c44ee-125">出现应用更改提示时，单击 **"是"** 。</span><span class="sxs-lookup"><span data-stu-id="c44ee-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="c44ee-126">安装 NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="c44ee-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="c44ee-127">NuGet 包管理器是将 Web API 程序集添加到 non-ASP.NET 项目的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="c44ee-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="c44ee-128">若要检查是否安装了 NuGet 包管理器，请单击 Visual Studio 中的 "**工具**" 菜单。</span><span class="sxs-lookup"><span data-stu-id="c44ee-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="c44ee-129">如果你看到名为 " **Nuget 包管理器**" 的菜单项，则具有 Nuget 包管理器。</span><span class="sxs-lookup"><span data-stu-id="c44ee-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="c44ee-130">安装 NuGet 包管理器：</span><span class="sxs-lookup"><span data-stu-id="c44ee-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="c44ee-131">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c44ee-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="c44ee-132">在“工具”菜单上，选择“扩展和更新”。</span><span class="sxs-lookup"><span data-stu-id="c44ee-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="c44ee-133">在 "**扩展和更新**" 对话框中，选择 "**联机**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="c44ee-134">如果看不到 "NuGet 程序包管理器"，请在 "搜索" 框中键入 "nuget 包管理器"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="c44ee-135">选择 NuGet 包管理器，然后单击 "**下载**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="c44ee-136">下载完成后，系统会提示你进行安装。</span><span class="sxs-lookup"><span data-stu-id="c44ee-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="c44ee-137">安装完成后，系统可能会提示你重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c44ee-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="c44ee-138">添加 Web API NuGet 包</span><span class="sxs-lookup"><span data-stu-id="c44ee-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="c44ee-139">安装 NuGet 包管理器后，将 Web API 自承载包添加到项目。</span><span class="sxs-lookup"><span data-stu-id="c44ee-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="c44ee-140">从 "**工具**" 菜单中选择 " **NuGet 包管理器**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="c44ee-141">*注意*：如果看不到此菜单项，请确保已正确安装 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="c44ee-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="c44ee-142">选择 "**管理解决方案的 NuGet 包**"</span><span class="sxs-lookup"><span data-stu-id="c44ee-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="c44ee-143">在 "**管理 NugGet 包**" 对话框中，选择 "**联机**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="c44ee-144">在搜索框中，键入 "WebApi"&quot;&quot;。</span><span class="sxs-lookup"><span data-stu-id="c44ee-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="c44ee-145">选择 ASP.NET Web API 己方主机包，然后单击 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="c44ee-146">安装包后，单击 "**关闭**" 以关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="c44ee-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="c44ee-147">请确保安装名为 WebApi 的包，而不是 AspNetWebApi. SelfHost。</span><span class="sxs-lookup"><span data-stu-id="c44ee-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="c44ee-148">创建模型和控制器</span><span class="sxs-lookup"><span data-stu-id="c44ee-148">Create the Model and Controller</span></span>

<span data-ttu-id="c44ee-149">本教程使用与[入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程相同的模型和控制器类。</span><span class="sxs-lookup"><span data-stu-id="c44ee-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="c44ee-150">添加一个名为 `Product`的公共类。</span><span class="sxs-lookup"><span data-stu-id="c44ee-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="c44ee-151">添加一个名为 `ProductsController`的公共类。</span><span class="sxs-lookup"><span data-stu-id="c44ee-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="c44ee-152">从**ApiController**派生此类。</span><span class="sxs-lookup"><span data-stu-id="c44ee-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="c44ee-153">有关此控制器中代码的详细信息，请参阅[入门](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="c44ee-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="c44ee-154">此控制器定义三个 GET 操作：</span><span class="sxs-lookup"><span data-stu-id="c44ee-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="c44ee-155">URI</span><span class="sxs-lookup"><span data-stu-id="c44ee-155">URI</span></span> | <span data-ttu-id="c44ee-156">说明</span><span class="sxs-lookup"><span data-stu-id="c44ee-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c44ee-157">/api/products</span><span class="sxs-lookup"><span data-stu-id="c44ee-157">/api/products</span></span> | <span data-ttu-id="c44ee-158">获取所有产品的列表。</span><span class="sxs-lookup"><span data-stu-id="c44ee-158">Get a list of all products.</span></span> |
| <span data-ttu-id="c44ee-159">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="c44ee-159">/api/products/*id*</span></span> | <span data-ttu-id="c44ee-160">按 ID 获取产品。</span><span class="sxs-lookup"><span data-stu-id="c44ee-160">Get a product by ID.</span></span> |
| <span data-ttu-id="c44ee-161">/api/products/？ category =*类别*</span><span class="sxs-lookup"><span data-stu-id="c44ee-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="c44ee-162">按类别获取产品列表。</span><span class="sxs-lookup"><span data-stu-id="c44ee-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="c44ee-163">承载 Web API</span><span class="sxs-lookup"><span data-stu-id="c44ee-163">Host the Web API</span></span>

<span data-ttu-id="c44ee-164">打开文件 Program.cs 并添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="c44ee-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="c44ee-165">将以下代码添加到**Program**类。</span><span class="sxs-lookup"><span data-stu-id="c44ee-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="c44ee-166">可有可无添加 HTTP URL 命名空间保留</span><span class="sxs-lookup"><span data-stu-id="c44ee-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="c44ee-167">此应用程序侦听 `http://localhost:8080/`。</span><span class="sxs-lookup"><span data-stu-id="c44ee-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="c44ee-168">默认情况下，侦听特定的 HTTP 地址需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="c44ee-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="c44ee-169">因此，当你运行本教程时，你可能会收到以下错误： "HTTP 无法注册 URL http://+:8080/" 可通过两种方法来避免此错误：</span><span class="sxs-lookup"><span data-stu-id="c44ee-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="c44ee-170">以提升的管理员权限运行 Visual Studio，或</span><span class="sxs-lookup"><span data-stu-id="c44ee-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="c44ee-171">使用 dism.exe 为你的帐户授予保留 URL 的权限。</span><span class="sxs-lookup"><span data-stu-id="c44ee-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="c44ee-172">若要使用 dism.exe，请使用管理员权限打开命令提示符，然后输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="c44ee-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="c44ee-173">其中，\*计算机 \* 是你的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="c44ee-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="c44ee-174">完成自承载后，请确保删除该保留：</span><span class="sxs-lookup"><span data-stu-id="c44ee-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="c44ee-175">从客户端应用程序调用 Web API （C#）</span><span class="sxs-lookup"><span data-stu-id="c44ee-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="c44ee-176">让我们编写一个简单的控制台应用程序来调用 web API。</span><span class="sxs-lookup"><span data-stu-id="c44ee-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="c44ee-177">向解决方案添加新的控制台应用程序项目：</span><span class="sxs-lookup"><span data-stu-id="c44ee-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="c44ee-178">在解决方案资源管理器中，右键单击解决方案并选择 "**添加新项目**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="c44ee-179">创建一个名为 &quot;ClientApp&quot;的新控制台应用程序。</span><span class="sxs-lookup"><span data-stu-id="c44ee-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="c44ee-180">使用 NuGet 包管理器添加 ASP.NET Web API 核心库包：</span><span class="sxs-lookup"><span data-stu-id="c44ee-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="c44ee-181">从 "工具" 菜单中选择 " **NuGet 包管理器**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="c44ee-182">选择 "**管理解决方案的 NuGet 包**"</span><span class="sxs-lookup"><span data-stu-id="c44ee-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="c44ee-183">在 "**管理 NuGet 包**" 对话框中，选择 "**联机**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="c44ee-184">在搜索框中，键入 "WebApi"&quot;&quot;。</span><span class="sxs-lookup"><span data-stu-id="c44ee-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="c44ee-185">选择 Microsoft ASP.NET Web API 客户端库 "包，然后单击"**安装**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="c44ee-186">将 ClientApp 中的引用添加到 SelfHost 项目：</span><span class="sxs-lookup"><span data-stu-id="c44ee-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="c44ee-187">在解决方案资源管理器中，右键单击 ClientApp 项目。</span><span class="sxs-lookup"><span data-stu-id="c44ee-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="c44ee-188">选择“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="c44ee-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="c44ee-189">在 "**引用管理器**" 对话框中的 "**解决方案**" 下，选择 "**项目**"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="c44ee-190">选择 SelfHost 项目。</span><span class="sxs-lookup"><span data-stu-id="c44ee-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="c44ee-191">单击“确定”。</span><span class="sxs-lookup"><span data-stu-id="c44ee-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="c44ee-192">打开客户端/Program .cs 文件。</span><span class="sxs-lookup"><span data-stu-id="c44ee-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="c44ee-193">添加以下 **using** 语句：</span><span class="sxs-lookup"><span data-stu-id="c44ee-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="c44ee-194">添加静态**HttpClient**实例：</span><span class="sxs-lookup"><span data-stu-id="c44ee-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="c44ee-195">添加以下方法以列出所有产品，按 ID 列出产品，并按类别列出产品。</span><span class="sxs-lookup"><span data-stu-id="c44ee-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="c44ee-196">上述每种方法都遵循相同的模式：</span><span class="sxs-lookup"><span data-stu-id="c44ee-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="c44ee-197">调用**HttpClient GetAsync**将 GET 请求发送到相应的 URI。</span><span class="sxs-lookup"><span data-stu-id="c44ee-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="c44ee-198">调用**HttpResponseMessage. EnsureSuccessStatusCode**。</span><span class="sxs-lookup"><span data-stu-id="c44ee-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="c44ee-199">如果 HTTP 响应状态是错误代码，则此方法将引发异常。</span><span class="sxs-lookup"><span data-stu-id="c44ee-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="c44ee-200">调用**ReadAsAsync&lt;t&gt;** 从 HTTP 响应反序列化 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="c44ee-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="c44ee-201">此方法是在**HttpContentExtensions**中定义的扩展方法。</span><span class="sxs-lookup"><span data-stu-id="c44ee-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="c44ee-202">**GetAsync**和**ReadAsAsync**方法都是异步的。</span><span class="sxs-lookup"><span data-stu-id="c44ee-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="c44ee-203">它们返回表示异步操作的**任务**对象。</span><span class="sxs-lookup"><span data-stu-id="c44ee-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="c44ee-204">获取**Result**属性会阻止线程，直到操作完成。</span><span class="sxs-lookup"><span data-stu-id="c44ee-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="c44ee-205">有关使用 HttpClient 的详细信息，包括如何发出非阻塞调用，请参阅[从 .Net 客户端调用 WEB API](../advanced/calling-a-web-api-from-a-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="c44ee-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="c44ee-206">在调用这些方法之前，请将 HttpClient 实例上的 BaseAddress 属性设置为 "`http://localhost:8080`"。</span><span class="sxs-lookup"><span data-stu-id="c44ee-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="c44ee-207">例如:</span><span class="sxs-lookup"><span data-stu-id="c44ee-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="c44ee-208">这应输出以下。</span><span class="sxs-lookup"><span data-stu-id="c44ee-208">This should output the following.</span></span> <span data-ttu-id="c44ee-209">（请记得先运行 SelfHost 应用程序。）</span><span class="sxs-lookup"><span data-stu-id="c44ee-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
