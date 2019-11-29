---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: '3 부: 관리 컨트롤러 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600037"
---
# <a name="part-3-creating-an-admin-controller"></a>3 부: 관리 컨트롤러 만들기

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a>관리 컨트롤러 추가

이 섹션에서는 제품에 대 한 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업을 지 원하는 Web API 컨트롤러를 추가 합니다. 컨트롤러는 Entity Framework을 사용 하 여 데이터베이스 계층과 통신 합니다. 관리자만이 컨트롤러를 사용할 수 있습니다. 고객은 다른 컨트롤러를 통해 제품에 액세스 합니다.

솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. **추가** 를 선택 하 고 **컨트롤러**를 선택 합니다.

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

**컨트롤러 추가** 대화 상자에서 컨트롤러 이름을 `AdminController`로 합니다. **템플릿**에서 Entity Framework&quot;를 사용 하 여 읽기/쓰기 동작이 포함 된 &quot;API 컨트롤러를 선택 합니다. **모델 클래스**에서 "Product (제품명)"를 선택 합니다. **데이터 컨텍스트**아래에서 "&lt;새 데이터 컨텍스트&gt;"를 선택 합니다.

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> **모델 클래스** 드롭다운이 모델 클래스를 표시 하지 않는 경우 프로젝트를 컴파일 했는지 확인 합니다. Entity Framework는 리플렉션을 사용 하므로 컴파일된 어셈블리가 필요 합니다.

"&lt;새 데이터 컨텍스트&gt;"를 선택 하면 **새 데이터 컨텍스트** 대화 상자가 열립니다. 데이터 컨텍스트 이름을 `ProductStore.Models.OrdersContext`로 합니다.

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

**확인** 을 클릭 하 여 **새 데이터 컨텍스트** 대화 상자를 닫습니다. **컨트롤러 추가** 대화 상자에서 **추가**를 클릭 합니다.

프로젝트에 추가 된 기능은 다음과 같습니다.

- **DbContext**에서 파생 되는 `OrdersContext` 라는 클래스입니다. 이 클래스는 POCO 모델과 데이터베이스 간의 붙이기를 제공 합니다.
- `AdminController`이라는 웹 API 컨트롤러 이 컨트롤러는 `Product` 인스턴스에 대 한 CRUD 작업을 지원 합니다. `OrdersContext` 클래스를 사용 하 여 Entity Framework와 통신 합니다.
- Web.config 파일의 새 데이터베이스 연결 문자열입니다.

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

OrdersContext.cs 파일을 엽니다. 생성자는 데이터베이스 연결 문자열의 이름을 지정 합니다. 이 이름은 Web.config에 추가 된 연결 문자열을 참조 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

`OrdersContext` 클래스에 다음 속성을 추가합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

**Dbset** 은 쿼리할 수 있는 엔터티 집합을 나타냅니다. 다음은 `OrdersContext` 클래스에 대 한 전체 목록입니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

`AdminController` 클래스는 기본 CRUD 기능을 구현 하는 5 개의 메서드를 정의 합니다. 각 메서드는 클라이언트에서 호출할 수 있는 URI에 해당 합니다.

| Controller 메서드 | 설명 | URI | HTTP 메서드 |
| --- | --- | --- | --- |
| GetProducts | 모든 제품을 가져옵니다. | a p i/제품 | 가져오기 |
| GetProduct | ID로 제품을 찾습니다. | a p i/제품/*i d* | 가져오기 |
| PutProduct | 제품을 업데이트 합니다. | a p i/제품/*i d* | PUT |
| PostProduct | 새 제품을 만듭니다. | a p i/제품 | 올리기 |
| DeleteProduct | 제품을 삭제 합니다. | a p i/제품/*i d* | Delete |

각 메서드는 `OrdersContext`를 호출 하 여 데이터베이스를 쿼리 합니다. 컬렉션 (PUT, POST 및 DELETE) 호출을 수정 하는 메서드는 데이터베이스에 대 한 변경 내용을 유지 하는 `db.SaveChanges` 합니다. 컨트롤러는 HTTP 요청당 생성 된 다음 삭제 되므로 메서드가 반환 되기 전에 변경 내용을 유지 해야 합니다.

## <a name="add-a-database-initializer"></a>데이터베이스 이니셜라이저 추가

Entity Framework에는 시작 시 데이터베이스를 채우고 모델이 변경 될 때마다 자동으로 데이터베이스를 다시 만들 수 있는 유용한 기능이 있습니다. 이 기능은 모델을 변경 하는 경우에도 항상 일부 테스트 데이터가 있으므로 개발 하는 동안 유용 합니다.

솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 `OrdersContextInitializer`라는 새 클래스를 만듭니다. 다음 구현에 붙여넣습니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

**Dropcreatedatabaseifmodelchanges** 클래스에서 상속 하 여 모델 클래스를 수정할 때마다 데이터베이스를 삭제 Entity Framework 합니다. Entity Framework 데이터베이스를 만들거나 다시 만들 때 **시드** 메서드를 호출 하 여 테이블을 채웁니다. **Seed** 메서드를 사용 하 여 몇 가지 예제 제품과 예제 순서를 추가 합니다.

이 기능은 테스트에 유용 하지만, 누군가가 모델 클래스를 변경 하는 경우 데이터가 손실 될 수 있으므로 프로덕션 환경에서는 **Dropcreatedatabaseifmodelchanges** 클래스를 사용 하지 마세요.

그런 다음 Global.asax를 열고 **응용 프로그램\_Start** 메서드에 다음 코드를 추가 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a>컨트롤러에 요청 보내기

이 시점에서 클라이언트 코드를 작성 하지 않았지만 웹 브라우저나 [Fiddler](http://www.fiddler2.com/fiddler2/)와 같은 HTTP 디버깅 도구를 사용 하 여 웹 API를 호출할 수 있습니다. Visual Studio에서 F5 키를 눌러 디버깅을 시작 합니다. 웹 브라우저가 `http://localhost:*portnum*/`으로 열립니다. 여기서 *portnum* 은 일부 포트 번호입니다.

"`http://localhost:*portnum*/api/admin`에 HTTP 요청을 보냅니다. Entity Framework는 데이터베이스를 만들고 초기값을 설정할 수 있기 때문에 첫 번째 요청은 완료 하는 데 속도가 느릴 수 있습니다. 응답은 다음과 유사 합니다.

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-2.md)
> [다음](using-web-api-with-entity-framework-part-4.md)
