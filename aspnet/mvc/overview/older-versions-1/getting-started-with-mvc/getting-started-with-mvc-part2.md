---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 添加控制器 |Microsoft Docs
author: shanselman
description: 如果本教程可在此处使用 Visual Studio 2013，则为已更新的版本。 新教程使用 ASP.NET MVC 5，它对 t 。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437564"
---
# <a name="adding-a-controller"></a>添加控制器

作者： [Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > 如果本教程可在[此处](../../getting-started/introduction/getting-started.md)使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，则为已更新的版本。 新教程使用 ASP.NET MVC 5，这在本教程中提供了许多改进。
>
>
> 本教程介绍了 ASP.NET MVC 的基本知识。 你将创建一个简单的 web 应用程序，用于读取和写入数据库。 请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。

MVC 代表模型、视图和控制器。 MVC 是用于开发应用程序的一种模式，因此，每个部件具有不同于另一个的责任。

- 模型：应用程序的数据
- 视图：你的应用程序将用于动态生成 HTML 响应的模板文件。
- 控制器：用于处理对应用程序的传入 URL 请求、检索模型数据，然后指定用于向客户端呈现响应的视图模板的类。

我们将在本教程中介绍所有这些概念，并说明如何使用它们来生成应用程序。

让我们通过右键单击 "解决方案资源管理器" 中的 "控制器" 文件夹，然后选择 "添加控制器" 来创建新的控制器。

[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)

将新控制器命名为 "HelloWorldController"，并单击 "添加"。

[![添加控制器对话框](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)

请注意，在右侧的 "解决方案资源管理器中，已为你创建了一个名为 HelloWorldController.cs 的新文件，并且该文件现在已在**IDE**中打开。

[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)

在新的公共类 HelloWorldController 中创建两个新的方法。 作为示例，我们将直接从控制器返回 HTML 字符串。

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

控制器名为 HelloWorldController，新方法称为 Index。 再次运行应用程序，就像之前一样（单击 "播放" 按钮或按 F5 执行此操作）。 浏览器启动后，请将地址栏中的路径更改为 `http://localhost:xx/HelloWorld` 其中 xx 是计算机选择的数字。 现在，浏览器应类似于下面的屏幕截图。 在上面的方法中，我们返回了传递到名为 "Content" 的方法中的字符串。 我们告诉系统只返回了一些 HTML，但确实返回了！

ASP.NET MVC 根据传入 URL 调用不同的控制器类（以及其中的不同操作方法）。 ASP.NET MVC 使用的默认映射逻辑使用如下格式来控制运行的代码：

/[Controller]/[ActionName]/[Parameters]

URL 的第一部分确定要执行的控制器类。 因此，/HelloWorld 映射到 HelloWorldController 类。 URL 的第二部分确定要执行的类的操作方法。 因此，/HelloWorld/Index 将导致 HelloWorldController 类的 Index （）方法执行。 请注意，我们只需要访问上面的/HelloWorld，而方法索引是隐含的。 这是因为，如果未显式指定一个名为 "Index" 的方法，则该方法将在控制器上调用。

[![这是我的默认操作](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)

现在，我们来访问 `http://localhost:xx/HelloWorld/Welcome.` 现在我们的欢迎方法已执行，并返回其 HTML 字符串。

同样，/[控制器]/[ActionName]/[参数] 因此控制器为 HelloWorld，欢迎是在这种情况下的方法。 尚未完成参数。

[![这是 "欢迎操作" 方法](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)

让我们略微修改示例，以便我们可以将中的某些信息从 URL 传递到控制器，例如：/HelloWorld/Welcome？ name = Scott&amp;numtimes = 4。 更改你的欢迎方法以包含两个参数，并按如下所示进行更新。 请注意，我们使用了C#可选的参数功能，指示如果不传入参数，numTimes 应默认为1。

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

运行应用程序，并访问 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 根据需要更改 name 和 numtimes 的值。 系统自动将命名参数从地址栏中的查询字符串映射到方法中的参数。

在这两个示例中，控制器都在执行所有工作，并且已直接返回 HTML。 通常情况下，我们不希望控制器直接返回 HTML，因为这样做的代码会非常麻烦。 我们通常会使用单独的视图模板文件来帮助生成 HTML 响应。 我们来看看如何实现此目的。 关闭浏览器并返回到 IDE。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part1.md)
> [下一页](getting-started-with-mvc-part3.md)
