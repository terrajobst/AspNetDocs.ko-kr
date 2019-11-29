---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-cs
title: 데이터 웹 컨트롤에 이진 데이터 표시 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 이미지 파일의 표시와 ' Download ' 링크의 프로 비전을 포함 하 여 웹 페이지에 이진 데이터를 표시 하는 옵션을 살펴봅니다.
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 5cbeb9f8-5f92-4ba8-87ae-0b4d460ae6d4
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: f38de7adcd77b3dc2622759646168cf533b8308f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74642485"
---
# <a name="displaying-binary-data-in-the-data-web-controls-c"></a>데이터 웹 컨트롤에 이진 데이터 표시(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_CS.exe) 또는 [PDF 다운로드](displaying-binary-data-in-the-data-web-controls-cs/_static/datatutorial55cs1.pdf)

> 이 자습서에서는 이미지 파일의 표시와 PDF 파일에 대 한 ' 다운로드 ' 링크의 프로 비전을 포함 하 여 웹 페이지에 이진 데이터를 표시 하는 옵션을 살펴봅니다.

## <a name="introduction"></a>소개

이전 자습서에서는 응용 프로그램의 기본 데이터 모델을 사용 하 여 이진 데이터를 연결 하 고 FileUpload 컨트롤을 사용 하 여 브라우저에서 웹 서버 파일 시스템으로 파일을 업로드 하는 두 가지 방법을 살펴보았습니다. 업로드 된 이진 데이터를 데이터 모델에 연결 하는 방법을 아직 확인 하지 않았습니다. 즉, 파일을 업로드 하 여 파일 시스템에 저장 한 후에는 파일에 대 한 경로를 적절 한 데이터베이스 레코드에 저장 해야 합니다. 데이터를 데이터베이스에 직접 저장 하는 경우 업로드 된 이진 데이터를 파일 시스템에 저장할 필요가 없지만 데이터베이스에 삽입 해야 합니다.

데이터 모델에 데이터를 연결 하는 방법에 대해서는 먼저 최종 사용자에 게 이진 데이터를 제공 하는 방법을 살펴보겠습니다. 텍스트 데이터를 표시 하는 것은 매우 간단 하지만 이진 데이터는 어떻게 표시 되나요? 물론 이진 데이터의 형식에 따라 달라 집니다. 이미지의 경우 이미지를 표시 하는 것이 좋습니다. Pdf, Microsoft Word 문서, ZIP 파일 및 다른 유형의 이진 데이터에 대 한 다운로드 링크를 제공 하는 것이 더 적합할 수 있습니다.

이 자습서에서는 GridView 및 DetailsView와 같은 데이터 웹 컨트롤을 사용 하 여 연결 된 텍스트 데이터와 함께 이진 데이터를 제공 하는 방법을 살펴보겠습니다. 다음 자습서에서는 업로드 된 파일을 데이터베이스와 연결 하는 데 주의를 기울여야 합니다.

## <a name="step-1-providingbrochurepathvalues"></a>1 단계:`BrochurePath`값 제공

`Categories` 테이블의 `Picture` 열은 다양 한 범주 이미지에 대 한 이진 데이터를 이미 포함 하 고 있습니다. 특히 각 레코드의 `Picture` 열에는 거친 품질이 낮은 16 색 비트맵 이미지의 이진 내용이 포함 되어 있습니다. 각 범주 이미지는 172 픽셀 너비와 120 픽셀 높이 이며 약 11kb를 사용 합니다. 자세히, `Picture` 열의 이진 콘텐츠에는 이미지를 표시 하기 전에 제거 해야 하는 78 바이트 [OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding) 헤더가 포함 되어 있습니다. 이 헤더 정보는 Northwind 데이터베이스의 루트가 Microsoft Access에 있기 때문에 표시 됩니다. Access에서 이진 데이터는 OLE 개체 데이터 형식 (이 헤더의 경우)을 사용 하 여 저장 됩니다. 지금은 그림을 표시 하기 위해 이러한 저품질 이미지에서 헤더를 제거 하는 방법을 알아봅니다. 이후 자습서에서는 범주 `Picture` 열을 업데이트 하는 인터페이스를 빌드하고 OLE 헤더를 사용 하는 이러한 비트맵 이미지를 불필요 한 OLE 헤더 없이 해당 JPG 이미지로 바꿉니다.

이전 자습서에서는 FileUpload 컨트롤을 사용 하는 방법을 살펴보았습니다. 따라서 계속 해 서 브로슈어 파일을 웹 서버 파일 시스템에 추가할 수 있습니다. 그러나 이렇게 하면 `Categories` 테이블의 `BrochurePath` 열이 업데이트 되지 않습니다. 다음 자습서에서는이를 수행 하는 방법을 확인할 수 있지만 지금은이 열에 대 한 값을 직접 제공 해야 합니다.

이 자습서의 다운로드에서는 해산물을 제외한 각 범주에 대해 하나씩, `~/Brochures` 폴더에서 7 개의 PDF 브로슈어 파일을 찾을 수 있습니다. 모든 레코드가 연결 된 이진 데이터를 갖지 않는 시나리오를 처리 하는 방법을 보여 주기 위해 해산물 브로셔 추가를 의도적으로 생략 했습니다. `Categories` 테이블을 이러한 값으로 업데이트 하려면 서버 탐색기에서 `Categories` 노드를 마우스 오른쪽 단추로 클릭 하 고 테이블 데이터 표시를 선택 합니다. 그런 다음 그림 1에 나와 있는 것 처럼 브로슈어를 포함 하는 각 범주에 대 한 브로셔 파일의 가상 경로를 입력 합니다. 해산물 범주에 대 한 브로슈어가 없으므로 `BrochurePath` 열 s 값을 `NULL`그대로 둡니다.

[![Categories 테이블 s BrochurePath 열에 대 한 값을 수동으로 입력 합니다.](displaying-binary-data-in-the-data-web-controls-cs/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image1.png)

**그림 1**: `Categories` 테이블 s `BrochurePath` 열에 대 한 값을 수동으로 입력 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image2.png))

## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>2 단계: GridView에서 브로슈어 용 다운로드 링크 제공

`Categories` 테이블에 대해 제공 된 `BrochurePath` 값을 사용 하 여 범주 브로슈어를 다운로드 하는 링크와 함께 각 범주를 나열 하는 GridView를 만들 준비가 되었습니다. 4 단계에서는이 GridView를 확장 하 여 범주 이미지도 표시 합니다.

먼저 도구 상자에서 GridView를 `BinaryData` 폴더의 `DisplayOrDownloadData.aspx` 페이지 디자이너로 끌어 옵니다. GridView s `ID`를 `Categories` 하 고 GridView s 스마트 태그를 통해 설정 하 고 새 데이터 원본에 바인딩하려면 선택 합니다. 특히 `CategoriesBLL` object s `GetCategories()` 메서드를 사용 하 여 데이터를 검색 하는 `CategoriesDataSource` ObjectDataSource에 바인딩합니다.

[새 ObjectDataSource 라는 범주 데이터 원본을 만듭니다 ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image3.png)

**그림 2**: `CategoriesDataSource` 라는 새 ObjectDataSource 만들기 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image4.png))

[범주 Bll 클래스를 사용 하도록 ObjectDataSource 구성 ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image5.png)

**그림 3**: `CategoriesBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image6.png))

[GetCategories () 메서드를 사용 하 여 범주 목록을 검색 ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image7.png)

**그림 4**: `GetCategories()` 메서드를 사용 하 여 범주 목록 검색 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image8.png))

데이터 소스 구성 마법사를 완료 한 후 Visual Studio는 `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`및 `BrochurePath` `DataColumn` s에 대 한 `Categories` GridView에 자동으로 BoundField를 추가 합니다. `GetCategories()` 메서드 쿼리가이 정보를 검색 하지 않으므로 계속 해 서 `NumberOfProducts` BoundField를 제거 합니다. 또한 `CategoryID` BoundField를 제거 하 고 `CategoryName` 및 `BrochurePath` BoundFields `HeaderText` 속성을 범주 및 브로슈어에 각각 합니다. 이러한 변경을 수행한 후 GridView와 ObjectDataSource의 선언적 태그는 다음과 같습니다.

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample1.aspx)]

브라우저를 통해이 페이지를 봅니다 (그림 5 참조). 각각의 8 개 범주가 나열 됩니다. `BrochurePath` 값이 있는 7 개 범주에는 해당 BoundField에 `BrochurePath` 값이 표시 됩니다. `BrochurePath`에 대 한 `NULL` 값이 있는 해산물은 빈 셀을 표시 합니다.

[![각 범주 이름, 설명 및 BrochurePath 값이 나열 됩니다.](displaying-binary-data-in-the-data-web-controls-cs/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image9.png)

**그림 5**: 각 범주 이름, 설명 및 `BrochurePath` 값이 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image10.png)).

`BrochurePath` 열의 텍스트를 표시 하는 대신 브로슈어에 대 한 링크를 만들려고 합니다. 이를 수행 하려면 `BrochurePath` BoundField를 제거 하 고 하이퍼링크 필드로 바꿉니다. 새 hyperlink Field s `HeaderText` 속성을 브로슈어에 설정 하 고 `Text` 속성을 브로슈어에 표시 하 고 `DataNavigateUrlFields` 속성을 `BrochurePath`로 설정 합니다.

![BrochurePath에 대 한 하이퍼링크 필드 추가](displaying-binary-data-in-the-data-web-controls-cs/_static/image6.gif)

**그림 6**: `BrochurePath`에 대 한 하이퍼링크 필드 추가

그림 7에 표시 된 것 처럼 GridView에 링크 열이 추가 됩니다. 보기 브로슈어 링크를 클릭 하면 PDF를 브라우저에 직접 표시 하거나 PDF 판독기가 설치 되어 있고 브라우저의 설정에 따라 사용자에 게 파일을 다운로드 하 라는 메시지를 표시 합니다.

[![브로슈어 보기 링크를 클릭 하 여 범주 브로슈어를 볼 수 있습니다.](displaying-binary-data-in-the-data-web-controls-cs/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image11.png)

**그림 7**: 보기 브로슈어 링크를 클릭 하 여 범주 브로슈어를 볼 수 있습니다 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image12.png)).

[![범주 브로슈어 PDF가 표시 됩니다.](displaying-binary-data-in-the-data-web-controls-cs/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image13.png)

**그림 8**: 범주 브로슈어 PDF가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image14.png)).

## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>브로슈어 없이 범주에 대 한 보기 브로슈어 텍스트 숨기기

그림 7에 표시 된 것 처럼 `BrochurePath` 하이퍼링크 필드에는 `BrochurePath`에 대 한`NULL` 아닌 값이 있는지 여부에 관계 없이 모든 레코드에 대 한 `Text` 속성 값 (보기 브로슈어)이 표시 됩니다. 물론 `BrochurePath` `NULL`되는 경우이 링크는 해산물 범주가 있는 경우 처럼 텍스트로만 표시 됩니다 (그림 7 참조). 텍스트 보기 브로슈어를 표시 하는 대신 사용 가능한 브로슈어와 같은 일부 대체 텍스트를 표시 하는 `BrochurePath` 값이 없는 범주를 사용 하는 것이 좋을 수 있습니다.

이 동작을 제공 하려면 `BrochurePath` 값에 따라 적절 한 출력을 내보내는 페이지 메서드 호출을 통해 해당 콘텐츠가 생성 되는 Templatefield로 변환를 사용 해야 합니다. 먼저 [GridView 컨트롤 자습서의 템플릿 사용 필드](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) 에서이 서식 지정 기술을 다시 살펴보았습니다.

`BrochurePath` 하이퍼링크 필드를 선택한 다음 열 편집 대화 상자에서이 필드를 Templatefield로 변환로 변환 링크를 클릭 하 여 hyperlink 필드를 Templatefield로 변환로 설정 합니다.

![하이퍼링크 필드를 Templatefield로 변환 변환](displaying-binary-data-in-the-data-web-controls-cs/_static/image9.gif)

**그림 9**: 하이퍼링크 필드를 templatefield로 변환 변환

이렇게 하면 `NavigateUrl` 속성이 `BrochurePath` 값에 바인딩되는 HyperLink 웹 컨트롤이 포함 된 `ItemTemplate`를 사용 하 여 Templatefield로 변환을 만듭니다. 이 태그를 `GenerateBrochureLink`메서드에 대 한 호출로 바꾸고 `BrochurePath`의 값을 전달 합니다.

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample2.aspx)]

그런 다음 `string`을 반환 하 고 `object`를 입력 매개 변수로 허용 하는 `GenerateBrochureLink` 라는 ASP.NET page s의 코드 숨김이 클래스에 `protected` 메서드를 만듭니다.

[!code-csharp[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample3.cs)]

이 메서드는 전달 된 `object` 값이 데이터베이스 `NULL` 인지 확인 하 고, 해당 하는 경우 범주에 브로슈어가 부족 함을 나타내는 메시지를 반환 합니다. 그렇지 않고 `BrochurePath` 값이 있으면 하이퍼링크에 표시 됩니다. `BrochurePath` 값이 제공 되 면 [`ResolveUrl(url)` 메서드에](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx)전달 됩니다. 이 메서드는 전달 된 *url*을 확인 하 여 `~` 문자를 적절 한 가상 경로로 바꿉니다. 예를 들어 응용 프로그램이 `/Tutorial55`를 기반으로 하는 경우 `ResolveUrl("~/Brochures/Meats.pdf")`는 `/Tutorial55/Brochures/Meat.pdf`를 반환 합니다.

그림 10에서는 이러한 변경 내용이 적용 된 후의 페이지를 보여 줍니다. 이제 해산물 범주 s `BrochurePath` 필드에 브로슈어를 사용할 수 없음 텍스트가 표시 됩니다.

[브로슈어 없이 해당 범주에 대해 사용 가능한 브로슈어가 없는 텍스트를 표시 ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image15.png)

**그림 10**: 브로슈어 없이 해당 범주에 대해 사용 가능한 브로슈어가 없는 텍스트 표시 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image16.png))

## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>3 단계: 범주 그림을 표시 하는 웹 페이지 추가

사용자가 ASP.NET 페이지를 방문 하면 ASP.NET 페이지의 HTML이 표시 됩니다. 받은 HTML은 텍스트 이며 이진 데이터를 포함 하지 않습니다. 이미지, 사운드 파일, Macromedia Flash 응용 프로그램, 포함 된 Windows Media Player 비디오 등의 추가 이진 데이터는 웹 서버에 별도의 리소스로 존재 합니다. HTML에는 이러한 파일에 대 한 참조가 포함 되지만 파일의 실제 내용은 포함 되지 않습니다.

예를 들어 HTML에서 `<img>` 요소는 그림을 참조 하는 데 사용 되며, `src` 특성은 다음과 같이 이미지 파일을 가리킵니다.

[!code-html[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample4.html)]

브라우저에서이 HTML을 받으면 웹 서버에서 이미지 파일의 이진 콘텐츠를 검색 하 여 브라우저에 표시 하는 또 다른 요청을 수행 합니다. 모든 이진 데이터에도 동일한 개념이 적용 됩니다. 2 단계에서 브로슈어는 페이지의 HTML 태그의 일부로 브라우저에 전송 되지 않습니다. 대신, 렌더링 된 HTML에는 클릭 하면 브라우저에서 PDF 문서를 직접 요청 하는 하이퍼링크가 제공 됩니다.

사용자가 데이터베이스에 있는 이진 데이터를 다운로드할 수 있도록 하려면 데이터를 반환 하는 별도의 웹 페이지를 만들어야 합니다. 응용 프로그램의 경우 데이터베이스에 직접 저장 된 이진 데이터 필드에는 범주 s 그림이 있습니다. 따라서 호출 된 경우 특정 범주에 대 한 이미지 데이터를 반환 하는 페이지가 필요 합니다.

`DisplayCategoryPicture.aspx`이라는 `BinaryData` 폴더에 새 ASP.NET 페이지를 추가 합니다. 이렇게 하려면 마스터 페이지 선택 확인란을 선택 하지 않은 상태로 둡니다. 이 페이지에서는 querystring의 `CategoryID` 값을 예상 하 고 해당 범주 `Picture` 열의 이진 데이터를 반환 합니다. 이 페이지는 이진 데이터를 반환 하 고 다른 항목은 반환 하지 않으므로 HTML 섹션에 태그가 필요 하지 않습니다. 따라서 왼쪽 아래 모서리의 원본 탭을 클릭 하 고 `<%@ Page %>` 지시어를 제외 하 고 모든 페이지 태그를 제거 합니다. 즉, `DisplayCategoryPicture.aspx` s 선언 태그는 한 줄로 구성 되어야 합니다.

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample5.aspx)]

`<%@ Page %>` 지시문에 `MasterPageFile` 특성이 표시 되는 경우 제거 합니다.

페이지의 코드 숨김이 클래스에서 다음 코드를 `Page_Load` 이벤트 처리기에 추가 합니다.

[!code-csharp[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample6.cs)]

이 코드는 `CategoryID` querystring 값을 `categoryID`라는 변수로 읽어 시작 합니다. 그런 다음 `CategoriesBLL` 클래스 `GetCategoryWithBinaryDataByCategoryID(categoryID)` 메서드에 대 한 호출을 통해 그림 데이터가 검색 됩니다. 이 데이터는 `Response.BinaryWrite(data)` 메서드를 사용 하 여 클라이언트에 반환 되지만이를 호출 하기 전에 `Picture` 열 값 s OLE 헤더를 제거 해야 합니다. 이 작업을 수행 하려면 `Picture` 열에 있는 것 보다 정확 하 게 78 문자를 저장 하는 `strippedImageData` 라는 `byte` 배열을 만듭니다. [`Array.Copy` 메서드](https://msdn.microsoft.com/library/z50k9bft.aspx) 는 78 위치에서 시작 하는 `category.Picture` 데이터를 `strippedImageData`로 복사 하는 데 사용 됩니다.

`Response.ContentType` 속성은 브라우저에서 렌더링 방법을 알 수 있도록 반환 되는 콘텐츠의 [MIME 형식을](http://en.wikipedia.org/wiki/MIME) 지정 합니다. `Categories` 테이블 s `Picture` 열이 비트맵 이미지 이므로 비트맵 MIME 형식이 여기 (image/bmp)에서 사용 됩니다. MIME 형식을 생략 하면 이미지 파일의 이진 데이터의 내용에 따라 형식을 유추할 수 있기 때문에 대부분의 브라우저에서 이미지를 올바르게 표시 합니다. 그러나 가능한 경우 MIME 형식을 포함 하는 것이 좋습니다. [MIME 미디어 유형의](http://www.iana.org/assignments/media-types/)전체 목록은 [인터넷 할당 번호 기관 웹 사이트](http://www.iana.org/) 를 참조 하세요.

이 페이지를 만든 후 `DisplayCategoryPicture.aspx?CategoryID=categoryID`를 방문 하 여 특정 범주 s 사진을 볼 수 있습니다. 그림 11은 `DisplayCategoryPicture.aspx?CategoryID=1`에서 볼 수 있는 음료 범주 s 그림을 보여 줍니다.

[음료 범주의 s 그림이 표시 되는 ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image17.png)

**그림 11**: 음료 범주 s 그림이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image18.png)).

`DisplayCategoryPicture.aspx?CategoryID=categoryID`방문할 때 ' System.web ' 형식의 개체를 ' system.string [] ' 형식으로 캐스팅할 수 없다는 예외가 발생 하면이를 발생 시킬 수 있는 두 가지 항목이 있습니다. 먼저 `Categories` 테이블 s `Picture` 열에서 `NULL` 값을 허용 합니다. 그러나 `DisplayCategoryPicture.aspx` 페이지는`NULL` 없는 값이 있다고 가정 합니다. `CategoriesDataTable`의 `Picture` 속성에 `NULL` 값이 있는 경우 직접 액세스할 수 없습니다. `Picture` 열에 대해 `NULL` 값을 허용 하려면 다음 조건을 포함 해야 합니다.

[!code-csharp[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample7.cs)]

위의 코드에서는 그림이 없는 범주에 대해 표시할 `Images` 폴더에 `NoPictureAvailable.gif` 라는 일부 이미지 파일이 있다고 가정 합니다.

이 예외는 `CategoriesTableAdapter` s `GetCategoryWithBinaryDataByCategoryID` method s `SELECT` 문이 주 쿼리 열 목록으로 다시 되돌아간 경우에 발생할 수 있습니다 .이는 임시 SQL 문을 사용 하 고 TableAdapter 주 쿼리에 대해 마법사를 다시 실행 하는 경우 발생할 수 있습니다. `GetCategoryWithBinaryDataByCategoryID` method s `SELECT` 문에 `Picture` 열이 계속 포함 되어 있는지 확인 합니다.

> [!NOTE]
> `DisplayCategoryPicture.aspx` 방문할 때마다 데이터베이스에 액세스 하 고 지정 된 범주에 대 한 그림 데이터가 반환 됩니다. 사용자가 마지막으로 표시 한 후에도 범주 그림이 변경 되지 않은 경우에는이 작업을 더 이상 사용 하지 않아도 됩니다. 다행히 HTTP에서는 *조건부*를 사용할 수 있습니다. 조건부 GET을 사용 하면 HTTP 요청을 수행 하는 클라이언트는 클라이언트에서 웹 서버에서이 리소스를 마지막으로 검색 한 날짜와 시간을 제공 하는 [`If-Modified-Since` http 헤더](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) 를 따라 보냅니다. 지정 된 날짜 이후에 콘텐츠가 변경 되지 않은 경우 웹 서버는 [수정 되지 않은 상태 코드 (304)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) 로 응답 하 고 요청 된 리소스의 콘텐츠를 다시은 선형화 수 있습니다. 간단히 말해서,이 기술은 클라이언트가 마지막으로 액세스 한 이후에 수정 되지 않은 경우 웹 서버에서 리소스에 대 한 콘텐츠를 다시 보내지 않도록 합니다.

그러나이 동작을 구현 하려면 `Picture` 열이 마지막으로 업데이트 되었을 때 캡처할 `Categories` 테이블에 `PictureLastModified` 열을 추가 하 고 `If-Modified-Since` 헤더를 확인 하는 코드를 사용 해야 합니다. `If-Modified-Since` 헤더 및 조건부 가져오기 워크플로에 대 한 자세한 내용은 [RSS 해커를 위한 Http 조건부 get](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers) 및 [ASP.NET 페이지에서 Http 요청을 수행 하](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx)는 방법을 자세히 알아봅니다.

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>4 단계: GridView에서 범주 그림 표시

이제 특정 범주 그림을 표시 하는 웹 페이지가 있으므로 [이미지 웹 컨트롤](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx) 또는 `DisplayCategoryPicture.aspx?CategoryID=categoryID`가리키는 HTML `<img>` 요소를 사용 하 여 표시할 수 있습니다. 데이터베이스 데이터에 의해 URL이 결정 되는 이미지는 ImageField을 사용 하 여 GridView 또는 DetailsView에 표시 될 수 있습니다. ImageField에는 하이퍼링크 필드 `DataNavigateUrlFields` 및 `DataNavigateUrlFormatString` 속성 처럼 작동 하는 `DataImageUrlField` 및 `DataImageUrlFormatString` 속성이 포함 되어 있습니다.

ImageField를 추가 하 여 각 범주에 그림을 표시 하는 `DisplayOrDownloadData.aspx` `Categories` GridView를 확대 합니다. 단순히 ImageField를 추가 하 고 해당 `DataImageUrlField` 및 `DataImageUrlFormatString` 속성을 `CategoryID` 및 `DisplayCategoryPicture.aspx?CategoryID={0}`로 각각 설정 합니다. 이렇게 하면 `src` 특성이 `DisplayCategoryPicture.aspx?CategoryID={0}`를 참조 하는 `<img>` 요소를 렌더링 하는 GridView 열이 만들어집니다. 여기서 {0}은 GridView 행의 `CategoryID` 값으로 바뀝니다.

![GridView에 ImageField 추가](displaying-binary-data-in-the-data-web-controls-cs/_static/image12.gif)

**그림 12**: GridView에 ImageField 추가

ImageField을 추가한 후에는 GridView의 선언적 구문이 soothe 다음과 같이 표시 됩니다.

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-cs/samples/sample8.aspx)]

잠시 시간을 사용 하 여 브라우저를 통해이 페이지를 봅니다. 각 레코드에는 이제 범주에 대 한 그림이 포함 되어 있습니다.

[각 행에 대 한 범주 s 그림이 표시 ![](displaying-binary-data-in-the-data-web-controls-cs/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-cs/_static/image19.png)

**그림 13**: 각 행에 대 한 범주 s 그림이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](displaying-binary-data-in-the-data-web-controls-cs/_static/image20.png)).

## <a name="summary"></a>요약

이 자습서에서는 이진 데이터를 표시 하는 방법을 살펴보았습니다. 데이터를 표시 하는 방법은 데이터 유형에 따라 달라 집니다. PDF 브로슈어 파일의 경우 클릭 하면 사용자가 PDF 파일에 직접 사용자를 게 사용 하는 보기 브로슈어 링크를 제공 했습니다. 범주 s 그림의 경우 먼저 데이터베이스에서 이진 데이터를 검색 하 여 반환 하는 페이지를 만든 다음,이 페이지를 사용 하 여 GridView의 각 범주를 표시 합니다.

이진 데이터를 표시 하는 방법을 살펴보았으므로 이제는 이진 데이터를 사용 하 여 데이터베이스에 대 한 삽입, 업데이트 및 삭제를 수행 하는 방법을 살펴볼 준비가 되었습니다. 다음 자습서에서는 업로드 한 파일을 해당 데이터베이스 레코드와 연결 하는 방법을 살펴보겠습니다. 이 자습서에서는 기존 이진 데이터를 업데이트 하는 방법 뿐만 아니라 연결 된 레코드가 제거 될 때 이진 데이터를 삭제 하는 방법을 알아봅니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 리드 검토자는 Teresa Murphy 및 Dave Gardner입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](uploading-files-cs.md)
> [다음](including-a-file-upload-option-when-adding-a-new-record-cs.md)
