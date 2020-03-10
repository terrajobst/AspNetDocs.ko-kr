---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: 데이터베이스 데이터 업데이트 ASP.NET 웹 페이지 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Razor (ASP.NET 웹 페이지)를 사용할 때 기존 데이터베이스 항목을 업데이트 (변경) 하는 방법을 보여 줍니다. 여기서는 시리즈를 완료 했다고 가정 합니다.
ms.author: riande
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 8f8bcfb7d9d2416a2699776cadbdaae8e12415ba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78463493"
---
# <a name="introducing-aspnet-web-pages---updating-database-data"></a>데이터베이스 데이터 업데이트 ASP.NET 웹 페이지 소개

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 Razor (ASP.NET 웹 페이지)를 사용할 때 기존 데이터베이스 항목을 업데이트 (변경) 하는 방법을 보여 줍니다. [ASP.NET 웹 페이지를 사용 하는 양식을 사용 하 여 데이터를 입력](entering-data.md)하는 과정을 통해 계열을 완료 했다고 가정 합니다.
> 
> 학습할 내용:
> 
> - `WebGrid` 도우미에서 개별 레코드를 선택 하는 방법입니다.
> - 데이터베이스에서 단일 레코드를 읽는 방법
> - 데이터베이스 레코드의 값을 사용 하 여 폼을 미리 로드 하는 방법
> - 데이터베이스에서 기존 레코드를 업데이트 하는 방법입니다.
> - 정보를 표시 하지 않고 페이지에 저장 하는 방법
> - 숨겨진 필드를 사용 하 여 정보를 저장 하는 방법입니다.
>   
> 
> 설명 하는 기능/기술:
> 
> - `WebGrid` 도우미입니다.
> - SQL `Update` 명령입니다.
> - `Database.Execute` 메서드
> - 숨겨진 필드 (`<input type="hidden">`)

## <a name="what-youll-build"></a>만들 내용

이전 자습서에서는 데이터베이스에 레코드를 추가 하는 방법을 알아보았습니다. 여기에서는 편집을 위해 레코드를 표시 하는 방법을 배웁니다. *동영상* 페이지에서 각 동영상 옆에 **편집** 링크가 표시 되도록 `WebGrid` 도우미를 업데이트 합니다.

![각 영화에 대 한 ' 편집 ' 링크를 포함 하 여 WebGrid 표시](updating-data/_static/image1.png)

**편집** 링크를 클릭 하면 동영상 정보가 이미 양식에 있는 다른 페이지로 이동 합니다.

![편집할 동영상이 표시 되는 영화 편집 페이지](updating-data/_static/image2.png)

모든 값을 변경할 수 있습니다. 변경 내용을 제출할 때 페이지의 코드는 데이터베이스를 업데이트 하 고 동영상 목록으로 돌아갑니다.

이 프로세스의 부분은 이전 자습서에서 만든 *Addmovie* 페이지와 거의 동일 하 게 작동 하므로이 자습서의 많은 부분이 익숙할 것입니다.

여러 가지 방법으로 개별 동영상을 편집 하는 방법을 구현할 수 있습니다. 표시 되는 방법은 구현 하기 쉬우며 이해 하기 쉽기 때문에 선택 되었습니다.

## <a name="adding-an-edit-link-to-the-movie-listing"></a>동영상 목록에 편집 링크 추가

시작 하려면 동영상 페이지를 업데이트 하 여 각 동영상 목록에도 **편집** 링크가 포함 *되도록 합니다.*

*영화 cshtml* 파일을 엽니다.

페이지 본문에서 열을 추가 하 여 `WebGrid` 태그를 변경 합니다. 수정 된 태그는 다음과 같습니다.

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

새 열은 다음과 같습니다.

[!code-html[Main](updating-data/samples/sample2.html)]

이 열은 텍스트가 "Edit" 라고 표시 된 링크 (`<a>` 요소)를 표시 하는 것입니다. 그 후의 작업은 페이지가 실행 될 때 다음과 같은 링크를 만드는 것 이며, 각 동영상 마다 `id` 값이 다릅니다.

[!code-css[Main](updating-data/samples/sample3.css)]

이 링크는 *Editmovie*라는 페이지를 호출 하 고 해당 페이지에 쿼리 문자열 `?id=7`를 전달 합니다.

새 열에 대 한 구문은 약간 복잡할 수 있지만이는 여러 요소를 함께 배치 하기 때문입니다. 각 개별 요소는 간단 합니다. `<a>` 요소에만 집중 하는 경우 다음과 같은 태그가 표시 됩니다.

[!code-html[Main](updating-data/samples/sample4.html)]

Grid의 작동 방식에 대 한 배경: 그리드는 각 데이터베이스 레코드에 대해 하나씩 행을 표시 하 고 데이터베이스 레코드의 각 필드에 대 한 열을 표시 합니다. 각 표 행을 생성 하는 동안 `item` 개체는 해당 행에 대 한 데이터베이스 레코드 (항목)를 포함 합니다. 이러한 정렬은 코드에서 해당 행에 대 한 데이터를 가져오는 방법을 제공 합니다. 여기에 표시 되는 것은 현재 데이터베이스 항목의 ID 값을 가져오는 식 `item.ID`입니다. `item.Title`, `item.Genre`또는 `item.Year`를 사용 하 여 동일한 방식으로 데이터베이스 값 (제목, 장르 또는 연도)을 가져올 수 있습니다.

식 `"~/EditMovie?id=@item.ID` 대상 URL (`~/EditMovie?id=`)의 하드 코드 된 부분을 동적으로 파생 된 ID와 결합 합니다. 이전 자습서에서 `~` 연산자를 살펴보았습니다. 현재 웹 사이트 루트를 나타내는 ASP.NET 연산자입니다.

그 결과 열에 있는 태그의이 부분에서는 런타임에 다음 태그와 같은 항목을 생성 합니다.

[!code-xml[Main](updating-data/samples/sample5.xml)]

기본적으로 `id`의 실제 값은 각 행 마다 다릅니다.

## <a name="creating-a-custom-display-for-a-grid-column"></a>표 열에 대 한 사용자 지정 표시 만들기

이제 표 형태 열로 돌아갑니다. 처음에는 표에 있었던 세 개의 열이 데이터 값 (제목, 장르 및 연도)만 표시 됩니다. 데이터베이스 열의 이름을 전달 하 여이 표시를 지정 했습니다 &mdash; 예: `grid.Column("Title")`.

이 새 링크 **편집** 열은 서로 다릅니다. 열 이름을 지정 하는 대신 `format` 매개 변수를 전달 합니다. 이 매개 변수를 사용 하면 `WebGrid` 도우미가 `item` 값과 함께 렌더링 하는 태그를 정의 하 여 열 데이터를 굵게 또는 녹색 또는 원하는 형식으로 표시할 수 있습니다. 예를 들어 제목을 굵게 표시 하려는 경우 다음 예제와 같은 열을 만들 수 있습니다.

[!code-html[Main](updating-data/samples/sample6.html)]

(`format` 속성에 표시 되는 다양 한 `@` 문자는 태그와 코드 값 사이에 전환을 표시 합니다.)

`format` 속성에 대 한 정보를 확인 한 후에는 새 링크 **편집** 열이 어떻게 함께 배치 되는지 쉽게 이해할 수 있습니다.

[!code-html[Main](updating-data/samples/sample7.html)]

열은 링크를 렌더링 하는 태그와 행의 데이터베이스 레코드에서 추출 된 일부 정보 (ID)로 *만* 구성 됩니다.

> [!TIP]
> 
> **메서드의 명명 된 매개 변수 및 위치 매개 변수**
> 
> 메서드를 호출 하 고 매개 변수를 전달한 경우에는 매개 변수 값을 쉼표로 구분 하 여 나열 했을 수 있습니다. 다음은 몇 가지 예입니다.
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> 이 코드를 처음 볼 때에는이 문제를 언급 하지 않았지만, 각 경우에 매개 변수가 해당 메서드에서 정의 되는 순서 &mdash; 같이 특정 순서로 메서드에 매개 변수를 전달 하는 것입니다. `db.Execute` 및 `Validation.RequireFields`에서 전달 하는 값의 순서를 혼합 하는 경우 페이지가 실행 될 때 또는 이상 이상한 결과가 발생 하는 경우 오류 메시지가 표시 됩니다. 에서 매개 변수를 전달 하는 순서를 알고 있어야 합니다. (WebMatrix에서 IntelliSense는 매개 변수의 이름, 형식 및 순서를 파악 하는 데 도움이 될 수 있습니다.)
> 
> 값을 순서 대로 전달 하는 대신 *명명 된 매개 변수*를 사용할 수 있습니다. 매개 변수를 순서 대로 전달 하는 것을 *위치 매개 변수*사용 이라고 합니다. 명명 된 매개 변수의 경우 해당 값을 전달할 때 매개 변수의 이름을 명시적으로 포함 합니다. 이러한 자습서에서는 이미 여러 번 명명 된 매개 변수를 사용 했습니다. 다음은 그 예입니다.
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> and
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> 명명 된 매개 변수는 특히 메서드가 많은 매개 변수를 사용 하는 경우에 유용 합니다. 하나 또는 두 개의 매개 변수만 전달 하려고 하지만 전달 하려는 값이 매개 변수 목록의 첫 번째 위치에 없는 경우를 들 수 있습니다. 사용자에 게 가장 적합 한 순서로 매개 변수를 전달 하 여 코드를 더 쉽게 읽을 수 있도록 하려는 경우가 있습니다.
> 
> 물론 명명 된 매개 변수를 사용 하려면 매개 변수의 이름을 알아야 합니다. WebMatrix IntelliSense는 이름을 *표시할* 수 있지만 현재 사용자를 채울 수 없습니다.

## <a name="creating-the-edit-page"></a>편집 페이지 만들기

이제 *Editmovie* 페이지를 만들 수 있습니다. 사용자가 **편집** 링크를 클릭 하면이 페이지가 표시 됩니다.

*Editmovie. cshtml* 라는 페이지를 만들고 파일에서 다음 태그로 바꿉니다.

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

이 태그와 코드는 *Addmovie* 페이지에 있는 것과 비슷합니다. 전송 단추에 대 한 텍스트에는 약간의 차이가 있습니다. *Addmovie* 페이지와 마찬가지로에는 유효성 검사 오류를 표시 하는 `Html.ValidationSummary` 호출이 있습니다. 이번에는 오류가 유효성 검사 요약에 표시 되기 때문에 `Validation.Message`에 대 한 호출을 종료 하 고 있습니다. 이전 자습서에서 언급 한 것 처럼 다양 한 조합에서 유효성 검사 요약 및 개별 오류 메시지를 사용할 수 있습니다.

`<form>` 요소의 `method` 특성이 `post`으로 설정 되어 있는지 다시 확인 합니다. *Addmovie. cshtml* 페이지와 마찬가지로이 페이지에서 데이터베이스를 변경 합니다. 따라서이 양식은 `POST` 작업을 수행 해야 합니다. `GET`와 `POST` 작업 간의 차이점에 대 한 자세한 내용은 HTML 폼 자습서의 [GET, POST 및 HTTP Verb Safety](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) 사이드바를 참조 하세요.

이전 자습서에서 살펴본 것 처럼 텍스트 상자의 `value` 특성을 미리 로드 하기 위해 Razor 코드를 사용 하 여 설정 합니다. 그러나 이번에는 `Request.Form["title"]`대신 해당 태스크에 대 한 `title` 및 `genre` 같은 변수를 사용 합니다.

`<input type="text" name="title" value="@title" />`

이전과 마찬가지로이 태그는 텍스트 상자 값을 동영상 값으로 미리 로드 합니다. 지금은 `Request` 개체를 사용 하는 대신 변수를 사용 하는 것이 좋습니다.

또한이 페이지에는 `<input type="hidden">` 요소가 있습니다. 이 요소는 페이지에 표시 하지 않고 영화 ID를 저장 합니다. ID는 처음에 쿼리 문자열 값을 사용 하 여 페이지에 전달 됩니다 (URL에서`?id=7` 또는 유사). ID 값을 숨겨진 필드에 두면 페이지가 호출 된 원본 URL에 대 한 액세스 권한이 더 이상 없는 경우에도 폼이 제출 될 때 사용할 수 있는지 확인할 수 있습니다.

*Addmovie* 페이지와 달리 *editmovie* 페이지의 코드에는 두 개의 고유한 함수가 있습니다. 첫 번째 함수는 페이지가 처음으로 표시 되 고 그 다음에 *만* 표시 되는 경우 코드는 쿼리 문자열에서 영화 ID를 가져옵니다. 그런 다음 코드는 ID를 사용 하 여 데이터베이스에서 해당 하는 영화를 읽고 텍스트 상자에 표시 (미리 로드) 합니다.

두 번째 함수는 사용자가 **변경 내용 전송** 단추를 클릭할 때 코드에서 텍스트 상자의 값을 읽고 유효성을 검사 해야 한다는 것입니다. 또한이 코드는 데이터베이스 항목을 새 값으로 업데이트 해야 합니다. 이 기법은 *Addmovie*에서 살펴본 것 처럼 레코드를 추가 하는 것과 비슷합니다.

## <a name="adding-code-to-read-a-single-movie"></a>단일 영화를 읽기 위한 코드 추가

첫 번째 함수를 수행 하려면 페이지 맨 위에 다음 코드를 추가 합니다.

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

이 코드의 대부분은 `if(!IsPost)`를 시작 하는 블록 내에 있습니다. `!` 연산자는 "not"을 의미 하므로 식은이 *요청이 post 제출이*아님을 의미 합니다 .이는이 *요청이 처음으로 실행*되는 경우이 요청이 간접적입니다. 앞에서 설명한 것 처럼이 코드는 페이지가 처음 실행 될 때 *만* 실행 해야 합니다. `if(!IsPost)`에서 코드를 묶지 않은 경우 처음으로 또는 단추 클릭에 대 한 응답으로 페이지가 호출 될 때마다 실행 됩니다.

이번에는 코드에 `else` 블록이 포함 되어 있습니다. `if` 블록을 도입 했을 때와 같이 테스트 하는 조건이 충족 되지 않는 경우에는 다른 코드를 실행 하려고 할 수 있습니다. 여기에는이 사례가 있습니다. 조건에 통과 하는 경우 (즉, 페이지에 전달 된 ID가 양호 하면) 데이터베이스에서 행을 읽습니다. 그러나 조건이 충족 되지 않으면 `else` 블록이 실행 되 고 코드에서 오류 메시지를 설정 합니다.

## <a name="validating-a-value-passed-to-the-page"></a>페이지에 전달 된 값의 유효성 검사

이 코드는 `Request.QueryString["id"]`를 사용 하 여 페이지에 전달 되는 ID를 가져옵니다. 이 코드는 값이 실제로 ID에 대해 전달 되었는지를 확인할 수 있도록 합니다. 값이 전달 되지 않은 경우 코드에서 유효성 검사 오류를 설정 합니다.

이 코드는 정보의 유효성을 검사 하는 다른 방법을 보여 줍니다. 이전 자습서에서는 `Validation` 도우미로 작업 했습니다. 유효성을 검사할 필드를 등록 하 고 `Html.ValidationMessage` 및 `Html.ValidationSummary`를 사용 하 여 유효성 검사 및 표시 된 오류를 자동으로 ASP.NET 했습니다. 그러나이 경우 사용자 입력의 유효성을 검사 하는 것은 아닙니다. 대신 다른 위치에서 페이지에 전달 된 값의 유효성을 검사 하 게 됩니다. `Validation` 도우미가이 작업을 수행 하지 않습니다.

따라서 `if(!Request.QueryString["ID"].IsEmpty()`으로 테스트 하 여 값을 직접 확인 합니다. 문제가 발생 하는 경우 `Validation` 도우미와 같이 `Html.ValidationSummary`를 사용 하 여 오류를 표시할 수 있습니다. 이렇게 하려면 `Validation.AddFormError`를 호출 하 고 메시지를 전달 하 여 메시지를 표시 합니다. `Validation.AddFormError`는 이미 친숙 한 유효성 검사 시스템에 연결 하는 사용자 지정 메시지를 정의할 수 있도록 하는 기본 제공 메서드입니다. (이 자습서의 뒷부분에서는이 유효성 검사 프로세스를 좀 더 강력 하 게 만드는 방법에 대해 설명 합니다.)

동영상에 대 한 ID가 있는지 확인 한 후 코드는 데이터베이스를 읽고 단일 데이터베이스 항목만 찾습니다. 데이터베이스 작업에 대 한 일반적인 패턴을 알고 있을 수 있습니다. 데이터베이스를 열고 SQL 문을 정의한 다음 문을 실행 합니다. 이번에는 SQL `Select` 문에 `WHERE ID = @0`포함 되어 있습니다. ID는 고유 하기 때문에 하나의 레코드만 반환 될 수 있습니다.

`db.QuerySingle`를 사용 하 여 쿼리를 수행 합니다 .이 쿼리는 동영상 목록에 사용 된 것 처럼 `db.Query`하지 않으며, 코드는 결과를 `row` 변수에 넣습니다. 이름 `row` 임의의 이름입니다. 원하는 모든 변수 이름을 지정할 수 있습니다. 그런 다음 위쪽에서 초기화 된 변수는 텍스트 상자에 이러한 값을 표시할 수 있도록 동영상 세부 정보로 채워집니다.

## <a name="testing-the-edit-page-so-far"></a>편집 페이지 테스트 (지금까지)

페이지를 테스트 하려면 지금 *영화* 페이지를 실행 하 고 동영상 옆의 **편집** 링크를 클릭 합니다. 선택한 영화에 대 한 세부 정보가 채워진 *동영상 편집* 페이지가 표시 됩니다.

![편집할 동영상이 표시 되는 영화 편집 페이지](updating-data/_static/image3.png)

페이지의 URL에 `?id=10` (또는 다른 숫자)와 같은 내용이 포함 되어 있습니다. 지금까지 *, 페이지에서* 쿼리 문자열의 ID를 읽고 단일 영화 레코드를 가져오기 위해 데이터베이스 쿼리가 **작동 하는지 테스트** 했을 수 있습니다.

영화 정보를 변경할 수 있지만 **변경 내용 전송**을 클릭 하면 아무 작업도 수행 되지 않습니다.

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a>사용자의 변경 내용을 사용 하 여 동영상을 업데이트 하는 코드 추가

*Editmovie. cshtml* 파일에서 두 번째 함수 (변경 내용 저장)를 구현 하려면 `@` 블록의 닫는 중괄호 바로 안에 다음 코드를 추가 합니다. 코드의 위치를 정확 하 게 알 수 없는 경우이 자습서의 끝에 표시 되는 [동영상 편집 페이지에 대 한 전체 코드 목록을](#Complete_Page_Listing_for_EditMovie) 살펴볼 수 있습니다.

[!code-csharp[Main](updating-data/samples/sample12.cs)]

이 태그와 코드는 *Addmovie*의 코드와 비슷합니다. 이 코드는 사용자가 **변경 내용 전송** &mdash; 단추를 클릭 한 경우에만 실행 되는 경우, 즉 폼이 게시 된 경우에만 실행 되기 때문에 `if(IsPost)` 블록에 있습니다. 이 경우에 `if(IsPost && Validation.IsValid())`와 같은 테스트를 사용 하 고 있지 않습니다. 즉, 및를 사용 하 여 두 테스트를 결합 하지 않습니다. 이 페이지에서는 먼저 양식 제출 (`if(IsPost)`)이 있는지 확인 한 다음 유효성 검사를 위해 필드를 등록 합니다. 그런 다음 유효성 검사 결과 (`if(Validation.IsValid()`)를 테스트할 수 있습니다. 흐름은 *Addmovie. cshtml* 페이지와 약간 다르지만 효과는 동일 합니다.

다른 `<input>` 요소에 대 한 `Request.Form["title"]` 및 유사한 코드를 사용 하 여 텍스트 상자의 값을 가져옵니다. 이번에는 코드가 숨겨진 필드 (`<input type="hidden">`)에서 영화 ID를 가져옵니다. 페이지가 처음 실행 되 면 코드는 쿼리 문자열에서 ID를 가져왔습니다. 이후에 쿼리 문자열이 변경 된 경우에는 숨겨진 필드에서 값을 가져와 원래 표시 된 동영상의 ID를 가져오는지 확인 합니다.

*Addmovie* 코드와이 코드의 매우 중요 한 차이점은이 코드에서는 `Insert Into` 문 대신 SQL `Update` 문을 사용 한다는 것입니다. 다음 예에서는 SQL `Update` 문의 구문을 보여 줍니다.

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

임의의 순서로 열을 지정할 수 있으며, `Update` 작업을 수행 하는 동안 모든 열을 업데이트할 필요는 없습니다. (이 경우에는 레코드를 새 레코드로 저장 하 고 `Update` 작업에는 사용할 수 없기 때문에 ID 자체를 업데이트할 수 없습니다.)

> [!NOTE] 
> 
> **중요** ID를 사용 하는 `Where` 절은 데이터베이스에서 업데이트 하려는 데이터베이스 레코드를 파악 하는 방법 이기 때문에 매우 중요 합니다. `Where` 절을 생략 한 경우 데이터베이스는 데이터베이스의 *모든* 레코드를 업데이트 합니다. 대부분의 경우에는 재해가 발생 합니다.

코드에서 업데이트할 값은 자리 표시자를 사용 하 여 SQL 문에 전달 됩니다. 이전에 언급 한 작업을 반복 하려면: 보안상의 이유로 자리 표시자 *를 사용 하 여 값을 SQL* 문에 전달 합니다.

코드에서 `db.Execute` 사용 하 여 `Update` 문을 실행 한 후에는 목록 페이지로 다시 리디렉션되고 변경 내용을 볼 수 있습니다.

> [!TIP] 
> 
> **다른 SQL 문, 다른 방법**
> 
> 약간 다른 방법을 사용 하 여 다른 SQL 문을 실행할 수 있습니다. 잠재적으로 여러 레코드를 반환 하는 `Select` 쿼리를 실행 하려면 `Query` 메서드를 사용 합니다. 하나의 데이터베이스 항목만 반환 될 것으로 알고 있는 `Select` 쿼리를 실행 하려면 `QuerySingle` 메서드를 사용 합니다. 변경 작업을 수행 하지만 데이터베이스 항목을 반환 하지 않는 명령을 실행 하려면 `Execute` 메서드를 사용 합니다.
> 
> `Query`와 `QuerySingle`의 차이에 이미 표시 된 것 처럼 각각 다른 결과를 반환 하기 때문에 다른 메서드를 가져야 합니다. `Execute` 메서드는 실제로 &mdash; 값을 반환 합니다. 즉, &mdash; 명령의 영향을 받는 데이터베이스 행의 수를 반환 하지만 지금 까지는 무시 했습니다.
> 
> 물론 `Query` 메서드는 데이터베이스 행을 하나만 반환할 수 있습니다. 그러나 ASP.NET는 항상 `Query` 메서드의 결과를 컬렉션으로 처리 합니다. 메서드가 하나의 행만 반환 하는 경우에도 컬렉션에서 해당 하는 단일 행을 추출 해야 합니다. 따라서 행을 하나만 *반환 하는* 경우 `QuerySingle`사용 하는 것이 더 편리 합니다.
> 
> 특정 유형의 데이터베이스 작업을 수행 하는 몇 가지 다른 메서드가 있습니다. [ASP.NET 웹 페이지 API 빠른 참조](../../api-reference/asp-net-web-pages-api-reference.md#Data)에서 데이터베이스 메서드 목록을 찾을 수 있습니다.

## <a name="making-validation-for-the-id-more-robust"></a>ID의 유효성을 보다 강력 하 게 확인

페이지가 처음으로 실행 될 때 데이터베이스에서 동영상을 가져올 수 있도록 쿼리 문자열에서 영화 ID를 가져옵니다. 이 코드를 사용 하 여 실제로 수행할 값이 실제로 있는지 확인 합니다.

[!code-csharp[Main](updating-data/samples/sample13.cs)]

이 코드를 사용 하 여 사용자가 *영화* 페이지에서 영화를 먼저 선택 하지 않고 *editmovies* 페이지로 이동할 경우 페이지에서 사용자에 게 친숙 한 오류 메시지를 표시 하는지 확인 합니다. 그렇지 않으면 사용자에 게 혼동을 주는 오류가 표시 됩니다.

그러나이 유효성 검사는 매우 강력 하지 않습니다. 이 페이지는 다음과 같은 오류와 함께 호출 될 수도 있습니다.

- ID가 숫자가 아닙니다. 예를 들어 `http://localhost:nnnnn/EditMovie?id=abc`와 같은 URL을 사용 하 여 페이지를 호출할 수 있습니다.
- ID는 숫자 이지만 존재 하지 않는 영화를 참조 합니다 (예: `http://localhost:nnnnn/EditMovie?id=100934`).

이러한 Url로 인해 발생 하는 오류를 확인 하려면 *동영상* 페이지를 실행 합니다. 편집할 동영상을 선택 하 고 *editmovie* 페이지의 url을 알파벳 id 또는 존재 하지 않는 동영상의 id를 포함 하는 url로 변경 합니다.

그렇다면 어떻게 해야 하나요? 첫 번째 해결 방법은 페이지에 전달 된 ID가 아니라 정수 인지 확인 하는 것입니다. `!IsPost` 테스트에 대 한 코드를 다음 예제와 같이 변경 합니다.

[!code-csharp[Main](updating-data/samples/sample14.cs)]

`IsEmpty` 테스트에 `&&` (논리적 AND)와 연결 된 두 번째 조건을 추가 했습니다.

[!code-csharp[Main](updating-data/samples/sample15.cs)]

[ASP.NET 웹 페이지 프로그래밍 자습서 소개](../introducing-razor-syntax-c.md) 에서 `AsInt` `AsBool` 같은 메서드가 문자열을 다른 데이터 형식으로 변환 하는 방법을 설명 합니다. `IsInt` 메서드 (`IsBool` 및 `IsDateTime`와 같은 기타)는 비슷합니다. 그러나 실제로 변환을 수행 하지 않고도 문자열을 변환할 *수* 있는지 여부를 테스트 합니다. 따라서 여기서 *는 쿼리 문자열 값을 정수로 변환할 수 있는지 여부*를 확인 합니다.

다른 잠재적인 문제는 존재 하지 않는 영화를 찾는 것입니다. 동영상을 가져오는 코드는 다음 코드와 같습니다.

[!code-csharp[Main](updating-data/samples/sample16.cs)]

실제 동영상과 일치 하지 않는 `QuerySingle` 메서드에 `movieId` 값을 전달 하는 경우 아무 것도 반환 되지 않고 다음 (예: `title=row.Title`)에 나오는 문에서 오류가 발생 합니다.

그러면 쉽게 해결할 수 있습니다. `db.QuerySingle` 메서드가 결과를 반환 하지 않는 경우에는 `row` 변수가 null이 됩니다. 따라서 값을 가져오기 전에 `row` 변수가 null 인지 여부를 확인할 수 있습니다. 다음 코드는 `row` 개체에서 값을 가져오는 문 주위에 `if` 블록을 추가 합니다.

[!code-csharp[Main](updating-data/samples/sample17.cs)]

이러한 두 가지 추가 유효성 검사 테스트를 사용 하면 페이지에 더 많은 글머리 기호가 추가 됩니다. 이제 `!IsPost` 분기에 대 한 전체 코드는 다음 예제와 같습니다.

[!code-csharp[Main](updating-data/samples/sample18.cs)]

이 작업을 `else` 블록에 사용 하는 것이 더 좋습니다. 테스트가 통과 하지 못하면 `else` 블록은 오류 메시지를 설정 합니다.

## <a name="adding-a-link-to-return-to-the-movies-page"></a>동영상 페이지로 돌아가는 링크 추가

최종 및 유용한 세부 정보는 *동영상* 페이지에 링크를 다시 추가 하는 것입니다. 일반적인 이벤트 흐름에서 사용자는 *동영상* 페이지에서 시작 하 여 **편집** 링크를 클릭 합니다. 그러면 동영상을 편집 하 고 단추를 클릭할 수 있는 *editmovie* 페이지로 이동 합니다. 코드는 변경을 처리 한 후 *동영상* 페이지로 다시 리디렉션됩니다.

그러나

- 사용자는 아무것도 변경 하지 않도록 결정할 수 있습니다.
- 사용자는 먼저 *동영상* 페이지에서 **편집** 링크를 클릭 하지 않고이 페이지로 이동할 수 있습니다.

어느 방법을 사용 하 든 쉽게 기본 목록으로 돌아갈 수 있습니다. 태그의 닫는 `</form>` 태그 바로 뒤에 다음 태그를 추가 &mdash; 쉽게 수정할 수 있습니다.

[!code-html[Main](updating-data/samples/sample19.html)]

이 태그는 다른 곳에서 표시 된 `<a>` 요소에 대해 동일한 구문을 사용 합니다. URL에는 "웹 사이트의 루트"를 의미 하는 `~` 포함 되어 있습니다.

## <a name="testing-the-movie-update-process"></a>동영상 업데이트 프로세스 테스트

이제를 테스트할 수 있습니다. 동영상 페이지 *를* 실행 하 고 동영상 옆의 **편집** 을 클릭 합니다. *Editmovie* 페이지가 표시 되 면 동영상을 변경 하 고 **변경 내용 전송**을 클릭 합니다. 영화 목록이 표시 되 면 변경 내용이 표시 되는지 확인 합니다.

유효성 검사가 작동 하는지 확인 하려면 다른 동영상에 대해 **편집** 을 클릭 합니다. *Editmovie* 페이지로 이동 하는 경우 **장르** 필드 (또는 **연도** 필드 또는 둘 다)의 선택을 취소 하 고 변경 내용을 제출 합니다. 다음과 같이 오류가 표시 됩니다.

![유효성 검사 오류를 보여 주는 동영상 편집 페이지](updating-data/_static/image4.png)

**영화 목록으로 돌아가기** 링크를 클릭 하 여 변경 내용을 중단 하 고 *동영상* 페이지로 돌아갑니다.

## <a name="coming-up-next"></a>다음에서 시작

다음 자습서에서는 영화 레코드를 삭제 하는 방법을 알아봅니다.

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a>동영상에 대 한 목록 완료 페이지 (편집 링크를 사용 하 여 업데이트 됨)

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a>동영상 편집 페이지의 전체 페이지 목록

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](../../getting-started/introducing-razor-syntax-c.md)
- W3Schools 사이트의 [SQL UPDATE 문](http://www.w3schools.com/sql/sql_update.asp)

> [!div class="step-by-step"]
> [이전](entering-data.md)
> [다음](deleting-data.md)
