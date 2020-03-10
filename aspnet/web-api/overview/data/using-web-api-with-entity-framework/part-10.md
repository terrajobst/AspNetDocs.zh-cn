---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: 将应用发布到 Azure Azure App Service |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504758"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a><span data-ttu-id="4b545-102">将应用发布到 Azure Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4b545-102">Publish the App to Azure Azure App Service</span></span>

<span data-ttu-id="4b545-103">作者： [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4b545-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="4b545-104">下载完成的项目</span><span class="sxs-lookup"><span data-stu-id="4b545-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="4b545-105">最后一步是将应用程序发布到 Azure。</span><span class="sxs-lookup"><span data-stu-id="4b545-105">As the last step, you will publish the application to Azure.</span></span> <span data-ttu-id="4b545-106">在解决方案资源管理器中，右键单击项目，然后选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="4b545-106">In Solution Explorer, right-click the project and select **Publish**.</span></span>

![](part-10/_static/image1.png)

<span data-ttu-id="4b545-107">单击 "**发布**" 将调用 "**发布 Web** " 对话框。</span><span class="sxs-lookup"><span data-stu-id="4b545-107">Clicking **Publish** invokes the **Publish Web** dialog.</span></span> <span data-ttu-id="4b545-108">如果在首次创建项目时选中了 "**在云中托管**"，则已配置连接和设置。</span><span class="sxs-lookup"><span data-stu-id="4b545-108">If you checked **Host in Cloud** when you first created the project, then the connection and settings are already configured.</span></span> <span data-ttu-id="4b545-109">在这种情况下，只需单击 "**设置**" 选项卡并选中 &quot;执行 Code First 迁移&quot;"。</span><span class="sxs-lookup"><span data-stu-id="4b545-109">In that case, just click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="4b545-110">（如果你未在云中检查 "在**云中托管**"，请按照[下一节](#new-website)中的步骤进行操作。）</span><span class="sxs-lookup"><span data-stu-id="4b545-110">(If you didn't check **Host in Cloud** at the beginning, then follow the steps in the [next section](#new-website).)</span></span>

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

<span data-ttu-id="4b545-111">若要部署应用，请单击 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="4b545-111">To deploy the app, click **Publish**.</span></span> <span data-ttu-id="4b545-112">您可以在 " **Web 发布活动**" 窗口中查看发布进度。</span><span class="sxs-lookup"><span data-stu-id="4b545-112">You can view the publishing progress in the **Web Publish Activity** window.</span></span> <span data-ttu-id="4b545-113">（从 "**视图**" 菜单中选择 "**其他窗口**"，然后选择 " **Web 发布活动**"。）</span><span class="sxs-lookup"><span data-stu-id="4b545-113">(From the **View** menu, select **Other Windows**, then select **Web Publish Activity**.)</span></span>

![](part-10/_static/image4.png)

<span data-ttu-id="4b545-114">当 Visual Studio 完成应用程序部署时，默认浏览器会自动打开到已部署网站的 URL，你创建的应用程序现在正在云中运行。</span><span class="sxs-lookup"><span data-stu-id="4b545-114">When Visual Studio finishes deploying the app, the default browser automatically opens to the URL of the deployed website, and the application that you created is now running in the cloud.</span></span> <span data-ttu-id="4b545-115">浏览器地址栏中的 URL 显示正在从 Internet 加载该站点。</span><span class="sxs-lookup"><span data-stu-id="4b545-115">The URL in the browser address bar shows that the site is being loaded from the Internet.</span></span>

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a><span data-ttu-id="4b545-116">部署到新网站</span><span class="sxs-lookup"><span data-stu-id="4b545-116">Deploying to a New Website</span></span>

<span data-ttu-id="4b545-117">如果在首次创建项目时未选中 "**在云中托管**"，则可以立即配置新的 web 应用。</span><span class="sxs-lookup"><span data-stu-id="4b545-117">If you did not check **Host in Cloud** when you first created the project, you can configure a new web app now.</span></span> <span data-ttu-id="4b545-118">在解决方案资源管理器中，右键单击项目，然后选择 "**发布**"。</span><span class="sxs-lookup"><span data-stu-id="4b545-118">In Solution Explorer, right-click the project and select **Publish**.</span></span> <span data-ttu-id="4b545-119">选择 "**配置文件**" 选项卡，然后单击 " **Microsoft Azure 网站**"。</span><span class="sxs-lookup"><span data-stu-id="4b545-119">Select the **Profile** tab and click **Microsoft Azure Websites**.</span></span> <span data-ttu-id="4b545-120">如果你当前未登录到 Azure，系统将提示你登录。</span><span class="sxs-lookup"><span data-stu-id="4b545-120">If you aren't currently signed in to Azure, you will be prompted to sign in.</span></span>

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

<span data-ttu-id="4b545-121">在 "**现有网站**" 对话框中，单击 "**新建**"。</span><span class="sxs-lookup"><span data-stu-id="4b545-121">In the **Existing Websites** dialog, click **New**.</span></span>

![](part-10/_static/image9.png)

<span data-ttu-id="4b545-122">输入站点名称。</span><span class="sxs-lookup"><span data-stu-id="4b545-122">Enter a site name.</span></span> <span data-ttu-id="4b545-123">选择 Azure 订阅和区域。</span><span class="sxs-lookup"><span data-stu-id="4b545-123">Select your Azure subscription and the region.</span></span> <span data-ttu-id="4b545-124">在 "**数据库服务器**" 下，选择 "**创建新服务器**"，或选择现有服务器。</span><span class="sxs-lookup"><span data-stu-id="4b545-124">Under **Database server**, select **Create New Server**, or select an existing server.</span></span> <span data-ttu-id="4b545-125">单击 **“创建”** 。</span><span class="sxs-lookup"><span data-stu-id="4b545-125">Click **Create**.</span></span>

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

<span data-ttu-id="4b545-126">单击 "**设置**" 选项卡，检查 &quot;"执行 Code First 迁移&quot;"。</span><span class="sxs-lookup"><span data-stu-id="4b545-126">Click the **Settings** tab and check &quot;Execute Code First Migrations&quot;.</span></span> <span data-ttu-id="4b545-127">然后单击“发布”。</span><span class="sxs-lookup"><span data-stu-id="4b545-127">Then click **Publish**.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4b545-128">上一页</span><span class="sxs-lookup"><span data-stu-id="4b545-128">Previous</span></span>](part-9.md)
