---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 模型和数据访问 |Microsoft Docs
author: rick-anderson
description: 注意：此动手实验假设你具有 ASP.NET MVC 的基本知识。 如果你之前未使用过 ASP.NET MVC，则建议你遍历 ASP.NET MVC 4 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451466"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a>ASP.NET MVC 4 模型和数据访问

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

此动手实验假设你具有**ASP.NET MVC**的基本知识。 如果你之前未使用过**ASP.NET mvc** ，则建议你浏览**ASP.NET mvc 4 基础**动手实验。

此实验室通过应用对源文件夹中提供的示例 Web 应用程序的少量更改，指导你完成前面介绍的增强功能和新功能。

> [!NOTE]
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中，在[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)中提供。 [ASP.NET MVC 4 模型和数据访问](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)中提供了此实验室特定的项目。

在**ASP.NET MVC 基础**动手实验中，你已将硬编码的数据从控制器传递到视图模板。 但为了构建真实的 Web 应用程序，您可能希望使用实际的数据库。

此动手实验将向您演示如何使用数据库引擎来存储和检索音乐应用商店应用程序所需的数据。 为实现此目的，你将从现有数据库开始，并从其创建实体数据模型。 在此实验室中，您将满足**Database First**方法以及**Code First**方法。

但是，您还可以使用**Model First**方法，使用这些工具创建相同的模型，然后从该模型生成数据库。

![Database First 与 Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First 与 Model First")

*Database First 与 Model First*

生成模型后，您将在 StoreController 中进行适当调整，以便为商店视图提供从数据库获取的数据，而不是使用硬编码数据。 你不需要对视图模板进行任何更改，因为 StoreController 将返回与视图模板相同的 Viewmodel，但这次数据将来自数据库。

**Code First 方法**

利用 Code First 方法，我们可以从代码定义模型，而无需生成通常与框架耦合的类。

在 "代码优先" 中，模型对象是用 Poco 定义的，&quot;纯旧 CLR 对象&quot;。 Poco 是简单的无继承类，不实现接口。 我们可以从这些数据库中自动生成数据库，也可以使用现有数据库并从代码生成类映射。

使用此方法的好处是，模型与持久性框架（在本例中为实体框架）保持独立，因为 Poco 类不与映射框架耦合。

> [!NOTE]
> 此实验室基于 ASP.NET MVC 4 和自定义和最小化的音乐应用商店示例应用程序版本，以仅适应此动手实验中显示的功能。
> 
> 若要浏览整个**音乐商店**教程应用程序，可以在[MVC-音乐存储](https://github.com/evilDave/MVC-Music-Store)中找到它。

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

你必须具有以下项才能完成此实验室：

- 适用于 Web 或高级的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （阅读[附录 A](#AppendixA)以获取有关如何安装的说明）。

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安装

**安装代码片段**

为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。 若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi**文件。

如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录[C： &quot;附录 C：&quot;的代码段](#AppendixC)。

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

此动手实验包括以下练习：

1. [练习1：添加数据库](#Exercise1)
2. [练习2：使用 Code First 创建数据库](#Exercise2)
3. [练习3：用参数查询数据库](#Exercise3)

> [!NOTE]
> 每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。 如果需要更多帮助，请使用此解决方案作为指导。

完成本实验的估计时间： **35 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a>练习1：添加数据库

在此练习中，您将学习如何将包含 MusicStore 应用程序的表的数据库添加到解决方案，以便使用其数据。 使用模型生成数据库并将其添加到解决方案后，您将修改 StoreController 类，以便为视图模板提供从数据库中提取的数据，而不是使用硬编码值。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a>任务 1-添加数据库

在此任务中，您将使用 MusicStore 应用程序的主表将已创建的数据库添加到解决方案。

1. 打开位于**Source/Ex1-AddingADatabaseDBFirst/begin/** Folder 的**begin**解决方案。

   1. 在继续之前，需要下载一些缺少的 NuGet 包。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 添加**MvcMusicStore**数据库文件。 在此动手实验中，您将使用已创建的名为**MvcMusicStore**的数据库。 为此，请右键单击 "**应用\_Data** " 文件夹，指向 "**添加**"，然后单击 "**现有项**"。 浏览到 **\Source\Assets**并选择**MvcMusicStore**文件。

    ![添加现有项](aspnet-mvc-4-models-and-data-access/_static/image2.png "添加现有项")

    *添加现有项*

    ![MvcMusicStore .mdf 数据库文件](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore .mdf 数据库文件")

    *MvcMusicStore .mdf 数据库文件*

    数据库已添加到该项目中。 即使数据库位于解决方案内部，你也可以在该数据库托管在不同的数据库服务器中时对其进行查询和更新。

    ![解决方案资源管理器中的 MvcMusicStore 数据库](aspnet-mvc-4-models-and-data-access/_static/image4.png "解决方案资源管理器中的 MvcMusicStore 数据库")

    *解决方案资源管理器中的 MvcMusicStore 数据库*
3. 验证与数据库的连接。 为此，请双击 " **MvcMusicStore** " 以建立连接。

    ![连接到 MvcMusicStore](aspnet-mvc-4-models-and-data-access/_static/image5.png "连接到 MvcMusicStore")

    *连接到 MvcMusicStore*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a>任务 2-创建数据模型

在此任务中，您将创建一个数据模型，用于与在上一任务中添加的数据库进行交互。

1. 创建将表示数据库的数据模型。 为此，请在解决方案资源管理器右键单击 "**模型**" 文件夹，指向 "**添加**"，然后单击 "**新建项**"。 在 "**添加新项**" 对话框中，选择 "**数据**" 模板，然后选择 " **ADO.NET" 实体数据模型**项。 将数据模型名称更改为**StoreDB** ，然后单击 "**添加**"。

    ![添加 StoreDB ADO.NET 实体数据模型](aspnet-mvc-4-models-and-data-access/_static/image6.png "添加 StoreDB ADO.NET 实体数据模型")

    *添加 StoreDB ADO.NET 实体数据模型*
2. 将显示**实体数据模型向导**。 此向导将引导您完成模型层的创建。 由于应基于最近添加的现有数据库创建该模型，请选择 "**从数据库生成**"，然后单击 "**下一步**"。

    ![选择模型内容](aspnet-mvc-4-models-and-data-access/_static/image7.png "选择模型内容")

    *选择模型内容*
3. 由于您是从数据库生成模型，因此您需要指定要使用的连接。 单击 "**新建连接**"。
4. 选择 " **Microsoft SQL Server 数据库文件**"，然后单击 "**继续**"。

    ![选择数据源](aspnet-mvc-4-models-and-data-access/_static/image8.png "选择数据源")

    *"选择数据源" 对话框*
5. 单击 "**浏览**"，然后选择位于**应用\_Data** "文件夹中的数据库" **MvcMusicStore** "，然后单击 **" 确定 "** 。

    ![连接属性](aspnet-mvc-4-models-and-data-access/_static/image9.png "连接属性")

    *连接属性*
6. 生成的类应具有与实体连接字符串相同的名称，因此请将其名称更改为**MusicStoreEntities** ，然后单击 "**下一步**"。

    ![选择数据连接](aspnet-mvc-4-models-and-data-access/_static/image10.png "选择数据连接")

    *选择数据连接*
7. 选择要使用的数据库对象。 由于实体模型将只使用数据库的表，因此请选择 "**表**" 选项，并确保还选择了 "模型" 和 "复数形式"**或 "确定所生成的对象名称**" 选项中的 "**包含外键列**"。 将模型命名空间更改为**MvcMusicStore** ，然后单击 "**完成**"。

    ![选择数据库对象](aspnet-mvc-4-models-and-data-access/_static/image11.png "选择数据库对象")

    *选择数据库对象*

    > [!NOTE]
    > 如果显示 "安全警告" 对话框，则单击 **"确定"** 以运行模板并为模型实体生成类。
8. 将显示该数据库的实体关系图，同时会创建一个单独的类，将每个表映射到数据库。 例如，影集表将由一个**唱片集**类表示，其中，表**中的每**一列都将映射到类属性。 这将允许您查询和使用表示数据库中的行的对象。

    ![实体关系图](aspnet-mvc-4-models-and-data-access/_static/image12.png "实体关系图")

    *实体关系图*

    > [!NOTE]
    > T4 模板（tt）运行代码以生成实体类，并将覆盖具有相同名称的现有类。 在此示例中，将在生成的代码中覆盖 &quot;唱片集&quot;、&quot;流派&quot; 和 &quot;艺术家&quot; 的类。

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a>任务 3-生成应用程序

在此任务中，您将检查是否已通过模型生成删除了**唱片集**、**流派**和**艺术家**模型类，并通过使用新的数据模型类成功生成项目。

1. 通过选择 "**生成**" 菜单项生成项目，然后**生成 MvcMusicStore**。

    ![生成项目](aspnet-mvc-4-models-and-data-access/_static/image13.png "生成项目")

    *生成项目*
2. 项目成功生成。 为什么仍然起作用？ 它的工作方式是，数据库表中包含的字段包含你在删除的类**唱**集中使用的**属性。**

    ![生成成功](aspnet-mvc-4-models-and-data-access/_static/image14.png "生成成功")

    *生成成功*
3. 设计器以关系图格式显示实体时，它们是实际C#的类。 在解决方案资源管理器中展开 " **StoreDB** " 节点，然后展开 " **StoreDB.tt**"，将看到新生成的实体。

    ![生成的文件](aspnet-mvc-4-models-and-data-access/_static/image15.png "生成的文件")

    *生成的文件*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>任务 4-查询数据库

在此任务中，你将更新 StoreController 类，以便它将查询数据库以检索信息，而不是使用硬编码数据。

1. 打开**Controllers\StoreController.cs**并将以下字段添加到类，以保存名为**storeDB**的**MusicStoreEntities**类的实例：

    （代码段-*模型和数据访问-Ex1 storeDB*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. **MusicStoreEntities**类公开数据库中每个表的集合属性。 更新**浏览**操作方法以检索包含所有**唱片集**的流派。

    （代码段-*模型和数据访问-Ex1 Store Browse*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > 你使用的是 .NET 的一项功能，该功能称为**LINQ** （语言集成查询），用于针对这些集合编写强类型的查询表达式，这些表达式将对数据库执行代码，并返回可对其进行编程的对象。
    > 
    > 有关 LINQ 的详细信息，请访问[msdn 网站](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)。
3. 更新**索引**操作方法以检索所有流派。

    （代码段-*模型和数据访问-Ex1 存储索引*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. 更新**索引**操作方法以检索所有流派，并将集合转换为列表。

    （代码段-*模型和数据访问-Ex1 Store GenreMenu*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，您将检查 "商店索引" 页现在是否将显示存储在数据库中的流派，而不是硬编码的流派。 无需更改视图模板，因为**StoreController**返回与以前相同的实体，但这次数据将来自数据库。

1. 重新生成解决方案，然后按**F5**运行该应用程序。
2. 项目在主页中启动。 验证**流派**菜单不再是硬编码的列表，并且直接从数据库中检索数据。

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    *从数据库浏览流派*
3. 现在，浏览到任何流派，并验证是否已从数据库填充唱集。

    ![从数据库浏览唱片集](aspnet-mvc-4-models-and-data-access/_static/image17.png "从数据库浏览唱片集")

    *从数据库浏览唱片集*

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a>练习2：使用 Code First 创建数据库

在此练习中，您将学习如何使用 Code First 方法创建包含 MusicStore 应用程序表的数据库，以及如何访问其数据。

生成模型后，您将修改 StoreController 以向视图模板提供从数据库获取的数据，而不是使用硬编码值。

> [!NOTE]
> 如果你已完成练习1并已使用 Database First 方法，你现在将了解如何使用不同的进程获得相同的结果。 与练习1共用的任务已经过标记，便于阅读。 如果你还未完成练习1，但想要了解 Code First 方法，你可以从本练习开始，并全面了解该主题。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a>任务 1-填充示例数据

在此任务中，将使用 "代码优先" 最初创建的示例数据填充数据库。

1. 打开位于**Source/buildingappswithcachingservice-ex2-getproducts latency-cs-CreatingADatabaseCodeFirst/begin/** Folder 的**begin**解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 将**SampleData.cs**文件添加到 "**模型**" 文件夹。 为此，请右键单击 "**模型**" 文件夹，指向 "**添加**"，然后单击 "**现有项**"。 浏览到 **\Source\Assets**并选择 " **SampleData.cs** " 文件。

    ![示例数据填充代码](aspnet-mvc-4-models-and-data-access/_static/image18.png "示例数据填充代码")

    *示例数据填充代码*
3. 打开**Global.asax.cs**文件并添加以下*using*语句。

    （代码段-*模型和数据访问-Buildingappswithcachingservice-ex2-getproducts latency-cs Global Global.asax using*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. 在**应用程序\_Start （）** 方法中，添加以下行以设置数据库初始值设定项。

    （代码段-*模型和数据访问-Buildingappswithcachingservice-ex2-getproducts latency-cs Global Global.asax database.setinitializer*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a>任务 2-配置与数据库的连接

现在您已将数据库添加到项目中，您将在**web.config 文件中**写入连接字符串。

1. **在 web.config 中添加**一个连接字符串。为此，**请在项目根中打开 web.config** ，并将名为 DefaultConnection 的连接字符串替换 **&lt;connectionStrings&gt;** 部分中的以下行：

    ![Web.config 文件位置](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 文件位置")

    *Web.config 文件位置*

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a>任务 3-使用模型

现在您已经配置了与数据库的连接，接下来您将模型链接到数据库表。 在此任务中，您将创建一个将链接到具有 Code First 的数据库的类。 请记住，存在一个应修改的 POCO 模型类。

> [!NOTE]
> 如果已完成练习1，则会注意到此步骤是由向导执行的。 通过执行 Code First，您将手动创建将链接到数据实体的类。

1. 从**模型**项目文件夹中打开 POCO 模型类**流派**，并包括 ID。 使用名为**GenreId**的 int 属性。

    （代码段-*模型和数据访问-buildingappswithcachingservice-ex2-getproducts latency-cs Code First 流派*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > 若要使用 Code First 约定，类流派必须具有将自动检测的主键属性。
    > 
    > 有关详细信息，请参阅此[msdn 文章](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)中的 Code First 约定。
2. 现在，从 "**模型**" 项目文件夹中打开 POCO 模型类**唱片集**并包含外键，创建名称为 " **GenreId** " 和 " **ArtistId**" 的属性。 此类已具有主键的**GenreId** 。

    （代码段-*模型和数据访问-buildingappswithcachingservice-ex2-getproducts latency-cs Code First 唱片集*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. 打开 POCO 模型类**艺术家**，并包括**ArtistId**属性。

    （代码段-*模型和数据访问-buildingappswithcachingservice-ex2-getproducts latency-cs Code First 艺术家*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. 右键单击 "**模型**" 项目文件夹，然后选择 "**添加 |类**。 将该文件命名为**MusicStoreEntities.cs**。 然后单击 "**添加"。**

    ![添加类](aspnet-mvc-4-models-and-data-access/_static/image20.png "添加类")

    *添加新项*

    ![添加 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "添加 class2")

    *添加类*
5. 打开刚刚创建的类（ **MusicStoreEntities.cs**），并包括命名空间**system.web**和**system.web. entity**。

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. 将类声明替换为扩展**DbContext**类：声明公共**DBSet**并重写**OnModelCreating**方法。 完成此步骤后，您将获得一个域类，该类将使用实体框架链接您的模型。 为此，请将类代码替换为以下代码：

    （代码段-*模型和数据访问-buildingappswithcachingservice-ex2-getproducts latency-cs Code First MusicStoreEntities*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> 通过实体框架**DbContext**和**DBSet** ，你将能够查询 POCO 类流派。 通过扩展**OnModelCreating**方法，您可以在**代码**中指定如何将流派映射到数据库表。 有关 DBContext 和 DBSet 的详细信息，请查看此 msdn 文章：[链接](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>任务 4-查询数据库

在此任务中，您将更新 StoreController 类，以便不使用硬编码的数据，而是从数据库中检索数据。

> [!NOTE]
> 此任务在练习1中很常见。
> 
> 如果已完成练习1，你会注意到这两个方法（数据库优先或代码优先）中的步骤相同。 它们在数据与模型的链接方式上有所不同，但对数据实体的访问权限对于控制器却是透明的。

1. 打开**Controllers\StoreController.cs**并将以下字段添加到类，以保存名为**storeDB**的**MusicStoreEntities**类的实例：

    （代码段-*模型和数据访问-Ex1 storeDB*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. **MusicStoreEntities**类公开数据库中每个表的集合属性。 更新**浏览**操作方法以检索包含所有**唱片集**的流派。

    （代码段-*模型和数据访问-Buildingappswithcachingservice-ex2-getproducts latency-cs Store Browse*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > 你使用的是 .NET 的一项功能，该功能称为**LINQ** （语言集成查询），用于针对这些集合编写强类型的查询表达式，这些表达式将对数据库执行代码，并返回可对其进行编程的对象。
    > 
    > 有关 LINQ 的详细信息，请访问[msdn 网站](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)。
3. 更新**索引**操作方法以检索所有流派。

    （代码段-*模型和数据访问-Buildingappswithcachingservice-ex2-getproducts latency-cs 存储索引*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. 更新**索引**操作方法以检索所有流派，并将集合转换为列表。

    （代码段-*模型和数据访问-Buildingappswithcachingservice-ex2-getproducts latency-cs Store GenreMenu*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，您将检查 "商店索引" 页现在是否将显示存储在数据库中的流派，而不是硬编码的流派。 无需更改视图模板，因为**StoreController**返回与以前相同的**StoreIndexViewModel** ，但这一次数据将来自数据库。

1. 重新生成解决方案，然后按**F5**运行该应用程序。
2. 项目在主页中启动。 验证**流派**菜单不再是硬编码的列表，并且直接从数据库中检索数据。

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    *从数据库浏览流派*
3. 现在，浏览到任何流派，并验证是否已从数据库填充唱集。

    ![从数据库浏览唱片集](aspnet-mvc-4-models-and-data-access/_static/image23.png "从数据库浏览唱片集")

    *从数据库浏览唱片集*

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a>练习3：用参数查询数据库

在此练习中，您将学习如何使用参数查询数据库，以及如何使用查询结果造型，这是一项可减少数据库访问以更高效方式检索数据的功能。

> [!NOTE]
> 有关查询结果造型的详细信息，请访问以下[msdn 文章](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a>任务 1-修改 StoreController 以从数据库中检索唱片集

在此任务中，你将更改**StoreController**类，以访问数据库以从特定的流派检索唱集。

1. 如果要使用 Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin**文件夹，** 如果要使用数据库优先方法，请打开位于 " " 文件夹中的 "**开始**" 解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 打开**StoreController**类以更改**浏览**操作方法。 为此，请在 "**解决方案资源管理器**中，展开"**控制器**"文件夹，然后双击" **StoreController.cs**"。
3. 更改**浏览**操作方法以检索特定流派的唱集。 为此，请替换以下代码：

    （代码段-*模型和数据访问-Section-cs StoreController BrowseMethod*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> 若要填充实体的集合，需要使用**Include**方法来指定是否也要检索唱片集。 您可以使用。LINQ 中的**Single （）** 扩展，因为在这种情况下，影集仅应有一个流派。 **Single （）** 方法采用 Lambda 表达式作为参数，这种情况下，该方法指定单个流派对象，使其名称与定义的值匹配。
> 
> 您将利用一项功能，该功能允许您在检索流派对象时指示要加载的其他相关实体。 此功能称为**查询结果整形**，可用于减少访问数据库以检索信息所需的次数。 在这种情况下，你将需要为检索的流派预先提取相册。
> 
> 查询包括**流派。包括（&quot;唱集&quot;）** 以指示还需要相关唱片集。 这将导致应用程序的效率更高，因为它将在单个数据库请求中检索流派和唱片集数据。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>任务 2-运行应用程序

在此任务中，您将运行应用程序，并从数据库中检索特定流派的唱片集。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 **/Store/Browse？流派 = Pop**以验证是否正在从数据库中检索结果。

    ![按流派浏览](aspnet-mvc-4-models-and-data-access/_static/image24.png "按流派浏览")

    *浏览/Store/Browse？流派 = Pop*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a>任务 3-按 Id 访问唱片集

在此任务中，您将重复前面的过程，按其 Id 获取唱片集。

1. 如果需要，请关闭浏览器以返回到 Visual Studio。 打开**StoreController**类，以更改**详细信息**操作方法。 为此，请在 "**解决方案资源管理器**中，展开"**控制器**"文件夹，然后双击" **StoreController.cs**"。
2. 更改**详细信息**操作方法，以根据其**Id**检索唱片集的详细信息。为此，请替换以下代码：

    （代码段-*模型和数据访问-Section-cs StoreController DetailsMethod*）

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在此任务中，将在 web 浏览器中运行应用程序，并按其 Id 获取唱片集详细信息。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 **/Store/Details/51**或浏览流派，并选择一个唱片集来验证是否正在从数据库中检索结果。

    ![浏览详细信息](aspnet-mvc-4-models-and-data-access/_static/image25.png "浏览详细信息")

    *浏览/Store/Details/51*

> [!NOTE]
> 此外，还可以在[附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序的](#AppendixB)Microsoft Azure 网站上部署此应用程序。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>摘要

完成此动手实验后，你已经了解了使用**Database First**方法以及**Code First**方法的 ASP.NET MVC 模型和数据访问的基础：

- 如何将数据库添加到解决方案以便使用其数据
- 如何更新控制器以向视图模板提供从数据库获取的数据而不是硬编码的数据
- 如何使用参数查询数据库
- 如何使用查询结果造型，这种功能可减少数据库访问的数量，以更有效的方式检索数据
- 如何使用 Microsoft 实体框架中的 Database First 和 Code First 方法将数据库与模型链接

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 A：安装 Visual Studio Express 2012 for Web

您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。 以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。

1. 请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序

本附录将演示如何从 Windows Azure 管理门户创建新的网站，以及如何利用 Microsoft Azure 提供的 Web 部署发布功能，发布通过实验室获取的应用程序。

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>任务 1-从 Microsoft Azure 门户创建新网站

1. 请使用[Windows Azure 管理门户](https://manage.windowsazure.com/)，并使用与你的订阅关联的 Microsoft 凭据登录。

    > [!NOTE]
    > 借助 Windows Azure，你可以免费托管10个 ASP.NET 的网站，然后随着流量的增长进行扩展。 你可以在[此处](https://aka.ms/aspnet-hol-azure)注册。

    ![登录到 Windows Azure 门户](aspnet-mvc-4-models-and-data-access/_static/image31.png "登录到 Microsoft Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击命令栏上的 "**新建**"。

    ![创建新网站](aspnet-mvc-4-models-and-data-access/_static/image32.png "创建新网站")

    *创建新网站*
3. 单击 "**计算** | **网站**"。 然后选择 "**快速创建**" 选项。 为新网站提供可用 URL，并单击 "**创建**网站"。

    > [!NOTE]
    > Windows Azure 网站是在云中运行的 Web 应用程序的宿主，你可以控制和管理这些应用程序。 使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Microsoft Azure 网站。 它不包括设置数据库的步骤。

    ![使用 "快速创建" 创建新网站](aspnet-mvc-4-models-and-data-access/_static/image33.png "使用“快速创建”创建新网站")

    *使用 "快速创建" 创建新网站*
4. 请**等到新网站创建完毕。**
5. 创建网站后，单击 " **URL** " 列下的链接。 检查新网站是否正常工作。

    ![浏览到新网站](aspnet-mvc-4-models-and-data-access/_static/image34.png "浏览到新网站")

    *浏览到新网站*

    ![网站正在运行](aspnet-mvc-4-models-and-data-access/_static/image35.png "网站正在运行")

    *网站正在运行*
6. 返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。

    ![打开网站管理页](aspnet-mvc-4-models-and-data-access/_static/image36.png "打开网站管理页")

    *打开网站管理页*
7. 在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。

    > [!NOTE]
    > *发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 microsoft Azure 网站所需的所有信息。 发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 microsoft Azure 网站。

    ![下载网站发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image37.png "下载网站发布配置文件")

    *下载网站发布配置文件*
8. 将发布配置文件下载到已知位置。 在本练习中，您将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Microsoft Azure 网站。

    ![正在保存发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image38.png "正在保存发布配置文件")

    *正在保存发布配置文件*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。 如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。

1. 你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。 可以在 Microsoft Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 MICROSOFT Azure 管理门户中查看 sql 数据库服务器。 如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。 记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。 请不要创建数据库，因为它将在后面的阶段创建。

    ![SQL 数据库服务器仪表板](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL 数据库服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。 为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 中选择 IP 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框，然后单击 "![添加-客户端-IP 地址-](aspnet-mvc-4-models-and-data-access/_static/image40.png)" 按钮。

    ![添加客户端 IP 地址](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    *添加客户端 IP 地址*
3. 将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。

    ![确认更改](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    *确认更改*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序

1. 返回到 ASP.NET MVC 4 解决方案。 在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。

    ![发布应用程序](aspnet-mvc-4-models-and-data-access/_static/image43.png "发布应用程序")

    *发布网站*
2. 导入您在第一个任务中保存的发布配置文件。

    ![导入发布配置文件](aspnet-mvc-4-models-and-data-access/_static/image44.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击 "**验证连接**"。 验证完成后，单击 "**下一步**"。

    > [!NOTE]
    > 验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。

    ![正在验证连接](aspnet-mvc-4-models-and-data-access/_static/image45.png "正在验证连接")

    *正在验证连接*
4. 在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。

    ![Web 部署配置](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web 部署配置")

    *Web 部署配置*
5. 按如下所示配置数据库连接：

   - 在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。
   - 在 "**用户名**" 中键入服务器管理员登录名。
   - 在 "**密码**" 中键入服务器管理员登录密码。
   - 键入新的数据库名称。

     ![正在配置目标连接字符串](aspnet-mvc-4-models-and-data-access/_static/image47.png "正在配置目标连接字符串")

     *正在配置目标连接字符串*
6. 然后单击 **“确定”** 。 系统提示创建数据库时，单击 **"是"** 。

    ![创建数据库](aspnet-mvc-4-models-and-data-access/_static/image48.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。 再单击 **“下一步”** 。

    ![指向 SQL 数据库的连接字符串](aspnet-mvc-4-models-and-data-access/_static/image49.png "指向 SQL 数据库的连接字符串")

    *指向 SQL 数据库的连接字符串*
8. 在 "**预览**" 页上，单击 "**发布**"。

    ![发布 web 应用程序](aspnet-mvc-4-models-and-data-access/_static/image50.png "发布 web 应用程序")

    *发布 web 应用程序*
9. 发布过程完成后，您的默认浏览器将打开已发布的网站。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附录 C：使用代码片段

使用代码片段，您可以随时获得所需的全部代码。 实验室文档将告诉你何时可以使用它们，如下图所示。

![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-models-and-data-access/_static/image51.png "使用 Visual Studio code 代码段将代码插入到项目中")

*使用 Visual Studio code 代码段将代码插入到项目中*

***使用键盘添加代码片段（C#仅限）***

1. 将光标放在要插入代码的位置。
2. 开始键入代码片段名称（不含空格或连字符）。
3. 请注意，IntelliSense 显示匹配的代码段名称。
4. 选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。
5. 按 Tab 键两次，将代码段插入到光标位置。

![开始键入代码片段名称](aspnet-mvc-4-models-and-data-access/_static/image52.png "开始键入代码片段名称")

*开始键入代码片段名称*

![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-models-and-data-access/_static/image53.png "按 Tab 键以选择突出显示的代码段")

*按 Tab 键以选择突出显示的代码段*

![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-models-and-data-access/_static/image54.png "再次按 Tab 键，代码片段将展开")

*再次按 Tab 键，代码片段将展开*

***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2. 右键单击要插入代码片段的位置。

1. 选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。
2. 通过单击从列表中选择相关的代码片段。

![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-models-and-data-access/_static/image55.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")

*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*

![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-models-and-data-access/_static/image56.png "通过单击从列表中选择相关的代码片段")

*通过单击从列表中选择相关的代码片段*
