---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: ASP.NET 2.0 페이지 모델 | Microsoft Docs
author: microsoft
description: ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 기반 코드 모델 중에서 선택할 것입니다. 코드 숨김이 Src 특성을 사용 하 여 구현 될 수 있습니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440711"
---
# <a name="the-aspnet-20-page-model"></a>ASP.NET 2.0 페이지 모델

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 기반 코드 모델 중에서 선택할 것입니다. 코드 숨김은 Src 특성을 사용 하거나 @Page 지시문의 CodeBehind 특성을 사용 하 여 구현할 수 있습니다. ASP.NET 2.0에서 개발자는 인라인 코드와 코드 숨김으로 선택할 수 있지만 코드 숨김이 크게 향상 되었습니다.

ASP.NET 1.x에서 개발자는 인라인 코드 모델과 코드 기반 코드 모델 중에서 선택할 것입니다. 코드 숨김은 Src 특성을 사용 하거나 @Page 지시문의 CodeBehind 특성을 사용 하 여 구현할 수 있습니다. ASP.NET 2.0에서 개발자는 인라인 코드와 코드 숨김으로 선택할 수 있지만 코드 숨김이 크게 향상 되었습니다.

## <a name="improvements-in-the-code-behind-model"></a>코드 숨김이 향상 된 기능

ASP.NET 2.0에서 코드 숨겨진 모델의 변경 내용을 완전히 이해 하려면 모델을 ASP.NET 1.x에 있던 것과 같이 신속 하 게 검토 하는 것이 가장 좋습니다.

## <a name="the-code-behind-model-in-aspnet-1x"></a>ASP.NET 1.x의 코드 숨김이 모델

ASP.NET 1.x에서 코드에 포함 된 모델은 ASPX 파일 (Webform) 및 프로그래밍 코드를 포함 하는 코드를 포함 하는 파일로 이루어져 있습니다. 두 파일은 ASPX 파일의 @Page 지시어를 사용 하 여 연결 되었습니다. ASPX 페이지의 각 컨트롤에는 인스턴스 변수로 코드 숨김이 파일에 해당 하는 선언이 있습니다. 코드 숨김으로는 이벤트 바인딩과 Visual Studio 디자이너에 필요한 생성 된 코드에 대 한 코드도 포함 되어 있습니다. 이 모델은 상당히 잘 작동 하지만, ASPX 페이지의 모든 ASP.NET 요소에 코드를 입력 하는 데 해당 코드가 필요 하므로 코드와 콘텐츠가 실제로 분리 되지 않았습니다. 예를 들어, 디자이너에서 Visual Studio IDE 외부의 ASPX 파일에 새 서버 컨트롤을 추가한 경우 코드 숨기기 파일의 해당 컨트롤에 대 한 선언이 없기 때문에 응용 프로그램이 중단 됩니다.

## <a name="the-code-behind-model-in-aspnet-20"></a>ASP.NET 2.0의 코드 숨김이 모델

ASP.NET 2.0은이 모델에 대해 크게 향상 되었습니다. ASP.NET 2.0에서 코드 숨김이 ASP.NET 2.0에 제공 된 새로운 *partial 클래스* 를 사용 하 여 구현 됩니다. ASP.NET 2.0의 코드 숨김이 클래스는 partial 클래스로 정의 됩니다. 즉, 클래스 정의의 일부만 포함 하 고 있습니다. 클래스 정의의 나머지 부분은 런타임에 ASPX 페이지를 사용 하 여 ASP.NET 2.0에 의해 동적으로 생성 되거나 웹 사이트를 미리 컴파일하는 경우에 생성 됩니다. @ Page 지시문을 사용 하 여 코드 숨김이 파일 및 ASPX 페이지 간의 링크를 설정할 수 있습니다. 그러나 CodeBehind 또는 Src 특성 대신 ASP.NET 2.0은 이제 CodeFile 특성을 사용 합니다. Inherits 특성은 페이지의 클래스 이름을 지정 하는 데도 사용 됩니다.

일반적인 @ Page 지시문은 다음과 같습니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

ASP.NET 2.0 코드 숨김으로 표시 되는 일반적인 클래스 정의는 다음과 같습니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C#및 Visual Basic는 현재 부분 클래스를 지 원하는 관리 되는 유일한 언어입니다. 따라서 j #을 사용 하는 개발자는 ASP.NET 2.0에서 코드 숨김이 모델을 사용할 수 없습니다.

개발자가 만든 코드만 포함 하는 코드 파일을 포함 하는 코드 파일을 새 모델에서 사용할 수 있습니다. 또한 코드 숨김이 파일에 인스턴스 변수 선언이 없기 때문에 코드와 콘텐츠의 진정한 분리를 제공 합니다.

> [!NOTE]
> ASPX 페이지의 partial 클래스는 이벤트 바인딩이 발생 하는 위치 이기 때문에 Visual Basic 개발자는 코드 숨김으로 Handles 키워드를 사용 하 여 이벤트를 바인딩하는 방법으로 약간의 성능 향상을 실현할 수 있습니다. C#에 해당 하는 키워드가 없습니다.

## <a name="new--page-directive-attributes"></a>새 @ Page 지시문 특성

ASP.NET 2.0는 @ Page 지시문에 많은 새 특성을 추가 합니다. ASP.NET 2.0의 새로운 특성은 다음과 같습니다.

## <a name="async"></a>Async

Async 특성을 사용 하면 비동기적으로 실행 되도록 페이지를 구성할 수 있습니다. 이 모듈의 뒷부분에서 비동기 페이지를 잘 다룹니다.

## <a name="asynctimeout"></a>AsyncTimeout

비동기 페이지에 대 한 제한 시간을 지정 했습니다. 기본값은 45 초입니다.

## <a name="codefile"></a>CodeFile

CodeFile 특성은 Visual Studio 2002/2003의 CodeBehind 특성에 대 한 대체입니다.

### <a name="codefilebaseclass"></a>CodeFileBaseClass

CodeFileBaseClass 특성은 여러 페이지가 단일 기본 클래스에서 파생 되 게 하려는 경우에 사용 됩니다. 이 특성이 없는 ASP.NET의 partial 클래스 구현으로 인해 안전망 컴파일 엔진은 페이지의 컨트롤을 기반으로 새 멤버를 자동으로 만들기 때문에 ASPX 페이지에 선언 된 컨트롤을 참조 하는 데 공유 공통 필드를 사용 하는 기본 클래스가 제대로 작동 하지 않습니다. 따라서 ASP.NET에서 둘 이상의 페이지에 대 한 공통 기본 클래스를 원하는 경우 CodeFileBaseClass 특성에 기본 클래스를 지정 하 고 해당 기본 클래스에서 각 pages 클래스를 파생 하도록 정의 해야 합니다. 이 특성을 사용 하는 경우에도 CodeFile 특성이 필요 합니다.

## <a name="compilationmode"></a>CompilationMode

이 특성을 사용 하면 ASPX 페이지의 CompilationMode 속성을 설정할 수 있습니다. CompilationMode 속성은 **항상**, **Auto**및 **Never**값을 포함 하는 열거형입니다. 기본값은 **항상**입니다. **자동** 설정은 ASP.NET가 페이지를 동적으로 컴파일하는 것을 방지 합니다 (가능한 경우). 동적 컴파일의 페이지를 제외 하면 성능이 향상 됩니다. 그러나 제외 된 페이지에 컴파일해야 하는 코드가 포함 되어 있으면 페이지를 검색할 때 오류가 발생 합니다.

## <a name="enableeventvalidation"></a>EnableEventValidation

이 특성은 다시 게시 및 콜백 이벤트의 유효성을 검사할지 여부를 지정 합니다. 이 기능을 사용 하는 경우 다시 게시 또는 콜백 이벤트에 대 한 인수를 검사 하 여 원래 렌더링 한 서버 컨트롤에서 해당 인수를 생성 했는지 확인 합니다.

## <a name="enabletheming"></a>EnableTheming

이 특성은 페이지에서 ASP.NET 테마를 사용할지 여부를 지정 합니다. 기본값은 **false**입니다. ASP.NET 테마는 [모듈 10](profiles-themes-and-web-parts.md)에서 설명 합니다.

## <a name="linepragmas"></a>LinePragmas

이 특성은 컴파일하는 동안 줄 pragma를 추가할지 여부를 지정 합니다. 줄 pragma는 디버거에서 특정 코드 섹션을 표시 하는 데 사용 되는 옵션입니다.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

이 특성은 포스트백 사이에서 스크롤 위치를 유지 하기 위해 JavaScript가 페이지에 삽입 되는지 여부를 지정 합니다. 이 특성은 기본적으로 **false** 입니다.

이 특성을 **true로 설정**하면 ASP.NET는 &lt;스크립트&gt; 추가 하 여 다음과 같은 다시 게시를 차단 합니다.

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

이 스크립트 블록의 src는 Webresource.axd입니다. 이 리소스는 실제 경로가 아닙니다. 이 스크립트를 요청 하면 ASP.NET는 스크립트를 동적으로 작성 합니다.

### <a name="masterpagefile"></a>MasterPageFile

이 특성은 현재 페이지의 마스터 페이지 파일을 지정 합니다. 경로는 상대적이거나 절대적일 수 있습니다. 마스터 페이지는 [모듈 4](master-pages.md)에서 다룹니다.

## <a name="stylesheettheme"></a>StyleSheetTheme

이 특성을 사용 하면 ASP.NET 2.0 테마에서 정의한 사용자 인터페이스 모양 속성을 재정의할 수 있습니다. 테마는 [모듈 10](profiles-themes-and-web-parts.md)에서 설명 합니다.

## <a name="theme"></a>테마

페이지의 테마를 지정 합니다. StyleSheetTheme 특성에 값이 지정 되지 않은 경우 테마 특성은 페이지의 컨트롤에 적용 된 모든 스타일을 재정의 합니다.

## <a name="title"></a>제목

페이지의 제목을 설정 합니다. 여기에 지정 된 값은 렌더링 된 페이지의 &lt;title&gt; 요소에 표시 됩니다.

### <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

ViewStateEncryptionMode 열거의 값을 설정 합니다. 사용 가능한 값은 **항상**, **자동**, **안 함**입니다. 기본값은 **Auto**입니다. 이 특성이 **Auto**값으로 설정 된 경우 viewstate는 암호화 됩니다. **RegisterRequiresViewStateEncryption** 메서드를 호출 하 여 컨트롤에서 요청 합니다.

## <a name="setting-public-property-values-via-the--page-directive"></a>@ Page 지시문을 통해 Public 속성 값 설정

ASP.NET 2.0의 @ Page 지시문의 또 다른 새로운 기능은 기본 클래스의 공용 속성에 대 한 초기 값을 설정 하는 기능입니다. 예를 들어, 기본 클래스에 **SomeText** 이라는 public 속성이 있고 페이지가 로드 될 때 **Hello** 로 초기화 되는 것과 같습니다. 이렇게 하려면 다음과 같이 @ Page 지시문의 값을 설정 하면 됩니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

@ Page 지시문의 **SomeText** 특성은 기본 클래스에 있는 SomeText 속성의 초기 값을 *Hello!* 로 설정 합니다. 다음 비디오는 @ Page 지시어를 사용 하 여 기본 클래스에서 공용 속성의 초기 값을 설정 하는 연습입니다.

![](the-asp-net-2-0-page-model/_static/image1.png)

[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>Page 클래스의 새 Public 속성

ASP.NET 2.0의 새로운 공용 속성은 다음과 같습니다.

## <a name="apprelativetemplatesourcedirectory"></a>AppRelativeTemplateSourceDirectory

페이지 또는 컨트롤에 대 한 응용 프로그램 상대 경로를 반환 합니다. 예를 들어 http://app/folder/page.aspx에 있는 페이지의 경우 속성은 ~/folder/.를 반환 합니다.

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

페이지 또는 컨트롤에 대 한 상대 가상 디렉터리 경로를 반환 합니다. 예를 들어 http://app/folder/page.aspx에 있는 페이지에 대 한 속성은

## <a name="asynctimeout"></a>AsyncTimeout

비동기 페이지 처리에 사용 되는 제한 시간을 가져오거나 설정 합니다. 비동기 페이지는이 모듈의 뒷부분에서 설명 합니다.

## <a name="clientquerystring"></a>ClientQueryString

요청 된 URL의 쿼리 문자열 부분을 반환 하는 읽기 전용 속성입니다. 이 값은 URL로 인코딩됩니다. HttpServerUtility 클래스의 UrlDecode 메서드를 사용 하 여이를 디코딩할 수 있습니다.

## <a name="clientscript"></a>ClientScript

이 속성은 클라이언트 쪽 스크립트의 안전망 내보내기를 관리 하는 데 사용할 수 있는 ClientScriptManager 개체를 반환 합니다. ClientScriptManager 클래스는이 모듈의 뒷부분에 설명 되어 있습니다.

## <a name="enableeventvalidation"></a>EnableEventValidation

이 속성은 다시 게시 및 콜백 이벤트에 대해 이벤트 유효성 검사를 사용할지 여부를 제어 합니다. 이 기능을 사용 하도록 설정 하면 다시 게시 또는 콜백 이벤트에 대 한 인수를 확인 하 여 원래 렌더링 한 서버 컨트롤에서 해당 인수를 생성 했는지 확인 합니다.

## <a name="enabletheming"></a>EnableTheming

이 속성은 ASP.NET 2.0 테마가 페이지에 적용 되는지 여부를 지정 하는 부울을 가져오거나 설정 합니다.

## <a name="form"></a>Form

이 속성은 ASPX 페이지의 HTML 폼을 HtmlForm 개체로 반환 합니다.

## <a name="header"></a>헤더

이 속성은 페이지 헤더를 포함 하는 HtmlHead 개체에 대 한 참조를 반환 합니다. 반환 된 HtmlHead 개체를 사용 하 여 스타일 시트, 메타 태그 등을 가져오거나 설정할 수 있습니다.

## <a name="idseparator"></a>IdSeparator

이 읽기 전용 속성은 ASP.NET가 페이지에서 컨트롤의 고유 ID를 빌드할 때 컨트롤 식별자를 구분 하는 데 사용 되는 문자를 가져옵니다. 코드에서 직접 사용하기에 적합하지 않습니다.

## <a name="isasync"></a>IsAsync

이 속성은 비동기 페이지를 허용 합니다. 비동기 페이지는이 모듈의 뒷부분에서 설명 합니다.

## <a name="iscallback"></a>IsCallback

이 읽기 전용 속성은 페이지가 콜백 된 경우 **true** 를 반환 합니다. 호출 백업은이 모듈의 뒷부분에서 설명 합니다.

## <a name="iscrosspagepostback"></a>IsCrossPagePostBack

페이지가 페이지 간 포스트백의 일부인 경우이 읽기 전용 속성은 **true** 를 반환 합니다. 페이지 간 포스트백은이 모듈의 뒷부분에서 설명 합니다.

## <a name="items"></a>Items

페이지 컨텍스트에 저장 된 모든 개체를 포함 하는 IDictionary 인스턴스에 대 한 참조를 반환 합니다. 이 IDictionary 개체에 항목을 추가할 수 있으며 컨텍스트의 수명 동안 해당 항목을 사용할 수 있습니다.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostBack

이 속성은 포스트백이 발생 한 후 브라우저에서 페이지 스크롤 위치를 유지 하는 JavaScript를 ASP.NET에서 제거할지 여부를 제어 합니다. 이 속성에 대 한 자세한 내용은이 모듈의 앞부분에서 설명 했습니다.

## <a name="master"></a>마스터

이 읽기 전용 속성은 마스터 페이지가 적용 된 페이지에 대 한 MasterPage 인스턴스에 대 한 참조를 반환 합니다.

## <a name="masterpagefile"></a>MasterPageFile

페이지의 마스터 페이지 파일 이름을 가져오거나 설정 합니다. 이 속성은 PreInit 메서드에만 설정할 수 있습니다.

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

이 속성은 페이지 상태에 대 한 최대 길이 (바이트)를 가져오거나 설정 합니다. 속성이 양수로 설정 된 경우 페이지 뷰 상태는 지정 된 바이트 수를 초과 하지 않도록 여러 개의 숨겨진 필드로 분할 됩니다. 속성이 음수 이면 뷰 상태가 청크로 분할 되지 않습니다.

## <a name="pageadapter"></a>PageAdapter

요청 하는 브라우저의 페이지를 수정 하는 PageAdapter 개체에 대 한 참조를 반환 합니다.

## <a name="previouspage"></a>PreviousPage

서버. 전송 또는 페이지 간 포스트백의 경우 이전 페이지에 대 한 참조를 반환 합니다.

## <a name="skinid"></a>SkinID

페이지에 적용할 ASP.NET 2.0 스킨을 지정 합니다.

## <a name="stylesheettheme"></a>StyleSheetTheme

이 속성은 페이지에 적용 되는 스타일 시트를 가져오거나 설정 합니다.

## <a name="templatecontrol"></a>TemplateControl

페이지의 포함 하는 컨트롤에 대 한 참조를 반환 합니다.

## <a name="theme"></a>테마

페이지에 적용 되는 ASP.NET 2.0 테마의 이름을 가져오거나 설정 합니다. PreInit 메서드 이전에이 값을 설정 해야 합니다.

## <a name="title"></a>제목

이 속성은 페이지 머리글에서 가져온 페이지의 제목을 가져오거나 설정 합니다.

## <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

페이지의 ViewStateEncryptionMode를 가져오거나 설정 합니다. 이 모듈의 앞부분에서이 속성에 대 한 자세한 설명을 참조 하세요.

## <a name="new-protected-properties-of-the-page-class"></a>Page 클래스의 새 Protected 속성

ASP.NET 2.0에서 페이지 클래스의 새 보호 된 속성은 다음과 같습니다.

## <a name="adapter"></a>어댑터

요청한 장치에서 페이지를 렌더링 하는 ControlAdapter에 대 한 참조를 반환 합니다.

## <a name="asyncmode"></a>AsyncMode

이 속성은 페이지가 비동기식으로 처리 되는지 여부를 나타냅니다. 런타임에 사용 하기 위한 것 이며 코드에서 직접 사용할 수 없습니다.

## <a name="clientidseparator"></a>ClientIDSeparator

이 속성은 컨트롤에 대 한 고유한 클라이언트 Id를 만들 때 구분 기호로 사용 되는 문자를 반환 합니다. 런타임에 사용 하기 위한 것 이며 코드에서 직접 사용할 수 없습니다.

## <a name="pagestatepersister"></a>PageStatePersister

이 속성은 페이지에 대 한 PageStatePersister 개체를 반환 합니다. 이 속성은 ASP.NET 컨트롤 개발자가 주로 사용 합니다.

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

이 속성은 브라우저 캐싱에 사용할 파일 경로에 추가 되는 고유 접미사를 반환 합니다. 기본값은 \_\_ufps =이 고 6 자리 숫자입니다.

## <a name="new-public-methods-for-the-page-class"></a>Page 클래스에 대 한 새 공용 메서드

다음 공용 메서드는 ASP.NET 2.0의 Page 클래스에 새로 있습니다.

## <a name="addonprerendercompleteasync"></a>AddOnPreRenderCompleteAsync

이 메서드는 비동기 페이지 실행에 대 한 이벤트 처리기 대리자를 등록 합니다. 비동기 페이지는이 모듈의 뒷부분에서 설명 합니다.

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

페이지 스타일 시트의 속성을 페이지에 적용 합니다.

## <a name="executeregisteredasynctasks"></a>ExecuteRegisteredAsyncTasks

이 메서드는 비동기 작업을 생물 합니다.

### <a name="getvalidators"></a>GetValidators

지정 된 유효성 검사 그룹에 대 한 유효성 검사기 컬렉션 또는 지정 된 항목이 없는 경우 기본 유효성 검사 그룹을 반환 합니다.

## <a name="registerasynctask"></a>RegisterAsyncTask

이 메서드는 새 비동기 작업을 등록 합니다. 비동기 페이지는이 모듈의 뒷부분에서 다룹니다.

## <a name="registerrequirescontrolstate"></a>RegisterRequiresControlState

이 메서드는 pages 컨트롤 상태를 유지 해야 ASP.NET에 지시 합니다.

## <a name="registerrequiresviewstateencryption"></a>RegisterRequiresViewStateEncryption

이 메서드는 페이지 viewstate에 암호화가 필요 ASP.NET에 지시 합니다.

## <a name="resolveclienturl"></a>ResolveClientUrl

이미지에 대 한 클라이언트 요청 등에 사용할 수 있는 상대 URL을 반환 합니다.

## <a name="setfocus"></a>SetFocus

이 메서드는 페이지가 처음 로드 될 때 지정 된 컨트롤에 포커스를 설정 합니다.

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState

이 메서드는 컨트롤 상태 지 속성을 더 이상 요구 하지 않으므로 전달 된 컨트롤의 등록을 취소 합니다.

## <a name="changes-to-the-page-lifecycle"></a>페이지 수명 주기에 대 한 변경

ASP.NET 2.0의 페이지 수명 주기는 크게 변경 되지 않았지만 알아야 할 몇 가지 새로운 방법이 있습니다. ASP.NET 2.0 페이지 수명 주기는 아래에 설명 되어 있습니다.

## <a name="preinit-new-in-aspnet-20"></a>PreInit (ASP.NET 2.0의 새로운 새)

PreInit 이벤트는 개발자가 액세스할 수 있는 수명 주기의 가장 이른 단계입니다. 이 이벤트를 추가 하면 프로그래밍 방식으로 ASP.NET 2.0 테마, 마스터 페이지, ASP.NET 2.0 프로필에 대 한 액세스 속성 등을 변경할 수 있습니다. 다시 게시 상태인 경우에는 Viewstate가 현재 수명 주기의이 시점에서 컨트롤에 아직 적용 되지 않았음을 인식 해야 합니다. 따라서 개발자가이 단계에서 컨트롤의 속성을 변경 하는 경우 나중에 페이지 수명 주기에서 덮어쓸 수 있습니다.

## <a name="init"></a>Init

Init 이벤트는 ASP.NET 1.x에서 변경 되지 않았습니다. 이 위치에서 페이지의 컨트롤 속성을 읽거나 초기화 하려고 합니다. 이 단계에서는 마스터 페이지, 테마 등이 페이지에 이미 적용 되어 있습니다.

## <a name="initcomplete-new-in-20"></a>InitComplete (2.0의 새로운 새)

InitComplete 이벤트는 페이지 초기화 단계가 끝날 때 호출 됩니다. 수명 주기의이 시점에서 페이지의 컨트롤에 액세스할 수 있지만 상태는 아직 채워지지 않았습니다.

## <a name="preload-new-in-20"></a>프리 로드 (2.0의 새로운 새)

이 이벤트는 모든 포스트백 데이터가 적용 된 후 페이지\_로드 직전에 호출 됩니다.

## <a name="load"></a>로드

ASP.NET 1. x에서 로드 이벤트가 변경 되지 않았습니다.

## <a name="loadcomplete-new-in-20"></a>LoadComplete (2.0의 새로운 새)

LoadComplete 이벤트는 페이지 로드 단계의 마지막 이벤트입니다. 이 단계에서는 모든 포스트백 및 viewstate 데이터가 페이지에 적용 되었습니다.

## <a name="prerender"></a>PreRender

페이지에 동적으로 추가 되는 컨트롤에 대해 viewstate를 적절히 유지 하려면 PreRender 이벤트를 추가할 수 있는 마지막 기회입니다.

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete (2.0의 새로운 새)

PreRenderComplete 단계에서 모든 컨트롤이 페이지에 추가 되 고 페이지가 렌더링 될 준비가 되었습니다. PreRenderComplete 이벤트는 페이지 viewstate가 저장 되기 전에 발생 한 마지막 이벤트입니다.

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete (2.0의 새로운 새)

SaveStateComplete 이벤트는 모든 페이지 viewstate와 컨트롤 상태가 저장 된 직후에 호출 됩니다. 이 이벤트는 페이지가 실제로 브라우저에 렌더링 되기 전의 마지막 이벤트입니다.

## <a name="render"></a>렌더링

ASP.NET 1.x 이후 렌더링 메서드가 변경 되지 않았습니다. HtmlTextWriter이 초기화 되 고 페이지가 브라우저에 렌더링 됩니다.

## <a name="cross-page-postback-in-aspnet-20"></a>ASP.NET 2.0에서 페이지 간 다시 게시

ASP.NET 1.x에서는 동일한 페이지에 게시 하는 데 포스트백이 필요 했습니다. 페이지 간 포스트백은 허용 되지 않습니다. ASP.NET 2.0는 IButtonControl 인터페이스를 통해 다른 페이지로 다시 게시 하는 기능을 추가 합니다. 새 IButtonControl 인터페이스를 구현 하는 모든 컨트롤 (Button, LinkButton 및 ImageButton과 타사 사용자 지정 컨트롤)은 PostBackUrl 특성을 사용 하 여이 새로운 기능을 활용할 수 있습니다. 다음 코드에서는 두 번째 페이지에 다시 게시 되는 단추 컨트롤을 보여 줍니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

페이지가 다시 게시 되 면 다시 게시를 시작 하는 페이지는 두 번째 페이지의 PreviousPage 속성을 통해 액세스할 수 있습니다. 이 기능은 ASP.NET 2.0에서 컨트롤이 다른 페이지에 다시 게시 될 때 해당 페이지에 렌더링 하는 새로운 WebForm\_DoPostBackWithOptions 클라이언트 쪽 함수를 통해 구현 됩니다. 이 JavaScript 함수는 클라이언트에 스크립트를 내보내는 새 Webresource.axd 처리기에서 제공 됩니다.

다음 비디오는 페이지 간 포스트백의 연습입니다.

![](the-asp-net-2-0-page-model/_static/image2.png)

[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>페이지 간 다시 게시에 대 한 자세한 내용

### <a name="viewstate"></a>뷰

페이지 간 다시 게시 시나리오에서 첫 페이지의 viewstate에 발생 하는 상황을 이미 확인 했을 수 있습니다. IPostBackDataHandler를 구현 하지 않는 모든 컨트롤은 viewstate를 통해 상태를 유지 하므로 페이지 간 다시 게시의 두 번째 페이지에서 해당 컨트롤의 속성에 액세스할 수 있도록 페이지의 viewstate에 대 한 액세스 권한이 있어야 합니다. ASP.NET 2.0는 \_\_PREVIOUSPAGE 이라는 두 번째 페이지에서 새 숨겨진 필드를 사용 하 여이 시나리오를 처리 합니다. \_\_PREVIOUSPAGE 양식 필드는 첫 번째 페이지의 viewstate를 포함 하 여 두 번째 페이지에 있는 모든 컨트롤의 속성에 액세스할 수 있도록 합니다.

### <a name="circumventing-findcontrol"></a>우회 FindControl

페이지 간 포스트백의 비디오 연습에서는 FindControl 메서드를 사용 하 여 첫 번째 페이지의 TextBox 컨트롤에 대 한 참조를 가져옵니다. 해당 메서드는 이러한 용도로도 잘 작동 하지만 FindControl는 비용이 많이 들고 추가 코드를 작성 해야 합니다. 다행히 ASP.NET 2.0은이 목적을 위해 여러 시나리오에서 작동 하는 FindControl에 대 한 대안을 제공 합니다. PreviousPageType 지시문을 사용 하면 TypeName 또는 VirtualPath 특성을 사용 하 여 이전 페이지에 대 한 강력한 형식의 참조를 사용할 수 있습니다. TypeName 특성을 사용 하면 이전 페이지의 형식을 지정할 수 있는 반면 VirtualPath 특성을 사용 하면 가상 경로를 사용 하 여 이전 페이지를 참조할 수 있습니다. PreviousPageType 지시문을 설정한 후에는 공용 속성을 사용 하 여 액세스를 허용 하려는 컨트롤 등을 노출 해야 합니다.

## <a name="lab-1-cross-page-postback"></a>랩 1 페이지 간 다시 게시

이 랩에서는 ASP.NET 2.0의 새로운 페이지 간 다시 게시 기능을 사용 하는 응용 프로그램을 만듭니다.

1. Visual Studio 2005를 열고 새 ASP.NET 웹 사이트를 만듭니다.
2. Webform 라는 새 새를 추가 합니다.
3. 디자인 뷰에서 default.aspx를 열고 단추 컨트롤과 TextBox 컨트롤을 추가 합니다. 

    1. 단추 컨트롤에 **Submitbutton 단추** 를 지정 하 고 TextBox 컨트롤에서 **UserName**id를 지정 합니다.
    2. 단추의 PostBackUrl 속성을로 설정 합니다.
4. 소스 뷰에서 default.aspx를 엽니다.
5. 아래와 같이 @ PreviousPageType 지시어를 추가 합니다.
6. 페이지\_페이지에 다음 코드를 추가 합니다. 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. 빌드 메뉴에서 빌드를 클릭 하 여 프로젝트를 빌드합니다.
8. Default.aspx의 코드 숨김으로 다음 코드를 추가 합니다. 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. 페이지를 .aspx에서 로드\_페이지를 다음으로 변경 합니다. 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. 프로젝트를 빌드합니다.
11. 프로젝트를 실행합니다.
12. 텍스트 상자에 사용자 이름을 입력 하 고 단추를 클릭 합니다.
13. 결과는 무엇 인가요?

## <a name="asynchronous-pages-in-aspnet-20"></a>ASP.NET 2.0의 비동기 페이지

ASP.NET의 많은 경합 문제는 외부 호출 (예: 웹 서비스 또는 데이터베이스 호출)의 대기 시간, 파일 IO 대기 시간 등으로 인해 발생 합니다. ASP.NET 응용 프로그램에 대해 요청을 수행 하는 경우 ASP.NET는 해당 작업자 스레드 중 하나를 사용 하 여 해당 요청을 처리 합니다. 요청이 완료 되 고 응답이 전송 될 때까지 해당 요청은 해당 스레드를 소유 합니다. ASP.NET 2.0는 페이지를 비동기적으로 실행 하는 기능을 추가 하 여 이러한 유형의 문제에 대 한 대기 시간 문제를 해결 합니다. 즉, 작업자 스레드가 요청을 시작한 다음 다른 스레드에 추가 실행을 전달 하 여 사용 가능한 스레드 풀로 신속 하 게 반환할 수 있습니다. 파일 IO, 데이터베이스 호출 등이 완료 되 면 요청을 완료 하기 위해 스레드 풀에서 새 스레드를 가져옵니다.

페이지를 비동기적으로 실행 하는 첫 번째 단계는 다음과 같이 페이지 지시문의 **Async** 특성을 설정 하는 것입니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

이 특성은 ASP.NET에 게 페이지에 대 한 IHttpAsyncHandler을 구현 하도록 지시 합니다.

다음 단계는 미리 렌더링 전의 페이지 수명 주기에 있는 지점에서 AddOnPreRenderCompleteAsync 메서드를 호출 하는 것입니다. 이 메서드는 일반적으로 페이지\_로드에서 호출 됩니다. AddOnPreRenderCompleteAsync 메서드는 두 개의 매개 변수를 사용 합니다. BeginEventHandler 및 EndEventHandler BeginEventHandler는 EndEventHandler에 매개 변수로 전달 되는 IAsyncResult를 반환 합니다.

아래 비디오는 비동기 페이지 요청을 연습 하는 것입니다.

![](the-asp-net-2-0-page-model/_static/image3.png)

[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> 비동기 페이지는 EndEventHandler가 완료 될 때까지 브라우저로 렌더링 되지 않습니다. 하지만 일부 개발자는 비동기 요청을 비동기 콜백과 유사한 것으로 생각 합니다. 이는 그렇지 않습니다. 비동기 요청의 혜택은 새 요청을 처리 하기 위해 첫 번째 작업자 스레드를 스레드 풀로 반환 하 여 IO 바인딩된 것으로 인해 경합이 감소 하는 것입니다.

## <a name="script-callbacks-in-aspnet-20"></a>ASP.NET 2.0의 스크립트 콜백

웹 개발자는 항상 콜백과 관련 된 깜박임을 방지 하는 방법을 살펴보았습니다. ASP.NET 1.x에서 SmartNavigation은 깜박임을 방지 하는 가장 일반적인 방법 이지만 SmartNavigation은 클라이언트에서 구현 하는 복잡성으로 인해 일부 개발자에 게 문제가 발생 했습니다. ASP.NET 2.0는 스크립트 콜백에서이 문제를 해결 합니다. 스크립트 콜백은 XMLHttp를 활용 하 여 JavaScript를 통해 웹 서버에 대 한 요청을 수행 합니다. XMLHttp 요청은 브라우저의 DOM을 통해 조작할 수 있는 XML 데이터를 반환 합니다. 새 Webresource.axd 처리기가 사용자에 게 XMLHttp 코드를 숨깁니다.

ASP.NET 2.0에서 스크립트 콜백을 구성 하기 위해 필요한 몇 가지 단계가 있습니다.

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>1 단계: ICallbackEventHandler 인터페이스 구현

ASP.NET가 스크립트 콜백에 참여 하는 것으로 페이지를 인식할 수 있도록 하려면 ICallbackEventHandler 인터페이스를 구현 해야 합니다. 다음과 같이 코드를 만든 파일에서이 작업을 수행할 수 있습니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

다음과 같이 @ Implements 지시문을 사용 하 여이 작업을 수행할 수도 있습니다.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

일반적으로 인라인 ASP.NET 코드를 사용할 때 @ Implements 지시문을 사용 합니다.

## <a name="step-2--call-getcallbackeventreference"></a>2 단계: GetCallbackEventReference 호출

앞에서 설명한 것 처럼 XMLHttp 호출은 Webresource.axd 처리기에 캡슐화 됩니다. 페이지가 렌더링 되 면 ASP.NET는 Webresource.axd에서 제공 하는 클라이언트 스크립트인 WebForm\_DoCallback에 대 한 호출을 추가 합니다. WebForm\_DoCallback 함수는 콜백에 대 한 \_\_doPostBack 함수를 대체 합니다. \_\_doPostBack은 페이지에 폼을 프로그래밍 방식으로 전송 합니다. 콜백 시나리오에서는 포스트백을 방지 하는 것이 좋습니다. 따라서 \_\_doPostBack이 충분 하지 않습니다.

> [!NOTE]
> \_\_doPostBack은 클라이언트 스크립트 콜백 시나리오에서 페이지에 계속 렌더링 됩니다. 그러나 콜백에는 사용 되지 않습니다.

WebForm\_DoCallback에 대 한 인수는 서버측 함수 GetCallbackEventReference를 통해 제공 됩니다 .이 함수는 일반적으로 페이지\_로드에서 호출 됩니다. GetCallbackEventReference에 대 한 일반적인 호출은 다음과 같습니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> 이 경우 cm은 ClientScriptManager의 인스턴스입니다. ClientScriptManager 클래스는이 모듈의 뒷부분에서 설명 합니다.

GetCallbackEventReference에는 여러 개의 오버 로드 된 버전이 있습니다. 이 경우 인수는 다음과 같습니다.

`this`

GetCallbackEventReference가 호출 되는 컨트롤에 대 한 참조입니다. 이 경우 페이지 자체입니다.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

클라이언트 쪽 코드에서 서버측 이벤트로 전달 되는 문자열 인수입니다. 이 경우에는 ddlCompany 라는 드롭다운 값을 전달 하는 Im입니다.

`ShowCompanyName`

서버 쪽 콜백 이벤트에서 반환 값 (문자열로)을 수락할 클라이언트 쪽 함수의 이름입니다. 이 함수는 서버 쪽 콜백이 성공한 경우에만 호출 됩니다. 따라서 견고성을 위해 일반적으로 오류가 발생 한 경우 실행할 클라이언트 쪽 함수의 이름을 지정 하는 추가 문자열 인수를 사용 하는 GetCallbackEventReference의 오버 로드 된 버전을 사용 하는 것이 좋습니다.

`null`

서버에 대 한 콜백 전에 시작 된 클라이언트 쪽 함수를 나타내는 문자열입니다. 이 경우에는 이러한 스크립트가 없으므로 인수가 null입니다.

`true`

콜백을 비동기적으로 수행할지 여부를 지정 하는 부울입니다.

클라이언트에서 WebForm\_DoCallback에 대 한 호출은 이러한 인수를 전달 합니다. 따라서이 페이지가 클라이언트에서 렌더링 되 면 해당 코드는 다음과 같이 표시 됩니다.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

클라이언트에서 함수 시그니처는 약간 다릅니다. 클라이언트 쪽 함수는 5 개의 문자열과 부울을 전달 합니다. 추가 문자열 (위 예제의 경우 null)에는 서버 쪽 콜백에서 발생 한 모든 오류를 처리 하는 클라이언트 쪽 함수가 포함 되어 있습니다.

## <a name="step-3--hook-the-client-side-control-event"></a>3 단계: 클라이언트 쪽 컨트롤 이벤트 후크

위의 GetCallbackEventReference 반환 값이 문자열 변수에 할당 된 것을 알 수 있습니다. 해당 문자열은 콜백을 시작 하는 컨트롤에 대 한 클라이언트 쪽 이벤트를 연결 하는 데 사용 됩니다. 이 예제에서 콜백은 페이지의 드롭다운에서 시작 되므로 *OnChange* 이벤트를 후크 하려고 합니다.

클라이언트 쪽 이벤트를 후크 하려면 다음과 같이 클라이언트 쪽 태그에 처리기를 추가 하기만 하면 됩니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

*CbRef* 는 GetCallbackEventReference에 대 한 호출의 반환 값입니다. 위에 표시 된 WebForm\_DoCallback에 대 한 호출을 포함 합니다.

## <a name="step-4--register-the-client-side-script"></a>4 단계: 클라이언트 쪽 스크립트 등록

GetCallbackEventReference에 대 한 호출은 서버 쪽 콜백이 성공할 때 **Showcompanyname** 이라는 클라이언트 쪽 스크립트가 실행 되도록 지정 했습니다. ClientScriptManager 인스턴스를 사용 하 여 페이지에 해당 스크립트를 추가 해야 합니다. ClientScriptManager 클래스는이 모듈의 뒷부분에서 설명 합니다. 이렇게 하려면 다음과 같이 합니다.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>5 단계: ICallbackEventHandler 인터페이스의 메서드 호출

ICallbackEventHandler에는 코드에서 구현 해야 하는 두 개의 메서드가 포함 되어 있습니다. **RaiseCallbackEvent** 및 **GetCallbackEvent**입니다.

**RaiseCallbackEvent** 는 문자열을 인수로 사용 하 고 아무 것도 반환 하지 않습니다. WebForm\_DoCallback에 대 한 클라이언트 쪽 호출에서 문자열 인수가 전달 됩니다. 이 경우 해당 값은 ddlCompany 라는 드롭다운에서 *value* 특성입니다. 서버 쪽 코드는 RaiseCallbackEvent 메서드에 배치 되어야 합니다. 예를 들어 콜백에서 외부 리소스에 대해 WebRequest를 만드는 경우 해당 코드를 RaiseCallbackEvent에 배치 해야 합니다.

**GetCallbackEvent** 는 클라이언트에 대 한 콜백 반환을 처리 해야 합니다. 인수를 사용 하지 않고 문자열을 반환 합니다. 반환 되는 문자열은 클라이언트 쪽 함수 (이 경우 *Showcompanyname*)에 인수로 전달 됩니다.

위의 단계를 완료 하면 ASP.NET 2.0에서 스크립트 콜백을 수행할 준비가 된 것입니다.

![](the-asp-net-2-0-page-model/_static/image4.png)

[전체 화면 비디오 열기](the-asp-net-2-0-page-model/_static/callback1.wmv)

ASP.NET의 스크립트 콜백은 XMLHttp 호출을 지 원하는 모든 브라우저에서 지원 됩니다. 현재 사용 중인 모든 최신 브라우저를 포함 합니다. Internet Explorer는 XMLHttp ActiveX 개체를 사용 하는 반면, 다른 최신 브라우저 (예정 된 IE 7 포함)는 내장 XMLHttp 개체를 사용 합니다. 브라우저에서 콜백을 지원 하는지 프로그래밍 방식으로 확인 하려면. **.Browser 콜백** 속성을 사용 하면 됩니다. 요청 하는 클라이언트가 스크립트 콜백을 지 원하는 경우이 속성은 **true** 를 반환 합니다.

## <a name="working-with-client-script-in-aspnet-20"></a>ASP.NET 2.0에서 클라이언트 스크립트 작업

ASP.NET 2.0의 클라이언트 스크립트는 ClientScriptManager 클래스를 사용 하 여 관리 됩니다. ClientScriptManager 클래스는 형식 및 이름을 사용 하 여 클라이언트 스크립트를 추적 합니다. 이렇게 하면 동일한 스크립트가 페이지에 두 번 이상 삽입 되지 않습니다.

> [!NOTE]
> 페이지에 스크립트가 성공적으로 등록 된 후에는 동일한 스크립트를 등록 하려고 하면 스크립트가 두 번 등록 되지 않습니다. 중복 스크립트가 추가 되지 않고 예외가 발생 하지 않습니다. 불필요 한 계산을 방지 하기 위해 두 번 이상 등록 하지 않도록 스크립트를 이미 등록 했는지 여부를 확인 하는 데 사용할 수 있는 메서드가 있습니다.

ClientScriptManager의 메서드는 모든 현재 ASP.NET 개발자에 게 친숙 해야 합니다.

## <a name="registerclientscriptblock"></a>RegisterClientScriptBlock

이 메서드는 렌더링 된 페이지의 맨 위에 스크립트를 추가 합니다. 이는 클라이언트에서 명시적으로 호출 되는 함수를 추가 하는 데 유용 합니다.

이 메서드의 오버 로드 된 두 가지 버전이 있습니다. 네 가지 인수 중 세 개는 공통 된 인수입니다. 아래에 이 계정과 키의 예제가 나와 있습니다.

`type (string)`

***형식*** 인수는 스크립트의 형식을 식별 합니다. 일반적으로 페이지의 형식 (이 경우)을 사용 하는 것이 좋습니다. 형식에 대 한 GetType ()).

`key (string)`

***키*** 인수는 스크립트의 사용자 정의 키입니다. 이는 각 스크립트에 대해 고유 해야 합니다. 이미 추가 된 스크립트와 동일한 키와 유형을 사용 하 여 스크립트를 추가 하려고 하면 해당 스크립트는 추가 되지 않습니다.

`script (string)`

***스크립트*** 인수는 추가할 실제 스크립트를 포함 하는 문자열입니다. StringBuilder를 사용 하 여 스크립트를 만든 다음 StringBuilder에서 ToString () 메서드를 사용 하 여 ***스크립트*** 인수를 할당 하는 것이 좋습니다.

3 개의 인수만 사용 하는 오버 로드 된 RegisterClientScriptBlock를 사용 하는 경우 스크립트에 스크립트 요소 (&lt;스크립트&gt; 및 &lt;/스크립트&gt;)를 포함 해야 합니다.

네 번째 인수를 사용 하는 RegisterClientScriptBlock의 오버 로드를 사용 하도록 선택할 수 있습니다. 네 번째 인수는 ASP.NET가 스크립트 요소를 추가 해야 하는지 여부를 지정 하는 부울입니다. 이 인수가 **true**이면 스크립트에 스크립트 요소를 명시적으로 포함 하면 안 됩니다.

IsClientScriptBlockRegistered 된 메서드를 사용 하 여 스크립트가 이미 등록 되었는지 확인 합니다. 이렇게 하면 이미 등록 된 스크립트를 다시 등록 하지 않아도 됩니다.

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude (2.0의 새로운 새)

RegisterClientScriptInclude 태그는 외부 스크립트 파일에 연결 되는 스크립트 블록을 만듭니다. 두 개의 오버 로드가 있습니다. 하나는 키와 URL을 사용 합니다. 두 번째는 형식을 지정 하는 세 번째 인수를 추가 합니다.

예를 들어 다음 코드는 응용 프로그램의 scripts 폴더 루트에 있는 jsfunctions에 연결 되는 스크립트 블록을 생성 합니다.

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

이 코드는 렌더링 된 페이지에 다음 코드를 생성 합니다.

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> 스크립트 블록은 페이지 아래쪽에 렌더링 됩니다.

IsClientScriptIncludeRegistered 메서드를 사용 하 여 스크립트가 이미 등록 되었는지 여부를 확인 합니다. 이렇게 하면 스크립트를 다시 등록 하지 않아도 됩니다.

## <a name="registerstartupscript"></a>RegisterStartupScript

RegisterStartupScript 메서드는 RegisterClientScriptBlock 메서드와 동일한 인수를 사용 합니다. RegisterStartupScript에 등록 된 스크립트는 페이지가 로드 된 후 OnLoad 클라이언트 쪽 이벤트 이전에 실행 됩니다. 1\.x에서 RegisterStartupScript로 등록 된 스크립트는 닫는 &lt;양식&gt; 태그 바로 앞에 배치 되었으며, RegisterClientScriptBlock에 등록 된 스크립트는 열기 &lt;양식&gt; 태그 바로 뒤에 배치 되었습니다. ASP.NET 2.0에서 두 가지 모두 닫는 &lt;양식&gt; 태그 바로 앞에 배치 됩니다.

> [!NOTE]
> RegisterStartupScript를 사용 하 여 함수를 등록 하는 경우 해당 함수는 클라이언트 쪽 코드에서 명시적으로 호출할 때까지 실행 되지 않습니다.

IsStartupScriptRegistered 메서드를 사용 하 여 스크립트가 이미 등록 되어 있는지 확인 하 고 스크립트를 다시 등록 하려고 시도 하지 않습니다.

## <a name="other-clientscriptmanager-methods"></a>기타 ClientScriptManager 메서드

ClientScriptManager 클래스의 다른 유용한 메서드는 다음과 같습니다.

|  <strong>GetCallbackEventReference</strong>   |                                                 이 모듈의 앞부분에서 콜백 스크립트를 참조 하세요.                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                클라이언트 쪽 이벤트에서 포스트백 하는 데 사용할 수 있는 JavaScript 참조 (javascript:&lt;호출&gt;)를 가져옵니다.                 |
|  <strong>System.web.ui.clientscriptmanager.getpostbackeventreference</strong>   |                                   클라이언트에서 다시 게시를 시작 하는 데 사용할 수 있는 문자열을 가져옵니다.                                    |
|      <strong>GetWebResourceUrl</strong>       | 어셈블리에 포함 된 리소스에 대 한 URL을 반환 합니다. <strong>RegisterClientScriptResource</strong>와 함께 사용 해야 합니다. |
| <strong>RegisterClientScriptResource</strong> |     페이지에 웹 리소스를 등록 합니다. 이러한 리소스는 어셈블리에 포함 되 고 새 Webresource.axd 처리기에서 처리 됩니다.      |
|     <strong>RegisterHiddenField</strong>      |                                                 페이지에 숨겨진 폼 필드를 등록 합니다.                                                 |
|  <strong>RegisterOnSubmitStatement</strong>   |                                  HTML 폼이 제출 될 때 실행 되는 클라이언트 쪽 코드를 등록 합니다.                                   |
