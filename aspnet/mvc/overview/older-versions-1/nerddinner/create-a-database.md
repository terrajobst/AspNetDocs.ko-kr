---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 데이터베이스 만들기 | Microsoft 문서
author: microsoft
description: 2 단계에서는 팀 간 Ddinner 응용 프로그램에 대 한 모든 dinner 및 RSVP 데이터를 보유 하는 데이터베이스를 만드는 단계를 보여 줍니다.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78469301"
---
# <a name="create-a-database"></a>데이터베이스 만들기

[Microsoft](https://github.com/microsoft) 에서

[PDF 다운로드](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> ASP.NET MVC 1을 사용 하 여 작고 완전 한 웹 응용 프로그램을 빌드하는 방법을 안내 하는 무료 ["Nerddinner" 응용 프로그램 자습서](introducing-the-nerddinner-tutorial.md) 의 2 단계입니다.
> 
> 2 단계에서는 팀 간 Ddinner 응용 프로그램에 대 한 모든 dinner 및 RSVP 데이터를 보유 하는 데이터베이스를 만드는 단계를 보여 줍니다.
> 
> ASP.NET MVC 3을 사용 하는 경우 [mvc 3 시작](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) 또는 [mvc Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) 자습서를 따르는 것이 좋습니다.

## <a name="nerddinner-step-2-creating-the-database"></a>NerdDinner Step 2: 데이터베이스 만들기

여기서는 데이터베이스를 사용 하 여 전체 고객 Ddinner 응용 프로그램에 대 한 모든 저녁 및 RSVP 데이터를 저장 합니다.

아래 단계는 무료 SQL Server Express 버전을 사용 하 여 데이터베이스를 만드는 것을 보여 줍니다 ( [Microsoft 웹 플랫폼 설치 관리자](https://www.microsoft.com/web/downloads/platform.aspx)의 V2를 사용 하 여 쉽게 설치할 수 있음). 작성 하는 모든 코드는 SQL Server Express와 전체 SQL Server 함께 작동 합니다.

### <a name="creating-a-new-sql-server-express-database"></a>새 SQL Server Express 데이터베이스 만들기

먼저 웹 프로젝트를 마우스 오른쪽 단추로 클릭 한 다음 **추가-&gt;새 항목** 메뉴 명령을 선택 합니다.

![](create-a-database/_static/image1.png)

그러면 Visual Studio의 "새 항목 추가" 대화 상자가 표시 됩니다. "Data" 범주를 기준으로 필터링 하 고 "SQL Server 데이터베이스" 항목 템플릿을 선택 합니다.

![](create-a-database/_static/image2.png)

SQL Server Express 데이터베이스의 이름을 "NerdDinner. .mdf"로 만들고 확인을 누릅니다. 그러면 Visual Studio에서이 파일을 \App\_데이터 디렉터리 (읽기 및 쓰기 보안 Acl을 사용 하 여 이미 설정 된 디렉터리)에 추가 하고자 하는지 확인 합니다.

![](create-a-database/_static/image3.png)

"예"를 클릭 하면 새 데이터베이스가 생성 되 고 솔루션 탐색기에 추가 됩니다.

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a>데이터베이스 내에 테이블 만들기

이제 빈 데이터베이스를 새로 만들었습니다. 여기에 일부 테이블을 추가 해 보겠습니다.

이렇게 하려면 데이터베이스와 서버를 관리할 수 있게 해 주는 Visual Studio 내에서 "서버 탐색기" 탭 창으로 이동 합니다. 응용 프로그램의 \App\_Data 폴더에 저장 된 SQL Server Express 데이터베이스는 자동으로 서버 탐색기 내에 표시 됩니다. 선택적으로 "서버 탐색기" 창의 맨 위에 있는 "데이터베이스에 연결" 아이콘을 사용 하 여 목록에 SQL Server 데이터베이스 (로컬 및 원격 모두)를 더 추가할 수 있습니다.

![](create-a-database/_static/image5.png)

Dinners를 저장 하 고 다른 하나는 RSVP acceptances을 추적 하는 두 개의 테이블을 두 개의 테이블에 추가 합니다. 데이터베이스 내에서 "Tables" 폴더를 마우스 오른쪽 단추로 클릭 하 고 "새 테이블 추가" 메뉴 명령을 선택 하 여 새 테이블을 만들 수 있습니다.

![](create-a-database/_static/image6.png)

이렇게 하면 테이블의 스키마를 구성 하는 데 사용할 수 있는 테이블 디자이너가 열립니다. "Dinners" 테이블의 경우 10 개의 데이터 열을 추가 합니다.

![](create-a-database/_static/image7.png)

"DinnerID" 열을 테이블의 고유 기본 키로 사용할 수 있습니다. "DinnerID" 열을 마우스 오른쪽 단추로 클릭 하 고 "기본 키 설정" 메뉴 항목을 선택 하 여이를 구성할 수 있습니다.

![](create-a-database/_static/image8.png)

테이블에 새 데이터 행이 추가 될 때 해당 값이 자동으로 증가 하는 "id" 열로 구성 하는 것 외에도이를 기본 키로 구성 하는 것이 좋습니다. 즉, 첫 번째 삽입 된 Dinner row에는 두 번째 삽입 된 행이 포함 됩니다. 은 (는) 2, 등의 d Innerid를 가집니다.

"DinnerID" 열을 선택한 다음 "열 속성" 편집기를 사용 하 여 열의 "(Id)" 속성을 "예"로 설정할 수 있습니다. 표준 id 기본값 (1에서 시작 하 고 새 Dinner row에서 1 씩 증가)을 사용 합니다.

![](create-a-database/_static/image9.png)

그런 다음 Ctrl + S를 입력 하거나 **파일&gt;저장** 메뉴 명령을 사용 하 여 테이블을 저장 합니다. 그러면 테이블의 이름을 입력 하 라는 메시지가 표시 됩니다. 이름을 "Dinners"로 표시 합니다.

![](create-a-database/_static/image10.png)

그러면 새 Dinners 테이블이 서버 탐색기의 데이터베이스 내에 표시 됩니다.

그런 다음 위의 단계를 반복 하 고 "RSVP" 테이블을 만듭니다. 의이 테이블에는 3 개의 열이 있습니다. RsvpID 열을 기본 키로 설정 하 고 id 열로 설정 합니다.

![](create-a-database/_static/image11.png)

이를 저장 하 고 이름을 "RSVP"로 지정 합니다.

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a>테이블 간의 외래 키 관계 설정

이제 데이터베이스에 두 개의 테이블이 있습니다. 마지막 스키마 디자인 단계는 이러한 두 테이블 간에 "일 대 다" 관계를 설정 하 여 각 Dinner row에 적용 되는 0 개 이상의 RSVP 행과 연결할 수 있도록 하는 것입니다. 이렇게 하려면 "Dinners" 테이블의 "DinnerID" 열에 대 한 외래 키 관계를 갖도록 RSVP 테이블의 "DinnerID" 열을 구성 하 여이 작업을 수행 합니다.

이렇게 하려면 서버 탐색기에서 테이블 디자이너를 두 번 클릭 하 여 테이블 디자이너 내에서 RSVP 테이블을 엽니다. 그런 다음 해당 내에서 "DinnerID" 열을 선택 하 고 마우스 오른쪽 단추를 클릭 한 다음 "관계 ..."를 선택 합니다. 상황에 맞는 메뉴 명령:

![](create-a-database/_static/image12.png)

그러면 테이블 간의 관계를 설정 하는 데 사용할 수 있는 대화 상자가 표시 됩니다.

![](create-a-database/_static/image13.png)

"추가" 단추를 클릭 하 여 대화 상자에 새 관계를 추가 합니다. 관계가 추가 되 면 대화 상자 오른쪽에 있는 속성 그리드 내에서 "테이블 및 열 사양" 트리 뷰 노드를 확장 한 다음 "..."를 클릭 합니다. 오른쪽에 있는 단추:

![](create-a-database/_static/image14.png)

"..."를 클릭 합니다. 단추를 클릭 하면 관계에 포함 된 테이블과 열을 지정할 수 있을 뿐만 아니라 관계의 이름을 지정할 수 있는 다른 대화 상자가 표시 됩니다.

기본 키 테이블을 "Dinners"로 변경 하 고 Dinners 테이블 내에서 기본 키로 "DinnerID" 열을 선택 합니다. RSVP 테이블은 외래 키 테이블 및 RSVP입니다. DinnerID 열은 외래 키로 연결 됩니다.

![](create-a-database/_static/image15.png)

이제 RSVP 테이블의 각 행이 Dinner table의 행과 연결 됩니다. SQL Server는 microsoft의 참조 무결성을 유지 하 고 유효한 저녁 행을 가리키지 않는 경우 새 RSVP 행을 추가 하지 않도록 합니다. 또한 여전히 RSVP 행을 참조 하는 경우 Dinner row를 삭제 하지 않습니다.

### <a name="adding-data-to-our-tables"></a>테이블에 데이터 추가

Dinners 테이블에 몇 가지 샘플 데이터를 추가 하는 것부터 살펴보겠습니다. 서버 탐색기 내에서 테이블을 마우스 오른쪽 단추로 클릭 하 고 "테이블 데이터 표시" 명령을 선택 하 여 테이블에 데이터를 추가할 수 있습니다.

![](create-a-database/_static/image16.png)

나중에 응용 프로그램 구현을 시작할 때 사용할 수 있는 Dinner data 행을 몇 개 추가 합니다.

![](create-a-database/_static/image17.png)

### <a name="next-step"></a>다음 단계

데이터베이스를 만들었습니다. 이제 쿼리 및 업데이트에 사용할 수 있는 모델 클래스를 만들어 보겠습니다.

> [!div class="step-by-step"]
> [이전](create-a-new-aspnet-mvc-project.md)
> [다음](build-a-model-with-business-rule-validations.md)
