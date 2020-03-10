---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: 创建 JavaScript 客户端 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504722"
---
# <a name="create-the-javascript-client"></a>创建 JavaScript 客户端

作者： [Mike Wasson](https://github.com/MikeWasson)

[下载完成的项目](https://github.com/MikeWasson/BookService)

在本部分中，你将使用 HTML、JavaScript 和[挖空的 node.js](http://knockoutjs.com/)库创建应用程序的客户端。 我们将分阶段生成客户端应用：

- 显示书籍列表。
- 显示书籍详细信息。
- 添加新书籍。

挖空库使用模型-视图-ViewModel （MVVM）模式：

- **模型**是业务域中的数据的服务器端表示形式（在我们的示例中为书籍和作者）。
- **视图**为表示层（HTML）。
- **视图模型**是保存模型的 JavaScript 对象。 视图模型是 UI 的代码抽象。 它不知道 HTML 表示形式。 相反，它表示视图的抽象功能，如&quot;&quot;书籍的列表。

视图被数据绑定到视图模型。 视图模型的更新会自动反映在视图中。 视图模型还可从视图中获取事件，如按钮单击。

![](part-6/_static/image1.png)

此方法可以轻松地更改应用的布局和 UI，因为可以更改绑定，而无需重写任何代码。 例如，可以将项目列表显示为 `<ul>`，然后将其更改为表。

## <a name="add-the-knockout-library"></a>添加挖空库

在 Visual Studio 中，从“工具”菜单中选择“NuGet 包管理器”。 然后选择 "**程序包管理器控制台**"。 在“Package Manager Console”窗口中，输入以下命令：

[!code-console[Main](part-6/samples/sample1.cmd)]

此命令将挖空文件添加到 Scripts 文件夹。

## <a name="create-the-view-model"></a>创建视图模型

将名为 node.js 的 JavaScript 文件添加到 Scripts 文件夹。 （在解决方案资源管理器中，右键单击 "脚本" 文件夹，选择 "**添加**"，然后选择 " **JavaScript 文件**"。）粘贴以下代码：

[!code-javascript[Main](part-6/samples/sample2.js)]

在挖空中，`observable` 类启用数据绑定。 当可观察的内容发生更改时，可观察的会通知所有数据绑定控件，因此它们可以自行更新。 （`observableArray` 类是可*观察*的数组版本。）首先，我们的视图模型有两个可观察量：

- `books` 包含书籍的列表。
- 如果 AJAX 调用失败，`error` 将包含一条错误消息。

`getAllBooks` 方法进行 AJAX 调用以获取书籍列表。 然后将结果推送到 `books` 数组。

`ko.applyBindings` 方法是挖空库的一部分。 它将视图模型作为参数，并设置数据绑定。

## <a name="add-a-script-bundle"></a>添加脚本捆绑包

绑定是 ASP.NET 4.5 中的一项功能，它使你可以轻松地将多个文件组合或捆绑到一个文件中。 绑定可减少向服务器发出的请求数，从而提高页面加载时间。

打开文件应用\_Start/BundleConfig。 将以下代码添加到 RegisterBundles 方法。

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> [上一页](part-5.md)
> [下一页](part-7.md)
