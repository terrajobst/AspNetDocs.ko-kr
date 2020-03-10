---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: 뷰 추가 (VB) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: fa200935d83bb26c07b302449a6eba6fd67b5322
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434519"
---
# <a name="adding-a-view-vb"></a>보기 추가(VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.
> 
> VB.NET 소스 코드를 사용 하는 Visual Web Developer 프로젝트를이 항목과 함께 사용할 수 있습니다. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 선호 C#하는 경우이 자습서의 [ C# 버전](../cs/adding-a-view.md) 으로 전환 합니다.

이 섹션에서는 뷰 템플릿 파일을 사용 하 여 클라이언트에 HTML 응답을 생성 하는 프로세스를 명확 하 게 캡슐화 하는 `HelloWorldController` 클래스를 수정 하겠습니다.

`HelloWorldController` 클래스에서 `Index` 메서드와 함께 뷰 템플릿을 사용 하 여 시작 해 보겠습니다. 현재 `Index` 메서드는 컨트롤러 클래스 내에서 하드 코딩 된 메시지와 함께 문자열을 반환 합니다. 다음과 같이 `Index` 메서드를 변경 하 여 `View` 개체를 반환 합니다.

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

이제 `Index` 메서드를 사용 하 여 호출할 수 있는 뷰 템플릿을 프로젝트에 추가 하겠습니다. 이렇게 하려면 `Index` 메서드 내부를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 클릭 합니다.

[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)

**뷰 추가** 대화 상자가 나타납니다. 기본 항목을 그대로 두고 **추가** 단추를 클릭 합니다.

[![3 Addview](adding-a-view/_static/image4.png "3 Addview")](adding-a-view/_static/image3.png)

*MvcMovie\Views\HelloWorld* 폴더와 *MvcMovie\Views\HelloWorld\Index.vbhtml* 파일이 만들어집니다. **솔루션 탐색기**에서 볼 수 있습니다.

[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)

`<h2>` 태그 아래에 HTML을 추가 합니다. 수정 된 *MvcMovie\Views\HelloWorld\Index.vbhtml* 파일은 다음과 같습니다.

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

응용 프로그램을 실행 하 고 &quot;hello 세계&quot; 컨트롤러 (`http://localhost:xxxx/HelloWorld`)로 이동 합니다. 컨트롤러의 `Index` 메서드가 많은 작업을 수행 하지 않았습니다. 단지 뷰 템플릿 파일을 사용 하 여 클라이언트에 대 한 응답을 렌더링 하려는 것으로 표시 된 `return View()`문을 실행 했습니다. 사용할 뷰 템플릿 파일의 이름을 명시적으로 지정 하지 않았기 때문에 ASP.NET MVC는 \Views\HelloWorld 폴더에 있는 파일을 사용 하 여 기본적으로 사용 *됩니다.* 아래 이미지는 뷰에 하드 코드 된 문자열을 보여 줍니다.

[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)

매우 유용 합니다. 그러나 브라우저의 제목 표시줄에 &quot;인덱스&quot;와 페이지의 큰 제목은 내 MVC 응용 프로그램 &quot;이라고 표시 됩니다.&quot; 변경 하겠습니다.

## <a name="changing-views-and-layout-pages"></a>보기 및 레이아웃 페이지 변경

먼저, 내 MVC 응용 프로그램 &quot;텍스트를 변경 하겠습니다. 텍스트를 공유 하 고 모든 페이지에 표시&quot; 합니다. 응용 프로그램의 모든 페이지에 있는 경우에도 실제로는 프로젝트의 한 곳에만 표시 됩니다. **솔루션 탐색기** 의 */Views/Shared* 폴더로 이동 하 여 *\_레이아웃. vbhtml* 파일을 엽니다. 이 파일을 레이아웃 페이지 라고 하며 다른 모든 페이지에서 사용 하&quot; 공유 &quot;shell입니다.

파일의 아래쪽 근처에 `@RenderBody()` 코드 줄을 확인 합니다. `RenderBody`은 사용자가 만드는 모든 페이지가 표시 되는 자리 표시자 이며 레이아웃 페이지에서&quot; &quot;래핑됩니다. `<h1>` 제목을 **&quot;** 내 Mvc 응용 프로그램&quot;에서 &quot;Mvc Movie 앱&quot;으로 변경 합니다.

[!code-html[Main](adding-a-view/samples/sample3.html)]

응용 프로그램을 실행 하 고 &quot;MVC Movie 앱&quot;을 참조 하세요. **About** 링크를 클릭 하면 해당 페이지에 &quot;MVC Movie 앱&quot;표시 됩니다.

전체 *\_레이아웃. vbhtml* 파일은 다음과 같습니다.

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

이제 인덱스 페이지 (보기)의 제목을 변경 하겠습니다.

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

*MvcMovie\Views\HelloWorld\Index.vbhtml*를 엽니다. 변경 하는 데는 두 가지 위치가 있습니다. 첫 번째는 브라우저의 제목에 표시 되는 텍스트이 고, 그 다음에는 보조 헤더 (`<h2>` 요소)에 표시 됩니다. 앱의 어느 부분에서 어떤 코드를 변경 하는지 확인할 수 있도록 약간 다르게 만들 것입니다.

응용 프로그램을 실행 하 고`http://localhost:xx/HelloWorld`로 이동 합니다. 브라우저 제목, 기본 제목 및 작은 제목이 변경된 것을 확인합니다. 보기를 약간만 변경 하 여 응용 프로그램을 크게 변경 하는 것이 쉽습니다. (브라우저에서 변경 내용을 확인할 수 없는 경우 캐시된 콘텐츠를 보고 있을 수도 있습니다. 브라우저에서 Ctrl+F5 키를 눌러서 로드될 응답을 강제로 서버에서 가져옵니다.)

[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)

그러나 약간의 &quot;데이터&quot; (이 경우 &quot;Hello World!&quot; 메시지)는 하드 코드 되어 있습니다. MVC 응용 프로그램에는 V (뷰)가 있지만 C (컨트롤러)는 있지만 M (모델)은 없습니다. 잠시 후 데이터베이스를 만들고 해당 데이터베이스에서 모델 데이터를 검색 하는 방법을 살펴보겠습니다.

## <a name="passing-data-from-the-controller-to-the-view"></a>컨트롤러에서 보기로 데이터 전달

데이터베이스로 이동 하 여 모델에 대해 이야기 하기 전에 먼저 컨트롤러에서 뷰로 정보를 전달 하는 방법에 대해 알아보겠습니다. HTML 응답을 클라이언트에 렌더링 하기 위해 뷰 템플릿이 필요한 항목을 전달 하려고 합니다. 이러한 개체는 일반적으로 컨트롤러 클래스에서 만들고 뷰 템플릿에 전달 하며, 뷰 템플릿에 필요한 데이터만 포함 해야 합니다.

이전에는 `HelloWorldController` 클래스를 사용 하 여 `Welcome` 동작 메서드에서 `name`와 `numTimes` 매개 변수를 사용 하 고 매개 변수 값을 브라우저에 출력 합니다. 컨트롤러에서이 응답을 계속 해 서 직접 렌더링 하는 대신 해당 데이터를 보기에 대 한 모음에 추가 하겠습니다. 컨트롤러와 뷰는 `ViewBag` 개체를 사용 하 여 해당 데이터를 보유할 수 있습니다. 이는 뷰 템플릿으로 자동으로 전달 되 고 모음 내용을 데이터로 사용 하 여 HTML 응답을 렌더링 하는 데 사용 됩니다. 이러한 방식으로 컨트롤러는 한 가지 작업 및 보기 템플릿과 관련 된 작업을 수행 하 여 응용 프로그램 내에서&quot; 문제를 명확 하 게 &quot;분리할 수 있도록 합니다.

또는 사용자 지정 클래스를 정의한 다음 해당 개체의 인스턴스를 만들어 데이터를 채운 다음 뷰로 전달할 수 있습니다. 이는 뷰의 사용자 지정 모델 이기 때문에 일반적으로 ViewModel 이라고 합니다. 그러나 적은 양의 데이터에 대해 ViewBag는 잘 작동 합니다.

*HelloWorldController* 파일로 돌아가면 메시지와 Numtimes를 viewbag에 넣기 위해 컨트롤러 내의 `Welcome` 메서드를 변경 합니다. ViewBag는 동적 개체입니다. 즉, 원하는 모든 항목을 배치할 수 있습니다. ViewBag에는 속성 내에 항목을 넣을 때까지 정의 된 속성이 없습니다.

동일한 파일에서 새 클래스를 사용 하 여 전체 `HelloWorldController.vb` 합니다.

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

이제 ViewBag에는 뷰에 자동으로 전달 되는 데이터가 포함 되어 있습니다. 마찬가지로, 좋아요를 사용할 경우 다음과 같이 자체 개체를 전달할 수도 있습니다.

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

이제 `WelcomeView` 템플릿이 필요 합니다. 새 코드를 컴파일하기 위해 응용 프로그램을 실행 합니다. 브라우저를 닫고 `Welcome` 메서드 내부를 마우스 오른쪽 단추로 클릭 한 다음 **뷰 추가**를 클릭 합니다.

**보기 추가** 대화 상자는 다음과 같습니다.

[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)

새 시작의 `<h2>` 요소 아래에 다음 코드를 추가 합니다 <em>.</em> vbhtml 파일. 사용자에 게 표시 되는 횟수 만큼 루프와 &quot;Hello&quot;를 살펴보겠습니다.

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

응용 프로그램을 실행 하 고 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`를 찾습니다.

이제 데이터가 URL에서 가져온 후 컨트롤러에 자동으로 전달 됩니다. 컨트롤러는 데이터를 `Model` 개체에 패키지 하 고 해당 개체를 뷰에 전달 합니다. 보기는 사용자에 게 데이터를 HTML로 표시 합니다.

[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)

모델에 대 한 &quot;M&quot;의 일종 이지만 데이터베이스 종류는 아닙니다. 지금까지 학습한 것을 살펴보고 동영상의 데이터베이스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](adding-a-controller.md)
> [다음](adding-a-model.md)
