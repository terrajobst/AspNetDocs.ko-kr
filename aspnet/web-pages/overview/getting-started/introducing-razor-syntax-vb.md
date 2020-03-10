---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개 (Visual Basic) | Microsoft Docs
author: Rick-Anderson
description: 이 부록에서는 Razor 구문를 사용 하 여 Visual Basic ASP.NET 웹 페이지를 사용한 프로그래밍에 대 한 개요를 제공 합니다.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78422663"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a>Razor 구문(Visual Basic)을 사용하는 ASP.NET 웹 프로그래밍 소개

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor 구문 및 Visual Basic를 사용 하 여 ASP.NET 웹 페이지 프로그래밍에 대 한 개요를 제공 합니다. ASP.NET는 웹 서버에서 동적 웹 페이지를 실행 하기 위한 Microsoft 기술입니다.
> 
> **학습 내용**:
> 
> - Razor 구문를 사용 하 여 프로그래밍 ASP.NET 웹 페이지 시작 하기 위한 상위 8 개 프로그래밍 팁.
> - 필요한 기본 프로그래밍 개념.
> - ASP.NET 서버 코드 및 Razor 구문은 무엇 인가요?
>   
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동 합니다.

Razor 구문에서 ASP.NET 웹 페이지를 사용 하는 대부분 C#의 예제는를 사용 합니다. 그러나 Razor 구문는 Visual Basic도 지원 합니다. Visual Basic에서 ASP.NET 웹 페이지를 프로그래밍 *하려면 파일 이름* 확장명을 사용 하 여 웹 페이지를 만든 다음 Visual Basic 코드를 추가 합니다. 이 문서에서는 ASP.NET 웹 페이지를 만들기 위한 Visual Basic 언어 및 구문을 사용 하는 방법에 대 한 개요를 제공 합니다.

> [!NOTE]
> Microsoft WebMatrix (**빵집**, **사진 갤러리**및 **스타터 사이트**등)의 기본 웹 사이트 템플릿은 및 Visual Basic 버전에서 C# 사용할 수 있습니다. NuGet 패키지로 Visual Basic 템플릿을 설치할 수 있습니다. 웹 사이트 템플릿은 *Microsoft templates*라는 폴더에 있는 사이트의 루트 폴더에 설치 됩니다.

## <a name="the-top-8-programming-tips"></a>상위 8 개 프로그래밍 팁

이 섹션에는 Razor 구문를 사용 하 여 ASP.NET 서버 코드 작성을 시작할 때 알아야 할 몇 가지 팁이 나열 되어 있습니다.

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. @ 문자를 사용 하 여 페이지에 코드를 추가 합니다.

`@` 문자는 인라인 식, 단일 문 블록 및 다중 문 블록을 시작 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![Razor-.Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 인코딩**
> 
> 앞의 예제와 같이 `@` 문자를 사용 하 여 페이지에 콘텐츠를 표시 하는 경우 ASP.NET은 출력을 HTML로 인코딩합니다. 이렇게 하면 예약 된 HTML 문자 (예: `<`, `>` 및 `&`)가 HTML 태그나 엔터티로 해석 되지 않고 웹 페이지에서 문자로 표시 될 수 있도록 하는 코드와 바뀝니다. HTML 인코딩이 없으면 서버 코드의 출력이 올바르게 표시 되지 않을 수 있으며, 페이지를 보안 위험에 노출 시킬 수 있습니다.
> 
> 태그를 태그로 렌더링 하는 HTML 태그를 출력 하는 경우 (`<p></p>` 예: 단락이 나 텍스트를 강조 하는 `<em></em>`)에는이 문서의 뒷부분에 나오는 [코드 블록의 텍스트, 태그 및 코드 결합](#BM_CombiningTextMarkupAndCode) 단원을 참조 하세요.
> 
> [ASP.NET 웹 페이지 사이트에서 Html 양식 사용](https://go.microsoft.com/fwlink/?LinkId=202892)에 대 한 자세한 내용을 확인할 수 있습니다.

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a>2. 코드 블록을 코드로 묶습니다. 최종 코드

코드 블록에는 하나 이상의 코드 문이 포함 되 고 `Code` 및 `End Code`키워드로 묶입니다. `@` 문자 &#8212; 바로 뒤에 여는 `Code` 키워드를 추가 합니다. 태그 사이에 공백이 있을 수 없습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a>3. 블록 내에서 각 코드 문을 줄 바꿈으로 종료 합니다.

Visual Basic 코드 블록에서 각 문은 줄 바꿈으로 끝납니다. (필요에 따라 긴 코드 문을 여러 줄로 래핑하는 방법에 대해서는이 문서의 뒷부분에서 설명 합니다.)

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a>4. 변수를 사용 하 여 값 저장

문자열, 숫자, 날짜 등을 포함 하 여 *변수에*값을 저장할 수 있습니다. `Dim` 키워드를 사용 하 여 새 변수를 만듭니다. `@`를 사용 하 여 페이지에 직접 변수 값을 삽입할 수 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. 리터럴 문자열 값을 큰따옴표로 묶습니다.

*문자열* 은 텍스트로 처리 되는 문자 시퀀스입니다. 문자열을 지정 하려면 큰따옴표로 묶습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

문자열 값에 큰따옴표를 포함 하려면 두 개의 큰따옴표 문자를 삽입 합니다. 페이지 출력에 큰따옴표를 한 번 표시 하려면 따옴표 붙은 문자열 내에 `""`로 입력 하 고, 두 번째 문자를 두 번 표시 하려면 따옴표 붙은 문자열 내에 `""""`로 입력 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a>6. Visual Basic 코드는 대/소문자를 구분 하지 않습니다.

Visual Basic 언어는 대/소문자를 구분 하지 않습니다. 프로그래밍 키워드 (예: `Dim`, `If`, `True`) 및 변수 이름 (예: `myString`또는 `subTotal`)은 어떤 경우 든 쓸 수 있습니다.

다음 코드 줄에서는 소문자 이름을 사용 하 `lastname` 변수에 값을 할당 한 다음 대문자 이름을 사용 하 여 변수 값을 페이지에 출력 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a>7. 코딩의 대부분이 개체 작업을 포함 합니다.

개체는 페이지, 텍스트 상자, 파일, 이미지 &#8212; , 웹 요청, 전자 메일 메시지, 고객 레코드 (데이터베이스 행) 등을 사용 하 여 프로그래밍할 수 있는 작업을 나타냅니다. 개체에는 텍스트 상자 개체에 &#8212; `Text` 속성이 있고, 요청 개체에 `Url` 속성이 있고, 메일 메시지에 `From` 속성이 있으며, customer 개체에 `FirstName` 속성이 있는 특성을 설명 하는 속성이 있습니다. 개체에는 수행할 수&quot; &quot;동사 인 메서드도 있습니다. 예제에는 파일 개체의 `Save` 메서드, 이미지 개체의 `Rotate` 메서드 및 전자 메일 개체의 `Send` 메서드가 포함 됩니다.

페이지의 양식 필드 값 (입력란 등), 요청을 만든 브라우저의 유형, 페이지 URL, 사용자 id 등의 정보를 제공 하는 `Request` 개체를 사용 하는 경우가 많습니다. 이 예제에서는 `Request` 개체의 속성에 액세스 하는 방법과 서버에서 페이지의 절대 경로를 제공 하는 `Request` 개체의 `MapPath` 메서드를 호출 하는 방법을 보여 줍니다.

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 결정을 내리는 코드를 작성할 수 있습니다.

동적 웹 페이지의 핵심 기능은 조건에 따라 수행할 작업을 결정할 수 있다는 것입니다. 이 작업을 수행 하는 가장 일반적인 방법은 `If` 문 (및 선택적 `Else` 문)을 사용 하는 것입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

`If IsPost` 문은 `If IsPost = True`를 작성 하는 간단한 방법입니다. `If` 문과 함께 조건을 테스트 하 고, 코드 블록을 반복 하 고,이 문서의 뒷부분에서 설명 하는 다양 한 방법이 있습니다.

브라우저에 표시 되는 결과 ( **Submit**를 클릭 한 후):

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **HTTP GET 및 POST 메서드 및 IsPost 속성**
> 
> 웹 페이지 (HTTP)에 사용 되는 프로토콜은 서버에 대 한 요청을 수행 하는 데 사용 되는 매우 제한 된 수의 메서드 (&quot;동사&quot;)를 지원 합니다. 가장 일반적인 두 가지는 페이지를 읽는 데 사용 되는 GET과 페이지를 전송 하는 데 사용 되는 게시물입니다. 일반적으로 사용자가 페이지를 처음 요청할 때 페이지는 GET을 사용 하 여 요청 됩니다. 사용자가 양식을 채운 다음 **제출**을 클릭 하면 브라우저에서 서버에 대 한 POST 요청을 수행 합니다.
> 
> 웹 프로그래밍에서 페이지를 처리 하는 방법을 알 수 있도록 페이지를 GET 또는 POST로 요청 하 고 있는지 여부를 확인 하는 것이 유용한 경우가 많습니다. ASP.NET 웹 페이지에서 `IsPost` 속성을 사용 하 여 요청이 GET 또는 POST 인지 여부를 확인할 수 있습니다. 요청이 POST 인 경우 `IsPost` 속성은 true를 반환 하 고 폼에서 텍스트 상자의 값을 읽는 등의 작업을 수행할 수 있습니다. `IsPost`값에 따라 페이지를 다르게 처리 하는 방법을 보여 주는 많은 예제가 나와 있습니다.

## <a name="a-simple-code-example"></a>간단한 코드 예제

이 절차에서는 기본 프로그래밍 기술을 보여 주는 페이지를 만드는 방법을 보여 줍니다. 이 예제에서는 사용자가 두 개의 숫자를 입력 하 고 그 결과를 추가 하 고 결과를 표시할 수 있는 페이지를 만듭니다.

1. 편집기에서 새 파일을 만들고 이름을 *Addnumbers. vbhtml*로 추가 합니다.
2. 페이지에 이미 있는 항목을 대체 하 여 다음 코드와 태그를 페이지에 복사 합니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    유의 해야 할 몇 가지 사항은 다음과 같습니다.

    - `@` 문자는 페이지에서 첫 번째 코드 블록을 시작 하 고 맨 아래에 포함 된 `totalMessage` 변수 앞에 옵니다.
    - 페이지 맨 위에 있는 블록은 `Code...End Code`로 묶여 있습니다.
    - 변수 `total`, `num1`, `num2`및 `totalMessage`에는 여러 숫자와 문자열이 저장 됩니다.
    - `totalMessage` 변수에 할당 된 리터럴 문자열 값이 큰따옴표로 묶여 있습니다.
    - Visual Basic 코드는 대/소문자를 구분 하지 않으므로 `totalMessage` 변수를 페이지의 아래쪽 근처에 사용 하는 경우 해당 이름은 페이지 맨 위에 있는 변수 선언의 철자와 일치 하기만 하면 됩니다. 대/소문자 구분은 중요 하지 않습니다.
    - 식 `num1.AsInt()` + `num2.AsInt()` 개체 및 메서드로 작업 하는 방법을 보여 줍니다. 각 변수의 `AsInt` 메서드는 사용자가 입력 한 문자열을 추가할 수 있는 정수 (정수)로 변환 합니다.
    - `<form>` 태그는 `method="post"` 특성을 포함 합니다. 이렇게 하면 사용자가 **추가**를 클릭 하면 HTTP POST 메서드를 사용 하 여 페이지가 서버에 전송 됩니다. 페이지가 전송 되 면 코드 `If IsPost`이 true로 평가 되 고 조건부 코드가 실행 되어 숫자를 더한 결과를 표시 합니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다. (파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 두 개의 정수를 입력 한 다음 **추가** 단추를 클릭 합니다.

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a>Visual Basic 언어 및 구문

앞에서 ASP.NET 웹 페이지를 만드는 방법 및 HTML 태그에 서버 코드를 추가 하는 방법의 기본 예를 살펴보았습니다. 여기서는 Visual Basic 사용 하 여 Razor 구문 &#8212; 프로그래밍 언어 규칙을 사용 하 여 ASP.NET 서버 코드를 작성 하는 기본 사항을 알아봅니다.

프로그래밍 경험이 있는 경우 (특히 C, C++, C#, Visual Basic 또는 JavaScript를 사용 하는 경우) 여기에서 읽는 많은 내용이 익숙할 것입니다. 사용자는 WebMatrix 코드를 *. vbhtml* 파일의 태그에 추가 하는 방법만 숙지 해야 할 것입니다.

### <a id="BM_CombiningTextMarkupAndCode"></a>코드 블록에서 텍스트, 태그 및 코드 결합

서버 코드 블록에서 텍스트 및 태그를 페이지에 출력 하는 경우가 많습니다. 서버 코드 블록에 코드가 아닌 텍스트가 포함 되어 있는 경우 해당 텍스트를 그대로 렌더링 해야 하는 경우 ASP.NET는 해당 텍스트를 코드와 구별할 수 있어야 합니다. 여러 가지 방법으로 이 작업을 수행할 수 있습니다.

- `<p></p>` 또는 `<em></em>`와 같은 HTML 블록 요소의 텍스트를 묶습니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    HTML 요소에는 텍스트, 추가 HTML 요소 및 서버 코드 식이 포함 될 수 있습니다. ASP.NET는 여는 HTML 태그 (예: `<p>`)를 볼 때 요소와 해당 콘텐츠를 브라우저에 그대로 렌더링 하 고 서버 코드 식을 확인 합니다.

- `@:` 연산자 또는 `<text>` 요소를 사용 합니다. `@:`는 일반 텍스트 또는 일치 하지 않는 HTML 태그를 포함 하는 단일 내용의 줄을 출력 합니다. `<text>` 요소는 여러 줄을 출력으로 묶습니다. 이러한 옵션은 HTML 요소를 출력의 일부로 렌더링 하지 않으려는 경우에 유용 합니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    다음 예제에서는 이전 예제를 반복 하지만 단일 쌍의 `<text>` 태그를 사용 하 여 렌더링할 텍스트를 묶습니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    다음 예제에서 `<text>` 및 `</text>` 태그는 세 개의 줄을 포함 하며, 모든 줄에는 포함 되지 않은 텍스트와 일치 하지 않는 HTML 태그 (`<br />`)가 서버 코드 및 일치 하는 HTML 태그와 함께 포함 됩니다. 또한 각 줄 앞에 `@:` 연산자를 사용 하 여 개별적으로 추가할 수 있습니다. 어떤 방법이 든 작동 합니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > HTML 요소를 사용 하 여이 섹션 &#8212; 에 표시 된 대로 텍스트를 출력 하는 경우 `@:` 연산자 또는 `<text>` &#8212; 요소 ASP.NET은 출력을 html로 인코딩하지 않습니다. 앞에서 설명한 것 처럼 ASP.NET는이 섹션에 설명 된 특수 한 사례를 제외 하 고 `@`뒤에 오는 서버 코드 식과 서버 코드 블록의 출력을 인코딩합니다.

### <a name="whitespace"></a>공백

문 (및 문자열 리터럴 외부)의 추가 공백은 문에 영향을 주지 않습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a>긴 문을 여러 줄로 분할

코드의 각 줄 뒤에 밑줄 문자 `_` (Visual Basic를 *연속 문자*라고 함)를 사용 하 여 긴 코드 문을 여러 줄로 나눌 수 있습니다. 문을 다음 줄로 나누려면 줄의 끝에 공백을 추가 하 고 연속 문자를 추가 합니다. 다음 줄에서 문을 계속 합니다. 가독성을 높이는 데 필요한 만큼의 줄로 문을 래핑할 수 있습니다. 다음 문은 동일합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

그러나 문자열 리터럴 중간에 줄을 줄 바꿈할 수는 없습니다. 다음 예는 작동 하지 않습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

위의 코드와 같이 여러 줄로 래핑하는 긴 문자열을 결합 하려면이 문서의 뒷부분에 나오는 *연결 연산자* (`&`)를 사용 해야 합니다.

### <a name="code-comments"></a>코드 주석

주석을 사용 하 여 자신에 게 메모를 남길 수 있습니다. Razor 구문 주석은 접두사로 `@*` 하 고 `*@`로 끝납니다.

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

코드 블록 내에서 Razor 구문 주석을 사용 하거나 각 줄 앞에 있는 작은따옴표 (`'`) 인 일반 Visual Basic 주석 문자를 사용할 수 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a>variables

변수는 데이터를 저장 하는 데 사용 하는 명명 된 개체입니다. 변수 이름을 지정할 수 있지만 이름은 영문자로 시작 해야 하며 공백 또는 예약 문자를 포함할 수 없습니다. Visual Basic에서 앞서 살펴본 것 처럼 변수 이름에 있는 문자의 대/소문자는 중요 하지 않습니다.

### <a name="variables-and-data-types"></a>변수 및 데이터 형식

변수에는 변수에 저장 되는 데이터의 종류를 나타내는 특정 데이터 형식이 있을 수 있습니다. 문자열 값 (&quot;예: Hello 세계&quot;), 정수 값 (예: 3 또는 79)을 저장 하는 정수 변수, 날짜 값을 다양 한 형식 (예: 4/12/2012 또는 3 월 2009)으로 저장 하는 날짜 변수를 저장 하는 문자열 변수를 사용할 수 있습니다. 사용할 수 있는 다른 많은 데이터 형식이 있습니다.

그러나 변수의 형식을 지정할 필요는 없습니다. 대부분의 경우 ASP.NET는 변수의 데이터를 사용 하는 방법에 따라 형식을 파악할 수 있습니다. 때로는 형식을 지정 해야 합니다 .이 경우에는 예제가 표시 됩니다.

형식을 지정 하지 않고 변수를 선언 하려면 `Dim` 및 변수 이름 (예 `Dim myVar`)을 사용 합니다. 형식을 사용 하 여 변수를 선언 하려면 `Dim`와 변수 이름을 차례로 사용 하 고 `As` 다음에 형식 이름 (예를 들어 `Dim myVar As String`)을 사용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

다음 예제에서는 웹 페이지의 변수를 사용 하는 일부 인라인 식을 보여 줍니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>데이터 형식 변환 및 테스트

ASP.NET는 일반적으로 데이터 형식을 자동으로 결정할 수 있지만 경우에 따라 자동으로 데이터 형식을 결정할 수는 없습니다. 따라서 명시적 변환을 수행 하 여 ASP.NET를 지원 해야 할 수 있습니다. 형식을 변환 하지 않아도 되는 경우에도 사용할 수 있는 데이터 형식을 테스트 하는 것이 도움이 될 수 있습니다.

가장 일반적인 경우는 문자열을 정수 또는 날짜와 같은 다른 형식으로 변환 해야 한다는 것입니다. 다음 예에서는 문자열을 숫자로 변환 해야 하는 일반적인 경우를 보여 줍니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

사용자 입력은 사용자가 문자열로 제공 됩니다. 사용자에 게 숫자를 입력 하 라는 메시지가 표시 되 고 숫자를 입력 한 경우에도 사용자 입력이 제출 되 고 코드에서이를 읽으면 데이터는 문자열 형식입니다. 따라서 문자열을 숫자로 변환 해야 합니다. 예를 들어 값을 변환 하지 않고 값에 대해 산술 연산을 수행 하려고 하면 ASP.NET에서 두 개의 문자열을 추가할 수 없기 때문에 다음과 같은 오류가 발생 합니다.

`Cannot implicitly convert type 'string' to 'int'.`

값을 정수로 변환 하려면 `AsInt` 메서드를 호출 합니다. 성공적으로 변환 되 면 숫자를 추가할 수 있습니다.

다음 표에서는 변수에 대 한 몇 가지 일반적인 변환과 테스트 메서드를 보여 줍니다.

:::row:::
    :::column:::
        <strong>메서드</strong>
    :::column-end:::
    :::column:::
        <strong>설명</strong>
    :::column-end:::
    :::column:::
        <strong>예제</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        정수 (예: &quot;593&quot;)를 나타내는 문자열을 정수로 변환 합니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        &quot;true&quot; 또는 &quot;false&quot; 같은 문자열을 부울 형식으로 변환 합니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        &quot;1.3&quot; 또는 &quot;7.439&quot; 같은 10 진수 값을 포함 하는 문자열을 부동 소수점 숫자로 변환 합니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        &quot;1.3&quot; 또는 &quot;7.439&quot; 같은 10 진수 값이 있는 문자열을 10 진수로 변환 합니다. ASP.NET에서 10 진수는 부동 소수점 숫자 보다 더 정확 합니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        날짜 및 시간 값을 나타내는 문자열을 ASP.NET `DateTime` 형식으로 변환 합니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        다른 모든 데이터 형식을 문자열로 변환 합니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>연산자

연산자는 식에서 수행할 명령의 종류를 ASP.NET 알려 주는 키워드 또는 문자입니다. Visual Basic는 많은 연산자를 지원 하지만 ASP.NET 웹 페이지 개발을 시작 하기 위해 몇 가지를 인식 하기만 하면 됩니다. 다음 표에서는 가장 일반적인 연산자를 요약 합니다.

:::row:::
    :::column:::
        <strong>연산자</strong>
    :::column-end:::
    :::column:::
        <strong>설명</strong>
    :::column-end:::
    :::column:::
        <strong>예</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        숫자 식에 사용 되는 수학 연산자입니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        할당 및 같음. 컨텍스트에 따라 문의 오른쪽에 있는 값을 좌 변에 있는 개체에 할당 하거나 값이 같은지 확인 합니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        같지 않음 값이 같지 않으면 `True`을 반환 합니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        보다 작음, 보다 큼, 작거나 같음, 보다 크거나 같음
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        연결-문자열을 조인 하는 데 사용 됩니다.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        증가 및 감소 연산자-변수에서 1 (각각)을 더하거나 뺍니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        점과. 개체와 해당 속성 및 메서드를 구분 하는 데 사용 됩니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        괄호. 식을 그룹화 하 고, 매개 변수를 메서드에 전달 하 고, 배열 및 컬렉션의 멤버에 액세스 하는 데 사용 됩니다.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        나타내지. True 값을 false로 바꾸고 그 반대의 경우도 마찬가지입니다. 일반적으로 `False` (즉, `True`)을 테스트 하는 간단한 방법으로 사용 됩니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        논리적 AND 및 OR 이며 조건을 함께 연결 하는 데 사용 됩니다.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a>코드에서 파일 및 폴더 경로 작업

코드에서 파일 및 폴더 경로를 사용 하 여 작업 하는 경우가 많습니다. 다음은 개발 컴퓨터에 표시 될 수 있는 웹 사이트의 물리적 폴더 구조에 대 한 예입니다.

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

Url 및 경로에 대 한 몇 가지 필수 정보는 다음과 같습니다.

- URL은 도메인 이름 (`http://www.example.com`) 또는 서버 이름 (`http://localhost`, `http://mycomputer`)으로 시작 합니다.
- URL은 호스트 컴퓨터의 실제 경로에 해당 합니다. 예를 들어 `http://myserver` 서버의 *C:\websites\mywebsite* 폴더에 해당할 수 있습니다.
- 가상 경로는 전체 경로를 지정 하지 않고도 코드에서 경로를 나타내는 축약형입니다. 도메인 또는 서버 이름 뒤에 오는 URL의 부분을 포함 합니다. 가상 경로를 사용 하는 경우 경로를 업데이트 하지 않고도 다른 도메인 이나 서버로 코드를 이동할 수 있습니다.

차이점을 이해 하는 데 도움이 되는 예는 다음과 같습니다.

| 전체 URL | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| 서버 이름 | *mycompanyserver* |
| 가상 경로 | */humanresources/CompanyPolicy.htm* |
| 실제 경로 | *C:\mywebsites\humanresources\CompanyPolicy.htm* |

C: 드라이브의 루트가 \ 인 것 처럼 가상 루트는/입니다. 가상 폴더 경로는 항상 슬래시를 사용 합니다. 폴더의 가상 경로에는 물리적 폴더와 동일한 이름을 사용할 수 없습니다. 별칭 일 수 있습니다. 프로덕션 서버에서 가상 경로는 정확히 실제 경로와 거의 일치 하지 않습니다.

코드에서 파일 및 폴더를 사용할 때 사용 하는 개체에 따라 실제 경로와 때때로 가상 경로를 참조 해야 하는 경우가 있습니다. ASP.NET는 코드에서 파일 및 폴더 경로를 사용 하기 위한 다음과 같은 도구를 제공 합니다. `Server.MapPath` 메서드 및 `~` 연산자 및 `Href` 메서드입니다.

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>가상에서 실제 경로로 변환: Server. MapPath 메서드

`Server.MapPath` 메서드는 가상 경로 (예: */default.cshtml*)를 절대 실제 경로 (예: *C:\WebSites\MyWebSiteFolder\default.cshtml*)로 변환 합니다. 이 메서드는 전체 실제 경로가 필요할 때마다 사용 합니다. 일반적인 예로 웹 서버에서 텍스트 파일 또는 이미지 파일을 읽거나 쓰는 경우를 들 수 있습니다.

일반적으로 호스팅 사이트 서버에서 사이트의 절대 실제 경로를 알 수 없으므로이 메서드는 사용자가 알고 있는 경로 (가상 경로)를 서버의 해당 경로로 변환할 수 있습니다. 파일이 나 폴더에 대 한 가상 경로를 메서드에 전달 하 고 실제 경로를 반환 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>가상 루트 참조: ~ operator 및 Href 메서드

*Cshtml* 또는 *vbhtml* 파일에서 `~` 연산자를 사용 하 여 가상 루트 경로를 참조할 수 있습니다. 이는 사이트에서 페이지를 이동할 수 있으며 다른 페이지에 포함 된 모든 링크가 손상 되지 않도록 하기 때문에 매우 편리 합니다. 웹 사이트를 다른 위치로 이동 하는 경우에도 유용 합니다. 예를 들어 다음과 같은 노래를 선택할 수 있다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

웹 사이트가 `http://myserver/myapp`경우 페이지가 실행 될 때 ASP.NET에서 이러한 경로를 처리 하는 방법은 다음과 같습니다.

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

이러한 경로는 변수의 값으로 실제로 표시 되지 않지만 ASP.NET는 경로를 해당 하는 것 처럼 처리 합니다.

다음과 같이 서버 코드와 태그에서 모두 `~` 연산자를 사용할 수 있습니다.

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

태그에서 `~` 연산자를 사용 하 여 이미지 파일, 다른 웹 페이지 및 CSS 파일과 같은 리소스에 대 한 경로를 만듭니다. 페이지가 실행 될 때 ASP.NET는 페이지 (코드 및 태그 모두)를 살펴보고 적절 한 경로에 대 한 모든 `~` 참조를 확인 합니다.

## <a name="conditional-logic-and-loops"></a>조건부 논리 및 루프

ASP.NET 서버 코드를 사용 하면 조건에 따라 작업을 수행 하 고 특정 횟수 (루프를 실행 하는 코드)로 문을 반복 하는 코드를 작성할 수 있습니다.

### <a name="testing-conditions"></a>테스트 조건

간단한 조건을 테스트 하려면 지정 하는 테스트에 따라 `True` 또는 `False`를 반환 하는 `If...Then` 문을 사용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

`If` 키워드는 블록을 시작 합니다. 실제 테스트 (조건)는 `If` 키워드를 따르며 true 또는 false를 반환 합니다. `If` 문이 `Then`로 끝납니다. 테스트를 true로 설정 하는 경우 실행 되는 문은 `If` 및 `End If`으로 묶입니다. `If` 문은 조건이 false 인 경우 실행할 문을 지정 하는 `Else` 블록을 포함할 수 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

`If` 문이 코드 블록을 시작 하는 경우 일반적인 `Code...End Code` 문을 사용 하 여 블록을 포함할 필요가 없습니다. 블록에 `@`를 추가 하기만 하면 작동 합니다. 이 방법은 `If`와 함께 사용할 수 있으며, `For`, `For Each`, `Do While`등의 코드 블록 뒤에 나오는 기타 Visual Basic 프로그래밍 키워드를 사용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

하나 이상의 `ElseIf` 블록을 사용 하 여 여러 조건을 추가할 수 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

이 예에서는 `If` 블록의 첫 번째 조건이 true가 아니면 `ElseIf` 조건이 검사 됩니다. 이러한 조건이 충족 되 면 `ElseIf` 블록의 문이 실행 됩니다. 조건을 충족 하는 조건이 없으면 `Else` 블록의 문이 실행 됩니다. 개수에 관계 없이 `ElseIf` 블록을 추가한 다음 `Else` 블록을 사용 하 여 다른 모든&quot; 조건으로 &quot;수 있습니다.

많은 수의 조건을 테스트 하려면 `Select Case` 블록을 사용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

테스트할 값이 괄호 안에 있습니다 (예: weekday 변수). 각 개별 테스트는 값을 나열 하는 `Case` 문을 사용 합니다. `Case` 문의 값이 테스트 값과 일치 하면 해당 `Case` 블록의 코드가 실행 됩니다.

브라우저에 표시 되는 마지막 두 조건부 블록의 결과입니다.

![Razor-Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a>반복 코드

동일한 문을 반복적으로 실행 해야 하는 경우가 많습니다. 이렇게 하려면 반복 합니다. 예를 들어 데이터 컬렉션의 각 항목에 대해 동일한 문을 실행 하는 경우가 많습니다. 반복 하려는 횟수를 정확히 알고 있는 경우 `For` 루프를 사용할 수 있습니다. 이러한 종류의 루프는 계산 하거나 계산 하는 데 특히 유용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

루프는 `For` 키워드로 시작 하 고 그 뒤에 세 개의 요소가 있습니다.

- `For` 문 바로 다음에는 카운터 변수를 선언 하 고 (`Dim`를 사용할 필요가 없음) `i = 10 to 20`에서와 같이 범위를 지정할 수 있습니다. 즉, `i` 변수는 10에서 계산을 시작 하 고 20 (포함)에 도달할 때까지 계속 됩니다.
- `For` 문과 `Next` 문은 블록의 내용입니다. 여기에는 각 루프에서 실행 되는 하나 이상의 코드 문이 포함 될 수 있습니다.
- `Next i` 문은 루프를 종료 합니다. 카운터를 증가 시키고 루프의 다음 반복을 시작 합니다.

`For`와 `Next` 줄 사이에 있는 코드 줄에는 루프가 반복 될 때마다 실행 되는 코드가 포함 됩니다. 태그는 매번 새 단락 (`<p>` 요소)을 만들고 출력에 줄을 추가 하 여 i (카운터)의 값을 표시 합니다. 이 페이지를 실행 하는 경우이 예제에서는 출력을 표시 하는 11 개의 줄을 만들며 각 줄의 텍스트는 항목 번호를 나타냅니다.

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

컬렉션 또는 배열에 대 한 작업을 수행 하는 경우에는 종종 `For Each` 루프를 사용 합니다. 컬렉션은 유사한 개체의 그룹 이며, `For Each` 루프를 사용 하 여 컬렉션의 각 항목에 대 한 작업을 수행할 수 있습니다. 이 유형의 루프는 `For` 루프와 달리 카운터를 증가 시키거나 제한을 설정할 필요가 없기 때문에 컬렉션에 편리 합니다. 대신 `For Each` 루프 코드는 완료 될 때까지 컬렉션을 진행 합니다.

이 예제에서는 웹 서버에 대 한 정보를 포함 하는 `Request.ServerVariables` 컬렉션의 항목을 반환 합니다. `For Each` 루프를 사용 하 여 HTML 글머리 기호 목록에 새 `<li>` 요소를 만들어 각 항목의 이름을 표시 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

`For Each` 키워드 뒤에는 컬렉션의 단일 항목을 나타내는 변수 (예: `myItem`)가 오고 그 뒤에 `In` 키워드가 오고 그 뒤에 반복 하려는 컬렉션이 나옵니다. `For Each` 루프의 본문에서 이전에 선언한 변수를 사용 하 여 현재 항목에 액세스할 수 있습니다.

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

보다 일반적인 용도의 루프를 만들려면 `Do While` 문을 사용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

이 루프는 `Do While` 키워드와 조건, 반복 되는 블록 순서로 시작 됩니다. 루프는 일반적으로 계산에 사용 되는 변수 또는 개체를 증가 (추가) 또는 감소 (빼기) 합니다. 예제에서 `+=` 연산자는 루프가 실행 될 때마다 변수 값에 1을 더 합니다. (에서 계산 되는 루프의 변수를 감소 시키려면 감소 연산자 `-=`를 사용 합니다.)

## <a name="objects-and-collections"></a>개체 및 컬렉션

ASP.NET 웹 사이트의 거의 모든 항목은 웹 페이지를 포함 하는 개체입니다. 이 섹션에서는 코드에서 자주 사용 하는 몇 가지 중요 한 개체에 대해 설명 합니다.

### <a name="page-objects"></a>Page 개체

ASP.NET의 가장 기본적인 개체는 페이지입니다. 정규화 된 개체 없이 페이지 개체의 속성에 직접 액세스할 수 있습니다. 다음 코드에서는 페이지의 `Request` 개체를 사용 하 여 페이지의 파일 경로를 가져옵니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

`Page` 개체의 속성을 사용 하 여 다음과 같은 많은 정보를 얻을 수 있습니다.

- `Request`입니다. 앞서 살펴본 것 처럼, 요청을 만든 브라우저의 유형, 페이지 URL, 사용자 id 등을 포함 하 여 현재 요청에 대 한 정보 컬렉션입니다.
- `Response`입니다. 서버 코드의 실행이 완료 되 면 브라우저로 전송 되는 응답 (페이지)에 대 한 정보 컬렉션입니다. 예를 들어이 속성을 사용 하 여 응답에 정보를 쓸 수 있습니다.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a>컬렉션 개체 (배열 및 사전)

컬렉션은 데이터베이스의 `Customer` 개체 컬렉션과 같이 동일한 유형의 개체 그룹입니다. ASP.NET에는 `Request.Files` 컬렉션과 같은 여러 기본 제공 컬렉션이 포함 되어 있습니다.

컬렉션의 데이터로 작업 하는 경우가 많습니다. 두 가지 일반적인 컬렉션 형식은 *배열* 및 *사전*입니다. 배열은 비슷한 항목의 컬렉션을 저장 하지만 각 항목을 저장할 별도의 변수를 만들지 않으려는 경우에 유용 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

배열을 사용 하 여 `String`, `Integer`또는 `DateTime`와 같은 특정 데이터 형식을 선언 합니다. 변수에 배열이 포함 될 수 있음을 나타내려면 선언에서 변수 이름에 괄호를 추가 합니다 (예: `Dim myVar() As String`). 해당 위치 (인덱스)를 사용 하거나 `For Each` 문을 사용 하 여 배열의 항목에 액세스할 수 있습니다. 배열 인덱스는 0부터 시작 &#8212; 합니다. 즉, 첫 번째 항목의 위치는 0이 고, 두 번째 항목은 위치 1에 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

`Length` 속성을 가져와서 배열의 항목 수를 확인할 수 있습니다. 배열에서 특정 항목의 위치를 가져오려면 (즉, 배열 검색) `Array.IndexOf` 메서드를 사용 합니다. 배열의 콘텐츠를 반전 (`Array.Reverse` 메서드) 하거나 내용을 정렬 (`Array.Sort` 메서드) 하는 등의 작업을 수행할 수도 있습니다.

브라우저에 표시 되는 문자열 배열 코드의 출력입니다.

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

사전은 키 (또는 이름)를 제공 하 여 해당 값을 설정 하거나 검색할 수 있는 키/값 쌍의 컬렉션입니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

사전을 만들려면 `New` 키워드를 사용 하 여 새 `Dictionary` 개체를 만들고 있음을 표시 합니다. `Dim` 키워드를 사용 하 여 변수에 사전을 할당할 수 있습니다. 괄호 (`( )`)를 사용 하 여 사전에 있는 항목의 데이터 형식을 표시 합니다. 선언 끝에서 다른 괄호 쌍을 추가 해야 합니다 .이는 실제로 새 사전을 만드는 메서드입니다.

사전에 항목을 추가 하려면 사전 변수의 `Add` 메서드 (이 경우`myScores`)를 호출한 다음 키와 값을 지정 하면 됩니다. 또는 다음 예제와 같이 괄호를 사용 하 여 키를 나타내고 간단한 할당을 수행할 수 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

사전에서 값을 가져오려면 괄호 안에 키를 지정 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a>매개 변수를 사용 하 여 메서드 호출

이 문서 앞부분에서 살펴본 것 처럼를 사용 하 여 프로그래밍 하는 개체에는 메서드가 있습니다. 예를 들어 `Database` 개체에는 `Database.Connect` 메서드가 있을 수 있습니다. 또한 많은 메서드에 하나 이상의 매개 변수가 있습니다. *매개 변수* 는 메서드가 해당 작업을 완료할 수 있도록 메서드에 전달 하는 값입니다. 예를 들어 다음 세 개의 매개 변수를 사용 하는 `Request.MapPath` 메서드에 대 한 선언을 살펴보세요.

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

이 메서드는 지정 된 가상 경로에 해당 하는 서버의 실제 경로를 반환 합니다. 메서드에 대 한 세 가지 매개 변수는 `virtualPath`, `baseVirtualDir`및 `allowCrossAppMapping`입니다. 선언에서 매개 변수는 허용 되는 데이터의 데이터 형식과 함께 나열 됩니다. 이 메서드를 호출 하는 경우 세 매개 변수 모두에 대 한 값을 제공 해야 합니다.

Razor 구문와 함께 Visual Basic를 사용 하는 경우 메서드에 매개 변수를 전달 하는 두 가지 옵션 ( *위치 매개 변수* 또는 *명명 된 매개*변수)이 있습니다. 위치 매개 변수를 사용 하 여 메서드를 호출 하려면 메서드 선언에 지정 된 엄격한 순서로 매개 변수를 전달 합니다. (일반적으로 메서드의 설명서를 읽어이 순서를 확인 합니다.) 순서를 따라야 하며 필요한 경우 매개 변수 &#8212; 를 건너뛸 수 없습니다. 값이 없는 위치 매개 변수에 대해 빈 문자열 (`""`) 또는 null을 전달 합니다.

다음 예제에서는 웹 사이트에 *scripts* 라는 폴더가 있다고 가정 합니다. 이 코드는 `Request.MapPath` 메서드를 호출 하 고 세 개의 매개 변수에 대 한 값을 올바른 순서로 전달 합니다. 그런 다음 결과 매핑된 경로를 표시 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

메서드에 대 한 매개 변수가 많은 경우 명명 된 매개 변수를 사용 하 여 코드를 더 간결 하 고 읽기 쉽게 유지할 수 있습니다. 명명 된 매개 변수를 사용 하 여 메서드를 호출 하려면 매개 변수 이름 뒤에 `:=`를 지정 하 고 값을 제공 합니다. 명명 된 매개 변수의 장점은 원하는 순서로 추가할 수 있다는 것입니다. 이는 메서드 호출이 압축 되지 않는다는 단점이 있습니다.

다음 예제에서는 위와 동일한 메서드를 호출 하지만 명명 된 매개 변수를 사용 하 여 값을 제공 합니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

여기에서 볼 수 있듯이 매개 변수는 다른 순서로 전달 됩니다. 그러나 이전 예제와이 예제를 실행 하면 동일한 값이 반환 됩니다.

## <a name="handling-errors"></a>오류 처리

### <a name="try-catch-statements"></a>Try-catch 문

코드에 컨트롤 외부의 이유로 실패할 수 있는 문이 종종 있습니다. 다음은 그 예입니다.

- 코드에서 파일 열기, 만들기, 읽기 또는 쓰기를 시도 하는 경우 모든 종류의 오류가 발생할 수 있습니다. 필요한 파일이 없거나, 잠겨 있거나, 코드에 권한이 없을 수 있습니다.
- 마찬가지로, 코드에서 데이터베이스의 레코드를 업데이트 하려고 시도 하는 경우에는 사용 권한 문제가 있을 수 있습니다. 데이터베이스에 대 한 연결이 삭제 될 수 있습니다. 저장할 데이터가 유효 하지 않을 수 있습니다.

프로그래밍 측면에서 이러한 상황을 *예외*라고 합니다. 코드에서 예외가 발생 하는 경우 사용자에 게 가장 잘 방해가 되는 오류 메시지를 생성 (throw) 합니다.

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

코드에 예외가 발생할 수 있는 상황에서이 유형의 오류 메시지를 방지 하기 위해 `Try/Catch` 문을 사용할 수 있습니다. `Try` 문에서 확인 중인 코드를 실행 합니다. 하나 이상의 `Catch` 문에서 발생 했을 수 있는 특정 오류 (특정 유형의 예외)를 찾을 수 있습니다. 예상 되는 오류를 찾기 위해 필요한 만큼 `Catch` 문을 포함할 수 있습니다.

> [!NOTE]
> `Try/Catch` 문에서는 `Response.Redirect` 메서드를 사용 하지 않는 것이 좋습니다 .이는 페이지에서 예외를 발생 시킬 수 있기 때문입니다.

다음 예에서는 첫 번째 요청에서 텍스트 파일을 만든 다음 사용자가 파일을 열 수 있도록 하는 단추를 표시 하는 페이지를 보여 줍니다. 이 예제에서는 예외를 발생 시 키 지 않도록 의도적으로 잘못 된 파일 이름을 사용 합니다. 이 코드에는 두 가지 예외에 대 한 `Catch` 문이 포함 되어 있습니다. `FileNotFoundException`는 파일 이름이 잘못 된 경우에 발생 하는 것이 고, ASP.NET에서 폴더를 찾을 수 없는 경우에 발생 하는 `DirectoryNotFoundException`입니다. (모든 것이 제대로 작동 하는 경우 실행 되는 방식을 확인 하기 위해 예제에서 문의 주석 처리를 제거할 수 있습니다.)

코드에서 예외를 처리 하지 않은 경우 이전 스크린샷과 같은 오류 페이지가 표시 됩니다. 그러나 `Try/Catch` 섹션을 사용 하면 사용자가 이러한 유형의 오류를 볼 수 있습니다.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a>추가 리소스

### <a name="reference-documentation"></a>참조 설명서

- [ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)
- [Visual Basic 언어](https://msdn.microsoft.com/library/2x7h1hfk.aspx)
