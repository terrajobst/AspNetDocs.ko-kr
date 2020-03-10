---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: '자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기 생성'
description: 이 자습서에서는 ASP.NET 스 캐 폴딩을 사용 하 여 컨트롤러 및 뷰를 생성 하는 방법을 집중적으로 다룹니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78499475"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a>자습서: ASP.NET MVC 앱을 사용 하 여 EF Database First에 대 한 보기 생성

MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 사용자가 데이터베이스 테이블에 있는 데이터를 표시, 편집, 만들기 및 삭제할 수 있도록 하는 코드를 자동으로 생성 하는 방법을 보여 줍니다. 생성 된 코드는 데이터베이스 테이블의 열에 해당 합니다.

이 자습서에서는 ASP.NET 스 캐 폴딩을 사용 하 여 컨트롤러 및 뷰를 생성 하는 방법을 집중적으로 다룹니다.

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 스 캐 폴드 추가
> * 새 뷰에 링크 추가
> * 학생 보기 표시
> * 등록 보기 표시

## <a name="prerequisite"></a>필수 요소

* [웹 응용 프로그램 및 데이터 모델 만들기](creating-the-web-application.md)

## <a name="add-scaffold"></a>스 캐 폴드 추가

모델 클래스에 대 한 표준 데이터 작업을 제공 하는 코드를 생성할 준비가 되었습니다. 스 캐 폴드 항목을 추가 하 여 코드를 추가 합니다. 추가할 수 있는 스 캐 폴딩 유형에 대 한 다양 한 옵션이 있습니다. 이 자습서에서 스 캐 폴드는 이전 섹션에서 만든 학생 및 등록 모델에 해당 하는 컨트롤러 및 보기를 포함 합니다.

프로젝트에서 일관성을 유지 하기 위해 새 컨트롤러를 기존 **Controllers** 폴더에 추가 합니다. **Controllers** 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가** > **새 스 캐 폴드 항목**을 선택 합니다.

Entity Framework 옵션 **을 사용 하 여 뷰가 포함 된 MVC 5 컨트롤러를** 선택 합니다. 이 옵션은 모델에서 데이터를 업데이트, 삭제, 생성 및 표시 하기 위한 컨트롤러 및 뷰를 생성 합니다.

![mvc 컨트롤러 추가](generating-views/_static/image2.png)

모델 클래스에 대해 **Student (ContosoSite)** 를 선택 하 고 컨텍스트 클래스에 대 한 **개체 (ContosoSite)** 를 선택 합니다. 컨트롤러 이름을 **studentscontroller.cs**으로 유지 합니다.

**추가**를 클릭합니다.

오류가 표시 되는 경우 이전 섹션에서 프로젝트를 빌드하지 않았기 때문일 수 있습니다. 그렇다면 프로젝트를 빌드한 다음 스 캐 폴드 항목을 다시 추가 하십시오.

코드 생성 프로세스가 완료 되 면 프로젝트의 **컨트롤러** 및 **뷰** > **학생** 폴더에 새 컨트롤러 및 뷰가 표시 됩니다.

동일한 단계를 다시 수행 하지만 **등록** 클래스에 대해 스 캐 폴드를 추가 합니다. 완료 되 면 **EnrollmentsController.cs** 파일이 있고 Create, Delete, Details, Edit 및 Index 뷰가 있는 **등록** **라는 이름의 폴더가** 있습니다.

## <a name="add-links-to-new-views"></a>새 뷰에 링크 추가

새 보기를 쉽게 탐색할 수 있도록 학생 및 등록의 인덱스 보기에 두 개의 하이퍼링크를 추가할 수 있습니다. 사이트의 홈 페이지인 **보기** > **홈** > *인덱스*에서 파일을 엽니다. Jumbotron 아래에 다음 코드를 추가 합니다.

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

Html.actionlink 메서드의 경우 첫 번째 매개 변수는 링크에 표시 되는 텍스트입니다. 두 번째 매개 변수는 작업이 고 세 번째 매개 변수는 컨트롤러의 이름입니다. 예를 들어 첫 번째 링크는 Studentscontroller.cs의 인덱스 작업을 가리킵니다. 실제 하이퍼링크는 이러한 값에서 생성 됩니다. 첫 번째 링크는 궁극적으로 **Views/학생용** 폴더 내의 **인덱스 cshtml** 파일로 이동 합니다.

## <a name="display-student-views"></a>학생 보기 표시

프로젝트에 추가 된 코드가 학생 목록을 올바르게 표시 하 고 사용자가 데이터베이스에서 학생 레코드를 편집, 생성 또는 삭제할 수 있는지 확인 합니다.

**Home** > *Index* > **뷰** 를 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 선택 합니다. 응용 프로그램 홈 페이지에서 **학생 목록**을 선택 합니다.

![](generating-views/_static/image6.png)

**인덱스** 페이지에서 학생 목록과이 데이터를 수정할 링크를 확인 합니다. 새 연결 **만들기** 링크를 선택 하 고 새 학생에 대 한 일부 값을 제공 합니다. **만들기**를 클릭 하면 새 학생이 목록에 추가 된 것을 확인할 수 있습니다.

**인덱스** 페이지로 돌아가서 **편집** 링크를 선택 하 고 학생에 대 한 일부 값을 변경 합니다. **저장**을 클릭 하면 학생 레코드가 변경 된 것을 확인할 수 있습니다.

마지막으로, **삭제** 링크를 선택 하 고 **삭제** 단추를 클릭 하 여 레코드 삭제를 확인 합니다.

코드를 작성 하지 않고도 학생 테이블의 데이터에 대 한 일반 작업을 수행 하는 뷰를 추가 했습니다.

필드에 대 한 텍스트 레이블이 데이터베이스 속성 (예: **LastName**)을 기반으로 한다는 것을 알고 있을 수 있습니다 .이는 웹 페이지에 표시할 내용이 반드시 필요한 것은 아닙니다. 예를 들어 레이블을 **성**으로 지정할 수 있습니다. 자습서의 뒷부분에서이 표시 문제를 해결 합니다.

## <a name="display-enrollment-views"></a>등록 보기 표시

데이터베이스에는 학생 및 등록 테이블 간에 일 대 다 관계가 포함 되 고 강좌와 등록 테이블 간의 일 대 다 관계가 포함 됩니다. 등록에 대 한 뷰는 이러한 관계를 올바르게 처리 합니다. 사이트의 홈 페이지로 이동 하 고 **등록 목록** 링크를 선택한 다음 **새로 만들기** 링크를 선택 합니다.

이 보기에는 새 등록 레코드를 만들기 위한 양식이 표시 됩니다. 특히 **CourseID** 드롭다운 목록과 **StudentID** 드롭다운 목록이 폼에 포함 되어 있는지 확인 합니다. 둘 다 관련 테이블의 값으로 채워집니다.

또한 제공 된 값의 유효성 검사는 필드의 데이터 형식에 따라 자동으로 적용 됩니다. **등급** 에는 숫자가 필요 하므로 호환 되지 않는 값을 제공 하려고 하면 오류 메시지가 표시 됩니다. *필드 등급은 숫자* 여야 합니다.

자동 생성 된 뷰가 사용자가 데이터베이스의 데이터를 사용할 수 있도록 하는 것을 확인 했습니다. 이 시리즈의 다음 자습서에서는 데이터베이스를 업데이트 하 고 웹 응용 프로그램에서 해당 변경 작업을 수행 합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 스 캐 폴드 추가 됨
> * 새 뷰에 링크 추가 됨
> * 표시 된 학생 보기
> * 표시 된 등록 보기

데이터베이스를 변경 하는 방법을 알아보려면 다음 자습서로 이동 합니다.
> [!div class="nextstepaction"]
> [데이터베이스 변경](changing-the-database.md)