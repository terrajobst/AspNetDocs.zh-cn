---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
title: 了解 ASP.NET AJAX 调试功能 |Microsoft Docs
author: scottcate
description: 调试代码的能力是一项技能，无论开发人员使用哪种技术，每个开发人员都应在其集中中拥有。 许多开发人员 。
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 7f9380c6-19f7-4c82-a019-916ec6dffc9c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
msc.type: authoredcontent
ms.openlocfilehash: 08ced380f3551407d757524dbc84b5feeeb5482b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510860"
---
# <a name="understanding-aspnet-ajax-debugging-capabilities"></a>了解 ASP.NET AJAX 调试功能

作者： [Scott Cate](https://github.com/scottcate)

[下载 PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial06_Debugging_MS_Ajax_Applications_cs.pdf)

> 调试代码的能力是一项技能，无论开发人员使用哪种技术，每个开发人员都应在其集中中拥有。 尽管很多开发人员都习惯使用 Visual Studio .NET 或 Web 开发人员 Express 来调试使用 VB.NET 或C#代码的 ASP.NET 应用程序，但某些开发人员并不知道它对于调试客户端代码（例如 JavaScript）也非常有用。 用于调试 .NET 应用程序的相同类型的技术也可以应用于启用了 AJAX 的应用程序，并且更具体地说就是 ASP.NET AJAX 应用程序。

## <a name="debugging-aspnet-ajax-applications"></a>调试 ASP.NET AJAX 应用程序

Dan Wahlin

调试代码的能力是一项技能，无论开发人员使用哪种技术，每个开发人员都应在其集中中拥有。 这种情况不会说，了解可用的不同调试选项可以节省大量时间，甚至可能会有一些麻烦。 尽管很多开发人员都习惯使用 Visual Studio .NET 或 Web 开发人员 Express 来调试使用 VB.NET 或C#代码的 ASP.NET 应用程序，但某些开发人员并不知道它对于调试客户端代码（例如 JavaScript）也非常有用。 用于调试 .NET 应用程序的相同类型的技术也可以应用于启用了 AJAX 的应用程序，并且更具体地说就是 ASP.NET AJAX 应用程序。

在本文中，你将了解如何使用 Visual Studio 2008 和多个其他工具来调试 ASP.NET AJAX 应用程序，以快速找到 bug 和其他问题。 此讨论将包含有关启用 Internet Explorer 6 或更高版本以进行调试的信息，使用 Visual Studio 2008 和脚本资源管理器可以单步执行代码，并使用其他免费工具（如 Web 开发帮助程序）。 你还将了解如何使用名为 Firebug 的扩展在 Firefox 中调试 ASP.NET AJAX 应用程序，这使你可以在浏览器中直接单步执行 JavaScript 代码，而无需任何其他工具。 最后，你将被引入 ASP.NET AJAX 库中的类，这些类可帮助进行各种调试任务，如跟踪和代码断言语句。

在尝试调试在 Internet Explorer 中查看的页面之前，需要执行几个基本步骤来进行调试。 让我们看看一些需要执行的基本设置要求才能开始使用。

## <a name="configuring-internet-explorer-for-debugging"></a>为调试配置 Internet Explorer

大多数人都不希望查看使用 Internet Explorer 查看网站时遇到的 JavaScript 问题。 事实上，一般用户甚至不知道他们看到错误消息怎么办。 因此，默认情况下，浏览器中的调试选项处于关闭状态。 但是，打开调试并使其在开发新的 AJAX 应用程序时使用非常简单。

若要启用调试功能，请在 Internet Explorer 菜单中转到 "工具" "Internet 选项"，然后选择 "高级" 选项卡。在浏览部分中，确保未选中以下项：

- 禁用脚本调试（Internet Explorer）
- 禁用脚本调试（其他）

尽管不是必需的，但如果你尝试调试应用程序，你可能希望该页中的任何 JavaScript 错误都立即可见且明显。 您可以通过选中 "显示每个脚本错误的通知" 复选框来强制显示所有错误。 尽管这是在开发应用程序时打开的一个不错的选项，但如果你只是浏览其他网站，那么这会很快变得非常麻烦，因为遇到 JavaScript 错误的可能性非常好。

图1显示了 Internet Explorer 高级对话框在正确配置进行调试之后应查看的内容。

[![配置 Internet Explorer 进行调试。](understanding-asp-net-ajax-debugging-capabilities/_static/image2.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image1.png)

**图 1**：配置 Internet Explorer 以进行调试。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image3.png)）

启用调试后，会在 "视图" 菜单中看到一个名为 "脚本调试器" 的新菜单项。 它有两个可用选项，包括在下一条语句中打开和中断。 如果选择 "打开"，系统将提示你在 Visual Studio 2008 中调试页面（请注意，Visual Web Developer Express 还可用于调试）。 如果 Visual Studio .NET 当前正在运行，你可以选择使用该实例或创建一个新的实例。 如果选择了 "在下一语句中断"，则在执行 JavaScript 代码时，系统将提示您调试该页。 如果 JavaScript 代码在页面的 onLoad 事件中执行，则可以刷新页面以触发调试会话。 如果在单击某个按钮后运行 JavaScript 代码，则在单击该按钮后将立即运行调试器。

> [!NOTE]
> 如果在已启用用户访问控制（UAC）的 Windows Vista 上运行，并且已将 Visual Studio 2008 设置为以管理员身份运行，则在系统提示附加时，Visual Studio 将无法附加到该进程。 若要解决此问题，请首先启动 Visual Studio，并使用该实例进行调试。

尽管下一节将演示如何直接从 Visual Studio 2008 内调试 ASP.NET AJAX 页面，但当页面已打开并且你想要对其进行更全面的检查时，使用 Internet Explorer 脚本调试器选项非常有用。

## <a name="debugging-with-visual-studio-2008"></a>用 Visual Studio 2008 进行调试

Visual Studio 2008 提供了世界各地开发人员依赖于日常调试 .NET 应用程序的调试功能。 内置调试器使你可以单步执行代码、查看对象数据、监视特定变量、监视调用堆栈等等。 除了调试 VB.NET 或C#代码以外，调试程序还有助于调试 ASP.NET AJAX 应用程序，并使你能够逐行逐句通过 JavaScript 代码。 下面的详细信息重点介绍可用于调试客户端脚本文件的技术，而不是在使用 Visual Studio 2008 调试应用程序的整个过程中提供 discourse。

在 Visual Studio 2008 中调试页的过程可以通过几种不同的方式启动。 首先，可以使用上一节中提到的 Internet Explorer 脚本调试器选项。 当浏览器中已加载某个页面并且你想要开始调试该页面时，这种方法很有效。 或者，您可以右键单击 "解决方案资源管理器中的 .aspx 页面，然后从菜单中选择" 设为起始页 "。 如果你习惯于调试 ASP.NET 页面，则可能需要先完成此操作。 按 F5 后，可以调试该页。 不过，尽管通常可以在 VB.NET 或C#代码中的任意位置设置断点，但使用 JavaScript 时并不总是如此，因为接下来会看到。

*嵌入脚本与外部脚本*

Visual Studio 2008 调试器将嵌入的 JavaScript 视为不同于外部 JavaScript 文件的页面。 使用外部脚本文件，可以打开文件，并在所选的任何行上设置断点。 通过单击代码编辑器窗口左侧的灰色托盘区域可以设置断点。 如果使用 `<script>` 标记将 JavaScript 直接嵌入到页面中，则不能通过单击灰色纸盒区来设置断点。 尝试在嵌入的脚本行上设置断点将导致警告，指出 "这不是断点的有效位置"。

若要解决此问题，可以将代码移到外部 .js 文件中，并使用 &lt;脚本&gt; 标记的 src 属性引用它：

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample1.html)]

如果将代码移到外部文件中是不是一个选项，或者需要的工作比值得的要多吗？ 尽管不能使用编辑器设置断点，但可以直接将调试器语句添加到要开始调试的代码中。 你还可以使用 ASP.NET AJAX 库中提供的 Sys.databases 类来强制启动调试。 你将在本文稍后部分了解有关 Sys.databases 类的详细信息。

下面是一个使用 `debugger` 关键字的示例。 此示例在调用 update 函数之前强制调试器中断。

**列表1。使用调试器关键字强制使 Visual Studio .NET 调试器中断。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample2.js)]

命中调试器语句后，系统会提示使用 Visual Studio .NET 调试页面，并可以开始逐句通过代码。 在此过程中，你可能会遇到访问页面中使用的 ASP.NET AJAX 库脚本文件的问题，因此，让我们来看看如何使用 Visual Studio。NET 的脚本资源管理器。

## <a name="using-visual-studio-net-windows-to-debug"></a>使用 Visual Studio .NET Windows 调试

启动调试会话并使用默认的 F11 键开始浏览代码后，你可能会遇到如图2所示的错误对话框，除非该页中使用的所有脚本文件都已打开并且可用于调试。

[当没有源代码可用于调试时显示 ![错误对话框。](understanding-asp-net-ajax-debugging-capabilities/_static/image5.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image4.png)

**图 2**：当没有源代码可用于调试时显示的错误对话框。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image6.png)）

显示此对话框的原因是 Visual Studio .NET 不确定如何访问页面引用的某些脚本的源代码。 尽管这可能会非常令人沮丧，但有一个简单的解决方法。 启动调试会话并命中断点后，请访问 Visual Studio 2008 菜单上的 "调试 Windows 脚本资源管理器" 窗口，或使用 Ctrl + Alt + N 热键。

> [!NOTE]
> 如果看不到 "脚本资源管理器" 菜单，请访问 Visual Studio .NET 菜单上的 "**工具**" > **自定义** > **命令**。 在 "类别" 部分中找到 "**调试**" 项，然后单击它以显示所有可用的菜单项。 在 "命令" 列表中，向下滚动到 "脚本资源管理器"，然后将其拖动到前面所述的 "调试 Windows" 菜单上。 这样做会使脚本资源管理器菜单项在每次运行 Visual Studio .NET 时可用。

脚本资源管理器可用于查看页中使用的所有脚本并在代码编辑器中打开它们。 打开脚本资源管理器后，双击当前正在调试的 .aspx 页面，然后在代码编辑器窗口中将其打开。 对脚本资源管理器中显示的所有其他脚本执行相同的操作。 在代码窗口中打开所有脚本后，可以按 F11 键（并使用其他调试热键）来逐步执行代码。 图3显示了脚本资源管理器的示例。 它列出了当前正在调试的文件（Demo）以及两个由 ASP.NET AJAX ScriptManager 动态注入到页面中的自定义脚本和两个脚本。

[![脚本资源管理器可以轻松访问页面中使用的脚本。](understanding-asp-net-ajax-debugging-capabilities/_static/image8.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image7.png)

**图 3**： 使用脚本资源管理器可以轻松访问页面中使用的脚本。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image9.png)）

其他几个窗口还可用于在单步执行页面中的代码时提供有用的信息。 例如，您可以使用 "局部变量" 窗口查看页面中使用的不同变量的值，使用 "即时" 窗口来计算特定变量或条件并查看输出。 你还可以使用 "输出" 窗口查看使用 Sys. trace 函数（将在本文稍后部分介绍）或 Internet Explorer 的 writeln 函数编写的跟踪语句。

当你使用调试器逐句通过代码时，你可以将鼠标悬停在代码中的变量上，以查看它们的分配值。 但是，当你将鼠标悬停在给定的 JavaScript 变量上时，脚本调试器偶尔不会显示任何内容。 若要查看该值，请在代码编辑器窗口中突出显示要尝试查看的语句或变量，然后将鼠标悬停在该窗口中。 虽然这种方法在每种情况下都不起作用，但很多时候都可以看到值，而无需在不同的调试窗口（如 "局部变量" 窗口）中查看。

此处所述的某些功能的视频教程可以[http://www.xmlforasp.net](http://www.xmlforasp.net)查看。

## <a name="debugging-with-web-development-helper"></a>用 Web 开发帮助器进行调试

尽管 Visual Studio 2008 （和 Visual Web Developer Express 2008）是功能强大的调试工具，但也可以使用其他选项，这些选项也更轻。 要发布的最新工具之一是 Web 开发帮助程序。 Microsoft 的 Nikhil Kothari （Microsoft 的一个关键 ASP.NET AJAX 架构师）编写了这种优秀的工具，该工具可以从简单调试执行许多不同的任务来查看 HTTP 请求和响应消息。 Web 开发帮助程序可以[http://projects.nikhilk.net/Projects/WebDevHelper.aspx](http://projects.nikhilk.net/Projects/WebDevHelper.aspx)下载。

Web 开发帮助程序可以直接在 Internet Explorer 中使用，从而使其更易于使用。 它通过从 Internet Explorer 菜单中选择 "工具" Web 开发帮助器来启动。 这将在浏览器的下半部分中打开该工具，因为无需离开浏览器来执行多个任务，如 HTTP 请求和响应消息日志记录。 图4显示了 "操作" 中的 Web 开发帮助器的外观。

[![Web 开发帮助程序](understanding-asp-net-ajax-debugging-capabilities/_static/image11.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image10.png)

**图 4**： Web 开发帮助程序（[单击以查看完全大小的图像](understanding-asp-net-ajax-debugging-capabilities/_static/image12.png)）

Web 开发帮助程序不是一种工具，你将使用它来逐行执行代码，就像 Visual Studio 2008。 不过，可以使用它来查看跟踪输出，轻松地评估脚本中的变量，或浏览数据位于 JSON 对象内部。 这对于查看传递到 ASP.NET AJAX 页和服务器的数据是非常有用的。

在 Internet Explorer 中打开 Web 开发帮助器后，必须通过从 Web 开发帮助器菜单中选择 "脚本启用脚本调试" 来启用脚本调试，如前面的图4所示。 这使工具能够截获在运行页面时出现的错误。 它还允许轻松访问页中输出的跟踪消息。 若要查看跟踪信息或执行脚本命令以测试页中的不同功能，请从 Web 开发帮助器菜单中选择 "脚本显示脚本控制台"。 这样就可以访问命令窗口和简单的即时窗口。

*查看跟踪消息和 JSON 对象数据*

可以使用 "即时" 窗口来执行脚本命令，甚至加载或保存用于在页中测试不同函数的脚本。 "命令" 窗口显示由正在查看的页面写入的跟踪或调试消息。 列表2演示了如何使用 Internet Explorer 的 writeln 函数编写跟踪消息。

**清单2。使用 Debug 类写出客户端跟踪消息。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample3.js)]

如果 LastName 属性包含值 Doe，Web 开发帮助器将在脚本控制台的命令窗口中显示消息 "Person： Doe" （假设已启用调试）。 Web 开发帮助程序还将顶级 debugService 对象添加到可用于写出跟踪信息或查看 JSON 对象内容的页面中。 列表3显示了使用 debugService 类的 trace 函数的示例。

**列表3。使用 Web 开发帮助器的 debugService 类编写跟踪消息。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample4.js)]

DebugService 类的一项不错的功能是，即使在 Internet Explorer 中未启用调试功能，它也可以轻松地在 Web 开发助手运行时始终访问跟踪数据。 当该工具不用于调试页面时，将忽略跟踪语句，因为对 debugService 的调用将返回 false。

DebugService 类还允许使用 Web 开发帮助器的检查器窗口查看 JSON 对象数据。 列表4创建包含 person 数据的简单 JSON 对象。 创建对象后，调用 debugService 类的 "检查函数" 以允许对 JSON 对象进行可视化检查。

**列表4。使用 debugService 函数查看 JSON 对象数据。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample5.js)]

在页中或通过 "即时" 窗口调用 GetPerson （）函数将导致 "对象检查器" 对话框窗口出现，如图5所示。 可以通过突出显示对象中的属性进行动态更改，更改 "值" 文本框中显示的值，然后单击 "更新" 链接。 使用对象检查器可以方便地查看 JSON 对象数据，并尝试对属性应用不同的值。

*调试错误*

除了允许显示跟踪数据和 JSON 对象之外，Web 开发帮助程序还可以帮助调试页面中的错误。 如果遇到错误，系统将提示您继续执行下一行代码或调试脚本（参见图6）。 "脚本错误对话框" 窗口显示了完整的调用堆栈以及行号，以便您可以轻松地识别脚本中的问题。

[![使用 "对象检查器" 窗口查看 JSON 对象。](understanding-asp-net-ajax-debugging-capabilities/_static/image14.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image13.png)

**图 5**：使用对象检查器窗口查看 JSON 对象。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image15.png)）

通过选择 "调试" 选项，您可以直接在 Web 开发帮助器的 "即时" 窗口中执行脚本语句，以查看变量的值、写出 JSON 对象等。 如果再次执行触发错误的相同操作，并且计算机上提供 Visual Studio 2008，则系统将提示您启动调试会话，以便您可以按上一部分所述逐行执行代码行。

[![Web 开发帮助器的脚本错误对话框](understanding-asp-net-ajax-debugging-capabilities/_static/image17.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image16.png)

**图 6**： Web 开发帮助器的脚本错误对话框（[单击以查看完全大小的图像](understanding-asp-net-ajax-debugging-capabilities/_static/image18.png)）

*检查请求和响应消息*

调试 ASP.NET AJAX 页面时，查看页面和服务器之间发送的请求和响应消息通常很有用。 查看消息中的内容可查看是否传递了正确的数据以及消息的大小。 Web 开发帮助程序提供了极佳的 HTTP 消息记录器功能，使你可以轻松地将数据作为原始文本或可读性更强的格式查看。

若要查看 ASP.NET AJAX 请求和响应消息，必须通过从 Web 开发帮助器菜单中选择 "HTTP 启用 HTTP 日志记录" 来启用 HTTP 记录器。 启用后，可以在 HTTP 日志查看器中查看从当前页发送的所有消息，可以通过选择 "HTTP Show HTTP 日志" 进行访问。

尽管查看每个请求/响应消息中发送的原始文本非常有用（并且是 Web 开发帮助器中的一个选项），但通常以更图形的格式查看消息数据通常更容易。 启用 HTTP 日志记录并记录消息后，双击 HTTP 日志查看器中的消息即可查看消息数据。 这样一来，您就可以查看与邮件关联的所有标头以及实际的消息内容。 图7显示了在 "HTTP 日志查看器" 窗口中查看的请求消息和响应消息的示例。

[![使用 HTTP 日志查看器来查看请求和响应消息数据。](understanding-asp-net-ajax-debugging-capabilities/_static/image20.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image19.png)

**图 7**：使用 HTTP 日志查看器查看请求和响应消息数据。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image21.png)）

HTTP 日志查看器自动分析 JSON 对象并使用树视图显示它们，使查看对象的属性数据变得快捷快捷。 当在 ASP.NET AJAX 页中使用 UpdatePanel 时，查看器将消息的每个部分分解为单独的部件，如图8所示。 这是一项很好的功能，与查看原始消息数据相比，此功能可让你更轻松地查看和了解消息中的内容。

[![使用 HTTP 日志查看器查看的 UpdatePanel 响应消息。](understanding-asp-net-ajax-debugging-capabilities/_static/image23.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image22.png)

**图 8**：使用 HTTP 日志查看器查看的 UpdatePanel 响应消息。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image24.png)）

除了 Web 开发帮助器外，还可以使用其他一些工具来查看请求和响应消息。 另一个不错的选择是 Fiddler，可在[http://www.fiddlertool.com](http://www.fiddlertool.com)免费使用。 尽管此处不会讨论 Fiddler，但当你需要全面检查消息标头和数据时，它也是一个不错的选择。

## <a name="debugging-with-firefox-and-firebug"></a>通过 Firefox 和 Firebug 进行调试

尽管 Internet Explorer 仍是最广泛使用的浏览器，但其他浏览器（如 Firefox）已变得非常受欢迎，而且正在使用越来越多的浏览器。 因此，需要在 Firefox 和 Internet Explorer 中查看和调试 ASP.NET AJAX 页面，以确保应用程序正常工作。 虽然 Firefox 无法直接绑定到 Visual Studio 2008 进行调试，但它具有一个名为 Firebug 的扩展，可用于调试页。 可以通过转到[http://www.getfirebug.com](http://www.getfirebug.com)免费下载 Firebug。

Firebug 提供了一个功能完备的调试环境，该环境可用于逐行执行代码，访问在页面内使用的所有脚本，查看 DOM 结构，显示 CSS 样式，甚至跟踪页面中发生的事件。 安装完成后，可以通过从 Firefox 菜单中选择 "工具 Firebug 打开 Firebug" 来访问 Firebug。 与 Web 开发帮助器一样，Firebug 可直接在浏览器中使用，不过它也可以用作独立的应用程序。

Firebug 运行后，无论是否在页面上嵌入脚本，都可以在 JavaScript 文件的任意行上设置断点。 若要设置断点，请首先加载要在 Firefox 中调试的相应页面。 加载页面后，从 Firebug 的脚本下拉列表中选择要调试的脚本。 将显示该页使用的所有脚本。 断点的设置方法是：在 Firebug 的灰色任务栏区域中单击断点应该执行的操作，就像在 Visual Studio 2008 中那样。

在 Firebug 中设置断点后，您可以执行执行需要调试的脚本所需的操作，例如单击按钮或刷新浏览器以触发 onLoad 事件。 在包含断点的行上，执行将自动停止。 图9显示了在 Firebug 中触发的断点的示例。

[![在 Firebug 中处理断点。](understanding-asp-net-ajax-debugging-capabilities/_static/image26.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image25.png)

**图 9**：在 Firebug 中处理断点。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image27.png)）

命中断点后，可以单步执行、逐过程执行或跳出代码，并使用箭头按钮。 单步执行代码时，脚本变量将显示在调试器的右侧部分，允许你查看值和向下钻取到对象。 Firebug 还包含 "调用堆栈" 下拉列表，以查看导致当前正在调试的行的脚本执行步骤。

Firebug 还包括一个控制台窗口，该窗口可用于测试不同的脚本语句、计算变量和查看跟踪输出。 可以通过单击 "Firebug" 窗口顶部的 "控制台" 选项卡访问它。 通过单击 "检查" 选项卡，还可以 "检查要调试的页" 以查看其 DOM 结构和内容。当你将鼠标悬停在检查器窗口中显示的不同 DOM 元素上时，将突出显示页面的相应部分，以便查看在页面中使用元素的位置。 与给定元素关联的属性值可以更改为 "实时"，以试验将不同的宽度、样式等应用到元素。 这是一项不错的功能，使您不必经常在源代码编辑器和 Firefox 浏览器之间切换，以查看简单更改如何影响页面。

图10显示了在页面中使用 DOM 检查器查找名为 txtCountry 的文本框的示例。 Firebug 检查器还可用于查看在页面中使用的 CSS 样式以及发生的事件，例如跟踪鼠标移动、按钮单击等。

[使用 Firebug 的 DOM 检查器 ![。](understanding-asp-net-ajax-debugging-capabilities/_static/image29.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image28.png)

**图 10**：使用 FIREBUG 的 DOM 检查器。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image30.png)）

Firebug 提供了一种轻型方法，可在 Firefox 中直接快速调试页面，并提供一个用于检查页面中不同元素的极佳工具。

## <a name="debugging-support-in-aspnet-ajax"></a>在 ASP.NET AJAX 中调试支持

ASP.NET AJAX 库包含许多不同的类，可用于简化将 AJAX 功能添加到网页中的过程。 您可以使用这些类来查找页面中的元素，并对其进行操作，添加新控件，调用 Web 服务，甚至处理事件。 ASP.NET AJAX 库还包含可用于增强调试页的过程的类。 本部分介绍了 Sys.databases 类，并了解如何在应用程序中使用它。

*使用 Sys.databases 类*

Sys.databases 类（位于 Sys 命名空间中的 JavaScript 类）可用于执行几个不同的功能，包括编写跟踪输出、执行代码断言并强制代码失败，以便可以对其进行调试。 它广泛用于 ASP.NET AJAX 库的调试文件（默认情况下安装在 C:\Program Files\Microsoft ASP. NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0 上）来执行条件测试（称为断言），可确保将参数正确传递给函数，该对象包含所需的数据并写入 trace 语句。

Sys.databases 类公开几个不同的函数，可用于处理跟踪、代码断言或失败，如表1所示。

**表1。Sys.databases 类函数。**

| **函数名** | **描述** |
| --- | --- |
| assert （condition，message，displayCaller） | 断言条件参数为 true。 如果要测试的条件为 false，则将使用消息框来显示消息参数值。 如果 displayCaller 参数为 true，则该方法还会显示有关调用方的信息。 |
| clearTrace() | 从跟踪操作中清除语句输出。 |
| 失败（消息） | 使程序停止执行并中断调试器。 消息参数可用于提供失败的原因。 |
| 跟踪（消息） | 将消息参数写入跟踪输出。 |
| traceDump （object，name） | 以可读格式输出对象的数据。 Name 参数可用于为跟踪转储提供标签。 默认情况下，将写出要转储的对象内的任何子对象。 |

可以使用与 ASP.NET 中提供的跟踪功能大致相同的方式来使用客户端跟踪。 这样，就可以轻松地查看不同的消息，而不会中断应用程序的流动。 列表5显示了使用 Sys.databases 函数写入跟踪日志的示例。 此函数只使用应作为参数写出的消息。

**列表5。使用 Sys. trace 函数。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample6.js)]

如果执行列表5中所示的代码，则不会在页面中看到任何跟踪输出。 查看它的唯一方法是使用 Visual Studio .NET、Web 开发帮助器或 Firebug 中提供的控制台窗口。 如果确实想要在页面中看到跟踪输出，则需要添加一个 TextArea 标记，并为其指定 id TraceConsole，如下所示：

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample7.html)]

页面中的任何 TraceConsole 语句都将写入到区。

如果要查看 JSON 对象中包含的数据，可以使用 Sys.databases 类的 traceDump 函数。 此函数采用两个参数（包括应转储到跟踪控制台的对象）和一个可用于在跟踪输出中标识该对象的名称。 列表6显示了使用 traceDump 函数的示例。

**清单6。使用 traceDump 函数。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample8.js)]

图11显示了如何调用 traceDump 函数的输出。 请注意，除编写 Person 对象的数据外，还会写出地址子对象的数据。

除了跟踪，Sys.databases 类还可用于执行代码断言。 断言用于测试应用程序运行时是否满足特定的条件。 ASP.NET AJAX 库脚本的调试版本包含多个断言语句来测试各种条件。

列表7显示了使用 Sys.databases 函数测试条件的示例。 此代码测试在更新 Person 对象之前地址对象是否为 null。

[traceDump 函数的 ![输出。](understanding-asp-net-ajax-debugging-capabilities/_static/image32.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image31.png)

**图 11**： traceDump 函数的输出。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image33.png)）

**列表7。使用 debug 函数。**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample9.js)]

将传递三个参数，包括要计算的条件、断言返回 false 时要显示的消息，以及是否应显示有关调用方的信息。 如果断言失败，则在第三个参数为 true 时将显示消息以及调用方信息。 图12显示了在列表7中显示的断言失败时显示的失败对话框的示例。

要覆盖的最终函数为 Sys.databases。失败。 如果要强制代码在脚本中的特定行上失败，则可以添加一个 Sys.databases. fail 调用，而不是通常在 JavaScript 应用程序中使用的调试器语句。 Sys. fail 函数接受一个字符串参数，该参数表示失败的原因，如下所示：

[!code-css[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample10.css)]

[![Sys.databases 失败消息。](understanding-asp-net-ajax-debugging-capabilities/_static/image35.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image34.png)

**图 12**：一个 sys.databases 失败消息。  （[单击以查看完全大小的映像](understanding-asp-net-ajax-debugging-capabilities/_static/image36.png)）

当执行脚本时，如果遇到 Sys.databases 语句，消息参数的值将显示在调试应用程序（如 Visual Studio 2008）的控制台中，系统将提示您调试应用程序。 这种方法非常有用的一种情况是，当你无法在内联脚本上使用 Visual Studio 2008 设置断点，但要在特定行上停止代码，以便你可以检查变量的值。

*了解 ScriptManager 控件的 ScriptMode 属性*

ASP.NET AJAX 库包含在 C:\Program Files\Microsoft ASP. NET\ASP.NET 2.0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0 上安装的调试和发布脚本版本。 调试脚本格式良好、易于读取，并在各个版本中分散多个 Sys.databases 调用，而发布脚本则去掉空格并使用 Sys.databases 类来最大程度地减小其整体大小。

添加到 ASP.NET AJAX 页面的 ScriptManager 控件在 web.config 中读取编译元素的 debug 特性，以确定要加载的库脚本的版本。 但是，你可以通过更改 ScriptMode 属性来控制是否加载调试或发布脚本（库脚本或你自己的自定义脚本）。 ScriptMode 接受其成员包括自动、调试、发布和继承的 ScriptMode 枚举。

ScriptMode 默认为 "自动"，这意味着 ScriptManager 将检查 web.config 中的调试属性。当 debug 为 false 时，ScriptManager 将加载 ASP.NET 的发布版本。 当 debug 为 true 时，将加载脚本的调试版本。 将 ScriptMode 属性更改为 Release 或 Debug 将强制 ScriptManager 加载相应的脚本，而不考虑 Debug 属性在 web.config 中具有什么值。列表8显示了使用 ScriptManager 控件从 ASP.NET AJAX 库加载调试脚本的示例。

**列表8。使用 ScriptManager 加载调试脚本**。

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample11.aspx)]

你还可以通过使用 ScriptManager 的 "脚本" 属性以及 ScriptReference 组件来加载你自己的自定义脚本的不同版本（"调试" 或 "发布"），如列表9所示。

**列表9。使用 ScriptManager 加载自定义脚本。**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample12.aspx)]

> [!NOTE]
> 如果使用 ScriptReference 组件加载自定义脚本，则必须通过在脚本底部添加以下代码，在脚本完成加载时通知 ScriptManager：

[!code-csharp[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample13.cs)]

列表9中所示的代码告诉 ScriptManager 查找 Person 脚本的调试版本，使其能够自动查找 person. node.js 而不是 Person。 如果找不到 Person. node.js 文件，将引发错误。

如果希望基于 ScriptManager 控件上设置的 ScriptMode 属性值加载自定义脚本的调试或发布版本，可以将 ScriptReference 控件的 ScriptMode 属性设置为 "继承"。 这将导致根据 ScriptManager 的 ScriptMode 属性加载适当版本的自定义脚本，如列表10所示。 由于 ScriptManager 控件的 "ScriptMode" 属性设置为 "调试"，因此将在页面中加载并使用 "Person" 脚本。

**列表10。从 ScriptManager 继承自定义脚本的 ScriptMode。**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample14.aspx)]

通过适当地使用 ScriptMode 属性，你可以更轻松地调试应用程序并简化整个过程。 由于在调试脚本专门用于调试目的时删除了代码格式，因此 ASP.NET AJAX 库的发布脚本比较难完成。

## <a name="conclusion"></a>结束语

Microsoft 的 ASP.NET AJAX 技术为构建支持 AJAX 的应用程序提供了坚实的基础，可增强最终用户的整体体验。 但是，与任何编程技术一样，bug 和其他应用程序问题肯定会发生。 了解可用的不同调试选项可节省大量时间，并导致产品更稳定。

在本文中，已介绍了几种不同的方法，可用于调试 ASP.NET AJAX 页面，包括带有 Visual Studio 2008、Web 开发帮助程序和 Firebug 的 Internet Explorer。 由于可以访问变量数据、逐行浏览代码和查看跟踪语句，因此这些工具可简化整体调试过程。 除了讨论的不同调试工具外，还了解了如何在应用程序中使用 ASP.NET AJAX 库的 Sys.databases 类，以及如何使用 ScriptManager 类来加载脚本的调试或发布版本。

## <a name="bio"></a>Bio

Dan Wahlin （Microsoft 最有价值专家，适用于 ASP.NET 和 XML Web 服务）是一个 .NET 开发讲师和体系结构顾问，位于界面技术培训（[www.interfacett.com）](http://www.interfacett.com)。 Dan 构建了 ASP.NET 开发人员网站（[www.XMLforASP.NET](http://www.XMLforASP.NET)）的 XML，位于 INETA 演讲者的局上，并发表了几个会议。 Dan 共同创作的专业 Windows 责任（Wrox）、ASP.NET：提示、教程和代码（Sams）、ASP.NET 1.1 有问必答解决方案、专业 ASP.NET 2.0 AJAX （Wrox）、ASP.NET 2.0 MVP 黑客和为 ASP.NET 开发人员编写的 XML （Sams）。 当他不编写代码、文章或书籍时，Dan 喜欢撰写和录制音乐，并通过他的妻子和孩子玩高尔夫和篮球。

Scott Cate 一直在使用 Microsoft Web 技术，因为1997，是 myKB.com （[www.myKB.com](http://www.myKB.com)）的总裁，他致力于编写基于知识库软件解决方案的基于 ASP.NET 的应用程序。 可以通过电子邮件联系 Scott [scott.cate@myKB.com](mailto:scott.cate@myKB.com)或[ScottCate.com](http://ScottCate.com)上的博客

> [!div class="step-by-step"]
> [上一页](understanding-asp-net-ajax-web-services.md)
