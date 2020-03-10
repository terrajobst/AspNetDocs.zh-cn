---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 第1部分：概述和文件-> 新项目 |Microsoft Docs
author: jongalloway
description: 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第1部分介绍了概述和文件 > 的新项目。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451280"
---
# <a name="part-1-overview-and-file-new-project"></a>第1部分：概述和文件-> 新项目

作者： [Jon Galloway](https://github.com/jongalloway)

> MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和 Visual Studio 进行 web 开发。  
>   
> MVC 音乐应用商店是一种轻型示例存储实现，它可以在线销售音乐专辑，并实现基本的网站管理、用户登录和购物车功能。  
>   
> 本教程系列详细介绍了生成 ASP.NET MVC 音乐应用商店示例应用程序所需执行的所有步骤。 第1部分介绍了概述和文件&gt;的新项目。

## <a name="overview"></a>概述

MVC 音乐应用商店是一个教程应用程序，该应用程序逐步介绍了如何使用 ASP.NET MVC 和用于 web 开发的 Visual Web Developer。 我们将启动缓慢，因此初级级别的 web 开发体验一切正常。

我们要构建的应用程序是一个简单的音乐应用商店。 应用程序有三个主要部分：购物、结帐和管理。

![](mvc-music-store-part-1/_static/image1.jpg)

访问者可以按流派浏览唱片集：

![](mvc-music-store-part-1/_static/image2.jpg)

他们可以查看单个唱片集并将其添加到购物车中：

![](mvc-music-store-part-1/_static/image3.jpg)

他们可以检查购物车，删除不再需要的任何项目：

![](mvc-music-store-part-1/_static/image4.jpg)

继续结帐会提示他们登录或注册用户帐户。

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

创建帐户后，他们可以通过填写发货和付款信息来完成订单。 为简单起见，我们正在运行精彩升级：如果他们输入促销代码 "免费"，则一切免费！

![](mvc-music-store-part-1/_static/image5.jpg)

排序后，他们会看到一个简单的确认屏幕：

![](mvc-music-store-part-1/_static/image6.jpg)

除了面向客户的页面之外，我们还将生成一个 "管理员" 部分，其中显示了管理员可从中创建、编辑和删除唱片集的相册列表：

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a>1. 文件-&gt; 新项目

### <a name="installing-the-software"></a>安装软件

本教程将使用免费的 Visual Web Developer 2010 Express （免费）创建新的 ASP.NET MVC 3 项目，然后我们将以增量方式添加功能，以创建完整的正常运行的应用程序。 在此过程中，我们将介绍数据库访问、窗体发布方案、数据验证、使用母版页实现一致的页面布局、使用 AJAX 进行页面更新和验证、用户登录等等。

可以按照步骤进行操作，也可以从[MVC-音乐商店](https://github.com/evilDave/MVC-Music-Store)下载已完成的应用程序。

可以使用 Visual Studio 2010 SP1 或 Visual Web Developer 2010 Express SP1 （Visual Studio 2010 的免费版本）来生成应用程序。 我们将使用 SQL Server Compact （也是免费）来托管数据库。 在开始之前，请确保已安装下列必备组件。

- [Visual Studio Web Developer Express SP1 先决条件]
- [ASP.NET MVC 3 工具更新]
- [SQL Server Compact 4.0]-包括运行时和工具支持

### <a name="creating-a-new-aspnet-mvc-3-project"></a>创建新的 ASP.NET MVC 3 项目

首先，在 Visual Web Developer 的 "文件" 菜单中选择 "新建项目"。 此时将打开 "新建项目" 对话框。

![](mvc-music-store-part-1/_static/image5.png)

选择左侧的 "视觉C#&gt; Web 模板" 组，然后在 "中心" 列中选择 "ASP.NET MVC 3 Web 应用程序" 模板。 将项目命名为 MvcMusicStore，然后按 "确定" 按钮。

![](mvc-music-store-part-1/_static/image8.jpg)

这将显示一个辅助对话框，使我们可以为项目创建一些 MVC 特定的设置。 选择以下项：

项目模板-选择空

查看引擎-选择 Razor

使用 HTML5 语义标记-已选中

验证你的设置如下所示，然后按 "确定" 按钮。

![](mvc-music-store-part-1/_static/image9.jpg)

这将创建项目。 让我们看看在右侧的解决方案资源管理器中已添加到应用程序中的文件夹。

![](mvc-music-store-part-1/_static/image10.jpg)

空 MVC 3 模板不完全为空-它会添加基本文件夹结构：

![](mvc-music-store-part-1/_static/image6.png)

ASP.NET MVC 对文件夹名称使用一些基本命名约定：

| **文件夹** | **目的** |
| --- | --- |
| **/Controllers** | 控制器响应浏览器的输入，决定要如何处理它，并向用户返回响应。 |
| **/Views** | 视图保存我们的 UI 模板 |
| **/Models** | 模型保存和操作数据 |
| **/Content** | 此文件夹包含图像、CSS 和任何其他静态内容 |
| **/Scripts** | 此文件夹包含 JavaScript 文件 |

即使在空的 ASP.NET MVC 应用程序中也包含这些文件夹，因为 ASP.NET MVC 框架默认情况下使用 "约定 over 配置" 方法，并基于文件夹命名约定做出一些默认假设。 例如，默认情况下，控制器将在 Views 文件夹中查找视图，无需在代码中显式指定此项。 坚持默认约定会减少需要编写的代码量，还可以使其他开发人员更容易了解你的项目。 在构建应用程序时，我们将更详细地介绍这些约定。

> [!div class="step-by-step"]
> [下一部分](mvc-music-store-part-2.md)
