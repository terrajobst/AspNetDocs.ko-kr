---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: 서버 쪽에서 애니메이션 수정 (VB) | Microsoft Docs
author: wenz
description: ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 애니메이션도 ...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: ebc311d1a931ad611d9556799c94440d41a9cf49
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74575220"
---
# <a name="modifying-animations-from-the-server-side-vb"></a>서버 쪽에서 애니메이션 수정 (VB)

[Christian Wenz](https://github.com/wenz) 별

[코드 다운로드](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)

> ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 서버 쪽에서 애니메이션을 변경할 수도 있습니다.

## <a name="overview"></a>개요

ASP.NET AJAX 컨트롤 도구 키트의 애니메이션 컨트롤은 컨트롤이 아니라 컨트롤에 애니메이션을 추가 하기 위한 전체 프레임 워크입니다. 서버 쪽에서 애니메이션을 변경할 수도 있습니다.

## <a name="steps"></a>단계

먼저 페이지에 `ScriptManager`를 포함 합니다. 그런 다음 ASP.NET AJAX 라이브러리가 로드 되어 컨트롤 도구 키트를 사용할 수 있습니다.

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

애니메이션은 다음과 같은 텍스트 패널에 적용 됩니다.

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

패널의 연결 된 CSS 클래스에서 좋은 배경색을 정의 하 고 패널의 고정 폭도 설정 합니다.

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

코드의 나머지 부분은 서버 쪽에서 실행 되며 태그를 사용 하지 않습니다. 대신 코드를 사용 하 여 `AnimationExtender` 컨트롤을 만듭니다.

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

그러나 컨트롤 도구 키트는 현재 개별 애니메이션을 만들기 위한 API 액세스를 제공 하지 않습니다. 그러나 애니메이션을 선언적으로 할당할 때 사용 되는 XML 태그를 포함 하는 문자열로 `AnimationExtender`의 애니메이션 속성을 설정할 수 있습니다. `<Animations>` 요소를 포함 하지 않아야 하는 XML을 만들려면 다음 코드에서와 같이 .NET Framework의 XML 지원 또는를 사용 하 여 문자열을 제공 하면 됩니다.

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

마지막으로, `<form runat="server">` 요소 내에서 현재 페이지에 `AnimationExtender` 컨트롤을 추가 하 여 애니메이션이 포함 되 고 실행 되는지 확인 합니다.

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]

[서버 쪽 C#/vb 코드를 사용 하 여 애니메이션을 만드는 ![](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)

애니메이션은 서버 쪽 C#/vb 코드를 사용 하 여 만듭니다 ([전체 크기 이미지를 보려면 클릭](modifying-animations-from-the-server-side-vb/_static/image3.png)).

> [!div class="step-by-step"]
> [이전](triggering-an-animation-in-another-control-vb.md)
> [다음](executing-animations-using-client-side-code-vb.md)
