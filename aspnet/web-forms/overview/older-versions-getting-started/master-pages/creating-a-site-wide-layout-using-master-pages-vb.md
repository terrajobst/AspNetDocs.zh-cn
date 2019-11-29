---
uid: web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
title: 使用母版页创建站点范围的布局（VB） |Microsoft Docs
author: rick-anderson
description: 本教程将演示母版页基础知识。 也就是说，母版页是什么，如何创建母版页，什么是内容占位符，如何使用一个 cr 。
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 30945276-8ed9-4b27-8e50-4309244d3559
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: c0ee6ed9d944b9a8ff2b2996e93706b8416de905
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74584316"
---
# <a name="creating-a-site-wide-layout-using-master-pages-vb"></a>使用母版页创建站点范围内布局 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_01_VB.zip)或[下载 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_01_VB.pdf)

> 本教程将演示母版页基础知识。 也就是说，母版页是什么、母版页如何创建母版页、什么是内容占位符、如何创建使用母版页的 ASP.NET 页、修改母版页在其关联的内容页中的自动反映方式等。

## <a name="introduction"></a>简介

设计良好的网站的一个特性是站点范围内一致的页面布局。 例如，学习 www.asp.net 网站。 撰写本文时，每个页面的顶部和底部都具有相同的内容。 如图1所示，每个页面的顶部都显示一个包含 Microsoft 社区列表的灰色栏。 这是网站徽标，其中包含已翻译的网站的语言列表，以及核心部分：家庭版、入门版、学习版、下载版等。 同样，页面底部还包括有关 www.asp.net 上的广告、版权声明和隐私声明的链接的信息。

[![www.asp.net 网站在所有页面中采用一致的外观](creating-a-site-wide-layout-using-master-pages-vb/_static/image2.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image1.png)

<strong>图 01</strong>： www.asp.net 网站在所有页面中采用一致的外观（[单击查看全尺寸图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image3.png)）

设计良好的网站的另一个属性是可以轻松地更改网站的外观。 图1显示了2008年3月之前的 www.asp.net 主页，但在此教程中，外观可能已更改。 可能顶部的菜单项将扩展为包含 MVC 框架的新部分。 或许有不同颜色、字体和布局的全新设计是公开了的。 将此类更改应用到整个站点应该是一个快速而简单的过程，无需修改组成网站的数千个网页。

通过使用*母版页*，可以在 ASP.NET 中创建站点范围的页面模板。 简而言之，母版页是一种特殊类型的 ASP.NET 页面，用于定义所有*内容页*中通用的标记，以及在内容页上按内容自定义的区域。 （内容页是绑定到母版页的 ASP.NET 页面。）只要更改了母版页的布局或格式设置，它的所有内容页的输出也会立即更新，这使得应用站点范围的外观与更新和部署单个文件（即母版页）一样简单。

这是一系列教程中的第一篇教程，其中介绍了如何使用母版页。 在本系列教程中，我们将：

- 检查创建母版页及其关联的内容页，
- 讨论各种提示、技巧和陷阱，
- 确定常见的母版页缺陷并探索解决方法，
- 请参阅如何从内容页访问母版页，反之亦然。
- 了解如何在运行时指定内容页的母版页，以及
- 其他高级母版页主题。

这些教程旨在简洁明了，并提供有关多个屏幕截图的分步说明，以直观地完成此过程。 每个教程都在C#和 Visual Basic 版本中提供，并包括所使用的完整代码的下载。

本便捷性教程首先介绍母版页的基本知识。 我们将讨论母版页的工作原理，查看如何使用 Visual Web Developer 创建母版页和关联的内容页，以及如何在其内容页中立即反映母版页的更改。 让我们进入正题！

## <a name="understanding-how-master-pages-work"></a>了解母版页的工作方式

构建具有一致站点范围的页面布局的网站要求每个网页发出常见格式标记以及其自定义内容。 例如，虽然 www.asp.net 上的每个教程或论坛帖子都具有自己独特的内容，但每个页面还会呈现一系列常见 `<div>` 元素，这些元素显示了顶层部分链接： Home、入门、学习等。

有多种方法可以创建具有一致外观的网页。 一种简单的方法是将通用布局标记复制并粘贴到所有网页中，但这种方法有很多缺点。 对于初学者，每次创建新页面时，都必须记得将共享内容复制并粘贴到页面中。 此类复制和粘贴操作对错误准备好，因为可能会意外地将共享标记的一个子集复制到新页中。 然后，这种方法可以将现有站点范围内的外观替换为新的，因为必须对站点中的每个页面进行编辑才能使用新的外观。

在 ASP.NET 版本2.0 之前，页面开发人员通常将常见标记放在[用户控件](https://msdn.microsoft.com/library/y6wb1a0e.aspx)中，然后将这些用户控件添加到每个页面。 这种方法要求页面开发人员记得手动将用户控件添加到每个新页面，但允许进行站点范围的更简单的修改，因为当只更新需要修改的用户控件时。 遗憾的是，Visual Studio .NET 2002 和 2003-用于创建 ASP.NET 1.x 应用程序的 Visual Studio 版本（设计视图中显示为灰色框）。 因此，使用此方法的页开发人员并不喜欢所见即所得的设计时环境。

使用用户控件的缺点在 ASP.NET 版本2.0 和 Visual Studio 2005 中进行了介绍，其中包含*母版页*。 母版页是一种特殊类型的 ASP.NET 页面，用于定义站点范围内的标记和关联的*内容页*定义其自定义标记的*区域*。 如我们将在步骤1中看到的，这些区域由 ContentPlaceHolder 控件定义。 ContentPlaceHolder 控件只是表示母版页控件层次结构中的一个位置，其中的自定义内容可由内容页注入。

> [!NOTE]
> ASP.NET 版本2.0 后，母版页的核心概念和功能尚未更改。 但是，Visual Studio 2008 为嵌套母版页提供设计时支持，这是 Visual Studio 2005 中缺少的一项功能。 在将来的教程中，我们将介绍如何使用嵌套母版页。

图2显示了 www.asp.net 的母版页的外观。 请注意，母版页定义公共站点范围的布局-每个页面的顶部、底部和右侧的标记，以及位于左侧的 ContentPlaceHolder （每个单独网页的唯一内容所在的位置）。

![母版页按内容页定义站点范围的布局和每个内容的可编辑区域](creating-a-site-wide-layout-using-master-pages-vb/_static/image4.png)

**图 02**：母版页定义站点范围的布局和内容每个内容页上的可编辑区域

定义母版页后，可以通过 checkbox 的勾选标记将其绑定到新的 ASP.NET 页面。 这些 ASP.NET 页-称为内容页-包含母版页的每个 ContentPlaceHolder 控件的内容控件。 通过浏览器访问内容页时，ASP.NET 引擎将创建母版页的控件层次结构，并将内容页的控件层次结构注入到适当的位置。 将呈现此组合控件层次结构，并将生成的 HTML 返回到最终用户的浏览器。 因此，"内容" 页将同时在其母版页中定义的公共标记和在其自己的内容控件中定义的页特定标记发出 ContentPlaceHolder 控件。 图3说明了这一概念。

[![将请求的页的标记融合到母版页中](creating-a-site-wide-layout-using-master-pages-vb/_static/image6.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image5.png)

**图 03**：请求的页的标记融合到了母版页中（[单击以查看完全大小的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image7.png)）

现在我们已讨论了母版页的工作原理，接下来让我们看看如何使用 Visual Web Developer 创建母版页和关联的内容页。

> [!NOTE]
> 为了吸引到最广泛的受众，我们在本系列教程中生成的 ASP.NET 网站将使用 ASP.NET 3.5 和 Microsoft 的 Visual Studio 2008 （ [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)）版本来创建。 如果尚未升级到 ASP.NET 3.5，别担心，这些教程中讨论的概念同样适用于 ASP.NET 2.0 和 Visual Studio 2005。 但是，某些演示应用程序可能使用 .NET Framework 版本3.5 的新增功能;如果使用了3.5 特定的功能，我将介绍如何在版本2.0 中实现类似功能。 请记住，可从每个教程下载的演示应用程序针对的是 .NET Framework 版本3.5，这将生成一个包含3.5 特定配置元素的 `Web.config` 文件。 简短故事：如果尚未在计算机上安装 .NET 3.5，下载的 web 应用程序将无法运行，而无需先从 `Web.config`中删除3.5 特定标记。 有关本主题的详细信息，请参阅[二级 ASP.NET 版本3.5 的 `Web.config` 文件](http://www.4guysfromrolla.com/articles/121207-1.aspx)。

## <a name="step-1-creating-a-master-page"></a>步骤1：创建母版页

首先，我们需要一个 ASP.NET 网站，然后才能探讨如何创建和使用母版页和内容页。 首先，创建新的基于文件系统的 ASP.NET 网站。 若要实现此目的，请启动 "Visual Web Developer"，然后在 "文件" 菜单中选择 "新建网站"，并显示 "新建网站" 对话框（请参阅图4）。 选择 ASP.NET 网站模板，将 "位置" 下拉列表设置为 "文件系统"，选择要放置该网站的文件夹，并将语言设置为 Visual Basic。 这将创建一个新网站，其中包含 `Default.aspx` ASP.NET "页、一个 `App_Data` 文件夹和一个 `Web.config` 文件。

> [!NOTE]
> Visual Studio 支持以下两种模式的项目管理：网站项目和 Web 应用程序项目。 网站项目缺少项目文件，而 Web 应用程序项目在 Visual Studio .NET 2002/2003 中模拟项目体系结构-它们包含一个项目文件，并将项目的源代码编译到一个程序集中，该程序集放置在 `/bin` 文件夹中。 仅当 Web 应用程序项目模型被引入 Service Pack 1 时，Visual Studio 2005 最初才支持网站项目;Visual Studio 2008 提供两个项目模型。 但是，Visual Web Developer 2005 和2008版本仅支持网站项目。 我在本系列教程中使用网站项目模型进行演示。 如果你使用的是非速成版，并且想要使用[Web 应用程序项目模型](https://msdn.microsoft.com/library/aa730880(vs.80).aspx)，则可以随意执行此操作，但请注意，你在屏幕上看到的内容和所显示的步骤以及这些教程中提供的说明之间可能存在一些差异。

[![创建基于文件系统的新网站](creating-a-site-wide-layout-using-master-pages-vb/_static/image9.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image8.png)

**图 04**：创建新的基于文件系统的网站（[单击查看完全大小的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image10.png)）

接下来，右键单击项目名称，选择 "添加新项"，然后选择 "母版页" 模板，将母版页添加到根目录。 请注意，母版页以扩展名 `.master`结尾。 将这个新的母版页命名 `Site.master` 然后单击 "添加"。

[![将名为 "网站" 的母版页添加到网站](creating-a-site-wide-layout-using-master-pages-vb/_static/image12.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image11.png)

**图 05**：将名为 `Site.master` 的母版页添加到网站（[单击查看完全大小的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image13.png)）

通过 Visual Web Developer 添加新的母版页文件会创建包含以下声明性标记的母版页：

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample1.aspx)]

声明性标记中的第一行是[`@Master` 指令](https://msdn.microsoft.com/library/ms228176.aspx)。 `@Master` 指令类似于 ASP.NET 页面中显示的[`@Page` 指令](https://msdn.microsoft.com/library/ydy4x04a.aspx)。 它定义服务器端语言（VB）以及母版页的代码隐藏类的位置和继承的相关信息。

`DOCTYPE` 和页面的声明性标记出现在 `@Master` 指令下。 此页包含静态 HTML 以及四个服务器端控件：

- **Web 窗体（`<form runat="server">`）** -因为所有 ASP.NET 页面通常都具有 Web 窗体，因此，因为母版页可能包含必须出现在 Web 窗体中的 web 控件，所以请确保将 Web 窗体添加到母版页（而不是向每个内容页添加 web 窗体）。
- **名为 `ContentPlaceHolder1`的 ContentPlaceHolder 控件**-此 ContentPlaceHolder 控件显示在 Web 窗体中，用作内容页的用户界面的区域。
- **服务器端 `<head>` 元素**-`<head>` 元素具有 `runat="server"` 特性，使其可以通过服务器端代码进行访问。 `<head>` 元素以这种方式实现，以便可以通过编程方式添加或调整页面的标题和其他与 `<head>`相关的标记。 例如，设置 ASP.NET 页的 `Title` 属性将更改由 `<head>` 服务器控件呈现的 `<title>` 元素。
- **名为 `head`的 ContentPlaceHolder 控件**-此 ContentPlaceHolder 控件出现在 `<head>` 服务器控件中，可用于以声明方式向 `<head>` 元素添加内容。

此默认母版页声明性标记用作设计你自己的母版页的起点。 可以随意编辑 HTML 或向母版页添加其他 Web 控件或 Contentplaceholder。

> [!NOTE]
> 设计母版页时，请确保母版页包含 Web 窗体并且此 Web 窗体中至少显示了一个 ContentPlaceHolder 控件。

### <a name="creating-a-simple-site-layout"></a>创建简单的站点布局

接下来，展开 `Site.master`的默认声明性标记，以创建所有页面共享的站点布局：公用标头;具有导航、新闻和其他站点范围内容的左侧列;以及显示 "由 Microsoft ASP.NET 支持" 图标的页脚。 图6显示了在浏览器中查看母版页的其中一个内容页时母版页的最终结果。 图6中的红色圆圈区域特定于要访问的页（`Default.aspx`）;其他内容在母版页中定义，因此在所有内容页中都是一致的。

[![母版页定义上、左和下部分的标记](creating-a-site-wide-layout-using-master-pages-vb/_static/image15.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image14.png)

**图 06**：母版页定义上、左和下部分的标记（[单击以查看完全大小的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image16.png)）

若要实现图6中所示的站点布局，请首先更新 `Site.master` 母版页，使其包含以下声明性标记：

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample2.aspx)]

母版页的布局使用一系列 `<div>` HTML 元素进行定义。 `topContent` `<div>` 包含在每页顶部显示的标记，而 `mainContent`、`leftContent`和 `footerContent` `<div>` 用于显示页面的内容、左侧的列和 "按 Microsoft ASP.NET 提供支持" 图标。 除了添加这些 `<div>` 元素外，还会将主 ContentPlaceHolder 控件的 `ID` 属性从 `ContentPlaceHolder1` 重命名为 `MainContent`。

在级联样式表（CSS）文件 `Styles.css`（通过母版页的 `<head>` 元素中的 `<link>` 元素指定）中，会在[级联样式表（CSS）](http://en.wikipedia.org/wiki/Cascading_Style_Sheets)文件中拼写这些 `<div>` 元素的格式设置和布局规则。 这些不同的规则定义上面所述的每个 `<div>` 元素的外观。 例如，`topContent` `<div>` 元素（用于显示 "母版页教程" 文本和链接）在 `Styles.css` 中指定了其格式设置规则，如下所示：

[!code-css[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample3.css)]

如果你正在计算机上进行以下工作，你将需要下载本教程附带的代码，并将 `Styles.css` 文件添加到你的项目中。 同样，你还需要创建一个名为 `Images` 的文件夹，然后将下载的演示网站中的 "由 Microsoft ASP.NET 提供支持" 图标复制到你的项目。

> [!NOTE]
> 对 CSS 和网页格式设置的讨论超出了本文的讨论范围。 有关 CSS 的详细信息，请参阅[W3Schools.com](http://www.w3schools.com/)上的[css 教程](http://www.w3schools.com/css/default.asp)。 我还鼓励您下载本教程附带的代码，并在 `Styles.css` 中开始处理 CSS 设置，以查看不同格式设置规则的效果。

### <a name="creating-a-master-page-using-an-existing-design-template"></a>使用现有设计模板创建母版页

多年来，我为中小型公司构建了许多 ASP.NET 的 web 应用程序。 我的某些客户端要使用现有的站点布局;其他人雇用了一个有能力的图形设计器。 一些用于设计网站布局的委托。 如图6所示，设计网站布局的程序员的任务通常与在您的会计师执行开放心的工作时进行的工作非常明智。

幸运的是，有一些 innumerous 网站提供免费的 HTML 设计模板-Google 为搜索词 "免费网站模板" 返回了6000000多个结果。 我最喜欢的一个是[OpenDesigns.org](http://opendesigns.org/)。找到所需的网站模板后，将 CSS 文件和图像添加到网站项目，并将模板的 HTML 集成到母版页中。

> [!NOTE]
> Microsoft 还提供了许多[免费的 ASP.NET 设计入门工具包模板](https://msdn.microsoft.com/asp.net/aa336613.aspx)，这些模板集成到 Visual Studio 中的 "新建网站" 对话框。

## <a name="step-2-creating-associated-content-pages"></a>步骤2：创建关联的内容页

创建母版页后，便可以开始创建绑定到母版页的 ASP.NET 页面了。 此类页称为 "*内容页*"。

让我们向项目添加一个新的 ASP.NET 页面，并将其绑定到 `Site.master` 母版页。 右键单击 "解决方案资源管理器中的项目名称，然后选择" 添加新项 "选项。 选择 "Web 窗体" 模板，输入名称 `About.aspx`，然后选中 "选择母版页" 复选框，如图7所示。 这样做将显示 "选择母版页" 对话框（见图8），您可以从该对话框中选择要使用的母版页。

> [!NOTE]
> 如果你使用 Web 应用程序项目模型而不是网站项目模型创建了你的 ASP.NET 网站，则在图7所示的 "添加新项" 对话框中将看不到 "选择母版页" 复选框。 若要在使用 Web 应用程序项目模型时创建内容页，您必须选择 Web 内容表单模板而不是 Web 窗体模板。 选择 Web 内容表单模板并单击 "添加" 后，将显示图8中所示的 "选择母版页" 对话框。

[!["添加新内容" 页](creating-a-site-wide-layout-using-master-pages-vb/_static/image18.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image17.png)

**图 07**：添加新的内容页（[单击以查看完全大小的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image19.png)）

[![选择网站。母版页母版页](creating-a-site-wide-layout-using-master-pages-vb/_static/image21.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image20.png)

**图 08**：选择 `Site.master` 的母版页（[单击以查看完全大小的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image22.png)）

如下面的声明性标记所示，新的内容页包含一个 `@Page` 指令，该指令指向其母版页，并为母版页的每个 ContentPlaceHolder 控件提供内容控件。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample4.aspx)]

> [!NOTE]
> 在步骤1中的 "创建简单的站点布局" 部分中，将 `ContentPlaceHolder1` 重命名为 `MainContent`。 如果未以相同方式重命名此 ContentPlaceHolder 控件的 `ID`，则内容页的声明性标记将与上面显示的标记略有不同。 也就是说，第二个内容控件的 `ContentPlaceHolderID` 将反映母版页中对应 ContentPlaceHolder 控件的 `ID`。

呈现内容页时，ASP.NET 引擎必须将页面的内容控件与母版页的 ContentPlaceHolder 控件一起使用。 ASP.NET 引擎根据 `@Page` 指令的 `MasterPageFile` 特性确定内容页的母版页。 如上标记所示，此内容页绑定到 `~/Site.master`。

由于母版页具有两个 ContentPlaceHolder 控件-`head` 和 `MainContent`-Visual Web Developer 生成了两个内容控件。 每个内容控件通过其 `ContentPlaceHolderID` 属性引用特定的 ContentPlaceHolder。

其中，母版页通过以前站点范围内的模板技术来提供支持。 图9显示了通过 Visual Web Developer 的设计视图进行查看时 `About.aspx` 的内容页面。 请注意，母版页内容可见时，它将灰显并且无法修改。 但与母版页的 Contentplaceholder 相对应的内容控件是可编辑的。 与任何其他 ASP.NET 页一样，你可以通过在 "源" 或 "设计" 视图中添加 Web 控件来创建内容页的接口。

["内容" 页的 "设计" 视图 ![显示页面特定内容和母版页内容](creating-a-site-wide-layout-using-master-pages-vb/_static/image24.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image23.png)

**图 09**： "内容" 页的 "设计" 视图显示页面特定内容和母版页内容（[单击以查看完全大小的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image25.png)）

### <a name="adding-markup-and-web-controls-to-the-content-page"></a>将标记和 Web 控件添加到内容页

请花片刻时间为 `About.aspx` 页面创建一些内容。 如图10中所示，我输入了 "关于作者" 标题和几个文本段落，但也可以随意添加 Web 控件。 创建此接口后，通过浏览器访问 `About.aspx` 页面。

[![通过浏览器访问 About 页](creating-a-site-wide-layout-using-master-pages-vb/_static/image27.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image26.png)

**图 10**：通过浏览器访问 `About.aspx` 页面（[单击查看完全尺寸的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image28.png)）

需要了解的是，所请求的内容页及其关联的母版页都已在 web 服务器上全部呈现并呈现为整体。 然后，最终用户的浏览器将发送到生成的带中的 HTML。 若要验证此情况，请转到 "视图" 菜单并选择 "源"，以查看浏览器收到的 HTML。 请注意，没有框架或任何其他用于在单个窗口中显示两个不同网页的专用技术。

### <a name="binding-a-master-page-to-an-existing-aspnet-page"></a>将母版页绑定到现有的 ASP.NET 页

正如本步骤中所述，将新的内容页添加到 ASP.NET web 应用程序非常简单，只需选中 "选择母版页" 复选框并选择母版页即可。 遗憾的是，将现有的 ASP.NET 页转换为母版页并不容易。

若要将母版页绑定到现有的 ASP.NET 页面，需要执行以下步骤：

1. 将 `MasterPageFile` 特性添加到 ASP.NET 页的 `@Page` 指令中，将其指向相应的母版页。
2. 为母版页中的每个 Contentplaceholder 添加内容控件。
3. 选择性地将 ASP.NET 页面的现有内容剪切并粘贴到相应的内容控件中。 我说 "有选择"，因为 ASP.NET 页面可能包含已由母版页表示的标记，例如 `DOCTYPE`、`<html>` 元素和 Web 窗体。

有关此过程的分步说明以及屏幕截图，请查看[Scott Guthrie](https://weblogs.asp.net/scottgu/)的[使用母版页和站点导航](http://webproject.scottgu.com/VisualBasic/MasterPages/MasterPages.aspx)教程。 "更新 `Default.aspx` 和 `DataSample.aspx` 使用母版页" 部分详细介绍了这些步骤。

由于创建新的内容页比将现有的 ASP.NET 页转换为内容页要容易得多，因此，我建议在每次创建新的 ASP.NET 网站时，将母版页添加到网站。 将所有新的 ASP.NET 页绑定到此母版页。 如果初始母版页非常简单或简洁，请不要担心;您可以在以后更新母版页。

> [!NOTE]
> 创建新的 ASP.NET 应用程序时，Visual Web Developer 会添加一个未绑定到母版页的 `Default.aspx` 页面。 如果要练习将现有的 ASP.NET 页转换为内容页，请继续操作并 `Default.aspx`。 或者，你可以删除 `Default.aspx` 然后重新添加它，但这一次选中 "选择母版页" 复选框。

## <a name="step-3-updating-the-master-pages-markup"></a>步骤3：更新母版页的标记

母版页的主要优点之一是可以使用单个母版页来定义站点上许多页面的整体布局。 因此，更新站点的外观和感觉需要更新单个文件-母版页。

为了说明此行为，我们将母版页更新为在左列顶部包含当前日期。 将名为 `DateDisplay` 的标签添加到 `leftContent` `<div>`中。

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample5.aspx)]

接下来，为母版页创建 `Page_Load` 事件处理程序并添加以下代码：

[!code-vb[Main](creating-a-site-wide-layout-using-master-pages-vb/samples/sample6.vb)]

上面的代码将标签的 `Text` 属性设置为当前日期和时间，其格式为一周中的某一天，月份名称和两位数日期（参见图11）。 进行此更改后，请重新访问其中一个内容页面。 如图11所示，生成的标记会立即更新，以包括对母版页所做的更改。

[![查看 "内容" 页时，将反映母版页的更改](creating-a-site-wide-layout-using-master-pages-vb/_static/image30.png)](creating-a-site-wide-layout-using-master-pages-vb/_static/image29.png)

**图 11**：查看 "内容" 页时，母版页的更改会反映出来（[单击查看完全大小的图像](creating-a-site-wide-layout-using-master-pages-vb/_static/image31.png)）

> [!NOTE]
> 如本示例所示，母版页可能包含服务器端 Web 控件、代码和事件处理程序。

## <a name="summary"></a>总结

通过母版页，ASP.NET 开发人员可以设计出一个易于更新的一致站点范围的布局。 创建母版页及其关联的内容页与创建标准 ASP.NET 页一样简单，因为 Visual Web Developer 提供丰富的设计时支持。

本教程中创建的母版页示例有两个 ContentPlaceHolder 控件： head 和 MainContent。 但我们仅在内容页中为 MainContent ContentPlaceHolder 控件指定了标记。 在下一教程中，我们将介绍如何在内容页中使用多个内容控件。 我们还将了解如何在母版页中定义内容控件的默认标记，以及如何在使用在母版页中定义的默认标记和从内容页提供自定义标记之间切换。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [面向设计人员的 ASP.NET：免费设计模板和有关使用 Web 标准构建 ASP.NET 网站的指南](https://msdn.microsoft.com/asp.net/aa336602.aspx)
- [ASP.NET 母版页概述](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [级联样式表（CSS）教程](http://www.w3schools.com/css/default.asp)
- [动态设置页面标题](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [ASP.NET 中的母版页](http://www.odetocode.com/articles/419.aspx)
- [母版页快速入门教程](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](nested-master-pages-cs.md)
> [下一页](multiple-contentplaceholders-and-default-content-vb.md)
