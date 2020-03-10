---
uid: signalr/overview/advanced/dependency-injection
title: SignalR 中的依赖项注入 |Microsoft Docs
author: bradygaster
description: 本主题中使用的软件版本 Visual Studio 2013 .NET 4.5 SignalR 版本2本主题的早期版本。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431864"
---
# <a name="dependency-injection-in-signalr"></a>SignalR 中的依赖项注入

作者： [Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 版本2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主题的早期版本
>
> 有关早期版本的 SignalR 的信息，请参阅[SignalR 旧版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>问题和注释
>
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

依赖关系注入是一种删除对象之间硬编码的依赖关系的方法，这样可以更轻松地替换对象的依赖项（使用模拟对象）或更改运行时行为。 本教程介绍如何在 SignalR 集线器上执行依赖关系注入。 它还演示了如何通过 SignalR 使用 IoC 容器。 IoC 容器是用于依赖关系注入的通用框架。

## <a name="what-is-dependency-injection"></a>什么是依赖项注入？

如果已熟悉依赖项注入，请跳过此部分。

*依赖关系注入*（DI）是一种模式，其中对象不负责创建其自身的依赖项。 下面是一个用于鼓励 DI 的简单示例。 假设你有一个需要记录消息的对象。 您可以定义日志记录接口：

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

在对象中，可以创建日志消息 `ILogger`：

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

这可行，但并不是最佳设计。 如果要将 `FileLogger` 替换为其他 `ILogger` 实现，则必须修改 `SomeComponent`。 Supposing 有很多其他对象使用 `FileLogger`，你将需要更改所有这些对象。 或者，如果您决定将 `FileLogger` 为单一实例，则还需要在整个应用程序中进行更改。

更好的方法是将 `ILogger` "注入" 对象（例如，通过使用构造函数参数）：

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

现在，对象不负责选择要使用的 `ILogger`。 可以切换 `ILogger` 实现，而无需更改依赖于它的对象。

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

此模式称为 "[构造函数注入](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)"。 另一种模式是 setter 注入，可通过 setter 方法或属性设置依赖关系。

## <a name="simple-dependency-injection-in-signalr"></a>SignalR 中的简单依赖关系注入

请考虑通过[SignalR 教程入门](../getting-started/tutorial-getting-started-with-signalr.md)的聊天应用程序。 下面是该应用程序的中心类：

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

假设你想要在发送聊天消息前将其存储在服务器上。 您可以定义一个用于提取此功能的接口，并使用 DI 将接口注入到 `ChatHub` 类中。

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

唯一的问题是 SignalR 应用程序不会直接创建集线器;SignalR 会为你创建它们。 默认情况下，SignalR 需要一个 hub 类具有无参数的构造函数。 不过，您可以轻松地注册一个函数来创建集线器实例，并使用此函数来执行 DI。 通过调用**GlobalHost**注册该函数。

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

现在，SignalR 将在需要创建 `ChatHub` 实例时调用此匿名函数。

## <a name="ioc-containers"></a>IoC 容器

对于简单的情况，上面的代码是正确的。 但你仍必须编写以下内容：

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

在具有许多依赖项的复杂应用程序中，你可能需要编写大量此 "布线" 代码。 此代码很难维护，尤其是在嵌套依赖项的情况下。 它也很难进行单元测试。

一种解决方法是使用 IoC 容器。 IoC 容器是负责管理依赖项的软件组件。使用容器注册类型，然后使用容器来创建对象。 容器自动找出依赖关系。 许多 IoC 容器还允许您控制对象生存期和范围等任务。

> [!NOTE]
> "IoC" 代表 "控制反转"，这是一个框架对应用程序代码进行调用的常规模式。 IoC 容器为你构造对象，这会 "反转" 正常的控制流。

## <a name="using-ioc-containers-in-signalr"></a>在 SignalR 中使用 IoC 容器

聊天应用程序可能太简单，无法从 IoC 容器中获益。 我们来看看[StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample)示例。

StockTicker 示例定义了两个主要类：

- `StockTickerHub`：用于管理客户端连接的中心类。
- `StockTicker`：保存股票价格并定期更新它们的单独。

`StockTickerHub` 保存对 `StockTicker` 单一实例的引用，而 `StockTicker` 保留对 `StockTickerHub`的**IHubConnectionContext**的引用。 它使用此接口与 `StockTickerHub` 实例通信。 （有关详细信息，请参阅[Server 广播网 with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md)。）

我们可以使用 IoC 容器解开这些依赖项。 首先，让我们来简化 `StockTickerHub` 和 `StockTicker` 类。 在下面的代码中，我注释掉了不需要的部分。

从 `StockTickerHub`中移除无参数的构造函数。 相反，我们将始终使用 DI 来创建中心。

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

对于 StockTicker，删除单一实例。 稍后，我们将使用 IoC 容器来控制 StockTicker 生存期。 此外，请使构造函数成为公共构造函数。

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

接下来，我们可以通过创建 `StockTicker`的接口来重构代码。 我们将使用此接口从 `StockTicker` 类中分离 `StockTickerHub`。

Visual Studio 可轻松实现这种重构。 打开文件 "StockTicker.cs"，右键单击 `StockTicker` 类声明，然后选择 "**重构**..."**提取接口**。

![](dependency-injection/_static/image1.png)

在 "**提取接口**" 对话框中，单击 "**全选**"。 保留其他默认值。 单击“确定”。

![](dependency-injection/_static/image2.png)

Visual Studio 将创建一个名为 `IStockTicker`的新接口，还会将 `StockTicker` 更改为从 `IStockTicker`派生。

打开文件 "IStockTicker.cs"，并将接口更改为 "**公共**"。

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

在 `StockTickerHub` 类中，将 `StockTicker` 的两个实例更改为 `IStockTicker`：

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

不一定要创建 `IStockTicker` 接口，但我希望显示 DI 如何帮助减少应用程序中组件之间的耦合。

## <a name="add-the-ninject-library"></a>添加 Ninject 库

.NET 有许多开源 IoC 容器。 在本教程中，我将使用[Ninject](http://www.ninject.org/)。 （其他常用库包括[城堡 Windsor](http://www.castleproject.org/)、 [Spring.Net](http://www.springframework.net/)、 [Autofac](https://code.google.com/p/autofac/)、 [Unity](https://github.com/unitycontainer/unity)和[StructureMap](http://docs.structuremap.net)。）

使用 NuGet 包管理器安装[Ninject 库](https://nuget.org/packages/Ninject/3.0.1.10)。 在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器** > **程序包管理器控制台**"。 在“Package Manager Console”窗口中，输入以下命令：

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a>替换 SignalR 依赖关系解析程序

若要在 SignalR 中使用 Ninject，请创建从**DefaultDependencyResolver**派生的类。

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

此类将重写**DefaultDependencyResolver**的**GetService**和**GetServices**方法。 SignalR 调用这些方法在运行时创建各种对象，包括中心实例，以及由 SignalR 在内部使用的各种服务。

- **GetService**方法创建类型的单个实例。 重写此方法，以调用 Ninject 内核的**TryGet**方法。 如果该方法返回 null，则回退到默认的冲突解决程序。
- **GetServices**方法创建指定类型的对象的集合。 重写此方法以将 Ninject 的结果与默认解析程序的结果连接。

## <a name="configure-ninject-bindings"></a>配置 Ninject 绑定

现在，我们将使用 Ninject 声明类型绑定。

打开应用程序的 Startup.cs 类（按照 `readme.txt`中的包说明手动创建，或通过向项目添加身份验证创建）。 在 `Startup.Configuration` 方法中，创建 Ninject 调用*内核*的 Ninject 容器。

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

创建自定义依赖关系解析程序的实例：

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

为 `IStockTicker` 创建绑定，如下所示：

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

此代码说明两个问题。 首先，每当应用程序需要 `IStockTicker`时，内核都应创建 `StockTicker`的实例。 其次，`StockTicker` 类应是创建为单一实例对象的。 Ninject 将创建一个对象实例，并为每个请求返回同一个实例。

创建**IHubConnectionContext**的绑定，如下所示：

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

此代码创建一个返回**IHubConnection**的匿名函数。 **WhenInjectedInto**方法告诉 Ninject 仅在创建 `IStockTicker` 实例时才使用此函数。 原因是 SignalR 在内部创建**IHubConnectionContext**实例，而我们不希望重写 SignalR 创建它们的方式。 此函数仅适用于我们的 `StockTicker` 类。

通过添加集线器配置将依赖关系解析程序传递到**MapSignalR**方法：

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

用新参数更新示例的 Startup 类中的 ConfigureSignalR 方法：

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

现在，SignalR 将使用**MapSignalR**中指定的冲突解决程序，而不是默认的冲突解决程序。

下面是 `Startup.Configuration`的完整代码列表。

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

若要在 Visual Studio 中运行 StockTicker 应用程序，请按 F5。 在浏览器窗口中，导航到 `http://localhost:*port*/SignalR.Sample/StockTicker.html`。

![](dependency-injection/_static/image3.png)

应用程序的功能与以前完全相同。 （有关说明，请参阅[使用 ASP.NET SignalR 进行服务器广播](../getting-started/tutorial-server-broadcast-with-signalr.md)。）我们尚未更改该行为;只是使代码更易于测试、维护和发展。
