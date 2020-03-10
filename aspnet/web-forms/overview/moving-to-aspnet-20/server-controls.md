---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: 服务器控件 |Microsoft Docs
author: microsoft
description: ASP.NET 2.0 通过多种方式增强服务器控件。 在此模块中，我们将介绍 ASP.NET 2.0 和 Visual Studio 200 的方式的一些体系结构更改 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: c02a633013f061c09141d4f98871848c011a799e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521090"
---
# <a name="server-controls"></a>服务器控件

由[Microsoft](https://github.com/microsoft)

> ASP.NET 2.0 通过多种方式增强服务器控件。 在此模块中，我们将介绍 ASP.NET 2.0 和 Visual Studio 2005 处理服务器控件的方式的一些体系结构更改。

ASP.NET 2.0 通过多种方式增强服务器控件。 在此模块中，我们将介绍 ASP.NET 2.0 和 Visual Studio 2005 处理服务器控件的方式的一些体系结构更改。

## <a name="view-state"></a>视图状态

ASP.NET 2.0 中视图状态的主要变化是大小大幅降低。 假设只有一个日历控件的页面。 下面是 ASP.NET 1.1 中的视图状态。

[!code-css[Main](server-controls/samples/sample1.css)]

下面是 ASP.NET 2.0 中相同页面上的视图状态。

[!code-css[Main](server-controls/samples/sample2.css)]

这是一种非常重要的变化，考虑到视图状态是在网络上来回进行的，此更改可使开发人员大大提高性能。 视图状态的减小很大程度上取决于我们在内部处理它的方式。 请记住，视图状态为 Base64 编码的字符串。 为了更好地了解 ASP.NET 2.0 中视图状态的变化，我们来看看上述示例中的解码值。

下面是1.1 视图状态解码：

[!code-css[Main](server-controls/samples/sample3.css)]

这看起来可能有点像杂乱，但这里有一种模式。 在 ASP.NET 1.x 中，我们使用了单个字符来识别数据类型，使用 &lt;&gt; 字符来识别分隔值。 上面视图状态示例中的 "t" 表示三态。 三元包含一对 Arraylist （"l" 表示 ArrayList。）其中一个 Arraylist 包含值为1的 Int32 （"i"），而另一个包含其他三元。 三元包含一对 Arraylist 等。需要记住的重要一点是，我们使用包含对的 Triplets，通过字母标识数据类型，并使用 &lt; 和 &gt; 字符作为分隔符。

在 ASP.NET 2.0 中，解码的视图状态看起来有点不同。

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

你应注意到已解码视图状态的外观发生了重大更改。 此更改具有多个体系结构 connect-through。 ASP.NET 1.x 中的视图状态使用 LosFormatter 来序列化数据。 在2.0 中，我们使用新的 ObjectStateFormatter 类。 此类专门用于帮助序列化和反序列化视图状态和控件状态。 （下一节将介绍控件状态。）通过更改进行序列化和反序列化的方法，可以获得许多好处。 最显著的一点是，与使用 LosFormatter 的情况不同的是，ObjectStateFormatter 使用 BinaryWriter。 这允许 ASP.NET 2.0 存储视图状态一系列字节而不是字符串。 例如，使用整数。 在 ASP.NET 1.1 中，需要4个字节的视图状态的整数。 在 ASP.NET 2.0 中，同一整数仅需要1个字节。 为了减少存储的视图状态量，已进行了其他增强。 例如，现在使用 Environment.tickcount 而不是字符串存储 DateTime 值。

就像这一切都不够，只需特别注意的是，在1.x 中，视图状态的最大使用者之一就是 DataGrid 和类似控件。 控件（如视图状态所处的数据网格）的主要缺点是它通常包含大量重复的信息。 在 ASP.NET 1.x 中，重复的信息完全存储在一起，从而导致臃肿的视图状态。 在 ASP.NET 2.0 中，我们使用新的 IndexedString 类来存储此类数据。 如果字符串重复，只需将 IndexedString 的标记和索引存储在正在运行的 IndexedString 对象的表中。

## <a name="control-state"></a>控件状态

开发人员对视图状态的主要牢骚之一是它添加到 HTTP 有效负载的大小。 如前文所述，视图状态的最大使用者之一是 DataGrid 控件。 为了避免 DataGrid 生成大量的视图状态，许多开发人员只是对该控件禁用了视图状态。 遗憾的是，这种解决方案并不总是很好。 ASP.NET 1.x 中的视图状态不仅包含正确的控件功能所必需的数据。 它还包含有关控件的 UI 状态的信息。 这意味着，如果你希望允许在 DataGrid 上进行分页，则必须启用视图状态，即使你不需要视图状态包含的所有 UI 信息。 这是一个全或无意义的方案。

在 ASP.NET 2.0 中，控件状态通过引入控件状态来解决该问题。 控件状态包含对于控件的适当功能绝对必要的数据。 与视图状态不同，控件状态无法禁用。 因此，非常重要的一点是，严格控制以控件状态存储的数据。

> [!NOTE]
> 控件状态与视图状态一起保留在 \_\_VIEWSTATE 隐藏窗体字段中。

此视频是有关视图状态和控件状态的演练。

![](server-controls/_static/image1.png)

[打开全屏视频](server-controls/_static/state1.wmv)

为了使服务器控件能够读取和写入控件状态，必须执行三个步骤。

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>步骤1：调用 RegisterRequiresControlState 方法

RegisterRequiresControlState 方法通知 ASP.NET 控件需要保持控件状态。 它采用一个类型为控件的参数，该参数是正在注册的控件。

请务必注意，注册不会从请求请求中保留。 因此，如果控件要保持控件状态，则必须在每个请求上调用此方法。 建议在 OnInit 中调用方法。

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>步骤2：重写 SaveControlState

SaveControlState 方法会在最后一次回发后保存控件的控件状态更改。 它返回表示控件状态的对象。

## <a name="step-3-override-loadcontrolstate"></a>步骤3：重写 LoadControlState

LoadControlState 方法将已保存状态加载到控件中。 方法采用一个类型为 Object 的参数，该参数保存控件的已保存状态。

## <a name="full-xhtml-compliance"></a>完全符合 XHTML 标准

任何 Web 开发人员都知道 Web 应用程序中标准的重要性。 为了维护基于标准的开发环境，ASP.NET 2.0 完全符合 XHTML 标准。 因此，在支持 HTML 4.0 或更高版本的浏览器中，将根据 XHTML 标准呈现所有标记。

ASP.NET 1.1 中的 DOCTYPE 定义如下所示：

[!code-html[Main](server-controls/samples/sample6.html)]

在 ASP.NET 2.0 中，默认 DOCTYPE 定义如下所示：

[!code-html[Main](server-controls/samples/sample7.html)]

如果选择，则可以通过配置文件中的 xhtmlConformance 节点更改默认的 XHTML 符合性。 例如，web.config 文件中的以下节点会将 XHTML 符合性更改为 XHTML 1.0 Strict：

[!code-xml[Main](server-controls/samples/sample8.xml)]

如果选择此项，还可以将 ASP.NET 配置为使用 ASP.NET 1.x 中使用的旧配置，如下所示：

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>使用适配器的自适应呈现

在 ASP.NET 1.x 中，配置文件包含一个填充 HttpBrowserCapabilities 对象的 &lt;browserCaps&gt; 部分。 此对象允许开发人员确定哪个设备发出特定请求并适当地呈现代码。 在 ASP.NET 2.0 中，模型已改进，现在使用新的 ControlAdapter 类。 ControlAdapter 类重写控件生命周期中的事件，并基于用户代理的功能控制控件的呈现。 特定用户代理的功能由存储在 c:\windows\microsoft.net\framework\v2.0. 中的浏览器定义文件（扩展名为 .browser 的文件）定义\*\*\*\*\CONFIG\Browsers 文件夹。

> [!NOTE]
> ControlAdapter 类是一个抽象类。

与 &lt;中的 browserCaps&gt; 部分非常类似，浏览器定义文件使用正则表达式来分析用户代理字符串，以便识别请求的浏览器。 它们定义了该用户代理的特定功能。 ControlAdapter 通过 Render 方法呈现控件。 因此，如果重写 Render 方法，则不应调用基类上的 Render。 这样做可能会导致呈现发生两次，一次针对适配器，一次用于控件本身。

## <a name="developing-a-custom-adapter"></a>开发自定义适配器

可以通过从 ControlAdapter 继承来开发您自己的自定义适配器。 此外，如果页面需要适配器，则可以从抽象类 PageAdapter 继承。 通过浏览器定义文件中的 &lt;controlAdapters&gt; 元素，可以将控件映射到自定义适配器。 例如，以下来自浏览器定义文件的 XML 将 Menu 控件映射到 MenuAdapter 类：

[!code-html[Main](server-controls/samples/sample10.html)]

使用此模型，控件开发人员可以很轻松地以特定设备或浏览器为目标。 对于开发人员而言，对每个设备上页面的呈现方式进行完全控制也非常简单。

## <a name="per-device-rendering"></a>每设备渲染

可以使用浏览器特定的前缀，为每个设备指定 ASP.NET 2.0 中的服务器控件属性。 例如，下面的代码将更改标签的文本，具体取决于浏览页面所使用的设备。

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

当从 Internet Explorer 浏览包含此标签的页面时，标签将显示 "您正在从 Internet Explorer 浏览" 的文本。 从 Firefox 浏览该页面时，标签将显示 "正在从 Firefox 浏览" 的文本。 从任何其他设备浏览该页面时，它将显示 "正在从未知设备进行浏览。" 可使用此特殊语法指定任何属性。

## <a name="setting-focus"></a>设置焦点

ASP.NET 1.x 开发人员经常会询问如何对特定控件设置初始焦点。 例如，在登录页上，在首次加载页面时，使 "用户 ID" 文本框获得焦点非常有用。 在 ASP.NET 1.x 中，执行此操作需要编写一些客户端脚本。 尽管此类脚本是一项简单的任务，但由于 SetFocus 方法，它在 ASP.NET 2.0 中不再是必需的。 SetFocus 方法采用一个参数，该参数指示应该接收焦点的控件。 此参数可以是控件的客户端 ID，也可以是作为控件对象的服务器控件的名称。 例如，若要在第一次加载页面时将初始焦点设置为一个名为 txtUserID 的 TextBox 控件，请将以下代码添加到页面\_负载：

[!code-csharp[Main](server-controls/samples/sample12.cs)]

--或

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2.0 使用 Webresource 处理程序（前面讨论过）来呈现设置焦点的客户端函数。 客户端函数的名称是 WebForm\_AutoFocus，如下所示：

[!code-html[Main](server-controls/samples/sample14.html)]

此外，还可以使用控件的焦点方法将初始焦点设置到该控件。 焦点方法派生自 Control 类，可用于所有 ASP.NET 2.0 控件。 还可以在发生验证错误时将焦点设置到特定控件。 将在后面的模块中介绍。

## <a name="new-server-controls-in-aspnet-20"></a>ASP.NET 2.0 中的新服务器控件

下面是 ASP.NET 2.0 中的新服务器控件。 我们将在后面的模块中详细介绍其中一些内容。

## <a name="imagemap-control"></a>ImageMap 控件

ImageMap 控件使你可以向映像添加热点，使其可以发起回发或导航到 URL。 有三种可用的热点类型;CircleHotSpot、RectangleHotSpot 和 PolygonHotSpot。 通过 Visual Studio 中的集合编辑器或以编程方式在代码中添加热点。 没有用户界面可用于绘制图像上的热点。 必须以声明方式指定作用点的坐标、大小或半径。 设计器中也没有热点的直观表示形式。 如果将作用点配置为导航到 URL，则 URL 是通过作用点的 NavigateUrl 属性指定的。 对于回发热点，PostBackValue 属性允许您传递回发中可在服务器端代码中检索的字符串。

![Visual Studio 中的作用点集合编辑器](server-controls/_static/image1.jpg)

**图 1**： Visual Studio 中的热点集合编辑器

## <a name="bulletedlist-control"></a>BulletedList 控件

BulletedList 控件是可以轻松地进行数据绑定的项目符号列表。 可以通过 BulletStyle 属性对该列表进行排序（编号）或无序。 列表中的每一项都由一个列表项对象表示。

![Visual Studio 中的 BulletedList 控件](server-controls/_static/image1.gif)

**图 2**： Visual Studio 中的 BulletedList 控件

## <a name="hiddenfield-control"></a>HiddenField 控件

HiddenField 控件向页面中添加一个隐藏的窗体字段，此字段的值在服务器端代码中可用。 在 post 后，隐藏的窗体字段的值通常应保持不变。 但是，恶意用户可能会在回发之前更改值。 如果发生这种情况，HiddenField 控件将引发 ValueChanged 事件。 如果 HiddenField 控件中包含敏感信息，并且要确保它保持不变，应在代码中处理 ValueChanged 事件。

## <a name="fileupload-control"></a>FileUpload 控件

ASP.NET 2.0 中的 FileUpload 控件使你可以通过 ASP.NET 页将文件上传到 Web 服务器。 此控件非常类似于 ASP.NET 1.x HtmlInputFile 类，但有一些例外情况。 在 ASP.NET 1.x 中，建议检查 PostedFile 属性是否为 null，以确定是否有合适的文件。 ASP.NET 2.0 中的 FileUpload 控件添加了一个新的 HasFile 属性，你可以将其用于相同的目的，而且效率更高。

PostedFile 属性仍可用于访问 HttpPostedFile 对象，但 HttpPostedFile 的某些功能现在可在 FileUpload 控件的内部使用。 例如，若要将上载的文件保存在 ASP.NET 1.x 中，请对 HttpPostedFile 对象调用 SaveAs 方法。 使用 ASP.NET 2.0 中的 FileUpload 控件，可以对 FileUpload 控件本身调用 SaveAs 方法。

2\.0 行为的另一个重大更改（并且可能是最重大的更改）是不再需要在保存之前将整个上载的文件加载到内存中。 在1.x 中，上传的任何文件都将在写入磁盘之前完全保存在内存中。 此体系结构阻止上传大型文件。

在 ASP.NET 2.0 中，httpRuntime 元素的 requestLengthDiskThreshold 属性允许你配置在将缓冲区中的缓冲区中包含多少 Kb，然后再将其写入磁盘。

**重要**说明： MSDN 文档（和其他位置的文档）指定此值以字节（而非 kb）为单位，默认值为256。 实际以 Kb 为单位指定该值，默认值为80。 通过将默认值设置为80K，我们确保缓冲区不会在大型对象堆上结束。

## <a name="wizard-control"></a>向导控件

使用面板或从页面传输到页面时，ASP.NET 开发人员努力尝试使用一系列 "页面" 收集信息非常常见。 通常情况下，这是一项令人沮丧的工作，非常耗时。 新向导控件通过允许用户熟悉的向导界面中的线性和非线性步骤，解决了问题。 该向导控件在一系列步骤中提供输入窗体。 每个步骤都是由控件的 StepType 属性指定的特定类型。 可用步骤类型如下：

| **步骤类型** | **解释** |
| --- | --- |
| 自动 | 向导会根据步骤在步骤层次结构内的位置自动确定步骤类型。 |
| Start | 第一步，通常用于提供介绍性语句。 |
| 步骤 | 正常步骤。 |
| 完成 | 最后一个步骤，通常用于显示完成向导的按钮。 |
| 完成 | 显示消息 "成功" 或 "失败"。 |

> [!NOTE]
> 向导控件使用 ASP.NET 控件状态来跟踪其状态。 因此，可以将 EnableViewState 属性设置为 false，无需任何不利。

此视频是向导控件的演练。

![](server-controls/_static/image2.png)

[打开全屏视频](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>本地化控件

"本地化" 控件类似于 "文本" 控件。 但 "本地化" 控件具有一个**模式**属性，该属性控制向其添加标记的方式。 Mode 属性支持以下值：

| **模式** | **解释** |
| --- | --- |
| Transform | 根据发出请求的浏览器的协议来转换标记。 |
| 直通 | 标记按原样呈现。 |
| 编码 | 添加到控件的标记使用 Server.htmlencode 进行编码。 |

## <a name="multiview-and-view-controls"></a>查看和查看控件

多视图控件用作视图控件的容器，而视图控件充当其他控件的容器（与面板控件非常相似）。 查看视图控件中的每个视图都由单个视图控件表示。 此视图中的第一个视图控件是 view 0，第二个视图控件是 view 1，依此类推。您可以通过指定 "ActiveViewIndex" 控件的 "视图" 来切换视图。

## <a name="substitution-control"></a>替换控件

替换控件与 ASP.NET 缓存结合使用。 如果你想要利用缓存，但你有一些必须在每个请求上更新的页面（换句话说，是从缓存中免除的部分），则替换组件会提供一个很好的解决方案。 控件实际上不会自行呈现任何输出。 而是绑定到服务器端代码中的方法。 请求页面时，将调用方法，而返回的标记将替换为替换控件。

通过方法**名称**属性指定替换控件所绑定到的方法。 该方法必须满足以下条件：

- 它必须是静态的（在 VB 中共享）方法。
- 它接受一个类型为 HttpContext 的参数。
- 它将返回一个字符串，该字符串表示应该替换页面上的控件的标记。

替换控件不能修改该页上的任何其他控件，但它可以通过其参数访问当前 HttpContext。

## <a name="gridview-control"></a>GridView 控件

GridView 控件是对 DataGrid 控件的替换。 稍后的模块中将更详细地介绍此控件。

## <a name="detailsview-control"></a>DetailsView 控件

使用 DetailsView 控件可以显示数据源中的单个记录，还可以编辑或删除该记录。 稍后的模块中更详细地介绍了这种情况。

## <a name="formview-control"></a>FormView 控件

FormView 控件用于在可配置接口中显示数据源中的单个记录。 稍后的模块中更详细地介绍了这种情况。

## <a name="accessdatasource-control"></a>AccessDataSource 控件

AccessDataSource 控件用于对 Access 数据库进行数据绑定。 稍后的模块中更详细地介绍了这种情况。

## <a name="objectdatasource-control"></a>ObjectDataSource 控件

ObjectDataSource 控件用于支持三层体系结构，使控件可以数据绑定到中间层业务对象，而不是将控件直接绑定到数据源的两层模型。 稍后的模块中将对此进行更详细的讨论。

## <a name="xmldatasource-control"></a>XmlDataSource 控件

XmlDataSource 控件用于将数据绑定到 XML 数据源。 稍后的模块中更详细地介绍了这种情况。

## <a name="sitemapdatasource-control"></a>SiteMapDataSource 控件

SiteMapDataSource 控件根据站点地图提供站点导航控件的数据绑定。 稍后的模块中将对此进行更详细的讨论。

## <a name="sitemappath-control"></a>SiteMapPath 控件

SiteMapPath 控件显示一系列通常称为痕迹导航的导航链接。 稍后的模块中更详细地介绍了这种情况。

## <a name="menu-control"></a>Menu 控件

Menu 控件使用 DHTML 显示动态菜单。 稍后的模块中更详细地介绍了这种情况。

## <a name="treeview-control"></a>TreeView 控件

TreeView 控件用于显示数据的分层树视图。 稍后的模块中更详细地介绍了这种情况。

## <a name="login-control"></a>登录控件

登录控件提供了用于登录到网站的机制。 稍后的模块中更详细地介绍了这种情况。

## <a name="loginview-control"></a>LoginView 控件

登录视图控件允许基于用户的登录状态显示不同的模板。 稍后的模块中更详细地介绍了这种情况。

## <a name="passwordrecovery-control"></a>PasswordRecovery 控件

PasswordRecovery 控件用于检索 ASP.NET 应用程序的用户的忘记密码。 稍后的模块中更详细地介绍了这种情况。

## <a name="loginstatus"></a>LoginStatus

LoginStatus 控件显示用户的登录状态。 稍后的模块中更详细地介绍了这种情况。

## <a name="loginname"></a>LoginName

LoginName 控件在登录到 ASP.NET 应用程序后显示用户的用户名。 稍后的模块中更详细地介绍了这种情况。

## <a name="createuserwizard"></a>CreateUserWizard

CreateUserWizard 是一个可配置的向导，它使用户能够创建 ASP.NET 成员资格帐户，以便在 ASP.NET 应用程序中使用。 稍后的模块中更详细地介绍了这种情况。

## <a name="changepassword"></a>ChangePassword

ChangePassword 控件允许用户为 ASP.NET 应用程序更改其密码。 稍后的模块中更详细地介绍了这种情况。

## <a name="various-webparts"></a>各种 Webpart

ASP.NET 2.0 附带了各种 Web 部件。 稍后的模块中将详细介绍这些内容。
