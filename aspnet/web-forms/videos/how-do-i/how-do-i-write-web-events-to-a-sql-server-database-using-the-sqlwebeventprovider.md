---
uid: web-forms/videos/how-do-i/how-do-i-write-web-events-to-a-sql-server-database-using-the-sqlwebeventprovider
title: '[如何实现：]使用 SqlWebEventProvider 将 Web 事件写入 SQL Server 数据库 |Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素演示了如何使用 ASP.NET 运行状况监视 SqlWebEventProvider 将网站中的错误记录到 SQL Server 数据库中。 首先，l 。
ms.author: riande
ms.date: 08/28/2008
ms.assetid: d4c08844-fe1c-4759-9ec7-66263ba678fb
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-write-web-events-to-a-sql-server-database-using-the-sqlwebeventprovider
msc.type: video
ms.openlocfilehash: 601da044c0c9679526eecaa09256e0100e7ad571
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517064"
---
# <a name="how-do-i-write-web-events-to-a-sql-server-database-using-the-sqlwebeventprovider"></a><span data-ttu-id="1010a-104">[如何实现：]使用 SqlWebEventProvider 将 Web 事件写入 SQL Server 数据库</span><span class="sxs-lookup"><span data-stu-id="1010a-104">[How Do I:] Write Web Events to a SQL Server Database Using the SqlWebEventProvider</span></span>

<span data-ttu-id="1010a-105">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="1010a-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="1010a-106">在此视频中，Chris 像素演示了如何使用 ASP.NET 运行状况监视 SqlWebEventProvider 将网站中的错误记录到 SQL Server 数据库中。</span><span class="sxs-lookup"><span data-stu-id="1010a-106">In this video Chris Pels shows how to use the ASP.NET health monitoring SqlWebEventProvider to log errors in a web site to a SQL Server database.</span></span> <span data-ttu-id="1010a-107">首先，了解 ASP.NET 运行状况监视中的提供程序和事件的角色。</span><span class="sxs-lookup"><span data-stu-id="1010a-107">First, learn the role of the provider and events in ASP.NET health monitoring.</span></span> <span data-ttu-id="1010a-108">接下来，请参阅如何配置 SQL Server 数据库，该数据库具有使用 aspnet\_regiis 实用工具记录运行状况监视事件的必要对象，这是用于配置 ASP.NET 成员身份的同一实用程序。</span><span class="sxs-lookup"><span data-stu-id="1010a-108">Next, see how to configure a SQL Server database with the necessary objects for recording health monitoring events using the aspnet\_regiis utility, the same utility used to configure ASP.NET Membership.</span></span> <span data-ttu-id="1010a-109">然后，了解如何在 web.config 文件中配置运行状况监视，以便将 ASP.NET 网站中的事件记录到新创建的 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="1010a-109">Then, learn how to configure health monitoring in the web.config file to record events in an ASP.NET web site to the newly created SQL Server database.</span></span> <span data-ttu-id="1010a-110">作为此配置的一部分，请参阅 .NET Framework 2.0 中的根 web.config 文件如何定义在配置运行状况监视时可以利用的提供程序和事件。</span><span class="sxs-lookup"><span data-stu-id="1010a-110">As part of this configuration, see how the root web.config file in the .NET Framework 2.0 has both providers and events defined that can be leveraged when configuring your health monitoring.</span></span> <span data-ttu-id="1010a-111">这些基础是创建自定义事件的基础，可将自己的特定信息记录到 ASP.NET 网站中的 SQL Server 数据库。</span><span class="sxs-lookup"><span data-stu-id="1010a-111">These fundamentals are a base upon which custom events can be created that log your own specific information to a SQL Server database in an ASP.NET web site.</span></span>

[<span data-ttu-id="1010a-112">&#9654;观看视频（31分钟）</span><span class="sxs-lookup"><span data-stu-id="1010a-112">&#9654; Watch video (31 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-write-web-events-to-a-sql-server-database-using-the-sqlwebeventprovider)
