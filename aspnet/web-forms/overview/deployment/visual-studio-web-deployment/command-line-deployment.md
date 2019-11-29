---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 使用 Visual Studio 的 ASP.NET Web 部署：命令行部署 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634207"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a>使用 Visual Studio 的 ASP.NET Web 部署：命令行部署

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。

## <a name="overview"></a>概述

本教程演示如何从命令行调用 Visual Studio web 发布管道。 这对于以下情况非常有用：您希望在 Visual Studio 中[自动执行部署过程](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)，而不是在 Visual Studio 中手动执行此操作，通常使用[源代码版本控制系统](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)。

## <a name="make-a-change-to-deploy"></a>进行部署更改

当前 "关于" 页显示模板代码。

![带有模板代码的 "关于" 页](command-line-deployment/_static/image1.png)

你需要将其替换为显示学生注册摘要的代码。

打开*About*页，删除 `MainContent` `Content` 元素内的所有标记，并在其位置插入以下标记：

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

运行该项目并选择 "**关于**" 页。

![“关于”页面](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a>使用命令行部署到测试

你不会部署其他数据库更改，因此请对 ContosoUniversity 数据库禁用 dbDacFx 数据库部署。 打开 "**发布 Web** " 向导，并在三个发布配置文件中的每一个配置文件中，清除 "**设置**" 选项卡上的 "**更新数据库**" 复选框。

在 Windows 8 "开始" 页中，搜索**VS2012 的开发人员命令提示**。

右键单击**VS2012 开发人员命令提示的**图标，然后单击 "以**管理员身份运行**"。

在命令提示符下输入以下命令，将解决方案文件的路径替换为解决方案文件的路径：

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

MSBuild 生成解决方案并将其部署到测试环境。

![命令行输出](command-line-deployment/_static/image3.png)

打开浏览器并中转到 `http://localhost/ContosoUniversity`，然后单击 "**关于**" 页以验证部署是否成功。

如果尚未创建任何学生进行测试，你会在 "**学生正文统计信息**" 标题下看到一个空页面。 请访问 "**学生**" 页，单击 "**添加学生**" 并添加一些学生，然后返回到 "**关于**" 页查看学生统计信息。

![测试环境中的 "关于" 页](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a>密钥命令行选项

你输入的命令将解决方案文件路径和两个属性传递到 MSBuild：

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a>部署解决方案与部署单个项目

指定解决方案文件将导致生成解决方案中的所有项目。 如果解决方案中有多个 web 项目，则以下 MSBuild 行为适用：

- 在命令行上指定的属性将传递给每个项目。 因此，每个 web 项目都必须具有您指定的名称的发布配置文件。 如果指定 `/p:PublishProfile=Test`，则每个 web 项目必须具有名为*Test*的发布配置文件。
- 如果一个项目甚至没有生成，你可能会成功发布一个项目。 有关详细信息，请参阅 stackoverflow 线程[MSBuild with 两个包失败](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)。

如果指定单个项目而不是解决方案，则必须添加一个指定 Visual Studio 版本的参数。 如果使用的是 Visual Studio 2012，命令行将类似于以下示例：

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

Visual Studio 2010 的版本号为10.0。 有关详细信息，请参阅[Visual Studio 项目兼容性和](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx)Sayed Hashimi 的博客上的 VisualStudioVersion。

### <a name="specifying-the-publish-profile"></a>指定发布配置文件

可以按名称或 *.pubxml*文件的完整路径指定发布配置文件，如以下示例中所示：

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a>支持命令行发布的 Web 发布方法

对于命令行发布，支持三种发布方法：

- `MSDeploy`-使用 Web 部署发布。
- `Package`-通过创建 Web 部署包进行发布。 必须从创建包的 MSBuild 命令单独安装包。
- `FileSystem`-通过将文件复制到指定的文件夹来发布。

### <a name="specifying-the-build-configuration-and-platform"></a>指定生成配置和平台

必须在 Visual Studio 或命令行中设置生成配置和平台。 发布配置文件包含名为 `LastUsedBuildConfiguration` 和 `LastUsedPlatform`的属性，但您不能设置这些属性以确定项目的生成方式。 有关详细信息，请参阅 Sayed Hashimi 的博客上的[MSBuild：如何设置配置属性](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)。

## <a name="deploy-to-staging"></a>部署到过渡环境

若要部署到 Azure，必须将密码添加到命令行。 如果你在 Visual Studio 中的发布配置文件中保存了密码，则该密码将以加密形式存储在 *.pubxml*文件中。 当你执行命令行部署时，MSBuild 不会访问该文件，因此你必须在命令行参数中传递密码。

1. 从之前为暂存网站下载的 *.publishsettings*文件中复制所需的密码。 密码是 Web 部署 `publishProfile` 元素的 `userPWD` 属性的值。

    ![Web 部署密码](command-line-deployment/_static/image5.png)
2. 在 Windows 8 "开始" 页上，搜索 "**开发人员命令提示**"，然后单击图标以打开命令提示符。 （此时无需在管理员的情况下将其打开，因为你不会部署到本地计算机上的 IIS。）
3. 在命令提示符下输入以下命令，将解决方案文件的路径替换为您的解决方案文件的路径，并将密码替换为您的密码：

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    请注意，此命令行包含额外参数： `/p:AllowUntrustedCertificate=true`。 编写本教程时，必须在从命令行发布到 Azure 时设置 `AllowUntrustedCertificate` 属性。 发布此 bug 的修补程序后，你不需要该参数。
4. 打开浏览器并中转到过渡站点的 URL，然后单击 "**关于**" 页以验证部署是否成功。

    正如你之前在测试环境中看到的那样，你可能需要创建一些学生，才能在 "**关于**" 页上查看统计信息。

## <a name="deploy-to-production"></a>部署到生产环境

部署到生产环境的过程类似于过渡过程。

1. 从之前为生产网站下载的 *.publishsettings*文件中复制所需的密码。
2. 打开**VS2012 开发人员命令提示**。
3. 在命令提示符下输入以下命令，将解决方案文件的路径替换为您的解决方案文件的路径，并将密码替换为您的密码：

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    对于实际的生产站点，如果也存在数据库更改，则通常会在部署之前将*应用\_脱机*文件复制到站点，并在部署成功后将其删除。
4. 打开浏览器并中转到过渡站点的 URL，然后单击 "**关于**" 页以验证部署是否成功。

## <a name="summary"></a>总结

现在，你已使用命令行部署了一个应用程序更新。

![测试环境中的 "关于" 页](command-line-deployment/_static/image6.png)

在下一教程中，你将看到有关如何扩展 web 发布管道的示例。 此示例将演示如何部署项目中未包含的文件。

> [!div class="step-by-step"]
> [上一页](deploying-a-database-update.md)
> [下一页](deploying-extra-files.md)
