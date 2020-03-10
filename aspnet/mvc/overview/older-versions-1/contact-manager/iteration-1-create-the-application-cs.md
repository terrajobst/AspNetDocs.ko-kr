---
uid: mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
title: '반복 #1 – 응용 프로그램 만들기 (C#) | Microsoft Docs'
author: microsoft
description: 첫 번째 반복에서는 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업 (만들기, 읽기, 업데이트 및 D ...)에 대 한 지원을 추가 합니다.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: db0f160b-901c-46d3-865e-7ab6cd4ed68d
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-1-create-the-application-cs
msc.type: authoredcontent
ms.openlocfilehash: d3a940308f21a4f87bf80249bd465e8812794f68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78470267"
---
# <a name="iteration-1--create-the-application-c"></a>반복 #1 – 응용 프로그램 만들기 (C#)

[Microsoft](https://github.com/microsoft) 에서

[코드 다운로드](iteration-1-create-the-application-cs/_static/contactmanager_1_cs1.zip)

> 첫 번째 반복에서는 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업 (만들기, 읽기, 업데이트 및 삭제 (CRUD))에 대 한 지원을 추가 합니다.

## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a>Contact Management ASP.NET MVC 응용 프로그램 빌드 (VB)

이 자습서 시리즈에서는 전체 연락처 관리 응용 프로그램을 처음부터 끝까지 빌드 합니다. 연락처 관리자 응용 프로그램을 사용 하면 연락처 정보 (이름, 전화 번호 및 전자 메일 주소)를 사용자 목록으로 저장할 수 있습니다.

여러 반복을 통해 응용 프로그램을 빌드합니다. 각 반복을 통해 응용 프로그램을 점진적으로 개선 합니다. 이 여러 반복 방법의 목표는 각 변경의 이유를 이해할 수 있게 하는 것입니다.

- 반복 #1-응용 프로그램을 만듭니다. 첫 번째 반복에서는 가장 간단한 방법으로 연락처 관리자를 만듭니다. 기본 데이터베이스 작업 (만들기, 읽기, 업데이트 및 삭제 (CRUD))에 대 한 지원을 추가 합니다.

- 반복 #2-응용 프로그램을 멋지게 만듭니다. 이 반복에서는 기본 ASP.NET MVC 뷰 마스터 페이지 및 css 스타일 시트를 수정 하 여 응용 프로그램의 모양을 개선 합니다.

- 반복 #3-양식 유효성 검사를 추가 합니다. 세 번째 반복에서는 기본 폼 유효성 검사를 추가 합니다. 사용자가 필요한 양식 필드를 완료 하지 않고 양식을 전송 하지 못하도록 합니다. 또한 전자 메일 주소 및 전화 번호의 유효성을 검사 합니다.

- 반복 #4-응용 프로그램이 느슨하게 결합 되도록 합니다. 이 네 번째 반복에서는 몇 가지 소프트웨어 디자인 패턴을 활용 하 여 연락처 관리자 응용 프로그램을 보다 쉽게 유지 관리 하 고 수정할 수 있습니다. 예를 들어 리포지토리 패턴 및 종속성 주입 패턴을 사용 하도록 응용 프로그램을 리팩터링 합니다.

- 반복 #5-단위 테스트를 만듭니다. 다섯 번째 반복에서는 단위 테스트를 추가 하 여 응용 프로그램을 더 쉽게 유지 관리 하 고 수정할 수 있도록 합니다. Microsoft는 데이터 모델 클래스를 모의 하 고 컨트롤러 및 유효성 검사 논리에 대 한 단위 테스트를 빌드 했습니다.

- 반복 #6-테스트 기반 개발을 사용 합니다. 이 여섯 번째 반복에서는 단위 테스트를 먼저 작성 하 고 단위 테스트에 대 한 코드를 작성 하 여 응용 프로그램에 새 기능을 추가 합니다. 이 반복에서는 연락처 그룹을 추가 합니다.

- 반복 #7-Ajax 기능을 추가 합니다. 일곱 번째 반복에서는 Ajax에 대 한 지원을 추가 하 여 응용 프로그램의 응답성과 성능을 향상 시킵니다.

## <a name="this-iteration"></a>이 반복

이 첫 번째 반복에서는 기본 응용 프로그램을 빌드합니다. 목표는 가능한 가장 빠르고 가장 간단한 방법으로 연락처 관리자를 빌드하는 것입니다. 이후 반복에서는 응용 프로그램의 디자인을 향상 시킵니다.

연락처 관리자 응용 프로그램은 기본 데이터베이스 기반 응용 프로그램입니다. 응용 프로그램을 사용 하 여 새 연락처를 만들고, 기존 연락처를 편집 하 고, 연락처를 삭제할 수 있습니다.

이 반복에서는 다음 단계를 완료 합니다.

1. ASP.NET MVC 응용 프로그램
2. 연락처를 저장 하는 데이터베이스 만들기
3. Microsoft Entity Framework를 사용 하 여 데이터베이스에 대 한 모델 클래스 생성
4. 컨트롤러 작업 및 보기를 만들어 데이터베이스의 모든 연락처를 나열할 수 있습니다.
5. 데이터베이스에서 새 연락처를 만들 수 있도록 하는 컨트롤러 작업 및 보기 만들기
6. 데이터베이스에서 기존 연락처를 편집할 수 있는 컨트롤러 작업 및 보기 만들기
7. 데이터베이스에서 기존 연락처를 삭제할 수 있는 컨트롤러 작업 및 보기 만들기

## <a name="software-prerequisites"></a>소프트웨어 필수 구성 요소

ASP.NET MVC 응용 프로그램에서 visual studio 2008 또는 Visual Web Developer 2008이 컴퓨터에 설치 되어 있어야 합니다 (Visual Web Developer는 visual Studio의 고급 기능을 모두 포함 하지 않는 visual Studio의 무료 버전). 다음 주소에서 Visual Studio 2008 또는 Visual Web Developer의 평가판을 다운로드할 수 있습니다.

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

> [!NOTE] 
> 
> Visual Web Developer를 사용 하는 ASP.NET MVC 응용 프로그램의 경우 Visual Web Developer 서비스 팩 1이 설치 되어 있어야 합니다. 서비스 팩 1을 사용 하지 않으면 웹 응용 프로그램 프로젝트를 만들 수 없습니다.

ASP.NET MVC 프레임 워크. ASP.NET MVC 프레임 워크는 다음 주소에서 다운로드할 수 있습니다.

[https://www.asp.net/mvc](../../../index.md)

이 자습서에서는 Microsoft Entity Framework를 사용 하 여 데이터베이스에 액세스 합니다. Entity Framework .NET Framework 3.5 서비스 팩 1에 포함 되어 있습니다. 다음 위치에서이 Service Pack를 다운로드할 수 있습니다.

[https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;d isplaylang = en](https://www.microsoft.com/downloads/details.aspx?familyid=ab99342f-5d1a-413d-8319-81da479ab0d7&amp;displaylang=en)

이러한 각 다운로드를 하나씩 수행 하는 대신 웹 플랫폼 설치 관리자 (웹 PI)를 활용할 수 있습니다. 다음 주소에서 웹 PI를 다운로드할 수 있습니다.

[https://www.asp.net/downloads/essential/](https://www.asp.net/downloads/essential)

## <a name="aspnet-mvc-project"></a>ASP.NET MVC 프로젝트

ASP.NET MVC 웹 응용 프로그램 프로젝트입니다. Visual Studio를 시작 하 고 메뉴 옵션 **파일, 새 프로젝트를**선택 합니다. **새 프로젝트** 대화 상자가 나타납니다 (그림 1 참조). **웹** 프로젝트 형식 및 **ASP.NET MVC 웹 응용 프로그램** 템플릿을 선택 합니다. 새 프로젝트의 이름을 새 프로젝트로 만들고 확인 *단추를 클릭* 합니다.

**새 프로젝트** 대화 상자의 오른쪽 위에 있는 드롭다운 목록에서 .NET Framework 3.5을 선택 했는지 확인 합니다. 그렇지 않으면 ASP.NET MVC 웹 응용 프로그램 템플릿이 표시 되지 않습니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image1.jpg)](iteration-1-create-the-application-cs/_static/image1.png)

**그림 01**: 새 프로젝트 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image2.png))

ASP.NET MVC 응용 프로그램, **단위 테스트 프로젝트 만들기** 대화 상자가 나타납니다. ASP.NET MVC 응용 프로그램을 만들 때이 대화 상자를 사용 하 여 단위 테스트 프로젝트를 만들어 솔루션에 추가 하도록 지정할 수 있습니다. 이 반복에서 단위 테스트를 빌드하지는 않지만 나중 반복에서 단위 테스트를 추가할 계획 이므로 **예, 단위 테스트 프로젝트 만들기** 옵션을 선택 해야 합니다. 새 ASP.NET MVC 프로젝트를 처음 만들 때 테스트 프로젝트를 추가 하는 것은 ASP.NET MVC 프로젝트를 만든 후 테스트 프로젝트를 추가 하는 것 보다 훨씬 쉽습니다.

> [!NOTE] 
> 
> Visual Web Developer는 테스트 프로젝트를 지원 하지 않기 때문에 Visual Web Developer를 사용 하는 경우 단위 테스트 프로젝트 만들기 대화 상자가 표시 되지 않습니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image2.jpg)](iteration-1-create-the-application-cs/_static/image3.png)

**그림 02**: 단위 테스트 프로젝트 만들기 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image4.png))

ASP.NET MVC 응용 프로그램이 Visual Studio 솔루션 탐색기 창에 표시 됩니다 (그림 3 참조). 솔루션 탐색기 창이 표시 되지 않으면 메뉴 옵션 **보기, 솔루션 탐색기를**선택 하 여이 창을 열 수 있습니다. 솔루션에는 ASP.NET MVC 프로젝트와 테스트 프로젝트의 두 프로젝트가 포함 되어 있습니다. ASP.NET MVC 프로젝트의 이름은입니다 .이 프로젝트는 테스트 프로젝트의 이름이입니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image3.jpg)](iteration-1-create-the-application-cs/_static/image5.png)

**그림 03**: 솔루션 탐색기 창 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image6.png))

## <a name="deleting-the-project-sample-files"></a>프로젝트 샘플 파일 삭제

ASP.NET MVC 프로젝트 템플릿에는 컨트롤러 및 뷰에 대 한 샘플 파일이 포함 되어 있습니다. 새 ASP.NET MVC 응용 프로그램을 만들기 전에 이러한 파일을 삭제 해야 합니다. 파일이 나 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **삭제**를 선택 하 여 솔루션 탐색기 창에서 파일과 폴더를 삭제할 수 있습니다.

ASP.NET MVC 프로젝트에서 다음 파일을 삭제 해야 합니다.

- \Controllers\HomeController.cs

- \Views\Home\About.aspx

- \Views\Home\Index.aspx

테스트 프로젝트에서 다음 파일을 삭제 해야 합니다.

\Controllers\HomeControllerTest.cs

## <a name="creating-the-database"></a>데이터베이스 만들기

연락처 관리자 응용 프로그램은 데이터베이스 기반 웹 응용 프로그램입니다. 데이터베이스를 사용 하 여 연락처 정보를 저장 합니다.

Microsoft SQL Server, Oracle, MySQL 및 IBM DB2 데이터베이스를 포함 하는 최신 데이터베이스를 포함 하는 ASP.NET MVC 프레임 워크입니다. 이 자습서에서는 Microsoft SQL Server 데이터베이스를 사용 합니다. Visual Studio를 설치 하면 Microsoft SQL Server 데이터베이스의 무료 버전인 Microsoft SQL Server Express를 설치할 수 있는 옵션이 제공 됩니다.

솔루션 탐색기 창에서 App\_Data 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 새 항목**메뉴 옵션을 선택 하 여 새 데이터베이스를 만듭니다. **새 항목 추가** 대화 상자에서 **데이터** 범주 및 **SQL Server 데이터베이스** 템플릿을 선택 합니다 (그림 4 참조). 새 데이터베이스의 이름을 같은 이름으로 만들고 확인 단추를 클릭 합니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image4.jpg)](iteration-1-create-the-application-cs/_static/image7.png)

**그림 04**: 새 Microsoft SQL Server Express 데이터베이스 만들기 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image8.png))

새 데이터베이스를 만들면 데이터베이스가 솔루션 탐색기 창의 App\_Data 폴더에 나타납니다. 두 번 클릭 하 여 서버 탐색기 창을 열고 데이터베이스에 연결 합니다.

> [!NOTE] 
> 
> Microsoft Visual Web Developer의 경우 서버 탐색기 창을 데이터베이스 탐색기 창 이라고 합니다.

서버 탐색기 창을 사용 하 여 데이터베이스 테이블, 뷰, 트리거 및 저장 프로시저와 같은 새 데이터베이스 개체를 만들 수 있습니다. Tables 폴더를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **새 테이블 추가**를 선택 합니다. 데이터베이스 테이블 디자이너 표시 됩니다 (그림 5 참조).

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image5.jpg)](iteration-1-create-the-application-cs/_static/image9.png)

**그림 05**: 데이터베이스 테이블 디자이너 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image10.png))

다음 열이 포함 된 테이블을 만들어야 합니다.

<a id="0.1_table01"></a>

| **열 이름** | **데이터 형식** | **Null 허용** |
| --- | --- | --- |
| Id | int | false |
| FirstName | nvarchar(50) | false |
| LastName | nvarchar(50) | false |
| Phone | nvarchar(50) | false |
| Email | nvarchar(255) | false |

첫 번째 열인 Id 열은 특수 합니다. Id 열을 id 열과 기본 키 열로 표시 해야 합니다. 열이 열 속성을 확장 하 고 (그림 6의 아래쪽을 확인) Id 사양 속성으로 스크롤하면 열이 Id 열 임을 나타낼 수 있습니다. **(Id)** 속성을 **Yes**값으로 설정 합니다.

열을 선택 하 고 키 아이콘이 있는 단추를 클릭 하 여 열을 기본 키 열로 표시 합니다. 열이 기본 키 열로 표시 된 후에는 열 옆에 키 아이콘이 표시 됩니다 (그림 6 참조).

테이블 만들기를 완료 한 후 저장 단추 (플로피 아이콘이 있는 단추)를 클릭 하 여 새 테이블을 저장 합니다. 새 테이블에 이름 *연락처*를 지정 합니다.

연락처 데이터베이스 테이블 만들기를 완료 한 후에는 테이블에 일부 레코드를 추가 해야 합니다. 서버 탐색기 창에서 Contacts 테이블을 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **테이블 데이터 표시**를 선택 합니다. 표시 되는 표에 연락처를 하나 이상 입력 합니다.

## <a name="creating-the-data-model"></a>데이터 모델 만들기

ASP.NET MVC 응용 프로그램은 모델, 뷰 및 컨트롤러로 구성 됩니다. 먼저 이전 섹션에서 만든 Contacts 테이블을 나타내는 모델 클래스를 만듭니다.

이 자습서에서는 Microsoft Entity Framework를 사용 하 여 데이터베이스에서 자동으로 모델 클래스를 생성 합니다.

> [!NOTE] 
> 
> ASP.NET MVC 프레임 워크는 어떤 방식으로든 Microsoft Entity Framework 연결 되지 않습니다. NHibernate 절전 모드, LINQ to SQL 또는 ADO.NET를 포함 하 여 대체 데이터베이스 액세스 기술과 함께 ASP.NET MVC를 사용할 수 있습니다.

데이터 모델 클래스를 만들려면 다음 단계를 수행 합니다.

1. 솔루션 탐색기 창에서 모델 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 새 항목을**차례로 선택 합니다. **새 항목 추가** 대화 상자가 나타납니다 (그림 6 참조).
2. **데이터** 범주 및 **ADO.NET 엔터티 데이터 모델** 템플릿을 선택 합니다. 데이터 모델의 이름을 선택 하 고 **추가** 단추를 클릭 *합니다.* 엔터티 데이터 모델 마법사가 나타납니다 (그림 7 참조).
3. **모델 콘텐츠 선택** 단계에서 **데이터베이스에서 생성** 을 선택 합니다 (그림 7 참조).
4. **데이터 연결 선택** 단계에서 동료 managerdb .mdf 데이터베이스를 선택 하 고 엔터티 연결 설정에 대 한 이름 (그림 8 참조 *)을 입력* 합니다.
5. **데이터베이스 개체 선택** 단계에서 테이블 레이블 확인란을 선택 합니다 (그림 9 참조). 데이터 모델에는 데이터베이스에 포함 된 모든 테이블이 포함 됩니다 (하나의 연락처만 테이블). 네임 스페이스 *모델*을 입력 합니다. 마침 단추를 클릭 하 여 마법사를 완료 합니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image6.jpg)](iteration-1-create-the-application-cs/_static/image11.png)

**그림 06**: 새 항목 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image12.png))

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image7.jpg)](iteration-1-create-the-application-cs/_static/image13.png)

**그림 07**: 모델 콘텐츠 선택 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image14.png))

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image8.jpg)](iteration-1-create-the-application-cs/_static/image15.png)

**그림 08**: 데이터 연결 선택 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image16.png))

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image9.jpg)](iteration-1-create-the-application-cs/_static/image17.png)

**그림 09**: 데이터베이스 개체 선택 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image18.png))

엔터티 데이터 모델 마법사를 완료 하면 엔터티 데이터 모델 디자이너가 나타납니다. 모델링 되는 각 테이블에 해당 하는 클래스가 디자이너에 표시 됩니다. 연락처 라는 클래스가 하나씩 표시 되어야 합니다.

엔터티 데이터 모델 마법사는 데이터베이스 테이블 이름을 기반으로 클래스 이름을 생성 합니다. 거의 항상 마법사에서 생성 된 클래스의 이름을 변경 해야 합니다. 디자이너에서 Contacts 클래스를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **이름 바꾸기**를 선택 합니다. 클래스의 이름을 연락처 (복수형)에서 연락처 (단수형)로 변경 합니다. 클래스 이름을 변경한 후에는 클래스가 그림 10과 같이 표시 됩니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image10.jpg)](iteration-1-create-the-application-cs/_static/image19.png)

**그림 10**: Contact 클래스 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image20.png))

이 시점에서 데이터베이스 모델을 만들었습니다. Contact 클래스를 사용 하 여 데이터베이스의 특정 연락처 레코드를 나타낼 수 있습니다.

## <a name="creating-the-home-controller"></a>홈 컨트롤러 만들기

다음 단계는 홈 컨트롤러를 만드는 것입니다. Home 컨트롤러는 ASP.NET MVC 응용 프로그램에서 호출 되는 기본 컨트롤러입니다.

솔루션 탐색기 창에서 Controllers 폴더를 마우스 오른쪽 단추로 클릭 하 고 **추가, 컨트롤러** 메뉴 옵션을 선택 하 여 홈 컨트롤러 클래스를 만듭니다 (그림 11 참조). **만들기, 업데이트 및 세부 정보 시나리오에 대 한 작업 메서드 추가**라는 확인란을 확인 합니다. **추가** 단추를 클릭 하기 전에이 확인란을 선택 했는지 확인 합니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image11.jpg)](iteration-1-create-the-application-cs/_static/image21.png)

**그림 11**: 홈 컨트롤러 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image22.png))

홈 컨트롤러를 만들 때 목록 1에 클래스를 가져옵니다.

**목록 1-Controllers\ homecontroller.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample1.cs)]

## <a name="listing-the-contacts"></a>연락처 나열

Contact 데이터베이스 테이블의 레코드를 표시 하려면 Index () 동작과 인덱스 뷰를 만들어야 합니다.

Home 컨트롤러에 이미 Index () 작업이 있습니다. 목록 2 처럼 보이도록이 메서드를 수정 해야 합니다.

**목록 2-Controllers\ homecontroller.cs**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample2.cs)]

목록 2의 홈 컨트롤러 클래스는 \_엔터티 라는 개인 필드를 포함 하 고 있습니다. 엔터티 \_필드는 데이터 모델의 엔터티를 나타냅니다. \_엔터티 필드를 사용 하 여 데이터베이스와 통신 합니다.

Index () 메서드는 Contacts 데이터베이스 테이블의 모든 연락처를 나타내는 뷰를 반환 합니다. 엔터티 \_식입니다. 연락처 Set. ToList ()는 연락처 목록을 제네릭 목록으로 반환 합니다.

이제 인덱스 컨트롤러를 만들었으므로 인덱스 뷰를 만들어야 합니다. 인덱스 뷰를 만들기 전에 **빌드, 솔루션 빌드**메뉴 옵션을 선택 하 여 응용 프로그램을 컴파일합니다. **뷰 추가** 대화 상자에 모델 클래스 목록을 표시 하려면 뷰를 추가 하기 전에 항상 프로젝트를 컴파일해야 합니다.

Index () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **뷰 추가** 를 선택 하 여 인덱스 뷰를 만듭니다 (그림 12 참조). 이 메뉴 옵션을 선택 하면 **보기 추가** 대화 상자가 열립니다 (그림 13 참조).

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image12.jpg)](iteration-1-create-the-application-cs/_static/image23.png)

**그림 12**: 인덱스 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image24.png))

**보기 추가** 대화 상자에서 **강력한 형식의 뷰 만들기**확인란을 선택 합니다. 데이터 보기 클래스. 연락처 및 콘텐츠 보기 목록을 선택 합니다. 이러한 옵션을 선택 하면 연락처 레코드 목록이 표시 되는 보기가 생성 됩니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image13.jpg)](iteration-1-create-the-application-cs/_static/image25.png)

**그림 13**: 보기 추가 대화 상자 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image26.png))

**추가** 단추를 클릭 하면 목록 3의 인덱스 뷰가 생성 됩니다. 파일의 맨 위에 표시 되는 &lt;% @ Page%&gt; 지시어를 확인 합니다. 인덱스 뷰는&lt;IEnumerable&lt;팀&gt;&gt; 클래스에서 상속 됩니다. 즉, 뷰의 모델 클래스는 연락처 엔터티 목록을 나타냅니다.

인덱스 뷰의 본문은 모델 클래스로 표시 되는 각 연락처를 반복 하는 foreach 루프를 포함 합니다. Contact 클래스의 각 속성 값은 HTML 테이블에 표시 됩니다.

**목록 3-Views\Home\Index.aspx (수정 되지 않음)**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample3.aspx)]

인덱스 뷰를 한 번 수정 해야 합니다. 자세히 보기를 만들지 않으므로 세부 정보 링크를 제거할 수 있습니다. 인덱스 뷰에서 다음 코드를 찾아 제거 합니다.

{id = 항목입니다. Id})%&gt;

인덱스 뷰를 수정한 후에는 연락처 관리자 응용 프로그램을 실행할 수 있습니다. 디버그, 디버깅 시작 메뉴 옵션을 선택 하거나 F5 키를 누르기만 하면 됩니다. 처음으로 응용 프로그램을 실행할 때 그림 14의 대화 상자가 표시 됩니다. **디버깅을 사용 하도록 web.config 파일을 수정** 합니다. 옵션을 선택 하 고 확인 단추를 클릭 합니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image14.jpg)](iteration-1-create-the-application-cs/_static/image27.png)

**그림 14**: 디버깅 사용 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image28.png))

인덱스 뷰가 기본적으로 반환 됩니다. 이 보기에는 연락처 데이터베이스 테이블의 모든 데이터가 나열 됩니다 (그림 15 참조).

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image15.jpg)](iteration-1-create-the-application-cs/_static/image29.png)

**그림 15**: 인덱스 뷰 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image30.png))

인덱스 뷰에는 보기의 맨 아래에 새로 만들기 라는 레이블이 포함 되어 있습니다. 다음 섹션에서는 새 연락처를 만드는 방법에 대해 알아봅니다.

## <a name="creating-new-contacts"></a>새 연락처 만들기

사용자가 새 연락처를 만들 수 있도록 하려면 두 개의 Create () 작업을 홈 컨트롤러에 추가 해야 합니다. 새 연락처를 만들기 위한 HTML 양식을 반환 하는 Create () 작업을 하나 만들어야 합니다. 새 연락처의 실제 데이터베이스 삽입을 수행 하는 두 번째 Create () 작업을 만들어야 합니다.

홈 컨트롤러에 추가 해야 하는 새 만들기 () 메서드는 목록 4에 포함 되어 있습니다.

**목록 4-Controllers\ homecontroller.cs (Create 메서드 포함)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample4.cs)]

첫 번째 Create () 메서드는 http GET을 사용 하 여 호출할 수 있으며 두 번째 Create () 메서드는 HTTP POST에 의해서만 호출 될 수 있습니다. 즉, 두 번째 Create () 메서드는 HTML 폼을 게시 하는 경우에만 호출할 수 있습니다. 첫 번째 Create () 메서드는 새 연락처를 만들기 위한 HTML 양식이 포함 된 뷰를 반환 합니다. 두 번째 Create () 메서드는 데이터베이스에 새 연락처를 추가 하는 것이 훨씬 더 흥미롭습니다.

Contact 클래스의 인스턴스를 수락 하도록 두 번째 Create () 메서드가 수정 되었습니다. HTML 양식에서 게시 된 양식 값은 ASP.NET MVC 프레임 워크에서 자동으로이 Contact 클래스에 바인딩됩니다. HTML 만들기 폼의 각 양식 필드는 Contact 매개 변수의 속성에 할당 됩니다.

Contact 매개 변수는 [Bind] 특성으로 데코 레이트 됩니다. [Bind] 특성은 바인딩에서 연락처 Id 속성을 제외 하는 데 사용 됩니다. Id 속성은 id 속성을 나타내므로 Id 속성을 설정 하는 것이 좋습니다.

Create () 메서드의 본문에서 Entity Framework는 새 연락처를 데이터베이스에 삽입 하는 데 사용 됩니다. 새 연락처는 기존 연락처 집합에 추가 되 고, SaveChanges () 메서드를 호출 하 여 이러한 변경 내용을 기본 데이터베이스로 다시 푸시합니다.

두 개의 Create () 메서드 중 하나를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 **추가 보기** 를 선택 하 여 새 연락처를 만들기 위한 HTML 양식을 생성할 수 있습니다 (그림 16 참조).

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image16.jpg)](iteration-1-create-the-application-cs/_static/image31.png)

**그림 16**: Create view 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image32.png))

**보기 추가** 대화 상자에서 콘텐츠 보기에 대 한 **연락처 관리자** 클래스 및 **만들기** 옵션을 선택 합니다 (그림 17 참조). **추가** 단추를 클릭 하면 Create view가 자동으로 생성 됩니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image17.jpg)](iteration-1-create-the-application-cs/_static/image33.png)

**그림 17**: 페이지 분해[보기 (전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image34.png))

만들기 뷰는 Contact 클래스의 각 속성에 대 한 양식 필드를 포함 합니다. 만들기 보기에 대 한 코드는 목록 5에 포함 되어 있습니다.

**목록 5-Views\Home\Create.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample5.aspx)]

Create () 메서드를 수정 하 고 만들기 보기를 추가한 후 Contact manager 응용 프로그램을 실행 하 고 새 연락처를 만들 수 있습니다. 인덱스 뷰에 표시 되는 **새로** 만들기 링크를 클릭 하 여 만들기 뷰로 이동 합니다. 그림 18에 보기가 표시 되어야 합니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image18.jpg)](iteration-1-create-the-application-cs/_static/image35.png)

**그림 18**: Create view ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image36.png))

## <a name="editing-contacts"></a>연락처 편집

연락처 레코드를 편집 하는 기능을 추가 하는 것은 새 연락처 레코드를 만들기 위한 기능을 추가 하는 것과 매우 비슷합니다. 먼저 홈 컨트롤러 클래스에 두 개의 새 편집 메서드를 추가 해야 합니다. 이러한 새 Edit () 메서드는 목록 6에 포함 되어 있습니다.

**목록 6-Controllers\ homecontroller.cs (Edit 메서드 포함)**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample6.cs)]

첫 번째 Edit () 메서드는 HTTP GET 작업에 의해 호출 됩니다. Id 매개 변수는 편집 중인 연락처 레코드의 Id를 나타내는이 메서드에 전달 됩니다. Entity Framework는 Id와 일치 하는 연락처를 검색 하는 데 사용 됩니다. 레코드 편집을 위한 HTML 양식이 포함 된 뷰가 반환 됩니다.

Second Edit () 메서드는 데이터베이스에 대 한 실제 업데이트를 수행 합니다. 이 메서드는 Contact 클래스의 인스턴스를 매개 변수로 받아들입니다. ASP.NET MVC 프레임 워크는 편집 폼의 양식 필드를이 클래스에 자동으로 바인딩합니다. 연락처를 편집할 때 [Bind] 특성을 포함 하지 않습니다 (Id 속성의 값이 필요 함).

Entity Framework은 수정 된 연락처를 데이터베이스에 저장 하는 데 사용 됩니다. 먼저 데이터베이스에서 원래 연락처를 검색 해야 합니다. 그런 다음 Entity Framework ApplyPropertyChanges () 메서드를 호출 하 여 연락처에 대 한 변경 내용을 기록 합니다. 마지막으로, Entity Framework SaveChanges () 메서드를 호출 하 여 기본 데이터베이스에 대 한 변경 내용을 유지 합니다.

편집 () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 뷰 추가를 선택 하 여 편집 양식이 포함 된 뷰를 생성할 수 있습니다. 보기 추가 대화 상자에서 **연락처 관리자** 클래스와 **편집** 보기 콘텐츠를 선택 합니다 (그림 19 참조).

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image19.jpg)](iteration-1-create-the-application-cs/_static/image37.png)

**그림 19**: 편집 뷰 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image38.png))

추가 단추를 클릭 하면 새 편집 뷰가 자동으로 생성 됩니다. 생성 된 HTML 폼에는 Contact 클래스의 각 속성에 해당 하는 필드가 포함 되어 있습니다 (목록 7 참조).

**목록 7-Views\Home\Edit.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample7.aspx)]

## <a name="deleting-contacts"></a>연락처 삭제

연락처를 삭제 하려면 홈 컨트롤러 클래스에 두 개의 Delete () 작업을 추가 해야 합니다. 첫 번째 Delete () 작업은 삭제 확인 폼을 표시 합니다. 두 번째 Delete () 작업은 실제 삭제를 수행 합니다.

> [!NOTE] 
> 
> 나중에 반복 #7에서 한 단계 Ajax 삭제를 지원 하도록 연락처 관리자를 수정 합니다.

두 개의 새 Delete () 메서드는 목록 8에 포함 되어 있습니다.

**Controllers\ homecontroller.cs (Delete 메서드) 목록**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample8.cs)]

첫 번째 Delete () 메서드는 데이터베이스에서 연락처 레코드를 삭제 하는 확인 양식을 반환 합니다 (Figure20 참조). Second Delete () 메서드는 데이터베이스에 대해 실제 삭제 작업을 수행 합니다. 데이터베이스에서 원래 연락처를 검색 한 후에는 Entity Framework DeleteObject () 및 SaveChanges () 메서드를 호출 하 여 데이터베이스 삭제를 수행 합니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image20.jpg)](iteration-1-create-the-application-cs/_static/image39.png)

**그림 20**: 삭제 확인 보기 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image40.png))

연락처 레코드를 삭제 하기 위한 링크가 포함 되도록 인덱스 보기를 수정 해야 합니다 (그림 21 참조). 편집 링크를 포함 하는 동일한 테이블 셀에 다음 코드를 추가 해야 합니다.

Html.actionlink ({id = 항목)입니다. Id})%&gt;

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image21.jpg)](iteration-1-create-the-application-cs/_static/image41.png)

**그림 21**: 편집 링크가 있는 인덱스 뷰 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image42.png))

다음으로 삭제 확인 보기를 만들어야 합니다. Home controller 클래스에서 Delete () 메서드를 마우스 오른쪽 단추로 클릭 하 고 메뉴 옵션 뷰 추가를 선택 합니다. 보기 추가 대화 상자가 나타납니다 (그림 22 참조).

목록 보기, 만들기 및 편집의 경우와 달리 보기 추가 대화 상자에는 삭제 보기를 만드는 옵션이 포함 되어 있지 않습니다. 대신, **연락처** 데이터 클래스와 **빈** 뷰 콘텐츠를 선택 합니다. 빈 콘텐츠 보기 옵션을 선택 하면 보기를 만드는 데 도움이 됩니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image22.jpg)](iteration-1-create-the-application-cs/_static/image43.png)

**그림 22**: 삭제 확인 보기 추가 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image44.png))

삭제 보기의 내용은 목록 9에 포함 되어 있습니다. 이 보기에는 특정 연락처를 삭제 해야 하는지 여부를 확인 하는 양식이 있습니다 (그림 21 참조).

**목록 9-Views\Home\Delete.aspx**

[!code-aspx[Main](iteration-1-create-the-application-cs/samples/sample9.aspx)]

## <a name="changing-the-name-of-the-default-controller"></a>기본 컨트롤러의 이름 변경

연락처를 사용 하기 위한 컨트롤러 클래스의 이름이 HomeController 클래스 라는 것을 확인할 수 있습니다. 컨트롤러의 이름을 "로 지정 해야 합니다.

이 문제는 쉽게 해결할 수 있습니다. 먼저 홈 컨트롤러의 이름을 리팩터링 해야 합니다. Visual Studio Code 편집기에서 HomeController 클래스를 열고 클래스 이름을 마우스 오른쪽 단추로 클릭 한 다음 **리팩터링, 이름 바꾸기**메뉴 옵션을 선택 합니다. 이 메뉴 옵션을 선택 하면 이름 바꾸기 대화 상자가 열립니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image23.jpg)](iteration-1-create-the-application-cs/_static/image45.png)

**그림 23**: 컨트롤러 이름 리팩터링 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image46.png))

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image24.jpg)](iteration-1-create-the-application-cs/_static/image47.png)

**그림 24**: 이름 바꾸기 대화 상자 사용 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image48.png))

컨트롤러 클래스의 이름을 바꾸는 경우에도 Visual Studio는 Views 폴더에서 폴더 이름을 업데이트 합니다. Visual Studio에서 \Views\Home 폴더의 이름을 \Views\Contact 폴더로 바꿉니다.

이러한 변경을 수행한 후에는 응용 프로그램에 더 이상 홈 컨트롤러가 없습니다. 응용 프로그램을 실행 하면 그림 25의 오류 페이지가 표시 됩니다.

[새 프로젝트 대화 상자 ![](iteration-1-create-the-application-cs/_static/image25.jpg)](iteration-1-create-the-application-cs/_static/image49.png)

**그림 25**: 기본 컨트롤러 없음 ([전체 크기 이미지를 보려면 클릭](iteration-1-create-the-application-cs/_static/image50.png))

Home 컨트롤러 대신 연락처 컨트롤러를 사용 하려면 global.asax 파일에서 기본 경로를 업데이트 해야 합니다. Global.asax 파일을 열고 기본 경로에 사용 되는 기본 컨트롤러를 수정 합니다 (목록 10 참조).

**10-Global.asax.cs 나열**

[!code-csharp[Main](iteration-1-create-the-application-cs/samples/sample10.cs)]

이러한 변경을 수행한 후에는 연락처 관리자가 올바르게 실행 됩니다. 이제 기본 컨트롤러로 Contact controller 클래스를 사용 합니다.

## <a name="summary"></a>요약

이 첫 번째 반복에서는 가장 빠른 방법으로 기본 연락처 관리자 응용 프로그램을 만들었습니다. Visual Studio를 활용 하 여 컨트롤러 및 뷰에 대 한 초기 코드를 자동으로 생성 했습니다. 또한 Entity Framework를 활용 하 여 데이터베이스 모델 클래스를 자동으로 생성 했습니다.

현재 연락처 관리자 응용 프로그램을 사용 하 여 연락처 레코드를 나열 하 고, 만들고, 편집 하 고, 삭제할 수 있습니다. 즉, 데이터베이스 기반 웹 응용 프로그램에 필요한 모든 기본 데이터베이스 작업을 수행할 수 있습니다.

아쉽게도 응용 프로그램에 몇 가지 문제가 있습니다. 첫째,이를 허용 하는 것이 가장 좋은 응용 프로그램은 주저. 디자인 작업이 필요 합니다. 다음 반복에서는 기본 보기 마스터 페이지와 css 스타일 시트를 변경 하 여 응용 프로그램의 모양을 개선 하는 방법을 살펴보겠습니다.

둘째, 폼 유효성 검사를 구현 하지 않았습니다. 예를 들어 양식 필드에 대 한 값을 입력 하지 않고 연락처 만들기 양식을 전송 하지 못하도록 하는 것은 없습니다. 또한 잘못 된 전화 번호와 전자 메일 주소를 입력할 수 있습니다. 반복 #3에서 폼 유효성 검사 문제를 해결 하기 시작 합니다.

마지막으로, 가장 중요 한 것은 연락처 관리자 응용 프로그램의 현재 반복을 쉽게 수정 하거나 유지 관리할 수 없다는 것입니다. 예를 들어 데이터베이스 액세스 논리는 컨트롤러 작업에 구운 됩니다. 이는 컨트롤러를 수정 하지 않고 데이터 액세스 코드를 수정할 수 없음을 의미 합니다. 이후 반복에서는 연락처 관리자의 복원 력을 높이기 위해 구현할 수 있는 소프트웨어 디자인 패턴을 살펴봅니다.

> [!div class="step-by-step"]
> [다음](iteration-2-make-the-application-look-nice-cs.md)
