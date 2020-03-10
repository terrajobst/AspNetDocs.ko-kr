---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: SignalR 확장 with Azure Service Bus (SignalR 1.x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449939"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a>Azure Service Bus로 SignalR 규모 확장(SignalR 1.x)

사람, [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

이 자습서에서는 Service Bus 후면판을 사용 하 여 각 역할 인스턴스에 메시지를 배포 하는 Windows Azure 웹 역할에 SignalR 응용 프로그램을 배포 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

필수 조건:

- Microsoft Azure 계정.
- [Microsoft AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)
- Visual Studio 2012.

Service bus 후면판은 Windows Server 버전 1.1 [에 대 한 Service Bus](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)와도 호환 됩니다. 그러나 Windows Server Service Bus 버전 1.0과 호환 되지 않습니다.

## <a name="pricing"></a>가격

Service Bus 백플레인는 항목을 사용 하 여 메시지를 보냅니다. 최신 가격 책정 정보는 [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/)를 참조 하세요. 이 문서를 작성 하는 시점에 $1 보다 작은 100만 메시지를 월 단위로 보낼 수 있습니다. 후면판은 SignalR hub 메서드를 호출할 때마다 service bus 메시지를 보냅니다. 연결, 연결 끊기, 그룹 연결 또는 탈퇴 등에 대 한 제어 메시지도 있습니다. 대부분의 응용 프로그램에서 대부분의 메시지 트래픽은 허브 메서드 호출이 됩니다.

## <a name="overview"></a>개요

자세한 자습서를 시작 하기 전에 수행할 작업에 대 한 간략 한 개요를 참조 하세요.

1. Windows Azure Portal를 사용 하 여 새 Service Bus 네임 스페이스를 만듭니다.
2. 응용 프로그램에 다음 NuGet 패키지를 추가 합니다. 

    - [SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [SignalR. ServiceBus](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. SignalR 응용 프로그램을 만듭니다.
4. Global.asax에 다음 코드를 추가 하 여 후면판을 구성 합니다. 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

각 응용 프로그램에 대해 "해당"에 대해 다른 값을 선택 합니다. 여러 응용 프로그램에서 동일한 값을 사용 하지 마십시오.

## <a name="create-the-azure-services"></a>Azure 서비스 만들기

[클라우드 서비스를 만들고 배포 하는 방법](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)에 설명 된 대로 클라우드 서비스를 만듭니다. "방법: 빠른 생성을 사용 하 여 클라우드 서비스 만들기" 섹션의 단계를 따릅니다. 이 자습서에서는 인증서를 업로드할 필요가 없습니다.

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

[Service Bus 토픽/구독을 사용 하는 방법](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)에 설명 된 대로 새 Service Bus 네임 스페이스를 만듭니다. "서비스 네임 스페이스 만들기" 섹션의 단계를 따릅니다.

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> 클라우드 서비스와 Service Bus 네임 스페이스에 대해 동일한 지역을 선택 해야 합니다.

## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Studio를 시작합니다. **파일** 메뉴에서 **새 프로젝트**를 클릭합니다.

**새 프로젝트** 대화 상자에서 **시각적 개체 C#** 를 확장 합니다. **설치 된 템플릿**에서 **클라우드** 를 선택 하 고 **Windows Azure 클라우드 서비스**를 선택 합니다. 기본값 .NET Framework 4.5를 유지 합니다. 응용 프로그램의 이름을 \ 서비스로 하 고 **확인**을 클릭 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

**새 Windows Azure 클라우드 서비스** 대화 상자에서 ASP.NET MVC 4 웹 역할을 선택 합니다. 오른쪽 화살표 단추 ( **&gt;** )를 클릭 하 여 솔루션에 역할을 추가 합니다.

새 역할 위로 마우스를 가져가면 연필 아이콘이 표시 됩니다. 역할의 이름을 바꾸려면이 아이콘을 클릭 합니다. 역할 이름을 "SignalRChat"로 하 고 **확인을**클릭 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

**새 ASP.NET MVC 4 프로젝트** 마법사에서 **인터넷 응용 프로그램**을 선택 합니다. **확인**을 클릭합니다. 프로젝트 마법사는 다음과 같은 두 개의 프로젝트를 만듭니다.

- 서버 서비스:이 프로젝트는 Windows Azure 응용 프로그램입니다. Azure 역할 및 기타 구성 옵션을 정의 합니다.
- SignalRChat:이 프로젝트는 ASP.NET MVC 4 프로젝트입니다.

## <a name="create-the-signalr-chat-application"></a>SignalR 채팅 응용 프로그램 만들기

채팅 응용 프로그램을 만들려면 자습서 [SignalR AND MVC 4 시작](tutorial-getting-started-with-signalr-and-mvc-4.md)의 단계를 따르세요.

NuGet을 사용 하 여 필요한 라이브러리를 설치 합니다. **도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. **패키지 관리자 콘솔** 창에서 다음 명령을 입력 합니다.

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

`-ProjectName` 옵션을 사용 하 여 Windows Azure 프로젝트가 아닌 ASP.NET MVC 프로젝트에 패키지를 설치 합니다.

## <a name="configure-the-backplane"></a>후면판 구성

응용 프로그램의 global.asax 파일에서 다음 코드를 추가 합니다.

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

이제 service bus 연결 문자열을 가져와야 합니다. Azure Portal에서 사용자가 만든 service bus 네임 스페이스를 선택 하 고 액세스 키 아이콘을 클릭 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

연결 문자열을 클립보드에 복사 하 고 *connectionString* 변수에 붙여 넣습니다.

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>Deploy to Azure

솔루션 탐색기에서 프로젝트 서비스 프로젝트 내의 **역할** 폴더를 확장 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

SignalRChat 역할을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **구성** 탭을 선택 합니다. **인스턴스** 아래에서 2를 선택 합니다. VM 크기를 **매우 작게**설정할 수도 있습니다.

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

변경 내용을 저장합니다.

솔루션 탐색기에서 마우스 오른쪽 단추로 클릭 하 여 서비스 프로젝트를 마우스 오른쪽 단추로 클릭 합니다. **게시**를 선택합니다.

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

처음으로 Windows Azure에 게시 하는 경우 자격 증명을 다운로드 해야 합니다. **게시** 마법사에서 "자격 증명을 다운로드 하려면 로그인"을 클릭 합니다. 그러면 Windows Azure Portal에 로그인 하 고 게시 설정 파일을 다운로드 하 라는 메시지가 표시 됩니다.

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

**가져오기** 를 클릭 하 고 다운로드 한 게시 설정 파일을 선택 합니다.

**다음**을 클릭합니다. **게시 설정** 대화 상자의 **클라우드 서비스**에서 이전에 만든 클라우드 서비스를 선택 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

**게시**를 클릭합니다. 응용 프로그램을 배포 하 고 Vm을 시작 하는 데 몇 분 정도 걸릴 수 있습니다.

이제 채팅 응용 프로그램을 실행할 때 역할 인스턴스는 Service Bus 항목을 사용 하 여 Azure Service Bus를 통해 통신 합니다. 토픽은 여러 구독자를 허용 하는 메시지 큐입니다.

후면판은 토픽 및 구독을 자동으로 만듭니다. 구독 및 메시지 작업을 보려면 Azure Portal를 열고 Service Bus 네임 스페이스를 선택한 다음 "항목"을 클릭 합니다.

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

메시지 활동이 대시보드에 표시 되는 데 몇 분 정도 걸릴 수 있습니다.

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

SignalR는 토픽 수명을 관리 합니다. 응용 프로그램이 배포 되는 동안 항목을 수동으로 삭제 하거나 항목의 설정을 변경 하지 마세요.
