---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC 라우팅 개요 (VB) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서 Stephen Walther는 ASP.NET MVC 프레임 워크에서 브라우저 요청을 컨트롤러 작업에 매핑하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486899"
---
# <a name="aspnet-mvc-routing-overview-vb"></a>ASP.NET MVC 라우팅 개요(VB)

[Stephen Walther](https://github.com/StephenWalther)

> 이 자습서에서 Stephen Walther는 ASP.NET MVC 프레임 워크에서 브라우저 요청을 컨트롤러 작업에 매핑하는 방법을 보여 줍니다.

이 자습서에서는 *ASP.NET Routing*이라는 모든 ASP.NET MVC 응용 프로그램의 중요 한 기능을 소개 합니다. ASP.NET 라우팅 모듈은 들어오는 브라우저 요청을 특정 MVC 컨트롤러 작업에 매핑하는 작업을 담당 합니다. 이 자습서를 마치면 표준 경로 테이블에서 컨트롤러 작업에 요청을 매핑하는 방법이 이해 됩니다.

## <a name="using-the-default-route-table"></a>기본 경로 테이블 사용

새 ASP.NET MVC 응용 프로그램을 만들 때 응용 프로그램은 이미 ASP.NET 라우팅을 사용 하도록 구성 되어 있습니다. ASP.NET 라우팅은 두 위치에 설치 됩니다.

먼저 ASP.NET 라우팅은 응용 프로그램의 웹 구성 파일 (web.config 파일)에서 사용 하도록 설정 됩니다. 구성 파일에는 경로와 관련 된 4 개의 섹션, 즉 system.web. httpModules 섹션, system.web. httpHandlers 섹션, system.webserver 섹션 및 system.webserver와 같은 4 개의 섹션이 있습니다. 이러한 섹션을 사용 하지 않으면 라우팅이 더 이상 작동 하지 않으므로 이러한 섹션을 삭제 하지 않도록 주의 해야 합니다.

둘째, 더 중요 한 점은 응용 프로그램의 Global.asax 파일에 경로 테이블이 생성 되는 것입니다. Global.asax 파일은 ASP.NET 응용 프로그램 수명 주기 이벤트에 대 한 이벤트 처리기를 포함 하는 특수 파일입니다. 경로 테이블은 응용 프로그램 시작 이벤트 중에 생성 됩니다.

목록 1의 파일에는 ASP.NET MVC 응용 프로그램에 대 한 기본 global.asax 파일이 포함 되어 있습니다.

**목록 1-global.asax .vb**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

MVC 응용 프로그램이 처음 시작 될 때 응용 프로그램\_Start () 메서드가 호출 됩니다. 이 메서드는 RegisterRoutes () 메서드를 차례로 호출 합니다. RegisterRoutes () 메서드는 경로 테이블을 만듭니다.

기본 경로 테이블에는 단일 경로 (기본값)가 포함 되어 있습니다. 기본 경로는 URL의 첫 번째 세그먼트를 컨트롤러 이름에 매핑하고, URL의 두 번째 세그먼트를 컨트롤러 작업에 매핑하고, 세 번째 세그먼트는 **id**라는 매개 변수에 매핑합니다.

웹 브라우저의 주소 표시줄에 다음 URL을 입력 한다고 가정 합니다.

/Home/Index/3

기본 경로는이 URL을 다음 매개 변수에 매핑합니다.

- 컨트롤러 = 홈

- 작업 = 인덱스

- id = 3

URL/Home/Index/3를 요청 하면 다음 코드가 실행 됩니다.

HomeController.Index(3)

기본 경로에는 세 매개 변수 모두에 대 한 기본값이 포함 됩니다. 컨트롤러를 제공 하지 않으면 컨트롤러 매개 변수의 기본값은 **Home**입니다. 동작을 제공 하지 않으면 action 매개 변수의 기본값은 value **Index**로 설정 됩니다. 마지막으로 id를 제공 하지 않으면 id 매개 변수의 기본값은 빈 문자열입니다.

기본 경로에서 Url을 컨트롤러 작업에 매핑하는 방법에 대 한 몇 가지 예를 살펴보겠습니다. 브라우저 주소 표시줄에 다음 URL을 입력 한다고 가정 합니다.

/Home

기본 경로 매개 변수 기본값으로 인해이 URL을 입력 하면 목록 2에서 HomeController 클래스의 Index () 메서드가 호출 됩니다.

**목록 2-HomeController**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

목록 2에서 HomeController 클래스에는 Id 라는 단일 매개 변수를 허용 하는 Index () 라는 메서드가 포함 되어 있습니다. URL/Home를 사용 하면 Id 매개 변수의 값으로 Nothing 값을 사용 하 여 Index () 메서드를 호출할 수 있습니다.

MVC 프레임 워크는 컨트롤러 작업을 호출 하는 방식 때문에 URL/Home는 목록 3에 있는 HomeController 클래스의 Index () 메서드와도 일치 합니다.

**목록 3-HomeController (매개 변수가 없는 인덱스 동작)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

목록 3의 Index () 메서드는 매개 변수를 허용 하지 않습니다. URL/Home는이 Index () 메서드를 호출 합니다. 또한 URL/Home/Index/3는이 메서드를 호출 합니다 (Id는 무시 됨).

URL/Home는 목록 4에 있는 HomeController 클래스의 Index () 메서드와도 일치 합니다.

**목록 4-HomeController (nullable 매개 변수가 있는 인덱스 작업)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

목록 4에서 Index () 메서드에 하나의 정수 매개 변수가 있습니다. 매개 변수는 null을 허용 하는 매개 변수 이므로 값을 지정할 수 없습니다. 오류를 발생 시 키 지 않고 인덱스 ()를 호출할 수 있습니다.

마지막으로, URL/Home를 사용 하 여 5 목록에서 Index () 메서드를 호출 하면 Id 매개 변수가 null을 허용 하는 매개 변수가 *아니기* 때문에 예외가 발생 합니다. Index () 메서드를 호출 하려고 하면 그림 1에 표시 된 오류가 표시 됩니다.

**목록 5-HomeController (Id 매개 변수가 있는 인덱스 작업)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

[매개 변수 값을 필요로 하는 컨트롤러 작업 호출 ![](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)

**그림 01**: 매개 변수 값을 필요로 하는 컨트롤러 작업 호출 ([전체 크기 이미지를 보려면 클릭](asp-net-mvc-routing-overview-vb/_static/image2.png))

반면에 URL/Home/Index/3는 목록 5의 인덱스 컨트롤러 작업에만 제대로 작동 합니다. Request/Home/Index/3를 사용 하면 값이 3 인 Id 매개 변수를 사용 하 여 Index () 메서드를 호출할 수 있습니다.

## <a name="summary"></a>요약

이 자습서의 목표는 ASP.NET 라우팅에 대 한 간략 한 소개를 제공 하는 것 이었습니다. 새 ASP.NET MVC 응용 프로그램을 사용 하 여 얻을 수 있는 기본 경로 테이블을 검사 했습니다. 기본 경로에서 Url을 컨트롤러 작업에 매핑하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](creating-an-action-cs.md)
> [다음](understanding-action-filters-vb.md)
