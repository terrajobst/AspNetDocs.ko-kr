---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-1 부 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup을 사용 하 여 작업 하는 방법에 대 한 기본 사항을 학습 합니다. ASP.NET m ...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: c1c2380f24c72f6aabaaacaf975e95288a384ff1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457624"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a>ASP.NET MVC에서 HTML5 및 jQuery UI Datepicker 팝업 일정 사용-1 부

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 ASP.NET MVC 웹 응용 프로그램에서 편집기 템플릿, 표시 템플릿 및 jQuery UI datepicker popup 일정을 사용 하는 방법에 대 한 기본 사항을 설명 합니다.

이 자습서에서는 ASP.NET MVC 웹 응용 프로그램에서 편집기 템플릿, 표시 템플릿 및 jQuery [UI datepicker popup 일정](http://plugins.jquery.com/project/datepicker) 을 사용 하는 방법에 대 한 기본 사항을 설명 합니다. 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (&quot;Visual Web Developer&quot;)을 사용 하거나 이미 있는 경우 Visual Studio 2010 s p 1을 사용할 수 있습니다.

시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 소프트웨어를 개별적으로 설치할 수 있습니다.

- [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)

Visual Web Developer 대신 visual Studio 2010을 사용 하는 경우 다음 링크를 클릭 하 여 필수 구성 요소를 설치 합니다. [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).

이 자습서에서는 [mvc 3 시작](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서를 완료 했거나 ASP.NET mvc 개발에 대해 잘 알고 있다고 가정 합니다. 이 자습서는 [MVC 3 시작](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서에서 완료 된 프로젝트로 시작 합니다.

이 자습서에서는의 코드 C#를 보여 줍니다. 그러나 [시작 프로젝트](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) 와 완료 된 프로젝트는 Visual Basic 에서도 사용할 수 있습니다.

및 Visual Basic 소스 코드를 C# 사용 하 여 Visual Studio 프로젝트를 [다운로드](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800)합니다.

### <a name="what-youll-build"></a>만들 내용

[MVC 3 시작](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 자습서에서 만든 간단한 영화 목록 응용 프로그램에 템플릿 (특히, 편집 및 표시 템플릿)을 추가 합니다. 또한 [JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/) popup 일정을 추가 하 여 날짜 입력 프로세스를 간소화 합니다. 다음 스크린샷에서는 jQuery UI datepicker popup이 표시 된 수정 된 응용 프로그램을 보여 줍니다.

![jQuery 완료](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a>학습할 기술

다음 내용을 학습하게 됩니다.

- [Dataannotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) 네임 스페이스의 특성을 사용 하 여 데이터가 표시 될 때 및 편집 모드에 있을 때의 형식을 제어 하는 방법입니다.
- 템플릿 (편집 및 표시 템플릿)을 만들어 데이터의 서식을 제어 하는 방법입니다.
- 데이터 필드를 입력 하는 방법으로 [JQUERY UI datepicker](http://jqueryui.com/demos/datepicker/) 를 추가 하는 방법입니다.

### <a name="getting-started"></a>시작하기

스타터 프로젝트에서 영화 목록 응용 프로그램이 아직 없는 경우 다운로드 합니다. 

* [다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).
* Windows 탐색기에서 *Mvcmovie .zip* 파일을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. 
* **Mvcmovie. Zip 속성** 대화 상자에서 **차단 해제**를 선택 합니다. (차단 해제는 웹에서 다운로드한 *.zip* 파일을 사용하려고 할 때 발생하는 보안 경고를 막습니다.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

*Mvcmovie .zip* 파일을 마우스 오른쪽 단추로 클릭 하 고 **압축 풀기** 를 선택 하 여 파일의 압축을 풉니다. Visual Web Developer 또는 Visual Studio 2010에서 *MvcMovieCS\_TU* 파일을 엽니다.

**솔루션 탐색기**에서 *Views\Shared\\_Layout* 두 번 클릭 하 여 엽니다. **MVC Movie 앱** 에서 **movie jQuery**로 `H1` 헤더를 변경 합니다. CTRL + F5 키를 눌러 응용 프로그램을 실행 하 고 **홈** 탭을 클릭 하 여 동영상 컨트롤러의 `Index` 메서드로 이동 합니다. 응용 프로그램을 사용해 보려면 **편집** 링크를 선택 하 고 동영상 중 하나에 대 한 **세부 정보** 링크를 선택 합니다. 인덱스, 편집 및 세부 정보 보기에서 릴리스 날짜와 가격은 깔끔하게 형식이 지정 됩니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

날짜 및 가격의 서식은 `Movie` 클래스의 속성에서 [Displayformat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) 특성을 사용한 결과입니다.

*Movie.cs* 파일을 열고 `ReleaseDate` 및 `Price` 속성에 `DisplayFormat` 특성을 주석으로 처리 합니다. 결과 `Movie` 클래스는 다음과 같습니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

CTRL + F5 키를 눌러 응용 프로그램을 실행 하 고 **홈** 탭을 선택 하 여 동영상 목록을 봅니다. 이번에는 릴리스 날짜에 날짜 및 시간이 표시 되 고 price 필드에는 더 이상 통화 기호가 표시 되지 않습니다. `Movie` 클래스에서 변경한 내용이 이전에 확인 된 좋은 서식을 취소 했지만 잠시 후에 수정할 수 있습니다.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a>DataAnnotations DataType 특성을 사용 하 여 데이터 형식 지정

`Date` 열거를 사용 하 여 `ReleaseDate` 속성의 주석 처리 된 `DisplayFormat` 특성을 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성으로 바꿉니다. 이번에는 `Currency` 열거를 사용 하 여 `Price` 속성의 `DisplayFormat` 특성을 [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성으로 대체 합니다. 완성 된 코드는 다음과 같습니다.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

애플리케이션을 실행합니다. 이제 릴리스 날짜와 price 속성의 형식이 올바르게 지정 됩니다 (즉, 적절 한 날짜 및 통화 형식 사용). [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) 특성은 필드가 올바른 형식으로 렌더링 되도록 기본 제공 ASP.NET MVC 템플릿에 대 한 형식 메타 데이터를 제공 합니다. `DataType` 특성을 사용 하면 국제화와 같이 모델을 더 깔끔하고 유연 하 게 만들 수 있기 때문에 `DataType` 특성을 사용 하는 것이 코드에서 원래 있던 `DisplayFormat` 특성을 사용 하는 것이 좋습니다.

다음 섹션에서는 날짜 필드를 표시 하는 사용자 지정 템플릿을 만드는 방법에 대해 알아봅니다.

> [!div class="step-by-step"]
> [다음](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
