---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: OWIN를 사용 하 여 자체 호스트 ASP.NET Web API-ASP.NET 4.x
author: rick-anderson
description: 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 주는 코드를 보여 주는 자습서입니다.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448331"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a>OWIN를 사용 하 여 자체 호스트 ASP.NET Web API 

> 이 자습서에서는 OWIN를 사용 하 여 Web API 프레임 워크를 자체 호스트 하는 콘솔 응용 프로그램에서 ASP.NET Web API를 호스트 하는 방법을 보여 줍니다.
>
> OWIN ( [Open Web Interface for .net](http://owin.org) )는 .net 웹 서버와 웹 응용 프로그램 간의 추상화를 정의 합니다. OWIN는 서버에서 웹 응용 프로그램을 분리 IIS 외부의 자체 프로세스에서 웹 응용 프로그램을 자체 호스트 하는 데 적합 합니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 
> - Web API 5.2.7

> [!NOTE]
> [Github.com/aspnet/samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample)에서이 자습서에 대 한 전체 소스 코드를 찾을 수 있습니다.

## <a name="create-a-console-application"></a>콘솔 애플리케이션 만들기

**파일** 메뉴에서 **새로 만들기**를 선택한 다음 **프로젝트**를 선택 합니다. **설치 됨**의 **시각적 개체 C#** 에서 **Windows 데스크톱** 을 선택한 다음 **콘솔 앱 (.net Framework)** 을 선택 합니다. 프로젝트 이름을 "OwinSelfhostSample"로 선택 하 고 **확인을**선택 합니다.

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a>Web API 및 OWIN 패키지 추가

**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

그러면 WebAPI OWIN selfhost 패키지와 필요한 모든 OWIN 패키지가 설치 됩니다.

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>자체 호스트에 대 한 Web API 구성

솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 / **클래스** **추가** 를 선택 하 여 새 클래스를 추가 합니다. 클래스 `Startup` 이름을 지정합니다.

![](use-owin-to-self-host-web-api/_static/image5.png)

이 파일의 모든 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>Web API 컨트롤러 추가

그런 다음 웹 API 컨트롤러 클래스를 추가 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 / **클래스** **추가** 를 선택 하 여 새 클래스를 추가 합니다. 클래스 `ValuesController` 이름을 지정합니다.

이 파일의 모든 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a>OWIN 호스트를 시작 하 고 HttpClient를 사용 하 여 요청 만들기

Program.cs 파일의 모든 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a>애플리케이션 실행

응용 프로그램을 실행 하려면 Visual Studio에서 F5 키를 누릅니다. 출력은 다음과 비슷합니다.

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>추가 리소스

[프로젝트 Katana 개요](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Azure 작업자 역할의 호스트 ASP.NET Web API](host-aspnet-web-api-in-an-azure-worker-role.md)
