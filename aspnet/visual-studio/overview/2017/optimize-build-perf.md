---
uid: visual-studio/overview/2017/optimize-build-perf
title: 优化解决方案的生成性能
author: AngelosP
description: 优化解决方案的生成性能
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050504"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="bcff7-103">优化解决方案的生成性能</span><span class="sxs-lookup"><span data-stu-id="bcff7-103">Optimize build performance for solution</span></span>

<span data-ttu-id="bcff7-104">Visual Studio 2017 15.8年或更高版本包括菜单项：**构建** > **ASP.NET 编译** > **优化解决方案的生成性能**。</span><span class="sxs-lookup"><span data-stu-id="bcff7-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![新的菜单项的屏幕截图](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="bcff7-106">ASP.NET 编译其视图在运行时，这意味着，在 ASP.NET 项目具有以来的编译器的副本。</span><span class="sxs-lookup"><span data-stu-id="bcff7-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="bcff7-107">但是开发人员计算机上的副本的编译器与 Visual Studio 的副本不匹配时生成性能会受到影响大约每个增量生成 1-3 秒。</span><span class="sxs-lookup"><span data-stu-id="bcff7-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="bcff7-108">此功能更新您的项目的副本以匹配 Visual Studio 的编译器，通常可加快增量生成。</span><span class="sxs-lookup"><span data-stu-id="bcff7-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="bcff7-109">**这适用于 ASP.NET Framework 4.7.1 或更高版本仅适用于项目，不适用于 ASP.NET Core。**</span><span class="sxs-lookup"><span data-stu-id="bcff7-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
