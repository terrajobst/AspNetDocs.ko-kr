---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: 성능 향상을 위해 ASP.NET 웹 페이지 (Razor) 사이트에서 데이터 캐싱 | Microsoft Docs
author: Rick-Anderson
description: 저장소를 저장 하 여 웹 사이트의 속도를 높일 수 있습니다. 즉, 일반적으로 ...을 검색 하거나 처리 하는 데 상당한 시간이 소요 되는 데이터의 결과를 캐시 합니다.
ms.author: riande
ms.date: 02/14/2014
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 01796d3ca699a6af5d9162b22a926551435c2040
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521159"
---
# <a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a>성능 향상을 위해 ASP.NET 웹 페이지 (Razor) 사이트에서 데이터 캐싱

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 도우미를 사용 하 여 ASP.NET 웹 페이지 (Razor) 웹 사이트에서 더 빠른 성능을 위해 정보를 캐시 하는 방법을 설명 합니다. 웹 사이트 &#8212; 의 속도를 향상 시킬 수 있습니다. 즉, 일반적으로 &#8212; 검색 또는 처리 하는 데 상당한 시간이 걸리고 자주 변경 되지 않는 데이터의 결과를 캐시 합니다.
> 
> **학습 내용:** 
> 
> - 캐싱을 사용 하 여 웹 사이트의 응답성을 향상 시키는 방법
> 
> 다음은이 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `WebCache` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

누군가가 사이트에서 페이지를 요청할 때마다 웹 서버는 요청을 수행 하기 위해 일부 작업을 수행 해야 합니다. 일부 페이지의 경우 서버는 데이터베이스에서 데이터를 검색 하는 것과 같이 비교적 긴 시간을 사용 하는 작업을 수행 해야 할 수 있습니다. 이러한 작업에는 절대 시간이 오래 걸리지 않지만 사이트에 많은 트래픽이 발생 하는 경우 웹 서버에서 복잡 한 작업을 수행 하는 일련의 개별 요청이 많은 작업을 추가할 수 있습니다. 이는 궁극적으로 사이트의 성능에 영향을 줄 수 있습니다.

이와 같은 상황에서 웹 사이트의 성능을 향상 시키는 한 가지 방법은 데이터를 캐시 하는 것입니다. 사이트에서 동일한 정보에 대 한 반복 된 요청을 가져오고 각 사용자에 대 한 정보를 수정할 필요가 없고 시간이 중요 하지 않은 경우에는 데이터를 한 번 페치 한 다음 결과를 저장할 수 있습니다. 다음에 해당 정보에 대 한 요청이 들어올 때 캐시에서 가져옵니다.

일반적으로 자주 변경 되지 않는 정보를 캐시 합니다. 캐시에 정보를 저장 하면 웹 서버의 메모리에 저장 됩니다. 몇 초에서 며칠까지 캐시 해야 하는 기간을 지정할 수 있습니다. 캐싱 기간이 만료 되 면 정보가 캐시에서 자동으로 제거 됩니다.

> [!NOTE]
> 캐시의 항목이 만료 된 것 이외의 이유로 인해 제거 될 수 있습니다. 예를 들어 웹 서버에 일시적으로 메모리가 부족 하거나 메모리를 회수할 수 있는 한 가지 방법은 캐시에서 항목을 throw 하는 것입니다. 캐시에 정보를 입력 한 경우에도 필요한 경우에도 해당 정보를 확인할 수 있는지 확인 해야 합니다.

웹 사이트에 현재 온도 및 날씨 예보를 표시 하는 페이지가 있다고 가정 합니다. 이러한 유형의 정보를 얻으려면 외부 서비스로 요청을 보낼 수 있습니다. 이 정보는 크게 변경 되지 않으므로 (예: 2 시간 동안) 외부 호출에 시간과 대역폭이 필요 하므로 캐싱에 적합 합니다.

## <a name="adding-caching-to-a-page"></a>페이지에 캐싱 추가

ASP.NET에는 사이트에 캐싱을 추가 하 고 캐시에 데이터를 추가 하는 데 사용 되는 `WebCache` 도우미가 포함 되어 있습니다. 이 절차에서는 현재 시간을 캐시 하는 페이지를 만듭니다. 실제 예는 아니지만 현재 시간은 자주 변경 되 고 계산 하기 복잡 하지 않기 때문입니다. 그러나 캐싱 작업을 설명 하는 좋은 방법입니다.

1. 웹 사이트에 *Webcache. cshtml* 라는 새 페이지를 추가 합니다.
2. 페이지에 다음 코드 및 태그를 추가 합니다.

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    데이터를 캐시 하는 경우 웹 사이트에서 고유한 이름을 사용 하 여 캐시에 저장 합니다. 이 경우 `CachedTime`라는 캐시 항목을 사용 합니다. 다음은 코드 예제에 표시 된 `cacheItemKey`입니다.

    코드는 먼저 `CachedTime` 캐시 엔트리를 읽습니다. 값이 반환 되는 경우 (즉, 캐시 엔트리가 null이 아닌 경우) 코드는 시간 변수의 값을 캐시 데이터로 설정 하기만 합니다.

    그러나 캐시 항목이 존재 하지 않는 경우 (즉, null) 코드에서 시간 값을 설정 하 고, 캐시에 추가 하 고, 만료 값을 1 분으로 설정 합니다. 1 분 후 캐시 항목이 삭제 됩니다. 캐시의 항목에 대 한 기본 만료 값은 20 분입니다. 명령 `WebCache.Set(cacheItemKey, time, 1, false)`는 캐시에 현재 시간 값을 추가 하 고 만료 시간을 1 분으로 설정 하는 방법을 보여 줍니다. *SlidingExpiration* 매개 변수를 `false`로 설정 하면 만료 시간이 요청 될 때마다 갱신 되지 않습니다. 원래 캐시에 추가 된 후 정확히 1 분 후에 만료 됩니다. 이 값을로 설정 하면 캐시에서 값이 요청 될 때마다 1 분의 만료 시간이 다시 설정 됩니다 `true`.

    이 코드는 데이터를 캐시할 때 항상 사용 해야 하는 패턴을 보여 줍니다. 캐시에서 항목을 가져오기 전에 항상 `WebCache.Get` 메서드가 null을 반환 했는지 여부를 먼저 확인 합니다. 캐시 엔트리가 만료 되었거나 일부 다른 이유로 제거 되었을 수 있으므로 지정 된 항목이 캐시에 있는 것이 보장 되지 않습니다.
3. 브라우저에서 *Webcache. cshtml* 를 실행 합니다. (파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 페이지를 처음 요청할 때 시간 데이터는 캐시에 없고 코드는 시간 값을 캐시에 추가 해야 합니다.

    ![cache-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. 브라우저에서 *Webcache. cshtml* 를 새로 고칩니다. 이번에는 시간 데이터가 캐시에 있습니다. 페이지를 마지막으로 본 이후 시간이 변경 되지 않은 것을 확인할 수 있습니다.

    ![cache-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. 캐시를 비울 때까지 1 분 정도 기다린 다음 페이지를 새로 고칩니다. 이 페이지는 캐시에서 데이터를 찾을 수 없는 시간 및 업데이트 된 시간을 캐시에 추가 했음을 나타냅니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [차트에 데이터 표시](https://go.microsoft.com/fwlink/?LinkId=202895)
- [Webcache API 참조](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)
