---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: ASP.NET MVC 응용 프로그램에 대 한 단위C#테스트 만들기 () | Microsoft Docs
author: StephenWalther
description: 컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 대해 알아봅니다. 이 자습서에서 Stephen Walther는 컨트롤러 작업에서 parti를 반환 하는지 여부를 테스트 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595291"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a>ASP.NET MVC 애플리케이션에 대한 단위 테스트 만들기(C#)

[Stephen Walther](https://github.com/StephenWalther)

[PDF 다운로드](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> 컨트롤러 작업에 대 한 단위 테스트를 만드는 방법에 대해 알아봅니다. 이 자습서에서 Stephen Walther는 컨트롤러 작업이 특정 뷰를 반환 하는지, 특정 데이터 집합을 반환 하는지 또는 다른 유형의 작업 결과를 반환 하는지를 테스트 하는 방법을 보여 줍니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 컨트롤러에 대 한 단위 테스트를 작성 하는 방법을 보여 주는 것입니다. 3 가지 유형의 단위 테스트를 빌드하는 방법을 설명 합니다. 컨트롤러 작업에서 반환 하는 뷰를 테스트 하는 방법, 컨트롤러 작업에서 반환 된 뷰 데이터를 테스트 하는 방법, 한 컨트롤러 작업이 두 번째 컨트롤러 작업으로 리디렉션하는 지 여부를 테스트 하는 방법을 알아봅니다.

## <a name="creating-the-controller-under-test"></a>테스트 중인 컨트롤러 만들기

먼저 테스트 하려는 컨트롤러를 만들어 보겠습니다. `ProductController`이라는 컨트롤러는 목록 1에 포함 되어 있습니다.

**목록 1 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

`ProductController`에는 `Index()` 및 `Details()`라는 두 개의 작업 메서드가 포함 되어 있습니다. 두 작업 메서드는 모두 뷰를 반환 합니다. `Details()` 작업은 Id 라는 매개 변수를 허용 합니다.

## <a name="testing-the-view-returned-by-a-controller"></a>컨트롤러에서 반환 된 뷰 테스트

`ProductController`에서 올바른 뷰를 반환 하는지 여부를 테스트 하려고 한다고 가정 합니다. `ProductController.Details()` 작업이 호출 될 때 세부 정보 뷰가 반환 되는지 확인 하려고 합니다. 목록 2의 테스트 클래스에는 `ProductController.Details()` 작업에서 반환 된 뷰를 테스트 하기 위한 단위 테스트가 포함 되어 있습니다.

**목록 2 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

목록 2의 클래스에는 `TestDetailsView()`이라는 테스트 메서드가 포함 되어 있습니다. 이 메서드에는 세 줄의 코드가 포함 되어 있습니다. 코드의 첫 번째 줄은 `ProductController` 클래스의 새 인스턴스를 만듭니다. 코드의 두 번째 줄은 컨트롤러의 `Details()` 작업 메서드를 호출 합니다. 마지막으로, 코드의 마지막 줄은 `Details()` 동작에서 반환 된 뷰가 자세히 뷰 인지 여부를 확인 합니다.

`ViewResult.ViewName` 속성은 컨트롤러에서 반환 된 뷰의 이름을 나타냅니다. 이 속성 테스트에 대 한 한 가지 큰 경고입니다. 컨트롤러에서 뷰를 반환 하는 방법에는 두 가지가 있습니다. 컨트롤러는 다음과 같이 명시적으로 뷰를 반환할 수 있습니다.

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

또는 다음과 같이 컨트롤러 작업의 이름에서 뷰 이름을 유추할 수 있습니다.

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

또한이 컨트롤러 작업은 `Details`라는 뷰를 반환 합니다. 그러나 뷰의 이름은 동작 이름에서 유추 됩니다. 뷰 이름을 테스트 하려면 컨트롤러 작업에서 뷰 이름을 명시적으로 반환 해야 합니다.

목록 2에서 키보드 조합 **Ctrl + R, A** 를 입력 하거나 **솔루션의 모든 테스트 실행** 단추를 클릭 하 여 단위 테스트를 실행할 수 있습니다 (그림 1 참조). 테스트가 통과 되 면 그림 2에 테스트 결과 창이 표시 됩니다.

[![솔루션의 모든 테스트 실행](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

**그림 01**: 솔루션에서 모든 테스트 실행 ([전체 크기 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))

[성공 ![](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

**그림 02**: 성공! ([전체 크기 이미지를 보려면 클릭](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))

## <a name="testing-the-view-data-returned-by-a-controller"></a>컨트롤러에서 반환 된 뷰 데이터 테스트

MVC 컨트롤러는 *`View Data`* 이라는 항목을 사용 하 여 뷰에 데이터를 전달 합니다. 예를 들어 `ProductController Details()` 작업을 호출할 때 특정 제품에 대 한 세부 정보를 표시 하려는 경우를 가정해 보겠습니다. 이 경우 모델에 정의 된 `Product` 클래스의 인스턴스를 만들고 `View Data`를 활용 하 여 `Details` 뷰에 인스턴스를 전달할 수 있습니다.

목록 3의 수정 된 `ProductController`에는 제품을 반환 하는 업데이트 된 `Details()` 작업이 포함 됩니다.

**목록 3 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

먼저 `Details()` 작업은 랩톱 컴퓨터를 나타내는 `Product` 클래스의 새 인스턴스를 만듭니다. 그런 다음 `Product` 클래스의 인스턴스가 `View()` 메서드에 두 번째 매개 변수로 전달 됩니다.

필요한 데이터가 뷰 데이터에 포함 되어 있는지 여부를 테스트 하는 단위 테스트를 작성할 수 있습니다. 목록 4에서 단위 테스트는 `ProductController Details()` 작업 메서드를 호출할 때 랩톱 컴퓨터를 나타내는 제품이 반환 되는지 여부를 테스트 합니다.

**목록 4 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

목록 4에서 `TestDetailsView()` 메서드는 `Details()` 메서드를 호출 하 여 반환 된 뷰 데이터를 테스트 합니다. `ViewData`은 `Details()` 메서드를 호출 하 여 반환 되는 `ViewResult` 속성으로 노출 됩니다. `ViewData.Model` 속성은 뷰에 전달 된 제품을 포함 합니다. 테스트는 보기 데이터에 포함 된 제품의 이름이 랩톱 인지 확인 합니다.

## <a name="testing-the-action-result-returned-by-a-controller"></a>컨트롤러에서 반환 하는 작업 결과 테스트

더 복잡 한 컨트롤러 작업은 컨트롤러 작업에 전달 되는 매개 변수의 값에 따라 다른 유형의 작업 결과를 반환할 수 있습니다. 컨트롤러 작업은 `ViewResult`, `RedirectToRouteResult`또는 `JsonResult`를 포함 하 여 다양 한 유형의 작업 결과를 반환할 수 있습니다.

예를 들어 목록 5에서 수정 된 `Details()` 작업은 올바른 제품 Id를 작업에 전달할 때 `Details` 뷰를 반환 합니다. 1 보다 작은 값이 포함 된 Id로 잘못 된 제품 Id를 전달 하면 `Index()` 작업으로 리디렉션됩니다.

**목록 5 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

목록 6에서 단위 테스트를 사용 하 여 `Details()` 작업의 동작을 테스트할 수 있습니다. 목록 6의 단위 테스트는 값이-1 인 Id가 `Details()` 메서드에 전달 될 때 `Index` 뷰로 리디렉션되도록 확인 합니다.

**목록 6 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

컨트롤러 작업에서 `RedirectToAction()` 메서드를 호출 하면 컨트롤러 작업에서 `RedirectToRouteResult`을 반환 합니다. 테스트는 `RedirectToRouteResult` 사용자를 `Index`라는 컨트롤러 작업으로 리디렉션할지 여부를 확인 합니다.

## <a name="summary"></a>요약

이 자습서에서는 MVC 컨트롤러 작업에 대 한 단위 테스트를 작성 하는 방법을 배웠습니다. 먼저 컨트롤러 작업에서 올바른 뷰가 반환 되는지 여부를 확인 하는 방법을 배웠습니다. `ViewResult.ViewName` 속성을 사용 하 여 뷰의 이름을 확인 하는 방법을 배웠습니다.

다음으로 `View Data`의 콘텐츠를 테스트할 수 있는 방법을 검토 했습니다. 컨트롤러 작업을 호출한 후 `View Data`에서 올바른 제품이 반환 되었는지 여부를 확인 하는 방법을 배웠습니다.

마지막으로 컨트롤러 작업에서 다른 유형의 작업 결과가 반환 되는지 여부를 테스트 하는 방법에 대해 설명 했습니다. 컨트롤러에서 `ViewResult` 또는 `RedirectToRouteResult`를 반환 하는지 여부를 테스트 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [다음](creating-unit-tests-for-asp-net-mvc-applications-vb.md)
