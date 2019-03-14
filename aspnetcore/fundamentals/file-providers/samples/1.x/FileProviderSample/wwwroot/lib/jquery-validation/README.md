---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57029990"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="0564a-101">[jQuery 유효성 검사 플러그 인](https://jqueryvalidation.org/) - 유효성 검사를 쉽게 형성합니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-101">[jQuery Validation Plugin](https://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="0564a-102">[![빌드 상태](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency 상태](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="0564a-102">[![Build Status](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency Status](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="0564a-103">jQuery 유효성 검사 플러그 인은 애플리케이션에 맞는 모든 종류의 사용자 지정을 쉽게 만들도록 하면서 기존 폼에 대한 드롭인 유효성 검사를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0564a-104">시작</span><span class="sxs-lookup"><span data-stu-id="0564a-104">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="0564a-105">사전 빌드된 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="0564a-105">Downloading the prebuilt files</span></span>

<span data-ttu-id="0564a-106">사전 빌드된 파일은 https://jqueryvalidation.org/에서 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-106">Prebuilt files can be downloaded from https://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="0564a-107">최신 변경 내용 다운로드</span><span class="sxs-lookup"><span data-stu-id="0564a-107">Downloading the latest changes</span></span>

<span data-ttu-id="0564a-108">릴리스되지 않은 개발 파일은 다음에서 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-108">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="0564a-109">이 리포지토리 [다운로드](https://github.com/jquery-validation/jquery-validation/archive/master.zip) 또는 포크</span><span class="sxs-lookup"><span data-stu-id="0564a-109">[Downloading](https://github.com/jquery-validation/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="0564a-110">빌드 설치</span><span class="sxs-lookup"><span data-stu-id="0564a-110">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="0564a-111">`grunt`를 실행하여 “dist” 디렉터리에 빌드된 파일 생성</span><span class="sxs-lookup"><span data-stu-id="0564a-111">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="0564a-112">페이지에 포함</span><span class="sxs-lookup"><span data-stu-id="0564a-112">Including it on your page</span></span>

<span data-ttu-id="0564a-113">페이지에 jQuery 및 플러그 인을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-113">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="0564a-114">그런 다음 유효성을 검사할 폼을 선택하고 `validate` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-114">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="0564a-115">또는 requirejs를 통해 모듈에 jQuery 및 플러그 인을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-115">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="0564a-116">규칙 및 사용자 지정을 설정하는 방법에 대한 자세한 내용은 [설명서를 확인](https://jqueryvalidation.org/documentation/)하세요.</span><span class="sxs-lookup"><span data-stu-id="0564a-116">For more information on how to setup a rules and customizations, [check the documentation](https://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="0564a-117">문제 보고 및 코드 참여</span><span class="sxs-lookup"><span data-stu-id="0564a-117">Reporting issues and contributing code</span></span>

<span data-ttu-id="0564a-118">자세한 내용은 [참여 지침](CONTRIBUTING.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0564a-118">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="0564a-119">**메일 유효성 검사에 대한 중요 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="0564a-119">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="0564a-120">버전 1.12.0에서 이 플러그 인은 [HTML5 사양이 브라우저에 사용하도록 제안](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)하는 동일한 정규식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-120">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="0564a-121">지침을 따르고 동일한 검사를 사용할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-121">We will follow their lead and use the same check.</span></span> <span data-ttu-id="0564a-122">사양이 잘못되었다고 생각되면 문제를 보고하세요.</span><span class="sxs-lookup"><span data-stu-id="0564a-122">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="0564a-123">다른 요구 사항이 있는 경우 [사용자 지정 메서드를 사용](https://jqueryvalidation.org/jQuery.validator.addMethod/)하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-123">If you have different requirements, consider [using a custom method](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>
<span data-ttu-id="0564a-124">기본 제공된 유효성 검사 정규식 패턴을 조정해야 하는 경우 [설명서를 따르세요](https://jqueryvalidation.org/jQuery.validator.methods/).</span><span class="sxs-lookup"><span data-stu-id="0564a-124">In case you need to adjust the built-in validation regular expression patterns, please [follow the documentation](https://jqueryvalidation.org/jQuery.validator.methods/).</span></span>

<span data-ttu-id="0564a-125">**필수 메서드에 대한 중요 정보**.</span><span class="sxs-lookup"><span data-stu-id="0564a-125">**IMPORTANT NOTE ABOUT REQUIRED METHOD**.</span></span> <span data-ttu-id="0564a-126">버전 1.14.0부터 이 플러그 인은 첨부된 요소의 값에서 공백 잘라내기를 중단합니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-126">As of version 1.14.0 this plugin stops trimming white spaces from the value of the attached element.</span></span> <span data-ttu-id="0564a-127">동일한 결과를 얻으려면 유효성 검사 전에 요소의 값을 변환하는 데 사용할 수 있는 [`normalizer`](https://jqueryvalidation.org/normalizer/)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-127">If you want to achieve the same result, you can use the [`normalizer`](https://jqueryvalidation.org/normalizer/) that can be used to transform the value of an element before validation.</span></span> <span data-ttu-id="0564a-128">이 기능은 `v1.15.0` 이후로 사용 가능해졌습니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-128">This feature was available since `v1.15.0`.</span></span> <span data-ttu-id="0564a-129">즉, 다음과 같은 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-129">In other words, you can do something like this:</span></span>
``` js
$("#myForm").validate({
    rules: {
        username: {
            required: true,
            // Using the normalizer to trim the value of the element
            // before validating it.
            //
            // The value of `this` inside the `normalizer` is the corresponding
            // DOMElement. In this example, `this` references the `username` element.
            normalizer: function(value) {
                return $.trim(value);
            }
        }
    }
});
```

## <a name="license"></a><span data-ttu-id="0564a-130">라이선스</span><span class="sxs-lookup"><span data-stu-id="0564a-130">License</span></span>
<span data-ttu-id="0564a-131">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="0564a-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="0564a-132">MIT 라이선스에 따라 사용이 허가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0564a-132">Licensed under the MIT license.</span></span>
