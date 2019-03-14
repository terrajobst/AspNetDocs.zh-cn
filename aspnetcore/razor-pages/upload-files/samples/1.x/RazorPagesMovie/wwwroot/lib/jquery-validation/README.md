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

[![生成状态](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency 状态](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)

jQuery 验证插件提供对现有窗体的嵌入式验证，同时使各种自定义轻松适应你的应用程序。

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[为项目助力](http://pledgie.com/campaigns/18159)

[![为项目助力](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)

此项目正寻求帮助！ [你可以为正在进行的 pledgie 活动捐款](http://pledgie.com/campaigns/18159)并帮助宣传。 如果你已使用该插件或计划使用，请考虑捐赠，无论金额多少都会有帮助。

你可以在 [pledgie 页](http://pledgie.com/campaigns/18159)上找到款项支出计划。

## <a name="get-started"></a>开始操作

### <a name="downloading-the-prebuilt-files"></a>下载预生成文件

可从 http://jqueryvalidation.org/ 下载预生成文件

### <a name="downloading-the-latest-changes"></a>下载最新更改

可以通过以下方式获取未发布的开发文件：

 1. [下载](https://github.com/jzaefferer/jquery-validation/archive/master.zip)此存储库或创建分支
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

有关如何设置规则和自定义的详细信息，请[检查文档](http://jqueryvalidation.org/documentation/)。

## <a name="reporting-issues-and-contributing-code"></a>报告问题和发布代码

有关详细信息，请参阅[参与准则](CONTRIBUTING.md)。

关于电子邮件验证的重要提示。 从版本 1.12.0 开始，该插件使用与 [HTML5 规范建议浏览器使用](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)的相同的正则表达式。 我们将遵循其指示并使用相同的检查。 如果你认为该规范是错误的，请向其报告问题。 如果你有不同的要求，请考虑[使用自定义方法](http://jqueryvalidation.org/jQuery.validator.addMethod/)。

## <a name="license"></a>许可证
版权所有 &copy; Jörn Zaefferer<br>
按照 MIT 许可证授予许可。
