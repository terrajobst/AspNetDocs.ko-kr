---
ms.openlocfilehash: dc6c86c48cfb4dd7e27c03ae29519417e60eac5b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57168665"
---
## <a name="multiple-authentication-providers"></a><span data-ttu-id="ef3a9-101">여러 인증 공급자</span><span class="sxs-lookup"><span data-stu-id="ef3a9-101">Multiple authentication providers</span></span>

<span data-ttu-id="ef3a9-102">앱에 여러 공급자가 필요한 경우 [AddAuthentication](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication) 뒤에 공급자 확장 메서드를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ef3a9-102">When the app requires multiple providers, chain the provider extension methods behind [AddAuthentication](/dotnet/api/microsoft.extensions.dependencyinjection.authenticationservicecollectionextensions.addauthentication):</span></span>

```csharp
services.AddAuthentication()
    .AddMicrosoftAccount(microsoftOptions => { ... })
    .AddGoogle(googleOptions => { ... })
    .AddTwitter(twitterOptions => { ... })
    .AddFacebook(facebookOptions => { ... });
```
