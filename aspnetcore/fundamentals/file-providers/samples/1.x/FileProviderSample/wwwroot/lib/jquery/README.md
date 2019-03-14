---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028280"
---
# <a name="jquery"></a><span data-ttu-id="e8ae3-101">jQuery</span><span class="sxs-lookup"><span data-stu-id="e8ae3-101">jQuery</span></span>

> <span data-ttu-id="e8ae3-102">jQuery는 빠르고 작고 기능이 풍부한 JavaScript 라이브러리입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-102">jQuery is a fast, small, and feature-rich JavaScript library.</span></span>

<span data-ttu-id="e8ae3-103">jQuery 시작 및 사용 방법에 대한 정보는 [jQuery 설명서](http://api.jquery.com/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-103">For information on how to get started and how to use jQuery, please see [jQuery's documentation](http://api.jquery.com/).</span></span>
<span data-ttu-id="e8ae3-104">소스 파일 및 문제의 경우 [jQuery 리포지토리](https://github.com/jquery/jquery)를 방문하세요.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-104">For source files and issues, please visit the [jQuery repo](https://github.com/jquery/jquery).</span></span>

<span data-ttu-id="e8ae3-105">업그레이드하는 경우 [3.3.1에 대한 블로그 게시물](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-105">If upgrading, please see the [blog post for 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span></span> <span data-ttu-id="e8ae3-106">여기에는 이전 버전과의 차이점과 더 읽기 편한 changelog가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-106">This includes notable differences from the previous version and a more readable changelog.</span></span>

## <a name="including-jquery"></a><span data-ttu-id="e8ae3-107">jQuery 포함</span><span class="sxs-lookup"><span data-stu-id="e8ae3-107">Including jQuery</span></span>

<span data-ttu-id="e8ae3-108">다음은 jQuery를 포함하는 가장 일반적인 방법 중 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-108">Below are some of the most common ways to include jQuery.</span></span>

### <a name="browser"></a><span data-ttu-id="e8ae3-109">브라우저</span><span class="sxs-lookup"><span data-stu-id="e8ae3-109">Browser</span></span>

#### <a name="script-tag"></a><span data-ttu-id="e8ae3-110">스크립트 태그</span><span class="sxs-lookup"><span data-stu-id="e8ae3-110">Script tag</span></span>

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a><span data-ttu-id="e8ae3-111">Babel</span><span class="sxs-lookup"><span data-stu-id="e8ae3-111">Babel</span></span>

<span data-ttu-id="e8ae3-112">[Babel](http://babeljs.io/)은 차세대 JavaScript 컴파일러입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-112">[Babel](http://babeljs.io/) is a next generation JavaScript compiler.</span></span> <span data-ttu-id="e8ae3-113">브라우저에서 이 기능을 기본적으로 지원하지 않는데도 지금 ES6/ES2015 모듈을 사용하는 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-113">One of the features is the ability to use ES6/ES2015 modules now, even though browsers do not yet support this feature natively.</span></span>

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a><span data-ttu-id="e8ae3-114">Browserify/Webpack</span><span class="sxs-lookup"><span data-stu-id="e8ae3-114">Browserify/Webpack</span></span>

<span data-ttu-id="e8ae3-115">[Browserify](http://browserify.org/) 및 [Webpack](https://webpack.github.io/)을 사용하는 방법은 여러 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-115">There are several ways to use [Browserify](http://browserify.org/) and [Webpack](https://webpack.github.io/).</span></span> <span data-ttu-id="e8ae3-116">이러한 도구를 사용하는 방법에 대한 자세한 내용은 해당 프로젝트의 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-116">For more information on using these tools, please refer to the corresponding project's documention.</span></span> <span data-ttu-id="e8ae3-117">스크립트에서 jQuery를 포함하면 일반적으로 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-117">In the script, including jQuery will usually look like this...</span></span>

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a><span data-ttu-id="e8ae3-118">AMD(비동기 모듈 정의)</span><span class="sxs-lookup"><span data-stu-id="e8ae3-118">AMD (Asynchronous Module Definition)</span></span>

<span data-ttu-id="e8ae3-119">AMD는 브라우저용으로 빌드된 모듈 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-119">AMD is a module format built for the browser.</span></span> <span data-ttu-id="e8ae3-120">자세한 내용은 [require.js 설명서](http://requirejs.org/docs/whyamd.html)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-120">For more information, we recommend [require.js' documentation](http://requirejs.org/docs/whyamd.html).</span></span>

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a><span data-ttu-id="e8ae3-121">노드</span><span class="sxs-lookup"><span data-stu-id="e8ae3-121">Node</span></span>

<span data-ttu-id="e8ae3-122">jQuery를 [Node](nodejs.org)에 포함하려면 먼저 npm을 사용하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-122">To include jQuery in [Node](nodejs.org), first install with npm.</span></span>

```sh
npm install jquery
```

<span data-ttu-id="e8ae3-123">Node에서 jQuery를 사용하려면 문서가 있는 창이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-123">For jQuery to work in Node, a window with a document is required.</span></span> <span data-ttu-id="e8ae3-124">Node에는 기본적으로 이러한 창이 없기 때문에 [jsdom](https://github.com/tmpvar/jsdom) 같은 도구로 모의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-124">Since no such window exists natively in Node, one can be mocked by tools such as [jsdom](https://github.com/tmpvar/jsdom).</span></span> <span data-ttu-id="e8ae3-125">이는 테스트용으로 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="e8ae3-125">This can be useful for testing purposes.</span></span>

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
