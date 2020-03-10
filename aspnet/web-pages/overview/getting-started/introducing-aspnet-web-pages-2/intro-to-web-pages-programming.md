---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: ASP.NET 网页编程基础知识简介 |Microsoft Docs
author: Rick-Anderson
description: 本教程概述了如何使用 Razor 语法在 ASP.NET 网页中进行编程。 你将学习的内容：用于 pr 的基本 "Razor" 语法
ms.author: riande
ms.date: 06/17/2015
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 474de7671ac2931e5ba9ff635d77385403644521
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509978"
---
# <a name="introducing-aspnet-web-pages---programming-basics"></a>ASP.NET 网页编程基础知识简介

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本教程概述了如何使用 Razor 语法在 ASP.NET 网页中进行编程。
> 
> 学习内容：
> 
> - 用于在 ASP.NET 网页中进行编程的基本 "Razor" 语法。
> - 一些基本C#，这是你将使用的编程语言。
> - 网页的一些基本编程概念。
> - 如何安装包（包含预先生成的代码的组件）以用于您的站点。
> - 如何使用*帮助*程序执行常见的编程任务。
>   
> 
> 介绍的功能/技术：
> 
> - NuGet 和包管理器。
> - `Gravatar` 帮助程序。

本教程主要为你介绍将用于 ASP.NET 网页的编程语法。 你将了解用 C#编程语言编写的 Razor 语法和代码。 你将在上一教程中大致了解此语法;在本教程中，我们将更详细地介绍语法。

我们保证本教程涉及到你在单个教程中看到的大多数编程，这是*仅有关编程的唯一教程*。 在此集的其余教程中，你将实际创建可执行有趣操作的页面。

你还将了解*帮助*程序。 帮助器是可添加到页面的组件（一段打包的代码）。 帮助器会为您执行工作，否则，手动操作可能单调乏味或复杂。

## <a name="creating-a-page-to-play-with-razor"></a>创建使用 Razor 播放的页面

在本部分中，你将玩 Razor，因此你可以了解基本语法。

如果它尚未运行，请启动 WebMatrix。 你将使用在上一教程中创建的网站（[入门](https://go.microsoft.com/fwlink/?LinkId=251578)网页）。 若要重新打开它，请单击 **"我的网站**" 并选择**WebPageMovies**：

![WebMatrix 开始屏幕显示 "打开网站选项" 和 "我的网站" 突出显示](intro-to-web-pages-programming/_static/image1.png)

选择 "**文件**" 工作区。

在功能区中，单击 "**新建**" 以创建页面。 选择 " **CSHTML** " 并将新页命名为*TestRazor*。

单击“确定”。

将以下内容复制到文件中，完全替换已存在的内容。

> [!NOTE]
> 将代码或标记从示例复制到页面时，缩进和对齐方式可能与教程中的不同。 不过，缩进和对齐不会影响代码的运行方式。

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a>检查 "示例" 页

你看到的大多数是普通的 HTML。 但在顶部有此代码块：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

请注意以下有关此代码块的事项：

- @ 字符告诉 ASP.NET，下面是 Razor 代码，而不是 HTML。 ASP.NET 会将 @ 字符后面的所有内容视为代码，直到它再次进入一些 HTML。 （在这种情况下，这是 &lt;！DOCTYPE&gt; 元素。
- 如果代码具有多个行，则大括号（{和}）包含一个 Razor 代码块。 大括号指示 ASP.NET 的代码在何处开始和结束。
- 字符标记注释，即不会执行的代码的一部分。
- 每个语句必须以分号（;) 结束。 （不过，不是注释。）
- 你可以将值存储在用关键字 var 创建（*声明*）的*变量*中。 创建变量时，可以为其指定一个名称，该名称可以包含字母、数字和下划线（\_）。 变量名不能以数字开头，也不能使用编程关键字的名称（如 var）。
- 用引号将字符串（如 "ASP.NET" 和 "Web Pages"）括起来。 （它们必须是双引号。）数字不是用引号引起来。
- 引号外的空白并不重要。 换行符通常无关紧要;例外情况是不能跨行拆分用引号引起来的字符串。 缩进和对齐并不重要。

在此示例中不明显的内容是所有代码都区分大小写。 这意味着变量参数是一个与可能名为参数或参数的变量不同的变量。 同样，var 是关键字，但 Var 却不是。

### <a name="objects-and-properties-and-methods"></a>对象和属性和方法

接下来就是表达式日期时间。 简而言之，DateTime 是一个*对象*。 对象是您可以使用进行编程的内容：页面、文本框、文件、图像、web 请求、电子邮件、客户记录等。对象具有一个或多个描述其特征的*属性*。 文本框对象具有文本属性（其他），请求对象具有 Url 属性（及其他），电子邮件中包含 From 属性和 To 属性等。 对象还包含它们可以执行的 "谓词" 的*方法*。 您将很多地处理对象。

如示例中所示，DateTime 是一个对象，可用于对日期和时间进行编程。 它有一个名为 "现在" 的属性，该属性返回当前日期和时间。

### <a name="using-code-to-render-markup-in-the-page"></a>使用代码在页中呈现标记

在页面的正文中，请注意以下事项：

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

同样，@ 字符告诉 ASP.NET，下面是代码而不是 HTML。 在标记中，可以添加 @，后跟代码表达式，ASP.NET 将在该点向右呈现该表达式的值。 在此示例中，@a 将呈现值为名为的变量，@product 呈现名为 product 的变量中的任何内容，等等。

不过，你并不局限于变量。 在此处的几个示例中，@ 字符位于表达式之前：

- @ （\*b）呈现变量 a 和 b 中的所有内容。 （\* 运算符表示乘法。）
- @ （技术 + "" + product）在连接变量并在两者之间添加空格后，呈现变量技术和产品中的值。 用于串联字符串的运算符（+）与用于添加数字的运算符相同。 ASP.NET 通常可以判断你使用的是数字还是字符串，并使用 + 运算符执行正确的操作。
- @Request.Url 呈现 Request 对象的 Url 属性。 Request 对象包含来自浏览器的当前请求的相关信息，当然，Url 属性包含该当前请求的 URL。

该示例还旨在向您演示如何以不同的方式执行工作。 可以在顶部的代码块中执行计算，将结果放入变量中，然后在标记中呈现变量。 或者，您可以在标记中的表达式中执行计算。 使用哪种方法取决于您所执行的操作，并且在某种程度上取决于您自己的喜好。

### <a name="seeing-the-code-in-action"></a>查看正在运行的代码

右键单击该文件的名称，然后选择 "**在浏览器中启动"** 。 你将在浏览器中看到页面中已解决的所有值和表达式。

![在浏览器中运行的 "TestRazor" 页](intro-to-web-pages-programming/_static/image2.png)

查看浏览器中的源。

![浏览器中的 "Test Razor" 页面源](intro-to-web-pages-programming/_static/image3.png)

正如你在上一教程中的经验所期望的那样，此页中不会有任何 Razor 代码。 您看到的只是实际显示值。 当你运行某个页面时，实际上就是发出到 WebMatrix 中内置的 web 服务器的请求。 收到请求后，ASP.NET 解析所有值和表达式，并将其值呈现到页面中。 然后，将该页发送到浏览器。

> [!TIP] 
> 
> **Razor 和C#**
> 
> 至此，我们已经说过使用 Razor 语法。 这是正确的，但它不是完整的故事。 你使用的实际编程语言称为*C#* 。 C#是 Microsoft 在十年前创建的，已成为创建 Windows 应用程序的主要编程语言之一。 已了解的有关如何命名变量以及如何创建语句等的所有规则实际上是该C#语言的所有规则。
> 
> Razor 特别适用于将此代码嵌入页面的一小部分约定。 例如，使用 @ 在页中标记代码，并使用 @ {} 嵌入代码块的约定是页面的 Razor 方面。 帮助器也被视为 Razor 的一部分。 Razor 语法在多个位置使用，而不只是在 ASP.NET 网页中使用。 （例如，它也用于 ASP.NET MVC 视图中。）
> 
> 我们提及这是因为，如果您查找有关编程 ASP.NET 网页的信息，您会发现很多对 Razor 的引用。 但是，其中许多引用不适用于您正在执行的操作，因此可能会造成混淆。 事实上，许多编程问题都确实涉及到使用C#或使用 ASP.NET。 因此，如果您特别了解 Razor 的相关信息，可能无法找到所需的答案。

## <a name="adding-some-conditional-logic"></a>添加一些条件逻辑

在页面中使用代码的一项强大功能是，可以根据各种条件更改发生的情况。 在本教程的此部分中，你将了解一些如何更改页面中显示的内容的方法。

该示例简单、有些精心设计，以便我们可以将精力集中在条件逻辑上。 你将创建的页面将执行以下操作：

- 在页面上显示不同的文本，具体取决于页面是第一次显示还是已单击按钮来提交页面。 这将是第一个条件测试。
- 仅当在 URL 的查询字符串中传递了某个值（http：//...？ show = true）时，才显示该消息。 这将是第二个条件测试。

在 WebMatrix 中创建页面，并将其命名为*TestRazorPart2*。 （在功能区中，单击 "**新建**"，选择 " **CSHTML**"，为文件命名，然后单击 **"确定"** 。）

将此页的内容替换为以下内容：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

顶部的代码块用一些文本初始化名为 message 的变量。 在页面的正文中，消息变量的内容显示在 &lt;p&gt; 元素中。 标记还包含一个 &lt;输入&gt; 元素来创建 "**提交**" 按钮。

运行页面，查看其工作原理。 现在，它基本上是一个静态页面，即使单击 "**提交**" 按钮也是如此。

返回到 WebMatrix。 在代码块中，在初始化消息的行*后*添加以下突出显示的代码：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a>If {} 块

刚添加的是 if 条件。 在代码中，if 条件的结构如下所示：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

要测试的条件用圆括号括起来。 它必须为值或返回 true 或 false 的表达式。 如果条件为 true，则 ASP.NET 将运行位于大括号内的语句或语句。 （这是*if*逻辑的*then*部分。）如果条件为 false，则跳过代码块。

下面是可以在 if 语句中测试的条件的几个示例：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

您可以通过使用*逻辑运算符*或*比较运算符*来对照值或表达式来测试变量：等于（= =）、大于（&gt;）、小于（&lt;）、大于或等于（&gt;=）以及小于或等于（&lt;=）。 ！ = 运算符表示不等于，例如，如果（a！ = 0）表示*不等于 0*。

> [!NOTE]
> 请务必注意，equals 的比较运算符（= =）与 = 不相同。 = 运算符仅用于赋值（var a = 2）。 如果将这些运算符组合在一起，则会出现错误，否则会出现一些奇怪的结果。

若要测试是否为 true，则完整的语法为 if （操作 = = true）。 但如果为（操作），则还可以使用快捷方式。 如果没有比较运算符，则 ASP.NET 假设您要测试是否为 true。

此 ! 运算符本身表示逻辑非。 例如，条件 if （！IsPost）表示*IsPost 是否不为 true*。

您可以通过使用逻辑 AND （&amp;&amp; 运算符）或逻辑 OR （| | 运算符）来组合条件。 例如，在前面的示例中，if 条件的最后一个表示*如果 FileProcessingIsDone 未设置为 TRUE 且 displayMessage 设置为 false*。

### <a name="the-else-block"></a>Else 块

如果是块，最后一件事： if 块后跟 else 块。 Else 块很有用，因为当条件为 false 时，必须执行不同的代码。 以下是一个简单的示例：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

你将在本系列的后续教程中看到一些示例，其中使用 else 块很有用。

### <a name="testing-whether-the-request-is-a-submit-post"></a>测试请求是否为提交（post）

还有很多，但让我们回到示例，该示例具有条件 if （IsPost） {...}。 IsPost 实际上是当前页的属性。 第一次请求页面时，IsPost 返回 false。 但是，如果您单击某一按钮或以其他方式提交该页（也就是说，您发布了它），则 IsPost 将返回 true。 因此，IsPost 可让你确定是否正在处理窗体提交。 （根据 HTTP 谓词，如果请求是 GET 操作，则 IsPost 将返回 false。 如果请求是 POST 操作，则 IsPost 将返回 true。）在后面的教程中，你将使用输入窗体，此测试将特别有用。

运行页面。 由于这是你第一次请求页面，你会看到 "这是你第一次请求页面"。 该字符串是将消息变量初始化为的值。 存在 if （IsPost）测试，但此时返回 false，因此 if 块内的代码不会运行。

单击 "**提交**" 按钮。 再次请求该页。 与之前一样，消息变量设置为 "这是第一次 ..."。 但这一次，测试 if （IsPost）将返回 true，因此 if 块内的代码会运行。 该代码将消息变量的值更改为一个不同的值，这是标记中呈现的内容。

现在，在标记中添加 if 条件。 在包含 "**提交**" 按钮的 &lt;p&gt; 元素下，添加以下标记：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

你将在标记内添加代码，因此必须从 @开始。 然后有一个 if 测试，它类似于你之前在代码块中添加的测试。 但在大括号内，你添加的是普通的 HTML，但至少在 @DateTime.Now之前，它是普通的。 这是另一小段 Razor 代码，因此，您必须在其前面加上 @。

此处的要点是，可以在顶部和标记中的代码块中添加条件。 如果在页面的正文中使用 if 条件，则块内的行可以是标记或代码。 在这种情况下，无论何时混合标记和代码，都必须使用 @ 以使其清楚地 ASP.NET 代码的位置。

运行页面，然后单击 "**提交**"。 这种情况下，你不仅可以在提交时看到不同的消息（"现在已提交 ..."），而且你会看到一条新消息，其中列出了日期和时间。

![在浏览器中运行的 "Test Razor 2" 页面，在提交后显示时间戳](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a>测试查询字符串的值

再一次测试。 这一次，你将添加一个用于测试在查询字符串中可能传递的名为 show 的值的 if 块。 （如下所示： `http://localhost:43097/TestRazorPart2.cshtml?show=true`）你将更改页面，以便仅当 show 的值为 true 时才显示已显示的消息（"这是第一个时间 ..." 等）。

在页面顶部（但内部）代码块的底部，添加以下内容：

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

完整的代码块现在如下例所示。 （请记住，将代码复制到页面时，缩进的外观可能会有所不同。 但这不会影响代码的运行方式。）

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

该块中的新代码将名为 showMessage 的变量初始化为 false。 然后，它会执行 if 测试，以在查询字符串中查找值。 第一次请求页面时，它具有如下所示的 URL：

`http://localhost:43097/TestRazorPart2.cshtml`

此代码确定 URL 是否在查询字符串中包含一个名为 show 的变量，如 URL 的此版本所示：

`http://localhost:43097/TestRazorPart2.cshtml`？ show = true

测试本身将查看 Request 对象的 QueryString 属性。 如果查询字符串包含名为 show 的项，并且该项设置为 true，则 if 块将运行，并将 showMessage 变量设置为 true。

这里有一种技巧，如您所见。 如名称所示，查询字符串是一个字符串。 但是，如果要测试的值为布尔值（true/false），则只能测试 true 和 false。 在查询字符串中显示变量的值之前，必须将其转换为布尔值。 这就是 AsBool 方法的作用，它采用字符串作为输入并将其转换为布尔值。 显然，如果字符串为 "true"，则 AsBool 方法会将该值转换为 true。 如果字符串的值为其他值，则 AsBool 返回 false。

> [!TIP] 
> 
> **数据类型和 As （）方法**
> 
> 到目前为止，我们只是在创建变量时使用关键字 var。 但这并不完整。 若要操作值（若要添加数字或连接字符串，或者比较日期或测试 true/false） C# ，必须使用适当的内部表示形式的值。 C#根据要对值执行的操作，*通常*可以确定表示形式应该是什么（即，数据的*类型*）。 不过，现在它无法做到这一点。 如果不是，则必须明确指出应该如何C#表示数据。 AsBool 方法执行此功能，它会C#告知字符串值 "true" 或 "false" 应被视为布尔值。 也存在将字符串表示为其他类型的类似方法，例如 AsInt （视为一个整数）、AsDateTime （视为日期/时间）、AsFloat （视为浮点数）等。 当你使用这些 As （）方法时， C#如果不能根据请求来表示字符串值，你会看到错误。

在页面的标记中，删除或注释掉此元素（此处显示注释掉）：

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

如果已删除或注释掉该文本，请添加以下内容：

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

If 测试表明，如果 showMessage 变量为 true，则将使用消息变量的值渲染 &lt;p&gt; 元素。

### <a name="summary-of-your-conditional-logic"></a>条件逻辑摘要

如果你并不完全确定刚刚完成的操作，则可以使用摘要。

- 消息变量将初始化为默认字符串（"这是第一次 ..."）。
- 如果页面请求是提交（post）的结果，则 "消息" 的值将更改为 "现在已提交 ..."
- ShowMessage 变量初始化为 false。
- 如果查询字符串包含？ show = true，则将 showMessage 变量设置为 true。
- 在标记中，如果 showMessage 为 true，则将呈现一个 &lt;p&gt; 元素，该元素显示 message 的值。 （如果 showMessage 为 false，则不会在标记中的该点呈现任何内容。）
- 在标记中，如果请求是 post，则会呈现 &lt;p&gt; 元素，该元素显示日期和时间。

运行页面。 没有消息，因为 showMessage 为 false，因此在标记中，if （showMessage）测试返回 false。

单击“提交”。 此时会显示日期和时间，但不会显示任何消息。

在浏览器中，选择 "URL" 框，并将以下内容添加到 URL 的末尾：？ show = true，然后按 Enter。

![显示查询字符串的浏览器中的 "Test Razor 2" 页](intro-to-web-pages-programming/_static/image5.png)

再次显示该页。 （因为你更改了 URL，所以这是一个新请求，而不是提交。）再次单击 "**提交**"。 此时将再次显示该消息，如日期和时间。

![如果有查询字符串，则在提交后出现 "Test Razor 2" 页](intro-to-web-pages-programming/_static/image6.png)

在 URL 中，更改？ show = true to？ show = false，然后按 Enter。 再次提交该页。 该页返回到你的开始方式-无消息。

如前所述，此示例的逻辑有点精心设计。 但是，如果要在许多页面中显示，将需要你在此处看到的一个或多个窗体。

## <a name="installing-a-helper-displaying-a-gravatar-image"></a>安装帮助程序（显示 Gravatar 的映像）

用户经常想要在网页上执行的某些任务需要大量代码或需要额外的知识。 示例：显示数据图表;在页面上放置 Facebook "赞" 按钮;从网站发送电子邮件;裁剪或调整图像大小;为站点使用 PayPal。 为了便于执行这些类型的操作，ASP.NET 网页允许使用*帮助*程序。 帮助器是为站点安装的组件，可让你使用只需几行 Razor 代码执行典型任务。

ASP.NET 网页内置了几个帮助程序。 但是，许多帮助程序都在使用 NuGet 包管理器提供的包（外接程序）中提供。 NuGet 允许您选择要安装的包，然后处理安装的所有详细信息。

在本教程的此部分，将安装帮助器，以显示 Gravatar （"全局识别的头像"）图像。 你将了解两个问题。 其中一种方法是查找并安装帮助程序。 你还将了解如何使用帮助程序轻松完成一些操作，你需要使用大量代码来完成此操作。

你可以在[http://www.gravatar.com/](http://www.gravatar.com/)上的 Gravatar 网站注册自己的 Gravatar，但创建 Gravatar 帐户并不是必需的。

在 WebMatrix 中，单击 " **NuGet** " 按钮。

![WebMatrix 中的 "NuGet 库" 对话框](intro-to-web-pages-programming/_static/image7.png)

这会启动 NuGet 包管理器，并显示可用的包。 （并不是所有的包都是帮助者; 某些包将添加到 WebMatrix 本身，一些是其他模板，等等。）可能会收到有关版本不兼容的错误消息。 您可以通过单击 **"确定"** 并继续学习本教程来忽略此错误消息。

![WebMatrix 中的 "NuGet 库" 对话框](intro-to-web-pages-programming/_static/image8.png)

在搜索框中，输入 "asp.net 帮助程序"。 NuGet 显示与搜索词匹配的包。

![WebMatrix 中显示包的 NuGet 库](intro-to-web-pages-programming/_static/image9.png)

ASP.NET Web 帮助程序库包含用于简化许多常见任务（包括使用 Gravatar 映像）的代码。 选择**ASP.NET Web 助手库**包，然后单击 "**安装**" 以启动安装程序。 当系统询问你是否要安装包，请选择 **"是"** ，并接受条款以完成安装。

介绍完毕。 NuGet 会下载并安装所有内容，包括可能需要的任何其他组件（*依赖项*）。

如果出于某种原因，您必须卸载帮助程序，该过程非常相似。 单击 " **NuGet** " 按钮，单击 "**已安装**" 选项卡，然后选择要卸载的包。

## <a name="using-a-helper-in-a-page"></a>在页面中使用帮助器

现在，你将使用刚刚安装的帮助器。 对于大多数帮助器，向页面添加帮助程序的过程类似。

在 WebMatrix 中创建页面，并将其命名为*GravatarTest. cshml*。 （您要创建一个特殊页面来测试帮助程序，但您可以在站点的任何页中使用帮助程序。）

在 &lt;主体&gt; 元素内，添加一个 &lt;div&gt; 元素。 在 &lt;div&gt; 元素内，键入以下内容：

@Gravatar。

@ 字符与用来标记 Razor 代码的字符相同。 **Gravatar**是您正在使用的帮助程序对象。

一旦键入句点（.），WebMatrix 就会显示 Gravatar helper 提供的*方法*（函数）的列表：

![Gravatar 帮助程序 IntelliSense 下拉列表](intro-to-web-pages-programming/_static/image10.png)

此功能称为*IntelliSense*。 它通过提供上下文相关的选项来帮助你进行编码。 IntelliSense 适用于在 WebMatrix 中受支持的 HTML、CSS、ASP.NET 代码、JavaScript 和其他语言。 这是另一项功能，可更轻松地在 WebMatrix 中开发网页。

在键盘上按 G，你会看到 IntelliSense 查找 GetHtml 方法。 按 Tab。 IntelliSense 会插入所选的方法（GetHtml）。 键入一个左括号，并注意右括号会自动添加。 在两个括号之间键入电子邮件地址，用引号引起来。 如果你有一个 Gravatar 帐户，将返回你的个人资料图片。 如果没有 Gravatar 帐户，将返回默认映像。 完成后，该行如下所示：

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

现在，在浏览器中查看页面。 你的照片或默认图像将显示，具体取决于你是否有 Gravatar 帐户。

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![默认图像](intro-to-web-pages-programming/_static/image12.png)

若要了解帮助程序的作用，请在浏览器中查看该页的源。 除了页面中包含的 HTML 外，还会看到一个包含标识符的图像元素。 这是帮助程序在您已 @Gravatar.GetHtml的位置呈现的页中的代码。 帮助器采取了提供的信息并生成了直接与 Gravatar 进行通信的代码，以便为所提供的帐户恢复正确的映像。

使用 GetHtml 方法，还可以通过提供其他参数来自定义映像。 下面的代码演示如何请求图像的宽度和高度均为40像素，如果指定的帐户不存在，则使用名为**wavatar**的指定默认图像。

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

此代码将产生类似于以下结果的内容（默认图像将随机改变）。

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a>下一步

为了使本教程简短，我们只关注几个基础知识。 从本质上来说，更多*的是*Razor C#和。 在学习这些教程时，你将了解更多。 如果希望了解有关 Razor 和C#更高的编程方面的详细信息，可以阅读此处的更详尽的介绍：[使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)。

下一教程将介绍如何使用数据库。 在本教程中，您将开始创建一个示例应用程序，该应用程序使您能够列出您最喜爱的电影。

## <a name="complete-listing-for-testrazor-page"></a>TestRazor 页的完整列表

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a>TestRazorPart2 页的完整列表

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a>GravatarTest 页的完整列表

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a>其他资源

- [使用 Razor 语法的 ASP.NET Web 编程简介](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Twitter 帮助程序](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> [上一页](getting-started.md)
> [下一页](displaying-data.md)
