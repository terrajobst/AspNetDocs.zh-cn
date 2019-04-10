---
uid: web-api/overview/older-versions/self-host-a-web-api
title: 自承载 ASP.NET Web API 1 (C#)-ASP.NET 4.x
author: MikeWasson
description: 使用代码的教程演示如何承载在控制台应用程序的 web API。
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: 7c73bf4734f8ed8a1bf93595c0847f611ad9cc15
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59409598"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="b1d9b-103">自承载 ASP.NET Web API 1 (C#)</span><span class="sxs-lookup"><span data-stu-id="b1d9b-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="b1d9b-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b1d9b-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="b1d9b-105">本教程演示如何承载在控制台应用程序的 web API。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="b1d9b-106">ASP.NET Web API 不需要 IIS。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="b1d9b-107">您可以在自己的主机进程中自托管 web API。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-107">You can self-host a web API in your own host process.</span></span> 
> 
> **<span data-ttu-id="b1d9b-108">新的应用程序应使用 OWIN 自托管 Web API。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-108">New applications should use OWIN to self-host Web API.</span></span>** <span data-ttu-id="b1d9b-109">请参阅[使用 OWIN 自托管 ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b1d9b-110">在本教程中使用的软件版本</span><span class="sxs-lookup"><span data-stu-id="b1d9b-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b1d9b-111">Web API 1</span><span class="sxs-lookup"><span data-stu-id="b1d9b-111">Web API 1</span></span>
> - <span data-ttu-id="b1d9b-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="b1d9b-112">Visual Studio 2012</span></span>


## <a name="create-the-console-application-project"></a><span data-ttu-id="b1d9b-113">创建控制台应用程序项目</span><span class="sxs-lookup"><span data-stu-id="b1d9b-113">Create the Console Application Project</span></span>

<span data-ttu-id="b1d9b-114">启动 Visual Studio 并选择**新的项目**从**启动**页。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="b1d9b-115">或者，从**文件**菜单中，选择**新建**，然后**项目**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="b1d9b-116">在中**模板**窗格中，选择**已安装的模板**展开**Visual C#** 节点。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="b1d9b-117">下**Visual C#**，选择**Windows**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="b1d9b-118">在项目模板列表中选择**控制台应用程序**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="b1d9b-119">将项目命名&quot;SelfHost&quot;然后单击**确定**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="b1d9b-120">设置目标框架 (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="b1d9b-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="b1d9b-121">如果使用 Visual Studio 2010，更改目标框架为.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="b1d9b-122">(默认情况下，项目模板面向[.Net Framework 客户端配置文件](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)。)</span><span class="sxs-lookup"><span data-stu-id="b1d9b-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="b1d9b-123">在解决方案资源管理器，右键单击该项目并选择**属性**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="b1d9b-124">在中**目标框架**下拉列表中，将目标框架更改为.NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="b1d9b-125">当系统提示以应用更改，单击**是**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="b1d9b-126">安装 NuGet 包管理器</span><span class="sxs-lookup"><span data-stu-id="b1d9b-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="b1d9b-127">NuGet 包管理器是 Web API 程序集添加到非 ASP.NET 项目的最简单方法。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="b1d9b-128">若要检查是否已安装 NuGet 包管理器，请单击**工具**Visual Studio 菜单中的。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="b1d9b-129">如果看到一个菜单项调用**NuGet 包管理器**，则具有 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="b1d9b-130">若要安装 NuGet 包管理器：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="b1d9b-131">启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="b1d9b-132">从**工具**菜单中，选择**扩展和更新**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="b1d9b-133">在中**扩展和更新**对话框中，选择**联机**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="b1d9b-134">如果看不到"NuGet 包管理器"，请在搜索框中键入"nuget 包管理器"。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="b1d9b-135">选择 NuGet 包管理器，然后单击**下载**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="b1d9b-136">下载完成后，系统将提示安装。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="b1d9b-137">安装完成后，你可能会提示您重新启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="b1d9b-138">添加 Web API NuGet 包</span><span class="sxs-lookup"><span data-stu-id="b1d9b-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="b1d9b-139">安装 NuGet 包管理器后，将 Web API 自托管包添加到你的项目。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="b1d9b-140">从**工具**菜单中，选择**NuGet 包管理器**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="b1d9b-141">*说明*：如果您不会看到此菜单项，请确保已正确安装该 NuGet 包管理器。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="b1d9b-142">选择**管理解决方案的 NuGet 包**</span><span class="sxs-lookup"><span data-stu-id="b1d9b-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="b1d9b-143">在中**Manage NugGet Packages**对话框中，选择**联机**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="b1d9b-144">在搜索框中，键入&quot;Microsoft.AspNet.WebApi.SelfHost&quot;。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="b1d9b-145">选择 ASP.NET Web API 自宿主包，然后单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="b1d9b-146">包将安装后，单击**关闭**关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="b1d9b-147">请确保安装名为 Microsoft.AspNet.WebApi.SelfHost，不 AspNetWebApi.SelfHost 的包。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="b1d9b-148">创建模型和控制器</span><span class="sxs-lookup"><span data-stu-id="b1d9b-148">Create the Model and Controller</span></span>

<span data-ttu-id="b1d9b-149">本教程使用相同的模型和控制器类[Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="b1d9b-150">添加一个名为的公共类`Product`。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="b1d9b-151">添加一个名为的公共类`ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="b1d9b-152">从该类派生**System.Web.Http.ApiController**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="b1d9b-153">有关此控制器中的代码的详细信息，请参阅[Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)教程。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="b1d9b-154">此控制器定义了三个 GET 操作：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="b1d9b-155">URI</span><span class="sxs-lookup"><span data-stu-id="b1d9b-155">URI</span></span> | <span data-ttu-id="b1d9b-156">描述</span><span class="sxs-lookup"><span data-stu-id="b1d9b-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b1d9b-157">/api/products</span><span class="sxs-lookup"><span data-stu-id="b1d9b-157">/api/products</span></span> | <span data-ttu-id="b1d9b-158">获取所有产品的列表。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-158">Get a list of all products.</span></span> |
| <span data-ttu-id="b1d9b-159">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="b1d9b-159">/api/products/*id*</span></span> | <span data-ttu-id="b1d9b-160">获取产品的 id。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-160">Get a product by ID.</span></span> |
| <span data-ttu-id="b1d9b-161">/api/products/?category=*category*</span><span class="sxs-lookup"><span data-stu-id="b1d9b-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="b1d9b-162">按类别获取的产品的列表。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="b1d9b-163">承载 Web API</span><span class="sxs-lookup"><span data-stu-id="b1d9b-163">Host the Web API</span></span>

<span data-ttu-id="b1d9b-164">打开文件 Program.cs 并添加以下 using 语句：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="b1d9b-165">将以下代码添加到**程序**类。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="b1d9b-166">（可选）添加 HTTP URL Namespace 保留</span><span class="sxs-lookup"><span data-stu-id="b1d9b-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="b1d9b-167">此应用程序侦听`http://localhost:8080/`。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="b1d9b-168">默认情况下，侦听特定的 HTTP 地址需要管理员权限。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="b1d9b-169">当您运行本教程时，因此，可能会收到此错误："HTTP 无法注册 URL http://+:8080/"有两种方法来避免此错误：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="b1d9b-170">使用提升的管理员权限运行 Visual Studio 或</span><span class="sxs-lookup"><span data-stu-id="b1d9b-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="b1d9b-171">使用 Netsh.exe 让你的帐户权限以保留该 URL。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="b1d9b-172">若要使用 Netsh.exe，使用管理员特权打开命令提示符并输入以下命令： 以下命令：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="b1d9b-173">其中*按*是您的用户帐户。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="b1d9b-174">完成之后自承载，请务必删除保留：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="b1d9b-175">从客户端应用程序 (C#) 中调用 Web API</span><span class="sxs-lookup"><span data-stu-id="b1d9b-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="b1d9b-176">让我们来编写一个简单的控制台应用程序调用 web API。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="b1d9b-177">将新的控制台应用程序项目添加到解决方案：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="b1d9b-178">在解决方案资源管理器，右键单击解决方案并选择**添加新项目**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="b1d9b-179">创建名为的新控制台应用程序&quot;ClientApp&quot;。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="b1d9b-180">使用 NuGet 包管理器来添加 ASP.NET Web API 的核心库包：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="b1d9b-181">从工具菜单中，选择**NuGet 包管理器**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="b1d9b-182">选择**管理解决方案的 NuGet 包**</span><span class="sxs-lookup"><span data-stu-id="b1d9b-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="b1d9b-183">在中**管理 NuGet 包**对话框中，选择**联机**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="b1d9b-184">在搜索框中，键入&quot;Microsoft.AspNet.WebApi.Client&quot;。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="b1d9b-185">选择 Microsoft ASP.NET Web API 客户端库包，然后单击**安装**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="b1d9b-186">到 SelfHost 项目 ClientApp 中添加的引用：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="b1d9b-187">在解决方案资源管理器，右键单击 ClientApp 项目。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="b1d9b-188">选择“添加引用”。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="b1d9b-189">在中**引用管理器**对话框下**解决方案**，选择**项目**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="b1d9b-190">选择 SelfHost 项目。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="b1d9b-191">单击 **“确定”**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="b1d9b-192">打开 Client/Program.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="b1d9b-193">添加以下**使用**语句：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="b1d9b-194">添加静态**HttpClient**实例：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="b1d9b-195">添加以下方法来按类别列出的所有产品，列表按 ID、 产品和产品列表。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="b1d9b-196">每种方法如下所示相同的模式：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="b1d9b-197">调用**HttpClient.GetAsync**将 GET 请求发送到的相应 URI。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="b1d9b-198">调用**HttpResponseMessage.EnsureSuccessStatusCode**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="b1d9b-199">如果 HTTP 响应状态为错误代码，此方法将引发异常。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="b1d9b-200">调用**ReadAsAsync&lt;T&gt;** 要反序列化的 HTTP 响应中的 CLR 类型。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="b1d9b-201">此方法是在定义的扩展方法**System.Net.Http.HttpContentExtensions**。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="b1d9b-202">**GetAsync**并**ReadAsAsync**方法均异步。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="b1d9b-203">它们将返回**任务**对象，后者表示异步操作。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="b1d9b-204">获取**结果**属性阻止线程，直到操作完成。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="b1d9b-205">有关使用 HttpClient，包括如何执行非阻止调用，请参阅[调用 Web API 从.NET 客户端](../advanced/calling-a-web-api-from-a-net-client.md)。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="b1d9b-206">调用这些方法之前, 将 BaseAddress 属性设置到 HttpClient 实例上"`http://localhost:8080`"。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="b1d9b-207">例如：</span><span class="sxs-lookup"><span data-stu-id="b1d9b-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="b1d9b-208">这应输出以下。</span><span class="sxs-lookup"><span data-stu-id="b1d9b-208">This should output the following.</span></span> <span data-ttu-id="b1d9b-209">（请记住要首先运行 SelfHost 应用程序。）</span><span class="sxs-lookup"><span data-stu-id="b1d9b-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
