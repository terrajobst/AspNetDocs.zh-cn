---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: 单元测试 SignalR 应用程序 |Microsoft Docs
author: bradygaster
description: 本文介绍如何使用 SignalR 2.0 的单元测试功能。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467300"
---
# <a name="unit-testing-signalr-applications"></a>对 SignalR 应用程序进行单元测试

作者： [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文介绍如何使用 SignalR 2 的单元测试功能。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主题中使用的软件版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 版本2
>
>
>
> ## <a name="questions-and-comments"></a>问题和注释
>
> 请提供有关你喜欢本教程的方式的反馈，并在页面底部的评论中留下反馈。 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET SignalR 论坛](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a>对 SignalR 应用程序进行单元测试

可以使用 SignalR 2 中的单元测试功能为 SignalR 应用程序创建单元测试。 SignalR 2 包括[IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)接口，该接口可用于创建 mock 对象来模拟用于测试的中心方法。

在本部分中，将使用[XUnit.net](https://github.com/xunit/xunit)和[Moq](https://github.com/Moq/moq4)为[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)中创建的应用程序添加单元测试。

XUnit.net 将用于控制测试;Moq 将用于创建用于测试的[模拟](http://en.wikipedia.org/wiki/Mock_object)对象。 如果需要，可以使用其他模拟框架;[NSubstitute](http://nsubstitute.github.io/)也是一个不错的选择。 本教程演示如何通过两种方式设置 mock 对象：第一种方法是使用 `dynamic` 对象（在 .NET Framework 4 中引入），第二种方式是使用接口。

### <a name="contents"></a>内容

本教程包含以下部分。

- [通过动态进行单元测试](#dynamic)
- [按类型进行单元测试](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a>通过动态进行单元测试

在本部分中，将使用动态对象为[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)中创建的应用程序添加单元测试。

1. 为 Visual Studio 2013 安装[XUnit 运行程序扩展](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099)。
2. 请完成[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)，或从[MSDN 代码库](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)下载完成的应用程序。
3. 如果使用的是入门应用程序的下载版本，请打开 "**程序包管理器控制台**"，然后单击 "**还原**"，将 SignalR 包添加到项目。

    ![还原包](unit-testing-signalr-applications/_static/image1.png)
4. 将项目添加到单元测试的解决方案中。 在**解决方案资源管理器**中右键单击解决方案，然后选择 "**添加**"、"**新建项目 ...** "。在**C#** 节点下，选择 " **Windows** " 节点。 选择 **"类库"** 。 将新项目命名为 " **TestLibrary** "，然后单击 **"确定"** 。

    ![创建测试库](unit-testing-signalr-applications/_static/image2.png)
5. 将测试库项目中的引用添加到 SignalRChat 项目。 右键单击 " **TestLibrary** " 项目，然后选择 "**添加**"、"**引用 ...** "。选择 "**解决方案**" 节点下的 "**项目**" 节点，并选中 " **SignalRChat**"。 单击“确定”。

    ![添加项目引用](unit-testing-signalr-applications/_static/image3.png)
6. 将 SignalR、Moq 和 XUnit 包添加到**TestLibrary**项目。 在 "**包管理器控制台**" 中，将 "**默认项目**" 下拉列表设置为**TestLibrary**。 在控制台窗口中运行以下命令：

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![安装包](unit-testing-signalr-applications/_static/image4.png)
7. 创建测试文件。 右键单击 " **TestLibrary** " 项目，然后单击 "**添加 ...** "、"**类**"。 将新类命名为**Tests.cs**。
8. 将 Tests.cs 的内容替换为以下代码。

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    在上面的代码中，使用类型为[IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)的[Moq](https://github.com/Moq/moq4)库中的 `Mock` 对象创建测试客户端（在 SignalR 2.1 中，为类型参数分配 `dynamic`。）`IHubCallerConnectionContext` 接口是用于在客户端上调用方法的代理对象。 然后为模拟客户端定义 `broadcastMessage` 函数，使其可以由 `ChatHub` 类调用。 然后，测试引擎调用 `ChatHub` 类的 `Send` 方法，该方法又调用模拟 `broadcastMessage` 函数。
9. 按**F6**生成解决方案。
10. 运行单元测试。 在 Visual Studio 中选择 "**测试**"、" **Windows**"、"**测试资源管理器**"。 在 "测试资源管理器" 窗口中，右键单击**HubsAreMockableViaDynamic** ，然后选择 "**运行选定的测试**"。

    ![测试资源管理器](unit-testing-signalr-applications/_static/image5.png)
11. 通过检查 "测试资源管理器" 窗口中的下窗格来验证测试是否通过。 此窗口将显示测试通过。

    ![已通过测试](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a>按类型进行单元测试

在本部分中，将使用包含要测试的方法的接口，为[入门教程](../getting-started/tutorial-getting-started-with-signalr.md)中创建的应用程序添加测试。

1. 通过上述动态教程完成[单元测试](#dynamic)中的步骤1-7。
2. 将 Tests.cs 的内容替换为以下代码。

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    在上面的代码中，将创建一个接口，该接口用于定义测试引擎将为其创建模拟客户端的 `broadcastMessage` 方法的签名。 然后，使用[IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx)类型的 `Mock` 对象创建模拟客户端（在 SignalR 2.1 中，为类型参数分配 `dynamic`。）`IHubCallerConnectionContext` 接口是用于在客户端上调用方法的代理对象。

    然后，该测试创建 `ChatHub`的实例，然后创建 `broadcastMessage` 方法的模拟版本，该方法反过来通过在中心调用 `Send` 方法来调用。
3. 按**F6**生成解决方案。
4. 运行单元测试。 在 Visual Studio 中选择 "**测试**"、" **Windows**"、"**测试资源管理器**"。 在 "测试资源管理器" 窗口中，右键单击**HubsAreMockableViaDynamic** ，然后选择 "**运行选定的测试**"。

    ![测试资源管理器](unit-testing-signalr-applications/_static/image7.png)
5. 通过检查 "测试资源管理器" 窗口中的下窗格来验证测试是否通过。 此窗口将显示测试通过。

    ![已通过测试](unit-testing-signalr-applications/_static/image8.png)
