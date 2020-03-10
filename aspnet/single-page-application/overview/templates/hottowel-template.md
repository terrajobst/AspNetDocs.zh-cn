---
uid: single-page-application/overview/templates/hottowel-template
title: 热的纸巾模板 |Microsoft Docs
author: madskristensen
description: HotTowel 模板
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467138"
---
# <a name="hot-towel-template"></a>Hot Towel 模板

作者： [Mads Kristensen](https://github.com/madskristensen)

> Papa 作者编写的
> 
> 选择要下载的版本：
> 
> [适用于 Visual Studio 2012 的热式纸巾 MVC 模板](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [Visual Studio 2013 的热的纸巾 MVC 模板](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> 热的，因为你不希望再转向 SPA！

想要生成 SPA，但不能决定从何处开始？ 使用热的纸巾，以秒为单位，你将拥有一个 SPA 和构建所需的所有工具。

"ASP.NET" 创建了一个很好的起点。 这种情况下，它为代码提供了模块化结构，可查看导航、数据绑定、丰富的数据管理以及简单而精致的样式。 热向下提供了构建 SPA 所需的一切，使你可以专注于应用，而不是管道。

> 详细了解如何从[John Papa 的视频、教程和 Pluralsight 课程](http://johnpapa.net/spa?vsix)构建 SPA。

## <a name="application-structure"></a>应用程序结构

"热的纸巾 SPA" 提供了一个应用文件夹，其中包含定义应用程序的 JavaScript 和 HTML 文件。

在 App 文件夹内：

- durandal
- 服务
- viewmodel
- 视图

应用文件夹包含模块的集合。 这些模块封装了功能并声明了其他模块上的依赖关系。 Views 文件夹包含应用程序的 HTML，viewmodel 文件夹包含视图的表示逻辑（一种公共 MVVM 模式）。 "服务" 文件夹非常适合用于容纳应用程序可能需要的任何常用服务，例如 HTTP 数据检索或本地存储交互。 多个 viewmodel 经常从服务模块重用代码。

## <a name="aspnet-mvc-server-side-application-structure"></a>ASP.NET MVC 服务器端应用程序结构

《热版，在熟悉且功能强大的 ASP.NET MVC 结构上构建。

- 应用\_启动
- 内容
- Controllers
- 模型
- 脚本
- 视图

## <a name="featured-libraries"></a>特色库

- ASP.NET MVC
- ASP.NET Web API
- ASP.NET Web 优化-捆绑和缩减
- 简单的[.js](http://Breezejs.com) -丰富的数据管理
- [Durandal](http://Durandaljs.com) -导航和查看组合
- [挖空](http://Knockoutjs.com)的数据绑定
- [要求 .js](http://requirejs.org) -具有 AMD 和优化的模块化
- [Toastr](http://jpapa.me/c7toastr) -弹出消息
- [Twitter 引导](https://twitter.github.com/bootstrap/)-强健的 CSS 样式

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a>通过 Visual Studio 2012 热视频 SPA 模板进行安装

可以将热式安装为 Visual Studio 2012 模板。 只需单击 "`File` | " `New Project` 并选择 "`ASP.NET MVC 4 Web Application`"。 然后选择 "热的单页面应用程序" 模板并运行！

## <a name="installing-via-the-nuget-package"></a>通过 NuGet 包安装

ASP.NET 也是一个 NuGet 包，用于补充现有的空的 MVC 项目。 只需使用 Nuget 安装，然后运行！

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a>如何在 ws-i 上构建？

只需开始添加代码！

1. 添加自己的服务器端代码，最好是实体框架和 WebAPI （这与）
2. 将视图添加到 `App/views` 文件夹
3. 将 viewmodel 添加到 `App/viewmodels` 文件夹
4. 将 HTML 和挖空数据绑定添加到新视图
5. 更新中的导航路由 `shell.js`

## <a name="walkthrough-of-the-htmljavascript"></a>HTML/JavaScript 演练

### <a name="viewshottowelindexcshtml"></a>Views/HotTowel/index.cshtml

索引为 MVC 应用程序的起始路由和视图。 它包含所需的所有标准 meta 标记、css 链接和 JavaScript 引用。 正文包含单个 `<div>`，其中的所有内容（你的视图）都将在请求时放置。 `@Scripts.Render` 使用需要 node.js 来运行应用程序代码的入口点，它包含在 `main.js` 文件中。 提供了一个初始屏幕，用于演示如何在应用程序加载时创建初始屏幕。

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a>App/main.js

`main.js` 文件包含将在你的应用程序加载后立即运行的代码。 这是要在其中定义导航路由、设置启动视图和执行任何安装程序/引导（如填充应用程序的数据）的位置。

`main.js` 文件定义了 durandal 的多个模块，以帮助应用程序启动。 Define 语句可帮助解析模块依赖项，以便它们可用于函数。 首先启用了调试消息，这会将有关应用程序正在执行的事件的消息发送到控制台窗口。 Durandal 框架用于启动应用程序。 设置约定，以便 durandal 知道所有视图和 viewmodel 分别包含在相同的命名文件夹中。 最后，`app.setRoot` 启动使用预定义 `entrance` 动画加载 `shell`。

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a>视图

视图位于 `App/views` 文件夹中。

### <a name="shellhtml"></a>shell.html

`shell.html` 包含 HTML 的母版布局。 你的所有其他视图将在你的 `shell` 视图的某个地方组合在一起。 "热 `shell`" 提供了包含三个这类区域的：页眉、内容区域和页脚。 在请求时，其中的每个区域都将与其他视图的内容一起加载。

标头和表尾的 `compose` 绑定将分别指向 `nav` 和 `footer` 视图。 `#content` 节的撰写绑定绑定到 `router` 模块的活动项。 换句话说，单击导航链接时，将在此区域中加载其对应的视图。

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a>nav.html

`nav.html` 包含 SPA 的导航链接。 例如，可以在此处放置菜单结构。 这通常是数据绑定（使用挖空）到 `router` 模块，以显示在 `shell.js`中定义的导航。 挖空会查找数据绑定属性，并将其绑定到 `shell` viewmodel 以显示导航路由，并将其绑定到 `router` 模块处于从一个视图导航到另一个视图（请参阅 `router.isNavigating`）的情况。

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a>home. html 和详细信息

这些视图包含用于自定义视图的 HTML。 单击 "`nav` 视图" 菜单中的 "`home`" 链接时，将在 "`shell`" 视图的 "内容" 区域中放置 `home` 视图。 可以扩充这些视图或将其替换为你自己的自定义视图。

### <a name="footerhtml"></a>footer.html

`footer.html` 包含在 `shell` 视图底部的脚注中显示的 HTML。

## <a name="viewmodels"></a>ViewModels

在 `App/viewmodels` 文件夹中找到 Viewmodel。

### <a name="shelljs"></a>shell.js

`shell` viewmodel 包含绑定到 `shell` 视图的属性和函数。 这通常是在其中找到菜单导航绑定的位置（请参阅 `router.mapNav` 逻辑）。

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a>node.js 和详细信息

这些 viewmodel 包含绑定到 `home` 视图的属性和函数。 它还包含视图的呈现逻辑，是数据和视图之间的粘附。

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a>服务

服务位于 "应用/服务" 文件夹中。 理想情况下，您可以将将来的服务（如 dataservice 模块）用于获取和发布远程数据。

### <a name="loggerjs"></a>logger.js

"暖色" 在 "服务" 文件夹中提供 `logger` 模块。 `logger` 模块非常适合用于将消息记录到控制台和弹出 toast 中的用户。
