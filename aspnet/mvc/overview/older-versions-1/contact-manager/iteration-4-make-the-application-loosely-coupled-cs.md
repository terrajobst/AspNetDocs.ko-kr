---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: '반복 #4 – 응용 프로그램을 느슨하게 결합 (C#) | Microsoft Docs'
author: microsoft
description: 이 네 번째 반복에서는 몇 가지 소프트웨어 디자인 패턴을 활용 하 여 연락처 관리자 응용 프로그램을 보다 쉽게 유지 관리 하 고 수정할 수 있습니다. For...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: ce8e3c4ff8a59be9f2f572813db599604216119d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437975"
---
# <a name="iteration-4--make-the-application-loosely-coupled-c"></a>반복 #4 – 응용 프로그램을 느슨하게 결합 (C#)

[Microsoft](https://github.com/microsoft) 에서

[코드 다운로드](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> 이 네 번째 반복에서는 몇 가지 소프트웨어 디자인 패턴을 활용 하 여 연락처 관리자 응용 프로그램을 보다 쉽게 유지 관리 하 고 수정할 수 있습니다. 예를 들어 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램을 리팩터링 합니다.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Contact Management ASP.NET MVC 응용 프로그램 빌드 (C#)

이 자습서 시리즈에서는 전체 연락처 관리 응용 프로그램을 처음부터 끝까지 빌드 합니다. 연락처 관리자 응용 프로그램을 사용 하면 연락처 정보 (이름, 전화 번호 및 전자 메일 주소)를 사용자 목록으로 저장할 수 있습니다.

여러 반복을 통해 응용 프로그램을 빌드합니다. 각 반복을 통해 응용 프로그램을 점진적으로 개선 합니다. 이 여러 반복 방법의 목표는 각 변경의 이유를 이해할 수 있게 하는 것입니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서는 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업 (만들기, 읽기, 업데이트 및 삭제 (CRUD))에 대 한 지원을 추가 합니다.

- 반복 #2-응용 프로그램을 멋지게 만듭니다. 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 css 스타일 시트를 수정 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사를 추가 합니다. 세 번째 반복에서는 기본 폼 유효성 검사를 추가 합니다. 사용자가 필요한 양식 필드를 완료 하지 않고 양식을 전송 하지 못하도록 합니다. 또한 전자 메일 주소 및 전화 번호의 유효성을 검사 합니다.

- 반복 #4-응용 프로그램이 느슨하게 결합 되도록 합니다. 이 네 번째 반복에서는 몇 가지 소프트웨어 디자인 패턴을 활용 하 여 연락처 관리자 응용 프로그램을 보다 쉽게 유지 관리 하 고 수정할 수 있습니다. 예를 들어 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램을 리팩터링 합니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서는 단위 테스트를 추가 하 여 응용 프로그램을 더 쉽게 유지 관리 하 고 수정할 수 있도록 합니다. Microsoft는 데이터 모델 클래스를 모의 하 고 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 빌드 했습니다.

- 반복 #6-테스트 기반 개발을 사용 합니다. 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성 하 고 단위 테스트에 대 한 코드를 작성 하 여 응용 프로그램에 새 기능을 추가 합니다. 이 반복에서는 연락처 그룹을 추가 합니다.

- 반복 #7-Ajax 기능을 추가 합니다. 일곱 번째 반복에서는 Ajax에 대 한 지원을 추가 하 여 응용 프로그램의 응답성과 성능을 향상 시킵니다.

## <a name="this-iteration"></a>이 반복

연락처 관리자 응용 프로그램의이 네 번째 반복에서는 응용 프로그램을 리팩터링하여 응용 프로그램을 더 느슨하게 결합 합니다. 응용 프로그램이 느슨하게 결합 되어 있으면 응용 프로그램의 다른 부분에서 코드를 수정할 필요 없이 응용 프로그램의 한 부분에서 코드를 수정할 수 있습니다. 느슨하게 결합 된 응용 프로그램을 변경 하는 것이 더 탄력적입니다.

현재 연락처 관리자 응용 프로그램에서 사용 하는 모든 데이터 액세스 및 유효성 검사 논리는 컨트롤러 클래스에 포함 되어 있습니다. 이는 잘못 된 개념입니다. 응용 프로그램의 한 부분을 수정 해야 할 때마다 응용 프로그램의 다른 부분에 버그가 발생 하는 위험을 초래할 수 있습니다. 예를 들어 유효성 검사 논리를 수정 하면 데이터 액세스 또는 컨트롤러 논리에 새 버그를 도입 하는 위험을 초래할 수 있습니다.

> [!NOTE] 
> 
> (SRP), 클래스는 둘 이상의 이유를 변경 하지 않아야 합니다. 컨트롤러, 유효성 검사 및 데이터베이스 논리를 혼합 하는 것은 단일 책임 원칙을 광범위 하 게 위반 하는 것입니다.

응용 프로그램을 수정 해야 하는 여러 가지 이유가 있습니다. 응용 프로그램에 새 기능을 추가 하거나, 응용 프로그램의 버그를 수정 해야 하거나, 응용 프로그램의 기능을 구현 하는 방법을 수정 해야 할 수 있습니다. 응용 프로그램은 거의 정적이 지 않습니다. 시간이 지남에 따라 증가 하 고 변화 하는 경향이 있습니다.

예를 들어, 데이터 액세스 계층을 구현 하는 방법을 변경 한다고 가정해 보겠습니다. 현재, Contact Manager 응용 프로그램은 Microsoft Entity Framework를 사용 하 여 데이터베이스에 액세스 합니다. 그러나 ADO.NET Data Services 또는 NHibernate 절전 모드와 같은 새로운 또는 대체 데이터 액세스 기술로 마이그레이션하도록 결정할 수 있습니다. 그러나 데이터 액세스 코드가 유효성 검사 및 컨트롤러 코드와 격리 되지 않으므로 데이터 액세스와 직접적인 관련이 없는 다른 코드를 수정 하지 않고도 응용 프로그램에서 데이터 액세스 코드를 수정할 수 있는 방법은 없습니다.

반면에 응용 프로그램이 느슨하게 결합 되어 있으면 응용 프로그램의 다른 부분을 건드리지 않고도 응용 프로그램의 한 부분을 변경할 수 있습니다. 예를 들어 유효성 검사 또는 컨트롤러 논리를 수정 하지 않고 데이터 액세스 기술을 전환할 수 있습니다.

이 반복에서는 몇 가지 소프트웨어 디자인 패턴을 활용 하 여 연락처 관리자 응용 프로그램을 느슨하게 결합 된 응용 프로그램으로 리팩터링할 수 있습니다. 완료 되 면 연락처 관리자가 이전에 수행 하지 않은 모든 작업을 수행 합니다. 그러나 나중에 응용 프로그램을 더 쉽게 변경할 수 있습니다.

> [!NOTE] 
> 
> 리팩터링은 기존 기능이 손실 되지 않는 방식으로 응용 프로그램을 다시 작성 하는 프로세스입니다.

## <a name="using-the-repository-software-design-pattern"></a>리포지토리 소프트웨어 디자인 패턴 사용

첫 번째 변경 내용은 리포지토리 패턴 이라는 소프트웨어 디자인 패턴을 활용 하는 것입니다. 리포지토리 패턴을 사용 하 여 응용 프로그램의 나머지 부분에서 데이터 액세스 코드를 격리 합니다.

리포지토리 패턴을 구현 하려면 다음 두 단계를 완료 해야 합니다.

1. 인터페이스 만들기
2. 인터페이스를 구현 하는 구체적인 클래스 만들기

먼저 수행 해야 하는 모든 데이터 액세스 방법을 설명 하는 인터페이스를 만들어야 합니다. IContactManagerRepository 인터페이스는 목록 1에 포함 되어 있습니다. 이 인터페이스는 CreateContact (), DeleteContact (), EditContact (), GetContact 및 ListContacts ()의 5 가지 메서드를 설명 합니다.

**목록 1-Models\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

다음으로 IContactManagerRepository 인터페이스를 구현 하는 구체적인 클래스를 만들어야 합니다. Microsoft Entity Framework를 사용 하 여 데이터베이스에 액세스 하기 때문에 EntityContactManagerRepository 라는 새 클래스를 만듭니다. 이 클래스는 목록 2에 포함 되어 있습니다.

**목록 2-Models\EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

EntityIContactManagerRepository Managerrepository 클래스는 인터페이스를 구현 합니다. 클래스는 해당 인터페이스에 설명 된 5 개의 메서드를 모두 구현 합니다.

인터페이스를 사용 해야 하는 이유를 궁금할 수 있습니다. 인터페이스와 인터페이스를 구현 하는 클래스를 모두 만들어야 하는 이유는 무엇 인가요?

한 가지 예외를 제외 하 고 응용 프로그램의 나머지 부분은 구체적 클래스가 아니라 인터페이스와 상호 작용 합니다. EntityContactManagerRepository 클래스에서 노출 하는 메서드를 호출 하는 대신 IContactManagerRepository 인터페이스에 의해 노출 되는 메서드를 호출 합니다.

이렇게 하면 응용 프로그램의 나머지 부분을 수정할 필요 없이 새 클래스를 사용 하 여 인터페이스를 구현할 수 있습니다. 예를 들어 향후에는 IContactManagerRepository 인터페이스를 구현 하는 DataServicesContactManagerRepository 클래스를 구현 하는 것이 좋습니다. DataServicesContactManagerRepository 클래스는 ADO.NET Data Services를 사용 하 여 Microsoft Entity Framework 대신 데이터베이스에 액세스할 수 있습니다.

응용 프로그램 코드가 구체적인 EntityIContactManagerRepository Managerrepository 클래스 대신 인터페이스에 대해 프로그래밍 되는 경우 코드의 나머지 부분을 수정 하지 않고도 구체적 클래스를 전환할 수 있습니다. 예를 들어 데이터 액세스 또는 유효성 검사 논리를 수정 하지 않고 EntityDataServicesContactManagerRepository Managerrepository 클래스에서 클래스로 전환할 수 있습니다.

구체적 클래스 대신 인터페이스 (추상화)를 프로그래밍 하면 응용 프로그램의 복원 력이 향상 됩니다.

> [!NOTE] 
> 
> 리팩터링, 인터페이스 추출 메뉴 옵션을 선택 하 여 Visual Studio 내의 구체적인 클래스에서 인터페이스를 빠르게 만들 수 있습니다. 예를 들어, 먼저 EntityIContactManagerRepository Managerrepository 클래스를 만든 후 Extract 인터페이스를 사용 하 여 자동으로 인터페이스를 생성할 수 있습니다.

## <a name="using-the-dependency-injection-software-design-pattern"></a>종속성 주입 소프트웨어 디자인 패턴 사용

데이터 액세스 코드를 별도의 리포지토리 클래스로 마이그레이션 했으므로이 클래스를 사용 하려면 연락처 컨트롤러를 수정 해야 합니다. 여기서는 종속성 주입 이라는 소프트웨어 디자인 패턴을 활용 하 여 컨트롤러에서 리포지토리 클래스를 사용 합니다.

수정 된 연락처 컨트롤러는 목록 3에 포함 되어 있습니다.

**목록 3-Controllerss\lostfilecs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

목록 3의 Contact 컨트롤러에는 두 개의 생성자가 있습니다. 첫 번째 생성자는 IContactManagerRepository 인터페이스의 구체적인 인스턴스를 두 번째 생성자에 전달 합니다. Contact controller 클래스는 *생성자 종속성 주입*을 사용 합니다.

Entity지 수 리포지토리 클래스는 첫 번째 생성자에만 사용 됩니다. 클래스의 나머지 부분에서는 구체적인 EntityIContactManagerRepository Managerrepository 클래스 대신에 인터페이스를 사용 합니다.

이렇게 하면 나중에 IContactManagerRepository 클래스의 구현을 쉽게 전환할 수 있습니다. EntityDataServicesContactRepository Managerrepository 클래스 대신에 클래스를 사용 하려면 첫 번째 생성자를 수정 하면 됩니다.

생성자 종속성 주입을 통해 Contact controller 클래스를 매우 쉽게 테스트할 수 있습니다. 단위 테스트에서 IContactManagerRepository 클래스의 모의 구현을 전달 하 여 Contact controller를 인스턴스화할 수 있습니다. 종속성 주입의이 기능은 다음 반복에서 연락처 관리자 응용 프로그램에 대 한 단위 테스트를 빌드할 때 매우 중요 합니다.

> [!NOTE] 
> 
> IContactManagerRepository 인터페이스의 특정 구현에서 Contact controller 클래스를 완전히 분리 하려는 경우 StructureMap 또는 Microsoft와 같은 종속성 주입을 지 원하는 프레임 워크를 활용할 수 있습니다. Entity Framework (MEF). 종속성 주입 프레임 워크를 활용 하 여 코드에서 구체적인 클래스를 참조할 필요가 없습니다.

## <a name="creating-a-service-layer"></a>서비스 계층 만들기

유효성 검사 논리는 여전히 목록 3의 수정 된 컨트롤러 클래스에 있는 컨트롤러 논리를 사용 하 여 혼합 된 것을 알 수 있습니다. 데이터 액세스 논리를 격리 하는 것과 같은 이유로 유효성 검사 논리를 격리 하는 것이 좋습니다.

이 문제를 해결 하기 위해 별도의 [*서비스 계층*](http://martinfowler.com/eaaCatalog/serviceLayer.html)을 만들 수 있습니다. 서비스 계층은 컨트롤러와 리포지토리 클래스 사이에 삽입할 수 있는 별도의 계층입니다. 서비스 계층에는 모든 유효성 검사 논리를 포함 하는 비즈니스 논리가 포함 되어 있습니다.

ContactManagerService는 목록 4에 포함 되어 있습니다. Contact controller 클래스의 유효성 검사 논리를 포함 합니다.

**목록 4-Models\ubmanagerserviceservice.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

ContactManagerService에 대 한 생성자에는 ValidationDictionary가 필요 합니다. 서비스 계층은이 ValidationDictionary를 통해 컨트롤러 계층과 통신 합니다. 다음 섹션에서는 데코레이터 패턴에 대해 자세히 설명 합니다.

또한 ContactManagerService는 IContactManagerService 인터페이스를 구현 합니다. 구체적 클래스 대신 인터페이스에 대해 프로그래밍 해야 합니다. Contact Manager 응용 프로그램의 다른 클래스는 ContactManagerService 클래스와 직접 상호 작용 하지 않습니다. 대신 한 가지 예외를 제외 하 고 연락처 관리자 응용 프로그램의 나머지 부분은 IContactManagerService 인터페이스에 대해 프로그래밍 됩니다.

IContactManagerService 인터페이스는 목록 5에 포함 되어 있습니다.

**목록 5-Models\IContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

수정 된 연락처 컨트롤러 클래스는 목록 6에 포함 되어 있습니다. 연락처 컨트롤러는 더 이상 동료 관리자 리포지토리와 상호 작용 하지 않습니다. 대신 연락처 컨트롤러는 연락처 관리자 서비스와 상호 작용 합니다. 각 계층은 다른 계층에서 최대한 많이 격리 됩니다.

**목록 6-Controllers\ContactController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

응용 프로그램은 더 이상 SRP (단일 책임 원칙)의 afoul을 실행 하지 않습니다. 목록 6의 연락처 컨트롤러는 응용 프로그램 실행 흐름을 제어 하는 것 외에는 모든 책임을 제거 했습니다. 모든 유효성 검사 논리가 Contact controller에서 제거 되어 서비스 계층으로 푸시 되었습니다. 모든 데이터베이스 논리가 리포지토리 계층으로 푸시 되었습니다.

## <a name="using-the-decorator-pattern"></a>데코레이터 패턴 사용

컨트롤러 계층에서 서비스 계층을 완전히 분리할 수 있습니다. 원칙적으로 MVC 응용 프로그램에 대 한 참조를 추가할 필요 없이 컨트롤러 계층과 별도의 어셈블리에서 서비스 계층을 컴파일할 수 있어야 합니다.

그러나 서비스 계층은 유효성 검사 오류 메시지를 컨트롤러 계층으로 다시 전달할 수 있어야 합니다. 컨트롤러 및 서비스 계층을 결합 하지 않고 유효성 검사 오류 메시지를 통신 하도록 서비스 계층을 설정 하려면 어떻게 해야 하나요? [데코레이터 패턴](http://en.wikipedia.org/wiki/Decorator_pattern)이라는 소프트웨어 디자인 패턴을 활용할 수 있습니다.

컨트롤러는 ModelStateDictionary 라는 ModelState를 사용 하 여 유효성 검사 오류를 나타냅니다. 따라서 컨트롤러 계층에서 서비스 계층으로 ModelState를 전달 하려고 할 수도 있습니다. 그러나 서비스 계층에서 ModelState를 사용 하면 서비스 계층이 ASP.NET MVC 프레임 워크의 기능에 종속 됩니다. 언젠가, ASP.NET MVC 응용 프로그램 대신 WPF 응용 프로그램에서 서비스 계층을 사용할 수 있기 때문에이는 좋지 않습니다. 이 경우 ModelStateDictionary 클래스를 사용 하기 위해 ASP.NET MVC 프레임 워크를 참조 하지 않으려고 합니다.

데코레이터 패턴을 사용 하면 인터페이스를 구현 하기 위해 기존 클래스를 새 클래스에 래핑할 수 있습니다. 연락처 관리자 프로젝트에는 목록 7에 포함 된 ModelStateWrapper 클래스가 포함 되어 있습니다. ModelStateWrapper 클래스는 목록 8의 인터페이스를 구현 합니다.

**목록 7-Models\Validation\ModelStateWrapper.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**목록 8-Models\Validation\IValidationDictionary.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

목록 5에 대 한 자세한 내용을 확인 하는 경우 연락처 관리자 서비스 계층이 IValidationDictionary 인터페이스를 독점적으로 사용 하는 것을 알 수 있습니다. ModelStateDictionary 클래스에 종속 되지 않은 연락처 관리자 서비스 연락처 컨트롤러에서 담당자 관리자 서비스를 만들 때 컨트롤러는 다음과 같이 ModelState를 래핑합니다.

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>요약

이 반복에서는 연락처 관리자 응용 프로그램에 새 기능을 추가 하지 않았습니다. 이 반복의 목표는 쉽게 유지 관리 하 고 수정할 수 있도록 Contact Manager 응용 프로그램을 리팩터링 하는 것입니다.

먼저 리포지토리 소프트웨어 디자인 패턴을 구현 했습니다. 모든 데이터 액세스 코드를 별도의 연락처 관리자 리포지토리 클래스로 마이그레이션 했습니다.

또한 컨트롤러 논리에서 유효성 검사 논리를 격리 했습니다. 모든 유효성 검사 코드를 포함 하는 별도의 서비스 계층을 만들었습니다. 컨트롤러 계층은 서비스 계층과 상호 작용 하 고 서비스 계층은 리포지토리 계층과 상호 작용 합니다.

서비스 계층을 만들 때 데코레이터 패턴을 활용 하 여 서비스 계층에서 ModelState를 격리 시켰습니다. 서비스 계층에서는 ModelState 대신 IValidationDictionary 인터페이스에 대해 프로그래밍 했습니다.

마지막으로 종속성 주입 패턴 이라는 소프트웨어 디자인 패턴을 활용 했습니다. 이 패턴을 사용 하면 구체적인 클래스 대신 인터페이스 (추상화)를 프로그래밍할 수 있습니다. 또한 종속성 주입 디자인 패턴을 구현 하면 코드를 더 쉽게 테스트할 수 있습니다. 다음 반복에서는 프로젝트에 단위 테스트를 추가 합니다.

> [!div class="step-by-step"]
> [이전](iteration-3-add-form-validation-cs.md)
> [다음](iteration-5-create-unit-tests-cs.md)
