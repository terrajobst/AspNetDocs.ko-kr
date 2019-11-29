---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
title: 데이터 액세스 레이어의 연결 및 명령 수준 설정 구성 (VB) | Microsoft Docs
author: rick-anderson
description: 형식화 된 데이터 집합 내의 Tableadapter는 자동으로 데이터베이스에 연결 하 고, 명령을 실행 하 고, 결과를 사용 하 여 DataTable을 채웁니다.
ms.author: riande
ms.date: 08/03/2007
ms.assetid: d57dfa2b-d627-45cb-b5b1-abbf3159d770
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/configuring-the-data-access-layer-s-connection-and-command-level-settings-vb
msc.type: authoredcontent
ms.openlocfilehash: fa2868fc0dd8acd76f600b47d92adb984ce8d105
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74573646"
---
# <a name="configuring-the-data-access-layers-connection--and-command-level-settings-vb"></a>데이터 액세스 레이어의 연결 및 명령 수준 설정 구성(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_72_VB.zip) 또는 [PDF 다운로드](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/datatutorial72vb1.pdf)

> 형식화 된 데이터 집합 내의 Tableadapter는 데이터베이스에 연결 하 고 명령을 실행 하며 결과를 사용 하 여 DataTable을 채우는 데 자동으로 처리 합니다. 이러한 세부 정보를 직접 처리 하고자 하는 경우가 있으며,이 자습서에서는 TableAdapter의 데이터베이스 연결 및 명령 수준 설정에 액세스 하는 방법을 알아봅니다.

## <a name="introduction"></a>소개

자습서 시리즈 전체에서 형식화 된 데이터 집합을 사용 하 여 계층화 된 아키텍처의 데이터 액세스 계층 및 비즈니스 개체를 구현 했습니다. [첫 번째 자습서](../introduction/creating-a-data-access-layer-vb.md)에서 설명한 대로 형식화 된 데이터 집합 s datatable는 데이터 리포지토리로 사용 되는 반면 tableadapter는 기본 데이터를 검색 하 고 수정 하기 위해 데이터베이스와 통신 하는 래퍼로 동작 합니다. Tableadapter는 데이터베이스 작업과 관련 된 복잡성을 캡슐화 하 고 데이터베이스에 연결 하거나, 명령을 실행 하거나, 결과를 DataTable로 채우는 코드를 작성할 필요가 없습니다.

그러나 TableAdapter의 깊이를 파악 하 고 ADO.NET 개체와 직접 작동 하는 코드를 작성 해야 하는 경우가 있습니다. 예를 들어 [트랜잭션 내에서 데이터베이스 수정 내용 래핑](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) 자습서에서 ADO.NET 트랜잭션을 시작, 커밋 및 롤백하는 메서드를 TableAdapter에 추가 했습니다. 이러한 메서드는 TableAdapter s `SqlCommand` 개체에 할당 된, 수동으로 만든 내부 `SqlTransaction` 개체를 사용 했습니다.

이 자습서에서는 TableAdapter의 데이터베이스 연결 및 명령 수준 설정에 액세스 하는 방법을 살펴봅니다. 특히 기본 연결 문자열과 명령 제한 시간 설정에 액세스할 수 있도록 하는 `ProductsTableAdapter`에 기능을 추가 합니다.

## <a name="working-with-data-using-adonet"></a>ADO.NET를 사용 하 여 데이터 작업

Microsoft .NET 프레임 워크에는 데이터 작업을 위해 특별히 디자인 된 클래스의 다양 한 포함 되어 있습니다. [`System.Data` 네임 스페이스](https://msdn.microsoft.com/library/system.data.aspx)내에 있는 이러한 클래스를 *ADO.NET* 클래스 라고 합니다. ADO.NET 파라솔 아래의 일부 클래스는 특정 *데이터 공급자*에 연결 됩니다. 데이터 공급자는 ADO.NET 클래스와 기본 데이터 저장소 간에 정보를 전달할 수 있도록 하는 통신 채널 이라고 생각할 수 있습니다. 특정 데이터베이스 시스템용으로 특별히 설계 된 공급자는 물론 OleDb 및 ODBC와 같은 일반화 된 공급자가 있습니다. 예를 들어 OleDb 공급자를 사용 하 여 Microsoft SQL Server 데이터베이스에 연결할 수 있지만 SqlClient 공급자는 SQL Server에 맞게 설계 되 고 최적화 되었기 때문에 훨씬 더 효율적입니다.

프로그래밍 방식으로 데이터에 액세스 하는 경우 일반적으로 다음 패턴이 사용 됩니다.

1. 데이터베이스에 대 한 연결을 설정 합니다.
2. 명령을 실행 합니다.
3. `SELECT` 쿼리의 경우 결과 레코드를 사용 합니다.

이러한 각 단계를 수행 하기 위한 별도의 ADO.NET 클래스가 있습니다. 예를 들어 SqlClient 공급자를 사용 하 여 데이터베이스에 연결 하려면 [`SqlConnection` 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection(VS.80).aspx)를 사용 합니다. 데이터베이스에 대 한 `INSERT`, `UPDATE`, `DELETE`또는 `SELECT` 명령을 실행 하려면 [`SqlCommand` 클래스](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.aspx)를 사용 합니다.

트랜잭션 자습서에 포함 된 [데이터베이스를 래핑하](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) 는 경우를 제외 하 고, tableadapter 자동 생성 코드는 데이터베이스에 연결 하 고, 명령을 실행 하 고, 데이터를 검색 하 고, 데이터를 datatable로 채우는 데 필요한 기능을 포함 하기 때문에 하위 수준 ADO.NET 코드를 작성 하지 않아도 됩니다. 그러나 이러한 하위 수준 설정을 사용자 지정 해야 하는 경우가 있을 수 있습니다. 다음 몇 단계에서 Tableadapter에 의해 내부적으로 사용 되는 ADO.NET 개체를 탭 하는 방법을 살펴보겠습니다.

## <a name="step-1-examining-with-the-connection-property"></a>1 단계: 연결 속성을 사용 하 여 검사

각 TableAdapter 클래스에는 데이터베이스 연결 정보를 지정 하는 `Connection` 속성이 있습니다. 이 속성의 데이터 형식 및 `ConnectionString` 값은 TableAdapter 구성 마법사에서 선택한 항목에 따라 결정 됩니다. 형식화 된 데이터 집합에 TableAdapter를 처음 추가할 때이 마법사는 데이터베이스 원본을 묻는 메시지를 표시 합니다 (그림 1 참조). 이 첫 번째 단계의 드롭다운 목록에는 구성 파일에 지정 된 데이터베이스와 서버 탐색기 s 데이터 연결의 다른 데이터베이스가 포함 됩니다. 사용 하려는 데이터베이스가 드롭다운 목록에 없는 경우 새 연결 단추를 클릭 하 고 필요한 연결 정보를 제공 하 여 새 데이터베이스 연결을 지정할 수 있습니다.

[TableAdapter 구성 마법사의 첫 번째 단계 ![](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image2.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image1.png)

**그림 1**: TableAdapter 구성 마법사의 첫 번째 단계 ([전체 크기 이미지를 보려면 클릭](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image3.png))

를 사용 하 여 TableAdapter `Connection` 속성에 대 한 코드를 검사 합니다. [데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서에 설명 된 대로 클래스 뷰 창으로 이동 하 여 적절 한 클래스로 드릴 다운 한 다음 멤버 이름을 두 번 클릭 하 여 자동 생성 된 TableAdapter 코드를 볼 수 있습니다.

보기 메뉴로 이동 하 여 클래스 뷰를 선택 하거나 Ctrl + Shift + C를 입력 하 여 클래스 뷰 창으로 이동 합니다. 클래스 뷰 창의 위쪽 절반에서 `NorthwindTableAdapters` 네임 스페이스로 드릴 다운 하 고 `ProductsTableAdapter` 클래스를 선택 합니다. 그러면 그림 2에 표시 된 것 처럼 클래스 뷰의 하단에 `ProductsTableAdapter` s 멤버가 표시 됩니다. `Connection` 속성을 두 번 클릭 하 여 해당 코드를 확인 합니다.

![자동 생성 된 코드를 보려면 클래스 뷰의 연결 속성을 두 번 클릭 합니다.](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image4.png)

**그림 2**: 자동 생성 된 코드를 보려면 클래스 뷰에서 연결 속성을 두 번 클릭 합니다.

TableAdapter s `Connection` 속성 및 기타 연결 관련 코드는 다음과 같습니다.

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample1.vb)]

TableAdapter 클래스를 인스턴스화하면 멤버 변수 `_connection` `Nothing`와 같습니다. `Connection` 속성에 액세스 하면 먼저 `_connection` 멤버 변수가 인스턴스화 되었는지 확인 합니다. 그렇지 않은 경우 `_connection`을 인스턴스화하고 `ConnectionString` 속성을 TableAdapter 구성 마법사의 첫 번째 단계에서 지정한 연결 문자열 값으로 설정 하는 `InitConnection` 메서드가 호출 됩니다.

`Connection` 속성은 `SqlConnection` 개체에 할당 될 수도 있습니다. 이렇게 하면 새 `SqlConnection` 개체가 각 TableAdapter s `SqlCommand` 개체와 연결 됩니다.

## <a name="step-2-exposing-connection-level-settings"></a>2 단계: 연결 수준 설정 노출

연결 정보는 TableAdapter 내에서 캡슐화 된 상태로 유지 되 고 응용 프로그램 아키텍처의 다른 계층에서는 액세스할 수 없습니다. 그러나 쿼리, 사용자 또는 ASP.NET 페이지에서 TableAdapter s 연결 수준 정보에 액세스 하거나 사용자 지정할 수 있어야 하는 시나리오가 있을 수 있습니다.

`Northwind` 데이터 집합의 `ProductsTableAdapter`을 확장 하 여 비즈니스 논리 계층에서 TableAdapter에 사용 되는 연결 문자열을 읽거나 변경 하는 데 사용할 수 있는 `ConnectionString` 속성을 포함 하도록 합니다.

> [!NOTE]
> *연결 문자열* 은 사용할 공급자, 데이터베이스 위치, 인증 자격 증명 및 기타 데이터베이스 관련 설정과 같은 데이터베이스 연결 정보를 지정 하는 문자열입니다. 다양 한 데이터 저장소 및 공급자에서 사용 하는 연결 문자열 패턴의 목록은 [ConnectionStrings.com](http://www.connectionstrings.com/)를 참조 하세요.

[데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서에 설명 된 대로 형식화 된 데이터 집합의 자동 생성 클래스는 partial 클래스를 사용 하 여 확장할 수 있습니다. 먼저 `~/App_Code/DAL` 폴더 아래에 `ConnectionAndCommandSettings` 라는 프로젝트에 새 하위 폴더를 만듭니다.

![ConnectionAndCommandSettings 라는 하위 폴더를 추가 합니다.](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image5.png)

**그림 3**: 이름이 `ConnectionAndCommandSettings` 하위 폴더 추가

`ProductsTableAdapter.ConnectionAndCommandSettings.vb` 이라는 새 클래스 파일을 추가 하 고 다음 코드를 입력 합니다.

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample2.vb)]

이 partial 클래스는 `ConnectionString` 이라는 `Public` 속성을 `ProductsTableAdapter` 클래스에 추가 하 여 모든 계층에서 TableAdapter의 기본 연결에 대 한 연결 문자열을 읽거나 업데이트할 수 있도록 합니다.

이 partial 클래스를 만들고 저장 한 다음 `ProductsBLL` 클래스를 엽니다. 기존 메서드 중 하나로 이동 하 고 `Adapter` 입력 한 다음 period 키를 눌러 IntelliSense를 표시 합니다. IntelliSense에서 사용할 수 있는 새 `ConnectionString` 속성이 표시 되어야 합니다. 즉, BLL에서이 값을 프로그래밍 방식으로 읽거나 조정할 수 있습니다.

## <a name="exposing-the-entire-connection-object"></a>전체 연결 개체 노출

이 partial 클래스는 기본 연결 개체인 `ConnectionString`의 속성을 하나만 노출 합니다. 전체 연결 개체를 TableAdapter의 범위를 넘어 사용할 수 있도록 하려는 경우에는 `Connection` 속성의 보호 수준을 변경할 수 있습니다. 1 단계에서 검사 한 자동 생성 코드는 TableAdapter s `Connection` 속성이 `Friend`으로 표시 되었음을 보여 줍니다. 즉, 동일한 어셈블리의 클래스 에서만 액세스할 수 있습니다. 그러나 TableAdapter s `ConnectionModifier` 속성을 통해 변경할 수 있습니다.

`Northwind` 데이터 집합을 열고 디자이너에서 `ProductsTableAdapter`를 클릭 한 다음 속성 창으로 이동 합니다. `ConnectionModifier` 설정 된 기본값 (`Assembly`)이 표시 됩니다. `Connection` 속성을 형식화 된 데이터 집합의 어셈블리 외부에서 사용할 수 있도록 하려면 `ConnectionModifier` 속성을 `Public`로 변경 합니다.

[연결 속성 s 액세스 가능성 수준은 ConnectionModifier 속성을 통해 구성할 수 ![.](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image7.png)](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image6.png)

**그림 4**: `ConnectionModifier` 속성을 통해 `Connection` 속성의 접근성 수준을 구성할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/_static/image8.png)).

데이터 집합을 저장 한 다음 `ProductsBLL` 클래스로 돌아갑니다. 이전 처럼 기존 메서드 중 하나로 이동 하 고 `Adapter` 입력 한 다음 period 키를 눌러 IntelliSense를 표시 합니다. 이 목록에는 `Connection` 속성이 포함 되어야 합니다. 즉, 이제 BLL에서 연결 수준 설정을 프로그래밍 방식으로 읽거나 할당할 수 있습니다.

## <a name="step-3-examining-the-command-related-properties"></a>3 단계: 명령 관련 속성 검사

TableAdapter는 기본적으로 자동 생성 된 `INSERT`, `UPDATE`및 `DELETE` 문을 포함 하는 주 쿼리로 구성 됩니다. 이 주 쿼리 `INSERT`, `UPDATE`및 `DELETE` 문은 TableAdapter s 코드에서 `Adapter` 속성을 통해 ADO.NET 데이터 어댑터 개체로 구현 됩니다. `Connection` 속성과 마찬가지로 `Adapter` 속성의 데이터 형식은 사용 된 데이터 공급자에 의해 결정 됩니다. 이러한 자습서에서는 SqlClient 공급자를 사용 하므로 `Adapter` 속성은 [`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter(VS.80).aspx)유형입니다.

TableAdapter s `Adapter` 속성에는 `INSERT`, `UPDATE`및 `DELETE` 문을 실행 하는 데 사용 하는 `SqlCommand` 형식의 세 가지 속성이 있습니다.

- `InsertCommand`
- `UpdateCommand`
- `DeleteCommand`

`SqlCommand` 개체는 데이터베이스에 특정 쿼리를 전송 하는 작업을 담당 하며 실행할 임시 SQL 문이나 저장 프로시저를 포함 하는 [`CommandText`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtext.aspx)와 같은 속성을 포함 합니다. 및 [`Parameters`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.parameters.aspx)`SqlParameter` 개체의 컬렉션입니다. [데이터 액세스 계층 만들기](../introduction/creating-a-data-access-layer-vb.md) 자습서에서 보았듯이 이러한 명령 개체는 속성 창를 통해 사용자 지정할 수 있습니다.

TableAdapter에는 주 쿼리 외에도 호출 시 데이터베이스에 지정 된 명령을 디스패치할 수 있는 여러 메서드가 포함 될 수 있습니다. 주 쿼리의 command 개체와 모든 추가 메서드에 대 한 명령 개체는 TableAdapter s `CommandCollection` 속성에 저장 됩니다.

를 사용 하 여 이러한 두 속성과 지원 멤버 변수 및 도우미 메서드에 대 한 `Northwind` 데이터 집합의 `ProductsTableAdapter`에서 생성 된 코드를 살펴보겠습니다.

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample3.vb)]

`Adapter` 및 `CommandCollection` 속성에 대 한 코드는 `Connection` 속성의 코드와 긴밀 하 게 유사 합니다. 속성에서 사용 하는 개체를 보유 하는 멤버 변수가 있습니다. 속성 `Get` 접근자는 해당 멤버 변수가 `Nothing`되었는지 확인 하 여 시작 합니다. 이 경우 멤버 변수의 인스턴스를 만들고 핵심 명령 관련 속성을 할당 하는 초기화 메서드가 호출 됩니다.

## <a name="step-4-exposing-command-level-settings"></a>4 단계: 명령 수준 설정 노출

명령 수준 정보는 데이터 액세스 계층 내에서 캡슐화 된 상태로 유지 되는 것이 가장 좋습니다. 이 정보는 아키텍처의 다른 계층에서 필요 하지만, 연결 수준 설정과 마찬가지로 partial 클래스를 통해 노출 될 수 있습니다.

TableAdapter에는 단일 `Connection` 속성만 있으므로 연결 수준 설정을 노출 하는 코드는 매우 간단 합니다. TableAdapter에는 `InsertCommand`, `UpdateCommand`및 `DeleteCommand`와 `CommandCollection` 속성의 여러 명령 개체를 포함 하 여 여러 명령 개체를 포함할 수 있기 때문에 명령 수준 설정을 수정할 때 약간 더 복잡 합니다. 명령 수준 설정을 업데이트 하는 경우 이러한 설정을 모든 명령 개체에 전파 해야 합니다.

예를 들어 TableAdapter에 실행 하는 데 매우 긴 시간이 소요 된 특정 쿼리가 있다고 가정 합니다. TableAdapter를 사용 하 여 이러한 쿼리 중 하나를 실행 하는 경우 명령 개체 [`CommandTimeout` 속성](https://msdn.microsoft.com/library/system.data.sqlclient.sqlcommand.commandtimeout.aspx)을 늘릴 수 있습니다. 이 속성은 명령이 실행 될 때까지 대기 하는 시간 (초)을 지정 하 고 기본값은 30입니다.

`CommandTimeout` 속성이 BLL에 의해 조정 될 수 있도록 하려면 2 단계에서 만든 partial 클래스 파일 (`ProductsTableAdapter.ConnectionAndCommandSettings.vb`)을 사용 하 여 `ProductsDataTable`에 다음 `Public` 메서드를 추가 합니다.

[!code-vb[Main](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb/samples/sample4.vb)]

이 메서드는 해당 TableAdapter 인스턴스의 모든 명령에 대 한 명령 제한 시간을 설정 하기 위해 BLL 또는 프레젠테이션 계층에서 호출 될 수 있습니다.

> [!NOTE]
> `Adapter` 및 `CommandCollection` 속성은 `Private`로 표시 됩니다. 즉, TableAdapter 내의 코드 에서만 액세스할 수 있습니다. `Connection` 속성과 달리 이러한 액세스 한정자는 구성할 수 없습니다. 따라서 아키텍처의 다른 계층에 명령 수준 속성을 노출 해야 하는 경우 위에 설명 된 부분 클래스 방식을 사용 하 여 `Private` 명령 개체를 읽거나 쓰는 `Public` 메서드나 속성을 제공 해야 합니다.

## <a name="summary"></a>요약

형식화 된 데이터 집합 내의 Tableadapter는 데이터 액세스 세부 정보 및 복잡성을 캡슐화 하는 데 사용 됩니다. Tableadapter를 사용 하 여 데이터베이스에 연결 하거나, 명령을 실행 하거나, 결과를 DataTable로 채우는 ADO.NET 코드를 작성 하는 것에 대해 걱정할 필요가 없습니다. 모든 것이 자동으로 처리 됩니다.

그러나 연결 문자열 또는 기본 연결 또는 명령 제한 시간 값을 변경 하는 것과 같은 하위 수준 ADO.NET 특성을 사용자 지정 해야 하는 경우가 있을 수 있습니다. TableAdapter에는 자동으로 생성 된 `Connection`, `Adapter`및 `CommandCollection` 속성이 있지만 기본적으로 `Friend` 또는 `Private`입니다. Partial 클래스를 사용 하 여 `Public` 메서드 또는 속성을 포함 하는 TableAdapter를 확장 하 여이 내부 정보를 노출할 수 있습니다. 또는 tableadapter s `Connection` 속성 액세스 한정자를 TableAdapter s `ConnectionModifier` 속성을 통해 구성할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Burnadette Leigh, S ren Jacob Lauritsen, Teresa Murphy 및 Hilton Geisenow 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](working-with-computed-columns-vb.md)
> [다음](protecting-connection-strings-and-other-configuration-information-vb.md)
