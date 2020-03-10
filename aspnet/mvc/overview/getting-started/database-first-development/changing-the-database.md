---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 教程：通过 ASP.NET MVC 应用更改 EF Database First 数据库
description: 本教程重点介绍如何更新数据库结构并在整个 web 应用程序中传播该更改。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499520"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a>教程：通过 ASP.NET MVC 应用更改 EF Database First 数据库

使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。 本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。 生成的代码与数据库表中的列相对应。

本教程重点介绍如何更新数据库结构并在整个 web 应用程序中传播该更改。

在本教程中，你将了解：

> [!div class="checklist"]
> * 添加列
> * 将属性添加到视图

## <a name="prerequisites"></a>系统必备

* [正在生成视图](generating-views.md)

## <a name="add-a-column"></a>添加列

如果更新数据库中表的结构，则需要确保将更改传播到数据模型、视图和控制器。

对于本教程，您将向 "学生" 表添加一个新列，以记录学生的中间名。 若要添加此列，请打开数据库项目，然后打开 Student .sql 文件。 通过设计器或 T-sql 代码，添加一个名为**MiddleName**的列，该列的数据类型为 NVARCHAR （50），并允许空值。

通过启动您的数据库项目（或按 F5），将此更改部署到您的本地数据库。 新字段将添加到表中。 如果在 SQL Server 对象资源管理器中看不到它，请单击窗格中的 "刷新" 按钮。

![显示新列](changing-the-database/_static/image2.png)

新列存在于数据库表中，但它当前不存在于数据模型类中。 您必须更新模型以包含您的新列。 在 "**模型**" 文件夹中，打开**ContosoModel**文件以显示模型关系图。 请注意，"学生" 模型不包含 MiddleName 属性。 右键单击设计图面上的任意位置，然后选择 "**从数据库更新模型**"。

在更新向导中，选择 "**刷新**" 选项卡，然后选择 "**表** > **dbo** > **Student**"。 单击“完成”。

更新过程完成后，数据库关系图将包含新的**MiddleName**属性。 保存**ContosoModel**文件。 若要将新属性传播到**Student.cs**类，必须保存此文件。 现已更新数据库和模型。

生成解决方案。

## <a name="add-the-property-to-the-views"></a>将属性添加到视图

遗憾的是，视图仍不包含新属性。 若要更新视图，可以使用两个选项来重新生成视图，方法是再次添加 Student 类的基架，也可以手动将新属性添加到现有视图。 在本教程中，您将再次添加基架，因为您没有对自动生成的视图进行任何自定义更改。 如果对视图进行了更改，并且不希望放弃这些更改，则可以考虑手动添加属性。

若要确保重新创建视图，请在 "**视图**" 下删除 "**学生**" 文件夹，并删除**StudentsController**。 然后，右键单击 "**控制器**" 文件夹并添加 "**学生**" 模型的基架。 同样，将控制器命名为**StudentsController**。 选择“添加”。

再次生成解决方案。 视图现在包含 MiddleName 属性。

![显示中间名](changing-the-database/_static/image5.png)

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 添加了列
> * 向视图添加了属性

转到下一教程，了解如何自定义视图以显示有关学生记录的详细信息。
> [!div class="nextstepaction"]
> [自定义视图](customizing-a-view.md)