---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: 데이터 전송 개체 만들기 (Dto) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449027"
---
# <a name="create-data-transfer-objects-dtos"></a>DTO(데이터 전송 개체) 만들기

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이제 web API는 데이터베이스 엔터티를 클라이언트에 노출 합니다. 클라이언트는 데이터베이스 테이블에 직접 매핑되는 데이터를 수신 합니다. 그러나 이것이 항상 좋은 것은 아닙니다. 클라이언트에 보내는 데이터의 셰이프를 변경 하려는 경우가 있습니다. 예를 들면 다음과 같습니다.

- 순환 참조를 제거 합니다 (이전 섹션 참조).
- 클라이언트가 볼 수 없는 특정 속성을 숨깁니다.
- 페이로드 크기를 줄이기 위해 일부 속성을 생략 합니다.
- 중첩 된 개체를 포함 하는 개체 그래프를 결합 하 여 클라이언트에 보다 편리 하 게 사용할 수 있도록 합니다.
- "과도 한 게시" 취약성을 방지 합니다. (오버 게시에 대 한 설명은 [모델 유효성 검사](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) 를 참조 하세요.)
- 데이터베이스 계층에서 서비스 계층을 분리 합니다.

이를 위해 DTO ( *데이터 전송 개체* )를 정의할 수 있습니다. DTO는 네트워크를 통해 데이터를 전송 하는 방법을 정의 하는 개체입니다. 설명서 엔터티를 사용 하 여 작동 하는 방식을 살펴보겠습니다. 모델 폴더에서 다음 두 개의 DTO 클래스를 추가 합니다.

[!code-csharp[Main](part-5/samples/sample1.cs)]

`BookDetailDto` 클래스에는 책 모델의 모든 속성이 포함 되어 있습니다. 단, `AuthorName`는 작성자 이름을 포함 하는 문자열입니다. `BookDto` 클래스는 `BookDetailDto`속성의 하위 집합을 포함 합니다.

다음으로 `BooksController` 클래스에서 두 개의 GET 메서드를 Dto를 반환 하는 버전으로 바꿉니다. LINQ **Select** 문을 사용 하 여 Book 엔터티에서 dto로 변환 합니다.

[!code-csharp[Main](part-5/samples/sample2.cs)]

새 `GetBooks` 메서드에서 생성 된 SQL은 다음과 같습니다. EF가 LINQ **select** 를 SQL select 문으로 변환 하는 것을 볼 수 있습니다.

[!code-sql[Main](part-5/samples/sample3.sql)]

마지막으로 `PostBook` 메서드를 수정 하 여 DTO를 반환 합니다.

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> 이 자습서에서는 코드에서 수동으로 Dto로 변환 합니다. 또 다른 옵션은 변환을 자동으로 처리 하는 [Automapper](http://automapper.org/) 와 같은 라이브러리를 사용 하는 것입니다.
> 
> [!div class="step-by-step"]
> [이전](part-4.md)
> [다음](part-6.md)
