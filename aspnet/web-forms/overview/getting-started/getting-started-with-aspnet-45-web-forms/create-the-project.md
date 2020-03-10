---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
title: 创建项目 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 2ce36f78-8ecb-4ab1-b748-6d0ab633ea3f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create-the-project
msc.type: authoredcontent
ms.openlocfilehash: 62918b17f42e54dfe4e45a08927b1039dcbb7012
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78461570"
---
# <a name="create-the-project"></a>创建项目

作者： [Erik Reitan](https://github.com/Erikre)

[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。 此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。

在本教程中，你将在 Visual Studio 中创建、查看和运行默认项目，这将允许你熟悉 ASP.NET 的功能。 此外，你将查看 Visual Studio 环境。

## <a name="what-youll-learn"></a>学习内容：

- 如何创建新的 Web 窗体项目。
- Web 窗体项目的文件结构。
- 如何在 Visual Studio 中运行项目。
- 默认 Web 窗体应用程序的不同功能。
- 有关如何使用 Visual Studio 环境的一些基础知识。

## <a name="creating-the-project"></a>创建项目

1. 打开 Visual Studio。
2. 从 Visual Studio 中的 "**文件**" 菜单选择 "**新建项目**"。 

    ![创建项目-"新建项目" 菜单项](create-the-project/_static/image1.png)
3. 选择左侧的 "**模板**" -&gt; **Visual C#**  -&gt; **Web**模板 "组。
4. 在中心列中选择 " **ASP.NET Web 应用程序**" 模板。  
 本教程系列使用 .NET Framework 4.5.2。
5. 将项目命名为*WingtipToys* ，然后选择 **"确定"** 按钮。 

    ![创建项目-"新建项目" 对话框](create-the-project/_static/image2.png)

    > [!NOTE]
    > 本系列教程中的项目名称为**WingtipToys**。 建议使用此*准确*的项目名称，使整个教程系列提供的代码按预期方式工作。

6. 单击“ **更改身份验证** ”按钮。 选择**单个用户帐户**，然后单击 **"确定"** 按钮。

7. 选择 " **Web 窗体**" 模板，然后单击 "**确定"** 按钮。

    ![创建项目-新建项目模板](create-the-project/_static/image3.png)

该项目将需要一些时间来创建。 准备就绪后，打开 " **default.aspx** " 页。

![创建项目-新建项目模板](create-the-project/_static/image4.png)

您可以通过选择中心窗口底部的选项在 "**设计**" 视图和 "**源**" 视图之间切换。 "**设计**" 视图使用接近 WYSIWYG 的视图显示 ASP.NET 网页、母版页、内容页、HTML 页和用户控件。 "**源**" 视图显示您的网页的 HTML 标记，您可以对其进行编辑。

> [!TIP] 
> 
> **了解 ASP.NET 框架**
> 
> 使用 ASP.NET Web 窗体，可以使用熟悉的拖放事件驱动模型来构建动态网站。 利用设计图面以及许多控件和组件，你可以迅速生成带有数据访问的高级的、功能强大的 UI 驱动型网站。 Wingtip 玩具商店基于 ASP.NET Web 窗体，但你在本教程系列中学到的许多概念都适用于所有 ASP.NET。
> 
> ASP.NET 提供四种主要开发框架：
> 
> - [ASP.NET Web 窗体](../../../index.md)  
>  Web 窗体框架面向更喜欢声明性和基于控件的编程的开发人员，如 Microsoft Windows 窗体（WinForms）和 WPF/XAML/Silverlight。 它提供了 WYSIWYG 设计器驱动开发模型，使开发人员在寻找适用于 web 开发的快速应用程序开发（RAD）环境时受欢迎。 如果你不熟悉 web 编程，并熟悉传统的 Microsoft RAD 客户端开发工具（例如，对于 Visual Basic 和视觉对象C#），则可以快速构建 web 应用程序，而无需使用 HTML 和 JavaScript。
> - [ASP.NET MVC](../../../../mvc/index.md)  
>  ASP.NET MVC 面向对模式和原理感兴趣的开发人员，如测试驱动开发、问题分离、控制反转（IoC）和依赖关系注入（DI）。 此框架鼓励 web 应用程序的业务逻辑层与其表示层分离。
> - [ASP.NET 网页](../../../../web-pages/index.md)  
>  ASP.NET 网页面向需要简单的 Web 开发案例的开发人员，以及 PHP 的各行。 在 "网页" 模型中，您将创建 HTML 页，然后将基于服务器的代码添加到页面，以便动态控制该标记的呈现方式。 网页专门设计为一个轻型框架，对于知道 HTML 但可能没有广泛编程体验（例如学生或爱好者）的用户来说，它是 ASP.NET 的最简单的入口点。 这也是一种很好的方法，适用于知道 PHP 或类似框架开始使用 ASP.NET 的 web 开发人员。
> - [ASP.NET 单页面应用程序](../../../../single-page-application/index.md)  
>  ASP.NET 单页应用程序（SPA）可帮助你使用 HTML 5、CSS 3 和 JavaScript 构建包含重要客户端交互的应用程序。 ASP.NET 和 Web 工具2012.2 更新提供了一个新模板，用于使用挖空和 ASP.NET Web API 生成单页面应用程序。 除了新的 SPA 模板以外，还可下载新的社区创建的 SPA 模板。
> 
> 除了四个主要的开发框架外，ASP.NET 还提供了一些重要的技术，这些技术对于了解和熟悉，而且不在本系列教程中进行介绍：
> 
> - [ASP.NET Web API](../../../../web-api/index.md) -一种框架，用于构建可访问范围广泛的客户端（包括浏览器和移动设备）的 HTTP 服务。
> - [ASP.NET SignalR](../../../../signalr/index.md) -可以轻松开发实时 web 功能的库。

### <a name="reviewing-the-project"></a>查看项目

在 Visual Studio 中，"**解决方案资源管理器**" 窗口使你可以管理项目的文件。 让我们看看**解决方案资源管理器**中已添加到应用程序中的文件夹。 Web 应用程序模板添加基本文件夹结构：

![创建项目-解决方案资源管理器](create-the-project/_static/image5.png)

Visual Studio 将为你的项目创建一些初始文件夹和文件。 稍后将在本教程中使用的第一个文件如下所示：

| **文件** | **目的** |
| --- | --- |
| *Default.aspx* | 通常是在浏览器中运行应用程序时显示的第一页。 |
| *站点主* | 允许您为应用程序中的页面创建一致的布局和使用标准行为的页面。 |
| *Global.asax* | 一个可选文件，其中包含用于响应由 ASP.NET 或 HTTP 模块引发的应用程序级事件和会话级事件的代码。 |
| *Web.config* | 应用程序的配置数据。 |

### <a name="running-the-default-web-application"></a>运行默认的 Web 应用程序

默认 Web 应用程序基于内置功能和支持提供丰富的体验。 如果不更改默认 Web 窗体项目，应用程序就可以在本地 Web 浏览器上运行。

1. 在 Visual Studio 中按***F5***键。   
 应用程序将在你的 Web 浏览器中生成和显示。  

    ![创建项目-默认页面](create-the-project/_static/image6.png)
2. 完成检查正在运行的应用程序后，请关闭浏览器窗口。

此默认 Web 应用程序中有三个主要页面 *： default.aspx* （Home）、 *About*和 *.aspx*。 可以从顶部导航栏中访问每个页面。 帐户文件夹中还有两个附加页面，即 "注册 .aspx" 页和 "登录 .aspx" 页。 这两个页面允许你使用 ASP.NET 的成员资格功能来创建、存储和验证用户凭据。

## <a name="aspnet-web-forms-background"></a>ASP.NET Web 窗体背景

ASP.NET Web 窗体是基于 Microsoft ASP.NET 技术的页面，在这些页面中，服务器上运行的代码会将网页输出动态生成到浏览器或客户端设备。 ASP.NET Web 窗体页自动为样式、布局等功能呈现正确的符合浏览器的 HTML。 Web 窗体兼容 .NET 公共语言运行时支持的任何语言，如 Microsoft Visual Basic 和 Microsoft 视觉对象C#。 而且，Web 窗体建立在[Microsoft .NET 框架](https://msdn.microsoft.com/vstudio/aa496123)之上，后者提供了托管环境、类型安全和继承等优点。

当 ASP.NET Web 窗体页运行时，该页面会经历一个生命周期，其中执行一系列处理步骤。 这些步骤包括初始化、实例化控件、还原和维护状态、运行事件处理程序代码以及呈现。 随着您对 ASP.NET Web 窗体的强大功能的熟悉，了解[ASP.NET 页面生命周期](https://msdn.microsoft.com/library/ms178472(v=vs.100).aspx)非常重要，这样您就可以在适当的生命周期阶段编写代码来实现所需的效果。

当 Web 服务器收到页请求时，它会查找该页，处理它，然后将其发送到浏览器，然后放弃所有页面信息。 如果用户再次请求同一页，服务器将重复整个序列，并从头开始重新处理页。 换句话说，服务器没有已处理的页的内存-页是无状态的。 ASP.NET 页框架自动处理维护页及其控件状态的任务，并提供了用于维护特定于应用程序的信息的状态的显式方法。

> [!TIP] 
> 
> **Web 窗体应用程序模板中的 web 应用程序功能**
> 
> ASP.NET Web 窗体应用程序模板提供一组丰富的内置功能。 它不但提供了一个*主页 .aspx*页面（一个*关于 .aspx*页面），还*提供了成员*资格功能，可注册用户并保存其凭据，使用户能够登录到你的网站。 此概述提供了有关 ASP.NET Web 窗体应用程序模板中包含的某些功能以及如何在 Wingtip 玩具应用程序中使用这些功能的详细信息。
> 
> **成员身份**
> 
> [ASP.NET](https://msdn.microsoft.com/library/yh26yfzy.aspx)标识将用户的凭据存储在由应用程序创建的数据库中。 当用户登录时，应用程序将通过读取数据库来验证凭据。 项目的*帐户*文件夹包含实现成员身份的各个部分的文件：注册、登录、更改密码和授权访问。 此外，ASP.NET Web 窗体支持 OAuth 和 OpenID。 这些身份验证增强功能允许用户使用现有凭据（来自 Facebook、Twitter、Windows Live 和 Google 等帐户）登录到你的站点。
> 
> ![创建项目-解决方案资源管理器（ASP.NET Identity）](create-the-project/_static/image7.png)
> 
> 默认情况下，模板使用默认数据库名称在 SQL Server Express LocalDB 的实例上创建成员资格数据库，该服务器附带了 Visual Studio Express 2013 for Web 的开发数据库服务器。
> 
> **SQL Server Express LocalDB**
> 
> [SQL Server Express LocalDB](https://technet.microsoft.com/library/hh510202.aspx)是 SQL Server 的轻型版本，它具有 SQL Server 数据库的多个可编程性功能。 SQL Server Express LocalDB 在用户模式下运行，并且具有快速的零配置安装，其中包含安装必备组件的简短列表。 在 Microsoft SQL Server 中，任何数据库或 Transact-sql 代码都可以从 SQL Server Express LocalDB 移到 SQL Server 和 SQL Azure，无需任何升级步骤。 因此，SQL Server Express LocalDB 可用作面向所有版本 SQL Server 的应用程序的开发人员环境。 SQL Server Express LocalDB 实现了一些功能，例如存储过程、用户定义函数和聚合、.NET Framework 集成、空间类型以及在 SQL Server Compact 中不可用的其他功能。
> 
> **母版页**
> 
> [ASP.NET 母版页](https://msdn.microsoft.com/library/wtxbf3hh.aspx)可为应用程序中的所有页面定义一致的外观和行为。 母版页的布局将与单个内容页中的内容合并，以生成用户看到的最后一页。 在 Wingtip 玩具应用程序中，你可以修改*网站。母版页*母版页，使 Wingtip 玩具网站中的所有页面共享相同的独特徽标和导航栏。
> 
> **HTML5**
> 
> ASP.NET Web 窗体应用程序模板支持[HTML5](http://www.w3schools.com/html/html5_intro.asp)，这是最新版本的 HTML 标记语言。 HTML5 支持有助于创建网站的新元素和功能。
> 
> **Modernizr**
> 
> 对于不支持 HTML5 的浏览器，可以使用[Modernizr](http://www.modernizr.com/)。 Modernizr 是一个开源 JavaScript 库，可以检测浏览器是否支持 HTML5 功能，如果不支持，则启用它们。 在 ASP.NET Web 窗体应用程序模板中，Modernizr 安装为 NuGet 包。
> 
> **Bootstrap**
> 
> Visual Studio 2013 项目模板使用由 Twitter 创建的[启动](http://getbootstrap.com/)、布局和主题框架。 启动使用 CSS3 来提供响应式设计，这意味着布局可以动态适应不同的浏览器窗口大小。 你还可以使用启动的主题功能轻松地对应用程序的外观进行更改。 默认情况下，Visual Studio 2013 中的 ASP.NET Web 应用程序模板包括作为 NuGet 包的启动。
> 
> **NuGet 包**
> 
> ASP.NET Web 窗体应用程序模板包含一组[NuGet](http://www.nuget.org/)包。 这些包以开源库和工具的形式提供组件化功能。 有多种包可帮助您创建和测试您的应用程序。 通过 Visual Studio，可以轻松地添加、删除和更新 NuGet 包。 开发人员也可以创建包并将其添加到 NuGet。
> 
> ![创建项目-NuGet 对话框](create-the-project/_static/image8.png)
> 
> 安装包时，NuGet 会将文件复制到解决方案，并自动进行任何所需的更改，如添加引用和更改与 Web 应用程序关联的配置。 如果决定删除库，NuGet 将删除文件并撤消在项目中所做的任何更改，以便不会留下混乱。 可以通过 Visual Studio 中的 "**工具**" 菜单获得 NuGet。
> 
> **jQuery**
> 
> [jQuery](http://jquery.com/)是一个快速而简洁的 JavaScript 库，可简化 HTML 文档遍历、事件处理、动画处理和 Ajax 交互，实现快速 web 开发。 JQuery JavaScript 库以 NuGet 包的形式包含在 ASP.NET Web 窗体应用程序模板中。
> 
> **非引人注目验证**
> 
> 内置的验证程序控件已配置为对客户端验证逻辑使用不引人注目的 JavaScript。 这可以显著减少在页面标记中以内联方式呈现的 JavaScript 数量，并减少总体页面大小。 根据应用程序根目录中的*web.config*文件 &lt;appSettings&gt; 元素中的设置，将非引人注目的验证全局添加到 ASP.NET Web 窗体应用程序模板。
> 
> **实体框架 Code First**
> 
> 除了 ASP.NET Web 窗体应用程序模板中的功能外，Wingtip 玩具应用程序还使用[实体框架 Code First](https://weblogs.asp.net/scottgu/archive/2010/12/08/announcing-entity-framework-code-first-ctp5-release.aspx)，这是一个 NuGet 库，用于在处理数据时实现以代码为中心的开发。 简单地说，它基于你编写的代码为你创建应用程序的数据库部分。 使用实体框架，你可以将数据作为强类型对象检索和操作。 这使你可以专注于应用程序中的业务逻辑，而不是访问数据访问方式的详细信息。
> 
> 有关 ASP.NET Web 窗体模板附带的已安装库和包的其他信息，请参阅已安装 NuGet 包的列表。 为此，请在 Visual Studio 中创建一个新的 Web 窗体项目，选择 "**工具**" > **Nuget 包管理器**" > **管理解决方案的 NuGet 包**"，然后在 "**管理 Nuget 包**" 对话框中选择 "**已安装的包**"。

### <a name="touring-visual-studio"></a>旅行 Visual Studio

Visual Studio 中的主窗口包括**解决方案资源管理器**、**服务器资源管理器**（在 Express 中**数据库资源管理器**）、"**属性" 窗口**、**工具箱**、**工具栏**和**文档窗口**。

![创建项目-NuGet 对话框](create-the-project/_static/image9.png)

有关 Visual Studio 的详细信息，请参阅 visual [Web Developer 的可视指南](https://msdn.microsoft.com/library/ee410104.aspx)。

## <a name="summary"></a>摘要

在本教程中，您已创建、查看并运行了默认的 Web 窗体应用程序。 你已查看默认 Web 窗体应用程序的不同功能，并了解有关如何使用 Visual Studio 环境的一些基础知识。 在以下教程中，将创建数据访问层。

## <a name="additional-resources"></a>其他资源

[选择正确的编程模型](../../../videos/how-do-i/choosing-the-right-programming-model.md)   
[Web 应用程序项目与网站项目](https://msdn.microsoft.com/library/dd547590.aspx)   
[ASP.NET Web 窗体页概述](https://msdn.microsoft.com/library/428509ah.aspx)

> [!div class="step-by-step"]
> [上一页](introduction-and-overview.md)
> [下一页](create_the_data_access_layer.md)
