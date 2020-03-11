---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: 쿼리 문자열 값을 사용 하 여 모델 바인딩 및 web forms을 사용 하 여 데이터 필터링 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78519083"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a>쿼리 문자열 값을 사용 하 여 모델 바인딩 및 web forms을 사용 하 여 데이터 필터링

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다. 이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.
> 
> 이 자습서에서는 쿼리 문자열에서 값을 전달 하 고이 값을 사용 하 여 모델 바인딩을 통해 데이터를 검색 하는 방법을 보여 줍니다.
> 
> 이 자습서는 시리즈의 [이전](retrieving-data.md) 부분에서 만든 프로젝트를 기반으로 합니다.
> 
> 또는 VB [download](https://go.microsoft.com/fwlink/?LinkId=286116) 에서 C# 전체 프로젝트를 다운로드할 수 있습니다. 다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013와 함께 작동 합니다. 이 자습서에서는이 자습서에 표시 된 Visual Studio 2013 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.

## <a name="what-youll-build"></a>빌드할 내용

이 자습서에서는 다음을 수행합니다.

1. 학생에 대해 등록 된 과정을 표시 하는 새 페이지를 추가 합니다.
2. 쿼리 문자열의 값을 기준으로 선택한 학생에 대해 등록 된 과정을 검색 합니다.
3. 표 보기의 쿼리 문자열 값이 포함 된 하이퍼링크를 새 페이지에 추가 합니다.

이 자습서의 단계는 드롭다운 목록에서 사용자가 선택한 항목을 기반으로 표시 된 학생을 필터링 하기 위해 이전 [자습서](sorting-paging-and-filtering-data.md) 에서 수행한 것과 매우 비슷합니다. 이 자습서에서는 select 메서드에 **컨트롤** 특성을 사용 하 여 매개 변수 값이 컨트롤에서 오는 것으로 지정 했습니다. 이 자습서에서는 select 메서드에 **QueryString** 특성을 사용 하 여 매개 변수 값이 쿼리 문자열에서 오는 것으로 지정 합니다.

## <a name="add-new-page-for-displaying-a-students-courses"></a>학생 과정을 표시 하기 위한 새 페이지 추가

Site.master 마스터 페이지를 사용 하는 새 웹 폼을 추가 하 고 페이지 **코스**의 이름을로 합니다.

**강의** 파일에서 선택한 학생에 대 한 과정을 표시 하는 그리드 보기를 추가 합니다.

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a>Select 메서드 정의

**Courses.aspx.cs**에서 표 뷰의 **SelectMethod** 속성에 지정한 이름으로 select 메서드를 추가 합니다. 이 메서드에서는 학생의 강좌를 검색 하는 쿼리를 정의 하 고 매개 변수와 이름이 같은 쿼리 문자열 값에서 매개 변수를 가져오도록 지정 합니다.

먼저 다음 **using** 문을 추가 해야 합니다.

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

그런 다음 Courses.aspx.cs에 다음 코드를 추가 합니다.

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

QueryString 특성은 StudentID 라는 쿼리 문자열 값이이 메서드의 매개 변수에 자동으로 할당 된다는 것을 의미 합니다.

## <a name="add-hyperlink-with-query-string-value"></a>쿼리 문자열 값을 사용 하 여 하이퍼링크 추가

학습자의 그리드 보기에서 새 과정 페이지에 연결 되는 하이퍼링크 필드를 추가 합니다. 하이퍼링크는 학생 id를 포함 하는 쿼리 문자열 값을 포함 합니다.

학생의 경우 전체 크레딧을 위한 필드 바로 아래에 있는 그리드 뷰 열에 다음 필드를 추가 합니다.

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

응용 프로그램을 실행 하 고 그리드 뷰에 이제 과정 링크가 포함 되어 있는지 확인 합니다.

![하이퍼링크 추가](using-query-string-values-to-retrieve-data/_static/image1.png)

링크 중 하나를 클릭 하면 학생의 등록 된 강좌가 표시 됩니다.

![과정 표시](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a>결론

이 자습서에서는 쿼리 문자열 값을 포함 하는 링크를 추가 했습니다. Select 메서드의 매개 변수 값에 해당 쿼리 문자열 값을 사용 했습니다.

다음 [자습서](adding-business-logic-layer.md)에서는 코드를 코드 숨김이 파일에서 비즈니스 논리 계층 및 데이터 액세스 계층으로 이동 합니다.

> [!div class="step-by-step"]
> [이전](integrating-jquery-ui.md)
> [다음](adding-business-logic-layer.md)
