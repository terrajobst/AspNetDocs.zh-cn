---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
title: 持续集成和持续交付（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: eaece9f5-f80c-428b-b771-5db66d275b7d
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
msc.type: authoredcontent
ms.openlocfilehash: 52c710053feca7872aa6fcc93c99bce90359f8fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74585883"
---
# <a name="continuous-integration-and-continuous-delivery-building-real-world-cloud-apps-with-azure"></a>持续集成和持续交付（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson]((https://twitter.com/RickAndMSFT))， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅[第一章](introduction.md)。

前两种建议的开发过程模式是[自动执行所有](automate-everything.md)操作和[源代码管理](source-control.md)，而第三个进程模式将它们进行组合。 持续集成（CI）是指当开发人员将代码签入到源存储库时，会自动触发生成。 持续交付（CD）进一步执行此步骤：在成功完成生成和自动单元测试后，会自动将应用程序部署到可执行更深入的测试的环境。

利用云，你可以最大程度地减少维护测试环境所需的成本，因为你只需在使用环境资源时为其付费。 您的 CD 过程可以在需要时设置测试环境，您可以在完成测试后关闭该环境。

## <a name="continuous-integration-and-continuous-delivery-workflow"></a>持续集成和持续交付工作流

通常，我们建议你在开发和过渡环境中持续交付。 大多数团队甚至在 Microsoft，都需要手动审查和批准生产部署过程。 对于生产部署，你可能希望在开发团队的关键人员可用于支持或在低流量期间进行操作。 但不能防止完全自动执行开发和测试环境，使开发人员需要做的就是检查更改，并为验收测试设置环境。

[Microsoft 模式和实践电子书中关于持续交付](https://aka.ms/ReleasePipeline)的下图展示了典型的工作流。 单击图像，在其原始上下文中查看其完整大小。

[![持续交付工作流](continuous-integration-and-continuous-delivery/_static/image1.png)](https://msdn.microsoft.com/library/dn449955.aspx)

## <a name="how-the-cloud-enables-cost-effective-ci-and-cd"></a>云如何启用经济高效的 CI 和 CD

在 Azure 中自动执行这些过程很简单。 由于你在云中运行一切，因此你无需为你的生成或测试环境购买或管理服务器。 您无需等待服务器可用于进行测试。 对于您的每个内部版本，你可以使用自动化脚本在 Azure 中启动一个测试环境，对其运行验收测试或更深入的测试，然后在你完成此操作时将其关闭。 如果你只是在2小时或8小时或一天内运行该服务器，则必须为该服务器支付多少钱，因为你只需为计算机实际运行的时间付费。 例如，如果您从免费级别向上一级，则 Fix it 应用程序所需的环境基本上的成本大约为每小时1美分。 在一个月中，如果每次只运行一次环境，则测试环境的成本可能低于在 Starbucks 购买的 latte。

## <a name="azure-devops-services"></a>Azure DevOps Services 

Azure DevOps Services 提供了许多功能，可帮助你从规划到部署的应用程序开发。

- 它支持 Git （分布式）和 TFVC （集中式）的源代码管理。
- 它提供弹性生成服务，这意味着它会在需要时动态创建生成服务器，并在完成时将其关闭。 当有人签入源代码更改时，你可以自动启动生成，而无需为大多数时间处于空闲状态的生成服务器分配和付费。 只要不超过一定数量的生成，生成服务就是免费的。 如果预计会生成大量的生成，则可以为保留生成服务器额外付费。
- 它支持向 Azure 持续交付。
- 它支持自动负载测试。 负载测试对于云应用非常重要，但通常会被忽略，直到其过迟。 负载测试模拟成千上万个用户对应用程序的大量使用，使你能够在将应用程序发布到生产环境之前查找瓶颈并提高吞吐量。
- 它支持团队聊天室协作，从而促进小型 agile 团队的实时通信和协作。
- 它支持敏捷项目管理。

有关 Azure DevOps Services 的持续集成和交付功能的详细信息，请参阅[Azure DevOps 文档](/azure/devops/index)。

如果你正在寻找关键项目管理、团队协作和源代码管理解决方案，请查看 Azure DevOps Services。 注册[Azure DevOps Services](https://dev.azure.com/)。

## <a name="summary"></a>总结

前三种云开发模式已经介绍了如何实现一个可重复、可靠、可预测的开发过程，时间较短。 [下一章](web-development-best-practices.md)将介绍体系结构和编码模式。

## <a name="resources"></a>资源

有关详细信息，请参阅[在 Azure App Service 中部署 web 应用](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)。

另请参阅以下资源：

- [使用 Team Foundation Server 2012 构建发布管道](https://aka.ms/ReleasePipeline)。 电子书、动手实验和 Microsoft 模式和实践的示例代码提供了持续交付的深入介绍。 介绍 Visual Studio 实验室管理和 Visual Studio Release Management 的用法。
- [ALM Rangers DevOps 工具和指南](https://aka.ms/vsarsolutions/)。 ALM Rangers 引入了 DevOps 工作台示例伴随解决方案，并与 &amp; 实践手册*使用 TFS 2012 构建发布管道*的模式进行协作，这是一种非常好的方法，可以开始了解适用于 tfs 2012 的 DevOps &amp; Release Management 的概念并开始使用轮胎。 本指南演示如何生成一次并部署到多个环境。
- [通过 Visual Studio 2012 对持续交付进行测试](https://msdn.microsoft.com/library/jj159345.aspx)。 Microsoft 模式和实践的电子书介绍了如何将自动测试与持续交付集成。
- [WindowsAzureDeploymentTracker](https://github.com/RyanTBerry/WindowsAzureDeploymentTracker)。 旨在从 TFS 捕获生成（基于标签）、生成、打包、允许 DevOps 角色中的用户配置其特定方面并将其推送到 Azure 的工具的源代码。 此工具将跟踪部署过程，以便能够将操作 "回滚" 到以前部署的版本。 该工具没有外部依赖关系，可使用 TFS Api 和 Azure SDK 独立运行。
- [持续交付：通过生成、测试和部署自动化实现可靠的软件发布](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1377126361)。 按 Jez humble 比较简陋的书籍。
- [发布！设计和部署生产就绪软件](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)。 Nygard 的书籍。

> [!div class="step-by-step"]
> [上一页](source-control.md)
> [下一页](web-development-best-practices.md)
