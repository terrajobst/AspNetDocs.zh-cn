---
uid: web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
title: '[如何实现：]将数据导出到应用程序（如 Excel）的逗号分隔（CSV）文件。Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素演示了如何从数据库或其他源获取数据，并将其导出到可在应用程序中使用的逗号分隔的文件 。
ms.author: riande
ms.date: 01/22/2009
ms.assetid: c9df86ad-aec2-43d5-bb8a-413ebb666673
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel
msc.type: video
ms.openlocfilehash: f27873eee345fe5347023b154de2b3833c9b6138
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78458066"
---
# <a name="how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel"></a><span data-ttu-id="f55a5-103">[如何实现：]将数据导出到 Excel 之类的应用程序的逗号分隔（CSV）文件</span><span class="sxs-lookup"><span data-stu-id="f55a5-103">[How Do I:] Export Data to a Comma Delimited (CSV) File for an Application Like Excel</span></span>

<span data-ttu-id="f55a5-104">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="f55a5-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="f55a5-105">在此视频中，Chris 像素演示了如何从数据库或其他源获取数据，并将其导出到可在 Excel 之类的应用程序中使用的逗号分隔文件。</span><span class="sxs-lookup"><span data-stu-id="f55a5-105">In this video Chris Pels shows how to take data from a database or other source and export it to a comma delimited file that can be used in an application like Excel.</span></span> <span data-ttu-id="f55a5-106">首先，将一组数据创建为 DataTable 对象。</span><span class="sxs-lookup"><span data-stu-id="f55a5-106">First, a set of data is created as a DataTable object.</span></span> <span data-ttu-id="f55a5-107">接下来，将清除当前网页请求的响应，并将标头和内容类型配置为 csv 文件。</span><span class="sxs-lookup"><span data-stu-id="f55a5-107">Next, the Response for the current web page request is cleared and the header and content type are configured to be a csv file.</span></span> <span data-ttu-id="f55a5-108">然后，通过首先写入 csv 文件的列标题，然后写入数据值，将实际数据添加到响应流。</span><span class="sxs-lookup"><span data-stu-id="f55a5-108">Then the actual data is added to the response stream by first writing the column headers for the csv file followed by the data values.</span></span> <span data-ttu-id="f55a5-109">当用户需要导出数据以便在 Excel 等程序中以本地方式操作时，此方法非常有用。</span><span class="sxs-lookup"><span data-stu-id="f55a5-109">This approach can be useful when users require an export of data so it can be manipulated locally in a program like Excel.</span></span>

[<span data-ttu-id="f55a5-110">&#9654;观看视频（19分钟）</span><span class="sxs-lookup"><span data-stu-id="f55a5-110">&#9654; Watch video (19 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-export-data-to-a-comma-delimited-csv-file-for-an-application-like-excel)
