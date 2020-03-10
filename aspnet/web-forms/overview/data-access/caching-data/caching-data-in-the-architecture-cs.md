---
uid: web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
title: 아키텍처에서 데이터 캐싱 (C#) | Microsoft Docs
author: rick-anderson
description: 이전 자습서에서는 프레젠테이션 계층에서 캐싱을 적용 하는 방법을 알아보았습니다. 이 자습서에서는 계층화 된 architectu을 활용 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 05/30/2007
ms.assetid: d29a7c41-0628-4a23-9dfc-bfea9c6c1054
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
msc.type: authoredcontent
ms.openlocfilehash: 192cadb8e2f862ac2a97a36b375e247b281ece93
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78443729"
---
# <a name="caching-data-in-the-architecture-c"></a>아키텍처에서 데이터 캐싱(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[샘플 앱 다운로드](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_59_CS.exe) 또는 [PDF 다운로드](caching-data-in-the-architecture-cs/_static/datatutorial59cs1.pdf)

> 이전 자습서에서는 프레젠테이션 계층에서 캐싱을 적용 하는 방법을 알아보았습니다. 이 자습서에서는 계층 아키텍처를 활용 하 여 비즈니스 논리 계층에서 데이터를 캐시 하는 방법에 대해 알아봅니다. 캐싱 계층을 포함 하도록 아키텍처를 확장 하 여이 작업을 수행 합니다.

## <a name="introduction"></a>소개

이전 자습서에서 살펴본 것 처럼 ObjectDataSource s 데이터를 캐시 하는 것은 몇 가지 속성을 설정 하는 것 만큼 간단 합니다. 아쉽게도 ObjectDataSource는 캐싱 정책을 ASP.NET 페이지와 긴밀 하 게 결합 프레젠테이션 계층에서 캐싱을 적용 합니다. 계층화 된 아키텍처를 만드는 이유 중 하나는 이러한 couplings의 중단을 허용 하는 것입니다. 예를 들어 비즈니스 논리 계층은 ASP.NET 페이지에서 비즈니스 논리를 분리 데이터 액세스 계층은 데이터 액세스 정보를 분리 합니다. 이러한 비즈니스 논리 및 데이터 액세스 세부 정보 분리는 시스템을 보다 쉽게 읽고 유지 관리할 수 있으며 유연 하 게 변경할 수 있기 때문에 매우 선호 됩니다. 또한 도메인 정보를 허용 하 고 프레젠테이션 계층에서 작업 하는 개발자가 작업을 수행 하기 위해 데이터베이스 세부 정보를 잘 알고 있어야 합니다. 프레젠테이션 계층에서 캐싱 정책을 분리 하면 비슷한 이점이 제공 됩니다.

이 자습서에서는 캐싱 정책을 활용 하는 *캐싱 계층* (또는 SHORT 용 CL)을 포함 하도록 아키텍처를 보강 합니다. 캐싱 계층에는 `GetProducts()`, `GetProductsByCategoryID(categoryID)`등의 메서드를 사용 하 여 제품 정보에 대 한 액세스를 제공 하는 `ProductsCL` 클래스가 포함 됩니다 .이 클래스를 호출 하면 먼저 캐시에서 데이터를 검색 하려고 합니다. 캐시가 비어 있으면 이러한 메서드는 BLL에서 적절 한 `ProductsBLL` 메서드를 호출 하 여 DAL에서 데이터를 가져옵니다. `ProductsCL` 메서드는 반환 하기 전에 BLL에서 검색 된 데이터를 캐시 합니다.

그림 1에 나와 있는 것 처럼 CL은 프레젠테이션과 비즈니스 논리 계층 사이에 있습니다.

![CL (캐싱 계층)은 아키텍처의 또 다른 계층입니다.](caching-data-in-the-architecture-cs/_static/image1.png)

**그림 1**: 아키텍처의 또 다른 계층을 위한 캐싱 계층 (CL)

## <a name="step-1-creating-the-caching-layer-classes"></a>1 단계: 캐싱 계층 클래스 만들기

이 자습서에서는 몇 가지 메서드만 있는 `ProductsCL` 단일 클래스를 사용 하 여 매우 간단한 CL을 만듭니다. 전체 응용 프로그램에 대 한 완전 한 캐싱 계층을 빌드하려면 `CategoriesCL`, `EmployeesCL`및 `SuppliersCL` 클래스를 만들고 BLL의 각 데이터 액세스 또는 수정 메서드에 대해 이러한 캐싱 계층 클래스에서 메서드를 제공 해야 합니다. BLL 및 DAL과 마찬가지로 캐싱 계층은 별도의 클래스 라이브러리 프로젝트로 구현 하는 것이 가장 좋습니다. 그러나 `App_Code` 폴더에서 클래스로 구현 합니다.

DAL 및 BLL 클래스에서 CL 클래스를 보다 명확 하 게 구분 하려면 `App_Code` 폴더에 새 하위 폴더를 만들어 보겠습니다. 솔루션 탐색기에서 `App_Code` 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 폴더를 선택한 다음 새 폴더의 이름을 `CL`로 설정 합니다. 이 폴더를 만든 후 `ProductsCL.cs`이라는 새 클래스를 추가 합니다.

![CL 이라는 새 폴더와 ProductsCL.cs 라는 클래스를 추가 합니다.](caching-data-in-the-architecture-cs/_static/image2.png)

**그림 2**: `CL` 이라는 새 폴더 및 라는 클래스를 추가 `ProductsCL.cs`

`ProductsCL` 클래스는 해당 하는 비즈니스 논리 계층 클래스 (`ProductsBLL`)에 있는 것과 동일한 데이터 액세스 및 수정 메서드 집합을 포함 해야 합니다. 이러한 메서드를 모두 생성 하는 대신, CL에서 사용 되는 패턴에 대 한 느낌을 얻기 위해 여기에 몇 가지를 작성해 보겠습니다. 특히 3 단계의 `GetProducts()` 및 `GetProductsByCategoryID(categoryID)` 메서드와 4 단계에서 `UpdateProduct` 오버 로드를 추가 합니다. 레저에 나머지 `ProductsCL` 메서드와 `CategoriesCL`, `EmployeesCL`및 `SuppliersCL` 클래스를 추가할 수 있습니다.

## <a name="step-2-reading-and-writing-to-the-data-cache"></a>2 단계: 데이터 캐시 읽기 및 쓰기

이전 자습서에서 살펴본 ObjectDataSource 캐싱 기능은 내부적으로 ASP.NET 데이터 캐시를 사용 하 여 BLL에서 검색 된 데이터를 저장 합니다. ASP.NET pages 코드 숨겨진 클래스 또는 웹 응용 프로그램 아키텍처의 클래스에서 프로그래밍 방식으로 데이터 캐시에 액세스할 수도 있습니다. ASP.NET page s의 코드 숨김으로 된 클래스에서 데이터 캐시를 읽고 쓰려면 다음 패턴을 사용 합니다.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample1.cs)]

[`Cache` 클래스](https://msdn.microsoft.com/library/system.web.caching.cache.aspx) [`Insert` 메서드에](https://msdn.microsoft.com/library/system.web.caching.cache.insert.aspx) 는 많은 오버 로드가 있습니다. `Cache["key"] = value` 및 `Cache.Insert(key, value)`는 동의어 이며 정의 된 만료 없이 지정 된 키를 사용 하 여 캐시에 항목을 추가 합니다. 일반적으로 캐시에 항목을 추가할 때 종속성, 시간 기반 만료 중 하나 또는 둘 다로 만료를 지정 하려고 합니다. 다른 `Insert` 메서드의 오버 로드 중 하나를 사용 하 여 종속성 또는 시간 기반 만료 정보를 제공 합니다.

캐싱 계층의 메서드는 먼저 요청 된 데이터가 캐시에 있는지 확인 하 고, 필요한 경우 여기에서 반환 합니다. 요청 된 데이터가 캐시에 없으면 적절 한 BLL 메서드를 호출 해야 합니다. 다음 시퀀스 다이어그램에서 보여 주는 것 처럼 반환 값을 캐시 한 후 반환 해야 합니다.

![캐싱 계층의 메서드는 캐시에서 데이터를 반환 합니다 (사용 가능한 경우).](caching-data-in-the-architecture-cs/_static/image3.png)

**그림 3**: 캐싱 계층의 메서드를 사용할 수 있는 경우 캐시에서 데이터 반환

그림 3에 표시 된 시퀀스는 다음과 같은 패턴을 사용 하 여 CL 클래스에서 수행 됩니다.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample2.cs)]

여기서는 `Northwind.ProductsDataTable`캐시에 저장 되는 데이터의 *형식입니다. 예를 들어* *key* 는 캐시 항목을 고유 하 게 식별 하는 키입니다. 지정 된 *키* 를 가진 항목이 캐시에 없으면 *인스턴스가* `null` 되며 적절 한 BLL 메서드에서 데이터가 검색 되어 캐시에 추가 됩니다. `return instance`에 도달 하면 *인스턴스* 는 캐시에서 또는 BLL에서 가져온 데이터에 대 한 참조를 포함 합니다.

캐시에서 데이터에 액세스할 때 위의 패턴을 사용 해야 합니다. 처음에는 동일 하 게 보이는 다음 패턴은 경합 상태를 소개 하는 미묘한 차이를 포함 합니다. 경합 상태는 산발적으로 노출 되 고 재현 하기 어렵기 때문에 디버깅 하기 어렵습니다.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample3.cs)]

이 두 번째 코드 조각에서는 캐시 된 항목에 대 한 참조를 지역 변수에 저장 하는 대신, 조건문 *과* `return`에서 직접 데이터 캐시에 액세스할 수 있다는 점이 다릅니다. 이 코드에 도달 하면 `Cache["key"]``null`되지 않지만 `return` 문에 도달 하기 전에 캐시에서 system 임의로 *키* 를 가정 합니다. 드문 경우 지만 코드에서 필요한 형식의 개체가 아니라 `null` 값을 반환 합니다.

> [!NOTE]
> 데이터 캐시는 스레드로부터 안전 하므로 단순 읽기 또는 쓰기를 위해 스레드 액세스를 동기화 할 필요가 없습니다. 그러나 원자성 이어야 하는 캐시의 데이터에 대해 여러 작업을 수행 해야 하는 경우에는 스레드 안전을 보장 하기 위해 잠금 또는 다른 메커니즘을 구현 해야 합니다. 자세한 내용은 [ASP.NET Cache에 대 한 액세스 동기화를](http://www.ddj.com/184406369) 참조 하세요.

다음과 같이 [`Remove` 메서드](https://msdn.microsoft.com/library/system.web.caching.cache.remove.aspx) 를 사용 하 여 프로그래밍 방식으로 데이터 캐시에서 항목을 제거할 수 있습니다.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample4.cs)]

## <a name="step-3-returning-product-information-from-theproductsclclass"></a>3 단계:`ProductsCL`클래스에서 제품 정보 반환

이 자습서에서는 `GetProducts()` 및 `GetProductsByCategoryID(categoryID)``ProductsCL` 클래스에서 제품 정보를 반환 하는 두 가지 메서드를 구현 합니다. 비즈니스 논리 계층의 `ProductsBL` 클래스와 마찬가지로, CL의 `GetProducts()` 메서드는 모든 제품에 대 한 정보를 `Northwind.ProductsDataTable` 개체로 반환 하는 반면 `GetProductsByCategoryID(categoryID)`는 지정 된 범주의 모든 제품을 반환 합니다.

다음 코드는 `ProductsCL` 클래스의 메서드 일부를 보여 줍니다.

[!code-vb[Main](caching-data-in-the-architecture-cs/samples/sample5.vb)]

먼저 클래스 및 메서드에 적용 된 `DataObject` 및 `DataObjectMethodAttribute` 특성을 확인 합니다. 이러한 특성은 마법사의 단계에 표시 되어야 하는 클래스 및 메서드를 나타내는 정보를 ObjectDataSource s 마법사에 제공 합니다. CL 클래스와 메서드는 프레젠테이션 계층의 ObjectDataSource에서 액세스 되므로 디자인 타임 환경을 향상 시키기 위해 이러한 특성을 추가 했습니다. 이러한 특성 및 해당 효과에 대 한 자세한 설명은 [비즈니스 논리 계층 만들기](../introduction/creating-a-business-logic-layer-cs.md) 자습서를 다시 참조 하세요.

`GetProducts()` 및 `GetProductsByCategoryID(categoryID)` 메서드에서는 `GetCacheItem(key)` 메서드에서 반환 되는 데이터가 지역 변수에 할당 됩니다. 잠시 후에 검사할 `GetCacheItem(key)` 메서드는 지정 된 *키*를 기준으로 캐시에서 특정 항목을 반환 합니다. 이러한 데이터를 캐시에서 찾을 수 없으면 해당 `ProductsBLL` 클래스 메서드에서 검색 된 다음 `AddCacheItem(key, value)` 메서드를 사용 하 여 캐시에 추가 됩니다.

`GetCacheItem(key)` 및 `AddCacheItem(key, value)` 메서드는 각각 데이터 캐시로 인터페이스 하 고 값을 읽고 씁니다. `GetCacheItem(key)` 방법은 두 가지 보다 간단 합니다. 단지 전달 된 *키*를 사용 하 여 Cache 클래스에서 값을 반환 합니다.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample6.cs)]

`GetCacheItem(key)`는 제공 되는 *키* 값을 사용 하지 않고 대신 `GetCacheKey(key)` 메서드를 호출 합니다 .이 메서드는 ProductsCache-앞에 있는 *키* 를 반환 합니다. ProductsCache 문자열을 포함 하는 `MasterCacheKeyArray`은 일시적으로 표시 되는 것 처럼 `AddCacheItem(key, value)` 메서드에서도 사용 됩니다.

ASP.NET page s의 코드 숨김이 클래스 [`Cache` 속성](https://msdn.microsoft.com/library/system.web.ui.page.cache.aspx)을 사용 하 여 데이터 캐시에 액세스할 수 있으며, 2 단계에 설명 `Page` 된 대로 `Cache["key"] = value`와 같은 구문을 사용할 수 있습니다. 아키텍처 내의 클래스에서 데이터 캐시는 `HttpRuntime.Cache` 또는 `HttpContext.Current.Cache`를 사용 하 여 액세스할 수 있습니다. [Peter Johnson](https://weblogs.asp.net/pjohnson/default.aspx)의 블로그 항목 HttpRuntime `HttpContext.Current`와 대신 `HttpRuntime`를 사용 하는 경우 성능이 약간 향상 [되었습니다.](https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache) 따라서 `ProductsCL`는 `HttpRuntime`를 사용 합니다.

> [!NOTE]
> 클래스 라이브러리 프로젝트를 사용 하 여 아키텍처가 구현 된 경우 [HttpRuntime](https://msdn.microsoft.com/library/system.web.httpruntime.aspx) 및 [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) 클래스를 사용 하려면 `System.Web` 어셈블리에 대 한 참조를 추가 해야 합니다.

캐시에서 항목을 찾을 수 없는 경우 `ProductsCL` 클래스의 메서드는 `AddCacheItem(key, value)` 메서드를 사용 하 여 BLL에서 데이터를 가져온 다음 캐시에 추가 합니다. 캐시에 *값* 을 추가 하려면 다음 코드를 사용할 수 있습니다 .이 코드는 60 초 만료 시간을 사용 합니다.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample7.cs)]

`DateTime.Now.AddSeconds(CacheDuration)`는 앞으로 시간 기반 만료 60 초를 지정 하 고 [`System.Web.Caching.Cache.NoSlidingExpiration`](https://msdn.microsoft.com/library/system.web.caching.cache.noslidingexpiration(vs.80).aspx) 는 슬라이딩 만료가 없음을 나타냅니다. 이 `Insert` 메서드 오버 로드에는 절대 및 슬라이딩 만료 모두에 대 한 입력 매개 변수가 있지만 둘 중 하나만 제공할 수 있습니다. 절대 시간과 시간 범위를 모두 지정 하려고 하면 `Insert` 메서드가 `ArgumentException` 예외를 throw 합니다.

> [!NOTE]
> 현재 `AddCacheItem(key, value)` 메서드의 구현에는 몇 가지 단점이 있습니다. 4 단계에서 이러한 문제를 해결 하 고 해결 합니다.

## <a name="step-4-invalidating-the-cache-when-the-data-is-modified-through-the-architecture"></a>4 단계: 아키텍처를 통해 데이터가 수정 될 때 캐시 무효화

데이터 검색 방법과 함께 캐싱 계층은 데이터 삽입, 업데이트 및 삭제를 위한 BLL과 동일한 메서드를 제공 해야 합니다. CL의 데이터 수정 메서드는 캐시 된 데이터를 수정 하지 않고 BLL의 해당 데이터 수정 메서드를 호출한 다음 캐시를 무효화 합니다. 앞의 자습서에서 살펴본 것 처럼이는 캐싱 기능을 사용 하도록 설정 하 고 해당 `Insert`, `Update`또는 `Delete` 메서드를 호출할 때 ObjectDataSource가 적용 하는 동작과 동일 합니다.

다음 `UpdateProduct` 오버 로드에서는 CL에서 데이터 수정 메서드를 구현 하는 방법을 보여 줍니다.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample8.cs)]

적절 한 데이터 수정 비즈니스 논리 계층 메서드가 호출 되지만 응답이 반환 되기 전에 캐시를 무효화 해야 합니다. 불행 하 게, `ProductsCL` 클래스 s `GetProducts()` 및 `GetProductsByCategoryID(categoryID)` 메서드가 각각 다른 키를 사용 하 여 캐시에 항목을 추가 하 고 `GetProductsByCategoryID(categoryID)` 메서드는 각 고유 *categoryID*에 대해 서로 다른 캐시 항목을 추가 하기 때문에 캐시를 무효화 하는 것은 간단 하지 않습니다.

캐시를 무효화 하는 경우 `ProductsCL` 클래스에서 추가 했을 수 있는 *모든* 항목을 제거 해야 합니다. *캐시 종속성* 을 `AddCacheItem(key, value)` 메서드의 캐시에 추가 된 각 항목과 연결 하 여이를 수행할 수 있습니다. 일반적으로 캐시 종속성은 캐시에 있는 다른 항목, 파일 시스템의 파일 또는 Microsoft SQL Server 데이터베이스의 데이터가 될 수 있습니다. 종속성이 변경 되거나 캐시에서 제거 되 면 연결 된 캐시 항목이 캐시에서 자동으로 제거 됩니다. 이 자습서에서는 `ProductsCL` 클래스를 통해 추가 된 모든 항목에 대 한 캐시 종속성으로 사용 되는 추가 항목을 캐시에 만들려고 합니다. 이렇게 하면 캐시 종속성을 제거 하 여 이러한 모든 항목을 캐시에서 제거할 수 있습니다.

를 사용 하 여이 메서드를 통해 캐시에 추가 된 각 항목이 단일 캐시 종속성과 연결 되도록 `AddCacheItem(key, value)` 메서드를 업데이트 합니다.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample9.cs)]

`MasterCacheKeyArray`는 단일 값 ProductsCache을 포함 하는 문자열 배열입니다. 먼저 캐시 항목을 캐시에 추가 하 고 현재 날짜 및 시간을 할당 합니다. 캐시 항목이 이미 있으면 업데이트 됩니다. 그런 다음 캐시 종속성을 만듭니다. [`CacheDependency` 클래스](https://msdn.microsoft.com/library/system.web.caching.cachedependency(VS.80).aspx) 의 생성자에는 많은 오버 로드가 있지만 여기에서 사용 되는 생성자에는 두 개의 `string` 배열 입력이 필요 합니다. 첫 번째는 종속성으로 사용할 파일 집합을 지정 합니다. 파일 기반 종속성을 사용 하지 않으려는 경우 첫 번째 입력 매개 변수에 `null` 값이 사용 됩니다. 두 번째 입력 매개 변수는 종속성으로 사용할 캐시 키 집합을 지정 합니다. 여기서는 `MasterCacheKeyArray`단일 종속성을 지정 합니다. 그런 다음 `CacheDependency` `Insert` 메서드에 전달 됩니다.

이러한 수정 작업을 `AddCacheItem(key, value)`하 여 캐시를 사용 하는 것은 종속성을 제거 하는 것 만큼 간단 합니다.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample10.cs)]

## <a name="step-5-calling-the-caching-layer-from-the-presentation-layer"></a>5 단계: 프레젠테이션 계층에서 캐싱 계층 호출

캐싱 계층의 클래스 및 메서드를 사용 하 여 이러한 자습서에서 검사 한 기술을 사용 하 여 데이터 작업을 수행할 수 있습니다. 캐시 된 데이터를 사용 하 여 작업 하는 방법을 설명 하려면 `ProductsCL` 클래스에 변경 내용을 저장 한 다음 `Caching` 폴더에서 `FromTheArchitecture.aspx` 페이지를 열고 GridView를 추가 합니다. GridView s 스마트 태그에서 새 ObjectDataSource를 만듭니다. 마법사의 첫 번째 단계에서는 `ProductsCL` 클래스가 드롭다운 목록의 옵션 중 하나로 표시 되어야 합니다.

[비즈니스 개체 드롭다운 목록에 제품 Scl 클래스 ![포함 되어 있습니다.](caching-data-in-the-architecture-cs/_static/image5.png)](caching-data-in-the-architecture-cs/_static/image4.png)

**그림 4**: `ProductsCL` 클래스가 비즈니스 개체 드롭다운 목록에 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](caching-data-in-the-architecture-cs/_static/image6.png)).

`ProductsCL`를 선택한 후 다음을 클릭 합니다. 선택 탭의 드롭다운 목록에는 `GetProducts()` 및 `GetProductsByCategoryID(categoryID)`의 두 항목이 있으며 업데이트 탭에는 유일한 `UpdateProduct` 오버 로드가 있습니다. 선택 탭에서 `GetProducts()` 메서드를 선택 하 고 업데이트 탭에서 `UpdateProducts` 방법을 선택한 다음 마침을 클릭 합니다.

[![는 제품 Scl 클래스의 메서드는 드롭다운 목록에 나열 됩니다.](caching-data-in-the-architecture-cs/_static/image8.png)](caching-data-in-the-architecture-cs/_static/image7.png)

**그림 5**: `ProductsCL` 클래스의 메서드는 드롭다운 목록에 나열 됩니다 ([전체 크기 이미지를 보려면 클릭](caching-data-in-the-architecture-cs/_static/image9.png)).

마법사를 완료 한 후 Visual Studio에서는 ObjectDataSource s `OldValuesParameterFormatString` 속성을 `original_{0}` 설정 하 고 적절 한 필드를 GridView에 추가 합니다. `OldValuesParameterFormatString` 속성을 `{0}`기본값으로 다시 변경 하 고 페이징, 정렬 및 편집을 지원 하도록 GridView를 구성 합니다. CL에서 사용 하는 `UploadProducts` 오버 로드는 편집 된 제품 이름 및 가격만 허용 하므로 이러한 필드만 편집할 수 있도록 GridView를 제한 합니다.

이전 자습서에서는 `ProductName`, `CategoryName`및 `UnitPrice` 필드에 대 한 필드를 포함 하도록 GridView를 정의 했습니다. 이 형식 및 구조를 자유롭게 복제할 수 있습니다 .이 경우 GridView 및 ObjectDataSource의 선언적 태그가 다음과 같이 표시 됩니다.

[!code-aspx[Main](caching-data-in-the-architecture-cs/samples/sample11.aspx)]

이 시점에서 캐싱 계층을 사용 하는 페이지가 있습니다. 작업 중인 캐시를 보려면 `ProductsCL` 클래스 `GetProducts()` 및 `UpdateProduct` 메서드에 중단점을 설정 합니다. 브라우저에서 페이지를 방문 하 고 정렬 및 페이징을 통해 코드를 단계별로 실행 하 여 캐시에서 끌어온 데이터를 확인 합니다. 그런 다음 레코드를 업데이트 하면 캐시가 무효화 되 고 데이터가 GridView에 다시 바인딩 되었을 때 BLL에서 검색 됩니다.

> [!NOTE]
> 이 문서와 함께 다운로드에 제공 된 캐싱 계층이 완전 하지 않습니다. 이 클래스에는 소수의 메서드만 스포츠 하는 하나의 클래스 `ProductsCL`포함 되어 있습니다. 또한 단일 ASP.NET 페이지만 CL (`~/Caching/FromTheArchitecture.aspx`)을 사용 하 고 다른 모든 페이지는 여전히 BLL을 직접 참조 합니다. 응용 프로그램에서 CL 사용을 계획 하는 경우 프레젠테이션 계층의 모든 호출은 CL로 이동 해야 합니다. 그러면 cl의 클래스 및 메서드가 프레젠테이션 계층에서 현재 사용 하 고 있는 BLL의 클래스와 메서드를 적용 해야 합니다.

## <a name="summary"></a>요약

캐싱을 ASP.NET 2.0 s SqlDataSource 및 ObjectDataSource 컨트롤과 함께 프레젠테이션 계층에 적용할 수 있지만, 아키텍처의 개별 계층에 가장 적합 한 캐싱 책임이 위임 될 수 있습니다. 이 자습서에서는 프레젠테이션 계층과 비즈니스 논리 계층 사이에 있는 캐싱 계층을 만들었습니다. 캐싱 계층은 BLL에 존재 하 고 프레젠테이션 계층에서 호출 되는 동일한 클래스 및 메서드 집합을 제공 해야 합니다.

이에 대해 살펴본 캐싱 계층 예제와 앞의 자습서에는 *사후 로드*가 있습니다. 사후 로드를 사용 하면 데이터에 대 한 요청을 수행 하 고 캐시에 데이터가 없는 경우에만 데이터가 캐시에 로드 됩니다. 데이터는 실제로 필요 하기 전에 캐시에 데이터를 로드 하는 기술인 캐시에 *사전 로드* 될 수도 있습니다. 다음 자습서에서는 응용 프로그램 시작 시 캐시에 정적 값을 저장 하는 방법을 살펴볼 때 사전 로드의 예제를 살펴보겠습니다.

행복 한 프로그래밍

## <a name="about-the-author"></a>저자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서의 리드 검토자는 Teresa Murph입니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](caching-data-with-the-objectdatasource-cs.md)
> [다음](caching-data-at-application-startup-cs.md)
