---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'ASP.NET Web API에서 HTML 양식 데이터 보내기: x-www-form-urlencoded Data-ASP.NET 4.x'
author: MikeWasson
description: 이 문서에서는 ASP.NET 4.x를 사용 하 여 Web API 컨트롤러에 양식 x-www-form-urlencoded 데이터를 게시 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449243"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a>ASP.NET Web API에서 HTML 양식 데이터 보내기: 양식 x-www-form-urlencoded 데이터

[Mike Wasson](https://github.com/MikeWasson)

## <a name="part-1-form-urlencoded-data"></a>1 부: 양식 x-www-form-urlencoded 데이터

이 문서에서는 Web API 컨트롤러에 양식-x-www-form-urlencoded 데이터를 게시 하는 방법을 보여 줍니다.

- [HTML 양식 개요](#overview_of_html_forms)
- [복합 형식 보내기](#sending_complex_types)
- [AJAX를 통해 폼 데이터 보내기](#sending_form_data_via_ajax)
- [단순 형식 보내기](#sending_simple_types)

> [!NOTE]
> [완료 된 프로젝트를 다운로드](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007)합니다.

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a>HTML 양식 개요

HTML 양식은 GET 또는 POST를 사용 하 여 서버에 데이터를 보냅니다. **Form** 요소의 **METHOD** 특성은 HTTP 메서드를 제공 합니다.

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

기본 메서드는 GET입니다. 폼에서 GET을 사용 하는 경우 양식 데이터는 URI에서 쿼리 문자열로 인코딩됩니다. 폼에서 POST를 사용 하는 경우 양식 데이터가 요청 본문에 배치 됩니다. 게시 된 데이터의 경우 **enctype** 특성은 요청 본문의 형식을 지정 합니다.

| enctype | Description |
| --- | --- |
| application/x-www-form-urlencoded | 양식 데이터는 URI 쿼리 문자열과 비슷하게 이름/값 쌍으로 인코딩됩니다. POST에 대 한 기본 형식입니다. |
| 다중 파트/폼 데이터 | 양식 데이터는 다중 파트 MIME 메시지로 인코딩됩니다. 서버에 파일을 업로드 하는 경우이 형식을 사용 합니다. |

이 문서의 1 부에서는 x-www-form-urlencoded 형식을 살펴봅니다. [2 부](sending-html-form-data-part-2.md) 에서는 다중 부분 MIME을 설명 합니다.

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a>복합 형식 보내기

일반적으로 여러 양식 컨트롤에서 가져온 값으로 구성 되는 복합 형식을 보냅니다. 상태 업데이트를 나타내는 다음 모델을 고려 하십시오.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

다음은 POST를 통해 `Update` 개체를 수락 하는 Web API 컨트롤러입니다.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> 이 컨트롤러는 [작업 기반 라우팅을](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)사용 하므로 경로 템플릿은 api/{controller}/{action}/{id}&quot;&quot;됩니다. 클라이언트는 &quot;/api/updates/complex&quot;에 데이터를 게시 합니다.

이제 사용자가 상태 업데이트를 제출 하는 HTML 양식을 작성해 보겠습니다.

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

폼의 **action** 특성은 컨트롤러 작업의 URI입니다. 다음은에 입력 된 일부 값이 있는 폼입니다.

![](sending-html-form-data-part-1/_static/image1.png)

사용자가 제출을 클릭 하면 브라우저에서 다음과 같은 HTTP 요청을 보냅니다.

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

요청 본문에는 이름/값 쌍으로 형식이 지정 된 양식 데이터가 포함 되어 있습니다. Web API는 이름/값 쌍을 자동으로 `Update` 클래스의 인스턴스로 변환 합니다.

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a>AJAX를 통해 폼 데이터 보내기

사용자가 폼을 제출 하면 브라우저가 현재 페이지에서 벗어나 응답 메시지의 본문을 렌더링 합니다. 응답이 HTML 페이지인 경우에는이 기능을 사용할 수 없습니다. 그러나 web API를 사용 하는 경우 응답 본문은 일반적으로 비어 있거나 JSON과 같은 구조화 된 데이터를 포함 합니다. 이 경우 페이지에서 응답을 처리할 수 있도록 AJAX 요청을 사용 하 여 폼 데이터를 전송 하는 것이 더 적합 합니다.

다음 코드에서는 jQuery를 사용 하 여 폼 데이터를 게시 하는 방법을 보여 줍니다.

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

JQuery **submit** 함수는 form 작업을 새 함수로 바꿉니다. 이는 제출 단추의 기본 동작을 재정의 합니다. **Serialize** 함수는 폼 데이터를 이름/값 쌍으로 serialize 합니다. 서버에 폼 데이터를 전송 하려면 `$.post()`를 호출 합니다.

요청이 완료 되 면 `.success()` 또는 `.error()` 처리기가 사용자에 게 적절 한 메시지를 표시 합니다.

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a>단순 형식 보내기

이전 섹션에서는 모델 클래스의 인스턴스로 deserialize 된 Web API를 복합 형식으로 보냈습니다. 문자열 등의 단순 형식을 보낼 수도 있습니다.

> [!NOTE]
> 단순 형식을 보내기 전에 복합 형식의 값을 대신 래핑하는 것이 좋습니다. 이렇게 하면 서버 쪽에서 모델 유효성 검사의 이점을 얻을 수 있으며 필요한 경우 모델을 더 쉽게 확장할 수 있습니다.

단순 유형을 전송 하는 기본 단계는 동일 하지만 두 가지 미묘한 차이점이 있습니다. 먼저 컨트롤러에서 **Frombody** 특성을 사용 하 여 매개 변수 이름을 데코레이팅 해야 합니다.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

기본적으로 웹 API는 요청 URI에서 단순 형식을 가져오려고 시도 합니다. **Frombody** 특성은 요청 본문에서 값을 읽도록 웹 API에 지시 합니다.

> [!NOTE]
> Web API는 응답 본문을 한 번만 읽어서 요청 본문에서 동작의 매개 변수를 하나만 가져올 수 있습니다. 요청 본문에서 여러 값을 가져와야 하는 경우에는 복합 형식을 정의 합니다.

둘째, 클라이언트는 다음 형식의 값을 보내야 합니다.

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

특히 이름/값 쌍의 이름 부분은 단순 형식에 대해 비어 있어야 합니다. 모든 브라우저에서 HTML 폼에 대해이 기능을 지원 하지는 않지만 다음과 같이 스크립트에서이 형식을 만들 수 있습니다.

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

예제 폼은 다음과 같습니다.

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

폼 값을 제출 하는 스크립트는 다음과 같습니다. 이전 스크립트의 유일한 차이점은 **post** 함수로 전달 되는 인수입니다.

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

동일한 방법을 사용 하 여 단순 형식의 배열을 보낼 수 있습니다.

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a>추가 리소스

[2 부: 파일 업로드 및 다중 파트 MIME](sending-html-form-data-part-2.md)
