---
ms.openlocfilehash: 3b33bb9bcab1aa7e5438c6fe3f2d7ba0833e7756
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57060820"
---
--

## <a name="reporting-an-issue"></a><span data-ttu-id="c2827-101">문제 신고</span><span class="sxs-lookup"><span data-stu-id="c2827-101">Reporting an Issue</span></span>

1. <span data-ttu-id="c2827-102">해결 중인 문제가 재현 가능한지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c2827-102">Make sure the problem you're addressing is reproducible.</span></span>
2. <span data-ttu-id="c2827-103">http://jsbin.com 또는 http://jsfiddle.net를 사용하여 테스트 페이지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-103">Use http://jsbin.com or http://jsfiddle.net to provide a test page.</span></span>
3. <span data-ttu-id="c2827-104">문제를 재현할 수 있는 브라우저를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-104">Indicate what browsers the issue can be reproduced in.</span></span> <span data-ttu-id="c2827-105">**참고: IE 호환성 모드 문제는 해결 되지 않습니다. 실제 브라우저에서 테스트하세요.**</span><span class="sxs-lookup"><span data-stu-id="c2827-105">**Note: IE Compatibilty mode issues won't be addressed. Make sure you test in a real browser!**</span></span>
4. <span data-ttu-id="c2827-106">문제가 재현될 수 있는 플러그 인 버전</span><span class="sxs-lookup"><span data-stu-id="c2827-106">What version of the plug-in is the issue reproducible in.</span></span> <span data-ttu-id="c2827-107">최신 버전으로 업데이트한 후 재현 가능한지 여부</span><span class="sxs-lookup"><span data-stu-id="c2827-107">Is it reproducible after updating to the latest version.</span></span>

<span data-ttu-id="c2827-108">설명서의 문제도 [jQuery 유효성 검사](https://github.com/jzaefferer/jquery-validation/issues) 문제 추적기에서 추적됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-108">Documentation issues are also tracked at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="c2827-109">설명서를 개선하기 위한 끌어오기 요청은 [jQuery 유효성 검사 설명서](https://github.com/jzaefferer/validation-content) 리포지토리에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-109">Pull Requests to improve the docs are welcome at the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository, though.</span></span>

<span data-ttu-id="c2827-110">**메일 유효성 검사에 대한 중요 참고 사항**</span><span class="sxs-lookup"><span data-stu-id="c2827-110">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="c2827-111">버전 1.12.0에서 이 플러그 인은 [HTML5 사양이 브라우저에 사용하도록 제안](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address)하는 동일한 정규식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-111">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="c2827-112">지침을 따르고 동일한 검사를 사용할 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-112">We will follow their lead and use the same check.</span></span> <span data-ttu-id="c2827-113">사양이 잘못되었다고 생각되면 문제를 보고하세요.</span><span class="sxs-lookup"><span data-stu-id="c2827-113">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="c2827-114">다른 요구 사항이 있는 경우 [사용자 지정 메서드를 사용](http://jqueryvalidation.org/jQuery.validator.addMethod/)하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-114">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="contributing-code"></a><span data-ttu-id="c2827-115">코드 참여</span><span class="sxs-lookup"><span data-stu-id="c2827-115">Contributing code</span></span>

<span data-ttu-id="c2827-116">참여해 주셔서 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-116">Thanks for contributing!</span></span> <span data-ttu-id="c2827-117">다음은 귀하의 참여에 도움이 되는 몇 가지 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-117">Here's a few guidelines to help your contribution get landed.</span></span>

1. <span data-ttu-id="c2827-118">해결 중인 문제가 재현 가능한지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="c2827-118">Make sure the problem you're addressing is reproducible.</span></span> <span data-ttu-id="c2827-119">jsbin.com 또는 jsfiddle.net을 사용하여 테스트 페이지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-119">Use jsbin.com or jsfiddle.net to provide a test page.</span></span>
2. <span data-ttu-id="c2827-120">[jQuery 스타일 가이드](http://contribute.jquery.com/style-guides/js)를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-120">Follow the [jQuery style guide](http://contribute.jquery.com/style-guides/js)</span></span>
3. <span data-ttu-id="c2827-121">패치와 함께 단위 테스트를 추가하거나 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-121">Add or update unit tests along with your patch.</span></span> <span data-ttu-id="c2827-122">최소한 하나의 브라우저에서 단위 테스트를 실행합니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="c2827-122">Run the unit tests in at least one browser (see below).</span></span>
4. <span data-ttu-id="c2827-123">`grunt`(아래 참조)를 실행하여 lint 및 기타 문제가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-123">Run `grunt` (see below) to check for linting and a few other issues.</span></span>
5. <span data-ttu-id="c2827-124">커밋 메시지의 변경 내용을 설명 하 고 다음과 같이 티켓을 참조 합니다. "데모: dynamic-totals 데모에 대한 대리자 버그를 수정했습니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-124">Describe the change in your commit message and reference the ticket, like this: "Demos: Fixed delegate bug for dynamic-totals demo.</span></span> <span data-ttu-id="c2827-125">Fixes #51”.</span><span class="sxs-lookup"><span data-stu-id="c2827-125">Fixes #51".</span></span> <span data-ttu-id="c2827-126">새 지역화 파일을 추가 하는 경우 다음과 같은 코드를 사용 합니다. "지역화 합니다. 추가 크로아티아어 (HR) 지역화 "</span><span class="sxs-lookup"><span data-stu-id="c2827-126">If you're adding a new localization file, use something like this: "Localization: Added croatian (HR) localization"</span></span>

## <a name="build-setup"></a><span data-ttu-id="c2827-127">빌드 설치</span><span class="sxs-lookup"><span data-stu-id="c2827-127">Build setup</span></span>

1. <span data-ttu-id="c2827-128">[NodeJS](http://nodejs.org)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-128">Install [NodeJS](http://nodejs.org).</span></span>
2. <span data-ttu-id="c2827-129">`npm install -g grunt-cli`를 실행하여 Grunt CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-129">Install the Grunt CLI To install by running `npm install -g grunt-cli`.</span></span> <span data-ttu-id="c2827-130">자세한 내용은 웹 사이트 http://gruntjs.com/getting-started에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-130">More details are available on their website http://gruntjs.com/getting-started.</span></span>
3. <span data-ttu-id="c2827-131">`npm install`을 실행하여 NPM 종속성을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-131">Install the NPM dependencies by running `npm install`.</span></span>
4. <span data-ttu-id="c2827-132">이제 `grunt`를 실행하여 빌드를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-132">The build can now be called by running `grunt`.</span></span>

## <a name="creating-a-new-additional-method"></a><span data-ttu-id="c2827-133">새 추가 메서드 만들기</span><span class="sxs-lookup"><span data-stu-id="c2827-133">Creating a new Additional Method</span></span>

<span data-ttu-id="c2827-134">additional-methods.js에서 참여하려는 사용자 지정 메서드를 작성한 경우:</span><span class="sxs-lookup"><span data-stu-id="c2827-134">If you've wrote custom methods that you'd like to contribute to additional-methods.js:</span></span>

1. <span data-ttu-id="c2827-135">분기 만들기</span><span class="sxs-lookup"><span data-stu-id="c2827-135">Create a branch</span></span>
2. <span data-ttu-id="c2827-136">메서드를 `src/additional`에 새 파일로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-136">Add the method as a new file in `src/additional`</span></span>
3. <span data-ttu-id="c2827-137">(선택 사항) `src/localization`에 번역을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-137">(Optional) Add translations to `src/localization`</span></span>
4. <span data-ttu-id="c2827-138">마스터 분기에 끌어오기 요청을 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-138">Send a pull request to the master branch.</span></span>

## <a name="unit-tests"></a><span data-ttu-id="c2827-139">단위 테스트</span><span class="sxs-lookup"><span data-stu-id="c2827-139">Unit Tests</span></span>

<span data-ttu-id="c2827-140">단위 테스트를 실행하려면 브라우저에서 `test/index.html`을 열기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-140">To run unit tests, just open `test/index.html` within your browser.</span></span> <span data-ttu-id="c2827-141">필요한 모든 종속성을 사용할 수 있도록 하려면 먼저 `npm install`을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-141">Make sure you ran `npm install` before so all required dependencies are available.</span></span>
<span data-ttu-id="c2827-142">수정 사항을 개발할 때는 브라우저 하나로 작업하다가 다른 브라우저에서도 실행한 후에 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-142">Start with one browser while developing the fix, then run against others before committing.</span></span> <span data-ttu-id="c2827-143">일반적으로 최신 Chrome, Firefox, Safari 및 Opera와 일부 IE를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-143">Usually latest Chrome, Firefox, Safari and Opera and a few IEs.</span></span>

## <a name="documentation"></a><span data-ttu-id="c2827-144">설명서</span><span class="sxs-lookup"><span data-stu-id="c2827-144">Documentation</span></span>

<span data-ttu-id="c2827-145">[jQuery 유효성 검사](https://github.com/jzaefferer/jquery-validation/issues) 문제 추적기에서 설명서 문제를 보고하세요.</span><span class="sxs-lookup"><span data-stu-id="c2827-145">Please report documentation issues at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="c2827-146">끌어오기 요청이 공용 API를 구현하거나 변경하는 경우 [jQuery 유효성 검사 설명서](https://github.com/jzaefferer/validation-content) 리포지토리에 대한 끌어오기 요청도 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2827-146">In case your pull request implements or changes public API it would be a plus you would provide a pull request against the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository.</span></span>

## <a name="linting"></a><span data-ttu-id="c2827-147">Lint</span><span class="sxs-lookup"><span data-stu-id="c2827-147">Linting</span></span>

<span data-ttu-id="c2827-148">JSHint 및 기타 도구를 실행하려면 `grunt`를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="c2827-148">To run JSHint and other tools, use `grunt`.</span></span>
