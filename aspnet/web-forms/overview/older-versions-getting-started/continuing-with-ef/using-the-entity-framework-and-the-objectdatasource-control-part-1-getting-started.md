---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: 'Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용, 1 부: 시작 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈는 Entity Framework 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. ...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 2f14707eb058d438495dd2bc4c17b976c471fc97
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78440405"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용, 1 부: 시작

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈는 [Entity Framework 4.0](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서의 시작 점으로, 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 수 있습니다. 전체 자습서 시리즈에서 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 수도 있습니다.
> 
> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은 가상의 Contoso 대학 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다.
> 
> 이 자습서에서는의 C#예제를 보여 줍니다. [다운로드 가능한 샘플](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 에는 및 Visual Basic C# 모두의 코드가 포함 되어 있습니다.
> 
> ## <a name="database-first"></a>Database First
> 
> Entity Framework에서 데이터를 사용할 수 있는 방법에는 *Database First*, *Model First*및 *Code First*의 세 가지가 있습니다. 이 자습서는 Database First에 대 한 것입니다. 이러한 워크플로의 차이점과 시나리오에 가장 적합 한 지침을 선택 하는 방법에 대 한 자세한 내용은 [Entity Framework 개발 워크플로](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)를 참조 하세요.
> 
> ## <a name="web-forms"></a>웹 양식
> 
> 시작 시리즈와 마찬가지로이 자습서 시리즈에서는 ASP.NET Web Forms 모델을 사용 하며, Visual Studio에서 ASP.NET Web Forms를 사용 하는 방법을 알고 있다고 가정 합니다. 그렇지 않은 경우 [ASP.NET 4.5 Web Forms 시작](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)을 참조 하세요. ASP.NET MVC 프레임 워크를 사용 하려는 경우 [ASP.NET mvc를 사용 하 여 Entity Framework 시작](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)을 참조 하세요.
> 
> ## <a name="software-versions"></a>소프트웨어 버전
> 
> | **자습서에 표시 됨** | **또한와 함께 작동 합니다.** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express for Web. 이 자습서는 이후 버전의 Visual Studio에서 테스트 되지 않았습니다. 메뉴 선택 항목, 대화 상자 및 템플릿에는 여러 가지 차이점이 있습니다. |
> | .NET 4 | .NET 4.5은 이전 버전인 .NET 4와 호환 되지만이 자습서는 .NET 4.5에서 테스트 되지 않았습니다. |
> | Entity Framework 4 | 이 자습서는 Entity Framework의 이후 버전에서 테스트 되지 않았습니다. Entity Framework 5부터 EF는 기본적으로 EF 4.1에 도입 된 `DbContext API`를 사용 합니다. EntityDataSource 컨트롤은 `ObjectContext` API를 사용 하도록 설계 되었습니다. `DbContext` API에서 EntityDataSource 컨트롤을 사용 하는 방법에 대 한 자세한 내용은 [이 블로그 게시물](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)을 참조 하세요. |
> 
> ## <a name="questions"></a>질문
> 
> 자습서와 직접 관련 되지 않은 질문이 있는 경우 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx), [Entity Framework 및 LINQ to Entities 포럼](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)또는 [StackOverflow.com](http://stackoverflow.com/)에 게시할 수 있습니다.

`EntityDataSource` 컨트롤을 사용 하면 응용 프로그램을 매우 빠르게 만들 수 있지만 일반적으로는 *.aspx* 페이지에서 상당한 양의 비즈니스 논리 및 데이터 액세스 논리를 유지 해야 합니다. 응용 프로그램의 복잡성이 증가 하 고 지속적으로 유지 관리를 요구 하는 경우 보다 쉽게 유지 관리 되는 *n 계층* 또는 *계층화* 된 응용 프로그램 구조를 만들기 위해 개발 시간을 더 많이 투자할 수 있습니다. 이 아키텍처를 구현 하려면 BLL (비즈니스 논리 계층) 및 DAL (데이터 액세스 계층)에서 프레젠테이션 계층을 분리 합니다. 이 구조를 구현 하는 한 가지 방법은 `EntityDataSource` 컨트롤 대신 `ObjectDataSource` 컨트롤을 사용 하는 것입니다. `ObjectDataSource` 컨트롤을 사용 하는 경우 고유한 데이터 액세스 코드를 구현한 다음 다른 데이터 소스 컨트롤과 동일한 많은 기능을 포함 하는 컨트롤을 사용 하 여 .aspx 페이지에서 호출 합니다 *.* 이를 통해 데이터 액세스를 위해 Web Forms 컨트롤을 사용할 때의 이점에 n 계층 방식의 이점을 결합할 수 있습니다.

`ObjectDataSource` 컨트롤은 다른 방법으로도 더 많은 유연성을 제공 합니다. 사용자 고유의 데이터 액세스 코드를 작성 하기 때문에 `EntityDataSource` 컨트롤에서 수행 하도록 디자인 된 작업 인 특정 엔터티 형식을 읽기, 삽입, 업데이트 또는 삭제 하는 것 보다 더 쉽게 수행할 수 있습니다. 예를 들어 엔터티가 업데이트 될 때마다 로깅을 수행 하거나, 엔터티가 삭제 될 때마다 데이터를 보관 하거나, 외래 키 값이 포함 된 행을 삽입할 때 필요한 경우 관련 데이터를 자동으로 확인 하 고 업데이트할 수 있습니다.

## <a name="business-logic-and-repository-classes"></a>비즈니스 논리 및 리포지토리 클래스

`ObjectDataSource` 컨트롤은 사용자가 만드는 클래스를 호출 하는 방식으로 작동 합니다. 클래스에는 데이터를 검색 하 고 업데이트 하는 메서드가 포함 되어 있으며, 이러한 메서드의 이름을 태그의 `ObjectDataSource` 컨트롤에 제공 합니다. 렌더링 또는 포스트백을 처리 하는 동안 `ObjectDataSource`는 사용자가 지정한 메서드를 호출 합니다.

기본 CRUD 작업 외에도 `ObjectDataSource` 컨트롤과 함께 사용 하기 위해 만든 클래스는 `ObjectDataSource` 데이터를 읽거나 업데이트할 때 비즈니스 논리를 실행 해야 할 수 있습니다. 예를 들어 부서를 업데이트할 때 한 명의 사용자가 둘 이상의 부서의 관리자가 될 수 없으므로 다른 부서가 동일한 관리자를 갖고 있지 않은지 유효성을 검사 해야 할 수 있습니다.

[ObjectDataSource 클래스 개요](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx)와 같은 일부 `ObjectDataSource` 설명서에서 컨트롤은 비즈니스 논리 및 데이터 액세스 논리를 모두 포함 하는 *비즈니스 개체로* 참조 되는 클래스를 호출 합니다. 이 자습서에서는 비즈니스 논리 및 데이터 액세스 논리를 위한 별도의 클래스를 만듭니다. 데이터 액세스 논리를 캡슐화 하는 클래스를 *리포지토리*라고 합니다. 비즈니스 논리 클래스는 비즈니스 논리 메서드와 데이터 액세스 메서드를 모두 포함 하지만 데이터 액세스 메서드는 리포지토리를 호출 하 여 데이터 액세스 작업을 수행 합니다.

또한 bll의 자동화 된 단위 테스트를 용이 하 게 하는 BLL 및 DAL 간에 추상화 계층을 만듭니다. 이 추상화 계층은 비즈니스 논리 클래스에서 리포지토리를 인스턴스화할 때 인터페이스를 만들고 인터페이스를 사용 하 여 구현 됩니다. 이를 통해 리포지토리 인터페이스를 구현 하는 모든 개체에 대 한 참조를 비즈니스 논리 클래스에 제공할 수 있습니다. 일반 작업의 경우 Entity Framework와 작동 하는 리포지토리 개체를 제공 합니다. 테스트를 위해 컬렉션으로 정의 된 클래스 변수와 같이 쉽게 조작할 수 있는 방식으로 저장 된 데이터와 함께 작동 하는 리포지토리 개체를 제공 합니다.

다음 그림에서는 리포지토리를 사용 하지 않는 데이터 액세스 논리와 리포지토리를 사용 하는 논리를 포함 하는 비즈니스 논리 클래스 간의 차이점을 보여 줍니다.

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

기본 데이터 액세스 작업만 수행 하므로 `ObjectDataSource` 컨트롤이 리포지토리에 직접 바인딩된 웹 페이지를 만드는 것부터 시작 합니다. 다음 자습서에서는 유효성 검사 논리를 사용 하 여 비즈니스 논리 클래스를 만들고 리포지토리 클래스가 아닌 해당 클래스에 `ObjectDataSource` 컨트롤을 바인딩합니다. 또한 유효성 검사 논리에 대 한 단위 테스트를 만듭니다. 이 시리즈의 세 번째 자습서에서는 응용 프로그램에 정렬 및 필터링 기능을 추가 합니다.

이 자습서에서 만드는 페이지는 초보자를 위한 [자습서 시리즈](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)에서 만든 데이터 모델의 `Departments` 엔터티 집합을 사용 하 여 작동 합니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>데이터베이스 및 데이터 모델 업데이트

데이터베이스에 두 가지 변경 내용을 적용 하 여이 자습서를 시작 합니다 .이 두 가지 경우 모두 [Entity Framework 시작 및 Web Forms](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서에서 만든 데이터 모델에 대 한 해당 변경 내용이 필요 합니다. 이러한 자습서 중 하나에서 데이터베이스를 변경한 후 디자이너에서 수동으로 변경 하 여 데이터 모델을 데이터베이스와 동기화 했습니다. 이 자습서에서는 **데이터베이스에서 디자이너의 업데이트 모델** 도구를 사용 하 여 데이터 모델을 자동으로 업데이트 합니다.

### <a name="adding-a-relationship-to-the-database"></a>데이터베이스에 관계 추가

Visual Studio에서 [Entity Framework 시작 및 Web Forms](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 자습서 시리즈에서 만든 Contoso 대학 웹 응용 프로그램을 연 다음 `SchoolDiagram` 데이터베이스 다이어그램을 엽니다.

데이터베이스 다이어그램의 `Department` 테이블을 살펴보면 `Administrator` 열이 있음을 알 수 있습니다. 이 열은 `Person` 테이블에 대 한 외래 키 이지만 데이터베이스에 외래 키 관계가 정의 되어 있지 않습니다. Entity Framework에서이 관계를 자동으로 처리할 수 있도록 관계를 만들고 데이터 모델을 업데이트 해야 합니다.

데이터베이스 다이어그램에서 `Department` 테이블을 마우스 오른쪽 단추로 클릭 하 고 **관계**를 선택 합니다.

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

**외래 키 관계** 상자에서 **추가**를 클릭 한 다음 **테이블 및 열 사양**에 대 한 줄임표를 클릭 합니다.

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

**테이블 및 열** 대화 상자에서 기본 키 테이블과 필드를 `Person` 및 `PersonID`로 설정 하 고 외래 키 테이블 및 필드를 `Department` 및 `Administrator`로 설정 합니다. 이렇게 하면 관계 이름이 `FK_Department_Department`에서 `FK_Department_Person`로 변경 됩니다.

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

**테이블 및 열** 상자에서 **확인** 을 클릭 하 고 **외래 키 관계** 상자에서 **닫기** 를 클릭 한 다음 변경 내용을 저장 합니다. `Person` 및 `Department` 테이블을 저장 하 시겠습니까 묻는 메시지가 표시 되 면 **예**를 클릭 합니다.

> [!NOTE]
> 이미 `Administrator` 열에 있는 데이터에 해당 하는 `Person` 행을 삭제 한 경우에는이 변경 내용을 저장할 수 없습니다. 이 경우 **서버 탐색기** 의 테이블 편집기를 사용 하 여 모든 `Department` 행의 `Administrator` 값에 실제로 `Person` 테이블에 있는 레코드의 ID가 포함 되어 있는지 확인 합니다.
> 
> 변경 내용을 저장 한 후에는 해당 사용자가 부서 관리자 인 경우 `Person` 테이블에서 행을 삭제할 수 없습니다. 프로덕션 응용 프로그램에서는 데이터베이스 제약 조건으로 인해 삭제 되지 않거나 연계 된 삭제를 지정 하는 경우 특정 오류 메시지를 제공 합니다. 계단식 삭제를 지정 하는 방법에 대 한 예는 [Entity Framework 및 ASP.NET – 시작 파트 2](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md)를 참조 하세요.

### <a name="adding-a-view-to-the-database"></a>데이터베이스에 뷰 추가

만들려는 새 학과 *.aspx* 페이지에서 사용자가 부서 관리자를 선택할 수 있도록 "last, first" 형식의 이름을 사용 하 여 강사의 드롭다운 목록을 제공 하려고 합니다. 더 쉽게 수행할 수 있도록 데이터베이스에서 뷰를 만듭니다. 뷰는 드롭다운 목록에 필요한 데이터 (올바른 형식의 전체 이름) 및 레코드 키로만 구성 됩니다.

**서버 탐색기**에서 *School*을 확장 하 고 **Views** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **새 뷰 추가**를 선택 합니다.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

**테이블 추가** 대화 상자가 나타나면 **닫기** 를 클릭 하 고 SQL 창에 다음 sql 문을 붙여넣습니다.

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

`vInstructorName`으로 보기를 저장 합니다.

### <a name="updating-the-data-model"></a>데이터 모델 업데이트

*DAL* 폴더에서 *SchoolModel* 파일을 열고 디자인 화면을 마우스 오른쪽 단추로 클릭 한 다음 **데이터베이스에서 모델 업데이트**를 선택 합니다.

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

**데이터베이스 개체 선택** 대화 상자에서 **추가** 탭을 선택 하 고 방금 만든 보기를 선택 합니다.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

**Finish**를 클릭합니다.

디자이너에서 도구가 `vInstructorName` 엔터티를 만들고 `Department`와 `Person` 엔터티 사이에 새 연결을 만든 것을 볼 수 있습니다.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> **출력** 및 **오류 목록** 창에서 도구가 새 `vInstructorName` 뷰에 대 한 기본 키를 자동으로 만들었음을 알리는 경고 메시지가 표시 될 수 있습니다. 이는 정상적인 동작입니다.

코드에서 새 `vInstructorName` 엔터티를 참조 하는 경우에는 소문자 "v"를 접두사로 사용 하는 데이터베이스 규칙을 사용 하지 않으려고 합니다. 따라서 모델에서 엔터티 및 엔터티 집합의 이름을 바꿉니다.

**모델 브라우저**를 엽니다. 엔터티 형식 및 뷰로 나열 `vInstructorName` 표시 됩니다.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

**SchoolModel** ( **SchoolModel**)에서 **vInstructorName** 을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다. **속성** 창에서 **이름** 속성을 "InstructorName"로 변경 하 고 **엔터티 집합 이름** 속성을 "InstructorNames"로 변경 합니다.

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

데이터 모델을 저장 하 고 닫은 다음 프로젝트를 다시 빌드합니다.

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>리포지토리 클래스 및 ObjectDataSource 컨트롤 사용

*DAL* 폴더에 새 클래스 파일을 만들고 이름을 *SchoolRepository.cs*로 바꾸고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

이 코드는 `Departments` 엔터티 집합의 모든 엔터티를 반환 하는 단일 `GetDepartments` 메서드를 제공 합니다. 반환 된 모든 행에 대해 `Person` 탐색 속성에 액세스 한다는 것을 알고 있으므로 `Include` 메서드를 사용 하 여 해당 속성에 대 한 즉시 로드를 지정 합니다. 또한 클래스는 개체가 삭제 될 때 데이터베이스 연결이 해제 되도록 `IDisposable` 인터페이스를 구현 합니다.

> [!NOTE]
> 일반적인 방법은 각 엔터티 형식에 대 한 리포지토리 클래스를 만드는 것입니다. 이 자습서에서는 여러 엔터티 형식에 대 한 리포지토리 클래스 하나를 사용 합니다. 리포지토리 패턴에 대 한 자세한 내용은 [Entity Framework 팀의 블로그](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) 및 [Julie Lerman의 블로그](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/)에서 게시물을 참조 하세요.

`GetDepartments` 메서드는 리포지토리 개체 자체가 삭제 된 후에도 반환 된 컬렉션을 사용할 수 있도록 하기 위해 `IQueryable` 개체가 아닌 `IEnumerable` 개체를 반환 합니다. `IQueryable` 개체는 액세스할 때마다 데이터베이스에 액세스할 수 있지만, 데이터 바인딩된 컨트롤이 데이터를 렌더링 하려고 시도 하는 시간에 의해 리포지토리 개체가 삭제 될 수 있습니다. `IEnumerable` 개체 대신 `IList` 개체와 같은 다른 컬렉션 형식을 반환할 수 있습니다. 그러나 `IEnumerable` 개체를 반환 하면 `foreach` 루프 및 LINQ 쿼리와 같은 일반적인 읽기 전용 목록 처리 작업을 수행할 수 있지만 컬렉션에서 항목을 추가 하거나 제거할 수 없습니다 .이 경우 이러한 변경 내용이 데이터베이스에 유지 됨을 의미할 수 있습니다.

*Site.master* 마스터 페이지를 사용 하는 학과 *.aspx* 페이지를 만들고 `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

이 태그는 방금 만든 리포지토리 클래스를 사용 하는 `ObjectDataSource` 컨트롤과 데이터를 표시 하는 `GridView` 컨트롤을 만듭니다. `GridView` 컨트롤은 **편집** 및 **삭제** 명령을 지정 하지만 아직 지 원하는 코드를 추가 하지 않았습니다.

자동 데이터 서식 지정 및 유효성 검사 기능을 활용할 수 있도록 여러 열 `DynamicField` 컨트롤을 사용 합니다. 이러한 작업을 수행 하려면 `Page_Init` 이벤트 처리기에서 `EnableDynamicData` 메서드를 호출 해야 합니다. `DynamicControl` 컨트롤은 탐색 속성에서 작동 하지 않으므로 `Administrator` 필드에서 사용 되지 않습니다.

`Vertical-Align="Top"` 특성은 나중에 중첩 된 `GridView` 컨트롤을 포함 하는 열을 표에 추가할 때 중요 하 게 됩니다.

*Departments.aspx.cs* 파일을 열고 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

그런 다음 페이지의 `Init` 이벤트에 대 한 다음 처리기를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

*DAL* 폴더에서 *Department.cs* 라는 새 클래스 파일을 만들고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

이 코드는 데이터 모델에 메타 데이터를 추가 합니다. 이 메서드는 데이터 형식이 `Decimal`되더라도 `Department` 엔터티의 `Budget` 속성이 실제로 통화를 나타내도록 지정 하 고 값이 0에서 $1000000.00 사이 여야 함을 지정 합니다. 또한 `StartDate` 속성을 mm/dd/yyyy 형식의 날짜로 지정 하도록 지정 합니다.

*부서 .aspx* 페이지를 실행 합니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

**예산** 또는 **시작 날짜** 열에 대해 *학과 페이지 태그* 에 서식 문자열을 지정 하지 않았지만 *Department.cs* 파일에 제공 된 메타 데이터를 사용 하 여 `DynamicField` 컨트롤에 의해 기본 통화 및 날짜 형식이 적용 됩니다.

## <a name="adding-insert-and-delete-functionality"></a>삽입 및 삭제 기능 추가

*SchoolRepository.cs*을 열고 `Insert` 메서드와 `Delete` 메서드를 만들기 위해 다음 코드를 추가 합니다. 또한이 코드에는 `Insert` 메서드에서 사용할 사용 가능한 다음 레코드 키 값을 계산 하는 `GenerateDepartmentID` 라는 메서드가 포함 되어 있습니다. 이는 데이터베이스가 `Department` 테이블에 대해 자동으로 계산 되도록 구성 되지 않았기 때문에 필요 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Attach 메서드

`DeleteDepartment` 메서드는 `Attach` 메서드를 호출 하 여 개체 컨텍스트의 개체 상태 관리자에서 메모리의 엔터티와 해당 엔터티가 나타내는 데이터베이스 행 사이에 유지 관리 되는 링크를 다시 설정 합니다. 이는 메서드가 `SaveChanges` 메서드를 호출 하기 전에 발생 해야 합니다.

용어 *개체 컨텍스트* 는 엔터티 집합 및 엔터티에 액세스 하는 데 사용 하는 `ObjectContext` 클래스에서 파생 되는 Entity Framework 클래스를 나타냅니다. 이 프로젝트에 대 한 코드에서 클래스는 `SchoolEntities`이름이 지정 되 고 인스턴스는 항상 `context`이름이 지정 됩니다. 개체 컨텍스트의 *개체 상태 관리자* 는 `ObjectStateManager` 클래스에서 파생 되는 클래스입니다. 개체 연락처는 개체 상태 관리자를 사용 하 여 엔터티 개체를 저장 하 고 각 항목이 데이터베이스의 해당 테이블 행과 동기화 되어 있는지 여부를 추적 합니다.

엔터티를 읽으면 개체 컨텍스트는 개체 상태 관리자에이를 저장 하 고 개체의 표현이 데이터베이스와 동기화 되어 있는지 여부를 추적 합니다. 예를 들어 속성 값을 변경 하는 경우 변경 된 속성이 더 이상 데이터베이스와 동기화 되지 않음을 나타내는 플래그가 설정 됩니다. 그런 다음 `SaveChanges` 메서드를 호출 하면 개체 상태 관리자가 엔터티의 현재 상태와 데이터베이스 상태 간의 차이점을 정확히 알 수 있으므로 개체 컨텍스트는 데이터베이스에서 수행할 작업을 알고 있습니다.

그러나이 프로세스는 일반적으로 웹 응용 프로그램에서 작동 하지 않습니다. 개체 상태 관리자의 모든 항목을 비롯 하 여 엔터티를 읽는 개체 컨텍스트 인스턴스는 페이지가 렌더링 된 후 삭제 되기 때문입니다. 변경 내용을 적용 해야 하는 개체 컨텍스트 인스턴스는 다시 게시 처리를 위해 인스턴스화된 새 개체입니다. `DeleteDepartment` 메서드의 경우 `ObjectDataSource` 컨트롤은 뷰 상태의 값에서 엔터티의 원래 버전을 다시 만들지만,이 다시 생성 된 `Department` 엔터티는 개체 상태 관리자에 존재 하지 않습니다. 이 다시 만든 엔터티에 대해 `DeleteObject` 메서드를 호출한 경우 개체가 데이터베이스와 동기화 되어 있는지 여부를 개체 컨텍스트에서 알 수 없기 때문에 호출이 실패 합니다. 그러나 `Attach` 메서드를 호출 하면 다시 생성 된 엔터티와 데이터베이스의 값이 동일한 추적을 다시 설정 하 게 됩니다 .이는 원래 개체 컨텍스트의 이전 인스턴스에서 엔터티를 읽을 때 원래 자동으로 수행 된 데이터베이스의 값과 동일 합니다.

개체 상태 관리자에서 엔터티를 추적 하지 않으려는 경우에는이 작업을 수행 하지 못하도록 플래그를 설정할 수 있습니다. 이에 대 한 예제는이 시리즈의 이후 자습서에 나와 있습니다.

### <a name="the-savechanges-method"></a>SaveChanges 메서드

이 간단한 리포지토리 클래스는 CRUD 작업을 수행 하는 방법에 대 한 기본 원칙을 보여 줍니다. 이 예제에서는 각 업데이트 직후에 `SaveChanges` 메서드가 호출 됩니다. 프로덕션 응용 프로그램에서는 데이터베이스가 업데이트 되는 시기를 보다 세밀 하 게 제어할 수 있도록 별도의 메서드에서 `SaveChanges` 메서드를 호출 하는 것이 좋습니다. 다음 자습서의 끝 부분에서는 관련 업데이트를 조정 하는 한 가지 방법인 작업 단위 패턴을 설명 하는 백서 링크를 찾을 수 있습니다. 또한이 예제에서는 `DeleteDepartment` 메서드에 동시성 충돌을 처리 하는 코드가 포함 되어 있지 않습니다. 이 작업을 수행 하는 코드는이 시리즈의 이후 자습서에서 추가 될 예정입니다.

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>삽입할 때 선택할 강사 이름 검색

사용자는 새 부서를 만들 때 드롭다운 목록에서 강사 목록에서 관리자를 선택할 수 있어야 합니다. 따라서 *SchoolRepository.cs* 에 다음 코드를 추가 하 여 이전에 만든 뷰를 사용 하 여 강사 목록을 검색 하는 메서드를 만듭니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>부서 삽입에 대 한 페이지 만들기

*DepartmentsAdd* 페이지를 사용 하 여 `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 *합니다.*

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

이 태그는 두 개의 `ObjectDataSource` 컨트롤을 만듭니다. 하나는 새 `Department` 엔터티를 삽입 하 고 다른 하나는 부서 관리자를 선택 하는 데 사용 되는 `DropDownList` 컨트롤의 강사 이름을 검색 하기 위한 것입니다. 태그는 새 부서를 시작 하기 위한 `DetailsView` 컨트롤을 만들고, `Administrator` 외래 키 값을 설정할 수 있도록 컨트롤의 `ItemInserting` 이벤트에 대 한 처리기를 지정 합니다. 끝에는 오류 메시지를 표시 하는 `ValidationSummary` 컨트롤이 있습니다.

*DepartmentsAdd.aspx.cs* 를 열고 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

다음 클래스 변수 및 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

`Page_Init` 메서드 Dynamic Data 기능을 사용 하도록 설정 합니다. `DropDownList` 컨트롤의 `Init` 이벤트에 대 한 처리기는 컨트롤에 대 한 참조를 저장 하 고 `DetailsView` 컨트롤의 `Inserting` 이벤트에 대 한 처리기는 해당 참조를 사용 하 여 선택한 강사의 `PersonID` 값을 가져오고 `Administrator` 엔터티의 `Department` 외래 키 속성을 업데이트 합니다.

페이지를 실행 하 고 새 부서에 대 한 정보를 추가한 다음 **삽입** 링크를 클릭 합니다.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

다른 새로운 부서에 대 한 값을 입력 합니다. **예산** 필드에서 1000000.00 보다 큰 숫자를 입력 하 고 다음 필드로 탭 합니다. 필드에 별표가 표시 되 면 해당 필드 위에 마우스 포인터를 놓으면 해당 필드에 대 한 메타 데이터에 입력 한 오류 메시지를 볼 수 있습니다.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

**삽입**을 클릭 하면 페이지 맨 아래에 `ValidationSummary` 컨트롤이 표시 하는 오류 메시지가 표시 됩니다.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

그런 다음 브라우저를 닫고 학과 *.aspx* 페이지를 엽니다. `ObjectDataSource` 컨트롤에 `DeleteMethod` 특성을 추가 하 고 `GridView` 컨트롤에 `DataKeyNames` 특성을 추가 하 여 *부서 .aspx* 페이지에 삭제 기능을 추가 합니다. 이러한 컨트롤의 여는 태그는 이제 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

페이지를 실행 합니다.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

*DepartmentsAdd* 페이지를 실행할 때 추가한 부서를 삭제 합니다.

## <a name="adding-update-functionality"></a>업데이트 기능 추가

*SchoolRepository.cs* 를 열고 다음 `Update` 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

학과 페이지에서 **업데이트** 를 클릭 하면 `ObjectDataSource` 컨트롤이 `UpdateDepartment` 메서드에 전달할 `Department` 엔터티 두 개를 *만듭니다.* 하나는 뷰 상태에 저장 된 원래 값을 포함 하 고 다른 하나는 `GridView` 컨트롤에 입력 된 새 값을 포함 합니다. `UpdateDepartment` 메서드의 코드는 엔터티와 데이터베이스에 있는 항목 간의 추적을 설정 하기 위해 원래 값이 있는 `Department` 엔터티를 `Attach` 메서드로 전달 합니다. 그런 다음 코드는 `ApplyCurrentValues` 메서드에 새 값이 있는 `Department` 엔터티를 전달 합니다. 개체 컨텍스트는 이전 값과 새 값을 비교 합니다. 새 값이 이전 값과 다르면 개체 컨텍스트는 속성 값을 변경 합니다. 그런 다음 `SaveChanges` 메서드는 데이터베이스에서 변경 된 열만 업데이트 합니다. 그러나이 엔터티의 업데이트 함수를 저장 프로시저에 매핑한 경우 변경 된 열에 관계 없이 전체 행이 업데이트 됩니다.

학과 *.aspx* 파일을 열고 다음 특성을 `DepartmentsObjectDataSource` 컨트롤에 추가 합니다.

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 이렇게 하면 `Update` 메서드의 새 값과 비교할 수 있도록 이전 값이 뷰 상태에 저장 됩니다.
- `OldValuesParameterFormatString="orig{0}"`   
 이는 원래 값 매개 변수의 이름이 `origDepartment` 되었음을 컨트롤에 알립니다.

이제 `ObjectDataSource` 컨트롤의 여는 태그에 대 한 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

`GridView` 컨트롤에 `OnRowUpdating="DepartmentsGridView_RowUpdating"` 특성을 추가 합니다. 드롭다운 목록에서 사용자가 선택 하는 행을 기반으로 `Administrator` 속성 값을 설정 하는 데 사용 합니다. 이제 `GridView` 여는 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

`Administrator` 열의 `EditItemTemplate` 컨트롤을 해당 열에 대 한 `ItemTemplate` 컨트롤 바로 다음에 `GridView` 컨트롤에 추가 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

이 `EditItemTemplate` 컨트롤은 *DepartmentsAdd* 페이지의 `InsertItemTemplate` 컨트롤과 비슷합니다. 차이점은 컨트롤의 초기 값이 `SelectedValue` 특성을 사용 하 여 설정 된다는 것입니다.

`GridView` 컨트롤 전에 *DepartmentsAdd* 페이지에서 했던 것 처럼 `ValidationSummary` 컨트롤을 추가 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

*Departments.aspx.cs* 를 열고 partial 클래스 선언 바로 뒤에 다음 코드를 추가 하 여 `DropDownList` 컨트롤을 참조 하는 전용 필드를 만듭니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

그런 다음 `DropDownList` 컨트롤의 `Init` 이벤트와 `GridView` 컨트롤의 `RowUpdating` 이벤트에 대 한 처리기를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

`Init` 이벤트에 대 한 처리기는 클래스 필드에 `DropDownList` 컨트롤에 대 한 참조를 저장 합니다. `RowUpdating` 이벤트에 대 한 처리기는 참조를 사용 하 여 사용자가 입력 한 값을 가져오고이를 `Department` 엔터티의 `Administrator` 속성에 적용 합니다.

*DepartmentsAdd* 페이지를 사용 하 여 새 부서를 추가 하 고, *.aspx* 페이지를 실행 하 고, 추가한 행에서 **편집** 을 클릭 합니다.

> [!NOTE]
> 데이터베이스에 잘못 된 데이터가 있으므로 추가 하지 않은 행 (데이터베이스에 이미 있었던)은 편집할 수 없습니다. 데이터베이스를 사용 하 여 만든 행의 관리자는 학생입니다. 이러한 항목 중 하나를 편집 하려고 하면 다음과 같은 오류를 보고 하는 오류 페이지가 표시 됩니다 `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.`

[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

잘못 된 **예산** 수량을 입력 한 다음 **업데이트**를 클릭 하면 *.aspx* 페이지에서 본 것과 동일한 별표 및 오류 메시지가 표시 됩니다.

필드 값을 변경 하거나 다른 관리자를 선택 하 고 **업데이트**를 클릭 합니다. 변경 내용이 표시 됩니다.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

이렇게 하면 Entity Framework를 사용 하 여 기본 CRUD (만들기, 읽기, 업데이트, 삭제) 작업에 대 한 `ObjectDataSource` 컨트롤 사용에 대 한 소개를 완료 합니다. 간단한 n 계층 응용 프로그램을 빌드 했지만 비즈니스 논리 계층은 계속 해 서 데이터 액세스 계층과 긴밀 하 게 결합 되어 자동화 된 단위 테스트를 복잡 하 게 만듭니다. 다음 자습서에서는 유닛 테스트를 용이 하 게 하는 리포지토리 패턴을 구현 하는 방법을 알아봅니다.

> [!div class="step-by-step"]
> [다음](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
