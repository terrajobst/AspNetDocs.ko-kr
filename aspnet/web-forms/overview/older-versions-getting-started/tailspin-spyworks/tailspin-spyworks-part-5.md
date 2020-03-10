---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: '5 부: 비즈니스 논리 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 5 부에서는 비즈니스 논리를 추가 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511547"
---
# <a name="part-5-business-logic"></a>5 부: 비즈니스 논리

만든 사람 [Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다. ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 5 부에서는 비즈니스 논리를 추가 합니다.

## <a id="_Toc260221671"></a>일부 비즈니스 논리 추가

누군가가 웹 사이트를 방문할 때마다 쇼핑 환경을 사용할 수 있도록 하려고 합니다. 방문자는 등록 되거나 로그인 되지 않은 경우에도 쇼핑 카트에 항목을 찾아보고 추가할 수 있습니다. 체크 아웃할 준비가 되 면 인증할 수 있는 옵션이 제공 되 고 아직 구성원이 아닌 경우에는 계정을 만들 수 있습니다.

즉, 쇼핑 카트를 익명 상태에서 "등록 된 사용자" 상태로 변환 하는 논리를 구현 해야 합니다.

"클래스" 라는 디렉터리를 만든 다음 폴더를 마우스 오른쪽 단추로 클릭 하 고 MyShoppingCart.cs 이라는 새 "클래스" 파일을 만듭니다.

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

앞에서 설명한 것 처럼 MyShoppingCart 페이지를 구현 하는 클래스를 확장 하 고를 사용 하 여이 작업을 수행 합니다. NET의 강력한 "Partial 클래스" 구문입니다.

MyShoppingCart.aspx.cf 파일에 대해 생성 된 호출은 다음과 같습니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

"Partial" 키워드를 사용 합니다.

방금 생성 한 클래스 파일은 다음과 같습니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

Partial 키워드를이 파일에 추가 하 여 구현을 병합 합니다.

이제 새 클래스 파일이 다음과 같이 표시 됩니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

클래스에 추가 하는 첫 번째 메서드는 "AddItem" 메서드입니다. 사용자가 제품 목록 및 제품 세부 정보 페이지에서 "아트에 추가" 링크를 클릭할 때 최종적으로 호출 되는 메서드입니다.

페이지 맨 위에 있는 using 문에 다음을 추가 합니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

그런 다음이 메서드를 MyShoppingCart 클래스에 추가 합니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

LINQ to Entities 사용 하 여 항목이 이미 카트에 있는지 확인 합니다. 이 경우 항목의 주문 수량을 업데이트 합니다. 그렇지 않으면 선택한 항목에 대 한 새 항목을 만듭니다.

이 메서드를 호출 하기 위해이 메서드를 클래스 뿐만 아니라 항목이 추가 된 후 현재 쇼핑 a = cart를 표시 하는 지 수 카트 .aspx 페이지를 구현 합니다.

솔루션 탐색기에서 솔루션 이름을 마우스 오른쪽 단추로 클릭 하 고 이전에 수행한 것 처럼 새 페이지와 새 페이지를 추가 합니다.

이 페이지를 사용 하 여 저렴 한 문제 등의 중간 결과를 표시할 수는 있지만 구현 시 페이지는 실제로 렌더링 되지 않고 "추가" 논리를 호출 하 고 리디렉션을 호출 합니다.

이를 위해 페이지\_Load 이벤트에 다음 코드를 추가 합니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

QueryString 매개 변수에서 쇼핑 카트에 추가 하 고 클래스의 AddItem 메서드를 호출 하 여 제품을 검색 합니다.

오류가 발생 하지 않는다고 가정할 경우 다음을 완벽 하 게 구현 하는 SHoppingCart 페이지로 제어가 전달 됩니다. 오류가 발생 해야 하는 경우 예외를 throw 합니다.

현재는 전역 오류 처리기를 아직 구현 하지 않았으므로이 예외는 응용 프로그램에서 처리 되지 않지만 곧 해결 될 예정입니다.

또한 Debug. Fail () 문을 사용 합니다 (`using System.Diagnostics;)`을 통해 사용 가능

응용 프로그램이 디버거 내에서 실행 되는 경우이 메서드는 지정 된 오류 메시지와 함께 응용 프로그램 상태에 대 한 정보가 포함 된 자세한 대화 상자를 표시 합니다.

프로덕션 환경에서 실행 하는 경우에는 Debug. Fail () 문이 무시 됩니다.

이 코드에서는 장바구니 클래스 이름 "GetShoppingCartId"의 메서드 호출을 확인 합니다.

다음과 같이 메서드를 구현 하는 코드를 추가 합니다.

또한 업데이트 및 체크 아웃 단추와 "total" 카트를 표시할 수 있는 레이블만 추가 했습니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

이제 쇼핑 카트에 항목을 추가할 수 있지만 제품을 추가한 후에 카트를 표시 하는 논리를 구현 하지 않았습니다.

따라서 MyShoppingCart 페이지에서 다음과 같이 EntityDataSource 컨트롤과 GridVire 컨트롤을 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

카트 업데이트 단추를 두 번 클릭 하 고 태그의 선언에 지정 된 click 이벤트 처리기를 생성할 수 있도록 디자이너에서 폼을 호출 합니다.

나중에 세부 정보를 구현 하지만,이 작업을 수행 하면 오류 없이 응용 프로그램을 빌드하고 실행할 수 있습니다.

응용 프로그램을 실행 하 고 장바구니에 항목을 추가 하면이 메시지가 표시 됩니다.

![](tailspin-spyworks-part-5/_static/image2.jpg)

3 개의 사용자 지정 열을 구현 하 여 "기본" 그리드 표시에서 벗어난 있습니다.

첫 번째는 수량에 대 한 편집 가능 "바인딩" 필드입니다.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

다음은 줄 항목 합계를 표시 하는 "계산 된" 열입니다. 항목의 순위는 주문 수량입니다.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

마지막으로 사용자가 쇼핑 차트에서 항목을 제거 해야 함을 나타내는 데 사용할 CheckBox 컨트롤이 포함 된 사용자 지정 열이 있습니다.

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

표시 된 것 처럼 주문 합계 행이 비어 있으므로 주문 합계를 계산 하는 논리를 추가할 수 있습니다.

먼저 MyShoppingCart 클래스에 대 한 "GetTotal" 메서드를 구현 합니다.

MyShoppingCart.cs 파일에서 다음 코드를 추가 합니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

그런 다음 페이지\_Load 이벤트 처리기에서 GetTotal 메서드를 호출할 수 있습니다. 동시에 테스트를 추가 하 여 쇼핑 카트가 비어 있는지 확인 하 고, 표시 되는 경우 적절 하 게 조정 합니다.

이제 장바구니를 비워 두면 다음을 얻을 수 있습니다.

![](tailspin-spyworks-part-5/_static/image4.jpg)

그렇지 않은 경우 합계가 표시 됩니다.

![](tailspin-spyworks-part-5/_static/image5.jpg)

그러나이 페이지는 아직 완료 되지 않았습니다.

제거 하도록 표시 된 항목을 제거 하 고 사용자가 표에서 일부를 변경 했을 때 새 수량 값을 확인 하 여 쇼핑 카트를 다시 계산 하는 추가 논리가 필요 합니다.

MyShoppingCart.cs의 쇼핑 카트 클래스에 "RemoveItem" 메서드를 추가 하 여 사용자가 제거를 위해 항목을 표시 하는 경우를 처리할 수 있습니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

이제 사용자가 GridView에서 주문할 품질을 변경 하는 경우를 처리 하는 방법을 알아보겠습니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

기본 제거 및 업데이트 기능을 사용 하면 데이터베이스에서 쇼핑 카트를 실제로 업데이트 하는 논리를 구현할 수 있습니다. (MyShoppingCart.cs)

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

이 메서드에는 두 개의 매개 변수가 필요 합니다. 하나는 쇼핑 카트 Id이 고 다른 하나는 사용자 정의 유형의 개체 배열입니다.

따라서 사용자 인터페이스 세부 사항에 대 한 논리 종속성을 최소화 하기 위해 GridView 컨트롤에 직접 액세스 해야 하는 메서드 없이 코드에 쇼핑 카트 항목을 전달 하는 데 사용할 수 있는 데이터 구조를 정의 했습니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

MyShoppingCart.aspx.cs 파일에서 다음과 같이 업데이트 단추 클릭 이벤트 처리기에서이 구조를 사용할 수 있습니다. 카트를 업데이트 하는 것 외에도 카트 합계도 업데이트 됩니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

특히 다음 코드 줄을 확인 합니다.

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

GetValues ()은 MyShoppingCart.aspx.cs에서 다음과 같이 구현할 특수 도우미 함수입니다.

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

이를 통해 GridView 컨트롤에서 바인딩된 요소의 값에 쉽게 액세스할 수 있습니다. "항목 제거" CheckBox 컨트롤이 바인딩되지 않았으므로 FindControl () 메서드를 통해 액세스 합니다.

프로젝트 개발의이 단계에서는 체크 아웃 프로세스를 구현할 준비를 합니다.

이렇게 하기 전에 Visual Studio를 사용 하 여 멤버 자격 데이터베이스를 생성 하 고 멤버 자격 리포지토리에 사용자를 추가 해 보겠습니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-4.md)
> [다음](tailspin-spyworks-part-6.md)
