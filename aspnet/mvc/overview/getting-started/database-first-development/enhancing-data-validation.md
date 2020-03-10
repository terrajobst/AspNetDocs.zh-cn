---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 教程：通过 ASP.NET MVC 应用增强 EF Database First 的数据验证
description: 本教程重点介绍如何将数据批注添加到数据模型，以指定验证要求和显示格式。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499532"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a>教程：通过 ASP.NET MVC 应用增强 EF Database First 的数据验证

使用 MVC、实体框架和 ASP.NET 基架，你可以创建一个 web 应用程序，用于向现有数据库提供接口。 本系列教程演示如何自动生成允许用户显示、编辑、创建和删除位于数据库表中的数据的代码。 生成的代码与数据库表中的列相对应。

本教程重点介绍如何将数据批注添加到数据模型，以指定验证要求和显示格式。 它已根据 "评论" 部分中用户的反馈进行了改进。

在本教程中，你将了解：

> [!div class="checklist"]
> * 添加数据批注
> * 添加元数据类

## <a name="prerequisites"></a>系统必备

* [自定义视图](customizing-a-view.md)

## <a name="add-data-annotations"></a>添加数据批注

正如您在前面的主题中看到的那样，某些数据验证规则将自动应用于用户输入。 例如，只能为评分属性提供一个数字。 若要指定更多的数据验证规则，可以将数据批注添加到模型类。 在整个 web 应用程序中，为指定的属性应用这些注释。 还可以应用更改属性显示方式的格式设置属性;例如，更改用于文本标签的值。

在本教程中，您将添加数据批注，以限制为 FirstName、LastName 和 MiddleName 属性提供的值的长度。 在数据库中，这些值限制为50个字符;但是，在 web 应用程序中，当前不强制使用字符限制。 如果用户为其中一个值提供了超过50个字符，则在尝试将该值保存到数据库时，此页将会崩溃。 还会将评分限制为介于0到4之间的值。

选择 > **ContosoModel** ** > 的** **模型**，并打开*Student.cs*文件。 将以下突出显示的代码添加到类。

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

打开*Enrollment.cs* ，并添加以下突出显示的代码。

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

生成解决方案。

单击 "**学生列表**"，然后选择 "**编辑**"。 如果尝试输入超过50个字符，将显示一条错误消息。

![显示错误消息](enhancing-data-validation/_static/image1.png)

返回到主页。 单击 "**注册列表**"，然后选择 "**编辑**"。 尝试提供高于4的等级。 您将收到此错误：*字段级别必须介于0到4之间。*

## <a name="add-metadata-classes"></a>添加元数据类

如果你不希望数据库发生更改，则直接将验证特性添加到模型类会有效：但是，如果您的数据库发生了更改，并且您需要重新生成模型类，则您将丢失已应用于 model 类的所有属性。 此方法可能非常低效，并容易丢失重要验证规则。

若要避免此问题，可以添加一个包含特性的元数据类。 将模型类关联到 metadata 类时，这些属性将应用于该模型。 在此方法中，可以重新生成模型类，而不会丢失已应用于元数据类的所有属性。

在 "**模型**" 文件夹中，添加名为*Metadata.cs*的类。

将*Metadata.cs*中的代码替换为以下代码。

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

这些元数据类包含之前应用于模型类的所有验证特性。 **显示**属性用于更改用于文本标签的值。

现在，必须将模型类与元数据类相关联。

在 "**模型**" 文件夹中，添加名为*PartialClasses.cs*的类。

将文件的内容替换为以下代码。

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

请注意，每个类都标记为 `partial` 类，每个类都将名称和命名空间与自动生成的类相匹配。 通过将 metadata 特性应用到分部类，可以确保将数据验证特性应用到自动生成的类。 重新生成模型类时这些属性将不会丢失，因为 metadata 特性应用于不会重新生成的分部类中。

若要重新生成自动生成的类，请打开*ContosoModel*文件。 再次右键单击设计图面，然后选择 "**从数据库更新模型**"。 即使尚未更改数据库，此过程也会重新生成类。 在 "**刷新**" 选项卡中，选择 "**表**" 和 "**完成**"。

保存*ContosoModel*文件以应用所做的更改。

打开*Student.cs*文件或*Enrollment.cs*文件，并注意你之前应用的数据验证属性已不再位于文件中。 但是，运行应用程序，请注意，当输入数据时，仍然会应用验证规则。

## <a name="conclusion"></a>结束语

此系列提供了一个简单的示例，说明如何从允许用户编辑、更新、创建和删除数据的现有数据库生成代码。 它使用 ASP.NET MVC 5，实体框架和 ASP.NET 基架来创建项目。 

有关 Code First 开发的介绍性示例，请参阅[与 ASP.NET MVC 5 入门](../introduction/getting-started.md)。 

有关更高级的示例，请参阅为[ASP.NET MVC 4 应用创建实体框架数据模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 请注意，用于在 Database First 中处理数据的 DbContext API 与在 Code First 中处理数据时使用的 API 相同。 即使你打算使用 Database First，也可以了解如何处理更复杂的方案，例如读取和更新相关数据、处理并发冲突等，以及从 Code First 教程中进行操作。 唯一的差别在于如何创建数据库、上下文类和实体类。

## <a name="additional-resources"></a>其他资源

有关可应用于属性和类的数据验证批注的完整列表，请参阅[system.componentmodel. DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)。

## <a name="next-steps"></a>后续步骤

在本教程中，你将了解：

> [!div class="checklist"]
> * 添加的数据批注
> * 添加的元数据类

若要了解如何将 web 应用和 SQL 数据库部署到 Azure App Service，请参阅本教程：
> [!div class="nextstepaction"]
> [将 .NET 应用部署到 Azure App Service](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
