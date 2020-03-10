---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: ASP.NET MVC와 함께 DropDownList 도우미 사용 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 6375bb2be158cea18309ffa71c71ac3e67bc91ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433079"
---
# <a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>ASP.NET MVC와 함께 DropDownList 도우미 사용

[Rick Anderson](https://twitter.com/RickAndMSFT)

이 자습서에서는 ASP.NET MVC 웹 응용 프로그램에서 [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 도우미와 [ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) 도우미를 사용 하는 기본 사항을 설명 합니다. Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 자습서를 수행할 수 있습니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.

- [Visual Studio Web Developer EXPRESS SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)<a id="post"></a>
- [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)

Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다. 이 자습서에서는 [ASP.NET mvc](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서 또는[ASP.NET mvc Music Store](../mvc-music-store/mvc-music-store-part-1.md) 자습서를 완료 했다고 가정 하거나 ASP.NET mvc 개발에 대해 잘 알고 있는 것으로 가정 합니다. 이 자습서는 [ASP.NET MVC Music Store](../mvc-music-store/mvc-music-store-part-1.md) 자습서에서 수정 된 프로젝트로 시작 합니다. 다음 링크를 통해 스타터 프로젝트를 다운로드 하 여 [버전을 C# 다운로드할](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)수 있습니다.

완료 된 자습서 C# 소스 코드가 포함 된 Visual Web Developer 프로젝트를이 항목에 사용할 수 있습니다. [다운로드](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d).

### <a name="what-youll-build"></a>만들 내용

[DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) 도우미를 사용 하 여 범주를 선택 하는 작업 메서드와 뷰를 만듭니다. 또한 **jQuery** 를 사용 하 여 장르 또는 음악가와 같은 새 범주를 필요로 하는 경우 사용할 수 있는 범주 삽입 대화 상자를 추가 합니다. 다음은 새 장르를 추가 하 고 새 음악가를 추가 하기 위한 링크를 보여 주는 만들기 뷰의 스크린샷입니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>학습할 기술

다음 내용을 학습하게 됩니다.

- [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) 도우미를 사용 하 여 범주 데이터를 선택 하는 방법입니다.
- **JQuery** 대화 상자를 추가 하 여 새 범주를 추가 하는 방법입니다.

### <a name="getting-started"></a>시작하기

[다운로드](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829)링크를 사용 하 여 시작 프로젝트를 다운로드 하 여 시작 합니다. Windows 탐색기에서 *DDL\_스타터 .zip* 파일을 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다. **DDL\_스타터. Zip 속성** 대화 상자에서 차단 해제를 선택 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

DDL\_스타터 .zip 파일을 마우스 오른쪽 단추로 클릭 하 고 **압축** 풀기를 선택 하 여 파일의 압축을 풉니다. Visual Web Developer 2010 Express ("Visual Web Developer" 또는 "VWD") 또는 Visual Studio 2010를 사용 하 여 *StartMusicStore* 파일을 엽니다.

CTRL + F5 키를 눌러 응용 프로그램을 실행 하 고 **테스트** 링크를 클릭 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

**영화 범주 선택 (단순)** 링크를 선택 합니다. 선택한 값을 코미디 하는 영화 유형 선택 목록이 표시 됩니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

브라우저를 마우스 오른쪽 단추로 클릭 하 고 소스 보기를 선택 합니다. 페이지의 HTML이 표시 됩니다. 아래 코드에서는 select 요소의 HTML을 보여 줍니다.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

Select 목록의 각 항목에는 값 (동작의 경우 0, 드라마의 경우 1, 코미디의 경우 2, 과학 Fiction의 경우 3) 및 표시 이름 (Action, 드라마, 코미디 및 과학 Fiction)이 있습니다. 위의 코드는 선택 목록에 대 한 표준 HTML입니다.

선택 목록을 드라마로 변경 하 고 **제출** 단추를 누릅니다. 브라우저의 URL이 `http://localhost:2468/Home/CategoryChosen?MovieType=1` 고 선택한 페이지가 표시 됩니다 **. 1**.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

*Controllers\ homecontroller.cs* 파일을 열고 `SelectCategory` 메서드를 검사 합니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

HTML select 목록을 만드는 데 사용 되는 [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) 도우미에는 명시적 또는 암시적으로 **IEnumerable&lt;selectlistitem &gt;** 필요 합니다. 즉, **ienumerable&lt;selectlistitem &gt;** 를 [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) 도우미에 명시적으로 전달 하거나, **selectlistitem** 에 대해 모델 속성과 같은 이름을 사용 하 여 **Ienumerable&lt;selectlistitem &gt;** 을 [viewbag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 에 추가할 수 있습니다. 암시적 및 명시적으로 **Selectlistitem** 을 전달 하는 방법은 자습서의 다음 부분에 설명 되어 있습니다. 위의 코드는 **IEnumerable&lt;SelectListItem &gt;** 를 만들고 텍스트 및 값으로 채울 수 있는 가장 간단한 방법을 보여 줍니다. `Comedy`[Selectlistitem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 은 [선택](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx) 된 속성을 **true** 로 설정 하 여 렌더링 된 select 목록에서 **코미디** 를 목록에서 선택한 항목으로 표시 합니다.

위에서 만든 **IEnumerable&lt;SelectListItem &gt;** 이름이 MovieType 인 [viewbag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 에 추가 됩니다. 이는 **IEnumerable&lt;SelectListItem &gt;** 를 아래 표시 된 [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) 도우미에 암시적으로 전달 하는 방법입니다.

*Views\Home\SelectCategory.cshtml* 파일을 열고 태그를 검사 합니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

세 번째 줄에서는 레이아웃을 Views/Shared/\_Simple\_Layout으로 설정 합니다 .이는 표준 레이아웃 파일의 단순화 된 버전입니다. 표시 및 렌더링 된 HTML을 간단 하 게 유지 하기 위해이 작업을 수행 합니다.

이 샘플에서는 응용 프로그램의 상태를 변경 하지 않으므로 http **POST**가 아닌 **http GET**을 사용 하 여 데이터를 전송 합니다. [HTTP GET 또는 POST를 선택 하려면 W3C 섹션 빠른 검사 목록](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)을 참조 하세요. 응용 프로그램을 변경 하 고 폼을 게시 하는 것이 아니므로 작업 메서드, 컨트롤러 및 폼 메서드 (**HTTP POST** 또는 **http GET**)를 지정할 수 있는 [html.beginform](https://msdn.microsoft.com/library/dd460344.aspx) 오버 로드를 사용 합니다. 일반적으로 뷰는 매개 변수를 사용 하지 않는 [html.beginform](https://msdn.microsoft.com/library/dd505244.aspx) 오버 로드를 포함 합니다. 매개 변수 버전 없음은 동일한 작업 메서드 및 컨트롤러의 POST 버전에 폼 데이터를 게시 하는 기본 설정입니다.

다음 줄

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

문자열 인수를 **DropDownList** 도우미에 전달 합니다. 이 예제에서 "MovieType" 문자열은 다음 두 가지를 수행 합니다.

- 이 클래스는 **Viewbag**의 **IEnumerable&lt;selectlistitem &gt;** 를 찾기 위해 **DropDownList** 도우미에 대 한 키를 제공 합니다.
- MovieType form 요소에 데이터 바인딩됩니다. Submit 메서드가 **HTTP GET**인 경우 `MovieType`는 쿼리 문자열입니다. Submit 메서드가 **HTTP POST**이면 메시지 본문에 `MovieType` 추가 됩니다. 다음 그림은 값이 1 인 쿼리 문자열을 보여 줍니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

다음 코드는 폼이 전송 된 `CategoryChosen` 메서드를 보여 줍니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

테스트 페이지로 다시 이동 하 여 **HTML SelectList** 링크를 선택 합니다. HTML 페이지는 simple ASP.NET MVC 테스트 페이지와 비슷한 select 요소를 렌더링 합니다. 브라우저 창을 마우스 오른쪽 단추로 클릭 하 고 **소스 보기**를 선택 합니다. 선택 목록에 대 한 HTML 태그는 본질적으로 동일 합니다. HTML 페이지를 테스트 합니다. ASP.NET MVC 작업 메서드 및 이전에 테스트 한 보기와 같이 작동 합니다.

### <a name="improving-the-movie-select-list-with-enums"></a>열거형을 사용 하 여 동영상 선택 목록 향상

응용 프로그램의 범주가 고정 되어 변경 되지 않는 경우에는 열거형을 활용 하 여 코드를 보다 강력 하 고 쉽게 확장할 수 있습니다. 새 범주를 추가 하면 올바른 범주 값이 생성 됩니다. 에서는 새 범주를 추가할 때 복사 및 붙여넣기 오류를 방지 하 고 범주 값을 업데이트 하는 것을 잊지 않습니다.

*Controllers\ homecontroller.cs* 파일을 열고 다음 코드를 검사 합니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

[열거형](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx) `eMovieCategories` 네 가지 동영상 형식을 캡처합니다. `SetViewBagMovieType` 메서드는 `eMovieCategories`**열거형**에서 **IEnumerable&lt;selectlistitem &gt;** 를 만들고 `Selected` 매개 변수에서 `selectedMovie` 속성을 설정 합니다. `SelectCategoryEnum` 동작 메서드는 `SelectCategory` 작업 메서드와 동일한 뷰를 사용 합니다.

테스트 페이지로 이동 하 여 `Select Movie Category (Enum)` 링크를 클릭 합니다. 이번에는 표시 되는 값 (숫자) 대신 열거형을 나타내는 문자열이 표시 됩니다.

### <a name="posting-enum-values"></a>열거형 값 게시

HTML 폼은 일반적으로 서버에 데이터를 게시 하는 데 사용 됩니다. 다음 코드에서는 `SelectCategoryEnumPost` 메서드의 `HTTP GET` 및 `HTTP POST` 버전을 보여 줍니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

`eMovieCategories` 열거형을 `POST` 메서드에 전달 하면 열거형 값과 열거형 문자열을 모두 추출할 수 있습니다. 샘플을 실행 하 고 테스트 페이지로 이동 합니다. `Select Movie Category(Enum Post)` 링크를 클릭 합니다. 영화 유형을 선택 하 고 제출 단추를 누릅니다. 표시에는 동영상 형식의 값과 이름이 모두 표시 됩니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>여러 Section Select 요소 만들기

[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) html 도우미는 `multiple` 특성을 사용 하 여 html `<select>` 요소를 렌더링 합니다. 그러면 사용자가 여러 항목을 선택할 수 있습니다. 테스트 링크로 이동한 다음, **국가 다중 선택** 링크를 선택 합니다. 렌더링 된 UI를 사용 하 여 여러 국가를 선택할 수 있습니다. 아래 이미지에서 캐나다 및 중국이 선택 됩니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>MultiSelectCountry 코드 검사

*Controllers\ homecontroller.cs* 파일에서 다음 코드를 검사 합니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

`GetCountries` 메서드는 국가 목록을 만든 다음 `MultiSelectList` 생성자에 전달 합니다. 위의 `GetCountries` 메서드에 사용 된 `MultiSelectList` 생성자 오버 로드에는 다음 4 개의 매개 변수가 사용 됩니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *items*: 목록의 항목을 포함 하는 [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 입니다. 위의 예제에서 국가 목록입니다.
2. *Datavaluefield*: **IEnumerable** 목록에서 값을 포함 하는 속성의 이름입니다. 위의 예제에서 `ID` 속성입니다.
3. *dataTextField*: 표시할 정보를 포함 하는 **IEnumerable** 목록의 속성 이름입니다. 위의 예제에서 `name` 속성입니다.
4. *selectedvalues*: 선택한 값의 목록입니다.

위의 예제에서 `MultiSelectCountry` 메서드는 선택한 국가에 대 한 `null` 값을 전달 하므로 UI가 표시 될 때 국가가 선택 되지 않습니다. 다음 코드는 `MultiSelectCountry` 뷰를 렌더링 하는 데 사용 되는 Razor 태그를 보여 줍니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

위에서 사용 된 HTML 도우미 [ListBox](https://msdn.microsoft.com/library/dd470200.aspx) 메서드는 두 개의 매개 변수, 모델 바인딩의 속성 이름 및 select 옵션과 값을 포함 하는 [multiselectlist](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx) 를 사용 합니다. 위의 `ViewBag.YouSelected` 코드는 양식을 제출할 때 선택한 국가의 값을 표시 하는 데 사용 됩니다. `MultiSelectCountry` 메서드의 HTTP POST 오버 로드를 검사 합니다.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

`ViewBag.YouSelected` 동적 속성은 양식 컬렉션에서 `Countries` 항목에 대해 가져온 선택 된 국가를 포함 합니다. 이 버전에서는 GetCountries 메서드에 선택한 국가의 목록이 전달 되므로 `MultiSelectCountry` 보기가 표시 되 면 선택한 국가가 UI에서 선택 됩니다.

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>선택한 jQuery 플러그 인을 사용 하 여 선택한 요소를 쉽게 만들기

[선택한](https://harvesthq.github.com/chosen/) jQuery 플러그 인을 HTML &lt;추가 하 여 사용자에 게 친숙 한 UI를 만들 수&gt; 요소를 선택할 수 있습니다. 아래 이미지는 `MultiSelectCountry` 뷰를 사용 하 여 [선택한](https://harvesthq.github.com/chosen/) jQuery 플러그 인을 보여 줍니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

아래 두 이미지에서 **캐나다** 를 선택 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

위의 이미지에서 캐나다를 선택 하 고 클릭 하 여 선택 항목을 제거할 수 있는 **x** 를 포함 합니다. 아래 이미지는 캐나다, 중국 및 일본을 선택 합니다.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>수집 된 jQuery 플러그 인을 후크 합니다.

다음 섹션은 jQuery를 사용 하는 경험이 있는 경우 더 쉽게 수행할 수 있습니다. 이전에 jQuery를 사용한 적이 없는 경우 다음 jQuery 자습서 중 하나를 시도해 볼 수 있습니다.

- [John Resig](http://ejohn.org/) 에서 [JQuery가 작동 하는 방식](http://docs.jquery.com/Tutorials:How_jQuery_Works)
- [Jörn Zaefferer](http://bassistance.de/) 에서 [jQuery 시작](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery)
- [Cody Lindley](http://codylindley.com/) 에서 [의 jQuery 라이브 예](http://codylindley.com/blogstuff/js/jquery/#)

선택한 플러그 인은이 자습서와 함께 제공 되는 스타터 및 completed 샘플 프로젝트에 포함 되어 있습니다. 이 자습서에서는 jQuery를 사용 하 여 UI에 연결 하기만 하면 됩니다. ASP.NET MVC 프로젝트에서 선택한 jQuery 플러그 인을 사용 하려면 다음을 수행 해야 합니다.

1. [Github](https://github.com/harvesthq/chosen/)에서 선택한 플러그 인을 다운로드 합니다. 이 단계가 수행 되었습니다.
2. ASP.NET MVC 프로젝트에 선택한 폴더를 추가 합니다. 이전 단계에서 다운로드 한 선택한 플러그 인에서 선택한 폴더에 자산을 추가 합니다. 이 단계가 수행 되었습니다.
3. 선택한 플러그 인을 **DropDownList** 또는 **ListBox** HTML 도우미에 연결 합니다.

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>선택한 플러그 인을 MultiSelectCountry 보기에 연결 합니다.

*Views\Home\MultiSelectCountry.cshtml* 파일을 열고 `Html.ListBox`에 `htmlAttributes` 매개 변수를 추가 합니다. 추가할 매개 변수에는 선택 목록에 대 한 클래스 이름 (`@class = "chzn-select"`)이 포함 됩니다. 완성 된 코드는 다음과 같습니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

위의 코드에서는 `class = "chzn-select"`HTML 특성 및 특성 값을 추가 합니다. 클래스 앞의 \@ 문자는 Razor 뷰 엔진과는 관련이 없습니다. `class`는 [ C# 키워드](https://msdn.microsoft.com/library/x53a06bb.aspx)입니다. C#키워드는 접두사로 \@를 포함 하지 않는 한 식별자로 사용할 수 없습니다. 위의 예제에서 `@class`는 유효한 식별자 **이지만 클래스는 키워드 이기 때문에** **클래스가** 아닙니다.

선택 된 */선택 된 jquery* 파일에 참조를 추가 하 고 *선택한/선택한 .css* 파일을 선택 합니다. 선택 된 */선택 된 jquery* . 및는 선택한 플러그 인의 기능적 기능을 구현 합니다. *선택/선택 된 .css* 파일은 스타일을 제공 합니다. *Views\Home\MultiSelectCountry.cshtml* 파일의 아래쪽에 이러한 참조를 추가 합니다. 다음 코드에서는 선택 된 플러그 인을 참조 하는 방법을 보여 줍니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

**Html. ListBox** 코드에 사용 된 클래스 이름을 사용 하 여 선택한 플러그 인을 활성화 합니다. 위의 예제에서는 클래스 이름이 `chzn-select`입니다. *Views\Home\MultiSelectCountry.cshtml* view 파일의 아래쪽에 다음 줄을 추가 합니다. 이 줄은 선택한 플러그 인을 활성화 합니다.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

다음 줄은 jQuery ready 함수를 호출 하는 구문입니다 .이 함수는 클래스 이름이 `chzn-select`인 DOM 요소를 선택 합니다.

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

위의 호출에서 반환 된 래핑된 집합은 선택한 메서드 (`.chosen();`)를 적용 하 여 선택한 플러그 인을 후크합니다.

다음 코드는 완성 된 *Views\Home\MultiSelectCountry.cshtml* view 파일을 보여 줍니다.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

응용 프로그램을 실행 하 고 `MultiSelectCountry` 뷰로 이동 합니다. 국가를 추가 및 삭제 해 보세요. 또한 제공 되는 샘플 다운로드에는 **Viewbag**대신 뷰 모델을 사용 하 여 MultiSelectCountry 기능을 구현 하는 `MultiCountryVM` 메서드와 뷰가 포함 되어 있습니다.

다음 섹션에서는 ASP.NET MVC 스 캐 폴딩 메커니즘이 **DropDownList** 도우미와 작동 하는 방식을 알아봅니다.

> [!div class="step-by-step"]
> [다음](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
