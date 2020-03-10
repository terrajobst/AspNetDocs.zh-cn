---
uid: identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
title: ASP.NET Identity：将 MySQL 存储用于 EntityFramework MySQL 提供程序（C#）-ASP.NET 4。x
author: maumar
description: 本教程介绍如何使用 EntityFramework （SQL 客户端提供程序）将用于 ASP.NET Identity 的默认数据存储机制替换为 MySQL 签约 。
ms.author: riande
ms.date: 12/10/2013
ms.assetid: 15253312-a92c-43ba-908e-b5dacd3d08b8
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider
msc.type: authoredcontent
ms.openlocfilehash: e89ed139657c5ce9ddcc56879946c62038919483
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471872"
---
# <a name="aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider-c"></a>ASP.NET Identity：将 MySQL 存储用于 EntityFramework MySQL 提供程序（C#）

作者： [Maurycy Markowski](https://github.com/maumar)， [Raquel Soares De Almeida](https://github.com/raquelsa)， [Robert mcmurray 有关](https://github.com/rmcmurray)

> 本教程介绍如何使用 EntityFramework （SQL 客户端提供程序）将[**ASP.NET Identity**](introduction-to-aspnet-identity.md)的默认数据存储机制替换为 MySQL 提供程序。

本教程将介绍以下主题：

- 在 Azure 上创建 MySQL 数据库
- 使用 Visual Studio 2013 MVC 模板创建 MVC 应用程序
- 将 EntityFramework 配置为使用 MySQL 数据库提供程序
- 运行应用程序以验证结果

在本教程结束时，将拥有一个 MVC 应用程序，其中包含使用 Azure 中托管的 MySQL 数据库的 ASP.NET Identity 存储。

## <a name="creating-a-mysql-database-instance-on-azure"></a>在 Azure 上创建 MySQL 数据库实例

1. 登录到 [Azure 门户](https://go.microsoft.com/fwlink/?linkid=529715&amp;clcid=0x409)。
2. 单击页面底部的 "**新建**"，然后选择 "**存储**"：

    [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.png)
3. 在 "**选择和外接程序**" 向导中，选择 " **ClearDB MySQL 数据库**"，然后单击框架底部的 "**下一步**" 箭头：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.png)
4. 保留默认的 "**免费**计划"，将**名称**更改为**IdentityMySQLDatabase**，选择离你最近的区域，然后单击框架底部的**下一步**箭头：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.png)
5. 单击 "**购买**" 复选标记以完成数据库创建。

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.png)
6. 在创建数据库后，可以从管理门户中的“外接程序”选项卡管理该数据库。 若要检索数据库的连接信息，请单击页面底部的 "**连接信息**"：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image10.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image9.png)
7. 通过单击**CONNECTIONSTRING**字段的复制按钮并保存来复制连接字符串;稍后在本教程中，你将在 MVC 应用程序中使用此信息：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image12.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image11.png)

## <a name="creating-an-mvc-application-project"></a>创建 MVC 应用程序项目

若要完成本教程的此部分中的步骤，首先需要安装[Visual Studio Express 2013 For Web](https://go.microsoft.com/fwlink/?LinkId=299058)或[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)。 安装 Visual Studio 后，请使用以下步骤创建新的 MVC 应用程序项目：

1. 打开 Visual Studio 2103。
2. 在**起始**页上单击 "**新建项目**"，或者单击 "**文件**" 菜单，然后单击 "**新建项目**"：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image2.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image1.jpg)
3. 当显示 "**新建项目**" 对话框时，展开模板列表中的 "**视觉C#对象**"，然后单击 " **web**"，然后选择 " **ASP.NET Web 应用程序**"。 将项目命名为 " **IdentityMySQLDemo** "，然后单击 **"确定"** ：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image14.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image13.png)
4. 在 "**新建 ASP.NET 项目**" 对话框中，选择 " **MVC** templatewith" 默认选项;这会将**各个用户帐户**配置为身份验证方法。 单击“确定”：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image16.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image15.png)

## <a name="configure-entityframework-to-work-with-a-mysql-database"></a>将 EntityFramework 配置为使用 MySQL 数据库

### <a name="update-the-entity-framework-assembly-for-your-project"></a>更新项目的实体框架程序集

从 Visual Studio 2013 模板创建的 MVC 应用程序包含对[EntityFramework 6.0.0](http://www.nuget.org/packages/EntityFramework)包的引用，但由于该程序集的版本包含显著的性能改进，因此对该程序集进行了更新。 若要在应用程序中使用这些最新的更新，请使用以下步骤。

1. 在 Visual Studio 中打开 MVC 项目。
2. 单击 "**工具**"，然后单击 " **NuGet 程序包管理器**"，然后单击 "**程序包管理器控制台**"：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image18.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image17.png)
3. **程序包管理器控制台**将显示在 Visual Studio 的底部。 键入 &quot;**更新-Package EntityFramework**&quot; 并按 enter：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image20.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image19.png)

### <a name="install-the-mysql-provider-for-entityframework"></a>安装适用于 EntityFramework 的 MySQL 提供程序

为了使 EntityFramework 能够连接到 MySQL 数据库，需要安装 MySQL 提供程序。 为此，请打开 "**程序包管理器控制台**"，然后键入 &quot;**安装-Package MySql.** &quot;，然后按 enter。

> [!NOTE]
> 这是程序集的预发布版本，因此它可能包含 bug。 不应在生产中使用提供程序的预发布版本。

[单击下图以将其展开。]

[![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image22.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image21.png)

### <a name="making-project-configuration-changes-to-the-webconfig-file-for-your-application"></a>对应用程序的 web.config 文件进行项目配置更改

在本部分中，你将配置实体框架以使用刚刚安装的 MySQL 提供程序，注册 MySQL 提供程序工厂，并添加 Azure 中的连接字符串。

> [!NOTE]
> 下面的示例包含用于 MySql 的特定程序集版本。 如果程序集版本发生更改，你将需要修改版本正确的适当配置设置。

1. 在 Visual Studio 2013 中打开项目的 web.config 文件。
2. 找到以下配置设置，这些设置为实体框架定义默认的数据库提供程序和工厂：

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample1.xml)]
3. 将这些配置设置替换为以下内容，这会将实体框架配置为使用 MySQL 提供程序：

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample2.xml)]
4. 找到 &lt;connectionStrings&gt; 部分，并将其替换为以下代码，此代码将定义托管在 Azure 上的 MySQL 数据库的连接字符串（请注意，providerName 值也已从原始值更改）：

    [!code-xml[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample3.xml?highlight=3-4)]

### <a name="adding-custom-migrationhistory-context"></a>添加自定义 MigrationHistory 上下文

实体框架 Code First 使用**MigrationHistory**表跟踪模型更改，并确保数据库架构和概念架构之间的一致性。 但是，默认情况下，此表不适用于 MySQL，因为主密钥太大。 若要纠正这种情况，需要为该表缩减密钥大小。 为此，请使用以下步骤：

1. 此表的架构信息是在**HistoryContext**中捕获的，可以将其修改为任何其他**DbContext**。 为此，请将名为**MySqlHistoryContext.cs**的新类文件添加到项目中，并将其内容替换为以下代码：

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample4.cs)]
2. 接下来，需要将实体框架配置为使用修改后的**HistoryContext**而不是默认值。 这可以通过使用基于代码的配置功能来实现。 为此，请将名为**MySqlConfiguration.cs**的新类文件添加到项目中，并将其内容替换为：

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample5.cs)]

### <a name="creating-a-custom-entityframework-initializer-for-applicationdbcontext"></a>为 ApplicationDbContext 创建自定义 EntityFramework 初始值设定项

本教程中介绍的 MySQL 提供程序当前不支持实体框架迁移，因此你需要使用模型初始值设定项来连接到数据库。 由于本教程使用的是 Azure 上的 MySQL 实例，因此你将需要创建一个自定义实体框架初始值设定项。

> [!NOTE]
> 如果要连接到 Azure 上的 SQL Server 实例，或者使用在本地托管的数据库，则不需要执行此步骤。

若要为 MySQL 创建自定义实体框架初始值设定项，请使用以下步骤：

1. 将名为**MySqlInitializer.cs**的新类文件添加到项目中，并将其内容替换为以下代码：

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample6.cs?highlight=23)]
2. 打开项目的**IdentityModels.cs**文件，该文件位于 "**模型**" 目录中，并将其内容替换为以下内容：

    [!code-csharp[Main](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/samples/sample7.cs)]

## <a name="running-the-application-and-verifying-the-database"></a>运行应用程序并验证数据库

完成前面几节中的步骤后，应测试数据库。 为此，请使用以下步骤：

1. 按**Ctrl + F5**生成并运行 web 应用程序。
2. 单击页面顶部的 "**注册**" 选项卡：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image4.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image3.jpg)
3. 输入新用户名和密码，然后单击 "**注册**"：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image24.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image23.png)
4. 此时，将在 MySQL 数据库上创建 ASP.NET Identity 表，并注册该用户并将其记录到应用程序中：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image6.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image5.jpg)

### <a name="installing-mysql-workbench-tool-to-verify-the-data"></a>安装 MySQL 工作台工具以验证数据

1. 从[mysql 下载页面](http://dev.mysql.com/downloads/windows/installer/)安装**mysql 工作台**工具
2. 在安装向导中： "**功能选择**" 选项卡上，选择 "**应用程序**" 部分下的**MySQL 工作台**。
3. 启动应用并使用在本教程的 begging 中创建的 Azure MySQL 数据库中的连接字符串数据添加新连接。
4. 建立连接后，检查在 IdentityMySQLDatabase 上创建的**ASP.NET Identity**表 **。**
5. 你将看到，创建了所有 ASP.NET Identity 必需的表，如下图所示：

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image8.jpg)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image7.jpg)
6. 检查**aspnetusers**表中的实例，以便在注册新用户时检查条目。

   [单击下图以将其展开。 ] [![](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image26.png)](aspnet-identity-using-mysql-storage-with-an-entityframework-mysql-provider/_static/image25.png)
