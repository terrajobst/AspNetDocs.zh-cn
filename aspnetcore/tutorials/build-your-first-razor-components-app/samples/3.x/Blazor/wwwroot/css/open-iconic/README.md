---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054214"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[Open Iconic v1.1.1](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a>Open Iconic 是 [Iconic](http://useiconic.com) 的开放源代码同级。 它是一个超清晰的包括 223 种图标的集合，内存占用很小 &mdash; 可以与 Bootstrap 和 Foundation 配合使用。 [查看集合](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>什么是 Open Iconic？

* 低至 8 像素、清晰可辨的 223 种图标
* 整套的超轻型 SVG 文件 - 61.8 
* SVG 子画面 &mdash; 图标字体的新式替代
* Webfont（EOT、OTF、SVG、TTF、WOFF）、PNG 和 WebP 格式
* CSS、LESS、SCSS 和 Stylus 格式的 Webfont 样式表（包括 Bootstrap 和 Foundation 版本）
* 8px、16px、24px、32 px、48px 和 64px 的 PNG 和 WebP 光栅图像。


## <a name="getting-started"></a>入门

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a>有关代码示例和开始使用 Open Iconic 所需的其他内容，请查看我们的[图标](http://useiconic.com/open#icons)和[引用](http://useiconic.com/open#reference)部分。

### <a name="general-usage"></a>常规使用情况

#### <a name="using-open-iconics-svgs"></a>使用 Open Iconic 的 SVG

我们喜欢 SVG，认为它是在 Web 上显示图标的一种方式。 由于 Open Iconic 都是基本 SVG，建议像任何其他图像一样显示它们（别忘了 `alt` 属性）。

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>使用 Open Iconic 的 SVG 子画面

Open Iconic 还提供 SVG 子画面，允许你通过单个请求显示集合中的所有图标。 它就像一个图标字体，无需非法侵入。

从 SVG 子画面添加图标与以往的做法略有不同，但仍是小菜一碟。 提示：若要使图标易于样式化，建议将常规类添加到 `<svg>` 标记并为*`<use>`*  标记中的每个不同图标添加唯一类名。  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

调整图标大小只需要基本 CSS。 所有图标都是正方形格式，所以只需将 `<svg>` 标记设置为宽度和高度相同的尺寸。

```
.icon {
  width: 16px;
  height: 16px;
}
```

着色图标更简单。 只需对 `<use>` 标记设置 `fill` 规则。

```
.icon-account-login {
  fill: #f00;
}
```

若要了解有关 SVG 子画面的详细信息，请阅读 [Chris Coyier 指南](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)。

#### <a name="using-open-iconics-icon-font"></a>使用 Open Iconic 的图标字体...


##### <a name="with-bootstrap"></a>...结合 Bootstrap

可以在 `font/css/open-iconic-bootstrap.{css, less, scss, styl}` 中找到在我们的 Bootstrap 样式表


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>...结合 Foundation

可以在 `font/css/open-iconic-foundation.{css, less, scss, styl}` 中找到在我们的 Foundation 样式表

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>…单独

可以在 `font/css/open-iconic.{css, less, scss, styl}` 中找到在我们的默认样式表

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>许可证

### <a name="icons"></a>图标

所有代码（包括 SVG 标记）都在 [MIT 许可证](http://opensource.org/licenses/MIT)下。

### <a name="fonts"></a>字体

所有字体都在 [SIL 许可](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web)下。
