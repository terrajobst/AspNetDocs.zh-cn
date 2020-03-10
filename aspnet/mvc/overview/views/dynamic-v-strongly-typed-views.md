---
uid: mvc/overview/views/dynamic-v-strongly-typed-views
title: 动态类型化视图与 强类型视图 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/27/2011
ms.assetid: 0cbd88da-0da6-4605-b222-2835c6478304
msc.legacyurl: /mvc/overview/views/dynamic-v-strongly-typed-views
msc.type: authoredcontent
ms.openlocfilehash: 3e81c6381b1e280e3b74cb7eb6ea6e6c3224e655
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78432572"
---
# <a name="dynamic-v-strongly-typed-views"></a>动态类型化视图与 强类型化视图

作者： [Rick Anderson](https://twitter.com/RickAndMSFT)

有三种方法可以将信息从控制器传递到 ASP.NET MVC 3 中的视图：

1. 作为强类型化模型对象。
2. 为动态类型（使用 @model dynamic）
3. 使用 ViewBag

我编写了一个简单的 MVC 3 顶级博客应用程序，用于比较和对比动态和强类型化的视图。 该控制器首先提供博客的简单列表：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample1.cs)]

右键单击 "IndexNotStonglyTyped" （）方法并添加 "Razor" 视图。

[![8475. NotStronglyTypedView [1]](dynamic-v-strongly-typed-views/_static/image2.png)](dynamic-v-strongly-typed-views/_static/image1.png)

请确保未选中 "**创建强类型视图**" 框。 生成的视图不包含太多内容：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample2.cshtml)]

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample3.cshtml)]

由于我们使用的是动态而不是强类型视图，intellisense 不能帮助我们。 完成的代码如下所示：

[!code-cshtml[Main](dynamic-v-strongly-typed-views/samples/sample4.cshtml)]

[![6646 NotStronglyTypedView_5F00_IE [1]](dynamic-v-strongly-typed-views/_static/image4.png)](dynamic-v-strongly-typed-views/_static/image3.png)

现在，我们将添加一个强类型视图。 将以下代码添加到控制器：

[!code-csharp[Main](dynamic-v-strongly-typed-views/samples/sample5.cs)]

请注意，它的返回视图（topBlogs）完全相同;作为非强类型视图调用。 在*StonglyTypedIndex （）* 中右键单击，然后选择 "**添加视图**"。 这次选择 "**博客**模型类"，然后选择 "**列表**" 作为基架模板。

[![5658. StrongView [1]](dynamic-v-strongly-typed-views/_static/image6.png)](dynamic-v-strongly-typed-views/_static/image5.png)

在新的视图模板中，我们获得 intellisense 支持。

[![7002 [1]](dynamic-v-strongly-typed-views/_static/image8.png)](dynamic-v-strongly-typed-views/_static/image7.png)

可在[此处](https://blogs.msdn.com/cfs-file.ashx/__key/CommunityServer-Blogs-Components-WeblogFiles/00-00-01-11-73-SSMS/1817.Mvc3ViewDemo.zip)下载 c # 项目。
