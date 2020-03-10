---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
title: 데이터 삽입, 업데이트 및 삭제에 대 한 개요 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 ObjectDataSource의 Insert (), Update () 및 Delete () 메서드를 BLL 클래스의 메서드에 매핑하는 방법 뿐만 아니라 configu ...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: b651dc58-93c7-4f83-a74e-3b99f6d60848
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
msc.type: authoredcontent
ms.openlocfilehash: e26b8e841f86272a158b0c09b62ab2790d01d191
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78479363"
---
# <a name="an-overview-of-inserting-updating-and-deleting-data-c"></a>데이터 삽입, 업데이트 및 삭제에 대 한 개요 (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_CS.exe) 또는 [PDF 다운로드](an-overview-of-inserting-updating-and-deleting-data-cs/_static/datatutorial16cs1.pdf)

> 이 자습서에서는 ObjectDataSource의 Insert (), Update () 및 Delete () 메서드를 BLL 클래스의 메서드에 매핑하는 방법 뿐만 아니라 GridView, DetailsView 및 FormView 컨트롤을 구성 하 여 데이터 수정 기능을 제공 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

지난 몇 가지 자습서에서 GridView, DetailsView 및 FormView 컨트롤을 사용 하 여 ASP.NET 페이지에 데이터를 표시 하는 방법을 살펴보았습니다. 이러한 컨트롤은 제공 된 데이터에 대해서만 작동 합니다. 일반적으로 이러한 컨트롤은 ObjectDataSource와 같은 데이터 소스 컨트롤을 사용 하 여 데이터에 액세스 합니다. ObjectDataSource가 ASP.NET 페이지와 기본 데이터 간의 프록시로 작동 하는 방법을 살펴보았습니다. GridView는 데이터를 표시 해야 하는 경우 해당 ObjectDataSource의 `Select()` 메서드를 호출 합니다 .이 메서드는 적절 한 DAL (데이터 액세스 계층) TableAdapter의 메서드를 호출 하는 BLL (비즈니스 논리 계층)에서 메서드를 호출 하 고이 메서드를 사용 하 여 `SELECT` 쿼리를 Northwind 데이터베이스로 보냅니다.

[첫 번째 자습서](../introduction/creating-a-data-access-layer-cs.md)의 DAL에서 tableadapter를 만들 때 Visual Studio는 기본 데이터베이스 테이블에서 데이터를 삽입, 업데이트 및 삭제 하는 메서드를 자동으로 추가 했습니다. 또한 [비즈니스 논리 계층을 만들](../introduction/creating-a-business-logic-layer-cs.md) 때 BLL에서 이러한 데이터 수정 DAL 메서드로 호출 된 메서드를 디자인 했습니다.

ObjectDataSource에는 `Select()` 메서드 외에도 `Insert()`, `Update()`및 `Delete()` 메서드가 있습니다. `Select()` 메서드와 마찬가지로이 세 가지 메서드는 기본 개체의 메서드에 매핑될 수 있습니다. 데이터를 삽입, 업데이트 또는 삭제 하도록 구성 된 경우 GridView, DetailsView 및 FormView 컨트롤은 기본 데이터를 수정 하기 위한 사용자 인터페이스를 제공 합니다. 이 사용자 인터페이스는 ObjectDataSource의 `Insert()`, `Update()`및 `Delete()` 메서드를 호출한 다음 기본 개체의 연결 된 메서드를 호출 합니다 (그림 1 참조).

[ObjectDataSource의 Insert (), Update () 및 Delete () 메서드 ![BLL에 프록시로 사용 됩니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image1.png)

**그림 1**: ObjectDataSource의 `Insert()`, `Update()`및 `Delete()` 메서드가 BLL ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image3.png))에 대 한 프록시 역할을 합니다.

이 자습서에서는 ObjectDataSource의 `Insert()`, `Update()`및 `Delete()` 메서드를 BLL 클래스의 메서드에 매핑하는 방법 뿐만 아니라 GridView, DetailsView 및 FormView 컨트롤을 구성 하 여 데이터 수정 기능을 제공 하는 방법을 알아봅니다.

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>1 단계: 삽입, 업데이트 및 삭제 자습서 웹 페이지 만들기

데이터를 삽입, 업데이트 및 삭제 하는 방법에 대 한 탐색을 시작 하기 전에 먼저 웹 사이트 프로젝트에서이 자습서에 필요한 ASP.NET 페이지와 그 다음 몇 가지 페이지를 만들어 보겠습니다. `EditInsertDelete`이라는 새 폴더를 추가 하 여 시작 합니다. 그런 다음, 다음 ASP.NET 페이지를 해당 폴더에 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![데이터 수정 관련 자습서에 대 한 ASP.NET 페이지 추가](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image4.png)

**그림 2**: 데이터 수정 관련 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `EditInsertDelete` 폴더의 `Default.aspx`에는 해당 섹션의 자습서가 나열 됩니다. `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 솔루션 탐색기에서 페이지의 디자인 뷰 끌어 `Default.aspx`에 추가 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image5.png)

**그림 3**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image7.png))

마지막으로 `Web.sitemap` 파일에 페이지를 항목으로 추가 합니다. 구체적으로, 사용자 지정 된 서식 `<siteMapNode>`뒤에 다음 태그를 추가 합니다.

[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample1.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에는 자습서 편집, 삽입 및 삭제를 위한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 자습서 편집, 삽입 및 삭제에 대 한 항목이 포함 됩니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image8.png)

**그림 4**: 이제 사이트 맵에 편집, 삽입 및 삭제 자습서에 대 한 항목이 포함 되어 있습니다.

## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>2 단계: ObjectDataSource 컨트롤 추가 및 구성

GridView, DetailsView 및 FormView는 각각 데이터 수정 기능과 레이아웃에 따라 다르므로 각각을 하나씩 살펴보겠습니다. 그러나 각 컨트롤에 자체 ObjectDataSource를 사용 하는 대신 세 개의 컨트롤 예제 모두에서 공유할 수 있는 단일 ObjectDataSource만 만들면 됩니다.

`Basics.aspx` 페이지를 열고, 도구 상자에서 ObjectDataSource를 디자이너로 끌고, 스마트 태그에서 데이터 소스 구성 링크를 클릭 합니다. `ProductsBLL`는 편집, 삽입 및 삭제 메서드를 제공 하는 유일한 BLL 클래스 이므로이 클래스를 사용 하도록 ObjectDataSource를 구성 합니다.

[ProductsBLL 클래스를 사용 하도록 ObjectDataSource 구성 ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image9.png)

**그림 5**: `ProductsBLL` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image11.png))

다음 화면에서 적절 한 탭을 선택 하 고 드롭다운 목록에서 메서드를 선택 하 여 ObjectDataSource의 `Select()`, `Insert()`, `Update()`및 `Delete()`에 매핑되는 `ProductsBLL` 클래스의 메서드를 지정할 수 있습니다. 그림 6은 이제 알아 두어야 하 고 ObjectDataSource의 `Select()` 메서드를 `ProductsBLL` 클래스의 `GetProducts()` 메서드에 매핑합니다. 목록에서 맨 위를 따라 적절 한 탭을 선택 하 여 `Insert()`, `Update()`및 `Delete()` 메서드를 구성할 수 있습니다.

[ObjectDataSource에서 모든 제품을 반환 ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image12.png)

**그림 6**: ObjectDataSource가 모든 제품을 반환 하도록 합니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image14.png)).

그림 7, 8 및 9에는 ObjectDataSource의 업데이트, 삽입 및 삭제 탭이 표시 됩니다. `Insert()`, `Update()`및 `Delete()` 메서드가 `ProductsBLL` 클래스의 `UpdateProduct`, `AddProduct`및 `DeleteProduct` 메서드를 각각 호출 하도록 이러한 탭을 구성 합니다.

[ObjectDataSource의 Update () 메서드를 Product Bll 클래스의 UpdateProduct 메서드에 ![매핑합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image15.png)

**그림 7**: ObjectDataSource의 `Update()` 메서드를 `ProductBLL` 클래스의 `UpdateProduct` 메서드에 매핑 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image17.png))

[ObjectDataSource의 Insert () 메서드를 Product Bll 클래스의 AddProduct 메서드에 ![매핑합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image18.png)

**그림 8**: ObjectDataSource의 `Insert()` 메서드를 `ProductBLL` 클래스의 Add `Product` 메서드에 매핑 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image20.png))

[ObjectDataSource의 Delete () 메서드를 Product Bll 클래스의 DeleteProduct 메서드에 매핑합니다 ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image21.png)

**그림 9**: ObjectDataSource의 `Delete()` 메서드를 `ProductBLL` 클래스의 `DeleteProduct` 메서드에 매핑 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image23.png))

업데이트, 삽입 및 삭제 탭의 드롭다운 목록에 이러한 메서드가 이미 선택 되어 있는 것을 알 수 있습니다. 이는 `ProductsBLL`의 메서드를 데코레이팅하는 `DataObjectMethodAttribute`을 사용 하기 위한 것입니다. 예를 들어 DeleteProduct 메서드의 시그니처는 다음과 같습니다.

[!code-csharp[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample2.cs)]

`DataObjectMethodAttribute` 특성은 선택, 삽입, 업데이트 또는 삭제에 대 한 각 방법의 용도와 기본값 인지 여부를 나타냅니다. BLL 클래스를 만들 때 이러한 특성을 생략 한 경우 업데이트, 삽입 및 삭제 탭에서 수동으로 메서드를 선택 해야 합니다.

적절 한 `ProductsBLL` 메서드가 ObjectDataSource의 `Insert()`, `Update()`및 `Delete()` 메서드에 매핑되는지 확인 한 후 마침을 클릭 하 여 마법사를 완료 합니다.

## <a name="examining-the-objectdatasources-markup"></a>ObjectDataSource의 태그 검사

마법사를 통해 ObjectDataSource를 구성한 후 원본 뷰로 이동 하 여 생성 된 선언적 태그를 검사 합니다. `<asp:ObjectDataSource>` 태그는 내부 개체와 호출할 메서드를 지정 합니다. 또한 `ProductsBLL` 클래스의 `AddProduct`, `UpdateProduct`및 `DeleteProduct` 메서드에 대 한 입력 매개 변수에 매핑되는 `DeleteParameters`, `UpdateParameters`및 `InsertParameters` 있습니다.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample3.aspx)]

ObjectDataSource에는 연결 된 메서드에 대 한 각 입력 매개 변수에 대 한 매개 변수가 포함 되어 있습니다 .이 목록에는 `GetProductsByCategoryID(categoryID)`와 같이 입력 매개 변수를 필요로 하는 select 메서드를 호출 하도록 ObjectDataSource가 구성 된 경우와 마찬가지로 `SelectParameter`의 목록이 표시 됩니다. 곧 볼 수 있듯이 이러한 `DeleteParameters`, `UpdateParameters`및 `InsertParameters`에 대 한 값은 ObjectDataSource의 `Insert()`, `Update()`또는 `Delete()` 메서드를 호출 하기 전에 GridView, DetailsView 및 FormView에서 자동으로 설정 됩니다. 이후 자습서에서 설명 하는 대로 필요에 따라 이러한 값을 프로그래밍 방식으로 설정할 수도 있습니다.

마법사를 사용 하 여 ObjectDataSource로 구성 하는 한 가지 부작용은 Visual Studio가 [Oldvaluesparameterformatstring 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx) 을 `original_{0}`로 설정 한다는 것입니다. 이 속성 값은 편집 중인 데이터의 원래 값을 포함 하는 데 사용 되며 다음과 같은 두 가지 시나리오에서 유용 합니다.

- 이면 레코드를 편집할 때 사용자가 기본 키 값을 변경할 수 있습니다. 이 경우 원래 기본 키 값이 있는 레코드를 찾아 해당 값을 적절 하 게 업데이트 하려면 새 기본 키 값과 원래 기본 키 값을 모두 제공 해야 합니다.
- 낙관적 동시성을 사용 하는 경우. 낙관적 동시성은 두 명의 동시 사용자가 다른 사용자의 변경 내용을 덮어쓰지 않도록 하는 기술 이며 이후 자습서에 대 한 항목입니다.

`OldValuesParameterFormatString` 속성은 원래 값에 대 한 기본 개체의 update 및 delete 메서드에서 입력 매개 변수의 이름을 나타냅니다. 낙관적 동시성을 탐색 하는 경우이 속성과 용도에 대해 더 자세히 설명 합니다. 그러나 현재 BLL의 메서드에 원래 값이 필요 하지 않으므로이 속성을 제거 하는 것이 중요 합니다. `OldValuesParameterFormatString` 속성을 기본값 (`{0}`) 이외의 값으로 설정 하면 ObjectDataSource가 지정 된 `UpdateParameters` 또는 `DeleteParameters`를 원래 값 매개 변수로 전달 하려고 하므로 데이터 웹 컨트롤에서 ObjectDataSource의 `Update()` 또는 `Delete()` 메서드를 호출 하려고 하면 오류가 발생 합니다.

이 분기 시점에 대해 그다지 명확 하지 않은 경우에는이 속성 및 해당 유틸리티를 나중에 살펴보겠습니다. 지금은 선언적 구문에서이 속성 선언을 완전히 제거 하거나 값을 기본값 ({0})으로 설정 해야 합니다.

> [!NOTE]
> 디자인 뷰의 속성 창에서 `OldValuesParameterFormatString` 속성 값을 제거 하는 경우에도 해당 속성은 선언적 구문에 있지만 빈 문자열로 설정 됩니다. 그러나이 경우에도 위에서 설명한 것과 동일한 문제가 발생 합니다. 따라서 선언적 구문에서 속성을 완전히 제거 하거나 속성 창에서 값을 기본값인 `{0}`로 설정 합니다.

## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>3 단계: 데이터 웹 컨트롤을 추가 하 고 데이터를 수정 하기 위해 구성

ObjectDataSource가 페이지에 추가 되 고 구성 되 면 데이터 웹 컨트롤을 페이지에 추가 하 여 데이터를 표시 하 고 최종 사용자가 수정할 수 있는 수단을 제공할 준비가 된 것입니다. 이러한 데이터 웹 컨트롤은 데이터 수정 기능 및 구성 마다 다르므로 GridView, DetailsView 및 FormView를 별도로 살펴보겠습니다.

이 문서의 나머지 부분에서 볼 수 있듯이, GridView, DetailsView 및 FormView 컨트롤을 통한 매우 기본적인 편집, 삽입 및 삭제 지원을 추가 하는 것은 사실 몇 가지 확인란을 선택 하는 것 만큼 간단 합니다. 실제 세계에는 단지 point와 클릭 보다 이러한 기능을 더 많이 제공 하는 많은 세부 사항 및에 지 사례가 있습니다. 그러나이 자습서는 단순한 데이터 수정 기능을 입증 하는 데만 초점을 맞춘 것입니다. 이후 자습서에서는 실제 설정에서 문제가 발생 하는 문제를 조사 합니다.

## <a name="deleting-data-from-the-gridview"></a>GridView에서 데이터 삭제

먼저 도구 상자에서 디자이너로 GridView를 끌어 옵니다. 그런 다음 GridView의 스마트 태그에 있는 드롭다운 목록에서 선택 하 여 ObjectDataSource를 GridView에 바인딩합니다. 이 시점에서 GridView의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample4.aspx)]

해당 스마트 태그를 통해 ObjectDataSource에 GridView를 바인딩하면 다음과 같은 두 가지 이점이 있습니다.

- ObjectDataSource에서 반환 하는 각 필드에 대해 BoundFields 및 CheckBoxFields가 자동으로 만들어집니다. 또한 BoundField 및 CheckBoxField의 속성은 기본 필드의 메타 데이터를 기반으로 설정 됩니다. 예를 들어 `ProductID`, `CategoryName`및 `SupplierName` 필드는 `ProductsDataTable`에서 읽기 전용으로 표시 되므로 편집할 때 업데이트할 수 없습니다. 이를 수용 하기 위해 이러한 BoundFields의 [ReadOnly 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx) 은 `true`로 설정 됩니다.
- [DataKeyNames 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx) 은 기본 개체의 기본 키 필드에 할당 됩니다. 이 속성은 데이터를 편집 하거나 삭제 하는 데 GridView를 사용할 때 반드시 필요 합니다 .이 속성은 각 레코드를 고유 하 게 식별 하는 필드 또는 필드 집합을 나타냅니다. `DataKeyNames` 속성에 대 한 자세한 내용은 [세부 정보 DetailView 자습서에서 선택 가능한 마스터 GridView를 사용 하 여 마스터/세부](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 정보를 다시 참조 하세요.

GridView를 속성 창 또는 선언 구문을 통해 ObjectDataSource에 바인딩할 수 있지만 이렇게 하려면 적절 한 BoundField 및 `DataKeyNames` 태그를 수동으로 추가 해야 합니다.

GridView 컨트롤은 행 수준 편집 및 삭제에 대 한 기본 제공 지원을 제공 합니다. 삭제를 지원 하도록 GridView를 구성 하면 삭제 단추의 열이 추가 됩니다. 최종 사용자가 특정 행에 대 한 삭제 단추를 클릭 하면 다시 게시 ensues 및 GridView가 다음 단계를 수행 합니다.

1. ObjectDataSource의 `DeleteParameters` 값이 할당 됩니다.
2. ObjectDataSource의 `Delete()` 메서드가 호출 되 고 지정 된 레코드를 삭제 합니다.
3. GridView는 `Select()` 메서드를 호출 하 여 ObjectDataSource에 다시 바인딩합니다.

`DeleteParameters`에 할당 되는 값은 삭제 단추를 클릭 한 행에 대 한 `DataKeyNames` 필드의 값입니다. 따라서 GridView의 `DataKeyNames` 속성을 올바르게 설정 하는 것이 중요 합니다. 누락 된 경우 1 단계에서 `DeleteParameters`에 `null` 값이 할당 됩니다. 그러면 2 단계에서 삭제 된 레코드가 반환 되지 않습니다.

> [!NOTE]
> `DataKeys` 컬렉션은 gridview의 컨트롤 상태에 저장 됩니다. 즉, GridView의 뷰 상태가 사용 하지 않도록 설정 된 경우에도 `DataKeys` 값이 포스트백을 통해 기억 됩니다. 그러나 편집 또는 삭제 (기본 동작)를 지 원하는 GridViews에 대해 뷰 상태를 설정 된 상태로 유지 하는 것은 매우 중요 합니다. GridView s `EnableViewState` 속성을 `false`로 설정 하면 편집 및 삭제 동작이 단일 사용자에 대해 제대로 작동 하지만 데이터를 동시에 삭제 하는 동시 사용자가 의도 하지 않은 레코드를 실수로 삭제 하거나 편집할 가능성이 있습니다. 자세한 내용은 내 블로그 항목, [경고: 편집 및/또는 삭제를 지원 하 고 보기 상태를 사용 하지 않도록 설정 된 ASP.NET 2.0 gridviews/DetailsView/FormViews의 동시성 문제](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx)를 참조 하세요.

이 경고는 DetailsViews 및 FormViews에도 적용 됩니다.

GridView에 삭제 기능을 추가 하려면 해당 스마트 태그로 이동 하 여 삭제 사용 확인란을 선택 하면 됩니다.

![삭제 사용 확인란을 선택 합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image24.png)

**그림 10**: 삭제 사용 확인란 선택

스마트 태그에서 삭제 사용 확인란을 선택 하면 CommandField가 GridView에 추가 됩니다. CommandField는 레코드 선택, 레코드 편집 및 레코드 삭제 작업 중 하나 이상을 수행 하는 단추를 사용 하 여 GridView의 열을 렌더링 합니다. 이전에는 [세부 정보 DetailView 자습서와 함께 선택 가능한 마스터 GridView를 사용 하 여 마스터/세부](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) 정보에서 레코드를 선택 하는 동작의 commandfield를 살펴보았습니다.

CommandField에는 CommandField에 표시 되는 일련의 단추를 나타내는 다양 한 `ShowXButton` 속성이 포함 되어 있습니다. 삭제 사용 확인란을 선택 하 여 `ShowDeleteButton` 속성이 `true` 인 CommandField를 GridView의 Columns 컬렉션에 추가 했습니다.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample5.aspx)]

이 시점에서 GridView에 지원 삭제를 추가 하는 작업이 완료 되었습니다. 그림 11에 나와 있는 것 처럼 브라우저를 통해이 페이지를 방문 하는 경우 삭제 단추 열이 있습니다.

[CommandField ![삭제 단추의 열을 추가 합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image25.png)

**그림 11**: Commandfield는 Delete 단추의 열을 추가 합니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image27.png)).

처음부터 직접이 자습서를 작성 한 경우에는이 페이지를 테스트할 때 삭제 단추를 클릭 하면 예외가 발생 합니다. 이러한 예외가 발생 한 이유와 해결 방법에 대 한 자세한 내용은 계속 읽어 보세요.

> [!NOTE]
> 이 자습서와 함께 제공 된 다운로드를 사용 하 여 수행 하는 경우에는 이러한 문제가 이미 고려 되었습니다. 그러나 발생할 수 있는 문제를 식별 하 고 적절 한 해결 방법을 확인 하려면 아래에 나열 된 세부 정보를 읽어보시기 바랍니다.

제품을 삭제 하려고 할 때 "*objectdatasource ' ObjectDataSource1 ' 매개 변수를 포함 하는 제네릭이 아닌 ' DeleteProduct ' 메서드를 찾을 수 없습니다 (productid, original\_productid*,"). objectdatasource에서 `OldValuesParameterFormatString` 속성을 제거 하지 않을 수 있습니다. 지정 된 `OldValuesParameterFormatString` 속성을 사용 하 여 ObjectDataSource는 `productID` 및 `original_ProductID` 입력 매개 변수를 `DeleteProduct` 메서드에 전달 하려고 시도 합니다. 그러나 `DeleteProduct`는 단일 입력 매개 변수만 허용 하므로 예외입니다. `OldValuesParameterFormatString` 속성을 제거 하거나 `{0}`로 설정 하면 ObjectDataSource에서 원래 입력 매개 변수를 전달 하려고 시도 하지 않습니다.

[OldValuesParameterFormatString 속성이 제거 되었는지 확인 ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image28.png)

**그림 12**: `OldValuesParameterFormatString` 속성의 선택이 취소 되었는지 확인 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image30.png))

`OldValuesParameterFormatString` 속성을 제거한 경우에도 "*delete 문이 참조 제약 조건과 충돌 합니다. ' FK\_Order\_Details\_Products '와 충돌*합니다." 라는 메시지가 포함 된 제품을 삭제 하려고 할 때 예외가 발생 합니다. Northwind 데이터베이스에는 `Order Details` 테이블과 `Products` 테이블 간의 foreign key 제약 조건이 포함 되어 있습니다. 즉, `Order Details` 테이블에 하나 이상의 레코드가 있는 경우 시스템에서 제품을 삭제할 수 없습니다. Northwind 데이터베이스의 모든 제품은 `Order Details`에 하나 이상의 레코드를 포함 하므로 먼저 제품의 연결 된 주문 정보 레코드를 삭제할 때까지 제품을 삭제할 수 없습니다.

[Foreign Key 제약 조건을 ![제품 삭제 금지](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image31.png)

**그림 13**: Foreign Key 제약 조건에서 제품 삭제를 금지 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image33.png))

이 자습서에서는 `Order Details` 테이블의 모든 레코드를 삭제 해 보겠습니다. 실제 응용 프로그램에서 다음 중 하나를 수행 해야 합니다.

- 주문 세부 정보를 관리 하는 다른 화면이 있습니다.
- 지정 된 제품의 주문 정보를 삭제 하는 논리를 포함 하도록 `DeleteProduct` 메서드를 확대 합니다.
- 지정 된 제품의 주문 정보 삭제를 포함 하기 위해 TableAdapter에서 사용 하는 SQL 쿼리를 수정 합니다.

Foreign key 제약 조건을 회피 하기 위해 `Order Details` 테이블에서 모든 레코드를 삭제 하겠습니다. Visual Studio에서 서버 탐색기로 이동 하 여 `NORTHWND.MDF` 노드를 마우스 오른쪽 단추로 클릭 하 고 새 쿼리를 선택 합니다. 그런 다음 쿼리 창에서 다음 SQL 문을 실행 합니다. `DELETE FROM [Order Details]`

[Order Details 테이블의 모든 레코드를 삭제 ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image34.png)

**그림 14**: `Order Details` 테이블에서 모든 레코드 삭제 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image36.png))

`Order Details` 테이블을 지운 후 삭제 단추를 클릭 하면 오류가 발생 하지 않고 제품이 삭제 됩니다. 삭제 단추를 클릭 해도 제품이 삭제 되지 않는 경우 GridView의 `DataKeyNames` 속성이 기본 키 필드 (`ProductID`)로 설정 되어 있는지 확인 합니다.

> [!NOTE]
> 삭제 단추를 클릭 하면 포스트백이 ensues 레코드는 삭제 됩니다. 실수로 잘못 된 행의 삭제 단추를 클릭할 수 있으므로이는 위험할 수 있습니다. 이후 자습서에서는 레코드를 삭제할 때 클라이언트 쪽 확인을 추가 하는 방법을 알아봅니다.

## <a name="editing-data-with-the-gridview"></a>GridView를 사용 하 여 데이터 편집

또한 삭제와 더불어 GridView 컨트롤은 기본 제공 행 수준 편집 지원도 제공 합니다. 편집을 지원 하도록 GridView를 구성 하면 편집 단추의 열이 추가 됩니다. 최종 사용자의 관점에서 행의 편집 단추를 클릭 하면 해당 행이 편집 가능 하 고, 기존 값을 포함 하는 입력란으로 셀을 바꾸고, 편집 단추를 업데이트 및 취소 단추로 바꿀 수 있습니다. 원하는 변경을 수행한 후 최종 사용자는 업데이트 단추를 클릭 하 여 변경 내용을 커밋하거나 취소 단추를 클릭 하 여 해당 변경 내용을 취소할 수 있습니다. 두 경우 모두 업데이트 또는 취소를 클릭 하면 GridView가 사전 편집 상태로 돌아갑니다.

페이지 개발자의 관점에서 최종 사용자가 특정 행에 대 한 편집 단추를 클릭 하면 다시 게시 ensues 및 GridView는 다음 단계를 수행 합니다.

1. GridView의 `EditItemIndex` 속성이 편집 단추를 클릭 한 행의 인덱스에 할당 됩니다.
2. GridView는 `Select()` 메서드를 호출 하 여 ObjectDataSource에 다시 바인딩합니다.
3. `EditItemIndex` 일치 하는 행 인덱스는 "편집 모드"로 렌더링 됩니다. 이 모드에서 편집 단추는 업데이트 및 취소 단추로 바뀌고 `ReadOnly` 속성이 False (기본값) 인 BoundFields는 `Text` 속성이 데이터 필드 값에 할당 된 TextBox 웹 컨트롤로 렌더링 됩니다.

이 시점에서 태그는 브라우저에 반환 되어 최종 사용자가 행의 데이터를 변경할 수 있도록 합니다. 사용자가 업데이트 단추를 클릭 하면 다시 게시가 발생 하 고 GridView에서 다음 단계를 수행 합니다.

1. ObjectDataSource의 `UpdateParameters` 값에는 최종 사용자가 입력 한 값이 GridView의 편집 인터페이스에 할당 됩니다.
2. ObjectDataSource의 `Update()` 메서드가 호출 되어 지정 된 레코드를 업데이트 합니다.
3. GridView는 `Select()` 메서드를 호출 하 여 ObjectDataSource에 다시 바인딩합니다.

1 단계에서 `UpdateParameters`에 할당 된 기본 키 값은 `DataKeyNames` 속성에 지정 된 값에서 가져오며, 기본 키가 아닌 값은 편집 된 행에 대 한 TextBox 웹 컨트롤의 텍스트에서 제공 됩니다. 삭제와 마찬가지로 GridView의 `DataKeyNames` 속성을 올바르게 설정 하는 것이 중요 합니다. 누락 된 경우 `UpdateParameters` 기본 키 값에 1 단계에서 `null` 값이 할당 됩니다. 그러면 2 단계에서 업데이트 된 레코드를 발생 시 키 지 않습니다.

GridView의 스마트 태그에서 편집 사용 확인란을 선택 하면 편집 기능을 활성화할 수 있습니다.

![편집 사용 확인란을 선택 합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image37.png)

**그림 15**: 편집 사용 확인란 선택

편집 사용 확인란을 선택 하면 CommandField (필요한 경우)가 추가 되 고 `ShowEditButton` 속성이 `true`로 설정 됩니다. 앞서 살펴본 것 처럼 CommandField에는 CommandField에 표시 되는 일련의 단추를 나타내는 다양 한 `ShowXButton` 속성이 포함 되어 있습니다. 편집 사용 확인란을 선택 하면 `ShowEditButton` 속성이 기존 CommandField에 추가 됩니다.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample6.aspx)]

기초적인 편집 지원을 추가 하는 것이 전부입니다. Figure16에 표시 된 것 처럼 편집 인터페이스는 `ReadOnly` 속성이 `false` (기본값)로 설정 되어 있는 각 BoundField를 조잡 합니다. 여기에는 다른 테이블에 대 한 키인 `CategoryID` 및 `SupplierID`같은 필드가 포함 됩니다.

[Chai s 편집 단추를 클릭 하면 행이 편집 모드에서 표시 됩니다. ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image38.png)

**그림 16**: Chai s 편집 단추를 클릭 하면 행이 편집 모드로 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image40.png)).

사용자가 외래 키 값을 직접 편집 하도록 요청 하는 것 외에도, 편집 인터페이스의 인터페이스는 다음과 같은 측면에서 부족 합니다.

- 사용자가 데이터베이스에 없는 `CategoryID` 또는 `SupplierID` 입력 하면 `UPDATE` 외래 키 제약 조건을 위반 하 여 예외가 발생 됩니다.
- 편집 인터페이스에는 유효성 검사가 포함 되지 않습니다. 필요한 값 (예: `ProductName`)을 제공 하지 않거나 숫자 값이 필요한 문자열 값을 입력 합니다 (예: "너무 많이 입력!"). `UnitPrice` 텍스트 상자)에서 예외가 throw 됩니다. 이후 자습서에서는 편집 사용자 인터페이스에 유효성 검사 컨트롤을 추가 하는 방법을 살펴봅니다.
- 현재 읽기 전용이 아닌 *모든* 제품 필드는 GridView에 포함 되어야 합니다. GridView에서 필드를 제거 하는 경우 `UnitPrice`, 예를 들어, 데이터를 업데이트 하는 경우 GridView에서 `UnitPrice` `UpdateParameters` 값을 설정 하지 않으므로 데이터베이스 레코드의 `UnitPrice` `NULL` 값으로 변경 됩니다. 마찬가지로, `ProductName`와 같은 필수 필드가 GridView에서 제거 되는 경우 "*열 ' ProductName '* 은 위에서 언급 한 null을 허용 하지 않습니다." 라는 예외를 사용 하 여 업데이트가 실패 합니다.
- 편집 인터페이스 서식 지정은 원하는 대로 유지 됩니다. `UnitPrice`는 네 개의 소수점 점으로 표시 됩니다. 이상적으로 `CategoryID` 및 `SupplierID` 값에는 시스템의 범주와 공급자를 나열 하는 Dropdownlist 포함 되어 있습니다.

이는 현재와 함께 사용 해야 하는 모든 단점 이지만 이후 자습서에서 해결 될 예정입니다.

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>DetailsView을 사용 하 여 데이터 삽입, 편집 및 삭제

이전 자습서에서 살펴본 것 처럼 DetailsView 컨트롤은 한 번에 하나의 레코드를 표시 하 고 GridView와 같이 현재 표시 된 레코드를 편집 하 고 삭제할 수 있습니다. DetailsView에서 항목을 편집 하 고 삭제 하는 최종 사용자 경험과 ASP.NET 쪽의 워크플로는 모두 GridView와 동일 합니다. 이때 DetailsView은 GridView와는 달리 기본 제공 삽입 지원도 제공 합니다.

GridView의 데이터 수정 기능을 보여 주려면 먼저 기존 GridView 위의 `Basics.aspx` 페이지에 DetailsView을 추가 하 고 DetailsView의 스마트 태그를 통해 기존 ObjectDataSource에 바인딩합니다. 그런 다음 DetailsView의 `Height` 및 `Width` 속성을 지우고, 스마트 태그에서 페이징 사용 옵션을 선택 합니다. 편집, 삽입 및 삭제 지원을 사용 하려면 스마트 태그에서 편집 사용, 삽입 사용 및 삭제 확인란을 선택 하면 됩니다.

![편집, 삽입 및 삭제를 지원 하도록 DetailsView 구성](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image41.png)

**그림 17**: 편집, 삽입 및 삭제를 지원 하도록 DetailsView 구성

GridView와 마찬가지로 편집, 삽입 또는 삭제 지원을 추가 하면 다음 선언적 구문에서 볼 수 있는 것 처럼 DetailsView에 CommandField가 추가 됩니다.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample7.aspx)]

DetailsView의 경우 CommandField는 기본적으로 Columns 컬렉션의 끝에 표시 됩니다. DetailsView의 필드는 행으로 렌더링 되므로 CommandField는 DetailsView의 아래쪽에 삽입, 편집 및 삭제 단추가 포함 된 행으로 표시 됩니다.

[편집, 삽입 및 삭제를 지원 하도록 DetailsView 구성 ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image42.png)

**그림 18**: 편집, 삽입 및 삭제를 지원 하도록 DetailsView 구성 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image44.png))

삭제 단추를 클릭 하면 GridView와 동일한 이벤트 시퀀스를 시작 합니다. 다시 게시 합니다. 그런 다음 `DataKeyNames` 값을 기준으로 ObjectDataSource의 `DeleteParameters`를 채우는 DetailsView 및는 해당 ObjectDataSource의 `Delete()` 메서드를 호출 합니다 .이 메서드는 실제로 데이터베이스에서 제품을 제거 합니다. 또한 DetailsView의 편집은 GridView와 동일한 방식으로 작동 합니다.

삽입을 위해 최종 사용자에 게 클릭 하면 DetailsView을 "삽입 모드"로 렌더링 하는 새 단추가 표시 됩니다. "삽입 모드"를 사용 하면 새 단추가 삽입 및 취소 단추로 바뀌고 `InsertVisible` 속성이 `true` (기본값)로 설정 되어 있는 BoundFields 표시 됩니다. `ProductID`와 같이 자동 증분 필드로 식별 되는 이러한 데이터 필드에는 스마트 태그를 통해 DetailsView를 데이터 소스에 바인딩할 때 [Insertvisible 속성이](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx) `false`로 설정 됩니다.

스마트 태그를 통해 DetailsView에 데이터 소스를 바인딩하는 경우 Visual Studio는 자동 증분 필드에 대해서만 `false` `InsertVisible` 속성을 설정 합니다. `CategoryName` 및 `SupplierName`와 같은 읽기 전용 필드는 `InsertVisible` 속성이 명시적으로 `false`로 설정 되지 않는 한 "삽입 모드" 사용자 인터페이스에 표시 됩니다. 잠시 후에이 두 필드의 `InsertVisible` 속성을 DetailsView의 선언 구문이 나 스마트 태그의 편집 필드 링크를 통해 `false`로 설정 합니다. 그림 19에서는 필드 편집 링크를 클릭 하 여 `false` `InsertVisible` 속성을 설정 하는 방법을 보여 줍니다.

[![Northwind Traders는 이제 Acme Tea을 제공 합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image45.png)

**그림 19**: 이제 Tea ([전체 크기 이미지를 보려면 클릭)를 제공 하](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image47.png)는 Northwind Traders에서 Acme를 제공 합니다.

`InsertVisible` 속성을 설정한 후 브라우저에서 `Basics.aspx` 페이지를 보고 새로 만들기 단추를 클릭 합니다. 그림 20은 제품 라인에 새 음료, Acme Tea를 추가 하는 경우 DetailsView을 보여 줍니다.

[![Northwind Traders는 이제 Acme Tea을 제공 합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image48.png)

**그림 20**: 이제는 이제 Acme Tea ([전체 크기 이미지를 보려면 클릭)를 제공 합니다](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image50.png).

Acme Tea에 대 한 세부 정보를 입력 하 고 삽입 단추를 클릭 하면 다시 게시 ensues 및 새 레코드가 `Products` 데이터베이스 테이블에 추가 됩니다. 이 DetailsView은 데이터베이스 테이블에 있는 제품을 순서 대로 나열 하므로 새 제품을 확인 하기 위해 마지막 제품으로 페이지를 표시 해야 합니다.

[Acme Tea에 대 한 ![세부 정보](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image51.png)

**그림 21**: Acme Tea에 대 한 세부 정보 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image53.png))

> [!NOTE]
> DetailsView의 [Currentmode 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx) 은 표시 되는 인터페이스를 나타내며 `Edit`, `Insert`또는 `ReadOnly`값 중 하나일 수 있습니다. [Defaultmode 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx) 은 편집 또는 삽입이 완료 된 후 detailsview에서 반환 하는 모드를 나타내며, 편집 또는 삽입 모드에서 영구적으로 detailsview을 표시 하는 데 유용 합니다.

DetailsView의 삽입 및 편집 기능을 가리키고 클릭 하면 GridView와 동일한 제한 사항이 적용 됩니다. 사용자는 텍스트 상자를 통해 기존 `CategoryID`를 입력 하 고 값을 `SupplierID` 해야 합니다. 인터페이스에 유효성 검사 논리가 부족 합니다. `NULL` 값을 허용 하지 않거나 데이터베이스 수준에서 기본값이 지정 되지 않은 모든 product 필드는 삽입 인터페이스 등에 포함 되어야 합니다.

이후 문서에서 GridView의 편집 인터페이스를 확장 하 고 개선 하기 위해 검토할 기술은 DetailsView 컨트롤의 편집 및 삽입 인터페이스에도 적용 될 수 있습니다.

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>보다 유연한 데이터 수정 사용자 인터페이스에 대해 FormView 사용

FormView는 데이터 삽입, 편집 및 삭제에 대 한 기본 제공 지원을 제공 하지만 필드 대신 템플릿을 사용 하기 때문에 GridView 및 DetailsView 컨트롤에서 데이터를 제공 하는 데 사용 하는 BoundFields 또는 CommandField를 추가할 장소가 없습니다. 수정 인터페이스입니다. 대신이 인터페이스는 새 항목을 추가 하거나 새로 만들기, 편집, 삭제, 삽입, 업데이트 및 취소 단추와 함께 기존 항목을 편집할 때 사용자 입력을 수집 하는 웹 컨트롤을 적절 한 템플릿에 수동으로 추가 해야 합니다. 다행히 Visual Studio는 해당 스마트 태그의 드롭다운 목록을 통해 FormView를 데이터 소스에 바인딩할 때 필요한 인터페이스를 자동으로 만듭니다.

이러한 기술을 설명 하려면 먼저 `Basics.aspx` 페이지에 FormView를 추가 하 고 FormView의 스마트 태그에서 이미 만든 ObjectDataSource에 바인딩합니다. 이렇게 하면 새로 만들기, 편집, 삭제, 삽입, 업데이트 및 취소 단추에 대 한 사용자의 입력 및 단추 웹 컨트롤을 수집 하기 위해 TextBox 웹 컨트롤을 사용 하 여 FormView에 대 한 `EditItemTemplate`, `InsertItemTemplate`및 `ItemTemplate` 생성 됩니다. 또한 FormView의 `DataKeyNames` 속성은 ObjectDataSource에서 반환 하는 개체의 기본 키 필드 (`ProductID`)로 설정 됩니다. 마지막으로 FormView의 스마트 태그에서 페이징 사용 옵션을 선택 합니다.

다음은 FormView를 ObjectDataSource에 바인딩한 후 FormView의 `ItemTemplate`에 대 한 선언적 태그를 보여 줍니다. 기본적으로 각 부울 값 필드 (`Discontinued`)는 사용 하지 않도록 설정 된 CheckBox 웹 컨트롤의 `Checked` 속성에 바인딩되기 때문에 각 부울 값이 아닌 product 필드는 Label 웹 컨트롤의 `Text` 속성에 바인딩됩니다. 클릭 하면 새, 편집 및 삭제 단추가 특정 FormView 동작을 트리거하기 위해 `CommandName` 값을 각각 `New`, `Edit`및 `Delete`로 설정 해야 합니다.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample8.aspx)]

그림 22는 브라우저를 통해 볼 때 FormView의 `ItemTemplate`을 보여 줍니다. 각 product 필드는 맨 아래에 새로 만들기, 편집 및 삭제 단추가 나열 됩니다.

[기본적 FormView ItemTemplate ![새, 편집 및 삭제 단추와 함께 각 Product 필드를 나열 합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image54.png)

**그림 22**: 기본적 FormView `ItemTemplate` 새, 편집 및 삭제 단추와 함께 각 제품 필드를 나열 합니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image56.png)).

GridView 및 DetailsView과 마찬가지로 Delete 단추를 클릭 하거나 `CommandName` 속성이 삭제로 설정 된 단추, LinkButton 또는 ImageButton을 클릭 하면 포스트백이 발생 하 고, FormView의 `DataKeyNames` 값을 기준으로 ObjectDataSource의 `DeleteParameters`를 채우고 ObjectDataSource의 `Delete()` 메서드를 호출 합니다.

편집 단추를 클릭 하 여 ensues를 클릭 하 고 데이터를 `EditItemTemplate`에 다시 바인딩할 경우이는 편집 인터페이스를 렌더링 하는 역할을 담당 합니다. 이 인터페이스는 업데이트 및 취소 단추와 함께 데이터를 편집 하는 웹 컨트롤을 포함 합니다. Visual Studio에서 생성 되는 기본 `EditItemTemplate`에는 자동 증분 필드 (`ProductID`)에 대 한 레이블, 부울이 아닌 값 필드에 대 한 입력란 및 각 부울 값 필드에 대 한 확인란이 포함 되어 있습니다. 이 동작은 GridView 및 DetailsView 컨트롤에서 자동 생성 된 BoundFields 매우 유사 합니다.

> [!NOTE]
> FormView의 `EditItemTemplate` 자동 생성에 대 한 한 가지 작은 문제는 `CategoryName` 및 `SupplierName`와 같이 읽기 전용인 필드에 대해 TextBox 웹 컨트롤을 렌더링 한다는 것입니다. 잠시 후에이를 고려 하는 방법을 살펴보겠습니다.

`EditItemTemplate`의 TextBox 컨트롤에는 *양방향 데이터 바인딩을*사용 하 여 해당 데이터 필드의 값에 바인딩된 `Text` 속성이 있습니다. `<%# Bind("dataField") %>`로 표시 되는 양방향 데이터 바인딩은 데이터를 템플릿에 바인딩할 때와 레코드 삽입 또는 편집을 위해 ObjectDataSource의 매개 변수를 채울 때 모두 데이터 바인딩을 수행 합니다. 즉, 사용자가 `ItemTemplate`에서 편집 단추를 클릭 하면 `Bind()` 메서드는 지정 된 데이터 필드 값을 반환 합니다. 사용자가 변경 하 고 업데이트를 클릭 하면 `Bind()`를 사용 하 여 지정한 데이터 필드에 해당 하는 다시 게시 된 값이 ObjectDataSource의 `UpdateParameters`에 적용 됩니다. 또는 `<%# Eval("dataField") %>`으로 표시 되는 단방향 데이터 바인딩은 데이터를 템플릿에 바인딩할 때만 데이터 필드 값을 검색 하 고 다시 게시할 때 사용자가 입력 한 값을 데이터 소스의 매개 변수에 반환 *하지* 않습니다.

다음 선언 태그는 FormView의 `EditItemTemplate`을 보여 줍니다. `Bind()` 메서드는 데이터 바인딩 구문에서 사용 되며, 업데이트 및 취소 단추 웹 컨트롤의 `CommandName` 속성을 적절 하 게 설정 합니다.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample9.aspx)]

현재 `EditItemTemplate`에서는이를 사용 하려고 할 때 예외가 throw 됩니다. 문제는 `CategoryName` 및 `SupplierName` 필드가 `EditItemTemplate`에서 TextBox 웹 컨트롤로 렌더링 된다는 것입니다. 이러한 텍스트 상자를 레이블로 변경 하거나 완전히 제거 해야 합니다. 단순히 `EditItemTemplate`에서 완전히 삭제 하겠습니다.

그림 23은 Chai에 대해 편집 단추를 클릭 한 후 브라우저의 FormView를 보여 줍니다. `EditItemTemplate`에서 제거 했으므로 `ItemTemplate`에 표시 된 `SupplierName` 및 `CategoryName` 필드가 더 이상 존재 하지 않습니다. 업데이트 단추를 클릭 하면 FormView는 GridView 및 DetailsView 컨트롤과 동일한 일련의 단계를 진행 합니다.

[![기본적으로 EditItemTemplate는 각 편집 가능한 제품 필드를 TextBox 또는 CheckBox로 표시 합니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image57.png)

**그림 23**: 기본적으로 `EditItemTemplate`는 각각의 편집 가능한 제품 필드를 TextBox 또는 CheckBox로 표시 합니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image59.png)).

삽입 단추를 클릭 하면 다시 게시 ensues `ItemTemplate` FormView가 클릭 됩니다. 그러나 새 레코드를 추가 하는 중이기 때문에 데이터는 FormView에 바인딩되지 않습니다. `InsertItemTemplate` 인터페이스에는 삽입 및 취소 단추와 함께 새 레코드를 추가 하는 웹 컨트롤이 포함 되어 있습니다. Visual Studio에서 생성 되는 기본 `InsertItemTemplate`에는 각 비 부울 값 필드에 대 한 텍스트 상자와 각 부울 값 필드에 대 한 CheckBox가 자동 생성 된 `EditItemTemplate`인터페이스와 유사 하 게 포함 됩니다. TextBox 컨트롤에는 양방향 데이터 바인딩을 사용 하 여 해당 데이터 필드의 값에 바인딩된 `Text` 속성이 있습니다.

다음 선언 태그는 FormView의 `InsertItemTemplate`을 보여 줍니다. `Bind()` 메서드는 데이터 바인딩 구문에서 사용 되며 삽입 및 취소 단추 웹 컨트롤의 `CommandName` 속성을 적절 하 게 설정 합니다.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample10.aspx)]

`InsertItemTemplate`의 FormView의 자동 생성을 사용 하는 미묘한 있습니다. 특히 TextBox 웹 컨트롤은 `CategoryName` 및 `SupplierName`와 같이 읽기 전용인 필드에 대해서도 생성 됩니다. `EditItemTemplate`와 마찬가지로 `InsertItemTemplate`에서 이러한 텍스트 상자를 제거 해야 합니다.

그림 24에서는 새 제품, Acme 커피를 추가할 때 브라우저의 FormView를 보여 줍니다. 방금 제거 했으므로 `ItemTemplate`에 표시 된 `SupplierName` 및 `CategoryName` 필드가 더 이상 존재 하지 않습니다. 삽입 단추를 클릭 하면 FormView는 DetailsView 컨트롤과 동일한 일련의 단계를 진행 하 여 `Products` 테이블에 새 레코드를 추가 합니다. 그림 25에서는 FormView가 삽입 된 후에 FormView의 Acme 제품 정보를 보여 줍니다.

[InsertItemTemplate는 FormView의 삽입 인터페이스를 지시 합니다. ![](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image60.png)

**그림 24**: FormView의 삽입 인터페이스를 결정 하는 `InsertItemTemplate` ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image62.png))

[새 제품에 대 한 세부 정보 (Acme 커피) ![FormView에 표시 됩니다.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image63.png)

**그림 25**: 새 제품에 대 한 세부 정보 (Acme 커피)는 FormView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image65.png)).

FormView를 사용 하면 읽기 전용, 편집 및 삽입 인터페이스를 세 개의 개별 템플릿으로 분리 하 여 DetailsView 및 GridView 보다 이러한 인터페이스를 보다 세밀 하 게 제어할 수 있습니다.

> [!NOTE]
> DetailsView과 마찬가지로 FormView의 `CurrentMode` 속성은 표시 되는 인터페이스를 나타내며, 해당 `DefaultMode` 속성은 편집 또는 삽입이 완료 된 후 FormView에서 반환 하는 모드를 나타냅니다.

## <a name="summary"></a>요약

이 자습서에서는 GridView, DetailsView 및 FormView를 사용 하 여 데이터를 삽입, 편집 및 삭제 하는 기본 사항을 살펴보았습니다. 이러한 세 가지 컨트롤은 데이터 웹 컨트롤과 ObjectDataSource 덕분에 ASP.NET 페이지에 코드를 한 줄도 작성 하지 않고도 활용할 수 있는 기본 제공 데이터 수정 기능을 제공 합니다. 그러나 단순 지점 및 클릭 기술은 매우 frail 및 naive 데이터 수정 사용자 인터페이스를 렌더링 합니다. 유효성 검사를 제공 하 고, 프로그래밍 방식 값을 삽입 하 고, 예외를 정상적으로 처리 하 고, 사용자 인터페이스를 사용자 지정 하기 위해 다음 몇 가지 자습서에서 설명 하는 기술 일련을 사용 해야 합니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

> [!div class="step-by-step"]
> [다음](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)
