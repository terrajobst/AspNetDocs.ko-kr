---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: ASP.NET Web API 2 OData-ASP.NET 4.x의 보안 지침
author: MikeWasson
description: ASP.NET 4.x의 ASP.NET Web API 2에 대해 OData를 통해 데이터 집합을 노출할 때 고려해 야 하는 보안 문제에 대해 설명 합니다.
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448295"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a>ASP.NET Web API 2 OData에 대 한 보안 지침

[Mike Wasson](https://github.com/MikeWasson)

이 항목에서는 ASP.NET 4.x의 ASP.NET Web API 2에 대해 OData를 통해 데이터 집합을 노출할 때 고려해 야 할 몇 가지 보안 문제에 대해 설명 합니다.

## <a name="edm-security"></a>EDM 보안

쿼리 의미 체계는 기본 모델 유형이 아닌 EDM (엔터티 데이터 모델)을 기반으로 합니다. EDM에서 속성을 제외할 수 있으며이 속성은 쿼리에 표시 되지 않습니다. 예를 들어 모델에 급여 속성이 있는 직원 형식이 포함 되어 있다고 가정 합니다. 클라이언트에서이 속성을 숨기려면 EDM에서이 속성을 제외 하는 것이 좋습니다.

EDM에서 속성을 제외 하는 방법에는 두 가지가 있습니다. 모델 클래스의 속성에서 **[Ignoredatamember]** 특성을 설정할 수 있습니다.

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

EDM에서 프로그래밍 방식으로 속성을 제거할 수도 있습니다.

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>쿼리 보안

악의적인 클라이언트나 naive 클라이언트는 실행 하는 데 시간이 오래 걸리는 쿼리를 만들 수 있습니다. 최악의 경우에는 서비스에 대 한 액세스를 중단할 수 있습니다.

**[쿼리할** 수 있는] 특성은 쿼리를 구문 분석 하 고, 유효성을 검사 하 고, 적용 하는 작업 필터입니다. 필터는 쿼리 옵션을 LINQ 식으로 변환 합니다. OData 컨트롤러에서 **iqueryable** 형식을 반환할 때 **iqueryable** linq 공급자는 linq 식을 쿼리로 변환 합니다. 따라서 성능은 사용 되는 LINQ 공급자와 데이터 집합 또는 데이터베이스 스키마의 특정 특성에 따라 달라 집니다.

ASP.NET Web API에서 OData 쿼리 옵션을 사용 하는 방법에 대 한 자세한 내용은 [Odata 쿼리 옵션 지원](supporting-odata-query-options.md)을 참조 하세요.

모든 클라이언트 (예: 엔터프라이즈 환경)를 신뢰할 수 있거나 데이터 집합이 작은 경우 쿼리 성능이 문제가 되지 않을 수 있습니다. 그렇지 않으면 다음과 같은 권장 사항을 고려해 야 합니다.

- 다양 한 쿼리를 사용 하 여 서비스를 테스트 하 고 DB를 프로 파일링 합니다.
- 서버 기반 페이징을 사용 하 여 하나의 쿼리에서 대량 데이터 집합을 반환 하지 않도록 합니다. 자세한 내용은 [서버 기반 페이징](supporting-odata-query-options.md#server-paging)을 참조 하세요. 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- $Filter 및 $orderby 필요 한가요? 일부 응용 프로그램에서는 $top 및 $skip를 사용 하 여 클라이언트 페이징을 허용할 수 있지만 다른 쿼리 옵션을 사용 하지 않도록 설정할 수 있습니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- 클러스터형 인덱스의 속성에 대 한 $orderby 제한 하십시오. 클러스터형 인덱스 없이 많은 양의 데이터를 정렬 하는 속도가 느립니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- 최대 노드 수: **[쿼리 가능]** 의 **MaxNodeCount** 속성은 $filter 구문 트리에서 허용 되는 최대 수 노드를 설정 합니다. 기본값은 100 이지만 더 작은 값을 설정 하는 것이 좋습니다 .이 경우 많은 수의 노드를 컴파일하면 속도가 느려질 수 있습니다. 이는 LINQ to Objects (즉, 중간 LINQ 공급자를 사용 하지 않고 메모리에서 컬렉션에 대 한 LINQ 쿼리)를 사용 하는 경우 특히 그렇습니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- Any () 및 all () 함수를 사용 하지 않도록 설정 하는 것이 좋습니다 .이는 속도가 느릴 수 있습니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- 예를 들어 문자열 속성에 긴&#8212;문자열이 포함 된 경우 제품 설명 또는 블로그 항목&#8212;에서 문자열 함수를 사용 하지 않도록 설정 하는 것이 좋습니다. 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- 탐색 속성에서 필터링을 허용 하지 않는 것이 좋습니다. 탐색 속성을 필터링 하면 조인이 발생할 수 있으며이는 데이터베이스 스키마에 따라 속도가 느릴 수 있습니다. 다음 코드는 탐색 속성에 대 한 필터링을 방지 하는 쿼리 유효성 검사기를 보여 줍니다. 쿼리 유효성 검사기에 대 한 자세한 내용은 [쿼리 유효성 검사](supporting-odata-query-options.md#query-validation)를 참조 하세요. 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- 데이터베이스에 대해 사용자 지정 된 유효성 검사기를 작성 하 여 $filter 쿼리를 제한 하는 것이 좋습니다. 예를 들어 다음 두 가지 쿼리를 고려해 보세요. 

  - 성이 ' A '로 시작 하는 행위자가 있는 모든 동영상
  - 1994에서 릴리스된 모든 동영상

    동영상이 행위자에 의해 인덱싱되지 않은 경우 첫 번째 쿼리에는 전체 동영상 목록을 검색 하는 DB 엔진이 필요할 수 있습니다. 그러나 두 번째 쿼리는 사용할 수 있지만 동영상이 릴리스 연도로 인덱싱되는 것으로 가정 합니다.

    다음 코드에서는 "ReleaseYear" 및 "Title" 속성을 필터링 할 수 있지만 다른 속성은 필터링 할 수 없는 유효성 검사기를 보여 줍니다.

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- 일반적으로 필요한 $filter 함수를 고려 합니다. 클라이언트에 $filter의 전체 표현을 필요 하지 않은 경우 허용 되는 함수를 제한할 수 있습니다.
