---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: 实现自定义 MySQL ASP.NET Identity 存储提供程序-ASP.NET 4。x
author: raquelsa
description: ASP.NET Identity 是一种可扩展系统，可让你创建自己的存储提供程序，并将其插入应用程序，而无需重新运行应用 。
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 2f0b47d45bce82c71d1864536309f9e2ffed2d63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500066"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>实现自定义 MySQL ASP.NET Identity 存储提供程序

作者： [Raquel Soares De Almeida](https://github.com/raquelsa)， [Suhas Joshi](https://github.com/suhasj)， [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET Identity 是一种可扩展系统，可让你创建自己的存储提供程序，并将其插入到应用程序中，而无需重新运行应用程序。 本主题介绍如何为 ASP.NET Identity 创建 MySQL 存储提供程序。 有关创建自定义存储提供程序的概述，请参阅[ASP.NET Identity 的自定义存储提供程序概述](overview-of-custom-storage-providers-for-aspnet-identity.md)。
> 
> 若要完成本教程，您必须具有更新 2 Visual Studio 2013。
> 
> 本教程将：
> 
> - 演示如何在 Azure 上创建 MySQL 数据库实例。
> - 演示如何使用 MySQL 客户端工具（MySQL 工作台）在 Azure 上创建表和管理远程数据库。
> - 介绍如何将默认的 ASP.NET Identity 存储实现替换为 MVC 应用程序项目中的自定义实现。
> 
> 本教程最初是通过 Raquel Soares De Almeida 和 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）编写的。 Suhas Joshi 为标识2.0 更新了示例项目。 本主题已通过 Tom FitzMacken 为标识2.0 更新。

## <a name="download-completed-project"></a>下载完成的项目

在本教程结束时，你将拥有一个 ASP.NET Identity 使用在 Azure 上托管的 MySQL 数据库的 MVC 应用程序项目。

可以在[AspNet. node.js （GitHub）](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL)下载已完成的 MySQL 存储提供程序。

## <a name="the-steps-you-will-perform"></a>将执行的步骤

在本教程中你将：

1. 在 Azure 上创建 MySQL 数据库
2. 在 MySQL 中创建 ASP.NET Identity 表
3. 创建 MVC 应用程序并将其配置为使用 MySQL 提供程序
4. 运行应用

本主题不涵盖 ASP.NET Identity 的体系结构，以及在实现客户存储提供商时必须做出的决策。 有关详细信息，请参阅[ASP.NET Identity 的自定义存储提供程序概述](overview-of-custom-storage-providers-for-aspnet-identity.md)。

## <a name="review-mysql-storage-provider-classes"></a>查看 MySQL 存储提供程序类

在转到创建 MySQL 存储提供程序的步骤之前，让我们先看一下构成存储提供程序的类。 你需要的类可管理从应用程序调用的数据库操作和类，以管理用户和角色。

### <a name="storage-classes"></a>存储类

- [IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -包含用户的属性。
- [UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) -包含添加、更新或检索用户的操作。
- [IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -包含角色的属性。
- [RoleStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) -包含添加、删除、更新和检索角色的操作。

### <a name="data-access-layer-classes"></a>数据访问层类

在此示例中，数据访问层类包含用于处理表的 SQL 语句;但是，在代码中，你可能需要使用对象关系映射（ORM），如实体框架或 NHibernate。 特别是，如果不包含包含延迟加载和对象缓存的 ORM，你的应用程序可能会遇到性能不佳的情况。 有关详细信息，请参阅[不实体框架 ASP.NET Identity 2.0？](https://aspnetidentity.codeplex.com/discussions/561828)

- [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -包含 MySQL 数据库连接和执行数据库操作的方法。 使用此类的实例来实例化 UserStore 和 RoleStore。
- [RoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) -包含用于存储角色的表的数据库操作。
- [UserClaimsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -包含用于存储用户声明的表的数据库操作。
- [UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -包含用于存储用户登录信息的表的数据库操作。
- [UserRoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -包含表的数据库操作，这些操作将存储哪些用户分配到哪些角色。
- [UserTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -包含用于存储用户的表的数据库操作。

## <a name="create-a-mysql-database-instance-on-azure"></a>在 Azure 上创建 MySQL 数据库实例

1. 登录到 [Azure 门户](https://manage.windowsazure.com/)。
2. 单击页面底部的 " **+ 新建**"，然后选择 "**存储**"。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. 在 "**选择和外接程序**" 向导中，选择 " **ClearDB MySQL 数据库**"，并单击对话框右下角的 "下一步" 箭头。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. 保留默认的 "**免费**" 计划，并将**名称**更改为**IdentityMySQLDatabase**。 选择离你最近的区域，然后单击 "下一步" 箭头。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. 单击复选标记以完成数据库创建。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. 在创建数据库后，可以从管理门户中的“外接程序”选项卡管理该数据库。   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. 可以通过单击页面底部的 "**连接信息**" 来获取数据库连接信息。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. 单击 "复制" 按钮以复制连接字符串，并将其保存，以便稍后在 MVC 应用程序中使用。   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>在 MySQL 数据库中创建 ASP.NET Identity 表

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>安装 MySQL 工作台工具以连接和管理 MySQL 数据库

1. 从[mysql 下载页面](http://dev.mysql.com/downloads/windows/installer/)安装**mysql 工作台**工具
2. 启动应用并单击 " **MySQLConnections +** " 按钮添加新连接。 使用您在本教程前面部分创建的 Azure MySQL 数据库中复制的连接字符串数据。
3. 建立连接后，请打开一个新的**查询**选项卡;将[MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)中的命令粘贴到查询中，并执行它以创建数据库表。
4. 现在，在 Azure 上托管的 MySQL 数据库上创建了所有 ASP.NET Identity 必需的表，如下所示。  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>从模板创建 MVC 应用程序项目，并将其配置为使用 MySQL 提供程序

如果需要，请为 Web 或更新2的[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)安装[Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。

### <a name="download-the-aspnetidentitymysql-project-from-github"></a>从 GitHub 下载 .asp .asp 项目

1. 浏览到 node.js [（GitHub）](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/)上的存储库 URL。
2. 下载源代码。
3. 将 .zip 文件解压缩到本地文件夹。
4. 打开 AspNet. node.js 解决方案并生成它。

### <a name="create-a-new-mvc-application-project-from-template"></a>通过模板创建新的 MVC 应用程序项目

1. 右键**单击 ""** **，然后**单击 "**新建项目**"
2. 在 "**添加新项目**" 对话框的左侧选择 "**视觉对象C#**  "，然后选择 " **web** "，然后选择 " **ASP.NET Web 应用程序**"。 将项目命名为**IdentityMySQLDemo**;然后单击 "确定"。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. 在 "**新建 ASP.NET 项目**" 对话框中，选择包含默认选项的 MVC 模板（其中包含**单独的用户帐户**作为身份验证方法），然后单击 **"确定"** 。![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. 在解决方案资源管理器中，右键单击 IdentityMySQLDemo 项目，然后选择 "**管理 NuGet 包**"。 在 "搜索文本框" 对话框中，键入**EntityFramework**。 在结果列表中选择此包，并单击 "**卸载**"。 系统将提示你卸载依赖项包 EntityFramework。 单击 "是"，因为此应用程序上不再有此包。
5. 右键单击 "IdentityMySQLDemo" 项目，选择 "**添加**"、"**引用"、"解决方案"、"项目**"，选择 "AspNet" 项目并单击 **"确定"** 。
6. 在 IdentityMySQLDemo 项目中，将所有引用替换为  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   替换为  
     `using AspNet.Identity.MySQL;`
7. 在 IdentityModels.cs 中，将**ApplicationDbContext**设置为从**MySqlDatabase**派生，并包含一个构造函数，该构造函数采用单个参数和连接名称。  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. 打开 IdentityConfig.cs 文件。 在**ApplicationUserManager**方法中，将实例化 UserManager 替换为以下代码：  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. 打开 web.config 文件并将 DefaultConnection 字符串替换为此项，将突出显示的值替换为前面步骤中创建的 MySQL 数据库的连接字符串：  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>运行应用并连接到 MySQL 数据库

1. 右键单击 " **IdentityMySQLDemo** " 项目，然后选择 "**设为启动项目**"
2. 按**Ctrl + F5**生成并运行应用。
3. 单击页面顶部的 "**注册**" 选项卡。
4. 输入新用户名和密码，然后单击 "**注册**"。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. 新用户现在已注册并登录。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. 返回到 MySQL 工作台工具并检查**IdentityMySQLDatabase**表的内容。 注册新用户时，请检查用户表中的条目。  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>后续步骤

有关如何在此应用上启用其他身份验证方法的详细信息，请参阅[使用 Facebook 和 Google OAuth2 创建 ASP.NET MVC 5 应用和 OpenID 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。

若要了解如何将 DB 与 OAuth 集成并设置角色，以限制用户对应用的访问权限，请参阅将[包含成员资格、OAuth 和 SQL 数据库的 Secure ASP.NET MVC 5 应用部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。
