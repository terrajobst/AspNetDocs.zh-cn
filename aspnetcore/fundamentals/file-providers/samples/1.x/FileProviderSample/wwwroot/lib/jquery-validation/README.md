---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029984"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a>[jQuery 验证插件](https://jqueryvalidation.org/) - 轻松实现窗体验证
================================

[![生成状态](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency 状态](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)

jQuery 验证插件提供对现有窗体的嵌入式验证，同时使各种自定义轻松适应你的应用程序。

## <a name="getting-started"></a>入门

### <a name="downloading-the-prebuilt-files"></a>下载预生成文件

可从 https://jqueryvalidation.org/ 下载预生成文件

### <a name="downloading-the-latest-changes"></a>下载最新更改

可以通过以下方式获取未发布的开发文件：

 1. [下载](https://github.com/jquery-validation/jquery-validation/archive/master.zip)此存储库或创建分支
 2. [设置生成](CONTRIBUTING.md#build-setup)
 3. 运行 `grunt` 以在“dist”目录中创建生成文件

### <a name="including-it-on-your-page"></a>将其包括在你的页面上

将 jQuery 和插件包括在页面上。 然后选择窗体以验证并调用 `validate` 方法。

```html
<form>
    <input required>
</form>
<script src="jquery.js"></script>
<script src="jquery.validate.js"></script>
<script>
$("form").validate();
</script>
```

或者通过 requirejs 在模块中纳入 jQuery 和插件。

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

有关如何设置规则和自定义的详细信息，请[检查文档](https://jqueryvalidation.org/documentation/)。

## <a name="reporting-issues-and-contributing-code"></a>报告问题和发布代码

有关详细信息，请参阅[参与准则](CONTRIBUTING.md)。

关于电子邮件验证的重要提示。 从版本 1.12.0 开始，该插件使用与 [HTML5 规范建议浏览器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)的相同的正则表达式。 我们将遵循其指示并使用相同的检查。 如果你认为该规范是错误的，请向其报告问题。 如果你有不同的要求，请考虑[使用自定义方法](https://jqueryvalidation.org/jQuery.validator.addMethod/)。
如果你需要调整内置验证正则表达式模式，请[按照文档说明操作](https://jqueryvalidation.org/jQuery.validator.methods/)。

**有关必需方法的重要说明**。 从版本 1.14.0 开始，此插件将停止从附加的元素的值修整空白字符。 如果要获得相同的结果，可以使用 [`normalizer`](https://jqueryvalidation.org/normalizer/) 转换元素值，然后再进行验证。 自 `v1.15.0` 开始提供此功能。 也就是说，可以执行如下操作：
``` js
$("#myForm").validate({
    rules: {
        username: {
            required: true,
            // Using the normalizer to trim the value of the element
            // before validating it.
            //
            // The value of `this` inside the `normalizer` is the corresponding
            // DOMElement. In this example, `this` references the `username` element.
            normalizer: function(value) {
                return $.trim(value);
            }
        }
    }
});
```

## <a name="license"></a>许可证
版权所有 &copy; Jörn Zaefferer<br>
按照 MIT 许可证授予许可。
