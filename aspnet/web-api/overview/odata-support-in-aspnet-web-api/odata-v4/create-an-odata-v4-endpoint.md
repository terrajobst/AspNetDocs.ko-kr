---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: ASP.NET Web API 2.2를 사용 하 여 OData v4 엔드포인트 만들기 Microsoft Docs
author: MikeWasson
description: OData (Open Data Protocol)는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 CRUD 작업을 통해 데이터 집합을 쿼리하고 조작 하는 일관 된 방법을 제공 합니다.
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484499"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a>ASP.NET Web API를 사용 하 여 OData v4 엔드포인트 만들기 

> OData (Open Data Protocol)는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 CRUD 작업 (만들기, 읽기, 업데이트 및 삭제)을 통해 데이터 집합을 쿼리하고 조작 하는 일관 된 방법을 제공 합니다.
>
> ASP.NET Web API는 프로토콜의 v3 및 v4를 모두 지원 합니다. V3 끝점과 side-by-side 끝점을 함께 실행 하는 v4 끝점을 사용할 수도 있습니다.
>
> 이 자습서에서는 CRUD 작업을 지 원하는 OData v4 끝점을 만드는 방법을 보여 줍니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
> - 웹 API 5.2
> - OData v4
> - Visual Studio 2017 (Visual [studio 2017 다운로드](https://visualstudio.microsoft.com/downloads/))
> - Entity Framework 6
> - .NET 4.7.2
>
> ## <a name="tutorial-versions"></a>자습서 버전
>
> OData 버전 3의 경우 [odata V3 끝점 만들기](../odata-v3/creating-an-odata-endpoint.md)를 참조 하세요.

## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

Visual Studio의 **파일** 메뉴에서 **새로 만들기** &gt; **프로젝트**를 선택 합니다.

**설치** &gt;  **C# Visual** &gt; **web**을 확장 하 고 **.NET Framework (ASP.NET Web Application)** 템플릿을 선택 합니다. Project &quot;제품 서비스&quot;에 이름을로 합니다.

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

**확인**을 선택합니다.

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

**비어 있는** 템플릿을 선택합니다. **다음에 대 한 폴더 및 핵심 참조 추가:** 에서 **Web API**를 선택 합니다. **확인**을 선택합니다.

## <a name="install-the-odata-packages"></a>OData 패키지 설치

**도구** 메뉴에서 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**을 선택합니다. 패키지 관리자 콘솔 창에서 다음을 입력 합니다.

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

이 명령은 최신 OData NuGet 패키지를 설치 합니다.

## <a name="add-a-model-class"></a>모델 클래스 추가

*모델* 은 응용 프로그램의 데이터 엔터티를 나타내는 개체입니다.

솔루션 탐색기에서 Models 폴더를 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴에서 &gt; **클래스** **추가** 를 선택 합니다.

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> 규칙에 따라 모델 클래스는 모델 폴더에 배치 되지만 사용자 고유의 프로젝트에서이 규칙을 따르지 않아도 됩니다.

클래스 `Product` 이름을 지정합니다. Product.cs 파일에서 상용구 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

`Id` 속성은 엔터티 키입니다. 클라이언트는 키를 기준으로 엔터티를 쿼리할 수 있습니다. 예를 들어 ID가 5 인 제품을 가져오려면 URI가 `/Products(5)`됩니다. 또한 `Id` 속성은 백 엔드 데이터베이스의 기본 키가 됩니다.

## <a name="enable-entity-framework"></a>Entity Framework 사용

이 자습서에서는 EF (Entity Framework) Code First를 사용 하 여 백 엔드 데이터베이스를 만듭니다.

> [!NOTE]
> Web API OData에는 EF가 필요 하지 않습니다. 데이터베이스 엔터티를 모델로 변환할 수 있는 모든 데이터 액세스 계층을 사용 합니다.

먼저 EF 용 NuGet 패키지를 설치 합니다. **도구** 메뉴에서 **NuGet 패키지 관리자** &gt; **패키지 관리자 콘솔**을 선택합니다. 패키지 관리자 콘솔 창에서 다음을 입력 합니다.

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

Web.config 파일을 열고 **구성** 요소 내의 **configsections** 요소 뒤에 다음 섹션을 추가 합니다.

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

이 설정은 LocalDB 데이터베이스에 대 한 연결 문자열을 추가 합니다. 이 데이터베이스는 응용 프로그램을 로컬로 실행할 때 사용 됩니다.

그런 다음 `ProductsContext` 라는 클래스를 모델 폴더에 추가 합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

생성자에서 `"name=ProductsContext"` 연결 문자열의 이름을 제공 합니다.

## <a name="configure-the-odata-endpoint"></a>OData 끝점 구성

File App\_Start/WebApiConfig .cs를 엽니다. 다음 **using** 문을 추가 합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

그런 다음 **Register** 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

이 코드는 다음 두 가지 작업을 수행 합니다.

- EDM (엔터티 데이터 모델)을 만듭니다.
- 경로를 추가 합니다.

EDM은 데이터의 추상 모델입니다. EDM은 서비스 메타 데이터 문서를 만드는 데 사용 됩니다. **ODataConventionModelBuilder** 클래스는 기본 명명 규칙을 사용 하 여 EDM을 만듭니다. 이 방법에는 최소한의 코드가 필요 합니다. EDM을 보다 세부적으로 제어 하려는 경우 **만드는** 클래스를 사용 하 여 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 edm을 만들 수 있습니다.

*경로* 는 HTTP 요청을 끝점으로 라우팅하는 방법을 웹 API에 알려 줍니다. OData v4 경로를 만들려면 **MapODataServiceRoute** 확장 메서드를 호출 합니다.

응용 프로그램에 여러 OData 끝점이 있는 경우 각각에 대해 별도의 경로를 만듭니다. 각 경로에 고유한 경로 이름 및 접두사를 지정 합니다.

## <a name="add-the-odata-controller"></a>OData 컨트롤러 추가

*컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다. OData 서비스의 각 엔터티 집합에 대해 별도의 컨트롤러를 만듭니다. 이 자습서에서는 `Product` 엔터티에 대해 하나의 컨트롤러를 만듭니다.

솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 &gt; **클래스** **추가** 를 선택 합니다. 클래스 `ProductsController` 이름을 지정합니다.

> [!NOTE]
> OData v3에 대 한이 자습서 버전은 컨트롤러 스 캐 폴딩 **추가** 를 사용 합니다. 현재 OData v4에 대 한 스 캐 폴딩이 없습니다.

ProductsController.cs의 상용구 코드를 다음으로 바꿉니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

컨트롤러는 `ProductsContext` 클래스를 사용 하 여 EF를 사용 하 여 데이터베이스에 액세스 합니다. 컨트롤러는 **dispose** 메서드를 재정의 하 여 **ProductsContext**을 삭제 합니다.

컨트롤러의 시작 지점입니다. 다음으로 모든 CRUD 작업에 대 한 메서드를 추가 합니다.

## <a name="query-the-entity-set"></a>엔터티 집합 쿼리

`ProductsController`에 다음 메서드를 추가 합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

매개 변수가 없는 `Get` 메서드의 버전은 전체 Products 컬렉션을 반환 합니다. *키* 매개 변수가 있는 `Get` 메서드는 해당 키를 사용 하 여 제품을 찾습니다 (이 경우에는 `Id` 속성).

**[Enablequery]** 특성을 사용 하면 클라이언트가 $filter, $sort 및 $page 같은 쿼리 옵션을 사용 하 여 쿼리를 수정할 수 있습니다. 자세한 내용은 [OData 쿼리 옵션 지원](../supporting-odata-query-options.md)을 참조 하세요.

## <a name="add-an-entity-to-the-entity-set"></a>엔터티 집합에 엔터티 추가

클라이언트가 데이터베이스에 새 제품을 추가 하도록 하려면 다음 메서드를 추가 하 여 `ProductsController`합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a>엔터티 업데이트

OData는 엔터티 업데이트, 패치 및 PUT에 대 한 두 가지 다른 의미 체계를 지원 합니다.

- 패치는 부분 업데이트를 수행 합니다. 클라이언트는 업데이트할 속성만 지정 합니다.
- PUT은 전체 엔터티를 대체 합니다.

PUT의 단점은 클라이언트는 변경 되지 않는 값을 포함 하 여 엔터티의 모든 속성에 대 한 값을 전송 해야 한다는 것입니다. [OData 사양](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) 에는 패치가 선호 됨이 명시 되어 있습니다.

어떤 경우 든, PATCH 및 PUT 메서드의 코드는 다음과 같습니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

패치의 경우 컨트롤러는 **델타&lt;t&gt;** 유형을 사용 하 여 변경 내용을 추적 합니다.

## <a name="delete-an-entity"></a>엔터티 삭제

클라이언트가 데이터베이스에서 제품을 삭제할 수 있게 하려면 다음 메서드를 `ProductsController`에 추가 합니다.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
