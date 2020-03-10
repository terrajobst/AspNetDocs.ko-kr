---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Azure Azure App Service에 앱 게시 Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78504761"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a>Azure Azure App Service에 앱 게시

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

마지막 단계로 Azure에 응용 프로그램을 게시 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다.

![](part-10/_static/image1.png)

**게시** 를 클릭 하면 **웹 게시** 대화 상자가 호출 됩니다. 프로젝트를 처음 만들 때 **클라우드에서 호스트** 를 선택한 경우 연결 및 설정이 이미 구성 되어 있습니다. 이 경우 **설정** 탭을 클릭 하 고 Code First 마이그레이션&quot;&quot;실행을 선택 합니다. (처음부터 **클라우드의 호스트** 를 확인 하지 않은 경우 [다음 섹션](#new-website)의 단계를 따르세요.)

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

앱을 배포 하려면 **게시**를 클릭 합니다. **웹 게시 작업** 창에서 게시 진행률을 볼 수 있습니다. **보기** 메뉴에서 **다른 창**을 선택한 다음 **웹 게시 작업**을 선택 합니다.

![](part-10/_static/image4.png)

Visual Studio에서 앱 배포가 완료 되 면 기본 브라우저가 자동으로 배포 된 웹 사이트의 URL로 열리며, 만든 응용 프로그램은 이제 클라우드에서 실행 됩니다. 브라우저 주소 표시줄의 URL은 사이트가 인터넷에서 로드 되 고 있음을 보여 줍니다.

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>새 웹 사이트에 배포

프로젝트를 처음 만들 때 **클라우드의 호스트** 를 확인 하지 않은 경우 지금 새 웹 앱을 구성할 수 있습니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 **게시**를 선택 합니다. **프로필** 탭을 선택 하 고 **Microsoft Azure Websites**를 클릭 합니다. 현재 Azure에 로그인 하지 않은 경우 로그인 하 라는 메시지가 표시 됩니다.

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

**기존 웹 사이트** 대화 상자에서 **새로 만들기**를 클릭 합니다.

![](part-10/_static/image9.png)

사이트 이름을 입력 합니다. Azure 구독 및 지역을 선택 합니다. **데이터베이스 서버**에서 **새 서버 만들기**를 선택 하거나 기존 서버를 선택 합니다. **만들기**를 클릭합니다.

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

**설정** 탭을 클릭 하 &quot;Code First 마이그레이션&quot;실행을 선택 합니다. 그런 다음, **게시**를 클릭합니다.

> [!div class="step-by-step"]
> [이전](part-9.md)
