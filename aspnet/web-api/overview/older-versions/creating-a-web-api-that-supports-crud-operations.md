---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: ASP.NET Web API 1-ASP.NET 4.x에서 CRUD 작업을 사용 하도록 설정
author: MikeWasson
description: 자습서에서는 ASP.NET 4.x의 ASP.NET Web API을 사용 하 여 HTTP 서비스에서 CRUD 작업을 지 원하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448043"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a>ASP.NET Web API 1에서 CRUD 작업 사용

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> 이 자습서에서는 ASP.NET 4.x의 ASP.NET Web API을 사용 하 여 HTTP 서비스에서 CRUD 작업을 지 원하는 방법을 보여 줍니다.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Visual Studio 2012
> - Web API 1 (Web API 2 에서도 작동)

CRUD는 네 가지 기본 데이터베이스 작업 인 &quot;만들기, 읽기, 업데이트 및 삭제&quot;를 나타냅니다. 또한 대부분의 HTTP 서비스는 REST 또는 REST Api를 통해 CRUD 작업을 모델링 합니다.

이 자습서에서는 매우 간단한 웹 API를 빌드하여 제품 목록을 관리 합니다. 각 제품에는 이름, 가격 및 범주 (예: &quot;장난감&quot; 또는 &quot;하드웨어&quot;)와 제품 ID가 포함 됩니다.

Products API는 다음 메서드를 노출 합니다.

| 작업 | HTTP 메서드 | 상대 URI |
| --- | --- | --- |
| 모든 제품 목록 가져오기 | GET | /api/제품 |
| ID로 제품 가져오기 | GET | /api/products/*id* |
| 범주별로 제품 가져오기 | GET | /api/products? 범주 =*범주* |
| 새 제품 만들기 | POST | /api/제품 |
| 제품 업데이트 | PUT | /api/products/*id* |
| 제품 삭제 | Delete | /api/products/*id* |

일부 Uri에는 경로에 제품 ID가 포함 되어 있습니다. 예를 들어 ID가 28 인 제품을 가져오기 위해 클라이언트는 `http://hostname/api/products/28`에 대 한 GET 요청을 보냅니다.

### <a name="resources"></a>리소스

제품 API는 다음 두 리소스 유형에 대 한 Uri를 정의 합니다.

| 리소스 | URI |
| --- | --- |
| 모든 제품의 목록입니다. | /api/제품 |
| 개별 제품입니다. | /api/products/*id* |

### <a name="methods"></a>메서드

다음과 같이 네 가지 주요 HTTP 메서드 (GET, PUT, POST 및 DELETE)를 CRUD 작업에 매핑할 수 있습니다.

- GET은 지정 된 URI에서 리소스의 표현을 검색 합니다. GET은 서버에 부작용이 없어야 합니다.
- 지정 된 URI에 리소스를 추가 합니다. 서버에서 클라이언트가 새 Uri를 지정할 수 있도록 허용 하는 경우 PUT을 사용 하 여 지정 된 URI에 새 리소스를 만들 수도 있습니다. 이 자습서의 경우 API는 PUT을 통해 만들기를 지원 하지 않습니다.
- POST는 새 리소스를 만듭니다. 서버는 새 개체에 대 한 URI를 할당 하 고이 URI를 응답 메시지의 일부로 반환 합니다.
- DELETE 지정 된 URI에서 리소스를 삭제 합니다.

참고: PUT 메서드는 전체 제품 엔터티를 대체 합니다. 즉, 클라이언트는 업데이트 된 제품의 전체 표현을 전송 해야 합니다. 부분 업데이트를 지원 하려는 경우 패치 방법이 선호 됩니다. 이 자습서에서는 패치를 구현 하지 않습니다.

## <a name="create-a-new-web-api-project"></a>새 Web API 프로젝트 만들기

먼저 Visual Studio를 실행 하 고 **시작** 페이지에서 **새 프로젝트** 를 선택 합니다. 또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고  **C# 시각적** 노드를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. 프로젝트 템플릿 목록에서 **ASP.NET MVC 4 웹 응용 프로그램**을 선택 합니다. 프로젝트 이름을 &quot;제품 저장소로&quot; 하 고 **확인**을 클릭 합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

**New ASP.NET MVC 4 프로젝트** 대화 상자에서 **Web API** 를 선택 하 고 **확인**을 클릭 합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a>모델 추가

*모델*은 애플리케이션에서 데이터를 나타내는 개체입니다. ASP.NET Web API에서는 강력한 형식의 CLR 개체를 모델로 사용할 수 있으며, 자동으로 클라이언트에 대해 XML 또는 JSON으로 serialize 됩니다.

제품 저장소 API의 경우 데이터는 제품으로 구성 되므로 `Product`이라는 새 클래스를 만듭니다.

솔루션 탐색기가 표시되지 않는 경우 **보기** 메뉴를 클릭하고 **솔루션 탐색기**를 선택합니다. 솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 **추가**를 선택한 다음 **클래스**를 선택 합니다. 클래스 이름을 Product&quot;&quot;합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

`Product` 클래스에 다음 속성을 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a>리포지토리 추가

제품 컬렉션을 저장 해야 합니다. 서비스 구현에서 컬렉션을 분리 하는 것이 좋습니다. 이렇게 하면 서비스 클래스를 다시 작성 하지 않고도 백업 저장소를 변경할 수 있습니다. 이러한 종류의 디자인을 *리포지토리* 패턴 이라고 합니다. 먼저 리포지토리의 제네릭 인터페이스를 정의 합니다.

솔루션 탐색기에서 **모델** 폴더를 마우스 오른쪽 단추로 클릭 합니다. **추가**를 선택한 다음 **새 항목**을 선택 합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고 노드 C# 를 확장 합니다. 에서 C# **코드**를 선택 합니다. 코드 템플릿 목록에서 **인터페이스**를 선택 합니다. 인터페이스 이름을 IProductRepository&quot;로 &quot;합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

다음 구현을 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

이제 &quot;ProductRepository 라는 모델 폴더에 다른 클래스를 추가 합니다.&quot;이 클래스는 `IProductRepository` 인터페이스를 구현 합니다. 다음 구현을 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

리포지토리는 로컬 메모리에 목록을 유지 합니다. 이는 자습서에서 양호 하지만 실제 응용 프로그램에서는 데이터를 외부에 저장 하거나 클라우드 저장소에 저장 합니다. 리포지토리 패턴을 사용 하면 나중에 구현을 더 쉽게 변경할 수 있습니다.

## <a name="adding-a-web-api-controller"></a>Web API 컨트롤러 추가

ASP.NET MVC를 사용 하 여 작업 한 경우 이미 컨트롤러에 대해 잘 알고 있는 것입니다. ASP.NET Web API에서 *컨트롤러* 는 클라이언트의 HTTP 요청을 처리 하는 클래스입니다. 새 프로젝트 마법사는 프로젝트를 만들 때 두 개의 컨트롤러를 만들었습니다. 이를 확인 하려면 솔루션 탐색기의 컨트롤러 폴더를 확장 합니다.

- HomeController는 기존의 ASP.NET MVC 컨트롤러입니다. 이는 사이트에 대 한 HTML 페이지의 서비스를 담당 하며 웹 API와 직접 관련 되지 않습니다.
- Valuecontroller는 예제 WebAPI controller입니다.

솔루션 탐색기에서 파일을 마우스 오른쪽 단추로 클릭 하 고 삭제를 선택 하 여 다음으로 이동 하 여 Valuecontroller를 삭제 **합니다.** 이제 다음과 같이 새 컨트롤러를 추가 합니다.

**솔루션 탐색기**에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭합니다. **추가**를 선택한 후 **컨트롤러**를 선택합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

**컨트롤러 추가** 마법사에서 컨트롤러 이름을 ProductsController&quot;로 &quot;합니다. **템플릿** 드롭다운 목록에서 **빈 API 컨트롤러**를 선택 합니다. 그런 다음, **추가**를 클릭합니다.

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> 컨트롤러를 컨트롤러 라는 폴더에 배치할 필요는 없습니다. 폴더 이름은 중요 하지 않습니다. 단순히 소스 파일을 구성 하는 편리한 방법입니다.

**컨트롤러 추가** 마법사가 Controllers 폴더에 ProductsController.cs 라는 파일을 만듭니다. 이 파일이 열려 있지 않으면 파일을 두 번 클릭하여 엽니다. 다음 **using** 문을 추가합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

**IProductRepository** 인스턴스를 보유 하는 필드를 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> 컨트롤러를 `IProductRepository`의 특정 구현에 연결 하기 때문에 컨트롤러에서 `new ProductRepository()`를 호출 하는 것은 최적의 디자인이 아닙니다. 더 나은 접근 방법은 [웹 API 종속성 확인자 사용](../advanced/dependency-injection.md)을 참조 하세요.

## <a name="getting-a-resource"></a>리소스 가져오기

제품 저장소 API는 여러 &quot;&quot; 작업을 HTTP GET 메서드로 표시 합니다. 각 작업은 `ProductsController` 클래스의 메서드에 해당 합니다.

| 작업 | HTTP 메서드 | 상대 URI |
| --- | --- | --- |
| 모든 제품 목록 가져오기 | GET | /api/제품 |
| ID로 제품 가져오기 | GET | /api/products/*id* |
| 범주별로 제품 가져오기 | GET | /api/products? 범주 =*범주* |

모든 제품 목록을 가져오려면 `ProductsController` 클래스에 다음 메서드를 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

메서드 이름은 GET&quot;&quot;으로 시작 되므로 규칙에 따라 GET 요청에 매핑됩니다. 또한 메서드에는 매개 변수가 없기 때문에 경로에 *&quot;id&quot;* 세그먼트가 포함 되지 않은 URI에 매핑됩니다.

ID로 제품을 가져오려면 `ProductsController` 클래스에 다음 메서드를 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

또한이 메서드 이름은 &quot;Get&quot;로 시작 하지만 메서드에 *id*라는 매개 변수가 있습니다. 이 매개 변수는 URI 경로의 &quot;id&quot; 세그먼트로 매핑됩니다. ASP.NET Web API 프레임 워크는 매개 변수에 대해 ID를 올바른 데이터 형식 (**int**)으로 자동 변환 합니다.

GetProduct 메서드는 *id* 가 유효 하지 않은 경우 **HttpResponseException** 형식의 예외를 throw 합니다. 이 예외는 프레임 워크에서 404 (찾을 수 없음) 오류로 변환 됩니다.

마지막으로, 범주를 기준으로 제품을 찾는 메서드를 추가 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

요청 URI에 쿼리 문자열이 있는 경우 Web API는 컨트롤러 메서드의 매개 변수와 쿼리 매개 변수를 일치 시 키 려 고 합니다. 따라서 "api/products? category =*category*" 형식의 URI가이 메서드에 매핑됩니다.

## <a name="creating-a-resource"></a>리소스 만들기

다음으로 `ProductsController` 클래스에 메서드를 추가 하 여 새 제품을 만듭니다. 다음은 메서드를 간단 하 게 구현한 것입니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

이 메서드에 대 한 두 가지 사항을 확인 합니다.

- 메서드 이름은 &quot;&quot;으로 시작 합니다. 새 제품을 만들기 위해 클라이언트는 HTTP POST 요청을 보냅니다.
- 메서드는 Product 형식의 매개 변수를 사용 합니다. Web API에서 복합 형식이 포함 된 매개 변수는 요청 본문에서 deserialize 됩니다. 따라서 클라이언트는 product 개체의 serialize 된 표현을 XML 또는 JSON 형식으로 보낼 것으로 간주 합니다.

이 구현은 작동 하지만 완전히 완전 하지는 않습니다. 이상적으로 HTTP 응답에는 다음과 같은 내용이 포함 됩니다.

- **응답 코드:** 기본적으로 Web API 프레임 워크는 응답 상태 코드를 200 (OK)로 설정 합니다. 하지만 HTTP/1.1 프로토콜에 따라 POST 요청으로 인해 리소스가 생성 될 때 서버는 상태 201 (만듦)로 회신 해야 합니다.
- **위치:** 서버는 리소스를 만들 때 응답의 Location 헤더에 새 리소스의 URI를 포함 해야 합니다.

ASP.NET Web API를 사용 하면 HTTP 응답 메시지를 쉽게 조작할 수 있습니다. 다음은 향상 된 구현입니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

이제 메서드 반환 형식은 **HttpResponseMessage**입니다. 제품 대신 **HttpResponseMessage** 를 반환 하 여 상태 코드 및 위치 헤더를 포함 하는 HTTP 응답 메시지의 세부 정보를 제어할 수 있습니다.

**CreateResponse** 메서드는 **HttpResponseMessage** 를 만들고 Product 개체의 serialize 된 표현을 응답 메시지의 본문에 자동으로 씁니다.

> [!NOTE]
> 이 예에서는 `Product`의 유효성을 검사 하지 않습니다. 모델 유효성 검사에 대 한 자세한 내용은 [ASP.NET Web API의 모델 유효성 검사](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)를 참조 하세요.

## <a name="updating-a-resource"></a>리소스 업데이트

PUT을 사용 하 여 제품을 업데이트 하는 것은 간단 합니다.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

메서드 이름은 &quot;Put ...&quot;로 시작 하므로 Web API는이를 일치 시켜 요청을 배치 합니다. 메서드는 제품 ID와 업데이트 된 제품의 두 매개 변수를 사용 합니다. *Id* 매개 변수는 URI 경로에서 가져오고 *product* 매개 변수는 요청 본문에서 deserialize 됩니다. 기본적으로 ASP.NET Web API 프레임 워크는 요청 본문의 경로 및 복합 형식에서 단순 매개 변수 형식을 사용 합니다.

## <a name="deleting-a-resource"></a>리소스 삭제

리소스를 삭제 하려면 "Delete ..."를 정의 합니다. 방법이.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

삭제 요청이 성공 하면 상태를 설명 하는 엔터티 본문과 함께 상태 200 (OK)을 반환할 수 있습니다. 삭제가 아직 보류 중인 경우 상태 202 (수락 됨) 또는 상태 204 (콘텐츠 없음) (엔터티 본문이 없음)입니다. 이 경우 `DeleteProduct` 메서드에 `void` 반환 형식이 있으므로 ASP.NET Web API에서 자동으로이를 상태 코드 204 (내용 없음)로 변환 합니다.
