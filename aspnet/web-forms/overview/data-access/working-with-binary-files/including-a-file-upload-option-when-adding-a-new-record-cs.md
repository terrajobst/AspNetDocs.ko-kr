---
uid: web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
title: 새 레코드를 추가할 때 파일 업로드 옵션 포함 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 사용자가 텍스트 데이터를 입력 하 고 이진 파일을 업로드 하는 데 사용할 수 있는 웹 인터페이스를 만드는 방법을 보여 줍니다. 사용할 수 있는 옵션을 설명 하려면 ...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 362ade25-3965-4fb2-88d2-835c4786244f
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/including-a-file-upload-option-when-adding-a-new-record-cs
msc.type: authoredcontent
ms.openlocfilehash: f1287e180151b3034a7b90ef4b3f1fbe68354a09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78475541"
---
# <a name="including-a-file-upload-option-when-adding-a-new-record-c"></a>새 레코드를 추가할 때 파일 업로드 옵션 포함(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_56_CS.exe) 또는 [PDF 다운로드](including-a-file-upload-option-when-adding-a-new-record-cs/_static/datatutorial56cs1.pdf)

> 이 자습서에서는 사용자가 텍스트 데이터를 입력 하 고 이진 파일을 업로드 하는 데 사용할 수 있는 웹 인터페이스를 만드는 방법을 보여 줍니다. 이진 데이터를 저장 하는 데 사용할 수 있는 옵션을 설명 하기 위해 한 파일은 데이터베이스에 저장 되 고 다른 파일은 파일 시스템에 저장 됩니다.

## <a name="introduction"></a>소개

이전 두 자습서에서는 응용 프로그램 데이터 모델에 연결 된 이진 데이터를 저장 하는 기술에 대해 살펴보았습니다. FileUpload 컨트롤을 사용 하 여 클라이언트에서 웹 서버로 파일을 전송 하는 방법 및 데이터에이 이진 데이터를 제공 하는 방법에 대해 살펴보았습니다. eb 컨트롤입니다. 그러나 업로드 된 데이터를 데이터 모델에 연결 하는 방법에 대해서는 아직 설명 하지 않았습니다.

이 자습서에서는 새 범주를 추가 하는 웹 페이지를 만듭니다. 범주 이름 및 설명에 대 한 텍스트 상자 외에도이 페이지에는 새 category s 그림에 대 한 두 개의 FileUpload 컨트롤과 브로슈어에 하나씩 포함 해야 합니다. 업로드 된 그림은 새 레코드의 `Picture` 열에 직접 저장 되는 반면, 브로슈어는 새 레코드의 `BrochurePath` 열에 저장 된 파일의 경로를 사용 하 여 `~/Brochures` 폴더에 저장 됩니다.

이 새 웹 페이지를 만들기 전에 아키텍처를 업데이트 해야 합니다. `CategoriesTableAdapter` s 주 쿼리는 `Picture` 열을 검색 하지 않습니다. 따라서 자동 생성 된 `Insert` 메서드에는 `CategoryName`, `Description`및 `BrochurePath` 필드에 대 한 입력만 있습니다. 따라서 `Categories` 필드 4 개 모두에 대해 요청 하는 추가 메서드를 TableAdapter에 만들어야 합니다. 비즈니스 논리 계층의 `CategoriesBLL` 클래스도 업데이트 해야 합니다.

## <a name="step-1-adding-aninsertwithpicturemethod-to-thecategoriestableadapter"></a>1 단계:`CategoriesTableAdapter`에`InsertWithPicture`메서드 추가

[데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-cs.md) 자습서로 `CategoriesTableAdapter`을 다시 만들 때 주 쿼리를 기반으로 `INSERT`, `UPDATE`및 `DELETE` 문을 자동으로 생성 하도록 구성 했습니다. 또한 `Insert`, `Update`및 `Delete`메서드를 만든 DB Direct 방법을 사용 하도록 TableAdapter에 지시 했습니다. 이러한 메서드는 자동 생성 된 `INSERT`, `UPDATE`및 `DELETE` 문을 실행 하므로 주 쿼리에서 반환 된 열을 기반으로 입력 매개 변수를 그대로 사용 합니다. [파일 업로드](uploading-files-cs.md) 자습서에서 `BrochurePath` 열을 사용 하도록 `CategoriesTableAdapter` s 주 쿼리를 확장 했습니다.

`CategoriesTableAdapter` s 주 쿼리가 `Picture` 열을 참조 하지 않으므로 새 레코드를 추가 하거나 기존 레코드를 `Picture` 열의 값으로 업데이트할 수 없습니다. 이 정보를 캡처하기 위해 특히 이진 데이터를 사용 하 여 레코드를 삽입 하는 데 사용 되는 TableAdapter에 새 메서드를 만들거나 자동 생성 된 `INSERT` 문을 사용자 지정할 수 있습니다. 자동 생성 된 `INSERT` 문을 사용자 지정 하는 데 문제가 있으면 마법사에서 사용자 지정 내용을 덮어쓸 위험이 있습니다. 예를 들어 `INSERT` 문을 사용자 지정 하 여 `Picture` 열을 사용 한다고 가정 합니다. 이는 범주 s 그림의 이진 데이터에 대 한 추가 입력 매개 변수를 포함 하도록 TableAdapter s `Insert` 메서드를 업데이트 합니다. 그런 다음이 DAL 메서드를 사용 하 고 프레젠테이션 계층을 통해이 BLL 메서드를 호출 하는 비즈니스 논리 계층에서 메서드를 만들 수 있으며, 모든 것이 wonderfully 작동 합니다. 즉, 다음 번에 TableAdapter 구성 마법사를 통해 TableAdapter를 구성할 때까지입니다. 마법사가 완료 되는 즉시 `INSERT` 문에 대 한 사용자 지정을 덮어쓰므로 `Insert` 메서드가 이전 형식으로 되돌아가고 코드는 더 이상 컴파일되지 않습니다.

> [!NOTE]
> 임시 SQL 문 대신 저장 프로시저를 사용 하는 경우에는 문제가 되지 않습니다. 이후 자습서에서는 데이터 액세스 계층에서 임시 SQL 문을 사용 하는 대신 저장 프로시저를 사용 하는 방법을 살펴봅니다.

자동 생성 된 SQL 문을 사용자 지정 하는 대신이 잠재적 골칫거리을 방지 하기 위해에서 TableAdapter에 대 한 새 메서드를 만들 수 있습니다. `InsertWithPicture`이라는이 메서드는 `CategoryName`, `Description`, `BrochurePath`및 `Picture` 열에 대 한 값을 허용 하 고 네 개의 값을 모두 새 레코드에 저장 하는 `INSERT` 문을 실행 합니다.

형식화 된 데이터 집합을 열고 디자이너에서 `CategoriesTableAdapter` s 헤더를 마우스 오른쪽 단추로 클릭 한 다음 상황에 맞는 메뉴에서 쿼리 추가를 선택 합니다. Tableadapter 쿼리가 데이터베이스에 액세스 하는 방법을 묻는 TableAdapter 쿼리 구성 마법사가 시작 됩니다. SQL 문 사용을 선택 하 고 다음을 클릭 합니다. 다음 단계에서는 생성할 쿼리 유형을 묻는 메시지를 표시 합니다. `Categories` 테이블에 새 레코드를 추가 하는 쿼리를 다시 작성 하기 때문에 삽입을 선택 하 고 다음을 클릭 합니다.

[삽입 옵션 ![선택 합니다.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image1.png)

**그림 1**: 삽입 옵션 선택 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.png))

이제 `INSERT` SQL 문을 지정 해야 합니다. 마법사에서는 TableAdapter 주 쿼리에 해당 하는 `INSERT` 문을 자동으로 제안 합니다. 이 경우 `CategoryName`, `Description`및 `BrochurePath` 값을 삽입 하는 `INSERT` 문입니다. `Picture` 열이 `@Picture` 매개 변수와 함께 포함 되도록 문을 업데이트 합니다. 예를 들면 다음과 같습니다.

[!code-sql[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample1.sql)]

마법사의 마지막 화면에서 새 TableAdapter 메서드의 이름을 묻는 메시지를 표시 합니다. `InsertWithPicture`를 입력 하 고 마침을 클릭 합니다.

[새 TableAdapter 메서드 InsertWithPicture의 이름을 ![합니다.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image2.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.png)

**그림 2**: 새 TableAdapter 메서드 이름 `InsertWithPicture` ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.png))

## <a name="step-2-updating-the-business-logic-layer"></a>2 단계: 비즈니스 논리 계층 업데이트

프레젠테이션 계층은 데이터 액세스 계층으로 직접 이동 하는 것이 아니라 비즈니스 논리 계층과만 인터페이스 해야 하기 때문에 방금 만든 DAL 메서드 (`InsertWithPicture`)를 호출 하는 BLL 메서드를 만들어야 합니다. 이 자습서에서는 입력으로 3 개의 `string` s와 `byte` 배열을 허용 하는 `InsertWithPicture` 라는 `CategoriesBLL` 클래스에 메서드를 만듭니다. `string` 입력 매개 변수는 범주 이름, 설명 및 브로셔 파일 경로에 대 한 것 이지만 `byte` 배열은 범주 그림의 이진 콘텐츠를 위한 것입니다. 다음 코드에 나와 있는 것 처럼이 BLL 메서드는 해당 DAL 메서드를 호출 합니다.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample2.cs)]

> [!NOTE]
> `InsertWithPicture` 메서드를 BLL에 추가 하기 전에 형식화 된 데이터 집합을 저장 했는지 확인 합니다. `CategoriesTableAdapter` 클래스 코드는 형식화 된 데이터 집합을 기반으로 자동 생성 되므로, 먼저 변경 내용을 형식화 된 데이터 집합에 저장 하지 않은 경우 `Adapter` 속성이 `InsertWithPicture` 메서드에 대해 인식 하지 못합니다.

## <a name="step-3-listing-the-existing-categories-and-their-binary-data"></a>3 단계: 기존 범주 및 해당 이진 데이터 나열

이 자습서에서는 최종 사용자가 시스템에 새 범주를 추가 하 여 새 범주에 대 한 그림과 브로슈어를 제공 하는 데 사용할 수 있는 페이지를 만듭니다. [이전 자습서](displaying-binary-data-in-the-data-web-controls-cs.md) 에서는 Templatefield로 변환 및 ImageField와 함께 GridView를 사용 하 여 각 범주 이름, 설명, 그림 및 브로슈어를 다운로드 하는 링크를 표시 했습니다. 에서이 자습서에 대 한 해당 기능을 복제 하 여 모든 기존 범주를 나열 하 고 새 범주를 만들 수 있는 페이지를 만들어 보겠습니다.

먼저 `BinaryData` 폴더에서 `DisplayOrDownload.aspx` 페이지를 엽니다. 원본 뷰로 이동 하 고 GridView 및 ObjectDataSource s 선언 구문을 복사 하 여 `UploadInDetailsView.aspx`의 `<asp:Content>` 요소 내에 붙여 넣습니다. 또한 `DisplayOrDownload.aspx`의 코드 숨김이 클래스에서 `GenerateBrochureLink` 메서드를 `UploadInDetailsView.aspx`로 복사 하는 것을 잊지 마십시오.

[![선언 구문을 복사 하 여 DisplayOrDownload에서 UploadInDetailsView에 붙여넣습니다.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image3.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.png)

**그림 3**: `DisplayOrDownload.aspx`의 선언 구문을 복사 하 여 `UploadInDetailsView.aspx`에 붙여넣기 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.png))

선언적 구문과 `GenerateBrochureLink` 메서드를 `UploadInDetailsView.aspx` 페이지로 복사한 후 브라우저를 통해 페이지를 확인 하 여 모든 항목이 올바르게 복사 되었는지 확인 합니다. 브로슈어를 다운로드할 수 있는 링크와 범주 그림을 포함 하는 8 개의 범주가 나열 된 GridView가 표시 됩니다.

[![이제 각 범주를 이진 데이터와 함께 표시 합니다.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image4.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.png)

**그림 4**: 이제 각 범주가 이진 데이터와 함께 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.png)).

## <a name="step-4-configuring-thecategoriesdatasourceto-support-inserting"></a>4 단계: 삽입을 지원 하도록`CategoriesDataSource`구성

`Categories` GridView에서 사용 하는 `CategoriesDataSource` ObjectDataSource는 현재 데이터를 삽입 하는 기능을 제공 하지 않습니다. 이 데이터 소스 컨트롤을 통해 삽입을 지원 하기 위해 `Insert` 메서드를 기본 개체인 `CategoriesBLL`의 메서드에 매핑해야 합니다. 특히 2 단계, `InsertWithPicture`에서 다시 추가한 `CategoriesBLL` 메서드에 매핑하려고 합니다.

먼저 ObjectDataSource s 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다. 첫 번째 화면에는 데이터 원본이 작동 하도록 구성 된 개체 `CategoriesBLL`표시 됩니다. 이 설정을 그대로 두고 다음을 클릭 하 여 데이터 메서드 정의 화면으로 이동 합니다. 삽입 탭으로 이동 하 고 드롭다운 목록에서 `InsertWithPicture` 메서드를 선택 합니다. 마침을 클릭하여 마법사를 완료합니다.

[InsertWithPicture 메서드를 사용 하도록 ObjectDataSource를 구성 ![](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image5.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.png)

**그림 5**: `InsertWithPicture` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.png))

> [!NOTE]
> 마법사가 완료 되 면 Visual Studio에서 필드와 키를 새로 고칠지 여부를 묻는 메시지를 표시할 수 있습니다. 그러면 데이터 웹 컨트롤 필드가 다시 생성 됩니다. 예를 선택 하면 수행한 필드 사용자 지정 항목을 덮어쓰기 때문에 아니요를 선택 합니다.

마법사를 완료 한 후에는 다음 선언 태그에서 보여 주는 것 처럼 ObjectDataSource에 `InsertMethod` 속성 값과 4 개의 범주 열에 대 한 `InsertParameters` 포함 됩니다.

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample3.aspx)]

## <a name="step-5-creating-the-inserting-interface"></a>5 단계: 삽입 인터페이스 만들기

[데이터 삽입, 업데이트 및 삭제에 대 한 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)에서 처음에 설명한 것 처럼 DetailsView 컨트롤은 삽입을 지 원하는 데이터 소스 컨트롤을 사용할 때 사용할 수 있는 기본 제공 삽입 인터페이스를 제공 합니다. 삽입 인터페이스를 영구적으로 렌더링 하 여 사용자가 새 범주를 신속 하 게 추가할 수 있도록 하는 GridView 위의이 페이지에 DetailsView 컨트롤을 추가 해 보겠습니다. DetailsView에 새 범주를 추가 하면 그 아래의 GridView가 자동으로 새로 고쳐 새 범주를 표시 합니다.

먼저 도구 상자의 DetailsView을 GridView 위의 디자이너로 끌어 옵니다. `ID` 속성을 `NewCategory`로 설정 하 고 `Height` 및 `Width` 속성 값을 선택 취소 합니다. DetailsView의 스마트 태그에서 기존 `CategoriesDataSource`에 바인딩한 다음 삽입 사용 확인란을 선택 합니다.

[![는 DetailsView을 범주 데이터 원본에 바인딩하고 삽입을 사용 하도록 설정 합니다.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image6.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.png)

**그림 6**: `CategoriesDataSource`에 DetailsView 바인딩 및 삽입 사용 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image12.png))

삽입 인터페이스에서 DetailsView을 영구적으로 렌더링 하려면 해당 `DefaultMode` 속성을 `Insert`로 설정 합니다.

BoundField는 `BrochurePath` 속성이 `CategoryID`로 설정 되어 있으므로 삽입 인터페이스에서 렌더링 되지 않지만, `CategoryName`, `Description`, `NumberOfProducts`및 `InsertVisible` BoundFields에는 5 개의 `CategoryID`있습니다.`false` 이러한 BoundFields는 `GetCategories()` 메서드에서 반환 되는 열 이기 때문에 존재 합니다 .이는 ObjectDataSource가 데이터를 검색 하기 위해 호출 하는 것입니다. 그러나 삽입을 위해 사용자가 `NumberOfProducts`에 대 한 값을 지정할 수 있도록 합니다. 또한 새 범주에 대 한 그림을 업로드 하 고 브로슈어에 PDF를 업로드 하도록 허용 해야 합니다.

DetailsView에서 `NumberOfProducts` BoundField를 완전히 제거한 다음 `CategoryName`의 `HeaderText` 속성 및 `BrochurePath` BoundFields를 각각 Category 및 브로셔로 업데이트 합니다. 그런 다음 `BrochurePath` BoundField를 Templatefield로 변환로 변환 하 고 그림에 대 한 새 Templatefield로 변환를 추가 하 여이 새 Templatefield로 변환에 그림의 `HeaderText` 값을 제공 합니다. `BrochurePath` Templatefield로 변환와 CommandField Templatefield로 변환 `Picture`를 이동 합니다.

![범주 데이터 원본에 DetailsView 바인딩 및 삽입 사용](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image7.gif)

**그림 7**: `CategoriesDataSource`에 DetailsView 바인딩 및 삽입 사용

필드 편집 대화 상자를 통해 `BrochurePath` BoundField를 Templatefield로 변환로 변환한 경우 Templatefield로 변환에는 `ItemTemplate`, `EditItemTemplate`및 `InsertItemTemplate`포함 됩니다. 그러나 `InsertItemTemplate` 필요한 경우에만 다른 두 템플릿을 제거할 수 있습니다. 이 시점에서 DetailsView의 선언적 구문은 다음과 같습니다.

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample4.aspx)]

## <a name="adding-fileupload-controls-for-the-brochure-and-picture-fields"></a>브로셔 및 그림 필드에 대 한 FileUpload 컨트롤 추가

현재 `BrochurePath` Templatefield로 변환 s `InsertItemTemplate`에는 TextBox가 포함 되어 있지만 `Picture` Templatefield로 변환에는 템플릿이 포함 되어 있지 않습니다. FileUpload 컨트롤을 사용 하려면 이러한 두 Templatefield로 변환 s `InsertItemTemplate`를 업데이트 해야 합니다.

DetailsView의 스마트 태그에서 템플릿 편집 옵션을 선택한 다음 드롭다운 목록에서 `BrochurePath` Templatefield로 변환 s `InsertItemTemplate`를 선택 합니다. 텍스트 상자를 제거한 다음 FileUpload 컨트롤을 도구 상자에서 템플릿으로 끌어 옵니다. FileUpload 컨트롤 s `ID`를 `BrochureUpload`로 설정 합니다. 마찬가지로 `Picture` Templatefield로 변환 s `InsertItemTemplate`에 FileUpload 컨트롤을 추가 합니다. 이 FileUpload 컨트롤 `ID` `PictureUpload`로 설정 합니다.

[FileUpload 컨트롤을 InsertItemTemplate에 추가 ![](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image8.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image13.png)

**그림 8**: `InsertItemTemplate`에 FileUpload 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image14.png))

이러한 추가 작업을 수행한 후에는 두 개의 Templatefield로 변환 s 선언 구문이 다음과 같이 됩니다.

[!code-aspx[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample5.aspx)]

사용자가 새 범주를 추가 하는 경우 브로슈어 및 그림이 올바른 파일 형식 인지 확인 하려고 합니다. 브로슈어에 대해 사용자는 PDF를 제공 해야 합니다. 그림의 경우 이미지 파일을 업로드 하는 데 사용자가 필요 하지만, Gif 또는 JPGs 같은 특정 형식의 이미지 파일 또는 이미지 *파일만 허용 하나요* ? 다양 한 파일 형식을 허용 하기 위해 파일 형식을 캡처하는 열을 포함 하도록 `Categories` 스키마를 확장 하 여 `DisplayCategoryPicture.aspx`의 `Response.ContentType`를 통해이 형식을 클라이언트에 보낼 수 있도록 해야 합니다. 이러한 열이 없기 때문에 특정 이미지 파일 형식만 제공 하도록 사용자를 제한 하는 것이 좋습니다. `Categories` 테이블 s 기존 이미지는 비트맵 이지만 JPGs는 웹을 통해 제공 되는 이미지에 대 한 보다 적절 한 파일 형식입니다.

사용자가 잘못 된 파일 형식을 업로드 하는 경우 삽입을 취소 하 고 문제를 나타내는 메시지를 표시 해야 합니다. DetailsView 아래에 Label 웹 컨트롤을 추가 합니다. `ID` 속성을 `UploadWarning`로 설정 하 고 `Text` 속성을 지우고 `CssClass` 속성을 경고로 설정 하 고 `Visible` 및 `EnableViewState` 속성을 `false`로 설정 합니다. `Warning` CSS 클래스는 `Styles.css`에서 정의 되며 텍스트를 크게, 빨강, 기울임꼴, 굵은 글꼴로 렌더링 합니다.

> [!NOTE]
> 이상적으로 `CategoryName` 및 `Description` BoundFields는 템플릿 필드 및 사용자 지정 된 삽입 인터페이스로 변환 됩니다. 예를 들어 `Description` 인터페이스를 삽입 하는 것은 여러 줄 텍스트 상자를 통해 보다 적합할 수 있습니다. `CategoryName` 열에 `NULL` 값이 허용 되지 않으므로 사용자가 새 범주 이름에 대 한 값을 제공할 수 있도록 RequiredFieldValidator를 추가 해야 합니다. 이러한 단계는 판독기에 대 한 연습으로 남아 있습니다. 데이터 수정 인터페이스를 확대 하는 방법에 대 한 자세한 내용은 [데이터 수정 인터페이스 사용자 지정](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) 을 참조 하세요.

## <a name="step-6-saving-the-uploaded-brochure-to-the-web-server-s-file-system"></a>6 단계: 업로드 된 브로슈어를 웹 서버의 파일 시스템에 저장

사용자가 새 범주에 대 한 값을 입력 하 고 삽입 단추를 클릭 하면 포스트백이 발생 하 고 삽입 워크플로가 펼칩니다 됩니다. 먼저 DetailsView s [`ItemInserting` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserting.aspx) 발생 합니다. 그런 다음 ObjectDataSource s `Insert()` 메서드를 호출 하 여 `Categories` 테이블에 새 레코드를 추가 합니다. 그 후에는 DetailsView s [`ItemInserted` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.iteminserted.aspx) 발생 합니다.

ObjectDataSource s `Insert()` 메서드를 호출 하기 전에 먼저 사용자가 적절 한 파일 형식이 업로드 되었는지 확인 한 다음 브로슈어 PDF를 웹 서버의 파일 시스템에 저장 해야 합니다. DetailsView s `ItemInserting` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample6.cs)]

이벤트 처리기는 DetailsView 템플릿에서 `BrochureUpload` FileUpload 컨트롤을 참조 하 여 시작 합니다. 그런 다음 브로슈어를 업로드 한 경우 업로드 된 파일의 확장명을 검사 합니다. 확장이이 아니면입니다. 그런 다음, 경고가 표시 되 고, 삽입이 취소 되 고, 이벤트 처리기 실행이 종료 됩니다.

> [!NOTE]
> 업로드 된 파일의 확장에 의존 하는 것은 업로드 된 파일이 PDF 문서 인지 확인 하기 위한 것입니다. 사용자는 `.Brochure`확장을 포함 하는 유효한 PDF 문서를 포함 하거나 PDF 문서가 아닌 문서를 가져와서 `.pdf` 확장명을 지정할 수 있습니다. 파일의 이진 콘텐츠는 파일 형식을 더 결론 내릴 확인 하기 위해 프로그래밍 방식으로 검사 해야 합니다. 그러나 이러한 철저 한 접근 방식은 일반적으로 과도 합니다. 대부분의 시나리오에서는 확장을 확인 하는 것 만으로도 충분 합니다.

파일 [업로드](uploading-files-cs.md) 자습서에서 설명한 대로 파일 시스템에 파일을 저장할 때는 한 사용자의 업로드가 다른를 덮어쓰지 않도록 주의를 기울여야 합니다. 이 자습서에서는 업로드 된 파일과 동일한 이름을 사용 하려고 합니다. 그러나 동일한 파일 이름을 가진 파일이 `~/Brochures` 디렉터리에 이미 있는 경우에는 고유한 이름을 찾을 때까지 끝에 번호를 추가 합니다. 예를 들어 사용자가 `Meats.pdf`이라는 브로슈어 파일을 업로드 하지만 `~/Brochures` 폴더에 이미 `Meats.pdf` 라는 파일이 있는 경우 저장 된 파일 이름을 `Meats-1.pdf`로 변경 합니다. 이 경우 고유한 파일 이름을 찾을 때까지 `Meats-2.pdf`시도 합니다.

다음 코드는 [`File.Exists(path)` 메서드](https://msdn.microsoft.com/library/system.io.file.exists.aspx) 를 사용 하 여 지정 된 파일 이름을 가진 파일이 이미 있는지 여부를 확인 합니다. 그렇다면 충돌을 찾을 수 없을 때까지 계속 해 서 브로슈어에 새 파일 이름을 시도 합니다.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample7.cs)]

유효한 파일 이름이 발견 되 면 파일을 파일 시스템에 저장 해야 하며,이 파일 이름을 데이터베이스에 쓰도록 ObjectDataSource s `brochurePath``InsertParameter` 값을 업데이트 해야 합니다. *파일 업로드* 자습서에서 돌아와서 FileUpload 컨트롤 `SaveAs(path)` 메서드를 사용 하 여 파일을 저장할 수 있습니다. ObjectDataSource s `brochurePath` 매개 변수를 업데이트 하려면 `e.Values` 컬렉션을 사용 합니다.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample8.cs)]

## <a name="step-7-saving-the-uploaded-picture-to-the-database"></a>7 단계: 업로드 된 그림을 데이터베이스에 저장

업로드 된 그림을 새 `Categories` 레코드에 저장 하려면 업로드 한 이진 콘텐츠를 DetailsView s `ItemInserting` 이벤트의 ObjectDataSource s `picture` 매개 변수에 할당 해야 합니다. 그러나이 할당을 수행 하기 전에 먼저 업로드 된 그림이 JPG 이며 다른 이미지 형식이 아닌 JPG 인지 확인 해야 합니다. 6 단계에서와 같이에서 업로드 된 사진의 파일 확장명을 사용 하 여 해당 형식을 확인 하도록 합니다.

`Categories` 테이블은 `Picture` 열에 `NULL` 값을 허용 하지만 모든 범주에는 현재 그림이 있습니다. 에서이 페이지를 통해 새 범주를 추가할 때 사용자가 그림을 제공 하도록 합니다. 다음 코드에서는 그림이 업로드 되었으며 적절 한 확장이 있는지 확인 합니다.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample9.cs)]

이 코드는 6 단계의 코드 *앞* 에 배치 해야 합니다. 그림 업로드에 문제가 발생 하는 경우 브로슈어 파일이 파일 시스템에 저장 되기 전에 이벤트 처리기가 종료 됩니다.

적절 한 파일을 업로드 했다고 가정 하 고 다음 코드 줄을 사용 하 여 업로드 된 이진 콘텐츠를 그림 매개 변수 s 값에 할당 합니다.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample10.cs)]

## <a name="the-completeiteminsertingevent-handler"></a>Complete`ItemInserting`이벤트 처리기

완전성을 위해 다음은 전체 `ItemInserting` 이벤트 처리기입니다.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample11.cs)]

## <a name="step-8-fixing-thedisplaycategorypictureaspxpage"></a>8 단계:`DisplayCategoryPicture.aspx`페이지 수정

를 사용 하 여 마지막 몇 단계에서 생성 된 `ItemInserting` 이벤트 처리기 및 삽입 인터페이스를 테스트 합니다. 브라우저를 통해 `UploadInDetailsView.aspx` 페이지를 방문 하 여 범주를 추가 하 고, 그림을 생략 하거나, 비 JPG 그림 또는 비-PDF 브로슈어를 지정 합니다. 이러한 경우에는 오류 메시지가 표시 되 고 삽입 워크플로가 취소 됩니다.

[![잘못 된 파일 형식이 업로드 된 경우 경고 메시지가 표시 됩니다.](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image9.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image15.png)

**그림 9**: 잘못 된 파일 형식이 업로드 된 경우 경고 메시지가 표시 됨 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image16.png))

페이지에서 그림을 업로드 해야 하는 것을 확인 하 고 비 PDF 또는 비 JPG 파일을 수락 하지 않도록 확인 한 후에는 유효한 JPG 그림이 있는 새 범주를 추가 하 여 브로슈어 필드가 비어 있는 상태로 둡니다. 삽입 단추를 클릭 하면 페이지가 다시 게시 되 고 업로드 된 이미지의 이진 내용이 데이터베이스에 직접 저장 된 `Categories` 테이블에 새 레코드가 추가 됩니다. GridView가 업데이트 되 고 새로 추가 된 범주에 대 한 행을 표시 하지만 그림 10에 표시 된 것 처럼 새 범주 s 그림이 올바르게 렌더링 되지 않습니다.

[새 범주 s 그림이 표시 되지 ![](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image10.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image17.png)

**그림 10**: 새 범주 s 그림이 표시 되지 않음 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image18.png))

새 그림이 표시 되지 않는 이유는 지정 된 범주를 반환 하는 `DisplayCategoryPicture.aspx` 페이지가 OLE 헤더를 포함 하는 비트맵을 처리 하도록 구성 되어 있기 때문입니다. 이 78 바이트 헤더는 `Picture` 열 s 이진 콘텐츠에서 제거 되어 클라이언트에 다시 전송 됩니다. 그러나 방금 새 범주에 대해 업로드 한 JPG 파일에는이 OLE 머리글이 없습니다. 따라서 필요한 바이트는 이미지 s의 이진 데이터에서 제거 됩니다.

이제 `Categories` 테이블에 OLE 헤더와 JPGs의 비트맵이 모두 있으므로 원본 8 개 범주에 대 한 OLE 헤더 제거를 수행 하 고 최신 범주 레코드에 대해이 제거를 무시 하도록 `DisplayCategoryPicture.aspx`를 업데이트 해야 합니다. 다음 자습서에서는 기존 레코드의 이미지를 업데이트 하는 방법을 살펴보겠습니다. 모든 이전 범주 사진은 JPGs 되도록 업데이트 합니다. 그러나 지금은 `DisplayCategoryPicture.aspx`에서 다음 코드를 사용 하 여 원래 8 개 범주에 대해서만 OLE 헤더를 제거 합니다.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample12.cs)]

이와 같이 변경 하면 JPG 이미지가 이제 GridView에서 올바르게 렌더링 됩니다.

[새 범주에 대 한 JPG 이미지가 올바르게 렌더링 ![](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image11.gif)](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image19.png)

**그림 11**: 새 범주의 JPG 이미지가 올바르게 렌더링 됨 ([전체 크기 이미지를 보려면 클릭](including-a-file-upload-option-when-adding-a-new-record-cs/_static/image20.png))

## <a name="step-9-deleting-the-brochure-in-the-face-of-an-exception"></a>9 단계: 예외의 면에서 브로슈어 삭제

이진 데이터를 웹 서버의 파일 시스템에 저장 하는 문제 중 하나는 데이터 모델과 해당 이진 데이터 간의 연결 해제를 도입 하는 것입니다. 따라서 레코드를 삭제할 때마다 파일 시스템의 해당 이진 데이터도 제거 해야 합니다. 삽입 하는 경우에도이를 재생할 수 있습니다. 사용자가 유효한 그림과 브로슈어를 지정 하 여 새 범주를 추가 하는 시나리오를 고려해 보십시오. 삽입 단추를 클릭 하면 포스트백이 발생 하 고 DetailsView s `ItemInserting` 이벤트가 발생 하 여 브로슈어에 웹 서버 파일 시스템에 저장 됩니다. 그런 다음 `CategoriesBLL` 클래스 s `InsertWithPicture` 메서드를 호출 하는 ObjectDataSource s `Insert()` 메서드를 호출 합니다 .이 메서드는 `CategoriesTableAdapter` s `InsertWithPicture` 메서드를 호출 합니다.

이제 데이터베이스가 오프 라인 상태 이거나 `INSERT` SQL 문에 오류가 있는 경우 어떻게 되나요? 분명히 삽입이 실패 하므로 새 범주 행이 데이터베이스에 추가 되지 않습니다. 그러나 업로드 된 브로슈어 파일은 웹 서버의 파일 시스템에 그대로 남아 있습니다. 삽입 하는 동안 예외가 발생 한 경우이 파일을 삭제 해야 합니다.

[ASP.NET 페이지 자습서의 BLL 및 DAL 수준 예외 처리](../editing-inserting-and-deleting-data/handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) 에서 앞서 설명한 것 처럼, 아키텍처의 깊이 내에서 예외가 throw 되 면 다양 한 계층을 통해 버블링 됩니다. 프레젠테이션 계층에서 DetailsView s `ItemInserted` 이벤트에서 예외가 발생 했는지 여부를 확인할 수 있습니다. 이 이벤트 처리기는 또한 ObjectDataSource s `InsertParameters`의 값을 제공 합니다. 따라서 예외가 있는지 확인 하 고, 필요한 경우 ObjectDataSource s `brochurePath` 매개 변수로 지정 된 파일을 삭제 하는 `ItemInserted` 이벤트에 대 한 이벤트 처리기를 만들 수 있습니다.

[!code-csharp[Main](including-a-file-upload-option-when-adding-a-new-record-cs/samples/sample13.cs)]

## <a name="summary"></a>요약

이진 데이터를 포함 하는 레코드를 추가 하기 위해 웹 기반 인터페이스를 제공 하기 위해 수행 해야 하는 여러 단계가 있습니다. 이진 데이터를 데이터베이스에 직접 저장 하는 경우에는 이진 데이터가 삽입 되는 경우를 처리 하는 특정 메서드를 추가 하 여 아키텍처를 업데이트 해야 할 가능성이 있습니다. 아키텍처가 업데이트 된 후 다음 단계는 삽입 인터페이스를 만드는 것입니다 .이 인터페이스는 각 이진 데이터 필드에 대 한 FileUpload 컨트롤을 포함 하도록 사용자 지정 된 DetailsView을 사용 하 여 수행할 수 있습니다. 업로드 된 데이터를 웹 서버의 파일 시스템에 저장 하거나 DetailsView s `ItemInserting` 이벤트 처리기의 데이터 원본 매개 변수에 할당할 수 있습니다.

이진 데이터를 파일 시스템에 저장 하려면 데이터를 데이터베이스에 직접 저장 하는 것 보다 더 많은 계획이 필요 합니다. 한 사용자의 업로드에서 다른 사용자를 덮어쓰는 것을 방지 하려면 이름 지정 체계를 선택 해야 합니다. 또한 데이터베이스 삽입에 실패 하는 경우 업로드 된 파일을 삭제 하려면 추가 단계를 수행 해야 합니다.

이제 브로슈어 및 그림을 사용 하 여 시스템에 새 범주를 추가할 수 있지만, 기존 범주 이진 데이터를 업데이트 하는 방법 또는 삭제 된 범주에 대 한 이진 데이터를 올바르게 제거 하는 방법을 확인 합니다. 다음 자습서에서는 이러한 두 가지 항목을 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 리드 검토자는 Dave Gardner, Teresa Murphy 및 Bernadette Leigh 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](displaying-binary-data-in-the-data-web-controls-cs.md)
> [다음](updating-and-deleting-existing-binary-data-cs.md)
