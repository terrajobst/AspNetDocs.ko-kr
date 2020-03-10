---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: '7 부: 기능 추가 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 7 부에서는 계정 revie 같은 추가 기능을 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521567"
---
# <a name="part-7-adding-features"></a>7 부: 기능 추가

만든 사람 [Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다. ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 7 부에서는 계정 검토, 제품 리뷰, "인기 있는 항목" 및 "구매한" 사용자 정의 컨트롤 등의 추가 기능을 추가 합니다.

## <a id="_Toc260221673"></a>기능 추가

사용자는 카탈로그를 찾아보고, 장바구니에 항목을 저장 하 고, 체크 아웃 프로세스를 완료할 수 있지만 사이트 개선을 위해 포함할 수 있는 다양 한 지원 기능이 있습니다.

1. 계정 검토 (주문 나열 및 세부 정보 보기)
2. 일부 컨텍스트별 콘텐츠를 프런트 페이지에 추가 합니다.
3. 사용자가 카탈로그에서 제품을 검토할 수 있는 기능을 추가 합니다.
4. 인기 있는 항목을 표시 하 고 해당 컨트롤을 front 페이지에 넣는 사용자 정의 컨트롤을 만듭니다.
5. "구매한 항목" 사용자 정의 컨트롤을 만들고 제품 정보 페이지에 추가 합니다.
6. 연락처 페이지를 추가 합니다.
7. 정보 페이지를 추가 합니다.
8. 전역 오류

## <a id="_Toc260221674"></a>계정 검토

"Account" 폴더에서 OrderDetails 라는 두 개의 .aspx 페이지를 만듭니다.

OrderList .aspx는 이전에 했던 것 처럼 GridView 및 EntityDataSource 컨트롤을 활용 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

EntityDataSource은 사용자가 로그인 할 때 세션 변수에 설정 된 사용자 이름 (WhereParameter 참조)에 대해 필터링 된 Orders 테이블에서 레코드를 선택 합니다.

또한 GridView의 하이퍼링크 필드에는 다음 매개 변수가 있습니다.

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

이는 OrderID 필드를 OrderDetails 페이지에 대 한 QueryString 매개 변수로 지정 하는 각 제품에 대 한 주문 정보 뷰에 대 한 링크를 지정 합니다.

## <a id="_Toc260221675"></a>OrderDetails

EntityDataSource 컨트롤을 사용 하 여 주문 데이터를 표시 하 고 FormView를 사용 하 여 주문 데이터를 표시 하 고 다른 EntityDataSource GridView를 사용 하 여 모든 주문의 줄 항목을 표시 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

코드 숨김이 파일 (OrderDetails.aspx.cs)에는 두 가지 약간의 정리 작업이 있습니다.

먼저 OrderDetails가 항상 OrderId를 사용 하도록 해야 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

또한 품목에서 주문 합계를 계산 하 여 표시 해야 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a>홈 페이지

Default.aspx 페이지에 일부 정적 콘텐츠를 추가 해 보겠습니다.

먼저 "Content" 폴더와이 폴더 내에 이미지 폴더를 만듭니다. 홈 페이지에서 사용할 이미지를 포함 합니다.

Default.aspx 페이지의 아래쪽 자리 표시자에 다음 태그를 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a>제품 리뷰

먼저 제품 검토를 시작 하는 데 사용할 수 있는 폼에 대 한 링크를 포함 하는 단추를 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

쿼리 문자열에 ProductID를 전달 합니다.

그런 다음 ReviewAdd 이라는 추가 페이지가 있습니다.

이 페이지에서는 ASP.NET AJAX 컨트롤 도구 키트를 사용 합니다. 아직 수행 하지 않은 경우 [Devexpress](http://devexpress.com/act) 에서 다운로드할 수 있습니다. 여기 [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)에서 Visual Studio와 함께 사용할 도구 키트를 설정 하는 방법에 대 한 지침이 있습니다.

디자인 모드에서 도구 상자의 컨트롤 및 유효성 검사기를 끌고 아래와 같은 폼을 작성 합니다.

![](tailspin-spyworks-part-7/_static/image2.jpg)

태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

이제 리뷰를 입력할 수 있으므로 제품 페이지에 해당 리뷰를 표시할 수 있습니다.

이 태그를 제품 세부 정보 .aspx 페이지에 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

지금 응용 프로그램을 실행 하 고 제품으로 이동 하면 고객 리뷰를 비롯 한 제품 정보가 표시 됩니다.

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a>인기 있는 항목 컨트롤 (사용자 정의 컨트롤 만들기)

웹 사이트에서 판매를 증가 시키기 위해 인기 있거나 관련 된 제품을 "추천 판매" 하는 두 가지 기능을 추가 합니다.

이러한 기능 중 첫 번째 기능은 제품 카탈로그의 인기 제품 목록입니다.

응용 프로그램의 홈 페이지에 상위 판매 항목을 표시 하는 "사용자 정의 컨트롤"을 만듭니다. 이 컨트롤은 컨트롤이 되기 때문에 Visual Studio 디자이너의 컨트롤을 원하는 페이지에 끌어서 놓는 방법으로 페이지에서 사용할 수 있습니다.

Visual Studio의 솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭 하 고 "Controls" 라는 새 디렉터리를 만듭니다. 이 작업을 수행할 필요는 없지만 "Controls" 디렉터리에 모든 사용자 정의 컨트롤을 만들어 프로젝트를 구성 하는 데 도움이 됩니다.

Controls 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 항목"을 선택 합니다.

![](tailspin-spyworks-part-7/_static/image4.jpg)

"PopularItems" 컨트롤의 이름을 지정 합니다. 사용자 정의 컨트롤용 파일 확장명은 .aspx이 아닙니다.

인기 있는 항목 사용자 정의 컨트롤은 다음과 같이 정의 됩니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

여기서는이 응용 프로그램에서 아직 사용 하지 않은 메서드를 사용 하 고 있습니다. Repeater 컨트롤을 사용 하는 대신, 데이터 소스 컨트롤을 사용 하는 대신 Repeater 컨트롤을 LINQ to Entities 쿼리의 결과에 바인딩합니다.

컨트롤의 코드 뒤에서 다음과 같이 작업을 수행 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

컨트롤 태그의 위쪽에 있는이 중요 한 줄도 확인 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

가장 인기 있는 항목은 분 단위로 변경 되지 않으므로 응용 프로그램의 성능을 향상 시키기 위해 aching 지시어를 추가할 수 있습니다. 이 지시문을 통해 컨트롤 코드는 캐시 된 컨트롤의 출력이 만료 될 때만 실행 됩니다. 그렇지 않으면 캐시 된 버전의 컨트롤 출력이 사용 됩니다.

이제 Default.aspx 페이지에 새로운 컨트롤을 포함 하기만 하면 됩니다.

끌어서 놓기를 사용 하 여 컨트롤의 인스턴스를 기본 폼의 열린 열에 놓습니다.

![](tailspin-spyworks-part-7/_static/image5.jpg)

이제 응용 프로그램을 실행할 때 홈 페이지에 가장 인기 있는 항목이 표시 됩니다.

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a>"구매한 사용자 정의 컨트롤 (매개 변수가 있는 사용자 정의 컨트롤)

만들 두 번째 사용자 정의 컨트롤은 컨텍스트 특이성를 추가 하 여 다음 수준으로 판매 하는 추천을 가져옵니다.

상위 "구매한" 항목을 계산 하는 논리는 trivial이 아닙니다.

"또한 구매한" 제어는 현재 선택 된 ProductID에 대 한 OrderDetails 레코드 (이전에 구매한)를 선택 하 고 발견 되는 각각의 고유한 주문에 대해 OrderIDs를 가져옵니다.

그런 다음 모든 주문에서 제품을 al으로 선택 하 고 구매한 수량을 합산 합니다. 이 수량 합계를 기준으로 제품을 정렬 하 고 상위 5 개 항목을 표시 합니다.

이 논리의 복잡성을 고려 하 여이 알고리즘을 저장 프로시저로 구현할 것입니다.

저장 프로시저에 대 한 T-sql은 다음과 같습니다.

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

이 저장 프로시저 (SelectPurchasedWithProducts)는 응용 프로그램에 포함 했을 때 데이터베이스에 있었지만, 필요한 테이블 및 뷰 외에도 지정 된 엔터티 데이터 모델를 생성 한 경우 엔터티 데이터 모델 이 저장 프로시저를 포함 해야 합니다.

엔터티 데이터 모델에서 저장 프로시저에 액세스 하려면 함수를 가져와야 합니다.

솔루션 탐색기에서 엔터티 데이터 모델을 두 번 클릭 하 여 디자이너에서 열고 모델 브라우저를 연 다음 디자이너를 마우스 오른쪽 단추로 클릭 하 고 "함수 가져오기 추가"를 선택 합니다.

![](tailspin-spyworks-part-7/_static/image1.png)

이렇게 하면이 대화 상자가 열립니다.

![](tailspin-spyworks-part-7/_static/image2.png)

위에 표시 된 대로 필드를 입력 하 고, "SelectPurchasedWithProducts"를 선택 하 고, 가져온 함수의 이름에 프로시저 이름을 사용 합니다.

"확인"을 클릭 합니다.

이 작업을 수행 하면 모델의 다른 항목을 비롯 하 여 저장 프로시저를 간단히 프로그래밍할 수 있습니다.

따라서 "Controls" 폴더에서 AlsoPurchased 이라는 새 사용자 정의 컨트롤을 만듭니다.

이 컨트롤에 대 한 태그는 PopularItems 컨트롤에 매우 익숙할 것입니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

주목할 만한 차이점은 렌더링 될 항목의 수는 제품 마다 다르므로 출력을 캐싱하지 않는다는 것입니다.

ProductId는 컨트롤에 대 한 "속성"이 됩니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

컨트롤의 PreRender 이벤트 처리기에서 3 가지 작업을 수행 하는 것을 eed.

1. ProductID가 설정 되어 있는지 확인 합니다.
2. 현재 제품으로 구매한 제품이 있는지 확인 합니다.
3. #2에서 결정 된 일부 항목을 출력 합니다.

모델을 통해 저장 프로시저를 호출 하는 것이 얼마나 쉬운지 확인 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

"구매"를 확인 한 후에는 쿼리에 의해 반환 된 결과에만 repeater를 바인딩할 수 있습니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

"구매한 항목" 항목이 없는 경우 카탈로그에서 다른 인기 항목을 표시 합니다.

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

"구매한 항목" 항목을 보려면 제품 세부 정보 .aspx 페이지를 열고 솔루션 탐색기에서 AlsoPurchased 컨트롤을 끌어 태그의이 위치에 표시 되도록 합니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

이렇게 하면 제품 세부 정보 페이지의 맨 위에 있는 컨트롤에 대 한 참조가 생성 됩니다.

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

AlsoPurchased 사용자 정의 컨트롤에 ProductId 숫자가 필요 하므로 페이지의 현재 데이터 모델 항목에 대 한 Eval 문을 사용 하 여 컨트롤의 ProductID 속성을 설정 합니다.

![](tailspin-spyworks-part-7/_static/image3.png)

지금 빌드하고 실행 하 여 제품으로 이동 하면 "구매한 항목" 항목이 표시 됩니다.

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-6.md)
> [다음](tailspin-spyworks-part-8.md)
