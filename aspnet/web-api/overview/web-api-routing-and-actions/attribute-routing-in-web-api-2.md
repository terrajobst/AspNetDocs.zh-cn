---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 中的属性路由 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446996"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 中的属性路由

作者： [Mike Wasson](https://github.com/MikeWasson)

*路由*是 Web API 与操作的 URI 匹配的方式。 Web API 2 支持一种新的路由类型，称为*属性路由*。 顾名思义，特性路由使用特性来定义路由。 特性路由使你可以更好地控制 web API 中的 Uri。 例如，你可以轻松地创建用于描述资源层次结构的 Uri。

仍完全支持早期的路由样式，称为基于约定的路由。 事实上，您可以将这两种技术组合到同一个项目中。

本主题演示如何启用属性路由，并介绍了用于属性路由的各种选项。 有关使用属性路由的端到端教程，请参阅使用[WEB API 2 中的属性路由创建 REST API](create-a-rest-api-with-attribute-routing.md)。

## <a name="prerequisites"></a>系统必备

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社区版、专业版或企业版

或者，使用 NuGet 包管理器来安装所需的包。 在 Visual Studio 的 "**工具**" 菜单中，选择 " **NuGet 包管理器**"，然后选择 "**程序包管理器控制台**"。 在 "包管理器控制台" 窗口中输入以下命令：

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>为什么选择属性？

Web API 使用的第一版*基于约定*的路由。 在该类型的路由中，可以定义一个或多个路由模板，它们基本上是参数化字符串。 当框架收到请求时，它会将 URI 与路由模板进行匹配。 （有关基于约定的路由的详细信息，请参阅[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。

基于约定的路由的优点之一是，在单个位置定义模板，并且在所有控制器上一致地应用路由规则。 遗憾的是，基于约定的路由使支持 RESTful Api 中常见的某些 URI 模式变得很困难。 例如，资源通常包含子资源：客户具有订单、电影具有参与者、书籍具有作者等。 创建反映这些关系的 Uri 很自然：

`/customers/1/orders`

使用基于约定的路由很难创建这种类型的 URI。 尽管可以完成此操作，但如果有多个控制器或资源类型，结果不会很好地进行缩放。

使用属性路由，为此 URI 定义路由很简单。 只需将属性添加到控制器操作即可：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

下面是一些其他模式，属性路由非常简单。

**API 版本控制**

在此示例中，"/api/v1/products" 将路由到与 "/api/v2/products" 不同的控制器。

`/api/v1/products`
`/api/v2/products`

**重载的 URI 段**

在此示例中，"1" 是订单号，但 "挂起" 映射到集合。

`/orders/1`
`/orders/pending`

**多个参数类型**

在此示例中，"1" 是订单号，而 "2013/06/16" 指定日期。

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>启用属性路由

若要启用属性路由，请在配置过程中调用**MapHttpAttributeRoutes** 。 此扩展方法在**HttpConfigurationExtensions**类中定义。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

属性路由可以与[基于约定](routing-in-aspnet-web-api.md)的路由结合。 若要定义基于约定的路由，请调用**MapHttpRoute**方法。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

有关配置 Web API 的详细信息，请参阅[配置 ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>注意：从 Web API 进行迁移

在 Web API 2 之前，Web API 项目模板生成的代码如下所示：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

如果启用了属性路由，则此代码将引发异常。 如果升级现有 Web API 项目以使用属性路由，请确保将此配置代码更新为以下内容：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> 有关详细信息，请参阅[配置包含 ASP.NET 托管的 WEB API](../advanced/configuring-aspnet-web-api.md#webhost)。

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>添加路由属性

下面是使用属性定义的路由示例：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

String &quot;customers/{customerId}/orders&quot; 是路由的 URI 模板。 Web API 尝试将请求 URI 与模板匹配。 在此示例中，"customers" 和 "orders" 是文本段，而 "{customerId}" 是变量参数。 以下 Uri 将与此模板匹配：

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

您可以使用[约束](#constraints)（本主题后面所述）限制匹配。

请注意，路由模板中的 &quot;{customerId}&quot; 参数与方法中的*customerId*参数的名称匹配。 当 Web API 调用控制器操作时，它会尝试绑定路由参数。 例如，如果 URI 是 `http://example.com/customers/1/orders`的，Web API 将尝试将值 "1" 绑定到操作中的*customerId*参数。

URI 模板可以有多个参数：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

没有路由属性的任何控制器方法都使用基于约定的路由。 这样，便可以在同一个项目中组合这两种类型的路由。

## <a name="http-methods"></a>HTTP 方法

Web API 还会根据请求的 HTTP 方法（GET、POST 等）来选择操作。 默认情况下，Web API 将查找与控制器方法名称开头的不区分大小写的匹配项。 例如，名为 `PutCustomers` 的控制器方法匹配 HTTP PUT 请求。

可以通过使用以下任何属性修饰方法来重写此约定：

- **HttpDelete**
- **[HttpGet]**
- **[HttpHead]**
- **HttpOptions**
- **[HttpPatch]**
- **HttpPost**
- **HttpPut**

下面的示例将 CreateBook 方法映射到 HTTP POST 请求。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

对于所有其他 HTTP 方法（包括非标准方法），请使用**AcceptVerbs**属性，该属性采用 HTTP 方法的列表。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>路由前缀

通常，控制器中的路由都以相同的前缀开头。 例如:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

可以使用 **[RoutePrefix]** 属性为整个控制器设置公共前缀：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

在方法特性上使用波形符（~）来重写路由前缀：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

路由前缀可以包含参数：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>路由约束

路由约束允许您限制路由模板中的参数的匹配方式。 一般语法为 &quot;{parameter： constraint}&quot;。 例如:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

此处，如果 URI &quot;id&quot; 段是一个整数，则仅选择第一个路由。 否则，将选择第二个路由。

下表列出了支持的约束。

| 约束 | 说明 | 示例 |
| --- | --- | --- |
| alpha | 匹配大写或小写拉丁字母字符（a-z、a-z） | {x:alpha} |
| bool | 与布尔值匹配。 | {x:bool} |
| datetime | 与**DateTime**值匹配。 | {x:datetime} |
| decimal | 匹配十进制值。 | {x:decimal} |
| double | 匹配64位浮点值。 | x：double |
| 浮点数 | 匹配32位浮点值。 | {x:float} |
| guid | 匹配 GUID 值。 | {x:guid} |
| int | 匹配32位整数值。 | {x:int} |
| length | 与指定长度或指定长度范围内的字符串匹配。 | {x:length （6）}{x:length （1，20）} |
| long | 匹配64位整数值。 | {x:long} |
| max | 匹配整数和最大值。 | {x:max(10)} |
| 长度 | 匹配最大长度的字符串。 | {x:maxlength （10）} |
| min | 匹配整数和最小值。 | {x:min （10）} |
| minlength | 匹配最小长度的字符串。 | {x:minlength （10）} |
| range | 匹配某个值范围内的一个整数。 | {x:range （10，50）} |
| 正则表达式 | 匹配正则表达式。 | {x:regex （^ \d{3}-\d{3}-\d{4}$）} |

请注意，某些约束（如 &quot;min&quot;）采用括号中的参数。 可以将多个约束应用于参数，并以冒号分隔。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>自定义路由约束

可以通过实现**IHttpRouteConstraint**接口创建自定义路由约束。 例如，下面的约束将参数限制为一个非零的整数值。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

下面的代码演示如何注册约束：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

现在，你可以在路由中应用约束：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

还可以通过实现**IInlineConstraintResolver**接口来替换整个**DefaultInlineConstraintResolver**类。 这样做将替换所有内置约束，除非**IInlineConstraintResolver**的实现专门添加它们。

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>可选 URI 参数和默认值

可以通过向 route 参数添加问号来使 URI 参数成为可选的。 如果路由参数是可选的，则必须为 method 参数定义默认值。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

在此示例中，`/api/books/locale/1033` 和 `/api/books/locale` 返回相同资源。

另外，还可以在路由模板中指定默认值，如下所示：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

这与前面的示例几乎相同，但在应用默认值时，行为存在细微的差异。

- 在第一个示例（"{lcid： int？}"）中，默认值1033将直接分配给 method 参数，因此参数将具有此精确值。
- 在第二个示例（"{lcid： int = 1033}"）中，默认值 "1033" 通过模型绑定过程。 默认的模型联编程序会将 "1033" 转换为数值1033。 但是，可以插入自定义模型绑定器，这可能会执行其他操作。

（在大多数情况下，除非管道中有自定义模型联编程序，否则两个窗体将是等效的。）

<a id="route-names"></a>
## <a name="route-names"></a>路由名称

在 Web API 中，每个路由都有一个名称。 路由名称用于生成链接，以便可以在 HTTP 响应中包含链接。

若要指定路由名称，请设置属性的**name**属性。 下面的示例演示如何设置路由名称，以及如何在生成链接时使用路由名称。

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>路由顺序

当框架尝试将 URI 与某个路由匹配时，它将按特定顺序计算路由。 若要指定顺序，请设置路由属性的**order**属性。 首先计算较小的值。 默认顺序值为零。

下面介绍如何确定总计排序：

1. 比较路由属性的**Order**属性。
2. 查看路由模板中的每个 URI 段。 对于每个段，按以下顺序排序：

    1. 文本段。
    2. 具有约束的路由参数。
    3. 不带约束的路由参数。
    4. 带有约束的通配符参数段。
    5. 没有约束的通配符参数段。
3. 对于并列，路由按路由模板的不区分大小写的序号字符串比较（[stringcomparison.ordinalignorecase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)）进行排序。

这是一个示例。 假设您定义了以下控制器：

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

这些路由顺序如下所示。

1. 订单/详细信息
2. orders/{id}
3. orders/{customerName}
4. 订单/{\*日期}
5. 订单/挂起

请注意，"详细信息" 是文本段，出现在 "{id}" 之前，但 "挂起" 显示在最后，因为**Order**属性为1。 （此示例假定不存在名为 "详细信息" 或 "挂起" 的客户。 一般情况下，请尽量避免出现不明确的路由。 在此示例中，`GetByCustomer` 的更好的路由模板为 "customers/{customerName}"）
