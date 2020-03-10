---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: ASP.NET MVC 简介 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469796"
---
# <a name="intro-to-aspnet-mvc"></a>ASP.NET MVC 简介

作者： [Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 如果本教程可在[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，则为已更新的版本。 新教程使用 ASP.NET MVC 5，这在本教程中提供了许多改进。
>
>
> 本教程介绍了 ASP.NET MVC 的基本知识。 你将创建一个简单的 web 应用程序，用于读取和写入数据库。 请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。

让我们使用[Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/)创建第一个 ASP.NET MVC Web 应用程序。 我们会创建一个小电影列表应用程序，让我们创建和列出电影。

## <a name="what-youll-build"></a>你将生成

下面是要生成的应用程序的两个屏幕截图。 您将获得一个包含各种列的简单影片表。

[![电影列表-Windows Internet Explorer （12）](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

您将创建一个窗体，以便可以将电影添加到列表。

[![创建电影-Windows Internet Explorer （2）](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>将要学到的技能

本教程将介绍使用 Visual Studio 生成 ASP.NET MVC Web 应用程序的基础知识。 学习内容：

- 如何创建新的 ASP.NET MVC 项目
- 如何使用 SQL Server 创建新数据库
- 如何创建 ASP.NET MVC 控制器和视图
- 如何检索和显示数据
- 如何编辑数据和启用数据验证
- 如何更新数据库架构

## <a name="get-started"></a>开始操作

首先，运行 Visual Web Developer 2010 Express （我将从现在开始将其称为 "VWD"），然后从 "开始" 屏幕中选择 "新建项目"。

Visual Web Developer 是 IDE 或集成开发人员环境。 就像使用 Microsoft Word 编写文档，你将使用 IDE 来创建应用程序。 顶部有一个工具栏，其中显示了你可以使用的各种选项，以及你还可以用来选择文件的菜单 |新项目。

[Microsoft Visual Web Developer 2010 Express ![](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>创建第一个应用程序

可以使用 Visual Basic 或视觉对象C#创建应用程序。 现在，在左侧选择C# "视觉对象"，然后选择 "ASP.NET MVC 2 Web 应用程序"。 将项目命名为 "电影"，然后单击 "确定"。

[![新项目](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

右侧是解决方案资源管理器显示应用程序中的所有文件和文件夹。 您可以在中间的大窗口中编辑代码并花费大部分时间。 Visual Studio 使用了你刚刚创建的 ASP.NET MVC 项目的默认模板，因此你现在无需执行任何操作即可使用有效的应用程序！ 这是一个简单的 "Hello World！ 对于我们的应用程序来说，这是一个不错的开端。

[Microsoft Visual Web Developer 2010 Express ![](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

选择工具栏上的 "播放" 按钮。

![开始调试](getting-started-with-mvc-part1/_static/image11.png)

它是一个指向右侧的绿色箭头，将编译您的程序并在 web 浏览器中启动您的应用程序。

*注意：你可以在键盘上按 F5，或者从 "调试" 菜单中选择 "调试-&gt;启动调试"。*

这样，Visual Web Developer 就可以启动开发 web 服务器并运行 web 应用程序（启用此操作无需进行配置或手动步骤）。 然后，它将启动一个浏览器并将其配置为浏览应用程序的主页。 请注意，浏览器的地址栏显示 "localhost"，而不是类似于 "example.com" 的内容。 这是因为，localhost 始终指向你自己的本地计算机-在本例中，这种情况下运行的是刚刚构建的应用程序。

[![主页](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

此默认模板为你提供了两个要访问的页面和一个基本登录页。 让我们更改此应用程序的工作方式，并在此过程中了解有关 ASP.NET MVC 的一些相关信息。 关闭浏览器并更改某些代码。

> [!div class="step-by-step"]
> [下一部分](getting-started-with-mvc-part2.md)
