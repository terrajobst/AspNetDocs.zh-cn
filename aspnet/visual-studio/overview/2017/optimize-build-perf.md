---
uid: visual-studio/overview/2017/optimize-build-perf
title: 优化解决方案的生成性能
author: AngelosP
description: 优化解决方案的生成性能
ms.author: riande
ms.date: 08/29/2018
msc.type: authoredcontent
ms.openlocfilehash: c1a5cf5e59374b4c0dd7150c5dd62fbde42af555
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504974"
---
# <a name="optimize-build-performance-for-solution"></a><span data-ttu-id="c1939-103">优化解决方案的生成性能</span><span class="sxs-lookup"><span data-stu-id="c1939-103">Optimize build performance for solution</span></span>

<span data-ttu-id="c1939-104">Visual Studio 2017 15.8 或更高版本包含菜单项：**生成** > **ASP.NET 编译** > **优化解决方案的生成性能**。</span><span class="sxs-lookup"><span data-stu-id="c1939-104">Visual Studio 2017 15.8 or later include a menu item: **Build** > **ASP.NET Compilation** > **Optimize Build Performance for Solution**.</span></span>

![新菜单项的屏幕截图](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

<span data-ttu-id="c1939-106">ASP.NET 在运行时编译其视图，这意味着 ASP.NET 项目随编译器一起提供编译器的副本。</span><span class="sxs-lookup"><span data-stu-id="c1939-106">ASP.NET compiles its views at runtime, which means that an ASP.NET project carries with it a copy of the compiler.</span></span> <span data-ttu-id="c1939-107">但在开发人员计算机上，当编译器副本与 Visual Studio 的副本不匹配时，生成性能将受每个增量生成1-3 秒的顺序的影响。</span><span class="sxs-lookup"><span data-stu-id="c1939-107">However on a developer machine when the copy of the compiler doesn't match Visual Studio's copy, build performance is impacted on the order of 1-3 seconds per incremental build.</span></span> <span data-ttu-id="c1939-108">此功能将更新你的项目的编译器副本以匹配 Visual Studio 的，这通常会加速增量生成。</span><span class="sxs-lookup"><span data-stu-id="c1939-108">This feature updates your project's copy of the compiler to match Visual Studio's, which usually speeds up incremental builds.</span></span>

<span data-ttu-id="c1939-109">**这仅适用于 ASP.NET Framework 4.7.1 或更高版本的项目，不适用于 ASP.NET Core。**</span><span class="sxs-lookup"><span data-stu-id="c1939-109">**This is applicable to ASP.NET Framework 4.7.1 or later projects only, it does not apply to ASP.NET Core.**</span></span>
