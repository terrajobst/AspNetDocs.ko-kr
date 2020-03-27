---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: 모델 바인딩 및 web forms를 사용 하 여 데이터 정렬, 페이징 및 필터링 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78441065"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a>모델 바인딩 및 web forms를 사용 하 여 데이터 정렬, 페이징 및 필터링

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다. 이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.
> 
> 이 자습서에서는 모델 바인딩을 통해 데이터의 정렬, 페이징 및 필터링을 추가 하는 방법을 보여 줍니다.
> 
> 이 자습서는 계열의 첫 번째 [부분](retrieving-data.md) 에서 만든 프로젝트를 기반으로 합니다.
> 
> 또는 VB 에서 C# 전체 프로젝트를 [다운로드](https://go.microsoft.com/fwlink/?LinkId=286116)할 수 있습니다. 다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013와 함께 작동 합니다. 이 자습서에서는이 자습서에 표시 된 Visual Studio 2013 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.

## <a name="what-youll-build"></a>빌드할 내용

이 자습서에서는 다음을 수행합니다.

1. 데이터 정렬 및 페이징 사용
2. 사용자가 선택한 항목을 기준으로 데이터 필터링 사용

## <a name="add-sorting"></a>정렬 추가

GridView에서 정렬을 사용 하는 것은 매우 쉽습니다. 학생용 .aspx 파일에서 GridView의 **Allowsorting** **true** 로 설정 하기만 하면 됩니다. DataField가 자동으로 사용 되기 때문에 각 열에 대해 **SortExpression** 값을 설정할 필요가 없습니다. GridView는 선택한 값을 기준으로 데이터 순서 지정을 포함 하도록 쿼리를 수정 합니다. 아래 강조 표시 된 코드는 정렬을 사용 하도록 설정 하는 데 필요한 추가 작업을 보여 줍니다.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

웹 응용 프로그램을 실행 하 고 여러 열의 값을 기준으로 학생 레코드 정렬을 테스트 합니다.

![학생 정렬](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a>페이징 추가

페이징을 사용 하는 것도 매우 쉽습니다. GridView에서 **AllowPaging** 속성을 **true** 로 설정 하 고 **PageSize** 속성을 각 페이지에 표시할 레코드 수로 설정 합니다. 이 자습서에서는 4로 설정할 수 있습니다.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

웹 응용 프로그램을 실행 합니다. 이제 레코드는 단일 페이지에 표시 되는 레코드가 4 개이 하를 포함 하는 여러 페이지로 나뉘어 있음을 알 수 있습니다.

![페이징 추가](sorting-paging-and-filtering-data/_static/image4.png)

지연 된 쿼리 실행은 응용 프로그램의 효율성을 향상 시킵니다. GridView는 전체 데이터 집합을 검색 하는 대신 현재 페이지에 대 한 레코드만 검색 하도록 쿼리를 수정 합니다.

## <a name="filter-records-by-user-selection"></a>사용자 선택에 따라 레코드 필터링

모델 바인딩은 모델 바인딩 메서드에서 매개 변수의 값을 설정 하는 방법을 지정할 수 있는 여러 특성을 추가 합니다. 이러한 특성은 **system.web. ModelBinding** 네임 스페이스에 있습니다. 다음과 같은 변경 내용이 해당됩니다.

- 컨트롤
- 쿠키
- Form
- 프로필
- QueryString
- RouteData
- 세션
- UserProfile
- ViewState

이 자습서에서는 컨트롤의 값을 사용 하 여 GridView에 표시 되는 레코드를 필터링 합니다. 이전에 만든 쿼리 메서드에 **컨트롤** 특성을 추가 합니다. [이후](using-query-string-values-to-retrieve-data.md) 자습서에서는 매개 변수 값이 쿼리 문자열 값에서 제공 되도록 지정 하기 위해 **QueryString** 특성을 매개 변수에 적용 합니다.

먼저 ValidationSummary 위에서 표시 되는 학생을 필터링 하기 위한 드롭다운 목록을 추가 합니다.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

코드 숨김이 파일에서 컨트롤의 값을 받도록 select 메서드를 수정 하 고, 매개 변수의 이름을 값을 제공 하는 컨트롤의 이름으로 설정 합니다.

컨트롤 특성을 확인 하려면 system.web **. ModelBinding** 네임 스페이스에 대 한 **using** 문을 추가 해야 합니다.

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

다음 코드는 드롭다운 목록의 값을 기준으로 반환 된 데이터를 필터링 하기 위해 다시 작동 하는 select 메서드를 보여 줍니다. 매개 변수 앞에 컨트롤 특성을 추가 하면이 매개 변수의 값이 같은 이름의 컨트롤에서 오는 것으로 지정 됩니다.

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

웹 응용 프로그램을 실행 하 고 드롭다운 목록에서 다른 값을 선택 하 여 학생 목록을 필터링 합니다.

![학생 필터링](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a>결론

이 자습서에서는 데이터의 정렬과 페이징을 사용 하도록 설정 했습니다. 또한 컨트롤의 값을 기준으로 데이터를 필터링 할 수 있습니다.

다음 [자습서](integrating-jquery-ui.md) 에서는 JQuery ui 위젯을 동적 데이터 템플릿에 통합 하 여 ui를 향상 시킵니다.

> [!div class="step-by-step"]
> [이전](updating-deleting-and-creating-data.md)
> [다음](integrating-jquery-ui.md)
