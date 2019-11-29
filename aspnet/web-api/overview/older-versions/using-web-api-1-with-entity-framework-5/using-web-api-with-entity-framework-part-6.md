---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: '6 부: 제품 및 주문 컨트롤러 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600023"
---
# <a name="part-6-creating-product-and-order-controllers"></a>6 부: 제품 및 주문 컨트롤러 만들기

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a>제품 컨트롤러 추가

관리자 컨트롤러는 관리자 권한을 가진 사용자를 위한 것입니다. 반면, 고객은 제품을 볼 수 있지만 생성, 업데이트 또는 삭제할 수는 없습니다.

Get 메서드를 열어 둔 상태에서 Post, Put 및 Delete 메서드에 대 한 액세스를 쉽게 제한할 수 있습니다. 그러나 제품에 대해 반환 되는 데이터를 확인 합니다.

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

`ActualCost` 속성은 고객에 게 표시 되지 않아야 합니다. 이 솔루션은 고객에 게 표시 되는 속성의 하위 집합을 포함 하는 DTO ( *데이터 전송 개체* )를 정의 하는 것입니다. LINQ to project `Product` 인스턴스를 사용 하 여 인스턴스를 `ProductDTO` 합니다.

`ProductDTO` 라는 클래스를 모델 폴더에 추가 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

이제 컨트롤러를 추가 합니다. 솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. **추가**를 선택한 다음 **컨트롤러**를 선택 합니다. **컨트롤러 추가** 대화 상자에서 컨트롤러 이름을 ProductsController&quot;로 &quot;합니다. **템플릿**아래에서 **빈 API 컨트롤러**를 선택 합니다.

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

소스 파일의 모든 항목을 다음 코드로 바꿉니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

컨트롤러는 여전히 `OrdersContext`를 사용 하 여 데이터베이스를 쿼리 합니다. 그러나 `Product` 인스턴스를 직접 반환 하는 대신 `MapProducts`를 호출 하 여 `ProductDTO` 인스턴스에 프로젝션 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

`MapProducts` 메서드는 **IQueryable**을 반환 하므로 다른 쿼리 매개 변수를 사용 하 여 결과를 작성할 수 있습니다. 쿼리에 **where** 절을 추가 하는 `GetProduct` 메서드에서이를 확인할 수 있습니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a>주문 컨트롤러 추가

그런 다음 사용자가 주문을 만들고 볼 수 있도록 하는 컨트롤러를 추가 합니다.

다른 DTO 시작 합니다. 솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 하 `OrderDTO` 라는 클래스를 추가 합니다. 다음 구현을 사용 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

이제 컨트롤러를 추가 합니다. 솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. **추가**를 선택한 다음 **컨트롤러**를 선택 합니다. **컨트롤러 추가** 대화 상자에서 다음 옵션을 설정 합니다.

- **컨트롤러 이름**에 "OrdersController"를 입력 합니다.
- **템플릿**에서 "Entity Framework 사용 하 여 읽기/쓰기 작업을 포함 하는 API 컨트롤러를 선택 합니다.
- **모델 클래스**에서 &quot;Order (제품 스토어. 모델)&quot;를 선택 합니다.
- **데이터 컨텍스트 클래스**에서 &quot;OrdersContext (제품 스토어. 모델)&quot;를 선택 합니다.

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

**추가**를 클릭합니다. 그러면 이름이 OrdersController.cs 인 파일이 추가 됩니다. 다음에는 컨트롤러의 기본 구현을 수정 해야 합니다.

먼저 `PutOrder` 및 `DeleteOrder` 메서드를 삭제 합니다. 이 샘플에서는 고객이 기존 주문을 수정 하거나 삭제할 수 없습니다. 실제 응용 프로그램에서는 이러한 경우를 처리 하는 백 엔드 논리가 많이 필요 합니다. (예를 들어 주문이 이미 배송 되었습니까?)

사용자에 게 속한 주문만 반환 하도록 `GetOrders` 메서드를 변경 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

`GetOrder` 메서드를 다음과 같이 변경 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

다음은 메서드에 적용 된 변경 내용입니다.

- 반환 값은 `Order`대신 `OrderDTO` 인스턴스입니다.
- 주문에 대 한 데이터베이스를 쿼리할 때 [Dbquery. Include](https://msdn.microsoft.com/library/gg696395) 메서드를 사용 하 여 관련 `OrderDetail` 및 `Product` 엔터티를 인출 합니다.
- 프로젝션을 사용 하 여 결과를 평면화 합니다.

HTTP 응답은 수량을 포함 하는 제품 배열을 포함 합니다.

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

이 형식은 클라이언트에서 중첩 된 엔터티 (주문, 세부 정보 및 제품)를 포함 하는 원래 개체 그래프 보다 더 쉽게 사용할 수 있습니다.

이 `PostOrder`가장 먼저 고려해 야 할 메서드입니다. 현재이 메서드는 `Order` 인스턴스를 사용 합니다. 그러나 클라이언트에서 다음과 같이 요청 본문을 보내는 경우에는 어떻게 되는지 고려해 야 합니다.

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

이는 잘 구성 된 순서 이며, Entity Framework는이를 데이터베이스에 삽입 합니다. 하지만 이전에 존재 하지 않았던 제품 엔터티를 포함 합니다. 클라이언트는 데이터베이스에 새 제품을 만들었습니다. 이는 koala의 주문에 대 한 주문이 표시 되는 주문 처리 부서에서 발생 합니다. 도덕적는 POST 또는 PUT 요청에서 허용 하는 데이터에 대 한 주의를 기울여야 합니다.

이 문제를 방지 하려면 `PostOrder` 메서드를 변경 하 여 `OrderDTO` 인스턴스를 사용 합니다. `OrderDTO`를 사용 하 여 `Order`를 만듭니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

`ProductID` 및 `Quantity` 속성을 사용 하며, 클라이언트에서 제품 이름 또는 가격 중 하나에 대해 보낸 값을 무시 합니다. 제품 ID가 유효 하지 않은 경우 데이터베이스의 foreign key 제약 조건을 위반 하 고 삽입이 실패 하 게 됩니다.

다음은 전체 `PostOrder` 메서드입니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

마지막으로 **권한 부여** 특성을 컨트롤러에 추가 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

이제 등록 된 사용자만 주문을 만들거나 볼 수 있습니다.

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-5.md)
> [다음](using-web-api-with-entity-framework-part-7.md)
