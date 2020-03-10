---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
title: .NET 클라이언트에서 OData 서비스 호출 (C#) | Microsoft Docs
author: MikeWasson
description: 이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다. 자습서 Visual Studio 2013에서 사용 되는 소프트웨어 버전 (Visual S와 함께 작동 ...
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 6f448917-ad23-4dcc-9789-897fad74051b
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/calling-an-odata-service-from-a-net-client
msc.type: authoredcontent
ms.openlocfilehash: 6a289fcb843634eeeefef1e0767e04e0be8b6973
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78498167"
---
# <a name="calling-an-odata-service-from-a-net-client-c"></a>.NET 클라이언트에서 OData 서비스 호출(C#)

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> 이 자습서에서는 C# 클라이언트 응용 프로그램에서 OData 서비스를 호출 하는 방법을 보여 줍니다.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) (Visual Studio 2012에서 작동)
> - [WCF Data Services 클라이언트 라이브러리](https://msdn.microsoft.com/library/cc668772.aspx)
> - Web API 2. 예제 OData 서비스는 Web API 2를 사용 하 여 작성 되지만 클라이언트 응용 프로그램은 Web API에 의존 하지 않습니다.

이 자습서에서는 OData 서비스를 호출 하는 클라이언트 응용 프로그램을 만드는 과정을 안내 합니다. OData 서비스는 다음 엔터티를 노출 합니다.

- `Product`
- `Supplier`
- `ProductRating`

![](calling-an-odata-service-from-a-net-client/_static/image1.png)

다음 문서에서는 Web API에서 OData 서비스를 구현 하는 방법을 설명 합니다. 그러나이 자습서를 이해 하기 위해 읽을 필요는 없습니다.

- [Web API 2에서 OData 엔드포인트 만들기](creating-an-odata-endpoint.md)
- [Web API 2의 OData 엔터티 관계](working-with-entity-relations.md)
- [Web API 2의 OData 작업](odata-actions.md)

## <a name="generate-the-service-proxy"></a>서비스 프록시를 생성 합니다.

첫 번째 단계는 서비스 프록시를 생성 하는 것입니다. 서비스 프록시는 OData 서비스에 액세스 하기 위한 메서드를 정의 하는 .NET 클래스입니다. 프록시는 메서드 호출을 HTTP 요청으로 변환 합니다.

![](calling-an-odata-service-from-a-net-client/_static/image2.png)

Visual Studio에서 OData 서비스 프로젝트를 열어 시작 합니다. IIS Express에서 로컬로 서비스를 실행 하려면 CTRL + F5 키를 누릅니다. Visual Studio에서 할당 하는 포트 번호를 포함 하 여 로컬 주소를 확인 합니다. 프록시를 만들 때이 주소가 필요 합니다.

그런 다음 Visual Studio의 다른 인스턴스를 열고 콘솔 응용 프로그램 프로젝트를 만듭니다. 콘솔 응용 프로그램은 OData 클라이언트 응용 프로그램이 됩니다. (서비스와 동일한 솔루션에 프로젝트를 추가할 수도 있습니다.)

> [!NOTE]
> 나머지 단계는 콘솔 프로젝트를 참조 합니다.

솔루션 탐색기에서 **참조** 를 마우스 오른쪽 단추로 클릭 하 고 **서비스 참조 추가**을 선택 합니다.

![](calling-an-odata-service-from-a-net-client/_static/image3.png)

**서비스 참조 추가** 대화 상자에서 OData 서비스의 주소를 입력 합니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample1.cmd)]

여기서 *port* 는 포트 번호입니다.

[![](calling-an-odata-service-from-a-net-client/_static/image5.png)](calling-an-odata-service-from-a-net-client/_static/image4.png)

**네임 스페이스**에 "제품 서비스"를 입력 합니다. 이 옵션은 프록시 클래스의 네임 스페이스를 정의 합니다.

**이동**을 클릭합니다. Visual Studio는 OData 메타 데이터 문서를 읽어 서비스의 엔터티를 검색 합니다.

[![](calling-an-odata-service-from-a-net-client/_static/image7.png)](calling-an-odata-service-from-a-net-client/_static/image6.png)

**확인** 을 클릭 하 여 프록시 클래스를 프로젝트에 추가 합니다.

![](calling-an-odata-service-from-a-net-client/_static/image8.png)

## <a name="create-an-instance-of-the-service-proxy-class"></a>서비스 프록시 클래스의 인스턴스를 만듭니다.

`Main` 메서드 내에서 다음과 같이 프록시 클래스의 새 인스턴스를 만듭니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample2.cs)]

서비스를 실행 하는 실제 포트 번호를 다시 사용 합니다. 서비스를 배포 하는 경우 라이브 서비스의 URI를 사용 합니다. 프록시를 업데이트할 필요가 없습니다.

다음 코드에서는 요청 Uri를 콘솔 창에 출력 하는 이벤트 처리기를 추가 합니다. 이 단계는 필요 하지 않지만 각 쿼리에 대 한 Uri를 확인 하는 것이 흥미롭습니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample3.cs)]

## <a name="query-the-service"></a>서비스 쿼리

다음 코드는 OData 서비스에서 제품 목록을 가져옵니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample4.cs)]

HTTP 요청을 보내거나 응답을 구문 분석 하는 코드를 작성할 필요가 없습니다. 프록시 클래스는 **foreach** 루프에서 `Container.Products` 컬렉션을 열거할 때이를 자동으로 수행 합니다.

응용 프로그램을 실행 하는 경우 출력은 다음과 같습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample5.cmd)]

ID로 엔터티를 가져오려면 `where` 절을 사용 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample6.cs)]

이 항목의 나머지 부분에서는 서비스를 호출 하는 데 필요한 코드를 비롯 하 여 전체 `Main` 함수를 표시 하지 않습니다.

## <a name="apply-query-options"></a>쿼리 옵션 적용

OData는 필터링, 정렬, 페이지 데이터 등에 사용할 수 있는 [쿼리 옵션](../supporting-odata-query-options.md) 을 정의 합니다. 서비스 프록시에서 다양 한 LINQ 식을 사용 하 여 이러한 옵션을 적용할 수 있습니다.

이 섹션에서는 간단한 예를 보여 드리겠습니다. 자세한 내용은 MSDN의 [LINQ 고려 사항 (WCF Data Services)](https://msdn.microsoft.com/library/ee622463.aspx) 항목을 참조 하십시오.

### <a name="filtering-filter"></a>필터링 ($filter)

필터링 하려면 `where` 절을 사용 합니다. 다음 예제에서는 제품 범주별로 필터링 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample7.cs)]

이 코드는 다음 OData 쿼리에 해당 합니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample8.cmd)]

프록시는 `where` 절을 OData `$filter` 식으로 변환 합니다.

### <a name="sorting-orderby"></a>정렬 ($orderby)

정렬 하려면 `orderby` 절을 사용 합니다. 다음 예에서는 가격을 기준으로 내림차순으로 정렬 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample9.cs)]

해당 OData 요청은 다음과 같습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample10.cmd)]

### <a name="client-side-paging-skip-and-top"></a>클라이언트 쪽 페이징 ($skip 및 $top)

대량 엔터티 집합의 경우 클라이언트에서 결과 수를 제한할 수 있습니다. 예를 들어 클라이언트에는 한 번에 10 개의 항목이 표시 될 수 있습니다. 이를 *클라이언트 쪽 페이징*이라고 합니다. 서버 [쪽 페이징은](../supporting-odata-query-options.md#server-paging)서버에서 결과 수를 제한 하는 역할도 합니다. 클라이언트 쪽 페이징을 수행 하려면 LINQ **Skip** 및 **Take** 메서드를 사용 합니다. 다음 예에서는 첫 번째 40 결과를 건너뛰고 다음 10 개를 사용 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample11.cs)]

해당 OData 요청은 다음과 같습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample12.cmd)]

### <a name="select-select-and-expand-expand"></a>($Select)를 선택 하 고 확장 ($expand)

관련 엔터티를 포함 하려면 `DataServiceQuery<t>.Expand` 메서드를 사용 합니다. 예를 들어 각 `Product`에 대 한 `Supplier`를 포함 하려면 다음을 수행 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample13.cs)]

해당 OData 요청은 다음과 같습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample14.cmd)]

응답의 셰이프를 변경 하려면 LINQ **select** 절을 사용 합니다. 다음 예에서는 각 제품의 이름만 가져오며 다른 속성은 포함 하지 않습니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample15.cs)]

해당 OData 요청은 다음과 같습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample16.cmd)]

Select 절은 관련 엔터티를 포함할 수 있습니다. 이 경우에는 **확장**을 호출 하지 마십시오. 이 경우 프록시는 자동으로 확장을 포함 합니다. 다음 예에서는 각 제품의 이름과 공급자를 가져옵니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample17.cs)]

해당 OData 요청은 다음과 같습니다. **$Expand** 옵션이 포함 되어 있습니다.

[!code-console[Main](calling-an-odata-service-from-a-net-client/samples/sample18.cmd)]

$Select 및 $expand에 대 한 자세한 내용은 [WEB API 2에서 $select, $expand 및 $Value 사용](../using-select-expand-and-value.md)을 참조 하세요.

## <a name="add-a-new-entity"></a>새 엔터티 추가

엔터티 집합에 새 엔터티를 추가 하려면 `AddToEntitySet`를 호출 합니다. 여기서 *EntitySet* 은 엔터티 집합의 이름입니다. 예를 들어 `AddToProducts`는 `Products` 엔터티 집합에 새 `Product`를 추가 합니다. 프록시를 생성할 때 WCF Data Services는 이러한 강력한 형식의 **AddTo** 메서드를 자동으로 만듭니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample19.cs)]

두 엔터티 간에 링크를 추가 하려면 **addlink** 및 **setlink** 메서드를 사용 합니다. 다음 코드는 새 공급 업체와 새 제품을 추가한 다음 두 제품 간에 링크를 만듭니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample20.cs)]

탐색 속성이 컬렉션인 경우 **Addlink** 를 사용 합니다. 이 예에서는 공급자의 `Products` 컬렉션에 제품을 추가 합니다.

탐색 속성이 단일 엔터티인 경우 **Setlink** 를 사용 합니다. 이 예에서는 제품의 `Supplier` 속성을 설정 합니다.

## <a name="update--patch"></a>업데이트/패치

엔터티를 업데이트 하려면 **Updateobject** 메서드를 호출 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample21.cs)]

**SaveChanges**를 호출 하면 업데이트가 수행 됩니다. 기본적으로 WCF는 HTTP MERGE 요청을 보냅니다. **PatchOnUpdate** 옵션은 HTTP 패치를 보내도록 WCF에 지시 합니다.

> [!NOTE]
> 패치 및 병합 이유 원래 HTTP 1.1 사양 ([RCF 2616](http://tools.ietf.org/html/rfc2616))이 "부분 업데이트" 의미 체계를 사용 하 여 http 메서드를 정의 하지 않았습니다. 부분 업데이트를 지원 하기 위해 OData 사양은 MERGE 메서드를 정의 합니다. 2010에서 [RFC 5789](http://tools.ietf.org/html/rfc5789) 은 부분 업데이트에 대 한 PATCH 메서드를 정의 했습니다. WCF Data Services 블로그의이 [블로그 게시물](https://blogs.msdn.com/b/astoriateam/archive/2008/05/20/merge-vs-replace-semantics-for-update-operations.aspx) 에서 일부 기록을 읽을 수 있습니다. 현재는 MERGE 보다 패치를 선호 합니다. Web API 스 캐 폴딩에서 만든 OData 컨트롤러는 두 가지 방법을 모두 지원 합니다.

전체 엔터티 (의미 체계 배치)를 대체 하려면 **ReplaceOnUpdate** 옵션을 지정 합니다. 이렇게 하면 WCF에서 HTTP PUT 요청을 보냅니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample22.cs)]

## <a name="delete-an-entity"></a>엔터티 삭제

엔터티를 삭제 하려면 **DeleteObject**를 호출 합니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample23.cs)]

## <a name="invoke-an-odata-action"></a>OData 동작 호출

OData에서 [작업](odata-actions.md) 은 엔터티에 대 한 CRUD 작업으로 쉽게 정의 되지 않는 서버 쪽 동작을 추가 하는 방법입니다.

OData 메타 데이터 문서에서 작업을 설명 하지만 프록시 클래스에서 해당 작업에 대 한 강력한 형식의 메서드를 만들지는 않습니다. 제네릭 **Execute** 메서드를 사용 하 여 여전히 OData 작업을 호출할 수 있습니다. 그러나 매개 변수의 데이터 형식과 반환 값을 알고 있어야 합니다.

예를 들어 `RateProduct` 작업은 `Int32` 형식의 "등급" 이라는 매개 변수를 사용 하 고 `double`을 반환 합니다. 다음 코드에서는이 작업을 호출 하는 방법을 보여 줍니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample24.cs)]

자세한 내용은[서비스 작업 및 작업 호출](https://msdn.microsoft.com/library/hh230677.aspx)을 참조 하세요.

한 가지 옵션은 **컨테이너** 클래스를 확장 하 여 동작을 호출 하는 강력한 형식의 메서드를 제공 하는 것입니다.

[!code-csharp[Main](calling-an-odata-service-from-a-net-client/samples/sample25.cs)]
