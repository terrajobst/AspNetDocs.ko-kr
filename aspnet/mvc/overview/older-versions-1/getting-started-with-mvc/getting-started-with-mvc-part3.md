---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 뷰 추가 | Microsoft Docs
author: shanselman
description: ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469775"
---
# <a name="adding-a-view"></a>보기 추가

[Scott Hanselman](https://github.com/shanselman)

> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다. [ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.

이 섹션에서는 HelloWorldController 클래스에서 뷰 템플릿 파일을 사용 하 여 클라이언트에 대 한 HTML 응답 생성을 완전히 캡슐화 하는 방법을 살펴보겠습니다.

인덱스 메서드와 함께 뷰 템플릿을 사용 하 여 시작 해 보겠습니다. 이 메서드는 인덱스 라고 하 고 HelloWorldController에 있습니다. 현재 Index () 메서드는 Controller 클래스 내에서 하드 코드 된 메시지를 포함 하는 문자열을 반환 합니다.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

이제 다음과 같이 인덱스 메서드를 변경 하겠습니다.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

이제 Index () 메서드에 사용할 수 있는 뷰 템플릿을 프로젝트에 추가 해 보겠습니다. 이렇게 하려면 인덱스 메서드 가운데에 마우스를 놓고 마우스 오른쪽 단추를 클릭 한 다음 보기 추가 ...를 클릭 합니다.

![이미지](getting-started-with-mvc-part3/_static/image1.png)

그러면 인덱스 메서드에서 사용할 수 있는 보기 템플릿을 만드는 방법에 대 한 몇 가지 옵션을 제공 하는 "뷰 추가" 대화 상자가 표시 됩니다. 지금은 아무것도 변경 하지 말고 추가 단추를 클릭 하면 됩니다.

[뷰 추가 ![대화 상자](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)

추가를 클릭 하면 여기에 표시 된 것 처럼 새 폴더와 새 파일이 솔루션 폴더에 표시 됩니다. 이제 보기 아래에 HelloWorld 폴더와 해당 폴더 안에 있는 인덱스 .aspx 파일이 있습니다.

[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)

새 인덱스 파일도 이미 열려 있으며 편집할 준비가 되었습니다. "Hello World"와 같이 첫 번째 &lt;h2&gt;인덱스&lt;/h 2&gt;에 일부 텍스트를 추가 합니다.

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

응용 프로그램을 실행 하 고 브라우저에서 [`http://localhost:xx/HelloWorld`](http://localhostxx) 를 다시 방문 하세요. 이 예에서 컨트롤러의 인덱스 메서드는 아무 작업을 수행 하지 않았지만 뷰 템플릿 파일을 사용 하 여 클라이언트에 응답을 다시 렌더링 하도록 지정 하는 "return 뷰 ()"를 호출 했습니다. 사용할 뷰 템플릿 파일의 이름을 명시적으로 지정 하지 않았기 때문에 ASP.NET MVC는 \Views\HelloWorld 폴더에 있는 파일을 사용 하 여 기본적으로 사용 됩니다. 이제 보기에 하드 코딩 된 문자열이 표시 됩니다.

[인덱스 ![-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)

매우 유용 합니다. 그러나 브라우저의 제목은 "인덱스"로 표시 되 고 페이지의 큰 제목은 "내 MVC 응용 프로그램" 이라고 표시 됩니다. 이러한 변경 내용을 살펴보겠습니다.

### <a name="changing-views-and-master-pages"></a>보기 및 마스터 페이지 변경

먼저 "내 MVC 응용 프로그램" 텍스트를 변경 하겠습니다. 이 텍스트는 공유 되 고 모든 페이지에 표시 됩니다. 실제로는 응용 프로그램의 모든 페이지에 있더라도 코드의 한 곳에만 표시 됩니다. 솔루션 탐색기의/Views/Shared 폴더로 이동 하 여 사이트 .Master 파일을 엽니다. 이 파일을 마스터 페이지 라고 하며 다른 모든 페이지에서 사용 하는 공유 "셸"입니다.

이 파일에는 ContentPlaceholder "MainContent" 라는 텍스트가 표시 됩니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

이 자리 표시자는 만든 모든 페이지가 마스터 페이지에 표시 되는 "래핑된" 위치입니다. 제목을 변경 하 고 앱을 실행 하 고 여러 페이지를 방문 하세요. 단일 변경 내용이 여러 페이지에 표시 되는 것을 알 수 있습니다.

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

이제 모든 페이지에 기본 제목이 있습니다. 여기에는 "내 MVC 영화 응용 프로그램"의 H1이 포함 됩니다. 위쪽에 있는 흰색 텍스트를 처리 하 고 모든 페이지에서 공유 됩니다.

변경 된 제목이 있는 Site.master는 다음과 같습니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

이제 인덱스 페이지의 제목을 변경 하겠습니다.

/HelloWorld/Index.aspx. 열기 변경 해야 하는 두 가지 위치가 있습니다. 먼저 브라우저 제목에 표시 되는 제목을 표시 한 다음 보조 헤더 (H2)도 표시 합니다. 앱의 일부를 변경 하는 코드의 비트를 확인할 수 있도록 각각 약간씩 다르게 만듭니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

앱을 실행 하 고/Movies.를 방문 합니다. 브라우저 제목, 주 머리글 및 보조 머리글이 변경 되었습니다. 보기를 약간만 변경 하 여 앱에서 큰 변경 작업을 쉽게 수행할 수 있습니다.

[![동영상 목록-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)

약간 약간의 "데이터" (이 경우 "Hello World!" 메시지)가 하드 코딩 되었습니다. V (뷰)가 있지만 C (컨트롤러)가 있지만 M (모델)은 아직 없습니다. 데이터베이스를 만들고 모델 데이터를 검색 하는 방법을 곧 살펴보겠습니다.

## <a name="passing-a-viewmodel"></a>ViewModel 전달

데이터베이스로 이동 하 여 모델에 대해 설명 하기 전에 먼저 "ViewModels"에 대해 알아보겠습니다. 이러한 개체는 뷰 템플릿이 클라이언트에 게 다시 HTML 응답을 렌더링 하는 데 필요한 항목을 나타냅니다. 일반적으로이 클래스는 컨트롤러 클래스에 의해 생성 되 고 뷰 템플릿에 전달 되며 뷰 템플릿에 필요한 데이터만 포함 해야 합니다.

이전에는 HelloWorld 샘플을 통해 환영 () 동작 메서드는 이름 및 numTimes 매개 변수를 사용 하 여 브라우저에 출력 합니다. 컨트롤러에서이 응답을 계속 직접 렌더링 하는 대신 해당 데이터를 저장 하는 작은 클래스를 만든 다음 뷰 템플릿에 전달 하 여 HTML 응답을 다시 렌더링 해 보겠습니다. 이러한 방식으로 컨트롤러는 응용 프로그램 내에서 문제를 명확 하 게 분리 하는 "문제를 해결 하는 데 도움이 됩니다.

HelloWorldController.cs 파일로 돌아가서 새 "WelcomeViewModel" 클래스를 추가 하 고 컨트롤러 내에서 시작 메서드를 변경 합니다. 다음은 동일한 파일에 새 클래스를 사용 하는 전체 HelloWorldController.cs입니다.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

여러 줄에 있는 경우에도 환영 메서드는 사실 두 개의 코드 문입니다. 첫 번째 문은 두 개의 매개 변수를 ViewModel 개체에 패키지 하 고, 두 번째 문은 결과 개체를 뷰에 전달 합니다.

이제 시작 보기 템플릿이 필요 합니다. 시작 메서드를 마우스 오른쪽 단추로 클릭 하 고 뷰 추가를 선택 합니다. 이번에는 "강력한 형식의 뷰 만들기"를 선택 하 고 드롭다운 목록에서 WelcomeViewModel 클래스를 선택 합니다. 이 새 뷰는 WelcomeViewModels 및 다른 유형의 개체는 인식 하지 못합니다.

> *참고: 드롭다운 목록에 표시 되는 WelcomeViewModel를 추가한 후 한 번 컴파일해야 합니다.*

보기 추가 대화 상자는 다음과 같습니다. 추가 단추를 클릭합니다. ![원 원으로 표시 되는 추가](getting-started-with-mvc-part3/_static/image10.png)

새 시작 .aspx의 &lt;h2&gt;에이 코드를 추가 합니다. 사용자에 게 표시 되는 횟수 만큼 루프와 Hello를 만들어 보겠습니다.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

또한 아래 스크린샷에 표시 된 것 처럼 모델 개체를 참조할 때마다 유용한 Intellisense를 제공 하기 위해 WelcomeViewModel에 대 한 보기를 제공 하기 때문에 입력 하는 것이 좋습니다.

[![NumTime 소스 코드](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)

응용 프로그램을 실행 하 고 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`를 다시 방문 하세요. 이제 URL에서 데이터를 가져오고, 컨트롤러에 자동으로 전달 됩니다. 컨트롤러는 데이터를 ViewModel으로 패키지 하 고 해당 개체를 보기에 전달 합니다. 보기는 사용자에 게 데이터를 HTML로 표시 합니다.

[![시작-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)

모델에 대 한 일종의 "M" 이지만 데이터베이스 종류는 아닙니다. 학습 한 내용을 살펴보고 영화 데이터베이스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part2.md)
> [다음](getting-started-with-mvc-part4.md)
