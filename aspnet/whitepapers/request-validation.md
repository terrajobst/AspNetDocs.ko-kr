---
uid: whitepapers/request-validation
title: 요청 유효성 검사-스크립트 공격 방지 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 기본적으로 응용 프로그램에서 인코딩되지 않은 HTML 콘텐츠 submitt ...를 처리 하지 못하도록 ASP.NET의 요청 유효성 검사 기능에 대해 설명 합니다.
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78520583"
---
# <a name="request-validation---preventing-script-attacks"></a>요청 유효성 검사 - 스크립트 공격 방지

> 이 문서에서는 기본적으로 응용 프로그램에서 서버에 전송 된 인코딩되지 않은 HTML 콘텐츠를 처리 하지 못하도록 하는 ASP.NET의 요청 유효성 검사 기능에 대해 설명 합니다. HTML 데이터를 안전 하 게 처리 하도록 응용 프로그램을 디자인 하는 경우이 요청 유효성 검사 기능을 사용 하지 않도록 설정할 수 있습니다.
> 
> ASP.NET 1.1 및 ASP.NET 2.0에 적용 됩니다.

버전 1.1부터 ASP.NET 기능 중 하나인 요청 유효성 검사는 서버에서 인코딩되지 않은 HTML을 포함한 콘텐츠를 허용하지 않도록 방지합니다. 이 기능은 클라이언트 스크립트 코드 또는 HTML을 무의식적으로 서버에 제출하고 저장한 다음 다른 사용자에게 제공할 수 있는 스크립트 삽입 공격을 방지하도록 설계되었습니다. 모든 입력 데이터의 유효성을 검사하고 적절한 경우 HTML로 인코딩하는 것이 좋습니다.

예를 들어 사용자의 전자 메일 주소를 요청 하 고 해당 전자 메일 주소를 데이터베이스에 저장 하는 웹 페이지를 만듭니다. 사용자가 유효한 전자 메일 주소 대신 &lt;스크립트&gt;경고 ("hello from SCRIPT")&lt;/스크립트&gt;를 입력 하는 경우 해당 데이터가 표시 되 면 콘텐츠가 제대로 인코딩되지 않은 경우이 스크립트를 실행할 수 있습니다. ASP.NET의 요청 유효성 검사 기능으로 인해이 문제가 발생 하지 않습니다.

## <a name="why-this-feature-is-useful"></a>이 기능이 유용한 이유

많은 사이트에서 간단한 스크립트 삽입 공격에 대해 공개 된 것을 인식 하지 못합니다. 이러한 공격의 목적이 HTML을 표시 하 여 사이트를 사용 하거나 잠재적으로 클라이언트 스크립트를 실행 하 여 사용자를 해커 사이트로 리디렉션하는 것이 든, 스크립트 삽입 공격은 웹 개발자가 경쟁 해야 하는 문제입니다.

스크립트 삽입 공격은 ASP.NET, ASP 또는 기타 웹 개발 기술을 사용 하는지에 관계 없이 모든 웹 개발자에 게 중요 합니다.

ASP.NET 요청 유효성 검사 기능은 개발자가 해당 콘텐츠를 허용 하도록 결정 하지 않는 한 서버에서 인코딩되지 않은 HTML 콘텐츠를 처리할 수 없도록 하 여 이러한 공격을 사전에 방지 합니다.

## <a name="what-to-expect-error-page"></a>예상치 못한 항목: 오류 페이지

아래 스크린샷은 몇 가지 샘플 ASP.NET 코드를 보여 줍니다.

![](request-validation/_static/image1.png)

이 코드를 실행 하면 텍스트 상자에 일부 텍스트를 입력할 수 있는 간단한 페이지가 표시 되며 단추를 클릭 하 고 레이블 컨트롤에 텍스트를 표시할 수 있습니다.

![](request-validation/_static/image2.png)

그러나 입력 및 제출할 `<script>alert("hello!")</script>`와 같은 JavaScript는 예외를 가져옵니다.

![](request-validation/_static/image3.png)

오류 메시지는 ' 잠재적으로 위험한 요청. 양식 값이 검색 되었습니다. ' 라는 메시지를 나타내고, 설명에 정확히 발생 한 작업과 동작을 변경 하는 방법에 대 한 자세한 정보를 제공 합니다. 다음은 그 예입니다.

요청 유효성 검사에서 잠재적으로 위험한 클라이언트 입력 값을 감지 하 여 요청 처리가 중단 되었습니다. 이 값은 사이트 간 스크립팅 공격과 같은 응용 프로그램의 보안을 손상 시키려는 시도를 나타낼 수 있습니다. 페이지 지시문 또는 구성 섹션에서 `validateRequest=false`을 설정 하 여 요청 유효성 검사를 사용 하지 않도록 설정할 수 있습니다. 그러나이 경우 응용 프로그램에서 모든 입력을 명시적으로 확인 하는 것이 좋습니다.

## <a name="disabling-request-validation-on-a-page"></a>페이지에서 요청 유효성 검사를 사용 하지 않도록 설정

페이지에서 요청 유효성 검사를 사용 하지 않도록 설정 하려면 Page 지시어의 `validateRequest` 특성을 `false`으로 설정 해야 합니다.

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> 요청 유효성 검사를 사용 하지 않도록 설정 하면 콘텐츠를 페이지에 제출할 수 있습니다. 콘텐츠를 제대로 인코드 또는 처리 하는지 확인 하는 것은 페이지 개발자의 책임입니다.

## <a name="disabling-request-validation-for-your-application"></a>응용 프로그램에 대 한 요청 유효성 검사 사용 안 함

응용 프로그램에 대 한 요청 유효성 검사를 사용 하지 않도록 설정 하려면 응용 프로그램에 대 한 web.config 파일을 수정 하거나 만들고 `<pages />` 섹션의 validateRequest 특성을 `false`으로 설정 해야 합니다.

[!code-xml[Main](request-validation/samples/sample2.xml)]

서버에 있는 모든 응용 프로그램에 대 한 요청 유효성 검사를 사용 하지 않도록 설정 하려면 Machine.config 파일을 수정 하면 됩니다.

> [!CAUTION]
> 요청 유효성 검사를 사용 하지 않도록 설정 하면 응용 프로그램에 콘텐츠를 제출할 수 있습니다. 응용 프로그램 개발자는 콘텐츠를 제대로 인코드 또는 처리 하는지 확인 해야 합니다.

아래 코드를 수정 하 여 요청 유효성 검사를 해제 합니다.

![](request-validation/_static/image4.png)

이제 다음 JavaScript가 텍스트 상자에 입력 되 면 결과가 `<script>alert("hello!")</script>` 됩니다.

![](request-validation/_static/image5.png)

이 문제가 발생 하지 않도록 하려면 요청 유효성 검사가 꺼져 있으면 콘텐츠를 HTML로 인코딩해야 합니다.

## <a name="how-to-html-encode-content"></a>콘텐츠를 HTML 인코딩하는 방법

요청 유효성 검사를 사용 하지 않도록 설정한 경우 나중에 사용 하기 위해 저장 되는 콘텐츠를 HTML로 인코딩하는 것이 좋습니다. HTML 인코딩은 '&lt;' 또는 '&gt;' (다른 여러 기호와 함께)를 해당 하는 HTML 인코딩된 표현으로 자동으로 바꿉니다. 예를 들어 '&lt;'는 '&amp;l t; '로 바뀌고 '&gt;'는 '&amp;gt; '로 바뀝니다. 브라우저는 이러한 특수 코드를 사용 하 여 브라우저에서 '&lt;' 또는 '&gt;'를 표시 합니다.

`Server.HtmlEncode(string)` API를 사용 하 여 서버에서 콘텐츠를 쉽게 HTML로 인코딩할 수 있습니다. 콘텐츠를 쉽게 HTML 디코딩할 수 있습니다. 즉, `Server.HtmlDecode(string)` 메서드를 사용 하 여 표준 HTML로 되돌릴 수도 있습니다.

![](request-validation/_static/image6.png)

결과:

![](request-validation/_static/image7.png)
