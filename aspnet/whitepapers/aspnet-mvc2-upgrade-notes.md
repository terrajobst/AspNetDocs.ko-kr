---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: ASP.NET MVC 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드 | Microsoft Docs
author: rick-anderson
description: 이 문서에서는 ASP.NET MVC 1.0 응용 프로그램을 사용 하 여 수동으로 및 마법사를 사용 하 여 ASP.NET MVC 2로 업그레이드 하는 방법을 설명 합니다. 이 문서는 d ...에도 제공 됩니다.
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78517301"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a>ASP.NET MVC 1.0 애플리케이션을 ASP.NET MVC 2로 업그레이드

> 이 문서에서는 ASP.NET MVC 1.0 응용 프로그램을 사용 하 여 수동으로 및 마법사를 사용 하 여 ASP.NET MVC 2로 업그레이드 하는 방법을 설명 합니다. 이 문서도 [다운로드할](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf) 수 있습니다.

## <a name="introduction"></a>소개

ASP.NET MVC 2는 동일한 서버에 ASP.NET MVC 1.0와 나란히 설치할 수 있습니다. 이를 통해 응용 프로그램 개발자는 ASP.NET MVC 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드할 시기를 유연 하 게 선택할 수 있습니다.

Visual Studio 2010에는 Visual Studio 2008로 빌드된 기존 ASP.NET MVC 1.0 프로젝트를 ASP.NET MVC 2로 업그레이드 하는 마법사가 포함 되어 있습니다. 업그레이드 마법사는 Visual Studio 2010에서 ASP.NET MVC 1.0 프로젝트를 열어 시작 합니다.

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a>ASP.NET MVC 1.0에 대 한 업그레이드 마법사 (Visual Studio 2008 SP1)

Visual Studio 2008 s p 1에서 ASP.NET MVC 1.0 응용 프로그램을 ASP.NET MVC 2로 업그레이드 하려면 지원 되지 않는 (지원 되지 않는) MvcAppConverter 응용 프로그램을 사용 합니다. 다음 URL에서이 응용 프로그램을 다운로드할 수 있습니다.

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a>ASP.NET MVC 1.0 프로젝트 수동 업그레이드

기존 ASP.NET MVC 1.0 응용 프로그램을 버전 2로 수동으로 업그레이드 하려면 다음 단계를 수행 합니다.

1. 기존 프로젝트의 백업을 만듭니다.
2. 텍스트 편집기에서 프로젝트 파일 (.csproj 또는 .vbproj 파일 확장명을 가진 파일)을 열고 ProjectTypeGuid 요소를 찾습니다. 해당 요소의 값으로 GUID {603c0e0b-db56-11dc-be95-000d561079b0}을 {F85E285D-A4E0-4152-9332-AB1D724D3325}로 바꿉니다. 완료 되 면 해당 요소의 값은 다음과 같아야 합니다. 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. 웹 응용 프로그램 루트 폴더에서 web.config 파일을 편집 합니다. System.web, Version = 1.0.0.0을 검색 하 고 모든 인스턴스를 System.web. Mvc, Version = 2.0.0.0으로 바꿉니다.
4. Views 폴더에 있는 web.config 파일에 대해 이전 단계를 반복 합니다.
5. Visual Studio를 사용 하 여 프로젝트를 열고 **솔루션 탐색기**에서 **참조** 노드를 확장 합니다. 버전 1.0 어셈블리를 가리키는 System.web에 대 한 참조를 삭제 합니다. System.web에 대 한 참조를 추가 합니다 (v 2.0.0.0).
6. 구성을 섹션의 응용 프로그램 루트에 있는 web.config 파일에 다음 bindingRedirect 요소를 추가 합니다.   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. 비어 있는 새 ASP.NET MVC 2 응용 프로그램을 만듭니다. 새 응용 프로그램의 Scripts 폴더에 있는 파일을 기존 응용 프로그램의 Scripts 폴더에 복사 합니다.
8. 기존 applicationâ s CSS 파일을 사이트 .css 파일의 CSS 스타일 정의로 업데이트 합니다.
9. 응용 프로그램을 컴파일하고 실행 합니다. 오류가 발생 하는 경우 [ASP.NET MVC 2의 새로운 기능](https://go.microsoft.com/fwlink/?LinkID=185038) 페이지의 주요 변경 내용 섹션을 참조 하세요.
