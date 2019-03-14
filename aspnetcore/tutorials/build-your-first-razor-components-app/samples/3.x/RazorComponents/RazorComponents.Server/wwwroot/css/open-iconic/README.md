---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064850"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[오픈 Iconic v1.1.1](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a>오픈 Iconic은 [Iconic](http://useiconic.com)의 오픈 소스 형제입니다. 부트스트랩 및 Foundation과 함께 사용할 수 있는 아주 작은 공간&mdash;으로 223개의 아이콘을 읽을 수 있는 모음입니다. [컬렉션 보기](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>오픈 Iconic이란?

* 8개의 픽셀까지 읽을 수 있도록 설계된 223개의 아이콘
* 매우 간단한 SVG 파일 - 전체 집합의 경우 61.8 
* SVG 스프라이트&mdash;아이콘 글꼴을 현대식으로 대체
* Webfont(EOT, OTF, SVG, TTF, WOFF), PNG 및 WebP 형식
* CSS, LESS, SCSS 및 Stylus 형식의 Webfont 스타일시트(부트스트랩 및 Foundation 버전 포함)
* PNG 및 WebP 래스터 이미지(8px, 16px, 24px, 32px, 48px 및 64px).


## <a name="getting-started"></a>시작

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a>코드 샘플과 오픈 Iconic을 시작하기 위해 필요한 기타 모든 내용은 [아이콘](http://useiconic.com/open#icons) 및 [참조](http://useiconic.com/open#reference) 섹션을 체크 아웃하세요.

### <a name="general-usage"></a>일반적인 사용법

#### <a name="using-open-iconics-svgs"></a>오픈 Iconic의 SVG 사용

SVG를 좋아하며 웹에 아이콘을 표시하는 방법이라고 생각합니다. 오픈 Iconic은 기본적인 SVG일 뿐이므로 다른 이미지처럼 표시하는 것이 좋습니다(`alt` 특성을 잊지 말 것).

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>오픈 Iconic의 SVG 스프라이트 사용

오픈 Iconic은 SVG 스프라이트에도 제공되어 단일 요청으로 집합의 모든 아이콘을 표시할 수 있습니다. 해킹하지 않고도 아이콘 글꼴과 같습니다.

SVG 스프라이트의 아이콘을 추가하는 것은 사용했던 것과 조금 다르지만 여전히 쉽습니다. *팁: 아이콘의 스타일을 쉽게 만들려면*  `<svg>` *태그에 일반 클래스 및*  `<use>` *태그에 있는 각기 다른 아이콘에 고유한 클래스 이름을 추가하는 것이 좋습니다.*  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

아이콘 크기 조정은 기본 CSS만 필요합니다. 모든 아이콘은 정사각형 형태이므로 너비와 높이가 동일한 치수로 `<svg>` 태그를 설정합니다.

```
.icon {
  width: 16px;
  height: 16px;
}
```

아이콘 색을 지정하는 것이 훨씬 더 쉽습니다. `<use>` 태그에 `fill` 규칙을 설정하기만 하면 됩니다.

```
.icon-account-login {
  fill: #f00;
}
```

SVG 스프라이트에 대한 자세한 내용은 [Chris Coyier 가이드](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)를 읽어보세요.

#### <a name="using-open-iconics-icon-font"></a>오픈 Iconic의 아이콘 글꼴 사용 중...


##### <a name="with-bootstrap"></a>...부트스트랩과 함께

부트스트랩 스타일시트는 `font/css/open-iconic-bootstrap.{css, less, scss, styl}`에서 찾을 수 있습니다.


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>...Foundation과 함께

Foundation 스타일시트는 `font/css/open-iconic-foundation.{css, less, scss, styl}`에서 찾을 수 있습니다.

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>...자체적으로

기본 스타일시트는 `font/css/open-iconic.{css, less, scss, styl}`에서 찾을 수 있습니다.

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>라이선스

### <a name="icons"></a>아이콘

모든 코드(SVG 태그 포함)는 [MIT 라이선스](http://opensource.org/licenses/MIT) 아래에 있습니다.

### <a name="fonts"></a>글꼴

모든 글꼴은 [SIL 라이선스됨](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web) 아래에 있습니다.
