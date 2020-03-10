---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-2
title: 모델 및 컨트롤러 추가 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 88908ff8-51a9-40eb-931c-a8139128b680
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-2
msc.type: authoredcontent
ms.openlocfilehash: 57dacda421968f341284d89c9a3ad80040c16e25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449189"
---
# <a name="add-models-and-controllers"></a>모델 및 컨트롤러 추가

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 데이터베이스 엔터티를 정의 하는 모델 클래스를 추가 합니다. 그런 다음 해당 엔터티에 대 한 CRUD 작업을 수행 하는 Web API 컨트롤러를 추가 합니다.

## <a name="add-model-classes"></a>모델 클래스 추가

이 자습서에서는 EF (Entity Framework)에 대 한 "Code First" 접근 방법을 사용 하 여 데이터베이스를 만듭니다. Code First를 사용 하 여 C# 데이터베이스 테이블에 해당 하는 클래스를 작성 하 고 EF는 데이터베이스를 만듭니다. 자세한 내용은 [Entity Framework 개발 방법](https://msdn.microsoft.com/library/ms178359%28v=vs.110%29.aspx#dbfmfcf)을 참조 하세요.

도메인 개체를 POCOs (일반-이전 CLR 개체)로 정의 하 여 시작 합니다. 다음 POCOs를 만들게 됩니다.

- 작성자
- Book

솔루션 탐색기에서 모델 폴더를 마우스 오른쪽 단추로 클릭 합니다. **추가**를 선택한 다음 **클래스**를 선택 합니다. 클래스 `Author` 이름을 지정합니다.

![](part-2/_static/image1.png)

Author.cs의 모든 상용구 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](part-2/samples/sample1.cs)]

다음 코드를 사용 하 여 `Book`라는 다른 클래스를 추가 합니다.

[!code-csharp[Main](part-2/samples/sample2.cs)]

Entity Framework은 이러한 모델을 사용 하 여 데이터베이스 테이블을 만듭니다. 각 모델에 대해 `Id` 속성은 데이터베이스 테이블의 기본 키 열이 됩니다.

Book 클래스에서 `AuthorId`는 `Author` 테이블에 외래 키를 정의 합니다. (간단히 하기 위해 각 책에 단일 저자가 있다고 가정 합니다.) Book 클래스에는 관련 된 `Author`에 대 한 탐색 속성도 포함 되어 있습니다. 탐색 속성을 사용 하 여 코드에서 관련 `Author`에 액세스할 수 있습니다. 4 부의 탐색 속성에 대해 자세히 언급 하 고 [엔터티 관계를 처리](part-4.md)합니다.

## <a name="add-web-api-controllers"></a>Web API 컨트롤러 추가

이 섹션에서는 CRUD 작업 (만들기, 읽기, 업데이트 및 삭제)을 지 원하는 Web API 컨트롤러를 추가 합니다. 컨트롤러는 Entity Framework을 사용 하 여 데이터베이스 계층과 통신 합니다.

먼저 file controller/Valuecontroller .cs를 삭제할 수 있습니다. 이 파일에는 웹 API 컨트롤러의 예가 포함 되어 있지만이 자습서에서는 필요 하지 않습니다.

![](part-2/_static/image2.png)

다음으로 프로젝트를 빌드합니다. 웹 API 스 캐 폴딩은 리플렉션을 사용 하 여 모델 클래스를 찾습니다. 따라서 컴파일된 어셈블리가 필요 합니다.

솔루션 탐색기에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 합니다. **추가**를 선택한 다음 **컨트롤러**를 선택 합니다.

![](part-2/_static/image3.png)

**스 캐 폴드 추가** 대화 상자에서 "작업을 사용 하는 웹 API 2 컨트롤러, Entity Framework 사용"을 선택 합니다. **추가**를 클릭합니다.

![](part-2/_static/image4.png)

**컨트롤러 추가** 대화 상자에서 다음을 수행 합니다.

1. **모델 클래스** 드롭다운에서 `Author` 클래스를 선택 합니다. 드롭다운 목록에 표시 되지 않는 경우 프로젝트를 빌드 했는지 확인 합니다.
2. "비동기 컨트롤러 작업 사용"을 선택 합니다.
3. 컨트롤러 이름을 &quot;AuthorsController&quot;으로 그대로 둡니다.
4. **데이터 컨텍스트 클래스**옆에 있는 더하기 (+) 단추를 클릭 합니다.

![](part-2/_static/image5.png)

**새 데이터 컨텍스트** 대화 상자에서 기본 이름을 그대로 두고 **추가**를 클릭 합니다.

![](part-2/_static/image6.png)

**추가** 를 클릭 하 여 **컨트롤러 추가** 대화 상자를 완료 합니다. 대화 상자에서 프로젝트에 두 개의 클래스를 추가 합니다.

- `AuthorsController`는 Web API 컨트롤러를 정의 합니다. 컨트롤러는 클라이언트가 저자 목록에서 CRUD 작업을 수행 하는 데 사용 하는 REST API를 구현 합니다.
- `BookServiceContext`는 런타임에 데이터베이스의 데이터로 개체 채우기, 변경 내용 추적 및 데이터베이스에 데이터 유지를 포함 하는 엔터티 개체를 관리 합니다. `DbContext`에서 상속받습니다.

![](part-2/_static/image7.png)

이제 프로젝트를 다시 빌드합니다. 이제 동일한 단계를 수행 하 여 `Book` 엔터티에 대 한 API 컨트롤러를 추가 합니다. 이번에는 모델 클래스에 대해 `Book`를 선택 하 고 데이터 컨텍스트 클래스에 대해 기존 `BookServiceContext` 클래스를 선택 합니다. 새 데이터 컨텍스트를 만들지 마세요. **추가** 를 클릭 하 여 컨트롤러를 추가 합니다.

![](part-2/_static/image8.png)

> [!div class="step-by-step"]
> [이전](part-1.md)
> [다음](part-3.md)
