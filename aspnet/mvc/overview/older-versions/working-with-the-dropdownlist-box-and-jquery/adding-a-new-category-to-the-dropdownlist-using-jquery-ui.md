---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: JQuery UI를 사용 하 여 DropDownList에 새 범주 추가 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: cb9053593e2ea788638aec063c845cb91121861b
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075114"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a>jQuery UI를 사용하여 DropDownList에 새 범주 추가

[Rick Anderson]((https://twitter.com/RickAndMSFT))

HTML `Select` 태그는 고정 된 범주 데이터의 목록을 제공 하는 데 이상적 이지만 새 범주를 추가 해야 하는 경우가 종종 있습니다. 데이터베이스의 범주에 "Opera" 장르를 추가 하려고 한다고 가정 합니다. 이 섹션에서는 jQuery UI를 사용 하 여 새 범주를 추가 하는 데 사용할 수 있는 대화 상자를 추가 합니다. 아래 이미지는 브라우저에서 UI가 표시 되는 방법을 보여 줍니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

사용자가 **새 장르 추가** 링크를 선택 하면 팝업 대화 상자에 사용자에 게 새 장르 이름과 설명 (선택 사항)을 입력 하 라는 메시지가 표시 됩니다. 아래 이미지는 **장르 추가** 팝업 대화 상자를 표시 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

새 장르 이름을 입력 하면 **저장** 단추가 푸시되 면 다음과 같은 상황이 발생 합니다.

1. AJAX 호출은 장르 컨트롤러의 Create 메서드에 데이터를 게시 합니다. 그러면 새 장르를 데이터베이스에 저장 하 고 새 장르 정보 (장르 이름 및 ID)를 JSON으로 반환 합니다.
2. JavaScript는 새 장르 데이터를 선택 목록에 추가 합니다.
3. JavaScript는 새 장르를 선택한 항목으로 만듭니다.

   아래 이미지에서 **Opera** 는 데이터베이스에 추가 되 고 **장르** 드롭다운 목록에서 선택 되었습니다. 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

*Views\StoreManager\Create.cshtml* 파일을 열고 장르 태그를 다음 코드로 바꿉니다.

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

`_ChooseGenre` 부분 보기에는 새 장르 추가 기능을 구현 하는 데 사용 되는 JavaScript 및 jQuery를 연결 하는 모든 논리가 포함 됩니다. 코드를 완료 한 후에는 음악가 UI를 사용 하 여 동일한 작업을 수행 하는 것이 간단 합니다.

솔루션 탐색기에서 *Views\StoreManager* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **보기**를 선택 합니다. **보기 이름** 입력에 `_ChooseGenre`를 입력 하 고 **추가**를 선택 합니다. *Views\StoreManager\\_ChooseGenre* 의 태그를 다음으로 바꿉니다.

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

첫 번째 줄은 모델 처럼 `Album`를 전달 한다는 것을 선언 하 고, Create view에 있는 동일한 모델 문을 정확히 검색 합니다. 다음 줄은 **레이블** 도우미 태그입니다. 다음 줄은 원래 Create view와 정확히 같은 **DropDownList** 도우미 호출입니다. 다음 줄은 `Add New Genre`이름이 있는 링크를 추가 하 고 단추 처럼 스타일을 만듭니다. `ValidationMessageFor`를 포함 하는 줄은 Create view에서 직접 복사 됩니다. 다음 줄:

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

ID가 `genreDialog`인 숨겨진 div를 만듭니다. JQuery를 사용 하 여이 div의 ID `genreDialog`를 사용 하 여 **장르 추가** 대화 상자를 연결 합니다. 마지막 두 스크립트 태그에는 새 장르 추가 기능을 구현 하는 데 사용할 JavaScript 파일에 대 한 링크가 포함 되어 있습니다. */Scripts/chooseGenre.js* 파일은 프로젝트에 제공 되며 자습서의 뒷부분에서 살펴보겠습니다.

응용 프로그램을 실행 하 고 **새 장르 추가** 단추를 클릭 합니다. **장르 추가** 대화 상자에서 **이름** 입력 상자에 **Opera** 를 입력 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

**저장** 단추를 클릭합니다. AJAX 호출은 Opera 범주를 만든 다음 Opera를 사용 하 여 드롭다운 목록을 채우고 Opera를 선택 된 장르로 설정 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

음악가, 제목 및 가격을 입력 한 다음 **만들기** 단추를 선택 합니다. $8.99 보다 작은 가격을 입력 하면 새 앨범이 인덱스 보기의 맨 위에 표시 됩니다. 새 앨범 항목이 데이터베이스에 저장 되었는지 확인 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

한 문자만 사용 하 여 새 장르를 만들어 보세요. *Models\genre.cs* 파일의 다음 코드는 장르 이름의 최소 및 최대 길이를 설정 합니다.

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

클라이언트 쪽 유효성 검사 보고서 2 ~ 007e; 20 자 사이의 문자열을 입력 해야 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a>데이터베이스 및 선택 목록에 새 장르를 추가 하는 방법을 검토 합니다.

*Scripts\chooseGenre.js* 파일을 열고 코드를 검사 합니다.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

두 번째 줄은 ID `genreDialog`를 사용 하 여 *Views\StoreManager\\_ChooseGenre. cshtml* 파일의 div 태그에 대화 상자를 만듭니다. 대부분의 명명 된 매개 변수는 자체 설명이 필요 합니다. `autoOpen` 매개 변수는 false로 설정 되 고, **장르 만들기** 단추를 선택 하면 대화 상자가 명시적으로 열립니다 (이에 대 한 뒷부분에서 설명). 대화 상자에는 **저장** 및 **취소**단추가 있습니다. **취소** 단추를 클릭 하면 대화 상자가 닫힙니다. 다음 코드에서는 **저장** 단추 함수를 보여 줍니다.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

`var createGenreForm` `createGenreForm` ID에서 선택 됩니다. `createGenreForm` ID는 *Views\Genre\\_CreateGenre. cshtml* 파일에 있는 다음 코드에서 설정 되었습니다.

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

*Views\Genre\\_CreateGenre* 에서 사용 되는 [html. html.beginform](https://msdn.microsoft.com/library/dd492714.aspx) 도우미 오버 로드는 폼을 전송 하기 위한 URL이 포함 된 action 특성으로 html을 생성 합니다. 브라우저에서 앨범 만들기 페이지를 표시 하 고 브라우저에서 소스 표시를 선택 하 여이를 확인할 수 있습니다. 다음 태그는 form 태그를 포함 하는 생성 된 HTML을 보여 줍니다.

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

JQuery `$.post` 줄은 작업 특성 (`/StoreManager/Create`)에 대 한 AJAX 호출을 수행 하 고 **장르 만들기** 대화 상자에서 데이터를 전달 합니다. 데이터는 새 장르 이름과 설명 (선택 사항)으로 구성 됩니다. AJAX 호출에 성공 하면 새 장르 이름과 값이 선택 태그에 추가 되 고 새 장르는 선택한 값으로 설정 됩니다. 이는 동적으로 생성 된 태그 이므로 브라우저에서 소스를 확인 하 여 새 선택 옵션을 볼 수 없습니다. IE 9 F12 개발자 도구를 사용 하 여 새 HTML을 볼 수 있습니다. 새 선택 옵션을 보려면 Internet Explorer 9에서 F12 키를 눌러 F12 개발자 도구를 시작 합니다. 만들기 페이지로 이동 하 고 새 장르를 추가 하 여 장르 선택 목록에서 새 장르를 선택 합니다. F12 개발자 도구:

1. HTML 탭을 선택 합니다.
2. 새로 고침 아이콘을 누릅니다.  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. 검색 상자에 GenreID를 입력 합니다.
4. 다음 아이콘을 사용 하 여   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   다음 select 태그로 이동 합니다.

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. 마지막 옵션 값을 확장 합니다.

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

*Scripts\chooseGenre.js* 파일의 다음 코드는 **새 장르 추가** 단추가 클릭 이벤트에 연결 되는 방법 및 **새 장르 추가** 대화 상자를 만드는 방법을 보여 줍니다.

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

첫 번째 줄에서는 **새 장르 추가** 단추에 연결 된 클릭 함수를 만듭니다. Views\StoreManager\\_ChooseGenre 파일의 다음 태그는 **새 장르 추가** 단추가 만들어지는 방법을 보여 줍니다.

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

Load 메서드는 장르 추가 대화 상자를 만들고 열고 jQuery `parse` 메서드를 호출 하 여 대화 상자에 입력 한 데이터에서 클라이언트 유효성 검사가 수행 되도록 합니다.

이 섹션에서는 선택 목록에 새 범주 데이터를 추가 하는 데 사용할 수 있는 대화 상자를 만드는 방법에 대해 알아보았습니다. 동일한 절차에 따라 새 음악가를 음악가 선택 목록에 추가 하는 UI를 만들 수 있습니다. 이 자습서에서는 ASP.NET MVC HTML 도우미 **DropDownList**사용에 대 한 개요를 제공 합니다. **DropDownList**사용에 대 한 자세한 내용은 아래의 추가 참조 섹션을 참조 하세요. 이 자습서를 통해 도움이 되는 경우 알려주세요.

Rick.Anderson[at]Microsoft.com

### <a name="additional-references"></a>추가 참조

- [ASP.NET MVC – 계단식 드롭다운 목록](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [Radu Enuca의](https://weblogs.asp.net/raduenuca/default.aspx) 자습서
- [선택](https://harvesthq.github.com/chosen/) 다중 선택 및 필터링을 지 원하는 JavaScript 플러그 인입니다.

### <a name="contributors"></a>참가자

- [Radu Ena](https://weblogs.asp.net/raduenuca/default.aspx)
- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)

### <a name="reviewers"></a>검토자

- Jean-Sébastien Goupil
- [Brad Wilson](http://bradwilson.typepad.com/)
- Mike Pope
- Tom Dykstra

> [!div class="step-by-step"]
> [이전](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
