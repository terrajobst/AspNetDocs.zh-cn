---
uid: mvc/overview/advanced/custom-mvc-templates
title: 自定义 MVC 模板 |Microsoft Docs
author: joeloff
description: 创建一个模板作为 VSIX 扩展。
ms.author: riande
ms.date: 12/10/2012
ms.assetid: b0a214c7-2f38-4dbc-b47f-bd7bd9df97bd
msc.legacyurl: /mvc/overview/advanced/custom-mvc-templates
msc.type: authoredcontent
ms.openlocfilehash: 0603bc24e070e223551813f66a75889a2e46fd35
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499598"
---
# <a name="custom-mvc-template"></a><span data-ttu-id="ccc08-103">自定义 MVC 模板</span><span class="sxs-lookup"><span data-stu-id="ccc08-103">Custom MVC Template</span></span>

<span data-ttu-id="ccc08-104">作者： [Jacques Eloff](https://github.com/joeloff)</span><span class="sxs-lookup"><span data-stu-id="ccc08-104">by [Jacques Eloff](https://github.com/joeloff)</span></span>

<span data-ttu-id="ccc08-105">版本的 MVC 3 Tools Update for Visual Studio 2010 为 MVC 项目引入了单独的项目向导。</span><span class="sxs-lookup"><span data-stu-id="ccc08-105">The release of MVC 3 Tools Update for Visual Studio 2010 introduced a separate project wizard for MVC projects.</span></span> <span data-ttu-id="ccc08-106">更改由两个因素驱动。</span><span class="sxs-lookup"><span data-stu-id="ccc08-106">The change was driven by two factors.</span></span> <span data-ttu-id="ccc08-107">首先，在 MVC 3 中引入了新模板，并支持 Razor 等其他视图引擎，从而 overcrowding Visual Studio 中的 "新建项目" 对话框。</span><span class="sxs-lookup"><span data-stu-id="ccc08-107">First, the introduction of new templates in MVC 3 and support for additional view engines such as Razor lead to overcrowding the New Project dialog in Visual Studio.</span></span> <span data-ttu-id="ccc08-108">其次，客户一直在寻求扩展点，而新的 MVC 项目向导将为我们提供响应这些请求的机会。</span><span class="sxs-lookup"><span data-stu-id="ccc08-108">Second, customers had been asking for extensibility points and the new MVC project wizard would afford us the opportunity to respond to these requests.</span></span>

<span data-ttu-id="ccc08-109">添加自定义模板是一个棘手进程，它依赖于使用注册表使新模板对 MVC 项目向导可见。</span><span class="sxs-lookup"><span data-stu-id="ccc08-109">Adding custom templates was an arduous process that relied on using the registry to make new templates visible to the MVC project wizard.</span></span> <span data-ttu-id="ccc08-110">新模板的作者必须将其包装在 MSI 内，以确保在安装时创建必要的注册表项。</span><span class="sxs-lookup"><span data-stu-id="ccc08-110">The author of a new template had to wrap it inside an MSI to ensure that the necessary registry entries would be created at install time.</span></span> <span data-ttu-id="ccc08-111">替代方法是生成包含模板的 ZIP 文件，并让最终用户手动创建所需的注册表项。</span><span class="sxs-lookup"><span data-stu-id="ccc08-111">The alternative was to make a ZIP file containing the template available and have the end-user create the required registry entries by hand.</span></span>

<span data-ttu-id="ccc08-112">上述两种方法都不是理想之选，因此我们决定利用[VSIX](https://msdn.microsoft.com/library/ff363239.aspx)扩展提供的一些现有基础结构，以便更轻松地创作、分发和安装自定义 mvc 模板（从针对 Visual Studio 2012 的 mvc 4 开始）。</span><span class="sxs-lookup"><span data-stu-id="ccc08-112">Neither of the aforementioned approaches is ideal so we decided to leverage some of the existing infrastructure provided by [VSIX](https://msdn.microsoft.com/library/ff363239.aspx) extensions to make it easier to author, distribute and install custom MVC templates starting with MVC 4 for Visual Studio 2012.</span></span> <span data-ttu-id="ccc08-113">此方法提供的一些优点包括：</span><span class="sxs-lookup"><span data-stu-id="ccc08-113">Some of the benefits provided by this approach are:</span></span>

- <span data-ttu-id="ccc08-114">VSIX 扩展可以包含多个支持不同语言（C#和 Visual Basic）和多个视图引擎（ASPX 和 Razor）的模板。</span><span class="sxs-lookup"><span data-stu-id="ccc08-114">A VSIX extension can contain multiple templates that support different languages (C# and Visual Basic) and multiple view engines (ASPX and Razor).</span></span>
- <span data-ttu-id="ccc08-115">VSIX 扩展可以面向 Visual Studio 的多个 Sku，包括 Express Sku。</span><span class="sxs-lookup"><span data-stu-id="ccc08-115">A VSIX extension can target multiple SKUs of Visual Studio including Express SKUs.</span></span>
- <span data-ttu-id="ccc08-116">[Visual Studio 库](https://visualstudiogallery.msdn.microsoft.com/)有助于将扩展分发给广大受众。</span><span class="sxs-lookup"><span data-stu-id="ccc08-116">The [Visual Studio Gallery](https://visualstudiogallery.msdn.microsoft.com/) facilitates distributing the extension to a wide audience.</span></span>
- <span data-ttu-id="ccc08-117">可以升级 VSIX 扩展，使你可以更轻松地为自定义模板创作更正和更新。</span><span class="sxs-lookup"><span data-stu-id="ccc08-117">VSIX extensions can be upgraded making it easier to author corrections and updates to your custom templates.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccc08-118">系统必备</span><span class="sxs-lookup"><span data-stu-id="ccc08-118">Prerequisites</span></span>

- <span data-ttu-id="ccc08-119">用户需要熟悉创作项目模板，包括必要的 .vstemplate 文件标记，等等。</span><span class="sxs-lookup"><span data-stu-id="ccc08-119">Users need to be familiar with authoring project templates, including the required markup for vstemplate files, etc.</span></span>
- <span data-ttu-id="ccc08-120">用户需要安装 Visual Studio Professional 和更高版本。</span><span class="sxs-lookup"><span data-stu-id="ccc08-120">Users will need to have Visual Studio Professional and higher installed.</span></span> <span data-ttu-id="ccc08-121">Express Sku 不支持创建 VSIX 项目。</span><span class="sxs-lookup"><span data-stu-id="ccc08-121">Express SKUs do not support creating VSIX projects.</span></span>
- <span data-ttu-id="ccc08-122">已安装[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) 。</span><span class="sxs-lookup"><span data-stu-id="ccc08-122">[Visual Studio 2012 SDK](https://www.microsoft.com/download/details.aspx?id=30668) installed.</span></span>

## <a name="example"></a><span data-ttu-id="ccc08-123">示例</span><span class="sxs-lookup"><span data-stu-id="ccc08-123">Example</span></span>

<span data-ttu-id="ccc08-124">第一步是使用C#或 Visual Basic 创建新的 VSIX 项目。</span><span class="sxs-lookup"><span data-stu-id="ccc08-124">The first step is to create a new VSIX project using either C# or Visual Basic.</span></span> <span data-ttu-id="ccc08-125">选择 "**文件" > "新建项目**"，然后单击左窗格中的 "**扩展性**"，然后选择 " **VSIX 项目**"。</span><span class="sxs-lookup"><span data-stu-id="ccc08-125">Select **File > New Project**, then click **Extensibility** in the left pane and select the **VSIX Project**.</span></span>

![新建项目](custom-mvc-templates/_static/image1.jpg)

<span data-ttu-id="ccc08-127">创建项目后，将打开 VSIX 设计器。</span><span class="sxs-lookup"><span data-stu-id="ccc08-127">After the project is created, the VSIX designer will be opened.</span></span>

![项目设计器元数据](custom-mvc-templates/_static/image2.jpg)

<span data-ttu-id="ccc08-129">设计器可用于编辑扩展的一些常规属性，这些属性将在用户安装扩展时向用户显示，或在 Visual Studio 中浏览已安装的扩展（**工具 > 扩展和更新**）。</span><span class="sxs-lookup"><span data-stu-id="ccc08-129">The designer can be used to edit some of the general properties of the extension that will be shown to users when they install the extension or browse the installed extensions in Visual Studio (**Tools > Extensions and Updates**).</span></span> <span data-ttu-id="ccc08-130">完成常规信息后，请单击 "**安装目标" 选项卡**。</span><span class="sxs-lookup"><span data-stu-id="ccc08-130">Once you have completed the general information click on the **Install Targets tab**.</span></span>

![项目设计器安装目标](custom-mvc-templates/_static/image3.jpg)

<span data-ttu-id="ccc08-132">此选项卡用于指定你的扩展所支持的 Visual Studio 的 Sku 和版本。</span><span class="sxs-lookup"><span data-stu-id="ccc08-132">This tab is used to specify the SKUs and versions of Visual Studio that are supported by your extension.</span></span> <span data-ttu-id="ccc08-133">选中 "为**所有用户安装此 VSIX**的复选框，以启用 vsix 的每计算机安装"。</span><span class="sxs-lookup"><span data-stu-id="ccc08-133">Select the checkbox for **This VSIX is installed for all users** to enable per-machine installs of the VSIX.</span></span> <span data-ttu-id="ccc08-134">单击右侧的 "**新建**" 按钮以添加其他 sku，如 Web Developer EXPRESS （VWD）。</span><span class="sxs-lookup"><span data-stu-id="ccc08-134">Click on the **New** button on the right to add additional SKUs such as Web Developer Express (VWD).</span></span>

![添加新的安装目标](custom-mvc-templates/_static/image4.jpg)

<span data-ttu-id="ccc08-136">如果你打算支持所有专业版和更高版本的 Sku （专业版、高级版和旗舰版），只需在家族**Microsoft.VisualStudio.Pro**中选择最低 SKU。</span><span class="sxs-lookup"><span data-stu-id="ccc08-136">If you intend to support all the Professional and higher SKUs (Professional, Premium and Ultimate) you only need to select the minimum SKU in the family, **Microsoft.VisualStudio.Pro**.</span></span> <span data-ttu-id="ccc08-137">完成安装目标后，请记得保存所有更改。</span><span class="sxs-lookup"><span data-stu-id="ccc08-137">Remember to save all your changes once you have completed the Install Targets.</span></span>

![项目设计器安装目标](custom-mvc-templates/_static/image5.jpg)

<span data-ttu-id="ccc08-139">"**资产**" 选项卡用于将所有内容文件添加到 VSIX 中。</span><span class="sxs-lookup"><span data-stu-id="ccc08-139">The **Assets** tab is used to add all your content files to the VSIX.</span></span> <span data-ttu-id="ccc08-140">由于 MVC 需要自定义元数据，你将编辑 VSIX 清单文件的原始 XML，而不是使用 "**资产**" 选项卡来添加内容。</span><span class="sxs-lookup"><span data-stu-id="ccc08-140">Since MVC requires custom metadata you will be editing the raw XML of the VSIX manifest file instead of using the **Assets** tab to add content.</span></span> <span data-ttu-id="ccc08-141">首先将模板内容添加到 VSIX 项目。</span><span class="sxs-lookup"><span data-stu-id="ccc08-141">Start by adding the template contents to the VSIX project.</span></span> <span data-ttu-id="ccc08-142">重要的是，文件夹的结构和内容反映了项目的布局。</span><span class="sxs-lookup"><span data-stu-id="ccc08-142">It is important that the structure of the folder and the contents mirror the layout of the project.</span></span> <span data-ttu-id="ccc08-143">下面的示例包含四个派生自基本 MVC 项目模板的项目模板。</span><span class="sxs-lookup"><span data-stu-id="ccc08-143">The example below contains four project templates that were derived from the Basic MVC project template.</span></span> <span data-ttu-id="ccc08-144">确保将包含项目模板的所有文件（ProjectTemplates 文件夹下的所有文件）添加到 VSIX 项目文件的**Content** itemgroup 中，并确保每个项包含**CopyToOutputDirectory**和**IncludeInVsix**元数据集，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="ccc08-144">Make sure that all the files that comprise your project template (everything underneath the ProjectTemplates folder) are added to the **Content** itemgroup in the VSIX project file and that each item contains the **CopyToOutputDirectory** and **IncludeInVsix** metadata set as shown in the example below.</span></span>

<span data-ttu-id="ccc08-145">&lt;Content Include =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span><span class="sxs-lookup"><span data-stu-id="ccc08-145">&lt;Content Include=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicWeb.config&quot;&gt;</span></span>

<span data-ttu-id="ccc08-146">&lt;CopyToOutputDirectory&gt;始终&lt;/CopyToOutputDirectory&gt;</span><span class="sxs-lookup"><span data-stu-id="ccc08-146">&lt;CopyToOutputDirectory&gt;Always&lt;/CopyToOutputDirectory&gt;</span></span>

<span data-ttu-id="ccc08-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span><span class="sxs-lookup"><span data-stu-id="ccc08-147">&lt;IncludeInVSIX&gt;true&lt;/IncludeInVSIX&gt;</span></span>

<span data-ttu-id="ccc08-148">&lt;/Content&gt;</span><span class="sxs-lookup"><span data-stu-id="ccc08-148">&lt;/Content&gt;</span></span>

<span data-ttu-id="ccc08-149">如果不是，则 IDE 将在生成 VSIX 时尝试编译模板的内容，并且可能会看到错误。</span><span class="sxs-lookup"><span data-stu-id="ccc08-149">If not, the IDE will try to compile the contents of the template when you build the VSIX and you will likely see an error.</span></span> <span data-ttu-id="ccc08-150">模板中的代码文件通常包含 Visual Studio 在实例化项目模板时使用的特殊[模板参数](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx)，因此无法在 IDE 中进行编译。</span><span class="sxs-lookup"><span data-stu-id="ccc08-150">Code files in templates often contain special [template parameters](https://msdn.microsoft.com/library/eehb4faa(v=vs.110).aspx) used by Visual Studio when the project template is instantiated and therefore cannot be compiled in the IDE.</span></span>

![“解决方案资源管理器”](custom-mvc-templates/_static/image6.jpg)

<span data-ttu-id="ccc08-152">关闭 VSIX 设计器，然后在**解决方案资源管理器**中右键单击**源文件**，然后选择 "**打开方式**" 并选择 " **XML （文本）编辑器**" 选项。</span><span class="sxs-lookup"><span data-stu-id="ccc08-152">Close the VSIX designer, then right click on the **source.extension.manifest** file in **Solution Explorer** and select **Open With** and choose the **XML (Text) Editor** option.</span></span>

![打开方式对话框](custom-mvc-templates/_static/image7.jpg)

<span data-ttu-id="ccc08-154">&gt;元素创建 **&lt;资产**，并为必须包括在 VSIX 中的每个文件添加 **&lt;资产&gt;** 元素。</span><span class="sxs-lookup"><span data-stu-id="ccc08-154">Create an **&lt;Assets&gt;** element and add an **&lt;Asset&gt;** element for each file that must be included in the VSIX.</span></span> <span data-ttu-id="ccc08-155">每个 **&lt;资产&gt;** 元素的**Type**属性必须设置为**VisualStudio**。</span><span class="sxs-lookup"><span data-stu-id="ccc08-155">The **Type** attribute of each **&lt;Asset&gt;** element must be set to **Microsoft.VisualStudio.Mvc.Template**.</span></span> <span data-ttu-id="ccc08-156">这是只有 MVC 项目向导理解的自定义命名空间。</span><span class="sxs-lookup"><span data-stu-id="ccc08-156">This is a custom namespace that only the MVC project wizard understands.</span></span> <span data-ttu-id="ccc08-157">有关清单文件的结构和布局的其他信息，请参阅 VSIX 2.0 架构文档。</span><span class="sxs-lookup"><span data-stu-id="ccc08-157">Refer to the VSIX 2.0 Schema documentation for additional information on the structure and layout of the manifest file.</span></span>

<span data-ttu-id="ccc08-158">只需将文件添加到 VSIX，就不能用 MVC 向导注册模板。</span><span class="sxs-lookup"><span data-stu-id="ccc08-158">Just adding the files to the VSIX is not sufficient to register the templates with the MVC wizard.</span></span> <span data-ttu-id="ccc08-159">你需要向 MVC 向导提供信息，如模板名称、说明、支持的视图引擎和编程语言。</span><span class="sxs-lookup"><span data-stu-id="ccc08-159">You need to provide information such as the template name, description, supported view engines and programming language to the MVC wizard.</span></span> <span data-ttu-id="ccc08-160">此信息在与每个 **.vstemplate**文件 **&lt;资产&gt;** 元素关联的自定义属性中执行。</span><span class="sxs-lookup"><span data-stu-id="ccc08-160">This information is carried in custom attributes associated with the **&lt;Asset&gt;** element for each **vstemplate** file.</span></span>

<span data-ttu-id="ccc08-161">&lt;资产 d:VsixSubPath =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-161">&lt;Asset d:VsixSubPath=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx&quot;</span></span>

<span data-ttu-id="ccc08-162">键入 =&quot;VisualStudio&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-162">Type=&quot;Microsoft.VisualStudio.Mvc.Template&quot;</span></span>

<span data-ttu-id="ccc08-163">d:Source =&quot;文件&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-163">d:Source=&quot;File&quot;</span></span>

<span data-ttu-id="ccc08-164">路径 =&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-164">Path=&quot;ProjectTemplates\MyMvcWebApplicationProjectTemplate.csaspx\BasicMvcWebApplicationProjectTemplate.11.csaspx.vstemplate&quot;</span></span>

<span data-ttu-id="ccc08-165">ProjectType =&quot;MVC&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-165">ProjectType=&quot;MVC&quot;</span></span>

<span data-ttu-id="ccc08-166">Language =&quot;C#&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-166">Language=&quot;C#&quot;</span></span>

<span data-ttu-id="ccc08-167">ViewEngine =&quot;Aspx&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-167">ViewEngine=&quot;Aspx&quot;</span></span>

<span data-ttu-id="ccc08-168">TemplateId =&quot;MyMvcApplication&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-168">TemplateId=&quot;MyMvcApplication&quot;</span></span>

<span data-ttu-id="ccc08-169">标题 =&quot;自定义基本 Web 应用程序&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-169">Title=&quot;Custom Basic Web Application&quot;</span></span>

<span data-ttu-id="ccc08-170">Description =&quot;从基本 MVC web 应用程序（Razor）派生的自定义模板&quot;</span><span class="sxs-lookup"><span data-stu-id="ccc08-170">Description=&quot;A custom template derived from a Basic MVC web application (Razor)&quot;</span></span>

<span data-ttu-id="ccc08-171">版本 =&quot;4.0&quot;/&gt;</span><span class="sxs-lookup"><span data-stu-id="ccc08-171">Version=&quot;4.0&quot;/&gt;</span></span>

<span data-ttu-id="ccc08-172">下面是必须存在的自定义属性的说明：</span><span class="sxs-lookup"><span data-stu-id="ccc08-172">Below is an explanation of the custom attributes that must be present:</span></span>

- <span data-ttu-id="ccc08-173">**ProjectType**必须设置为 MVC。</span><span class="sxs-lookup"><span data-stu-id="ccc08-173">**ProjectType** must be set to MVC.</span></span>
- <span data-ttu-id="ccc08-174">**Language**指定模板支持的开发语言。</span><span class="sxs-lookup"><span data-stu-id="ccc08-174">**Language** designates the development language supported by the template.</span></span> <span data-ttu-id="ccc08-175">有效值为C#或 VB。</span><span class="sxs-lookup"><span data-stu-id="ccc08-175">Valid values are either C# or VB.</span></span>
- <span data-ttu-id="ccc08-176">**ViewEngine**指定模板支持的视图引擎，如 Aspx 或 Razor。</span><span class="sxs-lookup"><span data-stu-id="ccc08-176">**ViewEngine** designates the view engine supported by the template such as Aspx or Razor.</span></span> <span data-ttu-id="ccc08-177">您可以为此字段指定自定义值。</span><span class="sxs-lookup"><span data-stu-id="ccc08-177">You can specify a custom value for this field.</span></span>
- <span data-ttu-id="ccc08-178">**TemplateId**用于将模板分组。</span><span class="sxs-lookup"><span data-stu-id="ccc08-178">**TemplateId** is used for grouping the templates.</span></span> <span data-ttu-id="ccc08-179">如果该值与现有的模板 ID 相匹配，则它将替代以前使用 MVC 向导注册的模板。</span><span class="sxs-lookup"><span data-stu-id="ccc08-179">If the value matches an existing template ID it will be override templates previously registered with the MVC wizard.</span></span>
- <span data-ttu-id="ccc08-180">**Title**指定在每个项目模板下的 MVC 向导中显示的简短说明。</span><span class="sxs-lookup"><span data-stu-id="ccc08-180">**Title** designates the short description displayed in the MVC wizard beneath each project template.</span></span>
- <span data-ttu-id="ccc08-181">**Description**指定模板的更详细说明。</span><span class="sxs-lookup"><span data-stu-id="ccc08-181">**Description** designates a more verbose description of the template.</span></span>

<span data-ttu-id="ccc08-182">将所有文件添加到清单并保存后，你会注意到，设计器中的 "**资产**" 选项卡将显示所有文件，而不是添加到 " **&lt;资产**" 的自定义属性&gt; **.vstemplate**文件的元素。</span><span class="sxs-lookup"><span data-stu-id="ccc08-182">After you have added all the files to the manifest and saved it, you will notice that the **Assets** tab in the designer will display all the files, but not the custom attributes you added to the **&lt;Asset&gt;** elements for the **vstemplate** files.</span></span>

![项目设计器资产](custom-mvc-templates/_static/image8.jpg)

<span data-ttu-id="ccc08-184">现在剩下的就是编译并安装 VSIX 项目。</span><span class="sxs-lookup"><span data-stu-id="ccc08-184">All that remains now is to compile the VSIX project and install it.</span></span>

<span data-ttu-id="ccc08-185">请确保 Visual Studio 的所有实例在要测试 VSIX 扩展的计算机上关闭。</span><span class="sxs-lookup"><span data-stu-id="ccc08-185">Make sure that all instances of Visual Studio are closed on the machine where you intend to test the VSIX extension.</span></span> <span data-ttu-id="ccc08-186">Visual Studio 将在启动过程中扫描新扩展，因此，如果在安装 VSIX 时 IDE 处于打开状态，则需要重启 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ccc08-186">Visual Studio scans for new extensions during startup, so if the IDE is open while installing a VSIX you will need to restart Visual Studio.</span></span> <span data-ttu-id="ccc08-187">在 "资源管理器" 中，双击 VSIX 文件以启动**Vsix 安装程序**，单击 "**安装**"，并启动 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="ccc08-187">In Explorer, double click on the VSIX file to launch the **VSIX Installer**, click **Install** and then launch Visual Studio.</span></span>

![VSIX 安装程序](custom-mvc-templates/_static/image9.jpg)

<span data-ttu-id="ccc08-189">从菜单中选择 "**工具" > "扩展和更新**" 以确认你的扩展已安装。</span><span class="sxs-lookup"><span data-stu-id="ccc08-189">From the menu, select **Tools > Extensions and Updates** to confirm that your extension was installed.</span></span> <span data-ttu-id="ccc08-190">如果在安装扩展期间，VSIX 安装程序报告了任何错误，则可以查看 VSIX 安装程序日志以获取详细信息。</span><span class="sxs-lookup"><span data-stu-id="ccc08-190">If the VSIX Installer reported any errors during the installation of the extension you can view the VSIX Installer log for more information.</span></span> <span data-ttu-id="ccc08-191">通常会在安装了扩展的用户的 **% temp%** 文件夹中创建日志，例如**C:\Users\Bob\AppData\Local\Temp**。</span><span class="sxs-lookup"><span data-stu-id="ccc08-191">The log is usually created in the **%temp%** folder of the user that installed the extension, for example **C:\Users\Bob\AppData\Local\Temp**.</span></span>

![扩展和更新](custom-mvc-templates/_static/image10.jpg)

<span data-ttu-id="ccc08-193">关闭窗口后，可以创建 MVC 4 项目，以查看新模板是否显示在 MVC 向导中。</span><span class="sxs-lookup"><span data-stu-id="ccc08-193">After closing the window you can create an MVC 4 project to see whether your new templates are shown in the MVC wizard.</span></span>

![新的 ASP.NET MVC 4 项目](custom-mvc-templates/_static/image11.jpg)

## <a name="limitations"></a><span data-ttu-id="ccc08-195">限制</span><span class="sxs-lookup"><span data-stu-id="ccc08-195">Limitations</span></span>

1. <span data-ttu-id="ccc08-196">MVC 向导不支持本地化的自定义模板。</span><span class="sxs-lookup"><span data-stu-id="ccc08-196">The MVC wizard does not support localized custom templates.</span></span>
2. <span data-ttu-id="ccc08-197">如果向导找不到自定义模板，则不会报告任何错误。</span><span class="sxs-lookup"><span data-stu-id="ccc08-197">The wizard will not report any errors if it fails to locate custom templates.</span></span> <span data-ttu-id="ccc08-198">如果缺少任何必需的自定义属性，该模板将直接从向导中排除。</span><span class="sxs-lookup"><span data-stu-id="ccc08-198">If any of the required custom attributes are absent, the template would simply be excluded from the Wizard.</span></span>
