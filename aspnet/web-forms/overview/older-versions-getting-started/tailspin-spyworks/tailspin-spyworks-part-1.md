---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 第1部分：文件-> 新项目 |Microsoft Docs
author: JoeStagner
description: 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第1部分介绍了概述和文件/新项目。
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516536"
---
# <a name="part-1-file--new-project"></a>第1部分：文件-> 新项目

作者： [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks 演示了创建适用于 .NET 平台的功能强大的可缩放应用程序是多么简单。 其中展示了如何使用 ASP.NET 4 中的优秀新功能构建在线商店，包括购物、结帐和管理。
> 
> 本教程系列详细介绍了生成 Tailspin Spyworks 示例应用程序所需执行的所有步骤。 第1部分介绍了概述和文件/新项目。

## <a id="_Toc260221666"></a>叙述

本教程介绍了 ASP.NET WebForms。 我们将启动缓慢，因此初级级别的 web 开发体验一切正常。

我们要构建的应用程序是一个简单的在线商店。

![](tailspin-spyworks-part-1/_static/image1.jpg)

访问者可以按类别浏览产品：

![](tailspin-spyworks-part-1/_static/image2.jpg)

他们可以查看单个产品并将其添加到购物车中：

![](tailspin-spyworks-part-1/_static/image3.jpg)

他们可以检查购物车，删除不再需要的任何项目：

![](tailspin-spyworks-part-1/_static/image4.jpg)

继续结帐会提示他们

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

排序后，他们会看到一个简单的确认屏幕：

![](tailspin-spyworks-part-1/_static/image7.jpg)

首先，我们将在 Visual Studio 2010 中创建新的 ASP.NET WebForms 项目，并以增量方式添加功能，以创建完整的正常运行的应用程序。 在此过程中，我们将介绍数据库访问、列表和网格视图、数据更新页面、数据验证、使用母版页以实现一致的页面布局、AJAX、验证、用户成员身份等。

可以按照步骤进行操作，也可以从[http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)下载已完成的应用程序。

可以从[https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/)使用 visual Studio 2010 或免费的 Visual Web Developer 2010。 若要生成应用程序，可以使用 SQL Server 或免费 SQL Server Express 来托管数据库。

## <a id="_Toc260221667"></a>文件/新建项目

首先从 Visual Studio 中的 "文件" 菜单中选择新项目。 此时将打开 "新建项目" 对话框。

![](tailspin-spyworks-part-1/_static/image8.jpg)

选择左侧的 "视觉C#对象"/"web 模板" 组，然后在 "中心" 列中选择 "ASP.NET Web 应用程序" 模板。 将项目命名为 TailspinSpyworks，然后按 "确定" 按钮。

![](tailspin-spyworks-part-1/_static/image9.jpg)

这将创建项目。 让我们看看应用程序中包含的文件夹，这些文件夹位于右侧的解决方案资源管理器中。

![](tailspin-spyworks-part-1/_static/image10.jpg)

空解决方案不完全为空-它添加了一个基本文件夹结构：

![](tailspin-spyworks-part-1/_static/image1.png)

请注意 ASP.NET 4 默认项目模板实现的约定。

- "帐户" 文件夹实现了 ASP 的基本用户界面。网络的成员资格子系统。
- "脚本" 文件夹将用作客户端 JavaScript 文件的存储库，并且默认情况下将提供 core jQuery .js 文件。
- "样式" 文件夹用于组织网站视觉对象（CSS 样式表）

如果按 F5 运行应用程序并呈现 default.aspx 页，将看到以下各项。

![](tailspin-spyworks-part-1/_static/image11.jpg)

第一次应用程序增强功能是将默认 WebForms 模板中的 Style .css 文件替换为 CSS 类和关联的图像文件，这些文件将呈现我们的 Tailspin Spyworks 应用程序所需的视觉对象 asthetics。

完成此操作后，我们的默认 .aspx 页面将呈现为此。

![](tailspin-spyworks-part-1/_static/image12.jpg)

请注意页面右上角的图像链接和已添加到母版页的菜单项。 只有 "登录" 和 "帐户" 链接指向存在的页面（由默认模板生成）以及我们将在构建应用程序时实现的其余页面。

我们还将母版页定位到样式目录。 尽管这只是一个首选项，但如果我们决定以后让应用程序 "skinable"，则可能会变得更容易。

完成此操作后，我们需要更改默认 ASP.NET WebForms 页面生成的所有 .aspx 文件中的母版页引用。

> [!div class="step-by-step"]
> [下一部分](tailspin-spyworks-part-2.md)
