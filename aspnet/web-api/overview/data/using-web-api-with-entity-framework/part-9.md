---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-9
title: 데이터베이스에 새 항목 추가 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0967c29e-e124-4db0-a788-c45d0ff5aff2
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-9
msc.type: authoredcontent
ms.openlocfilehash: 692269a2c11e529af78f24feca74bba704b5b54b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78448973"
---
# <a name="add-a-new-item-to-the-database"></a>데이터베이스에 새 항목 추가

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 사용자가 새 책을 만드는 기능을 추가 합니다. Node.js에서 뷰 모델에 다음 코드를 추가 합니다.

[!code-javascript[Main](part-9/samples/sample1.js)]

Index cshtml에서 다음 태그를 바꿉니다.

[!code-html[Main](part-9/samples/sample2.html)]

다음으로 바꿉니다.

[!code-html[Main](part-9/samples/sample3.html)]

이 태그는 새 작성자를 제출 하기 위한 폼을 만듭니다. Author 드롭다운 목록의 값은 뷰 모델에서 관찰 가능한 `authors`에 대 한 데이터 바인딩됩니다. 다른 양식 입력의 경우 값은 뷰 모델의 `newBook` 속성에 데이터 바인딩됩니다.

양식의 제출 처리기는 `addBook` 함수에 바인딩됩니다.

[!code-html[Main](part-9/samples/sample4.html)]

`addBook` 함수는 데이터 바인딩된 양식 입력의 현재 값을 읽어 JSON 개체를 만듭니다. 그런 다음 `/api/books`에 JSON 개체를 게시 합니다.

> [!div class="step-by-step"]
> [이전](part-8.md)
> [다음](part-10.md)
