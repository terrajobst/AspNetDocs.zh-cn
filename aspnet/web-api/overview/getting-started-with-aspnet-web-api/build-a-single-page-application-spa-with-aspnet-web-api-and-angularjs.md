---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: 动手实验：使用 ASP.NET Web API 和 ASP.NET 4.x 构建单页应用程序（SPA）
author: rick-anderson
description: 分步编码：生成包含 ASP.NET Web API 的单页面应用程序（SPA），并 ASP.NET 4.x。
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448760"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a>动手实验：使用 ASP.NET Web API 和 node.js 生成单页面应用程序（SPA）

由[Web 训练营团队](https://twitter.com/webcamps)使用

[下载 Web 训练营培训工具包](https://aka.ms/webcamps-training-kit)

此动手实验演示了如何使用 ASP.NET Web API 和 ASP.NET 的 node.js 构建单页面应用程序（SPA）。

在此试验实验室中，你将利用这些技术来实现书呆子测验，这是一个基于 SPA 概念的琐碎内容网站。 首先，通过 ASP.NET Web API 实现服务层，以便公开所需的终结点来检索测验问题并存储答案。 然后，你将使用 AngularJS 和 CSS3 转换效果生成丰富且响应迅速的 UI。

在传统 web 应用程序中，客户端（浏览器）通过请求页面来启动与服务器的通信。 服务器随后处理请求，并将页面的 HTML 发送到客户端。 在后续与页面的交互（例如，用户导航到链接或提交包含数据的窗体）时，会将新请求发送到服务器，并再次开始此流：服务器处理请求并将新页发送到浏览器，以响应新操作请求ed。
> 
> 在单页面应用程序（Spa）中，在初始请求后将整个页面加载到浏览器中，但后续交互会通过 Ajax 请求进行。 这意味着浏览器必须只更新页面中已更改的部分;无需重新加载整个页面。 SPA 方法会减少应用程序响应用户操作所需的时间，从而导致更流畅的体验。
> 
> SPA 的体系结构涉及传统 web 应用程序中不存在的某些挑战。 不过，新的技术（如 ASP.NET Web API）、AngularJS 的 JavaScript 框架以及 CSS3 提供的新样式功能使得设计和构建 Spa 变得非常容易。
> 
> 
> 所有示例代码和代码段都包含在 Web 训练营培训工具包中， [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)提供。

## <a name="overview"></a>概述

<a id="Objectives"></a>
### <a name="objectives"></a>目标

在本动手实验中，您将了解如何：

- 创建 ASP.NET Web API 服务来发送和接收 JSON 数据
- 使用 AngularJS 创建响应式 UI
- 利用 CSS3 转换增强 UI 体验

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>系统必备

完成本动手实验需要以下各项：

- Web 或更高版本[的 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)

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

1. [创建 Web API](#Exercise1)
2. [创建 SPA 接口](#Exercise2)

完成本实验的估计时间： **60 分钟**

> [!NOTE]
> 首次启动 Visual Studio 时，必须选择一个预定义的设置集合。 每个预定义的集合都设计为与特定的开发风格相匹配，并确定窗口布局、编辑器行为、IntelliSense 代码段和对话框选项。 此实验室中的过程描述在使用**常规开发设置**集合时，在 Visual Studio 中完成给定任务所需执行的操作。 如果为开发环境选择了其他设置集合，则需要考虑的步骤可能会有所不同。

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a>练习1：创建 Web API

SPA 的关键部分之一是服务层。 它负责处理 UI 发送的 Ajax 调用并返回响应该调用的数据。 检索到的数据应以计算机可读格式显示，以便客户端对其进行分析和使用。

Web API 框架是 ASP.NET 堆栈的一部分，旨在使实现 HTTP 服务（通常通过 RESTful API 发送和接收 JSON 或 XML 格式的数据）变得更加容易。 在本练习中，您将创建网站来托管书呆子测验应用程序，然后实现后端服务，以使用 ASP.NET Web API 公开和保存测验数据。

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a>任务1–创建书呆子测验的初始项目

在此任务中，您将开始创建一个新的 ASP.NET MVC 项目，该项目支持 ASP.NET Web API 基于 Visual Studio 附带的**一种 ASP.NET**项目类型。 **一个 ASP.NET**统一了所有 ASP.NET 技术，并为你提供了根据需要进行混合和匹配的选项。 然后，将添加实体框架的模型类和数据库初始值设定项以插入测验问题。

1. 打开 " **Web Visual Studio Express 2013** "，然后选择 "**文件" |新建项目 ...** 启动新解决方案。

    ![创建新项目](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "创建新项目")

    *创建新项目*
2. 在 "**新建项目**" 对话框中，选择 " **ASP.NET Web 应用程序**"。  **C#** 请确保选中 **.NET Framework 4.5** ，将其命名为*GeekQuiz*，选择一个**位置**，然后单击 **"确定"** 。

    ![创建新的 ASP.NET Web 应用程序项目](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "创建新的 ASP.NET Web 应用程序项目")

    *创建新的 ASP.NET Web 应用程序项目*
3. 在 "**新建 ASP.NET 项目**" 对话框中，选择 " **MVC** " 模板，然后选择 " **Web API** " 选项。 此外，请确保 "**身份验证**" 选项设置为 "**单个用户帐户**"。 单击 **“确定”** 继续。

    ![使用 MVC 模板创建新项目，包括 Web API 组件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    *使用 MVC 模板创建新项目，包括 Web API 组件*
4. 在**解决方案资源管理器**中，右键单击**GeekQuiz**项目的 "**模型**" 文件夹，然后选择 "**添加 |现有项 ...**

    ![添加现有项](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "添加现有项")

    *添加现有项*
5. 在 "**添加现有项**" 对话框中，导航到 "**源/资产/型号**" 文件夹，然后选择 "所有文件"。 单击 **“添加”** 。

    ![添加模型资产](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "添加模型资产")

    *添加模型资产*

    > [!NOTE]
    > 通过添加这些文件，您将为书呆子测验应用程序添加数据模型、实体框架的数据库上下文和数据库初始值设定项。
    > 
    > **实体框架（EF）** 是一个对象关系映射器（ORM），使您可以通过使用概念应用程序模型进行编程来创建数据访问应用程序，而无需使用关系存储架构直接编程。 可在[此处](../../../entity-framework.md)详细了解实体框架。
    > 
    > 下面是刚才添加的类的说明：
    > 
    > - **TriviaOption：** 表示与测验题关联的单个选项
    > - **TriviaQuestion：** 表示测验题，并通过**options**属性公开关联选项
    > - **TriviaAnswer：** 表示用户在响应测验问题时选择的选项
    > - **TriviaContext：** 表示书呆子测验应用程序的实体框架数据库上下文。 此类派生自**DContext** ，并公开**DbSet**属性，这些属性表示上述实体的集合。
    > - **TriviaDatabaseInitializer：** **TriviaContext**类的实体框架初始值设定项，该类继承自**CreateDatabaseIfNotExists**。 此类的默认行为是在数据库不存在时创建该数据库，并插入在**Seed**方法中指定的实体。
6. 打开**Global.asax.cs**文件并添加以下 using 语句。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. 在**应用程序\_Start**方法的开头添加以下代码，以将**TriviaDatabaseInitializer**设置为数据库初始值设定项。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. 修改**Home**控制器以限制对经过身份验证的用户的访问。 为此，请打开 "**控制器**" 文件夹中的**HomeController.cs**文件，并将**授权**属性添加到**HomeController**类定义。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > **授权**筛选器将检查是否对用户进行了身份验证。 如果用户未通过身份验证，则返回 HTTP 状态代码401（未授权），而无需调用该操作。 您可以在全局、控制器级别或单个操作级别应用筛选器。
9. 现在，您将自定义网页的布局和品牌。 为此，请打开视图中的 **\_布局 cshtml**文件 **|共享**文件夹，并通过将*ASP.NET 应用程序*替换为*书呆子测验*来更新 **&lt;标题&gt;** 元素的内容。

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. 在同一文件中，通过删除 "*关于*" 和 "*联系人*" 链接，然后重命名 "*开始* *播放*" 链接来更新导航栏。 此外，将*应用程序名称*链接重命名为 "*书呆子测验*"。 导航栏的 HTML 应类似于以下代码。

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. 通过使用*书呆子测验*替换*My ASP.NET 应用程序*来更新布局页的页脚。 为此，请将 **&lt;页脚&gt;** 元素的内容替换为以下突出显示的代码。

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a>任务2–创建 TriviaController Web API

在上一任务中，已创建书呆子测验 web 应用程序的初始结构。 你现在将生成一个简单的 Web API 服务，该服务与测验数据模型交互并公开以下操作：

- **获取/api/trivia**：从测验列表中检索要由经过身份验证的用户回答的下一个问题。
- **POST/api/trivia**：存储经过身份验证的用户指定的测验应答。

你将使用 Visual Studio 提供的 ASP.NET 基架工具为 Web API 控制器类创建基线。

1. 在**应用\_启动**文件夹内打开**WebApiConfig.cs**文件。 此文件定义了 Web API 服务的配置，如如何将路由映射到 Web API 控制器操作。
2. 在文件的开头添加以下 using 语句。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. 将以下突出显示的代码添加到**Register**方法，以全局配置由 Web API 操作方法检索的 JSON 数据的格式化程序。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > **CamelCasePropertyNamesContractResolver**自动将属性名称转换为*camel*大小写，这是 JavaScript 中属性名称的一般约定。
4. 在**解决方案资源管理器**中，右键单击**GeekQuiz**项目的 "**控制器**" 文件夹，然后选择 "**添加 |新建基架项 ...**

    ![创建新的基架项](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "创建新的基架项")

    *创建新的基架项*
5. 在 "**添加基架**" 对话框中，确保已在左窗格中选择 "**通用**" 节点。 然后，在中间窗格中选择 " **WEB API 2 控制器-空**" 模板，然后单击 "**添加**"。

    ![选择 "Web API 2 控制器" 空模板](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "选择 "Web API 2 控制器" 空模板")

    *选择 "Web API 2 控制器" 空模板*

    > [!NOTE]
    > **ASP.NET 基架**是用于 ASP.NET Web 应用程序的代码生成框架。 Visual Studio 2013 包含用于 MVC 和 Web API 项目的预安装代码生成器。 如果要快速添加与数据模型交互的代码，以减少开发标准数据操作所需的时间，则应在项目中使用基架。
    > 
    > 基架进程还可以确保在项目中安装所有必需的依赖项。 例如，如果您从一个空的 ASP.NET 项目开始，然后使用基架添加一个 Web API 控制器，则所需的 Web API NuGet 包和引用会自动添加到您的项目中。
6. 在 "**添加控制器**" 对话框中，在 "**控制器名称**" 文本框中键入*TriviaController* ，然后单击 "**添加**"。

    ![添加琐碎内容控制器](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "添加琐碎内容控制器")

    *添加琐碎内容控制器*
7. 然后，将**TriviaController.cs**文件添加到**GeekQuiz**项目的**控制器**文件夹中，其中包含一个空的**TriviaController**类。 在文件的开头添加以下 using 语句。

    （代码段- *AspNetWebApiSpa-Ex1-TriviaControllerUsings*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. 在**TriviaController**类的开头添加以下代码，以定义、初始化和处置控制器中的**TriviaContext**实例。

    （代码段- *AspNetWebApiSpa-Ex1-TriviaControllerContext*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > **TriviaController**的**Dispose**方法调用**TriviaContext**实例的**dispose**方法，这可确保在释放或垃圾回收**TriviaContext**实例时释放上下文对象使用的所有资源。 这包括关闭由实体框架打开的所有数据库连接。
9. 在**TriviaController**类的末尾添加以下帮助器方法。 此方法从数据库中检索要由指定用户应答的以下测验问题。

    （代码段- *AspNetWebApiSpa-Ex1-TriviaControllerNextQuestion*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. 向**TriviaController**类添加以下**Get**操作方法。 此操作方法调用在上一步中定义的**NextQuestionAsync** helper 方法，以检索经过身份验证的用户的下一个问题。

    （代码段- *AspNetWebApiSpa-Ex1-TriviaControllerGetAction*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. 在**TriviaController**类的末尾添加以下帮助器方法。 此方法将指定的答案存储在数据库中，并返回一个布尔值，指示答案是否正确。

    （代码段- *AspNetWebApiSpa-Ex1-TriviaControllerStoreAsync*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. 将以下**Post**操作方法添加到**TriviaController**类。 此操作方法将答案与经过身份验证的用户相关联，并调用**StoreAsync** helper 方法。 然后，它使用 helper 方法返回的布尔值发送响应。

    （代码段- *AspNetWebApiSpa-Ex1-TriviaControllerPostAction*）

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. 修改 Web API 控制器，通过向**TriviaController**类定义添加**授权**特性来限制对经过身份验证的用户的访问。

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>任务3–运行解决方案

在此任务中，你将验证你在上一任务中生成的 Web API 服务是否按预期方式工作。 你将使用 Internet Explorer **F12 开发人员工具**来捕获网络流量，并检查 Web API 服务的完整响应。

> [!NOTE]
> 请确保在 Visual Studio 工具栏上的 "**开始**" 按钮中选择了**Internet Explorer** 。
> 
> ![Internet Explorer 选项](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. 按 **“F5”** 运行该解决方案。 "**登录**" 页应出现在浏览器中。

    > [!NOTE]
    > 当应用程序启动时，将触发默认 MVC 路由，该路由默认映射到**HomeController**类的**索引**操作。 由于**HomeController**仅限于经过身份验证的用户（请记住，您在练习1中用**授权**属性修饰了该类），并且尚未对用户进行身份验证，因此应用程序会将原始请求重定向到登录页。

    ![运行解决方案](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "运行解决方案")

    *运行解决方案*
2. 单击 "**注册**" 以创建新用户。

    ![注册新用户](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "注册新用户")

    *注册新用户*
3. 在 "**注册**" 页上，输入**用户名**和**密码**，然后单击 "**注册**"。

    ![注册页面](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "注册页面")

    *注册页面*
4. 应用程序将注册新帐户，并对用户进行身份验证并重定向回主页。

    ![用户已进行身份验证](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "用户已进行身份验证")

    *用户已进行身份验证*
5. 在浏览器中，按**F12**打开**开发人员工具**面板。 按**CTRL + 4**或单击**网络**图标，然后单击绿色箭头按钮开始捕获网络流量。

    ![启动 Web API 网络捕获](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "启动 Web API 网络捕获")

    *启动 Web API 网络捕获*
6. 将**api/琐碎内容**追加到浏览器地址栏中的 URL。 现在，你将从**TriviaController**中的**Get**操作方法检查响应的详细信息。

    ![通过 Web API 检索下一个问题数据](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "通过 Web API 检索下一个问题数据")

    *通过 Web API 检索下一个问题数据*

    > [!NOTE]
    > 下载完成后，系统将提示您使用下载的文件进行操作。 让对话框保持打开状态，以便能够通过 "开发人员工具" 窗口观看响应内容。
7. 现在，你将检查响应的正文。 为此，请单击 "**详细信息**" 选项卡，然后单击 "**响应正文**"。 您可以使用 "属性"**选项**（这是**TriviaOption**对象的列表）的对象、 **id**和与**TriviaQuestion**类相对应的**标题**来检查下载的数据。

    ![查看 Web API 响应正文](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "查看 Web API 响应正文")

    *查看 Web API 响应正文*
8. 返回到 Visual Studio 并按**SHIFT + F5**停止调试。

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a>练习2：创建 SPA 接口

在本练习中，您将首先构建书呆子测验的 web 前端部分，重点介绍使用**AngularJS**的单页应用程序交互。 然后，你将通过使用 CSS3 来执行丰富的动画来增强用户体验，并在从一个问题转换到下一个问题时提供上下文切换的视觉效果。

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a>任务1–使用 AngularJS 创建 SPA 接口

在此任务中，您将使用**AngularJS**实现书呆子测验应用程序的客户端。 **AngularJS**是一个开源 JavaScript 框架，它将基于浏览器的应用程序与*模型-视图-控制器*（MVC）功能进行了补充，同时简化了开发和测试。

首先从 Visual Studio 的包管理器控制台安装 AngularJS。 然后，你将创建一个控制器来提供书呆子测验应用和视图的行为，以便使用 AngularJS 模板引擎呈现测验问题和答案。

> [!NOTE]
> 有关 AngularJS 的详细信息，请参阅[[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/)。

1. 打开**Visual Studio Express 2013 For Web** ，并打开位于**buildingappswithcachingservice-ex2-getproducts latency-cs-CreatingASPAInterface/Begin**文件夹中的**GeekQuiz**解决方案。 或者，你可以继续学习你在上一练习中获得的解决方案。
2. 从 "**工具**" > **NuGet 包管理器**"中打开**包管理器控制台**。 键入以下命令以安装**AngularJS** NuGet 包。

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. 在**解决方案资源管理器**中，右键单击**GeekQuiz**项目的 "**脚本**" 文件夹，然后选择 "**添加 |新文件夹**。 将文件夹命名为 " **app** "，并按**enter**。
4. 右键单击刚创建的**应用**文件夹，然后选择 "**添加 |JavaScript 文件**。

    ![创建新的 JavaScript 文件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    *创建新的 JavaScript 文件*
5. 在 "**指定项名称**" 对话框中，在 "**项名称**" 文本框中键入 "*测验-控制器*"，并单击 **"确定"** 。

    ![命名新的 JavaScript 文件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    *命名新的 JavaScript 文件*
6. 在**quiz-controller**文件中，添加以下代码以声明和初始化 AngularJS **QuizCtrl**控制器。

    （代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-AngularQuizController*）

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > **QuizCtrl**控制器的构造函数需要一个名为 **$scope**的 injectable 参数。 应通过将属性附加到 **$scope**对象，在构造函数中设置作用域的初始状态。 属性包含**视图模型**，在注册控制器时，模板将可对其进行访问。
    > 
    > **QuizCtrl**控制器是在名为**QuizApp**的模块中定义的。 模块是工作单元，可让你将应用程序分解为单独的组件。 使用模块的主要优点是代码更易于理解，并简化了单元测试、可重用性和可维护性。
7. 现在，你将向范围中添加行为，以便对从视图触发的事件做出反应。 在**QuizCtrl**控制器的末尾添加以下代码，以定义 **$scope**对象中的**nextQuestion**函数。

    （代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-AngularQuizControllerNextQuestion*）

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > 此函数检索在上一练习中创建的**琐碎内容**Web API 中的下一个问题，并将问题数据附加到 **$scope**的对象。
8. 在**QuizCtrl**控制器的末尾插入以下代码，以定义 **$scope**对象中的**sendAnswer**函数。

    （代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-AngularQuizControllerSendAnswer*）

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > 此函数将用户选择的答案发送到**琐碎内容**Web API，并将结果存储在 **$scope**对象中（即，如果答案是正确的）。
    > 
    > 上面的**nextQuestion**和**SendAnswer**函数使用 AngularJS **$http**对象，通过浏览器中的 XMLHTTPREQUEST JavaScript 对象抽象与 Web API 的通信。 AngularJS 支持另一种服务，该服务提供更高级别的抽象，以通过 RESTful Api 对资源执行 CRUD 操作。 AngularJS **$resource**对象具有一些操作方法，这些方法可提供高级行为，而无需与 **$http**对象进行交互。 考虑在需要 CRUD 模型的情况下使用 **$resource**对象（有关信息，请参阅[$resource 文档](https://docs.angularjs.org/api/ngResource/service/$resource)）。
9. 下一步是创建定义测验视图的 AngularJS 模板。 为此，请打开视图中的**索引 cshtml**文件 **|Home**文件夹，并将内容替换为以下代码。

    （代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-GeekQuizView*）

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > AngularJS 模板是一种声明性规范，使用模型和控制器中的信息将静态标记转换为用户在浏览器中看到的动态视图。 下面是可在模板中使用的 AngularJS 元素和元素特性的示例：
    > 
    > - " **Ng-app** " 指令告诉 AngularJS 表示应用程序的根元素的 DOM 元素。
    > - 在声明指令的点， **ng 控制器**指令将控制器附加到 DOM。
    > - 大括号表示法 **{{}}** 表示在控制器中定义的作用域属性的绑定。
    > - 使用**ng-click**指令可调用在响应用户单击的范围内定义的函数。
10. 打开**Content**文件夹中的**web.config**文件，并在该文件的末尾添加以下突出显示的样式，以提供测验视图的外观和感觉。

    （代码段- *AspNetWebApiSpa-buildingappswithcachingservice-ex2-getproducts latency-cs-GeekQuizStyles*）

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a>任务2–运行解决方案

在此任务中，你将使用通过 AngularJS 生成的新用户界面来执行该解决方案，以解答一些测验问题。

1. 按 **“F5”** 运行该解决方案。
2. 注册新的用户帐户。 为此，请按照练习1，任务3中所述的注册步骤操作。

    > [!NOTE]
    > 如果使用上一练习中的解决方案，则可以使用之前创建的用户帐户登录。
3. 将显示 "**主页**"，其中显示了测验的第一个问题。 单击其中一个选项即可回答问题。 这会触发前面定义的**sendAnswer**函数，该函数将所选选项发送到**琐碎内容**Web API。

    ![回答问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "回答问题")

    *回答问题*
4. 单击其中一个按钮后，将出现答案。 单击 "**下一问题**" 以显示以下问题。 这会触发控制器中定义的**nextQuestion**函数。

    ![请求下一个问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "请求下一个问题")

    *请求下一个问题*
5. 接下来应该会出现问题。 根据需要继续回答问题。 完成所有问题后，应返回到第一个问题。

    ![其他问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "其他问题")

    *下一个问题*
6. 返回到 Visual Studio 并按**SHIFT + F5**停止调试。

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a>任务3–使用 CSS3 创建翻转动画

在此任务中，你将使用 CSS3 属性来执行丰富的动画，方法是在解答问题后，在检索到下一个问题时添加一个翻转效果。

1. 在**解决方案资源管理器**中，右键单击**GeekQuiz**项目的**Content**文件夹，然后选择 "**添加 |现有项 ...**

    ![将现有项添加到 Content 文件夹](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "将现有项添加到 Content 文件夹")

    *将现有项添加到 Content 文件夹*
2. 在 "**添加现有项**" 对话框中，导航到 "**源/资源**" 文件夹，然后选择 "**反向**"。 单击 **“添加”** 。

    ![从资产中添加 Flip .css 文件](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "从资产中添加 Flip .css 文件")

    *从资产中添加 Flip .css 文件*
3. 打开刚才添加的 "**翻转 .css** " 文件并检查其内容。
4. 找到**翻转转换**注释。 此注释下的样式使用 CSS**透视**和**rotateY**转换来生成 &quot;卡片翻转&quot; 效果。

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. 在 "翻转注释" 中找到 "**隐藏背面" 窗格**。 此注释下的样式通过将**隐**CSS 属性设置为*隐藏*，隐藏了正面朝远离查看器的面。

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. 在**应用\_启动**文件夹内打开**BundleConfig.cs**文件，并在 **&quot;~/Content/css&quot;** 样式捆绑包中添加对**文件的**引用

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. 按**F5**运行该解决方案，并以您的凭据登录。
8. 单击其中一个选项即可回答问题。 请注意在视图间转换时的翻转效果。

    ![使用反转效果回答问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "使用反转效果回答问题")

    *使用反转效果回答问题*
9. 单击 "**下一问题**" 以检索以下问题。 翻转效果应再次出现。

    ![检索以下带有翻转效果的问题](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "检索以下带有翻转效果的问题")

    *检索以下带有翻转效果的问题*

---

<a id="Summary"></a>
## <a name="summary"></a>摘要

通过完成本动手实验，你学习了如何：

- 使用 ASP.NET 基架创建 ASP.NET Web API 控制器
- 实现 Web API Get 操作以检索下一个测验问题
- 实现 Web API 后操作以存储测验答案
- 从 Visual Studio 包管理器控制台安装 AngularJS
- 实现 AngularJS 模板和控制器
- 使用 CSS3 转换执行动画效果
