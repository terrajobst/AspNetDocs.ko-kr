---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: 유닛 테스트 ASP.NET Web API 2 | Entity Framework 모의 Microsoft Docs
author: Rick-Anderson
description: 이 지침 및 응용 프로그램에서는 Entity Framework를 사용 하는 Web API 2 응용 프로그램에 대 한 단위 테스트를 만드는 방법을 보여 줍니다. 다음을 수정 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447089"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a>유닛 테스트 ASP.NET Web API 2 Entity Framework 모의

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> 이 지침 및 응용 프로그램에서는 Entity Framework를 사용 하는 Web API 2 응용 프로그램에 대 한 단위 테스트를 만드는 방법을 보여 줍니다. 스 캐 폴드 컨트롤러를 수정 하 여 테스트를 위해 컨텍스트 개체를 전달할 수 있도록 하는 방법과 Entity Framework 작업 하는 테스트 개체를 만드는 방법을 보여 줍니다.
>
> ASP.NET Web API를 사용한 단위 테스트에 대 한 소개는 [ASP.NET Web API 2를 사용한 단위 테스트](unit-testing-with-aspnet-web-api.md)를 참조 하세요.
>
> 이 자습서에서는 사용자가 ASP.NET Web API의 기본 개념을 잘 알고 있다고 가정 합니다. 소개 자습서는 [ASP.NET Web API 2 시작](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)을 참조 하세요.
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
- [모델 클래스 만들기](#modelclass)
- [컨트롤러 추가](#controller)
- [종속성 주입 추가](#dependency)
- [테스트 프로젝트에 NuGet 패키지 설치](#testpackages)
- [테스트 컨텍스트 만들기](#testcontext)
- [테스트 만들기](#tests)
- [테스트 실행](#runtests)

[ASP.NET Web API 2를 사용 하 여 단위 테스트](unit-testing-with-aspnet-web-api.md)의 단계를 이미 완료 한 경우에는 [컨트롤러 추가](#controller)섹션으로 건너뛸 수 있습니다.

<a id="prereqs"></a>
## <a name="prerequisites"></a>사전 요구 사항

Visual Studio 2017 Community, Professional 또는 Enterprise edition

<a id="download"></a>
## <a name="download-code"></a>코드 다운로드

완료 된 [프로젝트](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)를 다운로드 합니다. 다운로드 가능한 프로젝트에는이 항목에 대 한 단위 테스트 코드와 [단위 테스트 ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) 항목 항목이 포함 되어 있습니다.

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>단위 테스트 프로젝트를 사용 하 여 응용 프로그램 만들기

응용 프로그램을 만들거나 기존 응용 프로그램에 단위 테스트 프로젝트를 추가할 때 단위 테스트 프로젝트를 만들 수 있습니다. 이 자습서에서는 응용 프로그램을 만들 때 단위 테스트 프로젝트를 만드는 방법을 보여 줍니다.

ASP.NET **app**이라는 새 웹 응용 프로그램을 만듭니다.

새 ASP.NET 프로젝트 창에서 **빈** 템플릿을 선택 하 고 Web API에 대 한 폴더 및 핵심 참조를 추가 합니다. **단위 테스트 추가** 옵션을 선택 합니다. 단위 테스트 프로젝트는 자동 **으로 이름이로 지정 됩니다.** 이 이름을 유지할 수 있습니다.

![단위 테스트 프로젝트 만들기](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

응용 프로그램을 만든 후에는 해당 응용 프로그램에 두 개의 **프로젝트를 포함** 하는 것을 볼 수 **있습니다.**

<a id="modelclass"></a>
## <a name="create-the-model-class"></a>모델 클래스 만들기

사용자 응용 프로그램 프로젝트에서 **Product.cs**라는 **모델** 폴더에 클래스 파일을 추가 합니다. 파일 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

솔루션을 빌드합니다.

<a id="controller"></a>
## <a name="add-the-controller"></a>컨트롤러 추가

Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** 및 **새 스 캐 폴드 항목**을 선택 합니다. Entity Framework를 사용 하 여 작업을 포함 하는 Web API 2 컨트롤러를 선택 합니다.

![새 컨트롤러 추가](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

다음 값을 설정합니다.

- 컨트롤러 이름: **제품 컨트롤러**
- 모델 클래스: **Product**
- 데이터 컨텍스트 클래스: [아래에 표시 된 값을 채우는 **새 데이터 컨텍스트** 단추 선택]

![컨트롤러 지정](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

**추가** 를 클릭 하 여 자동으로 생성 된 코드를 사용 하 여 컨트롤러를 만듭니다. 이 코드에는 Product 클래스의 인스턴스를 만들고, 검색 하 고, 업데이트 하 고, 삭제 하는 메서드가 포함 되어 있습니다. 다음 코드는 제품을 추가 하는 메서드를 보여 줍니다. 이 메서드는 **IHttpActionResult**의 인스턴스를 반환 합니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

IHttpActionResult는 Web API 2의 새로운 기능 중 하나로, 단위 테스트 개발을 간소화 합니다.

다음 섹션에서는 테스트 개체를 컨트롤러에 전달 하는 데 도움이 되도록 생성 된 코드를 사용자 지정 합니다.

<a id="dependency"></a>
## <a name="add-dependency-injection"></a>종속성 주입 추가

현재, 제품 컨트롤러 클래스는 하드 코드 되어 있으므로이 클래스의 인스턴스를 사용할 수 있습니다. 종속성 주입 이라고 하는 패턴을 사용 하 여 응용 프로그램을 수정 하 고 하드 코드 된 종속성을 제거 합니다. 이 종속성을 위반 하면 테스트할 때 모의 개체를 전달할 수 있습니다.

**모델** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **IStoreAppContext**이라는 새 인터페이스를 추가 합니다.

코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

StoreAppContext.cs 파일을 열고 다음과 같이 강조 표시를 변경 합니다. 유의 해야 할 중요 한 사항은 다음과 같습니다.

- IStoreAppContext Appcontext 클래스는 인터페이스를 구현 합니다.
- MarkAsModified 메서드를 구현 합니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

ProductController.cs 파일을 엽니다. 강조 표시 된 코드와 일치 하도록 기존 코드를 변경 합니다. 이러한 변경 내용으로 인해에는가 나 Appcontext에 대 한 종속성이 중단 되 고 다른 클래스가 컨텍스트 클래스에 대해 다른 개체를 전달할 수 있습니다. 이렇게 변경 하면 단위 테스트 중에 테스트 컨텍스트를 전달할 수 있습니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

제품 컨트롤러에서 수행 해야 하는 변경 내용이 하나 더 있습니다. **Putproduct** 메서드에서 엔터티 상태를 설정 하는 줄을 MarkAsModified 메서드에 대 한 호출로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

솔루션을 빌드합니다.

이제 테스트 프로젝트를 설정할 준비가 되었습니다.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>테스트 프로젝트에 NuGet 패키지 설치

빈 템플릿을 사용 하 여 응용 프로그램을 만드는 경우 단위 테스트 프로젝트 (사용자 응용 프로그램 테스트)에는 설치 된 NuGet 패키지가 포함 되지 않습니다. Web API 템플릿과 같은 다른 템플릿에는 단위 테스트 프로젝트의 일부 NuGet 패키지가 포함 됩니다. 이 자습서에서는 Entity Framework 패키지와 Microsoft ASP.NET Web API 2 Core 패키지를 테스트 프로젝트에 포함 해야 합니다.

마우스 오른쪽 단추를 클릭 하 여 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **NuGet 패키지 관리**를 선택 합니다. 해당 프로젝트에 패키지를 추가 하려면 사용자 응용 프로그램. 테스트 프로젝트를 선택 해야 합니다.

![패키지 관리](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

온라인 패키지에서 EntityFramework 패키지 (버전 6.0 이상)를 찾아서 설치 합니다. EntityFramework 패키지가 이미 설치 된 것으로 나타나는 경우에는 사용자 응용 프로그램 프로젝트 대신 파일 앱 프로젝트를 선택 했을 수 있습니다.

![add Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

Microsoft ASP.NET Web API 2 핵심 패키지를 찾아서 설치 합니다.

![web api core 패키지 설치](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

NuGet 패키지 관리 창을 닫습니다.

<a id="testcontext"></a>
## <a name="create-test-context"></a>테스트 컨텍스트 만들기

**Testdbset** 이라는 클래스를 테스트 프로젝트에 추가 합니다. 이 클래스는 테스트 데이터 집합에 대 한 기본 클래스로 사용 됩니다. 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

다음 코드를 포함 하는 테스트 프로젝트에 **Testproductdbset** 이라는 클래스를 추가 합니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

**Teststoreappcontext** 라는 클래스를 추가 하 고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a>테스트 만들기

기본적으로 테스트 프로젝트에는 **UnitTest1.cs**라는 빈 테스트 파일이 포함 되어 있습니다. 이 파일은 테스트 메서드를 만드는 데 사용 하는 특성을 보여 줍니다. 이 자습서에서는 새 테스트 클래스를 추가 하기 때문에이 파일을 삭제할 수 있습니다.

**Test제품 컨트롤러** 라는 클래스를 테스트 프로젝트에 추가 합니다. 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>테스트 실행

이제 테스트를 실행할 준비가 되었습니다. **TestMethod** 특성으로 표시 된 모든 메서드는 테스트 됩니다. **테스트** 메뉴 항목에서 테스트를 실행 합니다.

![테스트 실행](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

**테스트 탐색기** 창을 열고 테스트 결과를 확인 합니다.

![테스트 결과](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
