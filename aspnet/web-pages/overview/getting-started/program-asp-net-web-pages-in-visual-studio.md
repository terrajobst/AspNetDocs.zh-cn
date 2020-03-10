---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: 使用 Visual Studio 进行编程 ASP.NET 网页（Razor） |Microsoft Docs
author: Rick-Anderson
description: 本附录介绍了如何使用 Visual Studio 2010 或 Visual Web Developer 2010 Express 通过 Razor 语法来编程 ASP.NET 网页。
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78514292"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a>使用 Visual Studio 的编程 ASP.NET 网页（Razor）

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何使用 Visual Studio 或 Visual Web Developer Express 来计划 ASP.NET 网页（Razor）网站。
>
> 学习内容
>
> - 需要安装的内容（如果有），才能使用版本的 Visual Studio 中的 ASP.NET 网页。
> - 如何向 Visual Web Developer 2010 Express 添加对 ASP.NET 网页的支持。
> - 如何使用 Visual Studio 中的功能来处理 ASP.NET Razor 页面，包括 IntelliSense 和调试器。
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
>
>
> - ASP.NET 网页（Razor）3
> - Visual Studio 2013
> - WebMatrix 3
>
>
> 本教程还适用于 ASP.NET 网页2、Visual Studio 2012、Visual Studio 2010 和 WebMatrix 2。

您可以使用 WebMatrix 或许多其他代码编辑器通过 Razor 语法来编写 ASP.NET 网页。 你还可以使用 Microsoft Visual Studio 功能齐全的集成开发环境（IDE），它提供了一组功能强大的工具，可用于创建许多类型的应用程序（而不仅仅是网站）。 若要使用 ASP.NET Razor 页面，可以使用[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。

Visual Studio 提供的两个特别有用的功能可用于通过 ASP.NET Razor 网页进行编程：

- *IntelliSense*。 Visual Studio 中内置的 IntelliSense 功能比 WebMatrix 中的 IntelliSense 更为全面。
- *调试器*。 调试器允许您通过在程序运行、检查变量和逐行执行代码行的过程中停止程序来对代码进行故障排除。

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a>将 Visual Studio 与不同版本的 ASP.NET 网页一起使用

若要在 Visual Studio 2017 中开发 ASP.NET web 应用，请安装**ASP.NET 和 web 开发**工作负荷。

Visual Studio 2012 和 Visual Studio 2013 包括对 ASP.NET 网页的支持。 （安装 Visual Studio 时，会安装支持 ASP.NET 网页所需的包。）

默认情况下，Visual Studio 2010 不支持 ASP.NET 网页。 若要将 ASP.NET 网页与 Visual Studio 2010 一起使用，必须安装 ASP.NET MVC 包。 若要获取 ASP.NET 网页2，请安装 ASP.NET MVC 4。

下表汇总了对不同版本的 Visual Studio 中 ASP.NET 网页的支持。

|  | Visual Studio 2010 | Visual Studio 2012 | Visual Studio 2013 |
| --- | --- | --- | --- |
| **ASP.NET 网页2** | 安装 ASP.NET MVC 4 | 处于 | 处于 |
| **ASP.NET 网页3** |  | 通过 NuGet 更新到 ASP.NET 网页3 | 处于 |

若要使用 Visual Studio 2010，请参阅[安装 Visual studio 2010 中的 ASP.NET 网页支持](#vs2010support)。

## <a name="launching-visual-studio-from-webmatrix"></a>从 WebMatrix 启动 Visual Studio

如果已在 WebMatrix 中启动项目，并且想要切换到 Visual Studio，WebMatrix 提供了一个按钮，可以在 Visual Studio 中轻松打开项目。 若要启用此按钮，您必须在计算机上安装 Visual Studio。 下图显示了 WebMatrix 中的按钮。

![启动 Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

单击该按钮时，将在 Visual Studio 中打开该项目。 您可以在 WebMatrix 和 Visual Studio 之间来回切换，而不会出现任何问题。 如果其他环境中的任何文件发生了更改，则会收到通知，需要重新加载才能获得最新的更改。

## <a name="creating-aspnet-razor-site-in-visual-studio"></a>在 Visual Studio 中创建 ASP.NET Razor 网站

若要在 Visual Studio 中创建 ASP.NET Razor 网站：

1. 打开 Visual Studio。
2. 在 "**文件**" 菜单中，单击 "**新建**网站"。

    ![创建新网站](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. 在 "**新建**网站" 对话框中，选择要使用的语言（视觉C#对象或 Visual Basic）。
4. 选择**ASP.NET 网站（Razor）** 模板。

    ![razor 网站](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. 单击“确定”。

你的新项目存在，并填充了一些默认网页来帮助你入门。

### <a name="using-intellisense"></a>Using IntelliSense

现在，你已创建了一个网站，可以在 Visual Studio 中了解 IntelliSense 的工作方式。

1. 在刚创建的网站中，打开 "*默认.* #" 页。
2. 在页面的 `<h3>` 标记后，键入 `@ServerInfo.` （包括点）。 请注意 IntelliSense 如何在下拉列表中显示 `ServerInfo` 帮助器的可用方法。

    ![intellisense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. 从列表中选择 `GetHtml` 方法，然后按 Enter。 IntelliSense 自动填充方法。 （与中C#的任何方法一样，必须在方法之后添加 `()` 字符。）已完成的 `GetHtml` 方法代码类似于以下示例：

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. 按 Ctrl + F5 运行页面。 这是在浏览器中显示页面时的样子：

    ![浏览器中的默认页](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. 关闭浏览器。

### <a name="using-the-debugger"></a>使用调试器

1. 在默认的 " *cshtml* " 页的顶部，在 "`Page.Title`开头的行后添加以下代码行：

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. 在编辑器的灰色边距中，单击此新行旁边的，以便添加*断点*。 断点是通知调试器在该点停止运行程序的标记，这样您就可以看到发生了什么情况。

    ![设置断点](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. 删除对 `ServerInfo.GetHtml` 方法的调用，并在其位置添加对 `@myTime` 变量的调用。 此调用显示新代码行返回的当前时间值。
4. 按 F5 在调试器中运行该页面。 该页在你设置的断点处停止。 下图显示了在具有断点（黄色）的编辑器中，页面的外观。

    ![调试断点](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. 在 "调试" 工具栏中，单击 "**单步**执行" 按钮（或按 F11）以运行下一行代码。 每次单击此按钮时，会将执行前进到下一行代码。

    !["单步执行" 按钮](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. 通过将鼠标指针悬停在 `myTime` 变量上，或通过检查在 "**局部变量**" 和 "**调用堆栈**" 窗口中显示的值来检查变量的值。 Visual Studio 将显示变量的值。

    ![显示时间值](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. 完成检查变量并单步执行代码后，按 F5 继续运行页面，而不会在每一行停止。 完成所有代码的逐句后，浏览器将显示该页。

若要了解有关调试器以及如何在 Visual Studio 中调试代码的详细信息，请参阅[演练：在 Visual Web Developer 中调试网页](https://msdn.microsoft.com/library/z9e7w6cs.aspx)。

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a>使用 Visual Studio 在 ASP.NET MVC 项目中使用 Razor

Razor 语法还广泛地用于 ASP.NET MVC 项目。 MVC 是一种功能强大的基于模式的方式，用于生成动态网站。 如果 ASP.NET 网页站点难以维护，则可以考虑将其转换为 ASP.NET MVC 应用程序。 有关创建 MVC 应用程序的示例，请参阅[入门 with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md)。

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a>在 Visual Studio 2010 中安装 ASP.NET 网页支持

本部分介绍如何安装 Visual Web Developer Express 2010 和适用于 Visual Studio 的 ASP.NET 网页工具。

1. 如果还没有 Web 平台安装程序，请从以下 URL 下载：

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. 运行 Web 平台安装程序。
3. 单击 "**产品**" 选项卡。

    ![WebPI 产品选项卡](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. 搜索**ASP.NET MVC 4** （对于 ASP.NET 网页2），然后单击 "**添加**"。 这些产品包括用于生成 ASP.NET Razor 网站的 Visual Studio 工具。

    ![WebPi 安装选项](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. 单击 "**安装**" 以完成安装。
