---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: ASP.NET MVC 4 自定义操作筛选器 |Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 提供操作筛选器，用于在调用操作方法之前或之后执行筛选逻辑。 操作筛选器是自定义属性。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468176"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a>ASP.NET MVC 4 自定义操作筛选器

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 提供操作筛选器，用于在调用操作方法之前或之后执行筛选逻辑。 操作筛选器是自定义属性，可提供声明性方法，以将操作前和操作后行为添加到控制器的操作方法。

在此动手实验中，你将在 MvcMusicStore 解决方案中创建自定义操作筛选器属性，以捕获控制器的请求并将站点的活动记录到数据库表中。 你可以通过注入到任何控制器或操作来添加日志筛选器。 最后，您将看到显示访问者列表的日志视图。

此动手实验假设你具有**ASP.NET MVC**的基本知识。 如果你之前未使用过**ASP.NET mvc** ，则建议你浏览**ASP.NET mvc 4 基础**动手实验。

> [!NOTE]
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中，可从[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)获取。 [ASP.NET MVC 4 自定义操作筛选器](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters)中提供了此实验室特定的项目。

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在此动手实验中，您将学习如何：

- 创建自定义操作筛选器特性来扩展筛选功能
- 通过注入到特定级别应用自定义筛选器属性
- 全局注册自定义操作筛选器

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

1. [练习1：记录操作](#Exercise1)
2. [练习2：管理多个操作筛选器](#Exercise2)

完成本实验的估计时间： **30 分钟**。

> [!NOTE]
> 每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。 如果需要更多帮助，请使用此解决方案作为指导。

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a>练习1：记录操作

在此练习中，您将学习如何使用 ASP.NET MVC 4 筛选器提供程序创建自定义操作日志筛选器。 出于此目的，你需要将日志记录筛选器应用到 MusicStore 站点，该站点将记录所选控制器中的所有活动。

筛选器将扩展**ActionFilterAttributeClass**并重写**OnActionExecuting**方法以捕获每个请求，然后执行日志记录操作。 ASP.NET MVC **ActionExecutingContext**类将提供有关 HTTP 请求、执行方法、结果和参数的上下文信息 **。**

> [!NOTE]
> ASP.NET MVC 4 还具有可在不创建自定义筛选器的情况下使用的默认筛选器提供程序。 ASP.NET MVC 4 提供以下类型的筛选器：
> 
> - **授权**筛选器，用于做出有关是否执行操作方法的安全决策，如执行身份验证或验证请求的属性。
> - **操作**筛选器，它将操作方法执行打包。 此筛选器可以执行其他处理，如向操作方法提供额外数据、检查返回值或取消操作方法的执行
> - **结果**筛选器，用于包装 ActionResult 对象的执行。 此筛选器可以对结果执行其他处理，如修改 HTTP 响应。
> - **异常**筛选器，如果在操作方法中的某个位置引发了未经处理的异常，则将执行该筛选器，从授权筛选器开始，到结果的执行结束。 异常筛选器可用于执行诸如日志记录或显示错误页之类的任务。
> 
> 有关筛选器提供程序的详细信息，请访问此 MSDN 链接：（[https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)）。

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a>关于 MVC 音乐商店应用程序日志记录功能

此音乐应用商店解决方案有一个新的用于站点日志记录的数据模型表**ActionLog**，其中包含以下字段：收到请求的控制器的名称，称为 "操作"、"客户端 IP" 和 "时间戳"。

![数据模型。ActionLog 表。](aspnet-mvc-4-custom-action-filters/_static/image1.png "数据模型。ActionLog 表。")

*数据模型-ActionLog 表*

此解决方案提供了可在**MvcMusicStores/Views/ActionLog**上找到的操作日志的 ASP.NET MVC 视图：

![操作日志视图](aspnet-mvc-4-custom-action-filters/_static/image2.png "操作日志视图")

*操作日志视图*

使用此给定结构，所有工作都将重点放在中断控制器的请求并使用自定义筛选执行日志记录。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a>任务 1-创建自定义筛选器以捕获控制器的请求

在此任务中，您将创建一个将包含日志记录逻辑的自定义筛选器属性类。 出于此目的，你将扩展 ASP.NET MVC **ActionFilterAttribute**类并实现接口**IActionFilter**。

> [!NOTE]
> **ActionFilterAttribute**是所有属性筛选器的基类。 它提供以下方法，以便在控制器操作的执行前后执行特定逻辑：
> 
> - **OnActionExecuting**（ActionExecutingContext filterContext）：在调用操作方法之前。
> - **OnActionExecuted**（ActionExecutedContext filterContext）：调用操作方法并在执行结果之前（视图呈现之前）。
> - **OnResultExecuting**（ResultExecutingContext filterContext）：在执行结果之前（视图呈现之前）。
> - **OnResultExecuted**（ResultExecutedContext filterContext）：执行结果后（呈现视图后）。
> 
> 通过将这些方法中的任何方法重写到派生类中，你可以执行自己的筛选代码。

1. 打开位于 **\Source\Ex01-LoggingActions\Begin**文件夹的 "**开始**" 解决方案。

   1. 在继续之前，你将需要下载某些缺少的 NuGet 包。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
      > 
      > 有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 将新C#类添加到**Filters**文件夹，并将其命名为*CustomActionFilter.cs*。 此文件夹将存储所有自定义筛选器。
3. 打开**CustomActionFilter.cs** ，并添加对**system.web**和**MvcMusicStore**命名空间的引用：

    （代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1-CustomActionFilterNamespaces*）

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. 从**ActionFilterAttribute**继承**CustomActionFilter**类，然后使**CustomActionFilter**类实现**IActionFilter**接口。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. 使**CustomActionFilter**类重写方法**OnActionExecuting** ，并添加必要的逻辑来记录筛选器的执行。 为此，请在**CustomActionFilter**类中添加以下突出显示的代码。

    （代码段- *ASP.NET MVC 4 自定义操作筛选器-Ex1-LoggingActions*）

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > **OnActionExecuting**方法正在使用**实体框架**来添加新的 ActionLog 寄存器。 它使用来自**filterContext**的上下文信息创建并填充新的实体实例。
    > 
    > 可在[msdn](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx)上阅读有关**ControllerContext**类的详细信息。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a>任务 2-将代码侦听器注入到存储控制器类中

在此任务中，你将通过将自定义筛选器注入到将记录的所有控制器类和控制器操作来添加该筛选器。 对于本练习，商店控制器类将有一个日志。

调用注入的元素时，将运行来自**ActionLogFilterAttribute**自定义筛选器的方法**OnActionExecuting** 。

还可以截获特定控制器方法。

1. 在**MvcMusicStore\Controllers**中打开**StoreController** ，并添加对**筛选器**命名空间的引用：

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. 通过在类声明之前添加 **[CustomActionFilter]** 特性，将自定义筛选器**CustomActionFilter**注入到**StoreController**类中。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > 如果将筛选器注入控制器类中，则还会插入其所有操作。 如果要仅对一组操作应用筛选器，则必须将 **[CustomActionFilter]** 注入到其中的每一个操作：
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，您将测试日志记录筛选器是否正常工作。 您将启动该应用程序并访问应用商店，然后您将检查记录的活动。

1. 按 **F5** 运行该应用程序。
2. 浏览到 **/ActionLog**以查看日志视图初始状态：

    ![页面活动之前的日志跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image3.png "页面活动之前的日志跟踪器状态")

    *页面活动之前的日志跟踪器状态*

   > [!NOTE]
   > 默认情况下，它将始终显示检索菜单的现有流派时生成的一项。
   > 
   > 为简单起见，我们将在每次运行应用程序时清理**ActionLog**表，因此它只显示每个特定任务验证的日志。
   > 
   > 你可能需要从会话中删除以下代码 **\_Start**方法（在**global.asax**类中），以便为在存储控制器中执行的所有操作保存历史日志。
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. 单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。
4. 浏览到 **/ActionLog** ，如果日志为空，则按**F5**刷新页面。 检查是否跟踪了您的访问：

    ![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image4.png "已记录活动的操作日志")

    *已记录活动的操作日志*

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a>练习2：管理多个操作筛选器

在本练习中，您将向 StoreController 类添加另一个自定义操作筛选器，并定义两个筛选器的执行顺序。 然后，您将更新代码以全局注册筛选器。

定义筛选器的执行顺序时，需要考虑不同的选项。 例如，Order 属性和筛选器的作用域：

你可以为每个筛选器定义一个**范围**，例如，你可以将所有操作筛选器的范围限定为在**控制器范围**内运行，并将所有授权筛选器都指定为在**全局范围**内运行。 作用域具有定义的执行顺序。

此外，每个操作筛选器都具有 Order 属性，该属性用于确定筛选器范围内的执行顺序。

有关自定义操作筛选器执行顺序的详细信息，请访问此 MSDN 文章：（[https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)）。

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a>任务1：创建新的自定义操作筛选器

在此任务中，您将创建一个新的自定义操作筛选器以注入到 StoreController 类中，了解如何管理筛选器的执行顺序。

1. 打开位于 **\Source\Ex02-ManagingMultipleActionFilters\Begin**文件夹的 "**开始**" 解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

    1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
    2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
    3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

        > [!NOTE]
        > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
        > 
        > 有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 将新C#类添加到**Filters**文件夹，并将其命名为*MyNewCustomActionFilter.cs*
3. 打开**MyNewCustomActionFilter.cs** ，并添加对**system.web**和**MvcMusicStore**命名空间的引用：

    （代码段- *ASP.NET MVC 4 自定义操作筛选器-buildingappswithcachingservice-ex2-getproducts latency-cs-MyNewCustomActionFilterNamespaces*）

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. 将默认类声明替换为以下代码。

    （代码段- *ASP.NET MVC 4 自定义操作筛选器-buildingappswithcachingservice-ex2-getproducts latency-cs-MyNewCustomActionFilterClass*）

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > 此自定义操作筛选器与您在上一练习中创建的筛选器几乎相同。 主要区别在于它具有使用此新类名称更新 *&quot;属性记录的&quot;* ，以标识注册了日志的筛选器。

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a>任务2：将新的代码侦听器注入到 StoreController 类

在此任务中，将新的自定义筛选器添加到 StoreController 类中，并运行解决方案来验证这两个筛选器如何协同工作。

1. 打开位于**MvcMusicStore\Controllers**的**StoreController**类，并将新的自定义筛选器**MyNewCustomActionFilter**注入**StoreController**类，如下面的代码所示。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. 现在，运行应用程序，了解这两个自定义操作筛选器的工作原理。 为此，请按**F5**并等待，直到应用程序启动。
3. 浏览到 **/ActionLog**以查看日志视图的初始状态。

    ![页面活动之前的日志跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image5.png "页面活动之前的日志跟踪器状态")

    *页面活动之前的日志跟踪器状态*
4. 单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。
5. 检查此时间;您的访问被跟踪了两次：一次针对您在**StorageController**类中添加的每个自定义操作筛选器。

    ![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image6.png "已记录活动的操作日志")

    *已记录活动的操作日志*
6. 关闭浏览器。

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a>任务3：管理筛选器排序

在此任务中，您将学习如何使用 Order 属性来管理筛选器的执行顺序。

1. 打开位于**MvcMusicStore\Controllers**的**StoreController**类，并在这两个筛选器中指定**Order**属性，如下所示。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. 现在，请根据筛选器的 Order 属性值来验证执行筛选器的方式。 你会发现具有最小顺序值（**CustomActionFilter**）的筛选器是执行的第一个筛选器。 按**F5**并等待，直到应用程序启动。
3. 浏览到 **/ActionLog**以查看日志视图的初始状态。

    ![页面活动之前的日志跟踪器状态](aspnet-mvc-4-custom-action-filters/_static/image7.png "页面活动之前的日志跟踪器状态")

    *页面活动之前的日志跟踪器状态*
4. 单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。
5. 检查这一次是否跟踪了你的访问是否按筛选器的订单值： **CustomActionFilter** logs ' 排序。

    ![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image8.png "已记录活动的操作日志")

    *已记录活动的操作日志*
6. 现在，您将更新筛选器的 order 值，并验证日志记录顺序如何变化。 在**StoreController**类中，更新筛选器的 Order 值，如下所示。

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. 按**F5**再次运行该应用程序。
8. 单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。
9. 检查这一次， **MyNewCustomActionFilter**筛选器创建的日志会首先出现。

    ![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image9.png "已记录活动的操作日志")

    *已记录活动的操作日志*

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a>任务4：全局注册筛选器

在此任务中，你将更新解决方案，以将新筛选器（**MyNewCustomActionFilter**）注册为全局筛选器。 执行此操作后，在应用程序中执行的所有操作都将触发应用程序中执行的所有操作，而不仅是在上一个任务中的 StoreController 中执行。

1. 在**StoreController**类中，删除 [ **MyNewCustomActionFilter]** 属性和 **[CustomActionFilter]** 中的 order 属性。 该元素应类似于：

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. 打开**global.asax**文件，并找到**应用程序\_Start**方法。 请注意，每次应用程序启动时，都是通过调用**filterconfig.math**类中的**RegisterGlobalFilters**方法来注册全局筛选器。

    ![在 global.asax 中注册全局筛选器](aspnet-mvc-4-custom-action-filters/_static/image10.png "在 global.asax 中注册全局筛选器")

    *在 global.asax 中注册全局筛选器*
3. 在**应用\_启动**文件夹内打开**FilterConfig.cs**文件。
4. 使用 System.web 添加对的引用;使用 MvcMusicStore;名称.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. Update **RegisterGlobalFilters**方法添加您的自定义筛选器。 为此，请添加突出显示的代码：

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. 按 F5 运行应用程序。
7. 单击菜单中的某个**流派**，然后在其中执行一些操作，例如浏览可用的唱片集。
8. 检查现在 **[MyNewCustomActionFilter]** 是否在 HomeController 和 ActionLogController 中注入。

    ![已记录活动的操作日志](aspnet-mvc-4-custom-action-filters/_static/image11.png "已记录活动的操作日志")

    *已记录全局活动的操作日志*

> [!NOTE]
> 此外，还可以在[附录 B：使用 Web 部署发布 ASP.NET MVC 4 应用程序的](#AppendixB)Microsoft Azure 网站上部署此应用程序。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>摘要

完成此动手实验后，你已了解如何扩展操作筛选器以执行自定义操作。 还了解了如何将任何筛选器注入到页面控制器。 使用了以下概念：

- 如何通过 ASP.NET MVC ActionFilterAttribute 类创建自定义操作筛选器
- 如何将筛选器注入 ASP.NET MVC 控制器
- 如何使用 Order 属性管理筛选排序
- 如何全局注册筛选器

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 A：安装 Visual Studio Express 2012 for Web

您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。 以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。

1. 转到 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-custom-action-filters/_static/image16.png)

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

    ![登录到 Windows Azure 门户](aspnet-mvc-4-custom-action-filters/_static/image17.png "登录到 Microsoft Azure 门户")

    *登录到 Windows Azure 管理门户*
2. 单击命令栏上的 "**新建**"。

    ![创建新网站](aspnet-mvc-4-custom-action-filters/_static/image18.png "创建新网站")

    *创建新网站*
3. 单击 "**计算** | **网站**"。 然后选择 "**快速创建**" 选项。 为新网站提供可用 URL，并单击 "**创建**网站"。

    > [!NOTE]
    > Windows Azure 网站是在云中运行的 Web 应用程序的宿主，你可以控制和管理这些应用程序。 使用 "快速创建" 选项，可以从门户外部将已完成的 web 应用程序部署到 Microsoft Azure 网站。 它不包括设置数据库的步骤。

    ![使用 "快速创建" 创建新网站](aspnet-mvc-4-custom-action-filters/_static/image19.png "使用“快速创建”创建新网站")

    *使用 "快速创建" 创建新网站*
4. 请**等到新网站创建完毕。**
5. 创建网站后，单击 " **URL** " 列下的链接。 检查新网站是否正常工作。

    ![浏览到新网站](aspnet-mvc-4-custom-action-filters/_static/image20.png "浏览到新网站")

    *浏览到新网站*

    ![网站正在运行](aspnet-mvc-4-custom-action-filters/_static/image21.png "网站正在运行")

    *网站正在运行*
6. 返回到门户，并在 "**名称**" 列下单击网站的名称以显示管理页面。

    ![打开网站管理页](aspnet-mvc-4-custom-action-filters/_static/image22.png "打开网站管理页")

    *打开网站管理页*
7. 在 "**仪表板**" 页的 "**速览**" 部分下，单击 "**下载发布配置文件**" 链接。

    > [!NOTE]
    > *发布配置文件*包含为每个已启用的发布方法将 web 应用程序发布到 microsoft Azure 网站所需的所有信息。 发布配置文件包含有连接到并且验证该发布方法启用的每个端点所需的 URL、用户凭据和数据库字符串。 **Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支持读取发布配置文件，以便自动配置这些程序以将 Web 应用程序发布到 microsoft Azure 网站。

    ![下载网站发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image23.png "下载网站发布配置文件")

    *下载网站发布配置文件*
8. 将发布配置文件下载到已知位置。 在本练习中，您将了解如何使用此文件从 Visual Studio 将 web 应用程序发布到 Microsoft Azure 网站。

    ![正在保存发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image24.png "正在保存发布配置文件")

    *正在保存发布配置文件*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>任务 2-配置数据库服务器

如果应用程序使用 SQL Server 数据库，则需要创建 SQL 数据库服务器。 如果要部署不使用 SQL Server 的简单应用程序，则可以跳过此任务。

1. 你将需要一个用于存储应用程序数据库的 SQL 数据库服务器。 可以在 Microsoft Azure 管理门户中的**sql** **数据库 | server** | **服务器的仪表板**上的 MICROSOFT Azure 管理门户中查看 sql 数据库服务器。 如果尚未创建服务器，可以使用命令栏上的 "**添加**" 按钮创建一个服务器。 记下**服务器名称和 URL、管理员登录名和密码**，因为你将在后续任务中使用它们。 请不要创建数据库，因为它将在后面的阶段创建。

    ![SQL 数据库服务器仪表板](aspnet-mvc-4-custom-action-filters/_static/image25.png "SQL 数据库服务器仪表板")

    *SQL 数据库服务器仪表板*
2. 在下一任务中，您将从 Visual Studio 测试数据库连接，因此，需要在服务器的**允许 IP 地址**列表中包含本地 ip 地址。 为此，请单击 "**配置**"，从 "**当前客户端 IP 地址**" 中选择 IP 地址，并将其粘贴到 "**起始 Ip 地址**" 和 "**结束 ip 地址**" 文本框，然后单击 "![添加-客户端-IP 地址-](aspnet-mvc-4-custom-action-filters/_static/image26.png)" 按钮。

    ![添加客户端 IP 地址](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    *添加客户端 IP 地址*
3. 将**客户端 Ip 地址**添加到 "允许的 IP 地址" 列表中后，单击 "**保存**" 以确认更改。

    ![确认更改](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    *确认更改*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>任务 3-使用 Web 部署发布 ASP.NET MVC 4 应用程序

1. 返回到 ASP.NET MVC 4 解决方案。 在**解决方案资源管理器**中，右键单击网站项目，然后选择 "**发布**"。

    ![发布应用程序](aspnet-mvc-4-custom-action-filters/_static/image29.png "发布应用程序")

    *发布网站*
2. 导入您在第一个任务中保存的发布配置文件。

    ![导入发布配置文件](aspnet-mvc-4-custom-action-filters/_static/image30.png "导入发布配置文件")

    *导入发布配置文件*
3. 单击 "**验证连接**"。 验证完成后，单击 "**下一步**"。

    > [!NOTE]
    > 验证完成后，"验证连接" 按钮旁边会出现一个绿色的复选标记。

    ![正在验证连接](aspnet-mvc-4-custom-action-filters/_static/image31.png "正在验证连接")

    *正在验证连接*
4. 在 "**设置**" 页的 "**数据库**" 部分下，单击数据库连接的文本框旁边的按钮（即**DefaultConnection**）。

    ![Web 部署配置](aspnet-mvc-4-custom-action-filters/_static/image32.png "Web 部署配置")

    *Web 部署配置*
5. 按如下所示配置数据库连接：

   - 在 "**服务器名称**" 中，键入您的 SQL 数据库服务器 URL，使用*tcp：* prefix。
   - 在 "**用户名**" 中键入服务器管理员登录名。
   - 在 "**密码**" 中键入服务器管理员登录密码。
   - 键入新的数据库名称。

     ![正在配置目标连接字符串](aspnet-mvc-4-custom-action-filters/_static/image33.png "正在配置目标连接字符串")

     *正在配置目标连接字符串*
6. 然后单击 **“确定”** 。 系统提示创建数据库时，单击 **"是"** 。

    ![创建数据库](aspnet-mvc-4-custom-action-filters/_static/image34.png "创建数据库字符串")

    *创建数据库*
7. 将用于连接到 Windows Azure 中的 SQL 数据库的连接字符串显示在 "默认连接" 文本框中。 再单击 **“下一步”** 。

    ![指向 SQL 数据库的连接字符串](aspnet-mvc-4-custom-action-filters/_static/image35.png "指向 SQL 数据库的连接字符串")

    *指向 SQL 数据库的连接字符串*
8. 在 "**预览**" 页上，单击 "**发布**"。

    ![发布 web 应用程序](aspnet-mvc-4-custom-action-filters/_static/image36.png "发布 web 应用程序")

    *发布 web 应用程序*
9. 发布过程完成后，您的默认浏览器将打开已发布的网站。

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>附录 C：使用代码片段

使用代码片段，您可以随时获得所需的全部代码。 实验室文档将告诉你何时可以使用它们，如下图所示。

![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-custom-action-filters/_static/image37.png "使用 Visual Studio code 代码段将代码插入到项目中")

*使用 Visual Studio code 代码段将代码插入到项目中*

***使用键盘添加代码片段（C#仅限）***

1. 将光标放在要插入代码的位置。
2. 开始键入代码片段名称（不含空格或连字符）。
3. 请注意，IntelliSense 显示匹配的代码段名称。
4. 选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。
5. 按 Tab 键两次，将代码段插入到光标位置。

![开始键入代码片段名称](aspnet-mvc-4-custom-action-filters/_static/image38.png "开始键入代码片段名称")

*开始键入代码片段名称*

![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-custom-action-filters/_static/image39.png "按 Tab 键以选择突出显示的代码段")

*按 Tab 键以选择突出显示的代码段*

![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-custom-action-filters/_static/image40.png "再次按 Tab 键，代码片段将展开")

*再次按 Tab 键，代码片段将展开*

***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2. 右键单击要插入代码片段的位置。

1. 选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。
2. 通过单击从列表中选择相关的代码片段。

![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-custom-action-filters/_static/image41.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")

*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*

![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-custom-action-filters/_static/image42.png "通过单击从列表中选择相关的代码片段")

*通过单击从列表中选择相关的代码片段*
