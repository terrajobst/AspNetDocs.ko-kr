---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
title: ASP.NET MVC를 사용 하 여 15 분 내에 영화 데이터베이스 응용 프로그램 만들기 (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther는 전체 데이터베이스 기반 ASP.NET MVC 응용 프로그램을 처음부터 끝까지 빌드합니다. 이 자습서는 새로운 사용자를 위한 유용한 정보를 소개 합니다.
ms.author: riande
ms.date: 01/27/2009
ms.assetid: e4ba9786-734c-4eb3-91bb-089793325d0d
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb
msc.type: authoredcontent
ms.openlocfilehash: 0ce8161d29a8ab4005e2b20462b08c9e10ee815a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595737"
---
# <a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-vb"></a>ASP.NET MVC를 사용하여 15분 만에 영화 데이터베이스 애플리케이션 만들기(VB)

[Stephen Walther](https://github.com/StephenWalther)

[코드 다운로드](https://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_VB.zip)

> Stephen Walther는 전체 데이터베이스 기반 ASP.NET MVC 응용 프로그램을 처음부터 끝까지 빌드합니다. 이 자습서는 ASP.NET MVC 프레임 워크를 처음 접하는 사용자와 ASP.NET MVC 응용 프로그램 빌드 프로세스를 이해 하려는 사용자를 위한 유용한 정보를 제공 합니다.

이 자습서에서는 ASP.NET MVC 응용 프로그램을 작성 하는 "것과 같은 의미"를 제공 합니다. 이 자습서에서는 전체 ASP.NET MVC 응용 프로그램을 개발 하는 과정을 처음부터 끝까지 폭발 했습니다. 데이터베이스 레코드를 나열 하 고 만들고 편집할 수 있는 방법을 보여 주는 간단한 데이터베이스 기반 응용 프로그램을 빌드하는 방법을 보여 줍니다.

응용 프로그램 빌드 프로세스를 간소화 하기 위해 Visual Studio 2008의 스 캐 폴딩 기능을 활용 합니다. Visual Studio에서 컨트롤러, 모델 및 뷰에 대 한 초기 코드와 콘텐츠를 생성 하도록 합니다.

Active Server 페이지 또는 ASP.NET으로 작업 한 경우 ASP.NET MVC를 매우 잘 알고 있어야 합니다. ASP.NET MVC 뷰는 Active Server Pages 응용 프로그램의 페이지와 매우 비슷합니다. 기존 ASP.NET Web Forms 응용 프로그램과 마찬가지로 ASP.NET MVC는 .NET framework에서 제공 하는 다양 한 언어 및 클래스에 대 한 모든 권한을 제공 합니다.

이 자습서에서는 ASP.NET MVC 응용 프로그램을 빌드하는 환경이 Active Server 페이지 또는 ASP.NET Web Forms 응용 프로그램을 구축 하는 환경과 비슷하거나 다른 지를 보여 줍니다.

## <a name="overview-of-the-movie-database-application"></a>동영상 데이터베이스 응용 프로그램 개요

우리의 목표는 간단 하 게 유지 하는 것 이기 때문에 매우 간단한 영화 데이터베이스 응용 프로그램을 빌드할 것입니다. 간단한 영화 데이터베이스 응용 프로그램에서는 다음 세 가지 작업을 수행할 수 있습니다.

1. 동영상 데이터베이스 레코드 집합 나열
2. 새 동영상 데이터베이스 레코드 만들기
3. 기존 동영상 데이터베이스 레코드 편집

무엇 보다도 간단 하 게 유지 하기 위해 응용 프로그램을 빌드하는 데 필요한 ASP.NET MVC 프레임 워크의 최소 기능을 활용할 수 있습니다. 예를 들어 테스트 기반 개발을 활용할 수 없습니다.

응용 프로그램을 만들려면 다음 단계를 각각 완료 해야 합니다.

1. ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기
2. 데이터베이스 만들기
3. 데이터베이스 모델 만들기
4. ASP.NET MVC 컨트롤러 만들기
5. ASP.NET MVC 뷰 만들기

## <a name="preliminaries"></a>Preliminaries

ASP.NET MVC 응용 프로그램을 빌드하려면 Visual Studio 2008 또는 Visual Web Developer 2008 Express가 필요 합니다. ASP.NET MVC 프레임 워크도 다운로드 해야 합니다.

Visual Studio 2008을 소유 하 고 있지 않은 경우이 웹 사이트에서 Visual Studio 2008의 90 일 평가판 버전을 다운로드할 수 있습니다.

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

또는 Visual Web Developer Express 2008를 사용 하 여 ASP.NET MVC 응용 프로그램을 만들 수 있습니다. Visual Web Developer Express를 사용 하기로 결정 한 경우에는 서비스 팩 1이 설치 되어 있어야 합니다. 이 웹 사이트에서 Visual Web Developer 2008 Express 서비스 팩 1을 다운로드할 수 있습니다.

[https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

Visual Studio 2008 또는 Visual Web Developer 2008를 설치한 후 ASP.NET MVC 프레임 워크를 설치 해야 합니다. ASP.NET MVC 프레임 워크는 다음 웹 사이트에서 다운로드할 수 있습니다.

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> ASP.NET framework 및 ASP.NET MVC 프레임 워크를 개별적으로 다운로드 하는 대신 웹 플랫폼 설치 관리자를 활용할 수 있습니다. 웹 플랫폼 설치 관리자는 컴퓨터에 설치 된 응용 프로그램을 쉽게 관리할 수 있도록 하는 응용 프로그램입니다.
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)

## <a name="creating-an-aspnet-mvc-web-application-project"></a>ASP.NET MVC 웹 응용 프로그램 프로젝트 만들기

먼저 Visual Studio 2008에서 새 ASP.NET MVC 웹 응용 프로그램 프로젝트를 만들어 보겠습니다. 메뉴 옵션 **파일, 새 프로젝트** 를 선택 하면 그림 1에 새 프로젝트 대화 상자가 표시 됩니다. 프로그래밍 언어로 Visual Basic를 선택 하 고 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿을 선택 합니다. 프로젝트 이름을 MovieApp로 지정 하 고 확인 단추를 클릭 합니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image1.png)

**그림 01**: 새 프로젝트 대화 상자 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.png))

새 프로젝트 대화 상자의 맨 위에 있는 드롭다운 목록에서 .NET Framework 3.5을 선택 하거나 ASP.NET MVC 웹 응용 프로그램 프로젝트 템플릿이 나타나지 않도록 합니다.

새 MVC 웹 응용 프로그램 프로젝트를 만들 때마다 Visual Studio에서 별도의 단위 테스트 프로젝트를 만들라는 메시지를 표시 합니다. 그림 2의 대화 상자가 나타납니다. 시간 제약 조건으로 인해이 자습서에서 테스트를 만들 수 없기 때문에 (그리고, 예,이에 대 한 약간의 범하고 확인 해야 함) **아니요** 옵션을 선택 하 고 **확인** 단추를 클릭 합니다.

> [!NOTE] 
> 
> Visual Web Developer는 테스트 프로젝트를 지원 하지 않습니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.png)

**그림 02**: 단위 테스트 프로젝트 만들기 대화 상자 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.png))

ASP.NET MVC 응용 프로그램에는 모델, 뷰 및 컨트롤러 폴더의 표준 폴더 집합이 있습니다. 솔루션 탐색기 창에서이 표준 폴더 집합을 볼 수 있습니다. 동영상 데이터베이스 응용 프로그램을 빌드하기 위해 각 모델, 뷰 및 컨트롤러 폴더에 파일을 추가 해야 합니다.

Visual Studio를 사용 하 여 새 MVC 응용 프로그램을 만들면 샘플 응용 프로그램을 얻게 됩니다. 처음부터 시작 하려고 하기 때문에이 샘플 응용 프로그램에 대 한 콘텐츠를 삭제 해야 합니다. 다음 파일 및 폴더를 삭제 해야 합니다.

- Controllers\HomeController.vb
- Views\Home

## <a name="creating-the-database"></a>데이터베이스 만들기

동영상 데이터베이스 레코드를 보관할 데이터베이스를 만들어야 합니다. 다행히 Visual Studio에는 SQL Server Express 이라는 무료 데이터베이스가 포함 되어 있습니다. 데이터베이스를 만들려면 다음 단계를 수행 합니다.

1. 솔루션 탐색기 창에서 App\_Data 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목을**차례로 선택 합니다.
2. **데이터** 범주를 선택 하 고 **SQL Server 데이터베이스** 템플릿을 선택 합니다 (그림 3 참조).
3. 새 데이터베이스의 이름을 *MoviesDB* 로 추가 하 고 **추가** 단추를 클릭 합니다.

데이터베이스를 만든 후에는 App\_Data 폴더에 있는 MoviesDB 파일을 두 번 클릭 하 여 데이터베이스에 연결할 수 있습니다. MoviesDB 파일을 두 번 클릭 하면 서버 탐색기 창이 열립니다.

> [!NOTE] 
> 
> 서버 탐색기 창에는 Visual Web Developer의 경우 데이터베이스 탐색기 창으로 이름이 지정 됩니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.png)

**그림 03**: Microsoft SQL Server 데이터베이스 만들기 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.png))

다음으로 새 데이터베이스 테이블을 만들어야 합니다. 서버 탐색기 창에서 테이블 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **새 테이블 추가**를 선택 합니다. 이 메뉴 옵션을 선택 하면 데이터베이스 테이블 디자이너가 열립니다. 다음 데이터베이스 열을 만듭니다.

<a id="0.2_table01"></a>

| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| ID | 정수 | False |
| 제목 | Nvarchar (100) | False |
| Idm | Nvarchar (100) | False |
| DateReleased | DateTime | False |

첫 번째 열인 Id 열에는 두 개의 특수 속성이 있습니다. 먼저 Id 열을 기본 키 열로 표시 해야 합니다. Id 열을 선택한 후 **기본 키 설정** 단추를 클릭 합니다 (키 처럼 보이는 아이콘). 둘째, Id 열을 id 열로 표시 해야 합니다. 속성 창 열에서 Id 사양 섹션으로 스크롤하고 확장 합니다. **Is Identity** 속성을 **Yes**값으로 변경 합니다. 작업이 완료 되 면 그림 4와 같이 테이블이 표시 됩니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.png)

**그림 04**: 동영상 데이터베이스 테이블 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.png))

마지막 단계는 새 테이블을 저장 하는 것입니다. 저장 단추 (플로피 아이콘)를 클릭 하 고 새 테이블에 영화 이름을 지정 합니다.

테이블 만들기를 완료 한 후에는 테이블에 일부 영화 레코드를 추가 합니다. 서버 탐색기 창에서 동영상 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **테이블 데이터 표시**를 선택 합니다. 즐겨 찾는 동영상 목록을 입력 합니다 (그림 5 참조).

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.png)

**그림 05**: 동영상 레코드 입력 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.png))

## <a name="creating-the-model"></a>모델 만들기

다음에는 데이터베이스를 나타내는 클래스 집합을 만들어야 합니다. 데이터베이스 모델을 만들어야 합니다. Microsoft Entity Framework를 활용 하 여 데이터베이스 모델에 대 한 클래스를 자동으로 생성 합니다.

> [!NOTE] 
> 
> ASP.NET MVC 프레임 워크는 Microsoft Entity Framework에 연결 되지 않습니다. LINQ to SQL, Subsonic 및 NHibernate 모드를 비롯 한 다양 한 개체 관계형 매핑 (또는/M) 도구를 활용 하 여 데이터베이스 모델 클래스를 만들 수 있습니다.

엔터티 데이터 모델 마법사를 시작 하려면 다음 단계를 수행 합니다.

1. 솔루션 탐색기 창에서 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 새 항목을**차례로 선택 합니다.
2. **데이터** 범주를 선택 하 고 **ADO.NET 엔터티 데이터 모델** 템플릿을 선택 합니다.
3. 데이터 모델에 *MoviesDBModel* 의 이름을 지정 하 고 **추가** 단추를 클릭 합니다.

추가 단추를 클릭 하면 엔터티 데이터 모델 마법사가 나타납니다 (그림 6 참조). 마법사를 완료 하려면 다음 단계를 수행 합니다.

1. **모델 콘텐츠 선택** 단계에서 **데이터베이스에서 생성** 옵션을 선택 합니다.
2. **데이터 연결 선택** 단계에서 연결 설정에 대해 *MoviesDB* 데이터 연결 및 이름 *MoviesDBEntities* 을 사용 합니다. **다음** 단추를 클릭 합니다.
3. **데이터베이스 개체 선택** 단계에서 테이블 노드를 확장 하 고 동영상 테이블을 선택 합니다. *MovieApp* 네임 스페이스를 입력 하 고 **마침** 단추를 클릭 합니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.png)

**그림 06**: 엔터티 데이터 모델 마법사를 사용 하 여 데이터베이스 모델 생성 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.png))

엔터티 데이터 모델 마법사를 완료 하면 엔터티 데이터 모델 디자이너가 열립니다. 디자이너에 영화 데이터베이스 테이블이 표시 됩니다 (그림 7 참조).

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.png)

**그림 07**: 엔터티 데이터 모델 디자이너 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.png))

계속 하기 전에 한 가지 변경 작업을 수행 해야 합니다. 엔터티 데이터 마법사는 동영상 데이터베이스 테이블을 나타내는 영화 라는 모델 클래스를 생성 합니다. 영화 클래스를 사용 하 여 특정 영화를 나타내므로 클래스의 *이름을 동영상이* *아닌 영화 (* 복수형이 아닌 단일 영화)로 수정 해야 합니다.

디자이너 화면에서 클래스의 이름을 두 번 클릭 하 고 클래스의 이름을 동영상에서 동영상으로 변경 합니다. 이렇게 변경한 후에는 **저장** 단추 (플로피 디스크의 아이콘)를 클릭 하 여 Movie 클래스를 생성 합니다.

## <a name="creating-the-aspnet-mvc-controller"></a>ASP.NET MVC 컨트롤러 만들기

다음 단계는 ASP.NET MVC 컨트롤러를 만드는 것입니다. 컨트롤러는 사용자가 ASP.NET MVC 응용 프로그램과 상호 작용 하는 방법을 제어 해야 합니다.

다음 단계를 수행하십시오.

1. 솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가, 컨트롤러**를 선택 합니다.
2. 컨트롤러 추가 대화 상자에서 이름 *HomeController* 을 입력 하 고 **Create, Update 및 Details 시나리오에 대 한 작업 메서드 추가** 라는 확인란을 선택 합니다 (그림 8 참조).
3. **추가** 단추를 클릭 하 여 새 컨트롤러를 프로젝트에 추가 합니다.

이러한 단계를 완료 한 후에는 1을 나열 하는 컨트롤러가 생성 됩니다. Index, Details, Create 및 Edit 라는 메서드가 포함 되어 있습니다. 다음 섹션에서는 이러한 메서드가 작동 하도록 하는 데 필요한 코드를 추가 합니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image15.png)

**그림 08**: 새 ASP.NET MVC 컨트롤러 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image16.png))

**목록 1 – Controllers\HomeController.vb**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample1.vb)]

## <a name="listing-database-records"></a>데이터베이스 레코드 나열

Home 컨트롤러의 Index () 메서드는 ASP.NET MVC 응용 프로그램의 기본 메서드입니다. ASP.NET MVC 응용 프로그램을 실행 하는 경우 Index () 메서드는 호출 되는 첫 번째 컨트롤러 메서드입니다.

Index () 메서드를 사용 하 여 영화 데이터베이스 테이블의 레코드 목록을 표시 합니다. Index () 메서드를 사용 하 여 영화 데이터베이스 레코드를 검색 하기 위해 이전에 만든 데이터베이스 모델 클래스를 활용 합니다.

\_db 라는 새 private 필드를 포함 하도록 목록 2에서 HomeController 클래스를 수정 했습니다. MoviesDBEntities 클래스는 데이터베이스 모델을 나타내며이 클래스를 사용 하 여 데이터베이스와 통신 합니다.

또한 목록 2에서 Index () 메서드를 수정 했습니다. Index () 메서드는 MoviesDBEntities 클래스를 사용 하 여 영화 데이터베이스 테이블에서 모든 동영상 레코드를 검색 합니다. 식 *\_db입니다. MovieSet ()* 는 동영상 데이터베이스 테이블의 모든 동영상 레코드 목록을 반환 합니다.

영화 목록이 보기에 전달 됩니다. View () 메서드에 전달 되는 모든 항목은 뷰 데이터로 뷰에 전달 됩니다.

**목록 2 – Controllers/HomeController (수정 된 인덱스 메서드)**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample2.vb)]

Index () 메서드는 Index 라는 뷰를 반환 합니다. 동영상 데이터베이스 레코드 목록을 표시 하려면이 뷰를 만들어야 합니다. 다음 단계를 수행하십시오.

**뷰 추가** 대화 상자를 열기 전에 프로젝트를 빌드하거나 ( **빌드, 솔루션 빌드**) 메뉴 옵션을 선택 해야 합니다. 그렇지 않으면 **데이터 클래스 보기** 드롭다운 목록에 클래스가 표시 되지 않습니다.

1. 코드 편집기에서 Index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **뷰 추가** 를 선택 합니다 (그림 9 참조).
2. 보기 추가 대화 상자에서 **강력한 형식의 뷰 만들기** 확인란을 선택 했는지 확인 합니다.
3. **콘텐츠 보기** 드롭다운 목록에서 값 *목록*을 선택 합니다.
4. **데이터 클래스 보기** 드롭다운 목록에서 *MovieApp*값을 선택 합니다.
5. 추가 단추를 클릭 하 여 새 보기를 만듭니다 (그림 10 참조).

이러한 단계를 완료 하면 Views\Home 폴더에 Index .aspx 이라는 새 보기가 추가 됩니다. 인덱스 뷰의 내용은 목록 3에 포함 되어 있습니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image17.png)

**그림 09**: 컨트롤러 작업에서 뷰 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image18.png))

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image19.png)

**그림 10**: 보기 추가 대화 상자를 사용 하 여 새 보기 만들기 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image20.png))

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample3.aspx)]

인덱스 뷰는 HTML 테이블 내의 동영상 데이터베이스 테이블에 있는 모든 동영상 레코드를 표시 합니다. 뷰에는 ViewData 속성이 나타내는 각 영화를 반복 하는 For Each 루프가 포함 되어 있습니다. F5 키를 눌러 응용 프로그램을 실행 하는 경우 그림 11의 웹 페이지가 표시 됩니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image21.png)

**그림 11**: 인덱스 뷰 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image22.png))

## <a name="creating-new-database-records"></a>새 데이터베이스 레코드 만들기

이전 섹션에서 만든 인덱스 뷰에는 새 데이터베이스 레코드를 만들기 위한 링크가 포함 되어 있습니다. 계속 해 서 논리를 구현 하 고 새 동영상 데이터베이스 레코드를 만드는 데 필요한 뷰를 만듭니다.

Home 컨트롤러는 Create () 라는 두 개의 메서드를 포함 합니다. 첫 번째 Create () 메서드에는 매개 변수가 없습니다. Create () 메서드의이 오버 로드는 새 동영상 데이터베이스 레코드를 만들기 위한 HTML 양식을 표시 하는 데 사용 됩니다.

두 번째 Create () 메서드에는 FormCollection 매개 변수가 있습니다. Create () 메서드의이 오버 로드는 새 동영상을 만들기 위한 HTML 양식이 서버에 게시 될 때 호출 됩니다. 이 두 번째 Create () 메서드에는 HTTP Post 작업을 수행 하지 않는 한 메서드가 호출 되는 것을 방지 하는 AcceptVerbs 특성이 있습니다.

이 두 번째 Create () 메서드는 목록 4의 업데이트 된 HomeController 클래스에서 수정 되었습니다. 새 버전의 Create () 메서드는 영화 매개 변수를 허용 하 고 영화 데이터베이스 테이블에 새 동영상을 삽입 하기 위한 논리를 포함 합니다.

> [!NOTE] 
> 
> Bind 특성을 확인 합니다. Movie Id 속성을 HTML 양식에서 업데이트 하지 않으려면이 속성을 명시적으로 제외 해야 합니다.

**목록 4 – Controllers\HomeController.vb (수정 된 Create 메서드)**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample4.vb)]

Visual Studio를 사용 하면 새 영화 데이터베이스 레코드를 만들기 위한 양식을 쉽게 만들 수 있습니다 (그림 12 참조). 다음 단계를 수행하십시오.

1. 코드 편집기에서 Create () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **뷰 추가**를 선택 합니다.
2. **강력한 형식의 뷰 만들기** 확인란을 선택 했는지 확인 합니다.
3. **콘텐츠 보기** 드롭다운 목록에서 값 *만들기*를 선택 합니다.
4. **데이터 클래스 보기** 드롭다운 목록에서 *MovieApp*값을 선택 합니다.
5. **추가** 단추를 클릭 하 여 새 보기를 만듭니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image23.png)

**그림 12**: Create view 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image24.png))

Visual Studio는 목록 5에서 뷰를 자동으로 생성 합니다. 이 보기에는 Movie 클래스의 각 속성에 해당 하는 필드를 포함 하는 HTML 폼이 포함 되어 있습니다.

**목록 5 – Views\Home\Create.aspx**

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample5.aspx)]

> [!NOTE] 
> 
> 뷰 추가 대화 상자에서 생성 된 HTML 양식에서 Id 폼 필드가 생성 됩니다. Id 열은 Id 열 이므로이 양식 필드는 필요 하지 않으므로 안전 하 게 제거할 수 있습니다.

만들기 뷰를 추가한 후에는 데이터베이스에 새 영화 레코드를 추가할 수 있습니다. F5 키를 눌러 응용 프로그램을 실행 하 고 새로 만들기 링크를 클릭 하 여 그림 13의 양식을 표시 합니다. 양식을 완료 하 고 전송 하면 새 영화 데이터베이스 레코드가 만들어집니다.

폼 유효성 검사를 자동으로 가져옵니다. 동영상의 릴리스 날짜를 입력 하지 않거나 잘못 된 릴리스 날짜를 입력 한 경우 양식이 다시 표시 되 고 릴리스 날짜 필드가 강조 표시 됩니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image25.png)

**그림 13**: 새 동영상 데이터베이스 레코드 만들기 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image26.png))

## <a name="editing-existing-database-records"></a>기존 데이터베이스 레코드 편집

이전 섹션에서는 새 데이터베이스 레코드를 나열 하 고 만드는 방법에 대해 설명 했습니다. 이 마지막 섹션에서는 기존 데이터베이스 레코드를 편집 하는 방법을 설명 합니다.

먼저 편집 폼을 생성 해야 합니다. 이 단계는 Visual Studio에서 자동으로 편집 양식을 생성 하기 때문에 간단 합니다. Visual Studio 코드 편집기에서 HomeController 클래스를 열고 다음 단계를 수행 합니다.

1. 코드 편집기에서 Edit () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **뷰 추가** 를 선택 합니다 (그림 14 참조).
2. **강력한 형식의 뷰 만들기**확인란을 선택 합니다.
3. **콘텐츠 보기** 드롭다운 목록에서 값 *편집*을 선택 합니다.
4. **데이터 클래스 보기** 드롭다운 목록에서 *MovieApp*값을 선택 합니다.
5. **추가** 단추를 클릭 하 여 새 보기를 만듭니다.

이러한 단계를 완료 하면 Views\Home 폴더에 Edit .aspx 이라는 새 뷰가 추가 됩니다. 이 보기에는 영화 레코드를 편집 하는 HTML 양식이 포함 됩니다.

[새 프로젝트 대화 상자 ![](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image27.png)

**그림 14**: 편집 뷰 추가 ([전체 크기 이미지를 보려면 클릭](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/_static/image28.png))

> [!NOTE] 
> 
> 편집 뷰는 Movie Id 속성에 해당 하는 HTML 양식 필드를 포함 합니다. Id 속성의 값을 편집 하는 사람이 필요 하지 않기 때문에이 양식 필드를 제거 해야 합니다.

마지막으로, 데이터베이스 레코드 편집을 지원 하도록 홈 컨트롤러를 수정 해야 합니다. 업데이트 된 HomeController 클래스는 목록 6에 포함 되어 있습니다.

**목록 6 – Controllers\HomeController.vb (Edit 메서드)**

[!code-vb[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb/samples/sample6.vb)]

목록 6에서 Edit () 메서드의 오버 로드에 추가 논리를 추가 했습니다. 첫 번째 Edit () 메서드는 메서드에 전달 된 Id 매개 변수에 해당 하는 movie 데이터베이스 레코드를 반환 합니다. 두 번째 오버 로드는 데이터베이스의 영화 레코드에 대 한 업데이트를 수행 합니다.

원본 영화를 검색 한 다음 ApplyPropertyChanges ()를 호출 하 여 데이터베이스의 기존 동영상을 업데이트 해야 합니다.

## <a name="summary"></a>요약

이 자습서의 목적은 ASP.NET MVC 응용 프로그램을 빌드하는 환경을 이해 하는 것입니다. ASP.NET MVC 웹 응용 프로그램을 빌드하는 것은 Active Server Pages 또는 ASP.NET 응용 프로그램을 빌드하는 것과 매우 비슷합니다.

이 자습서에서는 ASP.NET MVC 프레임 워크의 가장 기본적인 기능만 검사 했습니다. 이후 자습서에서는 컨트롤러, 컨트롤러 작업, 보기, 데이터 보기 및 HTML 도우미와 같은 항목을 자세히 살펴보겠습니다.

> [!div class="step-by-step"]
> [이전](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs.md)
