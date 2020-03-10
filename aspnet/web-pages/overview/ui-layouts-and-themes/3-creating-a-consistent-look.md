---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: 在 ASP.NET 网页（Razor）网站中创建一致的布局 |Microsoft Docs
author: Rick-Anderson
description: 为了更高效地为网站创建网页，你可以为网站创建可重用的内容块（如页眉和页脚），并且你可以创建
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 3f63ce68ae4c13970ac0df196167ace0b22b592c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509096"
---
# <a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET 网页（Razor）网站中创建一致的布局

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何在 ASP.NET 网页（Razor）网站中使用布局页来创建可重用的内容块（如页眉和页脚），并为站点中的所有页面创建一致的外观。
> 
> **你将学习的内容：** 
> 
> - 如何创建可重用的内容块，如页眉和页脚。
> - 如何使用布局为站点中的所有页面创建一致的外观。
> - 如何在运行时将数据传递到布局页。
> 
> 下面是本文中介绍的 ASP.NET 功能：
> 
> - 内容块：包含要插入到多页中的 HTML 格式内容的文件。
> - 布局页，页面包含可由网站上的页面共享的 HTML 格式的内容。
> - `RenderPage`、`RenderBody`和 `RenderSection` 方法，这些方法告诉 ASP.NET 在何处插入页面元素。
> - `PageData` 字典，可用于在内容块和布局页之间共享数据。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

## <a name="about-layout-pages"></a>关于布局页

许多网站具有显示在每个页面上的内容，如页眉和页脚，或指示用户登录用户的框。 使用 ASP.NET 可以创建一个包含文本、标记和代码的单独文件，就像常规网页一样。 然后，你可以在要显示信息的站点上的其他页面中插入内容块。 这样就无需将相同的内容复制并粘贴到每个页面。 创建类似于这样的常用内容还可以更轻松地更新站点。 如果需要更改内容，只需更新单个文件，所做的更改就会反映到内容插入位置。

下图显示内容块的工作方式。 当浏览器请求 web 服务器中的某个页面时，ASP.NET 会在主页中调用 `RenderPage` 方法的位置插入内容块。 然后，将 "完成（合并）" 页发送到浏览器。

![显示 RenderPage 方法如何将引用的页插入当前页的概念图。](3-creating-a-consistent-look/_static/image1.jpg)

在此过程中，您将创建一个引用位于不同文件中的两个内容块（标头和脚注）的页。 你可以在站点中的任何页面上使用这些相同的内容块。 完成后，会看到如下所示的页面：

![显示浏览器中的页面的屏幕截图，其中包含对 RenderPage 方法的调用的页面。](3-creating-a-consistent-look/_static/image2.png)

1. 在网站的根文件夹中，创建一个名为 "*索引*" 的文件。
2. 将现有标记替换为以下内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. 在根文件夹中，创建一个名为 "*共享*" 的文件夹。

    > [!NOTE]
    > 常见的做法是在名为*shared*的文件夹中存储网页间共享的文件。
4. 在*共享*文件夹中，创建一个名为 *\_* 的文件。
5. 将所有现有内容替换为以下内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    请注意，文件名是 *\_的标头*，以下划线（\_）作为前缀。 如果 ASP.NET 的名称以下划线开头，则不会向浏览器发送页面。 这可防止用户直接请求（无意或其他）这些页面。 最好是使用下划线来命名包含内容块的页面，因为您并不想让用户完全请求将这些页面&#8212;完全插入到其他页面。
6. 在*共享*文件夹中，创建一个名为 *\_页脚*的文件，并将内容替换为以下内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. 在 "*索引*" 页上，添加两个对 `RenderPage` 方法的调用，如下所示：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    这说明了如何将内容块插入到网页中。 调用 `RenderPage` 方法，并向其传递要在该点插入其内容的文件的名称。 此时，您要将\_的标\_*头*的内容插入到 *索引的 cshtml*文件中。
8. 在浏览器中运行 "*索引*" 页。 （在 WebMatrix 中，在 "**文件**" 工作区中，右键单击该文件，然后选择 "**在浏览器中启动**"。）
9. 在浏览器中查看页面源。 （例如，在 Internet Explorer 中，右键单击该页面，然后单击 "**查看源**"。）

    这使你可以查看发送到浏览器的网页标记，该标记将索引页标记与内容块合并在一起。 下面的示例显示了为*索引.* 对插入到*Index*中的 `RenderPage` 的调用已替换为页眉和页脚文件的实际内容。

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a>使用布局页创建一致的外观

到目前为止，您已经了解到，在多个页面上包含相同的内容是很容易的。 若要为站点创建一致的外观，一种更结构化的方法是使用布局页。 布局页定义网页的结构，但不包含任何实际内容。 创建布局页后，可以创建包含内容的网页，然后将其链接到 "布局" 页。 显示这些页面后，将根据布局页面设置这些页面的格式。 （在这种意义上，布局页充当其他页中定义的内容的一种模板。）

布局页与任何 HTML 页面一样，只是它包含对 `RenderBody` 方法的调用。 "布局" 页中 `RenderBody` 方法的位置确定将包含内容页中信息的位置。

下图显示如何在运行时组合内容页和布局页以生成已完成的网页。 浏览器请求内容页。 "内容" 页中有代码，它指定要用于页结构的布局页。 在布局页中，将在调用 `RenderBody` 方法的位置插入内容。 还可以通过调用 `RenderPage` 方法（在上一节中的方式）将内容块插入到布局页中。 网页完成后，将发送到浏览器。

![显示浏览器中的页面的屏幕截图，其中包含对 RenderBody 方法的调用的页面。](3-creating-a-consistent-look/_static/image3.jpg)

下面的过程演示如何创建布局页并将内容页链接到它。

1. 在网站的*共享*文件夹中，创建一个名为 *\_Layout1*的文件。
2. 将所有现有内容替换为以下内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    您可以在布局页中使用 `RenderPage` 方法来插入内容块。 布局页只能包含对 `RenderBody` 方法的一次调用。
3. 在*共享*文件夹中，创建一个名为 *\_.header2*的文件，并将所有现有内容替换为以下内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. 在根文件夹中，创建一个新文件夹并将其命名为*样式*。
5. 在 "*样式*" 文件夹中，创建名为 " *web.config* " 的文件并添加以下样式定义：

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    此处的样式定义仅用于显示样式表如何与布局页一起使用。 如果需要，可以为这些元素定义自己的样式。
6. 在根文件夹中，创建一个名为*Content1*的文件，并将所有现有内容替换为以下内容：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    这是将使用布局页的页面。 页面顶部的代码块指示用于设置此内容格式的布局页。
7. 在浏览器中运行*Content1* 。 呈现的页使用 *\_Layout1*中定义的格式和样式表，以及在*Content1*中定义的文本（内容）。

    ![[图像]](3-creating-a-consistent-look/_static/image4.png)

    您可以重复步骤6来创建可以共享同一布局页的其他内容页面。

    > [!NOTE]
    > 你可以设置站点，以便可以为文件夹中的所有内容页自动使用相同的布局页。 有关详细信息，请参阅为[ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906)。

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a>设计具有多个内容节的布局页

内容页可以有多个部分，如果要使用具有可替换内容的多个区域的布局，这会很有用。 在 "内容" 页中，为每个部分指定唯一名称。 （默认节未命名。）在 "布局" 页中，添加一个 `RenderBody` 方法，以指定应显示未命名（默认）节的位置。 然后，添加单独的 `RenderSection` 方法以便单独呈现命名节。

下图显示了 ASP.NET 如何处理划分为多个部分的内容。 每个命名节包含在内容页的节块中。 （在示例中，它们被命名为 `Header` 和 `List`。）在调用 `RenderSection` 方法时，框架会将 "内容" 部分插入布局页中。 如前文所述，将在调用 `RenderBody` 方法的位置插入未命名的（默认）部分。

![显示 RenderSection 方法将引用节插入当前页的方式的概念图。](3-creating-a-consistent-look/_static/image5.jpg)

此过程演示如何创建包含多个内容节的内容页，以及如何使用支持多个内容节的布局页呈现该内容页。

1. 在*共享*文件夹中，创建一个名为 *\_Layout2*的文件。
2. 将所有现有内容替换为以下内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    使用 `RenderSection` 方法可呈现标头和列表部分。
3. 在根文件夹中，创建一个名为*Content2*的文件，并将所有现有内容替换为以下内容：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    此内容页在页面顶部包含一个代码块。 每个命名节包含在一个节块中。 页面的其余部分包含默认（未命名）内容部分。
4. 在浏览器中运行*Content2* 。

    ![显示浏览器中的页面的屏幕截图，其中包含对 RenderSection 方法的调用的页面。](3-creating-a-consistent-look/_static/image6.png)

## <a name="making-content-sections-optional"></a>使内容部分可选

通常，在内容页中创建的部分必须与布局页中定义的节匹配。 如果发生以下任何情况，则会出现错误：

- "内容" 页包含没有布局页中对应部分的部分。
- "布局" 页包含没有内容的部分。
- 布局页包含尝试多次呈现同一节的方法调用。

但是，您可以通过在布局页中将节声明为可选，来覆盖命名部分的此行为。 这允许您定义多个内容页，这些内容页可以共享布局页，但对于特定部分可能有也可能没有内容。

1. 打开*Content2*并删除以下部分：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. 保存该页，然后在浏览器中运行它。 将显示一条错误消息，因为内容页不提供布局页中定义的节的内容，即页眉节。

    ![屏幕截图，显示在运行调用 RenderSection 方法但未提供相应部分的页面时发生的错误。](3-creating-a-consistent-look/_static/image7.png)
3. 在*共享*文件夹中，打开 *\_Layout2* "页面并替换以下行：

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    替换为以下代码：

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    作为替代方法，您可以将之前的代码行替换为以下代码块，这会产生相同的结果：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. 再次在浏览器中运行*Content2*页。 （如果你仍在浏览器中打开此页，则可以只刷新它。）这一次，即使该页没有标头，也不会显示任何错误。

## <a name="passing-data-to-layout-pages"></a>将数据传递到布局页

你可能在 "内容" 页中定义了在布局页中需要引用的数据。 如果是这样，则需要将数据从 "内容" 页传递到 "布局" 页。 例如，你可能想要显示用户的登录状态，或者可能想要基于用户输入显示或隐藏内容区域。

若要将数据从内容页传递到布局页，可以将值放入内容页的 `PageData` 属性。 `PageData` 属性是名称/值对的集合，这些名称/值对保存你要在页面间传递的数据。 然后，您可以在 "布局" 页中读取 `PageData` 属性的值。

下面是另一个关系图。 这会显示 ASP.NET 如何使用 `PageData` 属性将值从内容页传递到布局页。 当 ASP.NET 开始生成网页时，它将创建 `PageData` 集合。 在 "内容" 页中，你将编写用于将数据放入 `PageData` 集合中的代码。 "内容" 页或其他内容块中的其他部分也可以访问 `PageData` 集合中的值。

![显示内容页如何填充 PageData 字典并将该信息传递到布局页的概念图。](3-creating-a-consistent-look/_static/image8.jpg)

下面的过程演示如何将数据从内容页传递到布局页。 当页面运行时，它会显示一个按钮，使用户可以隐藏或显示在布局页面中定义的列表。 当用户单击该按钮时，它会在 "`PageData`" 属性中设置 true/false （布尔值）值。 布局页读取该值，如果该值为 false，则隐藏列表。 还可以在 "内容" 页中使用该值来确定是否显示 "**隐藏列表**" 按钮或 "**显示列表**" 按钮。

![[图像]](3-creating-a-consistent-look/_static/image9.jpg)

1. 在根文件夹中，创建一个名为*Content3*的文件，并将所有现有内容替换为以下内容：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    该代码将两个数据片段存储在 "`PageData` &#8212; " 属性 "网页标题" 和 "true" 或 "false" 以指定是否显示列表。

    请注意，ASP.NET 允许你使用代码块有条件地将 HTML 标记放入页面。 例如，页体中的 `if/else` 块决定显示哪一窗体，具体取决于 `PageData["ShowList"]` 是否设置为 true。
2. 在*共享*文件夹中，创建一个名为 *\_Layout3*的文件，并将所有现有内容替换为以下内容：

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    布局页在 `<title>` 元素中包含一个表达式，该表达式可获取 `PageData` 属性的标题值。 它还使用 `PageData` 属性的 `ShowList` 值来确定是否显示列表内容块。
3. 在*共享*文件夹中，创建一个名为 *\_* 的文件，并将所有现有内容替换为以下内容：

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. 在浏览器中运行*Content3*页。 此时将显示该页，其中的列表显示在该页的左侧，**隐藏列表**按钮位于底部。

    ![屏幕截图，显示包含列表的页面和一个显示 "隐藏列表" 的按钮。](3-creating-a-consistent-look/_static/image10.png)
5. 单击 "**隐藏列表**"。 列表消失，按钮会变为 "**显示列表**"。

    ![显示页的屏幕截图，其中不包含列表和显示 "显示列表" 的按钮。](3-creating-a-consistent-look/_static/image11.png)
6. 单击 "**显示列表**" 按钮，然后重新显示列表。

## <a name="additional-resources"></a>其他资源

[为 ASP.NET 网页自定义站点范围的行为](https://go.microsoft.com/fwlink/?LinkId=202906)
