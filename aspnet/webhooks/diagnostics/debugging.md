---
uid: webhooks/diagnostics/debugging
title: ASP.NET Webhook 调试 |Microsoft Docs
author: rick-anderson
description: 如何调试 ASP.NET Webhook。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520598"
---
# <a name="aspnet-webhooks-debugging"></a>ASP.NET Webhook 调试  

## <a name="debugging-in-azure"></a>在 Azure 中调试

若要在 Azure 中运行时调试你的 Web 应用程序，请参阅教程[使用 Visual Studio 在 Azure App Service 中对 web 应用进行故障排除](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)。

## <a name="debugging-with-source-and-symbols"></a>用源和符号进行调试

除了调试你自己的代码外，还可以直接调试到 Microsoft ASP.NET Webhook，实际上是所有 .NET。 无论是本地调试还是远程调试，此操作都有效。 首先，将 Visual Studio 配置为通过转到 "**调试**"，然后选择 "**选项和设置**" 来查找源和符号。 设置如下所示的选项：

![选项和设置](_static/SourceSymbols.png)

然后添加指向[symbolsource.org](http://symbolsource.org)的链接以下载源和符号。 中转到上面菜单的 "**符号**" 选项卡，并将以下内容添加为符号位置：

```
http://srv.symbolsource.org/pdb/Public
```

此外，请确保缓存目录具有短名称;否则，文件名可能会太长，导致无法加载符号。 示例路径为：

```
C:\SymCache
```

设置应如下所示：

![选项符号文件位置示例](_static/SymSource.png)
