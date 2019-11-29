---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Razor 구문 (C#)을 사용 하는 ASP.NET 웹 프로그래밍 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 장에서는 Razor 구문를 사용 하 ASP.NET 웹 페이지 프로그래밍에 대 한 개요를 제공 합니다. ASP.NET는 동적 웹 pa를 실행 하는 Microsoft 기술입니다 ...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564882"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a>Razor 구문 (C#)을 사용 하는 ASP.NET 웹 프로그래밍 소개

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 Razor 구문를 사용 하 여 ASP.NET 웹 페이지 프로그래밍에 대 한 개요를 제공 합니다. ASP.NET는 웹 서버에서 동적 웹 페이지를 실행 하기 위한 Microsoft 기술입니다. 이 문서에서는 프로그래밍 언어를 C# 사용 하는 방법을 중점적으로 설명 합니다.
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

## <a name="the-top-8-programming-tips"></a>상위 8 개 프로그래밍 팁

이 섹션에는 Razor 구문를 사용 하 여 ASP.NET 서버 코드 작성을 시작할 때 알아야 할 몇 가지 팁이 나열 되어 있습니다.

> [!NOTE]
> Razor 구문은 C# 프로그래밍 언어를 기반으로 하며,이는 ASP.NET 웹 페이지에서 가장 자주 사용 되는 언어입니다. 그러나이 Razor 구문는 Visual Basic 언어도 지원 하 고 모든 사용자가 Visual Basic에서 수행할 수도 있습니다. 자세한 내용은 부록 [Visual Basic 언어 및 구문](https://go.microsoft.com/fwlink/?LinkId=202908)을 참조 하세요.

이러한 프로그래밍 기술에 대 한 자세한 내용은이 문서의 뒷부분에서 확인할 수 있습니다.

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. @ 문자를 사용 하 여 페이지에 코드를 추가 합니다.

`@` 문자는 인라인 식, 단일 문 블록 및 다중 문 블록을 시작 합니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

이는 페이지가 브라우저에서 실행 될 때 다음과 같이 표시 됩니다.

![Razor-.Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> **HTML 인코딩**
> 
> 앞의 예제와 같이 `@` 문자를 사용 하 여 페이지에 콘텐츠를 표시 하는 경우 ASP.NET은 출력을 HTML로 인코딩합니다. 이렇게 하면 예약 된 HTML 문자 (예: `<`, `>` 및 `&`)가 HTML 태그나 엔터티로 해석 되지 않고 웹 페이지에서 문자로 표시 될 수 있도록 하는 코드와 바뀝니다. HTML 인코딩이 없으면 서버 코드의 출력이 올바르게 표시 되지 않을 수 있으며, 페이지를 보안 위험에 노출 시킬 수 있습니다.
> 
> 태그를 태그로 렌더링 하는 HTML 태그를 출력 하는 경우 (`<p></p>` 예: 단락이 나 텍스트를 강조 하는 `<em></em>`)에는이 문서의 뒷부분에 나오는 [코드 블록의 텍스트, 태그 및 코드 결합](#BM_CombiningTextMarkupAndCode) 단원을 참조 하세요.
> 
> [양식 작업](https://go.microsoft.com/fwlink/?LinkId=202892)에서 HTML 인코딩에 대해 자세히 알아볼 수 있습니다.

### <a name="2-you-enclose-code-blocks-in-braces"></a>2. 코드 블록을 중괄호로 묶습니다.

*코드 블록* 에는 하나 이상의 코드 문이 포함 되 고 중괄호로 묶여 있습니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a>3. 블록 내에서 각 코드 문은 세미콜론으로 끝납니다.

코드 블록 내에서 각 완성 된 코드 문은 세미콜론으로 끝나야 합니다. 인라인 식은 세미콜론으로 끝나지 않습니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a>4. 변수를 사용 하 여 값 저장

문자열, 숫자, 날짜 등을 포함 하 여 *변수에*값을 저장할 수 있습니다. `var` 키워드를 사용 하 여 새 변수를 만듭니다. `@`를 사용 하 여 페이지에 직접 변수 값을 삽입할 수 있습니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. 리터럴 문자열 값을 큰따옴표로 묶습니다.

*문자열* 은 텍스트로 처리 되는 문자 시퀀스입니다. 문자열을 지정 하려면 큰따옴표로 묶습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

표시 하려는 문자열에 백슬래시 문자 (`\`) 또는 큰따옴표 (`"`)가 포함 된 경우에는 `@` 연산자 접두사가 붙은 *축 자 문자열 리터럴을* 사용 합니다. 에서 C#\ 문자는 축 자 문자열 리터럴을 사용 하지 않는 한 특별 한 의미를 갖습니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

큰따옴표를 포함 하려면 축 자 문자열 리터럴을 사용 하 고 따옴표를 반복 합니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

다음은 페이지에서 두 예제를 모두 사용 하는 결과입니다.

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> `@` 문자는 및의 C# 축 자 문자열 리터럴을 표시 하 고 ASP.NET 페이지에 코드를 표시 하는 데 사용 됩니다.

### <a name="6-code-is-case-sensitive"></a>6. 코드는 대/소문자를 구분 합니다.

에서 C#키워드 (예: `var`, `true`, `if`) 및 변수 이름은 대/소문자를 구분 합니다. 다음 코드 줄에서는 두 개의 서로 다른 변수 `lastName` 및 `LastName.`를 만듭니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

변수를 `var lastName = "Smith";` 선언 하 고 페이지에서 `@LastName`으로 해당 변수를 참조 하려고 하면 `"Smith"`대신 `"Jones"` 값이 표시 됩니다.

> [!NOTE]
> Visual Basic 키워드와 변수는 대/소문자를 구분 *하지 않습니다* .

### <a name="7-much-of-your-coding-involves-objects"></a>7. 대부분의 코딩에는 개체가 포함 됩니다.

*개체* 는 페이지, 텍스트 상자, 파일, 이미지 &#8212; , 웹 요청, 전자 메일 메시지, 고객 레코드 (데이터베이스 행) 등을 사용 하 여 프로그래밍할 수 있는 작업을 나타냅니다. 개체에는 특성을 설명 하는 속성이 있으며, 텍스트 상자 개체 &#8212; 에 `Text` 속성이 있는지 여부를 읽거나 변경할 수 있습니다. 즉, 요청 개체에는 `Url` 속성이 있고, 메일 메시지에는 `From` 속성이 있으며, 고객 개체에는 `FirstName` 속성이 있습니다. 개체에는 수행할 수&quot; &quot;동사 인 메서드도 있습니다. 예제에는 파일 개체의 `Save` 메서드, 이미지 개체의 `Rotate` 메서드 및 전자 메일 개체의 `Send` 메서드가 포함 됩니다.

페이지의 텍스트 상자 (양식 필드) 값, 요청을 만든 브라우저의 유형, 페이지 URL, 사용자 id 등의 정보를 제공 하는 `Request` 개체로 작업 하는 경우가 많습니다. 다음 예제에서는 `Request` 개체의 속성에 액세스 하는 방법과 서버에서 페이지의 절대 경로를 제공 하는 `Request` 개체의 `MapPath` 메서드를 호출 하는 방법을 보여 줍니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

브라우저에 표시 되는 결과는 다음과 같습니다.

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. 결정을 내리는 코드를 작성할 수 있습니다.

동적 웹 페이지의 핵심 기능은 조건에 따라 수행할 작업을 결정할 수 있다는 것입니다. 이 작업을 수행 하는 가장 일반적인 방법은 `if` 문 (및 선택적 `else` 문)을 사용 하는 것입니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

`if(IsPost)` 문은 `if(IsPost == true)`를 작성 하는 간단한 방법입니다. `if` 문과 함께 조건을 테스트 하 고, 코드 블록을 반복 하 고,이 문서의 뒷부분에서 설명 하는 다양 한 방법이 있습니다.

브라우저에 표시 되는 결과 ( **Submit**를 클릭 한 후):

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a>HTTP GET 및 POST 메서드 및 IsPost 속성
> 
> 웹 페이지 (HTTP)에 사용 되는 프로토콜은 서버에 대 한 요청을 수행 하는 데 사용 되는 매우 제한 된 수의 메서드 (동사)를 지원 합니다. 가장 일반적인 두 가지는 페이지를 읽는 데 사용 되는 GET과 페이지를 전송 하는 데 사용 되는 게시물입니다. 일반적으로 사용자가 페이지를 처음 요청할 때 페이지는 GET을 사용 하 여 요청 됩니다. 사용자가 양식을 채운 다음 제출 단추를 클릭 하면 브라우저에서 서버에 대 한 POST 요청을 수행 합니다.
> 
> 웹 프로그래밍에서 페이지를 처리 하는 방법을 알 수 있도록 페이지를 GET 또는 POST로 요청 하 고 있는지 여부를 확인 하는 것이 유용한 경우가 많습니다. ASP.NET 웹 페이지에서 `IsPost` 속성을 사용 하 여 요청이 GET 또는 POST 인지 여부를 확인할 수 있습니다. 요청이 POST 인 경우 `IsPost` 속성은 true를 반환 하 고 폼에서 텍스트 상자의 값을 읽는 등의 작업을 수행할 수 있습니다. `IsPost`값에 따라 페이지를 다르게 처리 하는 방법을 보여 주는 많은 예제가 나와 있습니다.

## <a name="a-simple-code-example"></a>간단한 코드 예제

이 절차에서는 기본 프로그래밍 기술을 보여 주는 페이지를 만드는 방법을 보여 줍니다. 이 예제에서는 사용자가 두 개의 숫자를 입력 하 고 그 결과를 추가 하 고 결과를 표시할 수 있는 페이지를 만듭니다.

1. 편집기에서 새 파일을 만들고 이름을 *Addnumbers. cshtml*로 추가 합니다.
2. 페이지에 이미 있는 항목을 대체 하 여 다음 코드와 태그를 페이지에 복사 합니다.  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    유의 해야 할 몇 가지 사항은 다음과 같습니다.

    - `@` 문자는 페이지에서 코드의 첫 번째 블록을 시작 하 고 페이지 아래쪽에 포함 된 `totalMessage` 변수 앞에 옵니다.
    - 페이지 맨 위에 있는 블록은 중괄호로 묶여 있습니다.
    - 위쪽의 블록에서 모든 줄은 세미콜론으로 끝납니다.
    - 변수 `total`, `num1`, `num2`및 `totalMessage`에는 여러 숫자와 문자열이 저장 됩니다.
    - `totalMessage` 변수에 할당 된 리터럴 문자열 값이 큰따옴표로 묶여 있습니다.
    - 코드는 대/소문자를 구분 하므로 `totalMessage` 변수를 페이지의 아래쪽 근처에 사용 하는 경우 해당 이름이 위쪽의 변수와 정확히 일치 해야 합니다.
    - 식 `num1.AsInt() + num2.AsInt()`는 개체 및 메서드를 사용 하는 방법을 보여 줍니다. 각 변수의 `AsInt` 메서드는 사용자가 입력 한 문자열을 숫자 (정수)로 변환 하 여 산술 연산을 수행할 수 있도록 합니다.
    - `<form>` 태그는 `method="post"` 특성을 포함 합니다. 이렇게 하면 사용자가 **추가**를 클릭 하면 HTTP POST 메서드를 사용 하 여 페이지가 서버에 전송 됩니다. 페이지가 제출 되 면 `if(IsPost)` 테스트가 true로 평가 되 고 조건부 코드가 실행 되어 숫자를 더한 결과를 표시 합니다.
3. 페이지를 저장 하 고 브라우저에서 실행 합니다. (파일을 실행 하기 전에 해당 페이지가 **파일** 작업 영역에서 선택 되어 있는지 확인 합니다.) 두 개의 정수를 입력 한 다음 **추가** 단추를 클릭 합니다. 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a>기본 프로그래밍 개념

이 문서에서는 ASP.NET 웹 프로그래밍에 대 한 개요를 제공 합니다. 가장 자주 사용 하는 프로그래밍 개념을 간략히 살펴보고 철저 하 게 조사 하는 것은 아닙니다. 심지어는 ASP.NET 웹 페이지을 시작 하는 데 필요한 거의 모든 것을 다룹니다.

하지만 첫 번째는 약간 기술적인 배경입니다.

### <a name="the-razor-syntax-server-code-and-aspnet"></a>Razor 구문, 서버 코드 및 ASP.NET

Razor 구문는 웹 페이지에 서버 기반 코드를 포함 하는 간단한 프로그래밍 구문입니다. Razor 구문를 사용 하는 웹 페이지에는 두 가지 종류의 콘텐츠, 즉 클라이언트 콘텐츠와 서버 코드가 있습니다. 클라이언트 콘텐츠는 HTML 태그 (요소), CSS와 같은 스타일 정보, JavaScript와 같은 일부 클라이언트 스크립트, 일반 텍스트 등의 웹 페이지에서 사용 하는 내용입니다.

Razor 구문를 사용 하 여이 클라이언트 콘텐츠에 서버 코드를 추가할 수 있습니다. 페이지에 서버 코드가 있으면 서버는 해당 코드를 먼저 실행 한 다음 페이지를 브라우저로 보냅니다. 서버에서를 실행 하는 경우 코드에서 서버 기반 데이터베이스에 액세스 하는 것과 같이 클라이언트 콘텐츠를 사용 하는 것 보다 복잡 한 작업을 수행할 수 있습니다. 가장 중요 한 점은 서버 코드에서 동적으로 클라이언트 &#8212; 콘텐츠를 만들 수 있으며, 즉석에서 HTML 태그나 기타 콘텐츠를 생성 한 다음 페이지에 포함 될 수 있는 정적 HTML과 함께 브라우저에 보낼 수 있습니다. 브라우저의 관점에서 보면 서버 코드에서 생성 되는 클라이언트 콘텐츠는 다른 클라이언트 콘텐츠와 다르지 않습니다. 앞서 살펴본 것 처럼 필요한 서버 코드는 매우 간단 합니다.

Razor 구문를 포함 하는 ASP.NET 웹 페이지에는 특수 한 파일 확장명 (cshtml *또는*)이 있습니다. 서버는 이러한 확장을 인식 하 고 Razor 구문 표시 된 코드를 실행 한 다음 페이지를 브라우저로 보냅니다.

### <a name="where-does-aspnet-fit-in"></a>ASP.NET는 어디에 있나요?

Razor 구문는 Microsoft에서 ASP.NET 이라는 기술을 기반으로 하며,이는 차례로 Microsoft .NET 프레임 워크를 기반으로 합니다. The.NET Framework는 거의 모든 종류의 컴퓨터 응용 프로그램을 개발 하기 위한 Microsoft의 대규모의 포괄적인 프로그래밍 프레임 워크입니다. ASP.NET는 웹 응용 프로그램을 만들기 위해 특별히 설계 된 .NET Framework의 일부입니다. 개발자는 ASP.NET를 사용 하 여 전 세계에서 가장 크고 트래픽이 많은 웹 사이트를 만들었습니다. 사이트에서 URL의 일부로 파일 이름 확장명 *.aspx* 가 표시 될 때마다 ASP.NET를 사용 하 여 사이트를 작성 한 것을 알 수 있습니다.

Razor 구문는 ASP.NET의 모든 기능을 제공 하지만 초보자 인 경우 더 쉽게 배울 수 있는 간소화 된 구문을 사용 하 여 생산성을 높여 줍니다. 이 구문을 사용 하는 것은 간단 하지만 ASP.NET 및 .NET Framework에 대 한 패밀리 관계는 웹 사이트가 더 정교 해지면 사용할 수 있는 더 큰 프레임 워크의 강력한 기능을 의미 합니다.

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> **클래스 및 인스턴스**
> 
> ASP.NET 서버 코드는 개체를 사용 하며,이는 클래스 개념을 기반으로 합니다. 클래스는 개체에 대 한 정의 또는 템플릿입니다. 예를 들어 응용 프로그램에는 고객 개체가 필요로 하는 속성과 메서드를 정의 하는 `Customer` 클래스가 포함 될 수 있습니다.
> 
> 응용 프로그램이 실제 고객 정보를 사용 해야 하는 경우 고객 개체의 인스턴스를 만듭니다 (또는 *인스턴스화*). 각 개별 고객은 `Customer` 클래스의 개별 인스턴스입니다. 모든 인스턴스는 동일한 속성 및 메서드를 지원 하지만 각 고객 개체는 고유 하기 때문에 각 인스턴스에 대 한 속성 값은 일반적으로 다릅니다. 한 고객 개체에서 `LastName` 속성은 "Smith" 일 수 있습니다. 다른 customer 개체에서 `LastName` 속성은 "Jones" 일 수 있습니다.
> 
> 마찬가지로, 사이트의 개별 웹 페이지는 `Page` 클래스 인스턴스인 `Page` 개체입니다. 페이지의 단추는 `Button` 클래스의 인스턴스인 `Button` 개체 등입니다. 각 인스턴스에는 고유한 특징이 있지만 모두 개체의 클래스 정의에 지정 된 항목을 기반으로 합니다.

## <a name="basic-syntax"></a>기본 구문

앞서 ASP.NET 웹 페이지 페이지를 만드는 방법의 기본 예제와 HTML 태그에 서버 코드를 추가 하는 방법을 살펴보았습니다. 여기서는 Razor 구문 &#8212; 프로그래밍 언어 규칙을 사용 하 여 ASP.NET 서버 코드를 작성 하는 기본 사항을 알아봅니다.

프로그래밍 경험이 있는 경우 (특히 C, C++, C#, Visual Basic 또는 JavaScript를 사용 하는 경우) 여기에서 읽는 많은 내용이 익숙할 것입니다. 서버 코드를 *. cshtml* 파일의 태그에 추가 하는 방법만 숙지 해야 합니다.

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a>코드 블록에서 텍스트, 태그 및 코드 결합

서버 코드 블록에서 텍스트 또는 태그 (또는 둘 다)를 페이지에 출력 하는 경우가 많습니다. 서버 코드 블록에 코드가 아닌 텍스트가 포함 되어 있는 경우 해당 텍스트를 그대로 렌더링 해야 하는 경우 ASP.NET는 해당 텍스트를 코드와 구별할 수 있어야 합니다. 다음과 같은 여러 가지 방법으로 이 작업을 수행할 수 있습니다.

- `<p></p>` 또는 `<em></em>`같은 HTML 요소로 텍스트를 묶습니다.   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    HTML 요소에는 텍스트, 추가 HTML 요소 및 서버 코드 식이 포함 될 수 있습니다. ASP.NET 여는 HTML 태그 (예: `<p>`)를 볼 때 요소와 해당 콘텐츠를 포함 하는 모든 항목을 브라우저에 그대로 렌더링 하 여 서버 코드 식이 이동 하는 것을 확인 합니다.
- `@:` 연산자 또는 `<text>` 요소를 사용 합니다. `@:`는 일반 텍스트 또는 일치 하지 않는 HTML 태그를 포함 하는 단일 내용의 줄을 출력 합니다. `<text>` 요소는 여러 줄을 출력으로 묶습니다. 이러한 옵션은 HTML 요소를 출력의 일부로 렌더링 하지 않으려는 경우에 유용 합니다.  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    여러 줄의 텍스트 또는 일치 하지 않는 HTML 태그를 출력 하려면 각 줄 앞에 `@:`를 사용 하거나 `<text>` 요소에 줄을 묶을 수 있습니다. `@:` 연산자와 마찬가지로`<text>` 태그는 ASP.NET에서 텍스트 콘텐츠를 식별 하는 데 사용 되며 페이지 출력에서 렌더링 되지 않습니다.

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    첫 번째 예제에서는 이전 예제를 반복 하지만 단일 쌍의 `<text>` 태그를 사용 하 여 렌더링할 텍스트를 묶습니다. 두 번째 예제에서 `<text>` 및 `</text>` 태그는 세 줄을 포함 하며, 모든 줄에는 포함 되지 않은 텍스트와 일치 하지 않는 HTML 태그 (`<br />`)가 서버 코드 및 일치 하는 HTML 태그와 함께 포함 됩니다. 또한 각 줄 앞에 `@:` 연산자를 사용 하 여 개별적으로 추가할 수 있습니다. 어떤 방법이 든 작동 합니다.

    > [!NOTE]
    > HTML 요소를 사용 하 여이 섹션 &#8212; 에 표시 된 대로 텍스트를 출력 하는 경우 `@:` 연산자 또는 `<text>` &#8212; 요소 ASP.NET은 출력을 html로 인코딩하지 않습니다. 앞에서 설명한 것 처럼 ASP.NET는이 섹션에 설명 된 특수 한 사례를 제외 하 고 `@`뒤에 오는 서버 코드 식과 서버 코드 블록의 출력을 인코딩합니다.

### <a name="whitespace"></a>Whitespace

문 (및 문자열 리터럴 외부)의 추가 공백은 문에 영향을 주지 않습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

문의 줄 바꿈은 문에 영향을 주지 않으며 가독성을 위해 문을 래핑할 수 있습니다. 다음 문은 동일합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

그러나 문자열 리터럴 중간에 줄을 줄 바꿈할 수는 없습니다. 다음 예는 작동 하지 않습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

위의 코드와 같이 여러 줄로 래핑하는 긴 문자열을 결합 하려면 두 가지 옵션이 있습니다. 연결 연산자 (`+`)를 사용할 수 있습니다 .이에 대해서는이 문서의 뒷부분에서 확인할 수 있습니다. 이 문서의 앞부분에서 살펴본 것 처럼 `@` 문자를 사용 하 여 축 자 문자열 리터럴을 만들 수도 있습니다. 약어 문자열 리터럴은 줄 전체로 나눌 수 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a>코드 및 태그 설명

주석을 사용 하 여 자신에 게 메모를 남길 수 있습니다. 또한 실행 하지 않으려는 코드 또는 태그 섹션을 사용 하지 않도록 설정 (*주석으로 처리*) 할 수 있지만 페이지에 유지 하려는 경우

Razor 코드 및 HTML 태그에 대 한 다양 한 주석 달기 구문이 있습니다. 모든 Razor 코드와 마찬가지로 페이지가 브라우저에 전송 되기 전에 서버에서 Razor 주석이 처리 된 후 제거 됩니다. 따라서 Razor 주석 구문을 사용 하면 파일을 편집할 때 볼 수 있는 코드 또는 태그에 주석을 추가할 수 있지만, 페이지 소스에도 표시 되지 않습니다.

ASP.NET Razor 주석의 경우 `@*`를 사용 하 여 주석을 시작 하 고 `*@`로 종료 합니다. 주석은 한 줄 또는 여러 줄에 있을 수 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

다음은 코드 블록 내의 주석입니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

다음은 코드 줄을 주석으로 처리 하 여 실행 되지 않도록 코드를 주석으로 처리 하는 것입니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

코드 블록 내에서 Razor 주석 구문을 사용 하는 대신 사용 중인 프로그래밍 언어의 주석 구문 (예 C#:)을 사용할 수 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

에서 C#한 줄로 된 주석에는 `//` 문자가 오고, 여러 줄 주석은 `/*`로 시작 하 고 `*/`로 끝납니다. Razor 주석과 마찬가지로 C# 주석은 브라우저에 렌더링 되지 않습니다.

태그에 대해 아시다시피 HTML 주석을 만들 수 있습니다.

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

HTML 주석은 `<!--` 문자로 시작 하 고 `-->`로 끝납니다. HTML 주석을 사용 하 여 텍스트 뿐만 아니라 페이지에 유지 하지만 렌더링 하지 않으려는 HTML 태그를 사용할 수 있습니다. 이 HTML 주석은 태그의 전체 내용과 여기에 포함 되는 텍스트를 숨깁니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

Razor 주석과 달리 HTML 주석은 페이지 *에 렌더링 되며* 사용자는 페이지 소스를 확인 하 여 볼 수 있습니다.

Razor에는의 C#중첩 된 블록에 대 한 제한이 있습니다. 자세한 내용은 [명명 된 변수 C# 및 중첩 블록에서 손상 된 코드 생성을](http://aspnetwebstack.codeplex.com/workitem/1914) 참조 하세요.

## <a name="variables"></a>변수

변수는 데이터를 저장 하는 데 사용 하는 명명 된 개체입니다. 변수 이름을 지정할 수 있지만 이름은 영문자로 시작 해야 하며 공백 또는 예약 문자를 포함할 수 없습니다.

### <a name="variables-and-data-types"></a>변수 및 데이터 형식

변수에는 변수에 저장 되는 데이터의 종류를 나타내는 특정 데이터 형식이 있을 수 있습니다. 문자열 값 (&quot;예: Hello 세계&quot;), 정수 값 (예: 3 또는 79)을 저장 하는 정수 변수, 날짜 값을 다양 한 형식 (예: 4/12/2012 또는 3 월 2009)으로 저장 하는 날짜 변수를 저장 하는 문자열 변수를 사용할 수 있습니다. 사용할 수 있는 다른 많은 데이터 형식이 있습니다.

그러나 일반적으로 변수의 형식을 지정할 필요가 없습니다. 대부분의 경우 ASP.NET는 변수의 데이터를 사용 하는 방법에 따라 형식을 파악할 수 있습니다. 때로는 형식을 지정 해야 합니다 .이 경우에는 예제가 표시 됩니다.

`var` 키워드 (형식을 지정 하지 않을 경우)를 사용 하거나 형식의 이름을 사용 하 여 변수를 선언 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

다음 예제에서는 웹 페이지에서 일반적으로 사용 되는 변수의 몇 가지를 보여 줍니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

페이지에서 이전 예제를 결합 하는 경우 브라우저에 표시 되는 것을 볼 수 있습니다.

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>데이터 형식 변환 및 테스트

ASP.NET는 일반적으로 데이터 형식을 자동으로 결정할 수 있지만 경우에 따라 자동으로 데이터 형식을 결정할 수는 없습니다. 따라서 명시적 변환을 수행 하 여 ASP.NET를 지원 해야 할 수 있습니다. 형식을 변환 하지 않아도 되는 경우에도 사용할 수 있는 데이터 형식을 테스트 하는 것이 도움이 될 수 있습니다.

가장 일반적인 경우는 문자열을 정수 또는 날짜와 같은 다른 형식으로 변환 해야 한다는 것입니다. 다음 예에서는 문자열을 숫자로 변환 해야 하는 일반적인 경우를 보여 줍니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

사용자 입력은 사용자가 문자열로 제공 됩니다. 사용자에 게 숫자를 입력 하 라는 메시지가 표시 되 고 숫자를 입력 한 경우에도 사용자 입력이 제출 되 고 코드에서이를 읽으면 데이터는 문자열 형식입니다. 따라서 문자열을 숫자로 변환 해야 합니다. 예를 들어 값을 변환 하지 않고 값에 대해 산술 연산을 수행 하려고 하면 ASP.NET에서 두 개의 문자열을 추가할 수 없기 때문에 다음과 같은 오류가 발생 합니다.

*' String ' 형식을 ' i n t '로 암시적으로 변환할 수 없습니다.*

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
    <strong>예</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    정수 값 (예: "593")을 나타내는 문자열을 정수로 변환 합니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
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
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>연산자

연산자는 식에서 수행할 명령의 종류를 ASP.NET 알려 주는 키워드 또는 문자입니다. 언어 C# (및이를 기반으로 하는 Razor 구문)는 많은 연산자를 지원 하지만 시작 하기 위해 몇 가지를 인식 하기만 하면 됩니다. 다음 표에서는 가장 일반적인 연산자를 요약 합니다.

:::row:::
    :::column:::
    <strong>Operator</strong>
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
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    숫자 식에 사용 되는 수학 연산자입니다.
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    할당. 문의 오른쪽에 있는 값을 좌 변에 있는 개체에 할당 합니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    같음 값이 같으면 `true`을 반환 합니다. `=` 연산자와 `==` 연산자의 차이를 확인 합니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    같지 않음 값이 같지 않으면 `true`을 반환 합니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    보다 작음, 보다 큼, 보다 작음, 작거나 같음, 크거나 같음.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    연결-문자열을 조인 하는 데 사용 됩니다. ASP.NET는이 연산자와 식의 데이터 형식에 따라 더하기 연산자의 차이를 알고 있습니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
    증가 및 감소 연산자-변수에서 1 (각각)을 더하거나 뺍니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    괄호. 식을 그룹화 하 고 메서드에 매개 변수를 전달 하는 데 사용 됩니다.
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    각괄호. 배열 또는 컬렉션의 값에 액세스 하는 데 사용 됩니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    나타내지. `true` 값을 반대로 `false` 하 고 그 반대의 경우도 마찬가지입니다. 일반적으로 `false` (즉, `true`)을 테스트 하는 간단한 방법으로 사용 됩니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&&` `||`
    :::column-end:::
    :::column:::
    논리적 AND 및 OR 이며 조건을 함께 연결 하는 데 사용 됩니다.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
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

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>가상 루트 참조: ~ operator 및 Href 메서드

*Cshtml* 또는 *vbhtml* 파일에서 `~` 연산자를 사용 하 여 가상 루트 경로를 참조할 수 있습니다. 이는 사이트에서 페이지를 이동할 수 있으며 다른 페이지에 포함 된 모든 링크가 손상 되지 않도록 하기 때문에 매우 편리 합니다. 웹 사이트를 다른 위치로 이동 하는 경우에도 유용 합니다. 다음은 몇 가지 예입니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

웹 사이트가 `http://myserver/myapp`경우 페이지가 실행 될 때 ASP.NET에서 이러한 경로를 처리 하는 방법은 다음과 같습니다.

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`

이러한 경로는 변수의 값으로 실제로 표시 되지 않지만 ASP.NET는 경로를 해당 하는 것 처럼 처리 합니다.

다음과 같이 서버 코드와 태그에서 모두 `~` 연산자를 사용할 수 있습니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

태그에서 `~` 연산자를 사용 하 여 이미지 파일, 다른 웹 페이지 및 CSS 파일과 같은 리소스에 대 한 경로를 만듭니다. 페이지가 실행 될 때 ASP.NET는 페이지 (코드 및 태그 모두)를 살펴보고 적절 한 경로에 대 한 모든 `~` 참조를 확인 합니다.

## <a name="conditional-logic-and-loops"></a>조건부 논리 및 루프

ASP.NET 서버 코드를 사용 하면 조건에 따라 작업을 수행 하 고 특정 횟수 (즉, 루프를 실행 하는 코드)에 문을 반복 하는 코드를 작성할 수 있습니다.

### <a name="testing-conditions"></a>테스트 조건

간단한 조건을 테스트 하려면 지정 하는 테스트에 따라 true 또는 false를 반환 하는 `if` 문을 사용 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

`if` 키워드는 블록을 시작 합니다. 실제 테스트 (조건)는 괄호 안에 있으며 true 또는 false를 반환 합니다. 테스트를 true로 설정 하는 경우 실행 되는 문은 중괄호로 묶여 있습니다. `if` 문은 조건이 false 인 경우 실행할 문을 지정 하는 `else` 블록을 포함할 수 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

`else if` 블록을 사용 하 여 여러 조건을 추가할 수 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

이 예에서는 if 블록의 첫 번째 조건이 true가 아닌 경우 `else if` 조건이 검사 됩니다. 이러한 조건이 충족 되 면 `else if` 블록의 문이 실행 됩니다. 조건을 충족 하는 조건이 없으면 `else` 블록의 문이 실행 됩니다. 원하는 수의 else if 블록을 추가한 다음 `else` 블록을 사용 하 여 다른 모든 항목을&quot; 조건에 &quot;수 있습니다.

많은 수의 조건을 테스트 하려면 `switch` 블록을 사용 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

테스트할 값은 괄호 안에 있습니다 (예: `weekday` 변수). 각 개별 테스트는 콜론으로 끝나는 `case` 문 (:)를 사용 합니다. `case` 문의 값이 테스트 값과 일치 하면 해당 case 블록의 코드가 실행 됩니다. `break` 문을 사용 하 여 각 case 문을 닫습니다. (각 `case` 블록에 중단을 포함 하는 것을 잊은 경우 다음 `case` 문의 코드도 실행 됩니다.) `switch` 블록에는 다른 모든 사례에 해당 하지 않는 경우 실행 되는 다른 모든 항목&quot; 옵션 &quot;에 대 한 마지막 사례로 `default` 문이 있는 경우가 많습니다.

브라우저에 표시 되는 마지막 두 조건부 블록의 결과입니다.

![Razor-Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a>반복 코드

동일한 문을 반복적으로 실행 해야 하는 경우가 많습니다. 이렇게 하려면 반복 합니다. 예를 들어 데이터 컬렉션의 각 항목에 대해 동일한 문을 실행 하는 경우가 많습니다. 반복 하려는 횟수를 정확히 알고 있는 경우 `for` 루프를 사용할 수 있습니다. 이러한 종류의 루프는 계산 하거나 계산 하는 데 특히 유용 합니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

루프는 `for` 키워드를 사용 하 여 시작 하 고, 괄호로 묶인 세 개의 문을 세미콜론으로 종료 합니다.

- 괄호 안에 첫 번째 문 (`var i=10;`)은 카운터를 만들고 10으로 초기화 합니다. 모든 변수를 사용할 수 `i` &#8212; 카운터의 이름을 지정할 필요가 없습니다. `for` 루프가 실행 되 면 카운터가 자동으로 증가 합니다.
- 두 번째 문 (`i < 21;`)은 계산 하려는 시간에 대 한 조건을 설정 합니다. 이 경우에는이 값을 최대 20 개까지 이동 하려고 합니다. 즉, 카운터가 21 보다 작은 경우 계속 진행 합니다.
- 세 번째 문 (`i++`)은 루프가 실행 될 때마다 카운터가 1을 추가 하도록 지정 하는 증분 연산자를 사용 합니다.

중괄호 안에는 루프가 반복 될 때마다 실행 되는 코드가 있습니다. 태그는 매번 새 단락 (`<p>` 요소)을 만들고 출력에 줄을 추가 하 여 `i` (카운터)의 값을 표시 합니다. 이 페이지를 실행 하는 경우이 예제에서는 출력을 표시 하는 11 개의 줄을 만들며 각 줄의 텍스트는 항목 번호를 나타냅니다.

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

컬렉션 또는 배열에 대 한 작업을 수행 하는 경우에는 종종 `foreach` 루프를 사용 합니다. 컬렉션은 유사한 개체의 그룹 이며, `foreach` 루프를 사용 하 여 컬렉션의 각 항목에 대 한 작업을 수행할 수 있습니다. 이 유형의 루프는 `for` 루프와 달리 카운터를 증가 시키거나 제한을 설정할 필요가 없기 때문에 컬렉션에 편리 합니다. 대신 `foreach` 루프 코드는 완료 될 때까지 컬렉션을 진행 합니다.

예를 들어 다음 코드는 웹 서버에 대 한 정보를 포함 하는 개체인 `Request.ServerVariables` 컬렉션의 항목을 반환 합니다. `foreac` h 루프를 사용 하 여 HTML 글머리 기호 목록에 새 `<li>` 요소를 만들어 각 항목의 이름을 표시 합니다.

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

`foreach` 키워드 뒤에는 컬렉션의 단일 항목을 나타내는 변수를 선언 하는 괄호 (예: `var item`)가 오고 그 뒤에 `in` 키워드가 오고 그 뒤에 반복 하려는 컬렉션이 나옵니다. `foreach` 루프의 본문에서 이전에 선언한 변수를 사용 하 여 현재 항목에 액세스할 수 있습니다.

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

보다 일반적인 용도의 루프를 만들려면 `while` 문을 사용 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

`while` 루프는 `while` 키워드로 시작 하 여 루프가 계속 되는 기간을 지정 하는 괄호 (`countNum`가 50 보다 작은 경우)로 시작 하 여 반복할 블록을 입력 합니다. 루프는 일반적으로 계산에 사용 되는 변수 또는 개체를 증가 (추가) 또는 감소 (빼기) 합니다. 예제에서 `+=` 연산자는 루프가 실행 될 때마다 `countNum`에 1을 추가 합니다. (에서 계산 되는 루프의 변수를 감소 시키려면 감소 연산자 `-=`)를 사용 합니다.

## <a name="objects-and-collections"></a>개체 및 컬렉션

ASP.NET 웹 사이트의 거의 모든 항목은 웹 페이지를 포함 하는 개체입니다. 이 섹션에서는 코드에서 자주 사용 하는 몇 가지 중요 한 개체에 대해 설명 합니다.

### <a name="page-objects"></a>Page 개체

ASP.NET의 가장 기본적인 개체는 페이지입니다. 정규화 된 개체 없이 페이지 개체의 속성에 직접 액세스할 수 있습니다. 다음 코드에서는 페이지의 `Request` 개체를 사용 하 여 페이지의 파일 경로를 가져옵니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

현재 페이지 개체의 속성 및 메서드를 참조 하 고 있음을 명확 하 게 하기 위해 선택적으로 `this` 키워드를 사용 하 여 코드의 페이지 개체를 나타낼 수 있습니다. 다음은 페이지를 나타내는 `this` 추가 된 이전 코드 예제입니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

`Page` 개체의 속성을 사용 하 여 다음과 같은 많은 정보를 얻을 수 있습니다.

- `Request`. 앞서 살펴본 것 처럼, 요청을 만든 브라우저의 유형, 페이지 URL, 사용자 id 등을 포함 하 여 현재 요청에 대 한 정보 컬렉션입니다.
- `Response`. 서버 코드의 실행이 완료 되 면 브라우저로 전송 되는 응답 (페이지)에 대 한 정보 컬렉션입니다. 예를 들어이 속성을 사용 하 여 응답에 정보를 쓸 수 있습니다. 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a>컬렉션 개체 (배열 및 사전)

*컬렉션* 은 데이터베이스의 `Customer` 개체 컬렉션과 같이 동일한 유형의 개체 그룹입니다. ASP.NET에는 `Request.Files` 컬렉션과 같은 여러 기본 제공 컬렉션이 포함 되어 있습니다.

컬렉션의 데이터로 작업 하는 경우가 많습니다. 두 가지 일반적인 컬렉션 형식은 *배열* 및 *사전*입니다. 배열은 비슷한 항목의 컬렉션을 저장 하지만 각 항목을 저장할 별도의 변수를 만들지 않으려는 경우에 유용 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

배열을 사용 하 여 `string`, `int`또는 `DateTime`와 같은 특정 데이터 형식을 선언 합니다. 변수에 배열이 포함 될 수 있음을 나타내려면 괄호를 선언에 추가 합니다 (예: `string[]` 또는 `int[]`). 해당 위치 (인덱스)를 사용 하거나 `foreach` 문을 사용 하 여 배열의 항목에 액세스할 수 있습니다. 배열 인덱스는 0부터 시작 &#8212; 합니다. 즉, 첫 번째 항목의 위치는 0이 고, 두 번째 항목은 위치 1에 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

`Length` 속성을 가져와서 배열의 항목 수를 확인할 수 있습니다. 배열에서 특정 항목의 위치를 가져오려면 (배열을 검색 하려면) `Array.IndexOf` 메서드를 사용 합니다. 배열의 콘텐츠를 반전 (`Array.Reverse` 메서드) 하거나 내용을 정렬 (`Array.Sort` 메서드) 하는 등의 작업을 수행할 수도 있습니다.

브라우저에 표시 되는 문자열 배열 코드의 출력입니다.

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

사전은 키 (또는 이름)를 제공 하 여 해당 값을 설정 하거나 검색할 수 있는 키/값 쌍의 컬렉션입니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

사전을 만들려면 `new` 키워드를 사용 하 여 새 사전 개체를 만들도록 지정 합니다. `var` 키워드를 사용 하 여 변수에 사전을 할당할 수 있습니다. 꺾쇠 괄호 (`< >`)를 사용 하 여 사전에 있는 항목의 데이터 형식을 표시 합니다. 선언 끝에 괄호 쌍을 추가 해야 합니다 .이는 실제로 새 사전을 만드는 메서드입니다.

사전에 항목을 추가 하려면 사전 변수의 `Add` 메서드 (이 경우`myScores`)를 호출한 다음 키와 값을 지정 하면 됩니다. 또는 다음 예제와 같이 대괄호를 사용 하 여 키를 나타내고 단순 할당을 수행할 수 있습니다.

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

사전에서 값을 가져오려면 대괄호 안에 키를 지정 합니다.

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a>매개 변수를 사용 하 여 메서드 호출

이 문서 앞부분에서 읽은 것 처럼를 사용 하 여 프로그래밍 하는 개체에는 메서드를 사용할 수 있습니다. 예를 들어 `Database` 개체에는 `Database.Connect` 메서드가 있을 수 있습니다. 또한 많은 메서드에 하나 이상의 매개 변수가 있습니다. *매개 변수* 는 메서드가 해당 작업을 완료할 수 있도록 메서드에 전달 하는 값입니다. 예를 들어 다음 세 개의 매개 변수를 사용 하는 `Request.MapPath` 메서드에 대 한 선언을 살펴보세요.

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

(줄은 더 쉽게 읽을 수 있도록 래핑됩니다. 따옴표로 묶인 문자열 내부를 제외 하 고 거의 모든 위치에 줄 바꿈을 넣을 수 있습니다.

이 메서드는 지정 된 가상 경로에 해당 하는 서버의 실제 경로를 반환 합니다. 메서드에 대 한 세 가지 매개 변수는 `virtualPath`, `baseVirtualDir`및 `allowCrossAppMapping`입니다. 선언에서 매개 변수는 허용 되는 데이터의 데이터 형식과 함께 나열 됩니다. 이 메서드를 호출 하는 경우 세 매개 변수 모두에 대 한 값을 제공 해야 합니다.

Razor 구문는 매개 변수를 메서드에 전달 하는 두 가지 옵션 ( *위치 매개 변수* 및 *명명 된 매개*변수)을 제공 합니다. 위치 매개 변수를 사용 하 여 메서드를 호출 하려면 메서드 선언에 지정 된 엄격한 순서로 매개 변수를 전달 합니다. (일반적으로 메서드의 설명서를 읽어이 순서를 확인 합니다.) 순서를 따라야 하 고 필요한 경우 매개 변수 &#8212; 를 건너뛸 수 없습니다. 값이 없는 위치 매개 변수에 대해 빈 문자열 (`""`) 또는 `null`를 전달 합니다.

다음 예제에서는 웹 사이트에 *scripts* 라는 폴더가 있다고 가정 합니다. 이 코드는 `Request.MapPath` 메서드를 호출 하 고 세 개의 매개 변수에 대 한 값을 올바른 순서로 전달 합니다. 그런 다음 결과 매핑된 경로를 표시 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

메서드에 매개 변수가 많은 경우 명명 된 매개 변수를 사용 하 여 코드를 더 읽기 쉽게 유지할 수 있습니다. 명명 된 매개 변수를 사용 하 여 메서드를 호출 하려면 매개 변수 이름 뒤에 콜론 (:), 값을 차례로 지정 합니다. 명명 된 매개 변수의 장점은 원하는 순서로 전달할 수 있다는 점입니다. 이는 메서드 호출이 압축 되지 않는다는 단점이 있습니다.

다음 예제에서는 위와 동일한 메서드를 호출 하지만 명명 된 매개 변수를 사용 하 여 값을 제공 합니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

여기에서 볼 수 있듯이 매개 변수는 다른 순서로 전달 됩니다. 그러나 이전 예제와이 예제를 실행 하면 동일한 값이 반환 됩니다.

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a>오류 처리

### <a name="try-catch-statements"></a>Try-catch 문

코드에 컨트롤 외부의 이유로 실패할 수 있는 문이 종종 있습니다. 예를 들면 다음과 같습니다.:

- 코드에서 파일을 만들거나 액세스 하려고 하면 모든 종류의 오류가 발생할 수 있습니다. 필요한 파일이 없거나, 잠겨 있거나, 코드에 권한이 없을 수 있습니다.
- 마찬가지로, 코드에서 데이터베이스의 레코드를 업데이트 하려고 시도 하는 경우에는 사용 권한 문제가 있을 수 있습니다. 데이터베이스에 대 한 연결이 삭제 될 수 있습니다. 저장할 데이터가 유효 하지 않을 수 있습니다.

프로그래밍 측면에서 이러한 상황을 *예외*라고 합니다. 코드에서 예외가 발생 하는 경우 사용자에 게 가장 잘 방해가 되는 오류 메시지를 생성 (throw) 합니다.

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

코드에 예외가 발생할 수 있는 상황에서이 유형의 오류 메시지를 방지 하기 위해 `try/catch` 문을 사용할 수 있습니다. `try` 문에서 확인 중인 코드를 실행 합니다. 하나 이상의 `catch` 문에서 발생 했을 수 있는 특정 오류 (특정 유형의 예외)를 찾을 수 있습니다. 예상 되는 오류를 찾기 위해 필요한 만큼 `catch` 문을 포함할 수 있습니다.

> [!NOTE]
> `try/catch` 문에서는 `Response.Redirect` 메서드를 사용 하지 않는 것이 좋습니다 .이는 페이지에서 예외를 발생 시킬 수 있기 때문입니다.

다음 예에서는 첫 번째 요청에서 텍스트 파일을 만든 다음 사용자가 파일을 열 수 있도록 하는 단추를 표시 하는 페이지를 보여 줍니다. 이 예제에서는 예외를 발생 시 키 지 않도록 의도적으로 잘못 된 파일 이름을 사용 합니다. 이 코드에는 두 가지 예외에 대 한 `catch` 문이 포함 되어 있습니다. `FileNotFoundException`는 파일 이름이 잘못 된 경우에 발생 하는 것이 고, ASP.NET에서 폴더를 찾을 수 없는 경우에 발생 하는 `DirectoryNotFoundException`입니다. (모든 것이 제대로 작동 하는 경우 실행 되는 방식을 확인 하기 위해 예제에서 문의 주석 처리를 제거할 수 있습니다.)

코드에서 예외를 처리 하지 않은 경우 이전 스크린샷과 같은 오류 페이지가 표시 됩니다. 그러나 `try/catch` 섹션을 사용 하면 사용자가 이러한 유형의 오류를 볼 수 있습니다.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a>추가 리소스

**Visual Basic를 사용한 프로그래밍**

[부록: Visual Basic 언어 및 구문](https://go.microsoft.com/fwlink/?LinkId=202908)

**참조 설명서**

[ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)

[C#언어도](https://msdn.microsoft.com/library/kx37x362.aspx)
