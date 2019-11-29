---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
title: JavaScript 코드를 사용 하 여 동적으로 컨트롤 채우기 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 결과 값을 t ...의 대상 컨트롤로 채웁니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 90582e54-3e90-432a-9da5-689fb39ed56b
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-using-javascript-code-vb
msc.type: authoredcontent
ms.openlocfilehash: b2bd5b1571ccebc9baa501b29743aecdb4543fb2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599213"
---
# <a name="dynamically-populating-a-control-using-javascript-code-vb"></a>JavaScript 코드를 사용하여 동적으로 컨트롤 채우기(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate1.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate1VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수도 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 `DynamicPopulate` 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수도 있습니다.

## <a name="steps"></a>단계

먼저 `DynamicPopulateExtender` 컨트롤에 의해 호출 되는 메서드를 구현 하는 ASP.NET 웹 서비스가 필요 합니다. `DynamicPopulate` 컨트롤이 각 웹 서비스 호출을 사용 하 여 하나의 컨텍스트 정보를 보내기 때문에 웹 서비스는 `contextKey`라는 문자열 형식의 인수 하나를 예상 하는 `getDate()` 메서드를 구현 합니다. 다음은 세 가지 형식 중 하나로 현재 날짜를 검색 하는 코드 (파일 `DynamicPopulate.vb.asmx`)입니다.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample1.aspx)]

다음 단계에서는 새 ASP.NET 사이트를 만들고 ASP.NET AJAX ScriptManager 컨트롤을 사용 하 여 시작 합니다.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample2.aspx)]

그런 다음 나중에 웹 서비스 호출의 결과를 표시 하는 동일한 이름의 HTML 컨트롤이 나 `<asp:Label />` 웹 컨트롤을 사용 하 여 레이블 컨트롤을 추가 합니다.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample3.aspx)]

그런 다음 `DynamicPopulateExtender` 컨트롤을 포함 하 고 웹 서비스 정보, 대상 제어를 제공 하지만, 채우기를 트리거하는 컨트롤의 이름은 나중에 사용자 지정 JavaScript를 사용 하 여 수행 됩니다.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample4.aspx)]

이제 JavaScript 파트로 돌아갑니다. ASP.NET AJAX 라이브러리에 의해 정의 되는 `$find()` 함수는 `DynamicPopulateExtender`와 같은 ASP.NET AJAX 컨트롤 도구 키트의 서버 쪽 개체에 대 한 참조를 반환 합니다. 현재 파일에서 `$find("dpe")`는 페이지의 한 `DynamicPopulateExtender` 컨트롤에 대 한 참조를 반환 합니다. 동적 채우기 프로세스를 트리거하는 `populate()` 이라는 메서드를 노출 합니다. `populate()` 메서드는 하나의 인수를 사용 해야 합니다. 컨텍스트 키는 `getDate()` 웹 메서드에 대 한 인수로 사용 됩니다. 예를 들어 `$find("dpe").populate("format1")`는 레이블을 월-일-연도 형식의 현재 날짜로 채웁니다.

예제를 좀 더 유연 하 게 만들기 위해 이제 사용자가 여러 날짜 형식 중에서 선택할 수 있습니다. 이러한 각 항목에 대해 라디오 단추가 표시 됩니다. 사용자가 라디오 단추를 클릭 하면 JavaScript 코드가 자동으로 레이블을 선택한 날짜 형식으로 채웁니다. 해당 라디오 단추는 다음과 같습니다.

[!code-aspx[Main](dynamically-populating-a-control-using-javascript-code-vb/samples/sample5.aspx)]

라디오 단추의 컨텍스트 내에서 JavaScript 식 `this.value`는 현재 단추의 값을 참조 하며,이 값은 `getDate()` 메서드가 사용할 수 있는 것과 정확히 동일한 정보를 사용 합니다.

[![단추를 클릭 하면 지정 된 형식으로 서버에서 날짜를 검색 합니다.](dynamically-populating-a-control-using-javascript-code-vb/_static/image2.png)](dynamically-populating-a-control-using-javascript-code-vb/_static/image1.png)

단추를 클릭 하면 서버에서 지정 된 형식으로 날짜가 검색 됩니다 ([전체 크기 이미지를 보려면 클릭](dynamically-populating-a-control-using-javascript-code-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](dynamically-populating-a-control-vb.md)
> [다음](using-dynamicpopulate-with-a-user-control-and-javascript-vb.md)
