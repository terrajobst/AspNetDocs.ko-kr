---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-vb
title: 마스터 페이지의 Url (VB) | Microsoft Docs
author: rick-anderson
description: 마스터 페이지 파일이 콘텐츠 페이지와 다른 상대 디렉터리에 있기 때문에 마스터 페이지의 Url이 중단 되는 방법을 다룹니다. 의 기준 주소를 찾습니다.
ms.author: riande
ms.date: 06/10/2008
ms.assetid: 43d1e83c-0092-4dcf-977c-e709c4dce7c3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 01627988f68bb619969a5fe3cfaae68fe70b5d4f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588222"
---
# <a name="urls-in-master-pages-vb"></a>마스터 페이지의 URL(VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_VB.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_VB.pdf)

> 마스터 페이지 파일이 콘텐츠 페이지와 다른 상대 디렉터리에 있기 때문에 마스터 페이지의 Url이 중단 되는 방법을 다룹니다. 선언 구문에서 ~를 통해의 기준 주소 Url을 확인 하 고 프로그래밍 방식으로 ResolveUrl 및 ResolveClientUrl를 사용 합니다. (참고 항목

## <a name="introduction"></a>소개

지금까지 살펴본 모든 예제에서 마스터 및 콘텐츠 페이지는 동일한 폴더 (웹 사이트의 루트 폴더)에 있습니다. 그러나 마스터 및 콘텐츠 페이지가 동일한 폴더에 있어야 하는 이유는 없습니다. 하위 폴더에 콘텐츠 페이지를 만들 수 있습니다. 마찬가지로, 사이트의 마스터 페이지를 저장 하는 `~/MasterPages/` 폴더를 만들 수 있습니다.

마스터 및 콘텐츠 페이지를 서로 다른 폴더에 배치 하는 경우 발생 하는 한 가지 잠재적인 문제는 끊어진 Url입니다. 마스터 페이지에 하이퍼링크, 이미지 또는 다른 요소의 상대 Url이 포함 된 경우 다른 폴더에 있는 콘텐츠 페이지에 대 한 링크는 유효 하지 않게 됩니다. 이 자습서에서는이 문제의 원본 및 해결 방법을 살펴봅니다.

## <a name="the-problem-with-relative-urls"></a>상대 Url에 대 한 문제

웹 페이지의 URL은 가리키는 리소스의 위치가 웹 사이트의 폴더 구조에서 웹 페이지의 위치를 기준으로 하는 경우 *상대 url* 이라고 합니다. 선행 슬래시 (`/`) 또는 프로토콜 (예: `http://`)로 시작 하지 않는 URL은 URL을 포함 하는 웹 페이지의 위치를 기반으로 브라우저에서 확인 되기 때문에 상대적입니다.

예를 들어 웹 사이트에는 단일 이미지 파일 `PoweredByASPNET.gif`있는 `~/Images/` 폴더가 있습니다. 다음 태그를 사용 하 여 마스터 페이지 파일 `Site.master` `footerContent` 영역에 `<img>` 요소가 있습니다.

[!code-html[Main](urls-in-master-pages-vb/samples/sample1.html)]

`<img>` 요소의 `src` 특성 값은 `/` 또는 `http://`로 시작 하지 않으므로 상대 URL입니다. 간단히 말해서 `src` 특성 값은 `PoweredByASPNET.gif`이라는 파일에 대해 `Images` 하위 폴더를 검색 하도록 브라우저에 지시 합니다.

콘텐츠 페이지를 방문 하면 위의 태그가 브라우저에 직접 전송 됩니다. 잠시 `About.aspx` 방문 하 여 브라우저에 전송 된 HTML 원본을 확인 하세요. 마스터 페이지에서 정확히 동일한 태그가 브라우저에 전송 된 것을 확인할 수 있습니다.

[!code-html[Main](urls-in-master-pages-vb/samples/sample2.html)]

콘텐츠 페이지가 루트 폴더에 있는 경우 (`About.aspx`) 루트 폴더에 상대적인 `Images` 하위 폴더가 있으므로 모든 것이 예상 대로 작동 합니다. 그러나 콘텐츠 페이지가 마스터 페이지가 아닌 다른 폴더에 있는 경우에는 작업이 중단 됩니다. 이를 설명 하려면 `Admin`라는 하위 폴더를 만듭니다. 그런 다음 `Admin` 폴더에 `Default.aspx` 라는 콘텐츠 페이지를 추가 하 여 `Site.master` 마스터 페이지에 새 페이지를 바인딩해야 합니다.

> [!NOTE]
> [*마스터 페이지에서 제목, 메타 태그 및 기타 HTML 헤더 지정*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) 자습서에서 콘텐츠 페이지의 제목을 자동으로 설정 하는 `BasePage` 라는 사용자 지정 기본 페이지 클래스를 만들었습니다 (명시적으로 할당 되지 않은 경우). 새로 만든 페이지의 코드 숨김이이 기능을 활용할 수 있도록 `BasePage`에서 파생 되도록 해야 합니다.

이 콘텐츠 페이지를 만든 후에는 솔루션 탐색기 그림 1과 같이 표시 됩니다.

![새 폴더 및 ASP.NET 페이지가 프로젝트에 추가 되었습니다.](urls-in-master-pages-vb/_static/image1.png)

**그림 01**: 새 폴더 및 ASP.NET 페이지가 프로젝트에 추가 되었습니다.

다음으로,이 단원에 대 한 새 `<siteMapNode>` 항목을 포함 하도록 `Web.sitemap` 파일을 업데이트 합니다. 다음 XML은 이제 세 번째 `<siteMapNode>` 요소를 추가 하는 것을 포함 하는 전체 `Web.sitemap` 태그를 보여 줍니다.

[!code-xml[Main](urls-in-master-pages-vb/samples/sample3.xml)]

새로 만든 `Default.aspx` 페이지에는 `Site.master`에서 4 개의 ContentPlaceHolders 표시자에 해당 하는 4 개의 콘텐츠 컨트롤이 있어야 합니다. `MainContent` ContentPlaceHolder를 참조 하는 콘텐츠 컨트롤에 일부 텍스트를 추가한 다음 브라우저를 통해 페이지를 방문 합니다. 그림 2에서 볼 수 있듯이 브라우저는 `PoweredByASPNET.gif` 이미지 파일을 찾을 수 없습니다. 여기에 무슨 일이 일어나고 있나요?

`~/Admin/Default.aspx` 콘텐츠 페이지는 `About.aspx` 페이지와 같이 `footerContent` 영역에 대해 동일한 HTML로 전송 됩니다.

[!code-html[Main](urls-in-master-pages-vb/samples/sample4.html)]

`<img>` 요소의 `src` 특성이 상대 URL 이므로 브라우저는 웹 페이지의 폴더 위치를 기준으로 `Images` 폴더를 찾으려고 시도 합니다. 즉, 브라우저는 `Admin/Images/PoweredByASPNET.gif`이미지 파일을 찾습니다.

[PoweredByASPNET .gif 이미지 파일을 찾을 수 ![.](urls-in-master-pages-vb/_static/image3.png)](urls-in-master-pages-vb/_static/image2.png)

**그림 02**: `PoweredByASPNET.gif` 이미지 파일을 찾을 수 없습니다 ([전체 크기 이미지를 보려면 클릭](urls-in-master-pages-vb/_static/image4.png)).

### <a name="replacing-relative-urls-with-absolute-urls"></a>상대 url을 절대 Url로 바꾸기

상대 URL의 반대는 *절대 url*로, 슬래시 (`/`)로 시작 하는 url 또는 `http://`와 같은 프로토콜로 시작 합니다. 절대 URL은 알려진 고정 점에서 리소스의 위치를 지정 하므로 웹 사이트의 폴더 구조에서 웹 페이지의 위치에 관계 없이 모든 웹 페이지에서 동일한 절대 URL이 유효 합니다.

그림 2에 표시 된 손상 된 이미지를 해결 하려면 상대 URL 대신 절대 URL을 사용 하도록 `<img>` 요소의 `src` 특성을 업데이트 해야 합니다. 올바른 절대 URL을 확인 하려면 웹 사이트의 웹 페이지 중 하나를 방문 하 여 주소 표시줄을 확인 합니다. 그림 2의 주소 표시줄에 표시 된 것 처럼 웹 응용 프로그램의 정규화 된 경로는 `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_VB/`됩니다. 따라서 `<img>` 요소의 `src` 특성을 다음 두 가지 절대 Url 중 하나로 업데이트할 수 있습니다.

- `/ASPNET_MasterPages_Tutorial_04_VB/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_VB/Images/PoweredByASPNET.gif`

잠시 후에 표시 된 양식 중 하나를 사용 하 여 `<img>` 요소의 `src` 특성을 절대 URL로 업데이트 한 다음 브라우저를 통해 `~/Admin/Default.aspx` 페이지를 방문 합니다. 이번에는 브라우저에서 `PoweredByASPNET.gif` 이미지 파일을 정확 하 게 찾아서 표시 합니다 (그림 3 참조).

[이제 PoweredByASPNET 이미지가 표시 ![.](urls-in-master-pages-vb/_static/image6.png)](urls-in-master-pages-vb/_static/image5.png)

**그림 03**: 이제 `PoweredByASPNET.gif` 이미지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](urls-in-master-pages-vb/_static/image7.png)).

절대 URL의 하드 코드는 작동 하는 반면 HTML을 웹 사이트의 서버 및 폴더 위치에 긴밀 하 게 결합 변경 될 수 있습니다. Visual Studio의 기본 제공 ASP.NET Development 웹 서버를 시작할 때마다 localhost 앞의 포트 번호가 자동으로 선택 되기 때문에 `http://localhost:3908/...` 형식의 절대 URL을 사용 하는 것은 불안정입니다. 마찬가지로 `http://localhost` 부분은 로컬로 테스트 하는 경우에만 유효 합니다. 코드가 프로덕션 서버에 배포 되 면 URL 기반이 `http://www.yourserver.com`와 같은 다른 항목으로 변경 됩니다. 이 응용 프로그램 경로가 개발 서버와 프로덕션 서버 간에 서로 다르기 때문에 brittleness의 절대 `/ASPNET_MasterPages_Tutorial_04_VB/...` URL은 동일한 에서도 마찬가지입니다.

좋은 소식은 ASP.NET는 런타임에 유효한 상대 URL을 생성 하는 메서드를 제공 한다는 것입니다.

## <a name="usingandresolveclienturl"></a>`~`및`ResolveClientUrl` 사용

절대 URL을 하드 코드 하는 대신 ASP.NET를 사용 하면 페이지 개발자가 물결표 (`~`)를 사용 하 여 웹 응용 프로그램의 루트를 나타낼 수 있습니다. 예를 들어이 자습서의 앞부분에서는 텍스트에서 `~/Admin/Default.aspx` 표기법을 사용 하 여 `Admin` 폴더의 `Default.aspx` 페이지를 참조 했습니다. `~` `Admin` 폴더가 웹 응용 프로그램 루트의 하위 폴더 임을 나타냅니다.

`Control` 클래스의 [`ResolveClientUrl` 메서드](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx) 는 URL을 사용 하 여 해당 컨트롤이 있는 웹 페이지에 해당 하는 상대 url로 수정 합니다. 예를 들어 `About.aspx`에서 `ResolveClientUrl("~/Images/PoweredByASPNET.gif")`를 호출 하면 `Images/PoweredByASPNET.gif`반환 됩니다. 그러나 `~/Admin/Default.aspx`에서 호출 하면 `../Images/PoweredByASPNET.gif`반환 됩니다.

> [!NOTE]
> 모든 ASP.NET 서버 컨트롤은 `Control` 클래스에서 파생 되기 때문에 모든 서버 컨트롤은 `ResolveClientUrl` 메서드에 액세스할 수 있습니다. `Page` 클래스도 `Control` 클래스에서 파생 됩니다. 즉,이 메서드는 ASP.NET 페이지의 코드 숨김이 클래스에서 직접 사용할 수 있습니다.

### <a name="usingin-the-declarative-markup"></a>선언 태그에`~`사용

여러 ASP.NET 웹 컨트롤에는 URL 관련 속성이 포함 됩니다. HyperLink 컨트롤에는 `NavigateUrl` 속성이 있습니다. 이미지 컨트롤에 `ImageUrl` 속성이 있습니다. 합니다. 렌더링 될 때 이러한 컨트롤은 URL 관련 속성 값을 `ResolveClientUrl`에 전달 합니다. 따라서 이러한 속성에 웹 응용 프로그램의 루트를 나타내는 `~` 포함 되어 있으면 URL이 유효한 상대 URL로 수정 됩니다.

ASP.NET 서버 컨트롤만 URL 관련 속성에서 `~`를 변환 한다는 점에 유의 하세요. `<img src="~/Images/PoweredByASPNET.gif" />`와 같이 정적 HTML 태그에 `~` 표시 되는 경우 ASP.NET 엔진은 HTML 콘텐츠와 함께 `~`를 브라우저에 보냅니다. 브라우저에서는 `~` URL의 일부인 것으로 가정 합니다. 예를 들어 브라우저 `<img src="~/Images/PoweredByASPNET.gif" />` 태그를 받으면 이미지 파일 `PoweredByASPNET.gif`포함 하는 하위 폴더 `Images` `~` 라는 하위 폴더가 있다고 가정 합니다.

`Site.master`에서 이미지 태그를 수정 하려면 기존 `<img>` 요소를 ASP.NET Image 웹 컨트롤로 바꿉니다. 이미지 웹 컨트롤의 `ID` `PoweredByImage`, `ImageUrl` 속성을 `~/Images/PoweredByASPNET.gif`로, 해당 `AlternateText` 속성을 "Powered by ASP.NET!"로 설정 합니다.

[!code-aspx[Main](urls-in-master-pages-vb/samples/sample5.aspx)]

마스터 페이지를 변경한 후 `~/Admin/Default.aspx` 페이지를 다시 방문 합니다. 이번에는 페이지에 `PoweredByASPNET.gif` 이미지 파일이 표시 됩니다 (그림 3 참조). 이미지 웹 컨트롤이 렌더링 되 면 `ResolveClientUrl` 메서드를 사용 하 여 `ImageUrl` 속성 값을 확인 합니다. `~/Admin/Default.aspx` HTML 소스의 다음 코드 조각에서 볼 수 있듯이 `ImageUrl`는 적절 한 상대 URL로 변환 됩니다.

[!code-html[Main](urls-in-master-pages-vb/samples/sample6.html)]

> [!NOTE]
> URL 기반 웹 컨트롤 속성에 사용 되는 것 외에도, `Response.Redirect` 및 `Server.MapPath` 메서드를 호출 하는 경우에도 `~`을 사용할 수 있습니다. 또한 필요한 경우 ASP.NET 또는 마스터 페이지의 선언적 태그에서 직접 `ResolveClientUrl` 메서드를 호출할 수 있습니다. [태그에서 `ResolveClientUrl`를 사용 하 여](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx) [Fritz 어니언](https://www.pluralsight.com/blogs/fritz/)의 블로그 항목을 참조 하세요.

## <a name="fixing-the-master-pages-remaining-relative-urls"></a>마스터 페이지의 나머지 상대 Url 수정

방금 수정한 `footerContent`의 `<img>` 요소 외에도 마스터 페이지에는 주의가 필요한 상대 URL이 하나 이상 포함 되어 있습니다. `topContent` 영역에는 `Default.aspx`를 가리키는 링크 "마스터 페이지 자습서"가 포함 되어 있습니다.

[!code-html[Main](urls-in-master-pages-vb/samples/sample7.html)]

이 URL은 상대적 이므로 방문한 콘텐츠 페이지의 폴더에 있는 `Default.aspx` 페이지로 사용자를 보냅니다. 이 링크가 항상 루트 폴더의 `Default.aspx`를 가리키도록 하려면 `~` 표기법을 사용할 수 있도록 `<a>` 요소를 하이퍼링크 웹 컨트롤로 바꾸어야 합니다.

`<a>` 요소 태그를 제거 하 고 그 자리에 하이퍼링크 컨트롤을 추가 합니다. 하이퍼링크의 `ID` `lnkHome`, `NavigateUrl` 속성을 `~/Default.aspx`로, 해당 `Text` 속성을 "마스터 페이지 자습서"로 설정 합니다.

[!code-aspx[Main](urls-in-master-pages-vb/samples/sample8.aspx)]

정말 간단하죠. 이 시점에서 마스터 페이지의 모든 Url은 마스터 페이지 및 콘텐츠 페이지가 있는 폴더에 관계 없이 콘텐츠 페이지에서 렌더링 될 때 적절 하 게 기반 합니다.

### <a name="automatic-url-resolution-in-theheadsection"></a>`<head>`섹션의 자동 URL 확인

[*마스터 페이지를 사용 하 여 사이트 전체 레이아웃 만들기*](creating-a-site-wide-layout-using-master-pages-vb.md) 자습서에서는 `<head>` 지역의 `Styles.css` 파일에 `<link>`를 추가 했습니다.

[!code-aspx[Main](urls-in-master-pages-vb/samples/sample9.aspx)]

`<link>` 요소의 `href` 특성은 상대적 이지만 런타임에 적절 한 경로로 자동으로 변환 됩니다. [*마스터 페이지 자습서에서 제목, 메타 태그 및 기타 HTML 헤더를 지정 하*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) 는 방법에 설명 된 대로 `<head>` 지역은 실제로 서버 쪽 컨트롤이 며,이 컨트롤은 렌더링 될 때 내부 컨트롤의 내용을 수정할 수 있도록 합니다.

이를 확인 하려면 `~/Admin/Default.aspx` 페이지를 다시 방문 하 여 브라우저에 전송 된 HTML 소스를 확인 합니다. 아래 코드 조각에서 설명 하는 것 처럼 `<link>` 요소의 `href` 특성은 적절 한 상대 URL `../Styles.css`자동으로 수정 되었습니다.

[!code-html[Main](urls-in-master-pages-vb/samples/sample10.html)]

## <a name="summary"></a>요약

마스터 페이지는 URL을 통해 지정 해야 하는 링크, 이미지 및 기타 외부 리소스를 포함 하는 경우가 많습니다. 마스터 페이지와 콘텐츠 페이지가 동일한 폴더에 없을 수 있으므로 상대 Url을 사용 하 여 abstain 하는 것이 중요 합니다. 하드 코드 된 절대 url을 사용할 수 있지만이 경우 웹 응용 프로그램에 대 한 절대 URL을 긴밀 하 게 결합. 웹 응용 프로그램을 이동 하거나 배포할 때와 마찬가지로 절대 URL이 변경 되 면 뒤로 돌아가 절대 Url을 업데이트 해야 합니다.

이상적인 방법은 물결표 (`~`)를 사용 하 여 응용 프로그램 루트를 나타내는 것입니다. URL 관련 속성을 포함 하는 ASP.NET 웹 컨트롤은 런타임에 응용 프로그램 루트에 `~`를 매핑합니다. 내부적으로 웹 컨트롤은 `Control` 클래스의 `ResolveClientUrl` 메서드를 사용 하 여 유효한 상대 URL을 생성 합니다. 이 메서드는 공용 이며, 모든 서버 컨트롤 (`Page` 클래스 포함)에서 사용할 수 있으므로 필요한 경우 코드 기반 클래스에서 프로그래밍 방식으로 사용할 수 있습니다.

행복 한 프로그래밍

### <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ASP.NET의 마스터 페이지](http://www.odetocode.com/Articles/419.aspx)
- [마스터 페이지의 URL의 기준 주소](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [태그에서 `ResolveClientUrl` 사용](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)는 여러 ASP/ASP. NET books의 작성자와 4GuysFromRolla.com의 창립자가 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 3.5을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. Scott은 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) 또는 [http://ScottOnWriting.NET](http://scottonwriting.net/)의 블로그를 통해 연결할 수 있습니다.

### <a name="special-thanks-to"></a>특별히 감사 합니다.

예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)에서 줄을 삭제 합니다.

> [!div class="step-by-step"]
> [이전](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)
> [다음](control-id-naming-in-content-pages-vb.md)
