---
ms.openlocfilehash: 545448e3673b02abc7e685bd987f2cf5f71375b4
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57051954"
---
> [!WARNING]
> 出于安全原因，必须选择绑定 `GET` 请求数据以对模型属性进行分页。 请在将用户输入映射到属性前对其进行验证。 当处理依赖查询字符串或路由值的方案时，选择加入 `GET` 绑定非常有用。
>
> 要将属性绑定在 `GET` 请求上，请将 [[BindProperty]](/dotnet/api/microsoft.aspnetcore.mvc.bindpropertyattribute) 特性的 `SupportsGet` 属性设置为 `true`: `[BindProperty(SupportsGet = true)]`
