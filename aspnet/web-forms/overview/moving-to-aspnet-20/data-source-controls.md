---
uid: web-forms/overview/moving-to-aspnet-20/data-source-controls
title: 데이터 원본 제어 | Microsoft Docs
author: microsoft
description: ASP.NET 1.x의 DataGrid 컨트롤은 웹 응용 프로그램에서 데이터 액세스의 향상 된 기능을 잘 표시 했습니다. 그러나 사용자에 게 친숙 한 것은 아닙니다.
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 78fd0e92-f9c6-4e96-a5e9-0375b307a828
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-source-controls
msc.type: authoredcontent
ms.openlocfilehash: a2e2cfbec3e5aebf42a2de30bab7d45b4b610298
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519353"
---
# <a name="data-source-controls"></a>데이터 소스 제어

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET 1.x의 DataGrid 컨트롤은 웹 응용 프로그램에서 데이터 액세스의 향상 된 기능을 잘 표시 했습니다. 그러나 사용자에 게 친숙 한 것은 아닙니다. 매우 유용한 기능을 얻기 위해서는 여전히 상당한 양의 코드가 필요 합니다. 이는 시도한의 모든 데이터 액세스에 대 한 모델입니다.

ASP.NET 1.x의 DataGrid 컨트롤은 웹 응용 프로그램에서 데이터 액세스의 향상 된 기능을 잘 표시 했습니다. 그러나 사용자에 게 친숙 한 것은 아닙니다. 매우 유용한 기능을 얻기 위해서는 여전히 상당한 양의 코드가 필요 합니다. 이는 시도한의 모든 데이터 액세스에 대 한 모델입니다.

ASP.NET 2.0는 데이터 소스 제어를 포함 하 여이를로 처리 합니다. ASP.NET 2.0의 데이터 소스 컨트롤을 사용 하면 개발자가 데이터를 검색 하 고, 데이터를 표시 하 고, 데이터를 편집 하기 위한 선언적 모델을 제공할 것입니다. 데이터 소스 컨트롤의 목적은 데이터의 소스에 관계 없이 데이터 바인딩된 컨트롤에 일관 된 데이터 표현을 제공 하는 것입니다. ASP.NET 2.0에서 데이터 소스 컨트롤의 핵심은 DataSourceControl abstract 클래스입니다. DataSourceControl 클래스는 IDataSource 인터페이스와 IListSource 인터페이스의 기본 구현을 제공 하 고, 후자를 사용 하면 데이터 소스 컨트롤을 데이터 바인딩된 컨트롤의 데이터 원본으로 할당할 수 있습니다 (새로운 DataSourceId 속성을 통해). 나중에 설명) 하 고 목록으로 데이터를 노출 합니다. 데이터 소스 컨트롤의 각 데이터 목록은 DataSourceView 개체로 노출 됩니다. DataSourceView 인스턴스에 대 한 액세스는 IDataSource 인터페이스에 의해 제공 됩니다. 예를 들어 GetViewNames 메서드는 특정 데이터 소스 컨트롤과 연결 된 DataSourceViews를 열거 하는 데 사용할 수 있는 ICollection을 반환 하 고, GetView 메서드를 사용 하면 이름별로 특정 DataSourceView 인스턴스에 액세스할 수 있습니다.

데이터 소스 컨트롤에는 사용자 인터페이스가 없습니다. 이러한 구문은 선언 구문을 지원 하 고 원하는 경우 페이지 상태에 액세스할 수 있도록 서버 컨트롤로 구현 됩니다. 데이터 소스 컨트롤은 HTML 태그를 클라이언트에 렌더링 하지 않습니다.

> [!NOTE]
> 나중에 볼 수 있듯이 데이터 소스 컨트롤을 사용 하 여 얻을 수 있는 캐싱 이점도 있습니다.

## <a name="storing-connection-strings"></a>연결 문자열 저장

데이터 원본 제어를 구성 하는 방법에 대 한 자세한 내용은 ASP.NET 2.0의 연결 문자열과 관련 된 새로운 기능을 포함 해야 합니다. ASP.NET 2.0에는 런타임에 동적으로 읽을 수 있는 연결 문자열을 쉽게 저장할 수 있도록 하는 새 섹션이 구성 파일에 도입 되었습니다. &lt;connectionStrings&gt; 섹션을 사용 하 여 연결 문자열을 쉽게 저장할 수 있습니다.

아래 코드 조각은 새 연결 문자열을 추가 합니다.

[!code-xml[Main](data-source-controls/samples/sample1.xml)]

> [!NOTE]
> &lt;appSettings&gt; 섹션과 마찬가지로 &lt;connectionStrings&gt; 섹션은 구성 파일의 &lt;system.web&gt; 섹션 외부에 표시 됩니다.

이 연결 문자열을 사용 하려면 서버 컨트롤의 ConnectionString 특성을 설정할 때 다음 구문을 사용할 수 있습니다.

[!code-aspx[Main](data-source-controls/samples/sample2.aspx)]

&lt;connectionStrings&gt; 섹션을 암호화 하 여 중요 한 정보가 노출 되지 않도록 할 수도 있습니다. 이 기능은 이후 모듈에서 다룰 예정입니다.

## <a name="caching-data-sources"></a>데이터 원본 캐싱

각 DataSourceControl는 캐싱을 구성 하기 위한 네 가지 속성을 제공 합니다. EnableCaching, CacheDuration, CacheExpirationPolicy 및 CacheKeyDependency.

## <a name="enablecaching"></a>EnableCaching

EnableCaching는 데이터 소스 컨트롤에 캐싱을 사용할 수 있는지 여부를 결정 하는 부울 속성입니다.

## <a name="cacheduration-property"></a>CacheDuration 속성

CacheDuration 속성은 캐시가 유효한 상태로 유지 되는 시간 (초)을 설정 합니다. 이 속성을 **0** 으로 설정 하면 명시적으로 무효화 될 때까지 캐시가 유효 하 게 유지 됩니다.

## <a name="cacheexpirationpolicy-property"></a>CacheExpirationPolicy 속성

CacheExpirationPolicy 속성은 **절대** 또는 **슬라이딩**로 설정할 수 있습니다. 이 값을 Absolute로 설정 하면 데이터가 캐시 되는 최대 시간이 CacheDuration 속성에서 지정한 시간 (초)입니다. 이를 슬라이딩로 설정 하면 각 작업이 수행 될 때 만료 시간이 다시 설정 됩니다.

## <a name="cachekeydependency-property"></a>CacheKeyDependency 속성

CacheKeyDependency 속성에 문자열 값이 지정 된 경우 ASP.NET는 해당 문자열을 기반으로 새 캐시 종속성을 설정 합니다. 이렇게 하면 CacheKeyDependency를 변경 하거나 제거 하 여 명시적으로 캐시를 무효화할 수 있습니다.

**중요**: 가장을 사용 하 고 데이터 원본 및/또는 데이터 내용에 대 한 액세스가 클라이언트 id를 기반으로 하는 경우 EnableCaching을 False로 설정 하 여 캐싱을 사용 하지 않도록 설정 하는 것이 좋습니다. 이 시나리오에서 캐싱이 사용 되 고 원래 데이터를 요청한 사용자 이외의 사용자가 요청을 실행 한 경우 데이터 원본에 대 한 권한 부여는 적용 되지 않습니다. 데이터는 단지 캐시에서 제공 됩니다.

## <a name="the-sqldatasource-control"></a>SqlDataSource 컨트롤

SqlDataSource 컨트롤을 사용 하면 개발자가 ADO.NET를 지 원하는 모든 관계형 데이터베이스에 저장 된 데이터에 액세스할 수 있습니다. 이 클래스는 OracleClient 공급자를 사용 하 여 Oracle에 액세스 하는 SQL Server 데이터베이스, System.web 공급자, system.xml 공급자 또는 공급자에 액세스할 수 있습니다. 따라서 SqlDataSource는 SQL Server 데이터베이스의 데이터에 액세스 하는 경우에만 사용 됩니다.

SqlDataSource를 사용 하기 위해 ConnectionString 속성에 대 한 값을 제공 하 고 SQL 명령 또는 저장 프로시저를 지정 하면 됩니다. SqlDataSource 컨트롤은 기본 ADO.NET 아키텍처 작업을 담당 합니다. 연결을 열고, 데이터 원본을 쿼리하거나, 저장 프로시저를 실행 하 고, 데이터를 반환한 다음, 연결을 닫습니다.

> [!NOTE]
> DataSourceControl 클래스는 자동으로 연결을 종료 하기 때문에 데이터베이스 연결을 누출 하 여 생성 되는 고객 호출 수를 줄여야 합니다.

아래 코드 조각에서는 위에 표시 된 것 처럼 구성 파일에 저장 된 연결 문자열을 사용 하 여 SqlDataSource 컨트롤에 DropDownList 컨트롤을 바인딩합니다.

[!code-aspx[Main](data-source-controls/samples/sample3.aspx)]

위에서 설명한 것 처럼 SqlDataSource의 DataSourceMode 속성은 데이터 원본에 대 한 모드를 지정 합니다. 위의 예제에서 DataSourceMode는 DataReader로 설정 됩니다. 이 경우 SqlDataSource는 앞 으로만 이동 가능한 읽기 전용 커서를 사용 하 여 IDataReader 개체를 반환 합니다. 반환 된 개체의 지정 된 형식은 사용 되는 공급자에 의해 제어 됩니다. 이 경우 web.config 파일의 &lt;connectionStrings&gt; 섹션에 지정 된 대로 System.object 공급자를 사용 합니다. 따라서 반환 되는 개체는 SqlDataReader 형식이 됩니다. 데이터 집합의 DataSourceMode 값을 지정 하 여 데이터를 서버의 데이터 집합에 저장할 수 있습니다. 이 모드를 사용 하 여 정렬, 페이징 등의 기능을 추가할 수 있습니다. SqlDataSource를 GridView 컨트롤에 데이터 바인딩하는 경우 데이터 집합 모드를 선택 했습니다. 그러나 DropDownList의 경우 DataReader 모드를 선택 하는 것이 적절 합니다.

> [!NOTE]
> SqlDataSource 또는 AccessDataSource를 캐시 하는 경우 DataSourceMode 속성을 DataSet으로 설정 해야 합니다. DataReader DataSourceMode를 사용 하 여 캐싱을 사용 하도록 설정 하면 예외가 발생 합니다.

## <a name="sqldatasource-properties"></a>SqlDataSource 속성

SqlDataSource 컨트롤의 일부 속성은 다음과 같습니다.

### <a name="cancelselectonnullparameter"></a>CancelSelectOnNullParameter

매개 변수 중 하나가 null 인 경우 select 명령이 취소 되는지 여부를 지정 하는 부울 값입니다. 기본적으로 true입니다.

### <a name="conflictdetection"></a>ConflictDetection

여러 사용자가 동시에 데이터 원본을 업데이트할 수 있는 경우 ConflictDetection 속성은 SqlDataSource 컨트롤의 동작을 결정 합니다. 이 속성은 ConflictOptions 열거형의 값 중 하나로 계산 됩니다. 이러한 값은 **Compareallvalues** 및 **OverwriteChanges**입니다. OverwriteChanges로 설정 되 면 데이터 원본에 데이터를 쓰는 마지막 사람이 이전 변경 내용을 덮어씁니다. 그러나 ConflictDetection 속성이 CompareAllValues로 설정 된 경우 SelectCommand 및 매개 변수에 의해 반환 되는 열에 대해 생성 된 매개 변수도 생성 되어 해당 열 각각의 원래 값을 유지 합니다. SelectCommand가 실행 된 이후 값이 변경 되었는지 여부를 확인 합니다.

### <a name="deletecommand"></a>DeleteCommand

데이터베이스에서 행을 삭제할 때 사용 되는 SQL 문자열을 설정 하거나 가져옵니다. SQL 쿼리 또는 저장 프로시저 이름일 수 있습니다.

### <a name="deletecommandtype"></a>DeleteCommandType

SQL 쿼리 (텍스트) 또는 저장 프로시저 (StoredProcedure)와 같은 delete 명령 유형을 설정 하거나 가져옵니다.

### <a name="deleteparameters"></a>DeleteParameters

SqlDataSource 컨트롤과 연결 된 SqlDataSourceView 개체의 DeleteCommand에 사용 되는 매개 변수를 반환 합니다.

### <a name="oldvaluesparameterformatstring"></a>OldValuesParameterFormatString

이 속성은 ConflictDetection 속성이 CompareAllValues로 설정 된 경우 원래 값 매개 변수의 형식을 지정 하는 데 사용 됩니다. 기본값은 {0} 원래 값 매개 변수가 원래 매개 변수와 동일한 이름을 사용 함을 의미 하는입니다. 즉, 필드 이름이 EmployeeID 인 경우 원래 값 매개 변수는 @EmployeeID됩니다.

### <a name="selectcommand"></a>SelectCommand

데이터베이스에서 데이터를 검색 하는 데 사용 되는 SQL 문자열을 설정 하거나 가져옵니다. SQL 쿼리 또는 저장 프로시저 이름일 수 있습니다.

### <a name="selectcommandtype"></a>SelectCommandType

Select 명령의 유형 (SQL 쿼리 (텍스트) 또는 저장 프로시저 (StoredProcedure))을 설정 하거나 가져옵니다.

### <a name="selectparameters"></a>SelectParameters

SqlDataSource 컨트롤과 연결 된 SqlDataSourceView 개체의 SelectCommand에서 사용 되는 매개 변수를 반환 합니다.

### <a name="sortparametername"></a>SortParameterName

데이터 소스 컨트롤에서 검색 한 데이터를 정렬할 때 사용 되는 저장 프로시저 매개 변수의 이름을 가져오거나 설정 합니다. SelectCommandType이 StoredProcedure로 설정 된 경우에만 유효 합니다.

### <a name="sqlcachedependency"></a>SqlCacheDependency

SQL Server cache 종속성에 사용 되는 데이터베이스 및 테이블을 지정 하는 세미콜론으로 구분 된 문자열입니다. SQL 캐시 종속성은 이후 모듈에서 설명 합니다.

### <a name="updatecommand"></a>UpdateCommand

데이터베이스의 데이터를 업데이트할 때 사용 되는 SQL 문자열을 설정 하거나 가져옵니다. SQL 쿼리 또는 저장 프로시저 이름일 수 있습니다.

### <a name="updatecommandtype"></a>UpdateCommandType

SQL 쿼리 (텍스트) 또는 저장 프로시저 (StoredProcedure)와 같은 update 명령 유형을 설정 하거나 가져옵니다.

### <a name="updateparameters"></a>UpdateParameters

SqlDataSource 컨트롤과 연결 된 SqlDataSourceView 개체를 UpdateCommand에서 사용 하는 매개 변수를 반환 합니다.

## <a name="the-accessdatasource-control"></a>AccessDataSource 컨트롤

AccessDataSource 컨트롤은 SqlDataSource 클래스에서 파생 되며 Microsoft Access 데이터베이스에 데이터 바인딩하는 데 사용 됩니다. AccessDataSource 컨트롤에 대 한 ConnectionString 속성은 읽기 전용 속성입니다. ConnectionString 속성을 사용 하는 대신 데이터 데이터 속성은 아래와 같이 Access 데이터베이스를 가리키는 데 사용 됩니다.

[!code-aspx[Main](data-source-controls/samples/sample4.aspx)]

AccessDataSource는 항상 기본 SqlDataSource의 ProviderName을 system.xml로 설정 하 고 Microsoft. j s. 4.0 OLE DB 공급자를 사용 하 여 데이터베이스에 연결 합니다. AccessDataSource 컨트롤을 사용 하 여 암호로 보호 된 Access 데이터베이스에 연결할 수 없습니다. 암호로 보호 된 데이터베이스에 연결 해야 하는 경우 SqlDataSource 컨트롤을 사용 해야 합니다.

> [!NOTE]
> 웹 사이트에 저장 된 Access 데이터베이스는 App\_Data 디렉터리에 배치 해야 합니다. ASP.NET는이 디렉터리의 파일을 검색할 수 없습니다. Access 데이터베이스를 사용할 때 process 계정에 앱\_데이터 디렉터리에 대 한 읽기 및 쓰기 권한을 부여 해야 합니다.

## <a name="the-xmldatasource-control"></a>XmlDataSource 컨트롤

XmlDataSource는 XML 데이터를 데이터 바인딩된 컨트롤에 데이터 바인딩하는 데 사용 됩니다. 데이터 파일 속성을 사용 하 여 XML 파일에 바인딩하거나 데이터 속성을 사용 하 여 XML 문자열에 바인딩할 수 있습니다. XmlDataSource는 XML 특성을 바인딩 가능한 필드로 노출 합니다. 특성으로 표시 되지 않은 값에 바인딩해야 하는 경우에는 XSL 변환을 사용 해야 합니다. XPath 식을 사용 하 여 XML 데이터를 필터링 할 수도 있습니다.

다음 XML 파일을 고려 하십시오.

[!code-xml[Main](data-source-controls/samples/sample5.xml)]

XmlDataSource는 *사용자/사람의* XPath 속성을 사용 하 여 &lt;Person&gt; 노드만 필터링 합니다. 그러면 DropDownList은 DataTextField 속성을 사용 하 여 LastName 특성에 데이터를 바인딩합니다.

XmlDataSource 컨트롤은 주로 읽기 전용 XML 데이터에 데이터 바인딩하는 데 사용 되지만 XML 데이터 파일을 편집할 수 있습니다. 이러한 경우 XML 파일의 정보 자동 삽입, 업데이트 및 삭제는 다른 데이터 원본 컨트롤과 마찬가지로 자동으로 발생 하지 않습니다. 대신 XmlDataSource 컨트롤의 다음 메서드를 사용 하 여 수동으로 데이터를 편집 하는 코드를 작성 해야 합니다.

### <a name="getxmldocument"></a>GetXmlDocument

XmlDataSource에서 검색 된 XML 코드를 포함 하는 XmlDocument 개체를 검색 합니다.

### <a name="save"></a>저장

메모리 내 XmlDocument를 데이터 원본에 다시 저장 합니다.

Save 메서드는 다음 두 조건이 충족 되는 경우에만 작동 합니다.

1. XmlDataSource는 데이터 파일 속성을 사용 하 여 메모리 내 XML 데이터에 바인딩하기 위해 데이터 속성 대신 XML 파일에 바인딩합니다.
2. Transform 또는 TransformFile 속성을 통해 변환이 지정 되지 않습니다.

또한 Save 메서드는 여러 사용자가 동시에 호출 하는 경우 예기치 않은 결과를 생성할 수 있습니다.

## <a name="the-objectdatasource-control"></a>ObjectDataSource 컨트롤

이 시점까지 살펴본 데이터 소스 컨트롤은 데이터 소스 컨트롤이 데이터 저장소와 직접 통신 하는 2 계층 응용 프로그램에 적합 합니다. 그러나 많은 실제 응용 프로그램은 데이터 원본 컨트롤이 비즈니스 개체와 통신 해야 하는 다중 계층 응용 프로그램으로, 데이터 계층과 통신 합니다. 이러한 상황에서 ObjectDataSource는 청구서를 깔끔하게 채웁니다. ObjectDataSource는 소스 개체와 함께 작동 합니다. ObjectDataSource 컨트롤은 원본 개체의 인스턴스를 만들고, 지정 된 메서드를 호출 하 고, 개체가 정적 메서드 (Visual Basic에서 공유) 대신 인스턴스 메서드를 포함 하는 경우 단일 요청의 범위 내에서 개체 인스턴스를 모두 삭제 합니다. 따라서 개체는 상태 비저장 이어야 합니다. 즉, 개체가 단일 요청 범위 내에서 필요한 모든 리소스를 확보 하 고 해제 해야 합니다. ObjectDataSource 컨트롤의 ObjectCreating 이벤트를 처리 하 여 원본 개체를 만드는 방법을 제어할 수 있습니다. 원본 개체의 인스턴스를 만든 다음 ObjectDataSourceEventArgs 클래스의 ObjectInstance 속성을 해당 인스턴스로 설정할 수 있습니다. ObjectDataSource 컨트롤은 자체적으로 인스턴스를 만드는 대신 ObjectCreating 이벤트에서 만들어진 인스턴스를 사용 합니다.

ObjectDataSource 컨트롤의 원본 개체가 데이터를 검색 하 고 수정 하기 위해 호출할 수 있는 공용 정적 메서드 (Visual Basic에서 공유)를 노출 하는 경우 ObjectDataSource 컨트롤이 해당 메서드를 직접 호출 합니다. ObjectDataSource 컨트롤이 메서드를 호출 하기 위해 원본 개체의 인스턴스를 만들어야 하는 경우 개체는 매개 변수를 사용 하지 않는 public 생성자를 포함 해야 합니다. ObjectDataSource 컨트롤은 소스 개체의 새 인스턴스를 만들 때이 생성자를 호출 합니다.

소스 개체에 매개 변수가 없는 public 생성자가 포함 되어 있지 않은 경우 ObjectCreating 이벤트의 ObjectDataSource 컨트롤에서 사용할 원본 개체의 인스턴스를 만들 수 있습니다.

## <a name="specifying-object-methods"></a>개체 메서드 지정

ObjectDataSource 컨트롤의 원본 개체는 데이터를 선택, 삽입, 업데이트 또는 삭제 하는 데 사용 되는 메서드를 개수에 관계 없이 포함할 수 있습니다. 이러한 메서드는 ObjectDataSource 컨트롤의 SelectMethod, InsertMethod, UpdateMethod 또는 DeleteMethod 속성 중 하나를 사용 하 여 식별 되는 메서드 이름에 따라 ObjectDataSource 컨트롤에 의해 호출 됩니다. 원본 개체는 선택적 SelectCount 메서드를 포함할 수도 있습니다 .이 메서드는 데이터 원본에서 개체의 총 수를 반환 하는 SelectCountMethod 속성을 사용 하 여 ObjectDataSource 컨트롤로 식별 됩니다. ObjectDataSource 컨트롤은 Select 메서드가 호출 된 후 SelectCount 메서드를 호출 하 여 데이터 소스에서 페이징할 때 사용할 총 레코드 수를 검색 합니다.

## <a name="lab-using-data-source-controls"></a>데이터 원본 제어를 사용 하는 랩

## <a name="exercise-1---displaying-data-with-the-sqldatasource-control"></a>연습 1-SqlDataSource 컨트롤을 사용 하 여 데이터 표시

다음 연습에서는 SqlDataSource 컨트롤을 사용 하 여 Northwind 데이터베이스에 연결 합니다. SQL Server 2000 인스턴스에서 Northwind 데이터베이스에 대 한 액세스 권한이 있다고 가정 합니다.

1. 새 ASP.NET 웹 사이트 만들기
2. 새 web.config 파일을 추가 합니다.

    1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 클릭 합니다.
    2. 템플릿 목록에서 웹 구성 파일을 선택 하 고 추가를 클릭 합니다.
3. &lt;connectionStrings&gt; 섹션을 다음과 같이 편집 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample6.aspx)]
4. 코드 뷰로 전환 하 고 다음과 같이 &lt;asp: SqlDataSource&gt; 컨트롤에 ConnectionString 특성과 SelectCommand 특성을 추가 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample7.aspx)]
5. 디자인 뷰에서 새 GridView 컨트롤을 추가 합니다.
6. GridView 작업 메뉴의 데이터 원본 선택 드롭다운에서 SqlDataSource1를 선택 합니다.
7. Default.aspx를 마우스 오른쪽 단추로 클릭 하 고 메뉴에서 브라우저에서 보기를 선택 합니다. 저장 하 라는 메시지가 표시 되 면 예를 클릭 합니다.
8. GridView는 Products 테이블의 데이터를 표시 합니다.

## <a name="exercise-2---editing-data-with-the-sqldatasource-control"></a>연습 2-SqlDataSource 컨트롤을 사용 하 여 데이터 편집

다음 연습에서는 선언적 구문을 사용 하 여 DropDownList 컨트롤에 데이터를 바인딩하는 방법을 보여 주며,이를 통해 DropDownList 컨트롤에 표시 되는 데이터를 편집할 수 있습니다.

1. 디자인 뷰에서 GridView 컨트롤을 Default.aspx에서 삭제 합니다. 

    **중요**: SqlDataSource 컨트롤을 페이지에 그대로 둡니다.
2. Default.aspx에 DropDownList 컨트롤을 추가 합니다.
3. 원본 뷰로 전환 합니다.
4. 다음과 같이 &lt;asp: DropDownList&gt; 컨트롤에 DataSourceId, DataTextField 및 DataValueField 특성을 추가 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample8.aspx)]
5. Default.aspx를 저장 하 고 브라우저에서 봅니다. DropDownList에는 Northwind 데이터베이스의 모든 제품이 포함 됩니다.
6. 브라우저를 닫습니다.
7. Default.aspx의 소스 뷰에서 DropDownList 컨트롤 아래에 새 TextBox 컨트롤을 추가 합니다. 텍스트 상자의 ID 속성을 txtProductName으로 변경 합니다.
8. TextBox 컨트롤에서 새 단추 컨트롤을 추가 합니다. 단추의 ID 속성을 btnUpdate로 변경 하 고 Text 속성을 클릭 하 여 **제품 이름을 업데이트**합니다.
9. Default.aspx의 원본 뷰에서 다음과 같이 UpdateCommand 속성 및 새 UpdateParameters 두 개를 SqlDataSource 태그에 추가 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample9.aspx)]

    > [!NOTE]
    > 이 코드에는 두 가지 업데이트 매개 변수 (ProductName 및 ProductID)가 추가 되어 있습니다. 이러한 매개 변수는 txtProductName TextBox의 Text 속성과 ddlProducts DropDownList의 SelectedValue 속성에 매핑됩니다.
10. 디자인 뷰로 전환 하 고 단추 컨트롤을 두 번 클릭 하 여 이벤트 처리기를 추가 합니다.
11. BtnUpdate\_에 다음 코드를 추가 하 고 코드를 클릭 합니다. 

    [!code-csharp[Main](data-source-controls/samples/sample10.cs)]
12. Default.aspx를 마우스 오른쪽 단추로 클릭 하 고 브라우저에서 확인을 선택 합니다. 모든 변경 내용을 저장할지 묻는 메시지가 표시 되 면 예를 클릭 합니다.
13. ASP.NET 2.0 partial 클래스는 런타임에 컴파일을 허용 합니다. 코드 변경 내용이 적용 되는 것을 확인 하기 위해 응용 프로그램을 빌드하는 것은 필요 하지 않습니다.
14. DropDownList에서 제품을 선택 합니다.
15. 텍스트 상자에 선택한 제품의 새 이름을 입력 한 다음 업데이트 단추를 클릭 합니다.
16. 데이터베이스에서 제품 이름이 업데이트 됩니다.

## <a name="exercise-3-using-the-objectdatasource-control"></a>연습 3 ObjectDataSource 컨트롤 사용

이 연습에서는 ObjectDataSource 컨트롤과 소스 개체를 사용 하 여 Northwind 데이터베이스와 상호 작용 하는 방법을 보여 줍니다.

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 클릭 합니다.
2. 템플릿 목록에서 Web Form을 선택 합니다. 이름을 .aspx로 변경 하 고 추가를 클릭 합니다.
3. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 클릭 합니다.
4. 템플릿 목록에서 클래스를 선택 합니다. 클래스의 이름을 NorthwindData.cs로 변경 하 고 추가를 클릭 합니다.
5. 앱\_코드 폴더에 클래스를 추가 하 라는 메시지가 표시 되 면 예를 클릭 합니다.
6. NorthwindData.cs 파일에 다음 코드를 추가 합니다. 

    [!code-csharp[Main](data-source-controls/samples/sample11.cs)]
7. 다음 코드를 개체 .aspx의 소스 뷰에 추가 합니다. 

    [!code-aspx[Main](data-source-controls/samples/sample12.aspx)]
8. 모든 파일을 저장 하 고 개체 .aspx를 검색 합니다.
9. 세부 정보를 보고, 직원을 편집 하 고, 직원을 추가 하 고, 직원을 삭제 하 여 인터페이스와 상호 작용 합니다.
