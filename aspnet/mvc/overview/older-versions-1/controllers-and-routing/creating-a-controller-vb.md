---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
title: 컨트롤러 만들기 (VB) | Microsoft Docs
author: StephenWalther
description: 이 자습서에서 Stephen Walther는 ASP.NET MVC 응용 프로그램에 컨트롤러를 추가 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 204b7e86-f560-4611-8adb-785b33e777b9
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
msc.type: authoredcontent
ms.openlocfilehash: 60636b79ab5fc06ca904dee90ce74f256e046d12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486833"
---
# <a name="creating-a-controller-vb"></a>컨트롤러 만들기(VB)

[Stephen Walther](https://github.com/StephenWalther)

> 이 자습서에서 Stephen Walther는 ASP.NET MVC 응용 프로그램에 컨트롤러를 추가 하는 방법을 보여 줍니다.

이 자습서의 목표는 새 ASP.NET MVC 컨트롤러를 만드는 방법을 설명 하는 것입니다. Visual Studio 컨트롤러 추가 메뉴 옵션을 사용 하 고 직접 클래스 파일을 만들어 컨트롤러를 만드는 방법에 대해 알아봅니다.

### <a name="using-the-add-controller-menu-option"></a>컨트롤러 추가 메뉴 옵션 사용

새 컨트롤러를 만드는 가장 쉬운 방법은 Visual Studio 솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 컨트롤러** 메뉴 옵션을 선택 하는 것입니다 (그림 1 참조). 이 메뉴 옵션을 선택 하면 **컨트롤러 추가** 대화 상자가 열립니다 (그림 2 참조).

[새 프로젝트 대화 상자 ![](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)

**그림 01**: 새 컨트롤러 추가 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-vb/_static/image2.png))

[새 프로젝트 대화 상자 ![](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)

**그림 02**: 컨트롤러 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-vb/_static/image4.png))

컨트롤러 이름의 첫 번째 부분은 **컨트롤러 추가** 대화 상자에서 강조 표시 됩니다. 모든 컨트롤러 이름은 접미사 *컨트롤러로*끝나야 합니다. 예를 들어 Product *controller* 라는 컨트롤러가 아니라 *Product*라는 컨트롤러를 만들 수 있습니다.

*컨트롤러 접미사가 없는* 컨트롤러를 만드는 경우 컨트롤러를 호출할 수 없습니다. 이 작업을 수행 하지 마세요 .이 작업을 수행한 후에는 많은 시간 동안 지속 됩니다.

**목록 1-Controller\entstomom.xml**

[!code-vb[Main](creating-a-controller-vb/samples/sample1.vb)]

항상 controllers 폴더에 컨트롤러를 만들어야 합니다. 그렇지 않으면 ASP.NET MVC의 규칙을 위반 하 게 됩니다. 다른 개발자는 응용 프로그램을 이해 하는 데 더 많은 시간이 걸립니다.

### <a name="scaffolding-action-methods"></a>스 캐 폴딩 작업 메서드

컨트롤러를 만들 때 만들기, 업데이트 및 세부 정보 작업 메서드를 자동으로 생성 하는 옵션이 있습니다 (그림 3 참조). 이 옵션을 선택 하면 목록 2의 컨트롤러 클래스가 생성 됩니다.

[작업 메서드 자동 생성 ![](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)

**그림 03**: 자동으로 작업 메서드 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-vb/_static/image6.png))

**목록 2-Controllers\CustomerController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample2.vb)]

이러한 생성 된 메서드는 스텁 메서드입니다. 고객에 대 한 세부 정보를 만들고, 업데이트 하 고, 표시 하는 실제 논리를 추가 해야 합니다. 그러나 스텁 메서드는 좋은 시작 지점을 제공 합니다.

### <a name="creating-a-controller-class"></a>컨트롤러 클래스 만들기

ASP.NET MVC 컨트롤러는 클래스 일 뿐입니다. 원하는 경우 편리한 Visual Studio 컨트롤러 스 캐 폴딩을 무시 하 고 컨트롤러 클래스를 직접 만들 수 있습니다. 다음 단계를 수행하세요.

1. Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목** 을 차례로 선택한 다음 **클래스** 템플릿을 선택 합니다 (그림 4 참조).
2. 새 클래스 이름을 PersonController로 하 고 **추가** 단추를 클릭 합니다.
3. 클래스가 기본 System.object 클래스에서 상속 하도록 결과 클래스 파일을 수정 합니다 (목록 3 참조).

[새 클래스를 만드는 ![](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)

**그림 04**: 새 클래스 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-controller-vb/_static/image8.png))

**목록 3-Controllers\PersonController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample3.vb)]

목록 3의 컨트롤러는 "Hello World!" 문자열을 반환 하는 Index () 라는 하나의 동작을 노출 합니다. 응용 프로그램을 실행 하 고 다음과 같은 URL을 요청 하 여이 컨트롤러 작업을 호출할 수 있습니다.

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET 개발 서버는 임의의 포트 번호 (예: 40071)를 사용 합니다. 컨트롤러를 호출 하는 데 사용할 URL을 입력 하는 경우 올바른 포트 번호를 제공 해야 합니다. 화면 오른쪽 아래에 있는 Windows 알림 영역에서 ASP.NET 개발 서버 아이콘 위에 마우스를 가져가면 포트 번호를 확인할 수 있습니다.
> 
> [!div class="step-by-step"]
> [이전](adding-dynamic-content-to-a-cached-page-vb.md)
> [다음](creating-an-action-vb.md)
