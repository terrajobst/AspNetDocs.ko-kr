---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: 경로 제약 조건 만들기 (C#) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서 Stephen Walther은 정규식을 사용 하 여 경로 제약 조건을 만들어 브라우저에서 경로를 검색 하는 방식을 제어 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470165"
---
# <a name="creating-a-route-constraint-c"></a>경로 제약 조건 만들기(C#)

[Stephen Walther](https://github.com/StephenWalther)

> 이 자습서에서 Stephen Walther은 정규식을 사용 하 여 경로 제약 조건을 만들어 브라우저에서 경로를 검색 하는 방식을 제어 하는 방법을 보여 줍니다.

경로 제약 조건을 사용 하 여 특정 경로와 일치 하는 브라우저 요청을 제한할 수 있습니다. 정규식을 사용 하 여 경로 제약 조건을 지정할 수 있습니다.

예를 들어 Global.asax 파일에서 목록 1에 경로를 정의 했다고 가정해 보겠습니다.

**목록 1-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

목록 1에는 Product 라는 경로가 포함 되어 있습니다. 제품 경로를 사용 하 여 브라우저 요청을 목록 2에 포함 된 제품 컨트롤러에 매핑할 수 있습니다.

**목록 2-Controllers\ProductController.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

제품 컨트롤러에서 노출 하는 Details () 작업은 productId 라는 단일 매개 변수를 허용 합니다. 이 매개 변수는 정수 매개 변수입니다.

목록 1에 정의 된 경로는 다음 Url과 일치 합니다.

- /Cv3
- /제품/7

불행 하 게도 경로는 다음 Url과 일치 합니다.

- /Product/blah
- /> Apple

Details () 작업에는 정수 매개 변수가 필요 하기 때문에 정수 값이 아닌 다른 항목을 포함 하는 요청을 수행 하면 오류가 발생 합니다. 예를 들어, 브라우저에 URL/Dva/>를 입력 하면 그림 1에 오류 페이지가 표시 됩니다.

[새 프로젝트 대화 상자 ![](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)

**그림 01**: 페이지 분해[보기 (전체 크기 이미지를 보려면 클릭](creating-a-route-constraint-cs/_static/image2.png))

원하는 것은 적절 한 정수 productId를 포함 하는 Url과 일치 하는 것입니다. 경로를 정의할 때 제약 조건을 사용 하 여 경로와 일치 하는 Url을 제한할 수 있습니다. 목록 3의 수정 된 제품 경로에는 정수와 일치 하는 정규식 제약 조건이 포함 되어 있습니다.

**목록 3-Global.asax.cs**

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

정규식 \d +는 하나 이상의 정수와 일치 합니다. 이 제약 조건으로 인해 제품 경로가 다음 Url과 일치 합니다.

- /Product/3
- /Cv99

그러나 다음 Url은 그렇지 않습니다.

- /> Apple
- /Product

- 이러한 브라우저 요청은 다른 경로에 의해 처리 되거나, 일치 하는 경로가 없는 경우 리소스를 *찾을* 수 없습니다. 오류가 반환 됩니다.

> [!div class="step-by-step"]
> [이전](creating-custom-routes-cs.md)
> [다음](creating-a-custom-route-constraint-cs.md)
