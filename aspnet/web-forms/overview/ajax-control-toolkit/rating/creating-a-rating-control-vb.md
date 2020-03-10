---
uid: web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
title: 등급 컨트롤 만들기 (VB) | Microsoft Docs
author: wenz
description: 전자 상거래에서 커뮤니티 사이트로의 많은 websites는 사용자에 게 문서 또는 항목의 등급을 제공 합니다. 일반적으로 몇 가지 코딩 작업이 필요 하지만 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6d0d70f4-725e-4258-8ae8-24a6ba1ddbf7
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/rating/creating-a-rating-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 08e245edfe73db4e3896db51151e5d7a0fa9697c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78496037"
---
# <a name="creating-a-rating-control-vb"></a>등급 컨트롤 만들기(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/rating0.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/rating0VB.pdf)

> 전자 상거래에서 커뮤니티 사이트로의 많은 websites는 사용자에 게 문서 또는 항목의 등급을 제공 합니다. 이 경우 일반적으로 몇 가지 코딩 노력이 필요 하지만, 제어 도구 키트가 있습니다.

## <a name="overview"></a>개요

전자 상거래에서 커뮤니티 사이트로의 많은 websites는 사용자에 게 문서 또는 항목의 등급을 제공 합니다. 이 경우 일반적으로 몇 가지 코딩 노력이 필요 하지만, 제어 도구 키트가 있습니다.

## <a name="steps"></a>단계

먼저 (적어도) 두 종류의 이미지가 표시 됩니다. 하나는 입력 된 등급 항목을 위한 것이 고 다른 하나는 빈 등급 항목입니다. 등급 항목은 일반적으로 별 이거나 웃는 얼굴입니다. 이 시나리오의 경우이 자습서에 대 한 소스 코드 다운로드의 일부로 smiley-done 및 빈 .png 및의 세 가지 파일을 찾을 수 있습니다.

그런 다음 새 ASP.NET 파일을 만들고이 파일에 `ScriptManager` 컨트롤을 추가 하는 것으로 시작 합니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample1.aspx)]

그런 다음 ASP.NET AJAX 컨트롤 도구 키트의 `Rating` 컨트롤을 추가 합니다. 이 예제에 대해 다음 특성을 설정 해야 합니다.

- 사용할 초기 등급을 `CurrentRating` 합니다.
- 최대 등급 `MaxRating`
- 등급 항목 (star)이 비어 있을 때 사용할 CSS 클래스를 `EmptyStarCssClass` 합니다.
- 등급 항목 (별모양)이 채워질 때 사용할 CSS 클래스를 `FilledStarCssClass` 합니다.
- 표시 되는 통계에 사용할 CSS 클래스를 `StarCssClass` 합니다.
- 스타 등급이 서버로 다시 전송 되는 동안 사용할 CSS 클래스를 `WaitingStarCssClass` 합니다.

다음은 처음에 아무것도 채워지지 않은 5 개 항목 (smileys)을 사용 하는 등급 컨트롤을 만드는 태그입니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample2.aspx)]

이제 세 개의 참조 된 CSS 클래스는 CSS를 사용 하 여 쉽게 수행할 수 있는 적절 한 이미지 파일을 표시 해야 합니다.

[!code-css[Main](creating-a-rating-control-vb/samples/sample3.css)]

3 개 이미지의 너비와 높이를 제공 해야 합니다. 그렇지 않으면 디스플레이에서 비트 문제가 발생 한 보일 수 있습니다.

마지막으로 등급의 결과가 사용자에 게 표시 되어야 합니다 (또는 적어도 데이터베이스에 저장 됨). 따라서 문자 메시지의 출력에 대 한 레이블을 추가 하 고 제출 단추를 추가 하 여 등급 양식을 서버에 다시 게시 합니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample4.aspx)]

서버 쪽 코드에서 `ID`를 통해 등급 컨트롤에 액세스 한 다음 선택 된 등급 항목의 수 인 `CurrentRating` 속성에 액세스 합니다. 예를 들어 0에서 5 사이의 값을 사용 합니다.

[!code-aspx[Main](creating-a-rating-control-vb/samples/sample5.aspx)]

페이지를 저장 하 고 브라우저에 로드 합니다. (처음에는 비어 있음) 등급 항목을 마우스로 가리키면 JavaScript 효과가 발생 합니다. 등급은 변경 됩니다. 별 집합을 클릭 하면 현재 등급은 유지 됩니다. 마지막으로 폼을 제출할 때 서버 쪽 코드는 선택한 등급을 출력 합니다.

[최소한의 코드로 등급 시스템을 만드는 ![](creating-a-rating-control-vb/_static/image2.png)](creating-a-rating-control-vb/_static/image1.png)

최소 코드로 등급 시스템 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-rating-control-vb/_static/image3.png))

> [!div class="step-by-step"]
> [이전](creating-a-rating-control-cs.md)
