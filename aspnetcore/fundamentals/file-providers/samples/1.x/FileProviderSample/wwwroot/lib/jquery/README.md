---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028274"
---
# <a name="jquery"></a>jQuery

> jQuery 是一个快速且功能丰富的小型 JavaScript 库。

有关如何入门以及如何使用 jQuery 的信息，请参阅 [jQuery 的文档](http://api.jquery.com/)。
有关源文件和问题，请访问 [jQuery 存储库](https://github.com/jquery/jquery)。

如果要升级，请参阅 [3.3.1 的博客文章](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/)。 其中包括来自以前的版本和更具可读性的更改日志的明显差异。

## <a name="including-jquery"></a>包含 jQuery

下面是包含 jQuery 的一些最常用方法。

### <a name="browser"></a>浏览者

#### <a name="script-tag"></a>脚本标记

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a>Babel

[Babel](http://babeljs.io/) 是下一代 JavaScript 编译器。 它其中一个功能是现在能够使用 ES6/ES2015 模块，即使浏览器在本机尚不支持此功能也是如此。

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a>Browserify/Webpack

可以通过多种方式使用 [Browserify](http://browserify.org/) 和 [Webpack](https://webpack.github.io/)。 有关使用这些工具的详细信息，请参阅相应项目的文档。 在脚本中包含 jQuery 通常如下所示：

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a>AMD（异步模块定义）

AMD 是为浏览器构建的模块格式。 有关详细信息，建议参阅 [require.js 文档](http://requirejs.org/docs/whyamd.html)。

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a>节点

若要在 [Node](nodejs.org) 中包含 jQuery，首先使用 npm 安装。

```sh
npm install jquery
```

若要使 jQuery 在 Node 中正常运行，需要一个包含文档的窗口。 由于 Node 中没有以本机方式存在的此类窗口，可以使用 [jsdom](https://github.com/tmpvar/jsdom) 等工具模拟一个窗口。 这可用于测试目的。

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
