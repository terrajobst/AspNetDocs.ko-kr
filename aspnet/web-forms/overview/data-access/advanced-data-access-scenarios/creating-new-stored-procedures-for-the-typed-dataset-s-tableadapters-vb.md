---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: 형식화 된 데이터 집합의 Tableadapter에 대 한 새 저장 프로시저 만들기 (VB) | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서는 코드에서 SQL 문을 만들고 실행할 데이터베이스에 문을 전달 했습니다. 다른 방법은를 사용 하는 것입니다.
ms.author: riande
ms.date: 07/18/2007
ms.assetid: a5a4a9ba-d18d-489a-a6b0-a3c26d6b0274
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: a7cc890038e5bb4eb61c7c3b808154c196ab2423
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74605997"
---
# <a name="creating-new-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>형식화된 데이터 세트의 TableAdapter에 대한 새로운 저장 프로시저 만들기(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_67_VB.zip) 또는 [PDF 다운로드](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial67vb1.pdf)

> 이전 자습서에서는 코드에서 SQL 문을 만들고 실행할 데이터베이스에 문을 전달 했습니다. 또 다른 방법은 SQL 문이 데이터베이스에서 미리 정의 되는 저장 프로시저를 사용 하는 것입니다. 이 자습서에서는 TableAdapter 마법사에서 새 저장 프로시저를 생성 하는 방법에 대해 알아봅니다.

## <a name="introduction"></a>소개

이러한 자습서에 대 한 DAL (데이터 액세스 계층)은 형식화 된 데이터 집합을 사용 합니다. [데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서에 설명 된 대로 형식화 된 데이터 집합은 강력한 형식의 Datatable 및 tableadapter로 구성 됩니다. Datatable는 데이터 액세스를 수행 하기 위해 기본 데이터베이스로 Tableadapter 인터페이스를 사용 하는 동안 시스템의 논리적 엔터티를 나타냅니다. 여기에는 데이터에 Datatable 채우기, 스칼라 데이터를 반환 하는 쿼리 실행, 데이터베이스에서 레코드 삽입, 업데이트 및 삭제가 포함 됩니다.

Tableadapter에 의해 실행 되는 SQL 명령은 `SELECT columnList FROM TableName`또는 저장 프로시저와 같은 임시 SQL 문 중 하나일 수 있습니다. 아키텍처의 Tableadapter는 임시 SQL 문을 사용 합니다. 그러나 대부분의 개발자와 데이터베이스 관리자는 보안, 유지 관리 효율성 및 업데이트 가능성을 위해 임시 SQL 문에 대 한 저장 프로시저를 선호 합니다. 다른 ardently은 유연성을 위해 임시 SQL 문을 선호 합니다. 자체 작업에서 임시 SQL 문에 대해 저장 프로시저를 선호 하지만 임시 SQL 문을 사용 하 여 이전 자습서를 간소화 하도록 선택 했습니다.

TableAdapter를 정의 하거나 새 메서드를 추가 하는 경우 TableAdapter 마법사를 사용 하면 임시 SQL 문을 사용 하는 것 처럼 새 저장 프로시저를 만들거나 기존 저장 프로시저를 쉽게 사용할 수 있습니다. 이 자습서에서는 TableAdapter s 마법사에서 저장 프로시저를 자동으로 생성 하는 방법을 살펴보겠습니다. 다음 자습서에서는 기존 또는 수동으로 만든 저장 프로시저를 사용 하도록 TableAdapter의 메서드를 구성 하는 방법을 살펴봅니다.

> [!NOTE]
> 저장 프로시저 및 임시 SQL의 장단점에 대 한 역동적인 논의는 Rob Howard의 블로그 항목에서 [저장 프로시저를 아직 사용 하지 않나요?](http://grokable.com/2003/11/dont-use-stored-procedures-yet-must-be-suffering-from-nihs-not-invented-here-syndrome/) 및 [frans Bouma](https://weblogs.asp.net/fbouma/) s 블로그 항목 [저장 프로시저는 잘못 된](https://weblogs.asp.net/fbouma/archive/2003/11/18/38178.aspx) 것입니다.

## <a name="stored-procedure-basics"></a>저장 프로시저 기본 사항

함수는 모든 프로그래밍 언어에 공통적인 구문입니다. 함수는 함수가 호출 될 때 실행 되는 문의 컬렉션입니다. 함수는 입력 매개 변수를 허용 하 고 선택적으로 값을 반환할 수 있습니다. *[저장 프로시저](http://en.wikipedia.org/wiki/Stored_procedure)* 는 프로그래밍 언어의 기능과 많은 유사성을 공유 하는 데이터베이스 구문입니다. 저장 프로시저는 저장 프로시저가 호출 될 때 실행 되는 T-sql 문 집합으로 구성 됩니다. 저장 프로시저는 0 개에서 많은 입력 매개 변수를 허용 하 고 `SELECT` 쿼리의 스칼라 값, 출력 매개 변수 또는 가장 일반적으로 결과 집합을 반환할 수 있습니다.

> [!NOTE]
> 저장 프로시저는 sprocs 또는 SPs 라고도 합니다.

저장 프로시저는 [`CREATE PROCEDURE`](https://msdn.microsoft.com/library/aa258259(SQL.80).aspx) t-sql 문을 사용 하 여 생성 됩니다. 예를 들어 다음 T-sql 스크립트는 `@CategoryID` 라는 단일 매개 변수를 사용 하는 `GetProductsByCategoryID` 라는 저장 프로시저를 만들고 `UnitPrice`테이블에서 일치 하는 `Discontinued` 값이 있는 열의 `ProductID`, `ProductName`, `Products` 및 `CategoryID` 필드를 반환 합니다.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

이 저장 프로시저를 만든 후에는 다음 구문을 사용 하 여 호출할 수 있습니다.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.sql)]

> [!NOTE]
> 다음 자습서에서는 Visual Studio IDE를 통해 저장 프로시저를 만드는 방법을 살펴봅니다. 그러나이 자습서에서는 TableAdapter 마법사가 저장 프로시저를 자동으로 생성 하도록 합니다.

저장 프로시저는 단순히 데이터를 반환 하는 것 외에도 단일 트랜잭션 범위 내에서 여러 데이터베이스 명령을 수행 하는 데 사용 됩니다. 예를 들어 `DeleteCategory`라는 저장 프로시저는 `@CategoryID` 매개 변수를 사용 하 고 두 개의 `DELETE` 문을 수행할 수 있습니다. 첫 번째는 관련 제품을 삭제 하 고 다른 하나는 지정 된 범주를 삭제 하는 문입니다. 저장 프로시저 내의 여러 문이 트랜잭션 내에서 자동으로 래핑되지 *않습니다* . 저장 프로시저의 여러 명령이 원자성 작업으로 처리 되도록 하기 위해 추가 T-sql 명령을 실행 해야 합니다. 이후 자습서의 트랜잭션 범위 내에서 저장 프로시저의 명령을 래핑하는 방법을 살펴보겠습니다.

아키텍처 내에서 저장 프로시저를 사용 하는 경우 데이터 액세스 계층의 메서드는 임시 SQL 문을 실행 하는 대신 특정 저장 프로시저를 호출 합니다. 이는 응용 프로그램 아키텍처 내에서 정의 하지 않고 데이터베이스에서 실행 되는 SQL 문의 위치를 중앙 집중화 합니다. 이러한 중앙 집중화를 통해 쿼리를 보다 쉽게 찾고 분석 하 고 조정할 수 있으며, 데이터베이스를 사용 하는 위치 및 방법에 대 한 보다 명확한 그림을 제공 합니다.

저장 프로시저 기본 사항에 대 한 자세한 내용은이 자습서의 끝부분에 있는 추가 읽기 섹션의 리소스를 참조 하세요.

## <a name="step-1-creating-the-advanced-data-access-layer-scenarios-web-pages"></a>1 단계: 고급 데이터 액세스 계층 시나리오 웹 페이지 만들기

저장 프로시저를 사용 하 여 DAL을 만드는 방법에 대 한 논의를 시작 하기 전에 먼저 웹 사이트 프로젝트에 ASP.NET 페이지를 만들어이에 필요한 다음 몇 가지 자습서를 수행 하겠습니다. `AdvancedDAL`이라는 새 폴더를 추가 하 여 시작 합니다. 그런 다음, 다음 ASP.NET 페이지를 해당 폴더에 추가 하 여 각 페이지를 `Site.master` 마스터 페이지에 연결 합니다.

- `Default.aspx`
- `NewSprocs.aspx`
- `ExistingSprocs.aspx`
- `JOINs.aspx`
- `AddingColumns.aspx`
- `ComputedColumns.aspx`
- `EncryptingConfigSections.aspx`
- `ManagedFunctionsAndSprocs.aspx`

![고급 데이터 액세스 계층 시나리오 자습서에 대 한 ASP.NET 페이지 추가](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**그림 1**: 고급 데이터 액세스 계층 시나리오 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `AdvancedDAL` 폴더의 `Default.aspx`에는 해당 섹션의 자습서가 나열 됩니다. `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤은이 기능을 제공 합니다. 따라서이 사용자 정의 컨트롤을 솔루션 탐색기에서 페이지 디자인 뷰로 끌어 `Default.aspx`에 추가 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)

**그림 2**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png))

마지막으로, 이러한 페이지를 `Web.sitemap` 파일에 항목으로 추가 합니다. 특히 `<siteMapNode>`일괄 처리 된 데이터로 작업 한 후 다음 태그를 추가 합니다.

[!code-xml[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에 고급 DAL 시나리오 자습서에 대 한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 고급 DAL 시나리오 자습서에 대 한 항목이 포함 되어 있습니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)

**그림 3**: 이제 사이트 맵에 고급 DAL 시나리오 자습서에 대 한 항목이 포함 되어 있습니다.

## <a name="step-2-configuring-a-tableadapter-to-create-new-stored-procedures"></a>2 단계: TableAdapter를 구성 하 여 새 저장 프로시저 만들기

임시 SQL 문 대신 저장 프로시저를 사용 하는 데이터 액세스 계층을 만드는 방법을 보여 주기 위해 `NorthwindWithSprocs.xsd`라는 `~/App_Code/DAL` 폴더에 형식화 된 새 데이터 집합을 만듭니다. 이전 자습서에서이 프로세스에 대해 자세히 설명 했으므로 여기의 단계를 빠르게 진행할 예정입니다. 형식화 된 데이터 집합을 만들고 구성 하는 방법에 대 한 자세한 단계별 지침이 발생 하거나 필요한 경우에는 [데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서를 다시 참조 하세요.

그림 4에 표시 된 것 처럼 `DAL` 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택한 다음 데이터 집합 템플릿을 선택 하 여 프로젝트에 새 데이터 집합을 추가 합니다.

[NorthwindWithSprocs 라는 프로젝트에 새 형식화 된 데이터 집합을 추가 ![합니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png)

**그림 4**: `NorthwindWithSprocs.xsd` 라는 프로젝트에 새 형식화 된 데이터 집합 추가 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png))

이렇게 하면 형식화 된 새 데이터 집합이 생성 되 고, 해당 디자이너를 열고, 새 TableAdapter를 만들고, TableAdapter 구성 마법사를 시작 합니다. TableAdapter 구성 마법사의 첫 번째 단계에서는 사용할 데이터베이스를 선택 하 라는 메시지를 표시 합니다. Northwind 데이터베이스에 대 한 연결 문자열이 드롭다운 목록에 나열 됩니다. 이 확인란을 선택 하 고 다음을 클릭 합니다.

다음 화면에서 TableAdapter가 데이터베이스에 액세스 하는 방법을 선택할 수 있습니다. 이전 자습서에서는 첫 번째 옵션인 SQL 문 사용을 선택 했습니다. 이 자습서에서는 두 번째 옵션인 새 저장 프로시저 만들기를 선택 하 고 다음을 클릭 합니다.

[TableAdapter에 새 저장 프로시저를 만들도록 지시 ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png)

**그림 5**: TableAdapter에 새 저장 프로시저를 만들도록 지시 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png))

임시 SQL 문을 사용 하는 것과 마찬가지로, 다음 단계에서는 TableAdapter 주 쿼리에 대 한 `SELECT` 문을 제공 하 라는 메시지가 표시 됩니다. 그러나 여기에 입력 된 `SELECT` 문을 사용 하 여 임시 쿼리를 직접 수행 하는 대신 TableAdapter s 마법사는이 `SELECT` 쿼리를 포함 하는 저장 프로시저를 만듭니다.

이 TableAdapter에 대해 다음 `SELECT` 쿼리를 사용 합니다.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]

[SELECT 쿼리를 입력 ![.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png)

**그림 6**: `SELECT` 쿼리 입력 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png))

> [!NOTE]
> 위의 쿼리는 `Northwind` 형식화 된 데이터 집합에 있는 `ProductsTableAdapter`의 주 쿼리와 약간 다릅니다. `Northwind` 형식화 된 데이터 집합의 `ProductsTableAdapter`에는 각 제품 범주와 공급자에 대 한 범주 이름과 회사 이름을 다시 가져오는 두 개의 상호 관련 된 하위 쿼리가 포함 되어 있습니다. 예정 된 [tableadapter를 사용 하 여 조인을 사용 하는 업데이트](updating-the-tableadapter-to-use-joins-vb.md) 자습서에서이 tableadapter에 이와 관련 된 데이터를 추가 하는 방법을 살펴보겠습니다.

잠시 시간을 클릭 하 여 고급 옵션 단추를 클릭 합니다. 여기서는 마법사에서 TableAdapter에 대해 insert, update 및 delete 문을 생성 해야 하는지 여부, 낙관적 동시성을 사용할지 여부 및 삽입 및 업데이트 후 데이터 테이블을 새로 고칠지 여부를 지정할 수 있습니다. Insert, Update 및 Delete 문 생성 옵션은 기본적으로 선택 되어 있습니다. 선택 된 상태로 둡니다. 이 자습서에서는 낙관적 동시성 사용 옵션을 선택 하지 않은 상태로 둡니다.

TableAdapter 마법사에서 자동으로 저장 프로시저를 만들면 데이터 테이블 새로 고침 옵션이 무시 되는 것으로 나타납니다. 이 확인란을 선택 했는지 여부에 관계 없이 3 단계에서 볼 수 있는 것 처럼 결과 insert 및 update 저장 프로시저는 방금 삽입 하거나 방금 업데이트 한 레코드를 검색 합니다.

![삽입, 업데이트 및 삭제 문 생성 옵션을 선택한 상태로 둡니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png)

**그림 7**: Insert, Update 및 Delete 문 생성 옵션 선택 된 상태로 두기

> [!NOTE]
> 낙관적 동시성 사용 옵션을 선택 하면 다른 필드가 변경 된 경우 데이터를 업데이트 하지 못하도록 하는 추가 조건이 `WHERE` 절에 추가 됩니다. TableAdapter s 기본 제공 낙관적 동시성 제어 기능을 사용 하는 방법에 대 한 자세한 내용은 [낙관적 동시성 구현](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md) 자습서를 다시 참조 하세요.

`SELECT` 쿼리를 입력 하 고 Insert, Update 및 Delete 문 생성 옵션이 선택 되어 있는지 확인 한 후 다음을 클릭 합니다. 그림 8에 표시 된 다음 화면은 마법사에서 데이터를 선택, 삽입, 업데이트 및 삭제 하는 데 사용할 저장 프로시저의 이름을 묻는 메시지를 표시 합니다. 이러한 저장 프로시저 이름을 `Products_Select`, `Products_Insert`, `Products_Update`및 `Products_Delete`로 변경 합니다.

[저장 프로시저 ![이름 바꾸기](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**그림 8**: 저장 프로시저 이름 바꾸기 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png))

TableAdapter 마법사가 4 개의 저장 프로시저를 만드는 데 사용 하는 T-sql을 보려면 SQL 스크립트 미리 보기 단추를 클릭 합니다. SQL 스크립트 미리 보기 대화 상자에서 스크립트를 파일에 저장 하거나 클립보드로 복사할 수 있습니다.

![저장 프로시저를 생성 하는 데 사용 되는 SQL 스크립트를 미리 봅니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**그림 9**: 저장 프로시저를 생성 하는 데 사용 되는 SQL 스크립트 미리 보기

저장 프로시저의 이름을 지정 하 고 다음을 클릭 하 여 TableAdapter의 해당 메서드 이름을 지정 합니다. 임시 SQL 문을 사용 하는 경우와 마찬가지로 기존 DataTable을 채우거 나 새 DataTable을 반환 하는 메서드를 만들 수 있습니다. 또한 TableAdapter에 레코드 삽입, 업데이트 및 삭제를 위한 DB 직접 패턴을 포함 해야 하는지 여부를 지정할 수 있습니다. 세 개의 확인란을 모두 선택 된 상태로 두고 이름이 DataTable 메서드 반환을 `GetProducts` (그림 10에 표시 된 것 처럼)로 바꿉니다.

[메서드 이름 채우기 및 GetProducts ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)

**그림 10**: `Fill` 메서드 이름 및 `GetProducts` ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png))

다음을 클릭 하 여 마법사에서 수행 하는 단계에 대 한 요약을 확인 합니다. 마침 단추를 클릭 하 여 마법사를 완료 합니다. 마법사가 완료 되 면 데이터 집합의 디자이너에 게 반환 되며, 이제 `ProductsDataTable`를 포함 해야 합니다.

[데이터 집합 ![디자이너에서 새로 추가 된 ProductsDataTable을 표시 합니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)

**그림 11**: 데이터 집합 s 디자이너에 새로 추가 된 `ProductsDataTable` 표시 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png))

## <a name="step-3-examining-the-newly-created-stored-procedures"></a>3 단계: 새로 생성 된 저장 프로시저 검사

2 단계에서 사용 되는 TableAdapter 마법사는 데이터를 선택, 삽입, 업데이트 및 삭제 하기 위한 저장 프로시저를 자동으로 만들었습니다. 이러한 저장 프로시저는 서버 탐색기로 이동 하 고 데이터베이스의 저장 프로시저 폴더로 드릴 다운 하 여 Visual Studio를 통해 보거나 수정할 수 있습니다. 그림 12와 같이 Northwind 데이터베이스에는 `Products_Delete`, `Products_Insert`, `Products_Select`및 `Products_Update`의 네 가지 새 저장 프로시저가 포함 되어 있습니다.

![2 단계에서 만든 4 개의 저장 프로시저는 데이터베이스의 저장 프로시저 폴더에서 찾을 수 있습니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)

**그림 12**: 2 단계에서 만든 4 개의 저장 프로시저는 데이터베이스의 저장 프로시저 폴더에서 찾을 수 있습니다.

> [!NOTE]
> 서버 탐색기 표시 되지 않으면 보기 메뉴로 이동 하 여 서버 탐색기 옵션을 선택 합니다. 2 단계에서 추가한 제품 관련 저장 프로시저가 표시 되지 않는 경우 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새로 고침을 선택 합니다.

저장 프로시저를 보거나 수정 하려면 서버 탐색기에서 해당 이름을 두 번 클릭 하거나 저장 프로시저를 마우스 오른쪽 단추로 클릭 하 고 열기를 선택 합니다. 그림 13은 열 때 `Products_Delete` 저장 프로시저를 보여 줍니다.

[![저장 프로시저는 Visual Studio 내에서 열고 수정할 수 있습니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png)

**그림 13**: Visual Studio 내에서 저장 프로시저를 열고 수정할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png)).

`Products_Delete`와 `Products_Select` 저장 프로시저의 내용은 모두 매우 간단 합니다. 반면에 `Products_Insert`와 `Products_Update` 저장 프로시저는 모두 `INSERT` 및 `UPDATE` 문 다음에 `SELECT` 문을 수행 하는 것을 더 자세히 검사 합니다. 예를 들어 다음 SQL은 `Products_Insert` 저장 프로시저를 만듭니다.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

저장 프로시저는 TableAdapter s 마법사에 지정 된 `SELECT` 쿼리에서 반환 된 `Products` 열을 입력 매개 변수로 받아들이고 이러한 값은 `INSERT` 문에서 사용 됩니다. `INSERT` 문을 따라 `SELECT` 쿼리를 사용 하 여 새로 추가 된 레코드의 `Products` 열 값 (`ProductID`포함)을 반환 합니다. 이 새로 고침 기능은 새로 추가 된 `ProductRow` 인스턴스 `ProductID` 속성을 데이터베이스에서 할당 한 자동 증가 값으로 자동으로 업데이트 하므로 일괄 처리 업데이트 패턴을 사용 하 여 새 레코드를 추가 하는 경우에 유용 합니다.

다음 코드에서는이 기능을 보여 줍니다. `NorthwindWithSprocs` 형식화 된 데이터 집합에 대해 생성 된 `ProductsTableAdapter` 및 `ProductsDataTable`를 포함 합니다. `ProductsRow` 인스턴스를 만들고 해당 값을 제공 하 고 TableAdapter s `Update` 메서드를 호출 하 여 `ProductsDataTable`을 전달 하면 새 제품이 데이터베이스에 추가 됩니다. 내부적으로 TableAdapter s `Update` 메서드는 전달 된 DataTable의 `ProductsRow` 인스턴스를 열거 하 고 (이 예제에서는 방금 추가한 하나만 있는 경우) 적절 한 insert, update 또는 delete 명령을 수행 합니다. 이 경우 `Products` 테이블에 새 레코드를 추가 하 고 새로 추가 된 레코드의 세부 정보를 반환 하는 `Products_Insert` 저장 프로시저가 실행 됩니다. 그러면 `ProductsRow` 인스턴스 `ProductID` 값이 업데이트 됩니다. `Update` 메서드가 완료 된 후에는 `ProductsRow` s `ProductID` 속성을 통해 새로 추가 된 레코드 s `ProductID` 값에 액세스할 수 있습니다.

[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.vb)]

`Products_Update` 저장 프로시저는 `UPDATE` 문 뒤에 `SELECT` 문을 포함 합니다.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample7.sql)]

이 저장 프로시저에는 `ProductID``@Original_ProductID` 및 `@ProductID`의 두 입력 매개 변수가 포함 되어 있습니다. 이 기능을 사용 하면 기본 키가 변경 될 수 있는 시나리오를 사용할 수 있습니다. 예를 들어 직원 데이터베이스에서 각 직원 레코드는 직원의 사회 보장 번호를 기본 키로 사용할 수 있습니다. 기존 직원 주민 등록 번호를 변경 하려면 새 주민 등록 번호와 원래 번호를 모두 제공 해야 합니다. `Products` 테이블의 경우 `ProductID` 열이 `IDENTITY` 열 이므로 이러한 기능이 필요 하지 않습니다. 실제로 `Products_Update` 저장 프로시저의 `UPDATE` 문에는 열 목록에 `ProductID` 열이 포함 되지 않습니다. 따라서 `UPDATE` 문 s `WHERE` 절에서 `@Original_ProductID` 사용 되는 동안 `Products` 테이블에 불필요 하며 `@ProductID` 매개 변수로 바꿀 수 있습니다. 저장 프로시저의 매개 변수를 수정 하는 경우 해당 저장 프로시저를 사용 하는 TableAdapter 메서드도 업데이트 해야 합니다.

## <a name="step-4-modifying-a-stored-procedure-s-parameters-and-updating-the-tableadapter"></a>4 단계: 저장 프로시저의 매개 변수 수정 및 TableAdapter 업데이트

`@Original_ProductID` 매개 변수는 불필요 하므로 `Products_Update` 저장 프로시저에서 모두 제거 합니다. `Products_Update` 저장 프로시저를 열고 `@Original_ProductID` 매개 변수를 삭제 한 다음 `UPDATE` 문의 `WHERE` 절에서 `@Original_ProductID`에서 사용 되는 매개 변수 이름을 `@ProductID`로 변경 합니다. 이러한 변경을 수행한 후 저장 프로시저 내의 T-sql은 다음과 같습니다.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample8.sql)]

이러한 변경 내용을 데이터베이스에 저장 하려면 도구 모음에서 저장 아이콘을 클릭 하거나 Ctrl + S를 누릅니다. 이 시점에서 `Products_Update` 저장 프로시저는 `@Original_ProductID` 입력 매개 변수를 필요로 하지 않지만 TableAdapter는 이러한 매개 변수를 전달 하도록 구성 됩니다. 데이터 집합 디자이너에서 TableAdapter를 선택 하 고 속성 창 이동한 다음 `UpdateCommand` s `Parameters` 컬렉션에서 줄임표를 클릭 하 여 TableAdapter가 `Products_Update` 저장 프로시저에 보낼 매개 변수를 볼 수 있습니다. 그러면 그림 14와 같이 매개 변수 컬렉션 편집기 대화 상자가 나타납니다.

![매개 변수 컬렉션 편집기에는 Products_Update 저장 프로시저에 전달 된 매개 변수가 나열 됩니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png)

**그림 14**: `Products_Update` 저장 프로시저에 전달 된 매개 변수를 나열 하는 매개 변수 컬렉션 편집기

멤버 목록에서 `@Original_ProductID` 매개 변수를 선택 하 고 제거 단추를 클릭 하 여 여기에서이 매개 변수를 제거할 수 있습니다.

또는 디자이너에서 TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 구성을 선택 하 여 모든 메서드에 사용 되는 매개 변수를 새로 고칠 수도 있습니다. 그러면 TableAdapter 구성 마법사가 표시 되 고 저장 프로시저에서 수신 하는 매개 변수와 함께 선택, 삽입, 업데이트 및 삭제에 사용 되는 저장 프로시저가 나열 됩니다. 업데이트 드롭다운 목록을 클릭 하면 `Products_Update` 저장 프로시저에 필요한 입력 매개 변수가 표시 됩니다. 여기에는 더 이상 `@Original_ProductID` 포함 되지 않습니다 (그림 15 참조). [마침]을 클릭 하면 TableAdapter에서 사용 되는 매개 변수 컬렉션을 자동으로 업데이트할 수 있습니다.

[또는 TableAdapter s 구성 마법사를 사용 하 여 메서드 매개 변수 컬렉션을 새로 고칠 수 ![.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**그림 15**: TableAdapter의 구성 마법사를 사용 하 여 메서드 매개 변수 컬렉션을 새로 고칠 수 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png)).

## <a name="step-5-adding-additional-tableadapter-methods"></a>5 단계: TableAdapter 메서드 추가

2 단계에서 설명 하는 것 처럼 새 TableAdapter를 만들 때 해당 하는 저장 프로시저가 자동으로 생성 되는 것이 쉽습니다. TableAdapter에 메서드를 더 추가 하는 경우에도 마찬가지입니다. 이를 설명 하기 위해 2 단계에서 만든 `ProductsTableAdapter`에 `GetProductByProductID(productID)` 메서드를 추가 해 보겠습니다. 이 메서드는 `ProductID` 값을 입력으로 사용 하 고 지정 된 제품에 대 한 세부 정보를 반환 합니다.

TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 쿼리 추가를 선택 하 여 시작 합니다.

![TableAdapter에 새 쿼리 추가](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**그림 16**: TableAdapter에 새 쿼리 추가

Tableadapter 쿼리 구성 마법사가 시작 되 고 TableAdapter가 데이터베이스에 액세스 하는 방법을 묻는 메시지가 표시 됩니다. 새 저장 프로시저를 만들도록 하려면 새 저장 프로시저 만들기 옵션을 선택 하 고 다음을 클릭 합니다.

[![새 저장 프로시저 만들기 옵션을 선택 합니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)

**그림 17**: 새 저장 프로시저 만들기 옵션 선택 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png))

다음 화면은 실행할 쿼리 유형을 식별 하거나, 행 집합 또는 단일 스칼라 값을 반환할지, 아니면 `UPDATE`, `INSERT`또는 `DELETE` 문을 수행할지를 묻는 메시지를 표시 합니다. `GetProductByProductID(productID)` 메서드는 행을 반환 하므로 행 반환 옵션을 선택한 상태로 두고 다음을 클릭 합니다.

[![행 반환 옵션을 선택 합니다.](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)

**그림 18**: 행을 반환 하는 선택 옵션 선택 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png))

다음 화면에는 저장 프로시저의 이름을 나열 하는 TableAdapter s 주 쿼리가 표시 됩니다 (`dbo.Products_Select`). 저장 프로시저 이름을 다음 `SELECT` 문으로 바꿉니다. 그러면 지정 된 제품에 대 한 모든 product 필드가 반환 됩니다.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample9.sql)]

[저장 프로시저 이름을 SELECT 쿼리로 대체 ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)

**그림 19**: 저장 프로시저 이름을 `SELECT` 쿼리로 바꾸기 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png))

이후 화면에서는 생성 될 저장 프로시저의 이름을 묻는 메시지를 표시 합니다. `Products_SelectByProductID` 이름을 입력 하 고 다음을 클릭 합니다.

[새 저장 프로시저의 이름을 ![Products_SelectByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image45.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**그림 20**: 새 저장 프로시저의 이름 `Products_SelectByProductID` ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image46.png))

마법사의 마지막 단계에서는 생성 된 메서드 이름을 변경 하 고 DataTable 패턴 채우기, DataTable 패턴 반환 또는 둘 다를 사용할지 여부를 지정할 수 있습니다. 이 메서드의 경우 두 옵션을 모두 선택 된 상태로 두고 메서드의 이름을 `FillByProductID`로 바꾸고 `GetProductByProductID`합니다. 다음을 클릭 하 여 마법사에서 수행 하는 단계에 대 한 요약을 확인 한 다음 마침을 클릭 하 여 마법사를 완료 합니다.

[TableAdapter의 메서드 이름을 FillByProductID 및 Getproductid Byproductid로 바꾸기 ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image48.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image47.png)

**그림 21**: TableAdapter의 메서드 이름을 `FillByProductID` 및 `GetProductByProductID`으로 바꾸기 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image49.png))

마법사를 완료 한 후 TableAdapter에는 호출할 때 방금 만든 `Products_SelectByProductID` 저장 프로시저를 실행 하는 `GetProductByProductID(productID)` 사용할 수 있는 새 메서드가 있습니다. 저장 프로시저 폴더를 열고 `Products_SelectByProductID`을 여는 서버 탐색기에서이 새 저장 프로시저를 확인해 보세요 (표시 되지 않는 경우 저장 프로시저 폴더를 마우스 오른쪽 단추로 클릭 하 고 새로 고침을 선택).

`SelectByProductID` 저장 프로시저는 입력 매개 변수로 `@ProductID`를 사용 하 고 마법사에서 입력 한 `SELECT` 문을 실행 합니다.

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample10.sql)]

## <a name="step-6-creating-a-business-logic-layer-class"></a>6 단계: 비즈니스 논리 계층 클래스 만들기

자습서 시리즈 전체에서 프레젠테이션 계층이 BLL (비즈니스 논리 계층)에 대 한 모든 호출을 수행 하는 계층화 된 아키텍처를 유지 관리 하도록 strived 했습니다. 이러한 디자인 결정을 따르기 위해 먼저 새 형식화 된 데이터 집합에 대 한 BLL 클래스를 만들어야 프레젠테이션 계층에서 제품 데이터에 액세스할 수 있습니다.

`~/App_Code/BLL` 폴더에 `ProductsBLLWithSprocs.vb` 라는 새 클래스 파일을 만들고 다음 코드에 추가 합니다.

[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample11.vb)]

이 클래스는 이전 자습서의 `ProductsBLL` 클래스 의미 체계를 모방 하지만 `ProductsTableAdapter`를 사용 하 고 `NorthwindWithSprocs` 데이터 집합의 개체를 `ProductsDataTable` 합니다. 예를 들어 클래스 파일의 시작 부분에 `Imports NorthwindTableAdapters` 문을 `ProductsBLL`에 포함 하는 대신 `ProductsBLLWithSprocs` 클래스는 `Imports NorthwindWithSprocsTableAdapters`를 사용 합니다. 마찬가지로이 클래스에서 사용 되는 `ProductsDataTable` 및 `ProductsRow` 개체에는 `NorthwindWithSprocs` 네임 스페이스가 접두사로 추가 됩니다. `ProductsBLLWithSprocs` 클래스는 `GetProducts` 및 `GetProductByProductID`라는 두 개의 데이터 액세스 메서드와 단일 제품 인스턴스를 추가, 업데이트 및 삭제 하는 메서드를 제공 합니다.

## <a name="step-7-working-with-thenorthwindwithsprocsdataset-from-the-presentation-layer"></a>7 단계: 프레젠테이션 계층에서`NorthwindWithSprocs`데이터 집합 사용

이 시점에서 저장 프로시저를 사용 하 여 기본 데이터베이스 데이터에 액세스 하 고 수정 하는 DAL을 만들었습니다. 또한 제품을 추가, 업데이트 및 삭제 하는 메서드와 함께 모든 제품 또는 특정 제품을 검색 하는 메서드를 사용 하 여 기초적인 BLL을 빌드 했습니다. 이 자습서를 반올림 하려면 `ProductsBLLWithSprocs` 클래스를 사용 하 여 레코드를 표시, 업데이트 및 삭제 하는 데 BLL s를 사용 하는 ASP.NET 페이지를 만들어 보겠습니다.

`AdvancedDAL` 폴더에서 `NewSprocs.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어와 `Products`이름을 지정 합니다. GridView의 스마트 태그를 선택 하 여 `ProductsDataSource`라는 새 ObjectDataSource에 바인딩합니다. 그림 22와 같이 `ProductsBLLWithSprocs` 클래스를 사용 하도록 ObjectDataSource를 구성 합니다.

[ProductsBLLWithSprocs 클래스를 사용 하도록 ObjectDataSource 구성 ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image51.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image50.png)

**그림 22**: `ProductsBLLWithSprocs` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image52.png))

선택 탭의 드롭다운 목록에는 `GetProducts` 및 `GetProductByProductID`의 두 옵션이 있습니다. GridView의 모든 제품을 표시 하려고 하므로 `GetProducts` 메서드를 선택 합니다. 업데이트, 삽입 및 삭제 탭의 드롭다운 목록에는 각각 하나의 메서드만 있습니다. 이러한 각 드롭다운 목록에서 적절 한 방법을 선택 했는지 확인 한 다음 마침을 클릭 합니다.

ObjectDataSource 마법사가 완료 되 면 Visual Studio에서 product 데이터 필드에 대 한 BoundFields 및 CheckBoxField를 GridView에 추가 합니다. 편집 사용 및 스마트 태그에 삭제 옵션 사용 옵션을 선택 하 여 GridView의 기본 제공 편집 및 삭제 기능을 설정 합니다.

[페이지에 편집 및 삭제 지원을 사용할 수 있는 GridView가 포함 된 ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image54.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image53.png)

**그림 23**: 편집 및 삭제 지원을 사용할 수 있는 GridView가 페이지에 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image55.png)).

이전 자습서에서 설명 했 듯이 ObjectDataSource s 마법사가 완료 되 면 Visual Studio는 `OldValuesParameterFormatString` 속성을 원래\_{0}으로 설정 합니다. BLL의 메서드에 필요한 매개 변수를 제공 하 여 데이터 수정 기능이 제대로 작동 하려면이 값을 기본값인 {0}로 되돌려야 합니다. 따라서 `OldValuesParameterFormatString` 속성을로 설정 하 여 선언적 구문에서 속성을 {0} 하거나 완전히 제거 해야 합니다.

데이터 원본 구성 마법사를 완료 한 후 GridView에서 지원 편집 및 삭제를 설정 하 고 ObjectDataSource s `OldValuesParameterFormatString` 속성을 기본값으로 반환 하면 페이지의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample12.aspx)]

이 시점에서 유효성 검사를 포함 하도록 편집 인터페이스를 사용자 지정 하 고, `CategoryID` 및 `SupplierID` 열을 Dropdownlist으로 렌더링 하는 등의 작업을 수행 하 여 GridView를 정리할 수 있습니다. 또한 클라이언트 쪽 확인을 삭제 단추에 추가할 수 있으며, 이러한 향상 된 기능을 구현 하는 데 걸리는 시간을 권장 합니다. 이러한 항목은 이전 자습서에서 설명 하기 때문에 여기서 다시 다루지 않습니다.

GridView를 개선 하는지 여부에 관계 없이 브라우저에서 페이지의 핵심 기능을 테스트 합니다. 그림 24와 같이 페이지에는 행당 편집 및 삭제 기능을 제공 하는 GridView의 제품이 나열 됩니다.

[GridView에서 제품을 보고 편집 하 고 삭제할 수 ![](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image57.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image56.png)

**그림 24**: GridView에서 제품을 보고 편집 하 고 삭제할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image58.png)).

## <a name="summary"></a>요약

형식화 된 데이터 집합의 Tableadapter는 임시 SQL 문이나 저장 프로시저를 사용 하 여 데이터베이스의 데이터에 액세스할 수 있습니다. 저장 프로시저를 사용 하 여 작업 하는 경우 기존 저장 프로시저를 사용 하거나 `SELECT` 쿼리를 기반으로 새 저장 프로시저를 만들 수 있도록 TableAdapter 마법사에 지시할 수 있습니다. 이 자습서에서는 저장 프로시저를 자동으로 생성 하는 방법을 살펴보았습니다.

저장 프로시저를 자동으로 생성 하 여 시간을 절약할 수 있는 반면, 마법사에서 생성 된 저장 프로시저는 사용자가 직접 만든 것과 일치 하지 않는 경우가 있습니다. 한 가지 예는 `@Original_ProductID` 매개 변수가 불필요 한 경우에도 `@Original_ProductID` 및 `@ProductID` 입력 매개 변수가 모두 필요한 `Products_Update` 저장 프로시저입니다.

대부분의 시나리오에서 저장 프로시저는 이미 생성 된 것일 수도 있고, 저장 프로시저의 명령을 보다 세부적으로 제어 하기 위해 수동으로 빌드해야 할 수도 있습니다. 두 경우 모두 TableAdapter에 메서드에 대 한 기존 저장 프로시저를 사용 하도록 지시 하는 것이 좋습니다. 다음 자습서에서이를 수행 하는 방법을 확인할 수 있습니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [저장 프로시저 만들기 및 유지 관리](https://msdn.microsoft.com/library/aa214299(SQL.80).aspx)
- [저장 프로시저에서 스칼라 데이터 검색](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)
- [SQL Server 저장 프로시저 기본 사항](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)
- [저장 프로시저: 개요](http://www.sqlteam.com/item.asp?ItemID=563)
- [저장 프로시저 작성](http://www.4guysfromrolla.com/webtech/111499-1.shtml)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Hilton Geisenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
> [다음](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
