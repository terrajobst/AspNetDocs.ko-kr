---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: 모델 바인딩 및 web forms를 사용 하 여 데이터 업데이트, 삭제 및 만들기 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78474137"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a>모델 바인딩 및 web forms를 사용 하 여 데이터 업데이트, 삭제 및 만들기

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다. 이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.
> 
> 이 자습서에서는 모델 바인딩을 사용 하 여 데이터를 만들고, 업데이트 하 고, 삭제 하는 방법을 보여 줍니다. 다음 속성을 설정 합니다.
> 
> - DeleteMethod
> - InsertMethod
> - UpdateMethod
> 
> 이러한 속성은 해당 작업을 처리 하는 메서드의 이름을 받습니다. 이 메서드 내에서 데이터와 상호 작용 하는 논리를 제공 합니다.
> 
> 이 자습서는 계열의 첫 번째 [부분](retrieving-data.md) 에서 만든 프로젝트를 기반으로 합니다.
> 
> 또는 VB [download](https://go.microsoft.com/fwlink/?LinkId=286116) 에서 C# 전체 프로젝트를 다운로드할 수 있습니다. 다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013와 함께 작동 합니다. 이 자습서에서는이 자습서에 표시 된 Visual Studio 2013 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.

## <a name="what-youll-build"></a>빌드할 내용

이 자습서에서는 다음을 수행합니다.

1. 동적 데이터 템플릿 추가
2. 모델 바인딩 메서드를 통해 데이터 업데이트 및 삭제 사용
3. 데이터 유효성 검사 규칙 적용-데이터베이스에 새 레코드를 만들 수 있습니다.

## <a name="add-dynamic-data-templates"></a>동적 데이터 템플릿 추가

최상의 사용자 환경을 제공 하 고 코드 반복을 최소화 하려면 동적 데이터 템플릿을 사용 합니다. NuGet 패키지를 설치 하 여 미리 작성 된 동적 데이터 템플릿을 기존 사이트에 쉽게 통합할 수 있습니다.

**NuGet 패키지 관리**에서 **DynamicDataTemplatesCS**를 설치 합니다.

![동적 데이터 템플릿](updating-deleting-and-creating-data/_static/image1.png)

이제 프로젝트에 이름이 **DynamicData**인 폴더가 포함 됩니다. 해당 폴더에서 web forms의 동적 컨트롤에 자동으로 적용 되는 템플릿을 찾을 수 있습니다.

![동적 데이터 폴더](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a>업데이트 및 삭제 사용

사용자가 데이터베이스의 레코드를 업데이트 하 고 삭제할 수 있도록 설정 하는 것은 데이터를 검색 하는 프로세스와 매우 비슷합니다. **UpdateMethod** 및 **DeleteMethod** 속성에서 이러한 작업을 수행 하는 메서드의 이름을 지정 합니다. GridView 컨트롤을 사용 하 여 편집 및 삭제 단추의 자동 생성을 지정할 수도 있습니다. 다음 강조 표시 된 코드는 GridView 코드에 추가 된 내용을 보여 줍니다.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

코드를 사용 하는 파일에서 **system.object**에 대 한 using 문을 추가 합니다.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

그런 다음, 다음 update 및 delete 메서드를 추가 합니다.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

**TryUpdateModel** 메서드는 일치 하는 데이터 바인딩된 값을 웹 폼에서 데이터 항목에 적용 합니다. 데이터 항목은 id 매개 변수의 값에 따라 검색 됩니다.

## <a name="enforce-validation-requirements"></a>유효성 검사 요구 사항 적용

Student 클래스의 FirstName, LastName 및 Year 속성에 적용 한 유효성 검사 특성은 데이터를 업데이트할 때 자동으로 적용 됩니다. DynamicField 컨트롤은 유효성 검사 특성에 따라 클라이언트 및 서버 유효성 검사기를 추가 합니다. FirstName 및 LastName 속성이 모두 필요 합니다. FirstName의 길이는 20 자를 초과할 수 없으며 LastName은 40 자를 초과할 수 없습니다. 연도는 AcademicYear 열거형에 유효한 값 이어야 합니다.

사용자가 유효성 검사 요구 사항 중 하나를 위반 하는 경우 업데이트가 진행 되지 않습니다. 오류 메시지를 보려면 GridView 위에 ValidationSummary 컨트롤을 추가 합니다. 모델 바인딩에서 유효성 검사 오류를 표시 하려면 **Showmodelstateerrors** 속성을 **true**로 설정 합니다. 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

웹 응용 프로그램을 실행 하 고 레코드를 업데이트 하 고 삭제 합니다.

![데이터 업데이트](updating-deleting-and-creating-data/_static/image3.png)

편집 모드에서 Year 속성의 값이 자동으로 드롭다운 목록으로 렌더링 됩니다. Year 속성은 열거형 값이 고, 열거형 값에 대 한 동적 데이터 템플릿은 편집할 드롭다운 목록을 지정 합니다. **DynamicData**/**fieldtemplates** 폴더에서 **\_편집** 을 열어이 템플릿을 찾을 수 있습니다.

유효한 값을 제공 하는 경우 업데이트가 성공적으로 완료 됩니다. 유효성 검사 요구 사항 중 하나를 위반 하는 경우 업데이트는 진행 되지 않으며 그리드 위에 오류 메시지가 표시 됩니다.

![오류 메시지](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a>새 레코드 추가

GridView 컨트롤에는 **InsertMethod** 속성이 포함 되어 있지 않으므로 모델 바인딩을 사용 하 여 새 레코드를 추가 하는 데 사용할 수 없습니다. **FormView**, **DetailsView**또는 **ListView** 컨트롤에서 InsertMethod 속성을 찾을 수 있습니다. 이 자습서에서는 FormView 컨트롤을 사용 하 여 새 레코드를 추가 합니다.

먼저 새 레코드를 추가 하기 위해 만들 새 페이지에 대 한 링크를 추가 합니다. ValidationSummary 위에 다음을 추가 합니다.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

새 링크가 학생 페이지의 콘텐츠 맨 위에 표시 됩니다.

![새 링크](updating-deleting-and-creating-data/_static/image5.png)

그런 다음 마스터 페이지를 사용 하 여 새 web form을 추가 하 고 이름을 **Addstudent**로 지정한 다음 마스터 페이지로 site.master를 선택 합니다.

**Dynamicentity** 컨트롤을 사용 하 여 새 학생을 추가 하기 위한 필드를 렌더링 합니다. DynamicEntity 컨트롤은 ItemType 속성에 지정 된 클래스에서 편집 가능한 속성을 렌더링 합니다. StudentID 속성이 **[ScaffoldColumn (false)]** 특성으로 표시 되어 렌더링 되지 않습니다. AddStudent 페이지의 MainContent 자리 표시자 페이지에서 다음 코드를 추가 합니다.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

코드 숨김이 파일 (AddStudent.aspx.cs)에서 네임 스페이스에 대 한 **using** 문을 추가 **합니다.**

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

그런 다음, 다음 메서드를 추가 하 여 새 레코드를 삽입 하는 방법과 취소 단추에 대 한 이벤트 처리기를 지정 합니다.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

모든 변경 내용을 저장 합니다.

웹 응용 프로그램을 실행 하 고 새 학생을 만듭니다.

![새 학생 추가](updating-deleting-and-creating-data/_static/image6.png)

**삽입** 을 클릭 하 고 새 학생을 만들었는지 확인 합니다.

![새 학생 표시](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a>결론

이 자습서에서는 데이터 업데이트, 삭제 및 만들기를 사용 하도록 설정 했습니다. 데이터와 상호 작용 하는 경우 유효성 검사 규칙이 적용 되었는지 확인 했습니다.

이 시리즈의 다음 [자습서](sorting-paging-and-filtering-data.md) 에서는 데이터 정렬, 페이징 및 필터링을 사용 하도록 설정 합니다.

> [!div class="step-by-step"]
> [이전](retrieving-data.md)
> [다음](sorting-paging-and-filtering-data.md)
