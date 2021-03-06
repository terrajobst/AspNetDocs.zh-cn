---
uid: web-forms/what-is-web-forms
title: 什么是 Web 窗体 |Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 5fa1daf9-1161-4cfa-bd4c-658f48b2c229
msc.legacyurl: /web-forms/what-is-web-forms
msc.type: content
ms.openlocfilehash: 19be419c499759713971a6c77674c924867d1bbc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516920"
---
# <a name="what-is-web-forms"></a>什么是 Web 窗体

ASP.NET Web 窗体是 ASP.NET web 应用程序框架的一部分，并包含在[Visual Studio](https://www.asp.net/downloads)中。 这是可用于创建 ASP.NET web 应用程序的四个编程模型之一，其他是 ASP.NET MVC、ASP.NET 网页和 ASP.NET 单页应用程序。

Web 窗体是用户使用浏览器请求的页面。 可以结合使用 HTML、客户端脚本、服务器控件和服务器代码来编写这些页面。 当用户请求某个页面时，框架会在服务器上编译并执行该页面，然后框架将生成浏览器可以呈现的 HTML 标记。 ASP.NET Web 窗体页向用户提供有关浏览器或客户端设备的信息。

使用 Visual Studio，可以创建 ASP.NET Web 窗体。 Visual Studio 集成开发环境（IDE）允许您拖放服务器控件以布局您的 Web 窗体页。 然后，可以轻松地为页面上的控件或页面本身设置属性、方法和事件。 这些属性、方法和事件用于定义网页的行为、外观，等等。 若要编写服务器代码来处理页面的逻辑，可以使用 .NET 语言，如 Visual Basic 或C#。

> [!NOTE] 
> 
> ASP.NET 和 Visual Studio 文档跨多个版本。 对于使用最新版本的当前任务和方案，突出显示先前版本中的功能的主题可能会很有用。

**ASP.NET Web 窗体为：** 

- 基于 Microsoft ASP.NET 技术，在服务器上运行的代码会将网页输出动态生成到浏览器或客户端设备。
- 与任何浏览器或移动设备兼容。 ASP.NET 网页自动为样式、布局等功能呈现正确的符合浏览器的 HTML。
- 兼容 .NET 公共语言运行时支持的任何语言，如 Microsoft Visual Basic 和 Microsoft 视觉对象C#。
- 基于 Microsoft .NET 框架构建。 这可提供框架的所有优点，包括托管环境、类型安全性和继承。
- 灵活，因为可以将用户创建的和第三方控件添加到其中。

**ASP.NET Web 窗体提供：** 

- 从应用程序逻辑分离 HTML 和其他 UI 代码。
- 用于常见任务的丰富的服务器控件套件，包括数据访问。
- 强大的数据绑定功能，具有强大的工具支持。
- 支持在浏览器中执行的客户端脚本。
- 支持各种其他功能，包括路由、安全性、性能、国际化、测试、调试、错误处理和状态管理。

## <a name="aspnet-web-forms-helps-you-overcome-challenges"></a>ASP.NET Web 窗体有助于应对挑战

Web 应用程序编程是指编程基于客户端的传统应用程序时通常不会出现的难题。 面临的挑战包括：

- **实现丰富的 Web 用户界面**-使用基本 HTML 功能设计和实现用户界面可能会很困难且单调乏味，尤其是在页面具有复杂布局、大量动态内容以及功能完备的用户交互式对象时。
- **客户端和服务器**之间的分离-在 Web 应用程序中，客户端（浏览器）和服务器通常运行在不同的计算机上（甚至在不同的操作系统上）。 因此，应用程序的两个部分共享几乎信息;它们可以通信，但通常仅交换小块简单信息。
- **无状态执行**-当 Web 服务器接收到页面的请求时，它会查找该页，处理它，然后将其发送到浏览器，然后放弃所有页面信息。 如果用户再次请求同一页，服务器将重复整个序列，并从头开始重新处理页。 换句话说，服务器没有已处理的页的内存，页是无状态的。 因此，如果应用程序需要维护有关页面的信息，则其无状态性质可能会成为问题。
- **未知的客户端功能**-在许多情况下，使用不同浏览器的多个用户可以访问 Web 应用程序。 浏览器具有不同的功能，因此很难创建在所有这些应用程序上都同样能正常运行的应用程序。
- **数据访问的复杂性**-从传统 Web 应用程序中读取和写入数据源可能会很复杂且消耗大量资源。
- **具有可伸缩性的复杂性**-在很多情况下，通过现有方法设计的 Web 应用程序无法实现可伸缩性目标，因为应用程序的各种组件之间缺乏兼容性。 对于较大的增长周期，这通常是应用程序的常见故障点。

满足这些 Web 应用程序的挑战可能需要大量的时间和精力。 ASP.NET Web 窗体和 ASP.NET 框架通过以下方式解决了这些难题：

- **直观、一致的对象模型**-ASP.NET 页框架提供一个对象模型，该模型使你能够将窗体视为一个单元，而不是单独的客户端和服务器部分。 在此模型中，你可以采用比在传统 Web 应用程序中更直观的方式来编程页面，包括设置页面元素的属性和响应事件的功能。 此外，ASP.NET 服务器控件是从 HTML 页面的物理内容到浏览器与服务器之间直接交互的抽象。 通常，你可以使用服务器控件，因为你可以在客户端应用程序中使用控件，而无需考虑如何创建 HTML 来显示和处理控件及其内容。
- **事件驱动的编程模型**-ASP.NET Web 窗体为 web 应用程序提供熟悉的模型，以便为客户端或服务器上发生的事件编写事件处理程序。 ASP.NET 页框架以这样一种方式对此模型进行抽象：捕获客户端上的事件、将其传输到服务器以及调用相应方法的基础机制都是自动进行的，并且对你不可见。 其结果是一个简单的简单编写的代码结构，支持事件驱动的开发。
- **直观状态管理**-ASP.NET 页框架自动处理维护页及其控件状态的任务，并为您提供用于维护特定于应用程序的信息状态的显式方法。 这是在不大量使用服务器资源的情况下完成的，并且可以使用或不向浏览器发送 cookie 来实现。
- **独立于浏览器的应用程序**-ASP.NET 页框架使你能够在服务器上创建所有应用程序逻辑，从而无需在浏览器中显式编写代码差异。 但是，它仍可让你通过编写客户端代码来利用特定于浏览器的功能，以提供改进的性能和更丰富的客户端体验。
- **.NET Framework 公共语言运行时支持**-ASP.NET 页框架是基于 .NET Framework 构建的，因此整个框架可用于任何 ASP.NET 应用程序。 您的应用程序可以用与运行时兼容的任何语言编写。 此外，通过使用 .NET Framework 提供的数据访问基础结构（包括 ADO.NET）简化了数据访问。
- **.NET Framework 可伸缩服务器性能**-使用 ASP.NET 页框架，可将 Web 应用程序从具有单处理器的一台计算机完全扩展到多计算机 Web 场，而无需对应用程序的逻辑进行复杂的更改。

## <a name="features-of-aspnet-web-forms"></a>ASP.NET Web 窗体的功能

- **服务器控件**-ASP.NET web 服务器控件是在请求页面时运行的 ASP.NET 网页上的对象，并将标记呈现到浏览器。 许多 Web 服务器控件类似于熟悉的 HTML 元素，如按钮和文本框。 其他控件包含可用于连接到数据源并显示数据的复杂行为，如日历控件和控件。
- **母版页**-ASP.NET 母版页允许您为应用程序中的页面创建一致的布局。 可以使用单个母版页定义应用程序中所有页（或一组页）的外观和标准行为。 然后，你可以创建包含想要显示的内容的各个内容页。 当用户请求内容页时，它们将与母版页合并，以生成将母版页布局与内容页的内容合并的输出。
- 使用**数据**-ASP.NET 提供了许多用于存储、检索和显示数据的选项。 在 ASP.NET Web 窗体应用程序中，可以使用数据绑定控件来自动显示或输入网页 UI 元素（例如表和文本框和下拉列表）中的数据。
- **成员身份**ASP.NET Identity 将用户的凭据存储在由应用程序创建的数据库中。 当用户登录时，应用程序将通过读取数据库来验证凭据。 项目的*帐户*文件夹包含实现成员身份的各个部分的文件：注册、登录、更改密码和授权访问。 此外，ASP.NET Web 窗体支持 OAuth 和 OpenID。 这些身份验证增强功能允许用户使用现有凭据（来自 Facebook、Twitter、Windows Live 和 Google 等帐户）登录到你的站点。 默认情况下，模板使用默认数据库名称在 SQL Server Express LocalDB 的实例上创建成员资格数据库，该服务器附带了 Visual Studio Express 2013 for Web 的开发数据库服务器。
- **客户端脚本和客户端框架**-可以通过在 ASP.NET Web 窗体页中包含客户端脚本功能来增强 ASP.NET 的基于服务器的功能。 可以使用客户端脚本向用户提供更丰富、更有响应能力的用户界面。 在浏览器中运行某个页面时，还可以使用客户端脚本对 Web 服务器进行异步调用。
- 使用**路由**URL 路由，你可以将应用程序配置为接受未映射到物理文件的请求 url。 请求 URL 只是用户在浏览器中输入的 URL，用于在您的网站上查找页面。 使用路由定义对用户具有语义意义的 Url，并可帮助搜索引擎优化（SEO）。
- **状态管理**-ASP.NET Web 窗体包含多个选项，这些选项可帮助您在每个页面和整个应用程序范围内保留数据。
- **安全性**-开发更安全的应用程序的一个重要部分是了解它的威胁。 Microsoft 开发了一种方法来分类威胁：欺骗、篡改、否认、信息泄露、拒绝服务和特权提升（STRIDE）。 在 ASP.NET Web 窗体中，你可以添加扩展点和配置选项，使你能够在 ASP.NET Web 窗体中自定义各种安全行为。
- **性能**-性能可能是成功的网站或项目的关键因素。 使用 ASP.NET Web 窗体，可以修改与页面和服务器控制处理、状态管理、数据访问、应用程序配置和加载以及高效编码做法相关的性能。
- **国际化**-ASP.NET Web 窗体使你可以基于浏览器的首选语言设置或基于用户的显式语言选择，创建可获取内容和其他数据的网页。 内容和其他数据称为资源，此类数据可以存储在资源文件或其他源中。 在 ASP.NET Web 窗体页中，可以将控件配置为从资源获取其属性值。 在运行时，资源表达式将替换为相应的本地化资源文件中的资源。
- **调试和错误处理**-ASP.NET 包含的功能可帮助你诊断 Web 窗体应用程序中可能出现的问题。 ASP.NET Web 窗体中支持调试和错误处理，以便您的应用程序能够有效地编译和运行。
- **部署和托管**-Visual Studio、ASP.NET、AZURE 和 IIS 提供的工具可帮助你部署和托管 Web 窗体应用程序。

## <a name="deciding-when-to-create-a-web-forms-application"></a>确定何时创建 Web 窗体应用程序

您必须仔细考虑是使用 ASP.NET Web 窗体模型还是其他模型（如 ASP.NET MVC 框架）来实现 Web 应用程序。 MVC 框架未取代 Web 窗体模型；您可以对 Web 应用程序使用任一框架。 在您决定为特定网站使用 Web 窗体模型或 MVC 框架之前，请先权衡每种方法的优点。

### <a name="advantages-of-a-web-forms-based-web-application"></a>基于 Web 窗体的 Web 应用程序的优点

基于 Web 窗体的框架具有以下优点：

- 它支持通过 HTTP 保留状态的事件模型，这有益于开发业务线 Web 应用程序。 基于 Web 窗体的应用程序提供了在数百个服务器控件中受支持的许多事件。
- 它使用页面控制器模式向单个页面添加功能。 有关详细信息，请参阅 MSDN 网站上的[页面控制器](https://go.microsoft.com/fwlink/?LinkId=106359 "页面控制器")。
- 它使用视图状态或基于服务器的窗体，这会使管理状态信息变得更加容易。
- 它非常适合想要利用大量组件快速开发应用程序的 Web 开发人员和设计人员的小型团队。
- 通常，应用程序开发不太复杂，因为组件（**页**类、控件等）紧密集成，通常需要的代码比 MVC 模型少。

### <a name="advantages-of-an-mvc-based-web-application"></a>基于 MVC 的 Web 应用程序的优点

ASP.NET MVC 框架具有以下优点：

- 通过将应用程序分为模型、视图和控制器，化繁为简的工作更加轻松。
- 它不使用视图状态或基于服务器的窗体。 这使得 MVC 框架特别适合想要完全控制应用程序行为的开发人员。
- 它使用一种通过单一控制器处理 Web 应用程序请求的前端控制器模式。 这使您可以设计一个支持丰富路由基础结构的应用程序。 有关详细信息，请参阅 MSDN 网站上的[前端控制器](https://go.microsoft.com/fwlink/?LinkId=106357 "前台控制器")。
- 它为测试驱动的开发 (TDD) 提供了更好的支持。
- 它适用于需要对应用程序行为进行高度控制的大型开发人员和 Web 设计人员支持的 Web 应用程序。
