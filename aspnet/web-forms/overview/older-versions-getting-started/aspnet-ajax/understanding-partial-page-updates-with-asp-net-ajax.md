---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
title: ASP.NET AJAX를 사용 하 여 부분 페이지 업데이트 이해 | Microsoft Docs
author: scottcate
description: ASP.NET AJAX 확장의 가장 눈에 띄는 기능은 t ...로 전체 포스트백을 수행 하지 않고 부분 또는 증분 페이지 업데이트를 수행 하는 기능입니다.
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 54d9df99-1161-4899-b4e8-2679c85915e7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
msc.type: authoredcontent
ms.openlocfilehash: 4b87cb8f58dbd7f27b16bcb0d488ff361770d4fe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439271"
---
# <a name="understanding-partial-page-updates-with-aspnet-ajax"></a>ASP.NET AJAX를 사용한 부분 페이지 업데이트 이해

[Scott cate cda (](https://github.com/scottcate)

[PDF 다운로드](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial01_Partial_Page_Updates_cs.pdf)

> ASP.NET AJAX 확장의 가장 눈에 띄는 기능은 코드를 변경 하거나 최소한의 태그를 변경 하지 않고 서버에 대 한 전체 포스트백을 수행 하지 않고 부분 또는 증분 페이지 업데이트를 수행 하는 기능입니다. 이러한 이점은 광범위 합니다. 즉, Adobe Flash 또는 Windows 미디어와 같은 멀티미디어의 상태는 변경 되지 않고 대역폭 비용이 감소 하며 클라이언트는 일반적으로 다시 게시와 관련 된 깜빡임을 발생 하지 않습니다.

## <a name="introduction"></a>소개

Microsoft의 ASP.NET 기술은 개체 지향 및 이벤트 구동 프로그래밍 모델을 제공 하 고 컴파일된 코드의 장점을 결합 합니다. 그러나 서버 쪽 처리 모델에는 기술에 내재 된 몇 가지 단점이 있습니다.

- 페이지를 업데이트 하려면 페이지를 새로 고쳐야 하는 서버로의 라운드트립이 필요 합니다.
- 라운드트립 시 Javascript 또는 다른 클라이언트 쪽 기술 (예: Adobe Flash)에서 생성 된 효과는 지속 되지 않습니다.
- 다시 게시 하는 동안 Microsoft Internet Explorer 이외의 브라우저는 스크롤 위치를 자동으로 복원 하는 기능을 지원 하지 않습니다. 뿐만 아니라 Internet Explorer 에서도 페이지가 새로 고쳐질 때 깜박임이 있습니다.
- \_\_VIEWSTATE 폼 필드가 커지면 특히 GridView 컨트롤 또는 반복기 같은 컨트롤을 처리할 때 포스트백에 많은 대역폭이 포함 될 수 있습니다.
- JavaScript 또는 다른 클라이언트 쪽 기술을 통해 웹 서비스에 액세스 하기 위한 통합 된 모델은 없습니다.

Microsoft의 ASP.NET AJAX 확장을 입력 합니다. 동기 **J** avaScript **a** nd **X** **ML을 의미** 하는 AJAX는 플랫폼 간 JavaScript를 통해 증분 페이지 업데이트를 제공 하는 통합 프레임 워크로, microsoft ajax 프레임 워크를 구성 하는 서버 쪽 코드로 구성 되며 microsoft ajax 스크립트 라이브러리 라는 스크립트 구성 요소로 구성 됩니다. ASP.NET AJAX 확장은 JavaScript를 통해 ASP.NET 웹 서비스에 액세스 하기 위한 플랫폼 간 지원도 제공 합니다.

이 백서에서는 ScriptManager 구성 요소, UpdatePanel 컨트롤 및 UpdateProgress 컨트롤을 포함 하는 ASP.NET AJAX 확장의 부분 페이지 업데이트 기능을 검사 하 고,이를 반드시 사용할 수 있어야 하는 시나리오를 고려 합니다. 사용한.

이 백서는 Visual Studio .NET Framework 2008의 Beta 2 릴리스와 ASP.NET AJAX 확장을 기본 클래스 라이브러리 (이전에는 ASP.NET 2.0에 사용할 수 있는 추가 기능 구성 요소 였던)에 통합 하는 3.5을 기반으로 합니다. 이 백서에서는 visual Web Developer Express Edition이 아닌 Visual Studio 2008을 사용 한다고 가정 합니다. 참조 되는 일부 프로젝트 템플릿은 Visual Web Developer Express 사용자에 게 제공 되지 않을 수 있습니다.

## <a name="partial-page-updates"></a>부분 페이지 업데이트

ASP.NET AJAX 확장의 가장 눈에 띄는 기능은 코드를 변경 하거나 최소한의 태그를 변경 하지 않고 서버에 대 한 전체 포스트백을 수행 하지 않고 부분 또는 증분 페이지 업데이트를 수행 하는 기능입니다. 장점은 광범위 합니다. 즉, Adobe Flash 또는 Windows 미디어와 같은 멀티미디어의 상태는 변경 되지 않고 대역폭 비용이 감소 하며 클라이언트는 일반적으로 다시 게시와 관련 된 깜빡임을 발생 하지 않습니다.

부분 페이지 렌더링을 통합 하는 기능은 프로젝트를 최소한으로 변경 하 여 ASP.NET에 통합 됩니다.

## <a name="walkthrough-integrating-partial-rendering-into-an-existing-project"></a>연습: 부분 렌더링을 기존 프로젝트에 통합

1. Microsoft Visual Studio 2008에서 <em>파일</em> <em>-&gt; 새</em> <em>-&gt; 웹 사이트로</em> 이동 하 고 대화 상자에서 ASP.NET 웹 사이트를 선택 하 여 새 ASP.NET 웹 사이트 프로젝트를 만듭니다. 원하는 대로 이름을 지정할 수 있으며, 파일 시스템 또는 인터넷 정보 서비스 (IIS)에 설치할 수 있습니다.
2. 기본 ASP.NET 마크업 (서버 쪽 폼 및 `@Page` 지시문)이 포함 된 빈 기본 페이지가 표시 됩니다. `Label1` 이라는 레이블과 폼 요소 내의 페이지에 `Button1` 이라는 단추를 놓습니다. 원하는 대로 텍스트 속성을 설정할 수 있습니다.
3. 디자인 뷰에서 `Button1`를 두 번 클릭 하 여 코드 숨김으로 이벤트 처리기를 생성 합니다. 이 이벤트 처리기에서 단추를 클릭 한 `Label1.Text` 설정 합니다. .

**목록 1: 부분 렌더링을 사용 하도록 설정 하기 전의 default.aspx 태그**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample1.aspx)]

**목록 2: default.aspx.cs에서 코드 숨김 (잘림)**

[!code-csharp[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample2.cs)]

1. F5 키를 눌러 웹 사이트를 시작 합니다. Visual Studio에서 디버깅을 사용 하도록 web.config 파일을 추가 하 라는 메시지를 표시 합니다. 이렇게 합니다. 단추를 클릭 하면 페이지를 새로 고쳐 레이블의 텍스트를 변경 하 고 페이지를 다시 그리면 잠시 깜박임이 있습니다.
2. 브라우저 창을 닫은 후 Visual Studio 및 태그 페이지로 돌아갑니다. Visual Studio 도구 상자에서 아래로 스크롤하고 AJAX 확장 탭을 찾습니다. (이 탭이 없는 경우 이전 버전의 AJAX 또는 Atlas 확장을 사용 하 고 있기 때문에이 백서에서 나중에 AJAX 확장 도구 상자 항목을 등록 하는 방법에 대 한 연습을 참조 하거나 다운로드 가능한 Windows Installer 최신 버전을 설치 합니다. 웹 사이트에서).

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image2.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image1.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image3.png))

1. <em>알려진 문제:</em> ASP.NET 2.0 AJAX 확장을 사용 하 여 visual Studio 2005이 이미 설치 된 컴퓨터에 Visual Studio 2008을 설치 하는 경우 Visual Studio 2008에서 AJAX 확장 도구 상자 항목을 가져옵니다. 구성 요소의 도구 설명을 검사 하 여이에 대 한 것인지 여부를 확인할 수 있습니다. 3.5.0.0 버전을 표시 해야 합니다. 버전 2.0.0.0이 있으면 이전 도구 상자 항목을 가져온 후 Visual Studio의 도구 상자 항목 선택 대화 상자를 사용 하 여 수동으로 가져와야 합니다. 디자이너를 통해 버전 2 컨트롤을 추가할 수 없습니다.

2. `<asp:Label>` 태그를 시작 하기 전에 공백 줄을 만들고 도구 상자에서 UpdatePanel 컨트롤을 두 번 클릭 합니다. 페이지 맨 위에 새 `@Register` 지시문이 포함 되어 있습니다. 즉, `asp:` 접두사를 사용 하 여 system.xml 네임 스페이스 내의 컨트롤을 가져와야 함을 나타냅니다.
3. 레이블 및 단추 컨트롤을 래핑된 상태로 요소를 올바르게 구성 하려면 closing `</asp:UpdatePanel>` 태그를 Button 요소의 끝을 지나서 끌어 옵니다.
4. `<asp:UpdatePanel>` 태그를 연 후 새 태그 열기를 시작 합니다. IntelliSense는 두 가지 옵션을 묻는 메시지를 표시 합니다. 이 경우 `<ContentTemplate>` 태그를 만듭니다. 태그가 올바른 형식이 되도록 레이블 및 단추 주위에이 태그를 래핑해야 합니다.

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image5.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image4.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image6.png))

1. `<form>` 요소 내의 아무 곳에 나 도구 상자에서 `ScriptManager` 항목을 두 번 클릭 하 여 ScriptManager 컨트롤을 포함 합니다.
2. 특성 `EnablePartialRendering= true`를 포함 하도록 `<asp:ScriptManager>` 태그를 편집 합니다.

**목록 3: 부분 렌더링이 설정 된 default.aspx의 태그**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample3.aspx)]

1. Web.config 파일을 엽니다. Visual Studio가 자동으로 System.web에 대 한 컴파일 참조를 추가 했습니다.

1. Visual Studio 2008의 새로운 기능: ASP.NET 웹 사이트 프로젝트 템플릿과 함께 제공 되는 web.config에는 ASP.NET AJAX 확장에 대 한 모든 참조가 자동으로 포함 되어 있으며, 추가 기능을 사용할 수 있도록 주석 처리를 해제 합니다. ASP.NET 2.0 AJAX 확장이 설치 된 경우 Visual Studio 2005에 비슷한 템플릿이 있습니다. 그러나 Visual Studio 2008에서는 AJAX 확장이 기본적으로 옵트아웃 됩니다. 즉, 기본적으로 참조 되지만 참조로 제거할 수 있습니다.

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image8.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image7.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image9.png))

1. F5 키를 눌러 웹 사이트를 시작 합니다. 부분 렌더링을 지원 하기 위해 소스 코드를 변경 해야 하는 것은 아닙니다. 태그만 변경 되었습니다.

웹 사이트를 시작할 때 이제는 단추를 클릭할 때 깜박임이 없고 페이지 스크롤 위치에 변경 내용이 표시 되지 않으므로 부분 렌더링이 이제 사용 하도록 설정 된 것을 볼 수 있습니다 (이 예제에서는 설명 하지 않음). 단추를 클릭 한 후 페이지의 렌더링 된 소스를 확인 하는 경우 다시 게시가 발생 하지 않은 것을 확인 합니다. 원래 레이블 텍스트가 여전히 소스 태그의 일부이 고 레이블이 JavaScript를 통해 변경 된 것을 확인 합니다.

Visual Studio 2008은 ASP.NET AJAX 사용 웹 사이트에 대해 미리 정의 된 템플릿과 함께 제공 되지 않습니다. 그러나 Visual Studio 2005 및 ASP.NET 2.0 AJAX 확장이 설치 된 경우 Visual Studio 2005 내에서 이러한 템플릿을 사용할 수 있습니다. 따라서 웹 사이트를 구성 하 고 AJAX 사용 웹 사이트 템플릿을 사용 하 여 시작 하는 것은 템플릿이 완전히 구성 된 web.config 파일을 포함 해야 하기 때문에 훨씬 더 쉬울 수 있습니다. 웹 서비스 액세스를 비롯 한 모든 ASP.NET AJAX 확장을 지원 합니다. 및 JSON serialization-JavaScript Object Notation) 및는 기본적으로 주 Web Forms 페이지 내의 UpdatePanel 및 System.windows.controls.contentcontrol.contenttemplate를 포함 합니다. 이 기본 페이지를 사용 하 여 부분 렌더링을 사용 하도록 설정 하는 것은이 연습의 10 단계를 방문 하 고 컨트롤을 페이지로 끌어 놓는 것 만큼 간단 합니다.

## <a name="the-scriptmanager-control"></a>ScriptManager 컨트롤

## <a name="scriptmanager-control-reference"></a>ScriptManager 컨트롤 참조

태그 사용 속성:

| **속성 이름** | **형식** | **설명** |
| --- | --- | --- |
| AllowCustomErrors-Redirect | Bool | Web.config 파일의 사용자 지정 오류 섹션을 사용 하 여 오류를 처리할지 여부를 지정 합니다. |
| AsyncPostBackError-Message | String | 오류가 발생 하는 경우 클라이언트에 전송 되는 오류 메시지를 가져오거나 설정 합니다. |
| AsyncPostBack-Timeout | Int32 | 비동기 요청이 완료 될 때까지 클라이언트가 대기 해야 하는 기본 시간을 가져오거나 설정 합니다. |
| EnableScript-Globalization | Bool | 스크립트 세계화를 사용 하는지 여부를 가져오거나 설정 합니다. |
| EnableScript-Localization | Bool | 스크립트 지역화를 사용 하는지 여부를 가져오거나 설정 합니다. |
| ScriptLoadTimeout | Int32 | 클라이언트에 스크립트를 로드 하는 데 허용 되는 시간 (초)을 결정 합니다. |
| ScriptMode | Enum (자동, 디버그, 릴리스, 상속) | 스크립트의 릴리스 버전을 렌더링할지 여부를 가져오거나 설정 합니다. |
| ScriptPath | String | 클라이언트에 보낼 스크립트 파일의 위치에 대 한 루트 경로를 가져오거나 설정 합니다. |

코드 전용 속성:

| **속성 이름** | **형식** | **설명** |
| --- | --- | --- |
| AuthenticationService | AuthenticationService-Manager | 클라이언트에 게 전송 될 ASP.NET 인증 서비스 프록시에 대 한 세부 정보를 가져옵니다. |
| IsDebuggingEnabled | Bool | 스크립트 및 코드 디버깅이 사용 되는지 여부를 가져옵니다. |
| IsInAsyncPostback | Bool | 페이지가 현재 비동기 포스트백 요청 인지 여부를 가져옵니다. |
| ProfileService | ProfileService-Manager | 클라이언트에 게 전송 될 ASP.NET 프로 파일링 서비스 프록시에 대 한 세부 정보를 가져옵니다. |
| 스크립트 | 수집&lt;스크립트-참조&gt; | 클라이언트에 전송 되는 스크립트 참조의 컬렉션을 가져옵니다. |
| Services | 컬렉션&lt;서비스 참조&gt; | 클라이언트에 전송 되는 웹 서비스 프록시 참조의 컬렉션을 가져옵니다. |
| SupportsPartialRendering | Bool | 현재 클라이언트가 부분 렌더링을 지원 하는지 여부를 가져옵니다. 이 속성이 **false**를 반환 하는 경우 모든 페이지 요청은 표준 포스트백이 됩니다. |

공용 코드 메서드:

| **메서드 이름** | **형식** | **설명** |
| --- | --- | --- |
| SetFocus(string) | Void | 요청이 완료 되 면 클라이언트의 포커스를 특정 컨트롤로 설정 합니다. |

태그 하위 항목:

| **Tag** | **설명** |
| --- | --- |
| &lt;AuthenticationService&gt; | ASP.NET 인증 서비스에 대 한 프록시에 대 한 세부 정보를 제공 합니다. |
| &lt;ProfileService&gt; | ASP.NET 프로 파일링 서비스에 프록시에 대 한 세부 정보를 제공 합니다. |
| &lt;스크립트&gt; | 추가 스크립트 참조를 제공 합니다. |
| &lt;asp: System.web.ui.scriptreference&gt; | 특정 스크립트 참조를 나타냅니다. |
| &lt;서비스&gt; | 프록시 클래스를 생성 하는 추가 웹 서비스 참조를 제공 합니다. |
| &lt;asp: ServiceReference&gt; | 특정 웹 서비스 참조를 나타냅니다. |

ScriptManager 컨트롤은 ASP.NET AJAX 확장의 필수 핵심입니다. 스크립트 라이브러리에 대 한 액세스를 제공 하 고 (광범위 한 클라이언트 쪽 스크립트 유형 시스템 포함) 부분 렌더링을 지원 하며, 추가 ASP.NET 서비스 (예: 인증 및 프로 파일링, 기타 웹 서비스)에 대 한 광범위 한 지원을 제공 합니다. 또한 ScriptManager 컨트롤은 클라이언트 스크립트에 대 한 세계화 및 지역화 지원을 제공 합니다.

## <a name="providing-alternative-and-supplemental-scripts"></a>대체 및 추가 스크립트 제공

Microsoft ASP.NET 2.0 AJAX 확장에는 디버그 버전과 릴리스 버전의 전체 스크립트 코드가 참조 된 어셈블리에 포함 된 리소스로 포함 되어 있지만, 개발자는 사용자 지정 된 스크립트 파일에 대 한 ScriptManager와 레지스터를 모두 사용할 수 있습니다. 추가 필요한 스크립트

WebForms 네임 스페이스 및 사용자 지정 입력 시스템을 지 원하는 스크립트와 같이 일반적으로 포함 된 스크립트에 대 한 기본 바인딩을 재정의 하려면 ScriptManager 클래스의 `ResolveScriptReference` 이벤트를 등록할 수 있습니다. 이 메서드가 호출 되 면 이벤트 처리기는 해당 스크립트 파일에 대 한 경로를 변경할 수 있습니다. 그러면 스크립트 관리자가 다른 또는 사용자 지정 된 스크립트 복사본을 클라이언트에 보냅니다.

또한 `ScriptReference` 클래스로 표시 되는 스크립트 참조를 프로그래밍 방식으로 또는 태그를 통해 포함할 수 있습니다. 이렇게 하려면 `ScriptManager.Scripts` 컬렉션을 프로그래밍 방식으로 수정 하거나 ScriptManager 컨트롤의 첫 번째 수준 자식인 `<Scripts>` 태그 아래에 `<asp:ScriptReference>` 태그를 포함 합니다.

## <a name="custom-error-handling-for-updatepanels"></a>UpdatePanels에 대 한 사용자 지정 오류 처리

업데이트는 UpdatePanel 컨트롤에 의해 지정 된 트리거에서 처리 되지만 오류 처리 및 사용자 지정 오류 메시지에 대 한 지원은 페이지의 ScriptManager 컨트롤 인스턴스에 의해 처리 됩니다. 이렇게 하려면 `AsyncPostBackError`이벤트를 페이지에 노출 하 여 사용자 지정 예외 처리 논리를 제공할 수 있습니다.

AsyncPostBackError 이벤트를 사용 하 여 `AsyncPostBackErrorMessage` 속성을 지정할 수 있습니다. 그러면 콜백이 완료 될 때 경고 상자가 발생 합니다.

기본 경고 상자를 사용 하는 대신 클라이언트 쪽 사용자 지정도 가능 합니다. 예를 들어 기본 브라우저 모달 대화 상자가 아닌 사용자 지정 된 `<div>` 요소를 표시 하려고 할 수 있습니다. 이 경우 클라이언트 스크립트에서 오류를 처리할 수 있습니다.

**목록 5: 사용자 지정 오류를 표시 하는 클라이언트 쪽 스크립트**

[!code-html[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample4.html)]

매우 간단 하 게 말하자면 위의 스크립트는 비동기 요청이 완료 되었을 때에 클라이언트 쪽 AJAX 런타임에 콜백을 등록 합니다. 그런 다음 오류가 보고 되었는지 여부를 확인 하 고, 오류가 발생 한 경우 해당 오류를 처리 하 고, 마지막으로 사용자 지정 스크립트에서 오류를 처리 했음을 런타임에 표시 합니다.

## <a name="globalization-and-localization-support"></a>세계화 및 지역화 지원

ScriptManager 컨트롤은 스크립트 문자열 및 사용자 인터페이스 구성 요소의 지역화에 대 한 광범위 한 지원을 제공 합니다. 그러나이 항목은이 백서에서 다루지 않습니다. 자세한 내용은 ASP.NET AJAX 확장에서의 세계화 지원 백서를 참조 하세요.

## <a name="the-updatepanel-control"></a>UpdatePanel 컨트롤

## <a name="updatepanel-control-reference"></a>UpdatePanel 컨트롤 참조

태그 사용 속성:

| **속성 이름** | **형식** | **설명** |
| --- | --- | --- |
| ChildrenAsTriggers | bool | 다시 게시할 때 자식 컨트롤이 새로 고침을 자동으로 호출할지 여부를 지정 합니다. |
| RenderMode | enum (블록, 인라인) | 콘텐츠를 시각적으로 표시 하는 방법을 지정 합니다. |
| UpdateMode | enum (항상, 조건부) | 부분적 렌더링 중 UpdatePanel을 항상 새로 고칠지 아니면 트리거가 적중 될 때만 새로 고칠지를 지정 합니다. |

코드 전용 속성:

| **속성 이름** | **형식** | **설명** |
| --- | --- | --- |
| IsInPartialRendering | bool | UpdatePanel이 현재 요청에 대 한 부분 렌더링을 지원 하는지 여부를 가져옵니다. |
| ContentTemplate | ITemplate | 업데이트 요청에 대 한 태그 템플릿을 가져옵니다. |
| ContentTemplateContainer | 제어 | 업데이트 요청에 대 한 프로그래밍 템플릿을 가져옵니다. |
| 트리거 | UpdatePanel-TriggerCollection | 현재 UpdatePanel과 연결 된 트리거의 목록을 가져옵니다. |

공용 코드 메서드:

| **메서드 이름** | **형식** | **설명** |
| --- | --- | --- |
| Update () | Void | 지정 된 UpdatePanel을 프로그래밍 방식으로 업데이트 합니다. 서버 요청에서 트리거 되지 않은 UpdatePanel의 부분 렌더링을 트리거할 수 있도록 허용 합니다. |

태그 하위 항목:

| **Tag** | **설명** |
| --- | --- |
| &lt;System.windows.controls.contentcontrol.contenttemplate&gt; | 부분 렌더링 결과를 렌더링 하는 데 사용할 태그를 지정 합니다. &lt;asp: UpdatePanel&gt;의 자식입니다. |
| &lt;트리거&gt; | 이 UpdatePanel 업데이트와 연결 된 *n 개* 컨트롤의 컬렉션을 지정 합니다. &lt;asp: UpdatePanel&gt;의 자식입니다. |
| &lt;asp: AsyncPostBackTrigger&gt; | 지정 된 UpdatePanel에 대해 부분 페이지 렌더링을 호출 하는 트리거를 지정 합니다. 이는 해당 하는 UpdatePanel의 하위 항목 일 수도 있고 그렇지 않을 수도 있습니다. 이벤트 이름에 대 한 세부적인 &lt;트리거의 자식&gt;입니다. |
| &lt;asp: PostBackTrigger&gt; | 전체 페이지를 새로 고치도록 하는 컨트롤을 지정 합니다. 이는 해당 하는 UpdatePanel의 하위 항목 일 수도 있고 그렇지 않을 수도 있습니다. 개체에 대 한 세부적인 &lt;트리거의 자식&gt;입니다. |

`UpdatePanel` 컨트롤은 AJAX 확장의 부분 렌더링 기능에 참여 하는 서버측 콘텐츠를 구분 하는 컨트롤입니다. 페이지에 있을 수 있는 UpdatePanel 컨트롤의 수에는 제한이 없으며 중첩 될 수도 있습니다. 각 UpdatePanel은 격리 되므로 각 UpdatePanel은 독립적으로 작동할 수 있습니다. 즉, 두 개의 UpdatePanels 동시에 실행 될 수 있으며 페이지의 포스트백과 독립적으로 페이지의 서로 다른 부분을 렌더링할 수 있습니다.

UpdatePanel 컨트롤은 주로 컨트롤 트리거를 처리 합니다. 기본적으로 다시 게시를 만드는 UpdatePanel의 `ContentTemplate` 내에 포함 된 모든 컨트롤은 UpdatePanel에 대 한 트리거로 등록 됩니다. 즉, UpdatePanel은 사용자 컨트롤을 포함 하 여 기본 데이터 바인딩된 컨트롤 (예: GridView)에서 사용할 수 있으며 스크립트에서 프로그래밍할 수 있습니다.

기본적으로 부분 페이지 렌더링을 트리거하는 경우 해당 작업에 대해 UpdatePanel 컨트롤에서 정의 된 트리거가 있는지 여부에 관계 없이 페이지의 모든 UpdatePanel 컨트롤이 새로 고쳐집니다. 예를 들어 하나의 UpdatePanel에서 단추 컨트롤을 정의 하 고 해당 단추 컨트롤을 클릭 하면 해당 페이지의 모든 UpdatePanel 컨트롤이 기본적으로 새로 고쳐집니다. 이는 기본적으로 UpdatePanel의 `UpdateMode` 속성이 `Always`로 설정 되었기 때문입니다. 또는 UpdateMode 속성을 `Conditional`로 설정할 수 있습니다. 즉, 특정 트리거가 적중 되는 경우에만 UpdatePanel을 새로 고칠 수 있습니다.

## <a name="custom-control-notes"></a>사용자 지정 컨트롤 메모

UpdatePanel은 모든 사용자 정의 컨트롤 또는 사용자 지정 컨트롤에 추가할 수 있습니다. 그러나 이러한 컨트롤이 포함 된 페이지에는 EnablePartialRendering 속성을 **true**로 설정 하 여 ScriptManager 컨트롤도 포함 되어야 합니다.

웹 사용자 지정 컨트롤을 사용할 때이를 고려 하는 한 가지 방법은 `CompositeControl` 클래스의 보호 된 `CreateChildControls()` 메서드를 재정의 하는 것입니다. 이렇게 하면 페이지에서 부분 렌더링을 지원 하는지 확인 하는 경우 컨트롤의 자식과 외부 영역 사이에 UpdatePanel을 삽입할 수 있습니다. 그렇지 않으면 자식 컨트롤을 컨테이너 `Control` 인스턴스로 계층화 하면 됩니다.

## <a name="updatepanel-considerations"></a>UpdatePanel 고려 사항

UpdatePanel은 JavaScript XMLHttpRequest의 컨텍스트 내에서 ASP.NET 다시 게시를 래핑하는 블랙 박스로 작동 합니다. 그러나 동작과 속도 측면에서 모두 염두에 두어야 하는 중요 한 성능 고려 사항이 있습니다. 사용 시기를 결정할 수 있도록 UpdatePanel이 작동 하는 방식을 이해 하려면 AJAX exchange를 검사 해야 합니다. 다음 예제에서는 기존 사이트 및 Firebug 확장을 사용 하는 Mozilla Firefox를 사용 합니다 (Firebug에서 XMLHttpRequest 데이터 캡처).

특히 폼 이나 컨트롤에서 city 및 state 필드를 채워야 하는 우편 번호 텍스트 상자가 있는 폼을 생각해 보겠습니다. 이 양식은 궁극적으로 사용자의 이름, 주소 및 연락처 정보를 비롯 한 멤버 자격 정보를 수집 합니다. 특정 프로젝트의 요구 사항에 따라 고려해 야 할 다양 한 디자인 고려 사항이 있습니다.

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image11.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image10.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image12.png))

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image14.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image13.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image15.png))

이 응용 프로그램의 원래 반복에서 우편 번호, 구/군/시 및 시/도를 포함 하 여 전체 사용자 등록 데이터를 통합 하는 컨트롤이 빌드 되었습니다. 전체 컨트롤이 UpdatePanel 내에 래핑되어 웹 폼에 끌어 놓 었으 며, 사용자가 우편 번호를 입력 하면 UpdatePanel은 트리거를 지정 하거나 ChildrenAsTriggers 속성을 true로 설정 하 여 백 엔드의 해당 TextChanged 이벤트를 검색 합니다. AJAX는 FireBug에서 캡처한 대로 UpdatePanel 내의 모든 필드를 게시 합니다 (오른쪽의 다이어그램 참조).

화면 캡처에 표시 된 것 처럼 UpdatePanel에 있는 모든 컨트롤의 값 (이 경우 모두 비어 있음) 및 ViewState 필드가 표시 됩니다. 실제로이 특정 요청을 수행 하는 데 5 바이트의 데이터만 필요한 경우 9kb를 초과 하는 데이터가 전송 됩니다. 응답은 훨씬 더 커질 수 있습니다. 즉, 총 57kb가 클라이언트에 전송 되 고 단순히 텍스트 필드 및 드롭다운 필드를 업데이트 합니다.

ASP.NET AJAX에서 프레젠테이션을 업데이트 하는 방법을 확인 하는 데에도 관심이 있을 수 있습니다. UpdatePanel의 업데이트 요청에 대 한 응답 부분이 왼쪽에 표시 되는 Firebug 콘솔에 표시 됩니다. 클라이언트 스크립트로 분할 된 다음 페이지에서 다시 어셈블된 특수 하 게 작성 된 파이프로 구분 된 문자열입니다. 특히 ASP.NET AJAX는 UpdatePanel을 나타내는 클라이언트의 HTML 요소에 대 한 *innerHTML* 속성을 설정 합니다. 브라우저에서 DOM을 다시 생성할 때 처리 해야 하는 정보의 양에 따라 약간의 지연이 발생 합니다.

DOM을 다시 생성 하면 많은 추가 문제가 발생 합니다.

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image17.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image16.png)

([전체 크기 이미지를 보려면 클릭](understanding-partial-page-updates-with-asp-net-ajax/_static/image18.png))

- 포커스가 있는 HTML 요소가 UpdatePanel 내에 있으면 포커스가 손실 됩니다. 따라서 Tab 키를 눌러 우편 번호 텍스트 상자를 종료 하는 사용자의 경우 다음 대상이 City 텍스트 상자입니다. 그러나 UpdatePanel에서 디스플레이를 새로 고치면 폼이 더 이상 포커스를 갖지 않으며 Tab 키를 누르면 포커스 요소 (예: 링크)가 강조 표시 되기 시작 했습니다.
- DOM 요소에 액세스 하는 사용자 지정 클라이언트 쪽 스크립트 형식이 사용 되는 경우 부분 포스트백 후에 함수에 의해 지속 된 참조가 존재 하지 않을 수 있습니다.

UpdatePanels는 전체 솔루션을 위한 것이 아닙니다. 대신, 프로토타입 (ASP.NET)을 비롯 한 특정 상황에 대 한 빠른 솔루션을 제공 하 고, .NET 개체 모델을 잘 알고 있지만 DOM을 사용 하는 것이 적은 개발자를 위한 친숙 한 인터페이스를 제공 합니다. 응용 프로그램 시나리오에 따라 성능을 향상 시킬 수 있는 여러 가지 대안이 있습니다.

- PageMethods 및 JSON (JavaScript Object Notation)을 사용 하면 개발자가 웹 서비스 호출이 호출 된 것 처럼 페이지에서 정적 메서드를 호출할 수 있습니다. 메서드가 정적 이므로 상태는 필요 하지 않습니다. 스크립트 호출자는 매개 변수를 제공 하 고 결과는 비동기식으로 반환 됩니다.
- 응용 프로그램 전체의 여러 위치에서 단일 컨트롤을 사용 해야 하는 경우 웹 서비스 및 JSON을 사용 하는 것이 좋습니다. 이렇게 하면 특별 한 작업이 거의 필요 하지 않으며 비동기적으로 작동 합니다.

웹 서비스 또는 페이지 메서드를 통해 기능을 통합 하는 경우에도 단점이 있습니다. 무엇 보다도 ASP.NET 개발자는 일반적으로 사용자 정의 컨트롤 (.ascx 파일)에 작은 기능 구성 요소를 빌드하는 경향이 있습니다. 페이지 메서드는 이러한 파일에서 호스팅될 수 없습니다. 실제 .aspx 페이지 클래스 내에서 호스팅되어야 합니다. 이와 유사 하 게 웹 서비스는 .asmx 클래스 내에서 호스팅되어야 합니다. 응용 프로그램에 따라이 아키텍처는 단일 책임 원칙을 위반할 수 있습니다. 단, 단일 구성 요소에 대 한 기능을 두 개 이상의 물리적 구성 요소에 분산 하는 것이 좋습니다.

마지막으로 응용 프로그램에서 UpdatePanels를 사용 해야 하는 경우 다음 지침을 사용 하 여 문제 해결 및 유지 관리를 지원 해야 합니다.

- **단위를 제외 하 고 코드 단위에 걸쳐 가능한 한 적은 UpdatePanels를 중첩 합니다.** 예를 들어, 컨트롤을 래핑하는 페이지에 UpdatePanel을 포함 하는 반면, 해당 컨트롤에는 UpdatePanel을 포함 하는 다른 컨트롤을 포함 하는 UpdatePanel이 포함 되어 있습니다. 이를 통해 새로 고쳐야 하는 요소를 명확 하 게 유지 하 고 예기치 않은 새로 고침을 자식 UpdatePanels 방지할 수 있습니다.
- ***ChildrenAsTriggers* 속성을 false로 설정 된 상태로 유지 하 고 트리거 이벤트를 명시적으로 설정 합니다.** `<Triggers>` 컬렉션을 활용 하 여 이벤트를 처리 하는 것이 훨씬 더 분명 하 고, 예기치 않은 동작을 방지 하 고 유지 관리 작업을 지원 하며 개발자가 이벤트를 옵트인 하도록 강제할 수 있습니다.
- **가장 작은 단위를 사용 하 여 기능을 달성할 수 있습니다.** 우편 번호 서비스에 대 한 설명에 나와 있는 것 처럼, 서버에 대 한 최소의 시간을 단축 하는 것 처럼, 전체 처리 및 클라이언트-서버 교환의 사용 공간에 대 한 공간을 래핑 하 여 성능을 향상 시킵니다.

## <a name="the-updateprogress-control"></a>UpdateProgress 컨트롤

## <a name="updateprogress-control-reference"></a>UpdateProgress 컨트롤 참조

태그 사용 속성:

| **속성 이름** | **형식** | **설명** |
| --- | --- | --- |
| AssociatedUpdate-PanelID | String | 이 UpdateProgress에서 보고 해야 하는 UpdatePanel의 ID를 지정 합니다. |
| DisplayAfter | Int | 비동기 요청이 시작 된 후이 컨트롤이 표시 되기까지 제한 시간 (밀리초)을 지정 합니다. |
| DynamicLayout | bool | 진행률이 동적으로 렌더링 되는지 여부를 지정 합니다. |

태그 하위 항목:

| **Tag** | **설명** |
| --- | --- |
| &lt;ProgressTemplate&gt; | 이 컨트롤과 함께 표시 되는 콘텐츠에 대 한 컨트롤 템플릿 집합을 포함 합니다. |

UpdateProgress 컨트롤은 서버에 전송 하는 데 필요한 작업을 수행 하는 동안 사용자의 관심을 유지 하는 피드백을 제공 합니다. 이렇게 하면 사용자가 명확 하지 않을 수 있지만, 특히 대부분의 사용자가 페이지 새로 고침 및 상태 표시줄 강조 표시에 사용 되기 때문에 사용자가 작업을 수행 하는 것을 알 수 있습니다.

참고로, UpdateProgress 컨트롤은 페이지 계층의 어디에 나 나타날 수 있습니다. 그러나 하위 updatepanel이 다른 UpdatePanel 내에 중첩 된 자식 UpdatePanel에서 시작 되는 경우 자식 UpdatePanel을 트리거하는 포스트백이 UpdateProgress 템플릿이 자식 키에 표시 됩니다. UpdatePanel 뿐만 아니라 부모 UpdatePanel도 있습니다. 그러나 트리거가 부모 UpdatePanel의 직계 자식인 경우 부모와 연결 된 UpdateProgress 템플릿만 표시 됩니다.

## <a name="summary"></a>요약

Microsoft ASP.NET AJAX 확장은 웹 콘텐츠를 보다 쉽게 액세스할 수 있도록 하 고 웹 응용 프로그램에 보다 풍부한 사용자 환경을 제공 하기 위해 설계 된 정교한 제품입니다. ASP.NET AJAX 확장의 일부로 ScriptManager, UpdatePanel 및 UpdateProgress 컨트롤을 포함 한 부분 페이지 렌더링 컨트롤은 도구 키트의 가장 표시 되는 구성 요소 중 일부입니다.

ScriptManager 구성 요소는 확장에 대 한 클라이언트 JavaScript의 프로 비전을 통합 하 고, 다양 한 서버 및 클라이언트 쪽 구성 요소가 개발 투자를 최소화 하면서 함께 작동할 수 있도록 합니다.

UpdatePanel 컨트롤은 UpdatePanel 내에서 서버 쪽 코드 숨김을 포함 하 고 페이지 새로 고침을 트리거하지 않을 수 있는 명백한 마법 상자 태그입니다. UpdatePanel 컨트롤은 중첩 될 수 있으며 다른 UpdatePanels의 컨트롤에 따라 달라질 수 있습니다. 기본적으로 UpdatePanels는 해당 하위 컨트롤에 의해 호출 되는 모든 포스트백을 처리 하지만 선언적으로 또는 프로그래밍 방식으로이 기능을 세밀 하 게 조정할 수 있습니다.

UpdatePanel 컨트롤을 사용 하는 경우 개발자는 잠재적으로 발생할 수 있는 성능 영향에 대해 알고 있어야 합니다. 응용 프로그램 디자인을 고려해 야 하지만 웹 서비스 및 페이지 메서드를 사용할 수도 있습니다.

UpdateProgress 컨트롤을 사용 하면 사용자가 무시 되 고 있지 않으며 페이지에서 사용자 입력에 응답 하기 위해 다른 작업을 수행 하지 않는 동안 백그라운드에서 요청을 처리 하 고 있음을 알 수 있습니다. 또한 부분 렌더링 결과를 중단할 수 있는 기능도 포함 되어 있습니다.

이러한 도구는 서버 작업을 사용자에 게 명확 하 게 구분 하 고 워크플로를 중단 하지 않도록 하 여 풍부 하 고 원활한 사용자 환경을 만드는 데 도움이 됩니다.

## <a name="bio"></a>약력

Scott Cate cda (는 1997부터 Microsoft 웹 기술을 사용 하 고 있으며 기술 자료 소프트웨어 솔루션에 초점을 맞춘 ASP.NET 기반 응용 프로그램을 전문적으로 작성 하는[www.myKB.com](http://www.myKB.com)(myKB.com)의 부사장입니다. Scott은 [scott.cate@myKB.com](mailto:scott.cate@myKB.com) 또는 [ScottCate.com](http://ScottCate.com) 의 블로그의 전자 메일을 통해 연락할 수 있습니다.

> [!div class="step-by-step"]
> [다음](understanding-asp-net-ajax-updatepanel-triggers.md)
