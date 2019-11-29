---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署 SQL Server 数据库更新-11 of 12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621091"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：部署 SQL Server 数据库更新-11 （共12个）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关显示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Microsoft Azure 网站，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

本教程介绍如何将数据库更新部署到完整的 SQL Server 数据库。 由于 Code First 迁移执行更新数据库的所有工作，因此该过程与[部署数据库更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教程中的 SQL Server Compact 过程几乎完全相同。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="adding-a-new-column-to-a-table"></a>向表中添加新列

在本教程的此部分中，你将进行数据库更改和相应的代码更改，然后在 Visual Studio 中对其进行测试，以便准备将其部署到测试环境和生产环境中。 此更改涉及到将 `OfficeHours` 列添加到 `Instructor` 实体，并在**讲师**网页中显示新信息。

在 ContosoUniversity 项目中，打开*Instructor.cs*并在 `HireDate` 和 `Courses` 属性之间添加以下属性：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

更新初始值设定项类，以便它将新列与测试数据进行种子设定。 打开*Migrations\Configuration.cs*并将开始 `var instructors = new List<Instructor>` 的代码块替换为以下代码块，其中包含新列：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

在 ContosoUniversity 项目中 *，打开 ""，然后*在第一个 `GridView` 控件中的 "结束 `</Columns>` 标记之前，添加一个新的" 模板 "字段：

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

生成解决方案。

打开 "**程序包管理器控制台**" 窗口，并选择 "ContosoUniversity" 作为**默认项目**。

输入以下命令：

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

运行应用程序并选择 "**讲师**" 页。 加载页面所需的时间比平时长，这是因为实体框架会重新创建数据库，并使用测试数据对其进行种子设定。

[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>将数据库更新部署到测试环境

使用 Code First 迁移时，将数据库更改部署到 SQL Server 的方法与 SQL Server Compact 相同。 但是，您必须更改测试发布配置文件，因为它仍设置为从 SQL Server Compact 迁移到 SQL Server。

第一步是删除在上一教程中创建的连接字符串转换。 不再需要这些信息，因为你将在发布配置文件中指定连接字符串转换，就像你在配置 "**包/发布 SQL** " 选项卡以便迁移到 SQL Server 之前所做的那样。

打开*web.config*文件并删除 `connectionStrings` 元素。 *Web.config*文件中唯一剩余的转换用于 `appSettings` 元素中的 `Environment` 值。

现在，你可以更新发布配置文件并发布到测试环境。

打开 "**发布 Web** " 向导，然后切换到 "**配置文件**" 选项卡。

选择 "**测试**发布配置文件"。

选择“设置”选项卡。

单击 **"启用新的数据库发布改进"** 。

在**SchoolContext**的 "连接字符串" 框中，输入在上一教程中用于*web.config*转换文件的相同值：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

选择 **"执行 Code First 迁移（在应用程序启动时运行）** 。 （在你的 Visual Studio 版本中，此复选框可能标记为**Apply Code First 迁移**。）

在**DefaultConnection**的 "连接字符串" 框中，输入在上一教程中用于*web.config*转换文件的相同值：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

清除 "**更新数据库**"。

单击“发布”。

Visual Studio 将代码更改部署到测试环境，并将浏览器打开到 Contoso 大学主页。

选择 "讲师" 页。

当应用程序运行此页时，它会尝试访问数据库。 Code First 迁移检查数据库是否是最新的，并且发现尚未应用最新的迁移。 Code First 迁移将应用最新的迁移，运行 `Seed` 方法，然后此页面就会正常运行。 将看到 "新的办公时间" 列，其中包含种子数据。

[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>将数据库更新部署到生产环境

还必须更改生产环境的发布配置文件。 在这种情况下，你将删除现有的配置文件，并通过导入已更新的 .publishsettings 文件来创建一个新的配置文件。 更新后的文件将包括位于 Cytanium 的 SQL Server 数据库的连接字符串。

正如你在将部署到测试环境时所看到的那样，在*web.config*转换文件中不再需要连接字符串转换。 打开该文件并删除 `connectionStrings` 元素。 其余转换适用于 `appSettings` 元素中的 `Environment` 值和限制访问 Elmah 错误报告的 `location` 元素。

在为生产创建新的发布配置文件之前，请使用与在[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)中的步骤相同的方法下载已更新的 .publishsettings 文件。 （在 Cytanium 控制面板中，单击 "**网站**"，然后单击 " **contosouniversity.com** " 网站。 选择 " **Web 发布**" 选项卡，然后单击 "**下载此网站的发布配置文件**"。）执行此操作的原因是在 .publishsettings 文件中选取数据库连接字符串。 首次下载该文件时，无法使用该连接字符串，因为你仍在使用 SQL Server Compact 并且尚未在 Cytanium 上创建 SQL Server 数据库。

现在，你可以更新发布配置文件并发布到生产环境。

打开 "**发布 Web** " 向导，然后切换到 "**配置文件**" 选项卡。

单击 "**管理配置文件**"，然后删除生产配置文件。

关闭 "**发布 Web** " 向导以保存此更改。

再次打开 "**发布 Web** " 向导，然后单击 "**导入**"。

如果使用的是临时 URL，请在 "**连接**" 选项卡上将 "**目标 URL** " 更改为适当的值。

单击 **“下一步”** 。

在 "**设置**" 选项卡上，单击 **"启用新的数据库发布改进"** 。

在**SchoolContext**的 "连接字符串" 下拉列表中，选择 "Cytanium 连接字符串"。

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

选择 **"执行 Code First 迁移（在应用程序启动时运行）"** 。

在**DefaultConnection**的 "连接字符串" 下拉列表中，选择 "Cytanium 连接字符串"。

选择 "**配置文件**" 选项卡，单击 "**管理配置文件**"，然后将配置文件从 "contosouniversity.com-Web 部署" 重命名为 "生产"。

关闭 "发布配置文件" 以保存更改，然后重新打开它。

单击“发布”。 （对于实际的生产网站，你会将*应用\_脱机*复制到生产，并将其放在项目文件夹中，然后再发布，然后在部署完成后将其删除。）

Visual Studio 将代码更改部署到测试环境，并将浏览器打开到 Contoso 大学主页。

选择 "讲师" 页。

Code First 迁移更新数据库的方式与在测试环境中的更新方式相同。 将看到 "新的办公时间" 列，其中包含种子数据。

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

现在，使用 SQL Server 数据库，已成功部署了包含数据库更改的应用程序更新。

## <a name="more-information"></a>详细信息

这将完成这一系列教程，介绍如何将 ASP.NET web 应用程序部署到第三方托管提供程序。 有关这些教程中所涉及的任何主题的详细信息，请参阅 MSDN 网站上的[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx)。

## <a name="acknowledgements"></a>致谢

我想感谢以下人员对本系列教程的内容进行了重大贡献：

- [Alberto Poblacion，MVP &amp; MCT，西班牙](https://mvp.support.microsoft.com/profile/Alberto)
- Jarod Ferguson，数据平台开发 MVP，美国
- 恶劣 Mittal，Microsoft
- [Kristina Olson，Microsoft](https://blogs.iis.net/krolson/default.aspx)
- [Mike Pope，Microsoft](http://www.mikepope.com/blog/DisplayBlog.aspx)
- Mohit Srivastava，Microsoft
- [Raffaele Rialdi，意大利](http://www.iamraf.net/)
- [Microsoft Rick Anderson](https://blogs.msdn.com/b/rickandy/)
- [Sayed Hashimi，Microsoft](http://sedodream.com/default.aspx)（twitter： [@sayedihashimi](http://twitter.com/sayedihashimi)）
- [Scott Hanselman](http://www.hanselman.com/blog/) （twitter： [@shanselman](http://twitter.com/shanselman)）
- [Scott Hunter，Microsoft](https://blogs.msdn.com/b/scothu/) （twitter： [@coolcsh](http://twitter.com/coolcsh)）
- [Srđan Božović，塞尔维亚](http://msforge.net/blogs/zmajcek/)
- [Vishal Joshi，Microsoft](http://vishaljoshi.blogspot.com/) （twitter： [@vishalrjoshi](http://twitter.com/vishalrjoshi)）

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [下一页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)
