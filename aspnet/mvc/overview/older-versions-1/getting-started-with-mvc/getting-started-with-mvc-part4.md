---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: 创建数据库 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469670"
---
# <a name="creating-a-database"></a>创建数据库

作者： [Scott Hanselman](https://github.com/shanselman)

> 本教程介绍了 ASP.NET MVC 的基本知识。 你将创建一个简单的 web 应用程序，用于读取和写入数据库。 请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。

在本部分中，我们将创建一个新的 SQL Express 数据库，我们将使用它来存储和检索电影数据。 在 Visual Web Developer IDE 中，选择 "视图" |服务器资源管理器。 右键单击 "数据连接"，然后单击 "添加连接 ..."

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

在 "选择数据源" 对话框中，选择 Microsoft SQL Server，然后选择 "继续"。

![](getting-started-with-mvc-part4/_static/image2.png)

在 "添加连接" 对话框中，输入 ".\SQLEXPRESS" 作为你的服务器名称，然后输入 "电影" 作为新数据库的名称。

[!["添加连接" 对话框](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

单击 "确定"，系统会询问您是否要创建该数据库。 选择 "是"。

[![创建电影？](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

现在，你已在服务器资源管理器中获取了一个空数据库。

![添加新表](getting-started-with-mvc-part4/_static/image7.png)

右键单击表，然后单击 "添加表"。 将显示表设计器。 添加 Id、标题、ReleaseDate、流派和价格的列。 右键单击 ID 列，然后单击 "设置主键"。 我的设计区域如下所示。

[![数据库表编辑器](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

此外，选择 "Id" 列，然后在 "列属性" 下，将 "标识规范" 更改为 "是"。

[![IsIdentity-列属性](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

完成后，单击工具栏中的 "保存" 图标或选择 "文件" |从菜单中保存，并将表命名为 "**Movie**" （单数形式）。 我们已经有了一个数据库和一个表！

[![选择名称](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

返回服务器资源管理器，右键单击电影表，然后选择 "显示表数据"。 输入几个电影，以便我们的数据库具有一些数据。

[![数据库表编辑](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a>创建模型

现在，切换回 IDE 右端的解决方案资源管理器，右键单击 "模型" 文件夹，然后选择 "添加 |新建项。

[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

我们将从新数据库创建实体模型。 这会向项目中添加一组类，使我们可以轻松地查询和操作数据库中的数据。 选择对话框左侧的 "数据" 节点，然后选择 "ADO.NET 实体数据模型项" 模板。 将其命名为 "电影"。

[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

单击 "添加" 按钮。 然后，这将启动 "实体数据模型向导"。

在弹出的新对话框中，选择 "从数据库生成"。 由于我们刚刚创建了一个数据库，因此，我们只需告诉实体框架我们的新数据库和表。 单击 "下一步"，在 web 应用程序的配置中保存数据库连接。 现在，选中 "表和电影" 复选框，然后单击 "完成"。

[![实体数据模型向导](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

现在，我们可以在 Entity Framework Designer 中看到新的电影表，并从代码访问它。

[![电影-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

在设计图面上，您可以看到一个 "电影" 类。 此类映射到数据库中的 "Movie" 表，其中的每个属性都映射到具有表的列。 "Movie" 类的每个实例都对应于 "影片" 表中的一行。

如果你不喜欢实体框架使用的默认命名和映射约定，则可以使用实体框架设计器来更改或自定义它们。 对于此应用程序，我们将使用默认值，只需按原样保存文件。

现在，让我们处理一些真实的数据！

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part3.md)
> [下一页](getting-started-with-mvc-part5.md)
