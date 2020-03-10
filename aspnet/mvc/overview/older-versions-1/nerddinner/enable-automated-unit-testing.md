---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: 자동화 된 단위 테스트 사용 | Microsoft Docs
author: microsoft
description: 12 단계는 팀의 내부 기능을 확인 하 고 변경할 수 있는 신뢰도를 제공 하는 자동화 된 단위 테스트 제품군을 개발 하는 방법을 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 09a7aa186605a6cce48ee94028425ded957c00d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78435593"
---
# <a name="enable-automated-unit-testing"></a>자동화된 유닛 테스트 사용

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 12 단계입니다.
> 
> 12 단계에서는 나머지 응용 프로그램의 기능을 확인 하 고 나중에 응용 프로그램을 변경 하 고 개선할 수 있는 신뢰도를 제공 하는 자동화 된 단위 테스트 제품군을 개발 하는 방법을 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner Step 12: 유닛 테스트

팀의 내부 기능을 확인 하 고 나중에 응용 프로그램을 변경 하 고 향상 시킬 수 있는 신뢰도를 제공 하는 자동화 된 단위 테스트 모음을 개발 해 보겠습니다.

### <a name="why-unit-test"></a>단위 테스트 이유

한 동안 작업 하는 경우 작업 중인 응용 프로그램에 대 한 정보를 갑자기 플래시 하 게 됩니다. 응용 프로그램을 크게 개선 하기 위해 구현할 수 있는 변경 내용이 있다는 것을 알게 될 것입니다. 코드를 정리 하거나, 새 기능을 추가 하거나, 버그를 수정 하는 리팩터링할 수 있습니다.

컴퓨터에 도착할 때 표시 되는 질문은 "안전 하 게 개선 하는 방법은 무엇입니까?"입니다. 변경 작업으로 인해 부작용이 발생 하는 경우 어떻게 되나요? 변경 작업은 간단 하 고 구현 하는 데 몇 분 밖에 걸리지 않지만 모든 응용 프로그램 시나리오를 수동으로 테스트 하는 데 시간이 소요 되는 경우는 어떻게 되나요? 시나리오를 다루며 손상 된 응용 프로그램이 프로덕션 환경으로 전환 되는 경우는 어떻게 되나요? 이 기능을 개선 하는 것은 정말 모든 노력이 필요 한가요?

자동화 된 단위 테스트는 응용 프로그램을 지속적으로 개선 하 고 작업 중인 코드의 부담을 피할 수 있는 보안 네트워크를 제공할 수 있습니다. 기능을 신속 하 게 확인 하는 자동화 된 테스트를 통해 안전 하 게 코드를 작성 하 고, 다른 방법으로는 편안 하 게 개선할 수 있습니다. 또한 더 쉽게 유지 관리 되 고 수명이 긴 솔루션을 만들 수 있습니다 .이를 통해 투자 수익률을 크게 높일 수 있습니다.

ASP.NET MVC 프레임 워크를 사용 하면 손쉽게 단위 테스트 응용 프로그램 기능을 만들 수 있습니다. 또한 테스트 기반 개발을 가능 하 게 하는 TDD (테스트 기반 개발) 워크플로를 사용할 수 있습니다.

### <a name="nerddinnertests-project"></a>NerdDinner.Tests Project

이 자습서의 시작 부분에서 동료 Ddinner 응용 프로그램을 만들 때 응용 프로그램 프로젝트와 함께 사용할 단위 테스트 프로젝트를 만들지 여부를 묻는 대화 상자가 표시 되었습니다.

![](enable-automated-unit-testing/_static/image1.png)

"예, 단위 테스트 프로젝트 만들기" 라디오 단추를 선택 하 여 솔루션에 "팀 간 Ddinner. 테스트" 프로젝트를 추가 했습니다.

![](enable-automated-unit-testing/_static/image2.png)

이 프로젝트는 응용 프로그램 기능을 확인 하는 자동화 된 테스트를 쉽게 추가할 수 있도록 해 주는 응용 프로그램 프로젝트 어셈블리를 참조 합니다.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>Dinner Model 클래스에 대 한 단위 테스트 만들기

모델 계층을 빌드할 때 만든 Dinner class를 확인 하는 테스트 프로젝트에 일부 테스트를 추가 해 보겠습니다.

먼저 모델 관련 테스트를 수행할 "모델" 이라는 테스트 프로젝트 내에 새 폴더를 만듭니다. 그런 다음 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가&gt;새 테스트** 메뉴 명령을 선택 합니다. 그러면 "새 테스트 추가" 대화 상자가 표시 됩니다.

"단위 테스트"를 만들고 이름을 "DinnerTest.cs"로 이름을 선택 합니다.

![](enable-automated-unit-testing/_static/image3.png)

"확인" 단추를 클릭 하면 Visual Studio에서 DinnerTest.cs 파일을 프로젝트에 추가 하 고 엽니다.

![](enable-automated-unit-testing/_static/image4.png)

기본 Visual Studio 단위 테스트 템플릿에는 약간의 상용구이 포함 되어 있습니다. 아래 코드를 포함 하도록 정리 하겠습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

위의 DinnerTest 클래스에 대 한 [TestClass] 특성은 테스트를 포함 하는 클래스로, 그리고 선택적인 테스트 초기화 및 해체 코드를 식별 합니다. [TestMethod] 특성을 포함 하는 공용 메서드를 추가 하 여 내에서 테스트를 정의할 수 있습니다.

Dinner class를 실행 하는 두 테스트 중 첫 번째 테스트는 다음과 같습니다. 첫 번째 테스트는 모든 속성을 올바르게 설정 하지 않고 새 Dinner를 만든 경우 Dinner is가 유효 하지 않은지 확인 합니다. 두 번째 테스트는 Dinner의 모든 속성이 유효한 값으로 설정 된 경우 Dinner is가 유효한 지 확인 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

테스트 이름은 매우 명확 하 고 자세한 정보를 제공 한다는 것을 알 수 있습니다. 수백 또는 수천 개의 작은 테스트를 만들 수 있기 때문에이 작업을 수행 하 고, 각각의 의도 및 동작을 쉽게 확인할 수 있도록 합니다 (특히 test runner에서 오류 목록을 살펴볼 때). 테스트 이름을 테스트 하는 기능 후에 이름을 지정 해야 합니다. 위에서 "명사\_는 동사를\_명명 패턴을 사용 합니다.

"정렬, Act, 어설션"을 나타내는 "AAA" 테스트 패턴을 사용 하 여 테스트를 구성할 것입니다.

- 정렬: 테스트 중인 단위를 설정 합니다.
- Act: 테스트 및 캡처 결과에서 단위를 실행 합니다.
- Assert: 동작을 확인 합니다.

테스트를 작성할 때 개별 테스트에서 너무 많은 작업을 수행 하는 것을 방지 하려고 합니다. 대신 각 테스트는 단일 개념도 확인 해야 하며,이를 통해 오류 원인을 보다 쉽게 파악할 수 있습니다. 적절 한 지침은 각 테스트에 대해 단일 assert 문만을 시도 하는 것입니다. 테스트 메서드에 둘 이상의 assert 문이 있는 경우 모두 동일한 개념을 테스트 하는 데 사용 되는지 확인 합니다. 확실 하지 않은 경우 다른 테스트를 수행 합니다.

### <a name="running-tests"></a>테스트 실행 중

Visual Studio 2008 Professional (이상 버전)에는 IDE 내에서 Visual Studio 단위 테스트 프로젝트를 실행 하는 데 사용할 수 있는 기본 제공 test runner가 포함 되어 있습니다. **테스트-&gt;실행-솔루션 메뉴에서 모든 테스트를&gt;** 하거나 Ctrl R, A를 입력 하 여 모든 단위 테스트를 실행할 수 있습니다. 또는 특정 테스트 클래스 또는 테스트 메서드 내에 커서를 배치 하 고 **현재 상황에 맞는 메뉴 명령의 테스트&gt;실행&gt;테스트** 를 사용 하거나 Ctrl R, t를 입력 하 여 단위 테스트의 하위 집합을 실행할 수 있습니다.

이제는 Dinnertest 클래스 내에 커서를 놓고 "Ctrl R, T"를 입력 하 여 방금 정의한 두 테스트를 실행 합니다. 이 작업을 수행 하면 Visual Studio 내에 "테스트 결과" 창이 표시 되 고 여기에 나열 된 테스트 실행 결과가 표시 됩니다.

![](enable-automated-unit-testing/_static/image5.png)

*참고: VS 테스트 결과 창에는 기본적으로 클래스 이름 열이 표시 되지 않습니다. 테스트 결과 창 내에서 마우스 오른쪽 단추를 클릭 하 고 열 추가/제거 메뉴 명령을 사용 하 여이를 추가할 수 있습니다.*

두 개의 테스트는 실행 하는 데 1 초 동안만 소요 되었으며 두 테스트 모두 통과 한 것을 볼 수 있습니다. 이제 특정 규칙 유효성 검사를 확인 하는 추가 테스트를 작성 하 고, Dinner class에 추가 된 두 개의 도우미 메서드 (IsUserHost () 및 isuserhost ())를 포함 하 여이를 확장 하 고 확장할 수 있습니다. Dinner class에 대해 이러한 모든 테스트를 수행 하면 나중에 새 비즈니스 규칙 및 유효성 검사를 더 쉽고 안전 하 게 추가할 수 있습니다. 저녁에 새 규칙 논리를 추가 하 고 몇 초 내에 이전 논리 기능이 손상 되지 않았는지 확인할 수 있습니다.

설명 테스트 이름을 사용 하면 각 테스트에서 확인 하는 내용을 쉽게 파악할 수 있습니다. **도구-&gt;옵션** 메뉴 명령을 사용 하 여 테스트 도구-&gt;테스트 실행 구성 화면을 열고 "실패 했거나 결과가 불충분 한 단위 테스트 결과를 두 번 클릭 하 여 테스트의 실패 지점 표시" 확인란을 선택 하는 것이 좋습니다. 이렇게 하면 테스트 결과 창에서 오류를 두 번 클릭 하 고 assert 실패로 바로 이동할 수 있습니다.

### <a name="creating-dinnerscontroller-unit-tests"></a>DinnersController 단위 테스트 만들기

이제는 DinnersController 기능을 확인 하는 단위 테스트를 만들어 보겠습니다. 먼저 테스트 프로젝트 내에서 "컨트롤러" 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가-&gt;새 테스트** 메뉴 명령을 선택 합니다. "단위 테스트"를 만들고 이름을 "DinnersControllerTest.cs"로 표시 합니다.

여기서는 두 가지 테스트 메서드를 만들어, 여기서는 d Innerscontroller에서 Details () 동작 메서드를 확인 합니다. 첫 번째는 기존 저녁이 요청 될 때 뷰가 반환 되는지 확인 합니다. 두 번째는 존재 하지 않는 Dinner if가 요청 될 때 "NotFound" 뷰가 반환 되는지 확인 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

위의 코드는 정리를 컴파일합니다. 그러나 테스트를 실행할 때 모두 실패 합니다.

![](enable-automated-unit-testing/_static/image6.png)

오류 메시지를 살펴보면, microsoft의 microsoft 리포지토리 클래스에서 데이터베이스에 연결할 수 없기 때문에 테스트가 실패 한 이유가 표시 됩니다. Microsoft의 팀 간 Ddinner 응용 프로그램은 로컬 SQL Server Express 파일에 대 한 연결 문자열을 사용 하 고 있습니다 .이 파일은 NerdDinner 응용 프로그램 프로젝트의 \App\_Data 디렉터리에 있습니다. 그와 같은 이유 때문에 테스트 프로젝트가 컴파일되고 다른 디렉터리에서 실행 되며, 응용 프로그램 프로젝트는 연결 문자열의 상대 경로 위치가 올바르지 않습니다.

SQL Express 데이터베이스 파일을 테스트 프로젝트에 복사한 다음 테스트 프로젝트의 App.config에서 적절 한 테스트 연결 문자열을 추가 하 여이 문제를 해결할 *수 있습니다* . 이렇게 하면 위 테스트가 차단 해제 되 고 실행 됩니다.

그러나 실제 데이터베이스를 사용 하는 단위 테스트 코드는 여러 가지 문제를 해결 합니다. 특히 다음에 대한 내용을 설명합니다.

- 단위 테스트의 실행 시간을 크게 줄일 수 있습니다. 테스트를 실행 하는 데 소요 되는 시간이 길수록 자주 실행 하는 것이 거의 없습니다. 단위 테스트를 몇 초 내에 실행 하 고 프로젝트를 컴파일할 때 자연스럽 게 사용할 수 있도록 하는 것이 좋습니다.
- 테스트 내에서 설정 및 정리 논리를 복잡 하 게 합니다. 각 단위 테스트를 격리 하 고 다른 사용자와 독립적으로 (파생 작업이 나 종속성 없이) 할 수 있습니다. 실제 데이터베이스에 대해 작업 하는 경우 상태를 염두에 하 고 테스트 간에 다시 설정 해야 합니다.

이러한 문제를 해결 하 고 테스트와 함께 실제 데이터베이스를 사용할 필요가 없도록 하는 "종속성 주입" 이라는 디자인 패턴을 살펴보겠습니다.

### <a name="dependency-injection"></a>종속성 주입

현재, 이제는 DinnersController가 Einnerrepository 클래스와 긴밀 하 게 "결합" 됩니다. "결합"은 클래스가 다른 클래스를 사용 하 여 작업 하기 위해 명시적으로 사용 하는 상황을 나타냅니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

데이터베이스에 대 한 액세스 권한이 필요한 경우에는 데이터베이스에 대 한 액세스 권한이 필요 하기 때문에, d Innerscontroller 클래스에 대 한 데이터베이스를 포함 하는 데는 데이터베이스에 대 한 액세스 권한이 필요 합니다.

"종속성 주입" 이라는 디자인 패턴을 사용 하 여이 문제를 해결할 수 있습니다. 여기에는 종속성 (데이터 액세스를 제공 하는 리포지토리 클래스 등)이이를 사용 하는 클래스 내에서 더 이상 암시적으로 생성 되지 않는 방법일 수 있습니다. 대신 생성자 인수를 사용 하 여 종속성을 사용 하는 클래스에 종속성을 명시적으로 전달할 수 있습니다. 인터페이스를 사용 하 여 종속성을 정의 하는 경우에는 단위 테스트 시나리오에 대 한 "가짜" 종속성 구현을 유연 하 게 전달할 수 있습니다. 이렇게 하면 실제로 데이터베이스에 액세스 하지 않아도 되는 테스트 관련 종속성 구현을 만들 수 있습니다.

이 작업을 수행 하는 것을 확인 하기 위해, DinnersController를 사용 하 여 종속성 주입을 구현 해 보겠습니다.

#### <a name="extracting-an-idinnerrepository-interface"></a>IDinnerRepository 인터페이스 추출

첫 번째 단계는 컨트롤러에서 Dinners를 검색 하 고 업데이트 하는 데 필요한 리포지토리 계약을 캡슐화 하는 새 IDinnerRepository 인터페이스를 만드는 것입니다.

\Stoml 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **추가-&gt;새 항목** 메뉴 명령을 선택 하 고 IDinnerRepository.cs 이라는 새 인터페이스를 만들어이 인터페이스 계약을 수동으로 정의할 수 있습니다.

또는 기본 제공 Visual Studio Professional (이상 버전)에 기본 제공 되는 리팩터링 도구를 사용 하 여 기존 DinnerRepository 클래스에서 인터페이스를 자동으로 추출 하 고 만들 수 있습니다. VS를 사용 하 여이 인터페이스를 추출 하려면, 차원 클래스의 텍스트 편집기에 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 **리팩터링-&gt;인터페이스 추출** 메뉴 명령을 선택 하면 됩니다.

![](enable-automated-unit-testing/_static/image7.png)

그러면 "인터페이스 추출" 대화 상자가 시작 되 고 만들 인터페이스의 이름을 묻는 메시지가 표시 됩니다. 기본적으로 IDinnerRepository로 설정 되 고 기존 DinnerRepository 클래스에서 모든 public 메서드를 자동으로 선택 하 여 인터페이스에 추가 합니다.

![](enable-automated-unit-testing/_static/image8.png)

"확인" 단추를 클릭 하면 Visual Studio에서 응용 프로그램에 새 IDinnerRepository 인터페이스를 추가 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

그리고 기존 DinnerRepository 클래스는 인터페이스를 구현 하도록 업데이트 됩니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>생성자 삽입을 지원 하도록 DinnersController를 업데이트 하는 중

이제 새 인터페이스를 사용 하도록 DinnersController 클래스를 업데이트 합니다.

현재는 "' d i n 리포지토리" 필드가 항상 다음의 경우에는

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

"DinnerRepository" 필드가 DinnerRepository 대신 IDinnerRepository 형식으로 변경 됩니다. 그런 다음 두 개의 public DinnersController 생성자를 추가 합니다. 생성자 중 하나를 사용 하 여 IDinnerRepository를 인수로 전달할 수 있습니다. 다른는 기존 DinnerRepository 구현을 사용 하는 기본 생성자입니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

ASP.NET MVC는 기본적으로 기본 생성자를 사용 하 여 컨트롤러 클래스를 만들기 때문에 런타임 시의 DinnersController는 계속 해 서 d Innerrepository 클래스를 사용 하 여 데이터 액세스를 수행 합니다.

그러나 이제는 단위 테스트를 업데이트 하 여 매개 변수 생성자를 사용 하 여 "가짜" 저녁 리포지토리 구현을 전달할 수 있습니다. 이 "가짜" 저녁 리포지토리에는 실제 데이터베이스에 액세스할 필요가 없으며 대신 메모리 내 샘플 데이터를 사용 합니다.

#### <a name="creating-the-fakedinnerrepository-class"></a>FakeDinnerRepository 클래스 만들기

FakeDinnerRepository 클래스를 만들어 보겠습니다.

먼저 Fakes에서 "" 디렉터리를 만든 다음 프로젝트에 새 FakeDinnerRepository 클래스를 추가 합니다. 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가-&gt;새 클래스**를 선택 합니다.

![](enable-automated-unit-testing/_static/image9.png)

FakeDinnerRepository 클래스가 IDinnerRepository 인터페이스를 구현 하도록 코드를 업데이트 합니다. 그런 다음이를 마우스 오른쪽 단추로 클릭 하 고 "interface IDinnerRepository 구현" 상황에 맞는 메뉴 명령을 선택할 수 있습니다.

![](enable-automated-unit-testing/_static/image10.png)

이렇게 하면 Visual Studio에서 기본 "스텁 아웃" 구현을 사용 하 여 FakeDinnerRepository 클래스에 모든 IDinnerRepository 인터페이스 멤버를 자동으로 추가 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

그런 다음 FakeDinnerRepository 구현을 업데이트 하 여이를 생성자 인수로 전달 된 Dinner&gt; collection&lt;메모리 내 목록에서 사용할 수 있습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

이제 데이터베이스를 필요로 하지 않는 가짜 IDinnerRepository 구현을 사용할 수 있으며, 대신 Dinner objects의 메모리 내 목록을 사용할 수 있습니다.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>단위 테스트에서 FakeDinnerRepository 사용

데이터베이스를 사용할 수 없기 때문에 이전에 실패 한 DinnersController 단위 테스트로 돌아가 보겠습니다. 아래 코드를 사용 하 여 샘플 메모리 내 저녁 데이터로 채워진 FakeDinnerRepository를 사용 하도록 테스트 메서드를 업데이트할 수 있습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

그리고 이제 이러한 테스트를 실행할 때 다음 두 테스트를 모두 통과 합니다.

![](enable-automated-unit-testing/_static/image11.png)

무엇 보다도 실행 하는 데는 1 초 정도 걸리며 복잡 한 설정/정리 논리가 필요 하지 않습니다. 이제 실제 데이터베이스에 연결할 필요 없이 모든 DinnersController 작업 메서드 코드 (목록, 페이징, 세부 정보, 만들기, 업데이트 및 삭제 포함)를 단위 테스트할 수 있습니다.

| **측면 토픽: 종속성 주입 프레임 워크** |
| --- |
| 수동 종속성 주입 (예: 위)을 수행 하는 것은 잘 작동 하지만 응용 프로그램의 종속성 및 구성 요소 수가 늘어나면 유지 관리가 어려워집니다. 더 많은 종속성 관리 유연성을 제공 하는 데 도움이 되는 .NET에 대 한 몇 가지 종속성 주입 프레임 워크가 있습니다. 이러한 프레임 워크 (IoC (제어 반전) 컨테이너 라고도 함)는 런타임에 개체에 대 한 종속성을 지정 하 고 전달 하는 추가 수준의 구성 지원을 가능 하 게 하는 메커니즘을 제공 합니다 (가장 자주 생성자 삽입 사용). ). .NET의 더 인기 있는 OSS 종속성 주입/IOC 프레임 워크에는 AutoFac, Ninject, Spring.NET, StructureMap 및 Windsor가 포함 됩니다. ASP.NET MVC는 개발자가 컨트롤러의 확인 및 인스턴스화에 참여할 수 있게 해 주는 확장성 Api를 제공 하며,이 프로세스 내에서 종속성 주입/IoC 프레임 워크가 완벽 하 게 통합 될 수 있도록 합니다. DI/IOC 프레임 워크를 사용 하 여이 기본 생성자를 DinnersController에서 제거할 수 있습니다 .이 생성자는이를 통해 it와 해당 계층 간의 결합을 완전히 제거 합니다. Microsoft는 동료 Ddinner 응용 프로그램에서 종속성 주입/IOC 프레임 워크를 사용 하지 않습니다. 하지만, 그와 같은 경우에는이를 고려할 수 있습니다. |

### <a name="creating-edit-action-unit-tests"></a>편집 작업 단위 테스트 만들기

이제는 DinnersController의 편집 기능을 확인 하는 단위 테스트를 만들어 보겠습니다. 먼저 HTTP-GET 버전의 편집 작업을 테스트 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

올바른 dinner on이 요청 될 때 다음을 수행 하 여 d Innerformviewmodel 개체에 의해 지원 되는 뷰가 다시 렌더링 되는지 확인 하는 테스트를 만듭니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

그러나 테스트를 실행할 때 Edit 메서드가 User.Identity.Name 속성에 액세스 하 여 IsHostedBy () 검사를 수행 하는 경우 null 참조 예외가 throw 되기 때문에 실패 하는 것을 알 수 있습니다.

컨트롤러 기본 클래스의 사용자 개체는 로그인 한 사용자에 대 한 세부 정보를 캡슐화 하 고 런타임에 컨트롤러를 만들 때 ASP.NET MVC에 의해 채워집니다. 웹 서버 환경 외부에서 DinnersController를 테스트 하므로 사용자 개체가 설정 되지 않습니다 (따라서 null 참조 예외).

### <a name="mocking-the-useridentityname-property"></a>User.Identity.Name 속성 모의

모의 프레임 워크를 사용 하면 테스트를 지 원하는 종속 개체의 가짜 버전을 동적으로 만들 수 있으므로 테스트를 더 쉽게 수행할 수 있습니다. 예를 들어 편집 작업 테스트에서 모의 프레임 워크를 사용 하 여 사용자 개체를 동적으로 만들 수 있습니다 .이 개체를 사용 하 여 사용자 개체를 동적으로 만들 수 있습니다. 이렇게 하면 테스트를 실행할 때 null 참조가 throw 되지 않습니다.

ASP.NET MVC와 함께 사용할 수 있는 많은 .NET 모의 프레임 워크가 있습니다. 여기에서 [http://www.mockframeworks.com/](http://www.mockframeworks.com/)의 목록을 볼 수 있습니다. 고객의 NerdDinner 응용 프로그램 테스트를 위해 "Moq" 라는 오픈 소스 모의 프레임 워크를 사용 합니다 .이 프레임 워크는 [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq)에서 무료로 다운로드할 수 있습니다.

다운로드 한 후에는 팀 프로젝트에 참조를 추가 합니다. 테스트 프로젝트에 Moq .dll 어셈블리를 추가 합니다.

![](enable-automated-unit-testing/_static/image12.png)

그런 다음 사용자 이름을 매개 변수로 사용 하는 테스트 클래스에 "CreateDinnersControllerAs (사용자 이름)" 도우미 메서드를 추가 하 고, 그 다음에는 User.Identity.Name 속성을

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

위에서 Moq를 사용 하 여 ControllerContext 개체를 fakes 하는 모의 개체를 만듭니다 .이 개체는 ASP.NET MVC가 컨트롤러 클래스에 전달 하 여 사용자, 요청, 응답 및 세션과 같은 런타임 개체를 노출 합니다. 이 모의 컨텍스트의 HttpContext.User.Identity.Name 속성이 도우미 메서드에 전달 된 사용자 이름 문자열을 반환 해야 함을 나타내기 위해 모의에서 "SetupGet" 메서드를 호출 합니다.

모든 수의 ControllerContext 속성 및 메서드를 mock 할 수 있습니다. 이를 설명 하기 위해 요청에 대해 SetupGet () 호출을 추가 했습니다. IsAuthenticated 속성 (실제로는 아래 테스트에는 필요 하지 않지만 모의 요청 속성을 제공 하는 방법을 설명 하는 데 도움이 됨). 완료 되 면 컨트롤러의 컨트롤러에 대 한 ControllerContext 모의 인스턴스를 할당 하는 도우미 메서드를 반환 합니다.

이제이 도우미 메서드를 사용 하 여 다른 사용자와 관련 된 편집 시나리오를 테스트 하는 단위 테스트를 작성할 수 있습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

이제 통과 한 테스트를 실행할 때 다음을 수행 합니다.

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>UpdateModel () 시나리오 테스트

편집 작업의 HTTP 가져오기 버전을 포함 하는 테스트를 만들었습니다. 이제 편집 작업의 HTTP POST 버전을 확인 하는 몇 가지 테스트를 만들어 보겠습니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

이 작업 메서드를 지원 하기 위한 흥미로운 새로운 테스트 시나리오는 컨트롤러 기본 클래스에서 UpdateModel () 도우미 메서드를 사용 하는 것입니다. 이 도우미 메서드를 사용 하 여 폼 게시 값을 Dinner object 인스턴스에 바인딩합니다.

다음은 UpdateModel () 도우미 메서드에 폼 게시 된 값을 제공 하 여 사용할 수 있는 방법을 보여 주는 두 가지 테스트입니다. FormCollection 개체를 만들고 채운 다음 컨트롤러의 "ValueProvider" 속성에 할당 하 여이 작업을 수행 합니다.

첫 번째 테스트는 저장이 성공 하면 브라우저가 세부 정보 작업으로 리디렉션되는 지 확인 합니다. 두 번째 테스트는 잘못 된 입력이 게시 되 면 작업에서 편집 뷰를 다시 표시 하 고 오류 메시지를 표시 하는지 확인 합니다.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>테스트 래핑

유닛 테스트 컨트롤러 클래스와 관련 된 핵심 개념을 설명 했습니다. 이러한 기술을 사용 하 여 응용 프로그램의 동작을 확인 하는 수백 개의 간단한 테스트를 쉽게 만들 수 있습니다.

컨트롤러 및 모델 테스트에는 실제 데이터베이스가 필요 하지 않으므로 매우 빠르고 쉽게 실행할 수 있습니다. 몇 초 안에 수백 개의 자동화 된 테스트를 실행 하 고 변경 내용이 변경 되었는지 여부에 대 한 피드백을 즉시 얻을 수 있습니다. 이렇게 하면 응용 프로그램을 지속적으로 개선, 리팩터링 및 구체화할 수 있는 확신을 제공할 수 있습니다.

이 챕터의 마지막 토픽으로 테스트를 진행 하 고 있습니다. 테스트는 개발 프로세스가 끝날 때 수행 해야 하는 작업입니다. 이와 반대로 개발 프로세스에서 가능한 한 빨리 자동화 된 테스트를 작성 해야 합니다. 이렇게 하면 개발 하는 즉시 피드백을 받을 수 있으며, 응용 프로그램의 사용 사례 시나리오에 대 한 신중을 고려 하 고 정리 된 계층화 및 결합으로 응용 프로그램을 디자인 하는 과정을 안내 합니다.

이 책의 이후 장에서는 TDD (테스트 기반 개발) 및 ASP.NET MVC와 함께 사용 하는 방법에 대해 설명 합니다. TDD는 결과 코드에서 충족 하는 테스트를 처음으로 작성 하는 반복적인 코딩 방법입니다. TDD를 사용 하 여 구현할 기능을 확인 하는 테스트를 만들어 각 기능을 시작 합니다. 먼저 단위 테스트를 작성 하면 기능 및 작동 방식을 명확 하 게 이해할 수 있습니다. 테스트를 작성 한 후 (그리고 실패를 확인 한 경우에만) 테스트에서 확인 하는 실제 기능을 구현 합니다. 이미 기능을 사용 하는 방법에 대 한 사용 사례를 고려 하 여 작업을 수행 하는 데 시간을 할애 했기 때문에 요구 사항 및 구현 모범 사례를 더 잘 이해 하 게 됩니다. 구현을 완료 한 후 테스트를 다시 실행 하 고 기능이 제대로 작동 하는지 여부에 대 한 즉각적인 피드백을 받을 수 있습니다. 10 장에서 TDD에 대해 더 자세히 살펴보겠습니다.

### <a name="next-step"></a>다음 단계

일부 최종 주석이 추가 되었습니다.

> [!div class="step-by-step"]
> [이전](use-ajax-to-implement-mapping-scenarios.md)
> [다음](nerddinner-wrap-up.md)
