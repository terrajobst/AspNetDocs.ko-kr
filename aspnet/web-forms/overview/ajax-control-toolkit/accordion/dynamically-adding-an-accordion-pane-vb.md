---
uid: web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
title: 아코디언 창 동적 추가 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 아코디언 컨트롤은 여러 창을 제공 하 고 사용자가 한 번에 하나씩 표시할 수 있도록 합니다. 패널은 일반적으로 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: fae968c9-1902-487d-b053-86a46dd52c3f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/dynamically-adding-an-accordion-pane-vb
msc.type: authoredcontent
ms.openlocfilehash: be48db5ea3de4af46b0f864cc9e73d2f518294a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78484145"
---
# <a name="dynamically-adding-an-accordion-pane-vb"></a>동적으로 아코디언 창 추가 (VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion2.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion2VB.pdf)

> AJAX 컨트롤 도구 키트의 아코디언 컨트롤은 여러 창을 제공 하 고 사용자가 한 번에 하나씩 표시할 수 있도록 합니다. 패널은 일반적으로 페이지 자체 내에서 선언 되지만 서버측 코드를 사용 하 여 동일한 결과를 얻을 수 있습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 아코디언 컨트롤은 여러 창을 제공 하 고 사용자가 한 번에 하나씩 표시할 수 있도록 합니다. 패널은 일반적으로 페이지 자체 내에서 선언 되지만 서버측 코드를 사용 하 여 동일한 결과를 얻을 수 있습니다.

## <a name="steps"></a>단계

아코디언 컨트롤은 모든 중요 한 속성을 서버 쪽 코드에 노출 합니다. 무엇 보다도 `Panes` 속성은 아코디언을 구성 하는 창의 컬렉션에 대 한 액세스 권한을 부여 합니다. 모든 창에는 `AccordionPane`유형이 있습니다. 따라서 이러한 창을 만드는 것은 간단 합니다.

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample1.vb)]

`AccordionPane`의 `HeaderContainer` 속성은 창의 헤더 섹션 내에서 ASP.NET 컨트롤에 대 한 액세스를 제공 합니다. `AccordionPane`의 `ContentContainer` 속성은 창의 내용 섹션에 대해 동일 하 게 수행 됩니다. 이렇게 하면 ASP.NET 코드에서 창에 콘텐츠를 추가할 수 있습니다.

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample2.vb)]

마지막으로, 창을 아코디언의 `Panes` 컬렉션에 추가 해야 합니다.

[!code-vb[Main](dynamically-adding-an-accordion-pane-vb/samples/sample3.vb)]

다음은 두 개의 창을 아코디언 컨트롤에 추가 하는 전체 서버 쪽 코드입니다.

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample4.aspx)]

유일한 요소는 ASP.NET `ScriptManager` 컨트롤의 존재 여부에 따라 달라 지는 아코디언 자체입니다.

[!code-aspx[Main](dynamically-adding-an-accordion-pane-vb/samples/sample5.aspx)]

예제를 완료 하기 위해 아코디언 컨트롤에서 참조 되는 두 개의 CSS 클래스는 브라우저에 대 한 스타일 정보를 제공 합니다.

[!code-css[Main](dynamically-adding-an-accordion-pane-vb/samples/sample6.css)]

[서버 쪽 코드에서 아코디언의 데이터를 동적으로 추가한 ![](dynamically-adding-an-accordion-pane-vb/_static/image2.png)](dynamically-adding-an-accordion-pane-vb/_static/image1.png)

아코디언의 데이터는 서버 쪽 코드에 의해 동적으로 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](dynamically-adding-an-accordion-pane-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](databinding-to-an-accordion-vb.md)
