---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
title: 了解 ASP.NET AJAX 本地化 |Microsoft Docs
author: scottcate
description: 本地化是设计特定语言和区域性并将其集成到应用程序或应用程序组件的支持的过程。 Mic 。
ms.author: riande
ms.date: 03/14/2008
ms.assetid: c1a35f18-bab9-41f7-8497-15530c37a09d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-localization
msc.type: authoredcontent
ms.openlocfilehash: 003e7939accd7a68dab97441b3d999bca835b85a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456626"
---
# <a name="understanding-aspnet-ajax-localization"></a>了解 ASP.NET AJAX 本地化

作者： [Scott Cate](https://github.com/scottcate)

[下载 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial04_Localization_cs.pdf)

> 本地化是设计特定语言和区域性并将其集成到应用程序或应用程序组件的支持的过程。 通过集成标准 .NET 本地化模型，Microsoft ASP.NET 平台为标准 ASP.NET 应用程序的本地化提供了广泛的支持;Microsoft AJAX Framework 利用集成模式来支持可执行本地化的各种方案。

## <a name="introduction"></a>简介

Microsoft 的 ASP.NET 技术引入了面向对象的和事件驱动的编程模型，并将其与编译的代码的优势结合起来。 但是，它的服务器端处理模型在技术方面有一些固有的缺点，其中许多功能都可以通过 System.web 命名空间中包含的新功能来解决，后者在 .NET Framework3.5。 这些扩展启用了许多丰富的客户端功能，以前作为 ASP.NET 2.0 AJAX 扩展的一部分提供，但现在是框架基类库的一部分。 此命名空间中的控件和功能包括页面的部分呈现，无需整页刷新、通过客户端脚本访问 Web 服务的能力（包括 ASP.NET 分析 API）以及用于镜像许多在 ASP.NET 服务器端控件集中显示的控件方案。

本白皮书介绍了 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库中存在的本地化功能，其中包含本地化支持的业务需求和对 web 中本地化的已集成支持.NET Framework 提供的应用程序。 Microsoft AJAX 脚本库利用了 .NET 应用程序已使用的 .resx 文件格式，该格式提供集成的 IDE 支持和可共享的资源类型。

本白皮书基于 Microsoft Visual Studio 2008 的 Beta 2 版本。 本白皮书还假设你将使用 Visual Studio 2008，而不是 Visual Web Developer Express，并将根据 Visual Studio 的用户界面提供演练。 一些代码示例将利用在 Visual Web Developer 速成版中可能不可用的项目模板。

## <a name="the-need-for-localization"></a>*本地化需要*

特别是对于企业应用程序开发人员和组件开发人员而言，创建可了解区域性与语言差异的工具的功能已变得越来越重要。 设计可适应客户端区域设置的组件可以提高开发人员的工作效率，并减少调整组件全局运行所需的工作量。

本地化是设计特定语言和区域性并将其集成到应用程序或应用程序组件的支持的过程。 通过集成标准 .NET 本地化模型，Microsoft ASP.NET 平台为标准 ASP.NET 应用程序的本地化提供了广泛的支持;Microsoft AJAX Framework 利用集成模式来支持可执行本地化的各种方案。 使用 Microsoft AJAX Framework，可以通过将脚本部署到附属程序集或利用静态文件系统结构来对脚本进行本地化。

## <a name="embedding-scripts-with-satellite-assemblies"></a>*将脚本嵌入附属程序集*

与标准 .NET Framework 本地化策略一致，资源可以包括在附属程序集中。 与二进制文件中的传统资源包含相比，附属程序集具有多项优势-任何指定的本地化都可以更新，而无需更新较大的映像，只需将附属程序集安装到项目文件夹和附属程序集均可部署，而不会导致主项目程序集重新加载。 特别是在 ASP.NET 项目中，这是很有用的，因为它可以显著减少增量更新所使用的系统资源量，并最大限度地降低生产网站的使用。

脚本嵌入到程序集中，方法是将它们包含在托管的 .resx （或编译的 .resources）文件中，这些文件将在编译时包含在程序集中。 然后通过程序集级别的属性，将其资源通过 AJAX 运行时生成的代码提供给脚本应用程序。

*嵌入的脚本文件的命名约定*

Microsoft AJAX Framework 脚本管理支持用于在部署和测试脚本时使用的各种选项，并且提供了有助于这些选项的指导原则。

*为了便于调试：*

Release （生产）脚本不应在文件名中包含 `.debug` 限定符。 为调试而设计的脚本应在文件名中包含 `.debug`。

*为简化本地化：*

非特定区域性脚本不应在文件的名称中包含任何区域性标识符。 对于包含本地化资源的脚本，应在文件名中指定 ISO 语言代码。 例如，`es-CO` 代表西班牙语，哥伦比亚。

下表总结了包含示例的文件命名约定：

| Filename | 含义 |
| --- | --- |
| Script.js | 非特定于版本区域性的脚本。 |
| Script.debug.js | 调试版本非特定于区域性的脚本。 |
| Script.en-US.js | 版本英语美国脚本。 |
| Script.debug.es-CO.js | Debug 版本西班牙语，哥伦比亚脚本。 |

## <a name="walkthrough-create-an-localized-embedded-script"></a>演练：创建本地化的嵌入脚本

*请注意：此演练要求使用 Visual Studio 2008，因为 Visual Web Developer Express 不包含用于类库项目的项目模板。*

1. 使用集成的 ASP.NET AJAX Extension 创建新的网站项目。 在名为 LocalizingResources 的解决方案中创建另一个项目（一个类库项目）。
2. 将名为 VerifyDeletion 的 Jscript 文件添加到 LocalizingResources 项目，并添加名为 DeletionResources 和 DeletionResources 的 .resx 资源文件。 前者包含非特定区域性的资源;后者将包含西班牙语语言资源。
3. 将以下代码添加到 VerifyDeletion：

[!code-javascript[Main](understanding-asp-net-ajax-localization/samples/sample1.js)]

对于使用 JavaScript Regex 语法不熟悉的对象，在单正斜杠中的文本（在上一个示例中，/FILENAME/是一个示例）表示 RegExp 对象。 MSDN Library 包含广泛的 JavaScript 参考，可以联机找到 JavaScript 本机对象上的资源。

1. 向 DeletionResources 添加以下资源字符串： 

    **VerifyDelete**：是否确实要删除文件名？

    **已删除**：已删除文件名。

1. 向 DeletionResources 添加以下资源字符串： 

    **VerifyDelete**： Est seguro 查询 DESEE quitar FILENAME？

    **已删除**： FILENAME se ha quitado。
2. 将以下代码行添加到 AssemblyInfo 文件：

[!code-csharp[Main](understanding-asp-net-ajax-localization/samples/sample2.cs)]

1. 向 LocalizingResources 项目添加对 System.web 和 System.object 的引用。
2. 从网站项目添加对 LocalizingResources 项目的引用。
3. 在 default.aspx 中，在网站项目下，用以下附加标记更新 ScriptManager 控件：

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample3.aspx)]

1. 在页面上的任何位置，在默认情况下，包括以下标记：

[!code-aspx[Main](understanding-asp-net-ajax-localization/samples/sample4.aspx)]

1. 按 F5。 如果系统提示，请启用调试。 加载页面后，按 "删除" 按钮。 请注意，系统会提示你输入英语（除非默认情况下，你的计算机设置为首选西班牙语语言资源）才能确认。
2. 关闭浏览器窗口并返回到 default.aspx。 在 @Page 标头指令中，将 Culture 和 UICulture 的 auto 替换为 es。 再次按 F5 在浏览器中重新启动 web 应用程序。 这一次，请注意，系统会提示删除西班牙语中的文件：

[![](understanding-asp-net-ajax-localization/_static/image2.png)](understanding-asp-net-ajax-localization/_static/image1.png)

（[单击以查看完全大小的映像](understanding-asp-net-ajax-localization/_static/image3.png)）

[![](understanding-asp-net-ajax-localization/_static/image5.png)](understanding-asp-net-ajax-localization/_static/image4.png)

（[单击以查看完全大小的映像](understanding-asp-net-ajax-localization/_static/image6.png)）

请注意，此演练有若干变化形式。 例如，可以在页面加载过程中以编程方式向 ScriptManager 控件注册脚本。

## <a name="including-a-static-script-file-structure"></a>*包括静态脚本文件结构*

使用静态脚本文件进行部署时，会丧失使用固有的 .NET 本地化方案的一些优点。 主要是：你丢失了从包含脚本资源文件生成的自动类型;例如，在上面的演练中，资源已由来自 ScriptManager 控件的名为 Message 的自动生成类型公开。

不过，使用静态脚本文件结构有一些优点。 可以在不重新编译和重新部署附属程序集的情况下执行更新，也可以通过使用静态文件结构来替代嵌入的脚本，从而集成可能未随组件一起提供的一小部分功能。

Microsoft 建议在项目编译期间自动生成脚本资源，以避免版本控制问题。 在维护广泛的脚本代码库时，确保代码更改反映在每个本地化脚本中可能会变得越来越困难。 作为替代方法，只需维护一个逻辑脚本和多个本地化脚本，生成项目时合并文件。

由于没有要以声明方式包含的资源，因此应通过将 `<asp:ScriptElement>` 元素添加为 ScriptManager 控件的 `<Scripts>` 标记的子元素，或通过编程方式将 `ScriptReference` 对象添加到运行时页上的 `ScriptManager` 控件的 `Scripts` 属性来引用静态脚本文件。

## <a name="the-scriptmanager-and-its-role-in-localization"></a>*ScriptManager 及其在本地化中的角色*

ScriptManager 为本地化的应用程序启用了几种自动行为：

- 它基于设置和命名约定自动定位脚本文件;例如，在调试模式下，它加载启用了调试的脚本，并基于浏览器的用户界面选择加载本地化的脚本。
- 它支持区域性的定义，其中包括自定义区域性。
- 它支持通过 HTTP 压缩脚本文件。
- 它缓存脚本以有效地管理多个请求。
- 它通过将其通过加密的 URL 来管道来向脚本添加一个间接层。

可以通过编程方式或声明性标记将脚本引用添加到 ScriptManager 控件。 当处理嵌入在网站项目本身之外的程序集中的脚本时，声明性标记特别有用，因为在通过推送修订时，脚本的名称可能不会更改。

## <a name="summary"></a>摘要

随着 web 应用程序越来越多地增长到更大的受众，需要能够更广泛的文化和社区成为业务模型的核心;电子商务 web 应用程序需要能够处理外国货币，内容管理系统不仅需要能够显示其内容，而且还需要提供其他语言的导航提示和表单字段，并且公司需要知道这种需要方便.

.NET Framework 本质上支持丰富的本地化框架，使用附属程序集和 XML 资源（.resx）文件来提供一种统一的方法来查找资源字符串和图像。 ASP.NET AJAX 扩展（包括 Microsoft AJAX Framework 和 Microsoft AJAX 脚本库）提供了对客户端代码的此编程模型的支持，从而实现了简单的资源字符串查找。 附属程序集支持通过 ScriptResource 自动包含脚本资源（实际的 .js 文件），只要文件名遵循给定的命名方案即可。 通过这种支持，ASP.NET AJAX 扩展简化了脚本本地化和应用程序的全球化。

## <a name="bio"></a>*Bio*

Scott Cate 一直在使用 Microsoft Web 技术，因为1997，是 myKB.com （[www.myKB.com](http://www.myKB.com)）的总裁，他致力于编写基于知识库软件解决方案的基于 ASP.NET 的应用程序。 可以通过电子邮件联系 Scott [scott.cate@myKB.com](mailto:scott.cate@myKB.com)或[ScottCate.com](http://ScottCate.com)上的博客

> [!div class="step-by-step"]
> [上一页](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
> [下一页](understanding-asp-net-ajax-web-services.md)
