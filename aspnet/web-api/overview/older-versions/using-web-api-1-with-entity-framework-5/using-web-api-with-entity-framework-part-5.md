---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 第5部分：使用挖空创建动态 UI |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447860"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>第5部分：使用挖空创建动态 UI

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>使用 Knockout.js 创建动态 UI

在本部分中，我们将使用 "挖空" 将功能添加到 "管理" 视图。

"[挖空](http://knockoutjs.com/)" 是一种 Javascript 库，可轻松地将 HTML 控件绑定到数据。 挖空 node.js 使用模型-视图-ViewModel （MVVM）模式。

- *模型*是业务域中的数据的服务器端表示形式（在我们的示例中，是产品和订单）。
- *视图*为表示层（HTML）。
- *视图模型*是包含模型数据的 Javascript 对象。 视图模型是 UI 的代码抽象。 它不知道 HTML 表示形式。 相反，它表示视图的抽象功能，如 "项目列表"。

视图被数据绑定到视图模型。 视图模型的更新会自动反映在视图中。 视图模型还可获取视图中的事件（如按钮单击），并在模型上执行操作，例如创建订单。

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

首先，我们将定义视图模型。 之后，我们将 HTML 标记绑定到视图模型。

将以下 Razor 节添加到管理员：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

可以将此部分添加到文件中的任何位置。 呈现视图时，该部分将显示在 HTML 页的底部，位于关闭 &lt;/body&gt; 标记之前。

此页的所有脚本都将进入注释指示的脚本标记内：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

首先，定义视图模型类：

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**observableArray**是挖空的特殊对象，称为可*观察*对象。 从[挖空的 .js 文档](http://knockoutjs.com/documentation/observables.html)：可观测对象是一个 "JavaScript 对象，可通知订阅服务器的更改"。 当可观察的内容更改时，视图将自动更新以匹配。

若要填充 `products` 数组，请向 web API 发出 AJAX 请求。 回忆一下，我们已将 API 的基本 URI 存储在视图包中（请参阅本教程的第[4 部分](using-web-api-with-entity-framework-part-4.md)）。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

接下来，将函数添加到视图模型，以创建、更新和删除产品。 这些函数将 AJAX 调用提交到 web API，并使用结果来更新视图模型。

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

现在最重要的部分是： fulled 加载 DOM 时，调用**applyBindings**函数并传入 `ProductsViewModel`的新实例：

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

**ApplyBindings**方法激活视图模型与视图的挖空和连线。

现在我们有了一个视图模型，接下来可以创建绑定。 在挖空中，可以通过将 `data-bind` 特性添加到 HTML 元素来实现此目的。 例如，若要将 HTML 列表绑定到数组，请使用 `foreach` 绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

`foreach` 绑定将循环访问数组，并为数组中的每个对象创建子元素。 子元素上的绑定可以引用数组对象中的属性。

将以下绑定添加到 "更新产品" 列表：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

`<li>` 元素出现在**foreach**绑定的作用域内。 这意味着，挖空会针对 `products` 数组中的每个产品呈现一次元素。 `<li>` 元素中的所有绑定都引用该产品实例。 例如，`$data.Name` 引用产品的 `Name` 属性。

若要设置文本输入的值，请使用 `value` 绑定。 使用 `click` 绑定将这些按钮绑定到模型视图上的函数。 产品实例作为参数传递给每个函数。 有关详细信息，请[参阅 "挖空](http://knockoutjs.com/documentation/observables.html)的" 文档对各种绑定有很好的说明。

接下来，在 "添加产品" 窗体上为**提交**事件添加绑定：

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

此绑定对视图模型调用 `create` 函数来创建新产品。

下面是管理视图的完整代码：

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

运行应用程序，用管理员帐户登录，然后单击 "管理员" 链接。 应会看到产品列表，并能够创建、更新或删除产品。

> [!div class="step-by-step"]
> [上一页](using-web-api-with-entity-framework-part-4.md)
> [下一页](using-web-api-with-entity-framework-part-6.md)
