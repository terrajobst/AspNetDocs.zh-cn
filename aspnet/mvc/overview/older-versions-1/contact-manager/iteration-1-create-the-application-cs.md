---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
title: '迭代 #1 –创建应用程序（C#） |Microsoft Docs'
author: microsoft
description: 在第一次迭代中，我们以尽可能简单的方式创建联系人管理器。 添加对基本数据库操作的支持： Create、Read、Update 和 D 。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: db0f160b-901c-46d3-865e-7ab6cd4ed68d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
msc.type: authoredcontent
ms.openlocfilehash: d3a940308f21a4f87bf80249bd465e8812794f68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470264"
---
# <a name="iteration-1--create-the-application-c"></a>迭代 #1 –创建应用程序（C#）

由[Microsoft](https://github.com/microsoft)

[下载代码](iteration-1-create-the-application-cs/_static/contactmanager_1_cs1.zip)

> 在第一次迭代中，我们以尽可能简单的方式创建联系人管理器。 添加对基本数据库操作的支持：创建、读取、更新和删除（CRUD）。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序（VB）

在本系列教程中，我们从一开始就生成一个完整的联系人管理应用程序。 联系人管理器应用程序允许您存储联系人信息名称、电话号码和电子邮件地址，以获取人员列表。

我们通过多个迭代生成应用程序。 随着每次迭代，我们将逐步改进应用程序。 此多个迭代方法的目标是使您能够了解每个更改的原因。

- 迭代 #1-创建应用程序。 在第一次迭代中，我们以尽可能简单的方式创建联系人管理器。 添加对基本数据库操作的支持：创建、读取、更新和删除（CRUD）。

- 迭代 #2-使应用程序看起来不错。 在此迭代中，我们通过修改默认的 ASP.NET MVC 视图母版页和级联样式表来改善应用程序的外观。

- 迭代 #3-添加窗体验证。 在第三次迭代中，我们将添加基本的窗体验证。 我们阻止用户提交窗体，而无需填写所需的窗体字段。 我们还验证了电子邮件地址和电话号码。

- 迭代 #4-使应用程序松散耦合。 在第四次迭代中，我们将利用多种软件设计模式来更轻松地维护和修改联系人管理器应用程序。 例如，我们重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 #5-创建单元测试。 在第五次迭代中，通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑生成单元测试。

- 迭代 #6-使用测试驱动开发。 在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。 在此迭代中，我们添加联系人组。

- 迭代 #7-添加 Ajax 功能。 在第七次迭代中，我们通过添加对 Ajax 的支持来提高应用程序的响应能力和性能。

## <a name="this-iteration"></a>此迭代

在第一次迭代中，我们将构建基本应用程序。 目标是以尽可能快、最简单的方式构建联系人管理器。 在后续迭代中，我们改进了应用程序的设计。

联系人管理器应用程序是一个基本的数据库驱动的应用程序。 您可以使用应用程序创建新联系人、编辑现有联系人和删除联系人。

在此迭代中，我们完成了以下步骤：

1. ASP.NET MVC 应用程序
2. 创建数据库以存储联系人
3. 使用 Microsoft 实体框架为数据库生成模型类
4. 创建控制器操作和视图，使我们能够列出数据库中的所有联系人
5. 创建控制器操作和一个视图，使我们能够在数据库中创建新联系人
6. 创建控制器操作和一个视图，使我们能够编辑数据库中的现有联系人
7. 创建允许删除数据库中现有联系人的控制器操作和视图

## <a name="software-prerequisites"></a>软件必备项

在 ASP.NET MVC 应用程序中，您的计算机上必须安装有 Visual Studio 2008 或 Visual Web Developer 2008 （Visual Web Developer 是 Visual Studio 的免费版本，不包括 Visual Studio 的所有高级功能）。 你可以从以下地址下载 Visual Studio 2008 或 Visual Web Developer 的试用版：

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> 对于使用 Visual Web Developer 的 ASP.NET MVC 应用程序，必须安装 Visual Web Developer Service Pack 1。 不带 Service Pack 1 的情况下，无法创建 Web 应用程序项目。

ASP.NET MVC 框架。 可以从以下地址下载 ASP.NET MVC 框架：

[https://www.asp.net/mvc](../../../index.md)

在本教程中，我们将使用 Microsoft 实体框架来访问数据库。 实体框架包含在 .NET Framework 3.5 Service Pack 1 中。 可以从以下位置下载此 Service Pack：

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

作为一种替代方法，你可以使用 Web 平台安装程序（Web PI）。 你可以从以下地址下载 Web PI：

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC 项目

ASP.NET MVC Web 应用程序项目。 启动 Visual Studio 并选择 "菜单" "**文件" "新建项目**"。 此时将显示 "**新建项目**" 对话框（请参阅图1）。 选择**Web**项目类型和**ASP.NET MVC Web 应用程序**模板。 将新项目命名为 " *ContactManager* "，然后单击 "确定" 按钮。

请确保在 "**新建项目**" 对话框右上角的下拉列表中选择了 .NET Framework 3.5。 否则，ASP.NET MVC Web 应用程序模板不会出现。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)

**图 01**： "新建项目" 对话框（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image2.png)）

ASP.NET MVC 应用程序时，将显示 "**创建单元测试项目**" 对话框。 你可以使用此对话框来指示你希望在创建 ASP.NET MVC 应用程序时创建单元测试项目并将其添加到解决方案中。 尽管我们不会在此迭代中构建单元测试，但应选择选项 **"是，创建单元测试项目**"，因为我们计划在以后的迭代中添加单元测试。 当你首次创建新的 ASP.NET MVC 项目时添加测试项目比在创建 ASP.NET MVC 项目后添加测试项目要容易得多。

> [!NOTE] 
> 
> 因为 Visual Web Developer 不支持测试项目，所以在使用 Visual Web Developer 时，您不会获得 "创建单元测试项目" 对话框。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)

**图 02**： "创建单元测试项目" 对话框（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image4.png)）

ASP.NET MVC 应用程序将显示在 Visual Studio 解决方案资源管理器窗口中（请参阅图3）。 如果看不到 "解决方案资源管理器" 窗口，则可以通过选择 "菜单" 选项**视图，解决方案资源管理器**打开此窗口。 请注意，该解决方案包含两个项目： ASP.NET MVC 项目和测试项目。 ASP.NET MVC 项目名为 ContactManager，测试项目命名为 ContactManager。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)

**图 03**： "解决方案资源管理器" 窗口（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image6.png)）

## <a name="deleting-the-project-sample-files"></a>删除项目示例文件

ASP.NET MVC 项目模板包含控制器和视图的示例文件。 在创建新的 ASP.NET MVC 应用程序之前，应删除这些文件。 您可以通过右键单击文件或文件夹，然后选择 "**删除**" 菜单选项，删除 "解决方案资源管理器" 窗口中的文件和文件夹。

需要从 ASP.NET MVC 项目删除以下文件：

- \Controllers\HomeController.cs

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

而且，您需要从测试项目删除以下文件：

\Controllers\HomeControllerTest.cs

## <a name="creating-the-database"></a>创建数据库

联系人管理器应用程序是数据库驱动的 web 应用程序。 我们使用数据库来存储联系信息。

包含 Microsoft SQL Server、Oracle、MySQL 和 IBM DB2 数据库的任何现代数据库的 ASP.NET MVC 框架。 在本教程中，我们使用 Microsoft SQL Server 的数据库。 安装 Visual Studio 时，可以选择安装 Microsoft SQL Server Express，这是 Microsoft SQL Server 数据库的免费版本。

右键单击 "解决方案资源管理器" 窗口中\_Data "文件夹的" 应用 "，然后选择"**添加 "、" 新建项**"菜单选项，创建一个新数据库。 在 "**添加新项**" 对话框中，选择 "**数据**" 类别和 " **SQL Server" 数据库**模板（参见图4）。 将新数据库命名为 ContactManagerDB，然后单击 "确定" 按钮。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)

**图 04**：创建新的 Microsoft SQL Server Express 数据库（[单击查看完全大小的映像](iteration-1-create-the-application-cs/_static/image8.png)）

创建新数据库后，该数据库将显示在 "应用\_Data" 文件夹的 "解决方案资源管理器" 窗口中。 双击 ContactManager 文件以打开 "服务器资源管理器" 窗口并连接到数据库。

> [!NOTE] 
> 
> 在 Microsoft Visual Web Developer 的情况下，"服务器资源管理器" 窗口称为数据库资源管理器 "窗口。

您可以使用 "服务器资源管理器" 窗口创建新的数据库对象，例如数据库表、视图、触发器和存储过程。 右键单击 "表" 文件夹，然后选择 "**添加新表**" 菜单选项。 此时将显示数据库表设计器（参见图5）。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)

**图 05**：数据库表设计器（[单击查看完全大小的映像](iteration-1-create-the-application-cs/_static/image10.png)）

我们需要创建一个包含以下列的表：

<a id="0.1_table01"></a>

| **列名称** | **数据类型** | **允许 Null 值** |
| --- | --- | --- |
| Id | int | 否 |
| FirstName | nvarchar(50) | 否 |
| LastName | nvarchar(50) | 否 |
| 电话 | nvarchar(50) | 否 |
| 电子邮件 | nvarchar(255) | 否 |

第一列是 "Id" 列。 需要将 Id 列标记为标识列和主键列。 通过展开 "列属性" （查看图6的底部）并向下滚动到 "标识规范" 属性，可以指示列是标识列。 将 " **（是标识）** " 属性设置为 **"是"** 。

通过选择列并单击带有键图标的按钮，可以将列标记为主键列。 将列标记为主键列后，列的旁边将显示一个键的图标（参见图6）。

创建完表后，单击 "保存" 按钮（带有软盘图标的按钮）以保存新表。 为新表命名 "*联系人*"。

创建完联系人数据库表后，应将一些记录添加到表中。 右键单击 "服务器资源管理器" 窗口中的 "联系人" 表，然后选择菜单选项 "**显示表数据**"。 在出现的网格中输入一个或多个联系人。

## <a name="creating-the-data-model"></a>创建数据模型

ASP.NET MVC 应用程序包含模型、视图和控制器。 首先，我们创建一个模型类，该类表示我们在上一节中创建的 "联系人" 表。

在本教程中，我们将使用 Microsoft 实体框架自动从数据库生成模型类。

> [!NOTE] 
> 
> ASP.NET MVC 框架不会以任何方式与 Microsoft 实体框架相关联。 可以将 ASP.NET MVC 与其他数据库访问技术（包括 NHibernate、LINQ to SQL 或 ADO.NET）配合使用。

按照以下步骤创建数据模型类：

1. 右键单击 "解决方案资源管理器" 窗口中的 "模型" 文件夹，然后选择 "**添加"、"新建项"** 。 此时将显示 "**添加新项**" 对话框（见图6）。
2. 选择 "**数据**" 类别和 " **ADO.NET 实体数据模型**" 模板。 将数据模型命名为*ContactManagerModel* ，然后单击 "**添加**" 按钮。 此时将显示 "实体数据模型" 向导（参见图7）。
3. 在 "**选择模型内容**" 步骤中，选择 "**从数据库生成**" （参见图7）。
4. 在 "**选择你的数据连接**" 步骤中，选择 "ContactManagerDB" 数据库，然后输入实体连接设置的名称 " *ContactManagerDBEntities* " （参见图8）。
5. 在 "**选择数据库对象**" 步骤中，选中标记为 "表" 的复选框（请参阅图9）。 数据模型将包含数据库中包含的所有表（只有一个表，即 Contacts 表）。 输入命名空间*模型*。 单击 "完成" 按钮以完成该向导。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)

**图 06**： "添加新项" 对话框（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image12.png)）

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)

**图 07**：选择模型内容（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image14.png)）

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)

**图 08**：选择你的数据连接（[单击以查看完全大小的映像](iteration-1-create-the-application-cs/_static/image16.png)）

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)

**图 09**：选择数据库对象（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image18.png)）

完成实体数据模型向导后，将显示 "实体数据模型设计器"。 设计器将显示一个与要建模的每个表相对应的类。 应该会看到一个名为 Contacts 的类。

实体数据模型向导根据数据库表名称生成类名称。 几乎始终需要更改由向导生成的类的名称。 右键单击设计器中的 "联系人" 类，然后选择菜单选项 "**重命名**"。 将类的名称从联系人（复数）更改为 Contact （单数）。 更改类名称后，类应如图10所示。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)

**图 10**： Contact 类（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image20.png)）

此时，我们已创建了数据库模型。 我们可以使用 Contact 类来表示数据库中的特定联系人记录。

## <a name="creating-the-home-controller"></a>创建主控制器

下一步是创建主控制器。 Home 控制器是在 ASP.NET MVC 应用程序中调用的默认控制器。

右键单击 "解决方案资源管理器" 窗口中的 "控制器" 文件夹，然后选择菜单选项 "**添加" 和 "控制器"，** 创建 Home 控制器类（见图11）。 请注意标记为 "**为创建、更新和详细方案添加操作方法**" 的复选框。 请确保在单击 "**添加**" 按钮之前选中此复选框。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)

**图 11**：添加主控制器（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image22.png)）

当你创建 Home 控制器时，你将获得列表1中的类。

**列表 1-Controllers\HomeController.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample1.cs)]

## <a name="listing-the-contacts"></a>列出联系人

为了显示联系人数据库表中的记录，我们需要创建索引（）操作和索引视图。

主控制器已包含 Index （）操作。 我们需要修改此方法，使其看起来类似于 "列表 2"。

**列表 2-Controllers\HomeController.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample2.cs)]

请注意，列表2中的 Home 控制器类包含一个名为 \_实体的私有字段。 "\_实体" 字段表示数据模型中的实体。 使用 "\_实体" 字段可以与数据库进行通信。

Index （）方法返回一个视图，该视图表示联系人数据库表中的所有联系人。 表达式 \_实体。ContactSet. System.linq.enumerable.tolist （）将联系人列表作为泛型列表返回。

至此，我们已创建索引控制器，接下来需要创建索引视图。 在创建索引视图之前，通过选择 "**生成、生成解决方案**" 菜单选项，编译应用程序。 在添加视图之前应始终编译项目，以便在 "**添加视图**" 对话框中显示的模型类列表。

您可以通过右键单击 Index （）方法并选择菜单选项 "**添加视图**" （参见图12）来创建索引视图。 选择此菜单选项将打开 "**添加视图**" 对话框（请参阅图13）。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)

**图 12**：添加索引视图（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image24.png)）

在 "**添加视图**" 对话框中，选中标记为 "**创建强类型视图**" 的复选框。 选择 "查看数据类" ContactManager 和 "查看内容" 列表。 选择这些选项将生成一个显示联系人记录列表的视图。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)

**图 13**： "添加视图" 对话框（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image26.png)）

单击 "**添加**" 按钮时，会生成列表3中的索引视图。 请注意，在文件顶部显示的 &lt;% @ Page%&gt; 指令。 索引视图从 ViewPage&lt;IEnumerable&lt;ContactManager&gt;&gt; 类继承而来。 换言之，视图中的 Model 类表示联系人实体的列表。

索引视图的主体包含一个 foreach 循环，该循环可循环访问模型类所表示的每个联系人。 Contact 类的每个属性的值显示在一个 HTML 表中。

**列表 3-Views\Home\Index.aspx （未修改）**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample3.aspx)]

我们需要对 "索引" 视图进行一项修改。 由于我们未创建详细信息视图，我们可以删除详细信息链接。 从 "索引" 视图中查找并删除以下代码：

{id = item。Id}）%&gt;

修改索引视图后，可以运行联系人管理器应用程序。 选择菜单选项 "调试"、"启动调试" 或只需按 F5。 第一次运行应用程序时，将看到图14中的对话框。 选择 "**修改 web.config 文件以启用调试**" 选项，然后单击 "确定" 按钮。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)

**图 14**：启用调试（[单击以查看完全大小的映像](iteration-1-create-the-application-cs/_static/image28.png)）

默认情况下，将返回索引视图。 此视图列出联系人数据库表中的所有数据（见图15）。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)

**图 15**： "索引" 视图（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image30.png)）

请注意，"索引" 视图包含标记为 "在视图底部创建新" 的链接。 在下一部分中，你将了解如何创建新联系人。

## <a name="creating-new-contacts"></a>创建新联系人

若要使用户能够创建新联系人，需要将两个 Create （）操作添加到主控制器。 我们需要创建一个 Create （）操作来返回用于创建新联系人的 HTML 表单。 我们需要创建另一个 Create （）操作来执行新联系人的实际数据库插入。

需要添加到 Home 控制器的新 Create （）方法包含在列表4中。

**列表 4-Controllers\HomeController.cs （包含 Create 方法）**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample4.cs)]

可以使用 HTTP GET 调用第一个 Create （）方法，同时第二个 Create （）方法只能由 HTTP POST 调用。 换句话说，只能在发布 HTML 窗体时调用第二个 Create （）方法。 第一个 Create （）方法只返回一个视图，其中包含用于创建新联系人的 HTML 窗体。 第二个 Create （）方法更为有趣：将新联系人添加到数据库中。

请注意，第二个 Create （）方法已修改为接受 Contact 类的实例。 ASP.NET MVC 框架自动将从 HTML 窗体发布的窗体值绑定到此 Contact 类。 将 HTML Create 窗体中的每个窗体字段分配给 Contact 参数的属性。

请注意，Contact 参数使用 [Bind] 属性修饰。 [Bind] 特性用于从绑定中排除联系人 Id 属性。 由于 Id 属性表示标识属性，因此我们不想设置 Id 属性。

在 Create （）方法的主体中，实体框架用于在数据库中插入新的联系人。 新联系人将添加到现有的联系人集中，并调用 SaveChanges （）方法将这些更改推送回底层数据库。

您可以通过右键单击两个 Create （）方法并选择菜单选项 "**添加视图**" （参见图16）来生成用于创建新联系人的 HTML 窗体。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)

**图 16**：添加 "创建" 视图（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image32.png)）

在 "**添加视图**" 对话框中，选择 " **ContactManager** " 类和 "查看内容" 的 "**创建**" 选项（参见图17）。 单击 "**添加**" 按钮时，会自动生成 "创建" 视图。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)

**图 17**：查看页面分解（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image34.png)）

"创建" 视图包含 Contact 类的每个属性的窗体字段。 "创建" 视图的代码包含在列表5中。

**列表 5-Views\Home\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample5.aspx)]

修改 Create （）方法并添加 "创建" 视图后，可以运行 "联系人管理器" 应用程序并创建新联系人。 单击 "索引" 视图中**显示的 "新建" 链接**以导航到 "创建" 视图。 应会看到图18中的视图。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)

**图 18**：创建视图（[单击查看完全尺寸的图像](iteration-1-create-the-application-cs/_static/image36.png)）

## <a name="editing-contacts"></a>编辑联系人

添加用于编辑联系人记录的功能与添加用于创建新联系人记录的功能非常相似。 首先，我们需要向 Home 控制器类添加两个新的编辑方法。 列表6中包含这些新的 Edit （）方法。

**清单 6-Controllers\HomeController.cs （包含 Edit 方法）**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample6.cs)]

第一个 Edit （）方法由 HTTP GET 操作调用。 Id 参数传递到此方法，该方法表示正在编辑的联系人记录的 Id。 实体框架用于检索与 Id 匹配的联系人。将返回一个视图，其中包含用于编辑记录的 HTML 窗体。

第二个 Edit （）方法对数据库执行实际更新。 此方法接受 Contact 类的实例作为参数。 ASP.NET MVC 框架会自动将编辑窗体中的表单字段绑定到此类。 请注意，编辑联系人时，不要包含 [Bind] 属性（我们需要 Id 属性的值）。

实体框架用于将修改后的联系人保存到数据库。 必须首先从数据库中检索原始联系人。 接下来，调用实体框架 ApplyPropertyChanges （）方法将更改记录到联系人。 最后，调用实体框架 SaveChanges （）方法将更改保存到基础数据库。

您可以通过右键单击 Edit （）方法并选择菜单选项 "添加视图" 来生成包含编辑窗体的视图。 在 "添加视图" 对话框中，选择 " **ContactManager** " 类和 "**编辑**" 视图内容（参见图19）。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)

**图 19**：添加编辑视图（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image38.png)）

单击 "添加" 按钮时，会自动生成一个新的编辑视图。 生成的 HTML 窗体包含与 Contact 类的每个属性对应的字段（请参阅列表7）。

**列表 7-Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>删除联系人

如果要删除联系人，则需要向 Home 控制器类添加两个 Delete （）操作。 第一个 Delete （）操作显示 "删除" 确认窗体。 第二个 Delete （）操作执行实际删除。

> [!NOTE] 
> 
> 稍后，在迭代 #7 中，我们将修改 Contact Manager，使其支持一个步骤 Ajax delete。

列表8中包含两个新的 Delete （）方法。

**列表 8-Controllers\HomeController.cs （删除方法）**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample8.cs)]

第一个 Delete （）方法返回一个确认窗体，以便从数据库中删除联系人记录（请参阅 Figure20）。 第二个 Delete （）方法对数据库执行实际的删除操作。 在从数据库中检索到原始联系人之后，将调用实体框架 DeleteObject （）和 SaveChanges （）方法来执行数据库删除。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)

**图 20**：删除确认视图（[单击查看完全大小的图像](iteration-1-create-the-application-cs/_static/image40.png)）

我们需要修改索引视图，使其包含用于删除联系人记录的链接（见图21）。 需要将以下代码添加到包含 "编辑" 链接的相同表格单元中：

Html.actionlink （{id = item）。Id}）%&gt;

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)

**图 21**：具有编辑链接的索引视图（[单击以查看完全大小的图像](iteration-1-create-the-application-cs/_static/image42.png)）

接下来，需要创建 "删除确认" 视图。 右键单击 Home 控制器类中的 Delete （）方法，然后选择菜单选项 "添加视图"。 此时将显示 "添加视图" 对话框（请参阅图22）。

与列表、创建和编辑视图不同，"添加视图" 对话框不包含用于创建删除视图的选项。 而是选择**ContactManager**数据类和**空**视图内容。 选择空的 "查看内容" 选项将要求我们自己创建视图。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)

**图 22**：添加 "删除确认" 视图（[单击查看完全尺寸的图像](iteration-1-create-the-application-cs/_static/image44.png)）

删除视图的内容包含在列表9中。 此视图包含一个窗体，该窗体确认是否应删除某个特定联系人（见图21）。

**列表 9-Views\Home\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>更改默认控制器的名称

这可能会让你困扰用于处理联系人的控制器类的名称，名称为 HomeController 类。 控制器不应命名为 ContactController？

此问题很容易解决。 首先，我们需要重构 Home 控制器的名称。 在 Visual Studio Code 编辑器中打开 "HomeController" 类，右键单击类的名称，然后选择 "**重构、重命名**" 菜单选项。 选择此菜单选项将打开 "重命名" 对话框。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)

**图 23**：重构控制器名称（[单击以查看完全大小的映像](iteration-1-create-the-application-cs/_static/image46.png)）

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)

**图 24**：使用 "重命名" 对话框（[单击查看完全大小的图像](iteration-1-create-the-application-cs/_static/image48.png)）

如果重命名控制器类，Visual Studio 也会更新 Views 文件夹中文件夹的名称。 Visual Studio 会将 \Views\Home 文件夹重命名为 \Views\Contact 文件夹。

做出此更改后，应用程序将不再具有主控制器。 运行应用程序时，会收到图25中的错误页。

[!["新建项目" 对话框](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)

**图 25**：无默认控制器（[单击以查看完全大小的映像](iteration-1-create-the-application-cs/_static/image50.png)）

我们需要更新 global.asax 文件中的默认路由，以使用联系人控制器而不是主控制器。 打开 global.asax 文件，修改默认路由使用的默认控制器（请参阅列表10）。

**列表 10-Global.asax.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample10.cs)]

进行这些更改后，联系人管理器将正常运行。 现在，它将使用 Contact controller 类作为默认控制器。

## <a name="summary"></a>摘要

在第一次迭代中，我们以尽可能快的方式创建了一个基本的联系人管理器应用程序。 我们充分利用了 Visual Studio 来自动生成控制器和视图的初始代码。 我们还充分利用了实体框架来自动生成数据库模型类。

目前，我们可以通过联系人管理器应用程序列出、创建、编辑和删除联系人记录。 换句话说，我们可以执行数据库驱动的 web 应用程序所需的所有基本数据库操作。

遗憾的是，我们的应用程序有一些问题。 首先，我想承认，联系人管理器应用程序并不是最具吸引力的应用程序。 它需要一些设计工作。 在下一次迭代中，我们将介绍如何更改默认视图母版页和级联样式表，以改善应用程序的外观。

其次，我们尚未实现任何窗体验证。 例如，无需为任何窗体字段输入值即可阻止你提交 "创建联系人" 窗体。 此外，还可以输入无效的电话号码和电子邮件地址。 我们开始在迭代 #3 中解决窗体验证问题。

最后，最重要的是，无法轻松修改或维护联系人管理器应用程序的当前迭代。 例如，数据库访问逻辑融入在控制器操作中。 这意味着，如果不修改控制器，就无法修改数据访问代码。 在后续迭代中，我们将探讨可实现的软件设计模式，以使联系人经理更具弹性的更改能力。

> [!div class="step-by-step"]
> [下一部分](iteration-2-make-the-application-look-nice-cs.md)
