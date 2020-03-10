---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 教程：通过 ASP.NET MVC 应用自定义 EF Database First 的视图
description: 本教程重点介绍如何更改自动生成的视图以增强演示。
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471518"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a>教程：通过 ASP.NET MVC 应用自定义 EF Database First 的视图

使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。 本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。 生成的代码与数据库表中的列相对应。

本教程重点介绍如何更改自动生成的视图以增强演示。

在本教程中，你将了解：

> [!div class="checklist"]
> * 向 "学生详细信息" 页添加课程
> * 确认已将课程添加到页面

## <a name="prerequisites"></a>系统必备

* [更改数据库](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a>向学生详细信息添加课程

生成的代码为应用程序提供了一个很好的起点，但它并不一定提供您的应用程序所需的所有功能。 你可以自定义代码来满足应用程序的特定要求。 目前，应用程序不会显示所选学生的已注册课程。 在本部分中，你将向学生的**详细信息**视图中添加每个学生的已注册课程。

 > *详细信息，*  > **学生**打开**视图**。 在最后一个 &lt;/dl&gt; 标记下，但在结束 &lt;/div&gt; 标记之前，添加以下代码。

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

此代码将创建一个表，该表为所选学生的注册表中的每个记录显示一行。 **显示**方法为表示表达式的对象（modelItem）呈现 HTML。 您可以使用显示方法（而不是只是将属性值嵌入到代码中）以确保值基于其类型和该类型的模板正确地进行格式设置。 在此示例中，每个表达式都将返回循环中的当前记录的单个属性，并且值是呈现为文本的基元类型。

## <a name="confirm-courses-are-added"></a>确认添加课程

运行该解决方案。 单击 "**学生列表**"，然后选择其中一个学生的 "**详细信息**"。 你将看到已注册的课程已包含在视图中。

![学生注册](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a>后续步骤
在本教程中，你将了解：

> [!div class="checklist"]
> * 向学生详细信息页添加了课程
> * 已确认将课程添加到页面

转到下一教程，了解如何添加数据批注来指定验证要求和显示格式。
> [!div class="nextstepaction"]
> [增强数据验证](enhancing-data-validation.md)
