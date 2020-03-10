---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: ASP.NET 웹 페이지 (Razor) 사이트에서 읽을 수 있는 Url 만들기 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트의 라우팅을 설명 하 고이를 통해 SEO에 대해 더 읽기 쉽고 향상 된 Url을 사용 하는 방법을 설명 합니다. 수행할 작업 ...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509909"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 읽을 수 있는 Url 만들기

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트의 라우팅을 설명 하 고이를 통해 SEO에 대해 더 읽기 쉽고 향상 된 Url을 사용 하는 방법을 설명 합니다.
> 
> 학습할 내용:
> 
> - ASP.NET에서 라우팅을 사용 하 여 더 읽기 쉽고 검색 가능한 Url을 사용할 수 있도록 하는 방법입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

## <a name="about-routing"></a>라우팅 정보

사이트의 페이지에 대 한 Url은 사이트의 작동 방식에 영향을 줄 수 있습니다. 친숙 한&quot; &quot;URL을 사용 하면 사용자가 사이트를 보다 쉽게 사용할 수 있습니다. 사이트의 SEO (검색 엔진 최적화)에도 도움이 될 수 있습니다. ASP.NET 웹 사이트에는 친숙 한 Url을 자동으로 사용 하는 기능이 포함 됩니다.

ASP.NET를 사용 하면 단순히 서버의 파일을 가리키는 대신 사용자 동작을 설명 하는 의미 있는 Url을 만들 수 있습니다. 가상 블로그에 대해 다음 Url을 고려 합니다.

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

이러한 Url을 다음과 같이 비교 합니다.

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

첫 번째 쌍의 사용자 *는 블로그의 blog 페이지를* 사용 하 여 블로그를 표시 하 고 올바른 범주나 날짜 범위를 가져오는 쿼리 문자열을 생성 해야 한다는 것을 알고 있어야 합니다. 두 번째 예제 집합은 이해 하 고 만드는 것이 훨씬 쉽습니다.

또한 첫 번째 예제에 대 한 Url은 특정 파일 (*블로그. cshtml*)을 직접 가리킵니다. 어떤 이유로 든 블로그를 서버의 다른 폴더로 이동 했거나 다른 페이지를 사용 하도록 블로그를 다시 작성 한 경우 링크가 잘못 된 것입니다. 두 번째 Url 집합은 특정 페이지를 가리키지 않으므로 블로그 구현이 나 위치가 변경 되더라도 Url은 여전히 유효 합니다.

ASP.NET는 *라우팅을*사용 하므로 ASP.NET 웹 페이지에서 위의 예제와 같은 친숙 한 url을 만들 수 있습니다. 라우팅은 URL에서 요청을 수행할 수 있는 페이지 (또는 페이지)로의 논리적 매핑을 만듭니다. 매핑은 논리적이 아닌 특정 파일에 대 한 논리적 이기 때문에 라우팅은 사이트의 Url을 정의 하는 방법에 뛰어난 유연성을 제공 합니다.

## <a name="how-routing-works"></a>라우팅 작동 방법

ASP.NET에서 요청을 처리 하는 경우 URL을 읽어 라우팅하는 방법을 결정 합니다. ASP.NET는 URL의 개별 세그먼트를 디스크의 파일 (왼쪽에서 오른쪽으로 이동)과 일치 시 키 려 고 시도 합니다. 일치 하는 항목이 있으면 URL에 남아 있는 항목이 *경로 정보*로 페이지에 전달 됩니다.

누군가가 다음 URL을 사용 하 여 요청을 한다고 가정 합니다.

`http://www.contoso.com/a/b/c`

검색은 다음과 같습니다.

1. */A/b/c.cshtml*경로와 이름을 가진 파일이 있나요? 이 경우 해당 페이지를 실행 하 고 정보를 전달 하지 않습니다. 기타...
2. */A/b.cshtml*경로와 이름을 가진 파일이 있나요? 이 경우 해당 페이지를 실행 하 여 `c` 값을 전달 합니다. 그렇지 않은 경우 ...
3. */A.cshtml*경로와 이름을 가진 파일이 있나요? 이 경우 해당 페이지를 실행 하 여 `b/c` 값을 전달 합니다.

지정 된 폴더에 있는 ASP.NET 파일에 *대해 정확* 하 게 일치 하는 항목이 검색에서 발견 된 경우에는 해당 파일을 계속 검색 합니다.

1. */a/b/c/default.cshtml* (경로 정보 없음).
2. */a/b/c/index.cshtml* (경로 정보 없음).

> [!NOTE]
> 명확 하 게 하기 위해 특정 페이지에 대 한 요청 (즉 *, 파일 확장명을 포함* 하는 요청)은 예상한 것과 똑같이 작동 합니다. `http://www.contoso.com/a/b.cshtml` 같은 요청은 b 페이지를 실행 합니다 *.*

페이지 내에서 페이지의 `UrlData` 속성 (사전)을 통해 경로 정보를 가져올 수 있습니다. 이름이 *Viewcustomers* 인 파일이 있고 사이트에서이 요청을 가져옵니다.

`http://mysite.com/myWebSite/ViewCustomers/1000`

위의 규칙에 설명 된 대로 요청이 페이지로 이동 합니다. 페이지 내에서 다음과 같은 코드를 사용 하 여 경로 정보를 가져오고 표시할 수 있습니다 (이 경우 값 &quot;1000&quot;).

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> 라우팅은 전체 파일 이름을 포함 하지 않으므로 이름이 같지만 파일 이름 확장명 (예: *m* 및 *m*)이 다른 페이지가 있는 경우 모호성이 있을 수 있습니다. 라우팅 문제를 방지 하기 위해 사이트에 이름이 서로 다른 페이지가 없는지 확인 하는 것이 가장 좋습니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

[WebMatrix-url, UrlData 및 SEO에 대 한 라우팅](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)입니다. Mike Brind의이 블로그 항목에서는 ASP.NET 웹 페이지에서 라우팅의 작동 방식에 대 한 추가 정보를 제공 합니다.
