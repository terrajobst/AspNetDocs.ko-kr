---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
title: 삭제할 때 클라이언트 쪽 확인 추가 (C#) | Microsoft Docs
author: rick-anderson
description: 지금까지 만든 인터페이스에서 사용자는 편집 단추를 클릭할 때 삭제 단추를 클릭 하 여 실수로 데이터를 삭제할 수 있습니다. 이 t ...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: f6e2a12a-2b5e-48fd-8db3-1e94a500c19a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: e7d53bc65fdbbfa9ce9bfa5fbdbfa0dea598eebe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78479819"
---
# <a name="adding-client-side-confirmation-when-deleting-c"></a>삭제할 때 클라이언트 쪽 확인 추가(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_22_CS.exe) 또는 [PDF 다운로드](adding-client-side-confirmation-when-deleting-cs/_static/datatutorial22cs1.pdf)

> 지금까지 만든 인터페이스에서 사용자는 편집 단추를 클릭할 때 삭제 단추를 클릭 하 여 실수로 데이터를 삭제할 수 있습니다. 이 자습서에서는 삭제 단추를 클릭할 때 표시 되는 클라이언트 쪽 확인 대화 상자를 추가 합니다.

## <a name="introduction"></a>소개

지난 몇 가지 자습서에서는 응용 프로그램 아키텍처, ObjectDataSource 및 데이터 웹 컨트롤을 사용 하 여 삽입, 편집 및 삭제 기능을 제공 하는 방법을 살펴보았습니다. 지금까지 검사 한 삭제 인터페이스는 클릭 하면 다시 게시를 발생 시키고 ObjectDataSource s `Delete()` 메서드를 호출 하는 삭제 단추로 구성 되었습니다. 그런 다음 `Delete()` 메서드는 데이터 액세스 계층에 대 한 호출을 전파 하 여 데이터베이스에 대 한 실제 `DELETE` 문을 실행 하는 비즈니스 논리 계층에서 구성 된 메서드를 호출 합니다.

이 사용자 인터페이스를 사용 하면 방문자가 GridView, DetailsView 또는 FormView 컨트롤을 통해 레코드를 삭제할 수 있지만, 사용자가 삭제 단추를 클릭 하면 어떠한 종류의 확인도 발생 하지 않습니다. 사용자가 편집을 클릭 하려는 경우 실수로 삭제 단추를 클릭 하면 업데이트 하려는 레코드가 대신 삭제 됩니다. 이를 방지 하기 위해이 자습서에서는 삭제 단추를 클릭할 때 표시 되는 클라이언트 쪽 확인 대화 상자를 추가 합니다.

JavaScript `confirm(string)` 함수는 문자열 입력 매개 변수를 모달 대화 상자에 표시 된 텍스트로 표시 합니다 .이 대화 상자에는 두 가지 단추 (확인 및 취소)가 제공 됩니다 (그림 1 참조). `confirm(string)` 함수는 클릭 한 단추에 따라 부울 값을 반환 합니다 (`true`, 사용자가 확인을 클릭 하면 `false` 하 고 취소를 클릭 하는 경우).

![JavaScript confirm (string) 메서드는 모달 클라이언트 쪽 Messagebox를 표시 합니다.](adding-client-side-confirmation-when-deleting-cs/_static/image1.png)

**그림 1**: JavaScript `confirm(string)` 메서드는 모달 클라이언트 쪽 Messagebox를 표시 합니다.

폼을 전송 하는 동안 클라이언트 쪽 이벤트 처리기에서 `false` 값이 반환 되 면 양식 전송이 취소 됩니다. 이 기능을 사용 하 여 삭제 단추를 사용 하 여 클라이언트 쪽 `onclick` 이벤트 처리기가 `confirm("Are you sure you want to delete this product?")`에 대 한 호출 값을 반환할 수 있습니다. 사용자가 취소를 클릭 하면 `confirm(string)` false를 반환 하 여 양식 제출을 취소 합니다. 다시 게시를 사용 하지 않으면 삭제 단추가 클릭 된 제품은 삭제 되지 않습니다. 그러나 사용자가 확인 대화 상자에서 확인을 클릭 하면 다시 게시가 계속 적용 되지 않으며 제품이 삭제 됩니다. 이 기술에 대 한 자세한 내용은 [JavaScript s `confirm()` 메서드를 사용 하 여 양식 전송 제어를](http://www.webreference.com/programming/javascript/confirm/) 참조 하세요.

CommandField를 사용할 때 보다 템플릿을 사용 하는 경우 필요한 클라이언트 쪽 스크립트를 추가 하는 것은 약간 다릅니다. 따라서이 자습서에서는 FormView 및 GridView 예제를 모두 살펴봅니다.

> [!NOTE]
> 이 자습서에 설명 된 것과 같은 클라이언트 쪽 확인 기법을 사용 하면 사용자가 JavaScript를 지 원하는 브라우저를 방문 하 고 JavaScript를 사용 하도록 설정한 것으로 가정 합니다. 이러한 가정 중 하나가 특정 사용자에 대해 true가 아니면 삭제 단추를 클릭 하면 즉시 다시 게시 (messagebox 확인 표시 안 함)가 발생 합니다.

## <a name="step-1-creating-a-formview-that-supports-deletion"></a>1 단계: 삭제를 지 원하는 FormView 만들기

먼저 `EditInsertDelete` 폴더의 `ConfirmationOnDelete.aspx` 페이지에 FormView를 추가 하 고 `ProductsBLL` 클래스 `GetProducts()` 메서드를 통해 제품 정보를 다시 가져오는 새 ObjectDataSource에 바인딩합니다. 또한 `ProductsBLL` 클래스 s `DeleteProduct(productID)` 메서드가 ObjectDataSource s `Delete()` 메서드에 매핑되도록 ObjectDataSource를 구성 합니다. 삽입 및 업데이트 탭 드롭다운 목록이 (없음)로 설정 되어 있는지 확인 합니다. 마지막으로 FormView의 스마트 태그에서 페이징 사용 확인란을 선택 합니다.

이러한 단계를 수행 하면 새 ObjectDataSource의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample1.aspx)]

낙관적 동시성을 사용 하지 않는 이전 예제와 마찬가지로 ObjectDataSource s `OldValuesParameterFormatString` 속성을 지우십시오.

삭제만 지 원하는 ObjectDataSource 컨트롤에 바인딩 되었으므로 FormView s `ItemTemplate`는 삭제 단추만 제공 하 고 새 및 업데이트 단추는 없습니다. 그러나 FormView의 선언적 태그는 제거 될 수 있는 불필요 한 `EditItemTemplate` 및 `InsertItemTemplate`를 포함 합니다. 를 사용 하 여 제품 데이터 필드의 하위 집합만 표시 되도록 `ItemTemplate`를 사용자 지정 합니다. 삭제 단추와 함께 공급자 및 범주 이름 위의 `<h3>` 제목에 제품 이름을 표시 하도록 광산을 구성 했습니다.

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample2.aspx)]

이러한 변경 내용으로, 사용자가 한 번에 하나씩 제품을 전환할 수 있는 완전 한 기능을 제공 하는 웹 페이지를 사용 하 여 삭제 단추를 클릭 하기만 하면 제품을 삭제할 수 있습니다. 그림 2에서는 브라우저를 통해 볼 때의 진행 상황을 보여 줍니다.

[FormView ![단일 제품에 대 한 정보를 표시 합니다.](adding-client-side-confirmation-when-deleting-cs/_static/image3.png)](adding-client-side-confirmation-when-deleting-cs/_static/image2.png)

**그림 2**: FormView는 단일 제품에 대 한 정보를 보여 줍니다 ([전체 크기 이미지를 보려면 클릭](adding-client-side-confirmation-when-deleting-cs/_static/image4.png)).

## <a name="step-2-calling-the-confirmstring-function-from-the-delete-buttons-client-side-onclick-event"></a>2 단계: 클라이언트 쪽 onclick 이벤트 삭제 단추에서 confirm (string) 함수 호출

FormView를 만든 후 마지막 단계는 방문자가 클릭할 때 JavaScript `confirm(string)` 함수가 호출 되도록 삭제 단추를 구성 하는 것입니다. ASP.NET 2.0에 새로 추가 된 `OnClientClick property`를 사용 하 여 클라이언트 쪽 `onclick` 이벤트에 대 한 클라이언트 쪽 스크립트를 추가할 수 있습니다. `confirm(string)` 함수의 값을 반환 하려고 하므로이 속성을로 설정 하면 됩니다. `return confirm('Are you certain that you want to delete this product?');`

이 변경 후 Delete LinkButton s 선언적 구문은 다음과 같습니다.

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample3.aspx)]

이것이 전부입니다! 그림 3에서는이 확인 작업의 스크린 샷을 보여 줍니다. 삭제 단추를 클릭 하면 확인 대화 상자가 나타납니다. 사용자가 취소를 클릭 하면 포스트백이 취소 되 고 제품이 삭제 되지 않습니다. 그러나 사용자가 확인을 클릭 하면 다시 게시가 계속 되 고 ObjectDataSource s `Delete()` 메서드가 호출 되 고 culminating 데이터베이스가 삭제 됩니다.

> [!NOTE]
> `confirm(string)` JavaScript 함수로 전달 되는 문자열은 따옴표 대신 아포스트로피를 사용 하 여 구분 됩니다. JavaScript에서는 두 문자를 사용 하 여 문자열을 구분할 수 있습니다. 여기에 아포스트로피를 사용 하 여 `confirm(string)`에 전달 된 문자열에 대 한 구분 기호가 `OnClientClick` 속성 값에 사용 된 구분 기호와 모호 하지 않도록 합니다.

[![삭제 단추를 클릭 하면 확인 메시지가 표시 됩니다.](adding-client-side-confirmation-when-deleting-cs/_static/image6.png)](adding-client-side-confirmation-when-deleting-cs/_static/image5.png)

**그림 3**: 삭제 단추를 클릭 하면 확인이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-client-side-confirmation-when-deleting-cs/_static/image7.png)).

## <a name="step-3-configuring-the-onclientclick-property-for-the-delete-button-in-a-commandfield"></a>3 단계: CommandField에서 삭제 단추에 대 한 OnClientClick 속성 구성

템플릿에서 직접 LinkButton 또는 ImageButton 단추를 사용할 때 JavaScript `confirm(string)` 함수의 결과를 반환 하도록 해당 `OnClientClick` 속성을 구성 하 여 확인 대화 상자를 연결할 수 있습니다. 그러나 GridView 또는 DetailsView에 삭제 단추 필드를 추가 하는 CommandField는 선언적으로 설정할 수 있는 `OnClientClick` 속성을 포함 하지 않습니다. 대신 GridView 또는 DetailsView의 적절 한 `DataBound` 이벤트 처리기에서 삭제 단추를 프로그래밍 방식으로 참조 한 다음 해당 `OnClientClick` 속성을 설정 해야 합니다.

> [!NOTE]
> 적절 한 `DataBound` 이벤트 처리기에서 삭제 단추 s `OnClientClick` 속성을 설정 하는 경우 데이터에 대 한 액세스 권한이 현재 레코드에 바인딩되어 있습니다. 즉, "Chai 제품을 삭제 하 시겠습니까?"와 같은 특정 레코드에 대 한 세부 정보를 포함 하도록 확인 메시지를 확장할 수 있습니다. 이러한 사용자 지정은 데이터 바인딩 구문을 사용 하는 템플릿에서도 가능 합니다.

CommandField에서 삭제 단추에 대 한 `OnClientClick` 속성을 설정 하는 연습을 위해 페이지에 GridView를 추가 해 보겠습니다. FormView에서 사용 하는 것과 동일한 ObjectDataSource 컨트롤을 사용 하도록 GridView를 구성 합니다. 또한 제품 이름, 범주 및 공급자를 포함 하도록 GridView s BoundFields 제한 합니다. 마지막으로 GridView의 스마트 태그에서 삭제 사용 확인란을 선택 합니다. 이렇게 하면 `ShowDeleteButton` 속성이 `true`로 설정 된 `Columns` 컬렉션에 CommandField가 추가 됩니다.

이러한 변경을 수행한 후 GridView의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample4.aspx)]

CommandField는 GridView s `RowDataBound` 이벤트 처리기에서 프로그래밍 방식으로 액세스할 수 있는 단일 Delete LinkButton 인스턴스를 포함 합니다. 참조 된 `OnClientClick` 속성을 적절 하 게 설정할 수 있습니다. 다음 코드를 사용 하 여 `RowDataBound` 이벤트에 대 한 이벤트 처리기를 만듭니다.

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample5.cs)]

이 이벤트 처리기는 삭제 단추를 포함 하는 데이터 행에서 작동 하 고 삭제 단추를 프로그래밍 방식으로 참조 하 여 시작 됩니다. 일반적으로 다음 패턴을 사용 합니다.

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample6.cs)]

*ButtonType* 는 commandfield-Button, LinkButton 또는 ImageButton에서 사용 되는 단추의 유형입니다. 기본적으로 CommandField는 Linkbutton을 사용 하지만 `ButtonType property`CommandField s를 통해 사용자 지정할 수 있습니다. *Commandfieldindex* 는 GridView `Columns` 컬렉션 내에서 commandfield의 서 수 인덱스이 고 *ControlIndex* 는 commandfield s `Controls` collection에 있는 삭제 단추의 인덱스입니다. *ControlIndex* 값은 commandfield의 다른 단추를 기준으로 하는 단추 위치에 따라 달라 집니다. 예를 들어 CommandField에 표시 되는 유일한 단추가 삭제 단추인 경우 0의 인덱스를 사용 합니다. 그러나 삭제 단추 앞에 편집 단추가 있는 경우 인덱스 2를 사용 합니다. 인덱스 2를 사용 하는 이유는 삭제 단추 앞에 두 개의 컨트롤이 추가 됩니다. 즉, 편집 단추와 편집 및 삭제 단추 사이에 공백을 추가 하는 데 사용 되는 LiteralControl 편집 단추입니다.

특정 예의 경우 CommandField는 Linkbutton을 사용 하 고, 맨 왼쪽 필드에는 *Commandfieldindex* 가 0입니다. CommandField에는 다른 단추가 없고 삭제 단추도 있으므로 *controlIndex* 0을 사용 합니다.

CommandField에서 삭제 단추를 참조 한 후에는 현재 GridView 행에 바인딩된 제품에 대 한 정보를 가져옵니다. 마지막으로 삭제 단추 s `OnClientClick` 속성을 제품 이름을 포함 하는 적절 한 JavaScript로 설정 합니다. `confirm(string)` 함수에 전달 된 JavaScript 문자열은 아포스트로피를 사용 하 여 구분 되므로 제품 이름 내에 표시 되는 모든 아포스트로피를 이스케이프 해야 합니다. 특히 제품 이름의 아포스트로피는 "`\'`"로 이스케이프 됩니다.

이러한 변경이 완료 되 면 GridView에서 삭제 단추를 클릭 하면 사용자 지정 된 확인 대화 상자가 표시 됩니다 (그림 4 참조). FormView의 확인 messagebox와 마찬가지로, 사용자가 취소를 클릭 하면 다시 게시가 취소 되어 삭제가 발생 하지 않도록 합니다.

> [!NOTE]
> 이 기술은 DetailsView의 CommandField에서 삭제 단추에 프로그래밍 방식으로 액세스 하는 데에도 사용할 수 있습니다. 그러나 DetailsView의 경우 DetailsView에 `RowDataBound` 이벤트가 없으므로 `DataBound` 이벤트에 대 한 이벤트 처리기를 만듭니다.

[GridView s 삭제 단추를 클릭 ![사용자 지정 된 확인 대화 상자가 표시 됩니다.](adding-client-side-confirmation-when-deleting-cs/_static/image9.png)](adding-client-side-confirmation-when-deleting-cs/_static/image8.png)

**그림 4**: GridView s 삭제 단추를 클릭 하면 사용자 지정 된 확인 대화 상자가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](adding-client-side-confirmation-when-deleting-cs/_static/image10.png)).

## <a name="using-templatefields"></a>서식 필드 사용

CommandField의 단점 중 하나는 인덱싱을 통해 해당 단추에 액세스 하 고 결과 개체를 적절 한 단추 유형 (Button, LinkButton 또는 ImageButton)으로 캐스팅 해야 한다는 것입니다. "매직 넘버" 및 하드 코드 된 형식을 사용 하면 런타임 시까지 검색할 수 없는 문제가 발생 합니다. 예를 들어, 또는 다른 개발자가 앞으로의 특정 시점 (예: 편집 단추)에서 CommandField에 새 단추를 추가 하거나 `ButtonType` 속성을 변경 하면 기존 코드는 오류 없이 컴파일되지만 코드 작성 방법 및 변경 된 내용에 따라 예외 또는 예기치 않은 동작이 발생할 수 있습니다.

다른 방법은 GridView 및 DetailsView s CommandFields를 템플릿 필드로 변환 하는 것입니다. 이렇게 하면 CommandField의 각 단추에 대해 LinkButton (또는 단추 또는 ImageButton)가 있는 `ItemTemplate`를 사용 하 여 Templatefield로 변환 생성 됩니다. 이러한 단추 `OnClientClick` 속성은 FormView에서 볼 때 선언적으로 할당 되거나 다음 패턴을 사용 하 여 적절 한 `DataBound` 이벤트 처리기에서 프로그래밍 방식으로 액세스할 수 있습니다.

[!code-csharp[Main](adding-client-side-confirmation-when-deleting-cs/samples/sample7.cs)]

여기서 *controlID* 는 단추 `ID` 속성의 값입니다. 이 패턴에는 캐스팅을 위해 하드 코드 된 형식이 필요 하지만 인덱싱의 필요성이 제거 되어 런타임 오류가 발생 하지 않고 레이아웃이 변경 될 수 있습니다.

## <a name="summary"></a>요약

JavaScript `confirm(string)` 함수는 양식 전송 워크플로를 제어 하는 데 일반적으로 사용 되는 기술입니다. 이 함수는 실행 될 때 두 개의 단추 (OK 및 Cancel)를 포함 하는 모달 클라이언트 쪽 대화 상자를 표시 합니다. 사용자가 확인을 클릭 하면 `confirm(string)` 함수는 `true`을 반환 합니다. 취소를 클릭 하면 `false`반환 됩니다. 전송 프로세스 중에 이벤트 처리기가 `false`반환 하는 경우이 기능을 사용 하 여 양식 전송을 취소할 수 있으며, 레코드를 삭제할 때 확인 messagebox를 표시 하는 데 사용할 수 있습니다.

`confirm(string)` 함수는 컨트롤의 `OnClientClick` 속성을 통해 단추 웹 컨트롤의 클라이언트 쪽 `onclick` 이벤트 처리기에 연결할 수 있습니다. FormView의 템플릿 또는 DetailsView 또는 GridView의 Templatefield로 변환에서 템플릿의 삭제 단추를 사용 하 여 작업 하는 경우이 자습서에서 살펴본 것 처럼이 속성을 선언적으로 설정 하거나 프로그래밍 방식으로 설정할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [이전](implementing-optimistic-concurrency-cs.md)
> [다음](limiting-data-modification-functionality-based-on-the-user-cs.md)
