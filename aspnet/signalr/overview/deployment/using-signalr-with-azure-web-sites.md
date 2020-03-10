---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Azure App Service에서 Web Apps와 함께 SignalR 사용 | Microsoft Docs
author: bradygaster
description: 이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법을 설명 합니다. 자습서 Visual Studio 2013 또는 Vis에서 사용 되는 소프트웨어 버전
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450185"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a>Azure App Service에서 Web Apps에 SignalR 사용

[Patrick Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 이 문서에서는 Microsoft Azure에서 실행 되는 SignalR 응용 프로그램을 구성 하는 방법을 설명 합니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) 또는 Visual Studio 2012
> - .NET 4.5
> - SignalR 버전 2
> - Visual Studio 2013 또는 2012 용 Azure SDK 2.3
>
>
>
> ## <a name="questions-and-comments"></a>질문 및 설명
>
> 이 자습서와 페이지 맨 아래에 있는 의견에서 개선할 수 있는 방법에 대 한 의견을 남겨 주세요. 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET SignalR 포럼](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/)또는 [Microsoft Azure 포럼](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)에 게시할 수 있습니다.

## <a name="table-of-contents"></a>목차

- [소개](#introduction)
- [Azure App Service에 SignalR 웹 앱 배포](#deploying)
- [Azure App Service에서 Websocket 사용](#websocket)
- [Azure Redis Cache 백플레인 사용](#backplane)
- [다음 단계](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a>소개

ASP.NET SignalR를 사용 하 여 서버와 웹 또는 .NET 클라이언트 간에 새로운 수준의 상호 작용을 가져올 수 있습니다. Azure에서 호스트 되는 경우 SignalR 응용 프로그램은 클라우드에서 실행 되는 고가용성, 확장 가능 및 고성능 환경을 활용할 수 있습니다.

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a>Azure App Service에 SignalR 웹 앱 배포

SignalR는 Azure에 응용 프로그램을 배포 하 고 온-프레미스 서버에 배포 하는 경우 특정 복잡성을 추가 하지 않습니다. SignalR를 사용 하는 응용 프로그램은 구성 또는 기타 설정의 변경 없이 Azure에서 호스팅될 수 있습니다 (Websocket 지원의 경우 아래 [Azure App Service에서 Websocket 사용](#websocket) 을 참조 하세요.) 이 자습서에서는 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md) 에서 만든 응용 프로그램을 Azure에 배포 합니다.

**필수 구성 요소**

- Visual Studio 2013. Visual Visual Studio 2013 Studio가 없는 경우 Express for Web이 Azure SDK의 설치에 포함 됩니다.
- [Visual Studio 2013 용 AZURE sdk 2.3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) 또는 [Visual Studio 2012 용 azure sdk 2.3](https://go.microsoft.com/fwlink/p/?linkid=323511)
- 이 자습서를 완료하려면 Azure 구독이 필요합니다. [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)하거나 [평가판 구독에 등록할](https://azure.microsoft.com/pricing/free-trial/)수 있습니다.

### <a name="deploying-a-signalr-web-app-to-azure"></a>SignalR 웹 앱을 Azure에 배포

1. 초보자를 위한 [자습서](../getting-started/tutorial-getting-started-with-signalr.md)를 완료 하거나 [코드 갤러리](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)에서 완료 된 프로젝트를 다운로드 합니다.
2. Visual Studio에서 **빌드**, **SignalR 채팅 게시**를 선택 합니다.
3. "웹 게시" 대화 상자에서 "Microsoft Azure 웹 사이트"를 선택 합니다.

    ![Azure 웹 사이트 선택](using-signalr-with-azure-web-sites/_static/image1.png)
4. Microsoft 계정에 로그인 하지 않은 경우 "기존 웹 사이트 선택" 대화 상자에서 **로그인 ...** 을 클릭 하 고 로그인 합니다.

    ![기존 웹 사이트 선택](using-signalr-with-azure-web-sites/_static/image2.png)    ![Azure에 로그인](using-signalr-with-azure-web-sites/_static/image3.png)
5. "기존 웹 사이트 선택" 대화 상자에서 **새로 만들기**를 클릭 합니다.

    ![새 웹 사이트](using-signalr-with-azure-web-sites/_static/image4.png)
6. "Windows Azure에서 사이트 만들기" 대화 상자에서 고유한 앱 이름을 입력 합니다. 지역 드롭다운에서 가장 가까운 지역을 선택 합니다. **만들기**를 클릭합니다.

    ![Azure에서 사이트 만들기](using-signalr-with-azure-web-sites/_static/image5.png)
7. "웹 게시" 대화 상자에서 **게시**를 클릭 합니다.

    ![사이트 게시](using-signalr-with-azure-web-sites/_static/image6.png)
8. 앱이 게시를 완료 하면 Azure App Service Web Apps에서 호스트 되는 SignalR Chat 응용 프로그램이 브라우저에서 열립니다.

    ![브라우저에서 사이트 열기](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a>Azure App Service Web Apps에서 Websocket 사용

Websocket은 SignalR 응용 프로그램에서 사용 하기 위해 웹 앱에서 명시적으로 사용 하도록 설정 해야 합니다. 그렇지 않으면 다른 프로토콜이 사용 됩니다. 자세한 내용은 [전송 및 대체](../getting-started/introduction-to-signalr.md#transports) 를 참조 하세요.

Azure App Service Web Apps에서 Websocket을 사용 하려면 웹 앱의 구성 섹션에서 사용 하도록 설정 합니다. 이렇게 하려면 [Azure 관리 포털](https://manage.windowsazure.com/)에서 웹 앱을 열고 구성을 선택 합니다.

![구성 탭](using-signalr-with-azure-web-sites/_static/image8.png)

구성 페이지의 맨 위에서 .NET 4.5이 웹 앱에 사용 되는지 확인 합니다.

![.NET framework 버전 4.5 설정](using-signalr-with-azure-web-sites/_static/image9.png)

구성 페이지의 **websocket** 설정에서 **켜기**를 선택 합니다.

![Websocket 설정: 설정](using-signalr-with-azure-web-sites/_static/image10.png)

구성 페이지의 맨 아래에서 **저장** 을 선택 하 여 변경 내용을 저장 합니다.

![설정 저장](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a>Azure Redis Cache 백플레인 사용

웹 앱에 여러 인스턴스를 사용 하 고 해당 인스턴스의 사용자가 서로 상호 작용 해야 하는 경우 (예를 들어 한 인스턴스에서 만든 채팅 메시지는 다른 인스턴스에 연결 된 사용자에 게 도달 하는 경우), 응용 프로그램에서 [Azure Redis Cache 백플레인](../performance/scaleout-with-redis.md) 를 구현 해야 합니다.

<a id="nextsteps"></a>
## <a name="next-steps"></a>다음 단계

Azure App Service Web Apps에 대 한 자세한 내용은 [Web Apps 개요](https://azure.microsoft.com/documentation/articles/app-service-web-overview/)를 참조 하세요.
