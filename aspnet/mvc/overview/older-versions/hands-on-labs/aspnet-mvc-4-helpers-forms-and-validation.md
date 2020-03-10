---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 帮助程序，窗体和验证 |Microsoft Docs
author: rick-anderson
description: 在 ASP.NET MVC 4 模型和数据访问动手实验中，你已从数据库加载并显示数据。 在此动手实验中，您将添加到 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433790"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a>ASP.NET MVC 4 帮助程序、窗体和验证

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

在**ASP.NET MVC 4 模型和数据访问**动手实验中，你已从数据库加载并显示数据。 在此动手实验中，你将向**音乐应用商店**应用程序添加编辑该数据的功能。

考虑到这一目标，您将首先创建一个支持创建、读取、更新和删除（CRUD）影集操作的控制器。 你将生成一个索引视图模板，该模板利用 ASP.NET MVC 的基架功能在 HTML 表中显示唱片集的属性。 若要增强该视图，您将添加一个将截断详细说明的自定义 HTML 帮助程序。

之后，您将添加 "编辑" 和 "创建" 视图，以使您能够在数据库中更改影集，并提供类似于下拉列表的窗体元素的帮助。

最后，您将允许用户删除唱片集，同时还会通过验证其输入来阻止他们输入错误的数据。

此动手实验假设你具有**ASP.NET MVC**的基本知识。 如果你之前未使用过**ASP.NET mvc** ，则建议使用**ASP.NET Mvc 基础**动手实验。

此实验室通过应用对源文件夹中提供的示例 Web 应用程序的少量更改，指导你完成前面介绍的增强功能和新功能。

> [!NOTE]
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中，在[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)中提供。 [ASP.NET MVC 4 帮助程序、窗体和验证中](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)提供了此实验室特定的项目。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在此动手实验中，您将学习如何：

- 创建控制器以支持 CRUD 操作
- 生成索引视图以显示 HTML 表中的实体属性
- 添加自定义 HTML 帮助程序
- 创建和自定义编辑视图
- 区分对 HTTP GET 或 HTTP POST 调用做出反应的操作方法
- 添加和自定义创建视图
- 处理实体的删除
- 验证用户输入

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

如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本 &quot;文档中的附录[：附录 B：使用代码片段](#AppendixB)&quot;。

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

以下练习构成了此动手实验：

1. [创建存储管理器控制器及其索引视图](#Exercise1)
2. [添加 HTML 帮助器](#Exercise2)
3. [创建编辑视图](#Exercise3)
4. [添加创建视图](#Exercise4)
5. [处理删除](#Exercise5)
6. [添加验证](#Exercise6)
7. [在客户端使用非引人注目 jQuery](#Exercise7)

> [!NOTE]
> 每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。 如果需要更多帮助，请使用此解决方案作为指导。

完成本实验的估计时间： **60 分钟**

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a>练习1：创建存储管理器控制器及其索引视图

在此练习中，您将学习如何创建新的控制器以支持 CRUD 操作，自定义其索引操作方法，以从数据库中返回影集列表，并最终生成一个利用 ASP.NET MVC 基架的索引视图模板。用于在 HTML 表中显示影集属性的功能。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a>任务 1-创建 StoreManagerController

在此任务中，你将创建一个名为**StoreManagerController**的新控制器以支持 CRUD 操作。

1. 打开位于**Source/Ex1-CreatingTheStoreManagerController/begin/** Folder 的**begin**解决方案。

   1. 在继续之前，需要下载一些缺少的 NuGet 包。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 添加新控制器。 为此，请在解决方案资源管理器中右键单击 "**控制器**" 文件夹，选择 "**添加**"，然后选择 "**控制器**" 命令。 将**控制器** **名称**更改为**StoreManagerController** ，并确保选中选项 "**带有空读/写操作的 MVC 控制器**"。 单击 **“添加”** 。

    !["添加控制器" 对话框](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "“添加控制器”对话框")

    *"添加控制器" 对话框*

    生成新的控制器类。 由于你指示添加对读/写操作的操作，因此，将在其中填充了 TODO 注释来创建常见的 CRUD 操作，并提示包含应用程序特定的逻辑。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a>任务 2-自定义 StoreManager 索引

在此任务中，您将自定义 StoreManager Index 操作方法，以从数据库中返回包含唱片集列表的视图。

1. 在 StoreManagerController 类中，添加以下*using*指令。

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-使用 MvcMusicStore 的 Ex1*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. 向**StoreManagerController**添加一个字段，用于保存 MusicStoreEntities 的实例 **。**

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex1 MusicStoreEntities*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. 实现 StoreManagerController 索引操作，以返回包含唱片集列表的视图。

    控制器操作逻辑与之前编写的 StoreController 索引操作非常相似。 使用 LINQ 检索所有相册，包括要显示的流派和艺术家信息。

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex1 StoreManagerController Index*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a>任务 3-创建索引视图

在此任务中，您将创建索引视图模板以显示由**StoreManager**控制器返回的唱片集列表。

1. 在创建新的视图模板之前，您应该生成项目，以便 "**添加视图" 对话框**知道要使用的**唱片集**类。 选择**生成 |生成 MvcMusicStore**以生成项目。
2. 在**索引**操作方法中右键单击，然后选择 "**添加视图**"。 此时将显示 "**添加视图**" 对话框。

    ![添加视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "添加视图")

    *从 Index 方法中添加视图*
3. 在 "添加视图" 对话框中，验证视图名称是否为 "**索引**"。 选择 "**创建强类型视图**" 选项，然后从 "**模型类**" 下拉选项中选择 "**唱片集（MvcMusicStore）** "。 从 "**基架模板**" 下拉列表中选择 "**列表**"。 将**视图引擎**保留为**Razor** ，将其他字段保留其默认值，然后单击 "**添加**"。

    ![添加索引视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "添加索引视图")

    *添加索引视图*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a>任务 4-自定义索引视图的基架

在此任务中，您将调整使用 ASP.NET MVC 基架功能创建的简单视图模板，使其显示所需的字段。

> [!NOTE]
> ASP.NET MVC 内的**基架**支持会生成一个简单的视图模板，其中列出了唱片集模型中的所有字段。 **基架**提供了开始强类型化视图的快速方法：不必手动编写视图模板，基架会快速生成默认模板，然后可以修改生成的代码。

1. 查看创建的代码。 生成的字段列表将是**基架**用于显示表格格式数据的以下 HTML 表的一部分。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. 将 **&lt;表**替换为以下代码&gt;代码，以便仅显示**流派**、**艺术家**、**唱片集标题**和**价格**字段。 这将删除**AlbumId**和**唱片集画面 URL**列。 此外，它会更改 GenreId 和 ArtistId 列，使其显示**Artist.Name**和**Genre.Name**的链接类属性，并删除**详细信息**链接。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. 更改以下说明。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，您将测试 " **StoreManager** **索引**" 视图模板是否根据前面步骤的设计显示唱片集列表。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 " **/StoreManager** " 以验证是否显示影集列表，并显示其**标题**、**艺术家**和**流派**。

    ![浏览唱片集列表](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "浏览唱片集列表")

    *浏览唱片集列表*

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a>练习2：添加 HTML 帮助器

"StoreManager 索引" 页有一个潜在的问题： "标题" 和 "艺术家名称" 属性的长度可以足以引发表格式设置。 在本练习中，您将学习如何添加自定义 HTML 帮助程序来截断该文本。

在下图中，可以看到，在使用较小浏览器大小时，如何修改格式，因为文本长度太长。

![浏览没有截断文本的唱片集列表](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "浏览没有截断文本的唱片集列表")

*浏览没有截断文本的唱片集列表*

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a>任务 1-扩展 HTML 帮助器

在此任务中，您将添加一个新方法，该方法将**截断**到在 ASP.NET MVC 视图中公开的**HTML**对象。 要执行此操作，需要为 ASP.NET MVC 提供的内置**HtmlHelper**类实现**扩展方法**。

> [!NOTE]
> 若要了解有关**扩展方法**的详细信息，请访问此 msdn 文章。 [https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx)。

1. 打开位于**Source/buildingappswithcachingservice-ex2-getproducts latency-cs-AddingAnHTMLHelper/begin/** Folder 的**begin**解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 打开 StoreManager 的 "索引" 视图。 为此，请在 "解决方案资源管理器展开" **Views** "文件夹，然后打开" **StoreManager** "**文件。**
3. 在<strong>@model</strong>指令下面添加以下代码，以定义<strong>截断</strong>helper 方法。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a>任务 2-截断页面中的文本

在此任务中，您将使用**截断**方法来截断视图模板中的文本。

1. 打开 StoreManager 的 "索引" 视图。 为此，请在 "解决方案资源管理器展开" **Views** "文件夹，然后打开" **StoreManager** "**文件。**
2. 替换显示**艺术家名称**和唱片集**标题**的行。 为此，请替换以下行。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，你将测试**StoreManager** **索引**视图模板是否截断了唱片集的标题和名称。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 " **/StoreManager** " 以验证 "**标题**" 和 "**艺术家**" 列中的长文本是否已截断。

    ![截断的标题和艺术家名称](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "截断的标题和艺术家名称")

    *截断的标题和艺术家姓名*

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a>练习3：创建编辑视图

在此练习中，您将学习如何创建窗体，以允许商店经理编辑唱片集。 他们将浏览 **/StoreManager/Edit/id** URL （**id**是要编辑的唱片集的唯一 id），从而对服务器发出 HTTP GET 调用。

控制器编辑操作方法将从数据库中检索相应的唱片集，创建**StoreManagerViewModel**对象以封装它（连同艺术家和流派的列表），然后将其传递给视图模板，以将 HTML 页面呈现给用户。 此页将包含一个 **&lt;窗体&gt;** 元素，其中包含用于编辑唱片集属性的文本框和下拉列表。

用户更新唱片集格式值并单击 "**保存**" 按钮后，将通过 HTTP POST 调用将更改提交回 **/StoreManager/Edit/id**。尽管 URL 与上一次调用中的内容相同，但 ASP.NET MVC 标识这是一个 HTTP POST，因此执行其他编辑操作方法（一个修饰使用 **[HttpPost]** ）。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a>任务 1-实现 HTTP-获取编辑操作方法

在此任务中，您将实现 "编辑操作" 方法的 HTTP 获取版本以从数据库中检索相应的唱片集，以及所有流派和艺术家的列表。 它会将此数据打包到上一步骤中定义的**StoreManagerViewModel**对象中，然后将该对象传递给视图模板以呈现响应。

1. 打开位于**Source/section-cs-CreatingTheEditView/begin/** Folder 的**begin**解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 打开**StoreManagerController**类。 为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。
3. 将**HTTP-GET 编辑**操作方法替换为以下代码，以检索相应的**唱片集**以及**流派**和**艺术家**列表。

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Section-cs STOREMANAGERCONTROLLER HTTP-获取编辑操作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > 正在为艺术家和**流派使用** **SelectList** ，而不是对**system.object**列表使用。
    > 
    > **SelectList**是一种用于填充 HTML 下拉列表并管理当前所选内容的更干净的方式。 实例化并稍后在控制器操作中设置这些 ViewModel 对象将使编辑窗体方案更整洁。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a>任务 2-创建编辑视图

在此任务中，您将创建一个稍后将显示唱片集属性的编辑视图模板。

1. 创建 "编辑" 视图。 为此，请在**编辑**操作方法内右键单击，然后选择 "**添加视图**"。
2. 在 "添加视图" 对话框中，验证视图名称是否为 "**编辑**"。 选中 "**创建强类型视图**" 复选框，然后从 "**查看数据类**" 下拉框中选择 "**唱片集（MvcMusicStore）** "。 从 "**基架模板**" 下拉选择 "**编辑**"。 让其他字段保留其默认值，然后单击 "**添加**"。

    ![添加编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "添加编辑视图")

    *添加编辑视图*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，您将测试**StoreManager**的 "**编辑**视图" 页是否显示作为参数传递的唱片集的属性值。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 " **/StoreManager/Edit/1** " 以验证是否显示了所传递的唱片集的属性值。

    ![浏览唱片集的编辑视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "浏览唱片集的编辑视图")

    *浏览唱片集的编辑视图*

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a>任务 4-在唱片集编辑器模板上实现下拉

在此任务中，您将向在上一个任务中创建的视图模板添加下拉列表，以便用户可以从艺术家和流派列表中进行选择。

1. 将所有**唱**集字段代码替换为以下代码：

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > 已将**DropDownList** helper 添加到用于选择艺术家和流派的渲染下拉。 传递给**DropDownList**的参数是：
    > 
    > 1. 窗体字段的名称（ **&quot;ArtistId&quot;** ）。
    > 2. 下拉的值的**SelectList** 。

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，您将测试**StoreManager**的 "**编辑**视图" 页是否显示下拉下拉标识符而不是艺术家和流派 ID 文本字段。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 " **/StoreManager/Edit/1** " 以验证它是否显示下拉项，而不是 "艺术家" 和 "流派 ID" 文本字段。

    ![浏览唱片集的编辑视图和下拉](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "浏览唱片集的编辑视图和下拉")

    *浏览唱片集的编辑视图，这一次带 dropdown*

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a>任务 6-实现 HTTP POST 编辑操作方法

编辑视图按预期显示后，需要实现 HTTP POST 编辑操作方法以保存对唱片集所做的更改。

1. 如果需要，请关闭浏览器以返回到 Visual Studio 窗口。 从 "**控制器**" 文件夹中打开**StoreManagerController** 。
2. 将**HTTP-POST 编辑**操作方法代码替换为以下代码（请注意，必须替换的方法是接收两个参数的重载版本）：

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Section-cs STOREMANAGERCONTROLLER HTTP-POST 编辑操作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > 此方法将在用户单击视图的 "**保存**" 按钮时执行，并将窗体值的 HTTP POST 返回给服务器，以将其保留在数据库中。 修饰器 **[HttpPost]** 指示该方法应该用于这些 HTTP POST 方案。 方法使用**唱片集**对象。 ASP.NET MVC 将自动从发布 &lt;窗体&gt; 值创建唱片集对象。
    > 
    > 方法将执行以下步骤：
    > 
    > 1. 如果模型有效：
    > 
    >     1. 更新上下文中的 "唱片集" 条目，以将其标记为已修改对象。
    >     2. 保存更改并重定向到索引视图。
    > 2. 如果该模型无效，它将用**GenreId**和**ArtistId**填充 ViewBag，然后它将返回包含已接收唱片集对象的视图，以允许用户执行任何所需的更新。

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>任务 7-运行应用程序

在此任务中，您将测试 StoreManager 的 "**编辑**视图" 页是否确实将更新后的唱片集数据保存到数据库中。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 **/StoreManager/Edit/1**。 更改要**加载**的唱片集标题，并单击 "**保存**"。 验证影集列表中的唱片集标题是否实际已更改。

    ![更新唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "更新唱片集")

    *更新唱片集*

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a>练习4：添加 "创建" 视图

既然**StoreManagerController**支持**编辑**功能，在此练习中，您将学习如何添加 "创建视图" 模板，以允许商店管理器向应用程序中添加新的唱片集。

与编辑功能一样，你将在**StoreManagerController**类中使用两个不同的方法来实现 Create 方案：

1. 当存储经理首次访问 **/StoreManager/Create** URL 时，一个操作方法将显示一个空窗体。
2. 第二个操作方法将处理方案，其中存储管理器在窗体中单击 "**保存**" 按钮，然后将值作为 HTTP POST 提交回 **/StoreManager/Create** URL。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a>任务 1-实现 HTTP 获取创建操作方法

在此任务中，您将实现 "创建操作" 方法的 HTTP GET 版本来检索所有流派和音乐家的列表，将此数据打包到**StoreManagerViewModel**对象，然后将该对象传递给视图模板。

1. 打开位于**Source/Ex4-AddingACreateView/begin/** Folder 的**begin**解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 打开**StoreManagerController**类。 为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。
3. 将**创建**操作方法代码替换为以下代码：

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex4 STOREMANAGERCONTROLLER HTTP-GET Create action*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a>任务 2-添加 "创建" 视图

在此任务中，您将添加 "创建视图" 模板，该模板将显示新的（空）唱集窗体。

1. 在**创建**操作方法中右键单击，然后选择 "**添加视图**"。 此时将显示 "添加视图" 对话框。
2. 在 "添加视图" 对话框中，验证视图名称是否为 "**创建**"。 选择 "**创建强类型视图**" 选项，然后从 "**模型类**" 下拉项中选择 "**唱片集（MvcMusicStore）** "，**并从 "** **基架模板**" 下拉。 让其他字段保留其默认值，然后单击 "**添加**"。

    ![添加创建视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view .png")

    *添加 "创建" 视图*
3. 更新 " **GenreId** " 和 " **ArtistId** " 字段，以使用如下所示的下拉列表：

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，您将测试**StoreManager** **创建**视图页是否显示空的唱片集窗体。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 **/StoreManager/Create**。 验证是否显示了一个空窗体，用于填充新的唱片集属性。

    ![使用空窗体创建视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "使用空窗体创建视图")

    *使用空窗体创建视图*

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a>任务 4-实现 HTTP POST 创建操作方法

在此任务中，你将实现创建操作方法的 HTTP POST 版本，该方法将在用户单击 "**保存**" 按钮时调用。 方法应将新的唱片集保存到数据库中。

1. 如果需要，请关闭浏览器以返回到 Visual Studio 窗口。 打开**StoreManagerController**类。 为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。
2. 将**HTTP POST 创建**操作方法代码替换为以下代码：

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex4 STOREMANAGERCONTROLLER HTTP-POST 创建操作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > "创建" 操作非常类似于上一编辑操作方法，而是将对象添加到上下文中，而不是将其设置为 "已修改"。

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，您将测试**StoreManager 创建**视图页是否允许您创建一个新的唱片集，然后重定向到 StoreManager 索引视图。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 **/StoreManager/Create**。 使用新唱片集的数据填充所有窗体字段，如下图所示：

    ![创建唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "创建唱片集")

    *创建唱片集*
3. 验证是否已重定向到包含刚刚创建的新唱片集的 StoreManager 索引视图。

    ![已创建新唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "已创建新唱片集")

    *已创建新唱片集*

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a>练习5：处理删除

尚未实现删除唱片集的功能。 本练习将介绍这一点。 与之前一样，你将使用**StoreManagerController**类中的两个单独方法实现删除方案：

1. 一个操作方法将显示确认窗体
2. 第二个操作方法将处理窗体提交

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a>任务 1-实现 HTTP-GET Delete 操作方法

在此任务中，您将实现 "删除操作" 方法的 HTTP 获取版本以检索唱片集的信息。

1. 打开位于**Source/Ex5-HandlingDeletion/begin/** Folder 的**begin**解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 打开**StoreManagerController**类。 为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。
3. 删除控制器操作与上一存储详细信息控制器操作完全相同：它使用 URL 中提供的**id**从数据库中查询**唱片集**对象，并返回相应的**视图**。 为此，请将 HTTP-GET**删除**操作方法代码替换为以下代码：

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex5 处理删除 HTTP-GET 删除操作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. 右键单击 "**删除**" 操作方法，然后选择 "**添加视图**"。 此时将显示 "添加视图" 对话框。
5. 在 "添加视图" 对话框中，验证视图名称是否为 "**删除**"。 选择 "**创建强类型视图**" 选项，然后从 "**模型类**" 下拉选项中选择 "**唱片集（MvcMusicStore）** "。 从 "基架"**模板**下拉选择 "**删除**"。 让其他字段保留其默认值，然后单击 "**添加**"。

    ![添加删除视图](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "添加删除视图")

    *添加删除视图*
6. "删除" 模板显示模型中的所有字段。 您将只显示唱片集的标题。 为此，请将视图的内容替换为以下代码：

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>任务 2-运行应用程序

在此任务中，您将测试**StoreManager** **删除**视图页是否显示确认删除窗体。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 **/StoreManager**。 单击 "**删除**" 以选择要删除的一个唱片集，并验证新视图是否已上传。

    ![删除唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "删除唱片集")

    *删除唱片集*

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a>任务 3-实现 HTTP POST 删除操作方法

在此任务中，您将实现删除操作方法的 HTTP POST 版本，当用户单击 "**删除**" 按钮时，将调用该方法。 方法应删除数据库中的唱片集。

1. 如果需要，请关闭浏览器以返回到 Visual Studio 窗口。 打开**StoreManagerController**类。 为此，请展开 "**控制器**" 文件夹并双击 " **StoreManagerController.cs**"。
2. 将**HTTP POST 删除**操作方法代码替换为以下代码：

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex5 处理删除 HTTP-POST 删除操作*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在此任务中，您将测试 StoreManager 的 "**删除**视图" 页是否允许您删除唱片集，然后重定向到 StoreManager 索引视图。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 **/StoreManager**。 单击 "删除"，选择要删除的一个唱片集 **。** 单击 "**删除**" 按钮确认删除：

    ![删除唱片集](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "删除唱片集")

    *删除唱片集*
3. 验证是否已删除该唱片集，因为它未出现在 "**索引**" 页中。

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a>练习6：添加验证

目前，所用的创建和编辑表单不执行任何类型的验证。 如果用户将必填字段留空，或在 "价格" 字段中键入字母，则将从数据库中获取第一个错误。

可以通过将数据批注添加到模型类来向应用程序添加验证。 数据批注允许描述要应用于模型属性的规则，ASP.NET MVC 将负责强制执行并向用户显示相应的消息。

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a>任务 1-添加数据批注

在此任务中，您将向唱片集添加数据批注，使 "创建" 和 "编辑" 页在适当的时候显示验证消息。

对于简单模型类，只需添加**system.componentmodel. DataAnnotation**的**using**语句，然后将 **[必需]** 特性置于适当的属性上即可处理添加数据批注。 下面的示例将**Name**属性设置为视图中的必填字段。

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

在此应用程序中生成实体数据模型的情况下，这种情况稍微复杂一些。 如果您将数据批注直接添加到模型类，则当您从数据库更新模型时，将覆盖这些注释。 相反，您可以使用元数据分部类，这些类将存在来保存批注，并使用 **[MetadataType]** 特性与模型类关联。

1. 打开位于**Source/Ex6-AddingValidation/begin/** Folder 的**begin**解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 从 "**模型**" 文件夹打开 " **Album.cs** "。
3. 将**Album.cs**的内容替换为突出显示的代码，使其类似于以下内容：

    > [!NOTE]
    > 行 **[DisplayFormat （ConvertEmptyStringToNull = false）]** 指示在数据源中更新数据字段时，模型中的空字符串不会转换为 null。 当实体框架在数据批注验证字段之前将 null 值分配给模型时，此设置将避免异常。

    （代码段- *ASP.NET MVC 4 帮助器和窗体和验证-Ex6 唱片集元数据分部类*）

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > 此**唱片集**分部类具有一个**MetadataType**属性，该属性指向数据批注的**AlbumMetaData**类。 下面是一些用于注释唱片集模型的数据批注属性：
    > 
    > - 必需-指示该属性是必填字段
    > - DisplayName-定义要用于窗体字段和验证消息的文本
    > - DisplayFormat-指定显示和格式化数据字段的方式。
    > - StringLength-定义字符串字段的最大长度
    > - Range-为数值字段提供最大值和最小值
    > - ScaffoldColumn-允许从编辑器窗体中隐藏字段

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>任务 2-运行应用程序

在此任务中，您将使用在上一任务中选择的显示名称来测试 "创建" 和 "编辑" 页是否验证字段。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 **/StoreManager/Create**。 验证显示名称是否与分部类中的名称匹配（例如**唱片集画面 URL**而不是**AlbumArtUrl**）
3. 单击 "**创建**"，不填充窗体。 验证是否获取了相应的验证消息。

    !["创建" 页中已验证的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png ""创建" 页中已验证的字段")

    *"创建" 页中已验证的字段*
4. 您可以通过 "**编辑**" 页验证是否出现了这种情况。 将 URL 更改为 **/StoreManager/Edit/1** ，并验证显示名称是否与分部类中的名称匹配（例如**唱片集画面 URL**而不是**AlbumArtUrl**）。 清空 "**标题**" 和 "**价格**" 字段，然后单击 "**保存**"。 验证是否获取了相应的验证消息。

    ![编辑页中已验证的字段](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    *编辑页中已验证的字段*

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a>练习7：在客户端使用非引人注目 jQuery

在此练习中，你将了解如何在客户端启用 MVC 4 非引人注目 jQuery 验证。

> [!NOTE]
> 非引人注目的 jQuery 使用数据 ajax 前缀 JavaScript 在服务器上调用操作方法，而不是 intrusively 发出内联客户端脚本。

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a>任务 1-在启用非引人注目 jQuery 之前运行应用程序

在此任务中，您将在包含 jQuery 之前运行该应用程序，以便比较这两个验证模型。

1. 打开位于**Source/Ex7-UnobtrusivejQueryValidation/begin/** Folder 的**begin**解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 按 **F5** 运行该应用程序。
3. 项目在主页中启动。 浏览 **/StoreManager/Create**并单击 "**创建**" 而不填满窗体，验证是否获取了验证消息：

    ![已禁用客户端验证](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "已禁用客户端验证")

    *已禁用客户端验证*
4. 在浏览器中，打开 HTML 源代码：

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a>任务 2-启用非介入式客户端验证

在此任务中，**将从 web.config 文件中启用**jQuery 非**引人注目的客户端验证**，默认情况下，在所有新的 ASP.NET MVC 4 项目中将其设置为 false。 此外，还将添加必要的脚本引用，以使 jQuery 不引人注目的客户端验证工作。

1. 在项目根目录**中打开 web.config**文件，并确保 " **ClientValidationEnabled** " 和 " **UnobtrusiveJavaScriptEnabled** " 键的值设置为 " **true**"。

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > 还可以通过 Global.asax.cs 中的代码启用客户端验证，以获得相同的结果：
    > 
    > **HtmlHelper. ClientValidationEnabled = true;**
    > 
    > 此外，还可以将 ClientValidationEnabled 属性分配到任何控制器，以获得自定义行为。
2. 在**Views\StoreManager**中打开 "**创建"。**
3. 请确保通过 &quot; **~/bundles/jqueryval**&quot; 捆绑在视图中引用以下脚本文件， **jquery. validate**和**jquery. validate**。

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > 所有这些 jQuery 库都包含在 MVC 4 新项目中。 你可以在项目的 **/Scripts**文件夹中找到更多库。
    > 
    > 若要使此验证库正常工作，需要添加对 jQuery framework 库的引用。 由于已将此引用添加到 **\_的布局 cshtml**文件中，因此您不需要在此特定视图中添加该引用。

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a>任务 3-使用非引人注目 jQuery 验证运行应用程序

在此任务中，将测试**StoreManager** create view 模板在用户创建新相册时使用 jQuery 库执行客户端验证。

1. 按 **F5** 运行该应用程序。
2. 项目在主页中启动。 浏览 **/StoreManager/Create**并单击 "**创建**" 而不填满窗体，验证是否获取了验证消息：

    ![已启用 jQuery 的客户端验证](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "已启用 jQuery 的客户端验证")

    *已启用 jQuery 的客户端验证*
3. 在浏览器中，打开 "创建视图" 的源代码：

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > 对于每个客户端验证规则，非引人注目的 jQuery 会将具有数据-*rulename*=的属性添加 &quot;*消息*&quot;。 下面是一个标记列表，其中的标记将不引人注目地插入 html 输入字段以执行客户端验证：
   > 
   > - 数据-val
   > - 数据值-数字
   > - 数据-范围
   > - 数据-值-范围-最小/数据-范围-最大值
   > - 数据-val-必需
   > - 数据长度-长度
   > - 数据-值-长度-最大/数据值-长度-分钟
   > 
   > 所有数据值都用模型**数据批注**填充。 然后，可以在客户端运行在服务器端工作的所有逻辑。 例如，Price 属性在模型中具有以下数据批注：
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > 使用非引人注目的 jQuery 后，生成的代码为：
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>摘要

完成此动手实验后，你已了解如何让用户使用以下内容更改存储在数据库中的数据：

- 索引、创建、编辑、删除等控制器操作
- 用于在 HTML 表中显示属性的 ASP.NET MVC 基架功能
- 用于改进用户体验的自定义 HTML 帮助程序
- 对 HTTP GET 或 HTTP POST 调用做出反应的操作方法
- 类似视图模板（如创建和编辑）的共享编辑器模板
- 窗体元素，例如下拉
- 模型验证的数据批注
- 使用 jQuery 非引人注目库进行客户端验证

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 A：安装 Visual Studio Express 2012 for Web

您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。 以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。

1. 请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>附录 B：使用代码片段

使用代码片段，您可以随时获得所需的全部代码。 实验室文档将告诉你何时可以使用它们，如下图所示。

![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "使用 Visual Studio code 代码段将代码插入到项目中")

*使用 Visual Studio code 代码段将代码插入到项目中*

***使用键盘添加代码片段（C#仅限）***

1. 将光标放在要插入代码的位置。
2. 开始键入代码片段名称（不含空格或连字符）。
3. 请注意，IntelliSense 显示匹配的代码段名称。
4. 选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。
5. 按 Tab 键两次，将代码段插入到光标位置。

![开始键入代码片段名称](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "开始键入代码片段名称")

*开始键入代码片段名称*

![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "按 Tab 键以选择突出显示的代码段")

*按 Tab 键以选择突出显示的代码段*

![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "再次按 Tab 键，代码片段将展开")

*再次按 Tab 键，代码片段将展开*

***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2. 右键单击要插入代码片段的位置。

1. 选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。
2. 通过单击从列表中选择相关的代码片段。

![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")

*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*

![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "通过单击从列表中选择相关的代码片段")

*通过单击从列表中选择相关的代码片段*
