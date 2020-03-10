---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: '迭代 #7 –添加 Ajax 功能（VB） |Microsoft Docs'
author: microsoft
description: 在第七次迭代中，我们通过添加对 Ajax 的支持来提高应用程序的响应能力和性能。
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: cee2b6e7c7517a1e03ae26d5233fc438857a030c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486998"
---
# <a name="iteration-7--add-ajax-functionality-vb"></a>迭代 #7 –添加 Ajax 功能（VB）

由[Microsoft](https://github.com/microsoft)

[下载代码](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> 在第七次迭代中，我们通过添加对 Ajax 的支持来提高应用程序的响应能力和性能。

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>构建联系人管理 ASP.NET MVC 应用程序（VB）

在本系列教程中，我们从一开始就生成一个完整的联系人管理应用程序。 联系人管理器应用程序允许您存储联系人信息名称、电话号码和电子邮件地址，以获取人员列表。

我们通过多个迭代生成应用程序。 随着每次迭代，我们将逐步改进应用程序。 此多个迭代方法的目标是使您能够了解每个更改的原因。

- 迭代 #1-创建应用程序。 在第一次迭代中，我们以尽可能简单的方式创建联系人管理器。 添加对基本数据库操作的支持：创建、读取、更新和删除（CRUD）。

- 迭代 #2-使应用程序看起来不错。 在此迭代中，我们通过修改默认的 ASP.NET MVC 视图母版页和级联样式表来改善应用程序的外观。

- 迭代 #3-添加窗体验证。 在第三次迭代中，我们将添加基本的窗体验证。 我们阻止用户提交窗体，而无需填写所需的窗体字段。 我们还验证了电子邮件地址和电话号码。

- 迭代 #4-使应用程序松散耦合。 在第四次迭代中，我们将利用多种软件设计模式来更轻松地维护和修改联系人管理器应用程序。 例如，我们重构应用程序以使用存储库模式和依赖关系注入模式。

- 迭代 #5-创建单元测试。 在第五次迭代中，通过添加单元测试使应用程序更易于维护和修改。 我们模拟数据模型类，并为控制器和验证逻辑生成单元测试。

- 迭代 #6-使用测试驱动开发。 在第六次迭代中，我们通过首先编写单元测试并针对单元测试编写代码，向应用程序添加新功能。 在此迭代中，我们添加联系人组。

- 迭代 #7-添加 Ajax 功能。 在第七次迭代中，我们通过添加对 Ajax 的支持来提高应用程序的响应能力和性能。

## <a name="this-iteration"></a>此迭代

在此 "联系人管理器" 应用程序的迭代中，我们重构应用程序以利用 Ajax。 利用 Ajax，我们使应用程序更具响应性。 当只需更新页面中的某个区域时，我们可以避免呈现整个页面。

我们将重构索引视图，以便每当有人选择新的联系人组时，都不需要重新显示整个页面。 相反，当有人单击联系人组时，我们将只更新联系人列表，并使页面的其余部分保持不变。

我们还将更改 "删除" 链接的工作方式。 我们会显示 JavaScript 确认对话框，而不是显示单独的确认页面。 如果确认要删除某一联系人，则将对该服务器执行 HTTP 删除操作，以便从数据库中删除该联系人记录。

此外，我们将利用 jQuery 将动画效果添加到索引视图。 当从服务器中提取新的联系人列表时，我们将显示一个动画。

最后，我们将利用 ASP.NET AJAX framework 对管理浏览器历史记录的支持。 我们将在执行 Ajax 调用以更新联系人列表时创建历史记录点。 这样，浏览器向后和向前的按钮都将起作用。

## <a name="why-use-ajax"></a>为什么使用 Ajax？

使用 Ajax 有很多好处。 首先，将 Ajax 功能添加到应用程序会导致更好的用户体验。 在普通 web 应用程序中，每次用户执行某个操作时，都必须将整个页面回发到服务器。 每次执行操作时，浏览器就会锁定，用户必须等待，直到提取并重新显示整个页面。

对于桌面应用程序，这是一个不可接受的体验。 但在传统上，在 web 应用程序中，我们会遇到这种不太好的用户体验，因为我们不知道我们能做得更好。 在实际情况下，我们认为它是 web 应用程序的一项限制，这只是我们的想象力限制。

在 Ajax 应用程序中，无需使用户体验只需停止即可更新页面。 相反，你可以在后台执行异步请求来更新页面。 不强制用户在部分页面更新时等待。

利用 Ajax，还可以提高应用程序的性能。 现在，请考虑在没有 Ajax 功能的情况下联系人管理器应用程序的工作方式。 单击联系人组时，必须重新显示整个索引视图。 必须从数据库服务器中检索联系人列表和联系人组列表。 所有这些数据必须通过网络从 web 服务器传递到 web 浏览器。

但是，在我们的应用程序中添加 Ajax 功能后，我们可以避免在用户单击联系人组时重新出现整个页面。 我们不再需要从数据库中获取联系人组。 我们也不需要跨线推送整个索引视图。 利用 Ajax，减少了数据库服务器必须执行的工作量，减少了应用程序所需的网络流量。

## <a name="don-t-be-afraid-of-ajax"></a>别害怕 Ajax

有些开发人员担心使用 Ajax，因为他们担心下层浏览器。 他们希望确保其 web 应用程序在被不支持 JavaScript 的浏览器访问时仍可正常工作。 由于 Ajax 依赖于 JavaScript，因此某些开发人员应避免使用 Ajax。

但是，如果您对如何实现 Ajax 特别小心，则可以生成适用于上级和下层浏览器的应用程序。 我们的联系人管理器应用程序将适用于支持 JavaScript 的浏览器和不支持的浏览器。

如果你将联系人管理器应用程序与支持 JavaScript 的浏览器结合使用，则你将获得更好的用户体验。 例如，单击联系人组时，只会更新显示联系人的页面区域。

另一方面，如果你将联系人管理器应用程序与不支持 JavaScript 的浏览器（或禁用了 JavaScript 的浏览器）结合使用，则你的用户体验将略有降低。 例如，单击联系人组时，必须将整个索引视图回发到浏览器，以显示联系人的匹配列表。

## <a name="adding-the-required-javascript-files"></a>添加所需的 JavaScript 文件

我们需要使用三个 JavaScript 文件将 Ajax 功能添加到我们的应用程序。 这三个文件都包含在新的 ASP.NET MVC 应用程序的 Scripts 文件夹中。

如果打算在应用程序的多个页面中使用 Ajax，则在应用程序的 "查看" 母版页中包含所需的 JavaScript 文件是有意义的。 这样一来，JavaScript 文件将自动包含在应用程序的所有页面中。

在视图母版页的 &lt;head&gt; 标记内添加以下 JavaScript 包含：

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>重构索引视图以使用 Ajax

首先，让我们修改索引视图，以便单击联系人组仅更新显示 "联系人" 的视图区域。 图1中的红色框包含要更新的区域。

[![仅更新联系人](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**图 01**：仅更新联系人（[单击查看完全大小的图像](iteration-7-add-ajax-functionality-vb/_static/image2.png)）

第一步是将要异步更新的视图部分分为单独的部分（查看用户控件）。 用于显示联系人表的 "索引" 视图部分已移入列表1的部分中。

**列表 1-Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

请注意，列表1中的部分具有与索引视图不同的模型。 &lt;% @ Page%&gt; 指令中的*inherits*属性指定部分继承自 ViewUserControl&lt;组&gt; 类。

已更新的索引视图包含在列表2中。

**列表 2-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

对于列表2中的更新视图，应注意两个问题。 首先，请注意，移动到部分中的所有内容都将替换为对 RenderPartial （）的调用。 当首次请求索引视图以便显示初始联系人集时，将调用 RenderPartial （）方法。

其次，请注意，用于显示联系人组的 .Html （）已替换为 Html.actionlink （）。 通过以下参数调用了 Ajax （）：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

第一个参数表示要为链接显示的文本，第二个参数表示路由值，第三个参数表示 Ajax 选项。 在这种情况下，我们将使用 UpdateTargetId Ajax 选项来指向在 Ajax 请求完成后要更新的 HTML &lt;div&gt; 标记。 我们想要用联系人的新列表更新 &lt;div&gt; 标记。

联系人控制器的更新索引（）方法包含在列表3中。

**列表 Controllers\ContactController.vb （Index 方法）**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

已更新的 Index （）操作有条件地返回两个项中的一个。 如果 Index （）操作由 Ajax 请求调用，则控制器返回部分。 否则，Index （）操作返回整个视图。

请注意，Index （）操作不需要在由 Ajax 请求调用时返回多少数据。 在正常请求的上下文中，索引操作返回所有联系人组和所选联系人组的列表。 在 Ajax 请求的上下文中，Index （）操作仅返回所选组。 Ajax 意味着在数据库服务器上工作量更少。

对于上级和下层浏览器，修改后的索引视图都适用。 如果单击某一联系人组，而您的浏览器支持 JavaScript，则仅更新该视图中包含联系人列表的区域。 另一方面，如果你的浏览器不支持 JavaScript，则会更新整个视图。

更新的索引视图有一个问题。 单击联系人组时，不会突出显示所选组。 由于组列表显示在 Ajax 请求期间更新的区域之外，因此不会突出显示适当的组。 我们将在下一节中解决此问题。

## <a name="adding-jquery-animation-effects"></a>添加 jQuery 动画效果

通常，单击网页中的链接时，可以使用浏览器进度栏来检测浏览器是否正在主动提取更新的内容。 另一方面，如果执行 Ajax 请求，浏览器进度栏不会显示任何进度。 这会使用户紧张。 如何确定浏览器是否已冻结？

可以通过多种方式向用户指示在执行 Ajax 请求时正在执行的工作。 一种方法是显示简单动画。 例如，你可以在 Ajax 请求开始时淡出区域，并在请求完成时在区域中淡化。

我们将使用 Microsoft ASP.NET MVC 框架附带的 jQuery library 来创建动画效果。 已更新的索引视图包含在列表4中。

**列表 4-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

请注意，更新的索引视图包含三个新的 JavaScript 函数。 在单击新的联系人组时，前两个函数使用 jQuery 来淡出并在联系人列表中淡化。 当 Ajax 请求导致错误（例如网络超时）时，第三个函数将显示错误消息。

第一个函数还负责突出显示所选组。 类 = 所选特性将添加到所单击元素的父元素（LI 元素）中。 同样，jQuery 使你可以轻松地选择正确的元素并添加 CSS 类。

这些脚本与带有 Ajax （） AjaxOptions 参数的帮助的组链接相关联。 更新的 Ajax （）方法调用如下所示：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>添加浏览器历史记录支持

通常，当您单击某个链接以更新页面时，您的浏览器历史记录将会更新。 这样，就可以单击浏览器的 "后退" 按钮，将时间向后移动到页面之前的状态。 例如，如果单击 "朋友联系人" 组，然后单击 "业务联系人" 组，则可以单击浏览器的 "后退" 按钮，在选择 "朋友联系人" 组时，导航回页面的状态。

遗憾的是，执行 Ajax 请求并不会自动更新浏览器历史记录。 如果单击联系人组，并使用 Ajax 请求检索匹配联系人列表，则不会更新浏览器历史记录。 选择新的联系人组后，不能使用浏览器的 "后退" 按钮导航回联系人组。

如果希望用户在执行 Ajax 请求后能够使用浏览器的 "后退" 按钮，则需要执行一些其他操作。 需要利用 ASP.NET AJAX Framework 中内置的浏览器历史记录管理功能。

ASP.NET AJAX browser history，你需要执行以下三项操作：

1. 通过将 enableBrowserHistory 属性设置为 true 来启用浏览器历史记录。
2. 当视图状态通过调用 addHistoryPoint （）方法更改时，保存历史记录点。
3. 在引发导航事件时重新构造视图状态。

已更新的索引视图包含在列表5中。

**列表 5-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

在列表5中，在 pageInit （）函数中启用了浏览器历史记录。 PageInit （）函数还用于设置导航事件的事件处理程序。 每当浏览器的 "前进" 或 "后退" 按钮使页面的状态发生更改时，就会引发导航事件。

单击联系人组时，将调用 beginContactList （）方法。 此方法通过调用 addHistoryPoint （）方法创建一个新的历史记录点。 单击的联系人组的 id 将添加到历史记录中。

组 id 是从联系人组链接上的 expando 属性检索的。 通过以下对 Html.actionlink （）的调用来呈现链接。

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

传递到 node.js （）的最后一个参数向链接添加一个名为 groupid 的 expando 特性（对于 XHTML 兼容性，小写）。

当用户点击浏览器的 "后退" 或 "前进" 按钮时，将引发导航事件并调用导航（）方法。 此方法更新页面中显示的联系人，使其与与传递到导航方法的浏览器历史记录点相对应的页面的状态相匹配。

## <a name="performing-ajax-deletes"></a>执行 Ajax 删除

目前，若要删除联系人，需要单击 "删除" 链接，然后单击 "删除确认" 页面中显示的 "删除" 按钮（参见图2）。 这看起来像是执行一些简单的操作，例如删除数据库记录。

[!["删除确认" 页面](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**图 02**： "删除确认" 页面（[单击以查看完全大小的图像](iteration-7-add-ajax-functionality-vb/_static/image4.png)）

可以跳过 "删除确认" 页面并直接从 "索引" 视图中删除联系人。 由于采用此方法会使应用程序打开安全漏洞，因此应避免此诱惑。 通常，在调用修改 web 应用程序状态的操作时，不需要执行 HTTP GET 操作。 执行删除操作时，需要执行 http POST 或更好的 HTTP 删除操作。

删除链接包含在 ContactList 部分中。 清单6中包含 ContactList 部分的更新版本。

**列表 6-Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

通过以下对 ImageActionLink （）方法的调用来呈现删除链接：

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> ImageActionLink （）不是 ASP.NET MVC 框架的标准部分。 ImageActionLink （）是联系人管理器项目中包含的自定义帮助器方法。

AjaxOptions 参数具有两个属性。 首先，Confirm 属性用于显示 popup JavaScript 确认对话框。 其次，HttpMethod 属性用于执行 HTTP 删除操作。

列表7包含已添加到联系人控制器的新 AjaxDelete （）操作。

**列表 7-Controllers\ContactController.vb （AjaxDelete）**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

AjaxDelete （）操作使用 AcceptVerbs 特性修饰。 此属性可防止除 HTTP 删除操作以外的任何 HTTP 操作都调用操作。 具体而言，无法使用 HTTP GET 调用此操作。

删除数据库记录后，需要显示已更新的不包含已删除记录的联系人列表。 AjaxDelete （）方法返回 ContactList 部分和更新后的联系人列表。

## <a name="summary"></a>摘要

在此迭代中，我们将 Ajax 功能添加到了我们的联系人管理器应用程序。 我们使用 Ajax 来改善应用程序的响应能力和性能。

首先，我们重构了索引视图，以便单击联系人组不会更新整个视图。 相反，单击联系人组只会更新联系人列表。

接下来，我们使用 jQuery 动画效果淡出，并在联系人列表中淡化。 向 Ajax 应用程序添加动画可用于向应用程序的用户提供与浏览器进度栏等效的操作。

我们还向 Ajax 应用程序添加了浏览器历史记录支持。 我们使用户能够单击浏览器的 "后退" 和 "前进" 按钮来更改索引视图的状态。

最后，我们创建了一个支持 HTTP 删除操作的 "删除" 链接。 通过执行 Ajax delete，用户可以删除数据库记录，而无需用户请求额外的 "删除" 确认页面。

> [!div class="step-by-step"]
> [上一页](iteration-6-use-test-driven-development-vb.md)
