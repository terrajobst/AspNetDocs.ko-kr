---
ms.openlocfilehash: 1b563a8c0674d51f893415221ca8fab574b78265
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57046550"
---
<a name="--"></a>--
================================

[![빌드 상태](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency 상태](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)

jQuery 유효성 검사 플러그 인은 애플리케이션에 맞는 모든 종류의 사용자 지정을 쉽게 만들도록 하면서 기존 폼에 대한 드롭인 유효성 검사를 제공합니다.

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[프로젝트 지원](http://pledgie.com/campaigns/18159)

[![프로젝트 지원](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)

이 프로젝트는 지원을 기다리고 있습니다. [진행 중인 pledgie 캠페인에 기부하고](http://pledgie.com/campaigns/18159) 캠페인 의도를 전달하는 데 도움을 주세요. 이 플러그 인을 사용해본 적이 있거나 사용할 계획인 경우 도움을 주실 수 있습니다.

[pledgie 페이지](http://pledgie.com/campaigns/18159)에서 기부하는 방법에 대한 계획을 찾으실 수 있습니다.

## <a name="get-started"></a>시작

### <a name="downloading-the-prebuilt-files"></a>사전 빌드된 파일 다운로드

사전 빌드된 파일은 http://jqueryvalidation.org/에서 다운로드할 수 있습니다.

### <a name="downloading-the-latest-changes"></a>최신 변경 내용 다운로드

릴리스되지 않은 개발 파일은 다음에서 얻을 수 있습니다.

 1. 이 리포지토리 [다운로드](https://github.com/jzaefferer/jquery-validation/archive/master.zip) 또는 포크
 2. [빌드 설치](CONTRIBUTING.md#build-setup)
 3. `grunt`를 실행하여 “dist” 디렉터리에 빌드된 파일 생성

### <a name="including-it-on-your-page"></a>페이지에 포함

페이지에 jQuery 및 플러그 인을 포함합니다. 그런 다음 유효성을 검사할 폼을 선택하고 `validate` 메서드를 호출합니다.

```html
<form>
    <input required>
</form>
<script src="jquery.js"></script>
<script src="jquery.validate.js"></script>
<script>
$("form").validate();
</script>
```

또는 requirejs를 통해 모듈에 jQuery 및 플러그 인을 포함합니다.

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

규칙 및 사용자 지정을 설정하는 방법에 대한 자세한 내용은 [설명서를 확인](http://jqueryvalidation.org/documentation/)하세요.

## <a name="reporting-issues-and-contributing-code"></a>문제 보고 및 코드 참여

자세한 내용은 [참여 지침](CONTRIBUTING.md)을 참조하세요.

**메일 유효성 검사에 대한 중요 참고 사항** 버전 1.12.0에서 이 플러그 인은 [HTML5 사양이 브라우저에 사용하도록 제안](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)하는 동일한 정규식을 사용합니다. 지침을 따르고 동일한 검사를 사용할 예정입니다. 사양이 잘못되었다고 생각되면 문제를 보고하세요. 다른 요구 사항이 있는 경우 [사용자 지정 메서드를 사용](http://jqueryvalidation.org/jQuery.validator.addMethod/)하는 것이 좋습니다.

## <a name="license"></a>라이선스
Copyright &copy; Jörn Zaefferer<br>
MIT 라이선스에 따라 사용이 허가됩니다.
