---
uid: webhooks/receiving/dependencies
title: ASP.NET Webhook 接收方依赖项 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 中的接收方依赖关系和依赖关系注入。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517526"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET Webhook 接收方依赖项

Microsoft ASP.NET Webhook 旨在考虑依赖项注入。 使用依赖关系注入引擎，可以将系统中的大多数依赖项替换为替代实现。

有关接收方依赖项的列表，请参阅[DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 。 如果尚未注册任何依赖项，则使用默认实现。 有关默认实现的列表，请参阅[ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 。
