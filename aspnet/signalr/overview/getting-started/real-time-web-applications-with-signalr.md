---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: '실습: SignalR를 사용 하는 실시간 웹 응용 프로그램 | Microsoft Docs'
author: bradygaster
description: 실시간 웹 응용 프로그램은 실시간으로 연결 된 클라이언트에 서버 쪽 콘텐츠를 푸시하는 기능을 제공 합니다. ASP.NET 개발자의 경우 ASP ....
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78431669"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a>실습: SignalR를 사용 하는 실시간 웹 응용 프로그램

[웹 캠프 팀](https://twitter.com/webcamps)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[웹 캠프 교육 키트, 2015 년 10 월 릴리스 다운로드](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> 실시간 웹 응용 프로그램은 실시간으로 연결 된 클라이언트에 서버 쪽 콘텐츠를 푸시하는 기능을 제공 합니다. ASP.NET 개발자의 경우 **ASP.NET SignalR** 는 응용 프로그램에 실시간 웹 기능을 추가 하는 라이브러리입니다. 클라이언트와 서버에서 사용할 수 있는 가장 적합 한 전송에 대해 자동으로 가장 적합 한 전송을 선택 하는 여러 전송을 활용 합니다. 이는 브라우저와 서버 간의 양방향 통신을 가능 하 게 하는 HTML5 API 인 **WebSocket**을 활용 합니다.
> 
> 또한 **SignalR** 는 ASP.NET 응용 프로그램에서 서버와 클라이언트 간 RPC를 수행 하 고, 클라이언트 브라우저에서 서버 쪽 .net 코드에서 JavaScript 함수를 호출 하 고, 연결/연결 끊기 이벤트, 그룹 연결, 권한 부여 등의 연결 관리에 대 한 유용한 후크를 추가 하는 간단한 고급 API를 제공 합니다.
> 
> **SignalR** 는 클라이언트와 서버 간의 실시간 작업을 수행 하는 데 필요한 일부 전송에 대 한 추상화입니다. **SignalR** 연결은 HTTP로 시작 되 고 사용 가능한 경우 **WebSocket** 연결로 승격 됩니다. **Websocket** 은 서버 메모리를 가장 효율적으로 사용 하 고, 대기 시간을 최소화 하며, 가장 엄격한 요구 사항이 있습니다 (예: 클라이언트와 서버 간의 전이중 통신). 또한 **websocket** 은 서버에서 **windows server 2012** 또는 **windows 8**을 사용 하 여 서버를 **.NET Framework 4.5**과 함께 사용 해야 하기 때문에 **SignalR**에 이상적인 전송입니다. 이러한 요구 사항이 충족 되지 않는 경우 **SignalR** 는 다른 전송을 사용 하 여 연결을 설정 하려고 합니다 (예: *Ajax 긴 폴링*).
> 
> **SignalR** API에는 클라이언트와 서버 간 통신을 위한 두 가지 모델 ( **영구 연결** 및 **허브**)이 포함 되어 있습니다. **연결은** 단일 받는 사람, 그룹화 또는 브로드캐스트 메시지를 보내기 위한 간단한 끝점을 나타냅니다. **허브** 는 클라이언트와 서버에서 직접 메서드를 호출할 수 있도록 하는 연결 API를 기반으로 하는 더 높은 수준의 파이프라인입니다.
> 
> ![SignalR 아키텍처](real-time-web-applications-with-signalr/_static/image1.png)
> 
> 모든 샘플 코드와 코드 조각은 [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)에서 사용할 수 있는 웹 캠프 교육 키트, 10 월 2015 릴리스에 포함 되어 있습니다.  해당 페이지의 설치 관리자 링크는 더 이상 작동 하지 않습니다. 대신 자산 섹션 아래에 있는 링크 중 하나를 사용 합니다.

<a id="Overview"></a>
## <a name="overview"></a>개요

<a id="Objectives"></a>
### <a name="objectives"></a>목표

이 실습 랩에서는 다음 방법에 대해 알아봅니다.

- SignalR를 사용 하 여 서버에서 클라이언트로 알림을 보냅니다.
- **SQL Server**를 사용 하 여 SignalR 응용 프로그램을 Scale Out 합니다.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>사전 요구 사항

이 실습 실습을 완료 하려면 다음이 필요 합니다.

- [웹 이상의 Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)

<a id="Setup"></a>
### <a name="setup"></a>설치 프로그램

이 실습 랩에서 연습을 실행 하려면 먼저 환경을 설정 해야 합니다.

1. Windows 탐색기 창을 열고 랩의 **원본** 폴더로 이동 합니다.
2. **Setup.exe** 를 마우스 오른쪽 단추로 클릭 하 고 **관리자 권한으로 실행** 을 선택 하 여 환경을 구성 하는 설치 프로세스를 시작 하 고이 랩에 대 한 Visual Studio 코드 조각을 설치 합니다.
3. 사용자 계정 컨트롤 대화 상자가 표시 되 면 계속 하려면 작업을 확인 합니다.

> [!NOTE]
> 설치 프로그램을 실행 하기 전에이 랩에 대 한 모든 종속성을 확인 했는지 확인 합니다.

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>코드 조각 사용

랩 문서 전체에서 코드 블록을 삽입 하 라는 지침이 표시 됩니다. 사용자 편의를 위해이 코드의 대부분은 Visual Studio 2013 내에서 액세스할 수 있는 Visual Studio Code 코드 조각으로 제공 되며,이를 수동으로 추가 하지 않아도 됩니다.

> [!NOTE]
> 각 연습에는 각 연습을 서로 독립적으로 수행할 수 있는 연습 **시작** 폴더에 있는 시작 솔루션이 있습니다. 연습 중에 추가 된 코드 조각은 이러한 시작 솔루션에서 누락 되었으며, 연습을 완료할 때까지 작동 하지 않을 수 있습니다. 연습에 대 한 소스 코드 내에서 해당 연습의 단계를 완료 하 여 생성 된 코드를 포함 하는 Visual Studio 솔루션을 포함 하는 **끝** 폴더를 찾을 수도 있습니다. 이 실습 랩을 통해 작업할 때 추가 도움이 필요한 경우 이러한 솔루션을 지침으로 사용할 수 있습니다.

---

<a id="Exercises"></a>
## <a name="exercises"></a>실습

이 실습 랩에는 다음 연습이 포함 되어 있습니다.

1. [SignalR를 사용 하 여 실시간 데이터 작업](#Exercise1)
2. [SQL Server를 사용 하 여 확장](#Exercise2)

이 랩을 완료 하는 데 소요 되는 예상 시간: **60 분**

> [!NOTE]
> Visual Studio를 처음 시작 하는 경우 미리 정의 된 설정 컬렉션 중 하나를 선택 해야 합니다. 미리 정의 된 각 컬렉션은 특정 개발 스타일에 맞게 디자인 되 고 창 레이아웃, 편집기 동작, IntelliSense 코드 조각 및 대화 상자 옵션을 결정 합니다. 이 실습의 절차에서는 **일반 개발 설정** 컬렉션을 사용 하는 경우 Visual Studio에서 지정 된 작업을 수행 하는 데 필요한 작업을 설명 합니다. 개발 환경에 대해 다른 설정 컬렉션을 선택 하는 경우 고려해 야 하는 단계에 차이가 있을 수 있습니다.

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a>연습 1: SignalR를 사용 하 여 실시간 데이터 작업

채팅은 종종 예로 사용 되지만 실시간 웹 기능을 사용 하면 훨씬 더 많은 작업을 수행할 수 있습니다. 사용자가 새 데이터를 볼 수 있도록 웹 페이지를 새로 고치거 나 페이지가 Ajax 긴 폴링을 구현 하 여 새 데이터를 검색 하는 경우에는 SignalR을 사용할 수 있습니다.

SignalR는 **서버 푸시** 또는 **브로드캐스팅** 기능을 지원 합니다. 연결 관리를 자동으로 처리 합니다. 클라이언트-서버 통신을 위한 클래식 HTTP 연결에서 각 요청에 대 한 연결이 다시 설정 되지만 SignalR는 클라이언트와 서버 간에 영구 연결을 제공 합니다. SignalR에서 서버 코드는 현재 알고 있는 요청-응답 모델이 아니라 RPC (원격 프로시저 호출)를 사용 하 여 브라우저에서 클라이언트 코드를 호출 합니다.

이 연습에서는 **Geek of 퀴즈** 응용 프로그램이 SignalR를 사용 하 여 전체 페이지를 새로 고치지 않고도 업데이트 된 메트릭을 사용 하 여 통계 대시보드를 표시 하도록 구성 합니다.

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a>작업 1 – Geek of 퀴즈 통계 페이지 탐색

이 작업에서는 응용 프로그램을 살펴보고 통계 페이지가 표시 되는 방식과 정보가 업데이트 되는 방식을 개선 하는 방법을 확인 합니다.

1. **웹에 대해 Visual Studio Express 2013** 을 열고 **Source\Ex1-WorkingWithRealTimeData\Begin** 폴더에 있는 **GeekQuiz** 솔루션을 엽니다.
2. **F5** 키를 눌러 솔루션을 실행합니다. **로그인** 페이지가 브라우저에 표시 됩니다.

    ![솔루션 실행](real-time-web-applications-with-signalr/_static/image2.png "솔루션 실행")

    *솔루션 실행*
3. 페이지의 오른쪽 위 모퉁이에 있는 **등록** 을 클릭 하 여 응용 프로그램에서 새 사용자를 만듭니다.

    ![링크 등록](real-time-web-applications-with-signalr/_static/image3.png "링크 등록")

    *링크 등록*
4. **등록** 페이지에서 **사용자 이름** 및 **암호**를 입력 한 다음 **등록**을 클릭 합니다.

    ![사용자 등록](real-time-web-applications-with-signalr/_static/image4.png "사용자 등록")

    *사용자 등록*
5. 응용 프로그램이 새 계정을 등록 하 고 사용자가 인증 되 고 첫 번째 퀴즈 질문을 표시 하는 홈 페이지로 다시 리디렉션됩니다.
6. 새 창에서 **통계** 페이지를 열고 **홈** 페이지와 **통계** 페이지를 나란히 배치 합니다.

    ![Side-by-side 창](real-time-web-applications-with-signalr/_static/image5.png "Side-by-side 창")

    *Side-by-side 창*
7. **홈** 페이지에서 옵션 중 하나를 클릭 하 여 질문에 대답 합니다.

    ![질문에 답변](real-time-web-applications-with-signalr/_static/image6.png "질문에 답변")

    *질문에 답변*
8. 단추 중 하나를 클릭 하면 대답이 표시 됩니다.

    ![질문에 대 한 답변이 올바릅니다.](real-time-web-applications-with-signalr/_static/image7.png "질문에 대 한 답변이 올바릅니다.")

    *질문에 대 한 대답이 올바르게*
9. 통계 페이지에 제공 된 정보는 오래 된 정보입니다. 업데이트 된 결과를 보려면 페이지를 새로 고칩니다.

    ![통계 페이지](real-time-web-applications-with-signalr/_static/image8.png "통계 페이지")

    *통계 페이지*
10. Visual Studio로 돌아가서 디버깅을 중지 합니다.

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a>작업 2 – Geek of 퀴즈에 SignalR를 추가 하 여 온라인 차트 표시

이 작업에서는 SignalR를 솔루션에 추가 하 고 새 대답이 서버에 전송 될 때 자동으로 클라이언트에 업데이트를 보냅니다.

1. Visual Studio의 **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 클릭 합니다.
2. **패키지 관리자 콘솔** 창에서 다음 명령을 실행 합니다.

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    ![SignalR 패키지 설치](real-time-web-applications-with-signalr/_static/image9.png "SignalR 패키지 설치")

    *SignalR 패키지 설치*

   > [!NOTE]
   > 새 MVC 5 응용 프로그램에서 **SignalR** NuGet 패키지 버전 2.0.2을 설치 하는 경우 SignalR를 설치 하기 전에 **OWIN** 패키지를 버전 2.0.1 이상으로 수동으로 업데이트 해야 합니다. 이렇게 하려면 **패키지 관리자 콘솔**에서 다음 스크립트를 실행할 수 있습니다.
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > SignalR의 이후 릴리스에서는 OWIN 종속성이 자동으로 업데이트 됩니다.
3. **솔루션 탐색기**에서 **Scripts** 폴더를 확장 하 고 SignalR *js* 파일이 솔루션에 추가 되었음을 확인 합니다.

    ![SignalR JavaScript 참조](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript 참조")

    *SignalR JavaScript 참조*
4. **솔루션 탐색기**에서 GeekQuiz 프로젝트를 마우스 오른쪽 단추로 클릭 하 | **새 폴더** **추가** 를 선택 하 고 이름을 **Hubs**로 .
5. **허브** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가 |를 선택 합니다. 새 항목**입니다.

    ![새 항목 추가](real-time-web-applications-with-signalr/_static/image11.png "새 항목 추가")

    *새 항목 추가*
6. **새 항목 추가** 대화 상자에서 **C# 시각적 개체 | 웹 |** 왼쪽 창의 SignalR 노드 가운데 창에서 **SignalR Hub 클래스 (v2)** 를 선택 하 고 파일 이름을 **StatisticsHub.cs** 로 선택한 후에 **추가**를 클릭 합니다.

    ![새 항목 추가 대화 상자](real-time-web-applications-with-signalr/_static/image12.png "새 항목 추가 대화 상자")

    *새 항목 추가 대화 상자*
7. **StatisticsHub** 클래스의 코드를 다음 코드로 바꿉니다.

    (코드 조각- *RealTimeSignalR-Ex1-StatisticsHubClass*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. **Startup.cs** 를 열고 **구성** 방법의 끝에 다음 줄을 추가 합니다.

    (코드 조각- *RealTimeSignalR-Ex1-MapSignalR*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. **Services** 폴더 내에서 **StatisticsService.cs** 페이지를 열고 다음 using 지시문을 추가 합니다.

    (코드 조각- *RealTimeSignalR-Ex1-UsingDirectives*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. 연결 된 클라이언트에 업데이트를 알리려면 먼저 현재 연결에 대 한 **컨텍스트** 개체를 검색 합니다. **허브** 개체는 단일 클라이언트에 메시지를 보내거나 연결 된 모든 클라이언트에 브로드캐스트하는 메서드를 포함 합니다. **StatisticsService** 클래스에 다음 메서드를 추가 하 여 통계 데이터를 브로드캐스트합니다.

    (코드 조각- *RealTimeSignalR-Ex1-NotifyUpdatesMethod*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > 위의 코드에서는 임의의 메서드 이름을 사용 하 여 클라이언트 (예: *updateStatistics*)에서 함수를 호출 합니다. 지정 하는 메서드 이름은 동적 개체로 해석 됩니다. 즉, IntelliSense 또는 컴파일 타임 유효성 검사를 수행 하지 않습니다. 식은 런타임에 계산 됩니다. 메서드 호출이 실행 되 면 SignalR는 메서드 이름 및 매개 변수 값을 클라이언트에 보냅니다. 클라이언트에 이름과 일치 하는 메서드가 있으면 해당 메서드가 호출 되 고 매개 변수 값이이 메서드에 전달 됩니다. 클라이언트에서 일치 하는 메서드를 찾을 수 없는 경우 오류가 발생 하지 않습니다. 자세한 내용은 [ASP.NET SignalR HUBS API 가이드](../guide-to-the-api/hubs-api-guide-server.md)를 참조 하세요.
11. **Controllers** 폴더 내에서 **TriviaController.cs** 페이지를 열고 다음 using 지시문을 추가 합니다.

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. **사후** 작업 메서드에 다음 강조 표시 된 코드를 추가 합니다.

    (코드 조각- *RealTimeSignalR-Ex1-NotifyUpdatesCall*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. 뷰 내에서 **통계. cshtml** 페이지를 엽니다. **| 홈** 폴더입니다. **스크립트** 섹션을 찾고 섹션의 시작 부분에 다음 스크립트 참조를 추가 합니다.

    (코드 조각- *RealTimeSignalR-Ex1-SignalRScriptReferences*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > SignalR 및 기타 스크립트 라이브러리를 Visual Studio 프로젝트에 추가 하면 패키지 관리자가이 항목에 표시 된 버전 보다 최신 버전인 SignalR 스크립트 파일을 설치할 수 있습니다. 코드의 스크립트 참조가 프로젝트에 설치 된 스크립트 라이브러리 버전과 일치 하는지 확인 합니다.
14. 다음 강조 표시 된 코드를 추가 하 여 클라이언트를 SignalR hub에 연결 하 고 허브에서 새 메시지가 수신 되 면 통계 데이터를 업데이트 합니다.

    (코드 조각- *RealTimeSignalR-Ex1-SignalRClientCode*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    이 코드에서는 허브 프록시를 만들고 서버에서 보낸 메시지를 수신 하기 위해 이벤트 처리기를 등록 합니다. 이 경우 *updateStatistics* 메서드를 통해 전송 되는 메시지를 수신 대기 합니다.

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>작업 3 – 솔루션 실행

이 태스크에서는 솔루션을 실행 하 여 새 질문에 답변 한 후 SignalR를 사용 하 여 통계 보기가 자동으로 업데이트 되는지 확인 합니다.

1. **F5** 키를 눌러 솔루션을 실행합니다.

    > [!NOTE]
    > 응용 프로그램에 아직 로그인 하지 않은 경우 작업 1에서 만든 사용자로 로그인 합니다.
2. 새 창에서 **통계** 페이지를 열고 작업 1에서와 같이 **홈** 페이지와 **통계** 페이지를 나란히 배치 합니다.
3. **홈** 페이지에서 옵션 중 하나를 클릭 하 여 질문에 대답 합니다.

    ![다른 질문에 답변](real-time-web-applications-with-signalr/_static/image13.png "다른 질문에 답변")

    *다른 질문에 답변*
4. 단추 중 하나를 클릭 하면 대답이 표시 됩니다. 페이지의 통계 정보는 전체 페이지를 새로 고칠 필요 없이 업데이트 된 정보를 사용 하 여 질문에 대답 한 후 자동으로 업데이트 됩니다.

    ![응답 후 새로 고쳐진 통계 페이지](real-time-web-applications-with-signalr/_static/image14.png "응답 후 새로 고쳐진 통계 페이지")

    *응답 후 새로 고쳐진 통계 페이지*

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a>연습 2: SQL Server을 사용 하 여 확장

웹 응용 프로그램의 크기를 조정 하는 경우 일반적으로 *수직 확장* 및 *수평 확장* 옵션 중에서 선택할 수 있습니다. 수직 *확장* 은 더 많은 리소스 (CPU, RAM 등)가 있는 대규모 서버를 사용 하는 것을 의미 합니다 .이는 부하를 처리할 서버를 더 추가 하 *는 것입니다* . 후자와 관련 하 여 발생 하는 문제는 클라이언트를 다른 서버로 라우팅할 수 있다는 것입니다. 한 서버에 연결 된 클라이언트는 다른 서버에서 보낸 메시지를 받지 않습니다.

서버 간에 메시지를 전달 하기 위해 *후면판*이라는 구성 요소를 사용 하 여 이러한 문제를 해결할 수 있습니다. 후면판을 사용 하는 경우 각 응용 프로그램 인스턴스는 후면판으로 메시지를 보내고, 후면판은이를 다른 응용 프로그램 인스턴스로 전달 합니다.

SignalR에 대 한 백플레인을에는 현재 다음과 같은 세 가지 유형이 있습니다.

- **Windows Azure Service Bus**. Service Bus는 구성 요소가 느슨하게 결합 된 메시지를 보낼 수 있도록 하는 메시징 인프라입니다.
- **SQL Server**. SQL Server 후면판은 메시지를 SQL 테이블에 기록 합니다. 후면판은 효율적인 메시징의 Service Broker를 사용 합니다. 그러나 Service Broker를 사용 하도록 설정 하지 않은 경우에도 작동 합니다.
- **Redis**. Redis는 메모리 내 키-값 저장소입니다. Redis는 메시지를 보내기 위한 게시/구독 ("pub/sub") 패턴을 지원 합니다.

모든 메시지는 메시지 버스를 통해 전송 됩니다. 메시지 버스는 게시/구독 추상화를 제공 하는 [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) 인터페이스를 구현 합니다. 백플레인을는 기본 **IMessageBus** 를 해당 후면판 용으로 설계 된 버스로 바꿔 작동 합니다.

각 서버 인스턴스는 버스를 통해 후면판에 연결 됩니다. 메시지가 전송 되 면 후면판으로 이동 하 여 후면판에서 모든 서버에 전송 합니다. 서버는 후면판에서 메시지를 받으면 해당 메시지를 로컬 캐시에 저장 합니다. 그런 다음 서버는 로컬 캐시에서 클라이언트로 메시지를 배달 합니다.

SignalR 후면판의 작동 방식에 대 한 자세한 내용은이 [문서](../performance/scaleout-in-signalr.md)를 참조 하세요.

> [!NOTE]
> 후면판이 병목 상태가 될 수 있는 몇 가지 시나리오가 있습니다. 몇 가지 일반적인 SignalR 시나리오는 다음과 같습니다.
> 
> - [서버 브로드캐스트](tutorial-server-broadcast-with-signalr.md) (예: 주식 종목): 백플레인을 서버에서 메시지를 보내는 속도를 제어 하므로이 시나리오에 대해 잘 작동 합니다.
> - [클라이언트-클라이언트](tutorial-getting-started-with-signalr.md) (예: 채팅):이 시나리오에서는 메시지 수가 클라이언트 수로 확장 되 면 후면판에서 병목 현상이 발생할 수 있습니다. 즉, 더 많은 클라이언트에 연결 될 때 메시지의 비율이 비례적으로 증가 하는 경우입니다.
> - [높은 빈도 실시간](tutorial-high-frequency-realtime-with-signalr.md) (예: 실시간 게임):이 시나리오에는 후면판을 권장 하지 않습니다.

이 연습에서는 **SQL Server** 를 사용 하 여 **geek of 퀴즈** 응용 프로그램에서 메시지를 배포 합니다. 이러한 작업을 단일 테스트 컴퓨터에서 실행 하 여 구성을 설정 하는 방법을 배울 수 있습니다. 그러나 전체 효과를 얻으려면 SignalR 응용 프로그램을 둘 이상의 서버에 배포 해야 합니다. 또한 서버 중 하나 또는 별도의 전용 서버에 SQL Server를 설치 해야 합니다.

![SQL Server 다이어그램을 사용 하 여 Scale Out](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a>작업 1-시나리오 이해

이 작업에서는 로컬 컴퓨터에서 여러 IIS 인스턴스를 시뮬레이션 하는 **Geek of 퀴즈** 의 두 인스턴스를 실행 합니다. 이 시나리오에서 한 응용 프로그램에 대 한 기타 정보 질문에 응답 하는 경우 두 번째 인스턴스의 통계 페이지에서 업데이트에 대 한 알림이 표시 되지 않습니다. 이 시뮬레이션은 응용 프로그램이 여러 인스턴스에 배포 되 고 부하 분산 장치를 사용 하 여 통신 하는 환경과 비슷합니다.

1. **Source/Ex2-ScalingOutWithSQLServer/begin** 폴더에 있는 **begin .sln** 솔루션을 엽니다. 로드 된 후에는 솔루션에 동일한 구조를 가진 두 개의 프로젝트가 있지만 이름이 다른 두 프로젝트가 **서버 탐색기** 에 대 한 알림이 표시 됩니다. 이렇게 하면 로컬 컴퓨터에서 동일한 응용 프로그램의 두 인스턴스를 실행 하는 것이 시뮬레이션 됩니다.

    ![Geek of 퀴즈의 2 개 인스턴스를 시뮬레이션 하는 솔루션 시작](real-time-web-applications-with-signalr/_static/image16.png "Geek of 퀴즈의 2 개 인스턴스를 시뮬레이션 하는 솔루션 시작")

    *Geek of 퀴즈의 2 개 인스턴스를 시뮬레이션 하는 솔루션 시작*
2. 솔루션 노드를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 하 여 솔루션의 속성 페이지를 엽니다. 시작 **프로젝트**에서 **여러 개의 시작 프로젝트** 를 선택 하 고 두 프로젝트의 **동작** 값을 *시작*으로 변경 합니다.

    ![여러 프로젝트 시작](real-time-web-applications-with-signalr/_static/image17.png "여러 프로젝트 시작")

    *여러 프로젝트 시작*
3. **F5** 키를 눌러 솔루션을 실행합니다. 응용 프로그램은 동일한 응용 프로그램의 여러 인스턴스를 시뮬레이션 하는 서로 다른 포트에서 **Geek of 퀴즈** 의 두 인스턴스를 시작 합니다. 왼쪽에 있는 브라우저 중 하나를 화면 오른쪽에 고정 합니다. 자격 증명을 사용 하 여 로그인 하거나 새 사용자를 등록 합니다. 로그인 되 면 왼쪽에 있는 기타 정보 페이지를 유지 하 고 오른쪽 브라우저의 **통계** 페이지로 이동 합니다.

    ![Geek of 퀴즈를 나란히](real-time-web-applications-with-signalr/_static/image18.png)

    *Geek of 퀴즈를 나란히*

    ![다른 포트의 geek of 퀴즈](real-time-web-applications-with-signalr/_static/image19.png)

    *다른 포트의 geek of 퀴즈*
4. 왼쪽 브라우저에서 질문에 대 한 대답을 시작 하면 오른쪽 브라우저의 **통계** 페이지가 업데이트 되지 않는 것을 알 수 있습니다. **SignalR** 는 로컬 캐시를 사용 하 여 클라이언트 전체에 메시지를 분산 하 고이 시나리오는 여러 인스턴스를 시뮬레이션 하기 때문에 캐시는 서로 공유 되지 않기 때문입니다. 동일한 단계를 테스트 하 고 단일 앱을 사용 하 여 **SignalR** 작동 하는지 확인할 수 있습니다. 다음 작업에서는 인스턴스 간에 메시지를 복제 하도록 후면판을 구성 합니다.
5. Visual Studio로 돌아가서 디버깅을 중지 합니다.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a>작업 2-SQL Server 백플레인 만들기

이 작업에서는 **Geek of 퀴즈** 응용 프로그램의 후면판 역할을 할 데이터베이스를 만듭니다. **SQL Server 개체 탐색기** 를 사용 하 여 서버를 검색 하 고 데이터베이스를 초기화 합니다. 또한 **Service Broker**를 사용 하도록 설정 합니다.

1. **Visual Studio**에서 메뉴 **보기** 를 열고 **SQL Server 개체 탐색기**를 선택 합니다.
2. **SQL Server** 노드를 마우스 오른쪽 단추로 클릭 하 고 **SQL Server 추가** ... 옵션을 선택 하 여 LocalDB 인스턴스에 연결 합니다.

    ![SQL Server 인스턴스 추가](real-time-web-applications-with-signalr/_static/image20.png "SQL Server 인스턴스 추가")

    *SQL Server 개체 탐색기에 SQL Server 인스턴스 추가*
3. **서버 이름** 을 *(localdb) \v11.0* 으로 설정 하 고 **Windows 인증** 을 인증 모드로 유지 합니다. **연결**을 클릭하여 계속합니다.

    ![LocalDB에 연결](real-time-web-applications-with-signalr/_static/image21.png "LocalDB에 연결")

    *LocalDB에 연결*
4. 이제 LocalDB 인스턴스에 연결 되었으므로 SignalR에 대 한 SQL Server 후면판을 나타내는 데이터베이스를 만들어야 합니다. 이렇게 하려면 **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭 하 고 **새 데이터베이스 추가**를 선택 합니다.

    ![새 데이터베이스 추가](real-time-web-applications-with-signalr/_static/image22.png "새 데이터베이스 추가")

    *새 데이터베이스 추가*
5. 데이터베이스 이름을 *SignalR* 로 설정 하 고 **확인** 을 클릭 하 여 만듭니다.

    ![SignalR 데이터베이스 만들기](real-time-web-applications-with-signalr/_static/image23.png "SignalR 데이터베이스 만들기")

    *SignalR 데이터베이스 만들기*

    > [!NOTE]
    > 데이터베이스의 이름을 선택할 수 있습니다.
6. 후면판에서 업데이트를 보다 효율적으로 수신 하려면 데이터베이스에 대해 Service Broker를 사용 하도록 설정 하는 것이 좋습니다. Service Broker은 SQL Server의 메시징 및 큐에 대 한 기본 지원을 제공 합니다. 후면판은 Service Broker 없이도 작동 합니다. 데이터베이스를 마우스 오른쪽 단추로 클릭 하 고 **새 쿼리**를 선택 하 여 새 쿼리를 엽니다.

    ![새 쿼리 열기](real-time-web-applications-with-signalr/_static/image24.png "새 쿼리 열기")

    *새 쿼리 열기*
7. Service Broker 사용 하도록 설정 되어 있는지 여부를 확인 하려면를 사용 **하 여** **\_Broker\_사용** 열을 쿼리 합니다. 최근에 열었던 쿼리 창에서 다음 스크립트를 실행 합니다.

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    ![Service Broker 상태 쿼리](real-time-web-applications-with-signalr/_static/image25.png "Service Broker 상태 쿼리")

    *Service Broker 상태 쿼리*
8. 의 값 **이\_broker\_사용 하도록 설정** 된 경우 데이터베이스에서 사용 하도록 설정 된 열이 0&quot;&quot;다음 명령을 사용 하 여 사용 하도록 설정 합니다. **&lt;데이터베이스&gt;** 을 만들 때 설정한 이름으로 바꿉니다 (예: SignalR).

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    ![Service Broker 사용](real-time-web-applications-with-signalr/_static/image26.png "Service Broker 사용")

    *Service Broker 사용*

    > [!NOTE]
    > 이 쿼리가 교착 상태로 표시 되는 경우 DB에 연결 된 응용 프로그램이 없는지 확인 합니다.

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a>작업 3-SignalR 응용 프로그램 구성

이 작업에서는 SQL Server 후면판에 연결 하도록 **Geek of 퀴즈** 를 구성 합니다. 먼저 **SignalR** NuGet 패키지를 추가 하 고 연결 문자열을 후면판 데이터베이스로 설정 합니다.

1. **도구** > **NuGet 패키지 관리자**에서 **패키지 관리자 콘솔** 을 엽니다. **기본 프로젝트** 드롭다운 목록에서 **GeekQuiz** 프로젝트가 선택 되어 있는지 확인 합니다. 다음 명령을 입력 하 여 **SignalR** NuGet 패키지를 설치 합니다.

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. 이전 단계를 반복 하지만 이번에는 project **GeekQuiz2**에 대해이 시간을 반복 합니다.
3. SQL Server 백플레인를 구성 하려면 **GeekQuiz** 프로젝트의 **Startup.cs** 파일을 열고 **configure** 메서드에 다음 코드를 추가 합니다. **&lt;-데이터베이스&gt;** 을 SQL Server 백플레인를 만들 때 사용한 데이터베이스 이름으로 바꿉니다. **GeekQuiz2** 프로젝트에 대해이 단계를 반복 합니다.

    (코드 조각- *RealTimeSignalR-Ex2-StartupConfiguration*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. 이제 두 프로젝트가 모두 SQL Server 후면판을 사용 하도록 구성 되었으므로 **F5** 키를 눌러 동시에 실행 합니다.
5. 다시 **Visual Studio** 는 서로 다른 포트에서 두 개의 **geek of 퀴즈** 인스턴스를 시작 합니다. 왼쪽에 있는 브라우저 중 하나를 화면 오른쪽에 고정 하 고 자격 증명을 사용 하 여 로그인 합니다. 왼쪽에 있는 기타 정보 페이지를 유지 하 고 오른쪽 브라우저에서 **통계** pagein 이동 합니다.
6. 왼쪽 브라우저에서 질문에 답변 하기 시작 합니다. 이번에는 후면판 덕분에 **통계** 페이지가 업데이트 됩니다. 응용 프로그램 사이를 전환 하 고 (이제**통계** 는 왼쪽에 있고, **기타 정보** 는 오른쪽에 있습니다.) 테스트를 반복 하 여 두 인스턴스에 대해 모두 작동 하는지 확인 합니다. 후면판은 연결 된 각 서버에 대 한 메시지의 *공유 캐시로* 사용 되며, 각 서버는 연결 된 클라이언트에 배포할 메시지를 자체 로컬 캐시에 저장 합니다.
7. Visual Studio로 돌아가서 디버깅을 중지 합니다.
8. SQL Server 백플레인 구성 요소는 지정 된 데이터베이스에 필요한 테이블을 자동으로 생성 합니다. **SQL Server 개체 탐색기** 패널에서 후면판에 대해 만든 데이터베이스 (예: SignalR)를 열고 해당 테이블을 확장 합니다. 다음 테이블이 표시 됩니다.

    ![후면판 생성 테이블](real-time-web-applications-with-signalr/_static/image27.png)

    *후면판 생성 테이블*
9. **SignalR\_0** 테이블을 마우스 오른쪽 단추로 클릭 하 고 **데이터 보기**를 선택 합니다.

    ![SignalR 후면판 메시지 보기 테이블](real-time-web-applications-with-signalr/_static/image28.png)

    *SignalR 후면판 메시지 보기 테이블*
10. 기타 정보 질문에 대답할 때 **허브** 로 전송 되는 다른 메시지를 볼 수 있습니다. 후면판은 이러한 메시지를 연결 된 인스턴스에 배포 합니다.

    ![후면판 메시지 테이블](real-time-web-applications-with-signalr/_static/image29.png)

    *후면판 메시지 테이블*

---

<a id="Summary"></a>
## <a name="summary"></a>요약

이 실습 랩에서는 응용 프로그램에 **SignalR** 를 추가 하 고 **허브**를 사용 하 여 서버에서 연결 된 클라이언트로 알림을 보내는 방법에 대해 알아보았습니다. 또한 응용 프로그램을 여러 IIS 인스턴스에 배포할 때 *후면판* 구성 요소를 사용 하 여 응용 프로그램을 확장 하는 방법을 배웠습니다.
