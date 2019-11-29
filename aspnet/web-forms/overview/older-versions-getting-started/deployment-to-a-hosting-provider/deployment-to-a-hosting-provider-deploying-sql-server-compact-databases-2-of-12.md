---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署 SQL Server Compact 数据库-2 个，共12个 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: 56ceabc79947967846d342354fd033510be5f05a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74625546"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署 SQL Server Compact 数据库-2 of 12

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

本教程介绍如何设置两个 SQL Server Compact 数据库和用于部署的数据库引擎。

对于数据库访问，Contoso 大学应用程序需要以下必须与应用程序一起部署的软件，因为它未包含在 .NET Framework 中：

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) （数据库引擎）。
- [ASP.NET 通用提供程序](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)（使 ASP.NET 成员资格系统可以使用 SQL Server Compact）
- [实体框架 5.0](https://msdn.microsoft.com/library/gg696172(d=lightweight,v=vs.103).aspx)（Code First 迁移）。

数据库结构和应用程序的两个数据库中的某些（而非全部）数据也必须部署。 通常，在开发应用程序时，您可以将测试数据输入到不想部署到实时站点的数据库中。 不过，您也可以输入一些您要部署的生产数据。 在本教程中，你将配置 Contoso 大学项目，以便在部署时包括所需的软件和正确的数据。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="sql-server-compact-versus-sql-server-express"></a>SQL Server Compact 与 SQL Server Express

示例应用程序使用 SQL Server Compact 4.0。 此数据库引擎是网站的一个相对全新的选项;早期版本的 SQL Server Compact 在 web 宿主环境中不起作用。 与使用 SQL Server Express 进行开发并将其部署到完整 SQL Server 更常见的方案相比，SQL Server Compact 提供了几个优点。 根据所选的托管提供程序，SQL Server Compact 可能会更便宜，因为某些提供程序需要额外付费来支持完全 SQL Server 的数据库。 SQL Server Compact 不会额外收取费用，因为你可以在 web 应用程序中部署数据库引擎本身。

但是，您还应知道其局限性。 SQL Server Compact 不支持存储过程、触发器、视图或复制。 （有关 SQL Server Compact 不支持 SQL Server 功能的完整列表，请参阅[SQL Server Compact 和 SQL Server 之间的差异](https://msdn.microsoft.com/library/bb896140.aspx)。）此外，某些可用于在 SQL Server Express 和 SQL Server 数据库中操作架构和数据的工具不能与 SQL Server Compact 一起使用。 例如，不能在 Visual Studio 中将 SQL Server Management Studio 或 SQL Server Data Tools 与 SQL Server Compact 数据库一起使用。 您可以使用其他选项来处理 SQL Server Compact 数据库：

- 你可以在 Visual Studio 中使用服务器资源管理器，这为 SQL Server Compact 提供了有限的数据库操作功能。
- 您可以使用[WebMatrix](https://www.microsoft.com/web/webmatrix/)的数据库操作功能，该功能的功能比服务器资源管理器多。
- 您可以使用相对功能最齐全的第三方或开源工具，如[SQL Server Compact 工具箱](https://github.com/ErikEJ/SqlCeToolbox)和[SQL Compact 数据和架构脚本实用工具](https://github.com/ErikEJ/SqlCeToolbox)。
- 您可以编写和运行自己的 DDL （数据定义语言）脚本来处理数据库架构。

你可以从 SQL Server Compact 开始，然后随着需求的发展，稍后再升级。 本系列后面的教程介绍如何从 SQL Server Compact 迁移到 SQL Server Express 并 SQL Server。 但是，如果你要创建新的应用程序并希望在不久的将来需要 SQL Server，则最好是从 SQL Server 或 SQL Server Express 开始。

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>为部署配置 SQL Server Compact 数据库引擎

通过安装以下 NuGet 包，添加了 Contoso 大学应用程序中数据访问所需的软件：

- [SqlServerCompact](http://nuget.org/List/Packages/SqlServerCompact)
- [System.web. Providers](http://nuget.org/List/Packages/System.Web.Providers) （ASP.NET 通用提供程序）
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework. SqlServerCompact](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

这些链接指向这些包的当前版本，这些包可能比你在本教程中下载的初学者项目中安装的版本更新。 若要部署到宿主提供程序，请确保使用实体框架5.0 或更高版本。 更早版本的 Code First 迁移需要完全信任，在许多托管提供程序中，你的应用程序将在中等信任环境下运行。 有关中等信任的详细信息，请参阅 "[以测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) " 教程。

NuGet 包安装通常负责将此软件与应用程序一起部署所需的所有内容。 在某些情况下，这涉及到任务，例如更改 Web.config 文件以及添加每次生成解决方案时运行的 PowerShell 脚本。 **如果要在不使用 NuGet 的情况下添加对其中任何功能（如 SQL Server Compact 和实体框架）的支持，请确保了解 NuGet 包安装的功能，以便可以手动执行相同的工作。**

有一个例外，NuGet 并不负责确保成功部署所需的一切内容。 SqlServerCompact NuGet 包将向项目中添加一个后期生成脚本，将本机程序集复制到项目*bin*文件夹下的*x86*和*amd64*子文件夹，但该脚本不包含项目中的这些文件夹。 因此，除非您手动将它们包含在项目中，否则 Web 部署不会将它们复制到目标网站。 （此行为是由默认部署配置生成的，另一个选项（在本教程中不会使用）是更改控制此行为的设置。 您可以更改的设置只是在**项目 "属性**" 窗口的 "**打包/发布 Web** " 选项卡下**要部署的项目**下**运行应用程序所需的文件**。 通常不建议更改此设置，因为这可能会导致将更多的文件部署到生产环境中，而不是所需的数量。 有关备选方案的详细信息，请参阅[配置项目属性](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)教程。）

生成项目，然后在**解决方案资源管理器**单击 "**显示所有文件**" （如果尚未这样做）。 你可能还需要单击 "**刷新**"。

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

展开**bin**文件夹以查看**amd64**和**x86**文件夹，然后选择这些文件夹，右键单击，然后选择 "**包括在项目中**"。

![amd64_and_x86_in_Solution_Explorer .png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

文件夹图标将更改为显示该文件夹已包含在项目中。

![Solution_Explorer_amd64_included .png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>配置应用程序数据库部署的 Code First 迁移

当你部署应用程序数据库时，通常不会只是将你的开发数据库部署到生产数据库中的所有数据，因为其中的很多数据可能仅用于测试目的。 例如，测试数据库中的学生姓名是虚构的。 另一方面，通常不能只部署数据库结构，根本就不会包含任何数据。 测试数据库中的某些数据可能是真实数据，当用户开始使用该应用程序时必须存在。 例如，您的数据库可能有一个表包含有效的评分值或实际的部门名称。

若要模拟这种常见方案，你将配置一个 Code First 迁移种子方法，该方法仅在生产中插入到数据库中的数据。 此种子方法不插入测试数据，因为它将在生产中 Code First 创建数据库后在生产中运行。

在发布迁移之前 Code First 早期版本中，种子方法经常插入测试数据，因为在开发过程中每个模型更改都必须完全删除并从头开始创建。 在 Code First 迁移的情况下，在数据库更改后会保留测试数据，因此不需要在 Seed 方法中包括测试数据。 下载的项目使用预迁移方法，将所有数据包含在初始值设定项类的 Seed 方法中。 在本教程中，您将禁用初始值设定项类并启用迁移。 然后，将更新迁移配置类中的 Seed 方法，以便只插入要在生产中插入的数据。

下图说明了应用程序数据库的架构：

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

对于这些教程，你将假设首次部署站点时，`Student` 和 `Enrollment` 表应为空。 其他表包含在应用程序进入活动时必须预加载的数据。

由于将使用 Code First 迁移，因此不再需要使用**DropCreateDatabaseIfModelChanges** Code First 初始值设定项。 此初始值设定项的代码位于 ContosoUniversity 项目的 SchoolInitializer.cs 文件中。 Web.config 文件的**appSettings**元素中的设置使此初始值设定项在应用程序首次尝试访问数据库时运行：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

打开应用程序 Web.config 文件，并从 appSettings 元素中删除指定 Code First 初始值设定项类的元素。 AppSettings 元素现在如下所示：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> 指定初始值设定项类的另一种方法是，在*global.asax*文件中的 `Application_Start` 方法中调用 `Database.SetInitializer`。 如果要在使用该方法来指定初始值设定项的项目中启用迁移，请删除该行代码。

接下来，启用 Code First 迁移。

第一步是确保将 ContosoUniversity 项目设置为启动项目。 在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后选择 "**设为启动项目**"。 Code First 迁移将在启动项目中查找数据库连接字符串。

从 "**工具**" 菜单中，依次单击 " **NuGet 包管理器**" 和 "**程序包管理器控制台**"。

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

在 "**包管理器控制台**" 窗口顶部，选择 "ContosoUniversity" 作为默认项目，然后在 `PM>` 提示符下输入 "启用-迁移"。

![enable-migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

此命令在 ContosoUniversity 项目中的新*迁移*文件夹中创建*Configuration.cs*文件。

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

你选择了 DAL 项目，因为必须在包含 Code First 上下文类的项目中执行 "启用-迁移" 命令。 当该类在类库项目中时，Code First 迁移将在解决方案的启动项目中查找数据库连接字符串。 在 ContosoUniversity 解决方案中，web 项目已设置为启动项目。 （如果你不想在 Visual Studio 中指定具有连接字符串的项目作为启动项目，则可以在 PowerShell 命令中指定启动项目。 若要查看 "启用-迁移" 命令的命令语法，可以输入 "get-help 启用-迁移" 命令。

打开 Configuration.cs 文件，并将 `Seed` 方法中的注释替换为以下代码：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

对 `List` 的引用在其下有红色的波浪线，因为尚没有用于其命名空间的 `using` 语句。 右键单击其中一个 `List` 实例，单击 "**解析**"，然后单击 "**使用 system.object**"。

![使用 using 语句解析](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

此菜单选择会将以下代码添加到文件顶部附近的 `using` 语句中。

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> 将代码添加到 `Seed` 方法是将固定数据插入数据库的多种方式之一。 一种替代方法是向每个迁移类的 `Up` 和 `Down` 方法中添加代码。 `Up` 和 `Down` 方法包含实现数据库更改的代码。 在[部署数据库更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教程中，你将看到这些示例的示例。
> 
> 你还可以使用 `Sql` 方法编写执行 SQL 语句的代码。 例如，如果您将某一预算列添加到部门表中，并且想要将所有部门预算初始化为 $1000.00，作为迁移的一部分，您可以将以下代码行添加到该迁移的 `Up` 方法中：
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> 本教程中显示的此示例使用 Code First 迁移 `Configuration` 类的 `Seed` 方法中的 `AddOrUpdate` 方法。 Code First 迁移将在每次迁移后调用 `Seed` 方法，此方法将更新已插入的行，如果它们尚不存在，则将其插入。 对于你的方案，`AddOrUpdate` 方法可能不是最佳选择。 有关详细信息，请参阅 Julie Lerman 的博客上的[EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

按 CTRL-SHIFT-B 生成项目。

下一步是创建用于初始迁移的 `DbMigration` 类。 希望此迁移创建新的数据库，因此必须删除已存在的数据库。 SQL Server Compact 数据库包含在*应用\_Data*文件夹中的 *.sdf*文件中。 在**解决方案资源管理器**中，展开 "ContosoUniversity" 项目中的 "*应用\_数据*" 以查看两个 SQL Server Compact 数据库，这些数据库由 *.sdf*文件表示。

右键单击 " *School .sdf* " 文件，然后单击 "**删除**"。

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

在 "**程序包管理器控制台**" 窗口中，输入 "添加迁移初始" 命令以创建初始迁移，并将其命名为 "初始"。

![添加-migration_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Code First 迁移在 "*迁移*" 文件夹中创建另一个类文件，此类包含用于创建数据库架构的代码。

在 "**程序包管理器控制台**" 中，输入命令 "更新数据库" 以创建数据库并运行**Seed**方法。

![更新-database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

（如果您收到一条错误消息，指示表已存在并且无法创建，则可能是您在删除数据库之后和执行 `update-database`之前运行了该应用程序。 在这种情况下，再次删除*School .sdf*文件，然后重试 `update-database` 命令。）

运行该应用程序。 现在，学生页面为空，但讲师页面包含指导员。 这是在部署应用程序后将在生产中获得的内容。

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

项目现已准备好部署*School*数据库。

## <a name="creating-a-membership-database-for-deployment"></a>为部署创建成员资格数据库

Contoso 大学应用程序使用 ASP.NET 成员资格系统和 forms 身份验证对用户进行身份验证和授权。 只有管理员才能访问其中一个页面。 若要查看此页，请运行应用程序，并从 "**课程**" 下的弹出菜单中选择 "**更新信用**"。 应用程序将显示 "**登录**" 页，因为只有管理员有权使用 "**更新信用额度**" 页。

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

使用密码 "Pas $ w0rd" 以 "管理员" 身份登录（请注意，"w0rd" 中的字母 "o" 的位置数字为零）。 登录后，将显示 "**更新信用额度**" 页。

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

首次部署站点时，通常会排除你为测试创建的大多数或所有用户帐户。 在这种情况下，你将部署一个管理员帐户，而不是用户帐户。 不是手动删除测试帐户，而是创建一个新的成员资格数据库，该数据库只具有在生产中需要的一个管理员用户帐户。

> [!NOTE]
> 成员资格数据库存储帐户密码的哈希。 若要从一台计算机向另一台计算机部署帐户，必须确保在目标服务器上哈希例程不会生成不同于源计算机的哈希。 当你使用 ASP.NET 通用提供程序时，只要不更改默认算法，它们就会生成相同的哈希。 默认算法是 HMACSHA256，它是在 web.config 文件中 **[machineKey](https://msdn.microsoft.com/library/w8h3skw9.aspx)** 元素的**验证**特性中指定的。

成员资格数据库不是由 Code First 迁移维护的，并且没有自动初始值设定项，它将数据库与测试帐户（如 School 数据库）进行种子设定。 因此，为了使测试数据可用，在创建新的测试数据库之前，将创建一个测试数据库的副本。

在**解决方案资源管理器**中，将*应用\_Data*文件夹中的*aspnet .Sdf*文件重命名为*aspnet-Dev*。 （不要制作副本，只需重命名即可，稍后会创建一个新数据库。）

在**解决方案资源管理器**中，确保选中 web 项目（ContosoUniversity，而不是 ContosoUniversity）。 然后，在 "**项目**" 菜单中，选择 " **ASP.NET 配置**" 以运行**网站管理工具**（哪些）。

选择“安全性”选项卡。

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

单击 "**创建或管理角色**" 并添加**管理员**角色。

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

向后导航到 "**安全**" 选项卡，单击 "**创建用户**"，并以管理员身份添加用户 "管理员"。 在单击 "**创建用户**" 页上的 "**创建用户**" 按钮之前，请确保选中 "**管理员**" 复选框。 本教程中使用的密码是 "Pas $ w0rd"，你可以输入任何电子邮件地址。

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

关闭浏览器。 在**解决方案资源管理器**中，单击 "刷新" 按钮以查看新的*aspnet .sdf*文件。

![New_aspnet. sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

右键**单击 "** "，然后选择 **"包括在项目中"** 。

## <a name="distinguishing-development-from-production-databases"></a>与生产数据库的开发区分开来

在本部分中，您将重命名数据库，使开发版本为 School-Dev 和 aspnet-Dev，并且生产版本为 School-Prod 和 aspnet-Prod。 这并不是必需的，但这样做将有助于使你无法获取数据库的测试版本和生产版本。

在**解决方案资源管理器**中，单击 "**刷新**"，然后展开 "应用\_数据" 文件夹以查看之前创建的 School 数据库;右键单击该项目，然后选择 **"包括在项目中"** 。

![Including_School. sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

将*aspnet .sdf*重命名为*aspnet-Prod*。

将*School*重命名为*School-Dev*。

当你在 Visual Studio 中运行应用程序时，不希望使用数据库文件的*生产*版本，你需要使用 *-Dev*版本。 因此，您必须更改 Web.config 文件中的连接字符串，以使其指向数据库的*开发*版本。 （您尚未创建 School-Prod 文件，但这是正常的，因为 Code First 在您首次运行应用程序时，会在生产环境中创建该数据库。）

打开应用程序的 web.config 文件，然后找到连接字符串：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

将 "aspnet .sdf" 更改为 "aspnet-Dev"，并将 "School .sdf" 改为 "School-Dev"：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

现在可以部署 SQL Server Compact 数据库引擎和两个数据库。 在以下教程中，您将为开发、测试和生产环境中必须不同的设置*设置自动 web.config*文件转换。 （在必须更改的设置中是连接字符串，但稍后在创建发布配置文件时将设置这些更改。）

## <a name="more-information"></a>详细信息

有关 NuGet 的详细信息，请参阅通过 NuGet 和[Nuget 文档](http://docs.nuget.org/docs/start-here/overview)[管理项目库](https://msdn.microsoft.com/magazine/hh547106.aspx)。 如果你不想使用 NuGet，你将需要了解如何分析 NuGet 包，以确定它在安装时执行的操作。 （例如，它可能配置*web.config*转换、将 PowerShell 脚本配置为在生成时运行，等等）若要详细了解 NuGet 的工作原理，请参阅特别是[创建和发布包](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package)、[配置文件和源代码转换](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-introduction-1-of-12.md)
> [下一页](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
