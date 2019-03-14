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
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a><span data-ttu-id="cbdd7-103">更少，Sass 和 Font Awesome ASP.NET Core 中</span><span class="sxs-lookup"><span data-stu-id="cbdd7-103">Less, Sass, and Font Awesome in ASP.NET Core</span></span>

<span data-ttu-id="cbdd7-104">作者：[Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="cbdd7-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="cbdd7-105">Web 应用程序的用户时要设置的样式和整体体验有多越来越高的期望。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-105">Users of web applications have increasingly high expectations when it comes to style and overall experience.</span></span> <span data-ttu-id="cbdd7-106">新式 web 应用程序经常利用丰富的工具和框架，可用于定义和管理其外观和感觉以一致的方式。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-106">Modern web applications frequently leverage rich tools and frameworks for defining and managing their look and feel in a consistent manner.</span></span> <span data-ttu-id="cbdd7-107">框架喜欢[Bootstrap](http://getbootstrap.com/)可以转多地定义一组通用的样式和 web 站点的布局选项。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-107">Frameworks like [Bootstrap](http://getbootstrap.com/) can go a long way toward defining a common set of styles and layout options for web sites.</span></span> <span data-ttu-id="cbdd7-108">但是，最重要的站点还受益于能够有效地定义和维护样式和级联样式表 (CSS) 文件，以及具有对非图像的图标，可帮助使站点的接口更直观的轻松访问权。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-108">However, most non-trivial sites also benefit from being able to effectively define and maintain styles and cascading style sheet (CSS) files, as well as having easy access to non-image icons that help make the site's interface more intuitive.</span></span> <span data-ttu-id="cbdd7-109">这正是语言和支持的工具[更少](http://lesscss.org/)并[Sass](http://sass-lang.com/)，库等[Font Awesome](http://fontawesome.io/)，进入。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-109">That's where languages and tools that support [Less](http://lesscss.org/) and [Sass](http://sass-lang.com/), and libraries like [Font Awesome](http://fontawesome.io/), come in.</span></span>

## <a name="css-preprocessor-languages"></a><span data-ttu-id="cbdd7-110">CSS 预处理器语言</span><span class="sxs-lookup"><span data-stu-id="cbdd7-110">CSS preprocessor languages</span></span>

<span data-ttu-id="cbdd7-111">为了改进的基础语言的使用体验编译成其他语言的语言称为预处理器。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-111">Languages that are compiled into other languages, in order to improve the experience of working with the underlying language, are referred to as preprocessors.</span></span> <span data-ttu-id="cbdd7-112">有两个常用的预处理器的 CSS:较低和 Sass。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-112">There are two popular preprocessors for CSS: Less and Sass.</span></span>  <span data-ttu-id="cbdd7-113">这些预处理器将功能添加到 CSS，例如对变量和嵌套的规则，从而提高大型的复杂样式表的可维护性的支持。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-113">These preprocessors add features to CSS, such as support for variables and nested rules, which improve the maintainability of large, complex stylesheets.</span></span> <span data-ttu-id="cbdd7-114">作为一种语言的 CSS 是非常简单，缺少很简单，例如变量，即使对于支持，这往往会重复和臃肿使 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-114">CSS as a language is very basic, lacking support even for something as simple as variables, and this tends to make CSS files repetitive and bloated.</span></span> <span data-ttu-id="cbdd7-115">添加预处理器通过实际编程语言功能有助于减少重复，并提供更好地组织的样式规则。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-115">Adding real programming language features via preprocessors can help reduce duplication and provide better organization of styling rules.</span></span> <span data-ttu-id="cbdd7-116">Visual Studio 提供了对这两个不太的内置支持和 Sass，以及使用这些语言时可以进一步改进开发体验的扩展。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-116">Visual Studio provides built-in support for both Less and Sass, as well as extensions that can further improve the development experience when working with these languages.</span></span>

<span data-ttu-id="cbdd7-117">预处理器可以如何改进可读性和可维护性的样式信息的快速示例，请考虑以下 CSS:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-117">As a quick example of how preprocessors can improve readability and maintainability of style information, consider this CSS:</span></span>

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

<span data-ttu-id="cbdd7-118">使用更少，这可重写以消除所有重复项，使用*mixin* (如此命名是因为它允许您"混用"属性从一个类或到另一个规则集):</span><span class="sxs-lookup"><span data-stu-id="cbdd7-118">Using Less, this can be rewritten to eliminate all of the duplication, using a *mixin* (so named because it allows you to "mix in" properties from one class or rule-set into another):</span></span>

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

## <a name="less"></a><span data-ttu-id="cbdd7-119">Less</span><span class="sxs-lookup"><span data-stu-id="cbdd7-119">Less</span></span>

<span data-ttu-id="cbdd7-120">使用 Node.js 运行不到 CSS 预处理器。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-120">The Less CSS preprocessor runs using Node.js.</span></span> <span data-ttu-id="cbdd7-121">若要安装更少，使用节点包管理器 (npm) 从命令提示符 (-g 意味着"全局"):</span><span class="sxs-lookup"><span data-stu-id="cbdd7-121">To install Less, use Node Package Manager (npm) from a command prompt (-g means "global"):</span></span>

```console
npm install -g less
```

<span data-ttu-id="cbdd7-122">如果你使用 Visual Studio，你可以开始使用小于通过将一个或多个较少文件添加到你的项目，然后配置 Gulp （或 Grunt） 在编译时处理它们。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-122">If you're using Visual Studio, you can get started with Less by adding one or more Less files to your project, and then configuring Gulp (or Grunt) to process them at compile-time.</span></span> <span data-ttu-id="cbdd7-123">添加*样式*向你的项目的文件夹，然后添加新的名为的文件小于*main.less*到此文件夹。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-123">Add a *Styles* folder to your project, and then add a new Less file named *main.less* to this folder.</span></span>

![添加较少的文件](less-sass-fa/_static/add-less-file.png)

<span data-ttu-id="cbdd7-125">添加后，您的文件夹结构应如下所示：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-125">Once added, your folder structure should look something like this:</span></span>

![文件夹结构](less-sass-fa/_static/folder-structure.png)

<span data-ttu-id="cbdd7-127">现在可以到文件，这将编译到 CSS 并部署到 wwwroot 文件夹 Gulp 通过添加一些基本的样式设置。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-127">Now you can add some basic styling to the file, which will be compiled into CSS and deployed to the wwwroot folder by Gulp.</span></span>

<span data-ttu-id="cbdd7-128">修改*main.less*包括以下内容，从单一的基础颜色创建简单的调色板。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-128">Modify *main.less* to include the following content, which creates a simple color palette from a single base color.</span></span>

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

<span data-ttu-id="cbdd7-129">`@base` 和其他@-prefixed项是变量。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-129">`@base` and the other @-prefixed items are variables.</span></span> <span data-ttu-id="cbdd7-130">每个表示一种颜色。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-130">Each of them represents a color.</span></span> <span data-ttu-id="cbdd7-131">除`@base`，设置它们并使用颜色函数： 变浅，变暗，并且全局。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-131">Except for `@base`, they're set using color functions: lighten, darken, and spin.</span></span> <span data-ttu-id="cbdd7-132">淡化和加深不要这么多了您所期望的内容;数值调节钮调整由大量度 （大约颜色盘） 的一种颜色的色调。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-132">Lighten and darken do pretty much what you would expect; spin adjusts the hue of a color by a number of degrees (around the color wheel).</span></span> <span data-ttu-id="cbdd7-133">更少的处理器非常智能，可忽略不会使用的变量，因此若要演示这些变量的工作原理，我们需要某个位置使用它们。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-133">The Less processor is smart enough to ignore variables that aren't used, so to demonstrate how these variables work, we need to use them somewhere.</span></span> <span data-ttu-id="cbdd7-134">类`.baseColor`，等将演示在生成的 CSS 文件中的变量的计算的值。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-134">The classes `.baseColor`, etc. will demonstrate the calculated values of each of the variables in the CSS file that's produced.</span></span>

### <a name="get-started"></a><span data-ttu-id="cbdd7-135">入门</span><span class="sxs-lookup"><span data-stu-id="cbdd7-135">Get started</span></span>

<span data-ttu-id="cbdd7-136">创建**npm 配置文件**(*package.json*) 项目文件夹中编辑它以引用`gulp`和`gulp-less`:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-136">Create an **npm Configuration File** (*package.json*) in your project folder and edit it to reference `gulp` and `gulp-less`:</span></span>

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

<span data-ttu-id="cbdd7-137">在项目文件夹，或在 Visual Studio 中安装的依赖项是在命令提示符**解决方案资源管理器**(**依赖项 > npm > 还原包**)。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-137">Install the dependencies either at a command prompt in your project folder, or in Visual Studio **Solution Explorer** (**Dependencies > npm > Restore packages**).</span></span>

```console
npm install
```

![VS 还原包](less-sass-fa/_static/restore-packages.png)

<span data-ttu-id="cbdd7-139">在项目文件夹中，创建**Gulp 配置文件**(*gulpfile.js*) 来定义自动化的过程。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-139">In the project folder, create a **Gulp Configuration File** (*gulpfile.js*) to define the automated process.</span></span>  <span data-ttu-id="cbdd7-140">在较低，表示的文件和运行更少的任务的顶部添加一个变量：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-140">Add a variable at the top of the file to represent Less, and a task to run Less:</span></span>

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

<span data-ttu-id="cbdd7-141">打开**Task Runner Explorer** (**视图 > 其他 Windows > 任务运行程序资源管理器**)。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-141">Open the **Task Runner Explorer** (**View > Other Windows > Task Runner Explorer**).</span></span> <span data-ttu-id="cbdd7-142">在任务之间应会看到名为的新任务`less`。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-142">Among the tasks, you should see a new task named `less`.</span></span> <span data-ttu-id="cbdd7-143">您可能需要刷新窗口。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-143">You might have to refresh the window.</span></span>

<span data-ttu-id="cbdd7-144">运行`less`任务，并看到类似于此处所示的输出：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-144">Run the `less` task, and you see output similar to what is shown here:</span></span>

![更少的任务运行程序](less-sass-fa/_static/less-task-runner.png)

<span data-ttu-id="cbdd7-146">*Wwwroot/css*文件夹中现在包含新的文件*main.css*:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-146">The *wwwroot/css* folder now contains a new file, *main.css*:</span></span>

![创建主 css](less-sass-fa/_static/main-css-created.png)

<span data-ttu-id="cbdd7-148">打开*main.css* ，看到类似于以下内容：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-148">Open *main.css* and you see something like the following:</span></span>

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

<span data-ttu-id="cbdd7-149">添加到一个简单的 HTML 页面*wwwroot*文件夹，然后引用*main.css*若要查看操作中的调色板。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-149">Add a simple HTML page to the *wwwroot* folder, and reference *main.css* to see the color palette in action.</span></span>

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

<span data-ttu-id="cbdd7-150">您所见上旋转 180 度`@base`用来制作`@background`导致对立的颜色的颜色盘`@base`:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-150">You can see that the 180 degree spin on `@base` used to produce `@background` resulted in the color wheel opposing color of `@base`:</span></span>

![不到测试示例](less-sass-fa/_static/less-test-screenshot.png)

<span data-ttu-id="cbdd7-152">小于还提供对嵌套的规则，以及嵌套的媒体查询的支持。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-152">Less also provides support for nested rules, as well as nested media queries.</span></span> <span data-ttu-id="cbdd7-153">例如，像菜单可能会导致详细 CSS 规则的定义嵌套层次结构像这样:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-153">For example, defining nested hierarchies like menus can result in verbose CSS rules like these:</span></span>

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

<span data-ttu-id="cbdd7-154">理想情况下的所有相关的样式规则将被放在一起在 CSS 文件中，但实际上没有什么强制实施此规则约定和可能是块注释除外。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-154">Ideally all of the related style rules will be placed together within the CSS file, but in practice there's nothing enforcing this rule except convention and perhaps block comments.</span></span>

<span data-ttu-id="cbdd7-155">定义使用小于这些相同的规则如下所示：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-155">Defining these same rules using Less looks like this:</span></span>

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

<span data-ttu-id="cbdd7-156">请注意，在本例中为所有的从属元素`nav`包含其作用域内。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-156">Note that in this case, all of the subordinate elements of `nav` are contained within its scope.</span></span> <span data-ttu-id="cbdd7-157">不再有任何重复的父元素 (`nav`， `li`， `a`)，并已删除的总的行计数 （尽管某些这是将值放在第二个示例的同一行上的结果）。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-157">There's no longer any repetition of parent elements (`nav`, `li`, `a`), and the total line count has dropped as well (though some of that's a result of putting values on the same lines in the second example).</span></span> <span data-ttu-id="cbdd7-158">它可以是非常有用，组织，若要查看所有明确界定作用域内的给定用户界面元素的规则在这种情况下该文件的其余部分由设置大括号。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-158">It can be very helpful, organizationally, to see all of the rules for a given UI element within an explicitly bounded scope, in this case set off from the rest of the file by curly braces.</span></span>

<span data-ttu-id="cbdd7-159">`&`语法是使用较少的选择器功能，和表示当前的选择器父级。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-159">The `&` syntax is a Less selector feature, with & representing the current selector parent.</span></span> <span data-ttu-id="cbdd7-160">这样，在 {...}</span><span class="sxs-lookup"><span data-stu-id="cbdd7-160">So, within the a {...}</span></span> <span data-ttu-id="cbdd7-161">块中，`&`表示`a`标记，并因此`&:link`等效于`a:link`。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-161">block, `&` represents an `a` tag, and thus `&:link` is equivalent to `a:link`.</span></span>

<span data-ttu-id="cbdd7-162">创建响应式设计中非常有用的媒体查询可以也是导致很大程度重复和 CSS 中的复杂性。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-162">Media queries, extremely useful in creating responsive designs, can also contribute heavily to repetition and complexity in CSS.</span></span> <span data-ttu-id="cbdd7-163">小于允许媒体查询在嵌套在类中，以便在整个类定义不需要重复出现在不同顶级`@media`元素。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-163">Less allows media queries to be nested within classes, so that the entire class definition doesn't need to be repeated within different top-level `@media` elements.</span></span> <span data-ttu-id="cbdd7-164">例如，下面是响应式菜单的 CSS:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-164">For example, here is CSS for a responsive menu:</span></span>

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

<span data-ttu-id="cbdd7-165">这可以以秒为更好地定义：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-165">This can be better defined in Less as:</span></span>

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

<span data-ttu-id="cbdd7-166">小于我们已经看到的另一项功能是它支持适用于数学运算，从而允许从预定义的变量构造的样式特性。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-166">Another feature of Less that we have already seen is its support for mathematical operations, allowing style attributes to be constructed from pre-defined variables.</span></span> <span data-ttu-id="cbdd7-167">这使得更新相关的样式更加容易，因为可以修改基变量和所有相关值自动更改。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-167">This makes updating related styles much easier, since the base variable can be modified and all dependent values change automatically.</span></span>

<span data-ttu-id="cbdd7-168">CSS 文件，尤其是对于大型站点 （和尤其是如果要使用媒体查询），往往会获得很大随着时间推移，从而使用它们难以处理。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-168">CSS files, especially for large sites (and especially if media queries are being used), tend to get quite large over time, making working with them unwieldy.</span></span> <span data-ttu-id="cbdd7-169">Less 文件可以单独定义的随后将提取使用`@import`指令。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-169">Less files can be defined separately, then pulled together using `@import` directives.</span></span> <span data-ttu-id="cbdd7-170">小于还可用来导入单个 CSS 文件，同样，如果所需的。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-170">Less can also be used to import individual CSS files, as well, if desired.</span></span>

<span data-ttu-id="cbdd7-171">*Mixin*可以接受参数，并小于支持 mixin 临界条件，以声明方式定义某些 mixin 生效的窗体中的条件逻辑。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-171">*Mixins* can accept parameters, and Less supports conditional logic in the form of mixin guards, which provide a declarative way to define when certain mixins take effect.</span></span> <span data-ttu-id="cbdd7-172">Mixin 临界条件的一个常见用途是调整基于如何光的颜色或深色源颜色是。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-172">A common use for mixin guards is to adjust colors based on how light or dark the source color is.</span></span> <span data-ttu-id="cbdd7-173">Mixin 防护给定 mixin 接受颜色的参数，用于修改基于该颜色 mixin:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-173">Given a mixin that accepts a parameter for color, a mixin guard can be used to modify the mixin based on that color:</span></span>

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

<span data-ttu-id="cbdd7-174">指定当前`@base`的值`#663333`，小于此脚本将生成以下 CSS:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-174">Given our current `@base` value of `#663333`, this Less script will produce the following CSS:</span></span>

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

<span data-ttu-id="cbdd7-175">小于提供了很多其他功能，但这应当会提供此功能的一些思路预处理语言。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-175">Less provides a number of additional features, but this should give you some idea of the power of this preprocessing language.</span></span>

## <a name="sass"></a><span data-ttu-id="cbdd7-176">Sass</span><span class="sxs-lookup"><span data-stu-id="cbdd7-176">Sass</span></span>

<span data-ttu-id="cbdd7-177">Sass 是类似于更少，提供对许多相同的功能，但稍有不同的语法的支持。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-177">Sass is similar to Less, providing support for many of the same features, but with slightly different syntax.</span></span> <span data-ttu-id="cbdd7-178">它使用 Ruby，而不是 JavaScript，构建，因此不同的安装要求。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-178">It's built using Ruby, rather than JavaScript, and so has different setup requirements.</span></span> <span data-ttu-id="cbdd7-179">原始 Sass 语言没有使用大括号或分号，而定义使用空白和缩进作用域。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-179">The original Sass language didn't use curly braces or semicolons, but instead defined scope using white space and indentation.</span></span> <span data-ttu-id="cbdd7-180">在版本 3 的 Sass，引入了一种新语法， **SCSS** ("Sassy CSS")。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-180">In version 3 of Sass, a new syntax was introduced, **SCSS** ("Sassy CSS").</span></span> <span data-ttu-id="cbdd7-181">SCSS 是类似于 CSS 它忽略缩进级别和空格，并改为使用分号和大括号。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-181">SCSS is similar to CSS in that it ignores indentation levels and whitespace, and instead uses semicolons and curly braces.</span></span>

<span data-ttu-id="cbdd7-182">若要安装 Sass，通常您将首先安装 Ruby （预装在 macOS 上），并运行：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-182">To install Sass, typically you would first install Ruby (pre-installed on macOS), and then run:</span></span>

```console
gem install sass
```

<span data-ttu-id="cbdd7-183">但是，如果要运行 Visual Studio，你可以开始使用 Sass 在很大程度相同的方式就像使用更少。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-183">However, if you're running Visual Studio, you can get started with Sass in much the same way as you would with Less.</span></span> <span data-ttu-id="cbdd7-184">打开*package.json*和"gulp sass"将包添加到`devDependencies`:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-184">Open *package.json* and add the "gulp-sass" package to `devDependencies`:</span></span>

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

<span data-ttu-id="cbdd7-185">接下来，修改*gulpfile.js*添加 sass 变量和要编译 Sass 文件并将结果放在 wwwroot 文件夹中的任务：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-185">Next, modify *gulpfile.js* to add a sass variable and a task to compile your Sass files and place the results in the wwwroot folder:</span></span>

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

<span data-ttu-id="cbdd7-186">现在，可以添加 Sass 文件*main2.scss*到*样式*中项目的根文件夹：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-186">Now you can add the Sass file *main2.scss* to the *Styles* folder in the root of the project:</span></span>

![添加 scss 文件](less-sass-fa/_static/add-scss-file.png)

<span data-ttu-id="cbdd7-188">打开*main2.scss*并添加以下：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-188">Open *main2.scss* and add the following:</span></span>

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

<span data-ttu-id="cbdd7-189">保存所有文件。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-189">Save all of your files.</span></span> <span data-ttu-id="cbdd7-190">现在刷新**Task Runner Explorer**，则请参阅`sass`任务。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-190">Now when you refresh **Task Runner Explorer**, you see a `sass` task.</span></span> <span data-ttu-id="cbdd7-191">运行它，并查找 */wwwroot/css*文件夹。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-191">Run it, and look in the */wwwroot/css* folder.</span></span> <span data-ttu-id="cbdd7-192">现在还有*main2.css*文件中的，使用以下内容：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-192">There's now a *main2.css* file, with these contents:</span></span>

```css
body {
    background-color: #CC0000;
}
```

<span data-ttu-id="cbdd7-193">Sass 支持嵌套在很大程度相同时，小于实现，它提供了类似的优势。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-193">Sass supports nesting in much the same was that Less does, providing similar benefits.</span></span> <span data-ttu-id="cbdd7-194">文件可以拆分函数并且包含使用`@import`指令：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-194">Files can be split up by function and included using the `@import` directive:</span></span>

```sass
@import 'anotherfile';
```

<span data-ttu-id="cbdd7-195">Sass 支持 mixin，使用`@mixin`关键字来定义它们并`@include`来包含它们从如此示例所示[sass lang.com](http://sass-lang.com):</span><span class="sxs-lookup"><span data-stu-id="cbdd7-195">Sass supports mixins as well, using the `@mixin` keyword to define them and `@include` to include them, as in this example from [sass-lang.com](http://sass-lang.com):</span></span>

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

<span data-ttu-id="cbdd7-196">Sass mixin，除了它还支持继承，的概念允许一个类来扩展另一个。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-196">In addition to mixins, Sass also supports the concept of inheritance, allowing one class to extend another.</span></span> <span data-ttu-id="cbdd7-197">它是从概念上讲类似于一个 mixin，但在更少的 CSS 代码中的结果。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-197">It's conceptually similar to a mixin, but results in less CSS code.</span></span> <span data-ttu-id="cbdd7-198">它通过`@extend`关键字。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-198">It's accomplished using the `@extend` keyword.</span></span> <span data-ttu-id="cbdd7-199">若要试用 mixin，将以下代码添加到您*main2.scss*文件：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-199">To try out mixins, add the following to your *main2.scss* file:</span></span>

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

<span data-ttu-id="cbdd7-200">检查中的输出*main2.css*运行之后`sass`中的任务**Task Runner Explorer**:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-200">Examine the output in *main2.css* after running the `sass` task in **Task Runner Explorer**:</span></span>

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

<span data-ttu-id="cbdd7-201">请注意，所有警报的 mixin 的常见属性在每个类中有重复。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-201">Notice that all of the common properties of the alert mixin are repeated in each class.</span></span> <span data-ttu-id="cbdd7-202">Mixin 可以很好地帮助消除在开发时，重复的但它仍创建 CSS 具有大量重复，从而导致大于必要的 CSS 文件的潜在性能问题。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-202">The mixin did a good job of helping eliminate duplication at development time, but it's still creating CSS with a lot of duplication in it, resulting in larger than necessary CSS files - a potential performance issue.</span></span>

<span data-ttu-id="cbdd7-203">现在，替换具有警报的 mixin`.alert`类，并更改`@include`到`@extend`(记住扩展`.alert`，而不`alert`):</span><span class="sxs-lookup"><span data-stu-id="cbdd7-203">Now replace the alert mixin with a `.alert` class, and change `@include` to `@extend` (remembering to extend `.alert`, not `alert`):</span></span>

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

<span data-ttu-id="cbdd7-204">再次运行 Sass 并检查生成 CSS:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-204">Run Sass once more, and examine the resulting CSS:</span></span>

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

<span data-ttu-id="cbdd7-205">现在仅作为很多时候根据需要定义属性，并更好地生成 CSS。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-205">Now the properties are defined only as many times as needed, and better CSS is generated.</span></span>

<span data-ttu-id="cbdd7-206">Sass 还包括函数和条件逻辑运算，类似于更少。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-206">Sass also includes functions and conditional logic operations, similar to Less.</span></span> <span data-ttu-id="cbdd7-207">实际上，这两种语言的功能都非常相似。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-207">In fact, the two languages' capabilities are very similar.</span></span>

## <a name="less-or-sass"></a><span data-ttu-id="cbdd7-208">较低或 Sass？</span><span class="sxs-lookup"><span data-stu-id="cbdd7-208">Less or Sass?</span></span>

<span data-ttu-id="cbdd7-209">还有关于是否通常最好使用更少或 Sass 不一致 （或甚至是否更喜欢原始 Sass 中较新的 SCSS 语法）。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-209">There's still no consensus as to whether it's generally better to use Less or Sass (or even whether to prefer the original Sass or the newer SCSS syntax within Sass).</span></span> <span data-ttu-id="cbdd7-210">最重要的决策是可能**使用这些工具之一**，而不是只需使用手工编码 CSS 文件。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-210">Probably the most important decision is to **use one of these tools**, as opposed to just hand-coding your CSS files.</span></span> <span data-ttu-id="cbdd7-211">后所做的决策，这两个不太和 Sass 是很好的选择。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-211">Once you've made that decision, both Less and Sass are good choices.</span></span>

## <a name="font-awesome"></a><span data-ttu-id="cbdd7-212">Font Awesome</span><span class="sxs-lookup"><span data-stu-id="cbdd7-212">Font Awesome</span></span>

<span data-ttu-id="cbdd7-213">除了 CSS 预处理器是 Font Awesome 样式新式 web 应用程序的另一个不错的资源。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-213">In addition to CSS preprocessors, another great resource for styling modern web applications is Font Awesome.</span></span> <span data-ttu-id="cbdd7-214">Font Awesome 是一个工具包，提供了 500 多个可以自由地使用 web 应用程序中的可缩放的向量图标。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-214">Font Awesome is a toolkit that provides over 500 scalable vector icons that can be freely used in your web applications.</span></span> <span data-ttu-id="cbdd7-215">它最初设计成可使用 Bootstrap，但它不依赖该框架或任何 JavaScript 库。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-215">It was originally designed to work with Bootstrap, but it has no dependency on that framework or on any JavaScript libraries.</span></span>

<span data-ttu-id="cbdd7-216">若要开始使用 Font Awesome 的最简单方法是添加对它，使用其公共内容交付网络 (CDN) 位置的引用：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-216">The easiest way to get started with Font Awesome is to add a reference to it, using its public content delivery network (CDN) location:</span></span>

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

<span data-ttu-id="cbdd7-217">您可以还将其添加到你的 Visual Studio 项目将其添加到"依赖关系"中*bower.json*:</span><span class="sxs-lookup"><span data-stu-id="cbdd7-217">You can also add it to your Visual Studio project by adding it to the "dependencies" in *bower.json*:</span></span>

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

<span data-ttu-id="cbdd7-218">Font Awesome 为页面上的引用后，您可以将图标添加到你的应用程序通过应用 Font Awesome 类，通常为前缀"fa-"，对内联 HTML 元素 (如`<span>`或`<i>`)。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-218">Once you have a reference to Font Awesome on a page, you can add icons to your application by applying Font Awesome classes, typically prefixed with "fa-", to your inline HTML elements (such as `<span>` or `<i>`).</span></span>  <span data-ttu-id="cbdd7-219">例如，可以将图标添加到简单列表和菜单使用如下代码：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-219">For example, you can add icons to simple lists and menus using code like this:</span></span>

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

<span data-ttu-id="cbdd7-220">这会生成在浏览器中的以下-请注意每个项旁边的图标：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-220">This produces the following in the browser - note the icon beside each item:</span></span>

![列表图标](less-sass-fa/_static/list-icons-screenshot.png)

<span data-ttu-id="cbdd7-222">您可以查看可用的图标的完整列表：</span><span class="sxs-lookup"><span data-stu-id="cbdd7-222">You can view a complete list of the available icons here:</span></span>

http://fontawesome.io/icons/

## <a name="summary"></a><span data-ttu-id="cbdd7-223">总结</span><span class="sxs-lookup"><span data-stu-id="cbdd7-223">Summary</span></span>

<span data-ttu-id="cbdd7-224">新式 web 应用程序越来越多地要求响应迅速、 流畅干净、 直观，且易于使用不同的设备的设计。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-224">Modern web applications increasingly demand responsive, fluid designs that are clean, intuitive, and easy to use from a variety of devices.</span></span> <span data-ttu-id="cbdd7-225">管理实现这些目标所需的 CSS 样式表的复杂程度最好的做法是不太使用预处理器类似于或 Sass。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-225">Managing the complexity of the CSS stylesheets required to achieve these goals is best done using a preprocessor like Less or Sass.</span></span> <span data-ttu-id="cbdd7-226">此外，如 Font Awesome 工具包快速提供到文本导航菜单的已知图标和按钮，从而提高整体用户体验的应用程序。</span><span class="sxs-lookup"><span data-stu-id="cbdd7-226">In addition, toolkits like Font Awesome quickly provide well-known icons to textual navigation menus and buttons, improving the overall user experience of your application.</span></span>
