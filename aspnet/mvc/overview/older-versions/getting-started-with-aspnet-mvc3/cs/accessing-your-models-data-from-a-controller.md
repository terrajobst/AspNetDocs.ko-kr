---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
title: 컨트롤러에서 모델의 데이터에 액세스 (C#) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 002ada5c-f114-47ab-a441-57dbdb728ea0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e9c7f24d426635760b613f570b85455ce71b3dc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78506027"
---
# <a name="accessing-your-models-data-from-a-controller-c"></a>컨트롤러에서 모델의 데이터에 액세스(C#)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > ASP.NET MVC 5와 Visual Studio 2013를 사용 하는이 자습서의 업데이트 된 버전 [을 사용할 수 있습니다.](../../../getting-started/introduction/getting-started.md) 더 안전 하 고 더 간단 하 고 더 많은 기능을 보여 줍니다.
> 
> 
> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.
> 
> 이 항목과 함께 사용할 수 있는 C# 소스 코드가 포함 된 Visual Web Developer 프로젝트를 사용할 수 있습니다. [버전을 C# 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. Visual Basic 선호 하는 경우이 자습서의 [Visual Basic 버전](../vb/intro-to-aspnet-mvc-3.md) 으로 전환 합니다.

이 섹션에서는 새 `MoviesController` 클래스를 만들고 영화 데이터를 검색 하 고 보기 템플릿을 사용 하 여 브라우저에 표시 하는 코드를 작성 합니다. 계속 하기 전에 응용 프로그램을 빌드해야 합니다.

*Controllers* 폴더를 마우스 오른쪽 단추로 클릭 하 고 새 `MoviesController` 컨트롤러를 만듭니다. 다음 옵션을 선택합니다.

- 컨트롤러 이름: **moviescontroller.cs**. 이것이 기본값입니다. )
- Template: **Entity Framework을 사용 하 여 읽기/쓰기 동작 및 뷰가 포함 된 컨트롤러**입니다.
- 모델 클래스: **movie (MvcMovie. 모델)** .
- 데이터 컨텍스트 클래스: **MovieDBContext (MvcMovie. 모델)** .
- 뷰: **Razor (CSHTML)** . 기본값은입니다.

[![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image2.png "AddScaffoldedMovieController")](accessing-your-models-data-from-a-controller/_static/image1.png)

**추가**를 클릭합니다. Visual Web Developer는 다음과 같은 파일 및 폴더를 만듭니다.

- 프로젝트의 *Controllers* 폴더에 있는 *MoviesController.cs* 파일입니다.
- 프로젝트의 *Views* 폴더에 있는 *동영상* 폴더입니다.
- 새 *Views\Movies* 폴더에서 *. cshtml, Delete cshtml, Details, Edit. cshtml*및 *인덱스* 를 만듭니다.

[![NewMovieControllerScreenShot](accessing-your-models-data-from-a-controller/_static/image4.png "NewMovieControllerScreenShot")](accessing-your-models-data-from-a-controller/_static/image3.png)

ASP.NET MVC 3 스 캐 폴딩 메커니즘은 자동으로 CRUD (만들기, 읽기, 업데이트 및 삭제) 작업 메서드와 뷰를 만듭니다. 이제 동영상 항목을 만들고, 나열 하 고, 편집 하 고, 삭제할 수 있는 완전히 작동 하는 웹 응용 프로그램이 있습니다.

응용 프로그램을 실행 하 고 브라우저의 주소 표시줄에 있는 URL에 */sourcea* 를 추가 하 여 `Movies` 컨트롤러를 찾습니다. 응용 프로그램이 *global.asax* 파일에 정의 된 기본 라우팅에 의존 하기 때문에 브라우저 요청 `http://localhost:xxxxx/Movies`는 `Movies` 컨트롤러의 기본 `Index` 작업 메서드로 라우팅됩니다. 즉, 브라우저 요청 `http://localhost:xxxxx/Movies`는 실제로 브라우저 요청 `http://localhost:xxxxx/Movies/Index`와 동일 합니다. 아직 추가 하지 않았기 때문에 빈 영화 목록이 생성 됩니다.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

### <a name="creating-a-movie"></a>동영상 만들기

**새로 만들기** 링크를 선택합니다. 동영상에 대 한 세부 정보를 입력 한 다음 **만들기** 단추를 클릭 합니다.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

[ **만들기** ] 단추를 클릭 하면 양식이 서버에 게시 되 고,이 경우 동영상 정보가 데이터베이스에 저장 됩니다. 그런 다음 목록에서 새로 만든 동영상을 볼 수 있는 */Clurl* 로 리디렉션됩니다.

[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png "IndexWhenHarryMet")](accessing-your-models-data-from-a-controller/_static/image7.png)

나머지 몇 개의 동영상 항목을 만듭니다. 모두 작동하는 **편집**, **세부 정보** 및 **삭제** 링크를 사용해 봅니다.

## <a name="examining-the-generated-code"></a>생성 된 코드 검사

*Controllers\MoviesController.cs* 파일을 열고 생성 된 `Index` 메서드를 검사 합니다. `Index` 메서드를 사용 하는 동영상 컨트롤러의 일부는 다음과 같습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

`MoviesController` 클래스의 다음 줄은 앞에서 설명한 대로 영화 데이터베이스 컨텍스트를 인스턴스화합니다. 동영상 데이터베이스 컨텍스트를 사용 하 여 영화를 쿼리, 편집 및 삭제할 수 있습니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

`Movies` 컨트롤러에 대 한 요청은 movie 데이터베이스의 `Movies` 테이블에 있는 모든 항목을 반환한 다음 결과를 `Index` 보기에 전달 합니다.

## <a name="strongly-typed-models-and-the-model-keyword"></a>강력한 형식의 모델 및 @model 키워드

이 자습서의 앞부분에서 컨트롤러가 `ViewBag` 개체를 사용 하 여 데이터 또는 개체를 뷰 템플릿에 전달 하는 방법을 살펴보았습니다. `ViewBag`은 뷰에 정보를 전달 하는 데 편리한 런타임에 바인딩되는 방법을 제공 하는 동적 개체입니다.

ASP.NET MVC는 또한 강력한 형식의 데이터 또는 개체를 뷰 템플릿에 전달 하는 기능을 제공 합니다. 강력 하 게 형식화 된이 접근 방식을 사용 하면 Visual Web Developer 편집기에서 코드 및 더 다양 한 IntelliSense의 컴파일 시간 검사를 더 효율적으로 수행할 수 있습니다. 이 방법을 `MoviesController` 클래스 및 인덱스를 사용 하 여 사용 합니다. *cshtml* 뷰 템플릿.

코드는 `Index` 동작 메서드에서 `View` 도우미 메서드를 호출할 때 [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) 개체를 만드는 방법을 확인 합니다. 그런 다음 코드는 컨트롤러에서 뷰로이 `Movies` 목록을 전달 합니다.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

뷰 템플릿 파일의 맨 위에 `@model` 문을 포함 하 여 뷰에 필요한 개체 유형을 지정할 수 있습니다. 동영상 컨트롤러를 만들 때 Visual Web Developer는 다음 `@model` 문을 *Index. cshtml* 파일의 맨 위에 자동으로 포함 합니다.

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

이 `@model` 지시어를 사용 하면 강력한 형식의 `Model` 개체를 사용 하 여 컨트롤러에서 뷰에 전달 된 동영상 목록에 액세스할 수 있습니다. 예를 들어, *인덱스인* 템플릿에서 코드는 강력한 형식의 `Model` 개체에 대해 `foreach` 문을 수행 하 여 동영상을 반복 합니다.

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml)]

`Model` 개체는 강력 하 게 형식화 되어 있기 때문에 (`IEnumerable<Movie>` 개체로) 루프의 각 `item` 개체는 `Movie`로 형식화 됩니다. 다른 이점 중 하나는 코드 편집기에서 코드 및 전체 IntelliSense 지원에 대 한 컴파일 시간 검사를 가져오는 것입니다.

[![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image10.png "ModelIntelliSense")](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>SQL Server Compact 사용

Entity Framework Code First 제공 된 데이터베이스 연결 문자열이 아직 존재 하지 않은 `Movies` 데이터베이스를 가리키고 있으므로 데이터베이스를 자동으로 만들 Code First. *앱\_데이터* 폴더를 확인 하 여 만들어졌는지 확인할 수 있습니다. *영화 .sdf* 파일이 표시 되지 않으면 **솔루션 탐색기** 도구 모음에서 **모든 파일 표시** 단추를 클릭 하 고 **새로 고침** 단추를 클릭 한 다음 *응용 프로그램\_데이터* 폴더를 확장 합니다.

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png "SDF_in_SolnExp")](accessing-your-models-data-from-a-controller/_static/image11.png)

*영화 .sdf* 를 두 번 클릭 하 여 **서버 탐색기**을 엽니다. 그런 다음 **테이블** 폴더를 확장 하 여 데이터베이스에서 만든 테이블을 확인 합니다.

> [!NOTE]
> *영화 .sdf*를 두 번 클릭할 때 오류가 발생 하면 [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)을 설치 했는지 확인 합니다. 소프트웨어에 대 한 링크는이 자습서 시리즈의 1 부에서 전제 조건 목록을 참조 하세요. 지금 릴리스를 설치 하는 경우에는 Visual Web Developer를 닫았다가 다시 열어야 합니다.

[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png "DB_explorer")](accessing-your-models-data-from-a-controller/_static/image13.png)

두 테이블은 `Movie` 엔터티 집합에 대 한 테이블과 `EdmMetadata` 테이블에 하나씩 있습니다. `EdmMetadata` 테이블은 Entity Framework에서 모델과 데이터베이스가 동기화 되지 않은 시기를 확인 하는 데 사용 됩니다.

`Movies` 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 데이터 표시** 를 선택 하 여 만든 데이터를 확인 합니다.

[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png "MoviesTable")](accessing-your-models-data-from-a-controller/_static/image15.png)

`Movies` 테이블을 마우스 오른쪽 단추로 클릭 하 고 **테이블 스키마 편집**을 선택 합니다.

[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png "EditTableSchema")](accessing-your-models-data-from-a-controller/_static/image17.png)

[![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image20.png "TableSchemaSM")](accessing-your-models-data-from-a-controller/_static/image19.png)

`Movies` 테이블의 스키마가 이전에 만든 `Movie` 클래스에 매핑되는 방식을 확인 합니다. Entity Framework Code First `Movie` 클래스에 따라이 스키마를 자동으로 만듭니다.

완료 되 면 연결을 닫습니다. 연결을 닫지 않은 경우 다음에 프로젝트를 실행할 때 오류가 발생할 수 있습니다.

[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image22.png "CloseConnection")](accessing-your-models-data-from-a-controller/_static/image21.png)

이제 데이터베이스 및 간단한 목록 페이지에서 콘텐츠를 표시할 수 있습니다. 다음 자습서에서는 스 캐 폴드 코드의 나머지 부분을 검토 하 고이 데이터베이스에서 영화를 검색할 수 있도록 하는 `SearchIndex` 메서드 및 `SearchIndex` 뷰를 추가 합니다.

> [!div class="step-by-step"]
> [이전](adding-a-model.md)
> [다음](examining-the-edit-methods-and-edit-view.md)
