---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
title: Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms을 시작 합니다. Microsoft Docs
author: tdykstra
description: Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 5cb00916-8f46-491f-be25-4739a615d619
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
msc.type: authoredcontent
ms.openlocfilehash: fd88b32ad2a65e5b4c7ead15f0d6dc5dc6e97e75
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78511679"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms"></a>Entity Framework 4.0 Database First 및 ASP.NET 4 Web Forms 시작

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> Contoso 대학 샘플 웹 응용 프로그램은 Entity Framework 4.0 및 Visual Studio 2010를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 방법을 보여 줍니다. 샘플 응용 프로그램은 가상의 Contoso 대학 웹 사이트입니다. 학생 입학, 강좌 개설 및 강사 할당과 같은 기능이 있습니다.
> 
> 이 자습서에서는의 C#예제를 보여 줍니다. [다운로드 가능한 샘플](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 에는 및 Visual Basic C# 모두의 코드가 포함 되어 있습니다.
> 
> ## <a name="database-first"></a>Database First
> 
> Entity Framework에서 데이터를 사용할 수 있는 방법에는 *Database First*, *Model First*및 *Code First*의 세 가지가 있습니다. 이 자습서는 Database First에 대 한 것입니다. 이러한 워크플로의 차이점과 시나리오에 가장 적합 한 지침을 선택 하는 방법에 대 한 자세한 내용은 [Entity Framework 개발 워크플로](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)를 참조 하세요.
> 
> ## <a name="web-forms"></a>웹 양식
> 
> 이 자습서 시리즈에서는 ASP.NET Web Forms 모델을 사용 하며, Visual Studio에서 ASP.NET Web Forms를 사용 하는 방법을 알고 있다고 가정 합니다. 그렇지 않은 경우 [ASP.NET 4.5 Web Forms 시작](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md)을 참조 하세요. ASP.NET MVC 프레임 워크를 사용 하려는 경우 [ASP.NET mvc를 사용 하 여 Entity Framework 시작](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)을 참조 하세요.
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

## <a name="overview"></a>개요

이러한 자습서에서 빌드할 응용 프로그램은 간단한 대학 웹 사이트입니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image1.png)

사용자는 학생, 강좌 및 강사 정보를 보고 업데이트할 수 있습니다. 만든 화면 중 몇 가지는 다음과 같습니다.

[![Image30](the-entity-framework-and-aspnet-getting-started-part-1/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image3.png)

[![Image37](the-entity-framework-and-aspnet-getting-started-part-1/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image5.png)

[![Image31](the-entity-framework-and-aspnet-getting-started-part-1/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image7.png)

[![Image32](the-entity-framework-and-aspnet-getting-started-part-1/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image9.png)

## <a name="creating-the-web-application"></a>웹 응용 프로그램 만들기

자습서를 시작 하려면 Visual Studio를 열고 **ASP.NET 웹 응용 프로그램** 템플릿을 사용 하 여 새 ASP.NET 웹 응용 프로그램 프로젝트를 만듭니다.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-1/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image11.png)

이 템플릿은 이미 스타일 시트 및 마스터 페이지를 포함 하는 웹 응용 프로그램 프로젝트를 만듭니다.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-1/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image13.png)

*Site.master* 파일을 열고 "My ASP.NET Application"을 "Contoso 대학"으로 변경 합니다.

[!code-html[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample1.html)]

`NavigationMenu` 이라는 *메뉴* 컨트롤을 찾아 다음 태그로 바꿉니다 .이 태그는 만들 페이지에 대 한 메뉴 항목을 추가 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample2.aspx)]

*Default.aspx 페이지를* 열고 `BodyContent` 이라는 `Content` 컨트롤을 다음과 같이 변경 합니다.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample3.aspx)]

이제는 다음과 같은 다양 한 페이지에 대 한 링크가 포함 된 간단한 홈 페이지가 제공 됩니다.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image15.png)

## <a name="creating-the-database"></a>데이터베이스 만들기

이러한 자습서에서는 Entity Framework 데이터 모델 디자이너를 사용 하 여 기존 데이터베이스 ( *데이터베이스 우선* 방식 이라고 함)를 기반으로 데이터 모델을 자동으로 만듭니다. 이 자습서 시리즈에 포함 되지 않은 대안은 데이터 모델을 수동으로 만든 다음 디자이너에서 데이터베이스를 만드는 스크립트를 생성 하도록 하는 것입니다 ( *모델 우선* 방법).

이 자습서에서 사용 되는 데이터베이스 우선 방법의 경우 다음 단계는 사이트에 데이터베이스를 추가 하는 것입니다. 가장 쉬운 방법은이 자습서와 함께 이동 하는 프로젝트를 먼저 다운로드 하는 것입니다. 그런 다음, *앱\_데이터* 폴더를 마우스 오른쪽 단추로 클릭 하 고, **기존 항목 추가**를 선택 하 고, 다운로드 한 프로젝트에서 *학교 .mdf* 데이터베이스 파일을 선택 합니다.

또 다른 방법은 [School 샘플 데이터베이스 만들기](https://msdn.microsoft.com/library/bb399731.aspx)의 지침을 따르는 것입니다. 데이터베이스를 다운로드 하거나 만드는 경우에는 다음 폴더의 *School .mdf* 파일을 응용 프로그램의 *앱\_Data* 폴더로 복사 합니다.

`%PROGRAMFILES%\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA`

*.Mdf* 파일의이 위치는 SQL Server 2008 Express를 사용 하 고 있다고 가정 합니다.

스크립트에서 데이터베이스를 만드는 경우 다음 단계를 수행 하 여 데이터베이스 다이어그램을 만듭니다.

1. **서버 탐색기**에서 **데이터 연결**, *School*을 차례로 확장 하 고 **데이터베이스 다이어그램**을 마우스 오른쪽 단추로 클릭 한 다음 **새 다이어그램 추가**를 선택 합니다.

    [![Image35](the-entity-framework-and-aspnet-getting-started-part-1/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image17.png)
2. 모든 테이블을 선택 하 고 **추가**를 클릭 합니다.

    [![Image36](the-entity-framework-and-aspnet-getting-started-part-1/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image19.png)

    SQL Server 테이블, 테이블의 열 및 테이블 간의 관계를 보여 주는 데이터베이스 다이어그램을 만듭니다. 테이블을 이동 하 여 원하는 대로 구성할 수 있습니다.
3. 다이어그램을 "SchoolDiagram"로 저장 하 고 닫습니다.

이 자습서와 함께 이동 하는 *School .mdf* 파일을 다운로드 하는 경우 **서버 탐색기**의 **데이터베이스 다이어그램** 에서 **SchoolDiagram** 를 두 번 클릭 하 여 데이터베이스 다이어그램을 볼 수 있습니다.

[![Image38](the-entity-framework-and-aspnet-getting-started-part-1/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image21.png)

다이어그램은 다음과 같이 표시 됩니다 (테이블이 여기에 표시 된 것과 다른 위치에 있을 수 있음).

[![Image04](the-entity-framework-and-aspnet-getting-started-part-1/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image23.png)

## <a name="creating-the-entity-framework-data-model"></a>Entity Framework 데이터 모델 만들기

이제이 데이터베이스에서 Entity Framework 데이터 모델을 만들 수 있습니다. 응용 프로그램의 루트 폴더에 데이터 모델을 만들 수 있지만이 자습서에서는 데이터 액세스 계층의 경우 *DAL* 이라는 폴더에 저장 합니다.

**솔루션 탐색기**에서 *DAL* 이라는 프로젝트 폴더를 추가 합니다 (솔루션이 아니라 프로젝트 아래에 있는지 확인).

*DAL* 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가** 및 **새 항목**을 선택 합니다. **설치 된 템플릿**에서 **데이터**를 선택 하 고 **ADO.NET 엔터티 데이터 모델** 템플릿을 선택 하 고 이름을 *SchoolModel*로 지정한 다음 **추가**를 클릭 합니다.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-1/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image25.png)

그러면 엔터티 데이터 모델 마법사가 시작 됩니다. 첫 번째 마법사 단계에서 **데이터베이스에서 생성** 옵션이 기본적으로 선택 되어 있습니다. **다음**을 클릭합니다.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-1/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image27.png)

**데이터 연결 선택** 단계에서 기본값을 그대로 두고 **다음**을 클릭 합니다. School 데이터베이스는 기본적으로 선택 되 고 연결 설정은 *web.config* 파일에 **SchoolEntities**로 저장 됩니다.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-1/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image29.png)

**데이터베이스 개체 선택** 마법사 단계에서 `sysdiagrams` (이전에 생성 한 다이어그램에 대해 만들어짐)를 제외한 모든 테이블을 선택 하 고 **마침**을 클릭 합니다.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-1/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image31.png)

모델 만들기를 완료 한 후에는 Visual Studio에서 데이터베이스 테이블에 해당 하는 Entity Framework 개체 (엔터티)를 그래픽으로 표시 합니다. (데이터베이스 다이어그램과 마찬가지로 개별 요소의 위치는이 그림에 표시 된 것과 다를 수 있습니다. 원하는 경우 요소를 그림에 맞게 끌어 놓을 수 있습니다.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-1/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image33.png)

## <a name="exploring-the-entity-framework-data-model"></a>Entity Framework 데이터 모델 살펴보기

엔터티 다이어그램이 데이터베이스 다이어그램과 매우 비슷해 보이지만 몇 가지 차이점이 있습니다. 한 가지 차이점은 연결 유형을 나타내는 각 연결의 끝에 기호를 추가 하는 것입니다 (테이블 관계는 데이터 모델에서 엔터티 연결 이라고 함).

- 일 대 일 또는 일 대 일 연결은 "1" 및 "0 ..1"으로 표시 됩니다.

    [![Image39](the-entity-framework-and-aspnet-getting-started-part-1/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image35.png)

    이 경우 `Person` 엔터티는 `OfficeAssignment` 엔터티와 연결 될 수도 있고 그렇지 않을 수도 있습니다. `OfficeAssignment` 엔터티는 `Person` 엔터티와 연결 되어야 합니다. 즉, 강사는 사무실에 할당 될 수도 있고 그렇지 않을 수도 있으며, 모든 사무실은 하나의 강사 에게만 할당 될 수 있습니다.
- 일 대 다 연결은 "1" 및 "\*"로 표시 됩니다.

    [![Image40](the-entity-framework-and-aspnet-getting-started-part-1/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image37.png)

    이 경우 `Person` 엔터티에는 연결 된 `StudentGrade` 엔터티가 있을 수도 있고 없을 수도 있습니다. `StudentGrade` 엔터티는 하나의 `Person` 엔터티와 연결 되어야 합니다. `StudentGrade` 엔터티는 실제로이 데이터베이스의 등록 된 과정을 나타냅니다. 학생 들이 강좌에 등록 되어 있고 아직 등급이 없는 경우 `Grade` 속성은 null입니다. 즉, 학생은 아직 강좌에 등록 되지 않았거나 한 과정에서 등록 되거나 여러 과정에서 등록 될 수 있습니다. 등록 된 과정의 각 등급은 한 명의 학생 에게만 적용 됩니다.
- 다대다 연결은 "\*" 및 "\*"로 표시 됩니다.

    [![Image41](the-entity-framework-and-aspnet-getting-started-part-1/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image39.png)

    이 경우 `Person` 엔터티에는 연결 된 `Course` 엔터티가 있을 수도 있고 그렇지 않을 수도 있으며, 반대의 경우도 마찬가지입니다. `Course` 엔터티에서 `Person` 엔터티가 연결 될 수도 있고 그렇지 않을 수도 있습니다. 즉, 강사는 여러 과정을 학습할 수 있으며 강좌는 여러 강사가 배울 수 있습니다. (이 데이터베이스에서이 관계는 강사 에게만 적용 되며 학습자를 과정에 연결 하지 않습니다. 학생은 StudentGrades 테이블에 의해 강의에 연결 됩니다.

데이터베이스 다이어그램과 데이터 모델의 또 다른 차이점은 각 엔터티에 대 한 추가 **탐색 속성** 섹션입니다. 엔터티의 탐색 속성은 관련 엔터티를 참조 합니다. 예를 들어 `Person` 엔터티의 `Courses` 속성은 해당 `Person` 엔터티와 관련 된 모든 `Course` 엔터티의 컬렉션을 포함 합니다.

[![Image12](the-entity-framework-and-aspnet-getting-started-part-1/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image41.png)

그러나 데이터베이스와 데이터 모델의 또 다른 차이점은 데이터베이스에서 `Person`를 연결 하는 데 사용 되는 `CourseInstructor` 연결 테이블 및 다 대 다 관계의 테이블 `Course` 없다는 것입니다. 탐색 속성을 사용 하면 `Person` 엔터티 및 관련 `Person` 엔터티에서 관련 `Course` 엔터티를 `Course` 엔터티에서 가져올 수 있으므로 데이터 모델에 연결 테이블을 표시할 필요가 없습니다.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-1/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image43.png)

이 자습서의 목적을 위해 `Person` 테이블의 `FirstName` 열에 실제로 사람의 이름과 중간 이름이 모두 포함 되어 있다고 가정 합니다. 필드 이름을 변경 하 여이를 반영 하려고 하지만 DBA (데이터베이스 관리자)가 데이터베이스를 변경 하지 않으려고 할 수 있습니다. 데이터 모델에서 `FirstName` 속성의 이름을 변경할 수 있으며 데이터베이스는 변경 되지 않은 상태로 유지 됩니다.

디자이너에서 `Person` 엔터티의 **FirstName** 을 마우스 오른쪽 단추로 클릭 한 다음 **이름 바꾸기**를 선택 합니다.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-1/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image45.png)

"FirstMidName" 라는 새 이름을 입력 합니다. 이렇게 하면 데이터베이스를 변경 하지 않고 코드에서 열을 참조 하는 방식이 변경 됩니다.

[![Image29](the-entity-framework-and-aspnet-getting-started-part-1/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image47.png)

모델 브라우저는 데이터베이스 구조, 데이터 모델 구조 및 두 요소 간의 매핑을 볼 수 있는 또 다른 방법을 제공 합니다. 이를 보려면 entity designer에서 빈 영역을 마우스 오른쪽 단추로 클릭 한 다음 **모델 브라우저**를 클릭 합니다.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-1/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image49.png)

**모델 브라우저** 창에 트리 뷰가 표시 됩니다. **모델 브라우저** 창이 **솔루션 탐색기** 창에 도킹 될 수 있습니다. **SchoolModel** 노드는 데이터 모델 구조를 나타내고 **SchoolModel** 노드는 데이터베이스 구조를 나타냅니다.

[![Image26](the-entity-framework-and-aspnet-getting-started-part-1/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image51.png)

**SchoolModel** 를 확장 하 여 테이블을 표시 하 고 테이블 **/뷰** 를 확장 하 여 테이블을 표시 한 다음 **코스** 를 확장 하 여 테이블의 열을 표시 합니다.

[![Image19](the-entity-framework-and-aspnet-getting-started-part-1/_static/image54.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image53.png)

**SchoolModel**를 확장 하 고 **엔터티 형식**을 확장 한 다음 **과정** 노드를 확장 하 여 엔터티 및 엔터티 내의 속성을 확인 합니다.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-1/_static/image56.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image55.png)

디자이너나 **모델 브라우저** 창에서 Entity Framework 두 모델의 개체와 어떻게 관련 되어 있는지 확인할 수 있습니다. `Person` 엔터티를 마우스 오른쪽 단추로 클릭 하 고 **테이블 매핑**을 선택 합니다.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-1/_static/image58.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image57.png)

**매핑 정보** 창이 열립니다. 이 창을 사용 하 여 데이터베이스 열 `FirstName` 데이터 모델에서 이름을 변경한 `FirstMidName`에 매핑되는 것을 확인할 수 있습니다.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-1/_static/image60.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image59.png)

Entity Framework는 XML을 사용 하 여 데이터베이스, 데이터 모델 및 데이터베이스 간의 매핑에 대 한 정보를 저장 합니다. *SchoolModel* 파일은 실제로이 정보를 포함 하는 XML 파일입니다. 디자이너가 그래픽 형식으로 정보를 렌더링 하지만 **솔루션 탐색기**에서 *.edmx* 파일을 마우스 오른쪽 단추로 클릭 하 고 **연결 프로그램**을 클릭 한 다음 **xml (텍스트) 편집기**를 선택 하 여 파일을 XML로 볼 수도 있습니다. (데이터 모델 디자이너와 XML 편집기는 동일한 파일을 열고 작업 하는 두 가지 방법이 있습니다. 따라서 디자이너를 열고 XML 편집기에서 파일을 동시에 열 수 없습니다.)

이제 웹 사이트, 데이터베이스 및 데이터 모델을 만들었습니다. 다음 연습에서는 데이터 모델 및 ASP.NET `EntityDataSource` 컨트롤을 사용 하 여 데이터 작업을 시작 합니다.

> [!div class="step-by-step"]
> [다음](the-entity-framework-and-aspnet-getting-started-part-2.md)
