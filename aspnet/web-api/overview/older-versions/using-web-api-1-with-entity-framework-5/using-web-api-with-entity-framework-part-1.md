---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 第1部分：概述和创建项目 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447932"
---
# <a name="part-1-overview-and-creating-the-project"></a>第1部分：概述和创建项目

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

实体框架是对象/关系映射框架。 它将代码中的域对象映射到关系数据库中的实体。 大多数情况下，你不必担心数据库层，因为实体框架会为你处理此层。 你的代码将操作这些对象，而更改将保存到数据库中。

## <a name="about-the-tutorial"></a>关于教程

在本教程中，你将创建一个简单的存储区应用程序。 应用程序有两个主要部分。 普通用户可以查看产品和创建订单：

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

管理员可以创建、删除或编辑产品：

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a>将要学到的技能

学习内容：

- 如何对 ASP.NET Web API 使用实体框架。
- 如何使用挖空创建动态客户端 UI。
- 如何使用 Web API 的 forms 身份验证对用户进行身份验证。

尽管本教程是独立的，但你可能希望先阅读以下教程：

- [第一个 ASP.NET Web API](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [创建支持 CRUD 操作的 Web API](../creating-a-web-api-that-supports-crud-operations.md)

[ASP.NET MVC](../../../../mvc/index.md)的一些知识也很有用。

## <a name="overview"></a>概述

从较高层次来看，此应用程序的体系结构如下：

- ASP.NET MVC 为客户端生成 HTML 页面。
- ASP.NET Web API 公开对数据（产品和订单）的 CRUD 操作。
- 实体框架将 Web C# API 使用的模型转换为数据库实体。

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

下图显示了如何在应用程序的各个层上表示域对象：数据库层、对象模型，最后是用于通过 HTTP 将数据传输到客户端的网络格式。

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a>创建 Visual Studio 项目

您可以使用 Visual Web Developer Express 或完整版 Visual Studio 创建教程项目。

从**起始**页中，单击 "**新建项目**"。

在 "**模板**" 窗格中，选择 "**已安装模板**"，然后展开**视觉对象C#** 节点。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET MVC 4 Web 应用程序**"。 将项目命名为 "ProductStore"，然后单击 **"确定**"。

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

在 "**新建 ASP.NET MVC 4 项目**" 对话框中，选择 " **Internet 应用程序**"，然后单击 **"确定"** 。

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

"Internet 应用程序" 模板创建一个支持窗体身份验证的 ASP.NET MVC 应用程序。 如果现在运行应用程序，该应用程序已经有一些功能：

- 新用户可以通过单击右上角的 "注册" 链接进行注册。
- 注册用户可以通过单击 "登录" 链接登录。

成员资格信息保留在自动创建的数据库中。 有关 ASP.NET MVC 中 forms 身份验证的详细信息，请参阅[演练：在 ASP.NET mvc 中使用 Forms 身份验证](https://msdn.microsoft.com/library/ff398049(VS.98).aspx)。

## <a name="update-the-css-file"></a>更新 CSS 文件

此步骤是表面的，但它会使页面呈现为之前的屏幕快照。

在解决方案资源管理器中，展开 "Content" 文件夹，然后打开名为 "web.config" 的文件。 添加以下 CSS 样式：

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [下一部分](using-web-api-with-entity-framework-part-2.md)
