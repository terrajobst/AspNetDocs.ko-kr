---
uid: signalr/overview/testing-and-debugging/unit-testing-signalr-applications
title: SignalR 응용 프로그램 단위 테스트 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 SignalR 2.0의 유닛 테스트 기능을 사용 하는 방법을 설명 합니다.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: d1983524-e0d5-4ee6-9d87-1f552f7cb964
msc.legacyurl: /signalr/overview/testing-and-debugging/unit-testing-signalr-applications
msc.type: authoredcontent
ms.openlocfilehash: 2cf2e88f141d89971439dc1fc4979849f8dded47
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78467303"
---
# <a name="unit-testing-signalr-applications"></a>SignalR 애플리케이션 유닛 테스트

[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 SignalR 2의 유닛 테스트 기능을 사용 하는 방법을 설명 합니다.
>
> ## <a name="software-versions-used-in-this-topic"></a>이 항목에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 버전 2
>
>
>
> ## <a name="questions-and-comments"></a>질문 및 설명
>
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) 또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

<a id="unit"></a>
## <a name="unit-testing-signalr-applications"></a>SignalR 응용 프로그램 단위 테스트

SignalR 2의 단위 테스트 기능을 사용 하 여 SignalR 응용 프로그램에 대 한 단위 테스트를 만들 수 있습니다. SignalR 2에는 테스트를 위한 허브 메서드를 시뮬레이션 하기 위해 모의 개체를 만드는 데 사용할 수 있는 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) 인터페이스가 포함 되어 있습니다.

이 섹션에서는 [XUnit.net](https://github.com/xunit/xunit) 및 [moq](https://github.com/Moq/moq4)를 사용 하 여 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md) 에서 만든 응용 프로그램에 대 한 단위 테스트를 추가 합니다.

XUnit.net는 테스트를 제어 하는 데 사용 됩니다. Moq는 테스트를 위한 [모의](http://en.wikipedia.org/wiki/Mock_object) 개체를 만드는 데 사용 됩니다. 원하는 경우 다른 모의 프레임 워크를 사용할 수 있습니다. [Nsubstitute](http://nsubstitute.github.io/) 좋은 선택 이기도 합니다. 이 자습서에서는 다음 두 가지 방법으로 모의 개체를 설정 하는 방법을 보여 줍니다. 첫 번째는 `dynamic` 개체 (.NET Framework 4에서 도입 됨)와 두 번째 인터페이스를 사용 하는 것입니다.

### <a name="contents"></a>콘텐츠

이 자습서에는 다음과 같은 섹션이 포함 되어 있습니다.

- [동적으로 단위 테스트](#dynamic)
- [유형별 단위 테스트](#type)

<a id="dynamic"></a>
### <a name="unit-testing-with-dynamic"></a>동적으로 단위 테스트

이 섹션에서는 동적 개체를 사용 하 여 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md) 에서 만든 응용 프로그램에 대 한 단위 테스트를 추가 합니다.

1. Visual Studio 2013에 대 한 [Xunit Runner 확장](https://visualstudiogallery.msdn.microsoft.com/463c5987-f82b-46c8-a97e-b1cde42b9099) 을 설치 합니다.
2. 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md)를 완료 하거나 [MSDN 코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)에서 완성 된 응용 프로그램을 다운로드 하세요.
3. 다운로드 버전의 시작 응용 프로그램을 사용 하는 경우 **패키지 관리자 콘솔** 을 열고 **복원** 을 클릭 하 여 SignalR 패키지를 프로젝트에 추가 합니다.

    ![패키지 복원](unit-testing-signalr-applications/_static/image1.png)
4. 단위 테스트에 대 한 프로젝트를 솔루션에 추가 합니다. **솔루션 탐색기** 에서 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가**, **새 프로젝트**...를 차례로 선택 합니다. **C#** 노드 아래에서 **Windows** 노드를 선택 합니다. **클래스 라이브러리**를 선택 합니다. 새 프로젝트의 이름을 **Testlibrary** 로 하 고 **확인**을 클릭 합니다.

    ![테스트 라이브러리 만들기](unit-testing-signalr-applications/_static/image2.png)
5. SignalRChat 프로젝트에 테스트 라이브러리 프로젝트에 대 한 참조를 추가 합니다. **Testlibrary** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가**, **참조 ...** 를 차례로 선택 합니다. **솔루션** 노드 아래에서 **프로젝트** 노드를 선택 하 고 **SignalRChat**를 확인 합니다. **확인**을 클릭합니다.

    ![프로젝트 참조 추가](unit-testing-signalr-applications/_static/image3.png)
6. **Testlibrary** 프로젝트에 SignalR, Moq 및 xunit 패키지를 추가 합니다. **패키지 관리자 콘솔**에서 **기본 프로젝트** 드롭다운을 **testlibrary**로 설정 합니다. 콘솔 창에서 다음 명령을 실행 합니다.

   - `Install-Package Microsoft.AspNet.SignalR`
   - `Install-Package Moq`
   - `Install-Package XUnit`

     ![패키지 설치](unit-testing-signalr-applications/_static/image4.png)
7. 테스트 파일을 만듭니다. **Testlibrary** 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **추가 ...** , **클래스**를 차례로 클릭 합니다. 새 클래스의 이름을 **Tests.cs**로 합니다.
8. Tests.cs의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample1.cs)]

    위의 코드에서 테스트 클라이언트는 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) 형식의 [moq](https://github.com/Moq/moq4) 라이브러리의 `Mock` 개체를 사용 하 여 만듭니다 (SignalR 2.1에서 형식 매개 변수에 대 한 `dynamic` 할당). `IHubCallerConnectionContext` 인터페이스는 클라이언트에서 메서드를 호출 하는 데 사용 되는 프록시 개체입니다. 그러면 `ChatHub` 클래스에서 호출할 수 있도록 `broadcastMessage` 함수가 모의 클라이언트에 대해 정의 됩니다. 그런 다음 테스트 엔진은 `ChatHub` 클래스의 `Send` 메서드를 호출 합니다. 그러면이 메서드는 모의 `broadcastMessage` 함수를 호출 합니다.
9. **F6**키를 눌러 솔루션을 빌드합니다.
10. 단위 테스트를 실행합니다. Visual Studio에서 **테스트**, **Windows**, **테스트 탐색기**를 선택 합니다. 테스트 탐색기 창에서 **HubsAreMockableViaDynamic** 를 마우스 오른쪽 단추로 클릭 하 고 **선택한 테스트 실행**을 선택 합니다.

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image5.png)
11. 테스트 탐색기 창에서 아래쪽 창을 확인 하 여 테스트가 통과 했는지 확인 합니다. 이 창에는 테스트 성공이 표시 됩니다.

    ![테스트 통과](unit-testing-signalr-applications/_static/image6.png)

<a id="type"></a>
### <a name="unit-testing-by-type"></a>유형별 단위 테스트

이 섹션에서는 테스트할 메서드가 포함 된 인터페이스를 사용 하 여 [시작 자습서](../getting-started/tutorial-getting-started-with-signalr.md) 에서 만든 응용 프로그램에 대 한 테스트를 추가 합니다.

1. 위의 [동적 자습서를 사용 하 여 단위 테스트](#dynamic) 에서 1-7 단계를 완료 합니다.
2. Tests.cs의 내용을 다음 코드로 바꿉니다.

    [!code-csharp[Main](unit-testing-signalr-applications/samples/sample2.cs)]

    위의 코드에서는 테스트 엔진에서 모의 클라이언트를 만들 `broadcastMessage` 메서드의 시그니처를 정의 하는 인터페이스가 생성 됩니다. 그런 다음 [IHubCallerConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.ihubcallerconnectioncontext(v=vs.118).aspx) 형식의 `Mock` 개체 (SignalR 2.1, 형식 매개 변수에 대 한 `dynamic` 할당)를 사용 하 여 모의 클라이언트를 만듭니다. `IHubCallerConnectionContext` 인터페이스는 클라이언트에서 메서드를 호출 하는 데 사용 되는 프록시 개체입니다.

    그런 다음 테스트는 `ChatHub`의 인스턴스를 만든 다음 `broadcastMessage` 메서드의 모의 버전을 만듭니다 .이 버전은 허브에서 `Send` 메서드를 호출 하 여 호출 됩니다.
3. **F6**키를 눌러 솔루션을 빌드합니다.
4. 단위 테스트를 실행합니다. Visual Studio에서 **테스트**, **Windows**, **테스트 탐색기**를 선택 합니다. 테스트 탐색기 창에서 **HubsAreMockableViaDynamic** 를 마우스 오른쪽 단추로 클릭 하 고 **선택한 테스트 실행**을 선택 합니다.

    ![테스트 탐색기](unit-testing-signalr-applications/_static/image7.png)
5. 테스트 탐색기 창에서 아래쪽 창을 확인 하 여 테스트가 통과 했는지 확인 합니다. 이 창에는 테스트 성공이 표시 됩니다.

    ![테스트 통과](unit-testing-signalr-applications/_static/image8.png)
