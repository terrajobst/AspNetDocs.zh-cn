---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-vb
title: 以编程方式指定母版页（VB） |Microsoft Docs
author: rick-anderson
description: 查看如何通过 PreInit 事件处理程序以编程方式设置内容页的母版页。
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 0edcd653-f24a-41aa-aef4-75f868fe5ac2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b039b22bef38ae6ebf80be070820dc1638f87f4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74618702"
---
# <a name="specifying-the-master-page-programmatically-vb"></a>以编程方式指定母版页 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_VB.zip)或[下载 PDF](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_VB.pdf)

> 查看如何通过 PreInit 事件处理程序以编程方式设置内容页的母版页。

## <a name="introduction"></a>简介

由于在[*使用母版页创建站点范围布局*](creating-a-site-wide-layout-using-master-pages-vb.md)的便捷性示例中，所有内容页都通过 `@Page` 指令中的 `MasterPageFile` 属性以声明方式引用了其母版页。 例如，以下 `@Page` 指令将内容页链接到母版页 `Site.master`：

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample1.aspx)]

`System.Web.UI` 命名空间中的[`Page` 类](https://msdn.microsoft.com/library/system.web.ui.page.aspx)包括一个[`MasterPageFile` 属性](https://msdn.microsoft.com/library/system.web.ui.page.masterpagefile.aspx)，该属性返回内容页的母版页的路径;此属性由 `@Page` 指令设置。 此属性还可用于以编程方式指定内容页的母版页。 如果要根据外部因素（如访问页面的用户）动态分配母版页，此方法非常有用。

在本教程中，我们将向网站添加另一个母版页，并动态确定要在运行时使用的母版页。

## <a name="step-1-a-look-at-the-page-lifecycle"></a>步骤1：查看页面生命周期

每当为内容页的 ASP.NET 页面的 web 服务器发出请求时，ASP.NET 引擎都必须将页面的内容控件保险丝到母版页的相应 ContentPlaceHolder 控件中。 这种合成创建单个控件层次结构，然后可以通过典型的页面生命周期进行处理。

图1演示了这种合成。 图1中的步骤1显示初始内容和母版页控件层次结构。 在 PreInit 阶段的结尾处，将页面中的内容控件添加到母版页中的相应 Contentplaceholder （步骤2）。 在这种合成后，母版页充当已保险丝控件层次结构的根。 然后，将此融合的控件层次结构添加到页面以生成最终控制层次结构（步骤3）。 最终结果是页面的控件层次结构包括已保险丝的控件层次结构。

[![母版页和内容页的控件层次结构在 PreInit 阶段一起融合在一起](specifying-the-master-page-programmatically-vb/_static/image2.png)](specifying-the-master-page-programmatically-vb/_static/image1.png)

**图 01**：母版页和内容页的控件层次结构在 PreInit 阶段一起融合在一起（[单击以查看完全大小的图像](specifying-the-master-page-programmatically-vb/_static/image3.png)）

## <a name="step-2-setting-themasterpagefileproperty-from-code"></a>步骤2：从代码设置`MasterPageFile`属性

此合成中 partakes 的内容取决于 `Page` 对象的 `MasterPageFile` 属性的值。 在 `@Page` 指令中设置 `MasterPageFile` 属性可以在初始化阶段（这是页面生命周期的第一阶段）中分配 `Page`的 `MasterPageFile` 属性的最终效果。 还可以通过编程方式设置此属性。 但是，在图1中的合成之前，必须设置此属性。

在 PreInit 阶段开始时，`Page` 对象将引发其[`PreInit` 事件](https://msdn.microsoft.com/library/system.web.ui.page.preinit.aspx)并调用其[`OnPreInit` 方法](https://msdn.microsoft.com/library/system.web.ui.page.onpreinit.aspx)。 若要以编程方式设置母版页，可以为 `PreInit` 事件创建事件处理程序，也可以重写 `OnPreInit` 方法。 让我们看看这两种方法。

首先打开 `Default.aspx.vb`，它是站点主页的代码隐藏类文件。 键入以下代码，为页面的 `PreInit` 事件添加事件处理程序：

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample2.vb)]

可以从此处设置 "`MasterPageFile`" 属性。 更新代码，以便它将 "~/Site.master" 值分配给 `MasterPageFile` 属性。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample3.vb)]

如果设置了断点并开始调试，你将看到，无论何时访问 `Default.aspx` 页面，或每当此页面回发时，都将执行 `Page_PreInit` 事件处理程序，并将 `MasterPageFile` 属性分配给 "~/Site.master"。

或者，您可以重写 `Page` 类的 `OnPreInit` 方法，并在其中设置 `MasterPageFile` 属性。 在此示例中，我们不会在特定页面中设置母版页，而是从 `BasePage`。 回忆一下，我们在[*母版页教程中指定标题、Meta 标记和其他 HTML 标头*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)后，创建了一个自定义的基本页类（`BasePage`）。 目前 `BasePage` 重写 `Page` 类的 `OnLoadComplete` 方法，在该方法中，它基于站点地图数据设置页面的 `Title` 属性。 让我们更新 `BasePage`，`OnPreInit` 以通过编程方式指定母版页。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample4.vb)]

由于所有内容页均派生自 `BasePage`，因此所有内容页现在都以编程方式分配了其母版页。 此时，`Default.aspx.vb` 中的 `PreInit` 事件处理程序是多余的;随意将其删除。

### <a name="what-about-thepagedirective"></a>`@Page`指令呢？

这可能有点令人困惑：内容页的 `MasterPageFile` 属性现在是在两个位置指定的：在 `BasePage` 类的 `OnPreInit` 方法中以编程方式，以及通过每个内容页的 `@Page` 指令中的 `MasterPageFile` 特性。

页面生命周期的第一阶段是初始化阶段。 在此阶段中，`Page` 对象的 `MasterPageFile` 属性分配给 `@Page` 指令中 `MasterPageFile` 属性的值（如果已提供）。 PreInit 阶段遵循初始化阶段，这里是以编程方式设置 `Page` 对象的 `MasterPageFile` 属性，从而覆盖从 `@Page` 指令分配的值。 由于我们要以编程方式设置 `Page` 对象的 `MasterPageFile` 属性，因此可以从 `@Page` 指令中删除 `MasterPageFile` 属性，而不会影响最终用户的体验。 若要说服这一点，请继续从 `Default.aspx` 的 `@Page` 指令中删除 `MasterPageFile` 属性，然后通过浏览器访问该页面。 正如您所期望的那样，输出与删除属性之前相同。

是通过 `@Page` 指令还是以编程方式设置 `MasterPageFile` 属性无关紧要最终用户的体验。 但是，Visual Studio 会在设计时使用 `@Page` 指令中的 `MasterPageFile` 属性，以在设计器中生成 WYSIWYG 视图。 如果你返回到 Visual Studio 中的 `Default.aspx`，并导航到该设计器，则会看到消息 "母版页错误：页面上有需要母版页引用的控件，但未指定任何内容" （参见图2）。

简而言之，需要在 `@Page` 指令中保留 `MasterPageFile` 特性，以便在 Visual Studio 中使用丰富的设计时体验。

[![Visual Studio 使用 @Page 指令的 MasterPageFile 特性来呈现设计视图](specifying-the-master-page-programmatically-vb/_static/image5.png)](specifying-the-master-page-programmatically-vb/_static/image4.png)

**图 02**： Visual Studio 使用 `@Page` 指令的 `MasterPageFile` 属性呈现设计视图（[单击查看完全大小的图像](specifying-the-master-page-programmatically-vb/_static/image6.png)）

## <a name="step-3-creating-an-alternative-master-page"></a>步骤3：创建备用母版页

由于可以在运行时以编程方式设置内容页的母版页，因此可以根据某些外部条件动态加载特定的母版页。 此功能在站点布局需要根据用户的不同情况下非常有用。 例如，博客引擎 web 应用程序可能允许其用户为其博客选择布局，其中每个布局与不同的母版页关联。 在运行时，当访问者查看用户的博客时，web 应用程序需要确定博客的布局并动态地将相应的母版页与内容页相关联。

让我们看看如何根据某些外部条件在运行时动态加载母版页。 我们的网站当前只包含一个母版页（`Site.master`）。 我们需要另一个母版页来说明如何在运行时选择母版页。 此步骤重点介绍如何创建和配置新的母版页。 步骤4介绍如何确定要在运行时使用的母版页。

在名为 `Alternate.master`的根文件夹中创建新的母版页。 同时向网站添加一个名为 `AlternateStyles.css`的新样式表。

[![向网站添加另一个母版页和 CSS 文件](specifying-the-master-page-programmatically-vb/_static/image8.png)](specifying-the-master-page-programmatically-vb/_static/image7.png)

**图 03**：向网站添加另一个母版页和 CSS 文件（[单击以查看完全大小的图像](specifying-the-master-page-programmatically-vb/_static/image9.png)）

我已经设计了 `Alternate.master` 母版页，使标题显示在页面顶部、在深蓝色背景中居中显示。 我已经分配了左栏并将该内容移到 `MainContent` ContentPlaceHolder 控件下，该控件现在跨越整个页面的宽度。 此外，我 nixed 未排序的课程列表，并将其替换为上面 `MainContent`的水平列表。 我还更新了母版页使用的字体和颜色（通过扩展、其内容页）。 图4显示了使用 `Alternate.master` 母版页时的 `Default.aspx`。

> [!NOTE]
> ASP.NET 包括定义*主题*的功能。 主题是可在运行时应用于页面的图像、CSS 文件和样式相关的 Web 控件属性设置的集合。 如果你的网站布局不同于显示的图像及其 CSS 规则，则可以使用主题。 如果布局不同，如使用不同的 Web 控件或具有完全不同的布局，则需要使用单独的母版页。 有关主题的详细信息，请参阅本教程末尾的其他阅读部分。

[![我们的内容页现在可以使用全新的外观](specifying-the-master-page-programmatically-vb/_static/image11.png)](specifying-the-master-page-programmatically-vb/_static/image10.png)

**图 04**：现在，我们的内容页可以使用全新的外观（[单击查看完全大小的图像](specifying-the-master-page-programmatically-vb/_static/image12.png)）

当 "大纲" 和 "内容" 页的标记融合后，`MasterPage` 类将进行检查以确保内容页中的每个内容控件都引用母版页中的 ContentPlaceHolder。 如果找到引用不存在的 ContentPlaceHolder 的内容控件，则会引发异常。 换句话说，分配到内容页的母版页对于内容页中的每个内容控件都有一个 ContentPlaceHolder。

`Site.master` 母版页包含四个 ContentPlaceHolder 控件：

- `head`
- `MainContent`
- `QuickLoginUI`
- `LeftColumnContent`

网站中的某些内容页面只包含一个或两个内容控件;其他功能包括每个可用 Contentplaceholder 的内容控件。 如果新的母版页（`Alternate.master`）可能被分配给那些内容页，这些内容页在 `Site.master` 中具有所有 Contentplaceholder 的内容控件，则 `Alternate.master` 还必须包含与 `Site.master`相同的 ContentPlaceHolder 控件。

若要使 `Alternate.master` 母版页与地雷类似（参见图4），请首先在 `AlternateStyles.css` 样式表中定义母版页的样式。 将以下规则添加到 `AlternateStyles.css`：

[!code-css[Main](specifying-the-master-page-programmatically-vb/samples/sample5.css)]

接下来，将以下声明性标记添加到 `Alternate.master`。 如您所见，`Alternate.master` 包含四个具有与 `Site.master`中的 ContentPlaceHolder 控件相同的 `ID` 值的 ContentPlaceHolder 控件。 此外，它还包括一个 ScriptManager 控件，该控件对于使用 ASP.NET AJAX framework 的网站中的页面是必需的。

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample6.aspx)]

### <a name="testing-the-new-master-page"></a>测试新的母版页

若要测试此新母版页，请更新 `BasePage` 类的 `OnPreInit` 方法，以便将值分配给 `MasterPageFile` 属性 `"~/Alternate.maser"` 然后访问该网站。 每个页面都应正常运行，但不包括两个错误： `~/Admin/AddProduct.aspx` 和 `~/Admin/Products.aspx`。 将产品添加到 `~/Admin/AddProduct.aspx` 中的 DetailsView 将导致尝试设置母版页的 `GridMessageText` 属性的代码行 `NullReferenceException`。 当访问时 `~/Admin/Products.aspx` 在页面加载时引发 `InvalidCastException`，并出现以下消息： "无法将类型为" 的对象强制转换为类型 '\_.ASP\_master '。 "

之所以发生这些错误是因为 `Site.master` 代码隐藏类包括 `Alternate.master`中未定义的公共事件、属性和方法。 这两个页面的标记部分具有一个引用 `Site.master` 母版页的 `@MasterType` 指令。

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample7.aspx)]

此外，中的 DetailsView `ItemInserted` 事件处理程序 `~/Admin/AddProduct.aspx` 包括将松散类型化的 `Page.Master` 属性强制转换为类型 `Site`的对象的代码。 `@MasterType` 指令（以这种方式使用）和 `ItemInserted` 事件处理程序中的强制转换将 `~/Admin/AddProduct.aspx` 和 `~/Admin/Products.aspx` 页面紧密耦合到 `Site.master` 母版页。

若要中断此紧密耦合，我们可以让 `Site.master` 和 `Alternate.master` 派生自包含公共成员定义的公共基类。 接下来，我们可以更新 `@MasterType` 指令以引用此公共基类型。

### <a name="creating-a-custom-base-master-page-class"></a>创建自定义基母版页类

将新的类文件添加到名为 `BaseMasterPage.vb` `App_Code` 文件夹中，并将其从 `System.Web.UI.MasterPage`派生。 我们需要在 `BaseMasterPage`中定义 `RefreshRecentProductsGrid` 方法和 `GridMessageText` 属性，但我们不能只是将它们从 `Site.master` 中移出，因为这些成员使用的是特定于 `Site.master` 母版页的 Web 控件（`RecentProducts` GridView 和 `GridMessage` 标签）。

我们需要做的就是将 `BaseMasterPage` 配置为在其中定义这些成员，但实际是通过 `BaseMasterPage`派生类（`Site.master` 和 `Alternate.master`）实现的。 通过将类标记为 `MustInherit` 并将其成员标记为 `MustOverride`，可以实现这种类型的继承。 简而言之，将这些关键字添加到类及其两个成员，宣布 `BaseMasterPage` 未实现 `RefreshRecentProductsGrid` 和 `GridMessageText`，但其派生类将为。

还需要在 `BaseMasterPage` 中定义 `PricesDoubled` 事件，并为派生类提供一种引发事件的方法。 .NET Framework 中使用的模式可帮助实现此行为，这是在基类中创建一个公共事件，并添加一个名为 `OnEventName`的受保护的可重写方法。 然后，派生类可以调用此方法来引发事件，或者可以重写它以在引发事件之前或之后立即执行代码。

更新 `BaseMasterPage` 类，使其包含以下代码：

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample8.vb)]

接下来，请跳到 `Site.master` 代码隐藏类，并使其从 `BaseMasterPage`派生。 由于 `BaseMasterPage` 包含标记 `MustOverride` 成员，因此需要在 `Site.master`中覆盖这些成员。 将 `Overrides` 关键字添加到方法和属性定义。 此外，使用对基类的 `OnPricesDoubled` 方法的调用来更新在 `DoublePrice` 按钮的 `Click` 事件处理程序中引发 `PricesDoubled` 事件的代码。

修改后，`Site.master` 代码隐藏类应包含以下代码：

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample9.vb)]

我们还需要更新 `Alternate.master`的代码隐藏类，使其从 `BaseMasterPage` 派生并重写两个 `MustOverride` 成员。 但是，因为 `Alternate.master` 不包含列出了在将新产品添加到数据库后显示消息的 GridView，也不包含显示消息的 GridView，所以这些方法不需要执行任何操作。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample10.vb)]

### <a name="referencing-the-base-master-page-class"></a>引用基母版页类

现在，我们已完成了 `BaseMasterPage` 类，并让我们的两个母版页对其进行扩展，最后一步是更新 `~/Admin/AddProduct.aspx` 并 `~/Admin/Products.aspx` 页来引用此通用类型。 首先在以下两个页面中更改 `@MasterType` 指令：

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample11.aspx)]

结束时间：

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample12.aspx)]

`@MasterType` 属性现在引用基类型（`BaseMasterPage`），而不是引用文件路径。 因此，在这两个页面的代码隐藏类中使用的强类型 `Master` 属性现在为类型 `BaseMasterPage` （而不是类型 `Site`）。 利用此更改，`~/Admin/Products.aspx`。 以前，这会导致发生强制转换错误，因为该页配置为使用 `Alternate.master` 母版页，而 `@MasterType` 指令引用了 `Site.master` 文件。 但现在页面呈现时没有错误。 这是因为 `Alternate.master` 的母版页可以转换为 `BaseMasterPage` 类型的对象（因为它扩展了它）。

`~/Admin/AddProduct.aspx`需要进行一小的更改。 DetailsView 控件的 `ItemInserted` 事件处理程序同时使用强类型 `Master` 属性和松散类型化的 `Page.Master` 属性。 我们在更新 `@MasterType` 指令时修复了强类型引用，但我们仍需要更新松类型引用。 替换以下代码行：

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample13.vb)]

通过以下方式，将 `Page.Master` 转换为基类型：

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample14.vb)]

## <a name="step-4-determining-what-master-page-to-bind-to-the-content-pages"></a>步骤4：确定要绑定到内容页的母版页

`BasePage` 类当前将所有内容页的 `MasterPageFile` 属性设置为页面生命周期的 PreInit 阶段中的硬编码值。 我们可以更新此代码，使其基于某个外部因素的母版页。 可能要加载的母版页依赖于当前登录用户的首选项。 在这种情况下，我们需要在 `BasePage` 查找当前正在访问的用户的母版页首选项的 `OnPreInit` 方法中编写代码。

让我们创建一个网页，该网页允许用户选择要使用的母版页-`Site.master` 或 `Alternate.master` 并将此选项保存到 Session 变量中。 首先在名为 `ChooseMasterPage.aspx`的根目录中创建一个新网页。 创建此页面（或任何其他内容页面之后）时，无需将其绑定到母版页，因为母版页是以编程方式在 `BasePage`中设置的。 但是，如果不将新页绑定到母版页，则新页的默认声明性标记将包含由母版页提供的 Web 窗体和其他内容。 需要手动将此标记替换为适当的内容控件。 出于此原因，我发现将新的 ASP.NET 页面绑定到母版页更容易。

> [!NOTE]
> 由于 `Site.master` 和 `Alternate.master` 具有相同的一组 ContentPlaceHolder 控件，因此在创建新的内容页时选择的母版页并不重要。 为保持一致性，我建议使用 `Site.master`。

[![将新的内容页添加到网站](specifying-the-master-page-programmatically-vb/_static/image14.png)](specifying-the-master-page-programmatically-vb/_static/image13.png)

**图 05**：向网站添加新的内容页（[单击以查看完全大小的图像](specifying-the-master-page-programmatically-vb/_static/image15.png)）

更新 `Web.sitemap` 文件以包含本课中的条目。 将以下标记添加到母版页的 `<siteMapNode>` 下，并 ASP.NET AJAX 课程：

[!code-xml[Main](specifying-the-master-page-programmatically-vb/samples/sample15.xml)]

在将任何内容添加到 `ChooseMasterPage.aspx` 页面之前，请花点时间更新页面的代码隐藏类，使其从 `BasePage` （而不是 `System.Web.UI.Page`）派生。 接下来，向页面添加一个 DropDownList 控件，将其 `ID` 属性设置为 `MasterPageChoice`，然后添加两个 `Text` 值为 "~/Site.master" 和 "~/Alternate.master" 的 ListItems。

将按钮 Web 控件添加到页面，并将其 `ID` 和 `Text` 属性分别设置为 `SaveLayout` 和 "保存布局选项"。 此时，页面的声明性标记应如下所示：

[!code-aspx[Main](specifying-the-master-page-programmatically-vb/samples/sample16.aspx)]

首次访问页面时，需要显示用户当前选定的母版页选项。 创建 `Page_Load` 事件处理程序并添加以下代码：

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample17.vb)]

上述代码仅在第一页访问（而不是在后续回发上）执行。 它首先检查会话变量 `MyMasterPage` 是否存在。 如果是，则它会尝试在 `MasterPageChoice` DropDownList 中查找匹配的匹配项。 如果找到匹配的匹配，则将其 `Selected` 属性设置为 `True`。

我们还需要将用户的选择保存到 `MyMasterPage` Session 变量中的代码。 为 "`SaveLayout`" 按钮的 `Click` 事件创建事件处理程序，并添加以下代码：

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample18.vb)]

> [!NOTE]
> 在回发时，`Click` 事件处理程序的执行时间已被选中。 因此，在下一页访问之前，用户的下拉列表选择将不起作用。 `Response.Redirect` 强制浏览器重新请求 `ChooseMasterPage.aspx`。

`ChooseMasterPage.aspx` 页面完成后，最终任务就是 `BasePage` 分配 `MasterPageFile` 属性，具体取决于 `MyMasterPage` Session 变量的值。 如果未设置会话变量，则 `BasePage` 默认为 `Site.master`。

[!code-vb[Main](specifying-the-master-page-programmatically-vb/samples/sample19.vb)]

> [!NOTE]
> 我将指定 `Page` 对象的 `MasterPageFile` 属性的代码从 `OnPreInit` 事件处理程序移到了两个单独的方法中。 第一种方法 `SetMasterPageFile`，将 `MasterPageFile` 属性分配给第二个方法（`GetMasterPageFileFromSession`）返回的值。 我将 `SetMasterPageFile` 方法标记为 `Overridable` 这样，扩展 `BasePage` 的未来类可以根据需要重写该方法以实现自定义逻辑。 在下一教程中，我们将介绍覆盖 `BasePage`的 `SetMasterPageFile` 属性的示例。

准备好此代码后，请访问 `ChooseMasterPage.aspx` 页面。 最初，会选择 `Site.master` 母版页（参见图6），但用户可以从下拉列表中选择不同的母版页。

[使用 "站点" 母版页显示 ![内容页](specifying-the-master-page-programmatically-vb/_static/image17.png)](specifying-the-master-page-programmatically-vb/_static/image16.png)

**图 06**：使用 `Site.master` 母版页显示内容页（[单击以查看完全大小的图像](specifying-the-master-page-programmatically-vb/_static/image18.png)）

[现在使用备用母版页母版页显示 ![内容页](specifying-the-master-page-programmatically-vb/_static/image20.png)](specifying-the-master-page-programmatically-vb/_static/image19.png)

**图 07**：现在使用 "`Alternate.master`" 母版页显示内容页面（[单击查看完全大小的图像](specifying-the-master-page-programmatically-vb/_static/image21.png)）

## <a name="summary"></a>总结

访问内容页时，其内容控件与母版页的 ContentPlaceHolder 控件一起融合。 内容页的母版页由 `Page` 类的 `MasterPageFile` 属性表示，该属性在初始化阶段分配给 `@Page` 指令的 `MasterPageFile` 特性。 在本教程中，我们可以为 `MasterPageFile` 属性分配一个值，前提是在 PreInit 阶段结束之前执行此操作。 如果能够以编程方式指定母版页，则会为更高级的方案打开门，如根据外部因素动态地将内容页绑定到母版页。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 页生命周期关系图](http://emanish.googlepages.com/Asp.Net2.0Lifecycle.PNG)
- [ASP.NET 页生命周期概述](https://msdn.microsoft.com/library/ms178472.aspx)
- [ASP.NET 主题和外观概述](https://msdn.microsoft.com/library/ykzx33wh.aspx)
- [母版页：提示、技巧和陷阱](http://www.odetocode.com/articles/450.aspx)
- [ASP.NET 中的主题](http://www.odetocode.com/articles/423.aspx)

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Suchi Banerjee。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一页](master-pages-and-asp-net-ajax-vb.md)
> [下一页](nested-master-pages-vb.md)
