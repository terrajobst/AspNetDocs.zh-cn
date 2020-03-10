---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 添加 Create 方法和 Create View |Microsoft Docs
author: shanselman
description: 本教程介绍了 ASP.NET MVC 的基本知识。 创建一个从数据库中读取和写入数据的简单 web 应用程序。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437288"
---
# <a name="adding-a-create-method-and-create-view"></a>添加 Create 方法和创建视图

作者： [Scott Hanselman](https://github.com/shanselman)

> 本教程介绍了 ASP.NET MVC 的基本知识。 你将创建一个简单的 web 应用程序，用于读取和写入数据库。 请访问[ASP.NET mvc 学习中心](../../../index.md)，查找其他 ASP.NET mvc 教程和示例。

在本部分中，我们将实现使用户能够在数据库中创建新电影所需的支持。 我们将通过实现/Movies/Create URL 操作来实现此目的。

实现/Movies/Create URL 的过程分为两个步骤。 当用户首次访问/Movies/Create URL 时，我们想要向他们显示一个 HTML 窗体，用户可以填写该表单以输入新电影。 然后，当用户提交窗体并将数据回发到服务器时，我们想要检索已发布的内容并将其保存到数据库中。

我们将在 MoviesController 类中的两个 Create （）方法内实现这两个步骤。 一种方法将显示 &lt;窗体&gt; 用户应填写该窗体来创建新电影。 第二种方法将处理在用户将 &lt;窗体&gt; 回服务器，并将新电影保存在数据库中时，处理已发布数据。

下面是我们要将其添加到 MoviesController 类以实现此操作的代码：

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

上面的代码包含我们在控制器中需要的所有代码。

现在，让我们实现 "创建视图" 模板，用于向用户显示窗体。 我们将在第一个 Create 方法中右键单击，然后选择 "添加视图"，为电影窗体创建视图模板。

我们将选择我们要将 "电影" 作为其视图数据类传递到 "电影"，并指出我们想要 "基架" 模板。

[![添加视图](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)

单击 "添加" 按钮后，将为你创建 \Movies\Create.aspx 视图模板。 由于我们从 "查看内容" 下拉列表中选择了 "创建"，因此 "添加视图" 对话框会自动 "基架" 某些默认内容。 基架创建了 HTML &lt;窗体&gt;、用于验证错误消息的位置，并且由于基架知道了电影，因此它为类的每个属性创建了标签和字段。

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

由于数据库会自动为电影提供 ID，因此请删除引用模型的那些字段。创建视图的 Id。 在 &lt;图例后删除7行&gt;字段&lt;/legend&gt;，因为它们显示了我们不想要的 ID 字段。

现在，让我们创建一个新电影，并将其添加到数据库中。 为此，我们将再次运行该应用程序，并访问 "/Movies" URL，并单击 "创建" 链接以添加新电影。

[![创建-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)

单击 "创建" 按钮时，会将此窗体上的数据回发到刚刚创建的/Movies/Create 方法（通过 HTTP POST）。 就像系统自动从 URL 开始使用 "numTimes" 和 "name" 参数，并将其映射到前面方法中的参数时，系统将自动从 POST 获取窗体字段，并将它们映射到对象。 在这种情况下，HTML 中的字段中的值（如 "ReleaseDate" 和 "Title"）将自动放入电影新实例的正确属性。

让我们再次看一看 MoviesController 中的第二个 Create 方法。 请注意它如何将 "电影" 对象作为参数：

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

然后将此电影对象传递到创建操作方法的 [HttpPost] 版本，并将其保存在数据库中，然后将用户重定向回 Index （）操作方法，该操作方法会在电影列表中显示保存的结果：

[![电影列表-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)

但我们不会检查电影是否正确，并且数据库不会允许我们保存无标题的电影。 如果可以告诉用户在数据库出现错误之前，这会很好。 接下来，我们将向应用程序添加验证支持。

> [!div class="step-by-step"]
> [上一页](getting-started-with-mvc-part5.md)
> [下一页](getting-started-with-mvc-part7.md)
