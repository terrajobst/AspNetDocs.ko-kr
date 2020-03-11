---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2-ASP.NET 4. x의 미디어 포맷터
author: MikeWasson
description: ASP.NET 4.x의 ASP.NET Web API에서 추가 미디어 형식을 지 원하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448943"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a>ASP.NET Web API 2의 미디어 포맷터

[Mike Wasson](https://github.com/MikeWasson)

이 자습서에서는 ASP.NET Web API에서 추가 미디어 형식을 지 원하는 방법을 보여 줍니다.

## <a name="internet-media-types"></a>인터넷 미디어 유형

MIME 형식이 라고도 하는 미디어 유형은 데이터의 형식을 식별 합니다. HTTP에서 미디어 유형은 메시지 본문의 형식을 설명 합니다. 미디어 유형은 형식 및 하위 형식 이라는 두 개의 문자열로 구성 되어 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

- text/html
- image/png
- application/json

HTTP 메시지에 엔터티 본문이 포함 되어 있는 경우 Content-type 헤더는 메시지 본문의 형식을 지정 합니다. 메시지 본문의 내용을 구문 분석 하는 방법을 수신자에 게 알립니다.

예를 들어 HTTP 응답이 PNG 이미지를 포함 하는 경우 응답에는 다음과 같은 헤더가 있을 수 있습니다.

[!code-console[Main](media-formatters/samples/sample1.cmd)]

클라이언트는 요청 메시지를 보낼 때 Accept 헤더를 포함할 수 있습니다. Accept 헤더는 클라이언트가 서버에서 원하는 미디어 유형을 서버에 알려 줍니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

[!code-console[Main](media-formatters/samples/sample2.cmd)]

이 헤더는 클라이언트가 HTML, XHTML 또는 XML 중 하나를 원하는 지를 서버에 알려 줍니다.

미디어 유형은 웹 API에서 HTTP 메시지 본문을 직렬화 및 deserialize 하는 방법을 결정 합니다. Web API는 XML, JSON, BSON 및 양식 x-www-form-urlencoded 데이터를 기본적으로 지원 하며 *미디어 포맷터*를 작성 하 여 추가 미디어 유형을 지원할 수 있습니다.

미디어 포맷터를 만들려면 다음 클래스 중 하나에서 파생 합니다.

- [MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx). 이 클래스는 비동기 읽기 및 쓰기 메서드를 사용 합니다.
- [BufferedMediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx). 이 클래스는 **MediaTypeFormatter** 에서 파생 되지만 동기 읽기/쓰기 메서드를 사용 합니다.

비동기 코드가 없기 때문에 **BufferedMediaTypeFormatter** 에서 파생 하는 것이 더 간단 하지만 i/o 중에 호출 스레드가 차단 될 수 있음을 의미 하기도 합니다.

## <a name="example-creating-a-csv-media-formatter"></a>예: CSV 미디어 포맷터 만들기

다음 예에서는 Product 개체를 CSV (쉼표로 구분 된 값) 형식으로 serialize 할 수 있는 미디어 유형 포맷터를 보여 줍니다. 이 예에서는 [CRUD 작업을 지 원하는 WEB API 만들기](../older-versions/creating-a-web-api-that-supports-crud-operations.md)자습서에 정의 된 제품 유형을 사용 합니다. Product 개체의 정의는 다음과 같습니다.

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

CSV 포맷터를 구현 하려면 **BufferedMediaTypeFormatter**에서 파생 되는 클래스를 정의 합니다.

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

생성자에서 포맷터가 지 원하는 미디어 형식을 추가 합니다. 이 예제에서 포맷터는 단일 미디어 유형인 &quot;text/csv&quot;를 지원 합니다.

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

다음과 같이 **Canwritetype** 메서드를 재정의 하 여 포맷터가 serialize 할 수 있는 형식을 표시 합니다.

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

이 예제에서 포맷터는 단일 `Product` 개체 뿐만 아니라 `Product` 개체의 컬렉션을 serialize 할 수 있습니다.

마찬가지로 **CanReadType** 메서드를 재정의 하 여 포맷터가 deserialize 할 수 있는 형식을 표시 합니다. 이 예제에서 포맷터는 deserialization을 지원 하지 않으므로 메서드는 단순히 **false**를 반환 합니다.

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

마지막으로 **WriteToStream** 메서드를 재정의 합니다. 이 메서드는 스트림에 작성 하 여 형식을 serialize 합니다. 포맷터가 deserialization을 지 원하는 경우 **Readfromstream** 메서드를 재정의 합니다.

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>웹 API 파이프라인에 미디어 포맷터 추가

웹 API 파이프라인에 미디어 유형 포맷터를 추가 하려면 **Httpconfiguration** 개체에서 **포맷터** 속성을 사용 합니다.

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>문자 인코딩

필요에 따라 미디어 포맷터는 UTF-8 또는 ISO 8859-1 같은 여러 문자 인코딩을 지원할 수 있습니다.

생성자에서 **Supportedencodings** 컬렉션에 하나 이상의 [System.Text.Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) system.string 형식을 추가 합니다. 기본 인코딩을 먼저 배치 합니다.

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

**WriteToStream** 및 **readfromstream** 메서드에서 [MediaTypeFormatter](https://msdn.microsoft.com/library/hh969054.aspx) 를 호출 하 여 기본 문자 인코딩을 선택 합니다. 이 메서드는 지원 되는 인코딩 목록과 요청 헤더를 일치 시킵니다. 스트림에서 읽거나 쓸 때 반환 된 **인코딩을** 사용 합니다.

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
