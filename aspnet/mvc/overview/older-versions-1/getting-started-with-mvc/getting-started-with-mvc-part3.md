---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 添加视图 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469772"
---
# <a name="adding-a-view"></a>添加视图

作者： [Scott Hanselman](https://github.com/shanselman)

> 本教程介绍了 ASP.NET MVC 的基本知识。 你将创建一个简单的 web 应用程序，用于读取和写入数据库。 请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。

在本部分中，我们将了解如何让 HelloWorldController 类使用视图模板文件来将生成 HTML 响应完全封装回客户端。

首先，让我们将视图模板与索引方法结合使用。 我们的方法称为 Index，它位于 HelloWorldController 中。 目前，Index （）方法返回一个字符串，其中包含在控制器类中硬编码的消息。

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

现在，让我们将 Index 方法更改为，如下所示：

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

现在，我们将一个视图模板添加到我们的项目，我们可以将其用于索引（）方法。 为此，请在 Index 方法中间的某个位置右键单击鼠标，然后单击 "添加视图 ..."

![图像](getting-started-with-mvc-part3/_static/image1.png)

这将显示 "添加视图" 对话框，该对话框提供了一些选项，用于说明我们如何创建可供索引方法使用的视图模板。 现在，请不要更改任何内容，只需单击 "添加" 按钮即可。

[!["添加视图" 对话框](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)

单击 "添加" 后，解决方案文件夹中将显示一个新文件夹和一个新文件，如下所示。 我现在在 Views 下有一个 HelloWorld 文件夹，该文件夹内有一个索引 .aspx 文件。

[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)

新的索引文件也已经打开并可以进行编辑。 在第一个 &lt;h2 下添加一些文本&gt;Index&lt;/h2&gt; 如 "Hello World"。

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

运行应用程序，并在浏览器中再次访问[`http://localhost:xx/HelloWorld`](http://localhostxx) 。 在此示例中，控制器中的 Index 方法未执行任何操作，但调用了 "return View （）"，这表明我们希望使用视图模板文件来将响应呈现给客户端。 由于我们未显式指定要使用的视图模板文件的名称，因此 ASP.NET MVC 默认使用 \Views\HelloWorld 文件夹中的 "" 视图文件。 现在我们看到我们在视图中进行了硬编码的字符串。

[![索引-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)

看起来不错。 但请注意，浏览器的标题显示 "索引"，而页面上的大标题显示 "我的 MVC 应用程序"。 让我们更改这些。

### <a name="changing-views-and-master-pages"></a>更改视图和母版页

首先，让我们更改文本 "我的 MVC 应用程序"。 该文本是共享的，并显示在每一页上。 它实际上只显示在代码中的一个位置，即使它在应用程序的每一页上也是如此。 中转到解决方案资源管理器中的/Views/Shared 文件夹，然后打开 "Master" 文件。 此文件称为母版页，它是其他所有页面都使用的共享 "shell"。

请注意一些文本，其中显示了此文件中的 ContentPlaceholder "MainContent"。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

占位符是您创建的所有页面都显示在母版页中的位置。 尝试更改标题，并运行应用程序并访问多个页面。 你会注意到，你的一个更改出现在多个页面上。

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

现在，每个页面都有主要标题，即 "我的 MVC 电影应用程序" 的 "H1"。 处理所有页面之间共享的白色文本。

下面是一个完整的站点，其中包含已更改的标题：

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

现在，让我们更改索引页的标题。

打开/HelloWorld/Index.aspx。 这里有两个要更改的位置。 首先，在浏览器标题中显示的标题，然后是辅助标头。 我要使它们略有不同，以便您可以看到哪个代码更改了应用程序的哪一部分。

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

运行应用并访问/Movies。 请注意，浏览器标题、主标题和辅助标题已更改。 在您的应用程序中对视图进行较小的更改时，可以轻松地进行重大更改。

[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)

我们有点 "数据" （在本例中为 "Hello World！" 消息）虽然是硬编码的。 我们有 V （Views），我们有 C （控制器），但没有 M （模型）。 我们很快会演练如何创建数据库并从中检索模型数据。

## <a name="passing-a-viewmodel"></a>传递 ViewModel

不过，在开始使用数据库并讨论模型之前，先来谈谈 "Viewmodel"。 这些对象表示视图模板在向客户端呈现 HTML 响应时所需的内容。 它们通常由控制器类创建并传递给视图模板，只应包含视图模板所需的数据，而不能有更多的数据。

以前，我们的 HelloWorld 示例使用了一个名称和一个 numTimes 参数，并将其输出到浏览器。 不要让控制器继续直接呈现此响应，而是创建一个小类来保存该数据，然后将其传递到视图模板，以使用它呈现回 HTML 响应。 这样一来，控制器就会考虑到一个问题，另一个是查看模板，使我们能够在应用程序中保持干净的 "问题分离"。

返回到 HelloWorldController.cs 文件并添加新的 "WelcomeViewModel" 类，并更改控制器中的 "欢迎" 方法。 下面是在同一文件中包含新类的完整 HelloWorldController.cs。

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

即使是在多行上，欢迎方法也只是两个代码语句。 第一个语句将两个参数打包到一个 ViewModel 对象中，第二个语句将生成的对象传递到视图。

现在，我们需要一个欢迎视图模板！ 右键单击欢迎方法，然后选择 "添加视图"。 这次，我们将选中 "创建强类型视图"，然后从下拉列表中选择我们的 WelcomeViewModel 类。 此新视图将仅了解 WelcomeViewModels 和其他类型的对象。

> *注意：将 WelcomeViewModel 添加到后，需要编译一次，以便显示在下拉列表中。*

"添加视图" 对话框应如下所示。 单击“添加”按钮。 ![添加带圆圈的视图](getting-started-with-mvc-part3/_static/image10.png)

将此代码添加到新的 "欢迎"&gt; 中的 "&lt;h2" 下。 我们将进行一次循环，并将 "Hello" 当作用户说我们应该！

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

另外，请注意，当你键入这一点时，这是因为我们告诉此关于 WelcomeViewModel 的视图（他们已结婚，请记住？），我们每次引用模型对象时都会获得有用的 Intellisense，如以下屏幕截图所示：

[![NumTime 源代码](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)

运行应用程序并再次访问 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`。 现在，我们从 URL 获得数据，并自动将数据传递到控制器，控制器会将数据打包到 ViewModel，并将该对象传递到视图。 视图比向用户显示 HTML 数据。

[![欢迎使用 Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)

嗯，这是模型的 "M" 类型，但不是数据库类型。 接下来，我们来看一下我们学到的内容，创建了一个电影数据库。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part2.md)
> [下一页](getting-started-with-mvc-part4.md)
