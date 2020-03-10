---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: '7 부: 기본 페이지 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484451"
---
# <a name="part-7-creating-the-main-page"></a>7 부: 기본 페이지 만들기

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>기본 페이지 만들기

이 섹션에서는 주 응용 프로그램 페이지를 만듭니다. 이 페이지는 관리 페이지 보다 복잡 하므로 여러 단계로 접근 합니다. 이 과정에서 몇 가지 고급에 대 한 몇 가지 고급 녹아웃 기술이 표시 됩니다. 페이지의 기본 레이아웃은 다음과 같습니다.

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- "Products"는 제품 배열을 보유 합니다.
- "카트"는 수량이 포함 된 제품의 배열을 보유 합니다. "카트에 추가"를 클릭 하면 카트를 업데이트 합니다.
- "Orders"는 주문 Id의 배열을 보유 합니다.
- "세부 정보"는 항목 배열 (수량이 있는 제품) 인 주문 세부 정보를 포함 합니다.

데이터 바인딩이나 스크립트 없이 HTML에서 몇 가지 기본 레이아웃을 정의 하는 것부터 시작 합니다. 파일 Views/Home/Index를 열고 모든 내용을 다음으로 바꿉니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

다음으로 스크립트 섹션을 추가 하 고 빈 뷰-모델을 만듭니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

이전에 스케치 된 디자인을 기반으로 하는 보기 모델에는 제품, 카트, 주문 및 세부 정보에 대 한 관찰 가능 개체 필요 합니다. `AppViewModel` 개체에 다음 변수를 추가 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

사용자는 제품 목록의 항목을 카트에 추가 하 고 카트에 항목을 제거할 수 있습니다. 이러한 함수를 캡슐화 하기 위해 제품을 나타내는 또 다른 뷰 모델 클래스를 만듭니다. 다음 코드를 `AppViewModel`에 추가합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

`ProductViewModel` 클래스에는 카트에 제품을 이동 하는 데 사용 되는 두 개의 함수가 포함 되어 있습니다. `addItemToCart`는 제품의 한 단위를 카트에 추가 하 고 `removeAllFromCart` 제품의 모든 수량을 제거 합니다.

사용자는 기존 주문을 선택 하 고 주문 세부 정보를 가져올 수 있습니다. 이 기능은 다른 보기-모델에 캡슐화 됩니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

`OrderDetailsViewModel`은 순서로 초기화 되며 서버에 AJAX 요청을 전송 하 여 주문 정보를 페치합니다.

또한 `OrderDetailsViewModel`에 `total` 속성이 있는지 확인 합니다. 이 속성은 [계산 된 관찰](http://knockoutjs.com/documentation/computedObservables.html)가능 이라고 하는 특수 한 종류의 관찰 가능입니다. 이름에서 알 수 있듯이 계산 된 관찰 가능을 통해 계산 된 값&#8212;(이 경우 주문의 총 비용)에 데이터를 바인딩할 수 있습니다.

그런 다음 `AppViewModel`에 다음 함수를 추가 합니다.

- `resetCart` 카트에 있는 모든 항목을 제거 합니다.
- `getDetails`는 주문에 대 한 세부 정보를 가져옵니다 (`details` 목록에 새 `OrderDetailsViewModel` 푸시).
- `createOrder` 새 주문을 만들고 카트를 비웁니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

마지막으로 제품 및 주문에 대 한 AJAX 요청을 작성 하 여 뷰 모델을 초기화 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

코드는 많지만,이를 단계별로 작성 했으므로 디자인을 명확 하 게 만들 수 있습니다. 이제 HTML에 일부 녹아웃 바인딩을 추가할 수 있습니다.

**제품**

제품 목록에 대 한 바인딩은 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

이는 products 배열을 반복 하 고 이름 및 가격을 표시 합니다. "주문에 추가" 단추는 사용자가 로그인 한 경우에만 표시 됩니다.

"주문에 추가" 단추는 제품의 `ProductViewModel` 인스턴스에서 `addItemToCart`를 호출 합니다. 이는 녹아웃의 유용한 기능을 보여 줍니다. 뷰 모델에 다른 뷰 모델이 포함 되어 있으면 바인딩을 내부 모델에 적용할 수 있습니다. 이 예에서는 `foreach` 내의 바인딩이 각 `ProductViewModel` 인스턴스에 적용 됩니다. 이 방법은 모든 기능을 단일 뷰 모델에 배치 하는 것 보다 훨씬 더 간단 합니다.

**마차**

카트에 대 한 바인딩은 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

그러면 카트 배열을 반복 하 고 이름, 가격 및 수량을 표시 합니다. "제거" 링크와 "주문 만들기" 단추는 뷰 모델 함수에 바인딩되어 있습니다.

**주문과**

주문 목록에 대 한 바인딩은 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

주문을 반복 하 고 주문 ID를 표시 합니다. 링크의 click 이벤트는 `getDetails` 함수에 바인딩됩니다.

**주문 정보**

주문 정보에 대 한 바인딩은 다음과 같습니다.

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

그러면 주문의 항목을 반복 하 여 제품, 가격 및 수량을 표시 합니다. 주변 div는 세부 정보 배열에 하나 이상의 항목이 포함 된 경우에만 표시 됩니다.

## <a name="conclusion"></a>결론

이 자습서에서는 Entity Framework를 사용 하 여 데이터베이스와 통신 하는 응용 프로그램을 만들고 ASP.NET Web API 데이터 계층 위에 공용 인터페이스를 제공 합니다. ASP.NET MVC 4를 사용 하 여 HTML 페이지를 렌더링 하 고, .js와 jQuery를 사용 하 여 페이지를 다시 로드 하지 않고 동적 상호 작용을 제공 합니다.

추가 리소스:

- [ASP.NET 데이터 액세스 내용 맵](https://msdn.microsoft.com/library/6759sth4.aspx)
- [Entity Framework 개발자 센터](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-6.md)
