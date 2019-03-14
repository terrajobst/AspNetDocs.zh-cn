---
ms.openlocfilehash: 1f36b95063094e891c1e6b44fbf4ee7546853d89
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57038944"
---
# <a name="contributing-to-the-jquery-validation-plugin"></a><span data-ttu-id="af884-101">贡献 jQuery 验证插件</span><span class="sxs-lookup"><span data-stu-id="af884-101">Contributing to the jQuery Validation Plugin</span></span>

## <a name="reporting-an-issue"></a><span data-ttu-id="af884-102">报告问题</span><span class="sxs-lookup"><span data-stu-id="af884-102">Reporting an Issue</span></span>

1. <span data-ttu-id="af884-103">确保要解决的问题是可重现的。</span><span class="sxs-lookup"><span data-stu-id="af884-103">Make sure the problem you're addressing is reproducible.</span></span>
2. <span data-ttu-id="af884-104">使用 http://jsbin.com 或 http://jsfiddle.net 提供测试页。</span><span class="sxs-lookup"><span data-stu-id="af884-104">Use http://jsbin.com or http://jsfiddle.net to provide a test page.</span></span>
3. <span data-ttu-id="af884-105">指明此问题可在什么浏览器中重现。</span><span class="sxs-lookup"><span data-stu-id="af884-105">Indicate what browsers the issue can be reproduced in.</span></span> <span data-ttu-id="af884-106">**注意：不会解决 IE 兼容性模式问题。请确保在真实的浏览器环境中测试！**</span><span class="sxs-lookup"><span data-stu-id="af884-106">**Note: IE Compatibilty mode issues will not be addressed. Make sure you test in a real browser!**</span></span>
4. <span data-ttu-id="af884-107">哪个版本的插件可重现此问题。</span><span class="sxs-lookup"><span data-stu-id="af884-107">What version of the plug-in is the issue reproducible in.</span></span> <span data-ttu-id="af884-108">是否在更新到最新版本后重现。</span><span class="sxs-lookup"><span data-stu-id="af884-108">Is it reproducible after updating to the latest version.</span></span>

<span data-ttu-id="af884-109">文档问题也在 [jQuery 验证](https://github.com/jzaefferer/jquery-validation/issues) 问题跟踪程序中进行跟踪。</span><span class="sxs-lookup"><span data-stu-id="af884-109">Documentation issues are also tracked at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="af884-110">但是，用于改进文档的拉取请求在 [jQuery 验证文档](https://github.com/jzaefferer/validation-content)存储库中很受欢迎。</span><span class="sxs-lookup"><span data-stu-id="af884-110">Pull Requests to improve the docs are welcome at the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository, though.</span></span>

<span data-ttu-id="af884-111">关于电子邮件验证的重要提示。</span><span class="sxs-lookup"><span data-stu-id="af884-111">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="af884-112">从版本 1.12.0 开始，该插件使用与 [HTML5 规范建议浏览器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)的相同的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="af884-112">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="af884-113">我们将遵循其指示并使用相同的检查。</span><span class="sxs-lookup"><span data-stu-id="af884-113">We will follow their lead and use the same check.</span></span> <span data-ttu-id="af884-114">如果你认为该规范是错误的，请向其报告问题。</span><span class="sxs-lookup"><span data-stu-id="af884-114">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="af884-115">如果你有不同的要求，请考虑[使用自定义方法](http://jqueryvalidation.org/jQuery.validator.addMethod/)。</span><span class="sxs-lookup"><span data-stu-id="af884-115">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="contributing-code"></a><span data-ttu-id="af884-116">发布代码</span><span class="sxs-lookup"><span data-stu-id="af884-116">Contributing code</span></span>

<span data-ttu-id="af884-117">感谢参与！</span><span class="sxs-lookup"><span data-stu-id="af884-117">Thanks for contributing!</span></span> <span data-ttu-id="af884-118">下面是一些帮助你将参与落到实处的准则。</span><span class="sxs-lookup"><span data-stu-id="af884-118">Here's a few guidelines to help your contribution get landed.</span></span>

1. <span data-ttu-id="af884-119">确保要解决的问题是可重现的。</span><span class="sxs-lookup"><span data-stu-id="af884-119">Make sure the problem you're addressing is reproducible.</span></span> <span data-ttu-id="af884-120">使用 jsbin.com 或 jsfiddle.net 提供测试页。</span><span class="sxs-lookup"><span data-stu-id="af884-120">Use jsbin.com or jsfiddle.net to provide a test page.</span></span>
2. <span data-ttu-id="af884-121">请遵照 [jQuery 样式指南](http://contribute.jquery.com/style-guides/js)</span><span class="sxs-lookup"><span data-stu-id="af884-121">Follow the [jQuery style guide](http://contribute.jquery.com/style-guides/js)</span></span>
3. <span data-ttu-id="af884-122">添加或更新单元测试以及修补程序。</span><span class="sxs-lookup"><span data-stu-id="af884-122">Add or update unit tests along with your patch.</span></span> <span data-ttu-id="af884-123">至少在一个浏览器中运行单元测试（请参见下文）。</span><span class="sxs-lookup"><span data-stu-id="af884-123">Run the unit tests in at least one browser (see below).</span></span>
4. <span data-ttu-id="af884-124">运行 `grunt`（请参见下文）以检查 linting 和一些其他问题。</span><span class="sxs-lookup"><span data-stu-id="af884-124">Run `grunt` (see below) to check for linting and a few other issues.</span></span>
5. <span data-ttu-id="af884-125">提交消息中描述更改并引用了票证，如下："演示：已修复 dynamic-totals 演示的委托 bug。</span><span class="sxs-lookup"><span data-stu-id="af884-125">Describe the change in your commit message and reference the ticket, like this: "Demos: Fixed delegate bug for dynamic-totals demo.</span></span> <span data-ttu-id="af884-126">Fixes #51”。</span><span class="sxs-lookup"><span data-stu-id="af884-126">Fixes #51".</span></span> <span data-ttu-id="af884-127">如果要添加新的本地化文件，使用类似如下代码："本地化：已添加克罗地亚语 (HR) 本地化"</span><span class="sxs-lookup"><span data-stu-id="af884-127">If you're adding a new localization file, use something like this: "Localization: Added croatian (HR) localization"</span></span>

## <a name="build-setup"></a><span data-ttu-id="af884-128">生成设置</span><span class="sxs-lookup"><span data-stu-id="af884-128">Build setup</span></span>

1. <span data-ttu-id="af884-129">安装 [NodeJS](http://nodejs.org)。</span><span class="sxs-lookup"><span data-stu-id="af884-129">Install [NodeJS](http://nodejs.org).</span></span>
2. <span data-ttu-id="af884-130">通过运行 `npm install -g grunt-cli` 安装 Grunt CLI。</span><span class="sxs-lookup"><span data-stu-id="af884-130">Install the Grunt CLI To install by running `npm install -g grunt-cli`.</span></span> <span data-ttu-id="af884-131">可访问其网站 http://gruntjs.com/getting-started 获取更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="af884-131">More details are available on their website http://gruntjs.com/getting-started.</span></span>
3. <span data-ttu-id="af884-132">通过运行 `npm install` 安装 NPM 依赖关系。</span><span class="sxs-lookup"><span data-stu-id="af884-132">Install the NPM dependencies by running `npm install`.</span></span>
4. <span data-ttu-id="af884-133">现在可以通过运行 `grunt` 调用生成。</span><span class="sxs-lookup"><span data-stu-id="af884-133">The build can now be called by running `grunt`.</span></span>

## <a name="creating-a-new-additional-method"></a><span data-ttu-id="af884-134">新建附加方法</span><span class="sxs-lookup"><span data-stu-id="af884-134">Creating a new Additional Method</span></span>

<span data-ttu-id="af884-135">如果你已编写想要加入 additional-methods.js 的自定义方法：</span><span class="sxs-lookup"><span data-stu-id="af884-135">If you've wrote custom methods that you'd like to contribute to additional-methods.js:</span></span>

1. <span data-ttu-id="af884-136">创建分支</span><span class="sxs-lookup"><span data-stu-id="af884-136">Create a branch</span></span>
2. <span data-ttu-id="af884-137">在 `src/additional` 中将方法添加为新文件</span><span class="sxs-lookup"><span data-stu-id="af884-137">Add the method as a new file in `src/additional`</span></span>
3. <span data-ttu-id="af884-138">（可选）将翻译添加到 `src/localization`</span><span class="sxs-lookup"><span data-stu-id="af884-138">(Optional) Add translations to `src/localization`</span></span>
4. <span data-ttu-id="af884-139">将拉取请求发送到主分支。</span><span class="sxs-lookup"><span data-stu-id="af884-139">Send a pull request to the master branch.</span></span>

## <a name="unit-tests"></a><span data-ttu-id="af884-140">单元测试</span><span class="sxs-lookup"><span data-stu-id="af884-140">Unit Tests</span></span>

<span data-ttu-id="af884-141">要运行单元测试，只需在浏览器中打开 `test/index.html` 即可。</span><span class="sxs-lookup"><span data-stu-id="af884-141">To run unit tests, just open `test/index.html` within your browser.</span></span> <span data-ttu-id="af884-142">请确保在所需的所有依赖关系可用之前运行 `npm install`。</span><span class="sxs-lookup"><span data-stu-id="af884-142">Make sure you ran `npm install` before so all required dependencies are available.</span></span>
<span data-ttu-id="af884-143">开发修补程序时从一个浏览器开始，然后在提交之前针对其他浏览器运行。</span><span class="sxs-lookup"><span data-stu-id="af884-143">Start with one browser while developing the fix, then run against others before committing.</span></span> <span data-ttu-id="af884-144">通常是最新的 Chrome、Firefox、Safari 和 Opera 以及几个 IE。</span><span class="sxs-lookup"><span data-stu-id="af884-144">Usually latest Chrome, Firefox, Safari and Opera and a few IEs.</span></span>

## <a name="documentation"></a><span data-ttu-id="af884-145">文档</span><span class="sxs-lookup"><span data-stu-id="af884-145">Documentation</span></span>

<span data-ttu-id="af884-146">请在 [jQuery 验证](https://github.com/jzaefferer/jquery-validation/issues)问题跟踪程序中报告文档问题。</span><span class="sxs-lookup"><span data-stu-id="af884-146">Please report documentation issues at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="af884-147">如果你的拉取请求实现或更改了公共 API（这是一个附加项），那么你应该提供针对 [jQuery 验证文档](https://github.com/jzaefferer/validation-content)存储库的拉取请求。</span><span class="sxs-lookup"><span data-stu-id="af884-147">In case your pull request implements or changes public API it would be a plus you would provide a pull request against the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository.</span></span>

## <a name="linting"></a><span data-ttu-id="af884-148">Linting</span><span class="sxs-lookup"><span data-stu-id="af884-148">Linting</span></span>

<span data-ttu-id="af884-149">若要运行 JSHint 和其他工具，使用 `grunt`。</span><span class="sxs-lookup"><span data-stu-id="af884-149">To run JSHint and other tools, use `grunt`.</span></span>
