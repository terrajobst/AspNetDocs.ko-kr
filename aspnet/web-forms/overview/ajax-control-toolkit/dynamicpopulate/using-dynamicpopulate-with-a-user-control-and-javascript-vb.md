---
uid: web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
title: 사용자 컨트롤 및 JavaScript에서 DynamicPopulate 사용 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 결과 값을 t ...의 대상 컨트롤로 채웁니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 778b9009-76f2-4665-940e-afc0e35bc917
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/dynamicpopulate/using-dynamicpopulate-with-a-user-control-and-javascript-vb
msc.type: authoredcontent
ms.openlocfilehash: ee5923ad6d8b101f689a0564aef8b1e0e00a7639
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497303"
---
# <a name="using-dynamicpopulate-with-a-user-control-and-javascript-vb"></a>사용자 정의 컨트롤 및 JavaScript에 DynamicPopulate 사용(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/d/8/f/d8f2f6f9-1b7c-46ad-9252-e1fc81bdea3e/dynamicpopulate2.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/dynamicpopulate2VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 DynamicPopulate 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수도 있습니다. 그러나 extender가 사용자 정의 컨트롤에 있는 경우 특별 한 주의를 기울여야 합니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 `DynamicPopulate` 컨트롤은 웹 서비스 (또는 페이지 메서드)를 호출 하 고 페이지를 새로 고치지 않고 결과 값을 페이지의 대상 컨트롤로 채웁니다. 사용자 지정 클라이언트 쪽 JavaScript 코드를 사용 하 여 채우기를 트리거할 수도 있습니다. 그러나 extender가 사용자 정의 컨트롤에 있는 경우 특별 한 주의를 기울여야 합니다.

## <a name="steps"></a>단계

먼저 `DynamicPopulateExtender` 컨트롤에 의해 호출 되는 메서드를 구현 하는 ASP.NET 웹 서비스가 필요 합니다. `DynamicPopulate` 컨트롤이 각 웹 서비스 호출을 사용 하 여 하나의 컨텍스트 정보를 보내기 때문에 웹 서비스는 `contextKey`라는 문자열 형식의 인수 하나를 예상 하는 `getDate()` 메서드를 구현 합니다. 다음은 세 가지 형식 중 하나로 현재 날짜를 검색 하는 코드 (파일 `DynamicPopulate.vb.asmx`)입니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample1.aspx)]

다음 단계에서 첫 번째 줄에서 다음 선언으로 표시 되는 새 사용자 정의 컨트롤 (`.ascx` 파일)을 만듭니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample2.aspx)]

&lt;`label`&gt; 요소는 서버에서 들어오는 데이터를 표시 하는 데 사용 됩니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample3.aspx)]

또한 사용자 정의 컨트롤 파일에는 웹 서비스에서 지 원하는 세 가지 날짜 형식 중 하나를 나타내는 세 개의 라디오 단추가 사용 됩니다. 사용자가 라디오 단추 중 하나를 클릭 하면 브라우저에서 다음과 같은 JavaScript 코드를 실행 합니다.

[!code-powershell[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample4.ps1)]

이 코드는 `DynamicPopulateExtender`에 액세스 합니다 (이상한 ID에 대해서는 걱정할 필요가 없으며,이 내용은 나중에 설명 됨), 데이터를 사용 하 여 동적 채우기를 트리거합니다. 현재 라디오 단추의 컨텍스트에서 `this.value`는 `format1`, `format2` 또는 `format3` 웹 메서드에 필요한 것과 같은 값을 나타냅니다.

사용자 정의 컨트롤에서 아직 누락 된 것은 웹 서비스에 라디오 단추를 연결 하는 `DynamicPopulateExtender` 컨트롤입니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample5.aspx)]

이 경우에도 컨트롤에서 사용 되는 이상한 ID를 `myDate`대신 `mcd1$myDate` 합니다. 이전에는 JavaScript 코드를 사용 하 여 `dpe1`대신 `DynamicPopulateExtender`에 액세스 `mcd1_dpe1` 했습니다. 이 명명 전략은 사용자 정의 컨트롤 내에서 `DynamicPopulateExtender`를 사용할 때 특별 한 요구 사항입니다. 또한 모든 작업을 수행 하기 위해 특정 방법으로 사용자 정의 컨트롤을 포함 해야 합니다. 새 ASP.NET 페이지를 만들고 방금 구현한 사용자 정의 컨트롤에 대 한 태그 접두사를 등록 합니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample6.aspx)]

그런 다음 새 페이지에 ASP.NET AJAX `ScriptManager` 컨트롤을 포함 합니다.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample7.aspx)]

마지막으로 페이지에 사용자 정의 컨트롤을 추가 합니다. `ID` 특성 (및 `runat="server"`)만 설정 해야 하지만,이를 특정 이름으로 설정 해야 합니다 .이는 JavaScript를 사용 하 여 액세스 하기 위해 사용자 정의 컨트롤 내에서 사용 되는 접두사 이므로 `mcd1`.

[!code-aspx[Main](using-dynamicpopulate-with-a-user-control-and-javascript-vb/samples/sample8.aspx)]

이것으로 끝입니다! 페이지가 예상 대로 동작 합니다. 사용자가 라디오 단추 중 하나를 클릭 하면 도구 키트의 컨트롤이 웹 서비스를 호출 하 고 원하는 형식으로 현재 날짜를 표시 합니다.

[사용자 정의 컨트롤에 있는 라디오 단추 ![](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image2.png)](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image1.png)

라디오 단추는 사용자 정의 컨트롤에 있습니다 ([전체 크기 이미지를 보려면 클릭](using-dynamicpopulate-with-a-user-control-and-javascript-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](dynamically-populating-a-control-using-javascript-code-vb.md)
