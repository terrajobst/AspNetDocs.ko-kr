---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 컨트롤러 및 뷰를 사용 하 여 목록/세부 정보 UI 구현 | Microsoft Docs
author: microsoft
description: 4 단계에서는 모델을 활용 하는 응용 프로그램에 컨트롤러를 추가 하 여 사용자에 게 데이터 목록/세부 정보 탐색 환경을 제공 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486221"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>컨트롤러 및 보기를 사용하여 목록/세부 정보 UI 구현

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 4 단계입니다.
> 
> 4 단계에서는 모델을 활용 하 여 응용 프로그램에 컨트롤러를 추가 하는 방법을 보여 줍니다 .이 모델을 사용 하 여 사용자에 게 dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공할 수 있습니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-4-controllers-and-views"></a>Nerddinner Step 4: 컨트롤러 및 뷰

기존 웹 프레임 워크 (기존 ASP, PHP, ASP.NET Web Forms 등)를 사용 하 여 들어오는 Url은 일반적으로 디스크의 파일에 매핑됩니다. 예: "/Products.aspx" 또는 "/Products.php"와 같은 URL에 대 한 요청은 "" 또는 "" 파일에 의해 처리 될 수 있습니다.

웹 기반 MVC 프레임 워크는 Url을 서버 코드에 약간 다른 방식으로 매핑합니다. 들어오는 Url을 파일에 매핑하는 대신, 해당 url을 클래스의 메서드에 매핑합니다. 이러한 클래스를 "컨트롤러" 라고 하며, 들어오는 HTTP 요청을 처리 하 고, 사용자 입력을 처리 하 고, 데이터를 검색 및 저장 하 고, 클라이언트로 다시 보낼 응답을 결정 합니다 (HTML 표시, 파일 다운로드, 다른 위치로 리디렉션). URL 등).

이제 동료 Ddinner 응용 프로그램에 대 한 기본 모델을 빌드 했으므로 다음 단계는 응용 프로그램에 컨트롤러를 추가 하 여 사용자에 게 사이트의 Dinners에 대 한 데이터 목록/세부 정보 탐색 환경을 제공 하는 것입니다.

### <a name="adding-a-dinnerscontroller-controller"></a>DinnersController 컨트롤러 추가

웹 프로젝트 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가&gt;컨트롤러** 메뉴 명령을 선택 하 여 시작 합니다 (Ctrl + M, Ctrl + C를 입력 하 여이 명령을 실행할 수도 있음).

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

그러면 "컨트롤러 추가" 대화 상자가 표시 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

새 컨트롤러의 이름을 "DinnersController"로 하 고 "추가" 단추를 클릭 합니다. 그러면 Visual Studio가 \Controllers 디렉터리 아래에 DinnersController.cs 파일을 추가 합니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

또한 코드 편집기 내에서 새로운 DinnersController 클래스를 엽니다.

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>Index () 및 Details () 동작 메서드를 DinnersController 클래스에 추가

응용 프로그램을 사용 하 여 방문자가 예정 된 dinners 목록을 검색 하 고 목록에서 저녁을 클릭 하 여이에 대 한 특정 세부 정보를 볼 수 있도록 합니다. 응용 프로그램에서 다음 Url을 게시 하 여이 작업을 수행 합니다.

| **URL** | **용도** |
| --- | --- |
| */Dinners/* | 예정 된 dinners의 HTML 목록 표시 |
| */Dinners/Details/[id]* | URL에 포함 된 "id" 매개 변수로 표시 되는 특정 dinner a에 대 한 세부 정보를 표시 합니다 .이 매개 변수는 데이터베이스에 있는 dinner of의 DinnerID와 일치 합니다. 예:/Dinners/Details/2는 해당 DinnerID 값이 2 인 Dinner a에 대 한 세부 정보가 포함 된 HTML 페이지를 표시 합니다. |

이러한 Url의 초기 구현은 아래와 같이 DinnersController 클래스에 두 개의 공용 "작업 메서드"를 추가 하 여 게시 합니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

그런 다음,이 응용 프로그램을 호출 하는 데 브라우저를 사용 합니다. *"/Dinners/"* URL에 입력 하면 *Index ()* 메서드가 실행 되 고 다음 응답이 다시 전송 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

*"/Dinners/Details/2"* URL에 입력 하면 *Details ()* 메서드가 실행 되 고 다음 응답이 다시 전송 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

ASP.NET MVC에서 사용자의 microsoft의 microsoft 차원 클래스를 만들고 해당 메서드를 호출 하는 방법을 궁금할 수 있습니다. 이를 이해 하기 위해 라우팅을 어떻게 작동 하는지 살펴보겠습니다.

### <a name="understanding-aspnet-mvc-routing"></a>ASP.NET MVC 라우팅 이해

ASP.NET MVC에는 Url이 컨트롤러 클래스에 매핑되는 방식을 유연 하 게 제어할 수 있는 강력한 URL 라우팅 엔진이 포함 되어 있습니다. ASP.NET MVC에서 만들 컨트롤러 클래스를 선택 하 고, 호출할 메서드를 선택 하 고, 변수를 URL/Querystring에서 자동으로 구문 분석 하 여 매개 변수 인수로 메서드에 전달할 수 있는 다양 한 방법을 구성 하는 방법을 완벽 하 게 사용자 지정할 수 있습니다. 응용 프로그램에서 원하는 URL 구조를 게시할 뿐만 아니라 SEO (검색 엔진 최적화)를 위해 사이트를 완전히 최적화할 수 있는 유연성을 제공 합니다.

기본적으로 새 ASP.NET MVC 프로젝트에는 미리 구성 된 URL 라우팅 규칙 집합이 이미 등록 되어 있습니다. 이렇게 하면 명시적으로 아무것도 구성 하지 않고도 응용 프로그램을 쉽게 시작할 수 있습니다. 기본 라우팅 규칙 등록은 프로젝트의 "응용 프로그램" 클래스 내에서 찾을 수 있습니다. 프로젝트의 루트에 있는 "global.asax" 파일을 두 번 클릭 하 여 열 수 있습니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

기본 ASP.NET MVC 라우팅 규칙은이 클래스의 "RegisterRoutes" 메서드 내에 등록 됩니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"경로입니다. MapRoute () "메서드 호출은 URL 형식을 사용 하 여 들어오는 Url을 컨트롤러 클래스에 매핑하는 기본 라우팅 규칙을 등록 합니다."/{controller}/{action}/{id} "-여기서" controller "는 인스턴스화할 컨트롤러 클래스의 이름이 고," action "은 해당 클래스에 대해 호출할 public 메서드의 이름이 고," id "는 메서드에 인수로 전달 될 수 있는 URL 내에 포함 된 선택적 매개 변수입니다. "MapRoute ()" 메서드 호출에 전달 되는 세 번째 매개 변수는 URL (Controller = "Home", Action = "Index", Id = "")에 없는 이벤트의 컨트롤러/작업/id 값에 사용할 기본값 집합입니다.

다음은 기본 "<em>/{controllers}/{action}/{id}"</em>경로 규칙을 사용 하 여 다양 한 url이 매핑되는 방법을 보여 주는 표입니다.

| **URL** | **Controller 클래스** | **Action 메서드** | **매개 변수가 전달 되었습니다.** |
| --- | --- | --- | --- |
| */Dinners/Details/2* | DinnersController | 세부 정보 (id) | id=2 |
| */Dinners/Edit/5* | DinnersController | Edit(id) | id=5 |
| */Dinners/Create* | DinnersController | Create() | 해당 없음 |
| */Dinners* | DinnersController | Index () | 해당 없음 |
| */Home* | HomeController | Index () | 해당 없음 |
| */* | HomeController | Index () | 해당 없음 |

마지막 세 행에는 사용 되는 기본값 (Controller = Home, Action = Index, Id = "")이 표시 됩니다. "Index" 메서드가 지정 되지 않은 경우 기본 작업 이름으로 등록 되기 때문에 "/Dinners" 및 "/Home" Url을 지정 하면 해당 컨트롤러 클래스에서 Index () 작업 메서드가 호출 됩니다. "홈" 컨트롤러가 지정 되지 않은 경우 기본 컨트롤러로 등록 되기 때문에 "/" URL을 통해 HomeController 생성 되 고 Index () 작업 메서드가 호출 됩니다.

이러한 기본 URL 라우팅 규칙을 원하지 않는 경우에는 위의 RegisterRoutes 메서드 내에서 간단히 변경 하는 것이 좋습니다. 그러나 이러한 공동으로 사용 하는 Ddinner 응용 프로그램의 경우 기본 URL 라우팅 규칙을 변경 하지 않습니다. 대신 그대로 사용 합니다.

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>Binnerscontroller의 DinnerRepository 사용

이제 microsoft의 DinnersController Index () 및 Details () 작업 메서드의 현재 구현을 모델을 사용 하는 구현으로 바꿉니다.

이전에 빌드한 DinnerRepository 클래스를 사용 하 여 동작을 구현 합니다. "NerdDinner. 모델" 네임 스페이스를 참조 하는 "using" 문을 추가한 다음 Dinnerrepository 클래스의 필드로 DinnerRepository의 인스턴스를 선언 하는 것으로 시작 합니다.

이 챕터의 뒷부분에서는 "종속성 주입"의 개념을 소개 하 고 컨트롤러에서 더 나은 단위 테스트를 가능 하 게 하는 다른 방법을 보여 줍니다. 그러나 이제는이에 대 한 올바른 단위 테스트를 제공 합니다. 아래와 같이 인라인 합니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

이제 검색 된 데이터 모델 개체를 사용 하 여 HTML 응답을 다시 생성할 준비가 되었습니다.

### <a name="using-views-with-our-controller"></a>컨트롤러에서 보기 사용

작업 메서드 내에 HTML을 조합 하는 코드를 작성 한 다음, *응답. write ()* 도우미 메서드를 사용 하 여 클라이언트에 다시 보낼 수 있지만, 이러한 접근 방식은 속도가 훨씬 어렵습니다. 훨씬 더 나은 방법은 microsoft의 경우에는 microsoft의 응용 프로그램 및 데이터 논리를 microsoft의 microsoft 응용 프로그램 및 데이터 논리를 수행 하 고 html 표현을 출력 하는 별도의 "뷰" 템플릿에 HTML 응답을 렌더링 하는 데 필요한 데이터를 전달 하는 것입니다. 합니다. 잠시 후에 표시 되는 것 처럼 "뷰" 템플릿은 일반적으로 HTML 태그와 포함 된 렌더링 코드의 조합을 포함 하는 텍스트 파일입니다.

컨트롤러 논리를 뷰 렌더링에서 분리 하면 몇 가지 큰 이점이 있습니다. 특히 응용 프로그램 코드와 UI 서식/렌더링 코드 간에 명확 하지 않은 "문제 분리"를 강제 적용 하는 데 도움이 됩니다. 이를 통해 UI 렌더링 논리와 격리 하는 단위 테스트 응용 프로그램 논리를 훨씬 쉽게 수행할 수 있습니다. 나중에 응용 프로그램 코드를 변경 하지 않고도 UI 렌더링 템플릿을 더 쉽게 수정할 수 있습니다. 개발자와 디자이너가 더 쉽게 프로젝트에서 공동 작업을 수행할 수 있습니다.

' Void ' 반환 형식이 "ActionResult" 인 반환 형식을 대신 사용 하 여 두 작업 메서드의 메서드 시그니처를 변경 하 여 HTML UI 응답을 다시 보내도록 하기 위해이 클래스를 업데이트할 수 있습니다. 그런 다음 컨트롤러 기본 클래스에서 *View ()* 도우미 메서드를 호출 하 여 아래와 같이 "viewresult" 개체를 다시 반환할 수 있습니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

위에서 사용 하는 *View ()* 도우미 메서드의 시그니처는 아래와 같습니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

*View ()* 도우미 메서드의 첫 번째 매개 변수는 HTML 응답을 렌더링 하는 데 사용 하려는 뷰 템플릿 파일의 이름입니다. 두 번째 매개 변수는 뷰 템플릿이 HTML 응답을 렌더링 하기 위해 필요로 하는 데이터를 포함 하는 모델 개체입니다.

Index () 작업 메서드 내에서 *view ()* 도우미 메서드를 호출 하 고 "인덱스" 뷰 템플릿을 사용 하 여 DINNERS의 HTML 목록을 렌더링 하려고 함을 나타냅니다. 다음에서 목록을 생성 하기 위해 뷰 템플릿이 Dinner objects의 시퀀스를 전달 합니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

Details () 작업 메서드 내에서 URL에 제공 된 id를 사용 하 여 Dinner object를 검색 하려고 합니다. 유효한 Dinner found가 발견 되 면 "Details" 뷰 템플릿을 사용 하 여 검색 된 Dinner object를 렌더링 함을 나타내는 *view ()* 도우미 메서드를 호출 합니다. 잘못 된 dinner를 요청 하는 경우 "NotFound" 뷰 템플릿 (그리고 템플릿 이름만 사용 하는 *뷰 ()* 도우미 메서드의 오버 로드 된 버전)을 사용 하 여 dinner is가 없다는 것을 나타내는 유용한 오류 메시지를 렌더링 합니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

이제 "NotFound", "Details" 및 "Index" 뷰 템플릿을 구현 해 보겠습니다.

### <a name="implementing-the-notfound-view-template"></a>"NotFound" 뷰 템플릿 구현

먼저 "NotFound" 보기 템플릿을 구현 하 여 요청 된 저녁을 찾을 수 없음을 나타내는 오류 메시지를 표시 합니다.

컨트롤러 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 "보기 추가" 메뉴 명령을 선택 하 여 새 보기 템플릿을 만든 다음 Ctrl + M, Ctrl + V를 입력 하 여이 명령을 실행할 수도 있습니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

그러면 아래와 같이 "뷰 추가" 대화 상자가 표시 됩니다. 기본적으로 대화 상자는 대화가 시작 될 때 커서가 있던 동작 메서드의 이름과 일치 하도록 만들 뷰의 이름을 미리 채웁니다 (이 경우 "Details"). "NotFound" 템플릿을 먼저 구현 하려고 하기 때문에이 뷰 이름을 재정의 하 고 대신 "NotFound"로 설정 합니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

"추가" 단추를 클릭 하면 Visual Studio는 "\Views\Dinners" 디렉터리 내에 새 "NotFound .aspx" 보기 템플릿을 만듭니다 (디렉터리가 아직 없는 경우에도 생성 됨).

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

또한 코드 편집기 내에서 새로운 "NotFound .aspx" 보기 템플릿을 엽니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

기본적으로 템플릿 보기에는 콘텐츠와 코드를 추가할 수 있는 두 개의 "콘텐츠 영역"이 있습니다. 첫 번째 방법에서는 다시 보낸 HTML 페이지의 "제목"을 사용자 지정할 수 있습니다. 두 번째 방법을 사용 하면 다시 보낸 HTML 페이지의 "주 콘텐츠"를 사용자 지정할 수 있습니다.

"NotFound" 뷰 템플릿을 구현 하려면 몇 가지 기본 콘텐츠를 추가 합니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

그런 다음 브라우저에서 사용해 볼 수 있습니다. 이렇게 하려면 *"/Dinners/Details/9999"* URL을 요청 하겠습니다. 이는 데이터베이스에 현재 존재 하지 않는 dinner to를 참조 하 고,이를 통해 "NotFound" 뷰 템플릿을 렌더링 하는 데에는 DinnersController. Details () 작업 메서드가 발생 합니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

위의 스크린샷에서 볼 수 있는 한 가지 사항은 기본 보기 템플릿이 화면에서 주 콘텐츠를 둘러싸는 많은 HTML을 상속한 것입니다. 이는 보기 템플릿이 사이트의 모든 보기에서 일관적인 레이아웃을 적용할 수 있는 "마스터 페이지" 템플릿을 사용 하기 때문입니다. 이 자습서의 뒷부분에서 마스터 페이지의 작동 방식에 대해 설명 합니다.

### <a name="implementing-the-details-view-template"></a>"Details" 뷰 템플릿 구현

이제 단일 Dinner model에 대 한 HTML을 생성 하는 "Details" 뷰 템플릿을 구현 하겠습니다.

이렇게 하려면 세부 정보 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 "보기 추가" 메뉴 명령을 선택 하거나 Ctrl + M, Ctrl + V를 누릅니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

그러면 "보기 추가" 대화 상자가 표시 됩니다. 기본 보기 이름 ("Details")을 유지 합니다. 또한 대화 상자에서 "강력한 형식의 뷰 만들기" 확인란을 선택 하 고 컨트롤러에서 뷰로 전달할 모델 유형의 이름을 선택 합니다 (combobox 드롭다운 사용). 이 뷰에서는 Dinner object를 전달 합니다 .이 형식의 정규화 된 이름은 "NerdDinner. 모델인"입니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

"빈 뷰"를 만들도록 선택한 이전 템플릿과 달리 이번에는 "Details" 템플릿을 사용 하 여 보기를 자동으로 "스 캐 폴드" 할 수 있습니다. 위의 대화 상자에서 "콘텐츠 보기" 드롭다운을 변경 하 여이를 나타낼 수 있습니다.

"스 캐 폴딩"은 전달 하는 Dinner object를 기반으로 세부 정보 보기 템플릿의 초기 구현을 생성 합니다. 이를 통해 보기 템플릿 구현을 신속 하 게 시작할 수 있습니다.

"추가" 단추를 클릭 하면 Visual Studio에서 "\Views\Dinners" 디렉터리 내에 새 "Details .aspx" 보기 템플릿 파일을 만듭니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

또한 코드 편집기 내에서 새로운 "Details .aspx" 보기 템플릿을 엽니다. Dinner model을 기반으로 하는 세부 정보 보기의 초기 스 캐 폴드 구현을 포함 합니다. 스 캐 폴딩 엔진은 .NET 리플렉션을 사용 하 여 전달 된 클래스에 노출 되는 공용 속성을 확인 하 고 찾은 각 형식에 따라 적절 한 콘텐츠를 추가 합니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

*"/Dinners/Details/1"* URL을 요청 하 여 브라우저에서 "세부 정보" 스 캐 폴드 구현이 어떻게 표시 되는지 확인할 수 있습니다. 이 URL을 사용 하면 처음 만들 때 데이터베이스에 수동으로 추가 된 dinners 중 하나가 표시 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

이를 통해 신속 하 게 실행 하 고 세부 정보 .aspx 보기의 초기 구현을 제공 합니다. 그런 다음이를 이동 하 고 조정 하 여 UI를 사용자의 만족도로 사용자 지정할 수 있습니다.

세부 정보 .aspx 템플릿을 자세히 살펴보면 포함 된 렌더링 코드 뿐만 아니라 정적 HTML도 포함 되어 있습니다. &lt;%%&gt; 코드 너 깃는 뷰 템플릿이 렌더링 될 때 코드를 실행 하 고, &lt;% =%&gt; 코드는 해당 코드 내에 포함 된 코드를 실행 한 다음 결과를 템플릿의 출력 스트림으로 렌더링 합니다.

강력한 형식의 "모델" 속성을 사용 하 여 컨트롤러에서 전달 된 "Dinner" 모델 개체에 액세스 하는 코드를 보기 내에 작성할 수 있습니다. Visual Studio는 편집기 내에서이 "모델" 속성에 액세스할 때 전체 코드 intellisense를 제공 합니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

최종 세부 정보 보기 템플릿의 소스가 아래와 같이 약간의 작업을 수행해 보겠습니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

*"/Dinners/Details/1"* URL에 다시 액세스 하면 이제 아래와 같이 렌더링 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>"인덱스" 뷰 템플릿 구현

이제 "인덱스" 뷰 템플릿을 구현 하 여 예정 된 Dinners 목록을 생성 하겠습니다. 이렇게 하려면 인덱스 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 "보기 추가" 메뉴 명령을 선택 하거나 Ctrl + M, Ctrl + V를 누릅니다.

"뷰 추가" 대화 상자 내에서 "Index" 라는 뷰 템플릿을 유지 하 고 "강력한 형식의 뷰 만들기" 확인란을 선택 합니다. 이번에는 "목록" 보기 템플릿을 자동으로 생성 하 고 뷰에 전달 되는 모델 형식으로 "스 캐 폴드"를 선택 합니다 .이 경우 "목록"을 만드는 것으로 표시 되었기 때문에 보기 추가 대화 상자에서 보기 추가 대화 상자를 표시 합니다. 컨트롤러에서 뷰로 Dinner objects 시퀀스 전달:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

"추가" 단추를 클릭 하면 Visual Studio에서 "\Views\Dinners" 디렉터리 내에 새 "" 템플릿 파일을 만듭니다. 뷰에 전달 된 Dinners의 HTML 테이블 목록을 제공 하는 초기 구현을 "스 캐 폴드" 합니다.

응용 프로그램을 실행 하 고 *"/Dinners/"* URL에 액세스 하면 Dinners 목록이 다음과 같이 렌더링 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

위의 테이블 솔루션은 Dinner data의 그리드와 유사한 레이아웃을 제공 합니다 .이는 고객의 저녁 식사 목록에 대해 원하는 내용이 아닙니다. 위의 코드를 사용 하 여 테이블 대신 열을 렌더링 하는 데&gt; &lt;사용할 수 있는 데이터 열을 나열 하 고이를 수정할 수 있습니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

위의 foreach 문 내에서 "var" 키워드를 사용 하 여 모델의 각 dinner 루프를 반복 합니다. 3\.0에 C# 익숙하지 않은 것은 "var"을 사용 하면 dinner object가 런타임에 바인딩되어 있음을 의미 합니다. 대신, 컴파일러에서 강력한 형식의 "모델" 속성 ("IEnumerable&lt;Dinner&gt;" 형식)에 대해 형식 유추를 사용 하 고 로컬 "dinner" 변수를 Dinner type으로 컴파일 했음을 의미 합니다. 즉, 코드 블록 내에서 전체 intellisense 및 컴파일 시간 검사를 가져옵니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

브라우저에서 */Dinners* URL에 대 한 새로 고침을 누르면 업데이트 된 보기가 다음과 같이 표시 됩니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

이는 더 나은 방법 이지만 완전히 아직 없습니다. 마지막 단계는 최종 사용자가 목록에서 개별 Dinners를 클릭 하 고 세부 정보를 볼 수 있도록 하는 것입니다. 이를 구현 하는 것은 microsoft의 자세한 작업 메서드에 연결 하는 HTML 하이퍼링크 요소를

인덱스 보기 내에서 다음 두 가지 방법 중 하나로 이러한 하이퍼링크를 생성할 수 있습니다. 첫 번째 방법은 &lt;HTML 요소&gt; 내에 &lt;%%&gt; 블록을 포함 하는 아래와 같은&gt; 요소에 HTML &lt;수동으로 만드는 것입니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

사용할 수 있는 다른 방법은 컨트롤러의 다른 작업 메서드에 연결 되는&gt; 요소를 프로그래밍 방식으로 &lt;HTML을 지 원하는 ASP.NET MVC 내에서 기본 제공 "Html.actionlink ()" 도우미 메서드를 활용 하는 것입니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

Html에 대 한 첫 번째 매개 변수입니다. Html.actionlink () 도우미 메서드는 표시할 링크 텍스트 (이 경우 dinner of의 제목)이 고, 두 번째 매개 변수는 링크를 생성할 컨트롤러 작업 이름 (이 경우 Details 메서드)이 고, 세 번째 매개 변수는 작업에 보낼 매개 변수 집합입니다 (속성 이름/값을 사용 하 여 무명 형식으로 구현 됨). 이 경우에는 연결 하려는 dinner a의 "id" 매개 변수를 지정 합니다. ASP.NET MVC의 기본 URL 라우팅 규칙은 "{Controller}/{Action}/{id}" 이므로 html.actionlink () 도우미 메서드는 다음과 같은 출력을 생성 합니다.

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

여기서는 Html.actionlink () 도우미 메서드를 사용 하 고 목록에 있는 각 dinner를 적절 한 세부 정보 URL에 연결 합니다.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

이제 */Dinners* URL에 도달 하면 dinner list는 다음과 같습니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

목록에서 Dinners를 클릭 하면이에 대 한 세부 정보를 볼 수 있습니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>규칙 기반 명명 및 \Views 디렉터리 구조

ASP.NET MVC 응용 프로그램은 기본적으로 보기 템플릿을 확인할 때 규칙 기반 디렉터리 명명 구조를 사용 합니다. 이를 통해 개발자는 컨트롤러 클래스 내에서 뷰를 참조할 때 위치 경로를 정규화 하지 않아도 됩니다. 기본적으로 ASP.NET MVC는 응용 프로그램 아래의 * \Views\[ControllerName]\* 디렉터리에서 뷰 템플릿 파일을 찾습니다.

예를 들어, "Index", "Details" 및 "NotFound"와 같은 세 가지 뷰 템플릿을 명시적으로 참조 하는 ASP.NET MVC는 응용 프로그램 루트 디렉터리 아래의 *\Views\Dinners* 디렉터리 내에서 이러한 뷰를 기본적으로 찾습니다.

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

이전에는 프로젝트에 현재 세 개의 컨트롤러 클래스 (HomeController 및 AccountController – 프로젝트를 만들 때 마지막 2 개가 기본적으로 추가 됨) 및 세 개의 하위 디렉터리 (각각 하나씩)가 있습니다. controller)를 클릭 합니다.

Home 및 Accounts 컨트롤러에서 참조 되는 뷰는 해당 *\Views\Home* 및 *\Views\Account* 디렉터리에서 해당 뷰 템플릿을 자동으로 확인 합니다. *\Views\Shared* 하위 디렉터리는 응용 프로그램 내의 여러 컨트롤러에서 다시 사용 되는 뷰 템플릿을 저장할 수 있는 방법을 제공 합니다. ASP.NET MVC는 뷰 템플릿을 확인 하려고 할 때 먼저 *\Views\[Controller]* 특정 디렉터리 내에서 확인 하 고, 해당 디렉터리에서 뷰 템플릿을 찾을 수 없는 경우 *\Views\Shared* 디렉터리 내에서 볼 수 있습니다.

개별 뷰 템플릿 이름을 지정 하는 것이 좋습니다. 뷰 템플릿이 렌더링을 유발한 동작 메서드와 동일한 이름을 공유 하도록 하는 것이 좋습니다. 예를 들어 "Index" 동작 메서드에서는 "Index" 뷰를 사용 하 여 뷰 결과를 렌더링 하 고 "Details" 작업 메서드는 "Details" 뷰를 사용 하 여 결과를 렌더링 합니다. 이렇게 하면 각 작업에 연결 된 템플릿을 빠르게 쉽게 확인할 수 있습니다.

개발자는 뷰 템플릿의 이름이 컨트롤러에서 호출 되는 작업 메서드와 같을 때 뷰 템플릿 이름을 명시적으로 지정할 필요가 없습니다. 대신, 뷰 이름을 지정 하지 않고 "View ()" 도우미 메서드에 모델 개체를 전달할 수 있으며, ASP.NET MVC는 *\Views\[ControllerName]\[ActionName]* 를 사용 하 여 디스크에서이 템플릿을 렌더링 하려고 함을 자동으로 유추 합니다.

이를 통해 컨트롤러 코드를 약간 정리 하 고 코드에서 이름을 두 번 중복 하지 않을 수 있습니다.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

위의 코드는 사이트에 대 한 훌륭한 저녁 목록/세부 경험을 구현 하는 데 필요 합니다.

#### <a name="next-step"></a>다음 단계

이제 훌륭한 Dinner 브라우징 환경을 구축 했습니다.

이제 CRUD (만들기, 읽기, 업데이트, 삭제) 데이터 폼 편집 지원을 사용 하도록 하겠습니다.

> [!div class="step-by-step"]
> [이전](build-a-model-with-business-rule-validations.md)
> [다음](provide-crud-create-read-update-delete-data-form-entry-support.md)
