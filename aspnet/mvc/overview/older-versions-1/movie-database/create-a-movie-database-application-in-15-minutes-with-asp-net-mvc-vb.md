---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: 使用 ASP.NET MVC 在15分钟内创建电影数据库应用程序（VB） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 从头开始构建整个数据库驱动的 ASP.NET MVC 应用程序。 本教程非常介绍了新的 t 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ce8161d29a8ab4005e2b20462b08c9e10ee815a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435770"
---
# <a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a>使用 ASP.NET MVC 在 15 分钟内创建电影数据库应用程序 (VB)

作者： [Stephen Walther](https://github.com/StephenWalther)

[下载代码](https://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> Stephen Walther 从头开始构建整个数据库驱动的 ASP.NET MVC 应用程序。 本教程非常介绍了 ASP.NET MVC 框架的新手，并希望了解构建 ASP.NET MVC 应用程序的过程。

本教程的目的是让你了解一下如何构建 ASP.NET MVC 应用程序。 在本教程中，我将从开始到完成构建整个 ASP.NET MVC 应用程序。 我向您展示了如何构建一个简单的数据库驱动的应用程序，该应用程序说明了如何列出、创建和编辑数据库记录。

为了简化生成应用程序的过程，我们将利用 Visual Studio 2008 的基架功能。 我们会让 Visual Studio 为控制器、模型和视图生成初始代码和内容。

如果你使用的是 Active Server Pages 或 ASP.NET，则应该会发现 ASP.NET MVC 非常熟悉。 ASP.NET MVC 视图非常类似于 Active Server Pages 应用程序中的页面。 与传统的 ASP.NET Web 窗体应用程序一样，ASP.NET MVC 为你提供 .NET framework 提供的丰富语言和类的完全访问权限。

我希望在本教程中，您可以了解构建 ASP.NET MVC 应用程序的体验与生成 Active Server Pages 或 ASP.NET Web 窗体应用程序的体验是类似的。

## <a name="overview-of-the-movie-database-application"></a>电影数据库应用程序概述

由于我们的目标是简单起见，我们将构建一个非常简单的电影数据库应用程序。 简单的电影数据库应用程序将允许我们执行以下三项操作：

1. 列出一组电影数据库记录
2. 创建新的电影数据库记录
3. 编辑现有的电影数据库记录

同样，由于我们想要简单简单，我们将利用构建应用程序所需的 ASP.NET MVC 框架的最小功能数。 例如，我们不会利用测试驱动的开发。

若要创建应用程序，需要完成以下每个步骤：

1. 创建 ASP.NET MVC Web 应用程序项目
2. 创建数据库
3. 创建数据库模型
4. 创建 ASP.NET MVC 控制器
5. 创建 ASP.NET MVC 视图

## <a name="preliminaries"></a>初步操作

需要 Visual Studio 2008 或 Visual Web Developer 2008 Express 才能生成 ASP.NET MVC 应用程序。 还需要下载 ASP.NET MVC 框架。

如果你没有 Visual Studio 2008，你可以从以下网站90下载试用版的 Visual Studio 2008：

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

或者，可以通过 Visual Web Developer Express 2008 创建 ASP.NET MVC 应用程序。 如果决定使用 Visual Web Developer Express，则必须安装 Service Pack 1。 你可以从此网站下载 Visual Web Developer 2008 Express Service Pack 1：

[https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

安装 Visual Studio 2008 或 Visual Web Developer 2008 后，需要安装 ASP.NET MVC 框架。 你可以从以下网站下载 ASP.NET MVC 框架：

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> 你可以利用 Web 平台安装程序，而不是单独下载 ASP.NET framework 和 ASP.NET MVC 框架。 Web 平台安装程序是一种应用程序，使你能够轻松地管理已安装的应用程序是否为你的计算机：
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)

## <a name="creating-an-aspnet-mvc-web-application-project"></a>创建 ASP.NET MVC Web 应用程序项目

首先，让我们在 Visual Studio 2008 中创建新的 ASP.NET MVC Web 应用程序项目。 选择菜单选项 "**文件"、"新建项目**"，您将看到图1中的 "新建项目" 对话框。 选择 "Visual Basic" 作为编程语言，然后选择 "ASP.NET MVC Web 应用程序" 项目模板。 为项目指定名称 MovieApp，然后单击 "确定" 按钮。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)

**图 01**： "新建项目" 对话框（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png)）

请确保从 "新建项目" 对话框顶部的下拉列表中选择 .NET Framework 3.5，否则不会出现 "ASP.NET MVC Web 应用程序" 项目模板。

每次创建新的 MVC Web 应用程序项目时，Visual Studio 都会提示您创建一个单独的单元测试项目。 图2中的对话框随即出现。 由于我们不会在本教程中创建测试，因为存在时间限制（是的，我们应该感觉到投机取巧），请选择 "**否**" 选项，然后单击 **"确定"** 按钮。

> [!NOTE] 
> 
> Visual Web Developer 不支持测试项目。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)

**图 02**： "创建单元测试项目" 对话框（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png)）

ASP.NET MVC 应用程序具有一组标准文件夹：模型、视图和控制器文件夹。 您可以在 "解决方案资源管理器" 窗口中查看此标准文件夹集。 为了构建电影数据库应用程序，我们需要将文件添加到每个模型、视图和控制器文件夹中。

使用 Visual Studio 创建新的 MVC 应用程序时，将获得一个示例应用程序。 由于我们要从头开始，我们需要删除此示例应用程序的内容。 需要删除以下文件和下列文件夹：

- Controllers\HomeController.vb
- Views\Home

## <a name="creating-the-database"></a>创建数据库

我们需要创建一个数据库来存放电影数据库记录。 幸运的是，Visual Studio 包括一个名为 SQL Server Express 的免费数据库。 按照以下步骤创建数据库：

1. 右键单击 "解决方案资源管理器" 窗口中的 "应用\_Data" 文件夹，然后选择 "**添加"、"新建项**" 菜单。
2. 选择 "**数据**" 类别，然后选择 " **SQL Server" 数据库**模板（请参阅图3）。
3. 将新数据库命名为*MoviesDB* ，然后单击 "**添加**" 按钮。

创建数据库后，可以通过双击位于应用\_Data 文件夹中的 MoviesDB 文件来连接到数据库。 双击 MoviesDB 文件将打开 "服务器资源管理器" 窗口。

> [!NOTE] 
> 
> 在 Visual Web Developer 的情况下，"服务器资源管理器" 窗口称为数据库资源管理器 "窗口。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)

**图 03**：创建 Microsoft SQL Server 数据库（[单击查看完全大小的映像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png)）

接下来，需要创建一个新的数据库表。 从 "服务器资源管理器" 窗口中，右键单击 "表" 文件夹，然后选择菜单选项 "**添加新表**"。 选择此菜单选项将打开数据库表设计器。 创建以下数据库列：

<a id="0.2_table01"></a>

| **列名称** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| Id | Int | False |
| 标题 | Nvarchar(100) | False |
| 导演 | Nvarchar(100) | False |
| DateReleased | DateTime | False |

第一列（Id 列）包含两个特殊属性。 首先，需要将 Id 列标记为主键列。 选择 Id 列后，单击 "**设置主键**" 按钮（它是看起来像一个键的图标）。 其次，需要将 Id 列标记为标识列。 在属性窗口列中，向下滚动到 "标识规范" 部分并展开它。 将 "**是" 标识**属性更改为 **"是"** 。 完成后，表应如图4所示。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)

**图 04**：电影数据库表（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png)）

最后一步是保存新表。 单击 "保存" 按钮（软盘的图标），并为新表命名为 "电影"。

创建完表后，将一些电影记录添加到表中。 右键单击 "服务器资源管理器" 窗口中的 "电影" 表，然后选择菜单选项 "**显示表数据**"。 输入喜欢的电影列表（见图5）。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)

**图 05**：输入电影记录（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png)）

## <a name="creating-the-model"></a>创建模型

接下来，需要创建一组类以表示数据库。 我们需要创建一个数据库模型。 我们将利用 Microsoft 实体框架自动为数据库模型生成类。

> [!NOTE] 
> 
> ASP.NET MVC 框架不与 Microsoft 实体框架相关联。 可以通过利用各种对象关系映射（或/M）工具（包括 LINQ to SQL、Subsonic 和 NHibernate）来创建数据库模型类。

请按照以下步骤启动实体数据模型向导：

1. 右键单击 "解决方案资源管理器" 窗口中的 "模型" 文件夹，然后选择 "**添加"、"新建项**" 菜单。
2. 选择 "**数据**" 类别，然后选择 " **ADO.NET 实体数据模型**" 模板。
3. 为数据模型指定名称*MoviesDBModel* ，并单击 "**添加**" 按钮。

单击 "添加" 按钮后，将显示 "实体数据模型" 向导（见图6）。 按照以下步骤完成向导：

1. 在 "**选择模型内容**" 步骤中，选择 "**从数据库生成**" 选项。
2. 在 "**选择你的数据连接**" 步骤中，使用*MoviesDB*数据连接，并为连接设置使用名称 " *MoviesDBEntities* "。 单击“下一步”按钮。
3. 在 "**选择数据库对象**" 步骤中，展开 "表" 节点，然后选择 "电影" 表。 输入命名空间*MovieApp* ，并单击 "**完成**" 按钮。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)

**图 06**：使用实体数据模型向导生成数据库模型（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png)）

完成实体数据模型向导后，"实体数据模型设计器会打开。 设计器应显示电影数据库表（参见图7）。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)

**图 07**：实体数据模型设计器（[单击查看完全尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png)）

在继续操作之前，我们需要进行一项更改。 实体数据向导将生成一个名为电影的模型类，该类表示电影数据库表。 由于我们将使用 movie 类来表示特定电影，因此我们需要将类的名称修改为*电影*，而不是*影片*（单数形式）。

双击设计器图面上类的名称，并将类的名称从 "电影" 更改为 "电影"。 做出此更改后，单击 "**保存**" 按钮（软盘的图标）以生成 Movie 类。

## <a name="creating-the-aspnet-mvc-controller"></a>创建 ASP.NET MVC 控制器

下一步是创建 ASP.NET MVC 控制器。 控制器负责控制用户如何与 ASP.NET MVC 应用程序交互。

请执行这些步骤：

1. 在 "解决方案资源管理器" 窗口中，右键单击 "控制器" 文件夹，然后选择 "**添加"、"控制器**" 菜单。
2. 在 "添加控制器" 对话框中，输入名称*HomeController* ，并选中标签为 "**添加" "创建"、"更新" 和 "详细信息" 方案的 "操作方法**" 的复选框（见图8）
3. 单击 "**添加**" 按钮将新的控制器添加到项目。

完成这些步骤后，会创建列表1中的控制器。 请注意，它包含名为索引、详细信息、创建和编辑的方法。 在以下部分中，我们将添加所需的代码以使这些方法正常工作。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)

**图 08**：添加新的 ASP.NET MVC 控制器（[单击以查看完全大小的映像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png)）

**列表1– Controllers\HomeController.vb**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a>列出数据库记录

Home 控制器的 Index （）方法是 ASP.NET MVC 应用程序的默认方法。 运行 ASP.NET MVC 应用程序时，Index （）方法是调用的第一个控制器方法。

我们将使用 Index （）方法显示电影数据库表中的记录列表。 我们将利用之前创建的数据库模型类，通过 Index （）方法检索电影数据库记录。

我修改了清单2中的 HomeController 类，使其包含一个名为 \_db 的新私有字段。 MoviesDBEntities 类表示我们的数据库模型，我们将使用此类与数据库进行通信。

我还在清单2中修改了 Index （）方法。 Index （）方法使用 MoviesDBEntities 类来检索电影数据库表中的所有电影记录。 表达式 *\_db。MovieSet. System.linq.enumerable.tolist （）* 返回电影数据库表中所有电影记录的列表。

电影列表将传递给视图。 传递给 View （）方法的任何内容都将作为视图数据传递给视图。

**列出2–控制器/HomeController （修改的索引方法）**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

Index （）方法返回一个名为 Index 的视图。 需要创建此视图来显示电影数据库记录的列表。 请执行这些步骤：

在打开 "**添加视图**" 对话框或在 "**查看数据类**" 下拉列表中未显示任何类之前，应生成项目（选择菜单选项 "**生成"、"生成解决方案**"）。

1. 在代码编辑器中右键单击 Index （）方法，然后选择菜单选项 "**添加视图**" （参见图9）。
2. 在 "添加视图" 对话框中，验证是否选中了标记为 "**创建强类型视图**" 的复选框。
3. 从 "**查看内容**" 下拉列表中，选择 "值"*列表*。
4. 从 "**查看数据类**" 下拉列表中，选择值*MovieApp*。
5. 单击 "添加" 按钮创建新视图（请参阅图10）。

完成这些步骤后，会将名为 "Views\Home" 的新视图添加到 "" 文件夹。 索引视图的内容包括在列表3中。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)

**图 09**：通过控制器操作添加视图（[单击查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png)）

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)

**图 10**：使用 "添加视图" 对话框创建新视图（[单击查看完全尺寸的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png)）

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

"索引" 视图显示 HTML 表中电影数据库表的所有电影记录。 视图包含一个 For Each 循环，该循环遍历 ViewData 属性所表示的每个电影。 如果通过按 F5 键运行应用程序，则会看到图11中的网页。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)

**图 11**： "索引" 视图（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png)）

## <a name="creating-new-database-records"></a>创建新的数据库记录

在上一部分中创建的 "索引" 视图包含用于创建新数据库记录的链接。 接下来，实现逻辑，并创建创建新的电影数据库记录所需的视图。

Home 控制器包含两个名为 Create （）的方法。 第一个 Create （）方法没有参数。 Create （）方法的此重载用于显示用于创建新的电影数据库记录的 HTML 窗体。

第二个 Create （）方法具有 FormCollection 参数。 在将用于创建新电影的 HTML 表单发送到服务器时，将调用 Create （）方法的此重载。 请注意，第二个 Create （）方法具有 AcceptVerbs 属性，该属性阻止调用方法，除非执行 HTTP Post 操作。

此第二个 Create （）方法已在清单4的更新的 HomeController 类中进行了修改。 新版本的 Create （）方法接受 Movie 参数，并包含用于将新电影插入到电影数据库表的逻辑。

> [!NOTE] 
> 
> 请注意 "绑定" 属性。 由于我们不想更新 HTML 格式的电影 Id 属性，因此需要显式排除此属性。

**列表4– Controllers\HomeController.vb （已修改的 Create 方法）**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

使用 Visual Studio 可以轻松地创建新的电影数据库记录（见图12）。 请执行这些步骤：

1. 在代码编辑器中右键单击 Create （）方法，然后选择菜单选项 "**添加视图**"。
2. 验证标记为 "**创建强类型视图**" 的复选框。
3. 从 "**查看内容**" 下拉列表中，选择 "值" "*创建*"。
4. 从 "**查看数据类**" 下拉列表中，选择值*MovieApp*。
5. 单击 "**添加**" 按钮创建新视图。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)

**图 12**：添加 "创建" 视图（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png)）

Visual Studio 会自动生成列表5中的视图。 此视图包含一个 HTML 窗体，其中包含与 Movie 类的每个属性对应的字段。

**列表5– Views\Home\Create.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> "添加视图" 对话框生成的 HTML 窗体将生成一个 Id 窗体字段。 由于 Id 列是标识列，因此不需要此窗体字段，你可以安全地将其删除。

添加 "创建" 视图后，可以将新的电影记录添加到数据库中。 按 F5 键运行应用程序，并单击 "新建" 链接以查看图13中的窗体。 如果完成并提交了窗体，则将创建一个新的电影数据库记录。

请注意，会自动获得窗体验证。 如果您忘记为电影输入发布日期或输入无效的发布日期，则会重新显示窗体，并突出显示 "发布日期" 字段。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)

**图 13**：创建新的电影数据库记录（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png)）

## <a name="editing-existing-database-records"></a>编辑现有的数据库记录

在前面的部分中，我们讨论了如何列出和创建新的数据库记录。 在此最后一节中，我们将讨论如何编辑现有的数据库记录。

首先，我们需要生成编辑窗体。 此步骤很简单，因为 Visual Studio 会自动为我们生成编辑窗体。 在 Visual Studio 代码编辑器中打开 HomeController 类，然后执行以下步骤：

1. 右键单击代码编辑器中的 Edit （）方法，然后选择 "**添加视图**" 菜单选项（见图14）。
2. 选中标签为 "**创建强类型视图**" 的复选框。
3. 从 "**查看内容**" 下拉列表中，选择 "值" "*编辑*"。
4. 从 "**查看数据类**" 下拉列表中，选择值*MovieApp*。
5. 单击 "**添加**" 按钮创建新视图。

完成这些步骤后，会将名为 "Views\Home" 的新视图添加到 "" 文件夹。 此视图包含用于编辑电影记录的 HTML 窗体。

[!["新建项目" 对话框](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)

**图 14**：添加编辑视图（[单击以查看完全大小的图像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png)）

> [!NOTE] 
> 
> 编辑视图包含与 "电影 Id" 属性相对应的 HTML 表单域。 由于不希望用户编辑 Id 属性的值，因此应删除此窗体字段。

最后，我们需要修改 Home 控制器，使其支持编辑数据库记录。 已更新的 HomeController 类包含在列表6中。

**清单6– Controllers\HomeController.vb （编辑方法）**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

在列表6中，我已将其他逻辑添加到了 Edit （）方法的两个重载。 第一个 Edit （）方法返回与传递给该方法的 Id 参数相对应的电影数据库记录。 第二个重载对数据库中的电影记录执行更新。

请注意，必须检索原始电影，然后调用 ApplyPropertyChanges （）来更新数据库中的现有电影。

## <a name="summary"></a>摘要

本教程的目的是让你了解构建 ASP.NET MVC 应用程序的体验。 我希望您发现生成 ASP.NET MVC web 应用程序的过程与生成 Active Server Pages 或 ASP.NET 应用程序的体验非常类似。

在本教程中，我们仅检查了 ASP.NET MVC 框架的最基本功能。 在将来的教程中，我们将深入探讨控制器、控制器操作、视图、视图数据和 HTML 帮助器等主题。

> [!div class="step-by-step"]
> [上一页](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)
