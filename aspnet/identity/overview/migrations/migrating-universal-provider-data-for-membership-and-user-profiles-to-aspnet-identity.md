---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: 将成员身份和用户配置文件的通用提供程序数据C#迁移到 ASP.NET Identity （）-ASP.NET 4。x
author: rustd
description: 本教程介绍迁移使用现有应用通用提供程序创建的用户和角色数据和用户配置文件数据所需的步骤 。
ms.author: riande
ms.date: 12/13/2013
ms.custom: seoapril2019
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 31f02a0cec3c531c45c37b7aad8456e01e80b5ea
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456106"
---
# <a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a>将成员身份和用户配置文件的通用提供程序数据迁移到 ASP.NET Identity (C#)

作者： [Pranav rastogi 撰写](https://github.com/rustd)、 [Rick Anderson](https://twitter.com/RickAndMSFT)、 [Robert mcmurray 有关](https://github.com/rmcmurray)、 [Suhas Joshi](https://github.com/suhasj)

> 本教程介绍将使用现有应用程序通用提供程序创建的用户和角色数据和用户配置文件数据迁移到 ASP.NET Identity 模型所需的步骤。 此处所述的用于迁移用户配置文件数据的方法也可以在具有 SQL 成员身份的应用程序中使用。

随着 Visual Studio 2013 的发布，ASP.NET 团队引入了新的 ASP.NET Identity 系统，你可以在[此处](../../index.md)阅读有关该版本的详细信息。 本文介绍了如何将 web 应用程序从[SQL 成员身份迁移到新的标识系统](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)，本文介绍了将遵循提供程序模型的现有应用程序迁移到新的标识模型的步骤。 本教程的重点是迁移用户配置文件数据，将其无缝地挂钩到新系统。 迁移用户和角色信息与 SQL 成员身份类似。 迁移配置文件数据后的方法也可在具有 SQL 成员身份的应用程序中使用。

例如，我们将从使用提供程序模型的 Visual Studio 2012 创建的 web 应用开始。 接下来，我们将添加用于配置文件管理的代码，注册用户，为用户添加配置文件数据，迁移数据库架构，然后将应用程序更改为使用标识系统进行用户和角色管理。 作为迁移测试，使用通用提供程序创建的用户应能够登录，并且新用户应该能够注册。

> [!NOTE]
> 可以在[https://github.com/suhasj/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations)找到完整示例。

## <a name="profile-data-migration-summary"></a>配置文件数据迁移摘要

在开始迁移之前，让我们看一下如何在提供程序模型中存储配置文件数据。 应用程序用户的配置文件数据可以通过多种方式进行存储，最常见的方法是使用随通用提供程序提供的内置配置文件提供程序。 步骤包括

1. 添加一个具有用于存储配置文件数据的属性的类。
2. 添加一个扩展 "ProfileBase" 的类，并实现方法以获取用户的上述配置文件数据。
3. 启用 web.config 文件中的默认配置*文件提供*程序，并定义在步骤 #2 中声明的类，以便在访问配置文件信息时使用。

配置文件信息作为序列化的 xml 和二进制数据存储在数据库的 "配置文件" 表中。

迁移应用程序以使用新的 ASP.NET Identity 系统后，配置文件信息将反序列化并存储为用户类的属性。 然后，可以将每个属性映射到用户表中的列。 此处的优点是，属性可以直接使用 user 类，而不必在每次访问数据信息时都对其进行序列化/反序列化。

## <a name="getting-started"></a>入门

1. 在 Visual Studio 2012 中创建新的 ASP.NET 4.5 Web 窗体应用程序。 当前示例使用 Web 窗体模板，但也可以使用 MVC 应用程序。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. 创建新的文件夹 "模型" 以存储配置文件信息  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. 例如，让我们在配置文件中存储用户的出生日期、城市、高度和权重。 高度和权重存储为名为 "PersonalStats" 的自定义类。 若要存储和检索配置文件，需要一个扩展了 "ProfileBase" 的类。 让我们创建一个新类 "AppProfile" 以获取和存储配置文件信息。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. 启用*web.config 文件中的配置文件。* 输入用于存储/检索在步骤 #3 中创建的用户信息的类名称。

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. 在 "帐户" 文件夹中添加一个 web 窗体页面，以获取用户的配置文件数据并将其存储。 右键单击 "项目"，然后选择 "添加新项"。 添加带有母版页 "AddProfileData" 的新 webforms 页面。 将以下内容复制到 "MainContent" 部分：

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

   在代码隐藏中添加以下代码：

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

   添加用于定义 AppProfile 类的命名空间，以删除编译错误。
6. 运行应用并创建用户名为 "**olduser"** 的新用户。 导航到 "AddProfileData" 页，并为用户添加配置文件信息。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

您可以使用 "服务器资源管理器" 窗口验证数据是否作为序列化的 xml 存储在 "配置文件" 表中。 在 Visual Studio 的 "视图" 菜单中，选择 "服务器资源管理器"。 应为*web.config*文件中定义的数据库提供数据连接。 单击数据连接将显示不同的子类别。 展开 "表" 以显示数据库中的不同表，右键单击 "配置文件"，然后选择 "显示表数据" 以查看存储在配置文件表中的配置文件数据。

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a>迁移数据库架构

为了使现有数据库与标识系统一起工作，我们需要更新标识数据库中的架构，以支持添加到原始数据库中的字段。 这可以通过使用 SQL 脚本来创建新表并复制现有信息来实现。 在 "服务器资源管理器" 窗口中，展开 "DefaultConnection" 以显示表。 右键单击 "表" 并选择 "新建查询"

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

粘贴[https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt)的 SQL 脚本，然后运行该脚本。 如果刷新了 "DefaultConnection"，则可以看到添加了新表。 可以检查表中的数据，以查看信息是否已迁移。

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a>正在迁移应用程序以使用 ASP.NET Identity

1. 安装 ASP.NET Identity 所需的 Nuget 包：

    - Microsoft.AspNet.Identity.EntityFramework
    - Microsoft.AspNet.Identity.Owin
    - Microsoft.Owin.Host.SystemWeb
    - Microsoft.Owin.Security.Facebook
    - Microsoft.Owin.Security.Google
    - Microsoft.Owin.Security.MicrosoftAccount
    - Microsoft.Owin.Security.Twitter

   可在[此处](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog)找到有关管理 Nuget 包的详细信息
2. 若要处理表中的现有数据，需要创建模型类，这些类映射回表并在标识系统中将它们挂钩。 作为标识协定的一部分，模型类应实现在 EntityFramework 中定义的接口，或者可以扩展这些接口在中的现有实现方式。 我们将使用现有的角色类、用户登录名和用户声明。 对于我们的示例，我们需要使用自定义用户。 右键单击该项目，然后创建新文件夹 "IdentityModels"。 添加新的 "User" 类，如下所示：

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

   请注意，"ProfileInfo" 现在是 user 类的属性。 因此，我们可以使用 user 类直接处理配置文件数据。

从下载源（ [https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ）复制**IdentityModels**和**IdentityAccount**文件夹中的文件。 它们具有使用 ASP.NET Identity Api 的其他模型类和用户和角色管理所需的新页面。 使用的方法与 SQL 成员身份类似，可以在[此处](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)找到详细说明。

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

## <a name="copying-profile-data-to-the-new-tables"></a>将配置文件数据复制到新表

如前文所述，我们需要在配置文件表中反序列化 xml 数据，并将其存储在 AspNetUsers 表的列中。 新列是在上一步的 "用户" 表中创建的，因此，剩下的就是用所需的数据填充这些列。 为此，我们将使用控制台应用程序，该应用程序将运行一次，以便在用户表中填充新创建的列。

1. 在现有解决方案中创建新的控制台应用程序。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. 安装最新版本的实体框架包。
3. 将上面创建的 web 应用程序添加到控制台应用程序的引用中。 要执行此操作，请右键单击项目，然后单击 "添加引用"，然后单击 "解决方案"，然后单击项目，并单击 "确定"。
4. 将下面的代码复制到 Program.cs 类中。 此逻辑读取每个用户的配置文件数据，将其序列化为 "ProfileInfo" 对象，并将其存储回数据库。

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

   某些使用的模型是在 web 应用程序项目的 "IdentityModels" 文件夹中定义的，因此您必须包含相应的命名空间。
5. 上述代码适用于在之前步骤中创建的 web 应用程序项目\_Data 文件夹中的数据库文件。 若要引用该，请将控制台应用程序的 app.config 文件中的连接字符串更新为 web 应用程序的 web.config 中的连接字符串。 还提供 "AttachDbFilename" 属性中的完整物理路径。
6. 打开命令提示符并导航到上述控制台应用程序的 bin 文件夹。 运行可执行文件，并查看日志输出，如下图所示。  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. 在服务器资源管理器中打开 "AspNetUsers" 表，并验证包含属性的新列中的数据。 应将这些属性值更新为相应的属性值。

## <a name="verify-functionality"></a>验证功能

使用通过 ASP.NET Identity 实现的新添加的成员资格页从旧数据库登录用户。 用户应能够使用相同的凭据登录。 尝试其他功能，例如添加 OAuth、创建新用户、更改密码、添加角色、将用户添加到角色等。

应检索旧用户和新用户的配置文件数据，并将其存储在用户表中。 不应再引用旧表。

## <a name="conclusion"></a>结束语

本文介绍了将使用提供程序模型进行成员身份 ASP.NET Identity 的 web 应用程序迁移到的过程。 此外，还概述了如何将用户的配置文件数据迁移到标识系统。 有关迁移应用时遇到的问题和问题，请在下面留下评论。

*感谢 Rick Anderson 和 Robert Mcmurray 有关，用于查看本文。*
