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
ms.openlocfilehash: aa6c6e38559830b3caae9f8d46abfbe87415fe4f
ms.sourcegitcommit: a49c47d5a573379effee5c6b6e36f5c302aa756b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100551674"
---
整个应用通过 `_Imports.razor` 文件提供 <xref:Microsoft.AspNetCore.Components.Authorization?displayProperty=fullName> 命名空间：

::: moniker range=">= aspnetcore-5.0"

[!code-razor[](imports-hosted-5x.razor?highlight=3)]

::: moniker-end

::: moniker range="< aspnetcore-5.0"

[!code-razor[](imports-hosted-3x.razor?highlight=3)]

::: moniker-end
