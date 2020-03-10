---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: '9 부: 등록 및 체크 아웃 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 9 부에서는 등록 및 체크 아웃을 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450899"
---
# <a name="part-9-registration-and-checkout"></a>9 부: 등록 및 체크 아웃

받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.  
>   
> MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 9 부에서는 등록 및 체크 아웃을 다룹니다.

이 섹션에서는 쇼핑객의 주소 및 지불 정보를 수집 하는 CheckoutController를 만듭니다. 사용자는 체크 아웃 하기 전에 사이트에 등록 해야 하므로이 컨트롤러는 권한 부여가 필요 합니다.

사용자는 "체크 아웃" 단추를 클릭 하 여 쇼핑 카트에서 체크 아웃 프로세스로 이동 합니다.

![](mvc-music-store-part-9/_static/image1.jpg)

사용자가 로그인 되어 있지 않으면 사용자에 게 로그인 하 라는 메시지가 표시 됩니다.

![](mvc-music-store-part-9/_static/image1.png)

로그인에 성공 하면 사용자에 게 주소 및 지불 보기가 표시 됩니다.

![](mvc-music-store-part-9/_static/image2.png)

양식을 채우고 주문을 제출 하면 주문 확인 화면이 표시 됩니다.

![](mvc-music-store-part-9/_static/image3.png)

존재 하지 않는 순서 또는 사용자에 게 속하지 않는 순서를 보려는 경우 오류 보기가 표시 됩니다.

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a>쇼핑 카트 마이그레이션

쇼핑 프로세스는 익명 이지만 사용자가 체크 아웃 단추를 클릭 하면 등록 하 고 로그인 해야 합니다. 사용자는 방문 간에 쇼핑 카트 정보를 유지 관리 하므로 등록 또는 로그인이 완료 되 면 장바구니 정보를 사용자와 연결 해야 합니다.

ShoppingCart 클래스에는 현재 카트에 있는 모든 항목을 사용자 이름과 연결 하는 메서드가 이미 있기 때문에 실제로는이 작업을 수행 하는 것이 매우 간단 합니다. 사용자가 등록 또는 로그인을 완료 하는 경우에만이 메서드를 호출 해야 합니다.

멤버 자격 및 권한 부여를 설정할 때 추가한 **Accountcontroller** 클래스를 엽니다. MvcMusicStore를 참조 하는 using 문을 추가 하 고 다음 MigrateShoppingCart 메서드를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

다음으로, 아래와 같이 사용자의 유효성을 검사 한 후 MigrateShoppingCart를 호출 하도록 LogOn post 작업을 수정 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

사용자 계정이 성공적으로 생성 된 후 즉시 등록 게시 작업을 동일 하 게 변경 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

이제 등록 또는 로그인에 성공 하면 익명 쇼핑 카트는 사용자 계정으로 자동으로 전송 됩니다.

## <a name="creating-the-checkoutcontroller"></a>CheckoutController 만들기

Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 빈 컨트롤러 템플릿을 사용 하 여 CheckoutController 라는 프로젝트에 새 컨트롤러를 추가 합니다.

![](mvc-music-store-part-9/_static/image5.png)

먼저, 사용자가를 체크 인하기 전에 등록 하도록 요구 하도록 컨트롤러 클래스 선언 위에 권한 부여 특성을 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

*참고:이는 이전에 StoreManagerController에 대 한 변경 내용과 유사 하지만,이 경우에는 사용자가 관리자 역할에 있어야 합니다. 체크 아웃 컨트롤러에서는 사용자에 게 로그인이 필요 하지만 관리자가 될 필요는 없습니다.*

간단히 하기 위해이 자습서에서는 지불 정보를 처리 하지 않습니다. 대신, 사용자가 판촉 코드를 사용 하 여 체크 아웃할 수 있습니다. PromoCode 라는 상수를 사용 하 여이 프로 모션 코드를 저장 합니다.

StoreController와 마찬가지로 storeDB 라는 MusicStoreEntities 클래스의 인스턴스를 포함 하는 필드를 선언 합니다. MusicStoreEntities 클래스를 사용 하기 위해 MvcMusicStore 네임 스페이스에 대 한 using 문을 추가 해야 합니다. 체크 아웃 컨트롤러의 위쪽이 아래에 나타납니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

CheckoutController에는 다음과 같은 컨트롤러 작업이 포함 됩니다.

**AddressAndPayment (GET 메서드)** 는 사용자가 정보를 입력할 수 있는 폼을 표시 합니다.

**AddressAndPayment (POST 메서드)** 는 입력의 유효성을 검사 하 고 주문을 처리 합니다.

사용자가 체크 아웃 프로세스를 성공적으로 완료 한 후 **완료** 가 표시 됩니다. 이 보기에는 확인으로 사용자의 주문 번호가 포함 됩니다.

먼저 AddressAndPayment에 대해 컨트롤러를 만들 때 생성 된 인덱스 컨트롤러 작업의 이름을 바꿉니다. 이 컨트롤러 작업은 단순히 체크 아웃 폼을 표시 하므로 모델 정보가 필요 하지 않습니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

AddressAndPayment POST 메서드는 StoreManagerController에서 사용한 것과 동일한 패턴을 따릅니다. 즉, 폼 제출을 수락 하 고 주문을 완료 하 고 실패 하면 양식을 다시 표시 합니다.

양식 입력이 주문에 대 한 유효성 검사 요구 사항을 충족 하는지 확인 한 후에는 PromoCode 양식 값을 직접 확인 합니다. 모든 것이 올바르면 주문에 업데이트 된 정보를 저장 하 고, 주문 프로세스를 완료 하도록 ShoppingCart 개체에 지시 하 고, 전체 작업으로 리디렉션합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

체크 아웃 프로세스가 성공적으로 완료 되 면 사용자가 전체 컨트롤러 작업으로 리디렉션됩니다. 이 작업은 주문 번호를 확인으로 표시 하기 전에 주문이 로그인 한 사용자에 게 실제로 속하는지 확인 하는 간단한 검사를 수행 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

*참고: 프로젝트를 시작 했을 때/Views/Shared 폴더에 오류 보기가 자동으로 생성 되었습니다.*

전체 CheckoutController 코드는 다음과 같습니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a>AddressAndPayment 뷰 추가

이제 AddressAndPayment view를 만들어 보겠습니다. AddressAndPayment controller 작업 중 하나를 마우스 오른쪽 단추로 클릭 하 고 아래와 같이 강력한 형식의 AddressAndPayment 라는 뷰를 추가 합니다.

![](mvc-music-store-part-9/_static/image6.png)

이 보기는 StoreManagerEdit 뷰를 작성 하는 동안 확인 된 기술 중 두 가지를 사용 합니다.

- Html. EditorForModel ()을 사용 하 여 주문 모델에 대 한 양식 필드를 표시 합니다.
- 유효성 검사 특성을 사용 하 여 Order 클래스를 사용 하는 유효성 검사 규칙을 활용 합니다.

먼저 Html. EditorForModel ()을 사용 하 고 프로 모션 코드에 대 한 추가 텍스트 상자를 사용 하도록 양식 코드를 업데이트 합니다. AddressAndPayment 뷰에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a>주문에 대 한 유효성 검사 규칙 정의

이제 뷰가 설정 되었으므로 이전에 앨범 모델에 대해 했던 것 처럼 주문 모델에 대 한 유효성 검사 규칙을 설정 합니다. 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 Order 라는 클래스를 추가 합니다. 이전에 앨범에 사용한 유효성 검사 특성 외에도 정규식을 사용 하 여 사용자 전자 메일 주소의 유효성을 검사 합니다.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

누락 되거나 잘못 된 정보를 사용 하 여 양식을 전송 하려고 하면 클라이언트 쪽 유효성 검사를 사용 하 여 오류 메시지가 표시 됩니다.

![](mvc-music-store-part-9/_static/image7.png)

확인 프로세스에 대 한 대부분의 하드 작업을 완료 했습니다. 몇 가지 경우에는 거의 필요 하지 않으며 종료 될 것입니다. 두 개의 간단한 뷰를 추가 해야 하며 로그인 프로세스 중에 카트 정보를 전달 해야 합니다.

## <a name="adding-the-checkout-complete-view"></a>체크 아웃 완료 보기 추가

주문 ID를 표시 하기만 하면 체크 아웃 완료 보기가 매우 간단 합니다. 전체 컨트롤러 작업을 마우스 오른쪽 단추로 클릭 하 고 int로 강력 하 게 형식화 된 Complete 라는 뷰를 추가 합니다.

![](mvc-music-store-part-9/_static/image8.png)

이제 아래와 같이 주문 ID를 표시 하도록 뷰 코드를 업데이트 합니다.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a>오류 보기 업데이트

기본 템플릿에는 사이트의 다른 곳에서 다시 사용할 수 있도록 공유 보기 폴더의 오류 보기가 포함 되어 있습니다. 이 오류 보기에는 매우 간단한 오류가 포함 되어 있으며 사이트 레이아웃을 사용 하지 않으므로 업데이트 합니다.

일반 오류 페이지 이므로 콘텐츠는 매우 간단 합니다. 사용자가 작업을 다시 시도 하려는 경우 기록에서 이전 페이지로 이동 하는 메시지와 링크를 포함 합니다.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-8.md)
> [다음](mvc-music-store-part-10.md)
