---
ms.openlocfilehash: 170d5ec71b0789bc1efb43fbdd4e24eab36a8cc4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57049294"
---
<a name="--"></a>--
==================

## <a name="core"></a>核心
  * 删除未使用的 removeAttrs 方法
  * 替换 url 方法的正则表达式
  * 删除被 $.extend 覆盖的 $.ajax 中无效的 url 参数
  * 正确地处理嵌套的取消提交按钮
  * 修复缩进
  * 重构 attributeRules 和 dataRules 以共享规范化程序
  * dataRules 方法将值转换为适合数字输入的数字
  * 更新 url 方法以允许协议相对 URL
  * 删除弃用的 $.format 占位符
  * 使用 jQuery 1.7+ on/off，添加 destroy 方法
  * IE8 兼容性将 .indexOf 更改为 $.inArray
  * 将 NaN 值属性转换为 Opera Mini 的未定义属性
  * 停止 required 方法内的剪裁值
  * 使用：已禁用的选择器，以匹配已禁用的元素
  * 排除某些键盘键以防止重新验证字段
  * 请勿搜索整个 DOM 来查找单选框/复选框元素
  * 对于无效的规则方法抛出更适当的错误
  * 修复数字验证错误
  * 修复对 whatwg 规范的引用
  * 在验证一组自定义输入时将焦点放在无效元素上
  * 使用自定义突出显示方法时重置元素样式
  * 错误 id 中的转义美元符号
  * 还原“忽略只读字段以及已禁用的字段”。
  * 更新 Luhn 算法的注释中的链接

## <a name="additionals"></a>附加项
  * 更新 dateITA 以解决时区问题
  * 仅修复方法期间的扩展方法
  * 仅修复匹配期间的 accept 方法
  * 更新时间方法以允许使用一位数的小时数
  * 删除 notEqualTo 方法的无效测试
  * 添加 notEqualTo 方法
  * 通过 `$` 使用正确的 jQuery 引用
  * 删除 iban 方法中无用的正则表达式检查
  * 巴西 CPF 编号

## <a name="localization"></a>本地化
  * 更新 messages_tr.js
  * 更新 messages_sr_lat.js
  * 添加秘鲁西班牙语 (ES PE)
  * 添加格鲁吉亚语 (ქართული, ge)
  * 修复了加泰罗尼亚语翻译中的拼写错误
  * 改进芬兰语 (fi) 翻译
  * 添加亚美尼亚语 (hy_AM) 区域设置
  * 使用货币方法扩展意大利语 (it) 翻译
  * 添加 bn_BD 区域设置
  * 更新 zh 区域设置
  * 删除意大利语消息末尾的句号

<a name="1131--2014-10-14"></a>1.13.1 / 2014-10-14
==================

## <a name="core"></a>核心
  * 允许 0 作为 autoCreateRanges 的值
  * 对所有 validationTargetFor 元素应用忽略设置
  * 不修剪 min/max/rangelength 方法中的值
  * 转义 id/name，然后在 errorsFor 中将其用作选择器
  * focusCleanup 选项的显式默认值
  * 修复 describedby 匹配程序不正确的正则表达式
  * 忽略只读字段以及已禁用的字段
  * 改进 id 转义，将转义的 id 存储在 describedby 中
  * 使用 submitHandler 的返回值以允许或阻止窗体提交

## <a name="additionals"></a>附加项
  * 添加 postalcodeBR 方法
  * 当参数为字符串时修复模式方法


<a name="1130--2014-07-01"></a>1.13.0 / 2014-07-01
==================

## <a name="all"></a>全部
* 添加插件 UMD 包装器

## <a name="core"></a>核心
* 采用非错误 aria-describedby 和隐藏的空白错误
* 改进 dateISO RegExp
* 添加了单选框/复选框以委托 click 事件
* 对非标签元素使用 aria-describedby
* 还在单选框/复选框上注册 focusin、focusout 和 keyup
* 为 rangelength 属性值修复规范化
* 更新 elementValue 方法以处理 type="number" 字段
* 对字符串使用 charAt 而不是数组表示法以支持 IE8(?)

## <a name="localization"></a>本地化
* 修复 rangelength 方法的 sk 转换
* 添加芬兰语方法
* 修复了 GL 编号验证消息
* 修复了 ES 编号方法验证消息
* 添加了加利西亚语 (GL)
* 修复了 min 和 max 方法的法语消息

## <a name="additionals"></a>附加项
* 添加 statesUS 方法
* 修复 dateITA 方法以处理 DST bug
* 添加波斯语日期方法
* 添加 postalCodeCA 方法
* 添加 postalcodeIT 方法

<a name="1120--2014-04-01"></a>1.12.0 / 2014-04-01
==================

* 添加 ARIA 测试 ([3d5658e](https://github.com/jzaefferer/jquery-validation/commit/3d5658e9e4825fab27198c256beed86f0bd12577))
* 添加 es-AR 本地化消息。 ([7b30beb](https://github.com/jzaefferer/jquery-validation/commit/7b30beb8ebd218c38a55d26a63d529e16035c7a2))
* 将缺少的点添加到 es 和 es_AR 消息。 ([a2a653c](https://github.com/jzaefferer/jquery-validation/commit/a2a653cb68926ca034b4b09d742d275db934d040))
* 添加了印度尼西亚语 (ID) 本地化 ([1d348bd](https://github.com/jzaefferer/jquery-validation/commit/1d348bdcb65807c71da8d0bfc13a97663631cd3a))
* 添加了 NIF、NIE 和 CIF 西班牙语文档数字验证 ([#830](https://github.com/jzaefferer/jquery-validation/issues/830), [317c20f](https://github.com/jzaefferer/jquery-validation/commit/317c20fa9bb772770bb9b70d46c7081d7cfc6545))
* 已将当前窗体添加到远程 ajax 请求的上下文 ([0a18ae6](https://github.com/jzaefferer/jquery-validation/commit/0a18ae65b9b6d877e3d15650a5c2617a9d2b11d5))
* 附加：更新 IBAN 方法，修剪尾随空格 ([#970](https://github.com/jzaefferer/jquery-validation/issues/970)， [347b04a](https://github.com/jzaefferer/jquery-validation/commit/347b04a7d4e798227405246a5de3fc57451d52e1))
* BIC 方法：提高正则表达式，{1}始终是冗余的。 关闭 gh-744 ([5cad6b4](https://github.com/jzaefferer/jquery-validation/commit/5cad6b493575e8a9a82470d17e0900c881130873))
* Bower:包注册添加 Bower.json ([e86ccb0](https://github.com/jzaefferer/jquery-validation/commit/e86ccb06e301613172d472cf15dd4011ff71b398))
* 更改 jQuery 的美元引用，以便与 jQuery.noConflict 兼容。 关闭 gh-754 ([2049afe](https://github.com/jzaefferer/jquery-validation/commit/2049afe46c1be7b3b89b1d9f0690f5bebf4fbf68))
* 核心：将"method"字段添加到错误列表条目 ([89a15c7](https://github.com/jzaefferer/jquery-validation/commit/89a15c7a4b17fa2caaf4ff817f09b04c094c3884))
* 核心：添加了对通过 data-msg 属性的泛型消息 ([5bebaa5](https://github.com/jzaefferer/jquery-validation/commit/5bebaa5c55c73f457c0e0181ec4e3b0c409e2a9d))
* 核心：允许属性具有值为零 (例如最小值 ="0") ([#854](https://github.com/jzaefferer/jquery-validation/issues/854)， [9dc0d1d](https://github.com/jzaefferer/jquery-validation/commit/9dc0d1dd946b2c6178991fb16df0223c76162579))
* 核心：禁用弃用的 $.format ([#755](https://github.com/jzaefferer/jquery-validation/issues/755)， [bf3b350](https://github.com/jzaefferer/jquery-validation/commit/bf3b3509140ea8ab5d83d3ec58fd9f1d7822efc5))
* 核心：修复对多个错误类的支持 ([c1f0baf](https://github.com/jzaefferer/jquery-validation/commit/c1f0baf36c21ca175bbc05fb9345e5b44b094821))
* 核心：忽略被忽略的元素上的事件 ([#700](https://github.com/jzaefferer/jquery-validation/issues/700)， [a864211](https://github.com/jzaefferer/jquery-validation/commit/a86421131ea69786ee9e0d23a68a54a7658ccdbf))
* 核心：改进 elementValue 方法 ([6c041ed](https://github.com/jzaefferer/jquery-validation/commit/6c041edd21af1425d12d06cdd1e6e32a78263e82))
* 核心：确保正常运行 element （） 处理忽略的元素。 ([3f464a8](https://github.com/jzaefferer/jquery-validation/commit/3f464a8da49dbb0e4881ada04165668e4a63cecb))
* 核心：切换 dataRules 分析到 W3C HTML5 规范样式 ([460fd22](https://github.com/jzaefferer/jquery-validation/commit/460fd22b6c84a74c825ce1fa860c0a9da20b56bb))
* 核心：触发成功，但有其他成功的验证程序 ([#851](https://github.com/jzaefferer/jquery-validation/issues/851)， [f93e1de](https://github.com/jzaefferer/jquery-validation/commit/f93e1deb48ec8b3a8a54e946a37db2de42d3aa2a))
* 核心：使用纯元素而不是未环绕再次的元素 ([03cd4c9](https://github.com/jzaefferer/jquery-validation/commit/03cd4c93069674db5415a0bf174a5870da47e5d2))
* 核心：确保最后远程执行 ([#711](https://github.com/jzaefferer/jquery-validation/issues/711), [ad91b6f](https://github.com/jzaefferer/jquery-validation/commit/ad91b6f388b7fdfb03b74e78554cbab9fd8fca6f))
* 演示：在多部分的演示中使用正确的选项。 ([#1025](https://github.com/jzaefferer/jquery-validation/issues/1025), [070edc7](https://github.com/jzaefferer/jquery-validation/commit/070edc7be4de564cb74cfa9ee4e3f40b6b70b76f))
* 修复其他方法中的 $/jQuery 使用情况。 修复 #839 ([#839](https://github.com/jzaefferer/jquery-validation/issues/839), [59bc899](https://github.com/jzaefferer/jquery-validation/commit/59bc899e4586255a4251903712e813c21d25b3e1))
* 改进中文翻译 ([1a0bfe3](https://github.com/jzaefferer/jquery-validation/commit/1a0bfe32b16f8912ddb57388882aa880fab04ffe))
* 初始 ARIA 所需的实现 ([bf3cfb2](https://github.com/jzaefferer/jquery-validation/commit/bf3cfb234ede2891d3f7e19df02894797dd7ba5e))
* 本地化：将接受值更改为扩展名。 修复 #771，关闭 gh 793。 ([#771](https://github.com/jzaefferer/jquery-validation/issues/771), [12edec6](https://github.com/jzaefferer/jquery-validation/commit/12edec66eb30dc7e86756222d455d49b34016f65))
* 消息：添加 icelandic 本地化 ([dc88575](https://github.com/jzaefferer/jquery-validation/commit/dc885753c8872044b0eaa1713cecd94c19d4c73d))
* 消息：将缺少的点添加到 bg、 fr 和 sr 消息。 ([adbc636](https://github.com/jzaefferer/jquery-validation/commit/adbc6361c377bf6b74c35df9782479b1115fbad7))
* 消息：创建 messages_sr_lat.js ([f2f9007](https://github.com/jzaefferer/jquery-validation/commit/f2f90076518014d98495c2a9afb9a35d45d184e6))
* 消息：创建 messages_tj.js ([de830b3](https://github.com/jzaefferer/jquery-validation/commit/de830b3fd8689a7384656c17565ee92c2878d8a5))
* 消息：修复 sr_lat 翻译，添加缺少的空格 ([880ba1c](https://github.com/jzaefferer/jquery-validation/commit/880ba1ca545903a41d8c5332fc4038a7e9a580bd))
* 消息：更新 messages_sr.js，修复缺少的空格 ([10313f4](https://github.com/jzaefferer/jquery-validation/commit/10313f418c18ea75f385248468c2d3600f136cfb))
* 方法：添加货币的其他方法 ([1a981b4](https://github.com/jzaefferer/jquery-validation/commit/1a981b440346620964c87ebdd0fa03246348390e))
* 方法：添加弯引号删除 stripHTML 的标点 ([aa0d624](https://github.com/jzaefferer/jquery-validation/commit/aa0d6241c3ea04663edc1e45ed6e6134630bdd2f))
* 方法：修复 dateITA 方法，避免夏季时间错误 ([279b932](https://github.com/jzaefferer/jquery-validation/commit/279b932c1267b7238e6652880b7846ba3bbd2084))
* 方法：本地化符合智利文化 (es CL) 的方法 ([cf36b93](https://github.com/jzaefferer/jquery-validation/commit/cf36b933499e435196d951401221d533a4811810))
* 方法：更新电子邮件以使用 HTML5 正则表达式，删除 email2 方法 ([#828](https://github.com/jzaefferer/jquery-validation/issues/828)， [dd162ae](https://github.com/jzaefferer/jquery-validation/commit/dd162ae360639f73edd2dcf7a256710b2f5a4e64))
* 模式方法：删除分隔符，因为 HTML5 实现不包括这些。 ([37992c1](https://github.com/jzaefferer/jquery-validation/commit/37992c1c9e2e0be8b315ccccc2acb74863439d3e))
* 限制信用卡验证程序以包括长度检查。 关闭 gh-772 ([f5f47c5](https://github.com/jzaefferer/jquery-validation/commit/f5f47c5c661da5b0c0c6d59d169e82230928a804))
* 更新 messages_ko.js - 关闭 gh-715 ([5da3085](https://github.com/jzaefferer/jquery-validation/commit/5da3085ff02e0e6ecc955a8bfc3bb9a8d220581b))
* 更新 messages_pt_BR.js。 关闭 gh-782 ([4bf813b](https://github.com/jzaefferer/jquery-validation/commit/4bf813b751ce34fac3c04eaa2e80f75da3461124))
* 更新 phonesUK 和 mobileUK 以接受新前缀。 关闭 gh-750 ([d447b41](https://github.com/jzaefferer/jquery-validation/commit/d447b41b830dee984be21d8281ec7b87a852001d))
* 验证九位数邮政编码。 关闭 gh-726 ([165005d](https://github.com/jzaefferer/jquery-validation/commit/165005d4b5780e22d13d13189d107940c622a76f))
* phoneUS:添加 N11 排除项。 关闭 gh 861 ([519bbc6](https://github.com/jzaefferer/jquery-validation/commit/519bbc656bcb26e8aae5166d7b2e000014e0d12a))
* resetForm 应清除任何 aria 无效的值 ([4f8a631](https://github.com/jzaefferer/jquery-validation/commit/4f8a631cbe84f496ec66260ada52db2aa0bb3733))
* valid （):检查所有元素。 修复 #791 - valid() 仅验证第一个（无效）元素 ([#791](https://github.com/jzaefferer/jquery-validation/issues/791), [6f26803](https://github.com/jzaefferer/jquery-validation/commit/6f268031afaf4e155424ee74dd11f6c47fbb8553))

<a name="1111--2013-03-22"></a>1.11.1 / 2013-03-22
==================

  * 还原以便也将范围方法的参数转换为数字。 关闭 gh-702
  * 用 mockjax 处理程序替换大多数的 PHP 用法。 也执行一些演示清理，更新到较新的掩码输入插件。 在 PHP 中保留 captcha 演示。 修复 #662
  * 从 Milk 演示删除突出显示的内联代码。 查看源代码功能正常。
  * 通过从模板内容剪裁空格，然后传递到 jQuery 构造函数来修复 dynamic-totals 演示
  * 修复 min/max 验证。 关闭 gh-666。 修复 #648
  * 修复了作为规则出现并且会在通过规则 ("add") 更新后引发异常的 messages。 关闭 gh-670，修复 #624
  * 添加朝鲜语 (ko) 本地化。 关闭 gh-671
  * 改进了英国的邮政编码方法以筛选更多无效的邮政编码。 关闭 #682
  * 更新 messages_sv.js。 关闭 #683
  * 将 Grunt 链接更改为项目网站。 关闭 #684
  * 将远程方法在列表中下移到最后一个运行，以便在应用到字段的所有其他方法之后运行。 修复 #679
  * 更新 plugin.json 说明，应包含单词 'validate'
  * 修复拼写错误
  * 修复 jQuery 加载程序以使用其自己的路径。 修复嵌套的演示。
  * 通过节点模块 phantomjs 安装时，更新 grunt-contrib-qunit 以使用 PhantomJS 1.8
  * 使 valid() 返回一个布尔值而不是 0 或 1。 修复 #109 - valid() 不返回布尔值

<a name="1110--2013-02-04"></a>1.11.0 / 2013-02-04
==================

  * 删除作为 `min`、`max` 和 `range` 规则数量的清算。 修复 #455。 关闭 gh-528。
  * 更新预先存在的标签 - 修复 #430，关闭 gh-436
  * 修复 $.validator.format 以避免组内插，其中 IE8/9 至少用匹配项替换 -bash。 修复 #614
  * 修复 mimetype 正则表达式
  * 添加插件清单并将标头更新到 MIT 许可，放弃不必要的双许可（如 jQuery）。
  * 希伯来消息：末尾的句子-修复 gh-568 删除的点
  * Require_from_group 验证的法语翻译。 修复 gh-573。
  * 允许组为数组或字符串 - 修复 #479
  * 已删除多个 MIME 类型的空格
  * 修复一些日期验证、JS 语法错误。
  * 移除对元数据插件的支持，并替换为 data-rule- 和 data-msg-（907467e8 中已添加）属性。
  * 已添加 sftp 作为有效的 url-pattern
  * 添加马来语 (my) 本地化
  * 更新 localization/messages_hu.js
  * 删除 focusin/focusout polyfill。 修复 #542 - 包含 jquery.validate 会干扰 IE9 中的 focusin 和 focusout 事件
  * 本地化：芬兰语翻译中固定拼写错误
  * 从有效转回无效时修复 RTM 演示以显示无效图标
  * 修复了远程函数中的过早返回，防止在输入过快的情况下发生 ajax 调用。 确保远程验证始终验证最新值。
  * 撤消修复 #244。 修复 #521 - 文本在字段中时立即触发电子邮件验证。

<a name="1100--2012-09-07"></a>1.10.0 / 2012-09-07
===================

  * 已根据社区反馈更正 nowhitespace、phoneUS、phoneUK 和 mobileUK 的法语字符串。
  * 根据 ISO_3166-1 标准 (http://en.wikipedia.org/wiki/ISO_3166-1) 重命名 language_REGION 的文件，对于中国台湾而言，语言为中文 (zh)，区域为中国台湾 (TW)
  * 优化 RegEx 模式，尤其是对于英国电话号码。
  * 为每个文件添加语言名称，根据 ISO 639 标准 (http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 重命名爱沙尼亚语、格鲁吉亚语、乌克兰语和中文的语言代码
  * 已添加克罗地亚语 (HR) 本地化
  * 编辑现有的法语翻译，并且添加了其他方法的法语翻译。
  * 合并用于在数据属性中指定自定义错误消息的更改
  * 已为新号码更新英国移动电话号码正则表达式。 修复 #154
  * 添加元素以成功调用测试。 修复 #60
  * 修复时间附加方法的正则表达式。 修复 #131
  * resetForm 现在清除窗体元素中旧的 previousValue。 修复 #312
  * 已将复选框测试添加到 require_from_group 并更改了 require_from_group 以使用 elementValue。 修复 #359
  * 在 jQuery 1.5.2+ 中修复 dataFilter 响应问题。 修复 #405
  * 添加了 jQuery Mobile 演示。 修复 #249
  * 反优化 findByName 以进行更正。 修复 #82 - $.validator.prototype.findByName 在 IE7 中断开
  * 添加了美国邮政编码支持和测试。 修复 #90
  * 在 keyup 中将 lastElement 更改为 lastActive，跳过选项卡上的验证或空元素。 修复 #244
  * 从 stripHtml 中删除了数字去除。 修复 #2
  * 修复了从无效到有效远程验证的无效计数。 修复 #286
  * 将 file_input 的链接添加到演示索引
  * 已将旧的 accept 方法移至扩展 additional-method，添加了新的 accept 方法来处理标准浏览器的 mimetype 筛选。 修复 #287 并取代 #369
  * Onfocusout 设置为 false 时禁用 blur 事件。 已添加测试。
  * 修复单选按钮和复选框的值问题。 修复 #363
  * 为 rangeWords 添加了测试并修复了方法中的正则表达式和边界。 修复 #308
  * 已修复 TinyMCE 演示并在演示页上添加了链接。 修复 #382
  * 已更改 min/max 的本地化消息。修复 #273
  * 已添加文本输入类型的伪选择器，以修复默认空白类型属性的问题。 已添加测试和一些测试标记。 修复 #217
  * 已修复 dynamic-totals 演示的委托 bug。 修复 #51
  * 为字母数字验证程序修复不正确的消息
  * 已删除所需属性的不正确的 false 检查
  * 需要非 html5 浏览器的属性修复。 修复 #301
  * 添加了 "require_from_group" 和 "skip_or_fill_minimum" 方法
  * 为瑞典语使用正确的 iso 代码
  * 已更新演示 HTML 文件以使用 HTML5 doctype
  * 已修复不带前导零的小数位数的正则表达式问题。 已添加新方法的测试。 修复 #41
  * 引入对仅字符串值进行规范化的 elementValue 方法（不要更改多选数组值）。 修复 #116
  * 支持动态添加的提交按钮和更新的测试用例。 使用 validateDelegate。 PR #9 中的代码
  * 修复测试固件中错误的双引号
  * 修复 maxWords 方法以包括上限值，而不是排除它。 修复 #284
  * 已修复德语范围验证程序消息中的语法错误。 修复 #315
  * 已修复对 errorClass 选项的多个类名称的处理。 由 Max Lynch 测试。 修复 #280
  * 修复 jQuery.format 用法，应是 $.validator.format。 修复 #329
  * 针对“所有”英国电话号码 + 英国邮政编码的方法
  * 模式方法：将字符串参数转换为 RegExp。 修复问题 #223
  * 德语本地化文件中的语法错误
  * 已添加爱沙尼亚语本地化消息
  * 改进 themerollered 演示的工具提示处理
  * 将 type="text" 添加到没有 type 属性的输入字段，以便使用 qSA
  * 更新 themerollered 演示以使用工具提示，以叠加方式显示错误。
  * 更新 themerollered 演示以使用最新 jQuery UI（以及更新的 jQuery 版本）。 移动代码以加快页面加载速度。
  * 已修复中断的 min 日语错误消息。
  * 将窗体插件更新到最新版本。 增强 ajaxSubmit 演示。
  * 从 classRuleSettings 中删除 dateDE 和 numberDE 方法，遗留项移至本地化方法
  * 将 submit 事件传递到 submitHandler 回调
  * 修复 #219 - 通过依存关系回调或依存关系表达式修复元素中的 valid()。
  * 改进了内部版本以删除 dist dir，确保仅压缩当前版本

<a name="190"></a>1.9.0
---
* 已添加巴斯克语 (EU) 本地化
* 已添加斯洛文尼亚语 (SL) 本地化
* 已修复问题 #127 - 芬兰语翻译有一个“：”而不是“；”
* 已修复俄语本地化、次要语法问题
* 已添加对 HTML5 输入类型的支持，修复 #97
* 通过在窗体上设置 novalidate 属性和读取类型属性改进了 HTML5 支持。
* 已修复 showLabel()，从错误元素中删除所有类。 仅删除 settings.validClass。 修复 #151
* 已将 'pattern' 添加到附加方法以对任意正则表达式进行验证。
* 已改进电子邮件方法，不允许在末尾处使用点（由 RFC 验证，但此处并不需要）。 修复 #143
* 已修复瑞典语和挪威语翻译，min/max 消息已切换。 修复 #181
* 已修复 #184 - resetForm：应取消设置 lastElement
* 已修复 #71 - 改进现有的时间方法，并添加 12 小时上午/下午时间格式的 time12h 方法
* 已修复 #177 - 修复单个单选按钮或复选框输入的验证
* 已修复 #189 - 现在默认忽略隐藏元素
* 已修复 #194 - 如果 jQuery>=1.6，则“必填”属性会失效 - 使用.prop 而不是 .attr
* 已修复 #47、#39、#32 - 允许信用卡号包含空格以及短划线（空格通常由用户输入）。

<a name="181"></a>1.8.1
---
* 已添加泰语 (TH) 本地化，修复 #85
* 已添加越南语 (VI) 本地化，感谢 Ngoc
* 已修复问题 #78。 错误/有效样式应用于相同组的所有单选按钮以进行所需验证。
* 请勿使用 form.elements，因为 jQuery 1.6 中不再为其提供支持。 而且它会发生错误 (IE6-8: form.elements === form)。

<a name="180"></a>1.8.0
---
* 已改进 NL 本地化 (http://plugins.jquery.com/node/14120)
* 已添加格鲁吉亚语 (GE) 本地化，感谢 Avtandil Kikabidze
* 已添加塞尔维亚语 (SR) 本地化，感谢 Aleksandar Milovac
* 已将 ipv4 和 ipv6 添加到附加方法，感谢 Natal Ngétal
* 已添加日语 (JA) 本地化，感谢 Bryan Meyerovich
* 已添加加泰罗尼亚语 (CA) 本地化，感谢 Xavier de Pedro
* 已修复 for-in 循环内缺少的 var 语句
* 修复远程验证，其中设置了格式的消息会发生混乱 (https://github.com/jzaefferer/jquery-validation/issues/11)
* 修复与 jQuery 1.5.1 的兼容性问题，同时保持向后兼容性

<a name="17"></a>1.7
---
* 已添加立陶宛语 (LT) 本地化
* 已添加希腊语 (EL) 本地化 (http://plugins.jquery.com/node/12319)
* 已添加拉脱维亚语 (LV) 本地化 (http://plugins.jquery.com/node/12349)
* 已添加希伯来语 (HE) 本地化 (http://plugins.jquery.com/node/12039)
* 已修复西班牙语 (ES) 本地化 (http://plugins.jquery.com/node/12696)
* 已添加 jQuery UI themerolled 演示
* 已删除 cmxform.js
* 已修复四个丢失的分号 (http://plugins.jquery.com/node/12639)
* 将 additional-methods.js 中的 phone-method 重命名为 phoneUS
* 已将 phoneUK 和 mobileUK 方法添加到 additional-methods.js (http://plugins.jquery.com/node/12359)
* 深入扩展选项，用于避免在对单个元素使用 rules-method 时修改多个窗体 (http://plugins.jquery.com/node/12411)
* 修复与 jQuery 1.4.2 的兼容性问题，同时保持向后兼容性

<a name="16"></a>1.6
---
* 已添加阿拉伯语 (AR)、葡萄牙语 (PTPT)、波斯语 (FA)、芬兰语 (FI) 和保加利亚语 (BR) 本地化
* 已更新瑞典语 (SE) 本地化（一些缺少的 html iso 字符）
* 已修复 $.validator.addMethod 来正确处理消息参数的空字符串与未定义的字符串
* 已修复两个意外的全局变量
* 已增强 min/max/rangeWords（在 additional-methods.js 中）以便在计数之前去除 html；在 RTF 编辑器中统计单词时正常运行
* 已经为 DE、NL 和 PT 添加了本地化方法，删除了 dateDE 和 numberDE 方法（改用带 date 和 number 方法的 messages_de.js 和 methods_de.js）
* 已修复从 kudos 到 Matas Petrikas 的远程窗体提交同步
* 已改进交互式选择验证，现在也对 click 进行验证（通过 option 或 select，浏览器间不一致）；在 Safari 中不起作用，在 select 元素上不会触发 click 事件；修复 http://plugins.jquery.com/node/11520
* 已更新到最新窗体插件（2.36 版），修复 http://plugins.jquery.com/node/11487
* 绑定到 equalTo 目标的 blur 事件，以在目标更改时重新验证，修复 http://plugins.jquery.com/node/11450
* 简化 select 验证，委托到 jQuery 的 val() 方法以获取 select 值；应修复 http://plugins.jquery.com/node/11239
* 已修复默认数字消息 (http://plugins.jquery.com/node/9853)
* 已修复缓存的远程消息问题（ http://plugins.jquery.com/node/11029 和 http://plugins.jquery.com/node/9351)
* 已修复 additional-methods.js 中丢失的分号 (http://plugins.jquery.com/node/9233)
* 已在消息中添加替换参数的自动检测，无需提供格式函数 (http://plugins.jquery.com/node/11195)
* 已修复 Sizzle 引起的 :filled/:blank 问题 (http://plugins.jquery.com/node/11144)
* 已将整数方法添加到 additional-methods.js (http://plugins.jquery.com/node/9612)
* 已修复 errorsFor 方法，其中 for-attribute 包含需要转义才会在选择器内有效的字符 (http://plugins.jquery.com/node/9611)

<a name="155"></a>1.5.5
---
* 修复 http://plugins.jquery.com/node/8659
* 已修复 messages_cs.js 中的尾随逗号

<a name="154"></a>1.5.4
---
* 已修复远程方法 bug (http://plugins.jquery.com/node/8658)

<a name="153"></a>1.5.3
---
* 已修复与 wrapper-option 相关的 bug，其中选择了与 wrapper-option 匹配的所有上级元素 (http://plugins.jquery.com/node/7624)
* 已更新多部分的演示以便使用最新的 jQuery UI accordion
* 已将 dateNL 和 time 方法添加到 additionalMethods.js
* 已添加繁体中文 (Taiwan, tw) 和哈萨克斯坦 (KK) 本地化
* 已将 jQuery.format（之前为 String.format）移动至 jQuery.validator.format，已弃用 jQuery.format 并将在 1.6 中删除（请参阅 http://code.google.com/p/jquery-utils/issues/detail?id=15 了解详细信息）
* 已清理 messages_pl.js 和 messages_ptbr.js（仍定义 max/min/rangeValue 的消息，1.4 中已删除这些消息）
* 已修复多个元素的 valid-plugin-method 中有缺陷的布尔逻辑；现在所有元素都必须对 boolean-true 结果有效 (http://plugins.jquery.com/node/8481)
* 增强 $。 validator.addMethod:未定义第三个 message-argument 不会覆盖一个现有的消息 （ http://plugins.jquery.com/node/8443)
* SubmitHandler 选项的增强功能：使用时，在事件提交按钮，将捕获并将提交按钮的单击是调用 submitHandler 之前, 插入到窗体，然后删除;保留提交按钮保持不变 （ http://plugins.jquery.com/node/7183#comment-3585)
* 添加了选项 validClass，默认值为 "valid"，该选项在验证后将此类添加到所有有效元素 (http://dev.jquery.com/ticket/2205)
* 已将 creditcardtypes 方法添加到 additionalMethods.js，包括测试（通过 http://dev.jquery.com/ticket/3635)）
* 已改进远程方法，通过使用客户端定义的消息允许将服务器端消息用作字符串，有效时为 true，或无效时为 false (http://dev.jquery.com/ticket/3807)
* 已改进 accept 方法，并接受逗号分隔的 Drupal 样式列表值 (http://plugins.jquery.com/node/8580)

<a name="152"></a>1.5.2
---
* 已经为 maxWords、minWords 和 rangeWords 修复 additional-methods.js 中的消息，以包含对 $.format 的调用
* 已修复传递到方法的值以排除回车 (\r)，与 jQuery 的 val() 相同
* 已添加斯洛伐克语 (sk) 本地化
* 已添加有关与 jQuery UI 选项卡集成的演示
* 已将 selects-grouping 示例添加到选项卡演示（请参考第二个选项卡，即生日字段）

<a name="151"></a>1.5.1
---
* 已更新 marketo 演示以使用 invalidHandler 选项，而不是绑定 invalid-form 事件
* 已添加 TinyMCE 集成示例
* 已添加乌克兰语 (ua) 本地化
* 已修复长度验证以使用剪裁值（从 1.5 回归，其中已删除验证前的一般剪裁）
* 支持与 1.2.6 和 1.3 兼容的各种小修补程序

<a name="15"></a>1.5
---
* 已改进基本演示，密码更改后验证 confirm-password 字段
* 已修复基本验证，将未剪裁的输入值作为第一个参数传递给验证方法，相应地进行了必需的更改；打破依靠剪裁的现有定制方法
* 已添加挪威语 (no)、意大利语 (it)、匈牙利语 (hu) 和罗马尼亚语 (ro) 本地化
* 已修复的 # 3195:瑞典语本地化中的两个缺陷
* 修复的 # 3503:扩展了以接受 messages 属性： 用于指定将自定义消息添加到通过 rules ("添加"，{消息: {需要："Required ！ 元素
* 已修复的 # 3356:使用 meta-option 时从 # 2908年回归
* 已修复的 # 3370:已添加的 ignoreTitle 选项，设置要从 title 属性，跳过读取消息有助于避免 Google 工具栏; 的问题默认值为 false 的兼容性
* 修复的 # 3516:即使涉及远程验证触发 invalid-form 事件
* 已将 invalidHandler 选项作为快捷方式添加到 bind("invalid-form", function() {})
* 已修复 ajaxSubmit-integration-demo 中加载指示器的 Safari 问题（先追加到 body，然后隐藏）
* 已添加信用卡验证的测试并改进默认消息
* 已增强远程验证，接受作为参数传递给 $.ajax 的选项（url 字符串或选项，包括 url 属性以及 $.ajax 支持的其他所有内容）

<a name="14"></a>1.4
---
* 已修复 #2931，验证按文档顺序排列的元素并忽略 type=image 输入
* 已修复 $ 和 jQuery 变量的用法，现在与 noConflict 用法的所有变体完全兼容
* 已实施 #2908，通过元数据 ala class="{required:true,messages:{required:'required field'}}" 启用自定义消息，添加了 demo/custom-messages-metadata-demo.html
* 删除了弃用的方法 minValue (min)、maxValue (max)、rangeValue (rangevalue)、minLength (minlength)、maxLength (maxlength)、rangeLength (rangelength)
* 修复的 # 2215年回归：仅对于当前元素，并非所有内容都调用 unhighlight
* 已实施 #2989，启用图像按钮以取消验证
* 已修复 IE 针对 maxlength=0 错误验证的问题
* 已添加捷克语 (cs) 本地化
* 在 validator.resetForm() 中重置 validator.submitted，必要时启用完全重置
* 已修复 #3035，在读取规则时跳过所有的错误属性（0，未定义，空字符串），删除了 maxlength 解决方法的部分（对于 0）
* 已添加荷兰语 (nl) 本地化 (#3201)

<a name="13"></a>1.3
---
* 已修复 invalid-form 事件，现在仅在窗体无效时触发
* 已添加西班牙语 (es)、俄语 (ru)、葡萄牙语(巴西) (ptbr)、土耳其语 (tr) 和波兰语 (pl) 本地化
* 已添加 removeAttrs 插件，以帮助添加和删除多个属性
* 已添加组选项，通过 groups: { arbitraryGroupName: "fieldName1 fieldName2[, fieldNameN" } 为多个元素显示一条消息
* 已增强用于添加和删除（静态）规则的 rules()：rules("add", "method1[, methodN]"/{method1:param[, method_n:param]}) 和 rules("remove"[, "method1[, method_n]")
* 已增强 rules-option，接受以空格分隔的方法字符串列表，例如， {birthdate: "required date"}
* 使用内联规则修复复选框组验证：现在正确验证的组，只要这些规则指定的第一个元素上单击
* 已修复 #2473，忽略具有 boolean-false 的显式参数的所有规则，例如， required:false 与完全不指定 required 相同（目前为止作为 required:true 处理）
* 修复的 # 2424，从 # 2473 中已修改的修补程序：返回依赖项不匹配的方法不停止再; 评估其他规则尽管如此，成功不适用于可选字段
* 已修复 url 和电子邮件验证，不使用剪裁后的值
* 已修复信用卡验证以接受仅数字和短划线（asdf 是无效的信用卡号）
* 允许取消按钮的按钮元素和输入元素（通过 class="cancel"）
* 已修复的 # 2215:已修复的消息显示，调用 unhighlight 作为显示和隐藏消息，没有更多视觉副作用检查元素，将提取的 validator.checkForm 以验证没有 UI 副作用的窗体时的一部分
* 通过函数重写自定义选择器 (:blank, :filled, :unchecked) 以实现与 AIR 的兼容性

<a name="121"></a>1.2.1
-----

* 已捆绑委托插件与验证插件 - 始终需要
* 已改进远程验证，包含来自 ajaxQueue 插件的部分以执行正确的同步（不需要额外的插件）
* 已修复 stopRequest 以阻止 pendingRequest < 0
* 已添加 jQuery.validator.autoCreateRanges 属性，默认为 false，启用以便将 min/max 转换为 range，将 minlength/maxlength 转换为 rangelength；这样做基本上可修复由于自动在 1.2 中创建范围引发的问题
* 已修复 optional-methods，如果字段为空，则不突出显示任何内容，即不触发 success
* 允许使用 highlight/unhighlight 选项的 false/null，而不是强制执行 do-nothing-callback，即使无需突出显示任何内容也是如此
* 已修复未选择任何元素的 validate() 调用，返回 undefined 而不是引发错误
* 已改进演示，将元数据替换为用于指定规则的类/属性
* 已修复无自定义消息用于远程验证时的错误
* 已修改电子邮件和 url 验证，需要域标签和顶部标签
* 已修复 url 和电子邮件验证，需要 TLD（实际上需要域标签）；1.2 版本（TLD 可选）移到 url2 和 email2 的附加项
* 已修复 IE6/7 中的 dynamic-totals 演示并已改进模板化，使用 textarea 存储多行模板和字符串内插
* 已添加登录窗体示例，其中包含将密码字段设为可选的“电子邮件密码”链接
* 已增强 dynamic-totals 演示，其中包含为两个字段使用一条消息的示例

<a name="12"></a>1.2
---

* 已添加 AJAX-captcha 验证示例（基于 http://psyrens.com/captcha/)
* 已添加 remember-the-milk-demo（感谢 RTM 团队授予权限！）
* 已添加 marketo-demo（感谢 Glen Lipka！）
* 已添加 ajax-validation 支持，请参阅方法“remote”；服务器端返回 JSON，对于有效元素为 true，对于无效元素为 false 或 String，String 用作消息
* 已添加突出显示和未突出显示选项，默认情况下切换元素中的 errorClass，允许自定义突出显示
* 已添加 valid() 插件方法，用于以编程方式简单地检查窗体和字段，无需使用验证程序 API
* 已添加 rules() 插件方法，用以读取和写入元素的规则（当前是只读）
* 已替换电子邮件方法的正则表达式，感谢 Scott Gonzalez 的贡献，请参阅 http://projects.scottsplayground.com/email_address_validation/
* 已重构事件架构以完全依赖委托，既提高了性能，又易于开发人员使用（需 jquery.delegate.js）
* 已将文档从内联移到 http://docs.jquery.com/Plugins/Validation - 包括所有方法的交互式示例
* 已删除 validator.refresh()，验证现在完全是动态的
* 将 minValue 重命名为 min，将 maxValue 重命名为 max，将 rangeValue 重命名为 range，弃用以前的名称（将在 1.3 中删除）
* 将 minLength 重命名为 minlength，将 maxLength 重命名为 maxlength，将 rangeLength 重命名为 rangelength，弃用以前的名称（将在 1.3 中删除）
* 已添加功能，将 min + max 合并到 range，将 minlength + maxlength 合并到 rangelength
* 已添加对动态规则参数的支持，允许指定一个函数作为参数，例如， 对于 minlength，在验证此元素时调用
* 允许指定 null 或空字符串作为不显示任何内容的消息（参见 marketo 演示）
* 规则检修：现在支持组合的规则选项、 元数据、 类 （新） 和属性 （新），请参阅 rules 有关详细信息

<a name="112"></a>1.1.2
---

* 已替换用于 URL 方法的 regex ，感谢 Scott Gonzalez 的贡献，请参阅 http://projects.scottsplayground.com/iri/
* 已改进电子邮件方法以更好地处理 Unicode 字符
* 已修复所有元素有效（而不仅仅是在提交窗体时）时的隐藏容器错误，
* 已将 String.format 修复为 jQuery.format（移至 jQuery 命名空间）
* 已修复 accept 方法以接受大写和小写扩展名
* 已修复 validate() 插件方法，仅为一个给定的窗体创建一个验证器实例，并且始终返回这个实例（避免多次绑定事件）
* 已将 debug-mode 控制台日志从“错误”级别更改为“警告”级别

<a name="111"></a>1.1.1
-----

* 已修复无效的 XHTML，防止自 jQuery 1.1.4 以后在 IE 中创建错误标签
* 固定和改进了 String.format:全局搜索和替换，更好地处理数组参数
* 已修复取消按钮处理，用于使用验证器对象来存储状态而不是窗体元素
* 已修复名称选择器来处理“复杂”名称，例如， 包含括号 ("list[]")
* 已添加按钮并禁用了从验证中排除的元素
* 移动了要刷新的元素事件处理程序，以便能够将处理程序添加到新元素
* 已修复电子邮件验证以允许使用较长的顶级域名（例如， ".travel"）
* 已将 showErrors() 从 valid() 移至 form()
* 已添加 validator.size()：返回当前错误数
* 调用 submitHandler 和验证程序作为作用域，以便访问其方法，例如， 使用 errorsFor(Element) 查找错误标签
* 与 jQuery 1.1.x 和 1.2.x 兼容

<a name="11"></a>1.1
---

* 已添加对 blur、keyup 和 click（用于复选框和单选按钮）的验证。 替换 event-option。
* 已修复 resetForm
* 已修复 custom-methods-demo

<a name="10"></a>1.0
---

* 已改进 number 和 numberDE 方法来通过分隔符检查正确的十进制数
* 仅检查具有规则的元素（否则 success-option 应用于所有元素）
* 已添加信用卡号方法（感谢 Brian Klug）
* 已添加 ignore-option，例如， ignore: "[@type=hidden]"，使用该表达式排除要验证的元素。 默认值：无，但始终忽略提交和重置按钮
* 通过提供灵活的 String.format 帮助程序，大大增强了 Functions-as-messages
* Accept 函数作为消息，提供 runtime-custom-messages
* 已修复元素排除问题，没有来自 successList 的规则
* 已修复 custom-method-demo，用显示错误数量的消息替换了警报
* 修复了使用 submitHandler 时的 form-submit-prevention 问题
* 已完全删除元素 ID 的依赖项，尽管仍然会使用它们（存在时）将错误标签链接到输入。 通过使用具有 {name, message, element} 的数组来实现，而不是使用具有 id:message 对（用于内部 errorList）的对象。
* 已添加对指定简单规则作为简单字符串的支持，例如， "required" 相当于 {required: true}
* 添加了的功能：将 errorClass 添加到无效的字段的父元素，从而轻松设置标签/字段容器或字段的标签的样式。
* 已添加功能：focusCleanup - 如果启用，从无效元素中删除 errorClass，并在聚焦该元素时隐藏所有错误消息。
* 已添加 success 选项以显示已成功验证字段
* 已修复 Opera select-issue（避免 attribute-collision）
* 已修复在 IE 中聚焦隐藏元素的问题
* 已添加功能，以便跳过通过类“cancel”验证提交按钮的操作
* 通过在 title 属性上优先使用插件选项消息来修复 Google 工具栏的潜在问题
* submitHandler 仅在处理实际的提交事件时调用，validator.form() 仅为无效的窗体返回 false
* 无效的元素现在仅在提交时或通过 validator.focusInvalid() 聚焦，避免所有与 focus-on-blur 相关的麻烦
* IE6 错误容器布局问题已解决
* 通过 errorElement 选项自定义错误元素
* 已添加 validator.refresh() 以在窗体中查找新输入
* 已添加接受验证方法，检查文件扩展名
* 通过添加两个自定义表达式改进了依赖项功能：“:blank”用于选择具有空值的元素，而“:filled”用于选择具有值的元素，两者都不包含空格
* 添加到验证程序 resetform （） 方法：重置每个窗体元素 （如果可用，则使用窗体插件），删除无效元素上的类并隐藏所有错误消息
* 已修复 validator.showErrors() 的文档
* 已修复错误标签创建以始终使用 html() 而不 text()，允许作为消息传递的任何 HTML
* 已修复错误标签创建以使用指定的错误类
* 已添加依赖关系功能：Requires 方法接受 String （jQuery 表达式） 和函数作为自变量
* 大大改进了错误消息显示的自定义：使用普通消息并显示/隐藏附加的容器;完全替换消息显示为用自己的机制 （同时能够委托给默认处理程序;自定义放置生成的标签 （而不是默认下面的元素）
* 已修复 IE（错误容器）和 Opera（元数据）中的两个主要 bug
* 已修改验证方法以接受空字段为有效字段（异常：“required”和“equalTo”方法）
* 将“min”重命名为“minLength”，将“max”重命名为“maxLength”，将“length”重命名为“rangeLength”
* 已添加“minValue”、“maxValue”和“rangeValue”
* 已简化 API 以支持不同的事件。 可以禁用默认值 submit。 如果指定了任何事件，该事件会应用于每个元素（而不是整个窗体）。 将 keyup-validation 与 submit-validation 组合在一起，现在非常容易设置
* 已添加通过插件设置定义消息时对 one-message-per-rule 的支持
* 已添加对在某些父元素中包装元数据的支持。 这在元数据用于其他插件时也有用。
* 重构的测试和演示：更少文件，更好地演示
* 改进的文档：方法的更多示例，更多的参考文本来解释的一些基础知识
