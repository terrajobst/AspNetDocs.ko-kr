---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 컨트롤러 추가 | Microsoft Docs
author: shanselman
description: Visual Studio 2013를 사용 하 여이 자습서를 사용할 수 있는 경우 업데이트 된 버전입니다. 새 자습서에서는 ASP.NET MVC 5를 사용 하 여 여러 가지 향상 된 기능을 제공 합니다.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437567"
---
# <a name="adding-a-controller"></a>컨트롤러 추가

[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)를 [사용 하 여](../../getting-started/introduction/getting-started.md) 이 자습서를 사용할 수 있는 경우 업데이트 된 버전입니다. 새 자습서에서는이 자습서를 통해 많은 향상 된 기능을 제공 하는 ASP.NET MVC 5를 사용 합니다.
>
>
> ASP.NET MVC의 기본 사항을 소개 하는 초보자를 위한 자습서입니다. 데이터베이스에서 읽고 쓰는 간단한 웹 응용 프로그램을 만듭니다. [ASP.NET mvc 학습 센터](../../../index.md) 를 방문 하 여 다른 ASP.NET mvc 자습서 및 샘플을 찾습니다.

MVC는 모델, 뷰, 컨트롤러를 나타냅니다. MVC는 응용 프로그램을 개발 하는 패턴으로, 각 파트에는 다른 책임이 있습니다.

- Model: 응용 프로그램의 데이터
- 보기: 응용 프로그램에서 HTML 응답을 동적으로 생성 하는 데 사용 하는 템플릿 파일입니다.
- 컨트롤러: 응용 프로그램에 대 한 들어오는 URL 요청을 처리 하 고, 모델 데이터를 검색 한 후 클라이언트에 응답을 다시 렌더링 하는 뷰 템플릿을 지정 하는 클래스입니다.

이 자습서에서는 이러한 모든 개념을 설명 하 고 응용 프로그램을 빌드하는 데 사용 하는 방법을 보여 줍니다.

솔루션 탐색기에서 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 컨트롤러 추가를 선택 하 여 새 컨트롤러를 만들어 보겠습니다.

[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)

새 컨트롤러의 이름을 "HelloWorldController"로 하 고 추가를 클릭 합니다.

[![컨트롤러 추가 대화 상자](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)

솔루션 탐색기에서 HelloWorldController.cs 라는 새 파일이 생성 되었으며 해당 파일이 이제 **IDE**에서 열려 있음을 확인 합니다.

[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)

새 public 클래스 HelloWorldController 내에서 다음과 같은 두 개의 새로운 메서드를 만듭니다. 예를 들어 컨트롤러에서 직접 HTML 문자열을 반환 합니다.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

컨트롤러 이름이 HelloWorldController이 고 새 메서드를 Index 라고 합니다. 이전과 마찬가지로 응용 프로그램을 다시 실행 합니다. 재생 단추를 클릭 하거나 F5 키를 눌러이 작업을 수행 합니다. 브라우저가 시작 되 면 주소 표시줄의 경로를 `http://localhost:xx/HelloWorld`로 변경 합니다. 여기서 xx는 컴퓨터에서 선택한 숫자입니다. 이제 브라우저가 아래 스크린샷 처럼 보입니다. 위의 메서드에서는 "Content" 라는 메서드에 전달 된 문자열을 반환 했습니다. 시스템이 몇 가지 HTML을 반환 하는 것입니다.

ASP.NET MVC는 들어오는 URL에 따라 서로 다른 컨트롤러 클래스 (및 그 안의 다른 작업 메서드)를 호출 합니다. ASP.NET MVC에서 사용 하는 기본 매핑 논리는 다음과 같은 형식을 사용 하 여 실행 되는 코드를 제어 합니다.

/[Controller]/[ActionName]/[Parameters]

URL의 첫 번째 부분은 실행할 컨트롤러 클래스를 결정 합니다. 그러면/HelloWorld가 HelloWorldController 클래스에 매핑됩니다. URL의 두 번째 부분은 실행할 클래스에 대 한 작업 메서드를 결정 합니다. 따라서/HelloWorld/Index는 HelloWorldController 클래스의 Index () 메서드를 실행 합니다. 위의/HelloWorld를 방문 하기만 하면 메서드 인덱스가 암시 됩니다. 이는 "Index" 라는 메서드가 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 메서드 이기 때문입니다.

[기본 작업 ![](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)

이제 환영 메서드가 실행 되어 해당 HTML 문자열을 반환 하는 `http://localhost:xx/HelloWorld/Welcome.`를 방문해 보겠습니다.

다시,/[Controller]/[ActionName]/[Parameters]를 다시 한 번, 컨트롤러는 HelloWorld 이며이 경우에는 환영입니다. 매개 변수를 아직 수행 하지 않았습니다.

[시작 작업 방법 ![](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)

URL에서 컨트롤러로 일부 정보를 전달할 수 있도록 샘플을 약간 수정 하겠습니다. 예를 들어/HelloWorld/Welcome? name = Scott&amp;numtimes = 4와 같습니다. 두 개의 매개 변수를 포함 하도록 환영 메서드를 변경 하 고 아래와 같이 업데이트 합니다. C# 선택적 매개 변수 기능을 사용 하 여 numtimes 매개 변수가 전달 되지 않은 경우 기본값을 1로 지정 해야 함을 지정 했습니다.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

응용 프로그램을 실행 하 고 이름 및 numtimes 값을 원하는 대로 변경 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`를 방문 합니다. 시스템은 주소 표시줄의 쿼리 문자열에서 메서드의 매개 변수로 명명 된 매개 변수를 자동으로 매핑합니다.

두 예제 모두에서 컨트롤러는 모든 작업을 수행 하 고 HTML을 직접 반환 했습니다. 일반적으로 컨트롤러에서 HTML을 직접 반환 하는 것을 원하지 않습니다 .이는 코드를 매우 복잡 하 게 종료 하기 때문입니다. 대신 일반적으로 별도의 뷰 템플릿 파일을 사용 하 여 HTML 응답을 생성 합니다. 이 작업을 수행 하는 방법을 살펴보겠습니다. 브라우저를 닫고 IDE로 돌아갑니다.

> [!div class="step-by-step"]
> [이전](getting-started-with-mvc-part1.md)
> [다음](getting-started-with-mvc-part3.md)
