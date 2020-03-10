---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: 사용자 지정 경로 만들기C#() | Microsoft Docs
author: microsoft
description: ASP.NET MVC 응용 프로그램에 사용자 지정 경로를 추가 하는 방법에 대해 알아봅니다. 이 자습서에서는 global.asax 파일에서 기본 경로 테이블을 수정 하는 방법에 대해 알아봅니다.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 58f72e390f0053d136ef00ddbda0b071ba225d98
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486725"
---
# <a name="creating-custom-routes-c"></a>사용자 지정 경로 만들기(C#)

[Microsoft](https://github.com/microsoft) 에서

> ASP.NET MVC 응용 프로그램에 사용자 지정 경로를 추가 하는 방법에 대해 알아봅니다. 이 자습서에서는 global.asax 파일에서 기본 경로 테이블을 수정 하는 방법에 대해 알아봅니다.

이 자습서에서는 ASP.NET MVC 응용 프로그램에 사용자 지정 경로를 추가 하는 방법에 대해 알아봅니다. 사용자 지정 경로를 사용 하 여 Global.asax 파일에서 기본 경로 테이블을 수정 하는 방법에 대해 알아봅니다.

여러 간단한 ASP.NET MVC 응용 프로그램의 경우 기본 경로 테이블은 정상적으로 작동 합니다. 그러나 특별 한 라우팅 요구 사항이 있다는 것을 알 수 있습니다. 이 경우 사용자 지정 경로를 만들 수 있습니다.

예를 들어, 블로그 응용 프로그램을 빌드하는 경우를 가정해 보겠습니다. 다음과 같은 들어오는 요청을 처리 하는 것이 좋습니다.

/Archive/12-25-2009

사용자가이 요청을 입력 하면 날짜 12/25/2009에 해당 하는 블로그 항목을 반환 하려고 합니다. 이러한 유형의 요청을 처리 하려면 사용자 지정 경로를 만들어야 합니다.

1을 나열 하는 Global.asax 파일에는/Archive/*entry date*와 같은 요청을 처리 하는 새 사용자 지정 경로 라는 이름이 있습니다.

**목록 1-global.asax (사용자 지정 경로 사용)**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

경로 테이블에 추가 하는 경로의 순서는 중요 합니다. 새 사용자 지정 블로그 경로가 기존 기본 경로 앞에 추가 됩니다. 순서를 반대로 하면 기본 경로가 항상 사용자 지정 경로 대신 호출 됩니다.

사용자 지정 블로그 경로는/Archive/.로 시작 하는 모든 요청과 일치 합니다. 따라서 다음 Url이 모두 일치 합니다.

- /Archive/12-25-2009

- /Archive/10-6-2004

- /Archive/apple

사용자 지정 경로는 수신 된 요청을 Archive 컨트롤러에 매핑하고 Entry () 작업을 호출 합니다. Entry () 메서드를 호출 하면 항목 날짜가 entryDate 라는 매개 변수로 전달 됩니다.

목록 2의 컨트롤러와 함께 블로그 사용자 지정 경로를 사용할 수 있습니다.

**목록 2-ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

목록 2의 Entry () 메서드는 DateTime 형식의 매개 변수를 허용 합니다. MVC 프레임 워크는 URL의 항목 날짜를 자동으로 DateTime 값으로 변환할 수 있을 정도로 지능적입니다. URL의 entry date 매개 변수를 DateTime으로 변환할 수 없는 경우 오류가 발생 합니다 (그림 1 참조).

**그림 1-변환 매개 변수 오류**

[새 프로젝트 대화 상자 ![](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**그림 01**: 매개 변수 변환 오류 ([전체 크기 이미지를 보려면 클릭](creating-custom-routes-cs/_static/image2.png))

## <a name="summary"></a>요약

이 자습서의 목표는 사용자 지정 경로를 만드는 방법을 설명 하는 것입니다. 블로그 항목을 나타내는 global.asax 파일의 경로 테이블에 사용자 지정 경로를 추가 하는 방법을 배웠습니다. 블로그 항목에 대 한 요청을 ArchiveController 이라는 컨트롤러에 매핑하는 방법과 Entry () 라는 컨트롤러 작업을 매핑하는 방법에 대해 설명 했습니다.

> [!div class="step-by-step"]
> [이전](aspnet-mvc-controllers-overview-cs.md)
> [다음](creating-a-route-constraint-cs.md)
