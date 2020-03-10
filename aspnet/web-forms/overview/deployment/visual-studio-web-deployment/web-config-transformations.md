---
uid: web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
title: 使用 Visual Studio 的 ASP.NET Web 部署： web.config 文件转换 |Microsoft Docs
author: tdykstra
description: 本系列教程介绍了如何通过来将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供程序。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 5a2a927b-14cb-40bc-867a-f0680f9febd7
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations
msc.type: authoredcontent
ms.openlocfilehash: a9d39547c94a63003442ba6fe1257693dde24b05
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78513710"
---
# <a name="aspnet-web-deployment-using-visual-studio-webconfig-file-transformations"></a>使用 Visual Studio 的 ASP.NET Web 部署： web.config 文件转换

作者： [Tom Dykstra](https://github.com/tdykstra)

[下载初学者项目](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本系列教程介绍了如何使用 Visual Studio 2012 或 Visual Studio 2010，将 ASP.NET web 应用程序部署（发布）到 Azure App Service Web 应用或第三方托管提供商。 有关序列的信息，请参阅本[系列中的第一个教程](introduction.md)。

## <a name="overview"></a>概述

本教程介绍如何在将 web.config 文件部署到不同目标环境时，自动完成更改*该文件的*过程。 大多数应用*程序的 web.config 文件中*的设置在部署应用程序时必须不同。 自动执行这些更改的过程使您无需在每次部署时手动执行这些更改，这会导致单调乏味且容易出错。

提醒：如果你收到一条错误消息或在你完成本教程时无法正常工作，请务必查看[故障排除页](troubleshooting.md)。

## <a name="webconfig-transformations-versus-web-deploy-parameters"></a>Web.config 转换与 Web 部署参数

可以通过两种方法自动*执行更改 web.config*文件设置的过程： web.config[转换](https://msdn.microsoft.com/library/dd465326.aspx)和[Web 部署参数](https://msdn.microsoft.com/library/ff398068.aspx)。 Web.config*转换文件*包含 XML 标记，该标记*指定在部署 web.config 文件时*如何对其进行更改。 您可以为特定的生成配置和特定发布配置文件指定不同的更改。 默认生成配置为 "调试" 和 "发布"，您可以创建自定义生成配置。 发布配置文件通常对应于目标环境。 （有关详细信息，请参阅在[部署到 IIS 作为测试环境](deploying-to-iis.md)教程中发布配置文件。）

Web 部署参数可用于指定在部署过程中必须配置的多种不同类型的设置，包括在*web.config*文件中找到的设置。 当*用于指定 web.config*文件更改时，Web 部署参数的设置将更复杂，但在部署之前，您不知道要设置的值，则这些参数非常有用。 例如，在企业环境中，你可以创建一个*部署包*，并将其提供给 it 部门中的人员，以便在生产环境中安装，并且该用户必须能够输入你不知道的连接字符串或密码。

对于本教程系列涵盖的方案，你事先知道需要对*web.config 文件进行的所有*操作，因此你无需使用 Web 部署参数。 您将根据所使用的生成配置，配置一些不同的转换，并且某些转换因所使用的发布配置文件而有所不同。

<a id="watransforms"></a>

## <a name="specifying-webconfig-settings-in-azure"></a>在 Azure 中指定 web.config 设置

如果要更改的*web.config*文件设置位于 `<connectionStrings>` 或 `<appSettings>` 元素中，并且如果要部署到 Azure App Service 中的 web 应用，则可以使用另一个选项在部署期间自动执行更改。 可以在 web 应用的 "管理门户" 页的 "**配置**" 选项卡中输入想要在 Azure 中生效的设置（向下滚动到 "**应用设置**" 和 "**连接字符串**" 部分）。 部署项目时，Azure 会自动应用所做的更改。 有关详细信息，请参阅[Microsoft Azure 网站：应用程序字符串和连接字符串的工作原理](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx)。

## <a name="default-transformation-files"></a>默认转换文件

在**解决方案资源管理器**中，*展开 web.config*以查看默认情况下为两个默认生成配置*创建的 web.config 和* *web.config*转换文件。

![Web.config_transform_files](web-config-transformations/_static/image1.png)

您可以通过右键单击 web.config 文件，然后从上下文菜单中选择 "**添加配置转换**"，为自定义生成配置创建转换文件。 对于本教程，无需执行此操作，并且菜单选项被禁用，因为尚未创建任何自定义生成配置。

稍后，你将创建三个更多转换文件，分别用于测试、暂存和生产发布配置文件。 你将在发布配置文件转换文件中处理的设置的一个典型示例，因为它依赖于目标环境是一个不同于测试与生产的 WCF 终结点。 您将在后面的教程中创建发布配置文件转换文件，之后再创建这些文件。

## <a name="disable-debug-mode"></a>禁用调试模式

依赖于生成配置的设置（而不是目标环境）的一个示例是 `debug` 特性。 对于发布版本，通常要禁用调试，而不考虑要部署到的环境。 因此，默认情况下，Visual Studio 项目模板会创建*web.config*转换文件，其中包含从 `compilation` 元素中移除 `debug` 特性的代码。 下面是默认的*web.config*：除了注释掉的一些示例转换代码，它还包括删除 `debug` 属性的 `compilation` 元素中的代码：

[!code-xml[Main](web-config-transformations/samples/sample1.xml?highlight=18)]

`xdt:Transform="RemoveAttributes(debug)"` 特性指定要从已部署的*web.config*文件中的 `system.web/compilation` 元素中移除 `debug` 特性。 这将在每次部署发布版本时完成。

## <a name="limit-error-log-access-to-administrators"></a>限制对管理员的错误日志访问

如果在应用程序运行时出现错误，应用程序将显示一个通用错误页来代替系统生成的错误页，并使用[Elmah NuGet 包](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)进行错误日志记录和报告。 应用程序*web.config*文件中的 `customErrors` 元素指定错误页：

[!code-xml[Main](web-config-transformations/samples/sample2.xml)]

若要查看错误页，请暂时将 `customErrors` 元素的 `mode` 属性从 "RemoteOnly" 更改为 "打开"，并从 Visual Studio 运行该应用程序。 请求无效的 URL （如*Studentsxxx*）会导致错误。 您将看到*GenericErrorPage*页，而不是 IIS 生成的 "找不到资源" 错误页。

![错误页](web-config-transformations/_static/image2.png)

若要查看错误日志，请将 URL 中的所有内容替换为*elmah. axd*的端口号（例如 `http://localhost:51130/elmah.axd`），然后按 enter：

![ELMAH 页面](web-config-transformations/_static/image3.png)

完成后，不要忘记将 `customErrors` 元素设置回 "RemoteOnly" 模式。

在您的开发计算机上，可以方便地访问错误日志页，但在生产环境中，这会带来安全风险。 对于生产站点，你希望添加一个限制对管理员的错误日志访问的授权规则，并确保你还需要将此限制用于测试和过渡。 因此，这是你想要在每次部署发布版本时实现的另一项更改，因此它属于*web.config*文件。

打开*web.config*并在关闭 `configuration` 标记之前添加新的 `location` 元素，如下所示。

[!code-xml[Main](web-config-transformations/samples/sample3.xml?highlight=27-34)]

"Insert" `Transform` 特性值导致将此 `location` 元素添加为*web.config*文件中任何现有 `location` 元素的同级元素。 （已经有一个 `location` 元素指定了**更新信用额度**页面的授权规则。）

现在可以预览转换，确保正确编码。

在**解决方案资源管理器**中，右键单击 " *web.config* " 并单击 "**预览转换**"。

![预览转换菜单](web-config-transformations/_static/image4.png)

此时将打开一个页面，其中显示了左侧*的开发 web.config*文件，并突出显示了所部署的*web.config*文件。

![调试转换预览](web-config-transformations/_static/image5.png)

![位置转换预览](web-config-transformations/_static/image6.png)

（在预览版中，你可能会注意到一些你没有编写转换的其他更改：这通常涉及到删除不影响功能的空白。）

部署后测试站点时，还需进行测试，以验证授权规则是否有效。

> [!NOTE] 
> 
> **安全说明**切勿在生产应用程序中向公众显示错误详细信息，或者将该信息存储在公共位置。 攻击者可以使用错误信息发现站点中的漏洞。 如果在自己的应用程序中使用 ELMAH，请配置 ELMAH 以将安全风险降至最低。 本教程中的 ELMAH 示例不应被视为建议的配置。 这是一个示例，它是为了说明如何处理应用程序必须能够在其中创建文件的文件夹。 有关详细信息，请参阅[保护 ELMAH 终结点](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)。

## <a name="a-setting-that-youll-handle-in-publish-profile-transformation-files"></a>你将在发布配置文件转换文件中处理的设置

常见的情况是，在你部署到的每个环境中必须有不同的*web.config 文件设置。* 例如，调用 WCF 服务的应用程序可能需要在测试环境和生产环境中使用不同的终结点。 Contoso 大学应用程序还包括此类型的设置。 此设置控制站点页面上的可见指示器，该指示器告诉你处于哪个环境（例如开发、测试或生产）。 设置值确定应用程序是将 "（Dev）" 还是 "（Test）" 追加到站点的主标题上 *。母版页*母版页：

![环境指示器](web-config-transformations/_static/image7.png)

当应用程序在过渡或生产环境中运行时，将省略环境指示器。

Contoso 大学网页读取在*web.config 文件 `appSettings`* 中设置的值，以确定应用程序运行的环境：

[!code-xml[Main](web-config-transformations/samples/sample4.xml)]

在测试环境中，该值应为 "Test"，过渡和生产的值应为 "生产"。

转换文件中的以下代码将实现此转换：

[!code-xml[Main](web-config-transformations/samples/sample5.xml)]

`xdt:Transform` 属性值 "SetAttributes" 指示此转换的目的是更改*web.config 文件中*现有元素的属性值。 `xdt:Locator` 属性值 "Match （key）" 指示要修改的元素是其 `key` 属性与此处指定的 `key` 属性匹配的元素。 `add` 元素的唯一其他属性 `value`，这就是在部署的*web.config*文件中将更改的内容。 此处显示的代码导致在*部署的 web.config 文件中*将 `Environment` `appSettings` 元素的 `value` 属性设置为 "Test"。

此转换属于尚未创建的发布配置文件转换文件。 在为测试、过渡和生产环境创建发布配置文件时，你将创建和更新实现此更改的转换文件。 你将在 "[部署到 IIS](deploying-to-iis.md) " 和 "[部署到生产](deploying-to-production.md)" 教程中执行此操作。

> [!NOTE]
> 由于此设置位于 `<appSettings>` 元素中，因此，你可以使用另一种方法在部署到 Web 应用时指定转换 Azure App Service 请参阅本主题前面的在[Azure 中指定 web.config 设置](#watransforms)。

## <a name="setting-connection-strings"></a>设置连接字符串

尽管默认转换文件包含演示如何更新连接字符串的示例，但在大多数情况下，你不需要设置连接字符串转换，因为你可以在发布配置文件中指定连接字符串。 你将在 "[部署到 IIS](deploying-to-iis.md) " 和 "[部署到生产](deploying-to-production.md)" 教程中执行此操作。

## <a name="summary"></a>摘要

在创建发布配置文件之前，你已完成*了与 web.config 转换相同*的操作，并且已查看部署的 web.config 文件中将包含的内容的预览。

![位置转换预览](web-config-transformations/_static/image8.png)

在以下教程中，你将负责执行需要设置项目属性的部署设置任务。

## <a name="more-information"></a>详细信息

有关本教程涵盖的主题的详细信息，请参阅在 Visual Studio 和 ASP.NET 的 Web 部署内容映射中的[部署过程中，使用 web.config 转换更改目标 web.config 文件或 app.config 文件中的设置](https://go.microsoft.com/fwlink/p/?LinkId=282413#transforms)。

> [!div class="step-by-step"]
> [上一页](preparing-databases.md)
> [下一页](project-properties.md)
