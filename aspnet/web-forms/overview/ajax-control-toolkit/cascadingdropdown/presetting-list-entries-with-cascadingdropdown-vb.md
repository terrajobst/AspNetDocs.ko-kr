---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
title: CascadingDropDown를 사용 하 여 목록 항목 미리 설정 (VB) | Microsoft Docs
author: wenz
description: AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 anoth에 연결 된 값을 로드 하도록 합니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: ec61ced7-bbca-4bdd-aa3b-80878f295181
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/presetting-list-entries-with-cascadingdropdown-vb
msc.type: authoredcontent
ms.openlocfilehash: 58d675993777f9dcbe0ce1890a60046c91ee8907
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78483809"
---
# <a name="presetting-list-entries-with-cascadingdropdown-vb"></a>CascadingDropDown으로 목록 항목 미리 설정(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown2.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/CascadingDropDown2VB.pdf)

> AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다. 약간의 코드를 사용 하면 데이터가 동적으로 로드 된 후에 목록 요소가 미리 선택 될 수 있습니다.

## <a name="overview"></a>개요

AJAX 컨트롤 도구 키트의 CascadingDropDown 컨트롤은 dropdownlist 컨트롤을 확장 하 여 한 DropDownList의 변경 내용이 다른 DropDownList의 관련 값을 로드 하도록 합니다. 예를 들어, 한 목록에는 미국 주 목록이 제공 되며 다음 목록에는 해당 상태의 주 도시가 채워집니다. 약간의 코드를 사용 하면 데이터가 동적으로 로드 된 후에 목록 요소가 미리 선택 될 수 있습니다.

## <a name="steps"></a>단계

ASP.NET AJAX 및 Control Toolkit의 기능을 활성화 하려면 페이지의 아무 곳에 나 `<form>` 요소 내에 `ScriptManager` 컨트롤을 배치 해야 합니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample1.aspx)]

그런 다음, DropDownList 컨트롤이 필요 합니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample2.aspx)]

이 목록에 대해 웹 서비스 URL 및 메서드 정보를 제공 하는 CascadingDropDown extender가 추가 됩니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample3.aspx)]

그런 다음 CascadingDropDown extender는 다음 메서드 시그니처를 사용 하 여 웹 서비스를 비동기적으로 호출 합니다.

[!code-vb[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample4.vb)]

메서드는 CascadingDropDown value 형식의 배열을 반환 합니다. 형식의 생성자는 먼저 목록 항목의 캡션과 값 (HTML `value` 특성)을 먼저 예상 합니다. 세 번째 인수를 true로 설정 하면 목록 요소가 브라우저에서 자동으로 선택 됩니다.

[!code-aspx[Main](presetting-list-entries-with-cascadingdropdown-vb/samples/sample5.aspx)]

브라우저에서 페이지를 로드 하면 세 공급 업체가 세 번째로 미리 선택 된 상태로 드롭다운 목록을 채웁니다.

[목록이 채워지고 자동으로 미리 선택 된 ![](presetting-list-entries-with-cascadingdropdown-vb/_static/image2.png)](presetting-list-entries-with-cascadingdropdown-vb/_static/image1.png)

목록이 자동으로 채워지고 미리 선택 됩니다 ([전체 크기 이미지를 보려면 클릭](presetting-list-entries-with-cascadingdropdown-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](using-cascadingdropdown-with-a-database-vb.md)
> [다음](using-auto-postback-with-cascadingdropdown-vb.md)
