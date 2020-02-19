---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 컨트롤러 추가 | Microsoft Docs
author: Rick-Anderson
description: 참고:이 자습서의 업데이트 된 버전은 ASP.NET MVC 5 및 Visual Studio 2013를 사용 하는 여기에서 사용할 수 있습니다. 보다 안전 하 고, 보다 간단 하 고 데모를 수행 하는 것이 더 간단 합니다.
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f528c56435976c7f31fce453c834ef9eaebe6244
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456104"
---
# <a name="adding-a-controller"></a>컨트롤러 추가

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../getting-started/introduction/getting-started.md) 더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.

MVC는 *모델-뷰-컨트롤러*를 나타냅니다. MVC는 잘 설계 되 고, 테스트 가능 하 고, 유지 관리 하기 쉬운 응용 프로그램을 개발 하기 위한 패턴입니다. MVC 기반 응용 프로그램에는 다음이 포함 됩니다.

- **M** odels: 응용 프로그램의 데이터를 나타내고 유효성 검사 논리를 사용 하 여 해당 데이터에 대 한 비즈니스 규칙을 적용 하는 클래스입니다.
- **V** iews: 응용 프로그램에서 HTML 응답을 동적으로 생성 하는 데 사용 하는 템플릿 파일입니다.
- **C** ontrollers: 들어오는 브라우저 요청을 처리 하 고, 모델 데이터를 검색 하 고, 브라우저에 응답을 반환 하는 보기 템플릿을 지정 하는 클래스입니다.

Microsoft는이 자습서 시리즈의 모든 개념을 다루며 응용 프로그램을 빌드하는 데 사용 하는 방법을 보여 줍니다.

먼저 컨트롤러 클래스를 만들어 보겠습니다. **솔루션 탐색기**에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **컨트롤러 추가**를 선택 합니다.

![](adding-a-controller/_static/image1.png)

새 컨트롤러의 이름을 HelloWorldController&quot;로 &quot;합니다. 기본 템플릿을 **빈 MVC 컨트롤러로** 그대로 두고 **추가**를 클릭 합니다.

![컨트롤러 추가](adding-a-controller/_static/image2.png)

*HelloWorldController.cs*라는 새 파일이 생성 **솔루션 탐색기** 합니다. 파일이 IDE에 열려 있습니다.

![](adding-a-controller/_static/image3.png)

파일 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

컨트롤러 메서드는 HTML 문자열을 예제로 반환 합니다. 컨트롤러는 `HelloWorldController` 이름이 지정 되 고 위의 첫 번째 메서드는 `Index`으로 이름이 지정 됩니다. 브라우저에서 호출 해 보겠습니다. F5 키 또는 Ctrl + F5 키를 눌러 응용 프로그램을 실행 합니다. 브라우저에서 주소 표시줄의 경로에 &quot;HelloWorld&quot;를 추가 합니다. (예를 들어 아래 그림에서는 `http://localhost:1234/HelloWorld.`) 브라우저의 페이지는 다음 스크린샷 처럼 표시 됩니다. 위의 메서드에서 코드는 문자열을 직접 반환 했습니다. 일부 HTML만 반환 하도록 시스템에 지시 했습니다.

![](adding-a-controller/_static/image4.png)

ASP.NET MVC는 들어오는 URL에 따라 서로 다른 컨트롤러 클래스 (및 그 안의 다른 작업 메서드)를 호출 합니다. ASP.NET MVC에서 사용 하는 기본 URL 라우팅 논리는 다음과 같은 형식을 사용 하 여 호출할 코드를 결정 합니다.

`/[Controller]/[ActionName]/[Parameters]`

URL의 첫 번째 부분은 실행할 컨트롤러 클래스를 결정 합니다. 따라서 */HelloWorld* 는 `HelloWorldController` 클래스에 매핑됩니다. URL의 두 번째 부분은 실행할 클래스에 대 한 작업 메서드를 결정 합니다. 따라서 */HelloWorld/Index* 을 실행 하면 `HelloWorldController` 클래스의 `Index` 메서드가 실행 될 수 있습니다. */Helloworld* 로 이동 하기만 하면 `Index` 메서드가 기본적으로 사용 되었습니다. 이는 `Index` 라는 메서드가 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 메서드 이기 때문입니다.

[https://www.microsoft.com]\(`http://localhost:xxxx/HelloWorld/Welcome`) 로 이동합니다. `Welcome` 메서드는 시작 작업 메서드인 &quot;문자열을 실행 하 고&quot;반환 합니다. 기본 MVC 매핑은 `/[Controller]/[ActionName]/[Parameters]`입니다. 이 URL의 경우 컨트롤러는 `HelloWorld`이고 `Welcome`이 작업 메서드입니다. 아직 URL의 `[Parameters]` 부분을 사용하지 않았습니다.

![](adding-a-controller/_static/image5.png)

URL의 일부 매개 변수 정보를 컨트롤러에 전달할 수 있도록 예제를 약간 수정 하겠습니다 (예: */HelloWorld/Welcome? name = Scott&amp;numtimes = 4*). 아래와 같이 두 개의 매개 변수를 포함 하도록 `Welcome` 메서드를 변경 합니다. 이 코드는 C# 선택적 매개 변수 기능을 사용 하 여 해당 매개 변수에 대해 전달 된 값이 없는 경우 `numTimes` 매개 변수를 기본값 1로 지정 합니다.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

응용 프로그램을 실행 하 고 예제 URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`로 이동 합니다. URL에서 `name` 및 `numtimes`에 다른 값을 사용할 수 있습니다. [ASP.NET MVC 모델 바인딩 시스템](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) 은 주소 표시줄의 쿼리 문자열에서 명명 된 매개 변수를 메서드의 매개 변수에 자동으로 매핑합니다.

![](adding-a-controller/_static/image6.png)

이러한 두 예제에서 컨트롤러는 MVC의 &quot;VC&quot; 부분을 수행 했습니다. 즉, 뷰 및 컨트롤러가 작동 합니다. 컨트롤러가 HTML을 직접 반환하고 있습니다. 일반적으로 컨트롤러는 코드를 매우 복잡 하 게 하기 때문에 HTML을 직접 반환 하는 것을 원하지 않습니다. 대신 일반적으로 별도의 뷰 템플릿 파일을 사용 하 여 HTML 응답을 생성 합니다. 이 작업을 수행 하는 방법에 대해 알아보겠습니다.

> [!div class="step-by-step"]
> [이전](intro-to-aspnet-mvc-4.md)
> [다음](adding-a-view.md)
