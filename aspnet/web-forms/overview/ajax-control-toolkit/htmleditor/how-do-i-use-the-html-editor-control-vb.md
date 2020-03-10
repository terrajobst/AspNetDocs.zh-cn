---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
title: 如何实现使用 HTML 编辑器控件吗？ (VB) | Microsoft Docs
author: microsoft
description: HTMLEditor 是一个 ASP.NET AJAX 控件，可用于通过工具栏中的按钮轻松创建和编辑 HTML 内容。
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 32ec9321-7c8c-4b0f-8234-99acb56df6b5
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 20f8a2f8148bc658370ba1a939ebf1b62d376bc0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446282"
---
# <a name="how-do-i-use-the-html-editor-control-vb"></a><span data-ttu-id="ffa62-104">如何实现使用 HTML 编辑器控件吗？</span><span class="sxs-lookup"><span data-stu-id="ffa62-104">How do I use the HTML Editor Control?</span></span> <span data-ttu-id="ffa62-105">(VB)</span><span class="sxs-lookup"><span data-stu-id="ffa62-105">(VB)</span></span>

<span data-ttu-id="ffa62-106">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="ffa62-106">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="ffa62-107">HTMLEditor 是一个 ASP.NET AJAX 控件，可用于通过工具栏中的按钮轻松创建和编辑 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="ffa62-107">HTMLEditor is an ASP.NET AJAX Control that allows you to easily create and edit HTML content via buttons in a toolbar.</span></span>

<span data-ttu-id="ffa62-108">本教程的目的是提供 AJAX 控件工具包中包含的 HTML 编辑器控件的概述。</span><span class="sxs-lookup"><span data-stu-id="ffa62-108">The goal of this tutorial is to provide you with an overview of the HTML Editor control included with the AJAX Control Toolkit.</span></span> <span data-ttu-id="ffa62-109">HTML 编辑器包含用于更改字体大小、选择字体、更改背景色、修改前景颜色、添加链接、添加图像、更改文本对齐方式和执行剪切、复制和粘贴操作的选项（请参阅图1）。</span><span class="sxs-lookup"><span data-stu-id="ffa62-109">The HTML Editor includes options for changing font size, selecting a font, changing background color, modifying the foreground color, adding links, adding images, changing text alignment, and performing cut, copy, and paste operations (see Figure 1).</span></span>

<span data-ttu-id="ffa62-110">[![HTML 编辑器](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="ffa62-110">[![The HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image1.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image1.png)</span></span>

<span data-ttu-id="ffa62-111">**图 01**： HTML 编辑器（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="ffa62-111">**Figure 01**: The HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image2.png))</span></span>

<span data-ttu-id="ffa62-112">使用 HTML 编辑器，您可以使用设计模式输入内容，也可以直接输入 HTML。</span><span class="sxs-lookup"><span data-stu-id="ffa62-112">The HTML editor enables you to enter content using a design mode or you can enter HTML directly.</span></span> <span data-ttu-id="ffa62-113">还提供了用于预览 HTML 内容的选项（参见图2）。</span><span class="sxs-lookup"><span data-stu-id="ffa62-113">You also are provided with the option to preview your HTML content (see Figure 2).</span></span>

<span data-ttu-id="ffa62-114">[![设计、HTML 和预览按钮](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="ffa62-114">[![Design, HTML, and Preview buttons](how-do-i-use-the-html-editor-control-vb/_static/image2.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image3.png)</span></span>

<span data-ttu-id="ffa62-115">**图 02**：设计、HTML 和预览按钮（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="ffa62-115">**Figure 02**: Design, HTML, and Preview buttons([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image4.png))</span></span>

<span data-ttu-id="ffa62-116">在本教程中，您将学习如何显示 HTML 编辑器、如何自定义出现在 HTML 编辑器中的工具栏按钮，以及如何避免跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="ffa62-116">In this tutorial, you learn how to display the HTML Editor, how to customize the toolbar buttons that appear in the HTML Editor, and how to avoid Cross-Site Scripting Attacks.</span></span>

## <a name="displaying-the-html-editor"></a><span data-ttu-id="ffa62-117">显示 HTML 编辑器</span><span class="sxs-lookup"><span data-stu-id="ffa62-117">Displaying the HTML Editor</span></span>

<span data-ttu-id="ffa62-118">在 ASP.NET 页中使用 HTML 编辑器之前，必须先将 ScriptManager 控件添加到该页。</span><span class="sxs-lookup"><span data-stu-id="ffa62-118">Before you can use the HTML Editor in an ASP.NET page, you must first add a ScriptManager control to the page.</span></span> <span data-ttu-id="ffa62-119">ScriptManager 控件位于 Visual Studio/Visual Web Developer Express 工具箱中的 "AJAX 扩展" 选项卡下。</span><span class="sxs-lookup"><span data-stu-id="ffa62-119">The ScriptManager control is located beneath the AJAX Extensions tab in the Visual Studio/Visual Web Developer Express toolbox.</span></span>

<span data-ttu-id="ffa62-120">应将 ScriptManager 控件置于页面顶部，然后再放置页面上的任何其他控件。</span><span class="sxs-lookup"><span data-stu-id="ffa62-120">You should place the ScriptManager control at the top of the page before any other controls on the page.</span></span> <span data-ttu-id="ffa62-121">例如，你可以将其放在打开的服务器端 &lt;窗体的紧下方&gt; 标记。</span><span class="sxs-lookup"><span data-stu-id="ffa62-121">For example, you can place it immediately below the opening server-side &lt;form&gt; tag.</span></span>

<span data-ttu-id="ffa62-122">HTML 编辑器控件位于工具箱中，其中包含其他 AJAX 控件工具包控件。</span><span class="sxs-lookup"><span data-stu-id="ffa62-122">The HTML Editor control is located in the toolbox with the rest of the AJAX Control Toolkit controls.</span></span> <span data-ttu-id="ffa62-123">它名为编辑器控件（参见图3）。</span><span class="sxs-lookup"><span data-stu-id="ffa62-123">It is named the Editor control (see Figure 3).</span></span>

<span data-ttu-id="ffa62-124">[![HTML 编辑器控件](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="ffa62-124">[![The HTML Editor control](how-do-i-use-the-html-editor-control-vb/_static/image3.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image5.png)</span></span>

<span data-ttu-id="ffa62-125">**图 03**： HTML 编辑器控件（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="ffa62-125">**Figure 03**: The HTML Editor control([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image6.png))</span></span>

<span data-ttu-id="ffa62-126">将 HTML 编辑器拖到页面上之后，可以在属性表中设置其属性。</span><span class="sxs-lookup"><span data-stu-id="ffa62-126">After you drag the HTML Editor onto a page, you can set its properties in the property sheet.</span></span> <span data-ttu-id="ffa62-127">例如，通常需要设置 "宽度" 和 "高度" 属性。</span><span class="sxs-lookup"><span data-stu-id="ffa62-127">For example, you normally want to set the Width and Height properties.</span></span> <span data-ttu-id="ffa62-128">列表1包含包含 HTML 编辑器的 ASP.NET 页面的源。</span><span class="sxs-lookup"><span data-stu-id="ffa62-128">Listing 1 contains the source for an ASP.NET page that contains an HTML editor.</span></span>

<span data-ttu-id="ffa62-129">**列表 1-SimpleEditor .aspx**</span><span class="sxs-lookup"><span data-stu-id="ffa62-129">**Listing 1 - SimpleEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample1.aspx)]

<span data-ttu-id="ffa62-130">列表1中的页包含 HTML 编辑器控件、按钮控件和文本控件。</span><span class="sxs-lookup"><span data-stu-id="ffa62-130">The page in Listing 1 contains an HTML Editor control, a Button control, and a Literal control.</span></span> <span data-ttu-id="ffa62-131">单击该按钮时，HTML 编辑器的内容将显示在文字控件中（见图4）。</span><span class="sxs-lookup"><span data-stu-id="ffa62-131">When you click the button, the contents of the HTML Editor appear in the Literal control (see Figure 4).</span></span>

<span data-ttu-id="ffa62-132">[![使用 HTML 编辑器提交窗体](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="ffa62-132">[![Submitting a form with an HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image4.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image7.png)</span></span>

<span data-ttu-id="ffa62-133">**图 04**：使用 HTML 编辑器提交窗体（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="ffa62-133">**Figure 04**: Submitting a form with an HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image8.png))</span></span>

<span data-ttu-id="ffa62-134">"HTML 编辑器内容" 属性用于检索输入到 HTML 编辑器中的 HTML 内容。</span><span class="sxs-lookup"><span data-stu-id="ffa62-134">The HTML Editor Content property is used to retrieve the HTML content entered into the HTML Editor.</span></span> <span data-ttu-id="ffa62-135">请注意，此 HTML 内容可以包含 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="ffa62-135">Be aware that this HTML content can contain JavaScript.</span></span> <span data-ttu-id="ffa62-136">在下一部分中，我们将讨论如何防止 JavaScript 注入攻击。</span><span class="sxs-lookup"><span data-stu-id="ffa62-136">In the next section, we discuss how you can prevent JavaScript Injection Attacks.</span></span>

## <a name="customizing-the-html-editor-toolbar"></a><span data-ttu-id="ffa62-137">自定义 HTML 编辑器工具栏</span><span class="sxs-lookup"><span data-stu-id="ffa62-137">Customizing the HTML Editor Toolbar</span></span>

<span data-ttu-id="ffa62-138">您可以自定义在编辑器中显示的确切按钮。</span><span class="sxs-lookup"><span data-stu-id="ffa62-138">You can customize exactly which buttons appear in the editor.</span></span> <span data-ttu-id="ffa62-139">例如，你可能想要删除 HTML 选项卡，以防止用户将 HTML 编辑器切换为 HTML 模式。</span><span class="sxs-lookup"><span data-stu-id="ffa62-139">For example, you might want to remove the HTML tab to prevent users from switching the HTML Editor into HTML mode.</span></span> <span data-ttu-id="ffa62-140">或者，您可能想要删除字体大小下拉列表，以防止用户在论坛消息文章中创建过大的文本（请参阅图5）。</span><span class="sxs-lookup"><span data-stu-id="ffa62-140">Or, you might want to remove the font size dropdown list to prevent users from creating overly large text in a forum message post (see Figure 5).</span></span>

<span data-ttu-id="ffa62-141">[![自定义的 HTML 编辑器](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="ffa62-141">[![A customized HTML Editor](how-do-i-use-the-html-editor-control-vb/_static/image5.jpg)](how-do-i-use-the-html-editor-control-vb/_static/image9.png)</span></span>

<span data-ttu-id="ffa62-142">**图 05**：自定义的 HTML 编辑器（[单击以查看完全大小的图像](how-do-i-use-the-html-editor-control-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="ffa62-142">**Figure 05**: A customized HTML Editor([Click to view full-size image](how-do-i-use-the-html-editor-control-vb/_static/image10.png))</span></span>

<span data-ttu-id="ffa62-143">您可以通过从基编辑器类中派生新的 HTML 编辑器来自定义工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="ffa62-143">You customize the toolbar buttons by deriving a new HTML Editor from the base Editor class.</span></span> <span data-ttu-id="ffa62-144">例如，"列表 2" 中的自定义编辑器仅包含粗体和斜体的工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="ffa62-144">For example, the custom editor in Listing 2 only contains toolbar buttons for bold and italic.</span></span> <span data-ttu-id="ffa62-145">所有其他工具栏按钮均已删除。</span><span class="sxs-lookup"><span data-stu-id="ffa62-145">All other toolbar buttons have been removed.</span></span> <span data-ttu-id="ffa62-146">此外，"HTML" 选项卡已从编辑器底部删除（但 "设计" 和 "预览" 选项卡仍然存在）。</span><span class="sxs-lookup"><span data-stu-id="ffa62-146">Furthermore, the HTML tab has been removed from the bottom of the editor (but the Design and Preview tabs are still there).</span></span>

<span data-ttu-id="ffa62-147">**列出 2-应用\_Code\CustomEditor.vb**</span><span class="sxs-lookup"><span data-stu-id="ffa62-147">**Listing 2 - App\_Code\CustomEditor.vb**</span></span>

[!code-vb[Main](how-do-i-use-the-html-editor-control-vb/samples/sample2.vb)]

<span data-ttu-id="ffa62-148">必须将清单2中的类添加到应用\_代码文件夹，以便自动编译该类。</span><span class="sxs-lookup"><span data-stu-id="ffa62-148">You must add the class in Listing 2 to your App\_Code folder so that the class will be compiled automatically.</span></span> <span data-ttu-id="ffa62-149">如果您的网站中不存在应用程序\_代码文件夹，则只需添加文件夹即可。</span><span class="sxs-lookup"><span data-stu-id="ffa62-149">If the App\_Code folder does not exist in your website then you can simply add the folder.</span></span>

<span data-ttu-id="ffa62-150">创建自定义编辑器后，可以将其添加到 "ASP.NET" 页，其方式与添加普通 HTML 编辑器的方式相同（请参阅列表3）。</span><span class="sxs-lookup"><span data-stu-id="ffa62-150">After you create a custom editor, you can add it to an ASP.NET page in the same way as you add the normal HTML Editor (see Listing 3).</span></span>

<span data-ttu-id="ffa62-151">**列表 3-ShowCustomEditor**</span><span class="sxs-lookup"><span data-stu-id="ffa62-151">**Listing 3 - ShowCustomEditor.aspx**</span></span>

[!code-aspx[Main](how-do-i-use-the-html-editor-control-vb/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a><span data-ttu-id="ffa62-152">避免跨站点脚本（XSS）攻击</span><span class="sxs-lookup"><span data-stu-id="ffa62-152">Avoiding Cross-Site Scripting (XSS) Attacks</span></span>

<span data-ttu-id="ffa62-153">每当你接受来自用户的输入并在你的网站上重新显示该输入时，可能会将你的网站打开到跨站点脚本（XSS）攻击。</span><span class="sxs-lookup"><span data-stu-id="ffa62-153">Whenever you accept input from a user, and redisplay that input on your website, you potentially open your website to Cross-Site Scripting (XSS) Attacks.</span></span> <span data-ttu-id="ffa62-154">理论上，恶意黑客可能会提交在重新显示输入时执行的 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="ffa62-154">In theory, a malicious hacker could submit JavaScript code that gets executed when the input is redisplayed.</span></span> <span data-ttu-id="ffa62-155">JavaScript 可用于窃取用户密码或其他敏感信息。</span><span class="sxs-lookup"><span data-stu-id="ffa62-155">The JavaScript could be used to steal user passwords or other sensitive information.</span></span>

<span data-ttu-id="ffa62-156">通常情况下，你可以通过 HTML 编码使 XSS 攻击在显示在网页中之前从用户那里检索到的任何输入。</span><span class="sxs-lookup"><span data-stu-id="ffa62-156">Normally, you can defeat XSS attacks by HTML encoding whatever input you retrieve from a user before displaying it in a web page.</span></span> <span data-ttu-id="ffa62-157">但 HTML 编码 HTML 编辑器的输出不仅 &lt;脚本&gt; 标记编码，还会对所有 HTML 标记进行编码。</span><span class="sxs-lookup"><span data-stu-id="ffa62-157">However, HTML encoding the output of the HTML Editor would not only encode &lt;script&gt; tags, it would also encode all HTML tags.</span></span> <span data-ttu-id="ffa62-158">换句话说，您将丢失所有格式设置，如字体类型、字号和背景色。</span><span class="sxs-lookup"><span data-stu-id="ffa62-158">In other words, you would lose all of the formatting such as the font type, font size, and background color.</span></span>

<span data-ttu-id="ffa62-159">如果要从用户收集敏感信息（如密码、信用卡号和社会安全号码），则不应显示使用 HTML 编辑器从用户那里检索到的未编码内容。</span><span class="sxs-lookup"><span data-stu-id="ffa62-159">If you are collecting sensitive information from your users -- such as passwords, credit-card numbers, and social security numbers - then you should not display un-encoded content that you retrieve from a user with the HTML Editor.</span></span> <span data-ttu-id="ffa62-160">仅在不重新出现 HTML 内容或 HTML 内容正在由受信任方提交到您的网站时，才应使用 HTML 编辑器。</span><span class="sxs-lookup"><span data-stu-id="ffa62-160">You should use the HTML Editor only in situations in which you are not redisplaying the HTML content, or the HTML content is being submitted to your website by a trusted party.</span></span>

<span data-ttu-id="ffa62-161">例如，假设你要创建一个博客应用程序。</span><span class="sxs-lookup"><span data-stu-id="ffa62-161">Imagine, for example, that you are creating a blog application.</span></span> <span data-ttu-id="ffa62-162">在这种情况下，在撰写博客文章时使用 HTML 编辑器是有意义的。</span><span class="sxs-lookup"><span data-stu-id="ffa62-162">In this situation, it makes sense to use the HTML Editor when composing blog posts.</span></span> <span data-ttu-id="ffa62-163">你是提交博客文章的唯一人员，因此你可以信任自己来不提交恶意 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="ffa62-163">You are the only one who submits a blog post and, presumably, you can trust yourself not to submit malicious JavaScript.</span></span> <span data-ttu-id="ffa62-164">但是，在允许匿名用户发布注释时，使用 HTML 编辑器是没有意义的。</span><span class="sxs-lookup"><span data-stu-id="ffa62-164">However, it does not make sense to use the HTML Editor when allowing anonymous users to post comments.</span></span> <span data-ttu-id="ffa62-165">在用户提交敏感信息（如密码）的情况下，应特别小心。</span><span class="sxs-lookup"><span data-stu-id="ffa62-165">You should be especially careful in situations in which users submit sensitive information such as passwords.</span></span> <span data-ttu-id="ffa62-166">恶意用户可能会发布包含正确 JavaScript 的注释来窃取密码。</span><span class="sxs-lookup"><span data-stu-id="ffa62-166">Potentially, a malicious user could post a comment that contains the right JavaScript for stealing a password.</span></span>

## <a name="summary"></a><span data-ttu-id="ffa62-167">摘要</span><span class="sxs-lookup"><span data-stu-id="ffa62-167">Summary</span></span>

<span data-ttu-id="ffa62-168">在本教程中，我们提供了包含在 AJAX 控件工具包中的 HTML 编辑器控件的简要概述。</span><span class="sxs-lookup"><span data-stu-id="ffa62-168">In this tutorial, you were provided with a brief overview of the HTML Editor control included in the AJAX Control Toolkit.</span></span> <span data-ttu-id="ffa62-169">您学习了如何使用 HTML 编辑器接受来自用户的丰富内容并将内容提交给服务器。</span><span class="sxs-lookup"><span data-stu-id="ffa62-169">You learned how to use the HTML Editor to accept rich content from a user and submit the content to the server.</span></span> <span data-ttu-id="ffa62-170">还介绍了如何自定义 HTML 编辑器显示的工具栏按钮。</span><span class="sxs-lookup"><span data-stu-id="ffa62-170">We also discussed how you can customize the toolbar buttons that are displayed by the HTML Editor.</span></span> <span data-ttu-id="ffa62-171">最后，你已了解如何在使用 HTML 编辑器接受潜在的恶意输入时避免跨站点脚本攻击。</span><span class="sxs-lookup"><span data-stu-id="ffa62-171">Finally, you learned how to avoid Cross-Site Scripting Attacks when using the HTML Editor to accept potentially malicious input.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ffa62-172">上一页</span><span class="sxs-lookup"><span data-stu-id="ffa62-172">Previous</span></span>](how-do-i-use-the-html-editor-control-cs.md)
