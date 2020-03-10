---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API의 모델 유효성 검사-ASP.NET 4.x
author: MikeWasson
description: ASP.NET 4.x 용 ASP.NET Web API의 모델 유효성 검사 개요.
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448931"
---
# <a name="model-validation-in-aspnet-web-api"></a>ASP.NET Web API의 모델 유효성 검사

[Mike Wasson](https://github.com/MikeWasson)

이 문서에서는 모델에 주석을 달고 데이터 유효성 검사에 주석을 사용 하 고 web API에서 유효성 검사 오류를 처리 하는 방법을 보여 줍니다. 클라이언트에서 web API로 데이터를 전송 하는 경우 처리를 수행 하기 전에 데이터의 유효성을 검사 하는 경우가 많습니다. 

## <a name="data-annotations"></a>데이터 주석

ASP.NET Web API에서 [system.componentmodel](/dotnet/api/system.componentmodel.dataannotations) 네임 스페이스의 특성을 사용 하 여 모델의 속성에 대 한 유효성 검사 규칙을 설정할 수 있습니다. 다음 모델을 살펴보세요.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

ASP.NET MVC에서 모델 유효성 검사를 사용한 경우에는 잘 알고 있어야 합니다. **필수** 특성은 `Name` 속성이 null이 아니어야 함을 의미 합니다. **Range** 특성은 `Weight` 0에서 999 사이 여야 함을 의미 합니다.

클라이언트에서 다음 JSON 표현으로 POST 요청을 보내는 것으로 가정 합니다.

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

필수로 표시 된 `Name` 속성이 클라이언트에 포함 되지 않은 것을 볼 수 있습니다. Web API가 JSON을 `Product` 인스턴스로 변환 하는 경우 유효성 검사 특성에 대해 `Product`의 유효성을 검사 합니다. 컨트롤러 작업에서 모델이 유효한 지 여부를 확인할 수 있습니다.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

모델 유효성 검사는 클라이언트 데이터의 안전성을 보장 하지 않습니다. 응용 프로그램의 다른 계층에서 추가 유효성 검사가 필요할 수 있습니다. 예를 들어 데이터 계층에서 foreign key 제약 조건을 적용할 수 있습니다. [웹 API를 사용 하 여 Entity Framework에](../data/using-web-api-with-entity-framework/part-1.md) 대 한 자습서에서는 이러한 문제 중 일부를 살펴봅니다.

**"게시 중"** : 클라이언트에서 일부 속성을 벗어날 때 게시가 발생 합니다. 예를 들어 클라이언트에서 다음을 전송 한다고 가정 합니다.

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

여기서 클라이언트는 `Price` 또는 `Weight`에 대 한 값을 지정 하지 않았습니다. JSON 포맷터는 0의 기본값을 누락 된 속성에 할당 합니다.

![](model-validation-in-aspnet-web-api/_static/image1.png)

모델 상태는 유효 합니다. 0은 이러한 속성에 대해 유효한 값입니다. 이것이 문제 인지 여부는 시나리오에 따라 달라 집니다. 예를 들어 업데이트 작업에서 "0"과 "not set"을 구분 해야 할 수 있습니다. 클라이언트에서 값을 설정 하도록 하려면 속성을 nullable로 설정 하 고 **필요한** 특성을 설정 합니다.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

**"과도 한 게시"** : 클라이언트는 예상 보다 *많은* 데이터를 보낼 수도 있습니다. 다음은 그 예입니다.

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

여기서 JSON에는 `Product` 모델에 없는 속성 ("Color")이 포함 되어 있습니다. 이 경우 JSON 포맷터는이 값을 무시 합니다. XML 포맷터는 동일 하 게 수행 됩니다. 오버 게시를 사용 하면 모델에 읽기 전용으로 설정 된 속성이 있는 경우 문제가 발생 합니다. 다음은 그 예입니다.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

사용자가 `IsAdmin` 속성을 업데이트 하 고 관리자에 게 권한을 상승 시 키라는 것을 원하지 않습니다. 가장 안전한 전략은 클라이언트에서 보낼 수 있는 것과 정확히 일치 하는 모델 클래스를 사용 하는 것입니다.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> Brad Wilson의 블로그 게시물 "[ASP.NET MVC의 입력 유효성 검사 및 모델 유효성 검사](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)"는 게시 중인 게시 및 과도 한 게시에 대 한 좋은 토론입니다. Post가 ASP.NET MVC 2에 대 한 것 이지만 문제는 Web API와도 관련이 있습니다.

## <a name="handling-validation-errors"></a>유효성 검사 오류 처리

유효성 검사에 실패 하는 경우 Web API는 자동으로 오류를 클라이언트에 반환 하지 않습니다. 모델 상태를 확인 하 고 적절 하 게 응답 하는 것은 컨트롤러 작업입니다.

또한 컨트롤러 작업을 호출 하기 전에 모델 상태를 확인 하는 작업 필터를 만들 수 있습니다. 다음은 예를 보여 주는 코드입니다.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

모델 유효성 검사가 실패 하는 경우이 필터는 유효성 검사 오류를 포함 하는 HTTP 응답을 반환 합니다. 이 경우 컨트롤러 작업은 호출 되지 않습니다.

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

모든 Web API 컨트롤러에이 필터를 적용 하려면 필터의 인스턴스를 Httpconfiguration에 추가 **합니다. 필터** 를 구성 하는 동안 컬렉션:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

또 다른 옵션은 개별 컨트롤러 또는 컨트롤러 작업에 대 한 특성으로 필터를 설정 하는 것입니다.

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
