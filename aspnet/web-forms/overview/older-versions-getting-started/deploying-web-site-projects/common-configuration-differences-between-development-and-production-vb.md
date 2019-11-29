---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
title: 开发和生产之间的常见配置差异（VB） |Microsoft Docs
author: rick-anderson
description: 在前面的教程中，我们通过将所有相关文件从开发环境复制到生产环境来部署我们的网站。 但是，我 。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 548e75f6-4d6c-4cb4-8da8-417915eb8393
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-vb
msc.type: authoredcontent
ms.openlocfilehash: cc65af6eb4fca8b3b805e11e26da468a958a4221
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619954"
---
# <a name="common-configuration-differences-between-development-and-production-vb"></a>开发和生产之间的常见配置差异 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial05_ConfigDifferences_vb.pdf)

> 在前面的教程中，我们通过将所有相关文件从开发环境复制到生产环境来部署我们的网站。 但是，环境之间的配置差异很少，这就要求每个环境都有一个唯一的 Web.config 文件。 本教程检查典型的配置差异，并查看用于维护单独配置信息的策略。

## <a name="introduction"></a>简介

最后两个教程介绍了如何部署简单的 web 应用程序。 [*使用 FTP 客户端部署站点*](deploying-your-site-using-an-ftp-client-vb.md)教程介绍了如何使用独立的 ftp 客户端将开发环境中所需的文件复制到生产环境中。 前面的教程[*使用 Visual Studio 部署网站*](deploying-your-site-using-visual-studio-vb.md)，并使用 visual studio 的 "复制网站" 工具和 "发布" 选项进行部署。 在两个教程中，生产环境中的每个文件都是开发环境中的文件的副本。 但是，生产环境中的配置文件与开发环境中的配置文件不同，这种情况并不常见。 Web 应用程序的配置存储在 `Web.config` 文件中，通常包括有关外部资源（例如数据库、web 和电子邮件服务器）的信息。 它还在某些情况下（例如，在发生未经处理的异常时要执行的操作过程）来拼写应用程序的行为。

在部署 web 应用程序时，正确的配置信息会在生产环境中结束，这一点很重要。 在大多数情况下，不能按原样将开发环境中的 `Web.config` 文件复制到生产环境中。 相反，需要将自定义版本的 `Web.config` 上载到生产。 本教程简要回顾一些更常见的配置差异;它还汇总了一些在环境之间维护不同配置信息的方法。

## <a name="typical-configuration-differences-between-the-development-and-production-environments"></a>开发环境与生产环境之间的典型配置差异

`Web.config` 文件包括 ASP.NET 应用程序的一种配置信息。 不管环境如何，其中的某些配置信息都是相同的。 例如，无论环境如何，在 `Web.config` 文件的 `<authentication>` 和 `<authorization>` 元素中拼写的身份验证设置和 URL 授权规则都是相同的。 但其他配置信息（如有关外部资源的信息）通常因环境而异。

数据库连接字符串是根据环境不同的配置信息的一个典型示例。 当 web 应用程序与数据库服务器通信时，它必须首先建立一个连接，并通过[连接字符串](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)实现该连接。 尽管可以在网页或连接到数据库的代码中直接对数据库连接字符串进行硬编码，但最好将其放置 `Web.config`的[`<connectionStrings>` 元素](https://msdn.microsoft.com/library/bf7sd233.aspx)，以便连接字符串信息位于单个集中位置。 开发期间通常使用不同的数据库，而不是在生产环境中使用;因此，每个环境的连接字符串信息必须是唯一的。

> [!NOTE]
> 以后的教程会探讨如何部署数据驱动的应用程序，此时我们将深入探讨如何将数据库连接字符串存储在配置文件中。

开发和生产环境的预期行为明显不同。 开发环境中的 web 应用程序由一小组开发人员创建、测试和调试。 在生产环境中，许多不同的用户同时访问同一应用程序。 ASP.NET 包括许多功能，可帮助开发人员测试和调试应用程序，但在生产环境中，应禁用这些功能以提高性能和安全性。 让我们看看几个这样的配置设置。

### <a name="configuration-settings-that-impact-performance"></a>影响性能的配置设置

当首次访问 ASP.NET 页面时（或首次访问该页面后），必须将其声明性标记转换为类，并且必须编译此类。 如果 web 应用程序使用自动编译，则还需要编译该页的代码隐藏类。 可以通过 `Web.config` 文件的[`<compilation>` 元素](https://msdn.microsoft.com/library/s10awwz0.aspx)来配置一分类编译选项。

Debug 特性是 `<compilation>` 元素中最重要的属性之一。 如果 `debug` 特性设置为 "true"，则已编译的程序集包含调试符号，调试符号在 Visual Studio 中调试应用程序时需要用到。 但调试符号会增加程序集的大小，并在运行代码时增加额外的内存需求。 此外，当 `debug` 特性设置为 "true" 时，不缓存 `WebResource.axd` 返回的任何内容，这意味着每次用户访问某个页面时，他们将需要重新下载 `WebResource.axd`返回的静态内容。

> [!NOTE]
> `WebResource.axd` 是在 ASP.NET 2.0 中引入的内置 HTTP 处理程序，服务器控件使用它来检索嵌入的资源，如脚本文件、图像、CSS 文件和其他内容。 若要详细了解 `WebResource.axd` 的工作原理以及如何使用它从自定义服务器控件访问嵌入的资源，请参阅[使用 `WebResource.axd`通过 URL 访问嵌入的资源](http://aspnet.4guysfromrolla.com/articles/080906-1.aspx)。

在开发环境中，`<compilation>` 元素的 `debug` 属性通常设置为 "true"。 事实上，若要调试 web 应用程序，必须将此属性设置为 "true";如果尝试从 Visual Studio 中调试 ASP.NET 应用程序，并且 `debug` 特性设置为 "false"，则 Visual Studio 将显示一条消息，说明在将 `debug` 属性设置为 "true" 之前无法调试应用程序，并将为您提供此更改。

不应在生产环境中将 `debug` 特性设置为 "true"，因为它**会**对性能造成影响。 有关本主题的更多详细讨论，请参阅[Scott Guthrie](https://weblogs.asp.net/scottgu/)的博客文章，[不要在启用 `debug="true"` 的情况下运行生产 ASP.NET 应用程序](https://weblogs.asp.net/scottgu/442448)。

### <a name="custom-errors-and-tracing"></a>自定义错误和跟踪

当 ASP.NET 应用程序中发生未经处理的异常时，它将冒泡到运行时，此时将发生以下三种情况之一：

- 显示一般运行时错误消息。 本页通知用户出现了运行时错误，但未提供有关错误的任何详细信息。
- 将显示异常详细信息消息，其中包含有关刚刚引发的异常的信息。
- 此时将显示自定义错误页，这是你创建的 ASP.NET 页面，用于显示你需要的任何消息。

出现未经处理的异常时，会发生什么情况取决于 `Web.config` 文件的[`<customErrors>` 部分](https://msdn.microsoft.com/library/h0hfz6fc.aspx)。

开发和测试应用程序时，它有助于在浏览器中查看任何异常的详细信息。 但是，在生产环境中显示异常详细信息可能会带来安全风险。 此外，它还 unflattering，并使网站 unprofessional。 理想情况下，在发生未经处理的异常的情况下，开发环境中的 web 应用程序将显示异常的详细信息，而生产中的同一应用程序将显示自定义错误页。

> [!NOTE]
> 默认 `<customErrors>` 节设置仅在通过 localhost 访问页面时显示异常详细信息消息，否则显示 "一般运行时错误" 页。 这并不理想，但需要知道，默认行为不会向非本地访问者显示异常详细信息。 以后的教程将更详细地研究 `<customErrors>` 部分，并演示如何在生产中发生错误时显示自定义错误页。

在开发过程中非常有用的另一 ASP.NET 功能是跟踪。 如果启用跟踪，则会记录每个传入请求的相关信息，并提供一个用于查看最近请求详细信息的特殊网页 `Trace.axd`。 您可以通过 `Web.config`中的[`<trace>` 元素](https://msdn.microsoft.com/library/6915t83k.aspx)打开和配置跟踪。

如果启用跟踪，请确保在生产环境中禁用跟踪。 由于跟踪信息包括 cookie、会话数据和其他可能的敏感信息，因此在生产中禁用跟踪非常重要。 好消息是，默认情况下禁用跟踪功能，只能通过 localhost 访问 `Trace.axd` 文件。 如果在开发中更改这些默认设置，请确保它们在生产环境中处于禁用状态。

## <a name="techniques-for-maintaining-separate-configuration-information"></a>用于维护单独的配置信息的技术

开发和生产环境中具有不同的配置设置会使部署过程复杂化。 在前两个教程中，部署过程涉及到将所有必需的文件复制到生产环境中，但这种方法仅适用于两种环境中的配置信息相同的情况。 有多种方法可用于部署具有不同配置信息的应用程序。 让我们为托管的 web 应用程序编目其中一些选项。

### <a name="manually-deploying-the-production-environment-configuration-file"></a>手动部署生产环境配置文件

最简单的方法是维护 `Web.config` 文件的两个版本：一个用于开发环境，另一个用于生产环境。 将站点部署到生产环境中，需要将所有文件复制到开发环境中的生产服务器（`Web.config` 文件*除外*）。 相反，特定于生产环境的 `Web.config` 文件将复制到生产环境中。

这种方法并不是非常复杂，但很容易实现，因为配置信息的更改不频繁。 它最适用于具有小型开发团队的应用程序，这些应用程序托管在单个 web 服务器上，并且不经常更改其配置信息。 使用独立 FTP 客户端手动部署应用程序文件时，这是最 tenable 的。 使用 Visual Studio 的 "复制网站" 工具或 "发布" 选项时，需要先使用特定于生产的 `Web.config` 文件，然后再进行部署，然后在部署完成后将这些文件交换回来。

### <a name="change-the-configuration-during-the-build-or-deployment-process"></a>在生成或部署过程中更改配置

到目前为止，讨论已采用即席生成和部署过程。 许多较大的软件项目都具有更好的形式，使用开源、家庭发展或第三方工具。 对于此类项目，你可能会自定义生成或部署过程，以便在将配置信息推送到生产环境之前对其进行适当的修改。 如果使用[MSBuild](http://en.wikipedia.org/wiki/MSBuild)、 [NAnt](http://nant.sourceforge.net/)或其他某个生成工具生成 web 应用程序，则可能会添加一个生成步骤来修改 `Web.config` 文件，以包含特定于生产的设置。 或者，您的部署工作流可以通过编程方式连接到源代码管理服务器并检索相应的 `Web.config` 文件。

根据您的工具和工作流，将适当的配置信息提供给生产的实际方法发生了很大的变化。 因此，我们不会进一步深入探讨本主题。 如果你使用的是 MSBuild 或 NAnt 等常用的生成工具，则可以通过 web 搜索查找特定于这些工具的部署文章和教程。

### <a name="managing-configuration-differences-via-the-web-deployment-project-add-in"></a>通过 Web 部署项目外接程序管理配置差异

在2006中，Microsoft 发布了用于 Visual Studio 2005 的 Web 开发项目外接程序。 Visual Studio 2008 的外接程序已在2008中发布。 使用此外接程序，ASP.NET 开发人员可以创建单独的 Web 部署项目，并在生成时显式编译 web 应用程序并将文件复制到本地输出目录。 Web 应用程序项目在幕后使用 MSBuild。

默认情况下，开发环境的 `Web.config` 文件复制到输出目录中，但你可以设置 Web 部署项目以自定义

通过以下方式复制到此目录的配置信息：

- 通过 `Web.config` 文件部分替换，其中指定要替换的部分以及包含替换文本的 XML 文件。
- 提供外部配置源文件的路径。 选中此选项后，Web 部署项目会将特定 `Web.config` 文件复制到输出目录（而不是开发环境中使用的 `Web.config` 文件）。
- 通过将自定义规则添加到 Web 部署项目使用的 MSBuild 文件。

若要部署 web 应用程序，请生成 Web 部署项目，然后将文件从项目的输出文件夹复制到生产环境。

若要了解有关使用 Web 部署项目的详细信息，请参阅[MSDN 杂志](https://msdn.microsoft.com/magazine/default.aspx)2007 年4月版中的 "[此 web 部署项目](https://msdn.microsoft.com/magazine/cc163448.aspx)" 一文，或查阅本教程末尾的其他阅读部分中的链接。

> [!NOTE]
> 不能将 Web 部署项目与 Visual Web Developer 一起使用，因为 Web 部署项目是作为 Visual Studio 外接程序实现的，而 Visual Studio Express 版本（包括 Visual Web Developer）不支持外接程序。

## <a name="summary"></a>总结

开发中的 web 应用程序的外部资源和行为通常不同于生产中的同一应用程序。 例如，在发生未经处理的异常时，数据库连接字符串、编译选项和行为通常在环境之间有所不同。 部署过程必须满足这些差异。 如本教程中所述，最简单的方法是将备用配置文件手动复制到生产环境。 当使用 Web 部署项目外接程序时，或者使用可容纳此类自定义项的更规范化的生成或部署过程时，可以使用更优雅的解决方案。

很高兴编程！

### <a name="further-reading"></a>其他阅读材料

有关本教程中讨论的主题的详细信息，请参阅以下资源：

- [说明的连接字符串](http://www.connectionstrings.com/Articles/Show/what-is-a-connection-string)
- [数据库连接字符串 @ ConnectionStrings.com](http://www.connectionstrings.com/)
- [请勿在启用 `debug="true"` 的情况中运行生产 ASP.NET 应用程序](https://weblogs.asp.net/scottgu/Don_1920_t-run-production-ASP.NET-Applications-with-debug_3D001D20_true_1D20_-enabled)
- [正确响应未处理的异常-显示用户友好的错误页](http://aspnet.4guysfromrolla.com/articles/090606-1.aspx)
- [如何实现：使用 Visual Studio 2008 Web 部署项目？](../../../videos/how-do-i/how-do-i-use-a-visual-studio-2008-web-deployment-project.md)
- [部署数据库时的密钥配置设置](http://aspnet.4guysfromrolla.com/articles/121008-1.aspx)
- [Visual studio 2008 Web 部署项目下载](https://www.microsoft.com/downloads/details.aspx?FamilyId=0AA30AE8-C73B-4BDD-BB1B-FE697256C459&amp;displaylang=en) | [Visual Studio 2005 Web 部署项目下载](https://download.microsoft.com/download/9/4/9/9496adc4-574e-4043-bb70-bc841e27f13c/WebDeploymentSetup.msi)
- 已发布[vs 2008](https://weblogs.asp.net/scottgu/archive/2005/11/06/429723.aspx) Web 部署[项目 | Vs 2008 Web 部署项目支持](https://weblogs.asp.net/scottgu/archive/2008/01/28/vs-2008-web-deployment-project-support-released.aspx)
- [Web 部署项目](https://msdn.microsoft.com/magazine/cc163448.aspx)

> [!div class="step-by-step"]
> [上一页](deploying-your-site-using-visual-studio-vb.md)
> [下一页](core-differences-between-iis-and-the-asp-net-development-server-vb.md)
