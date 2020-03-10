---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기 사용자 지정'
description: 이 자습서에서는 자동으로 생성 된 보기를 변경 하 여 프레젠테이션을 개선 하는 방법을 집중적으로 설명 합니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471521"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기 사용자 지정

MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 사용자가 데이터베이스 테이블에 있는 데이터를 표시, 편집, 만들기 및 삭제할 수 있도록 하는 코드를 자동으로 생성 하는 방법을 보여 줍니다. 생성 된 코드는 데이터베이스 테이블의 열에 해당 합니다.

이 자습서에서는 자동으로 생성 된 보기를 변경 하 여 프레젠테이션을 개선 하는 방법을 집중적으로 설명 합니다.

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 학생 세부 정보 페이지에 과정 추가
> * 코스가 페이지에 추가 되었는지 확인

## <a name="prerequisites"></a>사전 요구 사항

* [데이터베이스 변경](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a>학생 세부 정보에 강좌 추가

생성 된 코드는 응용 프로그램에 적합 한 시작 지점을 제공 하지만 응용 프로그램에서 필요한 모든 기능을 제공 하는 것은 아닙니다. 응용 프로그램의 특정 요구 사항에 맞게 코드를 사용자 지정할 수 있습니다. 현재 응용 프로그램에는 선택한 학생에 대해 등록 된 강좌가 표시 되지 않습니다. 이 섹션에서는 각 학생에 대해 등록 된 과정을 학생에 대 한 **세부 정보** 보기에 추가 합니다.

**학습자** >  > **보기** 를 엽니다. *cshtml*. 마지막 &lt;/dl&gt; 태그 아래에 있지만 closing &lt;/div&gt; 태그 앞에 다음 코드를 추가 합니다.

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

이 코드는 선택한 학생에 대해 등록 테이블의 각 레코드에 대 한 행을 표시 하는 테이블을 만듭니다. **표시** 메서드는 식을 나타내는 개체 (modelitem)의 HTML을 렌더링 합니다. 표시 메서드 (코드에 속성 값을 포함 하는 것이 아님)를 사용 하 여 해당 형식 및 해당 형식의 템플릿에 따라 값의 형식이 올바르게 지정 되었는지 확인 합니다. 이 예에서는 각 식이 루프의 현재 레코드에서 단일 속성을 반환 하 고, 값은 텍스트로 렌더링 되는 기본 형식입니다.

## <a name="confirm-courses-are-added"></a>강좌 추가 확인

솔루션을 실행합니다. **학생 목록** 을 클릭 하 고 학생 중 한 명에 대 한 **세부 정보** 를 선택 합니다. 등록 된 강좌가 보기에 포함 되어 있는 것을 볼 수 있습니다.

![등록 된 학생](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a>다음 단계
이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 학생 세부 정보 페이지에 강좌를 추가 했습니다.
> * 코스가 페이지에 추가 되었는지 확인

다음 자습서로 이동 하 여 유효성 검사 요구 사항을 지정 하 고 서식을 표시 하는 데이터 주석을 추가 하는 방법을 알아봅니다.
> [!div class="nextstepaction"]
> [데이터 유효성 검사 향상](enhancing-data-validation.md)
