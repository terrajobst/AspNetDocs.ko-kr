---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
title: '반복 #7 – Ajax 기능 추가 (VB) | Microsoft Docs'
author: microsoft
description: 일곱 번째 반복에서는 Ajax에 대 한 지원을 추가 하 여 응용 프로그램의 응답성과 성능을 향상 시킵니다.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f640e063-150e-453d-8cfc-7e54a6ce0f1e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-vb
msc.type: authoredcontent
ms.openlocfilehash: cee2b6e7c7517a1e03ae26d5233fc438857a030c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487001"
---
# <a name="iteration-7--add-ajax-functionality-vb"></a>반복 #7 – Ajax 기능 추가 (VB)

[Microsoft](https://github.com/microsoft) 에서

[코드 다운로드](iteration-7-add-ajax-functionality-vb/_static/contactmanager_7_vb1.zip)

> 일곱 번째 반복에서는 Ajax에 대 한 지원을 추가 하 여 응용 프로그램의 응답성과 성능을 향상 시킵니다.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Contact Management ASP.NET MVC 응용 프로그램 빌드 (VB)

이 자습서 시리즈에서는 전체 연락처 관리 응용 프로그램을 처음부터 끝까지 빌드 합니다. 연락처 관리자 응용 프로그램을 사용 하면 연락처 정보 (이름, 전화 번호 및 전자 메일 주소)를 사용자 목록으로 저장할 수 있습니다.

여러 반복을 통해 응용 프로그램을 빌드합니다. 각 반복을 통해 응용 프로그램을 점진적으로 개선 합니다. 이 여러 반복 방법의 목표는 각 변경의 이유를 이해할 수 있게 하는 것입니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서는 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업 (만들기, 읽기, 업데이트 및 삭제 (CRUD))에 대 한 지원을 추가 합니다.

- 반복 #2-응용 프로그램을 멋지게 만듭니다. 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 css 스타일 시트를 수정 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사를 추가 합니다. 세 번째 반복에서는 기본 폼 유효성 검사를 추가 합니다. 사용자가 필요한 양식 필드를 완료 하지 않고 양식을 전송 하지 못하도록 합니다. 또한 전자 메일 주소 및 전화 번호의 유효성을 검사 합니다.

- 반복 #4-응용 프로그램이 느슨하게 결합 되도록 합니다. 이 네 번째 반복에서는 몇 가지 소프트웨어 디자인 패턴을 활용 하 여 연락처 관리자 응용 프로그램을 보다 쉽게 유지 관리 하 고 수정할 수 있습니다. 예를 들어 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램을 리팩터링 합니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서는 단위 테스트를 추가 하 여 응용 프로그램을 더 쉽게 유지 관리 하 고 수정할 수 있도록 합니다. Microsoft는 데이터 모델 클래스를 모의 하 고 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 빌드 했습니다.

- 반복 #6-테스트 기반 개발을 사용 합니다. 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성 하 고 단위 테스트에 대 한 코드를 작성 하 여 응용 프로그램에 새 기능을 추가 합니다. 이 반복에서는 연락처 그룹을 추가 합니다.

- 반복 #7-Ajax 기능을 추가 합니다. 일곱 번째 반복에서는 Ajax에 대 한 지원을 추가 하 여 응용 프로그램의 응답성과 성능을 향상 시킵니다.

## <a name="this-iteration"></a>이 반복

이 연락처 관리자 응용 프로그램 반복에서는 Ajax를 사용 하도록 응용 프로그램을 리팩터링 합니다. Ajax를 활용 하면 응용 프로그램의 응답성이 향상 됩니다. 페이지의 특정 영역을 업데이트 해야 하는 경우 전체 페이지를 렌더링 하지 않을 수 있습니다.

사용자가 새 연락처 그룹을 선택할 때마다 전체 페이지를 다시 표시 하지 않아도 되도록 인덱스 보기를 리팩터링할 것입니다. 대신, 누군가가 연락처 그룹을 클릭 하면 연락처 목록만 업데이트 하 고 페이지의 나머지만 그대로 둡니다.

또한 삭제 링크의 작동 방식을 변경 합니다. 별도의 확인 페이지를 표시 하는 대신 JavaScript 확인 대화 상자를 표시 합니다. 연락처 삭제를 확인 하는 경우 서버에 대해 HTTP 삭제 작업을 수행 하 여 데이터베이스에서 연락처 레코드를 삭제 합니다.

또한 jQuery를 활용 하 여 인덱스 뷰에 애니메이션 효과를 추가할 예정입니다. 새 연락처 목록이 서버에서 인출 되는 경우 애니메이션을 표시 합니다.

마지막으로, 브라우저 기록을 관리 하는 ASP.NET AJAX 프레임 워크 지원을 활용 합니다. Ajax 호출을 수행 하 여 연락처 목록을 업데이트할 때마다 기록 점수를 만듭니다. 이렇게 하면 브라우저의 뒤로 및 앞으로 단추를 사용할 수 있습니다.

## <a name="why-use-ajax"></a>Ajax를 사용 하는 이유

Ajax를 사용 하면 많은 이점이 있습니다. 먼저 응용 프로그램에 Ajax 기능을 추가 하면 사용자 환경이 향상 됩니다. 일반 웹 응용 프로그램에서는 사용자가 작업을 수행할 때마다 전체 페이지를 서버에 다시 게시 해야 합니다. 작업을 수행할 때마다 브라우저가 잠기고 사용자는 전체 페이지를 페치 하 고 다시 표시할 때까지 기다려야 합니다.

데스크톱 응용 프로그램의 경우이는 허용 되지 않는 환경입니다. 그러나 일반적으로 웹 응용 프로그램의 경우에는 더 나은 작업을 수행할 수 있다는 것을 알 수 없기 때문에 이러한 잘못 된 사용자 환경을 사용 하 게 됩니다. 실제로는 imaginations의 제한 사항 이라고 생각 하는 경우 웹 응용 프로그램의 제한 사항 이라고 생각 합니다.

Ajax 응용 프로그램에서는 페이지를 업데이트 하기 위해 사용자 환경을 중단으로 전환할 필요가 없습니다. 대신 백그라운드에서 비동기 요청을 수행 하 여 페이지를 업데이트할 수 있습니다. 페이지의 일부가 업데이트 되는 동안 사용자가 대기 하도록 강제 하지 않습니다.

Ajax를 활용 하 여 응용 프로그램의 성능을 향상 시킬 수도 있습니다. 이제 Ajax 기능 없이 연락처 관리자 응용 프로그램이 작동 하는 방식을 살펴보겠습니다. 연락처 그룹을 클릭 하면 전체 인덱스 뷰가 다시 표시 되어야 합니다. 연락처 목록과 연락처 그룹 목록을 데이터베이스 서버에서 검색 해야 합니다. 이러한 모든 데이터는 웹 서버에서 웹 브라우저로 전달 되어야 합니다.

그러나 응용 프로그램에 Ajax 기능을 추가한 후에는 사용자가 연락처 그룹을 클릭할 때 전체 페이지를 다시 정의 하지 않을 수 있습니다. 더 이상 데이터베이스에서 연락처 그룹을 가져올 필요가 없습니다. 또한 네트워크를 통해 전체 인덱스 뷰를 푸시할 필요가 없습니다. Ajax를 활용 하면 데이터베이스 서버에서 수행 해야 하는 작업의 양이 줄어들고 응용 프로그램에 필요한 네트워크 트래픽 양이 줄어듭니다.

## <a name="don-t-be-afraid-of-ajax"></a>Ajax를 사용할 수 없음

일부 개발자는 하위 수준 브라우저에 대해 걱정 하므로 Ajax를 사용 하지 않습니다. JavaScript를 지원 하지 않는 브라우저에서 액세스할 때 해당 웹 응용 프로그램은 계속 작동 하는지 확인 하려고 합니다. Ajax는 JavaScript에 따라 달라 지므로 일부 개발자는 Ajax를 사용 하지 않습니다.

그러나 Ajax를 구현 하는 방법에 대해 잘 알고 있는 경우에는 상위 그룹과 하위 브라우저 모두에서 작동 하는 응용 프로그램을 빌드할 수 있습니다. Microsoft의 연락처 관리자 응용 프로그램은 JavaScript 및 브라우저를 지 원하는 브라우저에서 작동 합니다.

JavaScript를 지 원하는 브라우저에서 연락처 관리자 응용 프로그램을 사용 하는 경우 더 나은 사용자 환경을 제공 합니다. 예를 들어 연락처 그룹을 클릭 하면 연락처를 표시 하는 페이지의 지역만 업데이트 됩니다.

반면 JavaScript를 지원 하지 않는 브라우저에서 연락처 관리자 응용 프로그램을 사용 하는 경우 (또는 JavaScript를 사용 하지 않는 경우)에는 사용자 환경이 약간 더 필요 하지 않습니다. 예를 들어 연락처 그룹을 클릭 하면 일치 하는 연락처 목록을 표시 하기 위해 전체 인덱스 뷰가 브라우저에 다시 게시 되어야 합니다.

## <a name="adding-the-required-javascript-files"></a>필요한 JavaScript 파일 추가

응용 프로그램에 Ajax 기능을 추가 하려면 세 가지 JavaScript 파일을 사용 해야 합니다. 이러한 세 파일은 모두 새로운 ASP.NET MVC 응용 프로그램의 Scripts 폴더에 포함 되어 있습니다.

응용 프로그램의 여러 페이지에서 Ajax를 사용 하려는 경우 응용 프로그램의 보기 마스터 페이지에 필요한 JavaScript 파일을 포함 하는 것이 좋습니다. 이렇게 하면 JavaScript 파일이 응용 프로그램의 모든 페이지에 자동으로 포함 됩니다.

보기 마스터 페이지의 &lt;head&gt; 태그 안에 다음 JavaScript 포함을 추가 합니다.

[!code-html[Main](iteration-7-add-ajax-functionality-vb/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Ajax를 사용 하도록 인덱스 뷰 리팩터링

연락처 그룹을 클릭 하면 연락처를 표시 하는 보기만 업데이트 되도록 인덱스 보기를 수정 하 여를 시작 하겠습니다. 그림 1의 빨간색 상자에는 업데이트 하려는 지역이 포함 되어 있습니다.

[연락처만 ![업데이트](iteration-7-add-ajax-functionality-vb/_static/image1.jpg)](iteration-7-add-ajax-functionality-vb/_static/image1.png)

**그림 01**: 연락처만 업데이트 ([전체 크기 이미지를 보려면 클릭](iteration-7-add-ajax-functionality-vb/_static/image2.png))

첫 번째 단계는 비동기적으로 업데이트 하려는 뷰 부분을 개별 부분 (사용자 정의 컨트롤 보기)으로 분리 하는 것입니다. 연락처의 테이블을 표시 하는 인덱스 뷰의 섹션이 목록 1의 부분으로 이동 되었습니다.

**목록 1-Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample2.aspx)]

목록 1의 부분에는 인덱스 뷰와 다른 모델이 있습니다. &lt;% @ Page%&gt; 지시어의 *inherits* 특성은 viewusercontrol&lt;Group&gt; 클래스에서 부분을 상속 하도록 지정 합니다.

업데이트 된 인덱스 보기는 목록 2에 포함 되어 있습니다.

**목록 2-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample3.aspx)]

목록 2에서는 업데이트 된 보기에 대해 확인 해야 하는 두 가지 항목이 있습니다. 먼저 부분으로 이동한 모든 콘텐츠가 Html. RenderPartial ()에 대 한 호출로 대체 되는지 확인 합니다. Html RenderPartial () 메서드는 초기 연락처 집합을 표시 하기 위해 인덱스 뷰가 처음 요청 될 때 호출 됩니다.

둘째, 연락처 그룹을 표시 하는 데 사용 되는 html.actionlink ()가 Ajax. 1 ()로 대체 되었습니다. 다음 매개 변수를 사용 하 여 Ajax. Html.actionlink ()를 호출 합니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample4.aspx)]

첫 번째 매개 변수는 링크에 대해 표시할 텍스트를 나타내고, 두 번째 매개 변수는 경로 값을 나타내며, 세 번째 매개 변수는 Ajax 옵션을 나타냅니다. 이 경우 UpdateTargetId Ajax 옵션을 사용 하 여 Ajax 요청이 완료 된 후에 업데이트 하려는 HTML &lt;div&gt; 태그를 가리킵니다. &lt;div&gt; 태그를 새 연락처 목록으로 업데이트 하려고 합니다.

연락처 컨트롤러의 업데이트 된 Index () 메서드는 목록 3에 포함 되어 있습니다.

**목록 3-Controller\stststomomoms (인덱스 메서드)**

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample5.vb)]

업데이트 된 Index () 작업은 조건에 따라 두 항목 중 하나를 반환 합니다. Index () 작업이 Ajax 요청에 의해 호출 되 면 컨트롤러는 부분을 반환 합니다. 그렇지 않으면 Index () 동작에서 전체 뷰를 반환 합니다.

Index () 작업은 Ajax 요청에 의해 호출 될 때 많은 데이터를 반환할 필요가 없습니다. 일반 요청의 컨텍스트에서 인덱스 작업은 모든 연락처 그룹 및 선택한 연락처 그룹의 목록을 반환 합니다. Ajax 요청의 컨텍스트에서 Index () 작업은 선택 된 그룹만 반환 합니다. Ajax는 데이터베이스 서버에서 작업을 줄일 것을 의미 합니다.

수정 된 인덱스 보기는 상위 그룹과 하위 수준 브라우저 모두의 경우에 작동 합니다. 연락처 그룹을 클릭 하 고 브라우저에서 JavaScript를 지 원하는 경우 연락처 목록이 포함 된 보기의 지역만 업데이트 됩니다. 반면, 브라우저에서 JavaScript를 지원 하지 않는 경우 전체 뷰가 업데이트 됩니다.

업데이트 된 인덱스 보기에는 한 가지 문제가 있습니다. 연락처 그룹을 클릭 하면 선택한 그룹이 강조 표시 되지 않습니다. 그룹 목록이 Ajax 요청 중에 업데이트 되는 지역 외부에 표시 되기 때문에 오른쪽 그룹이 강조 표시 되지 않습니다. 다음 섹션에서이 문제를 해결할 예정입니다.

## <a name="adding-jquery-animation-effects"></a>JQuery 애니메이션 효과 추가

일반적으로 웹 페이지에서 링크를 클릭 하면 브라우저 진행률 표시줄을 사용 하 여 브라우저에서 업데이트 된 콘텐츠를 적극적으로 페치하는 지 여부를 검색할 수 있습니다. 반면 Ajax 요청을 수행할 때 브라우저 진행률 표시줄에 진행률이 표시 되지 않습니다. 이렇게 하면 사용자가 불안해 수 있습니다. 브라우저의 고정 여부는 어떻게 알 수 있나요?

Ajax 요청을 수행 하는 동안 작업을 수행 하는 사용자에 게 나타낼 수 있는 여러 가지 방법이 있습니다. 한 가지 방법은 간단한 애니메이션을 표시 하는 것입니다. 예를 들어 Ajax 요청이 시작 되 면 영역을 페이드 아웃 하 고 요청이 완료 되 면 지역에서 페이드 아웃할 수 있습니다.

Microsoft ASP.NET MVC 프레임 워크와 함께 제공 되는 jQuery 라이브러리를 사용 하 여 애니메이션 효과를 만듭니다. 업데이트 된 인덱스 보기는 목록 4에 포함 되어 있습니다.

**목록 4-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample6.aspx)]

업데이트 된 인덱스 뷰에는 세 개의 새로운 JavaScript 함수가 포함 되어 있습니다. 처음 두 함수는 jQuery를 사용 하 여 새 연락처 그룹을 클릭 하면 연락처 목록을 페이드 아웃 하 고 페이드 아웃 합니다. 세 번째 함수는 Ajax 요청으로 인해 오류가 발생 하는 경우 오류 메시지를 표시 합니다 (예: 네트워크 시간 제한).

또한 첫 번째 함수는 선택한 그룹의 강조 표시를 처리 합니다. 클래스 = 선택한 특성이 클릭 한 요소의 부모 요소 (LI 요소)에 추가 됩니다. 다시 jQuery를 사용 하면 올바른 요소를 쉽게 선택 하 고 CSS 클래스를 추가할 수 있습니다.

이러한 스크립트는 AjaxOptions () 매개 변수의 도움말과 함께 그룹 링크에 연결 됩니다. 업데이트 된 Ajax. Html.actionlink () 메서드 호출은 다음과 같습니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>브라우저 기록 지원 추가

일반적으로 링크를 클릭 하 여 페이지를 업데이트 하면 브라우저 기록이 업데이트 됩니다. 이렇게 하면 브라우저 뒤로 단추를 클릭 하 여 시간을 페이지의 이전 상태로 전환할 수 있습니다. 예를 들어 친구 연락처 그룹을 클릭 한 다음 회사 연락처 그룹을 클릭 하면 브라우저 뒤로 단추를 클릭 하 여 친구 연락처 그룹이 선택 된 경우 페이지의 상태로 다시 이동할 수 있습니다.

아쉽게도 Ajax 요청을 수행 하면 브라우저 기록이 자동으로 업데이트 되지 않습니다. 연락처 그룹을 클릭 하면 일치 하는 연락처 목록이 Ajax 요청과 함께 검색 되 면 브라우저 기록이 업데이트 되지 않습니다. 새 연락처 그룹을 선택한 후에는 브라우저 뒤로 단추를 사용 하 여 연락처 그룹으로 다시 이동할 수 없습니다.

사용자가 Ajax 요청을 수행한 후 브라우저 뒤로 단추를 사용할 수 있도록 하려면 약간 더 많은 작업을 수행 해야 합니다. ASP.NET AJAX 프레임 워크에서 빌드된 브라우저 기록 관리 기능을 활용 해야 합니다.

ASP.NET AJAX 브라우저 기록을 실행 하려면 다음 세 가지 작업을 수행 해야 합니다.

1. EnableBrowserHistory 속성을 true로 설정 하 여 브라우저 기록을 사용 하도록 설정 합니다.
2. AddHistoryPoint () 메서드를 호출 하 여 뷰의 상태가 변경 될 때 기록 위치를 저장 합니다.
3. 탐색 이벤트가 발생할 때 뷰의 상태를 다시 생성 합니다.

업데이트 된 인덱스 보기는 목록 5에 포함 되어 있습니다.

**목록 5-Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample8.aspx)]

목록 5에서 브라우저 기록은 pageInit () 함수에서 사용 하도록 설정 됩니다. PageInit () 함수는 navigate 이벤트에 대 한 이벤트 처리기를 설정 하는 데도 사용 됩니다. 브라우저 앞으로 또는 뒤로 단추를 클릭 하면 페이지 상태가 변경 될 때마다 탐색 이벤트가 발생 합니다.

Begin담당자 목록 () 메서드는 연락처 그룹을 클릭할 때 호출 됩니다. 이 메서드는 addHistoryPoint () 메서드를 호출 하 여 새 기록 지점을 만듭니다. 클릭 한 연락처 그룹의 id가 기록에 추가 됩니다.

그룹 id는 연락처 그룹 링크의 expando 특성에서 검색 됩니다. 이 링크는 다음과 같은 Ajax. () 호출을 사용 하 여 렌더링 됩니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample9.aspx)]

마지막 매개 변수는 이름이 groupid 인 이름이 groupid 인 속성을 링크에 추가 합니다 (XHTML 호환성의 경우 소문자).

사용자가 브라우저 뒤로 또는 앞으로 단추를 누르면 탐색 이벤트가 발생 하 고 navigate () 메서드가 호출 됩니다. 이 메서드는 navigate 메서드에 전달 된 브라우저 기록 지점에 해당 하는 페이지의 상태와 일치 하도록 페이지에 표시 되는 연락처를 업데이트 합니다.

## <a name="performing-ajax-deletes"></a>Ajax 삭제 수행

현재 연락처를 삭제 하려면 삭제 링크를 클릭 한 다음 삭제 확인 페이지에 표시 된 삭제 단추를 클릭 해야 합니다 (그림 2 참조). 이는 데이터베이스 레코드를 삭제 하는 것 처럼 간단한 작업을 수행 하기 위한 많은 페이지 요청 처럼 보입니다.

[삭제 확인 페이지 ![](iteration-7-add-ajax-functionality-vb/_static/image2.jpg)](iteration-7-add-ajax-functionality-vb/_static/image3.png)

**그림 02**: 삭제 확인 페이지 ([전체 크기 이미지를 보려면 클릭](iteration-7-add-ajax-functionality-vb/_static/image4.png))

삭제 확인 페이지를 건너뛰고 인덱스 보기에서 직접 연락처를 삭제 하는 것이 좋습니다. 이 접근 방식을 사용 하면 응용 프로그램이 보안 허점을 하려는 유혹이 방법을 사용 하지 않는 것이 좋습니다. 일반적으로 웹 응용 프로그램의 상태를 수정 하는 작업을 호출할 때 HTTP GET 작업을 수행 하지 않으려고 합니다. 삭제를 수행할 때 http POST를 수행 하거나 HTTP 삭제 작업을 더 잘 수행 하려고 합니다.

Delete 링크는 연락처 목록 부분에 포함 됩니다. 업데이트 된 버전의 연락처 목록 부분은 목록 6에 포함 되어 있습니다.

**목록 6-Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample10.aspx)]

Delete 링크는 다음 호출을 통해 Ajax. ImageActionLink) 메서드를 호출 하 여 렌더링 됩니다.

[!code-aspx[Main](iteration-7-add-ajax-functionality-vb/samples/sample11.aspx)]

> [!NOTE] 
> 
> ASP.NET MVC 프레임 워크의 표준 부분은 Ajax. ImageActionLink. imageactionlink)입니다. Ajax. ImageActionLink)는 Contact Manager 프로젝트에 포함 된 사용자 지정 도우미 메서드입니다.

AjaxOptions 매개 변수에는 두 개의 속성이 있습니다. 먼저 Confirm 속성은 popup JavaScript 확인 대화 상자를 표시 하는 데 사용 됩니다. 둘째, HttpMethod 속성은 HTTP DELETE 작업을 수행 하는 데 사용 됩니다.

목록 7에는 연락처 컨트롤러에 추가 된 새 AjaxDelete () 작업이 포함 되어 있습니다.

**7-Controllers\AjaxDelete (영문) 표시**   

[!code-vb[Main](iteration-7-add-ajax-functionality-vb/samples/sample12.vb)]

AjaxDelete () 동작은 AcceptVerbs 특성으로 데코 레이트 됩니다. 이 특성은 HTTP DELETE 작업 이외의 HTTP 작업을 제외 하 고 작업을 호출 하지 않도록 합니다. 특히 HTTP GET을 사용 하 여이 작업을 호출할 수 없습니다.

데이터베이스 레코드를 삭제 한 후 삭제 된 레코드를 포함 하지 않는 연락처의 업데이트 된 목록을 표시 해야 합니다. AjaxDelete () 메서드는 연락처 목록 부분 및 업데이트 된 연락처 목록을 반환 합니다.

## <a name="summary"></a>요약

이 반복에서는 연락처 관리자 응용 프로그램에 Ajax 기능을 추가 했습니다. Ajax를 사용 하 여 응용 프로그램의 응답성과 성능을 개선 했습니다.

첫째, 연락처 그룹을 클릭 해도 전체 보기가 업데이트 되지 않도록 인덱스 보기를 리팩터링 했습니다. 대신 연락처 그룹을 클릭 하면 연락처 목록만 업데이트 됩니다.

다음으로, jQuery 애니메이션 효과를 사용 하 여 연락처 목록을 페이드 아웃 하 고 페이드 아웃 했습니다. Ajax 응용 프로그램에 애니메이션을 추가 하는 것은 응용 프로그램 사용자에 게 브라우저 진행률 표시줄에 해당 하는 기능을 제공 하는 데 사용할 수 있습니다.

또한 Ajax 응용 프로그램에 브라우저 기록 지원을 추가 했습니다. 사용자가 브라우저 뒤로 및 앞으로 단추를 클릭 하 여 인덱스 뷰의 상태를 변경할 수 있습니다.

마지막으로, HTTP DELETE 작업을 지 원하는 삭제 링크를 만들었습니다. Ajax 삭제를 수행 하면 사용자가 추가 삭제 확인 페이지를 요청 하지 않고도 데이터베이스 레코드를 삭제할 수 있습니다.

> [!div class="step-by-step"]
> [이전](iteration-6-use-test-driven-development-vb.md)
