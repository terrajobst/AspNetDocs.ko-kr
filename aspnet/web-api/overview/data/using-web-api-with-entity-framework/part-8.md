---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-8
title: 항목 세부 정보 표시 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 75ef94b1-bbec-4681-9210-452dba816144
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-8
msc.type: authoredcontent
ms.openlocfilehash: 3f48c5ad73ceb9a4873fbbb621b518553a498966
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449003"
---
# <a name="display-item-details"></a>항목 세부 정보 표시

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 각 책에 대 한 세부 정보를 볼 수 있는 기능을 추가 합니다. Node.js에서 뷰 모델에 다음 코드를 추가 합니다.

[!code-javascript[Main](part-8/samples/sample1.js)]

Views/Home/Index. cshtml에서 데이터 바인딩 요소를 세부 정보 링크에 추가 합니다.

[!code-html[Main](part-8/samples/sample2.html?highlight=5)]

&gt; 요소 &lt;의 클릭 처리기를 뷰 모델의 `getBookDetail` 함수에 바인딩합니다.

동일한 파일에서 다음 표시를 바꿉니다.

[!code-html[Main](part-8/samples/sample3.html)]

다음 코드로 바꿉니다.

[!code-html[Main](part-8/samples/sample4.html)]

이 태그는 뷰 모델의 `detail` 관찰 가능 속성에 데이터 바인딩된 테이블을 만듭니다.

"&lt;!--ko--&gt;&quot; 구문을 사용 하면 DOM 요소 외부에 녹아웃 바인딩을 포함할 수 있습니다. 이 경우 `if` 바인딩은 `details` null이 아닌 경우에만 태그의이 섹션을 표시 합니다.

[!code-html[Main](part-8/samples/sample5.html)]

이제 앱을 실행 하 고 &quot;세부 정보&quot; 링크 중 하나를 클릭 하면 앱에 책 세부 정보가 표시 됩니다.

[![](part-8/_static/image2.png)](part-8/_static/image1.png)

> [!div class="step-by-step"]
> [이전](part-7.md)
> [다음](part-9.md)
