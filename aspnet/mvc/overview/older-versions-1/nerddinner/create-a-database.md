---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 创建数据库 | Microsoft Docs
author: microsoft
description: 步骤2显示了创建包含我们的 NerdDinner 应用程序的所有晚餐和 RSVP 数据的数据库的步骤。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469298"
---
# <a name="create-a-database"></a>创建数据库

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第2步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤2显示了创建包含我们的 NerdDinner 应用程序的所有晚餐和 RSVP 数据的数据库的步骤。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner 步骤2：创建数据库

我们将使用数据库来存储 NerdDinner 应用程序的所有晚餐和 RSVP 数据。

下面的步骤演示如何使用免费的 SQL Server Express 版（可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 轻松安装）创建数据库。 我们编写的所有代码都适用于 SQL Server Express 和完整 SQL Server。

### <a name="creating-a-new-sql-server-express-database"></a>创建新的 SQL Server Express 数据库

首先，右键单击 web 项目，然后选择 "**添加-&gt;新项**" 菜单命令：

![](create-a-database/_static/image1.png)

这会显示 Visual Studio 的 "添加新项" 对话框。 我们将按 "数据" 类别进行筛选，然后选择 "SQL Server 数据库" 项模板：

![](create-a-database/_static/image2.png)

我们将为要创建的 SQL Server Express 数据库命名，并单击 "确定"。 然后，Visual Studio 会询问我们是否要将此文件添加到 \App\_数据目录（这是已设置了读写安全 Acl 的目录）：

![](create-a-database/_static/image3.png)

单击 "是" 将创建新数据库并将其添加到我们的解决方案资源管理器中：

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>在数据库中创建表

现在，我们有一个新的空数据库。 让我们向其中添加一些表。

为此，我们将导航到 Visual Studio 中的 "服务器资源管理器" 选项卡窗口，这使我们可以管理数据库和服务器。 SQL Server Express 存储在应用程序的 \App\_Data 文件夹中的数据库将自动显示在服务器资源管理器中。 可以选择使用 "服务器资源管理器" 窗口顶部的 "连接到数据库" 图标，同时将其他 SQL Server 数据库（本地和远程）添加到列表中：

![](create-a-database/_static/image5.png)

我们会将两个表添加到我们的 NerdDinner 数据库中-一个用于存储就，另一个用于跟踪 RSVP 历史性。 可以通过右键单击数据库中的 "Tables" 文件夹并选择 "添加新表" 菜单命令来创建新表：

![](create-a-database/_static/image6.png)

这将打开一个表设计器，它允许我们配置表的架构。 对于我们的 "就" 表，我们将添加10列数据：

![](create-a-database/_static/image7.png)

我们想要 "DinnerID" 列是表的唯一主键。 可以通过右键单击 "DinnerID" 列并选择 "设置主键" 菜单项来进行配置：

![](create-a-database/_static/image8.png)

除了将 DinnerID 设置为主键外，还需要将其配置为 "标识" 列，该列的值自动递增，因为新行的数据将添加到表中（也就是说，第一个插入的晚餐行的 DinnerID 为1，第二个插入的行将具有2的 DinnerID，等等）。

为此，我们可以选择 "DinnerID" 列，然后使用 "列属性" 编辑器将该列的 "（是标识）" 属性设置为 "是"。 我们将使用标准标识默认值（从1开始，在每个新晚餐行的增量为1）：

![](create-a-database/_static/image9.png)

然后，通过键入 Ctrl S 或使用**文件&gt;** 的 "保存" 菜单命令保存表。 这会提示我们为该表命名。 我们会将其命名为 "就"：

![](create-a-database/_static/image10.png)

新的就表随后将显示在服务器资源管理器中的数据库中。

然后，重复上述步骤，并创建一个 "RSVP" 表。 此表具有3列。 我们会将 RsvpID 列设置为主键，并使其成为标识列：

![](create-a-database/_static/image11.png)

我们会将其保存，并为其指定名称 "RSVP"。

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>设置表之间的外键关系

现在，我们的数据库中有两个表。 我们的最后一个架构设计步骤是在这两个表之间设置 "一对多" 关系，以便将每个晚餐行与适用于它的零个或多个 RSVP 行相关联。 为此，我们将配置 RSVP 表的 "DinnerID" 列，使其与 "就" 表中的 "DinnerID" 列之间具有外键关系。

为此，我们将通过在 "服务器资源管理器" 中双击来打开 "表设计器" 中的 "RSVP" 表。 然后，选择其中的 "DinnerID" 列，右键单击，然后选择 "关系 ..."上下文菜单命令：

![](create-a-database/_static/image12.png)

这会显示一个对话框，可用于设置表之间的关系：

![](create-a-database/_static/image13.png)

我们将单击 "添加" 按钮将新的关系添加到对话框中。 添加了关系后，我们将在对话框右侧的属性网格中展开 "表和列规范" 树视图节点，然后单击 "..."按钮右侧：

![](create-a-database/_static/image14.png)

单击 "..."按钮将显示另一个对话框，该对话框允许您指定关系中涉及的表和列，并使我们能够命名关系。

我们将主键表更改为 "就"，并在就表中选择 "DinnerID" 列作为主键。 RSVP 表将为外键表和 RSVP。DinnerID 列将与外键关联：

![](create-a-database/_static/image15.png)

现在，RSVP 表中的每一行都与晚餐表中的一行相关联。 SQL Server 将为我们维护引用完整性，并防止我们添加新的 RSVP 行（如果它未指向有效的晚餐行）。 如果仍有 RSVP 行引用它，它还会阻止我们删除晚餐行。

### <a name="adding-data-to-our-tables"></a>向表中添加数据

首先，将一些示例数据添加到就表中。 可以通过在服务器资源管理器中右键单击数据，然后选择 "显示表数据" 命令，将数据添加到表中：

![](create-a-database/_static/image16.png)

我们将添加几行晚餐数据，我们稍后会在开始实现应用程序时使用这些数据：

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>下一步

我们已经完成了数据库的创建。 现在，让我们创建可用于查询和更新模型的类。

> [!div class="step-by-step"]
> [上一页](create-a-new-aspnet-mvc-project.md)
> [下一页](build-a-model-with-business-rule-validations.md)
