---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: '자습서: MVC 5를 사용 하 여 EF Database First 시작'
description: 이 자습서에서는 기존 데이터베이스로 시작 하 고 사용자가 데이터와 상호 작용할 수 있도록 하는 웹 응용 프로그램을 신속 하 게 만드는 방법을 보여 줍니다.
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78471461"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a>자습서: MVC 5를 사용 하 여 EF Database First 시작

MVC, Entity Framework 및 ASP.NET 스 캐 폴딩을 사용 하 여 기존 데이터베이스에 대 한 인터페이스를 제공 하는 웹 응용 프로그램을 만들 수 있습니다. 이 자습서 시리즈에서는 사용자가 데이터베이스 테이블에 있는 데이터를 표시, 편집, 만들기 및 삭제할 수 있도록 하는 코드를 자동으로 생성 하는 방법을 보여 줍니다. 생성 된 코드는 데이터베이스 테이블의 열에 해당 합니다. 시리즈의 마지막 부분에서는 데이터 모델에 데이터 주석을 추가 하 여 유효성 검사 요구 사항을 지정 하 고 서식을 표시 하는 방법에 대해 알아봅니다. 완료 되 면 Azure 문서로 이동 하 여 .NET 앱 및 SQL database를 Azure App Service에 배포 하는 방법을 배울 수 있습니다.

이 자습서에서는 기존 데이터베이스로 시작 하 고 사용자가 데이터와 상호 작용할 수 있도록 하는 웹 응용 프로그램을 신속 하 게 만드는 방법을 보여 줍니다. Entity Framework 6 및 MVC 5를 사용 하 여 웹 응용 프로그램을 빌드합니다. ASP.NET 스 캐 폴딩 기능을 사용 하면 데이터를 표시, 업데이트, 만들기 및 삭제 하는 코드를 자동으로 생성할 수 있습니다. Visual Studio 내에서 게시 도구를 사용 하 여 사이트 및 데이터베이스를 Azure에 쉽게 배포할 수 있습니다.

시리즈의이 부분에서는 데이터베이스를 만들고 데이터를 채우는 방법을 중점적으로 설명 합니다.

이 시리즈는 Tom Dykstra 및 Rick Anderson의 기여를 통해 작성 되었습니다. 의견 섹션에서 사용자의 의견에 따라 개선 되었습니다.

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 데이터베이스 설정

## <a name="prerequisites"></a>사전 요구 사항

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a>데이터베이스 설정

기존 데이터베이스를 사용 하는 환경을 모방 하려면 먼저 미리 채워진 일부 데이터를 사용 하 여 데이터베이스를 만든 다음 데이터베이스에 연결 하는 웹 응용 프로그램을 만듭니다.

이 자습서는 Visual Studio 2017에서 LocalDB를 사용 하 여 개발 되었습니다. LocalDB 대신 기존 데이터베이스 서버를 사용할 수 있지만 Visual Studio의 버전 및 사용자의 데이터베이스 형식에 따라 Visual Studio의 모든 데이터 도구가 지원 되지 않을 수 있습니다. 데이터베이스에 대 한 도구를 사용할 수 없는 경우 데이터베이스에 대 한 관리 도구 모음 내에서 데이터베이스 관련 단계 중 일부를 수행 해야 할 수 있습니다.

Visual Studio 버전의 데이터베이스 도구에 문제가 있는 경우 최신 버전의 데이터베이스 도구를 설치 했는지 확인 합니다. 데이터베이스 도구를 업데이트 하거나 설치 하는 방법에 대 한 자세한 내용은 [Microsoft SQL Server Data tools](https://msdn.microsoft.com/data/hh297027)를 참조 하세요.

Visual Studio를 시작 하 고 **SQL Server 데이터베이스 프로젝트**를 만듭니다. 프로젝트 이름을 a **Osouniversitydata**로 합니다.

![데이터베이스 프로젝트 만들기](setting-up-database/_static/image1.png)

이제 빈 데이터베이스 프로젝트가 있습니다. 이 데이터베이스를 Azure에 배포할 수 있는지 확인 하려면 프로젝트의 대상 플랫폼으로 Azure SQL Database를 설정 합니다. 대상 플랫폼을 설정 해도 데이터베이스는 실제로 배포 되지 않습니다. 데이터베이스 프로젝트가 대상 플랫폼과 호환 되는지 확인 하는 것만을 의미 합니다. 대상 플랫폼을 설정 하려면 프로젝트의 **속성** 을 열고 대상 플랫폼에 대 한 **Microsoft Azure SQL Database** 를 선택 합니다.

테이블을 정의 하는 SQL 스크립트를 추가 하 여이 자습서에 필요한 테이블을 만들 수 있습니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목을 추가 합니다. 테이블 **및 뷰** 를 선택 하 > **테이블** 을 선택 하 고 이름을 *Student*로 이름을 선택 합니다.

테이블 파일에서 테이블을 만들기 위해 T-sql 명령을 다음 코드로 바꿉니다.

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

디자인 창이 코드와 자동으로 동기화 됩니다. 코드 또는 디자이너를 사용 하 여 작업할 수 있습니다.

![코드 및 디자인 표시](setting-up-database/_static/image5.png)

다른 테이블을 추가 합니다. 이번에는 이름으로 강좌를 만들고 다음 T-sql 명령을 사용 합니다.

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

그리고 한 번 더 반복 하 여 등록 이라는 테이블을 만듭니다.

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

데이터베이스가 배포 된 후 실행 되는 스크립트를 통해 데이터를 데이터로 채울 수 있습니다. 프로젝트에 배포 후 스크립트를 추가 합니다. 프로젝트를 마우스 오른쪽 단추로 클릭 하 고 새 항목을 추가 합니다. **배포 후 스크립트** > **사용자 스크립트** 를 선택 합니다. 기본 이름을 사용할 수 있습니다.

다음 T-sql 코드를 배포 후 스크립트에 추가 합니다. 이 스크립트는 일치 하는 레코드가 없는 경우에만 데이터베이스에 데이터를 추가 합니다. 데이터베이스에 입력 했을 수 있는 데이터는 덮어쓰거나 삭제 하지 않습니다.

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

배포 후 스크립트는 데이터베이스 프로젝트를 배포할 때마다 실행 된다는 점에 유의 해야 합니다. 따라서이 스크립트를 작성할 때 요구 사항을 신중 하 게 고려해 야 합니다. 경우에 따라 프로젝트가 배포 될 때마다 알려진 데이터 집합에서 시작할 수 있습니다. 다른 경우에는 기존 데이터를 변경 하지 않는 것이 좋습니다. 요구 사항에 따라 배포 후 스크립트 또는 스크립트에 포함 해야 하는 항목이 필요한 지 여부를 결정할 수 있습니다. 배포 후 스크립트를 사용 하 여 데이터베이스를 채우는 방법에 대 한 자세한 내용은 [SQL Server 데이터베이스 프로젝트에 데이터 포함](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)을 참조 하세요.

이제 4 개의 SQL 스크립트 파일이 있지만 실제 테이블은 없습니다. 데이터베이스 프로젝트를 localdb에 배포할 준비가 되었습니다. Visual Studio에서 시작 단추 (또는 F5)를 클릭 하 여 데이터베이스 프로젝트를 빌드하고 배포 합니다. **출력** 탭을 확인 하 여 빌드 및 배포가 성공 했는지 확인 합니다.

새 데이터베이스가 생성 되었는지 확인 하려면 **SQL Server 개체 탐색기** 를 열고 올바른 로컬 데이터베이스 서버 (이 경우 **localdb) \ProjectsV13**)에서 프로젝트 이름을 찾습니다.

테이블이 데이터로 채워져 있는지 확인 하려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 **데이터 보기**를 선택 합니다.

![테이블 데이터 표시](setting-up-database/_static/image9.png)

테이블 데이터의 편집 가능 뷰가 표시 됩니다. 예를 들어 **테이블** > **dbo** 를 선택 하 > 데이터를 **볼**경우 세 개의 열 (**코스**, **제목**및 **크레딧**)과 4 개의 행이 있는 테이블이 표시 됩니다.

## <a name="additional-resources"></a>추가 리소스

Code First 개발의 소개 예제는 [ASP.NET MVC 5 시작](../introduction/getting-started.md)을 참조 하세요. 고급 예제를 보려면 [ASP.NET MVC 4 앱에 대 한 Entity Framework 데이터 모델 만들기](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)를 참조 하세요.

사용할 Entity Framework 방식을 선택 하는 방법에 대 한 지침은 [개발 방법 Entity Framework](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)을 참조 하세요.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행합니다.

> [!div class="checklist"]
> * 데이터베이스 설정

웹 응용 프로그램 및 데이터 모델을 만드는 방법에 대해 알아보려면 다음 자습서로 이동 합니다.
> [!div class="nextstepaction"]
> [웹 응용 프로그램 및 데이터 모델 만들기](creating-the-web-application.md)
