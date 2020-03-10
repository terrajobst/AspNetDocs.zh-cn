---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013 中的 ASP.NET 基架 |Microsoft Docs
author: Rick-Anderson
description: ASP.NET 基架是 Visual Studio 2013 中包含的一项新功能。
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449564"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a>Visual Studio 2013 中的 ASP.NET 基架

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> ASP.NET 基架是 Visual Studio 2013 中包含的一项新功能。

## <a name="overview"></a>概述

ASP.NET 基架是用于 ASP.NET Web 应用程序的代码生成框架。 Visual Studio 2013 包含用于 MVC 和 Web API 项目的预安装代码生成器。 若要快速添加与数据模型交互的代码，请将基架添加到项目。 使用基架可以减少在项目中开发标准数据操作所需的时间。

默认情况下，Visual Studio 2013 不支持为 Web 窗体项目生成代码，但你可以通过将 MVC 依赖项添加到项目或安装扩展，将基架与 Web 窗体一起使用。 下面显示了这两种方法。

Visual Studio 2013 Update 2 （当前 RC）提供了扩展 ASP.NET 基架以满足方案要求的功能。 利用此功能，你可以创建一个自定义的基架模板并将其添加到 "添加新基架" 对话框。 在自定义模板中，指定添加基架项时生成的代码。 有关详细信息，请参阅[创建自定义 Scaffolder For Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029)。

## <a name="prerequisites"></a>系统必备

若要使用 ASP.NET 基架，必须具备：

- Microsoft Visual Studio 2013
- Web 开发人员工具（默认 Visual Studio 2013 安装的一部分）
- ASP.NET Web 框架和工具2013（默认 Visual Studio 2013 安装的一部分）

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a>将基架项添加到 MVC 或 Web API

若要添加基架，请右键单击项目或项目中的文件夹，然后选择 "**添加**-**新建基架项**"，如下图所示。

![添加基架项](aspnet-scaffolding-overview/_static/image1.png)

从 "**添加基架**" 窗口中，选择要添加的基架类型。

![选择基架的类型](aspnet-scaffolding-overview/_static/image2.png)

"**添加控制器**" 窗口可让你选择用于生成控制器的选项，包括是否要使用实体框架6中的新异步功能。

![添加控制器](aspnet-scaffolding-overview/_static/image3.png)

将为你的方案创建相关的类和页。 例如，下图显示了通过基架为名为电影的模型类创建的 MVC 控制器和视图。

![创建的文件](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a>将基架项添加到 Web 窗体

若要添加生成 Web 窗体代码的基架，你必须安装 Visual Studio 的扩展或添加 MVC 依赖项。 下面显示了这两种方法，但只需执行这些方法之一。

### <a name="web-forms-scaffolding-extension"></a>Web 窗体基架扩展

可以安装 Visual Studio 扩展，使你能够将基架用于 Web 窗体项目。 在 Visual Studio 中，依次选择 "**工具**" 和 "**扩展和更新**"。 从此对话框中，在 Visual Studio 库中搜索**Web 窗体基架**。

![安装 web 窗体基架](aspnet-scaffolding-overview/_static/image5.png)

有关详细信息，请参阅[Web 窗体基架](https://go.microsoft.com/fwlink/p/?LinkId=396478)。

### <a name="mvc-dependencies"></a>MVC 依赖项

若要添加 MVC 依赖项，请选择 "**添加** - **新基架项**"。 在 "添加基架" 窗口中，选择 " **MVC 依赖项**"，如下所示。

![添加 MVC 依赖项](aspnet-scaffolding-overview/_static/image6.png)

基架 MVC 有两个选项：最小和完整。 如果选择 "最小"，则只会将 NuGet 包和 ASP.NET MVC 的引用添加到你的项目中。 如果选择 "完全" 选项，则会添加最小依赖项，以及 MVC 项目所需的内容文件。 若要轻松使用基架，请选择 "完全依赖项"。

![选择完全依赖项](aspnet-scaffolding-overview/_static/image7.png)

添加依赖项后，你将看到 readme.txt**文件。** 仔细按照此文件中的说明进行操作，以确保您的项目正常工作。

完成 readme.txt 文件中的步骤后，可以添加新的基架项，如上一部分有关 MVC 和 Web API 的内容所示。 自动生成的视图和控制器将在你的项目中正确运行。

## <a name="tutorials"></a>教程

若要创建自定义的 scaffolder，请参阅[为 Visual Studio 创建自定义 scaffolder](https://go.microsoft.com/fwlink/p/?LinkId=395029)。

若要自定义生成的文件，请参阅[如何自定义 "新建基架项" 对话框中生成的文件](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx)。

有关将基架与**Database First 开发**结合使用的示例，请参阅[使用 ASP.NET MVC Database First EF](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md)。

有关在**MVC**项目中使用基架的示例，请参阅[与 ASP.NET MVC 5 入门](../../../mvc/overview/getting-started/introduction/getting-started.md)。

有关在**WEB api**项目中使用基架的示例，请参阅使用[web api 2 中的属性路由创建 REST API](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md)。
