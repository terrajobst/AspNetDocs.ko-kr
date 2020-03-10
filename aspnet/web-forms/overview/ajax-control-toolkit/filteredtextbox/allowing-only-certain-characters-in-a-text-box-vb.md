---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: 텍스트 상자에 특정 문자만 허용 (VB) | Microsoft Docs
author: wenz
description: ASP.NET 유효성 검사 컨트롤을 사용 하면 사용자 입력에 특정 문자만 허용 되도록 할 수 있습니다. 그러나이 경우 사용자가 잘못 된 형식을 입력 하는 것을 방지할 수 없습니다.
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 895708ebecc30c5f35e6ecd0349604bb777cbd93
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78497165"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a>텍스트 상자에 특정 문자만 허용(VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)

> ASP.NET 유효성 검사 컨트롤을 사용 하면 사용자 입력에 특정 문자만 허용 되도록 할 수 있습니다. 그러나이 경우에도 사용자는 잘못 된 문자를 입력 하 고 양식을 전송 하는 것을 방지할 수 없습니다.

## <a name="overview"></a>개요

ASP.NET 유효성 검사 컨트롤을 사용 하면 사용자 입력에 특정 문자만 허용 되도록 할 수 있습니다. 그러나이 경우에도 사용자는 잘못 된 문자를 입력 하 고 양식을 전송 하는 것을 방지할 수 없습니다.

## <a name="steps"></a>단계

ASP.NET AJAX 컨트롤 도구 키트는 텍스트 상자를 확장 하는 `FilteredTextBox` 컨트롤을 포함 합니다. 활성화 된 후에는 특정 문자 집합만 필드에 입력할 수 있습니다.

이 작업을 수행 하려면 먼저 ASP.NET AJAX 컨트롤 Toolkit 에서도 사용 되는 JavaScript 라이브러리를 로드 하는 ASP.NET AJAX `ScriptManager` 일반적으로 필요 합니다.

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

그런 다음 텍스트 상자가 필요 합니다.

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

마지막으로, `FilteredTextBoxExtender` 컨트롤은 사용자가 입력할 수 있는 문자를 제한 합니다. 먼저 `TargetControlID` 특성을 `TextBox` 컨트롤의 `ID` 설정 합니다. 그런 다음 사용 가능한 `FilterType` 값 중 하나를 선택 합니다.

- `Custom` 기본값 유효한 문자 목록을 제공 해야 합니다.
- `LowercaseLetters` 소문자만
- `Numbers` 숫자만
- 대문자 `UppercaseLetters`

`Custom FilterType`를 사용 하는 경우 `ValidChars` 속성을 설정 하 고 입력 될 수 있는 문자 목록을 제공 해야 합니다. 텍스트 상자에 텍스트를 붙여 넣으려고 하면 잘못 된 모든 문자가 제거 됩니다.

숫자만 허용 하는 `FilteredTextBoxExtender` 컨트롤에 대 한 태그는 다음과 같습니다 (`FilterType="Numbers"`에서도 가능한 항목).

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

페이지를 실행 하 고 JavaScript를 사용 하는 경우 문자를 입력 하 여 작업을 수행 하지 않습니다. 그러나 숫자는 페이지에 표시 됩니다. 그러나 제공 되는 보호 `FilteredTextBox`는 글머리 기호가 아닙니다. JavaScript를 사용 하는 경우 텍스트 상자에 데이터를 입력할 수 있으므로 추가 유효성 검사 (예: ASP)를 사용 해야 합니다. NET의 유효성 검사 컨트롤입니다.

[![숫자만 입력할 수 있습니다.](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)

숫자만 입력할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](allowing-only-certain-characters-in-a-text-box-cs.md)
