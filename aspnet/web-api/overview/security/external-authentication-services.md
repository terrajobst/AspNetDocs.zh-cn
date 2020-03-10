---
uid: web-api/overview/security/external-authentication-services
title: 带有 ASP.NET Web API （C#）的外部身份验证服务 |Microsoft Docs
author: rmcmurray
description: 介绍如何使用中的外部身份验证服务 ASP.NET Web API。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447416"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a>带 ASP.NET Web API 的外部身份验证C#服务（）

Visual Studio 2017 和 ASP.NET 4.7.2 展开了[单页面应用程序](../../../single-page-application/index.md)（SPA）和[Web API](../../index.md)服务的安全选项，以与外部身份验证服务（包括多个 OAuth/OpenID 和社交媒体身份验证服务）集成： Microsoft 帐户、Twitter、Facebook 和 Google。  

### <a name="in-this-walkthrough"></a>本演练中

- [使用外部身份验证服务](#USING)
- [创建示例 Web 应用程序](#SAMPLE)
- [启用 Facebook 身份验证](#FACEBOOK)
- [启用 Google 身份验证](#GOOGLE)
- [启用 Microsoft 身份验证](#MICROSOFT)
- [启用 Twitter 身份验证](#TWITTER)
- [其他信息](#MOREINFO)

    - [合并外部身份验证服务](#COMBINE)
    - [将 IIS Express 配置为使用完全限定的域名](#FQDN)
    - [如何获取 Microsoft 身份验证的应用程序设置](#OBTAIN)
    - [可选：禁用本地注册](#DISABLE)

### <a name="prerequisites"></a>系统必备

若要执行本演练中的示例，需要具备以下各项：

- Visual Studio 2017
- 一个开发人员帐户，其中包含以下社交媒体身份验证服务之一的应用程序标识符和密钥：

  - Microsoft 帐户（[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)）
  - Twitter （[https://dev.twitter.com/](https://dev.twitter.com/)）
  - Facebook （[https://developers.facebook.com/](https://developers.facebook.com/)）
  - Google （[https://developers.google.com/](https://developers.google.com)）

<a id="USING"></a>
## <a name="using-external-authentication-services"></a>使用外部身份验证服务

目前可供 web 开发人员使用的外部身份验证服务丰富，有助于在创建新的 web 应用程序时缩短开发时间。 Web 用户通常有多个现有帐户用于常用 web 服务和社交媒体网站，因此，当 web 应用程序从外部 web 服务或社交媒体网站实施身份验证服务时，它将保存创建身份验证实现需要花费一些时间。 使用外部身份验证服务可以使最终用户不必为你的 web 应用程序创建另一个帐户，也不必记住其他用户名和密码。

过去，开发人员有两种选择：创建自己的身份验证实现，或了解如何将外部身份验证服务集成到其应用程序中。 在最基本的层面上，下图演示了一个简单的用户代理（web 浏览器）请求流，该请求流请求配置为使用外部身份验证服务的 web 应用程序中的信息：

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

在前面的关系图中，用户代理（或此示例中的 web 浏览器）向 web 应用程序发出请求，该请求将 web 浏览器重定向到外部身份验证服务。 用户代理将其凭据发送到外部身份验证服务，并且如果用户代理已成功通过身份验证，则外部身份验证服务会将用户代理重定向到原始 web 应用程序，该应用程序的用户代理将发送到 web 应用程序。 Web 应用程序将使用令牌来验证是否已成功通过外部身份验证服务对用户代理进行了身份验证，并且 web 应用程序可以使用令牌来收集有关用户代理的详细信息。 一旦应用程序处理完用户代理的信息，web 应用程序就会根据其授权设置向用户代理返回适当的响应。

在第二个示例中，用户代理与 web 应用程序和外部授权服务器协商，web 应用程序与外部授权服务器进行其他通信以检索有关用户的其他信息代理商

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

Visual Studio 2017 和 ASP.NET 4.7.2 通过为以下身份验证服务提供内置集成，使开发人员可以更轻松地与外部身份验证服务集成：

- Facebook
- Google
- Microsoft 帐户（Windows Live ID 帐户）
- Twitter

本演练中的示例将演示如何使用随 Visual Studio 2017 随附的新的 ASP.NET Web 应用程序模板配置每个受支持的外部身份验证服务。

> [!NOTE]
> 如果需要，你可能需要将 FQDN 添加到外部身份验证服务的设置。 此要求基于某些外部身份验证服务的安全约束，要求应用程序设置中的 FQDN 与客户端使用的 FQDN 相匹配。 （对于每个外部身份验证服务，此操作的步骤会很大; 您将需要查阅每个外部身份验证服务的文档，以确定是否需要这样做，以及如何配置这些设置。）如果需要将 IIS Express 配置为使用 FQDN 来测试此环境，请参阅本演练后面的[配置 IIS Express 以使用完全限定的域名](#FQDN)部分。

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a>创建示例 Web 应用程序

以下步骤将引导你完成使用 ASP.NET Web 应用程序模板创建示例应用程序的步骤，在本演练后面的部分中，你将为每个外部身份验证服务使用此示例应用程序。

启动 Visual Studio 2017，然后从起始页中选择 "**新建项目**"。 或者，从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

显示 "**新建项目**" 对话框时，选择 "**已安装**" 并展开 "**视觉对象C#** "。 在 **" C#视觉对象**" 下选择 " **Web**"。 在项目模板列表中，选择 " **ASP.NET Web 应用程序（.Net Framework）** "。 输入项目的名称，然后单击 **"确定"** 。

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

显示**新的 ASP.NET 项目**时，选择 "**单页面应用程序**" 模板，然后单击 "**创建项目**"。

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

等待 Visual Studio 2017 创建项目。

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

当 Visual Studio 2017 创建完你的项目后，打开位于**应用\_Start**文件夹中的*Startup.Auth.cs*文件。

首次创建项目时，不会在*Startup.Auth.cs*文件中启用任何外部身份验证服务;下面演示了你的代码可能会出现的情况，其中突出显示了在其中启用外部身份验证服务的部分以及任何相关设置，以便将 Microsoft 帐户、Twitter、Facebook 或 Google 身份验证用于 ASP.NET 应用程序：

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

当你按 F5 生成和调试 web 应用程序时，它将显示一个登录屏幕，你会在其中看到未定义任何外部身份验证服务。

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

在以下部分中，你将了解如何在 Visual Studio 2017 中启用与 ASP.NET 一起提供的每个外部身份验证服务。

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a>启用 Facebook 身份验证

使用 Facebook 身份验证要求你创建 Facebook 开发人员帐户，你的项目将需要 Facebook 中的应用程序 ID 和密钥，才能正常运行。 有关创建 Facebook 开发人员帐户和获取应用程序 ID 和机密密钥的信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)。

获取应用程序 ID 和密钥后，请使用以下步骤为 web 应用程序启用 Facebook 身份验证：

1. 在 Visual Studio 2017 中打开项目后，打开*Startup.Auth.cs*文件。

2. 找到代码的 "Facebook 身份验证" 部分：

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. 删除 &quot;//&quot; 字符取消注释突出显示的代码行，然后添加应用程序 ID 和密钥。 添加这些参数后，可以重新编译项目：

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. 按 F5 在 web 浏览器中打开 web 应用程序时，将看到 Facebook 已定义为外部身份验证服务：

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. 单击 " **facebook** " 按钮后，浏览器将重定向到 Facebook 登录页：

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. 输入 Facebook 凭据并单击 "**登录**" 后，web 浏览器将重定向回 web 应用程序，该应用程序将提示你输入要与 Facebook 帐户关联的**用户名**：

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. 输入用户名并单击 "**注册**" 按钮后，你的 web 应用程序将显示 Facebook 帐户的默认**主页**：

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a>启用 Google 身份验证

使用 Google authentication 需要你创建 Google 开发人员帐户，你的项目将需要 Google 中的应用程序 ID 和密钥，才能正常运行。 有关创建 Google 开发人员帐户和获取应用程序 ID 和机密密钥的信息，请参阅[https://developers.google.com](https://developers.google.com)。

若要为 web 应用程序启用 Google 身份验证，请使用以下步骤：

1. 在 Visual Studio 2017 中打开项目后，打开*Startup.Auth.cs*文件。

2. 找到代码的 "Google 身份验证" 部分：

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. 删除 &quot;//&quot; 字符取消注释突出显示的代码行，然后添加应用程序 ID 和密钥。 添加这些参数后，可以重新编译项目：

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. 按 F5 在 web 浏览器中打开 web 应用程序时，将看到 Google 已定义为外部身份验证服务：

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. 单击 " **google** " 按钮后，浏览器将重定向到 Google 登录页：

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. 输入 Google 凭据并单击 "**登录**" 后，Google 会提示你验证你的 web 应用程序是否有权访问 Google 帐户：

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. 单击 "**接受**" 时，web 浏览器将重定向回 web 应用程序，该应用程序将提示你输入要与 Google 帐户关联的**用户名**：

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. 输入用户名并单击 "**注册**" 按钮后，你的 web 应用程序将显示 Google 帐户的默认**主页**：

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a>启用 Microsoft 身份验证

Microsoft 身份验证要求您创建开发人员帐户，并需要客户端 ID 和客户端密码才能工作。 有关创建 Microsoft 开发人员帐户和获取客户端 ID 和客户端密钥的信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)。

获取使用者密钥和使用者机密后，请使用以下步骤为你的 web 应用程序启用 Microsoft 身份验证：

1. 在 Visual Studio 2017 中打开项目后，打开*Startup.Auth.cs*文件。

2. 找到代码的 "Microsoft 身份验证" 部分：

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. 删除 &quot;//&quot; 字符取消注释突出显示的代码行，然后添加你的客户端 ID 和客户端密码。 添加这些参数后，可以重新编译项目：

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. 按 F5 在 web 浏览器中打开 web 应用程序时，将看到 Microsoft 已定义为外部身份验证服务：

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. 单击 " **microsoft** " 按钮后，浏览器将重定向到 microsoft 登录页：

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. 输入 Microsoft 凭据并单击 "**登录**" 后，系统将提示你确认你的 web 应用程序有权访问 Microsoft 帐户：

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. 单击 **"是"** 后，web 浏览器将重定向回到 web 应用程序，该应用程序将提示你输入要与 Microsoft 帐户关联的**用户名**：

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. 输入用户名并单击 "**注册**" 按钮后，你的 web 应用程序将显示 Microsoft 帐户的默认**主页**：

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a>启用 Twitter 身份验证

Twitter 身份验证要求你创建开发人员帐户，并需要使用者密钥和使用者机密才能工作。 有关创建 Twitter 开发人员帐户和获取使用者密钥和使用者机密的信息，请参阅[https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)。

获取使用者密钥和使用者机密后，请使用以下步骤为你的 web 应用程序启用 Twitter 身份验证：

1. 在 Visual Studio 2017 中打开项目后，打开*Startup.Auth.cs*文件。

2. 找到代码的 "Twitter 身份验证" 部分：

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. 删除 &quot;//&quot; 字符取消注释突出显示的代码行，然后添加使用者密钥和使用者机密。 添加这些参数后，可以重新编译项目：

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. 按 F5 在 web 浏览器中打开 web 应用程序时，将看到 Twitter 已定义为外部身份验证服务：

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. 单击 " **twitter** " 按钮后，浏览器将重定向到 Twitter 登录页面：

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. 输入 Twitter 凭据并单击 "**授权应用**" 后，web 浏览器将重定向回 web 应用程序，该应用程序将提示你输入要与 Twitter 帐户关联的**用户名**：

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. 输入用户名并单击 "**注册**" 按钮后，你的 web 应用程序将显示 Twitter 帐户的默认**主页**：

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a>其他信息

有关创建使用 OAuth 和 OpenID 的应用程序的其他信息，请参阅以下 Url：

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a>合并外部身份验证服务

为了获得更大的灵活性，你可以同时定义多个外部身份验证服务-这允许你的 web 应用程序的用户使用任何已启用的外部身份验证服务中的帐户：

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a>将 IIS Express 配置为使用完全限定的域名

某些外部身份验证提供程序不支持使用 HTTP 地址（如 `http://localhost:port/`）来测试应用程序。 若要解决此问题，可以向主机文件添加一个静态完全限定的域名（FQDN）映射，并在 Visual Studio 2017 中将项目选项配置为使用 FQDN 进行测试/调试。 为此，请使用以下步骤：

- 添加静态 FQDN 映射主机文件：

  1. 在 Windows 中打开提升的命令提示符。
  2. 键入以下命令：

      <kbd>记事本%WinDir%\system32\drivers\etc\hosts</kbd>
  3. 在 HOSTS 文件中添加类似于以下内容的条目：

      <kbd>127.0.0.1 www.wingtiptoys.com</kbd>
  4. 保存并关闭主机文件。

- 将 Visual Studio 项目配置为使用 FQDN：

  1. 在 Visual Studio 2017 中打开项目时，单击 "**项目**" 菜单，然后选择项目的属性。 例如，可以选择 " **WebApplication1 属性**"。
  2. 选择 " **Web** " 选项卡。
  3. 输入你的 FQDN 作为<strong>项目 Url</strong>。 例如，如果是添加到 HOSTS 文件的 FQDN 映射，则需要输入<kbd><http://www.wingtiptoys.com></kbd> 。

- 将 IIS Express 配置为使用应用程序的 FQDN：

    1. 在 Windows 中打开提升的命令提示符。
    2. 键入以下命令以更改到 IIS Express 文件夹：

        <kbd>cd/d &quot;%ProgramFiles%\IIS Express&quot;</kbd>
    3. 键入以下命令，将 FQDN 添加到应用程序：

        <kbd>appcmd.exe 设置配置-节： system.web/sites/+&quot;[name = ' WebApplication1 ']。[protocol = ' http '，bindingInformation = ' *：80： wingtiptoys ']&quot;/commit： apphost</kbd>

  其中， **WebApplication1**是项目的名称， **bindingInformation**包含要用于测试的端口号和 FQDN。

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a>如何获取 Microsoft 身份验证的应用程序设置

将应用程序链接到 Windows Live for Microsoft 身份验证是一个简单的过程。 如果尚未将应用程序链接到 Windows Live，可以使用以下步骤：

1. 浏览到[https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070)并在出现提示时输入 Microsoft 帐户的名称和密码，并单击 "**登录**"：

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. 选择 "**添加应用**"，并在出现提示时输入应用程序的名称，然后单击 "**创建**"：

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. 在 "**名称**" 下选择你的应用，并显示其应用程序属性页。

4. 输入应用程序的重定向域。 复制**应用程序 ID** ，然后在 "**应用程序机密**" 下选择 "**生成密码**"。 复制显示的密码。 应用程序 ID 和密码是你的客户端 ID 和客户端密码。 选择 **"确定"** ，然后单击 "**保存**"。

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a>可选：禁用本地注册

当前 ASP.NET 本地注册功能不会阻止自动程序（bot）创建成员帐户;例如，使用[CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md)等机器人防护和验证技术。 因此，你应该在登录页上删除本地登录窗体和注册链接。 为此，请在你的项目中打开 *\_Login* ，然后注释掉本地登录面板和注册链接的行。 生成的页应类似于以下代码示例：

[!code-html[Main](external-authentication-services/samples/sample10.html)]

禁用本地登录面板和注册链接后，登录页将仅显示已启用的外部身份验证提供程序：

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)
