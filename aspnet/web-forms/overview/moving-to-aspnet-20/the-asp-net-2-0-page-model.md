---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 页模型 |Microsoft Docs
author: microsoft
description: 在 ASP.NET 1.x 中，开发人员可选择内联代码模型和代码隐藏代码模型。 代码隐藏可以使用 Src attr 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440708"
---
# <a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 页模型

由[Microsoft](https://github.com/microsoft)

> 在 ASP.NET 1.x 中，开发人员可选择内联代码模型和代码隐藏代码模型。 可以使用 Src 特性或 @Page 指令的代码隐藏特性来实现代码隐藏。 在 ASP.NET 2.0 中，开发人员仍然可以在内联代码和代码隐藏之间做出选择，但对代码隐藏模型进行了重大的改进。

在 ASP.NET 1.x 中，开发人员可选择内联代码模型和代码隐藏代码模型。 可以使用 Src 特性或 @Page 指令的代码隐藏特性来实现代码隐藏。 在 ASP.NET 2.0 中，开发人员仍然可以在内联代码和代码隐藏之间做出选择，但对代码隐藏模型进行了重大的改进。

## <a name="improvements-in-the-code-behind-model"></a>代码隐藏模型改进

为了充分了解 ASP.NET 2.0 中代码隐藏模型的更改，最好快速查看 ASP.NET 1.x 中存在的模型。

## <a name="the-code-behind-model-in-aspnet-1x"></a>ASP.NET 1.x 中的代码隐藏模型

在 ASP.NET 1.x 中，代码隐藏模型由一个 ASPX 文件（Webform）和一个包含编程代码的代码隐藏文件组成。 使用 ASPX 文件中的 @Page 指令连接了这两个文件。 ASPX 页上的每个控件在代码隐藏文件中都有一个对应的声明作为实例变量。 代码隐藏文件还包含用于事件绑定的代码，以及 Visual Studio 设计器所需的生成代码。 此模型的工作良好，但由于 ASPX 页中的每个 ASP.NET 元素都需要代码隐藏文件中的相应代码，因此没有真正的代码和内容分离。 例如，如果设计器将新的服务器控件添加到 Visual Studio IDE 之外的 ASPX 文件中，则该应用程序将因缺少代码隐藏文件中该控件的声明而中断。

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2.0 中的代码隐藏模型

ASP.NET 2.0 在此模型上大大改进。 在 ASP.NET 2.0 中，代码隐藏是使用 ASP.NET 2.0 中提供的新*分部类*实现的。 ASP.NET 2.0 中的代码隐藏类定义为分部类，这意味着它仅包含类定义的一部分。 类定义的其余部分是 ASP.NET 2.0 在运行时或在预编译网站时使用 ASPX 页动态生成的。 代码隐藏文件和 ASPX 页之间的链接仍使用 @ Page 指令建立。 但是，ASP.NET 2.0 现在使用 CodeFile 属性，而不是代码隐藏或 Src 特性。 Inherits 特性还用于指定页的类名。

典型的 @ Page 指令可能如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 代码隐藏文件中的典型类定义可能如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C#和 Visual Basic 是当前支持分部类的唯一托管语言。 因此，使用 j # 的开发人员将不能使用 ASP.NET 2.0 中的代码隐藏模型。

新模型增强了代码隐藏模型，因为开发人员现在只包含其创建的代码。 它还提供了代码和内容的真正分离，因为代码隐藏文件中没有实例变量声明。

> [!NOTE]
> 由于 ASPX 页的分部类是发生事件绑定的位置，Visual Basic 开发人员可以通过在代码隐藏中使用 Handles 关键字来绑定事件，从而实现略微提高性能。 C#没有等效关键字。

## <a name="new--page-directive-attributes"></a>新 @ Page 指令特性

ASP.NET 2.0 将许多新属性添加到 @ Page 指令中。 以下属性是 ASP.NET 2.0 中的新增属性。

## <a name="async"></a>Async

Async 属性允许您配置要异步执行的页。 本模块稍后部分介绍的异步页面。

## <a name="asynctimeout"></a>AsyncTimeout

指定了异步页面的超时时间。 默认值为45秒。

## <a name="codefile"></a>CodeFile

CodeFile 特性是 Visual Studio 2002/2003 中的代码隐藏特性的替换项。

### <a name="codefilebaseclass"></a>CodeFileBaseClass

如果希望从一个基类派生多个页，则使用 CodeFileBaseClass 特性。 由于 ASP.NET 中的分部类的实现，如果没有此特性，则使用共享公共字段来引用 ASPX 页中声明的控件的基类将无法正常工作，因为网络编译引擎将基于该页中的控件自动创建新成员。 因此，如果想要在 ASP.NET 中的两个或更多页面上使用一个公共基类，则需要定义在 CodeFileBaseClass 属性中指定基类，然后从该基类派生每个页面类。 使用此属性时，CodeFile 属性也是必需的。

## <a name="compilationmode"></a>CompilationMode

此特性允许您设置 ASPX 页的 CompilationMode 属性。 CompilationMode 属性是一个枚举，其中包含值**Always**、 **Auto**和**Never**。 默认值**始终**为。 如果可能，**自动**设置将阻止 ASP.NET 动态编译页面。 排除动态编译中的页会提高性能。 但是，如果排除的页包含必须编译的代码，则在浏览该页时会引发错误。

## <a name="enableeventvalidation"></a>EnableEventValidation

此特性指定是否验证回发和回调事件。 启用此功能后，将检查回发或回调事件的参数，以确保它们源自最初呈现它们的服务器控件。

## <a name="enabletheming"></a>EnableTheming

此属性指定页面上是否使用 ASP.NET 主题。 默认值为 false。 [模块 10](profiles-themes-and-web-parts.md)中介绍了 ASP.NET 主题。

## <a name="linepragmas"></a>LinePragmas

此属性指定在编译期间是否应添加行杂注。 行杂注是调试器用来标记代码的特定部分的选项。

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

此特性指定是否在页中注入 JavaScript 以便维护回发之间的滚动位置。 默认情况下，此属性为**false** 。

如果此属性为**true**，则 ASP.NET 将在回发时添加一个 &lt;脚本&gt; 块，如下所示：

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

请注意，此脚本块的源为 WebResource。 此资源不是物理路径。 请求此脚本时，ASP.NET 会动态生成脚本。

### <a name="masterpagefile"></a>MasterPageFile

此属性指定当前页的母版页文件。 路径可以是相对路径或绝对路径。 主页面在[模块 4](master-pages.md)中介绍。

## <a name="stylesheettheme"></a>StyleSheetTheme

此属性允许你重写 ASP.NET 2.0 主题定义的用户界面外观属性。 [模块 10](profiles-themes-and-web-parts.md)中介绍了主题。

## <a name="theme"></a>主题

指定页面的主题。 如果没有为 StyleSheetTheme 属性指定值，则主题属性将覆盖应用于页面上的控件的所有样式。

## <a name="title"></a>标题

设置页面的标题。 此处指定的值将显示在所呈现页面的 &lt;标题&gt; 元素中。

### <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

设置 ViewStateEncryptionMode 枚举的值。 可用值**始终**为 "**自动**" 和 "**从不**"。 默认值为 "**自动**"。如果将此属性设置为 "**自动**"，则将对 viewstate 进行加密，这是一个控件通过调用**RegisterRequiresViewStateEncryption**方法发出请求。

## <a name="setting-public-property-values-via-the--page-directive"></a>通过 @ Page 指令设置公共属性值

ASP.NET 2.0 中 @ Page 指令的另一项新功能是能够设置基类的公共属性的初始值。 例如，假设你在基类中有一个名为**SomeText**的公共属性，并且你希望在加载页面时将其初始化为**Hello** 。 只需在 @ Page 指令中设置值即可实现此目的，如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

@ Page 指令的**SomeText**属性将基类中 SomeText 属性的初始值设置为*Hello！* 。 下面的视频介绍如何使用 @ Page 指令在基类中设置公共属性的初始值。

![](the-asp-net-2-0-page-model/_static/image1.png)

[打开全屏视频](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>Page 类的新公共属性

以下公共属性是 ASP.NET 2.0 中的新增属性。

## <a name="apprelativetemplatesourcedirectory"></a>AppRelativeTemplateSourceDirectory

返回页面或控件的应用程序相对路径。 例如，对于位于 http://app/folder/page.aspx的页，属性将返回 ~/folder/。

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

返回页面或控件的相对虚拟目录路径。 例如，对于位于 http://app/folder/page.aspx的页，属性将返回 ~/folder/page.aspx。

## <a name="asynctimeout"></a>AsyncTimeout

获取或设置用于异步页面处理的超时值。 （此模块稍后将介绍异步页面。）

## <a name="clientquerystring"></a>ClientQueryString

一个只读属性，该属性返回所请求 URL 的查询字符串部分。 此值为 URL 编码。 可以使用 HttpServerUtility 类的 UrlDecode 方法对其进行解码。

## <a name="clientscript"></a>ClientScript

此属性返回一个 ClientScriptManager 对象，该对象可用于管理客户端脚本的网络辐射。 （本模块稍后将介绍 ClientScriptManager 类。）

## <a name="enableeventvalidation"></a>EnableEventValidation

此属性控制是否为回发和回调事件启用事件验证。 启用后，将验证回发或回调事件的参数，以确保它们源自最初呈现它们的服务器控件。

## <a name="enabletheming"></a>EnableTheming

此属性获取或设置一个布尔值，该值指定是否将 ASP.NET 2.0 主题应用于页面。

## <a name="form"></a>窗体

此属性以 HtmlForm 对象的形式返回 ASPX 页上的 HTML 窗体。

## <a name="header"></a>Header

此属性返回对 HtmlHead 对象的引用，该对象包含页眉。 可以使用返回的 HtmlHead 对象来获取/设置样式表、Meta 标记等。

## <a name="idseparator"></a>IdSeparator

此只读属性获取 ASP.NET 在为页上的控件生成唯一 ID 时用于分隔控件标识符的字符。 它不可直接通过代码使用。

## <a name="isasync"></a>IsAsync

此属性允许异步页面。 此模块稍后将讨论异步页面。

## <a name="iscallback"></a>IsCallback

如果该页是回调的结果，则此只读属性返回**true** 。 本模块稍后将讨论调用支持。

## <a name="iscrosspagepostback"></a>IsCrossPagePostBack

如果页面是跨页面回发的一部分，则此只读属性返回**true** 。 本模块稍后将介绍跨页面回发。

## <a name="items"></a>项

返回对 IDictionary 实例的引用，该实例包含存储在页上下文中的所有对象。 可以将项添加到此 IDictionary 对象，它们将在上下文的整个生存期内可用。

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostBack

此属性控制是否在发生回发后，ASP.NET 发出用于维护浏览器中的页面滚动位置的 JavaScript。 （此模块前面讨论了此属性的详细信息。）

## <a name="master"></a>主机

此只读属性返回对已应用母版页的页面的 MasterPage 实例的引用。

## <a name="masterpagefile"></a>MasterPageFile

获取或设置页面的母版页文件名。 只能在 PreInit 方法中设置此属性。

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

此属性获取或设置页面状态的最大长度（以字节为单位）。 如果将属性设置为正数，则页面视图状态将被拆分为多个隐藏字段，以使其不超过指定的字节数。 如果该属性为负数，则视图状态不会分解为块。

## <a name="pageadapter"></a>PageAdapter

返回对 PageAdapter 对象的引用，该对象修改请求浏览器的页。

## <a name="previouspage"></a>PreviousPage

返回对服务器传输或跨页面回发的情况下的上一页的引用。

## <a name="skinid"></a>SkinID

指定要应用于页面的 ASP.NET 2.0 外观。

## <a name="stylesheettheme"></a>StyleSheetTheme

此属性获取或设置应用于页面的样式表。

## <a name="templatecontrol"></a>TemplateControl

返回对页的包含控件的引用。

## <a name="theme"></a>主题

获取或设置应用于页面的 ASP.NET 2.0 主题的名称。 必须在 PreInit 方法之前设置此值。

## <a name="title"></a>标题

此属性获取或设置从页面页眉获取的页面的标题。

## <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

获取或设置页的 ViewStateEncryptionMode。 请参阅此模块前面的此属性的详细讨论。

## <a name="new-protected-properties-of-the-page-class"></a>页类的新的受保护属性

下面是 ASP.NET 2.0 中 Page 类的新保护属性。

## <a name="adapter"></a>适配器

返回对在请求该页面的设备上呈现页面的 ControlAdapter 的引用。

## <a name="asyncmode"></a>AsyncMode

此属性指示是否异步处理页。 它旨在供运行时使用，而不是直接在代码中使用。

## <a name="clientidseparator"></a>ClientIDSeparator

此属性返回在为控件创建唯一的客户端 Id 时用作分隔符的字符。 它旨在供运行时使用，而不是直接在代码中使用。

## <a name="pagestatepersister"></a>PageStatePersister

此属性返回页的 PageStatePersister 对象。 此属性主要由 ASP.NET 控件开发人员使用。

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

此属性返回追加到用于缓存浏览器的文件路径的唯一后缀。 默认值为 \_\_ufps = 和6位数字。

## <a name="new-public-methods-for-the-page-class"></a>Page 类的新公共方法

以下公共方法是 ASP.NET 2.0 中 Page 类的新方法。

## <a name="addonprerendercompleteasync"></a>AddOnPreRenderCompleteAsync

此方法为异步页执行注册事件处理程序委托。 此模块稍后将讨论异步页面。

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

将页样式表中的属性应用于页面。

## <a name="executeregisteredasynctasks"></a>ExecuteRegisteredAsyncTasks

此方法是一种异步任务。

### <a name="getvalidators"></a>GetValidators

如果未指定，则返回指定验证组的验证程序的集合或默认验证组。

## <a name="registerasynctask"></a>RegisterAsyncTask

此方法注册新的异步任务。 此模块的后面部分介绍了异步页面。

## <a name="registerrequirescontrolstate"></a>RegisterRequiresControlState

此方法告诉 ASP.NET，必须保留 pages 控件状态。

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateEncryption

此方法告知 ASP.NET 页面视图状态要求加密。

## <a name="resolveclienturl"></a>ResolveClientUrl

返回一个相对 URL，该 URL 可用于对图像的客户端请求等。

## <a name="setfocus"></a>SetFocus

此方法会将焦点设置到最初加载页面时指定的控件。

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState

此方法将注销传递给它的控件，而不再需要控件状态持久性。

## <a name="changes-to-the-page-lifecycle"></a>对页面生命周期的更改

ASP.NET 2.0 的页面生命周期未发生明显变化，但你应该注意一些新的方法。 ASP.NET 2.0 页面生命周期如下所述。

## <a name="preinit-new-in-aspnet-20"></a>PreInit （ASP.NET 2.0 中的新增项）

PreInit 事件是开发人员可以访问的生命周期中的最早阶段。 添加此事件可以以编程方式更改 ASP.NET 2.0 主题、母版页、ASP.NET 2.0 配置文件的访问属性等。如果处于 "回发" 状态，则必须认识到在生命周期的这一点，视图状态尚未应用于控件。 因此，如果开发人员在此阶段更改控件的属性，则可能会在稍后的页面生命周期中覆盖该属性。

## <a name="init"></a>Init

Init 事件未在 ASP.NET 1.x 中发生更改。 你需要在此页上读取或初始化控件的属性。 在此阶段，母版页、主题等已应用于页面。

## <a name="initcomplete-new-in-20"></a>InitComplete （2.0 中的新增项）

在页面初始化阶段结束时调用 InitComplete 事件。 此时，你可以访问页面上的控件，但尚未填充其状态。

## <a name="preload-new-in-20"></a>预加载（2.0 中的新增项）

此事件在所有回发数据已应用并刚好在页面\_负载之前调用。

## <a name="load"></a>Load

Load 事件未在 ASP.NET 1.x 中发生更改。

## <a name="loadcomplete-new-in-20"></a>System.web.ui.page.loadcomplete （2.0 中的新增项）

System.web.ui.page.loadcomplete 事件是页面加载阶段中的最后一个事件。 在此阶段，所有回发和 viewstate 数据都已应用到页面。

## <a name="prerender"></a>PreRender

如果希望为动态添加到页面中的控件正确维护视图状态，则预呈现事件是最后添加它们的机会。

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete （2.0 中的新增项）

在 PreRenderComplete 阶段，所有控件都已添加到页面中，并且页已准备好进行呈现。 PreRenderComplete 事件是在保存页面 viewstate 之前引发的最后一个事件。

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete （2.0 中的新增项）

在保存所有页面视图状态和控件状态之后，会立即调用 SaveStateComplete 事件。 这是页面实际呈现到浏览器之前的最后一个事件。

## <a name="render"></a>Render

自 ASP.NET 1.x 后，Render 方法尚未更改。 这是 HtmlTextWriter 的初始化位置，页面呈现到浏览器。

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0 中的跨页面回发

在 ASP.NET 1.x 中，回发到相同的页面需要回发。 不允许跨页面回发。 ASP.NET 2.0 添加了通过 IButtonControl 接口回发到不同页的功能。 除了第三方自定义控件以外，任何实现新的 IButtonControl 接口（Button、LinkButton 和 ImageButton）的控件都可以通过使用 PostBackUrl 特性来利用此新功能。 下面的代码演示了一个按钮控件，该按钮控件回发到第二页。

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

页面回发后，可以通过第二页上的 PreviousPage 属性访问启动回发的页面。 此功能通过新的 WebForm\_DoPostBackWithOptions 客户端函数实现，当控件回发到其他页时，ASP.NET 2.0 将呈现到页面。 此 JavaScript 函数由将脚本发送到客户端的新 WebResource 处理程序提供。

以下视频是跨页面回发的演练。

![](the-asp-net-2-0-page-model/_static/image2.png)

[打开全屏视频](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>跨页面回发的详细信息

### <a name="viewstate"></a>Viewstate

您可能已就跨页面回发方案的第一页中的视图状态进行了询问。 毕竟，任何未实现 IPostBackDataHandler 的控件都将通过 viewstate 保持其状态，因此，若要在跨页面回发的第二页上访问该控件的属性，您必须对该页的视图状态具有访问权限。 ASP.NET 2.0 使用名为 \_\_PREVIOUSPAGE 的第二页中的新隐藏字段来处理这种情况。 \_\_PREVIOUSPAGE 窗体字段包含第一页的视图状态，以便您可以访问第二页中所有控件的属性。

### <a name="circumventing-findcontrol"></a>规避 FindControl

在跨页面回发的视频演练中，我使用了 FindControl 方法获取对第一页上 TextBox 控件的引用。 这种方法非常适用于这种用途，但 FindControl 的开销很高，需要编写其他代码。 幸运的是，在许多情况下，ASP.NET 2.0 为此目的提供了 FindControl 的替代方法。 使用 PreviousPageType 指令，可以通过使用 TypeName 或 VirtualPath 属性对上一页进行强类型引用。 TypeName 属性允许您指定上一页的类型，而 VirtualPath 属性允许您使用虚拟路径引用上一页。 设置 PreviousPageType 指令后，必须使用公共属性公开要允许其访问的控件等。

## <a name="lab-1-cross-page-postback"></a>实验室1跨页面回发

在此实验室中，您将创建一个应用程序，该应用程序使用 ASP.NET 2.0 的新跨页面回发功能。

1. 打开 Visual Studio 2005 并创建新的 ASP.NET 网站。
2. 添加一个名为 page2 的新 Webform。
3. 在设计视图中打开 default.aspx 并添加 "按钮" 控件和 "TextBox" 控件。 

    1. 为 "Button" 控件指定 ID " **SubmitButton** "，并在文本框中控制**用户名**的 id。
    2. 将按钮的 PostBackUrl 属性设置为 page2。
4. 在源视图中打开 page2。
5. 添加 @ PreviousPageType 指令，如下所示：
6. 将以下代码添加到 page2 的代码隐藏页\_负载： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. 通过单击 "生成" 菜单上的 "生成" 来生成项目。
8. 将以下代码添加到 default.aspx 的代码隐藏中： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. 将 page2 中的页\_负载更改为以下内容： 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. 生成项目。
11. 运行该项目。
12. 在文本框中输入您的姓名，然后单击该按钮。
13. 结果是什么？

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0 中的异步页面

ASP.NET 中的许多争用问题都是由外部调用（如 Web 服务或数据库调用）延迟、文件 IO 延迟等引起的。对 ASP.NET 应用程序发出请求时，ASP.NET 会使用其工作线程之一来处理请求。 请求完成并发送响应之前，该请求拥有该线程。 ASP.NET 2.0 通过添加以异步方式执行页面的功能，查找解决此类问题的延迟问题。 这意味着，工作线程可以启动请求，然后将其他执行移交给另一个线程，从而快速返回到可用线程池。 文件 IO、数据库调用等完成后，将从线程池中获取一个新线程来完成请求。

使页面异步执行的第一步是设置页面指令的**Async**属性，如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

此属性告知 ASP.NET 实现页面的 IHttpAsyncHandler。

下一步是在页面生命周期中的某个时间点调用 AddOnPreRenderCompleteAsync 方法，然后再开始呈现。 （此方法通常在页\_负载中调用。）AddOnPreRenderCompleteAsync 方法采用两个参数;一个来和一个 EndEventHandler。 来返回 IAsyncResult，然后将其作为参数传递给 EndEventHandler。

以下视频是异步页面请求的演练。

![](the-asp-net-2-0-page-model/_static/image3.png)

[打开全屏视频](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> 在 EndEventHandler 完成之前，async page 不会呈现给浏览器。 毫无疑问，但某些开发人员会将异步请求视为类似于异步回调。 请注意，这一点很重要。 异步请求的好处是，第一个工作线程可以返回给线程池以处理新请求，从而减少由于 IO 绑定等原因导致的争用。

## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0 中的脚本回调

Web 开发人员一直在寻找阻止与回叫关联的闪烁的方式。 在 ASP.NET 1.x 中，SmartNavigation 是避免闪烁的最常见方法，但 SmartNavigation 为某些开发人员带来了问题，因为它在客户端上的实现复杂度很高。 ASP.NET 2.0 解决了脚本回调的这一问题。 脚本回调利用 XMLHttp 通过 JavaScript 向 Web 服务器发出请求。 XMLHttp 请求返回可通过浏览器的 DOM 操作的 XML 数据。 新的 WebResource 处理程序对用户隐藏了 XMLHttp 代码。

在 ASP.NET 2.0 中配置脚本回叫需要几个步骤。

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>步骤1：实现 ICallbackEventHandler 接口

为了使 ASP.NET 能够将页面视为参与脚本回调，必须实现 ICallbackEventHandler 接口。 可在代码隐藏文件中执行此操作，如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

还可以使用 @ Implements 指令执行此操作，如下所示：

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

使用内联 ASP.NET 代码时，通常使用 @ Implements 指令。

## <a name="step-2--call-getcallbackeventreference"></a>步骤2：调用 GetCallbackEventReference

如前所述，XMLHttp 调用封装在 WebResource 处理程序中。 呈现页面时，ASP.NET 将添加对 WebForm\_DoCallback 的调用，该脚本是由 WebResource 提供的客户端脚本。 WebForm\_DoCallback 函数将替换回调的 \_\_doPostBack 函数。 请记住，\_\_doPostBack 以编程方式在页面上提交窗体。 在回调方案中，您想要阻止回发，因此 \_\_doPostBack 将无法满足要求。

> [!NOTE]
> \_\_doPostBack 仍在客户端脚本回调方案中呈现给页面。 但是，它不用于回调。

WebForm\_DoCallback 客户端函数的参数是通过服务器端函数 GetCallbackEventReference 提供的，该函数通常会在页面\_负载中调用。 典型的 GetCallbackEventReference 调用可能如下所示：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> 在这种情况下，cm 是 ClientScriptManager 的实例。 本模块稍后将介绍 ClientScriptManager 类。

GetCallbackEventReference 有几个重载版本。 在这种情况下，参数如下所示：

`this`

对在其中调用 GetCallbackEventReference 的控件的引用。 在这种情况下，它是页面本身。

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

将从客户端代码传递到服务器端事件的字符串参数。 在这种情况下，Im 传递名为 ddlCompany 的下拉列表的值。

`ShowCompanyName`

将接受来自服务器端回调事件的返回值（字符串）的客户端函数的名称。 只有服务器端回调成功时，才会调用此函数。 因此，为实现稳定性，通常建议使用 GetCallbackEventReference 的重载版本，该版本使用额外的字符串参数指定在发生错误时要执行的客户端函数的名称。

`null`

表示它在回调服务器之前启动的客户端函数的字符串。 在这种情况下，没有这样的脚本，因此参数为 null。

`true`

指定是否异步执行回调的布尔值。

对客户端上的 WebForm\_DoCallback 的调用将传递这些参数。 因此，当在客户端上呈现此页时，该代码将如下所示：

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

请注意，客户端上函数的签名有点不同。 客户端函数传递5个字符串和一个布尔值。 附加字符串（在上面的示例中为 null）包含将处理服务器端回调中的任何错误的客户端函数。

## <a name="step-3--hook-the-client-side-control-event"></a>步骤3：挂钩客户端控件事件

请注意，上面 GetCallbackEventReference 的返回值已分配给字符串变量。 该字符串用于挂钩启动回调的控件的客户端事件。 在此示例中，回调由页面上的下拉列表启动，因此我想要挂钩*OnChange*事件。

若要挂钩客户端事件，只需按如下所示将处理程序添加到客户端标记：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

请记住， *cbRef*是对 GetCallbackEventReference 的调用的返回值。 它包含上面所示的对 WebForm\_DoCallback 的调用。

## <a name="step-4--register-the-client-side-script"></a>步骤4：注册客户端脚本

请注意，调用 GetCallbackEventReference 指定了服务器端回调成功时，将执行名为**ShowCompanyName**的客户端脚本。 该脚本需要使用 ClientScriptManager 实例添加到页面。 （本模块稍后将讨论 ClientScriptManager 类。）如下所示：

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>步骤5：调用 ICallbackEventHandler 接口的方法

ICallbackEventHandler 包含两个需要在代码中实现的方法。 它们分别是**RaiseCallbackEvent**和**GetCallbackEvent**。

**RaiseCallbackEvent**采用字符串作为参数，并且不返回任何内容。 字符串自变量将从客户端对 WebForm\_DoCallback 的调用传递。 在这种情况下，该值是名为 ddlCompany 的 dropdown 的*value*属性。 服务器端代码应放置在 RaiseCallbackEvent 方法中。 例如，如果你的回调正在对外部资源进行 WebRequest，则该代码应放置在 RaiseCallbackEvent 中。

**GetCallbackEvent**负责处理返回给客户端的回调。 它不采用任何参数并返回字符串。 它返回的字符串将作为参数传递到客户端函数（在本例中为*ShowCompanyName*）。

完成上述步骤后，即可在 ASP.NET 2.0 中执行脚本回调。

![](the-asp-net-2-0-page-model/_static/image4.png)

[打开全屏视频](the-asp-net-2-0-page-model/_static/callback1.wmv)

支持发出 XMLHttp 调用的任何浏览器都支持 ASP.NET 中的脚本回调。 这包括目前正在使用的所有新式浏览器。 Internet Explorer 使用 XMLHttp ActiveX 对象，而其他新式浏览器（包括即将推出的 IE 7）使用内部 XMLHttp 对象。 若要以编程方式确定浏览器是否支持回调，可以使用**SupportCallback**属性。 如果请求的客户端支持脚本回调，则此属性将返回**true** 。

## <a name="working-with-client-script-in-aspnet-20"></a>在 ASP.NET 2.0 中使用客户端脚本

ASP.NET 2.0 中的客户端脚本通过使用 ClientScriptManager 类进行管理。 ClientScriptManager 类跟踪使用类型和名称的客户端脚本。 这可以防止在页上以编程方式多次插入同一脚本。

> [!NOTE]
> 在页面上成功注册了脚本后，任何以后注册同一个脚本的尝试都将导致脚本不会第二次注册。 不会添加重复的脚本，也不会发生任何异常。 若要避免不必要的计算，可以使用一些方法来确定脚本是否已注册，以便不会多次尝试注册。

所有当前 ASP.NET 开发人员都应该熟悉 ClientScriptManager 的方法：

## <a name="registerclientscriptblock"></a>RegisterClientScriptBlock

此方法将脚本添加到呈现的页面的顶部。 这对于添加将在客户端上显式调用的函数很有用。

此方法有两个重载版本。 其中有三个参数共同。 它们是：

`type (string)`

***类型***参数标识脚本的类型。 通常最好使用页面的类型（此为。类型的 GetType （））。

`key (string)`

***Key***参数是该脚本的用户定义的键。 对于每个脚本，这应该是唯一的。 如果尝试添加的脚本的键和类型与已添加的脚本的类型相同，则不会添加该脚本。

`script (string)`

***脚本***参数是包含要添加的实际脚本的字符串。 建议使用 StringBuilder 创建脚本，然后对 StringBuilder 使用 ToString （）方法以分配***脚本***参数。

如果使用只使用三个参数的重载 Page.clientscript.registerclientscriptblock，则必须在脚本中包含 script 元素（&lt;script&gt; 和 &lt;/script&gt;）。

您可以选择使用 Page.clientscript.registerclientscriptblock 的重载，该重载采用第四个参数。 第四个参数是一个布尔值，该值指定 ASP.NET 是否应为您添加脚本元素。 如果此参数为**true**，则脚本不应显式包含脚本元素。

使用 IsClientScriptBlockRegistered 方法来确定脚本是否已注册。 这使你可以避免尝试重新注册已注册的脚本。

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude （2.0 中的新增项）

RegisterClientScriptInclude 标记创建链接到外部脚本文件的脚本块。 它有两个重载。 一个使用密钥和 URL。 第二个添加指定类型的第三个参数。

例如，下面的代码生成一个脚本块，该脚本块链接到应用程序的 scripts 文件夹的根目录中的 jsfunctions：

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

此代码在呈现的页中生成以下代码：

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> 脚本块呈现在页面的底部。

使用 IsClientScriptIncludeRegistered 方法来确定脚本是否已注册。 这样可以避免尝试重新注册脚本。

## <a name="registerstartupscript"></a>RegisterStartupScript

Page.clientscript.registerstartupscript 方法采用与 Page.clientscript.registerclientscriptblock 方法相同的参数。 使用 Page.clientscript.registerstartupscript 注册的脚本在页面加载后，但在 OnLoad 客户端事件之前执行。 在1.x 中，向 Page.clientscript.registerstartupscript 注册的脚本放置在结束 &lt;/form&gt; 标记之前，而向 Page.clientscript.registerclientscriptblock 注册的脚本则紧靠在开始 &lt;窗体&gt; 标记之后。 在 ASP.NET 2.0 中，两者紧靠在结束 &lt;/form&gt; 标记之前。

> [!NOTE]
> 如果向 Page.clientscript.registerstartupscript 注册一个函数，则在客户端代码中显式调用该函数之前，该函数将不会执行。

使用 IsStartupScriptRegistered 方法来确定脚本是否已注册，并避免尝试重新注册脚本。

## <a name="other-clientscriptmanager-methods"></a>其他 ClientScriptManager 方法

下面是 ClientScriptManager 类的一些其他有用方法。

|  <strong>GetCallbackEventReference</strong>   |                                                 请参阅此模块前面的脚本回调。                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                获取可用于从客户端事件回发的 JavaScript 引用（javascript：&lt;调用&gt;）。                 |
|  <strong>System.web.ui.clientscriptmanager.getpostbackeventreference</strong>   |                                   获取一个字符串，该字符串可用于从客户端启动回发。                                    |
|      <strong>GetWebResourceUrl</strong>       | 返回嵌入到程序集中的资源的 URL。 必须与<strong>RegisterClientScriptResource</strong>结合使用。 |
| <strong>RegisterClientScriptResource</strong> |     向页注册 Web 资源。 这些资源嵌入在程序集中，并由新的 WebResource 处理程序进行处理。      |
|     <strong>RegisterHiddenField</strong>      |                                                 向页面注册一个隐藏的窗体字段。                                                 |
|  <strong>RegisterOnSubmitStatement</strong>   |                                  注册在提交 HTML 窗体时执行的客户端代码。                                   |
