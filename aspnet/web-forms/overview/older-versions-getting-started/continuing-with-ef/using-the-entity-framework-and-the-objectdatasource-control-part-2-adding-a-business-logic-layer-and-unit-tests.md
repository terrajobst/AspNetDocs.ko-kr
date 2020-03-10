---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: 'Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용, 2 부: 비즈니스 논리 계층 및 단위 테스트 추가 | Microsoft Docs'
author: tdykstra
description: 이 자습서 시리즈는 Entity Framework 4.0 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 24344cc33d7c26d7c408db26c0530ef2c708a7d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78439955"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>Entity Framework 4.0 및 ObjectDataSource 컨트롤 사용, 2 부: 비즈니스 논리 계층 및 단위 테스트 추가

만든 사람 [Tom Dykstra](https://github.com/tdykstra)

> 이 자습서 시리즈는 [Entity Framework 4.0](https://asp.net/entity-framework/tutorials#Getting%20Started) 자습서 시리즈 시작에서 만든 Contoso 대학 웹 응용 프로그램을 기반으로 합니다. 이전 자습서를 완료 하지 않은 경우이 자습서의 시작 점으로, 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) 수 있습니다. 전체 자습서 시리즈에서 만든 [응용 프로그램을 다운로드할](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) 수도 있습니다. 자습서에 대 한 질문이 있는 경우 [ASP.NET Entity Framework 포럼](https://forums.asp.net/1227.aspx)에 게시할 수 있습니다.

이전 자습서에서는 Entity Framework 및 `ObjectDataSource` 컨트롤을 사용 하 여 n 계층 웹 응용 프로그램을 만들었습니다. 이 자습서에서는 BLL (비즈니스 논리 계층) 및 DAL (데이터 액세스 계층)을 별도로 유지 하면서 비즈니스 논리를 추가 하는 방법을 보여 주고 BLL에 대해 자동화 된 단위 테스트를 만드는 방법을 보여 줍니다.

이 자습서에서는 다음 작업을 완료 합니다.

- 필요한 데이터 액세스 메서드를 선언 하는 리포지토리 인터페이스를 만듭니다.
- 리포지토리 클래스에서 리포지토리 인터페이스를 구현 합니다.
- 리포지토리 클래스를 호출 하 여 데이터 액세스 함수를 수행 하는 비즈니스 논리 클래스를 만듭니다.
- `ObjectDataSource` 컨트롤을 리포지토리 클래스가 아닌 비즈니스 논리 클래스에 연결 합니다.
- 데이터 저장소에 대 한 메모리 내 컬렉션을 사용 하는 단위 테스트 프로젝트 및 리포지토리 클래스를 만듭니다.
- 비즈니스 논리 클래스에 추가 하려는 비즈니스 논리에 대 한 단위 테스트를 만든 다음 테스트를 실행 하 고 실패를 확인 합니다.
- 비즈니스 논리 클래스에서 비즈니스 논리를 구현 하 고 단위 테스트를 다시 실행 하 여 통과 하는지 확인 합니다.

이전 자습서에서 만든 *DepartmentsAdd 및 .aspx* *페이지를 사용* 합니다.

## <a name="creating-a-repository-interface"></a>리포지토리 인터페이스 만들기

먼저 리포지토리 인터페이스를 만들어야 합니다.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

*DAL* 폴더에서 새 클래스 파일을 만들고 이름을 *ISchoolRepository.cs*로 바꾸고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

인터페이스는 리포지토리 클래스에서 만든 CRUD (만들기, 읽기, 업데이트, 삭제) 메서드에 대해 하나의 메서드를 정의 합니다.

*SchoolRepository.cs*의 `SchoolRepository` 클래스에서이 클래스가 `ISchoolRepository` 인터페이스를 구현 함을 표시 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>비즈니스 논리 클래스 만들기

다음으로 비즈니스 논리 클래스를 만듭니다. 이렇게 하면 `ObjectDataSource` 컨트롤에 의해 실행 되는 비즈니스 논리를 추가할 수 있지만 아직 수행 하지는 않습니다. 현재, 새 비즈니스 논리 클래스는 리포지토리에서 수행 하는 것과 동일한 CRUD 작업을 수행 합니다.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

새 폴더를 만들고 이름을 *BLL*으로 만듭니다. 실제 응용 프로그램에서 비즈니스 논리 계층은 일반적으로 별도 프로젝트인 클래스 라이브러리로 구현 되지만이 자습서를 간단 하 게 유지 하기 위해 BLL 클래스는 프로젝트 폴더에 유지 됩니다.

*BLL* 폴더에서 새 클래스 파일을 만들고 이름을 *SchoolBL.cs*로 바꾸고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

이 코드는 이전에 리포지토리 클래스에서 살펴본 것과 동일한 CRUD 메서드를 만들지만 Entity Framework 메서드에 직접 액세스 하는 대신 리포지토리 클래스 메서드를 호출 합니다.

리포지토리 클래스에 대 한 참조를 포함 하는 클래스 변수는 인터페이스 형식으로 정의 되며 리포지토리 클래스를 인스턴스화하는 코드는 두 개의 생성자에 포함 됩니다. 매개 변수가 없는 생성자는 `ObjectDataSource` 컨트롤에서 사용 됩니다. 이전에 만든 `SchoolRepository` 클래스의 인스턴스를 만듭니다. 다른 생성자는 비즈니스 논리 클래스를 인스턴스화하는 모든 코드에서 리포지토리 인터페이스를 구현 하는 개체를 전달 하도록 허용 합니다.

리포지토리 클래스 및 두 생성자를 호출 하는 CRUD 메서드를 사용 하면 선택한 백 엔드 데이터 저장소에 비즈니스 논리 클래스를 사용할 수 있습니다. 비즈니스 논리 클래스는 호출 하는 클래스가 데이터를 유지 하는 방법을 인식할 필요가 없습니다. 이를 일반적으로 *지 속성 무시*합니다. 이렇게 하면 데이터를 저장 하기 위해 메모리 내 `List` 컬렉션과 같이 간단한 항목을 사용 하는 리포지토리 구현에 비즈니스 논리 클래스를 연결할 수 있으므로 단위 테스트를 용이 하 게 할 수 있습니다.

> [!NOTE]
> 기술적으로 엔터티 개체는 Entity Framework의 `EntityObject` 클래스에서 상속 되는 클래스에서 인스턴스화되기 때문에 여전히 지 속성을 무시 하지 않습니다. 완전 지 속성 무시을 위해 `EntityObject` 클래스에서 상속 되는 개체 대신 *일반 이전 CLR 개체*또는 *pocos*를 사용할 수 있습니다. POCOs를 사용 하는 것은이 자습서의 범위를 벗어나는 것입니다. 자세한 내용은 MSDN 웹 사이트의 [테스트 용이성 및 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx) 을 참조 하세요.

이제 리포지토리가 아닌 비즈니스 논리 클래스에 `ObjectDataSource` 컨트롤을 연결 하 고 모든 항목이 이전과 동일한 방식으로 작동 하는지 확인할 수 있습니다.

*DepartmentsAdd 및*에서 각각의 `TypeName="ContosoUniversity.DAL.SchoolRepository"` `TypeName="ContosoUniversity.BLL.SchoolBL`"로 변경 *합니다.* 모든에는 네 개의 인스턴스가 있습니다.

*DepartmentsAdd* 및 *.aspx 페이지를 실행* 하 여 이전과 동일한 작업을 수행 하는지 확인 합니다.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>단위 테스트 프로젝트 및 리포지토리 구현 만들기

**테스트 프로젝트** 템플릿을 사용 하 여 솔루션에 새 프로젝트를 추가 하 고 이름을 `ContosoUniversity.Tests`로 합니다.

테스트 프로젝트에서 `System.Data.Entity`에 대 한 참조를 추가 하 고 `ContosoUniversity` 프로젝트에 프로젝트 참조를 추가 합니다.

이제 단위 테스트에 사용할 리포지토리 클래스를 만들 수 있습니다. 이 리포지토리에 대 한 데이터 저장소는 클래스 내에 있습니다.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

테스트 프로젝트에서 새 클래스 파일을 만들고 이름을 *MockSchoolRepository.cs*로 바꾸고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

이 리포지토리 클래스는 Entity Framework에 직접 액세스 하는 것과 동일한 CRUD 메서드를 갖지만, 데이터베이스를 사용 하는 대신 메모리의 `List` 컬렉션에서 작동 합니다. 이렇게 하면 테스트 클래스가 비즈니스 논리 클래스에 대 한 단위 테스트를 쉽게 설정 하 고 유효성을 검사할 수 있습니다.

## <a name="creating-unit-tests"></a>단위 테스트 만들기

**테스트** 프로젝트 템플릿에서 스텁 단위 테스트 클래스를 만들었으며 다음 작업은 비즈니스 논리 클래스에 추가 하려는 비즈니스 논리에 대 한 단위 테스트 메서드를 추가 하 여이 클래스를 수정 하는 것입니다.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

Contoso 대학에서 개별 강사는 단일 부서의 관리자만 가능 하며,이 규칙을 적용 하려면 비즈니스 논리를 추가 해야 합니다. 테스트를 추가 하 고 테스트를 실행 하 여 실패를 확인 하는 것으로 시작 합니다. 그런 다음 코드를 추가 하 고 테스트가 성공 하는 것으로 예상 되는 테스트를 다시 실행 합니다.

*UnitTest1.cs* 파일을 열고 ContosoUniversity 프로젝트에서 만든 비즈니스 논리 및 데이터 액세스 계층에 대 한 `using` 문을 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

`TestMethod1` 메서드를 다음 메서드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

`CreateSchoolBL` 메서드는 단위 테스트 프로젝트에 대해 만든 리포지토리 클래스의 인스턴스를 만들어 비즈니스 논리 클래스의 새 인스턴스에 전달 합니다. 그런 다음 메서드는 비즈니스 논리 클래스를 사용 하 여 테스트 메서드에서 사용할 수 있는 세 개의 부서를 삽입 합니다.

테스트 메서드는 다른 사용자가 기존 학과와 동일한 관리자를 사용 하 여 새 부서를 삽입 하려고 하거나 다른 사용자가 자신의 ID로 설정 하 여 부서 관리자를 업데이트 하려고 하는 경우 예외를 throw 하는지 확인 합니다. 이미 다른 부서의 관리자 인 경우

예외 클래스를 아직 만들지 않았으므로이 코드는 컴파일되지 않습니다. 컴파일하려면 `DuplicateAdministratorException`를 마우스 오른쪽 단추로 클릭 하 고 **생성**, **클래스**를 차례로 선택 합니다.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

그러면 주 프로젝트에서 예외 클래스를 만든 후에 삭제할 수 있는 클래스를 테스트 프로젝트에 만듭니다. 및는 비즈니스 논리를 구현 했습니다.

테스트 프로젝트를 실행 합니다. 테스트가 정상적으로 실패 합니다.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>비즈니스 논리를 추가 하 여 테스트 통과

다음으로, 다른 부서를 이미 관리자 인 다른 부서의 관리자로 설정할 수 없게 하는 비즈니스 논리를 구현 합니다. 비즈니스 논리 계층에서 예외를 throw 한 다음 사용자가 부서를 편집 하 고 이미 관리자 인 사용자를 선택한 후에 **업데이트** 를 클릭 하면 프레젠테이션 계층에서 예외를 catch 합니다. (페이지를 렌더링 하기 전에 이미 관리자 인 드롭다운 목록에서 강사를 제거할 수도 있지만 여기서는 비즈니스 논리 계층에서 작업 하는 용도로 사용 됩니다.)

먼저 사용자가 두 개 이상의 부서 관리자에 게 강사를 만들려고 할 때 throw 되는 예외 클래스를 만듭니다. 주 프로젝트에서 *BLL* 폴더에 새 클래스 파일을 만들고 이름을 *DuplicateAdministratorException.cs*로 바꾸고 기존 코드를 다음 코드로 바꿉니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

이제 이전에 테스트 프로젝트에서 만든 임시 *DuplicateAdministratorException.cs* 파일을 삭제 하 여 컴파일할 수 있습니다.

주 프로젝트에서 *SchoolBL.cs* 파일을 열고 유효성 검사 논리를 포함 하는 다음 메서드를 추가 합니다. 코드는 나중에 만들 메서드를 참조 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

다른 부서에 동일한 관리자가 이미 있는지 확인 하기 위해 `Department` 엔터티를 삽입 하거나 업데이트 하는 경우이 메서드를 호출 합니다.

이 코드는 메서드를 호출 하 여 데이터베이스에서 삽입 또는 업데이트 중인 엔터티와 `Administrator` 속성 값이 동일한 `Department` 엔터티를 검색 합니다. 하나를 찾은 경우 코드에서 예외를 throw 합니다. 삽입 또는 업데이트 중인 엔터티에 `Administrator` 값이 없는 경우에는 유효성 검사가 필요 하지 않으며, 업데이트 중에 메서드가 호출 되 고 검색 된 `Department` 엔터티가 업데이트 중인 `Department` 엔터티와 일치 하는 경우에는 예외가 throw 되지 않습니다.

`Insert` 및 `Update` 메서드에서 새 메서드를 호출 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

*ISchoolRepository.cs*에서 새 데이터 액세스 메서드에 대해 다음 선언을 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

*SchoolRepository.cs*에서 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

*SchoolRepository.cs*에서 다음과 같은 새로운 데이터 액세스 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

이 코드는 지정 된 관리자가 있는 `Department` 엔터티를 검색 합니다. 부서를 하나만 찾을 수 있습니다 (있는 경우). 그러나 데이터베이스에 제약 조건이 제공 되지 않으므로 여러 부서가 있는 경우 반환 형식은 컬렉션입니다.

기본적으로 개체 컨텍스트는 데이터베이스에서 엔터티를 검색할 때 개체 상태 관리자에서 엔터티를 추적 합니다. `MergeOption.NoTracking` 매개 변수는이 쿼리에 대해이 추적을 수행 하지 않도록 지정 합니다. 쿼리에서 업데이트 하려는 정확한 엔터티를 반환할 수 있으며 해당 엔터티를 연결할 수 없기 때문에이 작업이 필요 합니다. 예를 들어 *학과 페이지에서* history 부서를 편집 하 고 관리자를 변경 하지 않은 상태로 두면이 쿼리는 기록 부서를 반환 합니다. `NoTracking`를 설정 하지 않으면 개체 컨텍스트는 이미 개체 상태 관리자에 기록 부서 엔터티를 포함 합니다. 그런 다음 뷰 상태에서 다시 만들어진 기록 부서 엔터티를 연결 하면 개체 컨텍스트는 `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`라는 예외를 throw 합니다.

`MergeOption.NoTracking`지정 하는 대신이 쿼리에 대해서만 새 개체 컨텍스트를 만들 수 있습니다. 새 개체 컨텍스트에는 자체 개체 상태 관리자가 있기 때문에 `Attach` 메서드를 호출 하면 충돌이 발생 하지 않습니다. 새 개체 컨텍스트는 원본 개체 컨텍스트와 메타 데이터 및 데이터베이스 연결을 공유 하므로이 대체 방법의 성능 저하는 최소화 됩니다. 그러나 여기에 표시 된 방법에는 다른 컨텍스트에서 유용 하 게 사용할 수 있는 `NoTracking` 옵션이 도입 되었습니다. `NoTracking` 옵션은이 시리즈의 이후 자습서에서 자세히 설명 합니다.)

테스트 프로젝트에서 *MockSchoolRepository.cs*에 새 데이터 액세스 메서드를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

이 코드는 LINQ를 사용 하 여 `ContosoUniversity` 프로젝트 리포지토리에서 LINQ to Entities 사용 하는 것과 동일한 데이터 선택 항목을 수행 합니다.

테스트 프로젝트를 다시 실행 합니다. 이번에는 테스트가 성공합니다.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>ObjectDataSource 예외 처리

`ContosoUniversity` 프로젝트에서 *부서나 .aspx* 페이지를 실행 하 고 다른 부서에 대 한 관리자가 이미 있는 사용자로 부서 관리자를 변경 합니다. (데이터베이스가 잘못 된 데이터로 미리 로드 되었으므로이 자습서 중에 추가한 부서만 편집할 수 있습니다.) 다음 서버 오류 페이지가 표시 됩니다.

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

사용자에 게 이러한 종류의 오류 페이지를 표시 하지 않으려면 오류 처리 코드를 추가 해야 합니다. 학과 *.aspx* 를 열고 `DepartmentsObjectDataSource`의 `OnUpdated` 이벤트에 대 한 처리기를 지정 합니다. 이제 `ObjectDataSource` 여는 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

*Departments.aspx.cs*에서 다음 `using` 문을 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

`Updated` 이벤트에 대 한 다음 처리기를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

`ObjectDataSource` 컨트롤이 업데이트를 수행 하려고 할 때 예외를 catch 하는 경우 이벤트 인수 (`e`)의 예외를이 처리기에 전달 합니다. 처리기의 코드는 예외가 중복 된 관리자 예외 인지 여부를 확인 합니다. 인 경우 코드에서 표시할 `ValidationSummary` 컨트롤에 대 한 오류 메시지를 포함 하는 유효성 검사기 컨트롤을 만듭니다.

페이지를 실행 하 고 다른 사람에 게 두 부서의 관리자를 다시 시도 합니다. 이번에는 `ValidationSummary` 컨트롤에서 오류 메시지를 표시 합니다.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

*DepartmentsAdd* 페이지에서 유사한 변경 작업을 수행 합니다. *DepartmentsAdd*에서 `DepartmentsObjectDataSource`의 `OnInserted` 이벤트에 대 한 처리기를 지정 합니다. 결과 태그는 다음 예제와 유사 합니다.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

*DepartmentsAdd.aspx.cs*에서 동일한 `using` 문을 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

다음 이벤트 처리기를 추가 합니다.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

이제 *DepartmentsAdd.aspx.cs* 페이지를 테스트 하 여 한 사람을 두 명 이상의 부서 관리자로 만드는 시도도 올바르게 처리 되는지 확인할 수 있습니다.

이렇게 하면 Entity Framework에서 `ObjectDataSource` 컨트롤을 사용 하기 위한 리포지토리 패턴 구현에 대 한 소개를 완료 합니다. 리포지토리 패턴 및 테스트 용이성에 대 한 자세한 내용은 MSDN 백서 [테스트 용이성 및 Entity Framework 4.0](https://msdn.microsoft.com/library/ff714955.aspx)을 참조 하세요.

다음 자습서에서는 응용 프로그램에 정렬 및 필터링 기능을 추가 하는 방법을 알아봅니다.

> [!div class="step-by-step"]
> [이전](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [다음](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
