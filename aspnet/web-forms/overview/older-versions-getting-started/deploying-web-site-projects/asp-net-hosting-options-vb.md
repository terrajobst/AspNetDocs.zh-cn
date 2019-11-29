---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-vb
title: ASP.NET 承载选项（VB） |Microsoft Docs
author: rick-anderson
description: ASP.NET web 应用程序通常在本地开发环境中设计、创建和测试，并需要部署到生产环境 o 。
ms.author: riande
ms.date: 04/01/2009
ms.assetid: 492f5ae2-bad7-4107-89a9-f04a9525dee7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/asp-net-hosting-options-vb
msc.type: authoredcontent
ms.openlocfilehash: 4293114002aee15ddace1a3f19c240f35e6065f5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620761"
---
# <a name="aspnet-hosting-options-vb"></a>ASP.NET 托管选项 (VB)

作者： [Scott Mitchell](https://twitter.com/ScottOnWriting)

[下载 PDF](https://download.microsoft.com/download/E/8/9/E8920AE6-D441-41A7-8A77-9EF8FF970D8B/aspnet_tutorial01_Basics_vb.pdf)

> ASP.NET web 应用程序通常在本地开发环境中设计、创建和测试，并在准备好发布后，需要部署到生产环境中。 本教程提供了部署过程的高级概述，并提供了本系列教程的简介。

## <a name="introduction"></a>简介

通常，Web 应用程序在开发环境中设计、创建和测试，只能供在站点上工作的程序员访问。 在应用程序准备好进行发布后，会将其移动到可以由 Internet 上的任何人访问的生产环境中。 此部署过程带来了很多挑战：

- 生产环境必须存在并正确设置，然后才能部署 ASP.NET 应用程序;此外，生产环境必须与最新的安全修补程序保持同步。
- 必须将正确的标记文件、代码文件和支持文件集从开发环境复制到生产环境。 对于数据驱动的应用程序，这可能还需要复制数据库架构和/或数据。
- 这两种环境之间可能存在配置差异。 开发环境中使用的数据库连接字符串或电子邮件服务器可能与生产环境不同。 而且，应用程序的行为可能取决于环境。 例如，在开发过程中发生错误时，可以在屏幕上显示错误的详细信息，但在生产中发生错误时，应改为显示用户友好的错误页，并通过电子邮件将错误详细信息发送给开发人员。

这样就不第一次挑战-设置和维护生产环境-许多个人和企业将其生产环境外包给*web 托管提供商*。 Web 托管提供商是指代表您管理生产环境的公司。 有无数个 web 主机提供商，每个都有不同的价格和服务级别;有关查找此类服务提供程序的提示，请参阅 "查找 Web 宿主提供程序" 一节。

这是一系列教程中的第一篇教程，其中介绍了将 ASP.NET web 应用程序部署到由 web 主机提供商管理的生产环境中所涉及的步骤。 在这些教程中，我们将检查：

- 需要将哪些文件部署到 web 宿主提供程序。
- 简化部署过程的工具。
- 如何部署数据库。
- 有关部署使用[基于 SQL 的成员资格和角色提供程序](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md)的数据库的技巧，以及在生产环境中模拟网站管理工具的方法。
- 在开发过程中进行的更改，用于在生产环境中流畅地更新数据库的策略。
- 用于记录在生产中发生的错误的方法，以及在发生错误时通知开发人员的方式。

这些教程非常简单，并且提供了许多屏幕截图的分步说明，可帮助你直观地完成此过程。 本便捷性教程提供了 ASP.NET 部署过程的概述，以及有关查找 web 托管提供程序的建议。 让我们进入正题！

## <a name="an-overview-of-the-aspnet-deployment-process"></a>ASP.NET 部署过程概述

简而言之，部署 ASP.NET 应用程序需要执行以下三个步骤：

1. 在生产环境中配置 web 应用程序、web 服务器和数据库。
2. 同步 ASP.NET 页、代码文件、`Bin` 文件夹中的程序集和与 HTML 相关的支持文件（如 CSS 和 JavaScript 文件）。
3. 同步数据库架构和/或数据。

Web 应用程序的配置信息通常位于 `Web.config` 文件中，其中包括数据库连接字符串、错误处理条件、URL 重写规则和电子邮件服务器信息。 对于开发中的应用程序与生产环境中的应用程序，此信息通常是不同的。 例如，在开发应用程序时，最好使用开发数据库，这样就不会针对生产数据库进行测试。 因此，数据库连接字符串通常在开发和生产应用程序之间有所不同。 由于这些差异，部署的一部分涉及到更改 web 应用程序的配置信息。

除了 web 应用程序配置更改之外，步骤1还可能需要对 web 服务器和数据库进行配置。 例如，如果 ASP.NET 页面在 web 服务器上的目录中创建或删除文件，则需要将 web 服务器配置为允许这些文件系统修改。 同样，可能有需要对数据库进行的权限或身份验证设置。

步骤2涉及在开发和生产环境之间同步一组基本的 ASP.NET 页和支持文件。 需要在两个环境之间同步的一组特定的 ASP.NET 相关文件取决于你在 Visual Studio 中创建的项目的类型，在下一教程中，<em>[确定需要部署哪些文件](determining-what-files-need-to-be-deployed-vb.md)</em>。 第三个和第四个教程-<em>[使用 FTP 部署网站](deploying-your-site-using-an-ftp-client-vb.md)</em>和<em>[使用 Visual Studio 部署网站](deploying-your-site-using-visual-studio-vb.md)</em>-查看同步这些文件的不同工具和技术。

构建数据驱动的应用程序时，通常会使用两个数据库：一个数据库用于开发，另一个用于生产。 在开发过程中，可能会修改开发数据库的架构以包含新表、列、存储过程和触发器，或者可以修改它们以删除或重命名现有数据库对象。 在进行这些更改的时间和将应用程序部署到生产环境之间的时间之间，开发和生产数据库不同步。在部署过程中，需要修复此异步。 以后的教程中会检查这些挑战。

## <a name="finding-a-web-host-provider"></a>查找 Web 宿主提供程序

可以将 ASP.NET 应用程序部署到安装了 .NET Framework 和 Internet Information Services （IIS）的任何 web 服务器。 假设你有到 Internet 的宽带连接，并且知道如何将路由器配置为允许传入的 web 请求，则可以从个人计算机托管站点。 你还可以在 intranet 上托管某个计算机，就像许多公司一样。 不过，这些教程的重点是使用 web 主机提供商托管你的网站。

> [!NOTE]
> [IIS](https://www.iis.net/)是 Microsoft 的企业级 web 服务器。 它附带 windows 的非 Home 版本，如 Windows Server 2008 和某些版本的 Windows Vista。 在开发环境中，不需要安装 IIS 来提供 ASP.NET 应用程序，因为 Visual Studio 包括 ASP.NET 开发 Web 服务器。 但是，ASP.NET 开发 Web 服务器仅接受本地连接，因此不能在生产环境中使用。

在将网站部署到 web 主机提供程序之前，必须首先确定要使用哪种公司来处理业务。 Marketplace 中有无数的 web 托管公司;搜索 "web 托管公司" 时返回的结果超过5000000。 如何找到适合你的情况？ 你最喜欢的搜索引擎是一个不错的开端，就像[TopHosts](http://www.tophosts.com/)和[HostCritique](http://www.hostcritique.net/)之类的网站，它比较和对比各种托管服务。 我还建议向您的同事和同事提出任何建议;你还可以在[ASP.NET 论坛](https://forums.asp.net/)上的[托管开放论坛](https://forums.asp.net/158.aspx)上提出建议。

Web 托管公司通常提供共享的托管计划和专用的托管计划。 使用共享托管时，如果不是数百个不同的网站，则承载数十个 web 服务器。 借助专用托管，你可以从公司租赁计算机，该计算机只为你的站点和站点提供服务。 共享托管计划可能包括对 ASP.NET 页的支持、使用 Microsoft Access 数据库的功能、5 GB 磁盘空间和每月 $9.95 的每月带宽流量 100 GB。 其他共享的托管计划可能包括对 ASP.NET 页的支持、对 Microsoft SQL Server 2008 数据库服务器的访问、每月 10 GB 的磁盘空间和 250 GB 的每月带宽流量（每月 $19.95）。 专用的托管计划通常成本更高，每月计费100美元，但提供比共享托管选项更好的性能和更多控制。 选择哪种计划取决于预算、网站收到的流量以及预计需要的功能。

选择 web 主机提供商时，有两个重要的注意事项是客户服务和服务质量。 如果遇到问题或配置问题，需要多长时间才能将问题提交给 web 主机的支持人员，直到收到响应？ 公司服务的可靠性如何？ 它们是否经常停止数据库？ 电子邮件服务器脱机的频率如何？ 你始终可以要求公司提供有关其正常运行时间和查询其客户服务策略的详细信息，但更 surefire 的方法是征求当前和过去的客户的反馈，你可以通过在线论坛、新闻组和电子邮件 listservs.

> [!NOTE]
> 某些 web 宿主公司将其业务集中在特定的技术堆栈上，如 .NET[或灯泡](http://en.wikipedia.org/wiki/LAMP_stack)（**L** Inux **、Pache** 、 **M** ySQL 和**P** HP），因此请确保选择的公司托管 ASP.NET 应用程序。 另外，请检查以确保它们支持用于生成应用程序的 ASP.NET 版本。 如果要构建数据驱动的应用程序，请确保 web 主机提供了所用的相同数据库服务器和版本。

## <a name="summary"></a>总结

ASP.NET web 应用程序通常在本地开发环境中设计、创建和测试。 版本准备好发布后，将移到生产环境。 尽管可以在个人计算机或公司内的服务器上托管 ASP.NET 网站，但许多企业和个人都选择将其托管外包给 web 主机提供商。

本系列教程将介绍将 ASP.NET 应用程序部署到 web 主机提供程序的步骤，探讨常见的难题。 本教程提供了 ASP.NET 部署过程的高级概述，并提供了查找合适的 web 宿主提供程序的提示。 下一教程将介绍在部署网站时需要将哪些 ASP.NET 相关文件复制到生产环境中。

很高兴编程！

### <a name="special-thanks-to"></a>特别感谢 。

此教程系列由许多有用的审阅者查看。 本教程的主管审查人员是 Teresa Murphy。 想要查看我即将发布的 MSDN 文章？ 如果是这样，请在[mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)放置一行。

> [!div class="step-by-step"]
> [上一页](users-and-roles-on-the-production-website-cs.md)
> [下一页](determining-what-files-need-to-be-deployed-vb.md)
