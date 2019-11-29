---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署到测试 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 738318cce442fdc5d58dd1e4c992d4941be2487e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591241"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a>使用 Visual Studio 的 ASP.NET Web 部署：部署到测试

作者： [Tom Dykstra](https://github.com/tdykstra)

本系列教程演示如何使用 Visual Studio 2017 将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。

有关部署到 Azure 的当前版本，请参阅[在 azure 中创建 ASP.NET Core web 应用](/azure/app-service/app-service-web-get-started-dotnet)。

## <a name="overview"></a>概述

在本教程中，将 ASP.NET web 应用程序部署到本地计算机上的 Internet Information Server （IIS）。

通常，在开发应用程序时，在 Visual Studio 中运行应用程序并对其进行测试。 默认情况下，Visual Studio 2017 中的 web 应用程序项目将 IIS Express 用作开发 web 服务器。 IIS Express 的行为与 Visual Studio 开发服务器（也称为 Cassini）完全相同，Visual Studio 2017 默认情况下使用。 但是，开发 web 服务器的工作方式与 IIS 完全相同。 因此，应用可以在 Visual Studio 中正确运行和测试，但在将其部署到 IIS 时将失败。

可以通过两种方式可靠地测试应用程序：

1. 使用你稍后将应用程序部署到生产环境时将使用的相同过程，将你的应用程序部署到你的开发计算机上的 IIS。

   你可以将 Visual Studio 配置为在运行 web 项目时使用 IIS，但不会测试你的部署过程。 此方法验证你的部署过程，并且你的应用程序在 IIS 下正常运行。

2. 将应用程序部署到类似于生产环境的测试环境。 
 
   这些教程的生产环境是 Azure App Service 中的 Web 应用。 理想的测试环境是在 Azure 服务中创建的其他 web 应用。 尽管设置的方式与生产 web 应用相同，但只是将其用于测试。

选项2是最可靠的测试方法。 如果使用选项2，则不一定需要使用选项1。 但是，如果要部署到第三方托管提供商，则选项2可能不可行或开销较大，因此本教程系列将显示这两种方法。 [部署到生产环境](deploying-to-production.md)教程中提供了选项2的指南。

有关在 Visual Studio 中使用 web 服务器的详细信息，请参阅[Visual studio for ASP.NET Web 项目中的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](troubleshooting.md)。

## <a name="download-the-contoso-university-starter-project"></a>下载 Contoso 大学初学者项目

下载并安装 Contoso 大学 Visual Studio starter 解决方案和项目。 此解决方案包含已完成的教程。 

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a>安装 IIS

若要在开发计算机上部署到 IIS，请确认已安装 IIS 和 Web 部署。 默认情况下，Visual Studio 会安装 Web 部署，但 IIS 不包含在默认的 Windows 10、Windows 8 或 Windows 7 配置中。 如果已安装 IIS 并且默认应用程序池已设置为 .NET 4，请跳到[下一部分](#sqlexpress)。

1. 建议使用[Web 平台安装程序（WPI）](https://www.microsoft.com/web/downloads/platform.aspx)安装 IIS 和 Web 部署。 WPI 安装建议的 IIS 配置，其中包括 IIS 和 Web 部署先决条件（如有必要）。

   如果你已经安装了 IIS、Web 部署或任何所需的组件，则 WPI 仅安装缺少的内容。

   * 使用 Web 平台安装程序安装 IIS 和 Web 部署：
    
     ![使用 WPI 安装 IIS](deploying-to-iis/_static/image30.png)

     ![使用 WPI 安装 Web 部署](deploying-to-iis/_static/image31.png)

     你将看到指示将安装 IIS 7 的消息。 该链接适用于 Windows 8 中的 IIS 8;但对于 Windows 8 及更高版本，请执行以下步骤，确保安装了 ASP.NET 4.7：

   * 打开 **"控制面板"**  > **程序**" > "**程序和功能 "，**  > **启用或禁用 Windows 功能**。

   * 展开**Internet Information Services**、 **World Wide Web 服务**和**应用程序开发功能**。
   
   * 确认已选中 " **ASP.NET 4.7** "。

     ![选择 ASP.NET 4。7](deploying-to-iis/_static/image1a.png)

   * 确认已选择 "**万维网服务**和**IIS 管理控制台**"。 这会安装 IIS 和 IIS 管理器。
    
     ![选择 "万维网服务"](deploying-to-iis/_static/image24.png)    
  
   * 选择“确定”。 显示指示安装正在进行的对话框消息。

安装 IIS 后，请运行**Iis 管理器**以确保将 .NET Framework 版本4分配给默认应用程序池。

1. 按 WINDOWS + R 打开 "**运行**" 对话框。

   （在 Windows 8 或更高版本上，在 "**开始**" 页上输入 "运行"。 在 Windows 7 中，从 "**开始**" 菜单中选择 "**运行**"。 如果 "**开始**" 菜单中没有 "**运行**"，请右键单击任务栏，选择 "**属性**"，选择 "**开始" 菜单**选项卡，选择 "**自定义**"，然后选择 "**运行命令**"。）

2. 输入 "inetmgr"，然后选择 **"确定**"。

3. 在 "**连接**" 窗格中，展开服务器节点，然后选择 "**应用程序池**"。 如果将**DefaultAppPool**分配给 .net framework 版本4（如下图所示），请在 "**应用程序池**" 窗格中跳到下一部分。

   ![Inetmgr_showing_4. 0_app_pools](deploying-to-iis/_static/image5a.png)

4. 如果只看到两个应用程序池，并且两者都设置为 .NET Framework 2.0，请在 IIS 中安装 ASP.NET 4。

   对于 Windows 8 或更高版本，请参阅上一节说明，以确保已安装 ASP.NET 4.7，或参阅[如何在 windows 8 和 Windows Server 2012 上安装 ASP.NET 4.5](https://support.microsoft.com/kb/2736284)。 对于 Windows 7，通过右键单击 Windows "**开始**" 菜单中的 "**命令提示符**" 并选择 "以**管理员身份运行**"，打开 "命令提示符" 窗口。 运行[aspnet\_regiis](https://msdn.microsoft.com/library/k6h9cz8h.aspx) ，使用以下命令在 IIS 中安装 ASP.NET 4。 （在32位系统中，将 "Framework64" 替换为 "框架"。）

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   此命令为 .NET Framework 4 创建新的应用程序池，但默认应用程序池将保持设置为2.0。 正在将面向 .NET 4 的应用程序部署到该应用程序池，因此请将应用程序池更改为 .NET 4。

5. 如果关闭了**IIS 管理器**，请再次运行它，展开服务器节点，然后选择 "**应用程序池**"。

6. 在 "**应用程序池**" 窗格中，选择 " **DefaultAppPool**"。 在 "**操作**" 窗格中，选择 "**基本设置**"。

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. 在 "**编辑应用程序池**" 对话框中，将 " **.net clr 版本**" 更改为 " **.net clr 4.0.30319**"。 选择“确定”。

   ![Selecting_. NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

你现在可以将 web 应用程序发布到 IIS。 但首先要创建用于测试的数据库。

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a>安装 SQL Server Express

LocalDB 不适用于 IIS，因此测试环境必须安装 SQL Server Express。 如果使用的是 Visual Studio 2010 SQL Server Express，则默认情况下已安装该程序。 如果使用的是 Visual Studio 2012 或更高版本，请安装 SQL Server Express。

若要安装 SQL Server Express，请从下载中心下载并安装它[： Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express)。 

在 SQL Server 安装中心的第一页上，选择 "**新建 SQL Server 独立安装或向现有安装添加功能**"，并按照说明接受默认选择。 在安装向导中，接受默认设置。 有关安装选项的详细信息，请参阅安装[SQL Server 从安装向导（安装程序）](https://msdn.microsoft.com/library/ms143219.aspx)。

## <a name="create-sql-server-express-databases-for-the-test-environment"></a>为测试环境创建 SQL Server Express 数据库

Contoso 大学应用程序有两个数据库： 

1. 成员资格数据库 
2. 应用程序数据库 

您可以将这些数据库部署到两个不同的数据库或单个数据库。 组合它们会使数据库在它们之间的联接更为容易。 

如果要部署到第三方托管提供商，则托管计划还可能会为您提供组合的原因。 例如，提供程序可能会为多个数据库收取更多的费用，甚至可能甚至不允许多个数据库。

在本教程中，你将在测试环境中部署到两个数据库，并部署到过渡环境和生产环境中的一个数据库。

在 Visual Studio 的 "**视图**" 菜单中，选择 "**服务器资源管理器**" （visual Web Developer 中的**数据库资源管理器**）。 右键单击 "**数据连接**"，然后选择 "**新建 SQL Server 数据库**"。

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

在 "新建**SQL Server 数据库**" 对话框的 "**服务器名称**" 框中，输入 ".\SQLExpress"，在 "**新数据库名称**" 框中输入 "ContosoUniversity"。 选择“确定”。

![创建 aspnet-ContosoUniversity](deploying-to-iis/_static/image9.png)

按照相同的过程创建名为 `ContosoUniversity`的新 SQL Server Express School 数据库。

**服务器资源管理器**显示两个新数据库。

![服务器资源管理器中的新数据库](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a>为新数据库创建授予脚本

当应用程序在开发计算机上的 IIS 中运行时，应用程序将使用默认应用程序池的凭据来访问数据库。 但是，默认情况下，应用程序池没有打开数据库的权限。 这意味着需要运行脚本来授予该权限。 在本部分中，你将创建该脚本并稍后运行它，以确保应用程序在 IIS 中运行时可以打开数据库。

在文本编辑器中，将以下 SQL 命令复制到一个新文件中，并将其另存为*Grant .sql*。 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

在 Visual Studio 中，打开 Contoso 大学解决方案。 右键单击该解决方案（不是项目之一），然后选择 "**添加**"。 选择 "**现有项**"，浏览到*Grant*，然后将其打开。

> [!NOTE]
> 此脚本旨在与 SQL Server Express 2012 或更高版本以及在本教程中指定的 windows 10、Windows 8 或 Windows 7 中的 IIS 设置一起使用。 如果使用的是其他版本的 SQL Server 或 Windows，或者在计算机上以不同的方式设置 IIS，则可能需要对此脚本进行更改。 有关 SQL Server 脚本的详细信息，请参阅[SQL Server 联机丛书](https://go.microsoft.com/fwlink/?LinkId=132511)。

> [!NOTE] 
> **安全说明**此脚本向用户提供对在运行时访问数据库的 `db_owner` 权限，您将在生产环境中使用该权限。 在某些情况下，你可能想要指定具有仅用于部署的完整数据库架构更新权限的用户，并为运行时指定仅拥有读取和写入数据权限的其他用户。 有关详细信息，请参阅本教程后面的[查看自动的 Web.config 更改 Code First 迁移](#reviewingmigrations)。

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a>在应用程序数据库中运行 grant 脚本

你可以将发布配置文件配置为在部署期间在成员资格数据库中运行授予脚本，因为该数据库部署使用[dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing)提供程序。 在 Code First 迁移部署过程中无法运行脚本，这是部署应用程序数据库的方式。 这意味着在应用程序数据库中进行部署之前，必须手动运行该脚本。

1. 在 Visual Studio 中，打开之前创建的*Grant .sql*文件。

2. 选择 "**连接**"。 

    ![连接按钮](deploying-to-iis/_static/image11.png)

3. 在 "**连接到服务器**" 对话框中，输入 " *.\SQLExpress* " 作为**服务器名称**。 选择 "**连接**"。

4. 在 "数据库" 下拉列表中，选择 " **ContosoUniversity**"。 选择 "**执行**"。 

   ![](deploying-to-iis/_static/image12.png)

默认应用程序池标识现在在应用程序数据库中具有足够的权限，以便在应用程序运行时创建数据库表 Code First 迁移。

## <a name="publish-to-iis"></a>发布到 IIS

可以通过多种方式使用 Visual Studio 和 Web 部署部署到 IIS：

* 使用 Visual Studio 一键式发布。
* 从命令行发布。
* 创建部署包，并使用 IIS 管理器进行安装。 该包具有一个 .zip 文件，其中包含在 IIS 中安装站点所需的所有文件和元数据。
* 使用命令行创建部署包并进行安装。

在前面的教程中，设置 Visual Studio 以自动完成部署任务的过程适用于所有这些方法。 在这些教程中，你将使用前两种方法。 有关使用部署包的信息，请参阅在 Visual Studio 和 ASP.NET 的 Web 部署内容映射中[创建和安装 web 部署包来部署 web 应用程序](https://go.microsoft.com/fwlink/p/?LinkId=282413#package)。

在发布之前，请确保在管理员模式下运行 Visual Studio。 如果在标题栏中看不到 "**管理员**"，请关闭 Visual Studio。 在 Windows 8 （或更高版本 **）或**windows 7 "**开始**" 菜单中，右键单击 Visual Studio 图标，然后选择 "以**管理员身份运行**"。 只有在发布到本地计算机上的 IIS 时才需要管理员模式。

### <a name="create-the-publish-profile"></a>创建发布配置文件

1. 在**解决方案资源管理器**中，右键单击**ContosoUniversity**项目（而不是**ContosoUniversity**项目）。 选择“发布”。 此时将显示 "**发布**" 页。

2. 选择 "**新建配置文件**"。 此时将显示 "**选取发布目标**" 对话框。

3. 选择 " **IIS"、"FTP" 等**。选择 "**创建配置文件**"。 此时将显示**发布**向导。

   ![发布 Web 向导 "配置文件" 选项卡](deploying-to-iis/_static/image26.png)

4. 从 "**发布方法**" 下拉菜单中选择 " **Web 部署**"。

5. 对于 "**服务器**"，请输入*localhost*。

6. 对于 "**站点名称**"，输入*默认网站/ContosoUniversity*。

7. 对于 "**目标 URL**"，请输入 *http://localhost/ContosoUniversity* 。

   不需要 "**目标 URL** " 设置。 当 Visual Studio 完成应用程序的部署时，它会自动打开此 URL 的默认浏览器。 如果你不希望在部署后自动打开浏览器，请将此框留空。

8. 选择 "**验证连接**" 以验证设置是否正确，并且你可以连接到本地计算机上的 IIS。

   绿色复选标记将验证连接是否成功。

   ![发布 Web 向导连接选项卡](deploying-to-iis/_static/image27.png)

9. 选择 "**下一步**" 转到 "**设置**" 选项卡。

10. "**配置**" 下拉框指定要部署的生成配置。 将其设置为 "**发布**" 的默认值。 在本教程中不会部署调试版本。

11. 展开 "**文件发布选项**"。 选择 **"从应用程序中排除文件\_Data 文件夹**。

    在测试环境中，应用程序将访问在本地 SQL Server Express 实例中创建的数据库，而不是*应用\_Data*文件夹中的 .mdf 文件。

12. 在 "发布并**删除目标中的其他文件**" 复选框处于清除状态**时保留预编译**。

    !["设置" 选项卡中的文件发布选项](deploying-to-iis/_static/image15a.png)

    预编译是主要用于大站点的选项。 它可以在站点发布后第一次请求页面时减少启动时间。

    你不需要删除其他文件，因为这是首次部署，但目标文件夹中没有任何文件。

    > [!NOTE] 
    > 如果你选择 "**删除目标中的其他文件**" 以便向同一站点进行后续部署，请确保使用预览功能，以便在部署之前提前了解哪些文件将被删除。 预期的行为是，Web 部署会删除已在项目中删除的目标服务器上的文件。 但会比较源文件夹和目标文件夹下的整个文件夹结构;在某些情况下，Web 部署可能会删除不想删除的文件。
    > 
    > 例如，如果在将项目部署到根文件夹时在服务器上的子文件夹中有一个 web 应用程序，则该子文件夹将被删除。 你可能在 contoso.com 的主站点上有一个项目，另一个项目用于 contoso.com/blog 的博客。 博客应用程序位于子文件夹中。 如果您在部署主站点时选择了 "**删除目标位置的其他文件**"，则会删除该博客应用程序。
    > 
    > 对于另一个示例，应用\_Data 文件夹可能会意外删除。 某些数据库（如 SQL Server Compact）将数据库文件存储在应用\_Data 文件夹中。 初始部署后，你不想在后续部署中继续复制数据库文件，因此，你可以在 "包/发布 Web" 选项卡上选择 "**排除应用程序\_数据**"。执行此操作后，如果选择了 "**在目标上删除其他文件**"，则在下一次发布时，将删除数据库文件和应用\_Data 文件夹本身。

### <a name="configure-deployment-for-the-membership-database"></a>为成员资格数据库配置部署

以下步骤适用于对话框的 "**数据库**" 部分中的**DefaultConnection**数据库。

1. 在 "**远程连接字符串**" 框中，输入以下指向新 SQL Server Express 成员资格数据库的连接字符串。

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   部署过程会将此连接字符串放在部署的 Web.config 文件中，原因是选择了 "**在运行时使用此连接字符串**"。

    还可以从**服务器资源管理器**获取连接字符串。 在**服务器资源管理器**中，展开 "**数据连接**"，然后选择 **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity**数据库，然后从 "**属性**" 窗口复制**连接字符串**值。 该连接字符串将有一个可以删除的其他设置： `Pooling=False`。

2. 选择 "**更新数据库**"。

   这会导致在部署过程中在目标数据库中创建数据库架构。 在后续步骤中，你将指定你需要运行的其他脚本：一个用于授予对默认应用程序池的数据库访问权限，另一个用于部署数据。

3. 选择 "**配置数据库更新**"。
 
4. 在 "**配置数据库更新**" 对话框中，选择 "**添加 SQL 脚本**"。 导航到之前在解决方案文件夹中保存的*Grant .sql*脚本。

5. 重复此过程以添加*aspnet-data-dev*脚本。

   ![为成员资格数据库配置数据库更新](deploying-to-iis/_static/image16.png)

6. 选择“关闭”。

### <a name="configure-deployment-for-the-application-database"></a>为应用程序数据库配置部署

当 Visual Studio 检测到实体框架 `DbContext` 类时，它将在 "**数据库**" 部分创建一个具有 "**执行 Code First 迁移**" 复选框而不是 "**更新数据库**" 复选框的条目。 对于本教程，你将使用此复选框来指定 Code First 迁移部署。

在某些情况下，你可能正在使用 `DbContext` 数据库，但你想要使用 dbDacFx 提供程序而不是迁移来部署数据库。 在这种情况下，请参阅 MSDN 上的 ASP.NET Web 部署常见问题解答中的[如何实现部署 Code First 数据库（不迁移](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations)）。

以下步骤适用于对话框的 "**数据库**" 部分中的**SchoolContext**数据库。

1. 在 "**远程连接字符串**" 框中，输入以下指向新 SQL Server Express 应用程序数据库的连接字符串。

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   部署过程会将此连接字符串放在部署的 Web.config 文件中，原因是选择了 "**在运行时使用此连接字符串**"。

   你还可以从**服务器资源管理器**获取应用程序数据库连接字符串，其方式与获取成员资格数据库连接字符串的方式相同。

2. 选择 **"执行 Code First 迁移（在应用程序启动时运行）** 。

   此选项将导致部署过程配置部署的 Web.config 文件以指定 `MigrateDatabaseToLatestVersion` 初始值设定项。 当应用程序在部署后首次访问数据库时，此初始值设定项会将数据库自动更新到最新版本。

### <a name="configure-publish-profile-transforms"></a>配置发布配置文件转换

1. 选择“关闭”。 如果系统询问是否要保存更改，请选择 **"是"** 。

2. 在**解决方案资源管理器**中，展开 "**属性**"，然后展开**PublishProfiles**。

3. 右键单击*CustomProfile .pubxml*并将其重命名为 *.pubxml*。

4. 右键单击 *.pubxml*。 选择 "**添加配置转换**"。

   ![添加配置转换菜单](deploying-to-iis/_static/image17.png)

   Visual Studio 将创建*web.config*转换文件并将其打开。

5. 在*web.config*转换文件中，将以下代码插入到紧靠在开始配置标记之后。

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    使用测试发布配置文件时，此转换会将环境指示器设置为 "测试"。 在部署的站点中，你将看到 "Contoso 大学" H1 标题后面的 "（测试）"。

6. 保存并关闭文件。

7. 右键单击 " *web.config* " 文件，然后选择 "**预览转换**"，以确保编码的转换生成所需的更改。

    Web.config**预览**窗口显示了同时应用*web.config*转换和*web.config 转换的结果。 ""* 。

### <a name="preview-the-deployment-updates"></a>预览部署更新

1. 再次打开 "**发布 Web** " 向导（右键单击 ContosoUniversity 项目，选择 "**发布**"，然后选择 "**预览**"）。

2. 在 "**预览**" 对话框中，选择 "**开始预览**" 以查看要复制的文件的列表。 

   ![发布预览](deploying-to-iis/_static/image29.png)

   还可以选择 "**预览数据库**" 链接，查看将在成员资格数据库中运行的脚本。 （没有为 Code First 迁移部署运行脚本，因此应用程序数据库无需预览。）

3. 选择“发布”。

   如果 Visual Studio 未处于管理员模式，你可能会收到权限错误消息。 在这种情况下，请关闭 Visual Studio，在管理员模式下打开它，然后再次尝试发布。

   如果 Visual Studio 处于管理员模式下，则 "**输出**" 窗口将报告成功的生成和发布。

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   如果在 "发布配置文件**连接**" 选项卡上的 "**目标 URL** " 框中输入了 URL，浏览器会自动打开到计算机上 IIS 中运行的 Contoso 大学主页。

## <a name="test-in-the-test-environment"></a>测试环境中的测试

请注意，环境指示器显示 "（测试）"，而不是 "（开发）"，这表明环境指示器的*web.config 转换已*成功。

运行**讲师**页，验证 Code First 用指导员数据对数据库进行种子设定。 选择此页时，可能需要几分钟的时间才能加载，因为 Code First 会创建数据库，然后运行 `Seed` 方法。 （如果你在主页上，则不会执行此操作，因为应用程序尚未尝试访问数据库。）

选择 "**学生**" 选项卡，验证部署的数据库是否没有学生。

从 "**学生**" 菜单中选择 "**添加学生**"。 添加一个学生，然后在 "**学生**" 页中查看新学生。 这将验证是否可以成功写入数据库。

从**课程**菜单中，选择 "**更新信用**"。 **更新信用**页面需要管理员权限，因此将显示 "**登录**" 页。 输入先前创建的管理员帐户凭据（"admin" 和 "devpwd"）。 将显示 "**更新信用额度**" 页。 这将验证你在上一教程中创建的管理员帐户是否已正确部署到测试环境中。

验证*c:\inetpub\wwwroot\ContosoUniversity*文件夹中是否存在只包含占位符文件的*ELMAH*文件夹。

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a>查看自动 Code First 迁移的 web.config 更改

在 C:\inetpub\wwwroot\ContosoUniversity*中的已*部署应用程序中打开 web.config文件，并可以看到部署过程的配置 Code First 迁移将数据库自动更新到最新版本。

![](deploying-to-iis/_static/image21.png)

部署过程还为 Code First 迁移创建了一个新的连接字符串，以独占方式用于更新数据库架构：

![Database_Publish 连接字符串](deploying-to-iis/_static/image22.png)

使用此附加连接字符串，您可以为数据库架构更新指定一个用户帐户，并为应用程序数据访问指定不同的用户帐户。 例如，可以将**db\_所有者**角色分配给应用程序的 Code First 迁移和**db\_** 与**db\_datawriter**角色。 这是一种常见的深层防御模式，可防止应用程序中可能存在的恶意代码更改数据库架构。 （例如，这可能会在成功的 SQL 注入攻击中发生。）这些教程不使用这种模式。 若要在方案中实现此模式，请执行以下步骤：

1. 在 "**发布 Web** " 向导中的 "**设置**" 选项卡下，输入指定具有完整数据库架构更新权限的用户的连接字符串。 清除 "**在运行时使用此连接字符串**" 复选框。 在部署的 Web.config 文件中，这将成为 `DatabasePublish` 的连接字符串。

2. 为希望应用程序在运行时使用的连接字符串创建 web.config 文件转换。

## <a name="summary"></a>总结

现在，你已将应用程序部署到 IIS 开发计算机上，并在其中进行测试。

![测试中的主页](deploying-to-iis/_static/image23.png)

这会验证部署过程是否已将应用程序的内容复制到适当的位置（不包括你不想部署的文件），同时还会在部署过程中正确 Web 部署配置 IIS。 在下一教程中，您将运行一个查找尚未完成的部署任务的测试：设置 "*榆树 ah* " 文件夹的文件夹权限。

## <a name="more-information"></a>更多信息

有关在 Visual Studio 中运行 IIS 或 IIS Express 的信息，请参阅以下资源：

- [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 站点上的概述。
- Scott Guthrie 的博客[介绍 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) 。
- [Visual Studio 中用于 ASP.NET Web 项目的 Web 服务器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。
- [IIS 与 ASP.NET 站点上的 ASP.NET 开发服务器之间的核心差异](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)。

有关应用程序以中等信任模式运行时可能会出现的问题的信息，请参阅在 Rolla 站点的四个用户上[托管中等信任中的 ASP.NET 应用程序](http://www.4guysfromrolla.com/articles/100307-1.aspx)。

> [!div class="step-by-step"]
> [上一页](project-properties.md)
> [下一页](setting-folder-permissions.md)
