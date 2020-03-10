---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API 中的模型验证-ASP.NET 4。x
author: MikeWasson
description: ASP.NET 4.x 的 ASP.NET Web API 中的模型验证概述。
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448928"
---
# <a name="model-validation-in-aspnet-web-api"></a>ASP.NET Web API 中的模型验证

作者： [Mike Wasson](https://github.com/MikeWasson)

本文介绍如何批注模型、使用批注进行数据验证以及处理 web API 中的验证错误。 当客户端将数据发送到 web API 时，通常需要在进行任何处理之前验证数据。 

## <a name="data-annotations"></a>数据注释

在 ASP.NET Web API 中，你可以使用[system.componentmodel. DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)命名空间中的属性为模型上的属性设置验证规则。 考虑下列模型：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

如果已在 ASP.NET MVC 中使用了模型验证，则会看到这种情况。 **必需**的属性指示 `Name` 属性不得为 null。 **Range**特性指示 `Weight` 必须介于0到999之间。

假设客户端发送 POST 请求，其 JSON 表示形式如下：

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

您可以看到，客户端不包括标记为必需的 `Name` 属性。 当 Web API 将 JSON 转换为 `Product` 实例时，它会对照验证特性来验证 `Product`。 在控制器操作中，可以检查模型是否有效：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

模型验证不保证客户端数据是安全的。 在应用程序的其他层中可能需要进行其他验证。 （例如，数据层可能强制外键约束。）[使用带有实体框架的 WEB API](../data/using-web-api-with-entity-framework/part-1.md)的教程探讨了其中一些问题。

**"** 正在进行中"：当客户端省略某些属性时，将发生正在进行的发布。 例如，假设客户端发送以下内容：

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

此时，客户端未指定 `Price` 或 `Weight`的值。 JSON 格式化程序将默认值0赋给缺少的属性。

![](model-validation-in-aspnet-web-api/_static/image1.png)

模型状态有效，因为零是这些属性的有效值。 这是否是一个问题取决于你的方案。 例如，在更新操作中，你可能希望区分 "零" 和 "未设置"。 若要强制客户端设置值，请将属性设置为可以为 null，并设置**所需**的属性：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

**"过度发布"** ：客户端还可以发送比预期*更多*的数据。 例如:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

此处的 JSON 包含 `Product` 模型中不存在的属性（"颜色"）。 在这种情况下，JSON 格式化程序只会忽略此值。 （XML 格式化程序执行相同的功能。）如果您的模型具有您打算为只读的属性，则过度发布会导致问题。 例如:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

您不希望用户更新 `IsAdmin` 属性，并将自己提升为管理员！ 最安全的策略是使用与客户端可以发送的内容完全匹配的模型类：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> Brad Wilson 的博客文章 "[输入验证与 ASP.NET MVC 中的模型验证" 相比](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)，有很好地讨论了下发和过账。 尽管 post 与 ASP.NET MVC 2 相关，但问题仍与 Web API 相关。

## <a name="handling-validation-errors"></a>处理验证错误

验证失败时，Web API 不会自动向客户端返回错误。 它由控制器操作来检查模型状态，并做出相应的响应。

你还可以创建一个操作筛选器，以在调用控制器操作之前检查模型状态。 以下代码展示一个示例：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

如果模型验证失败，此筛选器将返回包含验证错误的 HTTP 响应。 在这种情况下，不会调用控制器操作。

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

若要将此筛选器应用于所有 Web API 控制器，请在配置过程中将筛选器的实例添加到**HttpConfiguration**集合中：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

另一种方法是将筛选器设置为单个控制器或控制器操作上的属性：

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
