---
uid: identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
title: 将密码和其他敏感数据部署到 ASP.NET 和 Azure App Service-ASP.NET 4。x
author: Rick-Anderson
description: 本教程介绍你的代码如何安全地存储和访问安全信息。 最重要的一点是，切勿存储密码或其他 sen。
ms.author: riande
ms.date: 05/21/2015
ms.assetid: 97902c66-cb61-4d11-be52-73f962f2db0a
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure
msc.type: authoredcontent
ms.openlocfilehash: 8356a90611f791779cc4ff4730038d82cd76242f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457045"
---
# <a name="best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure-app-service"></a>向 ASP.NET 和 Azure 应用服务部署密码和其他敏感数据的最佳做法

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程介绍你的代码如何安全地存储和访问安全信息。 最重要的一点是，切勿在源代码中存储密码或其他敏感数据，并且不应在开发和测试模式下使用生产机密。
> 
> 示例代码是一个简单的 WebJob 控制台应用程序和一个需要访问数据库连接字符串 password、Twilio、Google 和 SendGrid 安全密钥的 ASP.NET MVC 应用程序。
> 
> 此外，还介绍了本地设置和 PHP。

- [在开发环境中使用密码](#pwd)
- [使用开发环境中的连接字符串](#con)
- [Web 作业控制台应用](#wj)
- [将机密部署到 Azure](#da)
- [本地和 PHP 说明](#not)
- [其他资源](#addRes)

<a id="pwd"></a>
## <a name="working-with-passwords-in-the-development-environment"></a>在开发环境中使用密码

教程经常在源代码中显示敏感数据，但愿您一定不要将敏感数据存储在源代码中。 例如，我[的 ASP.NET MVC 5 应用程序与 SMS 和 EMAIL 2FA](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md) *教程在 web.config 文件中*显示以下内容：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample1.xml)]

Web.config*文件是*源代码，因此这些机密永远不会存储在该文件中。 幸运的是，`<appSettings>` 元素具有一个 `file` 属性，可用于指定包含敏感应用程序配置设置的外部文件。 只要外部文件未签入源树，就可以将所有机密移动到外部文件。 例如，在以下标记中，文件*AppSettingsSecrets*包含所有应用机密：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample2.xml)]

外部文件（在本示例中为*AppSettingsSecrets* ）中的标记是在*web.config 文件中*找到的相同标记：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample3.xml)]

ASP.NET 运行时将外部文件的内容与 &lt;appSettings&gt; 元素中的标记合并。 如果找不到指定的文件，运行时会忽略文件属性。

> [!WARNING]
> 安全性-不要将您的*机密 .config*文件添加到项目或将其签入源代码管理。 默认情况下，Visual Studio 会将 `Build Action` 设置为 `Content`，这意味着该文件已部署。 有关详细信息，请参阅[为何我的项目文件夹中的所有文件都已部署？](https://msdn.microsoft.com/library/ee942158(v=vs.110).aspx#can_i_exclude_specific_files_or_folders_from_deployment) 虽然你可以将任何扩展用于该*密钥*文件，但最好是将其保留为 .config，因为 IIS 不提供配置文件 *。* 另请注意， *AppSettingsSecrets* *文件是 web.config 文件中*的两个目录级别，因此它完全超出了解决方案目录。 通过将文件移出解决方案目录，&quot;git add \*&quot; 不会将其添加到存储库中。

<a id="con"></a>
## <a name="working-with-connection-strings-in-the-development-environment"></a>使用开发环境中的连接字符串

Visual Studio 将创建使用[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)的新 ASP.NET 项目。 LocalDB 是专门为开发环境创建的。 它不需要密码，因此您无需执行任何操作即可阻止将机密签入您的源代码。 某些开发团队使用需要密码的 SQL Server （或其他 DBMS）的完整版本。

您可以使用 `configSource` 特性来替换整个 `<connectionStrings>` 标记。 与用于合并标记的 `<appSettings>` `file` 特性不同，`configSource` 特性替换标记。 下面的标记*显示了 web.config 文件中*的 `configSource` 特性：

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample4.xml?highlight=1)]

> [!NOTE]
> 如果使用上面所示的 `configSource` 属性将连接字符串移到外部文件，并让 Visual Studio 创建新网站，则它无法检测到你正在使用的数据库，并且在从 Visual Studio 发布到 Azure 时，你将不会获得配置数据库的选项。 如果你使用的是 `configSource` 属性，则可以使用 PowerShell 创建和部署你的网站和数据库，也可以在发布之前在门户中创建网站和数据库。 [New-AzureWebsitewithDB](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)脚本将创建一个新的网站和数据库。

> [!WARNING]
> 安全性-与*AppSettingsSecrets*文件不同，外部连接字符串文件必须与根*web.config*文件位于同一目录中，因此，您必须采取预防措施以确保不将其签入源存储库。

> [!NOTE]
> **机密文件的安全警告：** 最佳做法是不在测试和开发中使用生产机密。 使用测试或开发中的生产密码会泄漏这些机密。

<a id="wj"></a>
## <a name="webjobs-console-apps"></a>Web 作业控制台应用

控制台*应用使用的 app.config 文件不*支持相对路径，但它支持绝对路径。 可以使用绝对路径将机密移出项目目录。 以下标记显示了*C:\secrets\AppSettingsSecrets.config*文件中的机密以及*app.config*文件中的非敏感数据。

[!code-xml[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample5.xml?highlight=2)]

<a id="da"></a>
## <a name="deploying-secrets-to-azure"></a>将机密部署到 Azure

将 web 应用部署到 Azure 时，不会部署*AppSettingsSecrets*文件（这就是所需的文件）。 可以通过[Azure 管理门户](https://azure.microsoft.com/services/management-portal/)进行手动设置，以执行以下操作：

1. 中转到[https://portal.azure.com](https://portal.azure.com)，然后用 Azure 凭据登录。
2. 单击 "**浏览 &gt; Web 应用**"，然后单击你的 web 应用的名称。
3. 单击 "**所有设置" &gt; 应用程序设置**。

**应用设置**和**连接字符串**值覆盖*web.config 文件中的相同*设置。 在我们的示例中，我们未将这些设置部署到 Azure，但如果这些密钥在*web.config 文件中*，则门户上显示的设置优先。

最佳做法是遵循[DevOps 工作流](../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything.md)，并使用[Azure PowerShell](https://azure.microsoft.com/documentation/articles/install-configure-powershell/) （或其他框架，如[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)）自动在 Azure 中设置这些值。 下面的 PowerShell 脚本使用[export-clixml](http://www.powershellcookbook.com/recipe/PukO/securely-store-credentials-on-disk)将加密的机密导出到磁盘：

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample6.ps1)]

在上面的脚本中，"Name" 是机密密钥的名称，如 "&quot;FB\_AppSecret&quot; 或" TwitterSecret "。 你可以在浏览器中查看脚本所创建的 "credential" 文件。 下面的代码段测试每个凭据文件并为命名的 web 应用设置机密：

[!code-powershell[Main](best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure/samples/sample7.ps1)]

> [!WARNING]
> 安全性-在 PowerShell 脚本中不包括密码或其他机密，这样做将不会使用 PowerShell 脚本来部署敏感数据。 [获取凭据](https://technet.microsoft.com/library/hh849815.aspx)cmdlet 提供了一种安全机制，用于获取密码。 使用 UI 提示符会阻止泄漏密码。

### <a name="deploying-db-connection-strings"></a>部署 DB 连接字符串

DB 连接字符串的处理方式类似于应用程序设置。 如果从 Visual Studio 部署 web 应用，则会为你配置连接字符串。 可以在门户中对此进行验证。 设置连接字符串的建议方法是使用 PowerShell。 有关 PowerShell 脚本的示例，请创建网站和数据库，并设置网站中的连接字符串，从[Azure 脚本库](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)下载[New-AzureWebsitewithDB。](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3)

<a id="not"></a>
## <a name="notes-for-php"></a>PHP 说明

由于**应用设置**和**连接字符串**的键值对存储在 Azure App Service 上的环境变量中，因此使用任何 web 应用框架（如 PHP）的开发人员可以轻松地检索这些值。 请参阅 Stefan Schackow 的[Microsoft Azure 网站：应用程序字符串和连接字符串的工作原理](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)博客文章，其中显示了用于读取应用程序设置和连接字符串的 PHP 代码段。

## <a name="notes-for-on-premises-servers"></a>本地服务器的说明

如果要部署到本地 web 服务器，可以[加密配置文件的配置节](https://msdn.microsoft.com/library/ff647398.aspx)，以帮助保护机密。 作为替代方法，你可以使用为 Azure 网站推荐的相同方法：在配置文件中保留开发设置，并使用环境变量值进行生产设置。 但在这种情况下，你必须为 Azure 网站中的自动功能编写应用程序代码：检索环境变量中的设置，并使用这些值替换配置文件设置，或在以下情况下使用配置文件设置：找不到环境变量。

<a id="addRes"></a>
## <a name="additional-resources"></a>其他资源

有关创建 web 应用和数据库的 PowerShell 脚本的示例，请设置连接字符串 + 应用设置，从[Azure 脚本库](https://gallery.technet.microsoft.com/scriptcenter/site/search?f%5B0%5D.Type=RootCategory&amp;f%5B0%5D.Value=WindowsAzure)下载[New-AzureWebsitewithDB。](https://gallery.technet.microsoft.com/scriptcenter/Ultimate-Create-Web-SQL-DB-9e0fdfd3) 

请参阅 Stefan Schackow 的[Microsoft Azure 网站：应用程序字符串和连接字符串的工作原理](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/)

特别感谢 Barry Dorrans （ [@blowdart](https://twitter.com/blowdart) ）和 Carlos Farre 进行评审。
