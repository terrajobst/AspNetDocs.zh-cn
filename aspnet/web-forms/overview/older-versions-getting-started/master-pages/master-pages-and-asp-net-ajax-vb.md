---
uid: web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-vb
title: 母版页和 ASP.NET AJAX （VB） |Microsoft Docs
author: rick-anderson
description: 讨论使用 ASP.NET AJAX 和母版页的选项。 查看使用 ScriptManagerProxy 类;讨论如何加载各种 JS 文件 dependi
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 0ee9318c-29bb-4d58-b1dc-94e575b8ae10
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-vb
msc.type: authoredcontent
ms.openlocfilehash: 7be4ff422b91321ff83ed1f1c731c9a0bfe768f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78421814"
---
# <a name="master-pages-and-aspnet-ajax-vb"></a>母版页和 ASP.NET AJAX (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_08_VB.zip)或[下载 PDF](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_08_VB.pdf)

> 讨论使用 ASP.NET AJAX 和母版页的选项。 查看使用 ScriptManagerProxy 类;讨论如何加载各种 JS 文件，具体取决于是否在母版页或内容页中使用了 ScriptManager。

## <a name="introduction"></a>简介

过去几年来，越来越多的开发人员构建了支持 AJAX 的 web 应用程序。 启用了 AJAX 的网站使用多种相关的 web 技术来提供更具响应能力的用户体验。 由于 Microsoft 的 ASP.NET AJAX framework，创建启用 AJAX 的 ASP.NET 应用程序非常容易极为。 ASP.NET AJAX 内置于 ASP.NET 3.5 和 Visual Studio 2008;它还可作为 ASP.NET 2.0 应用程序的单独下载提供。

使用 ASP.NET AJAX framework 生成启用了 AJAX 的网页时，必须将一个 ScriptManager 控件精确添加到使用该框架的每个页面。 顾名思义，ScriptManager 管理启用了 AJAX 的网页中使用的客户端脚本。 ScriptManager 至少会发出 HTML，指示浏览器下载构成 ASP.NET AJAX 客户端库的 JavaScript 文件。 它还可用于注册自定义 JavaScript 文件、启用脚本的 web 服务以及自定义应用程序服务功能。

如果你的网站使用的是母版页（如应有），则不一定需要将 ScriptManager 控件添加到每个单个内容页;相反，可以向母版页添加 ScriptManager 控件。 本教程演示如何将 ScriptManager 控件添加到母版页。 还介绍了如何使用 ScriptManagerProxy 控件在特定内容页中注册自定义脚本和脚本服务。

> [!NOTE]
> 本教程不会探讨如何通过 ASP.NET AJAX framework 设计或构建支持 AJAX 的 web 应用程序。 有关使用 AJAX 的详细信息，请参阅 ASP.NET AJAX 视频和教程，以及本教程末尾的其他阅读部分中列出的那些资源。

## <a name="examining-the-markup-emitted-by-the-scriptmanager-control"></a>检查 ScriptManager 控件发出的标记

ScriptManager 控件发出标记，指示浏览器下载构成 ASP.NET AJAX 客户端库的 JavaScript 文件。 它还会将一些内联 JavaScript 添加到初始化此库的页面。 以下标记显示了添加到包含 ScriptManager 控件的页面的呈现输出的内容：

[!code-html[Main](master-pages-and-asp-net-ajax-vb/samples/sample1.html)]

`<script src="url"></script>` 标记指示浏览器下载并执行*url*处的 JavaScript 文件。 ScriptManager 发出三个此类标记;一个引用 `WebResource.axd`文件，另一个引用文件 `ScriptResource.axd`。 这些文件实际上并不作为文件存在于你的网站中。 相反，当对其中任一文件的请求到达 web 服务器时，ASP.NET 引擎会检查 querystring 并返回相应的 JavaScript 内容。 这三个外部 JavaScript 文件提供的脚本构成了 ASP.NET AJAX framework 的客户端库。 ScriptManager 发出的其他 `<script>` 标记包含用于初始化此库的内联脚本。

ScriptManager 发出的外部脚本引用和内联脚本对于使用 ASP.NET AJAX framework 的页面是必不可少的，但对于不使用框架的页面不是必需的。 因此，您可能会因为仅将 ScriptManager 添加到使用 ASP.NET AJAX framework 的页面。 这就足够了，但如果您有许多使用该框架的页面，最终会将 ScriptManager 控件添加到所有页面中，这是一个重复的任务。 或者，你可以将 ScriptManager 添加到母版页，然后将此必要的脚本注入到所有内容页。 使用此方法时，无需记得将 ScriptManager 添加到使用 ASP.NET AJAX framework 的新页面，因为该页面已经包含在母版页中。 步骤1演练如何向母版页添加 ScriptManager。

> [!NOTE]
> 如果你计划在母版页的用户界面中包含 AJAX 功能，则不会有任何选择，因为你必须在母版页中包含 ScriptManager。

将 ScriptManager 添加到母版页的一个缺点是，上面的脚本将在*每个*页面中发出，无论其是否需要。 这显然会导致这些页面的带宽浪费在包含 ScriptManager （通过母版页）的页面上，但不会使用 ASP.NET AJAX framework 的任何功能。 但只是浪费了多少带宽呢？

- ScriptManager 所发出的实际内容（如上所示）的总计超过1KB。
- 但 `<script>` 元素所引用的三个外部脚本文件，只包含未压缩的数据的 450KB;在使用 gzip 压缩的网站中，可以降低100KB 的总带宽。 但是，浏览器会缓存这些脚本文件一年，这意味着它们只需下载一次，然后在站点的其他页面上重复使用。

在最佳情况下，当缓存脚本文件时，总开销为1KB，这是可忽略的。 然而，在最坏的情况下，这种情况下，这种情况下，如果脚本文件尚未下载并且 web 服务器不使用任何形式的压缩，则带宽命中率为450KB，它可以将宽带连接上的一个或两个位置添加到长达一分钟的 通过拨号调制解调器的用户。 好消息是因为外部脚本文件由浏览器进行缓存，所以这种最坏的情况很少出现。

> [!NOTE]
> 如果您仍不舒服将 ScriptManager 控件置于母版页中，请考虑 Web 窗体（母版页中 `<form runat="server">` 标记）。 使用回发模型的每个 ASP.NET 页必须精确包含一个 Web 窗体。 添加 Web 窗体后，会添加其他内容：多个隐藏的窗体字段、`<form>` 标记本身，以及用于从脚本启动回发的 JavaScript 函数（如有必要）。 不回发的页面不需要此标记。 通过从母版页中删除 Web 窗体，然后将其手动添加到每个需要的内容页，可以消除此无关标记。 不过，使 Web 窗体在母版页中的好处比不必要地将其添加到某些内容页中的缺点要大一些。

## <a name="step-1-adding-a-scriptmanager-control-to-the-master-page"></a>步骤1：向母版页添加 ScriptManager 控件

使用 ASP.NET AJAX framework 的每个网页必须精确包含一个 ScriptManager 控件。 由于这一要求，通常可以将单个 ScriptManager 控件置于母版页上，以便所有内容页都自动包含 ScriptManager 控件。 此外，ScriptManager 必须位于 ASP.NET AJAX 服务器控件之前，如 UpdatePanel 和 UpdateProgress 控件。 因此，最好将 ScriptManager 置于 Web 窗体中的任何 ContentPlaceHolder 控件之前。

打开 `Site.master` 母版页，并将 ScriptManager 控件添加到 Web 窗体中的页面，而不是添加到 `<div id="topContent">` 元素之前（参见图1）。 如果使用 Visual Web Developer 2008 或 Visual Studio 2008，则 ScriptManager 控件位于 "AJAX 扩展" 选项卡的 "工具箱" 中。如果使用的是 Visual Studio 2005，则需要首先安装 ASP.NET AJAX framework 并将控件添加到 "工具箱"。 请访问 ASP.NET AJAX 下载页，获取 ASP.NET 2.0 的框架。

将 ScriptManager 添加到页面后，将其 `ID` 从 "`ScriptManager1`" 更改为 "`MyManager`"。

[![将 ScriptManager 添加到母版页](master-pages-and-asp-net-ajax-vb/_static/image2.png)](master-pages-and-asp-net-ajax-vb/_static/image1.png)

**图 01**：向母版页添加 ScriptManager （[单击以查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image3.png)）

## <a name="step-2-using-the-aspnet-ajax-framework-from-a-content-page"></a>步骤2：使用内容页中的 ASP.NET AJAX Framework

将 ScriptManager 控件添加到母版页后，现在可以在任何内容页中添加 ASP.NET AJAX framework 功能。 让我们创建一个新的 ASP.NET 页面，用于显示 Northwind 数据库中随机选择的产品。 我们将使用 ASP.NET AJAX framework 的计时器控件每15秒更新一次显示，并显示新产品。

首先在名为 `ShowRandomProduct.aspx`的根目录中创建一个新页面。 别忘了将此新页绑定到 `Site.master` 母版页。

[![将新的 ASP.NET 页面添加到网站](master-pages-and-asp-net-ajax-vb/_static/image5.png)](master-pages-and-asp-net-ajax-vb/_static/image4.png)

**图 02**：向网站添加新的 "ASP.NET" 页（[单击以查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image6.png)）

请注意，在母版页中指定标题、Meta 标记和其他 HTML 标头 [SKM1] 教程中，我们创建了一个名为 `BasePage` 的自定义基类类，如果未显式设置该页面的标题，则生成该页面的标题。 转到 "`ShowRandomProduct.aspx`" 页的代码隐藏类，并使其从 `BasePage` （而不是从 `System.Web.UI.Page`）派生。

最后，更新 `Web.sitemap` 文件以包含本课中的条目。 将以下标记添加到 "母版页到内容" 页面交互课程的 `<siteMapNode>` 下面：

[!code-xml[Main](master-pages-and-asp-net-ajax-vb/samples/sample2.xml)]

此 `<siteMapNode>` 元素的添加将反映在课程列表中（见图5）。

### <a name="displaying-a-randomly-selected-product"></a>显示随机选择的产品

返回 `ShowRandomProduct.aspx`。 从设计器中，将 "UpdatePanel" 控件从 "工具箱" 拖动到 `MainContent` 内容控件，并将其 `ID` 属性设置为 "`ProductPanel`"。 UpdatePanel 表示屏幕上可通过部分页面回发异步更新的区域。

我们的第一个任务是在 UpdatePanel 内显示有关随机选择的产品的信息。 首先，将 DetailsView 控件拖到 UpdatePanel 中。 将 DetailsView 控件的 `ID` 属性设置为 `ProductInfo` 并清除其 `Height` 和 `Width` 属性。 展开 DetailsView 的智能标记，然后从 "选择数据源" 下拉列表中，选择将 DetailsView 绑定到名为 `RandomProductDataSource`的新 SqlDataSource 控件。

[![将 DetailsView 绑定到新的 SqlDataSource 控件](master-pages-and-asp-net-ajax-vb/_static/image8.png)](master-pages-and-asp-net-ajax-vb/_static/image7.png)

**图 03**：将 DetailsView 绑定到新的 SqlDataSource 控件（[单击以查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image9.png)）

将 SqlDataSource 控件配置为通过 "内容" 页上的 "与母版页交互" [SKM2] 教程中创建的 `NorthwindConnectionString` 连接到 Northwind 数据库。 配置 select 语句时，请选择指定自定义 SQL 语句，然后输入以下查询：

[!code-sql[Main](master-pages-and-asp-net-ajax-vb/samples/sample3.sql)]

`SELECT` 子句中的 `TOP 1` 关键字只返回查询返回的第一条记录。 `NEWID()` 函数将生成一个新的全局唯一标识符值（GUID），并可以在 `ORDER BY` 子句中使用，以随机顺序返回表的记录。

[![配置 SqlDataSource 以返回单个随机选择的记录](master-pages-and-asp-net-ajax-vb/_static/image11.png)](master-pages-and-asp-net-ajax-vb/_static/image10.png)

**图 04**：配置 SqlDataSource 以返回单个随机选择的记录（[单击以查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image12.png)）

完成向导后，Visual Studio 将为上述查询返回的两个列创建一个 BoundField。 此时，页面的声明性标记应如下所示：

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample4.aspx)]

图5显示了通过浏览器查看 `ShowRandomProduct.aspx` 页面。 单击浏览器的 "刷新" 按钮以重新加载页面;应该会看到一个新的随机选定记录的 `ProductName` 和 `UnitPrice` 值。

[显示 ![随机产品的名称和价格](master-pages-and-asp-net-ajax-vb/_static/image14.png)](master-pages-and-asp-net-ajax-vb/_static/image13.png)

**图 05**：显示随机产品的名称和价格（[单击查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image15.png)）

### <a name="automatically-displaying-a-new-product-every-15-seconds"></a>每15秒自动显示新产品

ASP.NET AJAX 框架包含一个 Timer 控件，该控件在指定时间执行回发;回发时，引发计时器的 `Tick` 事件。 如果计时器控件置于 UpdatePanel 内，则会触发部分页面回发，在此期间，我们可以将数据重新绑定到 DetailsView，以显示新的随机选择的产品。

若要实现此目的，请将计时器从工具箱拖放到 UpdatePanel 中。 将计时器的 `ID` 从 `Timer1` 更改为 `ProductTimer`，并将其 `Interval` 属性从60000更改为15000。 `Interval` 属性指示回发之间的毫秒数;将其设置为15000将导致计时器每15秒触发部分页面回发。 此时，计时器的声明性标记应如下所示：

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample5.aspx)]

为计时器的 `Tick` 事件创建事件处理程序。 在此事件处理程序中，需要通过调用 DetailsView 的 `DataBind` 方法将数据重新绑定到 DetailsView。 这样做会指示 DetailsView 重新检索其数据源控件中的数据，这将选择并显示新的随机选择的记录（就像通过单击浏览器的 "刷新" 按钮重新加载页面时）。

[!code-vb[Main](master-pages-and-asp-net-ajax-vb/samples/sample6.vb)]

就这么简单！ 通过浏览器重新访问页面。 最初，将显示随机产品的信息。 如果你耐心观看屏幕，你会注意到，在15秒后，有关新产品的信息会神奇地替换现有的显示内容。

为了更好地了解此处发生的情况，让我们将 "标签" 控件添加到 UpdatePanel，以显示上次更新显示的时间。 在 UpdatePanel 中添加标签 Web 控件，将其 `ID` 设置为 `LastUpdateTime`，并清除其 `Text` 属性。 接下来，为 UpdatePanel 的 `Load` 事件创建事件处理程序，并在标签中显示当前时间。 （UpdatePanel 的 `Load` 事件将在每次完全或部分页面回发时触发。）

[!code-vb[Main](master-pages-and-asp-net-ajax-vb/samples/sample7.vb)]

完成此更改后，页面将包括当前显示的产品的加载时间。 图6显示第一次访问的页面。 图7稍后显示了15秒的时间段，在计时器控件具有 "勾选" 后，UpdatePanel 已刷新以显示有关新产品的信息。

[![随机选择的产品显示在页面加载上](master-pages-and-asp-net-ajax-vb/_static/image17.png)](master-pages-and-asp-net-ajax-vb/_static/image16.png)

**图 06**：随机选择的产品显示在页面加载上（[单击以查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image18.png)）

[每15秒 ![显示一个新随机选择的产品](master-pages-and-asp-net-ajax-vb/_static/image20.png)](master-pages-and-asp-net-ajax-vb/_static/image19.png)

**图 07**：显示新随机选择的产品的每15秒（[单击以查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image21.png)）

## <a name="step-3-using-the-scriptmanagerproxy-control"></a>步骤3：使用 ScriptManagerProxy 控件

除了包括 ASP.NET AJAX framework 客户端库所需的脚本外，ScriptManager 还可以注册自定义 JavaScript 文件、对启用脚本的 Web 服务的引用以及自定义的身份验证、授权和配置文件服务。 通常，此类自定义项特定于某个页面。 但是，如果自定义脚本文件、Web 服务引用、身份验证、授权或配置文件服务在母版页的 ScriptManager 中被引用，则它们将包含在网站的所有页面中。

若要逐页添加 ScriptManager 相关自定义项，请使用 ScriptManagerProxy 控件。 你可以将 ScriptManagerProxy 添加到内容页，然后从 ScriptManagerProxy 注册自定义 JavaScript 文件、Web 服务引用、身份验证、授权或配置文件服务;这就是为特定内容页注册这些服务的效果。

> [!NOTE]
> ASP.NET 页只能有一个 ScriptManager 控件存在。 因此，如果已在母版页中定义了 ScriptManager 控件，则无法将 ScriptManager 控件添加到内容页中。 ScriptManagerProxy 的唯一目的是提供一种方法，使开发人员能够在母版页中定义 ScriptManager，但仍可以逐页添加 ScriptManager 自定义项。

若要查看 ScriptManagerProxy 控件的操作，请在 `ShowRandomProduct.aspx` 中增加 UpdatePanel，使其包含一个按钮，该按钮使用客户端脚本来暂停或继续计时器控件。 计时器控件具有三个可用于实现所需功能的客户端方法：

- `_startTimer()`-启动计时器控件
- `_raiseTick()`-使计时器控件 "计时"，从而在服务器上回发并引发其 Tick 事件
- `_stopTimer()`-停止计时器控件

让我们创建一个 JavaScript 文件，其中包含一个名为 `timerEnabled` 的变量和一个名为 `ToggleTimer`的函数。 `timerEnabled` 变量指示当前是启用还是禁用计时器控件;默认值为 true。 `ToggleTimer` 函数接受两个输入参数：对计时器控件的 "暂停/继续" 按钮和客户端 `id` 值的引用。 此函数会切换 `timerEnabled`的值、获取对计时器控件的引用、启动或停止计时器（具体取决于 `timerEnabled`的值），并将按钮的显示文本更新为 "暂停" 或 "恢复"。 只要单击 "暂停/继续" 按钮，就会调用此函数。

首先在名为 `Scripts`的网站中创建一个新文件夹。 接下来，将新文件添加到类型为 JScript 文件的名为 `TimerScript.js` 的 Scripts 文件夹中。

[![将新的 JavaScript 文件添加到 Scripts 文件夹](master-pages-and-asp-net-ajax-vb/_static/image23.png)](master-pages-and-asp-net-ajax-vb/_static/image22.png)

**图 08**：将新的 JavaScript 文件添加到 `Scripts` 文件夹（[单击查看完全大小的映像](master-pages-and-asp-net-ajax-vb/_static/image24.png)）

[已将新的 JavaScript 文件添加到网站 ![](master-pages-and-asp-net-ajax-vb/_static/image26.png)](master-pages-and-asp-net-ajax-vb/_static/image25.png)

**图 09**：已将新的 JavaScript 文件添加到网站（[单击查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image27.png)）

接下来，将以下脚本添加到 `TimerScript.js` 文件：

[!code-csharp[Main](master-pages-and-asp-net-ajax-vb/samples/sample8.cs)]

现在，我们需要在 `ShowRandomProduct.aspx`中注册此自定义 JavaScript 文件。 返回到 `ShowRandomProduct.aspx` 并向页面添加 ScriptManagerProxy 控件;将其 `ID` 设置为 `MyManagerProxy`。 若要注册自定义 JavaScript 文件，请在设计器中选择 "ScriptManagerProxy" 控件，然后执行属性窗口。 其中一个属性的标题为 "脚本"。 选择此属性将显示如图10所示的 ScriptReference 集合编辑器。 单击 "添加" 按钮以添加新的脚本引用，然后在 "路径" 属性： "`~/Scripts/TimerScript.js`中输入脚本文件的路径。

[![将脚本引用添加到 ScriptManagerProxy 控件](master-pages-and-asp-net-ajax-vb/_static/image29.png)](master-pages-and-asp-net-ajax-vb/_static/image28.png)

**图 10**：向 ScriptManagerProxy 控件添加脚本引用（[单击查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image30.png)）

添加脚本引用后，将更新 ScriptManagerProxy 控件的声明性标记，使其包含一个具有单个 `ScriptReference` 条目的 `<Scripts>` 集合，如以下标记片段所示：

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample9.aspx)]

`ScriptReference` 项指示 ScriptManagerProxy 在其呈现的标记中包含对 JavaScript 文件的引用。 也就是说，通过将自定义脚本注册到 ScriptManagerProxy 中，`ShowRandomProduct.aspx` 页面呈现的输出现在包含另一个 `<script src="url"></script>` 标记： `<script src="Scripts/TimerScript.js" type="text/javascript"></script>`。

现在，我们可以从 "`ShowRandomProduct.aspx`" 页中的客户端脚本调用在 `TimerScript.js` 中定义的 `ToggleTimer` 函数。 在 UpdatePanel 中添加以下 HTML：

[!code-aspx[Main](master-pages-and-asp-net-ajax-vb/samples/sample10.aspx)]

这会显示一个带有文本 "Pause" 的按钮。 只要单击该按钮，就会调用 JavaScript 函数 `ToggleTimer`，同时传递对该按钮的引用和 Timer 控件的 `id` 值（`ProductTimer`）。 请注意用于获取计时器控件的 `id` 值的语法。 `<%=ProductTimer.ClientID%>` 发出 `ProductTimer` 计时器控件 `ClientID` 属性的值。 在内容页中的控件 ID 命名 [SKM3] 教程中，我们讨论了服务器端 `ID` 值和生成的客户端 `id` 值之间的差异，以及 `ClientID` 如何返回客户端 `id`。

图11：首次通过浏览器访问时显示此页。 计时器当前正在运行，每15秒更新一次显示的产品信息。 图12在单击 "暂停" 按钮后显示屏幕。 单击 "暂停" 按钮将停止计时器，并将该按钮的文本更新为 "Resume"。 用户单击 "继续" 后，将刷新产品信息（并每15秒刷新一次）。

[![单击 "暂停" 按钮停止计时器控件](master-pages-and-asp-net-ajax-vb/_static/image32.png)](master-pages-and-asp-net-ajax-vb/_static/image31.png)

**图 11**：单击 "暂停" 按钮以停止计时器控件（[单击以查看完全大小的图像](master-pages-and-asp-net-ajax-vb/_static/image33.png)）

[![单击 "继续" 按钮重新启动计时器](master-pages-and-asp-net-ajax-vb/_static/image35.png)](master-pages-and-asp-net-ajax-vb/_static/image34.png)

**图 12**：单击 "继续" 按钮以重新启动计时器（[单击以查看完全大小的映像](master-pages-and-asp-net-ajax-vb/_static/image36.png)）

## <a name="summary"></a>摘要

使用 ASP.NET AJAX framework 生成启用 AJAX 的 web 应用程序时，必须确保每个启用 AJAX 的网页都包含 ScriptManager 控件。 为简化此过程，我们可以将 ScriptManager 添加到母版页，而不必记得向每个内容页添加 ScriptManager。 步骤1说明了如何将 ScriptManager 添加到母版页，步骤2中介绍了如何实现内容页中的 AJAX 功能。

如果需要向特定内容页添加自定义脚本、对启用了脚本的 Web 服务的引用或者自定义的身份验证、授权或配置文件服务，请将 ScriptManagerProxy 控件添加到内容页，然后配置自定义。 步骤3检查了如何使用 ScriptManagerProxy 在特定内容页中注册自定义 JavaScript 文件。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET AJAX Framework](../../../../ajax/index.md)
- [ASP.NET AJAX 教程](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)
- [ASP.NET AJAX 视频](../../../videos/aspnet-ajax/index.md)
- [Microsoft ASP.NET AJAX 构建交互式用户界面](http://aspnet.4guysfromrolla.com/articles/101007-1.aspx)
- [使用 NEWID 对记录进行随机排序](http://www.sqlteam.com/article/using-newid-to-randomly-sort-records)
- [使用计时器控件](http://aspnet.4guysfromrolla.com/articles/061808-1.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](interacting-with-the-content-page-from-the-master-page-vb.md)
> [下一页](specifying-the-master-page-programmatically-vb.md)
