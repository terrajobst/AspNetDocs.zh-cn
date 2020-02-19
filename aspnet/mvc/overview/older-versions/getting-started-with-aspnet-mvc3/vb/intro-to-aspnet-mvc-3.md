---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: ASP.NET MVC 3 简介（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC Web 应用程序的基础知识 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 24f7de303ef7f5a457bd509ecc6bd0e3be7e3d9d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456300"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a>ASP.NET MVC 3 简介 (VB)

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：
> 
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）
> 
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。
> 
> 本主题附带有 VB.NET 源代码的 Visual Web Developer 项目。 [下载 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。 如果愿意C#，请切换到本教程的[ C#版本](../cs/intro-to-aspnet-mvc-3.md)。

本教程将教你如何使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 （Microsoft Visual Studio 免费版）生成 ASP.NET MVC Web 应用程序的基础知识。 在开始之前，请确保已安装下列必备组件。 可以通过单击以下链接安装所有这些[程序： Web 平台安装程序](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。 或者，你可以使用以下链接单独安装必备组件：

- [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 工具更新](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（运行时 + 工具支持）

如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请通过单击以下链接安装必备组件： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。

本主题提供了包含 VB 源代码的 Visual Web Developer 项目。 [在此处下载 VB 版本](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824)。 如果你更愿意使用 CSharp，请切换到此教程的[CSharp 版本](../cs/intro-to-aspnet-mvc-3.md)。

## <a name="what-youll-build"></a>所需操作

您将实现一个简单的电影列表应用程序，该应用程序支持从数据库创建、编辑和列出影片。 下面是要生成的应用程序的两个屏幕截图。 它包含一个页面，其中显示了数据库中的电影列表：

[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)

应用程序还可用于添加、编辑和删除电影，以及查看有关单个影片的详细信息。 所有数据输入方案都包括验证，以确保数据库中存储的数据是正确的。

[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="skills-youll-learn"></a>将要学到的技能

学习内容：

- 如何创建新的 ASP.NET MVC 项目
- 如何使用实体框架代码优先创建新数据库
- 如何创建 ASP.NET MVC 控制器和视图
- 如何检索和显示数据
- 如何编辑数据和启用数据验证

## <a name="getting-started"></a>入门

首先运行 Visual Web Developer 2010 Express （简称 "VWD"），然后从**起始**页中选择 "**新建项目**"。

Visual Web Developer 是一个 IDE 或集成开发环境。 就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。 在 Visual Web Developer 中，顶部有一个工具栏，其中显示了可供你使用的各种选项。 还有一个菜单，该菜单提供了在 IDE 中执行任务的另一种方法。 （例如，可以使用菜单并选择 "**文件**" &gt; "**新建项目**"，而不是从**起始**页中选择 "**新建项目**"。）

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a>创建第一个应用程序

您可以使用您选择的 Visual Basic 或 Visual C#作为编程语言来创建应用程序。 对于本教程，请选择左侧 Visual Basic，然后选择 " **ASP.NET MVC 3 Web 应用程序**"。 将项目命名为 "MvcMovie"，然后单击 **"确定**"。

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

在 "**新建 ASP.NET MVC 3 项目**" 对话框中，选择 " **Internet 应用程序**"。 保留**Razor**作为默认视图引擎。

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

单击“确定”。 Visual Web Developer 使用您刚创建的 ASP.NET MVC 项目的默认模板，因此您现在无需执行任何操作即可使用有效的应用程序！ 这是一个简单的 "Hello World！" 项目，这是启动应用程序的好地方。

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

从“调试”菜单中选择“启动调试”。

![](intro-to-aspnet-mvc-3/_static/image11.png)

请注意，启动调试的键盘快捷方式是 F5。

使用 F5，Visual Web Developer 可以启动开发 web 服务器并运行您的 web 应用程序。 然后，VWD 启动浏览器并打开应用程序的主页。 请注意，浏览器的地址栏会显示 `localhost`，而不是类似 `example.com`。 这是因为 `localhost` 始终指向您自己的本地计算机，在本例中，该计算机运行刚构建的应用程序。 当 VWD 运行 web 项目时，该项目将使用一个随机端口。 在下图中，随机端口号为43246。 你的项目可能会使用其他端口号。

![](intro-to-aspnet-mvc-3/_static/image12.png)

此默认模板为你提供了两个要访问的页面和一个基本登录页。 让我们更改此应用程序的工作方式，并在此过程中了解有关 ASP.NET MVC 的一些相关信息。 关闭浏览器并更改某些代码。

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)
