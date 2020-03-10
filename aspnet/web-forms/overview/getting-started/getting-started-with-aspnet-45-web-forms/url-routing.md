---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 라우팅 | Microsoft Docs
author: Erikre
description: 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다.
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474815"
---
# <a name="url-routing"></a>URL 라우팅

[Erik Reitan](https://github.com/Erikre)

[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> 이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio Express 2013 for Web을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 기본 사항을 설명 합니다. [소스 코드를 포함 C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 하는 Visual Studio 2013 프로젝트는이 자습서 계열과 함께 사용할 수 있습니다.

이 자습서에서는 URL 라우팅을 지원 하도록 정문 장난감 샘플 응용 프로그램을 수정 합니다. 라우팅을 사용 하면 웹 응용 프로그램에서 친숙 하 고 쉽게 기억할 수 있는 Url을 사용 하 고 검색 엔진에서 지원할 수 있습니다. 이 자습서는 이전 자습서 "멤버 자격 및 관리"를 기반으로 하며, 정문 장난감 자습서 시리즈의 일부입니다.

## <a name="what-youll-learn"></a>학습할 내용:

- ASP.NET Web Forms 응용 프로그램에 대 한 경로를 등록 하는 방법입니다.
- 웹 페이지에 경로를 추가 하는 방법
- 경로를 지원 하기 위해 데이터베이스에서 데이터를 선택 하는 방법

## <a name="aspnet-routing-overview"></a>ASP.NET 라우팅 개요

URL 라우팅을 사용 하면 실제 파일에 매핑되지 않는 요청 Url을 허용 하도록 응용 프로그램을 구성할 수 있습니다. 요청 URL은 웹 사이트에서 페이지를 찾기 위해 사용자가 브라우저에 입력 하는 URL입니다. 라우팅을 사용 하 여 사용자에 게 의미 있는 의미 있는 Url을 정의 하 고 SEO (검색 엔진 최적화)에 도움이 될 수 있습니다.

기본적으로 Web Forms 템플릿에는 [ASP.NET 친화적인 url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)이 포함 되어 있습니다. 기본 라우팅 작업의 대부분은 *친숙 한 url*을 사용 하 여 구현 됩니다. 그러나이 자습서에서는 사용자 지정 된 라우팅 기능을 추가 합니다.

URL 라우팅을 사용자 지정 하기 전에 다음 URL을 사용 하 여 정문 장난감 샘플 응용 프로그램을 제품에 연결할 수 있습니다.

`https://localhost:44300/ProductDetails.aspx?productID=2`

URL 라우팅을 사용자 지정 하 여 URL을 더 쉽게 읽을 수 있도록 정문 장난감 샘플 응용 프로그램이 동일한 제품에 연결 됩니다.

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a>경로

경로는 처리기에 매핑되는 URL 패턴입니다. 처리기는 Web Forms 응용 프로그램의 .aspx 파일과 같은 물리적 파일이 될 수 있습니다. 처리기는 요청을 처리 하는 클래스 일 수도 있습니다. 경로를 정의 하려면 경로 클래스의 인스턴스를 만듭니다. 여기에는 URL 패턴, 처리기 및 경로 이름 (선택 사항)을 지정 합니다.

`RouteTable` 클래스의 정적 `Routes` 속성에 `Route` 개체를 추가 하 여 응용 프로그램에 경로를 추가 합니다. 경로 속성은 응용 프로그램에 대 한 모든 경로를 저장 하는 `RouteCollection` 개체입니다.

### <a name="url-patterns"></a>URL 패턴

URL 패턴에는 리터럴 값과 변수 자리 표시자 (URL 매개 변수 라고 함)가 포함 될 수 있습니다. 리터럴과 자리 표시자는 슬래시 (`/`) 문자로 구분 되는 URL의 세그먼트에 있습니다.

웹 응용 프로그램에 대 한 요청을 만들면 URL은 세그먼트와 자리 표시자로 구문 분석 되 고 변수 값은 요청 처리기에 제공 됩니다. 이 프로세스는 쿼리 문자열의 데이터를 구문 분석 하 여 요청 처리기에 전달 하는 방법과 비슷합니다. 두 경우 모두 변수 정보는 URL에 포함 되 고 키-값 쌍 형식으로 처리기에 전달 됩니다. 쿼리 문자열의 경우 키와 값은 모두 URL에 있습니다. 경로의 경우 키는 URL 패턴에 정의 된 자리 표시자 이름이 고, 값만 URL에 있습니다.

URL 패턴에서 자리 표시자를 중괄호 (`{` 및 `}`)로 묶어 정의 합니다. 세그먼트에 두 개 이상의 자리 표시자를 정의할 수 있지만 자리 표시자를 리터럴 값으로 구분 해야 합니다. 예를 들어 `{language}-{country}/{action}`은 유효한 경로 패턴입니다. 그러나 자리 표시자 사이에 리터럴 값 이나 구분 기호가 없기 때문에 `{language}{country}/{action}`은 올바른 패턴이 아닙니다. 따라서 라우팅은 국가 자리 표시자에 대 한 값에서 언어 자리 표시자 값을 분리할 위치를 결정할 수 없습니다.

### <a name="mapping-and-registering-routes"></a>경로 매핑 및 등록

정문 장난감 샘플 응용 프로그램의 페이지에 대 한 경로를 포함 하려면 먼저 응용 프로그램이 시작 될 때 경로를 등록 해야 합니다. 경로를 등록 하려면 `Application_Start` 이벤트 처리기를 수정 합니다.

1. Visual Studio **솔루션 탐색기**에서 *Global.asax.cs* 파일을 찾아 엽니다.
2. 다음과 같이 노란색으로 강조 표시 된 코드를 *Global.asax.cs* 파일에 추가 합니다.   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

정문 장난감 샘플 응용 프로그램이 시작 되 면 `Application_Start` 이벤트 처리기가 호출 됩니다. 이 이벤트 처리기의 끝 부분에서 `RegisterCustomRoutes` 메서드가 호출 됩니다. `RegisterCustomRoutes` 메서드는 `RouteCollection` 개체의 `MapPageRoute` 메서드를 호출 하 여 각 경로를 추가 합니다. 경로는 경로 이름, 경로 URL 및 실제 URL을 사용 하 여 정의 됩니다.

첫 번째 매개 변수 ("`ProductsByCategoryRoute`")는 경로 이름입니다. 필요할 때 경로를 호출 하는 데 사용 됩니다. 두 번째 매개 변수 ("`Category/{categoryName}`")는 코드에 따라 동적으로 사용할 수 있는 대체 URL을 정의 합니다. 데이터를 기반으로 생성 된 링크를 사용 하 여 데이터 컨트롤을 채울 때이 경로를 사용 합니다. 경로는 다음과 같이 표시 됩니다.

[!code-csharp[Main](url-routing/samples/sample2.cs)]

경로의 두 번째 매개 변수에는 중괄호 (`{ }`)로 지정 된 동적 값이 포함 됩니다. 이 경우 `categoryName`은 적절 한 라우팅 경로를 결정 하는 데 사용 되는 변수입니다.

> [!NOTE] 
> 
> **선택 사항**
> 
> `RegisterCustomRoutes` 메서드를 별도의 클래스로 이동 하 여 코드를 보다 쉽게 관리할 수 있습니다. *논리* 폴더에서 별도의 `RouteActions` 클래스를 만듭니다. *Global.asax.cs* 파일에서 위의 `RegisterCustomRoutes` 메서드를 새 `RoutesActions` 클래스로 이동 합니다. *Global.asax.cs* 파일에서 `RegisterCustomRoutes` 메서드를 호출 하는 방법의 예로 `RoleActions` 클래스 및 `createAdmin` 메서드를 사용 합니다.

`Application_Start` 이벤트 처리기의 시작 부분에서 `RouteConfig` 개체를 사용 하 여 `RegisterRoutes` 메서드 호출을 발견할 수도 있습니다. 이 호출은 기본 라우팅을 구현 하기 위해 수행 됩니다. Visual Studio의 Web Forms 템플릿을 사용 하 여 응용 프로그램을 만들 때 기본 코드로 포함 되었습니다.

## <a name="retrieving-and-using-route-data"></a>경로 데이터 검색 및 사용

위에서 설명한 것 처럼 경로를 정의할 수 있습니다. *Global.asax.cs* 파일에서 `Application_Start` 이벤트 처리기에 추가한 코드는 정의 가능한 경로를 로드 합니다.

### <a name="setting-routes"></a>경로 설정

경로를 추가 하려면 코드를 추가 해야 합니다. 이 자습서에서는 모델 바인딩을 사용 하 여 데이터 컨트롤의 데이터를 사용 하 여 경로를 생성할 때 사용 되는 `RouteValueDictionary` 개체를 검색 합니다. `RouteValueDictionary` 개체에는 제품의 특정 범주에 속하는 제품 이름 목록이 포함 됩니다. 데이터 및 경로를 기반으로 하 여 각 제품에 대 한 링크가 생성 됩니다.

#### <a name="enable-routes-for-categories-and-products"></a>범주 및 제품에 대 한 경로 사용

다음으로 `ProductsByCategoryRoute`를 사용 하 여 각 제품 범주 링크에 포함할 올바른 경로를 결정 하도록 응용 프로그램을 업데이트 합니다. 또한 각 제품에 대 한 라우트된 링크를 포함 하도록 *ProductList* 페이지를 업데이트 합니다. 이 링크는 변경 전 상태로 표시 되지만 이제 링크에서 URL 라우팅을 사용 합니다.

1. **솔루션 탐색기**에서 site.master 페이지가 아직 열려 있지 않으면 엽니다 *.*
2. "`categoryList`" 이라는 **ListView** 컨트롤을 노란색으로 강조 표시 된 변경 내용으로 업데이트 하므로 태그는 다음과 같이 표시 됩니다.   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. **솔루션 탐색기**에서 *ProductList* 페이지를 엽니다.
4. 노란색으로 강조 표시 된 업데이트를 사용 하 여 *ProductList* 페이지의 `ItemTemplate` 요소를 업데이트 합니다. 그러면 태그가 다음과 같이 표시 됩니다.   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. *ProductList.aspx.cs* 의 코드를 열고 노란색으로 강조 표시 된 다음 네임 스페이스를 추가 합니다.  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. 코드 숨김으로 (*ProductList.aspx.cs*)의 `GetProducts` 메서드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a>제품 정보에 대 한 코드 추가

이제 경로 데이터를 사용 하도록 *제품 세부 정보 .aspx* 페이지에 대 한 코드를 업데이트 합니다 (*ProductDetails.aspx.cs*). 새 `GetProduct` 메서드는 사용자에 게 더 이상 라우팅되지 않은 이전 URL을 사용 하는 링크가 있는 경우에도 쿼리 문자열 값을 허용 합니다.

1. 코드 숨김으로 (*ProductDetails.aspx.cs*)의 `GetProduct` 메서드를 다음 코드로 바꿉니다.   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a>응용 프로그램 실행

이제 응용 프로그램을 실행 하 여 업데이트 된 경로를 확인할 수 있습니다.

1. **F5** 키를 눌러 정문 장난감 샘플 응용 프로그램을 실행 합니다.  
 브라우저가 열리고 *default.aspx 페이지가 표시 됩니다.*
2. 페이지 맨 위에 있는 **제품** 링크를 클릭 합니다.  
 모든 제품은 *ProductList* 페이지에 표시 됩니다. 브라우저에 대 한 다음 URL (포트 번호 사용)이 표시 됩니다.  
    `https://localhost:44300/ProductList`
3. 그런 다음 페이지 위쪽의 **자동차** 범주 링크를 클릭 합니다.  
 자동차가 *ProductList* 페이지에만 표시 됩니다. 브라우저에 대 한 다음 URL (포트 번호 사용)이 표시 됩니다.  
    `https://localhost:44300/Category/Cars`
4. 페이지에 나열 된 첫 번째 자동차의 이름을 포함 하는 링크를 클릭 하여 제품 세부 정보를 표시 합니다.  
 브라우저에 대 한 다음 URL (포트 번호 사용)이 표시 됩니다.  
    `https://localhost:44300/Product/Convertible%20Car`
5. 그런 다음 경로를 사용 하지 않는 다음 URL을 브라우저에 입력 합니다.  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 코드는 사용자에 게 책갈피가 있는 링크를 포함 하는 경우 쿼리 문자열을 포함 하는 URL을 계속 인식 합니다.

## <a name="summary"></a>요약

이 자습서에서는 범주 및 제품에 대 한 경로를 추가 했습니다. 모델 바인딩을 사용 하는 데이터 컨트롤과 경로를 통합 하는 방법을 알아보았습니다. 다음 자습서에서는 전역 오류 처리를 구현 합니다.

## <a name="additional-resources"></a>추가 리소스

[ASP.NET 친화적인 Url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[멤버 자격, OAuth 및 SQL Database를 사용 하 여 보안 ASP.NET Web Forms 앱을 배포 Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure-무료 평가판](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [이전](membership-and-administration.md)
> [다음](aspnet-error-handling.md)
