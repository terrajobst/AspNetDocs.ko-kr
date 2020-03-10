---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: '2 부: 컨트롤러 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 2 부에서는 컨트롤러를 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78451193"
---
# <a name="part-2-controllers"></a>2 부: 컨트롤러

받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.  
>   
> MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 2 부에서는 컨트롤러를 다룹니다.

기존 웹 프레임 워크를 사용 하는 경우 들어오는 Url은 일반적으로 디스크의 파일에 매핑됩니다. 예: "/Products.aspx" 또는 "/Products.php"와 같은 URL에 대 한 요청은 "" 또는 "" 파일에 의해 처리 될 수 있습니다.

웹 기반 MVC 프레임 워크는 Url을 서버 코드에 약간 다른 방식으로 매핑합니다. 들어오는 Url을 파일에 매핑하는 대신, 해당 url을 클래스의 메서드에 매핑합니다. 이러한 클래스를 "컨트롤러" 라고 하며, 들어오는 HTTP 요청을 처리 하 고, 사용자 입력을 처리 하 고, 데이터를 검색 및 저장 하 고, 클라이언트로 다시 보낼 응답을 결정 합니다 (HTML 표시, 파일 다운로드, 다른 위치로 리디렉션). URL 등).

## <a name="adding-a-homecontroller"></a>HomeController 추가

사이트의 홈 페이지에 대 한 Url을 처리 하는 컨트롤러 클래스를 추가 하 여 MVC Music Store 응용 프로그램을 시작 합니다. ASP.NET MVC의 기본 명명 규칙을 따르고 HomeController를 호출 합니다.

솔루션 탐색기 내의 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "추가"를 선택 하 고 "컨트롤러 ..."를 선택 합니다. 명령

![](mvc-music-store-part-2/_static/image1.jpg)

그러면 "컨트롤러 추가" 대화 상자가 표시 됩니다. 컨트롤러 이름을 "HomeController"로 하 고 추가 단추를 누릅니다.

![](mvc-music-store-part-2/_static/image1.png)

그러면 다음 코드를 사용 하 여 새 파일인 HomeController.cs가 만들어집니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

가능한 한 간단 하 게 시작 하려면 Index 메서드를 단순히 문자열만 반환 하는 간단한 메서드로 바꿉니다. 다음 두 가지 변경 작업을 수행 합니다.

- 메서드를 변경 하 여 ActionResult 대신 문자열 반환
- Return 문을 변경 하 여 "Hello from Home"을 반환 합니다.

이제 메서드는 다음과 같습니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a>응용 프로그램 실행

이제 사이트를 실행 해 보겠습니다. 웹 서버를 시작 하 고 다음 중 하나를 사용 하 여 사이트를 사용해 볼 수 있습니다.

- 디버그 ⇨ 디버깅 시작 메뉴 항목을 선택 합니다.
- 도구 모음에서 녹색 화살표 단추를 클릭 ![](mvc-music-store-part-2/_static/image2.jpg)
- 키보드 바로 가기 인 F5 키를 사용 합니다.

위의 단계를 사용 하 여 프로젝트를 컴파일한 다음 Visual Web Developer에 기본 제공 되는 ASP.NET 개발 서버를 시작 합니다. 화면 하단에 ASP.NET 개발 서버 시작 됨을 나타내는 알림이 표시 되 고 실행 중인 포트 번호가 표시 됩니다 ().

![](mvc-music-store-part-2/_static/image2.png)

그러면 Visual Web Developer에서 웹 서버를 가리키는 URL이 있는 브라우저 창을 자동으로 엽니다. 이렇게 하면 웹 응용 프로그램을 빠르게 사용해 볼 수 있습니다.

![](mvc-music-store-part-2/_static/image3.png)

괜찮습니다 .이는 새로운 웹 사이트를 만들고, 세 개의 선 함수를 추가 했으며, 브라우저에서 텍스트를 얻었습니다. 로켓 과학은 아니지만 시작입니다.

*참고: Visual Web Developer에는 웹 사이트를 실행 하는 ASP.NET 개발 서버 포함 되어 있습니다. 위의 스크린샷에는 사이트가 `http://localhost:26641/`에서 실행 되므로 포트 26641를 사용 합니다. 포트 번호는 다를 수 있습니다. 이 자습서에서 URL과 같은 URL의 예를 보면 포트 번호 다음에 표시 됩니다. 포트 번호가 26641 인 것으로 가정 하 고/Sv/svto 찾아보기로 이동 하면 `http://localhost:26641/Store/Browse`검색을 의미 합니다.*

## <a name="adding-a-storecontroller"></a>StoreController 추가

사이트의 홈 페이지를 구현 하는 간단한 HomeController를 추가 했습니다. 이제 music store의 검색 기능을 구현 하는 데 사용할 다른 컨트롤러를 추가 해 보겠습니다. 저장소 컨트롤러는 세 가지 시나리오를 지원 합니다.

- Music store의 음악 장르 목록 페이지
- 특정 장르의 모든 음악 앨범을 나열 하는 찾아보기 페이지
- 특정 음악 앨범에 대 한 정보를 표시 하는 세부 정보 페이지

새 StoreController 클래스를 추가 하 여 시작 합니다. 아직 실행 하지 않은 경우 브라우저를 닫거나 디버그 ⇨ 디버깅 중지 메뉴 항목을 선택 하 여 응용 프로그램 실행을 중지 합니다.

이제 새 StoreController를 추가 합니다. HomeController를 사용 하는 것 처럼 솔루션 탐색기 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 하 고 추가&gt;컨트롤러 메뉴 항목을 선택 하 여이 작업을 수행 합니다.

![](mvc-music-store-part-2/_static/image4.png)

새 StoreController에는 이미 "Index" 메서드가 있습니다. 이 "인덱스" 메서드를 사용 하 여 음악 스토어의 모든 장르를 나열 하는 목록 페이지를 구현 합니다. 또한 StoreController에서 처리할 두 가지 다른 시나리오를 구현 하는 두 가지 메서드를 더 추가 하 여 찾아보기 및 세부 정보를 제공 합니다.

컨트롤러 내에서 이러한 메서드 (인덱스, 찾아보기 및 세부 정보)를 "컨트롤러 작업" 이라고 하며, 이미 HomeController () 작업 메서드를 사용 하는 경우 URL 요청에 응답 하 고 (일반적으로) 콘텐츠를 결정 하는 작업입니다. URL을 호출한 브라우저 또는 사용자에 게 다시 보내야 합니다.

Index () 메서드를 변경 하 여 "Hello from StoreController ()" 라는 문자열을 반환 하 고 Browse () 및 Details ()에 대해 비슷한 메서드를 추가 하 여 구현을 시작 합니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

프로젝트를 다시 실행 하 고 다음 Url을 찾아봅니다.

- /Store
- /Sver/찾아보기
- /Sv/ds/세부 정보

이러한 Url에 액세스 하면 컨트롤러 내에서 작업 메서드를 호출 하 고 문자열 응답을 반환 합니다.

![](mvc-music-store-part-2/_static/image5.png)

매우 유용 하지만 상수 문자열입니다. 동적으로 만들어 URL에서 정보를 가져와 페이지 출력에 표시 합니다.

먼저 찾아보기 동작 메서드를 변경 하 여 URL에서 querystring 값을 검색 합니다. 작업 메서드에 "장르" 매개 변수를 추가 하 여이 작업을 수행할 수 있습니다. 이 작업을 수행 하면 ASP.NET MVC가 호출 될 때 작업 메서드에 "장르" 라는 쿼리 문자열 또는 폼 게시 매개 변수를 자동으로 전달 합니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*참고: HtmlEncode 유틸리티 메서드를 사용 하 여 사용자 입력을 삭제 합니다. 이를 통해 사용자는/Vv/dher>와 같은 링크를 사용 하 여 Javascript를 뷰에 삽입할 수 없습니다. 장르 =&lt;스크립트&gt;창. location = 'http://hackersite.com'&lt;/script&gt;.*

이제/Dv>로 이동 하겠습니다. 장르 = Disco

![](mvc-music-store-part-2/_static/image6.png)

다음으로 자세히 작업을 변경 하 여 ID 라는 입력 매개 변수를 읽고 표시 합니다. 이전 메서드와 달리 ID 값을 querystring 매개 변수로 포함 하지 않습니다. 대신 URL 자체에 직접 포함 합니다. 예:/Store/Details/5.

ASP.NET MVC를 사용 하면 아무것도 구성 하지 않고도이 작업을 쉽게 수행할 수 있습니다. ASP.NET MVC의 기본 라우팅 규칙은 작업 메서드 이름 뒤에 있는 URL의 세그먼트를 "ID" 라는 매개 변수로 처리 하는 것입니다. 작업 메서드에 ID 라는 매개 변수가 있는 경우 ASP.NET MVC는 자동으로 URL 세그먼트를 매개 변수로 사용자에 게 전달 합니다.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

응용 프로그램을 실행 하 고/Store/Details/5로 이동 합니다.

![](mvc-music-store-part-2/_static/image7.png)

지금까지 수행한 작업을 간략하게 살펴보겠습니다.

- Visual Web Developer에서 새로운 ASP.NET MVC 프로젝트를 만들었습니다.
- ASP.NET MVC 응용 프로그램의 기본 폴더 구조에 대해 설명 했습니다.
- ASP.NET 개발 서버를 사용 하 여 웹 사이트를 실행 하는 방법을 알아보았습니다.
- HomeController 및 StoreController 라는 두 개의 컨트롤러 클래스를 만들었습니다.
- URL 요청에 응답 하 고 브라우저에 텍스트를 반환 하는 작업 메서드를 컨트롤러에 추가 했습니다.

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-1.md)
> [다음](mvc-music-store-part-3.md)
