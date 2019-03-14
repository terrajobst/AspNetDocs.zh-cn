---
ms.openlocfilehash: f60f934934ae9e16bbd1174959d99aecdbb5833d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57025104"
---
--

[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower 版本](https://img.shields.io/bower/v/bootstrap.svg)
[![npm 版本](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![生成状态](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency 状态](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium 测试状态](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)

Bootstrap 是一个时尚、直观且功能强大的前端框架，可加快和简化 Web 开发过程，由 [Mark Otto](https://twitter.com/mdo) 和 [Jacob Thornton](https://twitter.com/fat) 创建并由[核心团队](https://github.com/orgs/twbs/people)维护，得到了社区的大力支持和参与。

要开始使用，请查看 <http://getbootstrap.com>！


## <a name="table-of-contents"></a>目录

* [快速入门](#quick-start)
* [Bug 和功能请求](#bugs-and-feature-requests)
* [文档](#documentation)
* [参与](#contributing)
* [Community](#community)
* [版本控制](#versioning)
* [创建者](#creators)
* [版权和许可](#copyright-and-license)


## <a name="quick-start"></a>快速入门

提供了几个快速入门选项：

* [下载最新版本](https://github.com/twbs/bootstrap/archive/v3.3.7.zip)。
* 克隆存储库：`git clone https://github.com/twbs/bootstrap.git`。
* 通过 [Bower](http://bower.io) 安装：`bower install bootstrap`。
* 通过 [npm](https://www.npmjs.com) 安装：`npm install bootstrap@3`。
* 通过 [Meteor](https://www.meteor.com) 安装：`meteor add twbs:bootstrap`。
* 通过 [Composer](https://getcomposer.org) 安装：`composer require twbs/bootstrap`。

有关框架内容、模板和示例的信息，请参考[入门页](http://getbootstrap.com/getting-started/)。

### <a name="whats-included"></a>包含的组件

在下载项中，你可以找到以下目录和文件，从逻辑上将常用资源分组并提供编译和缩减的变体。 你将看到类似如下内容：

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

我们提供编译的 CSS 和 JS (`bootstrap.*`)，以及编译和缩减的 CSS 和 JS (`bootstrap.min.*`)。 CSS [source maps](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) 可用于某些浏览器的开发人员工具。 由于是可选的 Bootstrap 主题，包括 Glyphicons 的字体。


## <a name="bugs-and-feature-requests"></a>Bug 和功能请求

有 bug 或功能请求？ 请先阅读[问题准则](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker)，然后搜索现有和已关闭的问题。 如果你的问题或想法尚未得到解决，[请开启一个新问题](https://github.com/twbs/bootstrap/issues/new)。

请注意，**功能请求必须针对 [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev)，** 因为 Bootstrap v3 现在处于维护模式并关闭各项新功能。 这样我们就可以将精力重点放在 Bootstrap v4 上。


## <a name="documentation"></a>文档

Bootstrap 的文档包含在根目录的这个存储库中，它是通过 [Jekyll](http://jekyllrb.com) 构建的，并公开托管在 <http://getbootstrap.com> 的 GitHub 页上。 文档还可以在本地运行。

### <a name="running-documentation-locally"></a>在本地运行文档

1. 如有必要，请通过 `bundle install` [安装 Jekyll](http://jekyllrb.com/docs/installation) 与其他 Ruby 依赖关系。
   **针对 Windows 用户的说明：** 读取[非正式指南](http://jekyll-windows.juthilo.com/)获取 Jekyll 启动并运行，而问题。
2. 从根 `/bootstrap` 目录在命令行中运行 `bundle exec jekyll serve`。
4. 在你的浏览器中打开 `http://localhost:9001`。

阅读[文档](http://jekyllrb.com/docs/home/)以了解有关使用 Jekyll 的更多信息。

### <a name="documentation-for-previous-releases"></a>以前版本的文档

v2.3.2 文档现已在 <http://getbootstrap.com/2.3.2/> 上提供，人们可以转换到 Bootstrap 3。

[以前版本](https://github.com/twbs/bootstrap/releases)及其文档也已可供下载。


## <a name="contributing"></a>参与

请阅读我们的[参与准则](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md)。 其中包括有关打开问题、标准编码和开发说明的指导。

此外，如果你的拉取请求包含 JavaScript 修补程序或功能，则必须包含[相关单元测试](https://github.com/twbs/bootstrap/tree/master/js/tests)。 所有 HTML 和 CSS 都应符合[代码指南](https://github.com/mdo/code-guide)（由 [Mark Otto](https://github.com/mdo) 维护）。

**Bootstrap v3 现已关闭各项新功能。** 它已进入维护模式，以便我们可以将精力重点放在将来的框架 [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev) 上。 添加新功能（而不是修复 bug）的拉取请求应面向 [Bootstrap v4（`v4-dev` git 分支）](https://github.com/twbs/bootstrap/tree/v4-dev)。

编辑器首选项位于[编辑器配置](https://github.com/twbs/bootstrap/blob/master/.editorconfig)中，方便在通用文本编辑器中使用。 请访问 <http://editorconfig.org> 了解详细信息并下载插件。


## <a name="community"></a>社区

获取 Bootstrap 开发的更新，与项目维护人员和社区成员交流。

* [@getbootstrap在 Twitter](https://twitter.com/getbootstrap) 上关注。
* 阅读并订阅 [Bootstrap 官方博客](http://blog.getbootstrap.com)。
* 加入[官方 Slack 聊天室](https://bootstrap-slack.herokuapp.com)。
* 在 IRC 与其他 Bootstrap 同行聊天。 在 `irc.freenode.net` 服务器上，`##bootstrap` 频道。
* 可以在堆栈溢出（标记为 [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)）中找到实现帮助。
* 在通过 [npm](https://www.npmjs.com/browse/keyword/bootstrap) 或类似的交付机制进行分发以实现最大的可发现性时，开发人员应在修改或添加到 Bootstrap 功能的软件包中使用关键字 `bootstrap`。


## <a name="versioning"></a>版本管理

为了使我们的发布周期更加透明并努力保持向后兼容性，根据[语义化版本控制准则](http://semver.org/)维护 Bootstrap。 虽然有时会搞砸，但我们会尽可能地遵守这些准则。

请参阅 [GitHub 项目的版本部分](https://github.com/twbs/bootstrap/releases)，了解每个 Bootstrap 版本的更改日志。 [Bootstrap 官方博客](http://blog.getbootstrap.com)上的发行公告帖中包含各版本中最值得注意的更改摘要。


## <a name="creators"></a>创建者

**Mark Otto**

* <https://twitter.com/mdo>
* <https://github.com/mdo>

**Jacob Thornton**

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a>版权和许可

代码和文档版权所有 2011-2016 Twitter, Inc.按照 [MIT 许可证](https://github.com/twbs/bootstrap/blob/master/LICENSE)授予许可。 根据[知识共享](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE)发布的文档。
