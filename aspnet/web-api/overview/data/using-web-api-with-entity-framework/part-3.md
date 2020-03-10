---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Code First 마이그레이션를 사용 하 여 데이터베이스 초기값 | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78449117"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a>Code First 마이그레이션를 사용 하 여 데이터베이스 시드

[Mike Wasson](https://github.com/MikeWasson)

[완료 된 프로젝트 다운로드](https://github.com/MikeWasson/BookService)

이 섹션에서는 EF에서 [Code First 마이그레이션](https://msdn.microsoft.com/data/jj591621) 를 사용 하 여 테스트 데이터로 데이터베이스를 초기값으로 사용 합니다.

**도구** 메뉴에서 **NuGet 패키지 관리자**를 선택한 다음 **패키지 관리자 콘솔**을 선택 합니다. 패키지 관리자 콘솔 창에서 다음 명령을 입력합니다.

[!code-console[Main](part-3/samples/sample1.cmd)]

이 명령은 마이그레이션 폴더에 migration 이라는 폴더와 Configuration.cs 이라는 코드 파일을 추가 합니다.

![](part-3/_static/image1.png)

Configuration.cs 파일을 엽니다. 다음 **using** 문을 추가 합니다.

[!code-csharp[Main](part-3/samples/sample2.cs)]

그런 다음, 다음 코드를 **구성 초기값** 메서드에 추가 합니다.

[!code-csharp[Main](part-3/samples/sample3.cs)]

패키지 관리자 콘솔 창에서 다음 명령을 입력 합니다.

[!code-console[Main](part-3/samples/sample4.cmd)]

첫 번째 명령은 데이터베이스를 만드는 코드를 생성 하 고, 두 번째 명령은 해당 코드를 실행 합니다. 데이터베이스는 [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)를 사용 하 여 로컬로 만들어집니다.

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>API 탐색 (선택 사항)

F5 키를 눌러 디버그 모드에서 애플리케이션을 실행합니다. Visual Studio가 IIS Express를 시작 하 고 웹 앱을 실행 합니다. 그러면 Visual Studio가 브라우저를 시작 하 고 앱의 홈 페이지를 엽니다.

Visual Studio에서 웹 프로젝트를 실행 하는 경우 포트 번호를 할당 합니다. 아래 이미지에서 포트 번호는 50524입니다. 응용 프로그램을 실행 하면 다른 포트 번호가 표시 됩니다.

![](part-3/_static/image3.png)

홈 페이지는 ASP.NET MVC를 사용 하 여 구현 됩니다. 페이지 위쪽에 "API" 라는 링크가 있습니다. 이 링크를 통해 web API에 대 한 자동 생성 된 도움말 페이지로 이동할 수 있습니다. 이 도움말 페이지가 생성 되는 방법 및 페이지에 사용자 고유의 설명서를 추가 하는 방법에 대 한 자세한 내용은 [ASP.NET Web API에 대 한 도움말 페이지 만들기](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)를 참조 하세요. 도움말 페이지 링크를 클릭 하면 요청 및 응답 형식을 포함 하 여 API에 대 한 세부 정보를 볼 수 있습니다.

![](part-3/_static/image4.png)

API를 사용 하면 데이터베이스에서 CRUD 작업을 수행할 수 있습니다. 다음은 API를 요약 한 것입니다.

| Authors |  |
| --- | -- |
| GET api/authors | 모든 작성자를 가져옵니다. |
| GET api/authors/{id} | ID 별로 작성자를 가져옵니다. |
| POST /api/authors | 새 저자를 만듭니다. |
| PUT /api/authors/{id} | 기존 작성자를 업데이트 합니다. |
| DELETE /api/authors/{id} | 작성자를 삭제 합니다. |

| 서적 |  |
| --- | -- |
| GET /api/books | 모든 책을 가져옵니다. |
| GET /api/books/{id} | ID 별로 책을 가져옵니다. |
| POST /api/books | 새 책을 만듭니다. |
| PUT /api/books/{id} | 기존 책을 업데이트 합니다. |
| DELETE /api/books/{id} | 책을 삭제 합니다. |

## <a name="view-the-database-optional"></a>데이터베이스 보기 (옵션)

데이터베이스 업데이트 명령을 실행 한 경우 EF는 데이터베이스를 만들고 `Seed` 메서드를 호출 했습니다. 응용 프로그램을 로컬로 실행 하는 경우 EF는 [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)를 사용 합니다. Visual Studio에서 데이터베이스를 볼 수 있습니다. **보기** 메뉴에서 **SQL Server 개체 탐색기**를 선택합니다.

![](part-3/_static/image5.png)

**서버에 연결** 대화 상자의 **서버 이름** 입력란에 "(localdb) \v11.0"을 입력 합니다. **인증** 옵션을 "Windows 인증"으로 그대로 둡니다. **연결**을 클릭합니다.

![](part-3/_static/image6.png)

Visual Studio는 LocalDB에 연결 하 고 SQL Server 개체 탐색기 창에 기존 데이터베이스를 표시 합니다. 노드를 확장 하 여 EF에서 만든 테이블을 볼 수 있습니다.

![](part-3/_static/image7.png)

데이터를 보려면 테이블을 마우스 오른쪽 단추로 클릭 하 고 **데이터 보기**를 선택 합니다.

![](part-3/_static/image8.png)

다음 스크린샷에서는 Books 테이블의 결과를 보여 줍니다. EF는 데이터베이스를 초기값 데이터로 채우고 테이블에는 Authors 테이블에 대 한 외래 키가 포함 되어 있습니다.

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [이전](part-2.md)
> [다음](part-4.md)
