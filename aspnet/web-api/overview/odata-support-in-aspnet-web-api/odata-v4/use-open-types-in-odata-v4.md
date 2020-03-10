---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: ASP.NET Web API를 사용 하 여 OData v4에서 Open Types Microsoft Docs
author: microsoft
description: OData v4에서 개방형 형식은 형식 정의에 선언 된 속성 외에도 동적 속성을 포함 하는 구조화 된 형식입니다. 열기...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504581"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>ASP.NET Web API를 사용 하 여 OData v4에서 형식 열기

[Microsoft](https://github.com/microsoft) 에서

> OData v4에서 *개방형 형식은* 형식 정의에 선언 된 속성 외에도 동적 속성을 포함 하는 구조화 된 형식입니다. Open types를 사용 하면 데이터 모델에 유연성을 추가할 수 있습니다. 이 자습서에서는 ASP.NET Web API OData에서 open types를 사용 하는 방법을 보여 줍니다.
> 
> 이 자습서에서는 ASP.NET Web API에서 OData 끝점을 만드는 방법을 이미 알고 있다고 가정 합니다. 그렇지 않은 경우 먼저 [OData V4 끝점 만들기](create-an-odata-v4-endpoint.md) 를 읽어 보십시오.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - Web API OData 5.3
> - OData v4

첫째, 일부 OData 용어는 다음과 같습니다.

- 엔터티 형식: 키를 포함 하는 구조화 된 형식입니다.
- 복합 형식: 키가 없는 구조화 된 형식입니다.
- Open type: 동적 속성을 포함 하는 형식입니다. 엔터티 형식과 복합 형식이 모두 열릴 수 있습니다.

동적 속성의 값은 기본 형식, 복합 형식 또는 열거형 형식일 수 있습니다. 또는 이러한 형식의 컬렉션입니다. 개방형 형식에 대 한 자세한 내용은 [OData v4 사양을](http://www.odata.org/documentation/odata-version-4-0/)참조 하십시오.

## <a name="install-the-web-odata-libraries"></a>웹 OData 라이브러리를 설치 합니다.

NuGet 패키지 관리자를 사용 하 여 최신 Web API OData 라이브러리를 설치 합니다. 패키지 관리자 콘솔 창에서 다음을 수행 합니다.

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>CLR 형식 정의

먼저 EDM 모델을 CLR 형식으로 정의 합니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

EDM (엔터티 데이터 모델)을 만든 경우

- `Category`은 열거형 형식입니다.
- `Address`은 복합 유형입니다. (키가 없으므로 엔터티 형식이 아닙니다.)
- `Customer`은 엔터티 형식입니다. (키가 있습니다.)
- `Press`는 개방형 복합 유형입니다.
- `Book`는 개방형 엔터티 형식입니다.

개방형 형식을 만들려면 CLR 형식에 동적 속성을 포함 하는 `IDictionary<string, object>`형식의 속성이 있어야 합니다.

## <a name="build-the-edm-model"></a>EDM 모델 빌드

**ODataConventionModelBuilder** 를 사용 하 여 EDM을 만드는 경우 `Press` 및 `Book` `IDictionary<string, object>` 속성이 있는지 여부에 따라 자동으로 개방형 형식으로 추가 됩니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

**만드는**를 사용 하 여 EDM을 명시적으로 빌드할 수도 있습니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>OData 컨트롤러 추가

그런 다음 OData 컨트롤러를 추가 합니다. 이 자습서에서는 GET 및 POST 요청만 지원 하 고 메모리 내 목록을 사용 하 여 엔터티를 저장 하는 간단한 컨트롤러를 사용 합니다.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

첫 번째 `Book` 인스턴스에는 동적 속성이 없습니다. 두 번째 `Book` 인스턴스에는 다음과 같은 동적 속성이 있습니다.

- "게시 됨": 기본 형식
- "Authors": 기본 형식의 컬렉션
- "OtherCategories": 열거형 형식의 컬렉션입니다.

또한 해당 `Book` 인스턴스의 `Press` 속성에는 다음과 같은 동적 속성이 있습니다.

- "블로그": 기본 형식
- "Address": 복합 형식

## <a name="query-the-metadata"></a>메타 데이터 쿼리

OData 메타 데이터 문서를 가져오려면 GET 요청을 `~/$metadata`으로 보냅니다. 응답 본문은 다음과 같이 표시 됩니다.

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

메타 데이터 문서에서 다음을 확인할 수 있습니다.

- `Book` 및 `Press` 형식의 경우 `OpenType` 특성의 값은 true입니다. `Customer` 및 `Address` 형식에는이 특성이 없습니다.
- `Book` 엔터티 형식에는 네 개의 선언 된 속성, 즉 ISBN, Title 및 Press가 있습니다. OData 메타 데이터는 CLR 클래스의 `Book.Properties` 속성을 포함 하지 않습니다.
- 마찬가지로 `Press` 복합 형식에는 이름 및 범주 라는 두 개의 선언 된 속성만 있습니다. 메타 데이터는 CLR 클래스의 `Press.DynamicProperties` 속성을 포함 하지 않습니다.

## <a name="query-an-entity"></a>엔터티 쿼리

ISBN이 "978-0-7356-7942-9"와 같은 책을 가져오려면 GET 요청을 `~/Books('978-0-7356-7942-9')`으로 보냅니다. 응답 본문은 다음과 같이 표시 됩니다. (보다 쉽게 읽을 수 있도록 들여쓰기)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

동적 속성은 선언 된 속성을 사용 하 여 인라인으로 포함 됩니다.

## <a name="post-an-entity"></a>엔터티 게시

책 엔터티를 추가 하려면 `~/Books`에 POST 요청을 보냅니다. 클라이언트는 요청 페이로드에서 동적 속성을 설정할 수 있습니다.

예제 요청은 다음과 같습니다. "Price" 및 "게시 된" 속성을 확인 합니다.

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

컨트롤러 메서드에서 중단점을 설정 하는 경우 Web API가 `Properties` 사전에 이러한 속성을 추가 하는 것을 볼 수 있습니다.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>추가 리소스

[OData 형식 샘플 열기](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)
