---
uid: whitepapers/ms03-32-issue
title: 在应用 IE 的安全更新后修复 "服务器应用程序不可用" 错误Microsoft Docs
author: rick-anderson
description: 本文介绍修复了 Internet Explorer 的 MS03-32 安全更新的问题的修补程序，这些修补程序会1.0 影响在 Wi 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 1365eebb-bdf7-4a05-8d18-7f200531be55
msc.legacyurl: /whitepapers/ms03-32-issue
msc.type: content
ms.openlocfilehash: e0b6776cbfe22e341ac7105f03daac5074b480fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463454"
---
# <a name="fix-for-server-application-unavailable-error-after-applying-security-update-for-ie"></a>应用 IE 安全更新后，“服务器应用程序不可用”错误修复

> 本文介绍修复了 MS03-32 Security Update for Internet Explorer 的问题的修补程序，这些更新会影响 Windows XP Professional 上运行的 ASP.NET 1.0 应用程序。
> 
> 适用于 ASP.NET 1.0 和 Windows XP Professional。

Microsoft 发现在 Windows XP 上运行的 Internet Explorer 安全修补程序和 ASP.NET 1.0 的 MS03-32 安全更新存在问题。 此修补程序可以手动安装，也可以从 Windows 更新站点获取最近的关键更新。

此问题的症状是在 Windows XP 计算机上安装修补程序后，对本地 IIS 5.1 web 服务器上运行的 ASP.NET 应用程序的所有请求都会导致错误消息 "服务器应用程序不可用"。 对远程 web 服务器的请求不受影响。

此问题只会影响在 Windows XP 上运行 ASP.NET 1.0 的安装。 它不会影响运行 Windows 2000 或 Windows Server 2003 的计算机。 它也不会影响运行 Windows XP 且安装了 ASP.NET 1.1 的计算机。

请注意，此问题**不是**ASP.NET 的安全错误。 它不**会**打开或允许对 ASP.NET 应用程序或服务器进行任何恶意攻击。 相反，它仅仅是由修补程序本身导致的功能 bug。

我们正在努力解决此问题。 同时，你可以执行以下批处理文件作为此问题的解决方法。 批处理文件执行以下操作：

1. 停止 IIS 和 ASP.NET 状态服务
2. 使用已知的临时密码删除并重新创建 ASPNET 帐户
3. 使用 Windows `runas` 命令来启动可执行文件，该文件创建一个 ASPNET 用户配置文件
4. 重新注册 ASP.NET。 这会为该帐户创建新的随机密码，并为其应用默认的 ASP.NET 访问控制设置
5. 重新启动 IIS 服务

批处理文件包含 "<strong>1pass\@word</strong>" 的硬编码临时密码，在运行批处理文件时，系统将提示您输入 runas 命令。 Runas 命令完成后，将使用强随机值重新创建 ASPNET 帐户密码。 请注意，如果硬编码的密码不符合环境中的密码复杂性要求，则批处理文件可能会失败。 如果是这种情况，则可以将其更改为适用于您的环境的其他值。

*> [!IMPORTANT]* 如果已为 ASPNET 帐户添加了自定义访问控制设置或数据库帐户权限，则需要在此批处理文件完成后重新创建它们。 这是因为，当重新创建帐户时，它将获取一个新的安全标识符（SID）。

*> [!IMPORTANT]* 如果使用除 ASPNET 帐户以外的自定义帐户运行 ASP.NET 工作进程，则不应运行此批处理文件。 相反，应以交互方式登录或使用具有该帐户的 runas 命令，该命令将为该帐户创建用户配置文件。

此批处理文件包含在下面的自解压缩存档中。 使用方式：

1. 必须以具有管理员权限的帐户身份运行
2. [下载并打开自解压缩可执行文件](ms03-32-issue/_static/fixup1.exe)
3. 将内容提取到 c：\
4. 选择 "运行 ..."从 "开始" 菜单，然后输入 `cmd.exe`
5. 在 "打开命令" 窗口中，键入 `c:\fixup.cmd`。
6. 出现提示时，输入 " <strong>1pass\@word</strong> " 作为密码。
7. 如果你以前具有 ASPNET 帐户的自定义访问控制设置或数据库帐户权限，则现在需要重新应用这些设置。

许多道歉导致此导致的不便。 我们会在提供其他信息时将其发布。

下表列出了受此问题影响的平台和版本。

| .NET Framework | 平台 | 产生 |
| --- | --- | --- |
| 版本1。0 | Windows 2000 Professional | No |
| 版本1。0 | Windows 2000 Server | No |
| 版本1。0 | Windows XP Professional | 是 |
| 版本1。0 | Windows Server 2003 | No |
| 版本1。0 | Windows XP Home with Cassini | No |
| 版本 1.1 | Windows 2000 Professional | No |
| 版本 1.1 | Windows 2000 Server | No |
| 版本 1.1 | Windows XP Professional | No |
| 版本 1.1 | Windows Server 2003 | No |
| 版本 1.1 | Windows XP Home with Cassini | No |

致以感谢，   
 ASP.NET 团队
