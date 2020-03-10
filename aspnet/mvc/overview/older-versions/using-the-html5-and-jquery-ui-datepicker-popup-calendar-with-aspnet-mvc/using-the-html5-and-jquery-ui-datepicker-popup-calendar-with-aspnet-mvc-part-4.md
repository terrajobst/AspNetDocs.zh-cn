---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: 将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC-第4部分一起使用 |Microsoft Docs
author: Rick-Anderson
description: 本教程将指导你了解如何在 ASP.NET MV ... 中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 583e782641efea9a9517edb31f7718b28203d756
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433250"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>将 HTML5 和 jQuery UI Datepicker 快捷日历与 ASP.NET MVC 一起使用-第4部分

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 本教程将指导你了解如何在 ASP.NET MVC Web 应用程序中使用编辑器模板、显示模板和 jQuery UI datepicker 快捷日历。

### <a name="adding-a-template-for-editing-dates"></a>添加用于编辑日期的模板

在本节中，你将创建一个用于编辑日期的模板，当 ASP.NET MVC 显示用于编辑模型属性的 UI 时，该模板将标记为[数据类型](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)属性的**日期**枚举。 模板将只呈现日期;不会显示时间。 在模板中，你将使用[JQUERY UI Datepicker](http://jqueryui.com/demos/datepicker/)快捷日历来提供编辑日期的方法。

若要开始，请打开*Movie.cs*文件，并将包含**日期**枚举的[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx)特性添加到 `ReleaseDate` 属性，如以下代码所示：

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

此代码将导致显示 "`ReleaseDate`" 字段，而不会在显示模板和编辑模板中显示时间。 如果你的应用程序在*Views\Shared\EditorTemplates*文件夹或*Views\Movies\EditorTemplates*文件夹中包含一个*日期 cshtml*模板，则该模板将用于在编辑时呈现任何 `DateTime` 属性。 否则，内置 ASP.NET 模板系统将以日期形式显示属性。

按 Ctrl+F5 以运行应用程序。 选择 "编辑" 链接以验证 "发布日期" 的输入字段是否只显示日期。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

在**解决方案资源管理器**中，展开 " *Views* " 文件夹，展开*共享*文件夹，然后右键单击*Views\Shared\EditorTemplates*文件夹。

单击 "**添加**"，然后单击 "**查看**"。 将显示 "**添加视图**" 对话框。

在 "**视图名称**" 框中，键入 &quot;Date&quot;。

选中 "**作为分部视图创建**" 复选框。 请确保未选中 "**使用布局或母版页**" 和 "**创建强类型视图**" 复选框。

单击 **“添加”** 。 将创建*Views\Shared\EditorTemplates\Date.cshtml*模板。

将以下代码添加到*Views\Shared\EditorTemplates\Date.cshtml*模板。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

第一行将模型声明为 `DateTime` 类型。 尽管不需要在 "编辑" 和 "显示模板" 中声明模型类型，但这是一种最佳做法，以便您可以对要传递到视图的模型进行编译时检查。 （另一个优点是，你可以在 Visual Studio 的视图中获取模型的 IntelliSense。）如果未声明模型类型，则 ASP.NET MVC 会将其视为[动态](https://msdn.microsoft.com/library/dd264741.aspx)类型，并且不会进行编译时类型检查。 如果将模型声明为 `DateTime` 类型，则它将成为强类型。

第二行只是文本 HTML 标记，该标记显示在日期字段之前使用日期模板&quot; &quot;。 你将暂时使用此行来验证是否正在使用此日期模板。

下一行是一个[Html. TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx)帮助器，用于呈现一个文本框 `input` 字段。 帮助器的第三个参数使用匿名类型将文本框的类设置为要 `datefield` 的类型和要 `date`的类型。 （由于 `class` 是中C#的保留的，因此需要使用 `@` 字符来转义C#分析器中的 `class` 特性。）

"`date` 类型" 是一种 HTML5 输入类型，可用于启用 HTML5 感知浏览器来呈现 HTML5 日历控件。 稍后，你将使用 `datefield` 类添加一些 JavaScript，以将 jQuery datepicker 挂钩到 `Html.TextBox` 元素。

按 Ctrl+F5 以运行应用程序。 您可以验证 "编辑" 视图中的 "`ReleaseDate`" 属性是否正在使用编辑模板，因为模板显示 &quot;使用日期模板&quot; 紧靠 `ReleaseDate` 文本输入框之前，如下图所示：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

在浏览器中查看页面的源。 （例如，右键单击该页并选择 "**查看源**"。）下面的示例演示了页面的某些标记，阐释了呈现的 HTML 中的 `class` 和 `type` 特性。

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

返回到*Views\Shared\EditorTemplates\Date.cshtml*模板，并&quot; 标记中删除 &quot;使用日期模板。 现在，已完成的模板如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>使用 NuGet 添加 jQuery UI Datepicker 快捷日历

在本部分中，会将[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/)快捷日历添加到日期编辑模板。 [JQUERY UI](http://jqueryui.com/)库为动画、高级效果和可自定义的小组件提供支持。 它构建于 jQuery JavaScript 库之上。 使用日历（而不是输入字符串），datepicker 弹出日历使输入日期变得简单和自然。 此快捷方式还会将用户限制为法律日期-日期的普通文本输入允许输入诸如 `2/33/1999` （2月33rd，1999）之类的内容，但[JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/) popup 日历不允许这样做。

首先，必须安装 jQuery UI 库。 为此，你将使用 NuGet，这是 SP1 版本的 Visual Studio 2010 和 Visual Web Developer 中包含的程序包管理器。

在 Visual Web Developer 中的 "**工具**" 菜单中，选择 " **Nuget 包管理器**"，然后选择 "**管理 nuget 包**"。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

注意：如果 "**工具**" 菜单未显示 " **Nuget 包管理器**" 命令，则需按照 NuGet 网站 "[安装 nuget](http://docs.nuget.org/docs/start-here/installing-nuget) " 页上的说明安装 nuget。   
  
如果使用的是 Visual Studio，而不是 Visual Web Developer，请从 "**工具**" 菜单中选择 " **NuGet 包管理器**"，然后选择 "**添加库程序包引用**"。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

在 " **MVCMovie-管理 NuGet 包**" 对话框中，单击左侧的 "**联机**" 选项卡，然后在 "搜索" 框中输入 &quot;jQuery. UI&quot;。 选择 "j**查询 UI 小组件： Datepicker**"，并选择 "**安装**" 按钮。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet 将 jQuery UI Core 和 jQuery UI 日期选取器的这些调试版本和缩小版本添加到你的项目：

- *jquery. node.js*
- *jquery. core. .js*
- *jquery. datepicker*
- *jquery. datepicker。*

注意：调试版本（没有 *. .js*扩展名的文件）对调试非常有用，但在生产站点中，只包含缩小版本。

若要实际使用 jQuery 日期选取器，需要创建一个将日历小组件挂钩到编辑模板的 jQuery 脚本。 在**解决方案资源管理器**中，右键单击 "*脚本*" 文件夹，然后依次选择 "**添加**"、"**新建项**" 和 " **JScript 文件**"。 将该文件命名为*DatePickerReady*。

将以下代码添加到*DatePickerReady*文件：

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

如果你不熟悉 jQuery，这里提供了有关此操作的简要说明：第一行是 &quot;jQuery ready&quot; 函数，该函数在页中的所有 DOM 元素都已加载时调用。 第二行选择具有类名 `datefield`的所有 DOM 元素，然后为每个元素调用 `datepicker` 函数。 （请记住，在本教程的前面部分中，已将 `datefield` 类添加到*Views\Shared\EditorTemplates\Date.cshtml*模板。）

接下来，打开*Views\Shared\\_Layout* 。 你需要添加对以下文件的引用，这些文件都是必需的，以便你可以使用日期选取器：

- *内容/主题/基/jquery。*
- *Content/themes/base/jquery. datepicker*
- *内容/主题/基/jquery. ui*
- *jquery. core. .js*
- *jquery. datepicker。*
- *DatePickerReady*

下面的示例演示了应在*Views\Shared\\_Layout*的 `head` 元素的底部添加的实际代码。

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

完整的 `head` 部分如下所示：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

[URL 内容帮助器](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx)方法将资源路径转换为绝对路径。 当应用程序在 IIS 上运行时，必须使用 `@URL.Content` 来正确引用这些资源。

按 Ctrl+F5 以运行应用程序。 选择 "编辑" 链接，然后将插入点放入 " **ReleaseDate** " 字段。 显示 jQuery UI 快捷日历。

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

与大多数 jQuery 控件一样，datepicker 可让你对其进行广泛的自定义。 有关信息，请参阅可视化自定义：在[JQUERY ui](http://learn.jquery.com/jquery-ui/getting-started/)网站上[设计 jquery ui 主题](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme)。

### <a name="supporting-the-html5-date-input-control"></a>支持 HTML5 日期输入控件

随着更多浏览器支持 HTML5，你将需要使用本机 HTML5 输入，例如 `date` input 元素，而不是使用 jQuery UI 日历。 可以向应用程序添加逻辑，以便在浏览器支持 HTML5 控件时自动使用它们。 为此，请将*DatePickerReady*文件的内容替换为以下内容：

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

此脚本的第一行使用 Modernizr 来验证是否支持 HTML5 日期输入。 如果不支持，则改为与 jQuery UI 日期选取器挂钩。 （[Modernizr](http://www.modernizr.com/docs/)是一个开源 JavaScript 库，用于检测 HTML5 和 CSS3 的本机实现的可用性。 Modernizr 包含在您创建的任何新的 ASP.NET MVC 项目中。）

做出此更改后，可以使用支持 HTML5 的浏览器（如 Opera 11）对其进行测试。 使用与 HTML5 兼容的浏览器运行应用程序，并编辑电影条目。 使用 HTML5 日期控件，而不是 jQuery UI 快捷方式日历：

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

因为新版本的浏览器以增量方式实现 HTML5，所以现在最好的方法是将代码添加到适合各种 HTML5 支持的网站。 例如，下面显示了一个更可靠的*DatePickerReady*脚本，使你的站点支持仅部分支持 HTML5 日期控件的浏览器。

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

此脚本选择 `date` 类型的 HTML5 `input` 元素，这些元素不完全支持 HTML5 日期控件。 对于这些元素，它将挂钩 jQuery UI 弹出日历，然后将 `type` 属性从 `date` 更改为 `text`。 通过将 `type` 属性从 `date` 改为 `text`，消除了部分 HTML5 日期支持。 更可靠的*DatePickerReady*脚本可在[JSFIDDLE](http://jsfiddle.net/XSTK8/15/)中找到。

### <a name="adding-nullable-dates-to-the-templates"></a>向模板添加可以为 Null 的日期

如果使用现有的日期模板之一并传递 null 日期，则会出现运行时错误。 若要使日期模板更可靠，请将其更改为处理 null 值。 若要支持可以为 null 的日期，请将*Views\Shared\DisplayTemplates\DateTime.cshtml*中的代码更改为以下内容：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

当模型为**null**时，该代码将返回空字符串。

将*Views\Shared\EditorTemplates\Date.cshtml*文件中的代码更改为以下内容：

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

当此代码运行时，如果模型不为 null，则使用模型的 `DateTime` 值。 如果模型为 null，则改为使用当前日期。

### <a name="wrapup"></a>Wrapup

本教程介绍了 ASP.NET 模板化帮助器的基本知识，并演示了如何在 ASP.NET MVC 应用程序中使用 jQuery UI datepicker 弹出日历。 有关详细信息，请尝试以下资源：

- 有关本地化的详细信息，请参阅 Rajeesh 的博客[JQueryUI Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)。
- 有关 jQuery UI 的信息，请参阅[JQUERY ui](http://docs.jquery.com/UI)。
- 有关如何本地化 datepicker 控件的信息，请参阅[UI/datepicker/本地化](http://docs.jquery.com/UI/Datepicker/Localization)。
- 有关 ASP.NET MVC 模板的详细信息，请参阅[ASP.NET MVC 2 模板](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)上的 Brad Wilson 的博客系列。 尽管此系列是为 ASP.NET MVC 2 编写的，但材料仍适用于当前版本的 ASP.NET MVC。

> [!div class="step-by-step"]
> [上一页](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
