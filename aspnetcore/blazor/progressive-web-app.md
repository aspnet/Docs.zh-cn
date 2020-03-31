---
title: 利用 ASP.NET Core Blazor WebAssembly 生成渐进式 Web 应用程序
author: guardrex
description: 了解如何生成基于 Blazor 的渐进式 Web 应用 (PWA)，这类应用使用新式浏览器功能，与桌面应用行为一致。
monikerRange: '>= aspnetcore-3.1'
ms.author: riande
ms.custom: mvc
ms.date: 03/23/2020
no-loc:
- Blazor
- SignalR
uid: blazor/progressive-web-app
ms.openlocfilehash: fe69e51aefae9c80e5bb4b78151d384ce25d41a7
ms.sourcegitcommit: 91dc1dd3d055b4c7d7298420927b3fd161067c64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "80218942"
---
# <a name="build-progressive-web-applications-with-aspnet-core-blazor-webassembly"></a><span data-ttu-id="e0d60-103">利用 ASP.NET Core Blazor WebAssembly 生成渐进式 Web 应用</span><span class="sxs-lookup"><span data-stu-id="e0d60-103">Build Progressive Web Applications with ASP.NET Core Blazor WebAssembly</span></span>

<span data-ttu-id="e0d60-104">作者：[Steve Sanderson](https://github.com/SteveSandersonMS)</span><span class="sxs-lookup"><span data-stu-id="e0d60-104">By [Steve Sanderson](https://github.com/SteveSandersonMS)</span></span>

[!INCLUDE[](~/includes/blazorwasm-preview-notice.md)]

[!INCLUDE[](~/includes/blazorwasm-3.2-template-article-notice.md)]

<span data-ttu-id="e0d60-105">渐进式 Web 应用 (PWA) 是一种单页应用程序 (SPA)，它使用新式浏览器 API 和功能以表现得如桌面应用。</span><span class="sxs-lookup"><span data-stu-id="e0d60-105">A Progressive Web Application (PWA) is a Single Page Application (SPA) that uses modern browser APIs and capabilities to behave like a desktop app.</span></span> <span data-ttu-id="e0d60-106">Blazor WebAssembly 是基于标准的客户端 Web 应用平台，因此它可以使用任何浏览器 API，包括以下功能所需的 PWA API：</span><span class="sxs-lookup"><span data-stu-id="e0d60-106">Blazor WebAssembly is a standards-based client-side web app platform, so it can use any browser API, including PWA APIs required for the following capabilities:</span></span>

* <span data-ttu-id="e0d60-107">脱机工作并即时加载（不受网络速度影响）。</span><span class="sxs-lookup"><span data-stu-id="e0d60-107">Working offline and loading instantly, independent of network speed.</span></span>
* <span data-ttu-id="e0d60-108">在自己的应用窗口中运行，而不仅仅是在浏览器窗口中运行。</span><span class="sxs-lookup"><span data-stu-id="e0d60-108">Running in its own app window, not just a browser window.</span></span>
* <span data-ttu-id="e0d60-109">从主机操作系统的开始菜单、扩展坞或主屏幕启动。</span><span class="sxs-lookup"><span data-stu-id="e0d60-109">Being launched from the host's operating system start menu, dock, or home screen.</span></span>
* <span data-ttu-id="e0d60-110">从后端服务器接收推送通知，即使用户没有在使用该应用。</span><span class="sxs-lookup"><span data-stu-id="e0d60-110">Receiving push notifications from a backend server, even while the user isn't using the app.</span></span>
* <span data-ttu-id="e0d60-111">在后台自动更新。</span><span class="sxs-lookup"><span data-stu-id="e0d60-111">Automatically updating in the background.</span></span>

<span data-ttu-id="e0d60-112">使用“渐进式”一词来描述此类应用的原因如下  ：</span><span class="sxs-lookup"><span data-stu-id="e0d60-112">The word *progressive* is used to describe such apps because:</span></span>

* <span data-ttu-id="e0d60-113">用户可能先是在其网络浏览器中发现应用并使用它，就像任何其他单页应用程序一样。</span><span class="sxs-lookup"><span data-stu-id="e0d60-113">A user might first discover and use the app within their web browser like any other SPA.</span></span>
* <span data-ttu-id="e0d60-114">过了一段时间后，用户进而将其安装到操作系统中并启用推送通知。</span><span class="sxs-lookup"><span data-stu-id="e0d60-114">Later, the user progresses to installing it in their OS and enabling push notifications.</span></span>

## <a name="create-a-project-from-the-pwa-template"></a><span data-ttu-id="e0d60-115">通过 PWA 模板创建项目</span><span class="sxs-lookup"><span data-stu-id="e0d60-115">Create a project from the PWA template</span></span>

# <a name="visual-studio"></a>[<span data-ttu-id="e0d60-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e0d60-116">Visual Studio</span></span>](#tab/visual-studio)

<span data-ttu-id="e0d60-117">在“新建项目”对话框中创建新的“Blazor WebAssembly 应用”时，请选中“进度 Web 应用”复选框    ：</span><span class="sxs-lookup"><span data-stu-id="e0d60-117">When creating a new **Blazor WebAssembly App** in the **Create a New Project** dialog, select the **Progress Web Application** check box:</span></span>

![Visual Studio 的“新建项目”对话框中选中“渐进式 Web 应用”复选框。](progressive-web-app/_static/image1.png)

<!--

# [Visual Studio for Mac](#tab/visual-studio-mac)

-->

# <a name="visual-studio-code--net-core-cli"></a>[<span data-ttu-id="e0d60-119">Visual Studio Code/.NET Core CLI</span><span class="sxs-lookup"><span data-stu-id="e0d60-119">Visual Studio Code / .NET Core CLI</span></span>](#tab/visual-studio-code+netcore-cli)

<span data-ttu-id="e0d60-120">使用 `--pwa` 开关在命令 shell 中创建 PWA 项目：</span><span class="sxs-lookup"><span data-stu-id="e0d60-120">Create a PWA project in a command shell with the `--pwa` switch:</span></span>

```dotnetcli
dotnet new blazorwasm -o MyNewProject --pwa
```

---

<span data-ttu-id="e0d60-121">（可选）可以为通过 ASP.NET Core 托管的模板创建的应用配置 PWA。</span><span class="sxs-lookup"><span data-stu-id="e0d60-121">Optionally, PWA can be configured for an app created from the ASP.NET Core Hosted template.</span></span> <span data-ttu-id="e0d60-122">PWA 方案独立于托管模型。</span><span class="sxs-lookup"><span data-stu-id="e0d60-122">The PWA scenario is independent of the hosting model.</span></span>

## <a name="installation-and-app-manifest"></a><span data-ttu-id="e0d60-123">安装和应用部件清单 (manifest)</span><span class="sxs-lookup"><span data-stu-id="e0d60-123">Installation and app manifest</span></span>

<span data-ttu-id="e0d60-124">访问使用 PWA 模板创建的应用时，用户可以选择将应用安装到其 OS 的开始菜单、扩展坞或主屏幕。</span><span class="sxs-lookup"><span data-stu-id="e0d60-124">When visiting an app created using the PWA template, users have the option of installing the app into their OS's start menu, dock, or home screen.</span></span> <span data-ttu-id="e0d60-125">此选项的显示方式取决于用户的浏览器。</span><span class="sxs-lookup"><span data-stu-id="e0d60-125">The way this option is presented depends on the user's browser.</span></span> <span data-ttu-id="e0d60-126">使用基于桌面 Chromium 的浏览器（如 Edge 或 Chrome）时，URL 栏中会出现“添加”按钮  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-126">When using desktop Chromium-based browsers, such as Edge or Chrome, an **Add** button appears within the URL bar.</span></span> <span data-ttu-id="e0d60-127">用户选择“添加”按钮后，他们将收到一个确认对话框  ：</span><span class="sxs-lookup"><span data-stu-id="e0d60-127">After the user selects the **Add** button, they receive a confirmation dialog:</span></span>

![Google Chrome 中的确认对话框会向用户显示“MyBlazorPwa”应用的“安装”按钮。](progressive-web-app/_static/image2.png)

<span data-ttu-id="e0d60-129">在 iOS 上，访问者可以通过 Safari 的“共享”按钮和“添加到主屏幕”选项安装 PWA   。</span><span class="sxs-lookup"><span data-stu-id="e0d60-129">On iOS, visitors can install the PWA using Safari's **Share** button and its **Add to Homescreen** option.</span></span> <span data-ttu-id="e0d60-130">在适用于 Android 的 Chrome 上，用户应该选择右上角的“菜单”按钮，然后选择“添加到主屏幕”   。</span><span class="sxs-lookup"><span data-stu-id="e0d60-130">On Chrome for Android, users should select the **Menu** button in the upper-right corner, followed by **Add to Home screen**.</span></span>

<span data-ttu-id="e0d60-131">安装后，应用将显示在其自己的窗口中，没有任何地址栏：</span><span class="sxs-lookup"><span data-stu-id="e0d60-131">Once installed, the app appears in its own window without an address bar:</span></span>

![“MyBlazorPwa”应用在 Google Chrome 中运行时不显示地址栏。](progressive-web-app/_static/image3.png)

<span data-ttu-id="e0d60-133">若要自定义窗口的标题、配色方案、图标或其他详细信息，请参阅项目 wwwroot 目录中的 manifest.json 文件   。</span><span class="sxs-lookup"><span data-stu-id="e0d60-133">To customize the window's title, color scheme, icon, or other details, see the *manifest.json* file in the project's *wwwroot* directory.</span></span> <span data-ttu-id="e0d60-134">此文件的架构由 Web 标准定义。</span><span class="sxs-lookup"><span data-stu-id="e0d60-134">The schema of this file is defined by web standards.</span></span> <span data-ttu-id="e0d60-135">有关详细信息，请参阅 [MDN Web 文档：Web 应用部件清单](https://developer.mozilla.org/docs/Web/Manifest)。</span><span class="sxs-lookup"><span data-stu-id="e0d60-135">For more information, see [MDN web docs: Web App Manifest](https://developer.mozilla.org/docs/Web/Manifest).</span></span>

## <a name="offline-support"></a><span data-ttu-id="e0d60-136">脱机支持</span><span class="sxs-lookup"><span data-stu-id="e0d60-136">Offline support</span></span>

<span data-ttu-id="e0d60-137">默认情况下，使用 PWA 模板选项创建的应用支持脱机运行。</span><span class="sxs-lookup"><span data-stu-id="e0d60-137">By default, apps created using the PWA template option have support for running offline.</span></span> <span data-ttu-id="e0d60-138">用户首次访问该应用时需要联机访问。</span><span class="sxs-lookup"><span data-stu-id="e0d60-138">A user must first visit the app while they're online.</span></span> <span data-ttu-id="e0d60-139">浏览器会自动下载并缓存脱机操作所需的所有资源。</span><span class="sxs-lookup"><span data-stu-id="e0d60-139">The browser automatically downloads and caches all of the resources required to operate offline.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0d60-140">开发支持会干扰常规开发周期（进行更改和测试更改）。</span><span class="sxs-lookup"><span data-stu-id="e0d60-140">Development support would interfere with the usual development cycle of making changes and testing them.</span></span> <span data-ttu-id="e0d60-141">因此，脱机支持只对已发布的应用启用  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-141">Therefore, offline support is only enabled for *published* apps.</span></span> 

> [!WARNING]
> <span data-ttu-id="e0d60-142">如果打算分发启用脱机的 PWA，则存在[几个重要的警告和注意事项](#caveats-for-offline-pwas)。</span><span class="sxs-lookup"><span data-stu-id="e0d60-142">If you intend to distribute an offline-enabled PWA, there are [several important warnings and caveats](#caveats-for-offline-pwas).</span></span> <span data-ttu-id="e0d60-143">这些方案是脱机 PWA 所固有的，而不是特定于 Blazor。</span><span class="sxs-lookup"><span data-stu-id="e0d60-143">These scenarios are inherent to offline PWAs and not specific to Blazor.</span></span> <span data-ttu-id="e0d60-144">在对启用了脱机的应用的工作方式做出假设之前，请务必阅读并了解这些注意事项。</span><span class="sxs-lookup"><span data-stu-id="e0d60-144">Be sure to read and understand these caveats before making assumptions about how your offline-enabled app will work.</span></span>

<span data-ttu-id="e0d60-145">了解脱机支持的运行原理：</span><span class="sxs-lookup"><span data-stu-id="e0d60-145">To see how offline support works:</span></span>

1. <span data-ttu-id="e0d60-146">发布应用。</span><span class="sxs-lookup"><span data-stu-id="e0d60-146">Publish the app.</span></span> <span data-ttu-id="e0d60-147">有关详细信息，请参阅 <xref:host-and-deploy/blazor/index#publish-the-app>。</span><span class="sxs-lookup"><span data-stu-id="e0d60-147">For more information, see <xref:host-and-deploy/blazor/index#publish-the-app>.</span></span>
1. <span data-ttu-id="e0d60-148">将应用部署到支持 HTTPS 的服务器，并在浏览器中通过安全的 HTTPS 地址访问应用。</span><span class="sxs-lookup"><span data-stu-id="e0d60-148">Deploy the app to a server that supports HTTPS, and access the app in a browser at its secure HTTPS address.</span></span>
1. <span data-ttu-id="e0d60-149">打开浏览器的开发工具，并在“应用程序”选项卡上验证是否为主机注册了“服务工作进程”   ：</span><span class="sxs-lookup"><span data-stu-id="e0d60-149">Open the browser's dev tools and verify that a *Service Worker* is registered for the host on the **Application** tab:</span></span>

   ![Google Chrome 开发者工具的“应用程序”选项卡显示一个已激活且正在运行的服务工作进程。](progressive-web-app/_static/image4.png)

1. <span data-ttu-id="e0d60-151">重载页面并检查“网络”选项卡  。“服务工作进程”或“内存缓存”作为页面所有资产的源列出   ：</span><span class="sxs-lookup"><span data-stu-id="e0d60-151">Reload the page and examine the **Network** tab. **Service Worker** or **memory cache** are listed as the sources for all of the page's assets:</span></span>

   ![Google Chrome 开发者工具的“网络”选项卡，显示了页面所有资产的源。](progressive-web-app/_static/image5.png)

1. <span data-ttu-id="e0d60-153">要验证浏览器是否不依赖网络访问来加载应用，请执行以下任一操作：</span><span class="sxs-lookup"><span data-stu-id="e0d60-153">To verify that the browser isn't dependent on network access to load the app, either:</span></span>

   * <span data-ttu-id="e0d60-154">关闭 Web 服务器，并查看应用如何继续正常运行，包括页面重载。</span><span class="sxs-lookup"><span data-stu-id="e0d60-154">Shut down the web server and see how the app continues to function normally, which includes page reloads.</span></span> <span data-ttu-id="e0d60-155">同样，当网络连接速度缓慢时，应用仍可正常运行。</span><span class="sxs-lookup"><span data-stu-id="e0d60-155">Likewise, the app continues to function normally when there's a slow network connection.</span></span>
   * <span data-ttu-id="e0d60-156">指示浏览器模拟“网络”选项卡中的脱机模式  ：</span><span class="sxs-lookup"><span data-stu-id="e0d60-156">Instruct the browser to simulate offline mode in the **Network** tab:</span></span>

   ![Google Chrome 开发者工具的“网络”选项卡，其中浏览器模式下拉菜单从“联机”更改为“脱机”。](progressive-web-app/_static/image6.png)

<span data-ttu-id="e0d60-158">使用服务工作进程的脱机支持是一项 Web 标准，并非特定于 Blazor。</span><span class="sxs-lookup"><span data-stu-id="e0d60-158">Offline support using a service worker is a web standard, not specific to Blazor.</span></span> <span data-ttu-id="e0d60-159">有关服务工作进程的详细信息，请参阅 [MDN Web文档：服务工作进程 API](https://developer.mozilla.org/docs/Web/API/Service_Worker_API)。</span><span class="sxs-lookup"><span data-stu-id="e0d60-159">For more information on service workers, see [MDN web docs: Service Worker API](https://developer.mozilla.org/docs/Web/API/Service_Worker_API).</span></span> <span data-ttu-id="e0d60-160">要了解有关服务工作进程常见使用模式的详细信息，请参阅 [Google Web：服务工作进程生命周期](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle)。</span><span class="sxs-lookup"><span data-stu-id="e0d60-160">To learn more about common usage patterns for service workers, see [Google Web: The Service Worker Lifecycle](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle).</span></span>

Blazor<span data-ttu-id="e0d60-161"> 的 PWA 模板产生两个服务工作进程文件：</span><span class="sxs-lookup"><span data-stu-id="e0d60-161">'s PWA template produces two service worker files:</span></span>

* <span data-ttu-id="e0d60-162">在开发过程中使用的 wwwroot/service-worker.js  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-162">*wwwroot/service-worker.js*, which is used during development.</span></span>
* <span data-ttu-id="e0d60-163">在发布应用后使用的 wwwroot/service-worker.published.js  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-163">*wwwroot/service-worker.published.js*, which is used after the app is published.</span></span>

<span data-ttu-id="e0d60-164">要在两个服务工作进程文件之间共享逻辑，请考虑使用以下方法：</span><span class="sxs-lookup"><span data-stu-id="e0d60-164">To share logic between the two service worker files, consider the following approach:</span></span>

* <span data-ttu-id="e0d60-165">添加第三个 JavaScript 文件来保存通用逻辑。</span><span class="sxs-lookup"><span data-stu-id="e0d60-165">Add a third JavaScript file to hold the common logic.</span></span>
* <span data-ttu-id="e0d60-166">使用 [self.importScripts](https://developer.mozilla.org/docs/Web/API/WorkerGlobalScope/importScripts) 将通用逻辑同时加载到两个服务工作进程文件中。</span><span class="sxs-lookup"><span data-stu-id="e0d60-166">Use [self.importScripts](https://developer.mozilla.org/docs/Web/API/WorkerGlobalScope/importScripts) to load the common logic into both service worker files.</span></span>

### <a name="cache-first-fetch-strategy"></a><span data-ttu-id="e0d60-167">缓存优先提取策略</span><span class="sxs-lookup"><span data-stu-id="e0d60-167">Cache-first fetch strategy</span></span>

<span data-ttu-id="e0d60-168">内置 service-worker.published.js 服务工作进程使用“缓存优先”策略来解析请求   。</span><span class="sxs-lookup"><span data-stu-id="e0d60-168">The built-in *service-worker.published.js* service worker resolves requests using a *cache-first* strategy.</span></span> <span data-ttu-id="e0d60-169">这意味着，无论用户是否有网络访问权限或服务器上是否有更新的内容，服务工作进程始终优先返回缓存的内容。</span><span class="sxs-lookup"><span data-stu-id="e0d60-169">This means that the service worker prefers to return cached content, regardless of whether the user has network access or newer content is available on the server.</span></span>

<span data-ttu-id="e0d60-170">缓存优先策略非常有用，因为：</span><span class="sxs-lookup"><span data-stu-id="e0d60-170">The cache-first strategy is valuable because:</span></span>

* <span data-ttu-id="e0d60-171">它可确保可靠性。 </span><span class="sxs-lookup"><span data-stu-id="e0d60-171">**It ensures reliability.**</span></span> <span data-ttu-id="e0d60-172">&ndash; 网络访问不是布尔状态。</span><span class="sxs-lookup"><span data-stu-id="e0d60-172">&ndash; Network access isn't a boolean state.</span></span> <span data-ttu-id="e0d60-173">用户不只是“联机”或“脱机”：</span><span class="sxs-lookup"><span data-stu-id="e0d60-173">A user isn't simply online or offline:</span></span>

  * <span data-ttu-id="e0d60-174">用户的设备可能假设它处于联机状态，但可能由于网络速度太慢，根本无法加载。</span><span class="sxs-lookup"><span data-stu-id="e0d60-174">The user's device may assume it's online, but the network might be so slow as to be impractical to wait for.</span></span>
  * <span data-ttu-id="e0d60-175">网络可能会对某些 URL 返回无效结果（例如，当有一个强制 WIFI 门户当前正在阻止或重定向某些请求时）。</span><span class="sxs-lookup"><span data-stu-id="e0d60-175">The network might return invalid results for certain URLs, such as when there's a captive WIFI portal that's currently blocking or redirecting certain requests.</span></span>
  
  <span data-ttu-id="e0d60-176">这就是浏览器的 `navigator.onLine` API 不可靠并且不应依赖的原因。</span><span class="sxs-lookup"><span data-stu-id="e0d60-176">This is why the browser's `navigator.onLine` API isn't reliable and shouldn't be depended upon.</span></span>

* <span data-ttu-id="e0d60-177">它可确保正确性。 </span><span class="sxs-lookup"><span data-stu-id="e0d60-177">**It ensures correctness.**</span></span> <span data-ttu-id="e0d60-178">&ndash; 在生成脱机资源的缓存时，服务工作进程使用内容哈希，确保它在某个时刻提取了完整且自身一致的资源快照。</span><span class="sxs-lookup"><span data-stu-id="e0d60-178">&ndash; When building a cache of offline resources, the service worker uses content hashing to guarantee it has fetched a complete and self-consistent snapshot of resources at a single instant in time.</span></span> <span data-ttu-id="e0d60-179">此缓存随后用作原子单元。</span><span class="sxs-lookup"><span data-stu-id="e0d60-179">This cache is then used as an atomic unit.</span></span> <span data-ttu-id="e0d60-180">没有必要向网络请求更新的资源，因为需要的版本已经缓存了。</span><span class="sxs-lookup"><span data-stu-id="e0d60-180">There's no point asking the network for newer resources, since the only versions required are the ones already cached.</span></span> <span data-ttu-id="e0d60-181">其他任何版本都会产生不一致和不兼容的风险（例如，尝试使用未一起编译的 .NET 程序集的版本）。</span><span class="sxs-lookup"><span data-stu-id="e0d60-181">Anything else risks inconsistency and incompatibility (for example, trying to use versions of .NET assemblies that weren't compiled together).</span></span>

### <a name="background-updates"></a><span data-ttu-id="e0d60-182">后台更新</span><span class="sxs-lookup"><span data-stu-id="e0d60-182">Background updates</span></span>

<span data-ttu-id="e0d60-183">作为一种思维模型，你可以将脱机优先 PWA 的行为视为与可安装的移动应用类似。</span><span class="sxs-lookup"><span data-stu-id="e0d60-183">As a mental model, you can think of an offline-first PWA as behaving like a mobile app that can be installed.</span></span> <span data-ttu-id="e0d60-184">无论网络连接情况如何，应用都会立即启动，但是已安装的应用逻辑来自可能不是最新版本的时间点快照。</span><span class="sxs-lookup"><span data-stu-id="e0d60-184">The app starts up immediately regardless of network connectivity, but the installed app logic comes from a point-in-time snapshot that might not be the latest version.</span></span>

<span data-ttu-id="e0d60-185">Blazor PWA 模板生成的应用会在用户访问和具有正在工作的网络连接时，自动尝试在后台进行自我更新。</span><span class="sxs-lookup"><span data-stu-id="e0d60-185">The Blazor PWA template produces apps that automatically try to update themselves in the background whenever the user visits and has a working network connection.</span></span> <span data-ttu-id="e0d60-186">其工作方式如下所示：</span><span class="sxs-lookup"><span data-stu-id="e0d60-186">The way this works is as follows:</span></span>

* <span data-ttu-id="e0d60-187">在编译期间，项目将生成“服务工作进程资产清单”  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-187">During compilation, the project generates a *service worker assets manifest*.</span></span> <span data-ttu-id="e0d60-188">默认情况下，这称为 service-worker-assets.js  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-188">By default, this is called *service-worker-assets.js*.</span></span> <span data-ttu-id="e0d60-189">该清单列出了应用脱机工作所需的所有静态资源，如 .NET 程序集、JavaScript 文件和 CSS，包括其内容哈希。</span><span class="sxs-lookup"><span data-stu-id="e0d60-189">The manifest lists all the static resources that the app requires to function offline, such as .NET assemblies, JavaScript files, and CSS, including their content hashes.</span></span> <span data-ttu-id="e0d60-190">此资源列表由服务工作进程加载，这样它便知道要缓存哪些资源。</span><span class="sxs-lookup"><span data-stu-id="e0d60-190">The resource list is loaded by the service worker so that it knows which resources to cache.</span></span>
* <span data-ttu-id="e0d60-191">用户每次访问应用时，浏览器都会在后台重新请求 service-worker.js 和 service-worker-assets.js   。</span><span class="sxs-lookup"><span data-stu-id="e0d60-191">Each time the user visits the app, the browser re-requests *service-worker.js* and *service-worker-assets.js* in the background.</span></span> <span data-ttu-id="e0d60-192">将文件与现有已安装的服务工作进程逐字节进行比较。</span><span class="sxs-lookup"><span data-stu-id="e0d60-192">The files are compared byte-for-byte with the existing installed service worker.</span></span> <span data-ttu-id="e0d60-193">如果服务器为这些文件中的任一文件返回更改后的内容，则服务工作进程将尝试安装其自身的新版本。</span><span class="sxs-lookup"><span data-stu-id="e0d60-193">If the server returns changed content for either of these files, the service worker attempts to install a new version of itself.</span></span>
* <span data-ttu-id="e0d60-194">安装自身的新版本时，服务工作进程将为脱机资源创建新的独立缓存，并开始使用 service-worker-assets.js 中列出的资源填充该缓存  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-194">When installing a new version of itself, the service worker creates a new, separate cache for offline resources and starts populating the cache with resources listed in *service-worker-assets.js*.</span></span> <span data-ttu-id="e0d60-195">此逻辑在 service-worker.published.js 内的 `onInstall` 函数中实现  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-195">This logic is implemented in the `onInstall` function inside *service-worker.published.js*.</span></span>
* <span data-ttu-id="e0d60-196">如果所有资源正确加载，并且所有内容哈希匹配，则此进程将顺利完成。</span><span class="sxs-lookup"><span data-stu-id="e0d60-196">The process completes successfully when all of the resources are loaded without error and all content hashes match.</span></span> <span data-ttu-id="e0d60-197">如果成功完成，新服务工作进程将进入“等待激活”状态  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-197">If successful, the new service worker enters a *waiting for activation* state.</span></span> <span data-ttu-id="e0d60-198">用户关闭应用后（没有仍未关闭的应用选项卡或窗口），新的服务工作进程将变为活动状态，并用于后续的应用访问  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-198">As soon as the user closes the app (no remaining app tabs or windows), the new service worker becomes *active* and is used for subsequent app visits.</span></span> <span data-ttu-id="e0d60-199">旧服务工作进程及其缓存被删除。</span><span class="sxs-lookup"><span data-stu-id="e0d60-199">The old service worker and its cache are deleted.</span></span>
* <span data-ttu-id="e0d60-200">如果该进程未成功完成，则弃用新的服务工作进程实例。</span><span class="sxs-lookup"><span data-stu-id="e0d60-200">If the process doesn't complete successfully, the new service worker instance is discarded.</span></span> <span data-ttu-id="e0d60-201">用户下次访问时将再次尝试此更新进程，届时客户端最好使用更好的网络连接来完成请求。</span><span class="sxs-lookup"><span data-stu-id="e0d60-201">The update process is attempted again on the user's next visit, when hopefully the client has a better network connection that can complete the requests.</span></span>

<span data-ttu-id="e0d60-202">通过编辑服务工作进程逻辑来自定义此进程。</span><span class="sxs-lookup"><span data-stu-id="e0d60-202">Customize this process by editing the service worker logic.</span></span> <span data-ttu-id="e0d60-203">上述行为均不特定于 Blazor，只是 PWA 模板选项提供的默认体验。</span><span class="sxs-lookup"><span data-stu-id="e0d60-203">None of the preceding behavior is specific to Blazor but is merely the default experience provided by the PWA template option.</span></span> <span data-ttu-id="e0d60-204">有关详细信息，请参阅 [MDN Web 文档：服务工作进程 API](https://developer.mozilla.org/docs/Web/API/Service_Worker_API)。</span><span class="sxs-lookup"><span data-stu-id="e0d60-204">For more information, see [MDN web docs: Service Worker API](https://developer.mozilla.org/docs/Web/API/Service_Worker_API).</span></span>

### <a name="how-requests-are-resolved"></a><span data-ttu-id="e0d60-205">如何解析请求</span><span class="sxs-lookup"><span data-stu-id="e0d60-205">How requests are resolved</span></span>

<span data-ttu-id="e0d60-206">如上[缓存优先提取策略](#cache-first-fetch-strategy)部分所述，默认服务工作进程使用缓存优先策略，这意味着它会尽量提供缓存的内容（如果有）  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-206">As described in the [Cache-first fetch strategy](#cache-first-fetch-strategy) section, the default service worker uses a *cache-first* strategy, meaning that it tries to serve cached content when available.</span></span> <span data-ttu-id="e0d60-207">如果没有对某个 URL 缓存任何内容（例如，从后端 API 请求数据时），则服务工作进程会回退到定期网络请求。</span><span class="sxs-lookup"><span data-stu-id="e0d60-207">If there is no content cached for a certain URL, for example when requesting data from a backend API, the service worker falls back on a regular network request.</span></span> <span data-ttu-id="e0d60-208">如果服务器可访问，该网络请求将会成功。</span><span class="sxs-lookup"><span data-stu-id="e0d60-208">The network request succeeds if the server is reachable.</span></span> <span data-ttu-id="e0d60-209">此逻辑在 service-worker.published.js 内的 `onFetch` 中实现  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-209">This logic is implemented inside `onFetch` function within *service-worker.published.js*.</span></span>

<span data-ttu-id="e0d60-210">如果应用的 Razor 组件依赖于从后端 API 请求数据，并且你想要针对因网络不可用而导致请求失败的情况提供友好的用户体验，则需要在应用的组件中实现逻辑。</span><span class="sxs-lookup"><span data-stu-id="e0d60-210">If the app's Razor components rely on requesting data from backend APIs and you want to provide a friendly user experience for failed requests due to network unavailability, implement logic within the app's components.</span></span> <span data-ttu-id="e0d60-211">例如，对 `HttpClient` 请求使用 `try/catch`。</span><span class="sxs-lookup"><span data-stu-id="e0d60-211">For example, use `try/catch` around `HttpClient` requests.</span></span>

### <a name="support-server-rendered-pages"></a><span data-ttu-id="e0d60-212">支持服务器呈现的页面</span><span class="sxs-lookup"><span data-stu-id="e0d60-212">Support server-rendered pages</span></span>

<span data-ttu-id="e0d60-213">仔细想想用户第一次导航到应用中的 URL（如 `/counter`）或任何其他深层链接时会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="e0d60-213">Consider what happens when the user first navigates to a URL such as `/counter` or any other deep link in the app.</span></span> <span data-ttu-id="e0d60-214">在这些情况下，你不希望返回缓存为 `/counter` 的内容，而是需要浏览器加载缓存为 `/index.html` 的内容，以启动 Blazor WebAssembly 应用。</span><span class="sxs-lookup"><span data-stu-id="e0d60-214">In these cases, you don't want to return content cached as `/counter`, but instead need the browser to load the content cached as `/index.html` to start up your Blazor WebAssembly app.</span></span> <span data-ttu-id="e0d60-215">这些初始请求称为导航请求，而不是  ：</span><span class="sxs-lookup"><span data-stu-id="e0d60-215">These initial requests are known as *navigation* requests, as opposed to:</span></span>

* <span data-ttu-id="e0d60-216">针对图像、样式表或其他文件的子资源请求  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-216">*subresource* requests for images, stylesheets, or other files.</span></span>
* <span data-ttu-id="e0d60-217">针对 API 数据的“提取/XHR”请求  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-217">*fetch/XHR* requests for API data.</span></span>

<span data-ttu-id="e0d60-218">默认服务工作进程包含导航请求的特例逻辑。</span><span class="sxs-lookup"><span data-stu-id="e0d60-218">The default service worker contains special-case logic for navigation requests.</span></span> <span data-ttu-id="e0d60-219">服务工作进程通过返回 `/index.html` 的缓存内容来解析这些请求，而不管请求的 URL 是什么。</span><span class="sxs-lookup"><span data-stu-id="e0d60-219">The service worker resolves the requests by returning the cached content for `/index.html`, regardless of the requested URL.</span></span> <span data-ttu-id="e0d60-220">此逻辑在 service-worker.published.js 内的 `onFetch` 函数中实现  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-220">This logic is implemented in the `onFetch` function inside *service-worker.published.js*.</span></span>

<span data-ttu-id="e0d60-221">如果应用具有必须返回服务器呈现的 HTML 的某些 URL（而不是从缓存中提供 `/index.html`），则需要在服务工作进程中编辑该逻辑。</span><span class="sxs-lookup"><span data-stu-id="e0d60-221">If your app has certain URLs that must return server-rendered HTML, and not serve `/index.html` from the cache, then you need to edit the logic in your service worker.</span></span> <span data-ttu-id="e0d60-222">如果所有包含 `/Identity/` 的 URL 都需要作为对服务器的常规仅联机请求来处理，则需修改 service-worker.published.js `onFetch` 逻辑  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-222">If all URLs containing `/Identity/` need to be handled as regular online-only requests to the server, then modify *service-worker.published.js* `onFetch` logic.</span></span> <span data-ttu-id="e0d60-223">找到下列代码：</span><span class="sxs-lookup"><span data-stu-id="e0d60-223">Locate the following code:</span></span>

```javascript
const shouldServeIndexHtml = event.request.mode === 'navigate';
```

<span data-ttu-id="e0d60-224">将代码更改为以下内容：</span><span class="sxs-lookup"><span data-stu-id="e0d60-224">Change the code to the following:</span></span>

```javascript
const shouldServeIndexHtml = event.request.mode === 'navigate'
    && !event.request.url.includes('/Identity/');
```

<span data-ttu-id="e0d60-225">如果不执行此操作，则无论网络连接情况如何，服务工作进程都将截获此类 URL 的请求，并使用 `/index.html` 解析这些请求。</span><span class="sxs-lookup"><span data-stu-id="e0d60-225">If you don't do this, then regardless of network connectivity, the service worker intercepts requests for such URLs and resolves them using `/index.html`.</span></span>

### <a name="control-asset-caching"></a><span data-ttu-id="e0d60-226">控制资产缓存</span><span class="sxs-lookup"><span data-stu-id="e0d60-226">Control asset caching</span></span>

<span data-ttu-id="e0d60-227">如果项目定义了 `ServiceWorkerAssetsManifest` MSBuild 属性，则 Blazor 的生成工具将生成具有指定名称的服务工作进程资产清单。</span><span class="sxs-lookup"><span data-stu-id="e0d60-227">If your project defines the `ServiceWorkerAssetsManifest` MSBuild property, Blazor's build tooling generates a service worker assets manifest with the specified name.</span></span> <span data-ttu-id="e0d60-228">默认 PWA 模板生成包含以下属性的项目文件：</span><span class="sxs-lookup"><span data-stu-id="e0d60-228">The default PWA template produces a project file containing the following property:</span></span>

```xml
<ServiceWorkerAssetsManifest>service-worker-assets.js</ServiceWorkerAssetsManifest>
```

<span data-ttu-id="e0d60-229">该文件位于“wwwroot”输出目录中  ，因此浏览器可以通过请求 `/service-worker-assets.js` 检索此文件。</span><span class="sxs-lookup"><span data-stu-id="e0d60-229">The file is placed in the *wwwroot* output directory, so the browser can retrieve this file by requesting `/service-worker-assets.js`.</span></span> <span data-ttu-id="e0d60-230">要查看此文件的内容，请在文本编辑器中打开 /bin/Debug/{TARGET FRAMEWORK}/wwwroot/service-worker-assets.js  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-230">To see the contents of this file, open */bin/Debug/{TARGET FRAMEWORK}/wwwroot/service-worker-assets.js* in a text editor.</span></span> <span data-ttu-id="e0d60-231">不过，请不要编辑该文件，因为它会在每次生成时重新生成。</span><span class="sxs-lookup"><span data-stu-id="e0d60-231">However, don't edit the file, as it's regenerated on each build.</span></span>

<span data-ttu-id="e0d60-232">默认情况下，此清单列出：</span><span class="sxs-lookup"><span data-stu-id="e0d60-232">By default, this manifest lists:</span></span>

* <span data-ttu-id="e0d60-233">任何 Blazor 管理的资源（如 .NET 程序集）以及脱机工作所需的 .NET WebAssembly 运行时文件。</span><span class="sxs-lookup"><span data-stu-id="e0d60-233">Any Blazor-managed resources, such as .NET assemblies and the .NET WebAssembly runtime files required to function offline.</span></span>
* <span data-ttu-id="e0d60-234">用于发布到应用的 wwwroot 目录的所有资源，例如图像、样式表和 JavaScript 文件，包括由外部项目和 NuGet 包提供的静态 Web 资产  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-234">All resources for publishing to the app's *wwwroot* directory, such as images, stylesheets, and JavaScript files, including static web assets supplied by external projects and NuGet packages.</span></span>

<span data-ttu-id="e0d60-235">通过编辑 service-worker.published.js 中 `onInstall` 中的逻辑，可控制服务工作进程所提取和缓存的资源  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-235">You can control which of these resources are fetched and cached by the service worker by editing the logic in `onInstall` in *service-worker.published.js*.</span></span> <span data-ttu-id="e0d60-236">默认情况下，服务工作进程将提取并缓存与典型 Web 文件扩展名匹配的文件，例如 .html、.css、.js、.wasm 等文件，以及特定于 Blazor WebAssembly 的文件类型（.dll、.pdb）       。</span><span class="sxs-lookup"><span data-stu-id="e0d60-236">By default, the service worker fetches and caches files matching typical web filename extensions such as *.html*, *.css*, *.js*, and *.wasm*, plus file types specific to Blazor WebAssembly (*.dll*, *.pdb*).</span></span>

<span data-ttu-id="e0d60-237">要包括应用的 wwwroot 目录中不存在的其他资源，请定义额外的 MSBuild `ItemGroup` 条目，如以下示例所示  ：</span><span class="sxs-lookup"><span data-stu-id="e0d60-237">To include additional resources that aren't present in the app's *wwwroot* directory, define extra MSBuild `ItemGroup` entries, as shown in the following example:</span></span>

```xml
<ItemGroup>
  <ServiceWorkerAssetsManifestItem Include="MyDirectory\AnotherFile.json"
    RelativePath="MyDirectory\AnotherFile.json" AssetUrl="files/AnotherFile.json" />
</ItemGroup>
```

<span data-ttu-id="e0d60-238">`AssetUrl` 元数据指定了在提取要缓存的资源时浏览器应使用的基相对 URL。</span><span class="sxs-lookup"><span data-stu-id="e0d60-238">The `AssetUrl` metadata specifies the base-relative URL that the browser should use when fetching the resource to cache.</span></span> <span data-ttu-id="e0d60-239">它可以独立于磁盘上的原始源文件名。</span><span class="sxs-lookup"><span data-stu-id="e0d60-239">This can be independent of its original source file name on disk.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0d60-240">添加 `ServiceWorkerAssetsManifestItem` 不会导致文件发布到应用的 wwwroot 目录  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-240">Adding a `ServiceWorkerAssetsManifestItem` doesn't cause the file to be published in the app's *wwwroot* directory.</span></span> <span data-ttu-id="e0d60-241">必须单独控制发布输出。</span><span class="sxs-lookup"><span data-stu-id="e0d60-241">The publish output must be controlled separately.</span></span> <span data-ttu-id="e0d60-242">`ServiceWorkerAssetsManifestItem` 仅导致服务工作进程清单中出现一个额外条目。</span><span class="sxs-lookup"><span data-stu-id="e0d60-242">The `ServiceWorkerAssetsManifestItem` only causes an additional entry to appear in the service worker assets manifest.</span></span>

## <a name="push-notifications"></a><span data-ttu-id="e0d60-243">推送通知</span><span class="sxs-lookup"><span data-stu-id="e0d60-243">Push notifications</span></span>

<span data-ttu-id="e0d60-244">与任何其他 PWA 一样，Blazor WebAssembly PWA 可以从后端服务器接收推送通知。</span><span class="sxs-lookup"><span data-stu-id="e0d60-244">Like any other PWA, a Blazor WebAssembly PWA can receive push notifications from a backend server.</span></span> <span data-ttu-id="e0d60-245">服务器可以随时发送推送通知，即使用户不常使用该应用也是如此。</span><span class="sxs-lookup"><span data-stu-id="e0d60-245">The server can send push notifications at any time, even when the user isn't actively using the app.</span></span> <span data-ttu-id="e0d60-246">例如，当其他用户执行相关操作时，可以发送推送通知。</span><span class="sxs-lookup"><span data-stu-id="e0d60-246">For example, push notifications can be sent when a different user performs a relevant action.</span></span>

<span data-ttu-id="e0d60-247">发送推送通知的机制完全独立于 Blazor WebAssembly，因为它是由可以使用任何技术的后端服务器实现的。</span><span class="sxs-lookup"><span data-stu-id="e0d60-247">The mechanism for sending a push notification is entirely independent of Blazor WebAssembly, since it's implemented by the backend server which can use any technology.</span></span> <span data-ttu-id="e0d60-248">如果想要从 ASP.NET Core 服务器发送推送通知，请考虑[使用与 Blazing Pizza 研讨会中采用的方法类似的方法](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/09-progressive-web-app.md#sending-push-notifications)。</span><span class="sxs-lookup"><span data-stu-id="e0d60-248">If you want to send push notifications from an ASP.NET Core server, consider [using a technique similar to the approach taken in the Blazing Pizza workshop](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/09-progressive-web-app.md#sending-push-notifications).</span></span>

<span data-ttu-id="e0d60-249">在客户端上接收和显示推送通知的机制也独立于 Blazor WebAssembly，因为它是在服务工作进程 JavaScript 文件中实现的。</span><span class="sxs-lookup"><span data-stu-id="e0d60-249">The mechanism for receiving and displaying a push notification on the client is also independent of Blazor WebAssembly, since it's implemented in the service worker JavaScript file.</span></span> <span data-ttu-id="e0d60-250">例如，请参阅[在 Blazing Pizza 研讨会中使用的方法](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/09-progressive-web-app.md#displaying-notifications)。</span><span class="sxs-lookup"><span data-stu-id="e0d60-250">For an example, see [the approach used in the Blazing Pizza workshop](https://github.com/dotnet-presentations/blazor-workshop/blob/master/docs/09-progressive-web-app.md#displaying-notifications).</span></span>

## <a name="caveats-for-offline-pwas"></a><span data-ttu-id="e0d60-251">脱机 PWA 的注意事项</span><span class="sxs-lookup"><span data-stu-id="e0d60-251">Caveats for offline PWAs</span></span>

<span data-ttu-id="e0d60-252">并非所有应用都应尝试支持脱机使用。</span><span class="sxs-lookup"><span data-stu-id="e0d60-252">Not all apps should attempt to support offline use.</span></span> <span data-ttu-id="e0d60-253">脱机支持增加了相当大的复杂性，但并不总是与所需的用例相关。</span><span class="sxs-lookup"><span data-stu-id="e0d60-253">Offline support adds significant complexity, while not always being relevant for the use cases required.</span></span>

<span data-ttu-id="e0d60-254">脱机支持通常仅适用于以下情况：</span><span class="sxs-lookup"><span data-stu-id="e0d60-254">Offline support is usually relevant only:</span></span>

* <span data-ttu-id="e0d60-255">主数据存储是浏览器的本地数据存储。</span><span class="sxs-lookup"><span data-stu-id="e0d60-255">If the primary data store is local to the browser.</span></span> <span data-ttu-id="e0d60-256">例如，该方法与后述应用相关：该应用具有一个用于 [IoT](https://en.wikipedia.org/wiki/Internet_of_things) 设备的 UI，且该设备将数据存储在 `localStorage` 或 [IndexedDB](https://developer.mozilla.org/docs/Web/API/IndexedDB_API) 中。</span><span class="sxs-lookup"><span data-stu-id="e0d60-256">For example, the approach is relevant in an app with a UI for an [IoT](https://en.wikipedia.org/wiki/Internet_of_things) device that stores data in `localStorage` or [IndexedDB](https://developer.mozilla.org/docs/Web/API/IndexedDB_API).</span></span>
* <span data-ttu-id="e0d60-257">应用执行大量工作来提取和缓存与每个用户相关的后端 API 数据，以便用户可以脱机浏览数据。</span><span class="sxs-lookup"><span data-stu-id="e0d60-257">If the app performs a significant amount of work to fetch and cache the backend API data relevant to each user so that they can navigate through the data offline.</span></span> <span data-ttu-id="e0d60-258">应用必须支持编辑，需要生成一个用于跟踪更改并将数据与后端进行同步的系统。</span><span class="sxs-lookup"><span data-stu-id="e0d60-258">If the app must support editing, a system for tracking changes and synchronizing data with the backend must be built.</span></span>
* <span data-ttu-id="e0d60-259">目标是在不考虑网络状况的情况下保证应用立即加载，</span><span class="sxs-lookup"><span data-stu-id="e0d60-259">If the goal is to guarantee that the app loads immediately regardless of network conditions.</span></span> <span data-ttu-id="e0d60-260">则需要对后端 API 请求实现适当的用户体验，以显示请求的进度，并在请求因网络不可用而失败时妥善处理。</span><span class="sxs-lookup"><span data-stu-id="e0d60-260">Implement a suitable user experience around backend API requests to show the progress of requests and behave gracefully when requests fail due to network unavailability.</span></span>

<span data-ttu-id="e0d60-261">此外，支持脱机的 PWA 必须处理一系列额外的复杂操作。</span><span class="sxs-lookup"><span data-stu-id="e0d60-261">Additionally, offline-capable PWAs must deal with a range of additional complications.</span></span> <span data-ttu-id="e0d60-262">开发者应认真熟悉以下部分中的注意事项。</span><span class="sxs-lookup"><span data-stu-id="e0d60-262">Developers should carefully familiarize themselves with the caveats in the following sections.</span></span>

### <a name="offline-support-only-when-published"></a><span data-ttu-id="e0d60-263">仅在发布后支持脱机</span><span class="sxs-lookup"><span data-stu-id="e0d60-263">Offline support only when published</span></span>

<span data-ttu-id="e0d60-264">在开发过程中，通常希望看到各项更改立即反映在浏览器中，而无需经过后台更新过程。</span><span class="sxs-lookup"><span data-stu-id="e0d60-264">During development you typically want to see each change reflected immediately in the browser without going through a background update process.</span></span> <span data-ttu-id="e0d60-265">因此，Blazor 的 PWA 模板仅在发布后启用脱机支持。</span><span class="sxs-lookup"><span data-stu-id="e0d60-265">Therefore, Blazor's PWA template enables offline support only when published.</span></span>

<span data-ttu-id="e0d60-266">在构建支持脱机的应用时，仅在开发环境中测试应用是不够的。</span><span class="sxs-lookup"><span data-stu-id="e0d60-266">When building an offline-capable app, it's not enough to test the app in the Development environment.</span></span> <span data-ttu-id="e0d60-267">必须在已发布状态下测试应用，了解它对不同网络情况的响应。</span><span class="sxs-lookup"><span data-stu-id="e0d60-267">You must test the app in its published state to understand how it responds to different network conditions.</span></span>

### <a name="update-completion-after-user-navigation-away-from-app"></a><span data-ttu-id="e0d60-268">用户导航离开应用后完成更新</span><span class="sxs-lookup"><span data-stu-id="e0d60-268">Update completion after user navigation away from app</span></span>

<span data-ttu-id="e0d60-269">用户导航离开了所有选项卡中的应用后，更新才会完成。</span><span class="sxs-lookup"><span data-stu-id="e0d60-269">Updates don't complete until the user has navigated away from the app in all tabs.</span></span> <span data-ttu-id="e0d60-270">如[后台更新](#background-updates)部分中所述，在将更新部署到应用后，浏览器将提取更新后的服务工作进程文件以开始更新进程。</span><span class="sxs-lookup"><span data-stu-id="e0d60-270">As explained in the [Background updates](#background-updates) section, after you deploy an update to the app, the browser fetches the updated service worker files to begin the update process.</span></span>

<span data-ttu-id="e0d60-271">令许多开发人员惊讶的是，即使此更新完成，在用户导航离开所有选项卡之前，它也不会生效  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-271">What surprises many developers is that, even when this update completes, it does **not** take effect until the user has navigated away in all tabs.</span></span> <span data-ttu-id="e0d60-272">刷新显示应用的选项卡也不行，即使它是显示应用的唯一选项卡也是如此  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-272">It is **not** sufficient to refresh the tab displaying the app, even if it's the only tab displaying the app.</span></span> <span data-ttu-id="e0d60-273">在应用完全关闭之前，新的服务工作进程将保持“正在等待激活”状态  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-273">Until your app is completely closed, the new service worker remains in the *waiting to activate* status.</span></span> <span data-ttu-id="e0d60-274">这并不特定于 Blazor，而是标准 Web 平台行为。 </span><span class="sxs-lookup"><span data-stu-id="e0d60-274">**This is not specific to Blazor, but rather is a standard web platform behavior.**</span></span>

<span data-ttu-id="e0d60-275">这通常会给试图测试对其服务工作进程或脱机缓存资源的更新的开发人员造成麻烦。</span><span class="sxs-lookup"><span data-stu-id="e0d60-275">This commonly troubles developers who are trying to test updates to their service worker or offline cached resources.</span></span> <span data-ttu-id="e0d60-276">如果签入浏览器的开发者工具，可能会看到如下所示的内容：</span><span class="sxs-lookup"><span data-stu-id="e0d60-276">If you check in the browser's developer tools, you may see something like the following:</span></span>

![Google Chrome 的“应用程序”选项显示该应用的服务工作进程处于“正在等待激活”状态。](progressive-web-app/_static/image7.png)

<span data-ttu-id="e0d60-278">只要“客户端”列表（即显示应用的选项卡或窗口）不为空，工作进程就会继续等待。</span><span class="sxs-lookup"><span data-stu-id="e0d60-278">For as long as the list of "clients," which are tabs or windows displaying your app, is nonempty, the worker continues waiting.</span></span> <span data-ttu-id="e0d60-279">服务工作进程这样做的原因是为了保证一致性。</span><span class="sxs-lookup"><span data-stu-id="e0d60-279">The reason service workers do this is to guarantee consistency.</span></span> <span data-ttu-id="e0d60-280">一致性意味着所有资源都是从同一原子缓存中提取的。</span><span class="sxs-lookup"><span data-stu-id="e0d60-280">Consistency means that all resources are fetched from the same atomic cache.</span></span>

<span data-ttu-id="e0d60-281">测试更改时，你可能会发现，单击如上面的屏幕截图中所示的“skipWaiting”链接，然后重载页面，这样操作会比较方便。</span><span class="sxs-lookup"><span data-stu-id="e0d60-281">When testing changes, you may find it convenient to click the "skipWaiting" link as shown in the preceding screenshot, then reload the page.</span></span> <span data-ttu-id="e0d60-282">可以通过以下方式为所有用户自动实现此操作：对服务工作进程进行编码，[跳过“等待”阶段并在更新时立即激活](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle#skip_the_waiting_phase)。</span><span class="sxs-lookup"><span data-stu-id="e0d60-282">You can automate this for all users by coding your service worker to [skip the "waiting" phase and immediately activate on update](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle#skip_the_waiting_phase).</span></span> <span data-ttu-id="e0d60-283">如果跳过等待阶段，则无法保证资源始终一致地提取自同一缓存实例。</span><span class="sxs-lookup"><span data-stu-id="e0d60-283">If you skip the waiting phase, you're giving up the guarantee that resources are always fetched consistently from the same cache instance.</span></span>

### <a name="users-may-run-any-historical-version-of-the-app"></a><span data-ttu-id="e0d60-284">用户可以运行应用的任何历史版本</span><span class="sxs-lookup"><span data-stu-id="e0d60-284">Users may run any historical version of the app</span></span>

<span data-ttu-id="e0d60-285">Web 开发者通常期望用户仅运行其 Web 应用的最新部署版本，因为在传统的 Web 分发模型中这是正常现象。</span><span class="sxs-lookup"><span data-stu-id="e0d60-285">Web developers habitually expect that users only run the latest deployed version of their web app, since that's normal within the traditional web distribution model.</span></span> <span data-ttu-id="e0d60-286">但是，脱机优先 PWA 更类似于本机移动应用，用户不必运行最新版本。</span><span class="sxs-lookup"><span data-stu-id="e0d60-286">However, an offline-first PWA is more akin to a native mobile app, where users aren't necessarily running the latest version.</span></span>

<span data-ttu-id="e0d60-287">如[后台更新](#background-updates)部分中所述，在将更新部署到应用后，每个现有用户将继续使用以前的版本，至少再进行一次访问（因为更新在后台进行，且在用户离开后才会激活）  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-287">As explained in the [Background updates](#background-updates) section, after you deploy an update to your app, **each existing user continues to use a previous version for at least one further visit** because the update occurs in the background and isn't activated until the user thereafter navigates away.</span></span> <span data-ttu-id="e0d60-288">此外，使用的上一个版本不一定是之前所部署的版本。</span><span class="sxs-lookup"><span data-stu-id="e0d60-288">Plus, the previous version being used isn't necessarily the previous one you deployed.</span></span> <span data-ttu-id="e0d60-289">之前的版本可以是任何一个历史版本，具体取决于用户上次完成更新的时间  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-289">The previous version can be *any* historical version, depending on when the user last completed an update.</span></span>

<span data-ttu-id="e0d60-290">如果应用的前端和后端部分需要就 API 请求的架构达成一致，这可能是一个问题。</span><span class="sxs-lookup"><span data-stu-id="e0d60-290">This can be an issue if the frontend and backend parts of your app require agreement about the schema for API requests.</span></span> <span data-ttu-id="e0d60-291">要部署后向不兼容的 API 架构变更，必须先确保所有用户都已升级，</span><span class="sxs-lookup"><span data-stu-id="e0d60-291">You must not deploy backward-incompatible API schema changes until you can be sure that all users have upgraded.</span></span> <span data-ttu-id="e0d60-292">或者阻止用户使用不兼容的旧应用版本。</span><span class="sxs-lookup"><span data-stu-id="e0d60-292">Alternatively, block users from using incompatible older versions of the app.</span></span> <span data-ttu-id="e0d60-293">此方案的要求与本机移动应用的要求相同。</span><span class="sxs-lookup"><span data-stu-id="e0d60-293">This scenario requirement is the same as for native mobile apps.</span></span> <span data-ttu-id="e0d60-294">如果在服务器 API 中部署中断性变更，则尚未更新的用户的客户端应用将中断。</span><span class="sxs-lookup"><span data-stu-id="e0d60-294">If you deploy a breaking change in server APIs, the client app is broken for users who haven't yet updated.</span></span>

<span data-ttu-id="e0d60-295">如果可以，请勿将中断性变更部署到后端 API。</span><span class="sxs-lookup"><span data-stu-id="e0d60-295">If possible, don't deploy breaking changes to your backend APIs.</span></span> <span data-ttu-id="e0d60-296">但如果必须这样做，请考虑使用[标准服务工作进程 API（如 ServiceWorkerRegistration）](https://developer.mozilla.org/docs/Web/API/ServiceWorkerRegistration)，确定应用是否为最新版本；如果不是，则阻止使用。</span><span class="sxs-lookup"><span data-stu-id="e0d60-296">If you must do so, consider using [standard Service Worker APIs such as ServiceWorkerRegistration](https://developer.mozilla.org/docs/Web/API/ServiceWorkerRegistration) to determine whether the app is up-to-date, and if not, to prevent usage.</span></span>

### <a name="interference-with-server-rendered-pages"></a><span data-ttu-id="e0d60-297">干扰服务器呈现的页面</span><span class="sxs-lookup"><span data-stu-id="e0d60-297">Interference with server-rendered pages</span></span>

<span data-ttu-id="e0d60-298">如[支持服务器呈现的页面](#support-server-rendered-pages)部分中所述，若要绕过服务工作进程为所有导航请求返回 `/index.html` 内容的行为，请在服务工作进程中编辑该逻辑。</span><span class="sxs-lookup"><span data-stu-id="e0d60-298">As described in the [Support server-rendered pages](#support-server-rendered-pages) section, if you want to bypass the service worker's behavior of returning `/index.html` contents for all navigation requests, edit the logic in your service worker.</span></span>

### <a name="all-service-worker-asset-manifest-contents-are-cached-by-default"></a><span data-ttu-id="e0d60-299">默认缓存所有服务工作进程资产清单内容</span><span class="sxs-lookup"><span data-stu-id="e0d60-299">All service worker asset manifest contents are cached by default</span></span>

<span data-ttu-id="e0d60-300">如[控制资产缓存](#control-asset-caching)部分中所述，文件 service-worker-assets.js 是在生成过程中产生的，并且列出了服务工作进程应提取和缓存的所有资产  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-300">As described in the [Control asset caching](#control-asset-caching) section, the file *service-worker-assets.js* is generated during build and lists all assets the service worker should fetch and cache.</span></span>

<span data-ttu-id="e0d60-301">由于此列表默认包含发出到 wwwroot 的所有内容（包括外部包和项目提供的内容），因此必须注意不要将太多内容放在此处  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-301">Since this list by default includes everything emitted to *wwwroot*, including content supplied by external packages and projects, you must be careful not to put too much content there.</span></span> <span data-ttu-id="e0d60-302">如果 wwwroot 目录包含数百万个图像，服务工作进程会尝试提取并缓存它们，这会消耗过多的带宽，并且很可能无法成功完成  。</span><span class="sxs-lookup"><span data-stu-id="e0d60-302">If the *wwwroot* directory contains millions of images, the service worker tries to fetch and cache them all, consuming excessive bandwidth and most likely not completing successfully.</span></span>

<span data-ttu-id="e0d60-303">通过编辑 service-worker.published.js 中的 `onInstall` 函数  ，可以实现任意逻辑以控制应提取和缓存清单内容的哪个子集。</span><span class="sxs-lookup"><span data-stu-id="e0d60-303">Implement arbitrary logic to control which subset of the manifest's contents should be fetched and cached by editing the `onInstall` function in *service-worker.published.js*.</span></span>

### <a name="interaction-with-authentication"></a><span data-ttu-id="e0d60-304">与身份验证交互</span><span class="sxs-lookup"><span data-stu-id="e0d60-304">Interaction with authentication</span></span>

<span data-ttu-id="e0d60-305">可以结合使用 PWA 模板选项和身份验证选项。</span><span class="sxs-lookup"><span data-stu-id="e0d60-305">It's possible to use the PWA template option in conjunction with the authentication options.</span></span> <span data-ttu-id="e0d60-306">在用户具有网络连接时，支持脱机的 PWA 还可以支持身份验证。</span><span class="sxs-lookup"><span data-stu-id="e0d60-306">An offline-capable PWA can also support authentication when the user has network connectivity.</span></span>

<span data-ttu-id="e0d60-307">当用户没有网络连接时，他们无法进行身份验证或获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="e0d60-307">When a user doesn't have network connectivity, they can't authenticate or obtain access tokens.</span></span> <span data-ttu-id="e0d60-308">默认情况下，在没有网络访问权限的情况下尝试访问登录页面会导致出现“网络错误”消息。</span><span class="sxs-lookup"><span data-stu-id="e0d60-308">By default, attempting to visit the login page without network access results in a "network error" message.</span></span>

<span data-ttu-id="e0d60-309">必须设计一个 UI 流，使用户能够在脱机时执行实用的操作，而无需尝试进行身份验证或获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="e0d60-309">You must design a UI flow that lets the user do useful things while offline without attempting to authenticate or obtain access tokens.</span></span> <span data-ttu-id="e0d60-310">或者，将应用设计为在网络不可用时正常提示操作失败。</span><span class="sxs-lookup"><span data-stu-id="e0d60-310">Alternatively, you can design the app to fail in a graceful way when the network isn't available.</span></span> <span data-ttu-id="e0d60-311">如果这在应用中不可行，你可能不希望启用脱机支持。</span><span class="sxs-lookup"><span data-stu-id="e0d60-311">If this isn't possible in your app, you might not want to enable offline support.</span></span>