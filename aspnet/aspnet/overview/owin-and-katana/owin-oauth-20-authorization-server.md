---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2.0 授权服务器 |Microsoft Docs
author: hongyes
description: 本教程将指导你了解如何使用 OWIN OAuth 中间件实现 OAuth 2.0 授权服务器。 这是一个高级教程，仅 outlin
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 39c78ee57f791a94af7a5fb66c3ac42d7239760f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500234"
---
# <a name="owin-oauth-20-authorization-server"></a>OWIN OAuth 2.0 授权服务器

使用[OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) ，第三方应用可以获得对 HTTP 服务的有限访问权限。 客户端不使用资源所有者的凭据来访问受保护的资源，而是获取一个访问令牌（表示特定范围、生存期和其他访问属性的字符串）。 授权服务器将访问令牌颁发给第三方客户端，并批准资源所有者。

OWIN 定义 .NET web 服务器和 web 应用程序之间的标准接口。 OWIN 接口的目标是将服务器和应用程序分离，鼓励开发简单的 .NET web 开发模块，并通过作为开放标准来鼓励 .NET web 开发工具的开源生态系统。

有关详细信息，请参阅[OWIN](http://owin.org/)
