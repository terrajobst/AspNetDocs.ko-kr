---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
title: ASP.NET AJAX UpdatePanel 트리거 이해 | Microsoft Docs
author: scottcate
description: Visual Studio의 태그 편집기에서 작업 하는 경우 UpdatePanel 컨트롤의 자식 요소가 두 개 있음을 IntelliSense에서 볼 수 있습니다. 호환성이 중 하나입니다.
ms.author: riande
ms.date: 03/12/2008
ms.assetid: faab8503-2984-48a9-8a40-7728461abc50
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
msc.type: authoredcontent
ms.openlocfilehash: b1cc869f373d4f8283b4d92af74707c3f11fef61
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588780"
---
# <a name="understanding-aspnet-ajax-updatepanel-triggers"></a>ASP.NET AJAX UpdatePanel 트리거 이해

[Scott cate cda (](https://github.com/scottcate)

[PDF 다운로드](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial02_Triggers_cs.pdf)

> Visual Studio의 태그 편집기에서 작업 하는 경우 UpdatePanel 컨트롤의 자식 요소가 두 개 있음을 IntelliSense에서 볼 수 있습니다. 그 중 하나는 Triggers 요소입니다 .이 요소는 해당 요소가 있는 UpdatePanel 컨트롤의 부분 렌더링을 트리거하는 페이지의 컨트롤 (또는 사용자 정의 컨트롤을 사용 하는 경우)을 지정 합니다.

## <a name="introduction"></a>소개

Microsoft의 ASP.NET 기술은 개체 지향 및 이벤트 구동 프로그래밍 모델을 제공 하 고 컴파일된 코드의 장점을 결합 합니다. 그러나 서버 쪽 처리 모델에는 기술에서 내재 된 몇 가지 단점이 있습니다 .이 중 상당수는 Microsoft ASP.NET 3.5 AJAX 확장에 포함 된 새 기능으로 해결할 수 있습니다. 이러한 확장을 통해 전체 페이지를 새로 고치지 않고도 페이지의 부분 렌더링, 클라이언트 스크립트를 통해 웹 서비스에 액세스 하는 기능 (ASP.NET 프로 파일링 API 포함) 및 광범위 한 클라이언트 쪽 API를 비롯 한 다양 한 새 리치 클라이언트 기능을 사용할 수 있습니다. ASP.NET 서버 쪽 컨트롤 집합에 표시 되는 많은 컨트롤 스키마를 미러링 하도록 디자인 되었습니다.

이 백서에서는 ASP.NET AJAX `UpdatePanel` 구성 요소의 XML 트리거 기능을 검사 합니다. XML 트리거를 통해 특정 UpdatePanel 컨트롤에 대해 부분 렌더링을 발생 시킬 수 있는 구성 요소를 세부적으로 제어할 수 있습니다.

이 백서는 .NET Framework 3.5 및 Visual Studio 2008 베타 2 릴리스를 기반으로 합니다. 이전에는 ASP.NET 2.0를 대상으로 하는 추가 기능 어셈블리인 ASP.NET AJAX 확장이 .NET Framework 기본 클래스 라이브러리에 통합 되었습니다. 또한이 백서에서는 visual Web Developer Express가 아닌 Visual Studio 2008을 사용 하 고 visual Studio의 사용자 인터페이스에 따라 연습을 제공 한다고 가정 합니다 (코드 목록이 개발 환경).

## <a name="triggers"></a>*트리거*

기본적으로 지정 된 UpdatePanel에 대 한 트리거는 `AutoPostBack` 속성이 **true**로 설정 된 TextBox 컨트롤을 포함 하 여 다시 게시를 호출 하는 모든 자식 컨트롤을 자동으로 포함 합니다. 그러나 태그를 사용 하 여 트리거를 선언적으로 포함할 수도 있습니다. UpdatePanel 컨트롤 선언의 `<triggers>` 섹션 내에서이 작업을 수행 합니다. `Triggers` collection 속성을 통해 트리거를 액세스할 수 있지만, 런타임에 `Page_Load` 페이지에 대 한 ScriptManager 개체의 `RegisterAsyncPostBackControl(Control)` 메서드를 사용 하 여 디자인 타임에 컨트롤을 사용할 수 없는 경우와 같이 런타임에 부분 렌더링 트리거를 등록 하는 것이 좋습니다. 페이지는 상태 비저장 이므로 이러한 컨트롤을 만들 때마다 다시 등록 해야 합니다.

다시 게시를 만드는 자식 컨트롤이 `ChildrenAsTriggers` 속성을 **false**로 설정 하 여 자동으로 부분 렌더링을 트리거하지 않도록 자동 자식 트리거 포함을 사용 하지 않도록 설정할 수도 있습니다. 이를 통해 페이지 렌더링을 호출할 수 있는 특정 컨트롤을 매우 유연 하 게 할당할 수 있으므로, 개발자가 발생할 수 있는 이벤트를 처리 하는 대신 이벤트에 응답 하도록 옵트인 (opt in) 할 수 있습니다.

UpdatePanel 컨트롤이 중첩 된 경우 UpdateMode이 **조건부**로 설정 되어 있으면 자식 updatepanel이 트리거되고 부모는 그렇지 않으면 자식 updatepanel만 새로 고쳐집니다. 그러나 부모 UpdatePanel을 새로 고치면 자식 UpdatePanel도 새로 고쳐집니다.

## <a name="the-lttriggersgt-element"></a>*&lt;트리거&gt; 요소*

Visual Studio의 태그 편집기에서 작업 하는 경우 `UpdatePanel` 컨트롤의 자식 요소가 두 개 있음을 IntelliSense에서 볼 수 있습니다. 가장 자주 표시 되는 요소는 기본적으로 업데이트 패널 (부분 렌더링을 사용할 수 있는 콘텐츠)에서 보유 하는 콘텐츠를 캡슐화 하는 `<ContentTemplate>` 요소입니다. 다른 요소는 `<Triggers>` 요소입니다 .이 요소는 페이지의 컨트롤 (또는 사용자 정의 컨트롤을 사용 하는 경우)을 지정 합니다 .이 요소는 &lt;트리거&gt; 요소가 상주 하는 UpdatePanel 컨트롤의 부분 렌더링을 트리거합니다.

`<Triggers>` 요소에는 `<asp:AsyncPostBackTrigger>` 및 `<asp:PostBackTrigger>`라는 두 자식 노드의 숫자가 모두 포함 될 수 있습니다. 두 특성 모두 `ControlID` 및 `EventName`를 수락 하 고 현재 캡슐화 단위 내에서 컨트롤을 지정할 수 있습니다. 예를 들어, UpdatePanel 컨트롤이 웹 사용자 정의 컨트롤 내에 있는 경우 사용자 컨트롤이 상주할 페이지에서 컨트롤을 참조 하지 않아야 합니다.

`<asp:AsyncPostBackTrigger>` 요소는이 트리거가 자식인 UpdatePanel 뿐만 아니라 캡슐화 단위에서 updatepanel 컨트롤의 자식으로 존재 하는 *컨트롤의 모든* 이벤트를 대상으로 할 수 있는 경우에 특히 유용 합니다. 따라서 부분 페이지 업데이트를 트리거하기 위해 모든 컨트롤을 만들 수 있습니다.

마찬가지로 `<asp:PostBackTrigger>` 요소는 부분 페이지 렌더링을 트리거하는 데 사용 될 수 있지만 서버에 대 한 전체 왕복이 필요한 경우에도 마찬가지입니다. 컨트롤에서 일반적으로 부분 페이지 렌더링을 트리거하는 경우 (예를 들어, UpdatePanel 컨트롤의 `<ContentTemplate>` 요소에 `Button` 컨트롤이 있는 경우)이 트리거 요소를 사용 하 여 전체 페이지 렌더링을 강제로 수행할 수도 있습니다. 다시, PostBackTrigger 요소는 현재 캡슐화 단위에서 UpdatePanel 컨트롤의 자식인 모든 컨트롤을 지정할 수 있습니다.

## <a name="lttriggersgt-element-reference"></a>*&lt;트리거&gt; 요소 참조*

*태그 하위 항목:*

| **태그가** | **설명** |
| --- | --- |
| &lt;asp: AsyncPostBackTrigger&gt; | 이 트리거 참조를 포함 하는 UpdatePanel에 대 한 부분 페이지 업데이트를 발생 시킬 컨트롤 및 이벤트를 지정 합니다. |
| &lt;asp: PostBackTrigger&gt; | 전체 페이지를 업데이트 (전체 페이지 새로 고침) 할 컨트롤 및 이벤트를 지정 합니다. 이 태그는 컨트롤이 부분 렌더링을 트리거하는 경우 전체 새로 고침을 강제 적용 하는 데 사용할 수 있습니다. |

## <a name="walkthrough-cross-updatepanel-triggers"></a>*연습: UpdatePanel 간 트리거*

1. 부분 렌더링을 사용 하도록 설정 하려면 ScriptManager 개체가 설정 된 새 ASP.NET 페이지를 만듭니다. 이 페이지에 두 개의 UpdatePanels를 추가 합니다. 첫 번째에서는 레이블 컨트롤 (Label1)과 단추 컨트롤 2 개 (Button1 및 Button2)를 포함 합니다. Button1은 클릭 하 여 업데이트 하거나 해당 줄을 따라 클릭 하 여 업데이트 해야 합니다. 두 번째 UpdatePanel에는 레이블 컨트롤 (Label2)만 포함 되지만, 해당 ForeColor 속성을 기본값 이외의 다른 항목으로 설정 하 여 구별 합니다.
2. 두 UpdatePanel 태그의 UpdateMode 속성을 **조건부**로 설정 합니다.

**목록 1: default.aspx에 대 한 태그:** 

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample1.aspx)]

1. Button1에 대 한 Click 이벤트 처리기에서 Label2 및 ToLongTimeString를 시간에 따라 다르게 설정 합니다 (예: DateTime. ()). Button2에 대 한 Click 이벤트 처리기의 경우에는 Label1을 시간 종속 값으로 설정 합니다.

**목록 2: default.aspx.cs에서 코드 숨김 (잘림):** 

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample2.cs)]

1. F5 키를 눌러 프로젝트를 빌드하고 실행 합니다. 두 패널 모두 업데이트를 클릭 하면 두 레이블이 모두 텍스트를 변경 합니다. 그러나이 패널 업데이트를 클릭 하면 Label1 업데이트만 업데이트 됩니다.

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image2.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image1.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-updatepanel-triggers/_static/image3.png))

## <a name="under-the-hood"></a>*내부 살펴보기*

방금 만든 예제를 활용 하 여 AJAX가 수행 하는 작업 및 UpdatePanel 크로스 패널 트리거의 작동 방식을 ASP.NET 수 있습니다. 이렇게 하려면 생성 된 페이지 소스 HTML 뿐만 아니라 FireBug 이라는 Mozilla Firefox 확장을 사용 하 여 작업을 수행 합니다. 그러면 AJAX 포스트백을 쉽게 검토할 수 있습니다. 또한 Lutz Roeder를 사용 하 여 .NET 반영자 도구를 사용 합니다. 이러한 두 도구는 온라인에서 무료로 사용할 수 있으며 인터넷 검색을 통해 찾을 수 있습니다.

페이지 소스 코드를 검사 하면 거의 모든 것이 표시 되지 않습니다. UpdatePanel 컨트롤은 `<div>` 컨테이너로 렌더링 되며 `<asp:ScriptManager>`에서 제공 하는 스크립트 리소스를 볼 수 있습니다. AJAX 클라이언트 스크립트 라이브러리 내부에 있는 PageRequestManager에 대 한 몇 가지 새로운 AJAX 관련 호출도 있습니다. 마지막으로 두 개의 UpdatePanel 컨테이너를 표시 합니다. 하나는 렌더링 된 `<input>` 단추를 사용 하 고 두 개의 `<asp:Label>` 컨트롤은 `<span>` 컨테이너로 렌더링 됩니다. FireBug에서 DOM 트리를 검사 하면 레이블이 흐리게 표시 되어 표시 되는 콘텐츠를 생성 하지 않는다는 것을 알 수 있습니다.

이 패널 업데이트 단추를 클릭 하면 상위 UpdatePanel이 현재 서버 시간으로 업데이트 됩니다. FireBug에서 요청을 검사할 수 있도록 콘솔 탭을 선택 합니다. POST 요청 매개 변수를 먼저 검사 합니다.

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image5.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image4.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-updatepanel-triggers/_static/image6.png))

UpdatePanel은 `UpdatePanel1` 컨트롤의 `Button1` ScriptManager1 매개 변수를 통해 실행 된 컨트롤 트리를 정확 하 게 표시 합니다. 이제 두 패널 모두 업데이트 단추를 클릭 합니다. 그런 다음 응답을 검사 하 여 문자열에 설정 된 파이프로 구분 된 일련의 변수를 확인 합니다. 특히, `UpdatePanel1`맨 위에 있는 UpdatePanel이 브라우저에 전송 되는 전체 HTML을 표시 합니다. AJAX 클라이언트 스크립트 라이브러리는 `.innerHTML` 속성을 통해 UpdatePanel의 원래 HTML 콘텐츠를 새 콘텐츠로 대체 하므로 서버에서 변경 된 내용을 HTML로 서버에서 보냅니다.

이제 두 패널 모두 업데이트 단추를 클릭 하 고 서버에서 결과를 검사 합니다. 결과는 매우 유사 합니다. UpdatePanels는 서버에서 새 HTML을 받습니다. 이전 콜백과 마찬가지로 추가 페이지 상태가 전송 됩니다.

여기서 볼 수 있듯이 AJAX 다시 게시를 수행 하는 데 특별 한 코드가 사용 되지 않으므로 AJAX 클라이언트 스크립트 라이브러리는 추가 코드 없이 폼 포스트백을 가로챌 수 있습니다. 서버 컨트롤은 자동으로 JavaScript를 사용 하 여 자동으로 폼을 전송 하지 않습니다. ASP.NET는 자동으로 폼 유효성 검사 및 상태에 대 한 코드를 자동으로 삽입 합니다. 기본적으로 자동 스크립트 리소스 포함, PostBackOptions 클래스 및 ClientScriptManager 클래스

예를 들어 CheckBox 컨트롤을 생각해 보십시오. .NET 반영자의 클래스 디스어셈블리를 검사 합니다. 이렇게 하려면 System.web 어셈블리가 열려 있는지 확인 하 고 `System.Web.UI.WebControls.CheckBox` 클래스로 이동 하 여 `RenderInputTag` 메서드를 엽니다. `AutoPostBack` 속성을 확인 하는 조건부를 찾습니다.

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image8.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image7.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-updatepanel-triggers/_static/image9.png))

AutoPostBack 속성을 true로 설정 하 여 `CheckBox` 컨트롤에서 자동 포스트백을 사용 하는 경우 결과 `<input>` 태그가 `onclick` 특성의 ASP.NET 이벤트 처리 스크립트를 사용 하 여 렌더링 됩니다. 그런 다음 폼의 전송 가로채기를 통해 ASP.NET AJAX를 페이지 nonintrusively에 삽입할 수 있으므로 부정확 한 문자열 대체를 활용 하 여 발생할 수 있는 잠재적인 주요 변경 사항을 방지할 수 있습니다. 또한 *사용자 지정* ASP.NET 컨트롤은 UpdatePanel 컨테이너 내에서 사용을 지원 하기 위해 추가 코드 없이 ASP.NET AJAX의 기능을 활용할 수 있도록 합니다.

`<triggers>` 기능은 \_updateControls에 대 한 PageRequestManager 호출에서 초기화 된 값에 해당 합니다. ASP.NET AJAX 클라이언트 스크립트 라이브러리에서는 밑줄로 시작 하는 메서드, 이벤트 및 필드 이름이 internal로 표시 되 고 라이브러리 자체 외부에서 사용할 수 없는 규칙을 활용 합니다. 이를 통해 AJAX 포스트백을 발생 시킬 컨트롤을 확인할 수 있습니다.

예를 들어 페이지에 두 개의 컨트롤을 추가 하 여 UpdatePanels 외부에 있는 한 컨트롤을 완전히 남기고 UpdatePanel 내에 둘 수 있습니다. 위쪽 UpdatePanel 내에 CheckBox 컨트롤을 추가 하 고 목록 내에 정의 된 여러 색을 사용 하 여 DropDownList을 삭제 합니다. 새 태그는 다음과 같습니다.

**목록 3: 새 태그**

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample3.aspx)]

새 코드 숨김이 여기에 나와 있습니다.

**목록 4: 코드 숨김**

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample4.cs)]

이 페이지의 개념은 드롭다운 목록에서 세 가지 색 중 하나를 선택 하 여 두 번째 레이블을 표시 하 고, 확인란이 굵게 표시 되는지 여부와 날짜와 시간을 표시 하는지 여부를 결정 하는 것입니다. 확인란은 AJAX 업데이트를 발생 시 키 지 않아야 하지만, 드롭다운 목록에는 UpdatePanel이 포함 되어 있지 않은 경우에도 마찬가지입니다.

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image11.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image10.png)

([전체 크기 이미지를 보려면 클릭](understanding-asp-net-ajax-updatepanel-triggers/_static/image12.png))

위의 스크린샷에 나와 있는 것 처럼 가장 최근에 클릭 한 단추는 오른쪽 단추인이 패널을 업데이트 합니다 .이 패널은 최하위 시간에 독립적으로 업데이트 됩니다. 날짜가 아래쪽 레이블에 표시 되기 때문에 클릭 사이에 날짜가 전환 되었습니다. 가장 중요 한 점은 레이블 텍스트 보다 최근에 업데이트 된 것입니다 .이는 컨트롤 상태가 중요 하다는 것을 보여 주고 사용자가 AJAX 포스트백을 통해 유지 되는 것으로 간주 합니다. *그러나*시간이 업데이트 되지 않았습니다. 시간이 서버에서 컨트롤이 다시 렌더링 될 때 ASP.NET 런타임에 의해 해석 되는 페이지의 \_\_VIEWSTATE 필드를 지 속성을 통해 시간이 자동으로 다시 채워집니다. ASP.NET AJAX 서버 코드는 컨트롤이 변경 되 고 있는 메서드를 인식 하지 못합니다. 단지 뷰 상태에서 다시 채워지고 적절 한 이벤트를 실행 합니다.

그러나 페이지\_Load 이벤트에서 시간을 초기화 했지만 시간이 올바르게 증가 했을 수 있습니다. 따라서 개발자는 적절 한 이벤트 처리기에서 적절 한 코드를 실행 하 고 컨트롤 이벤트 처리기가 적절 한 경우 페이지\_로드를 사용 하지 않도록 주의 해야 합니다.

## <a name="summary"></a>요약

ASP.NET AJAX Extensions UpdatePanel 컨트롤은 다양 한 메서드를 사용 하 여 업데이트 되는 컨트롤 이벤트를 식별 하는 다양 한 메서드를 활용할 수 있습니다. 자식 컨트롤에 의해 자동으로 업데이트 되는 것을 지원 하지만 페이지의 다른 위치에서 컨트롤 이벤트에 응답할 수도 있습니다.

서버 처리 부하의 가능성을 줄이려면 UpdatePanel의 `ChildrenAsTriggers` 속성을 `false`로 설정 하 고 해당 이벤트를 기본적으로 포함 하지 않고 옵트인으로 설정 하는 것이 좋습니다. 이를 통해 불필요 한 이벤트에서 유효성 검사를 비롯 하 여 원치 않는 효과를 발생 시 키 지 않고 입력 필드의 변경 내용을 방지할 수도 있습니다. 이러한 유형의 버그는 사용자에 게 투명 하 게 업데이트 되기 때문에 격리 하기 어려울 수 있으며, 그 이유는 즉시 알 수 없습니다.

ASP.NET AJAX 폼 게시 가로채기 모델의 내부 작동을 검사 하 여 ASP.NET가 이미 제공 하는 프레임 워크를 활용 하는지 확인할 수 있었습니다. 이렇게 하면 동일한 프레임 워크를 사용 하 여 디자인 된 컨트롤과의 최대 호환성이 유지 되 고 해당 페이지에 대해 작성 된 추가 JavaScript의 개입 최소화 됩니다.

## <a name="bio"></a>약력

Rob Paveza는 Tempe, AZ의 첨단 대화형 마케팅 회사인 Terralever ([www.terralever.com](http://www.terralever.com))의 선임 .net 응용 프로그램 개발자입니다. [robpaveza@gmail.com](mailto:robpaveza@gmail.com)에 도달할 수 있으며 블로그는 [http://geekswithblogs.net/robp/](http://geekswithblogs.net/robp/)에 있습니다.

Scott Cate cda (는 1997부터 Microsoft 웹 기술을 사용 하 고 있으며 기술 자료 소프트웨어 솔루션에 초점을 맞춘 ASP.NET 기반 응용 프로그램을 전문적으로 작성 하는[www.myKB.com](http://www.myKB.com)(myKB.com)의 부사장입니다. Scott은 [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 또는 [ScottCate.com](http://ScottCate.com) 의 블로그의 전자 메일을 통해 연락할 수 있습니다.

> [!div class="step-by-step"]
> [이전](understanding-partial-page-updates-with-asp-net-ajax.md)
> [다음](understanding-asp-net-ajax-authentication-and-profile-application-services.md)
