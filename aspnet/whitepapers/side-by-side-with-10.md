---
uid: whitepapers/side-by-side-with-10
title: ASP.NET 并行执行 .NET Framework 1.0 和 1.1 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍如何在计算机上安装 .NET 1.0 和 .NET 1.1，使 ASP.NET Web 应用程序能够在任一版本的 fram 上运行 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513830"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a>.NET Framework 1.0 和 .NET Framework 1.1 的 ASP.NET 并行执行

> 本白皮书介绍如何在计算机上安装 .NET 1.0 和 .NET 1.1，以允许 ASP.NET Web 应用程序在任一版本的 framework 上运行。
> 
> 适用于 ASP.NET 1.0 和 ASP.NET 1.1。

在 ASP.NET 中，当应用程序安装在同一台计算机上时，它们被称为并行运行，但使用不同版本的 .NET Framework。 以下主题介绍如何为并行执行配置 ASP.NET 应用程序，并提供有关的详细步骤：

- [维护你的 Web 应用程序在安装过程中 .NET Framework 版本1.0 的映射](#1)
- [将 Web 应用程序映射到 .NET Framework 的特定版本](#2)
- [查找网站正在使用的 .NET Framework 的版本](#3)

传统上，在计算机上更新组件或应用程序时，将删除较旧的版本，并将其替换为较新的版本。 如果新版本与以前的版本不兼容，则通常会断开使用组件或应用程序的其他应用程序。 .NET Framework 支持并行执行，这允许同时在同一台计算机上安装程序集或应用程序的多个版本。 由于可以同时安装多个版本，因此托管应用程序可以选择使用哪个版本，而不影响使用不同版本的应用程序。

默认情况下，在安装 .NET Framework 版本1.1 的过程中，所有现有的 ASP.NET 应用程序都将自动重新配置为使用 .NET Framework 的最新版本。 如果你不希望 ASP.NET 应用程序默认 .NET Framework 1.1，请单击[此处](#1)了解如何在安装过程中阻止此操作。

如果将 Web 服务器更新为 .NET Framework 1.1，并且希望一个或多个 Web 应用程序运行 .NET Framework 1.0，则需要更新 Internet Information Services （IIS）脚本映射。 脚本映射是将特定 Web 应用程序的 .aspx 文件扩展名映射到 .NET Framework 版本的机制。 单击[此处](#2)了解如何将 Web 应用程序映射到 .NET Framework 的特定版本。

你可以使用 Internet 信息管理器或 ASP.NET IIS 注册工具（Aspnet\_regiis）来找出哪个 .NET Framework 版本正在运行特定的 Web 应用程序。 单击[此处](#3)了解如何查找网站正在使用的 .NET Framework 版本。

迁移到 .NET Framework 1.1 时，需要考虑的一个事项是 .NET Framework 的每个版本都使用其自己的 Machine.config 文件。 因此，如果 Web 管理员已对 machine.config 文件进行了更改，则这些更改必须迁移到 .NET Framework 1.1 Machine.config 文件中。

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a>在安装过程中维护 Web 应用程序到 .NET Framework 1.0 的映射

默认情况下，在安装过程中将自动重新配置所有现有的 ASP.NET 应用程序，以使用较新版本的 .NET Framework。 使用较新版本的 .NET Framework，应用程序可以充分利用新版本中包含的改进和新增功能。 同时，Web 管理员（可能需要对更新的应用程序进行精细控制）可以防止安装 .NET Framework 期间自动重映射所有现有的 ASP.NET 应用程序。

若要防止整个 ASP.NET 应用程序自动重新映射到较新版本的 .NET Framework，Web 管理员可以在 Dotnetfx.exe 安装程序中使用/noaspupgrade 命令行选项。

**阻止将 ASP.NET 应用程序的总重新映射到较新版本**

1. 转到“开始”。
2. 单击 "**运行**"。
3. 键入“cmd”。
4. 单击“确定”。  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. 在命令提示符下，键入以下行开始安装 .NET Framework： **dotnetfx.exe/c： "install/noaspupgrade？"** 。  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. 在 Microsoft .NET Framework 1.1 安装程序中单击 **"是"** 。 这将启动 .NET Framework 1.1 的设置过程。  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a>将 Web 应用程序映射到 .NET Framework 的特定版本

.NET Framework 的每个版本都包含一个 ASP.NET IIS 注册工具（Aspnet\_regiis）的版本。 管理员可以使用此工具指定在 .NET Framework 的特定版本下运行 Web 应用程序。 这称为将 Web 应用程序映射到 .NET Framework 版本。 管理员必须选择与要与 Web 应用程序关联的 .NET Framework 版本对应的 Aspnet\_regiis。 例如，要指定网站使用 .NET Framework 1.1 的管理员必须使用 .NET Framework 1.1 随附的 Aspnet\_regiis。

1\.0 版的 Aspnet\_regiis 位于：

- C:\WINDOWS\Microsoft.NET\Framework\\**v v1.0.3705**\aspnet\_regiis

版本1的 Aspnet\_regiis，1位于：

- C:\WINDOWS\Microsoft.NET\Framework\\**v 1.1.4322**\aspnet\_regiis

Aspnet\_regiis 为映射 Web 应用程序的脚本提供两个选项：

- **-s**设置路径及其子目录中的脚本映射。
- **-sn**仅在路径中设置脚本映射。

路径定义 Web 应用程序 IIS 元数据路径，该路径是以 W3SVC/ROOT/{WebSiteNumber}/{Application\_Name} 的形式定义的。 例如，对于 "默认网站" 下名为 "门户" 的 Web 应用程序，元数据库路径为 W3SVC/1/ROOT/门户。

![](side-by-side-with-10/_static/image4.gif)

请注意，还可以使用称为 "元数据库编辑器" 的工具来获取元数据库路径。 你可以从[https://support.microsoft.com/default.aspx?scid=kb; 232068;](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)的 Microsoft 支持部门网站下载此工具。

- 运行 Aspnet\_regiis-s W3SVC/1/ROOT/门户来更新门户 IIS script map 及其 subapplication。  
  
    ![](side-by-side-with-10/_static/image5.gif)

- 运行 Aspnet\_regiis-sn W3SVC/1/ROOT/门户来更新门户 IIS 脚本映射，而不影响门户子目录中的应用程序。  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a>查找 Web 应用程序正在使用的 .NET Framework 版本

管理员可以使用 Internet Service Manager 来查找 .NET Framework 运行网站的版本。 不同的操作系统版本以不同的方式启动 Internet Service Manager。 若要启动服务管理器，请执行下列步骤。

**启动 Internet Service Manager**

1. 转到“开始”。
2. 单击 "**运行**"。
3. 键入**inetmgr**。  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. 从 Internet Service Manager 中，选择想要了解其版本 .NET Framework 的 Web 应用程序。  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. 右键单击 Web 应用程序，然后单击 "属性" **。**  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. 在 "属性" 窗口中，选择 "**配置"。**  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. 从 "应用程序映射" 表中，选择 **.aspx**，然后单击 "**编辑**"。  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. 从 "**可执行文件**" 文本框中，通过滚动查看版本目录。 如果版本目录为1.1.4322，则将应用程序映射到 .NET Framework 1.1。 相反，如果版本目录是 v v1.0.3705，则会将应用程序映射到 .NET Framework 1.0。  
  
    ![](side-by-side-with-10/_static/image12.gif)
