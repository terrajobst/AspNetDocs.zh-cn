---
uid: webhooks/diagnostics/logging
title: ASP.NET Webhook 日志记录 |Microsoft Docs
author: rick-anderson
description: 如何在 ASP.NET Webhook 中进行日志记录。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: a05b32c4a8f9577bcf6170bd19a9e440b1aeb75b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457578"
---
# <a name="aspnet-webhooks-logging"></a>ASP.NET Webhook 日志记录

Microsoft ASP.NET Webhook 使用日志记录作为报告问题和问题的一种方式。 默认情况下，使用托管编写日志，使用[跟踪侦听器](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx)（如任何其他日志流）可以对其进行[。](https://msdn.microsoft.com/library/system.diagnostics.trace)

将 Web 应用程序部署为 Azure Web 应用时，将自动提取日志，并可将其与任何其他[诊断](https://msdn.microsoft.com/library/system.diagnostics.trace)日志记录一起进行管理。 有关详细信息，请参阅[在 Azure App Service 中启用 web 应用的诊断日志记录](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

此外，可以直接从 Visual Studio 内部获取日志，如[使用 Visual studio 在 Azure App Service 中对 web 应用进行故障排除](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)中所述。

## <a name="redirecting-logs"></a>重定向日志

可以提供可直接记录到日志管理器（例如[Log4Net](http://logging.apache.org/log4net/)和[NLog](http://nlog-project.org/)）的备用日志记录实现，而不是将日志[写入到 system.exception。](https://msdn.microsoft.com/library/system.diagnostics.trace) 只需提供[ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs)的实现，并将其注册到所选的依赖项注入引擎，并 Microsoft ASP.NET webhook 获取它。 有关详细信息，请参阅[ASP.NET Web API 2 中的依赖关系注入](https://www.asp.net/web-api/overview/advanced/dependency-injection)。
