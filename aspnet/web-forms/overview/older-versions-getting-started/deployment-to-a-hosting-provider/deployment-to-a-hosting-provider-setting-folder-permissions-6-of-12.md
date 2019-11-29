---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：设置文件夹权限-6/12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: cd03a188-e947-4f55-9bda-b8bce201d8c6
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12
msc.type: authoredcontent
ms.openlocfilehash: 85a77a196cf3458bbb2e6308838a846936cd070b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633529"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-setting-folder-permissions---6-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：设置文件夹权限-6/12

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

在本教程中，您将设置已部署网站中的*Elmah*文件夹的文件夹权限，以便应用程序可以在该文件夹中创建日志文件。

使用 Visual Studio 开发服务器（Cassini）在 Visual Studio 中测试 web 应用程序时，应用程序将在您的标识下运行。 您很可能是开发计算机上的管理员，并且具有完全权限，可以对任何文件夹中的任何文件执行任何操作。 但是，当应用程序在 IIS 下运行时，它将在为该站点分配到的应用程序池定义的标识下运行。 这通常是一个具有有限权限的系统定义的帐户。 默认情况下，它对 web 应用程序的文件和文件夹具有 "读取" 和 "执行" 权限，但它没有写入访问权限。

如果你的应用程序创建或更新文件（这是 web 应用程序中的常见需求），这会成为一个问题。 在 Contoso 大学应用程序中，Elmah 在*elmah*文件夹中创建 XML 文件，以便保存有关错误的详细信息。 即使你不使用类似于 Elmah 的内容，你的网站也可能允许用户上传文件或执行其他将数据写入你站点中的文件夹的任务。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="testing-error-logging-and-reporting"></a>测试错误日志记录和报告

若要查看应用程序在 IIS 中不能正常运行的方式（尽管在 Visual Studio 中对其进行测试时也是如此），则可能导致由 Elmah 记录的错误，并打开 Elmah 错误日志以查看详细信息。 如果 Elmah 无法创建 XML 文件并存储错误详细信息，则会看到一个空错误报告。

打开浏览器并中转到 `http://localhost/ContosoUniversity`，然后请求无效的 URL，如*Studentsxxx*。 由于 Web.config 文件中的 `customErrors` 设置为 "RemoteOnly"，并且在本地运行 IIS，因此会看到系统生成的错误页，而不是*GenericErrorPage*页：

[![Error_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image2.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image1.png)

现在，请运行*Elmah*以查看错误报告。 你会看到一个空的错误日志页面，因为 Elmah 无法在*elmah*文件夹中创建 XML 文件：

[![Error_log_page_empty](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image4.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image3.png)

## <a name="setting-write-permission-on-the-elmah-folder"></a>针对 Elmah 文件夹设置写入权限

您可以手动设置文件夹权限，也可以将其设置为部署过程的自动部分。 将其设置为自动需要复杂的 MSBuild 代码，因此，在首次部署时仅需执行此操作，本教程仅介绍了如何手动执行此操作。 （有关如何创建此部分部署过程的信息，请参阅在 Sayed Hashimi 的博客上[设置对 Web 发布的文件夹权限](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx)。）

在**Windows 资源管理器**中，导航到*C:\inetpub\wwwroot\ContosoUniversity*。 右键单击 " *Elmah* " 文件夹，选择 "**属性**"，然后选择 "**安全**" 选项卡。

[![Elmah_folder_Properties_Security_tab](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image6.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image5.png)

（如果在 "**组或用户名**" 列表中看不到 " **DefaultAppPool** "，则可能使用了一些其他方法，而不是本教程中指定的方法在计算机上设置 IIS 和 ASP.NET 4。 在这种情况下，请查看分配给 Contoso 大学应用程序的应用程序池使用的标识，并向该标识授予写入权限。 请参阅本教程末尾的链接 "关于应用程序池标识"。

单击“编辑”。 在 " **Elmah 的权限**" 对话框中，选择 " **DefaultAppPool**"，然后选中 "**允许**" 列中的 "**写入**" 复选框。

[![Permissions_for_Elmah_dialog_box](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image8.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image7.png)

在两个对话框中单击 **"确定"** 。

## <a name="retesting-error-logging-and-reporting"></a>重新测试错误日志记录和报告

通过相同方式（请求错误的 URL）再次导致错误的测试，并运行 "**错误日志**" 页。 这次，此错误将显示在该页上。

[![Elmah_Error_Log_page_Test](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image10.png)](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12/_static/image9.png)

你还需要对*应用\_Data*文件夹的写权限，因为该文件夹中已 SQL Server Compact 数据库文件，并且你希望能够更新这些数据库中的数据。 但是，在这种情况下，您无需执行任何额外操作，因为部署过程会自动对*应用\_Data*文件夹设置写入权限。

你现在已经完成了在本地计算机上的 IIS 中正常工作所需的所有任务。 在下一教程中，你将通过将网站部署到托管提供程序来公开发布该站点。

## <a name="more-information"></a>详细信息

在此示例中，Elmah 无法保存日志文件的原因相当明显。 在出现问题的原因不太明显的情况下，可以使用 IIS 跟踪;请参阅 IIS.net 站点上的[使用 IIS 7 中的跟踪对失败请求进行故障排除](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)。

有关如何向应用程序池标识授予权限的详细信息，请参阅 IIS.net 站点上的[文件系统 acl 中](https://www.iis.net/learn/get-started/planning-for-security/secure-content-in-iis-through-file-system-acls)的[应用程序池标识](https://www.iis.net/learn/manage/configuring-security/application-pool-identities)和 IIS 中的安全内容。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
