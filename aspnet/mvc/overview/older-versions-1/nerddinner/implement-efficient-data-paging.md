---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 효율적인 데이터 페이징 구현 | Microsoft Docs
author: microsoft
description: 8 단계에서는 수천 개의 Dinners를 한 번에 표시 하는 대신/Dinners URL에 페이징 지원을 추가 하는 방법을 보여 줍니다. 여기서는 10 개의 예정 된 Dinners
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2d9a0dba381b71755ac626f76d52bc5bcb434447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486485"
---
# <a name="implement-efficient-data-paging"></a>효율적인 데이터 페이징 구현

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 8 단계입니다.
> 
> 8 단계에서는 수천 개의 Dinners를 한 번에 표시 하는 대신/Dinners URL에 페이징 지원을 추가 하는 방법을 보여 줍니다 .이 경우에는 한 번에 10 개의 Dinners를 표시 하 고 최종 사용자가 다시 SEO 방식으로 전체 목록에 대 한 페이지를 앞뒤로 이동할 수 있도록 합니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-8-paging-support"></a>NerdDinner Step 8: 페이징 지원

사이트가 성공적으로 완료 되 면 수천 개의 예정 된 dinners가 있습니다. 이러한 모든 dinners를 처리 하 고 사용자가 탐색할 수 있도록 UI를 확장 해야 합니다. 이를 사용 하도록 설정 하기 위해 */Dinners* URL에 대 한 페이징 지원을 추가 하 여 수천 개의 Dinners를 한 번에 표시 하 고, 최종 사용자가 다시 SEO 방식으로 전체 목록에 대해 페이지를 이동 하 고 전달할 수 있도록 합니다.

### <a name="index-action-method-recap"></a>Index () 동작 메서드 요약

현재, DinnersController 클래스 내의 Index () 동작 메서드는 다음과 같습니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

*/Dinners* URL에 대 한 요청이 이루어지면 예정 된 모든 Dinners 목록을 검색 한 다음 모든 항목의 목록을 렌더링 합니다.

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>IQueryable&lt;T&gt; 이해

*IQueryable&lt;t&gt;* 은 .net 3.5의 일부로 LINQ를 사용 하 여 도입 된 인터페이스입니다. 이를 통해 강력한 "지연 된 실행" 시나리오를 사용할 수 있습니다 .이 시나리오에서는를 활용 하 여 페이징 지원을 구현할 수 있습니다.

이 FindUpcomingDinners () 메서드에서 IQueryable&lt;Dinner&gt; 시퀀스를 반환 합니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

FindUpcomingDinners () 메서드에서 반환 하는 IQueryable&lt;Dinner&gt; 개체는 LINQ to SQL를 사용 하 여 데이터베이스에서 Dinner objects를 검색 하는 쿼리를 캡슐화 합니다. 중요 한 점은 쿼리의 데이터에 대 한 액세스/반복을 시도 하거나에 대해 ToList () 메서드를 호출할 때까지 데이터베이스에 대해 쿼리를 실행 하지 않는다는 것입니다. FindUpcomingDinners () 메서드를 호출 하는 코드는 쿼리를 실행 하기 전에 필요에 따라 IQueryable&lt;Dinner&gt; 개체에 "연결 된" 작업/필터를 추가 하도록 선택할 수 있습니다. 그런 다음 데이터가 요청 될 때 데이터베이스에 대해 결합 된 쿼리를 실행 하기에 충분 한 LINQ to SQL 합니다.

페이징 논리를 구현 하기 위해 다음에는 ToList ()를 호출 하기 전에 반환 된 IQueryable&lt;Dinner&gt; 시퀀스에 추가 "Skip" 및 "Take" 연산자를 적용 하도록 DinnersController의 Index () 동작 메서드를 업데이트할 수 있습니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

위의 코드는 데이터베이스에서 처음 10 개의 예정 된 dinners를 건너뛴 다음 백 20 dinners을 반환 합니다. LINQ to SQL는 웹 서버가 아닌 SQL database에서이 건너뛴 논리를 수행 하는 최적화 된 SQL 쿼리를 생성할 수 있을 정도로 지능적입니다. 즉, 데이터베이스에 수백만 개의 예정 된 Dinners가 있는 경우에도이 요청에 포함 된 10 개만 검색 됩니다 (효율적이 고 확장 가능).

### <a name="adding-a-page-value-to-the-url"></a>URL에 "page" 값 추가

특정 페이지 범위를 하드 코딩 하는 대신 Url에 사용자가 요청 하는 Dinner range를 나타내는 "page" 매개 변수를 포함 하도록 합니다.

#### <a name="using-a-querystring-value"></a>Querystring 값 사용

아래 코드에서는 querystring 매개 변수를 지원 하도록 Index () 작업 메서드를 업데이트 하 고 */Dinners? page = 2*와 같은 url을 사용 하도록 설정 하는 방법을 보여 줍니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

위의 Index () 동작 메서드에는 "page" 라는 매개 변수가 있습니다. 이 매개 변수는 nullable 정수로 선언 됩니다 (int?는이를 나타냄). 즉, */Dinners? page = 2* URL을 사용 하면 값이 "2"가 매개 변수 값으로 전달 됩니다. */Dinners* URL (querystring 값이 없는 경우)을 사용 하면 null 값이 전달 됩니다.

페이지 값을 페이지 크기 (이 경우 10 행)로 곱하여 건너뛸 dinners 수를 결정 합니다. Nullable 형식을 처리할 때 유용 하 게 사용 되는 [ C# null "병합" 연산자 (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) 를 사용 합니다. 위의 코드는 페이지 매개 변수가 null 인 경우 페이지 값을 0으로 지정 합니다.

#### <a name="using-embedded-url-values"></a>포함 된 URL 값 사용

Querystring 값을 사용 하는 대신 실제 URL 내에 페이지 매개 변수를 포함 하는 것이 좋습니다. 예: */Dinners/Page/2* 또는 */Dinners/2*. ASP.NET MVC에는 이와 같은 시나리오를 쉽게 지원할 수 있게 해 주는 강력한 URL 라우팅 엔진이 포함 되어 있습니다.

들어오는 모든 URL 또는 URL 형식을 원하는 컨트롤러 클래스나 작업 메서드에 매핑하는 사용자 지정 라우팅 규칙을 등록할 수 있습니다. 프로젝트 내에서 global.asax 파일을 열려면 다음을 수행 하기만 하면 됩니다.

![](implement-efficient-data-paging/_static/image2.png)

그런 다음 경로에 대 한 첫 번째 호출과 같은 MapRoute () 도우미 메서드를 사용 하 여 새 매핑 규칙을 등록 합니다. MapRoute ():

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

위에서 "UpcomingDinners" 라는 새 라우팅 규칙을 등록 합니다. URL 형식 "Dinners/Page/{page}"를 나타냅니다. 여기서 {Page}는 URL에 포함 된 매개 변수 값입니다. MapRoute () 메서드의 세 번째 매개 변수는이 형식과 일치 하는 Url을 DinnersController 클래스의 Index () 동작 메서드에 매핑해야 함을 나타냅니다.

Querystring 시나리오를 사용 하 여 이전에 했던 것과 정확히 동일한 인덱스 () 코드를 사용할 수 있습니다. 단, 지금은 "page" 매개 변수는 URL에서 제공 되 고 querystring은 제공 하지 않습니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

이제 응용 프로그램을 실행 하 고 */Dinners* 를 입력 하는 경우 처음 10 개의 예정 Dinners이 표시 됩니다.

![](implement-efficient-data-paging/_static/image3.png)

*/Dinners/Page/1* 을 입력 하면 Dinners의 다음 페이지가 표시 됩니다.

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>페이지 탐색 UI 추가

페이징 시나리오를 완료 하는 마지막 단계는 사용자가 Dinner data를 쉽게 건너뛸 수 있도록 보기 템플릿 내에서 "다음" 및 "이전" 탐색 UI를 구현 하는 것입니다.

이를 올바르게 구현 하려면 데이터베이스의 총 Dinners 수와이를 변환 하는 데이터 페이지 수를 알고 있어야 합니다. 그런 다음 현재 요청 된 "페이지" 값이 데이터의 시작 또는 끝에 있는지 여부를 계산 하 고 그에 따라 "이전" 및 "다음" UI를 표시 하거나 숨깁니다. Index () 작업 메서드 내에서이 논리를 구현할 수 있습니다. 또는 더 다시 사용할 수 있는 방식으로이 논리를 캡슐화 하는 도우미 클래스를 프로젝트에 추가할 수 있습니다.

다음은 .NET Framework 기본 제공 되는 목록&lt;T&gt; 컬렉션 클래스에서 파생 되는 간단한 "PaginatedList" 도우미 클래스입니다. 이 클래스는 IQueryable 데이터의 시퀀스를 다시 매기는 데 사용할 수 있는 다시 사용할 수 있는 컬렉션 클래스를 구현 합니다. 이러한 작업을 수행 하는 데 사용 되는&lt;Dinner&gt; 결과에 대해 IQueryable을 사용 하는 것이 좋지만, iqueryable&lt;Product&gt; 또는 IQueryable&lt;고객&gt; 다른 응용 프로그램 시나리오에 대 한 결과를 쉽게 사용할 수 있습니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

위에서 "PageIndex", "PageSize", "TotalCount" 및 "TotalPages"와 같은 속성을 계산 하 고 표시 하는 방법을 확인 합니다. 또한 컬렉션의 데이터 페이지가 원래 시퀀스의 시작 또는 끝에 있는지 여부를 나타내는 두 개의 도우미 속성인 "HasPreviousPage" 및 "HasNextPage"를 노출 합니다. 위의 코드는 두 개의 SQL 쿼리를 실행 하 여 두 개의 SQL 쿼리를 실행 합니다. 첫 번째는 Dinner objects의 총 수를 검색 하는 것입니다 .이는 개체를 반환 하지 않고 정수를 반환 하는 "SELECT COUNT" 문을 수행 하는 것이 고, 두 번째는의 행만 검색 하는 것입니다. 현재 데이터 페이지의 데이터베이스에서 필요한 데이터입니다.

그런 다음 FindUpcomingDinners () 결과에서 PaginatedList&lt;Dinner&gt;를 만들어이를 뷰 템플릿에 전달 하는 데 사용할 수 있습니다. Index () 도우미 메서드를 업데이트할 수 있습니다.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

그런 다음 \Views\Dinners\Index.aspx view 템플릿이 viewpage&lt;에서 상속 하도록 view 템플릿을 업데이트 하 고, IEnumerable&lt;Dinner&lt;&gt;하는 ViewPage 대신 PaginatedList&lt;Dinner&gt;&gt; 하 고, 다음 코드를 보기 템플릿 아래쪽에 추가 하 여 다음 및 이전 탐색 UI를 표시 하거나 숨길 수 있습니다.&gt;

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

위의 RouteLink () 도우미 메서드를 사용 하 여 하이퍼링크를 생성 하는 방법에 대해 알아봅니다. 이 메서드는 이전에 사용한 Html.actionlink () 도우미 메서드와 비슷합니다. 차이점은 Global.asax 파일 내에서 설정 하는 "UpcomingDinners" 라우팅 규칙을 사용 하 여 URL을 생성 한다는 것입니다. 이렇게 하면 */Dinners/Page/{page}* – 형식의 Index () 작업 메서드에 대 한 url을 생성할 수 있습니다. 여기서 {Page} 값은 현재 PageIndex를 기준으로 위에서 제공 하는 변수입니다.

이제 응용 프로그램을 다시 실행 하면 브라우저에서 한 번에 10 개의 dinners 표시 됩니다.

![](implement-efficient-data-paging/_static/image5.png)

또한 페이지 맨 아래에는 &lt;&lt;&lt; 하 고 &gt;&gt;검색 엔진 액세스 가능 Url을 사용 하 여 데이터를 앞뒤로 건너뛸 수 있습니다.&gt;

![](implement-efficient-data-paging/_static/image6.png)

| **측면 토픽: IQueryable&lt;T&gt;의 의미 이해** |
| --- |
| IQueryable&lt;T&gt;는 페이징 및 컴퍼지션 기반 쿼리와 같은 다양 한 흥미로운 지연 된 실행 시나리오를 가능 하 게 해 주는 매우 강력한 기능입니다. 모든 강력한 기능을 사용 하는 것과 마찬가지로 사용 하는 방법에 주의 하 여 악용 되지 않는지 확인 합니다. 리포지토리에서 IQueryable&lt;T&gt; 결과를 반환 한다는 것을 인식 하는 것이 중요 합니다 .이를 통해 호출 코드에서 연결 된 연산자 메서드를 추가 하 여 최종 쿼리 실행에 참여할 수 있습니다. 이러한 기능을 호출 하는 코드를 제공 하지 않으려는 경우 이미 실행 한 쿼리 결과를 포함 하는 IList&lt;T&gt; 또는 IEnumerable&lt;T&gt; 결과를 다시 반환 해야 합니다. 페이지 매김 시나리오의 경우 실제 데이터 페이지 매김 논리를 호출 되는 리포지토리 메서드에 푸시 해야 합니다. 이 시나리오에서는 FindUpcomingDinners () finder 메서드를 업데이트 하 여 PaginatedList를 반환 하는 서명을 포함할 수 있습니다. PaginatedList&lt; Dinner&gt; FindUpcomingDinners (int pageIndex, int pageSize) {} 또는 IList&lt;Dinner&gt;을 반환 하 고 "totalCount" out 매개 변수를 사용 하 여 총 Dinners: IList&lt;Dinner&gt; FindUpcomingDinners (int pageIndex, int pageSize, out int totalCount) {}을 반환 합니다. |

### <a name="next-step"></a>다음 단계

이제 응용 프로그램에 인증 및 권한 부여 지원을 추가 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](re-use-ui-using-master-pages-and-partials.md)
> [다음](secure-applications-using-authentication-and-authorization.md)
