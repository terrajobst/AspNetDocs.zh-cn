---
uid: web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
title: 嵌套的母版页（C#） |Microsoft Docs
author: rick-anderson
description: 演示如何将一个母版页嵌套在另一个母版页内。
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 32b7fb6e-d74b-4048-91f8-70631b2523ee
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 67093266567a97cd22b353115616484fd9ef155e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74596475"
---
# <a name="nested-master-pages-c"></a>嵌套的母版页 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.zip)或[下载 PDF](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.pdf)

> 演示如何将一个母版页嵌套在另一个母版页内。

## <a name="introduction"></a>简介

在过去的九个教程中，我们了解了如何在母版页中实现站点范围的布局。 简而言之，母版页允许我们（页面开发人员）在母版页中定义常见标记，以及可以按内容页自定义的特定区域。 母版页中的 ContentPlaceHolder 控件表示可自定义的区域;ContentPlaceHolder 控件的自定义标记是通过内容控件在 "内容" 页中定义的。

如果你在整个站点上使用单个布局，我们目前探索到的母版页技术非常好。 但是，许多大型网站都具有跨各个部分自定义的网站布局。 例如，请考虑医院工作人员用来管理患者信息、活动和计费的卫生保健应用程序。 在此应用程序中，可能有三种类型的网页：

- 员工特定的页面，其中教职员工成员可以更新可用性、查看计划或请求休假时间。
- 患者特定的页面，其中的教职员工成员查看或编辑特定患者的信息。
- 会计查看当前声明状态和财务报告的计费特定页面。

每个页面都可能共用一个通用布局，例如，在顶部有一个菜单，一系列频繁使用的链接。 但工作人员、患者和计费特定页面可能需要自定义此通用布局。 例如，可能是所有员工特定的页面都应包括显示当前登录用户的可用性和每日计划的日历和任务列表。 可能所有特定于患者的页面都需要显示其信息正在编辑的患者的名称、地址和保险信息。

使用*嵌套的母版页*可以创建此类自定义的布局。 为实现上述方案，我们首先创建一个母版页，其中定义了站点范围的布局、菜单和页脚内容，并使用 Contentplaceholder 定义了可自定义的区域。 接下来，我们将创建三个嵌套的母版页，每个页面都有一个。 每个嵌套母版页都将定义使用母版页的内容页类型中的内容。 换句话说，特定于患者的内容页的嵌套母版页包含标记和编程逻辑，以便显示有关要编辑的患者的信息。 创建新的患者特定页面时，会将其绑定到此嵌套母版页。

本教程首先突出显示嵌套母版页的优点。 然后演示如何创建和使用嵌套母版页。

> [!NOTE]
> 由于版本2.0 的 .NET Framework，因此可能会嵌套母版页。 但是，Visual Studio 2005 未包括对嵌套母版页的设计时支持。 好消息是，Visual Studio 2008 为嵌套母版页提供丰富的设计时体验。 如果你有兴趣使用嵌套母版页，但仍在使用 Visual Studio 2005，请查看[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章，以及[在 VS 2005 设计时嵌套母版页的提示](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)。

## <a name="the-benefits-of-nested-master-pages"></a>嵌套母版页的优点

许多网站的网站设计和特定于某些类型的页面都有更多的自定义设计。 例如，在我们的演示 web 应用程序中，我们创建了一个基本的管理部分（`~/Admin` 文件夹中的页）。 目前，`~/Admin` 文件夹中的网页使用的母版页与 "管理" 部分中的页面不相同（即 `Site.master` 或 `Alternate.master`，具体取决于用户的选择）。

> [!NOTE]
> 现在，假设我们的站点只包含一个母版页，`Site.master`。 我们将使用嵌套母版页，其中包含了在本教程后面的两个（或多个）母版页，以 "使用嵌套母版页作为管理部分"。

假设我们要求你自定义管理页面的布局，以包含其他信息或站点中其他页面不会出现的链接。 实现此要求有四种方法：

1. 手动添加特定于管理的信息并链接到 `~/Admin` 文件夹中的每个内容页。
2. 更新 `Site.master` 母版页，使其包含特定于管理部分的信息和链接，然后将代码添加到母版页，以根据是否访问某个管理页面来显示或隐藏这些部分。
3. 为 "管理" 部分专门创建一个母版页，从 `Site.master`复制标记，添加特定于管理部分的信息和链接，然后更新 `~/Admin` 文件夹中的内容页以使用此新的母版页。
4. 创建一个绑定到 `Site.master` 的嵌套母版页，并使 `~/Admin` 文件夹中的内容页使用这一新的嵌套母版页。 此嵌套母版页只包含特定于 "管理" 页的附加信息和链接，并且不需要重复 `Site.master`中定义的标记。

第一个选项是最小愉快。 使用母版页的要点就是不需要将常见标记手动复制并粘贴到新的 ASP.NET 页面。 第二个选项是可接受的，但使应用程序的可维护性更低，因为它 bulks 仅偶尔显示的包含标记的母版页，并要求开发人员编辑母版页来处理此标记，并记住何时确切地说，特定标记是在隐藏时显示的。 这种方法不太 tenable，因为此母版页需要满足更多类型的网页的自定义。

第三个选项通过第二个选项删除出现的混乱和复杂性问题。 不过，第三种方法的主要缺点是，需要我们将通用布局从 `Site.master` 复制并粘贴到新的管理特定于区域的母版页。 如果以后决定更改站点范围的布局，则必须记得在两个位置进行更改。

第四个选项（即嵌套母版页）为我们最大的第二个和第三个选项。 站点范围内的布局信息保留在一个文件中-顶级母版页，而特定区域特定区域的内容将被分为不同的文件。

本教程首先介绍如何创建和使用简单的嵌套母版页。 我们创建了新的顶级母版页、两个嵌套母版页和两个内容页。 从 "使用用于管理的嵌套母版页" 部分开始，我们将介绍如何更新现有的母版页体系结构以包括嵌套母版页的使用。 具体而言，我们将创建一个嵌套的母版页，并使用它为 `~/Admin` 文件夹中的内容页包含其他自定义内容。

## <a name="step-1-creating-a-simple-top-level-master-page"></a>步骤1：创建简单的顶层母版页

基于某个现有的母版页创建嵌套的主控形状，然后更新现有内容页以使用此新的嵌套母版页，而不是顶层母版页，因为现有的内容页已经需要某些内容页顶层母版页中定义的 ContentPlaceHolder 控件。 因此，嵌套母版页还必须包含具有相同名称的相同 ContentPlaceHolder 控件。 而且，我们的特定演示应用程序有两个母版页（`Site.master` 和 `Alternate.master`），它们基于用户的首选项动态分配到内容页，这会进一步增加复杂性。 我们将在本教程的后面部分介绍如何更新现有应用程序以使用嵌套母版页，但我们首先要重点介绍简单的嵌套母版页示例。

创建名为 `NestedMasterPages` 的新文件夹，然后将新的母版页文件添加到名为 `Simple.master`的文件夹中。 （请参阅图1，了解在添加此文件夹和文件后解决方案资源管理器的屏幕截图。）将 `AlternateStyles.css` 样式表文件从解决方案资源管理器拖到设计器上。 这会将 `<link>` 元素添加到 `<head>` 元素中的样式表文件中，之后母版页的 `<head>` 元素的标记应如下所示：

[!code-aspx[Main](nested-master-pages-cs/samples/sample1.aspx)]

接下来，在 `Simple.master`的 Web 窗体中添加以下标记：

[!code-aspx[Main](nested-master-pages-cs/samples/sample2.aspx)]

此标记在页面顶部显示一个标题为 "嵌套母版页（Simple）" 的链接，在深蓝色背景上以大白色字体显示。 下面是 `MainContent` ContentPlaceHolder 的。 图1显示了在 Visual Studio 设计器中加载时的 `Simple.master` 母版页。

[![嵌套母版页会定义特定于 "管理" 部分页面的内容](nested-master-pages-cs/_static/image2.png)](nested-master-pages-cs/_static/image1.png)

**图 01**：嵌套母版页定义特定于 "管理" 部分中的页面的内容（[单击以查看完全大小的图像](nested-master-pages-cs/_static/image3.png)）

## <a name="step-2-creating-a-simple-nested-master-page"></a>步骤2：创建简单的嵌套母版页

`Simple.master` 包含两个 ContentPlaceHolder 控件：在 Web 窗体中添加的 `MainContent` ContentPlaceHolder 和 `<head>` 元素中的 `head` ContentPlaceHolder。 如果我们要创建内容页并将其绑定到 `Simple.master` 内容页将具有两个引用两个 Contentplaceholder 的内容控件。 同样，如果创建嵌套母版页并将其绑定到 `Simple.master`，则嵌套的母版页将具有两个内容控件。

让我们将新的嵌套母版页添加到名为 `SimpleNested.master`的 `NestedMasterPages` 文件夹。 右键单击 "`NestedMasterPages`" 文件夹，然后选择 "添加新项"。 此时将打开图2所示的 "添加新项" 对话框。 选择 "母版页" 模板类型，然后键入新的母版页的名称。 若要指示新的母版页应为嵌套母版页，请选中 "选择母版页" 复选框。

接下来，单击 "添加" 按钮。 这会显示将内容页绑定到母版页时看到的相同的 "选择母版页" 对话框（请参阅图3）。 选择 `NestedMasterPages` 文件夹中的 `Simple.master` 母版页，然后单击 "确定"。

> [!NOTE]
> 如果你使用 Web 应用程序项目模型而不是网站项目模型创建了你的 ASP.NET 网站，则在图2所示的 "添加新项" 对话框中将看不到 "选择母版页" 复选框。 若要在使用 Web 应用程序项目模型时创建嵌套母版页，必须选择嵌套母版页模板（而不是母版页模板）。 选择嵌套的母版页模板并单击 "添加" 后，将显示图3中所示的 "选择母版页" 对话框。

[![选中 "&quot;选择母版页&quot;" 复选框添加嵌套母版页](nested-master-pages-cs/_static/image5.png)](nested-master-pages-cs/_static/image4.png)

**图 02**：选中 "选择母版页" 复选框以添加嵌套母版页（[单击以查看完全大小的图像](nested-master-pages-cs/_static/image6.png)）

[![将嵌套母版页绑定到简单的母版页母版页](nested-master-pages-cs/_static/image8.png)](nested-master-pages-cs/_static/image7.png)

**图 03**：将嵌套母版页绑定到 `Simple.master` 母版页（[单击以查看完全大小的图像](nested-master-pages-cs/_static/image9.png)）

嵌套母版页的声明性标记（如下所示）包含两个内容控件，它们引用顶层母版页的两个 ContentPlaceHolder 控件。

[!code-aspx[Main](nested-master-pages-cs/samples/sample3.aspx)]

除 `<%@ Master %>` 指令外，嵌套母版页的初始声明性标记与将内容页绑定到相同顶级母版页时最初生成的标记相同。 与内容页的 `<%@ Page %>` 指令一样，此处的 `<%@ Master %>` 指令包含一个指定嵌套母版页的父母版页的 `MasterPageFile` 特性。 嵌套母版页和绑定到相同顶级母版页的内容页之间的主要区别在于，嵌套母版页可以包含 ContentPlaceHolder 控件。 嵌套母版页的 ContentPlaceHolder 控件定义内容页可自定义标记的区域。

更新此嵌套母版页，使其显示文本 "Hello，from SimpleNested！" 在与 `MainContent` ContentPlaceHolder 控件相对应的内容控件中。

[!code-aspx[Main](nested-master-pages-cs/samples/sample4.aspx)]

完成此添加后，保存嵌套的母版页，然后将新的内容页添加到名为 `Default.aspx``NestedMasterPages` 文件夹中，并将其绑定到 `SimpleNested.master` 母版页。 添加此页后，你可能会感到惊讶，因为它不包含任何内容控件（见图4）！ 内容页只能访问其*父*母版页的 contentplaceholder。 `SimpleNested.master` 不包含任何 ContentPlaceHolder 控件;因此，绑定到此母版页的任何内容页都不能包含任何内容控件。

[![新的内容页不包含任何内容控件](nested-master-pages-cs/_static/image11.png)](nested-master-pages-cs/_static/image10.png)

**图 04**：新的内容页不包含任何内容控件（[单击以查看完全大小的图像](nested-master-pages-cs/_static/image12.png)）

我们需要做的就是将嵌套的母版页（`SimpleNested.master`）更新为包含 ContentPlaceHolder 控件。 通常，您将希望嵌套母版页包含其父母版页所定义的每个 ContentPlaceHolder 的 ContentPlaceHolder，从而允许其子母版页或内容页使用顶层母版页的任何 ContentPlaceHolder控件.

更新 `SimpleNested.master` 母版页，使其在其两个内容控件中包含 ContentPlaceHolder。 为 ContentPlaceHolder 控件指定与其内容控件引用的 ContentPlaceHolder 控件相同的名称。 也就是说，将名为 `MainContent` 的 ContentPlaceHolder 控件添加到 `SimpleNested.master` 中的内容控件，该控件引用 `Simple.master`中的 `MainContent` ContentPlaceHolder。 在引用 `head` ContentPlaceHolder 的内容控件中执行相同的操作。

> [!NOTE]
> 尽管建议在嵌套母版页中命名 ContentPlaceHolder 控件的方式与顶层母版页中的 Contentplaceholder 相同，但不需要此命名对称。 可以在嵌套母版页中为 ContentPlaceHolder 控件指定任意名称。 但是，我发现，如果顶层母版页和嵌套母版页使用相同的名称，则可以更方便地记住哪些 Contentplaceholder 与页面区域相对应。

进行这些添加后，`SimpleNested.master` 母版页的声明性标记应如下所示：

[!code-aspx[Main](nested-master-pages-cs/samples/sample5.aspx)]

删除刚刚创建的 `Default.aspx` 内容页，然后重新添加该页面，并将其绑定到 `SimpleNested.master` 的母版页。 此时，Visual Studio 会将两个内容控件添加到 `Default.aspx`，同时引用 `SimpleNested.master` 中定义的 Contentplaceholder （参见图6）。 添加文本 "Hello，from default.aspx！" 在引用 `MainContent`的内容控件中。

图5显示了此处涉及的三个实体-`Simple.master`、`SimpleNested.master`和 `Default.aspx`，以及它们彼此之间的关系。 如图所示，嵌套母版页实现其父对象的 ContentPlaceHolder 的内容控件。 如果需要对内容页访问这些区域，则嵌套母版页必须将其自己的 Contentplaceholder 添加到内容控件。

[![顶级和嵌套母版页决定内容页的布局](nested-master-pages-cs/_static/image14.png)](nested-master-pages-cs/_static/image13.png)

**图 05**：顶级和嵌套母版页决定内容页的布局（[单击查看完全大小的图像](nested-master-pages-cs/_static/image15.png)）

此行为说明内容页或母版页如何只 cognizant 其父母版页。 Visual Studio 设计器也指出了此行为。 图6显示了 `Default.aspx`的设计器。 虽然设计器清楚地显示了哪些区域可从 "内容" 页进行编辑以及哪些部分不能，但它并不区分嵌套母版页中的哪些不可编辑区域以及顶层母版页中的区域。

[![内容页现在包含嵌套母版页的 Contentplaceholder 的内容控件。](nested-master-pages-cs/_static/image17.png)](nested-master-pages-cs/_static/image16.png)

**图 06**： "内容" 页现在包含用于嵌套母版页 Contentplaceholder 的内容控件（[单击以查看完全大小的图像](nested-master-pages-cs/_static/image18.png)）

## <a name="step-3-adding-a-second-simple-nested-master-page"></a>步骤3：添加第二个简单嵌套母版页

如果有多个嵌套母版页，则嵌套母版页的优点更明显。 为了说明此权益，请在 `NestedMasterPages` 文件夹中创建另一个嵌套的母版页;将这一新的嵌套母版页命名 `SimpleNestedAlternate.master`，并将其绑定到 `Simple.master` 母版页。 将 ContentPlaceHolder 控件添加到嵌套母版页的两个内容控件中，就像我们在步骤2中所做的一样。 同时添加文本 "Hello，from SimpleNestedAlternate！" 在与顶层母版页的 `MainContent` ContentPlaceHolder 的内容控件中。 进行这些更改后，新的嵌套母版页的声明性标记应如下所示：

[!code-aspx[Main](nested-master-pages-cs/samples/sample6.aspx)]

在 `NestedMasterPages` 文件夹中创建名为 `Alternate.aspx` 的内容页，并将其绑定到 `SimpleNestedAlternate.master` 嵌套母版页。 添加文本 "Hello，from 替补！" 在与 `MainContent`相对应的内容控件中。 图7显示了通过 Visual Studio 设计器查看 `Alternate.aspx`。

[![备用 .aspx 绑定到 SimpleNestedAlternate 母版页](nested-master-pages-cs/_static/image20.png)](nested-master-pages-cs/_static/image19.png)

**图 07**： `Alternate.aspx` 绑定到 `SimpleNestedAlternate.master` 母版页（[单击查看完全大小的图像](nested-master-pages-cs/_static/image21.png)）

将图7中的设计器与图6中的设计器进行比较。 这两个内容页共享在顶层母版页（`Simple.master`）中定义的同一布局，即 "嵌套母版页教程（简单）" 标题。 但它们的父母版页中都定义了不同的内容-文本 "Hello，from SimpleNested！" 图6和 "Hello，from SimpleNestedAlternate！" 图7所示。 当然，这种差异很简单，但你可以扩展此示例，使其包含更有意义的差异。 例如，"`SimpleNested.master`" 页可能包含一个菜单，其中包含特定于其内容页的选项，而 `SimpleNestedAlternate.master` 可能包含与绑定到它的内容页相关的信息。

现在，假设我们需要对 "网站布局" 进行更改。 例如，假设我们想要将常用链接列表添加到所有内容页。 为实现此目的，我们更新了顶层母版页，`Simple.master`。 任何更改都会立即反映在其嵌套的母版页中，并通过扩展的内容页进行。

若要演示如何轻松地更改 "网站布局"，请打开 `Simple.master` 母版页，并在 `topContent` 和 `mainContent` `<div>` 元素之间添加以下标记：

[!code-aspx[Main](nested-master-pages-cs/samples/sample7.aspx)]

这会将两个链接添加到绑定到 `Simple.master`、`SimpleNested.master`或 `SimpleNestedAlternate.master`的每个页面的顶部;这些更改将立即应用于所有嵌套母版页及其内容页。 图8显示了通过浏览器查看 `Alternate.aspx`。 请注意页面顶部的链接添加（与图7相比）。

[![更改为顶层母版页会立即反映在其嵌套母版页及其内容页中。](nested-master-pages-cs/_static/image23.png)](nested-master-pages-cs/_static/image22.png)

**图 08**：更改为顶层母版页会立即反映在其嵌套母版页及其内容页面中（[单击以查看完全大小的图像](nested-master-pages-cs/_static/image24.png)）

## <a name="using-a-nested-master-page-for-the-administration-section"></a>使用 "管理" 部分的嵌套母版页

此时，我们已经了解了嵌套母版页的优点，并了解了如何在 ASP.NET 应用程序中创建和使用它们。 不过，步骤1、2和3中的示例涉及到创建新的顶级母版页、新建嵌套母版页和新内容页。 如何使用现有顶级母版页和内容页向网站添加新的嵌套母版页呢？

将嵌套母版页集成到现有网站，并将其与现有内容页相关联需要比从头开始更多的工作。 步骤4、5、6和7介绍了这些难题，因为我们增加了演示应用程序以包括一个名为 `AdminNested.master` 的新嵌套母版页，其中包含管理员的说明，由 `~/Admin` 文件夹中的 ASP.NET 页使用。

将嵌套母版页集成到演示应用程序中带来了以下障碍：

- `~/Admin` 文件夹中的现有内容页具有其母版页的特定期望。 对于初学者，它们期望存在某些 ContentPlaceHolder 控件。 此外，`~/Admin/AddProduct.aspx` 和 `~/Admin/Products.aspx` 页将调用母版页的公共 `RefreshRecentProductsGrid` 方法，设置其 `GridMessageText` 属性，或具有其 `PricesDoubled` 事件的事件处理程序。 因此，嵌套母版页必须提供相同的 Contentplaceholder 和公共成员。
- 在前面的教程中，我们增强了 `BasePage` 类，以便基于会话变量动态设置 `Page` 对象的 `MasterPageFile` 属性。 使用嵌套母版页时，如何支持动态母版页？

当我们构建嵌套母版页，并从现有内容页中使用它时，这两个挑战将会出现。 我们会在出现这些问题时进行调查和克服。

## <a name="step-4-creating-the-nested-master-page"></a>步骤4：创建嵌套母版页

第一项任务是创建要由 "管理" 部分中的页面使用的嵌套母版页。 正如我们在步骤2中看到的，添加新的嵌套母版页时，需要指定嵌套母版页的父母版页。 但有两个顶级母版页： `Site.master` 和 `Alternate.master`。 回忆一下，我们在前面的教程中创建了 `Alternate.master`，并在 `BasePage` 类中编写了代码，该代码在运行时将页面对象的 `MasterPageFile` 属性设置为 `Site.master` 或 `Alternate.master`，具体取决于 `MyMasterPage` 会话变量的值。

如何配置嵌套母版页，使其使用适当的顶层母版页？ 我们有两个选项：

- 创建两个嵌套母版页，`AdminNestedSite.master` 和 `AdminNestedAlternate.master`，并分别将它们绑定到顶层母版页 `Site.master` 和 `Alternate.master`。 在 `BasePage`中，我们将 `Page` 对象的 `MasterPageFile` 设置为相应的嵌套母版页。
- 创建单个嵌套母版页，并使内容页使用该特定母版页。 然后，在运行时，需要在运行时将嵌套母版页的 `MasterPageFile` 属性设置为适当的顶级母版页。 （正如你现在可能已发现，母版页也有一个 `MasterPageFile` 属性。）

我们将使用第二个选项。 在名为 `AdminNested.master``~/Admin` 文件夹中创建单个嵌套母版页文件。 由于 `Site.master` 和 `Alternate.master` 都具有相同的一组 ContentPlaceHolder 控件，因此，尽管我建议您将其绑定到 `Site.master` 以实现一致性。

[![将嵌套的母版页添加到 ~/Admin 文件夹中。](nested-master-pages-cs/_static/image26.png)](nested-master-pages-cs/_static/image25.png)

**图 09**：将嵌套母版页添加到 `~/Admin` 文件夹。 （[单击以查看完全大小的映像](nested-master-pages-cs/_static/image27.png)）

由于嵌套母版页绑定到具有四个 ContentPlaceHolder 控件的母版页，因此 Visual Studio 会将四个内容控件添加到新的嵌套母版页文件的初始标记中。 与第2步和第3步一样，在每个内容控件中添加 ContentPlaceHolder 控件，使其与顶层母版页的 ContentPlaceHolder 控件的名称相同。 还将以下标记添加到与 `MainContent` ContentPlaceHolder 相对应的内容控件：

[!code-html[Main](nested-master-pages-cs/samples/sample8.html)]

接下来，在 `Styles.css` 和 `AlternateStyles.css` CSS 文件中定义 `instructions` CSS 类。 以下 CSS 规则会导致使用带有浅黄色背景色和黑色实线边框的 `instructions` 类样式的 HTML 元素显示：

[!code-css[Main](nested-master-pages-cs/samples/sample9.css)]

由于已将此标记添加到嵌套母版页，因此它将仅显示在使用此嵌套母版页的页面中（即，"管理" 部分中的页面）。

将这些添加到嵌套母版页后，其声明性标记应如下所示：

[!code-aspx[Main](nested-master-pages-cs/samples/sample10.aspx)]

请注意，每个内容控件都有一个 ContentPlaceHolder 控件，并且为 ContentPlaceHolder 控件的 `ID` 属性分配与顶层母版页中对应 ContentPlaceHolder 控件相同的值。 此外，"管理" 部分特定的标记将显示在 `MainContent` ContentPlaceHolder 中。

图10显示了通过 Visual Studio 的设计器查看 `AdminNested.master` 嵌套母版页。 可以在 `MainContent` 内容控件顶部的黄色框中查看说明。

[![嵌套的母版页扩展了顶层母版页，以包含管理员的说明。](nested-master-pages-cs/_static/image29.png)](nested-master-pages-cs/_static/image28.png)

**图 10**：嵌套的母版页扩展了顶层母版页，以包含管理员的说明。 （[单击以查看完全大小的映像](nested-master-pages-cs/_static/image30.png)）

## <a name="step-5-updating-the-existing-content-pages-to-use-the-new-nested-master-page"></a>步骤5：更新现有内容页以使用新的嵌套母版页

每次将新的内容页添加到 "管理" 部分时，需要将其绑定到刚刚创建的 `AdminNested.master` 母版页。 但现有内容页呢？ 当前，站点中的所有内容页派生自 `BasePage` 类，该类在运行时以编程方式设置内容页的母版页。 这不是我们想要用于 "管理" 部分中的内容页的行为。 相反，我们希望这些内容页始终使用 `AdminNested.master` 页。 嵌套母版页负责在运行时选择正确的顶级内容页。

若要实现此所需行为，最佳方法是创建一个新的名为 `AdminBasePage` 的自定义基类类，以扩展 `BasePage` 类。 然后 `AdminBasePage` 可以重写 `SetMasterPageFile` 并将 `Page` 对象的 `MasterPageFile` 设置为硬编码值 "~/Admin/AdminNested.master"。 通过这种方式，派生自 `AdminBasePage` 的任何页面都将使用 `AdminNested.master`，而从 `BasePage` 派生的任何页面都将基于 `MyMasterPage` 会话变量的值将其 `MasterPageFile` 属性动态设置为 "~/Site.master" 或 "~/Alternate.master"。

首先将新的类文件添加到名为 `AdminBasePage.cs``App_Code` 文件夹。 让 `AdminBasePage` 扩展 `BasePage`，然后重写 `SetMasterPageFile` 方法。 在该方法中，将 `MasterPageFile` 值 "~/Admin/AdminNested.master"。 进行这些更改后，类文件应如下所示：

[!code-csharp[Main](nested-master-pages-cs/samples/sample11.cs)]

现在，我们需要在 "管理" 部分中的现有内容页派生自 `AdminBasePage` 而不是 `BasePage`。 转到 `~/Admin` 文件夹中每个内容页面的代码隐藏类文件，然后进行此更改。 例如，在 `~/Admin/Default.aspx` 你需要更改的代码隐藏类声明：

[!code-csharp[Main](nested-master-pages-cs/samples/sample12.cs)]

结束时间：

[!code-csharp[Main](nested-master-pages-cs/samples/sample13.cs)]

图11描绘了顶层母版页（`Site.master` 或 `Alternate.master`）、嵌套母版页（`AdminNested.master`）和管理部分内容页之间的关系。

[![嵌套母版页会定义特定于 "管理" 部分页面的内容](nested-master-pages-cs/_static/image32.png)](nested-master-pages-cs/_static/image31.png)

**图 11**：嵌套母版页定义特定于 "管理" 部分中的页面的内容（[单击以查看完全大小的图像](nested-master-pages-cs/_static/image33.png)）

## <a name="step-6-mirroring-the-master-pages-public-methods-and-properties"></a>步骤6：镜像母版页的公共方法和属性

回忆一下，`~/Admin/AddProduct.aspx` 和 `~/Admin/Products.aspx` 页面以编程方式与母版页交互： `~/Admin/AddProduct.aspx` 调用母版页的公共 `RefreshRecentProductsGrid` 方法并设置其 `GridMessageText` 属性;`~/Admin/Products.aspx` 具有 `PricesDoubled` 事件的事件处理程序。 在前面的教程中，我们创建了一个定义这些公共成员的抽象 `BaseMasterPage` 类。

"`~/Admin/AddProduct.aspx`" 和 "`~/Admin/Products.aspx`" 页假定其母版页派生自 `BaseMasterPage` 类。 但 `AdminNested.master` 页当前扩展了 `System.Web.UI.MasterPage` 类。 因此，当访问 `~/Admin/Products.aspx` 引发 `InvalidCastException` 时，消息： "无法将类型为\_" adminnested\_master "的对象强制转换为类型" BaseMasterPage "。

若要解决此问题，我们需要让 `AdminNested.master` 代码隐藏类 `BaseMasterPage`扩展。 从以下项更新嵌套母版页的代码隐藏类声明：

[!code-csharp[Main](nested-master-pages-cs/samples/sample14.cs)]

结束时间：

[!code-csharp[Main](nested-master-pages-cs/samples/sample15.cs)]

尚未完成。 由于 `BaseMasterPage` 类是抽象类，因此需要重写 `abstract` 成员，`RefreshRecentProductsGrid` 和 `GridMessageText`。 顶级母版页使用这些成员更新其用户界面。 （实际上，只有 `Site.master` 的母版页使用这些方法，尽管这两个顶级母版页都实现了这些方法，因为这两种方法都扩展 `BaseMasterPage`。）

尽管我们需要在 `AdminNested.master`中实现这些成员，但所有这些实现都只需调用嵌套母版页所使用的顶级母版页中的同一成员。 例如，在 "管理" 部分中的 "内容" 页调用嵌套母版页的 `RefreshRecentProductsGrid` 方法时，所有嵌套母版页都需要做的就是调用 `Site.master` 或 `Alternate.master`的 `RefreshRecentProductsGrid` 方法。

若要实现此目的，请首先将以下 `@MasterType` 指令添加到 `AdminNested.master`顶部：

[!code-aspx[Main](nested-master-pages-cs/samples/sample16.aspx)]

请记住，`@MasterType` 指令将强类型属性添加到名为 `Master`的代码隐藏类。 然后，重写 `RefreshRecentProductsGrid` 和 `GridMessageText` 成员，只需将调用委托给 `Master`的相应方法即可：

[!code-csharp[Main](nested-master-pages-cs/samples/sample17.cs)]

使用此代码后，应能够访问并使用 "管理" 部分中的内容页。 图12显示了通过浏览器查看 `~/Admin/Products.aspx` 页面。 如您所见，页面包含在嵌套母版页中定义的 "管理说明" 框。

[!["管理" 部分中的内容页面包括每个页面顶部的说明](nested-master-pages-cs/_static/image35.png)](nested-master-pages-cs/_static/image34.png)

**图 12**： "管理" 部分中的内容页包含每个页面顶部的说明（[单击以查看完全大小的图像](nested-master-pages-cs/_static/image36.png)）

## <a name="step-7-using-the-appropriate-top-level-master-page-at-runtime"></a>步骤7：在运行时使用合适的顶级母版页

尽管 "管理" 部分中的所有内容页都可以完全正常运行，但它们都使用相同的顶层母版页，并忽略用户在 `ChooseMasterPage.aspx`选择的母版页。 此行为的原因是嵌套母版页的 `MasterPageFile` 属性静态设置为在其 `<%@ Master %>` 指令中 `Site.master`。

若要使用由最终用户选择的顶层母版页，需要将 `AdminNested.master`的 `MasterPageFile` 属性设置为 `MyMasterPage` Session 变量中的值。 由于我们在 `BasePage`中设置内容页的 `MasterPageFile` 属性，因此，你可能会认为在 `BaseMasterPage` 或 `AdminNested.master`的代码隐藏类中设置嵌套母版页的 `MasterPageFile` 属性。 但这不起作用，因为我们需要在 PreInit 阶段结束时设置 "`MasterPageFile`" 属性。 可以通过编程方式从母版页进入页面生命周期的最早时间是 Init 阶段（在 PreInit 阶段后发生）。

因此，需要从内容页设置嵌套母版页的 `MasterPageFile` 属性。 使用 `AdminNested.master` 母版页的唯一内容页派生自 `AdminBasePage`。 因此，可以将此逻辑放在此处。 在步骤5中，我们 u.i 了 `SetMasterPageFile` 方法，将 `Page` 对象的 `MasterPageFile` 属性设置为 "~/Admin/AdminNested.master"。 更新 `SetMasterPageFile`，同时将母版页的 `MasterPageFile` 属性设置为会话中存储的结果：

[!code-csharp[Main](nested-master-pages-cs/samples/sample18.cs)]

在前面的教程中，我们添加到 `BasePage` 类的 `GetMasterPageFileFromSession` 方法将根据会话变量值返回相应的母版页文件路径。

进行此更改后，用户的母版页选择会转到 "管理" 部分。 图13显示了与图12相同的页，但在用户将其母版页选择更改为 `Alternate.master`后。

[!["嵌套的管理" 页使用用户选择的顶层母版页](nested-master-pages-cs/_static/image38.png)](nested-master-pages-cs/_static/image37.png)

**图 13**：嵌套管理页使用用户选择的顶层母版页（[单击以查看完全大小的图像](nested-master-pages-cs/_static/image39.png)）

## <a name="summary"></a>总结

与内容页绑定到母版页的方式非常类似，可以通过将子母版页绑定到父母版页来创建嵌套母版页。 子母版页可以为其每个父级的 Contentplaceholder 定义内容控件;然后，它可以将其自己的 ContentPlaceHolder 控件（以及其他标记）添加到这些内容控件。 嵌套的母版页在大 web 应用程序中非常有用，在这种情况下，所有页面都具有大致的外观，但站点的某些部分需要独有的自定义。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [嵌套 ASP.NET 母版页](https://msdn.microsoft.com/library/x2b3ktt7.aspx)
- [嵌套母版页和 VS 2005 设计时的提示](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)
- [VS 2008 嵌套母版页支持](https://weblogs.asp.net/scottgu/archive/2007/07/09/vs-2008-nested-master-page-support.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](specifying-the-master-page-programmatically-cs.md)
> [下一页](creating-a-site-wide-layout-using-master-pages-vb.md)
