---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: 验证 ASP.NET 网页（Razor）站点中的用户输入 |Microsoft Docs
author: Rick-Anderson
description: 本文介绍如何验证从用户那里获取的信息 &mdash; 即，确保用户在中的 HTML 窗体中输入有效的信息。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454298"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a>验证 ASP.NET 网页（Razor）站点中的用户输入

作者： [Tom FitzMacken](https://github.com/tfitzmac)

> 本文介绍如何验证从用户那里获取的信息 &mdash; 即，确保用户在 ASP.NET 网页（Razor）站点中以 HTML 格式输入有效的信息。
> 
> 学习内容：
> 
> - 如何检查用户的输入是否与您定义的验证条件匹配。
> - 如何确定是否已通过所有验证测试。
> - 如何显示验证错误（以及如何设置它们的格式）。
> - 如何验证不直接来自用户的数据。
> 
> 下面是本文中引入的 ASP.NET 编程概念：
> 
> - `Validation` 帮助程序。
> - `Html.ValidationSummary` 和 `Html.ValidationMessage` 方法。
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>本教程中使用的软件版本
> 
> 
> - ASP.NET 网页（Razor）3
>   
> 
> 本教程还适用于 ASP.NET 网页2。

本文包含以下各节：

- [用户输入验证概述](#Overview_of_User_Input_Validation)
- [验证用户输入](#Validating_User_Input)
- [添加客户端验证](#Adding_Client-Side_Validation)
- [格式验证错误](#Formatting_Validation_Errors)
- [验证不直接来自用户的数据](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a>用户输入验证概述

如果要求用户在页面中输入信息（例如，转换为窗体），请务必确保输入的值有效。 例如，您不想处理丢失关键信息的窗体。

用户在 HTML 窗体中输入值时，它们输入的值是字符串。 在许多情况下，所需的值是一些其他数据类型，例如整数或日期。 因此，您还必须确保可以将用户输入的值正确地转换为相应的数据类型。

你可能还会对值有某些限制。 例如，即使用户正确输入整数，你可能也需要确保该值处于某个范围内。

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> **重要提示**验证用户输入对于安全性也很重要。 当您限制用户可在表单中输入的值时，您可以减少用户输入可能会危及您的网站安全的值的可能性。

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a>验证用户输入

在 ASP.NET 网页2中，你可以使用 `Validator` 帮助程序来测试用户输入。 基本方法是执行以下操作：

1. 确定要验证的输入元素（字段）。

    通常在窗体中 `<input>` 元素中验证值。 不过，最好是验证所有输入，甚至是来自受约束元素（例如 `<select>` 列表）的输入。 这有助于确保用户不会绕过页面上的控件并提交窗体。
2. 在页代码中，使用 `Validation` 帮助器的方法为每个输入元素添加单独的验证检查。

    若要检查必填字段，请使用 `Validation.RequireField(field, [error message])` （适用于单个字段）或 `Validation.RequireFields(field1, field2, ...))` （用于字段列表）。 对于其他类型的验证，请使用 `Validation.Add(field, ValidationType)`。 对于 `ValidationType`，可以使用以下选项：

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. 提交页面后，检查验证是否通过检查 `Validation.IsValid`传递：

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    如果存在任何验证错误，则会跳过正常页面处理。 例如，如果页面的目的是更新数据库，则在解决所有验证错误之前，您不会这样做。
4. 如果存在验证错误，请使用 `Html.ValidationSummary` 或 `Html.ValidationMessage`，或同时使用这两种方法在页的标记中显示错误消息。

下面的示例演示了一个说明这些步骤的页面。

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

若要查看验证的工作原理，请运行此页，并故意犯错误。 例如，如果您忘记输入课程名称，并且输入的日期无效，则下面是页面的外观：

![呈现的页中的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a>添加客户端验证

默认情况下，用户输入在用户提交页面后进行验证，即在服务器代码中执行验证。 这种方法的缺点是，用户在提交页面之前并不知道它们已发生错误。 如果窗体较长或复杂，则仅在提交页面后报告错误可能对用户不方便。

你可以添加支持，以在客户端脚本中执行验证。 在这种情况下，将在用户在浏览器中工作时执行验证。 例如，假设您指定一个值应为整数。 如果用户输入的值为非整数值，则只要用户离开输入字段，就会报告该错误。 用户会立即获得反馈，这对他们非常方便。 基于客户端的验证还可以减少用户提交窗体以更正多个错误的次数。

> [!NOTE]
> 即使使用客户端验证，也始终在服务器代码中执行验证。 在服务器代码中执行验证是一种安全措施，以防用户跳过基于客户端的验证。

1. 在页面中注册以下 JavaScript 库：  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   这两个库可从内容交付网络（CDN）中加载，因此你不必将它们安装在计算机或服务器上。 但是，必须具有 jquery 的本地副本。请*验证* 如果尚未使用包含库的 WebMatrix 模板（如**入门网站**），请创建基于**入门网站**的网页站点。 然后将 *.js*文件复制到当前站点。
2. 在标记中，为要验证的每个元素添加对 `Validation.For(field)`的调用。 此方法发出客户端验证使用的属性。 （而不是发出实际的 JavaScript 代码，该方法发出 `data-val-...`之类的属性。 这些属性支持使用 jQuery 执行工作的不引人注目的客户端验证。

以下页面显示了如何将客户端验证功能添加到前面所示的示例中。

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

并非所有验证检查都在客户端上运行。 特别是，数据类型验证（整数、日期等）不会在客户端上运行。 以下检查适用于客户端和服务器：

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

在此示例中，有效日期的测试在客户端代码中不起作用。 但是，将在服务器代码中执行测试。

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a>格式验证错误

您可以通过定义具有以下保留名称的 CSS 类来控制验证错误的显示方式：

- `field-validation-error`。 定义在显示错误时 `Html.ValidationMessage` 方法的输出。
- `field-validation-valid`。 如果没有错误，则定义 `Html.ValidationMessage` 方法的输出。
- `input-validation-error`。 定义在出现错误时如何呈现 `<input>` 元素。 （例如，如果其值无效，则可以使用此类将 &lt;input&gt; 元素的背景色设置为不同的颜色。此 CSS 类仅在客户端验证期间使用（在 ASP.NET 网页2）。
- `input-validation-valid`。 定义在没有错误时 `<input>` 元素的外观。
- `validation-summary-errors`。 定义 `Html.ValidationSummary` 方法的输出，它会显示错误列表。
- `validation-summary-valid`。 如果没有错误，则定义 `Html.ValidationSummary` 方法的输出。

以下 `<style>` 块显示了错误情况的规则。

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

如果在本文前面的示例页中包括此样式块，则错误显示将如下图所示：

![使用 CSS 样式类的验证错误](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> 如果在 ASP.NET 网页2中未使用客户端验证，则 `<input>` 元素（`input-validation-error` 和 `input-validation-valid` 的 CSS 类将不会产生任何影响。

### <a name="static-and-dynamic-error-display"></a>静态和动态错误显示

CSS 规则成对出现，如 `validation-summary-errors` 和 `validation-summary-valid`。 它们允许您为这两个条件定义规则：错误条件和 "正常" （非错误）条件。 必须了解的是，即使没有错误，也会始终呈现错误显示的标记。 例如，如果某页在标记中有 `Html.ValidationSummary` 方法，则即使第一次请求该页时，页源也将包含以下标记：

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

换句话说，`Html.ValidationSummary` 方法始终呈现 `<div>` 元素和列表，即使错误列表为空也是如此。 同样，`Html.ValidationMessage` 方法始终将 `<span>` 元素呈现为单个字段错误的占位符，即使没有错误也是如此。

在某些情况下，显示错误消息会导致页面重排，并会导致页面上的元素移动。 以 `-valid` 结尾的 CSS 规则使你能够定义可帮助防止此问题的布局。 例如，可以将 `field-validation-error` 和 `field-validation-valid` 定义为具有相同的固定大小。 这样一来，字段的显示区域是静态的，如果显示错误消息，则不会更改页面流。

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a>验证不直接来自用户的数据

有时，您必须验证不直接来自 HTML 格式的信息。 典型的示例是在查询字符串中传递值的页，如以下示例中所示：

`http://server/myapp/EditClassInformation?classid=1022`

在这种情况下，您需要确保传递到页面的值（此处为1022，`classid`的值）有效。 不能直接使用 `Validation` 帮助器来执行此验证。 但是，您可以使用验证系统的其他功能，例如显示验证错误消息的功能。

> [!NOTE] 
> 
> **重要提示**始终验证从*任何*源获取的值，包括窗体字段值、查询字符串值和 cookie 值。 用户可以轻松地更改这些值（可能出于恶意目的）。 因此，你必须检查这些值才能保护你的应用程序。

下面的示例演示如何验证在查询字符串中传递的值。 此代码测试该值是否不为空，以及该值是否为整数。

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

请注意，当请求不是窗体提交（`if(!IsPost)`）时，将执行该测试。 此测试将在第一次请求页面时通过，但不会在请求提交表单时通过。

若要显示此错误，可以通过调用 `Validation.AddFormError("message")`将错误添加到验证错误的列表中。 如果页面包含对 `Html.ValidationSummary` 方法的调用，则会在该处显示错误，就像用户输入验证错误一样。

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>其他资源

[在 ASP.NET 网页网站中使用 HTML 表单](https://go.microsoft.com/fwlink/?LinkID=202892)
