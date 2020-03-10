---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-4 부 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup을 사용 하 여 작업 하는 방법에 대 한 기본 사항을 학습 합니다. ASP.NET m ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 583e782641efea9a9517edb31f7718b28203d756
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433253"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-4 부

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 ASP.NET MVC 웹 응용 프로그램에서 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup 일정을 사용 하는 방법에 대 한 기본 사항을 설명 합니다.

### <a name="adding-a-template-for-editing-dates"></a>날짜 편집을 위한 템플릿 추가

이 섹션에서는 ASP.NET MVC가 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성의 **날짜** 열거형으로 표시 된 모델 속성을 편집 하기 위한 UI를 표시할 때 적용 되는 날짜를 편집 하기 위한 템플릿을 만듭니다. 템플릿은 날짜만 렌더링 합니다. 시간이 표시 되지 않습니다. 템플릿에서는 [JQUERY UI Datepicker](http://jqueryui.com/demos/datepicker/) popup 일정을 사용 하 여 날짜를 편집 하는 방법을 제공 합니다.

시작 하려면 *Movie.cs* 파일을 열고 다음 코드와 같이 **날짜** 열거형을 사용 하 여 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) 특성을 `ReleaseDate` 속성에 추가 합니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

이 코드를 사용 하면 표시 템플릿 및 편집 템플릿 모두에 시간 없이 `ReleaseDate` 필드가 표시 됩니다. 응용 프로그램의 *Views\Shared\EditorTemplates* 폴더 또는 *Views\Movies\EditorTemplates* 폴더에 *date. cshtml* 템플릿이 포함 된 경우 편집 하는 동안 `DateTime` 속성을 렌더링 하는 데 해당 템플릿이 사용 됩니다. 그렇지 않으면 기본 제공 ASP.NET 템플릿 시스템은 속성을 날짜로 표시 합니다.

Ctrl+F5를 눌러 애플리케이션을 실행합니다. 편집 링크를 선택 하 여 릴리스 날짜의 입력 필드가 날짜만 표시 되는지 확인 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

**솔루션 탐색기**에서 *Views* 폴더를 확장 하 고 *공유* 폴더를 확장 한 다음 *Views\Shared\EditorTemplates* 폴더를 마우스 오른쪽 단추로 클릭 합니다.

**추가**를 클릭 한 다음 **보기**를 클릭 합니다. **보기 추가** 대화 상자가 표시 됩니다.

**보기 이름** 상자에 &quot;Date&quot;를 입력 합니다.

**부분 뷰로 만들기** 확인란을 선택 합니다. **레이아웃 또는 마스터 페이지를 사용** 하 고 **강력한 형식의 뷰 만들기** 확인란을 선택 하지 않았는지 확인 합니다.

**추가**를 클릭합니다. *Views\Shared\EditorTemplates\Date.cshtml* 템플릿이 만들어집니다.

*Views\Shared\EditorTemplates\Date.cshtml* 템플릿에 다음 코드를 추가 합니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

첫 번째 줄은 모델을 `DateTime` 형식으로 선언 합니다. 편집 및 표시 템플릿에서 모델 유형을 선언할 필요가 없지만 뷰에 전달 되는 모델에 대 한 컴파일 시간 검사를 수행 하는 것이 가장 좋습니다. 또 다른 혜택은 Visual Studio의 뷰에서 모델에 대 한 IntelliSense를 가져오는 것입니다. 모델 형식이 선언 되지 않은 경우 ASP.NET MVC는이를 [동적](https://msdn.microsoft.com/library/dd264741.aspx) 형식으로 간주 하 고 컴파일 시간 형식 검사를 수행 하지 않습니다. 모델을 `DateTime` 형식으로 선언 하면 강력한 형식이 됩니다.

두 번째 줄은 날짜 필드 앞&quot; 날짜 템플릿을 사용 하 여 &quot;를 표시 하는 리터럴 HTML 태그입니다. 이 줄을 일시적으로 사용 하 여이 날짜 템플릿이 사용 되 고 있는지 확인 합니다.

다음 줄은 텍스트 상자에 `input` 필드를 렌더링 하는 [Html. TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) 도우미입니다. 도우미의 세 번째 매개 변수는 무명 형식을 사용 하 여 텍스트 상자에 대 한 클래스를 `datefield` 하 고 `date`형식을 설정 합니다. `class`은에 C#예약 되어 있으므로 `@` 문자를 사용 하 여 C# 파서의 `class` 특성을 이스케이프 해야 합니다.

`date` 형식은 html5에서 인식할 수 있는 브라우저에서 HTML5 달력 컨트롤을 렌더링 하는 데 사용할 수 있는 HTML5 입력 형식입니다. 나중에 `datefield` 클래스를 사용 하 여 jQuery datepicker을 `Html.TextBox` 요소에 연결 하는 몇 가지 JavaScript를 추가 합니다.

Ctrl+F5를 눌러 애플리케이션을 실행합니다. 이 이미지에 표시 된 것 처럼 템플릿이 날짜 템플릿을 사용 하 여 `ReleaseDate` 텍스트 입력란 바로 앞에&quot; &quot;를 표시 하기 때문에 편집 뷰의 `ReleaseDate` 속성이 편집 템플릿을 사용 하는지 확인할 수 있습니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

브라우저에서 페이지의 소스를 봅니다. 예를 들어 페이지를 마우스 오른쪽 단추로 클릭 하 고 **소스 보기**를 선택 합니다. 다음 예제에서는 렌더링 된 HTML의 `class` 및 `type` 특성을 보여 주는 페이지의 일부 태그를 보여 줍니다.

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

*Views\Shared\EditorTemplates\Date.cshtml* 템플릿으로 돌아가서 날짜 템플릿&quot; 태그를 사용 하 여 &quot;를 제거 합니다. 이제 완성 된 템플릿은 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>NuGet을 사용 하 여 jQuery UI Datepicker Popup 일정 추가

이 섹션에서는 [datepicker 템플릿에 JQUERY UI](http://jqueryui.com/demos/datepicker/) popup을 추가 합니다. [JQUERY UI](http://jqueryui.com/) 라이브러리는 애니메이션, 고급 효과 및 사용자 지정 가능한 위젯을 지원 합니다. JQuery JavaScript 라이브러리를 기반으로 빌드됩니다. Datepicker popup 달력을 사용 하면 문자열을 입력 하는 대신 달력을 사용 하 여 날짜를 쉽고 자연스럽 게 입력할 수 있습니다. 팝업 일정은 사용자를 법적 날짜로 제한 하기도 합니다. 날짜에 대 한 일반 텍스트 항목은 `2/33/1999` (2 월 3 일, 1999)와 같은 항목을 입력할 수 있지만 [JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/) popup은이를 허용 하지 않습니다.

먼저 jQuery UI 라이브러리를 설치 해야 합니다. 이렇게 하려면 SP1 버전의 Visual Studio 2010 및 Visual Web Developer에 포함 된 패키지 관리자 인 NuGet을 사용 합니다.

Visual Web Developer의 **도구** 메뉴에서 **nuget 패키지 관리자** 를 선택한 다음 **nuget 패키지 관리**를 선택 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

참고: **도구** 메뉴에 **nuget 패키지 관리자** 명령이 표시 되지 않는 경우 NuGet 웹 사이트의 [nuget 설치](http://docs.nuget.org/docs/start-here/installing-nuget) 페이지에 있는 지침에 따라 nuget을 설치 해야 합니다.   
  
Visual Web Developer 대신 Visual Studio를 사용 하는 경우 **도구** 메뉴에서 **NuGet 패키지 관리자** 를 선택한 다음 **라이브러리 패키지 참조 추가**를 선택 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

**Mvcmovie-NuGet 패키지 관리** 대화 상자에서 왼쪽의 **온라인** 탭을 클릭 한 다음 검색 상자에 &quot;&quot;을 입력 합니다. J **쿼리 UI 위젯: Datepicker**을 선택 하 고 **설치** 단추를 선택 합니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet은 jQuery UI Core 및 jQuery ui 날짜 선택기의 이러한 디버그 버전과 해당 버전을 프로젝트에 추가 합니다.

- *jquery.*
- *jquery. 핵심.*
- *datepicker.*
- *jquery. datepicker.*

참고: 디버그 버전 (확장명이. m. m *. m. m. m. m. m. m. m. m. m. m. m. m. m. m. m.* 확장명 없음)은 디버깅에 유용

JQuery 날짜 선택기를 실제로 사용 하려면 달력 위젯을 편집 템플릿에 연결 하는 jQuery 스크립트를 만들어야 합니다. **솔루션 탐색기**에서 *Scripts* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 항목**, **JScript 파일**을 차례로 선택 합니다. *Datepickerready*파일의 이름을로 합니다.

*Datepickerready .js* 파일에 다음 코드를 추가 합니다.

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

JQuery에 익숙하지 않은 경우이 작업에 대 한 간략 한 설명은 다음과 같습니다. 첫 번째 줄은 페이지의 모든 DOM 요소가 로드 될 때 호출 되는 &quot;jQuery ready&quot; 함수입니다. 두 번째 줄은 `datefield`클래스 이름이 있는 모든 DOM 요소를 선택 하 고 각 요소에 대해 `datepicker` 함수를 호출 합니다. (이 자습서의 앞부분에서 *Views\Shared\EditorTemplates\Date.cshtml* 템플릿에 `datefield` 클래스를 추가 했습니다.)

다음으로 *Views\Shared\\_Layout* 파일을 엽니다. 날짜 선택기를 사용 하려면 다음 파일에 대 한 참조를 추가 해야 합니다.

- *Content/themes/base/jquery. core .css*
- *Content/themes/base/jquery. datepicker*
- *Content/themes/base/jquery. theme. .css*
- *jquery. 핵심.*
- *jquery. datepicker.*
- *DatePickerReady .js*

다음 예제에서는 *Views\Shared\\_Layout. cshtml* 파일의 `head` 요소 아래에 추가 해야 하는 실제 코드를 보여 줍니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

전체 `head` 섹션은 다음과 같습니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

[URL 콘텐츠 도우미](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) 메서드는 리소스 경로를 절대 경로로 변환 합니다. 응용 프로그램이 IIS에서 실행 되는 경우 `@URL.Content`를 사용 하 여 이러한 리소스를 올바르게 참조 해야 합니다.

Ctrl+F5를 눌러 애플리케이션을 실행합니다. 편집 링크를 선택한 다음, 삽입 지점을 **Releasedate** 필드에 놓습니다. JQuery UI 팝업 일정이 표시 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

대부분의 jQuery 컨트롤과 마찬가지로 datepicker를 사용 하 여 광범위 하 게 사용자 지정할 수 있습니다. 자세한 내용은 Visual 사용자 지정: [JQUERY ui](http://learn.jquery.com/jquery-ui/getting-started/) 사이트에서 [Jquery ui 테마 디자인](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) 을 참조 하세요.

### <a name="supporting-the-html5-date-input-control"></a>HTML5 날짜 입력 컨트롤 지원

더 많은 브라우저에서 HTML5를 지원할 때 `date` input 요소와 같은 네이티브 HTML5 입력을 사용 하 고 jQuery UI 달력을 사용 하지 않을 수 있습니다. 응용 프로그램에 논리를 추가 하 여 브라우저에서 지원 되는 경우 자동으로 HTML5 컨트롤을 사용할 수 있습니다. 이렇게 하려면 *Datepickerready .js* 파일의 내용을 다음으로 바꿉니다.

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

이 스크립트의 첫 번째 줄에서는 Modernizr를 사용 하 여 HTML5 날짜 입력이 지원 되는지 확인 합니다. 지원 되지 않는 경우에는 jQuery UI 날짜 선택이 대신 후크 됩니다. ([Modernizr](http://www.modernizr.com/docs/) 는 HTML5 및 CSS3의 네이티브 구현에 대 한 가용성을 검색 하는 오픈 소스 JavaScript 라이브러리입니다. Modernizr은 사용자가 만드는 모든 새 ASP.NET MVC 프로젝트에 포함 됩니다.

이러한 변경을 수행한 후에는 HTML5를 지 원하는 브라우저 (예: Opera 11)를 사용 하 여 테스트할 수 있습니다. HTML5 호환 브라우저를 사용 하 여 응용 프로그램을 실행 하 고 동영상 항목을 편집 합니다. HTML5 날짜 컨트롤은 jQuery UI 팝업 달력 대신 사용 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

새 버전의 브라우저에서는 HTML5를 증분 방식으로 구현 하므로, 이제 다양 한 HTML5 지원을 수용 하는 코드를 웹 사이트에 추가 하는 것이 좋습니다. 예를 들어, 사이트에서 HTML5 날짜 컨트롤을 부분적 으로만 지원 하는 브라우저를 지원할 수 있는 보다 강력한 *Datepickerready .js* 스크립트가 아래에 나와 있습니다.

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

이 스크립트는 HTML5 날짜 컨트롤을 완벽 하 게 지원 하지 않는 `date` 형식의 HTML5 `input` 요소를 선택 합니다. 이러한 요소에 대해 jQuery UI popup 일정을 연결한 다음 `type` 특성을 `date`에서 `text`으로 변경 합니다. `type` 특성을 `date`에서 `text`으로 변경 하면 부분 HTML5 날짜 지원이 제거 됩니다. 훨씬 더 강력한 *Datepickerready .js* 스크립트는 [JSFIDDLE](http://jsfiddle.net/XSTK8/15/)에서 찾을 수 있습니다.

### <a name="adding-nullable-dates-to-the-templates"></a>템플릿에 Nullable 날짜 추가

기존 날짜 템플릿 중 하나를 사용 하 고 null 날짜를 전달 하면 런타임 오류가 발생 합니다. 날짜 템플릿을 더 강력 하 게 만들려면 null 값을 처리 하도록 변경 합니다. Nullable 날짜를 지원 하려면 *Views\Shared\DisplayTemplates\DateTime.cshtml* 의 코드를 다음과 같이 변경 합니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

모델이 **null**이면 코드에서 빈 문자열을 반환 합니다.

*Views\Shared\EditorTemplates\Date.cshtml* 파일의 코드를 다음과 같이 변경 합니다.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

이 코드가 실행 될 때 모델이 null이 아니면 모델의 `DateTime` 값이 사용 됩니다. 모델이 null 인 경우에는 현재 날짜가 대신 사용 됩니다.

### <a name="wrapup"></a>Wrapup

이 자습서에서는 ASP.NET 템플릿 도우미의 기본 사항에 대해 설명 하 고 ASP.NET MVC 응용 프로그램에서 jQuery UI datepicker popup을 사용 하는 방법을 보여 줍니다. 자세한 내용은 다음 리소스를 사용해 보세요.

- 지역화에 대 한 자세한 내용은 Rajeesh의 블로그 [Jqueryui Datepicker in ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/)를 참조 하세요.
- JQuery UI에 대 한 자세한 내용은 [JQUERY ui](http://docs.jquery.com/UI)를 참조 하세요.
- Datepicker 컨트롤을 지역화 하는 방법에 대 한 자세한 내용은 [UI/datepicker/지역화](http://docs.jquery.com/UI/Datepicker/Localization)를 참조 하세요.
- ASP.NET MVC 템플릿에 대 한 자세한 내용은 [ASP.NET mvc 2 템플릿에서](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html)Brad Wilson의 블로그 시리즈를 참조 하세요. ASP.NET MVC 2 용으로 작성 된 시리즈는 아직 ASP.NET MVC의 현재 버전에 적용 됩니다.

> [!div class="step-by-step"]
> [이전](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
