---
ms.openlocfilehash: eb2f83504129ae2b19ff5d85a2bc7d90293b43d6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57043394"
---
* Startup.cs:[Startup 类](xref:fundamentals/startup)-类配置处理对应用程序所做的所有请求的请求管道。
* Program.cs:[编程类](xref:fundamentals/index)，其中包含应用程序的主入口点。
* firstapp.csproj :[项目文件](/dotnet/articles/core/preview3/tools/csproj)ASP.NET Core 应用程序的 MSBuild 项目文件格式。 包含项目到项目的引用，NuGet 引用和其他项目相关的项。
* appsettings.json / appsettings。Development.json:环境基应用设置配置文件。 [请参阅配置](xref:fundamentals/configuration/index)。
* bower.json:Bower 包项目的依赖项。
* .bowerrc:Bower 配置文件定义当 Bower 下载资产时安装组件的位置。
* bundleconfig.json： 绑定和缩小前端的 JavaScript 和 CSS 资产的配置文件。
* 视图：包含 Razor 视图。 视图是显示应用用户界面 (UI) 的组件。 此 UI 通常会显示模型数据。
* 控制器：包含 MVC 控制器，最初*HomeController.cs*。 控制器是处理浏览器请求的类。
* wwwroot:Web 应用程序根文件夹。

有关详细信息请参阅[MVC 模式](xref:mvc/overview)。
