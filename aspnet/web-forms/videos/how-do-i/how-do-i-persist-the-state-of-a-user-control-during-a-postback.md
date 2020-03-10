---
uid: web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
title: '[How Do I]: Persist the State of a User Control During a Postback | Microsoft Docs'
author: rick-anderson
description: 在此视频中，Chris 像素介绍如何保存用户控件中一个或多个对象的状态。 首先，创建一个表示 abilit 的用户控件 。
ms.author: riande
ms.date: 04/02/2009
ms.assetid: d1bca4c6-838c-40f7-87ec-80bb67e483e5
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-persist-the-state-of-a-user-control-during-a-postback
msc.type: video
ms.openlocfilehash: c87bd6c5c993a1bde8f8a84f6d53b431e54541d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516272"
---
# <a name="how-do-i-persist-the-state-of-a-user-control-during-a-postback"></a><span data-ttu-id="dd444-103">[如何实现]：在回发期间保留用户控件的状态</span><span class="sxs-lookup"><span data-stu-id="dd444-103">[How Do I]: Persist the State of a User Control During a Postback</span></span>

<span data-ttu-id="dd444-104">作者： [Chris 像素](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="dd444-104">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="dd444-105">在此视频中，Chris 像素介绍如何保存用户控件中一个或多个对象的状态。</span><span class="sxs-lookup"><span data-stu-id="dd444-105">In this video Chris Pels shows how to persist the state of one or more objects in a user control.</span></span> <span data-ttu-id="dd444-106">首先，创建一个用户控件，该控件表示用户为搜索指定筛选条件的能力。</span><span class="sxs-lookup"><span data-stu-id="dd444-106">First, a user control is created that represents the ability for a user to specify filter criteria for a search.</span></span> <span data-ttu-id="dd444-107">此外，还创建了一个用于存储筛选器信息的伴随筛选器类。</span><span class="sxs-lookup"><span data-stu-id="dd444-107">In addition, a companion Filter class is created to store the filter information.</span></span> <span data-ttu-id="dd444-108">多个用户界面元素将添加到筛选器控件中，同时还添加了一些方法和属性，用于在筛选器类实例中存储当前筛选器信息。</span><span class="sxs-lookup"><span data-stu-id="dd444-108">Several user interface elements are added to the filter control along with some methods and properties to store the current filter information in the Filter class instance.</span></span> <span data-ttu-id="dd444-109">接下来，使用 RegisterRequiresControlState 方法和关联的保存/还原方法实现用户控件持久性。</span><span class="sxs-lookup"><span data-stu-id="dd444-109">Next, the user control persistence is implemented using the RegisterRequiresControlState method and associated Save/Restore methods.</span></span> <span data-ttu-id="dd444-110">这些方法在页回发过程中存储筛选器类及其数据的实例。</span><span class="sxs-lookup"><span data-stu-id="dd444-110">These methods store the instance of the filter class and its data during page postbacks.</span></span> <span data-ttu-id="dd444-111">最后，还讨论了如何在控件状态实现中存储多个对象。</span><span class="sxs-lookup"><span data-stu-id="dd444-111">Finally, there is a discussion of how to store multiple objects in control state implementation.</span></span>

[<span data-ttu-id="dd444-112">&#9654;观看视频（23分钟）</span><span class="sxs-lookup"><span data-stu-id="dd444-112">&#9654; Watch video (23 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-persist-the-state-of-a-user-control-during-a-postback)
