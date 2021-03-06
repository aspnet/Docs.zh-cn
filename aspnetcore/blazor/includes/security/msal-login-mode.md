---
no-loc:
- appsettings.json
- ASP.NET Core Identity
- cookie
- Cookie
- Blazor
- Blazor Server
- Blazor WebAssembly
- Identity
- Let's Encrypt
- Razor
- SignalR
ms.openlocfilehash: 1b045d437d1a16eabc0ab41573c8b66d9c4bb77e
ms.sourcegitcommit: a49c47d5a573379effee5c6b6e36f5c302aa756b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100551254"
---
框架默认为弹出式登录模式；如果无法打开弹出窗口，则回到重定向登录模式。 通过将 <xref:Microsoft.Authentication.WebAssembly.Msal.Models.MsalProviderOptions> 的 `LoginMode` 属性设置为 `redirect`，将 MSAL 配置为使用重定向登录模式：

```csharp
builder.Services.AddMsalAuthentication(options =>
{
    ...
    options.ProviderOptions.LoginMode = "redirect";
});
```

默认设置为 `popup`，字符串值不区分大小写。
