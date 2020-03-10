---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: Entity Framework 4.0의 새로운 기능 | Microsoft Docs
author: tdykstra
description: 이 자습서 시리즈는 Entity Framework 4.0 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 29d2bd61e8361b130e7b9415dad4fe1d5b847945
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78522149"
---
# <a name="whats-new-in-the-entity-framework-40"></a>Entity Framework 4.0의 새로운 기능

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈는 Entity Framework 자습서 시리즈 [시작](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) 에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서의 시작 점으로, 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 수 있습니다. 전체 자습서 시리즈에서 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 수도 있습니다. 자습서에 대 한 질문이 있는 경우 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)에 게시할 수 있습니다.

이전 자습서에서는 Entity Framework를 사용 하는 웹 응용 프로그램의 성능을 최대화 하기 위한 몇 가지 방법을 살펴보았습니다. 이 자습서에서는 Entity Framework 버전 4에서 가장 중요 한 몇 가지 새로운 기능을 검토 하 고 모든 새 기능에 대 한 전체 소개를 제공 하는 리소스에 연결 합니다. 이 자습서에 강조 표시 된 기능은 다음과 같습니다.

- 외래 키 연결입니다.
- 사용자 정의 SQL 명령 실행
- 모델 우선 개발
- POCO 지원.

또한 자습서에는 Entity Framework의 다음 릴리스에 제공 되는 기능인 *코드 우선 개발*이 간략하게 도입 되었습니다.

자습서를 시작 하려면 Visual Studio를 시작 하 고 이전 자습서에서 작업 하 던 Contoso 대학 웹 응용 프로그램을 엽니다.

## <a name="foreign-key-associations"></a>외래 키 연결

Entity Framework 버전 3.5에는 탐색 속성이 포함 되어 있지만 데이터 모델에 외래 키 속성이 포함 되어 있지 않습니다. 예를 들어 `StudentGrade` 테이블의 `CourseID` 및 `StudentID` 열은 `StudentGrade` 엔터티에서 생략 됩니다.

[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

이 접근 방식의 이유는 엄격 하 게 말하면 외래 키가 물리적 구현 세부 정보 이며 개념적 데이터 모델에 속하지 않기 때문입니다. 그러나 실질적으로 외래 키에 직접 액세스 하는 경우 코드에서 엔터티를 사용 하는 것이 더 쉬울 수 있습니다.

데이터 모델의 외래 키가 코드를 간소화 하는 방법에 대 한 예제는 *DepartmentsAdd* 페이지를 사용 하지 않고 코딩 해야 하는 방법을 고려 합니다. `Department` 엔터티에서 `Administrator` 속성은 `Person` 엔터티의 `PersonID`에 해당 하는 외래 키입니다. 새 학과와 해당 관리자의 연결을 설정 하기 위해 데이터 바인딩된 컨트롤의 `ItemInserting` 이벤트 처리기에서 `Administrator` 속성의 값을 설정 해야 했습니다.

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

데이터 모델에 외래 키가 없으면 엔터티가 엔터티 집합에 추가 되기 전에 엔터티 자체에 대 한 참조를 가져오기 위해 데이터 바인딩된 컨트롤의 `ItemInserting` 이벤트 대신 데이터 소스 컨트롤의 `Inserting` 이벤트를 처리 합니다. 해당 참조를 사용 하는 경우 다음 예제에서와 같은 코드를 사용 하 여 연결을 설정 합니다.

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

[외래 키 연결에 대](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx)한 Entity Framework 팀의 블로그 게시물에서 볼 수 있듯이 코드 복잡성의 차이가 훨씬 더 큰 경우도 있습니다. 더 간단한 코드를 위해 개념적 데이터 모델에서 구현 세부 사항을 선호 하는 요구 사항을 충족 하기 위해 Entity Framework는 이제 데이터 모델에 외래 키를 포함 하는 옵션을 제공 합니다.

Entity Framework 용어에서 데이터 모델에 외래 키를 포함 하는 경우 외래 *키 연결*을 사용 하 고 외래 키를 제외 하는 경우 *독립 연결*을 사용 합니다.

## <a name="executing-user-defined-sql-commands"></a>사용자 정의 SQL 명령 실행

이전 버전의 Entity Framework에서는 사용자 고유의 SQL 명령을 즉석에서 만들고 실행할 수 있는 쉬운 방법이 없었습니다. Entity Framework 동적으로 생성 된 SQL 명령 또는 저장 프로시저를 만들고 함수로 가져와야 했습니다. 버전 4에서는 쿼리를 데이터베이스에 직접 전달할 수 있도록 하는 `ObjectContext` 클래스에 `ExecuteStoreQuery` 및 `ExecuteStoreCommand` 메서드를 추가 합니다.

Contoso 대학 관리자는 저장 프로시저를 만들고 데이터 모델로 가져오는 과정을 거치지 않고도 데이터베이스에서 대량 변경을 수행할 수 있다고 가정 합니다. 첫 번째 요청은 데이터베이스의 모든 과정에 대 한 크레딧 수를 변경할 수 있는 페이지에 대 한 것입니다. 웹 페이지에서 모든 `Course` 행의 `Credits` 열 값을 곱하는 데 사용할 숫자를 입력할 수 있습니다.

*Site.master* 마스터 페이지를 사용 하 고 이름을 *UpdateCredits*로 하는 새 페이지를 만듭니다. 그런 다음 `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

이 태그는 사용자가 승수 값을 입력할 수 있는 `TextBox` 컨트롤, 명령을 실행 하기 위해 클릭할 `Button` 컨트롤, 영향을 받는 행 수를 나타내는 `Label` 컨트롤을 만듭니다.

*UpdateCredits.aspx.cs*를 열고 다음 `using` 문과 단추의 `Click` 이벤트에 대 한 처리기를 추가 합니다.

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

이 코드는 텍스트 상자의 값을 사용 하 여 SQL `Update` 명령을 실행 하 고 레이블을 사용 하 여 영향을 받는 행 수를 표시 합니다. 페이지를 실행 하기 전에 *과정 .aspx* 페이지를 실행 하 여 일부 데이터의 "이전" 그림을 가져옵니다.

[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

*UpdateCredits*를 실행 하 고 승수로 "10"을 입력 한 다음 **실행**을 클릭 합니다.

[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

*Default.aspx* 페이지를 다시 실행 하 여 변경 된 데이터를 확인 합니다.

[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

크레딧 수를 원래 값으로 다시 설정 하려면 *UpdateCredits.aspx.cs* 를 `Credits / {0}` `Credits * {0}` 변경 하 고 페이지를 다시 실행 하 고 10을 제수로 입력 합니다.

코드에서 정의한 쿼리를 실행 하는 방법에 대 한 자세한 내용은 [방법: 데이터 소스에 대해 직접 명령 실행](https://msdn.microsoft.com/library/ee358769.aspx)을 참조 하세요.

## <a name="model-first-development"></a>모델 우선 개발

이 연습에서는 먼저 데이터베이스를 만든 다음 데이터베이스 구조를 기반으로 데이터 모델을 생성 했습니다. Entity Framework 4에서는 데이터 모델을 대신 사용 하 여 데이터 모델 구조를 기반으로 데이터베이스를 생성할 수 있습니다. 데이터베이스가 아직 없는 응용 프로그램을 만드는 경우 모델 우선 방법을 사용 하면 개념적으로 응용 프로그램에 적합 한 엔터티 및 관계를 만들 수 있습니다. . 그러나이는 개발의 초기 단계에 대해서만 적용 됩니다. 결국 데이터베이스가 만들어지고 프로덕션 데이터를 포함 하며 모델에서 다시 만드는 것은 더 이상 실용적이 지 않습니다. 이 시점에서 데이터베이스 우선 방식으로 돌아갑니다.

자습서의이 섹션에서는 간단한 데이터 모델을 만들고이 모델에서 데이터베이스를 생성 합니다.

**솔루션 탐색기**에서 *DAL* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **새 항목 추가**를 선택 합니다. **새 항목 추가** 대화 상자의 **설치 된 템플릿** 에서 **데이터** 를 선택한 다음 **ADO.NET 엔터티 데이터 모델** 템플릿을 선택 합니다. 새 파일의 이름을 *AlumniAssociationModel* 로 하 고 **추가**를 클릭 합니다.

[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

그러면 엔터티 데이터 모델 마법사가 시작 됩니다. **모델 콘텐츠 선택** 단계에서 **빈 모델** 을 선택 하 고 **마침**을 클릭 합니다.

[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

빈 디자인 화면을 사용 하 여 **엔터티 데이터 모델 디자이너가** 열립니다. **엔터티** 항목을 **도구 상자** 에서 디자인 화면으로 끌어 옵니다.

[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

엔터티 이름을 `Entity1`에서 `Alumnus`로 변경 하 고 `Id` 속성 이름을 `AlumnusId`로 변경 하 고 이름이 `Name`인 새 스칼라 속성을 추가 합니다. 새 속성을 추가 하려면 `Id` 열의 이름을 변경한 후 Enter 키를 누르거나, 엔터티를 마우스 오른쪽 단추로 클릭 하 고 **스칼라 속성 추가**를 선택 합니다. 새 속성의 기본 형식은이 간단한 데모용으로는 `String`이지만, 물론 **속성** 창에서 데이터 형식 같은 항목을 변경할 수 있습니다.

동일한 방식으로 다른 엔터티를 만들고 `Donation`이름을로 만듭니다. `Id` 속성을 `DonationId`로 변경 하 고 `DateAndAmount`라는 스칼라 속성을 추가 합니다.

[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

이러한 두 엔터티 간에 연결을 추가 하려면 `Alumnus` 엔터티를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **연결**을 선택 합니다.

[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

**연결 추가** 대화 상자의 기본값은 원하는 것 (일 대 다, 탐색 속성 포함, 외래 키 포함) 이므로 **확인**을 클릭 하면 됩니다.

[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

디자이너에서 연결 선 및 외래 키 속성을 추가 합니다.

[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

이제 데이터베이스를 만들 준비가 되었습니다. 디자인 화면을 마우스 오른쪽 단추로 클릭 하 고 **모델에서 데이터베이스 생성**을 선택 합니다.

[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

그러면 데이터베이스 생성 마법사가 시작 됩니다. 엔터티가 매핑되지 않았음을 나타내는 경고가 표시 되는 경우 해당 시간에 대 한 무시 해도 됩니다.

**데이터 연결 선택** 단계에서 **새 연결**을 클릭 합니다.

[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

**연결 속성** 대화 상자에서 로컬 SQL Server Express 인스턴스를 선택 하 고 데이터베이스 이름을 `AlumniAssociation`로 선택 합니다.

[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

데이터베이스를 만들 것인지 묻는 메시지가 표시 되 면 **예** 를 클릭 합니다. **데이터 연결 선택** 단계가 다시 표시 되 면 **다음**을 클릭 합니다.

**요약 및 설정** 단계에서 **마침**을 클릭 합니다.

[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

DDL (데이터 정의 언어) 명령이 있는 *.sql* 파일이 만들어졌지만 명령이 아직 실행 되지 않았습니다.

[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

[시작 자습서 시리즈의 첫 번째 자습서](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)에 대 한 `School` 데이터베이스를 만들 때와 같이 스크립트를 실행 하 고 테이블을 만들기 위해 **SQL Server Management Studio** 와 같은 도구를 사용 합니다. (데이터베이스를 다운로드 하지 않은 경우)

이제 `School` 모델을 사용 하는 것과 같은 방법으로 웹 페이지에서 `AlumniAssociation` 데이터 모델을 사용할 수 있습니다. 이를 수행 하려면 테이블에 일부 데이터를 추가 하 고 데이터를 표시 하는 웹 페이지를 만듭니다.

**서버 탐색기**를 사용 하 여 `Alumnus` 및 `Donation` 테이블에 다음 행을 추가 합니다.

[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

*Site.master* 마스터 페이지를 사용 하는 *동문* 라는 새 웹 페이지를 만듭니다. `Content2`이라는 `Content` 컨트롤에 다음 태그를 추가 합니다.

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

이 태그는 중첩 된 `GridView` 컨트롤을 만들고, 외부 항목은 동문 이름을 표시 하 고 내부 날짜 및 금액을 표시 하는 내부를 표시 합니다.

*Alumni.aspx.cs*를 엽니다. 데이터 액세스 계층에 대 한 `using` 문과 외부 `GridView` 컨트롤의 `RowDataBound` 이벤트에 대 한 처리기를 추가 합니다.

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

이 코드는 현재 행의 `Alumnus` 엔터티의 `Donations` 탐색 속성을 사용 하 여 내부 `GridView` 컨트롤을 열의 합니다.

페이지를 실행 합니다.

[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

(참고:이 페이지는 다운로드 가능한 프로젝트에 포함 되어 있지만 작업을 수행 하려면 로컬 SQL Server Express 인스턴스에서 데이터베이스를 만들어야 합니다. 데이터베이스는 *응용 프로그램\_Data* 폴더에 *.mdf* 파일로 포함 되지 않습니다.)

Entity Framework의 모델 중심 기능 사용에 대 한 자세한 내용은 [Entity Framework 4의 모델 우선](https://msdn.microsoft.com/data/ff830362.aspx)기능을 참조 하세요.

## <a name="poco-support"></a>POCO 지원

도메인 기반 디자인 방법을 사용 하는 경우 비즈니스 도메인과 관련 된 데이터 및 동작을 나타내는 데이터 클래스를 디자인 합니다. 이러한 클래스는 데이터를 저장 (유지) 하는 데 사용 되는 특정 기술과 독립적 이어야 합니다. 즉, *지 속성을 무시*해야 합니다. 또한 단위 테스트 프로젝트는 테스트에 가장 편리한 지 속성 기술을 사용할 수 있기 때문에 지 속성 무시는 클래스를 단위 테스트에 더 쉽게 만들 수 있습니다. 이전 버전의 Entity Framework에서는 엔터티 클래스가 `EntityObject` 클래스에서 상속 해야 하므로 많은 Entity Framework 관련 기능이 포함 되어 있기 때문에 지 속성 무시에 대 한 지원이 제한적으로 제공 되었습니다.

Entity Framework 4에서는 `EntityObject` 클래스에서 상속 되지 않으므로 지 속성을 무시 하는 엔터티 클래스를 사용 하는 기능을 소개 합니다. Entity Framework 컨텍스트에서 이와 같은 클래스는 일반적으로 *일반-이전 CLR 개체* (POCO 또는 pocos) 라고 합니다. POCO 클래스를 수동으로 작성 하거나, Entity Framework에서 제공 하는 T4 (텍스트 템플릿 변환 도구 키트) 템플릿을 사용 하 여 기존 데이터 모델을 기반으로 자동으로 생성할 수 있습니다.

Entity Framework에서 POCOs를 사용 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [POCO 엔터티 작업](https://msdn.microsoft.com/library/dd456853.aspx) 이 문서에서는 POCOs에 대해 간략하게 설명 하 고 자세한 정보를 제공 하는 다른 문서에 대 한 링크를 제공 합니다.
- [연습: Entity Framework에 대 한 POCO 템플릿](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx) POCOs에 대 한 다른 블로그 게시물에 대 한 링크를 포함 하는 Entity Framework 개발 팀의 블로그 게시물입니다.

## <a name="code-first-development"></a>코드 우선 개발

Entity Framework 4의 POCO 지원에서는 여전히 데이터 모델을 만들고 엔터티 클래스를 데이터 모델에 연결 해야 합니다. Entity Framework의 다음 릴리스에는 *코드 우선 개발*이라는 기능이 포함 됩니다. 이 기능을 사용 하면 데이터 모델 디자이너나 데이터 모델 XML 파일을 사용 하지 않고도 사용자의 POCO 클래스에서 Entity Framework를 사용할 수 있습니다. 따라서이 옵션은 *코드 전용*이 라고도 합니다. *코드 우선* 및 *코드 전용* 은 모두 동일한 Entity Framework 기능을 참조 합니다.)

개발에 대 한 코드 우선 방법을 사용 하는 방법에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Entity Framework 4를 사용한 코드 우선 개발](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx) 이는 코드 우선 개발을 소개 하는 Scott Guthrie의 블로그 게시물입니다.
- [Entity Framework 개발 팀 블로그-태그가 지정 된 CodeOnly 게시](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [Entity Framework 개발 팀 블로그-태그가 지정 된 Code First 게시물](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [MVC Music Store 자습서-4 부: 모델 및 데이터 액세스](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [MVC 3 시작-4 부: 코드 우선 개발 Entity Framework](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

또한 Contoso 대학 응용 프로그램과 유사한 응용 프로그램을 빌드하는 새로운 MVC 코드 중심 자습서는 2011의 스프링에 게시 될 예정입니다 [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)

## <a name="more-information"></a>추가 정보

이렇게 하면 Entity Framework의 새로운 기능에 대 한 개요를 완료 하 고 Entity Framework 자습서 시리즈를 계속 진행 합니다. 여기에서 다루지 않는 Entity Framework 4의 새로운 기능에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ADO.NET의 새로운 기능](https://msdn.microsoft.com/library/ex6y04yf.aspx) Entity Framework 버전 4의 새로운 기능에 대 한 MSDN 항목입니다.
- [Entity Framework 4 릴리스 발표](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx) 버전 4의 새로운 기능에 대 한 Entity Framework 개발 팀의 블로그 게시물입니다.

> [!div class="step-by-step"]
> [이전](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)
