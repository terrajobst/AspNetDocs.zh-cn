---
title: 更少，Sass 和 Font Awesome ASP.NET Core 中
author: ardalis
description: 了解如何在 ASP.NET Core 应用程序中使用Less，Sass，和ont Awesome。
ms.author: tdykstra
ms.date: 10/14/2016
uid: client-side/less-sass-fa
ms.openlocfilehash: 2229c4e3b0238ff17c15e78f657b9acb10495c72
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57065554"
---
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a>更少，Sass 和 Font Awesome ASP.NET Core 中

作者：[Steve Smith](https://ardalis.com/)

Web 应用程序的用户时要设置的样式和整体体验有多越来越高的期望。 新式 web 应用程序经常利用丰富的工具和框架，可用于定义和管理其外观和感觉以一致的方式。 框架喜欢[Bootstrap](http://getbootstrap.com/)可以转多地定义一组通用的样式和 web 站点的布局选项。 但是，最重要的站点还受益于能够有效地定义和维护样式和级联样式表 (CSS) 文件，以及具有对非图像的图标，可帮助使站点的接口更直观的轻松访问权。 这正是语言和支持的工具[更少](http://lesscss.org/)并[Sass](http://sass-lang.com/)，库等[Font Awesome](http://fontawesome.io/)，进入。

## <a name="css-preprocessor-languages"></a>CSS 预处理器语言

为了改进的基础语言的使用体验编译成其他语言的语言称为预处理器。 有两个常用的预处理器的 CSS:较低和 Sass。  这些预处理器将功能添加到 CSS，例如对变量和嵌套的规则，从而提高大型的复杂样式表的可维护性的支持。 作为一种语言的 CSS 是非常简单，缺少很简单，例如变量，即使对于支持，这往往会重复和臃肿使 CSS 文件。 添加预处理器通过实际编程语言功能有助于减少重复，并提供更好地组织的样式规则。 Visual Studio 提供了对这两个不太的内置支持和 Sass，以及使用这些语言时可以进一步改进开发体验的扩展。

预处理器可以如何改进可读性和可维护性的样式信息的快速示例，请考虑以下 CSS:

```css
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    color: black;
    font-weight: bold;
    font-size: 14px;
    font-family: Helvetica, Arial, sans-serif;
}
```

使用更少，这可重写以消除所有重复项，使用*mixin* (如此命名是因为它允许您"混用"属性从一个类或到另一个规则集):

```less
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    .header;
    font-size: 14px;
}
```

## <a name="less"></a>Less

使用 Node.js 运行不到 CSS 预处理器。 若要安装更少，使用节点包管理器 (npm) 从命令提示符 (-g 意味着"全局"):

```console
npm install -g less
```

如果你使用 Visual Studio，你可以开始使用小于通过将一个或多个较少文件添加到你的项目，然后配置 Gulp （或 Grunt） 在编译时处理它们。 添加*样式*向你的项目的文件夹，然后添加新的名为的文件小于*main.less*到此文件夹。

![添加较少的文件](less-sass-fa/_static/add-less-file.png)

添加后，您的文件夹结构应如下所示：

![文件夹结构](less-sass-fa/_static/folder-structure.png)

现在可以到文件，这将编译到 CSS 并部署到 wwwroot 文件夹 Gulp 通过添加一些基本的样式设置。

修改*main.less*包括以下内容，从单一的基础颜色创建简单的调色板。

```less
@base: #663333;
@background: spin(@base, 180);
@lighter: lighten(spin(@base, 5), 10%);
@lighter2: lighten(spin(@base, 10), 20%);
@darker: darken(spin(@base, -5), 10%);
@darker2: darken(spin(@base, -10), 20%);

body {
    background-color:@background;
}
.baseColor  {color:@base}
.bgLight    {color:@lighter}
.bgLight2   {color:@lighter2}
.bgDark     {color:@darker}
.bgDark2    {color:@darker2}
```

`@base` 和其他@-prefixed项是变量。 每个表示一种颜色。 除`@base`，设置它们并使用颜色函数： 变浅，变暗，并且全局。 淡化和加深不要这么多了您所期望的内容;数值调节钮调整由大量度 （大约颜色盘） 的一种颜色的色调。 更少的处理器非常智能，可忽略不会使用的变量，因此若要演示这些变量的工作原理，我们需要某个位置使用它们。 类`.baseColor`，等将演示在生成的 CSS 文件中的变量的计算的值。

### <a name="get-started"></a>入门

创建**npm 配置文件**(*package.json*) 项目文件夹中编辑它以引用`gulp`和`gulp-less`:

```json
{
  "version": "1.0.0",
  "name": "asp.net",
  "private": true,
  "devDependencies": {
    "gulp": "3.9.1",
    "gulp-less": "3.3.0"
  }
}
```

在项目文件夹，或在 Visual Studio 中安装的依赖项是在命令提示符**解决方案资源管理器**(**依赖项 > npm > 还原包**)。

```console
npm install
```

![VS 还原包](less-sass-fa/_static/restore-packages.png)

在项目文件夹中，创建**Gulp 配置文件**(*gulpfile.js*) 来定义自动化的过程。  在较低，表示的文件和运行更少的任务的顶部添加一个变量：

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less");

gulp.task("less", function () {
  return gulp.src('Styles/main.less')
    .pipe(less())
    .pipe(gulp.dest('wwwroot/css'));
});
```

打开**Task Runner Explorer** (**视图 > 其他 Windows > 任务运行程序资源管理器**)。 在任务之间应会看到名为的新任务`less`。 您可能需要刷新窗口。

运行`less`任务，并看到类似于此处所示的输出：

![更少的任务运行程序](less-sass-fa/_static/less-task-runner.png)

*Wwwroot/css*文件夹中现在包含新的文件*main.css*:

![创建主 css](less-sass-fa/_static/main-css-created.png)

打开*main.css* ，看到类似于以下内容：

```css
body {
    background-color: #336666;
}
.baseColor {
    color: #663333;
}
.bgLight {
    color: #884a44;
}
.bgLight2 {
    color: #aa6355;
}
.bgDark {
    color: #442225;
}
.bgDark2 {
    color: #221114;
}
```

添加到一个简单的 HTML 页面*wwwroot*文件夹，然后引用*main.css*若要查看操作中的调色板。

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <link href="css/main.css" rel="stylesheet" />
    <title></title>
</head>
<body>
    <div>
        <div class="baseColor">BaseColor</div>
        <div class="bgLight">Light</div>
        <div class="bgLight2">Light2</div>
        <div class="bgDark">Dark</div>
        <div class="bgDark2">Dark2</div>
    </div>
</body>
</html>
```

您所见上旋转 180 度`@base`用来制作`@background`导致对立的颜色的颜色盘`@base`:

![不到测试示例](less-sass-fa/_static/less-test-screenshot.png)

小于还提供对嵌套的规则，以及嵌套的媒体查询的支持。 例如，像菜单可能会导致详细 CSS 规则的定义嵌套层次结构像这样:

```css
nav {
    height: 40px;
    width: 100%;
}
nav li {
    height: 38px;
    width: 100px;
}
nav li a:link {
    color: #000;
    text-decoration: none;
}
nav li a:visited {
    text-decoration: none;
    color: #CC3333;
}
nav li a:hover {
    text-decoration: underline;
    font-weight: bold;
}
nav li a:active {
    text-decoration: underline;
}
```

理想情况下的所有相关的样式规则将被放在一起在 CSS 文件中，但实际上没有什么强制实施此规则约定和可能是块注释除外。

定义使用小于这些相同的规则如下所示：

```less
nav {
    height: 40px;
    width: 100%;
    li {
        height: 38px;
        width: 100px;
        a {
            color: #000;
            &:link { text-decoration:none}
            &:visited { color: #CC3333; text-decoration:none}
            &:hover { text-decoration:underline; font-weight:bold}
            &:active {text-decoration:underline}
        }
    }
}
```

请注意，在本例中为所有的从属元素`nav`包含其作用域内。 不再有任何重复的父元素 (`nav`， `li`， `a`)，并已删除的总的行计数 （尽管某些这是将值放在第二个示例的同一行上的结果）。 它可以是非常有用，组织，若要查看所有明确界定作用域内的给定用户界面元素的规则在这种情况下该文件的其余部分由设置大括号。

`&`语法是使用较少的选择器功能，和表示当前的选择器父级。 这样，在 {...} 块中，`&`表示`a`标记，并因此`&:link`等效于`a:link`。

创建响应式设计中非常有用的媒体查询可以也是导致很大程度重复和 CSS 中的复杂性。 小于允许媒体查询在嵌套在类中，以便在整个类定义不需要重复出现在不同顶级`@media`元素。 例如，下面是响应式菜单的 CSS:

```css
.navigation {
    margin-top: 30%;
    width: 100%;
}
@media screen and (min-width: 40em) {
    .navigation {
        margin: 0;
    }
}
@media screen and (min-width: 62em) {
    .navigation {
        width: 960px;
        margin: 0;
    }
}
```

这可以以秒为更好地定义：

```less
.navigation {
    margin-top: 30%;
    width: 100%;
    @media screen and (min-width: 40em) {
        margin: 0;
    }
    @media screen and (min-width: 62em) {
        width: 960px;
        margin: 0;
    }
}
```

小于我们已经看到的另一项功能是它支持适用于数学运算，从而允许从预定义的变量构造的样式特性。 这使得更新相关的样式更加容易，因为可以修改基变量和所有相关值自动更改。

CSS 文件，尤其是对于大型站点 （和尤其是如果要使用媒体查询），往往会获得很大随着时间推移，从而使用它们难以处理。 Less 文件可以单独定义的随后将提取使用`@import`指令。 小于还可用来导入单个 CSS 文件，同样，如果所需的。

*Mixin*可以接受参数，并小于支持 mixin 临界条件，以声明方式定义某些 mixin 生效的窗体中的条件逻辑。 Mixin 临界条件的一个常见用途是调整基于如何光的颜色或深色源颜色是。 Mixin 防护给定 mixin 接受颜色的参数，用于修改基于该颜色 mixin:

```less
.box (@color) when (lightness(@color) >= 50%) {
    background-color: #000;
}
.box (@color) when (lightness(@color) < 50%) {
    background-color: #FFF;
}
.box (@color) {
    color: @color;
}

.feature {
    .box (@base);
}
```

指定当前`@base`的值`#663333`，小于此脚本将生成以下 CSS:

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

小于提供了很多其他功能，但这应当会提供此功能的一些思路预处理语言。

## <a name="sass"></a>Sass

Sass 是类似于更少，提供对许多相同的功能，但稍有不同的语法的支持。 它使用 Ruby，而不是 JavaScript，构建，因此不同的安装要求。 原始 Sass 语言没有使用大括号或分号，而定义使用空白和缩进作用域。 在版本 3 的 Sass，引入了一种新语法， **SCSS** ("Sassy CSS")。 SCSS 是类似于 CSS 它忽略缩进级别和空格，并改为使用分号和大括号。

若要安装 Sass，通常您将首先安装 Ruby （预装在 macOS 上），并运行：

```console
gem install sass
```

但是，如果要运行 Visual Studio，你可以开始使用 Sass 在很大程度相同的方式就像使用更少。 打开*package.json*和"gulp sass"将包添加到`devDependencies`:

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

接下来，修改*gulpfile.js*添加 sass 变量和要编译 Sass 文件并将结果放在 wwwroot 文件夹中的任务：

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less"),
  sass = require("gulp-sass");

// other content removed

gulp.task("sass", function () {
  return gulp.src('Styles/main2.scss')
    .pipe(sass())
    .pipe(gulp.dest('wwwroot/css'));
});
```

现在，可以添加 Sass 文件*main2.scss*到*样式*中项目的根文件夹：

![添加 scss 文件](less-sass-fa/_static/add-scss-file.png)

打开*main2.scss*并添加以下：

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

保存所有文件。 现在刷新**Task Runner Explorer**，则请参阅`sass`任务。 运行它，并查找 */wwwroot/css*文件夹。 现在还有*main2.css*文件中的，使用以下内容：

```css
body {
    background-color: #CC0000;
}
```

Sass 支持嵌套在很大程度相同时，小于实现，它提供了类似的优势。 文件可以拆分函数并且包含使用`@import`指令：

```sass
@import 'anotherfile';
```

Sass 支持 mixin，使用`@mixin`关键字来定义它们并`@include`来包含它们从如此示例所示[sass lang.com](http://sass-lang.com):

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

Sass mixin，除了它还支持继承，的概念允许一个类来扩展另一个。 它是从概念上讲类似于一个 mixin，但在更少的 CSS 代码中的结果。 它通过`@extend`关键字。 若要试用 mixin，将以下代码添加到您*main2.scss*文件：

```sass
@mixin alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @include alert;
    border-color: green;
}

.error {
    @include alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

检查中的输出*main2.css*运行之后`sass`中的任务**Task Runner Explorer**:

```css
.success {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    border-color: green;
 }

.error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    color: red;
    border-color: red;
    font-weight: bold;
}
```

请注意，所有警报的 mixin 的常见属性在每个类中有重复。 Mixin 可以很好地帮助消除在开发时，重复的但它仍创建 CSS 具有大量重复，从而导致大于必要的 CSS 文件的潜在性能问题。

现在，替换具有警报的 mixin`.alert`类，并更改`@include`到`@extend`(记住扩展`.alert`，而不`alert`):

```sass
.alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @extend .alert;
    border-color: green;
}

.error {
    @extend .alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

再次运行 Sass 并检查生成 CSS:

```css
.alert, .success, .error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    border-color: green;
}

.error {
    color: red;
    border-color: red;
    font-weight: bold;
}
```

现在仅作为很多时候根据需要定义属性，并更好地生成 CSS。

Sass 还包括函数和条件逻辑运算，类似于更少。 实际上，这两种语言的功能都非常相似。

## <a name="less-or-sass"></a>较低或 Sass？

还有关于是否通常最好使用更少或 Sass 不一致 （或甚至是否更喜欢原始 Sass 中较新的 SCSS 语法）。 最重要的决策是可能**使用这些工具之一**，而不是只需使用手工编码 CSS 文件。 后所做的决策，这两个不太和 Sass 是很好的选择。

## <a name="font-awesome"></a>Font Awesome

除了 CSS 预处理器是 Font Awesome 样式新式 web 应用程序的另一个不错的资源。 Font Awesome 是一个工具包，提供了 500 多个可以自由地使用 web 应用程序中的可缩放的向量图标。 它最初设计成可使用 Bootstrap，但它不依赖该框架或任何 JavaScript 库。

若要开始使用 Font Awesome 的最简单方法是添加对它，使用其公共内容交付网络 (CDN) 位置的引用：

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

您可以还将其添加到你的 Visual Studio 项目将其添加到"依赖关系"中*bower.json*:

```json
{
  "name": "ASP.NET",
  "private": true,
  "dependencies": {
    "bootstrap": "3.0.0",
    "jquery": "1.10.2",
    "jquery-validation": "1.11.1",
    "jquery-validation-unobtrusive": "3.2.2",
    "hammer.js": "2.0.4",
    "bootstrap-touch-carousel": "0.8.0",
    "Font-Awesome": "4.3.0"
  }
}
```

Font Awesome 为页面上的引用后，您可以将图标添加到你的应用程序通过应用 Font Awesome 类，通常为前缀"fa-"，对内联 HTML 元素 (如`<span>`或`<i>`)。  例如，可以将图标添加到简单列表和菜单使用如下代码：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <link href="lib/font-awesome/css/font-awesome.css" rel="stylesheet" />
</head>
<body>
    <ul class="fa-ul">
        <li><i class="fa fa-li fa-home"></i> Home</li>
        <li><i class="fa fa-li fa-cog"></i> Settings</li>
    </ul>
</body>
</html>
```

这会生成在浏览器中的以下-请注意每个项旁边的图标：

![列表图标](less-sass-fa/_static/list-icons-screenshot.png)

您可以查看可用的图标的完整列表：

http://fontawesome.io/icons/

## <a name="summary"></a>总结

新式 web 应用程序越来越多地要求响应迅速、 流畅干净、 直观，且易于使用不同的设备的设计。 管理实现这些目标所需的 CSS 样式表的复杂程度最好的做法是不太使用预处理器类似于或 Sass。 此外，如 Font Awesome 工具包快速提供到文本导航菜单的已知图标和按钮，从而提高整体用户体验的应用程序。
