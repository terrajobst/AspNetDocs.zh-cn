---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: 使用 AJAX 交付动态更新 |Microsoft Docs
author: microsoft
description: 步骤10实现对已登录用户的支持：通过使用晚餐详细信息中集成的基于 Ajax 的方法对已登录的用户进行的兴趣
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486308"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>使用 AJAX 提供动态更新

由[Microsoft](https://github.com/microsoft)

[下载 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 这是免费的["NerdDinner" 应用程序教程](introducing-the-nerddinner-tutorial.md)的步骤10，该教程演示如何使用 ASP.NET MVC 1 构建小型但完整的 web 应用程序。
> 
> 步骤10使用 "晚餐详细信息" 页中集成的基于 Ajax 的方法，实现对已登录用户的支持，以使其对参加晚宴感兴趣。
> 
> 如果你使用的是 ASP.NET MVC 3，则建议你遵循[MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[Mvc 音乐应用商店](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教程中的入门。

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner 步骤10： AJAX 启用 RSVPs 接受

现在，让我们将对已登录用户的支持用于向你提供对参加晚宴的兴趣。 我们将使用 "晚餐详细信息" 页中集成的基于 AJAX 的方法启用此项。

### <a name="indicating-whether-the-user-is-rsvpd"></a>指示用户是否为 RSVP

用户可以访问 */Dinners/Details/[id*] URL 来查看有关特定晚餐的详细信息：

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

详细信息（）操作方法的实现如下所示：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

实现 RSVP 支持的第一步是将 "IsUserRegistered （用户名）" 帮助器方法添加到晚餐对象（在前面构建的 Dinner.cs 分部类中）。 此帮助器方法返回 true 或 false，具体取决于用户当前是否为晚宴，以获取晚餐：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

然后，可以将以下代码添加到详细信息 .aspx 视图模板，以显示相应的消息，指示用户是否已注册事件：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

现在，当用户访问晚餐时，他们将会看到以下消息：

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

当他们访问晚餐时，他们并未注册，会看到以下消息：

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>实现注册操作方法

现在，让我们添加使用户能够通过 "详细信息" 页获取晚餐的必要功能。

若要实现此方法，我们将创建一个新的 "RSVPController" 类，方法是右键单击 "\Controllers" 目录，然后选择 "&gt;控制器" 菜单命令。

我们会在新的 RSVPController 类内实现一个 "注册" 操作方法，该方法采用获取晚餐的 id 作为参数，检索相应的晚餐对象，检查登录用户当前是否处于已注册的用户列表，以及不为其添加 RSVP 对象：

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

请注意，我们如何将简单字符串返回为操作方法的输出。 我们可以将此消息嵌入到视图模板中，但由于它太小了，因此我们只需在控制器基类上使用 Content （） helper 方法，并返回如上所示的字符串消息。

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>使用 AJAX 调用 RSVPForEvent 操作方法

我们将使用 AJAX 从详细信息视图中调用注册操作方法。 实现此过程相当简单。 首先，我们将添加两个脚本库引用：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

第一个库引用核心 ASP.NET AJAX 客户端脚本库。 此文件的大小大约为24k，包含核心客户端 AJAX 功能。 第二个库包含与 ASP.NET MVC 的内置 AJAX 帮助器方法（稍后将用到）集成的实用工具函数。

接下来，我们可以更新前面添加的视图模板代码，使其不会输出 "未注册此事件" 消息，而是呈现一个链接，当推送时，该链接将在我们的 RSVP 控制器上执行调用我们的 RSVPForEvent 操作方法的 AJAX 调用并 RSVPs 用户：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

上面使用的 Ajax （） helper 方法内置于 ASP.NET MVC 中，它类似于 Html.actionlink （） helper 方法，不同之处在于，在单击链接时，它会向操作方法发出 AJAX 调用。 以上，我们将对 "RSVP" 控制器调用 "Register" 操作方法，并将 DinnerID 作为 "id" 参数传递给它。 要传递的最终 AjaxOptions 参数表示我们要获取从操作方法返回的内容，并更新 id 为 "rsvpmsg" 的页面上的 HTML &lt;div&gt; 元素。

现在，当用户浏览到未注册的晚餐时，他们将看到一个到 RSVP 的链接：

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

如果他们单击 "此事件的 RSVP" 链接，则他们将对 RSVP 控制器进行 AJAX 调用注册操作方法，并在完成后，会看到如下所示的更新消息：

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

进行此 AJAX 调用时所涉及的网络带宽和流量确实非常轻量。 当用户单击 "此事件的 RSVP" 链接时，将对 */Dinners/Register/1* URL 发出小型 HTTP POST 网络请求，如下所示：

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

来自注册操作方法的响应只是：

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

此轻型调用速度快，甚至在慢速网络上都可以工作。

### <a name="adding-a-jquery-animation"></a>添加 jQuery 动画

我们实现的 AJAX 功能非常有效和快速。 有时，这种情况很快，用户可能不会注意到 RSVP 链接已替换为新文本。 为了使结果稍微明显明了，我们可以添加一个简单的动画来强调更新消息。

默认的 ASP.NET MVC 项目模板包含 jQuery – Microsoft 也支持的极佳（和非常流行的）开源 JavaScript 库。 jQuery 提供了许多功能，包括良好的 HTML DOM 选择和效果库。

若要使用 jQuery，我们首先要向其添加脚本引用。 由于我们将在我们的站点中的各种地方使用 jQuery，因此我们将在我们的站点中添加脚本引用。主母版页文件，以便所有页面都可以使用它。

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*提示：请确保已安装用于 VS 2008 SP1 的 JavaScript intellisense 修补程序，以便为 JavaScript 文件（包括 jQuery）启用更丰富的 intellisense 支持。可以从以下内容下载： http://tinyurl.com/vs2008javascripthotfix*

使用 JQuery 编写的代码通常使用全局 "$ （）" JavaScript 方法，该方法可使用 CSS 选择器检索一个或多个 HTML 元素。 例如， *$ （"#rsvpmsg"）* 选择 id 为 rsvpmsg 的任何 HTML 元素，而 *$ （"."）* 将选择具有 "内容" CSS 类名称的所有元素。 你还可以使用选择器查询（如： *$ （"input [@type= 收音机] [@checked]"）* 编写更多高级查询，如 "返回所有选中的单选按钮"。

选择元素后，可以对其调用方法来执行操作，如隐藏它们： *$ （"#rsvpmsg"）。 hide （）;*

对于 RSVP 方案，我们将定义一个名为 "AnimateRSVPMessage" 的简单 JavaScript 函数，该函数选择 "rsvpmsg" &lt;div&gt; 并对其文本内容的大小进行动画处理。 下面的代码将小小小，并使其在400毫秒的时间范围内增加：

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

接下来，我们可以将此 JavaScript 函数连接到 AJAX 调用成功完成后调用，方法是将其名称传递给我们的 Html.actionlink （） helper 方法（通过 AjaxOptions "OnSuccess" 事件属性）：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

现在，如果单击了 "RSVP for the 此事件" 链接，并且我们的 AJAX 调用成功完成，则发送回的内容消息将以动画和增长为大：

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

除了提供 "OnSuccess" 事件之外，AjaxOptions 对象还公开可处理的 OnBegin、OnFailure 和 OnComplete 事件（以及各种其他属性和有用的选项）。

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>清除-重构 RSVP 分部视图

我们的详细信息视图模板即将开始，这会使您难以理解。 为了帮助提高代码的可读性，我们将创建一个分部视图– RSVPStatus，它封装了详细信息页的所有 RSVP 查看代码。

为此，我们可以右键单击 \Views\Dinners 文件夹，然后选择 "添加&gt;视图" 菜单命令。 我们将把晚餐对象作为其强类型 ViewModel。 接下来，我们可以将这些 RSVP 内容从 .aspx 视图复制/粘贴到其中。

完成此操作后，还可以创建另一个分部视图– EditAndDeleteLinks，它封装了编辑和删除链接视图代码。 此外，我们还会将晚餐对象作为其强类型 ViewModel，并将其详细信息 .aspx 视图中的编辑和删除逻辑复制/粘贴到其中。

然后，详细信息视图模板可以在底部包含两个 RenderPartial （）方法调用：

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

这会使代码更简洁读取和维护。

### <a name="next-step"></a>下一步

现在我们来看看如何更进一步地使用 AJAX，并向应用程序中添加交互式映射支持。

> [!div class="step-by-step"]
> [上一页](secure-applications-using-authentication-and-authorization.md)
> [下一页](use-ajax-to-implement-mapping-scenarios.md)
