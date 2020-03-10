---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教程：在 ASP.NET MVC 应用中结合使用连接复原和命令截获
author: tdykstra
description: 在本教程中，你将了解如何使用连接复原和命令拦截。 它们是实体框架6的两项重要功能。
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: c89d809f-6c65-4425-a3fa-c9f6e8ac89f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 276266f8ae9df38529d44742ebe6ac0dc8e79727
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471398"
---
# <a name="tutorial-use-connection-resiliency-and-command-interception-with-entity-framework-in-an-aspnet-mvc-app"></a>教程：在 ASP.NET MVC 应用中使用连接复原和命令截获实体框架

到目前为止，应用程序已在本地 IIS Express 开发计算机上运行。 要使真实应用程序可供其他人通过 Internet 使用，你必须将其部署到 web 托管提供商，并且必须将数据库部署到数据库服务器。

在本教程中，你将了解如何使用连接复原和命令拦截。 它们是实体框架6的两项重要功能，在部署到云环境时特别有用：连接复原（暂时性错误的自动重试）和命令拦截（捕获发送到数据库的所有 SQL 查询以便记录或更改它们）。

此连接复原和命令拦截教程是可选的。 如果你跳过本教程，则在后续教程中将需要进行一些次要调整。

在本教程中，你将了解：

> [!div class="checklist"]
> * 启用连接复原
> * 启用命令拦截
> * 测试新配置

## <a name="prerequisites"></a>系统必备

* [排序、筛选和分页](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-connection-resiliency"></a>启用连接复原

将应用程序部署到 Windows Azure 时，会将数据库部署到 Microsoft Azure SQL 数据库（一种云数据库服务）。 当你连接到云数据库服务时，如果连接到同一数据中心的 web 服务器和数据库服务器直接连接到云数据库服务，则暂时性连接错误通常会更频繁。 即使云 web 服务器和云数据库服务托管在同一数据中心，它们之间的网络连接也可能存在问题，例如负载均衡器。

此外，云服务通常由其他用户共享，这意味着其响应能力可能会受到影响。 您对数据库的访问可能会受到限制。 限制意味着，当你尝试比你的服务级别协议（SLA）中的允许更频繁地访问它时，数据库服务将引发异常。

访问云服务时，很多或大多数连接问题都是暂时性的，也就是说，它们会在短时间内解决。 因此，当你尝试数据库操作并获取通常是暂时性的错误类型时，你可以在短时间等待后再次尝试该操作，并且该操作可能成功。 如果你通过自动重试来处理暂时性错误，则你可以为用户提供更好的体验，使他们对客户不可见。 实体框架6中的连接复原功能自动执行重试失败的 SQL 查询这一过程。

必须为特定数据库服务正确配置连接复原功能：

- 它必须知道哪些异常可能是暂时性的。 您希望重试由于网络连接暂时丢失而导致的错误，例如，不是由程序错误导致的错误。
- 它必须等待一段适当的时间，重试失败的操作。 在批处理过程中，你可以等待多长时间才能进行批处理，而不能在用户等待响应的联机网页之间等待。
- 它必须在放弃之前重试相应的次数。 你可能需要在联机应用程序的批处理过程中重试更多次。

你可以为实体框架提供程序支持的任何数据库环境手动配置这些设置，但通常适用于使用 Windows Azure SQL 数据库的联机应用程序的默认值已配置为你，这些是你将为 Contoso 大学应用程序实现的设置。

若要启用连接复原，只需在程序集中创建一个派生自[DbConfiguration](https://msdn.microsoft.com/data/jj680699.aspx)类的类，并在该类中设置 SQL 数据库*执行策略*，在 EF 中，这是*重试策略*的另一种术语。

1. 在 DAL 文件夹中，添加名为*SchoolConfiguration.cs*的类文件。
2. 将模板代码替换为以下代码：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

    实体框架会自动运行它在从 `DbConfiguration`派生的类中查找的代码。 您可以使用 `DbConfiguration` 类在代码中执行配置任务，*您将在 web.config 文件中*执行此操作。 有关详细信息，请参阅[EntityFramework 基于代码的配置](https://msdn.microsoft.com/data/jj680699)。
3. 在*StudentController.cs*中，添加 `System.Data.Entity.Infrastructure`的 `using` 语句。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]
4. 更改捕获 `DataException` 异常的所有 `catch` 块，使它们改为捕获 `RetryLimitExceededException` 异常。 例如:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=1)]

    你正在使用 `DataException` 来尝试标识可能是暂时性的错误，以便为友好的 "重试" 消息。 但既然您已经打开了重试策略，则仅有可能是暂时性的错误已尝试并失败多次，并且返回的实际异常将包装在 `RetryLimitExceededException` 异常中。

有关详细信息，请参阅[实体框架连接复原/重试逻辑](https://msdn.microsoft.com/data/dn456835)。

## <a name="enable-command-interception"></a>启用命令拦截

现在，你已启用重试策略，你如何进行测试来验证它是否按预期方式工作？ 不太容易强制发生暂时性错误，尤其是在本地运行时，将实际暂时性错误集成到自动单元测试中会特别困难。 若要测试连接复原功能，需要有一种方法来截获实体框架发送到 SQL Server 的查询，并将 SQL Server 响应替换为通常是暂时性的异常类型。

你还可以使用查询拦截来实现云应用程序的最佳做法：记录对外部服务（如数据库服务）的[所有调用的延迟、成功或失败](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)。 EF6 提供了一个[专用的日志记录 API](https://msdn.microsoft.com/data/dn469464) ，可让你更轻松地进行日志记录，但在本教程的此部分中，你将了解如何直接使用实体框架的[侦听功能](https://msdn.microsoft.com/data/dn469464)来记录和模拟暂时性错误。

### <a name="create-a-logging-interface-and-class"></a>创建日志记录接口和类

[日志记录的最佳做法](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log)是使用接口执行该操作，而不是对对 system.exception 或日志记录类的硬编码调用。 这样就可以在以后需要时更轻松地更改日志记录机制。 因此，在本部分中，你将创建日志记录接口和用于实现该接口的类。/p >

1. 在项目中创建一个文件夹并将其命名为*日志记录*。
2. 在 "*日志记录*" 文件夹中，创建一个名为*ILogger.cs*的类文件，并将模板代码替换为以下代码：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    接口提供三个跟踪级别来指示日志的相对重要性，另一个设计用于为外部服务调用（如数据库查询）提供滞后时间信息。 日志记录方法包含允许您在异常中传递的重载。 这是因为实现接口的类可以可靠地记录包括堆栈跟踪和内部异常的异常信息，而不是依赖于整个应用程序的每个日志记录方法调用中执行的操作。

    使用 TraceApi 方法可以跟踪对外部服务（如 SQL 数据库）进行的每个调用的延迟。
3. 在 "*日志记录*" 文件夹中，创建一个名为*Logger.cs*的类文件，并将模板代码替换为以下代码：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    实现使用 system.exception 进行跟踪。 这是 .NET 的内置功能，可轻松生成和使用跟踪信息。 可以将多个 "侦听器" 用于系统诊断跟踪、将日志写入文件或将其写入到 Azure 中的 blob 存储。 有关详细信息，请参阅[Visual Studio 中的 Azure 网站疑难解答](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio)中的一些选项和其他资源的链接。 对于本教程，只需在 Visual Studio 的 "**输出**" 窗口中查看日志。

    在生产应用程序中，你可能想要考虑除 ILogger 之外的跟踪包，并且如果你决定执行此操作，则可以相对容易地切换到其他跟踪机制。

### <a name="create-interceptor-classes"></a>创建侦听器类

接下来，你将创建实体框架将在每次将查询发送到数据库时调用的类，一个用于模拟暂时性错误，另一个用于执行日志记录。 这些侦听器类必须从 `DbCommandInterceptor` 类派生。 在其中，你编写了将在执行查询时自动调用的方法替代。 在这些方法中，你可以检查或记录要发送到数据库的查询，并且可以在将查询发送到数据库之前对其进行更改，也可以在不将查询传递到数据库的情况下将内容返回给实体框架。

1. 若要创建侦听器类，以便记录发送到数据库的每个 SQL 查询，请在*DAL*文件夹中创建一个名为*SchoolInterceptorLogging.cs*的类文件，并将模板代码替换为以下代码：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

    对于成功的查询或命令，此代码会写入包含延迟信息的信息日志。 对于异常，它将创建错误日志。
2. 若要创建将在 "**搜索**" 框中输入 "Throw" 时产生虚拟暂时性错误的侦听器类，请在*DAL*文件夹中创建名为*SchoolInterceptorTransientErrors.cs*的类文件，并将模板代码替换为以下代码：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

    此代码仅覆盖 `ReaderExecuting` 方法，该方法将为可以返回多行数据的查询调用。 如果要检查其他类型查询的连接复原能力，还可以重写 `NonQueryExecuting` 和 `ScalarExecuting` 方法，因为日志记录侦听器会这样做。

    当你运行 "学生" 页并输入 "Throw" 作为搜索字符串时，此代码将为错误编号20创建一个虚拟 SQL 数据库异常，这是一个已知通常为暂时性的类型。 目前识别为暂时性的其他错误号为64、233、10053、10054、10060、10928、10929、40197、40501和40613，但在 SQL 数据库的新版本中可能会有所更改。

    此代码会将异常返回到实体框架，而不是运行查询并传递返回查询结果。 暂时异常返回四次，然后代码恢复到将查询传递到数据库的正常过程。

    由于记录了所有内容，因此你将能够看到实体框架尝试在最后一次成功之前执行查询四次，并且应用程序的唯一区别在于，使用查询结果呈现页面需要更长时间。

    可以配置实体框架重试的次数;代码指定了四次，因为这是 SQL 数据库执行策略的默认值。 如果更改执行策略，则还需更改此处的代码，用于指定生成暂时性错误的次数。 你还可以更改代码以生成更多异常，以便实体框架将引发 `RetryLimitExceededException` 异常。

    在 "搜索" 框中输入的值将为 "`command.Parameters[0]`" 和 "`command.Parameters[1]`" （一个用于名字，另一个用于姓氏）。 找到值 "% Throw%" 时，将在这些参数中将 "Throw" 替换为 "a"，以便查找并返回某些学生。

    这只是一种简单的方法，可基于更改应用程序 UI 的某些输入来测试连接复原。 你还可以编写为所有查询或更新生成暂时性错误的代码，如稍后有关*DbInterception*方法的注释中所述。
3. 在*global.asax*中，添加以下 `using` 语句：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]
4. 将突出显示的行添加到 `Application_Start` 方法：

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=7-8)]

    如果实体框架将查询发送到数据库，则会导致侦听器代码运行的代码行。 请注意，由于你为暂时性错误模拟和日志记录创建了单独的侦听器类，因此你可以单独启用和禁用它们。

    可以在代码中的任意位置使用 `DbInterception.Add` 方法添加侦听器。不一定要使用 `Application_Start` 方法。 另一种选择是将此代码放在之前创建的 DbConfiguration 类中，以配置执行策略。

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=6-7)]

    无论你将此代码放在何处，请注意不要多次对同一侦听器执行 `DbInterception.Add`，否则你将获得其他侦听器实例。 例如，如果您添加日志记录侦听器两次，您将看到每个 SQL 查询都有两个日志。

    拦截按注册顺序执行（调用 `DbInterception.Add` 方法的顺序）。 此顺序可能取决于您在侦听器中所执行的操作。 例如，侦听器可能会更改它在 `CommandText` 属性中获取的 SQL 命令。 如果它确实更改了 SQL 命令，则下一个侦听器将获取更改的 SQL 命令，而不是原始 SQL 命令。

    您已编写暂时性错误模拟代码，使您可以通过在用户界面中输入不同的值导致暂时性错误。 作为替代方法，您可以编写侦听器代码，以便始终在不检查特定参数值的情况下生成暂时性异常序列。 然后，只需在要生成暂时性错误时才添加侦听器。 但是，如果您这样做，则在数据库初始化完成之前，不要添加侦听器。 换句话说，在开始生成暂时性错误之前，请至少执行一项数据库操作，例如对某个实体集进行查询。 实体框架在数据库初始化期间执行多个查询，它们不在事务中执行，因此在初始化期间发生的错误可能导致上下文进入不一致状态。

## <a name="test-the-new-configuration"></a>测试新配置

1. 按**F5**在调试模式下运行应用程序，然后单击 "**学生**" 选项卡。
2. 查看 Visual Studio "**输出**" 窗口以查看跟踪输出。 你可能需要向上滚动一些 JavaScript 错误才能访问记录器编写的日志。

    请注意，您可以查看发送到数据库的实际 SQL 查询。 你将看到一些初始查询和命令实体框架首先要开始、检查数据库版本和迁移历史记录表（你将在下一教程中了解迁移）。 你将看到一个用于分页的查询，确定有多少学生，最后你会看到获取学生数据的查询。

    ![正常查询的日志记录](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. 在 "**学生**" 页上，输入 "Throw" 作为搜索字符串，然后单击 "**搜索**"。

    ![引发搜索字符串](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    你会注意到，浏览器似乎已挂起几秒钟，而实体框架重试查询多次。 第一次重试会迅速发生，然后在每次重试前等待。 每次重试之前等待的这一过程称为*指数回退*。

    显示该页面时，显示名称中包含 "a" 的学生，查看 "输出" 窗口，你会看到同一查询尝试了五次，这四次返回暂时性的异常。 对于每个暂时性错误，您将看到在 `SchoolInterceptorTransientErrors` 类中生成暂时性错误（"命令返回暂时性错误"）时所编写的日志，并且当 `SchoolInterceptorLogging` 获取异常时，您将看到写入的日志。

    ![记录显示重试的输出](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    由于您输入了搜索字符串，因此返回学生数据的查询已参数化：

    [!code-sql[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.sql)]

    不会记录参数的值，但也可以这样做。 如果要查看参数值，则可以编写日志记录代码，以便从在侦听器方法中获取的 `DbCommand` 对象的 `Parameters` 属性获取参数值。

    请注意，除非停止并重新启动应用程序，否则不能重复此测试。 如果希望能够在应用程序的单个运行中多次测试连接复原，可以编写代码以在 `SchoolInterceptorTransientErrors`中重置错误计数器。
4. 若要查看执行策略（重试策略）的差异，请注释掉*SchoolConfiguration.cs*中的 `SetExecutionStrategy` 行，再次运行调试模式下的 "学生" 页，然后再次搜索 "Throw"。

    这次当首次尝试执行查询时，调试器会立即停止第一个生成的异常。

    ![虚拟异常](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
5. 取消对*SchoolConfiguration.cs*中的*SetExecutionStrategy*行的注释。

## <a name="get-the-code"></a>获取代码

[下载完成的项目](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他资源

可在[ASP.NET 数据访问-推荐的资源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到指向其他实体框架资源的链接。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 已启用连接复原
> * 启用的命令侦听
> * 已测试新配置

转到下一篇文章，了解 Code First 迁移和 Azure 部署。
> [!div class="nextstepaction"]
> [Code First 迁移和 Azure 部署](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)
