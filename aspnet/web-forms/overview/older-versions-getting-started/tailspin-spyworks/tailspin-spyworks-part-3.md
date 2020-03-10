---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: '3 부: 레이아웃 및 범주 메뉴 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 3 부에서는 레이아웃 및 범주 메뉴 추가에 대해 설명 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519101"
---
# <a name="part-3-layout-and-category-menu"></a>3 부: 레이아웃 및 범주 메뉴

만든 사람 [Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다. ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 3 부에서는 레이아웃 및 범주 메뉴 추가에 대해 설명 합니다.

## <a id="_Toc260221669"></a>일부 레이아웃 및 범주 메뉴 추가

사이트 마스터 페이지에서 제품 범주 메뉴가 포함 될 왼쪽 열에 대해 div를 추가 합니다.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

원하는 맞춤 및 기타 서식 지정은 스타일 .css 파일에 추가한 CSS 클래스에서 제공 합니다.

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

제품 범주 메뉴는 기존 제품 범주에 대 한 Commerce 데이터베이스를 쿼리하고 메뉴 항목과 해당 링크를 만들어 런타임에 동적으로 생성 됩니다.

이를 위해 두 개의 ASP를 사용 합니다. 네트워크의 강력한 데이터 컨트롤입니다. "엔터티 데이터 원본" 컨트롤 및 "ListView" 컨트롤입니다.

![](tailspin-spyworks-part-3/_static/image1.jpg)

"디자인 뷰"로 전환 하 고 도우미를 사용 하 여 컨트롤을 구성 하겠습니다.

![](tailspin-spyworks-part-3/_static/image2.jpg)

EntityDataSource ID 속성을 EDS\_Category\_메뉴로 설정 하 고 "데이터 소스 구성"을 클릭 합니다.

![](tailspin-spyworks-part-3/_static/image3.jpg)

상거래 데이터베이스용 엔터티 데이터 원본 모델을 만들 때 생성 된 주석 Erceentities 연결을 선택 하 고 "다음"을 클릭 합니다.

![](tailspin-spyworks-part-3/_static/image4.jpg)

"범주" 엔터티 집합 이름을 선택 하 고 나머지 옵션은 기본값으로 둡니다. "마침"을 클릭 합니다.

이제 페이지에 배치한 ListView 컨트롤 인스턴스의 ID 속성을 ListView\_ProductsMenu로 설정 하 고 해당 도우미를 활성화 해 보겠습니다.

![](tailspin-spyworks-part-3/_static/image5.jpg)

컨트롤 옵션을 사용 하 여 데이터 항목 표시 및 서식 지정의 서식을 지정할 수 있지만 메뉴 생성에는 간단한 태그만 필요 하므로 소스 뷰에 코드를 입력 합니다.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

"Eval" 문: &lt;% # Eval ("범주")%&gt;

ASP.NET 구문 &lt;% #%&gt;은 런타임에 포함 된 모든 항목을 실행 하 고 결과를 "줄 내"로 출력 하는 간단한 규칙입니다.

문 Eval ("범주")은 바인딩된 데이터 항목 컬렉션의 현재 항목에 대해 엔터티 모델 항목 이름 "범주"의 값을 인출 하도록 지시 합니다. 매우 강력한 기능을 위한 간결한 구문입니다.

이제 응용 프로그램을 실행할 수 있습니다.

![](tailspin-spyworks-part-3/_static/image6.jpg)

이제 제품 범주 메뉴가 표시 되 고 범주 메뉴 항목 중 하나를 마우스로 가리키면 메뉴 항목 링크가 ProductsList 이라는 이름으로 구현 해야 하는 페이지를 가리키는 것을 볼 수 있으며,이를 포함 하는 동적 쿼리 문자열 인수를 작성 했습니다.  범주 id입니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-2.md)
> [다음](tailspin-spyworks-part-4.md)
