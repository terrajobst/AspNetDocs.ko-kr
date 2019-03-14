---
title: Razor 구성 요소 디버깅
author: guardrex
description: Blazor 및 Razor 구성 요소 응용 프로그램을 디버깅 하는 방법에 알아봅니다.
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/debug
ms.openlocfilehash: fb7ddcf3ae40ec28a372adf724a293b375be28a1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57034120"
---
# <a name="debug-razor-components"></a>Razor 구성 요소 디버깅

[Daniel Roth](https://github.com/danroth27)

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

Razor 구성 요소는 일부 *초기* WebAssembly chrome에서에서 실행 되는 클라이언트 쪽 Blazor 앱 디버깅을 지원 합니다. 이 초기 디버깅 지원 매우 제한적이 고 윤이 나 지 않는 상태인 함께 기본 디버깅 인프라를 보여 줍니다.

Chrome에서 클라이언트 쪽 Blazor 앱을 디버그:

* 에 Blazor 앱 구축 `Debug` 구성 (게시 되지 않은 앱에 대 한 기본값).
* Chrome (버전 70 이상)에서 Blazor 앱을 실행 합니다.
* (개발 도구 패널 보다 디버깅 환경을 위해 아마도 닫아야)에 없는 앱에 키보드 포커스를 사용 하 여 다음 Blazor 관련 바로 가기 키를 선택 합니다.
  * `Shift+Alt+D` Windows/linux
  * `Shift+Cmd+D` macos

원격 디버깅을 사용한 Blazor 응용 프로그램을 디버깅 하려면 Chrome을 실행 합니다. 원격 디버깅을 사용 하지 않도록 설정 하는 경우에 오류 페이지가 크롬으로 생성 됩니다. 오류 페이지를 실행 하기 위한 Chrome 디버깅 포트를 사용 하 여 열고 Blazor 디버깅 프록시 앱에 연결할 수 있도록 지침을 포함 합니다. *모든 Chrome 인스턴스를 닫고* 설명 된 대로 Chrome을 다시 시작 합니다.

![Blazor 디버깅 오류 페이지](https://user-images.githubusercontent.com/1874516/43123091-01ec0796-8ed8-11e8-844c-23b4e6e9d069.png)

Chrome 원격 디버깅이 설정 된 상태로 실행 되 면 디버깅 바로 가기 키를 새 디버거 탭을 엽니다. 잠시 후 합니다 *원본* 탭에 응용 프로그램에.NET 어셈블리의 목록을 표시 합니다. 각 어셈블리를 확장 하 고 찾을 합니다 *.cs*/*.cshtml* 원본 파일에 디버깅에 사용할 수 있습니다. 중단점 설정 앱의 탭으로 다시 전환 하 고 중단점을 적중 합니다. 후 중단점에 도달 하면 단일 단계에는 (`F10`) 하거나 재개 (`F8`) 일반적으로 합니다.

![Blazor 디버깅](https://user-images.githubusercontent.com/1874516/43123060-efb0b3b0-8ed7-11e8-9ea5-97aa34247a0b.png)

Blazor 제공 디버깅 프록시를 구현 하는 [Chrome DevTools 프로토콜](https://chromedevtools.github.io/devtools-protocol/) 프로토콜을 사용 하 여 보강 하 고 있습니다. NET 관련 정보입니다. 디버깅 바로 가기 키를 누르면 Blazor 프록시에서 Chrome DevTools를 가리킵니다. 디버그를 검색 하는 브라우저 창에 연결 하는 프록시 (따라서 원격 디버깅 설정).

이유 브라우저 소스 맵만 사용 하지 궁금할 수 있습니다. 소스 맵 브라우저 컴파일된 파일의 원래 소스 파일에 다시 매핑할 수 있습니다. 그러나 Blazor 매핑되지 않거나 C# JS/WASM (적어도 아직 서비스 되지 않음)에 직접. 대신 Blazor 소스 맵과 관련이 있으므로 브라우저 내에서 IL 해석을 수행 합니다.

디버거 기능은 보면 **극히**합니다. 하면 현재만 됩니다.

* 설정 하 고 중단점을 제거 합니다.
* 한 단계씩 코드를 다시 시작 (`F8`).
* 에 *지역* 표시, 형식의 지역 변수 값을 확인할 `int`를 `string`, 및 `bool`합니다.
* .NET 및.NET에는 JavaScript에서 JavaScript로 이동 하는 호출 체인을 포함 하 여 호출 스택을 보려면.

있습니다 *없습니다*:

* 없는 모든 지역 변수의 값을 확인 한 `int`, `string`, 또는 `bool`.
* 클래스 속성 또는 필드의 값을 확인 합니다.
* 해당 값을 보려면 변수 위로
* 콘솔에서 식을 평가 합니다.
* 비동기 호출에서 실행 합니다.
* 대부분의 다른 일반적인 디버깅 시나리오를 수행 합니다.

추가 시나리오를 디버깅의 개발을 지속적으로 포커스가 엔지니어링 팀의 합니다.

## <a name="troubleshooting-tip"></a>문제 해결 팁

오류를 실행 하는 경우 다음 팁이 도움이 될 수 있습니다.

에 **디버거** 탭, 브라우저에서 개발자 도구를 엽니다. 콘솔에서 실행 `localStorage.clear()` 모든 중단점을 제거 합니다.
