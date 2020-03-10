---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-cs
title: 데이터베이스 배포 (C#) | Microsoft Docs
author: rick-anderson
description: ASP.NET 웹 응용 프로그램을 배포 하면 개발 환경에서 프로덕션 환경으로 필요한 파일 및 리소스를 가져올 수 있습니다. Da의 경우 ...
ms.author: riande
ms.date: 04/23/2009
ms.assetid: ff537a10-9f1f-43fe-9bcb-3dda161ba8f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/deploying-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 83657be794e1ea31f6ad2f2b4adc274724d60cf2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78518321"
---
# <a name="deploying-a-database-c"></a>데이터베이스 배포(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드 다운로드](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_07_CS.zip) 또는 [PDF 다운로드](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial07_DeployDB_cs.pdf)

> ASP.NET 웹 응용 프로그램을 배포 하면 개발 환경에서 프로덕션 환경으로 필요한 파일 및 리소스를 가져올 수 있습니다. 데이터 기반 웹 응용 프로그램의 경우 데이터베이스 스키마 및 데이터를 포함 합니다. 이 자습서는 개발 환경에서 프로덕션 환경으로 데이터베이스를 성공적으로 배포 하는 데 필요한 단계를 탐색 하는 시리즈의 첫 번째 자습서입니다.

## <a name="introduction"></a>소개

ASP.NET 웹 응용 프로그램을 배포 하면 개발 환경에서 프로덕션 환경으로 필요한 파일 및 리소스를 가져올 수 있습니다. 지난 6 가지 자습서를 진행 하면서 간단한 책 리뷰 웹 응용 프로그램을 배포 하는 방법을 살펴보았습니다. 이 데모 사이트는 이미지 및 CSS 파일과 같은 클라이언트 쪽 리소스 (ASP.NET 페이지, 구성 파일, `Web.sitemap` 파일 등)로 구성 되어 있습니다. 하지만 데이터 기반 웹 응용 프로그램은 어떻습니까? 데이터베이스를 사용 하는 웹 응용 프로그램을 배포 하기 위해 수행 해야 하는 추가 단계는 무엇 인가요?

다음 몇 가지 자습서에서 데이터 기반 웹 응용 프로그램을 배포 하는 데 필요한 단계를 설명 합니다. 이 자습서에서는 먼저 개발 환경에서 프로덕션 환경으로 데이터베이스의 스키마와 콘텐츠를 가져오는 방법을 검사 하는 방법을 보여 줍니다 .이 자습서에서는 다음 자습서에서 필요한 구성 변경 내용을 살펴봅니다. 다음으로 애플리케이션 서비스 (멤버 자격, 역할, 프로필 등)를 사용 하는 데이터베이스를 배포 하는 문제를 살펴보겠습니다.

## <a name="examining-the-updated-book-reviews-web-application"></a>업데이트 된 책 리뷰 웹 응용 프로그램 검사

데이터 기반 웹 응용 프로그램을 배포 하는 것을 보여 주기 위해 책 리뷰 웹 응용 프로그램을 간단한 정적 웹 사이트에서 데이터 기반 웹 응용 프로그램으로 업데이트 했습니다. 이전 처럼이 자습서에서는 웹 응용 프로그램 프로젝트 모델을 사용 하는 응용 프로그램 및 웹 사이트 프로젝트 모델을 사용 하는 응용 프로그램의 두 가지 버전을 다운로드 합니다.

업데이트 된 책 리뷰 웹 응용 프로그램은 사이트 s `App_Data` 폴더 (`~/App_Data/Reviews.mdf`)에 저장 된 [SQL Server 2008 Express Edition](https://www.microsoft.com/express/sql/default.aspx) 데이터베이스를 사용 합니다. 컴퓨터에 SQL Server 2008가 설치 되어 있는 경우 데모를 오류 없이 실행 해야 합니다. 이전 버전의 SQL Server 있는 경우 무료 SQL Server 2008 Express Edition을 설치 하거나이 자습서의 다운로드에서 사용할 수 있는 데이터베이스 스크립트를 사용 하 여 데이터베이스를 직접 만들 수 있습니다.

`Reviews.mdf` 데이터베이스에는 네 개의 테이블이 있습니다.

- `Genres`-기술, Fiction 및 비즈니스와 같은 각 장르에 대 한 레코드를 포함 합니다.
- `Books`-`Title`, `GenreId`, `ReviewDate`, `Review`등의 열을 포함 하 여 각 검토에 대 한 레코드를 포함 합니다.
- `Authors`-검토 된 책을 제공한 각 저자에 대 한 정보를 포함 합니다.
- `BooksAuthors`-책을 쓴 작성자를 지정 하는 다대다 조인 테이블입니다.

그림 1에서는 이러한 4 개의 테이블에 대 한 ER 다이어그램을 보여 줍니다.

[책에서 웹 응용 프로그램 데이터베이스가 4 개의 테이블로 구성 되어 ![](deploying-a-database-cs/_static/image2.jpg)](deploying-a-database-cs/_static/image1.jpg) 

**그림 1**: 웹 응용 프로그램의 데이터베이스가 4 개의 테이블로 구성 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image3.jpg)).

이전 버전의 북 리뷰 웹 사이트에는 각 책에 대 한 별도의 ASP.NET 페이지가 있었습니다. 예를 들어 *24 시간 이내에 ASP.NET 3.5에*대 한 검토를 포함 하는 `~/Tech/TYASP35.aspx` 라는 페이지가 있었습니다. 이 새로운 데이터 기반 버전의 웹 사이트에는 데이터베이스에 저장 된 검토와 단일 ASP.NET 페이지 (.aspx? ID =*Bookid*)가 포함 되어 있으며,이는 지정 된 책에 대 한 검토를 표시 합니다. 마찬가지로 지정 된 장르에서 검토 된 책을 나열 하는 GenreId? ID = 페이지가 있습니다.

그림 2와 3에서는 `Genre.aspx` 및 `Review.aspx` 페이지를 보여 줍니다. 각 페이지의 주소 표시줄에서 URL을 확인 합니다. 그림 2에서이는 85d164ba-1123-4c47-82a0-c8ec75de7e0e? ID =입니다. 85d164ba-1123-4c47-82a0-c8ec75de7e0e는 기술 장르에 대 한 `GenreId` 값 이므로 페이지의 머리글은 "기술 검토"를 읽고 글머리 기호 목록은이 장르 아래에 있는 사이트에 대 한 검토를 열거 합니다.

[기술 장르 페이지 ![](deploying-a-database-cs/_static/image5.jpg)](deploying-a-database-cs/_static/image4.jpg) 

**그림 2**: 기술 장르 페이지 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image6.jpg))

[ASP.NET 3.5를 24 시간 이내에 학습 하기 위해 리뷰를 ![합니다.](deploying-a-database-cs/_static/image8.jpg)](deploying-a-database-cs/_static/image7.jpg) 

**그림 3**: *24 시간 이내에 ASP.NET 3.5를 알려* 주는 리뷰 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image9.jpg))

또한 책 리뷰 웹 응용 프로그램에는 관리자가 장르, 리뷰 및 저자 정보를 추가, 편집 및 삭제할 수 있는 관리 섹션이 포함 되어 있습니다. 현재 방문자가 관리 섹션에 액세스할 수 있습니다. 이후 자습서에서는 사용자 계정에 대 한 지원을 추가 하 고 권한 있는 사용자만 관리 페이지에 허용 합니다.

책 리뷰 응용 프로그램을 다운로드 하는 경우에는 데이터 기반 응용 프로그램을 배포 하는 방법을 설명 합니다. 응용 프로그램 디자인 만큼 모범 사례를 제시 하지는 않습니다. 예를 들어 별도의 DAL (데이터 액세스 계층)이 없습니다. ASP.NET 페이지는 코드 지향 클래스에서 SqlDataSource 컨트롤 또는 ADO.NET 코드를 통해 데이터베이스와 직접 통신 합니다. 계층화 된 아키텍처를 사용 하 여 데이터 기반 응용 프로그램을 만드는 방법에 대 한 자세한 내용은 my [ *data* 자습서로 작업](../../data-access/index.md)을 참조 하세요.

## <a name="databases-on-development-versus-production"></a>개발 및 프로덕션의 데이터베이스

데이터 기반 웹 응용 프로그램에서 개발을 시작 하는 경우 데이터베이스에 연결 하는 방법에 대 한 응용 프로그램 세부 정보를 제공 하는 데이터베이스 연결 문자열을 지정 해야 합니다. 이 연결 문자열은 데이터베이스 서버, 데이터베이스 이름 및 보안 정보를 지정 합니다. 가장 자주, 개발 중에 응용 프로그램에서 사용 하는 데이터베이스는 프로덕션 환경에 사용 되는 데이터베이스와 다릅니다. 개발과 프로덕션에는 서로 다른 데이터베이스를 사용 하는 경우 다양 한 이점이 있습니다. 개발 중에 다른 데이터베이스를 사용 하면 실수로 라이브 데이터를 수정 하거나 삭제 하는 것을 걱정 하지 않아도 됩니다. 또한 프로덕션 환경에서 응용 프로그램에 미치는 영향에 대해 걱정할 필요 없이 더미 테스트 데이터를 추가 하거나 데이터 모델에 대 한 주요 변경 내용을 적용할 수 있습니다. 개발 및 프로덕션 환경에서 다른 데이터베이스를 사용할 때의 단점은 응용 프로그램을 배포할 때 데이터베이스 스키마 또는 데이터에 대 한 모든 관련 변경 내용이 배포 되어야 한다는 것입니다.

첫 번째 배포 이전에는 데이터베이스 인스턴스가 하나 뿐 이며 해당 인스턴스가 개발 환경에 있습니다. 처음으로 프로덕션 환경에 응용 프로그램을 배포 하는 경우 필요한 서버 쪽 및 클라이언트 쪽 파일을 복사할 뿐만 아니라 개발 환경에서 프로덕션 환경으로 데이터베이스를 복사 해야 합니다. 현재 책 리뷰 웹 응용 프로그램을 사용 하 고 있습니다. 데이터베이스는 개발 환경의 `App_Data` 폴더에 있지만 아직 프로덕션 환경으로 푸시되 지 않았습니다.

응용 프로그램이 배포 되 면 데이터베이스의 복사본 두 개가 있습니다. 응용 프로그램이 완성 되 면 새 기능을 추가할 수 있습니다. 즉, 기존 테이블에 새 열을 추가 하거나 기존 열을 변경 하 고 새 테이블을 추가 하는 등의 작업을 수행 합니다. 웹 응용 프로그램이 다음에 배포 되 면 마지막 배포 이후 개발 환경의 데이터베이스에 적용 된 변경 내용을 프로덕션 데이터베이스에 적용 해야 합니다. 이 프로세스를 관리 하기 위한 몇 가지 전략은 이후 자습서에서 설명 합니다. 이 자습서에서는 개발 환경에서 프로덕션 환경으로 전체 데이터베이스를 배포 하는 방법을 집중적으로 설명 합니다.

## <a name="deploying-the-database-to-the-production-environment"></a>프로덕션 환경에 데이터베이스 배포

이 자습서의 나머지 부분에서는 개발 환경에서 프로덕션 환경으로 데이터베이스를 배포 하는 방법을 보여 줍니다. 함께 사용 하는 경우 웹 호스트 공급자의 계정에 Microsoft SQL Server 데이터베이스 지원이 포함 되어 있는지 확인 해야 합니다. 또한 데이터베이스 서버 이름, 데이터베이스 이름 및 데이터베이스에 연결 하는 데 사용 되는 사용자 이름 및 암호와 같은 일부 정보를 제공 해야 합니다.

이 자습서의 앞부분에서 설명한 것 처럼 웹 사이트의 데이터베이스는 `App_Data` 폴더에 저장 된 SQL Server 2008 Express Edition 데이터베이스입니다. 이러한 데이터베이스를 배포 하는 것은 개발 환경에서 프로덕션 환경으로 `App_Data` 폴더를 복사 하는 것 처럼 간단 합니다. 그러나 대부분의 웹 호스트 공급자는 보안상의 이유로 `App_Data` 폴더에 있는 데이터베이스 호스팅을 지원 하지 않습니다. 대신 웹 호스트는 환경 내의 SQL Server 데이터베이스 서버에 계정을 제공 합니다. 개발 환경에서 프로덕션 환경으로 데이터베이스를 배포 하려면 웹 호스트의 데이터베이스 서버에 데이터베이스를 등록 해야 합니다.

그렇다면 개발 환경에서 프로덕션 환경으로 데이터베이스를 어떻게 가져올 수 있나요? 웹 호스트에서 제공 하는 서비스에 따라이 작업을 수행 하는 몇 가지 방법이 있습니다. 일부 호스트 (예: DiscountASP.NET)를 사용 하 여 데이터베이스 또는 실제 `.mdf` 파일의 백업을 웹 사이트로 FTP 한 다음 제어판에서 백업 파일을 복원 하거나 `.mdf` 파일을 SQL Server 데이터베이스 서버에 연결할 수 있습니다. 이러한 도구를 사용 하 여 데이터베이스를 배포 하는 것은 `App_Data` 폴더를 프로덕션 환경에 복사한 다음 제어판을 통해 연결 하는 것 만큼 간단 합니다. 이는 데이터베이스를 처음으로 게시 하는 가장 쉽고 빠른 방법입니다.

또 다른 방법은 데이터베이스 게시 마법사를 사용 하는 것입니다. 데이터베이스 게시 마법사는 데이터베이스의 스키마 (테이블, 저장 프로시저, 뷰, 사용자 정의 함수 등)를 만드는 SQL 명령을 생성 하 고 필요에 따라 테이블의 데이터를 생성 하는 Windows 데스크톱 응용 프로그램입니다. 그런 다음 SQL Server Management Studio 통해 웹 호스트 공급자의 데이터베이스 서버에 연결한 다음이 스크립트를 실행 하 여 프로덕션 환경에서 데이터베이스를 복제할 수 있습니다. 웹 호스트 공급자가 Microsoft [데이터베이스 게시 서비스](http://www.codeplex.com/sqlhost/Wiki/View.aspx?title=Database%20Publishing%20Services&amp;referringTitle=Home) 를 지 원하는 경우에도 데이터베이스 게시 마법사에서 생성 된 스크립트가 사용자 대신 데이터베이스 서버에서 자동으로 실행 되도록 할 수 있습니다. 데이터베이스 게시 마법사는 데이터베이스의 스키마와 데이터를 만드는 스크립트를 생성 하므로 웹 호스트 공급자가 업로드 된 `.mdf` 파일 첨부와 같은 기능을 제공 하는지 여부에 관계 없이 작동 합니다.

### <a name="generating-the-sql-commands-to-create-the-database-schema-and-data-using-the-database-publishing-wizard"></a>데이터베이스 게시 마법사를 사용 하 여 데이터베이스 스키마 및 데이터를 만드는 SQL 명령 생성

데이터베이스 게시 마법사를 사용 하 여 책 리뷰 데이터베이스를 프로덕션에 배포 하는 방법을 살펴보겠습니다. Visual Studio 2008 이상을 사용 하는 경우 데이터베이스 게시 마법사가 이미 설치 되어 있습니다. Visual Studio 2005을 사용 하는 경우 먼저 마법사를 다운로드 하 여 [설치](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en) 해야 합니다.

Visual Studio를 열고 `Reviews.mdf` 데이터베이스로 이동 합니다. Visual Web Developer를 사용 하는 경우 데이터베이스 탐색기로 이동 합니다. Visual Studio를 사용 하는 경우 서버 탐색기를 사용 합니다. 그림 4는 Visual Web Developer의 데이터베이스 탐색기에 `Reviews.mdf` 데이터베이스를 보여 줍니다. 그림 4에 표시 된 것 처럼 `Reviews.mdf` 데이터베이스는 네 개의 테이블, 세 개의 저장 프로시저 및 사용자 정의 함수로 구성 됩니다.

[데이터베이스 탐색기 또는 서버 탐색기에서 데이터베이스를 찾을 ![](deploying-a-database-cs/_static/image11.jpg)](deploying-a-database-cs/_static/image10.jpg) 

**그림 4**: 데이터베이스 탐색기 또는 서버 탐색기에서 데이터베이스 찾기 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image12.jpg))

데이터베이스 이름을 마우스 오른쪽 단추로 클릭 하 고 상황에 맞는 메뉴에서 "공급자에 게시" 옵션을 선택 합니다. 그러면 데이터베이스 게시 마법사가 시작 됩니다 (그림 5 참조). 시작 화면을 벗어나 이동 하려면 다음을 클릭 합니다.

[데이터베이스 게시 마법사 시작 화면 ![](deploying-a-database-cs/_static/image14.jpg)](deploying-a-database-cs/_static/image13.jpg) 

**그림 5**: 데이터베이스 게시 마법사 시작 화면 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image15.jpg))

마법사의 두 번째 화면에는 데이터베이스 게시 마법사에 액세스할 수 있는 데이터베이스가 나열 되며 선택한 데이터베이스의 모든 개체를 스크립팅할 지 아니면 스크립팅할 개체를 선택할 수 있습니다. 적절 한 데이터베이스를 선택 하 고 "선택한 데이터베이스의 모든 개체 스크립팅" 옵션을 선택 된 상태로 둡니다.

> [!NOTE]
> 그림 6에 표시 된 화면에서 다음을 클릭할 때 "이 마법사에서 스크립팅할 수 있는 유형의 데이터베이스 *databaseName* 에 개체가 없습니다." 오류가 표시 되 면 데이터베이스 파일의 경로가 너무 길지 않은지 확인 합니다. 데이터베이스 파일 경로가 너무 길면이 오류가 발생할 수 있음을 발견 했습니다.

[데이터베이스 게시 마법사 시작 화면 ![](deploying-a-database-cs/_static/image17.jpg)](deploying-a-database-cs/_static/image16.jpg) 

**그림 6**: 데이터베이스 게시 마법사 시작 화면 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image18.jpg))

다음 화면에서 스크립트 파일을 생성 하거나 웹 호스트에서 지 원하는 경우 데이터베이스를 웹 호스트 공급자의 데이터베이스 서버에 직접 게시 합니다. 그림 7에 표시 된 것 처럼 스크립트는 파일 `C:\REVIEWS.MDF.sql`에 기록 됩니다.

[데이터베이스를 파일에 스크립팅 ![웹 호스트 공급자에 게 직접 게시](deploying-a-database-cs/_static/image20.jpg)](deploying-a-database-cs/_static/image19.jpg) 

**그림 7**: 데이터베이스를 파일로 스크립팅 하거나 웹 호스트 공급자에 직접 게시 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image21.jpg))

이후 화면에는 다양 한 스크립팅 옵션을 묻는 메시지가 표시 됩니다. 스크립트에서 drop 문을 포함 하 여 이러한 기존 개체를 제거할지 여부를 지정할 수 있습니다. 기본값은 True로, 처음으로 데이터베이스를 배포 하는 경우에는 괜찮습니다. 대상 데이터베이스가 SQL Server 2000, SQL Server 2005 또는 SQL Server 2008 인지 여부도 지정할 수 있습니다. 마지막으로 스키마와 데이터를 스크립팅할 지, 데이터만 포함할지, 아니면 스키마만 스크립팅할 지를 나타낼 수 있습니다. 스키마는 데이터베이스 개체, 테이블, 저장 프로시저, 뷰 등의 컬렉션입니다. 데이터는 테이블에 있는 정보입니다.

그림 8에 나와 있는 것 처럼 마법사는 기존 데이터베이스 개체를 삭제 하 고 SQL Server 2008 데이터베이스에 대 한 스크립트를 생성 하 고 스키마와 데이터를 모두 게시 하도록 구성 했습니다.

[게시 옵션을 지정 ![](deploying-a-database-cs/_static/image23.jpg)](deploying-a-database-cs/_static/image22.jpg) 

**그림 8**: 게시 옵션 지정 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image24.jpg))

마지막 두 개의 화면에는 수행할 작업이 요약 되어 있으며 스크립팅 상태를 표시 합니다. 마법사를 실행 한 결과, 프로덕션 환경에서 데이터베이스를 만들고 개발과 동일한 데이터를 채우는 데 필요한 SQL 명령을 포함 하는 스크립트 파일이 있습니다.

### <a name="executing-the-sql-commands-on-the-production-environment-database"></a>프로덕션 환경 데이터베이스에서 SQL 명령 실행

이제 데이터베이스를 만드는 SQL 명령을 포함 하는 스크립트와 해당 데이터는 프로덕션 데이터베이스에서 스크립트를 실행 하는 것으로 남아 있습니다. 일부 웹 호스트 공급자는 해당 제어판에서 SQL 명령을 입력 하 여 데이터베이스에서 실행할 수 있는 텍스트 상자를 제공 합니다. 매우 큰 스크립트 파일이 있는 경우이 옵션이 작동 하지 않을 수 있습니다 (예를 들어 `REVIEWS.MDF.sql` 스크립트 파일의 크기가 425 KB를 초과 함).

SQL Server Management Studio (SSMS)를 사용 하 여 프로덕션 데이터베이스 서버에 직접 연결 하는 것이 더 나은 방법입니다. SQL Server Express 버전이 아닌 버전이 컴퓨터에 설치 되어 있는 경우 SSMS가 이미 설치 되어 있을 가능성이 높습니다. 그렇지 않으면 SQL Server Management Studio Express Edition의 무료 복사본을 [다운로드 하 여 설치할](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en) 수 있습니다.

SSMS를 실행 하 고 웹 호스트 공급자가 제공한 정보를 사용 하 여 웹 호스트의 데이터베이스 서버에 연결 합니다.

[웹 호스트 공급자의 데이터베이스 서버에 연결 ![](deploying-a-database-cs/_static/image26.jpg)](deploying-a-database-cs/_static/image25.jpg) 

**그림 9**: 웹 호스트 공급자의 데이터베이스 서버에 연결 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image27.jpg))

데이터베이스 탭을 확장 하 고 데이터베이스를 찾습니다. 도구 모음의 왼쪽 상단 모서리에 있는 새 쿼리 단추를 클릭 하 고 데이터베이스 게시 마법사를 통해 생성 된 스크립트 파일의 SQL 명령을 붙여넣은 다음 실행 단추를 클릭 하 여 프로덕션 데이터베이스 서버에서 이러한 명령을 실행 합니다. 스크립트 파일이 특히 크면 명령을 실행 하는 데 몇 분 정도 걸릴 수 있습니다.

[웹 호스트 공급자의 데이터베이스 서버에 연결 ![](deploying-a-database-cs/_static/image29.jpg)](deploying-a-database-cs/_static/image28.jpg) 

**그림 10**: 웹 호스트 공급자의 데이터베이스 서버에 연결 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image30.jpg))

이것이 전부입니다! 이 시점에서 개발 데이터베이스는 프로덕션으로 중복 됩니다. SSMS에서 데이터베이스를 새로 고치면 새 데이터베이스 개체가 표시 됩니다. 그림 11에서는 프로덕션 데이터베이스의 테이블, 저장 프로시저 및 사용자 정의 함수를 보여 줍니다 .이 함수는 개발 데이터베이스에 있는 테이블, 저장 프로시저 및 사용자 정의 함수를 반영 합니다. 그리고 데이터베이스 게시 마법사에서 데이터를 게시 하도록 지시 했으므로 마법사가 실행 될 때 프로덕션 데이터베이스의 테이블에는 개발 데이터베이스 테이블과 동일한 데이터가 포함 됩니다. 그림 12는 프로덕션 데이터베이스의 `Books` 테이블에 있는 데이터를 보여 줍니다.

[프로덕션 데이터베이스에서 데이터베이스 개체가 복제 ![](deploying-a-database-cs/_static/image32.jpg)](deploying-a-database-cs/_static/image31.jpg) 

**그림 11**: 데이터베이스 개체가 프로덕션 데이터베이스에서 중복 되었습니다 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image33.jpg)).

[프로덕션 데이터베이스에 개발 데이터베이스와 같은 데이터가 포함 된 ![](deploying-a-database-cs/_static/image35.jpg)](deploying-a-database-cs/_static/image34.jpg) 

**그림 12**: 프로덕션 데이터베이스에 개발 데이터베이스와 동일한 데이터가 포함 되어 있습니다 ([전체 크기 이미지를 보려면 클릭](deploying-a-database-cs/_static/image36.jpg)).

이 시점에서는 개발 데이터베이스를 프로덕션 환경에만 배포 했습니다. 아직 웹 응용 프로그램을 배포 하거나 프로덕션 환경에서 응용 프로그램이 프로덕션 데이터베이스를 사용 하는 데 필요한 구성 변경 내용을 검토 하지 않았습니다. 다음 자습서에서 이러한 문제를 살펴보겠습니다.

## <a name="summary"></a>요약

데이터 기반 웹 응용 프로그램을 배포 하려면 개발 중에 사용 되는 데이터베이스를 프로덕션 환경으로 복사 해야 합니다. 많은 웹 호스트 공급자는 데이터베이스 배포 프로세스를 간소화 하는 도구를 제공 합니다. 예를 들어 DiscountASP.NET를 사용 하 여 데이터베이스 `.mdf` 파일 (또는 백업)을 FTP 한 다음 제어판에서 데이터베이스 서버에 데이터베이스를 연결할 수 있습니다. 웹 호스트 공급자가 제공 하는 기능에 관계 없이 작동 하는 또 다른 옵션은 Microsoft s 데이터베이스 게시 마법사 도구입니다 .이 도구는 개발 데이터베이스의 스키마 및 데이터를 만드는 SQL 명령의 스크립트를 생성 합니다. 이 스크립트가 생성 되 면 프로덕션 데이터베이스에서 실행할 수 있습니다.

이제 웹 응용 프로그램의 데이터베이스를 프로덕션 환경에서 검토 했으므로 응용 프로그램을 배포할 수 있습니다. 그러나 웹 응용 프로그램의 구성 정보는 데이터베이스에 대 한 연결 문자열을 지정 하 고 해당 연결 문자열은 개발 데이터베이스를 참조 합니다. 프로덕션에 사이트를 배포할 때이 연결 문자열 정보를 업데이트 해야 합니다. 다음 자습서에서는 이러한 구성의 차이점을 확인 하 고 데이터 기반 서적 검토 사이트를 프로덕션에 게시 하는 데 필요한 단계를 안내 합니다.

행복 한 프로그래밍

#### <a name="further-reading"></a>추가 참고 자료

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [Microsoft SQL Server 데이터베이스 게시 마법사 다운로드 1.1](https://www.microsoft.com/downloads/details.aspx?familyid=56E5B1C5-BF17-42E0-A410-371A838E570A&amp;displaylang=en)
- [Express Edition Management Studio Microsoft SQL Server 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyId=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796&amp;displaylang=en)

> [!div class="step-by-step"]
> [이전](core-differences-between-iis-and-the-asp-net-development-server-cs.md)
> [다음](configuring-the-production-web-application-to-use-the-production-database-cs.md)
