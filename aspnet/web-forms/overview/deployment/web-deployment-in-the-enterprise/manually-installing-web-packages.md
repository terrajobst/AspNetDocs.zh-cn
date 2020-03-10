---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: 手动安装 Web 包 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何在 Internet Information Services （IIS）中手动导入 web 部署包。 本主题介绍如何生成和打包 Web Applicati 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: f778549d3e26989a2e71ef21171adec521842729
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514886"
---
# <a name="manually-installing-web-packages"></a>手动安装 Web 程序包

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何在 Internet Information Services （IIS）中手动导入 web 部署包。
> 
> "[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)" 一文介绍了如何将 IIS Web 部署工具（Web 部署）与 Microsoft 生成引擎（MSBuild）和 Web 发布管道（WPP）结合使用，以便将 Web 应用程序项目打包到一个 zip 文件中。 此文件（通常称为 "web 部署包"，或简称为 "部署包"）包含 IIS 在 web 服务器上重新创建 web 应用程序所需的所有内容和配置信息。
> 
> 创建 web 部署包后，可以通过多种方式将其发布到 IIS 服务器。 在许多情况下，你将需要利用 MSBuild、WPP 和 Web 部署之间的集成点，以便在自动或单步构建和部署过程中以远程方式创建和安装 Web 包。 [部署 Web 包](deploying-web-packages.md)中介绍了此过程。 但这并不总是可行。 假设要将 web 应用程序部署到面向 Internet 的生产环境中。 出于安全原因，在外围网络（也称为 DMZ、外围安全区域和外围子网）中，此类生产环境在不同于生成服务器的子网中的防火墙的最小可能性。 在许多情况下，生产环境将位于单独的域或物理上隔离的网络上。
> 
> 在这些情况下，唯一的选择可能是将 web 包移植到目标服务器上，并手动将其导入到 IIS 中。 尽管此方法阻止自动部署，但它仍然是一种用于发布 web 应用程序&#x2014;的非常有效的方法，只需将单个 zip 文件复制到 web 服务器，然后使用向导引导你完成导入过程。

本主题介绍一系列教程的一部分，这些教程基于名为 Fabrikam，Inc. 的虚构公司的企业部署要求。本教程系列使用一个示例解决方案&#x2014;，该解决方案使用[联系人管理器解决方案](the-contact-manager-solution.md)&#x2014;来表示具有真实复杂性级别的 web 应用程序，包括 ASP.NET MVC 3 应用程序、Windows Communication Foundation （WCF）服务和数据库项目。

## <a name="task-overview"></a>任务概述

需要完成这些高级任务，才能将 web 部署包导入到 IIS：

- 使用 MSBuild 命令行、Team Build 或 Visual Studio 2010 创建 web 部署包。
- 将 web 包复制到目标 web 服务器。
- 使用 IIS 管理器中的 "导入应用程序包" 向导安装 web 包，并为变量（如连接字符串和服务终结点）提供值。

本主题将演示如何执行这些过程。 本主题中的任务和演练假定您已熟悉 web 包、Web 部署和 WPP 后面的概念。 有关详细信息，请参阅[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)。

> [!NOTE]
> 本主题最适用于为[Web 部署发布（脱机部署）配置 Web 服务器](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)，这说明了如何安装所需的组件和准备 IIS 网站以便导入包。

## <a name="create-a-web-deployment-package"></a>创建 Web 部署包

第一个任务是为要部署的 web 应用程序项目创建 web 部署包。 可以通过多种方式创建 web 包。

**方法1：使用 Visual Studio 在生成过程中创建包**

你可以配置 web 应用程序项目，以便在每次生成后通过项目属性页上的 "**打包/发布 web** " 选项卡创建一个 web 部署包。 此过程在[生成和打包 Web 应用程序项目](building-and-packaging-web-application-projects.md)中进行了介绍。

**方法2：使用 MSBuild 在生成过程中创建包**

如果通过使用 MSBuild 直接生成 web 应用程序项目（通过自定义 MSBuild 项目文件或从命令行生成），可以通过在命令中包括**DeployOnBuild = true**和**DeployTarget = package**属性，在生成过程中创建 web 部署包。 [了解生成过程](understanding-the-build-process.md)中介绍了此过程。

**方法3：在 Visual Studio 中按需创建包**

可在 Visual Studio 2010 中随时为 web 应用程序项目创建 web 部署包。 为此，请在 "**解决方案资源管理器**" 窗口中，右键单击 web 应用程序项目，然后单击 "**生成部署包**"。

![](manually-installing-web-packages/_static/image1.png)

**方法4：按需从命令行创建包**

可以通过在 web 应用程序项目中使用 MSBuild 调用**包**目标，从命令行创建 web 部署包。 命令应如下所示：

[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]

无论使用哪种方法，最终结果是相同的。 此 WPP 在你的 web 应用程序项目的输出文件夹中创建一个 web 部署包作为 zip 文件以及各种支持资源。

![](manually-installing-web-packages/_static/image2.png)

当你计划手动导入 web 包时，只需 zip 文件。 将此文件复制到目标 web 服务器，然后可以开始导入过程。

## <a name="import-a-web-package-into-iis"></a>将 Web 包导入 IIS

您可以使用下一个过程将本地文件系统中的 web 部署包导入到 IIS 网站。 在执行此过程之前，请确保：

- 已将 web 部署包复制到 web 服务器。
- 配置了用于托管应用程序的 IIS web 服务器。

有关将 IIS web 服务器配置为支持 web 部署包的详细信息，请参阅[配置 Web 服务器以进行 Web 部署发布（脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。

**使用 IIS 管理器导入 web 部署包**

1. 在 IIS 管理器的 "**连接**" 窗格中，右键单击您的 IIS 网站，指向 "**部署**"，然后单击 "**导入应用程序**"。

    ![](manually-installing-web-packages/_static/image3.png)
2. 在 "导入应用程序包" 向导的 "**选择包**" 页上，浏览到 web 部署包所在的位置，然后单击 "**下一步**"。
3. 在 "**选择包的内容**" 页上，清除任何不需要的内容，然后单击 "**下一步**"。

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > 在许多情况下，你可能不希望导入 web 部署包附带的所有内容。 例如，你可能不希望允许 Web 部署替换关联的数据库。  
    > "**授予权限**" 项设置目标文件系统的权限，以确保应用程序池标识可以访问存储网站内容的物理文件夹。 此外，将向 "匿名身份验证" 用户授予对文件夹的 "读取" 权限，以允许应用程序为多用途 Internet 邮件扩展（MIME）类型文件提供服务。 如果需要，你可以删除这些条目并手动配置权限。
4. 在 "**输入应用程序包信息**" 页上，提供所需的信息。

    ![](manually-installing-web-packages/_static/image5.png)
5. 当你创建 web 包时，WPP 会分析你的应用程序的配置文件，并检测任何变量（如连接字符串和服务终结点）。 这种情况下：

    1. **应用程序路径**是要在其中安装应用程序的 IIS 路径。 此设置对于 WPP 创建的所有部署包都是通用的。
    2. **ContactService 服务终结点地址**是应用程序用来与部署的 WCF 服务进行通信的地址。 此设置对应于*web.config*文件中的条目。
    3. 第一个**连接字符串**设置是 Web 部署应该用于部署与应用程序关联的数据库的连接字符串（在本例中为 ASP.NET 成员资格数据库）。 此设置对应于 Visual Studio 中的 "**包/发布 SQL** " 选项卡上的设置。
    4. 第二个**连接字符串**设置是在启动和运行应用程序时，应用程序将实际用于与数据库通信的连接字符串。 这对应于*web.config 文件中的连接*字符串条目。

        > [!NOTE]
        > 有关这些参数的来源的详细信息，请参阅[为 Web 包部署配置参数](configuring-parameters-for-web-package-deployment.md)。
6. 单击 **“下一步”** 。
7. 如果这不是您首次将应用程序部署到此网站，系统将提示您指定是否要在安装之前删除所有现有内容。 选择适合你的要求的选项，然后单击 "**下一步**"。

    ![](manually-installing-web-packages/_static/image6.png)
8. 当 IIS 完成包的安装后，单击 "**完成**"。

    ![](manually-installing-web-packages/_static/image7.png)

此时，已成功将 web 应用程序发布到 IIS。

## <a name="conclusion"></a>结束语

本主题介绍了如何使用 IIS 管理器将 web 部署包导入到 IIS 网站。 当安全或基础结构限制不可能或不希望进行远程部署时，这种 web 应用程序发布方法非常合适。

## <a name="further-reading"></a>其他阅读材料

有关如何配置 IIS web 服务器以支持手动导入 web 包的指南，请参阅[配置 Web 服务器以进行 Web 部署发布（脱机部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。 有关部署 web 包的更多一般指南，请参阅[演练：使用 Web 部署包部署 Web 应用程序项目（第1部分，共4部分）](https://msdn.microsoft.com/library/dd483479.aspx)。

> [!div class="step-by-step"]
> [上一页](creating-and-running-a-deployment-command-file.md)
