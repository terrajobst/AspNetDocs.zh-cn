---
uid: web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
title: 使用 Visual Studio 的 ASP.NET Web 部署：准备数据库部署 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ae4def81-fa37-4883-a13e-d9896cbf6c36
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
msc.type: authoredcontent
ms.openlocfilehash: cdcb3578725c41e3c801afd54e6d34455bc4b281
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517280"
---
# <a name="aspnet-web-deployment-using-visual-studio-preparing-for-database-deployment"></a>使用 Visual Studio 的 ASP.NET Web 部署：准备数据库部署

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。

## <a name="overview"></a>概述

本教程演示如何为数据库部署准备项目。 数据库结构和应用程序的两个数据库中的某些（而非全部）数据必须部署到测试、过渡和生产环境中。

通常，在开发应用程序时，您可以将测试数据输入到不想部署到实时站点的数据库中。 但是，你可能还具有一些你要部署的生产数据。 在本教程中，你将配置 Contoso 大学项目并准备 SQL 脚本，以便在部署时包含正确的数据。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](troubleshooting.md)。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

示例应用程序使用 SQL Server Express LocalDB。 SQL Server Express 是 SQL Server 的免费版本。 它通常在开发过程中使用，因为它基于与 SQL Server 的完整版本相同的数据库引擎。 你可以使用 SQL Server Express 进行测试，确保应用程序在生产环境中的行为相同，但 SQL Server 版本不同的功能有一些例外。

LocalDB 是 SQL Server Express 的一种特殊执行模式，可用于将数据库作为 *.mdf*文件处理。 通常，LocalDB 数据库文件保存在 web 项目的*应用\_Data*文件夹中。 使用 SQL Server Express 中的用户实例功能，还可以使用 *.mdf*文件，但不推荐使用用户实例功能;因此，建议使用 LocalDB 来处理 *.mdf*文件。

通常 SQL Server Express 不用于生产 web 应用程序。 不建议将 LocalDB 特别用于 web 应用程序，因为它不能与 IIS 一起使用。

在 Visual Studio 2012 中，默认情况下使用 Visual Studio 安装 LocalDB。 在 Visual Studio 2010 及更早版本中，默认情况下，使用 Visual Studio 安装 SQL Server Express （无 LocalDB）;这就是你在[本系列的第一个教程](introduction.md)中将其作为先决条件之一安装的原因。

有关 SQL Server 版本（包括 LocalDB）的详细信息，请参阅使用[SQL Server 数据库](../../../../whitepapers/aspnet-data-access-content-map.md#sqlserver)的以下资源。

## <a name="entity-framework-and-universal-providers"></a>实体框架和通用提供程序

对于数据库访问，Contoso 大学应用程序需要以下必须与应用程序一起部署的软件，因为它未包含在 .NET Framework 中：

- [ASP.NET 通用提供程序](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx)（允许 ASP.NET 成员资格系统使用 Azure SQL 数据库）
- [Entity Framework](https://msdn.microsoft.com/library/gg696172.aspx)

由于此软件包含在 NuGet 包中，因此已设置该项目，以便在项目中部署所需的程序集。 （这些链接指向这些包的当前版本，这些包可能比你在本教程中下载的初学者项目中安装的版本更高。）

如果要部署到第三方托管提供程序而不是 Azure，请确保使用实体框架5.0 或更高版本。 更早版本的 Code First 迁移需要完全信任，大多数托管提供商将在中等信任环境下运行你的应用程序。 有关中等信任的详细信息，请参阅 "将[IIS 部署为测试环境](deploying-to-iis.md)" 教程。

## <a name="configure-code-first-migrations-for-application-database-deployment"></a>配置应用程序数据库部署 Code First 迁移

Contoso 大学应用程序数据库由 Code First 管理，你将使用 Code First 迁移来部署它。 有关使用 Code First 迁移进行数据库部署的概述，请参阅[本系列中的第一个教程](introduction.md)。

当你部署应用程序数据库时，通常不会只是将你的开发数据库部署到生产数据库中的所有数据，因为其中的很多数据可能仅用于测试目的。 例如，测试数据库中的学生姓名是虚构的。 另一方面，通常不能只部署数据库结构，根本就不会包含任何数据。 测试数据库中的某些数据可能是真实数据，当用户开始使用该应用程序时必须存在。 例如，您的数据库可能有一个表包含有效的评分值或实际的部门名称。

若要模拟这种常见方案，你将配置一个 Code First 迁移 `Seed` 方法，该方法仅在生产中插入到数据库中的数据。 此 `Seed` 方法不应插入测试数据，因为它将在生产中 Code First 创建数据库后在生产中运行。

在发布迁移之前 Code First 早期版本中，`Seed` 方法还经常插入测试数据，因为在开发过程中每个模型更改都必须完全删除并从头开始创建数据库。 在 Code First 迁移的情况下，在数据库更改后会保留测试数据，因此不需要在 `Seed` 方法中包括测试数据。 下载的项目使用方法将所有数据包含在初始值设定项类的 `Seed` 方法中。 在本教程中，您将禁用该初始化表达式类并启用迁移。 然后，将更新迁移配置类中的 `Seed` 方法，以便只插入要在生产中插入的数据。

下图说明了应用程序数据库的架构：

[![School_database_diagram](preparing-databases/_static/image2.png)](preparing-databases/_static/image1.png)

对于这些教程，你将假设首次部署站点时，`Student` 和 `Enrollment` 表应为空。 其他表包含在应用程序进入活动时必须预加载的数据。

### <a name="disable-the-initializer"></a>禁用初始值设定项

由于将使用 Code First 迁移，因此不必使用 `DropCreateDatabaseIfModelChanges` Code First 初始值设定项。 此初始值设定项的代码位于 ContosoUniversity 项目的*SchoolInitializer.cs*文件中。 *Web.config 文件的*`appSettings` 元素中的设置使此初始值设定项在应用程序首次尝试访问数据库时运行：

[!code-xml[Main](preparing-databases/samples/sample1.xml?highlight=3)]

打开应用程序*web.config*文件，删除或注释掉指定 Code First 初始值设定项类的 `add` 元素。 `appSettings` 元素现在如下所示：

[!code-xml[Main](preparing-databases/samples/sample2.xml)]

> [!NOTE]
> 指定初始值设定项类的另一种方法是，在*global.asax*文件中的 `Application_Start` 方法中调用 `Database.SetInitializer`。 如果要在使用该方法来指定初始值设定项的项目中启用迁移，请删除该行代码。

> [!NOTE]
> 如果使用 Visual Studio 2013，请在 PMC 中的步骤2和步骤3：（a）之间添加以下步骤，以获取 EF 的当前版本。 然后（b）生成项目以获取生成错误的列表，并修复这些错误。 对于不再存在的命名空间，请单击 "删除"，然后单击 "解析" 以添加所需的 using 语句，并将 EntityState 更改为 EntityState。

### <a name="enable-code-first-migrations"></a>启用 Code First 迁移

1. 确保将 ContosoUniversity 项目（而不是 ContosoUniversity）设置为启动项目。 在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后选择 "**设为启动项目**"。 Code First 迁移将在启动项目中查找数据库连接字符串。
2. 从 "**工具**" 菜单中，选择 " **NuGet 包管理器** > **程序包管理器控制台**"。

    ![Selecting_Package_Manager_Console](preparing-databases/_static/image3.png)
3. 在 "**包管理器控制台**" 窗口顶部，选择 "ContosoUniversity" 作为默认项目，然后在 `PM>` 提示符下输入 "启用-迁移"。

    ![启用-迁移命令](preparing-databases/_static/image4.png)

    （如果出现错误，指出无法识别 "*启用-迁移*" 命令，请输入命令*更新-package EntityFramework* ，然后重试。）

    此命令将在 ContosoUniversity 项目中创建一个*迁移*文件夹，并将其放在该文件夹中，这两个文件：一个可用于配置迁移的*Configuration.cs*文件，以及一个创建数据库的第一个迁移的*InitialCreate.cs*文件。

    ![迁移文件夹](preparing-databases/_static/image5.png)

    您在**包管理器控制台**的 "**默认项目**" 下拉列表中选择了 DAL 项目，因为必须在包含 Code First 上下文类的项目中执行 `enable-migrations` 命令。 当该类在类库项目中时，Code First 迁移将在解决方案的启动项目中查找数据库连接字符串。 在 ContosoUniversity 解决方案中，web 项目已设置为启动项目。 如果不想在 Visual Studio 中指定具有连接字符串作为启动项目的项目，可以在 PowerShell 命令中指定启动项目。 若要查看命令语法，请输入命令 `get-help enable-migrations`。

    `enable-migrations` 命令自动创建了第一个迁移，因为数据库已存在。 另一种方法是让迁移创建数据库。 为此，请使用**服务器资源管理器**或**SQL Server 对象资源管理器**在启用迁移之前删除 ContosoUniversity 数据库。 启用迁移后，通过输入命令 "add-InitialCreate" 手动创建第一次迁移。 然后，可以通过输入命令 "更新数据库" 来创建数据库。

### <a name="set-up-the-seed-method"></a>设置种子方法

对于本教程，你将通过将代码添加到 Code First 迁移 `Configuration` 类的 `Seed` 方法来添加固定数据。 Code First 迁移将在每次迁移后调用 `Seed` 方法。

由于 `Seed` 方法在每次迁移后运行，因此在首次迁移后，表中已有数据。 若要处理这种情况，你将使用 `AddOrUpdate` 方法来更新已插入的行，如果它们尚不存在，则将其插入。 对于你的方案，`AddOrUpdate` 方法可能不是最佳选择。 有关详细信息，请参阅 Julie Lerman 的博客上的[EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

1. 打开*Configuration.cs*文件，并将 `Seed` 方法中的注释替换为以下代码：

    [!code-csharp[Main](preparing-databases/samples/sample3.cs)]
2. 对 `List` 的引用在其下有红色的波浪线，因为尚没有用于其命名空间的 `using` 语句。 右键单击其中一个 `List` 实例，单击 "**解析**"，然后单击 "**使用 system.object**"。

    ![使用 using 语句解析](preparing-databases/_static/image6.png)

    此菜单选择会将以下代码添加到文件顶部附近的 `using` 语句中。

    [!code-csharp[Main](preparing-databases/samples/sample4.cs)]
3. 按 CTRL-SHIFT-B 生成项目。

项目现已准备好部署*ContosoUniversity*数据库。 部署应用程序后，第一次运行该应用程序并导航到访问数据库的页时，Code First 将创建数据库并运行此 `Seed` 方法。

> [!NOTE]
> 将代码添加到 `Seed` 方法是将固定数据插入数据库的多种方式之一。 一种替代方法是向每个迁移类的 `Up` 和 `Down` 方法中添加代码。 `Up` 和 `Down` 方法包含实现数据库更改的代码。 在[部署数据库更新](deploying-a-database-update.md)教程中，你将看到这些示例的示例。
> 
> 你还可以使用 `Sql` 方法编写执行 SQL 语句的代码。 例如，如果您将某一预算列添加到部门表中，并且想要将所有部门预算初始化为 $1000.00，作为迁移的一部分，您可以将以下代码行添加到该迁移的 `Up` 方法中：
> 
> `Sql("UPDATE Department SET Budget = 1000");`

## <a name="create-scripts-for-membership-database-deployment"></a>为成员资格数据库部署创建脚本

Contoso 大学应用程序使用 ASP.NET 成员资格系统和 forms 身份验证对用户进行身份验证和授权。 只有管理员角色中的用户才能访问 "**更新信用额度**" 页。

运行应用程序，单击 "**课程**"，然后单击 "**更新信用**"。

![单击更新信用额度](preparing-databases/_static/image7.png)

由于**更新信用**页面需要管理权限，因此将显示 "**登录**" 页。

输入*admin*作为用户名，并在*devpwd*中单击 "**登录**"。

![登录页](preparing-databases/_static/image8.png)

此时将显示 "**更新信用**" 页。

![更新信用额度页](preparing-databases/_static/image9.png)

用户和角色信息位于由*web.config 文件中的* **DefaultConnection**连接字符串指定的*ContosoUniversity*数据库中。

此数据库不是由实体框架 Code First 管理的，因此不能使用迁移来部署它。 您将使用 dbDacFx 提供程序部署数据库架构，并将发布配置文件配置为运行将向数据库表中插入初始数据的脚本。

> [!NOTE]
> Visual Studio 2013 中引入了一个新的 ASP.NET 成员资格系统（现在命名为 ASP.NET Identity）。 新系统使您能够将应用程序和成员关系表保存在同一个数据库中，并且可以使用 Code First 迁移部署这两个表。 示例应用程序使用不能使用 Code First 迁移部署的早期 ASP.NET 成员资格系统。 部署此成员资格数据库的过程也适用于任何其他方案，在此方案中，应用程序需要部署不由实体框架 Code First 创建的 SQL Server 数据库。

在此，您通常不希望在生产环境中使用与开发中的数据相同的数据。 首次部署站点时，通常会排除你为测试创建的大多数或所有用户帐户。 因此，下载的项目具有两个成员资格数据库： *aspnet-ContosoUniversity*和生产用户的*aspnet-ContosoUniversity-Prod* 。 对于本教程，两个数据库中的用户名相同： *admin*和*nonadmin*。 这两个用户在开发数据库中具有密码*devpwd* ，在生产数据库中具有*prodpwd* 。

你将开发用户部署到测试环境，并将生产用户部署到过渡和生产环境。 为此，你将在本教程中创建两个 SQL 脚本，一个用于开发，一个用于生产，稍后的教程中，你将配置发布过程以运行它们。

> [!NOTE]
> 成员资格数据库存储帐户密码的哈希。 若要从一台计算机向另一台计算机部署帐户，必须确保在目标服务器上哈希例程不会生成不同于源计算机的哈希。 当你使用 ASP.NET 通用提供程序时，只要不更改默认算法，它们就会生成相同的哈希。 默认算法是 HMACSHA256，它是在 web.config 文件中 **[machineKey](https://msdn.microsoft.com/library/system.web.configuration.machinekeysection.aspx)** 元素的**验证**特性中指定的。

您可以使用 SQL Server Management Studio （SSMS）或使用第三方工具手动创建数据部署脚本。 本教程的余下部分将介绍如何在 SSMS 中执行此操作，但如果不想安装和使用 SSMS，可以从项目的完整版本中获取脚本，并跳到在解决方案文件夹中存储它们的部分。

若要安装 SSMS，请从[下载中心安装： Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062)中单击 " [ENU\x64\SQLManagementStudio"\_x64\_](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLManagementStudio_x64_ENU.exe) "ENU\x86\SQLManagementStudio" 或 " [\_\_](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLManagementStudio_x86_ENU.exe)"。 如果您为系统选择了错误的安装程序，安装将失败，您可以尝试另一个安装程序。

（请注意，这是一个 600 MB 的下载。 可能需要很长时间才能安装，并且需要重新启动计算机。）

在 SQL Server 安装中心的第一页上，单击 "**新建 SQL Server 独立安装或向现有安装添加功能**"，然后按照说明接受默认选择。

### <a name="create-the-development-database-script"></a>创建开发数据库脚本

1. 运行 SSMS。
2. 在 "**连接到服务器**" 对话框中，输入 *（localdb） \v11.0*作为**服务器名称**，将 "**身份验证**" 设置为 " **Windows 身份验证**"，然后单击 "**连接**"。

    ![SSMS 连接到服务器](preparing-databases/_static/image10.png)
3. 在 "**对象资源管理器**" 窗口中，展开 "**数据库**"，右键单击 " **ContosoUniversity**"，单击 "**任务**"，然后单击 "**生成脚本**"。

    ![SSMS 生成脚本](preparing-databases/_static/image11.png)
4. 在 "**生成和发布脚本**" 对话框中，单击 "**设置脚本编写选项**"。

    您可以跳过 "**选择对象**" 步骤，因为默认值为 "**编写整个数据库的脚本" 和所有数据库对象**，并且这正是您所需要的。
5. 单击 **“高级”** 。

    ![SSMS 脚本选项](preparing-databases/_static/image12.png)
6. 在 "**高级脚本编写选项**" 对话框中，向下滚动到 "要**编写脚本的数据类型**"，然后单击下拉列表中的 "**仅数据**" 选项。
7. Change **SCRIPT USE DATABASE** to **False**。 USE 语句对于 Azure SQL 数据库无效，且在测试环境中部署到 SQL Server Express 时不需要这些语句。

    ![仅限 SSMS 脚本数据，无 USE 语句](preparing-databases/_static/image13.png)
8. 单击“确定”。
9. 在 "**生成和发布脚本**" 对话框中， **"文件名" 框指定**将创建脚本的位置。 更改解决方案文件夹（包含 ContosoUniversity 文件的文件夹）的路径，将文件名更改为*aspnet-data-dev*。
10. 单击 "**下一步**" 以切换到 "**摘要**" 选项卡，然后再次单击 "**下一步**" 以创建脚本。

    ![已创建 SSMS 脚本](preparing-databases/_static/image14.png)
11. 单击“完成”。

### <a name="create-the-production-database-script"></a>创建生产数据库脚本

由于尚未在生产数据库中运行该项目，因此它尚未附加到 LocalDB 实例。 因此，您需要首先附加数据库。

1. 在 SSMS**对象资源管理器**中，右键单击 "**数据库**"，然后单击 "**附加**"。

    ![SSMS 附加](preparing-databases/_static/image15.png)
2. 在 "**附加数据库**" 对话框中，单击 "**添加**"，然后导航到*应用\_Data* "文件夹中的*aspnet-ContosoUniversity-Prod*文件。

     ![SSMS 添加要附加的 .mdf 文件](preparing-databases/_static/image16.png)
3. 单击“确定”。
4. 按照前面使用的相同过程为生产文件创建脚本。 将脚本文件命名为*aspnet-data-prod*。

## <a name="summary"></a>摘要

现在，两个数据库都已准备好进行部署，您的解决方案文件夹中有两个数据部署脚本。

![数据部署脚本](preparing-databases/_static/image17.png)

在以下教程中，你将配置影响部署的项目设置，并为已部署的应用程序中必须不同的设置设置自动的*web.config*文件转换。

## <a name="more-information"></a>详细信息

有关 NuGet 的详细信息，请参阅通过 NuGet 和[Nuget 文档](http://docs.nuget.org/docs/start-here/overview)[管理项目库](https://msdn.microsoft.com/magazine/hh547106.aspx)。 如果你不想使用 NuGet，你将需要了解如何分析 NuGet 包，以确定它在安装时执行的操作。 （例如，它可能配置*web.config*转换、将 PowerShell 脚本配置为在生成时运行，等等）若要详细了解 NuGet 的工作原理，请参阅[创建和发布包](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package)、[配置文件和源代码转换](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)。

> [!div class="step-by-step"]
> [上一页](introduction.md)
> [下一页](web-config-transformations.md)
