---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터 유효성 검사 강화'
description: 이 자습서에서는 데이터 모델에 데이터 주석을 추가 하 여 유효성 검사 요구 사항을 지정 하 고 서식을 표시 하는 방법을 집중적으로 설명 합니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499535"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 데이터 유효성 검사 강화

MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 사용자가 데이터베이스 테이블에 있는 데이터를 표시, 편집, 만들기 및 삭제할 수 있도록 하는 코드를 자동으로 생성 하는 방법을 보여 줍니다. 생성 된 코드는 데이터베이스 테이블의 열에 해당 합니다.

이 자습서에서는 데이터 모델에 데이터 주석을 추가 하 여 유효성 검사 요구 사항을 지정 하 고 서식을 표시 하는 방법을 집중적으로 설명 합니다. 의견 섹션에서 사용자의 의견에 따라 개선 되었습니다.

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 데이터 주석 추가
> * 메타 데이터 클래스 추가

## <a name="prerequisites"></a>사전 요구 사항

* [보기 사용자 지정](customizing-a-view.md)

## <a name="add-data-annotations"></a>데이터 주석 추가

이전 항목에서 살펴본 것 처럼 일부 데이터 유효성 검사 규칙은 사용자 입력에 자동으로 적용 됩니다. 예를 들어 Grade 속성에는 숫자만 제공할 수 있습니다. 더 많은 데이터 유효성 검사 규칙을 지정 하기 위해 모델 클래스에 데이터 주석을 추가할 수 있습니다. 이러한 주석은 지정 된 속성에 대 한 웹 응용 프로그램 전체에 적용 됩니다. 속성이 표시 되는 방식을 변경 하는 서식 특성을 적용할 수도 있습니다. 와 같이 텍스트 레이블에 사용 되는 값을 변경 합니다.

이 자습서에서는 FirstName, LastName 및 MiddleName 속성에 대해 제공 되는 값의 길이를 제한 하는 데이터 주석을 추가 합니다. 데이터베이스에서 이러한 값은 50 자로 제한 됩니다. 그러나 웹 응용 프로그램에서는 현재 문자 제한이 적용 되지 않습니다. 사용자가 이러한 값 중 하나에 대해 50 자를 초과 하 여 제공 하는 경우에는 해당 값을 데이터베이스에 저장 하려고 할 때 페이지의 작동이 중단 됩니다. 또한 점수는 0과 4 사이의 값으로 제한 됩니다.

**모델** > **ContosoModel** > **ContosoModel.tt** 를 선택 하 고 *Student.cs* 파일을 엽니다. 클래스에 다음 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

*Enrollment.cs* 를 열고 다음 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

솔루션을 빌드합니다.

**학생 목록** 을 클릭 하 고 **편집**을 선택 합니다. 50 자를 초과 하는 문자를 입력 하려고 하면 오류 메시지가 표시 됩니다.

![오류 메시지 표시](enhancing-data-validation/_static/image1.png)

홈 페이지로 돌아갑니다. **등록 목록** 을 클릭 하 고 **편집**을 선택 합니다. 4 보다 높은 등급을 제공 하려고 합니다. 이 오류가 표시 됩니다. *필드 등급은 0에서 4 사이* 여야 합니다.

## <a name="add-metadata-classes"></a>메타 데이터 클래스 추가

모델 클래스에 직접 유효성 검사 특성을 추가 하는 것은 데이터베이스를 변경 하지 않을 때 작동 합니다. 그러나 데이터베이스를 변경 하 고 모델 클래스를 다시 생성 해야 하는 경우에는 모델 클래스에 적용 한 모든 특성을 잃게 됩니다. 이 접근 방식은 매우 비효율적 이며 중요 한 유효성 검사 규칙을 손실 하는 경향이 있습니다.

이 문제를 방지 하기 위해 특성을 포함 하는 메타 데이터 클래스를 추가할 수 있습니다. 모델 클래스를 메타 데이터 클래스에 연결 하면 해당 특성이 모델에 적용 됩니다. 이 방법에서는 메타 데이터 클래스에 적용 된 모든 특성을 잃지 않고 모델 클래스를 다시 생성할 수 있습니다.

**모델** 폴더에서 이름이 *Metadata.cs*인 클래스를 추가 합니다.

*Metadata.cs* 의 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

이러한 메타 데이터 클래스는 이전에 모델 클래스에 적용 한 모든 유효성 검사 특성을 포함 합니다. **표시** 특성은 텍스트 레이블에 사용 되는 값을 변경 하는 데 사용 됩니다.

이제 모델 클래스를 메타 데이터 클래스와 연결 해야 합니다.

**모델** 폴더에서 이름이 *PartialClasses.cs*인 클래스를 추가 합니다.

파일 내용을 다음 코드로 바꿉니다.

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

각 클래스는 `partial` 클래스로 표시 되 고 각각은 이름과 네임 스페이스를 자동으로 생성 되는 클래스로 일치 시킵니다. 메타 데이터 특성을 partial 클래스에 적용 하 여 데이터 유효성 검사 특성이 자동으로 생성 된 클래스에 적용 되도록 합니다. 메타 데이터 특성은 다시 생성 되지 않는 부분 클래스에서 적용 되므로 모델 클래스를 다시 생성할 때 이러한 특성은 손실 되지 않습니다.

자동으로 생성 된 클래스를 다시 생성 하려면 *ContosoModel* 파일을 엽니다. 다시 한 번 디자인 화면을 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스에서 모델 업데이트**를 선택 합니다. 데이터베이스를 변경 하지 않은 경우에도이 프로세스는 클래스를 다시 생성 합니다. **새로 고침** 탭에서 **테이블** 을 선택 하 고 **마침**을 선택 합니다.

*ContosoModel* 파일을 저장 하 여 변경 내용을 적용 합니다.

*Student.cs* 파일 또는 *Enrollment.cs* 파일을 열고 이전에 적용 한 데이터 유효성 검사 특성이 파일에 더 이상 표시 되지 않는지 확인 합니다. 그러나 응용 프로그램을 실행 하 고 데이터를 입력할 때 유효성 검사 규칙이 계속 적용 되는지 확인 합니다.

## <a name="conclusion"></a>결론

이 시리즈에서는 사용자가 데이터를 편집, 업데이트, 만들기 및 삭제할 수 있도록 하는 기존 데이터베이스에서 코드를 생성 하는 방법에 대 한 간단한 예를 제공 했습니다. ASP.NET MVC 5, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 프로젝트를 만듭니다. 

Code First 개발의 소개 예제는 [ASP.NET MVC 5 시작](../introduction/getting-started.md)을 참조 하세요. 

고급 예제를 보려면 [ASP.NET MVC 4 앱에 대 한 Entity Framework 데이터 모델 만들기](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요. Database First의 데이터로 작업 하는 데 사용 하는 DbContext API는 Code First의 데이터로 작업 하는 데 사용 하는 API와 동일 합니다. Database First를 사용 하려는 경우에도 Code First 자습서에서 관련 데이터 읽기 및 업데이트, 동시성 충돌 처리 등과 같은 보다 복잡 한 시나리오를 처리 하는 방법을 배울 수 있습니다. 유일한 차이점은 데이터베이스, 컨텍스트 클래스 및 엔터티 클래스를 만드는 방법입니다.

## <a name="additional-resources"></a>추가 리소스

속성 및 클래스에 적용할 수 있는 데이터 유효성 검사 주석의 전체 목록은 [System.componentmodel 주석을](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx)참조 하세요.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 추가 된 데이터 주석
> * 메타 데이터 클래스 추가

Azure App Service에 웹 앱과 SQL 데이터베이스를 배포 하는 방법을 알아보려면 다음 자습서를 참조 하세요.
> [!div class="nextstepaction"]
> [Azure App Service에 .NET 앱 배포](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)
