---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: 서비스 계층 (C#)으로 유효성 검사 Microsoft Docs
author: StephenWalther
description: 컨트롤러 작업 및 별도의 서비스 계층으로 유효성 검사 논리를 이동 하는 방법에 대해 알아봅니다. 이 자습서에서 Stephen Walther는 다음 방법을 설명 합니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: da1a1c9cc79a452eb0d7597810e86f7bcf6cd179
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78436607"
---
# <a name="validating-with-a-service-layer-c"></a>서비스 레이어를 사용한 유효성 검사(C#)

[Stephen Walther](https://github.com/StephenWalther)

> 컨트롤러 작업 및 별도의 서비스 계층으로 유효성 검사 논리를 이동 하는 방법에 대해 알아봅니다. 이 자습서에서 Stephen Walther는 컨트롤러 계층에서 서비스 계층을 격리 하 여 문제를 선명 하 게 분리 하는 방법을 설명 합니다.

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 한 가지 방법을 설명 하는 것입니다. 이 자습서에서는 컨트롤러의 유효성 검사 논리를 별도의 서비스 계층으로 이동 하는 방법에 대해 알아봅니다.

## <a name="separating-concerns"></a>문제 구분

ASP.NET MVC 응용 프로그램을 빌드하는 경우에는 데이터베이스 논리를 컨트롤러 작업 안에 넣지 않아야 합니다. 데이터베이스와 컨트롤러 논리를 함께 사용 하면 응용 프로그램을 시간이 지남에 따라 유지 하기가 더 어려워집니다. 모든 데이터베이스 논리를 별도의 리포지토리 계층에 저장 하는 것이 좋습니다.

예를 들어 목록 1은 ProductRepository 라는 간단한 리포지토리를 포함 합니다. 제품 리포지토리에는 응용 프로그램에 대 한 모든 데이터 액세스 코드가 포함 됩니다. 또한 목록에는 제품 리포지토리에서 구현 하는 IProductRepository 인터페이스가 포함 됩니다.

**목록 1--Models\ProductRepository.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

목록 2의 컨트롤러는 해당 Index () 및 Create () 작업에서 리포지토리 계층을 사용 합니다. 이 컨트롤러는 데이터베이스 논리를 포함 하지 않습니다. 리포지토리 계층을 만들면 문제를 완전히 분리 하 여 유지할 수 있습니다. 컨트롤러는 응용 프로그램 흐름 제어 논리를 담당 하며 리포지토리는 데이터 액세스 논리를 담당 합니다.

**목록 2-Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a>서비스 계층 만들기

따라서 응용 프로그램 흐름 제어 논리는 컨트롤러에 속하고 데이터 액세스 논리는 리포지토리에 속합니다. 이 경우 유효성 검사 논리를 어디에 배치 해야 하나요? 한 가지 옵션은 *서비스 계층*에 유효성 검사 논리를 추가 하는 것입니다.

서비스 계층은 컨트롤러와 리포지토리 계층 간의 통신을 중재 하는 ASP.NET MVC 응용 프로그램의 추가 계층입니다. 서비스 계층에는 비즈니스 논리가 포함 되어 있습니다. 특히 유효성 검사 논리를 포함 합니다.

예를 들어 목록 3의 제품 서비스 계층에는 CreateProduct () 메서드가 있습니다. CreateProduct () 메서드는 product 리포지토리에 제품을 전달 하기 전에 ValidateProduct () 메서드를 호출 하 여 새 제품의 유효성을 검사 합니다.

**목록 3-Models\ententservice.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

목록 4에서 제품 컨트롤러가 업데이트 되어 리포지토리 계층 대신 서비스 계층을 사용 합니다. 컨트롤러 계층은 서비스 계층에 대해 통신 합니다. 서비스 계층은 리포지토리 계층에 대해 통신 합니다. 각 계층에는 별도의 책임이 있습니다.

**목록 4-Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

Product service는 product controller 생성자에 생성 됩니다. 제품 서비스가 생성 되 면 모델 상태 사전이 서비스에 전달 됩니다. 제품 서비스는 모델 상태를 사용 하 여 유효성 검사 오류 메시지를 컨트롤러에 다시 전달 합니다.

## <a name="decoupling-the-service-layer"></a>서비스 계층 분리

컨트롤러 및 서비스 계층을 하나의 관점에서 격리 하지 못했습니다. 컨트롤러 및 서비스 계층은 모델 상태를 통해 통신 합니다. 즉, 서비스 계층은 ASP.NET MVC 프레임 워크의 특정 기능에 종속 됩니다.

가능 하면 컨트롤러 계층에서 서비스 계층을 격리 하려고 합니다. 이론적으로 ASP.NET MVC 응용 프로그램 뿐만 아니라 모든 유형의 응용 프로그램에서 서비스 계층을 사용할 수 있어야 합니다. 예를 들어 나중에 응용 프로그램에 대 한 WPF 프런트 엔드를 빌드할 수 있습니다. 서비스 계층에서 ASP.NET MVC 모델 상태에 대 한 종속성을 제거 하는 방법을 찾아야 합니다.

목록 5에서 서비스 계층은 더 이상 모델 상태를 사용 하지 않도록 업데이트 되었습니다. 대신, IValidationDictionary 인터페이스를 구현 하는 클래스를 사용 합니다.

**목록 5-Models\ProductService.cs (분리)**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

IValidationDictionary 인터페이스는 목록 6에 정의 되어 있습니다. 이 간단한 인터페이스에는 단일 메서드와 단일 속성이 있습니다.

**목록 6-Models\IValidationDictionary.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

ModelStateWrapper 클래스 라는 목록 7의 클래스는 IValidationDictionary 인터페이스를 구현 합니다. 모델 상태 사전을 생성자에 전달 하 여 ModelStateWrapper 클래스를 인스턴스화할 수 있습니다.

**목록 7-Models\ModelStateWrapper.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

마지막으로 목록 8의 업데이트 된 컨트롤러는 해당 생성자에서 서비스 계층을 만들 때 ModelStateWrapper를 사용 합니다.

**8-Controller\stvv 제품 목록 표시**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

IValidationDictionary 인터페이스 및 ModelStateWrapper 클래스를 사용 하 여 서비스 계층을 컨트롤러 계층에서 완전히 격리할 수 있습니다. 서비스 계층은 더 이상 모델 상태에 종속 되지 않습니다. IValidationDictionary 인터페이스를 구현 하는 모든 클래스를 서비스 계층에 전달할 수 있습니다. 예를 들어, WPF 응용 프로그램은 간단한 컬렉션 클래스를 사용 하 여 IValidationDictionary 인터페이스를 구현할 수 있습니다.

## <a name="summary"></a>요약

이 자습서의 목표는 ASP.NET MVC 응용 프로그램에서 유효성 검사를 수행 하는 방법에 대해 설명 하는 것입니다. 이 자습서에서는 모든 유효성 검사 논리를 컨트롤러에서 별도의 서비스 계층으로 이동 하는 방법을 배웠습니다. 또한 ModelStateWrapper 클래스를 만들어 컨트롤러 계층에서 서비스 계층을 분리 하는 방법을 배웠습니다.

> [!div class="step-by-step"]
> [이전](validating-with-the-idataerrorinfo-interface-cs.md)
> [다음](validation-with-the-data-annotation-validators-cs.md)
