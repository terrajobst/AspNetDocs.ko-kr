---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 작업 필터 이해 (C#) | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 작업 필터를 설명 하는 것입니다. 작업 필터는 컨트롤러 작업 또는 전체 컨트롤러에 적용할 수 있는 특성입니다.
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: d1c72c2355c6122f851351a8c1e8f04fa63ae04e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470003"
---
# <a name="understanding-action-filters-c"></a>작업 필터 이해(C#)

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> 이 자습서의 목표는 작업 필터를 설명 하는 것입니다. 작업 필터는 컨트롤러 작업 (또는 전체 컨트롤러)에 적용할 수 있는 특성으로, 작업이 실행 되는 방식을 수정 합니다.

## <a name="understanding-action-filters"></a>작업 필터 이해

이 자습서의 목표는 작업 필터를 설명 하는 것입니다. 작업 필터는 컨트롤러 작업 (또는 전체 컨트롤러)에 적용할 수 있는 특성으로, 작업이 실행 되는 방식을 수정 합니다. ASP.NET MVC 프레임 워크에는 다음과 같은 몇 가지 작업 필터가 포함 되어 있습니다.

- OutputCache –이 작업 필터는 지정 된 시간 동안 컨트롤러 작업의 출력을 캐시 합니다.
- HandleError –이 작업 필터는 컨트롤러 작업이 실행 될 때 발생 하는 오류를 처리 합니다.
- 권한 부여 –이 작업 필터를 사용 하면 특정 사용자 또는 역할에 대 한 액세스를 제한할 수 있습니다.

사용자 지정 작업 필터를 직접 만들 수도 있습니다. 예를 들어 사용자 지정 인증 시스템을 구현 하기 위해 사용자 지정 작업 필터를 만들 수 있습니다. 또는 컨트롤러 동작에서 반환 된 뷰 데이터를 수정 하는 작업 필터를 만들 수 있습니다.

이 자습서에서는 처음부터 작업 필터를 작성 하는 방법에 대해 알아봅니다. Visual Studio 출력 창에 작업 처리의 다양 한 단계를 기록 하는 로그 작업 필터를 만듭니다.

### <a name="using-an-action-filter"></a>작업 필터 사용

작업 필터는 특성입니다. 개별 컨트롤러 작업 또는 전체 컨트롤러에 대부분의 작업 필터를 적용할 수 있습니다.

예를 들어 목록 1의 데이터 컨트롤러는 현재 시간을 반환 하는 `Index()` 이라는 동작을 표시 합니다. 이 작업은 `OutputCache` 작업 필터로 데코 레이트 됩니다. 이 필터는 작업에서 반환 된 값이 10 초 동안 캐시 되도록 합니다.

**목록 1 – `Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

브라우저의 주소 표시줄에 URL/Data/Index를 입력 하 고 새로 고침 단추를 여러 번 눌러 `Index()` 작업을 반복적으로 호출 하면 10 초 동안 동일한 시간이 표시 됩니다. `Index()` 작업의 출력은 10 초 동안 캐시 됩니다 (그림 1 참조).

[![캐시 된 시간](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**그림 01**: 캐시 된 시간 ([전체 크기 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image3.png))

목록 1에서 `OutputCache` 작업 필터 – `Index()` 메서드에 적용 됩니다. 필요한 경우 여러 작업 필터를 동일한 작업에 적용할 수 있습니다. 예를 들어 `OutputCache` 및 `HandleError` 작업 필터를 모두 동일한 작업에 적용할 수 있습니다.

목록 1에서 `OutputCache` 작업 필터는 `Index()` 작업에 적용 됩니다. 또한 `DataController` 클래스 자체에이 특성을 적용할 수 있습니다. 이 경우 컨트롤러에서 노출 하는 작업에서 반환 된 결과는 10 초 동안 캐시 됩니다.

### <a name="the-different-types-of-filters"></a>여러 유형의 필터

ASP.NET MVC 프레임 워크는 다음과 같은 네 가지 유형의 필터를 지원 합니다.

1. 권한 부여 필터 – `IAuthorizationFilter` 특성을 구현 합니다.
2. 작업 필터 – `IActionFilter` 특성을 구현 합니다.
3. 결과 필터 – `IResultFilter` 특성을 구현 합니다.
4. 예외 필터 – `IExceptionFilter` 특성을 구현 합니다.

필터는 위에 나열 된 순서 대로 실행 됩니다. 예를 들어 권한 부여 필터는 항상 다른 모든 유형의 필터 후에 작업 필터 및 예외 필터가 실행 되기 전에 실행 됩니다.

권한 부여 필터는 컨트롤러 작업에 대 한 인증 및 권한 부여를 구현 하는 데 사용 됩니다. 예를 들어 권한 부여 필터는 권한 부여 필터의 예입니다.

작업 필터는 컨트롤러 작업이 실행 되기 전후에 실행 되는 논리를 포함 합니다. 예를 들어 작업 필터를 사용 하 여 컨트롤러 작업에서 반환 하는 뷰 데이터를 수정할 수 있습니다.

결과 필터에는 뷰 결과가 실행 되기 전후에 실행 되는 논리가 포함 되어 있습니다. 예를 들어 뷰가 브라우저에 렌더링 되기 바로 전에 뷰 결과를 수정할 수 있습니다.

예외 필터는 실행할 필터의 마지막 유형입니다. 예외 필터를 사용 하 여 컨트롤러 작업 또는 컨트롤러 작업 결과에서 발생 한 오류를 처리할 수 있습니다. 예외 필터를 사용 하 여 오류를 기록할 수도 있습니다.

각 유형의 필터는 특정 순서에 따라 실행 됩니다. 동일한 형식의 필터를 실행 하는 순서를 제어 하려면 필터의 순서 속성을 설정할 수 있습니다.

모든 작업 필터에 대 한 기본 클래스는 `System.Web.Mvc.FilterAttribute` 클래스입니다. 특정 형식의 필터를 구현 하려면 기본 필터 클래스에서 상속 하는 클래스를 만들고 `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`또는 `IExceptionFilter` 인터페이스 중 하나 이상을 구현 해야 합니다.

### <a name="the-base-actionfilterattribute-class"></a>기본 ActionFilterAttribute 클래스

사용자 지정 작업 필터를 쉽게 구현할 수 있도록 ASP.NET MVC 프레임 워크에는 기본 `ActionFilterAttribute` 클래스가 포함 됩니다. 이 클래스는 `IActionFilter` 및 `IResultFilter` 인터페이스를 모두 구현 하 고 `Filter` 클래스에서 상속 합니다.

여기에 나와 있는 용어는 완전히 일치 하지 않습니다. 기술적으로 ActionFilterAttribute 클래스에서 상속 되는 클래스는 작업 필터와 결과 필터입니다. 그러나 ASP.NET MVC 프레임 워크에서 모든 종류의 필터를 참조 하는 데에는 word 작업 필터가 사용 됩니다.

기본 `ActionFilterAttribute` 클래스에는 재정의할 수 있는 다음 메서드가 있습니다.

- OnActionExecuting –이 메서드는 컨트롤러 작업이 실행 되기 전에 호출 됩니다.
- OnActionExecuted –이 메서드는 컨트롤러 작업이 실행 된 후에 호출 됩니다.
- OnResultExecuting –이 메서드는 컨트롤러 작업 결과가 실행 되기 전에 호출 됩니다.
- OnResultExecuted – 컨트롤러 작업 결과가 실행 된 후이 메서드가 호출 됩니다.

다음 섹션에서는 이러한 여러 가지 방법을 구현 하는 방법을 살펴보겠습니다.

### <a name="creating-a-log-action-filter"></a>로그 작업 필터 만들기

사용자 지정 작업 필터를 작성 하는 방법을 보여 주기 위해 Visual Studio 출력 창에 컨트롤러 작업 처리 단계를 기록 하는 사용자 지정 작업 필터를 만듭니다. `LogActionFilter`은 목록 2에 포함 되어 있습니다.

**목록 2 – `ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

목록 2에서 `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`및 `OnResultExecuted()` 메서드는 모두 `Log()` 메서드를 호출 합니다. 메서드 이름과 현재 경로 데이터는 `Log()` 메서드에 전달 됩니다. `Log()` 메서드는 Visual Studio 출력 창에 메시지를 기록 합니다 (그림 2 참조).

[Visual Studio 출력 창에 쓰기 ![](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**그림 02**: Visual Studio 출력 창에 쓰기 ([전체 크기 이미지를 보려면 클릭](understanding-action-filters-cs/_static/image6.png))

목록 3의 홈 컨트롤러는 전체 컨트롤러 클래스에 로그 작업 필터를 적용할 수 있는 방법을 보여 줍니다. 홈 컨트롤러에서 노출 하는 작업 (`Index()` 메서드 또는 `About()` 메서드)이 호출 될 때마다 작업 처리 단계는 Visual Studio 출력 창에 로깅됩니다.

**목록 3 – `Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 작업 필터를 소개 했습니다. 권한 부여 필터, 작업 필터, 결과 필터 및 예외 필터와 같은 네 가지 유형의 필터에 대해 알아보았습니다. 또한 기본 `ActionFilterAttribute` 클래스에 대해 알아보았습니다.

마지막으로 간단한 작업 필터를 구현 하는 방법을 배웠습니다. Visual Studio 출력 창에 컨트롤러 작업을 처리 하는 단계를 기록 하는 로그 작업 필터를 만들었습니다.

> [!div class="step-by-step"]
> [이전](asp-net-mvc-routing-overview-cs.md)
> [다음](improving-performance-with-output-caching-cs.md)
