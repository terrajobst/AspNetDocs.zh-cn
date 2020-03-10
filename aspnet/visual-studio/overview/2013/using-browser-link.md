---
uid: visual-studio/overview/2013/using-browser-link
title: 在 Visual Studio 2013 中使用浏览器链接Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/04/2013
ms.assetid: 46cbfe20-b4dc-449b-9016-80657dd44fbe
msc.legacyurl: /visual-studio/overview/2013/using-browser-link
msc.type: authoredcontent
ms.openlocfilehash: 723a38de4569b0bb58817c70aabb84fef8e19591
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78505202"
---
# <a name="using-browser-link-in-visual-studio-2013"></a>在 Visual Studio 2013 中使用浏览器链接

作者： [Mike Wasson](https://github.com/MikeWasson)

Browser 链接是 Visual Studio 2013 中的一项新功能，它在开发环境和一个或多个 web 浏览器之间创建信道。 您可以使用浏览器链接一次刷新多个浏览器中的 web 应用程序，这对于跨浏览器测试非常有用。

- [浏览器刷新](#browser-refresh)
- [查看浏览器链接仪表板](#dashboard)
- [为静态 HTML 文件启用浏览器链接](#static-html)
- [禁用浏览器链接](#disabling)
- [它的工作原理是什么？](#how-it-works)

<a id="browser-refresh"></a>
## <a name="browser-refresh"></a>浏览器刷新

使用浏览器刷新，可以刷新通过浏览器链接连接到 Visual Studio 的多个浏览器。

若要使用浏览器刷新，请首先使用任意项目模板创建 ASP.NET 应用程序。 按 F5 或单击工具栏中的箭头图标来调试应用程序：

![](using-browser-link/_static/image1.png)

你还可以使用下拉列表选择特定的浏览器进行调试。

![](using-browser-link/_static/image2.png)

若要通过多个浏览器进行调试，请选择 "**浏览方式**"。 在 "**浏览**" 对话框中，按住 CTRL 键以选择多个浏览器。 单击 "**浏览**" 以通过所选浏览器进行调试。 如果从 Visual Studio 外部启动浏览器并导航到应用程序 URL，则浏览器链接也起作用。

![](using-browser-link/_static/image3.png)

浏览器链接控件位于包含环形箭头图标的下拉列表中。 箭头图标为 "**刷新**" 按钮。

![](using-browser-link/_static/image4.png)

若要查看连接了哪些浏览器，请在调试时将鼠标悬停在 "**刷新**" 按钮上。 已连接的浏览器将显示在工具提示窗口中。

![](using-browser-link/_static/image5.png)

若要刷新连接的浏览器，请单击 "**刷新**" 按钮或按 CTRL + ALT + enter。 例如，以下屏幕截图显示了我使用 MVC 5 项目模板创建的 ASP.NET 项目。 可以在顶部看到两个浏览器中运行的应用程序。 在底部，项目在 Visual Studio 中打开。

![](using-browser-link/_static/image6.png)

在 Visual Studio 中，我更改了主页的 &lt;h1&gt; 标题：

![](using-browser-link/_static/image7.png)

单击 "**刷新**" 按钮时，更改会出现在浏览器窗口中：

![](using-browser-link/_static/image8.png)

**注意**

- 若要启用浏览器链接，请在项目的 Web.config 文件中的[&lt;编译&gt;](https://msdn.microsoft.com/library/s10awwz0(v=vs.85).aspx)元素中设置 `debug=true`。
- 应用程序必须在 localhost 上运行。
- 应用程序必须面向 .NET 4.0 或更高版本。

<a id="dashboard"></a>
## <a name="viewing-the-browser-link-dashboard"></a>查看浏览器链接仪表板

浏览器链接仪表板显示有关浏览器链接连接的信息。 若要查看仪表板，请选择 "浏览器链接" 下拉菜单（"**刷新**" 按钮旁边的小箭头）。 然后单击 "**浏览器链接仪表板**"。

![](using-browser-link/_static/image9.png)

面板列出了连接的浏览器以及每个浏览器导航到的 URL。

![](using-browser-link/_static/image10.png)

"**先决条件**" 部分显示为该项目启用浏览器链接所需的任何步骤。 例如，以下屏幕截图显示了 Web.config 文件中的 "debug" 设置为 false 的项目。

![](using-browser-link/_static/image11.png)

<a id="static-html"></a>
## <a name="enabling-browser-link-for-static-html-files"></a>为静态 HTML 文件启用浏览器链接

若要为静态 HTML 文件启用浏览器链接，请将以下项添加到 web.config 文件中。

[!code-xml[Main](using-browser-link/samples/sample1.xml)]

出于性能方面的考虑，请在发布项目时删除此设置。

<a id="disabling"></a>
## <a name="disabling-browser-link"></a>禁用浏览器链接

默认情况下启用浏览器链接。 可以通过多种方式来禁用它：

- 在 "浏览器链接" 下拉菜单中，取消选中 "**启用浏览器链接**"。 

    ![](using-browser-link/_static/image12.png)
- 在 web.config 文件中，在 appSettings 节中添加一个名为 "vs： EnableBrowserLink" 的项，其值为 "false"。 

    [!code-xml[Main](using-browser-link/samples/sample2.xml)]
- 在 web.config 文件中，将 "debug" 设置为 "false"。 

    [!code-xml[Main](using-browser-link/samples/sample3.xml)]

<a id="how-it-works"></a>
## <a name="how-does-it-work"></a>它的工作原理是什么？

Browser Link 使用[SignalR](../../../signalr/index.md)在 Visual Studio 与浏览器之间创建信道。 启用浏览器链接后，Visual Studio 将充当 SignalR 服务器，多个客户端（浏览器）可以连接到该服务器。 浏览器链接还向 ASP.NET 注册 HTTP 模块。 此模块从服务器中插入特殊 &lt;脚本&gt; 对每个页面请求的引用。 可以通过在浏览器中选择 "查看源" 来查看脚本引用。

![](using-browser-link/_static/image13.png)

不会修改您的源文件。 HTTP 模块动态地插入脚本引用。

由于浏览器端代码都是 JavaScript，因此它适用于[SignalR 支持](../../../signalr/overview/getting-started/supported-platforms.md)的所有浏览器，无需任何浏览器插件。
