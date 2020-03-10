---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: 如何实现使用 HTML 编辑器控件吗？ (C#) | Microsoft Docs
author: microsoft
description: HTMLEditor 是一个 ASP.NET AJAX 控件，可用于通过工具栏中的按钮轻松创建和编辑 HTML 内容。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: cb7d75b59b1361abeb6d3c38ad6e42e34d6e3f7b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78466604"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a>如何实现使用 HTML 编辑器控件吗？ (C#)

由[Microsoft](https://github.com/microsoft)

> HTMLEditor 是一个 ASP.NET AJAX 控件，可用于通过工具栏中的按钮轻松创建和编辑 HTML 内容。

本教程的目的是提供 AJAX 控件工具包中包含的 HTML 编辑器控件的概述。 HTML 编辑器包含用于更改字体大小、选择字体、更改背景色、修改前景颜色、添加链接、添加图像、更改文本对齐方式和执行剪切、复制和粘贴操作的选项（请参阅图1）。

[![HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)

**图 01**： HTML 编辑器（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-cs/_static/image2.png)）

使用 HTML 编辑器，您可以使用设计模式输入内容，也可以直接输入 HTML。 还提供了用于预览 HTML 内容的选项（参见图2）。

[![设计、HTML 和预览按钮](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)

**图 02**：设计、HTML 和预览按钮（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-cs/_static/image4.png)）

在本教程中，您将学习如何显示 HTML 编辑器、如何自定义出现在 HTML 编辑器中的工具栏按钮，以及如何避免跨站点脚本攻击。

## <a name="displaying-the-html-editor"></a>显示 HTML 编辑器

在 ASP.NET 页中使用 HTML 编辑器之前，必须先将 ScriptManager 控件添加到该页。 ScriptManager 控件位于 Visual Studio/Visual Web Developer Express 工具箱中的 "AJAX 扩展" 选项卡下。

应将 ScriptManager 控件置于页面顶部，然后再放置页面上的任何其他控件。 例如，你可以将其放在打开的服务器端 &lt;窗体的紧下方&gt; 标记。

HTML 编辑器控件位于工具箱中，其中包含其他 AJAX 控件工具包控件。 它名为编辑器控件（参见图3）。

[![HTML 编辑器控件](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)

**图 03**： HTML 编辑器控件（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-cs/_static/image6.png)）

将 HTML 编辑器拖到页面上之后，可以在属性表中设置其属性。 例如，通常需要设置 "宽度" 和 "高度" 属性。 列表1包含包含 HTML 编辑器的 ASP.NET 页面的源。

**列表 1-SimpleEditor .aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

列表1中的页包含 HTML 编辑器控件、按钮控件和文本控件。 单击该按钮时，HTML 编辑器的内容将显示在文字控件中（见图4）。

[![使用 HTML 编辑器提交窗体](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)

**图 04**：使用 HTML 编辑器提交窗体（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-cs/_static/image8.png)）

"HTML 编辑器内容" 属性用于检索输入到 HTML 编辑器中的 HTML 内容。 请注意，此 HTML 内容可以包含 JavaScript。 在下一部分中，我们将讨论如何防止 JavaScript 注入攻击。

## <a name="customizing-the-html-editor-toolbar"></a>自定义 HTML 编辑器工具栏

您可以自定义在编辑器中显示的确切按钮。 例如，你可能想要删除 HTML 选项卡，以防止用户将 HTML 编辑器切换为 HTML 模式。 或者，您可能想要删除字体大小下拉列表，以防止用户在论坛消息文章中创建过大的文本（请参阅图5）。

[![自定义的 HTML 编辑器](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)

**图 05**：自定义的 HTML 编辑器（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-cs/_static/image10.png)）

您可以通过从基编辑器类中派生新的 HTML 编辑器来自定义工具栏按钮。 例如，"列表 2" 中的自定义编辑器仅包含粗体和斜体的工具栏按钮。 所有其他工具栏按钮均已删除。 此外，"HTML" 选项卡已从编辑器底部删除（但 "设计" 和 "预览" 选项卡仍然存在）。

**列出 2-应用\_Code\CustomEditor.cs**

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

必须将清单2中的类添加到应用\_代码文件夹，以便自动编译该类。 如果您的网站中不存在应用程序\_代码文件夹，则只需添加文件夹即可。

创建自定义编辑器后，可以将其添加到 "ASP.NET" 页，其方式与添加普通 HTML 编辑器的方式相同（请参阅列表3）。

**列表 3-ShowCustomEditor**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>避免跨站点脚本（XSS）攻击

每当你接受来自用户的输入并在你的网站上重新显示该输入时，可能会将你的网站打开到跨站点脚本（XSS）攻击。 理论上，恶意黑客可能会提交在重新显示输入时执行的 JavaScript 代码。 JavaScript 可用于窃取用户密码或其他敏感信息。

通常情况下，你可以通过 HTML 编码使 XSS 攻击在显示在网页中之前从用户那里检索到的任何输入。 但 HTML 编码 HTML 编辑器的输出不仅 &lt;脚本&gt; 标记编码，还会对所有 HTML 标记进行编码。 换句话说，您将丢失所有格式设置，如字体类型、字号和背景色。

如果要从用户收集敏感信息（如密码、信用卡号和社会安全号码），则不应显示使用 HTML 编辑器从用户那里检索到的未编码内容。 仅在不重新出现 HTML 内容或 HTML 内容正在由受信任方提交到您的网站时，才应使用 HTML 编辑器。

例如，假设你要创建一个博客应用程序。 在这种情况下，在撰写博客文章时使用 HTML 编辑器是有意义的。 你是提交博客文章的唯一人员，因此你可以信任自己来不提交恶意 JavaScript。 但是，在允许匿名用户发布注释时，使用 HTML 编辑器是没有意义的。 在用户提交敏感信息（如密码）的情况下，应特别小心。 恶意用户可能会发布包含正确 JavaScript 的注释来窃取密码。

## <a name="summary"></a>摘要

在本教程中，我们提供了包含在 AJAX 控件工具包中的 HTML 编辑器控件的简要概述。 您学习了如何使用 HTML 编辑器接受来自用户的丰富内容并将内容提交给服务器。 还介绍了如何自定义 HTML 编辑器显示的工具栏按钮。 最后，你已了解如何在使用 HTML 编辑器接受潜在的恶意输入时避免跨站点脚本攻击。

> [!div class="step-by-step"]
> [下一部分](how-do-i-use-the-html-editor-control-vb.md)
