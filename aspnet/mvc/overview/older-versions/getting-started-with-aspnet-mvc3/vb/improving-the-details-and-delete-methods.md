---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
title: 세부 정보 및 삭제 메서드 개선 (VB) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: c5c14ef0-c128-4dc1-8c01-7f0fdb09e411
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/improving-the-details-and-delete-methods
msc.type: authoredcontent
ms.openlocfilehash: 08d80cac071907e927bb30df53c6f84a28f53156
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78485543"
---
# <a name="improving-the-details-and-delete-methods-vb"></a>세부 정보 및 삭제 메서드 개선(VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.
> 
> VB.NET 소스 코드를 사용 하는 Visual Web Developer 프로젝트를이 항목과 함께 사용할 수 있습니다. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 선호 C#하는 경우이 자습서의 [ C# 버전](../cs/improving-the-details-and-delete-methods.md) 으로 전환 합니다.

자습서의이 부분에서는 자동으로 생성 된 `Details` 및 `Delete` 메서드를 몇 가지 개선 했습니다. 이러한 변경은 필요 하지 않지만 약간의 작은 코드를 사용 하면 응용 프로그램을 쉽게 향상 시킬 수 있습니다.

## <a name="improving-the-details-and-delete-methods"></a>세부 정보 및 삭제 메서드 개선

`Movie` 컨트롤러를 스 캐 폴드 때 잘 작동 했지만 몇 가지 약간만 변경 하 여 더 강력 하 게 만들 수 있는 MVC 생성 코드를 ASP.NET.

`Movie` 컨트롤러를 열고 영화를 찾을 수 없는 경우 `HttpNotFound`를 반환 하 여 `Details` 메서드를 수정 합니다. 또한 전달 되는 ID에 대 한 기본값을 설정 하려면 `Details` 메서드를 수정 해야 합니다. (이 자습서의 [6 부](examining-the-edit-methods-and-edit-view.md) 에서 `Edit` 메서드를 비슷하게 변경 했습니다.) 그러나 `HttpNotFound` 메서드가 `ViewResult` 개체를 반환 하지 않으므로 `Details` 메서드의 반환 형식을 `ViewResult`에서 `ActionResult`으로 변경 해야 합니다. 다음 예제에서는 수정 된 `Details` 메서드를 보여 줍니다.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample1.vb)]

Code First를 사용 하면 `Find` 메서드를 사용 하 여 데이터를 쉽게 검색할 수 있습니다. 메서드에 기본 제공 되는 중요 한 보안 기능은 코드에서 작업을 수행 하려고 시도 하기 전에 `Find` 메서드가 영화를 발견 했는지 확인 하는 것입니다. 예를 들어 해커가 `http://localhost:xxxx/Movies/Details/1`에서 만든 URL을 `http://localhost:xxxx/Movies/Details/12345` (또는 실제 영화를 나타내지 않는 다른 값)와 같이 변경 하 여 사이트에 오류를 발생 시킬 수 있습니다. Null 동영상을 검사 하지 않으면 데이터베이스 오류가 발생할 수 있습니다.

마찬가지로 `Delete` 및 `DeleteConfirmed` 메서드를 변경 하 여 ID 매개 변수의 기본값을 지정 하 고 동영상을 찾을 수 없는 경우 `HttpNotFound`을 반환 합니다. `Movie` 컨트롤러의 업데이트 된 `Delete` 메서드는 다음과 같습니다.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample2.vb)]

`Delete` 메서드는 데이터를 삭제 하지 않습니다. GET 요청에 대한 응답에서 삭제 작업을 수행하는 것은(또는 해당 문제에 대한 편집 작업, 만들기 작업 또는 데이터를 변경하는 기타 작업을 수행하는 것은) 보안 허점을 야기합니다. 이에 대 한 자세한 내용은 Stephen Walther의 블로그 항목 [ASP.NET MVC 팁 #46를 참조 하세요. 보안 허점을 만들기 때문에 Delete 링크를 사용 하지 마세요](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx).

데이터를 삭제하는 `HttpPost` 메서드의 이름은 HTTP POST 메서드에 고유한 서명 또는 이름을 부여하기 위해 `DeleteConfirmed`로 지정됩니다. 두 메서드의 서명은 다음과 같습니다.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample3.vb)]

CLR (공용 언어 런타임)에는 고유한 시그니처 (동일한 이름, 다른 매개 변수 목록)를 포함 하는 오버 로드 된 메서드가 필요 합니다. 그러나 여기에서 두 개의 Delete 메서드 (GET의 경우 하나, POST의 경우 one)가 필요 합니다. 둘 다 동일한 서명이 필요 합니다. (모두 매개 변수로 단일 정수를 허용해야 합니다.)

이를 정렬 하기 위해 몇 가지 작업을 수행할 수 있습니다. 하나는 메서드에 다른 이름을 지정 하는 것입니다. 앞의 예제에서이 작업을 수행 했습니다. 그러나 이는 작은 문제를 가져옵니다. ASP.NET은 URL의 세그먼트를 이름으로 작업 메서드에 매핑하고 메서드의 이름을 바꾸면 정상적으로 라우팅하여 해당 메서드를 찾을 수 없게 됩니다. 솔루션은 예제에서 확인한 것으로, `ActionName("Delete")` 특성을 `DeleteConfirmed` 메서드에 추가하는 것입니다. 이렇게 하면 POST 요청에 대 한 <em>/Delete/</em>를 포함 하는 URL이 `DeleteConfirmed` 메서드를 찾을 수 있도록 라우팅 시스템에 대 한 매핑이 효과적으로 수행 됩니다.

이름 및 시그니처가 동일한 메서드의 문제를 방지 하는 또 다른 방법은 사용 하지 않는 매개 변수를 포함 하도록 POST 메서드의 서명을 인위적으로 변경 하는 것입니다. 예를 들어, 일부 개발자는 POST 메서드로 전달 되는 `FormCollection` 매개 변수 형식을 추가한 다음 매개 변수를 사용 하지 않습니다.

[!code-vb[Main](improving-the-details-and-delete-methods/samples/sample4.vb)]

## <a name="wrapping-up"></a>래핑

이제 SQL Server Compact 데이터베이스에 데이터를 저장 하는 완전 한 ASP.NET MVC 응용 프로그램이 있습니다. 영화를 만들고, 읽고, 업데이트 하 고, 삭제 하 고, 검색할 수 있습니다.

![](improving-the-details-and-delete-methods/_static/image1.png)

이 기본 자습서에서는 컨트롤러를 만들어 뷰와 연결 하 고 하드 코드 된 데이터를 전달 하기 시작 했습니다. 그런 다음 데이터 모델을 만들고 디자인 했습니다. Code First Entity Framework는 즉시 데이터 모델에서 데이터베이스를 만들고 ASP.NET MVC 스 캐 폴딩 시스템에서 기본 CRUD 작업에 대 한 작업 메서드와 뷰를 자동으로 생성 했습니다. 그런 다음 사용자가 데이터베이스를 검색할 수 있는 검색 양식을 추가 했습니다. 새 데이터 열을 포함 하도록 데이터베이스를 변경한 다음 두 페이지를 업데이트 하 여이 새 데이터를 만들고 표시 합니다. `DataAnnotations` 네임 스페이스의 특성으로 데이터 모델을 표시 하 여 유효성 검사를 추가 했습니다. 결과 유효성 검사는 클라이언트와 서버에서 실행 됩니다.

응용 프로그램을 배포 하려는 경우 먼저 로컬 IIS 7 서버에서 응용 프로그램을 테스트 하는 것이 좋습니다. 이 [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=ASPNET;) 링크를 사용 하 여 ASP.NET 응용 프로그램에 대 한 IIS 설정을 사용 하도록 설정할 수 있습니다. 다음 배포 링크를 참조 하세요.

- [ASP.NET 배포 콘텐츠 맵](https://msdn.microsoft.com/library/dd394698.aspx)
- [IIS 4.x 사용](https://blogs.msdn.com/b/rickandy/archive/2011/03/14/enabling-iis-7-x-on-windows-7-vista-sp1-windows-2008-windows-2008-r2.aspx)
- [웹 응용 프로그램 프로젝트 배포](https://msdn.microsoft.com/library/dd394698.aspx)

이제 ASP.NET MVC 응용 프로그램 및 [Mvc Music Store](../../mvc-music-store/mvc-music-store-part-1.md) 자습서 [에 대 한 Entity Framework 데이터 모델을 만드는](../../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) 중간 수준으로 이동 하 여 [MSDN의 ASP.NET 문서](https://msdn.microsoft.com/library/gg416514(VS.98).aspx)를 탐색 하 고 [https://asp.net/mvc](https://asp.net/mvc) 에서 많은 비디오와 리소스를 확인 하 여 ASP.NET MVC에 대해 자세히 알아보세요. [ASP.NET MVC 포럼](https://forums.asp.net/1146.aspx) 은 질문을 할 수 있는 좋은 장소입니다.

마음껏 즐기세요!

-Scott Hanselman (Twitter의[http://hanselman.com](http://hanselman.com) 및 [@shanselman](http://twitter.com/shanselman) ) 및 Rick Anderson [blogs.msdn.com/rickAndy](https://blogs.msdn.com/rickAndy)

> [!div class="step-by-step"]
> [이전](adding-validation-to-the-model.md)
