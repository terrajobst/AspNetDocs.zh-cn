---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 向模型添加列 |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437222"
---
# <a name="adding-a-column-to-the-model"></a>向模型添加列

作者： [Scott Hanselman](https://github.com/shanselman)

> 本教程介绍了 ASP.NET MVC 的基本知识。 你将创建一个简单的 web 应用程序，用于读取和写入数据库。 请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。

在本部分中，我们将演练如何更改数据库的架构，并处理应用程序中的更改。

让我们将 "分级" 列添加到 "电影" 表中。 返回到 IDE，并单击数据库资源管理器。 右键单击电影表，然后选择 "打开表定义"。

添加 "评级" 列，如下所示。 由于我们现在没有任何分级，列可以允许空值。 单击“保存”。

[![编辑电影表](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

接下来，返回到解决方案资源管理器并打开电影 .edmx 文件（在 \Models 文件夹中）。 右键单击设计图面（白色区域），然后选择 "从数据库更新模型"。

[![电影-Microsoft Visual Web Developer 2010 Express （11）](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

这会启动 "更新向导"。 单击其中的 "刷新" 选项卡，然后单击 "完成"。 然后，将用新列更新我们的 Movie 模型类。

![更新向导（2）](getting-started-with-mvc-part8/_static/image5.png)

单击 "完成" 后，可以看到新的 "评级" 列已添加到模型中的 "电影" 实体。

[![电影实体](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

我们在数据库模型中添加了一个列，但视图并不知道它。

## <a name="update-views-with-model-changes"></a>用模型更改更新视图

可以通过几种方式来更新视图模板，以反映新的评级列。 由于我们通过 "添加视图" 对话框生成这些视图，因此可以将其删除并重新创建它们。 不过，通常情况下，用户已从初始基架生成中对其视图模板进行了修改，并需要手动添加或删除字段，就像我们使用 Create 的 ID 字段做的一样。

打开 "\Views\Movies\Index.aspx" 模板，将 &lt;&gt;评级添加到 "电影" 表的开头&lt;"&gt;"。 我添加了我在流派后的我。 然后，在同一列位置但向下减小，添加一行来输出我们的新分级。

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

最终的 "索引 .aspx" 模板将如下所示：

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

接下来，打开 \Views\Movies\Create.aspx 模板，为新的 "分级" 属性添加标签和文本框：

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

我们的最后一个 Create .aspx 模板将如下所示，并将浏览器的标题和辅助 &lt;&gt; h2 改为将其标题更改为类似于 "创建电影" 的内容，而在这里我们就会这样！

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

运行你的应用程序，此时已在数据库中添加了一个新字段，该字段已添加到 "创建" 页。 添加新电影-这次带有评级，并单击 "创建"。

[![创建电影-Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

单击 "创建" 后，将被发送到 "索引" 页，在该页面中，新电影将与数据库中的新 "分级" 列一起列出。

[![电影列表-Windows Internet Explorer （12）](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

本基本教程介绍了如何开始创建控制器，如何将它们与视图相关联，并将其传递给硬编码数据。 然后，我们创建并设计了一个数据库，并在其中放置了一些数据。 我们从数据库中检索数据并将其显示在 HTML 表中。 然后，我们添加了一个 Create 窗体，该窗体使用户能够在 Web 应用程序中向数据库本身添加数据。 我们添加了验证，然后在客户端使用 JavaScript 进行验证。 最后，我们已将数据库更改为包含新的数据列，然后更新了两个页面以创建和显示此新数据。

我现在建议你转到我们的中级教程 "[MVC 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)"，以及[https://asp.net/mvc](https://asp.net/mvc)的多个视频和资源，以详细了解 ASP.NET MVC！

请尽情体验吧！

- Scott Hanselman-在 Twitter 上[http://hanselman.com](http://hanselman.com)和[@shanselman](http://twitter.com/shanselman) 。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part7.md)
