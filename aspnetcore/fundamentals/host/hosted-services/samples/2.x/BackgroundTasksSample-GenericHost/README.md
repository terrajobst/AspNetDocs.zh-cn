---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57056484"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a><span data-ttu-id="9aa4b-101">ASP.NET Core 后台任务示例（通用主机）</span><span class="sxs-lookup"><span data-stu-id="9aa4b-101">ASP.NET Core Background Tasks Sample (Generic Host)</span></span>

<span data-ttu-id="9aa4b-102">本示例演示如何使用 [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice)。</span><span class="sxs-lookup"><span data-stu-id="9aa4b-102">This sample illustrates the use of [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span></span> <span data-ttu-id="9aa4b-103">本示例演示了[在 ASP.NET Core 中使用托管服务实现后台任务](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services)主题中描述的功能。</span><span class="sxs-lookup"><span data-stu-id="9aa4b-103">This sample demonstrates the features described in the [Background tasks with hosted services in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="9aa4b-104">在 [Visual Studio Code](https://code.visualstudio.com/) 中运行示例时，将“.vscode/launch.json”中控制台配置的“控制台”值设置为 `externalTerminal` 或 `integratedTerminal`。</span><span class="sxs-lookup"><span data-stu-id="9aa4b-104">When running the sample in [Visual Studio Code](https://code.visualstudio.com/), set the **console** value of the console configuration in *.vscode/launch.json* to either `externalTerminal` or `integratedTerminal`.</span></span> <span data-ttu-id="9aa4b-105">使用 `internalConsole` 与应用对后台工作项进行排队所使用的控制台击键输入不兼容。</span><span class="sxs-lookup"><span data-stu-id="9aa4b-105">Use of the `internalConsole` is incompatible with console keystroke input that the app uses to enqueue background work items.</span></span>
