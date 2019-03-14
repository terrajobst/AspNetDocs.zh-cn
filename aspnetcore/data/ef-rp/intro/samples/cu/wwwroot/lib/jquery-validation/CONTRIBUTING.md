---
ms.openlocfilehash: 1f36b95063094e891c1e6b44fbf4ee7546853d89
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57050454"
---
# <a name="contributing-to-the-jquery-validation-plugin"></a>贡献 jQuery 验证插件

## <a name="reporting-an-issue"></a>报告问题

1. 确保要解决的问题是可重现的。
2. 使用 http://jsbin.com 或 http://jsfiddle.net 提供测试页。
3. 指明此问题可在什么浏览器中重现。 **注意：不会解决 IE 兼容性模式问题。请确保在真实的浏览器环境中测试！**
4. 哪个版本的插件可重现此问题。 是否在更新到最新版本后重现。

文档问题也在 [jQuery 验证](https://github.com/jzaefferer/jquery-validation/issues) 问题跟踪程序中进行跟踪。
但是，用于改进文档的拉取请求在 [jQuery 验证文档](https://github.com/jzaefferer/validation-content)存储库中很受欢迎。

关于电子邮件验证的重要提示。 从版本 1.12.0 开始，该插件使用与 [HTML5 规范建议浏览器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)的相同的正则表达式。 我们将遵循其指示并使用相同的检查。 如果你认为该规范是错误的，请向其报告问题。 如果你有不同的要求，请考虑[使用自定义方法](http://jqueryvalidation.org/jQuery.validator.addMethod/)。

## <a name="contributing-code"></a>发布代码

感谢参与！ 下面是一些帮助你将参与落到实处的准则。

1. 确保要解决的问题是可重现的。 使用 jsbin.com 或 jsfiddle.net 提供测试页。
2. 请遵照 [jQuery 样式指南](http://contribute.jquery.com/style-guides/js)
3. 添加或更新单元测试以及修补程序。 至少在一个浏览器中运行单元测试（请参见下文）。
4. 运行 `grunt`（请参见下文）以检查 linting 和一些其他问题。
5. 提交消息中描述更改并引用了票证，如下："演示：已修复 dynamic-totals 演示的委托 bug。 Fixes #51”。 如果要添加新的本地化文件，使用类似如下代码："本地化：已添加克罗地亚语 (HR) 本地化"

## <a name="build-setup"></a>生成设置

1. 安装 [NodeJS](http://nodejs.org)。
2. 通过运行 `npm install -g grunt-cli` 安装 Grunt CLI。 可访问其网站 http://gruntjs.com/getting-started 获取更多详细信息。
3. 通过运行 `npm install` 安装 NPM 依赖关系。
4. 现在可以通过运行 `grunt` 调用生成。

## <a name="creating-a-new-additional-method"></a>新建附加方法

如果你已编写想要加入 additional-methods.js 的自定义方法：

1. 创建分支
2. 在 `src/additional` 中将方法添加为新文件
3. （可选）将翻译添加到 `src/localization`
4. 将拉取请求发送到主分支。

## <a name="unit-tests"></a>单元测试

要运行单元测试，只需在浏览器中打开 `test/index.html` 即可。 请确保在所需的所有依赖关系可用之前运行 `npm install`。
开发修补程序时从一个浏览器开始，然后在提交之前针对其他浏览器运行。 通常是最新的 Chrome、Firefox、Safari 和 Opera 以及几个 IE。

## <a name="documentation"></a>文档

请在 [jQuery 验证](https://github.com/jzaefferer/jquery-validation/issues)问题跟踪程序中报告文档问题。
如果你的拉取请求实现或更改了公共 API（这是一个附加项），那么你应该提供针对 [jQuery 验证文档](https://github.com/jzaefferer/validation-content)存储库的拉取请求。

## <a name="linting"></a>Linting

若要运行 JSHint 和其他工具，使用 `grunt`。
