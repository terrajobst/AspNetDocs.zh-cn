---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: 调试 ASP.NET 网页（Razor）站点简介 |Microsoft Docs
author: Rick-Anderson
description: 调试是在代码页中查找和修复错误的过程。 本章介绍了一些可用于调试和分析的工具和技术 。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: ae7d871e56326610c043dc20fe6e0919e1b4ac89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506456"
---
# <a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a>调试 ASP.NET 网页（Razor）站点简介

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍了在 ASP.NET 网页（Razor）网站中调试页面的各种方式。 调试是在代码页中查找和修复错误的过程。
>
> **你将学习的内容：**
>
> - 如何显示帮助分析和调试页面的信息。
> - 如何在 Visual Studio 中使用调试工具。
>
>
> 下面是本文中介绍的 ASP.NET 功能：
>
> - `ServerInfo` 帮助程序。
> - `ObjectInfo` 帮助程序。
>
>
> ## <a name="software-versions"></a>软件版本
>
>
> - ASP.NET 网页（Razor）3
> - Visual Studio 2013
>
>
> 本教程还适用于 ASP.NET 网页2。 可以使用 WebMatrix 3，但不支持集成调试器。

解决代码中的错误和问题的一个重要方面是，首先要避免这些错误。 可以通过将可能导致错误的代码部分放入 `try/catch` 块来实现此目的。 有关详细信息，请参阅[使用 Razor 语法对 ASP.NET Web 编程的介绍](https://go.microsoft.com/fwlink/?LinkId=202890)中有关处理错误的部分。

`ServerInfo` 帮助器是一个诊断工具，可提供有关承载页面的 web 服务器环境的信息。 它还显示了当浏览器请求页面时发送的 HTTP 请求信息。 `ServerInfo` 帮助程序显示当前用户标识、发出请求的浏览器的类型，等等。 此类信息可帮助你解决常见问题。

1. 创建名为*ServerInfo*的新网页。
2. 在页面末尾，紧靠在结束 `</body>` 标记之前，添加 `@ServerInfo.GetHtml()`：

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    可以将 `ServerInfo` 代码添加到页面中的任意位置。 但在结尾处添加它会使其输出与其他页面内容分离，使其更易于阅读。

    > [!NOTE]
    >
    > **重要提示**在将网页移动到生产服务器之前，应该从网页中删除任何诊断代码。 这适用于 `ServerInfo` 帮助程序以及本文中涉及将代码添加到页面的其他诊断技术。 您不希望您的网站访问者查看有关您的服务器名称、用户名、服务器上的路径和类似详细信息的信息，因为这种类型的信息可能对具有恶意行为的用户非常有用。
3. 保存页面并在浏览器中运行它。

    ![调试-1](introduction-to-debugging/_static/image1.jpg)

    `ServerInfo` 帮助程序在页面中显示四个信息表：

   - 服务器配置。 本部分提供有关托管 web 服务器的信息，包括计算机名称、正在运行的 ASP.NET 的版本、域名和服务器时间。
   - ASP.NET 服务器变量。 本部分提供有关多个 HTTP 协议的详细信息（称为 HTTP 变量）和每个网页请求中包含的值的详细信息。
   - HTTP 运行时信息。 本部分提供有关在其下运行网页的 Microsoft .NET 框架的版本、路径、有关缓存的详细信息等的详细信息。 （正如您在[使用 Razor 语法的 ASP.NET Web 编程](https://go.microsoft.com/fwlink/?LinkId=202890)中所学到的那样，使用 Razor 语法的 ASP.NET 网页是在 Microsoft 的 ASP.NET web 服务器技术的基础上构建的，它本身构建于一个称为 .NET Framework 的广泛软件开发库之上。）
   - 环境变量。 本部分提供了 web 服务器上所有本地环境变量及其值的列表。

     所有服务器和请求信息的完整说明超出了本文的范围，但你可以看到 `ServerInfo` 帮助程序返回了大量诊断信息。 有关 `ServerInfo` 返回的值的详细信息，请参阅 MSDN 网站上的 Microsoft TechNet 网站和[IIS 服务器变量](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)上[可识别的环境变量](https://technet.microsoft.com/library/dd560744(WS.10).aspx)。

## <a name="embedding-output-expressions-to-display-page-values"></a>嵌入用于显示页面值的输出表达式

查看代码中发生的情况的另一种方法是在页中嵌入输出表达式。 如您所知，可以通过将 `@myVariable` 或 `@(subTotal * 12)` 等内容添加到页面，直接输出变量的值。 对于调试，可以在代码中的战略点放置这些输出表达式。 这使您可以在页面运行时查看关键变量的值或计算的结果。 完成调试后，可以删除表达式或将其注释掉。此过程说明了使用嵌入表达式来帮助调试页的典型方法。

1. 创建名为*OutputExpression*的新 WebMatrix 页面。
2. 将页面内容替换为以下内容：

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    该示例使用 `switch` 语句来检查 `weekday` 变量的值，然后根据它的星期几显示不同的输出消息。 在此示例中，第一个代码块中的 `if` 块会通过将一天添加到当前工作日值来随意更改一周中的某一天。 这是出于说明目的导致的错误。
3. 保存页面并在浏览器中运行它。

    该页显示一周中错误日期的消息。 无论当天的哪一天，你都可以在一天后看到消息。 尽管在此情况下，你知道消息处于关闭状态的原因（因为代码特意设置了不正确的日期值），但在这种情况下，通常很难知道代码中发生错误的位置。 若要进行调试，需要了解关键对象和变量（如 `weekday`）的值发生了什么情况。
4. 通过插入 `@weekday` 来添加输出表达式，如代码中的注释所示。 这些输出表达式会在代码执行中显示变量的值。

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. 保存并在浏览器中运行页面。

    该页首先显示一周中的某一天，然后是从第一天开始得到的更新日期，然后是从 `switch` 语句产生的消息。 由于未向输出添加任何 HTML `<p>` 标记，因此两个变量表达式（`@weekday`）的输出在不同的日期之间没有空格。表达式仅用于测试。

    ![调试-2](introduction-to-debugging/_static/image2.jpg)

    现在，你可以看到错误的位置。 在代码中首次显示 `weekday` 变量时，它将显示正确的日期。 当第二次显示时，在代码中 `if` 块后，一天将关闭。 因此，您知道 weekday 变量的第一个和第二个外观之间发生了某些情况。 如果这是一个真实 bug，这种方法可帮助您缩小引起问题的代码的位置。
6. 通过删除添加的两个输出表达式，并删除更改周中某天的代码，修复页面中的代码。 其余的完整代码块如下例所示：

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. 在浏览器中运行页。 此时会看到显示的消息的正确消息。

## <a name="using-the-objectinfo-helper-to-display-object-values"></a>使用 ObjectInfo 帮助器显示对象值

`ObjectInfo` 帮助程序显示您传递给它的每个对象的类型和值。 您可以使用它查看代码中变量和对象的值（与上一示例中的输出表达式一样），还可以看到有关对象的数据类型信息。

1. 打开前面创建的名为*OutputExpression*的文件。
2. 将页面中的所有代码替换为以下代码块：

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. 保存并在浏览器中运行页面。

    ![调试-4](introduction-to-debugging/_static/image3.jpg)

    在此示例中，`ObjectInfo` 帮助程序显示两个项：

   - 类型。 对于第一个变量，类型为 `DayOfWeek`。 对于第二个变量，类型为 `String`。
   - 值。 在这种情况下，由于您已经在页面中显示了问候语变量的值，因此当您将该变量传递给 `ObjectInfo`时，将再次显示此值。

     对于更复杂的对象，`ObjectInfo` 帮助器&#8212;基本上可以显示更多信息，它可以显示对象的所有属性的类型和值。

## <a name="using-debugging-tools-in-visual-studio"></a>在 Visual Studio 中使用调试工具

若要获得更全面的调试体验，请使用[Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。 使用 Visual Studio，可以在代码中要检查的行处设置断点。

![设置断点](introduction-to-debugging/_static/image1.png)

测试网站时，执行代码将在断点处暂停。

![到达断点](introduction-to-debugging/_static/image2.png)

你可以检查变量的当前值，并逐行执行代码。

![查看值](introduction-to-debugging/_static/image3.png)

有关使用 Visual Studio 中的集成调试器调试 ASP.NET Razor 页面的信息，请参阅[使用 Visual studio 进行编程 ASP.NET 网页（Razor）](https://go.microsoft.com/fwlink/?LinkId=205854)。

## <a name="additional-resources"></a>其他资源

- [使用 Visual Studio 的编程 ASP.NET 网页（Razor）](https://go.microsoft.com/fwlink/?LinkId=205854)
- [IIS 服务器变量](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)（MSDN）
- [识别的环境变量](https://technet.microsoft.com/library/dd560744(WS.10).aspx)（TechNet）
