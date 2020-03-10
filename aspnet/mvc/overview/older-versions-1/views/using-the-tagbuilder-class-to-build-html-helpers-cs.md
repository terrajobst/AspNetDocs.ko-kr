---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: 빌드하는 tagbuilder 클래스를 사용 하 여 HTML 도우미 빌드C#() | Microsoft Docs
author: StephenWalther
description: Stephen Walther는 빌드하는 tagbuilder 클래스 라는 ASP.NET MVC 프레임 워크에서 유용한 유틸리티 클래스를 소개 합니다. 빌드하는 tagbuilder 클래스를 사용 하 여 쉽게 수행할 수 있습니다.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: c8eaea9932a30c744b9a69861619ce9458b5a23a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485609"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a>빌드하는 tagbuilder 클래스를 사용 하 여 HTML 도우미 (C#) 빌드

[Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther는 빌드하는 tagbuilder 클래스 라는 ASP.NET MVC 프레임 워크에서 유용한 유틸리티 클래스를 소개 합니다. 빌드하는 tagbuilder 클래스를 사용 하 여 HTML 태그를 쉽게 빌드할 수 있습니다.

ASP.NET MVC 프레임 워크에는 HTML 도우미를 빌드할 때 사용할 수 있는 빌드하는 tagbuilder 클래스 라는 유용한 유틸리티 클래스가 포함 되어 있습니다. 클래스 이름으로 빌드하는 tagbuilder 클래스를 사용 하면 HTML 태그를 쉽게 빌드할 수 있습니다. 이 간략 한 자습서에서는 빌드하는 tagbuilder 클래스에 대 한 개요를 제공 하 고, HTML &lt;img&gt; 태그를 렌더링 하는 간단한 HTML 도우미를 빌드할 때이 클래스를 사용 하는 방법을 알아봅니다.

## <a name="overview-of-the-tagbuilder-class"></a>빌드하는 tagbuilder 클래스 개요

빌드하는 tagbuilder 클래스는 System.web 네임 스페이스에 포함 되어 있습니다. 다음과 같은 5 가지 메서드가 있습니다.

- AddCssClass ()-새 *class = ""* 특성을 태그에 추가할 수 있습니다.
- GenerateId ()-태그에 id 특성을 추가할 수 있습니다. 이 메서드는 자동으로 id의 마침표를 바꿉니다 (기본적으로 마침표는 밑줄로 바뀜).
- MergeAttribute ()-태그에 특성을 추가할 수 있습니다. 이 메서드의 오버 로드가 여러 개 있습니다.
- SetInnerText ()-태그의 내부 텍스트를 설정할 수 있습니다. 내부 텍스트는 자동으로 인코딩됩니다.
- ToString ()-태그를 렌더링할 수 있습니다. 일반 태그, 시작 태그, 끝 태그 또는 자체 닫는 태그를 만들지 여부를 지정할 수 있습니다.

빌드하는 tagbuilder 클래스에는 다음과 같은 네 가지 중요 한 속성이 있습니다.

- 특성-태그의 모든 특성을 나타냅니다.
- IdAttributeDotReplacement-GenerateId () 메서드가 마침표를 대체 하는 데 사용 하는 문자를 나타냅니다 (기본값은 밑줄).
- InnerHTML-태그의 내부 콘텐츠를 나타냅니다. 문자열을이 속성에 할당 하면 문자열을 HTML로 *인코딩하지 않습니다.*
- TagName-태그의 이름을 나타냅니다.

이러한 메서드와 속성은 HTML 태그를 작성 하는 데 필요한 모든 기본 메서드 및 속성을 제공 합니다. 빌드하는 tagbuilder 클래스를 반드시 사용할 필요는 없습니다. 대신 StringBuilder 클래스를 사용할 수 있습니다. 그러나 빌드하는 tagbuilder 클래스를 사용 하면 좀 더 쉽게 사용할 수 있습니다.

## <a name="creating-an-image-html-helper"></a>이미지 HTML 도우미 만들기

빌드하는 tagbuilder 클래스의 인스턴스를 만들 때 빌드하는 tagbuilder 생성자에 빌드 하려는 태그의 이름을 전달 합니다. 그런 다음 AddCssClass 및 MergeAttribute () 메서드와 같은 메서드를 호출 하 여 태그의 특성을 수정할 수 있습니다. 마지막으로 ToString () 메서드를 호출 하 여 태그를 렌더링 합니다.

예를 들어 목록 1에는 이미지 HTML 도우미가 포함 되어 있습니다. 이미지 도우미는 HTML &lt;img&gt; 태그를 나타내는 빌드하는 tagbuilder를 사용 하 여 내부적으로 구현 됩니다.

**목록 1-Helpers\ImageHelper.cs**

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

1을 나열 하는 클래스에는 Image 라는 두 개의 정적 오버 로드 된 메서드가 포함 되어 있습니다. Image () 메서드를 호출 하는 경우 HTML 특성 집합을 나타내는 개체를 전달할 수 있습니다.

빌드하는 tagbuilder. MergeAttribute () 메서드를 사용 하 여 src 특성과 같은 개별 특성을 빌드하는 tagbuilder에 추가 하는 방법을 확인 합니다. 또한 빌드하는 tagbuilder. MergeAttributes () 메서드를 사용 하 여 빌드하는 tagbuilder에 특성 컬렉션을 추가 하는 방법도 살펴봅니다. MergeAttributes () 메서드는 Dictionary&lt;string, object&gt; 매개 변수를 허용 합니다. RouteValueDictionary 클래스는 특성의 컬렉션을 나타내는 개체를 사전&lt;문자열, 개체&gt;로 변환 하는 데 사용 됩니다.

이미지 도우미를 만든 후에는 다른 표준 HTML 도우미와 마찬가지로 ASP.NET MVC 뷰에서 도우미를 사용할 수 있습니다. 목록 2의 보기는 이미지 도우미를 사용 하 여 Xbox의 동일한 이미지를 두 번 표시 합니다 (그림 1 참조). Image () 도우미는 HTML 특성 컬렉션을 사용 하거나 사용 하지 않고 모두 호출 됩니다.

**목록 2-Home\Index.aspx**

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]

[새 프로젝트 대화 상자 ![](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)

**그림 01**: 이미지 도우미 사용 ([전체 크기 이미지를 보려면 클릭](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))

Index .aspx 뷰의 맨 위에 있는 이미지 도우미와 연결 된 네임 스페이스를 가져와야 합니다. 도우미는 다음 지시문을 사용 하 여 가져옵니다.

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> [이전](creating-custom-html-helpers-cs.md)
> [다음](creating-page-layouts-with-view-master-pages-cs.md)
