---
ms.openlocfilehash: 3be420696add54094f24424285a905e7e7963bad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028830"
---
# <a name="bootstraphttpgetbootstrapcom"></a>[부트스트랩](http://getbootstrap.com)

[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower 버전](https://img.shields.io/bower/v/bootstrap.svg)
[![npm 버전](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![빌드 상태](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency 상태](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium 테스트 상태](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)

부트스트랩은 더욱 쉽고 빠른 웹 개발을 위한 유연하고 직관적이며 강력한 프런트 엔드 프레임워크로, [Mark Otto](https://twitter.com/mdo)와 [Jacob Thornton](https://twitter.com/fat)이 만들었으며 커뮤니티의 전폭적인 지원과 참여를 통해 [핵심 팀](https://github.com/orgs/twbs/people)에서 유지 관리하고 있습니다.

시작하려면 <http://getbootstrap.com>을 체크 아웃하세요!


## <a name="table-of-contents"></a>목차

* [빠른 시작](#quick-start)
* [버그 및 기능 요청](#bugs-and-feature-requests)
* [문서](#documentation)
* [참여](#contributing)
* [커뮤니티](#community)
* [버전 관리](#versioning)
* [작성자](#creators)
* [저작권 및 라이선스](#copyright-and-license)


## <a name="quick-start"></a>빠른 시작

다음과 같은 몇 가지 빠른 시작 옵션을 사용할 수 있습니다.

* [최신 릴리스 다운로드](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).
* 리포지토리 복제: `git clone https://github.com/twbs/bootstrap.git`.
* [Bower](http://bower.io)를 사용하여 설치: `bower install bootstrap`.
* [npm](https://www.npmjs.com)을 사용하여 설치: `npm install bootstrap@3`.
* [Meteor](https://www.meteor.com)을 사용하여 설치: `meteor add twbs:bootstrap`.
* [Composer](https://getcomposer.org)를 사용하여 설치: `composer require twbs/bootstrap`.

프레임워크 콘텐츠, 템플릿 및 예제 등에 대한 내용은 [시작 페이지](http://getbootstrap.com/getting-started/)를 읽어 보세요.

### <a name="whats-included"></a>포함된 내용

다운로드 내에서 다음 디렉터리 및 파일을 찾을 수 있습니다. 여기에는 공통된 자산이 논리적으로 그룹화되어 있으며 컴파일 버전과 축소된 변형 버전이 모두 제공됩니다. 다음과 같은 코드를 볼 수 있습니다.

```
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/
    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2
```

컴파일된 축소형 CSS 및 JS(`bootstrap.min.*`) 뿐만 아니라 컴파일된 CSS 및 JS(`bootstrap.*`)도 제공됩니다. CSS [소스 맵](https://developer.chrome.com/devtools/docs/css-preprocessors)(`bootstrap.*.map`)은 특정 브라우저의 개발자 도구에서 사용할 수 있습니다. 선택적 부트스트랩 테마처럼 문자 모양 아이콘의 글꼴이 포함됩니다.


## <a name="bugs-and-feature-requests"></a>버그 및 기능 요청

버그 또는 기능 요청이 있나요? 먼저 [문제 지침](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker)을 읽고 기존 및 마감된 문제를 검색하세요. 문제 또는 아이디어가 아직 해결되지 않은 경우 [새 문제를 여세요](https://github.com/twbs/bootstrap/issues/new).

부트스트랩 v3가 현재 유지 관리 모드에 있고 새 기능을 제공하기 위해 종료되었으므로 **기능 요청이 [부트스트랩 v4](https://github.com/twbs/bootstrap/tree/v4-dev)** 를 대상으로 지정하는지 확인하세요. 이를 통해 Microsoft는 부트스트랩 v4에 노력을 집중할 수 있을 것입니다.


## <a name="documentation"></a>설명서

루트 디렉터리의 이 리포지토리에 포함되어 있는 부트스트랩의 설명서는 [Jekyll](http://jekyllrb.com)로 작성했으며 GitHub Pages <http://getbootstrap.com>에 공개적으로 호스트되어 있습니다. 문서를 로컬로 실행할 수도 있습니다.

### <a name="running-documentation-locally"></a>로컬로 문서 실행

1. 필요한 경우 `bundle install`을 사용하여 [Jekyll](http://jekyllrb.com/docs/installation) 및 기타 Ruby 종속성을 설치합니다.
   **Windows 사용자에 대 한 참고:** 읽기 [이 비공식 안내서](http://jekyll-windows.juthilo.com/) Jekyll을 문제 없이 실행 가져오려면.
2. 루트 `/bootstrap` 디렉터리에서 명령줄을 통해 `bundle exec jekyll serve`를 실행합니다.
4. 브라우저에서 `http://localhost:9001`을 엽니다.

해당 [설명서](http://jekyllrb.com/docs/home/)를 읽어 Jekyll 사용에 대해 자세히 알아보세요.

### <a name="documentation-for-previous-releases"></a>이전 릴리스에 대한 설명서

v2.3.2에 대한 설명서는 분기가 부트스트랩 3으로 전환되는 동안 <http://getbootstrap.com/2.3.2/>에서 사용할 수 있습니다.

[이전 릴리스](https://github.com/twbs/bootstrap/releases) 및 해당 설명서도 다운로드할 수 있습니다.


## <a name="contributing"></a>참여

[참여 지침](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md)을 잘 읽어보세요. 문제 개설 지침, 코딩 표준 및 개발 관련 참고 사항이 포함되어 있습니다.

또한 끌어오기 요청에 JavaScript 패치 또는 기능이 포함되어 있는 경우 [관련 단위 테스트](https://github.com/twbs/bootstrap/tree/master/js/tests)를 포함해야 합니다. 모든 HTML 및 CSS는 [Mark Otto](https://github.com/mdo)에서 관리하는 [코드 지침](https://github.com/mdo/code-guide)을 준수해야 합니다.

**이제 부트스트랩 v3는 새 기능을 제공하기 위해 종료되었습니다.** 이 버전은 유지 관리 모드로 전환되었으므로 향후 사용될 프레임워크인 [부트스트랩 v4](https://github.com/twbs/bootstrap/tree/v4-dev)에 노력을 집중할 수 있게 되었습니다. 새 기능을 추가하는(버그 수정 아님) 끌어오기 요청은 [부트스트랩 v4(`v4-dev` Git 분기)](https://github.com/twbs/bootstrap/tree/v4-dev)를 대상으로 지정해야 합니다.

일반 텍스트 편집기에서 쉽게 사용할 수 있도록 [편집기 구성](https://github.com/twbs/bootstrap/blob/master/.editorconfig)에서 편집기 기본 설정을 사용할 수 있습니다. <http://editorconfig.org>에서 자세한 내용을 알아보고 플러그 인을 다운로드합니다.


## <a name="community"></a>커뮤니티

부트스트랩 개발에 대한 업데이트를 받고 프로젝트 유지 관리 담당자 및 커뮤니티 멤버와 대화를 나눌 수 있습니다.

* [@getbootstrapTwitter 에서](https://twitter.com/getbootstrap) 을 팔로우합니다.
* [공식 부트스트랩 블로그](http://blog.getbootstrap.com)를 읽고 가입할 수 있습니다.
* [공식 Slack 방](https://bootstrap-slack.herokuapp.com)에 참가할 수 있습니다.
* IRC의 동료 부트스트래퍼와 대화를 나눌 수 있습니다. `irc.freenode.net` 서버의 `##bootstrap` 채널
* 구현 도움말은 Stack Overflow([`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3) 태그 지정)에서 찾을 수 있습니다.
* 개발자는 최대 검색 기능을 위해 [npm](https://www.npmjs.com/browse/keyword/bootstrap) 또는 유사한 배달 메커니즘을 통해 배포할 때 부트스트랩 기능을 수정하거나 추가 기능을 제공하는 패키지에 `bootstrap` 키워드를 사용해야 합니다.


## <a name="versioning"></a>버전 관리

릴리스 주기의 투명성을 보장하고 이전 버전과의 호환성을 유지하기 위해 부트스트랩은 [유의적 버전 지침](http://semver.org/)에 따라 유지 관리됩니다. 여의치 않은 경우도 있지만 최대한 이러한 규칙을 준수하려고 할 것입니다.

각 릴리스 버전의 부트스트랩에 대한 변경 로그를 보려면 [GitHub 프로젝트의 릴리스 섹션](https://github.com/twbs/bootstrap/releases)을 참조하세요. [공식 부트스트랩 블로그](http://blog.getbootstrap.com)의 릴리스 알림 게시물에는 각 릴리스에서 수행된 가장 중요한 변경 내용이 요약되어 있습니다.


## <a name="creators"></a>작성자

**Mark Otto**

* <https://twitter.com/mdo>
* <https://github.com/mdo>

**Jacob Thornton**

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a>저작권 및 라이선스

코드 및 문서 copyright 2011-2016 Twitter, Inc. 코드는 [MIT 라이선스](https://github.com/twbs/bootstrap/blob/master/LICENSE)에 따라 릴리스되었습니다. 문서는 [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE)에 따라 릴리스되었습니다.
