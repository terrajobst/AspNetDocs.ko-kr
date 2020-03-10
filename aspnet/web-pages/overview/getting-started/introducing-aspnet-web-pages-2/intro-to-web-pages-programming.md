---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: ASP.NET 웹 페이지 프로그래밍 기본 사항 소개 | Microsoft Docs
author: Rick-Anderson
description: "이 자습서에서는 Razor 구문를 사용 하 여 ASP.NET 웹 페이지에서 프로그래밍 하는 방법에 대 한 개요를 제공 합니다. 학습 내용: pr에 사용 하는 기본 ' Razor ' 구문"
ms.author: riande
ms.date: 06/17/2015
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 474de7671ac2931e5ba9ff635d77385403644521
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78509981"
---
# <a name="introducing-aspnet-web-pages---programming-basics"></a>ASP.NET 웹 페이지 프로그래밍 기본 사항 소개

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 Razor 구문를 사용 하 여 ASP.NET 웹 페이지에서 프로그래밍 하는 방법에 대 한 개요를 제공 합니다.
> 
> 학습할 내용:
> 
> - ASP.NET 웹 페이지에서 프로그래밍 하는 데 사용 하는 기본 "Razor" 구문입니다.
> - 사용할 프로그래밍 C#언어인 몇 가지 기본 사항입니다.
> - 웹 페이지에 대 한 몇 가지 기본적인 프로그래밍 개념.
> - 사이트에서 사용할 패키지 (미리 작성 된 코드를 포함 하는 구성 요소)를 설치 하는 방법
> - *도우미* 를 사용 하 여 일반적인 프로그래밍 작업을 수행 하는 방법입니다.
>   
> 
> 설명 하는 기능/기술:
> 
> - NuGet 및 패키지 관리자
> - `Gravatar` 도우미입니다.

이 자습서는 주로 ASP.NET 웹 페이지에 사용할 프로그래밍 구문을 소개 하는 연습입니다. 프로그래밍 언어로 작성 된 코드 Razor 구문 및 코드에 대해 알아봅니다. C# 이전 자습서에서이 구문을 잠깐 살펴볼 수 있습니다. 이 자습서에서는 구문에 대해 자세히 설명 합니다.

이 자습서에는 단일 자습서에서 볼 수 있는 가장 많은 프로그래밍이 포함 되어 있으며 프로그래밍에 *만* 해당 되는 유일한 자습서가 포함 되어 있습니다. 이 집합의 나머지 자습서에서는 실제로 흥미로운 작업을 수행 하는 페이지를 만듭니다.

또한 *도우미*에 대해 알아봅니다. 도우미는 페이지에 추가할 수 있는 패키지 된 코드 조각입니다. 도우미는 작업을 수행 하는 것이 좋습니다. 그렇지 않으면 수동 작업을 수행할 수 있습니다.

## <a name="creating-a-page-to-play-with-razor"></a>Razor로 재생할 페이지 만들기

이 섹션에서는 기본 구문에 대 한 의미를 얻을 수 있도록 Razor를 사용 하 여 재생 합니다.

아직 실행 중이 아닌 경우 WebMatrix를 시작 합니다. 이전 자습서에서 만든 웹 사이트 ([웹 페이지 시작](https://go.microsoft.com/fwlink/?LinkId=251578))를 사용 합니다. 다시 열려면 **내 사이트** 를 클릭 하 고 **WebPageMovies**를 선택 합니다.

![열려 있는 사이트 옵션 및 내 사이트를 강조 표시 하는 WebMatrix 시작 화면](intro-to-web-pages-programming/_static/image1.png)

**파일** 작업 영역을 선택 합니다.

리본에서 **새로** 만들기를 클릭 하 여 페이지를 만듭니다. **CSHTML** 를 선택 하 고 새 페이지의 이름을 *TestRazor*로 선택 합니다.

**확인**을 클릭합니다.

다음을 파일에 복사 하 여 이미 있는 항목을 완전히 바꿉니다.

> [!NOTE]
> 예제에서 코드 또는 태그를 페이지로 복사할 때 들여쓰기와 맞춤이 자습서의 경우와 다를 수 있습니다. 그러나 들여쓰기 및 맞춤은 코드가 실행 되는 방법에는 영향을 주지 않습니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a>예제 페이지 검사

표시 되는 대부분은 일반 HTML입니다. 그러나 맨 위에는 다음 코드 블록이 있습니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

이 코드 블록에 대해 다음 사항을 확인 합니다.

- @ 문자는 다음 항목이 HTML이 아닌 Razor 코드 ASP.NET 나타냅니다. ASP.NET는 다시 일부 HTML로 실행 될 때까지 @ 문자 이후의 모든 항목을 코드로 처리 합니다. (이 경우 &lt;! DOCTYPE&gt; 요소입니다.
- 중괄호 ({및})는 코드에 두 줄이 둘 이상 있는 경우 Razor 코드 블록을 묶습니다. 중괄호는 해당 블록의 코드를 시작 하 고 ASP.NET는 위치를 알려 줍니다.
- //문자는 주석을 표시 합니다. 즉, 실행 되지 않는 코드의 일부입니다.
- 각 문은 세미콜론 (;)로 끝나야 합니다. (그러나 주석이 아님)
- Var 키워드를 사용 하 여 생성 (*선언*) 하는 *변수에*값을 저장할 수 있습니다. 변수를 만들 때 이름을 지정 합니다. 여기에는 문자, 숫자 및 밑줄 (\_)이 포함 될 수 있습니다. 변수 이름은 숫자로 시작할 수 없으며, 프로그래밍 키워드 (예: var)의 이름을 사용할 수 없습니다.
- 문자열 (예: "ASP.NET" 및 "웹 페이지")을 큰따옴표로 묶습니다. 큰따옴표 여야 합니다. 숫자는 따옴표로 묶지 않습니다.
- 따옴표를 벗어난 공백은 중요 하지 않습니다. 줄 바꿈은 주로 중요 하지 않습니다. 단, 문자열을 따옴표로 묶지 않아도 됩니다. 들여쓰기와 맞춤이 중요 하지 않습니다.

이 예제에서 알 수 없는 모든 코드는 대/소문자를 구분 합니다. 즉, m 변수는 이름이 be um 또는 be um 일 수 있는 변수와 다른 변수 임을 의미 합니다. 마찬가지로 var은 키워드 이지만 Var은 그렇지 않습니다.

### <a name="objects-and-properties-and-methods"></a>개체 및 속성 및 메서드

이제 날짜/시간 식이 있습니다. 간단히 말해 DateTime은 *개체*입니다. 개체는 페이지, 텍스트 상자, 파일, 이미지, 웹 요청, 전자 메일 메시지, 고객 레코드 등을 사용 하 여 프로그래밍할 수 있는 것입니다. 개체에는 특성을 설명 하는 하나 이상의 *속성이* 있습니다. 텍스트 상자 개체에는 텍스트 속성이 있고, 요청 개체에는 Url 속성 (및 기타)이 있고, 메일 메시지에는 From 속성과 To 속성 등이 있습니다. 개체에는 수행할 수 있는 "동사"에 해당 하는 *메서드도* 있습니다. 개체를 많이 사용 하 게 됩니다.

예제에서 볼 수 있듯이 DateTime은 날짜와 시간을 프로그래밍할 수 있게 해 주는 개체입니다. 현재 날짜 및 시간을 반환 하는 라는 속성이 있습니다.

### <a name="using-code-to-render-markup-in-the-page"></a>코드를 사용 하 여 페이지에서 태그 렌더링

페이지 본문에서 다음을 확인 합니다.

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

다시 말해, @ 문자는 다음 항목이 HTML이 아닌 코드 ASP.NET 알려 줍니다. 태그에서 @ 다음에 코드 식을 추가 하면 ASP.NET가 해당 지점에서 바로 해당 식의 값을 렌더링 합니다. 이 예제에서 @a @product는 이름이 a 인 변수의 값을 렌더링 하 고,는 product 라는 변수에 있는 항목을 렌더링 하는 등의 모든 것을 렌더링 합니다.

하지만 변수로 국한 되지 않습니다. 여기에서 @ 문자는 식 앞에와 야 합니다.

- @ (a\*b)는 변수 a와 b에 있는 모든 항목의 곱을 렌더링 합니다. \* 연산자는 곱하기를 의미 합니다.
- @ (기술 + "" + 제품)은 변수 기술 및 제품을 연결 하 고 사이에 공백을 추가 하 여 값을 렌더링 합니다. 문자열을 연결 하기 위한 연산자 (+)는 숫자를 더하는 연산자와 동일 합니다. ASP.NET는 일반적으로 숫자나 문자열로 작업 하 고 있는지 여부를 알 수 있으며 + 연산자를 사용 하 여 적절 한 작업을 수행 합니다.
- @Request.Url는 Request 개체의 Url 속성을 렌더링 합니다. 요청 개체는 브라우저의 현재 요청에 대 한 정보를 포함 하며, 물론 Url 속성에는 현재 요청의 URL이 포함 됩니다.

또한이 예제는 다양 한 방법으로 작업을 수행할 수 있음을 보여 주기 위해 설계 되었습니다. 위쪽의 코드 블록에서 계산을 수행 하 고, 결과를 변수에 넣고, 변수를 태그에 렌더링할 수 있습니다. 또는 태그에서 바로 식에서 계산을 수행할 수 있습니다. 사용 하는 방법은 사용자의 기본 설정에 따라 수행 하는 작업 및 일부 범위에 따라 다릅니다.

### <a name="seeing-the-code-in-action"></a>작업 중인 코드 보기

파일 이름을 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서 시작**을 선택 합니다. 페이지에서 확인 된 모든 값과 식이 있는 브라우저에 페이지가 표시 됩니다.

![브라우저에서 ' TestRazor ' 페이지가 실행 되 고 있습니다.](intro-to-web-pages-programming/_static/image2.png)

브라우저에서 소스를 확인 합니다.

![브라우저의 ' Razor 테스트 ' 페이지 소스](intro-to-web-pages-programming/_static/image3.png)

이전 자습서의 경험에서 짐작할 수 있듯이, 페이지에 Razor 코드가 없습니다. 실제 표시 값이 표시 됩니다. 페이지를 실행 하는 경우에는 WebMatrix에 기본 제공 되는 웹 서버에 대 한 요청을 실제로 수행 하 게 됩니다. 요청이 수신 되 면 ASP.NET는 모든 값과 식을 확인 하 고 해당 값을 페이지에 렌더링 합니다. 그런 다음 페이지를 브라우저로 보냅니다.

> [!TIP] 
> 
> **Razor 및C#**
> 
> 지금까지 Razor 구문 작업 하 고 있습니다. 이것은 사실 이지만 전체 스토리가 아닙니다. 사용 중인 실제 프로그래밍 언어가 호출 *C#* 됩니다. C#는 Microsoft에서 10 년 전에 만들어졌으며 Windows 앱을 만들기 위한 기본 프로그래밍 언어 중 하나가 되었습니다. 변수 이름 및 문을 만드는 방법에 대해 살펴본 모든 규칙은 실제로 C# 언어의 모든 규칙입니다.
> 
> Razor는이 코드를 페이지에 포함 하는 방법에 대 한 간단한 규칙 집합을 더 구체적으로 지칭 합니다. 예를 들어 @을 사용 하 여 페이지에 코드를 표시 하 고 @ {}를 사용 하 여 코드 블록을 포함 하는 규칙은 페이지의 Razor 측면입니다. 또한 도우미는 Razor의 일부로 간주 됩니다. Razor 구문은 ASP.NET 웹 페이지 뿐만 아니라 더 많은 위치에서 사용 됩니다. 예를 들어 ASP.NET MVC 뷰에서만 사용 됩니다.
> 
> 프로그래밍 ASP.NET 웹 페이지에 대 한 정보를 찾는 경우 Razor에 대 한 많은 참조를 찾을 수 있기 때문에이를 언급 합니다. 그러나 이러한 참조는 많이 수행 하는 작업에는 적용 되지 않으므로 혼동 될 수 있습니다. 실제로 대부분의 프로그래밍 질문은 ASP.NET를 사용 C# 하거나 작업 하는 것에 대 한 것입니다. 따라서 Razor에 대 한 정보를 구체적으로 살펴보면 필요한 답을 찾지 못할 수 있습니다.

## <a name="adding-some-conditional-logic"></a>일부 조건부 논리 추가

페이지에서 코드를 사용 하는 방법에 대 한 유용한 기능 중 하나는 다양 한 조건에 따라 수행 되는 작업을 변경할 수 있다는 것입니다. 자습서의이 부분에서는 페이지에 표시 되는 내용을 변경 하는 몇 가지 방법에 대해 살펴봅니다.

이 예제는 단순 하 고 약간 거리가 조건부 논리에 집중할 수 있습니다. 만들 페이지는 다음과 같습니다.

- 페이지가 처음 표시 될 때 또는 페이지를 전송 하는 단추를 클릭 했는지 여부에 따라 페이지에 다른 텍스트를 표시 합니다. 첫 번째 조건부 테스트가 될 것입니다.
- URL의 쿼리 문자열에 특정 값이 전달 된 경우에만 메시지를 표시 합니다 (http://...? show = true). 이는 두 번째 조건 테스트입니다.

WebMatrix에서 페이지를 만들고 이름을 *TestRazorPart2*로 다시 만듭니다. 리본에서 **새로 만들기**를 클릭 하 고, **CSHTML**를 선택 하 고, 파일 이름을로 지정한 다음 **확인**을 클릭 합니다.

해당 페이지의 내용을 다음과 같이 바꿉니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

위쪽의 코드 블록은 일부 텍스트를 사용 하 여 message 라는 변수를 초기화 합니다. 페이지 본문에서 메시지 변수의 내용은 &lt;p&gt; 요소 내에 표시 됩니다. 태그에는 **제출** 단추를 만들기 위한 &lt;입력&gt; 요소도 포함 됩니다.

이제 페이지를 실행 하 여 작동 방식을 확인 합니다. 지금은 **제출** 단추를 클릭 하는 경우에도 기본적으로 정적 페이지가 됩니다.

WebMatrix로 돌아갑니다. 코드 블록 내에서 메시지를 초기화 하는 줄 *뒤* 에 다음 강조 표시 된 코드를 추가 합니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a>If {} 블록

방금 추가한 항목은 if 조건 이었습니다. 코드에서 if 조건의 구조는 다음과 같습니다.

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

테스트할 조건이 괄호 안에 있습니다. 값 이거나 true 또는 false를 반환 하는 식 이어야 합니다. 조건이 true 이면 ASP.NET는 중괄호 안에 있는 문을 실행 합니다. (Then 논리의 *다음* 부분입니다. ) 조건이 false 이면 코드 블록을 건너뜁니다.

If 문에서 테스트할 수 있는 조건의 몇 가지 예는 다음과 같습니다.

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

*논리 연산자* 또는 *비교 연산자*(같음 (= =), 보다 큼 (&gt;), 보다 작음 (&lt;), 크거나 같음 (&gt;=), 작거나 같음 (&lt;=)을 사용 하 여 변수를 값 이나 식에 대해 테스트할 수 있습니다. ! = 연산자는와 같지 않습니다. 예를 들어 (a! = 0)은가 *0과 같지*않음을 의미 합니다.

> [!NOTE]
> 같음 (= =)의 비교 연산자가 =와 같지 않은지 확인 합니다. = 연산자는 값을 할당 하는 데만 사용 됩니다 (var a = 2). 이러한 연산자를 함께 사용할 경우 오류가 발생 하거나 이상한 결과를 얻을 수 있습니다.

항목이 true 인지 여부를 테스트 하기 위해 전체 구문은 if (IsDone = = true)입니다. 그러나 (IsDone) 인 경우 바로 가기를 사용할 수도 있습니다. 비교 연산자가 없는 경우 ASP.NET는 true를 테스트 하는 것으로 가정 합니다.

! 연산자는 연산자 자체는 논리적 NOT을 의미 합니다. 예를 들어 조건 (! IsPost) *는 IsPost이 true가*아님을 의미 합니다.

논리적 AND (&amp;&amp; 연산자) 또는 논리적 OR (| | 연산자)를 사용 하 여 조건을 조합할 수 있습니다. 예를 들어 앞의 예에 있는 if 조건의 마지막은 *FileProcessingIsDone가 true로 설정 되어 있지 않고 displayMessage가 false로 설정*되어 있음을 의미 합니다.

### <a name="the-else-block"></a>Else 블록

If 블록에 대 한 마지막 한 가지 사항은 if 블록 뒤에 else 블록이 올 수 있습니다. Else 블록은 조건이 false 인 경우 다른 코드를 실행 해야 하는 경우에 유용 합니다. 간단한 예는 다음과 같습니다.

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

이 시리즈의 이후 자습서에서는 else 블록을 사용 하는 것이 유용한 몇 가지 예를 확인할 수 있습니다.

### <a name="testing-whether-the-request-is-a-submit-post"></a>요청이 제출 (post) 인지 테스트

더 많은 사항이 있지만 if (IsPost) {...} 조건이 있는 예제로 돌아갑니다. IsPost는 실제로 현재 페이지의 속성입니다. 페이지가 처음 요청 될 때 IsPost는 false를 반환 합니다. 그러나 단추를 클릭 하거나 페이지를 제출 하는 경우 (즉, IsPost는 true를 반환 합니다.) 따라서 IsPost를 사용 하 여 양식 제출을 처리 하 고 있는지 여부를 확인할 수 있습니다. HTTP 동사를 기준으로 요청이 GET 작업 인 경우 IsPost는 false를 반환 합니다. 요청이 POST 작업 인 경우 IsPost는 true를 반환 합니다. 이후 자습서에서는이 테스트가 특히 유용 하 게 사용 되는 입력 폼을 사용 합니다.

페이지를 실행 합니다. 페이지를 처음 요청 했으므로 "페이지를 처음 요청 했습니다" 라는 메시지가 표시 됩니다. 이 문자열은 메시지 변수를 초기화 한 값입니다. If (IsPost) 테스트가 있지만 지금은 false를 반환 하므로 if 블록 내의 코드는 실행 되지 않습니다.

**제출** 단추를 클릭 합니다. 페이지를 다시 요청 합니다. 이전 처럼 메시지 변수는 "This is first time ..."로 설정 됩니다. 그러나 이번에는 (IsPost)가 true를 반환 하 여 if 블록 내의 코드가 실행 되도록 테스트 합니다. 이 코드는 메시지 변수의 값을 다른 값으로 변경 합니다 .이 값은 태그에서 렌더링 됩니다.

이제 태그에 if 조건을 추가 합니다. **제출** 단추를 포함 하는 &lt;p&gt; 요소 아래에 다음 태그를 추가 합니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

태그 내부에 코드를 추가 하 여 @시작 해야 합니다. 그런 다음 코드 블록에서 이전에 추가한 것과 유사한 if 테스트가 있습니다. 그러나 중괄호 안에는 일반 HTML을 추가 하는 것이 좋습니다 .이는 최소한 @DateTime.Now될 때까지 일반적입니다. 이는 약간 약간 약간의 Razor 코드 이므로 다시 앞에 @를 추가 해야 합니다.

여기에서 요소는 위쪽 및 태그의 코드 블록에 if 조건을 추가할 수 있습니다. 페이지 본문에서 if 조건을 사용 하는 경우 블록 내부의 줄은 태그 또는 코드 일 수 있습니다. 이 경우와 as는 태그와 코드를 혼합할 때마다 true를 사용 하 여 코드의 위치를 ASP.NET 명확 하 게 만들어야 합니다.

페이지를 실행 하 고 **제출**을 클릭 합니다. 이번에는 제출할 때 다른 메시지 ("지금 전송 했습니다.")를 볼 수 있을 뿐 아니라 날짜 및 시간을 나열 하는 새 메시지가 표시 됩니다.

![제출 후 표시 되는 타임 스탬프를 사용 하 여 브라우저에서 실행 중인 ' 테스트 Razor 2 ' 페이지](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a>쿼리 문자열의 값 테스트

하나 이상의 테스트. 이번에는 쿼리 문자열에 전달 될 수 있는 show 라는 값을 테스트 하는 if 블록을 추가 합니다. (예: `http://localhost:43097/TestRazorPart2.cshtml?show=true`) 표시의 값이 true 인 경우에만 표시 되는 메시지를 표시 하도록 페이지를 변경 합니다 ("This is first ..." 등).

페이지 맨 위에 있는 코드 블록의 맨 아래에 다음을 추가 합니다.

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

이제 전체 코드 블록은 다음 예제와 같습니다. (페이지에 코드를 복사 하는 경우 들여쓰기가 다를 수 있습니다. 그러나 코드가 실행 되는 방식에는 영향을 주지 않습니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

블록의 새 코드는 showMessage 라는 변수를 false로 초기화 합니다. 그런 다음 if 테스트를 수행 하 여 쿼리 문자열에서 값을 찾습니다. 페이지를 처음 요청할 때이 페이지에는 다음과 같은 URL이 있습니다.

`http://localhost:43097/TestRazorPart2.cshtml`

이 코드는 url에 다음과 같이 쿼리 문자열에 show 라는 변수가 포함 되어 있는지 여부를 확인 합니다.

`http://localhost:43097/TestRazorPart2.cshtml`? show = true

테스트 자체는 Request 개체의 QueryString 속성을 살펴봅니다. 쿼리 문자열에 show 라는 항목이 포함 되어 있고 해당 항목이 true로 설정 된 경우 if 블록이 실행 되 고 showMessage 변수가 true로 설정 됩니다.

여기에서 볼 수 있듯이 트릭은 여기에 있습니다. 이름 처럼 쿼리 문자열은 문자열입니다. 그러나 테스트 하는 값이 부울 (true/false) 값인 경우에만 true 및 false를 테스트할 수 있습니다. 쿼리 문자열에서 show 변수의 값을 테스트 하려면 먼저이를 부울 값으로 변환 해야 합니다. AsBool 메서드에서는 문자열을 입력으로 사용 하 고이를 부울 값으로 변환 합니다. 분명히, 문자열이 "true" 이면 AsBool 메서드는 해당 값을 true로 변환 합니다. 문자열의 값이 다른 값 이면 AsBool은 false를 반환 합니다.

> [!TIP] 
> 
> **데이터 형식 및 As () 메서드**
> 
> 지금까지 변수를 만들 때 var 키워드를 사용 합니다. 그러나 전체 스토리가 아닙니다. 값을 조작 하기 위해 숫자를 추가 하거나, 문자열을 연결 하거나, 날짜를 비교 하거나, true/false를 테스트 C# 하기 위해는 값의 적절 한 내부 표현을 사용 해야 합니다. C#는 *일반적으로* 값을 사용 하 여 수행 하는 작업을 기반으로 하는 표현 (즉, 데이터의 *형식* )을 파악할 수 있습니다. 그러나 이제는 그렇게 할 수 없습니다. 그렇지 않은 경우 데이터를 표시 하는 방법을 C# 명시적으로 지정 하 여 도움을 받아야 합니다. AsBool 메서드는 문자열 값 "true" C# 또는 "false"를 부울 값으로 처리 하도록 지시 합니다. AsInt (정수로 처리), Asint (날짜/시간으로 처리), Asint (부동 소수점 숫자로 처리) 등의 다른 형식으로도 문자열을 나타내는 유사한 메서드가 있습니다. 이러한 As () 메서드를 사용 하는 경우 C# 요청 된 대로 문자열 값을 표현할 수 없는 경우 오류가 표시 됩니다.

페이지의 태그에서이 요소를 제거 하거나 주석으로 처리 합니다 (주석으로 표시 됨).

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

해당 텍스트를 제거 하거나 주석으로 처리 한 후에 다음을 추가 합니다.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

If 테스트는 showMessage 변수가 true 인 경우 메시지 변수의 값을 사용 하 여 &lt;p&gt; 요소를 렌더링 합니다.

### <a name="summary-of-your-conditional-logic"></a>조건부 논리 요약

방금 수행한 작업을 완전히 잘 모르는 경우에는 다음 요약을 참조 하세요.

- 메시지 변수는 기본 문자열 ("This is first time ...")으로 초기화 됩니다.
- 페이지 요청이 제출 (post)의 결과인 경우 메시지의 값이 "이제 제출 했습니다 ..."로 변경 됩니다.
- ShowMessage 변수가 false로 초기화 됩니다.
- 쿼리 문자열에? show = true가 포함 되어 있으면 showMessage 변수가 true로 설정 됩니다.
- 태그에서 showMessage가 true 이면 메시지의 값을 표시 하는 &lt;p&gt; 요소가 렌더링 됩니다. ShowMessage가 false 이면 태그의 해당 지점에서 아무것도 렌더링 되지 않습니다.
- 태그에서 요청이 post 이면 날짜 및 시간을 표시 하는 &lt;p&gt; 요소가 렌더링 됩니다.

페이지를 실행 합니다. ShowMessage가 false 이기 때문에 메시지는 표시 되지 않으므로 태그에서 if (showMessage) 테스트는 false를 반환 합니다.

**제출**을 클릭합니다. 날짜 및 시간이 표시 되지만 여전히 메시지는 표시 되지 않습니다.

브라우저에서 URL 상자로 이동 하 여? show = true URL의 끝에 다음을 추가 하 고 Enter 키를 누릅니다.

![쿼리 문자열을 보여 주는 브라우저의 ' Razor 2 테스트 ' 페이지](intro-to-web-pages-programming/_static/image5.png)

페이지가 다시 표시 됩니다. URL을 변경 했기 때문에이 요청은 전송이 아닌 새 요청입니다. **제출을** 다시 클릭 합니다. 이 메시지는 날짜 및 시간과 마찬가지로 다시 표시 됩니다.

![쿼리 문자열이 있을 때 전송 후 ' Razor 2 테스트 ' 페이지](intro-to-web-pages-programming/_static/image6.png)

URL에서? show = true to? show = false를 선택 하 고 Enter 키를 누릅니다. 페이지를 다시 제출 합니다. 페이지가 시작 된 방법으로 돌아갑니다 (메시지 없음).

앞에서 설명한 것 처럼이 예제의 논리는 약간 거리가. 그러나가 많은 페이지에서 제공 되는 경우 여기에 표시 된 하나 이상의 양식을 사용 합니다.

## <a name="installing-a-helper-displaying-a-gravatar-image"></a>도우미 설치 (Gravatar 이미지 표시)

사용자가 웹 페이지에서 자주 수행 하려는 일부 작업에는 많은 코드가 필요 하거나 추가 정보가 필요 합니다. 예: 데이터 차트 표시 페이지에 Facebook "좋아요" 단추 배치 웹 사이트에서 전자 메일 보내기 이미지 자르기 또는 크기 조정 사이트에 PayPal을 사용 합니다. 이러한 종류의 작업을 쉽게 수행할 수 있도록 ASP.NET 웹 페이지 *도우미*를 사용할 수 있습니다. 도우미는 사이트에 대해 설치 하 고 몇 줄의 Razor 코드만 사용 하 여 일반적인 작업을 수행할 수 있도록 하는 구성 요소입니다.

ASP.NET 웹 페이지에는 몇 가지 도우미가 내장 되어 있습니다. 그러나 NuGet 패키지 관리자를 사용 하 여 제공 되는 패키지 (추가 기능)에서 많은 도우미를 사용할 수 있습니다. NuGet을 사용 하면 설치할 패키지를 선택한 다음 설치의 모든 세부 정보를 처리할 수 있습니다.

자습서의이 부분에서는 Gravatar ("전역적으로 인식 된 아바타") 이미지를 표시할 수 있는 도우미를 설치 합니다. 두 가지 사항을 배우게 됩니다. 하나는 도우미를 찾고 설치 하는 방법입니다. 도우미를 사용 하 여 사용자가 직접 작성 해야 하는 많은 코드를 사용 하 여 수행 해야 하는 작업을 쉽게 수행할 수도 있습니다.

[http://www.gravatar.com/](http://www.gravatar.com/)의 Gravatar 웹 사이트에서 자신의 Gravatar를 등록할 수 있지만 자습서의이 부분을 수행 하기 위해 Gravatar 계정을 만드는 것은 중요 하지 않습니다.

WebMatrix에서 **NuGet** 단추를 클릭 합니다.

![WebMatrix의 NuGet 갤러리 대화 상자](intro-to-web-pages-programming/_static/image7.png)

NuGet 패키지 관리자를 시작 하 고 사용 가능한 패키지를 표시 합니다. 일부 패키지는 도우미가 아닙니다. 일부는 WebMatrix 자체에 기능을 추가 하 고, 일부는 추가 템플릿 등을 추가 합니다. 버전 비호환에 대 한 오류 메시지를 받을 수 있습니다. **확인** 을 클릭 하 여이 오류 메시지를 무시 하 고이 자습서를 계속 진행할 수 있습니다.

![WebMatrix의 NuGet 갤러리 대화 상자](intro-to-web-pages-programming/_static/image8.png)

검색 상자에 "asp.net 도우미"를 입력 합니다. NuGet은 검색 용어와 일치 하는 패키지를 표시 합니다.

![패키지를 표시 하는 WebMatrix의 NuGet 갤러리](intro-to-web-pages-programming/_static/image9.png)

ASP.NET 웹 도우미 라이브러리에는 Gravatar 이미지 사용을 비롯 하 여 여러 가지 일반적인 작업을 간소화 하는 코드가 포함 되어 있습니다. **ASP.NET 웹 도우미 라이브러리** 패키지를 선택 하 고 **설치** 를 클릭 하 여 설치 관리자를 시작 합니다. 패키지를 설치할지 묻는 메시지가 표시 되 면 **예** 를 선택 하 고 사용 약관에 동의 하 여 설치를 완료 합니다.

이것으로 끝입니다. NuGet은 필요할 수 있는 추가 구성 요소 (*종속성*)를 비롯 하 여 모든 항목을 다운로드 하 고 설치 합니다.

어떤 이유로 도우미가 제거 해야 하는 경우 프로세스는 매우 유사 합니다. **NuGet** 단추를 클릭 하 고 **설치 됨** 탭을 클릭 한 후에 제거할 패키지를 선택 합니다.

## <a name="using-a-helper-in-a-page"></a>페이지에서 도우미 사용

이제 방금 설치한 도우미를 사용 합니다. 페이지에 도우미를 추가 하는 프로세스는 대부분의 도우미에서 비슷합니다.

WebMatrix에서 페이지를 만들고 이름을 *GravatarTest*로 다시 만듭니다. 도우미를 테스트 하는 데 사용할 수 있는 특수 페이지를 만드는 중이지만 사이트의 모든 페이지에서 도우미를 사용할 수 있습니다.

&lt;body&gt; 요소 내에 &lt;div&gt; 요소를 추가 합니다. &lt;div&gt; 요소 내에 다음을 입력 합니다.

@Gravatar입니다.

@ 문자는 Razor 코드를 표시 하는 데 사용한 것과 동일한 문자입니다. **Gravatar** 는 작업 하는 도우미 개체입니다.

마침표 (.)를 입력 하는 즉시 WebMatrix는 Gravatar 도우미가 사용할 수 있도록 하는 *메서드* (함수)의 목록을 표시 합니다.

![Gravatar helper IntelliSense 드롭다운 목록](intro-to-web-pages-programming/_static/image10.png)

이 기능을 *IntelliSense*라고 합니다. 이를 통해 상황에 맞는 선택 항목을 제공 하 여 코드를 코딩할 수 있습니다. IntelliSense는 WebMatrix에서 지원 되는 HTML, CSS, ASP.NET 코드, JavaScript 및 기타 언어와 함께 작동 합니다. WebMatrix에서 웹 페이지를 보다 쉽게 개발할 수 있게 해 주는 또 다른 기능입니다.

키보드에서 G 키를 누르면 IntelliSense에서 GetHtml 메서드를 찾습니다. Tab 키를 누릅니다. IntelliSense는 선택한 메서드 (GetHtml)를 삽입 합니다. 여는 괄호를 입력 합니다. 그러면 닫는 괄호가 자동으로 추가 됩니다. 두 괄호 사이에 따옴표 안에 전자 메일 주소를 입력 합니다. Gravatar 계정이 있는 경우 프로필 그림이 반환 됩니다. Gravatar 계정이 없으면 기본 이미지가 반환 됩니다. 완료 되 면 줄은 다음과 같습니다.

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

이제 브라우저에서 페이지를 봅니다. Gravatar 계정이 있는지 여부에 따라 사진이 나 기본 이미지가 표시 됩니다.

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![기본 이미지](intro-to-web-pages-programming/_static/image12.png)

도우미가 어떤 작업을 수행 하 고 있는 것을 이해 하려면 브라우저에서 페이지의 원본을 확인 하세요. 페이지에 있는 HTML과 함께 식별자를 포함 하는 image 요소가 표시 됩니다. 이 코드는 도우미가 @Gravatar.GetHtml된 위치에서 페이지에 렌더링 하는 코드입니다. 도우미는 제공 된 정보를 제공 하 고 제공 된 계정에 대 한 올바른 이미지를 다시 가져오기 위해 Gravatar에 직접 통신 하는 코드를 생성 했습니다.

GetHtml 메서드를 사용 하면 다른 매개 변수를 제공 하 여 이미지를 사용자 지정할 수도 있습니다. 다음 코드에서는 40 픽셀의 너비와 높이가 있는 이미지를 요청 하는 방법을 보여 주며, 지정 된 계정이 없는 경우 **wavatar** 라는 지정 된 기본 이미지를 사용 합니다.

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

이 코드는 다음과 같은 결과를 생성 합니다. 기본 이미지는 임의로 달라 집니다.

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a>다음에서 시작

이 자습서를 간단 하 게 유지 하려면 몇 가지 기본 사항에만 초점을 맞춰야 합니다. 물론 Razor와 C#에 대 *한 많은 정보가* 있습니다. 이러한 자습서를 진행할 때 자세히 알아보세요. Razor C# 를 프로그래밍 하는 방법에 대 한 자세한 내용을 알아보려면 [razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=202890)를 참조 하세요.

다음 자습서에서는 데이터베이스를 사용 하는 방법을 소개 합니다. 이 자습서에서는 즐겨 사용 하는 영화를 나열할 수 있는 샘플 응용 프로그램을 만들기 시작 합니다.

## <a name="complete-listing-for-testrazor-page"></a>TestRazor 페이지에 대 한 전체 목록

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a>TestRazorPart2 페이지에 대 한 전체 목록

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a>GravatarTest 페이지에 대 한 전체 목록

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Twitter 도우미](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> [이전](getting-started.md)
> [다음](displaying-data.md)
