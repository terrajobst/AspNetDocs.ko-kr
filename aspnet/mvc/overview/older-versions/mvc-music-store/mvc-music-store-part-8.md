---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: '8 부: Ajax 업데이트가 포함 된 쇼핑 카트 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 8 부에서는 Ajax 업데이트가 포함 된 쇼핑 카트를 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433517"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a>8 부: Ajax 업데이트가 포함 된 쇼핑 카트

받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.  
>   
> MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 8 부에서는 Ajax 업데이트가 포함 된 쇼핑 카트를 다룹니다.

사용자가 등록 하지 않고 카트에 앨범을 저장할 수 있지만 체크 아웃을 완료 하려면 게스트로 등록 해야 합니다. 쇼핑 및 체크 아웃 프로세스는 두 개의 컨트롤러로 구분 됩니다. ShoppingCart Controller는 장바구니에 항목을 익명으로 추가할 수 있으며, 체크 아웃 프로세스를 처리 하는 체크 아웃 컨트롤러를 사용 합니다. 이 섹션에서 쇼핑 카트를 시작 하 고 다음 섹션에서 체크 아웃 프로세스를 빌드합니다.

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a>카트, 주문 및 OrderDetail 모델 클래스 추가

쇼핑 카트 및 체크 아웃 프로세스는 일부 새로운 클래스를 사용 합니다. 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 다음 코드를 사용 하 여 Cart 클래스 (Cart.cs)를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

이 클래스는 RecordId 속성에 대 한 [Key] 특성을 제외 하 고 지금까지 사용한 다른 다른 클래스와 매우 비슷합니다. 카트 항목에는 익명 쇼핑을 허용 하는 CartID 라는 문자열 식별자가 있지만 테이블에는 RecordId 라는 정수 기본 키가 포함 되어 있습니다. Entity Framework 규칙에 따라 코드 우선에는 Cart 라는 테이블의 기본 키가 CartId 또는 ID가 될 것으로 예상 되지만, 원하는 경우 주석이 나 코드를 통해 쉽게 재정의할 수 있습니다. 이는 Entity Framework 코드에서 간단한 규칙을 사용 하는 방법에 대 한 예입니다. 첫 번째 규칙을 사용 하는 경우에는 사용 하지 않는 것이 좋습니다.

다음으로, 다음 코드를 사용 하 여 Order 클래스 (Order.cs)를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

이 클래스는 주문의 요약 및 배달 정보를 추적 합니다. 아직 만들지 않은 클래스에 종속 된 OrderDetails 탐색 속성이 있으므로 **아직 컴파일되지 않습니다**. 이제 OrderDetail.cs 라는 클래스를 추가 하 고 다음 코드를 추가 하 여이를 수정 하겠습니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

MusicStoreEntities 클래스에 대 한 마지막 업데이트 중 하나는 Dbsets&lt;음악가&gt;포함 하 여 새 모델 클래스를 노출 하는 DbSets를 포함 하는 것입니다. 업데이트 된 MusicStoreEntities 클래스는 아래와 같이 표시 됩니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a>쇼핑 카트 비즈니스 논리 관리

다음으로 모델 폴더에 ShoppingCart 클래스를 만듭니다. ShoppingCart 모델은 Cart 테이블에 대 한 데이터 액세스를 처리 합니다. 또한 쇼핑 카트에 항목을 추가 하 고 제거 하는 비즈니스 논리를 처리 합니다.

사용자가 장바구니에 항목을 추가 하기 위해 계정에 등록 하도록 요구 하지 않기 때문에 사용자가 쇼핑 카트에 액세스할 때 GUID 또는 GUID (globally unique identifier)를 사용 하 여 사용자에 게 임시 고유 식별자를 할당 합니다. ASP.NET Session 클래스를 사용 하 여이 ID를 저장 합니다.

*참고: ASP.NET 세션은 사이트를 떠날 때 만료 되는 사용자 관련 정보를 저장 하는 편리한 장소입니다. 세션 상태를 잘못 사용 하는 것은 대규모 사이트에서 성능에 영향을 미칠 수 있지만, 데모용으로 사용 하는 것은 데모용입니다.*

ShoppingCart 클래스는 다음 메서드를 노출 합니다.

기능 **카트** 는 앨범을 매개 변수로 사용 하 여 사용자의 카트에 추가 합니다. 카트 테이블은 각 앨범의 수량을 추적 하므로 필요한 경우 새 행을 만들기 위한 논리를 포함 하거나 사용자가 이미 앨범 복사본 하나를 주문한 경우에만 수량을 증가 시킵니다.

**RemoveFromCart** 는 앨범 ID를 사용 하 여 사용자의 카트에 제거 합니다. 사용자가 카트에 앨범 복사본을 하나만 포함 하는 경우 행이 제거 됩니다.

**EmptyCart** 사용자의 쇼핑 카트에 있는 모든 항목을 제거 합니다.

**Getcartitems** 는 표시 또는 처리를 위해 cartitems 목록을 검색 합니다.

**Getcount** 는 사용자가 쇼핑 카트에 있는 총 앨범 수를 검색 합니다.

**Gettotal** 은 카트에 있는 모든 항목의 총 비용을 계산 합니다.

**Createorder** 는 체크 아웃 단계에서 쇼핑 카트를 주문으로 변환 합니다.

**Getcart** 는 컨트롤러에서 카트 개체를 얻을 수 있도록 하는 정적 메서드입니다. **Getcartid** 메서드를 사용 하 여 사용자 세션에서 cartid 읽기를 처리 합니다. GetCartId 메서드는 사용자의 세션에서 사용자의 CartId를 읽을 수 있도록 HttpContextBase를 요구 합니다.

전체 **ShoppingCart 클래스**는 다음과 같습니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a>ViewModels

쇼핑 카트 컨트롤러는 모델 개체에 명확 하 게 매핑되지 않는 일부 복잡 한 정보를 보기에 전달 해야 합니다. 보기에 맞게 모델을 수정 하지 않으려고 합니다. 모델 클래스는 사용자 인터페이스가 아니라 도메인을 나타내야 합니다. 저장소 관리자 드롭다운 정보에서와 같이 ViewBag 클래스를 사용 하 여 보기에 정보를 전달 하는 것이 한 가지 해결 방법 이지만 ViewBag를 통해 많은 정보를 전달 하는 것은 관리 하기가 어렵습니다.

이에 대 한 해결 방법은 *ViewModel* 패턴을 사용 하는 것입니다. 이 패턴을 사용 하는 경우 특정 뷰 시나리오에 최적화 된 강력한 형식의 클래스를 만들고, 뷰 템플릿에 필요한 동적 값/콘텐츠에 대 한 속성을 노출 합니다. 그러면 컨트롤러 클래스는 이러한 뷰 최적화 클래스를 채우고 사용할 뷰 템플릿으로 전달할 수 있습니다. 이렇게 하면 보기 템플릿 내에서 형식 안전성, 컴파일 시간 검사 및 편집기 IntelliSense를 사용할 수 있습니다.

쇼핑 카트 컨트롤러에서 사용할 두 가지 뷰 모델을 만듭니다. ShoppingCartViewModel는 사용자의 쇼핑 카트 콘텐츠를 보유 하 고, ShoppingCartRemoveViewModel는 사용자가 항목을 제거할 때 확인 정보를 표시 하는 데 사용 됩니다. 카트를 시작 합니다.

구성 된 상태를 유지 하기 위해 프로젝트의 루트에 새 ViewModels 폴더를 만들어 보겠습니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 추가/새 폴더를 선택 합니다.

![](mvc-music-store-part-8/_static/image1.jpg)

폴더 이름을 ViewModels으로 합니다.

![](mvc-music-store-part-8/_static/image1.png)

다음으로 ViewModels 폴더에 ShoppingCartViewModel 클래스를 추가 합니다. 여기에는 카트 항목의 목록 및 카트에 있는 모든 항목의 총 가격을 포함 하는 10 진수 값 이라는 두 가지 속성이 있습니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

이제 다음 네 가지 속성을 사용 하 여 ShoppingCartRemoveViewModel를 ViewModels 폴더에 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a>쇼핑 카트 컨트롤러

쇼핑 카트 컨트롤러에는 카트에 항목 추가, 카트에 항목 제거, 카트에 있는 항목 보기의 세 가지 주요 목적이 있습니다. ShoppingCartViewModel, ShoppingCartRemoveViewModel 및 ShoppingCart 라는 세 개의 클래스를 사용 합니다. StoreController 및 StoreManagerController와 마찬가지로 MusicStoreEntities의 인스턴스를 포함 하는 필드를 추가 합니다.

빈 컨트롤러 템플릿을 사용 하 여 프로젝트에 새 쇼핑 카트 컨트롤러를 추가 합니다.

![](mvc-music-store-part-8/_static/image2.png)

전체 ShoppingCart 컨트롤러는 다음과 같습니다. 인덱스 및 컨트롤러 추가 작업은 매우 익숙할 것입니다. 제거 및 Carttsummary 컨트롤러 작업은 다음 섹션에서 설명 하는 두 가지 특수 한 경우를 처리 합니다.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a>JQuery를 사용 하 여 Ajax 업데이트

다음으로 ShoppingCartViewModel에 강력한 형식의 쇼핑 카트 인덱스 페이지를 만들고 이전과 동일한 방법으로 목록 뷰 템플릿을 사용 합니다.

![](mvc-music-store-part-8/_static/image3.png)

그러나이 경우에는 html.actionlink를 사용 하 여 카트에 항목을 제거 하는 대신 jQuery를 사용 하 여이 보기의 모든 링크에 대 한 click 이벤트를 "연결" 하 여 HTML 클래스 RemoveLink를 사용 합니다. 이 click 이벤트 처리기는 폼을 게시 하는 대신 RemoveFromCart controller 동작에 대 한 AJAX 콜백을 만듭니다. RemoveFromCart는 JSON 직렬화 된 결과를 반환 합니다. 그러면 jQuery 콜백은 jQuery를 사용 하 여 페이지에 대 한 4 개의 빠른 업데이트를 구문 분석 하 고 수행 합니다.

- 1. 삭제 된 앨범을 목록에서 제거 합니다.
- 2. 헤더의 카트 수를 업데이트 합니다.
- 3. 사용자에 게 업데이트 메시지를 표시 합니다.
- 4. 카트 총 가격을 업데이트 합니다.

제거 시나리오는 인덱스 뷰 내에서 Ajax 콜백에 의해 처리 되므로 RemoveFromCart 작업에 대 한 추가 뷰는 필요 하지 않습니다. /ShoppingCart/Index 뷰에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

이를 테스트 하기 위해 쇼핑 카트에 항목을 추가할 수 있어야 합니다. "장바구니에 추가" 단추를 포함 하도록 **매장 세부 정보** 보기를 업데이트 합니다. 여기서는이 보기를 마지막으로 업데이트 한 이후 추가 된 앨범 추가 정보 (장르, 음악가, 가격 및 앨범 아트)를 포함할 수 있습니다. 업데이트 된 저장소 세부 정보 보기 코드는 아래와 같이 표시 됩니다.

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

이제 스토어를 클릭 하 고 쇼핑 카트에 앨범 추가 및 제거를 테스트할 수 있습니다. 응용 프로그램을 실행 하 고 저장소 인덱스를 찾습니다.

![](mvc-music-store-part-8/_static/image4.png)

다음으로, 장르를 클릭 하 여 앨범 목록을 봅니다.

![](mvc-music-store-part-8/_static/image5.png)

이제 앨범 제목을 클릭 하면 "장바구니에 추가" 단추를 포함 하 여 업데이트 된 앨범 세부 정보 보기가 표시 됩니다.

![](mvc-music-store-part-8/_static/image6.png)

"카트에 추가" 단추를 클릭 하면 장바구니 요약 목록이 포함 된 쇼핑 카트 인덱스 보기가 표시 됩니다.

![](mvc-music-store-part-8/_static/image7.png)

쇼핑 카트를 로드 한 후 카트에서 제거 링크를 클릭 하 여 쇼핑 카트에 Ajax 업데이트를 볼 수 있습니다.

![](mvc-music-store-part-8/_static/image8.png)

등록 되지 않은 사용자가 카트에 항목을 추가할 수 있도록 하는 작업 중인 장바구니를 구축 했습니다. 다음 섹션에서는 체크 아웃 프로세스를 등록 하 고 완료할 수 있도록 허용 합니다.

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-7.md)
> [다음](mvc-music-store-part-9.md)
