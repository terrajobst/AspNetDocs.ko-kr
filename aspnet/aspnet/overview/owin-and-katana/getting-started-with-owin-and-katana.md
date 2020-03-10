---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: OWIN 및 Katana 시작 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78472445"
---
# <a name="getting-started-with-owin-and-katana"></a>OWIN 및 Katana 시작

[Mike Wasson](https://github.com/MikeWasson)

[OWIN (Open Web Interface for .net)](http://owin.org/) 는 .net 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다. 웹 서버를 응용 프로그램에서 분리 하면 OWIN를 사용 하 여 .NET 웹 개발용 미들웨어를 보다 쉽게 만들 수 있습니다. 또한 OWIN를 사용 하면 웹 응용 프로그램을 다른 호스트로&#8212;더 쉽게 이식할 수 있습니다. 예를 들어 Windows 서비스 또는 기타 프로세스에서 자체 호스팅을 수행할 수 있습니다.

OWIN는 구현이 아니라 커뮤니티 소유 사양입니다. Katana 프로젝트는 Microsoft에서 개발 된 오픈 소스 OWIN 구성 요소 집합입니다. OWIN 및 Katana에 대 한 일반적인 개요는 [Project Katana의 개요](an-overview-of-project-katana.md)를 참조 하세요. 이 문서에서는 시작 하는 코드를 바로 시작 합니다.

이 자습서에서는 [Visual Studio 2013 릴리스 후보](https://go.microsoft.com/fwlink/?LinkId=306566)를 사용 하지만 Visual Studio 2012을 사용할 수도 있습니다. 몇 가지 단계는 Visual Studio 2012에서 다릅니다 .이에 대 한 자세한 내용은 아래를 참조 하세요.

## <a name="host-owin-in-iis"></a>IIS의 호스트 OWIN

이 섹션에서는 IIS에서 OWIN를 호스팅합니다. 이 옵션을 사용 하면 OWIN 파이프라인의 유연성과 composability을 IIS의 완성 된 기능 집합과 함께 사용할 수 있습니다. 이 옵션을 사용 하면 OWIN 응용 프로그램이 ASP.NET 요청 파이프라인에서 실행 됩니다.

먼저 새 ASP.NET 웹 응용 프로그램 프로젝트를 만듭니다. Visual Studio 2012에서는 ASP.NET 빈 웹 응용 프로그램 프로젝트 형식을 사용 합니다.

![](getting-started-with-owin-and-katana/_static/image1.png)

**새 ASP.NET 프로젝트** 대화 상자에서 **빈** 템플릿을 선택 합니다.

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a>NuGet 패키지 추가

다음으로 필요한 NuGet 패키지를 추가 합니다. **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a>시작 클래스 추가

다음으로 OWIN startup 클래스를 추가 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **새 항목**을 선택 합니다. **새 항목 추가** 대화 상자에서 **Owin 시작 클래스**를 선택 합니다. Startup 클래스를 구성 하는 방법에 대 한 자세한 내용은 [OWIN Startup 클래스 검색](owin-startup-class-detection.md)을 참조 하세요.

![](getting-started-with-owin-and-katana/_static/image4.png)

`Startup1.Configuration` 메서드에 다음 코드를 추가합니다.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

이 코드는 OWIN 파이프라인에 간단한 미들웨어를 추가 합니다 .이는 **OWIN 컨텍스트** 인스턴스를 수신 하는 함수로 구현 됩니다. 서버에서 HTTP 요청을 받으면 OWIN 파이프라인은 미들웨어를 호출 합니다. 미들웨어는 응답의 콘텐츠 형식을 설정 하 고 응답 본문을 씁니다.

> [!NOTE]
> OWIN Startup 클래스 템플릿은 Visual Studio 2013에서 사용할 수 있습니다. Visual Studio 2012을 사용 하는 경우 `Startup1`라는 비어 있는 새 클래스를 추가 하 고 다음 코드를 붙여 넣습니다.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a>애플리케이션 실행

F5를 눌러 디버깅을 시작합니다. Visual Studio에서 `http://localhost:*port*/`하는 브라우저 창이 열립니다. 페이지는 다음과 같습니다.

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a>콘솔 응용 프로그램의 자체 호스트 OWIN

사용자 지정 프로세스에서이 응용 프로그램을 IIS 호스팅에서 자체 호스팅으로 쉽게 변환할 수 있습니다. Iis를 호스트 하는 경우 IIS는 HTTP 서버와 서비스를 호스팅하는 프로세스 역할을 모두 수행 합니다. 자체 호스팅을 사용 하 여 응용 프로그램은 프로세스를 만들고 **HttpListener** 클래스를 HTTP 서버로 사용 합니다.

Visual Studio에서 새 콘솔 애플리케이션을 만듭니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`Install-Package Microsoft.Owin.SelfHost -Pre`

이 자습서의 1 부에서 프로젝트에 `Startup1` 클래스를 추가 합니다. 이 클래스는 수정할 필요가 없습니다.

응용 프로그램의 `Main` 메서드를 다음과 같이 구현 합니다.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

콘솔 응용 프로그램을 실행 하면 서버가 `http://localhost:9000`수신 대기를 시작 합니다. 웹 브라우저에서이 주소로 이동 하면 "Hello 세계" 페이지가 표시 됩니다.

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a>OWIN 진단 추가

Owin 패키지에는 처리 되지 않은 예외를 catch 하 고 오류 세부 정보를 포함 하는 HTML 페이지가 표시 되는 미들웨어가 포함 되어 있습니다. 이 페이지는 ASP.NET 오류 페이지와 매우 유사 하 게 작동 합니다 .이는 "[주황색 화면 (죽음](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow))"이 라고도 합니다. Katana 오류 페이지는 YSOD 같이 개발 중에 유용 하지만 프로덕션 모드에서 사용 하지 않도록 설정 하는 것이 좋습니다.

프로젝트에 진단 패키지를 설치 하려면 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

`install-package Microsoft.Owin.Diagnostics –Pre`

`Startup1.Configuration` 메서드의 코드를 다음과 같이 변경 합니다.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

이제 CTRL + f 5를 사용 하 여 디버깅 하지 않고 응용 프로그램을 실행 하면 Visual Studio가 예외에서 중단 되지 않습니다. 응용 프로그램은 `http://localhost/fail`이동할 때까지 응용 프로그램에서 예외를 throw 하는 시점까지 이전과 동일 하 게 동작 합니다. 오류 페이지 미들웨어는 예외를 catch 하 고 오류에 대 한 정보를 포함 하는 HTML 페이지를 표시 합니다. 탭을 클릭 하 여 스택, 쿼리 문자열, 쿠키, 요청 헤더 및 OWIN 환경 변수를 볼 수 있습니다.

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a>다음 단계

- [OWIN 시작 클래스 검색](owin-startup-class-detection.md)
- [OWIN를 사용 하 여 자체 호스트 ASP.NET Web API](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [OWIN를 사용 하 여 자체 호스트 SignalR](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)
