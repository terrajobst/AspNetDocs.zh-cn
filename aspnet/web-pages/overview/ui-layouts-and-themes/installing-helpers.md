---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: 在 ASP.NET 网页（Razor）站点中安装帮助程序 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何在 ASP.NET 网页（Razor）网站中安装帮助程序。 帮助器是一个可重用的组件，其中包括代码和每个的标记。
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518642"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a>在 ASP.NET 网页（Razor）站点中安装帮助器

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET 网页（Razor）网站中安装帮助程序。 *帮助器*是一种可重用的组件，其中包括用于执行可能比较繁琐或复杂的任务的代码和标记。
> 
> 学习内容：
> 
> - 如何在使用 WebMatrix 3 创建的网站中安装帮助程序。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - WebMatrix 3

## <a name="overview-of-helpers"></a>帮助器概述

用户经常想要在网页上执行的某些任务需要大量代码或需要额外的知识。 示例包括显示数据图表;将 Twitter "关注" 按钮置于页面上;从网站发送电子邮件;裁剪或调整图像大小;为站点使用 PayPal。 为了便于执行这些类型的操作，ASP.NET 网页允许使用*帮助*程序。 帮助器是为站点安装的组件，可让你使用一条或两条 Razor 代码执行典型任务。

ASP.NET 网页内置了几个帮助程序。 但是，许多帮助程序都在使用 NuGet 包管理器提供的包（外接程序）中提供。 NuGet 允许您选择要安装的包，然后处理安装的所有详细信息。

## <a name="installing-a-helper-in-webmatrix-3"></a>在 WebMatrix 3 中安装帮助器

1. 在 WebMatrix 3 中，单击 " **NuGet** " 按钮。

    ![WebMatrix 中的 "NuGet 库" 对话框](installing-helpers/_static/image1.png)
2. 这会启动 NuGet 包管理器，并显示可用的包。 在搜索框中，为要安装的帮助程序输入关键字。

    ![WebMatrix 中的 "NuGet 库" 对话框](installing-helpers/_static/image2.png)
3. 选择该包，然后单击 "**安装**"。 当系统询问你是否要安装包并指示你接受这些条款时，请单击 **"是"** 。

     如果这是您第一次安装帮助器，NuGet 将在您的网站中创建用于组成帮助器的代码的文件夹。
4. 若要卸载帮助程序，请单击 "**库**" 按钮，单击 "**已安装**" 选项卡，然后选择要卸载的包。

## <a name="installing-the-twitter-helper"></a>安装 Twitter 帮助程序

Twitter API 的最新版本与通过 NuGet 安装的 Twitter 帮助程序不兼容。 请参阅[Twitter helper With WebMatrix](twitter-helper.md)主题，了解有关如何在项目中设置 Twitter 帮助器的信息。

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

[介绍 ASP.NET 网页 2-编程基础知识](../getting-started/introducing-razor-syntax-c.md)

[Twitter Helper with WebMatrix](twitter-helper.md)
