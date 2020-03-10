---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署数据库更新-9 （共12个） |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78455102"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署数据库更新-9 （共12个）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

在本教程中，你将进行数据库更改和相关代码更改，在 Visual Studio 中测试更改，然后将更新部署到测试和生产环境中。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="adding-a-new-column-to-a-table"></a>向表中添加新列

在本部分中，会将一个出生日期列添加到 `Student` 的 `Person` 基类和 `Instructor` 实体。 然后更新显示讲师数据的页面，使其显示新列。

在*ContosoUniversity*项目中，打开*Person.cs* ，并将以下属性添加到 `Person` 类的末尾（后面应该有两个右大括号）：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

接下来，更新种子方法，使其为新列提供一个值。 打开*Migrations\Configuration.cs*并将开始 `var instructors = new List<Instructor>` 的代码块替换为以下代码块，其中包含出生日期信息：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

在 ContosoUniversity 项目中，打开 "*指导员*" 并添加新的 "模板" 字段以显示出生日期。 在雇用日期和办公室分配之间添加：

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

（如果代码缩进不同步，可以按下 CTRL-K，然后按 CTRL + D 自动重新格式化文件。）

生成解决方案，然后打开 "**包管理器控制台**" 窗口。 确保 "ContosoUniversity" 仍被选作**默认项目**。

在 "**程序包管理器控制台**" 窗口中，选择 " **ContosoUniversity** " 作为**默认项目**，然后输入以下命令：

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

此命令完成后，Visual Studio 将打开定义新 `DbMigration` 类的类文件，并在 `Up` 方法中，你可以看到创建新列的代码。

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

生成解决方案，然后在 "**包管理器控制台**" 窗口中输入以下命令（请确保 ContosoUniversity 项目仍处于选中状态）：

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

命令完成后，运行应用程序并选择 "讲师" 页。 加载页面时，你会看到它具有新的 "出生日期" 字段。

[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>将数据库更新部署到测试环境

在**解决方案资源管理器**选择 ContosoUniversity 项目。

在**Web 一键式发布**工具栏中，选择 "**测试**发布" 配置文件，然后单击 "**发布 Web**"。 （如果禁用工具栏，请在**解决方案资源管理器**中选择 ContosoUniversity 项目。）

Visual Studio 将部署更新后的应用程序，浏览器将打开主页。 运行 "讲师" 页，验证更新是否已成功部署。 当应用程序尝试访问此页的数据库时，Code First 更新数据库架构并运行 `Seed` 方法。 显示页面后，会看到 "预期的**出生日期**" 列中包含日期。

[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>将数据库更新部署到生产环境

你现在可以部署到生产环境。 唯一的区别在于，您将使用*应用程序\_"脱机*" 来防止用户访问该站点，从而在部署更改时更新数据库。 对于生产部署，请执行以下步骤：

- 将*应用\_脱机*文件上传到生产站点。
- 在 Visual Studio 中，在 Web 中选择 "生产" 配置文件，**单击 "发布**" 工具栏，然后单击 "**发布 Web**"。
- 从生产站点中删除*应用\_脱机 .htm*文件。

> [!NOTE]
> 当应用程序在生产环境中使用时，应实现备份计划。 也就是说，应定期将*School-Prod*和*aspnet-Prod*文件从生产站点复制到安全的存储位置，并且应保留多代此类备份。 更新数据库时，应立即从更改之前创建备份副本。 然后，如果您在将其部署到生产环境之前，不会发现该错误，则您仍然能够将数据库恢复到其损坏之前的状态。

当 Visual Studio 在浏览器中打开主页 URL 时，将显示 "*应用\_offline* " 页。 *\_脱机*文件删除应用后，你可以再次浏览到你的主页，以验证更新是否已成功部署。

[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)

现在，你已部署了一个应用程序更新，其中包括对测试和生产的数据库更改。 下一教程介绍如何将数据库从 SQL Server Compact 迁移到 SQL Server Express 和 SQL Server。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [下一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
