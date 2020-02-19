---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: ASP.NET MVC가 DropDownList 도우미를 스 캐 폴드 하는 방식 검사 | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457611"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a>ASP.NET MVC가 DropDownList 도우미를 스캐폴드하는 방법 검사

[Rick Anderson](https://twitter.com/RickAndMSFT)

**솔루션 탐색기**에서 *Controllers* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **컨트롤러 추가**를 선택 합니다. 컨트롤러 이름을 **StoreManagerController**로 합니다. 아래 이미지에 표시 된 것 처럼 **컨트롤러 추가** 대화 상자에 대 한 옵션을 설정 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

*StoreManager\Index.cshtml* view를 편집 하 고 `AlbumArtUrl`를 제거 합니다. `AlbumArtUrl` 제거 하면 프레젠테이션을 더 쉽게 읽을 수 있습니다. 완성된 코드는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

*Controllers\StoreManagerController.cs* 파일을 열고 `Index` 메서드를 찾습니다. `OrderBy` 절을 추가 하 여 앨범이 가격을 기준으로 정렬 됩니다. 전체 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

가격을 기준으로 정렬 하면 데이터베이스의 변경 내용을 보다 쉽게 테스트할 수 있습니다. 편집 및 만들기 메서드를 테스트할 때 낮은 가격을 사용 하 여 저장 된 데이터가 먼저 표시 되도록 할 수 있습니다.

*StoreManager\Edit.cshtml* 파일을 엽니다. 범례 태그 바로 뒤에 다음 줄을 추가 합니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

다음 코드는이 변경 내용의 컨텍스트를 보여 줍니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

앨범 레코드를 변경 하려면 `AlbumId` 필요 합니다.

Ctrl+F5를 눌러 애플리케이션을 실행합니다. **관리자** 링크를 선택 하 고 **새로 만들기** 링크를 선택 하 여 새 앨범을 만듭니다. 앨범 정보가 저장 되었는지 확인 합니다. 앨범을 편집 하 고 변경한 내용이 유지 되는지 확인 합니다.

### <a name="the-album-schema"></a>앨범 스키마

MVC 스 캐 폴딩 메커니즘을 사용 하 여 만든 `StoreManager` 컨트롤러는 music 저장소 데이터베이스의 앨범에 대 한 CRUD (만들기, 읽기, 업데이트, 삭제) 액세스를 허용 합니다. 앨범 정보에 대 한 스키마는 다음과 같습니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

`Albums` 테이블은 앨범 장르 및 설명을 저장 하지 않으며 `Genres` 테이블에 외래 키를 저장 합니다. `Genres` 테이블에는 장르 이름 및 설명이 포함 되어 있습니다. 마찬가지로 `Albums` 테이블에는 앨범 아티스트 이름 뿐만 아니라 `Artists` 테이블에 대 한 외래 키가 포함 되어 있습니다. `Artists` 테이블은 음악가의 이름을 포함 합니다. `Albums` 테이블의 데이터를 검사 하는 경우 각 행에 `Genres` 테이블에 대 한 외래 키와 `Artists` 테이블에 대 한 외래 키가 포함 되어 있는 것을 볼 수 있습니다. 아래 이미지는 `Albums` 테이블의 일부 테이블 데이터를 표시 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a>HTML Select 태그

Html [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 도우미에서 만든 html `<select>` 요소는 전체 값 목록 (예: 장르 목록)을 표시 하는 데 사용 됩니다. 편집 폼의 경우 현재 값을 알고 있는 경우 선택 목록에 현재 값이 표시 될 수 있습니다. 이전에 선택한 값을 **코미디**로 설정 하는 경우이에 대해 살펴보았습니다. Select 목록은 범주 또는 외래 키 데이터를 표시 하는 데 적합 합니다. 장르 외래 키에 대 한 `<select>` 요소는 가능한 장르 이름 목록을 표시 하지만 양식을 저장할 때 장르 속성은 표시 된 장르 이름이 아니라 장르 외래 키 값으로 업데이트 됩니다. 아래 이미지에서 선택 된 장르는 **Disco** 이며 음악가는 **Donna 여름**입니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a>ASP.NET MVC 스 캐 폴드 코드 검사

*Controllers\StoreManagerController.cs* 파일을 열고 `HTTP GET Create` 메서드를 찾습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

`Create` 메서드는 두 개의 [Selectlist](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) 개체를 `ViewBag`에 추가 하 고 하나는 장르 정보를 포함 하 고 다른 하나는 음악가 정보를 포함 합니다. 위에서 사용 된 [Selectlist](https://msdn.microsoft.com/library/dd505286.aspx) 생성자 오버 로드에는 세 개의 인수가 사용 됩니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. *items*: 목록의 항목을 포함 하는 [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) 입니다. 위의 예제에서는 `db.Genres`에서 반환 된 장르 목록을 표시 합니다.
2. *Datavaluefield*: 키 값을 포함 하는 **IEnumerable** 목록의 속성 이름입니다. 위의 예제에서 `GenreId` 하 고 `ArtistId`합니다.
3. *dataTextField*: 표시할 정보를 포함 하는 **IEnumerable** 목록의 속성 이름입니다. 음악가와 장르 테이블 모두에 `name` 필드가 사용 됩니다.

*Views\StoreManager\Create.cshtml* 파일을 열고 장르 필드에 대 한 `Html.DropDownList` 도우미 태그를 검사 합니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

첫 번째 줄에서는 create view가 `Album` 모델을 사용 하는 것을 보여 줍니다. 위에 표시 된 `Create` 메서드에서는 모델이 전달 되지 않으므로 뷰가 **null** `Album` 모델을 가져옵니다. 이 시점에서 새로운 앨범을 만드는 중 이므로 `Album` 데이터가 없습니다.

위에 표시 된 [Html DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) 오버 로드는 모델에 바인딩할 필드의 이름을 사용 합니다. 또한이 이름을 사용 하 여 [Selectlist](https://msdn.microsoft.com/library/dd505286.aspx) 개체를 포함 하는 **viewbag** 개체를 찾습니다. 이 오버 로드를 사용 하 여 `GenreId`**Viewbag SelectList** 개체의 이름을 입력 해야 합니다. 두 번째 매개 변수 (`String.Empty`)는 선택 된 항목이 없을 때 표시 되는 텍스트입니다. 새 앨범을 만들 때이 작업을 수행 하는 것이 좋습니다. 두 번째 매개 변수를 제거 하 고 다음 코드를 사용 하는 경우:

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

Select 목록은 기본적으로 첫 번째 요소 또는 샘플에서 록 표시 됩니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

`HTTP POST Create` 메서드 검사

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

`Create` 메서드의이 오버 로드는 게시 된 양식 값에서 ASP.NET MVC 모델 바인딩 시스템에 의해 생성 되는 `album` 개체를 사용 합니다. 새 앨범을 제출할 때 모델 상태가 올바르지만 데이터베이스 오류가 없으면 새 앨범이 데이터베이스에 추가 됩니다. 다음 이미지는 새 앨범을 만드는 방법을 보여 줍니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

[Fiddler 도구](http://www.fiddler2.com/fiddler2/) 를 사용 하 여 ASP.NET MVC 모델 바인딩에서 앨범 개체를 만드는 데 사용 하는 게시 된 양식 값을 검사할 수 있습니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png)입니다.

### <a name="refactoring-the-viewbag-selectlist-creation"></a>ViewBag SelectList 만들기를 리팩터링 합니다.

`Edit` 메서드와 `HTTP POST Create` 메서드는 모두 **Viewbag**에서 **selectlist** 를 설정 하는 동일한 코드를 가집니다. 이 [연습](http://en.wikipedia.org/wiki/Don't_repeat_yourself)에서는이 코드를 리팩터링할 예정입니다. 이 리팩터링 코드는 나중에 사용 합니다.

새 메서드를 만들어 장르 및 음악가 **Selectlist** 를 **viewbag**에 추가 합니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

각 `Create`의 `ViewBag` 설정 하 고 `SetGenreArtistViewBag` 메서드를 호출 하는 `Edit` 메서드를 설정 하는 두 줄을 바꿉니다. 완성된 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

새 앨범을 만들고 앨범을 편집 하 여 변경 내용이 작동 하는지 확인 합니다.

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a>SelectList를 DropDownList에 명시적으로 전달

ASP.NET MVC 스 캐 폴딩에서 만든 만들기 및 편집 뷰는 다음과 같은 **DropDownList** 오버 로드를 사용 합니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

Create view의 `DropDownList` 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

`SelectList`에 대 한 `ViewBag` 속성의 이름은 `GenreId`이므로 **DropDownList** 도우미는 **viewbag**의 `GenreId`**selectlist** 를 사용 합니다. 다음 **DropDownList** 오버 로드에서 `SelectList`은 명시적으로 전달 됩니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

*Views\StoreManager\Edit.cshtml* 파일을 열고 위의 오버 로드를 사용 하 여 **selectlist**를 명시적으로 전달 하도록 **DropDownList** 호출을 변경 합니다. 장르 범주에 대해이 작업을 수행 합니다. 완성 된 코드는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

응용 프로그램을 실행 하 고 **관리자** 링크를 클릭 한 다음 재즈 앨범으로 이동 하 여 **편집** 링크를 선택 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

현재 선택 된 장르로 재즈를 표시 하는 대신 바위가 표시 됩니다. 문자열 인수 (바인딩할 속성)와 **Selectlist** 개체의 이름이 같은 경우에는 선택한 값이 사용 되지 않습니다. 선택한 값이 없는 경우 브라우저는 기본적으로 **Selectlist**의 첫 번째 요소 (위 예제의 경우 **바위** )로 지정 됩니다. 이는 **DropDownList** 도우미의 알려진 제한 사항입니다.

*Controllers\StoreManagerController.cs* 파일을 열고 **selectlist** 개체 이름을 `Genres`로 변경 하 고 `Artists`합니다. 완성 된 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

장르 이름 및 음악가 이름에는 각 범주의 ID 외에도 더 많은 범주가 포함 되어 있습니다. 앞서 지불 했던 리팩터링 네 가지 방법으로 **Viewbag** 를 변경 하는 대신 변경 내용을 `SetGenreArtistViewBag` 메서드로 격리 했습니다.

Create 및 edit 뷰에서 **DropDownList** 호출을 변경 하 여 새 **selectlist** 이름을 사용 합니다. 편집 뷰의 새 태그는 다음과 같습니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

SelectList의 첫 번째 항목이 표시 되지 않도록 하려면 Create view에 빈 문자열이 필요 합니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

새 앨범을 만들고 앨범을 편집 하 여 변경 내용이 작동 하는지 확인 합니다. 바위 이외의 장르를 사용 하 여 앨범을 선택 하 여 편집 코드를 테스트 합니다.

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a>DropDownList 도우미와 함께 뷰 모델 사용

ViewModels 폴더에 `AlbumSelectListViewModel`라는 새 클래스를 만듭니다. `AlbumSelectListViewModel` 클래스의 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

`AlbumSelectListViewModel` 생성자는 앨범 및 음악가의 목록을 사용 하 고 장르 및 음악가의 앨범 및 `SelectList` 포함 된 개체를 만듭니다.

다음 단계에서 뷰를 만들 때 `AlbumSelectListViewModel`를 사용할 수 있도록 프로젝트를 빌드합니다.

`StoreManagerController`에 `EditVM` 메서드를 추가 합니다. 완성된 코드는 다음과 같습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

`AlbumSelectListViewModel`를 마우스 오른쪽 단추로 클릭 하 고 **해결**을 선택한 다음 **MvcMusicStore를 사용**합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

또는 다음 using 문을 추가할 수 있습니다.

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

`EditVM`를 마우스 오른쪽 단추로 클릭 하 고 **뷰 추가**를 선택 합니다. 아래에 표시 된 옵션을 사용 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

**추가**를 선택 하 고 *Views\StoreManager\EditVM.cshtml* 파일의 내용을 다음으로 바꿉니다.

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

`EditVM` 태그는 다음과 같은 예외를 제외 하 고 원래 `Edit` 태그와 매우 비슷합니다.

- `Edit` 뷰의 모델 속성은 `model.property`형식 (예: `model.Title`)입니다. `EditVm` 뷰의 모델 속성은 `model.Album.property`형식 (예: `model.Album.Title`)입니다. 이는 `EditVM` 뷰에 `Edit` 뷰에서와 `Album` 아닌 `Album`에 대 한 컨테이너가 전달 되기 때문입니다.
- **DropDownList** 두 번째 매개 변수는 **viewbag**아닌 뷰 모델에서 제공 됩니다.
- `EditVM` 뷰의 **html.beginform** 도우미는 `Edit` 작업 메서드에 명시적으로 다시 게시 합니다. `Edit` 작업에 다시 게시 하면 `HTTP POST EditVM` 작업을 작성할 필요가 없으며 `HTTP POST` `Edit` 작업을 다시 사용할 수 있습니다.

응용 프로그램을 실행 하 고 앨범을 편집 합니다. `EditVM`사용 하도록 URL을 변경 합니다. 필드를 변경 하 고 **저장** 단추를 눌러 코드가 작동 하는지 확인 합니다.

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a>어떤 방법을 사용 해야 하나요?

표시 되는 세 가지 방법을 모두 사용할 수 있습니다. 대부분의 개발자는 `ViewBag`를 사용 하 여 `SelectList`를 `DropDownList`에 명시적으로 전달 하는 것을 선호 합니다. 이 방법에는 컬렉션에 보다 적절 한 이름을 사용 하는 유연성을 제공 하는 추가적인 이점이 있습니다. 한 가지 주의할 점은 `ViewBag SelectList` 개체의 이름을 모델 속성과 같은 이름으로 지정할 수 없다는 것입니다.

일부 개발자는 ViewModel 접근 방식을 선호 합니다. 다른 방법으로는 더 자세한 태그를 고려 하 고 ViewModel의 생성 된 HTML을 사용 하는 것이 단점이 있습니다.

이 섹션에서는 범주 데이터와 함께 **DropDownList** 을 사용 하는 세 가지 방법을 배웠습니다. 다음 섹션에서는 새 범주를 추가 하는 방법을 보여 줍니다.

> [!div class="step-by-step"]
> [이전](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [다음](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)
