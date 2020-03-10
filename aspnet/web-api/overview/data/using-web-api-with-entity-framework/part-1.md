---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Entity Framework 6에서 Web API 2 사용 Microsoft Docs
author: MikeWasson
description: 이 자습서에서는 ASP.NET Web API 백 엔드를 사용 하 여 웹 응용 프로그램을 만드는 기본 사항을 설명 합니다. 이 자습서에서는 데이터 레이아웃에 Entity Framework 6을 사용 합니다.
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504839"
---
# <a name="using-web-api-2-with-entity-framework-6"></a>Entity Framework 6에 Web API 2 사용

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

> 이 자습서에서는 ASP.NET Web API 백 엔드를 사용 하 여 웹 응용 프로그램을 만드는 기본 사항을 설명 합니다. 이 자습서에서는 데이터 계층에 대해 Entity Framework 6을 사용 하 고 클라이언트 쪽 JavaScript 응용 프로그램에 대해 node.js를 사용 합니다. 또한 Web Apps Azure App Service에 앱을 배포 하는 방법도 보여 줍니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
> - 웹 API 2.1
> - Visual Studio 2017 (Visual [studio 2017 다운로드](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - Entity Framework 6
> - .NET 4.7
> - [녹아웃](http://knockoutjs.com/) 3.1

이 자습서에서는 Entity Framework 6과 함께 ASP.NET Web API 2를 사용 하 여 백 엔드 데이터베이스를 조작 하는 웹 응용 프로그램을 만듭니다. 다음은 만들 응용 프로그램의 스크린샷입니다.

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

앱은 SPA (단일 페이지 응용 프로그램) 디자인을 사용 합니다. "단일 페이지 응용 프로그램"은 단일 HTML 페이지를 로드 한 다음 새 페이지를 로드 하는 대신 페이지를 동적으로 업데이트 하는 웹 응용 프로그램에 대 한 일반적인 용어입니다. 초기 페이지 로드 후에 앱은 AJAX 요청을 통해 서버와 통신 합니다. AJAX 요청은 앱이 UI를 업데이트 하는 데 사용 하는 JSON 데이터를 반환 합니다.

AJAX는 새로운 것은 아니지만 오늘날에는 크고 정교한 SPA 응용 프로그램을 쉽게 빌드하고 유지 관리할 수 있는 JavaScript 프레임 워크가 있습니다. 이 자습서에서는 [node.js](http://knockoutjs.com/)를 사용 하지만 모든 JavaScript 클라이언트 프레임 워크를 사용할 수 있습니다.

이 앱에 대 한 기본 구성 요소는 다음과 같습니다.

- ASP.NET MVC는 HTML 페이지를 만듭니다.
- ASP.NET Web API는 AJAX 요청을 처리 하 고 JSON 데이터를 반환 합니다.
- .Js 데이터-HTML 요소를 JSON 데이터에 바인딩합니다.
- Entity Framework는 데이터베이스와 통신 합니다.

## <a name="see-this-app-running-on-azure"></a>Azure에서 실행 되는이 앱 확인

완료 된 사이트가 라이브 웹 앱으로 실행 되 고 있는지 확인 하 시겠습니까? 다음 단추를 선택 하 여 Azure 계정에 전체 버전의 앱을 배포할 수 있습니다.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

Azure에이 솔루션을 배포 하려면 Azure 계정이 필요 합니다. 계정이 아직 없는 경우 다음과 같은 옵션을 사용할 수 있습니다.

- [무료로 azure 계정 열기](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) -유료 azure 서비스를 사용 하는 데 사용할 수 있는 크레딧을 확보 하 고, 사용한 후에도 계정을 유지 하 고 무료 Azure 서비스를 사용할 수 있습니다.
- [Msdn 구독자 혜택 활성화](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -msdn 구독은 유료 Azure 서비스에 사용할 수 있는 크레딧을 매달 제공 합니다.

## <a name="create-the-project"></a>프로젝트 만들기

Visual Studio를 엽니다. **파일** 메뉴에서 **새로 만들기**를 선택한 다음 **프로젝트**를 선택 합니다. 또는 시작 페이지에서 **새 프로젝트** 를 선택 합니다.

**새 프로젝트** 대화 상자의 왼쪽 창에서 **웹** 을 선택 하 고 가운데 창에서 **ASP.NET 웹 응용 프로그램 (.NET Framework)** 을 선택 합니다. 프로젝트 이름을 **Bookservice** 로 하 고 **확인**을 선택 합니다.

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

**새 ASP.NET 프로젝트** 대화 상자에서 **Web API** 템플릿을 선택 합니다.

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

**확인**을 선택하여 프로젝트를 만듭니다.

## <a name="configure-azure-settings-optional"></a>Azure 설정 구성 (선택 사항)

프로젝트를 만든 후 언제 든 지 Azure App Service Web Apps에 배포 하도록 선택할 수 있습니다. 

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

2. 표시 되는 창에서 **시작**을 선택 합니다. **게시 대상 선택** 대화 상자가 나타납니다.

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. **프로필 만들기**를 선택합니다. **App Service 만들기** 대화 상자가 나타납니다.

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   기본값을 그대로 적용 하거나 응용 프로그램 이름, 리소스 그룹, 호스팅 계획, Azure 구독 및 지리적 지역에 대해 다른 값을 입력 합니다. 

4. **SQL 데이터베이스 만들기를**선택 합니다. **SQL Server 구성** 대화 상자가 나타납니다. 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   기본값을 그대로 적용 하거나 다른 값을 입력 합니다. 새 데이터베이스에 대 한 **관리자 사용자 이름** 및 **관리자 암호** 를 입력 합니다. 완료 되 면 **확인을** 선택 합니다. **App Service 만들기** 페이지가 다시 나타납니다.

5. **만들기** 를 선택 하 여 프로필을 만듭니다. 배포가 진행 중임을 나타내는 메시지가 오른쪽 아래 모퉁이에 표시 됩니다. 잠시 후에 **게시** 창이 다시 나타납니다.

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    앱을 배포 하기 위해 만든 프로필을 이제 사용할 수 있습니다. 

> [!div class="step-by-step"]
> [다음](part-2.md)
