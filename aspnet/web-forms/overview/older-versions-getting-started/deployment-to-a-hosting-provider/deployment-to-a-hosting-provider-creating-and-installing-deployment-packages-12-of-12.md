---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：疑难解答（12/12） |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: db8f58e3679e6dea865dadb6f64916032dd9f38c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78424034"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序：疑难解答（12/12）

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关显示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Microsoft Azure 网站，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

本页介绍使用 Visual Studio 部署 ASP.NET web 应用程序时可能出现的一些常见问题。 对于每个问题，都提供了一个或多个可能的原因和相应的解决方案。

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>"/" 应用程序中的服务器错误-当前自定义错误设置阻止远程查看错误的详细信息

### <a name="scenario"></a>方案

将站点部署到远程主机之后，会收到一条错误消息，其中提及了 Web.config 文件中的 customErrors 设置，但未指示错误的实际原因：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

默认情况下，仅当你的 web 应用程序在本地计算机上运行时，ASP.NET 才会显示详细的错误信息。 通常，当您的 web 应用程序在 Internet 上公开可用时，您不想显示详细的错误信息，因为黑客可能能够利用此信息来查找应用程序中的漏洞。 但是，在部署站点或更新站点时，有时会出现问题，需要获取实际的错误消息。

若要使应用程序能够在远程主机上运行时显示详细的错误消息，请编辑 Web.config 文件以将 `customErrors` 模式设置为 off，重新部署应用程序，然后再次运行应用程序：

1. 如果应用程序的 web.config 文件在 `system.web` 元素中具有 `customErrors` 元素，请将 `mode` 特性更改为 "off"。 否则，在 `mode` 特性设置为 "off" 的 `system.web` 元素中添加 `customErrors` 元素，如下面的示例中所示：

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. 部署应用程序。
3. 运行该应用程序，并重复您之前执行的任何导致错误的操作。 现在，你可以看到实际的错误消息是什么。
4. 解决错误后，还原原始 `customErrors` 设置并重新部署应用程序。

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>使用 SQL Server Compact 的网页中的访问被拒绝

### <a name="scenario"></a>方案

当你部署使用 SQL Server Compact 的站点，并且在已部署的站点中运行访问该数据库的页面时，你将看到以下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

服务器上的网络服务帐户需要能够读取*bin\amd64*或*bin\x86*文件夹中的 SQL 服务压缩本机二进制文件，但它不具有对这些文件夹的读取权限。 设置*bin*文件夹的 "网络服务的读取权限"，并确保将权限扩展到子文件夹。

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>由于权限不足而无法读取配置文件

### <a name="scenario"></a>方案

单击 Visual Studio 的 "发布" 按钮将应用程序部署到本地计算机上的 IIS 后，发布将失败，并且 "**输出**" 窗口将显示如下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

若要在本地计算机上使用一键式 "发布到 IIS"，必须使用管理员权限运行 Visual Studio。 关闭 Visual Studio 并以管理员权限重新启动它。

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>无法连接到目标计算机 .。。使用指定的进程

### <a name="scenario"></a>方案

单击 Visual Studio 的 "发布" 按钮以部署应用程序时，发布将失败，并且 "**输出**" 窗口将显示如下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

代理服务器中断了与目标服务器的通信。 在 Windows "控制面板" 或 Internet Explorer 中，选择 " **Internet 选项**"，然后选择 "**连接**" 选项卡。在 " **Internet 属性**" 对话框中，单击 " **LAN 设置**"。 在 "局域网 **（LAN）设置**" 对话框中，清除 "**自动检测设置**" 复选框。 然后再次单击 "发布" 按钮。

如果问题仍然存在，请与系统管理员联系，以确定可对代理或防火墙设置执行的操作。 发生此问题的原因是 Web 部署为 Web 管理服务部署使用非标准端口（8172）;对于其他连接，Web 部署使用端口80。 部署到第三方托管提供程序时，通常使用 Web 管理服务。

## <a name="default-net-40-application-pool-does-not-exist"></a>默认的 .NET 4.0 应用程序池不存在

### <a name="scenario"></a>方案

部署需要 .NET Framework 4 的应用程序时，将看到以下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

IIS 中未安装 ASP.NET 4。 如果你要部署到的服务器是你的开发计算机并在其上安装了 Visual Studio 2010，则将在计算机上安装 ASP.NET 4，但可能不会在 IIS 中安装。 在要部署到的服务器上，打开提升的命令提示符，并运行以下命令在 IIS 中安装 ASP.NET 4：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

你可能还需要手动设置默认应用程序池的 .NET Framework 版本。 有关详细信息，请参阅 "[以测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) " 教程。

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>初始化字符串的格式不符合从索引0处开始的规范。

### <a name="scenario"></a>方案

使用一键式发布部署应用程序后，在运行访问数据库的页时，会收到以下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

在部署*的站点*中打开 web.config 文件，然后检查连接字符串值是否以 `$(ReplaceableToken_`开头，如以下示例中所示：

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

如果连接字符串与此示例类似，则编辑项目文件，并将以下属性添加到适用于所有生成配置的 `PropertyGroup` 元素：

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

然后重新部署应用程序。

## <a name="http-500-internal-server-error"></a>HTTP 500 内部服务器错误

### <a name="scenario"></a>方案

当你运行部署的站点时，你将看到以下错误消息，其中没有指示错误原因的特定信息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

出现500错误的原因有很多，但如果您遵循这些教程，其中一种可能的原因是您将 XML 元素放在一个 XML 转换文件的错误位置。 例如，如果将插入 `<location>` 元素的转换置于 `<system.web>` 下而不是直接在 `<configuration>`下，则会出现此错误。 这种情况下的解决方案是更正 XML 转换文件并重新部署。

## <a name="http-50021-internal-server-error"></a>HTTP 500.21 内部服务器错误

### <a name="scenario"></a>方案

当你运行部署的站点时，你将看到以下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

部署的站点的目标为 ASP.NET 4，但未在服务器上的 IIS 中注册 ASP.NET 4。 在服务器上打开提升的命令提示符，并通过运行以下命令来注册 ASP.NET 4：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

你可能还需要手动设置默认应用程序池的 .NET Framework 版本。 有关详细信息，请参阅 "[以测试环境部署到 IIS](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) " 教程。

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a>登录无法在应用\_数据中打开 SQL Server Express 数据库

### <a name="scenario"></a>方案

在应用中*将 web.config 文件连接*字符串更新为指向 SQL Server Express 数据库的 *.Mdf*文件 *\_Data*文件夹，并且首次运行应用程序时，将看到以下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

即使删除了以前存在的数据库的 *.mdf*文件， *.mdf*文件的名称也不能与计算机上存在的任何 SQL Server Express 数据库的名称相匹配。 将 *.mdf*文件的名称更改为从未用作数据库名称的名称，并更改*web.config*文件以使用新名称。 作为替代方法，可以使用[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除以前存在的 SQL Server Express 数据库。

## <a name="model-compatibility-cannot-be-checked"></a>无法检查模型的兼容性

### <a name="scenario"></a>方案

已*将 web.config 文件连接*字符串更新为指向新的 SQL Server Express 数据库，并且首次运行应用程序时，将看到以下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

如果在您的计算机上曾经使用过您放置在 web.config 文件中的数据库名称，则可能已经存在包含某些表的数据库。 选择之前未在计算机上使用的新名称，*然后将 web.config 文件更改*为指向 "使用此新数据库名称"。 作为替代方法，可以使用[SQL Server Express 实用工具](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)或[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除现有数据库。

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>脚本尝试创建用户或角色时出现 SQL 错误

### <a name="scenario"></a>方案

你使用的是在 "**包/发布 SQL** " 选项卡上配置的数据库部署，在部署过程中运行的 SQL 脚本包含 "创建用户" 或 "创建角色" 命令，在执行这些命令时脚本执行将失败。 您可能会看到更详细的消息，如下所示：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

如果在 "**发布 Web** " 向导而不是 "**包/发布 SQL** " 选项卡中配置数据库部署后发生此错误，请在[配置和部署](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)论坛中创建一个线程，该解决方案将添加到此故障排除页。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

用于执行部署的用户帐户没有创建用户或角色的权限。 例如，托管公司可以将 `db_datareader`、`db_datawriter`和 `db_ddladmin` 角色分配给它为你设置的用户帐户。 它们足以用于创建大多数数据库对象，但不能用于创建用户或角色。 避免此错误的一种方法是从数据库部署中排除用户和角色。 为此，可以编辑数据库的自动生成脚本的 `PreSource` 元素，使其包含以下属性：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

有关如何编辑项目文件中的 `PreSource` 元素的信息，请参阅[如何：在项目文件中编辑部署设置](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)。 如果你的开发数据库中的用户或角色需要位于目标数据库中，请与你的托管提供商联系以获得帮助。

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>在部署过程中运行自定义脚本时出现 SQL Server 超时错误

### <a name="scenario"></a>方案

您已经指定了要在部署过程中运行的自定义 SQL 脚本，当 Web 部署运行它们时，它们将超时。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

运行具有不同事务模式的多个脚本会导致超时错误。 默认情况下，自动生成的脚本在事务中运行，但自定义脚本不会运行。 如果在 "**包/发布 SQL** " 选项卡上选择了 "**从现有数据库提取数据和/或架构**" 选项，并且添加自定义 SQL 脚本，则必须更改某些脚本的事务设置，以便所有脚本都使用相同的事务设置。 有关详细信息，请参阅[如何：使用 Web 应用程序项目部署数据库](https://msdn.microsoft.com/library/dd465343.aspx)。

如果已配置事务设置，使所有这些设置都相同但仍然出现此错误，则一种可能的解决方法是单独运行脚本。 在 "**包/发布**SQL" 选项卡的 "**数据库脚本**" 网格中，清除导致超时错误的脚本的 "**包含**" 复选框，然后发布项目。 然后返回到 "**数据库脚本**" 网格，选中该脚本的 "**包含**" 复选框，并清除其他脚本的 "**包含**" 复选框。 然后重新发布项目。 这一次，当你发布时，只会运行选定的自定义脚本。

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>站点清单的流数据尚不可用

### <a name="scenario"></a>方案

使用带有 `t` （test）选项的 *.deploy .cmd*文件安装包时，将看到以下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

错误消息表示该命令无法生成测试报告。 但是，如果使用 `y` （实际安装）选项，则该命令可能运行。 此消息仅指示在测试模式下运行命令时出现问题。

## <a name="this-application-requires-managedruntimeversion-v40"></a>此应用程序需要 ManagedRuntimeVersion v4。0

### <a name="scenario"></a>方案

当你尝试部署时，你会看到以下错误消息：

 错误： "sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript" 的流数据尚不可用。 尝试使用的应用程序池的 "managedRuntimeVersion" 属性设置为 "v2.0"。 此应用程序需要 "4.0"。 

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

IIS 中未安装 ASP.NET 4。 如果你要部署到的服务器是你的开发计算机并在其上安装了 Visual Studio 2010，则将在计算机上安装 ASP.NET 4，但可能不会在 IIS 中安装。 在要部署到的服务器上，打开提升的命令提示符，并运行以下命令在 IIS 中安装 ASP.NET 4：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>无法强制转换 DeploymentProviderOptions

### <a name="scenario"></a>方案

部署包时，将看到以下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

尝试使用 Web 部署 1.1 UI 从 IIS 管理器部署到安装了 Web 部署2.0 的服务器。 如果使用 IIS 远程管理工具通过导入包进行部署，请在建立连接时选中 "**可用的新功能**" 对话框。 （仅当首次建立连接时，才会显示此对话框。 若要清除连接并重新启动，请关闭 IIS 管理器，然后通过在命令提示符下输入 `inetmgr /reset` 来重新启动。）如果列出的其中一项功能**WEB 部署 UI**，并且版本号低于8，则部署到的服务器可能同时安装了1.1 和2.0 版本的 Web 部署。 要从安装了2.0 的客户端进行部署，服务器必须仅安装 Web 部署2.0。 您必须与您的宿主提供商联系以解决此问题。

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>无法加载 SQL Server Compact 的本机组件

### <a name="scenario"></a>方案

当你运行部署的站点时，你将看到以下错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

部署的站点在应用程序的*bin*文件夹下没有*amd64*和*x86*子文件夹，其中包含本机程序集。 在安装了 SQL Server Compact 的计算机上，本机程序集位于*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*中。 若要将正确的文件导入到 Visual Studio 项目中正确的文件夹中，最好的方法是安装 NuGet SqlServerCompact 包。 包安装将添加一个后期生成脚本，用于将本机程序集复制到*amd64*和*x86*。 但是，若要部署这些文件，必须手动将其包含在项目中。 有关详细信息，请参阅[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>Code First 应用程序部署实体框架后出现 "路径无效" 错误

### <a name="scenario"></a>方案

部署一个应用程序，该应用程序使用 Entity Framework Code First 迁移和 DBMS （如 SQL Server Compact）将其数据库存储在应用\_Data 文件夹中的文件中。 你已 Code First 迁移配置为在第一次部署后创建数据库。 运行应用程序时，会收到类似于以下示例的错误消息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

Code First 正在尝试创建数据库，但应用\_数据文件夹不存在。 你在部署时没有*应用\_Data*文件夹中的任何文件，或者在**项目属性**窗口的 "**打包/发布 Web** " 选项卡上选择了 "**排除应用\_数据**"。 如果要将文件夹中的文件复制到服务器，部署过程不会在服务器上创建一个文件夹。 如果已在站点中设置了数据库，则如果在发布配置文件中选择了 "**删除目标位置的其他文件**"，则部署过程将删除文件和*应用\_Data*文件夹本身。 若要解决此问题，请在*应用\_Data*文件夹中放置一个占位符文件（如 .txt 文件），请确保未选择 "**排除应用"\_数据**并重新部署。 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>"无法使用与其基础 RCW 分离的 COM 对象。"

### <a name="scenario"></a>方案

你已成功使用一键式发布来部署你的应用程序，然后你开始收到此错误：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

若要解决此错误，通常需要关闭并重新启动 Visual Studio。

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a>部署失败，因为用于发布的用户凭据没有 setACL 机构

### <a name="scenario"></a>方案

发布失败，并显示一条错误消息，指出你没有权限设置文件夹权限（你使用的用户帐户没有 setACL 权限）。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

默认情况下，Visual Studio 设置对该站点的根文件夹的 "读取" 权限，并对该应用\_Data 文件夹具有写入权限。 如果你知道站点文件夹上的默认权限是正确的，并且不需要设置，则可以通过将 **&lt;IncludeSetACLProviderOn 目标&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 添加到发布配置文件（影响单个配置文件）或 wpp 文件（以影响所有配置文件）来禁用此行为。 有关如何编辑这些文件的信息，请参阅[如何：编辑配置文件中的部署设置（. .pubxml）文件](https://msdn.microsoft.com/library/ff398069.aspx)。 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a>当应用程序尝试写入应用程序文件夹时出现 "拒绝访问" 错误

### <a name="scenario"></a>方案

应用程序在尝试创建或编辑其中一个应用程序文件夹中的文件时出错，因为它不具有该文件夹的写权限。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

默认情况下，Visual Studio 设置对该站点的根文件夹的 "读取" 权限，并对该应用\_Data 文件夹具有写入权限。 如果你的应用程序需要对子文件夹的写访问权限，你可以设置该文件夹的权限，如[设置文件夹权限](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)和[部署到生产环境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教程中所示。 如果你的应用程序需要对该站点的根文件夹具有写入权限，则必须通过将 **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 添加到发布配置文件（以影响单个配置文件）或 wpp 文件（以影响所有配置文件）来防止其在根文件夹上设置只读访问权限。 有关如何编辑这些文件的信息，请参阅[如何：编辑配置文件中的部署设置（. .pubxml）文件](https://msdn.microsoft.com/library/ff398069.aspx)。 <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>配置错误-targetFramework 特性引用的版本晚于安装的 .NET Framework 版本

### <a name="scenario"></a>方案

已成功发布面向 ASP.NET 4.5 的 web 项目，但当你运行应用程序时（在 web.config 文件中将 `customErrors` 模式设置为 "off"），会收到以下错误：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

错误页面的 "源错误" 框中突出显示了 web.config 中的以下行：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

服务器不支持 ASP.NET 4.5。 请与宿主提供商联系，以确定是否可以添加对 ASP.NET 4.5 的支持。 如果升级服务器不是一个选项，则必须部署面向 ASP.NET 4 或更早版本的 web 项目。如果将 ASP.NET 4 或更早版本的 web 项目部署到相同的目标，请在 "**发布 web** " 向导的 "**设置**" 选项卡上选中 "**删除目标上的其他文件**" 复选框。 如果未选择 "**删除目标中的其他文件**"，则将继续获取配置错误页。

"项目**属性**" 窗口包含一个 "目标框架" 下拉列表，但不能通过只是将其从 **.NET Framework 4.5**改为 **.NET Framework 4**来解决此问题。 如果将目标框架更改为早期版本，则该项目仍将引用更高版本的程序集，并且将不会运行。 你必须手动更改这些引用或创建一个面向 .NET Framework 4 或更早版本的新项目。 有关详细信息，请参阅网站[的 .NET Framework 目标](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
