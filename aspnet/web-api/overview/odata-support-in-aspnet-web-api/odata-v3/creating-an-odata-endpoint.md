---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Web API 2를 사용 하 여 OData v3 끝점 만들기 | Microsoft Docs
author: MikeWasson
description: OData (Open Data Protocol)는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 데이터를 구조화 하 고, 데이터를 쿼리하고, 데이터를 조작 하는 일관 된 방법을 제공 합니다.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600426"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>Web API 2를 사용 하 여 OData v3 끝점 만들기

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> OData ( [Open Data Protocol](http://www.odata.org/) )는 웹에 대 한 데이터 액세스 프로토콜입니다. OData는 데이터를 구조화 하 고, 데이터를 쿼리하고, CRUD 작업 (만들기, 읽기, 업데이트 및 삭제)을 통해 데이터 집합을 조작 하는 일관 된 방법을 제공 합니다. OData는 AtomPub (XML) 및 JSON 형식을 모두 지원 합니다. 또한 OData는 데이터에 대 한 메타 데이터를 노출 하는 방법을 정의 합니다. 클라이언트는 메타 데이터를 사용 하 여 데이터 집합에 대 한 형식 정보 및 관계를 검색할 수 있습니다.
>
> ASP.NET Web API를 사용 하면 데이터 집합에 대 한 OData 끝점을 쉽게 만들 수 있습니다. 끝점이 지 원하는 OData 작업을 정확 하 게 제어할 수 있습니다. 비 OData 끝점과 함께 여러 OData 끝점을 호스트할 수 있습니다. 데이터 모델, 백 엔드 비즈니스 논리 및 데이터 계층에 대 한 모든 권한을 가집니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - OData 버전 3
> - Entity Framework 6
> - [Fiddler 웹 디버깅 프록시 (선택 사항)](http://www.fiddler2.com)
>
> 웹 API OData 지원은 [ASP.NET 및 Web Tools 2012.2 업데이트](https://go.microsoft.com/fwlink/?LinkId=282650)에 추가 되었습니다. 그러나이 자습서에서는 Visual Studio 2013에 추가 된 스 캐 폴딩을 사용 합니다.

이 자습서에서는 클라이언트가 쿼리할 수 있는 간단한 OData 끝점을 만듭니다. 끝점에 대 한 C# 클라이언트도 만듭니다. 이 자습서를 완료 한 후에는 엔터티 관계, 동작 및 $expand/$select를 포함 하 여 더 많은 기능을 추가 하는 방법을 보여 주는 다음 자습서 집합이 있습니다.

- [Visual Studio 프로젝트 만들기](#create-project)
- [엔터티 모델 추가](#add-model)
- [OData 컨트롤러 추가](#add-controller)
- [EDM 및 경로 추가](#edm)
- [데이터베이스 초기값 지정 (선택 사항)](#seed-db)
- [OData 끝점 탐색](#explore)
- [OData 직렬화 형식](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>Visual Studio 프로젝트 만들기

이 자습서에서는 기본 CRUD 작업을 지 원하는 OData 끝점을 만듭니다. 이 끝점은 단일 리소스 (제품 목록)를 노출 합니다. 이후 자습서에서는 더 많은 기능을 추가 합니다.

Visual Studio를 시작 하 고 시작 페이지에서 **새 프로젝트** 를 선택 합니다. 또는 **파일** 메뉴에서 **새로 만들기** , **프로젝트**를 차례로 선택 합니다.

**템플릿** 창에서 **설치 된 템플릿** 을 선택 하 고 시각적 C# 노드를 확장 합니다. **시각적 개체 C#** 에서 **웹**을 선택 합니다. **ASP.NET 웹 응용 프로그램** 템플릿을 선택 합니다.

![](creating-an-odata-endpoint/_static/image1.png)

**새 ASP.NET 프로젝트** 대화 상자에서 **빈** 템플릿을 선택 합니다. &quot;에 대 한 폴더 및 핵심 참조 추가 &quot;에서 **WEB API**를 선택 합니다. **확인**을 클릭합니다.

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>엔터티 모델 추가

*모델*은 애플리케이션에서 데이터를 나타내는 개체입니다. 이 자습서에서는 제품을 나타내는 모델이 필요 합니다. 모델은 OData 엔터티 형식에 해당 합니다.

솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다. 상황에 맞는 메뉴에서 **추가** 를 선택한 다음 **클래스**를 선택 합니다.

![](creating-an-odata-endpoint/_static/image3.png)

새 항목 **추가** 대화 상자에서 클래스 이름을 Product&quot;로 &quot;합니다.

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> 규칙에 따라 모델 클래스는 모델 폴더에 배치 됩니다. 사용자 고유의 프로젝트에서이 규칙을 따를 필요는 없지만이 자습서에 사용 합니다.

Product.cs 파일에서 다음 클래스 정의를 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

ID 속성은 엔터티 키가 됩니다. 클라이언트는 ID로 제품을 쿼리할 수 있습니다. 이 필드는 백 엔드 데이터베이스의 기본 키 이기도 합니다.

이제 프로젝트를 빌드합니다. 다음 단계에서는 리플렉션을 사용 하 여 제품 유형을 찾는 몇 가지 Visual Studio 스 캐 폴딩을 사용 합니다.

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>OData 컨트롤러 추가

*컨트롤러* 는 HTTP 요청을 처리 하는 클래스입니다. OData 서비스에서 각 엔터티 집합에 대해 별도의 컨트롤러를 정의 합니다. 이 자습서에서는 단일 컨트롤러를 만듭니다.

솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. **추가** 를 선택한 다음 **컨트롤러**를 선택 합니다.

![](creating-an-odata-endpoint/_static/image5.png)

**스 캐 폴드 추가** 대화 상자에서 Entity Framework&quot;를 사용 하 여 작업을 포함 하는 Web API 2 OData 컨트롤러 &quot;를 선택 합니다.

![](creating-an-odata-endpoint/_static/image6.png)

**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을 "ProductsController"로 합니다. 비동기 컨트롤러 작업 사용 &quot;&quot; 확인란을 선택 합니다. **모델** 드롭다운 목록에서 Product 클래스를 선택 합니다.

![](creating-an-odata-endpoint/_static/image7.png)

**새 데이터 컨텍스트 ...** 단추를 클릭 합니다. 데이터 컨텍스트 형식에 대 한 기본 이름을 그대로 두고 **추가**를 클릭 합니다.

![](creating-an-odata-endpoint/_static/image8.png)

컨트롤러 추가 대화 상자에서 추가를 클릭 하 여 컨트롤러를 추가 합니다.

![](creating-an-odata-endpoint/_static/image9.png)

참고:&quot;유형을 가져오는 중 오류가 발생 했습니다 &quot;오류 메시지가 표시 되는 경우 Product 클래스를 추가한 후 Visual Studio 프로젝트를 빌드 했는지 확인 합니다. 스 캐 폴딩은 리플렉션을 사용 하 여 클래스를 찾습니다.

![](creating-an-odata-endpoint/_static/image10.png)

스 캐 폴딩은 두 코드 파일을 프로젝트에 추가 합니다.

- Products.cs는 OData 끝점을 구현 하는 Web API 컨트롤러를 정의 합니다.
- ProductServiceContext.cs는 Entity Framework 사용 하 여 기본 데이터베이스를 쿼리 하는 메서드를 제공 합니다.

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>EDM 및 경로 추가

솔루션 탐색기에서 앱\_시작 폴더를 확장 하 고 이름이 WebApiConfig.cs 인 파일을 엽니다. 이 클래스는 Web API에 대 한 구성 코드를 포함 합니다. 이 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

이 코드는 다음 두 가지 작업을 수행 합니다.

- OData 끝점에 대 한 EDM (엔터티 데이터 모델)을 만듭니다.
- 끝점에 대 한 경로를 추가 합니다.

EDM은 데이터의 추상 모델입니다. EDM은 메타 데이터 문서를 만들고 서비스에 대 한 Uri를 정의 하는 데 사용 됩니다. **ODataConventionModelBuilder** 는 기본 명명 규칙 edm 집합을 사용 하 여 edm을 만듭니다. 이 방법에는 최소한의 코드가 필요 합니다. EDM을 보다 세부적으로 제어 하려는 경우 **만드는** 클래스를 사용 하 여 속성, 키 및 탐색 속성을 명시적으로 추가 하 여 edm을 만들 수 있습니다.

**EntitySet** 메서드는 EDM에 엔터티 집합을 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

"Products" 문자열은 엔터티 집합의 이름을 정의 합니다. 컨트롤러의 이름은 엔터티 집합의 이름과 일치 해야 합니다. 이 자습서에서 엔터티 집합의 이름은 "Products"이 고 컨트롤러의 이름은 `ProductsController`입니다. "제품 집합" 엔터티 집합의 이름을 지정 하는 경우 컨트롤러의 이름을 `ProductSetController`합니다. 끝점에는 여러 엔터티 집합이 있을 수 있습니다. 각 엔터티 집합에 대해 **EntitySet&lt;t&gt;** 를 호출한 다음 해당 하는 컨트롤러를 정의 합니다.

**MapODataRoute** 메서드는 OData 끝점에 대 한 경로를 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

첫 번째 매개 변수는 경로에 대 한 친숙 한 이름입니다. 서비스의 클라이언트에는이 이름이 표시 되지 않습니다. 두 번째 매개 변수는 끝점의 URI 접두사입니다. 이 코드를 지정 하면 Products 엔터티 집합에 대 한 URI는 http://<em>hostname</em>/Odata/products로 설정 됩니다. 응용 프로그램에는 둘 이상의 OData 끝점이 있을 수 있습니다. 각 끝점에 대해 <strong>MapODataRoute</strong> 를 호출 하 고 고유한 경로 이름 및 고유한 URI 접두사를 제공 합니다.

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>데이터베이스 초기값 지정 (선택 사항)

이 단계에서는 Entity Framework를 사용 하 여 일부 테스트 데이터로 데이터베이스를 초기값으로 사용 합니다. 이 단계는 선택 사항 이지만 OData 끝점을 즉시 테스트할 수 있습니다.

**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

그러면 migration 이라는 폴더와 이름이 Configuration.cs 인 코드 파일이 추가 됩니다.

![](creating-an-odata-endpoint/_static/image12.png)

이 파일을 열고 다음 코드를 `Configuration.Seed` 메서드에 추가 합니다.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

이러한 명령은 데이터베이스를 만든 다음 해당 코드를 실행 하는 코드를 생성 합니다.

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>OData 끝점 탐색

이 섹션에서는 [Fiddler 웹 디버깅 프록시](http://www.fiddler2.com) 를 사용 하 여 끝점에 요청을 보내고 응답 메시지를 검사 합니다. 그러면 OData 끝점의 기능을 이해 하는 데 도움이 됩니다.

Visual Studio에서 F5 키를 눌러 디버깅을 시작 합니다. 기본적으로 Visual Studio는 `http://localhost:*port*`하기 위해 브라우저를 엽니다. 여기서 *port* 는 프로젝트 설정에 구성 된 포트 번호입니다.

프로젝트 설정에서 포트 번호를 변경할 수 있습니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. 속성 창에서 **웹**을 선택 합니다. **프로젝트 Url**아래에 포트 번호를 입력 합니다.

### <a name="service-document"></a>서비스 문서

*서비스 문서* 에는 OData 끝점에 대 한 엔터티 집합 목록이 포함 되어 있습니다. 서비스 문서를 가져오려면 서비스의 루트 URI에 GET 요청을 보냅니다.

Fiddler를 사용 하 여 **작성기** 탭에 다음 URI를 입력 합니다 `http://localhost:port/odata/`. 여기서 *port* 는 포트 번호입니다.

![](creating-an-odata-endpoint/_static/image13.png)

**실행** 단추를 클릭 합니다. Fiddler는 응용 프로그램에 HTTP GET 요청을 보냅니다. 웹 세션 목록에 응답이 표시 되어야 합니다. 모든 것이 작동 하는 경우 상태 코드는 200가 됩니다.

![](creating-an-odata-endpoint/_static/image14.png)

웹 세션 목록에서 응답을 두 번 클릭 하면 검사기 탭에서 응답 메시지의 세부 정보를 볼 수 있습니다.

![](creating-an-odata-endpoint/_static/image15.png)

원시 HTTP 응답 메시지는 다음과 같이 표시 됩니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

기본적으로 Web API는 AtomPub 형식으로 서비스 문서를 반환 합니다. JSON을 요청 하려면 HTTP 요청에 다음 헤더를 추가 합니다.

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

이제 HTTP 응답은 JSON 페이로드를 포함 합니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>서비스 메타 데이터 문서

*서비스 메타 데이터 문서* 에서는 CSDL (개념 스키마 정의 언어) 이라는 XML 언어를 사용 하 여 서비스의 데이터 모델에 대해 설명 합니다. 메타 데이터 문서는 서비스의 데이터 구조를 보여 주며 클라이언트 코드를 생성 하는 데 사용할 수 있습니다.

메타 데이터 문서를 가져오려면 GET 요청을 `http://localhost:port/odata/$metadata`으로 보냅니다. 이 자습서에 표시 된 끝점에 대 한 메타 데이터는 다음과 같습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>엔터티 집합

Products 엔터티 집합을 가져오려면 `http://localhost:port/odata/Products`에 GET 요청을 보냅니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>엔터티

개별 제품을 가져오려면 GET 요청을 `http://localhost:port/odata/Products(1)`으로 보냅니다. 여기서 "1"은 제품 ID입니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>OData 직렬화 형식

OData는 다음과 같은 여러 serialization 형식을 지원 합니다.

- Atom Pub (XML)
- JSON "light" (OData v3에 도입 됨)
- JSON "verbose" (OData v2)

기본적으로 Web API는 AtomPubJSON "light" 형식을 사용 합니다.

AtomPub 형식을 가져오려면 Accept 헤더를 "application/atom + xml"로 설정 합니다. 예제 응답 본문은 다음과 같습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

Atom 형식의 뚜렷한 단점 중 하나를 확인할 수 있습니다. JSON 밝은 것 보다 훨씬 더 자세한 정보를 표시 합니다. 그러나 클라이언트가 AtomPub를 이해 하는 경우 클라이언트는 JSON을 통해 해당 형식을 사용 하는 것이 좋습니다.

동일한 엔터티의 JSON light 버전은 다음과 같습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

JSON 광원 형식은 OData 프로토콜의 버전 3에서 도입 되었습니다. 이전 버전과의 호환성을 위해 클라이언트는 이전의 "verbose" JSON 형식을 요청할 수 있습니다. 자세한 JSON을 요청 하려면 Accept 헤더를 `application/json;odata=verbose`설정 합니다. 자세한 버전은 다음과 같습니다.

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

이 형식은 응답 본문에서 더 많은 메타 데이터를 전달 하므로 전체 세션에 상당한 오버 헤드를 추가할 수 있습니다. 또한 "d" 라는 속성에 개체를 래핑하여 간접 참조 수준을 추가 합니다.

## <a name="next-steps"></a>다음 단계

- [엔터티 관계 추가](working-with-entity-relations.md)
- [OData 작업 추가](odata-actions.md)
- [.NET 클라이언트에서 OData 서비스 호출](calling-an-odata-service-from-a-net-client.md)
