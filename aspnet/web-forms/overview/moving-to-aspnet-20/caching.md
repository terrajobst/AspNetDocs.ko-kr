---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: 캐싱 | Microsoft Docs
author: microsoft
description: 잘 작동 하는 ASP.NET 응용 프로그램에는 캐싱을 이해 하는 것이 중요 합니다. ASP.NET 1.x는 캐싱에 대 한 세 가지 옵션을 제공 합니다. 출력 캐싱,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: 4f0b021ca6ca151544dd9fb0587ed9e0cf14ff65
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78464957"
---
# <a name="caching"></a>캐싱

[Microsoft](https://github.com/microsoft) 에서

> 잘 작동 하는 ASP.NET 응용 프로그램에는 캐싱을 이해 하는 것이 중요 합니다. ASP.NET 1.x는 캐싱에 대 한 세 가지 옵션을 제공 합니다. 출력 캐싱, 조각 캐싱 및 캐시 API가 있습니다.

잘 작동 하는 ASP.NET 응용 프로그램에는 캐싱을 이해 하는 것이 중요 합니다. ASP.NET 1.x는 캐싱에 대 한 세 가지 옵션을 제공 합니다. 출력 캐싱, 조각 캐싱 및 캐시 API가 있습니다. ASP.NET 2.0는 이러한 메서드 중 세 가지를 모두 제공 하지만 몇 가지 중요 한 추가 기능을 추가 합니다. 몇 가지 새로운 캐시 종속성이 있으며 개발자는 이제 사용자 지정 캐시 종속성도 만들 수 있습니다. ASP.NET 2.0 에서도 캐싱 구성이 크게 향상 되었습니다.

## <a name="new-features"></a>새로운 기능

## <a name="cache-profiles"></a>캐시 프로필

캐시 프로필을 사용 하면 개발자가 개별 페이지에 적용할 수 있는 특정 캐시 설정을 정의할 수 있습니다. 예를 들어 12 시간 후에 캐시에서 만료 되어야 하는 일부 페이지가 있는 경우 해당 페이지에 적용할 수 있는 캐시 프로필을 쉽게 만들 수 있습니다. 새 캐시 프로필을 추가 하려면 구성 파일의 &lt;outputCacheSettings&gt; 섹션을 사용 합니다. 예를 들어 다음은 캐시 기간을 12 시간으로 구성 하는 *twoday* 라는 캐시 프로필의 구성입니다.

[!code-xml[Main](caching/samples/sample1.xml)]

이 캐시 프로필을 특정 페이지에 적용 하려면 아래와 같이 @ OutputCache 지시문의 CacheProfile 특성을 사용 합니다.

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>사용자 지정 캐시 종속성

ASP.NET 1.x 개발자는 사용자 지정 캐시 종속성을 제대로 합니다. ASP.NET 1.x에서 CacheDependency 클래스는 봉인 되어 개발자가 자체 클래스를 파생 시킬 수 없습니다. ASP.NET 2.0에서는이 제한이 제거 되 고 개발자는 자신의 고유한 사용자 지정 캐시 종속성을 자유롭게 개발할 수 있습니다. CacheDependency 클래스를 사용 하면 파일, 디렉터리 또는 캐시 키를 기반으로 하는 사용자 지정 캐시 종속성을 만들 수 있습니다.

예를 들어 아래 코드는 웹 응용 프로그램의 루트에 있는 .xml 이라는 파일을 기반으로 새 사용자 지정 캐시 종속성을 만듭니다.

[!code-csharp[Main](caching/samples/sample3.cs)]

이 시나리오에서 system.xml 파일이 변경 되 면 캐시 된 항목이 무효화 됩니다.

또한 캐시 키를 사용 하 여 사용자 지정 캐시 종속성을 만들 수 있습니다. 이 메서드를 사용 하 여 캐시 키를 제거 하면 캐시 된 데이터가 무효화 됩니다. 다음 예제에서는 이에 대해 설명합니다.

[!code-csharp[Main](caching/samples/sample4.cs)]

위에 삽입 된 항목을 무효화 하려면 캐시 키 역할을 할 캐시에 삽입 된 항목을 제거 하면 됩니다.

[!code-csharp[Main](caching/samples/sample5.cs)]

캐시 키 역할을 하는 항목의 키는 캐시 키 배열에 추가 된 값과 동일 해야 합니다.

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>폴링 기반 SQL 캐시 종속성 (테이블 기반 종속성이 라고도 함)

SQL Server 7 및 2000는 SQL 캐시 종속성에 대 한 폴링 기반 모델을 사용 합니다. 폴링 기반 모델은 테이블의 데이터가 변경 될 때 트리거되는 데이터베이스 테이블에 대 한 트리거를 사용 합니다. 이 트리거는 ASP.NET에서 정기적으로 확인 하는 알림 테이블에서 **Changeid** 필드를 업데이트 합니다. **Changeid** 필드가 업데이트 된 경우 ASP.NET는 데이터가 변경 된 것을 인식 하 고 캐시 된 데이터를 무효화 합니다.

> [!NOTE]
> SQL Server 2005는 폴링 기반 모델을 사용할 수도 있지만 폴링 기반 모델은 가장 효율적인 모델이 아니기 때문에 SQL Server 2005에서 쿼리 기반 모델 (나중에 설명)을 사용 하는 것이 좋습니다.

폴링 기반 모델을 사용 하는 SQL 캐시 종속성이 제대로 작동 하려면 테이블에 알림이 활성화 되어 있어야 합니다. SqlCacheDependencyAdmin 클래스를 사용 하거나 aspnet\_regsql 유틸리티를 사용 하 여 프로그래밍 방식으로이를 수행할 수 있습니다.

다음 명령줄은 SQL 캐시 종속성에 대해 *dbase* 라는 SQL Server 인스턴스에 있는 Northwind 데이터베이스의 Products 테이블을 등록 합니다.

[!code-console[Main](caching/samples/sample6.cmd)]

다음은 위의 명령에 사용 되는 명령줄 스위치에 대 한 설명입니다.

| **명령줄 스위치** | **용도** |
| --- | --- |
| -S *server* | 서버 이름을 지정합니다. |
| -ed | SQL 캐시 종속성을 사용 하도록 데이터베이스를 설정 하도록 지정 합니다. |
| -d *데이터베이스\_이름* | SQL 캐시 종속성에 사용할 데이터베이스 이름을 지정 합니다. |
| -E | Aspnet\_regsql에서 데이터베이스에 연결할 때 Windows 인증을 사용 하도록 지정 합니다. |
| -et | SQL 캐시 종속성에 데이터베이스 테이블을 사용 하도록 설정 합니다. |
| -t *테이블\_이름* | SQL 캐시 종속성에 사용할 데이터베이스 테이블의 이름을 지정 합니다. |

> [!NOTE]
> 다른 스위치는 aspnet\_에서 사용할 수 있습니다. 전체 목록을 보려면 aspnet\_를 실행 합니다. 명령줄에서

이 명령이 실행 되 면 SQL Server 데이터베이스가 다음과 같이 변경 됩니다.

- **AspNet\_SqlCacheTablesForChangeNotification** 테이블이 추가 됩니다. 이 테이블에는 SQL 캐시 종속성을 사용 하도록 설정 된 데이터베이스의 각 테이블에 대 한 행이 하나씩 포함 되어 있습니다.
- 데이터베이스 내에 생성 되는 저장 프로시저는 다음과 같습니다.

| AspNet\_SqlCachePollingStoredProcedure | AspNet\_SqlCacheTablesForChangeNotification 테이블을 쿼리하고 SQL 캐시 종속성을 사용 하도록 설정 된 모든 테이블과 각 테이블에 대 한 changeId 값을 반환 합니다. 이 저장 프로시저는 데이터가 변경 되었는지 확인 하기 위해 폴링을 위해 사용 됩니다. |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | AspNet\_SqlCacheTablesForChangeNotification 테이블을 쿼리하여 sql 캐시 종속성을 사용 하도록 설정 된 모든 테이블을 반환 하 여 SQL 캐시 종속성에 사용할 수 있는 모든 테이블을 반환 합니다. |
| AspNet\_SqlCacheRegisterTableStoredProcedure | 알림 테이블에 필요한 항목을 추가 하 여 SQL 캐시 종속성에 대 한 테이블을 등록 하 고 트리거를 추가 합니다. |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | 알림 테이블에서 항목을 제거 하 고 트리거를 제거 하 여 SQL 캐시 종속성에 대 한 테이블의 등록을 취소 합니다. |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | 변경 된 테이블에 대 한 changeId를 증가 시켜 알림 테이블을 업데이트 합니다. ASP.NET는이 값을 사용 하 여 데이터가 변경 되었는지 여부를 확인 합니다. 아래에 표시 된 것 처럼이 저장 프로시저는 테이블을 사용할 때 생성 된 트리거에 의해 실행 됩니다. |

- 테이블  **_\_이름_\_AspNet\_SqlCacheNotification\_trigger** 라는 SQL Server 트리거가 만들어집니다. 이 트리거는 테이블에서 삽입, 업데이트 또는 삭제를 수행할 때 AspNet\_SqlCacheUpdateChangeIdStoredProcedure를 실행 합니다.
- **Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** 라는 SQL Server 역할이 데이터베이스에 추가 됩니다.

**Aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server 역할에는 Aspnet\_SqlCachePollingStoredProcedure에 대 한 EXEC 권한이 있습니다. 폴링 모델이 제대로 작동 하려면 aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess 역할에 프로세스 계정을 추가 해야 합니다. Aspnet\_regsql .exe 도구는이 작업을 수행 하지 않습니다.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>폴링 기반 SQL 캐시 종속성 구성

폴링 기반 SQL 캐시 종속성을 구성 하는 데 필요한 몇 가지 단계가 있습니다. 첫 번째 단계는 위에서 설명한 대로 데이터베이스 및 테이블을 사용 하도록 설정 하는 것입니다. 해당 단계가 완료 되 면 구성의 나머지 부분은 다음과 같습니다.

- ASP.NET 구성 파일을 구성 하는 중입니다.
- SqlCacheDependency 구성

### <a name="configuring-the-aspnet-configuration-file"></a>ASP.NET 구성 파일 구성

이전 모듈에서 설명한 대로 연결 문자열을 추가 하는 것 외에도 아래와 같이 &lt;sqlCacheDependency&gt; 요소를 사용 하 여 &lt;cache&gt; 요소를 구성 해야 합니다.

[!code-xml[Main](caching/samples/sample7.xml)]

이 구성은 *pubs* 데이터베이스에서 SQL 캐시 종속성을 사용 하도록 설정 합니다. &lt;sqlCacheDependency&gt; 요소의 pollTime 특성 기본값은 6만 밀리초 또는 1 분입니다. 이 값은 500 밀리초 보다 적을 수 없습니다. 이 예제에서 &lt;add&gt; 요소는 새 데이터베이스를 추가 하 고 pollTime를 재정의 하 고이를 900만 밀리초로 설정 합니다.

#### <a name="configuring-the-sqlcachedependency"></a>SqlCacheDependency 구성

다음 단계는 SqlCacheDependency을 구성 하는 것입니다. 이 작업을 수행 하는 가장 쉬운 방법은 다음과 같이 @ Outcache 지시문에서 SqlDependency 특성의 값을 지정 하는 것입니다.

[!code-aspx[Main](caching/samples/sample8.aspx)]

위의 @ OutputCache 지시문에는 *pubs* 데이터베이스의 *authors* 테이블에 대해 SQL 캐시 종속성이 구성 되어 있습니다. 여러 종속성은 다음과 같이 세미콜론으로 구분 하 여 구성할 수 있습니다.

[!code-aspx[Main](caching/samples/sample9.aspx)]

SqlCacheDependency를 구성 하는 또 다른 방법은 프로그래밍 방식으로이 작업을 수행 하는 것입니다. 다음 코드는 *pubs* 데이터베이스의 *authors* 테이블에 새 SQL 캐시 종속성을 만듭니다.

[!code-csharp[Main](caching/samples/sample10.cs)]

SQL 캐시 종속성을 프로그래밍 방식으로 정의 하는 이점 중 하나는 발생할 수 있는 모든 예외를 처리할 수 있다는 것입니다. 예를 들어 알림에 대해 사용 하도록 설정 되지 않은 데이터베이스에 대 한 SQL 캐시 종속성을 정의 하려고 하면 **system.web.caching.databasenotenabledfornotificationexception** 예외가 throw 됩니다. 이 경우 **EnableNotifications** 메서드를 호출 하 고 데이터베이스 이름을 전달 하 여 알림에 대해 데이터베이스를 사용 하도록 설정할 수 있습니다.

마찬가지로, 알림이 활성화 되지 않은 테이블에 대해 SQL 캐시 종속성을 정의 하려고 하면 **system.web.caching.tablenotenabledfornotificationexception** 이 throw 됩니다. 그런 다음 데이터베이스 이름 및 테이블 이름을 전달 하 여 **SqlCacheDependencyAdmin** 을 호출할 수 있습니다.

다음 코드 샘플에서는 SQL 캐시 종속성을 구성할 때 예외 처리를 올바르게 구성 하는 방법을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample11.cs)]

추가 정보: [https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>쿼리 기반 SQL 캐시 종속성 (SQL Server 2005에만 해당)

SQL 캐시 종속성에 SQL Server 2005를 사용 하는 경우 폴링 기반 모델이 필요 하지 않습니다. SQL Server 2005와 함께 사용 하는 경우 SQL 캐시 종속성은 SQL Server 2005 쿼리 알림을 사용 하 여 SQL 연결을 통해 (추가 구성이 필요 하지 않음) SQL Server 인스턴스로 직접 통신 합니다.

쿼리 기반 알림을 사용 하도록 설정 하는 가장 간단한 방법은 데이터 원본 개체의 **SqlCacheDependency** 특성을 **CommandNotification** 로 설정 하 고 **EnableCaching** 특성을 **true**로 설정 하 여 선언적으로 수행 하는 것입니다. 이 메서드를 사용 하는 경우에는 코드가 필요 하지 않습니다. 데이터 원본에 대해 실행 된 명령의 결과가 변경 되 면 캐시 데이터가 무효화 됩니다.

다음 예제에서는 SQL 캐시 종속성에 대 한 데이터 원본 제어를 구성 합니다.

[!code-aspx[Main](caching/samples/sample12.aspx)]

이 경우 **SelectCommand** 에 지정 된 쿼리가 원래 결과와 다른 결과를 반환 하면 캐시 된 결과가 무효화 됩니다.

**@ OutputCache** 지시문의 **SqlDependency** 특성을 **CommandNotification**로 설정 하 여 모든 데이터 원본을 SQL 캐시 종속성에 대해 사용 하도록 지정할 수도 있습니다. 아래 예제에서는이를 보여 줍니다.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> SQL Server 2005의 쿼리 알림에 대 한 자세한 내용은 SQL Server 온라인 설명서을 참조 하십시오.

쿼리 기반 SQL 캐시 종속성을 구성 하는 또 다른 방법은 SqlCacheDependency 클래스를 사용 하 여 프로그래밍 방식으로이 작업을 수행 하는 것입니다. 다음 코드 샘플에서는이를 수행 하는 방법을 보여 줍니다.

[!code-csharp[Main](caching/samples/sample14.cs)]

추가 정보: [https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>캐시 후 대체

페이지를 캐시 하면 웹 응용 프로그램의 성능이 크게 향상 될 수 있습니다. 그러나 일부 경우에는 대부분의 페이지가 캐시 되 고 페이지 내의 일부 조각이 동적이 되도록 해야 합니다. 예를 들어 설정 된 기간 동안 완전히 정적인 뉴스 스토리의 페이지를 만드는 경우 전체 페이지를 캐시 되도록 설정할 수 있습니다. 모든 페이지 요청에서 변경 된 회전 광고 배너를 포함 하려면 광고가 포함 된 페이지의 일부가 동적 이어야 합니다. 페이지를 캐시할 수 있지만 일부 콘텐츠를 동적으로 대체 하려면 ASP.NET 사후 캐시 대체를 사용할 수 있습니다. 사후 캐시 대체를 사용 하면 전체 페이지는 캐싱에서 제외로 표시 된 특정 부분으로 캐시 된 출력입니다. 광고 배너의 예제에서 AdRotator 컨트롤을 사용 하면 캐시 후 대체를 활용 하 여 각 사용자 및 페이지 새로 고침에 대해 광고를 동적으로 만들 수 있습니다.

사후 캐시 대체를 구현 하는 방법에는 세 가지가 있습니다.

- 대체 컨트롤을 사용 하 여 선언적으로
- 대체 컨트롤 API를 사용 하 여 프로그래밍 방식으로
- 암시적으로 AdRotator 컨트롤을 사용 합니다.

### <a name="substitution-control"></a>대체 컨트롤

ASP.NET 대체 컨트롤은 캐시 된 페이지가 아닌 동적으로 생성 되는 캐시 된 페이지의 섹션을 지정 합니다. 페이지에서 동적 콘텐츠를 표시할 위치에 대체 컨트롤을 배치 합니다. 런타임에 대체 컨트롤은 MethodName 속성을 사용 하 여 지정 하는 메서드를 호출 합니다. 메서드는 문자열을 반환 하 고 대체 컨트롤의 내용을 대체 합니다. 이 메서드는 포함 하는 페이지 또는 UserControl 컨트롤에서 정적 메서드 여야 합니다. 대체 컨트롤을 사용 하면 클라이언트 쪽 캐시 가능성이 서버 캐시로 변경 되어 클라이언트에서 페이지가 캐시 되지 않습니다. 이렇게 하면 나중에 페이지에 대 한 요청을 통해 메서드를 다시 호출 하 여 동적 콘텐츠를 생성 합니다.

### <a name="substitution-api"></a>대체 API

프로그래밍 방식으로 캐시 된 페이지에 대 한 동적 콘텐츠를 만들려면 페이지 코드에서 [WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) 메서드를 호출 하 여 메서드의 이름을 매개 변수로 전달 하면 됩니다. 동적 콘텐츠 생성을 처리 하는 메서드는 단일 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) 매개 변수를 사용 하 여 문자열을 반환 합니다. 반환 문자열은 지정 된 위치에서 대체 되는 콘텐츠입니다. 대체 컨트롤을 선언적으로 사용 하는 대신 WriteSubstitution 메서드를 호출 하는 경우에는 페이지 또는 UserControl 개체의 정적 메서드를 호출 하는 대신 임의의 개체의 메서드를 호출할 수 있다는 장점이 있습니다.

WriteSubstitution 메서드를 호출 하면 클라이언트 쪽 캐시 가능성이 서버 캐시로 변경 되어 페이지가 클라이언트에 캐시 되지 않습니다. 이렇게 하면 나중에 페이지에 대 한 요청을 통해 메서드를 다시 호출 하 여 동적 콘텐츠를 생성 합니다.

### <a name="adrotator-control"></a>AdRotator 컨트롤

AdRotator 서버 컨트롤은 내부적으로 캐시 후 대체에 대 한 지원을 구현 합니다. 페이지에 AdRotator 컨트롤을 두면 부모 페이지가 캐시 되는지 여부와 관계 없이 각 요청에 대해 고유한 광고를 렌더링 합니다. 따라서 AdRotator 컨트롤이 포함 된 페이지는 단지 캐시 된 서버 쪽입니다.

## <a name="controlcachepolicy-class"></a>ControlCachePolicy 클래스

ControlCachePolicy 클래스를 사용 하면 사용자 정의 컨트롤을 사용 하 여 조각 캐싱을 프로그래밍 방식으로 제어할 수 있습니다. ASP.NET는 [BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) 인스턴스 내에 사용자 정의 컨트롤을 포함 합니다. BasePartialCachingControl 클래스는 출력 캐싱이 설정 된 사용자 정의 컨트롤을 나타냅니다.

[Partialcachingcontrol](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) 컨트롤의 [BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) 속성에 액세스 하는 경우 항상 유효한 ControlCachePolicy 개체를 받습니다. 그러나 [usercontrol](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) 컨트롤의 [CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) 속성에 액세스 하는 경우 사용자 컨트롤이 이미 BasePartialCachingControl 컨트롤로 래핑되는 경우에만 유효한 ControlCachePolicy 개체를 받습니다. 래핑되지 않은 경우 속성에서 반환 된 ControlCachePolicy 개체에는 연결 된 BasePartialCachingControl 없기 때문에 해당 개체를 조작 하려고 하면 예외가 throw 됩니다. UserControl 인스턴스가 예외를 생성 하지 않고 캐싱을 지원 하는지 확인 하려면 [SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx) 속성을 검사 합니다.

ControlCachePolicy 클래스를 사용 하는 것은 출력 캐싱을 사용 하도록 설정할 수 있는 여러 가지 방법 중 하나입니다. 다음 목록에서는 출력 캐싱을 사용 하도록 설정 하 여 메서드를 설명 합니다.

- [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) 지시문을 사용 하 여 선언 시나리오에서 출력 캐싱을 사용 하도록 설정 합니다.
- [Partialcachingattribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) 특성을 사용 하 여 코드 숨김이 있는 파일의 사용자 정의 컨트롤에 대 한 캐싱을 사용 하도록 설정 합니다.
- ControlCachePolicy 클래스를 사용 하 여 이전 메서드 중 하나를 사용 하 여 캐시를 사용 하도록 설정 하 고 BasePartialCachingControl를 사용 하 여 동적으로 로드 한 인스턴스로 작업 하는 프로그래밍 시나리오에서 캐시 설정을 [지정 합니다.](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx)

ControlCachePolicy 인스턴스는 컨트롤 수명 주기의 Init 및 PreRender 단계 간에만 성공적으로 조작할 수 있습니다. ControlCachePolicy 개체를 PreRender 단계 후에 수정 하는 경우 ASP.NET는 컨트롤이 렌더링 된 후 변경 내용이 실제로 캐시 설정에 영향을 미칠 수 없기 때문에 예외를 throw 합니다 (렌더링 단계 중에 컨트롤이 캐시 됨). 마지막으로, 사용자 정의 컨트롤 인스턴스 (그리고 따라서 ControlCachePolicy 개체)는 실제로 렌더링 되는 경우에만 프로그래밍 조작을 수행할 수 있습니다.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>캐싱 구성 변경-&lt;캐싱&gt; 요소

ASP.NET 2.0에는 캐싱 구성에 대 한 몇 가지 변경 사항이 있습니다. &lt;캐싱&gt; 요소는 ASP.NET 2.0의 새로운 기능이 며 구성 파일에서 캐싱을 구성할 수 있도록 합니다. 사용할 수 있는 특성은 다음과 같습니다.

| **Element** | **설명** |
| --- | --- |
| **캐시** | 선택적 요소입니다. 전역 응용 프로그램 캐시 설정을 정의 합니다. |
| **outputCache** | 선택적 요소입니다. 응용 프로그램 수준의 출력 캐시 설정을 지정 합니다. |
| **outputCacheSettings** | 선택적 요소입니다. 응용 프로그램의 페이지에 적용할 수 있는 출력 캐시 설정을 지정 합니다. |
| **sqlCacheDependency** | 선택적 요소입니다. ASP.NET 애플리케이션의 SQL 캐시 종속성을 구성합니다. |

### <a name="the-ltcachegt-element"></a>&lt;cache&gt; 요소

&lt;cache&gt; 요소에서 사용할 수 있는 특성은 다음과 같습니다.

| **Attribute** | **설명** |
| --- | --- |
| **disableMemoryCollection** | 선택적 **Boolean** 특성입니다. 컴퓨터의 메모리가 부족할 때 발생 하는 캐시 메모리 수집이 사용 하지 않도록 설정 되어 있는지 여부를 나타내는 값을 가져오거나 설정 합니다. |
| **disableExpiration** | 선택적 **Boolean** 특성입니다. 캐시 만료를 사용할 수 없는지 여부를 나타내는 값을 가져오거나 설정 합니다. 사용 하지 않도록 설정 하면 캐시 된 항목이 만료 되지 않고 만료 된 캐시 항목의 백그라운드 청소가 수행 되지 않습니다. |
| **privateBytesLimit** | 선택적 **Int64** 특성입니다. 캐시에서 만료 된 항목 플러시를 시작 하 고 메모리 회수를 시작 하기 전에 응용 프로그램 전용 바이트의 최대 크기를 나타내는 값을 가져오거나 설정 합니다. 이 제한에는 캐시에 사용 되는 메모리와 실행 중인 응용 프로그램의 일반 메모리 오버 헤드가 모두 포함 됩니다. 0으로 설정 하면 ASP.NET는 메모리 회수를 시작할 시기를 결정 하기 위해 자체 추론을 사용 함을 나타냅니다. |
| **percentagePhysicalMemoryUsedLimit** | 선택적 **Int32** 특성입니다. 캐시에서 만료 된 항목 플러시를 시작 하기 전에 응용 프로그램에서 사용할 수 있는 컴퓨터의 실제 메모리의 최대 비율을 나타내는 값을 가져오거나 설정 합니다 .이 메모리 사용에는 캐시에 사용 되는 메모리가 모두 포함 됩니다. 실행 중인 응용 프로그램의 일반 메모리 사용으로 사용 됩니다. 0으로 설정 하면 ASP.NET는 메모리 회수를 시작할 시기를 결정 하기 위해 자체 추론을 사용 함을 나타냅니다. |
| **privateBytesPollTime** | 선택적 **TimeSpan** 특성입니다. 응용 프로그램의 전용 바이트 메모리 사용에 대 한 폴링 사이의 시간 간격을 나타내는 값을 가져오거나 설정 합니다. |

### <a name="the-ltoutputcachegt-element"></a>&lt;outputCache&gt; 요소

&lt;outputCache&gt; 요소에 대해 사용할 수 있는 특성은 다음과 같습니다.

|       <strong>Attribute</strong>        |                                                                                                                                                                                                                                                       <strong>설명</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          선택적 <strong>Boolean</strong> 특성입니다. 페이지 출력 캐시를 사용 하거나 사용 하지 않도록 설정 합니다. 사용 하지 않도록 설정 된 경우 프로그래밍 방식 또는 선언적 설정에 관계 없이 페이지가 캐시 되지 않습니다. 기본값은 <strong>True</strong>입니다.                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                선택적 <strong>Boolean</strong> 특성입니다. 응용 프로그램 조각 캐시를 사용 하거나 사용 하지 않도록 설정 합니다. 사용 하지 않도록 설정 된 경우에는 사용 된 [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) 지시문 또는 캐싱 프로필에 관계 없이 페이지가 캐시 되지 않습니다. 에는 업스트림 프록시 서버 및 브라우저 클라이언트에서 페이지 출력을 캐시 하지 않아야 함을 나타내는 cache-control 헤더가 포함 되어 있습니다. 기본값은 <strong>false</strong>입니다.                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      선택적 <strong>Boolean</strong> 특성입니다. <strong>캐시 제어: 전용</strong> 헤더를 기본적으로 출력 캐시 모듈에서 보낼지 여부를 나타내는 값을 가져오거나 설정 합니다. 기본값은 <strong>false</strong>입니다.                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | 선택적 <strong>Boolean</strong> 특성입니다. 응답에서 Http "<strong>Vary: \</strong >" 헤더 보내기를 사용 하거나 사용 하지 않도록 설정<em>합니다. 기본 설정인 false로 설정 하면 "</em>* Vary: \*<strong>" 헤더가 출력 캐시 된 페이지에 대해 전송 됩니다. Vary 헤더를 보내면 Vary 헤더에 지정 된 내용에 따라 서로 다른 버전을 캐시할 수 있습니다. 예를 들어 <em>다음과 같이 변경 합니다. 사용자 에이전트</em> 는 요청을 실행 하는 사용자 에이전트에 따라 서로 다른 버전의 페이지를 저장 합니다. 기본값은 * * false</strong>입니다. |

### <a name="the-ltoutputcachesettingsgt-element"></a>&lt;outputCacheSettings&gt; 요소

&lt;outputCacheSettings&gt; 요소는 앞에서 설명한 대로 캐시 프로필을 만들 수 있도록 합니다. &lt;outputCacheSettings&gt; 요소에 대 한 자식 요소는 캐시 프로필을 구성 하기 위한 &lt;Outputcachesettings&gt; 요소입니다.

### <a name="the-ltsqlcachedependencygt-element"></a>&lt;sqlCacheDependency&gt; 요소

&lt;sqlCacheDependency&gt; 요소에 사용할 수 있는 특성은 다음과 같습니다.

| **Attribute** | **설명** |
| --- | --- |
| **사용** | 필수 **부울** 특성입니다. 에 대해 변경 내용을 폴링할 지 여부를 나타냅니다. |
| **pollTime** | 선택적 **Int32** 특성입니다. SqlCacheDependency가 데이터베이스 테이블에서 변경 내용을 폴링하는 빈도를 설정 합니다. 이 값은 연속 된 pollings 사이의 시간 (밀리초)에 해당 합니다. 500 밀리초 미만으로 설정할 수 없습니다. 기본값은 1 분입니다. |

### <a name="more-information"></a>추가 정보

캐시 구성과 관련 하 여 알아야 할 몇 가지 추가 정보가 있습니다.

- 작업자 프로세스 전용 바이트 제한이 설정 되지 않은 경우 캐시는 다음 제한 중 하나를 사용 합니다. 

    - x86 2GB: 800MB 또는 실제 RAM의 60% 중 더 작은 쪽
    - x86 3GB: 18MB 또는 실제 RAM의 60% 중 더 작은 쪽
    - x64: 실제 RAM의 1tb 또는 60% 중 더 작은 쪽
- 작업자 프로세스 전용 바이트 제한과 &lt;cache privateBytesLimit/&gt;를 모두 설정 하는 경우 캐시에서 최소 2를 사용 하 게 됩니다.
- 1\.x에서와 마찬가지로 캐시 항목을 삭제 하 고 GC를 호출 합니다. 다음 두 가지 이유로 수집 합니다. 

    - 전용 바이트 제한에 매우 가깝습니다.
    - 사용 가능한 메모리가 10% 보다 작거나 같습니다.
- &lt;cache percentagePhysicalMemoryUseLimit/&gt;를 100로 설정 하 여 사용 가능한 메모리 부족 상태에 대 한 trim 및 cache를 효과적으로 사용 하지 않도록 설정할 수 있습니다.
- 1\.x와 달리 2.0는 마지막 GC 인 경우 trim 및 collect 호출을 일시 중단 합니다. Collect는 전용 바이트 또는 관리 되는 힙의 크기 (캐시) 메모리 제한의 1%를 초과 하지 않습니다.

## <a name="lab1-custom-cache-dependencies"></a>Lab1: 사용자 지정 캐시 종속성

1. 새 웹 사이트를 만듭니다.
2. Cache .xml 이라는 새 XML 파일을 추가 하 고 웹 응용 프로그램의 루트에 저장 합니다.
3. Default.aspx의 코드에 있는 Load 메서드에 다음\_코드를 추가 합니다. 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. 소스 뷰에서 default.aspx의 맨 위에 다음을 추가 합니다. 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Default.aspx를 찾아봅니다. 시간 이란 무엇 인가요?
6. 브라우저를 새로 고칩니다. 시간 이란 무엇 인가요?
7. Cache .xml을 열고 다음 코드를 추가 합니다. 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. Cache .xml을 저장 합니다.
9. 브라우저를 새로 고칩니다. 시간 이란 무엇 인가요?
10. 이전에 캐시 된 값을 표시 하는 대신 업데이트 된 시간을 설명 합니다.

## <a name="lab-2-using-polling-based-cache-dependencies"></a>랩 2: 폴링 기반 캐시 종속성 사용

이 랩에서는 이전 모듈에서 만든 프로젝트를 사용 합니다 .이 프로젝트는 GridView 및 DetailsView 컨트롤을 통해 Northwind 데이터베이스에서 데이터를 편집할 수 있습니다.

1. Visual Studio 2005에서 프로젝트를 엽니다.
2. Northwind 데이터베이스에 대해 aspnet\_regsql 유틸리티를 실행 하 여 데이터베이스와 Products 테이블을 사용 하도록 설정 합니다. Visual Studio 명령 프롬프트에서 다음 명령을 사용 합니다. 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. Web.config 파일에 다음을 추가 합니다. 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. Showdata .aspx 라는 새로운 webform를 추가 합니다.
5. Showdata .aspx 페이지에 다음 @ outputcache 지시문을 추가 합니다. 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. Showdata .aspx의 페이지\_로드 페이지에 다음 코드를 추가 합니다. 

    [!code-html[Main](caching/samples/sample21.html)]
7. 새 SqlDataSource 컨트롤을 showdata .aspx에 추가 하 고 Northwind 데이터베이스 연결을 사용 하도록 구성 합니다. 다음을 클릭합니다.
8. ProductName 및 ProductID 확인란을 선택 하 고 다음을 클릭 합니다.
9. 마침을 클릭합니다.
10. Showdata .aspx 페이지에 새 GridView를 추가 합니다.
11. 드롭다운에서 SqlDataSource1를 선택 합니다.
12. Showdata .aspx를 저장 하 고 찾아봅니다. 표시 된 시간을 기록해 둡니다.
