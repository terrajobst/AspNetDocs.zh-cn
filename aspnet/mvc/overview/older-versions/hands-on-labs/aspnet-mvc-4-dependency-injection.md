---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: ASP.NET MVC 4 依赖关系注入 |Microsoft Docs
author: rick-anderson
description: 注意：此动手实验假设你具有 ASP.NET MVC 和 ASP.NET MVC 4 筛选器的基本知识。 如果以前未使用过 ASP.NET MVC 4 筛选器，我们将 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451820"
---
# <a name="aspnet-mvc-4-dependency-injection"></a>ASP.NET MVC 4 依赖项注入

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

此动手实验假设你具有**ASP.NET mvc**和**ASP.NET mvc 4 筛选器**的基本知识。 如果你之前未使用过**ASP.NET mvc 4 筛选器**，我们建议你使用**ASP.NET Mvc 自定义操作筛选器**动手实验。

> [!NOTE]
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中，可从[Microsoft-Web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)获取。 [ASP.NET MVC 4 依赖关系注入](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection)中提供了此实验室特定的项目。

在**面向对象的编程**范例中，对象在存在参与者和使用者的协作模型中协同工作。 当然，这种通信模型会生成对象与组件之间的依赖关系，在复杂性增加时变得难以管理。

![类依赖项和模型复杂性](aspnet-mvc-4-dependency-injection/_static/image1.png "类依赖项和模型复杂性")

*类依赖项和模型复杂性*

你可能听说过**工厂模式**以及接口和实现之间的分离使用服务，其中客户端对象通常负责服务定位。

依赖关系注入模式是一种特定的控制反转实现。 **控制反转（IoC）** 表示对象不会创建其他对象，这些对象依赖于它们来完成工作。 相反，它们从外部源（例如 xml 配置文件）获取所需的对象。

**依赖关系注入（DI）** 表示在没有对象干预的情况下执行此操作，通常由传递构造函数参数和设置属性的框架组件完成。

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>依赖关系注入（DI）设计模式

从较高层次来看，依赖关系注入的目标是客户端类（例如*高尔夫选手*）需要满足接口的某些内容（例如*IClub*）。 它并不关心具体类型是什么（例如 *，WoodClub、IronClub、WedgeClub*或*PutterClub*），而是希望别人处理该类型（例如，一个好的*caddy*）。 ASP.NET MVC 中的依赖关系解析程序可以让你在其他位置（例如，容器或*梅花包*）注册依赖逻辑。

![依赖关系注入关系图](aspnet-mvc-4-dependency-injection/_static/image2.png "依赖关系注入图")

*依赖关系注入-高尔夫类比*

使用依赖关系注入模式和控制反转的优点如下：

- 减少类耦合
- 增加代码重用
- 提高代码可维护性
- 改进应用程序测试

> [!NOTE]
> 依赖关系注入有时与抽象工厂设计模式比较，但这两种方法之间略有不同。 DI 具有一个框架，可用于通过调用工厂和注册的服务来解决依赖项。

现在，你已了解依赖关系注入模式，你将在本实验室中学习如何在 ASP.NET MVC 4 中应用此模式。 你将开始在**控制器**中使用依赖关系注入，以包含数据库访问服务。 接下来，您将向**视图**应用依赖关系注入，以使用服务并显示信息。 最后，将 DI 扩展到 ASP.NET MVC 4 筛选器，在解决方案中注入自定义操作筛选器。

在此动手实验中，您将学习如何：

- 将 ASP.NET MVC 4 与 Unity 集成，以便使用 NuGet 包进行依赖关系注入
- 在 ASP.NET MVC 控制器中使用依赖关系注入
- 在 ASP.NET MVC 视图中使用依赖关系注入
- 在 ASP.NET MVC 操作筛选器中使用依赖关系注入

> [!NOTE]
> 此实验室使用 Mvc3 NuGet 包进行依赖关系解析，但可以调整任何依赖关系注入框架，使其与 ASP.NET MVC 4 结合使用。

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

此动手实验包括以下练习：

1. [练习1：注入控制器](#Exercise1)
2. [练习2：注入视图](#Exercise2)
3. [练习3：注入筛选器](#Exercise3)

> [!NOTE]
> 每个练习都带有一个**结束**文件夹，其中包含在完成练习后应获得的结果解决方案。 如果需要更多帮助，请使用此解决方案作为指导。

完成本实验的估计时间： **30 分钟**。

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>练习1：注入控制器

在此练习中，您将学习如何通过使用 NuGet 包集成 Unity，在 ASP.NET MVC 控制器中使用依赖关系注入。 出于此原因，你将在 MvcMusicStore 控制器中包含服务，以将逻辑与数据访问分隔开来。 这些服务将在控制器构造函数中创建新的依赖关系，该依赖关系注入将通过**Unity**的帮助来解决。

此方法将向你展示如何生成更少耦合的应用程序，这些应用程序更灵活、更易于维护和测试。 你还将了解如何将 ASP.NET MVC 与 Unity 集成。

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>关于 StoreManager 服务

开始解决方案中提供的 MVC 音乐商店现在包含管理名为**StoreService**的存储控制器数据的服务。 下面你会发现存储服务实现。 请注意，所有方法都返回模型实体。

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

开始解决方案的**StoreController**现在使用**StoreService**。 所有数据引用均已从**StoreController**中删除，现在可以修改当前的数据访问接口，而无需更改任何使用**StoreService**的方法。

下面你会发现， **StoreController**实现在类构造函数内与**StoreService**具有依赖关系。

> [!NOTE]
> 本练习中引入的依赖关系与**控制反转**（IoC）有关。
> 
> **StoreController**类构造函数收到**IStoreService**类型参数，这对于从类内部执行服务调用至关重要。 不过， **StoreController**不实现任何控制器必须与 ASP.NET MVC 一起使用的默认构造函数（不带参数）。
> 
> 若要解决依赖关系，控制器必须由抽象工厂创建（一个返回指定类型的任何对象的类）。

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> 当类尝试创建 StoreController 时，如果没有声明无参数的构造函数，则会收到错误。

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>任务 1-运行应用程序

在此任务中，将运行 "开始" 应用程序，该应用程序将服务包含在将数据访问与应用程序逻辑分开的存储控制器中。

运行应用程序时，你将收到一个异常，因为默认情况下控制器服务不作为参数传递：

1. 打开位于**Source\Ex01-Injecting Controller\Begin**的 "**开始**" 解决方案。

   1. 在继续之前，需要下载一些缺少的 NuGet 包。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
2. 按**Ctrl + F5**以运行应用程序而不进行调试。 将收到错误消息，&quot;**没有为此对象定义无参数的构造函数**&quot;：

    ![运行 ASP.NET MVC Begin 应用程序时出错](aspnet-mvc-4-dependency-injection/_static/image3.png "运行 ASP.NET MVC Begin 应用程序时出错")

    *运行 ASP.NET MVC Begin 应用程序时出错*
3. 关闭浏览器。

在以下步骤中，你将使用音乐应用商店解决方案来注入此控制器所需的依赖项。

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>任务 2-包括 Unity 到 MvcMusicStore 解决方案

在此任务中，你将在解决方案中包括**Mvc3** NuGet 包。

> [!NOTE]
> Mvc3 包专为 ASP.NET MVC 3 设计，但它与 ASP.NET MVC 4 完全兼容。
> 
> Unity 是一个轻型的可扩展依赖关系注入容器，它支持实例和类型截取。 它是用于任何类型的 .NET 应用程序的常规用途容器。 它提供了依赖关系注入机制中的所有常见功能，包括：对象创建、通过在运行时通过指定依赖项来抽象要求，以及通过将组件配置推迟到容器来实现灵活性。

1. 在**MvcMusicStore**项目中安装**Mvc3** NuGet 包。 为此，请从 | **其他窗口**的**视图**中打开**包管理器控制台**。
2. 运行以下命令。

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![正在安装 Unity. Mvc3 NuGet 包](aspnet-mvc-4-dependency-injection/_static/image4.png "正在安装 Unity. Mvc3 NuGet 包")

    *正在安装 Unity. Mvc3 NuGet 包*
3. 安装**Mvc3**包后，浏览它自动添加的文件和文件夹，以便简化 Unity 配置。

    ![已安装 Mvc3 包](aspnet-mvc-4-dependency-injection/_static/image5.png "已安装 Mvc3 包")

    *已安装 Mvc3 包*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a>任务 3-在 Global.asax.cs 应用程序中注册 Unity\_开始

在此任务中，你将更新**Global.asax.cs**中的**应用程序\_Start**方法，以调用 Unity 引导程序初始值设定项，然后更新引导程序文件，以注册将用于依赖关系注入的服务和控制器。

1. 现在，你将挂接引导程序，这是用于初始化 Unity 容器和依赖关系解析程序的文件。 为此，请打开**Global.asax.cs** ，并在**应用程序\_Start**方法中添加以下突出显示的代码。

    （代码段- *ASP.NET 依赖关系注入实验室-Ex01-初始化 Unity*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. 打开**Bootstrapper.cs**文件。
3. 包含以下命名空间： **MvcMusicStore**和**MusicStore**。

    （代码段- *ASP.NET 依赖关系注入实验室-Ex01-引导程序添加命名空间*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. 将**BuildUnityContainer**方法的内容替换为以下代码，用于注册商店控制器和存储服务。

    （代码段- *ASP.NET 依赖关系注入实验室-Ex01-注册存储控制器和服务*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在此任务中，你将运行应用程序，以验证它现在可以在包含 Unity 之后加载。

1. 按**F5**运行应用程序，应用程序现在应加载，而不显示任何错误消息。

    ![正在运行具有依赖关系注入的应用程序](aspnet-mvc-4-dependency-injection/_static/image6.png "正在运行具有依赖关系注入的应用程序")

    *正在运行具有依赖关系注入的应用程序*
2. 浏览到 **/Store**。 这将调用现在使用**Unity**创建的**StoreController**。

    ![MVC 音乐商店](aspnet-mvc-4-dependency-injection/_static/image7.png "MVC 音乐商店")

    *MVC 音乐商店*
3. 关闭浏览器。

在以下练习中，您将学习如何扩展依赖项注入范围以便在 ASP.NET MVC 视图和操作筛选器中使用它。

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>练习2：注入视图

在此练习中，您将学习如何在视图中使用依赖关系注入，其中的新功能为 ASP.NET MVC 4 for Unity 集成。 为此，你将在 "应用商店" 浏览视图中调用一个自定义服务，此操作将显示以下消息和图像。

然后，将项目与 Unity 集成，并创建自定义依赖项解析程序来注入依赖项。

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>任务 1-创建使用服务的视图

在此任务中，您将创建一个视图，该视图执行服务调用以生成新的依赖关系。 此服务包含在此解决方案中包含的简单消息传递服务中。

1. 打开位于**Source\Ex02-Injecting View\Begin**文件夹中的 "**开始**" 解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
      > 
      > 有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 将**MessageService.cs**和**IMessageService.cs**类包括在 **/Services**的**源 \Assets**文件夹中。 为此，请右键单击 "**服务**" 文件夹，然后选择 "**添加现有项**"。 浏览到文件的位置并包含这些文件。

    ![添加消息服务和服务接口](aspnet-mvc-4-dependency-injection/_static/image8.png "添加消息服务和服务接口")

    *添加消息服务和服务接口*

    > [!NOTE]
    > **IMessageService**接口定义由**MessageService**类实现的两个属性。 这些属性-**message**和**ImageUrl**-存储消息以及要显示的图像的 URL。
3. 在项目的根文件夹中创建 **/Pages**文件夹，然后从**Source\Assets**添加现有类**MyBasePage.cs** 。 您将从继承的基本页具有以下结构。

    ![Pages 文件夹](aspnet-mvc-4-dependency-injection/_static/image9.png "Pages 文件夹")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. 打开 **/Views/Store**文件夹中的 "**浏览**" 视图，并使其从**MyBasePage.cs**继承。

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. 在 "**浏览**" 视图中，添加对**MessageService**的调用，以显示该服务检索的图像和消息。
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>任务 2-包括自定义依赖关系解析程序和自定义视图页激活器

在上一个任务中，您在视图内注入了新的依赖项，以便在其中执行服务调用。 现在，你将通过实现 ASP.NET MVC 依赖关系注入接口**IViewPageActivator**和**IDependencyResolver**来解析该依赖项。 你将在解决方案中包括**IDependencyResolver**的实现，该实现将使用 Unity 处理服务检索。 然后，您将包括**IViewPageActivator**接口的另一个自定义实现，该实现将解决视图的创建过程。

> [!NOTE]
> 由于 ASP.NET MVC 3，依赖关系注入的实现已简化了用于注册服务的接口。 **IDependencyResolver**和**IVIEWPAGEACTIVATOR**是 ASP.NET MVC 3 功能的一部分，用于进行依赖关系注入。
> 
> **-IDependencyResolver**接口替换之前的 IMvcServiceLocator。 IDependencyResolver 的实施者必须返回服务或服务集合的实例。
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-IViewPageActivator**接口可更精细地控制通过依赖关系注入来实例化视图页面的方式。 实现**IViewPageActivator**接口的类可以使用上下文信息创建视图实例。
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. 在项目的根文件夹中创建/**工厂**文件夹。
2. 将**CustomViewPageActivator.cs**从 **/Sources/Assets/** 添加到**工厂**文件夹中。 为此，请右键单击 **/Factories**文件夹，选择 "**添加" |"现有项目**"，然后选择 " **CustomViewPageActivator.cs**"。 此类实现**IViewPageActivator**接口以容纳 Unity 容器。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **CustomViewPageActivator**负责使用 Unity 容器来管理创建视图。
3. 将**UnityDependencyResolver.cs**文件从 **/Sources/Assets**添加到 **/Factories**文件夹。 为此，请右键单击 **/Factories**文件夹，选择 "**添加" |"现有项目**"，然后选择 " **UnityDependencyResolver.cs**文件"。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > **UnityDependencyResolver**类是 Unity 的自定义 DependencyResolver。 如果在 Unity 容器中找不到服务，则基本解析程序为 invocated。

在以下任务中，将注册这两种实现，以使模型知道服务和视图的位置。

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>任务 3-注册 Unity 容器中的依赖关系注入

在此任务中，您将所有前面的操作组合在一起，以进行依赖关系注入工作。

现在，你的解决方案包含以下元素：

- 从**MyBaseClass**继承并使用**MessageService**的**浏览**视图。
- 中间类-**MyBaseClass**-已为服务接口声明了依赖关系注入。
- **IMessageService**的**MessageService**及其接口。
- 针对 Unity **UnityDependencyResolver**的自定义依赖关系解析程序，用于处理服务检索。
- 视图页激活器- **CustomViewPageActivator** -用于创建页面。

若要注入**浏览**视图，你现在将在 Unity 容器中注册自定义依赖关系解析程序。

1. 打开**Bootstrapper.cs**文件。
2. 将**MessageService**的实例注册到 Unity 容器，以初始化服务：

    （代码段- *ASP.NET 依赖关系注入实验室-Ex02-注册消息服务*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. 添加对**MvcMusicStore**命名空间的引用。

    （代码段- *ASP.NET 依赖关系注入实验室-Ex02 命名空间*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. 将**CustomViewPageActivator**作为视图页激活器注册到 Unity 容器：

    （代码段- *ASP.NET 依赖关系注入实验室-Ex02-Register CustomViewPageActivator*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. 将 ASP.NET MVC 4 默认依赖关系解析程序替换为**UnityDependencyResolver**的实例。 为此，请将**Initialize**方法内容替换为以下代码：

    （代码段- *ASP.NET 依赖关系注入实验室-Ex02-更新依赖关系解析程序*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC 提供默认的依赖关系解析程序类。 若要使用自定义依赖关系解析程序作为我们为 unity 创建的冲突解决程序，必须替换此解析程序。

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>任务 4-运行应用程序

在此任务中，你将运行应用程序以验证应用商店浏览器是否使用该服务，并显示所检索的图像和消息：

1. 按 **F5** 运行该应用程序。
2. 单击 "流派" 菜单中的 "**岩石**"，并查看**MessageService**如何注入到视图并加载欢迎消息和图像。 在此示例中，我们将进入 &quot;**摇滚**&quot;：

    ![MVC 音乐商店-查看注入](aspnet-mvc-4-dependency-injection/_static/image10.png "MVC 音乐商店-查看注入")

    *MVC 音乐商店-查看注入*
3. 关闭浏览器。

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>练习3：注入操作筛选器

在以前的动手实验室**自定义操作筛选**器中，你使用了筛选器自定义和注入。 在此练习中，您将学习如何使用 Unity 容器注入具有依赖关系注入的筛选器。 为此，需要向音乐商店解决方案添加一个自定义操作筛选器，该操作筛选器将跟踪站点的活动。

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>任务 1-在解决方案中包括跟踪筛选器

在此任务中，你将在音乐存储中包括一个用于跟踪事件的自定义操作筛选器。 自定义操作筛选器概念已在以前的实验室中处理 &quot;自定义操作筛选器&quot;，你只需将 filter 类包括在此实验室的 "资产" 文件夹中，然后为 Unity 创建筛选器提供程序：

1. 打开位于 " **Source\Ex03-注入操作 Filter\Begin** " 文件夹中的 "**开始**" 解决方案。 否则，你可以继续使用通过完成前一练习所获得的**最终**解决方案。

   1. 如果你打开了提供的**开始**解决方案，则需要下载一些缺少的 NuGet 包，然后再继续。 为此，请单击 "**项目**" 菜单并选择 "**管理 NuGet 包**"。
   2. 在 "**管理 NuGet 包**" 对话框中，单击 "**还原**" 以下载缺少的包。
   3. 最后，通过单击 "**生成** | **生成解决方案**" 来生成解决方案。

      > [!NOTE]
      > 使用 NuGet 的优点之一是，无需将所有库都送到项目中，从而减少了项目的大小。 使用 NuGet 功能，通过在包 .config 文件中指定包版本，你可以在首次运行项目时下载所有必需的库。 这就是在从此实验室打开现有解决方案之后需要运行这些步骤的原因。
      > 
      > 有关详细信息，请参阅此文章： [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages)。
2. 将**TraceActionFilter.cs**文件从 **/Sources/Assets**添加到 **/Filters**文件夹。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > 此自定义操作筛选器执行 ASP.NET 跟踪。 可以查看&quot; 实验室 &quot;ASP.NET MVC 4 本地和动态操作筛选器以获取更多参考。
3. 将空类**FilterProvider.cs**添加到 **/Filters.** 文件夹中的项目。
4. 在**FilterProvider.cs**中添加**system.web**和 node.js 命名**空间。**

    （代码段- *ASP.NET 依赖关系注入实验室-Ex03-筛选器提供程序添加命名空间*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. 使类继承自**IFilterProvider**接口。

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. 在**FilterProvider**类中添加**IUnityContainer**属性，然后创建类构造函数来分配容器。

    （代码段- *ASP.NET 依赖关系注入实验室-Ex03 提供程序构造函数*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > 筛选器提供程序类构造函数未在中创建**新**的对象。 容器作为参数传递，并且依赖关系由 Unity 解决。
7. 在**FilterProvider**类中，从**IFilterProvider**接口实现方法**GetFilters** 。

    （代码段- *ASP.NET 依赖关系注入实验室-Ex03 Provider GetFilters*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>任务 2-注册并启用筛选器

在此任务中，您将启用站点跟踪。 为此，你将在**Bootstrapper.cs BuildUnityContainer**方法中注册筛选器以启动跟踪：

1. 打开位于项目根目录中**的 web.config，** 并在 system.web 组中启用跟踪跟踪。

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. 在项目根目录中打开**Bootstrapper.cs** 。
3. 添加对**MvcMusicStore**命名空间的引用。

    （代码段- *ASP.NET 依赖关系注入实验室-Ex03-引导程序添加命名空间*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. 选择**BuildUnityContainer**方法，并在 Unity 容器中注册筛选器。 必须注册筛选器提供程序和操作筛选器。

    （代码段- *ASP.NET 依赖关系注入实验室-Ex03-Register FilterProvider 和 ActionFilter*）

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>任务 3-运行应用程序

在此任务中，您将运行应用程序并测试自定义操作筛选器是否正在跟踪活动：

1. 按 **F5** 运行该应用程序。
2. 单击 "流派" 菜单中的 "**岩石**"。 如果需要，可以浏览更多流派。

    ![Music 商店](aspnet-mvc-4-dependency-injection/_static/image11.png "Music 商店")

    *Music 商店*
3. 浏览到 **/Trace.axd**以查看 "应用程序跟踪" 页，然后单击 "**查看详细信息**"。

    ![应用程序跟踪日志](aspnet-mvc-4-dependency-injection/_static/image12.png "应用程序跟踪日志")

    *应用程序跟踪日志*

    ![应用程序跟踪-请求详细信息](aspnet-mvc-4-dependency-injection/_static/image13.png "应用程序跟踪-请求详细信息")

    *应用程序跟踪-请求详细信息*
4. 关闭浏览器。

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>摘要

完成此动手实验后，你已了解如何通过使用 NuGet 包集成 Unity，在 ASP.NET MVC 4 中使用依赖关系注入。 为实现此目的，你已在控制器、视图和操作筛选器中使用了依赖关系注入。

介绍了以下概念：

- ASP.NET MVC 4 依赖项注入功能
- 使用 Unity 进行 unity 集成 Mvc3 NuGet 包
- 控制器中的依赖关系注入
- 视图中的依赖关系注入
- 操作筛选器的依赖项注入

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>附录 A：安装 Visual Studio Express 2012 for Web

您可以使用 **[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)** 为 Web 或其他 &quot;Express&quot; 版本安装**Microsoft Visual Studio Express 2012** 。 以下说明将指导你完成使用*Microsoft Web 平台安装程序*安装*Visual studio Express 2012 for Web*的步骤。

1. 转到 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。 或者，如果你已经安装了 Web 平台安装程序，则可以打开它并<em>使用 Windows AZURE SDK&quot;搜索 Visual Studio Express 2012 For Web</em>的产品 &quot;。
2. 单击 "**立即安装**"。 如果你没有**Web 平台安装程序**，则会重定向到 "下载并安装"。
3. **Web 平台安装程序**打开后，单击 "**安装**" 以启动安装程序。

    ![安装 Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "安装 Visual Studio Express")

    *安装 Visual Studio Express*
4. 阅读所有产品的许可证和条款，单击 "**我接受**" 以继续。

    ![接受许可条款](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *接受许可条款*
5. 等待下载和安装过程完成。

    ![安装进度](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *安装进度*
6. 安装完成后，单击 "**完成**"。

    ![安装完成](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *安装完成*
7. 单击 "**退出**" 以关闭 Web 平台安装程序。
8. 若要打开 Web Visual Studio Express，请在 "**开始**" 屏幕上，开始书写 &quot;**VS Express**&quot;，然后单击 " **VS Express for Web** " 磁贴。

    ![VS Express for Web 磁贴](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *VS Express for Web 磁贴*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>附录 B：使用代码片段

使用代码片段，您可以随时获得所需的全部代码。 实验室文档将告诉你何时可以使用它们，如下图所示。

![使用 Visual Studio code 代码段将代码插入到项目中](aspnet-mvc-4-dependency-injection/_static/image19.png "使用 Visual Studio code 代码段将代码插入到项目中")

*使用 Visual Studio code 代码段将代码插入到项目中*

***使用键盘添加代码片段（C#仅限）***

1. 将光标放在要插入代码的位置。
2. 开始键入代码片段名称（不含空格或连字符）。
3. 请注意，IntelliSense 显示匹配的代码段名称。
4. 选择正确的代码段（或保留键入内容，直到选择了整个代码段的名称）。
5. 按 Tab 键两次，将代码段插入到光标位置。

![开始键入代码片段名称](aspnet-mvc-4-dependency-injection/_static/image20.png "开始键入代码片段名称")

*开始键入代码片段名称*

![按 Tab 键以选择突出显示的代码段](aspnet-mvc-4-dependency-injection/_static/image21.png "按 Tab 键以选择突出显示的代码段")

*按 Tab 键以选择突出显示的代码段*

![再次按 Tab 键，代码片段将展开](aspnet-mvc-4-dependency-injection/_static/image22.png "再次按 Tab 键，代码片段将展开")

*再次按 Tab 键，代码片段将展开*

***使用鼠标添加代码片段（C#、Visual Basic 和 XML）*** 2. 右键单击要插入代码片段的位置。

1. 选择 "**插入**代码片段"，然后选择 **"我的代码片段"** 。
2. 通过单击从列表中选择相关的代码片段。

![右键单击要插入代码片段的位置，然后选择 "插入代码片段"](aspnet-mvc-4-dependency-injection/_static/image23.png "右键单击要插入代码片段的位置，然后选择 "插入代码片段"")

*右键单击要插入代码片段的位置，然后选择 "插入代码片段"*

![通过单击从列表中选择相关的代码片段](aspnet-mvc-4-dependency-injection/_static/image24.png "通过单击从列表中选择相关的代码片段")

*通过单击从列表中选择相关的代码片段*
