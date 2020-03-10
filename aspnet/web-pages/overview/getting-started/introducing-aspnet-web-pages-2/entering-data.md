---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: ASP.NET 웹 페이지 소개-폼을 사용 하 여 데이터베이스 데이터 입력 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 ASP.NET 웹 페이지 (...)를 사용할 때 양식에서 가져온 데이터를 데이터베이스 테이블에 입력 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: b9354a7b97a7df9020a681f709e16a92650cfcf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506603"
---
# <a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a>ASP.NET 웹 페이지 소개-폼을 사용 하 여 데이터베이스 데이터 입력

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 ASP.NET 웹 페이지 (Razor)를 사용할 때 입력 양식을 만들고 폼에서 데이터베이스 테이블로 가져오는 데이터를 입력 하는 방법을 보여 줍니다. [ASP.NET 웹 페이지에서 HTML 폼의 기본 사항을](https://go.microsoft.com/fwlink/?LinkId=251581)통해 계열을 완료 했다고 가정 합니다.
> 
> 학습할 내용:
> 
> - 항목 양식을 처리 하는 방법에 대해 자세히 알아봅니다.
> - 데이터베이스에서 데이터를 추가 (삽입) 하는 방법
> - 사용자가 양식에 필수 값을 입력 했는지 확인 하는 방법 (사용자 입력의 유효성을 검사 하는 방법)
> - 유효성 검사 오류를 표시 하는 방법입니다.
> - 현재 페이지에서 다른 페이지로 이동 하는 방법입니다.
>   
> 
> 설명 하는 기능/기술:
> 
> - `Database.Execute` 메서드
> - SQL `Insert Into` 문
> - `Validation` 도우미입니다.
> - `Response.Redirect` 메서드

## <a name="what-youll-build"></a>만들 내용

앞의 자습서에서는 데이터베이스를 만드는 방법을 보여 주었습니다 **. 데이터베이스 작업 영역에서** 작업 하는 WebMatrix에서 직접 데이터베이스를 편집 하 여 데이터베이스 데이터를 입력 했습니다. 그러나 대부분의 앱에서 데이터를 데이터베이스에 저장 하는 것은 실용적이 지 않습니다. 따라서이 자습서에서는 사용자가 데이터를 입력 하 고 데이터베이스에 저장 하는 데 사용할 수 있는 웹 기반 인터페이스를 만듭니다.

새 영화를 입력할 수 있는 페이지를 만듭니다. 이 페이지에는 영화 제목, 장르 및 연도를 입력할 수 있는 필드 (텍스트 상자)가 있는 항목 양식이 포함 됩니다. 페이지는 다음과 같이 표시 됩니다.

![브라우저의 ' 동영상 추가 ' 페이지](entering-data/_static/image1.png)

텍스트 상자는 다음과 같이 표시 되는 HTML `<input>` 요소가 됩니다.

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a>기본 항목 폼 만들기

*Addmovie. cshtml*라는 페이지를 만듭니다.

파일의 내용을 다음 태그로 바꿉니다. 모든 항목 덮어쓰기 잠시 후에 코드 블록을 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

이 예제에서는 폼을 만드는 일반적인 HTML을 보여 줍니다. 텍스트 상자 및 전송 단추에 대 한 `<input>` 요소를 사용 합니다. 텍스트 상자에 대 한 캡션은 표준 `<label>` 요소를 사용 하 여 만듭니다. `<fieldset>` 및 `<legend>` 요소는 폼 주위에 멋진 상자를 배치 합니다.

이 페이지에서 `<form>` 요소는 `post`를 `method` 특성의 값으로 사용 합니다. 이전 자습서에서는 `get` 메서드를 사용 하는 양식을 만들었습니다. 이는 양식이 서버에 값을 전송 하더라도 요청은 변경 하지 않았기 때문입니다. 모든 것이 다른 방법으로 데이터를 인출 했습니다. 그러나이 페이지에서는 새 데이터베이스 레코드를 추가 하 여 *변경 작업을 수행 합니다.* 따라서이 폼은 `post` 메서드를 사용 해야 합니다. `GET`와 `POST` 작업 간의 차이점에 대 한 자세한 내용은 이전 자습서의[GET, POST 및 HTTP Verb Safety](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) 사이드바를 참조 하세요.

각 텍스트 상자에는 `name` 요소 (`title`, `genre`, `year`)가 있습니다. 이전 자습서에서 살펴본 것 처럼 이러한 이름은 나중에 사용자의 입력을 받을 수 있도록 이러한 이름이 있어야 하기 때문에 중요 합니다. 임의의 이름을 사용할 수 있습니다. 작업 하는 데이터를 기억할 수 있도록 하는 의미 있는 이름을 사용 하는 것이 좋습니다.

각 `<input>` 요소의 `value` 특성에는 약간의 Razor 코드 (예: `Request.Form["title"]`)가 포함 되어 있습니다. 이전 자습서에서이 트릭의 버전을 학습 하 여 양식이 제출 된 후 입력란에 입력 된 값 (있는 경우)을 유지 했습니다.

## <a name="getting-the-form-values"></a>양식 값 가져오기

그런 다음 폼을 처리 하는 코드를 추가 합니다. 개요에서는 다음을 수행 합니다.

1. 페이지가 게시 되었는지 (제출 되었는지) 확인 합니다. 사용자가 단추를 클릭 한 경우에만 페이지가 처음으로 실행 되는 경우에만 코드를 실행 하려고 합니다.
2. 사용자가 텍스트 상자에 입력 한 값을 가져옵니다. 이 경우 폼이 `POST` 동사를 사용 하기 때문에 `Request.Form` 컬렉션에서 폼 값을 가져옵니다.
3. *동영상* 데이터베이스 테이블에 새 레코드로 값을 삽입 합니다.

파일 맨 위에 다음 코드를 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

처음 몇 줄은 텍스트 상자의 값을 포함 하는 변수 (`title`, `genre`및 `year`)를 만듭니다. 줄 `if(IsPost)`은 사용자가 **동영상 추가** 단추를 클릭할 때 (즉, 폼이 게시 된 경우)에 *만* 변수가 설정 되도록 합니다.

이전 자습서에서 살펴본 것 처럼 `Request.Form["name"]`와 같은 식을 사용 하 여 텍스트 상자의 값을 가져옵니다. 여기서 *name* 은 `<input>` 요소의 이름입니다.

변수 이름 (`title`, `genre`및 `year`)은 임의로 사용할 수 있습니다. `<input>` 요소에 할당 하는 이름과 마찬가지로 원하는 모든 항목을 호출할 수 있습니다. (변수의 이름이 폼에 있는 `<input>` 요소의 이름 특성과 일치 하지 않아도 됩니다.) 그러나 `<input>` 요소와 마찬가지로 포함 된 데이터를 반영 하는 변수 이름을 사용 하는 것이 좋습니다. 코드를 작성할 때 일관 된 이름을 사용 하면 작업 중인 데이터를 쉽게 기억할 수 있습니다.

## <a name="adding-data-to-the-database"></a>데이터베이스에 데이터 추가

방금 추가한 코드 블록의 닫는 중괄호 (`}` `if`) *내* 에서 (코드 블록 내부 뿐만 아니라) 다음 코드를 추가 합니다.

[!code-csharp[Main](entering-data/samples/sample3.cs)]

이 예제는 데이터를 가져오고 표시 하기 위해 이전 자습서에서 사용한 코드와 비슷합니다. `db =` 시작 하는 줄은 이전과 같이 데이터베이스를 열고 앞에서 살펴본 대로 다음 줄은 SQL 문을 정의 합니다. 그러나 이번에는 SQL `Insert Into` 문을 정의 합니다. 다음 예에서는 `Insert Into` 문의 일반적인 구문을 보여 줍니다.

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

즉, 삽입할 테이블을 지정한 다음 삽입할 열을 나열 하 고 삽입할 값을 나열 합니다. 앞에서 설명한 것 처럼 SQL은 대/소문자를 구분 하지 않지만 일부 사용자는 키워드를 사용 하 여 명령을 더 쉽게 읽을 수 있도록 합니다.

삽입 하는 열은 명령에 이미 나열 되어 `(Title, Genre, Year)`합니다. 흥미로운 부분은 텍스트 상자의 값을 명령의 `VALUES` 부분으로 가져오는 방법입니다. 실제 값 대신 자리 표시자 인 `@0`, `@1`및 `@2`표시 됩니다. `db.Execute` 줄에서 명령을 실행할 때 텍스트 상자에서 가져온 값을 전달 합니다.

**중요!** SQL 문에 사용자가 온라인으로 입력 한 데이터를 포함 하는 유일한 방법은 여기에 표시 된 대로 자리 표시자를 사용 하는 것입니다 (`VALUES(@0, @1, @2)`). 사용자 입력을 SQL 문에 연결 하는 경우 [ASP.NET 웹 페이지의 양식 기본 사항](https://go.microsoft.com/fwlink/?LinkId=251581) (이전 자습서)에 설명 된 대로 sql 삽입 공격을 직접 열 수 있습니다.

`if` 블록 내에서 `db.Execute` 줄 뒤에 다음 줄을 추가 합니다.

[!code-css[Main](entering-data/samples/sample4.css)]

새 동영상이 데이터베이스에 삽입 된 후이 줄은 사용자 (리디렉션)를 *동영상* 페이지로 이동 하 여 방금 입력 한 동영상을 볼 수 있도록 합니다. `~` 연산자는 "웹 사이트의 루트"를 의미 합니다. `~` 연산자는 일반적으로 HTML이 아닌 ASP.NET 페이지 에서만 작동 합니다.

전체 코드 블록은 다음 예제와 같습니다.

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a>삽입 명령 테스트 (지금까지)

아직 완료 되지 않았지만 지금 테스트 하는 것이 좋습니다.

WebMatrix의 파일 트리 뷰에서 *Addmovie. cshtml* 페이지를 마우스 오른쪽 단추로 클릭 한 다음 **브라우저에서 시작**을 클릭 합니다.

![브라우저의 ' 동영상 추가 ' 페이지](entering-data/_static/image2.png)

(브라우저에서 다른 페이지가 표시 되 면 URL이 `http://localhost:nnnnn/AddMovie`) 인지 확인 합니다. 여기서 *nnnnn* 은 사용 중인 포트 번호입니다.

오류 페이지가 있나요? 그렇다면, 신중 하 게 읽고 코드가 앞에서 설명한 것과 정확히 일치 하는지 확인 합니다.

예를 들어 "Kane", "드라마" 및 "1941"를 사용 하 여 &mdash; 양식에 영화를 입력 합니다. (또는 모든 항목) 그런 다음 **동영상 추가**를 클릭 합니다.

모든 작업이 제대로 진행 되 면 *동영상* 페이지로 리디렉션됩니다. 새 동영상이 나열 되는지 확인 합니다.

![새로 추가 된 동영상을 보여 주는 동영상 페이지](entering-data/_static/image3.png)

## <a name="validating-user-input"></a>사용자 입력 유효성 검사

*Addmovie* 페이지로 돌아가서 다시 실행 합니다. 다른 영화를 입력 합니다. 그러나 이번에는 &mdash; 제목만 입력 합니다. 예를 들어 "Singin'"를 입력 합니다. 그런 다음 **동영상 추가**를 클릭 합니다.

*동영상* 페이지로 다시 리디렉션됩니다. 새 동영상을 찾을 수 있지만 불완전 합니다.

![일부 값이 누락 된 새 동영상을 보여 주는 동영상 페이지](entering-data/_static/image4.png)

*동영상* 테이블을 만들 때 null 일 수 있는 필드는 없습니다. 새 영화에 대 한 입력 양식이 있고 필드를 비워 둡니다. 오류가 발생 했습니다.

이 경우 데이터베이스는 실제로 오류를 발생 시키거나 *throw*하지 않습니다. 장르 또는 연도를 제공 하지 않았으므로 *Addmovie* 페이지의 코드는 이러한 값을 *빈 문자열로*처리 합니다. SQL `Insert Into` 명령이 실행 될 때 장르 및 연도 필드에는 유용한 데이터가 없지만 null은 아닙니다.

사용자가 데이터베이스에 절반의 영화 정보를 입력할 수 없도록 하는 것이 좋습니다. 이 솔루션은 사용자 입력의 유효성을 검사 하는 것입니다. 처음에는 유효성 검사를 통해 사용자가 모든 필드 (즉, 빈 문자열은 포함 하지 않음)에 대 한 값을 입력 했는지 확인 합니다.

> [!TIP]
> 
> **Null 및 빈 문자열**
> 
> 프로그래밍에서는 서로 다른 개념 "no value"를 구분 합니다. 일반적으로 값은 설정 되거나 초기화 되지 않은 경우 *null* 입니다. 반대로 문자 데이터 (문자열)를 필요로 하는 변수를 *빈 문자열로*설정할 수 있습니다. 이 경우 값은 null이 아닙니다. 길이가 0 인 문자 문자열로 명시적으로 설정 되었습니다. 이 두 문은 다음과 같은 차이점을 보여 줍니다.
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> 보다 다소 복잡 하지만 `null`는 결정 되지 않은 상태를 나타내는 것입니다.
> 
> 이제 값이 null 인 경우와 빈 문자열일 때를 정확 하 게 이해 하는 것이 중요 합니다. *Addmovie* 의 코드 페이지에서 `Request.Form["title"]`를 사용 하 여 텍스트 상자의 값을 가져옵니다. 단추를 클릭 하기 전에 페이지를 처음 실행 하면 `Request.Form["title"]`의 값이 null입니다. 그러나 양식을 제출할 때 `title` 텍스트 상자의 값을 `Request.Form["title"]` 가져옵니다. 분명 한 것은 아니지만 빈 텍스트 상자는 null이 아닙니다. 빈 문자열을 포함 합니다. 그러면 단추 클릭에 대 한 응답으로 코드가 실행 될 때 `Request.Form["title"]`에 빈 문자열이 포함 됩니다.
> 
> 이러한 차이점이 중요 한 이유는 무엇 인가요? *동영상* 테이블을 만들 때 null 일 수 있는 필드는 없습니다. 하지만 여기서는 새 영화에 대 한 입력 양식이 있고 필드를 비워 둡니다. 장르 또는 연도에 대 한 값이 없는 새 영화를 저장 하려고 하면 데이터베이스가 정상적으로 사용할 수 있습니다. &mdash; 단, 해당 텍스트 상자를 비워 두는 경우에도 해당 값은 null이 아닙니다. 빈 문자열입니다. 결과적으로, 이러한 열이 비어 &mdash; 있지만 null이 아닌 새 동영상을 데이터베이스에 저장할 수 있습니다. &mdash; 값 따라서 사용자가 입력의 유효성을 검사 하 여 수행할 수 있는 빈 문자열을 제출 하지 않도록 해야 합니다.

### <a name="the-validation-helper"></a>유효성 검사 도우미

ASP.NET 웹 페이지에는 사용자가 요구 사항을 충족 하는 데이터를 입력 하는지 확인 하는 데 사용할 수 있는 도우미 &mdash; `Validation` 도우미 &mdash; 포함 됩니다. `Validation` 도우미는 ASP.NET 웹 페이지에 기본 제공 되는 도우미 중 하나 이며, 이전 자습서에서 Gravatar 도우미를 설치 하는 방식으로 NuGet을 사용 하 여 패키지로 설치할 필요가 없습니다.

사용자 입력의 유효성을 검사 하려면 다음을 수행 합니다.

- 코드를 사용 하 여 페이지의 텍스트 상자에 값을 요구 하도록 지정 합니다.
- 모든 것이 제대로 유효성을 검사 하는 경우에만 데이터베이스에 동영상 정보가 추가 되도록 테스트를 코드에 배치 합니다.
- 태그에 오류 메시지를 표시 하는 코드를 추가 합니다.

*Addmovie* 페이지의 코드 블록에서 변수 선언 앞의 위쪽에 다음 코드를 추가 합니다.

[!code-csharp[Main](entering-data/samples/sample7.cs)]

항목을 요구 하려는 각 필드 (`<input>` 요소)에 대해 `Validation.RequireField`를 한 번씩 호출 합니다. 여기에 표시 된 것 처럼 각 호출에 대 한 사용자 지정 오류 메시지를 추가할 수도 있습니다. (원하는 모든 항목을 배치할 수 있다는 것을 보여 주기 위해 메시지를 다양 하 게 설명 합니다.)

문제가 있는 경우 새 동영상 정보가 데이터베이스에 삽입 되지 않도록 합니다. `if(IsPost)` 블록에서 `&&` (논리적 AND)를 사용 하 여 `Validation.IsValid()`테스트 하는 다른 조건을 추가 합니다. 완료 되 면 전체 `if(IsPost)` 블록은 다음 코드와 같습니다.

[!code-csharp[Main](entering-data/samples/sample8.cs)]

`Validation` 도우미를 사용 하 여 등록 한 필드에 유효성 검사 오류가 있는 경우 `Validation.IsValid` 메서드에서 false를 반환 합니다. 이 경우 해당 블록의 코드는 실행 되지 않으므로 잘못 된 영화 항목이 데이터베이스에 삽입 되지 않습니다. 물론 *동영상* 페이지로 리디렉션되지 않습니다.

유효성 검사 코드를 비롯 한 전체 코드 블록은 이제 다음 예제와 같습니다.

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a>유효성 검사 오류 표시

마지막 단계는 오류 메시지를 표시 하는 것입니다. 각 유효성 검사 오류에 대 한 개별 메시지를 표시 하거나 요약 또는 둘 다를 표시할 수 있습니다. 이 자습서에서는 작동 방식을 확인할 수 있도록 두 작업을 모두 수행 합니다.

유효성을 검사 하는 각 `<input>` 요소 옆의 `Html.ValidationMessage` 메서드를 호출 하 고 유효성을 검사 하는 `<input>` 요소의 이름을 전달 합니다. 오류 메시지를 표시할 위치에 `Html.ValidationMessage` 메서드를 배치 합니다. 페이지가 실행 될 때 `Html.ValidationMessage` 메서드는 유효성 검사 오류가 발생 하는 `<span>` 요소를 렌더링 합니다. 오류가 없는 경우에는 `<span>` 요소가 렌더링 되지만 텍스트는 없습니다.

페이지에서 다음 예제와 같이 세 개의 `<input>` 요소 각각에 대 한 `Html.ValidationMessage` 메서드를 포함 하도록 페이지의 태그를 변경 합니다.

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

요약이 어떻게 작동 하는지 확인 하려면 페이지의 `<h1>Add a Movie</h1>` 요소 바로 뒤에 다음 태그와 코드를 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

기본적으로 `Html.ValidationSummary` 메서드는 목록에 모든 유효성 검사 메시지를 표시 합니다 (`<div>` 요소 내에 있는 `<ul>` 요소). `Html.ValidationMessage` 메서드와 마찬가지로 유효성 검사 요약에 대 한 태그는 항상 렌더링 됩니다. 오류가 없으면 목록 항목이 렌더링 되지 않습니다.

요약은 `Html.ValidationMessage` 메서드를 사용 하 여 각 필드별 오류를 표시 하는 대신 유효성 검사 메시지를 표시 하는 대체 방법이 될 수 있습니다. 또는 요약 및 세부 정보를 모두 사용할 수 있습니다. 또는 `Html.ValidationSummary` 메서드를 사용 하 여 일반 오류를 표시 한 다음 개별 `Html.ValidationMessage` 호출을 사용 하 여 세부 정보를 표시할 수 있습니다.

이제 전체 페이지는 다음 예와 같습니다.

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

이것으로 끝입니다. 이제 영화를 추가 하 고 하나 이상의 필드를 남기고 페이지를 테스트할 수 있습니다. 이렇게 하면 다음과 같은 오류 표시가 나타납니다.

![유효성 검사 오류 메시지를 보여 주는 동영상 추가](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a>유효성 검사 오류 메시지의 스타일 지정

오류 메시지가 표시 되는 것을 확인할 수 있지만,이는 정말 잘 작동 하지 않습니다. 그러나 오류 메시지의 스타일을 쉽게 적용할 수 있는 방법이 있습니다.

`Html.ValidationMessage`표시 되는 개별 오류 메시지의 스타일을 지정 하려면 `field-validation-error`라는 CSS 스타일 클래스를 만듭니다. 유효성 검사 요약에 대 한 검색을 정의 하려면 `validation-summary-errors`라는 CSS 스타일 클래스를 만듭니다.

이 기술의 작동 방식을 확인 하려면 페이지의 `<head>` 섹션 내에 `<style>` 요소를 추가 합니다. 그런 다음 다음 규칙을 포함 하는 `field-validation-error` 및 `validation-summary-errors` 이라는 스타일 클래스를 정의 합니다.

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

일반적으로 별도의 *.css* 파일에 스타일 정보를 저장 하는 것이 좋습니다. 편의상 페이지에 배치할 수 있습니다. 이 자습서의 뒷부분에서는 CSS 규칙을 별도 *.css* 파일로 이동 합니다.

유효성 검사 오류가 있는 경우 `Html.ValidationMessage` 메서드는 `class="field-validation-error"`를 포함 하는 `<span>` 요소를 렌더링 합니다. 해당 클래스에 대 한 스타일 정의를 추가 하 여 메시지가 표시 되는 모양을 구성할 수 있습니다. 오류가 있는 경우 `ValidationSummary` 메서드는 마찬가지로 특성 `class="validation-summary-errors"`를 동적으로 렌더링 합니다.

페이지를 다시 실행 하 고, 두 필드를 의도적으로 종료 합니다. 이제 오류가 더 두드러집니다. 실제로는이 작업을 수행할 수 있는 작업을 보여 주기 위한 것입니다.

![스타일이 지정 된 유효성 검사 오류를 보여 주는 동영상 추가 페이지](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a>동영상 페이지에 링크 추가

최종 단계 중 하나는 원래 동영상 목록에서 *addmovie* 페이지로 이동 하는 것입니다.

*동영상* 페이지를 다시 엽니다. `WebGrid` 도우미 뒤에 오는 closing `</div>` 태그 뒤에 다음 태그를 추가 합니다.

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

앞서 살펴본 것 처럼 ASP.NET는 `~` 연산자를 웹 사이트의 루트로 해석 합니다. `~` 연산자를 사용할 필요가 없습니다. 태그 `<a href="./AddMovie">Add a movie</a>` 또는 다른 방법을 사용 하 여 HTML에서 인식 하는 경로를 정의할 수 있습니다. 그러나 `~` 연산자는 Razor 페이지에 대 한 링크를 만들 때 적절 한 일반적인 방법입니다 .이는 사이트의 유연성을 향상 시킬 수 있기 때문입니다. 현재 페이지를 하위 폴더로 이동 하면 링크가 여전히 *Addmovie* 페이지로 이동 하 게 됩니다. `~` 연산자는 *. cshtml* 페이지 에서만 작동 합니다. ASP.NET는이를 이해 하지만 표준 HTML은 아닙니다.)

완료 되 면 *동영상* 페이지를 실행 합니다. 이 페이지가 다음과 같이 표시 됩니다.

![' 동영상 추가 ' 페이지에 대 한 링크가 있는 동영상 페이지](entering-data/_static/image7.png)

**동영상 추가** 링크를 클릭 하 여 *addmovie* 페이지로 이동 하는지 확인 합니다.

## <a name="coming-up-next"></a>다음에서 시작

다음 자습서에서는 데이터베이스에 이미 있는 데이터를 사용자가 편집할 수 있도록 하는 방법을 배웁니다.

## <a name="complete-listing-for-addmovie-page"></a>AddMovie 페이지의 전체 목록

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools 사이트의 [SQL INSERT INTO 문](http://www.w3schools.com/sql/sql_insert.asp)
- [ASP.NET 웹 페이지 사이트에서 사용자 입력의 유효성을 검사](https://go.microsoft.com/fwlink/?LinkId=253002)합니다. `Validation` 도우미를 사용 하는 방법에 대 한 자세한 정보.

> [!div class="step-by-step"]
> [이전](form-basics.md)
> [다음](updating-data.md)
