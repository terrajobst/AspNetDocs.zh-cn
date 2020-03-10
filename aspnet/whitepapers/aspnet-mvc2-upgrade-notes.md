---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: 将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2 |Microsoft Docs
author: rick-anderson
description: 本文档介绍了如何使用向导将 ASP.NET MVC 1.0 应用程序手动升级为 ASP.NET MVC 2。 此文档还适用于 d 。
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517298"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a>将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2 应用程序

> 本文档介绍了如何使用向导将 ASP.NET MVC 1.0 应用程序手动升级为 ASP.NET MVC 2。 此文档还可供[下载](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf)

## <a name="introduction"></a>简介

ASP.NET MVC 2 可与同一服务器上的 ASP.NET MVC 1.0 并行安装。 这使应用程序开发人员可以灵活选择何时将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2。

Visual Studio 2010 包含一个向导，该向导将使用 Visual Studio 2008 生成的现有 ASP.NET MVC 1.0 项目升级到 ASP.NET MVC 2。 通过在 Visual Studio 2010 中打开 ASP.NET MVC 1.0 项目来启动升级向导。

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a>Visual Studio 2008 SP1 上的 ASP.NET MVC 1.0 升级向导

若要将 ASP.NET MVC 1.0 应用程序升级到 Visual Studio 2008 SP1 中的 ASP.NET MVC 2，请使用（不支持的） MvcAppConverter 应用程序。 可以从以下 URL 下载此应用程序：

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a>手动升级 ASP.NET MVC 1.0 项目

若要手动将现有 ASP.NET MVC 1.0 应用程序升级到版本2，请遵循以下步骤：

1. 备份现有项目。
2. 在文本编辑器中，打开项目文件（扩展名为 .csproj 或 .vbproj 的文件），并查找 ProjectTypeGuid 元素。 作为该元素的值，将 GUID {603c0e0b-db56-11dc-be95-000d561079b0} 替换为 {F85E285D-A4E0-4152-9332-AB1D724D3325}。 完成后，该元素的值应如下所示： 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. 在 Web 应用程序根文件夹中，编辑 web.config 文件。 搜索 System.web，Version = 1.0.0.0，并将所有实例替换为 System.web，Version = 2.0.0.0。
4. 对位于 Views 文件夹中的 Web.config 文件重复上一步。
5. 使用 Visual Studio 打开项目，并在**解决方案资源管理器**中展开 "**引用**" 节点。 删除对 System.web （指向版本1.0 程序集）的引用。 添加对 System.web （v 2.0.0.0）的引用。
6. 将以下 bindingRedirect 元素添加到配置部分下的应用程序根目录中的 web.config 文件：   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. 创建新的空 ASP.NET MVC 2 应用程序。 将新应用程序的 "脚本" 文件夹中的文件复制到现有应用程序的 "脚本" 文件夹中。
8. 在应用程序文件中用 CSS 样式定义更新现有的€™ s CSS 文件。
9. 编译并运行该应用程序。 如果出现任何错误，请参阅[ASP.NET MVC 2 的新增功能页中](https://go.microsoft.com/fwlink/?LinkID=185038)的 "重大更改" 部分。
