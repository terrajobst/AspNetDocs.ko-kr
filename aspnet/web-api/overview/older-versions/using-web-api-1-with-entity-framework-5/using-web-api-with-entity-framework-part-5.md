---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: '5 부: 녹아웃을 사용 하 여 동적 UI 만들기 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78447863"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>5 부: 녹아웃을 사용 하 여 동적 UI 만들기

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>Knockout.js를 사용하여 동적 UI 만들기

이 섹션에서는 node.js를 사용 하 여 관리 보기에 기능을 추가 합니다.

[녹아웃](http://knockoutjs.com/) 은 HTML 컨트롤을 데이터에 쉽게 바인딩할 수 있도록 하는 Javascript 라이브러리입니다. 녹아웃은 MVVM (모델-뷰-ViewModel) 패턴을 사용 합니다.

- *모델* 은 비즈니스 도메인 (이 경우에는 제품 및 주문)의 데이터를 서버 쪽으로 표현한 것입니다.
- *뷰* 는 프레젠테이션 계층 (HTML)입니다.
- *뷰 모델* 은 모델 데이터를 포함 하는 Javascript 개체입니다. 뷰 모델은 UI의 코드 추상화입니다. HTML 표현에 대해 알지 못합니다. 대신, 뷰의 추상 기능 (예: "항목 목록")을 나타냅니다.

뷰가 뷰 모델에 대 한 데이터 바인딩된 뷰입니다. 뷰 모델에 대 한 업데이트는 뷰에 자동으로 반영 됩니다. 뷰 모델은 또한 보기에서 단추 클릭과 같은 이벤트를 가져와서 주문 생성과 같은 모델에 대 한 작업을 수행 합니다.

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

먼저 뷰 모델을 정의 합니다. 그러면 HTML 태그를 뷰 모델에 바인딩합니다.

다음 Razor 섹션을 관리자에 추가 합니다. cshtml:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

이 섹션은 파일의 아무 곳에 나 추가할 수 있습니다. 뷰가 렌더링 되 면 HTML 페이지 맨 아래에 닫는 &lt;/본문&gt; 태그 바로 앞에 섹션이 표시 됩니다.

이 페이지에 대 한 모든 스크립트는 주석으로 표시 된 스크립트 태그 안에 표시 됩니다.

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

먼저 뷰 모델 클래스를 정의 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**observableArray** 는 *관찰*가능 이라고 하는 녹아웃의 특수 한 종류의 개체입니다. [Default.js 설명서](http://knockoutjs.com/documentation/observables.html)에서: 관찰 가능은 "구독자에 게 변경 내용을 알릴 수 있는 JavaScript 개체"입니다. 관찰 가능의 내용이 변경 되 면 뷰가 일치 하도록 자동으로 업데이트 됩니다.

`products` 배열을 채우려면 웹 API에 대 한 AJAX 요청을 수행 합니다. API에 대 한 기본 URI를 보기 모음에 저장 했습니다 (자습서의 [4 부](using-web-api-with-entity-framework-part-4.md) 참조).

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

그런 다음 뷰-모델에 함수를 추가 하 여 제품을 만들고, 업데이트 하 고, 삭제 합니다. 이러한 함수는 AJAX 호출을 web API에 전송 하 고 결과를 사용 하 여 뷰 모델을 업데이트 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

이제 가장 중요 한 부분은 다음과 같습니다. DOM이 fulled 로드 되 면 **ko. applyBindings** 함수를 호출 하 고 `ProductsViewModel`의 새 인스턴스를 전달 합니다.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

**Ko-kr bindings** 메서드는 녹아웃을 활성화 하 고 뷰에 뷰 모델을 배선 합니다.

이제 뷰 모델이 있으므로 바인딩을 만들 수 있습니다. `data-bind` 특성을 HTML 요소에 추가 하 여이 작업을 수행 합니다. 예를 들어, HTML 목록을 배열에 바인딩하려면 `foreach` 바인딩을 사용 합니다.

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

`foreach` 바인딩은 배열을 반복 하 고 배열의 각 개체에 대해 자식 요소를 만듭니다. 자식 요소의 바인딩은 배열 개체의 속성을 참조할 수 있습니다.

"업데이트-제품" 목록에 다음 바인딩을 추가 합니다.

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

`<li>` 요소는 **foreach** 바인딩의 범위 내에서 발생 합니다. 즉, 녹아웃은 `products` 배열의 각 제품에 대해 요소를 한 번씩 렌더링 합니다. `<li>` 요소 내의 모든 바인딩은 해당 제품 인스턴스를 참조 합니다. 예를 들어 `$data.Name`은 제품의 `Name` 속성을 참조 합니다.

텍스트 입력의 값을 설정 하려면 `value` 바인딩을 사용 합니다. 단추는 `click` 바인딩을 사용 하 여 모델 뷰의 함수에 바인딩됩니다. Product 인스턴스는 각 함수에 매개 변수로 전달 됩니다. 자세한 내용은 [default.js 설명서](http://knockoutjs.com/documentation/observables.html) 에서 다양 한 바인딩에 대해 잘 설명 합니다.

다음으로, 제품 추가 양식에서 **전송** 이벤트에 대 한 바인딩을 추가 합니다.

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

이 바인딩은 뷰 모델에서 `create` 함수를 호출 하 여 새 제품을 만듭니다.

관리 보기에 대 한 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

응용 프로그램을 실행 하 고 관리자 계정으로 로그인 한 다음 "관리" 링크를 클릭 합니다. 제품 목록이 표시 되 고 제품을 생성, 업데이트 또는 삭제할 수 있습니다.

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-4.md)
> [다음](using-web-api-with-entity-framework-part-6.md)
