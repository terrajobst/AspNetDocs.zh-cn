---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: ASP.NET 错误处理 |Microsoft Docs
author: Erikre
description: 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为我们 Microsoft Visual Studio Express 2013 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: 9514142ca50b33470a3f4c033e4f8e319a9ee09b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636460"
---
# <a name="aspnet-error-handling"></a>ASP.NET 错误处理

作者： [Erik Reitan](https://github.com/Erikre)

[下载 Wingtip 玩具示例项目（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下载电子书（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 本系列教程将介绍使用 ASP.NET 4.5 构建 ASP.NET Web 窗体应用程序的基础知识，并为 Web Microsoft Visual Studio Express 2013。 此教程系列附带有[ C#源代码](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 项目。

在本教程中，您将修改 Wingtip 玩具示例应用程序以包括错误处理和错误日志记录。 错误处理将使应用程序能够正常处理错误并相应地显示错误消息。 错误日志记录将允许你查找并修复已发生的错误。 本教程以上一教程 "URL 路由" 为基础，是 Wingtip 玩具教程系列的一部分。

## <a name="what-youll-learn"></a>你将学习的内容：

- 如何将全局错误处理添加到应用程序的配置。
- 如何在应用程序、页和代码级别添加错误处理。
- 如何记录错误供以后查看。
- 如何显示不损害安全的错误消息。
- 如何实现错误日志记录模块和处理程序（ELMAH）错误日志记录。

## <a name="overview"></a>概述

ASP.NET 应用程序必须能够以一致的方式处理执行期间发生的错误。 ASP.NET 使用公共语言运行时（CLR），这提供了一种以统一方式向应用程序通知错误的方式。 出现错误时，将引发异常。 异常是指应用程序遇到的任何错误、条件或意外行为。

在 .NET Framework 中，异常是从 `System.Exception` 类继承的对象。 异常引发自发生问题的代码区域。 异常将在调用堆栈中向上传递到一个位置，应用程序提供代码来处理异常。 如果应用程序不处理此异常，则会强制浏览器显示错误详细信息。

最佳做法是在代码中的代码级别处理错误，`Try`/`Catch`/代码中的 `Finally` 块。 尝试放置这些块，以使用户能够在发生错误的上下文中更正问题。 如果错误处理块离错误发生的时间太远，则为用户提供解决问题所需的信息变得更加困难。

### <a name="exception-class"></a>Exception 类

Exception 类是异常从中继承的基类。 大多数异常对象是异常类的某个派生类（如 `SystemException` 类、`IndexOutOfRangeException` 类或 `ArgumentNullException` 类）的实例。 Exception 类具有属性，如 `StackTrace` 属性、`InnerException` 属性和 `Message` 属性，这些属性提供有关已发生的错误的特定信息。

### <a name="exception-inheritance-hierarchy"></a>异常继承层次结构

运行时具有从运行时在遇到异常时引发的 `SystemException` 类中派生的基本异常集。 大多数继承自异常类的类（如 `IndexOutOfRangeException` 类和 `ArgumentNullException` 类）都不实现其他成员。 因此，可在异常层次结构、异常名称和异常中包含的信息中找到异常的最重要信息。

### <a name="exception-handling-hierarchy"></a>异常处理层次结构

在 ASP.NET Web 窗体应用程序中，可以根据特定的处理层次结构来处理异常。 可以在以下级别处理异常：

- 应用程序级别
- 页面级别
- 代码级别

当应用程序处理异常时，通常可以检索有关继承自异常类的异常的其他信息，并向用户显示这些信息。 除应用程序、页和代码级别外，还可以使用 IIS 自定义处理程序来处理 HTTP 模块级别的异常。

### <a name="application-level-error-handling"></a>应用程序级别的错误处理

可以通过修改应用程序的配置或在应用程序的*global.asax*文件中添加 `Application_Error` 处理程序来处理应用程序级别的默认错误。

您可以通过向*web.config*文件添加 `customErrors` 节来处理默认错误和 HTTP 错误。 使用 "`customErrors`" 部分，可以指定发生错误时用户将重定向到的默认页面。 它还允许您为特定状态代码错误指定单独的页面。

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

遗憾的是，当你使用配置将用户重定向到其他页面时，你没有发生的错误的详细信息。

但是，你可以通过将代码添加到*global.asax*文件中的 `Application_Error` 处理程序来捕获应用程序中任何位置发生的错误。

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a>页级别错误事件处理

页面级处理程序将用户返回到发生错误的页面，但由于不保留控件的实例，因此页面上将不再有任何内容。 若要向应用程序的用户提供错误详细信息，必须专门将错误详细信息写入页面。

通常使用页面级错误处理程序来记录未处理的错误，或使用户进入可显示有用信息的页面。

此代码示例演示了 ASP.NET 网页中错误事件的处理程序。 此处理程序捕获页面中 `try`/`catch` 块内尚未处理的所有异常。

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

处理错误后，必须通过调用服务器对象的 `ClearError` 方法（`HttpServerUtility` 类）来清除该错误，否则将看到之前发生的错误。

### <a name="code-level-error-handling"></a>代码级别错误处理

Try-catch 语句包含一个 try 块，后跟一个或多个 catch 子句，这些子句指定不同异常的处理程序。 当引发异常时，公共语言运行时（CLR）将查找处理此异常的 catch 语句。 如果当前正在执行的方法不包含 catch 块，则 CLR 将查看调用当前方法的方法，依此类推，直到调用堆栈。 如果未找到 catch 块，则 CLR 向用户显示一条未处理的异常消息，并停止执行程序。

下面的代码示例演示了使用 `try`/`catch`/`finally` 处理错误的常见方法。

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

在上面的代码中，try 块包含需要针对可能的异常进行保护的代码。 在引发异常或成功完成块之前，将执行块。 如果出现 `FileNotFoundException` 异常或 `IOException` 异常，则将执行转移到其他页。 然后，将执行 finally 块中包含的代码，无论是否发生了错误。

## <a name="adding-error-logging-support"></a>添加错误日志记录支持

在将错误处理添加到 Wingtip 玩具示例应用程序之前，你将通过将 `ExceptionUtility` 类添加到*逻辑*文件夹来添加错误日志记录支持。 这样一来，每次应用程序处理错误时，错误详细信息都将添加到错误日志文件中。

1. 右键单击*逻辑*文件夹，然后选择 "**添加** -&gt;**新项**"。   
   随即出现“添加新项”对话框。
2. 选择左侧的 " **Visual C#**  -&gt;**代码**模板" 组。 然后，从中间列表中选择 "**类**"，并将其命名为**ExceptionUtility.cs**。
3. 选择“添加”。 将显示新的类文件。
4. 将现有代码替换为以下代码：  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

发生异常时，可以通过调用 `LogException` 方法，将异常写入异常日志文件。 此方法采用两个参数，即 exception 对象和包含有关异常源的详细信息的字符串。 异常日志将写入到*应用\_Data*文件夹中的错误日志文件 *。*

### <a name="adding-an-error-page"></a>添加错误页

在 Wingtip 玩具示例应用程序中，将使用一个页面来显示错误。 错误页旨在向网站用户显示一条安全的错误消息。 但是，如果用户是发出 HTTP 请求的开发人员，而该请求正在本地提供，则错误页面上将显示其他错误详细信息。

1. 在**解决方案资源管理器**中右键单击项目名称（**Wingtip 玩具**），然后选择 "**添加** -&gt;**新项**"。   
   随即出现“添加新项”对话框。
2. 选择左侧的 " **Visual C#**  -&gt; **Web**模板" 组。 从中间列表中，选择 "**带有母版页的 Web 窗体**"，并将其命名为**ErrorPage**。
3. 单击 **添加**。
4. 选择 "*网站*" 作为母版页的主文件，然后选择 **"确定"** 。
5. 将现有标记替换为以下内容：   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. 替换代码隐藏（*ErrorPage.aspx.cs*）的现有代码，使其显示如下：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

显示错误页面时，将执行 `Page_Load` 事件处理程序。 在 `Page_Load` 处理程序中，确定首先处理错误的位置。 然后，通过调用 Server 对象的 `GetLastError` 方法来确定发生的最后一个错误。 如果异常不再存在，则将创建一般异常。 然后，如果在本地发出 HTTP 请求，则显示所有错误详细信息。 在这种情况下，只有运行 web 应用程序的本地计算机才能看到这些错误的详细信息。 显示错误信息后，会将错误添加到日志文件中，并从服务器中清除错误。

### <a name="displaying-unhandled-error-messages-for-the-application"></a>显示应用程序的未处理错误消息

通过向*web.config*文件添加 `customErrors` 节，可以快速处理整个应用程序中发生的简单错误。 你还可以根据错误的状态代码值指定如何处理错误，如 "404-找不到文件"。

#### <a name="update-the-configuration"></a>更新配置

通过向*web.config*文件添加 `customErrors` 节来更新配置。

1. 在**解决方案资源管理器**中，找到并打开 Wingtip 玩具示例应用程序根目录*处的 web.config 文件。*
2. 将 `customErrors` 部分添加到 `<system.web>` 节点*内的 web.config 文件中*，如下所示：   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. 保存 web.config*文件。*

"`customErrors`" 部分指定模式，该模式设置为 "打开"。 它还指定了 `defaultRedirect`，它会告知应用程序发生错误时要导航到的页面。 此外，还添加了特定的 error 元素，该元素指定在找不到页面时如何处理404错误。 稍后在本教程中，你将添加其他错误处理，以在应用程序级别捕获错误的详细信息。

#### <a name="running-the-application"></a>运行应用程序

现在可以运行应用程序来查看更新的路由。

1. 按**F5**运行 Wingtip 玩具示例应用程序。  
 浏览器将打开并显示*default.aspx*页。
2. 在浏览器中输入以下 URL **（请务必使用端口**号）：  
    `https://localhost:44300/NoPage.aspx`
3. 查看浏览器中显示的*ErrorPage* 。 

    ![ASP.NET 错误处理-找不到页面错误](aspnet-error-handling/_static/image1.png)

当你请求不存在的*NoPage*页时，如果有更多详细信息，"错误" 页将显示简单错误消息和详细的错误信息。 但是，如果用户从远程位置请求了不存在的页，则 "错误" 页将只以红色显示错误消息。

### <a name="including-an-exception-for-testing-purposes"></a>包括用于测试目的的异常

若要在发生错误时验证应用程序的工作方式，可以在 ASP.NET 中特意创建错误条件。 在 Wingtip 玩具示例应用程序中，当加载默认页面时，将引发测试异常以查看发生的情况。

1. 在 Visual Studio 中打开*default.aspx*页的代码隐藏。   
   将显示*Default.aspx.cs*代码隐藏页面。
2. 在 `Page_Load` 处理程序中，添加代码，使处理程序如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

可以创建各种不同类型的异常。 在上面的代码中，将在加载*default.aspx*页面时创建 `InvalidOperationException`。

#### <a name="running-the-application"></a>运行应用程序

您可以运行应用程序，以了解应用程序如何处理异常。

1. 按**CTRL + F5**运行 Wingtip 玩具示例应用程序。  
 应用程序会引发 InvalidOperationException。 

    > [!NOTE] 
    > 
    > 您必须按**CTRL + F5**来显示页面，而不会中断代码以查看 Visual Studio 中的错误来源。
2. 查看浏览器中显示的*ErrorPage* 。 

    ![ASP.NET 错误处理-错误页](aspnet-error-handling/_static/image2.png)

如错误详细信息中所示，该异常已由*web.config 文件中*的 `customError` 节捕获。

### <a name="adding-application-level-error-handling"></a>添加应用程序级别的错误处理

不要使用*web.config*文件中的 `customErrors` 节来捕获异常，其中您几乎不会获得有关异常的信息，您可以在应用程序级别捕获错误并检索错误详细信息。

1. 在**解决方案资源管理器**中，找到并打开*Global.asax.cs*文件。
2. 添加**应用程序\_错误**处理程序，使其显示如下：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

当应用程序中出现错误时，将调用 `Application_Error` 处理程序。 在此处理程序中，将检索并查看最后一个异常。 如果异常未得到处理，并且异常包含内部异常详细信息（即，`InnerException` 不为 null），则应用程序会将执行转移到显示异常详细信息的错误页。

#### <a name="running-the-application"></a>运行应用程序

可以通过在应用程序级别处理异常来运行应用程序，以查看其他错误详细信息。

1. 按**CTRL + F5**运行 Wingtip 玩具示例应用程序。  
 应用程序引发 `InvalidOperationException`。
2. 查看浏览器中显示的*ErrorPage* 。 

    ![ASP.NET 错误处理-应用程序级别错误](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a>添加页面级错误处理

您可以通过使用将 `ErrorPage` 特性添加到页的 `@Page` 指令中，或通过将 `Page_Error` 事件处理程序添加到页的代码隐藏中，将页级别错误处理添加到页中。 在本部分中，将添加一个 `Page_Error` 事件处理程序，该处理程序将执行传输到*ErrorPage*页。

1. 在**解决方案资源管理器**中，找到并打开*Default.aspx.cs*文件。
2. 添加 `Page_Error` 处理程序，使代码隐藏如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

当页面上发生错误时，将调用 `Page_Error` 事件处理程序。 在此处理程序中，将检索并查看最后一个异常。 如果出现 `InvalidOperationException`，`Page_Error` 事件处理程序会将执行转移到显示异常详细信息的错误页。

#### <a name="running-the-application"></a>运行应用程序

现在可以运行应用程序来查看更新的路由。

1. 按**CTRL + F5**运行 Wingtip 玩具示例应用程序。  
 应用程序引发 `InvalidOperationException`。
2. 查看浏览器中显示的*ErrorPage* 。 

    ![ASP.NET 错误处理-页面级别错误](aspnet-error-handling/_static/image4.png)
3. 关闭浏览器窗口。

### <a name="removing-the-exception-used-for-testing"></a>删除用于测试的异常

若要允许 Wingtip 玩具示例应用程序正常运行而不引发您在本教程前面部分添加的异常，请删除该异常。

1. 打开*default.aspx*页的代码隐藏。
2. 在 `Page_Load` 处理程序中，删除引发异常的代码，使处理程序如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a>添加代码级别错误日志记录

如本教程前面所述，你可以添加 try/catch 语句来尝试运行部分代码，并处理发生的第一个错误。 在此示例中，只会将错误详细信息写入错误日志文件，以便以后可以查看该错误。

1. 在**解决方案资源管理器**的*逻辑*文件夹中，找到并打开*PayPalFunctions.cs*文件。
2. 更新 `HttpCall` 方法，使代码如下所示：   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

上面的代码调用 `ExceptionUtility` 类中包含的 `LogException` 方法。 在本教程的前面部分中，已将*ExceptionUtility.cs*类文件添加到*逻辑*文件夹中。 `LogException` 方法采用两个参数。 第一个参数是 exception 对象。 第二个参数是用于识别错误源的字符串。

### <a name="inspecting-the-error-logging-information"></a>检查错误日志记录信息

如前文所述，你可以使用错误日志来确定应用程序中应该首先修复哪些错误。 当然，只会记录已捕获并写入错误日志的错误。

1. 在**解决方案资源管理器**中，找到并打开*应用\_Data*文件夹中的*错误日志文件。*   
 可能需要选择 "**显示所有文件**" 选项，或从**解决方案资源管理器**顶部选择 "**刷新**" 选项以查看*错误日志*文件。
2. 查看在 Visual Studio 中显示的错误日志： 

    ![ASP.NET 错误处理-错误日志](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a>安全错误消息

**请务必注意**，当应用程序显示错误消息时，它不应提供恶意用户在攻击应用程序时可能会有帮助的信息。 例如，如果应用程序尝试将写入数据库失败，则不会显示一条错误消息，其中包含该数据库所使用的用户名。 出于此原因，将向用户显示红色的一般错误消息。 所有其他错误详细信息仅向开发人员显示在本地计算机上。

## <a name="using-elmah"></a>使用 ELMAH

ELMAH （错误日志记录模块和处理程序）是一个错误日志记录工具，它将你作为 NuGet 包插入 ASP.NET 应用程序。 ELMAH 提供以下功能：

- 未处理的异常的日志记录。
- 用于查看重新编码未经处理的异常的整个日志的网页。
- 用于查看每个记录的异常的完整详细信息的网页。
- 发生时每个错误的电子邮件通知。
- 日志中最后15个错误的 RSS 源。

使用 ELMAH 之前，必须先安装它。 使用*NuGet*包安装程序可以轻松地完成此过程。 如本系列教程前面所述，NuGet 是一个 Visual Studio 扩展，可让你轻松地在 Visual Studio 中安装和更新开源库和工具。

1. 在 Visual Studio 的 "**工具**" 菜单中，选择 " **Nuget 包管理器**" > "**管理解决方案的 NuGet 包**"。 

    ![ASP.NET 错误处理-管理解决方案的 NuGet 包](aspnet-error-handling/_static/image6.png)
2. 在 Visual Studio 中显示 "**管理 NuGet 包**" 对话框。
3. 在 "**管理 NuGet 包**" 对话框中，在左侧展开 "**联机**"，然后选择 " **nuget.org**"。然后，从可用包列表中查找并安装**ELMAH**包。 

    ![ASP.NET 错误处理-ELMA NuGet 包](aspnet-error-handling/_static/image7.png)
4. 需要建立 internet 连接才能下载包。
5. 在 "**选择项目**" 对话框中，确保选择了 " **WingtipToys** " 选项，然后单击 **"确定"** 。 

    ![ASP.NET 错误处理-"选择项目" 对话框](aspnet-error-handling/_static/image8.png)
6. 如果需要，请在 "**管理 NuGet 包**" 对话框中单击 "**关闭**"。
7. 如果 Visual Studio 请求你重新加载任何打开的文件，请选择 "**全部为**"。
8. ELMAH 包在项目*根目录的 web.config 文件中*添加其自身的条目。 如果 Visual Studio 询问你是否要重新加载修改后的*web.config*文件，请单击 **"是"** 。

ELMAH 现在可以存储发生的任何未经处理的错误。

### <a name="viewing-the-elmah-log"></a>查看 ELMAH 日志

查看 ELMAH 日志很简单，但首先您将创建一个将在 ELMAH 日志中记录的未经处理的异常。

1. 按**CTRL + F5**运行 Wingtip 玩具示例应用程序。
2. 若要将未经处理的异常写入 ELMAH 日志，请在浏览器中导航到以下 URL （使用端口号）：  
    `https://localhost:44300/NoPage.aspx` 将显示错误页。
3. 若要显示 ELMAH 日志，请在浏览器中导航到以下 URL （使用端口号）：  
    `https://localhost:44300/elmah.axd`

    ![ASP.NET 错误处理-ELMAH 错误日志](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a>总结

在本教程中，已了解如何在应用程序级别、页级别和代码级别处理错误。 还了解了如何记录已处理和未处理的错误，以便以后查看。 你已添加了 ELMAH 实用工具，使用 NuGet 向应用程序提供异常日志记录和通知。 此外，您还了解了安全错误消息的重要性。

## <a name="tutorial-series-conclusion"></a>教程系列结论

感谢大家关注。 我希望这一系列教程有助于您更熟悉 ASP.NET Web 窗体。 如果需要有关 ASP.NET 4.5 和 Visual Studio 2013 中提供的 Web 窗体功能的详细信息，请参阅[Visual Studio 2013 发行说明 ASP.NET 和 Web 工具](../../../../visual-studio/overview/2013/release-notes.md)。 另外，请务必查看**后续步骤**部分中提到的教程，并 defintely 试用[免费的 Azure 试用版](https://azure.microsoft.com/pricing/free-trial/)。

![感谢-Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a>后续步骤

有关将 web 应用程序部署到 Microsoft Azure 的详细信息，请参阅[使用成员资格、OAuth 和 SQL 数据库将安全的 ASP.NET Web 窗体应用程序部署到 Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)网站。

## <a name="free-trial"></a>免费试用版

[Microsoft Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/)  
 将网站发布到 Microsoft Azure 可节省时间、维护和支出。 将 web 应用部署到 Azure 的过程非常简单。 如果需要维护和监视 web 应用，Azure 提供各种工具和服务。 管理 Azure 中的数据、流量、标识、备份、消息传递、媒体和性能。 而且，所有这些都是以一种非常经济高效的方法提供的。

## <a name="additional-resources"></a>其他资源

[通过 ASP.NET 运行状况监视记录错误详细信息](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md)   
[ELMAH](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a>致谢

我想感谢以下人员对本系列教程的内容进行了重大贡献：

- [Alberto Poblacion，MVP &amp; MCT，西班牙](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- [Alex Thissen，荷兰](http://blog.alexthissen.nl/)（twitter： [@alexthissen](http://twitter.com/alexthissen)）
- [美国 Andre Tournier](http://andret503.wordpress.com/)
- Apurva Joshi，Microsoft
- [Bojan Vrhovnik，斯洛文尼亚](http://twitter.com/bvrhovnik)
- [Bruno Sonnino，巴西](http://msmvps.com/blogs/bsonnino)（twitter： [@bsonnino](http://twitter.com/bsonnino)）
- [Carlos dos Santos，巴西](http://www.carloscds.net/)
- [美国 Dave Campbell](http://www.wynapse.com/) （twitter： [@windowsdevnews](http://twitter.com/windowsdevnews)）
- [Jon Galloway，Microsoft](https://weblogs.asp.net/jgalloway) （twitter： [@jongalloway](http://twitter.com/jongalloway)）
- [Michael Sharps](http://www.930solutions.com/) （twitter： [@mrsharps](http://twitter.com/mrsharps)）
- Mike Pope
- [美国 Mitchel 卖方](http://www.mitchelsellers.com/)（twitter： [@MitchelSellers](http://twitter.com/MitchelSellers)）
- [Paul Cociuba，Microsoft](http://linqto.me/Links/pcociuba)
- [圣保罗 Morgado，葡萄牙](http://paulomorgado.net/)
- [Pranav Rastogi 撰写，Microsoft](https://blogs.msdn.com/b/pranav_rastogi)
- [Tim Ammann，Microsoft](https://blogs.iis.net/timamm/default.aspx)
- [Tom Dykstra，Microsoft](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a>社区参与

- Graham Mendick （[@grahammendick](http://twitter.com/grahammendick)）  
  MSDN 上的 Visual Studio 2012 相关代码示例：[导航 Wingtip 玩具](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)
- James Chaney （[jchaney@agvance.net](mailto:jchaney@agvance.net)）  
  MSDN 上的 Visual Studio 2012 相关代码示例： [ASP.NET 4.5 Web 窗体上的示例系列 Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)
- Andrielle Azevedo-Microsoft 技术受众撰稿人（twitter： @driazevedo）  
  Visual Studio 2012 翻译： [Iniciando com ASP.NET Web Forms 4.5-Parte 1-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)

> [!div class="step-by-step"]
> [上一部分](url-routing.md)
