---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: 모델 바인딩 및 web forms에 JQuery UI Datepicker 통합 | Microsoft Docs
author: Rick-Anderson
description: 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 상호 작용이 더 간편 하 게-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78521981"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a>모델 바인딩 및 web forms에 JQuery UI Datepicker 통합

[Tom FitzMacken](https://github.com/tfitzmac)

> 이 자습서 시리즈에서는 ASP.NET Web Forms 프로젝트를 사용 하 여 모델 바인딩을 사용 하는 기본적인 측면을 보여 줍니다. 모델 바인딩을 사용 하면 데이터 원본 개체 (예: ObjectDataSource 또는 SqlDataSource)를 처리 하는 것 보다 데이터 상호 작용이 보다 간단 하 게 진행 됩니다. 이 시리즈는 소개 자료로 시작 하 고 이후 자습서에서 보다 고급 개념으로 이동 합니다.
> 
> 이 자습서에서는 웹 양식에 JQuery UI [Datepicker 위젯을](http://jqueryui.com/datepicker/) 추가 하 고 모델 바인딩을 사용 하 여 선택한 값으로 데이터베이스를 업데이트 하는 방법을 보여 줍니다.
> 
> 이 자습서는 계열의 [첫](retrieving-data.md) 번째와 [두 번째](updating-deleting-and-creating-data.md) 부분에서 만든 프로젝트를 기반으로 합니다.
> 
> 또는 VB [download](https://go.microsoft.com/fwlink/?LinkId=286116) 에서 C# 전체 프로젝트를 다운로드할 수 있습니다. 다운로드 가능한 코드는 Visual Studio 2012 또는 Visual Studio 2013와 함께 작동 합니다. 이 자습서에서는이 자습서에 표시 된 Visual Studio 2013 템플릿과 약간 다른 Visual Studio 2012 템플릿을 사용 합니다.

## <a name="what-youll-build"></a>빌드할 내용

이 자습서에서는 다음을 수행합니다.

1. 모델에 속성을 추가 하 여 학생의 등록 날짜 기록
2. 사용자가 JQuery UI Datepicker 위젯을 사용 하 여 등록 날짜를 선택할 수 있습니다.
3. 등록 날짜에 대 한 유효성 검사 규칙 적용

사용자는 JQuery UI Datepicker 위젯을 사용 하 여 사용자가 필드와 상호 작용할 때 팝업 되는 달력에서 날짜를 쉽게 선택할 수 있습니다. 이 위젯을 사용 하면 사용자가 수동으로 날짜를 입력 하는 것 보다 더 편리할 수 있습니다. 데이터 작업에 모델 바인딩을 사용 하는 페이지에 Datepicker 위젯을 통합 하려면 약간의 추가 작업만 필요 합니다.

## <a name="add-a-new-property-to-the-model"></a>모델에 새 속성 추가

먼저 Student 모델에 **Datetime** 속성을 추가 하 고이 변경 내용을 데이터베이스로 마이그레이션합니다. **UniversityModels.cs**를 열고 강조 표시 된 코드를 학생 모델에 추가 합니다.

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

범위 **특성** 은 속성에 대 한 유효성 검사 규칙을 적용 하기 위해 포함 됩니다. 이 자습서에서는 Contoso 대학이 2013 년 1 월 1 일에 설립 된 것으로 가정 하므로 이전 등록 날짜가 유효 하지 않습니다.

패키지 관리 창에서 **add Migration AddEnrollmentDate**명령을 실행 하 여 마이그레이션을 추가 합니다. 마이그레이션 코드는 Student 테이블에 새 Datetime 열을 추가 합니다. 범위 특성에 지정 된 값과 일치 시키려면 아래 강조 표시 된 코드에 표시 된 대로 새 열에 대 한 기본값을 추가 합니다.

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

마이그레이션 파일의 변경 내용을 저장 합니다.

데이터를 다시 시드해야 할 필요는 없습니다. 따라서 마이그레이션 폴더에서 **Configuration.cs** 를 열고 **초기값** 메서드에서 코드를 제거 하거나 주석으로 처리 합니다. 파일을 저장하고 닫습니다.

이제 **update-database**명령을 실행 합니다. 이제 열이 데이터베이스에 존재 하 고 모든 기존 레코드에 EnrollmentDate에 대 한 기본값이 있습니다.

## <a name="add-dynamic-controls-for-enrollment-date"></a>등록 날짜에 대 한 동적 컨트롤 추가

이제 등록 날짜를 표시 하 고 편집 하기 위한 컨트롤을 추가 합니다. 이 시점에서 텍스트 상자를 통해 값을 편집 합니다. 이 자습서의 뒷부분에서 텍스트 상자를 JQuery Datepicker widget으로 변경 합니다.

먼저 **Addstudent .aspx** 파일을 변경 하지 않아도 된다는 점에 유의 해야 합니다. DynamicEntity 컨트롤이 새 속성을 자동으로 렌더링 합니다.

**학습자**를 열고 다음 강조 표시 된 코드를 추가 합니다.

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

응용 프로그램을 실행 하 고 날짜를 입력 하 여 등록 날짜의 값을 설정할 수 있는지 확인 합니다. 새 학생을 추가 하는 경우:

![날짜 설정](integrating-jquery-ui/_static/image1.png)

또는 기존 값을 편집 합니다.

![날짜 편집](integrating-jquery-ui/_static/image2.png)

날짜를 입력 하는 작업은 작동 하지만 사용자가 제공 하려는 사용자 환경이 아닐 수도 있습니다. 다음 섹션에서는 달력을 통해 날짜를 선택 하도록 설정 합니다.

## <a name="install-nuget-package-to-work-with-jquery-ui"></a>JQuery UI를 사용 하려면 NuGet 패키지를 설치 합니다.

**주스 ui** NuGet 패키지를 사용 하면 JQuery ui 위젯을 웹 응용 프로그램에 쉽게 통합할 수 있습니다. 이 패키지를 사용 하려면 NuGet을 통해 설치 합니다.

![주스 UI 추가](integrating-jquery-ui/_static/image3.png)

설치한 주스 UI 버전이 응용 프로그램의 JQuery 버전과 충돌할 수 있습니다. 이 자습서를 진행 하기 전에 응용 프로그램을 실행 해 보세요. JavaScript 오류가 발생 하면 JQuery 버전을 조정 해야 합니다. 필요한 JQuery 버전을 Scripts 폴더에 추가할 수 있습니다 (이 자습서를 작성할 때 버전 1.8.2). 또는 site.master에서 JQuery 파일의 경로를 지정 합니다.

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a>Datepicker 위젯을 포함 하도록 DateTime 템플릿 사용자 지정

Datetime 값을 편집 하기 위해 동적 데이터 템플릿에 Datepicker 위젯을 추가 합니다. 템플릿에 위젯을 추가 하면 새 학생을 추가 하기 위한 양식과 학생 편집을 위한 그리드 보기에서 자동으로 렌더링 됩니다. **날짜/시간\_** 을 열고 다음 강조 표시 된 코드를 추가 합니다.

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

코드 숨김이 있는 파일에서는 DatePicker에 대 한 최소 및 최대 날짜를 설정 합니다. 이러한 값을 설정 하 여 사용자가 잘못 된 날짜로 이동 하는 것을 방지할 수 있습니다. DateTime 속성의 범위 **특성** (제공 된 경우)에 대 한 최소값과 최대값을 검색 합니다. **DateTime\_Edit.ascx.cs**를 열고 페이지\_Load 메서드에 다음 강조 표시 된 코드를 추가 합니다.

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

웹 응용 프로그램을 실행 하 고 AddStudent 페이지로 이동 합니다. 필드에 대 한 값을 제공 합니다. 등록 날짜에 대 한 텍스트 상자를 클릭 하면 달력이 표시 됩니다.

![날짜 선택](integrating-jquery-ui/_static/image4.png)

날짜를 선택 하 고 **삽입**을 클릭 합니다. 범위 특성은 서버에 대 한 유효성 검사를 적용 합니다. Datepicker에 minDate 속성을 설정 하 여 클라이언트에서 유효성 검사도 적용 합니다. 달력을 사용 하면 사용자가 minDate 값 이전 날짜로 이동할 수 없습니다.

그리드 보기에서 레코드를 편집 하는 경우에도 달력이 표시 됩니다.

![GridView의 Datepicker](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a>결론

이 자습서에서는 모델 바인딩을 사용 하는 웹 폼에 JQuery 위젯을 통합 하는 방법에 대해 알아보았습니다.

다음 [자습서](using-query-string-values-to-retrieve-data.md)에서는 데이터를 선택 하는 경우 쿼리 문자열 값을 사용 합니다.

> [!div class="step-by-step"]
> [이전](sorting-paging-and-filtering-data.md)
> [다음](using-query-string-values-to-retrieve-data.md)
