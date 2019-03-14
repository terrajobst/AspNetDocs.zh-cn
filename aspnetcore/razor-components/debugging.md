---
title: 调试 Razor 组件
author: guardrex
description: 了解如何调试 Blazor 和 Razor 组件应用程序。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/debug
ms.openlocfilehash: fb7ddcf3ae40ec28a372adf724a293b375be28a1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034114"
---
# <a name="debug-razor-components"></a>调试 Razor 组件

[Daniel Roth](https://github.com/danroth27)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Razor 组件具有一些*很早*对调试上 WebAssembly 在 Chrome 中运行的客户端 Blazor 应用的支持。 虽然此初始的调试支持是非常有限的并且未磨光，它显示了集合在一起的基本调试基础结构。

若要调试在 Chrome 中的客户端 Blazor 应用：

* 生成 Blazor 应用`Debug`配置 （未发布应用程序的默认值）。
* 在 Chrome （版本 70 或更高版本） 中运行 Blazor 应用。
* 具有键盘焦点 （而不是在开发人员工具面板，您可能应关闭不太令人困惑的调试体验） 的应用上，选择以下特定于 Blazor 的键盘快捷方式：
  * `Shift+Alt+D` Windows/Linux 上
  * `Shift+Cmd+D` 在 macOS 上

启用调试 Blazor 应用远程调试运行 Chrome。 如果禁用远程调试，则由 Chrome 生成一个错误页面。 错误页包含有关运行 Chrome 调试端口打开，以便 Blazor 调试代理可以连接到该应用程序的说明。 *关闭所有 Chrome 实例*并重启 Chrome 所述。

![Blazor 调试错误页](https://user-images.githubusercontent.com/1874516/43123091-01ec0796-8ed8-11e8-844c-23b4e6e9d069.png)

Chrome 开始运行后启用远程调试，调试键盘快捷方式将打开一个新的调试器选项卡。片刻之后，*源*选项卡显示在应用程序的.NET 程序集列表。 展开每个程序集并查找 *.cs*/*.cshtml*源文件可用于调试。 设置断点，切换回应用的选项卡上和断点被命中。 断点后命中，单步执行 (`F10`) 或恢复 (`F8`) 通常情况下。

![Blazor 调试](https://user-images.githubusercontent.com/1874516/43123060-efb0b3b0-8ed7-11e8-9ea5-97aa34247a0b.png)

Blazor 提供调试代理实现[Chrome DevTools 协议](https://chromedevtools.github.io/devtools-protocol/)和增加内容使用的协议。特定于 NET 的信息。 按下调试键盘快捷方式时，Blazor 点 Chrome DevTools 在代理处。 代理连接到您没有找到要调试的浏览器窗口 (因此需要启用远程调试)。

您可能想知道为什么我们不只是使用浏览器源映射。 源映射允许浏览器将已编译的文件映射回其原始的源文件。 但是，Blazor 不映射C#直接向 JS/WASM （至少还没有）。 相反，Blazor 会在浏览器中的 IL 解释，因此源映射不相关。

请注意，调试器功能**非常有限**。 当前仅可：

* 设置和删除断点。
* 单步执行代码或恢复 (`F8`)。
* 在中*局部变量*显示中，类型的任何本地变量的值`int`， `string`，和`bool`。
* 查看调用堆栈，包括转到 JavaScript 的从.NET 到 JavaScript 和.NET 的调用链。

您*不能*:

* 观察的值不是任何局部变量`int`， `string`，或`bool`。
* 观察到的任何类属性或字段的值。
* 若要查看其值的变量将鼠标悬停
* 计算在控制台中的表达式。
* 单步执行异步调用。
* 执行大多数其他普通调试方案。

开发的进一步调试方案是工程团队正在焦点。

## <a name="troubleshooting-tip"></a>故障排除提示

如果遇到错误的过程中，以下提示可帮助：

在中**调试器**选项卡上，在浏览器中打开开发人员工具。 在控制台中，执行`localStorage.clear()`删除任何断点。
