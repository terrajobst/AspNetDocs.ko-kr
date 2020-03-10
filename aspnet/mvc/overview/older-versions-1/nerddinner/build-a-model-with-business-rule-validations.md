---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: 비즈니스 규칙 유효성 검사를 사용 하 여 모델 작성 | Microsoft Docs
author: microsoft
description: 3 단계에서는 팀 간 Ddinner 응용 프로그램의 데이터베이스를 쿼리 및 업데이트 하는 데 사용할 수 있는 모델을 만드는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 6ebf1b71c089229ba9139ff7dc788b8978724046
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435581"
---
# <a name="build-a-model-with-business-rule-validations"></a>비즈니스 규칙 유효성 검사를 사용하여 모델 빌드

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 3 단계입니다.
> 
> 3 단계에서는 팀 간 Ddinner 응용 프로그램의 데이터베이스를 쿼리 및 업데이트 하는 데 사용할 수 있는 모델을 만드는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner 3 단계: 모델 빌드

모델-뷰-컨트롤러 프레임 워크에서 "모델" 이라는 용어는 응용 프로그램의 데이터를 나타내는 개체와 유효성 검사 및 비즈니스 규칙을 통합 하는 해당 도메인 논리를 나타냅니다. 모델은 MVC 기반 응용 프로그램의 "핵심" 이며, 나중에 근본적으로 이러한 응용 프로그램의 동작을 구동 합니다.

ASP.NET MVC 프레임 워크는 모든 데이터 액세스 기술 사용을 지원 하 고 개발자는 다양 한 .NET 데이터 옵션 중에서 선택 하 여 LINQ to Entities, LINQ to SQL, NHibernate 절전 모드, LLBLGen Pro, SubSonic, WilsonORM 또는 단지 원시 ADO를 비롯 한 모델을 구현할 수 있습니다. NET DataReaders 또는 데이터 집합.

Microsoft는이 응용 프로그램을 사용 하 여 데이터베이스 디자인과 매우 긴밀 하 게 일치 하는 간단한 모델을 만들고 몇 가지 사용자 지정 유효성 검사 논리 및 비즈니스 규칙을 추가 하는 LINQ to SQL을 사용 합니다. 그런 다음 응용 프로그램의 나머지 부분에서 데이터 지 속성 구현을 추상화 하는 데 도움이 되는 리포지토리 클래스를 구현 하 고 단위 테스트를 쉽게 수행할 수 있도록 합니다.

### <a name="linq-to-sql"></a>LINQ to SQL

LINQ to SQL은 .NET 3.5의 일부로 제공 되는 ORM (개체 관계형 매퍼)입니다.

LINQ to SQL은 코드를 사용할 수 있는 .NET 클래스에 데이터베이스 테이블을 매핑할 수 있는 쉬운 방법을 제공 합니다. Microsoft는이 응용 프로그램을 사용 하 여 데이터베이스 내의 Dinners 및 RSVP 테이블을 Dinner and RSVP 클래스에 매핑합니다. Dinners 및 RSVP 테이블의 열은 Dinner and RSVP 클래스의 속성에 해당 합니다. 각 Dinner and RSVP 개체는 데이터베이스의 Dinners 또는 RSVP 테이블 내에서 별도의 행을 나타냅니다.

LINQ to SQL를 사용 하면 데이터베이스 데이터를 사용 하 여 Dinner 및 RSVP 개체를 검색 하 고 업데이트 하는 SQL 문을 수동으로 생성 하지 않아도 됩니다. 대신 Dinner and RSVP 클래스, 데이터베이스에 매핑되는 방법 및 두 클래스 간의 관계를 정의 합니다. 그러면 LINQ to SQL는 조작 하 고 사용할 때 런타임에 사용할 적절 한 SQL 실행 논리를 생성 합니다.

VB에서 LINQ 언어 지원을 사용 하 여 데이터베이스에서 C# DINNER and RSVP 개체를 검색 하는 표현 쿼리를 작성할 수 있습니다. 이렇게 하면 작성 해야 하는 데이터 코드의 양이 최소화 되며, 정말 명확한 응용 프로그램을 빌드할 수 있습니다.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>프로젝트에 LINQ to SQL 클래스 추가

먼저 프로젝트 내에서 "모델" 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가&gt;새 항목** 메뉴 명령을 선택 합니다.

![](build-a-model-with-business-rule-validations/_static/image1.png)

그러면 "새 항목 추가" 대화 상자가 표시 됩니다. "Data" 범주를 기준으로 필터링 하 고 내에서 "LINQ to SQL 클래스" 템플릿을 선택 합니다.

![](build-a-model-with-business-rule-validations/_static/image2.png)

항목의 이름을 "" 우 Ddinner "로 하 고" 추가 "단추를 클릭 합니다. Visual Studio는 \Stoml 디렉터리 아래에 해당 하는 파일을 추가 하 고 LINQ to SQL 개체 관계형 디자이너를 엽니다.

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>LINQ to SQL를 사용 하 여 데이터 모델 클래스 만들기

LINQ to SQL를 사용 하면 기존 데이터베이스 스키마에서 데이터 모델 클래스를 신속 하 게 만들 수 있습니다. 이렇게 하려면 서버 탐색기에서 작업 중인 데이터베이스를 열고 모델링 하려는 테이블을 선택 합니다.

![](build-a-model-with-business-rule-validations/_static/image4.png)

그런 다음 테이블을 LINQ to SQL 디자이너 화면으로 끌어 올 수 있습니다. LINQ to SQL이 작업을 수행 하면 테이블의 스키마 (데이터베이스 테이블 열에 매핑되는 클래스 속성 포함)를 사용 하 여 Dinner 및 RSVP 클래스가 자동으로 만들어집니다.

![](build-a-model-with-business-rule-validations/_static/image5.png)

기본적으로 LINQ to SQL 디자이너는 데이터베이스 스키마를 기반으로 클래스를 만들 때 테이블 및 열 이름을 자동으로 "복수 및" 합니다. 예를 들어 위의 예제에 있는 "Dinners" 테이블은 "Dinner" 클래스를 생성 했습니다. 이 클래스 이름 지정은 .NET 명명 규칙과 일치 하는 모델을 만드는 데 도움이 되며 일반적으로 디자이너가 많은 테이블을 추가할 때이를 편리 하 게 수정 합니다. 그러나 디자이너에서 생성 하는 클래스 또는 속성의 이름이 마음에 들지 않는 경우 언제 든 지이를 재정의 하 고 원하는 이름으로 변경할 수 있습니다. 디자이너 내에서 엔터티/속성 이름을 편집 하거나 속성 표를 통해 수정 하 여이 작업을 수행할 수 있습니다.

기본적으로 LINQ to SQL 디자이너는 테이블의 기본 키/외래 키 관계를 검사 하 고 그에 따라 생성 되는 여러 모델 클래스 사이에 기본 "관계 연결"을 자동으로 만듭니다. 예를 들어 Dinners 및 RSVP 테이블을 LINQ to SQL designer로 끌어 오면, RSVP 테이블에 Dinners 테이블에 대 한 외래 키가 있다는 사실을 기반으로 둘 간의 일 대 다 관계 연결이 유추 됩니다 .이는 디자이너):

![](build-a-model-with-business-rule-validations/_static/image6.png)

위의 연결을 사용 하면 LINQ to SQL는 개발자가 지정 된 RSVP와 연결 된 Dinner a에 액세스할 때 사용할 수 있는 RSVP 클래스에 강력한 형식의 "Dinner" 속성을 추가 합니다. 또한 Dinner class는 개발자가 특정 저녁에 연결 된 RSVP 개체를 검색 하 고 업데이트할 수 있도록 하는 "RSVPs" 컬렉션 속성을 갖게 됩니다.

아래에서 새 RSVP 개체를 만들어 Dinner RSVPs 컬렉션에 추가 하는 경우 Visual Studio 내에서 intellisense의 예제를 볼 수 있습니다. LINQ to SQL에서 Dinner object에 "RSVPs" 컬렉션을 자동으로 추가 하는 방법을 확인 합니다.

![](build-a-model-with-business-rule-validations/_static/image7.png)

RSVPs 컬렉션에 RSVP 개체를 추가 하 여 데이터베이스의 Dinner a 및 RSVP 행 사이에 외래 키 관계를 연결 하는 LINQ to SQL를 지시 합니다.

![](build-a-model-with-business-rule-validations/_static/image8.png)

디자이너에서 테이블 연결을 모델링 하거나 이름을 지정 하지 않은 경우 재정의할 수 있습니다. 디자이너 내에서 연결 화살표를 클릭 하 고 속성 표를 통해 속성에 액세스 하 여 이름을 바꾸거나 삭제 하거나 수정 합니다. 그러나 이러한 응용 프로그램의 경우에는 기본 연결 규칙이 작성 중인 데이터 모델 클래스에서 잘 작동 하며 기본 동작만 사용할 수 있습니다.

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext 클래스

Visual Studio는 LINQ to SQL 디자이너를 사용 하 여 정의 된 모델 및 데이터베이스 관계를 나타내는 .NET 클래스를 자동으로 만듭니다. 솔루션에 추가 된 각 LINQ to SQL 디자이너 파일에 대해 LINQ to SQL DataContext 클래스도 생성 됩니다. LINQ to SQL 클래스 항목 "NerdDinner"의 이름을 지정 했으므로 생성 된 DataContext 클래스를 "Cddinnerdatacontext" 라고 합니다. 이러한 작업은 데이터베이스와 상호 작용 하는 기본 방법입니다.

Microsoft의 NerdDinnerDataContext 클래스는 두 개의 속성 ("Dinners" 및 "RSVPs")을 제공 하며,이는 데이터베이스 내에서 모델링 된 두 테이블을 나타냅니다. 를 사용 C# 하 여 이러한 속성에 대해 LINQ 쿼리를 작성 하 고 데이터베이스에서 DINNER and RSVP 개체를 쿼리하고 검색할 수 있습니다.

다음 코드에서는 Dinners Ddinnerdatacontext 개체를 인스턴스화하고 앞으로 발생 하는 시퀀스를 가져오기 위해 LINQ 쿼리를 수행 하는 방법을 보여 줍니다. Visual Studio는 LINQ 쿼리를 작성할 때 전체 intellisense를 제공 하 고, 여기에서 반환 된 개체는 강력 하 게 형식화 되며 intellisense도 지원 합니다.

![](build-a-model-with-business-rule-validations/_static/image9.png)

저녁 및 RSVP 개체에 대 한 쿼리를 허용 하는 것 외에도, 작업을 수행 하는 Dinner a 및 RSVP 개체에 대 한 변경 내용을 자동으로 추적 합니다. 이 기능을 사용 하 여 명시적 SQL 업데이트 코드를 작성 하지 않고도 변경 내용을 데이터베이스에 다시 저장할 수 있습니다.

예를 들어 아래 코드는 LINQ 쿼리를 사용 하 여 데이터베이스에서 단일 Dinner object를 검색 하 고 두 개의 Dinner properties를 업데이트 한 후 변경 내용을 데이터베이스에 다시 저장 하는 방법을 보여 줍니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

위의 코드에서 작업 하는 해당 개체의 속성 변경 내용을 자동으로 추적 합니다. "SubmitChanges ()" 메서드를 호출 하면 업데이트 된 값을 다시 저장 하기 위해 데이터베이스에 적합 한 SQL "UPDATE" 문이 실행 됩니다.

### <a name="creating-a-dinnerrepository-class"></a>DinnerRepository 클래스 만들기

작은 응용 프로그램의 경우 컨트롤러가 LINQ to SQL DataContext 클래스에 대해 직접 작동 하 고 컨트롤러 내에 LINQ 쿼리를 포함 하는 것이 적절 하지 않을 수 있습니다. 그러나 응용 프로그램이 커질수록이 방법은 유지 관리 및 테스트에 번거로울 수 있습니다. 또한 동일한 LINQ 쿼리를 여러 위치에서 복제 하 게 될 수도 있습니다.

응용 프로그램을 더 쉽게 유지 관리 하 고 테스트할 수 있는 방법 중 하나는 "리포지토리" 패턴을 사용 하는 것입니다. 리포지토리 클래스를 사용 하 여 데이터 쿼리 및 지 속성 논리를 캡슐화 하 고, 응용 프로그램에서 데이터 지 속성의 구현 세부 정보를 추상화 합니다. 응용 프로그램 코드를 정리 하는 것 외에도, 리포지토리 패턴을 사용 하면 나중에 데이터 저장소 구현을 더 쉽게 변경할 수 있으며, 실제 데이터베이스를 요구 하지 않고 응용 프로그램 단위 테스트를 용이 하 게 할 수 있습니다.

Microsoft의 동료 Ddinner 응용 프로그램의 경우 다음 서명으로 DinnerRepository 클래스를 정의 합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*참고:이 챕터의 뒷부분에서는이 클래스에서 IDinnerRepository 인터페이스를 추출 하 고 컨트롤러에서 종속성 주입을 사용 하도록 설정 합니다. 이를 시작 하기 위해 간단 하 게 시작 하 고,이 작업을 수행 하는 것이 좋습니다.*

이 클래스를 구현 하려면 "모델" 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가&gt;새 항목** 메뉴 명령을 선택 합니다. "새 항목 추가" 대화 상자 내에서 "클래스" 템플릿을 선택 하 고 파일 이름을 "DinnerRepository.cs"로 표시 합니다.

![](build-a-model-with-business-rule-validations/_static/image10.png)

그런 다음 아래 코드를 사용 하 여 d Innerrepository 클래스를 구현할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>DinnerRepository 클래스를 사용 하 여 검색, 업데이트, 삽입 및 삭제

이제 microsoft에서 제공 하는 기본 작업을 보여 주는 몇 가지 코드 예제를 살펴보겠습니다.

#### <a name="querying-examples"></a>예제 쿼리

아래 코드는 다음 코드에서는 d Innerid 값을 사용 하 여 단일 저녁을 검색 합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

아래 코드는 예정 된 모든 dinners를 검색 하 고 반복 합니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>삽입 및 업데이트 예제

아래 코드에서는 두 개의 새 dinners를 추가 하는 방법을 보여 줍니다. 리포지토리에 대 한 추가/수정 내용은 "Save ()" 메서드가 호출 될 때까지 데이터베이스에 커밋되지 않습니다. LINQ to SQL은 데이터베이스 트랜잭션의 모든 변경 내용을 자동으로 래핑하고,이에 대 한 모든 변경 사항이 발생 하거나 리포지토리가 저장 될 때 수행 되지 않습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

아래 코드는 기존 Dinner object를 검색 하 고 그에 대 한 두 개의 속성을 수정 합니다. 저장소에서 "Save ()" 메서드를 호출 하면 변경 내용이 데이터베이스로 다시 커밋됩니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

아래 코드는 dinner a를 검색 한 다음 RSVP를 추가 합니다. RSVPs 컬렉션을 사용 하 여이를 수행 합니다 .이는 데이터베이스에서 두 개체 사이에 기본 키/외래 키 관계가 있기 때문에 생성 LINQ to SQL는 Dinner 개체의 경우에는이 컬렉션을 사용 합니다. 저장소에서 "Save ()" 메서드가 호출 되 면이 변경 내용은 새 RSVP 테이블 행으로 데이터베이스에 다시 저장 됩니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Delete 예제

아래 코드는 기존 Dinner object를 검색 한 다음 삭제 되도록 표시 합니다. 저장소에서 "Save ()" 메서드를 호출 하면 삭제 내용이 데이터베이스에 커밋됩니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>모델 클래스와 유효성 검사 및 비즈니스 규칙 논리 통합

유효성 검사 및 비즈니스 규칙 논리를 통합 하는 작업은 데이터를 사용 하는 응용 프로그램의 핵심 부분입니다.

#### <a name="schema-validation"></a>스키마 유효성 검사

LINQ to SQL 디자이너를 사용 하 여 모델 클래스를 정의 하는 경우 데이터 모델 클래스의 속성 데이터 형식은 데이터베이스 테이블의 데이터 형식에 해당 합니다. 예: Dinners 테이블의 "EventDate" 열이 "datetime" 인 경우 LINQ to SQL에서 만든 데이터 모델 클래스는 "DateTime" (기본 제공 .NET 데이터 형식) 형식이 됩니다. 즉, 코드에서 정수 또는 부울 값을 할당 하려고 하면 컴파일 오류가 발생 하 고, 런타임에 잘못 된 문자열 형식을 암시적으로 변환 하려고 하면 오류가 자동으로 발생 합니다.

문자열을 사용 하는 경우 SQL 삽입 공격 으로부터 사용자를 보호 하는 데 도움이 되는 문자열을 사용 하는 경우에도 자동으로 SQL 값 이스케이프 처리를 LINQ to SQL 합니다.

#### <a name="validation-and-business-rule-logic"></a>유효성 검사 및 비즈니스 규칙 논리

스키마 유효성 검사는 첫 번째 단계로 유용 하지만 거의 충분 하지 않습니다. 대부분의 실제 시나리오에서는 여러 속성을 확장 하 고, 코드를 실행 하 고, 종종 모델 상태를 인식 하는 (예:/updated/deleted를 만드는 경우) 또는 "보관 됨"과 같은 도메인별 상태에서 모델의 상태를 인식 하는 다양 한 유효성 검사 논리를 지정할 수 있어야 합니다. 모델 클래스에 대 한 유효성 검사 규칙을 정의 하 고 적용 하는 데 사용할 수 있는 다양 한 패턴 및 프레임 워크가 있습니다. 여기에는이를 도와 주는 데 사용할 수 있는 몇 가지 .NET 기반 프레임 워크가 있습니다. ASP.NET MVC 응용 프로그램 내에서 상당히 많은 것을 사용할 수 있습니다.

Microsoft는이 부분을 사용 하 여 microsoft는 Dinner model 개체에서 IsValid 속성 및 GetRuleViolations () 메서드를 노출 하는 비교적 간단 하 고 직접적인 전달 패턴을 사용 합니다. IsValid 속성은 유효성 검사 및 비즈니스 규칙이 모두 유효한 지 여부에 따라 true 또는 false를 반환 합니다. GetRuleViolations () 메서드는 규칙 오류 목록을 반환 합니다.

프로젝트에 "partial 클래스"를 추가 하 여 Dinner model에 대해 IsValid 및 GetRuleViolations ()을 구현 합니다. Partial 클래스를 사용 하 여 VS designer에서 유지 관리 되는 클래스에 메서드/속성/이벤트를 추가할 수 있으며 (예: LINQ to SQL designer에서 생성 한 Dinner class), 코드를 사용 하 여 messing에서 도구를 방지 하는 데 도움이 됩니다. \Stoml 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 항목 추가" 메뉴 명령을 선택 하 여 프로젝트에 새 partial 클래스를 추가할 수 있습니다. 그런 다음 "새 항목 추가" 대화 상자에서 "클래스" 템플릿을 선택 하 고 이름을 Dinner.cs으로 지정할 수 있습니다.

![](build-a-model-with-business-rule-validations/_static/image11.png)

"추가" 단추를 클릭 하면 Dinner.cs 파일이 프로젝트에 추가 되 고 IDE 내에서 열립니다. 그런 다음 아래 코드를 사용 하 여 기본 규칙/유효성 검사 적용 프레임 워크를 구현할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

위의 코드에 대 한 몇 가지 참고 사항:

- Dinner class 앞에는 "partial" 키워드가 붙습니다 .이는 그 안에 포함 된 코드가 LINQ to SQL designer에서 생성/유지 관리 되 고 단일 클래스로 컴파일되는 클래스와 결합 됨을 의미 합니다.
- RuleViolation 클래스는 규칙 위반에 대 한 자세한 정보를 제공할 수 있도록 프로젝트에 추가할 도우미 클래스입니다.
- Dinner. GetRuleViolations () 메서드를 통해 유효성 검사 및 비즈니스 규칙을 평가 합니다 (곧 구현 됨). 그런 다음 규칙 오류에 대 한 자세한 정보를 제공 하는 RuleViolation 개체의 시퀀스를 다시 반환 합니다.
- Dinner IsValid 속성은 Dinner object에 활성 RuleViolations 있는지 여부를 나타내는 편리한 도우미 속성을 제공 합니다. 언제 든 지 Dinner object를 사용 하 여 개발자가 사전에 확인할 수 있으며 예외를 발생 시 키 지 않습니다.
- OnValidate () 부분 메서드는 Dinner object가 데이터베이스 내에서 지속 될 때마다 알릴 수 있도록 하는 LINQ to SQL 제공 하는 후크입니다. 위의 OnValidate () 구현에서는 Dinner a가 저장 되기 전에 RuleViolations 없는지 확인 합니다. 잘못 된 상태에 있는 경우 예외를 발생 시킵니다 .이로 인해 LINQ to SQL 트랜잭션을 중단 합니다.

이 방법은 유효성 검사 및 비즈니스 규칙을에 통합할 수 있는 간단한 프레임 워크를 제공 합니다. 이제 GetRuleViolations () 메서드에 아래 규칙을 추가 해 보겠습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

의 C# "반환 반환" 기능을 사용 하 여 ruleviolations의 시퀀스를 반환 합니다. 위의 처음 6 개 규칙 검사는 Dinner in의 문자열 속성이 null 이거나 비어 있을 수 없음을 강제로 적용 합니다. 마지막 규칙은 더 흥미로운 일 이며, 프로젝트에 추가할 수 있는 PhoneValidator () 도우미 메서드를 호출 하 여 연락처 전화 번호 형식이 Dinner country와 일치 하는지 확인 합니다.

을 (를) 사용할 수 있습니다. 이 전화 유효성 검사 지원을 구현 하는 NET의 정규식 지원. 다음은 국가별 Regex 패턴 검사를 추가할 수 있도록 하는 프로젝트에 추가할 수 있는 간단한 PhoneValidator 구현입니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>유효성 검사 및 비즈니스 논리 위반 처리

위의 유효성 검사 및 비즈니스 규칙 코드를 추가 했으므로 Dinner를 만들거나 업데이트 하려고 할 때마다 유효성 검사 논리 규칙이 평가 되 고 적용 됩니다.

개발자는 다음과 같은 코드를 작성 하 여 Dinner object가 유효한 지 여부를 사전에 확인 하 고 예외를 발생 시 키 지 않고 모든 위반 목록을 검색할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

Dinner in을 잘못 된 상태로 저장 하려는 경우에는, d Innerrepository에서 Save () 메서드를 호출할 때 예외가 발생 합니다. 이는 LINQ to SQL이 dinner s 변경 내용을 저장 하기 전에 OnValidate () 부분 메서드를 자동으로 호출 하 고 OnValidate ()에 코드를 추가 하 여 저녁에 규칙 위반이 있는 경우 예외를 발생 시키기 때문에 발생 합니다. 이 예외를 catch 하 고 대응적 위반 목록을 검색 하 여 수정할 수 있습니다.

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

유효성 검사 및 비즈니스 규칙은 UI 계층 내에서 구현 되는 것이 아니라 모델 계층 내에서 구현 되기 때문에 응용 프로그램 내의 모든 시나리오에서 적용 되 고 사용 됩니다. 나중에 비즈니스 규칙을 변경 하거나 추가 하 고 Dinner objects를 사용 하는 모든 코드를 사용할 수 있습니다.

응용 프로그램 및 UI 논리 전체에서 이러한 변경 내용을 적용 하지 않고 비즈니스 규칙을 한 곳에서 유연 하 게 변경할 수 있으므로, 잘 작성 된 응용 프로그램의 부호와 MVC 프레임 워크가 권장 하는 이점을 누릴 수 있습니다.

### <a name="next-step"></a>다음 단계

이제 데이터베이스를 쿼리 및 업데이트 하는 데 사용할 수 있는 모델을 얻었습니다.

이제 HTML UI 환경을 빌드하는 데 사용할 수 있는 일부 컨트롤러 및 뷰를 프로젝트에 추가 해 보겠습니다.

> [!div class="step-by-step"]
> [이전](create-a-database.md)
> [다음](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
