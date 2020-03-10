---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: '3 부: 뷰 및 ViewModels | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 3 부에서는 뷰 및 ViewModels을 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451133"
---
# <a name="part-3-views-and-viewmodels"></a>3 부: 뷰 및 ViewModels

받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.  
>   
> MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 3 부에서는 뷰 및 ViewModels을 다룹니다.

지금까지 컨트롤러 작업에서 문자열을 반환 했습니다. 이 방법은 컨트롤러의 작동 방식을 파악 하는 좋은 방법 이지만 실제 웹 응용 프로그램을 빌드하는 방법은 아닙니다. 사이트를 방문 하는 브라우저에 다시 HTML을 생성 하는 더 나은 방법을 원할 것입니다. 즉, 템플릿 파일을 사용 하 여 HTML 콘텐츠를 더 쉽게 사용자 지정할 수 있습니다. 이는 보기에서 수행 하는 작업입니다.

## <a name="adding-a-view-template"></a>보기 템플릿 추가

뷰 템플릿을 사용 하려면 HomeController Index 메서드를 변경 하 여 ActionResult를 반환 하 고 아래와 같이 View ()를 반환 하도록 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

위의 변경 내용은 대신 문자열을 반환 하는 대신 "뷰"를 사용 하 여 결과를 다시 생성 하는 것을 나타냅니다.

이제 프로젝트에 적절 한 뷰 템플릿을 추가 합니다. 이렇게 하려면 인덱스 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 "뷰 추가"를 선택 합니다. 그러면 보기 추가 대화 상자가 표시 됩니다.

![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)

"뷰 추가" 대화 상자를 사용 하 여 보기 템플릿 파일을 빠르고 쉽게 생성할 수 있습니다. 기본적으로 "뷰 추가" 대화 상자는 만들 뷰 템플릿의 이름을 미리 채우고,이를 사용 하는 동작 메서드와 일치 하도록 만듭니다. HomeController의 Index () 동작 메서드 내에서 "뷰 추가" 상황에 맞는 메뉴를 사용 했으므로 위의 "뷰 추가" 대화 상자에는 기본적으로 미리 채워진 뷰 이름으로 "인덱스"가 있습니다. 이 대화 상자의 옵션을 변경할 필요 없이 추가 단추를 클릭 합니다.

추가 단추를 클릭 하면 Visual Web Developer에서 \Views\Home 디렉터리에 새 인덱스를 만듭니다 .이 폴더는 아직 존재 하지 않는 경우 폴더를 만듭니다.

![](mvc-music-store-part-3/_static/image2.png)

"Index. cshtml" 파일의 이름 및 폴더 위치는 중요 하며 기본 ASP.NET MVC 명명 규칙을 따릅니다. 디렉터리 이름 \Views\Home는 HomeController 라는 컨트롤러와 일치 합니다. 뷰 템플릿 이름 Index는 뷰를 표시 하는 컨트롤러 작업 메서드와 일치 합니다.

ASP.NET MVC를 사용 하면이 명명 규칙을 사용 하 여 뷰를 반환할 때 뷰 템플릿의 이름이 나 위치를 명시적으로 지정 하지 않아도 됩니다. HomeController 내에서 아래와 같이 코드를 작성할 때 기본적으로 \Views\Home\Index.cshtml view 템플릿이 렌더링 됩니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

"뷰 추가" 대화 상자에서 "추가" 단추를 클릭 한 후에 Visual Web Developer에서 "Index. cshtml" 뷰 템플릿을 만들고 열었습니다. Index. cshtml의 내용은 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

이 보기는 ASP.NET Web Forms 및 이전 버전의 ASP.NET MVC에서 사용 되는 Web Forms 뷰 엔진 보다 간결한 Razor 구문를 사용 합니다. Web Forms 뷰 엔진은 ASP.NET MVC 3에서 계속 사용할 수 있지만 대부분의 개발자는 Razor 뷰 엔진이 ASP.NET MVC 개발을 잘 충족 한다는 것을 알게 되었습니다.

처음 세 줄에서는 ViewBag를 사용 하 여 페이지 제목을 설정 합니다. 이 방법이 곧 어떻게 작동 하는지 살펴보겠습니다. 먼저 텍스트 제목 텍스트를 업데이트 하 고 페이지를 확인 하겠습니다. 아래와 같이 &lt;h2&gt; 태그를 "이것이 홈 페이지입니다."로 업데이트 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

응용 프로그램을 실행 하면 새 텍스트가 홈 페이지에 표시 되는 것을 볼 수 있습니다.

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a>공통 사이트 요소에 레이아웃 사용

대부분의 웹 사이트에는 탐색, 바닥글, 로고 이미지, 스타일 시트 참조 등 여러 페이지 간에 공유 되는 콘텐츠가 있습니다. Razor 뷰 엔진을 사용 하면/Views/Shared 폴더 내에 자동으로 생성 된 레이아웃. cshtml \_이라는 페이지를 사용 하 여이를 쉽게 관리할 수 있습니다.

![](mvc-music-store-part-3/_static/image4.png)

이 폴더를 두 번 클릭 하면 아래와 같은 내용이 표시 됩니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

개별 보기의 콘텐츠는 @RenderBody() 명령에 의해 표시 되 고 외부에 표시 하려는 모든 공통 콘텐츠는 \_레이아웃에 추가할 수 있습니다. cshtml 태그. MVC Music Store에는 홈 페이지에 대 한 링크가 포함 된 공통 헤더와 사이트의 모든 페이지에 대 한 저장 영역이 있으므로 해당 @RenderBody() 문 바로 위의 템플릿에 추가 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a>스타일 시트 업데이트

빈 프로젝트 템플릿에는 유효성 검사 메시지를 표시 하는 데 사용 되는 스타일을 포함 하는 매우 간소화 된 CSS 파일이 포함 되어 있습니다. Microsoft의 디자이너는 사이트의 모양과 느낌을 정의 하기 위해 몇 가지 CSS 및 이미지를 제공 했으므로 지금은이를 추가 합니다.

업데이트 된 CSS 파일 및 이미지는 MvcMusicStore-Assets의 콘텐츠 디렉터리에 포함 되며,이는 [MVC-음악 스토어](https://github.com/evilDave/MVC-Music-Store)에서 사용할 수 있습니다. Windows 탐색기에서 두 가지를 모두 선택 하 고 아래와 같이 Visual Web Developer의 솔루션 콘텐츠 폴더에 놓습니다.

![](mvc-music-store-part-3/_static/image5.png)

기존 사이트 .css 파일을 덮어쓸지 여부를 확인 하는 메시지가 표시 됩니다. 예를 클릭합니다.

![](mvc-music-store-part-3/_static/image6.png)

이제 응용 프로그램의 콘텐츠 폴더가 다음과 같이 표시 됩니다.

![](mvc-music-store-part-3/_static/image7.png)

이제 응용 프로그램을 실행 하 여 홈 페이지에 변경 내용이 어떻게 표시 되는지 확인해 보겠습니다.

![](mvc-music-store-part-3/_static/image8.png)

- 변경 된 내용 검토: 뷰 템플릿이 표준 명명 규칙을 준수 하기 때문에 HomeController의 인덱스 작업 메서드는 \Views\Home\Index.cshtmlView 템플릿을 찾아 표시 합니다.
- 홈 페이지에 \Views\Home\Index.cshtml view 템플릿 내에 정의 된 간단한 환영 메시지가 표시 됩니다.
- 홈 페이지는 \_레이아웃을 사용 하 고 있으므로 시작 메시지는 표준 사이트 HTML 레이아웃에 포함 됩니다.

## <a name="using-a-model-to-pass-information-to-our-view"></a>모델을 사용 하 여 보기에 정보 전달

하드 코딩 된 HTML을 표시 하는 보기 템플릿은 매우 흥미로운 웹 사이트를 만들지 않습니다. 동적 웹 사이트를 만들려면 컨트롤러 작업에서 보기 템플릿으로 정보를 전달 하려고 합니다.

모델-뷰-컨트롤러 패턴에서 모델 이라는 용어는 응용 프로그램의 데이터를 나타내는 개체를 나타냅니다. 종종 model 개체는 데이터베이스의 테이블에 해당 하지만 반드시 그런 것은 아닙니다.

ActionResult를 반환 하는 컨트롤러 동작 메서드는 모델 개체를 뷰에 전달할 수 있습니다. 이렇게 하면 컨트롤러에서 응답을 생성 하는 데 필요한 모든 정보를 완전히 패키지할 수 있으며,이 정보를 사용 하 여 적절 한 HTML 응답을 생성 하는 데 사용 하는 보기 템플릿에이 정보를 전달할 수 있습니다. 이 작업을 수행 하는 것을 이해 하는 것이 가장 쉬운 방법 이므로 시작 하겠습니다.

먼저 저장소 내에서 장르 및 앨범을 나타내는 일부 모델 클래스를 만듭니다. 먼저 장르 클래스를 만들어 보겠습니다. 프로젝트 내에서 "모델" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "클래스 추가" 옵션을 선택한 다음 파일 이름을 "Genre.cs"로 합니다.

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

그런 다음 생성 된 클래스에 공용 문자열 이름 속성을 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

*참고: 해당 하는 경우 {get; set;} 표기법은 C#의 자동 구현 속성 기능을 사용 합니다. 이를 통해 지원 필드를 선언 하지 않고도 속성의 이점을 얻을 수 있습니다.*

그런 다음, 동일한 단계를 수행 하 여 제목과 장르 속성이 있는 앨범 클래스 (이름이 Album.cs)를 만듭니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

이제 모델의 동적 정보를 표시 하는 보기를 사용 하도록 StoreController를 수정할 수 있습니다. 현재 데모 목적으로 사용 하는 경우, 요청 ID를 기준으로 앨범의 이름을 지정 하면 아래 보기와 같이 해당 정보를 표시할 수 있습니다.

![](mvc-music-store-part-3/_static/image10.png)

먼저 저장소 정보 작업을 변경 하 여 단일 앨범에 대 한 정보를 표시 합니다. **StoreControllers** 클래스의 맨 위에 "using" 문을 추가 하 여 MvcMusicStore 네임 스페이스를 포함 합니다. 따라서 앨범 클래스를 사용 하려고 할 때마다 MvcMusicStore를 입력할 필요가 없습니다. 이제 해당 클래스의 "using" 섹션이 다음과 같이 표시 됩니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

다음으로 HomeController의 Index 메서드와 같이 문자열이 아니라 ActionResult를 반환 하도록 세부 정보 컨트롤러 작업을 업데이트 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

이제 앨범 개체를 뷰에 반환 하도록 논리를 수정할 수 있습니다. 이 자습서의 뒷부분에서는 데이터베이스에서 데이터를 검색할 예정 이지만, 지금은 "더미 데이터"를 사용 하 여 시작 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

*참고:에 C#익숙하지 않은 경우 var을 사용 한다고 해 서 현재 앨범 변수가 런타임에 바인딩되어 있다고 가정할 수 있습니다. 올바르지 않습니다. 컴파일러는 C# 이 변수에 할당 하는 내용에 따라 형식 유추를 사용 하 여 앨범이 앨범 형식이 고 로컬 앨범 변수를 앨범 형식으로 컴파일 했기 때문에 컴파일 시간 검사 및 Visual Studio code-편집기를 지원 합니다.*

이제 앨범을 사용 하 여 HTML 응답을 생성 하는 보기 템플릿을 만들어 보겠습니다. 이렇게 하려면 먼저 새로 만든 앨범 클래스에 대해 보기 추가 대화 상자에서 알 수 있도록 프로젝트를 빌드해야 합니다. ⇨ Build MvcMusicStore 디버그 메뉴 항목을 선택 하 여 프로젝트를 빌드할 수 있습니다. 추가 크레딧을 위해 Ctrl + Shift + B 바로 가기를 사용 하 여 프로젝트를 빌드할 수 있습니다.

![](mvc-music-store-part-3/_static/image11.png)

이제 지원 클래스를 설정 했으므로 보기 템플릿을 빌드할 준비가 되었습니다. Details 메서드 내에서 마우스 오른쪽 단추를 클릭 하 고 "보기 추가 ..."를 선택 합니다. 상황에 맞는 메뉴에서.

![](mvc-music-store-part-3/_static/image12.png)

HomeController 이전에 했던 것 처럼 새 보기 템플릿을 만들 예정입니다. StoreController에서 생성 하기 때문에 기본적으로 \Views\Store\Index.cshtml 파일에 생성 됩니다.

이전과는 달리 "강력한 형식의" 보기 만들기 "확인란을 선택 하겠습니다. 그런 다음 "데이터 클래스 보기" 드롭다운 목록에서 "앨범" 클래스를 선택 합니다. 이렇게 하면 "뷰 추가" 대화 상자에서 앨범 개체를 사용 하기 위해 전달 될 것으로 예상 되는 보기 템플릿을 만듭니다.

![](mvc-music-store-part-3/_static/image13.png)

"추가" 단추를 클릭 하면 다음 코드가 포함 된 \Views\Store\Details.cshtml View 템플릿이 생성 됩니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

첫 번째 줄은이 뷰가 앨범 클래스에 강력한 형식 임을 나타냅니다. Razor 뷰 엔진은 앨범 개체가 전달 되었음을 인식 하므로 모델 속성에 쉽게 액세스할 수 있으며 Visual Web Developer 편집기에서 IntelliSense의 이점을 누릴 수 있습니다.

&lt;h2&gt; 태그를 업데이트 하 여 다음과 같이 표시 되도록 해당 줄을 수정 하 여 앨범의 Title 속성을 표시 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

@Model 키워드 뒤에 마침표를 입력 하면 해당 사용자가 앨범 클래스에서 지 원하는 속성 및 메서드를 표시 하는 IntelliSense가 트리거됩니다.

이제 프로젝트를 다시 실행 하 고/Store/Details/5 URL을 방문 하겠습니다. 아래와 같은 앨범의 세부 정보가 표시 됩니다.

![](mvc-music-store-part-3/_static/image14.png)

이제 Store Browse 동작 메서드에 대해 비슷한 업데이트를 수행 합니다. ActionResult를 반환 하도록 메서드를 업데이트 하 고 새 장르 개체를 만들어 뷰로 반환 하도록 메서드 논리를 수정 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

찾아보기 메서드를 마우스 오른쪽 단추로 클릭 하 고 "보기 추가 ..."를 선택 합니다. 상황에 맞는 메뉴에서 강력한 형식의 뷰를 추가 하 여 장르 클래스에 강력한 형식의를 추가 합니다.

![](mvc-music-store-part-3/_static/image15.png)

/Views/Store/Browse.cshtml에서 뷰 코드의 &lt;h2&gt; 요소를 업데이트 하 여 장르 정보를 표시 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

이제 프로젝트를 다시 실행 하 고/sv/dhers로 이동 하겠습니다. 장르 = Disco URL. 아래와 같이 표시 되는 찾아보기 페이지가 표시 됩니다.

![](mvc-music-store-part-3/_static/image16.png)

마지막으로 저장소 **인덱스** 작업 메서드 및 보기에 대해 약간 더 복잡 한 업데이트를 수행 하 여 스토어의 모든 장르 목록을 표시 해 보겠습니다. 이 작업을 수행 하려면 단일 장르 대신 모델 개체로 장르 목록을 사용 합니다.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

저장소 인덱스 작업 메서드를 마우스 오른쪽 단추로 클릭 하 고, 이전과 같이 뷰 추가를 선택 하 고, 모델 클래스로 장르를 선택 하 고, 추가 단추를 누릅니다.

![](mvc-music-store-part-3/_static/image17.png)

먼저 @model 선언을 변경 하 여 뷰가 하나만 아닌 여러 장르 개체가 필요한 것을 표시 합니다. 다음과 같이/Hfile/p\index.s의 첫 번째 줄을 다음과 같이 변경 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

이렇게 하면 여러 장르 개체를 보유할 수 있는 모델 개체를 사용 하 여 Razor 뷰 엔진에 지시할 수 있습니다. 이는 보다 일반적인 모델 형식을 IEnumerable 인터페이스를 지 원하는 개체 형식으로 변경할 수 있도록 하는 것이 더 일반적 이므로 목록&lt;장르&gt; 아닌 IEnumerable&lt;장르&gt;를 사용 하 고 있습니다.

다음으로, 아래 완성 된 뷰 코드에 표시 된 대로 모델의 장르 개체를 반복 합니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

이 코드를 입력할 때 전체 IntelliSense를 지원 하므로 "@Model"을 입력 하면 됩니다. 장르 형식의 IEnumerable에서 지 원하는 모든 메서드 및 속성이 표시 됩니다.

![](mvc-music-store-part-3/_static/image18.png)

"Foreach" 루프 내에서 Visual Web Developer는 각 항목이 장르 형식 이라는 것을 인식 하므로 각 장르 형식에 대해 IntelliSense를 참조 합니다.

![](mvc-music-store-part-3/_static/image19.png)

다음으로 스 캐 폴딩 기능은 장르 개체를 검사 하 고 각각에 Name 속성이 있음을 확인 했으므로이를 반복 하 고 작성 합니다. 또한 각 개별 항목에 대 한 편집, 세부 정보 및 삭제 링크를 생성 합니다. 저장소 관리자에서 나중에이 기능을 활용할 수 있지만 지금은 간단한 목록을 사용 하는 것이 좋습니다.

응용 프로그램을 실행 하 고/Store로 이동 하면 장르 수와 장르 목록이 모두 표시 됩니다.

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a>페이지 간 링크 추가

장르를 나열 하는/Store URL은 현재 장르 이름을 일반 텍스트로 나열 합니다. 이를 변경해 보겠습니다. 대신 "Disco"와 같은 음악 장르를 클릭 하면 "Disco"와 같은 음악 장르를 클릭 하 여 "Disco"로 이동 하는 것이 좋습니다. 아래와 같은 코드를 사용 하 여 이러한 링크를 출력 하도록 \Views\Store\Index.cshtml View 템플릿을 업데이트할 수 있습니다 **(이에 대 한 내용을 입력 하지 않음)** .

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

이는 작동 하지만, 나중에 하드 코드 된 문자열을 사용 하기 때문에 문제가 발생할 수 있습니다. 예를 들어 컨트롤러의 이름을 바꾸려는 경우 업데이트 해야 하는 링크를 찾는 코드를 검색 해야 합니다.

사용할 수 있는 다른 방법은 HTML 도우미 메서드를 활용 하는 것입니다. ASP.NET MVC에는 다음과 같은 다양 한 일반적인 작업을 수행 하기 위해 뷰 템플릿 코드에서 사용할 수 있는 HTML 도우미 메서드가 포함 되어 있습니다. Html.actionlink () 도우미 메서드는 특히 유용 하며,&gt; 링크를 &lt;HTML을 쉽게 빌드할 수 있도록 하 고 URL 경로가 적절 하 게 URL로 인코딩 되었는지 확인 하는 것과 같은 성가신 정보를 처리 합니다.

Html.actionlink ()에는 링크에 필요한 만큼의 정보를 지정할 수 있는 여러 오버 로드가 있습니다. 가장 간단한 경우에는 클라이언트에서 하이퍼링크를 클릭 했을 때 이동할 링크 텍스트 및 동작 메서드만 제공 합니다. 예를 들어 다음 호출을 사용 하 여 "저장소 인덱스로 이동" 링크 텍스트가 포함 된 저장소 세부 정보 페이지에서 "/Bv/" Index () 메서드에 연결할 수 있습니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

*참고:이 경우 현재 뷰를 렌더링 하는 것과 동일한 컨트롤러 내의 다른 작업에 연결 하 고 있으므로 컨트롤러 이름을 지정할 필요가 없습니다.*

찾아보기 페이지에 대 한 링크는 매개 변수를 전달 해야 합니다. 따라서 세 개의 매개 변수를 사용 하는 Html.

- 1. 장르 이름을 표시 하는 링크 텍스트
- 2. 컨트롤러 작업 이름 (찾아보기)
- 3. 이름 (장르) 및 값 (장르 이름)을 모두 지정 하는 경로 매개 변수 값

이를 모두 함께 저장 하면 다음은 저장소 인덱스 보기에 이러한 링크를 작성 하는 방법입니다.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

이제 프로젝트를 다시 실행 하 고/Svv/URL에 액세스할 때 장르 목록이 표시 됩니다. 각 장르는 하이퍼링크입니다. 클릭 하면/Dl/whhhhs? 장르 = *[장르]* URL로 이동 합니다.

![](mvc-music-store-part-3/_static/image3.jpg)

장르 목록의 HTML은 다음과 같습니다.

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-2.md)
> [다음](mvc-music-store-part-4.md)
