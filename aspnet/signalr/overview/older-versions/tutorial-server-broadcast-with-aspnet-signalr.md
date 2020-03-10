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
# <a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a>教程：通过 ASP.NET SignalR 1.x 进行服务器广播

作者： [Fletcher](https://github.com/pfletcher)， [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本教程介绍如何创建使用 ASP.NET SignalR 提供服务器广播功能的 web 应用程序。 服务器广播表示发送到客户端的通信由服务器启动。 此方案需要不同于对等方案的编程方法，例如聊天应用程序，其中发送到客户端的通信由一个或多个客户端启动。
> 
> 你将在本教程中创建的应用程序模拟股票行情，这是服务器广播功能的典型方案。
> 
> 欢迎使用教程中的注释。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com)。

## <a name="overview"></a>概述

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 包在 Visual Studio 项目中安装一个模拟股票行情滚动应用程序示例。 在本教程的第一部分中，你将从头开始创建该应用程序的简化版本。 在本教程的其余部分中，你将安装 NuGet 包并查看它创建的其他功能和代码。

股票行情应用程序是一种实时应用程序的代表，你希望在其中定期 "推送" 或 "广播" 从服务器到所有连接的客户端的通知。

您将在本教程的第一部分中生成的应用程序将显示一个包含股票数据的网格。

![StockTicker 初始版本](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

服务器会定期随机更新股票价格，并将更新推送到所有连接的客户端。 在浏览器中，**更改**和 **%** 列中的数字和符号会动态更改以响应来自服务器的通知。 如果你打开相同 URL 的其他浏览器，则它们都同时显示相同的数据和相同的数据更改。

本教程包含以下部分：

- [先决条件](#prerequisites)
- [创建项目](#createproject)
- [添加 SignalR NuGet 包](#nugetpackages)
- [设置服务器代码](#server)
- [设置客户端代码](#client)
- [测试应用程序](#test)
- [启用日志记录](#enablelogging)
- [安装和查看完整的 StockTicker 示例](#fullsample)
- [后续步骤](#nextsteps)

> [!NOTE]
> 如果不想完成生成应用程序的步骤，可以在新的**空 ASP.NET Web 应用程序**项目中安装 SignalR 包，然后通读这些步骤以获取代码的说明。 本教程的第一部分介绍 SignalR 代码的一个子集，第二部分说明 SignalR 包中附加功能的主要功能。

<a id="prerequisites"></a>

## <a name="prerequisites"></a>系统必备

在开始之前，请确保已在计算机上安装 Visual Studio 2012 或 2010 SP1。 如果没有 Visual Studio，请参阅[ASP.NET 下载](https://www.asp.net/downloads)以获取免费的 visual Studio 2012 Express for Web。

如果安装了 Visual Studio 2010，请确保已安装[NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 。

<a id="createproject"></a>

## <a name="create-the-project"></a>创建项目

1. 从“文件”菜单上，单击“新建项目”。
2. 在 "**新建项目**" 对话框中， **C#** 展开 "**模板**"，然后选择 " **Web**"。
3. 选择**ASP.NET 空 Web 应用程序**模板，将项目命名为*SignalR StockTicker*，然后单击 **"确定"** 。

    ![“新建项目”对话框](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a>添加 SignalR NuGet 包

### <a name="add-the-signalr-and-jquery-nuget-packages"></a>添加 SignalR 和 JQuery NuGet 包

可以通过安装 NuGet 包将 SignalR 功能添加到项目。

1. 单击 "**工具" |NuGet 包管理器 |程序包管理器控制台**。
2. 在 "包管理器" 中输入以下命令。

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    SignalR 包会安装多个其他 NuGet 包作为依赖项。 安装完成后，你将拥有在 ASP.NET 应用程序中使用 SignalR 所需的所有服务器和客户端组件。

<a id="server"></a>

## <a name="set-up-the-server-code"></a>设置服务器代码

在本部分中，您将设置在服务器上运行的代码。

### <a name="create-the-stock-class"></a>创建 Stock 类

首先，创建用于存储和传输股票信息的 Stock 模型类。

1. 在项目文件夹中创建一个新的类文件，将其命名为*Stock.cs*，然后将模板代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    创建股票时要设置的两个属性是符号（例如，MSFT for Microsoft）和价格。 其他属性取决于设置价格的方式和时间。 首次设置价格时，该值将传播到 DayOpen。 后续设置价格时，会根据价格和 DayOpen 之间的差异来计算 Change 和 PercentChange 属性值。

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a>创建 StockTicker 和 StockTickerHub 类

你将使用 SignalR 中心 API 来处理服务器到客户端的交互。 派生自 SignalR Hub 类的 StockTickerHub 类将处理从客户端接收连接和方法调用。 还需要维护股票数据并运行计时器对象，以定期触发价格更新，独立于客户端连接。 由于中心实例是暂时性的，因此不能将这些函数放在 Hub 类中。 集线器类实例是为集线器上的每个操作创建的，例如连接和从客户端到服务器的调用。 因此，用于保留股票数据、更新价格和广播价格更新的机制必须在单独的类中运行，你可以将其命名为 StockTicker。

![从 StockTicker 广播](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

你只希望在服务器上运行 StockTicker 类的一个实例，因此你将需要设置从每个 StockTickerHub 实例到 singleton StockTicker 实例的引用。 StockTicker 类必须能够广播到客户端，因为它具有股票数据并触发更新，但 StockTicker 不是中心类。 因此，StockTicker 类必须获取对 SignalR 中心连接上下文对象的引用。 然后，它可以使用 SignalR 连接上下文对象广播到客户端。

1. 在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加新项**"。
2. 如果安装了带有[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=279941)的 visual Studio 2012，请单击 "**视觉C#对象**" 下的 " **Web** "，然后选择 " **SignalR" 中心类**项模板。 否则，请选择 "**类**" 模板。
3. 将新类命名为*StockTickerHub.cs*，然后单击 "**添加**"。

    ![添加 StockTickerHub.cs](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. 将模板代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)类用于定义客户端可以在服务器上调用的方法。 您正在定义一个方法： `GetAllStocks()`。 当客户端最初连接到服务器时，它将调用此方法以获取所有股票的列表及其当前价格。 方法可以同步执行并返回 `IEnumerable<Stock>`，因为该方法从内存返回数据。 如果该方法必须通过执行需要等待的内容（如数据库查找或 web 服务调用）来获取数据，则应将 `Task<IEnumerable<Stock>>` 指定为返回值以启用异步处理。 有关详细信息，请参阅[ASP.NET SignalR HUB API 指南-Server-When to 异步执行的时间](index.md)。

    HubName 属性指定如何在客户端上的 JavaScript 代码中引用中心。 如果不使用此属性，则客户端上的默认名称是类名的大小写形式，在本例中为 stockTickerHub。

    稍后在创建 StockTicker 类时，将在其静态实例属性中创建该类的单一实例。 无论客户端连接或断开连接的客户端有多少个客户端，StockTicker 的单一实例都将保留在内存中，并且该实例是 GetAllStocks 方法用来返回当前股票信息的内容。
5. 在项目文件夹中创建一个新的类文件，将其命名为*StockTicker.cs*，然后将模板代码替换为以下代码：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    由于多个线程将运行 StockTicker 代码的同一个实例，因此 StockTicker 类必须是 threadsafe。

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a>将单一实例存储在静态字段中

    此代码初始化静态 \_实例字段，该字段将支持实例属性和类的实例，这是可以创建的类的唯一实例，因为构造函数被标记为私有。 [迟缓初始化](https://msdn.microsoft.com/library/dd997286.aspx)用于 \_实例字段，而不是出于性能原因，但要确保实例创建 threadsafe。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    每次客户端连接到服务器时，在单独的线程中运行的 StockTickerHub 类的新实例将从 StockTicker 静态属性获取 StockTicker 单一实例，如前面在 StockTickerHub 类中看到的那样。

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a>在 ConcurrentDictionary 中存储股票数据

    构造函数用一些示例股票数据初始化 \_股票集合，GetAllStocks 返回股票。 正如你之前所见，StockTickerHub 的这一组股票又由 GetAllStocks 返回，后者是客户端可调用的中心类中的服务器方法。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    股票集合定义为线程安全的[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)类型。 作为替代方法，可以使用[字典](https://msdn.microsoft.com/library/xfhwa508.aspx)对象，并在对字典进行更改时显式锁定字典。

    在此示例应用程序中，可以将应用程序数据存储在内存中，并在 StockTicker 实例被释放时丢失数据。 在实际应用程序中，你将使用后端数据存储（如数据库）。

    ### <a name="periodically-updating-stock-prices"></a>定期更新股票价格

    构造函数将启动一个 Timer 对象，该对象定期调用可随机更新股票价格的方法。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    UpdateStockPrices 由计时器调用，它在 state 参数中传递 null。 更新价格之前，会对 \_updateStockPricesLock 对象进行锁定。 该代码将检查是否有另一个线程正在更新价格，然后在列表中的每个股票上调用 TryUpdateStockPrice。 TryUpdateStockPrice 方法决定是否更改股票价格，以及要更改的数量。 如果更改了股票价格，则会调用 BroadcastStockPrice 将股票价格更改广播到所有连接的客户端。

    \_updatingStockPrices 标志标记为[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) ，以确保对其进行 threadsafe 访问。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    在实际应用程序中，TryUpdateStockPrice 方法将调用 web 服务来查找价格;在此代码中，它使用随机数生成器来随机进行更改。

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>获取 SignalR 上下文以便 StockTicker 类可以广播到客户端

    因为价格变化源自 StockTicker 对象，所以这是需要在所有已连接的客户端上调用 updateStockPrice 方法的对象。 在中心类中，你有一个用于调用客户端方法的 API，但 StockTicker 不是从 Hub 类派生的，并且没有对任何中心对象的引用。 因此，若要广播到连接的客户端，StockTicker 类必须获取 StockTickerHub 类的 SignalR 上下文实例，并使用该实例对客户端调用方法。

    此代码在创建单一实例类实例时获取对 SignalR 上下文的引用，将该引用传递给构造函数，构造函数将该引用传递给客户端属性。

    只想要获取上下文的两个原因是：获取上下文是一种开销高昂的操作，并将其一次确保发送到客户端的预期消息顺序得以保留。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    获取上下文的客户端属性，并将其放在 StockTickerClient 属性中，可以编写代码来调用与在 Hub 类中看起来相同的客户端方法。 例如，若要广播到所有客户端，你可以编写客户端。所有 updateStockPrice （股票）。

    在 BroadcastStockPrice 中调用的 updateStockPrice 方法尚不存在;稍后在编写在客户端上运行的代码时，将添加此代码。 你可以在此处引用 updateStockPrice，因为客户端是动态的，这意味着将在运行时计算表达式。 此方法调用执行时，SignalR 会将方法名称和参数值发送到客户端，如果客户端具有名为 updateStockPrice 的方法，则将调用该方法，并将参数值传递给该方法。

    All 表示发送到所有客户端。 SignalR 提供其他选项来指定要发送到的客户端或客户端组。 有关详细信息，请参阅[HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。

### <a name="register-the-signalr-route"></a>注册 SignalR 路由

服务器需要知道要截获哪个 URL，并将其定向到 SignalR。 要执行此操作，请将一些代码添加到*global.asax*文件。

1. 在**解决方案资源管理器**中，右键单击项目，然后单击 "**添加新项**"。
2. 选择 "**全局应用程序类**" 项模板，然后单击 "**添加**"。

    ![添加 global.asax](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. 将 SignalR 路由注册代码添加到应用程序\_启动方法：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    默认情况下，所有 SignalR 流量的基本 URL 都是 "/signalr"，而 "/signalr/hubs" 用于检索动态生成的 JavaScript 文件，该文件定义应用程序中的所有中心的代理。 Routeconfig 方法包括一些重载，可用于在[HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx)类的实例中指定不同的基 URL 和某些 SignalR 选项。
4. 将 using 语句添加到文件顶部：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. 保存并关闭*global.asax*文件，并生成项目。

你现在已经完成了服务器代码的设置。 在下一部分中，你将设置客户端。

<a id="client"></a>

## <a name="set-up-the-client-code"></a>设置客户端代码

1. 在项目文件夹中创建一个新的 HTML 文件，并将其命名为*StockTicker*。
2. 将模板代码替换为以下代码：

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    HTML 创建一个表，其中包含5列、标题行和数据行，其中的单个单元格跨所有5列。 数据行显示 "正在加载 ..."仅当应用程序启动时，才会立即显示。 JavaScript 代码将删除该行，并在其位置行中添加从服务器检索到的股票数据。

    脚本标记指定 jQuery 脚本文件、SignalR 核心脚本文件、SignalR 代理脚本文件以及稍后将创建的 StockTicker 脚本文件。 SignalR 代理脚本文件（指定 "/signalr/hubs" URL）是动态生成的，它为 Hub 类上的方法定义了代理方法，在本例中为 StockTickerHub. GetAllStocks。 如果愿意，可以使用[SignalR 实用工具](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手动生成此 JavaScript 文件，并在 routeconfig 方法调用中禁用动态文件创建。
3. > [!IMPORTANT]
   > 请确保*StockTicker*中的 JavaScript 文件引用正确。 也就是说，请确保脚本标记（本例中为1.8.2）中的 jQuery 版本与项目的 "*脚本*" 文件夹中的 jquery 版本相同，并确保脚本标记中的 SignalR 版本与项目的 "*脚本*" 文件夹中的 SignalR 版本相同。 如有必要，请更改脚本标记中的文件名。
4. 在**解决方案资源管理器**中，右键单击*StockTicker*，然后单击 "**设为起始页**"。
5. 在项目文件夹中创建一个新的 JavaScript 文件，并将其命名为*StockTicker*。
6. 将模板代码替换为以下代码：

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    $. 连接引用 SignalR 代理。 此代码将获取对 StockTickerHub 类的代理的引用，并将其放在 "股票行情" 变量中。 代理名称是 [HubName] 属性设置的名称：

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    定义所有变量和函数后，文件中的最后一行代码通过调用 SignalR start 函数初始化 SignalR 连接。 Start 函数以异步方式执行并返回[JQuery 延迟的对象](http://api.jquery.com/category/deferred-object/)，这意味着你可以调用 done 函数来指定要在异步操作完成时调用的函数。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    Init 函数调用服务器上的 getAllStocks 函数，并使用服务器返回的信息更新股票表。 请注意，默认情况下，你必须在客户端上使用 camel 大小写格式，但在服务器上，方法名称采用 pascal 大小写形式。 Camel 大小写规则仅适用于方法，而不适用于对象。 例如，你指的是股票。符号和股票。价格，而不是股票价格。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    如果要在客户端上使用 pascal 大小写，或想要使用完全不同的方法名称，则可以使用 HubMethodName 属性修饰集线器方法，就像使用 HubName 属性修饰集线器类本身一样。

    在 init 方法中，为从服务器接收的每个 stock 对象创建用于表行的 HTML，方法是调用 formatStock 来设置 stock 对象的属性的格式，然后通过调用取代（在*StockTicker*顶部定义），将 rowTemplate 变量中的占位符替换为 stock 对象属性值。 然后，将生成的 HTML 追加到 stock 表中。

    调用 init 的方法是，将其作为在异步启动函数完成后执行的回调函数传入。 如果在调用 start 后将 init 称为单独的 JavaScript 语句，该函数将失败，因为它会立即执行，而不会等待启动函数完成建立连接。 在这种情况下，init 函数将尝试在建立服务器连接之前调用 getAllStocks 函数。

    当服务器更改股票价格时，它将在连接的客户端上调用 updateStockPrice。 该函数将添加到 stockTicker 代理的客户端属性，以使其可用于来自服务器的调用。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    UpdateStockPrice 函数将从服务器接收的常用对象的格式设置为与 init 函数中相同的方式。 但是，它不会将行追加到表中，而是在表中查找库存的当前行，并将该行替换为新行。

<a id="test"></a>

## <a name="test-the-application"></a>测试应用程序

1. 按 F5 以调试模式运行应用程序。

    Stock 表最初显示 "正在加载 ..."行，然后在短暂延迟后显示初始股票数据，然后股票价格开始更改。

    ![“加载”](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![初始股票表](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![从服务器接收更改的股票表](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. 复制浏览器地址栏中的 URL，并将其粘贴到一个或多个新的浏览器窗口中。

    初始股票显示器与第一个浏览器相同，同时发生更改。
3. 关闭所有浏览器并打开一个新浏览器，然后切换到相同的 URL。

    StockTicker singleton 对象已继续在服务器中运行，因此，stock 表显示的是股票持续变化。 （看不到具有零更改图的初始表。）
4. 关闭浏览器。

<a id="enablelogging"></a>

## <a name="enable-logging"></a>启用日志记录

SignalR 具有内置日志记录功能，可以在客户端上启用该功能以帮助进行故障排除。 在本部分中，你将启用日志记录，并查看示例，这些示例演示了日志如何告诉你以下哪种传输方法 SignalR 正在使用：

- [Websocket](http://en.wikipedia.org/wiki/WebSocket)，受 IIS 8 和当前浏览器支持。
- Internet Explorer 之外的浏览器所支持的[服务器发送事件](http://en.wikipedia.org/wiki/Server-sent_events)。
- Internet Explorer 支持的[永久帧](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。
- 所有浏览器都支持[Ajax 长轮询](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)。

对于任何给定的连接，SignalR 将选择服务器和客户端都支持的最佳传输方法。

1. 打开*StockTicker* ，并添加一行代码，以便在文件末尾初始化连接的代码之前立即启用日志记录：

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. 按 F5 运行该项目。
3. 打开浏览器的 "开发人员工具" 窗口，并选择控制台查看日志。 您可能必须刷新该页才能查看为新连接协商传输方法的 Signalr 的日志。

    如果在 Windows 8 （IIS 8）上运行 Internet Explorer 10，则传输方法为 Websocket。

    ![IE 10 IIS 8 控制台](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    如果在 Windows 7 上运行 Internet Explorer 10 （IIS 7.5），则传输方法为 iframe。

    ![IE 10 控制台、IIS 7。5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    在 Firefox 中，安装 Firebug 外接程序以获取控制台窗口。 如果在 Windows 8 （IIS 8）上运行 Firefox 19，则传输方法为 Websocket。

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    如果在 Windows 7 上运行 Firefox 19 （IIS 7.5），则传输方法为服务器发送事件。

    ![Firefox 19 IIS 7.5 控制台](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a>安装和查看完整的 StockTicker 示例

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 包安装的 StockTicker 应用程序的功能比你刚从头创建的简化版本包含的功能更多。 在本教程的此部分中，你将安装 NuGet 包并查看实现这些功能的新功能和代码。

### <a name="install-the-signalrsample-nuget-package"></a>安装 SignalR NuGet 包

1. 在**解决方案资源管理器**中，右键单击该项目，然后单击 "**管理 NuGet 包**"。
2. 在 "**管理 NuGet 包**" 对话框中，单击 "**联机**"，在 "**联机搜索**" 框中输入*SignalR* ，然后单击**SignalR**包中的 "**安装**"。

    ![安装 SignalR 包](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. 在*global.asax*文件中，注释掉 RouteTable routeconfig （）;你之前在应用程序\_Start 方法中添加的行。

    不再需要*global.asax*中的代码，因为 SignalR 包在*应用\_Start/RegisterHubs*文件中注册 SignalR 路由：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    WebActivatorEx NuGet 包中包含由程序集特性引用的 WebActivator 类，它作为 SignalR 包的依赖项安装。
4. 在**解决方案资源管理器**中，展开通过安装 SignalR 包创建的*SignalR*文件夹。
5. 在*SignalR*文件夹中，右键单击 " *StockTicker*"，然后单击 "**设为起始页**"。

    > [!NOTE]
    > 安装 SignalR NuGet 包可能会更改你在*脚本*文件夹中拥有的 jQuery 版本。 包安装在*SignalR*文件夹中的新的*StockTicker*文件将与包所安装的 jQuery 版本同步，但是，如果你想要再次运行原始*StockTicker*文件，则可能需要先更新 script 标记中的 jQuery 引用。

### <a name="run-the-application"></a>运行此应用程序

1. 按 F5 运行该应用程序。

    除了前面看到的网格外，整个股票行情滚动应用程序还会显示一个水平滚动窗口，其中显示相同的股票数据。 首次运行应用程序时，"市场" 将为 "已关闭"，同时会显示静态网格和不滚动的滚动条窗口。

    ![StockTicker 屏幕启动](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    单击 "**公开市场**" 时，"**实时股票行情**" 框将开始水平滚动，服务器将开始随机广播股票价格变化。 每次股票价格变化时，都会更新 "**实时库存表**" 网格和 "**实时股票行情**" 框。 当股票价格变化为正时，股票显示为绿色背景，当更改为负值时，会显示红色背景。

    ![StockTicker 应用，市场开放式](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    "**关闭市场**" 按钮将停止更改并停止滚动更新，并在价格变化开始之前将所有股票数据**重置为**初始状态。 如果打开更多浏览器窗口并访问相同的 URL，则会在每个浏览器中同时动态更新相同的数据。 单击其中一个按钮时，所有浏览器将同时以相同的方式进行响应。

### <a name="live-stock-ticker-display"></a>直播股票行情显示

**Live 股票行情**显示在 div 元素中的一个无序列表，该列表通过 CSS 样式格式化为单个行。 该代号的初始化和更新方式与表的更新方式相同：在 &lt;li&gt; 模板字符串中替换占位符，并将 &lt;li&gt; 元素动态添加到 &lt;ul&gt; 元素。 使用 jQuery 动画函数执行滚动，以改变 div 中无序列表的左边距。

股票行情的 HTML：

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

股票行情，CSS：

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

使其滚动的 jQuery 代码：

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>客户端可以调用的服务器上的其他方法

StockTickerHub 类定义了客户端可以调用的四种附加方法：

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

将调用 OpenMarket、CloseMarket 和 Reset 来响应页面顶部的按钮。 它们演示了触发状态更改的一种客户端模式，这些更改会立即传播到所有客户端。 其中每个方法都调用 StockTicker 类中的一个方法，该方法影响市场状态更改，然后广播新状态。

在 StockTicker 类中，市场的状态由返回 MarketState 枚举值的 MarketState 属性来维护：

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

更改市场状态的每个方法都在锁定块中执行此操作，因为 StockTicker 类必须 threadsafe：

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

为了确保此代码是 threadsafe 的，支持 MarketState 属性的 \_marketState 字段被标记为 volatile，

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

BroadcastMarketStateChange 和 BroadcastMarketReset 方法类似于你已看到的 BroadcastStockPrice 方法，只不过它们调用在客户端定义的不同方法：

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>服务器可以调用的客户端上的其他函数

UpdateStockPrice 函数现在同时处理网格和滚动条的显示，并使用 jQuery。彩色闪烁红色和绿色颜色。

*SignalR*中的新函数基于市场状态启用和禁用按钮，并停止或启动 "滚动条" 窗口水平滚动。 由于将多个函数添加到了股市代号，因此使用[jQuery extend 函数](http://api.jquery.com/jQuery.extend/)添加它们。

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>建立连接后的其他客户端设置

客户端建立连接后，还需要执行一些额外的工作：查找市场是否已打开或关闭，以调用适当的 marketOpened 或 marketClosed 函数，并将服务器方法调用附加到这些按钮。

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

在建立连接之前，服务器方法不会连接到按钮，这样代码就不能尝试在可用之前调用服务器方法。

<a id="nextsteps"></a>

## <a name="next-steps"></a>后续步骤

在本教程中，你已了解如何对 SignalR 应用程序进行编程，以将消息从服务器广播到所有连接的客户端，这两个客户端均定期和响应来自任何客户端的通知。 使用多线程单独实例来维护服务器状态的模式也可以用于多玩家在线游戏方案。 有关示例，请参阅[基于 SignalR 的 ShootR 游戏](https://github.com/NTaylorMullen/ShootR)。

有关显示对等通信方案的教程，入门请参阅[SignalR With](index.md) And[实时更新 with SignalR](index.md)。

若要了解更高级的 SignalR 开发概念，请访问以下站点以获取 SignalR 源代码和资源：

- [ASP.NET SignalR](https://asp.net/signalr/)
- [SignalR 项目](http://signalr.net/)
- [SignalR Github 和示例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
