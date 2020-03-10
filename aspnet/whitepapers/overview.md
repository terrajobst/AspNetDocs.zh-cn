---
uid: whitepapers/overview
title: 白皮书 |Microsoft Docs
author: rick-anderson
description: 在此页上，你将找到白皮书，帮助你安装和配置 ASP.NET，并帮助你编写安全、快速且灵活的 ASP.NET 应用程序。
ms.author: riande
ms.date: 11/15/2011
ms.assetid: d5e79470-01f2-4d65-8077-11c3e10a6784
msc.legacyurl: /whitepapers
msc.type: content
ms.openlocfilehash: 1a3a9fe5d685d4b38efe666fc88ff57016482ada
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520586"
---
# <a name="whitepapers"></a>白皮书

> 在此页上，你将找到白皮书，帮助你安装和配置 ASP.NET，并帮助你编写安全、快速且灵活的 ASP.NET 应用程序。
> 
> - [ASP.NET 4](#aspnet4)
> - [ASP.NET 安全白皮书](#security)
> - [安装和设置白皮书](#setup)
> - [SQL Server 白皮书](#sql)
> - [一般白皮书](#general)

<a id="aspnet4"></a>
## <a name="aspnet-4"></a>ASP.NET 4

与 ASP.NET 4 和 Visual Studio 2010 相关的信息。

[ASP.NET MVC 4 发行说明](mvc4-beta-release-notes.md "mvc4-发行说明")

本文档介绍在 Visual Studio 2010 的 ASP.NET MVC 4 开发者预览版中引入的新功能和改进，以及安装说明和已知问题。

[ASP.NET MVC 3 发行说明](mvc3-release-notes.md "mvc3-发行说明")

本文档介绍了 ASP.NET MVC 3 中引入的新功能和改进，以及安装说明和已知问题。

[ASP.NET 4 和 Visual Studio 2010 Web 开发概述](aspnet4/index.md "aspnet4")

ASP.NET 的很多令人兴奋的更改都将出现在 .NET Framework 版本4中。 本文档概述了即将发布的版本中包含的许多新功能。

[ASP.NET 4 Beta 2 重大更改](aspnet4/breaking-changes.md "重大更改")

本文档介绍了对 .NET Framework 版本 4 Beta 2 版本（即 ASP.NET 4 Beta 2 版本）所做的更改，这些更改可能会影响使用早期版本（包括 ASP.NET 4 Beta 1 版本）创建的应用程序。

[ASP.NET MVC 2 的新增功能](what-is-new-in-aspnet-mvc.md "aspnet mvc 中的新增功能")

本文档介绍 ASP.NET MVC 2 中引入的新功能和改进。

[将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2 应用程序](aspnet-mvc2-upgrade-notes.md "mvc2-upgrade-notes")

ASP.NET MVC 2 可与同一服务器上的 ASP.NET MVC 1.0 并行安装。 这使应用程序开发人员可以灵活选择何时将 ASP.NET MVC 1.0 应用程序升级到 ASP.NET MVC 2。 本文档具备了如何手动升级，并使用 Visual 。

<a id="security"></a>
## <a name="aspnet-security-whitepapers"></a>ASP.NET 安全白皮书

安全性是 internet 应用程序的一个重要方面，这些白皮书介绍了如何设计和实现安全的 ASP.NET 应用程序。

[检测 ASP.NET 2.0 应用程序的安全性](https://msdn.microsoft.com/library/ms998325.aspx)

这说明了如何使用自定义运行状况监视事件来检测 ASP.NET 应用程序，以跟踪与安全相关的事件和操作。 ASP.NET 版本2.0 提供运行状况监视，其中包含许多标准 。

[针对 ASP.NET 2.0 执行安全部署评审](https://msdn.microsoft.com/library/ms998367.aspx)

这说明了如何为 ASP.NET 2.0 应用程序执行安全部署评审，以识别不正确的配置设置引入的潜在安全漏洞。 大多数审核过程都涉及到 。

[在 ASP.NET 2.0 中使用 ADAM 角色](https://msdn.microsoft.com/library/ms998331.aspx)

这说明了如何开发使用 Active Directory 应用程序模式（ADAM）来存储 ASP.NET 角色的 ASP.NET 网站。 其中介绍了如何配置 ADAM 和授权管理器（AzMan）策略存储，以及如何创建新的角色和 。

[将授权管理器（AzMan）与 ASP.NET 2.0 配合使用](https://msdn.microsoft.com/library/ms998336.aspx)

本指南演示了如何将授权管理器（AzMan）与 ASP.NET 角色管理器 API 结合使用，以管理角色、检查用户角色成员身份和授权角色对 AzMan 策略存储执行特定操作。 如何 。

[使用 ASP.NET 2.0 中的成员资格](https://msdn.microsoft.com/library/ms998347.aspx)

本指南演示如何使用 ASP.NET 版本2.0 应用程序中的成员资格功能。 其中介绍了如何使用两个不同的成员资格提供程序： ActiveDirectoryMembershipProvider 和 SqlMembershipProvider。 成员资格功能 。

[使用 ASP.NET 2.0 中的角色管理器](https://msdn.microsoft.com/library/ms998314.aspx)

本指南演示如何使用 ASP.NET 2.0 角色管理器。 角色管理器简化了管理角色以及在应用程序中执行基于角色的授权的任务。 其中介绍了如何配置各种角色提供程序以用于 。

[在 ASP.NET 2.0 中使用 Windows 身份验证](https://msdn.microsoft.com/library/ms998358.aspx)

本指南演示如何在 ASP.NET Web 应用程序中配置和使用 Windows 身份验证。 当用户属于 Windows 域时，windows 身份验证是首选方法。 此方法使你能够使用现有的标识存储 。

[针对托管代码执行安全代码评审（基线活动）](https://msdn.microsoft.com/library/ms998364.aspx)

这说明了如何执行安全代码评审。 此模块介绍活动中涉及的步骤，以及用于分析结果的方法。 使用此操作方法 "安全问题列表：托管代码（.NET Framework 2.0）" 。

[针对 ASP.NET 2.0 执行安全部署评审](https://msdn.microsoft.com/library/ms998367.aspx)

这说明了如何为 ASP.NET 2.0 应用程序执行安全部署评审，以识别不正确的配置设置引入的潜在安全漏洞。 大多数审核过程都涉及到 。

[实现适用于 Windows 2000 的 Kerberos 委派](https://msdn.microsoft.com/library/aa302400.aspx)

Kerberos 委派使你能够在应用程序的多个物理层之间流动经过身份验证的标识，以支持下游身份验证和授权。 这说明了执行此操作所需的配置步骤。

[在 ASP.NET 2.0 中使用模拟和委托](https://msdn.microsoft.com/library/ms998351.aspx)

这说明了如何以及何时应在 ASP.NET 2.0 应用程序中使用模拟。 默认情况下，模拟处于关闭状态，你可以使用 ASP.NET Web 应用程序的进程标识来访问资源。 但是，可以使用 。

[在设计时创建 Web 应用程序的威胁模型](https://msdn.microsoft.com/library/ms978527.aspx)

本如何介绍为 Web 应用程序创建威胁模型的方法。 威胁建模活动可帮助您对安全设计进行建模，这样您就可以在投入之前公开潜在的安全设计缺陷和漏洞 。

### <a name="forms-authentication"></a>Forms 身份验证

[保护 ASP.NET 2.0 中的 Forms 身份验证](https://msdn.microsoft.com/library/ms998310.aspx)

这说明了如何使用 ASP.NET 2.0 应用程序安全配置和使用 forms 身份验证。 要考虑的关键因素包括正确保护身份验证票证以及保护用户标识存储和对该存储区的访问。 ...

[在 ASP.NET 2.0 中将 Forms 身份验证与 Active Directory 配合使用](https://msdn.microsoft.com/library/ms998360.aspx)

本指南演示如何使用 ActiveDirectoryMembershipProvider 将 forms 身份验证与 Microsoft® Active Directory®目录服务一起使用。 如何向您说明如何配置提供程序，以及如何创建和验证用户身份 ...。

[在 ASP.NET 2.0 中将 Forms 身份验证与多个域中的 Active Directory 一起使用](https://msdn.microsoft.com/library/ms998345.aspx)

本指南演示如何使用 ActiveDirectoryMembershipProvider 将 forms 身份验证与 Microsoft® Active Directory®目录服务一起使用。 如何向您说明如何配置提供程序，以及如何创建和验证用户身份 ...。

[在 ASP.NET 2.0 中将 Forms 身份验证与 SQL Server 配合使用](https://msdn.microsoft.com/library/ms998317.aspx)

这说明了如何将 forms 身份验证与 SQL Server 成员资格提供程序结合使用。 使用 SQL Server 的 Forms 身份验证最适用于你的应用程序用户不是 Windows 域的一部分的情况，因此,。

[在 ASP.NET 1.1 中通过 Forms 身份验证创建 GenericPrincipal 对象](https://msdn.microsoft.com/library/aa302399.aspx)

这说明了如何在使用 Forms 身份验证时创建和处理 GenericPrincipal 和 FormsIdentity 对象。

[在 ASP.NET 1.1 中将 Forms 身份验证与 Active Directory 配合使用](https://msdn.microsoft.com/library/aa302397.aspx)

本操作指南文章介绍了如何针对 Active Directory 凭据存储实现 Forms 身份验证。

[在 ASP.NET 1.1 中将 Forms 身份验证与 SQL Server 配合使用](https://msdn.microsoft.com/library/aa302398.aspx)

本如何演示如何针对 SQL Server 凭据存储实现 Forms 身份验证。 还介绍了如何在数据库中存储密码摘要。

### <a name="user-input-data-validation"></a>用户输入数据验证

[请求验证 - 阻止脚本攻击](request-validation.md "请求-验证")

本文介绍了 ASP.NET 的请求验证功能，其中，默认情况下，阻止应用程序处理提交给服务器的未编码的 HTML 内容。 当应用程序已存在以下情况时，可以禁用此请求验证功能：

[阻止 ASP.NET 中的跨站点脚本](https://msdn.microsoft.com/library/ms998274.aspx)

这说明了如何通过使用正确的输入验证技术和对输出进行编码，来帮助保护 ASP.NET 应用程序免受跨站点脚本攻击。 还介绍了许多其他保护机制，你可以在中使用它们 。

[在 ASP.NET 中防止 SQL 注入](https://msdn.microsoft.com/library/ms998271.aspx)

这说明了如何通过多种方式来帮助保护 ASP.NET 应用程序免受 SQL 注入式攻击。 当应用程序使用输入来构造动态 SQL 语句或使用存储过程来连接到 。

[使用正则表达式来限制 ASP.NET 中的输入](https://msdn.microsoft.com/library/ms998267.aspx)

这说明了如何在 ASP.NET 应用程序中使用正则表达式来限制不受信任的输入。 正则表达式是验证名称、地址、电话号码和其他用户信息等文本字段的好方法。 你可以使用 。

### <a name="code-access-security"></a>代码访问安全性

[使用 ASP.NET 2.0 中的代码访问安全性](https://msdn.microsoft.com/library/ms998326.aspx)

这说明了如何为应用程序选择适当的信任级别，以及在必要时如何创建自定义 ASP.NET 代码访问安全策略文件来定义自定义信任级别。 你可以使用不同的代码访问安全性信任 。

[创建自定义加密权限](https://msdn.microsoft.com/library/aa302362.aspx)

这说明了如何创建自定义代码访问安全权限来控制对 Win32®数据保护 API （DPAPI）提供的非托管加密功能的编程访问。 将此自定义权限用于托管 DPAPI 包装 。

[使用代码访问安全策略来约束程序集](https://msdn.microsoft.com/library/aa302361.aspx)

管理员可以配置代码访问安全策略，以限制 .NET Framework 代码（程序集）的操作。 在此操作方法中，配置代码访问安全策略，以限制程序集执行文件 i/o 和限制 。

### <a name="communications-security"></a>通信安全

[在 Web 服务器上设置 SSL](https://msdn.microsoft.com/library/aa302411.aspx)

必须为 SSL 配置 Web 服务器，以便支持从客户端应用程序进行 https 连接。 本指南演示如何在 Web 服务器上配置 SSL。

[设置客户端证书](https://msdn.microsoft.com/library/aa302412.aspx)

IIS 支持客户端证书身份验证。 本如何向您演示如何将 Web 应用程序配置为需要客户端证书。 它还说明了如何在客户端计算机上安装证书，并在调用 Web 应用程序时使用证书。

[使用 IPSec 来筛选端口和进行身份验证](https://msdn.microsoft.com/library/aa302366.aspx)

Internet 协议安全（IPSec）是一种协议，而不是服务，它为基于 IP 的网络流量提供加密、完整性和身份验证服务。 由于 IPSec 提供服务器到服务器的保护，因此可以使用 IPSec 来应对内部威胁 。

[使用 IPSec 提供两个服务器之间的安全通信](https://msdn.microsoft.com/library/aa302413.aspx)

IPSec 是 Windows 2000 提供的一种技术，允许您在两个服务器之间创建加密通道。 IPSec 可用于筛选 IP 流量并对服务器进行身份验证。 这说明了如何配置 IPSec 以提供安全（加密） 。

[使用 SSL 来保护与 SQL Server 通信](https://msdn.microsoft.com/library/aa302414.aspx)

通常，应用程序必须能够保护与 SQL Server 数据库服务器之间传递的数据。 使用 SQL Server，可以使用 SSL 创建加密通道。 这说明了如何在数据库服务器上安装证书 。

[使用 ASP.NET 1.1 中的客户端证书调用 Web 服务](https://msdn.microsoft.com/library/aa302408.aspx)

本指南说明如何将客户端证书传递给 Web 服务，以便从 ASP.NET Web 应用程序或 Windows 窗体应用程序进行身份验证。 你可以在本地计算机存储或用户存储中安装客户端证书。 If 。

[使用 ASP.NET 1.1 的 SSL 调用 Web 服务](https://msdn.microsoft.com/library/aa302409.aspx)

安全套接字层（SSL）加密可用于保证传递给 Web 服务的消息的完整性和保密性。 这说明了如何将 SSL 用于 Web 服务。

### <a name="cryptography"></a>密码

[在 .NET 1.1 中创建 DPAPI 库](https://msdn.microsoft.com/library/aa302402.aspx)

这说明了如何创建一个托管类库，用于向要加密数据的应用程序（例如，数据库连接字符串和帐户凭据）公开 DPAPI 功能。

[在 .NET 1.1 中创建加密库](https://msdn.microsoft.com/library/aa302405.aspx)

本如何演示如何创建托管类库以提供应用程序的加密功能。 它允许应用程序选择加密算法。 支持的算法包括 DES、三重 DES、RC2 和 Rijndael。

[在 ASP.NET 1.1 的注册表中存储加密连接字符串](https://msdn.microsoft.com/library/aa302406.aspx)

应用程序可以选择在 Windows 注册表中存储加密数据，例如连接字符串和帐户凭据。 这说明了如何在注册表中存储和检索加密的字符串。

[使用来自 ASP.NET 1.1 的 DPAPI （计算机存储）](https://msdn.microsoft.com/library/aa302403.aspx)

本指南演示如何使用 ASP.NET Web 应用程序或 Web 服务中的 DPAPI 来加密敏感数据。

[将 ASP.NET 1.1 中的 DPAPI （用户存储）用于企业服务](https://msdn.microsoft.com/library/aa302404.aspx)

本指南演示如何使用 ASP.NET Web 应用程序或服务中的 DPAPI 来加密敏感数据。 这说明了如何在用户存储中使用 DPAPI，这需要使用进程外的企业服务组件。

<a id="setup"></a>
## <a name="installation-and-setup-whitepapers"></a>安装和设置白皮书

这些白皮书提供了在服务器上安装和配置 ASP.NET 的分步说明。

[创建 ASP.NET 2.0 应用程序的服务帐户](https://msdn.microsoft.com/library/ms998297.aspx)

本指南演示如何创建和配置自定义的最小特权服务帐户以运行 ASP.NET Web 应用程序。 默认情况下，Microsoft Windows Server 2003 和 IIS 6.0 上的 ASP.NET 应用程序使用内置网络服务运行 。

[在 ASP.NET 2.0 中托管多个应用程序时提高安全性](https://msdn.microsoft.com/library/aa480478.aspx)

这说明了如何将多个应用程序彼此隔离，以及如何在 Web 宿主环境中将这些应用程序与共享系统资源相互隔离。 宿主环境可能是由托管多个 ... 的 Internet 服务提供商（ISP）提供的 Web 服务器。

[在 ASP.NET 2.0 中使用中等信任](https://msdn.microsoft.com/library/ms998341.aspx)

本指南说明如何将 ASP.NET Web 应用程序配置为在中等信任环境下运行。 如果在同一台服务器上托管多个应用程序，则可以使用代码访问安全性和中等信任级别来提供应用程序隔离。 通过设置 。

[使用 Network Service 帐户访问 ASP.NET 2.0 中的资源](https://msdn.microsoft.com/library/ms998320.aspx)

这说明了如何使用 NT AUTHORITY\Network Service 计算机帐户来访问本地和网络资源。 默认情况下，在 Windows Server 2003 上，ASP.NET 应用程序使用此帐户的标识运行。 这是一个最小特权 。

[在 ASP.NET 2.0 中使用协议转换和约束委派](https://msdn.microsoft.com/library/ms998355.aspx)

这说明了如何配置和使用协议转换和约束委派，以允许 ASP.NET 应用程序在模拟原始调用方的同时访问网络资源。 Microsoft® Windows®2000操作系统 。

[ .NET Framework 1.0 和 .NET Framework 1.1 的 ASP.NET 并行执行](side-by-side-with-10.md "与1.0 并行")

本白皮书介绍如何在计算机上安装 .NET 1.0 和 .NET 1.1，以允许 ASP.NET Web 应用程序在任一版本的 framework 上运行。

[ASP.NET 拒绝了对 IIS 目录的访问](denied-access-to-iis-directories.md "拒绝访问 iis 目录")

本白皮书介绍当 ASP.NET 应用程序的请求返回 "拒绝访问*DirectoryName*目录" 时必须执行的操作。 未能开始监视目录更改。 "

[通过 IIS 6.0 运行 ASP.NET 1.1](aspnet-and-iis6.md "aspnet 和 iis6")

虽然 Windows Server 2003 同时包含 IIS 6.0 和 ASP.NET 1.1，但默认情况下这些组件处于禁用状态。 本白皮书介绍了如何启用 IIS 6.0 和 ASP.NET 1.1，并建议使用几个配置设置来获得最佳 。

[在应用 IE 的安全更新后修复 "服务器应用程序不可用" 错误](ms03-32-issue.md "ms03-32-问题")

本文介绍修复了 MS03-32 Security Update for Internet Explorer 的问题的修补程序，这些更新会影响 Windows XP Professional 上运行的 ASP.NET 1.0 应用程序。

[创建自定义帐户以运行 ASP.NET 1。1](https://msdn.microsoft.com/library/aa302396.aspx)

ASP.NET Web 应用程序通常使用内置的 ASPNET 帐户运行。 有时，你可能想要使用自定义帐户。 本操作指南文章介绍了如何创建最小特权的本地帐户来运行 ASP.NET Web 应用程序。 ...

### <a name="configuration"></a>Configuration

[在 ASP.NET 2.0 中配置计算机密钥](https://msdn.microsoft.com/library/ms998288.aspx)

此方法说明了 Web.config 文件中的 &lt;machineKey&gt; 元素，并演示了如何配置 &lt;machineKey&gt; 元素，以控制对视图状态、forms 身份验证票证和角色 cookie 进行篡改的校对和加密。 ViewState 已签名 。

[使用 DPAPI 加密 ASP.NET 2.0 中的配置节](https://msdn.microsoft.com/library/ms998280.aspx)

这说明了如何使用 Windows 数据保护应用程序编程接口（DPAPI）受保护的配置提供程序和 Aspnet\_regiis 工具来加密配置文件的各个部分。 你可以使用 Aspnet\_regiis 工具来 。

[使用 RSA 加密 ASP.NET 2.0 中的配置节](https://msdn.microsoft.com/library/ms998283.aspx)

这说明了如何使用 RSA 保护配置提供程序和 Aspnet\_regiis 工具来加密配置文件的各个部分。 你可以使用 Aspnet\_regiis 工具来加密敏感数据（如连接字符串）保存在 。

[在 ASP.NET 2.0 中使用模拟和委托](https://msdn.microsoft.com/library/ms998351.aspx)

这说明了如何以及何时应在 ASP.NET 2.0 应用程序中使用模拟。 默认情况下，模拟处于关闭状态，你可以使用 ASP.NET Web 应用程序的进程标识来访问资源。 但是，可以使用 。

<a id="sql"></a>
## <a name="sql-server-whitepapers"></a>SQL Server 白皮书

尽管 ASP.NET 适用于各种数据库，但以下白皮书专门介绍了如何将 ASP.NET 应用程序连接到 SQL Server。

[使用 ASP.NET 2.0 中的 SQL 身份验证连接到 SQL Server](https://msdn.microsoft.com/library/ms998300.aspx)

这说明了在数据库访问身份验证使用本机 SQL 身份验证时，如何将 ASP.NET 应用程序安全地连接到 Microsoft® SQL Server™。 建议使用 Windows 身份验证连接到 SQL Server，因为你 。

[使用 ASP.NET 2.0 中的 Windows 身份验证连接到 SQL Server](https://msdn.microsoft.com/library/ms998292.aspx)

本指南演示如何使用 ASP.NET 版本2.0 应用程序中的 Windows 服务帐户连接到 SQL Server 2000。 你应尽可能使用 Windows 身份验证而不是 SQL 身份验证，因为你可以避免在中存储凭据 。

[使用 SSL 来保护与 SQL Server 2000 的通信](https://msdn.microsoft.com/library/aa302414.aspx)

通常，应用程序必须能够保护与 SQL Server 数据库服务器之间传递的数据。 使用 SQL Server，可以使用 SSL 创建加密通道。 这说明了如何在数据库服务器上安装证书,。

<a id="general"></a>
## <a name="general-whitepapers"></a>一般白皮书

以下案例研究介绍了从传统宿主环境将 Microsoft 的 .NET 社区网站迁移到 Microsoft Azure 所使用的过程。

[将 Microsoft 的 ASP.NET 和 IIS.NET 社区网站迁移到 Microsoft Azure](https://go.microsoft.com/fwlink/?LinkId=400656)

这些白皮书涵盖了有关 ASP.NET 的各种主题。

[使用 ASP.NET 2.0 中的运行状况监视](https://msdn.microsoft.com/library/ms998306.aspx)

这说明了如何使用运行状况监视来检测应用程序的自定义事件。 若要创建自定义运行状况监视事件，请创建一个派生自 WebBaseEvent 的类，将 &lt;healthMonitoring&gt; 。

[实施修补程序管理](https://msdn.microsoft.com/library/aa302364.aspx)

这如何说明修补程序管理，包括如何使单个或多个服务器保持最新。 除可从 Microsoft 下载的工具外，不需要其他软件。 操作和安全策略应采用修补程序管理 。

[Silverlight 3 SDK 中 Silverlight 的 ASP.NET 服务器控件](https://go.microsoft.com/fwlink/?LinkId=153377)

Silverlight （"ASP.NET Silverlight controls"）的 ASP.NET 服务器控件已从 silverlight SDK for Silverlight 版本3中删除，这些控件是 ASP.NET MediaPlayer 和 Silverlight 控件。 本文档为处理这些 ASP.NET 的开发人员提供相关指南 。

[构建高性能 Web 应用程序](https://devexpress.com/act)

了解如何使用 ASP.NET Ajax 库中的新增功能构建高性能 Web 应用程序
