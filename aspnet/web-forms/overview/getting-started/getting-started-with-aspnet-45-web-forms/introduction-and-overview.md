---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: 入门 ASP.NET 4.7 Web 窗体和 Visual Studio 2017 |Microsoft Docs
author: Erikre
description: 此循序渐进教程系列将指导你使用 ASP.NET 4.7 和 Microsoft Visual Studio 构建 ASP.NET Web 窗体应用程序的基础知识
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615456"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a>与 ASP.NET 4.5 Web 窗体和 Visual Studio 2017 入门

[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

本系列教程演示如何使用 ASP.NET 4.5 和 Microsoft Visual Studio 2017 生成 ASP.NET Web 窗体应用程序。 

## <a name="introduction"></a>简介

本教程系列将指导你使用 Visual Studio 2017 和 ASP.NET 4.5 创建 ASP.NET Web 窗体应用程序。 你将创建一个名为 " **Wingtip 玩具**" 的应用程序，它是一个可联机销售项目的简化店面网站。 在序列中，将突出显示新的 ASP.NET 4.5 功能。

### <a name="target-audience"></a>目标受众

对于 ASP.NET Web 窗体，开发人员是本系列教程的目标受众。

你应了解以下几个方面的知识：

- 面向对象的编程（OOP）和语言
- Web 开发（HTML、CSS、JavaScript）
- 关系数据库
- N 层体系结构

若要查看这些区域，请考虑学习以下内容：

- [Visual C# 入门](https://msdn.microsoft.com/library/a72418yk.aspx)
- [Web 开发](https://msdn.microsoft.com/beginner/bb308760.aspx)， [HTML，CSS，JavaScript，SQL，PHP，JQuery](http://w3schools.com/)
- [关系数据库](http://en.wikipedia.org/wiki/Relational_database)
- [多层体系结构](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a>应用程序功能

本系列中介绍的 ASP.NET Web 窗体功能包括：

- Web 应用程序项目（而非网站项目）
- Web Forms — Web 窗体
- 母版页，配置
- Bootstrap
- 实体框架 Code First，LocalDB
- 请求验证
- 强类型数据控件
- 模型绑定
- 数据注释
- 值提供程序
- SSL 和 OAuth
- ASP.NET Identity、配置和授权
- 非引人注目验证
- 路由
- ASP.NET 错误处理

### <a name="application-scenarios-and-tasks"></a>应用程序方案和任务

教程系列任务包括：

- 创建、查看和运行新项目
- 创建数据库结构
- 初始化和播种数据库
- 使用样式、图形和母版页自定义 UI
- 添加页面和导航
- 显示菜单详细信息和产品数据
- 创建购物车
- 添加 SSL 和 OAuth 支持
- 添加付款方式
- 包括管理员角色和应用程序的用户
- 限制对特定页面和文件夹的访问
- 将文件上传到 web 应用程序
- 实现输入验证
- 注册 web 应用程序的路由
- 实现错误处理和错误日志记录

## <a name="overview"></a>概述

本教程系列适用于熟悉编程概念的人员，但却是 ASP.NET Web 窗体的新手。 如果已熟悉 ASP.NET Web 窗体，此系列仍可帮助你了解新的 ASP.NET 4.5 功能。 对于不熟悉编程概念和 ASP.NET Web 窗体的读者，请参阅 ASP.NET 网站上的[入门](../../../index.md)部分中提供的其他 Web 窗体教程。

本系列教程提供了 ASP.NET 4.5，其中包含以下功能：

- 用于创建[支持多个 ASP.NET 框架](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add)（Web 窗体、MVC 和 Web API）的项目的简单 UI。
- [启动](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap)、布局、主题和响应式设计框架。
- [ASP.NET Identity](../../../../identity/index.md)，这是一个新的 ASP.NET 成员资格系统，该系统在所有 ASP.NET 框架中运行相同的功能，并且适用于除 IIS 之外的 web 托管软件。
- [Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)

  更新实体框架使你能够：
  - 作为强类型对象检索和操作数据
  - 异步访问数据
  - 处理暂时性连接故障
  - 记录 SQL 语句

有关完整的 ASP.NET 4.5 功能列表，请参阅[Visual Studio 2013 发行说明 ASP.NET 和 Web 工具](../../../../visual-studio/overview/2013/release-notes.md)。

### <a name="the-wingtip-toys-sample-application"></a>Wingtip 玩具示例应用程序

以下屏幕截图来自您在本教程系列中创建的 ASP.NET Web 窗体应用程序。 在 Visual Studio 中运行应用程序时，将显示以下 web 主页。

![Wingtip 玩具-默认页面](introduction-and-overview/_static/image1.png)

你可以注册为新用户或以现有用户身份登录。 顶部导航栏中提供了来自数据库的产品类别和产品的链接。

如果选择 "**产品**"，则会显示所有可用的产品。 

![Wingtip 玩具-产品](introduction-and-overview/_static/image2.png)

如果选择特定产品，则将显示产品详细信息。

![Wingtip 玩具-产品详细信息](introduction-and-overview/_static/image3.png)

用户可以使用 Web 窗体模板默认功能注册并登录。 本教程还介绍如何使用现有 Gmail 帐户登录。 此外，您可以以管理员身份登录，以便在数据库中添加和删除产品。

![Wingtip 玩具-登录](introduction-and-overview/_static/image4.png)

以用户身份登录后，可以将产品添加到购物车，并使用 PayPal 结帐。 该示例应用程序设计用于在 PayPal 的开发人员沙盒中运行。 不会进行实际的 money 交易。

![Wingtip 玩具-购物车](introduction-and-overview/_static/image5.png)

PayPal 确认你的帐户、订单和付款信息。

![Wingtip 玩具-PayPal](introduction-and-overview/_static/image6.png)

从 PayPal 返回后，你可以查看并完成你的订单。

![Wingtip 玩具-订购审核](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a>先决条件

在开始之前，请确保已在计算机上安装以下软件：

- [Microsoft Visual Studio 2017 或 Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/)。

将自动安装 .NET Framework。

本教程系列使用 Microsoft Visual Studio Community 2017。 您可以使用该方法或 Microsoft Visual Studio 2017 来完成本系列教程。

请注意以下关于 Visual Studio 的内容：

* 在本系列教程中，Microsoft Visual Studio 2017 和 Microsoft Visual Studio Community 2017 称为*Visual Studio* 。

* Visual Studio 2017 安装在已安装的任何较旧版本旁边。 可在 Visual Studio 2017 中打开在早期版本中创建的网站，并在以前的版本中继续打开。

* 首次启动 Visual Studio 时，会假定你选择了*Web 开发*设置。 有关详细信息，请参阅[如何：选择 Web 开发环境设置](https://msdn.microsoft.com/library/ff521558.aspx)。

安装必备组件后，您就可以开始创建本教程系列中介绍的 Web 项目了。

## <a name="download-the-sample-application"></a>下载示例应用程序

 你可以随时从 MSDN 示例站点下载已完成的示例应用程序：

[与 ASP.NET 4.5 Web 窗体和 Visual Studio 2013-Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）入门 

 此下载包含以下各项：

- *WingtipToys*文件夹中的示例应用程序。
- 用于在*WingtipToys*文件夹中的*WingtipToys*文件夹中创建示例应用程序的资源。

下载文件为 *.zip*文件。 若要查看本教程系列创建的已完成项目，请在 .zip *C#* 文件中找到并选择该文件夹。 将C#文件夹保存到用于使用 Visual Studio 项目的文件夹中。 默认情况下，Visual Studio 2017 项目文件夹为：

<strong>C:\Users&#92;</strong>  <strong><em>&lt;用户名&gt;</em></strong> <strong>\source\repos</strong>

将***C#*** 文件夹重命名为***WingtipToys***。

> [!NOTE]
> 如果项目文件夹中已有一个名为*WingtipToys*的文件夹，请在将*C#* 文件夹重命名为*WingtipToys*之前暂时重命名该现有文件夹。

若要运行已完成的项目，请打开*WingtipToys*文件夹，然后双击*WingtipToys*文件。 Visual Studio 2017 打开项目。 接下来，在**解决方案资源管理器**中右键单击*default.aspx*文件，然后选择 **"在浏览器中查看"** 。

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a>参加 ASP.NET Web Forms 测验以查看内容

完成本系列教程后，请进行测验来测试您的知识和强化关键概念。 每个问题都提供了说明和指向其他指南的链接。

* [ASP.NET Web 窗体测验](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a>教程支持和注释

对于问题和意见，请使用入门中包含的 Q 和部分，[其中包含 ASP.NET 4.5 Web Forms 和 Visual Studio 2013-Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）示例页面。

欢迎使用本系列教程上的评论。 更新本系列教程后，每次都要考虑更正或改进建议。

如果发生错误，相应的错误消息可能会令人困惑，并没有关于如何修复此问题的好说明。 若要获得帮助，你可以查看[ASP.NET 论坛](https://forums.asp.net/)。 另一种好的来源是[入门使用 ASP.NET 4.5 Web 窗体和 Visual Studio 2013 Wingtip 玩具](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)（C#）示例页的 "问答" 部分。 

> [!div class="step-by-step"]
> [下一页](create-the-project.md)
