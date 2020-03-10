---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 教程：使用 MVC 5 开始使用 EF Database First
description: 本教程演示如何从现有数据库开始，并快速创建允许用户与数据进行交互的 web 应用程序。
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471458"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a>教程：使用 MVC 5 开始使用 EF Database First

使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。 本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。 生成的代码与数据库表中的列相对应。 在本系列文章的最后一部分，你将了解如何将数据批注添加到数据模型，以指定验证要求和显示格式。 完成后，可以转到 Azure 文章，了解如何将 .NET 应用和 SQL 数据库部署到 Azure App Service。

本教程演示如何从现有数据库开始，并快速创建允许用户与数据进行交互的 web 应用程序。 它使用实体框架6和 MVC 5 来构建 web 应用程序。 利用 ASP.NET 基架功能，你可以自动生成用于显示、更新、创建和删除数据的代码。 使用 Visual Studio 中的发布工具，可以轻松地将站点和数据库部署到 Azure。

这部分系列重点介绍如何创建数据库并使用数据对其进行填充。

本系列文章由 Tom Dykstra 和 Rick Anderson 提供。 它已根据 "评论" 部分中用户的反馈进行了改进。

在本教程中，你将了解：

> [!div class="checklist"]
> * 设置数据库

## <a name="prerequisites"></a>系统必备

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a>设置数据库

若要模拟具有现有数据库的环境，首先要创建一个具有一些预填充数据的数据库，然后创建连接到该数据库的 web 应用程序。

本教程是使用 LocalDB 和 Visual Studio 2017 开发的。 你可以使用现有的数据库服务器而不是 LocalDB，但根据你的 Visual Studio 版本和你的数据库类型，Visual Studio 中的所有数据工具可能都不受支持。 如果这些工具不适用于您的数据库，则可能需要在您的数据库的管理套件内执行特定于数据库的一些步骤。

如果你的 Visual Studio 版本中的数据库工具有问题，请确保已安装最新版本的数据库工具。 有关更新或安装数据库工具的信息，请参阅[Microsoft SQL Server Data tools](https://msdn.microsoft.com/data/hh297027)。

启动 Visual Studio 并创建一个**SQL Server 数据库项目**。 将项目命名为**ContosoUniversityData**。

![创建数据库项目](setting-up-database/_static/image1.png)

你现在已有一个空的数据库项目。 若要确保可以将此数据库部署到 Azure，请将 Azure SQL 数据库设置为项目的目标平台。 设置目标平台实际上不会部署数据库;这只意味着数据库项目将验证数据库设计是否与目标平台兼容。 若要设置目标平台，请打开该项目的 "**属性**"，然后选择目标平台**Microsoft Azure SQL 数据库**。

您可以通过添加定义表的 SQL 脚本来创建本教程所需的表。 右键单击您的项目并添加一个新项。 选择表**和视图** > **表**，并为*其命名*。

在表文件中，将 T-sql 命令替换为以下代码，以创建表。

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

请注意，设计窗口会自动与代码同步。 您可以使用代码或设计器。

![显示代码和设计](setting-up-database/_static/image5.png)

添加另一个表。 此时间为 it 课程命名，并使用以下 T-sql 命令。

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

再重复一次，创建名为 "注册" 的表。

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

您可以通过在部署数据库后运行的脚本，使用数据填充数据库。 向项目中添加后期部署脚本。 右键单击您的项目并添加一个新项。 选择 "**用户脚本**" > **部署后脚本**。 可以使用默认名称。

将以下 T-sql 代码添加到后期部署脚本。 此脚本仅在未找到匹配记录时将数据添加到数据库。 它不会覆盖或删除可能已输入数据库的任何数据。

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

请务必注意，每次部署数据库项目时都将运行后期部署脚本。 因此，在编写此脚本时，您需要仔细考虑您的要求。 在某些情况下，你可能希望在每次部署项目时从一组已知的数据开始。 在其他情况下，您可能不想以任何方式更改现有数据。 根据你的要求，你可以决定是需要部署后脚本还是需要在脚本中包括的内容。 有关使用后期部署脚本填充数据库的详细信息，请参阅[在 SQL Server 数据库项目中包含数据](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)。

现在有4个 SQL 脚本文件，但没有实际表。 你已准备好将数据库项目部署到 localdb。 在 Visual Studio 中，单击 "开始" 按钮（或按 F5）以生成并部署数据库项目。 检查 "**输出**" 选项卡，验证生成和部署是否成功。

若要查看是否已创建新数据库，请打开**SQL Server 对象资源管理器**，然后在正确的本地数据库服务器（在本例中为**localdb） \ProjectsV13**中查找该项目的名称。

若要查看表中是否填充了数据，请右键单击表，然后选择 "**查看数据**"。

![显示表数据](setting-up-database/_static/image9.png)

将显示表数据的可编辑视图。 例如，如果选择 "**表** > " > **查看数据**"，则会看到一个表，其中包含三列 **（课程**、**标题**和**信用**）和四**行。**

## <a name="additional-resources"></a>其他资源

有关 Code First 开发的介绍性示例，请参阅[与 ASP.NET MVC 5 入门](../introduction/getting-started.md)。 有关更高级的示例，请参阅为[ASP.NET MVC 4 应用创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。

有关选择使用哪种实体框架方法的指导，请参阅[实体框架开发方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 设置数据库

转到下一教程，了解如何创建 web 应用程序和数据模型。
> [!div class="nextstepaction"]
> [创建 web 应用程序和数据模型](creating-the-web-application.md)
