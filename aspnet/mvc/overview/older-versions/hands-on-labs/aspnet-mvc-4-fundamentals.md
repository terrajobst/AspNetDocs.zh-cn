---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 基础 |Microsoft Docs
author: rick-anderson
description: 此动手实验基于 MVC （模型视图控制器）音乐商店，这是一个教程应用程序，介绍如何使用 ASP.NET MV 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484568"
---
# <a name="aspnet-mvc-4-fundamentals"></a>ASP.NET MVC 4 基础知识

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

此动手实验基于 MVC （模型视图控制器）音乐商店，这是一个教程应用程序，介绍如何使用 ASP.NET MVC 和 Visual Studio 的分步说明。 在整个实验室中，您将学习这一简单功能，同时还能利用这些技术。 你将从一个简单的应用程序开始，并将生成该应用程序，直到你具有一个功能完备的 ASP.NET MVC 4 Web 应用程序。

此实验室与 ASP.NET MVC 4 结合使用。

若要浏览教程应用程序的 ASP.NET MVC 3 版本，可以在[mvc-音乐存储](https://github.com/evilDave/MVC-Music-Store)中找到它。

此动手实验假设开发人员在 Web 开发技术（例如 HTML 和 JavaScript）中拥有经验。

> [!NOTE]
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中，在[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)中提供。 [ASP.NET MVC 4 基础](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals)上提供了特定于此实验室的项目。

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a>音乐应用商店应用程序

将在整个实验室中生成的音乐应用商店 web 应用程序由三个主要部分组成：购物、结帐和管理。 访问者将能够按流派浏览唱片集，将唱片集添加到购物车，查看其选择内容，最后继续结帐以登录并完成订单。 此外，商店管理员还可以管理可用唱集及其主要属性。

![音乐应用商店屏幕](aspnet-mvc-4-fundamentals/_static/image1.png "音乐应用商店屏幕")

*音乐应用商店屏幕*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a>ASP.NET MVC 4 Essentials

将使用**模型视图控制器（MVC）** 构建音乐应用商店应用程序，这种体系结构模式将应用程序分成三个主要组件：

- **模型**：模型对象是应用程序中实现域逻辑的部分。 通常，模型对象还检索模型状态并将其存储在数据库中。
- **视图：** 视图是显示应用程序的用户界面（UI）的组件。 通常，此 UI 是用模型数据创建的。 例如，将根据唱片集对象的当前状态显示文本框和下拉列表的影集的 "编辑" 视图。
- **控制器：** 控制器是处理用户交互、操作模型并最终选择视图以呈现 UI 的组件。 在 MVC 应用程序中，视图仅显示信息；控制器处理并响应用户输入和交互。

MVC 模式可帮助你创建应用程序，用于分离应用程序的不同方面（输入逻辑、业务逻辑和 UI 逻辑），同时在这些元素之间提供松散耦合。 这种隔离可帮助你在构建应用程序时管理复杂性，因为它允许你一次集中关注实现的一个方面。 此外，MVC 模式使测试应用程序变得轻松，同时鼓励使用测试驱动开发（TDD）来创建应用程序。

**ASP.NET MVC**框架提供 ASP.NET Web 窗体模式的替代方法，用于创建基于 ASP.NET MVC 的 web 应用程序。 **ASP.NET MVC**框架是一种轻型、高度可测试的表示框架，与基于 Web 窗体的应用程序一样，它与现有的 ASP.NET 功能（如母版页和基于成员身份的身份验证）集成，因此你可以获得核心 .net framework 的所有功能。 如果已熟悉 ASP.NET Web 窗体，则这非常有用，因为你已使用的所有库也可用于 ASP.NET MVC 4 中。

此外，MVC 应用程序的三个主要组件之间的松散耦合还可促进并行开发。 例如，一个开发人员可以使用该视图，另一个开发人员可以处理控制器逻辑，而第三位开发人员可以专注于模型中的业务逻辑。

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在此动手实验中，您将学习如何：

- 根据音乐应用商店应用程序教程从头开始创建 ASP.NET MVC 应用程序
- 添加控制器以处理网站主页的 Url，并浏览其主要功能
- 添加视图以自定义显示的内容及其样式
- 添加模型类以包含和管理数据和域逻辑
- 使用视图模型模式将信息从控制器操作传递到视图模板
- 浏览 internet 应用程序的 ASP.NET MVC 4 新模板

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

你必须具有以下项才能完成此实验室：

- [Visual Studio 2012 Express For Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （有关如何安装的说明，请参阅[附录 A](#AppendixA) ）

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>安装

**安装代码片段**

为方便起见，你将通过此实验室管理的大部分代码都作为 Visual Studio code 片段提供。 若要安装代码段，请运行 **.\Source\Setup\CodeSnippets.vsi**文件。

如果你不熟悉 Visual Studio Code 代码段，并且想要了解如何使用它们，则可以参考本文档中的附录[C： &quot;附录 C：&quot;的代码段](#AppendixC)。

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>练习

此动手实验包括以下练习：

1. [练习1：创建 MusicStore ASP.NET MVC Web 应用程序项目](#Exercise1)
2. [练习2：创建控制器](#Exercise2)
3. [练习3：向控制器传递参数](#Exercise3)
4. [练习4：创建视图](#Exercise4)
5. [练习5：创建视图模型](#Exercise5)
6. [练习6：在视图中使用参数](#Exercise6)
7. [练习7：重叠 ASP.NET MVC 4 新模板](#Exercise7)

> [!NOTE]
> 每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。 如果需要更多帮助，请使用此解决方案作为指导。

完成本实验的估计时间： **60 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a>练习1：创建 MusicStore ASP.NET MVC Web 应用程序项目

在此练习中，您将学习如何在 Visual Studio 2012 Express for Web 及其主文件夹组织中创建 ASP.NET MVC 应用程序。 此外，你将了解如何添加新控制器并使其在应用程序的主页中显示一个简单的字符串。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a>任务 1-创建 ASP.NET MVC Web 应用程序项目

1. 在此任务中，你将使用 MVC Visual Studio 模板创建一个空的 ASP.NET MVC 应用程序项目。 开始**VS Express for Web**。
2. 在“文件”菜单上，单击“新建项目”。
3. 在 "**新建项目**" 对话框中，选择 " **ASP.NET MVC 4 Web 应用程序**" 项目类型，该类型位于 "  **C#Visual，** **web**模板列表" 下。
4. 将**名称**更改为*MvcMusicStore*。
5. 在此练习的源文件夹中，将解决方案的位置设置为新的**Begin**文件夹，例如 **[\Source\Ex01-CreatingMusicStoreProject\Begin]** 。 单击“确定”。

    !["创建新项目" 对话框](aspnet-mvc-4-fundamentals/_static/image2.png ""创建新项目" 对话框")

    *"创建新项目" 对话框*
6. 在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 "**基本**" 模板，并确保所选的**视图引擎**为**Razor**。 单击“确定”。

    !["新建 ASP.NET MVC 4 项目" 对话框](aspnet-mvc-4-fundamentals/_static/image3.png ""新建 ASP.NET MVC 4 项目" 对话框")

    *"新建 ASP.NET MVC 4 项目" 对话框*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a>任务 2-探索解决方案结构

ASP.NET MVC 框架包含一个 Visual Studio 项目模板，可帮助你创建支持 MVC 模式的 Web 应用程序。 此模板使用所需的文件夹、项模板和配置文件项创建一个新的 ASP.NET MVC Web 应用程序。

在此任务中，您将检查解决方案结构，以了解所涉及的元素以及它们之间的关系。 以下文件夹包含在所有 ASP.NET MVC 应用程序中，因为 ASP.NET MVC 框架默认情况下使用 &quot;约定 over 配置&quot; 方法，并基于文件夹命名约定做出一些默认假设。

1. 创建项目后，请查看在右侧的解决方案资源管理器中创建的文件夹结构：

    ![解决方案资源管理器中的 ASP.NET MVC 文件夹结构](aspnet-mvc-4-fundamentals/_static/image4.png "解决方案资源管理器中的 ASP.NET MVC 文件夹结构")

    *解决方案资源管理器中的 ASP.NET MVC 文件夹结构*

   1. **控制器**。 此文件夹将包含控制器类。 在基于 MVC 的应用程序中，控制器负责处理最终用户交互、操作模型，并最终选择用于呈现 UI 的视图。

       > [!NOTE]
       > MVC 框架要求所有控制器的名称以 &quot;控制器&quot;结束，例如 HomeController、LoginController 或 ProductController。
   2. **模型**。 此文件夹是为表示 MVC Web 应用程序的应用程序模型的类提供的。 这通常包括定义对象的代码和用于与数据存储区交互的逻辑。 通常，实际模型对象将位于单独的类库中。 但是，在创建新的应用程序时，您可能会包括类，然后在开发周期的稍后阶段将它们移到单独的类库中。
   3. **视图**。 此文件夹是视图的建议位置，这些组件负责显示应用程序的用户界面。 除了与呈现视图相关的任何其他文件，视图还使用 .aspx、.ascx、# 和 .master 文件。 Views 文件夹包含每个控制器的文件夹;文件夹以控制器名称前缀命名。 例如，如果你有一个名为**HomeController**的控制器，Views 文件夹将包含名为 Home 的文件夹。 默认情况下，当 ASP.NET MVC 框架加载视图时，它将在 Views\controllerName 文件夹（**views [controllerName] [action] .aspx**）或 Razor 视图的（**views [ControllerName] [action]** ）中查找具有请求的视图名称的 .aspx 文件。

      > [!NOTE]
      > 除了前面列出的文件夹，MVC Web 应用程序还使用**global.asax**文件设置全局 URL 路由默认值，并使用**web.config 文件来**配置应用程序。

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a>任务 3-添加 HomeController

在不使用 MVC 框架的 ASP.NET 应用程序中，用户交互按照页面以及从这些页面引发和处理事件的方式进行组织。 相比之下，用户与 ASP.NET MVC 应用程序的交互是围绕控制器及其操作方法组织的。

另一方面，ASP.NET MVC 框架将 Url 映射到称为控制器的类。 控制器处理传入的请求，处理用户输入和交互，执行适当的应用程序逻辑，并确定要发送回客户端的响应（显示 HTML、下载文件、重定向到其他 URL 等）。 对于显示 HTML，控制器类通常会调用单独的视图组件来生成请求的 HTML 标记。 在 MVC 应用程序中，视图仅显示信息；控制器处理并响应用户输入和交互。

在此任务中，你将添加一个控制器类，该类将处理指向音乐应用商店网站主页的 Url。

1. 在解决方案资源管理器中右键单击 "**控制器**" 文件夹，选择 "**添加**"，然后选择 "**控制器**" 命令：

    ![添加控制器命令](aspnet-mvc-4-fundamentals/_static/image5.png "添加控制器命令")

    *添加控制器命令*
2. "**添加控制器**" 对话框随即出现。 将控制器命名为*HomeController* ，然后按 "**添加**"。

    !["添加控制器" 对话框](aspnet-mvc-4-fundamentals/_static/image6.png ""添加控制器" 对话框")

    *"添加控制器" 对话框*
3. **在 controller 文件夹中**创建文件**HomeController.cs** 。 为了使**HomeController**返回其索引操作的字符串，请将**Index**方法替换为以下代码：

    （代码段- *ASP.NET MVC 4 基础-Ex1 HomeController Index*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在此任务中，你将在 web 浏览器中尝试应用程序。

1. 按**F5**运行该应用程序。 项目已编译并且本地 IIS Web 服务器启动。 本地 IIS Web 服务器将自动打开指向 Web 服务器 URL 的 web 浏览器。

    ![在 web 浏览器中运行的应用程序](aspnet-mvc-4-fundamentals/_static/image7.png "在 web 浏览器中运行的应用程序")

    *在 web 浏览器中运行的应用程序*

    > [!NOTE]
    > 本地 IIS Web 服务器将按随机可用端口号运行网站。 在上图中，站点正在 `http://localhost:50103/`上运行，因此使用的是端口50103。 端口号可能有所不同。
2. 关闭浏览器。

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a>练习2：创建控制器

在此练习中，您将学习如何更新控制器以实现音乐应用商店应用程序的简单功能。 该控制器将定义用于处理以下每个特定请求的操作方法：

- 音乐应用商店中音乐流派的列表页
- 列出特定流派的所有音乐唱片集的浏览页
- 显示特定音乐唱片集相关信息的详细信息页

对于本练习的作用域，这些操作将只返回一个字符串。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a>任务 1-添加新的 StoreController 类

在此任务中，将添加新的控制器。

1. 如果尚未打开，请启动**VS Express for Web 2012**。
2. 在 "**文件**" 菜单中，选择 "**打开项目**"。 在 "打开项目" 对话框中，浏览到**Source\Ex02-CreatingAController\Begin**，选择 "**开始**"，然后单击 "**打开**"。 或者，您也可以继续使用在完成上一练习后获得的解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
3. 添加新控制器。 为此，请在解决方案资源管理器中右键单击 "**控制器**" 文件夹，选择 "**添加**"，然后选择 "**控制器**" 命令。 将**控制器名称**更改为*StoreController*，并单击 "**添加**"。

    !["添加控制器" 对话框](aspnet-mvc-4-fundamentals/_static/image8.png ""添加控制器" 对话框")

    *"添加控制器" 对话框*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a>任务 2-修改 StoreController 的操作

在此任务中，您将修改称为**操作**的控制器方法。 操作负责处理 URL 请求，并确定应发送回调用 URL 的浏览器或用户的内容。

1. **StoreController**类已经有了**Index**方法。 稍后将在本实验室中使用它来实现列出音乐商店所有流派的页面。 现在，只需将**Index**方法替换为以下代码，即可从 Store （）&quot;返回字符串 &quot;Hello：

    （代码段- *ASP.NET MVC 4 基础-Buildingappswithcachingservice-ex2-getproducts latency-cs StoreController Index*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. 添加**浏览**和**详细信息**方法。 为此，请将以下代码添加到**StoreController**：

    （代码段- *ASP.NET MVC 4 基础-Buildingappswithcachingservice-ex2-getproducts latency-cs StoreController BrowseAndDetails*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，你将在 web 浏览器中尝试应用程序。

1. 按**F5**运行该应用程序。
2. 项目在**主页**中启动。 更改 URL 以验证每个操作的实现。

    1. **/Store**。 你将看到 **&quot;Hello From Store （）&quot;** 。
    2. **/Store/Browse**。 你将看到 **&quot;Hello From Store. Browse （）&quot;** 。
    3. **/Store/Details**。 你将看到 **&quot;Hello From Store. Details （）&quot;** 。

        ![浏览 StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "浏览 StoreBrowse")

        *浏览/Store/Browse*
3. 关闭浏览器。

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a>练习3：向控制器传递参数

到现在为止，您已经从控制器返回常量字符串。 在本练习中，您将学习如何使用 URL 和 querystring 将参数传递给控制器，然后使方法操作使用文本响应浏览器。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a>任务 1-将流派参数添加到 StoreController

在此任务中，您将使用**查询字符串**将参数发送到**StoreController**中的**Browse**操作方法。

1. 如果尚未打开，请启动**VS Express for Web**。
2. 在 "**文件**" 菜单中，选择 "**打开项目**"。 在 "打开项目" 对话框中，浏览到**Source\Ex03-PassingParametersToAController\Begin**，选择 "**开始**"，然后单击 "**打开**"。 或者，您也可以继续使用在完成上一练习后获得的解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
3. 打开**StoreController**类。 为此，请在 "**解决方案资源管理器**中，展开"**控制器**"文件夹，然后双击" **StoreController.cs**"。
4. 更改**Browse**方法，并添加一个字符串参数来请求特定的流派。 调用时，ASP.NET MVC 会自动将名为 "**流派**" 的任何 querystring 或窗体 post 参数传递到此操作方法。 为此，请将**Browse**方法替换为以下代码：

    （代码段- *ASP.NET MVC 4 基础-Section-cs StoreController BrowseMethod*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> 你使用的是**Httputility.javascriptstringencode server.htmlencode**实用工具方法，以防止用户使用/Store/Browse 之类的链接将 Javascript 注入到视图中 **？流派 =&lt;脚本&gt;window。 location = "[http://hackersite.com](http://hackersite.com)"&lt;/script&gt;** 。
> 
> 有关进一步说明，请访问[此 msdn 文章](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx)。

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>任务 2-运行应用程序

在此任务中，你将在 web 浏览器中试用应用程序并使用**流派**参数。

1. 按**F5**运行该应用程序。
2. 项目在**主页**中启动。 将 URL 更改为 */Store/Browse？流派 = Disco*验证操作是否收到流派参数。

    ![浏览 StoreBrowseGenre = Disco](aspnet-mvc-4-fundamentals/_static/image10.png "浏览 StoreBrowseGenre = Disco")

    *浏览/Store/Browse？流派 = Disco*
3. 关闭浏览器。

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a>任务 3-添加嵌入在 URL 中的 Id 参数

在此任务中，你将使用**URL**将**Id**参数传递给**StoreController**的**详细信息**操作方法。 ASP.NET MVC 的默认路由约定是将操作方法名称后面的 URL 段视为名为**Id**的参数。如果操作方法包含名为 Id 的参数，则 ASP.NET MVC 会自动将 URL 段作为参数传递给你。 在 URL**存储/详细信息/5**中， **Id**将解释为**5**。

1. 更改**StoreController**的**详细信息**方法，添加一个名为**id**的**int**参数。为此，请将**详细信息**方法替换为以下代码：

    （代码段- *ASP.NET MVC 4 基础-Section-cs StoreController DetailsMethod*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在此任务中，你将在 web 浏览器中试用应用程序并使用**Id**参数。

1. 按**F5**运行该应用程序。
2. 项目在**主页**中启动。 将 URL 更改为 " */Store/Details/5* " 以验证操作是否收到 id 参数。

    ![浏览 StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "浏览 StoreDetails5")

    *浏览/Store/Details/5*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a>练习4：创建视图

到目前为止，您已经从控制器操作返回了字符串。 尽管这是了解控制器工作方式的有用方法，但并不是实际的 Web 应用程序的构建方式。 视图是提供更好的方法，可让你使用模板文件在浏览器中生成 HTML。

在本练习中，您将学习如何添加布局母版页，以便为常见 HTML 内容设置模板、用于增强网站外观的样式表，以及用于使 HomeController 返回 HTML 的视图模板。

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a>任务 1-修改文件 \_layout

文件 **~/Views/Shared/\_layout**允许您设置一个模板，以便在整个网站中使用通用 HTML。 在此任务中，您将添加一个具有公共标题的布局母版页，其中包含指向主页和存储区的链接。

1. 如果尚未打开，请启动**VS Express for Web**。
2. 在 "**文件**" 菜单中，选择 "**打开项目**"。 在 "打开项目" 对话框中，浏览到**Source\Ex04-CreatingAView\Begin**，选择 "**开始**"，然后单击 "**打开**"。 或者，您也可以继续使用在完成上一练习后获得的解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
3. 文件<strong>\_layout</strong>包含网站上所有页的 HTML 容器布局。 它包括 HTML 响应的<strong>&lt;html&gt;</strong>元素，以及<strong>&lt;head&gt;</strong>和<strong>&lt;正文&gt;</strong>元素。 HTML 正文中的<strong>@RenderBody（）</strong>标识查看模板将能够用动态内容填充的区域。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. 添加一个公共标题，其中包含指向主页的链接和网站中所有页面上的存储区。 为此，请在下面 &lt;body&gt; 语句中添加以下代码。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. 包含一个 div，用于呈现每个页面的正文部分。 将<strong>@RenderBody（）</strong>替换为以下突出显示的代码C#：（）

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > 您知道吗？ Visual Studio 2012 提供了一些代码段，使你可以轻松地将常用代码添加到 HTML、代码文件等中！ 通过键入 **&lt;div&gt;** 并按**tab**两次以插入完整的**div**标记来尝试此方法。

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a>任务 2-添加 CSS 样式表

空项目模板包含一个非常简单的 CSS 文件，其中只包含用于显示基本窗体和验证消息的样式。 您将使用其他 CSS 和图像（可能由设计器提供）来增强网站的外观。

在此任务中，您将添加 CSS 样式表以定义站点的样式。

1. 此实验室的**Source\Assets\Content**文件夹中包括了 CSS 文件和映像。 若要将它们添加到应用程序，请将其内容从**Windows 资源管理器**窗口拖到 Visual Studio Express for Web 中的**解决方案资源管理器**，如下所示：

    ![拖动样式内容](aspnet-mvc-4-fundamentals/_static/image12.png "拖动样式内容")

    *拖动样式内容*
2. 将显示一个警告对话框，要求确认是否替换**Site .css**文件和一些现有的图像。 选中 "**应用到所有项**"，然后单击 **"是"** 。

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a>任务 3-添加视图模板

在此任务中，你将添加一个视图模板以生成将使用在本练习中添加的布局母版页和 CSS 的 HTML 响应。

1. 若要在浏览网站的主页时使用视图模板，首先需要指出， **HomeController Index**方法将返回一个**视图**，而不是返回一个字符串。 打开**HomeController**类并更改其**Index**方法以返回**ActionResult**，并使其返回**View （）** 。

    （代码段- *ASP.NET MVC 4 基础-Ex4 HomeController Index*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. 现在，需要添加相应的视图模板。 为此，请在**索引**操作方法中**右键单击**，然后选择 "**添加视图**"。 此时将显示 "**添加视图**" 对话框。

    ![从 Index 方法中添加视图](aspnet-mvc-4-fundamentals/_static/image13.png "从 Index 方法中添加视图")

    *从 Index 方法中添加视图*
3. 将显示 "**添加视图**" 对话框以生成视图模板文件。 默认情况下，此对话框预先填充视图模板的名称，使其与将使用它的操作方法匹配。 因为你在 HomeController 中使用了**索引**操作方法中的 "**添加视图**" 上下文菜单，所以 "**添加视图**" 对话框中的默认视图名称为 "索引"。 单击 **“添加”** 。

    ![添加视图对话框](aspnet-mvc-4-fundamentals/_static/image14.png "添加视图对话框")

    *添加视图对话框*
4. Visual Studio 将在**Views\Home**文件夹中生成一个**索引. cshtml**视图模板，然后将其打开。

    ![已创建主索引视图](aspnet-mvc-4-fundamentals/_static/image15.png "已创建主索引视图")

    *已创建主索引视图*

    > [!NOTE]
    > **索引 cshtml**文件的名称和位置与默认的 ASP.NET MVC 命名约定相关。
    > 
    > 文件夹 \Views\**home** 与控制器名称（**home**控制器）匹配。 视图模板名称（**Index**）匹配将显示视图的控制器操作方法。
    > 
    > 这样，当使用此命名约定返回视图时，ASP.NET MVC 就不必显式指定视图模板的名称或位置。
5. 生成的视图模板基于之前定义的 **\_布局 cshtml**模板。 将 ViewBag 属性更新为**home**，将主要内容更改为 **"** 主页"，如下面的代码所示：

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. 在解决方案资源管理器中选择 " **MvcMusicStore**项目"，并按**F5**运行该应用程序。

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a>任务4：验证

若要验证是否正确执行了上一练习中的所有步骤，请按以下步骤操作：

在浏览器中打开应用程序时，应注意以下事项：

1. HomeController 的索引操作方法会找到并显示 **\Views\Home\Index.cshtml**视图模板，即使代码调用了**返回视图（）** ，因为视图模板遵循了标准命名约定。
2. "主页" 页显示在 **\Views\Home\Index.cshtml**视图模板内定义的欢迎消息。
3. 主页使用 **\_layout**模板，因此欢迎消息包含在标准网站 HTML 布局中。

    ![使用定义的 LayoutPage 和样式的主索引视图](aspnet-mvc-4-fundamentals/_static/image16.png "使用定义的 LayoutPage 和样式的主索引视图")

    *使用定义的 LayoutPage 和样式的主索引视图*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a>练习5：创建视图模型

到目前为止，你已使视图显示了硬编码的 HTML，但为了创建动态 web 应用程序，视图模板应接收来自控制器的信息。 用于此目的的一种常见方法是**ViewModel**模式，该模式允许控制器打包生成相应 HTML 响应所需的所有信息。

在此练习中，您将学习如何创建 ViewModel 类并添加所需的属性：存储中的流派数量以及这些流派的列表。 您还将更新 StoreController 以使用创建的 ViewModel，最后，您将创建一个新的视图模板，该模板将在页面中显示所述的属性。

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a>任务 1-创建 ViewModel 类

在此任务中，你将创建一个 ViewModel 类，该类将实现商店流派列表方案。

1. 如果尚未打开，请启动**VS Express for Web**。
2. 在 "**文件**" 菜单中，选择 "**打开项目**"。 在 "打开项目" 对话框中，浏览到**Source\Ex05-CreatingAViewModel\Begin**，选择 "**开始**"，然后单击 "**打开**"。 或者，您也可以继续使用在完成上一练习后获得的解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
3. 创建用于保存 ViewModel 的**viewmodel**文件夹。 为此，请右键单击顶级**MvcMusicStore**项目，选择 "**添加**"，然后选择 "**新建文件夹**"。

    ![添加新文件夹](aspnet-mvc-4-fundamentals/_static/image17.png "添加新文件夹")

    *添加新文件夹*
4. 将文件夹命名为*viewmodel*。

    ![解决方案资源管理器中的 Viewmodel 文件夹](aspnet-mvc-4-fundamentals/_static/image18.png "解决方案资源管理器中的 Viewmodel 文件夹")

    *解决方案资源管理器中的 Viewmodel 文件夹*
5. 创建**ViewModel**类。 为此，请右键单击最近创建的**viewmodel**文件夹，选择 "**添加**"，然后选择 "**新建项**"。 在 "**代码**" 下，选择 "**类**" 项，并将文件命名为*StoreIndexViewModel.cs*，然后单击 "**添加**"。

    ![添加新类](aspnet-mvc-4-fundamentals/_static/image19.png "添加新类")

    *添加新类*

    ![创建 StoreIndexViewModel 类](aspnet-mvc-4-fundamentals/_static/image20.png "创建 StoreIndexViewModel 类")

    *创建 StoreIndexViewModel 类*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a>任务 2-将属性添加到 ViewModel 类

需要将 StoreController 中的两个参数传递给视图模板，才能生成所需的 HTML 响应：存储中的流派数量和这些流派的列表。

在此任务中，您将这两个属性添加到**StoreIndexViewModel**类： **NumberOfGenres** （整数）和**流派**（字符串列表）。

1. 将**NumberOfGenres**和**流派**属性添加到**StoreIndexViewModel**类。 为此，请向类定义添加以下两行：

    （代码段- *ASP.NET MVC 4 基础-Ex5 StoreIndexViewModel properties*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> **{Get; set;}** 表示法利用了C#自动实现的属性功能。 它提供属性的优点，而无需声明支持字段。

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a>任务 3-将 StoreController 更新为使用 StoreIndexViewModel

**StoreIndexViewModel**类将从**StoreController**的**Index**方法传递到视图模板所需的信息封装为生成响应。

在此任务中，你将更新**StoreController**以使用**StoreIndexViewModel**。

1. 打开**StoreController**类。

    ![打开 StoreController 类](aspnet-mvc-4-fundamentals/_static/image21.png "打开 StoreController 类")

    *打开 StoreController 类*
2. 若要使用**StoreController**中的**StoreIndexViewModel**类，请在**StoreController**代码的顶部添加以下命名空间：

    （代码段- *ASP.NET MVC 4 基础-Ex5 StoreIndexViewModel Using viewmodel*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. 更改**StoreController**的**索引**操作方法，使其创建并填充**StoreIndexViewModel**对象，然后将其传递给视图模板以生成 HTML 响应。

    > [!NOTE]
    > 在实验室 &quot;ASP.NET MVC 模型和数据访问&quot; 您将编写用于从数据库检索存储流派列表的代码。 在下面的代码中，将创建将填充**StoreIndexViewModel**的虚拟数据流派的**列表**。
    > 
    > 创建并设置**StoreIndexViewModel**对象后，它将作为参数传递给**视图**方法。 这表示视图模板将使用该对象来生成 HTML 响应。
4. 将**Index**方法替换为以下代码：

    （代码段- *ASP.NET MVC 4 基础-Ex5 StoreController Index 方法*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> 如果不熟悉C#，则可以假设使用**var**表示**viewModel**变量为后期绑定。 这不是正确的- C#编译器将根据分配给变量的内容来使用类型推理来确定**viewModel**类型是否为**StoreIndexViewModel**。 此外，通过将本地**viewModel**变量编译为**StoreIndexViewModel**类型，可以获取编译时检查和 Visual Studio 代码编辑器支持。

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a>任务 4-创建使用 StoreIndexViewModel 的视图模板

在此任务中，您将创建一个视图模板，该模板将使用从控制器传递的 StoreIndexViewModel 对象来显示流派列表。

1. 在创建新的视图模板之前，让我们生成项目，以便 "**添加视图" 对话框**了解**StoreIndexViewModel**类。 通过选择 "**生成**" 菜单项生成项目，然后**生成 MvcMusicStore**。

    ![生成项目](aspnet-mvc-4-fundamentals/_static/image22.png "生成项目")

    *生成项目*
2. 创建新的视图模板。 为此，请在**索引**方法中右键单击，然后选择 "**添加视图**"。

    ![添加视图](aspnet-mvc-4-fundamentals/_static/image23.png "添加视图")

    *添加视图*
3. 由于 "**添加视图" 对话框**是从**StoreController**调用的，因此它将在默认情况下添加到 **\Views\Store\Index.cshtml**文件中。 选中 "**创建强类型视图**" 复选框，然后选择 " **StoreIndexViewModel** " 作为**模型类**。 此外，请确保所选的视图引擎为**Razor**。 单击 **“添加”** 。

    ![添加视图对话框](aspnet-mvc-4-fundamentals/_static/image24.png "添加视图对话框")

    *添加视图对话框*

    将创建并打开 " **\Views\Store\Index.cshtml** " 视图模板文件。 根据在上一步中提供给 "**添加视图**" 对话框的信息，视图模板需要**StoreIndexViewModel**实例作为要用于生成 HTML 响应的数据。 你会注意到，模板在中C#继承 `ViewPage<musicstore.viewmodels.storeindexviewmodel>`。

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a>任务 5-更新视图模板

在此任务中，您将更新在上一任务中创建的视图模板以检索流派的数目及其在页面中的名称。

> [!NOTE]
> 您将使用 @ 语法（通常称为 &quot;代码片段&quot;）来执行视图模板中的代码。

1. 在**索引的 cshtml**文件中 **，将其**代码替换为以下代码：

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. 循环遍历**StoreIndexViewModel**中的流派列表，并使用**FOREACH**循环创建 HTML **&lt;ul&gt;** 列表。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. 按**F5**运行应用程序并浏览 **/Store**。 你将看到在**StoreIndexViewModel**对象中**传递给视图**模板的流派列表。

    ![显示流派列表的视图](aspnet-mvc-4-fundamentals/_static/image26.png "显示流派列表的视图")

    *显示流派列表的视图*
4. 关闭浏览器。

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a>练习6：在视图中使用参数

在练习3中，你学习了如何将参数传递给控制器。 在此练习中，您将学习如何在视图模板中使用这些参数。 为此，你将首先引入有助于管理你的数据和域逻辑的类。 此外，你将了解如何创建指向 ASP.NET MVC 应用程序内的页面的链接，而无需担心 URL 路径编码。

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a>任务 1-添加模型类

与 Viewmodel 不同，只是为了将信息从控制器传递到视图，而生成的模型类包含和管理数据和域逻辑。 在此任务中，您将添加两个模型类来表示这些概念：**流派**和**唱片集**。

1. 如果尚未打开，请启动**VS Express for Web**
2. 在 "**文件**" 菜单中，选择 "**打开项目**"。 在 "打开项目" 对话框中，浏览到**Source\Ex06-UsingParametersInView\Begin**，选择 "**开始**"，然后单击 "**打开**"。 或者，您也可以继续使用在完成上一练习后获得的解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
3. 添加**流派**模型类。 为此，请在**解决方案资源管理器**中右键单击 "**模型**" 文件夹，选择 "**添加**"，然后选择 "**新建项**" 选项。 在 "**代码**" 下，选择 "**类**" 项，并将文件命名为*Genre.cs*，然后单击 "**添加**"。

    ![添加类](aspnet-mvc-4-fundamentals/_static/image27.png "添加类")

    *添加新项*

    ![添加流派模型类](aspnet-mvc-4-fundamentals/_static/image28.png "添加流派模型类")

    *添加流派模型类*
4. 向流派类添加**Name**属性。 为此，请添加以下代码：

    （代码段- *ASP.NET MVC 4 基础-Ex6 流派*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. 按照与前面相同的过程操作，添加一个**唱片集**类。 为此，请在**解决方案资源管理器**中右键单击 "**模型**" 文件夹，选择 "**添加**"，然后选择 "**新建项**" 选项。 在 "**代码**" 下，选择 "**类**" 项，并将文件命名为*Album.cs*，然后单击 "**添加**"。
6. 向唱片集类添加两个属性： "**流派**" 和 "**标题**"。 为此，请添加以下代码：

    （代码段- *ASP.NET MVC 4 基础-Ex6 唱片集*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a>任务 2-添加 StoreBrowseViewModel

此任务中将使用**StoreBrowseViewModel**来显示与所选流派匹配的唱片集。 在此任务中，您将创建此类，然后添加两个属性来处理**流派**及其**唱片集**的列表。

1. 添加**StoreBrowseViewModel**类。 为此，请在**解决方案资源管理器**中右键单击**viewmodel**文件夹，选择 "**添加**"，然后选择 "**新建项**" 选项。 在 "**代码**" 下，选择 "**类**" 项，并将文件命名为*StoreBrowseViewModel.cs*，然后单击 "**添加**"。
2. 在**StoreBrowseViewModel**类中添加对模型的引用。 为此，请使用命名空间添加以下内容：

    （代码段- *ASP.NET MVC 4 基础-Ex6 UsingModel*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. 将两个属性添加到**StoreBrowseViewModel**类：**流派**和**唱片集**。 为此，请添加以下代码：

    （代码段- *ASP.NET MVC 4 基础-Ex6 ModelProperties*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> 什么是**list&lt;唱片集&gt;** ？：此定义使用**列表&lt;t&gt;** 类型，其中**t**限制此**列表**的元素所属的类型，在此示例中为**唱片集**（或其任意后代）。
> 
> 此功能用于设计类和方法，以延迟一种或多种类型的规范，直到客户端代码声明并实例化类或方法，这一功能C#称为**泛型**。
> 
> **List&lt;t&gt;** 是**ArrayList**类型的泛型等效项，并在**system.web**命名空间中可用。 使用**泛型**的优点之一是，由于指定了类型，因此您无需注意类型检查操作，例如将元素强制转换为**影集**，就像对**ArrayList**进行操作一样。

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a>任务 3-在 StoreController 中使用 New ViewModel

在此任务中，您将修改**StoreController**的**浏览**和**详细信息**操作方法以使用新的**StoreBrowseViewModel**。

1. 在**StoreController**类中添加对模型文件夹的引用。 为此，请展开**解决方案资源管理器**中的 "**控制器**" 文件夹，然后打开**StoreController**类。 然后添加以下代码：

    （代码段- *ASP.NET MVC 4 基础-Ex6 UsingModelInController*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. 替换**浏览**操作方法以使用**StoreViewBrowseController**类。 您将创建一个流派和两个包含虚拟数据的新的唱集对象（在下一个动手实验中，您将使用数据库中的真实数据）。 为此，请将**Browse**方法替换为以下代码：

    （代码段- *ASP.NET MVC 4 基础-Ex6 BrowseMethod*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. 替换**详细信息**操作方法以使用**StoreViewBrowseController**类。 您将创建一个新的**唱片集**对象以返回到**视图**中。 为此，请将**详细信息**方法替换为以下代码：

    （代码段- *ASP.NET MVC 4 基础-Ex6 DetailsMethod*）

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a>任务 4-添加浏览视图模板

在此任务中，您将添加一个**浏览**视图以显示针对特定流派找到的唱集。

1. 在创建新的视图模板之前，应生成项目，以便 "**添加视图**" 对话框知道要使用的**ViewModel**类。 通过选择 "**生成**" 菜单项生成项目，然后**生成 MvcMusicStore**。
2. 添加 "**浏览**" 视图。 为此，请在**StoreController**的 "**浏览**操作" 方法中右键单击，然后单击 "**添加视图**"。
3. 在 "**添加视图**" 对话框中，验证视图名称是否为 "**浏览**"。 选中 "**创建强类型视图**" 复选框，然后从 "**模型类**" 下拉列表中选择 " **StoreBrowseViewModel** "。 让其他字段保留其默认值。 然后单击 **“添加”** 。

    ![添加浏览视图](aspnet-mvc-4-fundamentals/_static/image29.png "添加浏览视图")

    *添加浏览视图*
4. 修改**Browse**以显示流派的信息，访问传递到视图模板的**StoreBrowseViewModel**对象。 为此，请将内容替换为以下内容：（C#）

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>任务 5-运行应用程序

在此任务中，您将测试**browse**方法是否从**浏览**方法操作检索相册。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 **/Store/Browse？流派 = Disco**验证操作是否返回了两个唱片集。

    ![浏览存储 Disco 唱集](aspnet-mvc-4-fundamentals/_static/image30.png "浏览存储 Disco 唱集")

    *浏览存储 Disco 唱集*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a>任务 6-显示有关特定唱片集的信息

在此任务中，您将实现 "**存储/详细信息**" 视图以显示有关特定唱片集的信息。 在此动手实验中，您将显示的有关唱片集的所有内容都已包含在**视图**模板中。 因此，你将使用当前的**StoreBrowseViewModel**模板将唱片集传递给它，而不是创建**StoreDetailsViewModel**类。

1. 如果需要，请关闭浏览器以返回到 Visual Studio 窗口。 为**StoreController**的**详细信息**操作方法添加新的**详细信息**视图。 为此，请在**StoreController**类中右键单击**详细信息**方法，然后单击 "**添加视图**"。
2. 在 "**添加视图**" 对话框中，验证**视图名称**是否为 "**详细信息**"。 选中 "**创建强类型视图**" 复选框，然后从 "**模型类**" 下拉框中选择 "**唱片集**"。 让其他字段保留其默认值。 然后单击 **“添加”** 。 这会创建并打开 **\Views\Store\Details.cshtml**文件。

    ![添加详细信息视图](aspnet-mvc-4-fundamentals/_static/image31.png "添加详细信息视图")

    *添加详细信息视图*
3. 修改**详细信息 cshtml**文件以显示唱片集的信息，并访问传递到视图模板的**唱片集**对象。 为此，请将内容替换为以下内容：（C#）

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>任务 7-运行应用程序

在此任务中，您将测试**详细**信息视图是否从**详细信息操作**方法中检索唱片集的信息。

1. 按**F5**运行该应用程序。
2. 项目在**主页**中启动。 将 URL 更改为 " **/Store/Details/5** " 以验证唱片集的信息。

    ![浏览唱片集详细信息](aspnet-mvc-4-fundamentals/_static/image32.png "浏览唱片集详细信息")

    *浏览唱片集的详细信息*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a>任务 8-在页面之间添加链接

在此任务中，你将在 "应用商店" 视图中添加一个链接，使每个流派名称中有一个链接到相应的 **/Store/Browse** URL。 这样一来，当您单击某个流派（例如**disco**）时，它将导航到 **/Store/Browse？流派 = Disco** URL。

1. 如果需要，请关闭浏览器以返回到 Visual Studio 窗口。 更新 "**索引**" 页以添加指向**浏览**页的链接。 为此，请在**解决方案资源管理器**展开**Views**文件夹，再展开 "**存储**" 文件夹，然后双击 "**索引**" 页。
2. 添加指向浏览视图的链接，指示所选流派。 为此，请将以下突出显示的代码替换 **&lt;li&gt;** 标记中：C#（）

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > 另一种方法是直接链接到页面，代码如下所示：
   > 
   > &lt;href =&quot;/Store/Browse？流派 =@genreName&quot;&gt;@genreName/a &lt;&gt;
   > 
   > 尽管此方法有效，但它依赖于硬编码的字符串。 如果以后重命名控制器，则必须手动更改此指令。 更好的替代方法是使用**HTML 帮助器**方法。 ASP.NET MVC 包含可用于此类任务的 HTML 帮助器方法。 使用**html.actionlink （）** helper 方法，可以轻松地生成 html **&lt;&gt;** 链接，确保 url 路径正确地进行 url 编码。
   > 
   > Html.actionlink 有多个重载。 在本练习中，您将使用一个带有三个参数的：
   > 
   > 1. 链接文本，将显示流派名称
   > 2. 控制器操作名称（**浏览**）
   > 3. 路由参数值，同时指定名称（**流派**）和值（**流派名称**）

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a>任务 9-运行应用程序

在此任务中，将测试是否显示每个流派，并提供指向相应 **/Store/Browse** URL 的链接。

1. 按**F5**运行该应用程序。
2. 项目在主页中启动。 将 URL 更改为 " **/Store** " 以验证每个流派是否链接到相应的 **/Store/Browse** URL。

    ![浏览具有浏览页链接的流派](aspnet-mvc-4-fundamentals/_static/image33.png "浏览具有浏览页链接的流派")

    *浏览具有浏览页链接的流派*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a>任务 10-使用动态 ViewModel 集合传递值

在此任务中，您将学习一种简单而有效的方法，可在控制器和视图之间传递值，而无需在模型中进行任何更改。 ASP.NET MVC 4 提供 &quot;ViewModel&quot;的集合，可将其分配给任何动态值，也可在控制器和视图中进行访问。

现在，你将使用 ViewBag 动态集合将 &quot;**带有星标&quot; 流派**的列表从控制器传递到视图。 "商店索引" 视图将访问**ViewModel**并显示信息。

1. 如果需要，请关闭浏览器以返回到 Visual Studio 窗口。 打开**StoreController.cs**并修改**Index**方法，以便在 ViewModel 集合中创建带有星标流派列表：

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > 你还可以使用语法**ViewBag [&quot;带有星标&quot;]** 来访问这些属性。
2. **&quot;"带有星标"&quot;** 的星形图标包含在此实验室的 " **Source\Assets\Images** " 文件夹中。 若要将该应用程序添加到应用程序，请将其内容从**Windows 资源管理器**窗口拖到 Visual Web Developer Express 中的**解决方案资源管理器**，如下所示：

    ![向解决方案添加星形图像](aspnet-mvc-4-fundamentals/_static/image34.png "向解决方案添加星形图像")

    *向解决方案添加星形图像*
3. 打开 "查看**存储/索引**" 并修改内容。 你将在**ViewBag**集合中读取 &quot;带有星标&quot; 属性，并询问当前流派名称是否在列表中。 在这种情况下，你将向流派链接显示一个星形图标。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a>任务 11-运行应用程序

在此任务中，您将测试带有星标流派是否显示星形图标。

1. 按**F5**运行该应用程序。
2. 项目在**主页**中启动。 将 URL 更改为 " **/Store** " 以验证每个特色流派是否具有 "尊重" 标签：

    ![浏览具有带有星标元素的流派](aspnet-mvc-4-fundamentals/_static/image35.png "浏览具有带有星标元素的流派")

    *浏览具有带有星标元素的流派*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a>练习7：重叠 ASP.NET MVC 4 新模板

在此练习中，你将了解 ASP.NET MVC 4 项目模板中的增强功能，其中介绍了新模板的最相关功能。

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a>任务1：浏览 ASP.NET MVC 4 Internet 应用程序模板

1. 如果尚未打开，请启动**VS Express for Web**
2. 选择**文件 |新建 |项目**菜单命令。 在 "**新建项目**" 对话框中，选择 "**视觉C#对象 |Web**模板 "，并选择" **ASP.NET MVC 4 Web 应用程序**"。 将项目**命名**为 " *MusicStore* " 并更新**解决方案名称**以*开始*，然后选择一个位置（或保留默认值），然后单击 **"确定"** 。

    ![创建新的 ASP.NET MVC 4 项目](aspnet-mvc-4-fundamentals/_static/image36.png "创建新的 ASP.NET MVC 4 项目")

    *创建新的 ASP.NET MVC 4 项目*
3. 在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**" 项目模板，然后单击 **"确定"** 。 请注意，可以选择 Razor 或 ASPX 作为视图引擎。

    ![创建新的 ASP.NET MVC 4 Internet 应用程序](aspnet-mvc-4-fundamentals/_static/image37.png "创建新的 ASP.NET MVC 4 Internet 应用程序")

    *创建新的 ASP.NET MVC 4 Internet 应用程序*

    > [!NOTE]
    > ASP.NET MVC 3 中引入了 Razor 语法。 其目标是最大程度地减少文件中所需的字符和击键数量，从而实现快速、流畅的编码工作流。 Razor 利用现有C#的/VB （或其他）语言技能，并提供了一个模板标记语法，可实现出色的 HTML 构造工作流。
4. 按**F5**运行解决方案并查看续订的模板。 您可以查看以下功能：

    1. **新式模板**

        这些模板已续订，提供了更新式的样式。

        ![ASP.NET MVC 4 改变模板](aspnet-mvc-4-fundamentals/_static/image38.png "ASP.NET MVC 4 改变模板")

        *ASP.NET MVC 4 改变模板*
    2. **自适应呈现**

        查看调整浏览器窗口的大小，并注意页面布局如何动态适应新的窗口大小。 这些模板使用自适应呈现技术在桌面和移动平台中正确呈现，无需进行任何自定义。

        ![不同浏览器大小的 ASP.NET MVC 4 项目模板](aspnet-mvc-4-fundamentals/_static/image39.png "不同浏览器大小的 ASP.NET MVC 4 项目模板")

        *不同浏览器大小的 ASP.NET MVC 4 项目模板*
5. 关闭浏览器以停止调试器并返回到 Visual Studio。
6. 现在，你可以浏览解决方案并查看项目模板中 ASP.NET MVC 4 引入的一些新功能。

    ![ASP.NET MVC4-应用程序-项目-模板](aspnet-mvc-4-fundamentals/_static/image40.png "ASP.NET MVC 4 Internet 应用程序项目模板")

    *ASP.NET MVC 4 Internet 应用程序项目模板*

   1. **HTML5 标记**

       浏览模板视图以找出新的主题标记，例如，在**主**文件夹内打开**About。**

       ![新模板，使用 Razor 和 HTML5 标记](aspnet-mvc-4-fundamentals/_static/image41.png "新模板，使用 Razor 和 HTML5 标记")

       *新模板，使用 Razor 和 HTML5 标记*
   2. **包括 JavaScript 库**

      1. **jquery**： jquery 简化了 HTML 文档遍历、事件处理、动画处理和 Ajax 交互。
      2. **JQUERY UI**：此库为基于 JQuery JavaScript 库的底层交互和动画、高级效果和 themeable 小组件提供抽象。

         > [!NOTE]
         > 可以在[[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)中了解 jQuery 和 jquery UI。
      3. **KnockoutJS**： ASP.NET MVC 4 默认模板现在包括**KnockoutJS**，这是一个 javascript MVVM 框架，可让你使用 JavaScript 和 HTML 创建丰富且响应迅速的 web 应用程序。 与 ASP.NET MVC 3 一样，jQuery 和 jQuery UI 库也包含在 ASP.NET MVC 4 中。

          > [!NOTE]
          > 可在以下链接中获取有关 KnockOutJS 库的详细信息： [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)。
      4. **Modernizr**：此库自动运行，在使用 HTML5 和 CSS3 技术时，使你的网站与旧版浏览器兼容。

          > [!NOTE]
          > 可在以下链接中获取有关 Modernizr 库的详细信息： [http://www.modernizr.com/](http://www.modernizr.com/)。
   3. **解决方案中包含的 SimpleMembership**

       SimpleMembership 已被设计为以前的 ASP.NET 角色和成员资格提供程序系统的替换。 它具有许多新功能，使开发人员能够更轻松地以更灵活的方式保护网页。

       Internet 模板已经设置了几项来集成 SimpleMembership，例如，AccountController 准备使用 OAuthWebSecurity （适用于 OAuth 帐户注册、登录、管理等）和 Web 安全。

       ![解决方案中包含的 SimpleMembership](aspnet-mvc-4-fundamentals/_static/image42.png "解决方案中包含的 SimpleMembership")

       *解决方案中包含的 SimpleMembership*

       > [!NOTE]
       > 在 MSDN 中查找有关[OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx)的详细信息。

> [!NOTE]
> 此外，还可以在[附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序的](#AppendixB)Microsoft Azure 网站上部署此应用程序。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>摘要

完成此动手实验后，你已了解 ASP.NET MVC 的基础知识：

- MVC 应用程序的核心元素及其交互方式
- 如何创建 ASP.NET MVC 应用程序
- 如何添加和配置控制器来处理通过 URL 和 querystring 传递的参数
- 如何添加布局母版页，为常见 HTML 内容设置模板; 用于增强外观的样式表和用于显示 HTML 内容的视图模板
- 如何使用 ViewModel 模式将属性传递给视图模板以显示动态信息
- 如何使用传递给视图模板中的控制器的参数
- 如何将链接添加到 ASP.NET MVC 应用程序内的页面
- 如何在视图中添加和使用动态属性
- ASP.NET MVC 4 项目模板中的增强功能

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 A：安装 Visual Studio Express 2012 for Web

您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。 以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。

1. 请参阅[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](aspnet-mvc-4-fundamentals/_static/image44.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-fundamentals/_static/image45.png)

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](aspnet-mvc-4-fundamentals/_static/image46.png)

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-fundamentals/_static/image47.png)

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

    ![登录到 Windows Azure 门户](aspnet-mvc-4-fundamentals/_static/image48.png "登录到 Microsoft Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击命令栏上的 "**新建**"。

    ![创建新网站](aspnet-mvc-4-fundamentals/_static/image49.png "创建新网站")

    *创建新网站*
3. 单击 "**计算** | **网站**"。 然后选择 "**快速创建**" 选项。 为新网站提供可用 URL，并单击 "**创建**网站"。

    > [!NOTE]
    > Windows Azure 网站是在云中运行的 Web 应用程序的宿主，你可以控制和管理这些应用程序。 使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Microsoft Azure 网站。 它不包括设置数据库的步骤。

    ![使用 "快速创建" 创建新网站](aspnet-mvc-4-fundamentals/_static/image50.png "使用“快速创建”创建新网站")

    *使用 "快速创建" 创建新网站*
4. 请**等到新网站创建完毕。**
5. 创建网站后，单击 " **URL** " 列下的链接。 检查新网站是否正常工作。

    ![浏览到新网站](aspnet-mvc-4-fundamentals/_static/image51.png "浏览到新网站")

    *浏览到新网站*

    ![网站正在运行](aspnet-mvc-4-fundamentals/_static/image52.png "网站正在运行")

    *网站正在运行*
6. 返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。

    ![打开网站管理页](aspnet-mvc-4-fundamentals/_static/image53.png "打开网站管理页")

    *打开网站管理页*
7. 在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。

    > [!NOTE]
    > *发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 microsoft Azure 网站所需的所有信息。 发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 microsoft Azure 网站。

    ![下载网站发布配置文件](aspnet-mvc-4-fundamentals/_static/image54.png "下载网站发布配置文件")

    *下载网站发布配置文件*
8. 将发布配置文件下载到已知位置。 在本练习中，您将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Microsoft Azure 网站。

    ![正在保存发布配置文件](aspnet-mvc-4-fundamentals/_static/image55.png "正在保存发布配置文件")

    *正在保存发布配置文件*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。 如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。

1. 你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。 可以在 Microsoft Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 MICROSOFT Azure 管理门户中查看 sql 数据库服务器。 如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。 记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。 请不要创建数据库，因为它将在后面的阶段创建。

    ![SQL 数据库服务器仪表板](aspnet-mvc-4-fundamentals/_static/image56.png "SQL 数据库服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。 为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 中选择 IP 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框，然后单击 "![添加-客户端-IP 地址-](aspnet-mvc-4-fundamentals/_static/image57.png)" 按钮。

    ![添加客户端 IP 地址](aspnet-mvc-4-fundamentals/_static/image58.png)

    *添加客户端 IP 地址*
3. 将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。

    ![确认更改](aspnet-mvc-4-fundamentals/_static/image59.png)

    *确认更改*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序

1. 返回到 ASP.NET MVC 4 解决方案。 在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。

    ![发布应用程序](aspnet-mvc-4-fundamentals/_static/image60.png "发布应用程序")

    *发布网站*
2. 导入您在第一个任务中保存的发布配置文件。

    ![导入发布配置文件](aspnet-mvc-4-fundamentals/_static/image61.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击 "**验证连接**"。 验证完成后，单击 "**下一步**"。

    > [!NOTE]
    > 验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。

    ![正在验证连接](aspnet-mvc-4-fundamentals/_static/image62.png "正在验证连接")

    *正在验证连接*
4. 在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。

    ![Web 部署配置](aspnet-mvc-4-fundamentals/_static/image63.png "Web 部署配置")

    *Web 部署配置*
5. 按如下所示配置数据库连接：

   - 在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。
   - 在 "**用户名**" 中键入服务器管理员登录名。
   - 在 "**密码**" 中键入服务器管理员登录密码。
   - 键入新的数据库名称，例如： *MVC4SampleDB*。

     ![正在配置目标连接字符串](aspnet-mvc-4-fundamentals/_static/image64.png "正在配置目标连接字符串")

     *正在配置目标连接字符串*
6. 然后单击 **“确定”** 。 系统提示创建数据库时，单击 **"是"** 。

    ![创建数据库](aspnet-mvc-4-fundamentals/_static/image65.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。 再单击 **“下一步”** 。

    ![指向 SQL 数据库的连接字符串](aspnet-mvc-4-fundamentals/_static/image66.png "指向 SQL 数据库的连接字符串")

    *指向 SQL 数据库的连接字符串*
8. 在 "**预览**" 页上，单击 "**发布**"。

    ![发布 web 应用程序](aspnet-mvc-4-fundamentals/_static/image67.png "发布 web 应用程序")

    *发布 web 应用程序*
9. 发布过程完成后，您的默认浏览器将打开已发布的网站。

    ![发布到 Windows Azure 的应用程序](aspnet-mvc-4-fundamentals/_static/image68.png "发布到 Windows Azure 的应用程序")

    *发布到 Windows Azure 的应用程序*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附录 C：使用代码片段

使用代码片段，您可以随时获得所需的全部代码。 实验室文档将告诉你何时可以使用它们，如下图所示。

![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-fundamentals/_static/image69.png "使用 Visual Studio code 代码段将代码插入到项目中")

*使用 Visual Studio code 代码段将代码插入到项目中*

***使用键盘添加代码片段（C#仅限）***

1. 将光标放在要插入代码的位置。
2. 开始键入代码片段名称（不含空格或连字符）。
3. 请注意，IntelliSense 显示匹配的代码段名称。
4. 选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。
5. 按 Tab 键两次，将代码段插入到光标位置。

![开始键入代码片段名称](aspnet-mvc-4-fundamentals/_static/image70.png "开始键入代码片段名称")

*开始键入代码片段名称*

![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-fundamentals/_static/image71.png "按 Tab 键以选择突出显示的代码段")

*按 Tab 键以选择突出显示的代码段*

![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-fundamentals/_static/image72.png "再次按 Tab 键，代码片段将展开")

*再次按 Tab 键，代码片段将展开*

***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2. 右键单击要插入代码片段的位置。

1. 选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。
2. 通过单击从列表中选择相关的代码片段。

![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-fundamentals/_static/image73.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")

*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*

![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-fundamentals/_static/image74.png "通过单击从列表中选择相关的代码片段")

*通过单击从列表中选择相关的代码片段*
