---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 使用 Visual Studio 的 ASP.NET Web 部署：部署数据库更新 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636834"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a>使用 Visual Studio 的 ASP.NET Web 部署：部署数据库更新

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。

## <a name="overview"></a>概述

在本教程中，你将进行数据库更改和相关的代码更改，在 Visual Studio 中测试更改，然后将更新部署到测试、过渡和生产环境。

本教程首先演示如何更新 Code First 迁移管理的数据库，然后，它将演示如何使用 dbDacFx 提供程序更新数据库。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](troubleshooting.md)。

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a>使用 Code First 迁移部署数据库更新

在本部分中，会将一个出生日期列添加到 `Student` 的 `Person` 基类和 `Instructor` 实体。 然后更新显示讲师数据的页面，使其显示新列。 最后，将所做的更改部署到测试、过渡和生产环境。

### <a name="add-a-column-to-a-table-in-the-application-database"></a>向应用程序数据库中的表添加列

1. 在*ContosoUniversity*项目中，打开*Person.cs* ，并将以下属性添加到 `Person` 类的末尾（后面应该有两个右大括号）：

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    接下来，更新 `Seed` 方法，使其为新列提供一个值。 打开*Migrations\Configuration.cs*并将开始 `var instructors = new List<Instructor>` 的代码块替换为以下代码块，其中包含出生日期信息：

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. 生成解决方案，然后打开 "**包管理器控制台**" 窗口。 确保 "ContosoUniversity" 仍被选作**默认项目**。
3. 在 "**程序包管理器控制台**" 窗口中，选择 " **ContosoUniversity** " 作为**默认项目**，然后输入以下命令：

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    此命令完成后，Visual Studio 将打开定义新 `DbMigration` 类的类文件，并在 `Up` 方法中，你可以看到创建新列的代码。 `Up` 方法将在您实现更改时创建列，并且 `Down` 方法在您回滚更改时删除列。

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. 生成解决方案，然后在 "**包管理器控制台**" 窗口中输入以下命令（请确保 ContosoUniversity 项目仍处于选中状态）：

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    实体框架运行 `Up` 方法，然后运行 `Seed` 方法。

### <a name="display-the-new-column-in-the-instructors-page"></a>在 "讲师" 页中显示新列

1. 在 ContosoUniversity 项目中，打开 "*指导员*" 并添加新的 "模板" 字段以显示出生日期。 在雇用日期和办公室分配之间添加：

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    （如果代码缩进不同步，可以按下 CTRL-K，然后按 CTRL + D 自动重新格式化文件。）
2. 运行应用程序，并单击 "**讲师**" 链接。

    加载页面时，你会看到它具有新的 "出生日期" 字段。

    ![包含出生日期的指导员页面](deploying-a-database-update/_static/image2.png)
3. 关闭浏览器。

### <a name="deploy-the-database-update"></a>部署数据库更新

1. 在**解决方案资源管理器**选择 ContosoUniversity 项目。
2. 在**Web 一键式发布**工具栏中，单击 "**测试**发布配置文件"，然后单击 "**发布 Web**"。 （如果禁用工具栏，请在**解决方案资源管理器**中选择 ContosoUniversity 项目。）

    Visual Studio 将部署更新后的应用程序，浏览器将打开主页。
3. 运行 "**讲师**" 页，验证更新是否已成功部署。

    当应用程序尝试访问此页的数据库时，Code First 更新数据库架构并运行 `Seed` 方法。 显示页面后，会看到 "预期的**出生日期**" 列中包含日期。
4. 在**Web 一键式发布**工具栏中，单击 "**过渡**发布配置文件"，然后单击 "**发布 Web**"。
5. 在过渡环境中运行**讲师**页，验证更新是否已成功部署。
6. 在**Web 一键式发布**工具栏中，单击 "**生产**" 发布配置文件，然后单击 "**发布 Web**"。
7. 在生产环境中运行**讲师**页，验证更新是否已成功部署。

    对于包含数据库更改的实际生产应用程序更新，通常还会在部署过程中使应用程序脱机，如前一教程中所述，使用*应用\_"脱机*"。

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a>使用 dbDacFx 提供程序部署数据库更新

在本部分中，将向成员资格数据库中的*用户*表添加*备注*列，并创建一个页面，用于显示和编辑每个用户的注释。 然后，将所做的更改部署到测试、过渡和生产环境。

### <a name="add-a-column-to-a-table-in-the-membership-database"></a>向成员资格数据库中的表添加列

1. 在 Visual Studio 中，打开**SQL Server 对象资源管理器**。
2. 展开 **（localdb） \v11.0**，展开 "**数据库**"，展开 " **ContosoUniversity** " （非**aspnet-ContosoUniversity**），然后展开 "**表**"。

    如果在**SQL Server** "节点下看不到" **（localdb） \v11.0** "，请右键单击" **SQL Server** "节点，然后单击"**添加 SQL Server**"。 在 "**连接到服务器**" 对话框中，输入 *（localdb） \v11.0*作为**服务器名称**，然后单击 "**连接**"。

    如果看不到**ContosoUniversity**，请运行项目并使用*管理员*凭据登录（password 为*devpwd*），然后刷新**SQL Server 对象资源管理器**窗口。
3. 右键单击 "**用户**" 表，然后单击 "**视图设计器**"。

    ![SSOX 视图设计器](deploying-a-database-update/_static/image3.png)
4. 在设计器中，添加 "*注释*" 列并将其设置为*nvarchar （128）* ，然后单击 "**更新**"。

    ![添加注释列](deploying-a-database-update/_static/image4.png)
5. 在 "**预览数据库更新**" 框中，单击 "**更新数据库**"。

    ![预览数据库更新](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a>创建页面以显示和编辑新列

1. 在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目中的**帐户**文件夹，单击 "**添加**"，然后单击 "**新建项**"。
2. 使用母版页创建新的**Web 窗体**，并将其命名为 "*用户"。* 接受默认的*Site master*文件作为母版页。
3. 将以下标记复制到 `MainContent` `Content` 元素（3个 `Content` 元素的最后一个元素）：

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. 右键单击 "*用户*" 页，然后单击 "**在浏览器中查看**"。
5. 使用*管理员*用户凭据（密码为*devpwd*）登录，并向用户添加一些注释以验证该页是否正常工作。

    ![用户页](deploying-a-database-update/_static/image6.png)
6. 关闭浏览器。

## <a name="deploy-the-database-update"></a>部署数据库更新

若要使用 dbDacFx 提供程序进行部署，只需在发布配置文件中选择 "**更新数据库**" 选项。 但是，在使用此选项时，对于初始部署，还配置了一些其他要运行的 SQL 脚本：这些脚本仍在配置文件中，必须阻止它们再次运行。

1. 右键单击 "ContosoUniversity" 项目并单击 "**发布**"，打开 "**发布 Web** " 向导。
2. 选择**测试**配置文件。
3. 单击 "**设置**" 选项卡。
4. 在**DefaultConnection**下，选择 "**更新数据库**"。
5. 禁用您配置为初始部署运行的其他脚本：

    1. 单击 "**配置数据库更新**"。
    2. 在 "**配置数据库更新**" 对话框中，清除 " *Grant* " 和 " *aspnet-data-dev*" 旁边的复选框。
    3. 单击 **“关闭”** 。
6. 单击 "**预览**" 选项卡。
7. 在**DefaultConnection**下的 "**数据库**" 下，单击 "**预览数据库**" 链接。

    ![数据库预览](deploying-a-database-update/_static/image7.png)

    预览窗口显示将在目标数据库中运行的脚本，以使该数据库架构与源数据库的架构匹配。 该脚本包含一个用于添加新列的 ALTER TABLE 命令。
8. 关闭 "**数据库预览**" 对话框，然后单击 "**发布**"。

    Visual Studio 将部署更新后的应用程序，浏览器将打开主页。
9. 运行 "用户信息" 页（向主页 URL 添加*帐户/用户*类型），验证更新是否已成功部署。 必须输入*admin*和*devpwd*登录。

    默认情况下，表中的数据不会进行部署，并且你没有配置要运行的数据部署脚本，因此你不会发现在开发中添加的注释。 你现在可以在 "过渡" 中添加新的注释，以验证是否已将更改部署到数据库，并且页面是否正常工作。
10. 按照相同的过程部署到过渡和生产环境。

    别忘了禁用多余的脚本。 与测试配置文件相比，唯一的区别在于，你只会在暂存和生产配置文件中禁用一个脚本，因为它们配置为仅运行*aspnet-prod-data*。

    用于过渡和生产的凭据为 admin 和 prodpwd。

    对于包含数据库更改的实际生产应用程序更新，通常还需要在部署过程中将应用程序脱机，方法是在发布和删除应用程序后将其上载 *\_* ，如[前一教程](deploying-a-code-update.md)中所述。

## <a name="summary"></a>总结

现在，你已部署了一个应用程序更新，其中包含使用 Code First 迁移和 dbDacFx 提供程序的数据库更改。

![包含出生日期的指导员页面](deploying-a-database-update/_static/image8.png)

![用户页](deploying-a-database-update/_static/image9.png)

下一教程将演示如何使用命令行执行部署。

> [!div class="step-by-step"]
> [上一页](deploying-a-code-update.md)
> [下一页](command-line-deployment.md)
