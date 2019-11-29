---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: '4 부: 관리 보기 추가 | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600010"
---
# <a name="part-4-adding-an-admin-view"></a>4 부: 관리 보기 추가

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a>관리 보기 추가

이제 클라이언트 쪽으로 전환 하 고 관리 컨트롤러의 데이터를 사용할 수 있는 페이지를 추가 합니다. 페이지를 통해 사용자는 AJAX 요청을 컨트롤러에 전송 하 여 제품을 생성, 편집 또는 삭제할 수 있습니다.

솔루션 탐색기에서 Controllers 폴더를 확장 하 고 이름이 HomeController.cs 인 파일을 엽니다. 이 파일은 MVC 컨트롤러를 포함 합니다. `Admin`라는 메서드를 추가 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

**HttpRouteUrl** 메서드는 web API에 대 한 URI를 만들고 나중에 사용할 수 있도록이를 보기 모음에 저장 합니다.

그런 다음 `Admin` 작업 메서드 내에 텍스트 커서를 놓고 마우스 오른쪽 단추를 클릭 한 다음 **뷰 추가**를 선택 합니다. 그러면 **보기 추가** 대화 상자가 표시 됩니다.

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

**보기 추가** 대화 상자에서 뷰 이름을 "Admin"으로 표시 합니다. **강력한 형식의 뷰 만들기**라는 확인란을 선택 합니다. **모델 클래스**에서 "Product (제품명)"를 선택 합니다. 다른 모든 옵션은 기본값으로 둡니다.

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

**추가** 를 클릭 하면 Views/Home 아래에 Admin 이라는 파일이 추가 됩니다. 이 파일을 열고 다음 HTML을 추가 합니다. 이 HTML은 페이지의 구조를 정의 하지만 아직 연결 된 기능은 없습니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a>관리 페이지에 대 한 링크 만들기

솔루션 탐색기에서 Views 폴더를 확장 한 다음 공유 폴더를 확장 합니다. \_Layout. cshtml 라는 파일을 엽니다. Id = "menu" 인 **ul** 요소와 관리 보기에 대 한 작업 링크를 찾습니다.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> 샘플 프로젝트에서는 "your your your your here" 문자열을 대체 하는 것과 같이 몇 가지 다른 외관상 변화를 만들었습니다. 응용 프로그램의 기능에는 영향을 주지 않습니다. 프로젝트를 다운로드 하 고 파일을 비교할 수 있습니다.

응용 프로그램을 실행 하 고 홈 페이지의 맨 위에 표시 되는 "관리" 링크를 클릭 합니다. 관리 페이지는 다음과 같습니다.

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

지금은 페이지에서 어떤 작업도 수행 하지 않습니다. 다음 섹션에서는 node.js를 사용 하 여 동적 UI를 만듭니다.

## <a name="add-authorization"></a>권한 부여 추가

현재이 사이트를 방문 하는 모든 사용자가 관리 페이지에 액세스할 수 있습니다. 관리자에 대 한 권한을 제한 하려면이를 변경해 보겠습니다.

"관리자" 역할 및 관리자 사용자를 추가 하 여 시작 합니다. 솔루션 탐색기에서 Filters 폴더를 확장 하 고 이름이 InitializeSimpleMembershipAttribute.cs 인 파일을 엽니다. `SimpleMembershipInitializer` 생성자를 찾습니다. **InitializeDatabaseConnection**에 대 한 호출 후 다음 코드를 추가 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

이는 "Administrator" 역할을 추가 하 고 역할에 대 한 사용자를 만들기 위한 신속 하 고 변경 된 방법입니다.

솔루션 탐색기에서 Controllers 폴더를 확장 하 고 HomeController.cs 파일을 엽니다. **권한 부여** 특성을 `Admin` 메서드에 추가 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

AdminController.cs 파일을 열고 **권한 부여** 특성을 전체 `AdminController` 클래스에 추가 합니다.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> MVC 및 Web API는 서로 다른 네임 스페이스에 **권한 부여** 특성을 정의 합니다. MVC에서는 **AuthorizeAttribute**를 사용 하 고 web API는 **AuthorizeAttribute**를 사용 합니다.

이제 관리자만이 관리 페이지를 볼 수 있습니다. 또한 관리 컨트롤러에 HTTP 요청을 보내는 경우 요청은 인증 쿠키를 포함 해야 합니다. 그렇지 않으면 서버에서 HTTP 401 (권한 없음) 응답을 보냅니다. `http://localhost:*port*/api/admin`에 GET 요청을 전송 하 여 Fiddler에서이를 확인할 수 있습니다.

> [!div class="step-by-step"]
> [이전](using-web-api-with-entity-framework-part-3.md)
> [다음](using-web-api-with-entity-framework-part-5.md)
