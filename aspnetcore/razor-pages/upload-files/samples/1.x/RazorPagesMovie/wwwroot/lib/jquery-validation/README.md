---
ms.openlocfilehash: 1b563a8c0674d51f893415221ca8fab574b78265
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046544"
---
<a name="--"></a>--
================================

<span data-ttu-id="f6c1c-101">[![生成状态](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency 状态](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="f6c1c-101">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="f6c1c-102">jQuery 验证插件提供对现有窗体的嵌入式验证，同时使各种自定义轻松适应你的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-102">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[<span data-ttu-id="f6c1c-103">为项目助力</span><span class="sxs-lookup"><span data-stu-id="f6c1c-103">Help the project</span></span>](http://pledgie.com/campaigns/18159)

<span data-ttu-id="f6c1c-104">[![为项目助力](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="f6c1c-104">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="f6c1c-105">此项目正寻求帮助！</span><span class="sxs-lookup"><span data-stu-id="f6c1c-105">This project is looking for help!</span></span> <span data-ttu-id="f6c1c-106">[你可以为正在进行的 pledgie 活动捐款](http://pledgie.com/campaigns/18159)并帮助宣传。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-106">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="f6c1c-107">如果你已使用该插件或计划使用，请考虑捐赠，无论金额多少都会有帮助。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-107">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="f6c1c-108">你可以在 [pledgie 页](http://pledgie.com/campaigns/18159)上找到款项支出计划。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-108">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="get-started"></a><span data-ttu-id="f6c1c-109">开始操作</span><span class="sxs-lookup"><span data-stu-id="f6c1c-109">Get Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="f6c1c-110">下载预生成文件</span><span class="sxs-lookup"><span data-stu-id="f6c1c-110">Downloading the prebuilt files</span></span>

<span data-ttu-id="f6c1c-111">可从 http://jqueryvalidation.org/ 下载预生成文件</span><span class="sxs-lookup"><span data-stu-id="f6c1c-111">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="f6c1c-112">下载最新更改</span><span class="sxs-lookup"><span data-stu-id="f6c1c-112">Downloading the latest changes</span></span>

<span data-ttu-id="f6c1c-113">可以通过以下方式获取未发布的开发文件：</span><span class="sxs-lookup"><span data-stu-id="f6c1c-113">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="f6c1c-114">[下载](https://github.com/jzaefferer/jquery-validation/archive/master.zip)此存储库或创建分支</span><span class="sxs-lookup"><span data-stu-id="f6c1c-114">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="f6c1c-115">设置生成</span><span class="sxs-lookup"><span data-stu-id="f6c1c-115">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="f6c1c-116">运行 `grunt` 以在“dist”目录中创建生成文件</span><span class="sxs-lookup"><span data-stu-id="f6c1c-116">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="f6c1c-117">将其包括在你的页面上</span><span class="sxs-lookup"><span data-stu-id="f6c1c-117">Including it on your page</span></span>

<span data-ttu-id="f6c1c-118">将 jQuery 和插件包括在页面上。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-118">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="f6c1c-119">然后选择窗体以验证并调用 `validate` 方法。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-119">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="f6c1c-120">或者通过 requirejs 在模块中纳入 jQuery 和插件。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-120">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="f6c1c-121">有关如何设置规则和自定义的详细信息，请[检查文档](http://jqueryvalidation.org/documentation/)。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-121">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="f6c1c-122">报告问题和发布代码</span><span class="sxs-lookup"><span data-stu-id="f6c1c-122">Reporting issues and contributing code</span></span>

<span data-ttu-id="f6c1c-123">有关详细信息，请参阅[参与准则](CONTRIBUTING.md)。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-123">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="f6c1c-124">关于电子邮件验证的重要提示。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-124">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="f6c1c-125">从版本 1.12.0 开始，该插件使用与 [HTML5 规范建议浏览器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)的相同的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-125">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="f6c1c-126">我们将遵循其指示并使用相同的检查。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-126">We will follow their lead and use the same check.</span></span> <span data-ttu-id="f6c1c-127">如果你认为该规范是错误的，请向其报告问题。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-127">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="f6c1c-128">如果你有不同的要求，请考虑[使用自定义方法](http://jqueryvalidation.org/jQuery.validator.addMethod/)。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-128">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="f6c1c-129">许可证</span><span class="sxs-lookup"><span data-stu-id="f6c1c-129">License</span></span>
<span data-ttu-id="f6c1c-130">版权所有 &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="f6c1c-130">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="f6c1c-131">按照 MIT 许可证授予许可。</span><span class="sxs-lookup"><span data-stu-id="f6c1c-131">Licensed under the MIT license.</span></span>
