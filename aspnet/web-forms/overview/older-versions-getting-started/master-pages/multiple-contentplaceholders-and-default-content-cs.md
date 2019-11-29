---
uid: web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-cs
title: 多个 Contentplaceholder 和默认内容C#（） |Microsoft Docs
author: rick-anderson
description: 检查如何将多个内容占位符添加到母版页，以及如何在内容占位符中指定默认内容。
ms.author: riande
ms.date: 05/21/2008
ms.assetid: b9b9798b-027d-46cc-9636-473378e437ac
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-cs
msc.type: authoredcontent
ms.openlocfilehash: e902bcae05c0e7976a20293f2b01e5f2e2bee13a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639538"
---
# <a name="multiple-contentplaceholders-and-default-content-c"></a>多个 ContentPlaceHolder 和默认内容 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_02_CS.zip)或[下载 PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_02_CS.pdf)

> 检查如何将多个内容占位符添加到母版页，以及如何在内容占位符中指定默认内容。

## <a name="introduction"></a>简介

在前面的教程中，我们介绍了母版页如何使 ASP.NET 开发人员能够创建一致的站点范围布局。 母版页将同时定义它的所有内容页和区域的通用标记，这些标记是逐页自定义的。 在上一教程中，我们创建了一个简单的母版页（`Site.master`）和两个内容页（`Default.aspx` 和 `About.aspx`）。 母版页包括两个分别名为 `head` 和 `MainContent`的 Contentplaceholder，分别位于 `<head>` 元素和 Web 窗体中。 虽然每个内容页都有两个内容控件，但我们只为对应于 `MainContent`的标记指定了标记。

作为 `Site.master`中两个 ContentPlaceHolder 控件的出现，一个母版页可能包含多个 Contentplaceholder。 而且，母版页可以为 ContentPlaceHolder 控件指定默认标记。 然后，内容页可以选择指定自己的标记或使用默认标记。 在本教程中，我们将介绍如何在母版页中使用多个内容控件，并查看如何在 ContentPlaceHolder 控件中定义默认标记。

## <a name="step-1-adding-additional-contentplaceholder-controls-to-the-master-page"></a>步骤1：向母版页添加其他 ContentPlaceHolder 控件

许多网站设计在屏幕上包含多个区域，这些区域是逐页自定义的。 `Site.master`，我们在上一教程中创建的母版页包含名为 `MainContent`的 Web 窗体中的单个 ContentPlaceHolder。 具体而言，此 ContentPlaceHolder 位于 `mainContent` `<div>` 元素中。

图1显示了通过浏览器查看 `Default.aspx`。 用红色圈出的区域是与 `MainContent`相对应的页面特定标记。

[![带圆圈的区域显示当前逐页自定义的区域](multiple-contentplaceholders-and-default-content-cs/_static/image2.png)](multiple-contentplaceholders-and-default-content-cs/_static/image1.png)

**图 01**：带圆圈的区域显示当前逐页自定义的区域（[单击以查看完全大小的图像](multiple-contentplaceholders-and-default-content-cs/_static/image3.png)）

假设除了图1所示的区域外，我们还需要将特定于页面的项目添加到 "课程和新闻" 部分下的左侧列中。 为实现此目的，我们向母版页添加了另一个 ContentPlaceHolder 控件。 若要继续操作，请在 Visual Web Developer 中打开 `Site.master` 母版页，然后将 "ContentPlaceHolder" 控件从 "工具箱" 拖动到 "新闻" 部分后面的设计器。 将 ContentPlaceHolder 的 `ID` 设置为 `LeftColumnContent`。

[![将 ContentPlaceHolder 控件添加到母版页的左栏](multiple-contentplaceholders-and-default-content-cs/_static/image5.png)](multiple-contentplaceholders-and-default-content-cs/_static/image4.png)

**图 02**：将 ContentPlaceHolder 控件添加到母版页的左栏（[单击以查看完全大小的图像](multiple-contentplaceholders-and-default-content-cs/_static/image6.png)）

向母版页添加 `LeftColumnContent` ContentPlaceHolder 后，我们可以通过在页面中包含内容控件（其 `ContentPlaceHolderID` 设置为 `LeftColumnContent`）来逐页定义此区域的内容。 我们在步骤2中检查此过程。

## <a name="step-2-defining-content-for-the-new-contentplaceholder-in-the-content-pages"></a>步骤2：在内容页中定义新 ContentPlaceHolder 的内容

将新的内容页添加到网站时，Visual Web Developer 会在页中为所选母版页中的每个 ContentPlaceHolder 自动创建一个内容控件。 将 `LeftColumnContent` ContentPlaceHolder 添加到了步骤1中的母版页后，新 ASP.NET 页面现在将有三个内容控件。

为了说明这一点，请将一个新的内容页添加到绑定到 `Site.master` 母版页的名为 `MultipleContentPlaceHolders.aspx` 的根目录。 Visual Web Developer 通过以下声明性标记创建此页：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample1.aspx)]

在引用 `MainContent` Contentplaceholder （`Content2`）的内容控件中输入一些内容。 接下来，将以下标记添加到 `Content3` 内容控件（引用 `LeftColumnContent` ContentPlaceHolder）：

[!code-html[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample2.html)]

添加此标记后，通过浏览器访问此页。 如图3所示，放置在 `Content3` 内容控件中的标记将显示在新闻部分下的左栏中（用红色圆圈）。 放置在 `Content2` 中的标记将显示在该页的右部分（用蓝色圆圈）。

[![左栏现在包含新闻部分下特定于页面的内容](multiple-contentplaceholders-and-default-content-cs/_static/image8.png)](multiple-contentplaceholders-and-default-content-cs/_static/image7.png)

**图 03**：左栏现在包含新闻部分下特定于页面的内容（[单击以查看完全大小的图像](multiple-contentplaceholders-and-default-content-cs/_static/image9.png)）

### <a name="defining-content-in-existing-content-pages"></a>在现有内容页中定义内容

创建新的 "内容" 页将自动包含我们在步骤1中添加的 ContentPlaceHolder 控件。 但这两个现有的内容页-`About.aspx` 和 `Default.aspx`-没有 `LeftColumnContent` ContentPlaceHolder 的内容控件。 若要在这两个现有页面中指定此 ContentPlaceHolder 的内容，需要添加一个内容控件。

与大多数 ASP.NET Web 控件不同，Visual Web Developer 工具箱不包含内容控件项。 我们可以手动在 "源" 视图中键入内容控件的声明性标记，但更简单快捷的方法是使用设计视图。 打开 `About.aspx` 页面并切换到设计视图。 如图4所示，`LeftColumnContent` ContentPlaceHolder 将出现在设计视图中;如果将鼠标悬停在其上方，则标题显示为 "LeftColumnContent （母版）"。 标题中包含 "Master" 表示此 ContentPlaceHolder 的页面中没有定义内容控件。 如果存在 ContentPlaceHolder 的内容控件（与 `MainContent`的情况相同），则标题将显示： "*ContentPlaceHolderID* （自定义）"。

若要将 `LeftColumnContent` ContentPlaceHolder 的内容控件添加到 `About.aspx`，请展开 ContentPlaceHolder 的智能标记，然后单击 "创建自定义内容" 链接。

[![有关 .aspx 的设计视图显示 LeftColumnContent ContentPlaceHolder](multiple-contentplaceholders-and-default-content-cs/_static/image11.png)](multiple-contentplaceholders-and-default-content-cs/_static/image10.png)

**图 04**： "设计" 视图 `About.aspx` 显示 `LeftColumnContent` ContentPlaceHolder （[单击查看完全大小的图像](multiple-contentplaceholders-and-default-content-cs/_static/image12.png)）

单击 "创建自定义内容" 链接会在页面中生成所需的内容控件，并将其 `ContentPlaceHolderID` 属性设置为 ContentPlaceHolder 的 `ID`。 例如，单击 `About.aspx` 中 `LeftColumnContent` 区域的 "创建自定义内容" 链接，可将以下声明性标记添加到页面：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample3.aspx)]

### <a name="omitting-content-controls"></a>省略内容控件

ASP.NET 不要求所有内容页都包含母版页中定义的每个 ContentPlaceHolder 和每个的内容控件。 如果省略内容控件，ASP.NET 引擎将使用在母版页中的 ContentPlaceHolder 中定义的标记。 此标记被称为 ContentPlaceHolder 的*默认内容*，在某些区域的内容在大多数页面中很常见，但需要为少量页面自定义的情况下很有用。 步骤3探讨了如何在母版页中指定默认内容。

目前，`Default.aspx` 包含 `head` 和 `MainContent` Contentplaceholder 的两个内容控件;它没有 `LeftColumnContent`的内容控件。 因此，`Default.aspx` 呈现时，将使用 `LeftColumnContent` ContentPlaceHolder 的默认内容。 由于我们还在为此 ContentPlaceHolder 定义了任何默认内容，因此净效果是不会为此区域发出任何标记。 若要验证此行为，请通过浏览器访问 `Default.aspx`。 如图5所示，在新闻部分下的左栏中不会发出任何标记。

[![不会为 LeftColumnContent ContentPlaceHolder 呈现任何内容。](multiple-contentplaceholders-and-default-content-cs/_static/image14.png)](multiple-contentplaceholders-and-default-content-cs/_static/image13.png)

**图 05**：对于 `LeftColumnContent` ContentPlaceHolder 不呈现任何内容（[单击以查看完全大小的图像](multiple-contentplaceholders-and-default-content-cs/_static/image15.png)）

## <a name="step-3-specifying-default-content-in-the-master-page"></a>步骤3：在母版页中指定默认内容

某些网站设计包含一个区域，该区域的内容与站点中所有页面的内容相同，但有一个或两个例外。 请考虑一个支持用户帐户的网站。 此类站点需要一个登录页面，访问者可以在其中输入其凭据以登录到站点。 为了加快登录过程，网站设计人员可能会在每个页面的左上角包含 "用户名" 和 "密码" 文本框，使用户无需显式访问登录页即可登录。 尽管这些 "用户名" 和 "密码" 文本框在大多数页面中都很有用，但它们在登录页中是多余的，它已经包含用户凭据的文本框。

若要实现此设计，可以在母版页的左上角创建一个 ContentPlaceHolder 控件。 在左上角显示 "用户名" 和 "密码" 文本框的每一页都将为此 ContentPlaceHolder 创建一个内容控件，并添加所需的接口。 另一方面，登录页将忽略为此 ContentPlaceHolder 添加内容控件，或创建没有定义标记的内容控件。 这种方法的缺点是，我们必须记得将 "用户名" 和 "密码" 文本框添加到添加到网站的每个页面（登录页除外）。 这会询问问题。 我们很可能忘记将这些文本框添加到一两页，更糟的是，我们可能不会正确实现接口（或许只需添加一个文本框，而不是两个）。

更好的解决方案是将 "用户名" 和 "密码" 文本框定义为 ContentPlaceHolder 的默认内容。 这样，我们只需在不显示 "用户名" 和 "密码" 文本框的几个页面（例如 "登录" 页）中覆盖此默认内容。 为了说明如何为 ContentPlaceHolder 控件指定默认内容，让我们实现刚才介绍的方案。

> [!NOTE]
> 本教程的其余部分将更新网站，以便在所有页面（登录页）的左栏中包含登录界面。 不过，本教程不会检查如何将网站配置为支持用户帐户。 有关本主题的详细信息，请参阅我的[Forms 身份验证、授权、用户帐户和角色](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)教程。

### <a name="adding-a-contentplaceholder-and-specifying-its-default-content"></a>添加 ContentPlaceHolder 并指定其默认内容

打开 `Site.master` 母版页，并将以下标记添加到 `DateDisplay` 标签和课程部分之间的左栏：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample4.aspx)]

添加此标记后，母版页的设计视图应类似于图6。

[![母版页包含登录控件](multiple-contentplaceholders-and-default-content-cs/_static/image17.png)](multiple-contentplaceholders-and-default-content-cs/_static/image16.png)

**图 06**：母版页包含登录控件（[单击以查看完全大小的图像](multiple-contentplaceholders-and-default-content-cs/_static/image18.png)）

此 ContentPlaceHolder `QuickLoginUI`将登录 Web 控件作为其默认内容。 登录控件显示一个用户界面，该用户界面提示用户输入其用户名和密码以及一个 "登录" 按钮。 单击 "登录" 按钮时，登录控件在内部根据成员身份 API 验证用户的凭据。 若要在实践中使用此登录控件，则需要将站点配置为使用成员资格。 本主题超出了本教程的范围;有关构建支持用户帐户的 web 应用程序的详细信息，请参阅我的[Forms 身份验证、授权、用户帐户和角色](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)教程。

随意自定义登录控件的行为或外观。 我已经设置了两个属性： `TitleText` 和 `FailureAction`。 默认为 "登录" 的 `TitleText` 属性值显示在控件的用户界面的顶部。 我已经设置了此属性，以便它将文本 "登录" 显示为 `<h3>` 元素。 `FailureAction` 属性指示用户的凭据无效时应执行的操作。 默认值为 `Refresh`的值，这会使用户处于同一页中，并在登录控件中显示失败消息。 我已将其更改为 `RedirectToLoginPage`，这会在凭据无效的情况下将用户发送到登录页。 当用户尝试从其他某个页面登录时，我更喜欢将用户发送到登录页，但会失败，因为登录页面可能包含无法轻松容纳到左栏的其他说明和选项。 例如，登录页面可能包括用于检索忘记密码或创建新帐户的选项。

### <a name="creating-the-login-page-and-overriding-the-default-content"></a>创建登录页并覆盖默认内容

母版页完成后，下一步是创建登录页。 将 ASP.NET 页面添加到名为 `Login.aspx`的网站根目录，并将其绑定到 `Site.master` 的母版页。 这样做会创建一个包含四个内容控件的页面，其中每个 `Site.master`中定义的 Contentplaceholder。

将登录控件添加到 `MainContent` 内容控件。 同样，也可以随意将任何内容添加到 `LeftColumnContent` 区域。 但是，请确保将 `QuickLoginUI` ContentPlaceHolder 的内容控件留空。 这将确保登录名控件不会显示在登录页的左列中。

为 `MainContent` 和 `LeftColumnContent` 区域定义内容后，登录页的声明性标记应如下所示：

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-cs/samples/sample5.aspx)]

图7在浏览器中查看时显示此页。 由于此页为 `QuickLoginUI` ContentPlaceHolder 指定了内容控件，因此它将覆盖在母版页中指定的默认内容。 最终效果是在母版页的设计视图中显示的登录控件（参见图6）不会在此页中呈现。

[![登录页 Represses QuickLoginUI ContentPlaceHolder 的默认内容](multiple-contentplaceholders-and-default-content-cs/_static/image20.png)](multiple-contentplaceholders-and-default-content-cs/_static/image19.png)

**图 07**：登录页 Represses `QuickLoginUI` ContentPlaceHolder 的默认内容（[单击查看完全大小的图像](multiple-contentplaceholders-and-default-content-cs/_static/image21.png)）

### <a name="using-the-default-content-in-new-pages"></a>使用新页面中的默认内容

我们希望在除登录页之外的所有页的左栏中显示登录控件。 若要实现此目的，登录页之外的所有内容页都应该省略 `QuickLoginUI` ContentPlaceHolder 的内容控件。 通过省略内容控件，将改为使用 ContentPlaceHolder 的默认内容。

我们现有的内容页-`Default.aspx`、`About.aspx`和 `MultipleContentPlaceHolders.aspx`，它们不包含 `QuickLoginUI` 的内容控件，因为在将 ContentPlaceHolder 控件添加到母版页之前，这些控件已创建。 因此，这些现有页面不需要更新。 但是，默认情况下，添加到网站的新页面包含 `QuickLoginUI` ContentPlaceHolder 的内容控件。 因此，在每次添加新的内容页时，我们必须记得删除这些内容控件（除非我们要重写 ContentPlaceHolder 的默认内容，如登录页的情况）。

若要删除内容控件，可以从 "源" 视图手动删除其声明性标记，或者从 "设计视图" 中，从智能标记中选择 "默认到母版页的内容" 链接。 这两种方法都将从页面中删除内容控件并生成相同的网络效果。

图8显示了通过浏览器查看 `Default.aspx`。 请记住，`Default.aspx` 仅在其声明性标记中指定了两个内容控件-一个用于 `head`，另一个用于 `MainContent`。 因此，将显示 `LeftColumnContent` 和 `QuickLoginUI` Contentplaceholder 的默认内容。

[显示 LeftColumnContent 和 QuickLoginUI Contentplaceholder 的默认内容 ![](multiple-contentplaceholders-and-default-content-cs/_static/image23.png)](multiple-contentplaceholders-and-default-content-cs/_static/image22.png)

**图 08**：显示 `LeftColumnContent` 和 `QuickLoginUI` Contentplaceholder 的默认内容（[单击以查看完全大小的图像](multiple-contentplaceholders-and-default-content-cs/_static/image24.png)）

## <a name="summary"></a>总结

ASP.NET 母版页模型允许在母版页中使用任意数量的 Contentplaceholder。 此外，Contentplaceholder 包括默认内容，该内容在内容页中没有相应的内容控件的情况下发出。 在本教程中，我们介绍了如何在母版页中包含其他 ContentPlaceHolder 控件，以及如何在新的和现有的 ASP.NET 页中定义这些新 Contentplaceholder 的内容控件。 我们还介绍了如何在 ContentPlaceHolder 中指定默认内容，这在只有少数页需要自定义特定区域中的其他标准化内容的情况下非常有用。

在下一教程中，我们将更详细地介绍 `head` ContentPlaceHolder，并了解如何以声明方式和编程方式逐页定义标题、元标记和其他 HTML 标头。

很高兴编程！

### <a name="about-the-author"></a>关于作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，创始人的多个 ASP/asp 和4GuysFromRolla.com 的作者已使用 Microsoft Web 技术，1998。 Scott 的工作方式是独立的顾问、培训师和撰稿人。 他的最新书籍是，[*在24小时内，sam ASP.NET 3.5*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 可以通过[http://ScottOnWriting.NET](http://scottonwriting.net/) [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)或通过他的博客访问 Scott。

### <a name="special-thanks-to"></a>特别感谢

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Suchi Banerjee。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](creating-a-site-wide-layout-using-master-pages-cs.md)
> [下一页](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
