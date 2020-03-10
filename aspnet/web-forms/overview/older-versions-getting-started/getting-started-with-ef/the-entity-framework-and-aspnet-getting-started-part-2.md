---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
title: Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-2 부 | Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 응용 프로그램 샘플은 ...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: fb63a326-a4ae-4b0c-a4f5-412327197216
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2
msc.type: authoredcontent
ms.openlocfilehash: bd6a2e29e6f0df04e39be29160e2e08cc99c4706
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78456449"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-2"></a>Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작-2 부

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 자습서 시리즈에 대 한 자세한 내용은 [시리즈의 첫 번째 자습서](the-entity-framework-and-aspnet-getting-started-part-1.md) 를 참조 하십시오.

## <a name="the-entitydatasource-control"></a>EntityDataSource 컨트롤

이전 자습서에서는 웹 사이트, 데이터베이스 및 데이터 모델을 만들었습니다. 이 자습서에서는 ASP.NET에서 제공 하는 `EntityDataSource` 컨트롤을 사용 하 여 Entity Framework 데이터 모델을 쉽게 사용할 수 있도록 합니다. 학생 데이터를 표시 하 고 편집 하는 `GridView` 컨트롤, 새 학생을 추가 하기 위한 `DetailsView` 컨트롤, 부서를 선택 하기 위한 `DropDownList` 컨트롤을 만듭니다 .이 컨트롤은 나중에 관련 과정을 표시 하는 데 사용 됩니다.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image1.png)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image3.png)

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image5.png)

이 응용 프로그램에서는 데이터베이스를 업데이트 하는 페이지에 입력 유효성 검사를 추가 하지 않으며, 일부 오류 처리는 프로덕션 응용 프로그램에서 필요한 것 만큼 강력 하지 않습니다. 그러면 자습서가 Entity Framework에 초점을 맞춘 상태로 유지 되며 너무 오래 지속 되지 않습니다. 이러한 기능을 응용 프로그램에 추가 하는 방법에 대 한 자세한 내용은 [ASP.NET 페이지 및 응용 프로그램에서 ASP.NET 웹 페이지 및 오류 처리](https://msdn.microsoft.com/library/w16865z6.aspx) [에서 사용자 입력 유효성 검사](https://msdn.microsoft.com/library/7kh55542.aspx) 를 참조 하세요.

## <a name="adding-and-configuring-the-entitydatasource-control"></a>EntityDataSource 컨트롤 추가 및 구성

먼저 `People` 엔터티 집합에서 `Person` 엔터티를 읽도록 `EntityDataSource` 컨트롤을 구성 합니다.

Visual Studio가 열려 있고 1 부에서 만든 프로젝트로 작업 하 고 있는지 확인 합니다. 데이터 모델을 만든 이후 또는 마지막으로 변경한 이후 프로젝트를 빌드하지 않은 경우 지금 프로젝트를 빌드합니다. 프로젝트를 빌드할 때 까지는 디자이너에서 데이터 모델에 대 한 변경 내용을 사용할 수 없습니다.

**마스터 페이지 템플릿을 사용 하 여 Web Form** 을 사용 하 여 새 웹 페이지를 만들고 이름을 *학생과 .aspx*로 만듭니다.

[![Image23](the-entity-framework-and-aspnet-getting-started-part-2/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image7.png)

마스터 페이지로 *site.master* 를 지정 합니다. 이러한 자습서에 대해 만든 모든 페이지는이 마스터 페이지를 사용 합니다.

[![Image24](the-entity-framework-and-aspnet-getting-started-part-2/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image9.png)

다음 예제와 같이 **소스** 뷰에서 `Content2`이라는 `Content` 컨트롤에 `h2` 제목을 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample1.aspx)]

**도구 상자**의 **데이터** 탭에서 `EntityDataSource` 컨트롤을 페이지로 끌고, 머리글 아래에 놓고, ID를 `StudentsEntityDataSource`로 변경 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample2.aspx)]

**디자인** 뷰로 전환 하 고, 데이터 소스 컨트롤의 스마트 태그를 클릭 한 다음 데이터 **원본 구성** 을 클릭 하 여 **데이터 원본 구성** 마법사를 시작 합니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-2/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image11.png)

**ObjectContext 구성** 마법사 단계에서 **명명 된 연결**에 대 한 값으로 **SchoolEntities** 을 선택 하 고 **DefaultContainerName** 값으로 **SchoolEntities** 를 선택 합니다. 그런 후 **Next** 를 클릭합니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-2/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image13.png)

참고:이 시점에서 다음과 같은 대화 상자가 표시 되 면 계속 하기 전에 프로젝트를 빌드해야 합니다.

[![Image25](the-entity-framework-and-aspnet-getting-started-part-2/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image15.png)

**데이터 선택 구성** 단계에서 **EntitySetName**에 대 한 값으로 **사용자** 를 선택 합니다. **선택**에서 ll **선택** 확인란을 선택 했는지 확인 합니다. 그런 다음 업데이트 및 삭제를 사용 하도록 설정 하는 옵션을 선택 합니다. 완료 되 면 **마침**을 클릭 합니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-2/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image17.png)

## <a name="configuring-database-rules-to-allow-deletion"></a>삭제할 수 있도록 데이터베이스 규칙 구성

사용자가 `Person` 테이블에서 학생을 삭제할 수 있는 페이지를 만듭니다 (`Course`, `StudentGrade`및 `OfficeAssignment`). 기본적으로 데이터베이스는 다른 테이블 중 하나에 관련 행이 있는 경우 `Person`의 행을 삭제 하는 것을 방지 합니다. 관련 행을 수동으로 삭제 하거나 `Person` 행을 삭제할 때 데이터베이스에서 자동으로 삭제 하도록 구성할 수 있습니다. 이 자습서에서 학생 레코드의 경우 관련 데이터를 자동으로 삭제 하도록 데이터베이스를 구성 합니다. 학습자는 `StudentGrade` 테이블에만 관련 행을 포함할 수 있기 때문에 세 관계 중 하나만 구성 해야 합니다.

이 자습서와 관련 된 프로젝트에서 다운로드 한 *School .mdf* 파일을 사용 하는 경우 이러한 구성 변경이 이미 수행 되었기 때문에이 섹션을 건너뛸 수 있습니다. 스크립트를 실행 하 여 데이터베이스를 만든 경우에는 다음 절차를 수행 하 여 데이터베이스를 구성 합니다.

**서버 탐색기**에서 1 부에서 만든 데이터베이스 다이어그램을 엽니다. `Person`와 `StudentGrade` 사이의 관계를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-2/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image19.png)

**속성** 창에서 **삽입 및 업데이트 사양** 을 확장 하 고 **DeleteRule** 속성을 **Cascade**로 설정 합니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-2/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image21.png)

다이어그램을 저장 하 고 닫습니다. 데이터베이스를 업데이트할지 여부를 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.

모델에서 메모리에 있는 엔터티가 데이터베이스에서 수행 하는 작업과 동기화 되도록 하려면 데이터 모델에서 해당 규칙을 설정 해야 합니다. *SchoolModel*를 열고 `Person`와 `StudentGrade`사이의 연결 선을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 선택 합니다.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-2/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image23.png)

**속성** 창에서 **End1 OnDelete** 를 **Cascade**로 설정 합니다.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-2/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image25.png)

*SchoolModel* 파일을 저장 하 고 닫은 다음 프로젝트를 다시 빌드합니다.

일반적으로 데이터베이스가 변경 되 면 모델을 동기화 하는 방법에 대 한 몇 가지 옵션을 선택할 수 있습니다.

- 특정 종류의 변경 (예: 테이블, 뷰 또는 저장 프로시저 추가 또는 새로 고침)의 경우 디자이너를 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스에서 모델 업데이트** 를 선택 하 여 디자이너가 자동으로 변경을 수행 하도록 합니다.
- 데이터 모델을 다시 생성 합니다.
- 다음과 같이 수동 업데이트를 만듭니다.

이 경우 모델을 다시 생성 하거나 관계 변경의 영향을 받는 테이블을 새로 고칠 수 있지만, 필드 이름 변경을 다시 수행 해야 합니다 (`FirstName`에서 `FirstMidName`로).

## <a name="using-a-gridview-control-to-read-and-update-entities"></a>GridView 컨트롤을 사용 하 여 엔터티 읽기 및 업데이트

이 섹션에서는 `GridView` 컨트롤을 사용 하 여 학생을 표시, 업데이트 또는 삭제 합니다.

을 열거나 *학습자* 로 전환 하 여 **디자인** 뷰로 전환 합니다. **도구 상자**의 **데이터** 탭에서 `GridView` 컨트롤을 `EntityDataSource` 컨트롤의 오른쪽으로 끌고 `StudentsGridView`이름을로 지정한 다음 스마트 태그를 클릭 하 고 **StudentsEntityDataSource** 를 데이터 원본으로 선택 합니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-2/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image27.png)

**스키마 새로 고침** (확인 메시지가 표시 되 면 **예** 를 클릭)을 클릭 하 고 **페이징 사용**, **정렬 사용**, **편집 사용**, **삭제 사용**을 차례로 클릭 합니다.

**열 편집**을 클릭 합니다.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-2/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image29.png)

**선택한 필드** 상자에서 **PersonID**, **LastName**및 **HireDate**를 삭제 합니다. 일반적으로 사용자에 게는 레코드 키가 표시 되지 않으며 고용 날짜는 학생에 게는 없으므로 이름 필드 중 하나만 있으면 됩니다.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-2/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image31.png)

**FirstMidName** 필드를 선택한 다음 **이 필드를 templatefield로 변환로 변환**을 클릭 합니다.

**EnrollmentDate**에 대해 동일한 작업을 수행 합니다.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-2/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image33.png)

**확인** 을 클릭 한 다음 **원본** 뷰로 전환 합니다. 나머지 변경 내용은 태그에서 직접 수행 하는 것이 더 쉽습니다. 이제 `GridView` 컨트롤 태그는 다음 예제와 같습니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample3.aspx)]

명령 필드 뒤의 첫 번째 열은 현재 이름을 표시 하는 템플릿 필드입니다. 이 템플릿 필드의 태그를 다음 예제와 같이 변경 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample4.aspx)]

표시 모드에서 두 개의 `Label` 컨트롤은 성과 이름을 표시 합니다. 편집 모드에서는 이름과 성을 변경할 수 있도록 두 개의 입력란이 제공 됩니다. 표시 모드의 `Label` 컨트롤과 마찬가지로, 데이터베이스에 직접 연결 되는 ASP.NET 데이터 소스 컨트롤을 사용 하는 것과 동일 하 게 `Bind` 및 `Eval` 식을 사용 합니다. 유일한 차이점은 데이터베이스 열 대신 엔터티 속성을 지정 하는 것입니다.

마지막 열은 등록 날짜를 표시 하는 템플릿 필드입니다. 이 필드에 대 한 태그를 다음 예제와 같이 변경 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample5.aspx)]

표시 및 편집 모드에서 형식 문자열 "{0, d}"는 날짜를 "간단한 날짜" 형식으로 표시 합니다. 이 자습서에 표시 된 화면 이미지와 다르게이 형식을 표시 하도록 컴퓨터를 구성할 수 있습니다.

이러한 각 템플릿 필드에서 디자이너는 기본적으로 `Bind` 식을 사용 했지만 `ItemTemplate` 요소의 `Eval` 식으로 변경 했습니다. `Bind` 식은 코드에서 데이터에 액세스 해야 하는 경우 데이터를 `GridView` 컨트롤 속성에서 사용할 수 있도록 합니다. 이 페이지에서는 코드에서이 데이터에 액세스할 필요가 없으므로 보다 효율적인 `Eval`를 사용할 수 있습니다. 자세한 내용은 데이터 [컨트롤에서 데이터 가져오기](https://weblogs.asp.net/davidfowler/archive/2008/12/12/getting-your-data-out-of-the-data-controls.aspx)를 참조 하세요.

## <a name="revising-entitydatasource-control-markup-to-improve-performance"></a>EntityDataSource 컨트롤 태그를 수정 하 여 성능 향상

`EntityDataSource` 컨트롤에 대 한 태그에서 `ConnectionString` 및 `DefaultContainerName` 특성을 제거 하 고이를 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 특성으로 바꿉니다. 이는 개체 컨텍스트 클래스에서 하드 코딩 된 연결을 사용 해야 하는 경우를 제외 하 고 `EntityDataSource` 컨트롤을 만들 때마다 수행 해야 하는 변경 내용입니다. `ContextTypeName` 특성을 사용 하면 다음과 같은 이점이 있습니다.

- 성능 향상. `EntityDataSource` 컨트롤은 `ConnectionString` 및 `DefaultContainerName` 특성을 사용 하 여 데이터 모델을 초기화할 때 모든 요청에 대해 메타 데이터를 로드 하기 위해 추가 작업을 수행 합니다. `ContextTypeName` 특성을 지정 하는 경우에는이 작업이 필요 하지 않습니다.
- 지연 로드는 4.0 Entity Framework에서 생성 된 개체 컨텍스트 클래스 (예:이 자습서의 `SchoolEntities`)에서 기본적으로 설정 되어 있습니다. 즉, 필요한 경우 탐색 속성이 관련 데이터로 자동으로 로드 됩니다. 지연 로드는이 자습서의 뒷부분에서 자세히 설명 합니다.
- 개체 컨텍스트 클래스에 적용 한 사용자 지정 (이 경우 `SchoolEntities` 클래스)은 `EntityDataSource` 컨트롤을 사용 하는 컨트롤에 사용할 수 있습니다. 개체 컨텍스트 클래스를 사용자 지정 하는 것은이 자습서 시리즈에서 다루지 않는 고급 항목입니다. 자세한 내용은 [생성 된 형식 Entity Framework 확장](https://msdn.microsoft.com/library/dd456844.aspx)을 참조 하세요.

이제 태그는 다음 예제와 유사 합니다. 속성의 순서는 다를 수 있습니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample6.aspx)]

`EnableFlattening` 특성은 외래 키 열이 엔터티 속성으로 노출 되지 않기 때문에 이전 버전의 Entity Framework에서 필요한 기능을 나타냅니다. 현재 버전을 사용 하면 *외래 키 연결*을 사용할 수 있습니다. 즉, foreign key 속성은 다대다 연결 모두에 대해 노출 됩니다. 엔터티에 외래 키 속성과 [복합 형식이](https://msdn.microsoft.com/library/bb738472.aspx)없는 경우이 특성을 `False`로 설정 된 상태로 둘 수 있습니다. 기본값은 `True`이므로 태그에서 특성을 제거 하지 마십시오. 자세한 내용은 [개체 평면화 (EntityDataSource)](https://msdn.microsoft.com/library/ee404746.aspx)를 참조 하세요.

페이지를 실행 하면 학생 및 직원 목록이 표시 됩니다 (다음 자습서에서 학생만 필터링 함). 이름 및 성이 함께 표시 됩니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-2/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image35.png)

표시를 정렬 하려면 열 이름을 클릭 합니다.

아무 행에서 나 **편집** 을 클릭 합니다. 텍스트 상자가 표시 되며, 여기서 성과 이름을 변경할 수 있습니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-2/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image37.png)

**삭제** 단추도 작동 합니다. 등록 날짜가 있는 행에 대해 삭제를 클릭 하면 행이 사라집니다. 등록 날짜가 없는 행은 강사를 나타내며 참조 무결성 오류가 발생할 수 있습니다. 다음 자습서에서는 학생만 포함 하도록이 목록을 필터링 합니다.

## <a name="displaying-data-from-a-navigation-property"></a>탐색 속성에서 데이터 표시

이제 각 학생이 등록 된 과정의 수를 알고 싶습니다. Entity Framework는 `Person` 엔터티의 `StudentGrades` 탐색 속성에 해당 정보를 제공 합니다. 데이터베이스 디자인은 등급이 할당 되지 않은 과정에서 학생 등록을 허용 하지 않기 때문에이 자습서에서는 과정에 연결 된 `StudentGrade` 테이블 행에 행이 있는 경우 과정에 등록 된 것과 동일한 것으로 간주할 수 있습니다. `Courses` 탐색 속성은 강사 전용입니다.

`EntityDataSource` 컨트롤의 `ContextTypeName` 특성을 사용 하는 경우 Entity Framework는 해당 속성에 액세스할 때 탐색 속성에 대 한 정보를 자동으로 검색 합니다. 이를 *지연 로드*라고 합니다. 그러나이는 추가 정보가 필요할 때마다 데이터베이스에 대 한 별도의 호출을 생성 하므로 비효율적 일 수 있습니다. `EntityDataSource` 컨트롤에서 반환 하는 모든 엔터티에 대 한 탐색 속성의 데이터가 필요한 경우 데이터베이스에 대 한 단일 호출에서 엔터티 자체와 함께 관련 데이터를 검색 하는 것이 더 효율적입니다. 이를 *즉시 로드*라고 하며, `EntityDataSource` 컨트롤의 `Include` 속성을 설정 하 여 탐색 속성에 대 한 즉시 로드를 지정 합니다.

*학습자*에서는 모든 학생에 대 한 과정의 수를 표시 하 여 즉시 로드를 선택 하는 것이 좋습니다. 모든 학생을 표시 했지만 일부에 대해서만 강좌 수를 표시 하는 경우 (태그 외에 일부 코드를 작성 해야 함) 지연 로드를 선택 하는 것이 더 적합할 수 있습니다.

을 열거나 *학습자*로 전환 하 고, **디자인** 뷰로 전환 하 고, `StudentsEntityDataSource`를 선택 하 고, **속성** 창에서 **Include** 속성을 **StudentGrades**로 설정 합니다. 여러 탐색 속성을 가져오려는 경우에는 이름을 쉼표로 구분 하 여 지정할 수 있습니다 (예: **StudentGrades, 강좌**).

[![Image19](the-entity-framework-and-aspnet-getting-started-part-2/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image39.png)

**원본** 뷰로 전환 합니다. `StudentsGridView` 컨트롤의 마지막 `asp:TemplateField` 요소 뒤에 다음 새 템플릿 필드를 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample7.aspx)]

`Eval` 식에서 `StudentGrades`탐색 속성을 참조할 수 있습니다. 이 속성에는 컬렉션이 포함 되어 있기 때문에 학생이 등록 된 과정 수를 표시 하는 데 사용할 수 있는 `Count` 속성이 있습니다. 이후 자습서에서는 컬렉션 대신 단일 엔터티를 포함 하는 탐색 속성의 데이터를 표시 하는 방법을 알아봅니다. `BoundField` 요소를 사용 하 여 탐색 속성의 데이터를 표시할 수 없습니다.

페이지를 실행 하면 각 학생이 등록 된 과정의 수를 확인할 수 있습니다.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-2/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image41.png)

## <a name="using-a-detailsview-control-to-insert-entities"></a>DetailsView 컨트롤을 사용 하 여 엔터티 삽입

다음 단계는 새 학생을 추가할 수 있는 `DetailsView` 컨트롤을 포함 하는 페이지를 만드는 것입니다. 브라우저를 닫은 다음, *site.master* 마스터 페이지를 사용 하 여 새 웹 페이지를 만듭니다. *StudentsAdd*페이지 이름을 지정한 다음 **소스** 뷰로 전환 합니다.

다음 태그를 추가 하 여 `Content2`이라는 `Content` 컨트롤에 대 한 기존 태그를 바꿉니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample8.aspx)]

이 태그를 사용 하면 *학습자*에서 만든 것과 비슷한 `EntityDataSource` 컨트롤을 만들 수 있습니다. 단, 삽입할 수 있습니다. `GridView` 컨트롤과 마찬가지로 `DetailsView` 컨트롤의 바인딩된 필드는 엔터티 속성을 참조 하는 경우를 제외 하 고는 데이터베이스에 직접 연결 하는 데이터 컨트롤의 경우와 동일 하 게 코딩 됩니다. 이 경우 `DetailsView` 컨트롤은 행을 삽입 하는 데만 사용 되므로 기본 모드를 `Insert`으로 설정 했습니다.

페이지를 실행 하 고 새 학생을 추가 합니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-2/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image43.png)

새 학생을 삽입 한 후에는 아무 작업도 수행 되지 않지만 이제 *학습자*를 실행 하는 경우 새 학생 정보를 볼 수 있습니다.

## <a name="displaying-data-in-a-drop-down-list"></a>드롭다운 목록에 데이터 표시

다음 단계에서는 `EntityDataSource` 컨트롤을 사용 하 여 `DropDownList` 컨트롤을 엔터티 집합에 대 한 databind 합니다. 자습서의이 부분에서는이 목록에서 많은 작업을 수행 하지 않습니다. 그러나 후속 부분에서이 목록을 사용 하 여 사용자가 부서를 선택 하 여 부서와 연결 된 과정을 표시할 수 있습니다.

*Default.aspx*라는 새 웹 페이지를 만듭니다. **소스** 뷰에서 이름이 `Content2`인 `Content` 컨트롤에 제목을 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample9.aspx)]

**디자인** 뷰에서 이전 처럼 페이지에 `EntityDataSource` 컨트롤을 추가 합니다. 단,이 시간 이름을 `DepartmentsEntityDataSource`. **EntitySetName** 값으로 **부서** 를 선택 하 고 **DepartmentID** 및 **Name** 속성만 선택 합니다.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-2/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image45.png)

**도구 상자**의 **표준** 탭에서 `DropDownList` 컨트롤을 페이지로 끌고, `DepartmentsDropDownList`이름을로 설정 하 고, 스마트 태그를 클릭 하 고, **데이터 소스 선택** 을 선택 하 여 **DataSource 구성 마법사**를 시작 합니다.

[![Image16](the-entity-framework-and-aspnet-getting-started-part-2/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image47.png)

**데이터 원본 선택** 단계에서 **DepartmentsEntityDataSource** 를 데이터 원본으로 선택 하 고 **스키마 새로 고침**을 클릭 한 다음, 표시할 데이터 필드로 **이름** 을 선택 하 고 값 데이터 필드로 **DepartmentID** 를 선택 합니다. **확인**을 클릭합니다.

[![Image17](the-entity-framework-and-aspnet-getting-started-part-2/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image49.png)

Entity Framework를 사용 하 여 컨트롤의 데이터를 바인딩하는 데 사용 하는 메서드는 엔터티와 엔터티 속성을 지정 하는 경우를 제외 하 고는 다른 ASP.NET 데이터 소스 컨트롤과 동일 합니다.

**원본** 뷰로 전환 하 고 `DropDownList` 컨트롤 바로 앞에 "부서 선택:"을 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-2/samples/sample10.aspx)]

이 시점에서 `ConnectionString` 및 `DefaultContainerName` 특성을 `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` 특성으로 바꿔서 `EntityDataSource` 컨트롤에 대 한 태그를 변경 합니다. `EntityDataSource` 컨트롤 태그를 변경 하기 전에 데이터 소스 컨트롤에 연결 된 데이터 바인딩된 컨트롤을 만들 때까지 기다리는 것이 좋습니다. 변경 후 디자이너는 데이터 바인딩된 컨트롤에 **새로 고침 스키마** 옵션을 제공 하지 않기 때문입니다.

페이지를 실행 하 고 드롭다운 목록에서 부서를 선택할 수 있습니다.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-2/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-2/_static/image51.png)

이렇게 하면 `EntityDataSource` 컨트롤 사용에 대 한 소개를 완료 합니다. 일반적으로이 컨트롤을 사용 하는 것은 테이블 및 열 대신 엔터티와 속성을 참조 한다는 점을 제외 하 고는 다른 ASP.NET 데이터 원본 컨트롤과 작업 하는 것과는 다릅니다. 단, 탐색 속성에 액세스 하려는 경우는 예외입니다. 다음 자습서에서는 데이터를 필터링, 그룹화 및 정렬 하는 경우 `EntityDataSource` 컨트롤과 함께 사용 하는 구문이 다른 데이터 소스 컨트롤과 다를 수 있다는 것을 알 수 있습니다.

> [!div class="step-by-step"]
> [이전](the-entity-framework-and-aspnet-getting-started-part-1.md)
> [다음](the-entity-framework-and-aspnet-getting-started-part-3.md)
