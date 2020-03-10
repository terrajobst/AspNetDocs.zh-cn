---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 （C#）简介Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434726"
---
# <a name="intro-to-aspnet-mvc-3-c"></a>ASP.NET MVC 3 简介 (C#)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > [此处](../../../getting-started/introduction/getting-started.md)提供了本教程的更新版本，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全的方法是遵循更多功能，并演示更多的功能。
> 
> 
> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题提供了包含C#源代码的 Visual Web Developer 项目。 [下载C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果希望 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。

## <a name="what-youll-build"></a>你将生成

您将实现一个简单的电影列表应用程序，该应用程序支持从数据库创建、编辑和列出影片。 下面是要生成的应用程序的两个屏幕截图。 它包含一个页面，其中显示了数据库中的电影列表：

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

应用程序还可用于添加、编辑和删除电影，以及查看有关单个影片的详细信息。 所有数据输入方案都包括验证，以确保数据库中存储的数据是正确的。

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a>将要学到的技能

学习内容：

- 如何创建新的 ASP.NET MVC 项目。
- 如何创建 ASP.NET MVC 控制器和视图。
- 如何使用实体框架 Code First 范例创建新数据库。
- 如何检索和显示数据。
- 如何编辑数据和启用数据验证。

## <a name="getting-started"></a>入门

首先运行 Visual Web Developer 2010 Express （"Visual Web Developer"），并从 "**开始**" 页选择 "**新建项目**"。

Visual Web Developer 是一个 IDE 或集成开发环境。 就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。 在 Visual Web Developer 中，顶部有一个工具栏，其中显示了可供你使用的各种选项。 还有一个菜单，该菜单提供了在 IDE 中执行任务的另一种方法。 （例如，可以使用菜单并选择 "**文件**" &gt; "**新建项目**"，而不是从**起始**页中选择 "**新建项目**"。）

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a>创建第一个应用程序

您可以使用 Visual Basic 或 Visual C#作为编程语言来创建应用程序。 选择左侧C#的 "视觉对象"，然后选择 " **ASP.NET MVC 3 Web 应用程序**"。 将项目命名为 "MvcMovie"，然后单击 **"确定**"。 （如果你喜欢 Visual Basic，请切换到本教程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。）

![](intro-to-aspnet-mvc-3/_static/image5.png)

在 "**新建 ASP.NET MVC 3 项目**" 对话框中，选择 " **Internet 应用程序**"。 选中 "**使用 HTML5 标记**并将**Razor**保留为默认视图引擎"。

![](intro-to-aspnet-mvc-3/_static/image6.png)

单击“确定”。 Visual Web Developer 使用您刚创建的 ASP.NET MVC 项目的默认模板，因此您现在无需执行任何操作即可使用有效的应用程序！ 这是一个简单的 "Hello World！" 项目，这是启动应用程序的好地方。

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

从“调试”菜单中选择“启动调试”。

![](intro-to-aspnet-mvc-3/_static/image9.png)

请注意，启动调试的键盘快捷方式是 F5。

使用 F5，Visual Web Developer 可以启动开发 web 服务器并运行您的 web 应用程序。 然后，Visual Web Developer 会启动浏览器并打开应用程序的主页。 请注意，浏览器的地址栏会显示 `localhost`，而不是类似 `example.com`。 这是因为 `localhost` 始终指向您自己的本地计算机，在本例中，该计算机运行刚构建的应用程序。 当 Visual Web Developer 运行 web 项目时，会将随机端口用于 web 服务器。 在下图中，随机端口号为43246。 运行应用程序时，可能会看到不同的端口号。

![](intro-to-aspnet-mvc-3/_static/image10.png)

右侧此默认模板提供两个要访问的页面和一个基本登录页。 下一步是更改此应用程序的工作方式，并在此过程中了解有关 ASP.NET MVC 的一些相关信息。 关闭浏览器并更改某些代码。

> [!div class="step-by-step"]
> [下一部分](adding-a-controller.md)
