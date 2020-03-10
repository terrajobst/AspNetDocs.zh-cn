---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: 设置联系人管理器解决方案 |Microsoft Docs
author: jrjlee
description: 本主题介绍如何下载和配置 Contact Manager 解决方案，以在开发人员工作站上本地运行。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511160"
---
# <a name="setting-up-the-contact-manager-solution"></a>设置 Contact Manager 解决方案

作者： [Jason](https://github.com/jrjlee)

[下载 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主题介绍如何下载和配置 Contact Manager 解决方案，以在开发人员工作站上本地运行。

## <a name="system-requirements"></a>系统要求

若要在本地运行 Contact Manager 解决方案并执行本教程中所述的其他任务，你将需要在开发人员工作站上安装此软件：

- Visual Studio 2010 Service Pack 1、高级版或旗舰版
- Internet Information Services (IIS) 7.5 Express
- SQL Server Express 2008 R2
- IIS Web 部署工具（Web 部署）2.1 或更高版本
- ASP.NET 4.0
- ASP.NET MVC 3
- .NET Framework 4
- .NET Framework 3.5 SP1

除了 Visual Studio 2010，你可以通过[Web 平台安装程序](https://go.microsoft.com/?linkid=9805118)下载并安装所有这些产品和组件的最新版本。

## <a name="download-and-extract-the-solution"></a>下载并提取解决方案

你可以从[此处](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)的 MSDN 代码库下载联系人管理器示例应用程序。

## <a name="configure-and-run-the-solution"></a>配置和运行解决方案

若要在本地计算机上配置和运行 Contact Manager 解决方案，需要执行以下高级步骤：

1. 如果还没有，请创建一个启用了成员身份和角色管理功能的本地 ASP.NET 应用程序服务数据库。
2. 编辑*web.config*文件中的连接字符串以指向本地 SQL Server Express 实例。
3. 从 Visual Studio 2010 运行解决方案。

本部分的其余部分提供了有关如何完成上述每项任务的更多指导。

**创建应用程序服务数据库**

1. 打开 Visual Studio 2010 命令提示符。 为此，请在 "**开始**" 菜单上，指向 "**所有程序**"，依次单击**Microsoft Visual Studio 2010**"、" **Visual Studio Tools**"和" **Visual Studio 命令提示（2010）** "。
2. 在命令提示符下，键入以下命令，然后按 Enter：

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. 使用 **– C**开关为数据库服务器指定连接字符串。
    2. 使用 **– A**开关指定要添加到数据库中的应用程序服务功能。 在这种情况下， **m**表示你要添加对成员资格提供程序的支持， **r**表示你要添加对角色管理器的支持。
    3. 使用 **– d**开关指定你的应用程序服务数据库的名称。 如果省略此开关，实用工具将创建默认名称为**aspnetdb.mdf**的数据库。
3. 成功创建数据库后，命令提示符将显示一条确认消息。

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> 有关 aspnet\_regsql 实用工具的详细信息，请参阅[ASP.NET SQL Server 注册工具（aspnet\_regsql）](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx)。

下一步是确保 "联系人管理器" 解决方案中的连接字符串指向 SQL Server Express 的本地实例。

**更新连接字符串**

1. 在 Visual Studio 2010 中打开联系人管理器解决方案。
2. 在 "**解决方案资源管理器**" 窗口中，展开 " **ContactManager** " 项目，然后双击**web.config 节点。**

    > [!NOTE]
    > ContactManager 项目*包含两个 web.config 文件*。 需要编辑项目级文件。

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. 在**connectionStrings**元素中，验证名为**microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception**的连接字符串是否指向本地 ASP.NET 应用程序服务数据库。

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. 在 "**解决方案资源管理器**" 窗口中，展开 " **ContactManager** " 项目，然后双击**web.config 节点。**

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. 在**connectionStrings**元素中，在名为**ContactManagerContext**的连接字符串中，验证 "**数据源**" 属性是否设置为 SQL Server Express 的本地实例。 不需要更改连接字符串中的任何其他内容。

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. 保存所有打开的文件。

现在，你应该已准备好在本地计算机上运行 Contact Manager 解决方案。

> [!NOTE]
> 如果在未首先创建应用程序服务数据库的情况下执行这些步骤，则在您首次尝试创建用户时，ASP.NET 将创建该数据库。 但是，手动创建数据库可以更好地控制要支持的应用程序服务功能集。

**运行 Contact Manager 解决方案**

1. 在 Visual Studio 2010 中，按 F5。
2. Internet Explorer 启动并请求 Contact Manager ASP.NET MVC 3 应用程序的 URL。 默认情况下，应用程序显示 "**所有联系人**" 页。

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. 添加一些联系人，然后验证应用程序是否按预期方式工作。

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. 如果要将应用程序托管在其他端口上，请浏览到 `http://localhost:50114/Account/Register` （调整 URL）。 添加用户名、电子邮件地址和密码，并验证是否能够成功注册帐户。

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. 如果要将应用程序托管在其他端口上，请浏览到 `http://localhost:50114/Account/LogOn` （调整 URL）。 验证是否能够使用刚刚创建的帐户登录。

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. 关闭 Internet Explorer 以停止调试。

## <a name="conclusion"></a>结束语

此时，联系人管理器解决方案应完全配置为在本地计算机上运行。 在完成本教程中的其他主题时，可以使用该解决方案作为参考。

下一主题[了解项目文件](understanding-the-project-file.md)，说明如何使用联系人管理器解决方案中的自定义 Microsoft 生成引擎（MSBuild）项目文件来控制部署过程。

> [!div class="step-by-step"]
> [上一页](the-contact-manager-solution.md)
> [下一页](understanding-the-project-file.md)
