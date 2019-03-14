---
ms.openlocfilehash: 7eb0f9b556f0663a5208310d2d4864eca28f8632
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57057344"
---
# <a name="contributing-to-the-jquery-validation-plugin"></a><span data-ttu-id="1f066-101">贡献 jQuery 验证插件</span><span class="sxs-lookup"><span data-stu-id="1f066-101">Contributing to the jQuery Validation Plugin</span></span>

## <a name="reporting-an-issue"></a><span data-ttu-id="1f066-102">报告问题</span><span class="sxs-lookup"><span data-stu-id="1f066-102">Reporting an Issue</span></span>

1. <span data-ttu-id="1f066-103">确保要解决的问题是可重现的。</span><span class="sxs-lookup"><span data-stu-id="1f066-103">Make sure the problem you're addressing is reproducible.</span></span>
2. <span data-ttu-id="1f066-104">使用 https://jsbin.com 或 https://jsfiddle.net 提供测试页。</span><span class="sxs-lookup"><span data-stu-id="1f066-104">Use https://jsbin.com or https://jsfiddle.net to provide a test page.</span></span>
3. <span data-ttu-id="1f066-105">指明此问题可在什么浏览器中重现。</span><span class="sxs-lookup"><span data-stu-id="1f066-105">Indicate what browsers the issue can be reproduced in.</span></span> <span data-ttu-id="1f066-106">**注意：不会解决 IE 兼容性模式问题。请确保在真实的浏览器环境中测试！**</span><span class="sxs-lookup"><span data-stu-id="1f066-106">**Note: IE Compatibilty mode issues will not be addressed. Make sure you test in a real browser!**</span></span>
4. <span data-ttu-id="1f066-107">哪个版本的插件可重现此问题。</span><span class="sxs-lookup"><span data-stu-id="1f066-107">What version of the plug-in is the issue reproducible in.</span></span> <span data-ttu-id="1f066-108">是否在更新到最新版本后重现。</span><span class="sxs-lookup"><span data-stu-id="1f066-108">Is it reproducible after updating to the latest version.</span></span>

<span data-ttu-id="1f066-109">文档问题也在 [jQuery 验证](https://github.com/jquery-validation/jquery-validation/issues) 问题跟踪程序中进行跟踪。</span><span class="sxs-lookup"><span data-stu-id="1f066-109">Documentation issues are also tracked at the [jQuery Validation](https://github.com/jquery-validation/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="1f066-110">但是，用于改进文档的拉取请求在 [jQuery 验证文档](https://github.com/jquery-validation/validation-content)存储库中很受欢迎。</span><span class="sxs-lookup"><span data-stu-id="1f066-110">Pull Requests to improve the docs are welcome at the [jQuery Validation docs](https://github.com/jquery-validation/validation-content) repository, though.</span></span>

<span data-ttu-id="1f066-111">关于电子邮件验证的重要提示。</span><span class="sxs-lookup"><span data-stu-id="1f066-111">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="1f066-112">从版本 1.12.0 开始，该插件使用与 [HTML5 规范建议浏览器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)的相同的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="1f066-112">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="1f066-113">我们将遵循其指示并使用相同的检查。</span><span class="sxs-lookup"><span data-stu-id="1f066-113">We will follow their lead and use the same check.</span></span> <span data-ttu-id="1f066-114">如果你认为该规范是错误的，请向其报告问题。</span><span class="sxs-lookup"><span data-stu-id="1f066-114">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="1f066-115">如果你有不同的要求，请考虑[使用自定义方法](http://jqueryvalidation.org/jQuery.validator.addMethod/)。</span><span class="sxs-lookup"><span data-stu-id="1f066-115">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>
<span data-ttu-id="1f066-116">如果你需要调整内置验证正则表达式模式，请[按照文档说明操作](http://jqueryvalidation.org/jQuery.validator.methods/)。</span><span class="sxs-lookup"><span data-stu-id="1f066-116">In case you need to adjust the built-in validation regular expression patterns, please [follow the documentation](http://jqueryvalidation.org/jQuery.validator.methods/).</span></span>

## <a name="contributing-code"></a><span data-ttu-id="1f066-117">发布代码</span><span class="sxs-lookup"><span data-stu-id="1f066-117">Contributing code</span></span>

<span data-ttu-id="1f066-118">感谢参与！</span><span class="sxs-lookup"><span data-stu-id="1f066-118">Thanks for contributing!</span></span> <span data-ttu-id="1f066-119">下面是一些帮助你将参与落到实处的准则。</span><span class="sxs-lookup"><span data-stu-id="1f066-119">Here's a few guidelines to help your contribution get landed.</span></span>

1. <span data-ttu-id="1f066-120">确保要解决的问题是可重现的。</span><span class="sxs-lookup"><span data-stu-id="1f066-120">Make sure the problem you're addressing is reproducible.</span></span> <span data-ttu-id="1f066-121">使用 jsbin.com 或 jsfiddle.net 提供测试页。</span><span class="sxs-lookup"><span data-stu-id="1f066-121">Use jsbin.com or jsfiddle.net to provide a test page.</span></span>
2. <span data-ttu-id="1f066-122">请遵照 [jQuery 样式指南](http://contribute.jquery.com/style-guides/js)</span><span class="sxs-lookup"><span data-stu-id="1f066-122">Follow the [jQuery style guide](http://contribute.jquery.com/style-guides/js)</span></span>
3. <span data-ttu-id="1f066-123">添加或更新单元测试以及修补程序。</span><span class="sxs-lookup"><span data-stu-id="1f066-123">Add or update unit tests along with your patch.</span></span> <span data-ttu-id="1f066-124">至少在一个浏览器中运行单元测试（请参见下文）。</span><span class="sxs-lookup"><span data-stu-id="1f066-124">Run the unit tests in at least one browser (see below).</span></span>
4. <span data-ttu-id="1f066-125">运行 `grunt`（请参见下文）以检查 linting 和一些其他问题。</span><span class="sxs-lookup"><span data-stu-id="1f066-125">Run `grunt` (see below) to check for linting and a few other issues.</span></span>
5. <span data-ttu-id="1f066-126">提交消息中描述更改并引用了票证，如下："演示：已修复 dynamic-totals 演示的委托 bug。</span><span class="sxs-lookup"><span data-stu-id="1f066-126">Describe the change in your commit message and reference the ticket, like this: "Demos: Fixed delegate bug for dynamic-totals demo.</span></span> <span data-ttu-id="1f066-127">Fixes #51”。</span><span class="sxs-lookup"><span data-stu-id="1f066-127">Fixes #51".</span></span> <span data-ttu-id="1f066-128">如果要添加新的本地化文件，使用类似如下代码："本地化：已添加克罗地亚语 (HR) 本地化"</span><span class="sxs-lookup"><span data-stu-id="1f066-128">If you're adding a new localization file, use something like this: "Localization: Added croatian (HR) localization"</span></span>

## <a name="build-setup"></a><span data-ttu-id="1f066-129">生成设置</span><span class="sxs-lookup"><span data-stu-id="1f066-129">Build setup</span></span>

1. <span data-ttu-id="1f066-130">安装 [NodeJS](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="1f066-130">Install [NodeJS](http://nodejs.org).</span></span>
2. <span data-ttu-id="1f066-131">通过运行 `npm install -g grunt-cli` 安装 Grunt CLI。</span><span class="sxs-lookup"><span data-stu-id="1f066-131">Install the Grunt CLI To install by running `npm install -g grunt-cli`.</span></span> <span data-ttu-id="1f066-132">可访问其网站 http://gruntjs.com/getting-started 获取更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="1f066-132">More details are available on their website http://gruntjs.com/getting-started.</span></span>
3. <span data-ttu-id="1f066-133">通过运行 `npm install` 安装 NPM 依赖关系。</span><span class="sxs-lookup"><span data-stu-id="1f066-133">Install the NPM dependencies by running `npm install`.</span></span>
4. <span data-ttu-id="1f066-134">现在可以通过运行 `grunt` 调用生成。</span><span class="sxs-lookup"><span data-stu-id="1f066-134">The build can now be called by running `grunt`.</span></span>

## <a name="creating-a-new-additional-method"></a><span data-ttu-id="1f066-135">新建附加方法</span><span class="sxs-lookup"><span data-stu-id="1f066-135">Creating a new Additional Method</span></span>

<span data-ttu-id="1f066-136">如果你已编写想要加入 additional-methods.js 的自定义方法：</span><span class="sxs-lookup"><span data-stu-id="1f066-136">If you've wrote custom methods that you'd like to contribute to additional-methods.js:</span></span>

1. <span data-ttu-id="1f066-137">创建分支</span><span class="sxs-lookup"><span data-stu-id="1f066-137">Create a branch</span></span>
2. <span data-ttu-id="1f066-138">在 `src/additional` 中将方法添加为新文件</span><span class="sxs-lookup"><span data-stu-id="1f066-138">Add the method as a new file in `src/additional`</span></span>
3. <span data-ttu-id="1f066-139">（可选）将翻译添加到 `src/localization`</span><span class="sxs-lookup"><span data-stu-id="1f066-139">(Optional) Add translations to `src/localization`</span></span>
4. <span data-ttu-id="1f066-140">将拉取请求发送到主分支。</span><span class="sxs-lookup"><span data-stu-id="1f066-140">Send a pull request to the master branch.</span></span>

## <a name="unit-tests"></a><span data-ttu-id="1f066-141">单元测试</span><span class="sxs-lookup"><span data-stu-id="1f066-141">Unit Tests</span></span>

<span data-ttu-id="1f066-142">要运行单元测试，只需在浏览器中打开 `test/index.html` 即可。</span><span class="sxs-lookup"><span data-stu-id="1f066-142">To run unit tests, just open `test/index.html` within your browser.</span></span> <span data-ttu-id="1f066-143">请确保在所需的所有依赖关系可用之前运行 `npm install`。</span><span class="sxs-lookup"><span data-stu-id="1f066-143">Make sure you ran `npm install` before so all required dependencies are available.</span></span>
<span data-ttu-id="1f066-144">开发修补程序时从一个浏览器开始，然后在提交之前针对其他浏览器运行。</span><span class="sxs-lookup"><span data-stu-id="1f066-144">Start with one browser while developing the fix, then run against others before committing.</span></span> <span data-ttu-id="1f066-145">通常是最新的 Chrome、Firefox、Safari 和 Opera 以及几个 IE。</span><span class="sxs-lookup"><span data-stu-id="1f066-145">Usually latest Chrome, Firefox, Safari and Opera and a few IEs.</span></span>

## <a name="documentation"></a><span data-ttu-id="1f066-146">文档</span><span class="sxs-lookup"><span data-stu-id="1f066-146">Documentation</span></span>

<span data-ttu-id="1f066-147">请在 [jQuery 验证](https://github.com/jquery-validation/jquery-validation/issues)问题跟踪程序中报告文档问题。</span><span class="sxs-lookup"><span data-stu-id="1f066-147">Please report documentation issues at the [jQuery Validation](https://github.com/jquery-validation/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="1f066-148">如果你的拉取请求实现或更改了公共 API（这是一个附加项），那么你应该提供针对 [jQuery 验证文档](https://github.com/jquery-validation/validation-content)存储库的拉取请求。</span><span class="sxs-lookup"><span data-stu-id="1f066-148">In case your pull request implements or changes public API it would be a plus you would provide a pull request against the [jQuery Validation docs](https://github.com/jquery-validation/validation-content) repository.</span></span>

## <a name="linting"></a><span data-ttu-id="1f066-149">Linting</span><span class="sxs-lookup"><span data-stu-id="1f066-149">Linting</span></span>

<span data-ttu-id="1f066-150">若要运行 JSHint 和其他工具，使用 `grunt`。</span><span class="sxs-lookup"><span data-stu-id="1f066-150">To run JSHint and other tools, use `grunt`.</span></span>
