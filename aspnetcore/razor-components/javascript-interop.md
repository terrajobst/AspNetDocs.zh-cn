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
# <a name="razor-components-javascript-interop"></a>Razor JavaScript 组件互操作

通过[Javier Calvarro Nelson](https://github.com/javiercn)， [Daniel Roth](https://github.com/danroth27)，和[Luke Latham](https://github.com/guardrex)

Razor 组件应用程序可以调用 JavaScript 函数，从.NET 和.NET 中的 JavaScript 代码的方法。

## <a name="invoke-javascript-functions-from-net-methods"></a>调用 JavaScript 函数的.NET 方法

有些的时候需要调用 JavaScript 函数的.NET 代码时。 例如，浏览器功能或从 JavaScript 库向应用程序的功能，可以公开 JavaScript 调用。

若要从.NET 调用的 JavaScript，请使用`IJSRuntime`抽象。 `InvokeAsync<T>`方法`IJSRuntime`采用你想要与任意数量的 JSON 可序列化参数一起调用的 JavaScript 函数的标识符。 函数标识符是相对于全局作用域 (`window`)。 如果你想要调用`window.someScope.someFunction`，该标识符是`someScope.someFunction`。 没有无需注册该函数之前调用它。 返回类型`T`还必须是 JSON 可序列化。

对于服务器端 ASP.NET Core Razor 组件应用程序：

* 由服务器端应用程序处理多个用户请求。 不要调用`JSRuntime.Current`组件调用 JavaScript 函数中。
* 注入`IJSRuntime`抽象和使用注入的对象发出 JavaScript 互操作调用。

下面的示例基于[TextDecoder](https://developer.mozilla.org/docs/Web/API/TextDecoder)，实验性的基于 JavaScript 的解码器。 该示例演示如何调用一个 JavaScript 函数中的C#方法。 JavaScript 函数接受字节数组从C#方法，对数组进行解码并返回到显示的组件的文本。

内部`<head>`的元素*wwwroot/index.html*，提供一个函数来使用`TextDecoder`传递的数组进行解码：

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

此外可以通过对中的脚本文件的引用的 JavaScript 文件加载 JavaScript 代码，例如在前面的示例所示的代码*wwwroot/index.html*文件。

以下组件：

* 调用`ConvertArray`JavaScript 函数使用`JsRuntime`的组件按钮时 (**转换数组**) 处于选中状态。
* JavaScript 函数调用之后，则将传递的数组转换为字符串。 供显示的组件返回的字符串。

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

对于客户端 Blazor 应用，`IJSRuntime`抽象是可从访问`JSRuntime.Current`，这是指当前用户的请求。 由于只有一个用户的客户端 Blazor 应用程序，使用`JSRuntime.Current`调用 JavaScript 函数通常会正常工作。 只能使用`JSRuntime.Current`客户端 Blazor 应用中。

在客户端的示例应用中本主题附带，两个 JavaScript 函数可供与 DOM 来接收用户输入并显示一条欢迎消息进行交互的客户端应用：

* `showPrompt` &ndash; 生成提示接受用户输入 （用户的名称），并返回给调用方的名称。
* `displayWelcome` &ndash; 将一条欢迎消息从调用方分配给具有的 DOM 对象`id`的`welcome`。

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=2-7)]

位置`<script>`引用的 JavaScript 文件中的标记*wwwroot/index.html*文件：

[!code-html[](./common/samples/3.x/BlazorSample/wwwroot/index.html?highlight=16)]

不要将组件文件中的脚本标记，因为无法动态更新的脚本标记。

使用通过调用 JavaScript 函数的.NET 方法互操作`InvokeAsync<T>`方法`IJSRuntime`。

示例应用使用一对C#方法，`Prompt`并`Display`，以调用`showPrompt`并`displayWelcome`JavaScript 函数：

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=6-8,14-16)]

`IJSRuntime`抽象是异步模式，以允许服务器端的方案。 如果应用在运行客户端，并且你想要调用的 JavaScript 函数以同步方式，向下转换到`IJSInProcessRuntime`，并调用`Invoke<T>`相反。 我们建议，大多数 JavaScript 库的互操作使用异步 Api，以确保库是在所有方案，客户端或服务器端中可用。

示例应用包含用于演示 JS 互操作的组件。 组件：

* 接收通过 JS 提示用户输入。
* 返回对组件进行处理的文本。
* 调用与 DOM 以显示一条欢迎消息进行交互的第二个 JS 函数。

*Pages/JSInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=1&end=21&highlight=2-3,9-11,13,16-20)]

1. 当`TriggerJsPrompt`选择该组件的执行**触发器 JavaScript 提示**按钮，`ExampleJsInterop.Prompt`中的方法C#调用代码。
1. `Prompt`方法执行 JavaScript`showPrompt`函数中提供*wwwroot/exampleJsInterop.js*文件。
1. `showPrompt`函数可接受用户输入 （用户的名称），这是 HTML 编码并返回到`Prompt`方法并最终返回到该组件。 该组件将用户的名称存储在本地变量中， `name`。
1. 将字符串存储在`name`合并到一条欢迎消息，后者将传递给第二个C#方法， `ExampleJsInterop.Display`。
1. `Display` 调用 JavaScript 函数， `displayWelcome`，它的标题标记将呈现的欢迎消息。

## <a name="capture-references-to-elements"></a>捕获对元素的引用

某些[JavaScript 互操作](xref:razor-components/javascript-interop)情况下，需要对 HTML 元素的引用。 例如，用户界面库可能需要元素引用进行初始化，或者可能需要在元素上，调用类似于命令的 Api，例如`focus`或`play`。

你可以通过添加捕获对组件中的 HTML 元素的引用`ref`属性的 HTML 元素，然后定义类型的字段`ElementRef`其名称与匹配的值`ref`属性。

下面的示例显示了捕获用户名输入元素的引用：

```csharp
<input ref="username" ... />

@functions {
    ElementRef username;
}
```

> [!NOTE]
> 不要**不**作为填充 DOM 的一种方法使用捕获的元素引用 执行此操作可能会影响声明性呈现模型。

就.NET 代码而言，`ElementRef`是不透明的句柄。 *仅*可以用它做的事情是通过 JavaScript 互操作将通过其传递给 JavaScript 代码。 当你执行此操作时，在 JavaScript 端代码接收`HTMLElement`实例，它可以与普通的 DOM Api 配合使用。

例如，下面的代码定义一个.NET 扩展方法，使将焦点设置在元素上：

*mylib.js*:

```javascript
window.myLib = {
  focusElement : function (element) {
    element.focus();
  }
}
```

*ElementRefExtensions.cs*:

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

现在您可以在任何你的组件集中输入：

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
> `username`组件呈现并包括其输出后，仅填充变量`<input>`元素。 如果你尝试传递即便`ElementRef`向 JavaScript 代码的 JavaScript 代码接收`null`。 操作元素的引用，该组件已经完成呈现 （将在元素上设置初始焦点） 使用后`OnAfterRenderAsync`或`OnAfterRender`[组件生命周期方法](xref:razor-components/components#lifecycle-methods)。

## <a name="invoke-net-methods-from-javascript-functions"></a>调用 JavaScript 函数中的.NET 方法

### <a name="static-net-method-call"></a>静态.NET 方法调用

若要调用静态.NET 方法从 JavaScript，请使用`DotNet.invokeMethod`或`DotNet.invokeMethodAsync`函数。 传入你想要调用的函数，并且任何自变量包含的程序集名称的静态方法的标识符。 同样，被首选的异步版本来支持服务器端的方案。 若要成为可从 JavaScript 调用，.NET 方法必须是公共、 静态的并使用经过修饰`[JSInvokable]`。 默认情况下，方法标识符是方法名称，但可以指定不同的标识符使用`JSInvokableAttribute`构造函数。 调用开放式泛型方法当前不支持。

示例应用包含C#方法返回的数组`int`s。 该方法用修饰`JSInvokable`属性。

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=47&end=58&highlight=7-11)]

客户端的 JavaScript 调用C#.NET 方法。

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=8-12)]

当**触发器.NET 静态方法 ReturnArrayAsync**按钮处于选中状态，请查看浏览器的 web 开发人员工具中的控制台输出：

```console
Array(4) [ 1, 2, 3, 4 ]
```

第四个数组值推送到的数组 (`data.push(4);`) 返回的`ReturnArrayAsync`。

### <a name="instance-method-call"></a>实例方法调用

此外可以从 JavaScript 调用.NET 实例方法。 若要调用的 JavaScript 的.NET 实例方法，第一次的实例传递给.NET 到 JavaScript 通过包装在`DotNetObjectRef`实例。 .NET 实例通过引用传递给 JavaScript，并可调用实例使用的.NET 实例方法`invokeMethod`或`invokeMethodAsync`函数。 调用其他.NET 方法从 JavaScript 时，还可以作为参数传递.NET 实例。

> [!NOTE]
> 示例应用程序将消息记录到客户端的控制台。 对于以下示例所演示的示例应用中，检查浏览器的开发人员工具中的浏览器的控制台输出。

当**触发器.NET 实例方法 HelloHelper.SayHello**选择按钮时，`ExampleJsInterop.CallHelloHelperSayHello`调用，并将传递一个名称， `Blazor`，给该方法。

*Pages/JsInterop.cshtml*:

[!code-cshtml[](./common/samples/3.x/BlazorSample/Pages/JsInterop.cshtml?start=60&end=69&highlight=8)]

`CallHelloHelperSayHello` 调用 JavaScript 函数`sayHello`新实例的`HelloHelper`。

*JsInteropClasses/ExampleJsInterop.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/ExampleJsInterop.cs?name=snippet1&highlight=19-25)]

*wwwroot/exampleJsInterop.js*:

[!code-javascript[](./common/samples/3.x/BlazorSample/wwwroot/exampleJsInterop.js?highlight=15-17)]

名称传递给`HelloHelper`的构造函数中，这会设置`HelloHelper.Name`属性。 当 JavaScript 函数`sayHello`执行时，`HelloHelper.SayHello`返回`Hello, {Name}!`消息，通过 JavaScript 函数写入到控制台。

*JsInteropClasses/HelloHelper.cs*:

[!code-csharp[](./common/samples/3.x/BlazorSample/JsInteropClasses/HelloHelper.cs?name=snippet1&highlight=5,10-11)]

控制台输出中浏览器的 web 开发人员工具：

```console
Hello, Blazor!
```

## <a name="share-interop-code-in-a-razor-component-class-library"></a>共享组件 Razor 类库中的互操作代码

可以在 Razor 组件的类库中包含 JavaScript 互操作代码 (`dotnet new blazorlib`)，这样您就可以共享 NuGet 程序包中的代码。

Razor 组件类库处理生成的程序集中嵌入的 JavaScript 资源。 JavaScript 文件将放入*wwwroot*文件夹中和工具处理的嵌入资源生成库时。

就像引用任何普通的 NuGet 包，生成的 NuGet 程序包引用在项目文件中的应用程序。 就像已还原应用程序后，应用程序代码可以调用到 JavaScript C#。
