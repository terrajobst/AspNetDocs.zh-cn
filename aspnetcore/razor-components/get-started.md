---
title: 开始使用 Razor 组件
author: guardrex
description: 了解如何开始使用 Razor 组件创建和修改 Razor 组件项目。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 02/03/2019
uid: razor-components/get-started
ms.openlocfilehash: a9ada603e5ed4e0e75c4aebc5105c331118666e6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57036384"
---
# <a name="get-started-with-razor-components"></a><span data-ttu-id="11fc7-103">开始使用 Razor 组件</span><span class="sxs-lookup"><span data-stu-id="11fc7-103">Get started with Razor Components</span></span>

<span data-ttu-id="11fc7-104">作者：[Daniel Roth](https://github.com/danroth27) 和 [Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="11fc7-104">By [Daniel Roth](https://github.com/danroth27) and [Luke Latham](https://github.com/guardrex)</span></span>

# <a name="visual-studiotabvisual-studio"></a>[<span data-ttu-id="11fc7-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="11fc7-105">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="11fc7-106">先决条件：</span><span class="sxs-lookup"><span data-stu-id="11fc7-106">Prerequisites:</span></span>

[!INCLUDE[](~/includes/net-core-prereqs-vs-3.0.md)]

<span data-ttu-id="11fc7-107">在 Visual Studio 中创建第一个 Razor 组件项目：</span><span class="sxs-lookup"><span data-stu-id="11fc7-107">To create your first Razor Components project in Visual Studio:</span></span>

1. <span data-ttu-id="11fc7-108">选择**文件** > **新建项目** > **Web** > **ASP.NET Core Web 应用程序**。</span><span class="sxs-lookup"><span data-stu-id="11fc7-108">Select **File** > **New Project** > **Web** > **ASP.NET Core Web Application**.</span></span>
1. <span data-ttu-id="11fc7-109">请确保 **.NET Core**并**ASP.NET Core 3.0**顶部选择。</span><span class="sxs-lookup"><span data-stu-id="11fc7-109">Make sure **.NET Core** and **ASP.NET Core 3.0** are selected at the top.</span></span>
1. <span data-ttu-id="11fc7-110">选择**Razor 组件**模板，然后选择**确定**。</span><span class="sxs-lookup"><span data-stu-id="11fc7-110">Choose the **Razor Components** template and select **OK**.</span></span>

   ![新建应用对话框](https://msdnshared.blob.core.windows.net/media/2019/01/razor-components-template.png)

1. <span data-ttu-id="11fc7-112">按 F5  运行应用。</span><span class="sxs-lookup"><span data-stu-id="11fc7-112">Press **F5** to run the app.</span></span>

<span data-ttu-id="11fc7-113">祝贺你！</span><span class="sxs-lookup"><span data-stu-id="11fc7-113">Congratulations!</span></span> <span data-ttu-id="11fc7-114">只需运行第一个 Razor 组件应用 ！</span><span class="sxs-lookup"><span data-stu-id="11fc7-114">You just ran your first Razor Components app!</span></span>

<!--

# [Visual Studio Code](#tab/visual-studio-code)

Prerequisites:

[!INCLUDE[](~/includes/net-core-prereqs-vsc-3.0.md)]

To create your first Razor Components project in Visual Studio Code:

1. Execute the following command from a command shell:

   ```console
   dotnet new razorcomponents -o WebApplication1
   ```

1. Open the *WebApplication1* folder in Visual Studio Code.

1. Add a *.vscode* folder.

1. Add a *tasks.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/tasks.json)]

1. Add a *launch.json* file to the *.vscode* folder with the following content:

   [!code-json[](get-started/samples_snapshot/3.x/launch.json)]

1. Execute the app using the Visual Studio Code debugger.

1. In a browser, navigate to `https://localhost:5001`.

Congratulations! You just ran your first Razor Components app!

# [Visual Studio for Mac](#tab/visual-studio-mac)

.NET Core 3.0 will be supported with Visual Studio for Mac version 8.0 or later. Visual Studio for Mac version 8.0 Preview isn't available at this time.

Use the [.NET Core CLI version of this topic](xref:razor-components/get-started?tabs=netcore-cli) on macOS.


[!INCLUDE[](~/includes/net-core-prereqs-mac-3.0.md)]

To create your first project Razor Components project in Visual Studio for Mac:

1. Select **File** > **New Solution** or **New Project**.
1. In the sidebar, select **.NET Core** > **App**.
1. Select **ASP.NET Core Razor Components** and select **Next**.
1. The **Target Framework** defaults to **.NET Core 3.0**. Select **Next**.
1. In the **Project Name** field, enter `WebApplication1`. Select **Create**.
1. Select **Run** > **Run Without Debugging** to run the app *without the debugger*. Running with the debugger isn't supported at this time.

Congratulations! You just ran your first Razor Components app!
-->

# <a name="net-core-clitabnetcore-cli"></a>[<span data-ttu-id="11fc7-115">.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="11fc7-115">.NET Core CLI</span></span>](#tab/netcore-cli/)

<span data-ttu-id="11fc7-116">先决条件：</span><span class="sxs-lookup"><span data-stu-id="11fc7-116">Prerequisites:</span></span>

* [<span data-ttu-id="11fc7-117">.NET core SDK 3.0 预览</span><span class="sxs-lookup"><span data-stu-id="11fc7-117">.NET Core SDK 3.0 Preview</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0)

1. <span data-ttu-id="11fc7-118">若要从命令行界面创建第一个 Razor 组件项目：</span><span class="sxs-lookup"><span data-stu-id="11fc7-118">To create your first Razor Components project from a command shell:</span></span>

   ```console
   dotnet new razorcomponents -o WebApplication1
   cd WebApplication1
   dotnet run
   ```

1. <span data-ttu-id="11fc7-119">在浏览器中导航到 `https://localhost:5001`。</span><span class="sxs-lookup"><span data-stu-id="11fc7-119">In a browser, navigate to `https://localhost:5001`.</span></span>

<span data-ttu-id="11fc7-120">祝贺你！</span><span class="sxs-lookup"><span data-stu-id="11fc7-120">Congratulations!</span></span> <span data-ttu-id="11fc7-121">只需运行第一个 Razor 组件应用 ！</span><span class="sxs-lookup"><span data-stu-id="11fc7-121">You just ran your first Razor Components app!</span></span>

---

## <a name="razor-components-project"></a><span data-ttu-id="11fc7-122">Razor 组件项目</span><span class="sxs-lookup"><span data-stu-id="11fc7-122">Razor Components project</span></span>

<span data-ttu-id="11fc7-123">由 Razor 组件模板创建的解决方案包含两个项目：</span><span class="sxs-lookup"><span data-stu-id="11fc7-123">The solution created by the Razor Components template contains two projects:</span></span>

* <span data-ttu-id="11fc7-124">*WebApplication1.Server* &ndash;服务器项目是将设置为托管 Razor 组件应用程序的 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="11fc7-124">*WebApplication1.Server* &ndash; The server project is an ASP.NET Core project set up to host the Razor Components app.</span></span>
* <span data-ttu-id="11fc7-125">*WebApplication1.App* &ndash;使用 Razor 组件的客户端的 web UI 项目。</span><span class="sxs-lookup"><span data-stu-id="11fc7-125">*WebApplication1.App* &ndash; The client-side web UI project that uses Razor Components.</span></span>

<span data-ttu-id="11fc7-126">中的 UI 逻辑*WebApplication1.App*项目分开由于 ASP.NET Core 3.0 Preview 2 中的技术限制应用的其余部分。</span><span class="sxs-lookup"><span data-stu-id="11fc7-126">The UI logic in the *WebApplication1.App* project is separated from the rest of the app due to a technical limitation in ASP.NET Core 3.0 Preview 2.</span></span> <span data-ttu-id="11fc7-127">Razor 文件扩展名 (*.cshtml*) 使用的 Razor 组件还可用于 Razor 页面和 MVC 视图。</span><span class="sxs-lookup"><span data-stu-id="11fc7-127">The Razor file extension (*.cshtml*) used for Razor Components is also used for Razor Pages and MVC views.</span></span> <span data-ttu-id="11fc7-128">目前，Razor 组件和 Razor 页面/MVC 具有不同的编译模型，以便保留单独的 Razor 组件 Razor 文件。</span><span class="sxs-lookup"><span data-stu-id="11fc7-128">Currently, Razor Components and Razor Pages/MVC have different compilation models, so the Razor Components Razor files are kept separate.</span></span> <span data-ttu-id="11fc7-129">在将来的预览版，我们计划引入新的文件扩展名为 Razor 组件 (*.razor*)。</span><span class="sxs-lookup"><span data-stu-id="11fc7-129">In a future preview, we plan to introduce a new file extension for Razor Components (*.razor*).</span></span> <span data-ttu-id="11fc7-130">将托管组件、 页面和视图*同一项目中*。</span><span class="sxs-lookup"><span data-stu-id="11fc7-130">Components, pages, and views will be hosted *in the same project*.</span></span>

<span data-ttu-id="11fc7-131">当应用运行时，多个页侧栏中的选项卡中有：</span><span class="sxs-lookup"><span data-stu-id="11fc7-131">When the app is run, multiple pages are available from tabs in the sidebar:</span></span>

* <span data-ttu-id="11fc7-132">主页</span><span class="sxs-lookup"><span data-stu-id="11fc7-132">Home</span></span>
* <span data-ttu-id="11fc7-133">计数器</span><span class="sxs-lookup"><span data-stu-id="11fc7-133">Counter</span></span>
* <span data-ttu-id="11fc7-134">提取数据</span><span class="sxs-lookup"><span data-stu-id="11fc7-134">Fetch data</span></span>

<span data-ttu-id="11fc7-135">在“计数器”页上，选择“单击我”按钮，在不刷新页面的情况下增加计数器值。</span><span class="sxs-lookup"><span data-stu-id="11fc7-135">On the Counter page, select the **Click me** button to increment the counter without a page refresh.</span></span> <span data-ttu-id="11fc7-136">增加网页中的计数器值通常需要编写 JavaScript，但 Razor 组件使用 C# 提供了更好的方法。</span><span class="sxs-lookup"><span data-stu-id="11fc7-136">Incrementing a counter in a webpage normally requires writing JavaScript, but Razor Components provides a better approach using C#.</span></span>

<span data-ttu-id="11fc7-137">*WebApplication1.App/Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="11fc7-137">*WebApplication1.App/Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter1.cshtml)]

<span data-ttu-id="11fc7-138">请求`/counter`中指定的浏览器，通过`@page`指令在顶部，会导致计数器组件来呈现其内容。</span><span class="sxs-lookup"><span data-stu-id="11fc7-138">A request for `/counter` in the browser, as specified by the `@page` directive at the top, causes the Counter component to render its content.</span></span> <span data-ttu-id="11fc7-139">组件将使用灵活且高效的方式更新 UI 的呈现器树的内存中表示形式呈现。</span><span class="sxs-lookup"><span data-stu-id="11fc7-139">Components render into an in-memory representation of the render tree that can then be used to update the UI in a flexible and efficient way.</span></span>

<span data-ttu-id="11fc7-140">每次**Click me**按钮处于选中状态：</span><span class="sxs-lookup"><span data-stu-id="11fc7-140">Each time the **Click me** button is selected:</span></span>

* <span data-ttu-id="11fc7-141">`onclick`触发事件。</span><span class="sxs-lookup"><span data-stu-id="11fc7-141">The `onclick` event is fired.</span></span>
* <span data-ttu-id="11fc7-142">调用 `IncrementCount` 方法。</span><span class="sxs-lookup"><span data-stu-id="11fc7-142">The `IncrementCount` method is called.</span></span>
* <span data-ttu-id="11fc7-143">`currentCount`会递增。</span><span class="sxs-lookup"><span data-stu-id="11fc7-143">The `currentCount` is incremented.</span></span>
* <span data-ttu-id="11fc7-144">再次呈现该组件。</span><span class="sxs-lookup"><span data-stu-id="11fc7-144">The component is rendered again.</span></span>

<span data-ttu-id="11fc7-145">在运行时比较至以前的内容的新内容，并仅将更改的内容应用到文档对象模型 (DOM)。</span><span class="sxs-lookup"><span data-stu-id="11fc7-145">The runtime compares the new content to the previous content and only applies the changed content to the Document Object Model (DOM).</span></span>

<span data-ttu-id="11fc7-146">将组件添加到另一个组件使用类似于 HTML 的语法。</span><span class="sxs-lookup"><span data-stu-id="11fc7-146">Add a component to another component using an HTML-like syntax.</span></span> <span data-ttu-id="11fc7-147">使用属性或子内容指定组件参数。</span><span class="sxs-lookup"><span data-stu-id="11fc7-147">Component parameters are specified using attributes or child content.</span></span> <span data-ttu-id="11fc7-148">例如，计数器组件可以已添加到应用程序的主页添加`<Counter />`元素到索引组件。</span><span class="sxs-lookup"><span data-stu-id="11fc7-148">For example, a Counter component can be added to the app's homepage by adding a `<Counter />` element to the Index component.</span></span>

<span data-ttu-id="11fc7-149">*WebApplication1.App/Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="11fc7-149">*WebApplication1.App/Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index1.cshtml?highlight=7)]

<span data-ttu-id="11fc7-150">运行应用。</span><span class="sxs-lookup"><span data-stu-id="11fc7-150">Run the app.</span></span> <span data-ttu-id="11fc7-151">主页都有它自己的计数器。</span><span class="sxs-lookup"><span data-stu-id="11fc7-151">The homepage has its own counter.</span></span>

<span data-ttu-id="11fc7-152">若要将参数添加到计数器组件，更新组件的`@functions`块：</span><span class="sxs-lookup"><span data-stu-id="11fc7-152">To add a parameter to the Counter component, update the component's `@functions` block:</span></span>

* <span data-ttu-id="11fc7-153">添加的属性`IncrementAmount`修饰的`[Parameter]`属性。</span><span class="sxs-lookup"><span data-stu-id="11fc7-153">Add a property for `IncrementAmount` decorated with the `[Parameter]` attribute.</span></span>
* <span data-ttu-id="11fc7-154">增加 `currentCount` 的值时，更改 `IncrementCount` 方法以使用 `IncrementAmount`。</span><span class="sxs-lookup"><span data-stu-id="11fc7-154">Change the `IncrementCount` method to use the `IncrementAmount` when increasing the value of `currentCount`.</span></span>

<span data-ttu-id="11fc7-155">*WebApplication1.App/Pages/Counter.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="11fc7-155">*WebApplication1.App/Pages/Counter.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Counter2.cshtml?highlight=4,8)]

<span data-ttu-id="11fc7-156">使用属性在 Home 组件的 `<Counter>` 元素中指定 `IncrementAmount` 参数。</span><span class="sxs-lookup"><span data-stu-id="11fc7-156">Specify an `IncrementAmount` parameter in the Home component's `<Counter>` element using an attribute.</span></span>

<span data-ttu-id="11fc7-157">*WebApplication1.App/Pages/Index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="11fc7-157">*WebApplication1.App/Pages/Index.cshtml*:</span></span>

[!code-cshtml[](get-started/samples_snapshot/3.x/Index2.cshtml)]

<span data-ttu-id="11fc7-158">运行应用。</span><span class="sxs-lookup"><span data-stu-id="11fc7-158">Run the app.</span></span> <span data-ttu-id="11fc7-159">主页具有其自己计数器，它每次按 10 递增**Click me**按钮处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="11fc7-159">The homepage has its own counter that increments by ten each time the **Click me** button is selected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11fc7-160">后续步骤</span><span class="sxs-lookup"><span data-stu-id="11fc7-160">Next steps</span></span>

<xref:tutorials/first-razor-components-app>
