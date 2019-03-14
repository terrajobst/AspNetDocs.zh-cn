---
title: Razor 组件布局
author: guardrex
description: 了解如何创建可重用布局 Blazor 和 Razor 组件应用程序的组件。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/layouts
ms.openlocfilehash: 23d8f441c0b3bbde7a73717f6257013831617ec0
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57039034"
---
# <a name="razor-components-layouts"></a><span data-ttu-id="4cc09-103">Razor 组件布局</span><span class="sxs-lookup"><span data-stu-id="4cc09-103">Razor Components layouts</span></span>

<span data-ttu-id="4cc09-104">通过[Rainer Stropek](https://www.timecockpit.com)</span><span class="sxs-lookup"><span data-stu-id="4cc09-104">By [Rainer Stropek](https://www.timecockpit.com)</span></span>

<span data-ttu-id="4cc09-105">应用程序通常包含多个页。</span><span class="sxs-lookup"><span data-stu-id="4cc09-105">Apps typically contain more than one page.</span></span> <span data-ttu-id="4cc09-106">布局元素，如菜单、 版权消息和徽标，必须在所有页面上存在。</span><span class="sxs-lookup"><span data-stu-id="4cc09-106">Layout elements, such as menus, copyright messages, and logos, must be present on all pages.</span></span> <span data-ttu-id="4cc09-107">将这些布局元素的代码复制到的所有应用的页面不是一个有效的解决方案。</span><span class="sxs-lookup"><span data-stu-id="4cc09-107">Copying the code of these layout elements into all of the pages of an app isn't an efficient solution.</span></span> <span data-ttu-id="4cc09-108">此类重复难以维护，并随着时间的推移可能导致不一致的内容。</span><span class="sxs-lookup"><span data-stu-id="4cc09-108">Such duplication is hard to maintain and probably leads to inconsistent content over time.</span></span> <span data-ttu-id="4cc09-109">*布局*解决此问题。</span><span class="sxs-lookup"><span data-stu-id="4cc09-109">*Layouts* solve this problem.</span></span>

<span data-ttu-id="4cc09-110">从技术上讲，布局是只是另一个组件。</span><span class="sxs-lookup"><span data-stu-id="4cc09-110">Technically, a layout is just another component.</span></span> <span data-ttu-id="4cc09-111">布局定义 Razor 模板中或在C#代码，并可以包含数据绑定、 依赖关系注入和其他普通功能的组件。</span><span class="sxs-lookup"><span data-stu-id="4cc09-111">A layout is defined in a Razor template or in C# code and can contain data binding, dependency injection, and other ordinary features of components.</span></span> <span data-ttu-id="4cc09-112">打开两个其他方面*组件*成*布局*:</span><span class="sxs-lookup"><span data-stu-id="4cc09-112">Two additional aspects turn a *component* into a *layout*:</span></span>

* <span data-ttu-id="4cc09-113">布局组件必须继承自`BlazorLayoutComponent`。</span><span class="sxs-lookup"><span data-stu-id="4cc09-113">The layout component must inherit from `BlazorLayoutComponent`.</span></span> <span data-ttu-id="4cc09-114">`BlazorLayoutComponent` 定义`Body`属性，其中包含布局内呈现的内容。</span><span class="sxs-lookup"><span data-stu-id="4cc09-114">`BlazorLayoutComponent` defines a `Body` property that contains the content to be rendered inside the layout.</span></span>
* <span data-ttu-id="4cc09-115">布局组件使用`Body`属性指定的正文内容应呈现使用 Razor 语法`@Body`。</span><span class="sxs-lookup"><span data-stu-id="4cc09-115">The layout component uses the `Body` property to specify where the body content should be rendered using the Razor syntax `@Body`.</span></span> <span data-ttu-id="4cc09-116">在呈现期间`@Body`布局的内容替换为。</span><span class="sxs-lookup"><span data-stu-id="4cc09-116">During rendering, `@Body` is replaced by the content of the layout.</span></span>

<span data-ttu-id="4cc09-117">下面的代码示例显示了布局组件的 Razor 模板。</span><span class="sxs-lookup"><span data-stu-id="4cc09-117">The following code sample shows the Razor template of a layout component.</span></span> <span data-ttu-id="4cc09-118">请注意，使用`BlazorLayoutComponent`和`@Body`:</span><span class="sxs-lookup"><span data-stu-id="4cc09-118">Note the use of `BlazorLayoutComponent` and `@Body`:</span></span>

```csharp
@inherits BlazorLayoutComponent

<header>
    <h1>ERP Master 3000</h1>
</header>

<nav>
    <a href="master-data">Master Data Management</a>
    <a href="invoicing">Invoicing</a>
    <a href="accounting">Accounting</a>
</nav>

@Body

<footer>
    &copy; by @CopyrightMessage
</footer>

@functions {
    public string CopyrightMessage { get; set; }
    ...
}
```

## <a name="use-a-layout-in-a-component"></a><span data-ttu-id="4cc09-119">在组件中使用的布局</span><span class="sxs-lookup"><span data-stu-id="4cc09-119">Use a layout in a component</span></span>

<span data-ttu-id="4cc09-120">使用 Razor 指令`@layout`要应用于组件的布局。</span><span class="sxs-lookup"><span data-stu-id="4cc09-120">Use the Razor directive `@layout` to apply a layout to a component.</span></span> <span data-ttu-id="4cc09-121">编译器将转换到此指令`LayoutAttribute`，其应用到 component 类。</span><span class="sxs-lookup"><span data-stu-id="4cc09-121">The compiler converts this directive into a `LayoutAttribute`, which is applied to the component class.</span></span>

<span data-ttu-id="4cc09-122">下面的代码示例演示了这一概念。</span><span class="sxs-lookup"><span data-stu-id="4cc09-122">The following code sample demonstrates the concept.</span></span> <span data-ttu-id="4cc09-123">此组件的内容插入到*MasterLayout*的位置处`@Body`:</span><span class="sxs-lookup"><span data-stu-id="4cc09-123">The content of this component is inserted into the *MasterLayout* at the position of `@Body`:</span></span>

```csharp
@layout MasterLayout

@page "/master-data"

<h2>Master Data Management</h2>
...
```

## <a name="centralized-layout-selection"></a><span data-ttu-id="4cc09-124">选择集中式的布局</span><span class="sxs-lookup"><span data-stu-id="4cc09-124">Centralized layout selection</span></span>

<span data-ttu-id="4cc09-125">每个文件夹的应用程序可以选择包含名为的模板文件 *_ViewImports.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="4cc09-125">Every folder of a an app can optionally contain a template file named *_ViewImports.cshtml*.</span></span> <span data-ttu-id="4cc09-126">编译器包含在同一文件夹中的 Razor 模板和以递归方式在所有子文件夹中的所有视图导入文件中指定的指令。</span><span class="sxs-lookup"><span data-stu-id="4cc09-126">The compiler includes the directives specified in the view imports file in all of the Razor templates in the same folder and recursively in all of its subfolders.</span></span> <span data-ttu-id="4cc09-127">因此， *_ViewImports.cshtml*文件中含有`@layout MainLayout`确保所有文件夹，请使用中的组件*MainLayout*布局。</span><span class="sxs-lookup"><span data-stu-id="4cc09-127">Therefore, a *_ViewImports.cshtml* file containing `@layout MainLayout` ensures that all of the components in a folder use the *MainLayout* layout.</span></span> <span data-ttu-id="4cc09-128">无需反复添加`@layout`的所有 *\*.cshtml*文件。</span><span class="sxs-lookup"><span data-stu-id="4cc09-128">There's no need to repeatedly add `@layout` to all of the *\*.cshtml* files.</span></span>

<span data-ttu-id="4cc09-129">请注意，使用默认模板 *_ViewImports.cshtml*机制，用于选择布局。</span><span class="sxs-lookup"><span data-stu-id="4cc09-129">Note that the default template uses the *_ViewImports.cshtml* mechanism for layout selection.</span></span> <span data-ttu-id="4cc09-130">新创建的应用程序包含 *_ViewImports.cshtml*中的文件*页面*文件夹。</span><span class="sxs-lookup"><span data-stu-id="4cc09-130">A newly created app contains the *_ViewImports.cshtml* file in the *Pages* folder.</span></span>

## <a name="nested-layouts"></a><span data-ttu-id="4cc09-131">嵌套的布局</span><span class="sxs-lookup"><span data-stu-id="4cc09-131">Nested layouts</span></span>

<span data-ttu-id="4cc09-132">应用可以包含嵌套的布局。</span><span class="sxs-lookup"><span data-stu-id="4cc09-132">Apps can consist of nested layouts.</span></span> <span data-ttu-id="4cc09-133">一个组件可以引用又引用另一个布局的布局。</span><span class="sxs-lookup"><span data-stu-id="4cc09-133">A component can reference a layout which in turn references another layout.</span></span> <span data-ttu-id="4cc09-134">例如，可以使用嵌套的布局以反映多级别的菜单结构。</span><span class="sxs-lookup"><span data-stu-id="4cc09-134">For example, nesting layouts can be used to reflect a multi-level menu structure.</span></span>

<span data-ttu-id="4cc09-135">下面的代码示例演示如何使用嵌套的布局。</span><span class="sxs-lookup"><span data-stu-id="4cc09-135">The following code samples show how to use nested layouts.</span></span> <span data-ttu-id="4cc09-136">*CustomersComponent.cshtml*文件是要显示的组件。</span><span class="sxs-lookup"><span data-stu-id="4cc09-136">The *CustomersComponent.cshtml* file is the component to display.</span></span> <span data-ttu-id="4cc09-137">请注意，该组件会引用布局`MasterDataLayout`。</span><span class="sxs-lookup"><span data-stu-id="4cc09-137">Note that the component references the layout `MasterDataLayout`.</span></span>

<span data-ttu-id="4cc09-138">*CustomersComponent.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="4cc09-138">*CustomersComponent.cshtml*:</span></span>

```csharp
@layout MasterDataLayout

@page "/master-data/customers"

<h1>Customer Maintenance</h1>
...
```

<span data-ttu-id="4cc09-139">*MasterDataLayout.cshtml*文件提供了`MasterDataLayout`。</span><span class="sxs-lookup"><span data-stu-id="4cc09-139">The *MasterDataLayout.cshtml* file provides the `MasterDataLayout`.</span></span> <span data-ttu-id="4cc09-140">布局引用另一个布局`MainLayout`，它要嵌入。</span><span class="sxs-lookup"><span data-stu-id="4cc09-140">The layout references another layout, `MainLayout`, where it's going to be embedded.</span></span>

<span data-ttu-id="4cc09-141">*MasterDataLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="4cc09-141">*MasterDataLayout.cshtml*:</span></span>

```csharp
@layout MainLayout
@inherits BlazorLayoutComponent

<nav>
    <!-- Menu structure of master data module -->
    ...
</nav>

@Body
```

<span data-ttu-id="4cc09-142">最后，`MainLayout`包含的顶级布局元素，如页眉、 页脚和主菜单。</span><span class="sxs-lookup"><span data-stu-id="4cc09-142">Finally, `MainLayout` contains the top-level layout elements, such as the header, footer, and main menu.</span></span>

<span data-ttu-id="4cc09-143">*MainLayout.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="4cc09-143">*MainLayout.cshtml*:</span></span>

```csharp
@inherits BlazorLayoutComponent

<header>...</header>
<nav>...</nav>

@Body
```
