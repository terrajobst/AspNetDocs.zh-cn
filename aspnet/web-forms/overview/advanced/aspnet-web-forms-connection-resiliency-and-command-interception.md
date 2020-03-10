---
uid: web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
title: ASP.NET Web Forms 连接复原和命令侦听 |Microsoft Docs
author: Erikre
description: 本教程介绍如何修改示例应用程序，以支持连接复原和命令侦听。
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 6d497001-fa80-4765-b4cc-181fe90b894e
msc.legacyurl: /web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
msc.type: authoredcontent
ms.openlocfilehash: 95f0b5635c12d5ef88622e5766c1278c6570dd4d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484232"
---
# <a name="aspnet-web-forms-connection-resiliency-and-command-interception"></a>ASP.NET Web 窗体连接复原和命令截获

作者： [Erik Reitan](https://github.com/Erikre)

在本教程中，您将修改 Wingtip 玩具示例应用程序，以支持连接复原和命令拦截。 启用连接复原后，当发生云环境的典型暂时性错误时，Wingtip 玩具示例应用程序将自动重试数据调用。 此外，通过实现命令拦截，Wingtip 玩具示例应用程序将捕获发送到数据库的所有 SQL 查询，以便记录或更改这些查询。

> [!NOTE] 
> 
> 此 Web 窗体教程基于 Tom Dykstra 的以下 MVC 教程：  
> [ASP.NET MVC 应用程序中的实体框架的连接复原和命令截获](../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="what-youll-learn"></a>学习内容：

- 如何提供连接复原能力。
- 如何实现命令截取。

## <a name="prerequisites"></a>系统必备

在开始之前，请确保计算机上已安装了以下软件：

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs)或[Microsoft Visual Studio Express 2013 for Web](https://www.microsoft.com/visualstudio/11/downloads#express-web)。 将自动安装 .NET Framework。
- Wingtip 玩具示例项目，以便可以在 Wingtip 玩具项目中实现本教程中所述的功能。 以下链接提供了下载详细信息：

    - [入门 4.5.1 Web 窗体-Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409)（C#）
- 在完成本教程之前，请考虑查看相关的教程系列，[并入门 ASP.NET 4.5 Web Forms 和 Visual Studio 2013](../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 本教程系列将帮助你熟悉**WingtipToys**项目和代码。

## <a name="connection-resiliency"></a>连接复原

考虑将应用程序部署到 Windows Azure 时，需要考虑的一个选项是将数据库部署到**microsoft** **azure SQL 数据库**（一个云数据库服务）。 当你连接到云数据库服务时，如果连接到同一数据中心的 web 服务器和数据库服务器直接连接到云数据库服务，则暂时性连接错误通常会更频繁。 即使云 web 服务器和云数据库服务托管在同一数据中心，它们之间的网络连接也可能存在问题，例如负载均衡器。

此外，云服务通常由其他用户共享，这意味着其响应能力可能会受到影响。 您对数据库的访问可能会受到限制。 限制意味着，当你尝试比你的*服务级别协议*（SLA）中的允许更频繁地访问它时，数据库服务将引发异常。

访问云服务时出现的许多或大多数连接问题都是暂时性的，也就是说，它们会在短时间内解决。 因此，当你尝试数据库操作并获取通常是暂时性的错误类型时，你可以在短时间等待后再次尝试该操作，并且该操作可能成功。 如果你通过自动重试来处理暂时性错误，则你可以为用户提供更好的体验，使他们对客户不可见。 实体框架6中的连接复原功能自动执行重试失败的 SQL 查询这一过程。

必须为特定数据库服务正确配置连接复原功能：

1. 它必须知道哪些异常可能是暂时性的。 您希望重试由于网络连接暂时丢失而导致的错误，例如，不是由程序错误导致的错误。
2. 它必须等待一段适当的时间，重试失败的操作。 在批处理过程中，你可以等待多长时间才能进行批处理，而不能在用户等待响应的联机网页之间等待。
3. 它必须在放弃之前重试相应的次数。 你可能需要在联机应用程序的批处理过程中重试更多次。

你可以为实体框架提供程序支持的任何数据库环境手动配置这些设置。

若要启用连接复原，只需在程序集中创建一个派生自 `DbConfiguration` 类的类，并在该类中设置 SQL 数据库执行策略，该策略在实体框架中是重试策略的另一种术语。

### <a name="implementing-connection-resiliency"></a>实现连接复原

1. 下载并在 Visual Studio 中打开[WingtipToys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409)示例 Web 窗体应用程序。
2. 在**WingtipToys**应用程序的*逻辑*文件夹中，添加名为*WingtipToysConfiguration.cs*的类文件。
3. 用下面的代码替换现有代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample1.cs)]

实体框架会自动运行它在从 `DbConfiguration`派生的类中查找的代码。 您可以使用 `DbConfiguration` 类在代码中执行配置任务，*您将在 web.config 文件中*执行此操作。 有关详细信息，请参阅[EntityFramework 基于代码的配置](https://msdn.microsoft.com/data/jj680699)。

1. 在*逻辑*文件夹中，打开*AddProducts.cs*文件。
2. 为 `System.Data.Entity.Infrastructure` 添加 `using` 语句，如黄色突出显示：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample2.cs?highlight=6)]
3. 将 `catch` 块添加到 `AddProduct` 方法，以便将 `RetryLimitExceededException` 记录为黄色突出显示的部分：   

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample3.cs?highlight=14-15,17-22)]

通过添加 `RetryLimitExceededException` 异常，可以提供更好的日志记录或向用户显示一条错误消息，用户可在其中选择重试该过程。 捕获 `RetryLimitExceededException` 异常后，只需尝试并失败几次，就可能会发生暂时性错误。 返回的实际异常将包装在 `RetryLimitExceededException` 异常中。 此外，还添加了一个常规 catch 块。 有关 `RetryLimitExceededException` 异常的详细信息，请参阅[实体框架连接复原/重试逻辑](https://msdn.microsoft.com/data/dn456835)。

## <a name="command-interception"></a>命令侦听

现在，你已启用重试策略，你如何进行测试来验证它是否按预期方式工作？ 不太容易强制发生暂时性错误，尤其是在本地运行时，将实际暂时性错误集成到自动单元测试中会特别困难。 若要测试连接复原功能，需要有一种方法来截获实体框架发送到 SQL Server 的查询，并将 SQL Server 响应替换为通常是暂时性的异常类型。

你还可以使用查询拦截来实现云应用程序的最佳做法：记录对外部服务（如数据库服务）的所有调用的延迟、成功或失败。

在本教程的此部分中，你将使用实体框架的[*拦截功能*](https://msdn.microsoft.com/data/dn469464)来记录和模拟暂时性错误。

### <a name="create-a-logging-interface-and-class"></a>创建日志记录接口和类

日志记录的最佳做法是使用[`interface`](https://msdn.microsoft.com/library/ms173156.aspx) ，而不是对 `System.Diagnostics.Trace` 或日志记录类的硬编码调用。 这样就可以在以后需要时更轻松地更改日志记录机制。 因此，在本部分中，你将创建日志记录接口和类以实现它。

根据上述过程，已在 Visual Studio 中下载并打开了**WingtipToys**示例应用程序。

1. 在**WingtipToys**项目中创建一个文件夹并将其命名为*日志记录*。
2. 在*日志记录*文件夹中，创建一个名为*ILogger.cs*的类文件，并将默认代码替换为以下代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample4.cs)]

   接口提供三个跟踪级别来指示日志的相对重要性，另一个设计用于为外部服务调用（如数据库查询）提供滞后时间信息。 日志记录方法包含允许您在异常中传递的重载。 这是因为实现接口的类可以可靠地记录包括堆栈跟踪和内部异常的异常信息，而不是依赖于整个应用程序的每个日志记录方法调用中执行的操作。  
  
   使用 `TraceApi` 方法可以跟踪对外部服务（如 SQL 数据库）的每个调用的延迟。
3. 在*日志记录*文件夹中，创建一个名为*Logger.cs*的类文件，并将默认代码替换为以下代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample5.cs)]

实现使用 `System.Diagnostics` 进行跟踪。 这是 .NET 的内置功能，可轻松生成和使用跟踪信息。 可以将许多 &quot;侦听器&quot; 用于 `System.Diagnostics` 跟踪、将日志写入文件，或者将日志写入 Windows Azure 中的 blob 存储。 有关详细信息，请参阅[Visual Studio 中的 Microsoft Azure 网站疑难解答](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)中的一些选项和其他资源的链接。 对于本教程，只需在 Visual Studio 的 "**输出**" 窗口中查看日志。

在生产应用程序中，您可能需要考虑使用除 `System.Diagnostics`以外的跟踪框架，如果您决定执行该操作，则可以使用 `ILogger` 接口，使其相对容易地切换到不同的跟踪机制。

### <a name="create-interceptor-classes"></a>创建侦听器类

接下来，您将创建实体框架将在每次将查询发送到数据库时调用的类，一个用于模拟暂时性错误，另一个用于执行日志记录。 这些侦听器类必须从 `DbCommandInterceptor` 类派生。 在这些方法中，你将编写在要执行查询时自动调用的方法重写。 在这些方法中，你可以检查或记录要发送到数据库的查询，并且可以在将查询发送到数据库之前对其进行更改，也可以在不将查询传递到数据库的情况下将内容返回给实体框架。

1. 若要创建侦听器类，以便在将每个 SQL 查询发送到数据库之前对其进行记录，请在*逻辑*文件夹中创建一个名为*InterceptorLogging.cs*的类文件，并将默认代码替换为以下代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample6.cs)]

   对于成功的查询或命令，此代码会写入包含延迟信息的信息日志。 对于异常，它将创建错误日志。
2. 若要创建将在名为*AdminPage*的页面上的 "**名称**" 文本框中输入 &quot;Throw&quot; 时生成虚拟暂时性错误的侦听器类，请在*逻辑*文件夹中创建一个名为*InterceptorTransientErrors.cs*的类文件，并将默认代码替换为以下代码：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample7.cs)]

    此代码仅覆盖 `ReaderExecuting` 方法，该方法将为可以返回多行数据的查询调用。 如果要检查其他类型查询的连接复原能力，还可以重写 `NonQueryExecuting` 和 `ScalarExecuting` 方法，因为日志记录侦听器会这样做。  
  
   稍后，你将以 "管理员" 身份登录，并选择顶部导航栏上的 "**管理员**" 链接。 然后，在 " *AdminPage* " 页上，你将添加一个名为 &quot;Throw&quot;的产品。 此代码为错误编号20创建了一个虚拟 SQL 数据库异常，这是一个已知通常为暂时性的类型。 目前识别为暂时性的其他错误号为64、233、10053、10054、10060、10928、10929、40197、40501和40613，但在 SQL 数据库的新版本中可能会有所更改。 该产品将重命名为 "TransientErrorExample"，你可以在*InterceptorTransientErrors.cs*文件的代码中执行此操作。  
  
   此代码会将异常返回到实体框架，而不是运行查询并传递回结果。 暂时异常返回*四*次，然后代码恢复到将查询传递到数据库的正常过程。

    由于记录了所有内容，因此你将能够看到实体框架尝试在最后一次成功之前执行查询四次，并且应用程序的唯一区别在于，使用查询结果呈现页面需要更长时间。  
  
   可以配置实体框架重试的次数;代码指定了四次，因为这是 SQL 数据库执行策略的默认值。 如果更改执行策略，则还需更改此处的代码，用于指定生成暂时性错误的次数。 你还可以更改代码以生成更多异常，以便实体框架将引发 `RetryLimitExceededException` 异常。
3. 在*global.asax*中，添加以下 using 语句：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample8.cs)]
4. 然后，将突出显示的行添加到 `Application_Start` 方法：  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample9.cs?highlight=17-20)]

如果实体框架将查询发送到数据库，则会导致侦听器代码运行的代码行。 请注意，由于你为暂时性错误模拟和日志记录创建了单独的侦听器类，因此你可以单独启用和禁用它们。   
  
 可以在代码中的任意位置使用 `DbInterception.Add` 方法添加侦听器。不一定要使用 `Application_Start` 方法。 另一种方法是，如果未在 `Application_Start` 方法中添加侦听器，将更新或添加名为*WingtipToysConfiguration.cs*的类，并将上面的代码放在 `WingtipToysConfiguration` 类构造函数的末尾。

无论你将此代码放在何处，请注意不要多次对同一侦听器执行 `DbInterception.Add`，否则你将获得其他侦听器实例。 例如，如果您添加日志记录侦听器两次，您将看到每个 SQL 查询都有两个日志。

拦截按注册顺序执行（调用 `DbInterception.Add` 方法的顺序）。 此顺序可能取决于您在侦听器中所执行的操作。 例如，侦听器可能会更改它在 `CommandText` 属性中获取的 SQL 命令。 如果它确实更改了 SQL 命令，则下一个侦听器将获取更改的 SQL 命令，而不是原始 SQL 命令。

您已编写暂时性错误模拟代码，使您可以通过在用户界面中输入不同的值导致暂时性错误。 作为替代方法，您可以编写侦听器代码，以便始终在不检查特定参数值的情况下生成暂时性异常序列。 然后，只需在要生成暂时性错误时才添加侦听器。 但是，如果您这样做，则在数据库初始化完成之前，不要添加侦听器。 换句话说，在开始生成暂时性错误之前，请至少执行一项数据库操作，例如对某个实体集进行查询。 实体框架在数据库初始化期间执行多个查询，它们不在事务中执行，因此在初始化期间发生的错误可能导致上下文进入不一致状态。

## <a name="test-logging-and-connection-resiliency"></a>测试日志记录和连接复原

1. 在 Visual Studio 中，按**F5**以调试模式运行应用程序，然后使用 "Pa $ $word" 作为密码以 "管理员" 身份登录。
2. 在顶部的导航栏中选择 "**管理员**"。
3. 输入具有适当说明、价格和图像文件的名为 "Throw" 的新产品。
4. 按 "**添加产品**" 按钮。  
   你会注意到，浏览器似乎已挂起几秒钟，而实体框架重试查询多次。 第一次重试发生的速度非常快，在每次重试前等待增加。 每次重试之前等待的这一过程称为*指数回退*。
5. 等待，直到页面不再尝试加载。
6. 停止项目，并查看 "Visual Studio**输出**" 窗口以查看跟踪输出。 可以通过选择 "**调试**" -&gt; **Windows** -&gt;**输出**来查找 "**输出**" 窗口。 您可能必须滚动使用记录器编写的其他几个日志。  
  
   请注意，您可以查看发送到数据库的实际 SQL 查询。 你将看到一些初始查询和命令，实体框架在开始之前，请检查数据库版本和迁移历史记录表。   
    ![输出窗口](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image1.png)   
   请注意，除非停止并重新启动应用程序，否则不能重复此测试。 如果希望能够在应用程序的单个运行中多次测试连接复原，可以编写代码以在 `InterceptorTransientErrors` 中重置错误计数器。
7. 若要查看执行策略（重试策略）的差异，请在*逻辑*文件夹中注释掉*WingtipToysConfiguration.cs*文件中的 `SetExecutionStrategy` 行，再次运行调试模式中的 "**管理**" 页，然后添加名为 &quot;的产品&quot; 再次引发。  
  
   这次当首次尝试执行查询时，调试器会立即停止第一个生成的异常。  
    ![调试-查看详细信息](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image2.png)
8. 取消注释*WingtipToysConfiguration.cs*文件中的 `SetExecutionStrategy` 行。

## <a name="summary"></a>摘要

在本教程中，你已了解如何修改 Web 窗体示例应用程序，以支持连接复原和命令截获。

## <a name="next-steps"></a>后续步骤

在 ASP.NET Web 窗体中查看了连接复原和命令截获后，请查看[ASP.NET 4.5 中](../performance-and-caching/using-asynchronous-methods-in-aspnet-45.md)的 ASP.NET Web 窗体主题异步方法。 本主题将介绍使用 Visual Studio 生成异步 ASP.NET Web 窗体应用程序的基础知识。
