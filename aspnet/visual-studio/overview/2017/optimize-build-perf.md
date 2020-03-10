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
# <a name="optimize-build-performance-for-solution"></a>优化解决方案的生成性能

Visual Studio 2017 15.8 或更高版本包含菜单项：**生成** > **ASP.NET 编译** > **优化解决方案的生成性能**。

![新菜单项的屏幕截图](optimize-build-perf/_static/optimize-build-performance-for-solution.png)

ASP.NET 在运行时编译其视图，这意味着 ASP.NET 项目随编译器一起提供编译器的副本。 但在开发人员计算机上，当编译器副本与 Visual Studio 的副本不匹配时，生成性能将受每个增量生成1-3 秒的顺序的影响。 此功能将更新你的项目的编译器副本以匹配 Visual Studio 的，这通常会加速增量生成。

**这仅适用于 ASP.NET Framework 4.7.1 或更高版本的项目，不适用于 ASP.NET Core。**
