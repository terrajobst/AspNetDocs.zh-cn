---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
title: 通过 ASP.NET AJAX 了解部分页面更新 |Microsoft Docs
author: scottcate
description: 也许，ASP.NET AJAX 扩展的最明显的功能是能够执行部分或增量页面更新，而无需执行到 t 的完整回发 。
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 54d9df99-1161-4899-b4e8-2679c85915e7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
msc.type: authoredcontent
ms.openlocfilehash: 4b87cb8f58dbd7f27b16bcb0d488ff361770d4fe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439268"
---
# <a name="understanding-partial-page-updates-with-aspnet-ajax"></a>了解使用 ASP.NET AJAX 的部分页面更新

作者： [Scott Cate](https://github.com/scottcate)

[下载 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial01_Partial_Page_Updates_cs.pdf)

> 也许，ASP.NET AJAX Extension 的最明显的功能是能够在不完全回发到服务器的情况下执行部分或增量页面更新，而无需更改代码和最小程度的标记更改。 优点非常多–多媒体的状态（如 Adobe Flash 或 Windows Media）保持不变，带宽成本降低，客户端不会遇到通常与回发关联的闪烁。

## <a name="introduction"></a>简介

Microsoft 的 ASP.NET 技术引入了面向对象的和事件驱动的编程模型，并将其与编译的代码的优势结合起来。 不过，它的服务器端处理模型在技术上有一些固有的缺点：

- 页面更新要求与服务器之间的往返，这需要刷新页面。
- 往返不会保留 Javascript 或其他客户端技术（如 Adobe Flash）生成的任何影响。
- 在回发期间，Microsoft Internet Explorer 以外的浏览器不支持自动还原滚动位置。 甚至在 Internet Explorer 中，在页面刷新时仍会出现闪烁。
- 如果 \_\_VIEWSTATE 窗体字段可能会增长，则回发可能会涉及大量带宽，特别是在处理控件（如 GridView 控件或中继器）时。
- 通过 JavaScript 或其他客户端技术，没有用于访问 Web 服务的统一模型。

输入 Microsoft 的 ASP.NET AJAX 扩展。 AJAX**是指同步** **J** avaScript **a** nd **X** ML，是一种集成框架，可通过跨平台 JavaScript 提供增量页面更新，由包含 microsoft Ajax FRAMEWORK 的服务器端代码和称为 microsoft ajax 脚本库的脚本组件提供。 ASP.NET AJAX 扩展还提供跨平台支持，以便通过 JavaScript 访问 ASP.NET Web 服务。

本白皮书检查 ASP.NET AJAX 扩展的部分页面更新功能，其中包括 ScriptManager 组件、UpdatePanel 控件和 UpdateProgress 控件，并考虑它们应该或不应处于的情况超载.

本白皮书基于 Visual Studio 2008 和 .NET Framework 3.5 的 Beta 2 版本，该版本将 ASP.NET AJAX 扩展集成到基类库中（以前是可用于 ASP.NET 2.0 的附加组件）。 本白皮书还假设你使用的是 Visual Studio 2008，而不是 Visual Web Developer 速成版;引用的某些项目模板可能不适用于 Visual Web Developer Express 用户。

## <a name="partial-page-updates"></a>部分页面更新

也许，ASP.NET AJAX Extension 的最明显的功能是能够在不完全回发到服务器的情况下执行部分或增量页面更新，而无需更改代码和最小程度的标记更改。 优点非常广泛-多媒体的状态（如 Adobe Flash 或 Windows Media）保持不变，带宽成本降低，客户端不会遇到通常与回发关联的闪烁。

集成部分页面呈现的功能集成到了 ASP.NET 中，对项目进行了最少的更改。

## <a name="walkthrough-integrating-partial-rendering-into-an-existing-project"></a>演练：将部分呈现集成到现有项目中

1. 在 Microsoft Visual Studio 2008 中，通过转到 "<em>文件</em><em>-" &gt; 新</em>的<em>-&gt;</em>网站并从对话框中选择 "ASP.NET" 网站来创建新的 ASP.NET 网站项目。 可以将其命名为任何所需内容，并且可以将其安装到文件系统或 Internet Information Services （IIS）中。
2. 将显示具有基本 ASP.NET 标记（服务器端窗体和 `@Page` 指令）的空白默认页。 将名为 `Label1` 的标签和一个名为 `Button1` 的按钮拖到窗体元素中的页上。 可以将其文本属性设置为所需的任何内容。
3. 在设计视图中，双击 "`Button1`" 生成代码隐藏事件处理程序。 在此事件处理程序中，将 `Label1.Text` 设置为单击按钮！ .

**列表1：启用部分呈现之前的默认 .aspx 标记**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample1.aspx)]

**列表2： default.aspx.cs 中的代码隐藏（已剪裁）**

[!code-csharp[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample2.cs)]

1. 按 F5 启动您的网站。 Visual Studio 将提示你添加 web.config 文件以启用调试;执行此操作。 单击该按钮时，请注意，页面会刷新以更改标签中的文本，并且会在页面重绘时出现短暂的闪烁。
2. 关闭浏览器窗口后，返回到 Visual Studio 并返回到标记页。 在 Visual Studio "工具箱" 中向下滚动，找到标记为 "AJAX 扩展" 的选项卡。 （如果你没有此选项卡，因为你使用的是较旧版本的 AJAX 或阿特拉斯扩展，请参阅本白皮书后面的注册 AJAX Extension 工具箱项演练，或安装 Windows Installer 可下载的当前版本从网站中）。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image2.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image1.png)

（[单击以查看完全大小的映像](understanding-partial-page-updates-with-asp-net-ajax/_static/image3.png)）

1. <em>已知问题：</em>如果将 Visual Studio 2008 安装到已安装了具有 ASP.NET 2.0 AJAX 扩展的 Visual Studio 2005 的计算机上，则 Visual Studio 2008 将导入 AJAX Extension 工具箱项。 您可以通过检查组件的工具提示来确定是否是这种情况;它们应该会说版本3.5.0.0。 如果它们使用版本2.0.0.0，则已导入旧的工具箱项，需要使用 Visual Studio 中的 "选择工具箱项" 对话框手动导入它们。 您将无法通过设计器添加版本2控件。

2. 开始 `<asp:Label>` 标记之前，请创建一个空白行，然后双击工具箱中的 UpdatePanel 控件。 请注意，新的 `@Register` 指令包含在页面顶部，指示应使用 `asp:` 前缀导入 System.web 命名空间中的控件。
3. 拖动结束标记元素末尾的结束 `</asp:UpdatePanel>` 标记，使元素的格式正确，并将标记和按钮控件换行。
4. 开始 `<asp:UpdatePanel>` 标记后，开始打开新标记。 请注意，IntelliSense 会提示你提供两个选项。 在这种情况下，请创建 `<ContentTemplate>` 标记。 请确保将此标记环绕在标签和按钮上，使标记格式正确。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image5.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image4.png)

（[单击以查看完全大小的映像](understanding-partial-page-updates-with-asp-net-ajax/_static/image6.png)）

1. 在 `<form>` 元素中的任意位置，通过双击工具箱中的 "`ScriptManager`" 项来包含 ScriptManager 控件。
2. 编辑 `<asp:ScriptManager>` 标记，使其包含特性 `EnablePartialRendering= true`。

**列表3：启用了部分呈现的默认 .aspx 标记**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample3.aspx)]

1. 打开 web.config 文件。 请注意，Visual Studio 已自动添加对 System.web 的编译引用。

1. Visual Studio 2008 中的新增功能： ASP.NET 网站项目模板附带的 web.config 会自动包含对 ASP.NET AJAX 扩展的所有必要引用，并包含配置信息的注释部分，这些信息可以取消注释以启用其他功能。 安装 ASP.NET 2.0 AJAX 扩展时，Visual Studio 2005 具有类似的模板。 但是，在 Visual Studio 2008 中，默认情况下将选择退出 AJAX 扩展（即，默认情况下将引用它们，但可以将其作为引用删除）。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image8.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image7.png)

（[单击以查看完全大小的映像](understanding-partial-page-updates-with-asp-net-ajax/_static/image9.png)）

1. 按 F5 启动你的网站。 请注意，不需要更改源代码即可支持仅限部分呈现的标记。

当你启动网站时，你应该会看到部分呈现已启用，因为当你单击按钮时，不会出现闪烁，页面滚动位置中也不会有任何变化（此示例不演示）。 如果在单击按钮后查看页面的呈现源，它将确认是否确实发生了回发，因为原始标签文本仍是源标记的一部分，并且标签已通过 JavaScript 更改。

Visual Studio 2008 似乎不带有预定义的模板，适用于启用 AJAX ASP.NET 的网站。 但是，如果安装了 Visual Studio 2005 和 ASP.NET 2.0 AJAX 扩展，则此类模板在 Visual Studio 2005 中提供。 因此，配置网站并从启用 AJAX 的网站模板开始可能会更容易，因为模板应包含完全配置的 web.config 文件（支持所有 ASP.NET AJAX 扩展，包括 Web 服务访问权限）和 JSON 序列化 JavaScript 对象表示法），并且默认情况下在主 Web 窗体页中包含一个 UpdatePanel 和 System.windows.controls.contentcontrol.contenttemplate。 通过此默认页启用部分呈现只是与重新获得本演练中的步骤10和将控件放到页面上一样简单。

## <a name="the-scriptmanager-control"></a>ScriptManager 控件

## <a name="scriptmanager-control-reference"></a>ScriptManager 控件引用

启用标记的属性：

| **属性名称** | **Type** | **描述** |
| --- | --- | --- |
| AllowCustomErrors-Redirect | Bool | 指定是否使用 web.config 文件的自定义错误部分来处理错误。 |
| AsyncPostBackError-Message | String | 获取或设置在引发错误时发送给客户端的错误消息。 |
| AsyncPostBack-Timeout | Int32 | 获取或设置客户端应等待异步请求完成的默认时间量。 |
| EnableScript-Globalization | Bool | 获取或设置是否启用脚本全球化。 |
| EnableScript-Localization | Bool | 获取或设置是否启用脚本本地化。 |
| ScriptLoadTimeout | Int32 | 确定允许将脚本加载到客户端的秒数 |
| ScriptMode | Enum （自动、调试、发布、继承） | 获取或设置是否呈现脚本的发布版本 |
| ScriptPath | String | 获取或设置指向要发送到客户端的脚本文件的位置的根路径。 |

仅限代码的属性：

| **属性名称** | **Type** | **描述** |
| --- | --- | --- |
| AuthenticationService | AuthenticationService-Manager | 获取有关将发送到客户端的 ASP.NET Authentication 服务代理的详细信息。 |
| IsDebuggingEnabled | Bool | 获取是否启用脚本和代码调试。 |
| IsInAsyncPostback | Bool | 获取页面当前是否处于异步回发请求。 |
| ProfileService | ProfileService-Manager | 获取有关将发送到客户端的 ASP.NET 分析服务代理的详细信息。 |
| 脚本 | &lt;脚本引用的集合&gt; | 获取将发送到客户端的脚本引用的集合。 |
| 服务 | 集合&lt;服务引用&gt; | 获取将发送到客户端的 Web 服务代理引用的集合。 |
| SupportsPartialRendering | Bool | 获取当前客户端是否支持部分呈现。 如果此属性返回**false**，则所有页面请求均为标准回发。 |

公共代码方法：

| **方法名称** | **Type** | **描述** |
| --- | --- | --- |
| SetFocus(string) | Void | 当请求完成时，将客户端的焦点设置到特定控件。 |

标记后代：

| **标记** | **描述** |
| --- | --- |
| &lt;AuthenticationService&gt; | 提供有关 ASP.NET authentication 服务的代理的详细信息。 |
| &lt;ProfileService&gt; | 提供有关 ASP.NET 分析服务代理的详细信息。 |
| &lt;脚本&gt; | 提供其他脚本引用。 |
| &lt;asp： ScriptReference&gt; | 表示特定的脚本引用。 |
| &lt;服务&gt; | 提供将生成代理类的其他 Web 服务引用。 |
| &lt;asp： ServiceReference&gt; | 表示特定的 Web 服务引用。 |

ScriptManager 控件是 ASP.NET AJAX 扩展的基本核心。 它提供对脚本库（包括广泛的客户端脚本类型系统）的访问权限，支持部分呈现，并为其他 ASP.NET 服务（例如身份验证和分析，以及其他 Web 服务）提供广泛支持。 ScriptManager 控件还提供客户端脚本的全球化和本地化支持。

## <a name="providing-alternative-and-supplemental-scripts"></a>提供备用和补充脚本

尽管 Microsoft ASP.NET 2.0 AJAX 扩展包含调试版和发布版中的整个脚本代码（作为嵌入到引用程序集中的资源），但开发人员可随意将 ScriptManager 重定向到自定义脚本文件，并注册其他必需的脚本。

若要覆盖通常包含的脚本（如支持 WebForms 命名空间和自定义类型系统的脚本）的默认绑定，可以注册 ScriptManager 类的 `ResolveScriptReference` 事件。 调用此方法时，事件处理程序有机会更改相关脚本文件的路径;然后，脚本管理器将不同或自定义的脚本副本发送到客户端。

此外，脚本引用（由 `ScriptReference` 类表示）可以通过编程方式或通过标记进行包含。 为此，可以通过编程方式修改 `ScriptManager.Scripts` 集合，或在 `<Scripts>` 标记下包含 `<asp:ScriptReference>` 标记，该标记是 ScriptManager 控件的一级子控件。

## <a name="custom-error-handling-for-updatepanels"></a>针对 UpdatePanels 的自定义错误处理

尽管更新由 UpdatePanel 控件指定的触发器处理，但对错误处理和自定义错误消息的支持由页面的 ScriptManager 控件实例处理。 这是通过向页面公开事件 `AsyncPostBackError`来完成的，该事件可提供自定义异常处理逻辑。

通过使用 AsyncPostBackError 事件，您可以指定 `AsyncPostBackErrorMessage` 属性，该属性随后会在回调完成后引发一个警报框。

还可以使用客户端自定义，而不是使用默认警报框;例如，你可能想要显示自定义的 `<div>` 元素，而不是默认浏览器模式对话框。 在这种情况下，可以处理客户端脚本中的错误：

**列表5：用于显示自定义错误的客户端脚本**

[!code-html[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample4.html)]

简单地说，以上脚本在完成异步请求后，会向客户端 AJAX 运行时注册回调。 然后，它会检查是否报告了错误，如果是，则会处理它的详细信息，最后指示运行时在自定义脚本中处理错误。

## <a name="globalization-and-localization-support"></a>全球化和本地化支持

ScriptManager 控件为脚本字符串和用户界面组件的本地化提供了广泛的支持;但是，该主题超出了本白皮书的讨论范围。 有关详细信息，请参阅白皮书： ASP.NET AJAX Extensions 中的全球化支持。

## <a name="the-updatepanel-control"></a>UpdatePanel 控件

## <a name="updatepanel-control-reference"></a>UpdatePanel 控件引用

启用标记的属性：

| **属性名称** | **Type** | **描述** |
| --- | --- | --- |
| ChildrenAsTriggers | bool | 指定子控件在回发时是否自动调用刷新。 |
| RenderMode | enum （块，内联） | 指定内容的直观显示方式。 |
| UpdateMode | enum （Always，条件） | 指定 UpdatePanel 是否始终在部分呈现期间刷新，或是否仅在命中触发器时刷新。 |

仅限代码的属性：

| **属性名称** | **Type** | **描述** |
| --- | --- | --- |
| IsInPartialRendering | bool | 获取 UpdatePanel 是否支持当前请求的部分呈现。 |
| ContentTemplate | ITemplate | 获取更新请求的标记模板。 |
| ContentTemplateContainer | 控件 | 获取更新请求的编程模板。 |
| 触发器 | UpdatePanel- TriggerCollection | 获取与当前 UpdatePanel 关联的触发器的列表。 |

公共代码方法：

| **方法名称** | **Type** | **描述** |
| --- | --- | --- |
| Update （） | Void | 以编程方式更新指定的 UpdatePanel。 允许服务器请求触发存 UpdatePanel 的部分呈现。 |

标记后代：

| **标记** | **描述** |
| --- | --- |
| &lt;System.windows.controls.contentcontrol.contenttemplate&gt; | 指定要用于呈现部分呈现结果的标记。 &lt;asp： UpdatePanel&gt;的子项。 |
| &lt;触发器&gt; | 指定与更新此 UpdatePanel 关联的*n*个控件的集合。 &lt;asp： UpdatePanel&gt;的子项。 |
| &lt;asp： AsyncPostBackTrigger&gt; | 指定一个触发器，该触发器调用给定 UpdatePanel 的部分页面呈现。 这可能是一个控件，也可能不是相关 UpdatePanel 的后代。 精确到事件名称。&gt;&lt;触发器的子项。 |
| &lt;asp： PostBackTrigger&gt; | 指定使整个页面刷新的控件。 这可能是一个控件，也可能不是相关 UpdatePanel 的后代。 精确到对象。 &gt;&lt;触发器的子项。 |

`UpdatePanel` 控件是指分隔将参与 AJAX 扩展的部分呈现功能的服务器端内容的控件。 页面上可包含的 UpdatePanel 控件数没有限制，可以嵌套。 每个 UpdatePanel 都是独立的，因此每个 UpdatePanel 都可以独立工作（可以同时运行两个 UpdatePanels，从而呈现页面的不同部分，而不受页面的回发的影响）。

UpdatePanel 控件主要用于处理控件触发器-默认情况下，将创建回发的 UpdatePanel `ContentTemplate` 中包含的任何控件注册为 UpdatePanel 的触发器。 这意味着，UpdatePanel 可以使用用户控件来处理默认数据绑定控件（如 GridView），并可以在脚本中对其进行编程。

默认情况下，当触发部分页面呈现时，将刷新页面上的所有 UpdatePanel 控件，无论 UpdatePanel 控件是否为此类操作定义了触发器。 例如，如果一个 UpdatePanel 定义了一个按钮控件并且单击了该按钮控件，则默认情况下，该页面上的所有 UpdatePanel 控件都将刷新。 这是因为，默认情况下，UpdatePanel 的 `UpdateMode` 属性设置为 `Always`。 或者，你可以将 UpdateMode 属性设置为 `Conditional`，这意味着仅当命中特定触发器时才会刷新 UpdatePanel。

## <a name="custom-control-notes"></a>自定义控件注释

可以向任何用户控件或自定义控件添加 UpdatePanel;但是，包含这些控件的页面还必须包含属性 EnablePartialRendering 设置为**true**的 ScriptManager 控件。

在使用 Web 自定义控件时，您可以使用此方法来替代 `CompositeControl` 类的受保护的 `CreateChildControls()` 方法。 这样，如果确定页面支持部分呈现，则可以在控件的子控件与外部世界之间注入 UpdatePanel;否则，只需将子控件分层到容器 `Control` 实例即可。

## <a name="updatepanel-considerations"></a>UpdatePanel 注意事项

UpdatePanel 在 JavaScript XMLHttpRequest 的上下文中以黑框 ASP.NET 的方式运行。 但是，在行为和速度方面，需要牢记重要的性能注意事项。 若要理解 UpdatePanel 的工作方式，以便您可以最好地决定何时使用合适的方法，应检查 AJAX exchange。 下面的示例使用现有站点，并使用 Firebug 扩展（Firebug 捕获 XMLHttpRequest 数据）的 Mozilla Firefox。

请考虑这样一种形式，其中的窗体中的邮政编码为 "邮政编码" 文本框，该文本框应填充窗体或控件上的 city 和 state 字段。 此窗体最终收集成员身份信息，其中包括用户的姓名、地址和联系人信息。 根据特定项目的要求，需要考虑多个设计注意事项。

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image11.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image10.png)

（[单击以查看完全大小的映像](understanding-partial-page-updates-with-asp-net-ajax/_static/image12.png)）

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image14.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image13.png)

（[单击以查看完全大小的映像](understanding-partial-page-updates-with-asp-net-ajax/_static/image15.png)）

在此应用程序的原始迭代中，构建了一个控件，该控件合并了整个用户注册数据，其中包括邮政编码、城市和省/市/自治区。 整个控件被包装在 UpdatePanel 内并拖放到 Web 窗体上。 用户输入邮政编码时，UpdatePanel 会通过指定触发器或使用 ChildrenAsTriggers 属性设置为 true 来检测事件（后端中的相应 TextChanged 事件）。 AJAX 按照 FireBug 捕获的方式发布 UpdatePanel 中的所有字段（请参阅右侧的关系图）。

在屏幕截图指示的情况下，UpdatePanel 中每个控件的值（在本例中为空）和视图状态字段均为空。 发送的所有数据都是通过9kb 发送的，实际上只需要五个字节的数据就能进行此特定请求。 响应更臃肿： total，57kb 将发送到客户端，只是更新文本字段和下拉字段。

还需要了解 ASP.NET AJAX 如何更新演示。 UpdatePanel 更新请求的响应部分显示在左侧的 Firebug 控制台中;它是由客户端脚本拆分并在页面上重新组合在一起的由客户端脚本分割的特殊的、以竖线分隔的字符串。 具体而言，ASP.NET AJAX 设置代表您的 UpdatePanel 的客户端上的 HTML 元素的*innerHTML*属性。 当浏览器重新生成 DOM 时，会稍微延迟，具体取决于需要处理的信息量。

重新生成 DOM 会触发许多其他问题：

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image17.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image16.png)

（[单击以查看完全大小的映像](understanding-partial-page-updates-with-asp-net-ajax/_static/image18.png)）

- 如果焦点 HTML 元素在 UpdatePanel 内，则会失去焦点。 因此，对于按 Tab 键退出 "邮政编码" 文本框的用户，下一个目标是 "城市" 文本框。 但是，当 UpdatePanel 刷新显示后，窗体将不再具有焦点，按 Tab 会开始突出显示焦点元素（如链接）。
- 如果正在使用的任何类型的自定义客户端脚本访问 DOM 元素，则在部分回发后，函数保留的引用可能会失效。

UpdatePanels 不应作为全部捕获解决方案。 相反，它们为某些情况提供快速的解决方案（包括原型设计、小控制更新），并为可能熟悉 .NET 对象模型的开发人员和 DOM 提供熟悉的界面。 有多种方法可以提高性能，具体取决于应用程序方案：

- 请考虑使用 PageMethods 和 JSON （JavaScript 对象表示法）允许开发人员在页面上调用静态方法，就像调用 web 服务调用一样。 由于这些方法是静态的，因此无需状态;脚本调用方提供参数，并以异步方式返回结果。
- 如果需要在应用程序的多个位置使用单个控件，请考虑使用 Web 服务和 JSON。 这又需要很少的特殊工作，并以异步方式运行。

通过 Web 服务或页方法引入功能也有缺点。 首先，ASP.NET 开发人员通常会在用户控件（.ascx 文件）中构建少量的功能组件。 页面方法不能在这些文件中托管;它们必须托管在实际 .aspx 页类中。 同样，Web 服务必须承载于 .asmx 类中。 根据应用程序的不同，此体系结构可能违反了单一责任原则，因为单个组件的功能现在分布在两个或更多物理组件中，这两个或多个物理组件可能几乎不存在或没有任何内聚性。

最后，如果应用程序需要使用 UpdatePanels，请遵循以下准则，以帮助进行故障排除和维护。

- **尽可能少嵌套 UpdatePanels，而不仅是在单位内，还可以跨代码单元嵌套。** 例如，在某个页面上包含一个用于包装控件的 UpdatePanel，而该控件还包含一个 UpdatePanel，其中包含另一个包含 UpdatePanel 的控件，它是跨单元嵌套。 这可以帮助你清楚地了解哪些元素应该刷新，并防止意外刷新到子 UpdatePanels。
- **将*ChildrenAsTriggers*属性设置为 false，并显式设置触发事件。** 利用 `<Triggers>` 集合是处理事件的更清晰的方式，可能会阻止意外行为，从而帮助维护任务和强制开发人员选择加入事件。
- **使用最小的可能单位来实现功能。** 如邮政编码服务的讨论中所述，仅将最小值仅放在服务器上、总处理时间和客户端-服务器交换的占用量上，从而提高性能。

## <a name="the-updateprogress-control"></a>UpdateProgress 控件

## <a name="updateprogress-control-reference"></a>UpdateProgress 控件引用

启用标记的属性：

| **属性名称** | **Type** | **描述** |
| --- | --- | --- |
| AssociatedUpdate-PanelID | String | 指定此 UpdateProgress 应报告的 UpdatePanel 的 ID。 |
| DisplayAfter | Int | 指定在异步请求开始后显示此控件之前的超时时间（以毫秒为单位）。 |
| DynamicLayout | bool | 指定是否动态呈现进度。 |

标记后代：

| **标记** | **描述** |
| --- | --- |
| &lt;ProgressTemplate&gt; | 包含将与此控件一起显示的内容的控件模板集。 |

UpdateProgress 控件提供了一种反馈措施，可以在执行传输到服务器所需的工作时，使用户保持兴趣。 这可以帮助您的用户了解您正在执行的操作，尽管它可能并不明显，尤其是因为大多数用户都使用页面刷新并查看状态栏突出显示。

请注意，UpdateProgress 控件可以出现在页层次结构上的任何位置。 但是，在从子 UpdatePanel （其中，UpdatePanel 嵌套在另一个 UpdatePanel 内）启动部分回发的情况下，触发子 UpdatePanel 的回发将导致为子项显示 UpdateProgress 模板UpdatePanel 以及父 UpdatePanel。 但如果触发器是父级 UpdatePanel 的直接子级，则只会显示与父级关联的 UpdateProgress 模板。

## <a name="summary"></a>摘要

Microsoft ASP.NET AJAX 扩展是一种复杂的产品，旨在帮助使 web 内容更易于访问，并为 web 应用程序提供更丰富的用户体验。 作为 ASP.NET AJAX 扩展的一部分，部分页面呈现控件（包括 ScriptManager、UpdatePanel 和 UpdateProgress 控件）是该工具包的一些最明显的组件。

ScriptManager 组件集成了用于扩展的客户端 JavaScript 的设置，并使各种服务器和客户端组件与最小开发投资一起工作。

UpdatePanel 控件是 UpdatePanel 中外观较强的标记，它可以包含服务器端代码隐藏，而不会触发页面刷新。 UpdatePanel 控件可以嵌套，并可依赖于其他 UpdatePanels 中的控件。 默认情况下，UpdatePanels 处理由其后代控件调用的任何回发，不过，可以通过声明方式或编程方式对此功能进行微调。

使用 UpdatePanel 控件时，开发人员应该知道可能会发生的性能影响。 可能的替代项包括 web 服务和页面方法，但应考虑应用程序的设计。

UpdateProgress 控件使用户可以知道，她或他不会被忽略，并且在页面不会执行任何响应用户输入的情况下，后台请求将继续进行。 它还包括用于中止部分呈现结果的功能。

这些工具共同提供了丰富且无缝的用户体验，因为它使服务器对用户的影响更不明显，中断工作流。

## <a name="bio"></a>Bio

Scott Cate 一直在使用 Microsoft Web 技术，因为1997，是 myKB.com （[www.myKB.com](http://www.myKB.com)）的总裁，他致力于编写基于知识库软件解决方案的基于 ASP.NET 的应用程序。 可以通过电子邮件联系 Scott [scott.cate@myKB.com](mailto:scott.cate@myKB.com)或[ScottCate.com](http://ScottCate.com)上的博客

> [!div class="step-by-step"]
> [下一部分](understanding-asp-net-ajax-updatepanel-triggers.md)
