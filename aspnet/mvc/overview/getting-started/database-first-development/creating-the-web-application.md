---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 教程：创建 Web 应用程序和数据模型用于 EF Database First 与 ASP.NET MVC
description: 本教程重点介绍如何创建 web 应用程序，以及如何基于数据库表生成数据模型。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499526"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a>教程：创建 Web 应用程序和数据模型用于 EF Database First 与 ASP.NET MVC

 使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。 本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。 生成的代码与数据库表中的列相对应。

本教程重点介绍如何创建 web 应用程序，以及如何基于数据库表生成数据模型。

在本教程中，你将了解：

> [!div class="checklist"]
> * 创建 ASP.NET Web 应用
> * 生成模型

## <a name="prerequisites"></a>系统必备

* [使用 MVC 5 Database First 实体框架6入门](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a>创建 ASP.NET Web 应用

在新解决方案或与数据库项目相同的解决方案中，在 Visual Studio 中创建一个新项目，然后选择 " **ASP.NET Web 应用程序**" 模板。 将项目命名为**ContosoSite**。

![创建项目](creating-the-web-application/_static/image1.png)

单击“确定”。

在 "新建 ASP.NET 项目" 窗口中，选择 " **MVC** " 模板。 你现在可以**在云中选项中清除主机**，因为你稍后会将该应用程序部署到云。 单击 **"确定"** 以创建该应用程序。

项目是用默认文件和文件夹创建的。

在本教程中，您将使用实体框架6。 可以通过 "管理 NuGet 包" 窗口，仔细检查项目中实体框架的版本。 如有必要，请更新实体框架的版本。

![显示版本](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a>生成模型

现在，您将从数据库表创建实体框架模型。 这些模型是将用于处理数据的类。 每个模型镜像数据库中的一个表，并包含与表中的列相对应的属性。

右键单击 "**模型**" 文件夹，然后选择 "**添加**" 和 "**新建项**"。

在 "添加新项" 窗口中，选择左窗格中的 "**数据**"，并从中间窗格的选项中**ADO.NET 实体数据模型**。 将新的模型文件命名为**ContosoModel**。

单击 **“添加”** 。

在实体数据模型向导中，选择 "**从数据库中选择 EF 设计器**"。

单击 **“下一步”** 。

如果在开发环境中定义了数据库连接，则可能会看到预先选择了这些连接之一。 但是，您希望创建一个与您在本教程第一部分中创建的数据库的新连接。 单击 "**新建连接**" 按钮。

在 "连接属性窗口中，提供创建数据库的本地服务器的名称（在本例中为" **（localdb） \ProjectsV13**） "。 提供服务器名称后，从可用数据库中选择 "ContosoUniversityData"。

![设置连接属性](creating-the-web-application/_static/image8.png)

单击“确定”。

现在会显示正确的连接属性。 可以在 web.config 文件中使用连接的默认名称。

单击 **“下一步”** 。

选择最新版本的实体框架。

单击 **“下一步”** 。

选择要为所有三个表生成模型的**表**。

单击“完成”。

如果收到安全警告，请选择 **"确定"** 以继续运行模板。

将从数据库表中生成模型，并显示一个关系图，其中显示表之间的属性和关系。

![模型示意图](creating-the-web-application/_static/image11.png)

"模型" 文件夹现在包含许多与从数据库生成的模型相关的新文件。

**ContosoModel.Context.cs**文件包含从**DbContext**类派生的类，并为对应于数据库表的每个模型类提供一个属性。 **Course.cs**、 **Enrollment.cs**和**Student.cs**文件包含表示数据库表的模型类。 使用基架时，将使用上下文类和模型类。

在继续学习本教程之前，请生成项目。 在下一节中，您将生成基于数据模型的代码，但如果尚未生成项目，该部分将无法工作。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 创建 ASP.NET web 应用
> * 生成模型

转到下一教程，了解如何创建基于数据模型的代码。
> [!div class="nextstepaction"]
> [正在生成视图](generating-views.md)
