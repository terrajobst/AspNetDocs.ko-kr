---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
title: CascadingDropDown를 사용 하 여 목록C#채우기 () | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 anoth에 연결 된 값을 로드 하도록 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: f949aafa-fe57-43b0-b722-f0dd33a900be
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/filling-a-list-using-cascadingdropdown-cs
msc.type: authoredcontent
ms.openlocfilehash: b5e9874fb5b6d3e55c8af5b85d12bf1ffacc116b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74574835"
---
# <a name="filling-a-list-using-cascadingdropdown-c"></a>CascadingDropDown을 사용하여 목록 채우기(C#)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown0.cs.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown0CS.pdf)

> AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다. 예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 가장 먼저 해결 해야 하는 문제는이 컨트롤을 사용 하 여 드롭다운 목록을 실제로 채우는 것입니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다. 예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 가장 먼저 해결 해야 하는 문제는이 컨트롤을 사용 하 여 드롭다운 목록을 실제로 채우는 것입니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample1.aspx)]

그런 다음, DropDownList 컨트롤이 필요 합니다.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample2.aspx)]

이 목록에는 CascadingDropDown extender가 추가 됩니다. 웹 서비스에 대 한 비동기 요청을 보냅니다. 그러면 목록에 표시 될 항목의 목록이 반환 됩니다. 이 작업을 수행 하려면 다음 CascadingDropDown 특성을 설정 해야 합니다.

- `ServicePath`: 목록 항목을 제공 하는 웹 서비스의 URL
- `ServiceMethod`: 목록 항목을 전달 하는 웹 메서드
- `TargetControlID`: 드롭다운 목록의 ID
- `Category`: 호출 시 웹 메서드에 제출 되는 범주 정보
- `PromptText`: 서버에서 목록 데이터를 비동기적으로 로드할 때 표시 되는 텍스트입니다.

`CascadingDropDown` 요소에 대 한 태그는 다음과 같습니다. C# 와 VB의 유일한 차이점은 연결 된 웹 서비스의 이름입니다.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample3.aspx)]

`CascadingDropDown` extender에서 들어오는 JavaScript 코드는 다음 서명을 사용 하 여 웹 서비스 메서드를 호출 합니다.

[!code-csharp[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample4.cs)]

따라서 중요 한 점은 메서드가 `CascadingDropDownNameValue` 형식의 배열을 반환 해야 한다는 것입니다 (ASP.NET AJAX 컨트롤 Toolkit에 정의 됨). `CascadingDropDownNameValue` 생성자에서 목록 항목의 텍스트를 먼저 입력 한 다음 HTML로 `<option value="VALUE">NAME</option>` 하는 것과 마찬가지로 해당 값을 제공 해야 합니다. 다음은 몇 가지 샘플 데이터입니다.

[!code-aspx[Main](filling-a-list-using-cascadingdropdown-cs/samples/sample5.aspx)]

브라우저에서 페이지를 로드 하면 3 개의 공급 업체가 채워질 목록이 트리거됩니다.

[목록이 자동으로 채워질 ![](filling-a-list-using-cascadingdropdown-cs/_static/image2.png)](filling-a-list-using-cascadingdropdown-cs/_static/image1.png)

목록이 자동으로 채워집니다 ([전체 크기 이미지를 보려면 클릭](filling-a-list-using-cascadingdropdown-cs/_static/image3.png)).

> [!div class="step-by-step"]
> [다음](using-cascadingdropdown-with-a-database-cs.md)
