---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
title: 用实体框架创建模型类（VB） |Microsoft Docs
author: microsoft
description: 在本教程中，了解如何将 ASP.NET MVC 与 Microsoft 实体框架结合使用。 了解如何使用实体向导创建 ADO.NET 实体 Da 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: ff8322c9-12f3-4e24-aba6-a38046b9bb0d
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-vb
msc.type: authoredcontent
ms.openlocfilehash: f6c896c6f5f6d898ac6f99d5998fb29cb73bcb10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437006"
---
# <a name="creating-model-classes-with-the-entity-framework-vb"></a>使用 Entity Framework 创建模型类 (VB)

由[Microsoft](https://github.com/microsoft)

> 在本教程中，了解如何将 ASP.NET MVC 与 Microsoft 实体框架结合使用。 了解如何使用实体向导创建 ADO.NET 实体数据模型。 在本教程中，我们将构建一个 web 应用程序，该应用程序演示如何使用实体框架来选择、插入、更新和删除数据库数据。

本教程的目的是说明如何在生成 ASP.NET MVC 应用程序时使用 Microsoft 实体框架来创建数据访问类。 本教程假定你以前没有 Microsoft 实体框架知识。 在本教程结束时，您将了解如何使用实体框架来选择、插入、更新和删除数据库记录。

Microsoft 实体框架是一种对象关系映射（O/RM）工具，它使您能够从数据库中自动生成数据访问层。 使用实体框架可以避免手动生成数据访问类的单调工作。

> [!NOTE] 
> 
> ASP.NET MVC 与 Microsoft 实体框架之间没有必要的连接。 可以将实体框架一些替代方法用于 ASP.NET MVC。 例如，你可以使用其他 O/RM 工具（如 Microsoft LINQ to SQL、NHibernate 或 SubSonic）来构建 MVC 模型类。

为了说明如何将 Microsoft 实体框架与 ASP.NET MVC 结合使用，我们将构建一个简单的示例应用程序。 我们将创建一个电影数据库应用程序，用于显示和编辑电影数据库记录。

本教程假定你具有 Visual Studio 2008 或带有 Service Pack 1 的 Visual Web Developer 2008。 需要 Service Pack 1 才能使用实体框架。 你可以从以下地址下载 Visual Studio 2008 Service Pack 1 或带 Service Pack 1 的 Visual Web Developer：

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

## <a name="creating-the-movie-sample-database"></a>创建电影示例数据库

电影数据库应用程序使用名为电影的数据库表，其中包含以下列：

| 列名 | 数据类型 | 是否允许空？ | 为主键？ |
| --- | --- | --- | --- |
| Id | int | False | True |
| 标题 | nvarchar(100) | False | False |
| 导演 | nvarchar(100) | False | False |

可以通过以下步骤将此表添加到 ASP.NET MVC 项目：

1. 右键单击 "解决方案资源管理器" 窗口中的 "应用\_Data" 文件夹，然后选择 "**添加"、"新建项**" 菜单。
2. 从 "**添加新项**" 对话框中，选择 " **SQL Server 数据库**"，为数据库指定名称 MoviesDB，然后单击 "**添加**" 按钮。
3. 双击 MoviesDB 文件以打开 "服务器资源管理器/数据库资源管理器" 窗口。
4. 展开 "MoviesDB" 数据库连接，右键单击 "表" 文件夹，然后选择 "**添加新表**" 菜单选项。
5. 在表设计器中，添加 "Id"、"标题" 和 "主管" 列。
6. 单击 "**保存**" 按钮（它具有软盘图标），以将新表保存为电影名称。

创建电影数据库表后，应将一些示例数据添加到表中。 右键单击电影表，然后选择菜单选项 "**显示表数据**"。 可以在显示的网格中输入虚假电影数据。

## <a name="creating-the-adonet-entity-data-model"></a>创建 ADO.NET 实体数据模型

若要使用实体框架，需要创建一个实体数据模型。 你可以利用 Visual Studio*实体数据模型向导*来自动从数据库生成实体数据模型。

请执行这些步骤：

1. 右键单击 "解决方案资源管理器" 窗口中的 "模型" 文件夹，然后选择 "**添加"、"新建项**" 菜单。
2. 在 "**添加新项**" 对话框中，选择数据类别（请参阅图1）。
3. 选择 " **ADO.NET 实体数据模型**" 模板，将 "名称" 指定实体数据模型为 "MoviesDBModel"，然后单击 "**添加**" 按钮。 单击 "**添加**" 按钮将启动数据模型向导。
4. 在 "**选择模型内容**" 步骤中，选择 "**从数据库生成**" 选项，然后单击 "**下一步**" 按钮（参见图2）。
5. 在 "**选择你的数据连接**" 步骤中，选择 "MoviesDB" 数据库连接，输入实体连接设置 "名称 MoviesDBEntities"，然后单击 "**下一步**" 按钮（见图3）。
6. 在 "**选择数据库对象**" 步骤中，选择 "电影数据库" 表，然后单击 "**完成**" 按钮（见图4）。

完成这些步骤后，将打开 "ADO.NET 实体数据模型设计器（Entity Designer）"。

**图 1-创建新实体数据模型**

![clip_image002](creating-model-classes-with-the-entity-framework-vb/_static/image1.jpg)

**图 2-选择模型内容步骤**

![clip_image004](creating-model-classes-with-the-entity-framework-vb/_static/image2.jpg)

**图 3-选择你的数据连接**

![clip_image006](creating-model-classes-with-the-entity-framework-vb/_static/image3.jpg)

**图 4-选择数据库对象**

![clip_image008](creating-model-classes-with-the-entity-framework-vb/_static/image4.jpg)

## <a name="modifying-the-adonet-entity-data-model"></a>修改 ADO.NET 实体数据模型

创建实体数据模型后，可以通过利用 Entity Designer 来修改模型（请参阅图5）。 您可以通过双击 "解决方案资源管理器" 窗口中的 "模型" 文件夹中包含的 "MoviesDBModel" 文件，随时打开 Entity Designer。

**图5– ADO.NET 实体数据模型设计器**

![clip_image010](creating-model-classes-with-the-entity-framework-vb/_static/image5.jpg)

例如，您可以使用 Entity Designer 更改实体模型数据向导生成的类的名称。 向导已创建名为 "电影" 的新数据访问类。 换言之，向导为类提供与数据库表的名称相同的名称。 由于我们将使用此类来表示特定的电影实例，因此应将类从电影重命名为电影。

如果要重命名实体类，可以双击 "Entity Designer 中的类名称，然后输入新名称（见图6）。 或者，在 Entity Designer 中选择实体后，可以更改属性窗口中的实体的名称。

**图 6-更改实体名称**

![clip_image012](creating-model-classes-with-the-entity-framework-vb/_static/image6.jpg)

请记住在进行修改后保存实体数据模型，方法是单击 "保存" 按钮（软盘的图标）。 在幕后，Entity Designer 将生成一组 Visual Basic 的 .NET 类。 可以通过从 "解决方案资源管理器" 窗口打开 MoviesDBModel 文件来查看这些类。

请勿修改设计器 .vb 文件中的代码，因为下次使用 Entity Designer 时，所做的更改将被覆盖。 如果要扩展在设计器 .vb 文件中定义的实体类的功能，则可以在单独的文件中创建*分部类*。

#### <a name="selecting-database-records-with-the-entity-framework"></a>选择包含实体框架的数据库记录

接下来，我们将创建一个显示电影记录列表的页面，开始构建电影数据库应用程序。 列表1中的 Home 控制器公开一个名为 Index （）的操作。 Index （）操作利用实体框架从电影数据库表中返回所有电影记录。

**列表1– Controllers\HomeController.vb**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample1.vb)]

请注意，列表1中的控制器包含构造函数。 构造函数初始化名为 \_db 的类级字段。 \_db 字段表示由 Microsoft 实体框架生成的数据库实体。 \_db 字段是 Entity Designer 生成的 MoviesDBEntities 类的实例。

\_db 字段用于索引（）操作，用于从电影数据库表中检索记录。 表达式 \_db。MovieSet 表示电影数据库表中的所有记录。 System.linq.enumerable.tolist （）方法用于将电影集转换为电影对象的通用集合： List （电影）。

可以通过 LINQ to Entities 的帮助检索电影记录。 列表1中的 Index （）操作使用 LINQ*方法语法*来检索数据库记录集。 如果您愿意，也可以改用 LINQ*查询语法*。 以下两个语句执行的操作完全相同：

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample2.vb)]

使用您最直观的任何 LINQ 语法–方法语法或查询语法。 这两种方法之间没有性能差异–唯一的区别在于样式。

清单2中的视图用于显示电影记录。

**列表 2-Views\Home\Index.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample3.aspx)]

"列表 2" 中的视图包含**每个**循环遍历每个电影记录并显示影片记录的 "标题" 和 "控制器" 属性值的。 请注意，"编辑" 和 "删除" 链接将显示在每个记录的旁边。 此外，"添加电影" 链接将显示在视图的底部（请参阅图7）。

**图7–索引视图**

![clip_image014](creating-model-classes-with-the-entity-framework-vb/_static/image7.jpg)

索引视图是*类型化的视图*。 索引视图的 &lt;% @ 页面%&gt; 指令包含 Inherits 属性。 Inherits 属性将 ViewData 属性强制转换为电影对象的强类型化的泛型列表集合–一个列表（电影）。

## <a name="inserting-database-records-with-the-entity-framework"></a>插入具有实体框架的数据库记录

您可以使用实体框架以便于将新记录插入数据库表中。 列表3包含向 Home 控制器类添加的两个新操作，可用于将新记录插入到电影数据库表中。

**列表3– Controllers\HomeController.vb （添加方法）**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample4.vb)]

第一个 Add （）操作只返回视图。 视图包含用于添加新的电影数据库记录的窗体（参见图8）。 提交窗体时，将调用第二个 Add （）操作。

请注意，第二个 Add （）操作是用 AcceptVerbs 特性修饰的。 此操作只能在执行 HTTP POST 操作时调用。 换句话说，此操作只能在发布 HTML 窗体时调用。

第二个 Add （）操作使用 ASP.NET MVC TryUpdateModel （）方法的帮助创建实体框架 Movie 类的新实例。 TryUpdateModel （）方法使用传递给 Add （）方法的 FormCollection 中的字段，并将这些 HTML 窗体字段的值分配给 Movie 类。

使用实体框架时，在使用 TryUpdateModel 或 UpdateModel 方法更新实体类的属性时，必须提供属性的 "白列表"。

接下来，Add （）操作执行一些简单的窗体验证。 操作将验证 Title 和 Director 属性是否都具有值。 如果存在验证错误，则会将验证错误消息添加到 ModelState。

如果没有验证错误，则会将一个新的电影记录添加到 "电影数据库" 表，并提供实体框架的帮助。 新记录将添加到数据库，其中包含以下两行代码：

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample5.vb)]

第一行代码将新的 Movie 实体添加到实体框架正在跟踪的电影集。 第二行代码保存对要追溯到基础数据库的电影所做的任何更改。

**图8– "添加" 视图**

![clip_image016](creating-model-classes-with-the-entity-framework-vb/_static/image8.jpg)

## <a name="updating-database-records-with-the-entity-framework"></a>用实体框架更新数据库记录

您可以遵循与使用实体框架相同的方法编辑数据库记录，就像我们在插入新的数据库记录的方法一样。 列表4包含两个名为 Edit （）的新控制器操作。 第一个 Edit （）操作返回用于编辑电影记录的 HTML 窗体。 第二个 Edit （）操作尝试更新数据库。

**列表4– Controllers\HomeController.vb （编辑方法）**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample6.vb)]

第二个 Edit （）操作通过从数据库检索与正在编辑的电影的 Id 相匹配的电影记录开始。 下面的 LINQ to Entities 语句获取与特定 Id 匹配的第一个数据库记录：

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample7.vb)]

接下来，使用 TryUpdateModel （）方法将 HTML 窗体字段的值分配给 movie 实体的属性。 请注意，提供允许列表来指定要更新的确切属性。

接下来，执行一些简单的验证来验证电影标题和控制器属性是否都具有值。 如果任一属性缺少值，则会将验证错误消息添加到 ModelState，ModelState 将返回值 false。

最后，如果没有验证错误，则通过调用 SaveChanges （）方法，使用任何更改更新基础电影数据库表。

编辑数据库记录时，需要将正在编辑的记录的 Id 传递给执行数据库更新的控制器操作。 否则，控制器操作将不知道要在基础数据库中更新哪个记录。 "列表 5" 中包含的 "编辑" 视图包含一个隐藏的窗体字段，该字段表示正在编辑的数据库记录的 Id。

**列表5– Views\Home\Edit.aspx**

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a>删除具有实体框架的数据库记录

在本教程中，需要处理的最终数据库操作是删除数据库记录。 您可以使用清单6中的控制器操作删除特定的数据库记录。

**列表 6--\Controllers\HomeController.vb （删除操作）**

[!code-vb[Main](creating-model-classes-with-the-entity-framework-vb/samples/sample9.vb)]

Delete （）操作首先检索与传递给操作的 Id 相匹配的 "电影" 实体。 接下来，通过调用 DeleteObject （）方法并随后使用 SaveChanges （）方法从数据库中删除此电影。 最后，将用户重定向回索引视图。

## <a name="summary"></a>摘要

本教程的目的是演示如何通过利用 ASP.NET MVC 和 Microsoft 实体框架来构建数据库驱动的 web 应用程序。 您学习了如何构建可用于选择、插入、更新和删除数据库记录的应用程序。

首先，我们讨论了如何使用实体数据模型向导在 Visual Studio 中生成实体数据模型。 接下来，您将了解如何使用 LINQ to Entities 从数据库表中检索一组数据库记录。 最后，我们使用了实体框架来插入、更新和删除数据库记录。

> [!div class="step-by-step"]
> [上一页](validation-with-the-data-annotation-validators-cs.md)
> [下一页](creating-model-classes-with-linq-to-sql-vb.md)
