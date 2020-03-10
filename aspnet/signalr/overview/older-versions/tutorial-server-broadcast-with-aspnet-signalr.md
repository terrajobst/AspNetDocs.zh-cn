---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: 教程：通过 ASP.NET SignalR 1.x 进行服务器广播 |Microsoft Docs
author: bradygaster
description: 本教程介绍如何创建使用 ASP.NET SignalR 提供服务器广播功能的 web 应用程序。 服务器广播意味着 communic
ms.author: bradyg
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 68908be34f6b010e512677fe5f5e31bfdefab592
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467930"
---
# <a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a><span data-ttu-id="c4502-104">教程：通过 ASP.NET SignalR 1.x 进行服务器广播</span><span class="sxs-lookup"><span data-stu-id="c4502-104">Tutorial: Server Broadcast with ASP.NET SignalR 1.x</span></span>

<span data-ttu-id="c4502-105">作者： [Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="c4502-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c4502-106">本教程介绍如何创建使用 ASP.NET SignalR 提供服务器广播功能的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4502-106">This tutorial shows how to create a web application that uses ASP.NET SignalR to provide server broadcast functionality.</span></span> <span data-ttu-id="c4502-107">服务器广播表示发送到客户端的通信由服务器启动。</span><span class="sxs-lookup"><span data-stu-id="c4502-107">Server broadcast means that communications sent to clients are initiated by the server.</span></span> <span data-ttu-id="c4502-108">此方案需要不同于对等方案的编程方法，例如聊天应用程序，其中发送到客户端的通信由一个或多个客户端启动。</span><span class="sxs-lookup"><span data-stu-id="c4502-108">This scenario requires a different programming approach than peer-to-peer scenarios such as chat applications, in which communications sent to clients are initiated by one or more of the clients.</span></span>
> 
> <span data-ttu-id="c4502-109">你将在本教程中创建的应用程序模拟股票行情，这是服务器广播功能的典型方案。</span><span class="sxs-lookup"><span data-stu-id="c4502-109">The application that you'll create in this tutorial simulates a stock ticker, a typical scenario for server broadcast functionality.</span></span>
> 
> <span data-ttu-id="c4502-110">欢迎使用教程中的注释。</span><span class="sxs-lookup"><span data-stu-id="c4502-110">Comments on the tutorial are welcome.</span></span> <span data-ttu-id="c4502-111">如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="c4502-111">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com).</span></span>

## <a name="overview"></a><span data-ttu-id="c4502-112">概述</span><span class="sxs-lookup"><span data-stu-id="c4502-112">Overview</span></span>

<span data-ttu-id="c4502-113">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 包在 Visual Studio 项目中安装一个模拟股票行情滚动应用程序示例。</span><span class="sxs-lookup"><span data-stu-id="c4502-113">The [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package installs a sample simulated stock ticker application in a Visual Studio project.</span></span> <span data-ttu-id="c4502-114">在本教程的第一部分中，你将从头开始创建该应用程序的简化版本。</span><span class="sxs-lookup"><span data-stu-id="c4502-114">In the first part of this tutorial, you'll create a simplified version of that application from scratch.</span></span> <span data-ttu-id="c4502-115">在本教程的其余部分中，你将安装 NuGet 包并查看它创建的其他功能和代码。</span><span class="sxs-lookup"><span data-stu-id="c4502-115">In the remainder of the tutorial, you'll install the NuGet package and review the additional features and code that it creates.</span></span>

<span data-ttu-id="c4502-116">股票行情应用程序是一种实时应用程序的代表，你希望在其中定期 "推送" 或 "广播" 从服务器到所有连接的客户端的通知。</span><span class="sxs-lookup"><span data-stu-id="c4502-116">The stock ticker application is a representative of a kind of real-time application in which you want to periodically "push," or broadcast, notifications from the server to all connected clients.</span></span>

<span data-ttu-id="c4502-117">您将在本教程的第一部分中生成的应用程序将显示一个包含股票数据的网格。</span><span class="sxs-lookup"><span data-stu-id="c4502-117">The application that you'll build in the first part of this tutorial displays a grid with stock data.</span></span>

![StockTicker 初始版本](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

<span data-ttu-id="c4502-119">服务器会定期随机更新股票价格，并将更新推送到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="c4502-119">Periodically the server randomly updates stock prices and pushes the updates to all connected clients.</span></span> <span data-ttu-id="c4502-120">在浏览器中，**更改**和 **%** 列中的数字和符号会动态更改以响应来自服务器的通知。</span><span class="sxs-lookup"><span data-stu-id="c4502-120">In the browser the numbers and symbols in the **Change** and **%** columns dynamically change in response to notifications from the server.</span></span> <span data-ttu-id="c4502-121">如果你打开相同 URL 的其他浏览器，则它们都同时显示相同的数据和相同的数据更改。</span><span class="sxs-lookup"><span data-stu-id="c4502-121">If you open additional browsers to the same URL, they all show the same data and the same changes to the data simultaneously.</span></span>

<span data-ttu-id="c4502-122">本教程包含以下部分：</span><span class="sxs-lookup"><span data-stu-id="c4502-122">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="c4502-123">先决条件</span><span class="sxs-lookup"><span data-stu-id="c4502-123">Prerequisites</span></span>](#prerequisites)
- [<span data-ttu-id="c4502-124">创建项目</span><span class="sxs-lookup"><span data-stu-id="c4502-124">Create the project</span></span>](#createproject)
- [<span data-ttu-id="c4502-125">添加 SignalR NuGet 包</span><span class="sxs-lookup"><span data-stu-id="c4502-125">Add the SignalR NuGet packages</span></span>](#nugetpackages)
- [<span data-ttu-id="c4502-126">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="c4502-126">Set up the server code</span></span>](#server)
- [<span data-ttu-id="c4502-127">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="c4502-127">Set up the client code</span></span>](#client)
- [<span data-ttu-id="c4502-128">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="c4502-128">Test the application</span></span>](#test)
- [<span data-ttu-id="c4502-129">启用日志记录</span><span class="sxs-lookup"><span data-stu-id="c4502-129">Enable logging</span></span>](#enablelogging)
- [<span data-ttu-id="c4502-130">安装和查看完整的 StockTicker 示例</span><span class="sxs-lookup"><span data-stu-id="c4502-130">Install and review the full StockTicker sample</span></span>](#fullsample)
- [<span data-ttu-id="c4502-131">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c4502-131">Next steps</span></span>](#nextsteps)

> [!NOTE]
> <span data-ttu-id="c4502-132">如果不想完成生成应用程序的步骤，可以在新的**空 ASP.NET Web 应用程序**项目中安装 SignalR 包，然后通读这些步骤以获取代码的说明。</span><span class="sxs-lookup"><span data-stu-id="c4502-132">If you don't want to work through the steps of building the application, you can install the SignalR.Sample package in a new **Empty ASP.NET Web Application** project, and read through these steps to get explanations of the code.</span></span> <span data-ttu-id="c4502-133">本教程的第一部分介绍 SignalR 代码的一个子集，第二部分说明 SignalR 包中附加功能的主要功能。</span><span class="sxs-lookup"><span data-stu-id="c4502-133">The first part of the tutorial covers a subset of the SignalR.Sample code, and the second part explains key features of the additional functionality in the SignalR.Sample package.</span></span>

<a id="prerequisites"></a>

## <a name="prerequisites"></a><span data-ttu-id="c4502-134">系统必备</span><span class="sxs-lookup"><span data-stu-id="c4502-134">Prerequisites</span></span>

<span data-ttu-id="c4502-135">在开始之前，请确保已在计算机上安装 Visual Studio 2012 或 2010 SP1。</span><span class="sxs-lookup"><span data-stu-id="c4502-135">Before you start, make sure that you have Visual Studio 2012 or 2010 SP1 installed on your computer.</span></span> <span data-ttu-id="c4502-136">如果没有 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)以获取免费的 visual Studio 2012 Express for Web。</span><span class="sxs-lookup"><span data-stu-id="c4502-136">If you don't have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express for Web.</span></span>

<span data-ttu-id="c4502-137">如果安装了 Visual Studio 2010，请确保已安装[NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 。</span><span class="sxs-lookup"><span data-stu-id="c4502-137">If you have Visual Studio 2010, make sure that [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) is installed.</span></span>

<a id="createproject"></a>

## <a name="create-the-project"></a><span data-ttu-id="c4502-138">创建项目</span><span class="sxs-lookup"><span data-stu-id="c4502-138">Create the project</span></span>

1. <span data-ttu-id="c4502-139">从“文件”菜单上，单击“新建项目”。</span><span class="sxs-lookup"><span data-stu-id="c4502-139">From the **File** menu click **New Project**.</span></span>
2. <span data-ttu-id="c4502-140">在 "**新建项目**" 对话框中， **C#** 展开 "**模板**"，然后选择 " **Web**"。</span><span class="sxs-lookup"><span data-stu-id="c4502-140">In the **New Project** dialog box, expand **C#** under **Templates** and select **Web**.</span></span>
3. <span data-ttu-id="c4502-141">选择**ASP.NET 空 Web 应用程序**模板，将项目命名为*SignalR StockTicker*，然后单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="c4502-141">Select the **ASP.NET Empty Web Application** template, name the project *SignalR.StockTicker*, and click **OK**.</span></span>

    ![“新建项目”对话框](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a><span data-ttu-id="c4502-143">添加 SignalR NuGet 包</span><span class="sxs-lookup"><span data-stu-id="c4502-143">Add the SignalR NuGet Packages</span></span>

### <a name="add-the-signalr-and-jquery-nuget-packages"></a><span data-ttu-id="c4502-144">添加 SignalR 和 JQuery NuGet 包</span><span class="sxs-lookup"><span data-stu-id="c4502-144">Add the SignalR and JQuery NuGet Packages</span></span>

<span data-ttu-id="c4502-145">可以通过安装 NuGet 包将 SignalR 功能添加到项目。</span><span class="sxs-lookup"><span data-stu-id="c4502-145">You can add SignalR functionality to a project by installing a NuGet package.</span></span>

1. <span data-ttu-id="c4502-146">单击 "**工具" |NuGet 包管理器 |程序包管理器控制台**。</span><span class="sxs-lookup"><span data-stu-id="c4502-146">Click **Tools | NuGet Package Manager | Package Manager Console**.</span></span>
2. <span data-ttu-id="c4502-147">在 "包管理器" 中输入以下命令。</span><span class="sxs-lookup"><span data-stu-id="c4502-147">Enter the following command in the package manager.</span></span>

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    <span data-ttu-id="c4502-148">SignalR 包会安装多个其他 NuGet 包作为依赖项。</span><span class="sxs-lookup"><span data-stu-id="c4502-148">The SignalR package installs a number of other NuGet packages as dependencies.</span></span> <span data-ttu-id="c4502-149">安装完成后，你将拥有在 ASP.NET 应用程序中使用 SignalR 所需的所有服务器和客户端组件。</span><span class="sxs-lookup"><span data-stu-id="c4502-149">When the installation is finished you have all of the server and client components required to use SignalR in an ASP.NET application.</span></span>

<a id="server"></a>

## <a name="set-up-the-server-code"></a><span data-ttu-id="c4502-150">设置服务器代码</span><span class="sxs-lookup"><span data-stu-id="c4502-150">Set up the server code</span></span>

<span data-ttu-id="c4502-151">在本部分中，您将设置在服务器上运行的代码。</span><span class="sxs-lookup"><span data-stu-id="c4502-151">In this section you set up the code that runs on the server.</span></span>

### <a name="create-the-stock-class"></a><span data-ttu-id="c4502-152">创建 Stock 类</span><span class="sxs-lookup"><span data-stu-id="c4502-152">Create the Stock class</span></span>

<span data-ttu-id="c4502-153">首先，创建用于存储和传输股票信息的 Stock 模型类。</span><span class="sxs-lookup"><span data-stu-id="c4502-153">You begin by creating the Stock model class that you'll use to store and transmit information about a stock.</span></span>

1. <span data-ttu-id="c4502-154">在项目文件夹中创建一个新的类文件，将其命名为*Stock.cs*，然后将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c4502-154">Create a new class file in the project folder, name it *Stock.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    <span data-ttu-id="c4502-155">创建股票时要设置的两个属性是符号（例如，MSFT for Microsoft）和价格。</span><span class="sxs-lookup"><span data-stu-id="c4502-155">The two properties that you'll set when you create stocks are the Symbol (for example, MSFT for Microsoft) and the Price.</span></span> <span data-ttu-id="c4502-156">其他属性取决于设置价格的方式和时间。</span><span class="sxs-lookup"><span data-stu-id="c4502-156">The other properties depend on how and when you set Price.</span></span> <span data-ttu-id="c4502-157">首次设置价格时，该值将传播到 DayOpen。</span><span class="sxs-lookup"><span data-stu-id="c4502-157">The first time you set Price, the value gets propagated to DayOpen.</span></span> <span data-ttu-id="c4502-158">后续设置价格时，会根据价格和 DayOpen 之间的差异来计算 Change 和 PercentChange 属性值。</span><span class="sxs-lookup"><span data-stu-id="c4502-158">Subsequent times when you set Price, the Change and PercentChange property values are calculated based on the difference between Price and DayOpen.</span></span>

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a><span data-ttu-id="c4502-159">创建 StockTicker 和 StockTickerHub 类</span><span class="sxs-lookup"><span data-stu-id="c4502-159">Create the StockTicker and StockTickerHub classes</span></span>

<span data-ttu-id="c4502-160">你将使用 SignalR 中心 API 来处理服务器到客户端的交互。</span><span class="sxs-lookup"><span data-stu-id="c4502-160">You'll use the SignalR Hub API to handle server-to-client interaction.</span></span> <span data-ttu-id="c4502-161">派生自 SignalR Hub 类的 StockTickerHub 类将处理从客户端接收连接和方法调用。</span><span class="sxs-lookup"><span data-stu-id="c4502-161">A StockTickerHub class that derives from the SignalR Hub class will handle receiving connections and method calls from clients.</span></span> <span data-ttu-id="c4502-162">还需要维护股票数据并运行计时器对象，以定期触发价格更新，独立于客户端连接。</span><span class="sxs-lookup"><span data-stu-id="c4502-162">You also need to maintain stock data and run a Timer object to periodically trigger price updates, independently of client connections.</span></span> <span data-ttu-id="c4502-163">由于中心实例是暂时性的，因此不能将这些函数放在 Hub 类中。</span><span class="sxs-lookup"><span data-stu-id="c4502-163">You can't put these functions in a Hub class, because Hub instances are transient.</span></span> <span data-ttu-id="c4502-164">集线器类实例是为集线器上的每个操作创建的，例如连接和从客户端到服务器的调用。</span><span class="sxs-lookup"><span data-stu-id="c4502-164">A Hub class instance is created for each operation on the hub, such as connections and calls from the client to the server.</span></span> <span data-ttu-id="c4502-165">因此，用于保留股票数据、更新价格和广播价格更新的机制必须在单独的类中运行，你可以将其命名为 StockTicker。</span><span class="sxs-lookup"><span data-stu-id="c4502-165">So the mechanism that keeps stock data, updates prices, and broadcasts the price updates has to run in a separate class, which you'll name StockTicker.</span></span>

![从 StockTicker 广播](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

<span data-ttu-id="c4502-167">你只希望在服务器上运行 StockTicker 类的一个实例，因此你将需要设置从每个 StockTickerHub 实例到 singleton StockTicker 实例的引用。</span><span class="sxs-lookup"><span data-stu-id="c4502-167">You only want one instance of the StockTicker class to run on the server, so you'll need to set up a reference from each StockTickerHub instance to the singleton StockTicker instance.</span></span> <span data-ttu-id="c4502-168">StockTicker 类必须能够广播到客户端，因为它具有股票数据并触发更新，但 StockTicker 不是中心类。</span><span class="sxs-lookup"><span data-stu-id="c4502-168">The StockTicker class has to be able to broadcast to clients because it has the stock data and triggers updates, but StockTicker is not a Hub class.</span></span> <span data-ttu-id="c4502-169">因此，StockTicker 类必须获取对 SignalR 中心连接上下文对象的引用。</span><span class="sxs-lookup"><span data-stu-id="c4502-169">Therefore, the StockTicker class has to get a reference to the SignalR Hub connection context object.</span></span> <span data-ttu-id="c4502-170">然后，它可以使用 SignalR 连接上下文对象广播到客户端。</span><span class="sxs-lookup"><span data-stu-id="c4502-170">It can then use the SignalR connection context object to broadcast to clients.</span></span>

1. <span data-ttu-id="c4502-171">在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加新项**"。</span><span class="sxs-lookup"><span data-stu-id="c4502-171">In **Solution Explorer**, right-click the project and click **Add New Item**.</span></span>
2. <span data-ttu-id="c4502-172">如果安装了带有[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=279941)的 visual Studio 2012，请单击 "**视觉C#对象**" 下的 " **Web** "，然后选择 " **SignalR" 中心类**项模板。</span><span class="sxs-lookup"><span data-stu-id="c4502-172">If you have Visual Studio 2012 with the [ASP.NET and Web Tools 2012.2 Update](https://go.microsoft.com/fwlink/?LinkId=279941), click **Web** under **Visual C#** and select the **SignalR Hub Class** item template.</span></span> <span data-ttu-id="c4502-173">否则，请选择 "**类**" 模板。</span><span class="sxs-lookup"><span data-stu-id="c4502-173">Otherwise, select the **Class** template.</span></span>
3. <span data-ttu-id="c4502-174">将新类命名为*StockTickerHub.cs*，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="c4502-174">Name the new class *StockTickerHub.cs*, and then click **Add**.</span></span>

    ![添加 StockTickerHub.cs](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. <span data-ttu-id="c4502-176">将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c4502-176">Replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    <span data-ttu-id="c4502-177">[Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)类用于定义客户端可以在服务器上调用的方法。</span><span class="sxs-lookup"><span data-stu-id="c4502-177">The [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) class is used to define methods the clients can call on the server.</span></span> <span data-ttu-id="c4502-178">您正在定义一个方法： `GetAllStocks()`。</span><span class="sxs-lookup"><span data-stu-id="c4502-178">You are defining one method: `GetAllStocks()`.</span></span> <span data-ttu-id="c4502-179">当客户端最初连接到服务器时，它将调用此方法以获取所有股票的列表及其当前价格。</span><span class="sxs-lookup"><span data-stu-id="c4502-179">When a client initially connects to the server, it will call this method to get a list of all of the stocks with their current prices.</span></span> <span data-ttu-id="c4502-180">方法可以同步执行并返回 `IEnumerable<Stock>`，因为该方法从内存返回数据。</span><span class="sxs-lookup"><span data-stu-id="c4502-180">The method can execute synchronously and return `IEnumerable<Stock>` because it is returning data from memory.</span></span> <span data-ttu-id="c4502-181">如果该方法必须通过执行需要等待的内容（如数据库查找或 web 服务调用）来获取数据，则应将 `Task<IEnumerable<Stock>>` 指定为返回值以启用异步处理。</span><span class="sxs-lookup"><span data-stu-id="c4502-181">If the method had to get the data by doing something that would involve waiting, such as a database lookup or a web service call, you would specify `Task<IEnumerable<Stock>>` as the return value to enable asynchronous processing.</span></span> <span data-ttu-id="c4502-182">有关详细信息，请参阅[ASP.NET SignalR HUB API 指南-Server-When to 异步执行的时间](index.md)。</span><span class="sxs-lookup"><span data-stu-id="c4502-182">For more information, see [ASP.NET SignalR Hubs API Guide - Server - When to execute asynchronously](index.md).</span></span>

    <span data-ttu-id="c4502-183">HubName 属性指定如何在客户端上的 JavaScript 代码中引用中心。</span><span class="sxs-lookup"><span data-stu-id="c4502-183">The HubName attribute specifies how the Hub will be referenced in JavaScript code on the client.</span></span> <span data-ttu-id="c4502-184">如果不使用此属性，则客户端上的默认名称是类名的大小写形式，在本例中为 stockTickerHub。</span><span class="sxs-lookup"><span data-stu-id="c4502-184">The default name on the client if you don't use this attribute is a camel-cased version of the class name, which in this case would be stockTickerHub.</span></span>

    <span data-ttu-id="c4502-185">稍后在创建 StockTicker 类时，将在其静态实例属性中创建该类的单一实例。</span><span class="sxs-lookup"><span data-stu-id="c4502-185">As you'll see later when you create the StockTicker class, a singleton instance of that class is created in its static Instance property.</span></span> <span data-ttu-id="c4502-186">无论客户端连接或断开连接的客户端有多少个客户端，StockTicker 的单一实例都将保留在内存中，并且该实例是 GetAllStocks 方法用来返回当前股票信息的内容。</span><span class="sxs-lookup"><span data-stu-id="c4502-186">That singleton instance of StockTicker remains in memory no matter how many clients connect or disconnect, and that instance is what the GetAllStocks method uses to return current stock information.</span></span>
5. <span data-ttu-id="c4502-187">在项目文件夹中创建一个新的类文件，将其命名为*StockTicker.cs*，然后将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c4502-187">Create a new class file in the project folder, name it *StockTicker.cs*, and then replace the template code with the following code:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    <span data-ttu-id="c4502-188">由于多个线程将运行 StockTicker 代码的同一个实例，因此 StockTicker 类必须是 threadsafe。</span><span class="sxs-lookup"><span data-stu-id="c4502-188">Since multiple threads will be running the same instance of StockTicker code, the StockTicker class has to be threadsafe.</span></span>

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a><span data-ttu-id="c4502-189">将单一实例存储在静态字段中</span><span class="sxs-lookup"><span data-stu-id="c4502-189">Storing the singleton instance in a static field</span></span>

    <span data-ttu-id="c4502-190">此代码初始化静态 \_实例字段，该字段将支持实例属性和类的实例，这是可以创建的类的唯一实例，因为构造函数被标记为私有。</span><span class="sxs-lookup"><span data-stu-id="c4502-190">The code initializes the static \_instance field that backs the Instance property with an instance of the class, and this is the only instance of the class that can be created, because the constructor is marked as private.</span></span> <span data-ttu-id="c4502-191">[迟缓初始化](https://msdn.microsoft.com/library/dd997286.aspx)用于 \_实例字段，而不是出于性能原因，但要确保实例创建 threadsafe。</span><span class="sxs-lookup"><span data-stu-id="c4502-191">[Lazy initialization](https://msdn.microsoft.com/library/dd997286.aspx) is used for the \_instance field, not for performance reasons but to ensure that the instance creation is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    <span data-ttu-id="c4502-192">每次客户端连接到服务器时，在单独的线程中运行的 StockTickerHub 类的新实例将从 StockTicker 静态属性获取 StockTicker 单一实例，如前面在 StockTickerHub 类中看到的那样。</span><span class="sxs-lookup"><span data-stu-id="c4502-192">Each time a client connects to the server, a new instance of the StockTickerHub class running in a separate thread gets the StockTicker singleton instance from the StockTicker.Instance static property, as you saw earlier in the StockTickerHub class.</span></span>

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a><span data-ttu-id="c4502-193">在 ConcurrentDictionary 中存储股票数据</span><span class="sxs-lookup"><span data-stu-id="c4502-193">Storing stock data in a ConcurrentDictionary</span></span>

    <span data-ttu-id="c4502-194">构造函数用一些示例股票数据初始化 \_股票集合，GetAllStocks 返回股票。</span><span class="sxs-lookup"><span data-stu-id="c4502-194">The constructor initializes the \_stocks collection with some sample stock data, and GetAllStocks returns the stocks.</span></span> <span data-ttu-id="c4502-195">正如你之前所见，StockTickerHub 的这一组股票又由 GetAllStocks 返回，后者是客户端可调用的中心类中的服务器方法。</span><span class="sxs-lookup"><span data-stu-id="c4502-195">As you saw earlier, this collection of stocks is in turn returned by StockTickerHub.GetAllStocks which is a server method in the Hub class that clients can call.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    <span data-ttu-id="c4502-196">股票集合定义为线程安全的[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)类型。</span><span class="sxs-lookup"><span data-stu-id="c4502-196">The stocks collection is defined as a [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) type for thread safety.</span></span> <span data-ttu-id="c4502-197">作为替代方法，可以使用[字典](https://msdn.microsoft.com/library/xfhwa508.aspx)对象，并在对字典进行更改时显式锁定字典。</span><span class="sxs-lookup"><span data-stu-id="c4502-197">As an alternative, you could use a [Dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx) object and explicitly lock the dictionary when you make changes to it.</span></span>

    <span data-ttu-id="c4502-198">在此示例应用程序中，可以将应用程序数据存储在内存中，并在 StockTicker 实例被释放时丢失数据。</span><span class="sxs-lookup"><span data-stu-id="c4502-198">For this sample application, it's OK to store application data in memory and to lose the data when the StockTicker instance is disposed.</span></span> <span data-ttu-id="c4502-199">在实际应用程序中，你将使用后端数据存储（如数据库）。</span><span class="sxs-lookup"><span data-stu-id="c4502-199">In a real application you would work with a back-end data store such as a database.</span></span>

    ### <a name="periodically-updating-stock-prices"></a><span data-ttu-id="c4502-200">定期更新股票价格</span><span class="sxs-lookup"><span data-stu-id="c4502-200">Periodically updating stock prices</span></span>

    <span data-ttu-id="c4502-201">构造函数将启动一个 Timer 对象，该对象定期调用可随机更新股票价格的方法。</span><span class="sxs-lookup"><span data-stu-id="c4502-201">The constructor starts up a Timer object that periodically calls methods that update stock prices on a random basis.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    <span data-ttu-id="c4502-202">UpdateStockPrices 由计时器调用，它在 state 参数中传递 null。</span><span class="sxs-lookup"><span data-stu-id="c4502-202">UpdateStockPrices is called by the Timer, which passes in null in the state parameter.</span></span> <span data-ttu-id="c4502-203">更新价格之前，会对 \_updateStockPricesLock 对象进行锁定。</span><span class="sxs-lookup"><span data-stu-id="c4502-203">Before updating prices, a lock is taken on the \_updateStockPricesLock object.</span></span> <span data-ttu-id="c4502-204">该代码将检查是否有另一个线程正在更新价格，然后在列表中的每个股票上调用 TryUpdateStockPrice。</span><span class="sxs-lookup"><span data-stu-id="c4502-204">The code checks if another thread is already updating prices, and then it calls TryUpdateStockPrice on each stock in the list.</span></span> <span data-ttu-id="c4502-205">TryUpdateStockPrice 方法决定是否更改股票价格，以及要更改的数量。</span><span class="sxs-lookup"><span data-stu-id="c4502-205">The TryUpdateStockPrice method decides whether to change the stock price, and how much to change it.</span></span> <span data-ttu-id="c4502-206">如果更改了股票价格，则会调用 BroadcastStockPrice 将股票价格更改广播到所有连接的客户端。</span><span class="sxs-lookup"><span data-stu-id="c4502-206">If the stock price is changed, BroadcastStockPrice is called to broadcast the stock price change to all connected clients.</span></span>

    <span data-ttu-id="c4502-207">\_updatingStockPrices 标志标记为[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) ，以确保对其进行 threadsafe 访问。</span><span class="sxs-lookup"><span data-stu-id="c4502-207">The \_updatingStockPrices flag is marked as [volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) to ensure that access to it is threadsafe.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    <span data-ttu-id="c4502-208">在实际应用程序中，TryUpdateStockPrice 方法将调用 web 服务来查找价格;在此代码中，它使用随机数生成器来随机进行更改。</span><span class="sxs-lookup"><span data-stu-id="c4502-208">In a real application, the TryUpdateStockPrice method would call a web service to look up the price; in this code it uses a random number generator to make changes randomly.</span></span>

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a><span data-ttu-id="c4502-209">获取 SignalR 上下文以便 StockTicker 类可以广播到客户端</span><span class="sxs-lookup"><span data-stu-id="c4502-209">Getting the SignalR context so that the StockTicker class can broadcast to clients</span></span>

    <span data-ttu-id="c4502-210">因为价格变化源自 StockTicker 对象，所以这是需要在所有已连接的客户端上调用 updateStockPrice 方法的对象。</span><span class="sxs-lookup"><span data-stu-id="c4502-210">Because the price changes originate here in the StockTicker object, this is the object that needs to call an updateStockPrice method on all connected clients.</span></span> <span data-ttu-id="c4502-211">在中心类中，你有一个用于调用客户端方法的 API，但 StockTicker 不是从 Hub 类派生的，并且没有对任何中心对象的引用。</span><span class="sxs-lookup"><span data-stu-id="c4502-211">In a Hub class you have an API for calling client methods, but StockTicker does not derive from the Hub class and does not have a reference to any Hub object.</span></span> <span data-ttu-id="c4502-212">因此，若要广播到连接的客户端，StockTicker 类必须获取 StockTickerHub 类的 SignalR 上下文实例，并使用该实例对客户端调用方法。</span><span class="sxs-lookup"><span data-stu-id="c4502-212">Therefore, in order to broadcast to connected clients, the StockTicker class has to get the SignalR context instance for the StockTickerHub class and use that to call methods on clients.</span></span>

    <span data-ttu-id="c4502-213">此代码在创建单一实例类实例时获取对 SignalR 上下文的引用，将该引用传递给构造函数，构造函数将该引用传递给客户端属性。</span><span class="sxs-lookup"><span data-stu-id="c4502-213">The code gets a reference to the SignalR context when it creates the singleton class instance, passes that reference to the constructor, and the constructor puts it in the Clients property.</span></span>

    <span data-ttu-id="c4502-214">只想要获取上下文的两个原因是：获取上下文是一种开销高昂的操作，并将其一次确保发送到客户端的预期消息顺序得以保留。</span><span class="sxs-lookup"><span data-stu-id="c4502-214">There are two reasons why you want to get the context just once: getting the context is an expensive operation, and getting it once ensures that the intended order of messages sent to clients is preserved.</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    <span data-ttu-id="c4502-215">获取上下文的客户端属性，并将其放在 StockTickerClient 属性中，可以编写代码来调用与在 Hub 类中看起来相同的客户端方法。</span><span class="sxs-lookup"><span data-stu-id="c4502-215">Getting the Clients property of the context and putting it in the StockTickerClient property lets you write code to call client methods that looks the same as it would in a Hub class.</span></span> <span data-ttu-id="c4502-216">例如，若要广播到所有客户端，你可以编写客户端。所有 updateStockPrice （股票）。</span><span class="sxs-lookup"><span data-stu-id="c4502-216">For instance, to broadcast to all clients you can write Clients.All.updateStockPrice(stock).</span></span>

    <span data-ttu-id="c4502-217">在 BroadcastStockPrice 中调用的 updateStockPrice 方法尚不存在;稍后在编写在客户端上运行的代码时，将添加此代码。</span><span class="sxs-lookup"><span data-stu-id="c4502-217">The updateStockPrice method that you are calling in BroadcastStockPrice doesn't exist yet; you'll add it later when you write code that runs on the client.</span></span> <span data-ttu-id="c4502-218">你可以在此处引用 updateStockPrice，因为客户端是动态的，这意味着将在运行时计算表达式。</span><span class="sxs-lookup"><span data-stu-id="c4502-218">You can refer to updateStockPrice here because Clients.All is dynamic, which means the expression will be evaluated at runtime.</span></span> <span data-ttu-id="c4502-219">此方法调用执行时，SignalR 会将方法名称和参数值发送到客户端，如果客户端具有名为 updateStockPrice 的方法，则将调用该方法，并将参数值传递给该方法。</span><span class="sxs-lookup"><span data-stu-id="c4502-219">When this method call executes, SignalR will send the method name and the parameter value to the client, and if the client has a method named updateStockPrice, that method will be called and the parameter value will be passed to it.</span></span>

    <span data-ttu-id="c4502-220">All 表示发送到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="c4502-220">Clients.All means send to all clients.</span></span> <span data-ttu-id="c4502-221">SignalR 提供其他选项来指定要发送到的客户端或客户端组。</span><span class="sxs-lookup"><span data-stu-id="c4502-221">SignalR gives you other options to specify which clients or groups of clients to send to.</span></span> <span data-ttu-id="c4502-222">有关详细信息，请参阅[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="c4502-222">For more information, see [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).</span></span>

### <a name="register-the-signalr-route"></a><span data-ttu-id="c4502-223">注册 SignalR 路由</span><span class="sxs-lookup"><span data-stu-id="c4502-223">Register the SignalR route</span></span>

<span data-ttu-id="c4502-224">服务器需要知道要截获哪个 URL，并将其定向到 SignalR。</span><span class="sxs-lookup"><span data-stu-id="c4502-224">The server needs to know which URL to intercept and direct to SignalR.</span></span> <span data-ttu-id="c4502-225">要执行此操作，请将一些代码添加到*global.asax*文件。</span><span class="sxs-lookup"><span data-stu-id="c4502-225">To do that you'll add some code to the *Global.asax* file.</span></span>

1. <span data-ttu-id="c4502-226">在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加新项**"。</span><span class="sxs-lookup"><span data-stu-id="c4502-226">In **Solution Explorer**, right-click the project, and then click **Add New Item**.</span></span>
2. <span data-ttu-id="c4502-227">选择 "**全局应用程序类**" 项模板，然后单击 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="c4502-227">Select the **Global Application Class** item template, and then click **Add**.</span></span>

    ![添加 global.asax](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. <span data-ttu-id="c4502-229">将 SignalR 路由注册代码添加到应用程序\_启动方法：</span><span class="sxs-lookup"><span data-stu-id="c4502-229">Add the SignalR route registration code to the Application\_Start method:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    <span data-ttu-id="c4502-230">默认情况下，所有 SignalR 流量的基本 URL 都是 "/signalr"，而 "/signalr/hubs" 用于检索动态生成的 JavaScript 文件，该文件定义应用程序中的所有中心的代理。</span><span class="sxs-lookup"><span data-stu-id="c4502-230">By default, the base URL for all SignalR traffic is "/signalr", and "/signalr/hubs" is used to retrieve a dynamically generated JavaScript file that defines proxies for all the Hubs you have in your application.</span></span> <span data-ttu-id="c4502-231">Routeconfig 方法包括一些重载，可用于在[HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx)类的实例中指定不同的基 URL 和某些 SignalR 选项。</span><span class="sxs-lookup"><span data-stu-id="c4502-231">The MapHubs method includes overloads that let you specify a different base URL and certain SignalR options in an instance of the [HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) class.</span></span>
4. <span data-ttu-id="c4502-232">将 using 语句添加到文件顶部：</span><span class="sxs-lookup"><span data-stu-id="c4502-232">Add a using statement at the top of the file:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. <span data-ttu-id="c4502-233">保存并关闭*global.asax*文件，并生成项目。</span><span class="sxs-lookup"><span data-stu-id="c4502-233">Save and close the *Global.asax* file, and build the project.</span></span>

<span data-ttu-id="c4502-234">你现在已经完成了服务器代码的设置。</span><span class="sxs-lookup"><span data-stu-id="c4502-234">You have now completed setting up the server code.</span></span> <span data-ttu-id="c4502-235">在下一部分中，你将设置客户端。</span><span class="sxs-lookup"><span data-stu-id="c4502-235">In the next section you'll set up the client.</span></span>

<a id="client"></a>

## <a name="set-up-the-client-code"></a><span data-ttu-id="c4502-236">设置客户端代码</span><span class="sxs-lookup"><span data-stu-id="c4502-236">Set up the client code</span></span>

1. <span data-ttu-id="c4502-237">在项目文件夹中创建一个新的 HTML 文件，并将其命名为*StockTicker*。</span><span class="sxs-lookup"><span data-stu-id="c4502-237">Create a new HTML file in the project folder, and name it *StockTicker.html*.</span></span>
2. <span data-ttu-id="c4502-238">将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c4502-238">Replace the template code with the following code:</span></span>

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    <span data-ttu-id="c4502-239">HTML 创建一个表，其中包含5列、标题行和数据行，其中的单个单元格跨所有5列。</span><span class="sxs-lookup"><span data-stu-id="c4502-239">The HTML creates a table with 5 columns, a header row, and a data row with a single cell that spans all 5 columns.</span></span> <span data-ttu-id="c4502-240">数据行显示 "正在加载 ..."仅当应用程序启动时，才会立即显示。</span><span class="sxs-lookup"><span data-stu-id="c4502-240">The data row displays "loading..." and will only be shown momentarily when the application starts.</span></span> <span data-ttu-id="c4502-241">JavaScript 代码将删除该行，并在其位置行中添加从服务器检索到的股票数据。</span><span class="sxs-lookup"><span data-stu-id="c4502-241">JavaScript code will remove that row and add in its place rows with stock data retrieved from the server.</span></span>

    <span data-ttu-id="c4502-242">脚本标记指定 jQuery 脚本文件、SignalR 核心脚本文件、SignalR 代理脚本文件以及稍后将创建的 StockTicker 脚本文件。</span><span class="sxs-lookup"><span data-stu-id="c4502-242">The script tags specify the jQuery script file, the SignalR core script file, the SignalR proxies script file, and a StockTicker script file that you'll create later.</span></span> <span data-ttu-id="c4502-243">SignalR 代理脚本文件（指定 "/signalr/hubs" URL）是动态生成的，它为 Hub 类上的方法定义了代理方法，在本例中为 StockTickerHub. GetAllStocks。</span><span class="sxs-lookup"><span data-stu-id="c4502-243">The SignalR proxies script file, which specifies the "/signalr/hubs" URL, is dynamically generated and defines proxy methods for the methods on the Hub class, in this case for StockTickerHub.GetAllStocks.</span></span> <span data-ttu-id="c4502-244">如果愿意，可以使用[SignalR 实用工具](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手动生成此 JavaScript 文件，并在 routeconfig 方法调用中禁用动态文件创建。</span><span class="sxs-lookup"><span data-stu-id="c4502-244">If you prefer, you can generate this JavaScript file manually by using [SignalR Utilities](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) and disable dynamic file creation in the MapHubs method call.</span></span>
3. > [!IMPORTANT]
   > <span data-ttu-id="c4502-245">请确保*StockTicker*中的 JavaScript 文件引用正确。</span><span class="sxs-lookup"><span data-stu-id="c4502-245">Make sure that the JavaScript file references in *StockTicker.html* are correct.</span></span> <span data-ttu-id="c4502-246">也就是说，请确保脚本标记（本例中为1.8.2）中的 jQuery 版本与项目的 "*脚本*" 文件夹中的 jquery 版本相同，并确保脚本标记中的 SignalR 版本与项目的 "*脚本*" 文件夹中的 SignalR 版本相同。</span><span class="sxs-lookup"><span data-stu-id="c4502-246">That is, make sure that the jQuery version in your script tag (1.8.2 in the example) is the same as the jQuery version in your project's *Scripts* folder, and make sure that the SignalR version in your script tag is the same as the SignalR version in your project's *Scripts* folder.</span></span> <span data-ttu-id="c4502-247">如有必要，请更改脚本标记中的文件名。</span><span class="sxs-lookup"><span data-stu-id="c4502-247">Change the file names in the script tags if necessary.</span></span>
4. <span data-ttu-id="c4502-248">在**解决方案资源管理器**中，右键单击*StockTicker*，然后单击 "**设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="c4502-248">In **Solution Explorer**, right-click *StockTicker.html*, and then click **Set as Start Page**.</span></span>
5. <span data-ttu-id="c4502-249">在项目文件夹中创建一个新的 JavaScript 文件，并将其命名为*StockTicker*。</span><span class="sxs-lookup"><span data-stu-id="c4502-249">Create a new JavaScript file in the project folder and name it *StockTicker.js*..</span></span>
6. <span data-ttu-id="c4502-250">将模板代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="c4502-250">Replace the template code with the following code:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    <span data-ttu-id="c4502-251">$. 连接引用 SignalR 代理。</span><span class="sxs-lookup"><span data-stu-id="c4502-251">$.connection refers to the SignalR proxies.</span></span> <span data-ttu-id="c4502-252">此代码将获取对 StockTickerHub 类的代理的引用，并将其放在 "股票行情" 变量中。</span><span class="sxs-lookup"><span data-stu-id="c4502-252">The code gets a reference to the proxy for the StockTickerHub class and puts it in the ticker variable.</span></span> <span data-ttu-id="c4502-253">代理名称是 [HubName] 属性设置的名称：</span><span class="sxs-lookup"><span data-stu-id="c4502-253">The proxy name is the name that was set by the [HubName] attribute:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    <span data-ttu-id="c4502-254">定义所有变量和函数后，文件中的最后一行代码通过调用 SignalR start 函数初始化 SignalR 连接。</span><span class="sxs-lookup"><span data-stu-id="c4502-254">After all the variables and functions are defined, the last line of code in the file initializes the SignalR connection by calling the SignalR start function.</span></span> <span data-ttu-id="c4502-255">Start 函数以异步方式执行并返回[JQuery 延迟的对象](http://api.jquery.com/category/deferred-object/)，这意味着你可以调用 done 函数来指定要在异步操作完成时调用的函数。</span><span class="sxs-lookup"><span data-stu-id="c4502-255">The start function executes asynchronously and returns a [jQuery Deferred object](http://api.jquery.com/category/deferred-object/), which means you can call the done function to specify the function to call when the asynchronous operation is completed..</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    <span data-ttu-id="c4502-256">Init 函数调用服务器上的 getAllStocks 函数，并使用服务器返回的信息更新股票表。</span><span class="sxs-lookup"><span data-stu-id="c4502-256">The init function calls the getAllStocks function on the server and uses the information that the server returns to update the stock table.</span></span> <span data-ttu-id="c4502-257">请注意，默认情况下，你必须在客户端上使用 camel 大小写格式，但在服务器上，方法名称采用 pascal 大小写形式。</span><span class="sxs-lookup"><span data-stu-id="c4502-257">Notice that by default, you have to use camel casing on the client although the method name is pascal-cased on the server.</span></span> <span data-ttu-id="c4502-258">Camel 大小写规则仅适用于方法，而不适用于对象。</span><span class="sxs-lookup"><span data-stu-id="c4502-258">The camel-casing rule only applies to methods, not objects.</span></span> <span data-ttu-id="c4502-259">例如，你指的是股票。符号和股票。价格，而不是股票价格。</span><span class="sxs-lookup"><span data-stu-id="c4502-259">For example, you refer to stock.Symbol and stock.Price, not stock.symbol or stock.price.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    <span data-ttu-id="c4502-260">如果要在客户端上使用 pascal 大小写，或想要使用完全不同的方法名称，则可以使用 HubMethodName 属性修饰集线器方法，就像使用 HubName 属性修饰集线器类本身一样。</span><span class="sxs-lookup"><span data-stu-id="c4502-260">If you wanted to use pascal casing on the client, or if you wanted to use a completely different method name, you could decorate the Hub method with the HubMethodName attribute the same way you decorated the Hub class itself with the HubName attribute.</span></span>

    <span data-ttu-id="c4502-261">在 init 方法中，为从服务器接收的每个 stock 对象创建用于表行的 HTML，方法是调用 formatStock 来设置 stock 对象的属性的格式，然后通过调用取代（在*StockTicker*顶部定义），将 rowTemplate 变量中的占位符替换为 stock 对象属性值。</span><span class="sxs-lookup"><span data-stu-id="c4502-261">In the init method, HTML for a table row is created for each stock object received from the server by calling formatStock to format properties of the stock object, and then by calling supplant (which is defined at the top of *StockTicker.js*) to replace placeholders in the rowTemplate variable with the stock object property values.</span></span> <span data-ttu-id="c4502-262">然后，将生成的 HTML 追加到 stock 表中。</span><span class="sxs-lookup"><span data-stu-id="c4502-262">The resulting HTML is then appended to the stock table.</span></span>

    <span data-ttu-id="c4502-263">调用 init 的方法是，将其作为在异步启动函数完成后执行的回调函数传入。</span><span class="sxs-lookup"><span data-stu-id="c4502-263">You call init by passing it in as a callback function that executes after the asynchronous start function completes.</span></span> <span data-ttu-id="c4502-264">如果在调用 start 后将 init 称为单独的 JavaScript 语句，该函数将失败，因为它会立即执行，而不会等待启动函数完成建立连接。</span><span class="sxs-lookup"><span data-stu-id="c4502-264">If you called init as a separate JavaScript statement after calling start, the function would fail because it would execute immediately without waiting for the start function to finish establishing the connection.</span></span> <span data-ttu-id="c4502-265">在这种情况下，init 函数将尝试在建立服务器连接之前调用 getAllStocks 函数。</span><span class="sxs-lookup"><span data-stu-id="c4502-265">In that case, the init function would try to call the getAllStocks function before the server connection is established.</span></span>

    <span data-ttu-id="c4502-266">当服务器更改股票价格时，它将在连接的客户端上调用 updateStockPrice。</span><span class="sxs-lookup"><span data-stu-id="c4502-266">When the server changes a stock's price, it calls the updateStockPrice on connected clients.</span></span> <span data-ttu-id="c4502-267">该函数将添加到 stockTicker 代理的客户端属性，以使其可用于来自服务器的调用。</span><span class="sxs-lookup"><span data-stu-id="c4502-267">The function is added to the client property of the stockTicker proxy in order to make it available to calls from the server.</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    <span data-ttu-id="c4502-268">UpdateStockPrice 函数将从服务器接收的常用对象的格式设置为与 init 函数中相同的方式。</span><span class="sxs-lookup"><span data-stu-id="c4502-268">The updateStockPrice function formats a stock object received from the server into a table row the same way as in the init function.</span></span> <span data-ttu-id="c4502-269">但是，它不会将行追加到表中，而是在表中查找库存的当前行，并将该行替换为新行。</span><span class="sxs-lookup"><span data-stu-id="c4502-269">However, instead of appending the row to the table, it finds the stock's current row in the table and replaces that row with the new one.</span></span>

<a id="test"></a>

## <a name="test-the-application"></a><span data-ttu-id="c4502-270">测试应用程序</span><span class="sxs-lookup"><span data-stu-id="c4502-270">Test the application</span></span>

1. <span data-ttu-id="c4502-271">按 F5 以调试模式运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4502-271">Press F5 to run the application in debug mode.</span></span>

    <span data-ttu-id="c4502-272">Stock 表最初显示 "正在加载 ..."行，然后在短暂延迟后显示初始股票数据，然后股票价格开始更改。</span><span class="sxs-lookup"><span data-stu-id="c4502-272">The stock table initially displays the "loading..." line, then after a short delay the initial stock data is displayed, and then the stock prices start to change.</span></span>

    ![“加载”](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![初始股票表](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![从服务器接收更改的股票表](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. <span data-ttu-id="c4502-276">复制浏览器地址栏中的 URL，并将其粘贴到一个或多个新的浏览器窗口中。</span><span class="sxs-lookup"><span data-stu-id="c4502-276">Copy the URL from the browser address bar and paste it into one or more new browser window(s).</span></span>

    <span data-ttu-id="c4502-277">初始股票显示器与第一个浏览器相同，同时发生更改。</span><span class="sxs-lookup"><span data-stu-id="c4502-277">The initial stock display is the same as the first browser and changes happen simultaneously.</span></span>
3. <span data-ttu-id="c4502-278">关闭所有浏览器并打开一个新浏览器，然后切换到相同的 URL。</span><span class="sxs-lookup"><span data-stu-id="c4502-278">Close all browsers and open a new browser, then go to the same URL.</span></span>

    <span data-ttu-id="c4502-279">StockTicker singleton 对象已继续在服务器中运行，因此，stock 表显示的是股票持续变化。</span><span class="sxs-lookup"><span data-stu-id="c4502-279">The StockTicker singleton object has continued to run in the server, so the stock table display shows that the stocks have continued to change.</span></span> <span data-ttu-id="c4502-280">（看不到具有零更改图的初始表。）</span><span class="sxs-lookup"><span data-stu-id="c4502-280">(You don't see the initial table with zero change figures.)</span></span>
4. <span data-ttu-id="c4502-281">关闭浏览器。</span><span class="sxs-lookup"><span data-stu-id="c4502-281">Close the browser.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="c4502-282">启用日志记录</span><span class="sxs-lookup"><span data-stu-id="c4502-282">Enable logging</span></span>

<span data-ttu-id="c4502-283">SignalR 具有内置日志记录功能，可以在客户端上启用该功能以帮助进行故障排除。</span><span class="sxs-lookup"><span data-stu-id="c4502-283">SignalR has a built-in logging function that you can enable on the client to aid in troubleshooting.</span></span> <span data-ttu-id="c4502-284">在本部分中，你将启用日志记录，并查看示例，这些示例演示了日志如何告诉你以下哪种传输方法 SignalR 正在使用：</span><span class="sxs-lookup"><span data-stu-id="c4502-284">In this section you enable logging and see examples that show how logs tell you which of the following transport methods SignalR is using:</span></span>

- <span data-ttu-id="c4502-285">[Websocket](http://en.wikipedia.org/wiki/WebSocket)，受 IIS 8 和当前浏览器支持。</span><span class="sxs-lookup"><span data-stu-id="c4502-285">[WebSockets](http://en.wikipedia.org/wiki/WebSocket), supported by IIS 8 and current browsers.</span></span>
- <span data-ttu-id="c4502-286">Internet Explorer 之外的浏览器所支持的[服务器发送事件](http://en.wikipedia.org/wiki/Server-sent_events)。</span><span class="sxs-lookup"><span data-stu-id="c4502-286">[Server-sent events](http://en.wikipedia.org/wiki/Server-sent_events), supported by browsers other than Internet Explorer.</span></span>
- <span data-ttu-id="c4502-287">Internet Explorer 支持的[永久帧](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。</span><span class="sxs-lookup"><span data-stu-id="c4502-287">[Forever frame](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe), supported by Internet Explorer.</span></span>
- <span data-ttu-id="c4502-288">所有浏览器都支持[Ajax 长轮询](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)。</span><span class="sxs-lookup"><span data-stu-id="c4502-288">[Ajax long polling](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling), supported by all browsers.</span></span>

<span data-ttu-id="c4502-289">对于任何给定的连接，SignalR 将选择服务器和客户端都支持的最佳传输方法。</span><span class="sxs-lookup"><span data-stu-id="c4502-289">For any given connection, SignalR chooses the best transport method that both the server and the client support.</span></span>

1. <span data-ttu-id="c4502-290">打开*StockTicker* ，并添加一行代码，以便在文件末尾初始化连接的代码之前立即启用日志记录：</span><span class="sxs-lookup"><span data-stu-id="c4502-290">Open *StockTicker.js* and add a line of code to enable logging immediately before the code that initializes the connection at the end of the file:</span></span>

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. <span data-ttu-id="c4502-291">按 F5 运行该项目。</span><span class="sxs-lookup"><span data-stu-id="c4502-291">Press F5 to run the project.</span></span>
3. <span data-ttu-id="c4502-292">打开浏览器的 "开发人员工具" 窗口，并选择控制台查看日志。</span><span class="sxs-lookup"><span data-stu-id="c4502-292">Open your browser's developer tools window, and select the Console to see the logs.</span></span> <span data-ttu-id="c4502-293">您可能必须刷新该页才能查看为新连接协商传输方法的 Signalr 的日志。</span><span class="sxs-lookup"><span data-stu-id="c4502-293">You might have to refresh the page to see the logs of Signalr negotiating the transport method for a new connection.</span></span>

    <span data-ttu-id="c4502-294">如果在 Windows 8 （IIS 8）上运行 Internet Explorer 10，则传输方法为 Websocket。</span><span class="sxs-lookup"><span data-stu-id="c4502-294">If you are running Internet Explorer 10 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![IE 10 IIS 8 控制台](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    <span data-ttu-id="c4502-296">如果在 Windows 7 上运行 Internet Explorer 10 （IIS 7.5），则传输方法为 iframe。</span><span class="sxs-lookup"><span data-stu-id="c4502-296">If you are running Internet Explorer 10 on Windows 7 (IIS 7.5), the transport method is iframe.</span></span>

    ![IE 10 控制台、IIS 7。5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    <span data-ttu-id="c4502-298">在 Firefox 中，安装 Firebug 外接程序以获取控制台窗口。</span><span class="sxs-lookup"><span data-stu-id="c4502-298">In Firefox, install the Firebug add-in to get a Console window.</span></span> <span data-ttu-id="c4502-299">如果在 Windows 8 （IIS 8）上运行 Firefox 19，则传输方法为 Websocket。</span><span class="sxs-lookup"><span data-stu-id="c4502-299">If you are running Firefox 19 on Windows 8 (IIS 8), the transport method is WebSockets.</span></span>

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    <span data-ttu-id="c4502-301">如果在 Windows 7 上运行 Firefox 19 （IIS 7.5），则传输方法为服务器发送事件。</span><span class="sxs-lookup"><span data-stu-id="c4502-301">If you are running Firefox 19 on Windows 7 (IIS 7.5), the transport method is server-sent events.</span></span>

    ![Firefox 19 IIS 7.5 控制台](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a><span data-ttu-id="c4502-303">安装和查看完整的 StockTicker 示例</span><span class="sxs-lookup"><span data-stu-id="c4502-303">Install and review the full StockTicker sample</span></span>

<span data-ttu-id="c4502-304">[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 包安装的 StockTicker 应用程序的功能比你刚从头创建的简化版本包含的功能更多。</span><span class="sxs-lookup"><span data-stu-id="c4502-304">The StockTicker application that is installed by the [Microsoft.AspNet.SignalR.Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet package includes more features than the simplified version that you just created from scratch.</span></span> <span data-ttu-id="c4502-305">在本教程的此部分中，你将安装 NuGet 包并查看实现这些功能的新功能和代码。</span><span class="sxs-lookup"><span data-stu-id="c4502-305">In this section of the tutorial, you install the NuGet package and review the new features and the code that implements them.</span></span>

### <a name="install-the-signalrsample-nuget-package"></a><span data-ttu-id="c4502-306">安装 SignalR NuGet 包</span><span class="sxs-lookup"><span data-stu-id="c4502-306">Install the SignalR.Sample NuGet package</span></span>

1. <span data-ttu-id="c4502-307">在**解决方案资源管理器**中，右键单击该项目，然后单击 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="c4502-307">In **Solution Explorer**, right-click the project and click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="c4502-308">在 "**管理 NuGet 包**" 对话框中，单击 "**联机**"，在 "**联机搜索**" 框中输入*SignalR* ，然后单击**SignalR**包中的 "**安装**"。</span><span class="sxs-lookup"><span data-stu-id="c4502-308">In the **Manage NuGet Packages** dialog box, click **Online**, enter *SignalR.Sample* in the **Search Online** box, and then click **Install** in the **SignalR.Sample** package.</span></span>

    ![安装 SignalR 包](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. <span data-ttu-id="c4502-310">在*global.asax*文件中，注释掉 RouteTable routeconfig （）;你之前在应用程序\_Start 方法中添加的行。</span><span class="sxs-lookup"><span data-stu-id="c4502-310">In the *Global.asax* file, comment out the RouteTable.Routes.MapHubs(); line that you added earlier in the Application\_Start method.</span></span>

    <span data-ttu-id="c4502-311">不再需要*global.asax*中的代码，因为 SignalR 包在*应用\_Start/RegisterHubs*文件中注册 SignalR 路由：</span><span class="sxs-lookup"><span data-stu-id="c4502-311">The code in *Global.asax* is no longer needed because the SignalR.Sample package registers the SignalR route in the *App\_Start/RegisterHubs.cs* file:</span></span>

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    <span data-ttu-id="c4502-312">WebActivatorEx NuGet 包中包含由程序集特性引用的 WebActivator 类，它作为 SignalR 包的依赖项安装。</span><span class="sxs-lookup"><span data-stu-id="c4502-312">The WebActivator class that is referenced by the assembly attribute is included in the WebActivatorEx NuGet package, which is installed as a dependency of the SignalR.Sample package.</span></span>
4. <span data-ttu-id="c4502-313">在**解决方案资源管理器**中，展开通过安装 SignalR 包创建的*SignalR*文件夹。</span><span class="sxs-lookup"><span data-stu-id="c4502-313">In **Solution Explorer**, expand the *SignalR.Sample* folder which was created by installing the SignalR.Sample package.</span></span>
5. <span data-ttu-id="c4502-314">在*SignalR*文件夹中，右键单击 " *StockTicker*"，然后单击 "**设为起始页**"。</span><span class="sxs-lookup"><span data-stu-id="c4502-314">In the *SignalR.Sample* folder, right-click *StockTicker.html*, and then click **Set As Start Page**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c4502-315">安装 SignalR NuGet 包可能会更改你在*脚本*文件夹中拥有的 jQuery 版本。</span><span class="sxs-lookup"><span data-stu-id="c4502-315">Installing The SignalR.Sample NuGet package might change the version of jQuery that you have in your *Scripts* folder.</span></span> <span data-ttu-id="c4502-316">包安装在*SignalR*文件夹中的新的*StockTicker*文件将与包所安装的 jQuery 版本同步，但是，如果你想要再次运行原始*StockTicker*文件，则可能需要先更新 script 标记中的 jQuery 引用。</span><span class="sxs-lookup"><span data-stu-id="c4502-316">The new *StockTicker.html* file that the package installs in the *SignalR.Sample* folder will be in sync with the jQuery version that the package installs, but if you want to run your original *StockTicker.html* file again, you might have to update the jQuery reference in the script tag first.</span></span>

### <a name="run-the-application"></a><span data-ttu-id="c4502-317">运行此应用程序</span><span class="sxs-lookup"><span data-stu-id="c4502-317">Run the application</span></span>

1. <span data-ttu-id="c4502-318">按 F5 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4502-318">Press F5 to run the application.</span></span>

    <span data-ttu-id="c4502-319">除了前面看到的网格外，整个股票行情滚动应用程序还会显示一个水平滚动窗口，其中显示相同的股票数据。</span><span class="sxs-lookup"><span data-stu-id="c4502-319">In addition to the grid that you saw earlier, the full stock ticker application shows a horizontally scrolling window that displays the same stock data.</span></span> <span data-ttu-id="c4502-320">首次运行应用程序时，"市场" 将为 "已关闭"，同时会显示静态网格和不滚动的滚动条窗口。</span><span class="sxs-lookup"><span data-stu-id="c4502-320">When you run the application for the first time, the "market" is "closed" and you see a static grid and a ticker window that isn't scrolling.</span></span>

    ![StockTicker 屏幕启动](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    <span data-ttu-id="c4502-322">单击 "**公开市场**" 时，"**实时股票行情**" 框将开始水平滚动，服务器将开始随机广播股票价格变化。</span><span class="sxs-lookup"><span data-stu-id="c4502-322">When you click **Open Market**, the **Live Stock Ticker** box starts to scroll horizontally, and the server starts to periodically broadcast stock price changes on a random basis.</span></span> <span data-ttu-id="c4502-323">每次股票价格变化时，都会更新 "**实时库存表**" 网格和 "**实时股票行情**" 框。</span><span class="sxs-lookup"><span data-stu-id="c4502-323">Each time a stock price changes, both the **Live Stock Table** grid and the **Live Stock Ticker** box are updated.</span></span> <span data-ttu-id="c4502-324">当股票价格变化为正时，股票显示为绿色背景，当更改为负值时，会显示红色背景。</span><span class="sxs-lookup"><span data-stu-id="c4502-324">When a stock's price change is positive, the stock is shown with a green background, and when the change is negative, the stock is shown with a red background.</span></span>

    ![StockTicker 应用，市场开放式](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    <span data-ttu-id="c4502-326">"**关闭市场**" 按钮将停止更改并停止滚动更新，并在价格变化开始之前将所有股票数据**重置为**初始状态。</span><span class="sxs-lookup"><span data-stu-id="c4502-326">The **Close Market** button stops the changes and stops the ticker scrolling, and the **Reset** button resets all stock data to the initial state before price changes started.</span></span> <span data-ttu-id="c4502-327">如果打开更多浏览器窗口并访问相同的 URL，则会在每个浏览器中同时动态更新相同的数据。</span><span class="sxs-lookup"><span data-stu-id="c4502-327">If you open more browser windows and go to the same URL, you see the same data dynamically updated at the same time in each browser.</span></span> <span data-ttu-id="c4502-328">单击其中一个按钮时，所有浏览器将同时以相同的方式进行响应。</span><span class="sxs-lookup"><span data-stu-id="c4502-328">When you click one of the buttons, all browsers respond the same way at the same time.</span></span>

### <a name="live-stock-ticker-display"></a><span data-ttu-id="c4502-329">直播股票行情显示</span><span class="sxs-lookup"><span data-stu-id="c4502-329">Live Stock Ticker display</span></span>

<span data-ttu-id="c4502-330">**Live 股票行情**显示在 div 元素中的一个无序列表，该列表通过 CSS 样式格式化为单个行。</span><span class="sxs-lookup"><span data-stu-id="c4502-330">The **Live Stock Ticker** display is an unordered list in a div element that is formatted into a single line by CSS styles.</span></span> <span data-ttu-id="c4502-331">该代号的初始化和更新方式与表的更新方式相同：在 &lt;li&gt; 模板字符串中替换占位符，并将 &lt;li&gt; 元素动态添加到 &lt;ul&gt; 元素。</span><span class="sxs-lookup"><span data-stu-id="c4502-331">The ticker is initialized and updated the same way as the table: by replacing placeholders in a &lt;li&gt; template string and dynamically adding the &lt;li&gt; elements to the &lt;ul&gt; element.</span></span> <span data-ttu-id="c4502-332">使用 jQuery 动画函数执行滚动，以改变 div 中无序列表的左边距。</span><span class="sxs-lookup"><span data-stu-id="c4502-332">The scrolling is performed by using the jQuery animate function to vary the margin-left of the unordered list within the div.</span></span>

<span data-ttu-id="c4502-333">股票行情的 HTML：</span><span class="sxs-lookup"><span data-stu-id="c4502-333">The stock ticker HTML:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

<span data-ttu-id="c4502-334">股票行情，CSS：</span><span class="sxs-lookup"><span data-stu-id="c4502-334">The stock ticker CSS:</span></span>

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

<span data-ttu-id="c4502-335">使其滚动的 jQuery 代码：</span><span class="sxs-lookup"><span data-stu-id="c4502-335">The jQuery code that makes it scroll:</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a><span data-ttu-id="c4502-336">客户端可以调用的服务器上的其他方法</span><span class="sxs-lookup"><span data-stu-id="c4502-336">Additional methods on the server that the client can call</span></span>

<span data-ttu-id="c4502-337">StockTickerHub 类定义了客户端可以调用的四种附加方法：</span><span class="sxs-lookup"><span data-stu-id="c4502-337">The StockTickerHub class defines four additional methods that the client can call:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

<span data-ttu-id="c4502-338">将调用 OpenMarket、CloseMarket 和 Reset 来响应页面顶部的按钮。</span><span class="sxs-lookup"><span data-stu-id="c4502-338">OpenMarket, CloseMarket, and Reset are called in response to the buttons at the top of the page.</span></span> <span data-ttu-id="c4502-339">它们演示了触发状态更改的一种客户端模式，这些更改会立即传播到所有客户端。</span><span class="sxs-lookup"><span data-stu-id="c4502-339">They demonstrate the pattern of one client triggering a change in state that is immediately propagated to all clients.</span></span> <span data-ttu-id="c4502-340">其中每个方法都调用 StockTicker 类中的一个方法，该方法影响市场状态更改，然后广播新状态。</span><span class="sxs-lookup"><span data-stu-id="c4502-340">Each of these methods calls a method in the StockTicker class that effects the market state change and then broadcasts the new state.</span></span>

<span data-ttu-id="c4502-341">在 StockTicker 类中，市场的状态由返回 MarketState 枚举值的 MarketState 属性来维护：</span><span class="sxs-lookup"><span data-stu-id="c4502-341">In the StockTicker class, the state of the market is maintained by a MarketState property that returns a MarketState enum value:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

<span data-ttu-id="c4502-342">更改市场状态的每个方法都在锁定块中执行此操作，因为 StockTicker 类必须 threadsafe：</span><span class="sxs-lookup"><span data-stu-id="c4502-342">Each of the methods that change the market state do so inside a lock block because the StockTicker class has to be threadsafe:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

<span data-ttu-id="c4502-343">为了确保此代码是 threadsafe 的，支持 MarketState 属性的 \_marketState 字段被标记为 volatile，</span><span class="sxs-lookup"><span data-stu-id="c4502-343">To ensure that this code is threadsafe, the \_marketState field that backs the MarketState property is marked as volatile,</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

<span data-ttu-id="c4502-344">BroadcastMarketStateChange 和 BroadcastMarketReset 方法类似于你已看到的 BroadcastStockPrice 方法，只不过它们调用在客户端定义的不同方法：</span><span class="sxs-lookup"><span data-stu-id="c4502-344">The BroadcastMarketStateChange and BroadcastMarketReset methods are similar to the BroadcastStockPrice method that you already saw, except they call different methods defined at the client:</span></span>

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a><span data-ttu-id="c4502-345">服务器可以调用的客户端上的其他函数</span><span class="sxs-lookup"><span data-stu-id="c4502-345">Additional functions on the client that the server can call</span></span>

<span data-ttu-id="c4502-346">UpdateStockPrice 函数现在同时处理网格和滚动条的显示，并使用 jQuery。彩色闪烁红色和绿色颜色。</span><span class="sxs-lookup"><span data-stu-id="c4502-346">The updateStockPrice function now handles both the grid and the ticker display, and it uses jQuery.Color to flash red and green colors.</span></span>

<span data-ttu-id="c4502-347">*SignalR*中的新函数基于市场状态启用和禁用按钮，并停止或启动 "滚动条" 窗口水平滚动。</span><span class="sxs-lookup"><span data-stu-id="c4502-347">New functions in *SignalR.StockTicker.js* enable and disable the buttons based on market state, and they stop or start the ticker window horizontal scrolling.</span></span> <span data-ttu-id="c4502-348">由于将多个函数添加到了股市代号，因此使用[jQuery extend 函数](http://api.jquery.com/jQuery.extend/)添加它们。</span><span class="sxs-lookup"><span data-stu-id="c4502-348">Since multiple functions are being added to ticker.client, the [jQuery extend function](http://api.jquery.com/jQuery.extend/) is used to add them.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a><span data-ttu-id="c4502-349">建立连接后的其他客户端设置</span><span class="sxs-lookup"><span data-stu-id="c4502-349">Additional client setup after establishing the connection</span></span>

<span data-ttu-id="c4502-350">客户端建立连接后，还需要执行一些额外的工作：查找市场是否已打开或关闭，以调用适当的 marketOpened 或 marketClosed 函数，并将服务器方法调用附加到这些按钮。</span><span class="sxs-lookup"><span data-stu-id="c4502-350">After the client establishes the connection, it has some additional work to do: find out if the market is open or closed in order to call the appropriate marketOpened or marketClosed function, and attach the server method calls to the buttons.</span></span>

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

<span data-ttu-id="c4502-351">在建立连接之前，服务器方法不会连接到按钮，这样代码就不能尝试在可用之前调用服务器方法。</span><span class="sxs-lookup"><span data-stu-id="c4502-351">The server methods are not wired up to the buttons until after the connection is established, so that the code can't try to call the server methods before they are available.</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="c4502-352">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c4502-352">Next steps</span></span>

<span data-ttu-id="c4502-353">在本教程中，你已了解如何对 SignalR 应用程序进行编程，以将消息从服务器广播到所有连接的客户端，这两个客户端均定期和响应来自任何客户端的通知。</span><span class="sxs-lookup"><span data-stu-id="c4502-353">In this tutorial you've learned how to program a SignalR application that broadcasts messages from the server to all connected clients, both on a periodic basis and in response to notifications from any client.</span></span> <span data-ttu-id="c4502-354">使用多线程单独实例来维护服务器状态的模式也可以用于多玩家在线游戏方案。</span><span class="sxs-lookup"><span data-stu-id="c4502-354">The pattern of using a multi-threaded singleton instance to maintain server state can also be also used in multi-player online game scenarios.</span></span> <span data-ttu-id="c4502-355">有关示例，请参阅[基于 SignalR 的 ShootR 游戏](https://github.com/NTaylorMullen/ShootR)。</span><span class="sxs-lookup"><span data-stu-id="c4502-355">For an example, see [the ShootR game that is based on SignalR](https://github.com/NTaylorMullen/ShootR).</span></span>

<span data-ttu-id="c4502-356">有关显示对等通信方案的教程，入门请参阅[SignalR With](index.md) And[实时更新 with SignalR](index.md)。</span><span class="sxs-lookup"><span data-stu-id="c4502-356">For tutorials that show peer-to-peer communication scenarios, see [Getting Started with SignalR](index.md) and [Real-Time Updating with SignalR](index.md).</span></span>

<span data-ttu-id="c4502-357">若要了解更高级的 SignalR 开发概念，请访问以下站点以获取 SignalR 源代码和资源：</span><span class="sxs-lookup"><span data-stu-id="c4502-357">To learn more advanced SignalR development concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="c4502-358">ASP.NET SignalR</span><span class="sxs-lookup"><span data-stu-id="c4502-358">ASP.NET SignalR</span></span>](https://asp.net/signalr/)
- [<span data-ttu-id="c4502-359">SignalR 项目</span><span class="sxs-lookup"><span data-stu-id="c4502-359">SignalR Project</span></span>](http://signalr.net/)
- [<span data-ttu-id="c4502-360">SignalR Github 和示例</span><span class="sxs-lookup"><span data-stu-id="c4502-360">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="c4502-361">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="c4502-361">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
