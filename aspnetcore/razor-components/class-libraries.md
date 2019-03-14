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
# <a name="razor-components-class-libraries"></a><span data-ttu-id="9ef4b-103">Razor 组件类库</span><span class="sxs-lookup"><span data-stu-id="9ef4b-103">Razor Components Class Libraries</span></span>

<span data-ttu-id="9ef4b-104">通过[Simon Timms](https://github.com/stimms)</span><span class="sxs-lookup"><span data-stu-id="9ef4b-104">By [Simon Timms](https://github.com/stimms)</span></span>

> [!NOTE]
> <span data-ttu-id="9ef4b-105">.NET Core 3.0 Preview 2 SDK 不包括项目模板，为 Razor 组件类库，但我们希望在将来的预览版中添加一个模板。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-105">The .NET Core 3.0 Preview 2 SDK doesn't include a project template for Razor Component Class Libraries, but we expect to add a template in a future preview.</span></span> <span data-ttu-id="9ef4b-106">同时，在您可以使用本主题中所述的 Blazor 组件类库模板。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-106">In meantime, you can use the Blazor Component Class Library template explained in this topic.</span></span>

<span data-ttu-id="9ef4b-107">组件可跨项目共享组件库中。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-107">Components can be shared in component libraries across projects.</span></span> <span data-ttu-id="9ef4b-108">组件可以从包含：</span><span class="sxs-lookup"><span data-stu-id="9ef4b-108">Components can be included from:</span></span>

* <span data-ttu-id="9ef4b-109">在解决方案中的另一个项目。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-109">Another project in the solution.</span></span>
* <span data-ttu-id="9ef4b-110">NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-110">A NuGet package.</span></span>
* <span data-ttu-id="9ef4b-111">引用的.NET 库。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-111">A referenced .NET library.</span></span>

<span data-ttu-id="9ef4b-112">正如组件是常规的.NET 类型，组件库是普通的.NET 程序集。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-112">Just as components are regular .NET types, component libraries are normal .NET assemblies.</span></span>

<span data-ttu-id="9ef4b-113">若要创建新的组件库，请使用`blazorlib`具有模板[dotnet 新](/dotnet/core/tools/dotnet-new)命令。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-113">To create a new component library, use the `blazorlib` template with the [dotnet new](/dotnet/core/tools/dotnet-new) command.</span></span> <span data-ttu-id="9ef4b-114">模板是安装的模板的一部分时[设置 Razor 组件](xref:razor-components/get-started)。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-114">The template is part of the templates installed when [setting up Razor Components](xref:razor-components/get-started).</span></span>

```console
dotnet new blazorlib -o MyComponentLib1
```

<span data-ttu-id="9ef4b-115">若要将库添加到现有项目，请使用[dotnet sln](/dotnet/core/tools/dotnet-sln)命令：</span><span class="sxs-lookup"><span data-stu-id="9ef4b-115">To add the library to an existing project, use the [dotnet sln](/dotnet/core/tools/dotnet-sln) command:</span></span>

```console
dotnet sln add .\MyComponentLib1
```

<span data-ttu-id="9ef4b-116">组件库可能包含静态文件，如图像、 JavaScript 和样式表。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-116">Component libraries may contain static files, such as images, JavaScript, and stylesheets.</span></span> <span data-ttu-id="9ef4b-117">在生成时，静态文件嵌入到生成的程序集文件 (*.dll*)，而无需担心如何包含其资源允许使用的组件。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-117">At build time, static files are embedded into the built assembly file (*.dll*), which allows consumption of the components without having to worry about how to include their resources.</span></span> <span data-ttu-id="9ef4b-118">中包括的任何文件`content`目录标记为嵌入的资源。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-118">Any files included in the `content` directory are marked as an embedded resource.</span></span> 

## <a name="consume-a-library-component"></a><span data-ttu-id="9ef4b-119">使用的库组件</span><span class="sxs-lookup"><span data-stu-id="9ef4b-119">Consume a library component</span></span>

<span data-ttu-id="9ef4b-120">为了使用在另一个项目中，库中定义的组件[ @addTagHelper ](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label)必须使用指令。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-120">In order to consume components defined in a library in another project, the [@addTagHelper](/aspnet/core/mvc/views/tag-helpers/intro#add-helper-label) directive must be used.</span></span> <span data-ttu-id="9ef4b-121">单个组件可能添加的名称。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-121">Individual components may be added by name.</span></span> <span data-ttu-id="9ef4b-122">例如，添加以下指令`Component1`的`MyComponentLib1`:</span><span class="sxs-lookup"><span data-stu-id="9ef4b-122">For example, the following directive adds `Component1` of `MyComponentLib1`:</span></span>

```cshtml
@addTagHelper MyComponentLib1.Component1, MyComponentLib1
```

<span data-ttu-id="9ef4b-123">指令的常规格式为：</span><span class="sxs-lookup"><span data-stu-id="9ef4b-123">The general format of the directive is:</span></span>

```cshtml
@addTagHelper <namespaced component name>, <assembly name>
```

<span data-ttu-id="9ef4b-124">但是，很常见，以包含所有中使用通配符的程序集的组件：</span><span class="sxs-lookup"><span data-stu-id="9ef4b-124">However, it's common to include all of the components from an assembly using a wildcard:</span></span>

```cshtml
@addTagHelper *, MyComponentLib1
```

<span data-ttu-id="9ef4b-125">`@addTagHelper`指令将其纳入 *_ViewImport.cshtml*若要使组件可用于整个项目或已应用到单个页面或组的文件夹中的页面。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-125">The `@addTagHelper` directive can be included in *_ViewImport.cshtml* to make the components available for an entire project or applied to a single page or set of pages within a folder.</span></span> <span data-ttu-id="9ef4b-126">使用`@addTagHelper`指令后，组件库的组件可以使用像与应用位于同一程序集中。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-126">With the `@addTagHelper` directive in place, the components of the component library can be consumed as if they were in the same assembly as the app.</span></span> 

## <a name="build-pack-and-ship-to-nuget"></a><span data-ttu-id="9ef4b-127">生成、 包和发送到 NuGet</span><span class="sxs-lookup"><span data-stu-id="9ef4b-127">Build, pack, and ship to NuGet</span></span>

<span data-ttu-id="9ef4b-128">由于组件库是标准.NET 库，打包并传送到 NuGet 没有任何差别打包和传送到 NuGet 的任何库。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-128">Because component libraries are standard .NET libraries, packaging and shipping them to NuGet is no different from packaging and shipping any library to NuGet.</span></span> <span data-ttu-id="9ef4b-129">使用执行打包[dotnet pack](/dotnet/core/tools/dotnet-pack)命令：</span><span class="sxs-lookup"><span data-stu-id="9ef4b-129">Packaging is performed using the [dotnet pack](/dotnet/core/tools/dotnet-pack) command:</span></span>

```console
dotnet pack
```

<span data-ttu-id="9ef4b-130">将包上载到使用 NuGet [dotnet nuget 发布](/dotnet/core/tools/dotnet-nuget-push)命令：</span><span class="sxs-lookup"><span data-stu-id="9ef4b-130">Upload the package to NuGet using the [dotnet nuget publish](/dotnet/core/tools/dotnet-nuget-push) command:</span></span>

```console
dotnet nuget publish
```

<span data-ttu-id="9ef4b-131">任何包含静态资源包含在 NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-131">Any included static resources are included in the NuGet package.</span></span> <span data-ttu-id="9ef4b-132">库的使用者自动接收脚本和样式表，因此使用者无需手动安装的资源。</span><span class="sxs-lookup"><span data-stu-id="9ef4b-132">Library consumers automatically receive scripts and stylesheets, so consumers aren't required to manually install the resources.</span></span>
