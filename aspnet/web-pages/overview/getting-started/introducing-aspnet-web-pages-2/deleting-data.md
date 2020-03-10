---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: ASP.NET 웹 페이지-데이터베이스 데이터 삭제 소개 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다. ASP.NET 웹 Pa에서 데이터베이스 데이터를 업데이트 하 여 시리즈를 완료 했다고 가정 합니다.
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78510461"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a>ASP.NET 웹 페이지 소개-데이터베이스 데이터 삭제

만든 사람 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서에서는 개별 데이터베이스 항목을 삭제 하는 방법을 보여 줍니다. [ASP.NET 웹 페이지에서 데이터베이스 데이터를 업데이트](updating-data.md)하 여 계열을 완료 했다고 가정 합니다.
> 
> 학습할 내용:
> 
> - 레코드 목록에서 개별 레코드를 선택 하는 방법
> - 데이터베이스에서 단일 레코드를 삭제 하는 방법
> - 특정 단추를 폼에서 클릭 했는지 확인 하는 방법
>   
> 
> 설명 하는 기능/기술:
> 
> - `WebGrid` 도우미입니다.
> - SQL `Delete` 명령입니다.
> - SQL `Delete` 명령을 실행 하는 `Database.Execute` 메서드입니다.

## <a name="what-youll-build"></a>만들 내용

이전 자습서에서는 기존 데이터베이스 레코드를 업데이트 하는 방법을 알아보았습니다. 이 자습서는 레코드를 업데이트 하는 대신 삭제 하는 것을 제외 하 고는 유사 합니다. 이러한 프로세스는 거의 동일 합니다. 단, 삭제가 더 간단 하기 때문에이 자습서는 짧습니다.

*동영상* 페이지에서 이전에 추가한 **편집** 링크와 함께 각 동영상 옆에 있는 **삭제** 링크를 표시 하도록 `WebGrid` 도우미를 업데이트 합니다.

![각 영화에 대 한 삭제 링크를 보여 주는 동영상 페이지](deleting-data/_static/image1.png)

편집과 마찬가지로, **삭제** 링크를 클릭 하면 동영상 정보가 이미 양식에 있는 다른 페이지로 이동 합니다.

![동영상이 표시 된 동영상 페이지 삭제](deleting-data/_static/image2.png)

그런 다음 단추를 클릭 하 여 레코드를 영구적으로 삭제할 수 있습니다.

## <a name="adding-a-delete-link-to-the-movie-listing"></a>동영상 목록에 삭제 링크 추가

먼저 `WebGrid` 도우미에 **삭제** 링크를 추가 합니다. 이 링크는 이전 자습서에서 추가한 **편집** 링크와 비슷합니다.

*영화 cshtml* 파일을 엽니다.

열을 추가 하 여 페이지 본문의 `WebGrid` 태그를 변경 합니다. 수정 된 태그는 다음과 같습니다.

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

새 열은 다음과 같습니다.

[!code-html[Main](deleting-data/samples/sample2.html)]

표를 구성 하는 방법은 **편집** 열이 표의 맨 위에 있고 **삭제** 열은 가장 오른쪽입니다. (현재는 `Year` 열 뒤에 쉼표가 있습니다. 이러한 링크 열이 이동 하는 위치에 대 한 특별 한 사항은 없으며, 서로에 게 쉽게 배치할 수 있습니다. 이 경우 혼합 하는 것이 더 어려워집니다.

![편집 및 세부 정보 링크가 있는 동영상 페이지는 서로 옆에 있지 않은 것으로 표시 됩니다.](deleting-data/_static/image3.png)

새 열은 텍스트가 "Delete" 라고 표시 된 링크 (`<a>` 요소)를 표시 합니다. 링크의 대상 (`href` 특성)은 다음 URL과 같이 궁극적으로 확인 되는 코드로, 각 동영상 마다 `id` 값이 다릅니다.

[!code-css[Main](deleting-data/samples/sample3.css)]

이 링크는 *DeleteMovie* 라는 페이지를 호출 하 고 선택한 영화 ID를 전달 합니다.

이 자습서는 이전 자습서의 **편집** 링크와 거의 동일 하기 때문에이 링크를 생성 하는 방법에 대해서는 자세히 다루지 않습니다 ([ASP.NET 웹 페이지의 데이터베이스 데이터 업데이트](updating-data.md)).

## <a name="creating-the-delete-page"></a>삭제 페이지 만들기

이제 표에서 **삭제** 링크의 대상이 될 페이지를 만들 수 있습니다.

> [!NOTE] 
> 
> **중요** 먼저 삭제할 레코드를 선택 하 고 별도의 페이지 및 단추를 사용 하 여 프로세스를 확인 하는 방법은 보안에 매우 중요 합니다. 이전 자습서에서 읽은 것 처럼 웹 사이트를 변경 하는 것은 *항상* HTTP POST 작업을 사용 하는 양식 &mdash;를 사용 하 여 수행 해야 합니다. 링크를 클릭 하 여 사이트를 변경 (즉, 가져오기 작업 사용) 할 수 있는 경우 사용자가 사이트에 대 한 간단한 요청을 만들고 데이터를 삭제할 수 있습니다. 사이트를 인덱싱하는 검색 엔진 크롤러도 다음 링크를 통해 실수로 데이터를 삭제할 수 있습니다.
> 
> 앱에서 사용자가 레코드를 변경할 수 있는 경우 편집을 위해 사용자에 게 레코드를 표시 해야 합니다. 그러나 레코드를 삭제 하는 경우이 단계를 건너뛸 수 있습니다. 그러나이 단계를 건너뛰지 마십시오. 사용자가 레코드를 확인 하 고 의도 한 레코드를 삭제 하 고 있는지 확인 하는 것도 유용 합니다.
> 
> 이후 자습서 집합에서 사용자가 레코드를 삭제 하기 전에 로그인 해야 하는 로그인 기능을 추가 하는 방법을 확인할 수 있습니다.

*DeleteMovie* 라는 페이지를 만들고 파일의 내용을 다음 태그로 바꿉니다.

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

이 태그는 텍스트 상자 (`<input type="text">`)를 사용 하는 대신 `<span>` 요소를 포함 하는 것을 제외 하 고는 *Editmovie* 페이지와 비슷합니다. 편집할 항목이 없습니다. 사용자가 오른쪽 동영상을 삭제 하 고 있는지 확인할 수 있도록 영화 세부 정보를 표시 하면 됩니다.

태그에는 사용자가 동영상 목록 페이지로 돌아갈 수 있는 링크가 이미 포함 되어 있습니다.

*Editmovie* 페이지에서와 같이 선택한 동영상의 ID는 숨겨진 필드에 저장 됩니다. 이는 첫 번째 위치의 페이지에 쿼리 문자열 값으로 전달 됩니다. 유효성 검사 오류를 표시 하는 `Html.ValidationSummary` 호출이 있습니다. 이 경우 페이지에 전달 된 영화 ID가 없거나 동영상 ID가 잘못 된 경우 오류가 발생할 수 있습니다. 이 상황은 다른 사람이 *영화* 페이지에서 영화를 먼저 선택 하지 않고이 페이지를 실행 한 경우에 발생할 수 있습니다.

단추 캡션은 **동영상 삭제**이며 해당 name 특성은 `buttonDelete`로 설정 됩니다. `name` 특성은 폼을 전송한 단추를 식별 하기 위해 코드에서 사용 됩니다.

1\) 코드를 작성 해야 합니다. 페이지가 처음 표시 될 때 영화 세부 정보를 읽고 사용자가 단추를 클릭 하면 동영상이 실제로 삭제 됩니다.

## <a name="adding-code-to-read-a-single-movie"></a>단일 영화를 읽기 위한 코드 추가

*DeleteMovie* 페이지 위쪽에 다음 코드 블록을 추가 합니다.

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

이 태그는 *Editmovie* 페이지의 해당 코드와 동일 합니다. 쿼리 문자열에서 영화 ID를 가져오고 ID를 사용 하 여 데이터베이스에서 레코드를 읽습니다. 이 코드는 페이지에 전달 되는 영화 ID가 유효한 지 확인 하기 위해 유효성 검사 테스트 (`IsInt()` 및 `row != null`)를 포함 합니다.

이 코드는 페이지가 처음 실행 될 때만 실행 해야 합니다. 사용자가 **동영상 삭제** 단추를 클릭할 때 데이터베이스에서 동영상 레코드를 다시 읽지 않으려고 합니다. 따라서 영화를 읽는 코드는 *요청이 post 작업 (양식 전송)이 아닌 경우*에 `if(!IsPost)` &mdash; 있음을 나타내는 테스트 내에 있습니다.

## <a name="adding-code-to-delete-the-selected-movie"></a>선택한 동영상을 삭제 하는 코드 추가

사용자가 단추를 클릭할 때 동영상을 삭제 하려면 `@` 블록의 닫는 중괄호 바로 안에 다음 코드를 추가 합니다.

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

이 코드는 기존 레코드를 업데이트 하는 코드와 유사 하지만 더 간단 합니다. 이 코드는 기본적으로 SQL `Delete` 문을 실행 합니다.

 *Editmovie* 페이지에서와 같이 코드는 `if(IsPost)` 블록에 있습니다. 이번에는 `if()` 조건이 약간 더 복잡 합니다. 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

여기에는 두 가지 조건이 있습니다. 첫 번째는 `if(IsPost)`&mdash; 하기 전에 표시 된 페이지를 전송 하는 것입니다.

두 번째 조건은 `!Request["buttonDelete"].IsEmpty()`이며,이는 요청에 `buttonDelete`라는 개체가 있음을 의미 합니다. 이는 폼을 제출한 단추를 간접적으로 테스트 하는 것입니다. 양식에 여러 전송 단추가 있는 경우 클릭 한 단추의 이름만 요청에 표시 됩니다. 따라서 논리적으로 특정 단추의 이름이 요청 &mdash;에 표시 되거나 코드에 명시 된 대로 표시 되는 경우 해당 단추가 비어 있지 않으면 폼을 전송한 단추 &mdash;.

`&&` 연산자는 "and" (논리적 AND)를 의미 합니다. 따라서 전체 `if` 조건은 ...입니다.

*이 요청은 post (첫 번째 시간 요청이 아님)입니다.*  
  
 AND  
  
`buttonDelete`단추 *는* *폼을 전송 하는 단추입니다.*

이 폼에는 하나의 단추만 포함 되어 있으므로 `buttonDelete`에 대 한 추가 테스트는 기술적으로 필요 하지 않습니다. 계속 해 서 데이터를 영구적으로 제거 하는 작업을 수행 하려고 합니다. 사용자가 명시적으로 요청한 경우에만 작업을 수행 하는 것이 가능한 지 확인할 수 있습니다. 예를 들어이 페이지를 나중에 확장 하 고 다른 단추를 추가 했다고 가정 합니다. 이 경우에도 `buttonDelete` 단추를 클릭 한 경우에만 동영상을 삭제 하는 코드가 실행 됩니다.

*Editmovie* 페이지에서와 같이 hidden 필드에서 ID를 가져온 다음 SQL 명령을 실행 합니다. `Delete` 문의 구문은 다음과 같습니다.

`DELETE FROM table WHERE ID = value`

`WHERE` 절과 ID를 포함 하는 것이 중요 합니다. WHERE 절을 생략 하면 *테이블의 모든 레코드가 삭제*됩니다. 표시 된 대로 자리 표시자를 사용 하 여 ID 값을 SQL 명령에 전달 합니다.

## <a name="testing-the-movie-delete-process"></a>동영상 삭제 프로세스 테스트

이제를 테스트할 수 있습니다. 동영상 페이지 *를* 실행 하 고 동영상 옆의 **삭제** 를 클릭 합니다. *DeleteMovie* 페이지가 표시 되 면 **동영상 삭제**를 클릭 합니다.

![동영상 삭제 단추가 강조 표시 된 동영상 삭제](deleting-data/_static/image4.png)

이 단추를 클릭 하면 코드가 영화를 삭제 하 고 동영상 목록으로 돌아갑니다. 여기에서 삭제 된 동영상을 검색 하 고 삭제 되었는지 확인할 수 있습니다.

## <a name="coming-up-next"></a>다음에서 시작

다음 자습서에서는 사이트의 모든 페이지에 공통적인 모양과 레이아웃을 제공 하는 방법을 보여 줍니다.

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a>동영상에 대 한 목록 완료 페이지 (Delete 링크로 업데이트 됨)

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a>DeleteMovie 페이지에 대 한 전체 목록

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a>추가 리소스

- [Razor 구문을 사용한 ASP.NET 웹 프로그래밍 소개](../introducing-razor-syntax-c.md)
- W3Schools 사이트의 [SQL DELETE 문](http://www.w3schools.com/sql/sql_delete.asp)

> [!div class="step-by-step"]
> [이전](updating-data.md)
> [다음](layouts.md)
