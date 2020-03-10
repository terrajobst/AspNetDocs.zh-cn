---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: OWIN 启动类检测 |Microsoft Docs
author: Praburaj
description: 本教程介绍如何配置加载的 OWIN startup 类。 有关 OWIN 的详细信息，请参阅项目 Katana 概述。 本教程为 。
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78500180"
---
# <a name="owin-startup-class-detection"></a><span data-ttu-id="04cc4-105">OWIN 启动类检测</span><span class="sxs-lookup"><span data-stu-id="04cc4-105">OWIN Startup Class Detection</span></span>

> <span data-ttu-id="04cc4-106">本教程介绍如何配置加载的 OWIN startup 类。</span><span class="sxs-lookup"><span data-stu-id="04cc4-106">This tutorial shows how to configure which OWIN startup class is loaded.</span></span> <span data-ttu-id="04cc4-107">有关 OWIN 的详细信息，请参阅[项目 Katana 概述](an-overview-of-project-katana.md)。</span><span class="sxs-lookup"><span data-stu-id="04cc4-107">For more information on OWIN, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="04cc4-108">本教程由 Rick Anderson （ [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ）、Praburaj Thiagarajan 和 Howard Dierking （ [@howard\_Dierking](https://twitter.com/howard_dierking) ）编写。</span><span class="sxs-lookup"><span data-stu-id="04cc4-108">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan, and Howard Dierking ( [@howard\_dierking](https://twitter.com/howard_dierking) ).</span></span>
>
> ## <a name="prerequisites"></a><span data-ttu-id="04cc4-109">系统必备</span><span class="sxs-lookup"><span data-stu-id="04cc4-109">Prerequisites</span></span>
>
> [<span data-ttu-id="04cc4-110">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="04cc4-110">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a><span data-ttu-id="04cc4-111">OWIN 启动类检测</span><span class="sxs-lookup"><span data-stu-id="04cc4-111">OWIN Startup Class Detection</span></span>

 <span data-ttu-id="04cc4-112">每个 OWIN 应用程序都有一个 startup 类，您可以在其中为应用程序管道指定组件。</span><span class="sxs-lookup"><span data-stu-id="04cc4-112">Every OWIN Application has a startup class where you specify components for the application pipeline.</span></span> <span data-ttu-id="04cc4-113">可以通过不同的方式将启动类连接到运行时，具体取决于所选的托管模型（Owinhost.exe、IIS 和 IIS Express）。</span><span class="sxs-lookup"><span data-stu-id="04cc4-113">There are different ways you can connect your startup class with the runtime, depending on the hosting model you choose (OwinHost, IIS, and IIS-Express).</span></span> <span data-ttu-id="04cc4-114">本教程中所示的 startup 类可用于每个托管应用程序。</span><span class="sxs-lookup"><span data-stu-id="04cc4-114">The startup class shown in this tutorial can be used in every hosting application.</span></span> <span data-ttu-id="04cc4-115">使用以下方法之一将 startup 类与宿主运行时连接：</span><span class="sxs-lookup"><span data-stu-id="04cc4-115">You connect the startup class with the hosting runtime using one of the these approaches:</span></span>

1. <span data-ttu-id="04cc4-116">**命名约定**： Katana 在与程序集名称或全局命名空间匹配的命名空间中查找名为 `Startup` 的类。</span><span class="sxs-lookup"><span data-stu-id="04cc4-116">**Naming Convention**: Katana looks for a class named `Startup` in namespace matching the assembly name or the global namespace.</span></span>
2. <span data-ttu-id="04cc4-117">**OwinStartup 特性**：这是大多数开发人员用来指定 startup 类的方法。</span><span class="sxs-lookup"><span data-stu-id="04cc4-117">**OwinStartup Attribute**: This is the approach most developers will take to specify the startup class.</span></span> <span data-ttu-id="04cc4-118">以下属性会将 startup 类设置为 `StartupDemo` 命名空间中的 `TestStartup` 类。</span><span class="sxs-lookup"><span data-stu-id="04cc4-118">The following attribute will set the startup class to the `TestStartup` class in the `StartupDemo` namespace.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   <span data-ttu-id="04cc4-119">`OwinStartup` 特性将重写命名约定。</span><span class="sxs-lookup"><span data-stu-id="04cc4-119">The `OwinStartup` attribute overrides the naming convention.</span></span> <span data-ttu-id="04cc4-120">你还可以使用此特性指定友好名称，但是，使用友好名称还需要使用配置文件中的 `appSetting` 元素。</span><span class="sxs-lookup"><span data-stu-id="04cc4-120">You can also specify a friendly name with this attribute, however, using a friendly name requires you to also use the `appSetting` element in the configuration file.</span></span>
3. <span data-ttu-id="04cc4-121">**配置文件中的 appSetting 元素**： `appSetting` 元素将重写 `OwinStartup` 属性和命名约定。</span><span class="sxs-lookup"><span data-stu-id="04cc4-121">**The appSetting element in the Configuration file**: The `appSetting` element overrides the `OwinStartup` attribute and naming convention.</span></span> <span data-ttu-id="04cc4-122">可以有多个启动类（每个类都使用 `OwinStartup` 属性），并配置将使用类似于下面的标记在配置文件中加载的启动类：</span><span class="sxs-lookup"><span data-stu-id="04cc4-122">You can have multiple startup classes (each using an `OwinStartup` attribute) and configure which startup class will be loaded in a configuration file using markup similar to the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   <span data-ttu-id="04cc4-123">以下显式指定 startup 类和程序集的键也可以使用：</span><span class="sxs-lookup"><span data-stu-id="04cc4-123">The following key, which explicitly specifies the startup class and assembly can also be used:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   <span data-ttu-id="04cc4-124">配置文件中的以下 XML 指定友好的启动类名称 `ProductionConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="04cc4-124">The following XML in the configuration file specifies a friendly startup class name of `ProductionConfiguration`.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   <span data-ttu-id="04cc4-125">以上标记必须与以下 `OwinStartup` 特性一起使用，该特性指定友好名称并导致 `ProductionStartup2` 类运行。</span><span class="sxs-lookup"><span data-stu-id="04cc4-125">The above markup must be used with the following `OwinStartup` attribute which specifies a friendly name and causes the `ProductionStartup2` class to run.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. <span data-ttu-id="04cc4-126">若要禁用 OWIN 启动发现，请在 web.config 文件中添加值为 `"false"` 的 `appSetting owin:AutomaticAppStartup`。</span><span class="sxs-lookup"><span data-stu-id="04cc4-126">To disable OWIN startup discovery add the `appSetting owin:AutomaticAppStartup` with a value of `"false"` in the web.config file.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a><span data-ttu-id="04cc4-127">使用 OWIN 启动创建 ASP.NET Web 应用</span><span class="sxs-lookup"><span data-stu-id="04cc4-127">Create an ASP.NET Web App using OWIN Startup</span></span>

1. <span data-ttu-id="04cc4-128">创建一个空的 Asp.Net web 应用程序并将其命名为**StartupDemo**。</span><span class="sxs-lookup"><span data-stu-id="04cc4-128">Create an empty Asp.Net web application and name it **StartupDemo**.</span></span> <span data-ttu-id="04cc4-129">-使用 NuGet 包管理器安装 `Microsoft.Owin.Host.SystemWeb`。</span><span class="sxs-lookup"><span data-stu-id="04cc4-129">- Install `Microsoft.Owin.Host.SystemWeb` using the NuGet package manager.</span></span> <span data-ttu-id="04cc4-130">从 "**工具**" 菜单中，依次选择 " **NuGet 包管理器**" 和 "**程序包管理器控制台**"。</span><span class="sxs-lookup"><span data-stu-id="04cc4-130">From the **Tools** menu, select **NuGet Package Manager**, and then **Package Manager Console**.</span></span> <span data-ttu-id="04cc4-131">输入以下命令：</span><span class="sxs-lookup"><span data-stu-id="04cc4-131">Enter the following command:</span></span>

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. <span data-ttu-id="04cc4-132">添加 OWIN startup 类。</span><span class="sxs-lookup"><span data-stu-id="04cc4-132">Add an OWIN startup class.</span></span> <span data-ttu-id="04cc4-133">在 Visual Studio 2017 中，右键单击项目并选择 "**添加类**"。-在 "**添加新项**" 对话框中，在搜索字段中输入*OWIN* ，将名称更改为 Startup.cs，然后选择 "**添加**"。</span><span class="sxs-lookup"><span data-stu-id="04cc4-133">In Visual Studio 2017 right-click the project and select **Add Class**.- In the **Add New Item** dialog box, enter *OWIN* in the search field, and change the name to Startup.cs, and then select **Add**.</span></span>

     ![](owin-startup-class-detection/_static/image1.png)

   <span data-ttu-id="04cc4-134">下次要添加*Owin Startup 类*时，它将在 "**添加**" 菜单中可用。</span><span class="sxs-lookup"><span data-stu-id="04cc4-134">The next time you want to add an *Owin Startup class*, it will be in available from the **Add** menu.</span></span>

     ![](owin-startup-class-detection/_static/image2.png)

   <span data-ttu-id="04cc4-135">或者，您可以右键单击该项目并选择 "**添加**"，然后选择 "**新建项**"，然后选择 " **Owin Startup 类**"。</span><span class="sxs-lookup"><span data-stu-id="04cc4-135">Alternatively, you can right-click the project and select **Add**, then select **New Item**, and then select the **Owin Startup class**.</span></span>

     ![](owin-startup-class-detection/_static/image3.png)

- <span data-ttu-id="04cc4-136">将*Startup.cs*文件中生成的代码替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="04cc4-136">Replace the generated code in the *Startup.cs* file with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  <span data-ttu-id="04cc4-137">`app.Use` lambda 表达式用于向 OWIN 管道注册指定的中间件组件。</span><span class="sxs-lookup"><span data-stu-id="04cc4-137">The `app.Use` lambda expression is used to register the specified middleware component to the OWIN pipeline.</span></span> <span data-ttu-id="04cc4-138">在这种情况下，我们将在响应传入请求之前设置传入请求的日志记录。</span><span class="sxs-lookup"><span data-stu-id="04cc4-138">In this case we are setting up logging of incoming requests before responding to the incoming request.</span></span> <span data-ttu-id="04cc4-139">`next` 参数是管道中的下一个组件的委托（ [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt;[任务](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx)&gt;）。</span><span class="sxs-lookup"><span data-stu-id="04cc4-139">The `next` parameter is the delegate ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) to the next component in the pipeline.</span></span> <span data-ttu-id="04cc4-140">`app.Run` lambda 表达式将管道与传入请求挂钩，并提供响应机制。</span><span class="sxs-lookup"><span data-stu-id="04cc4-140">The `app.Run` lambda expression hooks up the pipeline to incoming requests and provides the response mechanism.</span></span>
     > [!NOTE]
     > <span data-ttu-id="04cc4-141">在上面的代码中，我们已注释掉 `OwinStartup` 属性，我们将依赖于运行名为 `Startup` 的类的约定。-按***F5***运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="04cc4-141">In the code above we have commented out the `OwinStartup` attribute and we're relying on the convention of running the class named `Startup` .- Press ***F5*** to run the application.</span></span> <span data-ttu-id="04cc4-142">命中刷新几次。</span><span class="sxs-lookup"><span data-stu-id="04cc4-142">Hit refresh a few times.</span></span>

    <span data-ttu-id="04cc4-143">![](owin-startup-class-detection/_static/image4.png) 注意：本教程的图像中显示的数字与你看到的数字不匹配。</span><span class="sxs-lookup"><span data-stu-id="04cc4-143">![](owin-startup-class-detection/_static/image4.png) Note: The number shown in the images in this tutorial will not match the number you see.</span></span> <span data-ttu-id="04cc4-144">毫秒字符串用于在刷新页面时显示新的响应。</span><span class="sxs-lookup"><span data-stu-id="04cc4-144">The millisecond string is used to show a new response when you refresh the page.</span></span>
  <span data-ttu-id="04cc4-145">可以在 "**输出**" 窗口中查看跟踪信息。</span><span class="sxs-lookup"><span data-stu-id="04cc4-145">You can see the trace information in the **Output** window.</span></span>

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a><span data-ttu-id="04cc4-146">添加更多启动类</span><span class="sxs-lookup"><span data-stu-id="04cc4-146">Add More Startup Classes</span></span>

<span data-ttu-id="04cc4-147">在本部分中，我们将添加另一个启动类。</span><span class="sxs-lookup"><span data-stu-id="04cc4-147">In this section we'll add another Startup class.</span></span> <span data-ttu-id="04cc4-148">可以向应用程序添加多个 OWIN startup 类。</span><span class="sxs-lookup"><span data-stu-id="04cc4-148">You can add multiple OWIN startup class to your application.</span></span> <span data-ttu-id="04cc4-149">例如，你可能想要创建启动类以进行开发、测试和生产。</span><span class="sxs-lookup"><span data-stu-id="04cc4-149">For example, you might want to create startup classes for development, testing and production.</span></span>

1. <span data-ttu-id="04cc4-150">创建新的 OWIN Startup 类并将其命名为 `ProductionStartup`。</span><span class="sxs-lookup"><span data-stu-id="04cc4-150">Create a new OWIN Startup class and name it `ProductionStartup`.</span></span>
2. <span data-ttu-id="04cc4-151">将生成的代码替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="04cc4-151">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. <span data-ttu-id="04cc4-152">按 Ctrl F5 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="04cc4-152">Press Control F5 to run the app.</span></span> <span data-ttu-id="04cc4-153">`OwinStartup` 属性指定运行生产启动类。</span><span class="sxs-lookup"><span data-stu-id="04cc4-153">The `OwinStartup` attribute specifies the production startup class is run.</span></span>

    ![](owin-startup-class-detection/_static/image6.png)
4. <span data-ttu-id="04cc4-154">创建另一个 OWIN Startup 类并将其命名 `TestStartup`。</span><span class="sxs-lookup"><span data-stu-id="04cc4-154">Create another OWIN Startup class and name it `TestStartup`.</span></span>
5. <span data-ttu-id="04cc4-155">将生成的代码替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="04cc4-155">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   <span data-ttu-id="04cc4-156">上述 `OwinStartup` 特性重载将 `TestingConfiguration` 指定为 Startup 类的*友好*名称。</span><span class="sxs-lookup"><span data-stu-id="04cc4-156">The `OwinStartup` attribute overload above specifies `TestingConfiguration` as the *friendly* name of the Startup class.</span></span>
6. <span data-ttu-id="04cc4-157">打开 web.config*文件，* 并添加 OWIN 应用启动密钥，该密钥指定 startup 类的友好名称：</span><span class="sxs-lookup"><span data-stu-id="04cc4-157">Open the *web.config* file and add the OWIN App startup key which specifies the friendly name of the Startup class:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. <span data-ttu-id="04cc4-158">按 Ctrl F5 运行该应用程序。</span><span class="sxs-lookup"><span data-stu-id="04cc4-158">Press Control F5 to run the app.</span></span> <span data-ttu-id="04cc4-159">应用设置元素使用引用单元格，并运行测试配置。</span><span class="sxs-lookup"><span data-stu-id="04cc4-159">The app settings element takes precedent, and the test configuration is run.</span></span>

    ![](owin-startup-class-detection/_static/image7.png)
8. <span data-ttu-id="04cc4-160">从 `TestStartup` 类的 `OwinStartup` 特性中删除*友好*名称。</span><span class="sxs-lookup"><span data-stu-id="04cc4-160">Remove the *friendly* name from the `OwinStartup` attribute in the `TestStartup` class.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. <span data-ttu-id="04cc4-161">*将 web.config 文件中*的 OWIN 应用启动密钥替换为以下内容：</span><span class="sxs-lookup"><span data-stu-id="04cc4-161">Replace the OWIN App startup key in the *web.config* file with the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. <span data-ttu-id="04cc4-162">将每个类中的 `OwinStartup` 属性还原为 Visual Studio 生成的默认属性代码：</span><span class="sxs-lookup"><span data-stu-id="04cc4-162">Revert the `OwinStartup` attribute in each class to the default attribute code generated by Visual Studio:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    <span data-ttu-id="04cc4-163">下面的每个 OWIN 应用启动密钥将导致生产类运行。</span><span class="sxs-lookup"><span data-stu-id="04cc4-163">Each of the OWIN App startup keys below will cause the production class to run.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    <span data-ttu-id="04cc4-164">最后一个启动密钥指定启动配置方法。</span><span class="sxs-lookup"><span data-stu-id="04cc4-164">The last startup key specifies the startup configuration method.</span></span> <span data-ttu-id="04cc4-165">以下 OWIN 应用启动键允许你将配置类的名称更改为 `MyConfiguration`。</span><span class="sxs-lookup"><span data-stu-id="04cc4-165">The following OWIN App startup key allows you to change the name of the configuration class to `MyConfiguration` .</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a><span data-ttu-id="04cc4-166">使用 Owinhost.exe</span><span class="sxs-lookup"><span data-stu-id="04cc4-166">Using Owinhost.exe</span></span>

1. <span data-ttu-id="04cc4-167">将 web.config 文件替换为以下标记：</span><span class="sxs-lookup"><span data-stu-id="04cc4-167">Replace the Web.config file with the following markup:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   <span data-ttu-id="04cc4-168">最后一个键为 wins，因此在这种情况下，指定 `TestStartup`。</span><span class="sxs-lookup"><span data-stu-id="04cc4-168">The last key wins, so in this case `TestStartup` is specified.</span></span>
2. <span data-ttu-id="04cc4-169">从 PMC 安装 Owinhost.exe：</span><span class="sxs-lookup"><span data-stu-id="04cc4-169">Install Owinhost from the PMC:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. <span data-ttu-id="04cc4-170">导航到应用程序文件夹（包含*web.config 文件的*文件夹），并在命令提示符下键入：</span><span class="sxs-lookup"><span data-stu-id="04cc4-170">Navigate to the application folder (the folder containing the *Web.config* file) and in a command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   <span data-ttu-id="04cc4-171">命令窗口将显示：</span><span class="sxs-lookup"><span data-stu-id="04cc4-171">The command window will show:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. <span data-ttu-id="04cc4-172">使用 URL `http://localhost:5000/`启动浏览器。</span><span class="sxs-lookup"><span data-stu-id="04cc4-172">Launch a browser with the URL `http://localhost:5000/`.</span></span>

    ![](owin-startup-class-detection/_static/image8.png)

   <span data-ttu-id="04cc4-173">Owinhost.exe 遵循上面列出的启动约定。</span><span class="sxs-lookup"><span data-stu-id="04cc4-173">OwinHost honored the startup conventions listed above.</span></span>
5. <span data-ttu-id="04cc4-174">在命令窗口中，按 Enter 退出 Owinhost.exe。</span><span class="sxs-lookup"><span data-stu-id="04cc4-174">In the command window, press Enter to exit OwinHost.</span></span>
6. <span data-ttu-id="04cc4-175">在 `ProductionStartup` 类中，添加以下 OwinStartup 属性，该属性指定*ProductionConfiguration*的友好名称。</span><span class="sxs-lookup"><span data-stu-id="04cc4-175">In the `ProductionStartup` class, add the following OwinStartup attribute which specifies a friendly name of *ProductionConfiguration*.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. <span data-ttu-id="04cc4-176">在命令提示符下，键入：</span><span class="sxs-lookup"><span data-stu-id="04cc4-176">In the command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   <span data-ttu-id="04cc4-177">将加载生产启动类。</span><span class="sxs-lookup"><span data-stu-id="04cc4-177">The Production startup class is loaded.</span></span>
    ![](owin-startup-class-detection/_static/image9.png)

   <span data-ttu-id="04cc4-178">我们的应用程序具有多个启动类，在此示例中，我们已将要加载的启动类推迟到运行时。</span><span class="sxs-lookup"><span data-stu-id="04cc4-178">Our application has multiple startup classes, and in this example we have deferred which startup class to load until runtime.</span></span>
8. <span data-ttu-id="04cc4-179">测试以下运行时启动选项：</span><span class="sxs-lookup"><span data-stu-id="04cc4-179">Test the following runtime startup options:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]
