---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：迁移到 SQL Server-10 个，共12个 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462836"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：迁移到 SQL Server-10 （共12个）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

本教程演示如何从 SQL Server Compact 迁移到 SQL Server。 您可能想要这样做的一个原因是利用 SQL Server Compact 不支持的 SQL Server 功能，如存储过程、触发器、视图或复制。 有关 SQL Server Compact 和 SQL Server 之间的差异的详细信息，请参阅[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。

### <a name="sql-server-express-versus-full-sql-server-for-development"></a>用于开发的 SQL Server Express 与完全 SQL Server

一旦决定升级到 SQL Server，你可能希望在开发和测试环境中使用 SQL Server 或 SQL Server Express。 除了工具支持和数据库引擎功能中的差异外，SQL Server Compact 与 SQL Server 的其他版本之间提供程序实现之间的差异。 这些差异可能会导致相同的代码生成不同的结果。 因此，如果您决定将 SQL Server Compact 作为开发数据库，则应在每次部署到生产环境之前，在测试环境中全面测试您的站点 SQL Server 或 SQL Server Express。

与 SQL Server Compact 不同，SQL Server Express 实质上是相同的数据库引擎，并使用与完整 SQL Server 相同的 .NET 提供程序。 当你测试 SQL Server Express 时，你可以放心地获得与 SQL Server 相同的结果。 您可以将大多数相同的数据库工具与 SQL Server Express 一起使用，这些工具可用于 SQL Server （一个值得[SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)的值得注意的异常），并支持其他 SQL Server 功能，如存储过程、视图、触发器和复制。 （但是，您通常必须在生产网站中使用完整 SQL Server。 SQL Server Express 可以在共享的宿主环境中运行，但并不是针对此环境设计的，并且许多宿主提供程序不支持它。）

如果使用的是 Visual Studio 2012，通常会为开发环境选择 SQL Server Express LocalDB，因为这是 Visual Studio 默认安装的内容。 但是，LocalDB 在 IIS 中不起作用，因此对于测试环境，必须使用 SQL Server 或 SQL Server Express。

### <a name="combining-databases-versus-keeping-them-separate"></a>合并数据库，并将其保持独立

Contoso 大学应用程序有两个 SQL Server Compact 数据库：成员资格数据库（*aspnet*）和应用程序数据库（*School .sdf*）。 迁移时，可以将这些数据库迁移到两个不同的数据库或单个数据库。 你可能想要将它们组合在一起，以便于你的应用程序数据库和成员资格数据库之间进行数据库联接。 托管计划还可能会提供组合的原因。 例如，宿主提供程序可能会为多个数据库收取更多的费用，甚至可能甚至不允许多个数据库。 这就是本教程中使用的 Cytanium Lite 托管帐户，只允许单个 SQL Server 数据库。

在本教程中，你将以这种方式迁移两个数据库：

- 迁移到开发环境中的两个 LocalDB 数据库。
- 迁移到测试环境中的两个 SQL Server Express 数据库。
- 在生产环境中迁移到一个组合的完整 SQL Server 数据库。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="installing-sql-server-express"></a>安装 SQL Server Express

默认情况下，默认情况下，将使用 Visual Studio 2010 自动安装 SQL Server Express，但默认情况下它不与 Visual Studio 2012 一起安装。 若要安装 SQL Server 2012 Express，请单击以下链接

- [SQL Server Express 2012](https://www.microsoft.com/download/details.aspx?id=29062)

选择*简体中文/x64/sqlexpr.exe\_x64\_简体中文*或*简体中文/x86/sqlexpr.exe\_x86\_简体中文*，然后在安装向导中接受默认设置。 有关安装选项的详细信息，请参阅[从安装向导安装 SQL Server 2012 （安装程序）](https://msdn.microsoft.com/library/ms143219.aspx)。

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a>为测试环境创建 SQL Server Express 数据库

下一步是创建 ASP.NET 成员身份和 School 数据库。

从 "**视图**" 菜单中选择 "**服务器资源管理器**（Visual Web Developer 中的**数据库资源管理器**）"，然后右键单击 "**数据连接**"，然后选择 "**创建新的 SQL Server 数据库**"。

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

在 "新建**SQL Server 数据库**" 对话框的 "**服务器名称**" 框中，输入 ".\SQLExpress"，在 "**新数据库名称**" 框中输入 "aspnet-测试"，然后单击 **"确定**"。

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

按照相同的过程创建一个名为 "School Test" 的新 SQL Server Express School 数据库。

（你要将 "Test" 追加到这些数据库名称，因为稍后你将为开发环境创建每个数据库的另一个实例，并且你需要能够区分这两个数据库集。）

**服务器资源管理器**现在显示两个新数据库。

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a>为新数据库创建 Grant 脚本

当应用程序在开发计算机上的 IIS 中运行时，应用程序将通过使用默认应用程序池的凭据来访问数据库。 但是，默认情况下，应用程序池标识没有打开数据库的权限。 因此，你必须运行脚本来授予该权限。 在本部分中，将创建稍后要运行的脚本，以确保应用程序在 IIS 中运行时可以打开数据库。

在 "[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)的解决方案" 教程中创建的解决方案的*SolutionFiles*文件夹中，创建一个名为*Grant*.sql 的新 SQL 文件。 将以下 SQL 命令复制到该文件中，然后保存并关闭该文件：

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> 此脚本旨在与 SQL Server 2008 和 Windows 7 中的 IIS 设置一起使用，因为在本教程中指定了这些设置。 如果使用的是其他版本的 SQL Server 或 Windows，或者在计算机上以不同的方式设置 IIS，则可能需要对此脚本进行更改。 有关 SQL Server 脚本的详细信息，请参阅[SQL Server 联机丛书](https://go.microsoft.com/fwlink/?LinkId=132511)。

> [!NOTE] 
> 
> **安全说明**此脚本向 db\_所有者授予在运行时访问数据库的用户的权限，您将在生产环境中使用该权限。 在某些情况下，你可能想要指定具有仅用于部署的完整数据库架构更新权限的用户，并为运行时指定仅拥有读取和写入数据权限的其他用户。 有关详细信息，请参阅在[部署到 IIS 作为测试环境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)中查看**Code First 迁移的自动 web.config 更改**。

## <a name="configuring-database-deployment-for-the-test-environment"></a>为测试环境配置数据库部署

接下来，你将配置 Visual Studio，以便它将为每个数据库执行以下任务：

- 生成一个 SQL 脚本，该脚本在目标数据库中创建源数据库的结构（表、列、约束等）。
- 生成一个 SQL 脚本，用于将源数据库的数据插入目标数据库的表中。
- 在目标数据库中运行生成的脚本以及您创建的授予脚本。

打开项目的 "**属性**" 窗口，然后选择 "**包/发布 SQL** " 选项卡。

请确保在 "**配置**" 下拉列表中选择 "**活动（发布）** " 或 "**发布**"。

单击 "**启用此页**"。

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

"**包/发布 SQL** " 选项卡通常处于禁用状态，因为它指定了旧的部署方法。 在大多数情况下，应在 "**发布 Web** " 向导中配置数据库部署。 从 SQL Server Compact 迁移到 SQL Server 或 SQL Server Express 是一个特殊情况，此方法是一个不错的选择。

单击 "**从 Web.config 导入**"。

![Selecting_Import_from_Web.config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

Visual Studio 将在*web.config*文件中查找连接字符串，找到一个用于成员资格数据库，另一个用于 School 数据库，并添加与**数据库条目**表中的每个连接字符串相对应的行。 它找到的连接字符串适用于现有 SQL Server Compact 数据库，下一步是配置这些数据库的部署方式和位置。

您可以在 "数据库条目**详细信息**" 部分的 "**数据库**项" 表下输入数据库部署设置。 "**数据库条目详细信息**" 部分中显示的设置与 "**数据库项**" 表中的哪个行相关，如下图所示。

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a>为成员资格数据库配置部署设置

若要配置应用于成员资格数据库的设置，请在 "**数据库条目**" 表中选择 " **DefaultConnection** " 行。

在 "**目标数据库的连接字符串**" 中，输入指向新 SQL Server Express 成员资格数据库的连接字符串。 你可以从**服务器资源管理器**获取所需的连接字符串。 在**服务器资源管理器**中，展开 "**数据连接**" 并选择 " **aspnetTest** " 数据库，然后在 "**属性**" 窗口中复制**连接字符串**值。

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

此处重现相同的连接字符串：

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

将此连接字符串复制并粘贴到 "**包/发布 SQL** " 选项卡中**目标数据库的连接字符串**中。

请确保已选择 "**从现有数据库提取数据和/或架构**"。 这会导致在目标数据库中自动生成并运行 SQL 脚本。

**源数据库值的连接字符串**是从*web.config 文件中*提取的，指向开发 SQL Server Compact 数据库。 这是将用于生成稍后将在目标数据库中运行的脚本的源数据库。 由于你想要部署数据库的生产版本，因此请将 "aspnet-Dev" 更改为 "aspnet-Prod"。

由于要复制数据（用户帐户和角色）以及数据库结构，因此请将**数据库脚本选项**从**架构仅**更改为**架构和数据**。

若要配置部署以运行之前创建的 grant 脚本，必须将其添加到 "**数据库脚本**" 部分。 单击 "**添加脚本**"，然后在 "**添加 SQL 脚本**" 对话框中，导航到你在其中存储了 grant 脚本的文件夹（这是包含你的解决方案文件的文件夹）。 选择名为*Grant .sql*的文件，并单击 "**打开**"。

[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)

**数据库条目**中的**DefaultConnection**行的设置现在如下图所示：

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>为 School 数据库配置部署设置

接下来，在 "**数据库项**" 表中选择 " **SchoolContext** " 行，以便为 School 数据库配置部署设置。

您可以使用之前使用的方法来获取新的 SQL Server Express 数据库的连接字符串。 将此连接字符串复制到 "**包/发布 SQL** " 选项卡中**目标数据库的连接字符串**中。

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

请确保已选择 "**从现有数据库提取数据和/或架构**"。

**源数据库值的连接字符串**是从*web.config 文件中*提取的，指向开发 SQL Server Compact 数据库。 将 "School-Dev" 更改为 "School-Prod" 以部署数据库的生产版本。 （您从未在\_Data 文件夹的应用程序中创建了一个 School-Prod 文件，因此你稍后将从测试环境将该文件复制到 ContosoUniversity 项目文件夹中的应用程序\_Data 文件夹。）

将**数据库脚本选项**更改为**架构和数据**。

还需要运行脚本来向应用程序池标识授予对此数据库的读取和写入权限，因此请添加*grant .sql*脚本文件，就像对成员资格数据库执行的操作一样。

完成后，**数据库条目**中**SchoolContext**行的设置如下图所示：

![Database_Entry_Details_for_SchoolContext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

保存对 "**包/发布 SQL** " 选项卡所做的更改。

将*School-Prod*文件从*c:\inetpub\wwwroot\ContosoUniversity\App\_data*文件夹复制到 ContosoUniversity 项目中的*应用\_data*文件夹。

### <a name="specifying-transacted-mode-for-the-grant-script"></a>为授予脚本指定事务处理模式

部署过程将生成用于部署数据库架构和数据的脚本。 默认情况下，这些脚本在事务中运行。 但是，默认情况下，自定义脚本（如授予脚本）不能在事务中运行。 如果部署过程混合使用事务模式，则在部署过程中运行脚本时，可能会出现超时错误。 在本部分中，将编辑项目文件，以便将自定义脚本配置为在事务中运行。

在**解决方案资源管理器**中，右键单击**ContosoUniversity**项目，然后选择 "**卸载项目**"。

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

然后再次右键单击该项目，然后选择 "**编辑 ContosoUniversity**"。

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

Visual Studio 编辑器会显示项目文件的 XML 内容。 请注意，有几个 `PropertyGroup` 元素。 （在该图中，已省略 `PropertyGroup` 元素的内容。）

![项目文件编辑器窗口](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

第一个没有 `Condition` 属性的是适用于无论生成配置如何适用的设置。 一个 `PropertyGroup` 元素仅适用于调试生成配置（注意 `Condition` 属性），一个仅适用于发布生成配置，另一个仅适用于测试生成配置。 在发布生成配置的 `PropertyGroup` 元素中，你将看到一个 `PublishDatabaseSettings` 元素，其中包含你在 "**包/发布 SQL** " 选项卡上输入的设置。存在与指定的每个 grant 脚本对应的 `Object` 元素（请注意 "Grant" 的两个实例）。 默认情况下，将 `False`每个 grant 脚本的 `Source` 元素的 `Transacted` 属性。

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

将 `Source` 元素的 `Transacted` 属性的值更改为 "`True`"。

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

保存并关闭项目文件，然后在**解决方案资源管理器**中右键单击该项目，然后选择 "**重新加载项目**"。

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a>设置连接字符串的 web.config 转换

在 "**包/发布 SQL** " 选项卡上输入的新 SQL Express 数据库的连接字符串仅 Web 部署用于在部署期间更新目标数据库。 你仍必须设置*web.config*转换，以便部署的*web.config*文件中的连接字符串指向新的 SQL Server Express 数据库。 （使用 "**包/发布 SQL** " 选项卡时，无法在发布配置文件中配置连接字符串。）

打开*web.config*并将 `connectionStrings` 元素替换为以下示例中的 `connectionStrings` 元素。 （请确保仅复制 connectionStrings 元素，而不是此处所示的环绕代码来提供上下文。）

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

此代码会使每个 `add` 元素的 `connectionString` 和 `providerName` 属性替换为*已部署的 web.config 文件*。 这些连接字符串与您在 "**包/发布 SQL** " 选项卡中输入的字符串不同。已将设置 "MultipleActiveResultSets = True" 添加到其中，因为实体框架和通用提供程序需要此设置。

## <a name="installing-sql-server-compact"></a>安装 SQL Server Compact

SqlServerCompact NuGet 包提供 Contoso 大学应用程序的 SQL Server Compact 数据库引擎程序集。 但现在它并不是必须能够读取 SQL Server Compact 数据库的应用程序，Web 部署而是为了创建要在 SQL Server 数据库中运行的脚本。 若要启用 Web 部署读取 SQL Server Compact 数据库，请使用以下链接在开发计算机上安装 SQL Server Compact： [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)。

## <a name="deploying-to-the-test-environment"></a>部署到测试环境

若要发布到测试环境，您必须创建一个配置为使用用于数据库发布的 "**包/发布 SQL** " 选项卡而不是 "发布配置文件数据库" 设置的发布配置文件。

首先，删除现有的测试配置文件。

在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**发布**"。

选择 "**配置文件**" 选项卡。

单击“管理配置文件”。

选择 "**测试**"，单击 "**删除**"，然后单击 "**关闭**"。

关闭 "**发布 Web** " 向导以保存此更改。

接下来，创建一个新的测试配置文件并使用它来发布项目。

在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**发布**"。

选择 "**配置文件**" 选项卡。

从下拉列表中选择 " **&lt;新建 ..."&gt;** ，并输入 "Test" 作为配置文件名称。

在 "**服务 URL** " 框中，输入*localhost*。

在 "**站点/应用程序**" 框中，输入*Default Web Site/ContosoUniversity*。

在 "**目标 URL** " 框中，输入 `http://localhost/ContosoUniversity/`。

单击 **“下一步”** 。

"**设置**" 选项卡警告你已配置 "**包/发布 SQL** " 选项卡，并且通过单击 "启用新的数据库发布改进"，你可以重写这些选项卡。 对于此部署，不想覆盖 "**打包/发布 SQL** " 选项卡设置，只需单击 "**下一步**"。

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

"**预览**" 选项卡上的消息指示**未选择要发布的数据库**，但这仅意味着在发布配置文件中未配置数据库发布。

单击“发布”。

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

Visual Studio 将部署应用程序，并将浏览器打开到测试环境中站点的主页。 运行 "讲师" 页，看看它是否显示了你之前看到的相同数据。 运行 "**添加学生**" 页，添加一个新的学生，然后在 "**学生**" 页中查看新的学生。 这将验证是否可以更新数据库。 选择 "**更新信用额度**" 页（需要登录）以验证是否已部署成员资格数据库并且您有权访问该数据库。

## <a name="creating-a-sql-server-database-for-the-production-environment"></a>为生产环境创建 SQL Server 数据库

现在，你已将部署到测试环境，接下来可以设置生产的部署。 您可以通过创建要部署到的数据库，开始对测试环境执行的操作。 在您想起此概述后，Cytanium Lite 托管计划仅允许单个 SQL Server 数据库，因此您只需要设置一个数据库而不是两个数据库。 成员资格和学校 SQL Server Compact 数据库中的所有表和数据将部署到生产环境中的一个 SQL Server 数据库。

在[http://panel.cytanium.com](http://panel.cytanium.com)中转到 Cytanium 控制面板。 将鼠标停留在**数据库**上，然后单击 " **SQL Server 2008**"。

[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)

在**SQL Server 2008** "页上，单击"**创建数据库**"。

[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)

将数据库命名为 "School"，然后单击 "**保存**"。 （该页面自动添加前缀 "contosou"，因此有效名称将为 "contosouSchool"。）

[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)

在同一页上，单击 "**创建用户**"。 在 Cytanium 服务器上，而不是使用集成的 Windows 安全性，并让应用程序池标识打开数据库，则将创建一个拥有打开数据库的权限的用户。 将用户的凭据添加到生产*web.config*文件中的连接字符串。 在此步骤中，你将创建这些凭据。

[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)

在**SQL 用户属性**页中填写必填字段：

- 输入 "ContosoUniversityUser" 作为名称。
- 输入密码。
- 选择**contosouSchool**作为默认数据库。
- 选中 " **contosouSchool** " 复选框。

[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)

## <a name="configuring-database-deployment-for-the-production-environment"></a>为生产环境配置数据库部署

现在，你已准备好在 "**打包/发布 SQL** " 选项卡中设置数据库部署设置，正如之前在测试环境中所做的那样。

打开**项目**的 "属性" 窗口，选择 "**包/发布 SQL** " 选项卡，并确保在 "**配置**" 下拉列表中选择 "**活动（发布）** " 或 "**发布**"。

为每个数据库配置部署设置时，为生产环境和测试环境执行的操作的主要区别在于如何配置连接字符串。 对于测试环境，你输入了不同的目标数据库连接字符串，但对于生产环境，目标连接字符串对于这两个数据库都是相同的。 这是因为你要将两个数据库部署到生产环境中的一个数据库。

### <a name="configuring-deployment-settings-for-the-membership-database"></a>为成员资格数据库配置部署设置

若要配置应用于成员资格数据库的设置，请在 "**数据库项**" 表中选择 " **DefaultConnection** " 行。

在 "**目标数据库的连接字符串**" 中，输入指向刚刚创建的新生产 SQL Server 数据库的连接字符串。 可以从欢迎电子邮件中获取连接字符串。 电子邮件的相关部分包含以下示例连接字符串：

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

替换这三个变量后，所需的连接字符串如下例所示：

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

将此连接字符串复制并粘贴到 "**包/发布 SQL** " 选项卡中**目标数据库的连接字符串**中。

确保仍选择了**现有数据库中的 "请求数据" 和/或 "架构**"，并且**数据库脚本选项**仍为 "架构" 和 "**数据**"。

在 "**数据库脚本**" 框中，清除 Grant 脚本旁边的复选框。

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>为 School 数据库配置部署设置

接下来，在 "**数据库项**" 表中选择 " **SchoolContext** " 行，以便配置 School 数据库设置。

将相同的连接字符串复制到为成员资格数据库复制到该字段中的**目标数据库的连接字符串**中。

确保仍选择了**现有数据库中的 "请求数据" 和/或 "架构**"，并且**数据库脚本选项**仍为 "架构" 和 "**数据**"。

在 "**数据库脚本**" 框中，清除 Grant 脚本旁边的复选框。

保存对 "**包/发布 SQL** " 选项卡所做的更改。

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a>将连接字符串的 web.config 转换设置为生产数据库

接下来，您将设置*web.config*转换，以便将部署的*web.config*文件中的连接字符串指向新的生产数据库。 在 "**包/发布 SQL** " 选项卡上为 Web 部署所输入的连接字符串与应用程序需要使用的连接字符串相同，但添加了 "`MultipleResultSets`" 选项。

打开*web.config*并将 `connectionStrings` 元素替换为 `connectionStrings` 元素，如下面的示例所示。 （仅复制 `connectionStrings` 元素，而不是为显示上下文而提供的周围标记。）

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

有时会看到通知，告诉您*始终对 web.config 文件中*的连接字符串进行加密。 如果要部署到自己公司的网络上的服务器，这可能是合适的。 但是，在部署到共享的宿主环境时，将信任托管提供程序的安全做法，并且不需要或不切实际地对连接字符串进行加密。

## <a name="deploying-to-the-production-environment"></a>部署到生产环境

现在，你已准备好部署到生产环境。 Web 部署将读取项目*应用\_Data*文件夹中的 SQL Server Compact 数据库，并在生产 SQL Server 数据库中重新创建其所有表和数据。 若要使用 "**打包/发布 Web** " 选项卡设置进行发布，必须为生产创建新的发布配置文件。

首先，删除现有的生产配置文件，就像之前测试配置文件一样。

在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**发布**"。

选择 "**配置文件**" 选项卡。

单击“管理配置文件”。

选择 "**生产**"，单击 "**删除**"，然后单击 "**关闭**"。

关闭 "**发布 Web** " 向导以保存此更改。

接下来，创建新的生产配置文件并使用它来发布项目。

在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后单击 "**发布**"。

选择 "**配置文件**" 选项卡。

单击 "**导入**"，然后选择前面下载的 .publishsettings 文件。

在 "**连接**" 选项卡上，将 "**目标 URL** " 更改为正确的临时 URL，在此示例中 http://contosouniversity.com.vserver01.cytanium.com。

将该配置文件重命名为生产。 （选择 "**配置文件**" 选项卡，然后单击 "**管理配置文件**"）。

关闭 "**发布 Web** " 向导以保存你所做的更改。

在实际应用程序中，如果在生产环境中更新数据库，则可以在发布之前执行两个额外的步骤：

1. 如[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程中所示，将应用上传到 *\_offline。*
2. 使用 Cytanium "控制面板" 的 "**文件管理器**" 功能，将*aspnet-Prod*和*School-Prod*文件从生产站点复制到 ContosoUniversity 项目的 "*应用\_Data* " 文件夹中。 这可确保正在部署到新 SQL Server 数据库的数据包含生产网站所做的最新更新。

在**Web 一键式发布**工具栏中，确保选择了 "**生产**配置文件"，然后单击 "**发布**"。

如果在发布之前上传<em>\_offline 的应用</em>，则必须使用 Cytanium 控制面板中的 "<strong>文件管理器</strong>" 实用程序来删除<em>脱机应用\_。</em>htm。 同时，还可以从<em>应用\_Data</em>文件夹中删除<em>.sdf</em>文件。

你现在可以打开浏览器，并使用你的公共网站的 URL 来测试应用程序，就像在部署到测试环境后执行的操作一样。

## <a name="switching-to-sql-server-express-localdb-in-development"></a>切换到开发 SQL Server Express LocalDB

如概述中所述，通常最好在用于测试和生产的开发环境中使用相同的数据库引擎。 （请记住，使用开发 SQL Server Express 的优势在于，数据库在开发、测试和生产环境中的工作方式相同。）在本部分中，你将在从 Visual Studio 中运行应用程序时，将 ContosoUniversity 项目设置为使用 SQL Server Express LocalDB。

要执行此迁移，最简单的方法是让 Code First 和成员资格系统为您创建这两个新的开发数据库。 使用此方法迁移需要三个步骤：

1. 更改连接字符串以指定新的 SQL Express LocalDB 数据库。
2. 运行网站管理工具来创建管理员用户。 这会创建成员资格数据库。
3. 使用 Code First 迁移更新数据库命令创建应用程序数据库并设定其种子。

### <a name="updating-connection-strings-in-the-webconfig-file"></a>更新 Web.config 文件中的连接字符串

打开 web.config*文件并*将 `connectionStrings` 元素替换为以下代码：

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a>创建成员资格数据库

在**解决方案资源管理器**中，选择 "ContosoUniversity" 项目，然后单击 "**项目**" 菜单中的 " **ASP.NET 配置**"。

选择“安全”选项卡。

单击 "**创建或管理角色**"，然后创建**管理员**角色。

返回到 "安全" 选项卡。

单击 "**创建用户**"，然后选中 "**管理员**" 复选框并创建名为 "管理员" 的用户。

关闭**网站管理工具**。

### <a name="creating-the-school-database"></a>创建 School 数据库

打开 "包管理器控制台" 窗口。

在 "**默认项目**" 下拉列表中，选择 ContosoUniversity 项目。

输入以下命令：

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

Code First 迁移应用创建数据库的初始迁移，然后应用 AddBirthDate 迁移，然后运行 Seed 方法。

按 Ctrl-F5 运行该站点。 与测试环境和生产环境相同，运行 "**添加学生**" 页，添加新的学生，然后在 "**学生**" 页中查看新的学生。 这会验证 School 数据库是否已创建和初始化，以及你是否具有对该数据库的读写访问权限。

选择 "**更新信用额度**" 页，然后登录以验证是否已部署成员资格数据库以及您是否有权访问该数据库。 如果你没有迁移你的用户帐户，请创建一个管理员帐户，然后选择 "**更新信用额度**" 页以验证其是否正常工作。

## <a name="cleaning-up-sql-server-compact-files"></a>清理 SQL Server Compact 文件

你不再需要包含的文件和 NuGet 包来支持 SQL Server Compact。 如果需要（此步骤不是必需的），可以清除不需要的文件和引用。

在**解决方案资源管理器**中，从*应用程序\_Data*文件夹中删除 *.sdf*文件，并从*bin*文件夹中删除*amd64*和*x86*文件夹。

在**解决方案资源管理器**中，右键单击该解决方案（不是项目之一），然后单击 "**管理解决方案的 NuGet 包**"。

在 "**管理 NuGet 包**" 对话框的左窗格中，选择 "**已安装包**"。

选择**EntityFramework SqlServerCompact**包，并单击 "**管理**"。

在 "**选择项目**" 对话框中，这两个项目都处于选中状态。 若要在这两个项目中卸载包，请清除这两个复选框，然后单击 **"确定"** 。

在询问是否要卸载依赖包的对话框中，单击 "否"。 其中一个是您必须保留的实体框架包。

按照相同的过程卸载**SqlServerCompact**包。 （必须按此顺序卸载包，因为**EntityFramework SqlServerCompact**包依赖于**SqlServerCompact**包。）

你现在已成功迁移到 SQL Server Express 和完整 SQL Server。 在下一教程中，你将进行另一次数据库更改，当你的测试数据库和生产数据库使用 SQL Server Express 和完全 SQL Server 时，你将了解如何部署数据库更改。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [下一页](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
