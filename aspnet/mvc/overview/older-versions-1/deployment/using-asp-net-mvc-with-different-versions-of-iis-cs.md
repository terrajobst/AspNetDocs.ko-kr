---
uid: mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
title: 다른 버전의 IIS ()에서 ASP.NET MVCC#사용 () | Microsoft Docs
author: microsoft
description: 이 자습서에서는 다양 한 버전의 인터넷 정보 서비스에서 ASP.NET MVC 및 URL 라우팅을 사용 하는 방법에 대해 알아봅니다. 다른 전략을 배우고 있습니다 ...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: b0cf4a34-2c1d-4717-bb54-ff029e722990
msc.legacyurl: /mvc/overview/older-versions-1/deployment/using-asp-net-mvc-with-different-versions-of-iis-cs
msc.type: authoredcontent
ms.openlocfilehash: 3b0a9509c0600f3598fd1218a7b383430548d4c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486527"
---
# <a name="using-aspnet-mvc-with-different-versions-of-iis-c"></a>다양한 버전의 IIS에 ASP.NET MVC 사용(C#)

[Microsoft](https://github.com/microsoft) 에서

> 이 자습서에서는 다양 한 버전의 인터넷 정보 서비스에서 ASP.NET MVC 및 URL 라우팅을 사용 하는 방법에 대해 알아봅니다. Iis 7.0 (클래식 모드), IIS 6.0 및 이전 버전의 IIS에서 ASP.NET MVC를 사용 하기 위한 다양 한 전략에 대해 알아봅니다.

ASP.NET MVC 프레임 워크는 ASP.NET 라우팅에 의존 하 여 브라우저 요청을 컨트롤러 작업으로 라우팅합니다. ASP.NET 라우팅을 활용 하기 위해 웹 서버에서 추가 구성 단계를 수행 해야 할 수 있습니다. 응용 프로그램의 인터넷 정보 서비스 (IIS) 버전과 요청 처리 모드에 따라 달라 집니다.

다음은 다양 한 버전의 IIS에 대 한 요약입니다.

- IIS 7.0 (통합 모드)-ASP.NET 라우팅을 사용 하는 데 필요한 특별 한 구성이 없습니다.
- IIS 7.0 (클래식 모드)-ASP.NET 라우팅을 사용 하기 위해 특별 한 구성을 수행 해야 합니다.
- IIS 6.0 이상-ASP.NET 라우팅을 사용 하기 위해 특별 한 구성을 수행 해야 합니다.

IIS의 최신 버전은 7.5 (Win7) 버전입니다. Iis의 IIS 7은 Windows Server 2008 및 VISTA/SP1 이상에 포함 되어 있습니다. 또한 Home Basic을 제외한 모든 버전의 Vista 운영 체제에 IIS 7.0를 설치할 수 있습니다 ( [https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx](https://technet.microsoft.com/library/cc731179%28WS.10%29.aspx)참조).

IIS 7.0는 요청을 처리 하기 위한 두 가지 모드를 지원 합니다. 통합 모드 또는 클래식 모드를 사용할 수 있습니다. 통합 모드에서 IIS 7.0를 사용 하는 경우 특별 한 구성 단계를 수행할 필요가 없습니다. 그러나 클래식 모드에서 IIS 7.0를 사용 하는 경우 추가 구성을 수행 해야 합니다.

Microsoft Windows Server 2003에는 IIS 6.0이 포함 되어 있습니다. Windows Server 2003 운영 체제를 사용 하는 경우 IIS 6.0를 IIS 7.0로 업그레이드할 수 없습니다. IIS 6.0를 사용 하는 경우 추가 구성 단계를 수행 해야 합니다.

Microsoft Windows XP Professional에는 IIS 5.1이 포함 되어 있습니다. IIS 5.1를 사용 하는 경우 추가 구성 단계를 수행 해야 합니다.

마지막으로 Microsoft Windows 2000 및 Microsoft Windows 2000 Professional에는 IIS 5.0가 포함 되어 있습니다. IIS 5.0를 사용 하는 경우 추가 구성 단계를 수행 해야 합니다.

## <a name="integrated-versus-classic-mode"></a>통합 모드 및 클래식 모드

IIS 7.0는 서로 다른 두 가지 요청 처리 모드인 통합 및 클래식 모드를 사용 하 여 요청을 처리할 수 있습니다. 통합 모드는 더 나은 성능과 더 많은 기능을 제공 합니다. 클래식 모드는 이전 버전의 IIS와 이전 버전과의 호환성을 위해 포함 되었습니다.

요청 처리 모드는 응용 프로그램 풀에 의해 결정 됩니다. 응용 프로그램과 연결 된 응용 프로그램 풀을 확인 하 여 특정 웹 응용 프로그램에서 사용 하는 처리 모드를 확인할 수 있습니다. 다음 단계를 수행하세요.

1. 인터넷 정보 서비스 관리자를 시작 합니다.
2. 연결 창에서 응용 프로그램을 선택 합니다.
3. 작업 창에서 **기본 설정** 링크를 클릭 하 여 응용 프로그램 편집 대화 상자를 엽니다 (그림 1 참조).
4. 선택한 응용 프로그램 풀을 기록해 둡니다.

기본적으로 IIS는 **DefaultAppPool** 및 **클래식 .net AppPool**의 두 가지 응용 프로그램 풀을 지원 하도록 구성 됩니다. DefaultAppPool를 선택 하면 응용 프로그램이 통합 요청 처리 모드로 실행 됩니다. 클래식 .NET AppPool이 선택 되어 있으면 응용 프로그램이 클래식 요청 처리 모드로 실행 되 고 있는 것입니다.

[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image1.png)

**그림 1**: 요청 처리 모드 검색 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.png))

응용 프로그램 편집 대화 상자에서 요청 처리 모드를 수정할 수 있습니다. 선택 단추를 클릭 하 고 응용 프로그램과 연결 된 응용 프로그램 풀을 변경 합니다. 클래식 모드에서 통합 모드로 ASP.NET 응용 프로그램을 변경 하는 경우 호환성 문제가 있음을 알 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.

- Windows Vista 및 Windows Server 2008에서 ASP.NET 1.1를 IIS 7.0로 업그레이드 [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/upgrading-aspnet-11-to-iis-on-windows-vista-and-windows-server-2008)
- ASP.NET와 IIS 7.0 통합- [https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis](https://www.iis.net/learn/application-frameworks/building-and-running-aspnet-applications/aspnet-integration-with-iis)

ASP.NET 응용 프로그램에서 DefaultAppPool를 사용 하는 경우 추가 단계를 수행 하 여 ASP.NET 라우팅 (그리고 따라서 ASP.NET MVC)이 작동 하도록 할 필요가 없습니다. 그러나 ASP.NET 응용 프로그램이 클래식 .NET AppPool을 사용 하도록 구성 된 경우에는 계속 해 서 읽기 작업을 수행 해야 합니다.

## <a name="using-aspnet-mvc-with-older-versions-of-iis"></a>이전 버전의 IIS에서 ASP.NET MVC 사용

Iis 7.0 보다 이전 버전의 IIS에서 ASP.NET MVC를 사용 해야 하거나 클래식 모드에서 IIS 7.0를 사용 해야 하는 경우에는 두 가지 옵션이 있습니다. 먼저, 경로 테이블을 수정 하 여 파일 확장명을 사용할 수 있습니다. 예를 들어/Dv/cvdetails와 같은 URL을 요청 하는 대신/Store.aspx/Details.와 같은 URL을 요청 합니다.

두 번째 옵션은 *와일드 카드 스크립트 맵*이라는 항목을 만드는 것입니다. 와일드 카드 스크립트 맵을 사용 하면 모든 요청을 ASP.NET 프레임 워크에 매핑할 수 있습니다.

웹 서버에 대 한 액세스 권한이 없는 경우 (예: ASP.NET MVC 응용 프로그램이 인터넷 서비스 공급자에 의해 호스트 되는 경우) 첫 번째 옵션을 사용 해야 합니다. Url의 모양을 수정 하지 않고 웹 서버에 액세스할 수 있는 경우 두 번째 옵션을 사용할 수 있습니다.

다음 섹션에서 각 옵션에 대해 자세히 살펴봅니다.

## <a name="adding-extensions-to-the-route-table"></a>경로 테이블에 확장 추가

이전 버전의 IIS에서 작동 하도록 ASP.NET 라우팅을 가져오는 가장 쉬운 방법은 global.asax 파일에서 경로 테이블을 수정 하는 것입니다. 목록 1의 기본 및 수정 되지 않은 global.asax 파일은 기본 경로 라는 하나의 경로를 구성 합니다.

**목록 1-global.asax (수정 되지 않음)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample1.cs)]

목록 1에서 구성 된 기본 경로를 사용 하면 다음과 같은 Url을 라우팅할 수 있습니다.

/Home/Index

/Product/Details/3

/Product

아쉽게도 이전 버전의 IIS는 이러한 요청을 ASP.NET 프레임 워크에 전달 하지 않습니다. 따라서 이러한 요청은 컨트롤러에 라우팅되지 않습니다. 예를 들어/Home/Index URL에 대 한 브라우저 요청을 만들면 그림 2의 오류 페이지가 표시 됩니다.

[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image2.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.png)

**그림 2**: 404를 찾을 수 없음 오류 수신 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.png))

이전 버전의 IIS는 특정 요청을 ASP.NET 프레임 워크에 매핑합니다. 올바른 파일 확장명을 포함 하는 URL에 대 한 요청 이어야 합니다. 예를 들어/SomePage.aspx에 대 한 요청은 ASP.NET 프레임 워크에 매핑됩니다. 그러나/SomePage.htm에 대 한 요청은 그렇지 않습니다.

따라서 ASP.NET 라우팅이 작동 하려면 ASP.NET 프레임 워크에 매핑되는 파일 확장명을 포함 하도록 기본 경로를 수정 해야 합니다.

`registermvc.wsf`이라는 스크립트를 사용 하 여이 작업을 수행 합니다. ASP.NET MVC 1 릴리스에는 `C:\Program Files\Microsoft ASP.NET\ASP.NET MVC\Scripts`에 포함 되어 있지만 ASP.NET 2부터이 스크립트는 [http://aspnet.codeplex.com/releases/view/39978](http://aspnet.codeplex.com/releases/view/39978)에서 사용할 수 있는 ASP.NET 퓨처로 이동 되었습니다.

이 스크립트를 실행 하면 IIS를 사용 하 여 새로운 mvc 확장이 등록 됩니다. Mvc 확장명을 등록 한 후에는 Global.asax 파일에서 경로를 수정 하 여 경로에. i a g 확장명을 사용할 수 있습니다.

목록 2에서 수정 된 global.asax 파일은 이전 버전의 IIS와 함께 작동 합니다.

**목록 2-global.asax (확장으로 수정 됨)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample2.cs)]

**중요**: global.asax 파일을 변경한 후 ASP.NET MVC 응용 프로그램을 다시 빌드해야 합니다.

목록 2의 Global.asax 파일에는 두 가지 중요 한 변경 사항이 있습니다. 이제 Global.asax에 정의 된 두 개의 경로가 있습니다. 기본 경로에 대 한 URL 패턴 인 첫 번째 경로는 다음과 같습니다.

{controller}.mvc/{action}/{id}

. M a m 확장명을 추가 하면 ASP.NET 라우팅 모듈이 가로채는 파일 형식을 변경 합니다. 이러한 변경으로 ASP.NET MVC 응용 프로그램은 이제 다음과 같은 요청을 라우팅합니다.

/Home.mvc/Index/

/Product.mvc/Details/3

/Product.mvc/

두 번째 경로인 루트 경로는 new입니다. 루트 경로에 대 한이 URL 패턴은 빈 문자열입니다. 이 경로는 응용 프로그램의 루트에 대해 수행 된 요청을 일치 시키는 데 필요 합니다. 예를 들어 루트 경로는 다음과 같은 요청과 일치 합니다.

[http://www.YourApplication.com/](http://www.YourApplication.com/)

경로 테이블을 수정한 후에는 응용 프로그램의 모든 링크가 이러한 새 URL 패턴과 호환 되는지 확인 해야 합니다. 즉, 모든 링크에 해당 하는 확장명을 포함 해야 합니다. Html.actionlink () 도우미 메서드를 사용 하 여 링크를 생성 하는 경우 변경할 필요가 없습니다.

Registermvc. wcf 스크립트를 사용 하는 대신 ASP.NET framework에 직접 매핑된 IIS에 새 확장을 추가할 수 있습니다. 새 확장을 직접 추가 하는 경우 **해당 파일이 있는지 확인** 확인란을 선택 하지 않았는지 확인 합니다.

## <a name="hosted-server"></a>호스팅된 서버

웹 서버에 대 한 액세스 권한이 항상 있는 것은 아닙니다. 예를 들어 인터넷 호스팅 공급자를 사용 하 여 ASP.NET MVC 응용 프로그램을 호스트 하는 경우 IIS에 대 한 액세스 권한이 반드시 있어야 하는 것은 아닙니다.

이 경우 ASP.NET framework에 매핑되는 기존 파일 확장명 중 하나를 사용 해야 합니다. ASP.NET에 매핑되는 파일 확장명의 예로는 .aspx, trace.axd 및 .ashx 확장명이 있습니다.

예를 들어 목록 3의 수정 된 global.asax 파일은. x 확장명 대신 .aspx 확장명을 사용 합니다.

**목록 3-global.asax (.aspx 확장명으로 수정 됨)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample3.cs)]

목록 3의 Global.asax 파일은 이전 global.asax 파일과 정확히 동일 합니다. 단,이 파일은 확장명이. x x x 인 확장명이 아닌 .aspx 확장명을 사용 합니다. .Aspx 확장을 사용 하기 위해 원격 웹 서버에서 설치를 수행할 필요가 없습니다.

## <a name="creating-a-wildcard-script-map"></a>와일드 카드 스크립트 매핑 만들기

ASP.NET MVC 응용 프로그램에 대 한 Url을 수정 하지 않고 웹 서버에 액세스할 수 있는 경우에는 추가 옵션을 사용할 수 있습니다. 웹 서버에 대 한 모든 요청을 ASP.NET 프레임 워크로 매핑하는 와일드 카드 스크립트 맵을 만들 수 있습니다. 이렇게 하면 기본 ASP.NET MVC 경로 테이블을 IIS 7.0 (클래식 모드) 또는 IIS 6.0과 함께 사용할 수 있습니다.

이 옵션을 선택 하면 IIS에서 웹 서버에 대해 수행 된 모든 요청을 가로챕니다. 여기에는 이미지, 기본 ASP 페이지 및 HTML 페이지에 대 한 요청이 포함 됩니다. 따라서 와일드 카드 스크립트 맵을 ASP.NET에 사용 하도록 설정 하면 성능에 영향을 줍니다.

IIS 7.0에 대 한 와일드 카드 스크립트 맵을 사용 하도록 설정 하는 방법은 다음과 같습니다.

1. 연결 창에서 응용 프로그램을 선택 합니다.
2. **기능** 보기가 선택 되어 있는지 확인 합니다.
3. **처리기 매핑** 단추를 두 번 클릭 합니다.
4. **와일드 카드 스크립트 매핑 추가** 링크를 클릭 합니다 (그림 3 참조).
5. Aspnet\_isapi .dll 파일의 경로를 입력 합니다 (이 경로를 PageHandlerFactory 스크립트 맵에서 복사할 수 있음).
6. 이름 MVC 입력
7. **확인** 단추를 클릭 합니다.

[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image3.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.png)

**그림 3**: IIS 7.0를 사용 하 여 와일드 카드 스크립트 매핑 만들기 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image6.png))

IIS 6.0를 사용 하 여 와일드 카드 스크립트 맵을 만들려면 다음 단계를 따르세요.

1. 웹 사이트를 마우스 오른쪽 단추로 클릭 하 고 속성을 선택 합니다.
2. **홈 디렉터리** 탭을 선택 합니다.
3. **구성** 단추를 클릭 합니다.
4. **매핑** 탭 선택
5. **삽입** 단추를 클릭 합니다 (그림 4 참조).
6. Aspnet\_의 경로를 실행 파일 필드에 붙여넣습니다 (.aspx 파일에 대 한 스크립트 맵에서이 경로를 복사할 수 있음).
7. **해당 파일이 있는지 확인** 이라는 레이블이 지정 된 확인란의 선택을 취소 합니다.
8. **확인** 단추를 클릭 합니다.

[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image4.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image7.png)

**그림 4**: IIS 6.0를 사용 하 여 와일드 카드 스크립트 매핑 만들기 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image8.png))

와일드 카드 스크립트 맵을 사용 하도록 설정한 후에는 루트 경로를 포함 하도록 Global.asax 파일의 경로 테이블을 수정 해야 합니다. 그렇지 않으면 응용 프로그램의 루트 페이지에 대 한 요청을 수행할 때 그림 5의 오류 페이지가 표시 됩니다. 목록 4에서 수정 된 global.asax 파일을 사용할 수 있습니다.

[새 프로젝트 대화 상자 ![](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image5.jpg)](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image9.png)

**그림 5**: 루트 경로 오류 누락 ([전체 크기 이미지를 보려면 클릭](using-asp-net-mvc-with-different-versions-of-iis-cs/_static/image10.png))

**목록 4-global.asax (루트 경로를 사용 하 여 수정 됨)**

[!code-csharp[Main](using-asp-net-mvc-with-different-versions-of-iis-cs/samples/sample4.cs)]

IIS 7.0 또는 IIS 6.0에 대해 와일드 카드 스크립트 맵을 사용 하도록 설정한 후 다음과 같이 기본 경로 테이블에서 작동 하는 요청을 만들 수 있습니다.

/

/Home/Index

/Product/Details/3

/Product

## <a name="summary"></a>요약

이 자습서의 목표는 이전 버전의 IIS를 사용 하는 경우 ASP.NET MVC를 사용 하는 방법, 즉 클래식 모드에서 IIS 7.0를 사용 하는 방법을 설명 하는 것입니다. ASP.NET 라우팅은 이전 버전의 IIS에서 작동 하는 두 가지 방법, 즉 기본 경로 테이블 수정 또는 와일드 카드 스크립트 맵 만들기에 대해 설명 했습니다.

첫 번째 옵션을 사용 하려면 ASP.NET MVC 응용 프로그램에서 사용 되는 Url을 수정 해야 합니다. 이 첫 번째 옵션의 가장 큰 이점 중 하나는 경로 테이블을 수정 하기 위해 웹 서버에 액세스할 필요가 없다는 것입니다. 즉, 인터넷 호스팅 회사에서 ASP.NET MVC 응용 프로그램을 호스트 하는 경우에도이 첫 번째 옵션을 사용할 수 있습니다.

두 번째 옵션은 와일드 카드 스크립트 맵을 만드는 것입니다. 이 두 번째 옵션은 Url을 수정할 필요가 없다는 장점이 있습니다. 이 두 번째 옵션의 단점은 ASP.NET MVC 응용 프로그램의 성능에 영향을 줄 수 있다는 것입니다.

> [!div class="step-by-step"]
> [다음](using-asp-net-mvc-with-different-versions-of-iis-vb.md)
