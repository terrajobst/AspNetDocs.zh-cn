---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署到生产环境-7/12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: b83ab819-2b05-4776-b7b4-79ef78d457a5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
msc.type: authoredcontent
ms.openlocfilehash: db838633accdedd7c0693b126a007e254ca681e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458168"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-the-production-environment---7-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署到生产环境-7/12

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

在本教程中，将使用托管提供程序设置一个帐户，并使用 Visual Studio 一键式发布功能将 ASP.NET web 应用程序部署到生产环境。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="selecting-a-hosting-provider"></a>选择宿主提供程序

对于 Contoso 大学应用程序和本系列教程，您需要一个支持 ASP.NET 4 的提供程序和 Web 部署。 选择了特定的托管公司，以便教程能够说明部署到实时网站的完整体验。 每个托管公司都提供不同的功能，部署到其服务器的体验会略有不同。 但是，在整个过程中，本教程中所述的过程是典型过程。 本教程中使用的托管提供程序 Cytanium.com 是其中的一个可用的提供程序，在本教程中，其使用并不构成认可或建议。

当你准备选择自己的托管提供程序时，可以在 Microsoft.com/web 站点上的[提供程序库](https://www.microsoft.com/web/hosting)中比较功能和价格。

## <a name="creating-an-account"></a>创建帐户

在选定的提供程序中创建帐户。 如果对完整 SQL Server 数据库的支持增加了，则不需要在本教程中对其进行选择，但对于[迁移到 SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)本系列教程的教程，将需要它。

对于这些教程，无需注册新的域名。 你可以通过使用提供程序为站点分配的临时 URL 来测试以验证部署是否成功。

帐户创建完成后，通常会收到欢迎电子邮件，其中包含部署和管理站点所需的所有信息。 你的托管提供商发送的信息将类似于此处显示的信息。 发送到新帐户所有者的 Cytanium 欢迎电子邮件包含以下信息：

- 提供程序的 "控制面板" 站点的 URL，您可以在其中管理站点的设置。 你指定的 ID 和密码将包含在欢迎电子邮件的此部分中以供参考。 （这两个更改都已更改为此图的演示值。）

    [![Welcome_Email_Control_Panel_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image1.png)
- 默认 .NET Framework 版本和有关如何更改该版本的信息。 许多托管站点的默认值均为2.0，适用于面向 .NET Framework 2.0、3.0 或3.5 的 ASP.NET 应用程序。 但 Contoso 大学是 .NET Framework 4 应用程序，因此必须更改此设置。 （对于 ASP.NET 4.5 应用程序，应使用 .NET 4.0 设置。）

    [![Welcome_Email_Framework_Version](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image3.png)
- 可用于访问您的网站的临时 URL。 创建此帐户时，"contosouniversity.com" 已作为现有域名输入。 因此 `http://contosouniversity.com.vserver01.cytanium.com`临时 URL。

    [![Welcome_Email_Temporary_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image5.png)
- 有关如何设置数据库的信息，以及用于访问数据库的连接字符串：

    [![Welcome_Email_Database_Info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image7.png)
- 有关部署网站的工具和设置的信息。 （来自 Cytanium 的电子邮件也提到 WebMatrix，此处省略了此内容。）

    [![Welcome_Email_Deploy_info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image10.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image9.png)

## <a name="setting-the-net-framework-version"></a>设置 .NET Framework 版本

Cytanium 欢迎电子邮件包含一个链接，该链接指向有关如何更改 .NET Framework 版本的说明。 这些说明解释了可以通过 Cytanium 控制面板完成此操作。 其他提供商具有不同的控制面板站点，或者它们可能会指示您以不同的方式执行此操作。

中转到控制面板 URL。 用用户名和密码登录后，会看到 "控制面板"。

[![Cytanium_Control_Panel](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image11.png)

在 "**托管空间**" 框中，将指针放在 Web 图标上，并从菜单**中选择 "网站"** 。

[![Cytanium_Control_Panel_selecting_Web_Sites](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image13.png)

在 "**网站" 框中**，单击 " **contosouniversity.com** " （在创建帐户时使用的站点的名称）。

[![Cytanium_Control_Panel_selecting_contosouniversity](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image15.png)

在 "**网站属性**" 框中，选择 "**扩展**" 选项卡。

[![Cytanium_Control_Panel_Extensions_tab](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image17.png)

将 ASP.NET 从**2.0 集成管道**更改为**4.0 （集成管道）** ，然后单击 "**更新**"。

## <a name="publishing-to-the-hosting-provider"></a>发布到宿主提供程序

宿主提供商提供的欢迎电子邮件包含发布项目所需的所有设置，您可以手动将该信息输入到发布配置文件中。 但您将使用一种更简单、更不容易出错的方法来配置对提供程序的部署：您将下载一个 *.publishsettings*文件并将其导入到发布配置文件中。

在浏览器中，打开 Cytanium 控制面板并选择 " **web** "，然后选择 "网站" **。**

![选择网站的控制面板](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image19.png)

选择**contosouniversity.com**网站。

![选择 contosouniversity.com 的控制面板](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image20.png)

选择 " **Web 发布**" 选项卡。

![控制面板 Web 发布选项卡](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image21.png)

输入用户名和密码，创建 web 发布所使用的凭据。 您可以输入用于登录到控制面板的相同凭据。 单击“启用”。

![控制面板创建发布凭据](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image22.png)

单击 "**下载此网站的发布配置文件**"。

![控制面板下载发布配置文件](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image23.png)

当系统提示你打开或保存文件时，请保存该文件。

![保存发布配置文件](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image24.png)

在 Visual Studio**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后选择 "**发布**"。 将在 "**预览**" 选项卡上打开 "**发布 Web** " 对话框，其中选择了**测试**配置文件，因为这是你使用的最后一个配置文件。

选择 "**配置文件**" 选项卡，然后单击 "**导入**"。

![发布 Web 向导导入按钮](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image25.png)

在 "**导入发布设置**" 对话框中，选择已下载的 *.publishsettings*文件，然后单击 "**打开**"。 向导将前进到 "连接" 选项卡，其中填充了所有字段。

![发布 Web 向导连接选项卡](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image26.png)

.Publishsettings 文件在 "目标 URL" 框中放置站点的计划永久 URL，但如果尚未购买该域，请将值替换为临时 URL。 在此示例中，  *[http://contosouniversity.com.vserver01.cytanium.com](http://contosouniversity.com.vserver01.cytanium.com)了 URL。* 此框的唯一用途是指定浏览器在部署后成功自动打开的 URL。 如果将其留空，则唯一的结果是浏览器在部署后将不会自动启动。

单击 "**验证连接**"，验证设置是否正确以及是否可以连接到服务器。 如前文所述，绿色复选标记将验证连接是否成功。

单击 "验证连接" 时，可能会出现 "**证书错误**" 对话框。 如果执行此操作，请验证服务器名称是否与预期的相同。 如果是，请选择 "**为 Visual Studio 的未来会话保存此证书**"，然后单击 "**接受**"。 （此错误意味着宿主提供程序已选择避免为你要部署到的 URL 购买 SSL 证书。 如果你希望使用有效的证书建立安全连接，请与你的托管提供商联系。）

![证书错误](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image27.png)

单击 **“下一步”** 。

在 "**设置**" 选项卡的 "**数据库**" 部分中，输入为测试发布配置文件输入的相同值。 你将在下拉列表中找到所需的连接字符串。

- 在 SchoolContext 的 "连接字符串" 框中 **，** 选择 `Data Source=|DataDirectory|School-Prod.sdf`
- 在**SchoolContext**下，选择 "**应用 Code First 迁移**"。
- 在**DefaultConnection**的 "连接字符串" 框中，选择 `Data Source=|DataDirectory|aspnet-Prod.sdf`
- 在**DefaultConnection**下，清除 "**更新数据库**"。

![发布 Web 向导设置选项卡](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image28.png)

单击 **“下一步”** 。

在 "**预览**" 选项卡中，单击 "**开始预览**" 以查看要复制的文件的列表。 你会看到在本地计算机上部署到 IIS 时之前看到的相同列表。

在发布之前，更改配置文件的名称，以应用 Web.config 转换文件。 选择 "**配置文件**" 选项卡，然后单击 "**管理配置文件**"。

![发布 Web 向导管理配置文件](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image29.png)

在 "**编辑 Web 发布配置文件**" 对话框中，选择 "生产" 配置文件，单击 "**重命名**"，然后将配置文件名称更改为 "生产"。 然后单击 **“关闭”** 。

!["编辑 Web 发布配置文件" 对话框](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image30.png)

单击“发布”。

该应用程序将发布到宿主提供程序。 结果将显示在 "**输出**" 窗口中。

![部署后的输出窗口](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image31.png)

浏览器会自动打开到在 "**发布 Web** " 向导的 "**连接**" 选项卡上的 "**目标 url** " 框中输入的 url。 你会看到与在 Visual Studio 中运行站点时相同的主页，只不过标题栏中没有 "（测试）" 或 "（开发）" 环境指示器。 这表示*环境指示器 web.config*转换正常运行。

> [!NOTE]
> 如果标题中仍然出现 "（测试）"，请从 ContosoUniversity 项目中删除*obj*文件夹，并重新部署。 在该软件的预发布版本中，可以再次应用以前应用的转换文件（Web.config），尽管你使用的是生产配置文件。

[![Home_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image33.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image32.png)

在运行导致数据库访问的页面之前，请确保 Elmah 能够记录发生的任何错误。

## <a name="setting-folder-permissions-for-elmah"></a>设置 Elmah 的文件夹权限

在此系列的前一教程中，你必须确保应用程序对应用程序中的文件夹具有写入权限，其中 Elmah 存储错误日志文件。 当你在计算机上本地部署到 IIS 时，你可以手动设置这些权限。 在本部分中，你将了解如何在 Cytanium 中设置权限。 （某些宿主提供程序可能不允许你执行此操作; 这些提供程序可能会提供一个或多个具有写入权限的预定义文件夹。 在这种情况下，你必须修改应用程序以使用指定的文件夹。）

可以在 "Cytanium" 控制面板中设置文件夹权限。 请在 "控制面板 URL" 中，选择 "**文件管理器**"。

[![Cytanium_Control_Panel_with_File_Manager_selected](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image35.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image34.png)

在 "**文件管理器**" 框中，选择 " **contosouniversity.com** "，然后选择 " **wwwroot** " 以查看该应用程序的根文件夹。 单击 " **Elmah**" 旁边的挂锁图标。

[![Cytanium_Control_Panel_File_Manager_at_root_folder](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image37.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image36.png)

在 "**文件**/**文件夹权限**" 窗口中，选择**contosouniversity.com**的 "**读取**" 和 "**写入**" 复选框，然后单击 "**设置权限**"。

[![Cytanium_Control_Panel_File_Folder_Permissions_Elmah](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image39.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image38.png)

通过导致错误然后显示 Elmah 错误报告，确保 Elmah 对*elmah*文件夹具有写入访问权限。 请求一个无效的 URL，如*Studentsxxx*。 与前面一样，你会看到 " *GenericErrorPage* " 页。 单击 "**注销**" 链接，然后运行*Elmah. axd*。 首先获取**登录**页，验证*web.config*转换是否成功添加了 Elmah 授权。 登录后，将看到显示您刚刚引发的错误的报告。

[![Elmah. axd_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image41.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image40.png)

## <a name="testing-in-the-production-environment"></a>在生产环境中进行测试

运行 "**学生**" 页。 应用程序首次尝试访问 School 数据库，这会触发 Code First 迁移来创建数据库。 当页面在一段时间后显示时，显示没有学生。

[![Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image43.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image42.png)

运行 "**讲师**" 页，验证种子数据是否成功地在数据库中插入了指导员数据。

[![Instructors_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image45.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image44.png)

如您在测试环境中所做的那样，您需要验证数据库更新是否在生产环境中运行，但您通常不希望将测试数据输入到生产数据库中。 对于本教程，您将使用您在测试中使用的方法。 但在实际的应用程序中，您可能需要查找验证数据库更新是否成功的方法，而不会将测试数据引入到生产数据库中。 在某些应用程序中，添加内容并将其删除可能不切实际。

添加一个学生，然后查看您在 "**学生**" 页中输入的数据，以验证您可以更新数据库中的数据。

[![Add_Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image47.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image46.png)

[![Students_page_with_new_student_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image49.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image48.png)

从**课程**菜单中选择 "**更新信用**"，验证授权规则是否正常工作。 将显示 "**登录**" 页。 输入管理员帐户凭据，单击 "**登录**"，将显示 "**更新信用额度**" 页。

[![Log_In_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image51.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image50.png)

如果登录成功，将显示 "**更新信用额度**" 页。 这表示已成功部署 ASP.NET 成员资格数据库（具有单一管理员帐户）。

[![Update_Credits_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image53.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image52.png)

现在，你已成功部署并测试了你的网站，它可通过 Internet 公开使用。

## <a name="creating-a-more-reliable-test-environment"></a>创建更可靠的测试环境

如[部署到测试环境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教程中所述，最可靠的测试环境是托管提供商的第二个帐户，就像生产帐户一样。 这会比使用本地 IIS 作为测试环境更昂贵，因为你需要注册第二个托管帐户。 但如果它阻止生产站点错误或中断，则可能会确定这是一种成本。

创建和部署到测试帐户的大多数过程类似于你已部署到生产环境的过程：

- 创建 web.config*转换文件*。
- 在宿主提供程序中创建帐户。
- 创建新的发布配置文件，并将其部署到测试帐户。

### <a name="preventing-public-access-to-the-test-site"></a>阻止公共访问测试站点

测试帐户的一个重要考虑因素是它将在 Internet 上出现，但你不希望公开使用。 若要使站点保持私密，你可以使用以下一种或多种方法：

- 请与宿主提供商联系以设置防火墙规则，以便仅允许通过用于测试的 IP 地址访问测试站点。
- 伪装 URL，使其与公共网站的 URL 不相似。
- 使用*机器人 .txt*文件可确保搜索引擎不会对测试站点进行爬网，并在搜索结果中向其报告链接。

这三种方法中的第一种方法显然是最安全的，但本教程中不会介绍此方法的具体过程。 如果与托管提供商进行了安排，只允许您的 IP 地址浏览到测试帐户 URL，则理论上不必担心搜索引擎对其进行爬网。 但是，即使在这种情况下，在意外关闭防火墙规则的情况下，部署*机器人 .txt*文件也是一个不错的主意。

*机器人 .txt*文件将进入你的项目文件夹，并且应在其中包含以下文本：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/samples/sample1.cmd)]

"`User-agent`" 行通知搜索引擎文件中的规则适用于所有搜索引擎 web 爬网程序（机器人），`Disallow` 行指定不应爬网网站上的任何页面。

你可能希望搜索引擎为你的生产站点分类，因此你需要从生产部署中排除此文件。 若要执行此操作，请参阅[ASP.NET Web 应用程序项目部署常见问题](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)中的 **"能否从部署中排除特定文件或文件夹？"** 。 请确保只为生产发布配置文件指定排除项。

创建第二个托管帐户是一种使用不需要的测试环境的方法，但可能需要支付额外的费用。 在以下教程中，将继续使用 IIS 作为测试环境。

在下一教程中，你将更新应用程序代码并将更改部署到测试和生产环境中。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
