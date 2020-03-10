---
uid: mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
title: 通过 Forms 身份验证对用户C#进行身份验证（） |Microsoft Docs
author: microsoft
description: 了解如何使用 [授权] 特性来保护 MVC 应用程序中的特定页面。 了解如何使用网站管理 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 239fd3ca-5630-4b8d-bc4b-2f906b1d3504
msc.legacyurl: /mvc/overview/older-versions-1/security/authenticating-users-with-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: bed2eafa47fec25ac04cb07e0037f596494bb7d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435446"
---
# <a name="authenticating-users-with-forms-authentication-c"></a>使用 Forms 身份验证对用户进行身份验证 (C#)

由[Microsoft](https://github.com/microsoft)

> 了解如何使用 [授权] 特性来保护 MVC 应用程序中的特定页面。 了解如何使用网站管理工具来创建和管理用户和角色。 你还将了解如何配置存储用户帐户和角色信息的位置。

本教程的目的是说明如何使用窗体身份验证来保护 ASP.NET MVC 应用程序中的视图。 了解如何使用网站管理工具来创建用户和角色。 你还将了解如何防止未经授权的用户调用控制器操作。 最后，你将了解如何配置存储用户名和密码的位置。

#### <a name="using-the-web-site-administration-tool"></a>使用网站管理工具

在执行其他操作之前，应首先创建一些用户和角色。 创建新用户和角色的最简单方法是利用 Visual Studio 2008 网站管理工具。 你可以通过选择 "**项目"、"ASP.NET 配置**" 菜单选项来启动此工具。 或者，您可以通过单击 "解决方案资源管理器" 窗口顶部的 "hammer" 旁边的 "（有点可怕的）" 图标来启动网站管理工具（请参阅图1）。

**图 1-启动网站管理工具**

![clip_image002](authenticating-users-with-forms-authentication-cs/_static/image1.jpg)

在网站管理工具中，通过选择 "安全" 选项卡来创建新的用户和角色。单击 "**创建用户**" 链接，创建名为 Stephen 的新用户（参见图2）。 为 Stephen 用户提供所需的任何密码（例如， *secret*）。

**图2–创建新用户**

![clip_image004](authenticating-users-with-forms-authentication-cs/_static/image2.jpg)

首先要启用角色并定义一个或多个角色，从而创建新的角色。 通过单击 "**启用角色**" 链接启用角色。 接下来，通过单击 "**创建或管理角色**" 链接，创建名为 "*管理员*" 的角色（请参阅图3）。

**图 3-创建新角色**

![clip_image006](authenticating-users-with-forms-authentication-cs/_static/image3.jpg)

最后，创建一个名为 Sally 的新用户，并在创建 Sally 时单击 "创建用户" 链接并选择 "管理员"，将 Sally 关联到管理员角色（请参阅图4）。

**图 4-将用户添加到角色**

![clip_image008](authenticating-users-with-forms-authentication-cs/_static/image4.jpg)

完成所有工作后，应该有两个名为 "Stephen" 和 "Sally" 的新用户。 还应具有名为管理员的新角色。 Sally 是 "管理员" 角色的成员，而 "Stephen" 不是。

#### <a name="requiring-authorization"></a>需要授权

您可以通过将 [授权] 特性添加到操作，要求用户先进行身份验证，然后才能调用控制器操作。 可以将 [授权] 属性应用于单个控制器操作，也可以将此属性应用于整个控制器类。

例如，列表1中的控制器公开一个名为 CompanySecrets （）的操作。 由于此操作是使用 [授权] 特性修饰的，因此除非用户经过身份验证，否则无法调用此操作。

**列表1– Controllers\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample1.cs)]

如果通过在浏览器的地址栏中输入 URL/Home/CompanySecrets 来调用 CompanySecrets （）操作，并且不是经过身份验证的用户，则会自动重定向到登录视图（参见图5）。

**图5–登录视图**

![clip_image010](authenticating-users-with-forms-authentication-cs/_static/image5.jpg)

您可以使用登录视图输入您的用户名和密码。 如果你不是已注册的用户，你可以单击 "**注册**" 链接以导航到 "注册" 视图（参见图6）。 您可以使用注册视图创建新的用户帐户。

**图 6-注册视图**

![clip_image012](authenticating-users-with-forms-authentication-cs/_static/image6.jpg)

成功登录后，可以看到 "CompanySecrets" 视图（参见图7）。 默认情况下，你将继续登录到你关闭浏览器窗口。

**图7– CompanySecrets 视图**

![clip_image014](authenticating-users-with-forms-authentication-cs/_static/image7.jpg)

#### <a name="authorizing-by-user-name-or-user-role"></a>按用户名或用户角色授权

您可以使用 [授权] 属性将对控制器操作的访问限制为特定的一组用户或一组特定的用户角色。 例如，清单2中修改后的主控制器包含两个名为 StephenSecrets （）和 AdministratorSecrets （）的新操作。

**列表 2-Controllers\HomeController.cs**

[!code-csharp[Main](authenticating-users-with-forms-authentication-cs/samples/sample2.cs)]

只有具有 user name Stephen 的用户可以调用 StephenSecrets （）操作。 所有其他用户都将重定向到登录视图。 Users 属性接受以逗号分隔的用户帐户名称列表。

只有管理员角色中的用户可以调用 AdministratorSecrets （）操作。 例如，由于 Sally 是 Administrators 组的成员，因此她可以调用 AdministratorSecrets （）操作。 所有其他用户都将重定向到登录视图。 Role 属性接受以逗号分隔的角色名称列表。

#### <a name="configuring-authentication"></a>配置身份验证

此时，您可能想知道用户帐户和角色信息的存储位置。 默认情况下，此信息存储在一个名为 ASPNETDB.MDF 的 SQL Express 数据库中，该数据库位于 MVC 应用程序的应用\_Data 文件夹中。 此数据库由 ASP.NET 框架在你开始使用成员身份时自动生成。

若要在 "解决方案资源管理器" 窗口中查看 ASPNETDB.MDF 数据库，首先需要选择 "菜单" "项目" "项目" "显示所有文件"。

开发应用程序时，使用默认的 SQL Express 数据库是正确的。 不过，您很可能不希望对生产应用程序使用默认的 ASPNETDB.MDF 数据库。 在这种情况下，你可以通过完成以下两个步骤来更改存储用户帐户信息的位置：

1. 将应用程序服务数据库对象添加到生产数据库-更改应用程序的连接字符串以指向生产数据库

第一步是将所有必要的数据库对象（表和存储过程）添加到生产数据库中。 将这些对象添加到新数据库的最简单方法是使用 ASP.NET SQL Server 安装向导（见图8）。 若要启动此工具，可以从 Microsoft Visual Studio 2008 程序组打开 Visual Studio 2008 命令提示符，然后从命令提示符处执行以下命令：

aspnet\_regsql

**图8– ASP.NET SQL Server 安装向导**

![clip_image016](authenticating-users-with-forms-authentication-cs/_static/image8.jpg)

使用 ASP.NET SQL Server 安装向导，可以选择网络上的 SQL Server 数据库，并安装 ASP.NET 应用程序服务所需的所有数据库对象。 不需要在本地计算机上安装数据库服务器。

> [!NOTE] 
> 
> 如果不想使用 ASP.NET SQL Server 安装向导，则可以在以下文件夹中找到用于添加应用程序服务数据库对象的 SQL 脚本：
> 
> > C:\Windows\Microsoft.NET\Framework\v2.0.50727

创建所需的数据库对象后，需要修改 MVC 应用程序使用的数据库连接。 修改 web 配置（web.config）文件中的 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 连接字符串，使其指向生产数据库。 例如，列表3中的已修改连接指向名为 MyProductionDB 的数据库（原始 Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception 连接字符串已被注释掉）。

**列表 3-web.config**

[!code-xml[Main](authenticating-users-with-forms-authentication-cs/samples/sample3.xml)]

#### <a name="configuring-database-permissions"></a>配置数据库权限

如果使用集成安全性来连接到数据库，则需要将正确的 Windows 用户帐户作为登录名添加到数据库中。 正确的帐户取决于你使用的是 ASP.NET 开发服务器还是 Internet Information Services 作为你的 web 服务器。 正确的用户帐户也依赖于您的操作系统。

如果使用的是 ASP.NET 开发服务器（Visual Studio 使用的默认 web 服务器），则应用程序将在 Windows 用户帐户的上下文中执行。 在这种情况下，你需要添加 Windows 用户帐户作为数据库服务器登录名。

或者，如果使用 Internet Information Services，则需要添加 ASPNET 帐户或 NT 颁发机构/网络服务帐户作为数据库服务器登录名。 如果使用的是 Windows XP，请将 ASPNET 帐户作为登录名添加到数据库中。 如果你使用的是更新的操作系统（例如 Windows Vista 或 Windows Server 2008），则添加 NT 颁发机构/网络服务帐户作为数据库登录名。

您可以使用 Microsoft SQL Server Management Studio 将新用户帐户添加到数据库（请参阅图9）。

**图9–创建新的 Microsoft SQL Server 登录名**

![clip_image018](authenticating-users-with-forms-authentication-cs/_static/image9.jpg)

创建所需的登录名后，需要将登录名映射到具有正确数据库角色的数据库用户。 双击该登录名，然后选择 "用户映射" 选项卡。选择一个或多个应用程序服务数据库角色。 例如，要对用户进行身份验证，你需要启用 aspnet\_成员身份\_BasicAccess 数据库角色。 若要创建新用户，你需要启用 aspnet\_成员身份\_FullAccess 数据库角色（请参阅图10）。

**图 10-添加应用程序服务数据库角色**

![clip_image020](authenticating-users-with-forms-authentication-cs/_static/image10.jpg)

#### <a name="summary"></a>摘要

在本教程中，已了解如何在生成 ASP.NET MVC 应用程序时使用 Forms 身份验证。 首先，您学习了如何通过利用网站管理工具来创建新用户和角色。 接下来，您学习了如何使用 [授权] 属性来防止未经授权的用户调用控制器操作。 最后，你已了解如何将 MVC 应用程序配置为将用户和角色信息存储在生产数据库中。

> [!div class="step-by-step"]
> [下一部分](authenticating-users-with-windows-authentication-cs.md)
