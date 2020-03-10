---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 시작 | Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ca39bc37c757c0452cf56624c8e37c04df4b41f2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487955"
---
# <a name="getting-started-with-aspnet-mvc-5"></a>ASP.NET MVC 5 시작

[Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](../../../../includes/razor.md)]

이 자습서에서는 [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)을 사용 하 여 ASP.NET MVC 5 웹 앱을 빌드하는 기본 사항을 설명 합니다. 자습서의 최종 소스 코드는 [GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)에 있습니다.

이 자습서는 [Scott Guthrie](https://weblogs.asp.net/scottgu/) (twitter[@scottgu](https://twitter.com/scottgu) ), [scott Hanselman](http://www.hanselman.com/blog/) (Twitter: [@shanselman](https://twitter.com/shanselman) ) 및 [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) )에 의해 작성 되었습니다.

Azure에이 앱을 배포 하려면 Azure 계정이 필요 합니다.

- [Azure 계정을 무료로 열](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) 수 있음-유료 azure 서비스를 사용 하는 데 사용할 수 있는 크레딧을 확보 하 고, 사용한 후에도 계정을 유지 하 고 무료 Azure 서비스를 사용할 수 있습니다.
- [MSDN 구독자 혜택을 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) 할 수 있음 - MSDN 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공합니다.

## <a name="get-started"></a>시작하기

[Visual Studio 2017을 설치](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)하 여 시작 합니다. 그런 다음 Visual Studio를 엽니다.

Visual Studio는 IDE 또는 통합 된 개발 환경입니다. Microsoft Word를 사용 하 여 문서를 작성 하는 것 처럼 IDE를 사용 하 여 응용 프로그램을 만듭니다. Visual Studio에는 제공 되는 다양 한 옵션을 보여 주는 목록이 있습니다. IDE에서 작업을 수행 하는 다른 방법을 제공 하는 메뉴도 있습니다. 예를 들어 **시작 페이지**에서 **새 프로젝트** 를 선택 하는 대신 메뉴 모음을 사용 하 여 **파일** > **새 프로젝트**를 선택할 수 있습니다.

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a>첫 번째 앱 만들기

**시작 페이지**에서 **새 프로젝트**를 선택 합니다. **새 프로젝트** 대화 상자에서 왼쪽의 **시각적 C#**  범주를 선택한 다음 **웹**을 선택 하 고 **.NET Framework (ASP.NET web Application)** 프로젝트 템플릿을 선택 합니다. 프로젝트 이름을 "MvcMovie"로 지정한 다음 **확인을**선택 합니다.

![](getting-started/_static/image2.png)

**New ASP.NET 웹 응용 프로그램** 대화 상자에서 **MVC** 를 선택한 다음 **확인**을 선택 합니다.

![](getting-started/_static/image3.png)

Visual Studio는 방금 만든 ASP.NET MVC 프로젝트에 대 한 기본 템플릿을 사용 하 여 작업을 수행 하는 응용 프로그램을 지금 수행 하지 않습니다. 이는 간단한 "Hello World!"입니다. 프로젝트를 시작 하 고 응용 프로그램을 시작 하는 것이 좋습니다.

![](getting-started/_static/image4.png)

**F5** 키를 눌러 디버깅을 시작합니다. **F5**키를 누르면 Visual Studio에서 [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) 시작 하 고 웹 앱을 실행 합니다. 그러면 Visual Studio가 브라우저를 시작 하 고 응용 프로그램의 홈 페이지를 엽니다. 브라우저의 주소 표시줄에 `localhost:port#` 표시 되 고 `example.com`와 같은 것은 아닙니다. `localhost`은 항상 자신의 로컬 컴퓨터를 가리키지만이 경우에는 방금 빌드한 응용 프로그램을 실행 하는 것입니다. Visual Studio에서 웹 프로젝트를 실행 하면 웹 서버에 대해 임의의 포트가 사용 됩니다. 아래 이미지에서 포트 번호는 1234입니다. 응용 프로그램을 실행 하면 다른 포트 번호가 표시 됩니다.

![](getting-started/_static/image5.png)

바로이 기본 템플릿은 `Home`, `Contact`및 `About` 페이지를 제공 합니다. 아래 이미지는 **홈**, **정보**및 **연락처** 링크를 표시 하지 않습니다. 브라우저 창의 크기에 따라 탐색 아이콘을 클릭 하 여 이러한 링크를 확인 해야 할 수도 있습니다.

![](getting-started/_static/image6.png)

응용 프로그램은 등록 및 로그인도 지원 합니다. 다음 단계는이 응용 프로그램의 작동 방식을 변경 하 고 ASP.NET MVC에 대해 약간 자세히 알아보는 것입니다. ASP.NET MVC 응용 프로그램을 닫고 일부 코드를 변경 하겠습니다.

현재 자습서 목록은 [MVC 권장 문서](../mvc-learning-sequence.md)를 참조 하세요.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 앱 확인

완료 된 사이트가 라이브 웹 앱으로 실행 되 고 있는지 확인 하 시겠습니까? 다음 단추를 클릭 하기만 하면 Azure 계정에 전체 버전의 앱을 배포할 수 있습니다.

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음 옵션 중 하나를 사용 하 여 계정을 만듭니다.

- [무료로 azure 계정 열기](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -유료 azure 서비스를 사용 하는 데 사용할 수 있는 크레딧을 확보 하 고, 사용한 후에도 계정을 유지 하 고 무료 Azure 서비스를 사용할 수 있습니다.
- [Visual studio 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) -visual studio 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공 합니다.

> [!div class="step-by-step"]
> [다음](adding-a-controller.md)
