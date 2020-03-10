---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: 컨트롤러 추가 (VB) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e77f62a9796211b0e59a99c71bc532659b7cb92
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434597"
---
# <a name="adding-a-controller-vb"></a>컨트롤러 추가(VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.
> 
> VB.NET 소스 코드를 사용 하는 Visual Web Developer 프로젝트를이 항목과 함께 사용할 수 있습니다. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 선호 C#하는 경우이 자습서의 [ C# 버전](../cs/adding-a-controller.md) 으로 전환 합니다.

MVC는 *모델-뷰-컨트롤러*를 나타냅니다. MVC는 응용 프로그램을 개발 하기 위한 패턴으로, 각 부분에 별도의 책임이 있습니다.

- Model: 응용 프로그램에 대 한 데이터입니다.
- 보기: 응용 프로그램에서 HTML 응답을 동적으로 생성 하는 데 사용 하는 템플릿 파일입니다.
- 컨트롤러: 응용 프로그램에 대 한 들어오는 URL 요청을 처리 하 고 모델 데이터를 검색 한 다음 클라이언트에 응답을 렌더링 하는 뷰 템플릿을 지정 하는 클래스입니다.

이 자습서에서는 이러한 모든 개념을 설명 하 고 응용 프로그램을 빌드하는 데 사용 하는 방법을 보여 줍니다.

**솔루션 탐색기** 의 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **컨트롤러 추가**를 선택 하 여 새 컨트롤러를 만듭니다.

[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)

새 컨트롤러의 이름을 HelloWorldController&quot;로 &quot;하 고 **추가**를 클릭 합니다.

[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)

*HelloWorldController.cs* 라는 이름으로 새 파일이 생성 되 고 파일이 IDE에 열려 있음을 **솔루션 탐색기** 에서 확인 합니다.

새 `public class HelloWorldController` 블록 내에서 다음 코드와 같은 두 개의 새 메서드를 만듭니다. 예를 들어 컨트롤러에서 직접 HTML 문자열을 반환 합니다.

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

컨트롤러의 이름은 `HelloWorldController`이 고 새 메서드의 이름은 `Index`입니다. F5 키 또는 Ctrl + F5 키를 눌러 응용 프로그램을 실행 합니다. 브라우저가 시작 되 면 주소 표시줄의 경로에 &quot;HelloWorld&quot;를 추가 합니다. (내 컴퓨터에 `http://localhost:43246/HelloWorld`) 브라우저는 아래 스크린샷 처럼 보입니다. 위의 메서드에서 코드는 문자열을 직접 반환 했습니다. 일부 HTML만 반환 하도록 시스템에 지시 했습니다.

![](adding-a-controller/_static/image5.png)

ASP.NET MVC는 들어오는 URL에 따라 서로 다른 컨트롤러 클래스 (및 그 안의 다른 작업 메서드)를 호출 합니다. ASP.NET MVC에서 사용 하는 기본 매핑 논리는 다음과 같은 형식을 사용 하 여 호출 되는 코드를 제어 합니다.

`/[Controller]/[ActionName]/[Parameters]`

URL의 첫 번째 부분은 실행할 컨트롤러 클래스를 결정 합니다. 따라서 */HelloWorld* 는 `HelloWorldController` 클래스에 매핑됩니다. URL의 두 번째 부분은 실행할 클래스에 대 한 작업 메서드를 결정 합니다. 따라서 */HelloWorld/Index* 을 실행 하면 `HelloWorldController` 클래스의 `Index` 메서드가 실행 될 수 있습니다. 위의 */Helloworld* 를 방문 하 고 `Index` 메서드를 기본적으로 사용 했습니다. 이는 `Index` 라는 메서드가 명시적으로 지정 되지 않은 경우 컨트롤러에서 호출 되는 기본 메서드 이기 때문입니다.

[https://www.microsoft.com]\(`http://localhost:xxxx/HelloWorld/Welcome`) 로 이동합니다. `Welcome` 메서드는 시작 작업 메서드인 &quot;문자열을 실행 하 고&quot;반환 합니다. 기본 MVC 매핑은 `/[Controller]/[ActionName]/[Parameters]`입니다. 이 URL의 경우 컨트롤러는 `HelloWorld` 되며 `Welcome` 메서드입니다. 아직 URL의 `[Parameters]` 부분을 사용 하지 않았습니다.

![](adding-a-controller/_static/image6.png)

URL의 일부 매개 변수 정보를 컨트롤러에 전달할 수 있도록 예제를 약간 수정 하겠습니다 (예: */HelloWorld/Welcome? name = Scott&amp;numtimes = 4*). 아래와 같이 두 개의 매개 변수를 포함 하도록 `Welcome` 메서드를 변경 합니다. VB 선택적 매개 변수 기능을 사용 하 여 해당 매개 변수에 대 한 값이 전달 되지 않는 경우 `numTimes` 매개 변수를 기본값 1로 지정 해야 합니다.

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

응용 프로그램을 실행 하 고 `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`로 이동 **합니다.** `name` 및 `numtimes`에 대해 다른 값을 사용해 볼 수 있습니다. 시스템은 주소 표시줄의 쿼리 문자열에 있는 명명 된 매개 변수를 메서드의 매개 변수에 자동으로 매핑합니다.

![](adding-a-controller/_static/image7.png)

이러한 두 예제에서 컨트롤러는 MVC의 VC 부분을 수행 하 고 있으며,이는 뷰 및 컨트롤러 작업입니다. 컨트롤러가 HTML을 직접 반환하고 있습니다. 일반적으로는 코드가 매우 복잡 해지기 때문에 컨트롤러에서 HTML을 직접 반환 하지 않습니다. 대신 일반적으로 별도의 뷰 템플릿 파일을 사용 하 여 HTML 응답을 생성 합니다. 이 작업을 수행 하는 방법을 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](intro-to-aspnet-mvc-3.md)
> [다음](adding-a-view.md)
