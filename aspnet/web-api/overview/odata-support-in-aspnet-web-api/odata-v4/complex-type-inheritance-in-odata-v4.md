---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: ASP.NET Web API를 사용한 OData v4의 복합 형식 상속 Microsoft Docs
author: microsoft
description: OData v4 사양에 따라 복합 형식은 다른 복합 형식에서 상속할 수 있습니다. 복합 형식은 키가 없는 구조화 된 형식입니다. 웹 API ...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448133"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>ASP.NET Web API와 OData v4의 복합 형식 상속

[Microsoft](https://github.com/microsoft) 에서

> OData v4 [사양](http://www.odata.org/documentation/odata-version-4-0/)에 따라 복합 형식은 다른 복합 형식에서 상속할 수 있습니다. *복합* 형식은 키가 없는 구조화 된 형식입니다. Web API OData 5.3는 복합 형식 상속을 지원 합니다.
> 
> 이 항목에서는 복잡 한 상속 형식을 사용 하 여 EDM (엔터티 데이터 모델)을 빌드하는 방법을 보여 줍니다. 전체 소스 코드는 [OData 복합 형식 상속 샘플](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt)을 참조 하세요.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API OData 5.3
> - OData v4

## <a name="model-hierarchy"></a>모델 계층 구조

복합 형식 상속을 보여 주기 위해 다음 클래스 계층 구조를 사용 합니다.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape`은 추상 복합 형식입니다. `Rectangle`, `Triangle`및 `Circle`은 `Shape`에서 파생 되는 복합 형식이 며 `RoundRectangle` `Rectangle`에서 파생 됩니다. `Window`은 엔터티 형식이 며 `Shape` 인스턴스를 포함 합니다.

이러한 형식을 정의 하는 CLR 클래스는 다음과 같습니다.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>EDM 모델 빌드

EDM을 만들려면 CLR 형식에서 상속 관계를 유추 하는 **ODataConventionModelBuilder**를 사용할 수 있습니다.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

**만드는**를 사용 하 여 EDM을 명시적으로 빌드할 수도 있습니다. 이는 더 많은 코드를 사용 하지만 EDM을 보다 세부적으로 제어할 수 있도록 합니다.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

이러한 두 예제는 동일한 EDM 스키마를 만듭니다.

## <a name="metadata-document"></a>메타 데이터 문서

다음은 복합 형식 상속을 보여 주는 OData 메타 데이터 문서입니다.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

메타 데이터 문서에서 다음을 확인할 수 있습니다.

- `Shape` 복합 형식이 추상 형식입니다.
- `Rectangle`, `Triangle`및 `Circle` 복합 형식에는 `Shape`기본 형식이 있습니다.
- `RoundRectangle` 형식 `Rectangle`기본 형식입니다.

## <a name="casting-complex-types"></a>복합 형식 캐스팅

이제 복합 형식에 대 한 캐스팅이 지원 됩니다. 예를 들어 다음 쿼리는 `Shape` `Rectangle`로 캐스팅 합니다.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

응답 페이로드는 다음과 같습니다.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]
