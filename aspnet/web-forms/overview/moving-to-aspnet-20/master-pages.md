---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: 母版页 |Microsoft Docs
author: microsoft
description: 成功的网站的关键组件之一是一致的外观。 在 ASP.NET 1.x 中，开发人员使用用户控件来复制常见页面 elem 。
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: 36f2caf7c2c9bcafd22c8f6681c1d6b19fe5078a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457580"
---
# <a name="master-pages"></a>母版页

由[Microsoft](https://github.com/microsoft)

> 成功的网站的关键组件之一是一致的外观。 在 ASP.NET 1.x 中，开发人员使用用户控件跨 Web 应用程序复制常见页面元素。 虽然这无疑是一个可行的解决方案，但使用用户控件确实存在一些缺点。 例如，对用户控件位置的更改需要对一个站点中的多个页面进行更改。 在将用户控件插入页面后，还不会在设计视图中呈现这些控件。

成功的网站的关键组件之一是一致的外观。 在 ASP.NET 1.x 中，开发人员使用用户控件跨 Web 应用程序复制常见页面元素。 虽然这无疑是一个可行的解决方案，但使用用户控件确实存在一些缺点。 例如，对用户控件位置的更改需要对一个站点中的多个页面进行更改。 在将用户控件插入页面后，还不会在设计视图中呈现这些控件。

ASP.NET 2.0 将母版页作为一种保持一致的外观和感觉的方式引入，你很快就会看到，母版页表示对用户控件方法的重大改进。

## <a name="why-master-pages"></a>母版页的原因

您可能想知道为什么在 ASP.NET 2.0 中需要母版页。 毕竟，网站开发人员已在 ASP.NET 1.x 中使用用户控件在页面之间共享内容区域。 由于用户控件是创建通用布局的最佳解决方案，因此实际上有多种原因。

用户控件并不实际定义页面布局。 相反，它们定义了页面部分的布局和功能。 这两者之间的区别非常重要，因为它使用户控制解决方案的可管理性更难。 例如，要更改用户控件在页面上的位置，则必须编辑显示用户控件的实际页面。 如果只有几个页面，但在大型站点中，这种方法很快就会成为站点管理工作的麻烦！

使用用户控件定义通用布局的另一个缺点是，ASP.NET 本身的体系结构。 如果更改了用户控件的任何公共成员，则需要重新编译使用该用户控件的所有页。 接下来，ASP.NET 将在首次访问页面时重新 JIT。 同样，这会为较大的站点生成不可缩放的体系结构和站点管理问题。

这两个问题（及更多）都通过 ASP.NET 2.0 中的母版页得到了良好的处理。

## <a name="how-master-pages-work"></a>母版页的工作方式

母版页类似于其他页面的模板。 应在其他页面之间共享的页面元素（例如菜单、边框等）添加到母版页中。 将新页面添加到站点时，可以将它们与母版页关联。 与母版页关联的页称为 "**内容页**"。 默认情况下，内容页将从母版页获得外观。 但是，在创建母版页时，可以定义页面中内容页可以替换为其自身内容的部分。 使用 ASP.NET 2.0 中引入的新控件定义这些部分。**ContentPlaceHolder**控件。

一个母版页可以包含任意数量的 ContentPlaceHolder 控件（或全部无）。在 "内容" 页上，ContentPlaceHolder 控件中的内容显示在**内容**控件中，另一个新控件 ASP.NET 2.0。 默认情况下，内容页内容控件为空，因此你可以提供自己的内容。 如果要使用内容控件中的母版页的内容，则可以执行此操作，如本模块后面的内容所示。 内容控件通过内容控件的 ContentPlaceHolderID 特性映射到 ContentPlaceHolder 控件。 下面的代码将内容控件映射到母版页上名为 mainBody 的 ContentPlaceHolder 控件。

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> 你通常会听到人们将母版页描述为其他页面的基类。 事实上，事实不是这样。 母版页和内容页之间的关系不是继承之一。

**图 1**显示了在 Visual Studio 2005 中显示的母版页和关联的内容页。 你可以在母版页和内容页中的相应内容控件中查看 ContentPlaceHolder 控件。 请注意，ContentPlaceHolder 外部的母版页内容可见，但在内容页中显示为灰色。 内容页仅可以 supplanted ContentPlaceHolder 内的内容。 来自母版页的所有其他内容都是不可变的。

![母版页及其关联的内容页](master-pages/_static/image1.jpg)

**图 1**：母版页及其关联的内容页

## <a name="creating-a-master-page"></a>创建母版页

若要创建新的母版页：

1. 打开 Visual Studio 2005 并创建新网站。
2. 单击 "文件"、"新建"、"文件"。
3. 从 "添加新项" 对话框中选择 "主文件"，如**图 2**所示。
4. 单击“添加”。

![创建新的母版页](master-pages/_static/image2.jpg)

**图 2**：创建新的母版页

请注意，母版页的文件扩展名为*master*。 这是母版页不同于普通页面的方法之一。 另一个主要区别是，在代替 @Page 指令时，母版页包含 @Master 指令。 切换到刚刚创建的母版页的 "源" 视图，然后查看代码。

默认情况下，新的母版页将具有一个 ContentPlaceHolder 控件。 在大多数情况下，首先创建公共页面元素，然后插入需要自定义内容的 ContentPlaceHolder 控件，这样做会更有意义。 在这些情况下，开发人员需要删除默认的 ContentPlaceHolder 控件并在开发页面时插入新控件。 尽管 ContentPlaceHolder 控件确实显示大小调整控点，但无法调整其大小。 ContentPlaceHolder 控件根据其所包含的内容自动调整大小，但有一个例外;如果将 ContentPlaceHolder 控件放置在块元素（例如表单元）内，则它将根据元素的大小进行调整。

## <a name="lab-1-working-with-master-pages"></a>实验室1使用母版页

在此实验室中，您将创建一个新的母版页，并定义三个 ContentPlaceHolder 控件。 然后，将创建一个新的内容页并替换至少一个 ContentPlaceHolder 控件中的内容。

1. 创建一个母版页并插入 ContentPlaceHolder 控件。 

    1. 如上所述，创建新的母版页。
    2. 删除默认的 ContentPlaceHolder 控件。
    3. 通过单击控件的灰色上边框来选择 ContentPlaceHolder 控件，然后按键盘上的 DEL 键将其删除。
    4. 使用*标头和端*模板插入新表，如图3所示。 将宽度和高度分别更改为90%，使整个表在设计器中可见。

![](master-pages/_static/image3.jpg)

**图3**

1. 将光标置于表的每个单元格中，并将*valign*属性设置为*top*。
2. 从 "工具箱" 中，将 "ContentPlaceHolder" 控件插入到表的顶部单元格中（标题单元格）。
3. 插入此 ContentPlaceHolder 控件时，你会注意到，行高会占用整个页面，如图4所示。 此时，不要担心这一点。

![空格与 ContentPlaceHolder 位于同一单元中](master-pages/_static/image1.gif)

**图 4**：空白空间与 ContentPlaceHolder 位于同一单元中

1. 将 ContentPlaceHolder 控件放在其他两个单元格中。 插入其他 ContentPlaceHolder 控件后，表单元格的大小应与预期的大小相同。 该页现在应类似于**图 5**所示的页面。

![具有所有 ContentPlaceHolder 控件的主节点。 请注意，标题单元格的单元格高度现在就是](master-pages/_static/image2.gif)

**图 5**：包含所有 ContentPlaceHolder 控件的主节点。 请注意，标题单元格的单元格高度现在就是

1. 在三个 ContentPlaceHolder 控件中的每个控件中输入一些所选文本。
2. 将母版页保存为 exercise1。
3. 创建新的 Web 窗体，并将其与 exercise1 母版页关联。
4. 在 Visual Studio 2005 中选择 "文件"、"新建" 和 "文件"。
5. 在 "添加新项" 对话框中选择 " **Web 窗体**"。
6. 请确保选中 "选择母版页" 复选框，如图6所示。

![添加新的内容页](master-pages/_static/image3.gif)

**图 6**：添加新的内容页

1. 单击“添加”。
2. 在 "选择母版页" 对话框中选择 "exercise1"，如图7所示。
3. 单击 "确定" 以添加新的内容页面。

新的内容页将显示在 Visual Studio 中，其中，母版页上的每个 ContentPlaceHolder 控件都有一个内容控件。 默认情况下，内容控件为空，以便您可以添加自己的内容。 如果希望它们使用母版页上的 ContentPlaceHolder 控件中的内容，只需单击智能标记符号（控件右上角的小黑色箭头），然后从智能标记中选择 "*默认为主控内容*"，如**图 8**所示。 当你执行此操作时，菜单项会更改以*创建自定义内容*。 在该点单击该点将从母版页中删除内容，以便为该特定内容控件定义自定义内容。

![将内容控件设置为默认母版页内容](master-pages/_static/image4.gif)

**图 7**：将内容控件设置为默认为母版页内容

## <a name="connecting-master-page-and-content-pages"></a>连接母版页和内容页

可以通过以下四种不同方式之一配置母版页和内容页之间的关联：

- @Page 指令的<strong>MasterPageFile</strong>特性
- 在代码中设置**MasterPageFile**属性。
- **&lt;页面**在应用程序配置文件（应用程序的根文件夹中的 web.config）&gt;元素
- **&lt;页面&gt;** 子文件夹配置文件中的元素（子文件夹中的 web.config）

## <a name="masterpagefile-attribute"></a>MasterPageFile 特性

使用 MasterPageFile 属性可以轻松地将母版页应用到特定的 ASP.NET 页面。 当您在练习1中选中 "**选择母版页**" 复选框时，也可以使用此方法来应用母版页。

## <a name="setting-pagemasterpagefile-in-code"></a>在代码中设置 MasterPageFile

通过在代码中设置 MasterPageFile 属性，您可以在运行时将特定母版页应用于内容。 当你可能需要根据用户角色或某些其他条件应用特定母版页时，这非常有用。 必须在 PreInit 方法中设置 MasterPageFile 属性。 如果在 PreInit 方法之后设置，则会引发 InvalidOperationException。 在其上设置此属性的页面上，还必须将内容控件作为页面的顶级控件。 否则，在设置 MasterPageFile 属性时，将引发 HttpException。

## <a name="using-the-ltpagesgt-element"></a>使用 &lt;pages&gt; 元素

通过在 web.config 文件的 &lt;pages&gt; 元素中设置 masterPageFile 属性，可以为页面配置母版页。 使用此方法时，请记住，在应用程序结构中较低的 web.config 文件可以重写此设置。 @Page 指令中设置的任何 MasterPageFile 属性还将重写此设置。 通过使用 &lt;pages&gt; 元素，可以轻松创建在特定文件夹或文件中需要重写的*主*母版页。

## <a name="properties-in-master-pages"></a>母版页中的属性

母版页只需在母版页内使这些属性公开即可公开属性。 例如，下面的代码定义了一个名为 SomeProperty 的属性：

[!code-csharp[Main](master-pages/samples/sample2.cs)]

若要从 "内容" 页访问 SomeProperty 属性，需要使用 Master 属性，如下所示：

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>嵌套母版页

母版页是确保大型 Web 应用程序的常见外观的理想解决方案。 但是，在某些情况下，大型站点的某些部分共享公共接口并不常见，而其他部分则共享不同的接口。 为了满足这种需要，多个母版页是最佳解决方案。 但是，这仍不能解决这样一种情况：大型应用程序可能有某些组件（例如菜单）在所有页面和其他仅在站点的特定部分中共享的组件之间共享。 对于这种情况，嵌套的母版页非常适合需要。 正如您所看到的，普通的母版页包含一个母版页和一个内容页面。 在嵌套的母版页情况下，有两个母版页;父主机和子主节点。 子母版页也是内容页，其母版页是父级母版页。

下面是典型母版页的代码：

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

在嵌套的主方案中，这将是父主节点。 另一个母版页将使用此页作为其母版页，代码如下所示：

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

请注意，在这种情况下，子主节点也是父主节点的内容页。 所有子母版页的内容都显示在内容控件中，该控件从父级的 ContentPlaceHolder 控件获取其内容。

> [!NOTE]
> 设计器支持不可用于嵌套母版页。 使用嵌套母版进行开发时，需要使用源视图。

此视频演示如何使用嵌套母版页。

![](master-pages/_static/image1.png)

[打开全屏视频](master-pages/_static/nested1.wmv)

![选择母版页](master-pages/_static/image4.jpg)

**图 8**：选择母版页
