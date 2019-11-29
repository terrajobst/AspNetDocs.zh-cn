---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-vb
title: 通过 ASP.NET 运行状况监视日志记录错误详细信息（VB） |Microsoft Docs
author: rick-anderson
description: Microsoft 的运行状况监视系统提供一种简单且可自定义的方式来记录各种 web 事件，包括未经处理的异常。 本教程将指导将 。
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 09a6c74e-936a-4c04-8547-5bb313a4e4a3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-vb
msc.type: authoredcontent
ms.openlocfilehash: f57aca41771adfd9a7c7f38da1916db9197262da
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74587779"
---
# <a name="logging-error-details-with-aspnet-health-monitoring-vb"></a>ASP.NET 运行状况监视的日志记录错误详细信息 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载代码](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_13_VB.zip)或[下载 PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial13_HealthMonitoring_vb.pdf)

> Microsoft 的运行状况监视系统提供一种简单且可自定义的方式来记录各种 web 事件，包括未经处理的异常。 本教程介绍如何设置运行状况监视系统，以将未经处理的异常记录到数据库，并通过电子邮件通知开发人员。

## <a name="introduction"></a>简介

日志记录是一种有用的工具，用于监视已部署应用程序的运行状况，并诊断可能出现的任何问题。 尤其重要的是记录已部署的应用程序中发生的错误，以便可以对其进行修正。 ASP.NET 应用程序中发生未经处理的异常时，将引发 `Error` 事件;[前面的教程](processing-unhandled-exceptions-vb.md)演示了如何通过为 `Error` 事件创建事件处理程序，通知开发人员出现错误并记录其详细信息。 但是，创建一个 `Error` 事件处理程序来记录错误的详细信息并通知开发人员，这是不必要的，因为此任务可以由 ASP 执行。网络*运行状况监视系统*。

运行状况监视系统是在 ASP.NET 2.0 中引入的，旨在通过记录应用程序或请求生存期内发生的事件来监视已部署的 ASP.NET 应用程序的运行状况。 运行状况监视系统记录的事件被称为*运行状况监视事件*或*Web 事件*，包括：

- 应用程序生存期事件，例如当应用程序启动或停止时
- 安全事件，包括登录尝试失败和失败的 URL 授权请求
- 应用程序错误，包括未经处理的异常、查看状态分析异常、请求验证异常、编译错误以及其他类型的错误。

当引发运行状况监视事件时，可以将其记录到任意数量的指定*日志源*中。 运行状况监视系统附带日志源，用于将 Web 事件记录到 Microsoft SQL Server 数据库、Windows 事件日志或通过电子邮件发送给其他人。 还可以创建自己的日志源。

运行状况监视系统日志以及使用的日志源的事件是在 `Web.config`中定义的。 使用几行配置标记，您可以使用运行状况监视将所有未经处理的异常记录到数据库中，并通过电子邮件向您通知例外。

## <a name="exploring-the-health-monitoring-systems-configuration"></a>了解运行状况监视系统的配置

运行状况监视系统的行为由其在 `Web.config`的[`<healthMonitoring>` 元素](https://msdn.microsoft.com/library/2fwh2ss9.aspx)中的配置信息定义。 此配置节定义了以下三个重要信息，其中包括：

1. 应记录引发时的运行状况监视事件，
2. 日志源和
3. （1）中定义的每个运行状况监视事件如何映射到（2）中定义的日志源。

此信息通过三个子配置元素来指定：分别[`<eventMappings>`](https://msdn.microsoft.com/library/yc5yk01w.aspx)、 [`<providers>`](https://msdn.microsoft.com/library/zaa41kz1.aspx)和[`<rules>`](https://msdn.microsoft.com/library/fe5wyxa0.aspx)。

默认的运行状况监视系统配置信息可在 `%WINDIR%\Microsoft.NET\Framework\version\CONFIG` 文件夹中的 `Web.config` 文件中找到。 此默认配置信息（为了简洁起见，移除了一些标记）如下所示：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample1.xml)]

相关的运行状况监视事件在 `<eventMappings>` 元素中定义，该元素向运行状况监视事件的类提供一个友好名称。 在上面的标记中，`<eventMappings>` 元素将友好名称 "所有错误" 分配给类型为 `WebBaseErrorEvent` 的运行状况监视事件，并将名称 "失败审核" 分配给 `WebFailureAuditEvent`类型的运行状况监视事件。

`<providers>` 元素定义日志源，为它们提供友好名称，并指定任何特定于日志源的配置信息。 第一个 `<add>` 元素定义 "EventLogProvider" 提供程序，该提供程序使用 `EventLogWebEventProvider` 类记录指定的运行状况监视事件。 `EventLogWebEventProvider` 类将事件记录到 Windows 事件日志中。 第二个 `<add>` 元素定义 "SqlWebEventProvider" 提供程序，该提供程序通过 `SqlWebEventProvider` 类将事件记录到 Microsoft SQL Server 数据库。 "SqlWebEventProvider" 配置在其他配置选项中指定数据库的连接字符串（`connectionStringName`）。

`<rules>` 元素将 `<eventMappings>` 元素中指定的事件映射到 `<providers>` 元素中的日志源。 默认情况下，ASP.NET web 应用程序将所有未经处理的异常和审核失败记录到 Windows 事件日志中。

## <a name="logging-events-to-a-database"></a>将事件记录到数据库

通过向应用程序的 `Web.config` 文件添加 `<healthMonitoring>` 部分，可以在 web 应用程序的基础上按 web 应用程序自定义运行状况监视系统的默认配置。 您可以使用 `<add>` 元素在 `<eventMappings>`、`<providers>`和 `<rules>` 部分中包含其他元素。 若要从默认配置中删除设置，请使用 `<remove>` 元素，或使用 `<clear />` 删除这些部分中的所有默认值。 接下来，让我们将书籍评论 web 应用程序配置为使用 `SqlWebEventProvider` 类将所有未经处理的异常记录到 Microsoft SQL Server 数据库中。

`SqlWebEventProvider` 类是运行状况监视系统的一部分，它将运行状况监视事件记录到指定的 SQL Server 数据库。 `SqlWebEventProvider` 类需要指定的数据库包含名为 `aspnet_WebEvent_LogEvent`的存储过程。 此存储过程将传递事件的详细信息，并负责存储事件的详细信息。 好消息是不需要创建此存储过程，也不需要创建表来存储事件的详细信息。 可以使用 `aspnet_regsql.exe` 工具将这些对象添加到数据库。

> [!NOTE]
> 在[*配置使用应用程序服务*教程的网站时，将在配置使用教程的网站](configuring-a-website-that-uses-application-services-vb.md)上讨论 `aspnet_regsql.exe` 工具。网络的应用程序服务。 因此，书籍检查网站的数据库已经包含 `aspnet_WebEvent_LogEvent` 存储过程，该存储过程将事件信息存储到名为 `aspnet_WebEvent_Events`的表中。

将所需的存储过程和表添加到数据库后，剩下的就是指示运行状况监视将所有未经处理的异常记录到数据库中。 通过将以下标记添加到网站的 `Web.config` 文件来完成此操作：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample2.xml)]

上面的运行状况监视配置标记使用 `<clear />` 元素从 `<eventMappings>`、`<providers>`和 `<rules>` 部分中擦除预定义的运行状况监视配置信息。 然后，它向其中每个部分添加一个条目。

- `<eventMappings>` 元素定义了一个名为 "所有错误" 的名为 "所有错误" 的运行状况监视事件，每当发生未处理的异常时都会引发该事件。
- `<providers>` 元素定义了使用 `SqlWebEventProvider` 类的名为 "SqlWebEventProvider" 的单一日志源。 `connectionStringName` 属性设置为 "ReviewsConnectionString"，这是在 `<connectionStrings>` 部分中定义的连接字符串的名称。
- 最后，&lt;规则&gt; 元素指示当 "所有错误" 事件发生应使用 "SqlWebEventProvider" 提供程序记录它时的情况。

此配置信息指示运行状况监视系统将所有未经处理的异常记录到书籍检查数据库。

> [!NOTE]
> 仅对服务器错误引发 `WebBaseErrorEvent` 事件;对于 HTTP 错误，不会引发此错误，例如，请求找不到 ASP.NET 资源。 这不同于为服务器和 HTTP 错误引发 `HttpApplication` 类的 `Error` 事件的行为。

若要查看运行状况监视系统的运行状况，请访问网站并通过访问 `Genre.aspx?ID=foo`生成运行时错误。 应会看到相应的错误页-异常详细信息黄色屏幕死亡（在本地访问时）或自定义错误页（访问生产中的站点时）。 在后台，运行状况监视系统将错误信息记录到数据库中。 `aspnet_WebEvent_Events` 表中应有一条记录（请参阅**图 1**）;此记录包含有关刚刚发生的运行时错误的信息。

[![](logging-error-details-with-asp-net-health-monitoring-vb/_static/image2.png)](logging-error-details-with-asp-net-health-monitoring-vb/_static/image1.png)

**图 1**：错误详细信息已记录到 `aspnet_WebEvent_Events` 表中  
（[单击以查看完全大小的映像](logging-error-details-with-asp-net-health-monitoring-vb/_static/image3.png)）

### <a name="displaying-the-error-log-in-a-web-page"></a>在网页中显示错误日志

在网站的当前配置中，运行状况监视系统会将所有未经处理的异常记录到数据库中。 但是，运行状况监视并不提供通过网页查看错误日志的任何机制。 但是，您可以生成一个从数据库显示此信息的 ASP.NET 页面。 （正如我们稍后将看到的，你可以选择在电子邮件中向你发送错误详细信息。）

如果创建此类页面，请确保只允许授权用户查看错误详细信息。 如果你的站点已使用用户帐户，则可以使用 URL 授权规则将对页面的访问限制为特定的用户或角色。 若要详细了解如何根据登录的用户授予或限制对网页的访问权限，请参阅[网站安全教程](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)。

> [!NOTE]
> 后续教程将探讨一项名为 ELMAH 的替代错误日志记录和通知系统。 ELMAH 包含一种内置机制，用于从网页和 RSS 源查看错误日志。

## <a name="logging-events-to-email"></a>将事件记录到电子邮件

运行状况监视系统包含一个日志源提供程序，该提供程序将事件 "记录" 到电子邮件中。 日志源包括在电子邮件正文中记录到数据库中的相同信息。 你可以使用此日志源在发生特定的运行状况监视事件时通知开发人员。

接下来，我们将对网站的配置进行更新，以便在出现异常时收到电子邮件。 若要实现此目的，我们需要执行三项任务：

1. 将 ASP.NET web 应用程序配置为发送电子邮件。 这是通过指定如何通过 `<system.net>` 配置元素发送电子邮件来实现的。 有关在 ASP.NET 应用程序中发送电子邮件的详细信息，请参阅[在 ASP.NET 中发送电子](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)邮件和[系统 .NET. Mail 常见问题解答](http://systemnetmail.com/)。
2. 在 `<providers>` 元素中注册电子邮件日志源提供程序，并
3. 将一个项添加到 `<rules>` 元素，该元素将 "所有错误" 事件映射到步骤中添加的日志源提供程序（2）。

运行状况监视系统包括两个电子邮件日志源提供程序类： `SimpleMailWebEventProvider` 和 `TemplatedMailWebEventProvider`。 [`SimpleMailWebEventProvider` 类](https://msdn.microsoft.com/library/system.web.management.simplemailwebeventprovider.aspx)发送包含事件详细信息的纯文本电子邮件，并对电子邮件正文进行了很少的自定义。 使用[`TemplatedMailWebEventProvider` 类](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx)指定 ASP.NET 页，该页面的呈现的标记用作电子邮件的正文。 使用[`TemplatedMailWebEventProvider` 类](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx)可以更好地控制电子邮件的内容和格式，但需要更多的前期工作，因为必须创建 ASP.NET 页面来生成电子邮件的正文。 本教程重点介绍如何使用 `SimpleMailWebEventProvider` 类。

在 `Web.config` 文件中更新运行状况监视系统的 `<providers>` 元素，以包括 `SimpleMailWebEventProvider` 类的日志源：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample3.xml)]

上述标记使用 `SimpleMailWebEventProvider` 类作为日志源提供程序，并为其指定友好名称 "EmailWebEventProvider"。 此外，`<add>` 属性还包括附加的配置选项，如电子邮件的 "发件地址" 和 "发件地址"。

定义电子邮件日志源后，剩下的就是指示运行状况监视系统使用此源来 "记录" 未处理的异常。 这是通过在 `<rules>` 部分中添加新规则来完成的：

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-vb/samples/sample4.xml)]

`<rules>` 部分现在包括两个规则。 第一个名称为 "所有错误发至电子邮件"，将所有未经处理的异常发送到 "EmailWebEventProvider" 日志源。 此规则的效果是将网站上有关错误的详细信息发送到指定的以解决问题。 "对数据库的所有错误" 规则将错误详细信息记录到站点的数据库中。 因此，只要站点上出现未处理的异常，其详细信息就会记录到数据库中并发送到指定的电子邮件地址。

**图 2**显示访问 `Genre.aspx?ID=foo`时由 `SimpleMailWebEventProvider` 类生成的电子邮件。

[![](logging-error-details-with-asp-net-health-monitoring-vb/_static/image5.png)](logging-error-details-with-asp-net-health-monitoring-vb/_static/image4.png)

**图 2**：在电子邮件中发送错误详细信息  
（[单击以查看完全大小的映像](logging-error-details-with-asp-net-health-monitoring-vb/_static/image6.png)）

## <a name="summary"></a>总结

ASP.NET 运行状况监视系统旨在允许管理员监视已部署的 web 应用程序的运行状况。 展开某些操作时，将引发运行状况监视事件，例如当应用程序停止时、用户成功登录到站点时或发生未经处理的异常时。 这些事件可以记录到任意数量的日志源中。 本教程演示了如何通过电子邮件将未经处理的异常的详细信息记录到数据库中。

本教程重点介绍如何使用运行状况监视来记录未经处理的异常，但请记住，运行状况监视旨在衡量已部署的 ASP.NET 应用程序的总体运行状况，并包括大量的运行状况监视事件和日志源本文探讨。 而且，如果需要，你可以创建自己的运行状况监视事件和日志源。 如果有兴趣了解有关运行状况监视的详细信息，最好是通读[Erik Reitan](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)的[运行状况监视常见问题解答](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)。 请参阅[如何：在 ASP.NET 2.0 中使用运行状况监视](https://msdn.microsoft.com/library/ms998306.aspx)。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [ASP.NET 运行状况监视概述](https://msdn.microsoft.com/library/bb398933.aspx)
- [配置和自定义 ASP.NET 的运行状况监视系统](http://dotnetslackers.com/articles/aspnet/ConfiguringAndCustomizingTheHealthMonitoringSystemOfASPNET.aspx)
- [常见问题解答-ASP.NET 2.0 中的运行状况监视](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)
- [如何：发送用于运行状况监视通知的电子邮件](https://msdn.microsoft.com/library/ms227553.aspx)
- [如何：在 ASP.NET 中使用运行状况监视](https://msdn.microsoft.com/library/ms998306.aspx)
- [ASP.NET 中的运行状况监视](http://aspnet.4guysfromrolla.com/articles/031407-1.aspx)

> [!div class="step-by-step"]
> [上一页](processing-unhandled-exceptions-vb.md)
> [下一页](logging-error-details-with-elmah-vb.md)
