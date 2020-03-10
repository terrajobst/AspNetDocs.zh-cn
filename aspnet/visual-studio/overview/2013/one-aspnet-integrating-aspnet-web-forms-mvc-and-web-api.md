---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 动手实验：一个 ASP.NET：集成 ASP.NET Web 窗体、MVC 和 Web API |Microsoft Docs
author: rick-anderson
description: ASP.NET 是一个框架，用于构建网站、应用程序和服务（使用 MVC、Web API 等专用技术）。 带有扩展 ASP.NET h 。
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505454"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>动手实验：一个 ASP.NET：集成 ASP.NET Web 窗体、MVC 和 Web API

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

> ASP.NET 是一个框架，用于构建网站、应用程序和服务（使用 MVC、Web API 等专用技术）。 由于扩展 ASP.NET 的创建和表示需要集成这些技术，因此，最新的工作就是使用**一个 ASP.NET**。
> 
> Visual Studio 2013 引入了一个新的统一项目系统，可让你在一个项目中构建应用程序并使用所有 ASP.NET 技术。 此功能无需在项目开始时选取一种技术并坚持使用，而是鼓励在一个项目中使用多个 ASP.NET 框架。
> 
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)提供。

<a id="Overview"></a>
## <a name="overview"></a>概述

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，您将了解如何：

- 基于**一个 ASP.NET**项目类型创建网站
- 在同一项目中使用不同的**ASP.NET**框架，如**MVC**和**Web API**
- 标识**ASP.NET**应用程序的主要组件
- 利用**ASP.NET 基架**框架自动创建控制器和视图，以根据模型类执行 CRUD 操作
- 为每个作业使用合适的工具公开计算机和人工可读格式的相同信息集

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下各项：

- Web 或更高版本[的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)
- [Visual Studio 2013 Update 1](https://go.microsoft.com/fwlink/?LinkId=301714)

<a id="Setup"></a>
### <a name="setup"></a>安装

若要运行此动手实验中的练习，您需要先设置您的环境。

1. 打开 Windows 资源管理器并浏览到实验室的**源**文件夹。
2. 右键单击 " **setup.exe** "，然后选择 "以**管理员身份运行**" 以启动安装过程，该过程将配置环境并安装 Visual Studio code 代码段。
3. 如果显示了 "用户帐户控制" 对话框，请确认操作以继续。

> [!NOTE]
> 确保在运行安装过程之前，您已检查本实验的所有依赖项。

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>使用代码段

在整个实验文档中，将指示您插入代码块。 为方便起见，此代码的大部分作为 Visual Studio Code 代码段提供，你可以从 Visual Studio 2013 中访问这些代码段，以避免手动添加它。

> [!NOTE]
> 每个练习都附带了一个起始解决方案，该解决方案位于练习的 "**开始**" 文件夹中，使您可以单独执行每个练习。 请注意，这些开始解决方案中缺少在练习中添加的代码段，并且在完成此练习之前，可能无法工作。 在练习的源代码中，还会找到一个包含 Visual Studio 解决方案的**结束**文件夹，该解决方案的代码是完成相应练习中的步骤所产生的。 如果您在演练本动手实验时需要其他帮助，则可以使用这些解决方案作为指南。

---

<a id="Exercises"></a>
## <a name="exercises"></a>练习

本动手实验包括以下练习：

1. [创建新的 Web 窗体项目](#Exercise1)
2. [使用基架创建 MVC 控制器](#Exercise2)
3. [使用基架创建 Web API 控制器](#Exercise3)

完成本实验的估计时间： **60 分钟**

> [!NOTE]
> 首次启动 Visual Studio 时，必须选择一个预定义的设置集合。 每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。 此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。 如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>练习1：创建新的 Web 窗体项目

在此练习中，你将使用**ASP.NET**统一项目体验在 Visual Studio 2013 中创建一个新的 Web 窗体网站，这将允许你轻松地将 Web 窗体、MVC 和 web API 组件集成到同一个应用程序中。 然后，你将浏览生成的解决方案并确定其部件，最后你会看到网站正在运行。

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>任务1–使用一 ASP.NET 体验创建新站点

在此任务中，你将基于 " **ASP.NET** " 项目类型在 Visual Studio 中开始创建新网站。 **一个 ASP.NET**统一了所有 ASP.NET 技术，并为你提供了根据需要进行混合和匹配的选项。 然后，你将识别应用程序中并行存在的 Web 窗体、MVC 和 Web API 的不同组件。

1. 打开 " **Web Visual Studio Express 2013** "，然后选择 "**文件" |新建项目 ...** 启动新解决方案。

    ![创建新项目](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *创建新项目*
2. 在 "**新建项目**" 对话框中，选择 " **ASP.NET Web 应用程序**"。  **C#"Web** " 选项卡，并确保选择 **.NET Framework 4.5** "。 将项目命名为*MyHybridSite*，选择一个**位置**，然后单击 **"确定"** 。

    ![新的 ASP.NET Web 应用程序项目](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *创建新的 ASP.NET Web 应用程序项目*
3. 在 "**新建 ASP.NET 项目**" 对话框中，选择 " **Web 窗体**" 模板，并选择 " **MVC**和**Web API**选项"。 此外，请确保 "**身份验证**" 选项设置为 "**单个用户帐户**"。 单击 **“确定”** 继续。

    ![使用 Web 窗体模板创建新的项目，包括 Web API 和 MVC 组件](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *使用 Web 窗体模板创建新的项目，包括 Web API 和 MVC 组件*
4. 你现在可以浏览生成的解决方案的结构。

    ![探索生成的解决方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *探索生成的解决方案*

    1. **帐户：** 此文件夹包含要注册的 Web 窗体页，登录并管理应用程序的用户帐户。 当在 Web 窗体项目模板的配置过程中选择**单个用户帐户**身份验证选项时，将添加此文件夹。
    2. **模型：** 此文件夹将包含表示应用程序数据的类。
    3. **控制器**和**视图**： **ASP.NET MVC**和**ASP.NET Web API**组件需要这些文件夹。 你将在下一练习中探索 MVC 和 Web API 技术。
    4. Default.aspx **、default.aspx**和 **.aspx**文件是预定义的 Web 窗体**页，你**可以使用它们作为开始点来构建特定于你的应用程序的页面。 这些文件的编程逻辑位于一个单独的文件中，该文件称为 &quot;代码隐藏&quot; 文件，该文件具有 &quot;&quot; 或 &quot;&quot; 扩展（具体取决于所使用的语言）。 代码隐藏逻辑在服务器上运行，并动态生成页面的 HTML 输出。
    5. **Master**和**node.js 页面定义**了应用程序中的所有页面的外观和标准行为。
5. 双击**default.aspx**文件，浏览页面的内容。

    ![浏览 default.aspx 页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *浏览 default.aspx 页*

    > [!NOTE]
    > 文件顶部的**Page**指令定义 Web 窗体页的属性。 例如， **MasterPageFile**属性指定母版页的路径（在本例中为 "*站点母版页*"），**继承**属性定义要继承的页面的代码隐藏类。 此类位于由代码**隐藏**特性确定的文件中。
    > 
    > **Asp： Content**控件保存页面的实际内容（文本、标记和控件），并映射到母版页上的**asp： ContentPlaceHolder**控件。 在这种情况下，将在 "MainContent *" 页中*定义的 " " 控件内呈现页面内容。
6. 展开**应用\_启动**文件夹，然后注意**WebApiConfig.cs**文件。 Visual Studio 将该文件包含在生成的解决方案中，因为在配置项目时包含一个 ASP.NET 模板。
7. 打开**WebApiConfig.cs**文件。 在*webapiconfig.cs*类中，你将找到与 web api 关联的配置，该配置将 HTTP 路由映射到**web api 控制器**。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. 打开**RouteConfig.cs**文件。 在*RegisterRoutes*方法中，你将找到与 mvc 关联的配置，该配置将 HTTP 路由映射到**mvc 控制器**。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>任务2–运行解决方案

在此任务中，你将运行生成的解决方案，浏览应用及其一些功能，如 URL 重写和内置身份验证。

1. 若要运行解决方案，请按**F5**或单击工具栏上的 "**开始**" 按钮。 应用程序主页应在浏览器中打开。

    ![运行解决方案](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. 验证是否正在调用 Web 窗体页。 为此，请将 **/contact.aspx**追加到地址栏中的 URL，然后按**enter**。

    ![友好的 URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *友好 Url*

    > [!NOTE]
    > 如您所见，URL 将更改为 **/contact**。 从**ASP.NET 4**开始，URL 路由功能已添加到 Web 窗体，因此你可以编写类似 *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* 的 url，而不是 *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* 。 有关详细信息，请参阅[URL 路由](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md)。
3. 现在，你将浏览集成到应用程序中的身份验证流。 为此，请单击页面右上角的 "**注册**"。

    ![注册新用户](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *注册新用户*
4. 在 "**注册**" 页上，输入**用户名**和**密码**，然后单击 "**注册**"。

    ![注册页面](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *注册页面*
5. 应用程序将注册新帐户，并对用户进行身份验证。

    ![用户已进行身份验证](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *用户已进行身份验证*
6. 返回到 Visual Studio 并按**SHIFT + F5**停止调试。

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>练习2：使用基架创建 MVC 控制器

在本练习中，你将利用 Visual Studio 提供的 ASP.NET 基架框架来创建 ASP.NET MVC 5 控制器，其中包含操作和 Razor 视图来执行 CRUD 操作，而无需编写任何代码。 基架进程将使用实体框架 Code First 在 SQL 数据库中生成数据上下文和数据库架构。

**关于实体框架 Code First**

实体框架（EF）是一个对象关系映射器（ORM），使您可以通过使用概念应用程序模型进行编程来创建数据访问应用程序，而无需使用关系存储架构直接编程。

利用实体框架 Code First 建模工作流，你可以使用自己的域类来表示 EF 在执行查询、更改跟踪和更新功能时所依赖的模型。 使用 Code First 开发工作流，无需通过创建数据库或指定架构来启动应用程序。 相反，您可以编写为您的应用程序定义最适当的域模型对象的标准 .NET 类，实体框架将为您创建数据库。

> [!NOTE]
> 可在[此处](../../../entity-framework.md)详细了解实体框架。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>任务1–创建新模型

你现在将定义**Person**类，这将是基架进程用来创建 MVC 控制器和视图的模型。 首先要创建**Person**模型类，并使用基架功能自动创建控制器中的 CRUD 操作。

1. 打开**Visual Studio Express 2013 For Web** ，并打开位于**buildingappswithcachingservice-ex2-getproducts latency-cs-MvcScaffolding/Begin**文件夹中的**MyHybridSite**解决方案。 或者，你可以继续学习你在上一练习中获得的解决方案。
2. 在**解决方案资源管理器**中，右键单击**MyHybridSite**项目的 "**模型**" 文件夹，然后选择 "**添加 |类 ...** 。

    ![添加 Person 模型类](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *添加 Person 模型类*
3. 在 "**添加新项**" 对话框中，将文件命名为 " *Person.cs* "，然后单击 "**添加**"。

    ![创建 Person 模型类](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *创建 Person 模型类*
4. 将**Person.cs**文件的内容替换为以下代码。 按**CTRL + S**保存更改。

    （代码段- *BringingTogetherOneAspNet-buildingappswithcachingservice-ex2-getproducts latency-cs-PersonClass*）

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. 在**解决方案资源管理器**中，右键单击**MyHybridSite**项目并选择 "**生成**"，或按**CTRL + SHIFT + B**生成项目。

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>任务2–创建 MVC 控制器

创建**人员**模型后，将使用带有实体框架的 ASP.NET MVC 基架为**Person**创建 CRUD 控制器操作和视图。

1. 在**解决方案资源管理器**中，右键单击**MyHybridSite**项目的 "**控制器**" 文件夹，然后选择 "**添加 |新建基架项 ...**

    ![创建新的基架控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *创建新的基架控制器*
2. 在 "**添加基架**" 对话框中，选择 **"包含视图的 MVC 5 控制器，使用实体框架**"，然后单击 "**添加"。**

    ![选择包含视图和实体框架的 MVC 5 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *选择包含视图和实体框架的 MVC 5 控制器*
3. 将*MvcPersonController*设置为**控制器名称**，选择 "**使用异步控制器操作**" 选项，并选择**Person （MyHybridSite）** 作为**模型类**。

    ![使用基架添加 MVC 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *使用基架添加 MVC 控制器*
4. 在 "**数据上下文类**" 下，单击 "**新建数据上下文 ...** "。

    ![创建新的数据上下文](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *创建新的数据上下文*
5. 在 "**新建数据上下文**" 对话框中，将新的数据上下文命名为*PersonContext* ，然后单击 "**添加**"。

    ![创建新的 PersonContext](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *创建新的 PersonContext 类型*
6. 单击 "**添加**" 以创建具有基架的**人员**的新控制器。 然后，Visual Studio 将生成控制器操作、人员数据上下文和 Razor 视图。

    ![用基架创建 MVC 控制器之后](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *用基架创建 MVC 控制器之后*
7. 打开 "**控制器**" 文件夹中的**MvcPersonController.cs**文件。 请注意，CRUD 操作方法已自动生成。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > 通过从前面步骤中的 "基架" 选项中选择 "**使用异步控制器操作**" 复选框，Visual Studio 将为涉及到 Person 数据上下文访问权限的所有操作生成异步操作方法。 建议为长时间运行的非 CPU 绑定的请求使用异步操作方法，以避免在处理请求时阻止 Web 服务器执行工作。

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>任务3–运行解决方案

在此任务中，您将再次运行该解决方案以验证**人员**的视图是否按预期方式工作。 您将添加一个新人员来验证是否已成功将其保存到数据库。

1. 按 **“F5”** 运行该解决方案。
2. 导航到 **/MvcPerson**。 显示人员列表的基架视图应显示。
3. 单击 "**新建**" 以添加新人员。

    ![导航到基架 MVC 视图](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *导航到基架 MVC 视图*
4. 在 "**创建**" 视图中，为人员提供**名称**和**年龄**，并单击 "**创建**"。

    ![添加新人员](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *添加新人员*
5. 新用户将添加到列表。 在元素列表中，单击 "**详细信息**" 以显示人员的详细信息视图。 然后，在**详细信息**视图中，单击 "**返回到列表**"，返回到列表视图。

    ![人员的详细信息视图](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *人员的详细信息视图*
6. 单击 "**删除**" 链接以删除该用户。 在 "**删除**" 视图中，单击 "**删除**" 确认操作。

    ![删除人员](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *删除人员*
7. 返回到 Visual Studio 并按**SHIFT + F5**停止调试。

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>练习3：使用基架创建 Web API 控制器

Web API 框架是 ASP.NET 堆栈的一部分，旨在使实现 HTTP 服务更简单，通常通过 RESTful API 发送和接收 JSON 或 XML 格式的数据。

在此练习中，您将再次使用 ASP.NET 基架以生成 Web API 控制器。 您将使用上一练习中的同一**person**和**PersonContext**类，以 JSON 格式提供同一个人数据。 你将了解如何以不同的方式在同一个 ASP.NET 应用程序中公开相同的资源。

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>任务1–创建 Web API 控制器

在此任务中，您将创建一个新的**WEB API 控制器**，它将以计算机可使用的格式（如 JSON）公开用户数据。

1. 如果尚未打开，请打开**Visual Studio Express 2013 For Web** ，并打开位于**section-cs-WebAPI/Begin**文件夹中的**MyHybridSite**解决方案。 或者，你可以继续学习你在上一练习中获得的解决方案。

    > [!NOTE]
    > 如果从练习3开始处理开始的解决方案，请按**CTRL + SHIFT + B**生成解决方案。
2. 在**解决方案资源管理器**中，右键单击**MyHybridSite**项目的 "**控制器**" 文件夹，然后选择 "**添加 |新建基架项 ...**

    ![创建新的基架控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *创建新的基架控制器*
3. 在 "**添加基架**" 对话框中，选择左窗格中的 " **web api** "，然后在中间窗格中选择 "**包含实体框架操作的 web api 2 控制器**"，并单击 "**添加"。**

    ![选择包含操作和实体框架的 Web API 2 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "选择包含操作和实体框架的 Web API 2 控制器")

    *选择包含操作和实体框架的 Web API 2 控制器*
4. 将*ApiPersonController*设置为**控制器名称**，选择 "**使用异步控制器操作**" 选项，并分别选择**Person （MyHybridSite）** 和**PersonContext （MyHybridSite）** 作为**模型**和**数据上下文**类。 然后单击 **“添加”** 。

    ![使用基架添加 Web API 控制器](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "使用基架添加 Web API 控制器")

    *使用基架添加 Web API 控制器*
5. 然后，Visual Studio 将生成具有四个 CRUD 操作的**ApiPersonController**类来处理数据。

    ![创建具有基架的 Web API 控制器之后](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "创建具有基架的 Web API 控制器之后")

    *创建具有基架的 Web API 控制器之后*
6. 打开**ApiPersonController.cs**文件并检查*GetPeople*操作方法。 此方法查询**PersonContext**类型的 db 字段，以获取人员数据。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. 现在，请注意方法定义上方的注释。 它提供公开此操作的 URI，你将在下一任务中使用此操作。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > 默认情况下，Web API 配置为将查询捕获到 */api*路径，以避免与 MVC 控制器冲突。 如果需要更改此设置，请参阅[ASP.NET Web API 中的路由](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md)。

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>任务2–运行解决方案

在此任务中，您将使用 Internet Explorer **F12 开发人员工具**来检查 Web API 控制器的完整响应。 你将了解如何捕获网络流量，以便更深入地了解应用程序数据。

> [!NOTE]
> 请确保在 Visual Studio 工具栏上的 "**开始**" 按钮中选择了**Internet Explorer** 。
> 
> ![Internet Explorer 选项](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **F12 开发人员工具**具有一组广泛的功能，不在此动手实验中介绍。 如果要了解有关详细信息，请参阅[使用 F12 开发人员工具](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85))。

1. 按 **“F5”** 运行该解决方案。

    > [!NOTE]
    > 为了正确执行此任务，应用程序需要有数据。 如果数据库为空，则可以返回到练习2中的任务3，并按照如何使用 MVC 视图创建新人员的步骤进行操作。
2. 在浏览器中，按**F12**打开**开发人员工具**面板。 按**CTRL** + **4**或单击**网络**图标，然后单击绿色箭头按钮开始捕获网络流量。

    ![启动 Web API 网络捕获](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "启动 Web API 网络捕获")

    *启动 Web API 网络捕获*
3. 将**api/ApiPerson**追加到浏览器地址栏中的 URL。 现在，你将从**ApiPersonController**检查响应的详细信息。

    ![通过 Web API 检索人员数据](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "通过 Web API 检索人员数据")

    *通过 Web API 检索人员数据*

    > [!NOTE]
    > 下载完成后，系统将提示您使用下载的文件进行操作。 让对话框保持打开状态，以便能够通过 "开发人员工具" 窗口观看响应内容。
4. 现在，你将检查响应的正文。 为此，请单击 "**详细信息**" 选项卡，然后单击 "**响应正文**"。 您可以检查下载的数据是否是对象的列表，这些对象具有与**Person**类对应的 " **Id**"、"**名称**" 和 "**年龄**"。

    ![查看 Web API 响应正文](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "查看 Web API 响应正文")

    *查看 Web API 响应正文*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>任务3–添加 Web API 帮助页

创建 Web API 时，创建帮助页非常有用，以便其他开发人员知道如何调用 API。 您可以手动创建和更新文档页，但最好是自动生成文档页，以避免执行维护工作。 在此任务中，你将使用 Nuget 包自动向解决方案生成 Web API 帮助页。

1. 在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后单击 "**程序包管理器控制台**"。
2. 在 "**包管理器控制台**" 窗口中，执行以下命令：

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > **WebApi. HelpPage**包将安装所需的程序集，并添加 "**区域/HelpPage** " 文件夹下 "帮助" 页的 MVC 视图。

    ![HelpPage 面积图](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "HelpPage 面积图")

    *HelpPage 面积图*
3. 默认情况下，帮助页包含文档的占位符字符串。 您可以使用 XML 文档注释来创建文档。 若要启用此功能，请打开**HelpPageConfig.cs**文件，该文件位于 "**区域/HelpPage/应用\_Start** " 文件夹中，并取消注释以下行：

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. 在**解决方案资源管理器**中，右键单击**MyHybridSite**项目，选择 "**属性**"，然后单击 "**生成**" 选项卡。

    ![生成选项卡](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "生成部分")

    *生成选项卡*
5. 在 "**输出**" 下，选择 " **XML 文档文件**"。 在 "编辑" 框中，键入**App\_Data/xml**。

    !["生成" 选项卡中的输出部分](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png ""生成" 选项卡中的输出部分")

    *"生成" 选项卡中的输出部分*
6. 按**CTRL** + **S**保存更改。
7. 从 "**控制器**" 文件夹打开**ApiPersonController.cs**文件。
8. 在*GetPeople*方法签名和 *//GET api/ApiPerson*注释之间输入一个新行，然后键入三个正斜杠。

    > [!NOTE]
    > Visual Studio 会自动插入定义方法文档的 XML 元素。
9. 为*GetPeople*方法添加摘要文本和返回值。 其外观应如下所示。

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. 按 **“F5”** 运行该解决方案。
11. 将 **/help**追加到地址栏中的 URL，浏览到 "帮助" 页。

    ![ASP.NET Web API 帮助页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "ASP.NET Web API 帮助页")

    *ASP.NET Web API 帮助页*

    > [!NOTE]
    > 页面的主要内容是 Api 表，按控制器分组。 表项是使用**IApiExplorer**接口动态生成的。 如果添加或更新 API 控制器，下一次生成应用程序时，该表会自动更新。
    > 
    > " **API** " 列列出 HTTP 方法和相对 URI。 "**说明**" 列包含已从方法的文档中提取的信息。
12. 请注意，在 "说明" 列中将显示在方法定义上方添加的说明。

    ![API 方法说明](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "API 方法说明")

    *API 方法说明*
13. 单击其中一个 API 方法可以导航到包含更多详细信息（包括示例响应正文）的页面。

    ![详细信息页](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "详细信息页")

    *详细信息页*

---

<a id="Summary"></a>
## <a name="summary"></a>摘要

通过完成本动手实验，你学习了如何：

- 在 Visual Studio 2013 中使用一种 ASP.NET 体验创建新的 Web 应用程序
- 将多个 ASP.NET 技术集成到一个项目中
- 使用 ASP.NET 基架从模型类生成 MVC 控制器和视图
- 生成 Web API 控制器，该控制器通过使用异步编程和数据访问等功能实体框架
- 为控制器自动生成 Web API 帮助页
