---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 캐시 된 페이지에 동적 콘텐츠 추가 (C#) | Microsoft Docs
author: microsoft
description: 동일한 페이지에서 동적 및 캐시 된 콘텐츠를 혼합 하는 방법에 대해 알아봅니다. 캐시 후 대체를 사용 하 여 배너 광고 o와 같은 동적 콘텐츠를 표시할 수 있습니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: be43712d3dd5235117558e991d9dd71aa30ec470
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78486941"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a>캐시된 페이지에 동적 콘텐츠 추가(C#)

[Microsoft](https://github.com/microsoft) 에서

> 동일한 페이지에서 동적 및 캐시 된 콘텐츠를 혼합 하는 방법에 대해 알아봅니다. 캐시 후 대체를 사용 하면 출력이 캐시 된 페이지 내에서 배너 광고 또는 뉴스 항목과 같은 동적 콘텐츠를 표시할 수 있습니다.

출력 캐싱을 활용 하면 ASP.NET MVC 응용 프로그램의 성능을 크게 향상 시킬 수 있습니다. 페이지가 요청 될 때마다 페이지를 다시 생성 하는 대신 페이지를 한 번 생성 하 고 여러 사용자를 위해 메모리에 캐시할 수 있습니다.

하지만 문제가 있습니다. 페이지에 동적 콘텐츠를 표시 해야 하는 경우 어떻게 하나요? 예를 들어 페이지에 배너 광고를 표시 하려고 한다고 가정 합니다. 모든 사용자가 동일한 보급 알림을 볼 수 있도록 배너 보급 알림이 캐시 되는 것을 원하지 않습니다. 그렇게 하는 것은 아닙니다.

다행히 쉬운 솔루션이 있습니다. *사후 캐시 대체*라는 ASP.NET 프레임 워크의 기능을 활용할 수 있습니다. 캐시 후 대체를 사용 하 여 메모리에 캐시 된 페이지에서 동적 콘텐츠를 대체할 수 있습니다.

일반적으로 [OutputCache] 특성을 사용 하 여 페이지 캐시를 출력 하면 페이지가 서버와 클라이언트 (웹 브라우저) 모두에 캐시 됩니다. 사후 캐시 대체를 사용 하는 경우 페이지는 서버에만 캐시 됩니다.

#### <a name="using-post-cache-substitution"></a>사후 캐시 대체 사용

사후 캐시 대체를 사용 하려면 두 단계가 필요 합니다. 먼저 캐시 된 페이지에 표시 하려는 동적 콘텐츠를 나타내는 문자열을 반환 하는 메서드를 정의 해야 합니다. 다음으로 Httpresponse.cache () 메서드를 호출 하 여 페이지에 동적 콘텐츠를 삽입 합니다.

예를 들어 캐시 된 페이지에 다른 뉴스 항목을 임의로 표시 하려는 경우를 가정해 보겠습니다. 목록 1의 클래스는 RenderNews () 라는 단일 메서드를 노출 하 여 세 개의 뉴스 항목 목록에서 뉴스 항목 하나를 임의로 반환 합니다.

**목록 1 – Models\News.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

사후 캐시 대체를 활용 하려면 WriteSubstitution () 메서드를 호출 Httpresponse.cache. WriteSubstitution () 메서드는 캐시 된 페이지의 영역을 동적 콘텐츠로 바꾸도록 코드를 설정 합니다. WriteSubstitution () 메서드는 목록 2의 보기에 임의의 뉴스 항목을 표시 하는 데 사용 됩니다.

**목록 2 – Views\Home\Index.aspx**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

RenderNews 메서드는 WriteSubstitution () 메서드에 전달 됩니다. RenderNews 메서드는 호출 되지 않습니다 (괄호 없음). 대신 메서드에 대 한 참조는 WriteSubstitution ()에 전달 됩니다.

인덱스 뷰가 캐시 됩니다. 뷰는 컨트롤러에서 목록 3에 의해 반환 됩니다. Index () 동작은 인덱스 보기가 60 초 동안 캐시 되도록 하는 [OutputCache] 특성으로 데코 레이트 됩니다.

**목록 3 – Controllers\ homecontroller.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

인덱스 뷰가 캐시 된 경우에도 인덱스 페이지를 요청 하면 다른 임의의 뉴스 항목이 표시 됩니다. 인덱스 페이지를 요청 하는 경우 페이지에 표시 되는 시간은 60 초 동안 변경 되지 않습니다 (그림 1 참조). 시간이 변경 되지 않는다는 사실은 페이지가 캐시 되었음을 증명 합니다. 그러나 WriteSubstitution () 메서드에 의해 삽입 된 콘텐츠 (임의 뉴스 항목)는 각 요청과 함께 변경 됩니다.

**그림 1-캐시 된 페이지에 동적 뉴스 항목 삽입**

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a>도우미 메서드에서 캐시 후 대체 사용

사후 캐시 대체를 활용 하는 보다 쉬운 방법은 사용자 지정 도우미 메서드 내에서 WriteSubstitution () 메서드에 대 한 호출을 캡슐화 하는 것입니다. 이 방법은 목록 4의 도우미 메서드에 의해 설명 됩니다.

**목록 4 – AdHelper.cs**

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

목록 4에는 RenderBanner ()와 RenderBannerInternal () 라는 두 개의 메서드를 노출 하는 정적 클래스가 있습니다. RenderBanner () 메서드는 실제 도우미 메서드를 나타냅니다. 이 메서드는 다른 도우미 메서드와 마찬가지로 뷰에서 Html RenderBanner ()를 호출할 수 있도록 표준 ASP.NET MVC HtmlHelper 클래스를 확장 합니다.

RenderBanner () 메서드는 RenderBannerInternal () 메서드를 WriteSubstitution () 메서드에 전달 하는 WriteSubstitution () 메서드를 호출 합니다.

RenderBannerInternal () 메서드는 전용 메서드입니다. 이 메서드는 도우미 메서드로 노출 되지 않습니다. RenderBannerInternal () 메서드는 세 개의 배너 광고 이미지 목록에서 하나의 배너 광고 이미지를 임의로 반환 합니다.

목록 5의 수정 된 인덱스 뷰는 RenderBanner () 도우미 메서드를 사용 하는 방법을 보여 줍니다. MvcApplication1 네임 스페이스를 가져오기 위해 추가 &lt;% @ Import%&gt; 지시어가 뷰의 맨 위에 포함 됩니다. 이 네임 스페이스를 가져오지 않는 경우 RenderBanner () 메서드는 Html 속성에 메서드로 표시 되지 않습니다.

**목록 5 – Views\Home\Index.aspx (RenderBanner () 메서드 포함)**

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

목록 5에서 보기에 의해 렌더링 된 페이지를 요청 하면 각 요청과 함께 다른 배너 알림이 표시 됩니다 (그림 2 참조). 페이지가 캐시 되지만 배너 보급 알림은 RenderBanner () 도우미 메서드에 의해 동적으로 삽입 됩니다.

**그림 2 – 무작위 배너 광고를 표시 하는 인덱스 뷰**

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a>요약

이 자습서에서는 캐시 된 페이지의 콘텐츠를 동적으로 업데이트 하는 방법에 대해 설명 했습니다. WriteSubstitution () 메서드를 사용 하 여 캐시 된 페이지에 동적 콘텐츠를 삽입할 수 있도록 설정 하는 방법을 배웠습니다 Httpresponse.cache. 또한 HTML 도우미 메서드 내에서 WriteSubstitution () 메서드에 대 한 호출을 캡슐화 하는 방법을 배웠습니다.

가능 하면 캐시 활용 – 웹 응용 프로그램의 성능에 큰 영향을 줄 수 있습니다. 이 자습서에 설명 된 대로 페이지에 동적 콘텐츠를 표시 해야 하는 경우에도 캐싱을 활용할 수 있습니다.

> [!div class="step-by-step"]
> [이전](improving-performance-with-output-caching-cs.md)
> [다음](creating-a-controller-cs.md)
