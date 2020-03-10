---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: JavaScript 삽입 공격 방지 (VB) | Microsoft Docs
author: StephenWalther
description: JavaScript 삽입 공격 및 사이트 간 스크립팅 공격이 발생 하지 않도록 합니다. 이 자습서에서 Stephen Walther는 쉽게 제거할 수 있는 방법을 설명 합니다.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: dfe09085f26c62c566649bc6f570aa25367a0f07
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506225"
---
# <a name="preventing-javascript-injection-attacks-vb"></a>JavaScript 삽입 공격 방지(VB)

[Stephen Walther](https://github.com/StephenWalther)

[PDF 다운로드](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> JavaScript 삽입 공격 및 사이트 간 스크립팅 공격이 발생 하지 않도록 합니다. 이 자습서에서 Stephen Walther는 콘텐츠를 HTML 인코딩하여 이러한 유형의 공격을 쉽게 방지할 수 있는 방법에 대해 설명 합니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 JavaScript 삽입 공격을 방지 하는 방법을 설명 하는 것입니다. 이 자습서에서는 JavaScript 삽입 공격 으로부터 웹 사이트를 방어 하는 두 가지 방법을 설명 합니다. 표시 되는 데이터를 인코딩하여 JavaScript 삽입 공격을 방지 하는 방법에 대해 알아봅니다. 또한 사용자가 수락한 데이터를 인코딩하여 JavaScript 삽입 공격을 방지 하는 방법을 알아봅니다.

## <a name="what-is-a-javascript-injection-attack"></a>JavaScript 삽입 공격 이란?

사용자 입력을 수락 하 고 사용자 입력을 다시 표시할 때마다 JavaScript 삽입 공격에 대해 웹 사이트를 엽니다. JavaScript 삽입 공격에 공개 된 구체적인 응용 프로그램을 살펴보겠습니다.

사용자 의견 웹 사이트를 만들었다고 가정 합니다 (그림 1 참조). 고객은 웹 사이트를 방문 하 여 제품 사용 경험에 대 한 피드백을 입력할 수 있습니다. 고객이 피드백을 제출 하면 피드백 페이지에 피드백이 표시 됩니다.

[사용자 의견 웹 사이트 ![](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)

**그림 01**: 사용자 의견 웹 사이트 ([전체 크기 이미지를 보려면 클릭](preventing-javascript-injection-attacks-vb/_static/image3.png))

사용자 의견 웹 사이트는 목록 1에 `controller`를 사용 합니다. 이 `controller`에는 `Index()` 및 `Create()`라는 두 개의 작업이 포함 되어 있습니다.

**목록 1 – `HomeController.vb`**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

`Index()` 메서드는 `Index` 뷰를 표시 합니다. 이 메서드는 LINQ to SQL 쿼리를 사용 하 여 데이터베이스에서 피드백을 검색 하 여 모든 이전 사용자 의견을 `Index` 보기에 전달 합니다.

`Create()` 메서드는 새 피드백 항목을 만들어 데이터베이스에 추가 합니다. 고객이 양식에 입력 하는 메시지는 메시지 매개 변수에서 `Create()` 메서드에 전달 됩니다. 피드백 항목이 만들어지고 메시지가 피드백 항목의 `Message` 속성에 할당 됩니다. 사용자 의견 항목이 `DataContext.SubmitChanges()` 메서드 호출로 데이터베이스에 전송 됩니다. 마지막으로 방문자는 모든 피드백이 표시 되는 `Index` 보기로 다시 리디렉션됩니다.

`Index` 보기는 목록 2에 포함 되어 있습니다.

**목록 2 – `Index.aspx`**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

`Index` 보기에는 두 개의 섹션이 있습니다. 위쪽 섹션에는 실제 사용자 의견 양식이 포함 되어 있습니다. 아래쪽 섹션에는에 대 한이 포함 되어 있습니다. 모든 이전 사용자 의견 항목을 반복 하 고 각 피드백 항목의 EntryDate 및 Message 속성을 표시 하는 각 루프

사용자 의견 웹 사이트는 간단한 웹 사이트입니다. 불행 하 게도 웹 사이트는 JavaScript 삽입 공격에 공개 됩니다.

사용자 의견 양식에 다음 텍스트를 입력 한다고 가정 합니다.

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

이 텍스트는 경고 메시지 상자를 표시 하는 JavaScript 스크립트를 나타냅니다. 사용자가이 스크립트를 사용자 의견 양식에 제출한 후 메시지는 <em>Boo!</em> 나중에 누구나 고객 피드백 웹 사이트를 방문할 때마다 표시 됩니다 (그림 2 참조).

[JavaScript 삽입 ![](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)

**그림 02**: JavaScript 삽입 ([전체 크기 이미지를 보려면 클릭](preventing-javascript-injection-attacks-vb/_static/image6.png))

이제 JavaScript 삽입 공격에 대 한 초기 응답이 apathy 될 수 있습니다. JavaScript 삽입 공격은 단순히 *파손* 공격의 유형 이라고 생각할 수 있습니다. JavaScript 삽입 공격을 커밋하여 어떤 것도 진정한 영향을 주지 않는 것으로 생각할 수 있습니다.

불행 하 게도 해커는 JavaScript를 웹 사이트에 삽입 하 여 정말 나쁜 작업을 수행할 수 있습니다. JavaScript 삽입 공격을 사용 하 여 XSS (사이트 간 스크립팅) 공격을 수행할 수 있습니다. 사이트 간 스크립팅 공격에서는 기밀 사용자 정보를 도용 하 고 다른 웹 사이트로 정보를 보냅니다.

예를 들어 해커가 JavaScript 삽입 공격을 사용 하 여 다른 사용자의 브라우저 쿠키 값을 도용할 수 있습니다. 암호, 신용 카드 번호 또는 주민 등록 번호와 같은 중요 한 정보가 브라우저 쿠키에 저장 된 경우 해커가 JavaScript 삽입 공격을 사용 하 여이 정보를 도용할 수 있습니다. 또는 JavaScript 공격으로 손상 된 페이지에 포함 된 양식 필드에 중요 한 정보를 입력 하는 경우 해커가 삽입 된 JavaScript를 사용 하 여 양식 데이터를 가져와서 다른 웹 사이트로 보낼 수 있습니다.

*무서 워 하세요*. JavaScript 주입 공격을 심각 하 게 수행 하 고 사용자의 기밀 정보를 보호 합니다. 다음 두 섹션에서는 JavaScript 삽입 공격 으로부터 ASP.NET MVC 응용 프로그램을 보호 하는 데 사용할 수 있는 두 가지 방법을 설명 합니다.

## <a name="approach-1-html-encode-in-the-view"></a>#1 방식: 뷰에서 HTML 인코드

JavaScript 삽입 공격을 방지 하는 한 가지 쉬운 방법은 뷰에서 데이터를 다시 표시할 때 웹 사이트 사용자가 입력 한 데이터를 HTML 인코딩하는 것입니다. 목록 3의 업데이트 된 `Index` 보기는이 접근 방식을 따릅니다.

**목록 3 – `Index.aspx` (HTML 인코딩)**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

값이 다음 코드와 함께 표시 되기 전에 `feedback.Message` 값이 HTML로 인코딩됩니다.

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

HTML 인코딩 이란 무엇을 의미 하나요? 문자열을 HTML로 인코딩하면 `<` 및 `>`와 같은 위험한 문자가 `&lt;` 및 `&gt;`같은 HTML 엔터티 참조로 바뀝니다. 따라서 `<script>alert("Boo!")</script>` 문자열을 HTML로 인코딩하면 `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`으로 변환 됩니다. 인코딩된 문자열은 브라우저에서 해석 될 때 더 이상 JavaScript 스크립트로 실행 되지 않습니다. 대신 그림 3의 무해 한 페이지가 표시 됩니다.

[![JavaScript 공격 공격](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)

**그림 03**: JavaScript 공격 거부 ([전체 크기 이미지를 보려면 클릭](preventing-javascript-injection-attacks-vb/_static/image9.png))

목록 3의 `Index` 뷰에서는 `feedback.Message` 값만 인코딩됩니다. `feedback.EntryDate`의 값은 인코딩되지 않습니다. 사용자가 입력 한 데이터만 인코딩해야 합니다. EntryDate의 값이 컨트롤러에서 생성 되었기 때문에이 값을 HTML로 인코딩할 필요가 없습니다.

## <a name="approach-2-html-encode-in-the-controller"></a>방법 #2: 컨트롤러에서 HTML 인코드

데이터를 뷰에 표시할 때 HTML 인코딩 데이터 대신 데이터를 데이터베이스로 전송 하기 바로 전에 데이터를 HTML로 인코딩할 수 있습니다. 이 두 번째 방법은 목록 4의 `controller` 경우에 적용 됩니다.

**목록 4 – `HomeController.cs` (HTML 인코딩)**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

메시지의 값이 `Create()` 작업 내에서 데이터베이스로 전송 되기 전에 HTML로 인코딩됩니다. 메시지가 뷰에서 다시 표시 되 면 메시지는 HTML로 인코딩되고 메시지에 삽입 된 모든 JavaScript는 실행 되지 않습니다.

일반적으로이 자습서에서 설명 하는 첫 번째 방법에는이 두 번째 방법을 사용 하는 것이 좋습니다. 이 두 번째 방법의 문제는 데이터베이스에서 HTML로 인코딩된 데이터를 종료 하는 것입니다. 즉, 데이터베이스 데이터는 재미 있는 문자를 사용 하 여 변경 된 됩니다.

이것이 왜 바람직하지 않나요? 웹 페이지가 아닌 다른 항목에 데이터베이스 데이터를 표시 해야 하는 경우에는 문제가 발생 합니다. 예를 들어 Windows Forms 응용 프로그램에서 더 이상 데이터를 더 이상 표시 하지 않을 수 있습니다.

## <a name="summary"></a>요약

이 자습서의 목적은 JavaScript 삽입 공격의 잠재 고객을 부담 하는 것 이었습니다. 이 자습서에서는 JavaScript 삽입 공격 으로부터 ASP.NET MVC 응용 프로그램을 보호 하는 두 가지 방법에 대해 설명 했습니다. 뷰에서 사용자가 제출한 데이터를 HTML로 인코딩하거나 컨트롤러에서 사용자가 제출한 데이터를 HTML 인코딩할 수 있습니다.

> [!div class="step-by-step"]
> [이전](authenticating-users-with-windows-authentication-vb.md)
