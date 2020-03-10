---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: 创建新的 ASP.NET MVC 项目 |Microsoft Docs
author: microsoft
description: 步骤1说明了如何就地放置基本 NerdDinner 应用程序结构。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469238"
---
# <a name="create-a-new-aspnet-mvc-project"></a>新建 ASP.NET MVC 项目

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的第1步，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤1说明了如何就地放置基本 NerdDinner 应用程序结构。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner 步骤1：文件-&gt;新项目

在 Visual Studio 2008 或免费的 Visual Web Developer 2008 Express 中，通过选择 "**文件&gt;新的" 项目**"菜单项开始我们的 NerdDinner 应用程序。

这将显示 "新建项目" 对话框。 若要创建新的 ASP.NET MVC 应用程序，我们将选择对话框左侧的 "Web" 节点，然后选择右侧的 "ASP.NET MVC Web 应用程序" 项目模板：

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*重要提示：请确保已下载并安装 ASP.NET MVC-否则它不会显示在 "新建项目" 对话框中。如果尚未安装，则可以使用[Microsoft Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)的 V2 （在 "Web 平台-&gt;框架和运行时" 一节中提供了 ASP.NET MVC）。*

我们会将新项目命名为 "NerdDinner"，然后单击 "确定" 按钮进行创建。

单击 "确定" 时，Visual Studio 将显示一个额外的对话框，提示我们还可以选择为新应用程序创建单元测试项目。 此单元测试项目使我们能够创建自动测试来验证应用程序的功能和行为（我们将在本教程的后面部分介绍如何执行此操作）。

![](create-a-new-aspnet-mvc-project/_static/image2.png)

以上对话框中的 "测试框架" 下拉列表中填充了计算机上安装的所有可用 ASP.NET MVC 单元测试项目模板。 可下载的版本可用于 NUnit、MBUnit 和 XUnit。 此外，还支持内置 Visual Studio 单元测试框架。

*注意： Visual Studio 单元测试框架仅适用于 Visual Studio 2008 Professional 和更高版本。如果使用 VS 2008 Standard Edition 或 Visual Web Developer 2008 Express，则需要下载并安装 ASP.NET MVC 的 NUnit、MBUnit 或 XUnit 扩展，以便显示此对话框。如果未安装任何测试框架，则不会显示该对话框。*

我们将使用我们创建的测试项目的默认 "NerdDinner" 名称，并使用 "Visual Studio 单元测试" 框架选项。 单击 "确定" 按钮时，Visual Studio 将为我们创建一个包含两个项目的解决方案-一个用于我们的 web 应用程序，另一个用于我们的单元测试：

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>检查 NerdDinner 目录结构

当使用 Visual Studio 创建新的 ASP.NET MVC 应用程序时，它会自动将许多文件和目录添加到项目中：

![](create-a-new-aspnet-mvc-project/_static/image4.png)

默认情况下，ASP.NET MVC 项目具有六个顶级目录：

| **目录** | **目的** |
| --- | --- |
| **/Controllers** | 放置处理 URL 请求的控制器类的位置 |
| **/Models** | 放置表示和操作数据的类的位置 |
| **/Views** | 放置负责呈现输出的 UI 模板文件的位置 |
| **/Scripts** | 在其中放置 JavaScript 库文件和脚本（.js） |
| **/Content** | 放置 CSS 和映像文件的位置以及其他非动态/非 JavaScript 内容 |
| **/App\_数据** | 存储要读取/写入的数据文件的位置。 |

ASP.NET MVC 不需要此结构。 事实上，处理大型应用程序的开发人员通常会在多个项目中对应用程序进行分区，以使其更易于管理（例如：数据模型类通常与 web 应用程序在单独的类库项目中）。 不过，默认的项目结构提供了一个非常好的默认目录约定，可以使用它来使应用程序保持干净整洁。

展开/Controllers 目录后，我们会发现，Visual Studio 会将两个控制器类（HomeController 和 AccountController）添加到项目中：

![](create-a-new-aspnet-mvc-project/_static/image5.png)

当我们展开/Views 目录时，将在默认情况下，找到三个子目录–/Home、/Account 和/Shared –其中的多个模板文件也会添加到项目中：

![](create-a-new-aspnet-mvc-project/_static/image6.png)

展开 "/Content" 和 "/Scripts" 目录时，会找到一个用于为站点上的所有 HTML 提供样式的 web.config 文件，以及可以在应用程序中启用 ASP.NET AJAX 和 jQuery 支持的 JavaScript 库：

![](create-a-new-aspnet-mvc-project/_static/image7.png)

展开 NerdDinner 项目时，我们会看到两个包含控制器类的单元测试的类：

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Visual Studio 添加的这些默认文件为我们提供了一个用于工作的工作应用程序的基本结构，即主页、页面、帐户登录/注销/注册页和未经处理的错误页（所有有线和开箱即用）。

### <a name="running-the-nerddinner-application"></a>运行 NerdDinner 应用程序

可以通过选择 "**调试"&gt;、"启动调试**" 或 "**调试-&gt;启动而不调试**" 菜单项来运行项目：

![](create-a-new-aspnet-mvc-project/_static/image9.png)

这将启动 Visual Studio 附带的内置 ASP.NET Web 服务器，并运行应用程序：

![](create-a-new-aspnet-mvc-project/_static/image10.png)

下面是新项目（URL： "/"）在运行时的主页：

![](create-a-new-aspnet-mvc-project/_static/image11.png)

单击 "关于" 选项卡将显示 "关于" 页（URL： "/Home/About"）：

![](create-a-new-aspnet-mvc-project/_static/image12.png)

单击右上方的 "登录" 链接将转到登录页（URL： "/Account/LogOn"）

![](create-a-new-aspnet-mvc-project/_static/image13.png)

如果没有登录帐户，我们可以单击 "注册" 链接（URL： "/Account/Register"）创建一个：

![](create-a-new-aspnet-mvc-project/_static/image14.png)

默认情况下，在创建新项目时，会添加用于实现上述 home、about 和注销/注册功能的代码。 我们会将其用作应用程序的起点。

### <a name="testing-the-nerddinner-application"></a>测试 NerdDinner 应用程序

如果使用的是专业版或更高版本的 Visual Studio 2008，则可以使用 Visual Studio 中的内置单元测试 IDE 支持来测试项目：

![](create-a-new-aspnet-mvc-project/_static/image15.png)

选择上述选项之一将打开 IDE 中的 "测试结果" 窗格，并在包含在新项目中的27个单元测试中为我们提供 "通过/失败" 状态，涵盖内置功能：

![](create-a-new-aspnet-mvc-project/_static/image16.png)

稍后在本教程中，我们将详细介绍自动测试，并添加其他涵盖我们实现的应用程序功能的单元测试。

### <a name="next-step"></a>下一步

现在，我们已经获得了一个基本的应用程序结构。 现在，让我们[创建一个用于存储应用程序数据的数据库](create-a-database.md)。

> [!div class="step-by-step"]
> [上一页](introducing-the-nerddinner-tutorial.md)
> [下一页](create-a-database.md)
