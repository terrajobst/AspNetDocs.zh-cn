---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: 向模型添加验证 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437276"
---
# <a name="adding-validation-to-the-model"></a>向模型添加验证

作者： [Scott Hanselman](https://github.com/shanselman)

> 本教程介绍了 ASP.NET MVC 的基本知识。 你将创建一个简单的 web 应用程序，用于读取和写入数据库。 请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。

在本部分中，我们将实现在应用程序中启用输入验证所需的支持。 我们将确保数据库内容始终正确，并在最终用户尝试输入电影数据无效时向最终用户提供有用的错误消息。 首先向 Movie 类添加少量验证逻辑。

右键单击模型文件夹，然后选择 "添加类"。 将类命名为 "Movie"。

当我们前面创建了 "电影" 实体模型时，IDE 创建了一个 Movie 类。 事实上，Movie 类的一部分可以在一个文件中，也可以位于另一个文件中。 这称为分部类。 我们要从另一个文件扩展 Movie 类。

我们将创建一个指向 "合作者类" 的部分电影类，其中的某些属性将向系统提供验证提示。 我们将根据需要标记标题和价格，还会坚持价格在某个范围内。 右键单击 "模型" 文件夹，然后选择 "添加类"。 命名类电影，并单击 "确定" 按钮。 下面是我们的部分电影类的外观。

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

重新运行应用程序，并尝试输入价格超过100的电影。 提交表单后，会收到错误。 此错误在服务器端捕获，并在发布窗体后发生。 请注意，ASP.NET MVC 的内置 HTML 帮助程序的智能方式足以显示错误消息，并在 textbox 元素中为我们维护值：

[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)

这很好，但如果我们可以立即在客户端上通知用户，则这会很好。

让我们使用 JavaScript 启用一些客户端验证。

## <a name="adding-client-side-validation"></a>添加客户端验证

由于我们的 Movie 类已经有一些验证属性，因此我们只需将一些 JavaScript 文件添加到我们的 Create .aspx 视图模板，然后添加一行代码来实现客户端验证。

从 VWD 中，请访问我们的 "视图"/"电影" 文件夹，然后打开 "创建 .aspx"。

在解决方案资源管理器中打开 "脚本" 文件夹，并将以下三个脚本拖到 &lt;head&gt; 标记中。

- MicrosoftAjax.js
- MicrosoftMvcValidation.js

希望这些脚本文件按此顺序显示。

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

此外，将此单行添加到 Html.beginform：

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

下面是 IDE 中显示的代码。

[![电影-Microsoft Visual Web Developer 2010 Express （10）](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)

运行应用程序并再次访问/Movies/Create，并单击 "创建" 而不输入任何数据。 错误消息会立即显示，而不是将数据完全发送到服务器时所关联的页面 flash。 这是因为 ASP.NET MVC 现在正在验证客户端（使用 JavaScript）和服务器上的输入。

[![创建-Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)

这看起来不错！ 现在，我们将另一个列添加到数据库中。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part6.md)
> [下一页](getting-started-with-mvc-part8.md)
