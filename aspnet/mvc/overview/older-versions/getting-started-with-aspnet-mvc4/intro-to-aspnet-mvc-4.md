---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: ASP.NET MVC 4 简介 |Microsoft Docs
author: Rick-Anderson
description: 如果本教程可在此处使用 Visual Studio 2013，则为已更新的版本。 新教程使用 ASP.NET MVC 5，它对 t 。
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51709a9c6ddb39b8fcd1cd94cd08d530a595825a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485276"
---
# <a name="intro-to-aspnet-mvc-4"></a>ASP.NET MVC 4 简介

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 如果本教程可在[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，则为已更新的版本。 新教程使用 ASP.NET MVC 5，这在本教程中提供了许多改进。
>
> 本教程将教你使用 Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)或 Visual Web Developer 2010 Express Service Pack 1 构建 ASP.NET MVC 4 Web 应用程序的基础知识。 建议使用 Visual Studio 2012，无需安装任何内容即可完成本教程。 如果你使用的是 Visual Studio 2010，则必须安装以下组件。 可以通过单击以下链接安装所有这些程序：
>
> - [Visual Studio Web Developer Express SP1 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 4 的 WPI 安装程序](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [SSDT](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
>
> 如果你使用的是 Visual Studio 2010 而不是 Visual Web Developer 2010，请安装[适用于 ASP.NET MVC 4 的 WPI 安装程序](https://go.microsoft.com/fwlink/?LinkId=243392)和： [Visual Studio 2010 必备组件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
>
> 本主题提供了包含C#源代码的 Visual Web Developer 项目。 [下载C#版本](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip)。
>
> 在本教程中，你将在 Visual Studio 中运行应用程序。 还可以通过将应用程序部署到托管提供程序来使应用程序在 Internet 上可用。 Microsoft 在免费的 microsoft [Azure 试用帐户](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中为多达10个网站提供免费的 web 托管。 有关如何将 Visual Studio web 项目部署到 Microsoft Azure 网站的信息，请参阅[使用 Visual Studio 创建和部署 ASP.NET 网站和 SQL 数据库](https://docs.microsoft.com/dotnet/azure/)。 该教程还演示了如何使用 Entity Framework Code First 迁移将 SQL Server 数据库部署到 Microsoft Azure SQL 数据库（以前称为 SQL Azure）。
>
> 本教程由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）编写。

## <a name="what-youll-build"></a>你将生成

> [!NOTE]
> 如果本教程可在[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，则为已更新的版本。 新教程使用 ASP.NET MVC 5，这在本教程中提供了许多改进。

您将实现一个简单的电影列表应用程序，该应用程序支持从数据库创建、编辑、搜索和列出影片。 下面是要生成的应用程序的两个屏幕截图。 它包含一个页面，其中显示了数据库中的电影列表：

![](intro-to-aspnet-mvc-4/_static/image1.png)

应用程序还可用于添加、编辑和删除电影，以及查看有关单个影片的详细信息。 所有数据输入方案都包括验证，以确保数据库中存储的数据是正确的。

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a>入门

首先运行 Visual Studio Express 2012 或 Visual Web Developer 2010 Express。 此系列中的大部分屏幕快照都使用 Visual Studio Express 2012，但你可以使用 Visual Studio 2010/SP1、Visual Studio 2012、Visual Studio Express 2012 或 Visual Web Developer 2010 Express 来完成本教程。 从**起始**页中选择 "**新建项目**"。

Visual Studio 是一个 IDE，或集成的开发环境。 就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。 在 Visual Studio 中，顶部有一个工具栏，其中显示了可供你使用的各种选项。 还有一个菜单，该菜单提供了在 IDE 中执行任务的另一种方法。 （例如，可以使用菜单并选择 "**文件**" &gt; "**新建项目**"，而不是从**起始**页中选择 "**新建项目**"。）

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a>创建第一个应用程序

您可以使用 Visual Basic 或 Visual C#作为编程语言来创建应用程序。 选择左侧C#的 "视觉对象"，然后选择 " **ASP.NET MVC 4 Web 应用程序**"。 将项目命名为 &quot;MvcMovie&quot; 然后单击 **"确定"** 。

![](intro-to-aspnet-mvc-4/_static/image4.png)

在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**"。 保留**Razor**作为默认视图引擎。

![](intro-to-aspnet-mvc-4/_static/image5.png)

单击“确定”。 Visual Studio 使用了你刚刚创建的 ASP.NET MVC 项目的默认模板，因此你现在无需执行任何操作即可使用有效的应用程序！ 这是一个简单的 &quot;Hello World！&quot; 项目，它是启动应用程序的好地方。

![](intro-to-aspnet-mvc-4/_static/image6.png)

从“调试”菜单中选择“启动调试”。

![](intro-to-aspnet-mvc-4/_static/image7.png)

请注意，启动调试的键盘快捷方式是 F5。

F5 会使 Visual Studio 启动 IIS Express 并运行你的 web 应用程序。 然后，Visual Studio 会启动浏览器并打开应用程序的主页。 请注意，浏览器的地址栏会显示 `localhost`，而不是类似 `example.com`。 这是因为 `localhost` 始终指向您自己的本地计算机，在本例中，该计算机运行刚构建的应用程序。 当 Visual Studio 运行 web 项目时，会将随机端口用于 web 服务器。 在下图中，端口号为41788。 运行应用程序时，可能会看到不同的端口号。

![](intro-to-aspnet-mvc-4/_static/image8.png)

立即将此默认模板提供给你的 "主页"、"联系人" 和 "关于" 页。 它还支持注册和登录，并提供到 Facebook 和 Twitter 的链接。 下一步是更改此应用程序的工作原理，并了解 ASP.NET MVC 的一些相关信息。 关闭浏览器并更改某些代码。

> [!div class="step-by-step"]
> [下一部分](adding-a-controller.md)
