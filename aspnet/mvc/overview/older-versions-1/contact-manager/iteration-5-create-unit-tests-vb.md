---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
title: '반복 #5-단위 테스트 만들기 (VB) | Microsoft Docs'
author: microsoft
description: 다섯 번째 반복에서는 단위 테스트를 추가 하 여 응용 프로그램을 더 쉽게 유지 관리 하 고 수정할 수 있도록 합니다. Microsoft는 데이터 모델 클래스를 모의 하 고 o에 대 한 단위 테스트를 빌드 ...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: c6e5c036-2265-4fa7-a9eb-47f197bdc262
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-vb
msc.type: authoredcontent
ms.openlocfilehash: 4ce1c6224a7e9203ff62f136f4f3a43e4561a904
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78437837"
---
# <a name="iteration-5--create-unit-tests-vb"></a>반복 #5-단위 테스트 만들기 (VB)

[Microsoft](https://github.com/microsoft) 에서

[코드 다운로드](iteration-5-create-unit-tests-vb/_static/contactmanager_5_vb1.zip)

> 다섯 번째 반복에서는 단위 테스트를 추가 하 여 응용 프로그램을 더 쉽게 유지 관리 하 고 수정할 수 있도록 합니다. Microsoft는 데이터 모델 클래스를 모의 하 고 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 빌드 했습니다.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Contact Management ASP.NET MVC 응용 프로그램 빌드 (VB)

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

연락처 관리자 응용 프로그램의 이전 반복에서는 더욱 느슨하게 결합 되도록 응용 프로그램을 리팩터링 했습니다. 응용 프로그램을 별도의 컨트롤러, 서비스 및 리포지토리 계층으로 분리 했습니다. 각 레이어는 인터페이스를 통해 그 아래에 있는 계층과 상호 작용 합니다.

응용 프로그램을 더 쉽게 유지 관리 하 고 수정할 수 있도록 응용 프로그램을 리팩터링 했습니다. 예를 들어 새 데이터 액세스 기술을 사용 해야 하는 경우 컨트롤러 또는 서비스 계층을 건드리지 않고도 리포지토리 계층을 변경할 수 있습니다. 연락처 관리자를 느슨하게 결합 하면 응용 프로그램을 더 탄력적으로 변경할 수 있게 되었습니다.

하지만 연락처 관리자 응용 프로그램에 새 기능을 추가 해야 하는 경우 어떻게 되나요? 또는 버그를 수정 하는 경우 어떻게 되나요? 코드를 작성 하는 것은 슬픈 이지만, 코드를 작성 하는 경우에는 코드를 터치 하는 경우 새 버그를 도입할 위험이 있습니다.

예를 들어, 관리자는 연락처 관리자에 새 기능을 추가 하 라는 메시지를 표시 합니다. 연락처 그룹에 대 한 지원을 추가 하려고 합니다. 사용자가 연락처를 친구, 비즈니스 등의 그룹으로 구성할 수 있도록 하려고 합니다.

이 새로운 기능을 구현 하기 위해 연락처 관리자 응용 프로그램의 3 계층을 모두 수정 해야 합니다. 컨트롤러, 서비스 계층 및 리포지토리에 새 기능을 추가 해야 합니다. 코드 수정을 시작 하는 즉시 이전에 작동 했던 기능을 손상 시킬 위험이 있습니다.

이전 반복과 같이 응용 프로그램을 별도의 계층으로 리팩터링 하는 것이 좋습니다. 응용 프로그램의 나머지 부분을 건드리지 않고도 전체 계층을 변경할 수 있기 때문에 유용 합니다. 그러나 계층 내에서 코드를 쉽게 유지 관리 하 고 수정할 수 있도록 하려면 코드에 대 한 단위 테스트를 만들어야 합니다.

단위 테스트를 사용 하 여 개별 코드 단위를 테스트 합니다. 이러한 코드 단위는 전체 응용 프로그램 계층 보다 작습니다. 일반적으로 단위 테스트를 사용 하 여 코드의 특정 메서드가 원하는 방식으로 동작 하는지 확인 합니다. 예를 들어 ContactManagerService 클래스에서 노출 하는 CreateContact () 메서드에 대 한 단위 테스트를 만들 수 있습니다.

응용 프로그램에 대 한 단위 테스트는 보안 네트워크와 마찬가지로 작동 합니다. 응용 프로그램의 코드를 수정할 때마다 단위 테스트 집합을 실행 하 여 수정으로 인해 기존 기능이 중단 되는지 여부를 확인할 수 있습니다. 단위 테스트를 통해 코드를 쉽게 수정할 수 있습니다. 단위 테스트를 사용 하면 응용 프로그램의 모든 코드를 더 탄력적으로 변경할 수 있습니다.

이 반복에서는 연락처 관리자 응용 프로그램에 단위 테스트를 추가 합니다. 이렇게 하면 다음 반복에서 기존 기능의 중단을 걱정 하지 않고 연락처 그룹을 응용 프로그램에 추가할 수 있습니다.

> [!NOTE] 
> 
> NUnit, xUnit.net 및 MbUnit를 포함 한 다양 한 유닛 테스트 프레임 워크가 있습니다. 이 자습서에서는 Visual Studio에 포함 된 단위 테스트 프레임 워크를 사용 합니다. 그러나 이러한 대체 프레임 워크 중 하나를 쉽게 사용할 수 있습니다.

## <a name="what-gets-tested"></a>테스트 대상

완벽 한 지역에서 모든 코드는 단위 테스트를 통해 적용 됩니다. 완벽 한 세계에서는 완벽 한 보안 네트워크를 사용할 수 있습니다. 응용 프로그램에서 코드 줄을 수정 하 고, 단위 테스트를 실행 하 여 변경 내용이 기존 기능을 중단 하는지 여부를 즉시 파악할 수 있습니다.

그러나 완벽 한 세계에는 살고 있지 않습니다. 실제로 단위 테스트를 작성할 때 비즈니스 논리에 대 한 테스트 작성에 집중 합니다 (예: 유효성 검사 논리). 특히 데이터 액세스 논리 나 뷰 논리에 대 한 단위 테스트를 작성 *하지* 않습니다.

유용 하 게 사용할 수 있도록 단위 테스트는 매우 신속 하 게 실행 해야 합니다. 응용 프로그램에 대해 수백 개의 단위 테스트와 수천 개의 단위 테스트를 쉽게 누적 시킬 수 있습니다. 단위 테스트를 실행 하는 데 시간이 오래 걸리는 경우에는 실행 하지 않는 것이 좋습니다. 즉, 장기 실행 단위 테스트는 일상적인 코딩 용도로는 쓸모가 없습니다.

따라서 일반적으로 데이터베이스와 상호 작용 하는 코드에 대 한 단위 테스트를 작성 하지 않습니다. 라이브 데이터베이스에 대해 수백 개의 단위 테스트를 실행 하면 너무 느릴 수 있습니다. 대신 데이터베이스를 mock 하 고 모의 데이터베이스와 상호 작용 하는 코드를 작성 합니다 (아래 데이터베이스의 mock에 대해 설명).

이와 비슷한 이유로 일반적으로 보기에 대 한 단위 테스트를 작성 하지 않습니다. 뷰를 테스트 하려면 웹 서버를 실행 해야 합니다. 웹 서버를 회전 하는 과정은 상대적으로 느리므로 보기에 대 한 단위 테스트를 만드는 것은 권장 되지 않습니다.

보기에 복잡 한 논리가 포함 된 경우에는 논리를 도우미 메서드로 이동 하는 것을 고려해 야 합니다. 웹 서버를 표시 하지 않고 실행 되는 도우미 메서드에 대 한 단위 테스트를 작성할 수 있습니다.

> [!NOTE] 
> 
> 데이터 액세스 논리 또는 뷰 논리에 대 한 테스트를 작성 하는 것은 단위 테스트를 작성할 때 적절 하지 않습니다. 이러한 테스트는 기능 또는 통합 테스트를 빌드할 때 매우 중요할 수 있습니다.

> [!NOTE] 
> 
> ASP.NET MVC는 Web Forms 뷰 엔진입니다. Web Forms 뷰 엔진은 웹 서버에 종속 되어 있지만 다른 뷰 엔진은 그렇지 않을 수도 있습니다.

## <a name="using-a-mock-object-framework"></a>모의 개체 프레임 워크 사용

단위 테스트를 작성할 때는 대부분 모의 개체 프레임 워크를 사용 해야 합니다. 모의 개체 프레임 워크를 사용 하면 응용 프로그램의 클래스에 대해 모의 개체와 스텁을 만들 수 있습니다.

예를 들어 모의 개체 프레임 워크를 사용 하 여 리포지토리 클래스의 모의 버전을 생성할 수 있습니다. 이렇게 하면 단위 테스트에서 실제 리포지토리 클래스 대신 모의 리포지토리 클래스를 사용할 수 있습니다. 모의 리포지토리를 사용 하면 단위 테스트를 실행할 때 데이터베이스 코드를 실행 하지 않아도 됩니다.

Visual Studio에는 모의 개체 프레임 워크가 포함 되어 있지 않습니다. 그러나 .NET framework에서 사용할 수 있는 상용 및 오픈 소스 모의 개체 프레임 워크는 다음과 같이 여러 가지가 있습니다.

1. Moq-이 프레임 워크는 오픈 소스 BSD 라이선스에서 사용할 수 있습니다. [https://code.google.com/p/moq/](https://code.google.com/p/moq/)에서 moq를 다운로드할 수 있습니다.
2. Rhino 모의-이 프레임 워크는 오픈 소스 BSD 라이선스에서 사용할 수 있습니다. [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)에서 Rhino mock를 다운로드할 수 있습니다.
3. Typemock Isolator-상용 프레임 워크입니다. [http://www.typemock.com/](http://www.typemock.com/)에서 평가판 버전을 다운로드할 수 있습니다.

이 자습서에서는 Moq를 사용 하기로 결정 했습니다. 그러나 Rhino 모의 또는 Typemock Isolator를 사용 하 여 연락처 관리자 응용 프로그램에 대 한 모의 개체를 쉽게 만들 수 있습니다.

Moq를 사용 하려면 먼저 다음 단계를 완료 해야 합니다.

1. .
2. 다운로드의 압축을 풀려면 먼저 파일을 마우스 오른쪽 단추로 클릭 하 고 **차단 해제** 라는 레이블이 지정 된 단추를 클릭 해야 합니다 (그림 1 참조).
3. 다운로드의 압축을 풉니다.
4. 메뉴 옵션 **프로젝트, 참조 추가** 를 선택 하 여 **참조 추가** 대화 상자를 열고 moq 어셈블리에 대 한 참조를 테스트 프로젝트에 추가 합니다. 찾아보기 탭에서 Moq의 압축을 푼 폴더로 이동한 후 Moq .dll 어셈블리를 선택 합니다. **확인** 단추를 클릭 합니다 (그림 2 참조).

[![차단 해제 Moq](iteration-5-create-unit-tests-vb/_static/image1.jpg)](iteration-5-create-unit-tests-vb/_static/image1.png)

**그림 01**: 차단 해제 moq ([전체 크기 이미지를 보려면 클릭](iteration-5-create-unit-tests-vb/_static/image2.png))

[Moq를 추가한 후 참조 ![](iteration-5-create-unit-tests-vb/_static/image2.jpg)](iteration-5-create-unit-tests-vb/_static/image3.png)

**그림 02**: moq를 추가한 후 참조 ([전체 크기 이미지를 보려면 클릭](iteration-5-create-unit-tests-vb/_static/image4.png))

## <a name="creating-unit-tests-for-the-service-layer"></a>서비스 계층에 대 한 단위 테스트 만들기

연락처 관리자 응용 프로그램의 서비스 계층에 대 한 단위 테스트 집합을 만들어 시작 해 보겠습니다. 이러한 테스트를 사용 하 여 유효성 검사 논리를 확인 합니다.

프로젝트 관리자 프로젝트에서 모델 이라는 새 폴더를 만듭니다. 그런 다음, 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 새 테스트를**선택 합니다. 그림 3에 표시 된 **새 테스트 추가** 대화 상자가 나타납니다. **단위 테스트** 템플릿을 선택 하 고 새 테스트 ContactManagerServiceTest의 이름을로 선택 합니다. **확인** 단추를 클릭 하 여 테스트 프로젝트에 새 테스트를 추가 합니다.

> [!NOTE] 
> 
> 일반적으로 테스트 프로젝트의 폴더 구조를 ASP.NET MVC 프로젝트의 폴더 구조와 일치 시 키 려 고 합니다. 예를 들어 컨트롤러 테스트를 컨트롤러 폴더에 놓고 모델 테스트를 모델 폴더에 저장 하는 등의 방법을 사용할 수 있습니다.

[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-vb/_static/image3.jpg)](iteration-5-create-unit-tests-vb/_static/image5.png)

**그림 03**: Models\ContactManagerServiceTest.cs ([전체 크기 이미지를 보려면 클릭](iteration-5-create-unit-tests-vb/_static/image6.png))

처음에는 ContactManagerService 클래스에서 노출 하는 CreateContact () 메서드를 테스트 하려고 합니다. 다음 다섯 가지 테스트를 만듭니다.

- CreateContact ()-유효한 연락처가 메서드에 전달 될 때 CreateContact ()에서 true 값을 반환 하는지 테스트 합니다.
- CreateContactRequiredFirstName ()-이름이 누락 된 연락처가 CreateContact () 메서드에 전달 되 면 오류 메시지가 모델 상태에 추가 되는지 테스트 합니다.
- CreateContactRequiredLastName ()-마지막 이름이 누락 된 연락처가 CreateContact () 메서드에 전달 될 때 오류 메시지가 모델 상태에 추가 되는지 테스트 합니다.
- CreateContactInvalidPhone ()-전화 번호가 잘못 된 연락처가 CreateContact () 메서드에 전달 될 때 오류 메시지가 모델 상태에 추가 되는지 테스트 합니다.
- CreateContactInvalidEmail ()-잘못 된 전자 메일 주소가 포함 된 연락처가 CreateContact () 메서드에 전달 될 때 오류 메시지가 모델 상태에 추가 되는지 테스트 합니다.

첫 번째 테스트는 유효한 연락처가 유효성 검사 오류를 생성 하지 않는지 확인 합니다. 나머지 테스트는 각 유효성 검사 규칙을 검사 합니다.

이러한 테스트에 대 한 코드는 목록 1에 포함 되어 있습니다.

**목록 1-Models\ContactManagerServiceTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample1.vb)]

목록 1에서 Contact 클래스를 사용 하므로 테스트 프로젝트에 Microsoft Entity Framework에 대 한 참조를 추가 해야 합니다. System.object 어셈블리에 대 한 참조를 추가 합니다.

목록 1에는 [TestInitialize] 특성으로 데코레이팅된 Initialize () 라는 메서드가 있습니다. 이 메서드는 각 단위 테스트를 실행 하기 전에 자동으로 호출 됩니다 (각 단위 테스트 바로 전에 5 번 호출 됨). Initialize () 메서드는 다음 코드 줄을 사용 하 여 모의 리포지토리를 만듭니다.

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample2.vb)]

이 코드 줄에서는 Moq 프레임 워크를 사용 하 여 IContactManagerRepository 인터페이스에서 모의 리포지토리를 생성 합니다. 각 단위 테스트를 실행할 때 데이터베이스에 액세스 하지 못하도록 하기 위해 실제 EntityContactManagerRepository 대신 모의 리포지토리가 사용 됩니다. 모의 리포지토리는 IContactManagerRepository 인터페이스의 메서드를 구현 하지만 실제로는 아무것도 수행 하지 않습니다.

> [!NOTE] 
> 
> Moq 프레임 워크를 사용 하는 경우 \_mockRepository \_mockRepository 간의 차이가 있습니다. 이전에는 모의 리포지토리의 동작 방식을 지정 하는 메서드가 포함 된 모의 (Of IContactManagerRepository) 클래스를 참조 합니다. 후자는 IContactManagerRepository 인터페이스를 구현 하는 실제 모의 리포지토리를 나타냅니다.

모의 리포지토리는 ContactManagerService 클래스의 인스턴스를 만들 때 Initialize () 메서드에서 사용 됩니다. 모든 개별 단위 테스트는 ContactManagerService 클래스의이 인스턴스를 사용 합니다.

목록 1에는 각 단위 테스트에 해당 하는 5 개의 메서드가 있습니다. 이러한 각 메서드는 [TestMethod] 특성으로 데코 레이트 됩니다. 단위 테스트를 실행 하면이 특성이 있는 메서드가 호출 됩니다. 즉, [TestMethod] 특성으로 데코레이팅된 메서드는 단위 테스트입니다.

CreateContact () 이라는 첫 번째 단위 테스트는 Contact 클래스의 올바른 인스턴스가 메서드에 전달 될 때 CreateContact () 호출에서 true 값을 반환 하는지 확인 합니다. 테스트는 Contact 클래스의 인스턴스를 만들고, CreateContact () 메서드를 호출 하 고, CreateContact ()이 true 값을 반환 하는지 확인 합니다.

나머지 테스트는 잘못 된 연락처를 사용 하 여 CreateContact () 메서드를 호출할 때 메서드가 false를 반환 하 고 예상 유효성 검사 오류 메시지가 모델 상태에 추가 되는지 확인 합니다. 예를 들어 CreateContactRequiredFirstName () 테스트는 FirstName 속성에 대해 빈 문자열을 사용 하 여 Contact 클래스의 인스턴스를 만듭니다. 그런 다음 CreateContact () 메서드가 잘못 된 연락처를 사용 하 여 호출 됩니다. 마지막으로 테스트에서는 CreateContact ()이 false를 반환 하 고 해당 모델 상태에 "First name required required" 라는 예상 유효성 검사 오류 메시지가 포함 되어 있는지 확인 합니다.

**테스트, 실행, 솔루션의 모든 테스트 (CTRL + R, A)** 메뉴 옵션을 선택 하 여 목록 1에서 단위 테스트를 실행할 수 있습니다. 테스트 결과가 테스트 결과 창에 표시 됩니다 (그림 4 참조).

[![테스트 결과](iteration-5-create-unit-tests-vb/_static/image4.jpg)](iteration-5-create-unit-tests-vb/_static/image7.png)

**그림 04**: 테스트 결과 ([전체 크기 이미지를 보려면 클릭](iteration-5-create-unit-tests-vb/_static/image8.png))

## <a name="creating-unit-tests-for-controllers"></a>컨트롤러에 대 한 단위 테스트 만들기

ASP.NET MVC 응용 프로그램은 사용자 상호 작용의 흐름을 제어 합니다. 컨트롤러를 테스트할 때 컨트롤러에서 올바른 작업 결과 및 뷰 데이터를 반환 하는지 여부를 테스트 하려고 합니다. 또한 컨트롤러가 예상 대로 모델 클래스와 상호 작용 하는지 여부를 테스트할 수 있습니다.

예를 들어 목록 2에는 Contact controller Create () 메서드에 대 한 두 개의 단위 테스트가 포함 되어 있습니다. 첫 번째 단위 테스트는 올바른 연락처가 Create () 메서드에 전달 될 때 Create () 메서드가 인덱스 작업으로 리디렉션하는 지 확인 합니다. 즉, 유효한 연락처를 전달 하는 경우 Create () 메서드는 인덱스 작업을 나타내는 RedirectToRouteResult를 반환 해야 합니다.

컨트롤러 계층을 테스트할 때 연락처 관리자 서비스 계층을 테스트 하 고 싶지 않습니다. 따라서 Initialize 메서드에서 다음 코드를 사용 하 여 서비스 계층을 모의 합니다.

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample3.vb)]

Createcode Contact () 단위 테스트에서 다음 코드 줄을 사용 하 여 service layer CreateContact () 메서드를 호출 하는 동작을 mock 했습니다.

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample4.vb)]

이 코드 줄은 CreateContact () 메서드가 호출 될 때 모의 연락처 관리자 서비스가 값 true를 반환 하도록 합니다. 서비스 계층의 mock를 통해 서비스 계층에서 코드를 실행할 필요 없이 컨트롤러의 동작을 테스트할 수 있습니다.

두 번째 단위 테스트는 잘못 된 연락처가 메서드에 전달 될 때 Create () 작업이 만들기 뷰를 반환 하는지 확인 합니다. Service layer CreateContact () 메서드는 다음 코드 줄을 사용 하 여 false 값을 반환 합니다.

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample5.vb)]

Create () 메서드가 정상적으로 동작 하는 경우 서비스 계층이 false 값을 반환할 때 Create 뷰를 반환 해야 합니다. 그러면 컨트롤러는 만들기 보기에 유효성 검사 오류 메시지를 표시 하 고 사용자가 잘못 된 연락처 속성을 수정할 수 있습니다.

컨트롤러에 대 한 단위 테스트를 빌드하려면 컨트롤러 작업에서 명시적 뷰 이름을 반환 해야 합니다. 예를 들어 다음과 같이 뷰를 반환 하지 마십시오.

반환 뷰 ()

대신 다음과 같이 뷰를 반환 합니다.

반환 뷰 ("만들기")

뷰를 반환할 때 명시적이 아닌 경우 ViewName 속성은 빈 문자열을 반환 합니다.

**목록 2-Controllers\ContactControllerTest.vb**

[!code-vb[Main](iteration-5-create-unit-tests-vb/samples/sample6.vb)]

## <a name="summary"></a>요약

이 반복에서는 연락처 관리자 응용 프로그램에 대 한 단위 테스트를 만들었습니다. 언제 든 지 이러한 단위 테스트를 실행 하 여 응용 프로그램이 필요한 방식으로 작동 하는지 확인할 수 있습니다. 단위 테스트는 나중에 응용 프로그램을 안전 하 게 수정할 수 있도록 응용 프로그램에 대 한 안전한 네트워크 역할을 합니다.

두 개의 단위 테스트 집합을 만들었습니다. 먼저 서비스 계층에 대 한 단위 테스트를 만들어 유효성 검사 논리를 테스트 했습니다. 다음으로 컨트롤러 계층에 대 한 단위 테스트를 만들어 흐름 제어 논리를 테스트 했습니다. 서비스 계층을 테스트할 때 리포지토리 계층의 mock를 통해 리포지토리 계층에서 서비스 계층에 대 한 테스트를 격리 했습니다. 컨트롤러 계층을 테스트할 때 서비스 계층의 mock를 통해 컨트롤러 계층에 대 한 테스트를 격리 했습니다.

다음 반복에서는 연락처 그룹을 지원 하도록 연락처 관리자 응용 프로그램을 수정 합니다. 테스트 기반 개발 이라는 소프트웨어 디자인 프로세스를 사용 하 여 응용 프로그램에이 새로운 기능을 추가 합니다.

> [!div class="step-by-step"]
> [이전](iteration-4-make-the-application-loosely-coupled-vb.md)
> [다음](iteration-6-use-test-driven-development-vb.md)
