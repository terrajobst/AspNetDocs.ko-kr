---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
title: ASP.NET MVC 컨트롤러 개요 (VB) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서 Stephen Walther는 ASP.NET MVC 컨트롤러를 소개 합니다. 새 컨트롤러를 만들고 다양 한 유형의 작업을 반환 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 02/16/2008
ms.assetid: 94c3e5d9-a904-445e-a34e-d92fd1ca108a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-controller-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f19e7dd7fc025de2e0c387db898d36623e790e6a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486923"
---
# <a name="aspnet-mvc-controller-overview-vb"></a>ASP.NET MVC 컨트롤러 개요(VB)

[Stephen Walther](https://github.com/StephenWalther)

> 이 자습서에서 Stephen Walther는 ASP.NET MVC 컨트롤러를 소개 합니다. 새 컨트롤러를 만들고 다른 유형의 작업 결과를 반환 하는 방법에 대해 알아봅니다.

이 자습서에서는 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 작업 결과 항목을 살펴봅니다. 이 자습서를 완료 한 후에는 컨트롤러가 ASP.NET MVC 웹 사이트와 상호 작용 하는 방식을 제어 하는 데 컨트롤러를 사용 하는 방법을 이해 하 게 됩니다.

## <a name="understanding-controllers"></a>컨트롤러 이해

MVC 컨트롤러는 ASP.NET MVC 웹 사이트에 대 한 요청에 응답 해야 합니다. 각 브라우저 요청은 특정 컨트롤러에 매핑됩니다. 예를 들어 브라우저의 주소 표시줄에 다음 URL을 입력 한다고 가정 합니다.

`http://localhost/Product/Index/3`

이 경우에는 제품 컨트롤러 라는 컨트롤러가 호출 됩니다. 제품 컨트롤러는 브라우저 요청에 대 한 응답을 생성 합니다. 예를 들어 컨트롤러가 특정 뷰를 브라우저에 다시 반환 하거나 컨트롤러가 사용자를 다른 컨트롤러로 리디렉션할 수 있습니다.

목록 1은 제품 컨트롤러 라는 간단한 컨트롤러를 포함 합니다.

**Listing1-Controllers\ProductController.vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample1.vb)]

목록 1에서 볼 수 있듯이 컨트롤러는 단지 클래스 (Visual Basic .NET 또는 C# 클래스)입니다. 컨트롤러는 기본 System.object 클래스에서 파생 되는 클래스입니다. 컨트롤러가이 기본 클래스에서 상속 하기 때문에 컨트롤러는 몇 가지 유용한 메서드를 무료로 상속 합니다 (이 메서드에 대해 잠시 설명).

## <a name="understanding-controller-actions"></a>컨트롤러 작업 이해

컨트롤러는 컨트롤러 작업을 노출 합니다. 작업은 브라우저 주소 표시줄에 특정 URL을 입력할 때 호출 되는 컨트롤러의 메서드입니다. 예를 들어 다음 URL에 대 한 요청을 수행 한다고 가정해 보겠습니다.

`http://localhost/Product/Index/3`

이 경우에는 Index () 메서드가 제품 컨트롤러 클래스에서 호출 됩니다. Index () 메서드는 컨트롤러 작업의 예입니다.

컨트롤러 작업은 컨트롤러 클래스의 공용 메서드 여야 합니다. Visual Basic.NET 메서드는 기본적으로 공용 메서드입니다. 컨트롤러 클래스에 추가 하는 공용 메서드는 컨트롤러 작업으로 자동으로 노출 됩니다. 예를 들어, 컨트롤러 작업은 간단 하 게 브라우저 주소 표시줄에 올바른 URL을 입력 하 여 universe의 모든 사용자가 호출할 수 있기 때문에 주의 해야 합니다.

컨트롤러 작업에서 충족 해야 하는 몇 가지 추가 요구 사항이 있습니다. 컨트롤러 작업으로 사용 되는 메서드는 오버 로드할 수 없습니다. 또한 컨트롤러 작업은 정적 메서드가 될 수 없습니다. 그 외에는 모든 메서드를 컨트롤러 작업으로 사용할 수 있습니다.

## <a name="understanding-action-results"></a>작업 결과 이해

컨트롤러 작업은 *작업 결과*라고 하는 항목을 반환 합니다. 작업 결과는 브라우저 요청에 대 한 응답으로 컨트롤러 작업에서 반환 하는 작업입니다.

ASP.NET MVC 프레임 워크는 다음과 같은 몇 가지 유형의 작업 결과를 지원 합니다.

1. ViewResult-HTML 및 태그를 나타냅니다.
2. EmptyResult-결과가 없음을 나타냅니다.
3. RedirectResult-새 URL로의 리디렉션을 나타냅니다.
4. JsonResult-AJAX 응용 프로그램에서 사용할 수 있는 JavaScript Object Notation 결과를 나타냅니다.
5. JavaScriptResult-JavaScript 스크립트를 나타냅니다.
6. ContentResult-텍스트 결과를 나타냅니다.
7. FileContentResult-다운로드 가능한 파일 (이진 콘텐츠 포함)을 나타냅니다.
8. FilePathResult-다운로드 가능한 파일 (경로 포함)을 나타냅니다.
9. FileStreamResult-다운로드 가능한 파일 (파일 스트림 포함)을 나타냅니다.

이러한 모든 작업 결과는 기본 ActionResult 클래스에서 상속 됩니다.

대부분의 경우 컨트롤러 작업은 ViewResult를 반환 합니다. 예를 들어 목록 2의 인덱스 컨트롤러 동작은 ViewResult를 반환 합니다.

**목록 2-controllers\bookcontroller**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample2.vb)]

작업에서 ViewResult를 반환 하면 HTML이 브라우저로 반환 됩니다. 목록 2의 Index () 메서드는 브라우저에 대 한 Index 라는 뷰를 반환 합니다.

목록 2의 Index () 동작은 ViewResult ()를 반환 하지 않습니다. 대신 컨트롤러 기본 클래스의 View () 메서드를 호출 합니다. 일반적으로 작업 결과를 직접 반환 하지 않습니다. 대신 컨트롤러 기본 클래스의 다음 메서드 중 하나를 호출 합니다.

1. View-ViewResult 작업 결과를 반환 합니다.
2. 리디렉션-RedirectResult 작업 결과를 반환 합니다.
3. RedirectToAction-RedirectToRouteResult 작업 결과를 반환 합니다.
4. RedirectToRoute-RedirectToRouteResult 작업 결과를 반환 합니다.
5. Json-JsonResult 작업 결과를 반환 합니다.
6. JavaScriptResult-JavaScriptResult을 반환 합니다.
7. 콘텐츠-ContentResult 작업 결과를 반환 합니다.
8. File-메서드에 전달 된 매개 변수에 따라 FileContentResult, FilePathResult 또는 FileStreamResult를 반환 합니다.

따라서 브라우저에 뷰를 반환 하려는 경우 View () 메서드를 호출 합니다. 한 컨트롤러 동작에서 다른 컨트롤러로 사용자를 리디렉션하려면 RedirectToAction () 메서드를 호출 합니다. 예를 들어 목록 3의 Details () 동작은 Id 매개 변수에 값이 있는지 여부에 따라 뷰를 표시 하거나 사용자를 Index () 동작으로 리디렉션합니다.

**목록 3-CustomerController .vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample3.vb)]

ContentResult 작업 결과는 특수 합니다. ContentResult 작업 결과를 사용 하 여 일반 텍스트로 작업 결과를 반환할 수 있습니다. 예를 들어 4를 나열 하는 Index () 메서드는 메시지를 HTML이 아닌 일반 텍스트로 반환 합니다.

**목록 4-Controllers\StatusController.vb**

> StatusController
> 
> 
> System.Web.Mvc.Controller

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample4.vb)]

StatusController. Index () 동작을 호출 하면 뷰가 반환 되지 않습니다. 대신 "Hello World!" 원시 텍스트가 이 브라우저에 반환 됩니다.

컨트롤러 작업이 작업 결과가 아닌 결과 (예: 날짜 또는 정수)를 반환 하는 경우 결과가 ContentResult에 자동으로 래핑됩니다. 예를 들어 목록 5에서 작업 컨트롤러의 Index () 동작을 호출 하면 해당 날짜는 자동으로 ContentResult로 반환 됩니다.

**목록 5-근무 컨트롤러 .vb**

[!code-vb[Main](asp-net-mvc-controller-overview-vb/samples/sample5.vb)]

목록 5의 Index () 동작은 DateTime 개체를 반환 합니다. ASP.NET MVC 프레임 워크는 DateTime 개체를 문자열로 변환 하 고 ContentResult의 DateTime 값을 자동으로 래핑합니다. 브라우저는 날짜와 시간을 일반 텍스트로 받습니다.

## <a name="summary"></a>요약

이 자습서에서는 ASP.NET MVC 컨트롤러, 컨트롤러 작업 및 컨트롤러 작업 결과에 대 한 개념을 소개 합니다. 첫 번째 섹션에서는 ASP.NET MVC 프로젝트에 새 컨트롤러를 추가 하는 방법을 알아보았습니다. 다음으로 컨트롤러의 공용 메서드를 컨트롤러 작업으로 universe에 노출 하는 방법을 배웠습니다. 마지막으로, 컨트롤러 작업에서 반환 될 수 있는 다양 한 유형의 작업 결과에 대해 설명 했습니다. 특히 컨트롤러 작업에서 ViewResult, RedirectToActionResult 및 ContentResult를 반환 하는 방법에 대해 설명 했습니다.

> [!div class="step-by-step"]
> [이전](creating-a-custom-route-constraint-cs.md)
> [다음](creating-custom-routes-vb.md)
