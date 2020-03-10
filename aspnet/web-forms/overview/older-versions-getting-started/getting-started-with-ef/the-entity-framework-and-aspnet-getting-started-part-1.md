---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
title: 入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体 |Microsoft Docs
author: tdykstra
description: Contoso 大学示例 web 应用程序演示如何使用实体框架4.0 和 Visual Studio 2010 。
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 5cb00916-8f46-491f-be25-4739a615d619
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
msc.type: authoredcontent
ms.openlocfilehash: fd88b32ad2a65e5b4c7ead15f0d6dc5dc6e97e75
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511676"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms"></a>入门实体框架 4.0 Database First 和 ASP.NET 4 Web 窗体

作者： [Tom Dykstra](https://github.com/tdykstra)

> Contoso 大学示例 web 应用程序演示了如何使用实体框架4.0 和 Visual Studio 2010 创建 ASP.NET Web 窗体应用程序。 该示例应用程序是一个虚构的 Contoso 大学的网站。 它包括诸如学生入学、 课程创建和导师分配等功能。
> 
> 本教程演示中C#的示例。 [可下载的示例](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a)包含C#和 Visual Basic 中的代码。
> 
> ## <a name="database-first"></a>Database First
> 
> 可以通过三种方式使用实体框架中的数据： *Database First*、 *Model First*和*Code First*。 本教程适用于 Database First。 有关这些工作流之间的差异以及如何为你的方案选择最佳方案的指南的信息，请参阅[实体框架开发工作流](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。
> 
> ## <a name="web-forms"></a>Web Forms — Web 窗体
> 
> 本教程系列使用 ASP.NET Web 窗体模型，并假设你知道如何在 Visual Studio 中使用 ASP.NET Web 窗体。 否则，请参阅[ASP.NET 4.5 Web Forms 入门](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)。 如果希望使用 ASP.NET MVC 框架，请参阅[使用 ASP.NET mvc 入门与实体框架](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。
> 
> ## <a name="software-versions"></a>软件版本
> 
> | **教程中所示** | **还适用于** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express for Web。 本教程尚未通过更高版本的 Visual Studio 进行测试。 菜单选择、对话框和模板有很多不同之处。 |
> | .NET 4 | .NET 4.5 向后兼容 .NET 4，但本教程尚未通过 .NET 4.5 进行测试。 |
> | 实体框架4 | 本教程尚未测试实体框架的更高版本。 从实体框架5开始，EF 默认使用 EF 4.1 引入的 `DbContext API`。 EntityDataSource 控件设计为使用 `ObjectContext` API。 有关如何将 EntityDataSource 控件与 `DbContext` API 一起使用的信息，请参阅[此博客文章](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)。 |
> 
> ## <a name="questions"></a>问题
> 
> 如果你有与本教程不直接相关的问题，则可以将其发布到[ASP.NET 实体框架论坛](https://forums.asp.net/1227.aspx)、[实体框架和 LINQ to Entities 论坛](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。

## <a name="overview"></a>概述

你将在这些教程中构建的应用程序是一个简单的大学网站。

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image1.png)

用户可以查看和更新学生、 课程和教师信息。 下面显示了你将创建的几个屏幕。

[![Image30](the-entity-framework-and-aspnet-getting-started-part-1/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image3.png)

[![Image37](the-entity-framework-and-aspnet-getting-started-part-1/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image5.png)

[![Image31](the-entity-framework-and-aspnet-getting-started-part-1/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image7.png)

[![Image32](the-entity-framework-and-aspnet-getting-started-part-1/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image9.png)

## <a name="creating-the-web-application"></a>创建 Web 应用程序

若要开始学习本教程，请打开 Visual Studio，然后使用**ASP.NET Web 应用程序**模板创建新的 ASP.NET Web 应用程序项目：

[![Image01](the-entity-framework-and-aspnet-getting-started-part-1/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image11.png)

此模板创建已包含样式表和母版页的 web 应用程序项目：

[![Image02](the-entity-framework-and-aspnet-getting-started-part-1/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image13.png)

打开*网站 .master*文件，将 "My ASP.NET Application" 更改为 "Contoso 大学"。

[!code-html[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample1.html)]

找到名为 `NavigationMenu` 的*菜单*控件，并将其替换为以下标记，该标记将为要创建的页添加菜单项。

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample2.aspx)]

打开*default.aspx*页，将名为 `BodyContent` 的 `Content` 控件更改为：

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample3.aspx)]

现在，你有了一个简单的主页，其中包含指向要创建的各个页面的链接：

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image15.png)

## <a name="creating-the-database"></a>创建数据库

对于这些教程，您将使用实体框架数据模型设计器自动基于现有数据库创建数据模型（通常称为*数据库优先*的方法）。 本系列教程未涵盖的替代方法是手动创建数据模型，然后让设计器生成用于创建数据库的脚本（*模型优先*的方法）。

对于本教程中使用的数据库优先方法，下一步是将数据库添加到站点。 最简单的方法是先下载本教程中的项目。 然后右键单击 "*应用\_Data* " 文件夹，选择 "**添加现有项**"，然后从下载的项目中选择*School .mdf*数据库文件。

一种替代方法是按照[创建 School 示例数据库](https://msdn.microsoft.com/library/bb399731.aspx)中的说明进行操作。 无论是下载数据库还是创建数据库，请将以下文件夹中的*School .mdf*文件复制到应用程序的应用程序 *\_Data*文件夹：

`%PROGRAMFILES%\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA`

（此 *.mdf*文件的位置假设你使用 SQL Server 2008 Express。）

如果从脚本创建数据库，请执行以下步骤来创建数据库关系图：

1. 在**服务器资源管理器**中，展开 "**数据连接**"，展开 " *School*"，右键单击 "**数据库关系图**"，然后选择 "**添加新关系图**"。

    [![Image35](the-entity-framework-and-aspnet-getting-started-part-1/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image17.png)
2. 选择所有表，然后单击 "**添加**"。

    [![Image36](the-entity-framework-and-aspnet-getting-started-part-1/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image19.png)

    SQL Server 创建一个数据库关系图，该关系图显示表、表中的列以及表之间的关系。 您可以根据自己的需要移动表以对它们进行组织。
3. 将关系图保存为 "SchoolDiagram" 并将其关闭。

如果下载本教程附带的*School .mdf*文件，则可以通过在**服务器资源管理器**中的 "**数据库关系图**" 下双击**SchoolDiagram**来查看数据库关系图。

[![Image38](the-entity-framework-and-aspnet-getting-started-part-1/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image21.png)

关系图看起来类似于下面这样的内容（表可能位于不同位置，如下所示）：

[![Image04](the-entity-framework-and-aspnet-getting-started-part-1/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image23.png)

## <a name="creating-the-entity-framework-data-model"></a>创建实体框架数据模型

现在，您可以从该数据库创建实体框架的数据模型。 您可以在应用程序的根文件夹中创建数据模型，但对于本教程，您需要将其放在名为*DAL*的文件夹（对于数据访问层）中。

在**解决方案资源管理器**中，添加一个名为*DAL*的项目文件夹（确保它位于项目下，而不是在解决方案下）。

右键单击*DAL*文件夹，然后选择 "**添加**" 和 "**新建项**"。 在 "**已安装的模板**" 下，选择 "**数据**"，选择 " **ADO.NET 实体数据模型**" 模板，将其命名为*SchoolModel*，然后单击 "**添加**"。

[![Image05](the-entity-framework-and-aspnet-getting-started-part-1/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image25.png)

这将启动实体数据模型向导。 在第一个向导步骤中，默认情况下将选择 "**从数据库生成**" 选项。 单击 **“下一步”** 。

[![Image06](the-entity-framework-and-aspnet-getting-started-part-1/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image27.png)

在 "**选择你的数据连接**" 步骤中，保留默认值，然后单击 "**下一步**"。 默认情况下，School 数据库处于选中状态，并且连接设置在 web.config*文件中*保存为**SchoolEntities**。

[![Image07](the-entity-framework-and-aspnet-getting-started-part-1/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image29.png)

在 "**选择数据库对象**" 向导步骤中，选择除 "`sysdiagrams`" 之外的所有表（为之前生成的关系图创建），然后单击 "**完成**"。

[![Image08](the-entity-framework-and-aspnet-getting-started-part-1/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image31.png)

模型创建完成后，Visual Studio 将显示与数据库表相对应的实体框架对象（实体）的图形化表示形式。 （与数据库关系图一样，各个元素的位置可能不同于在此图中看到的内容。 如果需要，可以拖动围绕的元素来匹配图。）

[![Image09](the-entity-framework-and-aspnet-getting-started-part-1/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image33.png)

## <a name="exploring-the-entity-framework-data-model"></a>浏览实体框架数据模型

您可以看到，实体关系图与数据库关系图非常相似，但有几个不同之处。 一个不同之处是在每个关联的末尾添加符号，以指示关联的类型（数据模型中的表关系称为实体关联）：

- 一对零或一的关联由 "1" 和 "0 .0" 表示。

    [![Image39](the-entity-framework-and-aspnet-getting-started-part-1/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image35.png)

    在这种情况下，`Person` 实体不一定与 `OfficeAssignment` 实体相关联。 `OfficeAssignment` 实体必须与 `Person` 实体相关联。 换句话说，指导员可以或不能分配到办公室，任何办公室都只能分配给一个教师。
- 一对多关联由 "1" 和 "\*" 表示。

    [![Image40](the-entity-framework-and-aspnet-getting-started-part-1/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image37.png)

    在这种情况下，`Person` 实体不一定有关联的 `StudentGrade` 实体。 `StudentGrade` 实体必须与一个 `Person` 实体相关联。 `StudentGrade` 实体实际表示此数据库中的已注册课程;如果学生已在课程中注册，但没有评分，则 `Grade` 属性为 null。 换句话说，一名学生可能尚未注册到任何课程中，可以在一个课程中注册，也可以在多个课程中注册。 注册课程中的每个成绩仅适用于一个学生。
- 多对多关联由 "\*" 和 "\*" 表示。

    [![Image41](the-entity-framework-and-aspnet-getting-started-part-1/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image39.png)

    在这种情况下，`Person` 实体可能具有也可能不具有关联的 `Course` 实体，反之亦然： `Course` 实体可能具有或没有关联的 `Person` 实体。 换句话说，讲师可以讲授多个课程，一个课程可能由多个讲师讲授。 （在此数据库中，此关系仅适用于讲师; 它不会将学生链接到课程。 学生通过 StudentGrades 表链接到课程。）

数据库关系图和数据模型之间的另一个差异是每个实体的其他**导航属性**部分。 实体的导航属性引用相关实体。 例如，`Person` 实体中的 `Courses` 属性包含与该 `Person` 实体相关的所有 `Course` 实体的集合。

[![Image12](the-entity-framework-and-aspnet-getting-started-part-1/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image41.png)

但数据库和数据模型之间的另一个差异在于，数据库中使用的 `CourseInstructor` 关联表与多对多关系中的 `Person` 和 `Course` 表之间没有关联。 使用导航属性，您可以从 "`Person`" 实体和 "`Course`" 实体中的相关 `Person` 实体获取相关 `Course` 实体，因此不需要在数据模型中表示关联表。

[![Image11](the-entity-framework-and-aspnet-getting-started-part-1/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image43.png)

出于本教程的目的，假设 `Person` 表的 `FirstName` 列实际包含人员的名字和中间名。 您要更改字段的名称以反映这一点，但数据库管理员（DBA）可能不想更改数据库。 您可以在数据模型中更改 `FirstName` 属性的名称，同时使其数据库的等效项保持不变。

在设计器中，右键单击 "`Person`" 实体中的 "**名字**"，然后选择 "**重命名**"。

[![Image13](the-entity-framework-and-aspnet-getting-started-part-1/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image45.png)

键入新名称 "FirstMidName"。 这会改变您在代码中引用列的方式，而无需更改数据库。

[![Image29](the-entity-framework-and-aspnet-getting-started-part-1/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image47.png)

模型浏览器提供另一种方法来查看数据库结构、数据模型结构以及它们之间的映射。 若要查看它，请在实体设计器中右键单击空白区域，然后单击 "**模型浏览器**"。

[![Image18](the-entity-framework-and-aspnet-getting-started-part-1/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image49.png)

"**模型浏览器**" 窗格显示树视图。 （"**模型浏览器**" 窗格可能与 "**解决方案资源管理器**" 窗格停靠在一起。）**SchoolModel**节点表示数据模型结构， **SchoolModel**节点表示数据库结构。

[![Image26](the-entity-framework-and-aspnet-getting-started-part-1/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image51.png)

展开**SchoolModel**以查看表，展开 "**表/视图**" 以查看表，然后展开 "**课程**" 以查看表中的列。

[![Image19](the-entity-framework-and-aspnet-getting-started-part-1/_static/image54.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image53.png)

展开 " **SchoolModel**"，展开 "**实体类型**"，然后展开 "**课程**" 节点以查看实体和实体中的属性。

[![Image20](the-entity-framework-and-aspnet-getting-started-part-1/_static/image56.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image55.png)

在 "设计器" 或 "**模型浏览器**" 窗格中，可以看到实体框架如何将这两个模型的对象相关联。 右键单击 "`Person`" 实体，然后选择 "**表映射**"。

[![Image21](the-entity-framework-and-aspnet-getting-started-part-1/_static/image58.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image57.png)

这将打开 "**映射详细信息**" 窗口。 请注意，此窗口使你可以看到 `FirstName` 的数据库列映射到数据模型中将其重命名为的 `FirstMidName`。

[![Image22](the-entity-framework-and-aspnet-getting-started-part-1/_static/image60.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image59.png)

实体框架使用 XML 存储有关数据库、数据模型和它们之间的映射的信息。 *SchoolModel*文件实际上是包含此信息的 XML 文件。 设计器以图形格式呈现信息，但您也可以通过在**解决方案资源管理器**中右键单击 *.edmx*文件，然后单击 "**打开方式**"，然后选择 " **xml （文本）编辑器**"，以 XML 格式查看文件。 （数据模型设计器和 XML 编辑器只是打开和使用同一文件的两种不同方式，因此您不能同时打开设计器并在 XML 编辑器中打开该文件。）

你现在已经创建了一个网站、一个数据库和一个数据模型。 在下一个演练中，你将开始使用数据模型和 ASP.NET `EntityDataSource` 控件处理数据。

> [!div class="step-by-step"]
> [下一部分](the-entity-framework-and-aspnet-getting-started-part-2.md)
