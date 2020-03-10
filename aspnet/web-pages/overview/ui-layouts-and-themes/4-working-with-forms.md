---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: 在 ASP.NET 网页（Razor）站点中使用 HTML 窗体 |Microsoft Docs
author: Rick-Anderson
description: 窗体是 HTML 文档的一个部分，您可以在其中放置用户输入控件（如文本框、复选框、单选按钮和下拉列表）。 使用 forms 符合 。
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519602"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a>在 ASP.NET 网页（Razor）站点中使用 HTML 表单

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍当你在 ASP.NET 网页（Razor）网站中工作时如何处理 HTML 窗体（带有文本框和按钮）。
> 
> **你将学习的内容：** 
> 
> - 如何创建 HTML 窗体。
> - 如何读取窗体中的用户输入。
> - 如何验证用户输入。
> - 如何在提交页面后还原表单值。
> 
> 下面是本文中引入的 ASP.NET 编程概念：
> 
> - `Request` 对象。
> - 输入验证。
> - HTML 编码。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

## <a name="creating-a-simple-html-form"></a>创建简单的 HTML 窗体

1. 创建新网站。
2. 在根文件夹中，创建一个名为 "*窗体*" 的网页，然后输入以下标记：

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. 在浏览器中启动页面。 （在 WebMatrix 中，在 "**文件**" 工作区中，右键单击该文件，然后选择 "**在浏览器中启动**"。）将显示一个简单的窗体，其中包含三个输入字段和一个**提交**按钮。

    ![带有三个文本框的窗体的屏幕截图。](4-working-with-forms/_static/image1.png)

    此时，如果单击 "**提交**" 按钮，则不会执行任何操作。 若要使窗体有用，必须添加一些将在服务器上运行的代码。

## <a name="reading-user-input-from-the-form"></a>从窗体读取用户输入

若要处理窗体，请添加代码，用于读取已提交的字段值并对其执行操作。 此过程说明如何读取字段并在页面上显示用户输入。 （在生产应用程序中，你通常会对用户输入执行更有趣的操作。 你将在有关使用数据库的文章中完成此操作。）

1. 在 "# *.* #" 文件的顶部，输入以下代码：

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    当用户首次请求页面时，只显示空窗体。 用户（将是你）将填写表单，然后单击 "**提交**"。 这会将用户输入提交（发布）到服务器。 默认情况下，该请求将进入同一页（即，*窗体.* #）。

    此时，在您提交该页时，您输入的值将显示在窗体的上方：

    ![屏幕截图，显示你在页面上显示的输入值。](4-working-with-forms/_static/image2.png)

    查看页面的代码。 首先使用 `IsPost` 方法来确定页面是否正在发布&#8212; ，即用户是否单击 "**提交**" 按钮。 如果这是 post，`IsPost` 返回 true。 这是 ASP.NET 网页确定使用的是初始请求（GET 请求）还是回发（POST 请求）的标准方法。 （有关 GET 和 POST 的详细信息，请参阅[使用 Razor 语法 ASP.NET 网页编程简介](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)中的边栏 "HTTP GET 和 Post 和 IsPost 属性"。）

    接下来，从 `Request.Form` 对象获取用户填写的值，并将其放在变量中供以后查看。 `Request.Form` 对象包含通过页提交的所有值，每个值都由一个键标识。 该键等效于要读取的窗体字段的 `name` 属性。 例如，若要读取 `companyname` 字段（文本框），请使用 `Request.Form["companyname"]`。

    表单值作为字符串存储在 `Request.Form` 对象中。 因此，当您必须使用值作为数字、日期或其他类型的值时，必须将其从字符串转换为该类型。 在此示例中，`Request.Form` 的 `AsInt` 方法用于将 employees 字段（包含雇员计数）的值转换为整数。
2. 在浏览器中启动页面，填写表单域，并单击 "**提交**"。 页面将显示您输入的值。

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a>外观和安全性的 HTML 编码
> 
> HTML 对 `<`、`>`和 `&`等字符具有特殊用途。 如果这些特殊字符出现在不预期的位置，则它们可能会破坏网页的外观和功能。 例如，浏览器将 `<` 字符（除非后跟空格）解释为 HTML 元素的开头，如 `<b>` 或 `<input ...>`。 如果浏览器不能识别元素，则只会丢弃以 `<` 开头的字符串，直到到达它再次识别的内容。 很明显，这可能会导致页面中出现某种奇怪的渲染。
> 
> HTML 编码将这些保留字符替换为浏览器解释为正确符号的代码。 例如，`<` 字符将替换为 `&lt;`，`>` 字符将替换为 `&gt;`。 浏览器将这些替换字符串呈现为你要查看的字符。
> 
> 在显示从用户那里获得的字符串（输入）时，最好使用 HTML 编码。 如果不这样做，用户可以尝试让您的网页运行恶意脚本，或执行其他影响您的站点安全的操作，或者不是您所期望的内容。 （如果您采用用户输入，将其存储在其他位置，然后在以后&#8212;显示（例如，作为博客注释、用户评论或类似的内容），这一点特别重要。
> 
> 为了帮助防止这些问题，ASP.NET 网页自动对您从代码中输出的任何文本内容进行 HTML 编码。 例如，当使用代码（如 `@MyVar`）显示变量或表达式的内容时，ASP.NET 网页会自动对输出进行编码。

## <a name="validating-user-input"></a>验证用户输入

用户出错。 要求用户填写某个字段，并将其忽略，或者要求他们输入雇员数量并改为键入名称。 若要确保窗体在处理之前已正确填充，需验证用户的输入。

此过程说明如何验证所有三个窗体字段，以确保用户不将其留空。 还应检查员工计数值是否为数字。 如果有错误，将显示一条错误消息，告知用户哪些值未通过验证。

1. 在 "# *" 文件中，将第*一个代码块替换为以下代码： 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    若要验证用户输入，请使用 `Validation` 帮助程序。 可以通过调用 `Validation.RequireField`来注册必填字段。 您可以通过调用 `Validation.Add` 并指定要验证的字段和要执行的验证类型来注册其他类型的验证。

    当页面运行时，ASP.NET 将为你执行所有验证。 您可以通过调用 `Validation.IsValid`来检查结果，如果所有内容均通过验证，则返回 true; 如果任何字段未通过验证，则返回 false。 通常，在对用户输入执行任何处理之前，先调用 `Validation.IsValid`。
2. 通过向 `Html.ValidationMessage` 方法添加三次调用来更新 `<body>` 元素，如下所示：

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    若要显示验证错误消息，可以调用 Html.`ValidationMessage` 并向其传递您需要消息的字段的名称。
3. 运行页面。 将字段留空，然后单击 "**提交**"。 你将看到错误消息。

    ![显示在用户输入未通过验证时显示的错误消息的屏幕截图。](4-working-with-forms/_static/image3.jpg)
4. 将字符串（例如，"ABC"）添加到 "**员工计数**" 字段，然后再次单击 "**提交**"。 此时会出现一个错误，指示该字符串的格式不正确，即整数。

    ![显示在用户为 "员工" 字段输入字符串时显示的错误消息的屏幕截图。](4-working-with-forms/_static/image4.jpg)

ASP.NET 网页提供了用于验证用户输入的更多选项，其中包括使用客户端脚本自动执行验证的功能，以便用户可以在浏览器中获得即时反馈。 有关详细信息，请参阅[其他资源](#Additional_Resources)部分。

## <a name="restoring-form-values-after-postbacks"></a>在回发之后还原窗体值

当你在上一节中测试页面时，你可能已注意到，如果有验证错误，则你输入的所有内容（不只是无效数据）都已消失，你必须为所有字段重新输入值。 这说明了一个重要的要点：提交页面并处理它，然后再次呈现页面时，将从头开始重新创建页面。 正如您所看到的，这意味着页面上提交的任何值都将丢失。

不过，您可以轻松地解决此问题。 你有权访问已提交的值（在 `Request.Form` 对象中），因此，在呈现页面时可以将这些值填充到窗体字段。

1. *在 "#" 文件中*，使用 `value` 属性替换 `<input>` 元素的 `value` 属性。： 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    已将 `<input>` 元素的 `value` 属性设置为从 `Request.Form` 对象动态读取字段值。 第一次请求页面时，`Request.Form` 对象中的值全部为空。 这很好，因为该窗体为空白。
2. 在浏览器中启动页面，填写表单域或将其保留为空，然后单击 "**提交**"。 将显示一页，其中显示了提交的值。

    ![forms 5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>其他资源

- [从 Web 用户获取输入的1001方法](https://msdn.microsoft.com/library/ms971057.aspx)
- [使用窗体和处理用户输入](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)
- [在 ASP.NET 网站中验证用户输入](https://go.microsoft.com/fwlink/?LinkId=253002)
- [使用 HTML 窗体中的自动完成功能](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)
