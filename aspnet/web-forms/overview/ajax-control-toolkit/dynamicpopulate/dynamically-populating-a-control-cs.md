---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
title: 동적으로 컨트롤 채우기 (C#) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 결과 값을 t ...의 대상 컨트롤로 채웁니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: e1fec43e-1daf-49d2-b0c7-7f1b930455cc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/dynamically-populating-a-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 24f88e44e0f878127314774d4e8846f80133413e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599281"
---
# <a name="dynamically-populating-a-control-c"></a>동적으로 컨트롤 채우기(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate0.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate0CS.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 `DynamicPopulate` 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다. 이 자습서에서는이를 설정 하는 방법을 보여 줍니다.

## <a name="steps"></a>단계

먼저 `DynamicPopulate`에 의해 호출 되는 메서드를 구현 하는 ASP.NET 웹 서비스가 필요 합니다. 웹 서비스 클래스에는 `Microsoft.Web.Script.Services`내에 정의 된 `ScriptService` 특성이 필요 합니다. 그렇지 않으면 ASP.NET AJAX는 웹 서비스에 대 한 클라이언트 쪽 JavaScript 프록시를 만들 수 없으며,이 프록시는 `DynamicPopulate`에 필요 합니다.

`DynamicPopulate` 컨트롤은 각 웹 서비스 호출을 사용 하 여 하나의 컨텍스트 정보를 보내기 때문에 웹 메서드는 `contextKey`라는 문자열 형식의 인수를 하나 이상 사용 해야 합니다. 다음 웹 서비스는 `contextKey` 인수로 표시 되는 형식으로 현재 날짜를 반환 합니다.

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample1.aspx)]

그런 다음 웹 서비스는 `DynamicPopulate.cs.asmx`로 저장 됩니다. 또는 `DynamicPopulate` 컨트롤을 사용 하 여 실제 ASP.NET 페이지 내에서 `getDate()` 메서드를 페이지 메서드로 구현할 수 있습니다.

다음 단계에서 새 ASP.NET 파일을 만듭니다. 항상 첫 번째 단계는 현재 페이지에 `ScriptManager`를 포함 하 여 ASP.NET AJAX 라이브러리를 로드 하 고 컨트롤 도구 키트의 작업을 수행 하는 것입니다.

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample2.aspx)]

그런 다음 나중에 웹 서비스 호출의 결과를 표시 하는 동일한 이름의 HTML 컨트롤이 나 &gt; 웹 컨트롤  /`asp:Label`&lt;을 사용 하 여 레이블 컨트롤을 추가 합니다.

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample3.aspx)]

HTML 단추 (서버에 대 한 포스트백을 요구 하지 않으므로 HTML 컨트롤)는 동적 채우기를 트리거하는 데 사용 됩니다.

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample4.aspx)]

마지막으로, 항목을 연결 하는 `DynamicPopulateExtender` 컨트롤이 필요 합니다. 다음 특성이 설정 됩니다 (분명 한 것은 `ID`, `runat`=`"server"`).

- 웹 서비스 호출에서 결과를 넣을 위치를 `TargetControlID` 합니다.
- 웹 서비스의 `ServicePath` 경로 (페이지 메서드를 사용 하려는 경우 생략)
- 웹 메서드 또는 페이지 메서드의 `ServiceMethod` 이름
- 웹 서비스로 보낼 컨텍스트 정보를 `ContextKey` 합니다.
- 웹 서비스 호출을 트리거하는 `PopulateTriggerControlID` 요소
- 웹 서비스 호출 중에 대상 요소를 비울 지 여부를 `ClearContentsDuringUpdate` 합니다.

여기에서 볼 수 있듯이, 컨트롤에는 일부 정보가 필요 하지만 모든 항목을 제자리에 배치 하는 것은 매우 간단 합니다. 현재 시나리오의 `DynamicPopulateExtender` 컨트롤에 대 한 태그는 다음과 같습니다.

[!code-aspx[Main](dynamically-populating-a-control-cs/samples/sample5.aspx)]

브라우저에서 ASP.NET 페이지를 실행 하 고 단추를 클릭 합니다. 월-일-연도 형식으로 현재 날짜를 받게 됩니다.

[![단추를 클릭 하면 서버에서 날짜가 검색 됩니다.](dynamically-populating-a-control-cs/_static/image2.png)](dynamically-populating-a-control-cs/_static/image1.png)

단추를 클릭 하면 서버에서 날짜가 검색 됩니다 ([전체 크기 이미지를 보려면 클릭](dynamically-populating-a-control-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [다음](dynamically-populating-a-control-using-javascript-code-cs.md)
