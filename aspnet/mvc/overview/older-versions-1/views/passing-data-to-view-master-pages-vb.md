---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 보기 마스터 페이지에 데이터 전달 (VB) | Microsoft Docs
author: microsoft
description: 이 자습서의 목표는 컨트롤러에서 뷰 마스터 페이지로 데이터를 전달 하는 방법을 설명 하는 것입니다. 보기에 데이터를 전달 하기 위한 두 가지 전략을 살펴봅니다.
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9f768f47557adedc43cebfa2c092014bba5842de
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593691"
---
# <a name="passing-data-to-view-master-pages-vb"></a>보기 마스터 페이지에 데이터 전달(VB)

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> 이 자습서의 목표는 컨트롤러에서 뷰 마스터 페이지로 데이터를 전달 하는 방법을 설명 하는 것입니다. 보기 마스터 페이지에 데이터를 전달 하기 위한 두 가지 전략을 살펴봅니다. 먼저 응용 프로그램을 유지 관리 하기 어려운 쉬운 솔루션에 대해 설명 합니다. 다음으로, 좀 더 많은 초기 작업을 필요로 하는 훨씬 더 나은 솔루션을 검토 하 고 더 많은 유지 관리 가능한 응용 프로그램을 생성 합니다.

## <a name="passing-data-to-view-master-pages"></a>보기 마스터 페이지에 데이터 전달

이 자습서의 목표는 컨트롤러에서 뷰 마스터 페이지로 데이터를 전달 하는 방법을 설명 하는 것입니다. 보기 마스터 페이지에 데이터를 전달 하기 위한 두 가지 전략을 살펴봅니다. 먼저 응용 프로그램을 유지 관리 하기 어려운 쉬운 솔루션에 대해 설명 합니다. 다음으로, 좀 더 많은 초기 작업을 필요로 하는 훨씬 더 나은 솔루션을 검토 하 고 더 많은 유지 관리 가능한 응용 프로그램을 생성 합니다.

### <a name="the-problem"></a>문제

동영상 데이터베이스 응용 프로그램을 빌드하고 응용 프로그램의 모든 페이지에 영화 범주 목록을 표시 하려는 경우를 가정 합니다 (그림 1 참조). 또한 영화 범주 목록이 데이터베이스 테이블에 저장 되어 있다고 가정 합니다. 이 경우 데이터베이스에서 범주를 검색 하 고 보기 마스터 페이지 내에서 동영상 범주 목록을 렌더링 하는 것이 좋습니다.

[보기 마스터 페이지에서 동영상 범주를 표시 ![](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)

**그림 01**: 보기 마스터 페이지에서 동영상 범주 표시 ([전체 크기 이미지를 보려면 클릭](passing-data-to-view-master-pages-vb/_static/image3.png))

문제는 다음과 같습니다. 마스터 페이지에서 영화 범주의 목록을 검색 하려면 어떻게 해야 하나요? 마스터 페이지에서 직접 모델 클래스의 메서드를 호출 하는 것이 좋습니다. 즉, 마스터 페이지에서 데이터베이스의 데이터를 검색 하는 코드를 포함 하는 것이 좋습니다. 그러나 MVC 컨트롤러를 우회 하 여 데이터베이스에 액세스 하면 MVC 응용 프로그램을 빌드할 때의 주요 이점 중 하나인 문제를 명확 하 게 분리 하는 것을 위반할 수 있습니다.

Mvc 응용 프로그램에서 mvc 뷰와 mvc 모델 간의 모든 상호 작용을 MVC 컨트롤러에서 처리 해야 합니다. 이러한 문제를 분리 하면 더 쉽게 유지 관리, 조정 및 테스트 가능한 응용 프로그램을 생성 합니다.

MVC 응용 프로그램에서 보기 마스터 페이지를 포함 하 여 뷰로 전달 되는 모든 데이터는 컨트롤러 작업에 의해 뷰로 전달 되어야 합니다. 또한 데이터는 뷰 데이터를 활용 하 여 전달 해야 합니다. 이 자습서의 나머지 부분에서는 뷰 데이터를 뷰 마스터 페이지에 전달 하는 두 가지 방법을 살펴보겠습니다.

### <a name="the-simple-solution"></a>간단한 솔루션

컨트롤러에서 뷰 마스터 페이지로의 뷰 데이터를 전달 하는 가장 간단한 솔루션부터 살펴보겠습니다. 가장 간단한 해결 방법은 각 및 모든 컨트롤러 작업에서 마스터 페이지에 대 한 뷰 데이터를 전달 하는 것입니다.

목록 1의 컨트롤러를 고려 합니다. `Index()` 및 `Details()`라는 두 개의 동작을 노출 합니다. `Index()` 동작 메서드는 동영상 데이터베이스 테이블의 모든 동영상을 반환 합니다. `Details()` 동작 메서드는 특정 영화 범주의 모든 영화를 반환 합니다.

**목록 1 – `Controllers\HomeController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

`Index()`와 `Details()` 동작은 모두 데이터를 볼 두 개의 항목을 추가 합니다. `Index()` 작업은 범주와 영화 라는 두 개의 키를 추가 합니다. 범주 키는 마스터 보기 페이지에 표시 되는 영화 범주의 목록을 나타냅니다. 영화 키는 인덱스 뷰 페이지에 표시 되는 동영상 목록을 나타냅니다.

또한 `Details()` 작업은 범주 및 영화 라는 두 개의 키를 추가 합니다. 범주 키는 다시 한 번, 보기 마스터 페이지에서 표시 하는 영화 범주의 목록을 나타냅니다. 영화 키는 자세히 보기 페이지에 표시 되는 특정 범주의 동영상 목록을 나타냅니다 (그림 2 참조).

[자세히 보기 ![](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)

**그림 02**: 자세히 보기 ([전체 크기 이미지를 보려면 클릭](passing-data-to-view-master-pages-vb/_static/image6.png))

인덱스 뷰는 목록 2에 포함 되어 있습니다. 단순히 데이터 보기에서 영화 항목이 나타내는 영화 목록을 반복 합니다.

**목록 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

보기 마스터 페이지는 목록 3에 포함 되어 있습니다. 뷰 마스터 페이지는 뷰 데이터의 범주 항목이 나타내는 모든 동영상 범주를 반복 하 고 렌더링 합니다.

**목록 3 – `Views\Shared\Site.master`**

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

모든 데이터는 뷰 데이터를 통해 뷰 및 뷰 마스터 페이지에 전달 됩니다. 이는 마스터 페이지에 데이터를 전달 하는 올바른 방법입니다.

그렇다면이 솔루션에는 무엇이 잘못 되었나요? 문제는이 솔루션이 마른 (반복 금지) 원칙을 위반 하는 것입니다. 각 및 모든 컨트롤러 작업은 데이터를 보기 위해 동일한 동영상 범주 목록을 추가 해야 합니다. 응용 프로그램에 중복 코드가 있으면 응용 프로그램을 유지 관리, 조정 및 수정 하기가 훨씬 더 어려워집니다.

### <a name="the-good-solution"></a>좋은 솔루션

이 섹션에서는 컨트롤러 작업에서 뷰 마스터 페이지로 데이터를 전달 하는 대안 및 더 나은 솔루션을 살펴봅니다. 각 및 모든 컨트롤러 작업에서 마스터 페이지의 동영상 범주를 추가 하는 대신, 보기 데이터에 영화 범주를 한 번만 추가 합니다. 보기 마스터 페이지에서 사용 하는 모든 뷰 데이터는 응용 프로그램 컨트롤러에 추가 됩니다.

ApplicationController 클래스는 목록 4에 포함 되어 있습니다.

ApplicationController 클래스는 목록 4에 포함 되어 있습니다.

**목록 4 – `Controllers\ApplicationController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

목록 4에서는 응용 프로그램 컨트롤러에 대해 세 가지 사항을 확인 해야 합니다. 먼저 클래스가 기본 system.string 클래스에서 상속 되는지 확인 합니다. 응용 프로그램 컨트롤러는 컨트롤러 클래스입니다.

둘째, 응용 프로그램 컨트롤러 클래스는 MustInherit 클래스입니다. MustInherit 클래스는 구체적 클래스에서 구현 해야 하는 클래스입니다. 응용 프로그램 컨트롤러는 MustInherit 클래스 이므로 클래스에 정의 된 메서드를 직접 호출할 수 없습니다. 응용 프로그램 클래스를 직접 호출 하려고 하면 리소스를 찾을 수 없습니다. 오류 메시지가 표시 됩니다.

셋째, 응용 프로그램 컨트롤러에는 데이터를 볼 수 있는 영화 범주의 목록을 추가 하는 생성자가 포함 되어 있습니다. 응용 프로그램 컨트롤러에서 상속 되는 모든 컨트롤러 클래스는 응용 프로그램 컨트롤러의 생성자를 자동으로 호출 합니다. 응용 프로그램 컨트롤러에서 상속 하는 모든 컨트롤러에서 작업을 호출할 때마다 동영상 범주가 자동으로 보기 데이터에 포함 됩니다.

목록 5의 동영상 컨트롤러는 응용 프로그램 컨트롤러에서 상속 됩니다.

**목록 5 – `Controllers\MoviesController.vb`**

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

이전 섹션에서 설명한 Home 컨트롤러와 마찬가지로 영화 컨트롤러는 `Index()` 및 `Details()`라는 두 개의 작업 메서드를 노출 합니다. 보기 마스터 페이지에 표시 되는 영화 범주의 목록이 `Index()` 또는 `Details()` 방법 중 하나에서 데이터를 볼 수 있도록 추가 되지 않습니다. 동영상 컨트롤러는 응용 프로그램 컨트롤러에서 상속 되기 때문에 데이터를 자동으로 볼 수 있도록 동영상 범주 목록이 추가 됩니다.

보기 마스터 페이지에 대 한 뷰 데이터를 추가 하는이 솔루션은 마른 (반복 금지) 원칙을 위반 하지 않습니다. 데이터를 보기 위해 동영상 범주 목록을 추가 하는 코드는 한 위치 (응용 프로그램 컨트롤러에 대 한 생성자)에만 포함 되어 있습니다.

### <a name="summary"></a>요약

이 자습서에서는 컨트롤러에서 뷰 마스터 페이지로 뷰 데이터를 전달 하는 두 가지 방법에 대해 설명 했습니다. 첫째, 간단 하 게 검사 했지만 접근 방식을 유지 하기 어렵습니다. 첫 번째 섹션에서는 응용 프로그램의 모든 컨트롤러 작업에서 보기 마스터 페이지에 대 한 뷰 데이터를 추가 하는 방법에 대해 설명 했습니다. 이는 마른 (반복 금지) 원칙을 위반 하기 때문에 잘못 된 방법 이었습니다.

다음으로는 보기 마스터 페이지에서 데이터를 보는 데 필요한 데이터를 추가 하기 위한 훨씬 더 나은 전략을 검토 했습니다. 각 및 모든 컨트롤러 작업에서 뷰 데이터를 추가 하는 대신 응용 프로그램 컨트롤러 내에서 뷰 데이터를 한 번만 추가 했습니다. 이렇게 하면 ASP.NET MVC 응용 프로그램에서 뷰 마스터 페이지로 데이터를 전달할 때 중복 코드를 방지할 수 있습니다.

> [!div class="step-by-step"]
> [이전](creating-page-layouts-with-view-master-pages-vb.md)
