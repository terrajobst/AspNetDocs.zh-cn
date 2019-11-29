---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序： web.config 文件转换-3/12 |Microsoft Docs
author: tdykstra
description: 本系列教程说明如何使用 Visual Stu 部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 2b0df3d9-450b-4ea6-b315-4c9650722cad
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12
msc.type: authoredcontent
ms.openlocfilehash: fe71e6cfb0f4c5f1d99b326e9d90edb6c8c5feee
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600545"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-webconfig-file-transformations---3-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 应用程序： web.config 文件转换-3/12

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 本系列教程介绍了如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，部署（发布）包含 SQL Server Compact 数据库的 ASP.NET web 应用程序项目。 如果安装 Web 发布更新，还可以使用 Visual Studio 2010。 有关系列的简介，请参阅本[系列中的第一个教程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。
> 
> 有关演示 Visual Studio 2012 RC 版本后引入的部署功能的教程，演示如何部署 SQL Server Compact 以外的 SQL Server 版本，并演示如何部署到 Azure App Service Web 应用，请参阅[使用 Visual Studio 的 ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概述

本教程介绍如何在将 web.config 文件部署到不同目标环境时，自动完成更改*该文件的*过程。 大多数应用*程序的 web.config 文件中*的设置在部署应用程序时必须不同。 自动执行这些更改的过程使您无需在每次部署时手动执行这些更改，这会导致单调乏味且容易出错。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 转换与 Web 部署参数

可以通过两种方法自动*执行更改 web.config*文件设置的过程： web.config[转换](https://msdn.microsoft.com/library/dd465326.aspx)和[Web 部署参数](https://msdn.microsoft.com/library/ff398068.aspx)。 Web.config*转换文件*包含 XML 标记，该标记*指定在部署 web.config 文件时*如何对其进行更改。 您可以为特定的生成配置和特定发布配置文件指定不同的更改。 默认生成配置为 "调试" 和 "发布"，您可以创建自定义生成配置。 发布配置文件通常对应于目标环境。 （有关详细信息，请参阅在[部署到 IIS 作为测试环境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教程中发布配置文件。）

Web 部署参数可用于指定在部署过程中必须配置的多种不同类型的设置，包括在*web.config*文件中找到的设置。 当*用于指定 web.config*文件更改时，Web 部署参数的设置将更复杂，但在部署之前，您不知道要设置的值，则这些参数非常有用。 例如，在企业环境中，你可以创建一个*部署包*，并将其提供给 it 部门中的人员，以便在生产环境中安装，并且该用户必须能够输入你不知道的连接字符串或密码。

对于本教程所涵盖的方案，您知道必须对*web.config 文件执行的所有*操作，因此您无需使用 Web 部署参数。 您将根据所使用的生成配置，配置一些不同的转换，并且某些转换因所使用的发布配置文件而有所不同。

## <a name="creating-transformation-files-for-publish-profiles"></a>为发布配置文件创建转换文件

在**解决方案资源管理器**中，*展开 web.config*以查看默认情况下为两个默认生成配置*创建的 web.config 和* *web.config*转换文件。

![Web。 config_transform_files](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image1.png)

您可以创建自定义生成配置的转换文件，方法是右键单击 web.config 文件，然后从上下文菜单中选择 "**添加配置转换**"，但对于本教程，无需执行此操作。

确实需要两个转换文件，用于配置与部署目标（而不是生成配置）相关的更改。 此类设置的一个典型示例是不同于测试与生产的 WCF 终结点。 在后面的教程中，你将创建名为 "测试" 和 "生产" 的发布配置文件，因此需要一个*web.config*文件和一个*web.config*文件。

必须手动创建绑定到发布配置文件的转换文件。 在**解决方案资源管理器**中，右键单击 ContosoUniversity 项目，然后选择 "**在 Windows 资源管理器中打开文件夹**"。

![Open_folder_in_Windows_Explorer](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image2.png)

在**Windows 资源管理器**中，选择*web.config*文件，复制文件，然后粘贴两个副本。 重命名这些副本*web.config* *和 web.config*，然后关闭**Windows 资源管理器**。

在**解决方案资源管理器**中，单击 "**刷新**" 以查看新文件。

选择新文件，右键单击，然后单击上下文菜单中的 "**包括在项目**中"。

![在项目中包括测试和生产配置文件](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image3.png)

若要防止部署这些文件，请在**解决方案资源管理器**中选择这些文件，然后在 "**属性**" 窗口中，将 "**生成操作**" 属性从 "**内容**" 更改为 "**无**"。 （将自动禁止部署基于生成配置的转换文件。）

你现在已准备好将*web.config 转换输入到* *web.config 转换文件中。*

## <a name="limiting-error-log-access-to-administrators"></a>限制对管理员的错误日志访问

如果在应用程序运行时出现错误，应用程序将显示一个通用错误页来代替系统生成的错误页，并使用[Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)进行错误日志记录和报告。 *Web.config 文件中*的 `customErrors` 元素指定错误页：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample1.xml)]

若要查看错误页，请暂时将 `customErrors` 元素的 `mode` 属性从 "RemoteOnly" 更改为 "打开"，并从 Visual Studio 运行该应用程序。 请求无效的 URL （如*Studentsxxx*）会导致错误。 你会看到 " *GenericErrorPage* " 页，而不是 IIS 生成的 "找不到页" 错误页。

[![Error_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image5.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image4.png)

若要查看错误日志，请将 URL 中的所有内容替换为*elmah. axd*的端口号（在屏幕截图中，`http://localhost:51130/elmah.axd`），然后按 enter：

[![Elmah_log_page](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image7.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image6.png)

完成后，不要忘记将 `customErrors` 元素设置回 "RemoteOnly" 模式。

在您的开发计算机上，可以方便地访问错误日志页，但在生产环境中，这会带来安全风险。 对于生产站点，可以通过在*web.config*文件中配置转换来添加一个授权规则，该规则会将错误日志访问仅限于管理员。

打开*web.config* ，并在打开的 `configuration` 标记后立即添加一个新的 `location` 元素，如下所示。 （请确保仅添加 `location` 元素，而不是在此处显示的周围标记，以提供某些上下文。）

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample2.xml?highlight=2-9)]

"Insert" `Transform` 特性值导致将此 `location` 元素添加为*web.config*文件中任何现有 `location` 元素的同级元素。 （已经有一个 `location` 元素指定了**更新信用额度**页面的授权规则。）在部署后测试生产站点时，将进行测试，以验证此授权规则是否有效。

不需要在测试环境中限制错误日志访问，因此不需要将此代码添加到*web.config*文件。

> [!NOTE] 
> 
> **安全说明**切勿在生产应用程序中向公众显示错误详细信息，或者将该信息存储在公共位置。 攻击者可以使用错误信息发现站点中的漏洞。 如果你在自己的应用程序中使用 ELMAH，请务必调查如何配置 ELMAH 来最大程度地降低安全风险。 本教程中的 ELMAH 示例不应被视为建议的配置。 这是一个示例，它是为了说明如何处理应用程序必须能够在其中创建文件的文件夹。

## <a name="setting-an-environment-indicator"></a>设置环境指示器

常见的情况是，在你部署到的每个环境中必须有不同的*web.config 文件设置。* 例如，调用 WCF 服务的应用程序可能需要在测试环境和生产环境中使用不同的终结点。 Contoso 大学应用程序还包括此类型的设置。 此设置控制站点页面上的可见指示器，该指示器告诉你处于哪个环境（例如开发、测试或生产）。 设置值确定应用程序是将 "（Dev）" 还是 "（Test）" 追加到站点的主标题上 *。母版页*母版页：

[![Environment_indicator](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image9.png)](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/_static/image8.png)

当应用程序在生产环境中运行时，将省略环境指示器。

Contoso 大学网页读取在*web.config 文件 `appSettings`* 中设置的值，以确定应用程序运行的环境：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample3.xml)]

在测试环境中，该值应为 "Test"，在生产环境中应为 "生产"。

打开*web.config* ，并在前面添加的 `location` 元素的开始标记前面添加一个 `appSettings` 元素：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample4.xml)]

`xdt:Transform` 属性值 "SetAttributes" 指示此转换的目的是更改*web.config 文件中*现有元素的属性值。 `xdt:Locator` 属性值 "Match （key）" 指示要修改的元素是其 `key` 属性与此处指定的 `key` 属性匹配的元素。 `add` 元素的唯一其他属性 `value`，这就是在部署的*web.config*文件中将更改的内容。 此代码会导致在部署到*生产的 web.config 文件中*将 `Environment` `appSettings` 元素的 `value` 属性设置为 "生产"。

接下来，将相同的更改应用到*web.config*文件，但将 `value` 设置为 "Test" 而不是 "生产"。 完成后， *web.config*中的 `appSettings` 部分将类似于以下示例：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample5.xml)]

## <a name="disabling-debug-mode"></a>禁用调试模式

对于发布版本，无论部署到哪个环境，都不需要启用调试。 默认情况下，将使用从 `compilation` 元素删除 `debug` 特性的代码自动创建*web.config*转换文件：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample6.xml)]

在部署发布版本时，`Transform` 特性会使已部署的*web.config*文件中省略 `debug` 特性。

此相同转换在测试和生产转换文件中，因为您是通过复制发布转换文件创建的。 不需要将其复制到该文件中，因此请打开每个文件，删除**编译**元素，并保存并关闭每个文件。

## <a name="setting-connection-strings"></a>设置连接字符串

在大多数情况下，你不需要设置连接字符串转换，因为你可以在发布配置文件中指定连接字符串。 但在部署 SQL Server Compact 数据库时，如果使用 Entity Framework Code First 迁移更新目标服务器上的数据库，则会出现异常。 对于这种情况，您必须指定将在服务器上用于更新数据库架构的其他连接字符串。 若要设置此转换，请将一个 **&lt;connectionStrings&gt;** 元素添加到紧跟在*web.config*和*web.config 转换文件*中的打开 **&lt;配置&gt;** 标记之后：

[!code-xml[Main](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12/samples/sample7.xml)]

`Transform` 特性指定此连接字符串将添加到已部署的*web.config*文件中的*connectionStrings*元素。 （如果不存在，则发布过程会自动创建此附加的连接字符串，但默认情况下， **providerName**特性设置为 `System.Data.SqlClient`，这不能 SQL Server Compact。 通过手动添加连接字符串，你可以保持部署过程创建具有错误的提供程序名称的连接字符串元素。）

你现在已经指定了部署 Contoso 大学应用程序进行测试和生产所*需的所有 web.config 转换。* 在以下教程中，你将负责执行需要设置项目属性的部署设置任务。

## <a name="more-information"></a>详细信息

有关本教程涵盖的主题的详细信息，请参阅[ASP.NET 部署内容映射](https://msdn.microsoft.com/library/bb386521.aspx)中的 web.config 转换方案。

> [!div class="step-by-step"]
> [上一页](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)
> [下一页](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
