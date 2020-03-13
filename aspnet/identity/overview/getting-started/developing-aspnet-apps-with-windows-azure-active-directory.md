---
uid: identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
title: 通过 Azure Active Directory-ASP.NET 4.x 开发 ASP.NET 应用
author: Rick-Anderson
description: Microsoft ASP.NET 的 Azure Active Directory 工具使你可以轻松地为在 Azure 上托管的 web 应用程序启用身份验证。 可以使用 Azure 身份 。
ms.author: riande
ms.date: 08/14/2014
ms.assetid: 457d7eaf-ee76-4ceb-9082-c7c1721435ad
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/developing-aspnet-apps-with-windows-azure-active-directory
msc.type: authoredcontent
ms.openlocfilehash: 28425ea8d1312dfc6e14df9677396f2cbcf6f16d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471740"
---
# <a name="developing-aspnet-apps-with-azure-active-directory"></a>借助 Azure Active Directory 开发 ASP.NET 应用

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

Azure Active Directory Microsoft ASP.NET 工具简化了在[Azure](https://www.windowsazure.com/home/features/web-sites/)上托管的 web 应用的身份验证。 你可以使用 Azure 身份验证对你的组织中的 Office 365 用户、从本地 Active Directory 同步的公司帐户或在你自己的自定义 Azure Active Directory 域中创建的用户进行身份验证。 启用 Windows Azure 身份验证可以将应用程序配置为使用单个[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/)租户对用户进行身份验证。

本教程将演示如何创建 ASP.NET 应用程序，该应用程序配置为使用[Azure Active Directory](https://msdn.microsoft.com/library/azure/mt168838.aspx) （Azure AD）进行登录。 你还将了解如何调用图形 API 以获取有关当前已登录用户的信息，以及如何将应用程序部署到 Azure。

## <a name="prerequisites"></a>系统必备

1. 用于 Web 或 [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) 的 [Visual Studio Express 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013#d-2013-express) 。
2. 需要[Visual Studio 2013 Update 4](https://www.microsoft.com/download/details.aspx?id=44921)更新3或更高版本。
3. 一个 Azure 帐户。 如果还没有帐户，[请单击此处](https://azure.microsoft.com/pricing/free-trial/)获取免费试用版。

## <a name="add-a-global-administrator-to-your-active-directory"></a>将全局管理员添加到 Active Directory

1. 登录到 [Azure 管理门户](https://manage.windowsazure.com/)。
2. 所有 Azure 帐户都包含一个**默认目录**，单击它，然后单击页面顶部的 "**用户**" 选项卡（请参阅下图）。
3. 单击“添加用户”。
    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image1.png)
4. 使用 "**全局管理员**" 角色创建新用户。 单击顶部菜单中的 "**用户**"，然后单击命令栏上的 "**添加用户**" 按钮。
5. 在 "**添加用户**" 对话框中，输入新用户的名称，然后单击右箭头。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image2.png)
6. 输入用户名并将 "角色" 设置为 "**全局管理员**"。 全局管理员需要使用备用电子邮件地址进行密码恢复。 完成后，单击右箭头。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image3.png)
7. 在对话框的下一页上，单击 "**创建**"。 将为新用户创建一个临时密码，并显示在对话框中。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image4.png)

   保存密码，你将需要在首次登录后更改密码。 下图显示了新的管理员帐户。 您必须使用 Azure Active Directory 登录到您的应用程序，而不是此页面上显示的 Microsoft 帐户。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image5.png)

## <a name="create-an-aspnet-application"></a>创建 ASP.NET 应用程序

以下步骤使用[Visual Studio Express 2013 For Web](https://www.microsoft.com/download/details.aspx?id=40747)，并需要[Visual Studio 2013 Update 3](https://www.microsoft.com/download/details.aspx?id=43721)。

1. 在 Visual Studio 中，依次单击 "**文件**" 和 "**新建项目**"。 在 "**新建项目**" 对话框中，从C#左侧菜单中选择 "可视 Web 项目"，然后单击 **"确定"** 。 如果不需要应用程序的功能，则可能还需要取消选中 "**将 Application Insights 添加到项目**"。
2. 在 "**新建 ASP.NET 项目**" 对话框中，选择 " **MVC**"，然后单击 "**更改身份验证**"。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image6.png)
3. 在 "**更改身份验证**" 对话框中，选择 "**组织帐户**"。 这些选项可用于自动向 Azure AD 注册应用程序，以及自动配置应用程序以与 Azure AD 集成。 你不必使用 "**更改身份验证**" 对话框来注册和配置你的应用程序，但这样做会更容易。 例如，如果使用的是 Visual Studio 2012，你仍可以在 Azure 管理门户中手动注册应用程序，并更新其配置以与 Azure AD 集成。
   在下拉菜单中，选择 "**云-单一组织**" 和 **"单一登录"，读取目录数据**。 输入 Azure AD 目录的域（例如，在下图中） *aricka0yahoo.onmicrosoft.com*，然后单击 **"确定"** 。 你可以从 azure 门户上的默认目录的 "域" 选项卡获取域名（请参阅下图）。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image7.png)

   下图显示了 Azure 门户中的域名。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image8.png)

    > [!NOTE]
    > 通过单击 "**更多选项**"，可以选择配置将在 Azure AD 中注册的应用程序 ID URI。 应用 ID URI 是应用程序的唯一标识符，该标识符在 Azure AD 中注册，并在与 Azure AD 通信时由应用程序用来标识自身。 有关已注册应用程序的应用 ID URI 和其他属性的详细信息，请参阅[此主题](https://msdn.microsoft.com/library/azure/dn499820.aspx#BKMK_Registering)。 单击 "应用 ID URI" 字段下面的复选框，你还可以选择覆盖 Azure AD 中使用相同应用 ID URI 的现有注册。
4. 单击 **"确定"** 后，将出现一个 "登录" 对话框，你将需要使用全局管理员帐户（而不是与你的订阅关联的 Microsoft 帐户）登录。 如果你之前创建了一个新的管理员帐户，则需要更改该密码，然后使用新密码再次登录。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image9.png)
5. 成功通过身份验证后，"**新建 ASP.NET 项目**" 对话框将显示身份验证选择（**组织**）以及将在其中注册新应用程序的目录（下图中的*aricka0yahoo.onmicrosoft.com* ）。 在此信息下方，选中标记为 **"在云中托管**" 的复选框。 如果选中此复选框，则会将项目设置为 Azure web 应用，并在以后轻松发布。 单击 **“确定”** 。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image10.png)
6. 将显示 "**配置 Azure 网站**" 对话框，其中使用自动生成的站点名称和区域。 另请注意对话框中当前登录的帐户。 需要确保此帐户是 Azure 订阅附加到的帐户，通常是 Microsoft 帐户。

    > [!NOTE]
    > 此项目需要数据库。 需要选择一个现有数据库，或创建一个新数据库。 数据库是必需的，因为该项目已使用本地数据库文件来存储少量的身份验证配置数据。 当你将应用程序部署到 Azure 网站时，此数据库不会与部署一起打包，因此你需要选择一个在云中可访问的数据库。 单击 **“确定”** 。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image11.png)
7. 将创建项目，并且会自动为该项目配置身份验证选项和 web 应用选项。 完成此过程后，按 **^ F5**在本地运行该项目。 你将需要使用你的组织帐户进行登录。 提供前面创建的帐户的用户名和密码，并单击 "**登录**"。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image12.png)
8. 成功登录后，ASP.NET 网站将显示已通过在页面右上角显示用户名进行身份验证。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image13.png)

   如果收到错误：值不能为 null 或为空。 参数名称： Externallink><maml linktext> ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image14.png)

   请参阅本教程末尾的 "[调试](#dbg)" 部分。

## <a name="basics-of-the-graph-api"></a>图形 API 基础知识

[图形 API](https://msdn.microsoft.com/library/azure/hh974476.aspx)是用于对 Azure AD 目录中的对象执行 CRUD 和其他操作的编程接口。 如果在 Visual Studio 2013 中创建新项目时，选择 "用于身份验证的组织帐户" 选项，则应用程序将配置为调用图形 API。 本部分简要介绍图形 API 的工作方式。

1. 在正在运行的应用程序中，单击页面右上角的已登录用户的名称。 这会将你转到 "用户配置文件" 页，该页面是对 Home 控制器的操作。 你会注意到，该表包含之前创建的管理员帐户的用户信息。 此信息存储在目录中，在加载页面时，将调用图形 API 来检索此信息。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image15.png)
2. 返回到 Visual Studio，展开 "**控制器**" 文件夹，然后打开**HomeController.cs**文件。 你将看到一个**UserProfile （）** 操作，其中包含用于检索令牌并调用图形 API 的代码。 此代码复制如下：

    [!code-csharp[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample1.cs?highlight=22)]

    若要调用图形 API，首先需要检索令牌。 检索令牌后，必须将其字符串值追加到图形 API 的所有后续请求的授权标头中。 上面的大多数代码都将处理对 Azure AD 的身份验证的详细信息，以获取令牌，并使用该令牌调用图形 API，然后转换响应以使其能够显示在视图中。

    讨论最相关的部分是以下突出显示的行： `UserProfile profile = JsonConvert.DeserializeObject<UserProfile>(responseString);`。 该行表示用户的名称，该名称已经从 JSON 响应反序列化，并显示在视图中。

    你可以使用 HttpClient 调用图形 API 并自行处理原始数据，但更简单的方法是使用[Graph 客户端库（可通过 NuGet 获得](http://www.nuget.org/packages/Microsoft.Azure.ActiveDirectory.GraphClient/)）。 客户端库处理原始 HTTP 请求和返回的数据的转换，并使在 .NET 环境中使用图形 API 变得更加容易。 请参阅 GitHub 上的相关图形 API 代码示例[。](https://github.com/AzureADSamples)

## <a name="deploy-the-application-to-azure"></a>将应用程序部署到 Azure

以下步骤将演示如何将应用程序部署到 Azure。 在前面的步骤中，已将新项目与 Azure 上的 web 应用连接，因此只需几个步骤即可发布。

1. 在 Visual Studio 中，右键单击该项目，然后选择 "**发布**"。 将显示 "**发布 Web** " 对话框，其中每个设置均已配置。 单击 "**下一步**" 按钮以切换到 "**设置**" 页。 系统可能会提示你进行身份验证;请确保使用 Azure 订阅帐户（通常是 Microsoft 帐户）进行身份验证，而不是之前创建的组织帐户进行身份验证。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image16.png)
2. 选中 "**启用组织身份验证**" 选项。 在 "**域**" 字段中，输入目录的域。 从 "**访问级别**" 下拉选择 "**单一登录"，然后选择 "读取目录数据"** 。 你会注意到，以前使用的数据库已在 "**数据库**" 部分中填充。 单击“发布”。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image17.png)
3. Visual Studio 将开始部署你的网站，然后将显示一个新的浏览器窗口。 系统可能会提示你再次向你的目录进行身份验证。 经过身份验证后，会重定向到 Azure 上新发布的网站。

    ![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image18.png)

<a id="dbg"></a>
## <a name="debugging-the-app"></a>调试应用程序

如果收到以下错误信息：值不能为 null 或为空。 参数名称： Externallink><maml linktext>

![](developing-aspnet-apps-with-windows-azure-active-directory/_static/image19.png)

将*Views\Shared\\_LoginPartial*的代码替换为以下代码：

[!code-cshtml[Main](developing-aspnet-apps-with-windows-azure-active-directory/samples/sample2.cshtml?highlight=1-8,15-16)]

运行应用后，如果登录用户显示 "Null 用户"，注销，然后重新登录到前面创建的 Active Directory 帐户。

要遵循的一个优秀教程是 Rick Rainey [深入探讨：使用 Azure AD](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/)的 Azure 网站和组织身份验证。

## <a name="more-information"></a>详细信息

- [深入了解：使用 Azure AD](http://rickrainey.com/2014/08/19/deep-dive-azure-websites-and-organizational-authentication-using-azure-ad/) 的 Azure 网站和组织身份验证
- [Azure AD 图形 API 概述](https://msdn.microsoft.com/library/azure/hh974476.aspx)
- [Azure AD 中的身份验证方案](https://msdn.microsoft.com/library/azure/dn499820.aspx)
- [GitHub 上的 Azure AD 代码示例](https://github.com/AzureADSamples)
