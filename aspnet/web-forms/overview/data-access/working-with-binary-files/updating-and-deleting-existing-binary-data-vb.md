---
uid: web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
title: 기존 이진 데이터 업데이트 및 삭제 (VB) | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서 GridView 컨트롤을 사용 하 여 텍스트 데이터를 간단 하 게 편집 하 고 삭제 하는 방법을 살펴보았습니다. 이 자습서에서는 GridView 컨트롤이 어떻게 설정 되었는지 확인 합니다.
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 3a052ced-9cf5-47b8-a400-934f0b687c26
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 27ff6941008b4e7bf6d632e4c248fd1d35fb3589
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621596"
---
# <a name="updating-and-deleting-existing-binary-data-vb"></a>기존 이진 데이터 업데이트 및 삭제(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_57_VB.exe) 또는 [PDF 다운로드](updating-and-deleting-existing-binary-data-vb/_static/datatutorial57vb1.pdf)

> 이전 자습서에서 GridView 컨트롤을 사용 하 여 텍스트 데이터를 간단 하 게 편집 하 고 삭제 하는 방법을 살펴보았습니다. 이 자습서에서는 GridView 컨트롤이 이진 데이터를 데이터베이스에 저장 하거나 파일 시스템에 저장 하는지 여부에 관계 없이이를 사용 하 여 이진 데이터를 편집 하 고 삭제할 수 있는 방법에 대해 알아봅니다.

## <a name="introduction"></a>소개

지난 세 자습서를 통해 이진 데이터를 사용 하기 위한 약간의 기능을 추가 했습니다. 먼저 `Categories` 테이블에 `BrochurePath` 열을 추가 하 고 그에 따라 아키텍처를 업데이트 합니다. 또한 이미지 파일의 이진 콘텐츠를 포함 하는 기존 `Picture` 열에 Categories 테이블 s를 사용 하 여 데이터 액세스 계층 및 비즈니스 논리 계층 메서드를 추가 했습니다. 에 이진 데이터를 제공 하는 웹 페이지를 GridView의 다운로드 링크에 표시 하 고, 범주를 `<img>` 요소에 표시 하 고, 사용자가 새 범주를 추가 하 고 브로슈어 및 그림 데이터를 업로드할 수 있도록 DetailsView을 추가 했습니다.

구현 된 것으로 남아 있는 모든 항목을 편집 하 고 삭제 하는 기능은 GridView s 기본 제공 편집 및 삭제 기능을 사용 하 여이 자습서에서 수행할 수 있습니다. 범주를 편집할 때 사용자는 필요에 따라 새 그림을 업로드 하거나 범주에서 기존 그림을 계속 사용할 수 있습니다. 브로슈어에는 기존 브로슈어를 사용 하도록 선택 하거나, 새 브로슈어를 업로드 하거나, 범주에 연결 된 브로슈어가 더 이상 없음을 나타낼 수 있습니다. S를 시작 하겠습니다.

## <a name="step-1-updating-the-data-access-layer"></a>1 단계: 데이터 액세스 계층 업데이트

DAL에는 자동으로 생성 된 `Insert`, `Update`및 `Delete` 메서드가 있지만 이러한 메서드는 `Picture` 열을 포함 하지 않는 `CategoriesTableAdapter` s 주 쿼리를 기반으로 생성 되었습니다. 따라서 `Insert` 및 `Update` 메서드에는 범주 그림에 대 한 이진 데이터를 지정 하는 매개 변수가 포함 되지 않습니다. [이전 자습서](including-a-file-upload-option-when-adding-a-new-record-vb.md)에서와 같이 이진 데이터를 지정할 때 `Categories` 테이블을 업데이트 하기 위한 새 TableAdapter 메서드를 만들어야 합니다.

형식화 된 데이터 집합을 열고 디자이너에서 `CategoriesTableAdapter` s 헤더를 마우스 오른쪽 단추로 클릭 한 다음 상황에 맞는 메뉴에서 쿼리 추가를 선택 하 여 TableAdapter 쿼리 구성 마법사를 시작 합니다. 이 마법사는 TableAdapter 쿼리가 데이터베이스에 액세스 하는 방법을 묻는 메시지를 사용 하 여 시작 합니다. SQL 문 사용을 선택 하 고 다음을 클릭 합니다. 다음 단계에서는 생성할 쿼리 유형을 묻는 메시지를 표시 합니다. `Categories` 테이블에 새 레코드를 추가 하는 쿼리를 다시 작성 하기 때문에 업데이트를 선택 하 고 다음을 클릭 합니다.

[업데이트 옵션 ![선택 합니다.](updating-and-deleting-existing-binary-data-vb/_static/image2.png)](updating-and-deleting-existing-binary-data-vb/_static/image1.png)

**그림 1**: 업데이트 옵션 선택 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image3.png))

이제 `UPDATE` SQL 문을 지정 해야 합니다. 마법사에서는 TableAdapter s 주 쿼리에 해당 하는 `UPDATE` 문을 자동으로 제안 합니다. 즉, `CategoryName`, `Description`및 `BrochurePath` 값을 업데이트 합니다. `Picture` 열이 `@Picture` 매개 변수와 함께 포함 되도록 문을 다음과 같이 변경 합니다.

[!code-sql[Main](updating-and-deleting-existing-binary-data-vb/samples/sample1.sql)]

마법사의 마지막 화면에서 새 TableAdapter 메서드의 이름을 묻는 메시지를 표시 합니다. `UpdateWithPicture`를 입력 하 고 마침을 클릭 합니다.

[새 TableAdapter 메서드 UpdateWithPicture의 이름을 ![합니다.](updating-and-deleting-existing-binary-data-vb/_static/image5.png)](updating-and-deleting-existing-binary-data-vb/_static/image4.png)

**그림 2**: 새 TableAdapter 메서드 이름 `UpdateWithPicture` ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image6.png))

## <a name="step-2-adding-the-business-logic-layer-methods"></a>2 단계: 비즈니스 논리 계층 메서드 추가

DAL을 업데이트 하는 것 외에도 범주를 업데이트 하 고 삭제 하는 메서드를 포함 하도록 BLL을 업데이트 해야 합니다. 이러한 메서드는 프레젠테이션 계층에서 호출 됩니다.

범주를 삭제 하는 경우 `CategoriesTableAdapter` s 자동 생성 `Delete` 메서드를 사용할 수 있습니다. `CategoriesBLL` 클래스에 다음 메서드를 추가 합니다.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample2.vb)]

이 자습서에서는를 사용 하 여 이진 그림 데이터를 필요로 하는 범주를 업데이트 하는 두 가지 메서드를 만들고 방금 `CategoriesTableAdapter`에 추가한 `UpdateWithPicture` 메서드를 호출 하 고, `CategoryName`, `Description`및 `BrochurePath` 값만 허용 하 고 `CategoriesTableAdapter` 클래스의 자동 생성 `Update` 문을 사용 합니다. 두 가지 방법을 사용 하는 이유는 경우에 따라 사용자가 범주 그림을 다른 필드와 함께 업데이트 하려고 할 수 있습니다 .이 경우 사용자가 새 그림을 업로드 해야 합니다. 업로드 된 그림의 이진 데이터는 `UPDATE` 문에서 사용할 수 있습니다. 다른 경우에는 사용자가 이름 및 설명만 업데이트 하는 것에 관심이 있을 수 있습니다. 그러나 `UPDATE` 문에 `Picture` 열의 이진 데이터만 필요한 경우에도 해당 정보를 제공 해야 합니다. 이렇게 하려면 편집 중인 레코드의 그림 데이터를 다시 가져오기 위해 데이터베이스에 대 한 추가 여행이 필요 합니다. 따라서 두 개의 `UPDATE` 메서드가 필요 합니다. 비즈니스 논리 계층에서는 범주를 업데이트할 때 그림 데이터가 제공 되는지 여부에 따라 사용할 항목을 결정 합니다.

이를 용이 하 게 하려면 두 개의 메서드를 모두 명명 된 `UpdateCategory``CategoriesBLL` 클래스에 추가 합니다. 첫 번째는 세 개의 `String` s, `Byte` 배열 및 `Integer`을 입력 매개 변수로 허용 해야 합니다. 두 번째는 두 개의 `String` s와 `Integer`입니다. `String` 입력 매개 변수는 범주 이름, 설명 및 브로슈어 파일 경로에 대 한 것이 고, `Byte` 배열은 범주 s 그림의 이진 콘텐츠에 대 한 것 이며, `Integer`는 업데이트할 레코드의 `CategoryID`를 식별 합니다. 전달 된 `Byte` 배열이 `Nothing`되는 경우 첫 번째 오버 로드는 두 번째 오버 로드를 호출 합니다.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample3.vb)]

## <a name="step-3-copying-over-the-insert-and-view-functionality"></a>3 단계: 삽입 및 보기 기능을 통해 복사

[이전 자습서](including-a-file-upload-option-when-adding-a-new-record-vb.md) 에서는 GridView의 모든 범주에 나열 된 `UploadInDetailsView.aspx` 라는 페이지를 만들고 DetailsView를 제공 하 여 시스템에 새 범주를 추가 했습니다. 이 자습서에서는 편집 및 삭제 지원을 포함 하도록 GridView를 확장 합니다. `UploadInDetailsView.aspx`에서 계속 작업 하는 대신이 자습서를 `UpdatingAndDeleting.aspx` 페이지에서 동일한 폴더 `~/BinaryData`에 추가 합니다. `UploadInDetailsView.aspx`에서 선언적 태그와 코드를 복사 하 여 `UpdatingAndDeleting.aspx`에 붙여넣습니다.

`UploadInDetailsView.aspx` 페이지를 열어 시작 합니다. 그림 3에 나와 있는 것 처럼 `<asp:Content>` 요소 내의 모든 선언 구문을 복사 합니다. 그런 다음 `UpdatingAndDeleting.aspx`를 열고 `<asp:Content>` 요소 내에이 태그를 붙여 넣습니다. 마찬가지로 `UploadInDetailsView.aspx` 페이지의 코드 숨김이 클래스에서 `UpdatingAndDeleting.aspx`로 코드를 복사 합니다.

[UploadInDetailsView에서 선언적 태그 ![복사 합니다.](updating-and-deleting-existing-binary-data-vb/_static/image8.png)](updating-and-deleting-existing-binary-data-vb/_static/image7.png)

**그림 3**: `UploadInDetailsView.aspx`에서 선언적 태그 복사 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image9.png))

선언적 태그와 코드를 복사한 후 `UpdatingAndDeleting.aspx`를 방문 합니다. 이전 자습서의 `UploadInDetailsView.aspx` 페이지와 동일한 출력이 표시 되 고 사용자 환경이 동일 해야 합니다.

## <a name="step-4-adding-deleting-support-to-the-objectdatasource-and-gridview"></a>4 단계: ObjectDataSource 및 GridView에 대 한 지원 삭제 추가

[데이터 삽입, 업데이트 및 삭제에 대 한 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 에 설명 된 대로, GridView는 기본 제공 되는 삭제 기능을 제공 하며, 표 원본 데이터 원본에서 삭제를 지 원하는 경우 확인란의 틱에서 이러한 기능을 사용 하도록 설정할 수 있습니다. 현재 GridView가 바인딩되는 ObjectDataSource (`CategoriesDataSource`)는 삭제를 지원 하지 않습니다.

이를 해결 하려면 ObjectDataSource s 스마트 태그에서 데이터 원본 구성 옵션을 클릭 하 여 마법사를 시작 합니다. 첫 번째 화면에서는 `CategoriesBLL` 클래스와 함께 사용 하도록 ObjectDataSource를 구성 하는 방법을 보여 줍니다. 다음에 적중 합니다. 현재는 ObjectDataSource s `InsertMethod` 및 `SelectMethod` 속성만 지정 됩니다. 그러나 마법사는 업데이트 및 삭제 탭의 드롭다운 목록을 각각 `UpdateCategory` 및 `DeleteCategory` 메서드와 함께 자동으로 채웁니다. 이는 `CategoriesBLL` 클래스에서를 업데이트 및 삭제를 위한 기본 메서드로 `DataObjectMethodAttribute`를 사용 하 여 이러한 메서드를 표시 했기 때문입니다.

지금은 업데이트 탭의 드롭다운 목록을 (없음)으로 설정 하 고, 삭제 탭의 드롭다운 목록을 `DeleteCategory`로 설정 된 상태로 둡니다. 6 단계에서이 마법사로 돌아와서 업데이트 지원을 추가 합니다.

[DeleteCategory 메서드를 사용 하도록 ObjectDataSource 구성 ![](updating-and-deleting-existing-binary-data-vb/_static/image11.png)](updating-and-deleting-existing-binary-data-vb/_static/image10.png)

**그림 4**: `DeleteCategory` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image12.png))

> [!NOTE]
> 마법사가 완료 되 면 Visual Studio에서 필드와 키를 새로 고칠지 여부를 묻는 메시지를 표시할 수 있습니다. 그러면 데이터 웹 컨트롤 필드가 다시 생성 됩니다. 예를 선택 하면 수행한 필드 사용자 지정 항목을 덮어쓰기 때문에 아니요를 선택 합니다.

이제 ObjectDataSource에는 `DeleteParameter`뿐만 아니라 `DeleteMethod` 속성 값이 포함 됩니다. 마법사를 사용 하 여 메서드를 지정 하는 경우 Visual Studio는 ObjectDataSource s `OldValuesParameterFormatString` 속성을 `original_{0}`로 설정 하므로 update 및 delete 메서드 호출에 문제가 발생 합니다. 따라서이 속성을 완전히 지우거 나 `{0}`기본값으로 다시 설정 합니다. 이 ObjectDataSource 속성에서 메모리를 새로 고쳐야 하는 경우에는 [데이터 삽입, 업데이트 및 삭제 자습서의 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 를 참조 하세요.

마법사를 완료 하 고 `OldValuesParameterFormatString`를 수정한 후 ObjectDataSource의 선언적 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample4.aspx)]

ObjectDataSource를 구성한 후 GridView의 스마트 태그에서 삭제 사용 확인란을 선택 하 여 GridView에 삭제 기능을 추가 합니다. 그러면 `ShowDeleteButton` 속성이 `True`로 설정 된 GridView 필드가 CommandField에 추가 됩니다.

[GridView에서 삭제에 대 한 지원을 사용 하도록 설정 ![](updating-and-deleting-existing-binary-data-vb/_static/image14.png)](updating-and-deleting-existing-binary-data-vb/_static/image13.png)

**그림 5**: GridView에서 삭제 지원 사용 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image15.png))

잠시 시간을 사용 하 여 삭제 기능을 테스트해 보세요. `Products` 테이블 s `CategoryID`와 `Categories` 테이블 s `CategoryID`사이에 외래 키가 있으므로 처음 8 개 범주 중 하나를 삭제 하려고 하면 foreign key 제약 조건 위반 예외가 발생 합니다. 이 기능을 테스트 하려면 브로슈어와 그림을 모두 제공 하 여 새 범주를 추가 합니다. 그림 6에 표시 된 내 테스트 범주에는 `Test.pdf` 및 테스트 그림 이라는 테스트 브로셔 파일이 포함 되어 있습니다. 그림 7에는 테스트 범주가 추가 된 후의 GridView가 나와 있습니다.

[브로슈어 및 이미지를 사용 하 여 테스트 범주 추가 ![](updating-and-deleting-existing-binary-data-vb/_static/image17.png)](updating-and-deleting-existing-binary-data-vb/_static/image16.png)

**그림 6**: 브로슈어 및 이미지를 사용 하 여 테스트 범주 추가 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image18.png))

[테스트 범주를 삽입 한 후 ![GridView에 표시 됩니다.](updating-and-deleting-existing-binary-data-vb/_static/image20.png)](updating-and-deleting-existing-binary-data-vb/_static/image19.png)

**그림 7**: 테스트 범주를 삽입 한 후 GridView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image21.png)).

Visual Studio에서 솔루션 탐색기를 새로 고칩니다. 이제 `Test.pdf` `~/Brochures` 폴더에 새 파일이 표시 됩니다 (그림 8 참조).

그런 다음 테스트 범주 행의 삭제 링크를 클릭 하 여 페이지를 다시 게시 하 고 `CategoriesBLL` 클래스 s `DeleteCategory` 메서드를 실행 합니다. 이렇게 하면 DAL s `Delete` 메서드가 호출 되어 적절 한 `DELETE` 문을 데이터베이스로 보냅니다. 그런 다음 데이터를 GridView로 다시 바인딩 하 고 테스트 범주가 더 이상 존재 하지 않는 상태로 클라이언트에 태그를 다시 보냅니다.

Delete 워크플로는 `Categories` 테이블에서 테스트 범주 레코드를 제거 했지만 웹 서버 파일 시스템에서 해당 브로슈어 파일을 제거 하지 않았습니다. 솔루션 탐색기를 새로 고치면 `Test.pdf` `~/Brochures` 폴더에 계속 남아 있는 것을 볼 수 있습니다.

![웹 서버 파일 시스템에서 테스트 .pdf 파일이 삭제 되지 않았습니다.](updating-and-deleting-existing-binary-data-vb/_static/image1.gif)

**그림 8**: 웹 서버 파일 시스템에서 `Test.pdf` 파일이 삭제 되지 않았습니다.

## <a name="step-5-removing-the-deleted-category-s-brochure-file"></a>5 단계: 삭제 된 범주 브로슈어 파일 제거

이진 데이터를 데이터베이스 외부에 저장 하는 단점이 중 하나는 연결 된 데이터베이스 레코드가 삭제 될 때 이러한 파일을 정리 하기 위해 추가 단계를 수행 해야 한다는 것입니다. GridView와 ObjectDataSource는 delete 명령이 수행 되기 전후에 발생 하는 이벤트를 제공 합니다. 실제로 사전 및 사후 작업 이벤트에 대 한 이벤트 처리기를 만들어야 합니다. `Categories` 레코드를 삭제 하기 전에 해당 PDF 파일의 경로를 확인 해야 하지만 일부 예외가 있고 범주가 삭제 되지 않는 경우 범주가 삭제 되기 전에 PDF를 삭제 하지 않으려고 합니다.

GridView s [`RowDeleting` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx) 는 ObjectDataSource s delete 명령이 호출 되기 전에 실행 되 고 그 후에는 해당 [`RowDeleted` 이벤트가](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleted.aspx) 발생 합니다. 다음 코드를 사용 하 여 이러한 두 이벤트에 대 한 이벤트 처리기를 만듭니다.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample5.vb)]

`RowDeleting` 이벤트 처리기에서 삭제 되는 행의 `CategoryID`는 GridView s `DataKeys` 컬렉션에서 grabbed `e.Keys` 컬렉션을 통해이 이벤트 처리기에서 액세스할 수 있습니다. 그런 다음 삭제할 레코드에 대 한 정보를 반환 하기 위해 `CategoriesBLL` 클래스 `GetCategoryByCategoryID(categoryID)`를 호출 합니다. 반환 된 `CategoriesDataRow` 개체에`NULL``BrochurePath` 값이 없는 경우 `RowDeleted` 이벤트 처리기에서 파일을 삭제할 수 있도록 `deletedCategorysPdfPath` 페이지 변수에 저장 됩니다.

> [!NOTE]
> `RowDeleting` 이벤트 처리기에서 삭제 되는 `Categories` 레코드에 대 한 `BrochurePath` 정보를 검색 하는 대신 GridView의 `DataKeyNames` 속성에 `BrochurePath`를 추가 하 고 `e.Keys` 컬렉션을 통해 레코드의 값에 액세스할 수도 있습니다. 이렇게 하면 GridView의 뷰 상태 크기가 약간 증가 하지만 필요한 코드의 양을 줄이고 데이터베이스에 대 한 왕복을 저장할 수 있습니다.

ObjectDataSource의 기본 delete 명령이 호출 된 후 GridView s `RowDeleted` 이벤트 처리기가 발생 합니다. 데이터를 삭제 하는 데 예외가 없고 `deletedCategorysPdfPath`에 대 한 값이 있는 경우 PDF는 파일 시스템에서 삭제 됩니다. 이 추가 코드는 그림에 연결 된 범주 이진 데이터를 정리 하는 데 필요 하지 않습니다. 이는 그림 데이터가 데이터베이스에 직접 저장 되기 때문에 `Categories` 행을 삭제 하면 해당 범주 그림 데이터도 삭제 됩니다.

두 이벤트 처리기를 추가한 후에이 테스트 사례를 다시 실행 합니다. 범주를 삭제 하면 연결 된 PDF도 삭제 됩니다.

기존 레코드의 연결 된 이진 데이터를 업데이트 하면 몇 가지 흥미로운 과제가 제공 됩니다. 이 자습서의 나머지 부분에서는 브로슈어 및 그림에 업데이트 기능을 추가 하는 것을 자세하게 다룹니다. 6 단계 7 단계에서 그림 업데이트를 확인 하는 동안 브로슈어 정보를 업데이트 하는 방법을 탐색 합니다.

## <a name="step-6-updating-a-category-s-brochure"></a>6 단계: 범주 브로슈어 업데이트

데이터 삽입, 업데이트 및 삭제에 대 한 개요에서 설명한 대로 GridView는 기본 데이터 소스가 적절 하 게 구성 된 경우 checkbox의 틱으로 구현할 수 있는 기본 제공 행 수준 편집 지원을 제공 합니다. 현재 `CategoriesDataSource` ObjectDataSource는 업데이트 지원을 포함 하도록 아직 구성 되지 않았기 때문에에 추가 해 보겠습니다.

ObjectDataSource s 마법사에서 데이터 소스 구성 링크를 클릭 하 고 두 번째 단계를 진행 합니다. `CategoriesBLL`에 사용 되는 `DataObjectMethodAttribute` 때문에 업데이트 드롭다운 목록은 4 개의 입력 매개 변수 (모든 열에 대해서는 `Picture`)를 허용 하는 `UpdateCategory` 오버 로드로 자동으로 채워집니다. 5 개의 매개 변수가 있는 오버 로드를 사용 하도록이를 변경 합니다.

[그림에 대 한 매개 변수를 포함 하는 UpdateCategory 메서드를 사용 하도록 ObjectDataSource를 구성 ![](updating-and-deleting-existing-binary-data-vb/_static/image23.png)](updating-and-deleting-existing-binary-data-vb/_static/image22.png)

**그림 9**: `Picture`에 대 한 매개 변수를 포함 하는 `UpdateCategory` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image24.png))

이제 ObjectDataSource는 `UpdateMethod` 속성 값과 해당 `UpdateParameter`를 포함 합니다. 4 단계에서 설명한 대로 Visual Studio에서는 데이터 소스 구성 마법사를 사용할 때 ObjectDataSource s `OldValuesParameterFormatString` 속성을 `original_{0}`로 설정 합니다. 이렇게 하면 update 및 delete 메서드 호출에 문제가 발생 합니다. 따라서이 속성을 완전히 지우거 나 `{0}`기본값으로 다시 설정 합니다.

마법사를 완료 하 고 `OldValuesParameterFormatString`를 수정한 후 ObjectDataSource의 선언적 태그는 다음과 같습니다.

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample6.aspx)]

GridView s 기본 제공 편집 기능을 켜려면 GridView의 스마트 태그에서 편집 사용 옵션을 선택 합니다. 그러면 CommandField s `ShowEditButton` 속성이 `True`으로 설정 되어 편집 단추와 편집 중인 행의 업데이트 및 취소 단추가 추가 됩니다.

[편집을 지원 하도록 GridView를 구성 ![](updating-and-deleting-existing-binary-data-vb/_static/image26.png)](updating-and-deleting-existing-binary-data-vb/_static/image25.png)

**그림 10**: 편집을 지원 하도록 GridView 구성 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image27.png))

브라우저를 통해 페이지를 방문 하 고 행의 편집 단추 중 하나를 클릭 합니다. `CategoryName` 및 `Description` BoundFields는 입력란으로 렌더링 됩니다. `BrochurePath` Templatefield로 변환에는 `EditItemTemplate`없으므로 해당 `ItemTemplate`을 브로슈어에 대 한 링크를 계속 표시 합니다. `Picture` ImageField는 `Text` 속성이 ImageField s `DataImageUrlField` 값의 값 (이 경우 `CategoryID`)을 할당 하는 TextBox로 렌더링 됩니다.

[![GridView에 BrochurePath에 대 한 편집 인터페이스가 없습니다.](updating-and-deleting-existing-binary-data-vb/_static/image29.png)](updating-and-deleting-existing-binary-data-vb/_static/image28.png)

**그림 11**: GridView에 `BrochurePath` ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image30.png))에 대 한 편집 인터페이스가 없습니다.

## <a name="customizing-thebrochurepaths-editing-interface"></a>`BrochurePath`s 편집 인터페이스 사용자 지정

사용자가 다음 중 하나를 수행할 수 있는 `BrochurePath` Templatefield로 변환에 대 한 편집 인터페이스를 만들어야 합니다.

- 범주 브로슈어를 있는 그대로 둡니다.
- 새 브로슈어를 업로드 하 여 범주 브로슈어를 업데이트 하거나
- 범주를 모두 제거 합니다 (범주가 더 이상 연결 된 브로슈어를 포함 하지 않는 경우).

또한 `Picture` ImageField s 편집 인터페이스를 업데이트 해야 하지만 7 단계에서이를 확인할 수 있습니다.

GridView s 스마트 태그에서 템플릿 편집 링크를 클릭 하 고 드롭다운 목록에서 `BrochurePath` Templatefield로 변환 s `EditItemTemplate`를 선택 합니다. RadioButtonList 웹 컨트롤을이 템플릿에 추가 하 고 해당 `ID` 속성을 `BrochureOptions`로 설정 하 고 `AutoPostBack` 속성을 `True`로 설정 합니다. 속성 창에서 `Items` 속성의 줄임표를 클릭 하면 `ListItem` 컬렉션 편집기가 표시 됩니다. 각각 `Value` s 1, 2, 3을 사용 하 여 다음 세 가지 옵션을 추가 합니다.

- 현재 브로슈어 사용
- 현재 브로슈어 제거
- 새 브로슈어 업로드

첫 번째 `ListItem` s `Selected` 속성을 `True`로 설정 합니다.

![RadioButtonList에 세 개의 ListItems를 추가 합니다.](updating-and-deleting-existing-binary-data-vb/_static/image2.gif)

**그림 12**: RadioButtonList에 세 개의 `ListItem` s 추가

RadioButtonList 아래에 `BrochureUpload`이라는 FileUpload 컨트롤을 추가 합니다. `Visible` 속성을 `False`로 설정 합니다.

[RadioButtonList 및 FileUpload 컨트롤을 EditItemTemplate에 추가 ![](updating-and-deleting-existing-binary-data-vb/_static/image32.png)](updating-and-deleting-existing-binary-data-vb/_static/image31.png)

**그림 13**: `EditItemTemplate`에 RadioButtonList 및 FileUpload 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image33.png))

이 RadioButtonList는 사용자에 대 한 세 가지 옵션을 제공 합니다. FileUpload 컨트롤은 마지막 옵션인 새 브로슈어 업로드가 선택 된 경우에만 표시 됩니다. 이 작업을 수행 하려면 RadioButtonList s `SelectedIndexChanged` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 추가 합니다.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample7.vb)]

RadioButtonList 및 FileUpload 컨트롤은 템플릿 내에 있으므로 프로그래밍 방식으로 이러한 컨트롤에 액세스 하려면 약간의 코드를 작성 해야 합니다. `SelectedIndexChanged` 이벤트 처리기는 `sender` 입력 매개 변수에 RadioButtonList의 참조를 전달 합니다. FileUpload 컨트롤을 가져오려면 RadioButtonList s 부모 컨트롤을 가져와 여기에서 `FindControl("controlID")` 메서드를 사용 해야 합니다. RadioButtonList 및 FileUpload 컨트롤에 대 한 참조가 있으면 FileUpload 컨트롤 s `Visible` 속성은 RadioButtonList s이 (가) 3 인 경우에만 `True`로 설정 됩니다 .이는 `SelectedValue` s가 새 브로슈어에 업로드 `ListItem``Value`입니다.

이 코드를 사용 하면 잠시 후 편집 인터페이스를 테스트 합니다. 행에 대 한 편집 단추를 클릭 합니다. 처음에는 현재 브로슈어 사용 옵션을 선택 해야 합니다. 선택한 인덱스를 변경 하면 포스트백이 발생 합니다. 세 번째 옵션을 선택 하면 FileUpload 컨트롤이 표시 되 고 그렇지 않으면 숨겨집니다. 그림 14에서는 편집 단추를 처음 클릭할 때 편집 인터페이스를 보여 줍니다. 그림 15에서는 새 브로슈어 업로드 옵션을 선택한 후의 인터페이스를 보여 줍니다.

[처음 ![현재 브로슈어 사용 옵션이 선택 되어 있습니다.](updating-and-deleting-existing-binary-data-vb/_static/image35.png)](updating-and-deleting-existing-binary-data-vb/_static/image34.png)

**그림 14**: 처음에는 현재 브로슈어 사용 옵션이 선택 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image36.png)).

[새 브로슈어 업로드 옵션을 선택 ![FileUpload 컨트롤이 표시 됩니다.](updating-and-deleting-existing-binary-data-vb/_static/image38.png)](updating-and-deleting-existing-binary-data-vb/_static/image37.png)

**그림 15**: 새 브로슈어 업로드 옵션을 선택 하면 FileUpload 컨트롤이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image39.png)).

## <a name="saving-the-brochure-file-and-updating-thebrochurepathcolumn"></a>브로슈어 파일 저장 및`BrochurePath`열 업데이트

GridView s 업데이트 단추를 클릭 하면 해당 `RowUpdating` 이벤트가 발생 합니다. ObjectDataSource s update 명령이 호출 된 다음 GridView s `RowUpdated` 이벤트가 발생 합니다. 삭제 워크플로와 마찬가지로 두 이벤트 모두에 대 한 이벤트 처리기를 만들어야 합니다. `RowUpdating` 이벤트 처리기에서 `BrochureOptions` RadioButtonList `SelectedValue`를 기반으로 수행할 작업을 결정 해야 합니다.

- `SelectedValue` 1 이면 동일한 `BrochurePath` 설정을 계속 사용 합니다. 따라서 ObjectDataSource s `brochurePath` 매개 변수를 업데이트할 레코드의 기존 `BrochurePath` 값으로 설정 해야 합니다. ObjectDataSource s `brochurePath` 매개 변수는 `e.NewValues["brochurePath"] = value`를 사용 하 여 설정할 수 있습니다.
- `SelectedValue` 2 인 경우에는 레코드 s `BrochurePath` 값을 `NULL`로 설정 합니다. ObjectDataSource s `brochurePath` 매개 변수를 `Nothing`로 설정 하면이를 수행할 수 있습니다. 그러면 `UPDATE` 문에서 데이터베이스 `NULL` 사용 됩니다. 제거할 기존 브로셔 파일이 있으면 기존 파일을 삭제 해야 합니다. 그러나 예외를 발생 시 키 지 않고 업데이트가 완료 되는 경우에만이 작업을 수행 하려고 합니다.
- `SelectedValue` 3 인 경우 사용자가 PDF 파일을 업로드 한 다음 파일 시스템에 저장 하 고 레코드의 `BrochurePath` 열 값을 업데이트 합니다. 또한 기존 브로셔 파일이 교체 되는 경우 이전 파일을 삭제 해야 합니다. 그러나 예외를 발생 시 키 지 않고 업데이트가 완료 되는 경우에만이 작업을 수행 하려고 합니다.

RadioButtonList s `SelectedValue`이 3 일 때 완료 해야 하는 단계는 DetailsView s `ItemInserting` 이벤트 처리기에서 사용 하는 것과 거의 동일 합니다. 이 이벤트 처리기는 [이전 자습서](including-a-file-upload-option-when-adding-a-new-record-vb.md)에서 추가한 DetailsView 컨트롤에서 새 범주 레코드가 추가 될 때 실행 됩니다. 따라서이 기능을 별도의 메서드로 리팩터링할 behooves. 특히 일반적인 기능을 다음 두 가지 방법으로 이동 했습니다.

- `ProcessBrochureUpload(FileUpload, out bool)`은 입력으로 FileUpload 제어 인스턴스와 삭제 또는 편집 작업을 계속할지 여부를 지정 하는 출력 부울 값과, 일부 유효성 검사 오류로 인해 취소 해야 하는지 여부를 지정 하는 출력 부울 값을 허용 합니다. 이 메서드는 저장 된 파일의 경로를 반환 하거나 파일을 저장 하지 않은 경우 `null`을 반환 합니다.
- `DeleteRememberedBrochurePath` `deletedCategorysPdfPath` `null`되지 않은 경우 `deletedCategorysPdfPath` 페이지 변수에서 경로에 지정 된 파일을 삭제 합니다.

이러한 두 메서드의 코드는 다음과 같습니다. 이전 자습서에서 `ProcessBrochureUpload`와 DetailsView s `ItemInserting` 이벤트 처리기 간의 유사성을 확인 합니다. 이 자습서에서는 이러한 새 메서드를 사용 하도록 DetailsView s 이벤트 처리기를 업데이트 했습니다. 이 자습서와 관련 된 코드를 다운로드 하 여 DetailsView 이벤트 처리기에 대 한 수정 내용을 확인 합니다.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample8.vb)]

다음 코드에 나와 있는 것 처럼 GridView s `RowUpdating` 및 `RowUpdated` 이벤트 처리기는 `ProcessBrochureUpload` 및 `DeleteRememberedBrochurePath` 메서드를 사용 합니다.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample9.vb)]

`RowUpdating` 이벤트 처리기는 일련의 조건문을 사용 하 여 `BrochureOptions` RadioButtonList s `SelectedValue` 속성 값을 기반으로 적절 한 작업을 수행 하는 방법을 확인 합니다.

이 코드를 사용 하면 범주를 편집 하 고 현재 브로슈어를 사용 하거나 브로슈어를 사용 하지 않거나 새 범주를 업로드할 수 있습니다. 계속 해 서 사용해 보세요. `RowUpdating` 및 `RowUpdated` 이벤트 처리기에 중단점을 설정 하 여 워크플로를 파악 합니다.

## <a name="step-7-uploading-a-new-picture"></a>7 단계: 새 그림 업로드

`Picture` ImageField s 편집 인터페이스는 `DataImageUrlField` 속성 값으로 채워진 textbox로 렌더링 됩니다. 편집 워크플로 중에 GridView는 매개 변수 이름에 ImageField s `DataImageUrlField` 속성 값을 입력 하 고 매개 변수 s 값을 편집 인터페이스의 텍스트 상자에 입력 하 여 매개 변수를 ObjectDataSource에 전달 합니다. 이 동작은 이미지를 파일 시스템에 파일로 저장 하 고 `DataImageUrlField`에 이미지의 전체 URL을 포함 하는 경우에 적합 합니다. 이러한 상황에서 편집 인터페이스는 사용자가 변경 하 고 데이터베이스에 다시 저장할 수 있는 텍스트 상자에 이미지 URL을 표시 합니다. 이 기본 인터페이스를 부여 하면 사용자가 새 이미지를 업로드할 수 없지만, 이미지의 URL을 현재 값에서 다른 값으로 변경할 수는 없습니다. 그러나이 자습서에서는 `Picture` 이진 데이터를 데이터베이스에 직접 저장 하 고 `DataImageUrlField` 속성에 `CategoryID`만 저장 되므로 ImageField s 기본 편집 인터페이스는 충분 하지 않습니다.

사용자가 ImageField를 사용 하 여 행을 편집할 때 자습서에서 수행 하는 작업을 더 잘 이해 하려면 다음 예제를 참조 하세요. 사용자가 10을 사용 하 `CategoryID` 여 행을 편집 하 여 `Picture` ImageField이 값 10을 사용 하는 textbox로 렌더링 되도록 합니다. 사용자가이 텍스트 상자의 값을 50로 변경 하 고 업데이트 단추를 클릭 한다고 가정 합니다. 포스트백이 발생 하 고 GridView는 처음에 값이 50 인 `CategoryID` 이라는 매개 변수를 만듭니다. 그러나 GridView가이 매개 변수와 `CategoryName` 및 `Description` 매개 변수)를 보내기 전에 `DataKeys` 컬렉션의 값에를 추가 합니다. 따라서 `CategoryID` 매개 변수를 현재 행의 기본 `CategoryID` 값 10으로 덮어씁니다. ImageField s 편집 인터페이스는 ImageField s `DataImageUrlField` 속성의 이름과 그리드 s `DataKey` 값이 동일 하기 때문에이 자습서의 편집 워크플로에는 영향을 주지 않습니다.

ImageField를 사용 하면 데이터베이스 데이터를 기반으로 이미지를 쉽게 표시할 수 있지만 편집 인터페이스에는 텍스트 상자를 제공 하지 않으려고 합니다. 대신 최종 사용자가 범주 그림을 변경 하는 데 사용할 수 있는 FileUpload 컨트롤을 제공 하려고 합니다. `BrochurePath` 값과 달리 이러한 자습서에서는 각 범주에 그림이 있어야 한다고 결정 했습니다. 따라서 사용자는 연결 된 그림이 없음을 나타낼 필요가 없습니다. 사용자는 새 그림을 업로드 하거나 현재 그림을 그대로 둘 수 있습니다.

ImageField s 편집 인터페이스를 사용자 지정 하려면 Templatefield로 변환로 변환 해야 합니다. GridView s 스마트 태그에서 열 편집 링크를 클릭 하 고 ImageField를 선택한 다음이 필드를 Templatefield로 변환로 변환 링크를 클릭 합니다.

![ImageField을 Templatefield로 변환로 변환](updating-and-deleting-existing-binary-data-vb/_static/image3.gif)

**그림 16**: ImageField을 templatefield로 변환로 변환

이러한 방식으로 ImageField를 Templatefield로 변환로 변환 하면 두 개의 템플릿이 있는 Templatefield로 변환 생성 됩니다. 다음 선언 구문에서 볼 수 있듯이 `ItemTemplate`에는 `ImageUrl` 속성이 ImageField s `DataImageUrlField` 및 `DataImageUrlFormatString` 속성을 기반으로 하는 데이터 바인딩 구문을 사용 하 여 할당 되는 이미지 웹 컨트롤이 포함 되어 있습니다. `EditItemTemplate`에는 `Text` 속성이 `DataImageUrlField` 속성에 지정 된 값에 바인딩되는 텍스트 상자가 포함 되어 있습니다.

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample10.aspx)]

FileUpload 컨트롤을 사용 하려면 `EditItemTemplate`를 업데이트 해야 합니다. GridView의 스마트 태그에서 템플릿 편집 링크를 클릭 한 다음 드롭다운 목록에서 `Picture` Templatefield로 변환 s `EditItemTemplate`를 선택 합니다. 템플릿에서이를 제거 하는 텍스트 상자가 표시 됩니다. 그런 다음 FileUpload 컨트롤을 도구 상자에서 템플릿으로 끌어 `ID`를 `PictureUpload`로 설정 합니다. 또한 범주 그림을 변경 하는 텍스트를 추가 하 고 새 그림을 지정 합니다. 범주를 동일 하 게 유지 하려면 필드를 서식 파일에도 비워 둡니다.

[FileUpload 컨트롤을 EditItemTemplate에 추가 ![](updating-and-deleting-existing-binary-data-vb/_static/image41.png)](updating-and-deleting-existing-binary-data-vb/_static/image40.png)

**그림 17**: `EditItemTemplate`에 FileUpload 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image42.png))

편집 인터페이스를 사용자 지정한 후 브라우저에서 진행 상황을 확인 합니다. 읽기 전용 모드에서 행을 볼 때는 이전 처럼 범주 이미지를 표시 하지만, 편집 단추를 클릭 하면 그림 열이 FileUpload 컨트롤을 사용 하는 텍스트로 렌더링 됩니다.

[![편집 인터페이스에 FileUpload 컨트롤이 포함 되어 있습니다.](updating-and-deleting-existing-binary-data-vb/_static/image44.png)](updating-and-deleting-existing-binary-data-vb/_static/image43.png)

**그림 18**: 편집 인터페이스에 FileUpload 컨트롤이 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](updating-and-deleting-existing-binary-data-vb/_static/image45.png)).

ObjectDataSource는 그림에 대 한 이진 데이터를 `Byte` 배열로 입력으로 허용 하는 `CategoriesBLL` 클래스 s `UpdateCategory` 메서드를 호출 하도록 구성 되어 있습니다. 그러나이 배열을 `Nothing`하는 경우 대체 `UpdateCategory` 오버 로드가 호출 되며,이를 통해 `Picture` 열을 수정 하지 않는 `UPDATE` SQL 문을 실행 하 여 범주를 현재 그림으로 그대로 둘 수 있습니다. 따라서 GridView s `RowUpdating` 이벤트 처리기에서 `PictureUpload` FileUpload 컨트롤을 프로그래밍 방식으로 참조 하 고 파일이 업로드 되었는지 확인 해야 합니다. 업로드 되지 않은 경우 `picture` 매개 변수에 대 한 값을 지정 *하지* 않도록 합니다. 반면에 파일이 `PictureUpload` FileUpload 컨트롤에 업로드 된 경우 JPG 파일 인지 확인 하려고 합니다. 인 경우 `picture` 매개 변수를 통해 ObjectDataSource로 이진 콘텐츠를 보낼 수 있습니다.

6 단계에서 사용 되는 코드와 마찬가지로 여기에 필요한 코드 대부분이 DetailsView s `ItemInserting` 이벤트 처리기에 이미 있습니다. 따라서 공용 기능을 새 메서드로 리팩터링하여 `ValidPictureUpload`하 고이 메서드를 사용 하도록 `ItemInserting` 이벤트 처리기를 업데이트 했습니다.

GridView s `RowUpdating` 이벤트 처리기의 시작 부분에 다음 코드를 추가 합니다. 잘못 된 그림 파일이 업로드 된 경우 브로슈어를 웹 서버 파일 시스템에 저장 하지 않기 때문에이 코드는 브로슈어 파일을 저장 하는 코드 앞에와 야 합니다.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample11.vb)]

`ValidPictureUpload(FileUpload)` 메서드는 FileUpload 컨트롤을 유일한 입력 매개 변수로 사용 하 고 업로드 된 파일의 확장명을 확인 하 여 업로드 된 파일이 JPG 인지 확인 합니다. 그림 파일이 업로드 된 경우에만 호출 됩니다. 파일이 업로드 되지 않으면 picture 매개 변수가 설정 되지 않으므로 `Nothing`의 기본값을 사용 합니다. 그림이 업로드 되 고 `ValidPictureUpload` `True`반환 되는 경우 `picture` 매개 변수에는 업로드 된 이미지의 이진 데이터가 할당 됩니다. 메서드가 `False`반환 하면 업데이트 워크플로가 취소 되 고 이벤트 처리기가 종료 됩니다.

DetailsView s `ItemInserting` 이벤트 처리기에서 리팩터링 된 `ValidPictureUpload(FileUpload)` 메서드 코드는 다음과 같습니다.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample12.vb)]

## <a name="step-8-replacing-the-original-categories-pictures-with-jpgs"></a>8 단계: 원래 범주 그림을 JPGs로 바꾸기

원래의 8 개 범주 그림은 OLE 헤더에 래핑된 비트맵 파일 임을 기억 하세요. 기존 레코드의 그림을 편집 하는 기능을 추가 했으므로 잠시 후에 이러한 비트맵을 JPGs으로 바꿉니다. 현재 범주 그림을 계속 사용 하려는 경우 다음 단계를 수행 하 여 JPGs으로 변환할 수 있습니다.

1. 하드 드라이브에 비트맵 이미지를 저장 합니다. 브라우저의 `UpdatingAndDeleting.aspx` 페이지를 방문 하 고 처음 8 개 범주 각각에 대해 이미지를 마우스 오른쪽 단추로 클릭 하 고 그림을 저장 하도록 선택 합니다.
2. 원하는 이미지 편집기에서 이미지를 엽니다. 예를 들어 Microsoft Paint를 사용할 수 있습니다.
3. 비트맵을 JPG 이미지로 저장 합니다.
4. JPG 파일을 사용 하 여 편집 인터페이스를 통해 범주 그림을 업데이트 합니다.

범주를 편집 하 고 JPG 이미지를 업로드 한 후에는 `DisplayCategoryPicture.aspx` 페이지가 처음 8 개 범주의 그림에서 처음 78 바이트를 제거 하기 때문에 이미지가 브라우저에서 렌더링 되지 않습니다. OLE 헤더 제거를 수행 하는 코드를 제거 하 여이 문제를 해결 합니다. 이 작업을 수행한 후 `DisplayCategoryPicture.aspx``Page_Load` 이벤트 처리기에는 다음 코드만 있어야 합니다.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample13.vb)]

> [!NOTE]
> `UpdatingAndDeleting.aspx` 페이지의 인터페이스 삽입 및 편집은 약간 더 많은 작업을 사용할 수 있습니다. DetailsView 및 GridView의 `CategoryName` 및 `Description` BoundFields는 템플릿 필드로 변환 되어야 합니다. `CategoryName`에서 `NULL` 값을 허용 하지 않으므로 RequiredFieldValidator를 추가 해야 합니다. `Description` TextBox는 여러 줄 텍스트 상자로 변환 될 수 있습니다. 이러한 마무리를 연습으로 유지 합니다.

## <a name="summary"></a>요약

이 자습서에서는 이진 데이터 작업을 완료 합니다. 이 자습서와 이전 세 가지에서는 이진 데이터를 파일 시스템에 저장 하거나 데이터베이스 내에 직접 저장 하는 방법을 살펴보았습니다. 사용자는 하드 드라이브에서 파일을 선택 하 고 웹 서버에 업로드 하 여 시스템에 이진 데이터를 제공 합니다 .이 파일을 파일 시스템에 저장 하거나 데이터베이스에 삽입할 수 있습니다. ASP.NET 2.0에는 이러한 인터페이스를 끌어서 놓기를 쉽게 제공할 수 있도록 하는 FileUpload 컨트롤이 포함 되어 있습니다. 그러나 [파일 업로드](uploading-files-vb.md) 자습서에 설명 된 대로 FileUpload 컨트롤은 비교적 작은 파일 업로드에만 적합 하며 메가바이트를 초과 하지 않는 것이 좋습니다. 또한 업로드 된 데이터를 기본 데이터 모델에 연결 하는 방법 뿐만 아니라 기존 레코드에서 이진 데이터를 편집 하 고 삭제 하는 방법도 살펴보았습니다.

다음 일련의 자습서에서는 다양 한 캐싱 기술을 살펴봅니다. 캐싱을 사용 하면 비용이 많이 드는 작업에서 결과를 가져와 보다 신속 하 게 액세스할 수 있는 위치에 저장 하 여 응용 프로그램의 전반적인 성능을 향상 시킬 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Teresa Murphy입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](including-a-file-upload-option-when-adding-a-new-record-vb.md)
