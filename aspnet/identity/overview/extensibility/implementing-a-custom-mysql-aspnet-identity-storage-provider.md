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
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a><span data-ttu-id="0b38e-103">实现自定义 MySQL ASP.NET Identity 存储提供程序</span><span class="sxs-lookup"><span data-stu-id="0b38e-103">Implementing a Custom MySQL ASP.NET Identity Storage Provider</span></span>

<span data-ttu-id="0b38e-104">作者： [Raquel Soares De Almeida](https://github.com/raquelsa)， [Suhas Joshi](https://github.com/suhasj)， [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="0b38e-104">by [Raquel Soares De Almeida](https://github.com/raquelsa), [Suhas Joshi](https://github.com/suhasj), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="0b38e-105">ASP.NET Identity 是一种可扩展系统，可让你创建自己的存储提供程序，并将其插入到应用程序中，而无需重新运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0b38e-105">ASP.NET Identity is an extensible system which enables you to create your own storage provider and plug it into your application without re-working the application.</span></span> <span data-ttu-id="0b38e-106">本主题介绍如何为 ASP.NET Identity 创建 MySQL 存储提供程序。</span><span class="sxs-lookup"><span data-stu-id="0b38e-106">This topic describes how to create a MySQL storage provider for ASP.NET Identity.</span></span> <span data-ttu-id="0b38e-107">有关创建自定义存储提供程序的概述，请参阅[ASP.NET Identity 的自定义存储提供程序概述](overview-of-custom-storage-providers-for-aspnet-identity.md)。</span><span class="sxs-lookup"><span data-stu-id="0b38e-107">For an overview of creating custom storage providers, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>
> 
> <span data-ttu-id="0b38e-108">若要完成本教程，您必须具有更新 2 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="0b38e-108">To complete this tutorial, you must have Visual Studio 2013 with Update 2.</span></span>
> 
> <span data-ttu-id="0b38e-109">本教程将：</span><span class="sxs-lookup"><span data-stu-id="0b38e-109">This tutorial will:</span></span>
> 
> - <span data-ttu-id="0b38e-110">演示如何在 Azure 上创建 MySQL 数据库实例。</span><span class="sxs-lookup"><span data-stu-id="0b38e-110">Show how to create a MySQL database instance on Azure.</span></span>
> - <span data-ttu-id="0b38e-111">演示如何使用 MySQL 客户端工具（MySQL 工作台）在 Azure 上创建表和管理远程数据库。</span><span class="sxs-lookup"><span data-stu-id="0b38e-111">Show how to use a MySQL client tool (MySQL Workbench) to create tables and manage your remote database on Azure.</span></span>
> - <span data-ttu-id="0b38e-112">介绍如何将默认的 ASP.NET Identity 存储实现替换为 MVC 应用程序项目中的自定义实现。</span><span class="sxs-lookup"><span data-stu-id="0b38e-112">Show how to replace the default ASP.NET Identity storage implementation with our custom implementation on a MVC application project.</span></span>
> 
> <span data-ttu-id="0b38e-113">本教程最初是通过 Raquel Soares De Almeida 和 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）编写的。</span><span class="sxs-lookup"><span data-stu-id="0b38e-113">This tutorial was originally written by Raquel Soares De Almeida and Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).</span></span> <span data-ttu-id="0b38e-114">Suhas Joshi 为标识2.0 更新了示例项目。</span><span class="sxs-lookup"><span data-stu-id="0b38e-114">The sample project was updated for Identity 2.0 by Suhas Joshi.</span></span> <span data-ttu-id="0b38e-115">本主题已通过 Tom FitzMacken 为标识2.0 更新。</span><span class="sxs-lookup"><span data-stu-id="0b38e-115">The topic was updated for Identity 2.0 by Tom FitzMacken.</span></span>

## <a name="download-completed-project"></a><span data-ttu-id="0b38e-116">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="0b38e-116">Download completed project</span></span>

<span data-ttu-id="0b38e-117">在本教程结束时，你将拥有一个 ASP.NET Identity 使用在 Azure 上托管的 MySQL 数据库的 MVC 应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="0b38e-117">At the end of this tutorial, you will have an MVC application project with ASP.NET Identity working with a MySQL database hosted on Azure.</span></span>

<span data-ttu-id="0b38e-118">可以在[AspNet. node.js （GitHub）](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL)下载已完成的 MySQL 存储提供程序。</span><span class="sxs-lookup"><span data-stu-id="0b38e-118">You can download the completed MySQL storage provider at [AspNet.Identity.MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL).</span></span>

## <a name="the-steps-you-will-perform"></a><span data-ttu-id="0b38e-119">将执行的步骤</span><span class="sxs-lookup"><span data-stu-id="0b38e-119">The steps you will perform</span></span>

<span data-ttu-id="0b38e-120">在本教程中你将：</span><span class="sxs-lookup"><span data-stu-id="0b38e-120">In this tutorial you will:</span></span>

1. <span data-ttu-id="0b38e-121">在 Azure 上创建 MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="0b38e-121">Create a MySQL database on Azure</span></span>
2. <span data-ttu-id="0b38e-122">在 MySQL 中创建 ASP.NET Identity 表</span><span class="sxs-lookup"><span data-stu-id="0b38e-122">Create the ASP.NET Identity tables in MySQL</span></span>
3. <span data-ttu-id="0b38e-123">创建 MVC 应用程序并将其配置为使用 MySQL 提供程序</span><span class="sxs-lookup"><span data-stu-id="0b38e-123">Create an MVC application and configure it to use the MySQL provider</span></span>
4. <span data-ttu-id="0b38e-124">运行应用</span><span class="sxs-lookup"><span data-stu-id="0b38e-124">Run the app</span></span>

<span data-ttu-id="0b38e-125">本主题不涵盖 ASP.NET Identity 的体系结构，以及在实现客户存储提供商时必须做出的决策。</span><span class="sxs-lookup"><span data-stu-id="0b38e-125">This topic does not cover the architecture of ASP.NET Identity and the decisions you must make when implementing a customer storage provider.</span></span> <span data-ttu-id="0b38e-126">有关详细信息，请参阅[ASP.NET Identity 的自定义存储提供程序概述](overview-of-custom-storage-providers-for-aspnet-identity.md)。</span><span class="sxs-lookup"><span data-stu-id="0b38e-126">For that information, see [Overview of Custom Storage Providers for ASP.NET Identity](overview-of-custom-storage-providers-for-aspnet-identity.md).</span></span>

## <a name="review-mysql-storage-provider-classes"></a><span data-ttu-id="0b38e-127">查看 MySQL 存储提供程序类</span><span class="sxs-lookup"><span data-stu-id="0b38e-127">Review MySQL storage provider classes</span></span>

<span data-ttu-id="0b38e-128">在转到创建 MySQL 存储提供程序的步骤之前，让我们先看一下构成存储提供程序的类。</span><span class="sxs-lookup"><span data-stu-id="0b38e-128">Before jumping into the steps to create the MySQL storage provider, let's look at the classes that make up the storage provider.</span></span> <span data-ttu-id="0b38e-129">你需要的类可管理从应用程序调用的数据库操作和类，以管理用户和角色。</span><span class="sxs-lookup"><span data-stu-id="0b38e-129">You will need classes that manage the database operations and classes that are called from the application to manage users and roles.</span></span>

### <a name="storage-classes"></a><span data-ttu-id="0b38e-130">存储类</span><span class="sxs-lookup"><span data-stu-id="0b38e-130">Storage classes</span></span>

- <span data-ttu-id="0b38e-131">[IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) -包含用户的属性。</span><span class="sxs-lookup"><span data-stu-id="0b38e-131">[IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) - contains properties for the user.</span></span>
- <span data-ttu-id="0b38e-132">[UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) -包含添加、更新或检索用户的操作。</span><span class="sxs-lookup"><span data-stu-id="0b38e-132">[UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) - contains operations for adding, updating or retrieving users.</span></span>
- <span data-ttu-id="0b38e-133">[IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) -包含角色的属性。</span><span class="sxs-lookup"><span data-stu-id="0b38e-133">[IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) - contains properties for roles.</span></span>
- <span data-ttu-id="0b38e-134">[RoleStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) -包含添加、删除、更新和检索角色的操作。</span><span class="sxs-lookup"><span data-stu-id="0b38e-134">[RoleStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) - contains operations for adding, deleting, updating and retrieving roles.</span></span>

### <a name="data-access-layer-classes"></a><span data-ttu-id="0b38e-135">数据访问层类</span><span class="sxs-lookup"><span data-stu-id="0b38e-135">Data access layer classes</span></span>

<span data-ttu-id="0b38e-136">在此示例中，数据访问层类包含用于处理表的 SQL 语句;但是，在代码中，你可能需要使用对象关系映射（ORM），如实体框架或 NHibernate。</span><span class="sxs-lookup"><span data-stu-id="0b38e-136">For this example, the data access layer classes contain SQL statements for working with the tables; however, in your code you might want to use object-relational mapping (ORM) such as Entity Framework or NHibernate.</span></span> <span data-ttu-id="0b38e-137">特别是，如果不包含包含延迟加载和对象缓存的 ORM，你的应用程序可能会遇到性能不佳的情况。</span><span class="sxs-lookup"><span data-stu-id="0b38e-137">In particular, your application may experience poor performance without an ORM that includes lazy loading and object caching.</span></span> <span data-ttu-id="0b38e-138">有关详细信息，请参阅[不实体框架 ASP.NET Identity 2.0？](https://aspnetidentity.codeplex.com/discussions/561828)</span><span class="sxs-lookup"><span data-stu-id="0b38e-138">For more information, see [ASP.NET Identity 2.0 without Entity Framework?](https://aspnetidentity.codeplex.com/discussions/561828)</span></span>

- <span data-ttu-id="0b38e-139">[MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) -包含 MySQL 数据库连接和执行数据库操作的方法。</span><span class="sxs-lookup"><span data-stu-id="0b38e-139">[MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) - contains the MySQL database connection and methods for performing database operations.</span></span> <span data-ttu-id="0b38e-140">使用此类的实例来实例化 UserStore 和 RoleStore。</span><span class="sxs-lookup"><span data-stu-id="0b38e-140">UserStore and RoleStore are both instantiated with an instance of this class.</span></span>
- <span data-ttu-id="0b38e-141">[RoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) -包含用于存储角色的表的数据库操作。</span><span class="sxs-lookup"><span data-stu-id="0b38e-141">[RoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) - contains database operations for the table that stores roles.</span></span>
- <span data-ttu-id="0b38e-142">[UserClaimsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) -包含用于存储用户声明的表的数据库操作。</span><span class="sxs-lookup"><span data-stu-id="0b38e-142">[UserClaimsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) - contains database operations for the table that stores user claims.</span></span>
- <span data-ttu-id="0b38e-143">[UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) -包含用于存储用户登录信息的表的数据库操作。</span><span class="sxs-lookup"><span data-stu-id="0b38e-143">[UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) - contains database operations for the table that stores user login information.</span></span>
- <span data-ttu-id="0b38e-144">[UserRoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) -包含表的数据库操作，这些操作将存储哪些用户分配到哪些角色。</span><span class="sxs-lookup"><span data-stu-id="0b38e-144">[UserRoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) - contains database operations for the table that stores which users are assigned to which roles.</span></span>
- <span data-ttu-id="0b38e-145">[UserTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -包含用于存储用户的表的数据库操作。</span><span class="sxs-lookup"><span data-stu-id="0b38e-145">[UserTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) - contains database operations for the table that stores users.</span></span>

## <a name="create-a-mysql-database-instance-on-azure"></a><span data-ttu-id="0b38e-146">在 Azure 上创建 MySQL 数据库实例</span><span class="sxs-lookup"><span data-stu-id="0b38e-146">Create a MySQL database instance on Azure</span></span>

1. <span data-ttu-id="0b38e-147">登录到 [Azure 门户](https://manage.windowsazure.com/)。</span><span class="sxs-lookup"><span data-stu-id="0b38e-147">Log in to the [Azure Portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="0b38e-148">单击页面底部的 " **+ 新建**"，然后选择 "**存储**"。</span><span class="sxs-lookup"><span data-stu-id="0b38e-148">Click **+NEW** at the bottom of the page, and then select **STORE**.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. <span data-ttu-id="0b38e-149">在 "**选择和外接程序**" 向导中，选择 " **ClearDB MySQL 数据库**"，并单击对话框右下角的 "下一步" 箭头。</span><span class="sxs-lookup"><span data-stu-id="0b38e-149">In the **Choose and Add-on** wizard, select **ClearDB MySQL Database** and click on the next arrow at the bottom right of the dialog.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. <span data-ttu-id="0b38e-150">保留默认的 "**免费**" 计划，并将**名称**更改为**IdentityMySQLDatabase**。</span><span class="sxs-lookup"><span data-stu-id="0b38e-150">Keep the default **Free** plan and change the **Name** to **IdentityMySQLDatabase**.</span></span> <span data-ttu-id="0b38e-151">选择离你最近的区域，然后单击 "下一步" 箭头。</span><span class="sxs-lookup"><span data-stu-id="0b38e-151">Select the region nearest you and then click the next arrow.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. <span data-ttu-id="0b38e-152">单击复选标记以完成数据库创建。</span><span class="sxs-lookup"><span data-stu-id="0b38e-152">Click the checkmark to complete the database creation.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. <span data-ttu-id="0b38e-153">在创建数据库后，可以从管理门户中的“外接程序”选项卡管理该数据库。</span><span class="sxs-lookup"><span data-stu-id="0b38e-153">After your database has been created, you can manage it from the **ADD-ONS** tab in the management portal.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. <span data-ttu-id="0b38e-154">可以通过单击页面底部的 "**连接信息**" 来获取数据库连接信息。</span><span class="sxs-lookup"><span data-stu-id="0b38e-154">You can get the database connection information by clicking on **CONNECTION INFO** at the bottom of the page.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. <span data-ttu-id="0b38e-155">单击 "复制" 按钮以复制连接字符串，并将其保存，以便稍后在 MVC 应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="0b38e-155">Copy the connection string by clicking on the copy button and save it so you can use later in your MVC application.</span></span>   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a><span data-ttu-id="0b38e-156">在 MySQL 数据库中创建 ASP.NET Identity 表</span><span class="sxs-lookup"><span data-stu-id="0b38e-156">Create the ASP.NET Identity tables in a MySQL database</span></span>

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a><span data-ttu-id="0b38e-157">安装 MySQL 工作台工具以连接和管理 MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="0b38e-157">Install MySQL Workbench tool to connect and manage MySQL database</span></span>

1. <span data-ttu-id="0b38e-158">从[mysql 下载页面](http://dev.mysql.com/downloads/windows/installer/)安装**mysql 工作台**工具</span><span class="sxs-lookup"><span data-stu-id="0b38e-158">Install the **MySQL Workbench** tool from the [MySQL downloads page](http://dev.mysql.com/downloads/windows/installer/)</span></span>
2. <span data-ttu-id="0b38e-159">启动应用并单击 " **MySQLConnections +** " 按钮添加新连接。</span><span class="sxs-lookup"><span data-stu-id="0b38e-159">Launch the app and add click on the **MySQLConnections +** button to add a new connection.</span></span> <span data-ttu-id="0b38e-160">使用您在本教程前面部分创建的 Azure MySQL 数据库中复制的连接字符串数据。</span><span class="sxs-lookup"><span data-stu-id="0b38e-160">Use the connection string data you copied from the Azure MySQL database you created earlier in this tutorial.</span></span>
3. <span data-ttu-id="0b38e-161">建立连接后，请打开一个新的**查询**选项卡;将[MySQLIdentity](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql)中的命令粘贴到查询中，并执行它以创建数据库表。</span><span class="sxs-lookup"><span data-stu-id="0b38e-161">After establishing the connection, open a new **Query** tab; paste the commands from [MySQLIdentity.sql](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) into the query and execute it in order to create the database tables.</span></span>
4. <span data-ttu-id="0b38e-162">现在，在 Azure 上托管的 MySQL 数据库上创建了所有 ASP.NET Identity 必需的表，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0b38e-162">You now have all the ASP.NET Identity necessary tables created on a MySQL database hosted on Azure as shown below.</span></span>  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a><span data-ttu-id="0b38e-163">从模板创建 MVC 应用程序项目，并将其配置为使用 MySQL 提供程序</span><span class="sxs-lookup"><span data-stu-id="0b38e-163">Create an MVC application project from template and configure it to use MySQL provider</span></span>

<span data-ttu-id="0b38e-164">如果需要，请为 Web 或更新2的[Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566)安装[Visual Studio Express 2013](https://go.microsoft.com/fwlink/?LinkId=299058) 。</span><span class="sxs-lookup"><span data-stu-id="0b38e-164">If needed, install either [Visual Studio Express 2013 for Web](https://go.microsoft.com/fwlink/?LinkId=299058) or [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) with Update 2.</span></span>

### <a name="download-the-aspnetidentitymysql-project-from-github"></a><span data-ttu-id="0b38e-165">从 GitHub 下载 .asp .asp 项目</span><span class="sxs-lookup"><span data-stu-id="0b38e-165">Download the ASP.NET.Identity.MySQL project from GitHub</span></span>

1. <span data-ttu-id="0b38e-166">浏览到 node.js [（GitHub）](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/)上的存储库 URL。</span><span class="sxs-lookup"><span data-stu-id="0b38e-166">Browse to the repository URL at [AspNet.Identity.MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/).</span></span>
2. <span data-ttu-id="0b38e-167">下载源代码。</span><span class="sxs-lookup"><span data-stu-id="0b38e-167">Download the source code.</span></span>
3. <span data-ttu-id="0b38e-168">将 .zip 文件解压缩到本地文件夹。</span><span class="sxs-lookup"><span data-stu-id="0b38e-168">Extract the .zip file into a local folder.</span></span>
4. <span data-ttu-id="0b38e-169">打开 AspNet. node.js 解决方案并生成它。</span><span class="sxs-lookup"><span data-stu-id="0b38e-169">Open the AspNet.Identity.MySQL solution and build it.</span></span>

### <a name="create-a-new-mvc-application-project-from-template"></a><span data-ttu-id="0b38e-170">通过模板创建新的 MVC 应用程序项目</span><span class="sxs-lookup"><span data-stu-id="0b38e-170">Create a new MVC application project from template</span></span>

1. <span data-ttu-id="0b38e-171">右键**单击 ""** **，然后**单击 "**新建项目**"</span><span class="sxs-lookup"><span data-stu-id="0b38e-171">Right click the **AspNet.Identity.MySQL** solution and **Add**, **New Project**</span></span>
2. <span data-ttu-id="0b38e-172">在 "**添加新项目**" 对话框的左侧选择 "**视觉对象C#**  "，然后选择 " **web** "，然后选择 " **ASP.NET Web 应用程序**"。</span><span class="sxs-lookup"><span data-stu-id="0b38e-172">In the **Add New Project** Dialog select **Visual C#** on the left, then **Web** and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="0b38e-173">将项目命名为**IdentityMySQLDemo**;然后单击 "确定"。</span><span class="sxs-lookup"><span data-stu-id="0b38e-173">Name your project **IdentityMySQLDemo**; and then click OK.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. <span data-ttu-id="0b38e-174">在 "**新建 ASP.NET 项目**" 对话框中，选择包含默认选项的 MVC 模板（其中包含**单独的用户帐户**作为身份验证方法），然后单击 **"确定"** 。![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span><span class="sxs-lookup"><span data-stu-id="0b38e-174">In the **New ASP.NET Project** dialog, select the MVC template with the default options (that includes **Individual User Accounts** as authentication method) and click **OK**.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)</span></span>
4. <span data-ttu-id="0b38e-175">在解决方案资源管理器中，右键单击 IdentityMySQLDemo 项目，然后选择 "**管理 NuGet 包**"。</span><span class="sxs-lookup"><span data-stu-id="0b38e-175">In Solution Explorer, right-click your IdentityMySQLDemo project and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="0b38e-176">在 "搜索文本框" 对话框中，键入**EntityFramework**。</span><span class="sxs-lookup"><span data-stu-id="0b38e-176">In the search text box dialog, type **Identity.EntityFramework**.</span></span> <span data-ttu-id="0b38e-177">在结果列表中选择此包，并单击 "**卸载**"。</span><span class="sxs-lookup"><span data-stu-id="0b38e-177">Select this package in the list of results and click **Uninstall**.</span></span> <span data-ttu-id="0b38e-178">系统将提示你卸载依赖项包 EntityFramework。</span><span class="sxs-lookup"><span data-stu-id="0b38e-178">You will be prompted to uninstall the dependency package EntityFramework.</span></span> <span data-ttu-id="0b38e-179">单击 "是"，因为此应用程序上不再有此包。</span><span class="sxs-lookup"><span data-stu-id="0b38e-179">Click on Yes as we will no longer this package on this application.</span></span>
5. <span data-ttu-id="0b38e-180">右键单击 "IdentityMySQLDemo" 项目，选择 "**添加**"、"**引用"、"解决方案"、"项目**"，选择 "AspNet" 项目并单击 **"确定"** 。</span><span class="sxs-lookup"><span data-stu-id="0b38e-180">Right click the IdentityMySQLDemo project, select **Add**, **Reference, Solution, Projects;** select the AspNet.Identity.MySQL project and click **OK**.</span></span>
6. <span data-ttu-id="0b38e-181">在 IdentityMySQLDemo 项目中，将所有引用替换为</span><span class="sxs-lookup"><span data-stu-id="0b38e-181">In the IdentityMySQLDemo project, replace all references to</span></span>  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   <span data-ttu-id="0b38e-182">替换为</span><span class="sxs-lookup"><span data-stu-id="0b38e-182">with</span></span>  
     `using AspNet.Identity.MySQL;`
7. <span data-ttu-id="0b38e-183">在 IdentityModels.cs 中，将**ApplicationDbContext**设置为从**MySqlDatabase**派生，并包含一个构造函数，该构造函数采用单个参数和连接名称。</span><span class="sxs-lookup"><span data-stu-id="0b38e-183">In IdentityModels.cs, set **ApplicationDbContext** to derive from **MySqlDatabase** and include a constructor that take a single parameter with the connection name.</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. <span data-ttu-id="0b38e-184">打开 IdentityConfig.cs 文件。</span><span class="sxs-lookup"><span data-stu-id="0b38e-184">Open the IdentityConfig.cs file.</span></span> <span data-ttu-id="0b38e-185">在**ApplicationUserManager**方法中，将实例化 UserManager 替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="0b38e-185">In the **ApplicationUserManager.Create** method, replace instantiating UserManager with the following code:</span></span>  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. <span data-ttu-id="0b38e-186">打开 web.config 文件并将 DefaultConnection 字符串替换为此项，将突出显示的值替换为前面步骤中创建的 MySQL 数据库的连接字符串：</span><span class="sxs-lookup"><span data-stu-id="0b38e-186">Open the web.config file and replace the DefaultConnection string with this entry replacing the highlighted values with the connection string of the MySQL database you created on previous steps:</span></span>  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a><span data-ttu-id="0b38e-187">运行应用并连接到 MySQL 数据库</span><span class="sxs-lookup"><span data-stu-id="0b38e-187">Run the app and connect to the MySQL DB</span></span>

1. <span data-ttu-id="0b38e-188">右键单击 " **IdentityMySQLDemo** " 项目，然后选择 "**设为启动项目**"</span><span class="sxs-lookup"><span data-stu-id="0b38e-188">Right click the **IdentityMySQLDemo** project and select **Set as Startup Project**</span></span>
2. <span data-ttu-id="0b38e-189">按**Ctrl + F5**生成并运行应用。</span><span class="sxs-lookup"><span data-stu-id="0b38e-189">Press **Ctrl + F5** to build and run the app.</span></span>
3. <span data-ttu-id="0b38e-190">单击页面顶部的 "**注册**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="0b38e-190">Click on **Register** tab on the top of the page.</span></span>
4. <span data-ttu-id="0b38e-191">输入新用户名和密码，然后单击 "**注册**"。</span><span class="sxs-lookup"><span data-stu-id="0b38e-191">Enter a new user name and password and then click on **Register**.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. <span data-ttu-id="0b38e-192">新用户现在已注册并登录。</span><span class="sxs-lookup"><span data-stu-id="0b38e-192">The new user is now registered and logged in.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. <span data-ttu-id="0b38e-193">返回到 MySQL 工作台工具并检查**IdentityMySQLDatabase**表的内容。</span><span class="sxs-lookup"><span data-stu-id="0b38e-193">Go back to the MySQL Workbench tool and inspect the **IdentityMySQLDatabase** table's contents.</span></span> <span data-ttu-id="0b38e-194">注册新用户时，请检查用户表中的条目。</span><span class="sxs-lookup"><span data-stu-id="0b38e-194">Inspect the users table for the entries as you register new users.</span></span>  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a><span data-ttu-id="0b38e-195">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0b38e-195">Next Steps</span></span>

<span data-ttu-id="0b38e-196">有关如何在此应用上启用其他身份验证方法的详细信息，请参阅[使用 Facebook 和 Google OAuth2 创建 ASP.NET MVC 5 应用和 OpenID 登录](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)。</span><span class="sxs-lookup"><span data-stu-id="0b38e-196">For more information on how to enable other authentication methods on this app, refer to [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).</span></span>

<span data-ttu-id="0b38e-197">若要了解如何将 DB 与 OAuth 集成并设置角色，以限制用户对应用的访问权限，请参阅将[包含成员资格、OAuth 和 SQL 数据库的 Secure ASP.NET MVC 5 应用部署到 Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)。</span><span class="sxs-lookup"><span data-stu-id="0b38e-197">To learn how to integrate your DB with OAuth and to set up roles to limit users access to your app, see [Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).</span></span>
