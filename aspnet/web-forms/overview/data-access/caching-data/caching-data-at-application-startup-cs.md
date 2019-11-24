---
uid: web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
title: 응용 프로그램 시작 시 데이터 캐싱C#() | Microsoft Docs
author: rick-anderson
description: 모든 웹 응용 프로그램에서 일부 데이터는 자주 사용 되 고 일부 데이터는 자주 사용 되지 않습니다. ASP.NET 응용 프로그램의 성능을 향상 시킬 수 있습니다.
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 22ca8efa-7cd1-45a7-b9ce-ce6eb3b3ff95
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
msc.type: authoredcontent
ms.openlocfilehash: a0b55b0df1b7843120de284891e16178df23fabe
ms.sourcegitcommit: fe5c7512383a9b0a05d321ff10d3cca1611556f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/05/2019
ms.locfileid: "70386511"
---
# <a name="caching-data-at-application-startup-c"></a>애플리케이션 시작 시 데이터 캐싱(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](caching-data-at-application-startup-cs/_static/datatutorial60cs1.pdf)

> 모든 웹 응용 프로그램에서 일부 데이터는 자주 사용 되 고 일부 데이터는 자주 사용 되지 않습니다. 자주 사용 하는 데이터 (캐싱 이라고 함)를 미리 로드 하 여 ASP.NET 응용 프로그램의 성능을 향상 시킬 수 있습니다. 이 자습서에서는 응용 프로그램 시작 시 캐시로 데이터를 로드 하는 사전 로드의 한 가지 방법을 보여 줍니다.

## <a name="introduction"></a>소개

위의 두 가지 자습서에서는 프레젠테이션 및 캐싱 계층에서 데이터를 캐시 하는 방법을 살펴보았습니다. ObjectDataSource를 사용 하 여 [데이터를 캐시할](caching-data-with-the-objectdatasource-cs.md)때 objectdatasource의 캐싱 기능을 사용 하 여 프레젠테이션 계층의 데이터를 캐시 하는 방법을 살펴보았습니다. [아키텍처의 데이터를 캐시](caching-data-in-the-architecture-cs.md) 하는 경우 별도의 새로운 캐싱 계층에서 캐싱이 검사 됩니다. 이러한 자습서는 모두 데이터 캐시 작업에서 *사후 로드* 를 사용 했습니다. 사후 로드를 사용 하면 데이터가 요청 될 때마다 시스템이 먼저 캐시에 있는지 확인 합니다. 그렇지 않으면 데이터베이스와 같은 원래 원본에서 데이터를 가져와 하 여 캐시에 저장 합니다. 사후 로드의 주요 이점은 구현의 용이성입니다. 이러한 단점 중 하나는 요청 간에 불균형 성능입니다. 이전 자습서의 캐싱 계층을 사용 하 여 제품 정보를 표시 하는 페이지를 상상해 보세요. 이 페이지를 처음으로 방문 하거나 메모리 제약 조건으로 인해 캐시 된 데이터가 제거 된 후 처음으로 방문 하거나 지정 된 만료에 도달 하면 데이터베이스에서 데이터를 검색 해야 합니다. 따라서 이러한 사용자 요청은 캐시에서 처리할 수 있는 사용자 요청 보다 오래 걸립니다.

*자동 관리 로드* 는 캐시 된 데이터를 필요에 따라 로드 하 여 요청 간에 성능을 저하 하는 대체 캐시 관리 전략을 제공 합니다. 일반적으로 자동 관리 로드에서는 기본 데이터에 대 한 업데이트가 있는 경우 주기적으로 확인 하거나 알림이 표시 되는 프로세스를 사용 합니다. 그런 다음이 프로세스는 캐시를 업데이트 하 여 최신 상태로 유지 합니다. 자동 관리 로드는 기본 데이터가 느린 데이터베이스 연결, 웹 서비스 또는 기타 기타 데이터 원본에서 제공 되는 경우에 특히 유용 합니다. 그러나 이러한 자동 관리 로드 방식은 변경을 확인 하 고 캐시를 업데이트 하는 프로세스를 만들고 관리 하 고 배포 해야 하므로 구현 하기가 더 어렵습니다.

다른 사전 로드 버전 및이 자습서에서 살펴볼 형식은 응용 프로그램 시작 시 캐시로 데이터를 로드 하는 것입니다. 이 방법은 데이터베이스 조회 테이블의 레코드와 같은 정적 데이터를 캐시 하는 데 특히 유용 합니다.

> [!NOTE]
> 자동 관리 및 사후 로드 간의 차이점 뿐만 아니라 전문가, 단점 및 구현 권장 사항의 목록을 자세히 보려면 [.NET Framework 응용 프로그램에 대 한 캐싱 아키텍처 가이드](https://msdn.microsoft.com/library/ms978498.aspx)의 [캐시 콘텐츠 관리](https://msdn.microsoft.com/library/ms978503.aspx) 섹션을 참조 하세요.

## <a name="step-1-determining-what-data-to-cache-at-application-startup"></a>1 단계: 응용 프로그램 시작 시 캐시할 데이터 결정

이전 두 자습서에서 검사 한 사후 처리 로드를 사용 하는 캐싱 예제는 주기적으로 변경 될 수 있는 데이터와 함께 작동 하며 생성 하는 데 exorbitantly 긴 시간이 소요 되지 않습니다. 그러나 캐시 된 데이터가 변경 되지 않는 경우 사후 로드에서 사용 하는 만료는 불필요 합니다. 마찬가지로 캐시 되는 데이터를 생성 하는 데 지나치게 긴 시간이 소요 되는 경우, 해당 캐시를 검색 하는 요청은 기본 데이터를 검색 하는 동안 긴 대기 시간을 endure 해야 합니다. 응용 프로그램 시작 시 생성 하는 데 매우 긴 시간이 소요 되는 정적 데이터 및 데이터를 캐싱하는 것이 좋습니다.

데이터베이스에는 자주 변경 되는 동적 값이 많이 있지만, 대부분의 경우에는 상당한 양의 정적 데이터도 있습니다. 예를 들어 거의 모든 데이터 모델에는 고정 된 선택 항목 집합에서 특정 값을 포함 하는 열이 하나 이상 있습니다. `Patients` 데이터베이스 테이블에는 값 집합을 영어, 스페인어, 프랑스어, 러시아어, 일본어 등으로 지정할 수 있는 `PrimaryLanguage` 열이 있을 수 있습니다. 이러한 유형의 열이 *조회 테이블*을 사용 하 여 구현 되는 경우가 많습니다. `Patients` 테이블에 영어 또는 프랑스어 문자열을 저장 하는 대신, 일반적으로 두 개의 열, 즉 고유 식별자와 문자열 설명을 포함 하는 두 번째 테이블이 생성 됩니다. 여기에는 가능한 각 값에 대 한 레코드가 포함 됩니다. `Patients` 테이블의 `PrimaryLanguage` 열은 조회 테이블에 해당 하는 고유 식별자를 저장 합니다. 그림 1에서 환자 John Doe의 주 언어는 영어이 고 Ed Johnson의는 러시아어입니다.

![언어 테이블은 환자 테이블에서 사용 하는 조회 테이블입니다.](caching-data-at-application-startup-cs/_static/image1.png)

**그림 1**: `Languages` 테이블은 `Patients` 테이블에서 사용 하는 조회 테이블입니다.

새 환자를 편집 하거나 만들기 위한 사용자 인터페이스에는 `Languages` 테이블의 레코드로 채워진 허용 가능한 언어의 드롭다운 목록이 포함 됩니다. 캐싱을 사용 하지 않는 경우이 인터페이스를 방문할 때마다 시스템에서 `Languages` 테이블을 쿼리해야 합니다. 조회 테이블 값은 매우 드물게 변경 되므로 불필요 하 고 필요 하지 않습니다.

이전 자습서에서 검사 한 것과 동일한 사후 로드 기법을 사용 하 여 `Languages` 데이터를 캐시할 수 있습니다. 그러나 사후 로드는 정적 조회 테이블 데이터에 필요 하지 않은 시간 기반 만료를 사용 합니다. 사후 로드를 사용 하는 캐싱은 캐싱을 전혀 사용 하지 않는 것이 좋지만 응용 프로그램 시작 시 조회 테이블 데이터를 캐시에 사전에 로드 하는 것이 가장 좋은 방법입니다.

이 자습서에서는 조회 테이블 데이터 및 기타 정적 정보를 캐시 하는 방법을 살펴보겠습니다.

## <a name="step-2-examining-the-different-ways-to-cache-data"></a>2 단계: 데이터를 캐시 하는 다양 한 방법 검사

정보는 다양 한 방법을 사용 하 여 프로그래밍 방식으로 ASP.NET 응용 프로그램에 캐시할 수 있습니다. 이전 자습서에서 데이터 캐시를 사용 하는 방법을 이미 살펴보았습니다. 또는 *정적 멤버나* *응용 프로그램 상태*를 사용 하 여 프로그래밍 방식으로 개체를 캐시할 수 있습니다.

클래스를 사용 하는 경우 일반적으로 해당 멤버에 액세스 하려면 먼저 클래스를 인스턴스화해야 합니다. 예를 들어 비즈니스 논리 계층의 클래스 중 하나에서 메서드를 호출 하려면 먼저 클래스의 인스턴스를 만들어야 합니다.

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample1.cs)]

*SomeMethod* 를 호출 하거나 *SomeProperty*를 사용 하 여 작업 하려면 먼저 `new` 키워드를 사용 하 여 클래스의 인스턴스를 만들어야 합니다. *SomeMethod* 및 *SomeProperty* 는 특정 인스턴스와 연결 됩니다. 이러한 멤버의 수명은 연결 된 개체의 수명에 연결 됩니다. 반면에 *정적 멤버*는 클래스의 *모든* 인스턴스 간에 공유 되는 변수, 속성 및 메서드로, 결과적으로 클래스의 수명 기간을 갖습니다. 정적 멤버는 `static`키워드로 표시 됩니다.

정적 멤버 외에도 응용 프로그램 상태를 사용 하 여 데이터를 캐시할 수 있습니다. 각 ASP.NET 응용 프로그램은 응용 프로그램의 모든 사용자 및 페이지에서 공유 되는 이름/값 컬렉션을 유지 관리 합니다. 이 컬렉션은 [`HttpContext` 클래스](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)의 [`Application` 속성](https://msdn.microsoft.com/library/system.web.httpcontext.application.aspx)을 사용 하 여 액세스할 수 있으며, 다음과 같이 ASP.NET 페이지의 코드 숨김이 아닌 클래스에서 사용 됩니다.

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample2.cs)]

데이터 캐시는 데이터를 캐시 하 고 시간 및 종속성 기반 expiries, 캐시 항목 우선 순위 등을 위한 메커니즘을 제공 하는 훨씬 더 풍부한 API를 제공 합니다. 정적 멤버와 응용 프로그램 상태를 사용 하면 페이지 개발자가 이러한 기능을 수동으로 추가 해야 합니다. 그러나 응용 프로그램을 시작할 때 응용 프로그램의 수명 동안 데이터를 캐시 하는 경우 데이터 캐시의 이점이 불과할 됩니다. 이 자습서에서는 정적 데이터 캐싱에 세 가지 기술을 모두 사용 하는 코드를 살펴보겠습니다.

## <a name="step-3-caching-thesupplierstable-data"></a>3 단계:`Suppliers`테이블 데이터 캐싱

지금까지 구현한 Northwind 데이터베이스 테이블에는 기존의 조회 테이블이 포함 되어 있지 않습니다. 해당 값이 비정적 인 모든 모델 테이블에서 구현 되는 네 가지 Datatable. 이 자습서에서는 DAL에 새 DataTable을 추가 하는 시간을 소비 하 고 BLL에 새 클래스와 메서드를 사용 하는 대신 `Suppliers` 테이블의 데이터가 정적인 것으로 가정 합니다. 따라서 응용 프로그램을 시작할 때이 데이터를 캐시할 수 있습니다.

시작 하려면 `CL` 폴더에 `StaticCache.cs` 라는 새 클래스를 만듭니다.

![CL 폴더에 StaticCache.cs 클래스 만들기](caching-data-at-application-startup-cs/_static/image2.png)

**그림 2**: `CL` 폴더에 `StaticCache.cs` 클래스 만들기

시작할 때 데이터를 로드 하는 메서드를 적절 한 캐시 저장소에 추가 하 고이 캐시에서 데이터를 반환 하는 메서드를 추가 해야 합니다.

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample3.cs)]

위의 코드에서는 정적 멤버 변수 `suppliers`를 사용 하 여 `LoadStaticCache()` 메서드에서 호출 되는 `SuppliersBLL` 클래스의 `GetSuppliers()` 메서드에서 결과를 저장 합니다. `LoadStaticCache()` 메서드는 응용 프로그램을 시작 하는 동안 호출 됩니다. 응용 프로그램 시작 시이 데이터가 로드 되 면 공급자 데이터로 작업 해야 하는 모든 페이지는 `StaticCache` 클래스의 `GetSuppliers()` 메서드를 호출할 수 있습니다. 따라서 공급자를 가져오기 위해 데이터베이스에 대 한 호출은 응용 프로그램 시작 시 한 번만 수행 됩니다.

정적 멤버 변수를 캐시 저장소로 사용 하는 대신 응용 프로그램 상태 또는 데이터 캐시를 사용 했을 수도 있습니다. 다음 코드에서는 응용 프로그램 상태를 사용 하는 클래스를 보여 줍니다.

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample4.cs)]

`LoadStaticCache()`공급자 정보는 응용 프로그램 변수 *키*에 저장 됩니다. `GetSuppliers()`에서 적절 한 형식 (`Northwind.SuppliersDataTable`)으로 반환 됩니다. 응용 프로그램 상태는 `Application["key"]`를 사용 하는 ASP.NET 페이지의 코드를 사용 하는 클래스에서 액세스할 수 있지만, 아키텍처에서는 현재 `HttpContext`를 얻기 위해 `HttpContext.Current.Application["key"]`를 사용 해야 합니다.

마찬가지로, 다음 코드에 나와 있는 것 처럼 데이터 캐시를 캐시 저장소로 사용할 수 있습니다.

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample5.cs)]

시간 기반 만료 없이 항목을 데이터 캐시에 추가 하려면 `System.Web.Caching.Cache.NoAbsoluteExpiration`를 사용 하 고 값을 입력 매개 변수로 `System.Web.Caching.Cache.NoSlidingExpiration` 합니다. 캐시 항목의 *우선 순위* 를 지정할 수 있도록 데이터 캐시의 `Insert` 메서드의이 오버 로드를 선택 했습니다. 우선 순위는 사용 가능한 메모리가 부족 한 경우 캐시에서 청소할 항목을 결정 하는 데 사용 됩니다. 여기서는이 캐시 항목이 청소 되지 않도록 하는 우선 순위 `NotRemovable`를 사용 합니다.

> [!NOTE]
> 이 자습서의 다운로드에서는 정적 멤버 변수 접근 방법을 사용 하 여 `StaticCache` 클래스를 구현 합니다. 응용 프로그램 상태 및 데이터 캐시 기술에 대 한 코드는 클래스 파일의 주석에서 사용할 수 있습니다.

## <a name="step-4-executing-code-at-application-startup"></a>4 단계: 응용 프로그램 시작 시 코드 실행

웹 응용 프로그램이 처음 시작 될 때 코드를 실행 하려면 `Global.asax`라는 특수 파일을 만들어야 합니다. 이 파일은 응용 프로그램, 세션 및 요청 수준 이벤트에 대 한 이벤트 처리기를 포함할 수 있으며 응용 프로그램이 시작 될 때마다 실행 되는 코드를 추가할 수 있습니다.

Visual Studio의 솔루션 탐색기에서 웹 사이트 프로젝트 이름을 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택 하 여 `Global.asax` 파일을 웹 응용 프로그램의 루트 디렉터리에 추가 합니다. 새 항목 추가 대화 상자에서 전역 응용 프로그램 클래스 항목 유형을 선택 하 고 추가 단추를 클릭 합니다.

> [!NOTE]
> 프로젝트에 `Global.asax` 파일이 이미 있는 경우 전역 응용 프로그램 클래스 항목 형식이 새 항목 추가 대화 상자에 표시 되지 않습니다.

[웹 응용 프로그램의 루트 디렉터리에 Global.asax 파일을 추가 ![](caching-data-at-application-startup-cs/_static/image4.png)](caching-data-at-application-startup-cs/_static/image3.png)

**그림 3**: 웹 응용 프로그램의 루트 디렉터리에 `Global.asax` 파일 추가 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-cs/_static/image5.png))

기본 `Global.asax` 파일 템플릿에는 서버 쪽 `<script>` 태그 내에 5 개의 메서드가 포함 되어 있습니다.

- 웹 응용 프로그램이 처음 시작 될 때 **`Application_Start`** 실행
- 응용 프로그램이 종료 될 때 **`Application_End`** 실행 됨
- 처리 되지 않은 예외가 응용 프로그램에 도달할 때마다 **`Application_Error`** 실행 됩니다.
- 새 세션이 생성 될 때 **`Session_Start`** 실행 됨
- 세션이 만료 되거나 중단 될 때 **`Session_End`** 실행 됨

`Application_Start` 이벤트 처리기는 응용 프로그램의 수명 주기 동안 한 번만 호출 됩니다. 응용 프로그램은 응용 프로그램에서 ASP.NET 리소스가 처음 요청 될 때 시작 되 고 응용 프로그램이 다시 시작 될 때까지 계속 실행 됩니다 .이는 `/Bin` 폴더의 콘텐츠를 수정 하거나 `Global.asax`수정 하거나 `App_Code` 폴더의 내용을 수정 하거나 `Web.config` 파일을 수정 하 여 발생할 수 있습니다. 응용 프로그램 수명 주기에 대 한 자세한 내용은 [ASP.NET 응용 프로그램 수명 주기 개요](https://msdn.microsoft.com/library/ms178473.aspx) 를 참조 하세요.

이러한 자습서의 경우 `Application_Start` 메서드에 코드를 추가 하기만 하면 됩니다. `Application_Start`에서 공급자 정보를 로드 하 고 캐시 하는 `StaticCache` 클래스의 `LoadStaticCache()` 메서드를 호출 하기만 하면 됩니다.

[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample6.aspx)]

이것이 전부입니다! 응용 프로그램 시작 시 `LoadStaticCache()` 메서드는 BLL에서 공급자 정보를 가져오고이를 정적 멤버 변수 (또는 `StaticCache` 클래스에서 사용 하 여 종료 한 캐시 저장소)에 저장 합니다. 이 동작을 확인 하려면 `Application_Start` 메서드에 중단점을 설정 하 고 응용 프로그램을 실행 합니다. 응용 프로그램이 시작 될 때 중단점이 적중 됩니다. 그러나 후속 요청으로 인해 `Application_Start` 메서드가 실행 되지 않습니다.

[중단점 ![사용 하 여 Application_Start 이벤트 처리기가 실행 되 고 있는지 확인 합니다.](caching-data-at-application-startup-cs/_static/image7.png)](caching-data-at-application-startup-cs/_static/image6.png)

**그림 4**: 중단점을 사용 하 여 `Application_Start` 이벤트 처리기가 실행 되 고 있는지 확인 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-cs/_static/image8.png))

> [!NOTE]
> 디버깅을 처음 시작할 때 `Application_Start` 중단점에 도달 하지 않으면 응용 프로그램이 이미 시작 되었기 때문입니다. `Global.asax` 또는 `Web.config` 파일을 수정 하 여 응용 프로그램을 강제로 다시 시작 하 고 다시 시도 하세요. 이러한 파일 중 하나의 끝에 빈 줄을 추가 (또는 제거) 하 여 응용 프로그램을 신속 하 게 다시 시작할 수 있습니다.

## <a name="step-5-displaying-the-cached-data"></a>5 단계: 캐시 된 데이터 표시

이 시점에서 `StaticCache` 클래스는 응용 프로그램 시작 시 캐시 된 공급자 데이터의 버전을 `GetSuppliers()` 메서드를 통해 액세스할 수 있습니다. 프레젠테이션 계층에서이 데이터를 사용 하려면 ObjectDataSource를 사용 하거나 ASP.NET 페이지의 코드 숨김이 클래스에서 `StaticCache` 클래스의 `GetSuppliers()` 메서드를 프로그래밍 방식으로 호출할 수 있습니다. ObjectDataSource 컨트롤과 GridView 컨트롤을 사용 하 여 캐시 된 공급자 정보를 표시 하는 방법을 살펴보겠습니다.

먼저 `Caching` 폴더에서 `AtApplicationStartup.aspx` 페이지를 엽니다. GridView를 도구 상자에서 디자이너로 끌어 `ID` 속성을 `Suppliers`로 설정 합니다. 다음으로 GridView의 스마트 태그에서 `SuppliersCachedDataSource`라는 새 ObjectDataSource를 만들도록 선택 합니다. `StaticCache` 클래스의 `GetSuppliers()` 메서드를 사용 하도록 ObjectDataSource를 구성 합니다.

[StaticCache 클래스를 사용 하도록 ObjectDataSource를 구성 ![](caching-data-at-application-startup-cs/_static/image10.png)](caching-data-at-application-startup-cs/_static/image9.png)

**그림 5**: `StaticCache` 클래스를 사용 하도록 ObjectDataSource 구성 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-cs/_static/image11.png))

[GetSuppliers () 메서드를 사용 하 여 캐시 된 공급자 데이터를 검색 ![](caching-data-at-application-startup-cs/_static/image13.png)](caching-data-at-application-startup-cs/_static/image12.png)

**그림 6**: `GetSuppliers()` 메서드를 사용 하 여 캐시 된 공급자 데이터 검색 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-cs/_static/image14.png))

마법사를 완료 한 후 Visual Studio는 `SuppliersDataTable`의 각 데이터 필드에 대해 BoundFields를 자동으로 추가 합니다. GridView와 ObjectDataSource의 선언 태그는 다음과 유사 하 게 표시 됩니다.

[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample7.aspx)]

그림 7은 브라우저를 통해 볼 때 페이지를 표시 합니다. 출력은 BLL의 `SuppliersBLL` 클래스에서 가져온 데이터를 갖지만 `StaticCache` 클래스를 사용 하 여 응용 프로그램 시작 시 캐시 된 공급자 데이터를 반환 합니다. `StaticCache` 클래스의 `GetSuppliers()` 메서드에 중단점을 설정 하 여이 동작을 확인할 수 있습니다.

[캐시 된 공급자 데이터가 GridView에 표시 ![](caching-data-at-application-startup-cs/_static/image16.png)](caching-data-at-application-startup-cs/_static/image15.png)

**그림 7**: 캐시 된 공급자 데이터가 GridView에 표시 됨 ([전체 크기 이미지를 보려면 클릭](caching-data-at-application-startup-cs/_static/image17.png))

## <a name="summary"></a>요약

대부분의 모든 데이터 모델에는 일반적으로 조회 테이블의 형태로 구현 되는 상당한 양의 정적 데이터가 포함 되어 있습니다. 이 정보는 정적 이므로이 정보를 표시 해야 할 때마다 데이터베이스에 지속적으로 액세스할 이유가 없습니다. 또한 정적 특성으로 인해 데이터를 캐시 하는 경우 만료에 대 한 필요는 없습니다. 이 자습서에서는 이러한 데이터를 가져와서 데이터 캐시, 응용 프로그램 상태 및 정적 멤버 변수를 통해 캐시 하는 방법을 살펴보았습니다. 이 정보는 응용 프로그램 시작 시 캐시 되며 응용 프로그램의 수명 동안 캐시에 남아 있습니다.

이 자습서와 지난 두 가지에서는 시간 기반 expiries을 사용 하는 것 뿐만 아니라 응용 프로그램의 수명 기간 동안 데이터를 캐시 하는 방법을 살펴보았습니다. 그러나 데이터베이스 데이터를 캐시 하는 경우 시간 기반 만료가 이상적인 시간 보다 낮을 수 있습니다. 캐시를 주기적으로 플러시하는 대신 기본 데이터베이스 데이터가 수정 될 때 캐시 된 항목만 제거 하는 것이 가장 좋습니다. 이러한 이상적인 방법은 다음 자습서에서 살펴볼 SQL 캐시 종속성을 사용 하 여 수행할 수 있습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Teresa Murphy 및 Zack Jones 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](caching-data-in-the-architecture-cs.md)
> [다음](using-sql-cache-dependencies-cs.md)
