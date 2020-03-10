---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 작업 만들기 (VB) | Microsoft Docs
author: microsoft
description: ASP.NET MVC 컨트롤러에 새 작업을 추가 하는 방법에 대해 알아봅니다. 메서드가 동작 하기 위한 요구 사항에 대해 알아봅니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: b1b53bea899deecef203551b23c087944e3990ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470159"
---
# <a name="creating-an-action-vb"></a>작업 만들기(VB)

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET MVC 컨트롤러에 새 작업을 추가 하는 방법에 대해 알아봅니다. 메서드가 동작 하기 위한 요구 사항에 대해 알아봅니다.

이 자습서의 목표는 새 컨트롤러 작업을 만드는 방법을 설명 하는 것입니다. 작업 방법의 요구 사항에 대해 알아봅니다. 메서드가 작업으로 노출 되지 않도록 하는 방법에 대해서도 알아봅니다.

## <a name="adding-an-action-to-a-controller"></a>컨트롤러에 작업 추가

컨트롤러에 새 메서드를 추가 하 여 컨트롤러에 새 작업을 추가 합니다. 예를 들어 1을 나열 하는 컨트롤러에는 Index () 라는 작업과 SayHello () 라는 동작이 포함 되어 있습니다. 두 메서드는 모두 작업으로 노출 됩니다.

**목록 1-Controllers\HomeController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

작업으로 universe에 노출 되기 위해 메서드는 특정 요구 사항을 충족 해야 합니다.

- 메서드는 public 이어야 합니다.
- 메서드는 정적 메서드 일 수 없습니다.
- 메서드는 확장 메서드 일 수 없습니다.
- 메서드는 생성자, getter 또는 setter가 될 수 없습니다.
- 이 메서드에는 개방형 제네릭 형식을 사용할 수 없습니다.
- 메서드가 컨트롤러 기본 클래스의 메서드가 아닙니다.
- 메서드는 **ref** 또는 **out** 매개 변수를 포함할 수 없습니다.

컨트롤러 작업의 반환 형식에 대 한 제한은 없습니다. 컨트롤러 작업은 문자열, 날짜/시간, 임의 클래스의 인스턴스 또는 void를 반환할 수 있습니다. ASP.NET MVC 프레임 워크는 작업 결과가 아닌 반환 형식을 문자열로 변환 하 고 브라우저에 문자열을 렌더링 합니다.

이러한 요구 사항을 위반 하지 않는 메서드를 컨트롤러에 추가 하면 메서드가 컨트롤러 작업으로 노출 됩니다. 여기에서 주의 하세요. 컨트롤러 작업은 인터넷에 연결 된 모든 사용자가 호출할 수 있습니다. 예를 들어 DeleteMyWebsite () 컨트롤러 작업을 만들 수 없습니다.

## <a name="preventing-a-public-method-from-being-invoked"></a>Public 메서드가 호출 되지 않도록 방지

컨트롤러 클래스에서 공용 메서드를 만들어야 하는데 컨트롤러 작업으로 메서드를 노출 하지 않으려는 경우 &lt;NonAction&gt; 특성을 사용 하 여 메서드가 호출 되지 않도록 할 수 있습니다. 예를 들어 목록 2의 컨트롤러에는 &lt;NonAction&gt; 특성으로 데코레이팅된 CompanySecrets () 라는 공용 메서드가 포함 되어 있습니다.

**목록 2-Controllerss\ststomom.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

브라우저의 주소 표시줄에/Work/CompanySecrets를 입력 하 여 CompanySecrets () 컨트롤러 작업을 호출 하려고 하면 그림 1에 표시 된 오류 메시지가 표시 됩니다.

[비 작업 메서드를 호출 하 ![](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**그림 01**: nonaction 메서드 호출 ([전체 크기 이미지를 보려면 클릭](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [이전](creating-a-controller-vb.md)
> [다음](aspnet-mvc-controllers-overview-cs.md)
