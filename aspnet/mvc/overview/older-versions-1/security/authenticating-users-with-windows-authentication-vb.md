---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
title: 通过 Windows 身份验证对用户进行身份验证（VB） |Microsoft Docs
author: microsoft
description: 了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。 了解如何在应用程序的 web co 中启用 Windows 身份验证 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 532fa051-7d5c-4d6d-87f6-339ce4b84c44
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-windows-authentication-vb
msc.type: authoredcontent
ms.openlocfilehash: aa64b1f9ef6461a81611ca066310dca2d545baa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506240"
---
# <a name="authenticating-users-with-windows-authentication-vb"></a>使用 Windows 身份验证对用户进行身份验证 (VB)

由[Microsoft](https://github.com/microsoft)

> 了解如何在 MVC 应用程序的上下文中使用 Windows 身份验证。 了解如何在应用程序的 web 配置文件中启用 Windows 身份验证，以及如何使用 IIS 配置身份验证。 最后，你将了解如何使用 [授权] 属性将对控制器操作的访问限制为特定的 Windows 用户或组。

本教程的目的是介绍如何利用 Internet Information Services 中内置的安全功能来保护 MVC 应用程序中的视图。 了解如何允许仅由特定 Windows 用户或特定 Windows 组成员的用户调用控制器操作。

在构建内部公司网站（intranet 站点）时，如果希望用户能够在访问网站时使用其标准的 Windows 用户名和密码，则使用 Windows 身份验证是非常有意义的。 如果要构建面向外的网站（Internet 网站），请考虑改用 Forms 身份验证。

#### <a name="enabling-windows-authentication"></a>启用 Windows 身份验证

创建新的 ASP.NET MVC 应用程序时，默认情况下不启用 Windows 身份验证。 Forms 身份验证是为 MVC 应用程序启用的默认身份验证类型。 必须通过修改 MVC 应用程序的 web 配置（web.config）文件来启用 Windows 身份验证。 找到 &lt;authentication&gt; 部分，并将其修改为使用 Windows 而不是 Forms 身份验证，如下所示：

[!code-xml[Main](authenticating-users-with-windows-authentication-vb/samples/sample1.xml)]

启用 Windows 身份验证后，web 服务器将负责对用户进行身份验证。 通常，在创建和部署 ASP.NET MVC 应用程序时，可以使用两种不同类型的 web 服务器。

首先，在开发 MVC 应用程序时，使用 Visual Studio 附带的 ASP.NET 开发 Web 服务器。 默认情况下，ASP.NET 开发 Web 服务器在当前 Windows 帐户的上下文中执行所有页面（你用于登录 Windows 的任何帐户）。

ASP.NET 开发 Web 服务器还支持 NTLM 身份验证。 可以通过在 "解决方案资源管理器" 窗口中右键单击项目名称，然后选择 "属性" 来启用 NTLM 身份验证。 接下来，选择 "Web" 选项卡并选中 "NTLM" 复选框（请参阅图1）。

**图1–为 ASP.NET 开发 Web 服务器启用 NTLM 身份验证**

![clip_image002](authenticating-users-with-windows-authentication-vb/_static/image1.jpg)

对于生产 web 应用程序，您可以使用 IIS 作为 web 服务器。 IIS 支持多种身份验证类型，包括：

- 基本身份验证-定义为 HTTP 1.0 协议的一部分。 在 Internet 上以明文（Base64 编码）发送用户名和密码。 -摘要式身份验证–通过 internet 发送密码的哈希，而不是密码本身。 -集成 Windows （NTLM）身份验证-使用 Windows 在 intranet 环境中使用的最佳身份验证类型。 -证书身份验证-使用客户端证书启用身份验证。 证书映射到 Windows 用户帐户。

> [!NOTE] 
> 
> 有关这些不同类型的身份验证的更详细概述，请参阅[https://msdn.microsoft.com/library/aa292114(VS.71).aspx](https://msdn.microsoft.com/library/aa292114(VS.71).aspx)。

您可以使用 Internet Information Services Manager 启用特定类型的身份验证。 请注意，所有类型的身份验证在每个操作系统中都不可用。 此外，如果您将 IIS 7.0 与 Windows Vista 一起使用，则在 Internet Information Services 管理器中显示之前，您将需要启用不同类型的 Windows 身份验证。 打开 "**控制面板"、"程序"、"程序和功能"、"打开或关闭 Windows 功能**"，然后展开 "Internet Information Services" 节点（参见图2）。

**图 2-启用 Windows IIS 功能**

![clip_image004](authenticating-users-with-windows-authentication-vb/_static/image2.jpg)

使用 Internet Information Services，可以启用或禁用不同类型的身份验证。 例如，图3说明了如何在使用 IIS 7.0 时禁用匿名身份验证和启用集成的 Windows （NTLM）身份验证。

**图 3-启用集成 Windows 身份验证**

![clip_image006](authenticating-users-with-windows-authentication-vb/_static/image3.jpg)

#### <a name="authorizing-windows-users-and-groups"></a>授权 Windows 用户和组

启用 Windows 身份验证后，可以使用 &lt;授权&gt; 属性控制对控制器或控制器操作的访问。 此属性可应用于整个 MVC 控制器或特定控制器操作。

例如，列表1中的 Home 控制器公开了三个名为 Index （）、CompanySecrets （）和 StephenSecrets （）的操作。 任何人都可以调用 Index （）操作。 但是，只有 Windows 本地管理器组的成员可以调用 CompanySecrets （）操作。 最后，只有名为 Stephen 的 Windows 域用户（在 Redmond 域中）才能调用 StephenSecrets （）操作。

**列表1– Controllers\HomeController.vb**

[!code-vb[Main](authenticating-users-with-windows-authentication-vb/samples/sample2.vb)]

> [!NOTE]
> 由于 Windows 用户帐户控制（UAC），与 Windows Vista 或 Windows Server 2008 一起使用时，本地管理员组的行为与其他组不同。 除非你修改计算机的 UAC 设置，否则 &lt;授权&gt; 属性将无法正确识别本地 Administrators 组的成员。

如果在不是正确权限的情况下尝试调用控制器操作，就会发生什么情况，具体取决于启用的身份验证类型。 默认情况下，使用 ASP.NET 开发服务器时，只需获取一个空白页。 该页提供了**401 未授权**的 HTTP 响应状态。

另一方面，如果你在使用 IIS 时禁用了匿名身份验证，并且启用了基本身份验证，则每次请求受保护的页时都将继续获取登录对话框提示（请参阅图4）。

**图4– "基本身份验证登录" 对话框**

![clip_image008](authenticating-users-with-windows-authentication-vb/_static/image4.jpg)

#### <a name="summary"></a>摘要

本教程介绍了如何在 ASP.NET MVC 应用程序的上下文中使用 Windows 身份验证。 已了解如何在应用程序的 web 配置文件中启用 Windows 身份验证，以及如何使用 IIS 配置身份验证。 最后，你已了解如何使用 &lt;授权&gt; 属性将对控制器操作的访问限制为特定的 Windows 用户或组。

> [!div class="step-by-step"]
> [上一页](authenticating-users-with-forms-authentication-vb.md)
> [下一页](preventing-javascript-injection-attacks-vb.md)
