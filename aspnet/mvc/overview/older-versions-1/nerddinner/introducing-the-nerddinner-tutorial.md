---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: NerdDinner 教程简介 |Microsoft Docs
author: shanselman
description: 了解新框架的最佳方式是使用它来构建一些内容。 本教程介绍如何使用 ASP.NE 构建小型但完整的应用程序 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468932"
---
# <a name="introducing-the-nerddinner-tutorial"></a>NerdDinner 教程简介

作者： [Scott Hanselman](https://github.com/shanselman)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 了解新框架的最佳方式是使用它来构建一些内容。 本教程介绍如何使用 ASP.NET MVC 1 构建小型但完整的应用程序，并介绍了其背后的一些核心概念。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-tutorial"></a>NerdDinner 教程

了解新框架的最佳方式是使用它来构建一些内容。 本教程介绍如何使用 ASP.NET MVC 构建小型但完整的应用程序，并介绍了其背后的一些核心概念。

要生成的应用程序称为 "NerdDinner"。 NerdDinner 提供了一种简单的方法，使用户能够轻松查找和组织就：

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner 允许注册用户创建、编辑和删除就。 它在应用程序中强制实施一组一致的验证和业务规则：

![](introducing-the-nerddinner-tutorial/_static/image2.png)

访问者可以使用基于 AJAX 的地图来搜索即将发布的就：

![](introducing-the-nerddinner-tutorial/_static/image3.png)

单击晚餐会将其转到详细信息页面，用户可在其中了解更多相关信息：

![](introducing-the-nerddinner-tutorial/_static/image4.png)

如果他们感兴趣，他们可以在网站上登录或注册：

![](introducing-the-nerddinner-tutorial/_static/image5.png)

然后，他们可以单击基于 AJAX 的 RSVP 链接参加事件：

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>实现 NerdDinner

接下来，我们将使用 Visual Studio 中的 "文件&gt;" 新建项目 "命令来创建全新的 ASP.NET MVC 项目。 然后，我们将增量添加功能和功能。 在此过程中，我们将介绍：

1. [如何创建新的 ASP.NET MVC 项目](create-a-new-aspnet-mvc-project.md)
2. [如何创建数据库](create-a-database.md)
3. [如何使用业务规则验证生成模型](build-a-model-with-business-rule-validations.md)
4. [如何使用控制器和视图实现列表/详细信息 UI](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [如何提供 CRUD （创建、读取、更新、删除）数据表单条目支持](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [如何使用 ViewData 和实现 ViewModel 类](use-viewdata-and-implement-viewmodel-classes.md)
7. [如何使用母版页和分区重新使用 UI](re-use-ui-using-master-pages-and-partials.md)
8. [如何实现高效的数据分页](implement-efficient-data-paging.md)
9. [如何使用身份验证和授权保护应用程序](secure-applications-using-authentication-and-authorization.md)
10. [如何使用 AJAX 交付动态更新](use-ajax-to-deliver-dynamic-updates.md)
11. [如何使用 AJAX 实现映射方案](use-ajax-to-implement-mapping-scenarios.md)
12. [如何启用自动单元测试](enable-automated-unit-testing.md)

你可以通过完成本章节中演练的每个步骤，从头开始生成你自己的 NerdDinner 副本。 或者，你可以在[GitHub 上](https://github.com/AspNetMVPSamples/NerdDinner)的以下位置下载源代码的完整版本： NerdDinner。 如果你想要脱机阅读本教程，还可以选择[下载本教程的免费 PDF 版本](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)。

可以使用 Visual Studio 2008 或免费的 Visual Web Developer 2008 Express 来生成应用程序。 您可以使用数据库的 SQL Server 或免费 SQL Server Express。

你可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 安装 ASP.NET MVC、Visual Web Developer 2008 Express 和 SQL Server Express （免费）

### <a name="now-lets-get-started"></a>现在让我们开始吧 ... 。

现在我们已介绍了哪些 NerdDinner，让我们来汇总我们的卷起，并编写一些代码。

首先，我们将使用 Visual Studio 中的文件&gt;新项目来创建 NerdDinner 应用程序。

> [!div class="step-by-step"]
> [下一部分](create-a-new-aspnet-mvc-project.md)
