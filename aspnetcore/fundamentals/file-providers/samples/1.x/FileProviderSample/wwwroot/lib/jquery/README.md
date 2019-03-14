---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028274"
---
# <a name="jquery"></a><span data-ttu-id="2aa73-101">jQuery</span><span class="sxs-lookup"><span data-stu-id="2aa73-101">jQuery</span></span>

> <span data-ttu-id="2aa73-102">jQuery 是一个快速且功能丰富的小型 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="2aa73-102">jQuery is a fast, small, and feature-rich JavaScript library.</span></span>

<span data-ttu-id="2aa73-103">有关如何入门以及如何使用 jQuery 的信息，请参阅 [jQuery 的文档](http://api.jquery.com/)。</span><span class="sxs-lookup"><span data-stu-id="2aa73-103">For information on how to get started and how to use jQuery, please see [jQuery's documentation](http://api.jquery.com/).</span></span>
<span data-ttu-id="2aa73-104">有关源文件和问题，请访问 [jQuery 存储库](https://github.com/jquery/jquery)。</span><span class="sxs-lookup"><span data-stu-id="2aa73-104">For source files and issues, please visit the [jQuery repo](https://github.com/jquery/jquery).</span></span>

<span data-ttu-id="2aa73-105">如果要升级，请参阅 [3.3.1 的博客文章](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/)。</span><span class="sxs-lookup"><span data-stu-id="2aa73-105">If upgrading, please see the [blog post for 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span></span> <span data-ttu-id="2aa73-106">其中包括来自以前的版本和更具可读性的更改日志的明显差异。</span><span class="sxs-lookup"><span data-stu-id="2aa73-106">This includes notable differences from the previous version and a more readable changelog.</span></span>

## <a name="including-jquery"></a><span data-ttu-id="2aa73-107">包含 jQuery</span><span class="sxs-lookup"><span data-stu-id="2aa73-107">Including jQuery</span></span>

<span data-ttu-id="2aa73-108">下面是包含 jQuery 的一些最常用方法。</span><span class="sxs-lookup"><span data-stu-id="2aa73-108">Below are some of the most common ways to include jQuery.</span></span>

### <a name="browser"></a><span data-ttu-id="2aa73-109">浏览者</span><span class="sxs-lookup"><span data-stu-id="2aa73-109">Browser</span></span>

#### <a name="script-tag"></a><span data-ttu-id="2aa73-110">脚本标记</span><span class="sxs-lookup"><span data-stu-id="2aa73-110">Script tag</span></span>

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a><span data-ttu-id="2aa73-111">Babel</span><span class="sxs-lookup"><span data-stu-id="2aa73-111">Babel</span></span>

<span data-ttu-id="2aa73-112">[Babel](http://babeljs.io/) 是下一代 JavaScript 编译器。</span><span class="sxs-lookup"><span data-stu-id="2aa73-112">[Babel](http://babeljs.io/) is a next generation JavaScript compiler.</span></span> <span data-ttu-id="2aa73-113">它其中一个功能是现在能够使用 ES6/ES2015 模块，即使浏览器在本机尚不支持此功能也是如此。</span><span class="sxs-lookup"><span data-stu-id="2aa73-113">One of the features is the ability to use ES6/ES2015 modules now, even though browsers do not yet support this feature natively.</span></span>

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a><span data-ttu-id="2aa73-114">Browserify/Webpack</span><span class="sxs-lookup"><span data-stu-id="2aa73-114">Browserify/Webpack</span></span>

<span data-ttu-id="2aa73-115">可以通过多种方式使用 [Browserify](http://browserify.org/) 和 [Webpack](https://webpack.github.io/)。</span><span class="sxs-lookup"><span data-stu-id="2aa73-115">There are several ways to use [Browserify](http://browserify.org/) and [Webpack](https://webpack.github.io/).</span></span> <span data-ttu-id="2aa73-116">有关使用这些工具的详细信息，请参阅相应项目的文档。</span><span class="sxs-lookup"><span data-stu-id="2aa73-116">For more information on using these tools, please refer to the corresponding project's documention.</span></span> <span data-ttu-id="2aa73-117">在脚本中包含 jQuery 通常如下所示：</span><span class="sxs-lookup"><span data-stu-id="2aa73-117">In the script, including jQuery will usually look like this...</span></span>

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a><span data-ttu-id="2aa73-118">AMD（异步模块定义）</span><span class="sxs-lookup"><span data-stu-id="2aa73-118">AMD (Asynchronous Module Definition)</span></span>

<span data-ttu-id="2aa73-119">AMD 是为浏览器构建的模块格式。</span><span class="sxs-lookup"><span data-stu-id="2aa73-119">AMD is a module format built for the browser.</span></span> <span data-ttu-id="2aa73-120">有关详细信息，建议参阅 [require.js 文档](http://requirejs.org/docs/whyamd.html)。</span><span class="sxs-lookup"><span data-stu-id="2aa73-120">For more information, we recommend [require.js' documentation](http://requirejs.org/docs/whyamd.html).</span></span>

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a><span data-ttu-id="2aa73-121">节点</span><span class="sxs-lookup"><span data-stu-id="2aa73-121">Node</span></span>

<span data-ttu-id="2aa73-122">若要在 [Node](nodejs.org) 中包含 jQuery，首先使用 npm 安装。</span><span class="sxs-lookup"><span data-stu-id="2aa73-122">To include jQuery in [Node](nodejs.org), first install with npm.</span></span>

```sh
npm install jquery
```

<span data-ttu-id="2aa73-123">若要使 jQuery 在 Node 中正常运行，需要一个包含文档的窗口。</span><span class="sxs-lookup"><span data-stu-id="2aa73-123">For jQuery to work in Node, a window with a document is required.</span></span> <span data-ttu-id="2aa73-124">由于 Node 中没有以本机方式存在的此类窗口，可以使用 [jsdom](https://github.com/tmpvar/jsdom) 等工具模拟一个窗口。</span><span class="sxs-lookup"><span data-stu-id="2aa73-124">Since no such window exists natively in Node, one can be mocked by tools such as [jsdom](https://github.com/tmpvar/jsdom).</span></span> <span data-ttu-id="2aa73-125">这可用于测试目的。</span><span class="sxs-lookup"><span data-stu-id="2aa73-125">This can be useful for testing purposes.</span></span>

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
