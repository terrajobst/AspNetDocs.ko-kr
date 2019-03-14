---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57028280"
---
# <a name="jquery"></a>jQuery

> jQuery는 빠르고 작고 기능이 풍부한 JavaScript 라이브러리입니다.

jQuery 시작 및 사용 방법에 대한 정보는 [jQuery 설명서](http://api.jquery.com/)를 참조하세요.
소스 파일 및 문제의 경우 [jQuery 리포지토리](https://github.com/jquery/jquery)를 방문하세요.

업그레이드하는 경우 [3.3.1에 대한 블로그 게시물](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/)을 참조하세요. 여기에는 이전 버전과의 차이점과 더 읽기 편한 changelog가 포함됩니다.

## <a name="including-jquery"></a>jQuery 포함

다음은 jQuery를 포함하는 가장 일반적인 방법 중 일부입니다.

### <a name="browser"></a>브라우저

#### <a name="script-tag"></a>스크립트 태그

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a>Babel

[Babel](http://babeljs.io/)은 차세대 JavaScript 컴파일러입니다. 브라우저에서 이 기능을 기본적으로 지원하지 않는데도 지금 ES6/ES2015 모듈을 사용하는 기능이 있습니다.

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a>Browserify/Webpack

[Browserify](http://browserify.org/) 및 [Webpack](https://webpack.github.io/)을 사용하는 방법은 여러 가지입니다. 이러한 도구를 사용하는 방법에 대한 자세한 내용은 해당 프로젝트의 설명서를 참조하세요. 스크립트에서 jQuery를 포함하면 일반적으로 다음과 같습니다.

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a>AMD(비동기 모듈 정의)

AMD는 브라우저용으로 빌드된 모듈 형식입니다. 자세한 내용은 [require.js 설명서](http://requirejs.org/docs/whyamd.html)를 참조하세요.

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a>노드

jQuery를 [Node](nodejs.org)에 포함하려면 먼저 npm을 사용하여 설치합니다.

```sh
npm install jquery
```

Node에서 jQuery를 사용하려면 문서가 있는 창이 필요합니다. Node에는 기본적으로 이러한 창이 없기 때문에 [jsdom](https://github.com/tmpvar/jsdom) 같은 도구로 모의할 수 있습니다. 이는 테스트용으로 유용합니다.

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
