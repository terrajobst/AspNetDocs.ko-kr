---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: '2 부: 데이터 액세스 계층 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 2 부에서는 데이터 액세스 계층 추가에 대해 설명 합니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78462653"
---
# <a name="part-2-data-access-layer"></a>2 부: 데이터 액세스 계층

만든 사람 [Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다. ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 2 부에서는 데이터 액세스 계층 추가에 대해 설명 합니다.

## <a id="_Toc260221668"></a>데이터 액세스 계층 추가

전자 상거래 응용 프로그램은 두 개의 데이터베이스에 따라 달라 집니다.

고객 정보는 표준 ASP.NET 멤버 자격 데이터베이스를 사용 합니다. 쇼핑 카트 및 제품 카탈로그의 경우 다음과 같이 SQL Express 데이터베이스를 구현 합니다.

![](tailspin-spyworks-part-2/_static/image1.jpg)

응용 프로그램의 앱\_데이터 폴더에 데이터베이스 (상거래)를 만들었으면 .NET Entity Framework를 사용 하 여 데이터 액세스 계층을 만들 수 있습니다.

"데이터\_액세스" 라는 폴더를 만들고 해당 폴더를 마우스 오른쪽 단추로 클릭 한 다음 "새 항목 추가"를 선택 합니다.

"설치 된 템플릿" 항목에서 "ADO.NET 엔터티 데이터 모델"를 선택 하 고 이름으로 EDM\_를 입력 한 다음 "추가" 단추를 클릭 합니다.

![](tailspin-spyworks-part-2/_static/image2.jpg)

"데이터베이스에서 생성"을 선택 합니다.

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

저장 하 고 빌드합니다.

이제 제품 범주 메뉴의 첫 번째 기능을 추가할 준비가 되었습니다.

> [!div class="step-by-step"]
> [이전](tailspin-spyworks-part-1.md)
> [다음](tailspin-spyworks-part-3.md)
