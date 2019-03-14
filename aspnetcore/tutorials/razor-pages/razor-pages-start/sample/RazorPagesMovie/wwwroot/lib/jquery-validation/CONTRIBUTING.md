---
ms.openlocfilehash: 3b33bb9bcab1aa7e5438c6fe3f2d7ba0833e7756
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57060820"
---
--

## <a name="reporting-an-issue"></a>문제 신고

1. 해결 중인 문제가 재현 가능한지 확인하세요.
2. http://jsbin.com 또는 http://jsfiddle.net를 사용하여 테스트 페이지를 제공합니다.
3. 문제를 재현할 수 있는 브라우저를 표시합니다. **참고: IE 호환성 모드 문제는 해결 되지 않습니다. 실제 브라우저에서 테스트하세요.**
4. 문제가 재현될 수 있는 플러그 인 버전 최신 버전으로 업데이트한 후 재현 가능한지 여부

설명서의 문제도 [jQuery 유효성 검사](https://github.com/jzaefferer/jquery-validation/issues) 문제 추적기에서 추적됩니다.
설명서를 개선하기 위한 끌어오기 요청은 [jQuery 유효성 검사 설명서](https://github.com/jzaefferer/validation-content) 리포지토리에 적합합니다.

**메일 유효성 검사에 대한 중요 참고 사항** 버전 1.12.0에서 이 플러그 인은 [HTML5 사양이 브라우저에 사용하도록 제안](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)하는 동일한 정규식을 사용합니다. 지침을 따르고 동일한 검사를 사용할 예정입니다. 사양이 잘못되었다고 생각되면 문제를 보고하세요. 다른 요구 사항이 있는 경우 [사용자 지정 메서드를 사용](http://jqueryvalidation.org/jQuery.validator.addMethod/)하는 것이 좋습니다.

## <a name="contributing-code"></a>코드 참여

참여해 주셔서 감사합니다. 다음은 귀하의 참여에 도움이 되는 몇 가지 지침입니다.

1. 해결 중인 문제가 재현 가능한지 확인하세요. jsbin.com 또는 jsfiddle.net을 사용하여 테스트 페이지를 제공합니다.
2. [jQuery 스타일 가이드](http://contribute.jquery.com/style-guides/js)를 따릅니다.
3. 패치와 함께 단위 테스트를 추가하거나 업데이트합니다. 최소한 하나의 브라우저에서 단위 테스트를 실행합니다(아래 참조).
4. `grunt`(아래 참조)를 실행하여 lint 및 기타 문제가 있는지 확인합니다.
5. 커밋 메시지의 변경 내용을 설명 하 고 다음과 같이 티켓을 참조 합니다. "데모: dynamic-totals 데모에 대한 대리자 버그를 수정했습니다. Fixes #51”. 새 지역화 파일을 추가 하는 경우 다음과 같은 코드를 사용 합니다. "지역화 합니다. 추가 크로아티아어 (HR) 지역화 "

## <a name="build-setup"></a>빌드 설치

1. [NodeJS](http://nodejs.org)를 설치합니다.
2. `npm install -g grunt-cli`를 실행하여 Grunt CLI를 설치합니다. 자세한 내용은 웹 사이트 http://gruntjs.com/getting-started에서 지원됩니다.
3. `npm install`을 실행하여 NPM 종속성을 설치합니다.
4. 이제 `grunt`를 실행하여 빌드를 호출할 수 있습니다.

## <a name="creating-a-new-additional-method"></a>새 추가 메서드 만들기

additional-methods.js에서 참여하려는 사용자 지정 메서드를 작성한 경우:

1. 분기 만들기
2. 메서드를 `src/additional`에 새 파일로 추가합니다.
3. (선택 사항) `src/localization`에 번역을 추가합니다.
4. 마스터 분기에 끌어오기 요청을 보냅니다.

## <a name="unit-tests"></a>단위 테스트

단위 테스트를 실행하려면 브라우저에서 `test/index.html`을 열기만 하면 됩니다. 필요한 모든 종속성을 사용할 수 있도록 하려면 먼저 `npm install`을 실행해야 합니다.
수정 사항을 개발할 때는 브라우저 하나로 작업하다가 다른 브라우저에서도 실행한 후에 커밋합니다. 일반적으로 최신 Chrome, Firefox, Safari 및 Opera와 일부 IE를 사용할 수 있습니다.

## <a name="documentation"></a>설명서

[jQuery 유효성 검사](https://github.com/jzaefferer/jquery-validation/issues) 문제 추적기에서 설명서 문제를 보고하세요.
끌어오기 요청이 공용 API를 구현하거나 변경하는 경우 [jQuery 유효성 검사 설명서](https://github.com/jzaefferer/validation-content) 리포지토리에 대한 끌어오기 요청도 제공해야 합니다.

## <a name="linting"></a>Lint

JSHint 및 기타 도구를 실행하려면 `grunt`를 사용하세요.
