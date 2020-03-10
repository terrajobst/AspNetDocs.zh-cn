---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: 使用 Razor 语法的 ASP.NET Web 编程简介（Visual Basic） |Microsoft Docs
author: Rick-Anderson
description: 本附录提供使用 Razor 语法 Visual Basic 中使用 ASP.NET 网页进行编程的概述。
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422660"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a>Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)（使用 Razor 语法的 ASP.NET Web 编程简介 (Visual Basic)）

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文提供使用 Razor 语法和 Visual Basic 对 ASP.NET 网页进行编程的概述。 ASP.NET 是 Microsoft 在 web 服务器上运行动态网页的技术。
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

使用 ASP.NET 网页 Razor 语法使用C#的大多数示例。 但 Razor 语法还支持 Visual Basic。 若要在 Visual Basic 中对 ASP.NET 网页进行编程，请创建一个具有 #*扩展名的网页*，然后添加 Visual Basic 代码。 本文概述如何使用 Visual Basic 语言和语法来创建 ASP.NET 网页。

> [!NOTE]
> Microsoft WebMatrix （**面包店**、**照片库**和**入门网站**等）的默认网站模板在和 Visual Basic 版本中C#可用。 你可以将 Visual Basic 模板按 NuGet 包的形式安装。 网站模板安装在网站的根文件夹中，该文件夹位于名为*Microsoft templates*的文件夹中。

## <a name="the-top-8-programming-tips"></a>前8个编程提示

本部分列出了开始使用 Razor 语法编写 ASP.NET 服务器代码时需要了解的一些提示。

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. 使用 @ 字符将代码添加到页面

`@` 字符将启动内联表达式、单语句块和多语句块：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

浏览器中显示的结果：

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 编码**
> 
> 如前面的示例中所示，使用 `@` 字符显示页面中的内容时，ASP.NET 对输出进行 HTML 编码。 这会将保留 HTML 字符（如 `<` 和 `>` 和 `&`）替换为代码，使字符在网页中显示为字符，而不是解释为 HTML 标记或实体。 如果没有 HTML 编码，服务器代码的输出可能无法正确显示，并且可能会使页面面临安全风险。
> 
> 如果你的目标是输出 HTML 标记，该标记将标记呈现为标记（例如，为段落 `<p></p>` 或 `<em></em>` 强调文本），请参阅本文后面的在[代码块中组合文本、标记和代码](#BM_CombiningTextMarkupAndCode)部分。
> 
> 有关 HTML 编码的详细信息，请参阅在[ASP.NET 网页网站中使用 Html 表单](https://go.microsoft.com/fwlink/?LinkId=202892)。

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a>2. 将代码块括在代码 .。。结束代码

代码块包含一个或多个代码语句，并以关键字 `Code` 和 `End Code`括起来。 将左 `Code` 关键字紧靠在 `@` 字符&#8212;后，它们之间不能有空格。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

浏览器中显示的结果：

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a>3. 在块中，用换行符结束每个代码语句

在 Visual Basic 代码块中，每个语句以换行符结尾。 （稍后在本文中，你将看到一种方法，以便在需要时将长代码语句包装到多行中。）

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a>4. 使用变量存储值

可以将值存储在*变量*中，包括字符串、数字和日期等。使用 `Dim` 关键字创建新变量。 您可以使用 `@`直接在页面中插入变量值。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

浏览器中显示的结果：

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. 将文字字符串值用双引号引起来

*字符串*是被视为文本的字符序列。 若要指定字符串，请用双引号将其引起来：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

若要在字符串值中嵌入双引号，请插入两个双引号字符。 如果希望双引号字符在页面输出中出现一次，则在带引号的字符串中输入它作为 `""`; 如果要显示两次，请在引号内的字符串中输入 `""""`。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

浏览器中显示的结果：

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a>6. Visual Basic 代码不区分大小写

Visual Basic 语言不区分大小写。 可以在任何情况下编写编程关键字（如 `Dim`、`If`和 `True`）和变量名称（如 `myString`或 `subTotal`）。

以下代码行使用小写名称将值分配给变量 `lastname`，然后使用大写名称将变量值输出到页面。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

浏览器中显示的结果：

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a>7. 您的大部分编码都涉及处理对象

对象表示您可以使用&#8212;页面、文本框、文件、图像、web 请求、电子邮件、客户记录（数据库行）等进行编程的内容。对象具有描述其特性&#8212;的属性：文本框对象具有 `Text` 属性，请求对象具有 `Url` 属性，电子邮件具有 `From` 属性，而 customer 对象具有 `FirstName` 属性。 对象还具有可执行&quot; &quot;谓词的方法。 示例包括文件对象的 `Save` 方法、图像对象的 `Rotate` 方法和电子邮件对象的 `Send` 方法。

你通常会使用 `Request` 对象，该对象提供有关页面上的窗体字段的值（文本框等）、发出请求的浏览器的类型、页面的 URL、用户标识等。此示例演示如何访问 `Request` 对象的属性，以及如何调用 `Request` 对象的 `MapPath` 方法，这为你提供了服务器上页面的绝对路径：

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

浏览器中显示的结果：

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 您可以编写代码来做出决策

动态网页的一项重要功能是，你可以根据条件确定要执行的操作。 要执行此操作，最常见的方法是用 `If` 语句（和可选的 `Else` 语句）。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

语句 `If IsPost` 是编写 `If IsPost = True`的一种简便方法。 除了 `If` 语句，还可以使用多种方法来测试条件、重复的代码块等，本文稍后将对此进行介绍。

在浏览器中显示的结果（在单击 "**提交**" 后）：

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **HTTP GET 和 POST 方法和 IsPost 属性**
> 
> 用于 web pages （HTTP）的协议支持用于向服务器发出请求的有限数量的方法（&quot;谓词&quot;）。 最常见的两个是 GET，用于读取页面，使用 POST 来提交页面。 通常，当用户第一次请求页面时，将使用 GET 请求页面。 如果用户填写表单，然后单击 "**提交**"，则浏览器向服务器发出 POST 请求。
> 
> 在 web 编程中，很有必要了解页面是否作为 GET 或 POST 请求，以便您知道如何处理页面。 在 ASP.NET 网页中，可以使用 `IsPost` 属性来查看请求是 GET 还是 POST。 如果请求是 POST，则 `IsPost` 属性将返回 true，您可以执行一些操作，例如读取窗体上的文本框的值。 你将看到的许多示例演示了如何根据 `IsPost`的值不同地处理页。

## <a name="a-simple-code-example"></a>简单的代码示例

此过程说明如何创建一个说明基本编程技术的页面。 在此示例中，您将创建一个允许用户输入两个数字的页面，然后将其添加并显示结果。

1. 在编辑器中，创建一个新文件并将其命名为*AddNumbers*。
2. 将以下代码和标记复制到页面中，替换页面中已有的任何内容。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    下面是要注意的一些事项：

    - `@` 字符将启动页面中的第一个代码块，并将其置于底部嵌入的 `totalMessage` 变量之前。
    - 页面顶部的块括在 `Code...End Code`中。
    - 变量 `total`、`num1`、`num2`和 `totalMessage` 存储几个数字和一个字符串。
    - 赋给 `totalMessage` 变量的文字字符串值用双引号引起来。
    - 由于 Visual Basic 代码不区分大小写，因此当在页面底部附近使用 `totalMessage` 变量时，其名称只需要与页面顶部的变量声明的拼写匹配。 大小写并不重要。
    - 表达式 `num1.AsInt()` + `num2.AsInt()` 演示了如何使用对象和方法。 每个变量的 `AsInt` 方法将用户输入的字符串转换为可添加的整数（整数）。
    - `<form>` 标记包含 `method="post"` 特性。 这指定在用户单击 "**添加**" 时，将使用 HTTP POST 方法将页发送到服务器。 提交页面后，代码 `If IsPost` 的计算结果为 true，并且运行条件代码，显示添加数字的结果。
3. 保存页面并在浏览器中运行它。 （请确保在运行之前在 "**文件**" 工作区中选择了该页面。）输入两个整数，然后单击 "**添加**" 按钮。

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a>Visual Basic 语言和语法

前面部分介绍了如何创建 ASP.NET 网页，以及如何将服务器代码添加到 HTML 标记的基本示例。 在这里，你将了解有关使用 Visual Basic 编写 ASP.NET 服务器代码的基础知识， &#8212;该 Razor 语法是编程语言规则。

如果你使用的是编程（尤其是在使用 C、 C++、 C#、Visual Basic 或 JavaScript）的情况下，你将会熟悉此处所述的大部分内容。 您可能只需要熟悉如何将 WebMatrix 代码添加到*vbhtml*文件中的标记。

### <a id="BM_CombiningTextMarkupAndCode"></a>在代码块中组合文本、标记和代码

在服务器代码块中，通常需要将文本和标记输出到页面。 如果服务器代码块包含不是代码的文本，而应按原样呈现，则 ASP.NET 需要能够区分该文本与代码。 有多种方法可实现此目的。

- 将文本括在 HTML 块元素中，如 `<p></p>` 或 `<em></em>`：

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    HTML 元素可以包括文本、附加 HTML 元素和服务器代码表达式。 当 ASP.NET 查看开始 HTML 标记（例如 `<p>`）时，它会将元素及其内容的所有内容呈现为浏览器（并解析服务器代码表达式）。

- 使用 `@:` 运算符或 `<text>` 元素。 `@:` 输出包含纯文本或不匹配 HTML 标记的单个行内容;`<text>` 元素包含多个要输出的行。 如果您不希望在输出过程中呈现 HTML 元素，则这些选项非常有用。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    下面的示例重复前面的示例，但使用一对 `<text>` 标记来包含要呈现的文本。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    在下面的示例中，"`<text>`" 和 "`</text>`" 标记包含三行，其中所有行都包含一些非包含文本和匹配的 HTML 标记（`<br />`）以及服务器代码和匹配的 HTML 标记。 同样，您还可以在每行的前面加上 `@:` 运算符;这两种方法都适用。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > 使用 HTML 元素输出此部分&#8212;中所示的文本时，`@:` 运算符或 `<text>` 元素&#8212; ASP.NET 不会对输出进行 HTML 编码。 （如前文所述，ASP.NET 会对前面是 `@`的服务器代码表达式和服务器代码块的输出进行编码，但本部分中所述的特殊情况除外。

### <a name="whitespace"></a>Whitespace

语句中的多余空格（字符串文字外）不会影响语句：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a>将长语句分解为多行

您可以在每个代码行后使用下划线字符 `_` （在 Visual Basic 中称为*继续*符），将长代码语句分解为多行。 若要将某个语句分解到下一行，请在该行的末尾添加一个空格，然后添加继续符。 继续执行下一行中的语句。 您可以根据需要将语句换行，以提高可读性。 下列语句相同：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

但是，不能在字符串文字的中间换行。 下面的示例不起作用：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

若要将换行的长字符串与以上代码一起使用，需要使用*串联运算符*（`&`），稍后将在本文中看到。

### <a name="code-comments"></a>代码注释

您可以为自己或其他人留言。 Razor 语法注释以 `@*` 为前缀，以 `*@`结尾。

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

在代码块中，你可以使用 Razor 语法注释，也可以使用普通的 Visual Basic 注释字符，这是每一行都作为前缀的单引号（`'`）。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a>变量

变量是用于存储数据的命名对象。 您可以将变量命名为任何名称，但该名称必须以字母字符开头且不能包含空格或保留字符。 在 Visual Basic 中，如前文所述，变量名称中字母的大小写并不重要。

### <a name="variables-and-data-types"></a>变量和数据类型

变量可以具有特定的数据类型，用于指示变量中存储的数据类型。 可以有存储字符串值（如 &quot;Hello world&quot;）的字符串变量、存储整数值的整数变量（例如3或79）以及以多种格式存储日期值的日期变量（如4/12/2012 或3月2009）。 还可以使用许多其他数据类型。

但是，您不必为变量指定类型。 在大多数情况下，ASP.NET 可以根据变量中的数据的使用方式判断出类型。 （有时您必须指定一个类型，您将看到这样的示例。）

若要在不指定类型的情况下声明变量，请使用 `Dim` 加变量名（例如，`Dim myVar`）。 若要声明类型为的变量，请使用 `Dim` 和变量名称，然后使用 `As` 和类型名称（例如，`Dim myVar As String`）。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

下面的示例演示一些使用网页中的变量的内联表达式。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

浏览器中显示的结果：

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>转换和测试数据类型

尽管 ASP.NET 通常可以自动确定数据类型，但有时不能。 因此，您可能需要通过执行显式转换来帮助 ASP.NET。 即使您不需要转换类型，有时也可以通过测试来查看您可能使用的数据类型。

最常见的情况是必须将字符串转换为其他类型，例如整数或日期。 下面的示例演示一个典型情况，您必须将字符串转换为数字。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

作为一种规则，用户输入作为字符串提供给你。 即使您已提示用户输入一个数字，甚至输入了一个数字，在提交用户输入并在代码中读取它时，数据仍采用字符串格式。 因此，必须将字符串转换为数字。 在此示例中，如果你尝试对值执行算术运算而不转换这些值，则会产生以下错误，因为 ASP.NET 无法添加两个字符串：

`Cannot implicitly convert type 'string' to 'int'.`

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
        将表示整数（如 &quot;593&quot;）的字符串转换为整数。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>运算符

运算符是一个关键字或字符，用于告知 ASP.NET 要在表达式中执行哪种类型的命令。 Visual Basic 支持许多运算符，但你只需要识别一些操作即可开始开发 ASP.NET 网页。 下表总结了最常见的运算符。

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
        `+ - * /`
    :::column-end:::
    :::column:::
        数值表达式中使用的数学运算符。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        赋值和相等。 根据上下文，可以将语句右侧的值分配给左侧的对象，也可以检查值是否相等。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        不相等。 如果值不相等，则返回 `True`。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        小于、大于、小于等于、大于或等于。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        串联，用于联接字符串。
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        递增和递减运算符，它们分别增加和减少1。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
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
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        括号. 用于对表达式进行分组、将参数传递给方法，以及访问数组和集合的成员。
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        不仅. 反转 true 值为 false，反之亦然。 通常用作测试 `False` （即，不 `True`）的一种简便方法。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        逻辑 "与" 或 "或"，用于将条件链接在一起。
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

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

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>引用虚拟根： ~ operator 和 Href 方法

在*cshtml*或*vbhtml*文件中，可以使用 `~` 运算符引用虚拟根路径。 这非常方便，因为您可以在站点中移动页面，并且任何包含到其他页面的链接都不会损坏。 如果你将网站移到其他位置，也可以方便地使用它。 下面是一些可能的恶意活动：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

如果网站 `http://myserver/myapp`，以下是在页面运行时 ASP.NET 将如何处理这些路径：

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

（实际上，您不会看到这些路径作为变量的值，而 ASP.NET 会将这些路径视为它们。）

可以在服务器代码（如上所示）和标记中使用 `~` 运算符，如下所示：

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

在标记中，使用 `~` 运算符来创建资源的路径，如图像文件、其他网页和 CSS 文件。 当该页运行时，ASP.NET 将浏览该页（代码和标记），并将所有 `~` 引用解析为相应的路径。

## <a name="conditional-logic-and-loops"></a>条件逻辑和循环

通过 ASP.NET 服务器代码，你可以根据条件执行任务，并编写代码，将语句重复指定次数（即运行循环的代码）。

### <a name="testing-conditions"></a>测试条件

若要测试简单的条件，请使用 `If...Then` 语句，该语句根据指定的测试返回 `True` 或 `False`：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

`If` 关键字启动块。 实际测试（条件）遵循 `If` 关键字，并返回 true 或 false。 `If` 语句以 `Then`结束。 如果测试为 true，则将运行的语句由 `If` 和 `End If`括起来。 `If` 语句可以包括指定语句的 `Else` 块，条件为 false 时运行：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

如果 `If` 语句启动一个代码块，则无需使用 normal `Code...End Code` 语句来包含这些块。 你只需将 `@` 添加到块中，它将正常工作。 此方法适用于 `If` 和后面跟有代码块的其他 Visual Basic 编程关键字，包括 `For`、`For Each`、`Do While`等。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

可以使用一个或多个 `ElseIf` 块添加多个条件：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

在此示例中，如果 `If` 块中的第一个条件不为 true，则检查 `ElseIf` 条件。 如果满足该条件，则执行 `ElseIf` 块中的语句。 如果未满足任何条件，则执行 `Else` 块中的语句。 你可以添加任意数量的 `ElseIf` 块，然后使用 `Else` 块作为 &quot;所有其他&quot; 条件来结束。

若要测试大量条件，请使用 `Select Case` 块：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

要测试的值位于括号内（在本示例中为 weekday 变量）。 每个单独的测试都使用 `Case` 语句来列出某个值。 如果 `Case` 语句的值与测试值匹配，则将执行该 `Case` 块中的代码。

在浏览器中显示的最后两个条件块的结果：

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a>循环代码

经常需要重复运行相同的语句。 通过循环执行此操作。 例如，通常对数据集合中的每个项运行相同的语句。 如果确切知道要循环多少次，则可以使用 `For` 循环。 此类循环特别适用于计算或计数：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

循环以 `For` 关键字开头，后跟三个元素：

- 紧跟在 `For` 语句之后，可以声明一个计数器变量（不必使用 `Dim`），然后指示范围，如 `i = 10 to 20`中所示。 这意味着变量 `i` 将开始计数为10，并继续，直到达到20（含）。
- `For` 和 `Next` 语句之间是块的内容。 这可以包含一个或多个在每个循环中执行的代码语句。
- `Next i` 语句结束循环。 它会递增计数器并启动循环的下一次迭代。

`For` 和 `Next` 行之间的代码行包含为每个循环迭代运行的代码。 标记每次创建一个新段落（`<p>` 元素）并向输出添加一行，并显示 i （计数器）的值。 运行此页时，此示例将创建11行显示输出，每行中的文本指示项号。

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

如果使用的是集合或数组，通常使用 `For Each` 循环。 集合是一组类似的对象，而 `For Each` 循环使你可以对集合中的每个项执行一个任务。 这种类型的循环非常适合于回收，因为与 `For` 循环不同，您不必递增计数器或设置限制。 相反，`For Each` 循环代码只需经过回收，直到完成。

此示例返回 `Request.ServerVariables` 集合中的项（包含有关 web 服务器的信息）。 它通过在 HTML 项目符号列表中创建新的 `<li>` 元素，使用 `For Each` 循环来显示每个项的名称。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

`For Each` 关键字后跟一个变量，该变量表示集合中的单个项（在本例中为 `myItem`），后跟 `In` 关键字，后跟要循环访问的集合。 在 `For Each` 循环的主体中，可以使用之前声明的变量访问当前项。

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

若要创建更通用的循环，请使用 `Do While` 语句：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

此循环以 `Do While` 关键字开头，后跟一个条件，然后是要重复的块。 循环通常会递增（添加到）或递减（减去）用于计数的变量或对象。 在此示例中，每次循环运行时，`+=` 运算符都向变量的值加1。 （若要减小循环中计算的变量，请使用减量运算符 `-=`。）

## <a name="objects-and-collections"></a>对象和集合

ASP.NET 网站中的几乎所有内容都是一个对象，包括网页本身。 本部分讨论你将经常在代码中使用的一些重要对象。

### <a name="page-objects"></a>页面对象

ASP.NET 中的最基本对象是页面。 您可以直接访问 page 对象的属性，而无需任何合格的对象。 下面的代码使用页面的 `Request` 对象获取页面的文件路径：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

您可以使用 `Page` 对象的属性来获取很多信息，例如：

- `Request`。 正如您所看到的，这是有关当前请求的信息的集合，包括发出请求的浏览器的类型、页面的 URL、用户标识等。
- `Response`。 这是在服务器代码完成运行时将发送到浏览器的响应（页）信息的集合。 例如，您可以使用此属性将信息写入响应中。

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a>集合对象（数组和字典）

集合是一组相同类型的对象，例如来自数据库的 `Customer` 对象的集合。 ASP.NET 包含许多内置集合，如 `Request.Files` 集合。

通常会使用集合中的数据。 两个常见的集合类型是*数组*和*字典*。 如果希望存储类似项的集合，但又不想创建单独的变量来保存每个项，则数组将非常有用：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

使用数组，可以声明特定的数据类型，例如 `String`、`Integer`或 `DateTime`。 若要指示变量可以包含数组，请在声明中向变量名称添加括号（如 `Dim myVar() As String`）。 您可以使用其位置（索引）或使用 `For Each` 语句来访问数组中的项。 数组索引从零开始， &#8212;这是，第一个项的位置为0，第二项位于位置1，依此类推。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

可以通过获取数组中的项的 `Length` 属性来确定这些项的数目。 若要获取数组中特定项的位置（即，若要搜索数组），请使用 `Array.IndexOf` 方法。 您还可以执行一些操作，例如反转数组的内容（`Array.Reverse` 方法）或对内容进行排序（`Array.Sort` 方法）。

在浏览器中显示的字符串数组代码的输出：

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

字典是键/值对的集合，其中提供了用于设置或检索相应值的键（或名称）：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

若要创建字典，请使用 `New` 关键字指示正在创建新的 `Dictionary` 对象。 可以使用 `Dim` 关键字为变量分配字典。 使用括号（`( )`）指示字典中项的数据类型。 在声明的末尾，你必须添加另一对括号，因为这实际上是创建新字典的方法。

若要将项添加到字典中，可以调用字典变量的 `Add` 方法（在本例中为`myScores`），然后指定键和值。 或者，您可以使用括号来指示密钥并执行简单的分配，如以下示例中所示：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

若要从字典中获取值，请在括号中指定密钥：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a>调用带参数的方法

正如您在本文前面所看到的那样，使用进行编程的对象具有方法。 例如，`Database` 对象可能具有 `Database.Connect` 方法。 许多方法还具有一个或多个参数。 *参数*是传递给方法以使方法完成其任务的值。 例如，查看 `Request.MapPath` 方法的声明，该方法采用三个参数：

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

此方法返回与指定虚拟路径相对应的服务器上的物理路径。 方法的三个参数 `virtualPath`、`baseVirtualDir`和 `allowCrossAppMapping`。 （请注意，在声明中，参数与它们将接受的数据的数据类型一起列出。）调用此方法时，必须为所有三个参数提供值。

使用 Razor 语法的 Visual Basic 时，有两个选项可用于将参数传递给方法：*位置参数*或*命名参数*。 若要使用位置参数调用方法，请按方法声明中指定的严格顺序传递参数。 （您通常可以通过阅读该方法的文档来了解此顺序。）必须按照顺序进行操作，如果必要，则不能跳过&#8212;任何参数，对于没有值的位置参数，可以传递空字符串（`""`）或 null。

以下示例假定网站上有一个名为 "*脚本*" 的文件夹。 此代码调用 `Request.MapPath` 方法，并按正确的顺序传递三个参数的值。 然后，它会显示生成的映射路径。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

如果有多个参数用于方法，则可以通过使用命名参数来使代码更简洁、更具可读性。 若要使用命名参数调用方法，请指定参数名称后接 `:=`，然后提供值。 命名参数的优点是可以按所需的任意顺序添加它们。 （缺点是方法调用并不是压缩方法。）

下面的示例调用与上面相同的方法，但使用命名参数来提供值：

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

正如您所看到的，参数以不同的顺序传递。 但是，如果运行前面的示例和此示例，它们将返回相同的值。

## <a name="handling-errors"></a>处理错误

### <a name="try-catch-statements"></a>Try-catch 语句

由于控件外的原因，你的代码中经常会出现语句。 例如:

- 如果你的代码尝试打开、创建、读取或写入文件，则可能会出现各种错误。 你需要的文件可能不存在，可能已被锁定，代码可能没有权限，等等。
- 同样，如果你的代码尝试更新数据库中的记录，则可能存在权限问题，可能会删除与数据库的连接，要保存的数据可能会无效，依此类推。

在编程术语中，这种情况称为 "*异常*"。 如果你的代码遇到异常，则会生成（引发）一条错误消息，该消息对用户而言是一种非常令人讨厌的错误消息。

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

在代码可能遇到异常的情况下，若要避免此类型的错误消息，可以使用 `Try/Catch` 语句。 在 `Try` 语句中，运行要检查的代码。 在一个或多个 `Catch` 语句中，可以查找可能发生的特定错误（特定类型的异常）。 您可以包含任意数量的 `Catch` 语句，以便查找您要预测的错误。

> [!NOTE]
> 建议避免在 `Try/Catch` 语句中使用 `Response.Redirect` 方法，因为这可能会导致页中出现异常。

下面的示例演示了在第一个请求中创建文本文件的页面，然后显示一个按钮，使用户可以打开该文件。 该示例有意使用错误的文件名，以便它将导致异常。 此代码包含两个可能的异常的 `Catch` 语句： `FileNotFoundException`，如果文件名错误 `DirectoryNotFoundException`，则会发生这种情况，在 ASP.NET 甚至不能找到该文件夹时，也会出现这种情况。 （您可以在示例中取消注释语句，以查看它在一切正常工作时的运行情况。）

如果代码未处理异常，则会看到一个错误页，如上一个屏幕截图所示。 但 `Try/Catch` 部分可帮助防止用户看到这些类型的错误。

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a>其他资源

### <a name="reference-documentation"></a>参考文档

- [ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)
- [Visual Basic 语言](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
