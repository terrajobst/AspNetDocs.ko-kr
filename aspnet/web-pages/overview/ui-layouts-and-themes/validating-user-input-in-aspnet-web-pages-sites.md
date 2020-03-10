---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: ASP.NET 웹 페이지 (Razor) 사이트에서 사용자 입력 유효성 검사 | Microsoft Docs
author: Rick-Anderson
description: 이 문서에서는 사용자에 게 제공 되는 &mdash; 정보를 확인 하는 방법에 대해 설명 합니다. 즉, 사용자가의 HTML 양식에 올바른 정보를 입력 하는 것을 확인 하려면 ...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78454301"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 사용자 입력 유효성 검사

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 사용자가 &mdash; 하는 정보를 확인 하는 방법에 대해 설명 합니다. 즉, 사용자가 Razor (ASP.NET 웹 페이지) 사이트의 HTML 양식으로 유효한 정보를 입력 하 게 됩니다.
> 
> 학습할 내용:
> 
> - 사용자의 입력이 정의 하는 유효성 검사 조건과 일치 하는지 확인 하는 방법입니다.
> - 모든 유효성 검사 테스트가 통과 했는지 여부를 확인 하는 방법입니다.
> - 유효성 검사 오류를 표시 하는 방법 및 형식을 지정 하는 방법입니다.
> - 사용자에 게 직접 제공 되지 않는 데이터의 유효성을 검사 하는 방법입니다.
> 
> 다음은이 문서에서 소개 하는 ASP.NET 프로그래밍 개념입니다.
> 
> - `Validation` 도우미입니다.
> - `Html.ValidationSummary` 및 `Html.ValidationMessage` 메서드입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

이 문서에는 다음과 같은 섹션이 포함되어 있습니다.

- [사용자 입력 유효성 검사 개요](#Overview_of_User_Input_Validation)
- [사용자 입력 유효성 검사](#Validating_User_Input)
- [클라이언트 쪽 유효성 검사 추가](#Adding_Client-Side_Validation)
- [유효성 검사 오류 서식 지정](#Formatting_Validation_Errors)
- [사용자에 게 직접 제공 되지 않는 데이터 유효성 검사](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a>사용자 입력 유효성 검사 개요

사용자에 게 페이지에 정보를 입력 하도록 요청 하는 경우 (예: 양식) 입력 하는 값이 유효한 지 확인 하는 것이 중요 합니다. 예를 들어 중요 한 정보가 없는 폼을 처리 하지 않으려는 경우

사용자가 HTML 양식에 값을 입력 하는 경우 입력 하는 값은 문자열입니다. 많은 경우에 필요한 값은 정수 또는 날짜와 같은 다른 데이터 형식입니다. 따라서 사용자가 입력 하는 값을 적절 한 데이터 형식으로 올바르게 변환할 수 있는지도 확인 해야 합니다.

값에 대 한 특정 제한이 있을 수도 있습니다. 예를 들어 사용자가 정수를 올바르게 입력 하는 경우에도 값이 특정 범위 내에 있는지 확인 해야 합니다.

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> **중요** 사용자 입력의 유효성을 검사 하는 것도 보안을 위해 중요 합니다. 사용자가 양식에 입력할 수 있는 값을 제한 하는 경우 사용자가 사이트의 보안을 손상 시킬 수 있는 값을 입력할 수 있는 기회가 줄어듭니다.

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a>사용자 입력 유효성 검사

ASP.NET 웹 페이지 2에서는 `Validator` 도우미를 사용 하 여 사용자 입력을 테스트할 수 있습니다. 기본적인 방법은 다음을 수행 하는 것입니다.

1. 유효성을 검사할 입력 요소 (필드)를 결정 합니다.

    일반적으로 폼의 `<input>` 요소에 있는 값의 유효성을 검사 합니다. 그러나 `<select>` 목록과 같이 제한 된 요소에서 제공 되는 입력을 비롯 하 여 모든 입력의 유효성을 검사 하는 것이 좋습니다. 이렇게 하면 사용자가 페이지에서 컨트롤을 우회 하 고 양식을 전송 하지 않도록 할 수 있습니다.
2. 페이지 코드에서 `Validation` 도우미의 메서드를 사용 하 여 각 입력 요소에 대 한 개별 유효성 검사를 추가 합니다.

    필수 필드를 확인 하려면 `Validation.RequireField(field, [error message])` (개별 필드의 경우) 또는 `Validation.RequireFields(field1, field2, ...))` (필드 목록의 경우)를 사용 합니다. 다른 형식의 유효성 검사를 수행 하려면 `Validation.Add(field, ValidationType)`을 사용 합니다. `ValidationType`의 경우 다음 옵션을 사용할 수 있습니다.

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. 페이지가 제출 되 면 유효성 검사를 `Validation.IsValid`확인 하 여 통과 했는지 확인 합니다.

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    유효성 검사 오류가 있는 경우 일반 페이지 처리를 건너뜁니다. 예를 들어, 페이지의 목적이 데이터베이스를 업데이트 하는 경우 모든 유효성 검사 오류가 해결 될 때까지이 작업을 수행 하지 않습니다.
4. 유효성 검사 오류가 있는 경우 `Html.ValidationSummary` 또는 `Html.ValidationMessage`또는 둘 다를 사용 하 여 페이지의 태그에 오류 메시지를 표시 합니다.

다음 예에서는 이러한 단계를 보여 주는 페이지를 보여 줍니다.

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

유효성 검사가 작동 하는 방식을 확인 하려면이 페이지를 실행 하 고 의도적으로 실수를 합니다. 예를 들어 강좌 이름을 입력 하 고,를 입력 하 고, 잘못 된 날짜를 입력 하는 경우 페이지는 다음과 같습니다.

![렌더링 된 페이지의 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a>클라이언트측 유효성 검사 추가

기본적으로 사용자 입력은 사용자가 페이지를 전송한 후 유효성 검사가 수행 됩니다. 즉, 서버 코드에서 유효성 검사가 수행 됩니다. 이 방법의 단점은 사용자가 페이지를 제출할 때까지 오류가 발생 한 것을 사용자가 알지 못하는 것입니다. 폼이 길거나 복잡 한 경우에는 사용자가 페이지를 전송한 후에만 오류를 보고 하는 것이 불편할 수 있습니다.

클라이언트 스크립트에서 유효성 검사를 수행 하는 지원을 추가할 수 있습니다. 이 경우 사용자가 브라우저에서 작업할 때 유효성 검사가 수행 됩니다. 예를 들어 값을 정수로 지정 한다고 가정 합니다. 사용자가 정수가 아닌 값을 입력 하는 경우 사용자가 입력 필드를 벗어나면 오류가 즉시 보고 됩니다. 사용자는 즉각적인 피드백을 받을 수 있습니다. 클라이언트 기반 유효성 검사를 사용 하면 사용자가 여러 오류를 수정 하기 위해 양식을 제출 해야 하는 횟수를 줄일 수 있습니다.

> [!NOTE]
> 클라이언트 쪽 유효성 검사를 사용 하더라도 유효성 검사는 항상 서버 코드 에서도 수행 됩니다. 사용자가 클라이언트 기반 유효성 검사를 우회 하는 경우 서버 코드에서 유효성 검사를 수행 하는 것이 보안 조치입니다.

1. 페이지에 다음 JavaScript 라이브러리를 등록 합니다.  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   라이브러리 중 두 개는 CDN (content delivery network)에서 로드할 수 있으므로 컴퓨터 또는 서버에 반드시 있어야 하는 것은 아닙니다. 그러나 사용자에 게는 jquery의 로컬 복사본이 있어야 합니다 *.* 라이브러리를 포함 하는 WebMatrix 템플릿 (예: **스타터 사이트** )을 아직 사용 하지 않는 경우 **스타터 사이트**를 기반으로 하는 웹 페이지 사이트를 만듭니다. 그런 다음, *.js* 파일을 현재 사이트에 복사 합니다.
2. 태그에서 유효성을 검사 하는 각 요소에 대해 `Validation.For(field)`에 대 한 호출을 추가 합니다. 이 메서드는 클라이언트 쪽 유효성 검사에 사용 되는 특성을 내보냅니다. 메서드는 실제 JavaScript 코드를 내보내는 대신 `data-val-...`와 같은 특성을 내보냅니다. 이러한 특성은 jQuery를 사용 하 여 작업을 수행 하는 클라이언트의 유효성 검사를 지원 하지 않습니다.

다음 페이지에서는 앞에 나온 예제에 클라이언트 유효성 검사 기능을 추가 하는 방법을 보여 줍니다.

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

일부 유효성 검사는 클라이언트에서 실행 되지 않습니다. 특히 데이터 형식 유효성 검사 (정수, 날짜 등)는 클라이언트에서 실행 되지 않습니다. 클라이언트와 서버 모두에서 다음 검사를 수행 합니다.

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

이 예제에서 유효한 날짜에 대 한 테스트는 클라이언트 코드에서 작동 하지 않습니다. 그러나 테스트는 서버 코드에서 수행 됩니다.

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a>유효성 검사 오류 서식 지정

다음 예약 된 이름이 있는 CSS 클래스를 정의 하 여 유효성 검사 오류를 표시 하는 방법을 제어할 수 있습니다.

- `field-validation-error`입니다. 오류가 표시 될 때 `Html.ValidationMessage` 메서드의 출력을 정의 합니다.
- `field-validation-valid`입니다. 오류가 없을 때 `Html.ValidationMessage` 메서드의 출력을 정의 합니다.
- `input-validation-error`입니다. 오류가 있을 때 `<input>` 요소가 렌더링 되는 방식을 정의 합니다. 예를 들어이 클래스를 사용 하 여 &lt;입력&gt; 요소의 배경색을 다른 색으로 설정할 수 있습니다 (해당 값이 유효 하지 않은 경우). 이 CSS 클래스는 클라이언트 유효성 검사 (ASP.NET 웹 페이지 2의 경우) 중에만 사용 됩니다.
- `input-validation-valid`입니다. 오류가 없을 때 `<input>` 요소의 모양을 정의 합니다.
- `validation-summary-errors`입니다. 오류 목록을 표시 하는 `Html.ValidationSummary` 메서드의 출력을 정의 합니다.
- `validation-summary-valid`입니다. 오류가 없을 때 `Html.ValidationSummary` 메서드의 출력을 정의 합니다.

다음 `<style>` 블록에서는 오류 조건에 대 한 규칙을 보여 줍니다.

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

이 문서 앞부분의 예제 페이지에이 스타일 블록을 포함 하는 경우 오류 표시는 다음 그림과 같이 표시 됩니다.

![CSS 스타일 클래스를 사용 하는 유효성 검사 오류](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> ASP.NET 웹 페이지 2에서 클라이언트 유효성 검사를 사용 하지 않는 경우 `<input>` 요소에 대 한 CSS 클래스 (`input-validation-error` 및 `input-validation-valid`는 아무런 영향을 주지 않습니다.

### <a name="static-and-dynamic-error-display"></a>정적 및 동적 오류 표시

CSS 규칙은 `validation-summary-errors` 및 `validation-summary-valid`와 같이 쌍으로 제공 됩니다. 이러한 쌍을 통해 오류 조건 및 "일반" (오류 아님) 조건에 대 한 규칙을 정의할 수 있습니다. 오류 표시에 대 한 태그는 오류가 없더라도 항상 렌더링 된다는 것을 이해 하는 것이 중요 합니다. 예를 들어 페이지의 태그에 `Html.ValidationSummary` 메서드가 있는 경우 페이지를 처음 요청 하는 경우에도 페이지 소스에는 다음 태그가 포함 됩니다.

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

즉, `Html.ValidationSummary` 메서드는 오류 목록이 비어 있는 경우에도 항상 `<div>` 요소와 목록을 렌더링 합니다. 마찬가지로 `Html.ValidationMessage` 메서드는 오류가 없더라도 항상 개별 필드 오류에 대 한 자리 표시자로 `<span>` 요소를 렌더링 합니다.

경우에 따라 오류 메시지를 표시 하면 페이지를 리플로우 하 여 페이지의 요소가 이동 될 수 있습니다. `-valid` 종료 되는 CSS 규칙을 사용 하면이 문제를 방지 하는 데 도움이 되는 레이아웃을 정의할 수 있습니다. 예를 들어 `field-validation-error`를 정의 하 고 둘 다의 고정 크기를 `field-validation-valid` 수 있습니다. 이렇게 하면 필드의 표시 영역이 정적이 고 오류 메시지가 표시 되 면 페이지 흐름이 변경 되지 않습니다.

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a>사용자에 게 직접 제공 되지 않는 데이터 유효성 검사

HTML 양식에서 직접 제공 하지 않는 정보의 유효성을 검사 해야 하는 경우도 있습니다. 일반적인 예는 다음 예제와 같이 쿼리 문자열에서 값이 전달 되는 페이지입니다.

`http://server/myapp/EditClassInformation?classid=1022`

이 경우 페이지에 전달 된 값 (여기서는 `classid`값의 1022)이 유효한 지 확인 하려고 합니다. `Validation` 도우미를 직접 사용 하 여이 유효성 검사를 수행할 수 없습니다. 그러나 유효성 검사 오류 메시지를 표시 하는 기능과 같은 유효성 검사 시스템의 다른 기능을 사용할 수 있습니다.

> [!NOTE] 
> 
> **중요** 양식 필드 값, 쿼리 문자열 값 및 쿠키 값을 포함 하 여 *모든* 원본에서 가져온 값의 유효성을 항상 검사 합니다. 사용자는 이러한 값을 쉽게 변경할 수 있습니다 (악의적인 목적을 위해). 따라서 응용 프로그램을 보호 하기 위해 이러한 값을 확인 해야 합니다.

다음 예에서는 쿼리 문자열에 전달 된 값의 유효성을 검사 하는 방법을 보여 줍니다. 이 코드는 값이 비어 있지 않고 정수 인지 테스트 합니다.

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

요청이 양식 전송 (`if(!IsPost)`)이 아닌 경우 테스트가 수행 됩니다. 이 테스트는 페이지가 처음 요청 될 때를 전달 하지만 요청이 양식 전송 인 경우에는 전달 되지 않습니다.

이 오류를 표시 하려면 `Validation.AddFormError("message")`를 호출 하 여 유효성 검사 오류 목록에 오류를 추가할 수 있습니다. 페이지에 `Html.ValidationSummary` 메서드에 대 한 호출이 포함 된 경우 사용자 입력 유효성 검사 오류와 마찬가지로 오류가 표시 됩니다.

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a>추가 리소스

[ASP.NET 웹 페이지 사이트에서 HTML 양식 사용](https://go.microsoft.com/fwlink/?LinkID=202892)
