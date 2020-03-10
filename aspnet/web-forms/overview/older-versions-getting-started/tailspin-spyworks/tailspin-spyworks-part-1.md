---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: '1 부: 파일 > 새 프로젝트 | Microsoft Docs'
author: JoeStagner
description: 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 1 부에서는 개요 및 파일/새 프로젝트를 다룹니다.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78516539"
---
# <a name="part-1-file--new-project"></a>1 부: 파일 > 새 프로젝트

만든 사람 [Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks는 .NET 플랫폼을 위한 강력 하 고 확장 가능한 응용 프로그램을 만드는 방법을 보여 줍니다. ASP.NET 4의 새로운 기능을 사용 하 여 쇼핑, 구매 및 관리를 포함 한 온라인 상점을 구축 하는 방법을 보여 줍니다.
> 
> 이 자습서 시리즈에서는 Tailspin Spyworks 샘플 응용 프로그램을 빌드하는 데 필요한 모든 단계에 대해 자세히 설명 합니다. 1 부에서는 개요 및 파일/새 프로젝트를 다룹니다.

## <a id="_Toc260221666"></a>설명은

이 자습서는 ASP.NET WebForms에 대 한 소개입니다. Microsoft는 느리게 시작 될 예정 이므로, 초급 수준의 웹 개발 환경을 사용할 수 있습니다.

빌드할 응용 프로그램은 간단한 온라인 상점입니다.

![](tailspin-spyworks-part-1/_static/image1.jpg)

방문자는 범주별로 제품을 찾아볼 수 있습니다.

![](tailspin-spyworks-part-1/_static/image2.jpg)

단일 제품을 보고 카트에 추가할 수 있습니다.

![](tailspin-spyworks-part-1/_static/image3.jpg)

해당 카트를 검토 하 여 더 이상 원하지 않는 항목을 제거할 수 있습니다.

![](tailspin-spyworks-part-1/_static/image4.jpg)

체크 아웃을 계속 하면 다음을 수행 하 라는 메시지가 표시 됩니다.

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

주문 후에는 간단한 확인 화면이 표시 됩니다.

![](tailspin-spyworks-part-1/_static/image7.jpg)

먼저 Visual Studio 2010에서 새로운 ASP.NET WebForms 프로젝트를 만들고 기능을 증분 추가 하 여 완전 한 기능을 갖춘 응용 프로그램을 만듭니다. 이 과정에서 데이터베이스 액세스, 목록 및 그리드 보기, 데이터 업데이트 페이지, 데이터 유효성 검사, 일관성 있는 페이지 레이아웃에 대 한 마스터 페이지 사용, AJAX, 유효성 검사, 사용자 멤버 자격 등을 다룹니다.

단계별로 수행 하거나 완료 된 응용 프로그램을 다운로드할 수 있습니다 [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)

[https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/)에서 visual Studio 2010 또는 무료 Visual Web Developer 2010 중 하나를 사용할 수 있습니다. 응용 프로그램을 빌드하기 위해 SQL Server 또는 무료 SQL Server Express를 사용 하 여 데이터베이스를 호스트할 수 있습니다.

## <a id="_Toc260221667"></a>파일/새 프로젝트

먼저 Visual Studio의 파일 메뉴에서 새 프로젝트를 선택 합니다. 그러면 새 프로젝트 대화 상자가 나타납니다.

![](tailspin-spyworks-part-1/_static/image8.jpg)

왼쪽의 시각적 개체 C# /웹 템플릿 그룹을 선택 하 고 가운데 열에서 "ASP.NET 웹 응용 프로그램" 템플릿을 선택 합니다. 프로젝트 이름을 TailspinSpyworks로 하 고 확인 단추를 누릅니다.

![](tailspin-spyworks-part-1/_static/image9.jpg)

그러면 프로젝트가 생성 됩니다. 오른쪽의 솔루션 탐색기에 응용 프로그램에 포함 된 폴더를 살펴보겠습니다.

![](tailspin-spyworks-part-1/_static/image10.jpg)

빈 솔루션은 완전히 비어 있지 않으며 기본 폴더 구조를 추가 합니다.

![](tailspin-spyworks-part-1/_static/image1.png)

ASP.NET 4 기본 프로젝트 템플릿에 의해 구현 된 규칙을 확인 합니다.

- "Account" 폴더는 ASP에 대 한 기본 사용자 인터페이스를 구현 합니다. NET의 멤버 자격 하위 시스템입니다.
- "Scripts" 폴더는 클라이언트 쪽 JavaScript 파일의 리포지토리 역할을 하며, 기본적으로 핵심 jQuery 파일을 사용할 수 있게 됩니다.
- "스타일" 폴더는 웹 사이트 시각적 개체 (CSS 스타일 시트)를 구성 하는 데 사용 됩니다.

F5 키를 눌러 응용 프로그램을 실행 하 고 default.aspx 페이지를 렌더링 하는 경우 다음이 표시 됩니다.

![](tailspin-spyworks-part-1/_static/image11.jpg)

첫 번째 응용 프로그램 향상은 기본 WebForms 템플릿에서 스타일 .css 파일을 Tailspin Spyworks 응용 프로그램에 대해 원하는 시각적 asthetics을 렌더링 하는 CSS 클래스 및 관련 이미지 파일로 바꾸는 것입니다.

그러면 default.aspx 페이지가 다음과 같이 렌더링 됩니다.

![](tailspin-spyworks-part-1/_static/image12.jpg)

페이지의 오른쪽 위에 있는 이미지 링크와 마스터 페이지에 추가 된 메뉴 항목이 있는지 확인 합니다. "로그인" 및 "계정" 링크만이 존재 하는 페이지 (기본 템플릿에 의해 생성 됨)와 응용 프로그램을 빌드할 때 구현할 나머지 페이지를 가리킵니다.

마스터 페이지를 스타일 디렉터리로 재배치할 수도 있습니다. 이는 기본 설정 이지만 나중에 응용 프로그램을 "skinable" 하도록 결정 하는 경우 더 쉽게 수행할 수 있습니다.

이 작업을 수행한 후에는 기본 ASP.NET WebForms 페이지에 의해 생성 된 모든 .aspx 파일의 마스터 페이지 참조를 변경 해야 합니다.

> [!div class="step-by-step"]
> [다음](tailspin-spyworks-part-2.md)
