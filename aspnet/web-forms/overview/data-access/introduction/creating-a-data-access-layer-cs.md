---
uid: web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
title: 데이터 액세스 계층 만들기 (C#) | Microsoft Docs
author: rick-anderson
description: 이 자습서에서는 처음부터 시작 하 여 형식화 된 데이터 집합을 사용 하 여 DAL (데이터 액세스 계층)을 만들어 데이터베이스의 정보에 액세스 합니다.
ms.author: riande
ms.date: 04/05/2010
ms.assetid: cfe2a6a0-1e56-4dc8-9537-c8ec76ba96a4
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 5aaf97dc8448dcb7b94ef2e4e23f34fd37ac4426
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74115323"
---
# <a name="creating-a-data-access-layer-c"></a>데이터 액세스 레이어 만들기(C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[PDF 다운로드](creating-a-data-access-layer-cs/_static/datatutorial01cs1.pdf)

> 이 자습서에서는 처음부터 시작 하 여 형식화 된 데이터 집합을 사용 하 여 DAL (데이터 액세스 계층)을 만들어 데이터베이스의 정보에 액세스 합니다.

## <a name="introduction"></a>소개

웹 개발자는 데이터 작업을 중심으로 노력 하 고 있습니다. 데이터를 저장 하는 데이터베이스, 데이터를 검색 및 수정 하는 코드, 데이터를 수집 하 고 요약 하는 웹 페이지를 만듭니다. 이 자습서는 ASP.NET 2.0에서 이러한 일반적인 패턴을 구현 하는 기술을 탐색 하는 긴 시리즈의 첫 번째 자습서입니다. 형식화 된 데이터 집합을 사용 하 여 DAL (데이터 액세스 계층), 사용자 지정 비즈니스 규칙을 적용 하는 BLL (비즈니스 논리 계층) 및 공통 페이지 레이아웃을 공유 하는 ASP.NET 페이지로 구성 된 프레젠테이션 계층을 사용 하 여 구성 된 [소프트웨어 아키텍처](http://en.wikipedia.org/wiki/Software_architecture) 를 만드는 과정을 시작 합니다. 이 백 엔드 기반이 배치 된 후에는 보고로 이동 하 여 웹 응용 프로그램에서 데이터를 표시 하 고, 요약 하 고, 수집 하 고, 유효성을 검사 하는 방법을 보여 줍니다. 이러한 자습서는 간결 하 게 만들어 프로세스를 시각적으로 안내 하는 다양 한 스크린 샷를 제공 하는 단계별 지침을 제공 합니다. 각 자습서는 및 Visual Basic C# 버전에서 사용할 수 있으며, 사용 되는 전체 코드의 다운로드를 포함 합니다. 이 첫 번째 자습서는 매우 긴 하지만 나머지는 훨씬 더 좋게 청크로 제공 됩니다.

이러한 자습서에서는 **응용 프로그램\_데이터** 디렉터리에 배치 된 Northwind 데이터베이스의 Microsoft SQL Server 2005 Express Edition 버전을 사용 합니다. 데이터베이스 파일 외에도 다른 데이터베이스 버전을 사용 하려는 경우에도 **응용 프로그램\_Data** 폴더에는 데이터베이스를 만들기 위한 SQL 스크립트가 포함 되어 있습니다. 원하는 경우 이러한 스크립트를 [Microsoft에서 직접 다운로드할](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en)수도 있습니다. 다른 SQL Server 버전의 Northwind 데이터베이스를 사용 하는 경우 응용 프로그램의 **web.config** 파일에서 **NORTHWNDConnectionString** 설정을 업데이트 해야 합니다. 웹 응용 프로그램은 Visual Studio 2005 Professional Edition을 파일 시스템 기반 웹 사이트 프로젝트로 사용 하 여 빌드 되었습니다. 그러나 모든 자습서는 visual Studio 2005, [Visual Web Developer](https://msdn.microsoft.com/vstudio/express/vwd/)의 무료 버전과 동일 하 게 작동 합니다.  
  
이 자습서에서는 처음부터 시작 하 여 DAL (데이터 액세스 계층)을 만든 다음 두 번째 자습서에서 BLL (비즈니스 논리 계층)을 만들고 세 번째 자습서에서 페이지 레이아웃 및 탐색에 대해 작업을 수행 합니다. 세 번째 자습서의 자습서는 처음 3 개에 배치 된 기반을 바탕으로 작성 됩니다. 이 첫 번째 자습서에 대해 많은 내용이 있으므로 Visual Studio를 실행 하 고 시작 해 보겠습니다.

## <a name="step-1-creating-a-web-project-and-connecting-to-the-database"></a>1 단계: 웹 프로젝트를 만들고 데이터베이스에 연결

DAL (데이터 액세스 계층)을 만들기 전에 먼저 웹 사이트를 만들고 데이터베이스를 설정 해야 합니다. 먼저 새 파일 시스템 기반 ASP.NET 웹 사이트를 만듭니다. 이를 위해 파일 메뉴로 이동 하 고 새 웹 사이트를 선택 하 여 새 웹 사이트 대화 상자를 표시 합니다. ASP.NET 웹 사이트 템플릿을 선택 하 고, 위치 드롭다운 목록을 파일 시스템으로 설정 하 고, 웹 사이트를 저장할 폴더를 선택 하 고, 언어를로 C#설정 합니다.

[새 파일 시스템 기반 웹 사이트 ![만들기](creating-a-data-access-layer-cs/_static/image2.png)](creating-a-data-access-layer-cs/_static/image1.png)

**그림 1**: 새 파일 시스템 기반 웹 사이트 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image3.png))

그러면 **default.aspx** ASP.NET 페이지와 **앱\_데이터** 폴더를 사용 하 여 새 웹 사이트를 만듭니다.

웹 사이트를 만든 후 다음 단계는 Visual Studio의 서버 탐색기에서 데이터베이스에 대 한 참조를 추가 하는 것입니다. 서버 탐색기에 데이터베이스를 추가 하 여 Visual Studio 내에서 테이블, 저장 프로시저, 뷰 등을 추가할 수 있습니다. 테이블 데이터를 보거나 쿼리 작성기를 통해 직접 또는 그래픽으로 직접 쿼리를 만들 수도 있습니다. 또한 DAL에 대해 형식화 된 데이터 집합을 작성 하는 경우 Visual Studio에서 형식화 된 데이터 집합을 생성 해야 하는 데이터베이스를 가리키도록 해야 합니다. 해당 시점에이 연결 정보를 제공할 수 있지만 Visual Studio는 서버 탐색기에 이미 등록 되어 있는 데이터베이스의 드롭다운 목록을 자동으로 채웁니다.

서버 탐색기에 Northwind 데이터베이스를 추가 하는 단계는 **응용 프로그램\_데이터** 폴더에서 SQL Server 2005 Express Edition 데이터베이스를 사용할지 아니면 대신 사용 하려는 Microsoft SQL Server 2000 또는 2005 데이터베이스 서버 설정이 있는지 여부에 따라 달라 집니다.

## <a name="using-a-database-in-the-app_data-folder"></a>앱\_데이터 폴더에 데이터베이스 사용

연결할 SQL Server 2000 또는 2005 데이터베이스 서버가 없거나 데이터베이스 서버에 데이터베이스를 추가 하지 않으려는 경우 다운로드 한 웹 사이트의 **App\_Data** 폴더 (northwnd.mdf)에 있는 SQL Server 2005 Express Edition 버전의 Northwind 데이터베이스를 사용할 수 있습니다 **. MDF**).

**앱\_데이터** 폴더에 배치 된 데이터베이스가 서버 탐색기에 자동으로 추가 됩니다. 컴퓨터에 SQL Server 2005 Express Edition 설치 되어 있다고 가정할 경우 이름이 NORTHWND.MDF 인 노드가 표시 되어야 합니다. MDF는 테이블, 뷰, 저장 프로시저 등을 확장 하 고 탐색할 수 있는 서버 탐색기입니다 (그림 2 참조).

**앱\_데이터** 폴더에는 Microsoft Access .mdb 파일이 포함 될 수도 있습니다 .이 파일은 해당 SQL Server와 마찬가지로 서버 탐색기에 자동으로 추가 됩니다 **.** SQL Server 옵션 중 하나를 사용 하지 않으려는 경우 항상 [Northwind 데이터베이스 파일의 Microsoft Access 버전을 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyID=C6661372-8DBE-422B-8676-C632D66C529C&amp;displaylang=EN) 하 여 **앱\_데이터** 디렉터리에 놓을 수 있습니다. 그러나 Access 데이터베이스는 SQL Server 처럼 기능이 풍부 하지 않으며 웹 사이트 시나리오에서 사용 하도록 설계 되지 않았습니다. 또한 35 개 이상의 자습서 중 몇 가지는 Access에서 지원 하지 않는 특정 데이터베이스 수준 기능을 활용 합니다.

## <a name="connecting-to-the-database-in-a-microsoft-sql-server-2000-or-2005-database-server"></a>Microsoft SQL Server 2000 또는 2005 데이터베이스 서버의 데이터베이스에 연결

또는 데이터베이스 서버에 설치 된 Northwind 데이터베이스에 연결할 수 있습니다. 데이터베이스 서버에 Northwind 데이터베이스가 아직 설치 되어 있지 않은 경우에는 먼저이 자습서의 다운로드에 포함 된 설치 스크립트를 실행 하거나 Microsoft 웹 사이트에서 직접 [SQL Server 2000 버전의 northwind 및 설치 스크립트를 다운로드](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en) 하 여 데이터베이스 서버에 추가 해야 합니다.

데이터베이스를 설치한 후에는 Visual Studio의 서버 탐색기로 이동 하 여 데이터 연결 노드를 마우스 오른쪽 단추로 클릭 하 고 연결 추가를 선택 합니다. 서버 탐색기 표시 되지 않으면 보기/서버 탐색기으로 이동 하거나 Ctrl + Alt + S를 누릅니다. 연결 추가 대화 상자가 표시 됩니다. 여기에서 연결할 서버, 인증 정보 및 데이터베이스 이름을 지정할 수 있습니다. 데이터베이스 연결 정보를 성공적으로 구성 하 고 확인 단추를 클릭 하면 데이터베이스는 데이터 연결 노드 아래에 노드로 추가 됩니다. 데이터베이스 노드를 확장 하 여 테이블, 뷰, 저장 프로시저 등을 탐색할 수 있습니다.

![데이터베이스 서버의 Northwind 데이터베이스에 대 한 연결 추가](creating-a-data-access-layer-cs/_static/image4.png)

**그림 2**: 데이터베이스 서버의 Northwind 데이터베이스에 대 한 연결 추가

## <a name="step-2-creating-the-data-access-layer"></a>2 단계: 데이터 액세스 계층 만들기

데이터를 사용 하 여 작업 하는 경우 데이터 관련 논리를 프레젠테이션 계층에 직접 포함 합니다. 웹 응용 프로그램에서는 ASP.NET 페이지가 프레젠테이션 계층을 구성 합니다. 이는 ASP.NET 페이지의 코드 부분에서 ADO.NET 코드를 작성 하거나 태그 부분에서 SqlDataSource 컨트롤을 사용 하는 형식을 사용할 수 있습니다. 두 경우 모두이 방법은 데이터 액세스 논리를 프레젠테이션 계층에 긴밀 하 게 결합. 그러나 권장 되는 방법은 프레젠테이션 계층에서 데이터 액세스 논리를 분리 하는 것입니다. 이 별도의 계층은 데이터 액세스 계층 이라고 하 고, 간단 하 게 DAL 하 고, 일반적으로 별도의 클래스 라이브러리 프로젝트로 구현 됩니다. 이 계층화 된 아키텍처의 이점은 잘 문서화 되어 있습니다 (이러한 이점에 대 한 자세한 내용은이 자습서의 끝부분에 있는 "추가 정보" 섹션 참조) .이 시리즈에서 수행할 방법입니다.

데이터베이스에 대 한 연결 만들기, **SELECT**, **INSERT**, **UPDATE**및 **DELETE** 명령 실행 등 기본 데이터 원본에 해당 하는 모든 코드는 DAL에 배치 해야 합니다. 프레젠테이션 계층은 이러한 데이터 액세스 코드에 대 한 참조를 포함 하지 않아야 합니다. 대신 모든 데이터 요청에 대해 DAL을 호출 해야 합니다. 데이터 액세스 계층은 일반적으로 기본 데이터베이스 데이터에 액세스 하기 위한 메서드를 포함 합니다. 예를 들어 Northwind 데이터베이스에는 판매 제품과 해당 제품이 속한 범주를 기록 하는 **제품** 및 **범주** 테이블이 있습니다. DAL에는 다음과 같은 메서드가 있습니다.

- **Getcategories ()** -모든 범주에 대 한 정보를 반환 합니다.
- **Getproducts ()** -모든 제품에 대 한 정보를 반환 합니다.
- **GetProductsByCategoryID (*categoryID*)** -지정 된 범주에 속하는 모든 제품을 반환 합니다.
- 특정 제품에 대 한 정보를 반환 하는 **Getproductid byproductid (*productid*)**

이러한 메서드는 호출 되 면 데이터베이스에 연결 되 고, 적절 한 쿼리를 실행 하 고, 결과를 반환 합니다. 이러한 결과를 반환 하는 방법은 중요 합니다. 이러한 메서드는 단순히 데이터베이스 쿼리로 채워진 데이터 집합 또는 DataReader를 반환할 수 있지만, *강력한 형식의 개체*를 사용 하 여 이러한 결과를 반환 해야 합니다. 강력한 형식의 개체는 스키마가 컴파일 시간에 정의 된 엄격 반면, 느슨하게 형식화 된 개체는 런타임이 될 때까지 알 수 없는 스키마가 있는 개체입니다.

예를 들어 DataReader와 데이터 집합 (기본적으로)은 스키마가 해당 스키마를 채우는 데 사용 되는 데이터베이스 쿼리에서 반환 된 열에 의해 정의 되므로 느슨하게 형식화 된 개체입니다. 느슨하게 형식화 된 DataTable에서 특정 열에 액세스 하려면 Datatable과 같은 구문을 사용 해야 합니다.  <strong>행 [<em>index</em>] ["<em>columnName</em>"]</strong>. 이 예에서 DataTable의 느슨한 입력은 문자열 또는 서 수 인덱스를 사용 하 여 열 이름에 액세스 해야 한다는 사실에 의해 제공 됩니다. 반면 강력한 형식의 DataTable은 각 열을 속성으로 구현 하 여 다음과 같은 코드를 생성 합니다.  <strong><em>datatable</em>. 행 [<em>index</em>]. *columnName</strong>* .

강력한 형식의 개체를 반환 하기 위해 개발자는 고유한 사용자 지정 비즈니스 개체를 만들거나 형식화 된 데이터 집합을 사용할 수 있습니다. 비즈니스 개체는 개발자가 일반적으로 비즈니스 개체가 나타내는 기본 데이터베이스 테이블의 열을 반영 하는 클래스로 구현 됩니다. 형식화 된 데이터 집합은 데이터베이스 스키마에 따라 Visual Studio에서 생성 하는 클래스로,이 스키마에 따라 해당 멤버를 강력 하 게 형식화 합니다. 형식화 된 데이터 집합 자체는 ADO.NET DataSet, DataTable 및 DataRow 클래스를 확장 하는 클래스로 구성 됩니다. 강력한 형식의 Datatable 외에도, 이제 형식화 된 데이터 집합에는 데이터 집합의 Datatable를 채우고 Datatable 내의 수정 내용을 데이터베이스에 다시 전파 하는 메서드를 사용 하는 Tableadapter가 포함 됩니다.

> [!NOTE]
> 형식화 된 데이터 집합 및 사용자 지정 비즈니스 개체 사용의 장점과 단점에 대 한 자세한 내용은 [데이터 계층 구성 요소 디자인 및 계층을 통해 데이터 전달](https://msdn.microsoft.com/library/ms978496.aspx)을 참조 하세요.

이러한 자습서의 아키텍처에 대해 강력한 형식의 데이터 집합을 사용 합니다. 그림 3에서는 형식화 된 데이터 집합을 사용 하는 응용 프로그램의 다양 한 계층 간 워크플로를 보여 줍니다.

[모든 데이터 액세스 코드 ![DAL에 Relegated](creating-a-data-access-layer-cs/_static/image6.png)](creating-a-data-access-layer-cs/_static/image5.png)

**그림 3**: 모든 데이터 액세스 코드가 DAL에 Relegated ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image7.png))

## <a name="creating-a-typed-dataset-and-table-adapter"></a>형식화 된 데이터 집합 및 테이블 어댑터 만들기

DAL을 만들기 시작 하려면 먼저 프로젝트에 형식화 된 데이터 집합을 추가 합니다. 이를 수행 하려면 솔루션 탐색기에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭 하 고 새 항목 추가를 선택 합니다. 템플릿 목록에서 데이터 집합 옵션을 선택 하 고 이름을 **Northwind .xsd**로 표시 합니다.

[프로젝트에 새 데이터 집합을 추가 ![선택 합니다.](creating-a-data-access-layer-cs/_static/image9.png)](creating-a-data-access-layer-cs/_static/image8.png)

**그림 4**: 프로젝트에 새 데이터 집합을 추가 하도록 선택 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image10.png))

추가를 클릭 한 후 **응용 프로그램\_코드** 폴더에 데이터 집합을 추가 하 라는 메시지가 표시 되 면 예를 선택 합니다. 그러면 형식화 된 데이터 집합에 대 한 디자이너가 표시 되 고 TableAdapter 구성 마법사가 시작 되어 형식화 된 데이터 집합에 첫 번째 TableAdapter를 추가할 수 있습니다.

형식화 된 데이터 집합은 강력한 형식의 데이터 컬렉션으로 사용 됩니다. 강력한 형식의 DataTable 인스턴스로 구성 되며, 각각은 강력한 형식의 DataRow 인스턴스로 구성 됩니다. 이 자습서 시리즈에서 작업 해야 하는 기본 데이터베이스 테이블 각각에 대해 강력한 형식의 DataTable을 만듭니다. **Products** 테이블에 대해 DataTable을 만드는 것부터 시작 해 보겠습니다.

강력한 형식의 Datatable는 기본 데이터베이스 테이블에서 데이터에 액세스 하는 방법에 대 한 정보를 포함 하지 않습니다. 데이터를 검색 하 여 DataTable을 채울 수 있도록 데이터 액세스 계층으로 작동 하는 TableAdapter 클래스를 사용 합니다. **Products** DataTable의 경우, TableAdapter는 **getproducts ()** , **Getproducts bycategoryid (*categoryid*)** 등의 메서드를 포함 하며,이는 프레젠테이션 계층에서 호출 됩니다. DataTable의 역할은 계층 간에 데이터를 전달 하는 데 사용 되는 강력한 형식의 개체 역할을 수행 하는 것입니다.

TableAdapter 구성 마법사는 작업할 데이터베이스를 선택 하 라는 메시지를 표시 하기 시작 합니다. 드롭다운 목록에 서버 탐색기의 해당 데이터베이스가 표시 됩니다. 서버 탐색기에 Northwind 데이터베이스를 추가 하지 않은 경우 새 연결 단추를 클릭 하 여이 작업을 수행할 수 있습니다.

[드롭다운 목록에서 Northwind 데이터베이스를 선택 ![](creating-a-data-access-layer-cs/_static/image12.png)](creating-a-data-access-layer-cs/_static/image11.png)

**그림 5**: 드롭다운 목록에서 Northwind 데이터베이스 선택 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image13.png))

데이터베이스를 선택 하 고 다음을 클릭 한 후에는 **web.config 파일에** 연결 문자열을 저장할지 여부를 묻는 메시지가 표시 됩니다. 연결 문자열을 저장 하면 TableAdapter 클래스에 하드 코딩 되지 않으므로 연결 문자열 정보가 나중에 변경 되는 경우 작업이 간단해 집니다. 구성 파일에 연결 문자열을 저장 하도록 [선택](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx) 하는 경우 **&lt;connectionStrings&gt;** 섹션에 배치 됩니다 .이 섹션은 나중에 IIS GUI 관리 도구 내의 새 ASP.NET 2.0 속성 페이지를 통해 수정 하거나 나중에 수정할 수 있습니다 .이는 관리자에 게 보다 적합 합니다.

[Web.config에 연결 문자열을 저장 ![](creating-a-data-access-layer-cs/_static/image15.png)](creating-a-data-access-layer-cs/_static/image14.png)

**그림 6**: **Web.config** 에 연결 문자열 저장 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image16.png))

다음으로 강력한 형식의 데이터 집합을 채울 때 첫 번째 강력한 형식의 DataTable에 대 한 스키마를 정의 하 고 TableAdapter에서 사용할 첫 번째 메서드를 제공 해야 합니다. 이러한 두 단계는 DataTable에 반영 하려는 테이블의 열을 반환 하는 쿼리를 만들어 동시에 수행 됩니다. 마법사의 끝 부분에서이 쿼리에 메서드 이름을 지정 합니다. 이를 완료 한 후에는 프레젠테이션 계층에서이 메서드를 호출할 수 있습니다. 메서드는 정의 된 쿼리를 실행 하 고 강력한 형식의 DataTable을 채웁니다.

SQL 쿼리 정의를 시작 하려면 먼저 TableAdapter에서 쿼리를 실행 하는 방법을 지정 해야 합니다. 임시 SQL 문을 사용 하거나, 새 저장 프로시저를 만들거나, 기존 저장 프로시저를 사용할 수 있습니다. 이러한 자습서에서는 임시 SQL 문을 사용 합니다. 저장 프로시저 [를 사용](http://briannoyes.net/)하는 예는 [Visual Studio 2005 데이터 집합 디자이너를 사용 하 여 데이터 액세스 계층 작성](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner) 문서를 참조 하세요.

[임시 SQL 문을 사용 하 여 데이터를 쿼리 ![](creating-a-data-access-layer-cs/_static/image18.png)](creating-a-data-access-layer-cs/_static/image17.png)

**그림 7**: 임시 SQL 문을 사용 하 여 데이터 쿼리 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image19.png))

이 시점에서 SQL 쿼리를 직접 입력할 수 있습니다. TableAdapter에서 첫 번째 메서드를 만들 때 일반적으로 쿼리에서 해당 DataTable에 표시 되어야 하는 열을 반환 하도록 하려고 합니다. **Products** 테이블의 모든 열과 모든 행을 반환 하는 쿼리를 만들어이 작업을 수행할 수 있습니다.

[텍스트 상자에 SQL 쿼리를 입력 ![.](creating-a-data-access-layer-cs/_static/image21.png)](creating-a-data-access-layer-cs/_static/image20.png)

**그림 8**: 텍스트 상자에 SQL 쿼리 입력 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image22.png))

또는 그림 9와 같이 쿼리 작성기 사용 하 여 쿼리를 그래픽으로 생성 합니다.

[쿼리 편집기를 통해 쿼리를 그래픽으로 만들 ![](creating-a-data-access-layer-cs/_static/image24.png)](creating-a-data-access-layer-cs/_static/image23.png)

**그림 9**: 쿼리 편집기를 통해 그래픽으로 쿼리 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image25.png))

쿼리를 만든 후 다음 화면으로 이동 하기 전에 고급 옵션 단추를 클릭 합니다. 웹 사이트 프로젝트에서 "Insert, Update 및 Delete 문 생성"은 기본적으로 선택 되어 있는 유일한 고급 옵션입니다. 클래스 라이브러리나 Windows 프로젝트에서이 마법사를 실행 하는 경우 "낙관적 동시성 사용" 옵션도 선택 됩니다. 지금은 "낙관적 동시성 사용" 옵션을 선택 하지 않은 상태로 둡니다. 이후 자습서에서 낙관적 동시성을 살펴보겠습니다.

[Insert, Update 및 Delete 문 생성 옵션만 선택 ![.](creating-a-data-access-layer-cs/_static/image27.png)](creating-a-data-access-layer-cs/_static/image26.png)

**그림 10**: Insert, Update 및 Delete 문 생성 옵션만 선택 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image28.png))

고급 옵션을 확인 한 후 다음을 클릭 하 여 최종 화면으로 이동 합니다. TableAdapter에 추가할 메서드를 선택 하 라는 메시지가 표시 됩니다. 데이터를 채우는 데는 다음과 같은 두 가지 패턴이 있습니다.

- 이 접근 방식을 사용 하 여 **datatable을 채웁니다** .이 메서드는 datatable을 매개 변수로 사용 하 고 쿼리 결과에 따라 채웁니다. 예를 들어 ADO.NET DataAdapter 클래스는 **Fill ()** 메서드를 사용 하 여이 패턴을 구현 합니다.
- 이 접근 방식을 사용 하 여 **datatable을 반환** 합니다. 메서드는 datatable을 만들어 채운 다음 메서드 반환 값으로 반환 합니다.

TableAdapter에서 이러한 패턴 중 하나 또는 둘 모두를 구현할 수 있습니다. 여기에 제공 된 메서드의 이름을 바꿀 수도 있습니다. 이러한 자습서 전체에서 후자의 패턴을 사용 하는 경우에도 두 확인란을 모두 선택 된 상태로 둡니다. 또한 대신 generic **GetData** 메서드 이름을 **getproducts**로 변경 하겠습니다.

이 확인란을 선택 하면 "GenerateDBDirectMethods" 라는 마지막 확인란이 TableAdapter에 대해 **Insert ()** , **Update (** ) 및 **Delete ()** 메서드를 만듭니다. 이 옵션을 선택 하지 않은 상태로 두면 형식화 된 데이터 집합, DataTable, 단일 DataRow 또는 Datarow의 배열을 사용 하는 TableAdapter의 유일한 **Update ()** 메서드를 통해 모든 업데이트를 수행 해야 합니다. (그림 9의 고급 속성에서 "Insert, Update 및 Delete 문 생성" 옵션을 선택 취소 한 경우이 확인란의 설정은 적용 되지 않습니다.) 이 확인란을 선택 해 둡니다.

[메서드 이름을 GetData에서 GetProducts로 변경 ![](creating-a-data-access-layer-cs/_static/image30.png)](creating-a-data-access-layer-cs/_static/image29.png)

**그림 11**: 메서드 이름을 **GetData** 에서 **getproducts** 로 변경 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image31.png))

마침을 클릭 하 여 마법사를 완료 합니다. 마법사를 닫으면 방금 만든 DataTable을 보여 주는 데이터 집합 디자이너로 돌아갑니다. Products DataTable (**ProductID**, **ProductName**등)의 열 목록과 **Products** **stableadapter** (**Fill ()** 및 **getproducts ()** 의 메서드를 볼 수 있습니다.

[Products DataTable 및 Products Stableadapter가 형식화 된 데이터 집합에 추가 ![](creating-a-data-access-layer-cs/_static/image33.png)](creating-a-data-access-layer-cs/_static/image32.png)

**그림 12**: **Products** DataTable 및 Products **Stableadapter** 가 형식화 된 데이터 집합에 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image34.png)).

이 시점에서 **Getproducts ()** 메서드를 사용 하 여 단일 DataTable (NorthwindTableAdapters) 및 강력한 형식의 DataAdapter**클래스 (** **stableadapter**)를 포함 하는 형식화 된 데이터 집합이 있습니다. 이러한 개체를 사용 하 여 코드에서와 같은 모든 제품 목록에 액세스할 수 있습니다.

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample1.html)]

이 코드는 데이터 액세스 관련 코드를 하나 이상 작성 하지 않아도 됩니다. ADO.NET 클래스를 인스턴스화할 필요가 없습니다. 연결 문자열, SQL 쿼리 또는 저장 프로시저를 참조할 필요가 없습니다. 대신 TableAdapter는 낮은 수준의 데이터 액세스 코드를 제공 합니다.

이 예제에서 사용 되는 각 개체는 강력 하 게 형식화 되어 있으므로 Visual Studio에서 IntelliSense 및 컴파일 시간 형식 검사를 제공할 수 있습니다. TableAdapter에서 반환 하는 모든 Datatable은 GridView, DetailsView, DropDownList, CheckBoxList 등과 같은 ASP.NET 데이터 웹 컨트롤에 바인딩될 수 있습니다. 다음 예제에서는 **Getproducts ()** 메서드에 의해 반환 된 DataTable을 **페이지\_Load** 이벤트 처리기에서 scant 세 줄의 코드를 GridView에 바인딩하는 방법을 보여 줍니다.

AllProducts .aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample2.aspx)]

AllProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample3.cs)]

[제품 목록이 GridView에 표시 ![](creating-a-data-access-layer-cs/_static/image36.png)](creating-a-data-access-layer-cs/_static/image35.png)

**그림 13**: 제품 목록이 GridView에 표시 됨 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image37.png))

이 예제에서는 ASP.NET 페이지의 **페이지\_Load** 이벤트 처리기에서 3 줄의 코드를 작성 해야 하지만, 이후 자습서에서는 ObjectDataSource를 사용 하 여 DAL에서 데이터를 선언적으로 검색 하는 방법을 살펴보겠습니다. ObjectDataSource를 사용 하면 코드를 작성할 필요가 없으며 페이징 및 정렬 지원도 지원 됩니다.

## <a name="step-3-adding-parameterized-methods-to-the-data-access-layer"></a>3 단계: 데이터 액세스 계층에 매개 변수가 있는 메서드 추가

이제 제품 **Stableadapter** 클래스에는 데이터베이스의 모든 제품을 반환 하는 **getproducts ()** 메서드가 하나 있습니다. 모든 제품을 사용할 수 있는 것은 매우 유용 하지만 특정 제품 또는 특정 범주에 속하는 모든 제품에 대 한 정보를 검색 하려는 경우가 있습니다. 데이터 액세스 계층에 이러한 기능을 추가 하려면 매개 변수가 있는 메서드를 TableAdapter에 추가할 수 있습니다.

**GetProductsByCategoryID (*categoryID*)** 메서드를 추가 해 보겠습니다. DAL에 새 메서드를 추가 하려면 데이터 집합 디자이너로 돌아가서, **제품 Stableadapter** 섹션을 마우스 오른쪽 단추로 클릭 하 고 쿼리 추가를 선택 합니다.

![TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 쿼리 추가를 선택 합니다.](creating-a-data-access-layer-cs/_static/image38.png)

**그림 14**: TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 쿼리 추가를 선택 합니다.

먼저 임시 SQL 문이나 기존 또는 기존 저장 프로시저를 사용 하 여 데이터베이스에 액세스할 지 여부를 묻는 메시지가 표시 됩니다. 임시 SQL 문을 다시 사용 하도록 선택 합니다. 다음으로, 사용 하고자 하는 SQL 쿼리 유형을 묻는 메시지가 표시 됩니다. 지정 된 범주에 속하는 모든 제품을 반환 하려고 하기 때문에 행을 반환 하는 **SELECT** 문을 작성 하려고 합니다.

[행을 반환 하는 SELECT 문을 만들도록 선택할 ![](creating-a-data-access-layer-cs/_static/image40.png)](creating-a-data-access-layer-cs/_static/image39.png)

**그림 15**: 행을 반환 하는 **SELECT** 문 만들기 선택 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image41.png))

다음 단계는 데이터에 액세스 하는 데 사용 되는 SQL 쿼리를 정의 하는 것입니다. 특정 범주에 속하는 제품만 반환 하려고 하므로 <strong>Getproducts ()</strong>에서 동일한 <strong>SELECT</strong> 문을 사용 하지만 where <strong>CategoryID = @CategoryID</strong> <strong>where 절을</strong> 추가 합니다. <strong>@CategoryID</strong> 매개 변수는 만들려는 메서드에 해당 형식의 입력 매개 변수 (즉, nullable 정수)가 필요한 TableAdapter 마법사를 나타냅니다.

[지정 된 범주의 제품만 반환 하는 쿼리를 입력 ![.](creating-a-data-access-layer-cs/_static/image43.png)](creating-a-data-access-layer-cs/_static/image42.png)

**그림 16**: 지정 된 범주의 제품만 반환 하는 쿼리 입력 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image44.png))

마지막 단계에서는 사용할 데이터 액세스 패턴을 선택 하 고 생성 되는 방법의 이름을 사용자 지정할 수 있습니다. 채우기 패턴의 경우 이름을 <strong>Fillbycategoryid</strong> 로 변경 하 고 DataTable 반환 패턴 ( <strong>Get*X</strong>*  메서드) 반환에 대해 <strong>GetProductsByCategoryID</strong>를 사용 하겠습니다.

[![TableAdapter 메서드의 이름을 선택 합니다.](creating-a-data-access-layer-cs/_static/image46.png)](creating-a-data-access-layer-cs/_static/image45.png)

**그림 17**: TableAdapter 메서드의 이름 선택 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image47.png))

마법사를 완료 한 후에는 데이터 집합 디자이너에 새 TableAdapter 메서드가 포함 됩니다.

![이제 제품을 범주별로 쿼리할 수 있습니다.](creating-a-data-access-layer-cs/_static/image48.png)

**그림 18**: 이제 제품을 범주별로 쿼리할 수 있습니다.

동일한 기술을 사용 하 여 **Getproductid byproductid (*productID*)** 메서드를 추가 합니다.

이러한 매개 변수가 있는 쿼리는 데이터 집합 디자이너에서 직접 테스트할 수 있습니다. TableAdapter에서 메서드를 마우스 오른쪽 단추로 클릭 하 고 데이터 미리 보기를 선택 합니다. 그런 다음 매개 변수에 사용할 값을 입력 하 고 미리 보기를 클릭 합니다.

[음료 범주에 속한 제품이 표시 됩니다 ![](creating-a-data-access-layer-cs/_static/image50.png)](creating-a-data-access-layer-cs/_static/image49.png)

**그림 19**: 음료 범주에 속한 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image51.png)).

DAL에서 **GetProductsByCategoryID (*categoryID*)** 메서드를 사용 하 여 이제 지정 된 범주의 제품만 표시 하는 ASP.NET 페이지를 만들 수 있습니다. 다음 예에서는 CategoryID 범주에 있는 모든 제품을 보여 줍니다. 여기서는 **CategoryID** 가 1입니다.

음료 .asp

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample4.aspx)]

Beverages.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample5.cs)]

[음료 범주의 제품이 표시 ![](creating-a-data-access-layer-cs/_static/image53.png)](creating-a-data-access-layer-cs/_static/image52.png)

**그림 20**: 음료 범주의 제품이 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image54.png)).

## <a name="step-4-inserting-updating-and-deleting-data"></a>4 단계: 데이터 삽입, 업데이트 및 삭제

데이터를 삽입, 업데이트 및 삭제 하는 데 일반적으로 사용 되는 두 가지 패턴이 있습니다. 데이터베이스 직접 패턴을 호출 하는 첫 번째 패턴은 호출 될 때 단일 데이터베이스 레코드에 대해 작동 하는 데이터베이스에 **INSERT**, **UPDATE**또는 **DELETE** 명령을 실행 하는 메서드를 만드는 것입니다. 이러한 메서드는 일반적으로 삽입, 업데이트 또는 삭제할 값에 해당 하는 일련의 스칼라 값 (정수, 문자열, 부울, 날짜/시간 등)으로 전달 됩니다. 예를 들어 **Products** 테이블에 대해이 패턴을 사용 하면 delete 메서드가 정수 매개 변수를 사용 하 여 삭제할 레코드의 **ProductID** 를 표시 하는 반면 insert 메서드는 **ProductName**에 대 한 문자열, **UnitPrice**의 경우 decimal, **UnitsOnStock**에 대 한 정수를 사용 합니다.

[각 삽입, 업데이트 및 삭제 요청 ![데이터베이스에 즉시 전송 됩니다.](creating-a-data-access-layer-cs/_static/image56.png)](creating-a-data-access-layer-cs/_static/image55.png)

**그림 21**: 각 삽입, 업데이트 및 삭제 요청은 즉시 데이터베이스로 전송 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image57.png)).

일괄 처리 업데이트 패턴으로 참조 하는 다른 패턴은 하나의 메서드 호출에서 전체 데이터 집합, DataTable 또는 Datarow의 컬렉션을 업데이트 하는 것입니다. 개발자는이 패턴을 사용 하 여 DataTable에서 Datarow을 삭제, 삽입 및 수정한 다음 이러한 Datarow 또는 DataTable을 update 메서드로 전달 합니다. 그런 다음이 메서드는 전달 된 Datarow를 열거 하 고,이를 수정, 추가 또는 삭제 (DataRow의 [RowState 속성](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) 값을 통해) 하는지 여부를 확인 하 고 각 레코드에 대해 적절 한 데이터베이스 요청을 실행 합니다.

[Update 메서드를 호출할 때 모든 변경 내용이 데이터베이스와 동기화 ![](creating-a-data-access-layer-cs/_static/image59.png)](creating-a-data-access-layer-cs/_static/image58.png)

**그림 22**: 업데이트 메서드를 호출할 때 모든 변경 내용이 데이터베이스와 동기화 됨 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image60.png))

TableAdapter는 기본적으로 batch 업데이트 패턴을 사용 하지만 DB 직접 패턴도 지원 합니다. TableAdapter를 만들 때 고급 속성에서 "Insert, Update 및 Delete 문 생성" 옵션을 선택 했으므로 **제품 Stableadapter** 는 batch 업데이트 패턴을 구현 하는 **update ()** 메서드를 포함 합니다. 특히 TableAdapter는 형식화 된 데이터 집합, 강력한 형식의 DataTable 또는 하나 이상의 Datarow를 전달할 수 있는 **Update ()** 메서드를 포함 합니다. TableAdapter를 처음 만들 때 "GenerateDBDirectMethods" 확인란을 선택한 경우 DB 직접 패턴도 **Insert ()** , **Update ()** 및 **Delete ()** 메서드를 통해 구현 됩니다.

두 데이터 수정 패턴 모두 TableAdapter의 **InsertCommand**, **UpdateCommand**및 **DeleteCommand** 속성을 사용 하 여 데이터베이스에 대 한 **삽입**, **업데이트**및 **삭제** 명령을 실행 합니다. 데이터 집합 디자이너에서 TableAdapter를 클릭 한 다음 속성 창로 이동 하 여 **InsertCommand**, **UpdateCommand**및 **DeleteCommand** 속성을 검사 하 고 수정할 수 있습니다. (TableAdapter를 선택 했는지 확인 하 고, 제품의 드롭다운 목록에서 선택한 **제품의 Stableadapter** 개체가 속성 창.

[![TableAdapter에 InsertCommand, UpdateCommand 및 DeleteCommand 속성이 있습니다.](creating-a-data-access-layer-cs/_static/image62.png)](creating-a-data-access-layer-cs/_static/image61.png)

**그림 23**: TableAdapter에 **InsertCommand**, **UpdateCommand**및 **DeleteCommand** 속성이 있음 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image63.png))

이러한 데이터베이스 명령 속성을 검토 하거나 수정 하려면 **CommandText** 하위 속성을 클릭 합니다. 그러면 쿼리 작성기이 표시 됩니다.

[![쿼리 작성기에서 INSERT, UPDATE 및 DELETE 문을 구성 합니다.](creating-a-data-access-layer-cs/_static/image65.png)](creating-a-data-access-layer-cs/_static/image64.png)

**그림 24**: 쿼리 작성기에서 **삽입**, **업데이트**및 **삭제** 문 구성 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image66.png))

다음 코드 예제에서는 배치 업데이트 패턴을 사용 하 여 더 이상 지원 되지 않으며 재고 단위가 25 단위인 모든 제품의 가격을 두 배로 만드는 방법을 보여 줍니다.

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample6.cs)]

아래 코드에서는 DB direct 패턴을 사용 하 여 프로그래밍 방식으로 특정 제품을 삭제 한 다음 업데이트 하 고 새 항목을 추가 하는 방법을 보여 줍니다.

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample7.cs)]

## <a name="creating-custom-insert-update-and-delete-methods"></a>사용자 지정 삽입, 업데이트 및 삭제 메서드 만들기

DB direct 메서드에서 만든 **Insert ()** , **Update (** ) 및 **Delete ()** 메서드는 특히 많은 열이 있는 테이블의 경우 다소 복잡할 수 있습니다. IntelliSense의 도움 없이 이전 코드 예제를 살펴보면 **Update ()** 및 **Insert ()** 메서드의 각 입력 매개 변수에 매핑되는 **제품** 테이블 열이 명확 하지 않습니다. 단일 열 또는 두 개의 열만 업데이트 하거나 새로 삽입 된 레코드의 **id** (자동 증가) 필드 값을 반환 하는 사용자 지정 된 **Insert ()** 메서드를 원하는 경우도 있습니다.

이러한 사용자 지정 메서드를 만들려면 데이터 집합 디자이너로 돌아갑니다. TableAdapter를 마우스 오른쪽 단추로 클릭 하 고 쿼리 추가를 선택 하 여 TableAdapter 마법사로 돌아갑니다. 두 번째 화면에서 만들 쿼리 유형을 나타낼 수 있습니다. 새 제품을 추가한 다음 새로 추가 된 레코드의 **ProductID**값을 반환 하는 메서드를 만들어 보겠습니다. 따라서 **INSERT** 쿼리를 만들도록 옵트인 합니다.

[Products 테이블에 새 행을 추가 하는 메서드를 만드는 ![](creating-a-data-access-layer-cs/_static/image68.png)](creating-a-data-access-layer-cs/_static/image67.png)

**그림 25**: **Products** 테이블에 새 행을 추가 하는 메서드 만들기 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image69.png))

다음 화면에서 **InsertCommand**의 **CommandText** 가 표시 됩니다. 쿼리 끝에 **SELECT SCOPE\_identity ()** 를 추가 하 여이 쿼리를 보강 합니다. 그러면 동일한 범위의 **id** 열에 삽입 된 마지막 id 값이 반환 됩니다. ( **) 범위\_identity ()** 에 대 한 자세한 내용 및 [@@IDENTITY를 사용 하\_IDENTITY () 범위를 사용 ](http://weblogs.sqlteam.com/travisl/archive/2003/10/29/405.aspx)하려는 이유는 [기술 설명서](https://msdn.microsoft.com/library/ms190315.aspx) 를 참조 하십시오. **SELECT** 문을 추가 하기 전에 세미콜론을 사용 하 여 **INSERT** 문을 종료 했는지 확인 합니다.

[SCOPE_IDENTITY () 값을 반환 하도록 쿼리를 보강 ![](creating-a-data-access-layer-cs/_static/image71.png)](creating-a-data-access-layer-cs/_static/image70.png)

**그림 26**: **범위\_IDENTITY ()** 값을 반환 하도록 쿼리 보강 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image72.png))

마지막으로 새 메서드 이름을 **Insertproduct**로 합니다.

[새 메서드 이름을 InsertProduct로 설정 ![](creating-a-data-access-layer-cs/_static/image74.png)](creating-a-data-access-layer-cs/_static/image73.png)

**그림 27**: 새 메서드 이름을 **insertproduct** 로 설정 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image75.png))

데이터 집합 디자이너로 돌아가면 상품 **Stableadapter** 에 새 메서드인 **insertproduct**가 포함 되어 있는 것을 볼 수 있습니다. 이 새 메서드에 **Products** 테이블의 각 열에 대 한 매개 변수가 없는 경우에는 세미콜론으로 **INSERT** 문을 종료 하지 않아도 됩니다. **Insertproduct** 메서드를 구성 하 고 **INSERT** 및 **SELECT** 문을 세미콜론으로 구분 하는지 확인 합니다.

기본적으로 insert 메서드는 쿼리가 아닌 메서드를 실행 하 여 영향을 받는 행의 수를 반환 합니다. 그러나 **Insertproduct** 메서드는 영향을 받는 행 수가 아니라 쿼리에서 반환 된 값을 반환 하려고 합니다. 이를 수행 하려면 **Insertproduct** 메서드의 **Executemode** 속성을 **스칼라**로 조정 합니다.

[![ExecuteMode 속성을 스칼라로 변경 합니다.](creating-a-data-access-layer-cs/_static/image77.png)](creating-a-data-access-layer-cs/_static/image76.png)

**그림 28**: **Executemode** 속성을 **스칼라** 로 변경 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image78.png))

다음 코드에서는이 새 **Insertproduct** 메서드를 실행 하는 방법을 보여 줍니다.

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample8.cs)]

## <a name="step-5-completing-the-data-access-layer"></a>5 단계: 데이터 액세스 계층 완료

**Products** **stableststststststststststststststststststststststststststststststststststststststststststststststststststststststststststststststststable** TableAdapter의 초기 메서드인 **Getproducts ()** 를 확장 하 여 **범주** 및 **CompanyName** 열 값을 모두 포함할 수 있습니다. 그러면 이러한 새 열도 포함 하도록 강력한 형식의 DataTable이 업데이트 됩니다.

그러나 데이터 삽입, 업데이트 및 삭제에 대 한 TableAdapter의 메서드는이 초기 방법을 기반으로 하기 때문에 문제를 일으킬 수 있습니다. 다행히 삽입, 업데이트 및 삭제를 위한 자동 생성 된 메서드는 **SELECT** 절의 하위 쿼리에서 영향을 받지 않습니다. **조인** 대신 **범주** 와 **공급자** 에 대 한 쿼리를 하위 쿼리로 추가 하면 데이터를 수정 하기 위해 이러한 메서드를 다시 사용 하지 않아도 됩니다. Products **Stableadapter** 에서 **getproducts ()** 메서드를 마우스 오른쪽 단추로 클릭 하 고 구성을 선택 합니다. 그런 다음 다음과 같이 **SELECT** 절을 조정 합니다.

[!code-sql[Main](creating-a-data-access-layer-cs/samples/sample9.sql)]

[GetProducts () 메서드에 대 한 SELECT 문을 업데이트 ![](creating-a-data-access-layer-cs/_static/image80.png)](creating-a-data-access-layer-cs/_static/image79.png)

**그림 29**: **getproducts ()** 메서드에 대 한 **SELECT** 문 업데이트 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image81.png))

**Getproducts ()** 메서드를 업데이트 하 여이 새 쿼리를 사용 하면 DataTable에는 두 개의 새 열인 **범주** 및 **SupplierName**포함 됩니다.

![Products DataTable에는 두 개의 새 열이 있습니다.](creating-a-data-access-layer-cs/_static/image82.png)

**그림 30**: **Products** DataTable에 두 개의 새 열이 있습니다.

**GetProductsByCategoryID (*categoryID*)** 메서드에서 **SELECT** 절도 업데이트 합니다.

**Getproducts ()** 를 업데이트 하는 경우 **조인** 구문 사용을 **선택** 합니다. 데이터 집합 디자이너는 DB direct 패턴을 사용 하 여 데이터베이스 데이터를 삽입, 업데이트 및 삭제 하는 메서드를 자동 생성할 수 없습니다. 대신이 자습서의 앞부분에서 **Insertproduct** 메서드를 사용 하는 것 처럼 수동으로 만들어야 합니다. 또한 일괄 업데이트 패턴을 사용 하려면 **InsertCommand**, **UpdateCommand**및 **DeleteCommand** 속성 값을 수동으로 제공 해야 합니다.

## <a name="adding-the-remaining-tableadapters"></a>나머지 Tableadapter 추가

지금까지 단일 TableAdapter를 단일 데이터베이스 테이블에 대 한 작업 으로만 살펴보았습니다. 그러나 Northwind 데이터베이스에는 웹 응용 프로그램에서 사용 해야 하는 여러 관련 테이블이 포함 되어 있습니다. 형식화 된 데이터 집합에는 관련 된 여러 Datatable 포함 될 수 있습니다. 따라서 DAL을 완료 하려면 이러한 자습서에서 사용할 다른 테이블에 대 한 Datatable를 추가 해야 합니다. 형식화 된 데이터 집합에 새 TableAdapter를 추가 하려면 데이터 집합 디자이너를 열고 디자이너를 마우스 오른쪽 단추로 클릭 한 다음 추가/TableAdapter를 선택 합니다. 그러면 새 DataTable 및 TableAdapter가 생성 되 고이 자습서의 앞부분에서 설명한 마법사를 안내 합니다.

다음 쿼리를 사용 하 여 다음 Tableadapter 및 메서드를 만드는 데 몇 분 정도 걸립니다. 상품 **Stableadapter** 의 쿼리에는 각 제품의 범주 및 공급자 이름을 가져오는 하위 쿼리가 포함 되어 있습니다. 또한 함께 수행 하는 경우 **제품 Stableadapter** 클래스의 **getproducts ()** 및 **GetProductsByCategoryID (*categoryID*)** 메서드를 이미 추가 했습니다.

- **제품 Stableadapter**

  - **Getproducts**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample10.sql)]
  - **GetProductsByCategoryID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample11.sql)]
  - **GetProductsBySupplierID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample12.sql)]
  - **Getproductid byproductid**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample13.sql)]
- **CategoriesTableAdapter**

  - **Getcategories**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample14.sql)]
  - **Getcategorybycategoryid**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample15.sql)]
- **SuppliersTableAdapter**

  - **Getsuppliers**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample16.sql)]
  - **GetSuppliersByCountry**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample17.sql)]
  - **GetSupplierBySupplierID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample18.sql)]
- **EmployeesTableAdapter**

  - **GetEmployees**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample19.sql)]
  - **GetEmployeesByManager**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample20.sql)]
  - **GetEmployeeByEmployeeID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample21.sql)]

[4 개의 Tableadapter가 추가 된 후 데이터 집합 디자이너를 ![합니다.](creating-a-data-access-layer-cs/_static/image84.png)](creating-a-data-access-layer-cs/_static/image83.png)

**그림 31**: 네 개의 Tableadapter가 추가 된 후의 데이터 집합 디자이너 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image85.png))

## <a name="adding-custom-code-to-the-dal"></a>DAL에 사용자 지정 코드 추가

형식화 된 데이터 집합에 추가 된 Tableadapter 및 Datatable는 XML 스키마 정의 파일 (**Northwind .xsd**)로 표시 됩니다. 솔루션 탐색기에서 **Northwind .xsd** 파일을 마우스 오른쪽 단추로 클릭 하 고 코드 보기를 선택 하 여이 스키마 정보를 볼 수 있습니다.

[Northwinds 형식화 된 데이터 집합에 대 한 XSD (XML 스키마 정의) 파일을 ![합니다.](creating-a-data-access-layer-cs/_static/image87.png)](creating-a-data-access-layer-cs/_static/image86.png)

**그림 32**: Northwinds 형식화 된 데이터 집합에 대 한 XSD (XML 스키마 정의) 파일 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image88.png))

이 스키마 정보는 런타임에 컴파일하거나 C# 런타임에 (필요한 경우) 실행 될 때 디자인 타임에 코드에서 또는 Visual Basic 코드로 변환 됩니다. 자동 생성 된 코드를 보려면 클래스 뷰로 이동 하 고 TableAdapter 또는 형식화 된 데이터 집합 클래스로 드릴 다운 합니다. 화면에 클래스 뷰 표시 되지 않으면 보기 메뉴로 이동 하 여 여기에서 선택 하거나 Ctrl + Shift + C를 누릅니다. 클래스 뷰에서 형식화 된 데이터 집합 및 TableAdapter 클래스의 속성, 메서드 및 이벤트를 볼 수 있습니다. 특정 메서드에 대 한 코드를 보려면 클래스 뷰에서 메서드 이름을 두 번 클릭 하거나 마우스 오른쪽 단추를 클릭 하 고 정의로 이동을 선택 합니다.

![클래스 뷰에서 정의로 이동을 선택 하 여 자동 생성 된 코드를 검사 합니다.](creating-a-data-access-layer-cs/_static/image89.png)

**그림 33**: 자동 생성 된 코드를 검사 하 여 클래스 뷰에서 정의로 이동을 선택 합니다.

자동 생성 된 코드는 상당한 시간 보호기가 될 수 있지만, 코드는 매우 일반적 이며 응용 프로그램의 고유한 요구 사항에 맞게 사용자 지정 해야 합니다. 그러나 자동 생성 된 코드를 확장할 경우 코드를 생성 하는 도구에서 사용자 지정을 "다시 생성" 하 고 덮어쓸 때를 결정할 수 있습니다. .NET 2.0의 새로운 partial 클래스 개념을 사용 하 여 여러 파일 간에 클래스를 분할 하는 것이 쉽습니다. 이를 통해 Visual Studio에서 사용자 지정을 덮어쓰는 걱정 없이 자동 생성 된 클래스에 고유한 메서드, 속성 및 이벤트를 추가할 수 있습니다.

DAL을 사용자 지정 하는 방법을 보여 주기 위해 **Getproducts ()** 메서드를 **SuppliersRow** 클래스에 추가 해 보겠습니다. **SuppliersRow** 클래스는 **Suppliers** 테이블의 단일 레코드를 나타냅니다. 각 공급 업체는 0 개 이상의 제품을 공급자에 게 제공 하므로 **Getproducts ()** 는 지정 된 공급자의 해당 제품을 반환 합니다. 이 작업을 수행 하려면 **SuppliersRow.cs** 이라는 **응용 프로그램\_코드** 폴더에 새 클래스 파일을 만들고 다음 코드를 추가 합니다.

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample22.cs)]

이 partial 클래스는 방금 정의한 **Getproducts ()** 메서드를 포함 하도록 **SuppliersRow** 클래스를 빌드할 때 컴파일러에 지시 합니다. 프로젝트를 빌드한 후 클래스 뷰으로 돌아가면 이제 **Getproducts ()** 가 **SuppliersRow**의 메서드로 나열 됩니다.

![GetProducts () 메서드는 이제 SuppliersRow 클래스의 일부입니다.](creating-a-data-access-layer-cs/_static/image90.png)

**그림 34**: **getproducts ()** 메서드는 이제 SuppliersRow 클래스의 일부입니다 **.**

이제 다음 코드와 같이 **Getproducts ()** 메서드를 사용 하 여 특정 공급자에 대 한 제품 집합을 열거할 수 있습니다.

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample23.html)]

이 데이터는 ASP에도 표시 될 수 있습니다. NET의 데이터 웹 컨트롤입니다. 다음 페이지에서는 두 개의 필드를 포함 하는 GridView 컨트롤을 사용 합니다.

- 각 공급자의 이름을 표시 하는 BoundField
- 각 공급자에 대해 **Getproducts ()** 메서드가 반환 하는 결과에 바인딩된 BulletedList 컨트롤을 포함 하는 templatefield로 변환입니다.

이후 자습서에서 이러한 마스터-세부 보고서를 표시 하는 방법을 살펴보겠습니다. 지금은이 예제에서는 **SuppliersRow** 클래스에 추가 된 사용자 지정 메서드를 사용 하는 방법을 보여 주도록 디자인 되었습니다.

SuppliersAndProducts

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample24.aspx)]

SuppliersAndProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample25.cs)]

[공급 업체의 회사 이름이 왼쪽 열에 표시 되 고 해당 제품을 오른쪽에 ![.](creating-a-data-access-layer-cs/_static/image92.png)](creating-a-data-access-layer-cs/_static/image91.png)

**그림 35**: 공급자의 회사 이름이 왼쪽 열에 표시 되 고 해당 제품은 오른쪽에 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](creating-a-data-access-layer-cs/_static/image93.png)).

## <a name="summary"></a>요약

웹 응용 프로그램을 빌드하는 경우 DAL을 만드는 첫 번째 단계 중 하나는 프레젠테이션 계층 만들기를 시작 하기 전에 발생 합니다. Visual Studio를 사용 하 여 형식화 된 데이터 집합을 기반으로 DAL을 만드는 작업은 코드 줄을 작성 하지 않고도 10-15 분 내에 수행할 수 있는 작업입니다. 앞으로 이동 하는 자습서는이 DAL을 기반으로 빌드됩니다. [다음 자습서](creating-a-business-logic-layer-cs.md) 에서는 여러 비즈니스 규칙을 정의 하 고 별도의 비즈니스 논리 계층에서 구현 하는 방법을 알아봅니다.

행복 한 프로그래밍

## <a name="further-reading"></a>추가 정보

이 자습서에서 설명 하는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [VS 2005 및 ASP.NET 2.0에서 강력한 형식의 Tableadapter 및 Datatable를 사용 하 여 DAL 빌드](https://weblogs.asp.net/scottgu/435498)
- [데이터 계층 구성 요소 디자인 및 계층을 통해 데이터 전달](https://msdn.microsoft.com/library/ms978496.aspx)
- [Visual Studio 2005 데이터 집합 디자이너를 사용 하 여 데이터 액세스 계층 빌드](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)
- [ASP.NET 2.0 응용 프로그램에서 구성 정보 암호화](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [TableAdapter 개요](https://msdn.microsoft.com/library/bz9tthwx.aspx)
- [형식화 된 데이터 집합 작업](https://msdn.microsoft.com/library/esbykkzb.aspx)
- [Visual Studio 2005 및 ASP.NET 2.0에서 강력한 형식의 데이터 액세스 사용](http://aspnet.4guysfromrolla.com/articles/020806-1.aspx)
- [TableAdapter 메서드를 확장 하는 방법](https://blogs.msdn.com/vbteam/archive/2005/05/04/ExtendingTableAdapters.aspx)
- [저장 프로시저에서 스칼라 데이터 검색](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>이 자습서에 포함 된 항목에 대 한 비디오 학습

- [ASP.NET 애플리케이션의 데이터 액세스 레이어](../../../videos/data-access/adonet-data-services/data-access-layers-in-aspnet-applications.md)
- [데이터 집합을 Datagrid에 수동으로 바인딩하는 방법](../../../videos/data-access/adonet-data-services/how-to-manually-bind-a-dataset-to-a-datagrid.md)
- [ASP 응용 프로그램에서 데이터 집합 및 필터를 사용 하는 방법](../../../videos/data-access/adonet-data-services/how-to-work-with-datasets-and-filters-from-an-asp-application.md)

## <a name="about-the-author"></a>작성자 정보

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)(7 개의 ASP/ASP. NET books 및 [4GuysFromRolla.com](http://www.4guysfromrolla.com)창립자)은 1998부터 Microsoft 웹 기술을 사용 하 여 작업 했습니다. Scott은 독립 컨설턴트, 강사 및 기록기로 작동 합니다. 최신 책은 [*24 시간 이내에 ASP.NET 2.0을 sams teach yourself*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)것입니다. mitchell@4GuysFromRolla.com에 도달할 수 있습니다 [.](mailto:mitchell@4GuysFromRolla.com) 또는 블로그를 통해 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)에서 찾을 수 있습니다.

## <a name="special-thanks-to"></a>특별히 감사 합니다.

이 자습서 시리즈는 많은 유용한 검토자가 검토 했습니다. 이 자습서에 대 한 잠재 고객 검토자는 녹색, Hilton Ron Esenow, Dennis Patterson이, Liz Shulok, Abel Gomez 및 Carlos Santos 였습니다. 예정 된 MSDN 문서를 검토 하는 데 관심이 있나요? 그렇다면mitchell@4GuysFromRolla.com에서 줄을 삭제 [합니다.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [다음](creating-a-business-logic-layer-cs.md)
