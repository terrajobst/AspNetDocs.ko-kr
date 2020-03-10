---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: '5 부: 양식 및 템플릿 편집 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 5 부에서는 편집 양식 및 템플릿을 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78450911"
---
# <a name="part-5-edit-forms-and-templating"></a>5 부: 양식 및 템플릿 편집

받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.  
>   
> MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.
> 
> 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 5 부에서는 편집 양식 및 템플릿을 다룹니다.

이전 장에서는 데이터베이스에서 데이터를 로드 하 고 표시 했습니다. 이 장에서는 데이터 편집도 사용할 수 있습니다.

## <a name="creating-the-storemanagercontroller"></a>StoreManagerController 만들기

먼저 **StoreManagerController**이라는 새 컨트롤러를 만듭니다. 이 컨트롤러의 경우 ASP.NET MVC 3 도구 업데이트에서 사용할 수 있는 스 캐 폴딩 기능을 활용 합니다. 아래와 같이 컨트롤러 추가 대화 상자에 대 한 옵션을 설정 합니다.

![](mvc-music-store-part-5/_static/image1.png)

추가 단추를 클릭 하면 ASP.NET MVC 3 스 캐 폴딩 메커니즘이 적절 한 작업을 수행 하는 것을 볼 수 있습니다.

- 로컬 Entity Framework 변수를 사용 하 여 새 StoreManagerController를 만듭니다.
- 프로젝트의 Views 폴더에 StoreManager 폴더를 추가 합니다.
- Create. cshtml, Delete. cshtml, Details, Edit. cshtml 및 Index. cshtml 뷰를 추가 합니다 .이는 앨범 클래스에 강력한 형식입니다.

![](mvc-music-store-part-5/_static/image2.png)

새 StoreManager controller 클래스에는 앨범 모델 클래스로 작업 하 고 데이터베이스 액세스에 Entity Framework 컨텍스트를 사용 하는 방법을 알고 있는 CRUD (만들기, 읽기, 업데이트, 삭제) 컨트롤러 작업이 포함 되어 있습니다.

## <a name="modifying-a-scaffolded-view"></a>스 캐 폴드 뷰 수정

이 코드는이 코드를 생성 하는 동안이 자습서 전체에서 작성 한 것 처럼 표준 ASP.NET MVC 코드 임을 기억해 야 합니다. 이 도구는 상용구 컨트롤러 코드를 작성 하 고 강력한 형식의 뷰를 수동으로 만드는 데 소비 하는 시간을 절약 하기 위해 작성 되었습니다 .이는 생성 된 코드의 종류 이며, 되어서는 안됩니다 변경 하는 방법에 대 한 주석에서 디렉터리 경고 앞에서 볼 수 있습니다. code. 코드를 변경 해야 합니다.

이제 StoreManager 인덱스 보기 (/Views/StoreManager/Index.cshtml)에 대 한 빠른 편집부터 살펴보겠습니다. 이 보기에는 편집/세부 정보/삭제 링크를 사용 하 여 스토어의 앨범을 나열 하 고 앨범의 공용 속성을 포함 하는 표가 표시 됩니다. AlbumArtUrl 필드는이 표시에서 그다지 유용 하지 않으므로 제거 합니다. 보기 코드의 &lt;테이블&gt; 섹션에서 아래 강조 표시 된 줄에 표시 된 것 처럼 AlbumArtUrl references 주위의 &lt;번째&gt; 및 &lt;td&gt; 요소를 제거 합니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

수정 된 뷰 코드는 다음과 같이 표시 됩니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>저장소 관리자에 대 한 첫 번째 보기

이제 응용 프로그램을 실행 하 고/StoreManager/.로 이동 합니다. 그러면 방금 수정한 저장소 관리자 인덱스가 표시 되 고 편집, 세부 정보 및 삭제 링크를 포함 하는 스토어의 앨범 목록이 표시 됩니다.

![](mvc-music-store-part-5/_static/image3.png)

편집 링크를 클릭 하면 장르 및 음악가 드롭다운을 비롯 하 여 앨범에 대 한 필드가 포함 된 편집 양식이 표시 됩니다.

![](mvc-music-store-part-5/_static/image4.png)

아래쪽의 "목록으로 돌아가기" 링크를 클릭 한 다음 앨범에 대 한 세부 정보 링크를 클릭 합니다. 그러면 개별 앨범에 대 한 세부 정보가 표시 됩니다.

![](mvc-music-store-part-5/_static/image5.png)

다시 목록으로 돌아가기 링크를 클릭 한 다음 삭제 링크를 클릭 합니다. 그러면 앨범 세부 정보를 표시 하 고 삭제 여부를 묻는 확인 대화 상자가 표시 됩니다.

![](mvc-music-store-part-5/_static/image6.png)

맨 아래에 있는 삭제 단추를 클릭 하면 앨범이 삭제 되 고 삭제 된 앨범이 표시 되는 인덱스 페이지로 돌아갑니다.

저장소 관리자를 사용 하 여 작업을 수행 하는 것은 아니지만, CRUD 작업을 시작 하는 데 사용할 수 있는 컨트롤러와 코드를 볼 수 있습니다.

## <a name="looking-at-the-store-manager-controller-code"></a>Store Manager 컨트롤러 코드 보기

저장소 관리자 컨트롤러에는 적절 한 양의 코드가 포함 되어 있습니다. 위에서 아래로 이동 하겠습니다. 컨트롤러에는 MVC 컨트롤러에 대 한 몇 가지 표준 네임 스페이스와 모델 네임 스페이스에 대 한 참조가 포함 되어 있습니다. 컨트롤러에는 데이터 액세스에 대 한 각 컨트롤러 작업에서 사용 되는 MusicStoreEntities의 전용 인스턴스가 있습니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>저장소 관리자 인덱스 및 세부 정보 작업

인덱스 뷰는 저장소 찾아보기 방법으로 작업할 때 이전에 확인 한 각 앨범의 참조 된 장르 및 음악가 정보를 포함 하 여 앨범 목록을 검색 합니다. 인덱스 뷰는 연결 된 개체에 대 한 참조를 따라 각 앨범의 장르 이름과 음악가 이름을 표시 하 여 컨트롤러를 효율적으로 만들고 원래 요청에서이 정보를 쿼리 합니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

StoreManager 컨트롤러의 세부 정보 컨트롤러 작업은 이전에 만든 저장소 컨트롤러 세부 정보 작업과 동일 하 게 작동 합니다. 여기서는 Find () 메서드를 사용 하 여 ID로 앨범을 쿼리 한 다음이를 뷰로 반환 합니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>작업 메서드 만들기

만들기 작업 메서드는 폼 입력을 처리 하기 때문에 지금까지 살펴본 것과 약간 다릅니다. 사용자가/StoreManager/Create/를 처음 방문 하면 빈 양식이 표시 됩니다. 이 HTML 페이지에는 사용자가 앨범 세부 정보를 입력할 수 있는 드롭다운 및 텍스트 상자 입력 요소를 포함 하는 &lt;form&gt; 요소가 포함 됩니다.

사용자가 앨범 양식 값을 채운 후 "저장" 단추를 눌러 이러한 변경 내용을 응용 프로그램에 다시 제출 하 여 데이터베이스 내에 저장할 수 있습니다. 사용자가 "저장" 단추를 누르면 &lt;양식&gt;에서 HTTP post를 다시 실행 하 여/StoreManager/Create/URL에 다시 게시 하 고 &lt;형식&gt; 값을 HTTP POST의 일부로 전송 합니다.

ASP.NET MVC를 사용 하면 StoreManagerController 클래스 내에서 두 개의 별도 "Create" 작업 메서드를 구현 하 여 (/StoreManager/Create/URL에 대 한 초기 HTTP-GET 찾아보기를 처리 하는 경우), 전송 된 변경 내용에 대 한 HTTP POST를 처리 하는 두 가지 URL 호출 시나리오의 논리를 쉽게 분할할 수 있습니다.

### <a name="passing-information-to-a-view-using-viewbag"></a>ViewBag를 사용 하 여 뷰에 정보 전달

이 자습서의 앞부분에서 ViewBag를 사용 했지만 많은 이야기를 하지 않았습니다. ViewBag 강력한 형식의 모델 개체를 사용 하지 않고 뷰에 정보를 전달할 수 있도록 합니다. 이 경우 편집 HTTP-컨트롤러 가져오기 작업은 드롭다운을 채우기 위해 장르 및 음악가 목록을 폼에 전달 해야 하며,이 작업을 수행 하는 가장 간단한 방법은 ViewBag 항목으로 반환 하는 것입니다.

ViewBag는 동적 개체입니다. 즉, 이러한 속성을 정의 하는 코드를 작성 하지 않고도 여기에 ViewBag 또는 ViewBag을 입력할 수 있습니다. 이 경우 컨트롤러 코드는 GenreId 및 Viewbag를 사용 하 여 폼으로 전송 된 드롭다운 값이 GenreId 및 ArtistId (설정 되는 앨범 속성)가 되도록 합니다.

이러한 드롭다운 값은 해당 목적 으로만 빌드되는 SelectList 개체를 사용 하 여 폼으로 반환 됩니다. 다음과 같은 코드를 사용 하 여이 작업을 수행 합니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

작업 메서드 코드에서 볼 수 있듯이 다음 세 개의 매개 변수를 사용 하 여이 개체를 만듭니다.

- 드롭다운이 표시 되는 항목 목록입니다. 이것은 단지 단지 문자열만이 아니라 장르 목록을 전달 하는 것입니다.
- SelectList에 전달 되는 다음 매개 변수는 선택 된 값입니다. 이 방법으로 목록에서 항목을 미리 선택 하는 방법을 선택 하는 방법을 알 수 있습니다. 편집 양식을 살펴보면 매우 유사 하 게 이해 하는 것이 더 쉽습니다.
- 마지막 매개 변수는 표시 되는 속성입니다. 이 경우 Genre.Name 속성은 사용자에 게 표시 되는 속성 임을 나타냅니다.

이 점을 염두에 두면 HTTP-GET 만들기 작업은 매우 간단 합니다. 두 개의 SelectLists가 ViewBag에 추가 되 고 모델 개체가 폼에 전달 되지 않습니다 (아직 생성 되지 않았기 때문).

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>만들기 뷰에서 드롭다운을 표시 하는 HTML 도우미

드롭다운 값을 보기에 전달 하는 방법에 대해 알아보았습니다. 뷰를 빠르게 확인 하 여 해당 값이 표시 되는 방식을 살펴보겠습니다. 코드 보기 (/Views/StoreManager/Create.cshtml)에서 다음 호출이 장르 드롭다운을 표시 하도록 설정 된 것을 볼 수 있습니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

이를 HTML 도우미 라고 하며이는 일반적인 뷰 작업을 수행 하는 유틸리티 메서드입니다. HTML 도우미는 보기 코드를 간결 하 고 읽기 쉽게 유지 하는 데 매우 유용 합니다. ASP.NET MVC는 Html DropDownList 도우미를 제공 하지만 나중에 볼 수 있듯이 응용 프로그램에서 다시 사용할 수 있는 보기 코드에 대 한 자체 도우미를 만들 수 있습니다.

Html DropDownList 호출은 표시할 목록을 가져올 위치와 미리 선택 해야 하는 값 (있는 경우)을 지정 해야 합니다. 첫 번째 매개 변수인 GenreId은 모델 또는 ViewBag에서 GenreId 라는 값을 검색 하도록 DropDownList에 지시 합니다. 두 번째 매개 변수는 드롭다운 목록에서 처음에 선택 된 대로 표시할 값을 나타내는 데 사용 됩니다. 이 폼은 만들기 양식 이므로 미리 선택 하 고 문자열을 비워 둘 수 없습니다.

### <a name="handling-the-posted-form-values"></a>게시 된 폼 값 처리

앞서 설명한 것 처럼 각 폼과 연결 된 두 가지 작업 메서드가 있습니다. 첫 번째는 HTTP GET 요청을 처리 하 고 폼을 표시 합니다. 두 번째는 전송 된 폼 값을 포함 하는 HTTP POST 요청을 처리 합니다. 컨트롤러 작업에는 HTTP POST 요청에만 응답 해야 한다는 사실을 ASP.NET MVC에 알리는 [HttpPost] 특성이 있습니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

이 작업에는 네 가지 책임이 있습니다.

- 1. 양식 값 읽기
- 2. 양식 값이 모든 유효성 검사 규칙을 통과 하는지 확인 합니다.
- 3. 양식 제출이 유효한 경우 데이터를 저장 하 고 업데이트 된 목록을 표시 합니다.
- 4. 양식 제출이 유효 하지 않은 경우 유효성 검사 오류로 폼을 다시 표시 합니다.

#### <a name="reading-form-values-with-model-binding"></a>모델 바인딩을 사용 하 여 폼 값 읽기

컨트롤러 작업은 GenreId 및 ArtistId에 대 한 값을 포함 하는 양식 전송 (드롭다운 목록에서) 및 제목, 가격 및 AlbumArtUrl의 텍스트 상자 값을 처리 합니다. 폼 값에 직접 액세스 하는 것이 가능 하지만 ASP.NET MVC에 기본 제공 되는 모델 바인딩 기능을 사용 하는 것이 더 나은 방법입니다. 컨트롤러 작업에서 모델 형식을 매개 변수로 사용 하는 경우 ASP.NET MVC는 경로 및 querystring 값 뿐만 아니라 양식 입력을 사용 하 여 해당 형식의 개체를 채우려고 시도 합니다. 이를 위해 이름이 model 개체의 속성과 일치 하는 값을 검색 합니다. 예를 들어 새 앨범 개체의 GenreId 값을 설정 하는 경우 이름이 GenreId 인 입력을 찾습니다. ASP.NET MVC의 표준 메서드를 사용 하 여 뷰를 만들 때 폼은 항상 속성 이름을 입력 필드 이름으로 사용 하 여 렌더링 되므로 필드 이름이 일치 합니다.

#### <a name="validating-the-model"></a>모델 유효성 검사

모델의 유효성을 검사 하려면 모델의 유효성을 검사 합니다. IsValid. 아직 모든 유효성 검사 규칙을 앨범 클래스에 추가 하지 않았습니다. 지금은 약간의 작업을 수행 합니다. 이제이 검사가 그다지 많지 않습니다. 중요 한 점은이 ModelStat 검사가 모델에 적용 되는 유효성 검사 규칙에 맞게 조정 되기 때문에 유효성 검사 규칙을 나중에 변경 하려면 컨트롤러 작업 코드를 업데이트할 필요가 없습니다.

#### <a name="saving-the-submitted-values"></a>전송 된 값 저장

양식 전송에서 유효성 검사를 통과 하는 경우에는 값을 데이터베이스에 저장 해야 합니다. Entity Framework를 사용 하는 경우에는 모델을 앨범 컬렉션에 추가 하 고 SaveChanges를 호출 하기만 하면 됩니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

Entity Framework은 적절 한 SQL 명령을 생성 하 여 값을 유지 합니다. 데이터를 저장 한 후에는 업데이트를 볼 수 있도록 앨범 목록으로 다시 리디렉션됩니다. 이 작업은 표시 하려는 컨트롤러 작업의 이름으로 RedirectToAction을 반환 하 여 수행 됩니다. 이 경우 인덱스 메서드입니다.

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>유효성 검사 오류가 있는 잘못 된 양식 전송 표시

잘못 된 폼 입력의 경우 드롭다운 값이 ViewBag에 추가 되 고 (HTTP GET 사례에서와 같이) 바인딩된 모델 값이 표시를 위해 뷰로 다시 전달 됩니다. 유효성 검사 오류는 @Html.ValidationMessageFor HTML 도우미를 사용 하 여 자동으로 표시 됩니다.

#### <a name="testing-the-create-form"></a>만들기 폼 테스트

이를 테스트 하려면 응용 프로그램을 실행 하 고/StoreManager/Create/로 이동 합니다. 그러면 StoreController Create HTTP-GET 메서드에서 반환 된 빈 양식이 표시 됩니다.

일부 값을 입력 하 고 만들기 단추를 클릭 하 여 양식을 제출 합니다.

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>편집 내용 처리

편집 작업 쌍 (HTTP-GET 및 HTTP POST)은 방금 살펴본 만들기 작업 메서드와 매우 유사 합니다. 편집 시나리오에서는 기존 앨범으로 작업 하는 작업이 포함 되므로 Edit HTTP-GET 메서드는 경로를 통해 전달 되는 "id" 매개 변수를 기반으로 하 여 앨범을 로드 합니다. AlbumId에서 앨범을 검색 하는이 코드는 이전에 자세히 컨트롤러 작업에서 살펴본 것과 같습니다. Create/HTTP GET 메서드와 마찬가지로 드롭다운 값이 ViewBag를 통해 반환 됩니다. 그러면 ViewBag를 통해 추가 데이터 (예: 장르 목록)를 전달 하는 동안 모델 개체로 앨범을 모델 개체로 반환 하 여 앨범 클래스에 강력한 형식으로 표시할 수 있습니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

HTTP-사후 편집 작업은 HTTP-사후 작업 만들기와 매우 비슷합니다. 유일한 차이점은 db에 새 앨범을 추가 하는 대신입니다. 앨범 컬렉션은 db를 사용 하 여 앨범의 현재 인스턴스를 찾는 중입니다. 항목 (앨범)을 입력 하 고 해당 상태를 수정 됨으로 설정 합니다. 이렇게 하면 새 앨범을 만드는 것과는 달리 기존 앨범을 수정 하는 Entity Framework에 게 알려 줍니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

응용 프로그램을 실행 하 고/StoreManger/로 이동한 다음 앨범의 편집 링크를 클릭 하 여이를 테스트할 수 있습니다.

![](mvc-music-store-part-5/_static/image9.png)

그러면 편집 HTTP-GET 메서드에 표시 되는 편집 양식이 표시 됩니다. 일부 값을 입력 하 고 저장 단추를 클릭 합니다.

![](mvc-music-store-part-5/_static/image10.png)

그러면 양식이 게시 되 고, 값이 저장 되며, 값이 업데이트 되었음을 보여 주는 앨범 목록으로 돌아옵니다.

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>삭제 처리

삭제는 편집 및 만들기와 동일한 패턴을 따르며, 한 컨트롤러 작업을 사용 하 여 확인 양식을 표시 하 고, 다른 컨트롤러 작업을 사용 하 여 양식 전송을 처리 합니다.

HTTP-삭제 컨트롤러 가져오기 작업은 이전 저장소 관리자 정보 컨트롤러 작업과 동일 합니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

보기 콘텐츠 삭제 템플릿을 사용 하 여 앨범 형식에 강력한 형식의 양식을 표시 합니다.

![](mvc-music-store-part-5/_static/image12.png)

Delete 템플릿은 모델에 대 한 모든 필드를 표시 하지만이를 상당히 줄일 수 있습니다. /Views/StoreManager/Delete.cshtml의 보기 코드를 다음과 같이 변경 합니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

이렇게 하면 간단한 삭제 확인이 표시 됩니다.

![](mvc-music-store-part-5/_static/image13.png)

삭제 단추를 클릭 하면 양식이 서버에 다시 게시 되어 DeleteConfirmed 작업이 실행 됩니다.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

HTTP-사후 삭제 컨트롤러 작업은 다음 작업을 수행 합니다.

- 1. ID 별로 앨범을 로드 합니다.
- 2. 앨범을 삭제 하 고 변경 내용을 저장 합니다.
- 3. 목록에서 앨범이 제거 되었음을 보여 주는 인덱스로 리디렉션합니다.

이를 테스트 하려면 응용 프로그램을 실행 하 고/StoreManager.로 이동 합니다. 목록에서 앨범을 선택 하 고 삭제 링크를 클릭 합니다.

![](mvc-music-store-part-5/_static/image14.png)

그러면 삭제 확인 화면이 표시 됩니다.

![](mvc-music-store-part-5/_static/image15.png)

삭제 단추를 클릭 하면 앨범이 제거 되 고 저장 관리자 인덱스 페이지로 반환 됩니다. 그러면 앨범이 삭제 된 것을 볼 수 있습니다.

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>사용자 지정 HTML 도우미를 사용 하 여 텍스트 자르기

Store Manager 인덱스 페이지에는 잠재적인 문제가 하나 있습니다. 앨범 제목 및 음악가 이름 속성은 모두 테이블 서식 지정을 해제할 수 있을 정도로 길어질 수 있습니다. 보기에서 이러한 속성과 다른 속성을 쉽게 잘라낼 수 있도록 사용자 지정 HTML 도우미를 만듭니다.

![](mvc-music-store-part-5/_static/image17.png)

Razor의 @helper 구문을 사용 하면 보기에 사용할 자체 도우미 함수를 쉽게 만들 수 있습니다. /Views/StoreManager/Index.cshtml view를 열고 @model 줄 바로 뒤에 다음 코드를 추가 합니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

이 도우미 메서드는 허용 되는 문자열 및 최대 길이를 사용 합니다. 제공 된 텍스트가 지정 된 길이 보다 짧으면 도우미는이를 있는 그대로 출력 합니다. 더 긴 경우 텍스트를 자르고 "..."를 렌더링 합니다. 나머지입니다.

이제 자르기 도우미를 사용 하 여 앨범 제목과 음악가 이름 속성이 모두 25 자 미만인 지 확인할 수 있습니다. 새 자르기 도우미를 사용 하는 전체 뷰 코드는 아래에 나타납니다.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

이제/StoreManager/URL을 찾아볼 때 앨범 및 제목은 최대 길이 미만으로 유지 됩니다.

![](mvc-music-store-part-5/_static/image18.png)

참고: 단일 뷰에서 도우미를 만들고 사용 하는 간단한 사례를 보여 줍니다. 사이트 전체에서 사용할 수 있는 도우미를 만드는 방법에 대 한 자세한 내용은 블로그 게시물: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-4.md)
> [다음](mvc-music-store-part-6.md)
