---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: 유닛 테스트 ASP.NET Web API 2 | Microsoft Docs
author: Rick-Anderson
description: 이 지침 및 응용 프로그램에서는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다. 이 자습서에서는 단위 테스트 proj를 포함 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78446987"
---
# <a name="unit-testing-aspnet-web-api-2"></a>유닛 테스트 ASP.NET Web API 2

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> 이 지침 및 응용 프로그램에서는 Web API 2 응용 프로그램에 대 한 간단한 단위 테스트를 만드는 방법을 보여 줍니다. 이 자습서에서는 솔루션에 단위 테스트 프로젝트를 포함 하 고 컨트롤러 메서드에서 반환 된 값을 확인 하는 테스트 메서드를 작성 하는 방법을 보여 줍니다.
>
> 이 자습서에서는 사용자가 ASP.NET Web API의 기본 개념을 잘 알고 있다고 가정 합니다. 소개 자습서는 [ASP.NET Web API 2 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)을 참조 하세요.
>
> 이 항목의 단위 테스트는 의도적으로 간단한 데이터 시나리오로 제한 됩니다. 단위 테스트에 대 한 고급 데이터 시나리오는 [단위 테스트를 ASP.NET Web API 때 Entity Framework mock](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)를 참조 하세요.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2

## <a name="in-this-topic"></a>항목 내용

이 항목에는 다음과 같은 섹션이 포함되어 있습니다.

- [필수 구성 요소](#prereqs)
- [코드 다운로드](#download)
- [단위 테스트 프로젝트를 사용 하 여 응용 프로그램 만들기](#appwithunittest)
    - [응용 프로그램을 만들 때 단위 테스트 프로젝트 추가](#whencreate)
    - [기존 응용 프로그램에 단위 테스트 프로젝트 추가](#addtoexisting)
- [Web API 2 응용 프로그램 설정](#setupproject)
- [테스트 프로젝트에 NuGet 패키지 설치](#testpackages)
- [테스트 만들기](#tests)
- [테스트 실행](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a>사전 요구 사항

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional 또는 Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>코드 다운로드

완료 된 [프로젝트](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)를 다운로드 합니다. 다운로드 가능한 프로젝트에는이 항목에 대 한 단위 테스트 코드와 [단위 테스트 ASP.NET Web API 토픽의 모의 Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) 이 포함 되어 있습니다.

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>단위 테스트 프로젝트를 사용 하 여 응용 프로그램 만들기

응용 프로그램을 만들거나 기존 응용 프로그램에 단위 테스트 프로젝트를 추가할 때 단위 테스트 프로젝트를 만들 수 있습니다. 이 자습서에서는 단위 테스트 프로젝트를 만드는 두 가지 방법을 보여 줍니다. 이 자습서를 따르려면 방법 중 하나를 사용할 수 있습니다.

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a>응용 프로그램을 만들 때 단위 테스트 프로젝트 추가

ASP.NET **app**이라는 새 웹 응용 프로그램을 만듭니다.

![프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image1.png)

새 ASP.NET 프로젝트 창에서 **빈** 템플릿을 선택 하 고 Web API에 대 한 폴더 및 핵심 참조를 추가 합니다. **단위 테스트 추가** 옵션을 선택 합니다. 단위 테스트 프로젝트는 자동 **으로 이름이로 지정 됩니다.** 이 이름을 유지할 수 있습니다.

![단위 테스트 프로젝트 만들기](unit-testing-with-aspnet-web-api/_static/image2.png)

응용 프로그램을 만든 후에는 두 개의 프로젝트가 포함 된 것을 볼 수 있습니다.

![두 프로젝트](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a>기존 응용 프로그램에 단위 테스트 프로젝트 추가

응용 프로그램을 만들 때 단위 테스트 프로젝트를 만들지 않은 경우 언제 든 지 추가할 수 있습니다. 예를 들어, 응용 프로그램 이름이 이미 있는 경우에는 단위 테스트를 추가 하려고 합니다. 단위 테스트 프로젝트를 추가 하려면 솔루션을 마우스 오른쪽 단추로 클릭 하 고 **추가** 및 **새 프로젝트**를 선택 합니다.

![솔루션에 새 프로젝트 추가](unit-testing-with-aspnet-web-api/_static/image4.png)

왼쪽 창에서 **테스트** 를 선택 하 고 프로젝트 형식에 대해 **단위 테스트 프로젝트** 를 선택 합니다. 프로젝트의 이름을 **응용 프로그램을 테스트**합니다.

![단위 테스트 프로젝트 추가](unit-testing-with-aspnet-web-api/_static/image5.png)

솔루션에 단위 테스트 프로젝트가 표시 됩니다.

단위 테스트 프로젝트에서 원본 프로젝트에 프로젝트 참조를 추가 합니다.

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a>Web API 2 응용 프로그램 설정

사용자 응용 프로그램 프로젝트에서 **Product.cs**라는 **모델** 폴더에 클래스 파일을 추가 합니다. 파일 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

솔루션을 빌드합니다.

Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 및 **새 스 캐 폴드 항목**을 선택 합니다. **웹 API 2 컨트롤러-비어 있음**을 선택 합니다.

![새 컨트롤러 추가](unit-testing-with-aspnet-web-api/_static/image6.png)

컨트롤러 이름을 **SimpleProductController**로 설정 하 고 **추가**를 클릭 합니다.

![컨트롤러 지정](unit-testing-with-aspnet-web-api/_static/image7.png)

기존 코드를 다음 코드로 바꿉니다. 이 예를 간소화 하기 위해 데이터는 데이터베이스가 아닌 목록에 저장 됩니다. 이 클래스에 정의 된 목록은 프로덕션 데이터를 나타냅니다. 컨트롤러에는 제품 개체 목록을 매개 변수로 사용 하는 생성자가 포함 되어 있습니다. 이 생성자를 사용 하면 단위 테스트 시 테스트 데이터를 전달할 수 있습니다. 또한 컨트롤러에는 비동기 메서드의 단위 테스트를 보여 주는 두 개의 **비동기** 메서드가 포함 되어 있습니다. 이러한 비동기 메서드는 불필요 한 코드를 최소화 하기 위해 **Task. FromResult** 를 호출 하 여 구현 되었지만 일반적으로는 리소스를 많이 사용 하는 작업을 포함 합니다.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

GetProduct 메서드는 **IHttpActionResult** 인터페이스의 인스턴스를 반환 합니다. IHttpActionResult는 Web API 2의 새로운 기능 중 하나로, 단위 테스트 개발을 간소화 합니다. IHttpActionResult 인터페이스를 구현 하는 클래스는 System.web. [Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) 네임 스페이스에 있습니다. 이러한 클래스는 작업 요청에서 발생 가능한 응답을 나타내며 HTTP 상태 코드에 해당 합니다.

솔루션을 빌드합니다.

이제 테스트 프로젝트를 설정할 준비가 되었습니다.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>테스트 프로젝트에 NuGet 패키지 설치

빈 템플릿을 사용 하 여 응용 프로그램을 만드는 경우 단위 테스트 프로젝트 (사용자 응용 프로그램 테스트)에는 설치 된 NuGet 패키지가 포함 되지 않습니다. Web API 템플릿과 같은 다른 템플릿에는 단위 테스트 프로젝트의 일부 NuGet 패키지가 포함 됩니다. 이 자습서에서는 Microsoft ASP.NET Web API 2 Core 패키지를 테스트 프로젝트에 포함 해야 합니다.

마우스 오른쪽 단추를 클릭 하 여 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다. 해당 프로젝트에 패키지를 추가 하려면 사용자 응용 프로그램. 테스트 프로젝트를 선택 해야 합니다.

![패키지 관리](unit-testing-with-aspnet-web-api/_static/image8.png)

Microsoft ASP.NET Web API 2 핵심 패키지를 찾아서 설치 합니다.

![web api core 패키지 설치](unit-testing-with-aspnet-web-api/_static/image9.png)

NuGet 패키지 관리 창을 닫습니다.

<a id="tests"></a>
## <a name="create-tests"></a>테스트 만들기

기본적으로 테스트 프로젝트에는 UnitTest1.cs 라는 빈 테스트 파일이 포함 되어 있습니다. 이 파일은 테스트 메서드를 만드는 데 사용 하는 특성을 보여 줍니다. 단위 테스트의 경우이 파일을 사용 하거나 파일을 직접 만들 수 있습니다.

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

이 자습서에서는 사용자 고유의 테스트 클래스를 만듭니다. UnitTest1.cs 파일을 삭제할 수 있습니다. **TestSimpleProductController.cs**라는 클래스를 추가 하 고 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>테스트 실행

이제 테스트를 실행할 준비가 되었습니다. **TestMethod** 특성으로 표시 된 모든 메서드는 테스트 됩니다. **테스트** 메뉴 항목에서 테스트를 실행 합니다.

![테스트 실행](unit-testing-with-aspnet-web-api/_static/image11.png)

**테스트 탐색기** 창을 열고 테스트 결과를 확인 합니다.

![테스트 결과](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a>요약

이 자습서를 완료했습니다. 이 자습서의 데이터는 단위 테스트 조건에 초점을 맞춘 의도적으로 간소화 되었습니다. 단위 테스트에 대 한 고급 데이터 시나리오는 [단위 테스트를 ASP.NET Web API 때 Entity Framework mock](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)를 참조 하세요.
