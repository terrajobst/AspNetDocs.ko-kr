---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: 마스터 페이지 및 부분를 사용 하 여 UI 다시 사용 | Microsoft Docs
author: microsoft
description: 7 단계에서는 부분 보기 템플릿 및 마스터 페이지를 사용 하 여 코드 중복을 제거 하기 위해 보기 템플릿 내에서 ' 마른 원칙 '을 적용할 수 있는 방법을 살펴봅니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78468725"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>마스터 페이지 및 부분을 사용하여 UI 재사용

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 7 단계입니다.
> 
> 7 단계에서는 부분 보기 템플릿 및 마스터 페이지를 사용 하 여 코드 중복을 제거 하기 위해 보기 템플릿 내에서 "건조 원칙"을 적용할 수 있는 방법을 살펴봅니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner Step 7: 부분 및 마스터 페이지

ASP.NET MVC의 디자인 철학 중 하나는 "직접 반복 안 함" 원칙 (일반적으로 "원음" 이라고 함)입니다. 마른 디자인은 코드 및 논리의 중복을 제거 하 여 궁극적으로 응용 프로그램을 더 빠르게 빌드하고 유지 관리할 수 있도록 합니다.

몇 가지 부분으로 이루어진 Ddinner 시나리오에 적용 된 마른 원칙이 이미 살펴보았습니다. 몇 가지 예: 유효성 검사 논리는 모델 계층 내에서 구현 되므로 컨트롤러의 편집 및 만들기 시나리오 모두에서 적용 될 수 있습니다. 편집, 세부 정보 및 삭제 동작 메서드에서 "NotFound" 뷰 템플릿을 다시 사용 하 고 있습니다. 뷰 () 도우미 메서드를 호출할 때 이름을 명시적으로 지정할 필요가 없도록 하는 뷰 템플릿에서 규칙 명명 패턴을 사용 합니다. 그리고 편집 및 만들기 작업 시나리오 모두에 대해 d Innerformviewmodel 클래스를 다시 사용 합니다.

이제 보기 템플릿 내에서 "마른 원칙"을 적용 하 여 코드 중복을 제거할 수 있는 방법을 살펴보겠습니다.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>편집 및 만들기 보기 템플릿 다시 방문

현재는 두 가지 보기 템플릿 "Edit .aspx" 및 ".aspx 만들기"를 사용 하 여 Dinner form UI를 표시 합니다. 시각적 개체를 시각적으로 비교 하면 어떻게 유사한 지 강조 표시 됩니다. 생성 형태는 다음과 같습니다.

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

"편집" 형태는 다음과 같습니다.

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

차이가 많지 않습니다. 제목 및 머리글 텍스트 외에도 양식 레이아웃과 입력 컨트롤은 동일 합니다.

"Edit .aspx" 및 ".aspx 만들기" 보기 템플릿을 열면 동일한 양식 레이아웃 및 입력 제어 코드가 포함 된 것을 알 수 있습니다. 이 중복은 새 Dinner property를 도입 하거나 변경할 때 언제 든 지 변경 내용을 두 번 수행 하는 것을 의미 합니다.

### <a name="using-partial-view-templates"></a>부분 뷰 템플릿 사용

ASP.NET MVC는 페이지의 하위 부분에 대 한 뷰 렌더링 논리를 캡슐화 하는 데 사용할 수 있는 "부분 뷰" 템플릿을 정의 하는 기능을 지원 합니다. "부분"는 뷰 렌더링 논리를 한 번 정의한 다음 응용 프로그램의 여러 위치에서 다시 사용 하는 유용한 방법을 제공 합니다.

편집 .aspx의 "건조" 및 .aspx 보기 템플릿 복제를 지원 하기 위해 두 가지 모두에 공통 된 양식 레이아웃 및 입력 요소를 캡슐화 하는 "' d a t e. n a m e. n a m e" 이라는 부분 뷰 템플릿을 만들 수 있습니다. /Views/Dinners 디렉터리를 마우스 오른쪽 단추로 클릭 하 고 "추가&gt;뷰" 메뉴 명령을 선택 하 여이 작업을 수행 합니다.

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

그러면 "보기 추가" 대화 상자가 표시 됩니다. "' D i n 폼"을 만들 새 뷰의 이름을 지정 하 고, 대화 상자 내에서 "부분 보기 만들기" 확인란을 선택 하 고,이를 d Innerformviewmodel 클래스로 전달 한다는 것을

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

"추가" 단추를 클릭 하면 Visual Studio에서 "\Views\Dinners" 디렉터리 내에 새 "" 보기 템플릿을 만듭니다.

그런 다음, Edit .aspx/Create .aspx 보기 템플릿에서 중복 양식 레이아웃/입력 컨트롤 코드를 복사 하 여 새 "' i n a m e. n a m e.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

그런 다음, 편집 및 만들기 보기 템플릿을 업데이트 하 여이 템플릿 부분 템플릿을 호출 하 고, 형식 중복을 제거할 수 있습니다. 이 작업을 수행 하려면 보기 템플릿 내에서 Html RenderPartial ("DinnerForm")를 호출 하면 됩니다.

##### <a name="createaspx"></a>.Aspx 만들기

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Html RenderPartial을 호출할 때 원하는 부분 템플릿의 경로를 명시적으로 한정할 수 있습니다. 예를 들어 ~ Views/Dinners/DinnerForm. 위의 코드에서는 ASP.NET MVC 내에서 규칙 기반 명명 패턴을 활용 하 고, 렌더링할 부분 이름으로 ""을 지정 하기만 하면 됩니다. 이 작업을 수행 하면 ASP.NET MVC가 규칙 기반 뷰 디렉터리에서 먼저 표시 됩니다 (이는/Views/Dinners이 됨). 부분 템플릿이 없으면/Views/Shared 디렉터리에서 찾을 수 있습니다.

부분 뷰의 이름만 사용 하 여 Html RenderPartial ()를 호출 하면 ASP.NET MVC는 호출 하는 뷰 템플릿에서 사용 하는 동일한 모델 및 ViewData dictionary 개체를 부분 뷰로 전달 합니다. 또는 사용할 부분 뷰에 대해 대체 모델 개체 및/또는 ViewData 사전을 전달할 수 있도록 하는 Html RenderPartial ()의 오버 로드 된 버전이 있습니다. 이는 전체 모델/ViewModel의 하위 집합만 전달 하려는 경우에 유용 합니다.

| **사이드 토픽: &lt;% =%&gt;대신%%&gt;을 (를) &lt;하는 이유는 무엇입니까?** |
| --- |
| 위의 코드에서 발견할 수 있는 사소한 작업 중 하나는 Html을 호출할 때 &lt;% =%&gt; 블록 대신 &lt;%%&gt; 블록을 사용 하는 것입니다. ASP.NET 의% =%&gt; 블록 &lt;개발자가 지정 된 값 (예: &lt;% = "Hello"%&gt; "Hello"를 렌더링)을 렌더링 하려고 함을 표시 합니다. 대신 &lt;%%&gt; 블록은 개발자가 코드를 실행 하 고 있는 모든 렌더링 된 출력을 명시적으로 수행 해야 함을 표시 합니다 (예: &lt;% Response ("Hello")%&gt;). Html로 &lt;%%&gt; 블록을 사용 하는 이유는 Html. RenderPartial () 메서드가 문자열을 반환 하지 않고 대신 호출 하는 뷰 템플릿의 출력 스트림으로 콘텐츠를 직접 출력 하기 때문입니다. 성능 효율성을 위해이 작업을 수행 합니다. 이렇게 하면 (잠재적으로 매우 큰) 임시 문자열 개체를 만들 필요가 없습니다. 이렇게 하면 메모리 사용이 줄어들고 전반적인 응용 프로그램 처리량이 향상 됩니다. Html RenderPartial ()를 사용할 때 한 가지 일반적인 실수는 &lt;%%&gt; 블록 내에 있는 경우 호출 끝에 세미콜론을 추가 하는 것입니다. 예를 들어 다음 코드는 컴파일러 오류를 발생 시킵니다. &lt;% Html RenderPartial ("' DinnerForm")%&gt;. 대신 &lt;% Html. RenderPartial ("DinnerForm");을 (를) 작성 해야 합니다. %&gt; &lt;%%&gt; 블록이 자체 포함 된 코드 문 이므로 코드 문을 사용 하 C# 는 경우 세미콜론으로 종료 해야 합니다. |

### <a name="using-partial-view-templates-to-clarify-code"></a>코드를 명확 하 게 나타내기 위해 부분 뷰 템플릿 사용

여러 위치에서 뷰 렌더링 논리가 중복 되는 것을 방지 하기 위해 "' d Innerform" 부분 뷰 템플릿을 만들었습니다. 이는 부분 뷰 템플릿을 만드는 가장 일반적인 이유입니다.

경우에 따라 단일 위치로만 호출 되는 경우에도 부분 뷰를 만드는 것이 좋습니다. 뷰 렌더링 논리를 추출 하 고 하나 이상의 잘 명명 된 부분 템플릿으로 분할 하는 경우 매우 복잡 한 뷰 템플릿을 더 쉽게 읽을 수 있습니다.

예를 들어, 프로젝트의 site.master 파일 (곧 살펴볼 예정)에서 아래 코드 조각을 살펴보겠습니다. 화면 오른쪽 위에 로그인/로그 아웃 링크를 표시 하는 논리가 "LogOnUserControl" 부분 안에 캡슐화 되기 때문에 코드는 비교적 간단 하 게 읽을 수 있습니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

보기 템플릿 내에서 html/code 태그를 이해 하는 것을 혼동 하는 경우, 그 중 일부를 추출 하 여 잘 명명 된 부분 뷰로 리팩터링할 때 명확 하지 않을 지 여부를 고려해 야 합니다.

### <a name="master-pages"></a>마스터 페이지

ASP.NET MVC는 부분 뷰를 지 원하는 것 외에도 사이트의 공통 레이아웃 및 최상위 html을 정의 하는 데 사용할 수 있는 "마스터 페이지" 템플릿을 만드는 기능을 지원 합니다. 그런 다음 콘텐츠 자리 표시자 컨트롤을 마스터 페이지에 추가 하 여 재정의할 수 있는 대체 가능 영역을 확인할 수 있습니다. 이를 통해 응용 프로그램 전체에 공통적인 레이아웃을 적용할 수 있습니다.

기본적으로 new ASP.NET MVC 프로젝트에는 마스터 페이지 템플릿이 자동으로 추가 됩니다. 이 마스터 페이지의 이름은 "\Views\Shared\"이 고,이 폴더는 다음과 같습니다.

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

기본 site.master 파일은 아래와 같습니다. 위쪽의 탐색 메뉴와 함께 사이트의 외부 html을 정의 합니다. 여기에는 제목에 대 한 두 개의 대체 가능한 콘텐츠 자리 표시자 컨트롤과 페이지의 기본 콘텐츠가 교체 되어야 하는 위치에 대 한 다른 두 개의 콘텐츠 자리 표시자 컨트롤이 포함 됩니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

팀 간 Ddinner 응용 프로그램에 대해 만든 모든 보기 템플릿 ("목록", "세부 정보", "편집", "만들기", "NotFound" 등)은이 사이트를 기반으로 합니다. 마스터 템플릿. 이는 "뷰 추가" 대화 상자를 사용 하 여 뷰를 만들 때 기본적으로 위쪽 &lt;% @ Page%&gt; 지시문에 추가 된 "MasterPageFile" 특성을 통해 표시 됩니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

즉, 사이트의 마스터 콘텐츠를 변경 하 고, 보기 템플릿을 렌더링할 때 변경 내용을 자동으로 적용 하 고 사용할 수 있습니다.

응용 프로그램의 헤더가 "내 MVC 응용 프로그램"이 아닌 "NerdDinner"가 되도록 site.master의 헤더 섹션을 업데이트 해 보겠습니다. 또한 탐색 메뉴를 업데이트 하 여 첫 번째 탭이 "Dinner a Dinner" (HomeController의 Index () 작업 메서드로 처리 됨)이 고, "Host a Dinner" 라는 새 탭을 추가 해 보겠습니다.

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Site.master 파일을 저장 하 고 브라우저를 새로 고치면 응용 프로그램 내의 모든 보기에 머리글 변경이 표시 되는 것을 볼 수 있습니다. 다음은 그 예입니다.

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

*/Dinners/Edit/[id]* URL:

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>다음 단계

부분 및 마스터 페이지는 보기를 명확 하 게 구성할 수 있는 매우 유연한 옵션을 제공 합니다. 보기 내용/코드를 복제 하는 것을 방지 하 고 보기 템플릿을 쉽게 읽고 유지 관리 하는 것을 확인할 수 있습니다.

이제 앞에서 빌드한 나열 시나리오를 다시 방문 하 고 확장 가능한 페이징 지원을 사용 하도록 하겠습니다.

> [!div class="step-by-step"]
> [이전](use-viewdata-and-implement-viewmodel-classes.md)
> [다음](implement-efficient-data-paging.md)
