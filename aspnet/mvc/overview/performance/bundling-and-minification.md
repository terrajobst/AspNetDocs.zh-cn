---
uid: mvc/overview/performance/bundling-and-minification
title: 绑定和缩减 |Microsoft Docs
author: Rick-Anderson
description: 绑定和缩减是可以在 ASP.NET 4.5 中使用的两种技术来提高请求加载时间。 绑定和缩减通过 reducin 缩短加载时间 。
ms.author: riande
ms.date: 08/23/2012
ms.assetid: 5894dc13-5d45-4dad-8096-136499120f1d
msc.legacyurl: /mvc/overview/performance/bundling-and-minification
msc.type: authoredcontent
ms.openlocfilehash: 61bfe5dbac04b57e1461183b66ead2f01fe0734c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432950"
---
# <a name="bundling-and-minification"></a>Bundling and Minification（绑定和缩小）

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

> 绑定和缩减是可以在 ASP.NET 4.5 中使用的两种技术来提高请求加载时间。 绑定和缩减减少了对服务器的请求数并减小了请求资产（如 CSS 和 JavaScript）的大小，从而缩短了加载时间。

大多数当前的主要浏览器将每个主机名的[同时连接](http://www.browserscope.org/?category=network)数限制为6。 这意味着，在处理六个请求时，对主机上的资产的其他请求将由浏览器进行排队。 在下图中，IE F12 开发人员工具网络选项卡显示示例应用程序的 "关于" 视图所需的资产计时。

![B/M](bundling-and-minification/_static/image1.png)

灰色条显示了在浏览器等待六个连接限制时，请求排队的时间。 黄色条为第一字节的请求时间，即，发送请求和接收来自服务器的第一个响应所需的时间。 蓝条显示从服务器接收响应数据所用的时间。 可以双击某个资产获取详细计时信息。 例如，下图显示了用于加载 */Scripts/MyScripts/JavaScript6.js*文件的计时详细信息。

![](bundling-and-minification/_static/image2.png)

上图显示了**开始**事件，此事件提供请求排队的时间，因为浏览器会限制同时连接的数量。 在这种情况下，请求会排队等候等待另一个请求完成的46毫秒。

## <a name="bundling"></a>捆绑

捆绑是 ASP.NET 4.5 中的一项新功能，可轻松地将多个文件组合或捆绑到一个文件中。 你可以创建 CSS、JavaScript 和其他捆绑包。 较少的文件意味着 HTTP 请求更少，并且可以提高首页加载性能。

下图显示了与前面所示的 "关于" 视图相同的计时视图，但此时启用了绑定和缩减。

![](bundling-and-minification/_static/image3.png)

## <a name="minification"></a>缩减

缩减对脚本或 css 执行各种不同的代码优化，如删除不必要的空白和注释并缩短变量名称为一个字符。 请考虑以下 JavaScript 函数。

[!code-javascript[Main](bundling-and-minification/samples/sample1.js)]

缩减之后，该函数将缩小为以下内容：

[!code-javascript[Main](bundling-and-minification/samples/sample2.js)]

除了删除注释和不必要的空格外，以下参数和变量名称已重命名（缩短），如下所示：

| **原始** | **更名** |
| --- | --- |
| imageTagAndImageID | n |
| imageContext | t |
| imageElement | i |

## <a name="impact-of-bundling-and-minification"></a>绑定和缩减的影响

下表显示了几个重要的差异，分别列出了每个资产，并使用了示例程序中的绑定和缩减（B/M）。

|  | **使用 B/M** | **无 B/M** | **更改** |
| --- | --- | --- | --- |
| **文件请求** | 9 | 34 | 256% |
| **已发送 KB** | 3.26 | 11.92 | 266% |
| **已收到 KB** | 388.51 | 530 | 36% |
| **加载时间** | 510 MS | 780 MS | 53% |

发送的字节数明显降低，因为浏览器与它们应用于请求的 HTTP 标头非常详细。 接收的字节数减少不大，因为最大文件（*脚本\\jquery-ui-* 和*脚本\\/selfservice/scripts/jquery-1.10.2.min.js 1.7.1*）已缩小。 注意：示例程序上的计时使用[Fiddler](http://www.fiddler2.com/fiddler2/)工具来模拟慢速网络。 （从 "Fiddler**规则**" 菜单中，选择 "**性能**"，然后**模拟调制解调器速度**。）

## <a name="debugging-bundled-and-minified-javascript"></a>调试捆绑的和缩小的 JavaScript

可以轻松地在开发环境中调试 JavaScript （其中*web.config*文件中的[编译元素](https://msdn.microsoft.com/library/s10awwz0.aspx)设置为 `debug="true"`），因为 javascript 文件不是捆绑的或缩小的。 你还可以调试在其中捆绑了 JavaScript 文件并缩小的发布版本。 使用 IE F12 开发人员工具，可以使用以下方法调试缩小捆绑中包含的 JavaScript 函数：

1. 选择 "**脚本**" 选项卡，然后选择 "**启动调试**" 按钮。
2. 使用 "资产" 按钮选择包含要调试的 JavaScript 函数的捆绑包。  
    ![](bundling-and-minification/_static/image4.png)
3. 通过选择 "**配置" 按钮**![](bundling-and-minification/_static/image5.png)设置缩小 javascript 的格式，然后选择 "**设置 javascript 格式**"。
4. 在 "**搜索脚本**" 输入框中，选择要调试的函数的名称。 在下图中，在 "**搜索脚本**" 输入框中输入**AddAltToImg** 。  
    ![](bundling-and-minification/_static/image6.png)

有关使用 F12 开发人员工具进行调试的详细信息，请参阅 MSDN 文章[使用 f12 开发人员工具调试 JavaScript 错误](https://msdn.microsoft.com/library/ie/gg699336(v=vs.85).aspx)。

## <a name="controlling-bundling-and-minification"></a>控制绑定和缩减

通过在*web.config 文件中的*[编译元素](https://msdn.microsoft.com/library/s10awwz0.aspx)中设置 debug 属性的值，可启用或禁用绑定和缩减。 在下面的 XML 中，`debug` 设置为 true，因此将禁用捆绑和缩减。

[!code-xml[Main](bundling-and-minification/samples/sample3.xml?highlight=2)]

若要启用捆绑和缩减，请将 `debug` 值设置为 "false"。 您可以用 `BundleTable`*类的 `EnableOptimizations`* 属性覆盖 web.config 设置。 下面的代码启用绑定和缩减，并覆盖*web.config*文件中的任何设置。

[!code-csharp[Main](bundling-and-minification/samples/sample4.cs?highlight=7)]

> [!NOTE]
> 除非 `true` `EnableOptimizations` 或*web.config 文件中的*[编译元素](https://msdn.microsoft.com/library/s10awwz0.aspx)中的 debug 特性设置为 `false`，否则，将不会捆绑文件或缩小文件。 此外，将不会使用文件的最小版本，将选择完整的调试版本。 `EnableOptimizations` 重写*web.config*文件中的[编译元素](https://msdn.microsoft.com/library/s10awwz0.aspx)中的 debug 特性

## <a name="using-bundling-and-minification-with-aspnet-web-forms-and-web-pages"></a>将绑定和缩减用于 ASP.NET Web 窗体和网页

- 对于网页，请参阅[将 Web 优化添加到网页站点](https://docs.microsoft.com/archive/blogs/rickandy/adding-web-optimization-to-a-web-pages-site)中的博客文章。
- 对于 Web 窗体，请参阅博客文章[将绑定和缩减添加到 Web 窗体](https://docs.microsoft.com/archive/blogs/rickandy/adding-bundling-and-minification-to-web-forms)。

## <a name="using-bundling-and-minification-with-aspnet-mvc"></a>将绑定和缩减用于 ASP.NET MVC

在本部分中，我们将创建一个 ASP.NET MVC 项目来检查绑定和缩减。 首先，创建一个名为**MvcBM**的新 ASP.NET MVC internet 项目，而无需更改任何默认值。

打开*应用程序\\\_启动\\BundleConfig.cs*文件，并检查用于创建、注册和配置绑定的 `RegisterBundles` 方法。 下面的代码演示 `RegisterBundles` 方法的一部分。

[!code-csharp[Main](bundling-and-minification/samples/sample5.cs)]

前面的代码将创建一个名为 *~/bundles/jquery*的新 JavaScript 包，其中包含所有合适的（即 debug 或缩小，但不包括）。*vsdoc*）*文件，该文件夹与*通配符 "~/Scripts/jquery-{version}.js" 匹配。 对于 ASP.NET MVC 4，这意味着，对于调试配置，会将文件 */selfservice/scripts/jquery-1.10.2.min.js 1.7.1*添加到绑定中。 在发布配置中，将添加 */selfservice/scripts/jquery-1.10.2.min.js 1.7.1* 。 绑定框架遵循几个常见约定，如：

- 如果存在*FileX*和*FileX* ，则选择 "文件" 进行发布。
- 选择要调试的非 "min" 版本。
- 忽略仅由 IntelliSense 使用的 "-vsdoc" 文件（如 */selfservice/scripts/jquery-1.10.2.min.js 1.7.1-vsdoc*）。

上面所示的 `{version}` 通配符用于在*脚本*文件夹中自动创建具有适当版本 jQuery 的 jquery 包。 在此示例中，使用通配符具有以下优势：

- 允许你使用 NuGet 更新到较新的 jQuery 版本，而无需在视图页中更改前面的绑定代码或 jQuery 引用。
- 将自动选择调试配置的完整版本，并为发布版本自动选择 "min" 版本。

## <a name="using-a-cdn"></a>使用 CDN

 以下代码使用 CDN jQuery 束替换本地 jQuery 包。

[!code-csharp[Main](bundling-and-minification/samples/sample6.cs)]

在上面的代码中，在发布模式下将从 CDN 请求 jQuery，并在调试模式下以本地方式提取 jQuery 的调试版本。 使用 CDN 时，应具有回退机制，以防 CDN 请求失败。 布局文件末尾的以下标记片段显示在 CDN 出现故障时，添加到请求 jQuery 的脚本。

[!code-cshtml[Main](bundling-and-minification/samples/sample7.cshtml?highlight=5-13)]

## <a name="creating-a-bundle"></a>创建捆绑包

[捆绑](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)类 `Include` 方法采用字符串数组，其中每个字符串都是资源的虚拟路径。 以下从应用中的 `RegisterBundles` 方法中的代码 *\\\_Start\\BundleConfig.cs*文件中显示如何将多个文件添加到捆绑包：

[!code-csharp[Main](bundling-and-minification/samples/sample8.cs)]

提供[捆绑](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)类 `IncludeDirectory` 方法，以添加与搜索模式匹配的目录（以及所有子目录）中的所有文件。 [包](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx)类 `IncludeDirectory` API 如下所示：

[!code-csharp[Main](bundling-and-minification/samples/sample9.cs)]

使用 Render 方法（用于 CSS 的`Styles.Render` 和 JavaScript 的 `Scripts.Render`），在视图中引用绑定。 *\\共享\\\_Layout*文件的视图中的以下标记显示了默认 ASP.NET internet 项目视图如何引用 CSS 和 JavaScript 捆绑。

[!code-cshtml[Main](bundling-and-minification/samples/sample10.cshtml?highlight=5-6,11)]

请注意，Render 方法采用字符串数组，因此你可以在一个代码行中添加多个绑定。 通常需要使用呈现方法，这些方法可创建所需的 HTML 来引用资产。 您可以使用 `Url` 方法生成资产的 URL，而无需使用引用资产所需的标记。 假设你想要使用新的 HTML5 [async](http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async)属性。 下面的代码演示如何使用 `Url` 方法引用 modernizr。

[!code-cshtml[Main](bundling-and-minification/samples/sample11.cshtml?highlight=11)]

## <a name="using-the--wildcard-character-to-select-files"></a>使用 "\*" 通配符选择文件

在 `Include` 方法中指定的虚拟路径和 `IncludeDirectory` 方法中的搜索模式可以接受一个 "\*" 通配符，作为最后一个路径段中的前缀或后缀。 搜索字符串不区分大小写。 `IncludeDirectory` 方法提供搜索子目录的选项。

请考虑使用以下 JavaScript 文件的项目：

- *脚本\\Common\\AddAltToImg*
- *脚本\\Common\\ToggleDiv*
- *脚本\\Common\\ToggleImg*
- *脚本\\Common\\Sub1\\ToggleLinks*

![dir imag](bundling-and-minification/_static/image7.png)

下表显示了使用通配符添加到捆绑包的文件，如下所示：

| **Call** | **添加的文件或引发的异常** |
| --- | --- |
| Include （"~/Scripts/Common/\*.js"） | *AddAltToImg*、 *ToggleDiv*、 *ToggleImg* |
| Include （"~/Scripts/Common/T\*.js"） | 模式异常无效。 仅前缀或后缀允许使用通配符。 |
| Include （"~/Scripts/Common/\*og。\*"） | 模式异常无效。 只允许使用一个通配符。 |
| Include （"~/Scripts/Common/T\*"） | *ToggleDiv*， *ToggleImg* |
| Include （"~/Scripts/Common/\*"） | 模式异常无效。 纯通配符段无效。 |
| IncludeDirectory （"~/Scripts/Common"，"T\*"） | *ToggleDiv*， *ToggleImg* |
| IncludeDirectory （"~/Scripts/Common"，"T\*"，true） | *ToggleDiv*、 *ToggleImg*、 *ToggleLinks* |

通常，出于以下原因，将每个文件显式添加到捆绑包通常是首选的：

- 按通配符添加脚本默认为按字母顺序加载它们，这通常不是你想要的。 通常需要以特定（非字母）顺序添加 CSS 和 JavaScript 文件。 可以通过添加自定义[IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx)实现来缓解这一风险，但显式添加每个文件会更容易出错。 例如，你可能会在将来向文件夹中添加新资产，这可能需要你修改[IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx)实现。
- 使用通配符加载查看添加到目录中的特定文件可以包含在引用该捆绑包的所有视图中。 如果将特定于视图的脚本添加到捆绑包，则可能会在引用此绑定的其他视图上出现 JavaScript 错误。
- 导入其他文件的 CSS 文件会导致导入的文件加载两次。 例如，下面的代码创建一个绑定，其中大部分 jQuery UI 主题都加载了两次。 

    [!code-csharp[Main](bundling-and-minification/samples/sample12.cs)]

  通配符选择器 "\*" 会引入文件夹中的每个 CSS 文件，包括*内容\\主题\\基本\\jquery. 所有 .css*文件。 *Jquery. the .css*文件导入其他 css 文件。

## <a name="bundle-caching"></a>绑定缓存

绑定将 HTTP Expires 标头设置为从创建捆绑包起一年。 如果导航到以前查看过的页面，则 Fiddler 会显示 IE 不会发出针对捆绑包的条件请求，即，来自 IE 的绑定没有 HTTP GET 请求，并且没有来自服务器的 HTTP 304 响应。 可以强制 IE 使用 F5 键对每个绑定发出条件请求（导致每个绑定出现 HTTP 304 响应）。 您可以使用 ^ F5 强制执行完全刷新（这会导致每个绑定出现 HTTP 200 响应）。

下图显示了 "Fiddler 响应" 窗格的 "**缓存**" 选项卡：

![fiddler 缓存图像](bundling-and-minification/_static/image8.png)

请求   
`http://localhost/MvcBM_time/bundles/AllMyScripts?v=r0sLDicvP58AIXN_mc3QdyVvVj5euZNzdsa2N1PKvb81`  
 适用于捆绑**AllMyScripts** ，包含查询字符串对**v = R0sLDicvP58AIXN\\\_mc3QdyVvVj5euZNzdsa2N1PKvb81**。 查询字符串**v**具有一个值标记，它是用于缓存的唯一标识符。 只要捆绑包不会更改，ASP.NET 应用程序就会使用此令牌请求**AllMyScripts**捆绑。 如果捆绑中的任何文件发生更改，ASP.NET 优化框架将生成新的令牌，以确保对绑定的浏览器请求获得最新的捆绑。

如果运行 IE9 F12 开发人员工具并导航到以前加载的页面，则 IE 会错误地显示对每个绑定和返回 HTTP 304 的服务器发出的条件 GET 请求。 你可以阅读为什么 IE9 在使用 Cdn 的博客条目中进行条件请求时遇到问题[，并使其过期以提高网站性能](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)。

## <a name="less-coffeescript-scss-sass-bundling"></a>LESS、CoffeeScript、SCSS、Sass 绑定。

绑定和缩减框架提供了一种机制来处理中间语言（如[SCSS](http://sass-lang.com/)、 [Sass](http://sass-lang.com/)、 [LESS](http://www.dotlesscss.org/)或[Coffeescript](http://coffeescript.org/)），并将缩减等转换应用到生成的绑定。 例如，若要将[文件添加](http://www.dotlesscss.org/)到 MVC 4 项目，请执行以下操作：

1. 为较少的内容创建一个文件夹。 下面的示例使用*Content\\MyLess*文件夹。
2. 将[不太少](http://www.dotlesscss.org/)的 NuGet**包添加到你的项目**中。  
    ![NuGet 无点安装](bundling-and-minification/_static/image9.png)
3. 添加一个实现[IBundleTransform](https://msdn.microsoft.com/library/system.web.optimization.ibundletransform(VS.110).aspx)接口的类。 对于更少的转换，请将以下代码添加到你的项目中。

    [!code-csharp[Main](bundling-and-minification/samples/sample13.cs)]
4. 使用 `LessTransform` 和[CssMinify](https://msdn.microsoft.com/library/system.web.optimization.cssminify(VS.110).aspx)转换创建更少的文件包。 将以下代码添加到应用中的 `RegisterBundles` 方法 *\\_Start\\BundleConfig.cs*文件。

    [!code-csharp[Main](bundling-and-minification/samples/sample14.cs)]
5. 将以下代码添加到引用较少绑定的任何视图。

    [!code-cshtml[Main](bundling-and-minification/samples/sample15.cshtml)]

## <a name="bundle-considerations"></a>捆绑包注意事项

创建捆绑包时应遵循的一个好约定是在绑定名称中包含 "捆绑" 作为前缀。 这会阻止可能的[路由冲突](https://forums.asp.net/post/5012037.aspx)。

更新捆绑包中的一个文件后，系统将为捆绑包查询字符串参数生成一个新的令牌，并且在客户端下次请求包含该绑定的页面时，必须下载完全绑定。 在每个资产单独列出的传统标记中，只会下载已更改的文件。 经常更改的资产可能不适合进行捆绑。

绑定和缩减主要改善第一页请求加载时间。 请求网页后，浏览器会缓存资产（JavaScript、CSS 和图像），因此，在请求同一页面或同一站点上请求同一资产的页面时，绑定和缩减不会提供任何性能提升。 如果你没有正确地在资产上设置 expires 标头，并且不使用捆绑和缩减，则浏览器新鲜度试探法会在几天后将资产标记为过时，并且浏览器将需要对每个资产进行验证请求。 在这种情况下，绑定和缩减在第一次请求页面后会提高性能。 有关详细信息，请参阅[使用 cdn 的博客并过期以提高网站性能](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)。

对于每个主机名，可以通过使用[CDN](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)来减少六个同时连接的浏览器限制。 由于 CDN 的主机名将不同于托管站点的主机名，因此来自 CDN 的资产请求将不会计为托管环境的六个同时连接限制。 CDN 还可以提供常见的包缓存和边缘缓存优点。

捆绑包应按需要它们的页面进行分区。 例如，internet 应用程序的默认 ASP.NET MVC 模板会创建独立于 jQuery 的 jQuery 验证捆绑。 由于创建的默认视图不包含任何输入，也不会发布值，因此它们不包括验证捆绑。

`System.Web.Optimization` 命名空间是在*system.web*中实现的。 它利用 WebGrease 库（*WebGrease*） for 缩减功能，后者又使用*Antlr3*。

*我使用 Twitter 进行快速发布和共享链接。我的 Twitter 句柄为*： [@RickAndMSFT](http://twitter.com/RickAndMSFT)

## <a name="additional-resources"></a>其他资源

- 视频：通过[Howard Dierking](https://twitter.com/#!/howard_dierking)进行[捆绑和优化](https://channel9.msdn.com/Events/aspConf/aspConf/Bundling-and-Optimizing)
- [将 Web 优化添加到网页站点](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx)。
- [将绑定和缩减添加到 Web 窗体](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx)。
- [Henrik F Nielsen](http://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen) [@frystyk](https://twitter.com/frystyk) [的 Web 浏览的绑定和缩减的性能影响](https://blogs.msdn.com/b/henrikn/archive/2012/06/17/performance-implications-of-bundling-and-minification-on-http.aspx)
- [使用 cdn 并过期](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)，通过 Rick Anderson [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)提高网站性能
- [最小化 RTT （往返时间）](https://developers.google.com/speed/docs/best-practices/rtt)

## <a name="contributors"></a>参与者

- Hao Kung
- [Howard Dierking](https://twitter.com/#!/howard_dierking)
- Diana LaRose
