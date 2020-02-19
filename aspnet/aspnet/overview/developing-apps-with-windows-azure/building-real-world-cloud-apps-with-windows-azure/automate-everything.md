---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: 自动执行所有操作（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: e741a753a36ebdaefbff8eee0b38911785c716ac
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457162"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a>自动执行所有操作（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的简介，请参阅[第一章](introduction.md)。

我们所要做的前三种模式实际上适用于任何软件开发项目，尤其是云项目。 此模式与自动执行开发任务有关。 这是一个重要的主题，因为手动过程速度慢且容易出错;尽可能多地自动执行这些功能可帮助设置快速、可靠和敏捷的工作流。 这对于云开发而言是唯一重要的，因为你可以在本地环境中轻松地自动执行许多难于或无法自动执行的任务。 例如，可以设置整个测试环境，包括新的 web 服务器和后端 Vm、数据库、blob 存储（文件存储）、队列等。

## <a name="devops-workflow"></a>DevOps 工作流

您越来越多地听到了 "DevOps" 一词。 这一术语是在识别中开发的，你必须集成开发和操作任务才能有效地开发软件。 要启用的工作流类型为：你可以在其中开发应用、部署应用、从产品的生产使用情况中进行更改、根据你了解的内容进行更改，以及快速可靠地重复周期。

一些成功的云开发团队每天将多次部署到实时环境。 每2-3 个月使用 Azure 团队部署一个主要更新，但现在它每2-3 天发布少量更新，每2-3 周发布一次主发布。 进入该节奏确实有助于您迅速响应客户反馈。

要执行此操作，必须启用可重复的、可靠的、可预测的开发和部署周期，并缩短周期时间。

![DevOps 工作流](automate-everything/_static/image1.png)

换句话说，您对某个功能的想法以及客户使用该功能并提供反馈的时间段必须尽可能简短。 前三种模式（自动执行所有操作、源代码管理和持续集成和交付）都涉及到为了启用这种过程而建议使用的最佳实践。

## <a name="azure-management-scripts"></a>Azure 管理脚本

[本电子书简介介绍](introduction.md)了基于 web 的控制台，即 Azure 管理门户。 使用管理门户可以监视和管理已部署在 Azure 上的所有资源。 这是创建和删除服务（如 web 应用和 Vm）、配置这些服务、监视服务操作等的简单方法。 这是一个很好的工具，但使用它是一个手动过程。 如果你打算开发任何规模的生产应用程序，尤其是在团队环境中，建议你通过门户 UI 来学习和探索 Azure，然后自动执行要重复执行的过程。

几乎可以在管理门户或 Visual Studio 中手动完成的所有操作也可以通过调用 REST 管理 API 来完成。 可以使用[Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)编写脚本，也可以使用开源框架（如[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)）。 你还可以在 Mac 或 Linux 环境中使用 Bash 命令行工具。 Azure 已为所有这些不同的环境编写 Api 脚本，并具有[.net 管理 API](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) ，以防你想要编写代码而不是脚本。

对于 Fix It 应用，我们创建了一些 Windows PowerShell 脚本，这些脚本会自动执行创建测试环境的过程，并将项目部署到该环境，我们将查看这些脚本的一些内容。

## <a name="environment-creation-script"></a>环境创建脚本

我们将查看的第一个脚本名为*New-AzureWebsiteEnv*。 它创建一个 Azure 环境，你可以将 Fix It 应用部署到该环境以进行测试。 此脚本执行的主要任务如下：

- 创建 Web 应用。
- 创建存储帐户。 （Blob 和队列需要，如后面的章节中所示。）
- 创建 SQL 数据库服务器和两个数据库：应用程序数据库和成员资格数据库。
- 在 Azure 中存储用于访问存储帐户和数据库的设置。
- 创建将用于自动部署的设置文件。

### <a name="run-the-script"></a>运行脚本

> [!NOTE]
> 本章的此部分将显示脚本的示例，以及为运行脚本而输入的命令。 这是一个演示，不提供运行脚本所需的知识。 有关分步操作说明，请参阅[附录： Fix It 示例应用程序](the-fix-it-sample-application.md#deploybase)。

要运行管理 Azure 服务的 PowerShell 脚本，你必须安装 Azure PowerShell 控制台并将其配置为使用 Azure 订阅。 设置后，可以使用以下命令运行 Fix It 环境创建脚本：

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

`Name` 参数指定在创建数据库和存储帐户时要使用的名称，而 `SqlDatabasePassword` 参数指定将为 SQL 数据库创建的管理员帐户的密码。 您可以使用其他参数，以后我们将对此进行介绍。

![PowerShell 窗口](automate-everything/_static/image2.png)

脚本完成后，可以在管理门户中看到创建的内容。 你会发现两个数据库：

![数据库](automate-everything/_static/image3.png)

存储帐户：

![存储帐户](automate-everything/_static/image4.png)

和 web 应用：

![网站](automate-everything/_static/image5.png)

在 web 应用的 "**配置**" 选项卡上，可以看到它已为 Fix it 应用程序设置了存储帐户设置和 SQL 数据库连接字符串。

![appSettings 和 connectionStrings](automate-everything/_static/image6.png)

*自动化*文件夹现在还包含一个 *&lt;websitename&gt;.pubxml*文件。 此文件存储 MSBuild 将用于将应用程序部署到刚刚创建的 Azure 环境的设置。 例如：

[!code-xml[Main](automate-everything/samples/sample1.xml)]

如您所见，该脚本创建了一个完整的测试环境，整个过程大约在90秒内完成。

如果你的团队中的其他人想要创建测试环境，则可以直接运行该脚本。 它不仅快速，而且还可以确信他们使用的环境与你使用的环境相同。 如果每个人都使用管理门户 UI 手动设置，就不能完全相信这一点。

### <a name="a-look-at-the-scripts"></a>查看脚本

实际上有三个用于执行此操作的脚本。 从命令行调用一个命令，它会自动使用其他两个任务来执行某些任务：

- *New-AzureWebSiteEnv*是主要脚本。

    - *New-AzureStorage*创建存储帐户。
    - *New-AzureSql*将创建数据库。

### <a name="parameters-in-the-main-script"></a>主脚本中的参数

主脚本*New-AzureWebSiteEnv*定义了多个参数：

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

需要两个参数：

- 此脚本创建的 web 应用的名称。 （这也用于 URL： `<name>.azurewebsites.net`。）
- 脚本创建的数据库服务器的新管理用户的密码。

可选参数可用于指定数据中心位置（默认为 "美国西部"）、数据库服务器管理员名称（默认为 "dbuser"）和数据库服务器的防火墙规则。

### <a name="create-the-web-app"></a>创建 Web 应用

脚本的第一件事就是通过调用 `New-AzureWebsite` cmdlet 创建 web 应用，并向其传递 web 应用名称和位置参数值：

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a>创建存储帐户

然后，主脚本运行*New-AzureStorage*脚本，并为存储帐户名称指定 " *&lt;websitename&gt;* 存储"，并为 web 应用指定相同的数据中心位置。

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

*New-AzureStorage*调用 `New-AzureStorageAccount` cmdlet 来创建存储帐户，并返回帐户名称和访问密钥值。 应用程序需要这些值才能访问存储帐户中的 blob 和队列。

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

您可能不需要始终创建新的存储帐户;可以通过添加参数来增强脚本，此参数可选择指示使用现有的存储帐户。

### <a name="create-the-databases"></a>创建数据库

然后，主脚本在设置默认数据库和防火墙规则名称后运行数据库创建脚本*New-AzureSql*：

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

数据库创建脚本检索 dev 计算机的 IP 地址并设置防火墙规则，以便 dev 计算机可以连接到服务器并对其进行管理。 然后，数据库创建脚本完成多个步骤以设置数据库：

- 使用 `New-AzureSqlDatabaseServer` cmdlet 创建服务器。

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- 创建防火墙规则，使开发计算机能够管理服务器并使 web 应用程序能够连接到该服务器。 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- 使用 `New-AzureSqlDatabaseServerContext` cmdlet 创建包括服务器名称和凭据的数据库上下文。

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    `New-PSCredentialFromPlainText` 是脚本中的一个函数，该函数调用 `ConvertTo-SecureString` cmdlet 来加密密码并返回 `PSCredential` 对象，这与 `Get-Credential` cmdlet 返回的类型相同。
- 使用 `New-AzureSqlDatabase` cmdlet 创建应用程序数据库和成员资格数据库。

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- 调用本地定义的函数以创建每个数据库的连接字符串。 应用程序将使用这些连接字符串访问数据库。 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    SQLAzureDatabaseConnectionString 是在脚本中定义的一个函数，该函数从提供给它的参数值创建连接字符串。

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- 返回一个哈希表，其中包含数据库服务器名称和连接字符串。

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

Fix It 应用使用单独的成员身份和应用程序数据库。 还可以将成员资格和应用程序数据放在单个数据库中。

### <a name="store-app-settings-and-connection-strings"></a>存储应用设置和连接字符串

Azure 提供了一项功能，使你能够存储设置和连接字符串，以便在尝试读取 web.config 文件中的 `appSettings` 或 `connectionStrings` 集合时自动覆盖返回到应用程序的内容。 这是在部署时应用 web.config[转换](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)的替代方法。 有关详细信息，请参阅本电子书后面的在[Azure 中存储敏感数据](source-control.md#appsettings)。

环境创建脚本将所有 `appSettings` 和 `connectionStrings` 值存储在 Azure 中，应用程序在 Azure 中运行时需要访问存储帐户和数据库。

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

[新 Relic](http://newrelic.com/)是一个遥测框架，在 "[监视和遥测](monitoring-and-telemetry.md)" 一章中演示。 环境创建脚本还会重启 web 应用，以确保它选取新的 Relic 设置。

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a>准备部署

在该过程结束时，环境创建脚本将调用两个函数来创建部署脚本将使用的文件。

其中一个函数将创建发布配置文件 *（&lt;websitename&gt;.pubxml*文件）。 此代码调用 Azure REST API 以获取发布设置，并将信息保存在 *.publishsettings*文件中。 然后，它将使用该文件中的信息以及模板文件（ *.pubxml*）来创建包含发布配置文件的 *.pubxml*文件。 此两步过程模拟您在 Visual Studio 中执行的操作：下载 *.publishsettings*文件并导入以创建发布配置文件。

另一个函数使用另一个模板文件（网站环境模板）创建*website-environment*文件，其中包含部署脚本将与 *.pubxml*文件一起使用的设置。

### <a name="troubleshooting-and-error-handling"></a>疑难解答和错误处理

脚本类似于程序：它们可能会失败，并且当用户需要了解失败和导致错误的原因时，它们也会失败。 出于此原因，环境创建脚本会将 `VerbosePreference` 变量的值从 `SilentlyContinue` 更改为 `Continue`，以便显示所有详细消息。 它还会将 `ErrorActionPreference` 变量的值从 `Continue` 更改为 `Stop`，以便即使在遇到非终止错误时，脚本也会停止：

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

在执行任何工作之前，该脚本会存储开始时间，以便它可以计算完成所用的时间：

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

工作完成后，该脚本将显示运行时间：

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

对于每个键操作，该脚本将编写详细消息，例如：

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a>部署脚本

*New-AzureWebsiteEnv*脚本在创建环境时执行的操作， *Publish-AzureWebsite*脚本用于部署应用程序。

部署脚本从环境创建脚本创建的*website-environment*文件中获取 web 应用的名称。

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

它从 *.publishsettings*文件中获取部署用户密码：

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

它执行生成和部署项目的[MSBuild](http://msbuildbook.com/)命令：

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

如果已在命令行中指定 `Launch` 参数，它将调用 `Show-AzureWebsite` cmdlet，以将默认浏览器打开到网站 URL。

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

可以使用如下命令运行部署脚本：

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

完成后，浏览器将打开，并在云中运行 `<websitename>.azurewebsites.net` URL 处运行的站点。

![修复部署到 Windows Azure 的 It 应用](automate-everything/_static/image7.png)

## <a name="summary"></a>总结

使用这些脚本，可以确信相同的步骤将始终使用相同的顺序执行。 这有助于确保团队中的每个开发人员不会错过某些事情，或在自己的计算机上部署自定义的内容，或将其部署到其他团队成员环境或生产环境中。

同样，可以通过使用可在 Linux 或 Mac 上运行的 REST API、Windows PowerShell 脚本、.NET 语言 API 或 Bash 实用程序，自动执行大多数可以在管理门户中执行的 Azure 管理功能。

在[下一章](source-control.md)中，我们将介绍源代码，并解释在源代码存储库中包含脚本非常重要的原因。

## <a name="resources"></a>资源

- [安装和配置适用于 Azure 的 Windows PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。 说明如何安装 Azure PowerShell cmdlet 以及如何在计算机上安装所需的证书，以便管理 Azure 帐户。 这是一个很好的入门教程，因为它还包含指向用于学习 PowerShell 本身的资源的链接。
- [Azure 脚本中心](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)。 用于开发管理 Azure 服务的脚本的资源的 WindowsAzure.com 门户，其中包含入门教程、cmdlet 参考文档和源代码以及示例脚本的链接
- [周末脚本编写：通过 Azure 和 PowerShell 入门](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)。 在专用于 Windows PowerShell 的博客中，这篇文章提供了有关使用 PowerShell 进行 Azure 管理功能的很好的介绍。
- [安装和配置 Azure 跨平台命令行界面](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。 适用于 Azure 脚本编写框架的入门教程，适用于 Mac 和 Linux 以及 Windows 系统。
- [下载 Azure sdk 和工具主题的命令行工具](https://azure.microsoft.com/downloads/)。 与适用于 Azure 的命令行工具相关的文档和下载的门户页。
- [使用 Azure 管理库和 .NET 使一切自动化](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。 Scott Hanselman 介绍了适用于 Azure 的 .NET 管理 API。
- [使用 Windows PowerShell 脚本发布到开发和测试环境](https://msdn.microsoft.com/library/azure/dn642480.aspx)。 介绍如何使用 Visual Studio 为 web 项目自动生成的发布脚本的 MSDN 文档。
- [PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)。 Visual Studio 扩展，在 Visual Studio 中为 Windows PowerShell 添加语言支持。

> [!div class="step-by-step"]
> [上一页](introduction.md)
> [下一页](source-control.md)
