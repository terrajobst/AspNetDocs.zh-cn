---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064844"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[<span data-ttu-id="df914-101">Open Iconic v1.1.1</span><span class="sxs-lookup"><span data-stu-id="df914-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a><span data-ttu-id="df914-102">Open Iconic 是 [Iconic](http://useiconic.com) 的开放源代码同级。</span><span class="sxs-lookup"><span data-stu-id="df914-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="df914-103">它是一个超清晰的包括 223 种图标的集合，内存占用很小 &mdash; 可以与 Bootstrap 和 Foundation 配合使用。</span><span class="sxs-lookup"><span data-stu-id="df914-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="df914-104">查看集合</span><span class="sxs-lookup"><span data-stu-id="df914-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="df914-105">什么是 Open Iconic？</span><span class="sxs-lookup"><span data-stu-id="df914-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="df914-106">低至 8 像素、清晰可辨的 223 种图标</span><span class="sxs-lookup"><span data-stu-id="df914-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="df914-107">整套的超轻型 SVG 文件 - 61.8</span><span class="sxs-lookup"><span data-stu-id="df914-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="df914-108">SVG 子画面 &mdash; 图标字体的新式替代</span><span class="sxs-lookup"><span data-stu-id="df914-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="df914-109">Webfont（EOT、OTF、SVG、TTF、WOFF）、PNG 和 WebP 格式</span><span class="sxs-lookup"><span data-stu-id="df914-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="df914-110">CSS、LESS、SCSS 和 Stylus 格式的 Webfont 样式表（包括 Bootstrap 和 Foundation 版本）</span><span class="sxs-lookup"><span data-stu-id="df914-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="df914-111">8px、16px、24px、32 px、48px 和 64px 的 PNG 和 WebP 光栅图像。</span><span class="sxs-lookup"><span data-stu-id="df914-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="df914-112">入门</span><span class="sxs-lookup"><span data-stu-id="df914-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a><span data-ttu-id="df914-113">有关代码示例和开始使用 Open Iconic 所需的其他内容，请查看我们的[图标](http://useiconic.com/open#icons)和[引用](http://useiconic.com/open#reference)部分。</span><span class="sxs-lookup"><span data-stu-id="df914-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="df914-114">常规使用情况</span><span class="sxs-lookup"><span data-stu-id="df914-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="df914-115">使用 Open Iconic 的 SVG</span><span class="sxs-lookup"><span data-stu-id="df914-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="df914-116">我们喜欢 SVG，认为它是在 Web 上显示图标的一种方式。</span><span class="sxs-lookup"><span data-stu-id="df914-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="df914-117">由于 Open Iconic 都是基本 SVG，建议像任何其他图像一样显示它们（别忘了 `alt` 属性）。</span><span class="sxs-lookup"><span data-stu-id="df914-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="df914-118">使用 Open Iconic 的 SVG 子画面</span><span class="sxs-lookup"><span data-stu-id="df914-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="df914-119">Open Iconic 还提供 SVG 子画面，允许你通过单个请求显示集合中的所有图标。</span><span class="sxs-lookup"><span data-stu-id="df914-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="df914-120">它就像一个图标字体，无需非法侵入。</span><span class="sxs-lookup"><span data-stu-id="df914-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="df914-121">从 SVG 子画面添加图标与以往的做法略有不同，但仍是小菜一碟。</span><span class="sxs-lookup"><span data-stu-id="df914-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="df914-122">提示：若要使图标易于样式化，建议将常规类添加到 `<svg>` 标记并为*`<use>`*  标记中的每个不同图标添加唯一类名。</span><span class="sxs-lookup"><span data-stu-id="df914-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="df914-123">调整图标大小只需要基本 CSS。</span><span class="sxs-lookup"><span data-stu-id="df914-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="df914-124">所有图标都是正方形格式，所以只需将 `<svg>` 标记设置为宽度和高度相同的尺寸。</span><span class="sxs-lookup"><span data-stu-id="df914-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="df914-125">着色图标更简单。</span><span class="sxs-lookup"><span data-stu-id="df914-125">Coloring icons is even easier.</span></span> <span data-ttu-id="df914-126">只需对 `<use>` 标记设置 `fill` 规则。</span><span class="sxs-lookup"><span data-stu-id="df914-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="df914-127">若要了解有关 SVG 子画面的详细信息，请阅读 [Chris Coyier 指南](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)。</span><span class="sxs-lookup"><span data-stu-id="df914-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="df914-128">使用 Open Iconic 的图标字体...</span><span class="sxs-lookup"><span data-stu-id="df914-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="df914-129">...结合 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="df914-129">…with Bootstrap</span></span>

<span data-ttu-id="df914-130">可以在 `font/css/open-iconic-bootstrap.{css, less, scss, styl}` 中找到在我们的 Bootstrap 样式表</span><span class="sxs-lookup"><span data-stu-id="df914-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="df914-131">...结合 Foundation</span><span class="sxs-lookup"><span data-stu-id="df914-131">…with Foundation</span></span>

<span data-ttu-id="df914-132">可以在 `font/css/open-iconic-foundation.{css, less, scss, styl}` 中找到在我们的 Foundation 样式表</span><span class="sxs-lookup"><span data-stu-id="df914-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="df914-133">…单独</span><span class="sxs-lookup"><span data-stu-id="df914-133">…on its own</span></span>

<span data-ttu-id="df914-134">可以在 `font/css/open-iconic.{css, less, scss, styl}` 中找到在我们的默认样式表</span><span class="sxs-lookup"><span data-stu-id="df914-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="df914-135">许可证</span><span class="sxs-lookup"><span data-stu-id="df914-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="df914-136">图标</span><span class="sxs-lookup"><span data-stu-id="df914-136">Icons</span></span>

<span data-ttu-id="df914-137">所有代码（包括 SVG 标记）都在 [MIT 许可证](http://opensource.org/licenses/MIT)下。</span><span class="sxs-lookup"><span data-stu-id="df914-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="df914-138">字体</span><span class="sxs-lookup"><span data-stu-id="df914-138">Fonts</span></span>

<span data-ttu-id="df914-139">所有字体都在 [SIL 许可](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web)下。</span><span class="sxs-lookup"><span data-stu-id="df914-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>
