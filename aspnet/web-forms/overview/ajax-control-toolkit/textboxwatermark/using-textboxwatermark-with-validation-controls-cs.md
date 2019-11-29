---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
title: 유효성 검사 컨트롤에 TextBoxWatermark 사용C#() | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 TextBoxWatermark 컨트롤은 입력란 내에 텍스트가 표시 되도록 텍스트 상자를 확장 합니다. 사용자가 상자를 클릭 하면 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: d49940cb-d38c-456a-b800-5f0eb705d09f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-with-validation-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: bc9498b1c5ba2f38b90706c9200ffa813a945fa9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74610898"
---
# <a name="using-textboxwatermark-with-validation-controls-c"></a>유효성 검사 컨트롤에 TextBoxWatermark 사용(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark2.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark2CS.pdf)

> AJAX 컨트롤 도구 키트의 TextBoxWatermark 컨트롤은 입력란 내에 텍스트가 표시 되도록 텍스트 상자를 확장 합니다. 사용자가 상자를 클릭 하면 해당 상자가 비워집니다. 사용자가 텍스트를 입력 하지 않고 상자를 벗어나면 미리 채워진 텍스트가 다시 나타납니다. 이는 동일한 페이지에서 ASP.NET 유효성 검사 컨트롤과 충돌할 수 있지만 이러한 문제를 해결할 수 있습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 `TextBoxWatermark` 컨트롤은 입력란 내에 텍스트가 표시 되도록 텍스트 상자를 확장 합니다. 사용자가 상자를 클릭 하면 해당 상자가 비워집니다. 사용자가 텍스트를 입력 하지 않고 상자를 벗어나면 미리 채워진 텍스트가 다시 나타납니다. 이는 동일한 페이지에서 ASP.NET 유효성 검사 컨트롤과 충돌할 수 있지만 이러한 문제를 해결할 수 있습니다.

## <a name="steps"></a>단계

샘플의 기본 설정은 다음과 같습니다. `TextBox` 컨트롤은 `TextBoxWatermarkExtender` 컨트롤을 사용 하 여 워터 마크 됩니다. 단추는 포스트백을 트리거하고 나중에 페이지에서 유효성 검사 컨트롤을 트리거하는 데 사용 됩니다. 또한 ASP.NET AJAX를 초기화 하려면 `ScriptManager` 컨트롤이 필요 합니다.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample1.aspx)]

이제 양식이 전송 될 때 필드에 텍스트가 있는지 여부를 확인 하는 `RequiredFieldValidator` 컨트롤을 추가 합니다. 유효성 검사기의 `InitialValue` 속성은 `TextBoxWatermarkExtender` 컨트롤에 사용 되는 것과 동일한 값으로 설정 해야 합니다. 폼이 제출 될 때 변경 되지 않은 텍스트 상자의 값은 그 안에 있는 워터 마크 값입니다.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample2.aspx)]

그러나이 방법에는 한 가지 문제가 있습니다. 클라이언트가 JavaScript를 사용 하지 않도록 설정 하는 경우 텍스트 필드가 워터 마크 텍스트로 미리 채워지지 않으므로 `RequiredFieldValidator`는 오류 메시지를 트리거하지 않습니다. 따라서 `InitialValue` 특성을 생략 하 고 빈 텍스트 상자를 확인 하는 두 번째 `RequiredFieldValidator` 컨트롤이 필요 합니다.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample3.aspx)]

두 유효성 검사기는 `Display`=`"Dynamic"`를 사용 하므로 최종 사용자는 두 가지 유효성 검사기의 시각적 모양을 구별할 수 없습니다. 그 중 하나만 있는 것 같습니다.

마지막으로, 유효성 검사기에서 오류 메시지를 발행 하지 않은 경우 필드의 텍스트를 출력 하는 서버 쪽 코드를 추가 합니다.

[!code-aspx[Main](using-textboxwatermark-with-validation-controls-cs/samples/sample4.aspx)]

[필드에 텍스트가 불만 유효성 검사기를 ![합니다.](using-textboxwatermark-with-validation-controls-cs/_static/image2.png)](using-textboxwatermark-with-validation-controls-cs/_static/image1.png)

유효성 검사기에서 필드에 텍스트가 불만 ([전체 크기 이미지를 보려면 클릭](using-textboxwatermark-with-validation-controls-cs/_static/image3.png))

> [!div class="step-by-step"]
> [이전](using-textboxwatermark-in-a-formview-cs.md)
> [다음](using-textboxwatermark-in-a-formview-vb.md)
