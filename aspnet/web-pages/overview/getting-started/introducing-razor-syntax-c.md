---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: 使用 Razor 语法的 ASP.NET Web 编程简介（C#） |Microsoft Docs
author: Rick-Anderson
description: 本章提供使用 Razor 语法对 ASP.NET 网页进行编程的概述。 ASP.NET 是 Microsoft 用于运行动态 web pa 的技术 。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564876"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a>使用 Razor 语法的 ASP.NET Web 编程简介（C#）

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文提供使用 Razor 语法对 ASP.NET 网页进行编程的概述。 ASP.NET 是 Microsoft 在 web 服务器上运行动态网页的技术。 本文重点介绍如何使用C#编程语言。
> 
> **你将学习的内容**：
> 
> - 使用 Razor 语法编程 ASP.NET 网页入门的前8个编程提示。
> - 需要的基本编程概念。
> - 什么是 ASP.NET 服务器代码和 Razor 语法都是如此。
>   
> 
> ## <a name="software-versions"></a>软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

## <a name="the-top-8-programming-tips"></a>前8个编程提示

本部分列出了开始使用 Razor 语法编写 ASP.NET 服务器代码时需要了解的一些提示。

> [!NOTE]
> Razor 语法基于C#编程语言，这是 ASP.NET 网页最常使用的语言。 但 Razor 语法还支持 Visual Basic 语言，你所看到的所有内容也可以在 Visual Basic 中执行。 有关详细信息，请参阅附录[Visual Basic 语言和语法](https://go.microsoft.com/fwlink/?LinkId=202908)。

可在本文后面的部分中找到有关这些编程技术的更多详细信息。

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. 使用 @ 字符将代码添加到页面

`@` 字符将启动内联表达式、单语句块和多语句块：

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

当页面在浏览器中运行时，这些语句如下所示：

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 编码**
> 
> 如前面的示例中所示，使用 `@` 字符显示页面中的内容时，ASP.NET 对输出进行 HTML 编码。 这会将保留 HTML 字符（如 `<` 和 `>` 和 `&`）替换为代码，使字符在网页中显示为字符，而不是解释为 HTML 标记或实体。 如果没有 HTML 编码，服务器代码的输出可能无法正确显示，并且可能会使页面面临安全风险。
> 
> 如果你的目标是输出 HTML 标记，该标记将标记呈现为标记（例如，为段落 `<p></p>` 或 `<em></em>` 强调文本），请参阅本文后面的在[代码块中组合文本、标记和代码](#BM_CombiningTextMarkupAndCode)部分。
> 
> 有关 HTML 编码的详细信息，请参阅[使用窗体](https://go.microsoft.com/fwlink/?LinkId=202892)。

### <a name="2-you-enclose-code-blocks-in-braces"></a>2. 将代码块括在大括号中

*代码块*包含一个或多个代码语句，并括在大括号中。

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

浏览器中显示的结果：

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a>3. 在块中，用分号结束每个代码语句

在代码块中，每个完整的代码语句必须以分号结束。 内联表达式不以分号结束。

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a>4. 使用变量存储值

可以将值存储在*变量*中，包括字符串、数字和日期等。使用 `var` 关键字创建新变量。 您可以使用 `@`直接在页面中插入变量值。

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

浏览器中显示的结果：

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. 将文字字符串值用双引号引起来

*字符串*是被视为文本的字符序列。 若要指定字符串，请用双引号将其引起来：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

如果要显示的字符串包含反斜杠字符（`\`）或双引号（`"`），请使用以 `@` 运算符为前缀的*原义字符串文本*。 （在C#中，除非使用原义字符串文本，否则，\ 字符具有特殊意义。）

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

若要嵌入双引号，请使用原义字符串并重复引号：

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

下面是在页面中使用这两个示例的结果：

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> 请注意，`@` 字符用于标记和中C#的原义字符串文本，以在 ASP.NET 页中标记代码。

### <a name="6-code-is-case-sensitive"></a>6. 代码区分大小写

在C#中，关键字（如 `var`、`true`和 `if`）和变量名称区分大小写。 以下代码行创建两个不同的变量，`lastName` 和 `LastName.`

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

如果将变量声明为 `var lastName = "Smith";`，并尝试在页中将该变量作为 `@LastName`进行引用，则会 `"Jones"` 而不是 `"Smith"`来获取值。

> [!NOTE]
> 在 Visual Basic 中，关键字和变量*不*区分大小写。

### <a name="7-much-of-your-coding-involves-objects"></a>7. 您的大部分编码都涉及对象

*对象*表示您可以使用&#8212;页面、文本框、文件、图像、web 请求、电子邮件、客户记录（数据库行）等进行编程的内容。对象具有描述其特性的属性，并且您可以读取或更改&#8212;文本框对象具有 `Text` 属性（其他），请求对象具有 `Url` 属性，电子邮件具有 `From` 属性，而 customer 对象具有 `FirstName` 属性。 对象还具有可执行&quot; &quot;谓词的方法。 示例包括文件对象的 `Save` 方法、图像对象的 `Rotate` 方法和电子邮件对象的 `Send` 方法。

你通常会使用 `Request` 对象，该对象提供的信息类似于页面上文本框（窗体字段）的值、发出请求的浏览器的类型、页面的 URL、用户标识等。下面的示例演示如何访问 `Request` 对象的属性，以及如何调用 `Request` 对象的 `MapPath` 方法，这为你提供了服务器上页面的绝对路径：

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

浏览器中显示的结果：

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 您可以编写代码来做出决策

动态网页的一项重要功能是，你可以根据条件确定要执行的操作。 要执行此操作，最常见的方法是用 `if` 语句（和可选的 `else` 语句）。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

语句 `if(IsPost)` 是编写 `if(IsPost == true)`的一种简便方法。 除了 `if` 语句，还可以使用多种方法来测试条件、重复的代码块等，本文稍后将对此进行介绍。

在浏览器中显示的结果（在单击 "**提交**" 后）：

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a>HTTP GET 和 POST 方法和 IsPost 属性
> 
> 用于 web pages （HTTP）的协议支持用于向服务器发出请求的有限数量的方法（谓词）。 最常见的两个是 GET，用于读取页面，使用 POST 来提交页面。 通常，当用户第一次请求页面时，将使用 GET 请求页面。 如果用户填写表单，然后单击 "提交" 按钮，则浏览器向服务器发出 POST 请求。
> 
> 在 web 编程中，很有必要了解页面是否作为 GET 或 POST 请求，以便您知道如何处理页面。 在 ASP.NET 网页中，可以使用 `IsPost` 属性来查看请求是 GET 还是 POST。 如果请求是 POST，则 `IsPost` 属性将返回 true，您可以执行一些操作，例如读取窗体上的文本框的值。 你将看到的许多示例演示了如何根据 `IsPost`的值不同地处理页。

## <a name="a-simple-code-example"></a>简单的代码示例

此过程说明如何创建一个说明基本编程技术的页面。 在此示例中，您将创建一个允许用户输入两个数字的页面，然后将其添加并显示结果。

1. 在编辑器中，创建一个新文件并将其命名为*AddNumbers*。
2. 将以下代码和标记复制到页面中，替换页面中已有的任何内容。  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    下面是要注意的一些事项：

    - `@` 字符将启动页面中的第一个代码块，并在嵌入到页面底部的 `totalMessage` 变量之前。
    - 页面顶部的块括在大括号中。
    - 在顶部的块中，所有行都以分号结束。
    - 变量 `total`、`num1`、`num2`和 `totalMessage` 存储几个数字和一个字符串。
    - 赋给 `totalMessage` 变量的文字字符串值用双引号引起来。
    - 由于代码区分大小写，因此，当在页面底部附近使用 `totalMessage` 变量时，其名称必须完全匹配顶部的变量。
    - 表达式 `num1.AsInt() + num2.AsInt()` 演示如何使用对象和方法。 每个变量的 `AsInt` 方法将用户输入的字符串转换为数字（整数），以便您可以对其执行算术运算。
    - `<form>` 标记包含 `method="post"` 特性。 这指定在用户单击 "**添加**" 时，将使用 HTTP POST 方法将页发送到服务器。 提交页面后，`if(IsPost)` 测试的计算结果为 true，并且运行条件代码，并显示添加数字的结果。
3. 保存页面并在浏览器中运行它。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）输入两个整数，然后单击 "**添加**" 按钮。 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a>基本编程概念

本文提供 ASP.NET web 编程的概述。 这并不是一种全面的调查，只是通过最常使用的编程概念的简要教程。 尽管如此，它还涵盖了开始 ASP.NET 网页所需的几乎所有内容。

但首先，这是一个很小的技术背景。

### <a name="the-razor-syntax-server-code-and-aspnet"></a>Razor 语法、服务器代码和 ASP.NET

Razor 语法是一种简单的编程语法，用于在网页中嵌入基于服务器的代码。 在使用 Razor 语法的网页中，有两种内容：客户端内容和服务器代码。 客户端内容是您在网页中使用的内容： HTML 标记（元素）、样式信息（如 CSS）或某些客户端脚本（如 JavaScript）和纯文本。

Razor 语法允许你将服务器代码添加到此客户端内容。 如果页中有服务器代码，则服务器会在将页发送到浏览器之前先运行该代码。 通过在服务器上运行，代码可以执行可能更复杂的任务，而不是使用客户端内容，如访问基于服务器的数据库。 最重要的是，服务器代码可以动态创建&#8212;客户端内容，它可以动态生成 HTML 标记或其他内容，然后将其连同页面可能包含的任何静态 HTML 一起发送到浏览器。 从浏览器的角度来看，服务器代码生成的客户端内容与任何其他客户端内容没有什么不同。 正如您所看到的，所需的服务器代码非常简单。

包含 Razor 语法的 ASP.NET 网页具有特殊的文件扩展名（*cshtml*或*vbhtml*）。 服务器可识别这些扩展，运行 Razor 语法标记的代码，然后将该页发送到浏览器。

### <a name="where-does-aspnet-fit-in"></a>ASP.NET 适用于何处？

Razor 语法基于 Microsoft 中称为 ASP.NET 的技术，后者又基于 Microsoft .NET 框架。 The.NET 框架是 Microsoft 提供的一个大型综合性编程框架，用于开发几乎任何类型的计算机应用程序。 ASP.NET 是专门为创建 web 应用程序而设计的 .NET Framework 部分。 开发人员使用 ASP.NET 在世界各地创建了许多最大和最高的流量网站。 （只要你在站点中的 URL 中看到文件扩展名 *.aspx* ，你就会知道该站点是使用 ASP.NET 编写的。）

Razor 语法提供了 ASP.NET 的全部功能，但使用简化的语法，可以更方便地了解你是否是初级用户，如果你是一位专家，这会使你的工作效率更高。 尽管该语法很简单，但它与 ASP.NET 的系列关系 .NET Framework 也是如此，这意味着当您的网站变得更加复杂时，您可以使用更大的框架。

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> **类和实例**
> 
> ASP.NET 服务器代码使用对象，这些对象又基于类的概念而构建。 类是对象的定义或模板。 例如，应用程序可能包含一个 `Customer` 类，该类定义任何客户对象所需的属性和方法。
> 
> 当应用程序需要使用实际的客户信息时，它将创建一个客户对象的实例（或实例*化*）。 每个客户都是 `Customer` 类的单独实例。 每个实例都支持相同的属性和方法，但每个实例的属性值通常是不同的，因为每个客户对象都是唯一的。 在一个客户对象中，`LastName` 属性可能为 "Smith";在另一个客户对象中，`LastName` 属性可能为 ""。
> 
> 同样，您站点中的任何单个网页都是 `Page` 对象，它是 `Page` 类的实例。 页面上的按钮是 `Button` 对象，它是 `Button` 类的实例等。 每个实例都有其自身的特征，但它们都基于对象的类定义中指定的内容。

## <a name="basic-syntax"></a>基本语法

前面部分介绍了如何创建 ASP.NET 网页页，以及如何将服务器代码添加到 HTML 标记的基本示例。 在这里，你将学习使用 Razor 语法&#8212; （即编程语言规则）编写 ASP.NET 服务器代码的基础知识。

如果你使用的是编程（尤其是在使用 C、 C++、 C#、Visual Basic 或 JavaScript）的情况下，你将会熟悉此处所述的大部分内容。 您可能只需要熟悉如何将服务器代码添加到*cshtml*文件中的标记。

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a>在代码块中组合文本、标记和代码

在服务器代码块中，通常需要将文本或标记（或两者）输出到页面。 如果服务器代码块包含不是代码的文本，而应按原样呈现，则 ASP.NET 需要能够区分该文本与代码。 有若干方法可实现此操作。

- 将文本括在 HTML 元素中，如 `<p></p>` 或 `<em></em>`：   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    HTML 元素可以包括文本、附加 HTML 元素和服务器代码表达式。 当 ASP.NET 查看开始 HTML 标记（例如 `<p>`）时，它会将所有内容（包括元素）和其内容呈现为浏览器，并在服务器代码表达式发生时进行解析。
- 使用 `@:` 运算符或 `<text>` 元素。 `@:` 输出包含纯文本或不匹配 HTML 标记的单个行内容;`<text>` 元素包含多个要输出的行。 如果您不希望在输出过程中呈现 HTML 元素，则这些选项非常有用。  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    如果要输出多行文本或不匹配的 HTML 标记，则可以在每行的前面加 `@:`，也可以在 `<text>` 元素中包含行。 与 `@:` 运算符一样，ASP.NET 使用`<text>` 标记来标识文本内容，而不会在页输出中呈现。

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    第一个示例重复前面的示例，但使用一对 `<text>` 标记来包含要呈现的文本。 在第二个示例中，"`<text>`" 和 "`</text>`" 标记包含三行，其中所有行都包含一些非包含文本和匹配的 HTML 标记（`<br />`）以及服务器代码和匹配的 HTML 标记。 同样，您还可以在每行的前面加上 `@:` 运算符;这两种方法都适用。

    > [!NOTE]
    > 使用 HTML 元素输出此部分&#8212;中所示的文本时，`@:` 运算符或 `<text>` 元素&#8212; ASP.NET 不会对输出进行 HTML 编码。 （如前文所述，ASP.NET 会对前面是 `@`的服务器代码表达式和服务器代码块的输出进行编码，但本部分中所述的特殊情况除外。

### <a name="whitespace"></a>Whitespace

语句中的多余空格（字符串文字外）不会影响语句：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

语句中的换行符对语句没有影响，您可以包装语句以便于阅读。 下列语句相同：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

但是，不能在字符串文字的中间换行。 下面的示例不起作用：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

若要将换行的长字符串与以上代码中的多个行合并，有两个选项。 可以使用串联运算符（`+`），稍后将在本文中看到。 你还可以使用 `@` 字符创建原义字符串，如本文前面所述。 可以跨行中断原义字符串文本：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a>代码（和标记）注释

您可以为自己或其他人留言。 它们还允许您禁用（*注释掉*）您不想运行但要在页面中保留的代码或标记的部分。

Razor 代码和 HTML 标记有不同的注释语法。 与所有 Razor 代码一样，在将页发送到浏览器之前，将在服务器上处理并删除 Razor 注释。 因此，Razor 注释语法使你可以将注释添加到代码中（甚至是标记中），你可以在编辑文件时查看这些注释，但即使在页面源中也不会看到。

对于 ASP.NET Razor 注释，会开始 `@*` 注释，并通过 `*@`结束。 注释可以在一行或多行上：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

下面是代码块中的注释：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

下面是相同的代码块，代码行已注释掉，因此无法运行：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

在代码块内，作为使用 Razor 注释语法的替代方法，你可以使用所使用的编程语言的注释语法，例如C#：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

在C#中，单行注释前面带有 `//` 字符，多行注释以 `/*` 开头，并以 `*/`结尾。 （与 Razor 注释一样， C#注释不会呈现给浏览器。）

对于标记，你可能知道，可以创建 HTML 注释：

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

HTML 注释从 `<!--` 字符开始，以 `-->`结束。 您可以使用 HTML 注释来包围文本，还可以使用任何 HTML 标记（您可能希望在页面中保留，但不希望呈现）。 此 HTML 注释将隐藏标记的全部内容及其包含的文本：

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

与 Razor 注释不同，HTML*注释呈现*到页面，用户可以通过查看页面源来查看这些注释。

Razor 的嵌套块有限制C#。 有关详细信息[，请C#参阅命名变量和嵌套块生成损坏的代码](http://aspnetwebstack.codeplex.com/workitem/1914)

## <a name="variables"></a>变量

变量是用于存储数据的命名对象。 您可以将变量命名为任何名称，但该名称必须以字母字符开头且不能包含空格或保留字符。

### <a name="variables-and-data-types"></a>变量和数据类型

变量可以具有特定的数据类型，用于指示变量中存储的数据类型。 可以有存储字符串值（如 &quot;Hello world&quot;）的字符串变量、存储整数值的整数变量（例如3或79）以及以多种格式存储日期值的日期变量（如4/12/2012 或3月2009）。 还可以使用许多其他数据类型。

但是，您通常不需要为变量指定类型。 大多数情况下，ASP.NET 可以根据变量中数据的使用方式来确定类型。 （有时您必须指定一个类型，您将看到这样的示例。）

使用 `var` 关键字声明一个变量（如果不希望指定类型）或使用该类型的名称：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

下面的示例演示了网页中变量的一些典型用法：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

如果将前面的示例组合到页面中，则会看到此显示在浏览器中：

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>转换和测试数据类型

尽管 ASP.NET 通常可以自动确定数据类型，但有时不能。 因此，您可能需要通过执行显式转换来帮助 ASP.NET。 即使您不需要转换类型，有时也可以通过测试来查看您可能使用的数据类型。

最常见的情况是必须将字符串转换为其他类型，例如整数或日期。 下面的示例演示一个典型情况，您必须将字符串转换为数字。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

作为一种规则，用户输入作为字符串提供给你。 即使您已提示用户输入一个数字，甚至输入了一个数字，在提交用户输入并在代码中读取它时，数据仍采用字符串格式。 因此，必须将字符串转换为数字。 在此示例中，如果你尝试对值执行算术运算而不转换这些值，则会产生以下错误，因为 ASP.NET 无法添加两个字符串：

*无法将类型 "string" 隐式转换为 "int"。*

若要将值转换为整数，请调用 `AsInt` 方法。 如果转换成功，则可以添加数字。

下表列出了一些常见的变量转换方法和测试方法。

:::row:::
    :::column:::
    <strong>方法</strong>
    :::column-end:::
    :::column:::
    <strong>描述</strong>
    :::column-end:::
    :::column:::
    <strong>示例</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    将表示整数的字符串（如 "593"）转换为整数。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
    将字符串（如 &quot;true&quot; 或 &quot;false&quot; 转换为布尔类型。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
    将具有十进制值（如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字符串转换为浮点数。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
    将具有十进制值（如 &quot;1.3&quot; 或 &quot;7.439&quot; 的字符串转换为十进制数字。 （在 ASP.NET 中，小数比浮点数更精确。）
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
    将表示日期和时间值的字符串转换为 ASP.NET `DateTime` 类型。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
    将任何其他数据类型转换为字符串。
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>运算符

运算符是一个关键字或字符，用于告知 ASP.NET 要在表达式中执行哪种类型的命令。 C#语言（以及基于它的 Razor 语法）支持许多运算符，但你只需要识别几个运算符即可开始使用。 下表总结了最常见的运算符。

:::row:::
    :::column:::
    <strong>Operator</strong>
    :::column-end:::
    :::column:::
    <strong>描述</strong>
    :::column-end:::
    :::column:::
    <strong>示例</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    数值表达式中使用的数学运算符。
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    赋值。 将语句右侧的值分配给左侧的对象。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    相等。 如果值相等，则返回 `true`。 （请注意 `=` 运算符与 `==` 运算符之间的区别。）
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    不相等。 如果值不相等，则返回 `true`。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    小于、大于、小于等于、等于、大于等于或大于或等于。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    串联，用于联接字符串。 ASP.NET 根据表达式的数据类型知道此运算符与加法运算符之间的差异。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
    递增和递减运算符，它们分别增加和减少1。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
    着重号. 用于区分对象及其属性和方法。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    括号. 用于对表达式分组并将参数传递给方法。
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    方括号. 用于访问数组或集合中的值。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    不仅. 反转 `true` 值为 `false`，反之亦然。 通常用作测试 `false` （即，不 `true`）的一种简便方法。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&&` `||`
    :::column-end:::
    :::column:::
    逻辑 "与" 或 "或"，用于将条件链接在一起。
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a>处理代码中的文件和文件夹路径

通常会在代码中使用文件和文件夹路径。 下面是网站的物理文件夹结构示例，因为它可能出现在开发计算机上：

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

下面是有关 Url 和路径的一些基本详细信息：

- URL 以域名（`http://www.example.com`）或服务器名称（`http://localhost`，`http://mycomputer`）开头。
- URL 对应于主计算机上的物理路径。 例如，`http://myserver` 可能对应于服务器上的*C:\websites\mywebsite*文件夹。
- 虚拟路径是在代码中表示路径的速记，无需指定完整路径。 它包括位于域或服务器名称后面的 URL 部分。 使用虚拟路径时，可以将代码移到不同的域或服务器上，而无需更新路径。

下面是一个示例，可帮助你了解不同之处：

| 完成 URL | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| 服务器名称 | *mycompanyserver* |
| 虚拟路径 | */humanresources/CompanyPolicy.htm* |
| 物理路径 | *C:\mywebsites\humanresources\CompanyPolicy.htm* |

虚拟根目录为/，正如 C：驱动器的根目录为 \。 （虚拟文件夹路径始终使用正斜杠。）文件夹的虚拟路径不必与物理文件夹同名;它可以是别名。 （在生产服务器上，虚拟路径很少匹配确切的物理路径。）

当你在代码中处理文件和文件夹时，有时需要引用物理路径，有时还需要引用虚拟路径，具体取决于你使用的对象。 ASP.NET 提供了以下工具来处理代码中的文件和文件夹路径： `Server.MapPath` 方法、`~` 运算符和 `Href` 方法。

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>将虚拟路径转换为物理路径：服务器. MapPath 方法

`Server.MapPath` 方法将虚拟路径（如 */default.cshtml*）转换为绝对物理路径（如*C:\WebSites\MyWebSiteFolder\default.cshtml*）。 任何时候都需要完整的物理路径时，可以使用此方法。 典型的示例是在 web 服务器上读取或写入文本文件或图像文件时。

您通常不知道站点在宿主站点的服务器上的绝对物理路径，因此此方法可以将您知道的路径（虚拟路径）转换为服务器上的相应路径。 将文件或文件夹的虚拟路径传递给方法，并返回物理路径：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>引用虚拟根： ~ operator 和 Href 方法

在*cshtml*或*vbhtml*文件中，可以使用 `~` 运算符引用虚拟根路径。 这非常方便，因为您可以在站点中移动页面，并且任何包含到其他页面的链接都不会损坏。 如果你将网站移到其他位置，也可以方便地使用它。 下面是一些可能的恶意活动：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

如果网站 `http://myserver/myapp`，以下是在页面运行时 ASP.NET 将如何处理这些路径：

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

（实际上，您不会看到这些路径作为变量的值，而 ASP.NET 会将这些路径视为它们。）

可以在服务器代码（如上所示）和标记中使用 `~` 运算符，如下所示：

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

在标记中，使用 `~` 运算符来创建资源的路径，如图像文件、其他网页和 CSS 文件。 当该页运行时，ASP.NET 将浏览该页（代码和标记），并将所有 `~` 引用解析为相应的路径。

## <a name="conditional-logic-and-loops"></a>条件逻辑和循环

通过 ASP.NET 服务器代码，你可以根据条件执行任务，并编写代码，将语句重复指定次数（即运行循环的代码）。

### <a name="testing-conditions"></a>测试条件

若要测试简单的条件，请使用 `if` 语句，该语句根据指定的测试返回 true 或 false：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

`if` 关键字启动块。 实际测试（条件）位于括号中，并返回 true 或 false。 如果测试为 true，则运行的语句括在大括号中。 `if` 语句可以包括指定语句的 `else` 块，条件为 false 时运行：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

您可以使用 `else if` 块添加多个条件：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

在此示例中，如果 if 块中的第一个条件不为 true，则选中 `else if` 条件。 如果满足该条件，则执行 `else if` 块中的语句。 如果未满足任何条件，则执行 `else` 块中的语句。 你可以添加任意数量的 else if block，然后使用 `else` 块关闭，因为 &quot;所有其他&quot; 条件。

若要测试大量条件，请使用 `switch` 块：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

要测试的值位于括号内（在本例中为 `weekday` 变量）。 每个单独的测试都使用以冒号（:) 结尾的 `case` 语句。 如果 `case` 语句的值与测试值匹配，则将执行该 case 块中的代码。 使用 `break` 语句关闭每个 case 语句。 （如果忘记在每个 `case` 块中包含 break，则下一 `case` 语句中的代码也会运行。）`switch` 块通常将 `default` 语句作为 &quot;所有其他情况下运行&quot; 选项的最后一种情况。

在浏览器中显示的最后两个条件块的结果：

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a>循环代码

经常需要重复运行相同的语句。 通过循环执行此操作。 例如，通常对数据集合中的每个项运行相同的语句。 如果确切知道要循环多少次，则可以使用 `for` 循环。 此类循环特别适用于计算或计数：

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

循环以 `for` 关键字开头，后跟括在括号中的三个语句，每个语句用分号结束。

- 在括号内，第一个语句（`var i=10;`）会创建一个计数器，并将其初始化为10。 无需命名计数器 `i` &#8212;可以使用任何变量。 `for` 循环运行时，计数器会自动递增。
- 第二个语句（`i < 21;`）设置要计数的条件。 在这种情况下，你希望其最大值为20（即，在计数器小于21的情况下继续）。
- 第三个语句（`i++`）使用增量运算符，该运算符仅指定在每次循环运行时应将计数器添加1。

大括号内是将为循环的每次迭代运行的代码。 标记每次创建一个新段落（`<p>` 元素），并在输出中添加一行，并显示 `i` （计数器）的值。 运行此页时，此示例将创建11行显示输出，每行中的文本指示项号。

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

如果使用的是集合或数组，通常使用 `foreach` 循环。 集合是一组类似的对象，而 `foreach` 循环使你可以对集合中的每个项执行一个任务。 这种类型的循环非常适合于回收，因为与 `for` 循环不同，您不必递增计数器或设置限制。 相反，`foreach` 循环代码只需经过回收，直到完成。

例如，下面的代码返回 `Request.ServerVariables` 集合中的项，这是一个包含有关 web 服务器的信息的对象。 它通过在 HTML 项目符号列表中创建一个新的 `<li>` 元素，使用 `foreac` h 循环来显示每个项的名称。

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

`foreach` 关键字后跟括号，在此括号中，你可以声明一个表示集合中单个项的变量（在本例中为 `var item`），后跟 `in` 关键字，后跟要循环访问的集合。 在 `foreach` 循环的主体中，可以使用之前声明的变量访问当前项。

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

若要创建更通用的循环，请使用 `while` 语句：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

`while` 循环以 `while` 关键字开头，后跟括号，可在其中指定循环的持续时间（在此之后，只要 `countNum` 小于50），就会重复执行块。 循环通常会递增（添加到）或递减（减去）用于计数的变量或对象。 在此示例中，每次循环运行时，`+=` 运算符都 `countNum` 加1。 （若要减小循环中计算的变量，请使用减量运算符 `-=`）。

## <a name="objects-and-collections"></a>对象和集合

ASP.NET 网站中的几乎所有内容都是一个对象，包括网页本身。 本部分讨论你将经常在代码中使用的一些重要对象。

### <a name="page-objects"></a>页面对象

ASP.NET 中的最基本对象是页面。 您可以直接访问 page 对象的属性，而无需任何合格的对象。 下面的代码使用页面的 `Request` 对象获取页面的文件路径：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

若要清楚地说您在当前 page 对象上引用属性和方法，您可以选择使用关键字 `this` 在代码中表示 page 对象。 下面是上面的代码示例，其中添加了 `this` 以表示页面：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

您可以使用 `Page` 对象的属性来获取很多信息，例如：

- `Request`。 正如您所看到的，这是有关当前请求的信息的集合，包括发出请求的浏览器的类型、页面的 URL、用户标识等。
- `Response`。 这是在服务器代码完成运行时将发送到浏览器的响应（页）信息的集合。 例如，您可以使用此属性将信息写入响应中。 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a>集合对象（数组和字典）

*集合*是一组相同类型的对象，例如来自数据库的 `Customer` 对象的集合。 ASP.NET 包含许多内置集合，如 `Request.Files` 集合。

通常会使用集合中的数据。 两个常见的集合类型是*数组*和*字典*。 如果希望存储类似项的集合，但又不想创建单独的变量来保存每个项，则数组将非常有用：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

使用数组，可以声明特定的数据类型，例如 `string`、`int`或 `DateTime`。 若要指示变量可以包含数组，请在声明中添加方括号（如 `string[]` 或 `int[]`）。 您可以使用其位置（索引）或使用 `foreach` 语句来访问数组中的项。 数组索引从零开始， &#8212;这是，第一个项的位置为0，第二项位于位置1，依此类推。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

可以通过获取数组中的项的 `Length` 属性来确定这些项的数目。 若要获取数组中特定项的位置（以搜索数组），请使用 `Array.IndexOf` 方法。 您还可以执行一些操作，例如反转数组的内容（`Array.Reverse` 方法）或对内容进行排序（`Array.Sort` 方法）。

在浏览器中显示的字符串数组代码的输出：

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

字典是键/值对的集合，其中提供了用于设置或检索相应值的键（或名称）：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

若要创建字典，请使用 `new` 关键字指示正在创建新的字典对象。 可以使用 `var` 关键字为变量分配字典。 使用尖括号（`< >`）指示字典中项的数据类型。 在声明的末尾，必须添加一对括号，因为这实际上是创建新字典的方法。

若要将项添加到字典中，可以调用字典变量的 `Add` 方法（在本例中为`myScores`），然后指定键和值。 或者，您可以使用方括号来指示密钥并执行简单的分配，如下面的示例中所示：

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

若要从字典中获取值，请在括号中指定密钥：

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a>调用带参数的方法

如本文前面所述，使用编写的对象可以有方法。 例如，`Database` 对象可能具有 `Database.Connect` 方法。 许多方法还具有一个或多个参数。 *参数*是传递给方法以使方法完成其任务的值。 例如，查看 `Request.MapPath` 方法的声明，该方法采用三个参数：

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

（此行已换行以使其更具可读性。 请记住，除了用引号引起来的字符串内，您几乎可以在任何位置放置换行符。）

此方法返回与指定虚拟路径相对应的服务器上的物理路径。 方法的三个参数 `virtualPath`、`baseVirtualDir`和 `allowCrossAppMapping`。 （请注意，在声明中，参数与它们将接受的数据的数据类型一起列出。）调用此方法时，必须为所有三个参数提供值。

Razor 语法提供了两个用于将参数传递给方法的选项：*位置参数*和*命名参数*。 若要使用位置参数调用方法，请按方法声明中指定的严格顺序传递参数。 （您通常可以通过阅读该方法的文档来了解此顺序。）必须按照顺序进行操作，如果需要，则不能跳过&#8212;任何参数，而是为没有值的位置参数传递空字符串（`""`）或 `null`。

以下示例假定网站上有一个名为 "*脚本*" 的文件夹。 此代码调用 `Request.MapPath` 方法，并按正确的顺序传递三个参数的值。 然后，它会显示生成的映射路径。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

如果方法具有多个参数，则可以通过使用命名参数使代码更具可读性。 若要使用命名参数调用方法，请指定参数名称后跟冒号（:)，然后输入值。 命名参数的优点是可以按所需的任意顺序传递它们。 （缺点是方法调用并不是压缩方法。）

下面的示例调用与上面相同的方法，但使用命名参数来提供值：

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

正如您所看到的，参数以不同的顺序传递。 但是，如果运行前面的示例和此示例，它们将返回相同的值。

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a>处理错误

### <a name="try-catch-statements"></a>Try-catch 语句

由于控件外的原因，你的代码中经常会出现语句。 例如：

- 如果代码尝试创建或访问文件，则可能会出现各种错误。 你需要的文件可能不存在，可能已被锁定，代码可能没有权限，等等。
- 同样，如果你的代码尝试更新数据库中的记录，则可能存在权限问题，可能会删除与数据库的连接，要保存的数据可能会无效，依此类推。

在编程术语中，这种情况称为 "*异常*"。 如果代码遇到异常，则会生成（引发）一条错误消息，该消息对于用户而言是一种非常令人讨厌的错误消息：

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

在代码可能遇到异常的情况下，若要避免此类型的错误消息，可以使用 `try/catch` 语句。 在 `try` 语句中，运行要检查的代码。 在一个或多个 `catch` 语句中，可以查找可能发生的特定错误（特定类型的异常）。 您可以包含任意数量的 `catch` 语句，以便查找您要预测的错误。

> [!NOTE]
> 建议避免在 `try/catch` 语句中使用 `Response.Redirect` 方法，因为这可能会导致页中出现异常。

下面的示例演示了在第一个请求中创建文本文件的页面，然后显示一个按钮，使用户可以打开该文件。 该示例有意使用错误的文件名，以便它将导致异常。 此代码包含两个可能的异常的 `catch` 语句： `FileNotFoundException`，如果文件名错误 `DirectoryNotFoundException`，则会发生这种情况，在 ASP.NET 甚至不能找到该文件夹时，也会出现这种情况。 （您可以在示例中取消注释语句，以查看它在一切正常工作时的运行情况。）

如果代码未处理异常，则会看到一个错误页，如上一个屏幕截图所示。 但 `try/catch` 部分可帮助防止用户看到这些类型的错误。

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a>其他资源

**用 Visual Basic 进行编程**

[附录： Visual Basic 语言和语法](https://go.microsoft.com/fwlink/?LinkId=202908)

**参考文档**

[ASP.NET 2.0](https://msdn.microsoft.com/library/ee532866.aspx)

[C#语言](https://msdn.microsoft.com/library/kx37x362.aspx)
