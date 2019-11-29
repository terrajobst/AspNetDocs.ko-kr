---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb
title: 트랜잭션 내에서 데이터베이스 수정 내용 래핑 (VB) | Microsoft Docs
author: rick-anderson
description: 이 자습서는 데이터 일괄 처리의 업데이트, 삭제 및 삽입을 확인 하는 4 개 중 첫 번째입니다. 이 자습서에서는 데이터베이스 트랜잭션을 허용 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 7d821db5-6cbb-4b38-af14-198f9155fc82
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb
msc.type: authoredcontent
ms.openlocfilehash: dee95ee2789a69aac5aa79b8358e58e3ee99e1b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636482"
---
# <a name="wrapping-database-modifications-within-a-transaction-vb"></a>트랜잭션 내에서 래핑된 데이터베이스 수정(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_VB.zip) 또는 [PDF 다운로드](wrapping-database-modifications-within-a-transaction-vb/_static/datatutorial63vb1.pdf)

> 이 자습서는 데이터 일괄 처리의 업데이트, 삭제 및 삽입을 확인 하는 4 개 중 첫 번째입니다. 이 자습서에서는 데이터베이스 트랜잭션에서 일괄 수정 작업을 원자성 작업으로 수행 하 여 모든 단계가 성공 하거나 모든 단계가 실패 하도록 하는 방법에 대해 알아봅니다.

## <a name="introduction"></a>소개

[데이터 삽입, 업데이트 및 삭제 자습서의 개요](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) 를 통해 GridView는 행 수준 편집 및 삭제를 기본적으로 지원 합니다. 마우스를 몇 번 클릭 하면 코드를 작성 하지 않고도 다양 한 데이터 수정 인터페이스를 만들 수 있습니다. 단, 편집 및 삭제를 사용 하는 경우에는 행 단위로 콘텐츠를 수정 해야 합니다. 그러나 특정 시나리오에서는 사용자에 게 레코드 일괄 처리를 편집 하거나 삭제할 수 있는 기능을 제공 해야 합니다.

예를 들어 대부분의 웹 기반 전자 메일 클라이언트는 그리드를 사용 하 여 각 행에 전자 메일 정보 (제목, 보낸 사람 등)와 함께 확인란이 포함 된 각 메시지를 나열 합니다. 이 인터페이스를 통해 사용자는 메시지를 확인 하 고 선택한 메시지 삭제 단추를 클릭 하 여 여러 메시지를 삭제할 수 있습니다. 일괄 처리 편집 인터페이스는 사용자가 일반적으로 여러 레코드를 편집 하는 경우에 적합 합니다. 사용자가 편집을 클릭 하 고 변경 내용을 적용 한 다음 수정 해야 하는 각 레코드에 대해 업데이트를 클릭 하는 대신 일괄 처리 편집 인터페이스에서 각 행을 편집 인터페이스로 렌더링 합니다. 사용자는 변경 해야 하는 행 집합을 신속 하 게 수정한 다음 모두 업데이트 단추를 클릭 하 여 이러한 변경 내용을 저장할 수 있습니다. 이 자습서 집합에서는 데이터 일괄 처리를 삽입, 편집 및 삭제 하기 위한 인터페이스를 만드는 방법을 살펴봅니다.

일괄 처리 작업을 수행할 때 일부 작업이 실패 하는 동안 일괄 처리의 일부 작업이 성공 하도록 할 수 있는지 여부를 확인 하는 것이 중요 합니다. 일괄 처리 삭제 인터페이스 – 첫 번째 선택 된 레코드가 성공적으로 삭제 되었지만 두 번째 레코드가 외래 키 제약 조건 위반으로 인해 실패 하는 경우 발생 하는 상황을 고려해 야 합니다. 첫 번째 레코드의 삭제를 롤백해야 합니까 아니면 첫 번째 레코드를 삭제 된 상태로 유지 해야 하나요?

일괄 처리 작업을 [원자성 작업](http://en.wikipedia.org/wiki/Atomic_operation)으로 처리 하려는 경우 모든 단계가 성공 하거나 모든 단계가 실패 한 경우에는 [데이터베이스 트랜잭션에](http://en.wikipedia.org/wiki/Database_transaction)대 한 지원을 포함 하도록 데이터 액세스 계층을 확대 해야 합니다. 데이터베이스 트랜잭션은 트랜잭션 상위에서 실행 되는 `INSERT`, `UPDATE`및 `DELETE` 문의 집합에 대해 원자성을 보장 하며 대부분의 최신 데이터베이스 시스템에서 지원 되는 기능입니다.

이 자습서에서는 데이터베이스 트랜잭션을 사용 하도록 DAL을 확장 하는 방법을 살펴보겠습니다. 이후 자습서에서는 인터페이스를 일괄 삽입, 업데이트 및 삭제 하기 위한 웹 페이지 구현을 검토 합니다. S를 시작 하겠습니다.

> [!NOTE]
> 일괄 처리 트랜잭션에서 데이터를 수정할 때 원자성은 항상 필요 하지는 않습니다. 일부 시나리오에서는 웹 기반 전자 메일 클라이언트에서 전자 메일 집합을 삭제 하는 경우와 같이 일부 데이터 수정 작업이 성공 하 고 동일한 일괄 처리에 있는 다른 사용자가 실패할 수 있습니다. 삭제 프로세스를 통해 중간에 데이터베이스 오류가 발생 하는 경우 오류 없이 처리 된 레코드가 삭제 된 상태로 남아 있을 수 있습니다. 이러한 경우 데이터베이스 트랜잭션을 지원 하기 위해 DAL을 수정할 필요가 없습니다. 그러나 원자성이 중요 한 다른 배치 작업 시나리오가 있습니다. 고객이 한 은행 계좌에서 다른 은행 계좌로 자금을 이동 하는 경우 두 가지 작업을 수행 해야 합니다. 자금은 첫 번째 계정에서 공제 다음 두 번째에 추가 해야 합니다. 뱅크는 첫 번째 단계에 성공 하지 못할 수 있지만 두 번째 단계가 실패 하는 경우 고객은 upset 당연히 수 있습니다. 이 자습서를 진행 하 여 데이터베이스 트랜잭션을 지원 하기 위해 DAL에 대 한 향상 된 기능을 구현 하는 것이 좋습니다. 여기에는 다음 세 가지 자습서에서 빌드할 인터페이스를 일괄 삽입, 업데이트 및 삭제 하는 방법에 대 한 계획을 수립 하지 않아도 됩니다.

## <a name="an-overview-of-transactions"></a>트랜잭션의 개요

대부분의 데이터베이스에는 여러 데이터베이스 명령을 단일 논리적 작업 단위로 그룹화 할 수 있도록 하는 *트랜잭션*지원이 포함 됩니다. 트랜잭션을 구성 하는 데이터베이스 명령은 원자성이 보장 됩니다. 즉, 모든 명령이 실패 하거나 모두 성공 하 게 됩니다.

일반적으로 트랜잭션은 다음 패턴을 사용 하 여 SQL 문을 통해 구현 됩니다.

1. 트랜잭션의 시작을 표시 합니다.
2. 트랜잭션을 구성 하는 SQL 문을 실행 합니다.
3. 2 단계의 문 중 하나에 오류가 있는 경우 트랜잭션을 롤백합니다.
4. 2 단계의 모든 문이 오류 없이 완료 되 면 트랜잭션을 커밋합니다.

SQL 스크립트를 작성 하거나 저장 프로시저를 만들 때 또는 ADO.NET 또는 [`System.Transactions` 네임 스페이스](https://msdn.microsoft.com/library/system.transactions.aspx)의 클래스를 사용 하 여 프로그래밍 방식으로 트랜잭션을 생성, 커밋 및 롤백하는 데 사용 되는 sql 문을 수동으로 입력할 수 있습니다. 이 자습서에서는 ADO.NET를 사용 하 여 트랜잭션 관리만 검토 합니다. 이후 자습서에서는 데이터 액세스 계층에서 저장 프로시저를 사용 하는 방법에 대해 설명 합니다 .이 경우에는 트랜잭션을 만들고 롤백하고 커밋하는 SQL 문을 살펴볼 것입니다. 자세한 내용은 [SQL Server 저장 프로시저의 트랜잭션 관리](http://www.4guysfromrolla.com/webtech/080305-1.shtml) 를 참조 하세요.

> [!NOTE]
> 개발자는 `System.Transactions` 네임 스페이스의 [`TransactionScope` 클래스](https://msdn.microsoft.com/library/system.transactions.transactionscope.aspx) 를 사용 하 여 트랜잭션 범위 내에서 일련의 문을 프로그래밍 방식으로 래핑하고, 서로 다른 두 데이터베이스 또는 Microsoft SQL Server 데이터베이스, Oracle 데이터베이스 및 웹 서비스와 같은 다른 유형의 데이터 저장소와 같은 여러 소스를 포함 하는 복잡 한 트랜잭션에 대 한 지원을 포함할 수 있습니다. ADO.NET가 데이터베이스 트랜잭션과 관련 되 고, 대부분의 경우 리소스를 훨씬 적게 사용 하기 때문에 `TransactionScope` 클래스 대신이 자습서에 대해 ADO.NET 트랜잭션을 사용 하기로 결정 했습니다. 또한 특정 시나리오에서는 `TransactionScope` 클래스가 MSDTC (Microsoft DTC(Distributed Transaction Coordinator))를 사용 합니다. MSDTC를 사용 하는 구성, 구현 및 성능 문제는 이러한 자습서의 범위를 벗어나 특수 하 고 고급 토픽입니다.

ADO.NET에서 SqlClient 공급자를 사용 하는 경우 트랜잭션은 [`SqlTransaction` 개체](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.aspx)를 반환 하는 [`SqlConnection` 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) [`BeginTransaction` 메서드](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.begintransaction.aspx)를 호출 하 여 시작 됩니다. 트랜잭션을 구성을 하는 데이터 수정 문은 `try...catch` 블록 내에 배치 됩니다. `try` 블록의 문에서 오류가 발생 하면 실행이 `SqlTransaction` 개체 [`Rollback` 메서드](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.rollback.aspx)를 통해 트랜잭션을 롤백할 수 있는 `catch` 블록으로 전송 됩니다. 모든 문이 성공적으로 완료 되 면 `try` 블록의 끝에 `SqlTransaction` 개체 s [`Commit` 메서드](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.commit.aspx) 를 호출 하면 트랜잭션이 커밋됩니다. 다음 코드 조각에서는이 패턴을 보여 줍니다. ADO.NET에서 트랜잭션을 사용 하는 방법에 대 한 추가 구문과 예는 [트랜잭션을 사용 하 여 데이터베이스 일관성 유지 관리](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx) 를 참조 하세요.

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample1.vb)]

기본적으로 형식화 된 데이터 집합의 Tableadapter는 트랜잭션을 사용 하지 않습니다. 트랜잭션에 대 한 지원을 제공 하려면 트랜잭션 범위 내에서 일련의 데이터 수정 문을 수행 하기 위해 위의 패턴을 사용 하는 추가 메서드를 포함 하도록 TableAdapter 클래스를 보강 해야 합니다. 2 단계에서는 partial 클래스를 사용 하 여 이러한 메서드를 추가 하는 방법을 알아봅니다.

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>1 단계: 일괄 처리 된 데이터 웹 페이지로 작업 만들기

데이터베이스 트랜잭션을 지원 하기 위해 DAL을 보강 하는 방법에 대 한 탐색을 시작 하기 전에 먼저이 자습서에 필요한 ASP.NET 웹 페이지를 만들고 다음 세 가지를 수행 합니다. `BatchData` 이라는 새 폴더를 추가 하 여 시작한 후 다음 ASP.NET 페이지를 추가 하 여 각 페이지를 `Site.master` 마스터 페이지와 연결 합니다.

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`

![SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가](wrapping-database-modifications-within-a-transaction-vb/_static/image1.gif)

**그림 1**: SqlDataSource 관련 자습서에 대 한 ASP.NET 페이지 추가

다른 폴더와 마찬가지로 `Default.aspx`에서는 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤을 사용 하 여 해당 섹션 내의 자습서를 나열 합니다. 따라서이 사용자 정의 컨트롤을 솔루션 탐색기에서 페이지 디자인 뷰로 끌어 `Default.aspx`에 추가 합니다.

[SectionLevelTutorialListing 사용자 정의 컨트롤을 Default.aspx에 추가 ![](wrapping-database-modifications-within-a-transaction-vb/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image1.png)

**그림 2**: `Default.aspx`에 `SectionLevelTutorialListing.ascx` 사용자 정의 컨트롤 추가 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-vb/_static/image2.png))

마지막으로, 이러한 4 개의 페이지를 `Web.sitemap` 파일에 항목으로 추가 합니다. 특히 사이트 맵 사용자 지정을 `<siteMapNode>`다음 태그를 추가 합니다.

[!code-xml[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample2.xml)]

`Web.sitemap`업데이트 한 후 브라우저를 통해 자습서 웹 사이트를 잠시 기다려 주십시오. 이제 왼쪽의 메뉴에 일괄 처리 된 데이터로 작업 하기 위한 항목이 포함 되어 있습니다.

![이제 사이트 맵에 일괄 처리 된 데이터 사용 자습서에 대 한 항목이 포함 됩니다.](wrapping-database-modifications-within-a-transaction-vb/_static/image3.gif)

**그림 3**: 이제 사이트 맵에 일괄 처리 된 데이터 사용 자습서에 대 한 항목이 포함 되어 있습니다.

## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>2 단계: 데이터베이스 트랜잭션을 지원 하도록 데이터 액세스 계층 업데이트

[데이터 액세스 계층을 만드는](../introduction/creating-a-data-access-layer-vb.md)첫 번째 자습서에서 설명 했 듯이 DAL의 형식화 된 데이터 집합은 Datatable 및 tableadapter로 구성 됩니다. Datatable은 데이터를 저장 하는 반면 Tableadapter는 데이터베이스에서 Datatable로 데이터를 읽는 기능을 제공 하 여 Datatable에 대 한 변경 내용으로 데이터베이스를 업데이트 하는 등의 작업을 수행 합니다. Tableadapter는 데이터 업데이트를 위한 두 가지 패턴을 제공 합니다 .이를 일괄 업데이트 및 DB 직접 이라고 합니다. 일괄 처리 업데이트 패턴을 사용 하 여 TableAdapter는 DataSet, DataTable 또는 Datarow의 컬렉션에 전달 됩니다. 이 데이터는 열거 되며 삽입, 수정 또는 삭제 된 각 행에 대해 `InsertCommand`, `UpdateCommand`또는 `DeleteCommand` 실행 됩니다. DB 직접 패턴을 사용 하면 TableAdapter는 단일 레코드를 삽입, 업데이트 또는 삭제 하는 데 필요한 열 값을 대신 전달 합니다. 그런 다음 DB 직접 패턴 메서드는 전달 된 값을 사용 하 여 적절 한 `InsertCommand`, `UpdateCommand`또는 `DeleteCommand` 문을 실행 합니다.

사용 되는 업데이트 패턴에 관계 없이 Tableadapter 자동 생성 된 메서드에서는 트랜잭션을 사용 하지 않습니다. 기본적으로 TableAdapter에서 수행 하는 각 삽입, 업데이트 또는 삭제는 단일 불연속 작업으로 처리 됩니다. 예를 들어, 데이터베이스에 10 개의 레코드를 삽입 하기 위해 BLL의 일부 코드에서 DB 직접 패턴을 사용 한다고 가정 합니다. 이 코드는 TableAdapter s `Insert` 메서드를 10 번 호출 합니다. 처음 5 개 삽입이 성공 하지만 여섯 번째 삽입이 예외를 발생 시킨 경우 처음 5 개의 삽입 된 레코드는 데이터베이스에 남아 있습니다. 마찬가지로 일괄 처리 업데이트 패턴을 사용 하 여 DataTable에서 삽입, 수정 및 삭제 된 행에 대 한 삽입, 업데이트 및 삭제를 수행 하는 경우, 처음 몇 번의 수정 작업에 성공 했지만 나중에 오류가 발생 한 경우 이전에 수정 된 내용이 완료 됨은 데이터베이스에 남아 있습니다.

특정 시나리오에서는 일련의 수정에 대해 원자성을 보장 하려고 합니다. 이렇게 하려면 트랜잭션 상위에서 `InsertCommand`, `UpdateCommand`및 `DeleteCommand`를 실행 하는 새 메서드를 추가 하 여 TableAdapter를 수동으로 확장 해야 합니다. [데이터 액세스 계층을 만들](../introduction/creating-a-data-access-layer-vb.md) 때 [partial 클래스](http://en.wikipedia.org/wiki/Partial_type) 를 사용 하 여 형식화 된 데이터 집합 내에서 datatable의 기능을 확장 하는 방법을 살펴보았습니다. 이 기술은 Tableadapter와 함께 사용할 수도 있습니다.

형식화 된 데이터 집합 `Northwind.xsd` `App_Code` 폴더 s `DAL` 하위 폴더에 있습니다. `TransactionSupport` 이라는 `DAL` 폴더에 하위 폴더를 만들고 `ProductsTableAdapter.TransactionSupport.vb` 라는 새 클래스 파일을 추가 합니다 (그림 4 참조). 이 파일은 트랜잭션을 사용 하 여 데이터 수정 작업을 수행 하기 위한 메서드를 포함 하는 `ProductsTableAdapter`의 부분 구현을 보유 합니다.

![TransactionSupport 라는 폴더와 이름이 Ststableadapter 인 클래스 파일을 추가 합니다.](wrapping-database-modifications-within-a-transaction-vb/_static/image4.gif)

**그림 4**: 이름이 `TransactionSupport` 폴더와 `ProductsTableAdapter.TransactionSupport.vb` 라는 클래스 파일 추가

`ProductsTableAdapter.TransactionSupport.vb` 파일에 다음 코드를 입력 합니다.

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample3.vb)]

클래스 선언의 `Partial` 키워드는에 추가 된 멤버가 `NorthwindTableAdapters` 네임 스페이스의 `ProductsTableAdapter` 클래스에 추가 된다는 것을 컴파일러에 나타냅니다. 파일 맨 위에 있는 `Imports System.Data.SqlClient` 문을 확인 합니다. TableAdapter는 SqlClient 공급자를 사용 하도록 구성 되었으므로 내부적으로 [`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter.aspx) 개체를 사용 하 여 데이터베이스에 대 한 명령을 실행 합니다. 따라서 `SqlTransaction` 클래스를 사용 하 여 트랜잭션을 시작한 다음 커밋하거나 롤백해야 합니다. Microsoft SQL Server 이외의 데이터 저장소를 사용 하는 경우 적절 한 공급자를 사용 해야 합니다.

이러한 메서드는 트랜잭션을 시작, 롤백 및 커밋하는 데 필요한 구성 요소를 제공 합니다. 이러한 항목은 `Public`표시 되어 `ProductsTableAdapter`, DAL의 다른 클래스 또는 BLL 등 아키텍처의 다른 계층에서 사용할 수 있습니다. `BeginTransaction`는 TableAdapter s 내부 `SqlConnection`를 열고 (필요한 경우) 트랜잭션을 시작 하 여 `Transaction` 속성에 할당 한 다음 해당 트랜잭션을 내부 `SqlDataAdapter` s `SqlCommand` 개체에 연결 합니다. `CommitTransaction` 및 `RollbackTransaction` 내부 `Rollback` 개체를 닫기 전에 `Transaction` 개체 `Commit` 및 `Connection` 메서드를 각각 호출 합니다.

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>3 단계: 트랜잭션 상위에서 데이터를 업데이트 및 삭제 하는 메서드 추가

이러한 메서드를 완료 한 후에는 트랜잭션 상위 수준에서 일련의 명령을 수행 하는 `ProductsDataTable` 또는 BLL에 메서드를 추가할 수 있습니다. 다음 메서드는 일괄 업데이트 패턴을 사용 하 여 트랜잭션을 사용 하 여 `ProductsDataTable` 인스턴스를 업데이트 합니다. `BeginTransaction` 메서드를 호출 하 여 트랜잭션을 시작한 다음 `Try...Catch` 블록을 사용 하 여 데이터 수정 문을 실행 합니다. `Adapter` 개체 s `Update` 메서드를 호출 하면 예외가 발생할 경우 트랜잭션이 롤백되고 예외가 다시 throw 되는 `catch` 블록으로 실행이 전송 됩니다. `Update` 메서드는 제공 된 `ProductsDataTable`의 행을 열거 하 고 필요한 `InsertCommand`, `UpdateCommand`및 `DeleteCommand` s를 수행 하 여 Batch 업데이트 패턴을 구현 합니다. 이러한 명령 중 하나에서 오류가 발생 하면 트랜잭션이 롤백되고 트랜잭션 수명 중에 수행 된 이전 수정 내용이 취소 됩니다. `Update` 문이 오류 없이 완료 되 면 트랜잭션이 전체적으로 커밋됩니다.

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample4.vb)]

`ProductsTableAdapter.TransactionSupport.vb`의 partial 클래스를 통해 `ProductsTableAdapter` 클래스에 `UpdateWithTransaction` 메서드를 추가 합니다. 또는 몇 가지 사소한 구문이 변경 된 상태에서이 메서드를 비즈니스 논리 계층 s `ProductsBLL` 클래스에 추가할 수 있습니다. 즉, `Me.BeginTransaction()`, `Me.CommitTransaction()`및 `Me.RollbackTransaction()`에서 `Me` 키워드를 `Adapter`으로 바꾸어야 합니다 (`Adapter` 형식 `ProductsBLL`의 속성 이름 `ProductsTableAdapter`).

`UpdateWithTransaction` 메서드는 일괄 업데이트 패턴을 사용 하지만 다음과 같이 트랜잭션 범위 내에서 일련의 DB 직접 호출을 사용할 수도 있습니다. `DeleteProductsWithTransaction` 메서드는 삭제할 `ProductID` 인 `Integer`형식의 `List(Of T)` 입력으로 받아들입니다. 메서드는 `BeginTransaction`에 대 한 호출을 통해 트랜잭션을 시작한 다음 `Try` 블록에서 각 `ProductID` 값에 대해 DB 직접 패턴 `Delete` 메서드를 호출 하는 제공 된 목록을 반복 합니다. `Delete`에 대 한 호출이 실패 하면 트랜잭션이 롤백된 `Catch` 블록으로 제어가 전송 되 고 예외가 다시 throw 됩니다. `Delete`에 대 한 모든 호출이 성공 하면 트랜잭션이 커밋됩니다. `ProductsBLL` 클래스에이 메서드를 추가 합니다.

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample5.vb)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>여러 Tableadapter에서 트랜잭션 적용

이 자습서에서 검사 한 트랜잭션 관련 코드를 사용 하 여 `ProductsTableAdapter`에 대 한 여러 문을 원자성 작업으로 처리할 수 있습니다. 그러나 다른 데이터베이스 테이블에 대 한 여러 수정 작업을 원자 단위로 수행 해야 하는 경우는 어떻게 되나요? 예를 들어 범주를 삭제할 때 먼저 다른 범주에 현재 제품을 다시 할당할 수 있습니다. 제품을 재할당 하 고 범주를 삭제 하는 두 단계는 원자성 작업으로 실행 되어야 합니다. 그러나 `ProductsTableAdapter`에는 `Products` 테이블을 수정 하는 메서드만 포함 되며 `CategoriesTableAdapter`에는 `Categories` 테이블을 수정 하는 메서드만 포함 됩니다. 그렇다면 트랜잭션은 Tableadapter를 어떻게 포함할 수 있나요?

한 가지 옵션은 메서드를 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 라는 `CategoriesTableAdapter`에 추가 하 고 해당 메서드가 제품을 다시 할당 하 고 저장 프로시저 내에서 정의 된 트랜잭션 범위 내에서 범주를 삭제 하는 저장 프로시저를 호출 하도록 하는 것입니다. 이후 자습서에서 저장 프로시저의 트랜잭션을 시작, 커밋 및 롤백하는 방법을 살펴보겠습니다.

다른 옵션은 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 메서드를 포함 하는 DAL에서 도우미 클래스를 만드는 것입니다. 이 메서드는 `CategoriesTableAdapter` 및 `ProductsTableAdapter`의 인스턴스를 만든 다음이 두 개의 Tableadapter `Connection` 속성을 동일한 `SqlConnection` 인스턴스로 설정 합니다. 이 시점에서 두 Tableadapter 중 하나가 `BeginTransaction`를 호출 하 여 트랜잭션을 시작 합니다. 제품을 다시 할당 하 고 범주를 삭제 하는 Tableadapter 메서드는 필요에 따라 트랜잭션을 커밋하거나 롤백하는 `Try...Catch` 블록에서 호출 됩니다.

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>4 단계: 비즈니스 논리 계층에`UpdateWithTransaction`메서드 추가

3 단계에서는 DAL의 `ProductsTableAdapter`에 `UpdateWithTransaction` 메서드를 추가 했습니다. 해당 메서드를 BLL에 추가 해야 합니다. 프레젠테이션 계층은 DAL을 직접 호출 하 여 `UpdateWithTransaction` 메서드를 호출할 수 있지만, 이러한 자습서는 프레젠테이션 계층에서 DAL을 분리 하는 계층화 된 아키텍처를 정의 하는 데 strived 있습니다. 따라서이 방법을 계속 behooves.

`ProductsBLL` 클래스 파일을 열고 단순히 해당 DAL 메서드를 호출 하는 `UpdateWithTransaction` 라는 메서드를 추가 합니다. 이제 `ProductsBLL`에 두 가지 새로운 메서드가 있습니다. `UpdateWithTransaction`는 방금 추가한 것 이며 3 단계에서 추가 된 `DeleteProductsWithTransaction`입니다.

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample6.vb)]

> [!NOTE]
> 이러한 메서드는 ASP.NET pages 코드 기반 클래스에서 직접 이러한 메서드를 호출 하기 때문에 `ProductsBLL` 클래스의 대부분의 다른 메서드에 할당 된 `DataObjectMethodAttribute` 특성을 포함 하지 않습니다. `DataObjectMethodAttribute`은 ObjectDataSource의 데이터 원본 구성 마법사와 대상 탭 (SELECT, UPDATE, INSERT 또는 DELETE)에 표시 되어야 하는 메서드를 플래그 지정 하는 데 사용 됩니다. GridView에는 일괄 편집 또는 삭제에 대 한 기본 제공 지원이 없으므로 코드 없는 선언적 방법을 사용 하는 대신 프로그래밍 방식으로 이러한 메서드를 호출 해야 합니다.

## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>5 단계: 프레젠테이션 계층에서 데이터베이스 데이터를 원자 단위로 업데이트

레코드가 일괄 처리를 업데이트할 때 트랜잭션 효과를 보여 주기 위해에서 GridView의 모든 제품을 나열 하는 사용자 인터페이스를 만들고 클릭 하면 제품 `CategoryID` 값을 다시 할당 하는 단추 웹 컨트롤을 포함 합니다. 특히 처음 몇 개 제품에 유효한 `CategoryID` 값이 할당 되 고 다른 사용자에 게 존재 하지 않는 `CategoryID` 값이 할당 되도록 범주 재할당이 진행 됩니다. `CategoryID` 기존 범주 `CategoryID`와 일치 하지 않는 제품을 사용 하 여 데이터베이스를 업데이트 하려고 하면 foreign key 제약 조건 위반이 발생 하 고 예외가 발생 합니다. 이 예에서는 트랜잭션을 사용할 때 foreign key 제약 조건 위반으로 인해 발생 하는 예외가 발생 하면 이전의 유효한 `CategoryID` 변경 내용이 롤백됩니다. 그러나 트랜잭션을 사용 하지 않는 경우 초기 범주에 대 한 수정 사항은 그대로 유지 됩니다.

먼저 `BatchData` 폴더에서 `Transactions.aspx` 페이지를 열고 GridView를 도구 상자에서 디자이너로 끌어 옵니다. 해당 `ID` `Products`로 설정 하 고 스마트 태그에서 `ProductsDataSource`라는 새 ObjectDataSource에 바인딩합니다. `ProductsBLL` 클래스 s `GetProducts` 메서드에서 데이터를 가져오도록 ObjectDataSource를 구성 합니다. 이는 읽기 전용 GridView 이므로 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 하 고 마침을 클릭 합니다.

[ProductsBLL 클래스 s GetProducts 메서드를 사용 하도록 ObjectDataSource를 구성 ![](wrapping-database-modifications-within-a-transaction-vb/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image3.png)

**그림 5**: `ProductsBLL` 클래스 s `GetProducts` 메서드를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-vb/_static/image4.png))

[업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)으로 설정 ![](wrapping-database-modifications-within-a-transaction-vb/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image5.png)

**그림 6**: 업데이트, 삽입 및 삭제 탭의 드롭다운 목록을 (없음)로 설정 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-vb/_static/image6.png))

데이터 소스 구성 마법사를 완료 한 후에는 Visual Studio에서 제품 데이터 필드에 대 한 BoundFields 및 CheckBoxField를 만듭니다. `ProductID`, `ProductName`, `CategoryID`및 `CategoryName`를 제외 하 고 이러한 필드를 모두 제거 하 고 `ProductName` 및 `CategoryName` BoundFields `HeaderText` 속성의 이름을 각각 Product 및 Category로 바꿉니다. 스마트 태그에서 페이징 사용 옵션을 선택 합니다. 이러한 수정 작업을 수행한 후 GridView와 ObjectDataSource의 선언 태그는 다음과 같습니다.

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample7.aspx)]

다음으로 GridView 위에 세 개의 단추 웹 컨트롤을 추가 합니다. 첫 번째 단추의 Text 속성을 표 새로 고침으로 설정 하 고, 두 번째를 사용 하 여 범주를 수정 하 고 (트랜잭션 사용), 세 번째를 사용 하 여 범주를 수정 합니다 (트랜잭션 없음).

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample8.aspx)]

이 시점에서 Visual Studio의 디자인 뷰 그림 7에 표시 된 화면과 비슷해야 합니다.

[페이지 ![GridView 및 3 개의 단추 웹 컨트롤이 포함 되어 있습니다.](wrapping-database-modifications-within-a-transaction-vb/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image7.png)

**그림 7**: GridView 및 3 개의 단추 웹 컨트롤 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-vb/_static/image8.png))이 페이지에 포함 되어 있습니다.

세 개의 단추 s `Click` 이벤트에 대 한 이벤트 처리기를 만들고 다음 코드를 사용 합니다.

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample9.vb)]

Refresh 단추 `Click` 이벤트 처리기는 `Products` GridView s `DataBind` 메서드를 호출 하 여 단순히 데이터를 GridView에 다시 바인딩합니다.

두 번째 이벤트 처리기는 `CategoryID` s 제품을 다시 할당 하 고 BLL의 새 트랜잭션 메서드를 사용 하 여 트랜잭션 상위에서 데이터베이스 업데이트를 수행 합니다. 각 제품 `CategoryID`은 `ProductID`와 동일한 값으로 임의로 설정 됩니다. 이러한 제품은 유효한 `CategoryID`에 매핑하기 위해 발생 하는 `ProductID` 값을 가지 므로 처음 몇 개 제품에 대해 제대로 작동 합니다. 그러나 `ProductID` s가 너무 커지면 `ProductID` s와 `CategoryID`가 더 이상 적용 되지 않습니다.

세 번째 `Click` 이벤트 처리기는 동일한 방식으로 `CategoryID` s 제품을 업데이트 하지만 `ProductsTableAdapter`의 기본 `Update` 메서드를 사용 하 여 데이터베이스에 업데이트를 보냅니다. 이 `Update` 메서드는 트랜잭션 내에서 일련의 명령을 래핑하지 않으므로 처음에 발생 한 외래 키 제약 조건 위반 오류가 지속 되기 전에 이러한 변경 사항이 적용 됩니다.

이 동작을 시연 하려면 브라우저를 통해이 페이지를 방문 하세요. 처음에는 그림 8에 표시 된 것 처럼 데이터의 첫 페이지가 표시 됩니다. 다음으로, 범주 수정 (트랜잭션 포함) 단추를 클릭 합니다. 이렇게 하면 포스트백이 발생 하 고 모든 제품 `CategoryID` 값이 업데이트 되지만 foreign key 제약 조건 위반이 발생 합니다 (그림 9 참조).

[제품이 페이징할 수 있는 GridView에 표시 되는 ![](wrapping-database-modifications-within-a-transaction-vb/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image9.png)

**그림 8**: 제품이 페이징할 수 있는 GridView에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-vb/_static/image10.png)).

[범주를 다시 할당 ![Foreign Key 제약 조건 위반이 발생 합니다.](wrapping-database-modifications-within-a-transaction-vb/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image11.png)

**그림 9**: 범주를 다시 할당 하면 Foreign Key 제약 조건 위반이 발생 합니다 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-vb/_static/image12.png)).

이제 브라우저의 뒤로 단추를 누른 다음 표 형태 창 새로 고침 단추를 클릭 합니다. 데이터를 새로 고칠 때 그림 8에 표시 된 것과 정확히 동일한 출력이 표시 되어야 합니다. 즉, `CategoryID` s 제품 중 일부가 올바른 값으로 변경 되 고 데이터베이스에서 업데이트 되더라도 foreign key 제약 조건 위반이 발생 했을 때 롤백됩니다.

이제 수정 (트랜잭션 없음) 단추를 클릭 해 봅니다. 이렇게 하면 동일한 foreign key 제약 조건 위반 오류가 발생 합니다 (그림 9 참조). 그러나 이번에는 `CategoryID` 값이 올바른 값으로 변경 된 제품은 롤백되지 않습니다. 브라우저의 뒤로 단추와 표 새로 고침 단추를 누릅니다. 그림 10에 표시 된 것 처럼 처음 8 개 제품의 `CategoryID`는 다시 할당 됩니다. 예를 들어 그림 8에서 파일과는 1 `CategoryID` 했지만 그림 10에서는 2에 다시 할당 되었습니다.

[일부 제품 CategoryID 값이 업데이트 되었지만 다른 항목은 업데이트 되지 ![](wrapping-database-modifications-within-a-transaction-vb/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image13.png)

**그림 10**: 일부 제품 `CategoryID` 값이 업데이트 되지 않은 경우 ([전체 크기 이미지를 보려면 클릭](wrapping-database-modifications-within-a-transaction-vb/_static/image14.png))

## <a name="summary"></a>요약

기본적으로 TableAdapter의 메서드는 트랜잭션 범위 내에서 실행 된 데이터베이스 문을 래핑하지 않지만 약간의 작업을 통해 트랜잭션을 만들고 커밋하고 롤백하는 메서드를 추가할 수 있습니다. 이 자습서에서는 `ProductsTableAdapter` 클래스에서 `BeginTransaction`, `CommitTransaction`및 `RollbackTransaction`의 세 가지 메서드를 만들었습니다. 이러한 메서드를 `Try...Catch` 블록과 함께 사용 하 여 일련의 데이터 수정 문이 원자성을 만드는 방법을 살펴보았습니다. 특히 제공 된 `ProductsDataTable`의 행에 대해 필요한 수정 작업을 수행 하기 위해 Batch 업데이트 패턴을 사용 하는 `ProductsTableAdapter``UpdateWithTransaction` 메서드를 만들었습니다. 또한 `DeleteProductsWithTransaction` 메서드를 BLL의 `ProductsBLL` 클래스에 추가 했습니다 .이 클래스는 `ProductID` 값의 `List`을 입력으로 수락 하 고 각 `Delete`에 대해 DB 직접 패턴 메서드 `ProductID`를 호출 합니다. 두 메서드는 트랜잭션을 만든 다음 `Try...Catch` 블록 내에서 데이터 수정 문을 실행 하 여 시작 합니다. 예외가 발생 하는 경우 트랜잭션이 롤백되고 그렇지 않은 경우 커밋됩니다.

5 단계는 트랜잭션 일괄 처리 업데이트 및 트랜잭션 사용을 중단 하는 일괄 처리 업데이트의 영향을 보여 줍니다. 다음 세 가지 자습서에서는이 자습서의 기반을 바탕으로 구축 하 고 배치 업데이트, 삭제 및 삽입을 수행 하기 위한 사용자 인터페이스를 만듭니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [트랜잭션과 함께 데이터베이스 일관성 유지 관리](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [SQL Server 저장 프로시저의 트랜잭션 관리](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [쉽게 만든 트랜잭션: `System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [TransactionScope 및 Dataadapter](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [.NET에서 Oracle Database 트랜잭션 사용](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Dave Gardner, Hilton Gid Esenow 및 Teresa Murphy 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](batch-inserting-cs.md)
> [다음](batch-updating-vb.md)
