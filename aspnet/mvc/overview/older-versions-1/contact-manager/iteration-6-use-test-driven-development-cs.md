---
uid: mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
title: '반복 #6 – 테스트 기반 개발 사용 (C#) | Microsoft Docs'
author: microsoft
description: 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성 하 고 단위 테스트에 대 한 코드를 작성 하 여 응용 프로그램에 새 기능을 추가 합니다. 이 반복의,...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 013c3c26-7dc3-41d1-8064-f233c86008b5
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-6-use-test-driven-development-cs
msc.type: authoredcontent
ms.openlocfilehash: aee0ff9d8d7f17e8a00dab12467bd3a3457fbe18
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78487127"
---
# <a name="iteration-6--use-test-driven-development-c"></a>반복 #6 – 테스트 기반 개발 사용 (C#)

[Microsoft](https://github.com/microsoft) 에서

[코드 다운로드](iteration-6-use-test-driven-development-cs/_static/contactmanager_6_cs1.zip)

> 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성 하 고 단위 테스트에 대 한 코드를 작성 하 여 응용 프로그램에 새 기능을 추가 합니다. 이 반복에서는 연락처 그룹을 추가 합니다.

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

연락처 관리자 응용 프로그램의 이전 반복에서는 코드에 대 한 보안 네트워크를 제공 하는 단위 테스트를 만들었습니다. 단위 테스트를 만드는 데는 코드의 복원 력이 향상 되었습니다. 단위 테스트를 사용 하 여 코드를 변경 하 고 기존 기능이 손상 되었는지 즉시 파악할 수 있습니다.

이 반복에서는 완전히 다른 용도로 단위 테스트를 사용 합니다. 이 반복에서는 *테스트 기반 개발*이라는 응용 프로그램 디자인 원칙의 일부로 단위 테스트를 사용 합니다. 테스트 기반 개발을 연습 하는 경우 먼저 테스트를 작성 한 다음 테스트에 대 한 코드를 작성 합니다.

보다 정확 하 게, 테스트 기반 개발을 수행할 때 코드를 만들 때 완료 해야 하는 세 가지 단계가 있습니다 (빨강/녹색/리팩터링).

1. 실패 한 단위 테스트 작성 (빨간색)
2. 단위 테스트를 통과 하는 코드 작성 (녹색)
3. 코드 리팩터링 (리팩터링)

먼저 단위 테스트를 작성 합니다. 단위 테스트는 코드의 동작 방식에 대 한 의도를 표현 해야 합니다. 단위 테스트를 처음 만들 때 단위 테스트가 실패 해야 합니다. 테스트를 충족 하는 응용 프로그램 코드를 아직 작성 하지 않았으므로 테스트가 실패 합니다.

다음으로 단위 테스트를 통과 하기 위해 충분 한 코드만 작성 합니다. 목표는 laziest, sloppiest 및 가장 빠른 방법으로 코드를 작성 하는 것입니다. 응용 프로그램의 아키텍처에 대해 생각 하는 시간을 낭비 해서는 안 됩니다. 대신 단위 테스트에서 표현 되는 의도를 충족 하는 데 필요한 최소한의 코드를 작성 하는 데 집중 해야 합니다.

마지막으로 충분 한 코드를 작성 한 후에는 응용 프로그램의 전반적인 아키텍처를 단계별로 실행 하 고 고려할 수 있습니다. 이 단계에서는 코드를 더 쉽게 유지 관리할 수 있도록 리포지토리 패턴과 같은 소프트웨어 디자인 패턴을 활용 하 여 코드를 다시 작성 (리팩터링) 합니다. 코드에 단위 테스트가 적용 되므로이 단계에서 코드를 다시 작성 하는 것이 통해 거침 없이 수 있습니다.

테스트 기반 개발을 연습 하 여 발생 하는 많은 이점이 있습니다. 먼저 테스트 기반 개발에서는 실제로 작성 해야 하는 코드에 초점을 맞춰야 합니다. 특정 테스트를 전달 하는 데 충분 한 코드를 작성 하는 것을 지속적으로 중심으로 하기 때문에 weeds로 wandering 하 고 사용 하지 않을 대량의 코드를 작성할 수 없습니다.

둘째, "테스트 먼저" 디자인 방법론을 사용 하면 코드를 사용 하는 방법의 관점에서 코드를 작성 합니다. 즉, 테스트 기반 개발을 연습 하는 경우 사용자 관점에서 지속적으로 테스트를 작성 하 게 됩니다. 따라서 테스트 기반 개발은 더 깔끔하고 이해 하기 쉬운 Api를 생성할 수 있습니다.

마지막으로 테스트 기반 개발에서는 응용 프로그램을 작성 하는 일반적인 프로세스의 일부로 단위 테스트를 작성 해야 합니다. 프로젝트 최종 기한 방법으로 테스트는 일반적으로 창을 이동 하는 첫 번째 작업입니다. 반면에 테스트 기반 개발을 수행 하는 경우 테스트 기반 개발은 응용 프로그램 빌드 프로세스를 중심으로 단위 테스트를 수행 하기 때문에 단위 테스트 작성에 대 한 고리가 만들어집니다 될 가능성이 높습니다.

> [!NOTE] 
> 
> 테스트 기반 개발에 대해 자세히 알아보려면 **기존 코드를 사용 하 여 작업을 효과적**으로 수행 하는 Michael Feathers book을 읽어 보는 것이 좋습니다.

이 반복에서는 연락처 관리자 응용 프로그램에 새 기능을 추가 합니다. 연락처 그룹에 대 한 지원을 추가 합니다. 연락처 그룹을 사용 하 여 연락처를 비즈니스 및 친구 그룹과 같은 범주로 구성할 수 있습니다.

테스트 기반 개발 프로세스를 수행 하 여 응용 프로그램에이 새로운 기능을 추가 합니다. 먼저 단위 테스트를 작성 하 고 이러한 테스트에 대 한 모든 코드를 작성 합니다.

## <a name="what-gets-tested"></a>테스트 대상

이전 반복에서 설명한 대로 일반적으로 데이터 액세스 논리 또는 뷰 논리에 대 한 단위 테스트를 작성 하지 않습니다. 데이터베이스에 액세스 하는 작업은 상대적으로 느리기 때문에 데이터 액세스 논리에 대 한 단위 테스트를 작성 하지 않습니다. 뷰에 액세스 하려면 비교적 속도가 긴 작업 인 웹 서버를 실행 해야 하기 때문에 뷰 논리에 대 한 단위 테스트를 작성 하지 않습니다. 테스트를 매우 빠르게 실행 하는 경우를 제외 하 고 단위 테스트를 작성 하면 안 됩니다.

테스트 기반 개발은 단위 테스트를 기반으로 하기 때문에 처음에는 컨트롤러 및 비즈니스 논리를 작성 하는 데 중점을 둡니다. 데이터베이스 또는 뷰를 건드리지 않습니다. 이 자습서를 마칠 때까지 데이터베이스를 수정 하거나 뷰를 만들지 않습니다. 테스트할 수 있는 것으로 시작 합니다.

## <a name="creating-user-stories"></a>사용자 스토리 만들기

테스트 기반 개발을 실행할 때는 항상 테스트를 작성 해야 합니다. 즉시 작성할 테스트를 어떻게 결정 하나요? 라는 질문을 즉시 발생 시킵니다. 이 질문에 대답 하려면 [**사용자 스토리**](http://en.wikipedia.org/wiki/User_stories)집합을 작성 해야 합니다.

사용자 스토리는 소프트웨어 요구 사항에 대 한 매우 간단한 (일반적으로 한 가지 문장) 설명입니다. 사용자 관점에서 작성 한 요구 사항에 대 한 기술 이외의 설명 이어야 합니다.

새 연락처 그룹 기능에 필요한 기능을 설명 하는 사용자 스토리 집합은 다음과 같습니다.

1. 사용자가 연락처 그룹 목록을 볼 수 있습니다.
2. 사용자가 새 연락처 그룹을 만들 수 있습니다.
3. 사용자가 기존 연락처 그룹을 삭제할 수 있습니다.
4. 사용자는 새 연락처를 만들 때 연락처 그룹을 선택할 수 있습니다.
5. 사용자는 기존 연락처를 편집할 때 연락처 그룹을 선택할 수 있습니다.
6. 연락처 그룹 목록이 인덱스 보기에 표시 됩니다.
7. 사용자가 연락처 그룹을 클릭 하면 일치 하는 연락처 목록이 표시 됩니다.

이 사용자 스토리 목록은 고객이 완전히 이해할 수 있습니다. 기술 구현 세부 정보는 다루지 않습니다.

응용 프로그램을 빌드하는 과정에서 사용자 스토리 집합이 더 구체화 될 수 있습니다. 사용자 스토리를 여러 스토리 (요구 사항)로 나눌 수 있습니다. 예를 들어 새 연락처 그룹을 만드는 것은 유효성 검사를 포함 하도록 결정할 수 있습니다. 이름 없이 연락처 그룹을 제출 하면 유효성 검사 오류가 반환 됩니다.

사용자 스토리 목록을 만든 후에는 첫 번째 단위 테스트를 작성할 준비가 된 것입니다. 먼저 연락처 그룹 목록을 볼 수 있는 단위 테스트를 만듭니다.

## <a name="listing-contact-groups"></a>연락처 그룹 나열

첫 번째 사용자 스토리는 사용자가 연락처 그룹 목록을 볼 수 있어야 한다는 것입니다. 이 스토리를 테스트로 표현 해야 합니다.

프로젝트 관리자의 컨트롤러 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 새 테스트**및 **단위 테스트** 템플릿을 선택 하 여 새 단위 테스트를 만듭니다 (그림 1 참조). 새 단위 테스트의 이름을 GroupControllerTest.cs **확인** 단추를 클릭 합니다.

[GroupControllerTest 단위 테스트를 추가 ![](iteration-6-use-test-driven-development-cs/_static/image1.jpg)](iteration-6-use-test-driven-development-cs/_static/image1.png)

**그림 01**: groupcontrollertest 단위 테스트 추가 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image2.png))

첫 번째 단위 테스트는 목록 1에 포함 되어 있습니다. 이 테스트는 그룹 컨트롤러의 Index () 메서드가 그룹 집합을 반환 하는지 확인 합니다. 테스트는 그룹 컬렉션이 데이터 보기에 반환 되는지 확인 합니다.

**목록 1-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample1.cs)]

Visual Studio의 목록 1에 코드를 처음 입력 하면 빨간색 물결 모양의 많은 줄이 표시 됩니다. GroupController 또는 Group 클래스를 만들지 않았습니다.

이 시점에서 첫 번째 단위 테스트를 실행할 수 있도록 응용 프로그램을 빌드할 수도 있습니다. 좋습니다. 실패 한 테스트로 계산 됩니다. 따라서 이제 응용 프로그램 코드 작성을 시작할 수 있는 권한이 있습니다. 테스트를 실행 하는 데 충분 한 코드를 작성 해야 합니다.

목록 2의 그룹 컨트롤러 클래스는 단위 테스트를 전달 하는 데 필요한 최소한의 코드를 포함 합니다. Index () 작업은 정적으로 코딩 된 그룹 목록을 반환 합니다 (그룹 클래스는 목록 3에서 정의 됨).

**목록 2-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample2.cs)]

**목록 3-Modelss\gss**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample3.cs)]

프로젝트에 GroupController 및 Group 클래스를 추가 하면 첫 번째 단위 테스트가 성공적으로 완료 됩니다 (그림 2 참조). 테스트를 통과 하는 데 필요한 최소 작업을 완료 했습니다. 축 시간입니다.

[성공 ![](iteration-6-use-test-driven-development-cs/_static/image2.jpg)](iteration-6-use-test-driven-development-cs/_static/image3.png)

**그림 02**: 성공! ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image4.png))

## <a name="creating-contact-groups"></a>연락처 그룹 만들기

이제 두 번째 사용자 스토리로 이동할 수 있습니다. 새 연락처 그룹을 만들 수 있어야 합니다. 테스트를 통해이 의도를 표현 해야 합니다.

목록 4의 테스트는 새 그룹을 사용 하 여 Create () 메서드를 호출 하면 해당 그룹이 Index () 메서드에 의해 반환 되는 그룹 목록에 추가 되는지 확인 합니다. 즉, 새 그룹을 만들면 Index () 메서드에서 반환 하는 그룹의 목록에서 새 그룹을 다시 가져올 수 있습니다.

**목록 4-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample4.cs)]

목록 4의 테스트는 새 연락처 그룹을 사용 하 여 그룹 컨트롤러 만들기 () 메서드를 호출 합니다. 그런 다음 테스트는 Group controller Index () 메서드를 호출 하 여 데이터 보기에 새 그룹을 반환 하는지 확인 합니다.

목록 5에 있는 수정 된 그룹 컨트롤러에는 새 테스트를 전달 하는 데 필요한 최소한의 변경 내용이 포함 되어 있습니다.

**목록 5-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample5.cs)]

## <a name="the-group-controller-in-listing-5-has-a-new-create-action-this-action-adds-a-group-to-a-collection-of-groups-notice-that-the-index-action-has-been-modified-to-return-the-contents-of-the-collection-of-groups"></a>목록 5의 그룹 컨트롤러에는 새 만들기 () 작업이 있습니다. 이 작업은 그룹 컬렉션에 그룹을 추가 합니다. Index () 작업은 그룹 컬렉션의 내용을 반환 하도록 수정 되었습니다.

다시 한 번, 단위 테스트를 전달 하는 데 필요한 최소한의 작업을 수행 했습니다. 그룹 컨트롤러를 변경한 후에는 모든 단위 테스트를 통과 합니다.

## <a name="adding-validation"></a>유효성 검사 추가

이 요구 사항은 사용자 스토리에 명시적으로 명시 되지 않았습니다. 그러나 그룹에는 이름이 있어야 합니다. 그렇지 않으면 연락처를 그룹으로 구성 하는 것이 매우 유용 하지 않습니다.

목록 6에는이 의도를 나타내는 새로운 테스트가 포함 되어 있습니다. 이 테스트는 이름을 제공 하지 않고 그룹을 만들려고 시도 하면 모델 상태에서 유효성 검사 오류 메시지가 발생 하는지 확인 합니다.

**목록 6-Controllers\GroupControllerTest.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample6.cs)]

이 테스트를 충족 하기 위해 그룹 클래스에 이름 속성을 추가 해야 합니다 (목록 7 참조). 또한 그룹 컨트롤러의 Create () 작업에 약간의 유효성 검사 논리를 추가 해야 합니다 (목록 8 참조).

**목록 7-Modelss\ents\web.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample7.cs)]

**목록 8-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample8.cs)]

이제 그룹 컨트롤러 만들기 () 작업에 유효성 검사 및 데이터베이스 논리가 모두 포함 됩니다. 현재 그룹 컨트롤러에서 사용 하는 데이터베이스는 메모리 내 컬렉션으로 구성 됩니다.

## <a name="time-to-refactor"></a>리팩터링 시간

빨강/녹색/리팩터링의 세 번째 단계는 리팩터링 파트입니다. 이 시점에서 코드를 다시 실행 하 고 응용 프로그램을 리팩터링하여 디자인을 개선 하는 방법을 고려해 야 합니다. 리팩터링 단계는 소프트웨어 디자인 원칙 및 패턴을 구현 하는 가장 좋은 방법을 잘 생각 하는 단계입니다.

코드 디자인을 개선 하기 위해 선택 하는 방법으로 코드를 자유롭게 수정할 수 있습니다. 기존 기능을 중단 하지 못하도록 하는 단위 테스트의 안전성을 보장 합니다.

현재 그룹 컨트롤러는 좋은 소프트웨어 디자인의 관점에서 매우 복잡 합니다. 그룹 컨트롤러에는 유효성 검사 및 데이터 액세스 코드가 얽 됩니다. 단일 책임 원칙을 위반 하지 않도록 하려면 이러한 문제를 다른 클래스로 분리 해야 합니다.

리팩터링된 그룹 컨트롤러 클래스는 목록 9에 포함 되어 있습니다. 컨트롤러가 연락처 관리자 서비스 계층을 사용 하도록 수정 되었습니다. 이는 연락처 컨트롤러와 함께 사용 하는 것과 동일한 서비스 계층입니다.

목록 10에는 그룹의 유효성 검사, 나열 및 만들기를 지원 하기 위해 연락처 관리자 서비스 계층에 추가 된 새 메서드가 포함 되어 있습니다. 새 메서드를 포함 하도록 IContactManagerService 인터페이스가 업데이트 되었습니다.

목록 11에는 IContactManagerRepository 인터페이스를 구현 하는 새 FakeContactManagerRepository 클래스가 포함 되어 있습니다. IContactManagerRepository 인터페이스를 구현 하는 EntityFakeContactManagerRepository 클래스와 달리 새로운 클래스는 데이터베이스와 통신 하지 않습니다. FakeContactManagerRepository 클래스는 메모리 내 컬렉션을 데이터베이스에 대 한 프록시로 사용 합니다. 이 클래스는 단위 테스트에서 가짜 리포지토리 계층으로 사용 됩니다.

**목록 9-Controllers\GroupController.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample9.cs)]

**10-Controllers\ubmanagerserviceservice.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample10.cs)]

**목록 11-Controllers\FakeContactManagerRepository.cs**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample11.cs)]

IContactManagerRepository 인터페이스를 수정 하려면를 사용 하 여 EntityContactManagerRepository 클래스에서 CreateGroup () 및 ListGroups () 메서드를 구현 해야 합니다. 이 작업을 수행 하는 laziest 및 가장 빠른 방법은 다음과 같이 스텁 메서드를 추가 하는 것입니다.   

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample12.cs)]

마지막으로, 이러한 응용 프로그램 디자인 변경으로 인해 단위 테스트를 수정 해야 합니다. 이제 단위 테스트를 수행할 때 FakeContactManagerRepository를 사용 해야 합니다. 업데이트 된 GroupControllerTest 클래스는 목록 12에 포함 되어 있습니다.

**12-Controllers\GroupControllerTest.cs 나열**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample13.cs)]

이러한 모든 변경 내용을 한 번 수행한 후에는 모든 단위 테스트를 통과 합니다. 빨강/녹색/리팩터링의 전체 주기를 완료 했습니다. 처음 두 사용자 스토리를 구현 했습니다. 이제 사용자 스토리에 표시 되는 요구 사항에 대 한 단위 테스트를 지원 합니다. 나머지 사용자 스토리를 구현 하는 것은 동일한 빨강/녹색/리팩터링 주기를 반복 하는 것입니다.

## <a name="modifying-our-database"></a>데이터베이스 수정

아쉽게도 단위 테스트로 표현 되는 요구 사항을 모두 충족 하는 경우에도 작업이 수행 되지 않습니다. 그래도 데이터베이스를 수정 해야 합니다.

새 그룹 데이터베이스 테이블을 만들어야 합니다. 다음 단계를 수행하세요.

1. 서버 탐색기 창에서 Tables 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **새 테이블 추가**를 선택 합니다.
2. 테이블 디자이너 아래에서 설명 하는 두 개의 열을 입력 합니다.
3. Id 열을 기본 키 및 Id 열로 표시 합니다.
4. 플로피 아이콘을 클릭 하 여 이름 그룹을 포함 하는 새 테이블을 저장 합니다.

<a id="0.11_table01"></a>

| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| Id | int | False |
| 속성 | nvarchar(50) | False |

다음으로 contact 테이블에서 모든 데이터를 삭제 해야 합니다. 그렇지 않으면 연락처와 그룹 테이블 간에 관계를 만들 수 없습니다. 다음 단계를 수행하세요.

1. Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **테이블 데이터 표시**를 선택 합니다.
2. 모든 행을 삭제 합니다.

그런 다음 그룹 데이터베이스 테이블과 기존 연락처 데이터베이스 테이블 간의 관계를 정의 해야 합니다. 다음 단계를 수행하세요.

1. 서버 탐색기 창에서 연락처 테이블을 두 번 클릭 하 여 테이블 디자이너를 엽니다.
2. GroupId 라는 연락처 테이블에 새 정수 열을 추가 합니다.
3. 관계 단추를 클릭 하 여 외래 키 관계 대화 상자를 엽니다 (그림 3 참조).
4. 추가 단추를 클릭합니다.
5. 테이블 및 열 사양 단추 옆에 나타나는 줄임표 단추를 클릭 합니다.
6. 테이블 및 열 대화 상자에서 기본 키 테이블 및 Id를 기본 키 열로 선택 합니다. 외래 키 테이블로 연락처를 선택 하 고 GroupId를 외래 키 열로 선택 합니다 (그림 4 참조). 확인 단추를 클릭합니다.
7. **INSERT 및 UPDATE 사양**에서 **Delete Rule**에 대 한 **Cascade** 값을 선택 합니다.
8. [닫기] 단추를 클릭 하 여 외래 키 관계 대화 상자를 닫습니다.
9. 저장 단추를 클릭 하 여 연락처 테이블의 변경 내용을 저장 합니다.

[데이터베이스 테이블 관계를 만드는 ![](iteration-6-use-test-driven-development-cs/_static/image3.jpg)](iteration-6-use-test-driven-development-cs/_static/image5.png)

**그림 03**: 데이터베이스 테이블 관계 만들기 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image6.png))

[테이블 관계 지정 ![](iteration-6-use-test-driven-development-cs/_static/image4.jpg)](iteration-6-use-test-driven-development-cs/_static/image7.png)

**그림 04**: 테이블 관계 지정 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image8.png))

### <a name="updating-our-data-model"></a>데이터 모델 업데이트

다음으로 새 데이터베이스 테이블을 나타내기 위해 데이터 모델을 업데이트 해야 합니다. 다음 단계를 수행하세요.

1. 모델 폴더에서 Entity Designer를 두 번 클릭 하 여 해당 파일을 엽니다.
2. 디자이너 화면을 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스에서 모델 업데이트**메뉴 옵션을 선택 합니다.
3. 업데이트 마법사에서 그룹 테이블을 선택 하 고 마침 단추를 클릭 합니다 (그림 5 참조).
4. Groups 엔터티를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **이름 바꾸기**를 선택 합니다. *그룹 엔터티의 이름을* *Group* (단수형)으로 변경 합니다.
5. Contact 엔터티 아래쪽에 표시 되는 그룹 탐색 속성을 마우스 오른쪽 단추로 클릭 합니다. *Groups* 탐색 속성의 이름을 *Group* (단수형)으로 변경 합니다.

[데이터베이스에서 Entity Framework 모델을 업데이트 ![](iteration-6-use-test-driven-development-cs/_static/image5.jpg)](iteration-6-use-test-driven-development-cs/_static/image9.png)

**그림 05**: 데이터베이스에서 Entity Framework 모델 업데이트 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image10.png))

이러한 단계를 완료 한 후에 데이터 모델은 연락처 및 그룹 테이블을 모두 나타냅니다. Entity Designer는 두 엔터티를 모두 표시 해야 합니다 (그림 6 참조).

[그룹 및 연락처를 표시 하는 ![Entity Designer](iteration-6-use-test-driven-development-cs/_static/image6.jpg)](iteration-6-use-test-driven-development-cs/_static/image11.png)

**그림 06**: 그룹 및 연락처 표시 Entity Designer ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image12.png))

### <a name="creating-our-repository-classes"></a>리포지토리 클래스 만들기

다음으로 리포지토리 클래스를 구현 해야 합니다. 이 반복 과정에서 단위 테스트를 충족 하는 코드를 작성 하는 동안 IContactManagerRepository 인터페이스에 몇 가지 새로운 메서드를 추가 했습니다. IContactManagerRepository 인터페이스의 최종 버전은 목록 14에 포함 되어 있습니다.

**14-Models\IContactManagerRepository.cs 나열**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample14.cs)]

연락처 그룹 작업과 관련 된 메서드를 실제로 구현 하지 않았습니다. 현재 EntityIContactManagerRepository Managerrepository 클래스에는 인터페이스에 나열 된 각 연락처 그룹 메서드에 대 한 스텁 메서드가 있습니다. 예를 들어 ListGroups () 메서드는 현재 다음과 같습니다.

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample15.cs)]

스텁 메서드를 사용 하 여 응용 프로그램을 컴파일하고 단위 테스트를 전달할 수 있었습니다. 그러나 이제 이러한 메서드를 실제로 구현할 때입니다. EntityContactManagerRepository 클래스의 최종 버전은 목록 13에 포함 되어 있습니다.

**13-Models\EntityContactManagerRepository.cs 나열**

[!code-csharp[Main](iteration-6-use-test-driven-development-cs/samples/sample16.cs)]

### <a name="creating-the-views"></a>뷰 만들기

ASP.NET MVC 응용 프로그램을 사용 하는 경우 기본 ASP.NET 뷰 엔진을 사용 합니다. 따라서 특정 단위 테스트에 대 한 응답으로 뷰를 만들지 않아도 됩니다. 그러나 응용 프로그램은 뷰가 없어도 쓸모 없게 되므로 연락처 관리자 응용 프로그램에 포함 된 보기를 만들고 수정 하지 않고도이 반복을 완료할 수 있습니다.

연락처 그룹을 관리 하기 위해 다음과 같은 새로운 뷰를 만들어야 합니다 (그림 7 참조).

- Views\Group\Index.aspx-연락처 그룹 목록을 표시 합니다.
- Views\Group\Delete.aspx-연락처 그룹을 삭제 하는 확인 양식을 표시 합니다.

[그룹 인덱스 보기를 ![합니다.](iteration-6-use-test-driven-development-cs/_static/image7.jpg)](iteration-6-use-test-driven-development-cs/_static/image13.png)

**그림 07**: 그룹 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image14.png))

연락처 그룹을 포함 하도록 다음 기존 보기를 수정 해야 합니다.

- Views\Home\Create.aspx
- Views\Home\Edit.aspx
- Views\Home\Index.aspx

이 자습서와 함께 제공 되는 Visual Studio 응용 프로그램을 살펴보면 수정 된 보기를 볼 수 있습니다. 예를 들어 그림 8은 연락처 인덱스 보기를 보여 줍니다.

[연락처 인덱스 보기 ![](iteration-6-use-test-driven-development-cs/_static/image8.jpg)](iteration-6-use-test-driven-development-cs/_static/image15.png)

**그림 08**: 연락처 인덱스 보기 ([전체 크기 이미지를 보려면 클릭](iteration-6-use-test-driven-development-cs/_static/image16.png))

## <a name="summary"></a>요약

이 반복에서는 테스트 기반 개발 응용 프로그램 디자인 방법론에 따라 연락처 관리자 응용 프로그램에 새 기능을 추가 했습니다. 사용자 스토리 집합을 만들어 시작 했습니다. 사용자 스토리로 표현 되는 요구 사항에 해당 하는 단위 테스트 집합을 만들었습니다. 마지막으로 단위 테스트로 표현 되는 요구 사항을 충족 하기에 충분 한 코드만 작성 했습니다.

단위 테스트로 표현 되는 요구 사항을 충족 하기에 충분 한 코드를 작성 하는 작업이 완료 되 면 데이터베이스와 뷰가 업데이트 됩니다. 데이터베이스에 새 그룹 테이블을 추가 하 고 Entity Framework 데이터 모델을 업데이트 했습니다. 또한 보기 집합을 만들고 수정 했습니다.

다음 반복 (최종 반복)에서 Ajax를 활용 하도록 응용 프로그램을 다시 작성 합니다. Ajax를 활용 하면 연락처 관리자 응용 프로그램의 응답성과 성능을 향상 시킬 수 있습니다.

> [!div class="step-by-step"]
> [이전](iteration-5-create-unit-tests-cs.md)
> [다음](iteration-7-add-ajax-functionality-cs.md)
