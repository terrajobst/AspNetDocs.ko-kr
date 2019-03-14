---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57064850"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[<span data-ttu-id="048fb-101">오픈 Iconic v1.1.1</span><span class="sxs-lookup"><span data-stu-id="048fb-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a><span data-ttu-id="048fb-102">오픈 Iconic은 [Iconic](http://useiconic.com)의 오픈 소스 형제입니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="048fb-103">부트스트랩 및 Foundation과 함께 사용할 수 있는 아주 작은 공간&mdash;으로 223개의 아이콘을 읽을 수 있는 모음입니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="048fb-104">컬렉션 보기</span><span class="sxs-lookup"><span data-stu-id="048fb-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="048fb-105">오픈 Iconic이란?</span><span class="sxs-lookup"><span data-stu-id="048fb-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="048fb-106">8개의 픽셀까지 읽을 수 있도록 설계된 223개의 아이콘</span><span class="sxs-lookup"><span data-stu-id="048fb-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="048fb-107">매우 간단한 SVG 파일 - 전체 집합의 경우 61.8</span><span class="sxs-lookup"><span data-stu-id="048fb-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="048fb-108">SVG 스프라이트&mdash;아이콘 글꼴을 현대식으로 대체</span><span class="sxs-lookup"><span data-stu-id="048fb-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="048fb-109">Webfont(EOT, OTF, SVG, TTF, WOFF), PNG 및 WebP 형식</span><span class="sxs-lookup"><span data-stu-id="048fb-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="048fb-110">CSS, LESS, SCSS 및 Stylus 형식의 Webfont 스타일시트(부트스트랩 및 Foundation 버전 포함)</span><span class="sxs-lookup"><span data-stu-id="048fb-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="048fb-111">PNG 및 WebP 래스터 이미지(8px, 16px, 24px, 32px, 48px 및 64px).</span><span class="sxs-lookup"><span data-stu-id="048fb-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="048fb-112">시작</span><span class="sxs-lookup"><span data-stu-id="048fb-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a><span data-ttu-id="048fb-113">코드 샘플과 오픈 Iconic을 시작하기 위해 필요한 기타 모든 내용은 [아이콘](http://useiconic.com/open#icons) 및 [참조](http://useiconic.com/open#reference) 섹션을 체크 아웃하세요.</span><span class="sxs-lookup"><span data-stu-id="048fb-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="048fb-114">일반적인 사용법</span><span class="sxs-lookup"><span data-stu-id="048fb-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="048fb-115">오픈 Iconic의 SVG 사용</span><span class="sxs-lookup"><span data-stu-id="048fb-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="048fb-116">SVG를 좋아하며 웹에 아이콘을 표시하는 방법이라고 생각합니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="048fb-117">오픈 Iconic은 기본적인 SVG일 뿐이므로 다른 이미지처럼 표시하는 것이 좋습니다(`alt` 특성을 잊지 말 것).</span><span class="sxs-lookup"><span data-stu-id="048fb-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="048fb-118">오픈 Iconic의 SVG 스프라이트 사용</span><span class="sxs-lookup"><span data-stu-id="048fb-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="048fb-119">오픈 Iconic은 SVG 스프라이트에도 제공되어 단일 요청으로 집합의 모든 아이콘을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="048fb-120">해킹하지 않고도 아이콘 글꼴과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="048fb-121">SVG 스프라이트의 아이콘을 추가하는 것은 사용했던 것과 조금 다르지만 여전히 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="048fb-122">*팁: 아이콘의 스타일을 쉽게 만들려면*  `<svg>` *태그에 일반 클래스 및*  `<use>` *태그에 있는 각기 다른 아이콘에 고유한 클래스 이름을 추가하는 것이 좋습니다.*</span><span class="sxs-lookup"><span data-stu-id="048fb-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="048fb-123">아이콘 크기 조정은 기본 CSS만 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="048fb-124">모든 아이콘은 정사각형 형태이므로 너비와 높이가 동일한 치수로 `<svg>` 태그를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="048fb-125">아이콘 색을 지정하는 것이 훨씬 더 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-125">Coloring icons is even easier.</span></span> <span data-ttu-id="048fb-126">`<use>` 태그에 `fill` 규칙을 설정하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="048fb-127">SVG 스프라이트에 대한 자세한 내용은 [Chris Coyier 가이드](http://css-tricks.com/svg-sprites-use-better-icon-fonts/)를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="048fb-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="048fb-128">오픈 Iconic의 아이콘 글꼴 사용 중...</span><span class="sxs-lookup"><span data-stu-id="048fb-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="048fb-129">...부트스트랩과 함께</span><span class="sxs-lookup"><span data-stu-id="048fb-129">…with Bootstrap</span></span>

<span data-ttu-id="048fb-130">부트스트랩 스타일시트는 `font/css/open-iconic-bootstrap.{css, less, scss, styl}`에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="048fb-131">...Foundation과 함께</span><span class="sxs-lookup"><span data-stu-id="048fb-131">…with Foundation</span></span>

<span data-ttu-id="048fb-132">Foundation 스타일시트는 `font/css/open-iconic-foundation.{css, less, scss, styl}`에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="048fb-133">...자체적으로</span><span class="sxs-lookup"><span data-stu-id="048fb-133">…on its own</span></span>

<span data-ttu-id="048fb-134">기본 스타일시트는 `font/css/open-iconic.{css, less, scss, styl}`에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="048fb-135">라이선스</span><span class="sxs-lookup"><span data-stu-id="048fb-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="048fb-136">아이콘</span><span class="sxs-lookup"><span data-stu-id="048fb-136">Icons</span></span>

<span data-ttu-id="048fb-137">모든 코드(SVG 태그 포함)는 [MIT 라이선스](http://opensource.org/licenses/MIT) 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="048fb-138">글꼴</span><span class="sxs-lookup"><span data-stu-id="048fb-138">Fonts</span></span>

<span data-ttu-id="048fb-139">모든 글꼴은 [SIL 라이선스됨](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web) 아래에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="048fb-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>
