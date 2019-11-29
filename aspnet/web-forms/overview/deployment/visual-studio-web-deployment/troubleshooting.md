---
uid: web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
title: 使用 Visual Studio 的 ASP.NET Web 部署：疑难解答 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 06/01/2015
ms.assetid: c0090595-ab3b-4b9b-9e16-7a1891e8cb2f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: b42476fca18b04f4557a216ee205cfd9220023e8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74623575"
---
# <a name="aspnet-web-deployment-using-visual-studio-troubleshooting"></a>使用 Visual Studio 的 ASP.NET Web 部署：疑难解答

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。

本页介绍使用 Visual Studio 部署 ASP.NET web 应用程序时可能出现的一些常见问题。 对于每个问题，都提供了一个或多个可能的原因和相应的解决方案。

显示的方案适用于 Azure 和第三方托管提供程序。 有关 Azure App Service 中的 web 应用进行故障排除的详细信息，请参阅以下资源：

- [使用 Visual Studio 对 Azure 应用服务中的 Web 应用进行故障排除](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)
- [监视 Azure App Service 中的 Web 应用](https://azure.microsoft.com/documentation/articles/web-sites-monitor//)
- [宣布推出 Windows AZURE SDK 2.0 for .net](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) （ScottGu 的博客，演示如何在 Visual Studio 中获取诊断日志）

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>"/" 应用程序中的服务器错误-当前自定义错误设置阻止远程查看错误的详细信息

### <a name="scenario"></a>方案

将站点部署到远程主机之后，会收到一条错误消息，其中提及了 Web.config 文件中的 customErrors 设置，但未指示错误的实际原因：

[!code-xml[Main](troubleshooting/samples/sample1.xml)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

默认情况下，仅当你的 web 应用程序在本地计算机上运行时，ASP.NET 才会显示详细的错误信息。 通常，当您的 web 应用程序在 Internet 上公开可用时，您不想显示详细的错误信息，因为黑客可能能够利用此信息来查找应用程序中的漏洞。 但是，在部署站点或更新站点时，有时会出现问题，需要获取实际的错误消息。

若要使应用程序能够在远程主机上运行时显示详细的错误消息，请编辑 Web.config 文件以将 customErrors 模式设置为 off，重新部署应用程序，然后再次运行应用程序：

1. 如果应用程序的 web.config 文件在 customErrors 元素中有一个 "" 元素，则将 mode 特性更改为 "off"。 否则，请将 customErrors 元素添加到 mode 特性设置为 "off" 的 "system.web" 元素中，如以下示例中所示： 

    [!code-xml[Main](troubleshooting/samples/sample2.xml)]
2. 部署应用程序。
3. 运行该应用程序，并重复您之前执行的任何导致错误的操作。 现在，你可以看到实际的错误消息是什么。
4. 解决错误后，还原原始 customErrors 设置并重新部署应用程序。

## <a name="cannot-createshadow-copy-contosouniversity-when-that-file-already-exists"></a>如果文件已存在，则无法创建/影像复制 ' ContosoUniversity '。

### <a name="scenario"></a>方案

尝试在 Visual Studio 中运行项目时，会出现一个错误页面，其中包含类似于以下示例的消息：

“/”应用程序中的服务器错误ЎЈ 如果文件已存在，则无法创建/影像复制 ' ContosoUniversity '。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

请稍等片刻并刷新浏览器，或重新编译该站点，然后再次尝试运行它。

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>使用 SQL Server Compact 的网页中的访问被拒绝

### <a name="scenario"></a>方案

当你部署使用 SQL Server Compact 的站点，并且在已部署的站点中运行访问该数据库的页面时，你将看到以下错误消息：

拒绝访问。 （HRESULT 中的异常：0x80070005 （E\_ACCESSDENIED））

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

服务器上的网络服务帐户需要能够读取*bin\amd64*或*bin\x86*文件夹中的 SQL 服务压缩本机二进制文件，但它不具有对这些文件夹的读取权限。 设置*bin*文件夹的 "网络服务的读取权限"，并确保将权限扩展到子文件夹。

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>由于权限不足而无法读取配置文件

### <a name="scenario"></a>方案

单击 Visual Studio 的 "发布" 按钮将应用程序部署到本地计算机上的 IIS 后，发布将失败，并且 "**输出**" 窗口将显示如下错误消息：

读取 IIS 配置文件 "计算机/重定向" 时出错。 执行此操作的标识为 .。。错误：无法读取配置文件，因为权限不足。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

若要在本地计算机上使用一键式 "发布到 IIS"，必须使用管理员权限运行 Visual Studio。 关闭 Visual Studio 并以管理员权限重新启动它。

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>无法连接到目标计算机 .。。使用指定的进程

### <a name="scenario"></a>方案

单击 Visual Studio 的 "发布" 按钮以部署应用程序时，发布将失败，并且 "**输出**" 窗口将显示如下错误消息：

[!code-console[Main](troubleshooting/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

代理服务器中断了与目标服务器的通信。 在 Windows "控制面板" 或 Internet Explorer 中，选择 " **Internet 选项**"，然后选择 "**连接**" 选项卡。在 " **Internet 属性**" 对话框中，单击 " **LAN 设置**"。 在 "局域网 **（LAN）设置**" 对话框中，清除 "**自动检测设置**" 复选框。 然后再次单击 "发布" 按钮。

如果问题仍然存在，请与系统管理员联系，以确定可对代理或防火墙设置执行的操作。 发生此问题的原因是 Web 部署为 Web 管理服务部署使用非标准端口（8172）;对于其他连接，Web 部署使用端口80。 部署到第三方托管提供程序时，通常使用 Web 管理服务。

## <a name="default-net-40-application-pool-does-not-exist"></a>默认的 .NET 4.0 应用程序池不存在

### <a name="scenario"></a>方案

部署需要 .NET Framework 4 的应用程序时，将看到以下错误消息：

默认的 .NET 4.0 应用程序池不存在，或无法添加应用程序。 请验证是否在此计算机上安装了 ASP.NET 4.0。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

IIS 中未安装 ASP.NET 4。 如果你要部署到的服务器是你的开发计算机并在其上安装了 Visual Studio 2010，则将在计算机上安装 ASP.NET 4，但可能不会在 IIS 中安装。 在要部署到的服务器上，打开提升的命令提示符，并运行以下命令在 IIS 中安装 ASP.NET 4：

[!code-console[Main](troubleshooting/samples/sample4.cmd)]

你可能还需要手动设置默认应用程序池的 .NET Framework 版本。 有关详细信息，请参阅本系列中的将部署到 IIS 作为测试环境教程。

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>初始化字符串的格式不符合从索引0处开始的规范。

### <a name="scenario"></a>方案

使用一键式发布部署应用程序后，在运行访问数据库的页时，会收到以下错误消息：

初始化字符串的格式不符合从索引0处开始的规范。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

在部署*的站点*中打开 web.config 文件，然后检查连接字符串值是否以 `$(ReplaceableToken_`开头，如以下示例中所示：

[!code-xml[Main](troubleshooting/samples/sample5.xml)]

如果连接字符串与此示例类似，则编辑项目文件，并将以下属性添加到适用于所有生成配置的 PropertyGroup 元素：

[!code-xml[Main](troubleshooting/samples/sample6.xml)]

然后重新部署应用程序。

## <a name="http-500-internal-server-error"></a>HTTP 500 内部服务器错误

### <a name="scenario"></a>方案

当你运行部署的站点时，你将看到以下错误消息，其中没有指示错误原因的特定信息：

HTTP 错误 500-内部服务器错误。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

出现500错误的原因有很多，但如果您遵循这些教程，其中一种可能的原因是您将 XML 元素放在某个 Web.config 转换文件的错误位置。 例如，如果将插入 &lt;位置&gt; 元素的转换添加到 &lt;system.web&gt; 下，而不是直接在 &lt;配置&gt;下，则会出现此错误。 您可以使用 web.config 转换预览功能来验证转换是否按预期方式工作。 如果找到编码错误的转换，则解决方案是更正转换文件并重新部署。 如果错误不明显，请尝试注释转换和重新部署，以查看导致500错误的转换。

## <a name="http-50021-internal-server-error"></a>HTTP 500.21 内部服务器错误

### <a name="scenario"></a>方案

当你运行部署的站点时，你将看到以下错误消息：

HTTP 错误 500.21-内部服务器错误。 处理程序 "Pagehandlerfactory-isapi-集成" 的模块列表中有一个错误的模块 "ManagedPipelineHandler"。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

部署的站点的目标为 ASP.NET 4，但未在服务器上的 IIS 中注册 ASP.NET 4。 在服务器上打开提升的命令提示符，并通过运行以下命令来注册 ASP.NET 4：

[!code-console[Main](troubleshooting/samples/sample7.cmd)]

你可能还需要手动设置默认应用程序池的 .NET Framework 版本。 有关详细信息，请参阅本系列中的将部署到 IIS 作为测试环境教程。

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a>登录无法在应用\_数据中打开 SQL Server Express 数据库

### <a name="scenario"></a>方案

在应用中*将 web.config 文件连接*字符串更新为指向 SQL Server Express 数据库的 *.Mdf*文件 *\_Data*文件夹，并且首次运行应用程序时，将看到以下错误消息：

SqlClient. SqlException：无法打开登录所请求的数据库 "DatabaseName"。 登录失败。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

即使删除了以前存在的数据库的 *.mdf*文件， *.mdf*文件的名称也不能与计算机上存在的任何 SQL Server Express 数据库的名称相匹配。 将 *.mdf*文件的名称更改为从未用作数据库名称的名称，并更改*web.config*文件以使用新名称。 作为替代方法，可以使用[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除以前存在的 SQL Server Express 数据库。

## <a name="model-compatibility-cannot-be-checked"></a>无法检查模型的兼容性

### <a name="scenario"></a>方案

已*将 web.config 文件连接*字符串更新为指向新的 SQL Server Express 数据库，并且首次运行应用程序时，将看到以下错误消息：

无法检查模型兼容性，因为数据库不包含模型元数据。 确保已将 IncludeMetadataConvention 添加到 DbModelBuilder 约定。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

如果在您的计算机上曾经使用过您放置在 web.config 文件中的数据库名称，则可能已经存在包含某些表的数据库。 选择之前未在计算机上使用的新名称，*然后将 web.config 文件更改*为指向 "使用此新数据库名称"。 作为替代方法，可以使用[SQL Server Express 实用工具](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)或[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)删除现有数据库。

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>脚本尝试创建用户或角色时出现 SQL 错误

### <a name="scenario"></a>方案

你使用的是在 "**包/发布 SQL** " 选项卡上配置的数据库部署，在部署过程中运行的 SQL 脚本包含 "创建用户" 或 "创建角色" 命令，在执行这些命令时脚本执行将失败。 您可能会看到更详细的消息，如下所示：

[!code-console[Main](troubleshooting/samples/sample8.cmd)]

如果在 "**发布 Web** " 向导而不是 "**包/发布 SQL** " 选项卡中配置数据库部署后发生此错误，请在[配置和部署](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)论坛中创建一个线程，该解决方案将添加到此故障排除页。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

用于执行部署的用户帐户没有创建用户或角色的权限。 例如，托管公司可以将 db\_datareader、db\_datawriter 和 db\_ddladmin 角色分配给它为您设置的用户帐户。 它们足以用于创建大多数数据库对象，但不能用于创建用户或角色。 避免此错误的一种方法是从数据库部署中排除用户和角色。 为此，可以编辑数据库的自动生成脚本的 PreSource 元素，使其包含以下属性：

[!code-console[Main](troubleshooting/samples/sample9.cmd)]

有关如何编辑项目文件中的 PreSource 元素的信息，请参阅[如何：在项目文件中编辑部署设置](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)。 如果你的开发数据库中的用户或角色需要位于目标数据库中，请与你的托管提供商联系以获得帮助。

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>在部署过程中运行自定义脚本时出现 SQL Server 超时错误

### <a name="scenario"></a>方案

您已经指定了要在部署过程中运行的自定义 SQL 脚本，当 Web 部署运行它们时，它们将超时。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

运行具有不同事务模式的多个脚本会导致超时错误。 默认情况下，自动生成的脚本在事务中运行，但自定义脚本不会运行。 如果在 "**包/发布 SQL** " 选项卡上选择了 "**从现有数据库提取数据和/或架构**" 选项，并且添加自定义 SQL 脚本，则必须更改某些脚本的事务设置，以便所有脚本都使用相同的事务设置。 有关详细信息，请参阅[如何：使用 Web 应用程序项目部署数据库](https://msdn.microsoft.com/library/dd465343.aspx)。

如果已配置事务设置，使所有这些设置都相同但仍然出现此错误，则一种可能的解决方法是单独运行脚本。 在 "**包/发布**SQL" 选项卡的 "**数据库脚本**" 网格中，清除导致超时错误的脚本的 "**包含**" 复选框，然后发布项目。 然后返回到 "**数据库脚本**" 网格，选中该脚本的 "**包含**" 复选框，并清除其他脚本的 "**包含**" 复选框。 然后重新发布项目。 这一次，当你发布时，只会运行选定的自定义脚本。

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>站点清单的流数据尚不可用

### <a name="scenario"></a>方案

当使用带有 t （test）选项的*deploy .cmd*文件安装包时，将看到以下错误消息：

错误： "sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript" 的流数据尚不可用。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

错误消息表示该命令无法生成测试报告。 但是，如果使用 y （实际安装）选项，则该命令可能运行。 此消息仅指示在测试模式下运行命令时出现问题。

## <a name="this-application-requires-managedruntimeversion-v40"></a>此应用程序需要 ManagedRuntimeVersion v4。0

### <a name="scenario"></a>方案

当你尝试部署时，你会看到以下错误消息：

尝试使用的应用程序池的 "managedRuntimeVersion" 属性设置为 "v2.0"。 此应用程序需要 "4.0"。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

IIS 中未安装 ASP.NET 4。 如果你要部署到的服务器是你的开发计算机并在其上安装了 Visual Studio 2010，则将在计算机上安装 ASP.NET 4，但可能不会在 IIS 中安装。 在要部署到的服务器上，打开提升的命令提示符，并运行以下命令在 IIS 中安装 ASP.NET 4：

[!code-console[Main](troubleshooting/samples/sample10.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>无法强制转换 DeploymentProviderOptions

### <a name="scenario"></a>方案

部署包时，将看到以下错误消息：

无法将类型为 "DeploymentProviderOptions" 的对象强制转换为 "DeploymentProviderOptions" 类型。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

尝试使用 Web 部署 1.1 UI 从 IIS 管理器部署到安装了 Web 部署2.0 的服务器。 如果使用 IIS 远程管理工具通过导入包进行部署，请在建立连接时选中 "**可用的新功能**" 对话框。 （仅当首次建立连接时，才会显示此对话框。 若要清除该连接并重新启动，请关闭 IIS 管理器，然后通过在命令提示符下输入 inetmgr/reset 来重新启动它。）如果列出的其中一项功能**WEB 部署 UI**，并且版本号低于8，则部署到的服务器可能同时安装了1.1 和2.0 版本的 Web 部署。 要从安装了2.0 的客户端进行部署，服务器必须仅安装 Web 部署2.0。 您必须与您的宿主提供商联系以解决此问题。

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>无法加载 SQL Server Compact 的本机组件

### <a name="scenario"></a>方案

当你运行部署的站点时，你将看到以下错误消息：

无法加载与版本8482的 ADO.NET 提供程序对应的 SQL Server Compact 的本机组件。 安装 SQL Server Compact 的正确版本。 有关更多详细信息，请参阅知识库文章974247。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

部署的站点在应用程序的*bin*文件夹下没有*amd64*和*x86*子文件夹，其中包含本机程序集。 在安装了 SQL Server Compact 的计算机上，本机程序集位于*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*中。 若要将正确的文件导入到 Visual Studio 项目中正确的文件夹中，最好的方法是安装 NuGet SqlServerCompact 包。 包安装将添加一个后期生成脚本，用于将本机程序集复制到*amd64*和*x86*。 但是，若要部署这些文件，必须手动将其包含在项目中。 有关详细信息，请参阅[部署 SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教程。

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>Code First 应用程序部署实体框架后出现 "路径无效" 错误

### <a name="scenario"></a>方案

部署一个应用程序，该应用程序使用 Entity Framework Code First 迁移和 DBMS （如 SQL Server Compact）将其数据库存储在应用\_Data 文件夹中的文件中。 你已 Code First 迁移配置为在第一次部署后创建数据库。 运行应用程序时，会收到类似于以下示例的错误消息：

路径无效。 检查数据库的目录。 [路径 = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf]

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

Code First 正在尝试创建数据库，但应用\_数据文件夹不存在。 你在部署时没有*应用\_Data*文件夹中的任何文件，或者在项目属性窗口的 "**包/发布 Web** " 选项卡上选择了 "**排除应用\_数据**"。 如果要将文件夹中的文件复制到服务器，部署过程不会在服务器上创建一个文件夹。 如果已在站点中设置了数据库，则如果在发布配置文件中选择了 "**删除目标位置的其他文件**"，则部署过程将删除文件和*应用\_Data*文件夹本身。 若要解决此问题，请在*应用\_Data*文件夹中放置一个占位符文件（如 .txt 文件），请确保未选择 "**排除应用"\_数据**并重新部署。

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>"无法使用与其基础 RCW 分离的 COM 对象。"

### <a name="scenario"></a>方案

你已成功使用一键式发布来部署你的应用程序，然后你开始收到此错误：

Web 部署任务失败。 （无法完成对远程代理 URL "<https://serverurl.com/msdeploy.axd?site=sitename>" 的请求。）  
 无法完成对远程代理 URL "<https://url/msdeploy.axd?site=sitename>" 的请求。  
请求已中止：请求已取消。  
不能使用与其基础 RCW 分离的 COM 对象。

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

默认情况下，Visual Studio 设置对该站点的根文件夹的 "读取" 权限，并对该应用\_Data 文件夹具有写入权限。 如果你的应用程序需要对子文件夹的写访问权限，你可以设置该文件夹的权限，如此系列中的设置文件夹权限和部署到生产环境教程中所示。 如果你的应用程序需要对该站点的根文件夹具有写入权限，则必须通过将 **&lt;IncludeSetACLProviderOn Destination&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 添加到发布配置文件（以影响单个配置文件）或 wpp 文件（以影响所有配置文件）来防止其在根文件夹上设置只读访问权限。 有关如何编辑这些文件的信息，请参阅[如何：编辑配置文件中的部署设置（. .pubxml）文件](https://msdn.microsoft.com/library/ff398069.aspx)。

<a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>配置错误-targetFramework 特性引用的版本晚于安装的 .NET Framework 版本

### <a name="scenario"></a>方案

已成功发布面向 ASP.NET 4.5 的 web 项目，但当你运行应用程序（在 web.config 文件中将 customErrors 模式设置为 "off"）时，会收到以下错误：

Web.config 文件的 &lt;编译&gt; 元素中的 "targetFramework" 特性仅用于面向 .NET Framework 版本4.0 和更高版本（例如，"&lt;编译 targetFramework =" 4.0 "&gt;"）。 "TargetFramework" 属性当前引用的版本高于 .NET Framework 安装的版本。 指定 .NET Framework 的有效目标版本，或者安装 .NET Framework 的所需版本。

错误页面的 "源错误" 框中突出显示了 web.config 中的以下行：

&lt;编译 targetFramework = "4.5"/&gt;

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

服务器不支持 ASP.NET 4.5。 请与宿主提供商联系，以确定是否可以添加对 ASP.NET 4.5 的支持。 如果升级服务器不是一个选项，则必须部署面向 ASP.NET 4 或更早版本的 web 项目。

如果将 ASP.NET 4 或更早版本的 web 项目部署到相同的目标，请在 "**发布 web** " 向导的 "**设置**" 选项卡上选中 "**删除目标上的其他文件**" 复选框。 如果未选择 "**删除目标中的其他文件**"，则将继续获取配置错误页。

"项目**属性**" 窗口包含一个 "目标框架" 下拉列表，但不能通过只是将其从 **.NET Framework 4.5**改为 **.NET Framework 4**来解决此问题。 如果将目标框架更改为早期版本，则该项目仍将引用更高版本的程序集，并且将不会运行。 你必须手动更改这些引用或创建一个面向 .NET Framework 4 或更早版本的新项目。 有关详细信息，请参阅网站[的 .NET Framework 目标](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)。

## <a name="medium-trust-errors"></a>中等信任错误

### <a name="scenario"></a>方案

在生产环境中运行应用程序时，它会获取与中等信任相关的错误。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

许多第三方托管提供商在中等信任环境下运行你的网站，这意味着不允许这样做。 例如，应用程序代码不能访问 Windows 注册表，也无法读取或写入您的应用程序的文件夹层次结构之外的文件。 默认情况下，你的应用程序在本地计算机上以*完全信任*的方式运行，这意味着应用程序可以执行在将其部署到生产环境时失败的操作。

你可以将应用程序配置为在本地 IIS 环境中的中等信任级别运行，以便进行故障排除。 为此，请打开应用程序的*web.config*文件，并在**system.web**元素中添加一个**信任**元素，如本示例中所示。

[!code-xml[Main](troubleshooting/samples/sample11.xml)]

现在，应用程序将在 IIS 中的中等信任环境中运行，即使在本地计算机上也是如此。

如果要部署到 Azure App Service，请不要执行此操作，因为 Azure 不需要中等信任。 在2012年2月编写本教程时，使用此方法使应用程序在中等信任环境下运行将导致 Azure 出错。

如果使用 Entity Framework Code First 迁移并且要将部署到在中等信任环境下运行应用程序的宿主提供程序，请确保已安装版本5.0 或更高版本。 在实体框架版本4.3 中，迁移需要完全信任才能更新数据库架构。

## <a name="http-40417-not-found-error"></a>"找不到 HTTP 404.17" 错误

### <a name="scenario"></a>方案

当你在 IIS 中的开发计算机上运行部署的站点时，你将看到以下错误消息，报告服务器无法处理 default.aspx：

HTTP 错误 404.17-未找到

请求的内容将显示为脚本，而不会由静态文件处理程序提供。

### <a name="possible-cause-and-solution"></a>可能的原因和解决方案

ASP.NET 4.5 可能未安装在您的计算机上。 请参阅本系列中的部署到 IIS 作为测试环境教程教程中的步骤，其中介绍了如何安装 ASP.NET 4.5。

> [!div class="step-by-step"]
> [上一部分](deploying-extra-files.md)
