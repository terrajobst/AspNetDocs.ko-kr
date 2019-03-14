---
ms.openlocfilehash: 93bda587eebc438e5da36b07cb7e4a37df8a91eb
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57062720"
---
# <a name="aspnet-core-response-caching-sample"></a><span data-ttu-id="eeb5b-101">ASP.NET Core 응답 캐싱 예제</span><span class="sxs-lookup"><span data-stu-id="eeb5b-101">ASP.NET Core Response Caching Sample</span></span>

<span data-ttu-id="eeb5b-102">이 샘플에서는 ASP.NET Core의 사용을 보여 줍니다 [응답 캐싱 미들웨어](https://docs.microsoft.com/aspnet/core/performance/caching/middleware)합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb5b-102">This sample illustrates the usage of ASP.NET Core [Response Caching Middleware](https://docs.microsoft.com/aspnet/core/performance/caching/middleware).</span></span>

<span data-ttu-id="eeb5b-103">해당 인덱스 페이지를 사용 하 여 앱이 응답 등을 `Cache-Control` 캐싱 동작을 구성 하는 헤더입니다.</span><span class="sxs-lookup"><span data-stu-id="eeb5b-103">The app responds with its Index page, including a `Cache-Control` header to configure caching behavior.</span></span> <span data-ttu-id="eeb5b-104">앱 설정 합니다 `Vary` 경우에만 응답에 맞도록 캐시를 구성 하는 헤더는 `Accept-Encoding` 후속 요청의 헤더는 원래 요청에서 일치 합니다.</span><span class="sxs-lookup"><span data-stu-id="eeb5b-104">The app also sets the `Vary` header to configure the cache to serve the response only if the `Accept-Encoding` header of subsequent requests matches that from the original request.</span></span>

<span data-ttu-id="eeb5b-105">이 샘플을 실행 하는 경우 인덱스 페이지가 저장 하 고 최대 10 초 동안 캐시 되 면 캐시에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="eeb5b-105">When running the sample, the Index page is served from cache when stored and cached for up to 10 seconds.</span></span>
