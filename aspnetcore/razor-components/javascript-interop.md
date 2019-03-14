---
title: Razor JavaScript 组件互操作
author: guardrex
description: 了解如何调用 JavaScript 函数，从.NET 和.NET 中 JavaScript Blazor 和 Razor 组件应用程序中的方法。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/javascript-interop
ms.openlocfilehash: 9f822fee8990b03ff15ffa9857a2ddd95328a6ce
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050364"
---
# <a name="razor-components-javascript-interop"></a><span data-ttu-id="860c4-103">Razor JavaScript 组件互操作</span><span class="sxs-lookup"><span data-stu-id="860c4-103">Razor Components JavaScript interop</span></span>

<span data-ttu-id="860c4-104">通过[Javier Calvarro Nelson](https://github.com/javiercn)， [Daniel Roth](https://github.com/danroth27)，和[Luke Latham](https://github.com/guardrex)</span><span class="sxs-lookup"><span data-stu-id="860c4-104">By [Javier Calvarro Nelson](https://github.com/javiercn), [Daniel Roth](https://github.com/danroth27), and [Luke Latham](https://github.com/guardrex)</span></span>

<span data-ttu-id="860c4-105">Razor 组件应用程序可以调用 JavaScript 函数，从.NET 和.NET 中的 JavaScript 代码的方法。</span><span class="sxs-lookup"><span data-stu-id="860c4-105">A Razor Components app can invoke JavaScript functions from .NET and .NET methods from JavaScript code.</span></span>

## <a name="invoke-javascript-functions-from-net-methods"></a><span data-ttu-id="860c4-106">调用 JavaScript 函数的.NET 方法</span><span class="sxs-lookup"><span data-stu-id="860c4-106">Invoke JavaScript functions from .NET methods</span></span>

<span data-ttu-id="860c4-107">有些的时候需要调用 JavaScript 函数的.NET 代码时。</span><span class="sxs-lookup"><span data-stu-id="860c4-107">There are times when .NET code is required to call a JavaScript function.</span></span> <span data-ttu-id="860c4-108">例如，浏览器功能或从 JavaScript 库向应用程序的功能，可以公开 JavaScript 调用。</span><span class="sxs-lookup"><span data-stu-id="860c4-108">For example, a JavaScript call can expose browser capabilities or functionality from a JavaScript library to the app.</span></span>

<span data-ttu-id="860c4-109">若要从.NET 调用的 JavaScript，请使用`IJSRuntime`抽象。</span><span class="sxs-lookup"><span data-stu-id="860c4-109">To call into JavaScript from .NET, use the `IJSRuntime` abstraction.</span></span> <span data-ttu-id="860c4-110">`InvokeAsync<T>`方法`IJSRuntime`采用你想要与任意数量的 JSON 可序列化参数一起调用的 JavaScript 函数的标识符。</span><span class="sxs-lookup"><span data-stu-id="860c4-110">The `InvokeAsync<T>` method on `IJSRuntime` takes an identifier for the JavaScript function you wish to invoke along with any number of JSON-serializable arguments.</span></span> <span data-ttu-id="860c4-111">函数标识符是相对于全局作用域 (`window`)。</span><span class="sxs-lookup"><span data-stu-id="860c4-111">The function identifier is relative to the global scope (`window`).</span></span> <span data-ttu-id="860c4-112">如果你想要调用`window.someScope.someFunction`，该标识符是`someScope.someFunction`。</span><span class="sxs-lookup"><span data-stu-id="860c4-112">If you wish to call `window.someScope.someFunction`, the identifier is `someScope.someFunction`.</span></span> <span data-ttu-id="860c4-113">没有无需注册该函数之前调用它。</span><span class="sxs-lookup"><span data-stu-id="860c4-113">There's no need to register the function before it's called.</span></span> <span data-ttu-id="860c4-114">返回类型`T`还必须是 JSON 可序列化。</span><span class="sxs-lookup"><span data-stu-id="860c4-114">The return type `T` must also be JSON serializable.</span></span>

<span data-ttu-id="860c4-115">对于服务器端 ASP.NET Core Razor 组件应用程序：</span><span class="sxs-lookup"><span data-stu-id="860c4-115">For server-side ASP.NET Core Razor Components apps:</span></span>

* <span data-ttu-id="860c4-116">由服务器端应用程序处理多个用户请求。</span><span class="sxs-lookup"><span data-stu-id="860c4-116">Multiple user requests are processed by the server-side app.</span></span> <span data-ttu-id="860c4-117">不要调用`JSRuntime.Current`组件调用 JavaScript 函数中。</span><span class="sxs-lookup"><span data-stu-id="860c4-117">Don't call `JSRuntime.Current` in a component to invoke JavaScript functions.</span></span>
* <span data-ttu-id="860c4-118">注入`IJSRuntime`抽象和使用注入的对象发出 JavaScript 互操作调用。</span><span class="sxs-lookup"><span data-stu-id="860c4-118">Inject the `IJSRuntime` abstraction and use the injected object to issue JavaScript interop calls.</span></span>

<span data-ttu-id="860c4-119">下面的示例基于[TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder)，实验性的基于 JavaScript 的解码器。</span><span class="sxs-lookup"><span data-stu-id="860c4-119">The following example is based on [TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder), an experimental JavaScript-based decoder.</span></span> <span data-ttu-id="860c4-120">该示例演示如何调用一个 JavaScript 函数中的C#方法。</span><span class="sxs-lookup"><span data-stu-id="860c4-120">The example demonstrates how to invoke a JavaScript function from a C# method.</span></span> <span data-ttu-id="860c4-121">JavaScript 函数接受字节数组从C#方法，对数组进行解码并返回到显示的组件的文本。</span><span class="sxs-lookup"><span data-stu-id="860c4-121">The JavaScript function accepts a byte array from a C# method, decodes the array, and returns the text to the component for display.</span></span>

<span data-ttu-id="860c4-122">内部`<head>`的元素*wwwroot/index.html*，提供一个函数来使用`TextDecoder`传递的数组进行解码：</span><span class="sxs-lookup"><span data-stu-id="860c4-122">Inside the `<head>` element of *wwwroot/index.html*, provide a function that uses `TextDecoder` to decode a passed array:</span></span>

```html
<script>
  window.ConvertArray = (win1251Array) => {
    var win1251decoder = new TextDecoder('windows-1251');
    var bytes = new Uint8Array(win1251Array);
    var decodedArray = win1251decoder.decode(bytes);
    console.log(decodedArray);
    return decodedArray;
  };
</script>
```

<span data-ttu-id="860c4-123">此外可以通过对中的脚本文件的引用的 JavaScript 文件加载 JavaScript 代码，例如在前面的示例所示的代码*wwwroot/index.html*文件。</span><span class="sxs-lookup"><span data-stu-id="860c4-123">JavaScript code, such as the code shown in the preceding example, can also be loaded by a JavaScript file with a reference to the script file in the *wwwroot/index.html* file.</span></span>

<span data-ttu-id="860c4-124">以下组件：</span><span class="sxs-lookup"><span data-stu-id="860c4-124">The following component:</span></span>

* <span data-ttu-id="860c4-125">调用`ConvertArray`JavaScript 函数使用`JsRuntime`的组件按钮时 (**转换数组**) 处于选中状态。</span><span class="sxs-lookup"><span data-stu-id="860c4-125">Invokes the `ConvertArray` JavaScript function using `JsRuntime` when a component button (**Convert Array**) is selected.</span></span>
* <span data-ttu-id="860c4-126">JavaScript 函数调用之后，则将传递的数组转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="860c4-126">After the JavaScript function is called, the passed array is converted into a string.</span></span> <span data-ttu-id="860c4-127">供显示的组件返回的字符串。</span><span class="sxs-lookup"><span data-stu-id="860c4-127">The string is returned to the component for display.</span></span>

```cshtml
@page "/"
@using Microsoft.JSInterop;
@inject IJSRuntime JsRuntime;

<h1>Call JavaScript Function Example</h1>

<button type="button" class="btn btn-primary" onclick="@ConvertArray">
    Convert Array
</button>

<p class="mt-2" style="font-size:1.6em">
    <span class="badge badge-success">
        @ConvertedText
    </span>
</p>

@functions {
    // Quote (c)2005 Universal Pictures: Serenity
    // https://www.uphe.com/movies/serenity
    // David Krumholtz on IMDB: https://www.imdb.com/name/nm0472710/

    private MarkupString ConvertedText =
        new MarkupString("Select the <b>Convert Array</b> button.");

    private uint[] QuoteArray = new uint[]
        {
            60, 101, 109, 62, 67, 97, 110, 39, 116, 32, 115, 116, 111, 112, 32,
            116, 104, 101, 32, 115, 105, 103, 110, 97, 108, 44, 32, 77, 97,
            108, 46, 60, 47, 101, 109, 62, 32, 45, 32, 77, 114, 46, 32, 85, 110,
            105, 118, 101, 114, 115, 101, 10, 10,
        };

    async void ConvertArray()
    {
        var text =
            await JsRuntime.InvokeAsync<string>("ConvertArray", QuoteArray);

        ConvertedText = new MarkupString(text);

        StateHasChanged();
    }
}
```

<span data-ttu-id="860c4-128">对于客户端 Blazor 应用，`IJSRuntime`抽象是可从访问`JSRuntime.Current`，这是指当前用户的请求。</span><span class="sxs-lookup"><span data-stu-id="860c4-128">For client-side Blazor apps, the `IJSRuntime` abstraction is accessible from `JSRuntime.Current`, which refers to the current user's request.</span></span> <span data-ttu-id="860c4-129">由于只有一个用户的客户端 Blazor 应用程序，使用`JSRuntime.Current`调用 JavaScript 函数通常会正常工作。</span><span class="sxs-lookup"><span data-stu-id="860c4-129">Because there's only a single user of a client-side Blazor app, using `JSRuntime.Current` to invoke a JavaScript function works normally.</span></span> <span data-ttu-id="860c4-130">只能使用`JSRuntime.Current`客户端 Blazor 应用中。</span><span class="sxs-lookup"><span data-stu-id="860c4-130">Only use `JSRuntime.Current` in client-side Blazor apps.</span></span>

<span data-ttu-id="860c4-131">在客户端的示例应用中本主题附带，两个 JavaScript 函数可供与 DOM 来接收用户输入并显示一条欢迎消息进行交互的客户端应用：</span><span class="sxs-lookup"><span data-stu-id="860c4-131">In the client-side sample app that accompanies this topic, two JavaScript functions are available to the client-side app that interact with the DOM to receive user input and display a welcome message:</span></span>

* <span data-ttu-id="860c4-132">`showPrompt` &ndash; 生成提示接受用户输入 （用户的名称），并返回给调用方的名称。</span><span class="sxs-lookup"><span data-stu-id="860c4-132">`showPrompt` &ndash; Produces a prompt to accept user input (the user's name) and returns the name to the caller.</span></span>
* <span data-ttu-id="860c4-133">`displayWelcome` &ndash; 将一条欢迎消息从调用方分配给具有的 DOM 对象`id`的`welcome`。</span><span class="sxs-lookup"><span data-stu-id="860c4-133">`displayWelcome` &ndash; Assigns a welcome message from the caller to a DOM object with an `id` of `welcome`.</span></span>

<span data-ttu-id="860c4-134">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="860c4-134">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

<span data-ttu-id="860c4-135">位置`<script>`引用的 JavaScript 文件中的标记*wwwroot/index.html*文件：</span><span class="sxs-lookup"><span data-stu-id="860c4-135">Place the `<script>` tag that references the JavaScript file in the *wwwroot/index.html* file:</span></span>

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=16)]

<span data-ttu-id="860c4-136">不要将组件文件中的脚本标记，因为无法动态更新的脚本标记。</span><span class="sxs-lookup"><span data-stu-id="860c4-136">Don't place a script tag in a component file because the script tag can't be updated dynamically.</span></span>

<span data-ttu-id="860c4-137">使用通过调用 JavaScript 函数的.NET 方法互操作`InvokeAsync<T>`方法`IJSRuntime`。</span><span class="sxs-lookup"><span data-stu-id="860c4-137">.NET methods interop with the JavaScript functions by calling `InvokeAsync<T>` method on `IJSRuntime`.</span></span>

<span data-ttu-id="860c4-138">示例应用使用一对C#方法，`Prompt`并`Display`，以调用`showPrompt`并`displayWelcome`JavaScript 函数：</span><span class="sxs-lookup"><span data-stu-id="860c4-138">The sample app uses a pair of C# methods, `Prompt` and `Display`, to invoke the `showPrompt` and `displayWelcome` JavaScript functions:</span></span>

<span data-ttu-id="860c4-139">*JsInteropClasses/ExampleJsInterop.cs*:</span><span class="sxs-lookup"><span data-stu-id="860c4-139">*JsInteropClasses/ExampleJsInterop.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=6-8,14-16)]

<span data-ttu-id="860c4-140">`IJSRuntime`抽象是异步模式，以允许服务器端的方案。</span><span class="sxs-lookup"><span data-stu-id="860c4-140">The `IJSRuntime` abstraction is asynchronous to allow for server-side scenarios.</span></span> <span data-ttu-id="860c4-141">如果应用在运行客户端，并且你想要调用的 JavaScript 函数以同步方式，向下转换到`IJSInProcessRuntime`，并调用`Invoke<T>`相反。</span><span class="sxs-lookup"><span data-stu-id="860c4-141">If the app runs client-side and you want to invoke a JavaScript function synchronously, downcast to `IJSInProcessRuntime` and call `Invoke<T>` instead.</span></span> <span data-ttu-id="860c4-142">我们建议，大多数 JavaScript 库的互操作使用异步 Api，以确保库是在所有方案，客户端或服务器端中可用。</span><span class="sxs-lookup"><span data-stu-id="860c4-142">We recommend that most JavaScript interop libraries use the async APIs to ensure the libraries are available in all scenarios, client-side or server-side.</span></span>

<span data-ttu-id="860c4-143">示例应用包含用于演示 JS 互操作的组件。</span><span class="sxs-lookup"><span data-stu-id="860c4-143">The sample app includes a component to demonstrate JS interop.</span></span> <span data-ttu-id="860c4-144">组件：</span><span class="sxs-lookup"><span data-stu-id="860c4-144">The component:</span></span>

* <span data-ttu-id="860c4-145">接收通过 JS 提示用户输入。</span><span class="sxs-lookup"><span data-stu-id="860c4-145">Receives user input via a JS prompt.</span></span>
* <span data-ttu-id="860c4-146">返回对组件进行处理的文本。</span><span class="sxs-lookup"><span data-stu-id="860c4-146">Returns the text to the component for processing.</span></span>
* <span data-ttu-id="860c4-147">调用与 DOM 以显示一条欢迎消息进行交互的第二个 JS 函数。</span><span class="sxs-lookup"><span data-stu-id="860c4-147">Calls a second JS function that interacts with the DOM to display a welcome message.</span></span>

<span data-ttu-id="860c4-148">*Pages/JSInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="860c4-148">*Pages/JSInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=1&end=21&highlight=2-3,9-11,13,16-20)]

1. <span data-ttu-id="860c4-149">当`TriggerJsPrompt`选择该组件的执行**触发器 JavaScript 提示**按钮，`ExampleJsInterop.Prompt`中的方法C#调用代码。</span><span class="sxs-lookup"><span data-stu-id="860c4-149">When `TriggerJsPrompt` is executed by selecting the component's **Trigger JavaScript Prompt** button, the `ExampleJsInterop.Prompt` method in C# code is called.</span></span>
1. <span data-ttu-id="860c4-150">`Prompt`方法执行 JavaScript`showPrompt`函数中提供*wwwroot/exampleJsInterop.js*文件。</span><span class="sxs-lookup"><span data-stu-id="860c4-150">The `Prompt` method executes the JavaScript `showPrompt` function provided in the *wwwroot/exampleJsInterop.js* file.</span></span>
1. <span data-ttu-id="860c4-151">`showPrompt`函数可接受用户输入 （用户的名称），这是 HTML 编码并返回到`Prompt`方法并最终返回到该组件。</span><span class="sxs-lookup"><span data-stu-id="860c4-151">The `showPrompt` function accepts user input (the user's name), which is HTML-encoded and returned to the `Prompt` method and ultimately back to the component.</span></span> <span data-ttu-id="860c4-152">该组件将用户的名称存储在本地变量中， `name`。</span><span class="sxs-lookup"><span data-stu-id="860c4-152">The component stores the user's name in a local variable, `name`.</span></span>
1. <span data-ttu-id="860c4-153">将字符串存储在`name`合并到一条欢迎消息，后者将传递给第二个C#方法， `ExampleJsInterop.Display`。</span><span class="sxs-lookup"><span data-stu-id="860c4-153">The string stored in `name` is incorporated into a welcome message, which is passed to a second C# method, `ExampleJsInterop.Display`.</span></span>
1. <span data-ttu-id="860c4-154">`Display` 调用 JavaScript 函数， `displayWelcome`，它的标题标记将呈现的欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="860c4-154">`Display` calls a JavaScript function, `displayWelcome`, which renders the welcome message into a heading tag.</span></span>

## <a name="capture-references-to-elements"></a><span data-ttu-id="860c4-155">捕获对元素的引用</span><span class="sxs-lookup"><span data-stu-id="860c4-155">Capture references to elements</span></span>

<span data-ttu-id="860c4-156">某些[JavaScript 互操作](xref:razor-components/javascript-interop)情况下，需要对 HTML 元素的引用。</span><span class="sxs-lookup"><span data-stu-id="860c4-156">Some [JavaScript interop](xref:razor-components/javascript-interop) scenarios require references to HTML elements.</span></span> <span data-ttu-id="860c4-157">例如，用户界面库可能需要元素引用进行初始化，或者可能需要在元素上，调用类似于命令的 Api，例如`focus`或`play`。</span><span class="sxs-lookup"><span data-stu-id="860c4-157">For example, a UI library may require an element reference for initialization, or you might need to call command-like APIs on an element, such as `focus` or `play`.</span></span>

<span data-ttu-id="860c4-158">你可以通过添加捕获对组件中的 HTML 元素的引用`ref`属性的 HTML 元素，然后定义类型的字段`ElementRef`其名称与匹配的值`ref`属性。</span><span class="sxs-lookup"><span data-stu-id="860c4-158">You can capture references to HTML elements in a component by adding a `ref` attribute to the HTML element and then defining a field of type `ElementRef` whose name matches the value of the `ref` attribute.</span></span>

<span data-ttu-id="860c4-159">下面的示例显示了捕获用户名输入元素的引用：</span><span class="sxs-lookup"><span data-stu-id="860c4-159">The following example shows capturing a reference to the username input element:</span></span>

```csharp
<input ref="username" ... />

@functions {
    ElementRef username;
}
```

> [!NOTE]
> <span data-ttu-id="860c4-160">不要**不**作为填充 DOM 的一种方法使用捕获的元素引用</span><span class="sxs-lookup"><span data-stu-id="860c4-160">Do **not** use captured element references as a way of populating the DOM.</span></span> <span data-ttu-id="860c4-161">执行此操作可能会影响声明性呈现模型。</span><span class="sxs-lookup"><span data-stu-id="860c4-161">Doing so may interfere with the declarative rendering model.</span></span>

<span data-ttu-id="860c4-162">就.NET 代码而言，`ElementRef`是不透明的句柄。</span><span class="sxs-lookup"><span data-stu-id="860c4-162">As far as .NET code is concerned, an `ElementRef` is an opaque handle.</span></span> <span data-ttu-id="860c4-163">*仅*可以用它做的事情是通过 JavaScript 互操作将通过其传递给 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="860c4-163">The *only* thing you can do with it is pass it through to JavaScript code via JavaScript interop.</span></span> <span data-ttu-id="860c4-164">当你执行此操作时，在 JavaScript 端代码接收`HTMLElement`实例，它可以与普通的 DOM Api 配合使用。</span><span class="sxs-lookup"><span data-stu-id="860c4-164">When you do so, the JavaScript-side code receives an `HTMLElement` instance, which it can use with normal DOM APIs.</span></span>

<span data-ttu-id="860c4-165">例如，下面的代码定义一个.NET 扩展方法，使将焦点设置在元素上：</span><span class="sxs-lookup"><span data-stu-id="860c4-165">For example, the following code defines a .NET extension method that enables setting the focus on an element:</span></span>

<span data-ttu-id="860c4-166">*mylib.js*:</span><span class="sxs-lookup"><span data-stu-id="860c4-166">*mylib.js*:</span></span>

```javascript
window.myLib = {
  focusElement : function (element) {
    element.focus();
  }
}
```

<span data-ttu-id="860c4-167">*ElementRefExtensions.cs*:</span><span class="sxs-lookup"><span data-stu-id="860c4-167">*ElementRefExtensions.cs*:</span></span>

```csharp
using Microsoft.AspNetCore.Blazor;
using Microsoft.JSInterop;
using System.Threading.Tasks;

namespace MyLib
{
    public static class MyLibElementRefExtensions
    {
        public static Task Focus(this ElementRef elementRef)
        {
            return JSRuntime.Current.InvokeAsync<object>("myLib.focusElement", elementRef);
        }
    }
}
```

<span data-ttu-id="860c4-168">现在您可以在任何你的组件集中输入：</span><span class="sxs-lookup"><span data-stu-id="860c4-168">Now you can focus inputs in any of your components:</span></span>

```cshtml
@using MyLib

<input ref="username" />
<button onclick="@SetFocus">Set focus</button>

@functions {
    ElementRef username;

    void SetFocus()
    {
        username.Focus();
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="860c4-169">`username`组件呈现并包括其输出后，仅填充变量`<input>`元素。</span><span class="sxs-lookup"><span data-stu-id="860c4-169">The `username` variable is only populated after the component renders and its output includes the `<input>` element.</span></span> <span data-ttu-id="860c4-170">如果你尝试传递即便`ElementRef`向 JavaScript 代码的 JavaScript 代码接收`null`。</span><span class="sxs-lookup"><span data-stu-id="860c4-170">If you try to pass an unpopulated `ElementRef` to JavaScript code, the JavaScript code receives `null`.</span></span> <span data-ttu-id="860c4-171">操作元素的引用，该组件已经完成呈现 （将在元素上设置初始焦点） 使用后`OnAfterRenderAsync`或`OnAfterRender`[组件生命周期方法](xref:razor-components/components#lifecycle-methods)。</span><span class="sxs-lookup"><span data-stu-id="860c4-171">To manipulate element references after the component has finished rendering (to set the initial focus on an element) use the `OnAfterRenderAsync` or `OnAfterRender` [component lifecycle methods](xref:razor-components/components#lifecycle-methods).</span></span>

## <a name="invoke-net-methods-from-javascript-functions"></a><span data-ttu-id="860c4-172">调用 JavaScript 函数中的.NET 方法</span><span class="sxs-lookup"><span data-stu-id="860c4-172">Invoke .NET methods from JavaScript functions</span></span>

### <a name="static-net-method-call"></a><span data-ttu-id="860c4-173">静态.NET 方法调用</span><span class="sxs-lookup"><span data-stu-id="860c4-173">Static .NET method call</span></span>

<span data-ttu-id="860c4-174">若要调用静态.NET 方法从 JavaScript，请使用`DotNet.invokeMethod`或`DotNet.invokeMethodAsync`函数。</span><span class="sxs-lookup"><span data-stu-id="860c4-174">To invoke a static .NET method from JavaScript, use the `DotNet.invokeMethod` or `DotNet.invokeMethodAsync` functions.</span></span> <span data-ttu-id="860c4-175">传入你想要调用的函数，并且任何自变量包含的程序集名称的静态方法的标识符。</span><span class="sxs-lookup"><span data-stu-id="860c4-175">Pass in the identifier of the static method you wish to call, the name of the assembly containing the function, and any arguments.</span></span> <span data-ttu-id="860c4-176">同样，被首选的异步版本来支持服务器端的方案。</span><span class="sxs-lookup"><span data-stu-id="860c4-176">Again, the async version is preferred to support server-side scenarios.</span></span> <span data-ttu-id="860c4-177">若要成为可从 JavaScript 调用，.NET 方法必须是公共、 静态的并使用经过修饰`[JSInvokable]`。</span><span class="sxs-lookup"><span data-stu-id="860c4-177">To be invokable from JavaScript, the .NET method must be public, static, and decorated with `[JSInvokable]`.</span></span> <span data-ttu-id="860c4-178">默认情况下，方法标识符是方法名称，但可以指定不同的标识符使用`JSInvokableAttribute`构造函数。</span><span class="sxs-lookup"><span data-stu-id="860c4-178">By default, the method identifier is the method name, but you can specify a different identifier using the `JSInvokableAttribute` constructor.</span></span> <span data-ttu-id="860c4-179">调用开放式泛型方法当前不支持。</span><span class="sxs-lookup"><span data-stu-id="860c4-179">Calling open generic methods isn't currently supported.</span></span>

<span data-ttu-id="860c4-180">示例应用包含C#方法返回的数组`int`s。</span><span class="sxs-lookup"><span data-stu-id="860c4-180">The sample app includes a C# method to return an array of `int`s.</span></span> <span data-ttu-id="860c4-181">该方法用修饰`JSInvokable`属性。</span><span class="sxs-lookup"><span data-stu-id="860c4-181">The method is decorated with the `JSInvokable` attribute.</span></span>

<span data-ttu-id="860c4-182">*Pages/JsInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="860c4-182">*Pages/JsInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=47&end=58&highlight=7-11)]

<span data-ttu-id="860c4-183">客户端的 JavaScript 调用C#.NET 方法。</span><span class="sxs-lookup"><span data-stu-id="860c4-183">JavaScript served to the client invokes the C# .NET method.</span></span>

<span data-ttu-id="860c4-184">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="860c4-184">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-12)]

<span data-ttu-id="860c4-185">当**触发器.NET 静态方法 ReturnArrayAsync**按钮处于选中状态，请查看浏览器的 web 开发人员工具中的控制台输出：</span><span class="sxs-lookup"><span data-stu-id="860c4-185">When the **Trigger .NET static method ReturnArrayAsync** button is selected, examine the console output in the browser's web developer tools:</span></span>

```console
Array(4) [ 1, 2, 3, 4 ]
```

<span data-ttu-id="860c4-186">第四个数组值推送到的数组 (`data.push(4);`) 返回的`ReturnArrayAsync`。</span><span class="sxs-lookup"><span data-stu-id="860c4-186">The fourth array value is pushed to the array (`data.push(4);`) returned by `ReturnArrayAsync`.</span></span>

### <a name="instance-method-call"></a><span data-ttu-id="860c4-187">实例方法调用</span><span class="sxs-lookup"><span data-stu-id="860c4-187">Instance method call</span></span>

<span data-ttu-id="860c4-188">此外可以从 JavaScript 调用.NET 实例方法。</span><span class="sxs-lookup"><span data-stu-id="860c4-188">You can also call .NET instance methods from JavaScript.</span></span> <span data-ttu-id="860c4-189">若要调用的 JavaScript 的.NET 实例方法，第一次的实例传递给.NET 到 JavaScript 通过包装在`DotNetObjectRef`实例。</span><span class="sxs-lookup"><span data-stu-id="860c4-189">To invoke a .NET instance method from JavaScript, first pass the .NET instance to JavaScript by wrapping it in a `DotNetObjectRef` instance.</span></span> <span data-ttu-id="860c4-190">.NET 实例通过引用传递给 JavaScript，并可调用实例使用的.NET 实例方法`invokeMethod`或`invokeMethodAsync`函数。</span><span class="sxs-lookup"><span data-stu-id="860c4-190">The .NET instance is passed by reference to JavaScript, and you can invoke .NET instance methods on the instance using the `invokeMethod` or `invokeMethodAsync` functions.</span></span> <span data-ttu-id="860c4-191">调用其他.NET 方法从 JavaScript 时，还可以作为参数传递.NET 实例。</span><span class="sxs-lookup"><span data-stu-id="860c4-191">The .NET instance can also be passed as an argument when invoking other .NET methods from JavaScript.</span></span>

> [!NOTE]
> <span data-ttu-id="860c4-192">示例应用程序将消息记录到客户端的控制台。</span><span class="sxs-lookup"><span data-stu-id="860c4-192">The sample app logs messages to the client-side console.</span></span> <span data-ttu-id="860c4-193">对于以下示例所演示的示例应用中，检查浏览器的开发人员工具中的浏览器的控制台输出。</span><span class="sxs-lookup"><span data-stu-id="860c4-193">For the following examples demonstrated by the sample app, examine the browser's console output in the browser's developer tools.</span></span>

<span data-ttu-id="860c4-194">当**触发器.NET 实例方法 HelloHelper.SayHello**选择按钮时，`ExampleJsInterop.CallHelloHelperSayHello`调用，并将传递一个名称， `Blazor`，给该方法。</span><span class="sxs-lookup"><span data-stu-id="860c4-194">When the **Trigger .NET instance method HelloHelper.SayHello** button is selected, `ExampleJsInterop.CallHelloHelperSayHello` is called and passes a name, `Blazor`, to the method.</span></span>

<span data-ttu-id="860c4-195">*Pages/JsInterop.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="860c4-195">*Pages/JsInterop.cshtml*:</span></span>

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=60&end=69&highlight=8)]

<span data-ttu-id="860c4-196">`CallHelloHelperSayHello` 调用 JavaScript 函数`sayHello`新实例的`HelloHelper`。</span><span class="sxs-lookup"><span data-stu-id="860c4-196">`CallHelloHelperSayHello` invokes the JavaScript function `sayHello` with a new instance of `HelloHelper`.</span></span>

<span data-ttu-id="860c4-197">*JsInteropClasses/ExampleJsInterop.cs*:</span><span class="sxs-lookup"><span data-stu-id="860c4-197">*JsInteropClasses/ExampleJsInterop.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=19-25)]

<span data-ttu-id="860c4-198">*wwwroot/exampleJsInterop.js*:</span><span class="sxs-lookup"><span data-stu-id="860c4-198">*wwwroot/exampleJsInterop.js*:</span></span>

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-17)]

<span data-ttu-id="860c4-199">名称传递给`HelloHelper`的构造函数中，这会设置`HelloHelper.Name`属性。</span><span class="sxs-lookup"><span data-stu-id="860c4-199">The name is passed to `HelloHelper`'s constructor, which sets the `HelloHelper.Name` property.</span></span> <span data-ttu-id="860c4-200">当 JavaScript 函数`sayHello`执行时，`HelloHelper.SayHello`返回`Hello, {Name}!`消息，通过 JavaScript 函数写入到控制台。</span><span class="sxs-lookup"><span data-stu-id="860c4-200">When the JavaScript function `sayHello` is executed, `HelloHelper.SayHello` returns the `Hello, {Name}!` message, which is written to the console by the JavaScript function.</span></span>

<span data-ttu-id="860c4-201">*JsInteropClasses/HelloHelper.cs*:</span><span class="sxs-lookup"><span data-stu-id="860c4-201">*JsInteropClasses/HelloHelper.cs*:</span></span>

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

<span data-ttu-id="860c4-202">控制台输出中浏览器的 web 开发人员工具：</span><span class="sxs-lookup"><span data-stu-id="860c4-202">Console output in the browser's web developer tools:</span></span>

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a><span data-ttu-id="860c4-203">共享组件 Razor 类库中的互操作代码</span><span class="sxs-lookup"><span data-stu-id="860c4-203">Share interop code in a Razor Component class library</span></span>

<span data-ttu-id="860c4-204">可以在 Razor 组件的类库中包含 JavaScript 互操作代码 (`dotnet new blazorlib`)，这样您就可以共享 NuGet 程序包中的代码。</span><span class="sxs-lookup"><span data-stu-id="860c4-204">JavaScript interop code can be included in a Razor Component class library (`dotnet new blazorlib`), which allows you to share the code in a NuGet package.</span></span>

<span data-ttu-id="860c4-205">Razor 组件类库处理生成的程序集中嵌入的 JavaScript 资源。</span><span class="sxs-lookup"><span data-stu-id="860c4-205">The Razor Component class library handles embedding JavaScript resources in the built assembly.</span></span> <span data-ttu-id="860c4-206">JavaScript 文件将放入*wwwroot*文件夹中和工具处理的嵌入资源生成库时。</span><span class="sxs-lookup"><span data-stu-id="860c4-206">The JavaScript files are placed in the *wwwroot* folder, and the tooling takes care of embedding the resources when the library is built.</span></span>

<span data-ttu-id="860c4-207">就像引用任何普通的 NuGet 包，生成的 NuGet 程序包引用在项目文件中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="860c4-207">The built NuGet package is referenced in the project file of the app just as any normal NuGet package is referenced.</span></span> <span data-ttu-id="860c4-208">就像已还原应用程序后，应用程序代码可以调用到 JavaScript C#。</span><span class="sxs-lookup"><span data-stu-id="860c4-208">After the app has been restored, app code can call into JavaScript as if it were C#.</span></span>
