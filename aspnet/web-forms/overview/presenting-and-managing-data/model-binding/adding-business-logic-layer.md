---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: 모델 바인딩 및 web forms를 사용 하는 프로젝트에 비즈니스 논리 계층 추가 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78515429"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a>모델 바인딩 및 web forms를 사용 하는 프로젝트에 비즈니스 논리 계층 추가

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다. 이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.
> 
> 이 자습서에서는 비즈니스 논리 계층에서 모델 바인딩을 사용 하는 방법을 보여 줍니다. OnCallingDataMethods 멤버를 설정 하 여 현재 페이지 이외의 개체를 사용 하 여 데이터 메서드를 호출 하도록 지정 합니다.
> 
> 이 자습서는 시리즈의 [이전](retrieving-data.md) 부분에서 만든 프로젝트를 기반으로 합니다.
> 
> 또는 VB [download](https://go.microsoft.com/fwlink/?LinkId=286116) 에서 C# 전체 프로젝트를 다운로드할 수 있습니다. 다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013와 함께 작동 합니다. 이 자습서에서는이 자습서에 표시 된 Visual Studio 2013 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.

## <a name="what-youll-build"></a>빌드할 내용

모델 바인딩을 사용 하면 웹 페이지 또는 별도의 비즈니스 논리 클래스에 대 한 코드 파일에 데이터 상호 작용 코드를 배치할 수 있습니다. 이전 자습서에서는 데이터 상호 작용 코드에 코드 숨김이 포함 된 파일을 사용 하는 방법을 보여 줍니다. 이 접근 방식은 작은 사이트에는 적용 되지만 큰 사이트를 유지 관리 하는 경우 코드를 반복 하 고 더 어려움을 일으킬 수 있습니다. 또한 추상 계층이 없기 때문에 코드 뒤에 있는 코드를 프로그래밍 방식으로 테스트 하는 것이 매우 어려울 수 있습니다.

데이터 상호 작용 코드를 중앙 집중화 하기 위해 데이터와 상호 작용 하는 모든 논리를 포함 하는 비즈니스 논리 계층을 만들 수 있습니다. 그런 다음 웹 페이지에서 비즈니스 논리 계층을 호출 합니다. 이 자습서에서는 이전 자습서에서 작성 한 모든 코드를 비즈니스 논리 계층으로 이동한 다음 페이지에서 해당 코드를 사용 하는 방법을 보여 줍니다.

이 자습서에서는 다음을 수행합니다.

1. 코드를 코드 숨김이 아닌 파일에서 비즈니스 논리 계층으로 이동
2. 비즈니스 논리 계층에서 메서드를 호출 하도록 데이터 바인딩된 컨트롤 변경

## <a name="create-business-logic-layer"></a>비즈니스 논리 계층 만들기

이제 웹 페이지에서 호출 되는 클래스를 만듭니다. 이 클래스의 메서드는 이전 자습서에서 사용한 메서드와 비슷하며 값 공급자 특성을 포함 합니다.

먼저 **BLL**이라는 새 폴더를 추가 합니다.

![폴더 추가](adding-business-logic-layer/_static/image1.png)

BLL 폴더에서 **SchoolBL.cs**이라는 새 클래스를 만듭니다. 여기에는 원래 코드 파일에 있는 모든 데이터 작업이 포함 됩니다. 메서드는 코드 숨김이 파일의 메서드와 거의 동일 하지만 몇 가지 변경 내용이 포함 됩니다.

가장 중요 한 변경 사항은 **Page** 클래스의 인스턴스 내에서 코드를 더 이상 실행 하지 않는다는 것입니다. Page 클래스에는 **TryUpdateModel** 메서드와 **modelstate** 속성이 포함 되어 있습니다. 이 코드를 비즈니스 논리 계층으로 이동 하면 더 이상 이러한 멤버를 호출할 수 있는 페이지 클래스 인스턴스가 없습니다. 이 문제를 해결 하려면 TryUpdateModel 또는 ModelState에 액세스 하는 메서드에 **Modelmethodcontext** 매개 변수를 추가 해야 합니다. 이 ModelMethodContext 매개 변수를 사용 하 여 TryUpdateModel를 호출 하거나 ModelState를 검색 합니다. 이 새 매개 변수를 고려 하 여 웹 페이지의 모든 항목을 변경할 필요는 없습니다.

SchoolBL.cs의 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a>기존 페이지를 수정 하 여 비즈니스 논리 계층에서 데이터 검색

마지막으로, 비즈니스 논리 계층을 사용 하 여 코드 숨김이 파일의 쿼리를 사용 하지 못하도록 학생 .aspx, AddStudent .aspx 및 강의 페이지를 변환 합니다.

학생, AddStudent 및 과정에 대 한 코드 숨겨진 파일에서 다음 쿼리 메서드를 삭제 하거나 주석 처리 합니다.

- studentsGrid\_GetData
- studentsGrid\_UpdateItem
- studentsGrid\_DeleteItem
- addStudentForm\_InsertItem
- coursesGrid\_GetData

이제 데이터 작업과 관련 된 코드 파일에 코드가 없어야 합니다.

**OnCallingDataMethods** 이벤트 처리기를 사용 하 여 데이터 메서드에 사용할 개체를 지정할 수 있습니다. 학생과 .aspx에서 해당 이벤트 처리기에 대 한 값을 추가 하 고 비즈니스 논리 클래스의 메서드 이름으로 데이터 메서드의 이름을 변경 합니다.

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

CallingDataMethods에 대 한 코드 숨김이 파일에서 이벤트 처리기를 정의 합니다. 이 이벤트 처리기에서 데이터 작업에 대 한 비즈니스 논리 클래스를 지정 합니다.

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

AddStudent .aspx에서 비슷한 변경을 수행 합니다.

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

Default.aspx에서 비슷한 변경을 수행 합니다.

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

응용 프로그램을 실행 하 고 모든 페이지가 이전 처럼 작동 하는지 확인 합니다. 유효성 검사 논리도 제대로 작동 합니다.

## <a name="conclusion"></a>결론

이 자습서에서는 데이터 액세스 계층 및 비즈니스 논리 계층을 사용 하도록 응용 프로그램을 다시 구성 합니다. 데이터 컨트롤에서 데이터 작업을 위해 현재 페이지가 아닌 개체를 사용 하도록 지정 했습니다.

> [!div class="step-by-step"]
> [이전](using-query-string-values-to-retrieve-data.md)
