---
ms.openlocfilehash: f60f934934ae9e16bbd1174959d99aecdbb5833d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57040944"
---
--

<span data-ttu-id="16d55-101">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower 版本](https://img.shields.io/bower/v/bootstrap.svg)
[![npm 版本](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![生成状态](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency 状态](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium 测试状态](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span><span class="sxs-lookup"><span data-stu-id="16d55-101">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower version](https://img.shields.io/bower/v/bootstrap.svg)
[![npm version](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![Build Status](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency Status](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium Test Status](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span></span>

<span data-ttu-id="16d55-102">Bootstrap 是一个时尚、直观且功能强大的前端框架，可加快和简化 Web 开发过程，由 [Mark Otto](https://twitter.com/mdo) 和 [Jacob Thornton](https://twitter.com/fat) 创建并由[核心团队](https://github.com/orgs/twbs/people)维护，得到了社区的大力支持和参与。</span><span class="sxs-lookup"><span data-stu-id="16d55-102">Bootstrap is a sleek, intuitive, and powerful front-end framework for faster and easier web development, created by [Mark Otto](https://twitter.com/mdo) and [Jacob Thornton](https://twitter.com/fat), and maintained by the [core team](https://github.com/orgs/twbs/people) with the massive support and involvement of the community.</span></span>

<span data-ttu-id="16d55-103">要开始使用，请查看 <http://getbootstrap.com>！</span><span class="sxs-lookup"><span data-stu-id="16d55-103">To get started, check out <http://getbootstrap.com>!</span></span>


## <a name="table-of-contents"></a><span data-ttu-id="16d55-104">目录</span><span class="sxs-lookup"><span data-stu-id="16d55-104">Table of contents</span></span>

* [<span data-ttu-id="16d55-105">快速入门</span><span class="sxs-lookup"><span data-stu-id="16d55-105">Quick start</span></span>](#quick-start)
* [<span data-ttu-id="16d55-106">Bug 和功能请求</span><span class="sxs-lookup"><span data-stu-id="16d55-106">Bugs and feature requests</span></span>](#bugs-and-feature-requests)
* [<span data-ttu-id="16d55-107">文档</span><span class="sxs-lookup"><span data-stu-id="16d55-107">Documentation</span></span>](#documentation)
* [<span data-ttu-id="16d55-108">参与</span><span class="sxs-lookup"><span data-stu-id="16d55-108">Contributing</span></span>](#contributing)
* [<span data-ttu-id="16d55-109">Community</span><span class="sxs-lookup"><span data-stu-id="16d55-109">Community</span></span>](#community)
* [<span data-ttu-id="16d55-110">版本控制</span><span class="sxs-lookup"><span data-stu-id="16d55-110">Versioning</span></span>](#versioning)
* [<span data-ttu-id="16d55-111">创建者</span><span class="sxs-lookup"><span data-stu-id="16d55-111">Creators</span></span>](#creators)
* [<span data-ttu-id="16d55-112">版权和许可</span><span class="sxs-lookup"><span data-stu-id="16d55-112">Copyright and license</span></span>](#copyright-and-license)


## <a name="quick-start"></a><span data-ttu-id="16d55-113">快速入门</span><span class="sxs-lookup"><span data-stu-id="16d55-113">Quick start</span></span>

<span data-ttu-id="16d55-114">提供了几个快速入门选项：</span><span class="sxs-lookup"><span data-stu-id="16d55-114">Several quick start options are available:</span></span>

* <span data-ttu-id="16d55-115">[下载最新版本](https://github.com/twbs/bootstrap/archive/v3.3.7.zip)。</span><span class="sxs-lookup"><span data-stu-id="16d55-115">[Download the latest release](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).</span></span>
* <span data-ttu-id="16d55-116">克隆存储库：`git clone https://github.com/twbs/bootstrap.git`。</span><span class="sxs-lookup"><span data-stu-id="16d55-116">Clone the repo: `git clone https://github.com/twbs/bootstrap.git`.</span></span>
* <span data-ttu-id="16d55-117">通过 [Bower](http://bower.io) 安装：`bower install bootstrap`。</span><span class="sxs-lookup"><span data-stu-id="16d55-117">Install with [Bower](http://bower.io): `bower install bootstrap`.</span></span>
* <span data-ttu-id="16d55-118">通过 [npm](https://www.npmjs.com) 安装：`npm install bootstrap@3`。</span><span class="sxs-lookup"><span data-stu-id="16d55-118">Install with [npm](https://www.npmjs.com): `npm install bootstrap@3`.</span></span>
* <span data-ttu-id="16d55-119">通过 [Meteor](https://www.meteor.com) 安装：`meteor add twbs:bootstrap`。</span><span class="sxs-lookup"><span data-stu-id="16d55-119">Install with [Meteor](https://www.meteor.com): `meteor add twbs:bootstrap`.</span></span>
* <span data-ttu-id="16d55-120">通过 [Composer](https://getcomposer.org) 安装：`composer require twbs/bootstrap`。</span><span class="sxs-lookup"><span data-stu-id="16d55-120">Install with [Composer](https://getcomposer.org): `composer require twbs/bootstrap`.</span></span>

<span data-ttu-id="16d55-121">有关框架内容、模板和示例的信息，请参考[入门页](http://getbootstrap.com/getting-started/)。</span><span class="sxs-lookup"><span data-stu-id="16d55-121">Read the [Getting started page](http://getbootstrap.com/getting-started/) for information on the framework contents, templates and examples, and more.</span></span>

### <a name="whats-included"></a><span data-ttu-id="16d55-122">包含的组件</span><span class="sxs-lookup"><span data-stu-id="16d55-122">What's included</span></span>

<span data-ttu-id="16d55-123">在下载项中，你可以找到以下目录和文件，从逻辑上将常用资源分组并提供编译和缩减的变体。</span><span class="sxs-lookup"><span data-stu-id="16d55-123">Within the download you'll find the following directories and files, logically grouping common assets and providing both compiled and minified variations.</span></span> <span data-ttu-id="16d55-124">你将看到类似如下内容：</span><span class="sxs-lookup"><span data-stu-id="16d55-124">You'll see something like this:</span></span>

```
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/
    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2
```

<span data-ttu-id="16d55-125">我们提供编译的 CSS 和 JS (`bootstrap.*`)，以及编译和缩减的 CSS 和 JS (`bootstrap.min.*`)。</span><span class="sxs-lookup"><span data-stu-id="16d55-125">We provide compiled CSS and JS (`bootstrap.*`), as well as compiled and minified CSS and JS (`bootstrap.min.*`).</span></span> <span data-ttu-id="16d55-126">CSS [source maps](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) 可用于某些浏览器的开发人员工具。</span><span class="sxs-lookup"><span data-stu-id="16d55-126">CSS [source maps](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) are available for use with certain browsers' developer tools.</span></span> <span data-ttu-id="16d55-127">由于是可选的 Bootstrap 主题，包括 Glyphicons 的字体。</span><span class="sxs-lookup"><span data-stu-id="16d55-127">Fonts from Glyphicons are included, as is the optional Bootstrap theme.</span></span>


## <a name="bugs-and-feature-requests"></a><span data-ttu-id="16d55-128">Bug 和功能请求</span><span class="sxs-lookup"><span data-stu-id="16d55-128">Bugs and feature requests</span></span>

<span data-ttu-id="16d55-129">有 bug 或功能请求？</span><span class="sxs-lookup"><span data-stu-id="16d55-129">Have a bug or a feature request?</span></span> <span data-ttu-id="16d55-130">请先阅读[问题准则](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker)，然后搜索现有和已关闭的问题。</span><span class="sxs-lookup"><span data-stu-id="16d55-130">Please first read the [issue guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) and search for existing and closed issues.</span></span> <span data-ttu-id="16d55-131">如果你的问题或想法尚未得到解决，[请开启一个新问题](https://github.com/twbs/bootstrap/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="16d55-131">If your problem or idea isn't addressed yet, [please open a new issue](https://github.com/twbs/bootstrap/issues/new).</span></span>

<span data-ttu-id="16d55-132">请注意，**功能请求必须针对 [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev)，** 因为 Bootstrap v3 现在处于维护模式并关闭各项新功能。</span><span class="sxs-lookup"><span data-stu-id="16d55-132">Note that **feature requests must target [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev),** because Bootstrap v3 is now in maintenance mode and is closed off to new features.</span></span> <span data-ttu-id="16d55-133">这样我们就可以将精力重点放在 Bootstrap v4 上。</span><span class="sxs-lookup"><span data-stu-id="16d55-133">This is so that we can focus our efforts on Bootstrap v4.</span></span>


## <a name="documentation"></a><span data-ttu-id="16d55-134">文档</span><span class="sxs-lookup"><span data-stu-id="16d55-134">Documentation</span></span>

<span data-ttu-id="16d55-135">Bootstrap 的文档包含在根目录的这个存储库中，它是通过 [Jekyll](http://jekyllrb.com) 构建的，并公开托管在 <http://getbootstrap.com> 的 GitHub 页上。</span><span class="sxs-lookup"><span data-stu-id="16d55-135">Bootstrap's documentation, included in this repo in the root directory, is built with [Jekyll](http://jekyllrb.com) and publicly hosted on GitHub Pages at <http://getbootstrap.com>.</span></span> <span data-ttu-id="16d55-136">文档还可以在本地运行。</span><span class="sxs-lookup"><span data-stu-id="16d55-136">The docs may also be run locally.</span></span>

### <a name="running-documentation-locally"></a><span data-ttu-id="16d55-137">在本地运行文档</span><span class="sxs-lookup"><span data-stu-id="16d55-137">Running documentation locally</span></span>

1. <span data-ttu-id="16d55-138">如有必要，请通过 `bundle install` [安装 Jekyll](http://jekyllrb.com/docs/installation) 与其他 Ruby 依赖关系。</span><span class="sxs-lookup"><span data-stu-id="16d55-138">If necessary, [install Jekyll](http://jekyllrb.com/docs/installation) and other Ruby dependencies with `bundle install`.</span></span>
   <span data-ttu-id="16d55-139">**针对 Windows 用户的说明：** 读取[非正式指南](http://jekyll-windows.juthilo.com/)获取 Jekyll 启动并运行，而问题。</span><span class="sxs-lookup"><span data-stu-id="16d55-139">**Note for Windows users:** Read [this unofficial guide](http://jekyll-windows.juthilo.com/) to get Jekyll up and running without problems.</span></span>
2. <span data-ttu-id="16d55-140">从根 `/bootstrap` 目录在命令行中运行 `bundle exec jekyll serve`。</span><span class="sxs-lookup"><span data-stu-id="16d55-140">From the root `/bootstrap` directory, run `bundle exec jekyll serve` in the command line.</span></span>
4. <span data-ttu-id="16d55-141">在你的浏览器中打开 `http://localhost:9001`。</span><span class="sxs-lookup"><span data-stu-id="16d55-141">Open `http://localhost:9001` in your browser, and voilà.</span></span>

<span data-ttu-id="16d55-142">阅读[文档](http://jekyllrb.com/docs/home/)以了解有关使用 Jekyll 的更多信息。</span><span class="sxs-lookup"><span data-stu-id="16d55-142">Learn more about using Jekyll by reading its [documentation](http://jekyllrb.com/docs/home/).</span></span>

### <a name="documentation-for-previous-releases"></a><span data-ttu-id="16d55-143">以前版本的文档</span><span class="sxs-lookup"><span data-stu-id="16d55-143">Documentation for previous releases</span></span>

<span data-ttu-id="16d55-144">v2.3.2 文档现已在 <http://getbootstrap.com/2.3.2/> 上提供，人们可以转换到 Bootstrap 3。</span><span class="sxs-lookup"><span data-stu-id="16d55-144">Documentation for v2.3.2 has been made available for the time being at <http://getbootstrap.com/2.3.2/> while folks transition to Bootstrap 3.</span></span>

<span data-ttu-id="16d55-145">[以前版本](https://github.com/twbs/bootstrap/releases)及其文档也已可供下载。</span><span class="sxs-lookup"><span data-stu-id="16d55-145">[Previous releases](https://github.com/twbs/bootstrap/releases) and their documentation are also available for download.</span></span>


## <a name="contributing"></a><span data-ttu-id="16d55-146">参与</span><span class="sxs-lookup"><span data-stu-id="16d55-146">Contributing</span></span>

<span data-ttu-id="16d55-147">请阅读我们的[参与准则](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md)。</span><span class="sxs-lookup"><span data-stu-id="16d55-147">Please read through our [contributing guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md).</span></span> <span data-ttu-id="16d55-148">其中包括有关打开问题、标准编码和开发说明的指导。</span><span class="sxs-lookup"><span data-stu-id="16d55-148">Included are directions for opening issues, coding standards, and notes on development.</span></span>

<span data-ttu-id="16d55-149">此外，如果你的拉取请求包含 JavaScript 修补程序或功能，则必须包含[相关单元测试](https://github.com/twbs/bootstrap/tree/master/js/tests)。</span><span class="sxs-lookup"><span data-stu-id="16d55-149">Moreover, if your pull request contains JavaScript patches or features, you must include [relevant unit tests](https://github.com/twbs/bootstrap/tree/master/js/tests).</span></span> <span data-ttu-id="16d55-150">所有 HTML 和 CSS 都应符合[代码指南](https://github.com/mdo/code-guide)（由 [Mark Otto](https://github.com/mdo) 维护）。</span><span class="sxs-lookup"><span data-stu-id="16d55-150">All HTML and CSS should conform to the [Code Guide](https://github.com/mdo/code-guide), maintained by [Mark Otto](https://github.com/mdo).</span></span>

<span data-ttu-id="16d55-151">**Bootstrap v3 现已关闭各项新功能。**</span><span class="sxs-lookup"><span data-stu-id="16d55-151">**Bootstrap v3 is now closed off to new features.**</span></span> <span data-ttu-id="16d55-152">它已进入维护模式，以便我们可以将精力重点放在将来的框架 [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev) 上。</span><span class="sxs-lookup"><span data-stu-id="16d55-152">It has gone into maintenance mode so that we can focus our efforts on [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev), the future of the framework.</span></span> <span data-ttu-id="16d55-153">添加新功能（而不是修复 bug）的拉取请求应面向 [Bootstrap v4（`v4-dev` git 分支）](https://github.com/twbs/bootstrap/tree/v4-dev)。</span><span class="sxs-lookup"><span data-stu-id="16d55-153">Pull requests which add new features (rather than fix bugs) should target [Bootstrap v4 (the `v4-dev` git branch)](https://github.com/twbs/bootstrap/tree/v4-dev) instead.</span></span>

<span data-ttu-id="16d55-154">编辑器首选项位于[编辑器配置](https://github.com/twbs/bootstrap/blob/master/.editorconfig)中，方便在通用文本编辑器中使用。</span><span class="sxs-lookup"><span data-stu-id="16d55-154">Editor preferences are available in the [editor config](https://github.com/twbs/bootstrap/blob/master/.editorconfig) for easy use in common text editors.</span></span> <span data-ttu-id="16d55-155">请访问 <http://editorconfig.org> 了解详细信息并下载插件。</span><span class="sxs-lookup"><span data-stu-id="16d55-155">Read more and download plugins at <http://editorconfig.org>.</span></span>


## <a name="community"></a><span data-ttu-id="16d55-156">社区</span><span class="sxs-lookup"><span data-stu-id="16d55-156">Community</span></span>

<span data-ttu-id="16d55-157">获取 Bootstrap 开发的更新，与项目维护人员和社区成员交流。</span><span class="sxs-lookup"><span data-stu-id="16d55-157">Get updates on Bootstrap's development and chat with the project maintainers and community members.</span></span>

* <span data-ttu-id="16d55-158">[@getbootstrap在 Twitter](https://twitter.com/getbootstrap) 上关注。</span><span class="sxs-lookup"><span data-stu-id="16d55-158">Follow [@getbootstrap on Twitter](https://twitter.com/getbootstrap).</span></span>
* <span data-ttu-id="16d55-159">阅读并订阅 [Bootstrap 官方博客](http://blog.getbootstrap.com)。</span><span class="sxs-lookup"><span data-stu-id="16d55-159">Read and subscribe to [The Official Bootstrap Blog](http://blog.getbootstrap.com).</span></span>
* <span data-ttu-id="16d55-160">加入[官方 Slack 聊天室](https://bootstrap-slack.herokuapp.com)。</span><span class="sxs-lookup"><span data-stu-id="16d55-160">Join [the official Slack room](https://bootstrap-slack.herokuapp.com).</span></span>
* <span data-ttu-id="16d55-161">在 IRC 与其他 Bootstrap 同行聊天。</span><span class="sxs-lookup"><span data-stu-id="16d55-161">Chat with fellow Bootstrappers in IRC.</span></span> <span data-ttu-id="16d55-162">在 `irc.freenode.net` 服务器上，`##bootstrap` 频道。</span><span class="sxs-lookup"><span data-stu-id="16d55-162">On the `irc.freenode.net` server, in the `##bootstrap` channel.</span></span>
* <span data-ttu-id="16d55-163">可以在堆栈溢出（标记为 [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)）中找到实现帮助。</span><span class="sxs-lookup"><span data-stu-id="16d55-163">Implementation help may be found at Stack Overflow (tagged [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).</span></span>
* <span data-ttu-id="16d55-164">在通过 [npm](https://www.npmjs.com/browse/keyword/bootstrap) 或类似的交付机制进行分发以实现最大的可发现性时，开发人员应在修改或添加到 Bootstrap 功能的软件包中使用关键字 `bootstrap`。</span><span class="sxs-lookup"><span data-stu-id="16d55-164">Developers should use the keyword `bootstrap` on packages which modify or add to the functionality of Bootstrap when distributing through [npm](https://www.npmjs.com/browse/keyword/bootstrap) or similar delivery mechanisms for maximum discoverability.</span></span>


## <a name="versioning"></a><span data-ttu-id="16d55-165">版本管理</span><span class="sxs-lookup"><span data-stu-id="16d55-165">Versioning</span></span>

<span data-ttu-id="16d55-166">为了使我们的发布周期更加透明并努力保持向后兼容性，根据[语义化版本控制准则](http://semver.org/)维护 Bootstrap。</span><span class="sxs-lookup"><span data-stu-id="16d55-166">For transparency into our release cycle and in striving to maintain backward compatibility, Bootstrap is maintained under [the Semantic Versioning guidelines](http://semver.org/).</span></span> <span data-ttu-id="16d55-167">虽然有时会搞砸，但我们会尽可能地遵守这些准则。</span><span class="sxs-lookup"><span data-stu-id="16d55-167">Sometimes we screw up, but we'll adhere to those rules whenever possible.</span></span>

<span data-ttu-id="16d55-168">请参阅 [GitHub 项目的版本部分](https://github.com/twbs/bootstrap/releases)，了解每个 Bootstrap 版本的更改日志。</span><span class="sxs-lookup"><span data-stu-id="16d55-168">See [the Releases section of our GitHub project](https://github.com/twbs/bootstrap/releases) for changelogs for each release version of Bootstrap.</span></span> <span data-ttu-id="16d55-169">[Bootstrap 官方博客](http://blog.getbootstrap.com)上的发行公告帖中包含各版本中最值得注意的更改摘要。</span><span class="sxs-lookup"><span data-stu-id="16d55-169">Release announcement posts on [the official Bootstrap blog](http://blog.getbootstrap.com) contain summaries of the most noteworthy changes made in each release.</span></span>


## <a name="creators"></a><span data-ttu-id="16d55-170">创建者</span><span class="sxs-lookup"><span data-stu-id="16d55-170">Creators</span></span>

<span data-ttu-id="16d55-171">**Mark Otto**</span><span class="sxs-lookup"><span data-stu-id="16d55-171">**Mark Otto**</span></span>

* <https://twitter.com/mdo>
* <https://github.com/mdo>

<span data-ttu-id="16d55-172">**Jacob Thornton**</span><span class="sxs-lookup"><span data-stu-id="16d55-172">**Jacob Thornton**</span></span>

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a><span data-ttu-id="16d55-173">版权和许可</span><span class="sxs-lookup"><span data-stu-id="16d55-173">Copyright and license</span></span>

<span data-ttu-id="16d55-174">代码和文档版权所有 2011-2016 Twitter, Inc.按照 [MIT 许可证](https://github.com/twbs/bootstrap/blob/master/LICENSE)授予许可。</span><span class="sxs-lookup"><span data-stu-id="16d55-174">Code and documentation copyright 2011-2016 Twitter, Inc. Code released under [the MIT license](https://github.com/twbs/bootstrap/blob/master/LICENSE).</span></span> <span data-ttu-id="16d55-175">根据[知识共享](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE)发布的文档。</span><span class="sxs-lookup"><span data-stu-id="16d55-175">Docs released under [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).</span></span>
