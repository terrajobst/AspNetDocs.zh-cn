---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: JSON 和 XML 序列化在 ASP.NET Web API-ASP.NET 4.x
author: MikeWasson
description: 介绍 ASP.NET Web API 中的 JSON 和 XML 格式化程序的 ASP.NET 4.x。
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: a9e7ed63a55c146976e0221214e722f3a2292fee
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59408272"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a><span data-ttu-id="2e4a9-103">JSON 和 ASP.NET Web API 中的 XML 序列化</span><span class="sxs-lookup"><span data-stu-id="2e4a9-103">JSON and XML Serialization in ASP.NET Web API</span></span>

<span data-ttu-id="2e4a9-104">通过[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2e4a9-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2e4a9-105">本指南介绍了 ASP.NET Web API 中的 JSON 和 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-105">This article describes the JSON and XML formatters in ASP.NET Web API.</span></span>

<span data-ttu-id="2e4a9-106">在 ASP.NET Web API 中，*媒体类型格式化程序*是一个对象，可以：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-106">In ASP.NET Web API, a *media-type formatter* is an object that can:</span></span>

- <span data-ttu-id="2e4a9-107">读取 CLR 对象从 HTTP 消息正文</span><span class="sxs-lookup"><span data-stu-id="2e4a9-107">Read CLR objects from an HTTP message body</span></span>
- <span data-ttu-id="2e4a9-108">将 CLR 对象写入到 HTTP 消息正文</span><span class="sxs-lookup"><span data-stu-id="2e4a9-108">Write CLR objects into an HTTP message body</span></span>

<span data-ttu-id="2e4a9-109">Web API 提供了对 JSON 和 XML 的媒体类型格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-109">Web API provides media-type formatters for both JSON and XML.</span></span> <span data-ttu-id="2e4a9-110">默认情况下，框架将这些格式化程序插入到管道。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-110">The framework inserts these formatters into the pipeline by default.</span></span> <span data-ttu-id="2e4a9-111">客户端可以请求的 HTTP 请求的 Accept 标头中的 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-111">Clients can request either JSON or XML in the Accept header of the HTTP request.</span></span>

## <a name="contents"></a><span data-ttu-id="2e4a9-112">内容</span><span class="sxs-lookup"><span data-stu-id="2e4a9-112">Contents</span></span>

- [<span data-ttu-id="2e4a9-113">JSON 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="2e4a9-113">JSON Media-Type Formatter</span></span>](#json_media_type_formatter)

    - [<span data-ttu-id="2e4a9-114">只读属性</span><span class="sxs-lookup"><span data-stu-id="2e4a9-114">Read-Only Properties</span></span>](#json_readonly)
    - [<span data-ttu-id="2e4a9-115">日期</span><span class="sxs-lookup"><span data-stu-id="2e4a9-115">Dates</span></span>](#json_dates)
    - [<span data-ttu-id="2e4a9-116">缩进</span><span class="sxs-lookup"><span data-stu-id="2e4a9-116">Indenting</span></span>](#json_indenting)
    - [<span data-ttu-id="2e4a9-117">驼峰式大小写</span><span class="sxs-lookup"><span data-stu-id="2e4a9-117">Camel Casing</span></span>](#json_camelcasing)
    - [<span data-ttu-id="2e4a9-118">匿名和弱类型化对象</span><span class="sxs-lookup"><span data-stu-id="2e4a9-118">Anonymous and Weakly-Typed Objects</span></span>](#json_anon)
- [<span data-ttu-id="2e4a9-119">XML 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="2e4a9-119">XML Media-Type Formatter</span></span>](#xml_media_type_formatter)

    - [<span data-ttu-id="2e4a9-120">只读属性</span><span class="sxs-lookup"><span data-stu-id="2e4a9-120">Read-Only Properties</span></span>](#xml_readonly)
    - [<span data-ttu-id="2e4a9-121">日期</span><span class="sxs-lookup"><span data-stu-id="2e4a9-121">Dates</span></span>](#xml_dates)
    - [<span data-ttu-id="2e4a9-122">缩进</span><span class="sxs-lookup"><span data-stu-id="2e4a9-122">Indenting</span></span>](#xml_indenting)
    - [<span data-ttu-id="2e4a9-123">设置每种类型的 XML 序列化程序</span><span class="sxs-lookup"><span data-stu-id="2e4a9-123">Setting Per-Type XML Serializers</span></span>](#xml_pertype)
- [<span data-ttu-id="2e4a9-124">删除 JSON 或 XML 格式化程序</span><span class="sxs-lookup"><span data-stu-id="2e4a9-124">Removing the JSON or XML Formatter</span></span>](#removing_the_json_or_xml_formatter)
- [<span data-ttu-id="2e4a9-125">处理循环对象引用</span><span class="sxs-lookup"><span data-stu-id="2e4a9-125">Handling Circular Object References</span></span>](#handling_circular_object_references)
- [<span data-ttu-id="2e4a9-126">测试对象序列化</span><span class="sxs-lookup"><span data-stu-id="2e4a9-126">Testing Object Serialization</span></span>](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a><span data-ttu-id="2e4a9-127">JSON 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="2e4a9-127">JSON Media-Type Formatter</span></span>

<span data-ttu-id="2e4a9-128">JSON 格式设置将由**JsonMediaTypeFormatter**类。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-128">JSON formatting is provided by the **JsonMediaTypeFormatter** class.</span></span> <span data-ttu-id="2e4a9-129">默认情况下**JsonMediaTypeFormatter**使用[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)库以执行序列化。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-129">By default, **JsonMediaTypeFormatter** uses the [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) library to perform serialization.</span></span> <span data-ttu-id="2e4a9-130">Json.NET 是第三方开放源代码项目。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-130">Json.NET is a third-party open source project.</span></span>

<span data-ttu-id="2e4a9-131">如果您愿意，可以配置**JsonMediaTypeFormatter**类，以使用**DataContractJsonSerializer**而不是 Json.NET。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-131">If you prefer, you can configure the **JsonMediaTypeFormatter** class to use the **DataContractJsonSerializer** instead of Json.NET.</span></span> <span data-ttu-id="2e4a9-132">若要执行此操作，设置**UseDataContractJsonSerializer**属性设置为**true**:</span><span class="sxs-lookup"><span data-stu-id="2e4a9-132">To do so, set the **UseDataContractJsonSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a><span data-ttu-id="2e4a9-133">JSON 序列化</span><span class="sxs-lookup"><span data-stu-id="2e4a9-133">JSON Serialization</span></span>

<span data-ttu-id="2e4a9-134">本部分介绍 JSON 格式化程序，使用默认的一些特定行为[Json.NET](https://github.com/JamesNK/Newtonsoft.Json)序列化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-134">This section describes some specific behaviors of the JSON formatter, using the default [Json.NET](https://github.com/JamesNK/Newtonsoft.Json) serializer.</span></span> <span data-ttu-id="2e4a9-135">这并不意味着要综合文档的 Json.NET 库;有关详细信息，请参阅[Json.NET 文档](http://james.newtonking.com/projects/json/help/)。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-135">This is not meant to be comprehensive documentation of the Json.NET library; for more information, see the [Json.NET Documentation](http://james.newtonking.com/projects/json/help/).</span></span>

#### <a name="what-gets-serialized"></a><span data-ttu-id="2e4a9-136">什么获取序列化？</span><span class="sxs-lookup"><span data-stu-id="2e4a9-136">What Gets Serialized?</span></span>

<span data-ttu-id="2e4a9-137">默认情况下，所有公共属性和字段会参与序列化的 JSON。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-137">By default, all public properties and fields are included in the serialized JSON.</span></span> <span data-ttu-id="2e4a9-138">若要忽略的属性或字段，给它装饰**JsonIgnore**属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-138">To omit a property or field, decorate it with the **JsonIgnore** attribute.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

<span data-ttu-id="2e4a9-139">如果您愿意&quot;参加&quot;方法，请修饰类与**DataContract**属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-139">If you prefer an &quot;opt-in&quot; approach, decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="2e4a9-140">如果存在此属性，则将忽略成员，除非它们具有**DataMember**。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-140">If this attribute is present, members are ignored unless they have the **DataMember**.</span></span> <span data-ttu-id="2e4a9-141">此外可以使用**DataMember**要序列化私有成员。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-141">You can also use **DataMember** to serialize private members.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="2e4a9-142">只读属性</span><span class="sxs-lookup"><span data-stu-id="2e4a9-142">Read-Only Properties</span></span>

<span data-ttu-id="2e4a9-143">默认情况下序列化只读属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-143">Read-only properties are serialized by default.</span></span>

<a id="json_dates"></a>
### <a name="dates"></a><span data-ttu-id="2e4a9-144">日期</span><span class="sxs-lookup"><span data-stu-id="2e4a9-144">Dates</span></span>

<span data-ttu-id="2e4a9-145">默认情况下，通过 Json.NET 可以将日期[ISO 8601](http://www.w3.org/TR/NOTE-datetime)格式。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-145">By default, Json.NET writes dates in [ISO 8601](http://www.w3.org/TR/NOTE-datetime) format.</span></span> <span data-ttu-id="2e4a9-146">使用"Z"后缀编写日期以 UTC （协调世界时）。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-146">Dates in UTC (Coordinated Universal Time) are written with a "Z" suffix.</span></span> <span data-ttu-id="2e4a9-147">以本地时间日期包含时区偏移量。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-147">Dates in local time include a time-zone offset.</span></span> <span data-ttu-id="2e4a9-148">例如：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-148">For example:</span></span>

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

<span data-ttu-id="2e4a9-149">默认情况下，Json.NET 保留时区。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-149">By default, Json.NET preserves the time zone.</span></span> <span data-ttu-id="2e4a9-150">您可以通过设置 DateTimeZoneHandling 属性覆盖此：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-150">You can override this by setting the DateTimeZoneHandling property:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

<span data-ttu-id="2e4a9-151">如果想要使用[Microsoft JSON 日期格式](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb)(`"\/Date(ticks)\/"`) 设置而不是 ISO 8601 **DateFormatHandling**上序列化程序设置属性：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-151">If you prefer to use [Microsoft JSON date format](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) instead of ISO 8601, set the **DateFormatHandling** property on the serializer settings:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="2e4a9-152">缩进</span><span class="sxs-lookup"><span data-stu-id="2e4a9-152">Indenting</span></span>

<span data-ttu-id="2e4a9-153">编写缩进的 JSON，请设置**格式设置**将设置为**当**:</span><span class="sxs-lookup"><span data-stu-id="2e4a9-153">To write indented JSON, set the **Formatting** setting to **Formatting.Indented**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a><span data-ttu-id="2e4a9-154">驼峰式大小写</span><span class="sxs-lookup"><span data-stu-id="2e4a9-154">Camel Casing</span></span>

<span data-ttu-id="2e4a9-155">编写 JSON 属性名称使用驼峰式大小写，而无需更改你的数据模型，请设置**CamelCasePropertyNamesContractResolver**上序列化程序：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-155">To write JSON property names with camel casing, without changing your data model, set the **CamelCasePropertyNamesContractResolver** on the serializer:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a><span data-ttu-id="2e4a9-156">匿名和弱类型化对象</span><span class="sxs-lookup"><span data-stu-id="2e4a9-156">Anonymous and Weakly-Typed Objects</span></span>

<span data-ttu-id="2e4a9-157">操作方法可以返回一个匿名对象和其序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-157">An action method can return an anonymous object and serialize it to JSON.</span></span> <span data-ttu-id="2e4a9-158">例如：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-158">For example:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

<span data-ttu-id="2e4a9-159">响应消息正文将包含以下 JSON:</span><span class="sxs-lookup"><span data-stu-id="2e4a9-159">The response message body will contain the following JSON:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

<span data-ttu-id="2e4a9-160">如果你的 web API 收到松散结构化 JSON 对象从客户端，您可以反序列化请求正文**Newtonsoft.Json.Linq.JObject**类型。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-160">If your web API receives loosely structured JSON objects from clients, you can deserialize the request body to a **Newtonsoft.Json.Linq.JObject** type.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

<span data-ttu-id="2e4a9-161">但是，它是通常最好使用强类型化的数据对象。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-161">However, it is usually better to use strongly typed data objects.</span></span> <span data-ttu-id="2e4a9-162">则不需要分析的数据，并获取模型验证的优点。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-162">Then you don't need to parse the data yourself, and you get the benefits of model validation.</span></span>

<span data-ttu-id="2e4a9-163">XML 序列化程序不支持匿名类型或**JObject**实例。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-163">The XML serializer does not support anonymous types or **JObject** instances.</span></span> <span data-ttu-id="2e4a9-164">如果您使用这些功能为你的 JSON 数据，应在本文后面部分所述从管道中，删除 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-164">If you use these features for your JSON data, you should remove the XML formatter from the pipeline, as described later in this article.</span></span>

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a><span data-ttu-id="2e4a9-165">XML 媒体类型格式化程序</span><span class="sxs-lookup"><span data-stu-id="2e4a9-165">XML Media-Type Formatter</span></span>

<span data-ttu-id="2e4a9-166">XML 格式提供**XmlMediaTypeFormatter**类。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-166">XML formatting is provided by the **XmlMediaTypeFormatter** class.</span></span> <span data-ttu-id="2e4a9-167">默认情况下**XmlMediaTypeFormatter**使用**DataContractSerializer**类来执行序列化。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-167">By default, **XmlMediaTypeFormatter** uses the **DataContractSerializer** class to perform serialization.</span></span>

<span data-ttu-id="2e4a9-168">如果您愿意，可以配置**XmlMediaTypeFormatter**若要使用**XmlSerializer**而不是**DataContractSerializer**。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-168">If you prefer, you can configure the **XmlMediaTypeFormatter** to use the **XmlSerializer** instead of the **DataContractSerializer**.</span></span> <span data-ttu-id="2e4a9-169">若要执行此操作，设置**UseXmlSerializer**属性设置为**true**:</span><span class="sxs-lookup"><span data-stu-id="2e4a9-169">To do so, set the **UseXmlSerializer** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

<span data-ttu-id="2e4a9-170">**XmlSerializer**类支持一组更窄的类型，而不**DataContractSerializer**，但提供了更好地控制生成的 XML。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-170">The **XmlSerializer** class supports a narrower set of types than **DataContractSerializer**, but gives more control over the resulting XML.</span></span> <span data-ttu-id="2e4a9-171">请考虑使用**XmlSerializer**如果你需要匹配现有 XML 架构。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-171">Consider using **XmlSerializer** if you need to match an existing XML schema.</span></span>

### <a name="xml-serialization"></a><span data-ttu-id="2e4a9-172">XML 序列化</span><span class="sxs-lookup"><span data-stu-id="2e4a9-172">XML Serialization</span></span>

<span data-ttu-id="2e4a9-173">本部分介绍 XML 格式化程序，使用默认的一些特定行为**DataContractSerializer**。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-173">This section describes some specific behaviors of the XML formatter, using the default **DataContractSerializer**.</span></span>

<span data-ttu-id="2e4a9-174">默认情况下，DataContractSerializer 的行为，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-174">By default, the DataContractSerializer behaves as follows:</span></span>

- <span data-ttu-id="2e4a9-175">所有公共读/写属性和字段进行序列化。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-175">All public read/write properties and fields are serialized.</span></span> <span data-ttu-id="2e4a9-176">若要忽略的属性或字段，给它装饰**IgnoreDataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-176">To omit a property or field, decorate it with the **IgnoreDataMember** attribute.</span></span>
- <span data-ttu-id="2e4a9-177">不序列化私有和受保护成员。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-177">Private and protected members are not serialized.</span></span>
- <span data-ttu-id="2e4a9-178">只读属性不会序列化。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-178">Read-only properties are not serialized.</span></span> <span data-ttu-id="2e4a9-179">（但是，只读集合属性的内容进行序列化。）</span><span class="sxs-lookup"><span data-stu-id="2e4a9-179">(However, the contents of a read-only collection property are serialized.)</span></span>
- <span data-ttu-id="2e4a9-180">类和成员名称是用 XML 类声明中显示的完全相同。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-180">Class and member names are written in the XML exactly as they appear in the class declaration.</span></span>
- <span data-ttu-id="2e4a9-181">使用默认 XML 命名空间。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-181">A default XML namespace is used.</span></span>

<span data-ttu-id="2e4a9-182">如果需要更好地控制序列化，您可以修饰的类**DataContract**属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-182">If you need more control over the serialization, you can decorate the class with the **DataContract** attribute.</span></span> <span data-ttu-id="2e4a9-183">当存在此属性时，类被序列，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-183">When this attribute is present, the class is serialized as follows:</span></span>

- <span data-ttu-id="2e4a9-184">&quot;选择加入&quot;方法：默认情况下不序列化属性和字段。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-184">&quot;Opt in&quot; approach: Properties and fields are not serialized by default.</span></span> <span data-ttu-id="2e4a9-185">要序列化的属性或字段，给它装饰**DataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-185">To serialize a property or field, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="2e4a9-186">要序列化的私有或受保护成员，给它装饰**DataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-186">To serialize a private or protected member, decorate it with the **DataMember** attribute.</span></span>
- <span data-ttu-id="2e4a9-187">只读属性不会序列化。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-187">Read-only properties are not serialized.</span></span>
- <span data-ttu-id="2e4a9-188">若要更改类名称在 XML 中的显示方式，请设置*名称*中的参数**DataContract**属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-188">To change how the class name appears in the XML, set the *Name* parameter in the **DataContract** attribute.</span></span>
- <span data-ttu-id="2e4a9-189">若要更改成员名称在 XML 中的显示方式，请设置*名称*中的参数**DataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-189">To change how a member name appears in the XML, set the *Name* parameter in the **DataMember** attribute.</span></span>
- <span data-ttu-id="2e4a9-190">若要更改的 XML 命名空间，请设置*Namespace*中的参数**DataContract**类。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-190">To change the XML namespace, set the *Namespace* parameter in the **DataContract** class.</span></span>

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a><span data-ttu-id="2e4a9-191">只读属性</span><span class="sxs-lookup"><span data-stu-id="2e4a9-191">Read-Only Properties</span></span>

<span data-ttu-id="2e4a9-192">只读属性不会序列化。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-192">Read-only properties are not serialized.</span></span> <span data-ttu-id="2e4a9-193">如果只读属性包含支持私有字段，可以将标记具有的私有字段**DataMember**属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-193">If a read-only property has a backing private field, you can mark the private field with the **DataMember** attribute.</span></span> <span data-ttu-id="2e4a9-194">这种方法需要**DataContract**类中的属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-194">This approach requires the **DataContract** attribute on the class.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a><span data-ttu-id="2e4a9-195">日期</span><span class="sxs-lookup"><span data-stu-id="2e4a9-195">Dates</span></span>

<span data-ttu-id="2e4a9-196">日期是采用 ISO 8601 格式编写的。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-196">Dates are written in ISO 8601 format.</span></span> <span data-ttu-id="2e4a9-197">例如， &quot;2012年-05-23T20:21:37.9116538Z&quot;。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-197">For example, &quot;2012-05-23T20:21:37.9116538Z&quot;.</span></span>

<a id="xml_indenting"></a>
### <a name="indenting"></a><span data-ttu-id="2e4a9-198">缩进</span><span class="sxs-lookup"><span data-stu-id="2e4a9-198">Indenting</span></span>

<span data-ttu-id="2e4a9-199">编写缩进的 XML，请设置**缩进**属性设置为**true**:</span><span class="sxs-lookup"><span data-stu-id="2e4a9-199">To write indented XML, set the **Indent** property to **true**:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a><span data-ttu-id="2e4a9-200">设置每种类型的 XML 序列化程序</span><span class="sxs-lookup"><span data-stu-id="2e4a9-200">Setting Per-Type XML Serializers</span></span>

<span data-ttu-id="2e4a9-201">可以为不同的 CLR 类型设置不同的 XML 序列化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-201">You can set different XML serializers for different CLR types.</span></span> <span data-ttu-id="2e4a9-202">例如，你可能需要的特定数据对象**XmlSerializer**为了向后兼容。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-202">For example, you might have a particular data object that requires **XmlSerializer** for backward compatibility.</span></span> <span data-ttu-id="2e4a9-203">可以使用**XmlSerializer**此对象，并继续使用**DataContractSerializer**对于其他类型。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-203">You can use **XmlSerializer** for this object and continue to use **DataContractSerializer** for other types.</span></span>

<span data-ttu-id="2e4a9-204">若要设置为特定类型的 XML 序列化程序，请调用**SetSerializer**。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-204">To set an XML serializer for a particular type, call **SetSerializer**.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

<span data-ttu-id="2e4a9-205">您可以指定**XmlSerializer**或任何派生的对象**XmlObjectSerializer**。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-205">You can specify an **XmlSerializer** or any object that derives from **XmlObjectSerializer**.</span></span>

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a><span data-ttu-id="2e4a9-206">删除 JSON 或 XML 格式化程序</span><span class="sxs-lookup"><span data-stu-id="2e4a9-206">Removing the JSON or XML Formatter</span></span>

<span data-ttu-id="2e4a9-207">如果您不想要使用它们，可以从列表中的格式化程序，删除 JSON 格式化程序或 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-207">You can remove the JSON formatter or the XML formatter from the list of formatters, if you do not want to use them.</span></span> <span data-ttu-id="2e4a9-208">若要执行此操作的主要原因是：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-208">The main reasons to do this are:</span></span>

- <span data-ttu-id="2e4a9-209">若要限制为特定媒体类型将 web API 响应。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-209">To restrict your web API responses to a particular media type.</span></span> <span data-ttu-id="2e4a9-210">例如，你可能决定以支持仅将 JSON 响应，并删除 XML 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-210">For example, you might decide to support only JSON responses, and remove the XML formatter.</span></span>
- <span data-ttu-id="2e4a9-211">若要使用自定义格式化程序替换默认的格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-211">To replace the default formatter with a custom formatter.</span></span> <span data-ttu-id="2e4a9-212">例如，可以使用您自己的 JSON 格式化程序的自定义实现来替换 JSON 格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-212">For example, you could replace the JSON formatter with your own custom implementation of a JSON formatter.</span></span>

<span data-ttu-id="2e4a9-213">下面的代码演示如何删除默认格式化程序。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-213">The following code shows how to remove the default formatters.</span></span> <span data-ttu-id="2e4a9-214">调用此成员，从你**应用程序\_启动**Global.asax 中定义的方法。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-214">Call this from your **Application\_Start** method, defined in Global.asax.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a><span data-ttu-id="2e4a9-215">处理循环对象引用</span><span class="sxs-lookup"><span data-stu-id="2e4a9-215">Handling Circular Object References</span></span>

<span data-ttu-id="2e4a9-216">默认情况下，JSON 和 XML 格式化程序编写的所有对象作为值。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-216">By default, the JSON and XML formatters write all objects as values.</span></span> <span data-ttu-id="2e4a9-217">如果两个属性引用同一对象，或者如果两次在集合中显示同一个对象，该格式化程序会将对象序列化两次。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-217">If two properties refer to the same object, or if the same object appears twice in a collection, the formatter will serialize the object twice.</span></span> <span data-ttu-id="2e4a9-218">这是特定问题如果对象图包含循环，因为它检测到循环关系图中时，序列化程序将引发异常。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-218">This is a particular problem if your object graph contains cycles, because the serializer will throw an exception when it detects a loop in the graph.</span></span>

<span data-ttu-id="2e4a9-219">请考虑下列对象模型和控制器。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-219">Consider the following object models and controller.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

<span data-ttu-id="2e4a9-220">调用此操作将导致到格式化程序引发了异常，这会转换为状态代码 500 （内部服务器错误） 响应向客户端。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-220">Invoking this action will cause the formatter to thrown an exception, which translates to a status code 500 (Internal Server Error) response to the client.</span></span>

<span data-ttu-id="2e4a9-221">若要保留在 JSON 中的对象引用，将以下代码添加到**应用程序\_启动**Global.asax 文件中的方法：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-221">To preserve object references in JSON, add the following code to **Application\_Start** method in the Global.asax file:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

<span data-ttu-id="2e4a9-222">现在的控制器操作将返回 JSON，如下所示：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-222">Now the controller action will return JSON that looks like this:</span></span>

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

<span data-ttu-id="2e4a9-223">请注意，序列化程序将添加&quot;$id&quot;到这两个对象的属性。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-223">Notice that the serializer adds an &quot;$id&quot; property to both objects.</span></span> <span data-ttu-id="2e4a9-224">此外，检测到 Employee.Department 属性创建一个循环，因此它将使用的对象引用替换值: {&quot;$ref&quot;:&quot;1&quot;}。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-224">Also, it detects that the Employee.Department property creates a loop, so it replaces the value with an object reference: {&quot;$ref&quot;:&quot;1&quot;}.</span></span>

> [!NOTE]
> <span data-ttu-id="2e4a9-225">对象引用不是标准 json 格式。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-225">Object references are not standard in JSON.</span></span> <span data-ttu-id="2e4a9-226">使用此功能之前，请考虑你的客户端是否将能够分析结果。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-226">Before using this feature, consider whether your clients will be able to parse the results.</span></span> <span data-ttu-id="2e4a9-227">它可能是更好，只是为了从关系图删除周期。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-227">It might be better simply to remove cycles from the graph.</span></span> <span data-ttu-id="2e4a9-228">例如，在此示例中不真正需要返回到部门员工的链接。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-228">For example, the link from Employee back to Department is not really needed in this example.</span></span>


<span data-ttu-id="2e4a9-229">若要保留在 XML 中的对象引用，您具有两个选项。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-229">To preserve object references in XML, you have two options.</span></span> <span data-ttu-id="2e4a9-230">更简单的做法是将添加`[DataContract(IsReference=true)]`到模型类。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-230">The simpler option is to add `[DataContract(IsReference=true)]` to your model class.</span></span> <span data-ttu-id="2e4a9-231">*IsReference*参数支持对象的引用。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-231">The *IsReference* parameter enables object references.</span></span> <span data-ttu-id="2e4a9-232">请记住， **DataContract**参加，使序列化，因此您还需要添加**DataMember**属性的属性：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-232">Remember that **DataContract** makes serialization opt-in, so you will also need to add **DataMember** attributes to the properties:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

<span data-ttu-id="2e4a9-233">现在，格式化程序将生成类似的 XML 到以下：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-233">Now the formatter will produce XML similar to following:</span></span>

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

<span data-ttu-id="2e4a9-234">如果你想要避免在模型类上的属性，则另一个选项：创建一个新的类型特定**DataContractSerializer**实例并设置*preserveObjectReferences*到**true**构造函数中。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-234">If you want to avoid attributes on your model class, there is another option: Create a new type-specific **DataContractSerializer** instance and set *preserveObjectReferences* to **true** in the constructor.</span></span> <span data-ttu-id="2e4a9-235">在 XML 媒体类型格式化程序上则设置为每种类型序列化程序的此实例。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-235">Then set this instance as a per-type serializer on the XML media-type formatter.</span></span> <span data-ttu-id="2e4a9-236">以下代码演示如何执行此操作：</span><span class="sxs-lookup"><span data-stu-id="2e4a9-236">The following code show how to do this:</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a><span data-ttu-id="2e4a9-237">测试对象序列化</span><span class="sxs-lookup"><span data-stu-id="2e4a9-237">Testing Object Serialization</span></span>

<span data-ttu-id="2e4a9-238">设计你的 web API 时，它可用于测试您的数据对象将序列化。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-238">As you design your web API, it is useful to test how your data objects will be serialized.</span></span> <span data-ttu-id="2e4a9-239">无需创建一个控制器或调用控制器操作，可以执行此操作。</span><span class="sxs-lookup"><span data-stu-id="2e4a9-239">You can do this without creating a controller or invoking a controller action.</span></span>

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
