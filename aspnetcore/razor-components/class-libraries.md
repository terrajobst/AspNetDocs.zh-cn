---
title: Razor 组件类库
author: guardrex
description: 发现如何组件可以包含在外部组件库中的 Razor 组件应用程序。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/09/2019
uid: razor-components/class-libraries
ms.openlocfilehash: 0e644627178bae2b8880760335860b3e0ebef156
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57037404"
---
# <a name="razor-components-class-libraries"></a>Razor 组件类库

通过[Simon Timms](https://github.com/stimms)

> [!NOTE]
> .NET Core 3.0 Preview 2 SDK 不包括项目模板，为 Razor 组件类库，但我们希望在将来的预览版中添加一个模板。 同时，在您可以使用本主题中所述的 Blazor 组件类库模板。

组件可跨项目共享组件库中。 组件可以从包含：

* 在解决方案中的另一个项目。
* NuGet 包。
* 引用的.NET 库。

正如组件是常规的.NET 类型，组件库是普通的.NET 程序集。

若要创建新的组件库，请使用`blazorlib`具有模板[dotnet 新](/dotnet/core/tools/dotnet-new)命令。 模板是安装的模板的一部分时[设置 Razor 组件](xref:razor-components/get-started)。

```console
dotnet new blazorlib -o MyComponentLib1
```

若要将库添加到现有项目，请使用[dotnet sln](/dotnet/core/tools/dotnet-sln)命令：

```console
dotnet sln add .\MyComponentLib1
```

组件库可能包含静态文件，如图像、 JavaScript 和样式表。 在生成时，静态文件嵌入到生成的程序集文件 (*.dll*)，而无需担心如何包含其资源允许使用的组件。 中包括的任何文件`content`目录标记为嵌入的资源。 

## <a name="consume-a-library-component"></a>使用的库组件

为了使用在另一个项目中，库中定义的组件[ @addTagHelper ](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label)必须使用指令。 单个组件可能添加的名称。 例如，添加以下指令`Component1`的`MyComponentLib1`:

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

指令的常规格式为：

```cshtml
@addTagHelper <namespaced component name>, <assembly name>
```

但是，很常见，以包含所有中使用通配符的程序集的组件：

```cshtml
@addTagHelper *, MyComponentLib1
```

`@addTagHelper`指令将其纳入 *_ViewImport.cshtml*若要使组件可用于整个项目或已应用到单个页面或组的文件夹中的页面。 使用`@addTagHelper`指令后，组件库的组件可以使用像与应用位于同一程序集中。 

## <a name="build-pack-and-ship-to-nuget"></a>生成、 包和发送到 NuGet

由于组件库是标准.NET 库，打包并传送到 NuGet 没有任何差别打包和传送到 NuGet 的任何库。 使用执行打包[dotnet pack](/dotnet/core/tools/dotnet-pack)命令：

```console
dotnet pack
```

将包上载到使用 NuGet [dotnet nuget 发布](/dotnet/core/tools/dotnet-nuget-push)命令：

```console
dotnet nuget publish
```

任何包含静态资源包含在 NuGet 包。 库的使用者自动接收脚本和样式表，因此使用者无需手动安装的资源。
