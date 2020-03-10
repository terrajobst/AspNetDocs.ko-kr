---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: 모델 추가 (VB) | Microsoft Docs
author: Rick-Anderson
description: 이 자습서에서는 Microsoft Visual Web Developer 2010 Express 서비스 팩 1 (...)을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다.
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e69d59aed4d74f08f1c653c4965b128c4dbe20ff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78434603"
---
# <a name="adding-a-model-vb"></a>모델 추가(VB)

[Rick Anderson](https://twitter.com/RickAndMSFT)

> 이 자습서에서는 Microsoft Visual Studio의 무료 버전인 Microsoft Visual Web Developer 2010 Express 서비스 팩 1을 사용 하 여 ASP.NET MVC 웹 응용 프로그램을 빌드하는 기본 사항을 학습 합니다. 시작 하기 전에 아래 나열 된 필수 구성 요소를 설치 했는지 확인 합니다. [웹 플랫폼 설치 관리자](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)링크를 클릭 하 여 모든 항목을 설치할 수 있습니다. 또는 다음 링크를 사용 하 여 필수 구성 요소를 개별적으로 설치할 수 있습니다.
> 
> - [Visual Studio Web Developer Express SP1 필수 구성 요소](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 도구 업데이트](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(런타임 + 도구 지원)
> 
> Visual Web Developer 2010 대신 Visual Studio 2010을 사용 하는 경우 [Visual studio 2010 필수 조건](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)링크를 클릭 하 여 필수 구성 요소를 설치 합니다.
> 
> VB.NET 소스 코드를 사용 하는 Visual Web Developer 프로젝트를이 항목과 함께 사용할 수 있습니다. [VB.NET 버전을 다운로드](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)합니다. 선호 C#하는 경우이 자습서의 [ C# 버전](../cs/adding-a-model.md) 으로 전환 합니다.

## <a name="adding-a-model"></a>모델 추가

이 섹션에서는 데이터베이스에서 동영상을 관리 하기 위한 몇 가지 클래스를 추가 합니다. 이러한 클래스는 ASP.NET MVC 응용 프로그램의 "모델" 부분이 됩니다.

이러한 모델 클래스를 정의 하 고 사용 하려면 Entity Framework 라는 .NET Framework 데이터 액세스 기술을 사용 합니다. Entity Framework (EF 라고도 함)는 *Code First*라는 개발 패러다임을 지원 합니다. Code First를 사용 하면 간단한 클래스를 작성 하 여 모델 개체를 만들 수 있습니다. 이러한 항목은 "일반-이전 CLR 개체"에서 POCO 클래스 라고도 합니다. 그런 다음 클래스에서 즉석에서 데이터베이스를 만들 수 있습니다. 이렇게 하면 매우 깔끔하고 빠른 개발 워크플로를 사용할 수 있습니다.

## <a name="adding-model-classes"></a>모델 클래스 추가

**솔루션 탐색기**에서 *모델* 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가**를 선택한 다음 **클래스**를 선택 합니다.

![](adding-a-model/_static/image1.png)

클래스 이름을 "Movie"로 합니다.

`Movie` 클래스에 다음 5 가지 속성을 추가 합니다.

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

`Movie` 클래스를 사용 하 여 데이터베이스의 영화를 나타냅니다. `Movie` 개체의 각 인스턴스는 데이터베이스 테이블의 행에 해당 하며 `Movie` 클래스의 각 속성은 테이블의 열에 매핑됩니다.

동일한 파일에서 다음 `MovieDBContext` 클래스를 추가 합니다.

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

`MovieDBContext` 클래스는 데이터베이스의 `Movie` 클래스 인스턴스 가져오기, 저장 및 업데이트를 처리 하는 Entity Framework movie 데이터베이스 컨텍스트를 나타냅니다. `MovieDBContext` Entity Framework에서 제공 하는 `DbContext` 기본 클래스에서 파생 됩니다. `DbContext` 및 `DbSet`에 대 한 자세한 내용은 [Entity Framework의 생산성 향상](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)을 참조 하세요.

`DbContext` 및 `DbSet`를 참조할 수 있도록 하려면 파일 맨 위에 다음 `imports` 문을 추가 해야 합니다.

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

전체 *동영상 .vb* 파일은 다음과 같습니다.

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>연결 문자열 만들기 및 SQL Server Compact 작업

만든 `MovieDBContext` 클래스는 데이터베이스에 연결 하 고 데이터베이스 레코드에 `Movie` 개체를 매핑하는 태스크를 처리 합니다. 한 가지 질문은 연결할 데이터베이스를 지정 하는 방법입니다. 응용 프로그램의 *web.config* 파일에 연결 정보를 추가 하 여이 작업을 수행 합니다.

응용 프로그램 루트 *web.config* 파일을 엽니다. *Views* 폴더에 있는 *web.config* 파일이 아닙니다. 아래 이미지에는 *web.config* 파일이 모두 표시 됩니다. red로 *원 된 web.config* 파일을 엽니다.

![](adding-a-model/_static/image2.png)

*Web.config 파일의* `<connectionStrings>` 요소에 다음 연결 문자열을 추가 합니다.

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

다음 예제에서는 새 연결 문자열이 추가 된 *web.config 파일의* 일부를 보여 줍니다.

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

이러한 소량의 코드와 XML은 동영상 데이터를 표시 하 고 데이터베이스에 저장 하기 위해 작성 해야 하는 모든 것입니다.

다음으로, 영화 데이터를 표시 하 고 사용자가 새 영화 목록을 만들 수 있도록 하는 새 `MoviesController` 클래스를 빌드합니다.

> [!div class="step-by-step"]
> [이전](adding-a-view.md)
> [다음](accessing-your-models-data-from-a-controller.md)
