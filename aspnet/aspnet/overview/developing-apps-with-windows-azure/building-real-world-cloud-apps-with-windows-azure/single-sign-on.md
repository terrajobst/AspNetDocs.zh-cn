---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
title: 单一登录（通过 Azure 构建实际的云应用） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 电子书构建真实的云应用基于 Scott Guthrie 开发的演示文稿。 它介绍了13种模式和实践，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 7d82d5e9-0619-4f22-9e03-32a6d52940a5
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/single-sign-on
msc.type: authoredcontent
ms.openlocfilehash: 1ca93cce22487295a24aae95437b3e69dfc5b504
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500522"
---
# <a name="single-sign-on-building-real-world-cloud-apps-with-azure"></a>单一登录（通过 Azure 构建实际的云应用）

作者： [Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom Dykstra](https://github.com/tdykstra)

[下载 Fix It 项目](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下载电子书](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 电子书构建真实的云应用**基于 Scott Guthrie 开发的演示文稿。 它介绍了可帮助你成功开发云的 web 应用的13种模式和实践。 有关电子书的信息，请参阅[第一章](introduction.md)。

开发云应用程序时需要考虑许多安全问题，但对于此系列，我们将重点介绍一种：单一登录。 用户经常问的问题是： "我主要为公司的员工构建应用;我如何将这些应用程序托管在云中，并使他们能够使用在本地环境中运行的应用程序时所用的相同安全模型？ 启用此方案的一种方式称为 Azure Active Directory （Azure AD）。 Azure AD 使你能够通过 Internet 提供企业业务线（LOB）应用，并使你能够将这些应用程序提供给业务合作伙伴。

## <a name="introduction-to-azure-ad"></a>Azure AD 简介

[Azure AD](https://docs.microsoft.com/azure/active-directory/)在云中提供[Active Directory](https://msdn.microsoft.com/library/windows/desktop/aa746492.aspx) 。 关键功能包括：

- 它与本地 Active Directory 集成。
- 它支持应用的单一登录。
- 它支持开放标准，如[SAML](http://en.wikipedia.org/wiki/SAML_2.0)、 [WS 送送](http://en.wikipedia.org/wiki/WS-Federation)和[OAuth 2.0](http://oauth.net/2/)。
- 它支持企业[关系图 REST API](https://msdn.microsoft.com/library/hh974476.aspx)。

假设你有一个本地 Windows Server Active Directory 环境，你可以使用它来使员工登录 Intranet 应用：

![](single-sign-on/_static/image1.png)

您可以使用哪些 Azure AD 在云中创建目录。 这是一项免费功能，易于设置。

它可以完全独立于本地 Active Directory;你可以将所需的任何人置于 Internet 应用中并对其进行身份验证。

![Windows Azure Active Directory](single-sign-on/_static/image2.png)

也可以将其与本地 AD 集成。

![AD 和 WAAD 集成](single-sign-on/_static/image3.png)

现在，可以在本地进行身份验证的所有员工还可以通过 Internet 进行身份验证–无需打开防火墙或在数据中心部署任何新服务器。 你可以继续利用你知道和使用的所有现有 Active Directory 环境，为你的内部应用程序使用单一登录功能。

在 AD 和 Azure AD 之间建立此连接后，你还可以让你的 web 应用和移动设备对云中的员工进行身份验证，并可以启用第三方应用（例如 Office 365、SalesForce.com 或 Google apps），以接受你的员工凭据。 如果你使用的是 Office 365，则已设置了 Azure AD，因为 Office 365 使用 Azure AD 进行身份验证和授权。

![第三方应用](single-sign-on/_static/image4.png)

这种方法的优点在于，无论你的组织是添加还是删除用户，或者用户更改密码，都可以使用你今天在本地环境中使用的相同过程。 所有本地 AD 更改都会自动传播到云环境。

如果你的公司使用或转到 Office 365，好消息是你将 Azure AD 自动设置，因为 Office 365 使用 Azure AD 进行身份验证。 因此，您可以在自己的应用程序中轻松地使用 Office 365 使用的相同身份验证。

## <a name="set-up-an-azure-ad-tenant"></a>设置 Azure AD 租户

Azure AD 目录称为 Azure AD[租户](https://technet.microsoft.com/library/jj573650.aspx)，设置租户非常简单。 我们将向你演示如何在 Azure 管理门户中完成此操作，以便阐释概念，但正如其他门户功能，你也可以通过使用脚本或管理 API 来执行此操作。

在管理门户中，单击 "Active Directory" 选项卡。

![门户中的 WAAD](single-sign-on/_static/image5.png)

你的 Azure 帐户会自动拥有一个 Azure AD 租户，你可以单击页面底部的 "**添加**" 按钮创建其他目录。 例如，你可能需要一个用于测试环境，一个用于生产环境。 仔细考虑新目录的名称。 如果使用目录的名称，然后对其中一个用户再次使用该名称，这可能会造成混淆。

![添加目录](single-sign-on/_static/image6.png)

门户完全支持创建、删除和管理此环境中的用户。 例如，若要添加用户，请单击 "**用户**" 选项卡，然后单击 "**添加用户**" 按钮。

![“添加用户”按钮](single-sign-on/_static/image7.png)

![添加用户对话框](single-sign-on/_static/image8.png)

你可以创建仅在此目录中存在的新用户，也可以将 Microsoft 帐户注册为此目录中的用户，或者在此目录中以用户的身份注册或其他 Azure AD 目录中的用户。 （在实际目录中，默认域为 ContosoTest.onmicrosoft.com。 你还可以使用自己选择的域，如 contoso.com。）

![用户类型](single-sign-on/_static/image9.png)

![添加用户对话框](single-sign-on/_static/image10.png)

您可以将用户分配到角色。

![用户配置文件](single-sign-on/_static/image11.png)

使用临时密码创建帐户。

![临时密码](single-sign-on/_static/image12.png)

你以这种方式创建的用户可以使用此云目录立即登录到你的 web 应用。

不过，企业单一登录的好处是 "**目录集成**" 选项卡：

![目录集成选项卡](single-sign-on/_static/image13.png)

如果启用 "目录集成" 和 "[下载工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)"，则可以将此云目录与已在组织内部使用的现有本地 Active Directory 同步。 然后，存储在目录中的所有用户将显示在此云目录中。 你的云应用现在可以使用其现有 Active Directory 凭据对你的所有员工进行身份验证。 所有这些都是免费的–同步工具和 Azure AD 本身。

此工具是一个易于使用的向导，如您在这些屏幕截图中看到的那样。 这些不是完整的说明，只是显示基本过程的示例。 有关操作方法的详细信息，请参阅本章末尾的[资源](#resources)部分中的链接。

![WAAD 同步工具配置向导](single-sign-on/_static/image14.png)

单击 "**下一步**"，然后输入 Azure Active Directory 凭据。

![WAAD 同步工具配置向导](single-sign-on/_static/image15.png)

单击 "**下一步**"，然后输入本地 AD 凭据。

![WAAD 同步工具配置向导](single-sign-on/_static/image16.png)

单击 "**下一步**"，然后指示是否要在云中存储 AD 密码的哈希。

![WAAD 同步工具配置向导](single-sign-on/_static/image17.png)

可以存储在云中的密码哈希是单向哈希;实际密码永远不会存储在 Azure AD 中。 如果决定不在云中存储哈希，则必须使用[Active Directory 联合身份验证服务](https://technet.microsoft.com/library/hh831502.aspx)（ADFS）。 [选择是否使用 ADFS 时，还需要考虑其他因素](https://technet.microsoft.com/library/jj573653.aspx)。 ADFS 选项需要几个附加的配置步骤。

如果选择在云中存储哈希，则完成后，当单击 "**下一步**" 时，该工具将开始同步目录。

![WAAD 同步工具配置向导](single-sign-on/_static/image18.png)

几分钟后你就会完成。

![WAAD 同步工具配置向导](single-sign-on/_static/image19.png)

只需在组织中的一个域控制器上运行，在 Windows 2003 或更高版本上运行。 且无需重新启动。 完成后，你的所有用户都位于云中，你可以使用 SAML、OAuth 或 WS-ADDRESSING 从任何 web 或移动应用程序进行单一登录。

有时，我们会询问您如何保护这一点– Microsoft 是否将其用于自己的敏感业务数据？ 答案是肯定的。 例如，如果你转到[https://microsoft.sharepoint.com/](https://microsoft.sharepoint.com/)的内部 Microsoft SharePoint 站点，则系统会提示你登录。

![Office 365 登录](single-sign-on/_static/image20.png)

Microsoft 已启用 ADFS，因此，当你输入 Microsoft ID 时，会重定向到 ADFS 登录页。

![ADFS 登录](single-sign-on/_static/image21.png)

输入存储在内部 Microsoft AD 帐户中的凭据后，即可访问此内部应用程序。

![MS SharePoint 站点](single-sign-on/_static/image22.png)

我们使用的是 AD 登录服务器，主要是因为在 Azure AD 可用之前已设置了 ADFS，但登录过程正在云中的 Azure AD 目录。 我们在云中提供重要文档、源代码管理、性能管理文件、销售报表等，并使用完全相同的解决方案来保护它们。

## <a name="create-an-aspnet-app-that-uses-azure-ad-for-single-sign-on"></a>创建使用 Azure AD 进行单一登录的 ASP.NET 应用

通过 Visual Studio，可以轻松地创建使用 Azure AD 进行单一登录的应用程序，就像从几个屏幕截图中看到的一样。

创建新的 ASP.NET 应用程序（MVC 或 Web 窗体）时，ASP.NET Identity 默认的身份验证方法。 若要将其更改为 Azure AD，请单击 "**更改身份验证**" 按钮。

![更改身份验证](single-sign-on/_static/image23.png)

选择 "组织帐户"，输入你的域名，然后选择 "单一登录"。

![配置身份验证对话框](single-sign-on/_static/image24.png)

还可以为应用程序提供目录数据的读取或读/写权限。 如果执行此操作，它可以使用[Azure Graph REST API](https://msdn.microsoft.com/library/windowsazure/hh974476.aspx)查找用户的电话号码，找出用户的电话号码、上次登录时间等。

这就是您需要做的一切-Visual Studio 要求提供 Azure AD 租户管理员的凭据，然后为新应用程序配置您的项目和 Azure AD 租户。

运行该项目时，你将看到一个登录页，你可以使用 Azure AD 目录中用户的凭据登录。

![组织帐户登录](single-sign-on/_static/image25.png)

![已登录](single-sign-on/_static/image26.png)

将应用部署到 Azure 时，你只需选择 "**启用组织身份验证**" 复选框，再一次，Visual Studio 会立即处理所有配置。

![发布网站](single-sign-on/_static/image27.png)

这些屏幕快照来自完整的分步教程，该教程演示如何生成使用 Azure AD 身份验证的应用程序：[使用 Azure Active Directory 开发 ASP.NET 应用](../../../../identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory.md)程序。

## <a name="summary"></a>摘要

在本章中，你已了解到 Azure Active Directory、Visual Studio 和 ASP.NET，使你可以轻松地在组织的用户的 Internet 应用程序中设置单一登录。 用户可以使用在内部网络中使用 Active Directory 登录所用的相同凭据登录到 Internet 应用。

[下一章](data-storage-options.md)介绍适用于云应用程序的数据存储选项。

<a id="resources"></a>
## <a name="resources"></a>资源

有关更多信息，请参见以下资源：

- [Azure Active Directory 文档](https://docs.microsoft.com/azure/active-directory/)。 Windowsazure.com 网站上 Azure AD 文档的门户页。 有关分步教程，请参阅**开发**部分。
- [Azure 多重身份验证](https://docs.microsoft.com/azure/multi-factor-authentication/)。 有关 Azure 中多重身份验证的文档的门户页。
- [组织帐户身份验证选项](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#orgauthoptions)。 Visual Studio 2013 "新建项目" 对话框中 Azure AD 身份验证选项的说明。
- [Microsoft 模式和实践-联合身份验证模式](https://msdn.microsoft.com/library/dn589790.aspx)。
- [如何：安装 Azure Active Directory 同步工具](https://social.technet.microsoft.com/wiki/contents/articles/19098.howto-install-the-windows-azure-active-directory-sync-tool-now-with-pictures.aspx)。
- [Active Directory 联合身份验证服务2.0 内容映射](https://social.technet.microsoft.com/wiki/contents/articles/2735.ad-fs-2-0-content-map.aspx)。 有关 ADFS 2.0 的文档的链接。
- [Windows Azure AD 应用程序中基于角色和基于 ACL 的授权](https://code.msdn.microsoft.com/Role-Based-and-ACL-Based-86ad71a1)。 示例应用程序。
- [Azure Active Directory 图形 API 博客](https://blogs.msdn.com/b/aadgraphteam/)。
- [混合标识基础结构中 BYOD 和目录集成中的访问控制](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/PCIT-B213#fbid=)。 Tech Ed 2014 讲座视频，通过 Gayana Bagdasaryan。

> [!div class="step-by-step"]
> [上一页](web-development-best-practices.md)
> [下一页](data-storage-options.md)
