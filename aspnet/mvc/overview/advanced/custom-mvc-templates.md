---
uid: mvc/overview/advanced/custom-mvc-templates
title: 自定义 MVC 模板 |Microsoft Docs
author: joeloff
description: 创建一个模板作为 VSIX 扩展。
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499598"
---
# <a name="custom-mvc-template"></a>自定义 MVC 模板

作者： [Jacques Eloff](https://github.com/joeloff)

版本的 MVC 3 Tools Update for Visual Studio 2010 为 MVC 项目引入了单独的项目向导。 更改由两个因素驱动。 首先，在 MVC 3 中引入了新模板，并支持 Razor 等其他视图引擎，从而 overcrowding Visual Studio 中的 "新建项目" 对话框。 其次，客户一直在寻求扩展点，而新的 MVC 项目向导将为我们提供响应这些请求的机会。

添加自定义模板是一个棘手进程，它依赖于使用注册表使新模板对 MVC 项目向导可见。 新模板的作者必须将其包装在 MSI 内，以确保在安装时创建必要的注册表项。 替代方法是生成包含模板的 ZIP 文件，并让最终用户手动创建所需的注册表项。

上述两种方法都不是理想之选，因此我们决定利用[VSIX](https://msdn.microsoft.com/library/ff363239.aspx)扩展提供的一些现有基础结构，以便更轻松地创作、分发和安装自定义 mvc 模板（从针对 Visual Studio 2012 的 mvc 4 开始）。 此方法提供的一些优点包括：

- VSIX 扩展可以包含多个支持不同语言（C#和 Visual Basic）和多个视图引擎（ASPX 和 Razor）的模板。
- VSIX 扩展可以面向 Visual Studio 的多个 Sku，包括 Express Sku。
- [Visual Studio 库](https://visualstudiogallery.msdn.microsoft.com/)有助于将扩展分发给广大受众。
- 可以升级 VSIX 扩展，使你可以更轻松地为自定义模板创作更正和更新。

## <a name="prerequisites"></a>系统必备

- 用户需要熟悉创作项目模板，包括必要的 .vstemplate 文件标记，等等。
- 用户需要安装 Visual Studio Professional 和更高版本。 Express Sku 不支持创建 VSIX 项目。
- 已安装[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) 。

## <a name="example"></a>示例

第一步是使用C#或 Visual Basic 创建新的 VSIX 项目。 选择 "**文件" > "新建项目**"，然后单击左窗格中的 "**扩展性**"，然后选择 " **VSIX 项目**"。

![新建项目](custom-mvc-templates/_static/image1.jpg)

创建项目后，将打开 VSIX 设计器。

![项目设计器元数据](custom-mvc-templates/_static/image2.jpg)

设计器可用于编辑扩展的一些常规属性，这些属性将在用户安装扩展时向用户显示，或在 Visual Studio 中浏览已安装的扩展（**工具 > 扩展和更新**）。 完成常规信息后，请单击 "**安装目标" 选项卡**。

![项目设计器安装目标](custom-mvc-templates/_static/image3.jpg)

此选项卡用于指定你的扩展所支持的 Visual Studio 的 Sku 和版本。 选中 "为**所有用户安装此 VSIX**的复选框，以启用 vsix 的每计算机安装"。 单击右侧的 "**新建**" 按钮以添加其他 sku，如 Web Developer EXPRESS （VWD）。

![添加新的安装目标](custom-mvc-templates/_static/image4.jpg)

如果你打算支持所有专业版和更高版本的 Sku （专业版、高级版和旗舰版），只需在家族**Microsoft.VisualStudio.Pro**中选择最低 SKU。 完成安装目标后，请记得保存所有更改。

![项目设计器安装目标](custom-mvc-templates/_static/image5.jpg)

"**资产**" 选项卡用于将所有内容文件添加到 VSIX 中。 由于 MVC 需要自定义元数据，你将编辑 VSIX 清单文件的原始 XML，而不是使用 "**资产**" 选项卡来添加内容。 首先将模板内容添加到 VSIX 项目。 重要的是，文件夹的结构和内容反映了项目的布局。 下面的示例包含四个派生自基本 MVC 项目模板的项目模板。 确保将包含项目模板的所有文件（ProjectTemplates 文件夹下的所有文件）添加到 VSIX 项目文件的**Content** itemgroup 中，并确保每个项包含**CopyToOutputDirectory**和**IncludeInVsix**元数据集，如以下示例中所示。

&lt;Content Include =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;

&lt;CopyToOutputDirectory&gt;始终&lt;/CopyToOutputDirectory&gt;

&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;

&lt;/Content&gt;

如果不是，则 IDE 将在生成 VSIX 时尝试编译模板的内容，并且可能会看到错误。 模板中的代码文件通常包含 Visual Studio 在实例化项目模板时使用的特殊[模板参数](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx)，因此无法在 IDE 中进行编译。

![“解决方案资源管理器”](custom-mvc-templates/_static/image6.jpg)

关闭 VSIX 设计器，然后在**解决方案资源管理器**中右键单击**源文件**，然后选择 "**打开方式**" 并选择 " **XML （文本）编辑器**" 选项。

![打开方式对话框](custom-mvc-templates/_static/image7.jpg)

&gt;元素创建 **&lt;资产**，并为必须包括在 VSIX 中的每个文件添加 **&lt;资产&gt;** 元素。 每个 **&lt;资产&gt;** 元素的**Type**属性必须设置为**VisualStudio**。 这是只有 MVC 项目向导理解的自定义命名空间。 有关清单文件的结构和布局的其他信息，请参阅 VSIX 2.0 架构文档。

只需将文件添加到 VSIX，就不能用 MVC 向导注册模板。 你需要向 MVC 向导提供信息，如模板名称、说明、支持的视图引擎和编程语言。 此信息在与每个 **.vstemplate**文件 **&lt;资产&gt;** 元素关联的自定义属性中执行。

&lt;资产 d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;

键入 =&quot;VisualStudio&quot;

d:Source =&quot;文件&quot;

路径 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;

ProjectType =&quot;MVC&quot;

Language =&quot;C#&quot;

ViewEngine =&quot;Aspx&quot;

TemplateId =&quot;MyMvcApplication&quot;

标题 =&quot;自定义基本 Web 应用程序&quot;

Description =&quot;从基本 MVC web 应用程序（Razor）派生的自定义模板&quot;

版本 =&quot;4.0&quot;/&gt;

下面是必须存在的自定义属性的说明：

- **ProjectType**必须设置为 MVC。
- **Language**指定模板支持的开发语言。 有效值为C#或 VB。
- **ViewEngine**指定模板支持的视图引擎，如 Aspx 或 Razor。 您可以为此字段指定自定义值。
- **TemplateId**用于将模板分组。 如果该值与现有的模板 ID 相匹配，则它将替代以前使用 MVC 向导注册的模板。
- **Title**指定在每个项目模板下的 MVC 向导中显示的简短说明。
- **Description**指定模板的更详细说明。

将所有文件添加到清单并保存后，你会注意到，设计器中的 "**资产**" 选项卡将显示所有文件，而不是添加到 " **&lt;资产**" 的自定义属性&gt; **.vstemplate**文件的元素。

![项目设计器资产](custom-mvc-templates/_static/image8.jpg)

现在剩下的就是编译并安装 VSIX 项目。

请确保 Visual Studio 的所有实例在要测试 VSIX 扩展的计算机上关闭。 Visual Studio 将在启动过程中扫描新扩展，因此，如果在安装 VSIX 时 IDE 处于打开状态，则需要重启 Visual Studio。 在 "资源管理器" 中，双击 VSIX 文件以启动**Vsix 安装程序**，单击 "**安装**"，并启动 Visual Studio。

![VSIX 安装程序](custom-mvc-templates/_static/image9.jpg)

从菜单中选择 "**工具" > "扩展和更新**" 以确认你的扩展已安装。 如果在安装扩展期间，VSIX 安装程序报告了任何错误，则可以查看 VSIX 安装程序日志以获取详细信息。 通常会在安装了扩展的用户的 **% temp%** 文件夹中创建日志，例如**C:\Users\Bob\AppData\Local\Temp**。

![扩展和更新](custom-mvc-templates/_static/image10.jpg)

关闭窗口后，可以创建 MVC 4 项目，以查看新模板是否显示在 MVC 向导中。

![新的 ASP.NET MVC 4 项目](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a>限制

1. MVC 向导不支持本地化的自定义模板。
2. 如果向导找不到自定义模板，则不会报告任何错误。 如果缺少任何必需的自定义属性，该模板将直接从向导中排除。
