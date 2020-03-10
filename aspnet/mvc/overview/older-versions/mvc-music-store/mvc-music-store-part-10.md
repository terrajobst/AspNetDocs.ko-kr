---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
title: '10 부: 탐색 및 사이트 디자인에 대 한 최종 업데이트, 결론 | Microsoft Docs'
author: jongalloway
description: 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 10 부에서는 탐색 및의 최종 업데이트를 다룹니다.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 0c6e4c2f-fcdb-4978-9656-1990c6f15727
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-10
msc.type: authoredcontent
ms.openlocfilehash: f701d1fbabc3e1a97c3750d00e96bf8dba1105cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78433613"
---
# <a name="part-10-final-updates-to-navigation-and-site-design-conclusion"></a>10 부: 탐색 및 사이트 디자인에 대 한 최종 업데이트, 결론

받은 사람 ( [Jon Galloway](https://github.com/jongalloway) )

> MVC Music Store는 웹 개발용 ASP.NET MVC 및 Visual Studio를 사용 하는 방법을 단계별로 소개 하 고 설명 하는 자습서 응용 프로그램입니다.  
>   
> MVC Music Store는 온라인으로 음악 앨범을 판매 하 고 기본적인 사이트 관리, 사용자 로그인 및 쇼핑 카트 기능을 구현 하는 간단한 샘플 저장소 구현입니다.  
>   
> 이 자습서 시리즈에서는 ASP.NET MVC Music Store 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 10 부에서는 탐색 및 사이트 디자인, 결론의 최종 업데이트를 다룹니다.

사이트에 대 한 모든 주요 기능을 완료 했지만 사이트 탐색, 홈 페이지 및 스토어 찾아보기 페이지에 몇 가지 기능을 추가할 수 있습니다.

## <a name="creating-the-shopping-cart-summary-partial-view"></a>쇼핑 카트 요약 부분 보기 만들기

전체 사이트에서 사용자의 쇼핑 카트에 있는 항목 수를 표시 하려고 합니다.

![](mvc-music-store-part-10/_static/image1.png)

사이트 마스터에 추가 되는 부분 보기를 만들어이를 쉽게 구현할 수 있습니다.

앞에서 설명한 것 처럼 ShoppingCart 컨트롤러에는 부분 뷰를 반환 하는 CartSummary 동작 메서드가 포함 되어 있습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample1.cs)]

CartSummary 부분 보기를 만들려면 Views/ShoppingCart 폴더를 마우스 오른쪽 단추로 클릭 하 고 뷰 추가를 선택 합니다. 보기의 이름을 CartSummary로 표시 하 고 아래와 같이 "부분 보기 만들기" 확인란을 선택 합니다.

![](mvc-music-store-part-10/_static/image2.png)

CartSummary 부분 보기는 정말 간단 합니다. 장바구니의 항목 수를 보여 주는 ShoppingCart Index 뷰에 대 한 링크 일 뿐입니다. CartSummary. cshtml의 전체 코드는 다음과 같습니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample2.cshtml)]

Html RenderAction 메서드를 사용 하 여 사이트 마스터를 포함 하 여 사이트의 모든 페이지에 부분 보기를 포함할 수 있습니다. RenderAction을 사용 하려면 아래와 같이 작업 이름 ("CartSummary") 및 컨트롤러 이름 ("ShoppingCart")을 지정 해야 합니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample3.cshtml)]

이를 사이트 레이아웃에 추가 하기 전에 모든 사이트를 한 번에 변경할 수 있도록 장르 메뉴도 만듭니다.

## <a name="creating-the-genre-menu-partial-view"></a>장르 메뉴 부분 보기 만들기

스토어에서 사용할 수 있는 장르를 모두 나열 하는 장르 메뉴를 추가 하 여 사용자가 스토어를 탐색 하는 것이 훨씬 더 쉬워질 수 있습니다.

![](mvc-music-store-part-10/_static/image3.png)

동일한 단계를 수행 하 여 GenreMenu 부분 보기를 만든 다음 두 항목을 모두 사이트 마스터에 추가할 수 있습니다. 먼저 StoreController에 다음 GenreMenu 컨트롤러 작업을 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample4.cs)]

이 작업은 부분 보기에 표시 되는 장르 목록을 반환 합니다. 여기에서 다음을 만듭니다.

*참고:이 컨트롤러 작업에는 [ChildActionOnly] 특성을 추가 했습니다 .이 작업은 부분 보기 에서만이 작업을 사용 하도록 합니다. 이 특성은/Store/GenreMenu. 이동 하 여 컨트롤러 작업을 실행할 수 없도록 합니다. 이는 부분 보기에는 필요 하지 않지만 컨트롤러 작업이 의도 한 대로 사용 되는지 확인 하는 것이 좋습니다. 또한 뷰가 아닌 PartialView를 반환 합니다 .이는 다른 보기에 포함 되어 있으므로이 뷰에 대 한 레이아웃을 사용 하지 않아야 함을 알 수 있습니다.*

GenreMenu 컨트롤러 작업을 마우스 오른쪽 단추로 클릭 하 고 아래와 같이 장르 뷰 데이터 클래스를 사용 하 여 강력한 형식의 GenreMenu 라는 부분 뷰를 만듭니다.

![](mvc-music-store-part-10/_static/image4.png)

다음과 같이 순서가 지정 되지 않은 목록을 사용 하 여 항목을 표시 하도록 GenreMenu 부분 뷰에 대 한 뷰 코드를 업데이트 합니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample5.cshtml)]

## <a name="updating-site-layout-to-display-our-partial-views"></a>부분 보기를 표시 하도록 사이트 레이아웃 업데이트

Html RenderAction ()을 호출 하 여 사이트 레이아웃 (/Views/Shared/\_Layout. cshtml)에 부분 보기를 추가할 수 있습니다. 아래와 같이에서 추가 태그를 추가 하 고 표시 하는 몇 가지 추가 태그를 추가 합니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample6.cshtml)]

이제 응용 프로그램을 실행할 때 왼쪽 탐색 영역에 장르를 표시 하 고 맨 위에 카트 요약을 표시 합니다.

## <a name="update-to-the-store-browse-page"></a>스토어 찾아보기 페이지로 업데이트

저장소 찾아보기 페이지가 작동 하지만 매우 양호 하지 않습니다. 다음과 같이 보기 코드 (/Views/Store/Browse.cshtml에 있음)를 업데이트 하 여 앨범을 더 나은 레이아웃으로 표시 하도록 페이지를 업데이트할 수 있습니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample7.cshtml)]

여기서는 Url을 사용 합니다. 즉, 링크에 특별 한 서식을 적용 하 여 앨범 아트 워크를 포함할 수 있습니다.

*참고: 이러한 앨범에 대 한 일반 앨범 커버를 표시 합니다. 이 정보는 데이터베이스에 저장 되며 저장소 관리자를 통해 편집할 수 있습니다. 사용자 고유의 아트 워크를 추가 하는 것을 환영 합니다.*

이제 장르를 찾으면 앨범 아트 워크가 있는 그리드에 표시 되는 앨범이 표시 됩니다.

![](mvc-music-store-part-10/_static/image5.png)

## <a name="updating-the-home-page-to-show-top-selling-albums"></a>홈 페이지를 업데이트 하 여 상위 판매 앨범 표시

판매를 늘리기 위해 홈 페이지에서 상위 판매 앨범을 기능 하려고 합니다. HomeController를 처리 하기 위해 몇 가지 업데이트를 수행 하 고 몇 가지 추가 그래픽도 추가 합니다.

먼저, EntityFramework가 연결 된 것을 알 수 있도록 앨범 클래스에 탐색 속성을 추가 합니다. 이제 **앨범** 클래스의 마지막 몇 줄은 다음과 같습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample8.cs)]

*참고:이 작업을 수행 하려면 using 문을 추가 하 여 system.xml 네임 스페이스를 가져와야 합니다.*

먼저 다른 컨트롤러에서와 같이 문을 사용 하 여 storeDB 필드와 MvcMusicStore를 추가 합니다. 다음으로, OrderDetails에 따라 가장 인기 있는 앨범을 찾기 위해 데이터베이스를 쿼리 하는 HomeController에 다음 메서드를 추가 합니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample9.cs)]

이것은 컨트롤러 작업으로 사용할 수 있도록 설정 하지 않기 때문에 전용 메서드입니다. 편의를 위해 HomeController에 포함 하는 것이 좋지만 비즈니스 논리를 별도의 서비스 클래스로 이동 하는 것이 좋습니다.

이렇게 하면 인덱스 컨트롤러 작업을 업데이트 하 여 상위 5 개 판매 된 앨범을 쿼리하고 뷰로 돌아갈 수 있습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample10.cs)]

업데이트 된 HomeController에 대 한 전체 코드는 다음과 같습니다.

[!code-csharp[Main](mvc-music-store-part-10/samples/sample11.cs)]

마지막으로, 모델 유형을 업데이트 하 고 아래쪽에 앨범 목록을 추가 하 여 앨범 목록을 표시할 수 있도록 홈 인덱스 보기를 업데이트 해야 합니다. 이 기회를 통해 페이지에 제목 및 판촉 섹션을 추가할 수 있습니다.

[!code-cshtml[Main](mvc-music-store-part-10/samples/sample12.cshtml)]

이제 응용 프로그램을 실행할 때 인기 있는 앨범 및 판촉 메시지를 포함 하는 업데이트 된 홈 페이지가 표시 됩니다.

![](mvc-music-store-part-10/_static/image1.jpg)

## <a name="conclusion"></a>결론

ASP.NET MVC를 사용 하면 데이터베이스 액세스, 멤버 자격, AJAX 등의 복잡 한 웹 사이트를 쉽게 만들 수 있습니다. 매우 빠르게 합니다. 이 자습서에서는 사용자 고유의 ASP.NET MVC 응용 프로그램 빌드를 시작 하는 데 필요한 도구를 제공 하는 데 도움을 바랍니다.

> [!div class="step-by-step"]
> [이전](mvc-music-store-part-9.md)
