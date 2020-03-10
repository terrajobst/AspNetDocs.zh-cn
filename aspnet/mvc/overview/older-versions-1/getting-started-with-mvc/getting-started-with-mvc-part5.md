---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 从控制器访问模型的数据 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437366"
---
# <a name="accessing-your-models-data-from-a-controller"></a>从控制器访问模型的数据

作者： [Scott Hanselman](https://github.com/shanselman)

> 本教程介绍了 ASP.NET MVC 的基本知识。 你将创建一个简单的 web 应用程序，用于读取和写入数据库。 请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。

在本部分中，我们将创建一个新的 MoviesController 类，并编写一些代码来检索电影数据，并使用视图模板将其显示到浏览器。

右键单击 "控制器" 文件夹，然后创建新的 MoviesController。

[![添加控制器](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)

这会在我们的项目中的 \Controllers 文件夹下创建新的 "MoviesController.cs" 文件。 让我们更新 MovieController，以便从新填充的数据库中检索电影列表。

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

我们正在执行 LINQ 查询，以便我们仅检索在1984年夏季发布的电影。 我们需要一个视图模板来呈现此电影列表，因此右键单击方法并选择 "添加视图" 以创建它。

在 "添加视图" 对话框中，我们将指示要将列表&lt;的电影.&gt; 电影传递到我们的视图模板。 与以前使用 "添加视图" 对话框并选择创建 "空" 模板不同的是，这次我们将指示我们希望 Visual Studio 自动 "基架" 视图模板用于某些默认内容。 为此，请选择 "查看内容" 下拉菜单中的 "列表" 项。

请记住，当你创建了一个新类时，需要编译你的应用程序，使其显示在 "添加视图" 对话框中。

![添加视图](getting-started-with-mvc-part5/_static/image3.png)

单击 "添加"，系统将自动为我们的视图生成显示电影列表的代码。 这是将 &lt;h2&gt; 标题更改为类似于 "我的电影列表" 的时间的好时机，就像我们先前在 Hello World 视图中做的一样。

[![电影-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)

运行应用程序，并在地址栏中访问/Movies。 现在，我们已使用控制器中的基本查询从数据库中检索数据，并将数据返回到了解电影的视图。 然后，该视图将旋转影片列表，并为我们创建一个数据表。

[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)

我们不会对此应用程序实现编辑、详细信息和删除功能，因此，我们不需要基架模板为我们创建的默认链接。 打开/Movies/Index.aspx 文件并将其删除。

下面是我们进行这些更改后，更新的视图模板应类似于的源代码：

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

它正在创建不需要的链接，因此，我们将在此示例中删除这些链接。 不过，我们将继续创建新的链接，接下来是这样！ 下面是删除此列后应用的外观。

[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)

现在，我们提供了电影数据的简单列表。 但是，如果单击 "新建" 链接，则会出现错误，因为它未挂钩！ 让我们实现一个创建操作方法，使用户能够在数据库中输入新电影。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part4.md)
> [下一页](getting-started-with-mvc-part6.md)
