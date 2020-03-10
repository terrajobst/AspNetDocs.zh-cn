---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 教程：通过 ASP.NET MVC 应用生成 EF Database First 视图
description: 本教程重点介绍如何使用 ASP.NET 基架生成控制器和视图。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499472"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a>教程：通过 ASP.NET MVC 应用生成 EF Database First 视图

使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。 本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。 生成的代码与数据库表中的列相对应。

本教程重点介绍如何使用 ASP.NET 基架生成控制器和视图。

在本教程中，你将了解：

> [!div class="checklist"]
> * 添加基架
> * 将链接添加到新视图
> * 显示学生视图
> * 显示注册视图

## <a name="prerequisite"></a>必备组件

* [创建 web 应用程序和数据模型](creating-the-web-application.md)

## <a name="add-scaffold"></a>添加基架

你已准备好生成代码，该代码将为模型类提供标准数据操作。 添加基架项即可添加代码。 可以添加的基架类型有很多选项;在本教程中，基架将包含与上一节中创建的学生和注册模型相对应的控制器和视图。

若要在项目中保持一致性，请将新的控制器添加到 "现有**控制器**" 文件夹。 右键单击 "**控制器**" 文件夹，然后选择 "**添加** > **新的基架项**"。

**使用 "实体框架" 选项，选择 "包含视图的 MVC 5 控制器"** 。 此选项将生成控制器和视图，用于更新、删除、创建和显示模型中的数据。

![添加 mvc 控制器](generating-views/_static/image2.png)

选择 "ContosoSite" 作为模型类的 "**学生（）** "，然后选择 "上下文" 类的**ContosoUniversityDataEntities （ContosoSite）** 。 将控制器名称保留为**StudentsController**。

单击 **“添加”** 。

如果收到错误，则可能是因为你在上一节中未生成项目。 如果是这样，请尝试生成该项目，然后再次添加基架项。

代码生成过程完成后，你将在项目的**控制器**中看到一个新的控制器和**视图，并 > ** **学生**文件夹中查看。

再次执行相同的步骤，但为**注册**类添加基架。 完成后，你将拥有一个**EnrollmentsController.cs**文件，并使用创建、删除、详细信息、编辑和索引视图在名为 "**注册**" 的**视图**下创建一个文件夹。

## <a name="add-links-to-new-views"></a>将链接添加到新视图

为了更轻松地导航到新视图，您可以向学生和注册的索引视图添加几个超链接。 在 > **home** > 的**视图**中打开文件，该文件是你的网站的*主页。* 在 jumbotron 下面添加以下代码。

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

对于 Html.actionlink 方法，第一个参数是要在链接中显示的文本。 第二个参数是操作，第三个参数是控制器的名称。 例如，第一个链接指向 StudentsController 中的 Index 操作。 实际的超链接是根据这些值构造的。 第一个链接最终将用户转到 "**视图/学生**" 文件夹内的**索引 cshtml**文件。

## <a name="display-student-views"></a>显示学生视图

你将验证添加到你的项目的代码是否正确显示了学生列表，并使用户能够在数据库中编辑、创建或删除学生记录。

右键单击 > **Home** > *索引的***视图**文件，然后选择 "**在浏览器中查看**"。 在应用程序主页上，选择 "**学生列表**"。

![](generating-views/_static/image6.png)

在 "**索引**" 页上，请注意学生列表和修改此数据的链接。 选择 "**新建**" 链接，并为新学生提供一些值。 单击 "**创建**"，并注意将新的学生添加到列表。

返回到 "**索引**" 页，选择 "**编辑**" 链接，然后更改学生的某些值。 单击 "**保存**"，并注意学生记录已更改。

最后，选择 "**删除**" 链接，并通过单击 "**删除**" 按钮确认是否要删除该记录。

在不编写任何代码的情况下，你添加了对 "学生" 表中的数据执行常见操作的视图。

您可能已注意到，字段的文本标签基于数据库属性（如**LastName**），这并不一定是您想要在网页上显示的内容。 例如，您可能希望标签为 "**姓氏**"。 你将在本教程的后面部分修复此显示问题。

## <a name="display-enrollment-views"></a>显示注册视图

您的数据库包含学生和注册表之间的一对多关系，以及课程表和注册表之间的一对多关系。 注册的视图会正确地处理这些关系。 导航到网站的主页并选择 "注册" 链接**列表**，然后选择 "**创建新**链接"。

此视图显示用于创建新注册记录的窗体。 特别要注意的是，该窗体包含**CourseID**下拉列表和**StudentID**下拉列表。 两者都用相关表中的值填充。

此外，系统会根据字段的数据类型自动应用对提供值的验证。 **评分**要求数字，因此如果您尝试提供不兼容的值，将显示一条错误消息：*字段级别必须为数字。*

您已经验证了自动生成的视图使用户能够处理数据库中的数据。 在本系列的下一个教程中，您将更新数据库，并在 web 应用程序中进行相应的更改。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 添加的基架
> * 添加了到新视图的链接
> * 显示的学生视图
> * 显示的注册视图

转到下一教程，了解如何更改数据库。
> [!div class="nextstepaction"]
> [更改数据库](changing-the-database.md)