---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: AJAX를 사용 하 여 동적 업데이트 제공 | Microsoft Docs
author: microsoft
description: 10 단계는 dinner detail 내에 통합 된 Ajax 기반 방법을 사용 하 여 저녁에 참석 하기 위해 로그인 한 사용자에 대 한 지원을 구현 합니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486311"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>AJAX를 사용하여 동적 업데이트 제공

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 10 단계입니다.
> 
> 10 단계는 dinner details 페이지 내에 통합 된 Ajax 기반 방법을 사용 하 여 저녁에 참석 하기 위해 로그인 한 사용자에 대 한 지원을 구현 합니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner 10 단계: RSVPs에서 허용 하는 AJAX 사용

이제 로그인 한 사용자에 대 한 지원을 구현 하 여 저녁에 참석 하는 데 관심을 가질 수 있습니다. Dinner details 페이지 내에 통합 된 AJAX 기반 방법을 사용 하 여이를 사용 하도록 설정 합니다.

### <a name="indicating-whether-the-user-is-rsvpd"></a>사용자에 게 RSVP가 있는지 여부를 나타내는

사용자는 */Dinners/Details/[id*] URL을 방문 하 여 특정 dinner a에 대 한 세부 정보를 볼 수 있습니다.

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

Details () 동작 메서드는 다음과 같이 구현 됩니다.

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

RSVP 지원을 구현 하기 위한 첫 번째 단계는 이전에 빌드한 Dinner.cs partial 클래스 내에서 "IsUserRegistered 된 (사용자 이름)" 도우미 메서드를 Dinner object에 추가 하는 것입니다. 이 도우미 메서드는 사용자가 현재 저녁 식사에 대해 RSVP를 수행 하 고 있는지 여부에 따라 true 또는 false를 반환 합니다.

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

그런 다음 세부 정보 .aspx 보기 템플릿에 다음 코드를 추가 하 여 사용자가 이벤트에 등록 되었는지 여부를 나타내는 적절 한 메시지를 표시할 수 있습니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

이제 사용자가 Dinner a를 방문 하면 다음과 같은 메시지가 표시 됩니다.

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

Dinner a를 방문 하면 등록 되지 않은 것입니다. 다음 메시지가 표시 됩니다.

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Register 동작 메서드 구현

이제 세부 정보 페이지에서 사용자에 게 저녁 식사에 대해 RSVP를 사용 하도록 설정 하는 데 필요한 기능을 추가 해 보겠습니다.

이를 구현 하기 위해 \Controllers 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 추가&gt;컨트롤러 메뉴 명령을 선택 하 여 새 "RSVPController" 클래스를 만듭니다.

새 RSVPController 클래스 내에서 Dinner a의 id를 인수로 사용 하 고, 적절 한 저녁 개체를 검색 하 고, 로그인 한 사용자가 현재 등록 된 사용자 목록에 있는지 확인 하 고, 다음을 수행 하는 "Register" 작업 메서드를 구현 합니다. 다음과 같이 RSVP 개체를 추가 하지 않습니다.

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

위에서 간단한 문자열을 작업 메서드의 출력으로 반환 하는 방법을 확인 합니다. 이 메시지는 보기 템플릿 내에 포함 될 수 있습니다. 하지만 매우 작으므로 컨트롤러 기본 클래스에서 Content () 도우미 메서드를 사용 하 고 위와 같은 문자열 메시지를 반환 합니다.

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>AJAX를 사용 하 여 RSVPForEvent Action 메서드 호출

AJAX를 사용 하 여 세부 정보 보기에서 등록 작업 메서드를 호출 합니다. 이를 구현 하는 것은 매우 쉽습니다. 먼저 두 개의 스크립트 라이브러리 참조를 추가 합니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

첫 번째 라이브러리는 core ASP.NET AJAX 클라이언트 쪽 스크립트 라이브러리를 참조 합니다. 이 파일의 크기는 약 24k (압축) 이며 핵심 클라이언트 쪽 AJAX 기능이 포함 되어 있습니다. 두 번째 라이브러리에는 ASP.NET MVC의 기본 제공 AJAX 도우미 메서드 (곧 사용 예정)와 통합 되는 유틸리티 함수가 포함 되어 있습니다.

그런 다음 앞에서 추가한 뷰 템플릿 코드를 업데이트할 수 있습니다. "이 이벤트에 등록 되지 않았습니다." 라는 메시지를 출력 하는 대신, 푸시 될 때 RSVP 컨트롤러에서 RSVPForEvent 작업 메서드를 호출 하는 AJAX 호출을 수행할 때 링크를 렌더링 합니다. 사용자 RSVPs:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

위에서 사용 된 ASP.NET () 도우미 메서드는 기본으로 제공 됩니다 .이 도우미 메서드는 표준 탐색을 수행 하는 대신 링크를 클릭할 때 작업 메서드에 대 한 AJAX 호출을 수행 한다는 점을 제외 하 고는 Html. a l l () 도우미 메서드와 비슷합니다. 위에서 "RSVP" 컨트롤러에 대 한 "Register" 작업 메서드를 호출 하 고이에 대 한 "id" 매개 변수로 DinnerID를 전달 합니다. 전달 되는 최종 AjaxOptions 매개 변수는 작업 메서드에서 반환 된 콘텐츠를 가져오고 id가 "rsvpmsg" 인 페이지에서 HTML &lt;div&gt; 요소를 업데이트 하려고 함을 나타냅니다.

이제 사용자가 dinner a를 탐색 하면 등록 되지 않은 경우에는 RSVP 링크를 볼 수 있습니다.

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

"이 이벤트에 대해 RSVP" 링크를 클릭 하면 RSVP 컨트롤러에서 등록 작업 메서드에 대 한 AJAX 호출이 수행 되 고, 완료 되 면 아래와 같은 업데이트 된 메시지가 표시 됩니다.

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

이 AJAX 호출을 수행할 때 수반 되는 네트워크 대역폭과 트래픽은 매우 간단 합니다. 사용자가 "이 이벤트에 대해 RSVP" 링크를 클릭 하면 아래와 같이 */Dinners/Register/1* URL에 작은 HTTP POST 네트워크 요청이 생성 됩니다.

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

그리고 등록 작업 메서드의 응답은 간단 합니다.

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

이 경량 호출은 속도가 빠르며 저속 네트워크 에서도 작동 합니다.

### <a name="adding-a-jquery-animation"></a>JQuery 애니메이션 추가

구현 된 AJAX 기능은 잘 작동 하 고 신속 하 게 작동 합니다. 경우에 따라 사용자에 게 RSVP 링크가 새 텍스트로 대체 된 것을 확인 하지 못할 수 있습니다. 결과를 좀 더 명확 하 게 만들기 위해 간단한 애니메이션을 추가 하 여 업데이트 메시지에 주목를 그릴 수 있습니다.

기본 ASP.NET MVC 프로젝트 템플릿에는 Microsoft 에서도 지 원하는 jQuery – 뛰어난 오픈 소스 JavaScript 라이브러리를 포함 합니다. jQuery는 멋진 HTML DOM 선택 및 효과 라이브러리를 비롯 한 다양 한 기능을 제공 합니다.

JQuery를 사용 하려면 먼저이에 대 한 스크립트 참조를 추가 합니다. 사이트 내의 다양 한 위치에서 jQuery를 사용 하기 때문에 모든 페이지에서 사용할 수 있도록 사이트 마스터 페이지 파일에 스크립트 참조를 추가 합니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*팁: JavaScript 파일 (jQuery 포함)에 대 한 보다 풍부한 intellisense 지원을 사용할 수 있는 VS 2008 s p 1 용 JavaScript intellisense 핫픽스를 설치 했는지 확인 합니다. http://tinyurl.com/vs2008javascripthotfix에서 다운로드할 수 있습니다.*

JQuery를 사용 하 여 작성 된 코드는 대개 CSS 선택기를 사용 하 여 하나 이상의 HTML 요소를 검색 하는 전역 "$ ()" JavaScript 메서드를 사용 합니다. 예를 들어 *$ ("#rsvpmsg")* 는 id가 RSVPMSG 인 HTML 요소를 선택 하 고, *$ ("...")* 는 "무언가" CSS 클래스 이름을 가진 모든 요소를 선택 합니다. 다음과 같은 선택기 쿼리를 사용 하 여 "선택한 라디오 단추 모두 반환"과 같은 고급 쿼리를 작성할 수도 있습니다. " *input [@type= radio] [@checked]")* .

요소를 선택한 후에는 해당 요소에서 메서드를 호출 하 여 (예: *$ ("#rsvpmsg"). hide ();)* 작업을 수행할 수 있습니다.

RSVP 시나리오의 경우 "rsvpmsg" &lt;div&gt;를 선택 하 고 텍스트 콘텐츠의 크기에 애니메이션을 적용 하는 "AnimateRSVPMessage" 라는 간단한 JavaScript 함수를 정의 합니다. 아래 코드는 작은 텍스트를 시작한 다음 400 밀리초를 초과 하 여 증가 시킵니다.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

그런 다음 ajax 호출이 성공적으로 완료 된 후이 JavaScript 함수를 호출할 수 있습니다 (AjaxOptions "OnSuccess" 이벤트 속성을 통해).

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

이제 "이 이벤트에 대해 RSVP" 링크를 클릭 하 여 AJAX 호출이 성공적으로 완료 되 면 다시 전송 된 콘텐츠 메시지는 애니메이션 효과를 주고 크게 증가 합니다.

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

AjaxOptions 개체는 "OnSuccess" 이벤트를 제공 하는 것 외에도, 다양 한 다른 속성 및 유용한 옵션과 함께 사용자가 처리할 수 있는 Onsuccess, Onsuccess 및 OnComplete 이벤트를 노출 합니다.

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>정리-RSVP 부분 보기를 리팩터링 합니다.

세부 정보 보기 템플릿은 약간의 시간을 얻기 위해 시작 하 고 있으며,이를 통해 더 많은 시간을 이해 하는 것이 더 어렵습니다. 코드 가독성을 향상 시키기 위해 세부 정보 페이지에 대 한 모든 RSVP 뷰 코드를 캡슐화 하는 부분 뷰 (RSVPStatus)를 만들어 보겠습니다.

\Views\Dinners 폴더를 마우스 오른쪽 단추로 클릭 한 다음 추가&gt;보기 메뉴 명령을 선택 하 여이 작업을 수행할 수 있습니다. 이제는 Dinner object를 강력한 형식의 ViewModel으로 사용 합니다. 그런 다음 세부 정보 .aspx 보기에서 RSVP 콘텐츠를 복사 하 여 붙여 넣을 수 있습니다.

이 작업을 완료 한 후에는 편집 및 삭제 링크 보기 코드를 캡슐화 하는 또 다른 부분 뷰 (EditAndDeleteLinks)를 만들어 보겠습니다. 또한 강력한 형식의 ViewModel으로 Dinner object를 사용 하 고 세부 정보 .aspx 보기의 편집 및 삭제 논리를 복사 하 여 붙여넣습니다.

세부 정보 보기 템플릿에는 아래쪽에 두 개의 Html RenderPartial () 메서드 호출을 포함할 수 있습니다.

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

이렇게 하면 코드를 더 깔끔하고 읽고 유지 관리할 수 있습니다.

### <a name="next-step"></a>다음 단계

이제 AJAX를 사용 하 여 응용 프로그램에 대화형 매핑 지원을 추가 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](secure-applications-using-authentication-and-authorization.md)
> [다음](use-ajax-to-implement-mapping-scenarios.md)
