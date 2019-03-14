---
ms.openlocfilehash: 282871e5db197dfb4226cc02918f2d6ba1135c04
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57045600"
---
# <a name="aspnet-core-middleware-extensibility-sample"></a>ASP.NET Core 미들웨어 확장성 샘플

이 샘플에서는 [IMiddleware](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddleware) 및 [IMiddlewareFactory](https://docs.microsoft.com/dotnet/api/microsoft.aspnetcore.http.imiddlewarefactory)를 타사 종속성 주입 컨테이너인 [간단한 인젝터](https://simpleinjector.org)와 함께 사용하는 방법을 보여 줍니다. 이 샘플에서는 [ASP.NET Core에서 타사 컨테이너를 사용하여 미들웨어 활성화](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/extensibility-third-party-container)에 설명된 기능을 보여 줍니다.
