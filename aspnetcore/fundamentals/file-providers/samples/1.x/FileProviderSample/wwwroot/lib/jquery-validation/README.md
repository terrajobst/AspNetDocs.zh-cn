---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029984"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="800a3-101">[jQuery 验证插件](https://jqueryvalidation.org/) - 轻松实现窗体验证</span><span class="sxs-lookup"><span data-stu-id="800a3-101">[jQuery Validation Plugin](https://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="800a3-102">[![生成状态](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency 状态](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="800a3-102">[![Build Status](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency Status](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="800a3-103">jQuery 验证插件提供对现有窗体的嵌入式验证，同时使各种自定义轻松适应你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="800a3-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="getting-started"></a><span data-ttu-id="800a3-104">入门</span><span class="sxs-lookup"><span data-stu-id="800a3-104">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="800a3-105">下载预生成文件</span><span class="sxs-lookup"><span data-stu-id="800a3-105">Downloading the prebuilt files</span></span>

<span data-ttu-id="800a3-106">可从 https://jqueryvalidation.org/ 下载预生成文件</span><span class="sxs-lookup"><span data-stu-id="800a3-106">Prebuilt files can be downloaded from https://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="800a3-107">下载最新更改</span><span class="sxs-lookup"><span data-stu-id="800a3-107">Downloading the latest changes</span></span>

<span data-ttu-id="800a3-108">可以通过以下方式获取未发布的开发文件：</span><span class="sxs-lookup"><span data-stu-id="800a3-108">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="800a3-109">[下载](https://github.com/jquery-validation/jquery-validation/archive/master.zip)此存储库或创建分支</span><span class="sxs-lookup"><span data-stu-id="800a3-109">[Downloading](https://github.com/jquery-validation/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="800a3-110">设置生成</span><span class="sxs-lookup"><span data-stu-id="800a3-110">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="800a3-111">运行 `grunt` 以在“dist”目录中创建生成文件</span><span class="sxs-lookup"><span data-stu-id="800a3-111">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="800a3-112">将其包括在你的页面上</span><span class="sxs-lookup"><span data-stu-id="800a3-112">Including it on your page</span></span>

<span data-ttu-id="800a3-113">将 jQuery 和插件包括在页面上。</span><span class="sxs-lookup"><span data-stu-id="800a3-113">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="800a3-114">然后选择窗体以验证并调用 `validate` 方法。</span><span class="sxs-lookup"><span data-stu-id="800a3-114">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="800a3-115">或者通过 requirejs 在模块中纳入 jQuery 和插件。</span><span class="sxs-lookup"><span data-stu-id="800a3-115">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="800a3-116">有关如何设置规则和自定义的详细信息，请[检查文档](https://jqueryvalidation.org/documentation/)。</span><span class="sxs-lookup"><span data-stu-id="800a3-116">For more information on how to setup a rules and customizations, [check the documentation](https://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="800a3-117">报告问题和发布代码</span><span class="sxs-lookup"><span data-stu-id="800a3-117">Reporting issues and contributing code</span></span>

<span data-ttu-id="800a3-118">有关详细信息，请参阅[参与准则](CONTRIBUTING.md)。</span><span class="sxs-lookup"><span data-stu-id="800a3-118">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="800a3-119">关于电子邮件验证的重要提示。</span><span class="sxs-lookup"><span data-stu-id="800a3-119">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="800a3-120">从版本 1.12.0 开始，该插件使用与 [HTML5 规范建议浏览器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)的相同的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="800a3-120">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="800a3-121">我们将遵循其指示并使用相同的检查。</span><span class="sxs-lookup"><span data-stu-id="800a3-121">We will follow their lead and use the same check.</span></span> <span data-ttu-id="800a3-122">如果你认为该规范是错误的，请向其报告问题。</span><span class="sxs-lookup"><span data-stu-id="800a3-122">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="800a3-123">如果你有不同的要求，请考虑[使用自定义方法](https://jqueryvalidation.org/jQuery.validator.addMethod/)。</span><span class="sxs-lookup"><span data-stu-id="800a3-123">If you have different requirements, consider [using a custom method](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>
<span data-ttu-id="800a3-124">如果你需要调整内置验证正则表达式模式，请[按照文档说明操作](https://jqueryvalidation.org/jQuery.validator.methods/)。</span><span class="sxs-lookup"><span data-stu-id="800a3-124">In case you need to adjust the built-in validation regular expression patterns, please [follow the documentation](https://jqueryvalidation.org/jQuery.validator.methods/).</span></span>

<span data-ttu-id="800a3-125">**有关必需方法的重要说明**。</span><span class="sxs-lookup"><span data-stu-id="800a3-125">**IMPORTANT NOTE ABOUT REQUIRED METHOD**.</span></span> <span data-ttu-id="800a3-126">从版本 1.14.0 开始，此插件将停止从附加的元素的值修整空白字符。</span><span class="sxs-lookup"><span data-stu-id="800a3-126">As of version 1.14.0 this plugin stops trimming white spaces from the value of the attached element.</span></span> <span data-ttu-id="800a3-127">如果要获得相同的结果，可以使用 [`normalizer`](https://jqueryvalidation.org/normalizer/) 转换元素值，然后再进行验证。</span><span class="sxs-lookup"><span data-stu-id="800a3-127">If you want to achieve the same result, you can use the [`normalizer`](https://jqueryvalidation.org/normalizer/) that can be used to transform the value of an element before validation.</span></span> <span data-ttu-id="800a3-128">自 `v1.15.0` 开始提供此功能。</span><span class="sxs-lookup"><span data-stu-id="800a3-128">This feature was available since `v1.15.0`.</span></span> <span data-ttu-id="800a3-129">也就是说，可以执行如下操作：</span><span class="sxs-lookup"><span data-stu-id="800a3-129">In other words, you can do something like this:</span></span>
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

## <a name="license"></a><span data-ttu-id="800a3-130">许可证</span><span class="sxs-lookup"><span data-stu-id="800a3-130">License</span></span>
<span data-ttu-id="800a3-131">版权所有 &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="800a3-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="800a3-132">按照 MIT 许可证授予许可。</span><span class="sxs-lookup"><span data-stu-id="800a3-132">Licensed under the MIT license.</span></span>
