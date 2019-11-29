---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
title: 日志记录错误详细信息（C#）Microsoft Docs
author: rick-anderson
description: 错误日志记录模块和处理程序（ELMAH）提供了在生产环境中记录运行时错误的另一种方法。 ELMAH 是一个免费的开源错误 。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 11f6fe44-64ef-4a38-a3b4-35c7bb992352
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-elmah-cs
msc.type: authoredcontent
ms.openlocfilehash: 5018023eced23e7a70eab90e649f85862c548940
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74570541"
---
# <a name="logging-error-details-with-elmah-c"></a>ELMAH 的日志记录错误详细信息 (C#)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_14_CS.zip)或[下载 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial14_ELMAH_cs.pdf)

> 错误日志记录模块和处理程序（ELMAH）提供了在生产环境中记录运行时错误的另一种方法。 ELMAH 是一个免费的开源错误日志记录库，其中包含一些功能，例如错误筛选功能，还可以查看网页中的错误日志，作为 RSS 源，或将其作为逗号分隔的文件下载。 本教程介绍如何下载和配置 ELMAH。

## <a name="introduction"></a>简介

[前面的教程](logging-error-details-with-asp-net-health-monitoring-cs.md)探讨了 ASP。NET 的运行状况监视系统，它提供了一个现成的库，用于记录范围广泛的 Web 事件。 许多开发人员使用运行状况监视来记录未经处理的异常的详细信息并发送电子邮件。 不过，此系统有一些难题。 首先，最重要的是，缺少任何类型的用户界面来查看有关记录的事件的信息。 如果要查看最近10个错误的摘要，或查看上周发生的错误的详细信息，则必须浏览数据库、扫描电子邮件收件箱或生成显示 `aspnet_WebEvent_Events` 表中的信息的网页。

其他难点围绕运行状况监视的复杂性。 由于运行状况监视可用于记录不同事件的很多，因此，由于有多种选项可用于指示事件的记录方式和时间，正确配置运行状况监视系统可能是一件繁重的任务。 最后，存在兼容性问题。 由于运行状况监视首先添加到版本2.0 中的 .NET Framework，因此对于使用 ASP.NET 版本1.x 生成的旧版 web 应用程序不可用。 此外，在前面的教程中，我们使用的 `SqlWebEventProvider` 类将错误详细信息记录到数据库中，只适用于 Microsoft SQL Server 的数据库。 如果需要将错误记录到备用数据存储（如 XML 文件或 Oracle 数据库），则需要创建自定义日志提供程序类。

运行状况监视系统的替代方法是错误日志记录模块和处理程序（ELMAH），这是由[Atif Aziz](http://www.raboof.com/)创建的一个免费的开源错误日志记录系统。 这两个系统之间最明显的区别在于，ELAMH 可以显示一个错误列表，还可以在网页中显示特定错误的详细信息，并将其作为 RSS 源来显示。 ELMAH 比运行状况监视更易于配置，因为它只记录错误。 此外，ELMAH 还支持 ASP.NET 1.x、ASP.NET 2.0 和 ASP.NET 3.5 应用程序，并附带各种日志源提供程序。

本教程介绍了向 ASP.NET 应用程序添加 ELMAH 所涉及的步骤。 让我们进入正题！

> [!NOTE]
> 运行状况监视系统和 ELMAH 都有其各自的优缺点。 我鼓励您尝试这两个系统，并决定哪一种最适合您的需求。

## <a name="adding-elmah-to-an-aspnet-web-application"></a>将 ELMAH 添加到 ASP.NET Web 应用程序

将 ELMAH 集成到新的或现有的 ASP.NET 应用程序是一个简单且简单的过程，只需5分钟即可完成。 简而言之，它涉及四个简单的步骤：

1. 下载 ELMAH 并将 `Elmah.dll` 程序集添加到你的 web 应用程序，
2. 在 `Web.config`中注册 ELMAH 的 HTTP 模块和处理程序。
3. 指定 ELMAH 的配置选项，并
4. 如果需要，请创建错误日志源基础结构。

让我们逐一演练其中每个步骤。

### <a name="step-1-downloading-the-elmah-project-files-and-addingelmahdllto-your-web-application"></a>步骤1：下载 ELMAH 项目文件并将`Elmah.dll`添加到 Web 应用程序

ELMAH 1.0 BETA 3 （版本10617）（编写时的最新版本）包含在随本教程提供的下载中。 或者，你可以访问[ELMAH 网站](https://code.google.com/p/elmah/)以获取最新版本或下载源代码。 将 ELMAH 下载内容提取到桌面上的文件夹，并找到 ELMAH assembly 文件（`Elmah.dll`）。

> [!NOTE]
> `Elmah.dll` 文件位于下载 `Bin` 文件夹中，该文件夹包含不同 .NET Framework 版本的子文件夹，以及发布和调试版本。 使用适当 framework 版本的发布版本。 例如，如果要生成 ASP.NET 3.5 web 应用程序，请从 `Bin\net-3.5\Release` 文件夹复制 `Elmah.dll` 文件。

接下来，打开 Visual Studio，右键单击 "解决方案资源管理器中的" 网站名称 "，然后从上下文菜单中选择" 添加引用 "，将程序集添加到项目。 此时将打开 "添加引用" 对话框。 导航到 "浏览" 选项卡，然后选择 "`Elmah.dll` 文件。 此操作会将 `Elmah.dll` 文件添加到 web 应用程序的 `Bin` 文件夹中。

> [!NOTE]
> Web 应用程序项目（WAP）类型不会在解决方案资源管理器中显示 `Bin` 文件夹。 相反，它会在 "引用" 文件夹下列出这些项。

`Elmah.dll` 程序集包括 ELMAH 系统使用的类。 这些类分为以下三个类别之一：

- **Http**模块-http 模块是为 `HttpApplication` 事件（如 `Error` 事件）定义事件处理程序的类。 ELMAH 包含多个 HTTP 模块，其中三个最无关： 

    - `ErrorLogModule`-将未经处理的异常记录到日志源中。
    - `ErrorMailModule`-发送电子邮件中未经处理的异常的详细信息。
    - `ErrorFilterModule`-应用开发人员指定的筛选器，以确定要记录的异常以及忽略哪些异常。
- **Http**处理程序-Http 处理程序是负责为特定类型的请求生成标记的类。 ELMAH 包含 HTTP 处理程序，该处理程序以网页形式呈现错误详细信息，作为 RSS 源，或以逗号分隔的文件（CSV）的形式呈现。
- **错误日志源**-在此情况下，ELMAH 可以将错误记录到内存、Microsoft SQL Server 数据库、Microsoft Access 数据库、Oracle 数据库、XML 文件、SQLite 数据库或 Vista DB 数据库。 与运行状况监视系统一样，ELMAH 的体系结构是使用提供程序模型构建的，这意味着，如果需要，你可以创建并无缝集成你自己的自定义日志源提供程序。

### <a name="step-2-registering-elmahs-http-module-and-handler"></a>步骤2：注册 ELMAH 的 HTTP 模块和处理程序

虽然 `Elmah.dll` 文件包含自动记录未经处理的异常和显示网页中的错误详细信息所需的 HTTP 模块和处理程序，但必须在 web 应用程序的配置中显式注册这些内容。 `ErrorLogModule` HTTP 模块在注册后会订阅 `HttpApplication`的 `Error` 事件。 每当引发此事件时，`ErrorLogModule` 会将异常的详细信息记录到指定的日志源中。 我们将在下一节 "配置 ELMAH" 中看到如何定义日志源提供程序。 在从网页查看错误日志时，`ErrorLogPageFactory` HTTP 处理程序工厂负责生成标记。

注册 HTTP 模块和处理程序的特定语法取决于为站点提供支持的 web 服务器。 对于 ASP.NET 开发服务器和 Microsoft 的 IIS 版本6.0 及更早版本，HTTP 模块和处理程序在 `<httpModules>` 和 `<httpHandlers>` 节中注册，这些部分显示在 `<system.web>` 元素中。 如果使用 IIS 7.0，则需要在 `<system.webServer>` 元素的 `<modules>` 和 `<handlers>` 节中注册它们。 幸运的是，无论使用哪种 web 服务器，*都可以在这两个*位置定义 HTTP 模块和处理程序。 此选项是最易于移植的选项，因为它允许在开发和生产环境中使用相同的配置，而不考虑所使用的 web 服务器。

首先，在 `<system.web>`的 `<httpModules>` 和 `<httpHandlers>` 部分中注册 `ErrorLogModule` HTTP 模块和 `ErrorLogPageFactory` HTTP 处理程序。 如果配置已定义了这两个元素，则只需包括 ELMAH 的 HTTP 模块和处理程序的 `<add>` 元素。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample1.xml)]

接下来，在 `<system.webServer>` 元素中注册 ELMAH 的 HTTP 模块和处理程序。 如前所述，如果在配置中不存在此元素，请添加该元素。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample2.xml)]

默认情况下，如果在 `<system.web>` 部分注册了 HTTP 模块和处理程序，则使用 IIS 7 投诉原因。 `<validation>` 元素中的 `validateIntegratedModeConfiguration` 属性指示 IIS 7 禁止显示此类错误消息。

请注意，用于注册 `ErrorLogPageFactory` HTTP 处理程序的语法包括设置为 `elmah.axd`的 `path` 属性。 此属性通知 web 应用程序，如果请求到达名为 `elmah.axd` 的页，则该请求应由 `ErrorLogPageFactory` HTTP 处理程序进行处理。 在本教程的后面部分，我们将看到 `ErrorLogPageFactory` 的 HTTP 处理程序。

### <a name="step-3-configuring-elmah"></a>步骤3：配置 ELMAH

ELMAH 会在名为 `<elmah>`的自定义配置节中的网站 `Web.config` 文件中查找其配置选项。 若要在中使用自定义节 `Web.config` 必须先在 `<configSections>` 元素中定义它。 打开 `Web.config` 文件，并将以下标记添加到 `<configSections>`：

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample3.xml)]

> [!NOTE]
> 如果要为 ASP.NET 1.x 应用程序配置 ELMAH，请从上面的 `<section>` 元素中删除 `requirePermission="false"` 特性。

上面的语法注册自定义 `<elmah>` 节及其子节： `<security>`、`<errorLog>`、`<errorMail>`和 `<errorFilter>`。

接下来，将 `<elmah>` 部分添加到 `Web.config`。 此部分应显示在与 `<system.web>` 元素相同的级别。 在 `<elmah>` 部分中，添加 `<security>` 和 `<errorLog>` 节，如下所示：

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample4.xml)]

`<security>` 节的 `allowRemoteAccess` 属性指示是否允许远程访问。 如果此值设置为0，则只能在本地查看 "错误日志" 网页。 如果将此属性设置为1，则将为远程和本地访问者启用 "错误日志" 网页。 现在，让我们禁用远程访问者的错误日志网页。 稍后我们将允许远程访问，稍后我们有机会讨论这样做的安全问题。

`<errorLog>` 部分定义错误日志源，该源指示记录错误详细信息的位置;它类似于运行状况监视系统中的 `<providers>` 部分。 上述语法将 `SqlErrorLog` 类指定为错误日志源，这会将错误记录到 `connectionStringName` 特性值所指定的 Microsoft SQL Server 数据库中。

> [!NOTE]
> ELMAH 附带了额外的错误日志提供程序，可用于将错误记录到 XML 文件、Microsoft Access 数据库、Oracle 数据库和其他数据存储区中。 有关如何使用这些备用错误日志提供程序的信息，请参阅包含在 ELMAH 下载中的示例 `Web.config` 文件。

### <a name="step-4-creating-the-error-log-source-infrastructure"></a>步骤4：创建错误日志源基础结构

ELMAH 的 `SqlErrorLog` 提供程序将错误详细信息记录到指定的 Microsoft SQL Server 数据库。 `SqlErrorLog` 提供程序要求此数据库具有一个名为 `ELMAH_Error` 的表和三个存储过程： `ELMAH_GetErrorsXml`、`ELMAH_GetErrorXml`和 `ELMAH_LogError`。 ELMAH 下载内容包括一个名为 `db` `SQLServer.sql` 的文件，该文件包含用于创建此表和这些存储过程的 T-sql。 需要在数据库上运行这些语句才能使用 `SqlErrorLog` 提供程序。

**图1和图** **2**显示了 `SqlErrorLog` 提供程序所需的数据库对象之后，Visual Studio 中的数据库资源管理器。

[![](logging-error-details-with-elmah-cs/_static/image2.png)](logging-error-details-with-elmah-cs/_static/image1.png)

**图 1**： `SqlErrorLog` 提供程序将错误记录到 `ELMAH_Error` 表中

[![](logging-error-details-with-elmah-cs/_static/image4.png)](logging-error-details-with-elmah-cs/_static/image3.png)

**图 2**： `SqlErrorLog` 提供程序使用三个存储过程

## <a name="elmah-in-action"></a>操作中的 ELMAH

此时，我们已将 ELMAH 添加到 web 应用程序中，注册了 `ErrorLogModule` HTTP 模块和 `ErrorLogPageFactory` HTTP 处理程序，在 `Web.config`中指定了 ELMAH 的配置选项，并为 `SqlErrorLog` 错误日志提供程序添加了所需的数据库对象。 现在，我们已准备好在操作中看到 ELMAH！ 访问书籍评论网站并访问生成运行时错误的页面（如 `Genre.aspx?ID=foo`）或不存在的页面（如 `NoSuchPage.aspx`）。 访问这些页面时看到的内容取决于 `<customErrors>` 配置以及你是在本地还是远程访问。 （请返回到[*显示自定义错误页*教程](displaying-a-custom-error-page-cs.md)，了解本主题的复习。）

当发生未经处理的异常时，ELMAH 不会影响向用户显示的内容;它只记录其详细信息。 可以从网站的根 `elmah.axd` 访问此错误日志，如 `http://localhost/BookReviews/elmah.axd`。 （此文件在物理上并不存在于你的项目中，但当请求进入时，`elmah.axd` 运行时将它调度到 `ErrorLogPageFactory` HTTP 处理程序，该处理程序会生成发送回浏览器的标记。）

> [!NOTE]
> 还可以使用 "`elmah.axd`" 页指示 ELMAH 生成测试错误。 访问 `elmah.axd/test` （如在中 `http://localhost/BookReviews/elmah.axd/test`）将导致 ELMAH 引发类型 `Elmah.TestException`的异常，该异常包含以下错误消息： "这是可以安全忽略的测试异常。"

**图 3**显示了从开发环境中访问 `elmah.axd` 时的错误日志。

[![](logging-error-details-with-elmah-cs/_static/image6.png)](logging-error-details-with-elmah-cs/_static/image5.png)

**图 3**： `Elmah.axd` 显示网页中的错误日志  
（[单击以查看完全大小的映像](logging-error-details-with-elmah-cs/_static/image7.png)）

**图 3**中的错误日志包含六个错误条目。 每个条目都包括 HTTP 状态代码（404或500，适用于这些错误）、类型、说明、发生错误时登录用户的名称以及日期和时间。 单击 "详细信息" 链接将显示一页，其中包含错误详细信息的黄色屏幕上显示的错误消息（请参阅**图 4**）以及错误发生时服务器变量的值（参见**图 5**）。 你还可以查看保存错误详细信息的原始 XML，其中包括其他信息，例如 HTTP POST 标头中的值。

[![](logging-error-details-with-elmah-cs/_static/image9.png)](logging-error-details-with-elmah-cs/_static/image8.png)

**图 4**：查看错误详细信息 YSOD  
（[单击以查看完全大小的映像](logging-error-details-with-elmah-cs/_static/image10.png)）

[![](logging-error-details-with-elmah-cs/_static/image12.png)](logging-error-details-with-elmah-cs/_static/image11.png)

**图 5**：在发生错误时浏览服务器变量集合的值  
（[单击以查看完全大小的映像](logging-error-details-with-elmah-cs/_static/image13.png)）

将 ELMAH 部署到生产网站需要：

- 将 `Elmah.dll` 文件复制到生产上的 `Bin` 文件夹中，
- 将 ELMAH 特定的配置设置复制到生产环境中使用的 `Web.config` 文件，并
- 将错误日志源基础结构添加到生产数据库中。

我们已经探讨了在以前的教程中将文件从开发复制到生产的方法。 最简单的方法是在生产数据库中获取错误日志源基础结构，以便使用 SQL Server Management Studio 连接到生产数据库，然后执行 `SqlServer.sql` 脚本文件，这将创建所需的表和存储过程。

### <a name="viewing-the-error-details-page-on-production"></a>查看生产中的错误详细信息页

将站点部署到生产环境后，请访问生产网站并生成未经处理的异常。 与开发环境一样，ELMAH 不会对在发生未经处理的异常时所显示的错误页产生任何影响;而只是记录错误。 如果尝试从生产环境访问 "错误日志" 页（`elmah.axd`），则将看到另与**图 6**中所示的 "禁止访问" 页。

[![](logging-error-details-with-elmah-cs/_static/image15.png)](logging-error-details-with-elmah-cs/_static/image14.png)

**图 6**：默认情况下，远程访问者无法查看错误日志网页  
（[单击以查看完全大小的映像](logging-error-details-with-elmah-cs/_static/image16.png)）

请记住，在 ELMAH 配置的 `<security>` 部分，我们将 `allowRemoteAccess` 属性设置为0，这将禁止远程用户查看错误日志。 必须禁止匿名访问者查看错误日志，因为错误详细信息可能会显示安全漏洞或其他敏感信息。 如果决定将此属性设置为1并启用对错误日志的远程访问，请务必锁定 `elmah.axd` 路径，以便只有授权的访问者可以访问它。 这可以通过将 `<location>` 元素添加到 `Web.config` 文件来实现。

以下配置仅允许管理员角色中的用户访问错误日志网页：

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample5.xml)]

> [!NOTE]
> 管理员角色和系统中的三个用户（Jisun 和 Alice）已在[*配置使用应用程序服务*教程的网站](configuring-a-website-that-uses-application-services-cs.md)中添加。 用户 Scott 和 Jisun 是管理员角色的成员。 有关身份验证和授权的详细信息，请参阅我的[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。

生产环境中的错误日志现在可以由远程用户查看;有关错误日志网页的屏幕截图，请参阅**图 3**、 **4**和**5** 。 但是，如果匿名或非管理员用户尝试查看错误日志页面，则会自动将其重定向到登录页（`Login.aspx`），如**图 7**所示。

[![](logging-error-details-with-elmah-cs/_static/image18.png)](logging-error-details-with-elmah-cs/_static/image17.png)

**图 7**：未经授权的用户将自动重定向到登录页  
（[单击以查看完全大小的映像](logging-error-details-with-elmah-cs/_static/image19.png)）

### <a name="programmatically-logging-errors"></a>以编程方式记录错误

ELMAH 的 `ErrorLogModule` HTTP 模块自动将未经处理的异常记录到指定的日志源中。 或者，您可以通过使用 `ErrorSignal` 类及其 `Raise` 方法来记录错误，而无需引发未经处理的异常。 向 `Raise` 方法传递 `Exception` 对象，并将其记录为已引发该异常，并已在未处理的情况下到达 ASP.NET 运行时。 但差别在于，请求在调用 `Raise` 方法后继续正常执行，而引发的未经处理的异常将中断请求的正常执行，并导致 ASP.NET 运行时显示配置的错误页。

如果某些操作可能会失败，则 `ErrorSignal` 类非常有用，但其失败对执行的整体操作并不是灾难性的。 例如，网站可能包含一个采用用户输入的窗体，将其存储在数据库中，然后向用户发送一封电子邮件，告知他们信息已处理。 如果成功将信息保存到数据库，则会发生什么情况，但在发送电子邮件时出现错误？ 一种选择是引发异常，并将用户发送到错误页。 但是，这可能会让用户认为他们输入的信息未保存。 另一种方法是记录与电子邮件相关的错误，但不以任何方式更改用户的体验。 这就是 `ErrorSignal` 类有用的地方。

[!code-csharp[Main](logging-error-details-with-elmah-cs/samples/sample6.cs)]

## <a name="error-notification-via-email"></a>通过电子邮件发送的错误通知

除了将错误记录到数据库之外，还可以将 ELMAH 配置为向指定接收方发送电子邮件错误详细信息。 此功能由 `ErrorMailModule` HTTP 模块提供;因此，必须在 `Web.config` 中注册此 HTTP 模块，才能通过电子邮件发送错误详细信息。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample7.xml)]

接下来，在 `<elmah>` 元素的 `<errorMail>` 部分指定有关错误电子邮件的信息，指示电子邮件的发件人和收件人、主题以及是否以异步方式发送电子邮件。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample8.xml)]

使用上述设置后，当发生运行时错误时，ELMAH 会向 support@example.com 发送一封电子邮件，其中包含错误详细信息。 ELMAH 的错误电子邮件包含与 "错误详细信息" 网页中显示的信息相同的信息，即错误消息、堆栈跟踪和服务器变量（请参阅**图 4**和**5**）。 错误电子邮件还包括异常详细信息，即死亡内容的黄色屏幕（`YSOD.html`）。

**图 8**显示了通过访问 `Genre.aspx?ID=foo`生成的 ELMAH 错误电子邮件。 虽然**图 8**只显示错误消息和堆栈跟踪，但服务器变量会在电子邮件的正文中进一步向下提供。

[![](logging-error-details-with-elmah-cs/_static/image21.png)](logging-error-details-with-elmah-cs/_static/image20.png)

**图 8**：你可以配置 ELMAH 以通过电子邮件发送错误详细信息  
（[单击以查看完全大小的映像](logging-error-details-with-elmah-cs/_static/image22.png)）

## <a name="only-logging-errors-of-interest"></a>仅记录相关错误

默认情况下，ELMAH 记录每个未处理的异常的详细信息，包括404和其他 HTTP 错误。 您可以指示 ELMAH 使用错误筛选来忽略这些错误或其他类型的错误。 筛选逻辑由 ELMAH 的 `ErrorFilterModule` HTTP 模块执行，你需要在 `Web.config` 中进行注册，才能使用筛选逻辑。 用于筛选的规则在 `<errorFilter>` 部分中指定。

以下标记指示 ELMAH 不记录404错误。

[!code-xml[Main](logging-error-details-with-elmah-cs/samples/sample9.xml)]

> [!NOTE]
> 别忘了，若要使用错误筛选，必须注册 `ErrorFilterModule` HTTP 模块。

`<test>` 部分内的 `<equal>` 元素称为 "断言"。 如果断言的计算结果为 true，则将根据 ELMAH 的日志筛选错误。 还有其他断言，其中包括： `<greater>`、`<greater-or-equal>`、`<not-equal>`、`<lesser>`、`<lesser-or-equal>`等。 你还可以使用 `<and>` 和 `<or>` 布尔运算符来合并断言。 此外，您甚至可以将简单的 JavaScript 表达式包含为断言，或在或 Visual Basic 中编写您自己C#的断言。

有关 ELMAH 的错误筛选功能的详细信息，请参阅[ELMAH wiki](https://code.google.com/p/elmah/w/list)中的[错误筛选部分](https://code.google.com/p/elmah/wiki/ErrorFiltering)。

## <a name="summary"></a>总结

ELMAH 提供一种简单而强大的机制，用于在 ASP.NET web 应用程序中记录错误。 与 Microsoft 的运行状况监视系统类似，ELMAH 可以将错误记录到数据库中，并可以通过电子邮件将错误详细信息发送给开发人员。 与运行状况监视系统不同，ELMAH 包含对更广泛的错误日志数据存储的全新支持，包括： Microsoft SQL Server、Microsoft Access、Oracle、XML 文件，等等。 此外，ELMAH 还提供了一种内置机制，用于查看错误日志以及有关网页中特定错误的详细信息，`elmah.axd`。 `elmah.axd` 页还可以将错误信息作为 RSS 源或以逗号分隔的值文件（CSV）的形式呈现，您可以使用 Microsoft Excel 读取该文件。 还可以指示 ELMAH 使用声明性或编程断言从日志中筛选错误。 和 ELMAH 可以与 ASP.NET 版本1.x 应用程序一起使用。

每个已部署的应用程序都应有一些机制来自动记录未经处理的异常，并向开发团队发送通知。 此操作是使用运行状况监视来实现还是使用 ELMAH 为辅助。 换句话说，无论你使用的是运行状况监视还是 ELMAH，都不是很重要。评估两个系统，然后选择最符合你需求的系统。 基本上重要的是，一些机制可用于在生产环境中记录未经处理的异常。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ELMAH-错误日志记录模块和处理程序](http://dotnetslackers.com/articles/aspnet/ErrorLoggingModulesAndHandlers.aspx)
- [ELMAH 项目页](https://code.google.com/p/elmah/)（源代码、示例、wiki）
- [将 ELMAH 插入 Web 应用程序以捕获未经处理的异常](http://screencastaday.com/ScreenCasts/43_Plugging_Elmah_into_Web_Application_to_Catch_Unhandled_Exceptions.aspx)（视频）
- [安全错误日志页面](https://code.google.com/p/elmah/wiki/SecuringErrorLogPages)
- [使用 HTTP 模块和处理程序创建可插入的 ASP.NET 组件](https://msdn.microsoft.com/library/aa479332.aspx)
- [网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [上一页](logging-error-details-with-asp-net-health-monitoring-cs.md)
> [下一页](precompiling-your-website-cs.md)
