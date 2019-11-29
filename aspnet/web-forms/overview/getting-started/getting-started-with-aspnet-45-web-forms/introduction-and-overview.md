---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
title: ASP.NET 4.7 Web Forms 및 Visual Studio 2017 시작 | Microsoft Docs
author: Erikre
description: 이 단계별 자습서 시리즈는 ASP.NET 4.7 및를 사용 하 여 ASP.NET Web Forms 응용 프로그램 빌드에 대 한 기본 사항을 알려 줍니다 Microsoft Visual Studio
ms.author: riande
ms.date: 01/09/2019
ms.assetid: 9b96eaa1-8ef0-4338-a2e8-e0f970bfaf68
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview
msc.type: authoredcontent
ms.openlocfilehash: 52d5eb7abe4520ebdf6667d299d055fc7619a635
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615460"
---
# <a name="getting-started-with-aspnet-45-web-forms-and-visual-studio-2017"></a>ASP.NET 4.5 Web Forms 및 Visual Studio 2017 시작

[정문 장난감 샘플 프로젝트 (C#) 다운로드](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) 또는 [전자 서적 다운로드 (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

이 자습서 시리즈에서는 ASP.NET 4.5 및 Microsoft Visual Studio 2017를 사용 하 여 ASP.NET Web Forms 응용 프로그램을 빌드하는 방법을 보여 줍니다. 

## <a name="introduction"></a>소개

이 자습서 시리즈에서는 Visual Studio 2017 및 ASP.NET 4.5을 사용 하 여 ASP.NET Web Forms 응용 프로그램을 만드는 과정을 안내 합니다. Storefront 라는 응용 프로그램을 만듭니다 .이 응용 프로그램은 **온라인에서 항목** 을 판매 하는 간단한 웹 사이트입니다. 시리즈 중에는 새 ASP.NET 4.5 기능이 강조 표시 됩니다.

### <a name="target-audience"></a>대상 사용자

ASP.NET Web Forms를 처음 접하는 개발자는이 자습서 시리즈의 대상 사용자입니다.

다음 영역에 대 한 지식이 있어야 합니다.

- OOP (개체 지향 프로그래밍) 및 언어
- 웹 개발 (HTML, CSS, JavaScript)
- 관계형 데이터베이스
- N 계층 아키텍처

이러한 영역을 검토 하려면 다음 내용을 연구 하십시오.

- [Visual C# 시작](https://msdn.microsoft.com/library/a72418yk.aspx)
- [웹 개발](https://msdn.microsoft.com/beginner/bb308760.aspx), [HTML, CSS, JavaScript, SQL, PHP, JQuery](http://w3schools.com/)
- [관계형 데이터베이스](http://en.wikipedia.org/wiki/Relational_database)
- [다중 계층 아키텍처](http://en.wikipedia.org/wiki/Multitier_architecture)

### <a name="application-features"></a>응용 프로그램 기능

이 시리즈에서 제공 되는 ASP.NET Web Form 기능은 다음과 같습니다.

- 웹 응용 프로그램 프로젝트 (웹 사이트 프로젝트가 아님)
- Web Forms
- 마스터 페이지, 구성
- 부트스트랩
- Entity Framework Code First, LocalDB
- 요청 유효성 검사
- 강력한 형식의 데이터 컨트롤
- 모델 바인딩
- 데이터 주석
- 값 공급자
- SSL 및 OAuth
- ASP.NET Identity, 구성 및 권한 부여
- 조심 스럽게 유효성 검사
- 라우팅
- ASP.NET 오류 처리

### <a name="application-scenarios-and-tasks"></a>응용 프로그램 시나리오 및 작업

자습서 시리즈 작업은 다음과 같습니다.

- 새 프로젝트 만들기, 검토 및 실행
- 데이터베이스 구조 만들기
- 데이터베이스 초기화 및 시드
- 스타일, 그래픽 및 마스터 페이지를 사용 하 여 UI 사용자 지정
- 페이지 및 탐색 추가
- 메뉴 세부 정보 및 제품 데이터 표시
- 쇼핑 카트 만들기
- SSL 및 OAuth 지원 추가
- 지불 방법 추가
- 응용 프로그램에 관리자 역할 및 사용자 포함
- 특정 페이지 및 폴더에 대 한 액세스 제한
- 웹 응용 프로그램에 파일 업로드
- 입력 유효성 검사 구현
- 웹 응용 프로그램에 대 한 경로 등록
- 오류 처리 및 오류 로깅 구현

## <a name="overview"></a>개요

이 자습서 시리즈는 프로그래밍 개념에 익숙한 사용자를 대상으로 하지만 ASP.NET Web Forms를 처음 사용 하는 사용자를 위한 것입니다. ASP.NET Web Forms에 대해 잘 알고 있는 경우에도이 시리즈는 새로운 ASP.NET 4.5 기능에 대해 배우는 데 도움이 될 수 있습니다. 프로그래밍 개념 및 ASP.NET Web Forms에 익숙하지 않은 독자의 경우 ASP.NET 웹 사이트의 [시작](../../../index.md) 섹션에서 제공 하는 추가 Web Forms 자습서를 참조 하세요.

이 자습서 시리즈에 제공 된 ASP.NET 4.5에는 다음과 같은 기능이 포함 되어 있습니다.

- 많은 ASP.NET 프레임 워크 (Web Forms, MVC 및 Web API) [에 대 한 지원을](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#add) 제공 하는 프로젝트를 만드는 간단한 UI입니다.
- [부트스트랩](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap), 레이아웃, 테마 및 응답성이 뛰어난 디자인 프레임 워크입니다.
- [ASP.NET Identity](../../../../identity/index.md)모든 ASP.NET 프레임 워크에서 동일 하 게 작동 하며 IIS 이외의 웹 호스팅 소프트웨어와 작동 하는 새로운 ASP.NET 멤버 자격 시스템입니다.
- [Entity Framework 6](https://msdn.microsoft.com/data/ef.aspx)

  Entity Framework 업데이트를 사용 하 여 다음을 수행할 수 있습니다.
  - 데이터를 강력한 형식의 개체로 검색 및 조작
  - 비동기적으로 데이터 액세스
  - 일시적인 연결 오류 처리
  - 로그 SQL 문

전체 ASP.NET 4.5 기능 목록은 [ASP.NET 및 Web Tools Visual Studio 2013 릴리스 정보](../../../../visual-studio/overview/2013/release-notes.md)를 참조 하세요.

### <a name="the-wingtip-toys-sample-application"></a>정문 장난감 샘플 응용 프로그램

다음 스크린샷은이 자습서 시리즈에서 만든 ASP.NET Web Forms 응용 프로그램에서 가져온 것입니다. Visual Studio에서 응용 프로그램을 실행 하면 다음 웹 홈 페이지가 표시 됩니다.

![정문 장난감-기본 페이지](introduction-and-overview/_static/image1.png)

새 사용자로 등록 하거나 기존 사용자로 로그인 할 수 있습니다. 상단 탐색에는 데이터베이스에서 제품 범주와 해당 제품에 대 한 링크가 있습니다.

**제품**을 선택 하면 사용 가능한 모든 제품이 표시 됩니다. 

![정문 장난감-제품](introduction-and-overview/_static/image2.png)

특정 제품을 선택 하는 경우 제품 정보가 표시 됩니다.

![정문 장난감-제품 세부 정보](introduction-and-overview/_static/image3.png)

사용자는 Web Forms 템플릿 기본 기능을 사용 하 여 등록 하 고 로그인 할 수 있습니다. 이 자습서에서는 기존 Gmail 계정을 사용 하 여 로그인 하는 방법에 대해서도 설명 합니다. 또한 관리자 권한으로 로그인 하 여 데이터베이스에서 제품을 추가 하 고 제거할 수 있습니다.

![동 장난감-로그인](introduction-and-overview/_static/image4.png)

사용자로 로그인 한 후에는 쇼핑 카트에 제품을 추가 하 고 PayPal으로 체크 아웃할 수 있습니다. 샘플 응용 프로그램은 PayPal의 개발자 샌드박스에서 사용할 수 있도록 설계 되었습니다. 실제 money 트랜잭션은 발생 하지 않습니다.

![정문 장난감-쇼핑 카트](introduction-and-overview/_static/image5.png)

PayPal은 계정, 주문 및 지불 정보를 확인 합니다.

![동 장난감-PayPal](introduction-and-overview/_static/image6.png)

PayPal에서 반환 된 후 주문을 검토 하 고 완료할 수 있습니다.

![동 장난감 주문 검토](introduction-and-overview/_static/image7.png)

## <a name="prerequisites"></a>Prerequisites

시작 하기 전에 다음 소프트웨어가 컴퓨터에 설치 되어 있는지 확인 합니다.

- [Microsoft Visual Studio 2017 또는 Microsoft Visual Studio Community 2017](https://visualstudio.microsoft.com/downloads/).

.NET Framework 자동으로 설치 됩니다.

이 자습서 시리즈에서는 Microsoft Visual Studio Community 2017를 사용 합니다. 또는 Microsoft Visual Studio 2017를 사용 하 여이 자습서 시리즈를 완료할 수 있습니다.

Visual Studio에 대 한 다음 사항에 유의 하세요.

* Microsoft Visual Studio 2017 및 Microsoft Visual Studio Community 2017은이 자습서 시리즈 전체에서 *Visual Studio* 라고 합니다.

* Visual Studio 2017는 이미 설치 된 이전 버전 옆에 설치 됩니다. 이전 버전에서 만든 사이트는 Visual Studio 2017에서 열 수 있으며 이전 버전에서 계속 열 수 있습니다.

* 처음 Visual Studio를 시작할 때 *웹 개발* 설정을 선택 했다고 가정 합니다. 자세한 내용은 [방법: 웹 개발 환경 설정 선택](https://msdn.microsoft.com/library/ff521558.aspx)을 참조 하세요.

필수 구성 요소를 설치한 후이 자습서 시리즈에 제공 된 웹 프로젝트를 만들 준비가 되었습니다.

## <a name="download-the-sample-application"></a>샘플 응용 프로그램 다운로드

 언제 든 지 MSDN Samples 사이트에서 완성 된 샘플 응용 프로그램을 다운로드할 수 있습니다.

[ASP.NET 4.5 Web Forms 및 Visual Studio 2013 시작-동 장난감](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 

 이 다운로드에는 다음과 같은 항목이 있습니다.

- *WingtipToys* 폴더에 있는 샘플 응용 프로그램입니다.
- *WingtipToys* 폴더의 *WingtipToys* 폴더에서 샘플 응용 프로그램을 만드는 데 사용 되는 리소스입니다.

다운로드는 *.zip* 파일입니다. 이 자습서 시리즈에서 만든 완료 된 프로젝트를 보려면 .zip 파일에서 *C#* 폴더를 찾아서 선택 합니다. Visual Studio C# 프로젝트 작업에 사용 하는 폴더에 폴더를 저장 합니다. 기본적으로 Visual Studio 2017 projects 폴더는 다음과 같습니다.

<strong>C:\Users&#92;</strong>  <strong><em>&lt;username&gt;</em></strong> <strong>\source\repos</strong>

***C#*** 폴더 이름을 ***WingtipToys***로 바꿉니다.

> [!NOTE]
> 프로젝트 폴더에 이름이 *WingtipToys* 인 폴더가 이미 있는 경우 *C#* 폴더 이름을 *WingtipToys*로 바꾸기 전에 기존 폴더의 이름을 임시로 바꿉니다.

완료 된 프로젝트를 실행 하려면 *WingtipToys* 폴더를 열고 *WingtipToys* 파일을 두 번 클릭 합니다. Visual Studio 2017에서 프로젝트가 열립니다. 다음으로 **솔루션 탐색기** 에서 default.aspx 파일을 마우스 오른쪽 단추로 클릭 하 고 **브라우저에서 보기**를 *선택 합니다.*

## <a name="take-a-aspnet-web-forms-quiz-to-review-content"></a>ASP.NET Web Forms 퀴즈를 사용 하 여 콘텐츠 검토

자습서 시리즈를 완료 한 후 퀴즈를 수행 하 여 지식을 테스트 하 고 주요 개념을 보강 합니다. 각 질문은 설명 및 추가 지침에 대 한 링크를 제공 합니다.

* [ASP.NET Web Forms 퀴즈](https://blogs.msdn.microsoft.com/erikreitan/2016/01/08/asp-net-web-forms-quiz/) 

## <a name="tutorial-support-and-comments"></a>자습서 지원 및 주석

질문과 의견은 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013-정문 장난감](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 샘플 페이지에 포함 된 Q 및 섹션을 사용 하세요.

이 자습서 시리즈에 대 한 설명은 환영 합니다. 이 자습서 시리즈를 업데이트 한 후에는 향상 된 기능에 대 한 수정 또는 제안을 고려 하 여 모든 노력이 필요 합니다.

오류가 발생 하는 경우 문제를 해결 하는 방법에 대 한 설명이 없는 해당 오류 메시지가 혼란 스 러 울 수 있습니다. 도움말은 [ASP.NET 포럼](https://forums.asp.net/)을 확인할 수 있습니다. 또 다른 좋은 소스는 [ASP.NET 4.5 Web Forms 및 Visual Studio 2013-정문 장난감](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#) 샘플 페이지의 Q 및 섹션입니다. 

> [!div class="step-by-step"]
> [다음](create-the-project.md)
