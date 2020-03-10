---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: '4 부: 제품 나열 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 4 부에서는 GridView를 사용 하 여 제품을 나열 하는 방법을 설명 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78457283"
---
# <a name="part-4-listing-products"></a>4 부: 제품 나열

만든 사람 [Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다. ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 4 부에서는 GridView 컨트롤을 사용 하 여 제품을 나열 하는 방법을 설명 합니다.

## <a id="_Toc260221670"></a>GridView 컨트롤을 사용 하 여 제품 나열

솔루션에서 "마우스 오른쪽 단추를 클릭" 하 고 "추가" 및 "새 항목"을 선택 하 여 ProductsList 페이지를 구현 해 보겠습니다.

![](tailspin-spyworks-part-4/_static/image1.jpg)

"마스터 페이지를 사용 하 여 웹 양식"을 선택 하 고 페이지 이름을 ProductsList로 입력 합니다.

"추가"를 클릭 합니다.

![](tailspin-spyworks-part-4/_static/image2.jpg)

그런 다음, Site.master 페이지를 배치할 "스타일" 폴더를 선택 하 고 "폴더 내용" 창에서 선택 합니다.

![](tailspin-spyworks-part-4/_static/image3.jpg)

"확인"을 클릭 하 여 페이지를 만듭니다.

데이터베이스는 아래와 같이 제품 데이터로 채워집니다.

![](tailspin-spyworks-part-4/_static/image4.jpg)

페이지를 만든 후에는 다시 엔터티 데이터 원본을 사용 하 여 해당 제품 데이터에 액세스할 수 있지만이 인스턴스에서는 제품 엔터티를 선택 해야 하며, 선택한 범주에 대 한 항목 으로만 반환 되는 항목을 제한 해야 합니다.

이를 위해 WHERE 절을 자동으로 생성 하도록 EntityDataSource에 지시 하 고 WhereParameter를 지정 합니다.

"제품 범주 메뉴"에서 메뉴 항목을 만들었을 때 각 링크에 대 한 QueryString에 CategoryID를 추가 하 여 링크를 동적으로 작성 했습니다. 해당 QueryString 매개 변수에서 WHERE 매개 변수를 파생 하도록 엔터티 데이터 소스에 지시 합니다.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

다음으로 제품 목록을 표시 하도록 ListView 컨트롤을 구성 합니다. 최적의 쇼핑 환경을 만들려면 ListVew에 표시 되는 각 개별 제품에 몇 가지 간결한 기능을 압축 합니다.

- 제품 이름은 제품의 세부 정보 보기에 대 한 링크입니다.
- 제품의 가격이 표시 됩니다.
- 제품 이미지가 표시 되 고 응용 프로그램의 카탈로그 이미지 디렉터리에서 이미지를 동적으로 선택 합니다.
- 특정 제품을 쇼핑 카트에 즉시 추가 하는 링크가 포함 됩니다.

ListView 컨트롤 인스턴스의 태그는 다음과 같습니다.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

표시 된 각 제품에 대 한 여러 링크를 동적으로 작성 합니다.

또한 새 페이지를 테스트 하기 전에 다음과 같이 제품 카탈로그 이미지에 대 한 디렉터리 구조를 만들어야 합니다.

![](tailspin-spyworks-part-4/_static/image1.png)

제품 이미지에 액세스할 수 있게 되 면 제품 목록 페이지를 테스트할 수 있습니다.

![](tailspin-spyworks-part-4/_static/image5.jpg)

사이트의 홈 페이지에서 범주 목록 링크 중 하나를 클릭 합니다.

![](tailspin-spyworks-part-4/_static/image6.jpg)

이제는 제품 세부 정보 .aspx 페이지 및 기능 카트 기능을 구현 해야 합니다.

파일-&gt;새로 만들기를 사용 하 여 이전에 했던 것 처럼 사이트 마스터 페이지를 사용 하 여 페이지 이름 제품 정보 .aspx를 만듭니다.

EntityDataSource 컨트롤을 다시 사용 하 여 데이터베이스의 특정 제품 레코드에 액세스 하 고, 다음과 같이 ASP.NET FormView 컨트롤을 사용 하 여 제품 데이터를 표시 합니다.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

서식 지정이 약간 재미를 보이는 경우 걱정 하지 마세요. 위의 태그는 나중에 구현할 몇 가지 기능에 대해 표시 레이아웃의 공간을 남겨 둡니다.

쇼핑 카트는 응용 프로그램의 더 복잡 한 논리를 나타냅니다. 시작 하려면 파일-&gt;New를 사용 하 여 MyShoppingCart 라는 페이지를 만듭니다.

ShoppingCart 이름은 선택 하지 않습니다.

데이터베이스는 "ShoppingCart" 라는 테이블을 포함 합니다. 엔터티 데이터 모델 생성 된 경우 데이터베이스의 각 테이블에 대해 클래스가 생성 됩니다. 따라서 엔터티 데이터 모델는 "ShoppingCart" 라는 엔터티 클래스를 생성 했습니다. 쇼핑 카트 구현에 해당 이름을 사용 하거나 필요에 맞게 확장할 수 있도록 모델을 편집할 수 있지만, 충돌을 방지 하는 이름을 대신 선택 하는 것이 좋습니다.

또한 간단한 쇼핑 카트를 만들고 쇼핑 카트 표시를 사용 하 여 쇼핑 카트 논리를 포함 하는 것이 좋습니다. 또한 완전히 별도의 비즈니스 계층에서 쇼핑 카트를 구현 하도록 선택할 수 있습니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-3.md)
> [다음](tailspin-spyworks-part-5.md)
