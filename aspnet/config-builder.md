---
uid: config-builder
title: ASP.NET 的配置生成器
author: rick-anderson
description: 了解如何从外部源获取 web.config 值以外的源中的配置数据。
ms.author: riande
ms.date: 10/29/2018
msc.type: content
ms.openlocfilehash: 5299d9ab057c3096773955a7461e77a80673ebfe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586765"
---
# <a name="configuration-builders-for-aspnet"></a><span data-ttu-id="e5377-103">ASP.NET 的配置生成器</span><span class="sxs-lookup"><span data-stu-id="e5377-103">Configuration builders for ASP.NET</span></span>

<span data-ttu-id="e5377-104">作者： [Stephen Molloy](https://github.com/StephenMolloy)和[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e5377-104">By [Stephen Molloy](https://github.com/StephenMolloy) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="e5377-105">配置生成器为 ASP.NET 应用提供了新式和敏捷机制，可从外部源获取配置值。</span><span class="sxs-lookup"><span data-stu-id="e5377-105">Configuration builders provide a modern and agile mechanism for ASP.NET apps to get configuration values from external sources.</span></span>

<span data-ttu-id="e5377-106">配置生成器：</span><span class="sxs-lookup"><span data-stu-id="e5377-106">Configuration builders:</span></span>

* <span data-ttu-id="e5377-107">在 .NET Framework 4.7.1 和更高版本中可用。</span><span class="sxs-lookup"><span data-stu-id="e5377-107">Are available in .NET Framework 4.7.1 and later.</span></span>
* <span data-ttu-id="e5377-108">提供用于读取配置值的灵活机制。</span><span class="sxs-lookup"><span data-stu-id="e5377-108">Provide a flexible mechanism for reading configuration values.</span></span>
* <span data-ttu-id="e5377-109">满足一些应用在容器和以云为中心的环境中的基本需求。</span><span class="sxs-lookup"><span data-stu-id="e5377-109">Address some of the basic needs of apps as they move into a container and cloud focused environment.</span></span>
* <span data-ttu-id="e5377-110">可用于通过从以前不可用的源（例如，Azure Key Vault 和环境变量）中进行绘制来改善对配置数据的保护。</span><span class="sxs-lookup"><span data-stu-id="e5377-110">Can be used to improve protection of configuration data by drawing from sources previously unavailable (for example, Azure Key Vault and environment variables) in the .NET configuration system.</span></span>

## <a name="keyvalue-configuration-builders"></a><span data-ttu-id="e5377-111">键/值配置生成器</span><span class="sxs-lookup"><span data-stu-id="e5377-111">Key/value configuration builders</span></span>

<span data-ttu-id="e5377-112">配置生成器可以处理的常见方案是为遵循键/值模式的配置节提供基本键/值替换机制。</span><span class="sxs-lookup"><span data-stu-id="e5377-112">A common scenario that can be handled by configuration builders is to provide a basic key/value replacement mechanism for configuration sections that follow a key/value pattern.</span></span> <span data-ttu-id="e5377-113">状态的 .NET Framework 概念并不限于特定的配置节或模式。</span><span class="sxs-lookup"><span data-stu-id="e5377-113">The .NET Framework concept of ConfigurationBuilders is not limited to specific configuration sections or patterns.</span></span> <span data-ttu-id="e5377-114">不过，`Microsoft.Configuration.ConfigurationBuilders` （[github](https://github.com/aspnet/MicrosoftConfigurationBuilders)， [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)）中的许多配置生成器都在键/值模式中工作。</span><span class="sxs-lookup"><span data-stu-id="e5377-114">However, many of the configuration builders in `Microsoft.Configuration.ConfigurationBuilders` ([github](https://github.com/aspnet/MicrosoftConfigurationBuilders), [NuGet](https://www.nuget.org/packages?q=Microsoft.Configuration.ConfigurationBuilders)) work within the key/value pattern.</span></span>

## <a name="keyvalue-configuration-builders-settings"></a><span data-ttu-id="e5377-115">键/值配置生成器设置</span><span class="sxs-lookup"><span data-stu-id="e5377-115">Key/value configuration builders settings</span></span>

<span data-ttu-id="e5377-116">以下设置适用于 `Microsoft.Configuration.ConfigurationBuilders`中的所有键/值配置生成器。</span><span class="sxs-lookup"><span data-stu-id="e5377-116">The following settings apply to all key/value configuration builders in `Microsoft.Configuration.ConfigurationBuilders`.</span></span>

### <a name="mode"></a><span data-ttu-id="e5377-117">模式</span><span class="sxs-lookup"><span data-stu-id="e5377-117">Mode</span></span>

<span data-ttu-id="e5377-118">配置生成器使用键/值信息的外部源来填充配置系统的选定键/值元素。</span><span class="sxs-lookup"><span data-stu-id="e5377-118">The configuration builders use an external source of key/value information to populate selected key/value elements of the configuration system.</span></span> <span data-ttu-id="e5377-119">具体而言，"`<appSettings/>`" 和 "`<connectionStrings/>`" 部分从配置生成器获得特殊处理。</span><span class="sxs-lookup"><span data-stu-id="e5377-119">Specifically, the `<appSettings/>` and `<connectionStrings/>` sections receive special treatment from the configuration builders.</span></span> <span data-ttu-id="e5377-120">生成器在三种模式下工作：</span><span class="sxs-lookup"><span data-stu-id="e5377-120">The builders work in three modes:</span></span>

* <span data-ttu-id="e5377-121">`Strict`-默认模式。</span><span class="sxs-lookup"><span data-stu-id="e5377-121">`Strict` - The default mode.</span></span> <span data-ttu-id="e5377-122">在此模式下，配置生成器仅适用于众所周知的键/值中心的配置节。</span><span class="sxs-lookup"><span data-stu-id="e5377-122">In this mode, the configuration builder only operates on well-known key/value-centric configuration sections.</span></span> <span data-ttu-id="e5377-123">`Strict` 模式枚举部分中的每个密钥。</span><span class="sxs-lookup"><span data-stu-id="e5377-123">`Strict` mode enumerates each key in the section.</span></span> <span data-ttu-id="e5377-124">如果在外部源中找到匹配的密钥：</span><span class="sxs-lookup"><span data-stu-id="e5377-124">If a matching key is found in the external source:</span></span>

   * <span data-ttu-id="e5377-125">配置生成器会将生成的配置节中的值替换为来自外部源的值。</span><span class="sxs-lookup"><span data-stu-id="e5377-125">The configuration builders replace the value in the resulting configuration section with the value from the external source.</span></span>
* <span data-ttu-id="e5377-126">`Greedy`-此模式与 `Strict` 模式密切相关。</span><span class="sxs-lookup"><span data-stu-id="e5377-126">`Greedy` - This mode is closely related to `Strict` mode.</span></span> <span data-ttu-id="e5377-127">而不是限于原始配置中已经存在的键：</span><span class="sxs-lookup"><span data-stu-id="e5377-127">Rather than being limited to keys that already exist in the original configuration:</span></span>

  * <span data-ttu-id="e5377-128">配置生成器会将外部源中的所有键/值对添加到生成的配置节。</span><span class="sxs-lookup"><span data-stu-id="e5377-128">The configuration builders adds all key/value pairs from the external source into the resulting configuration section.</span></span>

* <span data-ttu-id="e5377-129">`Expand`-在原始 XML 上进行操作，然后将其解析为配置节对象。</span><span class="sxs-lookup"><span data-stu-id="e5377-129">`Expand` - Operates on the raw XML before it's parsed into a configuration section object.</span></span> <span data-ttu-id="e5377-130">可以将它视为一个字符串中的标记扩展。</span><span class="sxs-lookup"><span data-stu-id="e5377-130">It can be thought of as an expansion of tokens in a string.</span></span> <span data-ttu-id="e5377-131">与模式 `${token}` 匹配的原始 XML 字符串的任何部分都是标记扩展的候选项。</span><span class="sxs-lookup"><span data-stu-id="e5377-131">Any part of the raw XML string that matches the pattern `${token}` is a candidate for token expansion.</span></span> <span data-ttu-id="e5377-132">如果在外部源中找不到相应的值，则不会更改该令牌。</span><span class="sxs-lookup"><span data-stu-id="e5377-132">If no corresponding value is found in the external source, then the token is not changed.</span></span> <span data-ttu-id="e5377-133">此模式中的生成器并不局限于 `<appSettings/>` 和 `<connectionStrings/>` 部分。</span><span class="sxs-lookup"><span data-stu-id="e5377-133">Builders in this mode are not limited to the `<appSettings/>` and `<connectionStrings/>` sections.</span></span>

<span data-ttu-id="e5377-134">Web.config 中的以下标记*将启用 `Strict`* 模式下的[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) ：</span><span class="sxs-lookup"><span data-stu-id="e5377-134">The following markup from *web.config* enables the [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/) in `Strict` mode:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebDefault.config?name=snippet)]

<span data-ttu-id="e5377-135">下面的代码读取前面的*web.config*文件中显示的 `<appSettings/>` 和 `<connectionStrings/>`：</span><span class="sxs-lookup"><span data-stu-id="e5377-135">The following code reads the `<appSettings/>` and `<connectionStrings/>` shown in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About.aspx.cs)]

<span data-ttu-id="e5377-136">前面的代码将属性值设置为：</span><span class="sxs-lookup"><span data-stu-id="e5377-136">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="e5377-137">如果未在环境变量中设置关键字，则为*web.config*文件中的值。</span><span class="sxs-lookup"><span data-stu-id="e5377-137">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="e5377-138">环境变量的值（如果已设置）。</span><span class="sxs-lookup"><span data-stu-id="e5377-138">The values of the environment variable, if set.</span></span>

<span data-ttu-id="e5377-139">例如，`ServiceID` 将包含：</span><span class="sxs-lookup"><span data-stu-id="e5377-139">For example, `ServiceID` will contain:</span></span>

* <span data-ttu-id="e5377-140">如果未设置环境 `ServiceID` 变量，则为 "ServiceID 中的值"。</span><span class="sxs-lookup"><span data-stu-id="e5377-140">"ServiceID value from web.config", if the environment variable `ServiceID` is not set.</span></span>
* <span data-ttu-id="e5377-141">`ServiceID` 环境变量的值（如果已设置）。</span><span class="sxs-lookup"><span data-stu-id="e5377-141">The value of the `ServiceID` environment variable, if set.</span></span>

<span data-ttu-id="e5377-142">下图显示了在环境编辑器中设置前面的*web.config*文件中的 `<appSettings/>` 键/值：</span><span class="sxs-lookup"><span data-stu-id="e5377-142">The following image shows the `<appSettings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![环境编辑器](config-builder/static/env.png)

<span data-ttu-id="e5377-144">注意：可能需要退出并重新启动 Visual Studio 才能查看环境变量中的更改。</span><span class="sxs-lookup"><span data-stu-id="e5377-144">Note: You might need to exit and restart Visual Studio to see changes in environment variables.</span></span>

### <a name="prefix-handling"></a><span data-ttu-id="e5377-145">前缀处理</span><span class="sxs-lookup"><span data-stu-id="e5377-145">Prefix handling</span></span>

<span data-ttu-id="e5377-146">密钥前缀可简化设置密钥的原因，原因如下：</span><span class="sxs-lookup"><span data-stu-id="e5377-146">Key prefixes can simplify setting keys because:</span></span>

* <span data-ttu-id="e5377-147">.NET Framework 配置是复杂的，并且是嵌套的。</span><span class="sxs-lookup"><span data-stu-id="e5377-147">The .NET Framework configuration is complex and nested.</span></span>
* <span data-ttu-id="e5377-148">外部键/值源通常是基本的并且本质上是平面的。</span><span class="sxs-lookup"><span data-stu-id="e5377-148">External key/value sources are commonly basic and flat by nature.</span></span> <span data-ttu-id="e5377-149">例如，环境变量不嵌套。</span><span class="sxs-lookup"><span data-stu-id="e5377-149">For example, environment variables are not nested.</span></span>

<span data-ttu-id="e5377-150">使用以下任一方法，通过环境变量注入配置 `<appSettings/>` 和 `<connectionStrings/>`：</span><span class="sxs-lookup"><span data-stu-id="e5377-150">Use any of the following approaches to inject both `<appSettings/>` and `<connectionStrings/>` into the configuration via environment variables:</span></span>

* <span data-ttu-id="e5377-151">在默认 `Strict` 模式下 `EnvironmentConfigBuilder`，并在配置文件中设置相应的密钥名称。</span><span class="sxs-lookup"><span data-stu-id="e5377-151">With the `EnvironmentConfigBuilder` in the default `Strict` mode and the appropriate key names in the configuration file.</span></span> <span data-ttu-id="e5377-152">前面的代码和标记采用这种方法。</span><span class="sxs-lookup"><span data-stu-id="e5377-152">The preceding code and markup takes this approach.</span></span> <span data-ttu-id="e5377-153">使用此方法时，`<appSettings/>` 和 `<connectionStrings/>`中的密钥**不**能相同。</span><span class="sxs-lookup"><span data-stu-id="e5377-153">Using this approach you can **not** have identically named keys in both `<appSettings/>` and `<connectionStrings/>`.</span></span>
* <span data-ttu-id="e5377-154">在具有不同前缀和 `stripPrefix`的 `Greedy` 模式下使用两个 `EnvironmentConfigBuilder`s。</span><span class="sxs-lookup"><span data-stu-id="e5377-154">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes and `stripPrefix`.</span></span> <span data-ttu-id="e5377-155">利用此方法，应用程序可以读取 `<appSettings/>` 和 `<connectionStrings/>`，而无需更新配置文件。</span><span class="sxs-lookup"><span data-stu-id="e5377-155">With this approach, the app can read `<appSettings/>` and `<connectionStrings/>` without needing to update the configuration file.</span></span> <span data-ttu-id="e5377-156">下一部分[stripPrefix](#stripprefix)介绍了如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="e5377-156">The next section,  [stripPrefix](#stripprefix),  shows how to do this.</span></span>
* <span data-ttu-id="e5377-157">在 `Greedy` 模式下使用具有不同前缀的两 `EnvironmentConfigBuilder`。</span><span class="sxs-lookup"><span data-stu-id="e5377-157">Use two `EnvironmentConfigBuilder`s in `Greedy` mode with distinct prefixes.</span></span> <span data-ttu-id="e5377-158">使用此方法时，不能具有重复的键名，因为键名称必须以前缀来区分。</span><span class="sxs-lookup"><span data-stu-id="e5377-158">With this approach you can't have duplicate key names as key names must differ by prefix.</span></span>  <span data-ttu-id="e5377-159">例如：</span><span class="sxs-lookup"><span data-stu-id="e5377-159">For example:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefix.config?name=snippet&highlight=11-99)]

<span data-ttu-id="e5377-160">使用上述标记，可以使用相同的平面键/值源来填充两个不同部分的配置。</span><span class="sxs-lookup"><span data-stu-id="e5377-160">With the preceding markup, the same flat key/value source can be used to populate configuration for two different sections.</span></span>

<span data-ttu-id="e5377-161">下图显示了在环境编辑器中设置前面的*web.config*文件中的 `<appSettings/>` 和 `<connectionStrings/>` 键/值：</span><span class="sxs-lookup"><span data-stu-id="e5377-161">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![环境编辑器](config-builder/static/prefix.png)

<span data-ttu-id="e5377-163">下面的代码读取前面的*web.config*文件中包含的 `<appSettings/>` 和 `<connectionStrings/>` 键/值：</span><span class="sxs-lookup"><span data-stu-id="e5377-163">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/Contact.aspx.cs?name=snippet)]

<span data-ttu-id="e5377-164">前面的代码将属性值设置为：</span><span class="sxs-lookup"><span data-stu-id="e5377-164">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="e5377-165">如果未在环境变量中设置关键字，则为*web.config*文件中的值。</span><span class="sxs-lookup"><span data-stu-id="e5377-165">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="e5377-166">环境变量的值（如果已设置）。</span><span class="sxs-lookup"><span data-stu-id="e5377-166">The values of the environment variable, if set.</span></span>

<span data-ttu-id="e5377-167">例如，使用以前的*web.config*文件、先前环境编辑器图像中的键/值和前面的代码，将设置以下值：</span><span class="sxs-lookup"><span data-stu-id="e5377-167">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="e5377-168">键</span><span class="sxs-lookup"><span data-stu-id="e5377-168">Key</span></span>              | <span data-ttu-id="e5377-169">{2&gt;值&lt;2}</span><span class="sxs-lookup"><span data-stu-id="e5377-169">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="e5377-170">AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="e5377-170">AppSetting_ServiceID</span></span>           | <span data-ttu-id="e5377-171">从 env 变量 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="e5377-171">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="e5377-172">AppSetting_default</span><span class="sxs-lookup"><span data-stu-id="e5377-172">AppSetting_default</span></span>            | <span data-ttu-id="e5377-173">从 env AppSetting_default 值</span><span class="sxs-lookup"><span data-stu-id="e5377-173">AppSetting_default value from env</span></span> |
|       <span data-ttu-id="e5377-174">ConnStr_default</span><span class="sxs-lookup"><span data-stu-id="e5377-174">ConnStr_default</span></span>         | <span data-ttu-id="e5377-175">从 env ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="e5377-175">ConnStr_default val from env</span></span>|

### <a name="stripprefix"></a><span data-ttu-id="e5377-176">stripPrefix</span><span class="sxs-lookup"><span data-stu-id="e5377-176">stripPrefix</span></span>

<span data-ttu-id="e5377-177">`stripPrefix`：布尔值，默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="e5377-177">`stripPrefix`: boolean, defaults to `false`.</span></span> 

<span data-ttu-id="e5377-178">上述 XML 标记将应用程序设置与连接字符串分离，但要求*web.config*文件中的所有键都使用指定的前缀。</span><span class="sxs-lookup"><span data-stu-id="e5377-178">The preceding XML markup separates app settings from connection strings but requires all the keys in the *web.config* file to use the specified prefix.</span></span> <span data-ttu-id="e5377-179">例如，必须将前缀 `AppSetting` 添加到 `ServiceID` 键（"AppSetting_ServiceID"）。</span><span class="sxs-lookup"><span data-stu-id="e5377-179">For example, the prefix `AppSetting` must be added to the `ServiceID` key ("AppSetting_ServiceID").</span></span> <span data-ttu-id="e5377-180">在 `stripPrefix`中，不会在*web.config 文件中*使用前缀。</span><span class="sxs-lookup"><span data-stu-id="e5377-180">With `stripPrefix`, the prefix is not used in the *web.config* file.</span></span> <span data-ttu-id="e5377-181">前缀在配置生成器源中是必需的（例如，在环境中。）我们预计大多数开发人员将使用 `stripPrefix`。</span><span class="sxs-lookup"><span data-stu-id="e5377-181">The prefix is required in the configuration builder source (for example, in the environment.) We anticipate most developers will use `stripPrefix`.</span></span>

<span data-ttu-id="e5377-182">应用程序通常会去除前缀。</span><span class="sxs-lookup"><span data-stu-id="e5377-182">Applications typically strip off the prefix.</span></span> <span data-ttu-id="e5377-183">下面的*web.config*去除前缀：</span><span class="sxs-lookup"><span data-stu-id="e5377-183">The following *web.config* strips the prefix:</span></span>

[!code-xml[Main](config-builder/MyConfigBuilders/WebPrefixStrip.config?name=snippet&highlight=14,19)]

<span data-ttu-id="e5377-184">在*前面的 web.config 文件*中，`default` 项位于 `<appSettings/>` 和 `<connectionStrings/>`。</span><span class="sxs-lookup"><span data-stu-id="e5377-184">In the preceding *web.config* file, the `default` key is in both the `<appSettings/>` and `<connectionStrings/>`.</span></span>

<span data-ttu-id="e5377-185">下图显示了在环境编辑器中设置前面的*web.config*文件中的 `<appSettings/>` 和 `<connectionStrings/>` 键/值：</span><span class="sxs-lookup"><span data-stu-id="e5377-185">The following image shows the `<appSettings/>` and `<connectionStrings/>` keys/values from the preceding *web.config* file set in the environment editor:</span></span>

![环境编辑器](config-builder/static/prefix.png)

<span data-ttu-id="e5377-187">下面的代码读取前面的*web.config*文件中包含的 `<appSettings/>` 和 `<connectionStrings/>` 键/值：</span><span class="sxs-lookup"><span data-stu-id="e5377-187">The following code reads the `<appSettings/>` and `<connectionStrings/>` keys/values contained in the preceding *web.config* file:</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/About2.aspx.cs?name=snippet)]

<span data-ttu-id="e5377-188">前面的代码将属性值设置为：</span><span class="sxs-lookup"><span data-stu-id="e5377-188">The preceding code will set the property values to:</span></span>

* <span data-ttu-id="e5377-189">如果未在环境变量中设置关键字，则为*web.config*文件中的值。</span><span class="sxs-lookup"><span data-stu-id="e5377-189">The values in the *web.config* file if the keys are not set in environment variables.</span></span>
* <span data-ttu-id="e5377-190">环境变量的值（如果已设置）。</span><span class="sxs-lookup"><span data-stu-id="e5377-190">The values of the environment variable, if set.</span></span>

<span data-ttu-id="e5377-191">例如，使用以前的*web.config*文件、先前环境编辑器图像中的键/值和前面的代码，将设置以下值：</span><span class="sxs-lookup"><span data-stu-id="e5377-191">For example, using the previous *web.config* file, the keys/values in the previous  environment editor image, and the previous code, the following values are set:</span></span>

|  <span data-ttu-id="e5377-192">键</span><span class="sxs-lookup"><span data-stu-id="e5377-192">Key</span></span>              | <span data-ttu-id="e5377-193">{2&gt;值&lt;2}</span><span class="sxs-lookup"><span data-stu-id="e5377-193">Value</span></span> |
| ----------------- | ------------ |
|     <span data-ttu-id="e5377-194">ServiceID</span><span class="sxs-lookup"><span data-stu-id="e5377-194">ServiceID</span></span>           | <span data-ttu-id="e5377-195">从 env 变量 AppSetting_ServiceID</span><span class="sxs-lookup"><span data-stu-id="e5377-195">AppSetting_ServiceID from env variables</span></span>|
|    <span data-ttu-id="e5377-196">默认值</span><span class="sxs-lookup"><span data-stu-id="e5377-196">default</span></span>            | <span data-ttu-id="e5377-197">从 env AppSetting_default 值</span><span class="sxs-lookup"><span data-stu-id="e5377-197">AppSetting_default value from env</span></span> |
|    <span data-ttu-id="e5377-198">默认值</span><span class="sxs-lookup"><span data-stu-id="e5377-198">default</span></span>         | <span data-ttu-id="e5377-199">从 env ConnStr_default val</span><span class="sxs-lookup"><span data-stu-id="e5377-199">ConnStr_default val from env</span></span>|

### <a name="tokenpattern"></a><span data-ttu-id="e5377-200">tokenPattern</span><span class="sxs-lookup"><span data-stu-id="e5377-200">tokenPattern</span></span>

<span data-ttu-id="e5377-201">`tokenPattern`： String，默认为 `@"\$\{(\w+)\}"`</span><span class="sxs-lookup"><span data-stu-id="e5377-201">`tokenPattern`: String, defaults to `@"\$\{(\w+)\}"`</span></span>

<span data-ttu-id="e5377-202">生成器的 `Expand` 行为会在原始 XML 中搜索类似于 `${token}`的令牌。</span><span class="sxs-lookup"><span data-stu-id="e5377-202">The `Expand` behavior of the builders searches the raw XML for tokens that look like `${token}`.</span></span> <span data-ttu-id="e5377-203">搜索是通过默认正则表达式 `@"\$\{(\w+)\}"`来完成的。</span><span class="sxs-lookup"><span data-stu-id="e5377-203">Searching is done with the default regular expression `@"\$\{(\w+)\}"`.</span></span> <span data-ttu-id="e5377-204">与 `\w` 匹配的字符集比 XML 和多个配置源允许的字符集更严格。</span><span class="sxs-lookup"><span data-stu-id="e5377-204">The set of characters that matches `\w` is more strict than XML and many configuration sources allow.</span></span> <span data-ttu-id="e5377-205">当令牌名称中需要超过 `@"\$\{(\w+)\}"` 个字符时，请使用 `tokenPattern`。</span><span class="sxs-lookup"><span data-stu-id="e5377-205">Use `tokenPattern` when more characters than `@"\$\{(\w+)\}"` are required in the token name.</span></span>

<span data-ttu-id="e5377-206">`tokenPattern`： String：</span><span class="sxs-lookup"><span data-stu-id="e5377-206">`tokenPattern`: String:</span></span>

* <span data-ttu-id="e5377-207">允许开发人员更改用于标记匹配的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="e5377-207">Allows developers to change the regex that is used for token matching.</span></span>
* <span data-ttu-id="e5377-208">未进行任何验证，以确保它是格式正确且不具有危险性的正则表达式。</span><span class="sxs-lookup"><span data-stu-id="e5377-208">No validation is done to make sure it is a well-formed, non-dangerous regex.</span></span>
* <span data-ttu-id="e5377-209">它必须包含一个捕获组。</span><span class="sxs-lookup"><span data-stu-id="e5377-209">It must contain a capture group.</span></span> <span data-ttu-id="e5377-210">整个正则表达式必须匹配整个标记。</span><span class="sxs-lookup"><span data-stu-id="e5377-210">The entire regex must match the entire token.</span></span> <span data-ttu-id="e5377-211">第一个捕获必须是要在配置源中查找的标记名称。</span><span class="sxs-lookup"><span data-stu-id="e5377-211">The first capture must be the token name to look up in the configuration source.</span></span>

## <a name="configuration-builders-in-microsoftconfigurationconfigurationbuilders"></a><span data-ttu-id="e5377-212">状态中的配置生成器</span><span class="sxs-lookup"><span data-stu-id="e5377-212">Configuration builders in Microsoft.Configuration.ConfigurationBuilders</span></span>

### <a name="environmentconfigbuilder"></a><span data-ttu-id="e5377-213">EnvironmentConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="e5377-213">EnvironmentConfigBuilder</span></span>

```xml
<add name="Environment"
    [mode|prefix|stripPrefix|tokenPattern] 
    type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Environment" />
```

<span data-ttu-id="e5377-214">[EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/)：</span><span class="sxs-lookup"><span data-stu-id="e5377-214">The [EnvironmentConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Environment/):</span></span>

* <span data-ttu-id="e5377-215">是最简单的配置生成器。</span><span class="sxs-lookup"><span data-stu-id="e5377-215">Is the simplest of the configuration builders.</span></span>
* <span data-ttu-id="e5377-216">从环境中读取值。</span><span class="sxs-lookup"><span data-stu-id="e5377-216">Reads values from the environment.</span></span>
* <span data-ttu-id="e5377-217">没有任何附加的配置选项。</span><span class="sxs-lookup"><span data-stu-id="e5377-217">Does not have any additional configuration options.</span></span>
* <span data-ttu-id="e5377-218">`name` 属性值为任意值。</span><span class="sxs-lookup"><span data-stu-id="e5377-218">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="e5377-219">**注意：** 在 Windows 容器环境中，在运行时设置的变量仅注入到入口点进程环境中。</span><span class="sxs-lookup"><span data-stu-id="e5377-219">**Note:** In a Windows container environment, variables set at run time are only injected into the EntryPoint process environment.</span></span> <span data-ttu-id="e5377-220">作为服务运行或非入口进程运行的应用不会选取这些变量，除非以其他方式通过容器中的机制注入它们。</span><span class="sxs-lookup"><span data-stu-id="e5377-220">Apps that run as a service or a non-EntryPoint process do not pick up these variables unless they are otherwise injected through a mechanism in the container.</span></span> <span data-ttu-id="e5377-221">对于[IIS](https://github.com/Microsoft/iis-docker/pull/41)/基于[ASP.NET](https://github.com/Microsoft/aspnet-docker)的容器， [ServiceMonitor](https://github.com/Microsoft/iis-docker/pull/41)的当前版本仅在*DefaultAppPool*中处理此项。</span><span class="sxs-lookup"><span data-stu-id="e5377-221">For [IIS](https://github.com/Microsoft/iis-docker/pull/41)/[ASP.NET](https://github.com/Microsoft/aspnet-docker)-based containers, the current version of [ServiceMonitor.exe](https://github.com/Microsoft/iis-docker/pull/41) handles this in the *DefaultAppPool* only.</span></span> <span data-ttu-id="e5377-222">其他基于 Windows 的容器变体可能需要为非入口进程开发自己的注入机制。</span><span class="sxs-lookup"><span data-stu-id="e5377-222">Other Windows-based container variants may need to develop their own injection mechanism for non-EntryPoint processes.</span></span>

### <a name="usersecretsconfigbuilder"></a><span data-ttu-id="e5377-223">UserSecretsConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="e5377-223">UserSecretsConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="e5377-224">切勿在源代码中存储密码、敏感连接字符串或其他敏感数据。</span><span class="sxs-lookup"><span data-stu-id="e5377-224">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="e5377-225">生产机密不应用于开发或测试。</span><span class="sxs-lookup"><span data-stu-id="e5377-225">Production secrets should not be used for development or test.</span></span>

```xml
<add name="UserSecrets"
    [mode|prefix|stripPrefix|tokenPattern]
    (userSecretsId="{secret string, typically a GUID}" | userSecretsFile="~\secrets.file")
    [optional="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.UserSecrets" />
```

<span data-ttu-id="e5377-226">此配置生成器提供类似于[ASP.NET Core 机密管理器](/aspnet/core/security/app-secrets)的功能。</span><span class="sxs-lookup"><span data-stu-id="e5377-226">This configuration builder provides a feature similar to [ASP.NET Core Secret Manager](/aspnet/core/security/app-secrets).</span></span>

<span data-ttu-id="e5377-227">[UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/)可用于 .NET Framework 项目，但必须指定密码文件。</span><span class="sxs-lookup"><span data-stu-id="e5377-227">The [UserSecretsConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.UserSecrets/) can be used in .NET Framework projects, but a secrets file must be specified.</span></span> <span data-ttu-id="e5377-228">或者，可以在项目文件中定义 `UserSecretsId` 属性，然后在正确的位置创建原始机密文件以进行读取。</span><span class="sxs-lookup"><span data-stu-id="e5377-228">Alternatively, you can define the `UserSecretsId` property in the project file and create the raw secrets file in the correct location for reading.</span></span> <span data-ttu-id="e5377-229">若要使外部依赖项不在项目中，则机密文件的格式为 XML。</span><span class="sxs-lookup"><span data-stu-id="e5377-229">To keep external dependencies out of your project, the secret file is XML formatted.</span></span> <span data-ttu-id="e5377-230">XML 格式是实现详细信息，不应依赖于该格式。</span><span class="sxs-lookup"><span data-stu-id="e5377-230">The XML formatting is an implementation detail, and the format should not be relied upon.</span></span> <span data-ttu-id="e5377-231">如果需要与 .NET Core 项目共享*机密 json*文件，请考虑使用[SimpleJsonConfigBuilder](#simplejsonconfigbuilder)。</span><span class="sxs-lookup"><span data-stu-id="e5377-231">If you need to share a *secrets.json* file with .NET Core projects, consider using the [SimpleJsonConfigBuilder](#simplejsonconfigbuilder).</span></span> <span data-ttu-id="e5377-232">还应将 .NET Core 的 `SimpleJsonConfigBuilder` 格式视为一个实现细节。</span><span class="sxs-lookup"><span data-stu-id="e5377-232">The `SimpleJsonConfigBuilder` format for .NET Core should also be considered an implementation detail subject to change.</span></span>

<span data-ttu-id="e5377-233">`UserSecretsConfigBuilder`的配置属性：</span><span class="sxs-lookup"><span data-stu-id="e5377-233">Configuration attributes for `UserSecretsConfigBuilder`:</span></span>

* <span data-ttu-id="e5377-234">`userSecretsId`-这是用于标识 XML 机密文件的首选方法。</span><span class="sxs-lookup"><span data-stu-id="e5377-234">`userSecretsId` - This is the preferred method for identifying an XML secrets file.</span></span> <span data-ttu-id="e5377-235">它的工作方式类似于 .NET Core，后者使用 `UserSecretsId` 项目属性来存储此标识符。</span><span class="sxs-lookup"><span data-stu-id="e5377-235">It works similar to .NET Core, which uses a `UserSecretsId` project property to store this identifier.</span></span> <span data-ttu-id="e5377-236">该字符串必须是唯一的，不需要是 GUID。</span><span class="sxs-lookup"><span data-stu-id="e5377-236">The string must be unique, it doesn't need to be a GUID.</span></span> <span data-ttu-id="e5377-237">使用此属性，`UserSecretsConfigBuilder` 在已知的本地位置（`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`）中查找属于此标识符的机密文件。</span><span class="sxs-lookup"><span data-stu-id="e5377-237">With this attribute, the `UserSecretsConfigBuilder` look in a well-known local location (`%APPDATA%\Microsoft\UserSecrets\<UserSecrets Id>\secrets.xml`) for a secrets file belonging to this identifier.</span></span>
* <span data-ttu-id="e5377-238">`userSecretsFile`-一个可选属性，用于指定包含机密的文件。</span><span class="sxs-lookup"><span data-stu-id="e5377-238">`userSecretsFile` - An optional attribute specifying the file containing the secrets.</span></span> <span data-ttu-id="e5377-239">可在开头使用 `~` 字符，以引用应用程序根目录。</span><span class="sxs-lookup"><span data-stu-id="e5377-239">The `~` character can be used at the start to reference the application root.</span></span> <span data-ttu-id="e5377-240">此属性或 `userSecretsId` 属性是必需的。</span><span class="sxs-lookup"><span data-stu-id="e5377-240">Either this attribute or the `userSecretsId` attribute is required.</span></span> <span data-ttu-id="e5377-241">如果同时指定两者，则 `userSecretsFile` 优先。</span><span class="sxs-lookup"><span data-stu-id="e5377-241">If both are specified, `userSecretsFile` takes precedence.</span></span>
* <span data-ttu-id="e5377-242">`optional`：布尔值、默认值 `true`-如果无法找到机密文件，则防止出现异常。</span><span class="sxs-lookup"><span data-stu-id="e5377-242">`optional`: boolean, default value `true` - Prevents an exception if the secrets file cannot be found.</span></span> 
* <span data-ttu-id="e5377-243">`name` 属性值为任意值。</span><span class="sxs-lookup"><span data-stu-id="e5377-243">The `name` attribute value is arbitrary.</span></span>

<span data-ttu-id="e5377-244">机密文件采用以下格式：</span><span class="sxs-lookup"><span data-stu-id="e5377-244">The secrets file has the following format:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<root>
  <secrets ver="1.0">
    <secret name="secret key name" value="secret value" />
  </secrets>
</root>
```

### <a name="azurekeyvaultconfigbuilder"></a><span data-ttu-id="e5377-245">AzureKeyVaultConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="e5377-245">AzureKeyVaultConfigBuilder</span></span>

```xml
<add name="AzureKeyVault"
    [mode|prefix|stripPrefix|tokenPattern]
    (vaultName="MyVaultName" |
     uri="https:/MyVaultName.vault.azure.net")
    [connectionString="connection string"]
    [version="secrets version"]
    [preloadSecretNames="true"]
    type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Azure" />
```

<span data-ttu-id="e5377-246">[AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/)读取存储在[Azure Key Vault](/azure/key-vault/key-vault-whatis)中的值。</span><span class="sxs-lookup"><span data-stu-id="e5377-246">The [AzureKeyVaultConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Azure/) reads values stored in the [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

<span data-ttu-id="e5377-247">需要 `vaultName` （保管库的名称或保管库的 URI）。</span><span class="sxs-lookup"><span data-stu-id="e5377-247">`vaultName` is required (either the name of the vault or a URI to the vault).</span></span> <span data-ttu-id="e5377-248">其他属性允许控制要连接到哪个保管库，但仅当应用程序未在使用 `Microsoft.Azure.Services.AppAuthentication`的环境中运行时才需要。</span><span class="sxs-lookup"><span data-stu-id="e5377-248">The other attributes allow control about which vault to connect to, but are only necessary if the application is not running in an environment that works with `Microsoft.Azure.Services.AppAuthentication`.</span></span> <span data-ttu-id="e5377-249">如果可能，将使用 Azure 服务身份验证库自动从执行环境中获取连接信息。</span><span class="sxs-lookup"><span data-stu-id="e5377-249">The Azure Services Authentication library is used to automatically pick up connection information from the execution environment if possible.</span></span> <span data-ttu-id="e5377-250">可以通过提供连接字符串来替代自动选取连接信息。</span><span class="sxs-lookup"><span data-stu-id="e5377-250">You can override automatically pick up of connection information by providing a connection string.</span></span>

* <span data-ttu-id="e5377-251">`vaultName`-如果未提供 `uri`，则为必需。</span><span class="sxs-lookup"><span data-stu-id="e5377-251">`vaultName` - Required if `uri` in not provided.</span></span> <span data-ttu-id="e5377-252">指定 Azure 订阅中要从中读取键/值对的保管库的名称。</span><span class="sxs-lookup"><span data-stu-id="e5377-252">Specifies the name of the vault in your Azure subscription from which to read key/value pairs.</span></span>
* <span data-ttu-id="e5377-253">`connectionString`- [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)可使用的连接字符串</span><span class="sxs-lookup"><span data-stu-id="e5377-253">`connectionString` - A connection string usable by [AzureServiceTokenProvider](https://docs.microsoft.com/azure/key-vault/service-to-service-authentication#connection-string-support)</span></span>
* <span data-ttu-id="e5377-254">`uri`-连接到具有指定 `uri` 值的其他 Key Vault 提供程序。</span><span class="sxs-lookup"><span data-stu-id="e5377-254">`uri` - Connects to other Key Vault providers with the specified `uri` value.</span></span> <span data-ttu-id="e5377-255">如果未指定，Azure （`vaultName`）是保管库提供程序。</span><span class="sxs-lookup"><span data-stu-id="e5377-255">If not specified, Azure (`vaultName`) is the vault provider.</span></span>
* <span data-ttu-id="e5377-256">`version` Azure Key Vault 为机密提供版本控制功能。</span><span class="sxs-lookup"><span data-stu-id="e5377-256">`version` - Azure Key Vault provides a versioning feature for secrets.</span></span> <span data-ttu-id="e5377-257">如果指定 `version`，生成器将仅检索与此版本匹配的机密。</span><span class="sxs-lookup"><span data-stu-id="e5377-257">If `version` is specified, the builder only retrieves secrets matching this version.</span></span>
* <span data-ttu-id="e5377-258">`preloadSecretNames`-默认情况下，此生成器将在初始化时 querys 密钥保管库中的**所有**密钥名称。</span><span class="sxs-lookup"><span data-stu-id="e5377-258">`preloadSecretNames` - By default, this builder querys **all** key names in the key vault when it is initialized.</span></span> <span data-ttu-id="e5377-259">若要防止读取所有键值，请将此属性设置为 `false`。</span><span class="sxs-lookup"><span data-stu-id="e5377-259">To prevent reading all key values, set this attribute to `false`.</span></span> <span data-ttu-id="e5377-260">将此设置为 `false` 一次读取一个机密。</span><span class="sxs-lookup"><span data-stu-id="e5377-260">Setting this to `false` reads secrets one at a time.</span></span> <span data-ttu-id="e5377-261">如果保管库允许 "获取" 访问权限，但不允许 "列表" 访问，则一次读取一个机密会很有用。</span><span class="sxs-lookup"><span data-stu-id="e5377-261">Reading secrets one at a time can useful if the vault allows "Get" access but not "List" access.</span></span> <span data-ttu-id="e5377-262">**注意：** 使用 `Greedy` 模式时，必须 `true` `preloadSecretNames` （默认值）。</span><span class="sxs-lookup"><span data-stu-id="e5377-262">**Note:** When using `Greedy` mode, `preloadSecretNames` must be `true` (the default.)</span></span>

### <a name="keyperfileconfigbuilder"></a><span data-ttu-id="e5377-263">KeyPerFileConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="e5377-263">KeyPerFileConfigBuilder</span></span>

```xml
<add name="KeyPerFile"
    [mode|prefix|stripPrefix|tokenPattern]
    (directoryPath="PathToSourceDirectory")
    [ignorePrefix="ignore."]
    [keyDelimiter=":"]
    [optional="false"]
    type="Microsoft.Configuration.ConfigurationBuilders.KeyPerFileConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.KeyPerFile" />
```

<span data-ttu-id="e5377-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/)是一个基本的配置生成器，它使用目录的文件作为值的源。</span><span class="sxs-lookup"><span data-stu-id="e5377-264">[KeyPerFileConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.KeyPerFile/) is a basic configuration builder that uses a directory's files as a source of values.</span></span> <span data-ttu-id="e5377-265">文件的名称为键，内容为值。</span><span class="sxs-lookup"><span data-stu-id="e5377-265">A file's name is the key, and the contents are the value.</span></span> <span data-ttu-id="e5377-266">在协调的容器环境中运行时，此配置生成器会很有用。</span><span class="sxs-lookup"><span data-stu-id="e5377-266">This configuration builder can be useful when running in an orchestrated container environment.</span></span> <span data-ttu-id="e5377-267">Docker Swarm 和 Kubernetes 等系统以每个文件的方式为其协调的 windows 容器提供 `secrets`。</span><span class="sxs-lookup"><span data-stu-id="e5377-267">Systems like Docker Swarm and Kubernetes provide `secrets` to their orchestrated windows containers in this key-per-file manner.</span></span>

<span data-ttu-id="e5377-268">属性详细信息：</span><span class="sxs-lookup"><span data-stu-id="e5377-268">Attribute details:</span></span>

* <span data-ttu-id="e5377-269">`directoryPath` - 必需。</span><span class="sxs-lookup"><span data-stu-id="e5377-269">`directoryPath` - Required.</span></span> <span data-ttu-id="e5377-270">指定要在其中查找值的路径。</span><span class="sxs-lookup"><span data-stu-id="e5377-270">Specifies a path to look in for values.</span></span> <span data-ttu-id="e5377-271">默认情况下，用于 Windows 的 Docker 密钥存储在*C:\ProgramData\Docker\secrets*目录中。</span><span class="sxs-lookup"><span data-stu-id="e5377-271">Docker for Windows secrets are stored in the *C:\ProgramData\Docker\secrets* directory by default.</span></span>
* <span data-ttu-id="e5377-272">`ignorePrefix`-不包括以此前缀开头的文件。</span><span class="sxs-lookup"><span data-stu-id="e5377-272">`ignorePrefix` - Files that start with this prefix are excluded.</span></span> <span data-ttu-id="e5377-273">默认值为“忽略”。</span><span class="sxs-lookup"><span data-stu-id="e5377-273">Defaults to "ignore.".</span></span>
* <span data-ttu-id="e5377-274">`keyDelimiter`-默认值为 `null`。</span><span class="sxs-lookup"><span data-stu-id="e5377-274">`keyDelimiter` - Default value is `null`.</span></span> <span data-ttu-id="e5377-275">如果已指定，则配置生成器将遍历目录的多个级别，并生成具有此分隔符的密钥名称。</span><span class="sxs-lookup"><span data-stu-id="e5377-275">If specified, the configuration builder traverses multiple levels of the directory, building up key names with this delimiter.</span></span> <span data-ttu-id="e5377-276">如果此值为 `null`，则配置生成器仅查看目录的顶层。</span><span class="sxs-lookup"><span data-stu-id="e5377-276">If this value is `null`, the configuration builder only looks at the top level of the directory.</span></span>
* <span data-ttu-id="e5377-277">`optional`-默认值为 `false`。</span><span class="sxs-lookup"><span data-stu-id="e5377-277">`optional` -  Default value is `false`.</span></span> <span data-ttu-id="e5377-278">如果源目录不存在，则指定配置生成器是否应导致错误。</span><span class="sxs-lookup"><span data-stu-id="e5377-278">Specifies whether the configuration builder should cause errors if the source directory doesn't exist.</span></span>

### <a name="simplejsonconfigbuilder"></a><span data-ttu-id="e5377-279">SimpleJsonConfigBuilder</span><span class="sxs-lookup"><span data-stu-id="e5377-279">SimpleJsonConfigBuilder</span></span>

> [!WARNING]
> <span data-ttu-id="e5377-280">切勿在源代码中存储密码、敏感连接字符串或其他敏感数据。</span><span class="sxs-lookup"><span data-stu-id="e5377-280">Never store passwords, sensitive connection strings, or other sensitive data in source code.</span></span> <span data-ttu-id="e5377-281">生产机密不应用于开发或测试。</span><span class="sxs-lookup"><span data-stu-id="e5377-281">Production secrets should not be used for development or test.</span></span>

```xml
<add name="SimpleJson"
    [mode|prefix|stripPrefix|tokenPattern]
    jsonFile="~\config.json"
    [optional="true"]
    [jsonMode="(Flat|Sectional)"]
    type="Microsoft.Configuration.ConfigurationBuilders.SimpleJsonConfigBuilder,
    Microsoft.Configuration.ConfigurationBuilders.Json" />
```

<span data-ttu-id="e5377-282">.NET Core 项目经常使用 JSON 文件进行配置。</span><span class="sxs-lookup"><span data-stu-id="e5377-282">.NET Core projects frequently use JSON files for configuration.</span></span> <span data-ttu-id="e5377-283">[SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/)生成器允许在 .NET Framework 中使用 .NET Core JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="e5377-283">The [SimpleJsonConfigBuilder](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Json/) builder allows .NET Core JSON files to be used in the .NET Framework.</span></span> <span data-ttu-id="e5377-284">此配置生成器提供了从平面键/值源到 .NET Framework 配置的特定键/值区域的基本映射。</span><span class="sxs-lookup"><span data-stu-id="e5377-284">This configuration builder is provides a basic mapping from a flat key/value source into specific key/value areas of .NET Framework configuration.</span></span> <span data-ttu-id="e5377-285">此配置生成器不**提供分层**配置。</span><span class="sxs-lookup"><span data-stu-id="e5377-285">This configuration builder does **not** provide for hierarchical configurations.</span></span> <span data-ttu-id="e5377-286">JSON 支持文件类似于字典，而不是复杂的层次结构对象。</span><span class="sxs-lookup"><span data-stu-id="e5377-286">The JSON backing file is similar to a dictionary, not a complex hierarchical object.</span></span> <span data-ttu-id="e5377-287">可以使用多级别的分层文件。</span><span class="sxs-lookup"><span data-stu-id="e5377-287">A multi-level hierarchical file can be used.</span></span> <span data-ttu-id="e5377-288">此访问接口通过使用 `:` 作为分隔符，在每个级别追加属性名称来 `flatten`深度。</span><span class="sxs-lookup"><span data-stu-id="e5377-288">This provider `flatten`s the depth by appending the property name at each level using `:` as a delimiter.</span></span>

<span data-ttu-id="e5377-289">属性详细信息：</span><span class="sxs-lookup"><span data-stu-id="e5377-289">Attribute details:</span></span>

* <span data-ttu-id="e5377-290">`jsonFile` - 必需。</span><span class="sxs-lookup"><span data-stu-id="e5377-290">`jsonFile` - Required.</span></span> <span data-ttu-id="e5377-291">指定要从中进行读取的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="e5377-291">Specifies the JSON file to read from.</span></span> <span data-ttu-id="e5377-292">可在开头使用 `~` 字符，以引用应用根目录。</span><span class="sxs-lookup"><span data-stu-id="e5377-292">The `~` character can be used at the start to reference the app root.</span></span>
* <span data-ttu-id="e5377-293">`optional` 布尔值，则 `true`默认值。</span><span class="sxs-lookup"><span data-stu-id="e5377-293">`optional` - Boolean,  default value is `true`.</span></span> <span data-ttu-id="e5377-294">如果找不到 JSON 文件，则防止引发异常。</span><span class="sxs-lookup"><span data-stu-id="e5377-294">Prevents throwing exceptions if the JSON file cannot be found.</span></span>
* <span data-ttu-id="e5377-295">`jsonMode` - `[Flat|Sectional]`。</span><span class="sxs-lookup"><span data-stu-id="e5377-295">`jsonMode` - `[Flat|Sectional]`.</span></span> <span data-ttu-id="e5377-296">默认为 `Flat`。</span><span class="sxs-lookup"><span data-stu-id="e5377-296">`Flat` is the default.</span></span> <span data-ttu-id="e5377-297">当 `Flat``jsonMode` 时，JSON 文件是单个平面键/值源。</span><span class="sxs-lookup"><span data-stu-id="e5377-297">When `jsonMode` is `Flat`, the JSON file is a single flat key/value source.</span></span> <span data-ttu-id="e5377-298">`EnvironmentConfigBuilder` 和 `AzureKeyVaultConfigBuilder` 也是单层的键/值源。</span><span class="sxs-lookup"><span data-stu-id="e5377-298">The `EnvironmentConfigBuilder` and `AzureKeyVaultConfigBuilder` are also single flat key/value sources.</span></span> <span data-ttu-id="e5377-299">在 `Sectional` 模式下配置 `SimpleJsonConfigBuilder` 时：</span><span class="sxs-lookup"><span data-stu-id="e5377-299">When the `SimpleJsonConfigBuilder` is configured in `Sectional` mode:</span></span>

  * <span data-ttu-id="e5377-300">JSON 文件在概念上只分成了多个字典。</span><span class="sxs-lookup"><span data-stu-id="e5377-300">The JSON file is conceptually divided just at the top level into multiple dictionaries.</span></span>
  * <span data-ttu-id="e5377-301">每个字典仅适用于与附加到它们的顶级属性名称匹配的配置节。</span><span class="sxs-lookup"><span data-stu-id="e5377-301">Each of the dictionaries is only applied to the configuration section that matches the top-level property name attached to them.</span></span> <span data-ttu-id="e5377-302">例如：</span><span class="sxs-lookup"><span data-stu-id="e5377-302">For example:</span></span>

```json
    {
        "appSettings" : {
            "setting1" : "value1",
            "setting2" : "value2",
            "complex" : {
                "setting1" : "complex:value1",
                "setting2" : "complex:value2",
            }
        }
    }
```

## <a name="implementing-a-custom-keyvalue-configuration-builder"></a><span data-ttu-id="e5377-303">实现自定义键/值配置生成器</span><span class="sxs-lookup"><span data-stu-id="e5377-303">Implementing a custom key/value configuration builder</span></span>

<span data-ttu-id="e5377-304">如果配置生成器不能满足您的需要，则可以编写一个自定义的。</span><span class="sxs-lookup"><span data-stu-id="e5377-304">If the configuration builders don't meet your needs, you can write a custom one.</span></span> <span data-ttu-id="e5377-305">`KeyValueConfigBuilder` 基类处理替换模式和大多数前缀问题。</span><span class="sxs-lookup"><span data-stu-id="e5377-305">The `KeyValueConfigBuilder` base class handles substitution modes and most prefix concerns.</span></span> <span data-ttu-id="e5377-306">实现项目只需要：</span><span class="sxs-lookup"><span data-stu-id="e5377-306">An implementing project need only:</span></span>

* <span data-ttu-id="e5377-307">从基类继承，并通过 `GetValue` 和 `GetAllValues`实现键/值对的基本源：</span><span class="sxs-lookup"><span data-stu-id="e5377-307">Inherit from the base class and implement a basic source of key/value pairs through the `GetValue` and `GetAllValues`:</span></span>
* <span data-ttu-id="e5377-308">将[状态](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/)添加到项目。</span><span class="sxs-lookup"><span data-stu-id="e5377-308">Add the [Microsoft.Configuration.ConfigurationBuilders.Base](https://www.nuget.org/packages/Microsoft.Configuration.ConfigurationBuilders.Base/) to the project.</span></span>

[!code-csharp[Main](config-builder/MyConfigBuilders/MyCustomConfigBuilder.cs)]

<span data-ttu-id="e5377-309">`KeyValueConfigBuilder` 基类在键/值配置生成器中提供了许多工作和一致的行为。</span><span class="sxs-lookup"><span data-stu-id="e5377-309">The `KeyValueConfigBuilder` base class provides much of the work and consistent behavior across key/value configuration builders.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e5377-310">其他资源</span><span class="sxs-lookup"><span data-stu-id="e5377-310">Additional resources</span></span>

* [<span data-ttu-id="e5377-311">配置生成器 GitHub 存储库</span><span class="sxs-lookup"><span data-stu-id="e5377-311">Configuration Builders GitHub repository</span></span>](https://github.com/aspnet/MicrosoftConfigurationBuilders)
* [<span data-ttu-id="e5377-312">使用 .NET Azure Key Vault 的服务到服务身份验证</span><span class="sxs-lookup"><span data-stu-id="e5377-312">Service-to-service authentication to Azure Key Vault using .NET</span></span>](/azure/key-vault/service-to-service-authentication#connection-string-support)
