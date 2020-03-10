---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET 拒绝了对 IIS 目录的访问 |Microsoft Docs
author: rick-anderson
description: 本白皮书介绍当 ASP.NET 应用程序的请求返回 "拒绝访问 DirectoryName 目录" 时必须执行的操作。 无法进行 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518570"
---
# <a name="aspnet-denied-access-to-iis-directories"></a>ASP.NET 拒绝了对 IIS 目录的访问

> 本白皮书介绍当 ASP.NET 应用程序的请求返回 "拒绝访问*DirectoryName*目录" 时必须执行的操作。 未能开始监视目录更改。 "
> 
> 适用于 ASP.NET 1.0 和 ASP.NET 1.1。

现在，使用在本地计算机上注册为 "ASPNET" 帐户的特权较低的 windows 帐户运行 ASP.NET V1 RTM。

在某些锁定的系统上，默认情况下，此帐户不能访问网站的内容目录、应用程序根目录或网站根目录。 在这种情况下，当从给定的 web 应用程序请求页面时，你将收到以下错误：

![](denied-access-to-iis-directories/_static/image1.jpg)

若要解决此问题，需要更改相应目录上的安全权限。

具体而言，ASP.NET 需要对网站根目录（例如： c:\inetpub\wwwroot 或你可能已在 IIS 中配置的任何备用网站目录）的 ASPNET 帐户的读取、执行和列表访问权限，内容目录和应用程序根目录以便监视配置文件更改。 应用程序根目录对应于 IIS 管理工具（inetmgr）中与应用程序虚拟目录关联的文件夹路径。

例如，请考虑 wwwroot 文件夹下的以下应用程序层次结构。

`C:\inetpub\wwwroot\myapp\default.aspx`

在此示例中，ASPNET 帐户需要在 myapp 和 wwwroot 目录中为内容定义以上的读取权限。 根文件夹中的单个继承 ACL 也可以选择性地用于这两个目录（如果它们是嵌套的）。

若要将权限添加到目录，请执行以下步骤：

- 使用 Windows 资源管理器导航到目录
- 右键单击目录文件夹，然后选择 "属性"
- 导航到属性对话框上的 "安全" 选项卡
- 单击 "添加" 按钮，然后输入计算机名称，后跟 ASPNET 帐户名称。 例如，在名为 "webdev.webserver.exe" 的计算机上，输入 webdev\ASPNET 并单击 "确定"。
- 确保 ASPNET 帐户选中 "读取 &amp; 执行"、"列出文件夹内容" 和 "读取" 复选框。
- 单击 "确定" 以关闭对话框并保存更改。

![](denied-access-to-iis-directories/_static/image2.jpg)

如果需要，可以使用随 Windows 一起提供的脚本或 "cacls .exe" 工具自动执行这些更改。 有关 ASPNET 帐户的详细信息，请参阅[FAQ 文档](https://go.microsoft.com/fwlink/?LinkId=5828)。

如果某个给定的 web 应用程序依赖于对特定文件夹或文件具有 "写入" 或 "修改" 权限，则可以按照相同的过程来授予此权限，并选中 "写入" 和/或 "修改" 复选框。

在 "允许每个人或用户组读取对这些目录的访问权限（这是默认配置）" 的计算机上，不会遇到任何问题，也不需要上述步骤。
