---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
title: 显示数据库数据表（C#） |Microsoft Docs
author: microsoft
description: 在本教程中，我将演示显示一组数据库记录的两种方法。 我显示了两种在 HTML ta 中设置一组数据库记录格式的方法 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: d6e758b6-6571-484d-a132-34ee6c47747a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 3c908d030076fc8400190ef3cf1672632ac1ed6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436844"
---
# <a name="displaying-a-table-of-database-data-c"></a>显示数据库数据表 (C#)

由[Microsoft](https://github.com/microsoft)

[下载 PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_CS.pdf)

> 在本教程中，我将演示显示一组数据库记录的两种方法。 我显示了两种用于对 HTML 表中的一组数据库记录进行格式设置的方法。 首先，我将介绍如何在视图中直接设置数据库记录的格式。 接下来，我将演示如何在设置数据库记录的格式时利用分区。

本教程的目的是介绍如何在 ASP.NET MVC 应用程序中显示数据库数据的 HTML 表。 首先，您将了解如何使用 Visual Studio 中包含的基架工具来生成自动显示一组记录的视图。 接下来，您将了解如何在设置数据库记录格式时使用部分作为模板。

## <a name="create-the-model-classes"></a>创建模型类

我们将显示电影数据库表中的记录集。 电影数据库表包含以下列：

<a id="0.3_table01"></a>

| **列名称** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| Id | Int | False |
| 标题 | Nvarchar （200） | False |
| 导演 | NVarchar(50) | False |
| DateReleased | DateTime | False |

为了表示我们的 ASP.NET MVC 应用程序中的电影表，我们需要创建一个模型类。 在本教程中，我们将使用 Microsoft 实体框架来创建模型类。

> [!NOTE] 
> 
> 在本教程中，我们将使用 Microsoft 实体框架。 但是，请务必了解，你可以使用各种不同的技术与 ASP.NET MVC 应用程序中的数据库进行交互，包括 LINQ to SQL、NHibernate 或 ADO.NET。

请按照以下步骤启动实体数据模型向导：

1. 右键单击 "解决方案资源管理器" 窗口中的 "模型" 文件夹，然后选择 "**添加"、"新建项**" 菜单。
2. 选择 "**数据**" 类别，然后选择 " **ADO.NET 实体数据模型**" 模板。
3. 为数据模型指定名称*MoviesDBModel* ，并单击 "**添加**" 按钮。

单击 "添加" 按钮后，将显示 "实体数据模型" 向导（参见图1）。 按照以下步骤完成向导：

1. 在 "**选择模型内容**" 步骤中，选择 "**从数据库生成**" 选项。
2. 在 "**选择你的数据连接**" 步骤中，使用*MoviesDB*数据连接，并为连接设置使用名称 " *MoviesDBEntities* "。 单击“下一步”按钮。
3. 在 "**选择数据库对象**" 步骤中，展开 "表" 节点，然后选择 "电影" 表。 输入命名空间*模型*，然后单击 "**完成**" 按钮。

[![创建 LINQ to SQL 类](displaying-a-table-of-database-data-cs/_static/image1.jpg)](displaying-a-table-of-database-data-cs/_static/image1.png)

**图 01**：创建 LINQ to SQL 类（[单击以查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image2.png)）

完成实体数据模型向导后，"实体数据模型设计器会打开。 设计器应显示电影实体（参见图2）。

[![实体数据模型设计器](displaying-a-table-of-database-data-cs/_static/image2.jpg)](displaying-a-table-of-database-data-cs/_static/image3.png)

**图 02**：实体数据模型设计器（[单击查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image4.png)）

在继续操作之前，我们需要进行一项更改。 实体数据向导将生成一个名为*电影*的模型类，该类表示电影数据库表。 由于我们将使用 movie 类来表示特定电影，因此我们需要将类的名称修改为*电影*，而不是*影片*（单数形式）。

双击设计器图面上类的名称，并将类的名称从 "电影" 更改为 "电影"。 做出此更改后，单击 "**保存**" 按钮（软盘的图标）以生成 Movie 类。

## <a name="create-the-movies-controller"></a>创建影片控制器

现在我们有了表示数据库记录的方法，我们可以创建一个返回电影集合的控制器。 在 Visual Studio 解决方案资源管理器 "窗口中，右键单击" 控制器 "文件夹，然后选择"**添加 "** 和" 控制器 "菜单选项（见图3）。

[!["添加控制器" 菜单](displaying-a-table-of-database-data-cs/_static/image3.jpg)](displaying-a-table-of-database-data-cs/_static/image5.png)

**图 03**： "添加控制器" 菜单（[单击以查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image6.png)）

"**添加控制器**" 对话框出现时，请输入控制器名称 MovieController （参见图4）。 单击 "**添加**" 按钮添加新控制器。

[!["添加控制器" 对话框](displaying-a-table-of-database-data-cs/_static/image4.jpg)](displaying-a-table-of-database-data-cs/_static/image7.png)

**图 04**： "添加控制器" 对话框（[单击以查看完全大小的映像](displaying-a-table-of-database-data-cs/_static/image8.png)）

我们需要修改电影控制器公开的 Index （）操作，使其返回一组数据库记录。 修改控制器，使其看起来像列表1中的控制器。

**列表1– Controllers\MovieController.cs**

[!code-csharp[Main](displaying-a-table-of-database-data-cs/samples/sample1.cs)]

在列表1中，MoviesDBEntities 类用于表示 MoviesDB 数据库。 若要使用此类，需导入 MvcApplication1 命名空间，如下所示：

using MvcApplication1.Models;

表达式*实体。MovieSet. System.linq.enumerable.tolist （）* 从电影数据库表中返回所有电影集。

## <a name="create-the-view"></a>创建视图

若要在 HTML 表中显示一组数据库记录，最简单的方法是利用 Visual Studio 提供的基架。

通过选择 "**生成、生成解决方案**" 菜单选项来生成应用程序。 您必须先生成应用程序，然后才能打开 "**添加视图**" 对话框，否则您的数据类将不会出现在对话框中。

右键单击 Index （）操作并选择 "**添加视图**" 菜单选项（见图5）。

[添加视图 ![](displaying-a-table-of-database-data-cs/_static/image5.jpg)](displaying-a-table-of-database-data-cs/_static/image9.png)

**图 05**：添加视图（[单击查看完全尺寸的图像](displaying-a-table-of-database-data-cs/_static/image10.png)）

在 "**添加视图**" 对话框中，选中标记为 "**创建强类型视图**" 的复选框。 选择 Movie 类作为**视图数据类**。 选择 "*列表*" 作为 "**查看内容**" （见图6）。 选择这些选项将生成显示电影列表的强类型视图。

[!["添加视图" 对话框](displaying-a-table-of-database-data-cs/_static/image6.jpg)](displaying-a-table-of-database-data-cs/_static/image11.png)

**图 06**： "添加视图" 对话框（[单击以查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image12.png)）

单击 "**添加**" 按钮后，会自动生成列表2中的视图。 此视图包含遍历电影集合并显示电影的每个属性所需的代码。

**列表 2-Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample2.aspx)]

您可以通过选择菜单选项 "**调试"、"启动调试"** （或按 F5 键）来运行该应用程序。 运行应用程序会启动 Internet Explorer。 如果导航到/Movie URL，则会看到图7中的页面。

[![电影表](displaying-a-table-of-database-data-cs/_static/image7.jpg)](displaying-a-table-of-database-data-cs/_static/image13.png)

**图 07**：电影表（[单击以查看完全大小的图像](displaying-a-table-of-database-data-cs/_static/image14.png)）

如果您不喜欢图7中数据库记录网格外观的任何内容，则可以直接修改索引视图。 例如，可以通过修改 "索引" 视图将*DateReleased*标头更改为 "已*发布*"。

## <a name="create-a-template-with-a-partial"></a>创建部分为的模板

视图变得过于复杂时，最好开始将视图分解为分区。 使用分区可使你的视图更易于理解和维护。 我们将创建一个部分，可将其用作模板来设置每个电影数据库记录的格式。

请按照以下步骤创建部分：

1. 右键单击 Views\Movie 文件夹，然后选择 "**添加视图**" 菜单。
2. 选中标签为 "*创建分部视图（.ascx）* " 的复选框。
3. 将部分*MovieTemplate*命名为。
4. 选中标签为 "**创建强类型视图**" 的复选框。
5. 选择 "影片" 作为 "*视图数据类*"。
6. 选择 "空" 作为 "*视图内容*"。
7. 单击 "**添加**" 按钮，将部分添加到您的项目中。

完成这些步骤后，将 MovieTemplate 部分修改为类似于列表3的外观。

**列表 3-Views\Movie\MovieTemplate.ascx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample3.aspx)]

列表3中的部分包含一个用于记录单行的模板。

列表4中修改的索引视图使用 MovieTemplate 部分。

**列表 4-Views\Movie\Index.aspx**

[!code-aspx[Main](displaying-a-table-of-database-data-cs/samples/sample4.aspx)]

列表4中的视图包含一个用于循环访问所有影片的 foreach 循环。 对于每个电影，将使用 MovieTemplate 部分来设置电影的格式。 MovieTemplate 通过调用 RenderPartial （） helper 方法呈现。

修改后的 "索引" 视图呈现数据库记录的完全相同的 HTML 表。 不过，视图已大大简化。

RenderPartial （）方法不同于大多数其他 helper 方法，因为它不返回字符串。 因此，必须使用 &lt;% RenderPartial （）调用 RenderPartial （）方法;%&gt; 而不是 &lt;% = RenderPartial （）;%&gt;。

## <a name="summary"></a>摘要

本教程的目的是说明如何在 HTML 表中显示一组数据库记录。 首先，您学习了如何通过利用 Microsoft 实体框架从控制器操作返回一组数据库记录。 接下来，您学习了如何使用 Visual Studio 基架生成一个视图，该视图自动显示项的集合。 最后，您学习了如何通过利用部分来简化视图。 您已经学习了如何使用部分模板作为模板，以便您可以对每个数据库记录进行格式设置。

> [!div class="step-by-step"]
> [上一页](creating-model-classes-with-linq-to-sql-cs.md)
> [下一页](performing-simple-validation-cs.md)
