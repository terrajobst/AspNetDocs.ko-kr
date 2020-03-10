---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: ASP.NET 웹 페이지 (Razor) 사이트에서 HTML 양식 사용 | Microsoft Docs
author: Rick-Anderson
description: 양식은 텍스트 상자, 확인란, 라디오 단추 및 풀 다운 목록과 같은 사용자 입력 컨트롤을 배치 하는 HTML 문서의 섹션입니다. 호환성이 폼을 사용 합니다.
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519605"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 HTML 양식 사용

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor (ASP.NET 웹 페이지) 웹 사이트에서 작업할 때 텍스트 상자와 단추를 사용 하 여 HTML 폼을 처리 하는 방법을 설명 합니다.
> 
> **학습 내용:** 
> 
> - HTML 폼을 만드는 방법
> - 양식에서 사용자 입력을 읽는 방법
> - 사용자 입력의 유효성을 검사 하는 방법입니다.
> - 페이지가 제출 된 후 양식 값을 복원 하는 방법입니다.
> 
> 다음은이 문서에서 소개 하는 ASP.NET 프로그래밍 개념입니다.
> 
> - `Request` 개체입니다.
> - 입력 유효성 검사
> - HTML 인코딩입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

## <a name="creating-a-simple-html-form"></a>간단한 HTML 폼 만들기

1. 새 웹 사이트를 만듭니다.
2. 루트 폴더에서 이름이 *Form* 인 웹 페이지를 만들고 다음 태그를 입력 합니다.

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. 브라우저에서 페이지를 시작 합니다. (WebMatrix의 **파일** 작업 영역에서 파일을 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서 시작**을 선택 합니다.) 3 개의 입력 필드와 **제출** 단추가 있는 간단한 양식이 표시 됩니다.

    ![3 개의 입력란이 있는 폼의 스크린샷](4-working-with-forms/_static/image1.png)

    이 시점에서 **제출** 단추를 클릭 하면 아무 일도 발생 하지 않습니다. 폼을 유용 하 게 만들려면 서버에서 실행 되는 일부 코드를 추가 해야 합니다.

## <a name="reading-user-input-from-the-form"></a>양식에서 사용자 입력 읽기

폼을 처리 하려면 전송 된 필드 값을 읽고이를 사용 하 여 작업을 수행 하는 코드를 추가 합니다. 이 절차에서는 필드를 읽고 페이지에서 사용자 입력을 표시 하는 방법을 보여 줍니다. 프로덕션 응용 프로그램에서는 일반적으로 사용자 입력을 통해 더 흥미로운 작업을 수행 합니다. 데이터베이스 사용에 대 한 문서에서이 작업을 수행 합니다.

1. *Cshtml* 파일의 맨 위에 다음 코드를 입력 합니다.

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    사용자가 페이지를 처음 요청 하면 빈 양식만 표시 됩니다. 사용자가 폼을 채운 다음 **제출**을 클릭 합니다. 사용자 입력을 서버에 제출 (게시) 합니다. 기본적으로이 요청은 동일한 페이지 (예를 들어, *폼. cshtml*)로 이동 합니다.

    이번에 페이지를 제출 하면 입력 한 값이 폼 바로 위에 표시 됩니다.

    ![사용자가 페이지에 표시 한 값을 보여 주는 스크린샷](4-working-with-forms/_static/image2.png)

    페이지의 코드를 확인 합니다. 먼저 `IsPost` 메서드를 사용 하 여 페이지가 게시 &#8212; 되었는지 여부, 즉 사용자가 **제출** 단추를 클릭 했는지 여부를 확인 합니다. Post 인 경우 `IsPost` true를 반환 합니다. 이는 초기 요청 (GET 요청)을 사용 하는지 아니면 포스트백 (POST 요청)을 사용 하 고 있는지를 확인 하는 ASP.NET 웹 페이지 표준 방법입니다. GET 및 POST에 대 한 자세한 내용은 [Razor 구문을 사용 하는 ASP.NET 웹 페이지 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost)의 "HTTP GET 및 Post 및 IsPost 속성"을 참조 하세요.

    그런 다음 사용자가 `Request.Form` 개체에서 채운 값을 가져와 나중에 사용할 수 있도록 변수에 저장 합니다. `Request.Form` 개체는 페이지를 사용 하 여 제출 된 모든 값을 포함 하며, 각 값은 키로 식별 됩니다. 키는 읽을 폼 필드의 `name` 특성과 동일 합니다. 예를 들어 `companyname` 필드 (텍스트 상자)를 읽으려면 `Request.Form["companyname"]`를 사용 합니다.

    양식 값은 `Request.Form` 개체에 문자열로 저장 됩니다. 따라서 값을 숫자 또는 날짜 또는 다른 형식으로 사용 해야 하는 경우 문자열에서 해당 형식으로 변환 해야 합니다. 이 예제에서 `Request.Form`의 `AsInt` 메서드는 직원 수를 포함 하는 employees 필드의 값을 정수로 변환 하는 데 사용 됩니다.
2. 브라우저에서 페이지를 시작 하 고 양식 필드를 입력 한 다음 **제출**을 클릭 합니다. 이 페이지에는 사용자가 입력 한 값이 표시 됩니다.

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a>모양 및 보안을 위한 HTML 인코딩
> 
> HTML에는 `<`, `>`및 `&`와 같은 문자에 대 한 특별 한 사용이 있습니다. 이러한 특수 문자가 필요 하지 않은 위치에 표시 되는 경우 웹 페이지의 모양과 기능을 ruin 수 있습니다. 예를 들어 브라우저는 `<b>` 또는 `<input ...>`와 같이 HTML 요소의 시작으로 `<` 문자 (공백이 뒤에 오지 않는 경우)를 해석 합니다. 브라우저에서 요소를 인식 하지 못하는 경우 다시 인식 되는 항목에 도달할 때까지 `<`로 시작 하는 문자열을 삭제 하기만 하면 됩니다. 이로 인해 페이지에서 이상한 렌더링이 발생할 수 있습니다.
> 
> HTML 인코딩은 이러한 예약 문자를 브라우저에서 올바른 기호로 해석 하는 코드로 바꿉니다. 예를 들어 `<` 문자는 `&lt;`로 바뀌고 `>` 문자는 `&gt;`로 바뀝니다. 브라우저는 이러한 대체 문자열을 확인 하려는 문자로 렌더링 합니다.
> 
> 사용자가 가져온 문자열 (입력)을 표시할 때마다 HTML 인코딩을 사용 하는 것이 좋습니다. 그렇지 않으면 사용자가 웹 페이지에서 악의적인 스크립트를 실행 하거나 사이트 보안을 손상 시키는 다른 작업을 수행 하거나 의도 한 것이 아닌 다른 작업을 수행할 수 있습니다. 사용자 입력을 사용 하 고 원하는 대로 저장 한 다음 나중 &#8212; 에 예를 들어 블로그 주석, 사용자 검토 또는 이와 같은 항목으로 표시 하는 경우에 특히 중요 합니다.
> 
> 이러한 문제를 방지 하기 위해 ASP.NET 웹 페이지 코드에서 출력 하는 텍스트 콘텐츠를 자동으로 HTML로 인코딩합니다. 예를 들어 `@MyVar`와 같은 코드를 사용 하 여 변수 또는 식의 내용을 표시 하는 경우 ASP.NET 웹 페이지 출력을 자동으로 인코딩합니다.

## <a name="validating-user-input"></a>사용자 입력 유효성 검사

사용자에 게 실수가 있습니다. 사용자가 필드를 채우도록 요청 하 고, 직원 수를 입력 하 라는 메시지를 표시 하거나 대신 이름을 입력 하도록 요청 합니다. 처리 하기 전에 양식이 올바르게 입력 되었는지 확인 하려면 사용자 입력의 유효성을 검사 합니다.

이 절차에서는 세 가지 양식 필드의 유효성을 검사 하 여 사용자가 비워 두지 않았는지 확인 하는 방법을 보여 줍니다. 또한 employee count 값이 숫자 인지 확인 합니다. 오류가 있는 경우 유효성 검사를 통과 하지 못한 값을 사용자에 게 알리는 오류 메시지를 표시 합니다.

1. *Cshtml* 파일에서 첫 번째 코드 블록을 다음 코드로 바꿉니다. 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    사용자 입력의 유효성을 검사 하려면 `Validation` 도우미를 사용 합니다. `Validation.RequireField`를 호출 하 여 필수 필드를 등록 합니다. `Validation.Add`를 호출 하 고 유효성을 검사할 필드와 수행할 유효성 검사 유형을 지정 하 여 다른 유형의 유효성 검사를 등록 합니다.

    페이지가 실행 될 때 ASP.NET는 모든 유효성 검사를 수행 합니다. `Validation.IsValid`를 호출 하 여 결과를 확인할 수 있습니다 .이는 모두 성공 하면 true를 반환 하 고, 필드의 유효성 검사에 실패 하면 false를 반환 합니다. 일반적으로 사용자 입력에 대 한 처리를 수행 하기 전에 `Validation.IsValid`를 호출 합니다.
2. 다음과 같이 `Html.ValidationMessage` 메서드에 세 개의 호출을 추가 하 여 `<body>` 요소를 업데이트 합니다.

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    유효성 검사 오류 메시지를 표시 하려면 Html.`ValidationMessage`를 호출 하면 됩니다. 메시지에 사용할 필드의 이름을 전달 합니다.
3. 페이지를 실행 합니다. 필드를 비워 두고 **전송**을 클릭 합니다. 오류 메시지가 표시 됩니다.

    ![사용자 입력이 유효성 검사를 통과 하지 못한 경우 표시 되는 오류 메시지를 보여 주는 스크린샷](4-working-with-forms/_static/image3.jpg)
4. **직원 수** 필드에 문자열 (예: "ABC")을 추가 하 고 **제출을** 다시 클릭 합니다. 이번에는 문자열이 올바른 형식 (예를 들어, 정수)이 아님을 나타내는 오류가 표시 됩니다.

    ![사용자가 직원 필드에 대 한 문자열을 입력 하는 경우 표시 되는 오류 메시지를 보여 주는 스크린샷](4-working-with-forms/_static/image4.jpg)

ASP.NET 웹 페이지은 사용자가 브라우저에서 즉각적인 피드백을 받을 수 있도록 클라이언트 스크립트를 사용 하 여 자동으로 유효성 검사를 수행 하는 기능을 포함 하 여 사용자 입력의 유효성을 검사 하는 옵션을 자세한 내용은 나중에 [추가 리소스](#Additional_Resources) 섹션을 참조 하세요.

## <a name="restoring-form-values-after-postbacks"></a>다시 게시 후 양식 값 복원

이전 섹션에서 페이지를 테스트 하는 경우 유효성 검사 오류가 발생 하 고 입력 한 모든 항목 (잘못 된 데이터만 아님)이 없어졌으므로 모든 필드에 대 한 값을 다시 입력 해야 하는 것을 알 수 있습니다. 이는 중요 한 점을 보여 줍니다. 페이지를 제출 하 고 처리 한 다음 페이지를 다시 렌더링 하면 페이지가 처음부터 다시 만들어집니다. 이는 표시 된 것 처럼 페이지에서 제출 된 모든 값이 손실 됩니다.

그러나이 문제는 쉽게 해결할 수 있습니다. 전송 된 값에 액세스할 수 있습니다 (`Request.Form` 개체에서 페이지가 렌더링 될 때 이러한 값을 양식 필드에 다시 채울 수 있습니다.

1. *형식. cshtml* 파일에서 `value` 특성을 사용 하 여 `<input>` 요소의 `value` 특성을 바꿉니다. 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    `<input>` 요소의 `value` 특성이 `Request.Form` 개체에서 필드 값을 동적으로 읽도록 설정 되었습니다. 페이지가 처음 요청 될 때 `Request.Form` 개체의 값은 모두 비어 있습니다. 이 방법은 폼이 비어 있기 때문에 문제가 없습니다.
2. 브라우저에서 페이지를 시작 하 고 양식 필드를 입력 하거나 비워 두고 **전송**을 클릭 합니다. 전송 된 값을 표시 하는 페이지가 표시 됩니다.

    ![양식-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 리소스

- [1001 웹 사용자의 입력을 가져오는 방법](https://msdn.microsoft.com/library/ms971057.aspx)
- [양식 사용 및 사용자 입력 처리](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)
- [ASP.NET 웹 페이지 사이트에서 사용자 입력 유효성 검사](https://go.microsoft.com/fwlink/?LinkId=253002)
- [HTML 양식에서 자동 완성 사용](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)
