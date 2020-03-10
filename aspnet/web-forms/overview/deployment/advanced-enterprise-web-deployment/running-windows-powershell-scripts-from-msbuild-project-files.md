---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: 从 MSBuild 项目文件中运行 Windows PowerShell 脚本 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在生成和部署过程中运行 Windows PowerShell 脚本。 你可以在本地运行脚本 (换而言之，在 b...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441446"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a>从 MSBuild 项目文件中运行 Windows PowerShell 脚本

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何在生成和部署过程中运行 Windows PowerShell 脚本。 你可以在本地（即在生成服务器上）或远程运行脚本，例如在目标 web 服务器或数据库服务器上运行。
> 
> 你可能想要运行部署后的 Windows PowerShell 脚本的原因有很多。 例如，你可能希望：
> 
> - 将自定义事件源添加到注册表。
> - 生成用于上传的文件系统目录。
> - 清理生成目录。
> - 将条目写入自定义日志文件。
> - 发送电子邮件邀请用户发送到新预配的 web 应用程序。
> - 创建具有适当权限的用户帐户。
> - 在 SQL Server 实例之间配置复制。
> 
> 本主题将说明如何从 Microsoft 生成引擎（MSBuild）项目文件中的自定义目标以本地方式或远程方式运行 Windows PowerShell 脚本。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

这些教程核心的部署方法基于[理解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)中所述的拆分项目文件方法，其中，生成过程由两个项目文件&#x2014;控制，其中一个包含适用于每个目标环境的生成说明，另一个包含特定于环境的生成和部署设置。 在生成时，特定于环境的项目文件将合并到环境无关的项目文件中，以形成一组完整的生成说明。

## <a name="task-overview"></a>任务概述

若要在自动或单步部署过程中运行 Windows PowerShell 脚本，需要完成以下高级任务：

- 将 Windows PowerShell 脚本添加到解决方案和源代码管理。
- 创建调用 Windows PowerShell 脚本的命令。
- 在命令中转义任何保留的 XML 字符。
- 在自定义 MSBuild 项目文件中创建一个目标，并使用**Exec**任务来运行命令。

本主题将演示如何执行这些过程。 本主题中的任务和演练假设你已熟悉 MSBuild 目标和属性，并且你了解如何使用自定义 MSBuild 项目文件来驱动生成和部署过程。 有关详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。

## <a name="creating-and-adding-windows-powershell-scripts"></a>创建和添加 Windows PowerShell 脚本

本主题中的任务使用名为**LogDeploy**的 Windows PowerShell 脚本示例，演示如何从 MSBuild 运行脚本。 **LogDeploy**脚本包含一个用于将单行条目写入日志文件的简单函数：

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

**LogDeploy**脚本接受两个参数。 第一个参数表示要向其中添加条目的日志文件的完整路径，第二个参数表示要在日志文件中记录的部署目标。 运行该脚本时，它会将行添加到日志文件中，格式如下：

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

若要使**LogDeploy**脚本可用于 MSBuild，需执行以下操作：

- 将脚本添加到源代码管理。
- 在 Visual Studio 2010 中将脚本添加到解决方案。

无论你是计划在生成服务器上运行脚本还是在远程计算机上运行脚本，都不需要使用解决方案内容部署脚本。 一种选择是将脚本添加到解决方案文件夹中。 在联系人管理器示例中，由于要在部署过程中使用 Windows PowerShell 脚本，因此将脚本添加到发布解决方案文件夹是有意义的。

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

解决方案文件夹的内容将以源材料的形式复制到生成服务器。 但是，它们不构成任何项目输出的任何部分。

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a>在生成服务器上执行 Windows PowerShell 脚本

在某些情况下，可能需要在生成项目的计算机上运行 Windows PowerShell 脚本。 例如，你可以使用 Windows PowerShell 脚本来清理生成文件夹，或将条目写入自定义日志文件。

就语法而言，从 MSBuild 项目文件中运行 Windows PowerShell 脚本与从常规命令提示符下运行 Windows PowerShell 脚本相同。 需要调用 ngen.exe 可执行文件，并使用 **–命令**开关提供 Windows powershell 要运行的命令。 （在 Windows PowerShell v2 中，你还可以使用 **-file**开关）。 此命令应采用以下格式：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

例如:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

如果脚本的路径包含空格，则需要将文件路径用单引号引起来，并在前面加上 "&" 符。 不能使用双引号，因为已使用双引号将命令括起来：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

从 MSBuild 调用此命令时还有一些其他注意事项。 首先，应包括 **–非交互式**标志，以确保脚本安静地执行。 接下来，应包含具有相应参数值的 **– set-executionpolicy**标志。 此参数指定 Windows PowerShell 将应用于脚本的执行策略，并允许你替代默认执行策略，这可能会阻止脚本的执行。 可以从以下参数值中进行选择：

- 如果值为 "**无限制**"，则将允许 Windows PowerShell 执行脚本，而不管脚本是否已签名。
- 如果值为**RemoteSigned** ，则 Windows PowerShell 将允许 Windows PowerShell 执行在本地计算机上创建的未签名脚本。 但是，必须对在其他位置创建的脚本进行签名。 （实际上，不太可能在生成服务器上本地创建 Windows PowerShell 脚本）。
- 值**AllSigned**将允许 Windows PowerShell 仅执行签名的脚本。

默认的执行策略受到**限制**，这会阻止 Windows PowerShell 运行任何脚本文件。

最后，需要对 Windows PowerShell 命令中出现的任何保留的 XML 字符进行转义：

- 将单引号替换 **&amp;**
- 用 **&amp;** 替换双引号
- 将 & 替换 **&amp;amp;**

- 进行这些更改时，命令将如下所示：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

在自定义 MSBuild 项目文件中，可以创建一个新的目标，并使用**Exec**任务运行此命令：

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

在此示例中，请注意：

- 任何变量（如参数值和 Windows PowerShell 可执行文件的位置）都声明为 MSBuild 属性。
- 包括条件，使用户能够从命令行重写这些值。
- **MSDeployComputerName**属性在项目文件中的其他位置声明。

当你作为生成过程的一部分执行此目标时，Windows PowerShell 将运行你的命令并将日志条目写入指定的文件。

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a>在远程计算机上执行 Windows PowerShell 脚本

Windows PowerShell 可以通过[Windows 远程管理](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx)（WinRM）在远程计算机上运行脚本。 为此，需要使用[命令调用](https://technet.microsoft.com/library/dd347578.aspx)cmdlet。 这使你可以针对一台或多台远程计算机执行脚本，而无需将该脚本复制到远程计算机。 所有结果都将返回到运行脚本的本地计算机上。

> [!NOTE]
> 在使用**Invoke** cmdlet 在远程计算机上执行 Windows PowerShell 脚本之前，你需要配置 WinRM 侦听器以接受远程消息。 可以通过在远程计算机上运行命令**winrm quickconfig**来执行此操作。 有关详细信息，请参阅[Windows 远程管理的安装和配置](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)。

在 Windows PowerShell 窗口中，可以使用此语法在远程计算机上运行**LogDeploy**脚本：

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> 使用**Invoke 命令**运行脚本文件的方法有多种，但当需要提供参数值并使用空格管理路径时，这种方法最简单。

在命令提示符下运行此命令时，需要调用 Windows PowerShell 可执行文件，并使用 **– command**参数来提供说明：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

与前面一样，在从 MSBuild 运行命令时，需要提供一些附加的开关并转义任何保留的 XML 字符：

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

最后，与之前一样，你可以使用自定义 MSBuild 目标内的**Exec**任务来执行命令：

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

作为生成过程的一部分执行此目标时，Windows PowerShell 将在 **– computername**参数中指定的计算机上运行脚本。

## <a name="conclusion"></a>结束语

本主题介绍了如何从 MSBuild 项目文件中运行 Windows PowerShell 脚本。 您可以使用此方法在本地或远程计算机上运行 Windows PowerShell 脚本，作为自动或单步构建和部署过程的一部分。

## <a name="further-reading"></a>其他阅读材料

有关对 Windows PowerShell 脚本进行签名和管理执行策略的指南，请参阅[运行 Windows Powershell 脚本](https://technet.microsoft.com/library/ee176949.aspx)。 有关从远程计算机运行 Windows PowerShell 命令的指南，请参阅[运行远程命令](https://technet.microsoft.com/library/dd819505.aspx)。

有关使用自定义 MSBuild 项目文件来控制部署过程的详细信息，请参阅[了解项目文件](../web-deployment-in-the-enterprise/understanding-the-project-file.md)和[了解生成过程](../web-deployment-in-the-enterprise/understanding-the-build-process.md)。

> [!div class="step-by-step"]
> [上一页](taking-web-applications-offline-with-web-deploy.md)
> [下一页](troubleshooting-the-packaging-process.md)
