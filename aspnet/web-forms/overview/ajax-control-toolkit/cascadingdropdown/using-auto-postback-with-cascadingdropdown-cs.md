---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
title: CascadingDropDown (C#)에서 자동 포스트백 사용 Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 anoth에 연결 된 값을 로드 하도록 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 6755d8d9-14be-4a1d-86e5-1a6110f3dea8
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-auto-postback-with-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: 8bccd716814e7de544798010cecbc148ec50b5cd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574519"
---
# <a name="using-auto-postback-with-cascadingdropdown-c"></a>CascadingDropDown으로 자동 포스트백 사용(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown3.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown3CS.pdf)

> AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다. 그러나 CascadingDropDown 컨트롤을 사용 하는 경우 ASP. 데이터를 목록에 비동기적으로 로드 하면 (불필요 한) 포스트백이 생성 되므로 NET의 DropDownList 컨트롤의 AutoPostBack 기능이 작동 하지 않습니다. 일부 JavaScript 코드를 사용 하면이 효과를 피할 수 있습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다. 예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 그러나 CascadingDropDown 컨트롤을 사용 하는 경우 ASP. 데이터를 목록에 비동기적으로 로드 하면 (불필요 한) 포스트백이 생성 되므로 NET의 DropDownList 컨트롤의 AutoPostBack 기능이 작동 하지 않습니다. 일부 JavaScript 코드를 사용 하면이 효과를 피할 수 있습니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `ScriptManager` 컨트롤을 배치 해야 합니다 (&lt;`form`&gt; 요소 내).

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample1.aspx)]

그런 다음, DropDownList 컨트롤이 필요 합니다.

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample2.aspx)]

이 목록에 대해 웹 서비스 URL 및 메서드 정보를 제공 하는 CascadingDropDown extender가 추가 됩니다.

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample3.aspx)]

그런 다음 CascadingDropDown extender는 다음 메서드 시그니처를 사용 하 여 웹 서비스를 비동기적으로 호출 합니다.

[!code-csharp[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample4.cs)]

메서드는 CascadingDropDown value 형식의 배열을 반환 합니다. 형식의 생성자는 먼저 목록 항목의 캡션과 값 (HTML `value` 특성)을 먼저 예상 합니다.

[!code-aspx[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample5.aspx)]

브라우저에서 페이지를 로드 하면 세 공급 업체가 세 번째로 미리 선택 된 상태로 드롭다운 목록을 채웁니다. 또한 ASP.NET는 `__doPostBack()` JavaScript 메서드를 정의 합니다. 페이지가 로드 되 면이 JavaScript 호출은 드롭다운 목록에 추가 되지만 여기에는 요소가 있는 경우에만 추가 됩니다. 목록에 요소가 없으면 컨트롤 도구 키트가 현재 로드 하 고 있으므로 JavaScript 코드는 시간 제한을 사용 하 고 0.5 초 후에 다시 시도 합니다.

[!code-html[Main](using-auto-postback-with-cascadingdropdown-cs/samples/sample6.html)]

이러한 방식으로, 목록에 실제로 요소가 있고 사용자가 항목을 선택 하는 경우에만 포스트백이 실행 됩니다.

[목록 요소를 선택 ![포스트백이 발생 합니다.](using-auto-postback-with-cascadingdropdown-cs/_static/image2.png)](using-auto-postback-with-cascadingdropdown-cs/_static/image1.png)

목록 요소를 선택 하면 포스트백이 발생 합니다 ([전체 크기 이미지를 보려면 클릭](using-auto-postback-with-cascadingdropdown-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](presetting-list-entries-with-cascadingdropdown-cs.md)
> [다음](filling-a-list-using-cascadingdropdown-vb.md)
